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
# <a name="manage-azure-data-lake-analytics-using-python"></a>Gerenciar o Azure Data Lake Analytics usando o Python

## <a name="python-versions"></a>Versões do Python

* Use uma versão de 64 bits do Python.
* Você pode usar a distribuição de Python padrão Olá encontrada em  **[Python.org downloads](https://www.python.org/downloads/)**. 
* Muitos desenvolvedores consideram conveniente toouse Olá  **[distribuição Anaconda Python](https://www.continuum.io/downloads)**.  
* Este artigo foi escrito com Python versão 3.6 de distribuição padrão de Python Olá

## <a name="install-azure-python-sdk"></a>Instalar o SDK do Python do Azure

Instale Olá módulos a seguir:

* Olá **azure-mgmt-resource** módulo inclui outros módulos do Azure para o Active Directory, etc.
* Olá **repositório azure-mgmt-datalake** módulo inclui operações de gerenciamento de conta de repositório Azure Data Lake hello.
* Olá **repositório do azure-datalake** módulo inclui operações de sistema de arquivos do repositório Azure Data Lake hello. 
* Olá **análise do azure-datalake** módulo inclui operações de análise do Azure Data Lake hello. 

Primeiro, verifique se você tem hello mais recente `pip` executando Olá comando a seguir:

```
python -m pip install --upgrade pip
```

Este documento foi escrito usando `pip version 9.0.1`.

Use Olá seguinte `pip` comandos tooinstall módulos Olá Olá de linha de comando:

```
pip install azure-mgmt-resource
pip install azure-datalake-store
pip install azure-mgmt-datalake-store
pip install azure-mgmt-datalake-analytics
```

## <a name="create-a-new-python-script"></a>Criar um novo script do Python

Cole Olá código a seguir para o script hello:

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

Execute este script tooverify que Olá módulos podem ser importados.

## <a name="authentication"></a>Autenticação

### <a name="interactive-user-authentication-with-a-pop-up"></a>Autenticação de usuário interativo com um pop-up

Não há suporte para esse método.

### <a name="interactive-user-authentication-with-a-device-code"></a>Autenticação de usuário interativo com um código de dispositivo

```python
user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
password = getpass.getpass()
credentials = UserPassCredentials(user, password)
```

### <a name="noninteractive-authentication-with-spi-and-a-secret"></a>Autenticação não interativa com SPI e um segredo

```python
credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')
```

### <a name="noninteractive-authentication-with-api-and-a-certificate"></a>Autenticação não interativa com API e um certificado

Não há suporte para esse método.

## <a name="common-script-variables"></a>Variáveis do script comum

Essas variáveis são usadas nos exemplos de saudação.

```python
subid= '<Azure Subscription ID>'
rg = '<Azure Resource Group Name>'
location = '<Location>' # i.e. 'eastus2'
adls = '<Azure Data Lake Store Account Name>'
adla = '<Azure Data Lake Analytics Account Name>'
```

## <a name="create-hello-clients"></a>Criar clientes Olá

```python
resourceClient = ResourceManagementClient(credentials, subid)
adlaAcctClient = DataLakeAnalyticsAccountManagementClient(credentials, subid)
adlaJobClient = DataLakeAnalyticsJobManagementClient( credentials, 'azuredatalakeanalytics.net')
```

## <a name="create-an-azure-resource-group"></a>Criar um grupo de recursos do Azure

```python
armGroupResult = resourceClient.resource_groups.create_or_update( rg, ResourceGroup( location=location ) )
```

## <a name="create-data-lake-analytics-account"></a>Criar conta da Análise Data Lake

Primeiro, crie uma conta de repositório.

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
Em seguida, crie uma conta do ADLA que usará o repositório.

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

## <a name="submit-a-job"></a>Enviar um trabalho

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

## <a name="wait-for-a-job-tooend"></a>Aguarde até que um trabalho tooend

```python
jobResult = adlaJobClient.job.get(adla, jobId)
while(jobResult.state != JobState.ended):
    print('Job is not yet done, waiting for 3 seconds. Current state: ' + jobResult.state.value)
    time.sleep(3)
    jobResult = adlaJobClient.job.get(adla, jobId)

print ('Job finished with result: ' + jobResult.result.value)
```

## <a name="list-pipelines-and-recurrences"></a>Listar pipelines e recorrências
Dependendo se os trabalhos tiverem metadados de pipeline ou de recorrência anexados, você poderá listar os pipelines e as recorrências.

```python
pipelines = adlaJobClient.pipeline.list(adla)
for p in pipelines:
    print('Pipeline: ' + p.name + ' ' + p.pipelineId)

recurrences = adlaJobClient.recurrence.list(adla)
for r in recurrences:
    print('Recurrence: ' + r.name + ' ' + r.recurrenceId)
```

## <a name="manage-compute-policies"></a>Gerenciar políticas de computação

Olá DataLakeAnalyticsAccountManagementClient fornece métodos para gerenciar Olá computação políticas para uma conta da análise Data Lake.

### <a name="list-compute-policies"></a>Listar políticas de computação

saudação de código a seguir recupera uma lista de políticas de computação para uma conta da análise Data Lake.

```python
policies = adlaAccountClient.computePolicies.listByAccount(rg, adla)
for p in policies:
    print('Name: ' + p.name + 'Type: ' + p.objectType + 'Max AUs / job: ' + p.maxDegreeOfParallelismPerJob + 'Min priority / job: ' + p.minPriorityPerJob)
```

### <a name="create-a-new-compute-policy"></a>Criar uma nova política de computação

saudação de código a seguir cria uma nova política de computação para uma conta da análise Data Lake, configuração Olá máximo Austrália disponível toohello especificado too50 de usuário e too250 de prioridade do trabalho mínimo hello.

```python
userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde"
newPolicyParams = ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250)
adlaAccountClient.computePolicies.createOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams)
```

## <a name="next-steps"></a>Próximas etapas

- toosee Olá mesmo tutorial usando outras ferramentas, clique em seletores de guia Olá na parte superior de saudação da página de saudação.
- toolearn U-SQL, consulte [começar com a linguagem da análise Azure Data Lake U-SQL](data-lake-analytics-u-sql-get-started.md).
- Para obter as tarefas de gerenciamento, confira [Gerenciar o Azure Data Lake Analytics usando o portal do Azure](data-lake-analytics-manage-use-portal.md).

