---
title: "aaaManage análise Azure Data Lake com Python | Microsoft Docs"
description: 'Saiba como toouse Python toocreate um Data Lake armazenam conta e enviar trabalhos. '
services: data-lake-analytics
documentationcenter: 
author: matt1883
manager: jhubbard
editor: cgronlun
ms.assetid: d4213a19-4d0f-49c9-871c-9cd6ed7cf731
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: saveenr
ms.openlocfilehash: 3c0fff155db7c4fd4e84c2562816995eb156be16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-python"></a><span data-ttu-id="520f3-103">Gerenciar o Azure Data Lake Analytics usando o Python</span><span class="sxs-lookup"><span data-stu-id="520f3-103">Manage Azure Data Lake Analytics using Python</span></span>

## <a name="python-versions"></a><span data-ttu-id="520f3-104">Versões do Python</span><span class="sxs-lookup"><span data-stu-id="520f3-104">Python versions</span></span>

* <span data-ttu-id="520f3-105">Use uma versão de 64 bits do Python.</span><span class="sxs-lookup"><span data-stu-id="520f3-105">Use a 64-bit version of Python.</span></span>
* <span data-ttu-id="520f3-106">Você pode usar a distribuição de Python padrão Olá encontrada em  **[Python.org downloads](https://www.python.org/downloads/)**.</span><span class="sxs-lookup"><span data-stu-id="520f3-106">You can use hello standard Python distribution found at **[Python.org downloads](https://www.python.org/downloads/)**.</span></span> 
* <span data-ttu-id="520f3-107">Muitos desenvolvedores consideram conveniente toouse Olá  **[distribuição Anaconda Python](https://www.continuum.io/downloads)**.</span><span class="sxs-lookup"><span data-stu-id="520f3-107">Many developers find it convenient toouse hello **[Anaconda Python distribution](https://www.continuum.io/downloads)**.</span></span>  
* <span data-ttu-id="520f3-108">Este artigo foi escrito com Python versão 3.6 de distribuição padrão de Python Olá</span><span class="sxs-lookup"><span data-stu-id="520f3-108">This article was written using Python version 3.6 from hello standard Python distribution</span></span>

## <a name="install-azure-python-sdk"></a><span data-ttu-id="520f3-109">Instalar o SDK do Python do Azure</span><span class="sxs-lookup"><span data-stu-id="520f3-109">Install Azure Python SDK</span></span>

<span data-ttu-id="520f3-110">Instale Olá módulos a seguir:</span><span class="sxs-lookup"><span data-stu-id="520f3-110">Install hello following modules:</span></span>

* <span data-ttu-id="520f3-111">Olá **azure-mgmt-resource** módulo inclui outros módulos do Azure para o Active Directory, etc.</span><span class="sxs-lookup"><span data-stu-id="520f3-111">hello **azure-mgmt-resource** module includes other Azure modules for Active Directory, etc.</span></span>
* <span data-ttu-id="520f3-112">Olá **repositório azure-mgmt-datalake** módulo inclui operações de gerenciamento de conta de repositório Azure Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="520f3-112">hello **azure-mgmt-datalake-store** module includes hello Azure Data Lake Store account management operations.</span></span>
* <span data-ttu-id="520f3-113">Olá **repositório do azure-datalake** módulo inclui operações de sistema de arquivos do repositório Azure Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="520f3-113">hello **azure-datalake-store** module includes hello Azure Data Lake Store filesystem operations.</span></span> 
* <span data-ttu-id="520f3-114">Olá **análise do azure-datalake** módulo inclui operações de análise do Azure Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="520f3-114">hello **azure-datalake-analytics** module includes hello Azure Data Lake Analytics operations.</span></span> 

<span data-ttu-id="520f3-115">Primeiro, verifique se você tem hello mais recente `pip` executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="520f3-115">First, ensure you have hello latest `pip` by running hello following command:</span></span>

```
python -m pip install --upgrade pip
```

<span data-ttu-id="520f3-116">Este documento foi escrito usando `pip version 9.0.1`.</span><span class="sxs-lookup"><span data-stu-id="520f3-116">This document was written using `pip version 9.0.1`.</span></span>

<span data-ttu-id="520f3-117">Use Olá seguinte `pip` comandos tooinstall módulos Olá Olá de linha de comando:</span><span class="sxs-lookup"><span data-stu-id="520f3-117">Use hello following `pip` commands tooinstall hello modules from hello commandline:</span></span>

```
pip install azure-mgmt-resource
pip install azure-datalake-store
pip install azure-mgmt-datalake-store
pip install azure-mgmt-datalake-analytics
```

## <a name="create-a-new-python-script"></a><span data-ttu-id="520f3-118">Criar um novo script do Python</span><span class="sxs-lookup"><span data-stu-id="520f3-118">Create a new Python script</span></span>

<span data-ttu-id="520f3-119">Cole Olá código a seguir para o script hello:</span><span class="sxs-lookup"><span data-stu-id="520f3-119">Paste hello following code into hello script:</span></span>

```python
## Use this only for Azure AD service-to-service authentication
#from azure.common.credentials import ServicePrincipalCredentials

## Use this only for Azure AD end-user authentication
#from azure.common.credentials import UserPassCredentials

## Required for Azure Resource Manager
from azure.mgmt.resource.resources import ResourceManagementClient
from azure.mgmt.resource.resources.models import ResourceGroup

## Required for Azure Data Lake Store account management
from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
from azure.mgmt.datalake.store.models import DataLakeStoreAccount

## Required for Azure Data Lake Store filesystem management
from azure.datalake.store import core, lib, multithread

## Required for Azure Data Lake Analytics account management
from azure.mgmt.datalake.analytics.account import DataLakeAnalyticsAccountManagementClient
from azure.mgmt.datalake.analytics.account.models import DataLakeAnalyticsAccount, DataLakeStoreAccountInfo

## Required for Azure Data Lake Analytics job management
from azure.mgmt.datalake.analytics.job import DataLakeAnalyticsJobManagementClient
from azure.mgmt.datalake.analytics.job.models import JobInformation, JobState, USqlJobProperties

## Required for Azure Data Lake Analytics catalog management
from azure.mgmt.datalake.analytics.catalog import DataLakeAnalyticsCatalogManagementClient

## Use these as needed for your application
import logging, getpass, pprint, uuid, time
```

<span data-ttu-id="520f3-120">Execute este script tooverify que Olá módulos podem ser importados.</span><span class="sxs-lookup"><span data-stu-id="520f3-120">Run this script tooverify that hello modules can be imported.</span></span>

## <a name="authentication"></a><span data-ttu-id="520f3-121">Autenticação</span><span class="sxs-lookup"><span data-stu-id="520f3-121">Authentication</span></span>

### <a name="interactive-user-authentication-with-a-pop-up"></a><span data-ttu-id="520f3-122">Autenticação de usuário interativo com um pop-up</span><span class="sxs-lookup"><span data-stu-id="520f3-122">Interactive user authentication with a pop-up</span></span>

<span data-ttu-id="520f3-123">Não há suporte para esse método.</span><span class="sxs-lookup"><span data-stu-id="520f3-123">This method is not supported.</span></span>

### <a name="interactive-user-authentication-with-a-device-code"></a><span data-ttu-id="520f3-124">Autenticação de usuário interativo com um código de dispositivo</span><span class="sxs-lookup"><span data-stu-id="520f3-124">Interactive user authentication with a device code</span></span>

```python
user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
password = getpass.getpass()
credentials = UserPassCredentials(user, password)
```

### <a name="noninteractive-authentication-with-spi-and-a-secret"></a><span data-ttu-id="520f3-125">Autenticação não interativa com SPI e um segredo</span><span class="sxs-lookup"><span data-stu-id="520f3-125">Noninteractive authentication with SPI and a secret</span></span>

```python
credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')
```

### <a name="noninteractive-authentication-with-api-and-a-certificate"></a><span data-ttu-id="520f3-126">Autenticação não interativa com API e um certificado</span><span class="sxs-lookup"><span data-stu-id="520f3-126">Noninteractive authentication with API and a certificate</span></span>

<span data-ttu-id="520f3-127">Não há suporte para esse método.</span><span class="sxs-lookup"><span data-stu-id="520f3-127">This method is not supported.</span></span>

## <a name="common-script-variables"></a><span data-ttu-id="520f3-128">Variáveis do script comum</span><span class="sxs-lookup"><span data-stu-id="520f3-128">Common script variables</span></span>

<span data-ttu-id="520f3-129">Essas variáveis são usadas nos exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="520f3-129">These variables are used in hello samples.</span></span>

```python
subid= '<Azure Subscription ID>'
rg = '<Azure Resource Group Name>'
location = '<Location>' # i.e. 'eastus2'
adls = '<Azure Data Lake Store Account Name>'
adla = '<Azure Data Lake Analytics Account Name>'
```

## <a name="create-hello-clients"></a><span data-ttu-id="520f3-130">Criar clientes Olá</span><span class="sxs-lookup"><span data-stu-id="520f3-130">Create hello clients</span></span>

```python
resourceClient = ResourceManagementClient(credentials, subid)
adlaAcctClient = DataLakeAnalyticsAccountManagementClient(credentials, subid)
adlaJobClient = DataLakeAnalyticsJobManagementClient( credentials, 'azuredatalakeanalytics.net')
```

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="520f3-131">Criar um grupo de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="520f3-131">Create an Azure Resource Group</span></span>

```python
armGroupResult = resourceClient.resource_groups.create_or_update( rg, ResourceGroup( location=location ) )
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="520f3-132">Criar conta da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="520f3-132">Create Data Lake Analytics account</span></span>

<span data-ttu-id="520f3-133">Primeiro, crie uma conta de repositório.</span><span class="sxs-lookup"><span data-stu-id="520f3-133">First create a store account.</span></span>

```python
adlaAcctResult = adlaAcctClient.account.create(
    rg,
    adla,
    DataLakeAnalyticsAccount(
        location=location,
        default_data_lake_store_account=adls,
        data_lake_store_accounts=[DataLakeStoreAccountInfo(name=adls)]
    )
).wait()
```
<span data-ttu-id="520f3-134">Em seguida, crie uma conta do ADLA que usará o repositório.</span><span class="sxs-lookup"><span data-stu-id="520f3-134">Then create an ADLA account that uses that store.</span></span>

```python
adlaAcctResult = adlaAcctClient.account.create(
    rg,
    adla,
    DataLakeAnalyticsAccount(
        location=location,
        default_data_lake_store_account=adls,
        data_lake_store_accounts=[DataLakeStoreAccountInfo(name=adls)]
    )
).wait()
```

## <a name="submit-a-job"></a><span data-ttu-id="520f3-135">Enviar um trabalho</span><span class="sxs-lookup"><span data-stu-id="520f3-135">Submit a job</span></span>

```python
script = """
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
"""

jobId = str(uuid.uuid4())
jobResult = adlaJobClient.job.create(
    adla,
    jobId,
    JobInformation(
        name='Sample Job',
        type='USql',
        properties=USqlJobProperties(script=script)
    )
)
```

## <a name="wait-for-a-job-tooend"></a><span data-ttu-id="520f3-136">Aguarde até que um trabalho tooend</span><span class="sxs-lookup"><span data-stu-id="520f3-136">Wait for a job tooend</span></span>

```python
jobResult = adlaJobClient.job.get(adla, jobId)
while(jobResult.state != JobState.ended):
    print('Job is not yet done, waiting for 3 seconds. Current state: ' + jobResult.state.value)
    time.sleep(3)
    jobResult = adlaJobClient.job.get(adla, jobId)

print ('Job finished with result: ' + jobResult.result.value)
```

## <a name="list-pipelines-and-recurrences"></a><span data-ttu-id="520f3-137">Listar pipelines e recorrências</span><span class="sxs-lookup"><span data-stu-id="520f3-137">List pipelines and recurrences</span></span>
<span data-ttu-id="520f3-138">Dependendo se os trabalhos tiverem metadados de pipeline ou de recorrência anexados, você poderá listar os pipelines e as recorrências.</span><span class="sxs-lookup"><span data-stu-id="520f3-138">Depending whether your jobs have pipeline or recurrence metadata attached, you can list pipelines and recurrences.</span></span>

```python
pipelines = adlaJobClient.pipeline.list(adla)
for p in pipelines:
    print('Pipeline: ' + p.name + ' ' + p.pipelineId)

recurrences = adlaJobClient.recurrence.list(adla)
for r in recurrences:
    print('Recurrence: ' + r.name + ' ' + r.recurrenceId)
```

## <a name="manage-compute-policies"></a><span data-ttu-id="520f3-139">Gerenciar políticas de computação</span><span class="sxs-lookup"><span data-stu-id="520f3-139">Manage compute policies</span></span>

<span data-ttu-id="520f3-140">Olá DataLakeAnalyticsAccountManagementClient fornece métodos para gerenciar Olá computação políticas para uma conta da análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="520f3-140">hello DataLakeAnalyticsAccountManagementClient object provides methods for managing hello compute policies for a Data Lake Analytics account.</span></span>

### <a name="list-compute-policies"></a><span data-ttu-id="520f3-141">Listar políticas de computação</span><span class="sxs-lookup"><span data-stu-id="520f3-141">List compute policies</span></span>

<span data-ttu-id="520f3-142">saudação de código a seguir recupera uma lista de políticas de computação para uma conta da análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="520f3-142">hello following code retrieves a list of compute policies for a Data Lake Analytics account.</span></span>

```python
policies = adlaAccountClient.computePolicies.listByAccount(rg, adla)
for p in policies:
    print('Name: ' + p.name + 'Type: ' + p.objectType + 'Max AUs / job: ' + p.maxDegreeOfParallelismPerJob + 'Min priority / job: ' + p.minPriorityPerJob)
```

### <a name="create-a-new-compute-policy"></a><span data-ttu-id="520f3-143">Criar uma nova política de computação</span><span class="sxs-lookup"><span data-stu-id="520f3-143">Create a new compute policy</span></span>

<span data-ttu-id="520f3-144">saudação de código a seguir cria uma nova política de computação para uma conta da análise Data Lake, configuração Olá máximo Austrália disponível toohello especificado too50 de usuário e too250 de prioridade do trabalho mínimo hello.</span><span class="sxs-lookup"><span data-stu-id="520f3-144">hello following code creates a new compute policy for a Data Lake Analytics account, setting hello maximum AUs available toohello specified user too50, and hello minimum job priority too250.</span></span>

```python
userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde"
newPolicyParams = ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250)
adlaAccountClient.computePolicies.createOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams)
```

## <a name="next-steps"></a><span data-ttu-id="520f3-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="520f3-145">Next steps</span></span>

- <span data-ttu-id="520f3-146">toosee Olá mesmo tutorial usando outras ferramentas, clique em seletores de guia Olá na parte superior de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="520f3-146">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>
- <span data-ttu-id="520f3-147">toolearn U-SQL, consulte [começar com a linguagem da análise Azure Data Lake U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="520f3-147">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
- <span data-ttu-id="520f3-148">Para obter as tarefas de gerenciamento, confira [Gerenciar o Azure Data Lake Analytics usando o portal do Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="520f3-148">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>

