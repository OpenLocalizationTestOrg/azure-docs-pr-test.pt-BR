---
title: Mover dados de armazenamentos de dados ODBC | Microsoft Docs
description: Saiba mais sobre como mover dados de armazenamentos de dados ODBC usando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ad70a598-c031-4339-a883-c6125403cb76
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: 269d9802ca4a6a16dbf9021929fe21104cb431f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a><span data-ttu-id="1a703-103">Mover dados de armazenamentos de dados ODBC usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1a703-103">Move data From ODBC data stores using Azure Data Factory</span></span>
<span data-ttu-id="1a703-104">Este artigo explica como usar a Atividade de Cópia no Azure Data Factory para mover dados de um repositório de dados ODBC.</span><span class="sxs-lookup"><span data-stu-id="1a703-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises ODBC data store.</span></span> <span data-ttu-id="1a703-105">Ele se baseia no artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md), que apresenta uma visão geral da movimentação de dados com a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="1a703-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="1a703-106">Você pode copiar dados de um repositório de dados ODBC para qualquer repositório de dados de coletor com suporte.</span><span class="sxs-lookup"><span data-stu-id="1a703-106">You can copy data from an ODBC data store to any supported sink data store.</span></span> <span data-ttu-id="1a703-107">Para obter uma lista de repositórios de dados com suporte como coletores da atividade de cópia, confira a tabela [Repositórios de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="1a703-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="1a703-108">Atualmente, o data factory dá suporte apenas à movimentação de dados de um repositório de dados ODBC para outros repositórios de dados, mas não à movimentação de dados de outros repositórios de dados para um repositório de dados ODBC.</span><span class="sxs-lookup"><span data-stu-id="1a703-108">Data factory currently supports only moving data from an ODBC data store to other data stores, but not for moving data from other data stores to an ODBC data store.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="1a703-109">Habilitando a conectividade</span><span class="sxs-lookup"><span data-stu-id="1a703-109">Enabling connectivity</span></span>
<span data-ttu-id="1a703-110">O serviço Data Factory dá suporte à conexão com fontes ODBC locais usando o Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="1a703-110">Data Factory service supports connecting to on-premises ODBC sources using the Data Management Gateway.</span></span> <span data-ttu-id="1a703-111">Consulte o artigo [movendo dados entre pontos locais e na nuvem](data-factory-move-data-between-onprem-and-cloud.md) para saber mais sobre o Gateway de gerenciamento de dados e obter instruções passo a passo de como configurar o gateway.</span><span class="sxs-lookup"><span data-stu-id="1a703-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="1a703-112">Use o gateway para se conectar a um repositório de dados ODBC, mesmo se ele estiver hospedado em uma VM IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a703-112">Use the gateway to connect to an ODBC data store even if it is hosted in an Azure IaaS VM.</span></span>

<span data-ttu-id="1a703-113">Você pode instalar o gateway no mesmo computador local ou na VM do Azure como o repositório de dados ODBC.</span><span class="sxs-lookup"><span data-stu-id="1a703-113">You can install the gateway on the same on-premises machine or the Azure VM as the ODBC data store.</span></span> <span data-ttu-id="1a703-114">No entanto, recomendamos que você instale o gateway em uma máquina separada/VM IaaS Azure para evitar a contenção de recursos e para melhorar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="1a703-114">However, we recommend that you install the gateway on a separate machine/Azure IaaS VM to avoid resource contention and for better performance.</span></span> <span data-ttu-id="1a703-115">Quando você instalar o gateway em um computador separado, o computador deverá ser capaz de acessar o computador com o armazenamento de dados ODBC.</span><span class="sxs-lookup"><span data-stu-id="1a703-115">When you install the gateway on a separate machine, the machine should be able to access the machine with the ODBC data store.</span></span>

<span data-ttu-id="1a703-116">Além do Gateway de Gerenciamento de Dados, você também precisa instalar o driver ODBC para o armazenamento de dados no computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="1a703-116">Apart from the Data Management Gateway, you also need to install the ODBC driver for the data store on the gateway machine.</span></span>

> [!NOTE]
> <span data-ttu-id="1a703-117">Consulte [Solucionar problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para ver dicas sobre como solucionar os problemas relacionados à conexão/gateway.</span><span class="sxs-lookup"><span data-stu-id="1a703-117">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="1a703-118">Introdução</span><span class="sxs-lookup"><span data-stu-id="1a703-118">Getting started</span></span>
<span data-ttu-id="1a703-119">Você pode criar um pipeline com uma atividade de cópia que mova dados de um repositório de dados ODBC usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="1a703-119">You can create a pipeline with a copy activity that moves data from an ODBC data store by using different tools/APIs.</span></span>

<span data-ttu-id="1a703-120">A maneira mais fácil de criar um pipeline é usar o **Assistente de Cópia**.</span><span class="sxs-lookup"><span data-stu-id="1a703-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="1a703-121">Confira [Tutorial: Criar um pipeline usando o Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md) para ver um breve passo a passo sobre como criar um pipeline usando o Assistente de cópia de dados.</span><span class="sxs-lookup"><span data-stu-id="1a703-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="1a703-122">Você também pode usar as seguintes ferramentas para criar um pipeline: **Portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="1a703-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="1a703-123">Confira o [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo sobre a criação de um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="1a703-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="1a703-124">Ao usar as ferramentas ou APIs, você executa as seguintes etapas para criar um pipeline que move dados de um armazenamento de dados de origem para um armazenamento de dados de coletor:</span><span class="sxs-lookup"><span data-stu-id="1a703-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="1a703-125">Criar **serviços vinculados** para vincular repositórios de dados de entrada e saída ao seu data factory.</span><span class="sxs-lookup"><span data-stu-id="1a703-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="1a703-126">Criar **conjuntos de dados** para representar dados de entrada e saída para a operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="1a703-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="1a703-127">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="1a703-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="1a703-128">Ao usar o assistente, as definições de JSON para essas entidades do Data Factory (serviços vinculados, conjuntos de dados e o pipeline) são automaticamente criadas para você.</span><span class="sxs-lookup"><span data-stu-id="1a703-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="1a703-129">Ao usar ferramentas/APIs (exceto a API .NET), você define essas entidades do Data Factory usando o formato JSON.</span><span class="sxs-lookup"><span data-stu-id="1a703-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="1a703-130">Para obter um exemplo com definições de JSON para entidades do Data Factory que são usadas para copiar dados de um repositório de dados ODBC, confira a seção [Exemplo de JSON: Copiar dados do repositório de dados ODBC para o Blob do Azure](#json-example-copy-data-from-odbc-data-store-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="1a703-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an ODBC data store, see [JSON example: Copy data from ODBC data store to Azure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="1a703-131">As seções que se seguem fornecem detalhes sobre as propriedades JSON que são usadas para definir entidades do Data Factory específicas a um repositório de dados ODBC:</span><span class="sxs-lookup"><span data-stu-id="1a703-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to ODBC data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="1a703-132">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="1a703-132">Linked service properties</span></span>
<span data-ttu-id="1a703-133">A tabela a seguir fornece a descrição para elementos JSON específicos do serviço vinculado do ODBC.</span><span class="sxs-lookup"><span data-stu-id="1a703-133">The following table provides description for JSON elements specific to ODBC linked service.</span></span>

| <span data-ttu-id="1a703-134">Propriedade</span><span class="sxs-lookup"><span data-stu-id="1a703-134">Property</span></span> | <span data-ttu-id="1a703-135">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a703-135">Description</span></span> | <span data-ttu-id="1a703-136">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a703-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a703-137">type</span><span class="sxs-lookup"><span data-stu-id="1a703-137">type</span></span> |<span data-ttu-id="1a703-138">A propriedade type deve ser definida como: **OnPremisesOdbc**</span><span class="sxs-lookup"><span data-stu-id="1a703-138">The type property must be set to: **OnPremisesOdbc**</span></span> |<span data-ttu-id="1a703-139">Sim</span><span class="sxs-lookup"><span data-stu-id="1a703-139">Yes</span></span> |
| <span data-ttu-id="1a703-140">connectionString</span><span class="sxs-lookup"><span data-stu-id="1a703-140">connectionString</span></span> |<span data-ttu-id="1a703-141">A parte da credencial que não está relacionada ao acesso da cadeia de conexão e uma credencial criptografada opcional.</span><span class="sxs-lookup"><span data-stu-id="1a703-141">The non-access credential portion of the connection string and an optional encrypted credential.</span></span> <span data-ttu-id="1a703-142">Veja os exemplos nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="1a703-142">See examples in the following sections.</span></span> |<span data-ttu-id="1a703-143">Sim</span><span class="sxs-lookup"><span data-stu-id="1a703-143">Yes</span></span> |
| <span data-ttu-id="1a703-144">credencial</span><span class="sxs-lookup"><span data-stu-id="1a703-144">credential</span></span> |<span data-ttu-id="1a703-145">A parte da credencial de acesso da cadeia de conexão especificada no formato propriedade-valor específico do driver.</span><span class="sxs-lookup"><span data-stu-id="1a703-145">The access credential portion of the connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="1a703-146">Exemplo: "Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;".</span><span class="sxs-lookup"><span data-stu-id="1a703-146">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="1a703-147">Não</span><span class="sxs-lookup"><span data-stu-id="1a703-147">No</span></span> |
| <span data-ttu-id="1a703-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="1a703-148">authenticationType</span></span> |<span data-ttu-id="1a703-149">Tipo de autenticação usado para se conectar ao armazenamento de dados ODBC.</span><span class="sxs-lookup"><span data-stu-id="1a703-149">Type of authentication used to connect to the ODBC data store.</span></span> <span data-ttu-id="1a703-150">Os valores possíveis são: Anonymous e Basic.</span><span class="sxs-lookup"><span data-stu-id="1a703-150">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="1a703-151">Sim</span><span class="sxs-lookup"><span data-stu-id="1a703-151">Yes</span></span> |
| <span data-ttu-id="1a703-152">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="1a703-152">username</span></span> |<span data-ttu-id="1a703-153">Especifique o nome de usuário se você estiver usando a autenticação Básica.</span><span class="sxs-lookup"><span data-stu-id="1a703-153">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="1a703-154">Não</span><span class="sxs-lookup"><span data-stu-id="1a703-154">No</span></span> |
| <span data-ttu-id="1a703-155">Senha</span><span class="sxs-lookup"><span data-stu-id="1a703-155">password</span></span> |<span data-ttu-id="1a703-156">Especifique a senha da conta de usuário que você especificou para o nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="1a703-156">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="1a703-157">Não</span><span class="sxs-lookup"><span data-stu-id="1a703-157">No</span></span> |
| <span data-ttu-id="1a703-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1a703-158">gatewayName</span></span> |<span data-ttu-id="1a703-159">O nome do gateway que o serviço Data Factory deve usar para se conectar ao armazenamento de dados ODBC.</span><span class="sxs-lookup"><span data-stu-id="1a703-159">Name of the gateway that the Data Factory service should use to connect to the ODBC data store.</span></span> |<span data-ttu-id="1a703-160">Sim</span><span class="sxs-lookup"><span data-stu-id="1a703-160">Yes</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="1a703-161">Usando a autenticação Básica</span><span class="sxs-lookup"><span data-stu-id="1a703-161">Using Basic authentication</span></span>

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```
### <a name="using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="1a703-162">Usando a autenticação Básica com credenciais criptografadas</span><span class="sxs-lookup"><span data-stu-id="1a703-162">Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="1a703-163">Você pode criptografar as credenciais usando o cmdlet [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (versão 1.0 do Azure PowerShell) ou [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (versão 0.9 ou anterior do Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="1a703-163">You can encrypt the credentials using the [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of the Azure PowerShell).</span></span>  

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a><span data-ttu-id="1a703-164">Usando a autenticação anônima</span><span class="sxs-lookup"><span data-stu-id="1a703-164">Using Anonymous authentication</span></span>

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "mygateway"
        }
    }
}
```


## <a name="dataset-properties"></a><span data-ttu-id="1a703-165">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="1a703-165">Dataset properties</span></span>
<span data-ttu-id="1a703-166">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, confira o artigo [Criando conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="1a703-166">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="1a703-167">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="1a703-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="1a703-168">A seção **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local dos dados no armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="1a703-168">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="1a703-169">A seção typeProperties do conjunto de dados do tipo **RelationalTable** (que inclui o conjunto de dados do ODBC) tem as propriedades a seguir</span><span class="sxs-lookup"><span data-stu-id="1a703-169">The typeProperties section for dataset of type **RelationalTable** (which includes ODBC dataset) has the following properties</span></span>

| <span data-ttu-id="1a703-170">Propriedade</span><span class="sxs-lookup"><span data-stu-id="1a703-170">Property</span></span> | <span data-ttu-id="1a703-171">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a703-171">Description</span></span> | <span data-ttu-id="1a703-172">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a703-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a703-173">tableName</span><span class="sxs-lookup"><span data-stu-id="1a703-173">tableName</span></span> |<span data-ttu-id="1a703-174">Nome da tabela no repositório de dados ODBC.</span><span class="sxs-lookup"><span data-stu-id="1a703-174">Name of the table in the ODBC data store.</span></span> |<span data-ttu-id="1a703-175">Sim</span><span class="sxs-lookup"><span data-stu-id="1a703-175">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="1a703-176">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="1a703-176">Copy activity properties</span></span>
<span data-ttu-id="1a703-177">Para obter uma lista completa das seções e propriedades disponíveis para definir atividades, confia o artigo [Criando pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="1a703-177">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="1a703-178">As propriedades, como nome, descrição, tabelas de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="1a703-178">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="1a703-179">As propriedades disponíveis na seção **typeProperties** da atividade, por outro lado, variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="1a703-179">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="1a703-180">Para a atividade de cópia, elas variam de acordo com os tipos de fonte e coletor.</span><span class="sxs-lookup"><span data-stu-id="1a703-180">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="1a703-181">Na atividade de cópia, quando a fonte for do tipo **RelationalSource** (que inclui o ODBC), as seguintes propriedades estarão disponíveis na seção typeProperties:</span><span class="sxs-lookup"><span data-stu-id="1a703-181">In copy activity, when source is of type **RelationalSource** (which includes ODBC), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="1a703-182">Propriedade</span><span class="sxs-lookup"><span data-stu-id="1a703-182">Property</span></span> | <span data-ttu-id="1a703-183">Descrição</span><span class="sxs-lookup"><span data-stu-id="1a703-183">Description</span></span> | <span data-ttu-id="1a703-184">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="1a703-184">Allowed values</span></span> | <span data-ttu-id="1a703-185">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="1a703-185">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1a703-186">query</span><span class="sxs-lookup"><span data-stu-id="1a703-186">query</span></span> |<span data-ttu-id="1a703-187">Utiliza a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="1a703-187">Use the custom query to read data.</span></span> |<span data-ttu-id="1a703-188">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="1a703-188">SQL query string.</span></span> <span data-ttu-id="1a703-189">Por exemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="1a703-189">For example: select * from MyTable.</span></span> |<span data-ttu-id="1a703-190">Sim</span><span class="sxs-lookup"><span data-stu-id="1a703-190">Yes</span></span> |


## <a name="json-example-copy-data-from-odbc-data-store-to-azure-blob"></a><span data-ttu-id="1a703-191">Exemplo de JSON: Copiar dados do repositório de dados ODBC para o Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="1a703-191">JSON example: Copy data from ODBC data store to Azure Blob</span></span>
<span data-ttu-id="1a703-192">Este exemplo fornece as definições de JSON que você pode usar para criar um pipeline usando o [Portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), ou o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="1a703-192">This example provides JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="1a703-193">Ele mostra como copiar dados de uma fonte ODBC para um Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a703-193">It shows how to copy data from an ODBC source to an Azure Blob Storage.</span></span> <span data-ttu-id="1a703-194">No entanto, os dados podem ser copiados para qualquer um dos coletores declarados [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando a Atividade de Cópia no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1a703-194">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="1a703-195">O exemplo tem as seguintes entidades de data factory:</span><span class="sxs-lookup"><span data-stu-id="1a703-195">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="1a703-196">Um serviço vinculado do tipo [OnPremisesOdbc](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a703-196">A linked service of type [OnPremisesOdbc](#linked-service-properties).</span></span>
2. <span data-ttu-id="1a703-197">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1a703-197">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="1a703-198">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a703-198">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="1a703-199">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1a703-199">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="1a703-200">Um [pipeline](data-factory-create-pipelines.md) com Atividade de Cópia que usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1a703-200">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="1a703-201">O exemplo copia dados de um resultado de consulta em um armazenamento de dados ODBC para um blob a cada hora.</span><span class="sxs-lookup"><span data-stu-id="1a703-201">The sample copies data from a query result in an ODBC data store to a blob every hour.</span></span> <span data-ttu-id="1a703-202">As propriedades JSON usadas nesses exemplos são descritas nas seções após os exemplos.</span><span class="sxs-lookup"><span data-stu-id="1a703-202">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="1a703-203">Como uma primeira etapa, configure o gateway de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="1a703-203">As a first step, set up the data management gateway.</span></span> <span data-ttu-id="1a703-204">As instruções estão no artigo [Mover dados entre fontes locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="1a703-204">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="1a703-205">**Serviço vinculado a ODBC** Esse exemplo usa a autenticação Básica.</span><span class="sxs-lookup"><span data-stu-id="1a703-205">**ODBC linked service** This example uses the Basic authentication.</span></span> <span data-ttu-id="1a703-206">Veja a seção [Serviço vinculado a ODBC](#linked-service-properties) para ver os diferentes tipos de autenticação que você pode usar.</span><span class="sxs-lookup"><span data-stu-id="1a703-206">See [ODBC linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "OnPremOdbcLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="1a703-207">**Serviço vinculado de armazenamento do Azure**</span><span class="sxs-lookup"><span data-stu-id="1a703-207">**Azure Storage linked service**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
    "typeProperties": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
    }
}
```

<span data-ttu-id="1a703-208">**Conjunto de dados de entrada do ODBC**</span><span class="sxs-lookup"><span data-stu-id="1a703-208">**ODBC input dataset**</span></span>

<span data-ttu-id="1a703-209">O exemplo supõe que você tenha criado uma tabela "MyTable" no armazenamento de dados ODBC e que ela contenha uma coluna chamada "timestampcolumn" para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="1a703-209">The sample assumes you have created a table “MyTable” in an ODBC database and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="1a703-210">Configurar “external”: “true” informa ao serviço Data Factory que o conjunto de dados é externo ao Data Factory e não é produzido por uma atividade no Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1a703-210">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremOdbcLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="1a703-211">**Conjunto de dados de saída de Blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="1a703-211">**Azure Blob output dataset**</span></span>

<span data-ttu-id="1a703-212">Os dados são gravados em um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="1a703-212">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="1a703-213">O caminho de pasta para o blob é avaliado dinamicamente com base na hora de início da fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="1a703-213">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="1a703-214">O caminho da pasta usa as partes ano, mês, dia e horas da hora de início.</span><span class="sxs-lookup"><span data-stu-id="1a703-214">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobOdbcDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odbc/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```


<span data-ttu-id="1a703-215">**Atividade de cópia em um pipeline com origem ODBC (RelationalSource) e coletor Blob (BlobSink)**</span><span class="sxs-lookup"><span data-stu-id="1a703-215">**Copy activity in a pipeline with ODBC source (RelationalSource) and Blob sink (BlobSink)**</span></span>

<span data-ttu-id="1a703-216">O pipeline contém uma Atividade de Cópia que está configurada para usar os conjuntos de dados de entrada e saída e agendada para ser executada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="1a703-216">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="1a703-217">Na definição JSON do pipeline, o tipo **source** está definido como **RelationalSource** e o tipo **sink** está definido como **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="1a703-217">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="1a703-218">A consulta SQL especificada para a propriedade **query** seleciona os dados na última hora para copiar.</span><span class="sxs-lookup"><span data-stu-id="1a703-218">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "OdbcDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOdbcDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "OdbcToBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-odbc"></a><span data-ttu-id="1a703-219">Mapeamento de tipos para ODBC</span><span class="sxs-lookup"><span data-stu-id="1a703-219">Type mapping for ODBC</span></span>
<span data-ttu-id="1a703-220">Conforme mencionado no artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md) , a Atividade de cópia executa conversões automáticas de tipo de fonte para tipos de coletor, com a abordagem em duas etapas descritas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1a703-220">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="1a703-221">Converter de tipos de fonte nativos para o tipo .NET</span><span class="sxs-lookup"><span data-stu-id="1a703-221">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="1a703-222">Converter do tipo .NET para o tipo de coletor nativo</span><span class="sxs-lookup"><span data-stu-id="1a703-222">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="1a703-223">Ao mover dados de repositórios de dados ODBC, os tipos de dados ODBC são mapeados para tipos .NET, como mencionado no tópico [Mapeamentos de tipo de dados ODBC](https://msdn.microsoft.com/library/cc668763.aspx) .</span><span class="sxs-lookup"><span data-stu-id="1a703-223">When moving data from ODBC data stores, ODBC data types are mapped to .NET types as mentioned in the [ODBC Data Type Mappings](https://msdn.microsoft.com/library/cc668763.aspx) topic.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="1a703-224">Mapear origem para colunas de coletor</span><span class="sxs-lookup"><span data-stu-id="1a703-224">Map source to sink columns</span></span>
<span data-ttu-id="1a703-225">Para saber mais sobre mapeamento de colunas no conjunto de dados de origem para colunas no conjunto de dados de coletor, confira [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md) (Mapeamento de colunas de conjunto de dados no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="1a703-225">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="1a703-226">Leitura repetida de fontes relacionais</span><span class="sxs-lookup"><span data-stu-id="1a703-226">Repeatable read from relational sources</span></span>
<span data-ttu-id="1a703-227">Ao copiar dados de armazenamentos de dados relacionais, lembre-se da capacidade de repetição para evitar resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="1a703-227">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="1a703-228">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="1a703-228">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="1a703-229">Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="1a703-229">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="1a703-230">Quando uma fatia é executada novamente, seja de que maneira for, você precisa garantir que os mesmos dados sejam lidos não importa quantas vezes uma fatia seja executada.</span><span class="sxs-lookup"><span data-stu-id="1a703-230">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="1a703-231">Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="1a703-231">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="ge-historian-store"></a><span data-ttu-id="1a703-232">Repositório GE Historian</span><span class="sxs-lookup"><span data-stu-id="1a703-232">GE Historian store</span></span>
<span data-ttu-id="1a703-233">Você cria um serviço vinculado de ODBC para vincular um armazenamento de dados [GE Proficy Historian (agora GE Historian)](http://www.geautomation.com/products/proficy-historian) a um Azure Data Factory, como mostrado no seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="1a703-233">You create an ODBC linked service to link a [GE Proficy Historian (now GE Historian)](http://www.geautomation.com/products/proficy-historian) data store to an Azure data factory as shown in the following example:</span></span>

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of the GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="1a703-234">Instale o Gateway de Gerenciamento de Dados em um computador local e registre o gateway no portal.</span><span class="sxs-lookup"><span data-stu-id="1a703-234">Install Data Management Gateway on an on-premises machine and register the gateway with the portal.</span></span> <span data-ttu-id="1a703-235">O gateway instalado no computador local usa o driver ODBC para GE Historian para se conectar ao repositório de dados GE Historian.</span><span class="sxs-lookup"><span data-stu-id="1a703-235">The gateway installed on your on-premises computer uses the ODBC driver for GE Historian to connect to the GE Historian data store.</span></span> <span data-ttu-id="1a703-236">Portanto, instale o driver, se ele ainda não estiver instalado no computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="1a703-236">Therefore, install the driver if it is not already installed on the gateway machine.</span></span> <span data-ttu-id="1a703-237">Veja a seção [Habilitando a conectividade](#enabling-connectivity) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="1a703-237">See [Enabling connectivity](#enabling-connectivity) section for details.</span></span>

<span data-ttu-id="1a703-238">Antes de usar o repositório GE Historian em uma solução de Data Factory, verifique se o gateway pode se conectar ao armazenamento de dados usando instruções na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="1a703-238">Before you use the GE Historian store in a Data Factory solution, verify whether the gateway can connect to the data store using instructions in the next section.</span></span>

<span data-ttu-id="1a703-239">Leia o artigo desde o início para uma visão geral detalhada do uso de dados ODBC armazena como armazenamentos de dados de origem em uma operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="1a703-239">Read the article from the beginning for a detailed overview of using ODBC data stores as source data stores in a copy operation.</span></span>  

## <a name="troubleshoot-connectivity-issues"></a><span data-ttu-id="1a703-240">Solucionar problemas de conectividade</span><span class="sxs-lookup"><span data-stu-id="1a703-240">Troubleshoot connectivity issues</span></span>
<span data-ttu-id="1a703-241">Para solucionar problemas de conexão, use a guia **Diagnósticos** do **Gerenciador de Configuração do Gateway de Gerenciamento de Dados**.</span><span class="sxs-lookup"><span data-stu-id="1a703-241">To troubleshoot connection issues, use the **Diagnostics** tab of **Data Management Gateway Configuration Manager**.</span></span>

1. <span data-ttu-id="1a703-242">Iniciar o **Gerenciador de Configuração de Gateway de Gerenciamento de Dados**.</span><span class="sxs-lookup"><span data-stu-id="1a703-242">Launch **Data Management Gateway Configuration Manager**.</span></span> <span data-ttu-id="1a703-243">Você pode executar "C:\Arquivos de Programas\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" diretamente (ou) pesquisar por **Gateway** para encontrar um link para o aplicativo **Gateway de Gerenciamento de Dados da Microsoft**, conforme mostrado na imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="1a703-243">You can either run "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" directly (or) search for **Gateway** to find a link to **Microsoft Data Management Gateway** application as shown in the following image.</span></span>

    ![Gateway de pesquisa](./media/data-factory-odbc-connector/search-gateway.png)
2. <span data-ttu-id="1a703-245">Alterne para a guia **Diagnóstico** .</span><span class="sxs-lookup"><span data-stu-id="1a703-245">Switch to the **Diagnostics** tab.</span></span>

    ![Diagnóstico de gateway](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. <span data-ttu-id="1a703-247">Selecione o **tipo** de armazenamento de dados (serviço vinculado).</span><span class="sxs-lookup"><span data-stu-id="1a703-247">Select the **type** of data store (linked service).</span></span>
4. <span data-ttu-id="1a703-248">Especifique a **autenticação** e digite as **credenciais** (ou) insira a **cadeia de conexão** usada para se conectar ao repositório de dados.</span><span class="sxs-lookup"><span data-stu-id="1a703-248">Specify **authentication** and enter **credentials** (or) enter **connection string** that is used to connect to the data store.</span></span>
5. <span data-ttu-id="1a703-249">Clique em **Testar Conexão** para testar a conexão com o armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="1a703-249">Click **Test connection** to test the connection to the data store.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="1a703-250">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="1a703-250">Performance and Tuning</span></span>
<span data-ttu-id="1a703-251">Veja o [Guia de desempenho e ajuste da Atividade de Cópia](data-factory-copy-activity-performance.md) para saber mais sobre os principais fatores que afetam o desempenho da movimentação de dados (Atividade de Cópia) no Azure Data Factory, além de várias maneiras de otimizar esse processo.</span><span class="sxs-lookup"><span data-stu-id="1a703-251">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
