---
title: Mover dados para e do SQL Server | Microsoft Docs
description: Saiba mais sobre como mover dados de/para o banco de dados do SQL Server local ou em uma VM do Azure usando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 864ece28-93b5-4309-9873-b095bbe6fedd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jingwang
ms.openlocfilehash: 9cd2077d897631457925cda5ef5e6df3c0c33177
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-to-and-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a><span data-ttu-id="cbb97-103">Mover dados para e do SQL Server local ou em IaaS (VM do Azure) usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="cbb97-103">Move data to and from SQL Server on-premises or on IaaS (Azure VM) using Azure Data Factory</span></span>
<span data-ttu-id="cbb97-104">Esse artigo explica como usar a Atividade de Cópia no Azure Data Factory para mover dados para/de um banco de dados do SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="cbb97-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from an on-premises SQL Server database.</span></span> <span data-ttu-id="cbb97-105">Ele se baseia no artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md), que apresenta uma visão geral da movimentação de dados com a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="cbb97-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="cbb97-106">Cenários com suporte</span><span class="sxs-lookup"><span data-stu-id="cbb97-106">Supported scenarios</span></span>
<span data-ttu-id="cbb97-107">Você pode copiar dados **de um banco de dados do SQL Server** para os seguintes armazenamentos de dados:</span><span class="sxs-lookup"><span data-stu-id="cbb97-107">You can copy data **from a SQL Server database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="cbb97-108">Você pode copiar dados dos armazenamentos de dados a seguir **para um banco de dados do SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="cbb97-108">You can copy data from the following data stores **to a SQL Server database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a><span data-ttu-id="cbb97-109">Versões do SQL Server com suporte</span><span class="sxs-lookup"><span data-stu-id="cbb97-109">Supported SQL Server versions</span></span>
<span data-ttu-id="cbb97-110">Este conector do SQL Server dá suporte à cópia de dados de e para as versões a seguir da instância hospedada localmente ou no IaaS do Azure usando a autenticação do SQL e do Windows: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008 e SQL Server 2005</span><span class="sxs-lookup"><span data-stu-id="cbb97-110">This SQL Server connector support copying data from/to the following versions of instance hosted on-premises or in Azure IaaS using both SQL authentication and Windows authentication: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="cbb97-111">Habilitando a conectividade</span><span class="sxs-lookup"><span data-stu-id="cbb97-111">Enabling connectivity</span></span>
<span data-ttu-id="cbb97-112">Os conceitos e as etapas necessários para conectar-se com o SQL Server hospedado localmente ou em máquinas virtuais do Azure IaaS (infraestrutura como serviço) são os mesmos.</span><span class="sxs-lookup"><span data-stu-id="cbb97-112">The concepts and steps needed for connecting with SQL Server hosted on-premises or in Azure IaaS (Infrastructure-as-a-Service) VMs are the same.</span></span> <span data-ttu-id="cbb97-113">Em ambos os casos, você precisa usar o Gateway de Gerenciamento de Dados para ter conectividade.</span><span class="sxs-lookup"><span data-stu-id="cbb97-113">In both cases, you need to use Data Management Gateway for connectivity.</span></span>

<span data-ttu-id="cbb97-114">Consulte o artigo [movendo dados entre pontos locais e na nuvem](data-factory-move-data-between-onprem-and-cloud.md) para saber mais sobre o Gateway de gerenciamento de dados e obter instruções passo a passo de como configurar o gateway.</span><span class="sxs-lookup"><span data-stu-id="cbb97-114">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="cbb97-115">Configurar uma instância de gateway é um pré-requisito para a conexão com o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cbb97-115">Setting up a gateway instance is a pre-requisite for connecting with SQL Server.</span></span>

<span data-ttu-id="cbb97-116">Embora você possa instalar o gateway no mesmo computador local ou instância de VM na nuvem que o SQL Server, para obter melhore desempenho, é recomendável instalá-los em computadores separados.</span><span class="sxs-lookup"><span data-stu-id="cbb97-116">While you can install gateway on the same on-premises machine or cloud VM instance as the SQL Server for better performance, we recommended that you install them on separate machines.</span></span> <span data-ttu-id="cbb97-117">Ter o gateway e o SQL Server em computadores distintos reduz a contenção de recursos.</span><span class="sxs-lookup"><span data-stu-id="cbb97-117">Having the gateway and SQL Server on separate machines reduces resource contention.</span></span>

## <a name="getting-started"></a><span data-ttu-id="cbb97-118">Introdução</span><span class="sxs-lookup"><span data-stu-id="cbb97-118">Getting started</span></span>
<span data-ttu-id="cbb97-119">Você pode criar um pipeline com atividade de cópia que move dados de/para um banco de dados SQL Server local por meio de ferramentas/APIs diferentes.</span><span class="sxs-lookup"><span data-stu-id="cbb97-119">You can create a pipeline with a copy activity that moves data to/from an on-premises SQL Server database by using different tools/APIs.</span></span>

<span data-ttu-id="cbb97-120">A maneira mais fácil de criar um pipeline é usar o **Assistente de Cópia**.</span><span class="sxs-lookup"><span data-stu-id="cbb97-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="cbb97-121">Confira [Tutorial: Criar um pipeline usando o Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md) para ver um breve passo a passo sobre como criar um pipeline usando o Assistente de cópia de dados.</span><span class="sxs-lookup"><span data-stu-id="cbb97-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="cbb97-122">Você também pode usar as seguintes ferramentas para criar um pipeline: **Portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="cbb97-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="cbb97-123">Confira o [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo sobre a criação de um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="cbb97-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="cbb97-124">Ao usar as ferramentas ou APIs, você executa as seguintes etapas para criar um pipeline que move dados de um armazenamento de dados de origem para um armazenamento de dados de coletor:</span><span class="sxs-lookup"><span data-stu-id="cbb97-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="cbb97-125">Criar uma **data factory**.</span><span class="sxs-lookup"><span data-stu-id="cbb97-125">Create a **data factory**.</span></span> <span data-ttu-id="cbb97-126">Um data factory pode conter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="cbb97-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="cbb97-127">Criar **serviços vinculados** para vincular repositórios de dados de entrada e saída ao seu data factory.</span><span class="sxs-lookup"><span data-stu-id="cbb97-127">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="cbb97-128">Por exemplo, se você estiver copiando dados de um banco de dados do SQL Server para um Armazenamento de Blobs do Azure, crie dois serviços vinculados para vincular seu banco de dados do SQL Server e conta de Armazenamento do Azure ao data factory.</span><span class="sxs-lookup"><span data-stu-id="cbb97-128">For example, if you are copying data from a SQL Server database to an Azure blob storage, you create two linked services to link your SQL Server database and Azure storage account to your data factory.</span></span> <span data-ttu-id="cbb97-129">Para propriedades do serviço vinculado que são específicas do banco de dados do SQL Server, consulte a seção [propriedades do serviço vinculado](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cbb97-129">For linked service properties that are specific to SQL Server database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="cbb97-130">Criar **conjuntos de dados** para representar dados de entrada e saída para a operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="cbb97-130">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="cbb97-131">No exemplo mencionado na última etapa, você cria um conjunto de dados para especificar a tabela SQL no banco de dados do SQL Server que contém os dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="cbb97-131">In the example mentioned in the last step, you create a dataset to specify the SQL table in your SQL Server database that contains the input data.</span></span> <span data-ttu-id="cbb97-132">Em seguida, você cria outro conjunto de dados para especificar o contêiner de blob e a pasta que contém os dados copiados do banco de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cbb97-132">And, you create another dataset to specify the blob container and the folder that holds the data copied from the SQL Server database.</span></span> <span data-ttu-id="cbb97-133">Para propriedades do conjunto de dados que são específicas do banco de dados do SQL Server, consulte a seção [propriedades do conjunto de dados](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cbb97-133">For dataset properties that are specific to SQL Server database, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="cbb97-134">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="cbb97-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="cbb97-135">No exemplo mencionado anteriormente, você usa SqlSource como fonte e BlobSink como coletor para a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="cbb97-135">In the example mentioned earlier, you use SqlSource as a source and BlobSink as a sink for the copy activity.</span></span> <span data-ttu-id="cbb97-136">De modo similar, se você estiver copiando do Armazenamento de Blobs do Azure para o banco de dados do SQL Server, você usará BlobSource e SqlSink na atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="cbb97-136">Similarly, if you are copying from Azure Blob Storage to SQL Server Database, you use BlobSource and SqlSink in the copy activity.</span></span> <span data-ttu-id="cbb97-137">Para propriedades da atividade de cópia que são específicas do banco de dados do SQL Server, consulte a seção [propriedades da atividade de cópia](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="cbb97-137">For copy activity properties that are specific to SQL Server Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="cbb97-138">Para obter detalhes sobre como usar um armazenamento de dados como uma origem ou um coletor, clique no link na seção anterior para o armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="cbb97-138">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span> 

<span data-ttu-id="cbb97-139">Ao usar o assistente, as definições de JSON para essas entidades do Data Factory (serviços vinculados, conjuntos de dados e o pipeline) são automaticamente criadas para você.</span><span class="sxs-lookup"><span data-stu-id="cbb97-139">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="cbb97-140">Ao usar ferramentas/APIs (exceto a API .NET), você define essas entidades do Data Factory usando o formato JSON.</span><span class="sxs-lookup"><span data-stu-id="cbb97-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="cbb97-141">Para obter exemplos com definições de JSON das entidades do Data Factory usadas para copiar dados bidirecionalmente em um banco de dados do SQL Server local, confira a seção [Exemplos de JSON](#json-examples-for-copying-data-from-and-to-sql-server) neste artigo.</span><span class="sxs-lookup"><span data-stu-id="cbb97-141">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an on-premises SQL Server database, see [JSON examples](#json-examples-for-copying-data-from-and-to-sql-server) section of this article.</span></span> 

<span data-ttu-id="cbb97-142">As seções que se seguem fornecem detalhes sobre as propriedades JSON que são usadas para definir entidades do Data Factory específicas ao SQL Server:</span><span class="sxs-lookup"><span data-stu-id="cbb97-142">The following sections provide details about JSON properties that are used to define Data Factory entities specific to SQL Server:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="cbb97-143">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="cbb97-143">Linked service properties</span></span>
<span data-ttu-id="cbb97-144">Você cria um serviço vinculado do tipo **OnPremisesSqlServer** para vincular um banco de dados do SQL Server local a um data factory.</span><span class="sxs-lookup"><span data-stu-id="cbb97-144">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="cbb97-145">A tabela a seguir fornece a descrição para elementos JSON específicos para o serviço vinculado do SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="cbb97-145">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="cbb97-146">A tabela a seguir fornece a descrição para elementos JSON específicos para o serviço vinculado do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cbb97-146">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="cbb97-147">Propriedade</span><span class="sxs-lookup"><span data-stu-id="cbb97-147">Property</span></span> | <span data-ttu-id="cbb97-148">Descrição</span><span class="sxs-lookup"><span data-stu-id="cbb97-148">Description</span></span> | <span data-ttu-id="cbb97-149">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="cbb97-149">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cbb97-150">type</span><span class="sxs-lookup"><span data-stu-id="cbb97-150">type</span></span> |<span data-ttu-id="cbb97-151">A propriedade type deve ser definida como: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="cbb97-151">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="cbb97-152">Sim</span><span class="sxs-lookup"><span data-stu-id="cbb97-152">Yes</span></span> |
| <span data-ttu-id="cbb97-153">connectionString</span><span class="sxs-lookup"><span data-stu-id="cbb97-153">connectionString</span></span> |<span data-ttu-id="cbb97-154">Especifique as informações de connectionString necessárias para conexão com o banco de dados do SQL Server local usando a autenticação do SQL ou então a autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="cbb97-154">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="cbb97-155">Sim</span><span class="sxs-lookup"><span data-stu-id="cbb97-155">Yes</span></span> |
| <span data-ttu-id="cbb97-156">gatewayName</span><span class="sxs-lookup"><span data-stu-id="cbb97-156">gatewayName</span></span> |<span data-ttu-id="cbb97-157">O nome do gateway que o serviço Data Factory deve usar para se conectar ao banco de dados do SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="cbb97-157">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="cbb97-158">Sim</span><span class="sxs-lookup"><span data-stu-id="cbb97-158">Yes</span></span> |
| <span data-ttu-id="cbb97-159">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="cbb97-159">username</span></span> |<span data-ttu-id="cbb97-160">Especifique o nome de usuário se você estiver usando a Autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="cbb97-160">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="cbb97-161">Exemplo: **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="cbb97-161">Example: **domainname\\username**.</span></span> |<span data-ttu-id="cbb97-162">Não</span><span class="sxs-lookup"><span data-stu-id="cbb97-162">No</span></span> |
| <span data-ttu-id="cbb97-163">Senha</span><span class="sxs-lookup"><span data-stu-id="cbb97-163">password</span></span> |<span data-ttu-id="cbb97-164">Especifique a senha da conta de usuário que você especificou para o nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="cbb97-164">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="cbb97-165">Não</span><span class="sxs-lookup"><span data-stu-id="cbb97-165">No</span></span> |

<span data-ttu-id="cbb97-166">Criptografe as credenciais usando o cmdlet **New-AzureRmDataFactoryEncryptValue** e use-as na cadeia de conexão, como mostrado no seguinte exemplo (propriedade **EncryptedCredential**):</span><span class="sxs-lookup"><span data-stu-id="cbb97-166">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a><span data-ttu-id="cbb97-167">Exemplos</span><span class="sxs-lookup"><span data-stu-id="cbb97-167">Samples</span></span>
<span data-ttu-id="cbb97-168">**JSON para usar Autenticação SQL**</span><span class="sxs-lookup"><span data-stu-id="cbb97-168">**JSON for using SQL Authentication**</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties":
    {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
<span data-ttu-id="cbb97-169">**JSON para usar Autenticação Windows**</span><span class="sxs-lookup"><span data-stu-id="cbb97-169">**JSON for using Windows Authentication**</span></span>

<span data-ttu-id="cbb97-170">O Gateway de Gerenciamento de Dados representará a conta de usuário especificada para se conectar ao banco de dados local do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cbb97-170">Data Management Gateway will impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> 

```json
{
     "Name": " MyOnPremisesSQLDB",
     "Properties":
     {
         "type": "OnPremisesSqlServer",
         "typeProperties": {
             "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
             "username": "<domain\\username>",
             "password": "<password>",
             "gatewayName": "<gateway name>"
        }
     }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="cbb97-171">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="cbb97-171">Dataset properties</span></span>
<span data-ttu-id="cbb97-172">Nos exemplos, você usou um conjunto de dados do tipo **SqlServerTable** para representar uma tabela em um banco de dados SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cbb97-172">In the samples, you have used a dataset of type **SqlServerTable** to represent a table in a SQL Server database.</span></span>  

<span data-ttu-id="cbb97-173">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, confira o artigo [Criando conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="cbb97-173">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="cbb97-174">Seções como estrutura, disponibilidade e política de um conjunto de dados JSON são semelhantes para todos os tipos de conjunto de dados (SQL Server, blob do Azure, tabela do Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="cbb97-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (SQL Server, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="cbb97-175">A seção typeProperties é diferente para cada tipo de conjunto de dados e fornece informações sobre o local dos dados no armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="cbb97-175">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="cbb97-176">A seção **typeProperties** do conjunto de dados do tipo **SqlServerTable** tem as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="cbb97-176">The **typeProperties** section for the dataset of type **SqlServerTable** has the following properties:</span></span>

| <span data-ttu-id="cbb97-177">Propriedade</span><span class="sxs-lookup"><span data-stu-id="cbb97-177">Property</span></span> | <span data-ttu-id="cbb97-178">Descrição</span><span class="sxs-lookup"><span data-stu-id="cbb97-178">Description</span></span> | <span data-ttu-id="cbb97-179">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="cbb97-179">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cbb97-180">tableName</span><span class="sxs-lookup"><span data-stu-id="cbb97-180">tableName</span></span> |<span data-ttu-id="cbb97-181">Nome da tabela ou exibição na instância do Banco de Dados SQL Server à qual o serviço vinculado se refere.</span><span class="sxs-lookup"><span data-stu-id="cbb97-181">Name of the table or view in the SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="cbb97-182">Sim</span><span class="sxs-lookup"><span data-stu-id="cbb97-182">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="cbb97-183">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="cbb97-183">Copy activity properties</span></span>
<span data-ttu-id="cbb97-184">Se você estiver movendo dados de um banco de dados SQL Server, defina o tipo de origem na atividade de cópia como **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="cbb97-184">If you are moving data from a SQL Server database, you set the source type in the copy activity to **SqlSource**.</span></span> <span data-ttu-id="cbb97-185">Da mesma forma você estiver movendo dados para um banco de dados SQL Server, defina o tipo de coletor na atividade de cópia como **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="cbb97-185">Similarly, if you are moving data to a SQL Server database, you set the sink type in the copy activity to **SqlSink**.</span></span> <span data-ttu-id="cbb97-186">Esta seção fornece uma lista das propriedades com suporte de SqlSource e SqlSink.</span><span class="sxs-lookup"><span data-stu-id="cbb97-186">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

<span data-ttu-id="cbb97-187">Para obter uma lista completa das seções e propriedades disponíveis para definir atividades, confia o artigo [Criando pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="cbb97-187">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="cbb97-188">As propriedades, como nome, descrição, tabelas de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="cbb97-188">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="cbb97-189">A Atividade de cópia usa apenas uma entrada e produz apenas uma saída.</span><span class="sxs-lookup"><span data-stu-id="cbb97-189">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="cbb97-190">Por outro lado, as propriedades disponíveis na seção typeProperties da atividade variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="cbb97-190">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="cbb97-191">Para a atividade de cópia, elas variam de acordo com os tipos de fonte e coletor.</span><span class="sxs-lookup"><span data-stu-id="cbb97-191">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="cbb97-192">SqlSource</span><span class="sxs-lookup"><span data-stu-id="cbb97-192">SqlSource</span></span>
<span data-ttu-id="cbb97-193">Quando a fonte em uma atividade de cópia for do tipo **SqlSource**, as seguintes propriedades estarão disponíveis na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="cbb97-193">When source in a copy activity is of type **SqlSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="cbb97-194">Propriedade</span><span class="sxs-lookup"><span data-stu-id="cbb97-194">Property</span></span> | <span data-ttu-id="cbb97-195">Descrição</span><span class="sxs-lookup"><span data-stu-id="cbb97-195">Description</span></span> | <span data-ttu-id="cbb97-196">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="cbb97-196">Allowed values</span></span> | <span data-ttu-id="cbb97-197">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="cbb97-197">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cbb97-198">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="cbb97-198">sqlReaderQuery</span></span> |<span data-ttu-id="cbb97-199">Utiliza a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="cbb97-199">Use the custom query to read data.</span></span> |<span data-ttu-id="cbb97-200">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="cbb97-200">SQL query string.</span></span> <span data-ttu-id="cbb97-201">Por exemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="cbb97-201">For example: select * from MyTable.</span></span> <span data-ttu-id="cbb97-202">Pode fazer referência a várias tabelas do banco de dados referenciado pelo conjunto de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="cbb97-202">May reference multiple tables from the database referenced by the input dataset.</span></span> <span data-ttu-id="cbb97-203">Se não for especificada, a instrução SQL que é executada é: select from MyTable.</span><span class="sxs-lookup"><span data-stu-id="cbb97-203">If not specified, the SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="cbb97-204">Não</span><span class="sxs-lookup"><span data-stu-id="cbb97-204">No</span></span> |
| <span data-ttu-id="cbb97-205">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="cbb97-205">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="cbb97-206">Nome do procedimento armazenado que lê os dados da tabela de origem.</span><span class="sxs-lookup"><span data-stu-id="cbb97-206">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="cbb97-207">Nome do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="cbb97-207">Name of the stored procedure.</span></span> <span data-ttu-id="cbb97-208">A última instrução SQL deve ser uma instrução SELECT no procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="cbb97-208">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="cbb97-209">Não</span><span class="sxs-lookup"><span data-stu-id="cbb97-209">No</span></span> |
| <span data-ttu-id="cbb97-210">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="cbb97-210">storedProcedureParameters</span></span> |<span data-ttu-id="cbb97-211">Parâmetros para o procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="cbb97-211">Parameters for the stored procedure.</span></span> |<span data-ttu-id="cbb97-212">Pares de nome/valor.</span><span class="sxs-lookup"><span data-stu-id="cbb97-212">Name/value pairs.</span></span> <span data-ttu-id="cbb97-213">Nomes e uso de maiúsculas e minúsculas de parâmetros devem corresponder aos nomes e o uso de maiúsculas e minúsculas dos parâmetros do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="cbb97-213">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="cbb97-214">Não</span><span class="sxs-lookup"><span data-stu-id="cbb97-214">No</span></span> |

<span data-ttu-id="cbb97-215">Se **sqlReaderQuery** for especificado para SqlSource, a Atividade de Cópia executará essa consulta na fonte do Banco do SQL Server para obter os dados.</span><span class="sxs-lookup"><span data-stu-id="cbb97-215">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the SQL Server Database source to get the data.</span></span>

<span data-ttu-id="cbb97-216">Como alternativa, você pode especificar um procedimento armazenado especificando o **sqlReaderStoredProcedureName** e o **storedProcedureParameters** (se o procedimento armazenado usa parâmetros).</span><span class="sxs-lookup"><span data-stu-id="cbb97-216">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="cbb97-217">Se você não especificar sqlReaderQuery nem sqlReaderStoredProcedureName, as colunas definidas na seção de estrutura serão usadas para criar uma consulta seleção a ser executada no Banco de Dados SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cbb97-217">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="cbb97-218">Se a definição de conjunto de dados não tem a estrutura, todas as colunas serão selecionadas da tabela.</span><span class="sxs-lookup"><span data-stu-id="cbb97-218">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="cbb97-219">Quando você usa **sqlReaderStoredProcedureName**, ainda é necessário especificar um valor para a propriedade **tableName** no JSON do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="cbb97-219">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="cbb97-220">Contudo, não há nenhuma validação executada nessa tabela.</span><span class="sxs-lookup"><span data-stu-id="cbb97-220">There are no validations performed against this table though.</span></span>

### <a name="sqlsink"></a><span data-ttu-id="cbb97-221">SqlSink</span><span class="sxs-lookup"><span data-stu-id="cbb97-221">SqlSink</span></span>
<span data-ttu-id="cbb97-222">**SqlSink** dá suporte às seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="cbb97-222">**SqlSink** supports the following properties:</span></span>

| <span data-ttu-id="cbb97-223">Propriedade</span><span class="sxs-lookup"><span data-stu-id="cbb97-223">Property</span></span> | <span data-ttu-id="cbb97-224">Descrição</span><span class="sxs-lookup"><span data-stu-id="cbb97-224">Description</span></span> | <span data-ttu-id="cbb97-225">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="cbb97-225">Allowed values</span></span> | <span data-ttu-id="cbb97-226">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="cbb97-226">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cbb97-227">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="cbb97-227">writeBatchTimeout</span></span> |<span data-ttu-id="cbb97-228">Tempo de espera para a operação de inserção em lotes ser concluída antes de atingir o tempo limite.</span><span class="sxs-lookup"><span data-stu-id="cbb97-228">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="cbb97-229">timespan</span><span class="sxs-lookup"><span data-stu-id="cbb97-229">timespan</span></span><br/><br/> <span data-ttu-id="cbb97-230">Exemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="cbb97-230">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="cbb97-231">Não</span><span class="sxs-lookup"><span data-stu-id="cbb97-231">No</span></span> |
| <span data-ttu-id="cbb97-232">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="cbb97-232">writeBatchSize</span></span> |<span data-ttu-id="cbb97-233">Insere dados na tabela SQL quando o tamanho do buffer atinge writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="cbb97-233">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="cbb97-234">Inteiro (número de linhas)</span><span class="sxs-lookup"><span data-stu-id="cbb97-234">Integer (number of rows)</span></span> |<span data-ttu-id="cbb97-235">Não (padrão: 10000)</span><span class="sxs-lookup"><span data-stu-id="cbb97-235">No (default: 10000)</span></span> |
| <span data-ttu-id="cbb97-236">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="cbb97-236">sqlWriterCleanupScript</span></span> |<span data-ttu-id="cbb97-237">Especifique a consulta para a Atividade de Cópia a ser executada para que os dados de uma fatia especifica sejam removidos.</span><span class="sxs-lookup"><span data-stu-id="cbb97-237">Specify query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="cbb97-238">Para obter mais informações, consulte a seção [Cópia repetida](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="cbb97-238">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="cbb97-239">Uma instrução de consulta.</span><span class="sxs-lookup"><span data-stu-id="cbb97-239">A query statement.</span></span> |<span data-ttu-id="cbb97-240">Não</span><span class="sxs-lookup"><span data-stu-id="cbb97-240">No</span></span> |
| <span data-ttu-id="cbb97-241">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="cbb97-241">sliceIdentifierColumnName</span></span> |<span data-ttu-id="cbb97-242">Especifique o nome de coluna para a Atividade de Cópia a ser preenchido com o identificador de fatia gerado automaticamente, que é usado para limpar dados de uma fatia específica quando executado novamente.</span><span class="sxs-lookup"><span data-stu-id="cbb97-242">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="cbb97-243">Para obter mais informações, consulte a seção [Cópia repetida](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="cbb97-243">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="cbb97-244">Nome de uma coluna com tipo de dados de binário (32).</span><span class="sxs-lookup"><span data-stu-id="cbb97-244">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="cbb97-245">Não</span><span class="sxs-lookup"><span data-stu-id="cbb97-245">No</span></span> |
| <span data-ttu-id="cbb97-246">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="cbb97-246">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="cbb97-247">Nome do procedimento armazenado que upserts (atualiza/insere) na tabela de destino.</span><span class="sxs-lookup"><span data-stu-id="cbb97-247">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="cbb97-248">Nome do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="cbb97-248">Name of the stored procedure.</span></span> |<span data-ttu-id="cbb97-249">Não</span><span class="sxs-lookup"><span data-stu-id="cbb97-249">No</span></span> |
| <span data-ttu-id="cbb97-250">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="cbb97-250">storedProcedureParameters</span></span> |<span data-ttu-id="cbb97-251">Parâmetros para o procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="cbb97-251">Parameters for the stored procedure.</span></span> |<span data-ttu-id="cbb97-252">Pares de nome/valor.</span><span class="sxs-lookup"><span data-stu-id="cbb97-252">Name/value pairs.</span></span> <span data-ttu-id="cbb97-253">Nomes e uso de maiúsculas e minúsculas de parâmetros devem corresponder aos nomes e o uso de maiúsculas e minúsculas dos parâmetros do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="cbb97-253">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="cbb97-254">Não</span><span class="sxs-lookup"><span data-stu-id="cbb97-254">No</span></span> |
| <span data-ttu-id="cbb97-255">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="cbb97-255">sqlWriterTableType</span></span> |<span data-ttu-id="cbb97-256">Especifique o nome do tipo de tabela a ser usado no procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="cbb97-256">Specify table type name to be used in the stored procedure.</span></span> <span data-ttu-id="cbb97-257">A atividade de cópia disponibiliza aqueles dados sendo movidos em uma tabela temporária com esse tipo de tabela.</span><span class="sxs-lookup"><span data-stu-id="cbb97-257">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="cbb97-258">O código de procedimento armazenado pode mesclar os dados sendo copiados com dados existentes.</span><span class="sxs-lookup"><span data-stu-id="cbb97-258">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="cbb97-259">Um nome de tipo de tabela.</span><span class="sxs-lookup"><span data-stu-id="cbb97-259">A table type name.</span></span> |<span data-ttu-id="cbb97-260">Não</span><span class="sxs-lookup"><span data-stu-id="cbb97-260">No</span></span> |


## <a name="json-examples-for-copying-data-from-and-to-sql-server"></a><span data-ttu-id="cbb97-261">Exemplos JSON para copiar dados de e para o SQL Server</span><span class="sxs-lookup"><span data-stu-id="cbb97-261">JSON examples for copying data from and to SQL Server</span></span>
<span data-ttu-id="cbb97-262">Os exemplos a seguir fornecem amostras de definições de JSON que você pode usar para criar um pipeline usando o [Portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="cbb97-262">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="cbb97-263">Os exemplos a seguir mostram como copiar dados entre o SQL Server e o Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="cbb97-263">The following samples show how to copy data to and from SQL Server and Azure Blob Storage.</span></span> <span data-ttu-id="cbb97-264">No entanto, os dados podem ser copiados **diretamente** de qualquer uma das fontes para qualquer um dos coletores declarados [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando a Atividade de Cópia no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="cbb97-264">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>     

## <a name="example-copy-data-from-sql-server-to-azure-blob"></a><span data-ttu-id="cbb97-265">Exemplo: copiar dados do SQL Server para Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="cbb97-265">Example: Copy data from SQL Server to Azure Blob</span></span>
<span data-ttu-id="cbb97-266">O exemplo a seguir mostra:</span><span class="sxs-lookup"><span data-stu-id="cbb97-266">The following sample shows:</span></span>

1. <span data-ttu-id="cbb97-267">Um serviço vinculado do tipo [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cbb97-267">A linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="cbb97-268">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cbb97-268">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="cbb97-269">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [SqlServerTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cbb97-269">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](#dataset-properties).</span></span>
4. <span data-ttu-id="cbb97-270">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cbb97-270">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="cbb97-271">O [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [SqlSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="cbb97-271">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="cbb97-272">O exemplo copia dados de série temporal de uma tabela do SQL Server para um blob do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="cbb97-272">The sample copies time-series data from a SQL Server table to an Azure blob every hour.</span></span> <span data-ttu-id="cbb97-273">As propriedades JSON usadas nesses exemplos são descritas nas seções após os exemplos.</span><span class="sxs-lookup"><span data-stu-id="cbb97-273">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="cbb97-274">Como uma primeira etapa, configure o gateway de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="cbb97-274">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="cbb97-275">As instruções estão no artigo [Mover dados entre fontes locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="cbb97-275">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="cbb97-276">**Serviço vinculado do SQL Server**</span><span class="sxs-lookup"><span data-stu-id="cbb97-276">**SQL Server linked service**</span></span>
```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
<span data-ttu-id="cbb97-277">**Serviço vinculado do armazenamento de Blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="cbb97-277">**Azure Blob storage linked service**</span></span>

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="cbb97-278">**Conjunto de dados de entrada do SQL Server**</span><span class="sxs-lookup"><span data-stu-id="cbb97-278">**SQL Server input dataset**</span></span>

<span data-ttu-id="cbb97-279">O exemplo supõe que você criou uma tabela "MyTable" no SQL Server e que ela contém uma coluna chamada "timestampcolumn" para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="cbb97-279">The sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="cbb97-280">Você pode consultar várias tabelas no mesmo banco de dados usando um único conjunto de dados, mas uma única tabela deve ser usada para a typeProperty de tableName do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="cbb97-280">You can query over multiple tables within the same database using a single dataset, but a single table must be used for the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="cbb97-281">Configurar "external": "true" informa ao serviço Data Factory que o conjunto de dados é externo ao Data Factory e não é produzido por uma atividade no Data Factory.</span><span class="sxs-lookup"><span data-stu-id="cbb97-281">Setting “external”: ”true” informs Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
  "name": "SqlServerInput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
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
<span data-ttu-id="cbb97-282">**Conjunto de dados de saída de Blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="cbb97-282">**Azure Blob output dataset**</span></span>

<span data-ttu-id="cbb97-283">Os dados são gravados em um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="cbb97-283">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="cbb97-284">O caminho de pasta para o blob é avaliado dinamicamente com base na hora de início da fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="cbb97-284">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="cbb97-285">O caminho da pasta usa as partes ano, mês, dia e horas da hora de início.</span><span class="sxs-lookup"><span data-stu-id="cbb97-285">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="cbb97-286">**Pipeline com Atividade de cópia**</span><span class="sxs-lookup"><span data-stu-id="cbb97-286">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="cbb97-287">O pipeline contém uma Atividade de Cópia que está configurada para usar os conjuntos de dados de entrada e saída e agendada para ser executada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="cbb97-287">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="cbb97-288">Na definição de JSON do pipeline, o tipo de **fonte** está definido como **SqlSource** e o tipo de **coletor** está definido como **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="cbb97-288">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="cbb97-289">A consulta SQL especificada para a propriedade **SqlReaderQuery** seleciona os dados na última hora a serem copiados.</span><span class="sxs-lookup"><span data-stu-id="cbb97-289">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2016-06-01T18:00:00",
    "end":"2016-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```
<span data-ttu-id="cbb97-290">Neste exemplo, **sqlReaderQuery** é especificada para SqlSource.</span><span class="sxs-lookup"><span data-stu-id="cbb97-290">In this example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="cbb97-291">A Atividade de Cópia executa essa consulta na fonte do Banco de Dados do SQL Server para obter os dados.</span><span class="sxs-lookup"><span data-stu-id="cbb97-291">The Copy Activity runs this query against the SQL Server Database source to get the data.</span></span> <span data-ttu-id="cbb97-292">Como alternativa, você pode especificar um procedimento armazenado especificando o **sqlReaderStoredProcedureName** e o **storedProcedureParameters** (se o procedimento armazenado usa parâmetros).</span><span class="sxs-lookup"><span data-stu-id="cbb97-292">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span> <span data-ttu-id="cbb97-293">A sqlReaderQuery pode fazer referência a várias tabelas no banco de dados referenciado pelo conjunto de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="cbb97-293">The sqlReaderQuery can reference multiple tables within the database referenced by the input dataset.</span></span> <span data-ttu-id="cbb97-294">A propriedade não se limita apenas à tabela definida como typeProperty de tableName do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="cbb97-294">It is not limited to only the table set as the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="cbb97-295">Se você não especificar sqlReaderQuery nem sqlReaderStoredProcedureName, as colunas definidas na seção de estrutura serão usadas para criar uma consulta seleção a ser executada no Banco de Dados SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cbb97-295">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="cbb97-296">Se a definição de conjunto de dados não tem a estrutura, todas as colunas serão selecionadas da tabela.</span><span class="sxs-lookup"><span data-stu-id="cbb97-296">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="cbb97-297">Consulte a seção [Sql Source](#sqlsource) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) para obter a lista de propriedades com suporte em SqlSource e BlobSink.</span><span class="sxs-lookup"><span data-stu-id="cbb97-297">See the [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSource and BlobSink.</span></span>

## <a name="example-copy-data-from-azure-blob-to-sql-server"></a><span data-ttu-id="cbb97-298">Exemplo: copiar dados do Blob do Azure para o SQL Server</span><span class="sxs-lookup"><span data-stu-id="cbb97-298">Example: Copy data from Azure Blob to SQL Server</span></span>
<span data-ttu-id="cbb97-299">O exemplo a seguir mostra:</span><span class="sxs-lookup"><span data-stu-id="cbb97-299">The following sample shows:</span></span>

1. <span data-ttu-id="cbb97-300">O serviço vinculado do tipo [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cbb97-300">The linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="cbb97-301">O serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cbb97-301">The linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="cbb97-302">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cbb97-302">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="cbb97-303">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cbb97-303">An output [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="cbb97-304">O [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [SqlSink](#sql-server-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="cbb97-304">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#sql-server-copy-activity-type-properties).</span></span>

<span data-ttu-id="cbb97-305">O exemplo copia dados de série temporal de um Blob do Azure para uma tabela do SQL Server a cada hora.</span><span class="sxs-lookup"><span data-stu-id="cbb97-305">The sample copies time-series data from an Azure blob to a SQL Server table every hour.</span></span> <span data-ttu-id="cbb97-306">As propriedades JSON usadas nesses exemplos são descritas nas seções após os exemplos.</span><span class="sxs-lookup"><span data-stu-id="cbb97-306">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="cbb97-307">**Serviço vinculado do SQL Server**</span><span class="sxs-lookup"><span data-stu-id="cbb97-307">**SQL Server linked service**</span></span>

```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
<span data-ttu-id="cbb97-308">**Serviço vinculado do armazenamento de Blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="cbb97-308">**Azure Blob storage linked service**</span></span>

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="cbb97-309">**Conjunto de dados de entrada de Blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="cbb97-309">**Azure Blob input dataset**</span></span>

<span data-ttu-id="cbb97-310">Os dados são coletados de um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="cbb97-310">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="cbb97-311">O caminho de pasta e nome de arquivo para o blob são avaliados dinamicamente com base na hora de início da fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="cbb97-311">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="cbb97-312">O caminho da pasta usa parte da hora de início do dia, mês e ano e o nome de arquivo usa a parte da hora de início.</span><span class="sxs-lookup"><span data-stu-id="cbb97-312">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="cbb97-313">A configuração "external": "true" informa o serviço Data Factory que o conjunto de dados é externo ao Data Factory e não é produzido por uma atividade no Data Factory.</span><span class="sxs-lookup"><span data-stu-id="cbb97-313">“external”: “true” setting informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
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
<span data-ttu-id="cbb97-314">**Conjunto de dados de saída do SQL Server**</span><span class="sxs-lookup"><span data-stu-id="cbb97-314">**SQL Server output dataset**</span></span>

<span data-ttu-id="cbb97-315">O exemplo copia dados para uma tabela chamada "MyTable" no SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cbb97-315">The sample copies data to a table named “MyTable” in SQL Server.</span></span> <span data-ttu-id="cbb97-316">Crie a tabela no SQL Server com o mesmo número de colunas que você espera que o arquivo CSV de Blob contenha.</span><span class="sxs-lookup"><span data-stu-id="cbb97-316">Create the table in SQL Server with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="cbb97-317">Novas linhas são adicionadas à tabela a cada hora.</span><span class="sxs-lookup"><span data-stu-id="cbb97-317">New rows are added to the table every hour.</span></span>

```json
{
  "name": "SqlServerOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="cbb97-318">**Pipeline com Atividade de cópia**</span><span class="sxs-lookup"><span data-stu-id="cbb97-318">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="cbb97-319">O pipeline contém uma Atividade de Cópia que está configurada para usar os conjuntos de dados de entrada e saída e agendada para ser executada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="cbb97-319">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="cbb97-320">Na definição de JSON do pipeline, o tipo de **fonte** está definido como **BlobSource** e o tipo de **coletor** está definido como **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="cbb97-320">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": " SqlServerOutput "
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```

## <a name="troubleshooting-connection-issues"></a><span data-ttu-id="cbb97-321">Solucionar problemas de conexão</span><span class="sxs-lookup"><span data-stu-id="cbb97-321">Troubleshooting connection issues</span></span>
1. <span data-ttu-id="cbb97-322">Configure seu SQL Server para aceitar conexões remotas.</span><span class="sxs-lookup"><span data-stu-id="cbb97-322">Configure your SQL Server to accept remote connections.</span></span> <span data-ttu-id="cbb97-323">Inicie o **SQL Server Management Studio**, clique com o botão direito do mouse em **servidor** e clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="cbb97-323">Launch **SQL Server Management Studio**, right-click **server**, and click **Properties**.</span></span> <span data-ttu-id="cbb97-324">Selecione **Conexões** na lista e marque a opção **Permitir conexões remotas com o servidor**.</span><span class="sxs-lookup"><span data-stu-id="cbb97-324">Select **Connections** from the list and check **Allow remote connections to the server**.</span></span>

    ![Habilitar conexões remotas](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    <span data-ttu-id="cbb97-326">Veja [Configurar a Opção de Configuração do Servidor de acesso remoto](https://msdn.microsoft.com/library/ms191464.aspx) para obter as etapas detalhadas.</span><span class="sxs-lookup"><span data-stu-id="cbb97-326">See [Configure the remote access Server Configuration Option](https://msdn.microsoft.com/library/ms191464.aspx) for detailed steps.</span></span>
2. <span data-ttu-id="cbb97-327">Inicie o **SQL Server Configuration Manager**(Gerenciador de Configuração do SQL Server).</span><span class="sxs-lookup"><span data-stu-id="cbb97-327">Launch **SQL Server Configuration Manager**.</span></span> <span data-ttu-id="cbb97-328">Expanda **Configuração de Rede do SQL Server** para a instância desejada e selecione **Protocolos para MSSQLSERVER**.</span><span class="sxs-lookup"><span data-stu-id="cbb97-328">Expand **SQL Server Network Configuration** for the instance you want, and select **Protocols for MSSQLSERVER**.</span></span> <span data-ttu-id="cbb97-329">Você deve ver os protocolos no painel à direita.</span><span class="sxs-lookup"><span data-stu-id="cbb97-329">You should see protocols in the right-pane.</span></span> <span data-ttu-id="cbb97-330">Habilite o TCP/IP clicando com o botão direito do mouse em **TCP/IP** e clicando em **Habilitar**.</span><span class="sxs-lookup"><span data-stu-id="cbb97-330">Enable TCP/IP by right-clicking **TCP/IP** and clicking **Enable**.</span></span>

    ![Habilitar TCP/IP](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    <span data-ttu-id="cbb97-332">Veja [Habilitar ou Desabilitar um Protocolo de Rede do Servidor](https://msdn.microsoft.com/library/ms191294.aspx) para ver detalhes e formas alternativas de habilitar um protocolo TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="cbb97-332">See [Enable or Disable a Server Network Protocol](https://msdn.microsoft.com/library/ms191294.aspx) for details and alternate ways of enabling TCP/IP protocol.</span></span>
3. <span data-ttu-id="cbb97-333">Na mesma janela, clique duas vezes em **TCP/IP** para iniciar a janela **Propriedades de TCP/IP**.</span><span class="sxs-lookup"><span data-stu-id="cbb97-333">In the same window, double-click **TCP/IP** to launch **TCP/IP Properties** window.</span></span>
4. <span data-ttu-id="cbb97-334">Alterne para a guia **Endereços IP** .</span><span class="sxs-lookup"><span data-stu-id="cbb97-334">Switch to the **IP Addresses** tab.</span></span> <span data-ttu-id="cbb97-335">Role para baixo para ver a seção **IPAll** .</span><span class="sxs-lookup"><span data-stu-id="cbb97-335">Scroll down to see **IPAll** section.</span></span> <span data-ttu-id="cbb97-336">Anote a **Porta TCP** (o padrão é **1433**).</span><span class="sxs-lookup"><span data-stu-id="cbb97-336">Note down the **TCP Port **(default is **1433**).</span></span>
5. <span data-ttu-id="cbb97-337">Crie uma **regra para o Firewall do Windows** no computador para permitir a entrada de tráfego por essa porta.</span><span class="sxs-lookup"><span data-stu-id="cbb97-337">Create a **rule for the Windows Firewall** on the machine to allow incoming traffic through this port.</span></span>  
6. <span data-ttu-id="cbb97-338">**Verifique a conexão**: para se conectar ao SQL Server usando nome totalmente qualificado, use o SQL Server Management Studio de um computador diferente.</span><span class="sxs-lookup"><span data-stu-id="cbb97-338">**Verify connection**: To connect to the SQL Server using fully qualified name, use SQL Server Management Studio from a different machine.</span></span> <span data-ttu-id="cbb97-339">Por exemplo: “<machine><domain>.corp<company>.com,1433”.</span><span class="sxs-lookup"><span data-stu-id="cbb97-339">For example: "<machine>.<domain>.corp.<company>.com,1433."</span></span>

   > [!IMPORTANT]

   > <span data-ttu-id="cbb97-340">Consulte [Mover dados entre fontes locais e a nuvem com o Gateway de Gerenciamento de Dados](data-factory-move-data-between-onprem-and-cloud.md) para obter informações detalhadas.</span><span class="sxs-lookup"><span data-stu-id="cbb97-340">See [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for detailed information.</span></span>
   >
   > <span data-ttu-id="cbb97-341">Consulte [Solucionar problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para ver dicas sobre como solucionar os problemas relacionados à conexão/gateway.</span><span class="sxs-lookup"><span data-stu-id="cbb97-341">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>
   >
   >


## <a name="identity-columns-in-the-target-database"></a><span data-ttu-id="cbb97-342">Colunas de identidade no banco de dados de destino</span><span class="sxs-lookup"><span data-stu-id="cbb97-342">Identity columns in the target database</span></span>
<span data-ttu-id="cbb97-343">Esta seção fornece um exemplo que copia dados de uma tabela de origem sem uma coluna de identidade para uma tabela de destino com uma coluna de identidade.</span><span class="sxs-lookup"><span data-stu-id="cbb97-343">This section provides an example that copies data from a source table with no identity column to a destination table with an identity column.</span></span>

<span data-ttu-id="cbb97-344">**Tabela de origem:**</span><span class="sxs-lookup"><span data-stu-id="cbb97-344">**Source table:**</span></span>

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="cbb97-345">**Tabela de destino:**</span><span class="sxs-lookup"><span data-stu-id="cbb97-345">**Destination table:**</span></span>

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

<span data-ttu-id="cbb97-346">Observe que a tabela de destino tem uma coluna de identidade.</span><span class="sxs-lookup"><span data-stu-id="cbb97-346">Notice that the target table has an identity column.</span></span>

<span data-ttu-id="cbb97-347">**Definição de JSON do conjunto de dados de origem**</span><span class="sxs-lookup"><span data-stu-id="cbb97-347">**Source dataset JSON definition**</span></span>

```json
{
    "name": "SampleSource",
    "properties": {
        "published": false,
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
<span data-ttu-id="cbb97-348">**Definição de JSON do conjunto de dados de destino**</span><span class="sxs-lookup"><span data-stu-id="cbb97-348">**Destination dataset JSON definition**</span></span>

```json
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

<span data-ttu-id="cbb97-349">Observe que sua tabela de origem e de destino têm um esquema diferente (a de destino tem uma coluna adicional com identidade).</span><span class="sxs-lookup"><span data-stu-id="cbb97-349">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="cbb97-350">Nesse cenário, você precisa especificar a propriedade **structure** na definição de conjunto de dados de destino, que não inclui a coluna de identidade.</span><span class="sxs-lookup"><span data-stu-id="cbb97-350">In this scenario, you need to specify **structure** property in the target dataset definition, which doesn’t include the identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="cbb97-351">Invocar o procedimento armazenado do coletor SQL</span><span class="sxs-lookup"><span data-stu-id="cbb97-351">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="cbb97-352">Para obter um exemplo de como invocar um procedimento armazenado do coletor SQL em uma atividade de cópia de um pipeline, confira o artigo [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) (Invocar procedimento armazenado para coletor SQL na atividade de cópia).</span><span class="sxs-lookup"><span data-stu-id="cbb97-352">See [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article for an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline.</span></span>

## <a name="type-mapping-for-sql-server"></a><span data-ttu-id="cbb97-353">Mapeamento de tipo para o SQL Server</span><span class="sxs-lookup"><span data-stu-id="cbb97-353">Type mapping for SQL server</span></span>
<span data-ttu-id="cbb97-354">Conforme mencionado no artigo sobre [atividades de movimentação de dados](data-factory-data-movement-activities.md) , a Atividade de Cópia executa conversões automáticas de tipos de fonte em tipos de coletor com a abordagem de duas etapas:</span><span class="sxs-lookup"><span data-stu-id="cbb97-354">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="cbb97-355">Converter de tipos de fonte nativos para o tipo .NET</span><span class="sxs-lookup"><span data-stu-id="cbb97-355">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="cbb97-356">Converter do tipo .NET para o tipo de coletor nativo</span><span class="sxs-lookup"><span data-stu-id="cbb97-356">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="cbb97-357">Ao mover dados bidirecionalmente no SQL Server, os mapeamentos a seguir são usados do tipo SQL para o tipo .NET e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="cbb97-357">When moving data to & from SQL server, the following mappings are used from SQL type to .NET type and vice versa.</span></span>

<span data-ttu-id="cbb97-358">O mapeamento é o mesmo que o mapeamento de tipo de dados do SQL Server para o ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="cbb97-358">The mapping is same as the SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="cbb97-359">Tipo de mecanismo do Banco de Dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="cbb97-359">SQL Server Database Engine type</span></span> | <span data-ttu-id="cbb97-360">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="cbb97-360">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="cbb97-361">bigint</span><span class="sxs-lookup"><span data-stu-id="cbb97-361">bigint</span></span> |<span data-ttu-id="cbb97-362">Int64</span><span class="sxs-lookup"><span data-stu-id="cbb97-362">Int64</span></span> |
| <span data-ttu-id="cbb97-363">binário</span><span class="sxs-lookup"><span data-stu-id="cbb97-363">binary</span></span> |<span data-ttu-id="cbb97-364">Byte[]</span><span class="sxs-lookup"><span data-stu-id="cbb97-364">Byte[]</span></span> |
| <span data-ttu-id="cbb97-365">bit</span><span class="sxs-lookup"><span data-stu-id="cbb97-365">bit</span></span> |<span data-ttu-id="cbb97-366">Booliano</span><span class="sxs-lookup"><span data-stu-id="cbb97-366">Boolean</span></span> |
| <span data-ttu-id="cbb97-367">char</span><span class="sxs-lookup"><span data-stu-id="cbb97-367">char</span></span> |<span data-ttu-id="cbb97-368">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="cbb97-368">String, Char[]</span></span> |
| <span data-ttu-id="cbb97-369">data</span><span class="sxs-lookup"><span data-stu-id="cbb97-369">date</span></span> |<span data-ttu-id="cbb97-370">DateTime</span><span class="sxs-lookup"><span data-stu-id="cbb97-370">DateTime</span></span> |
| <span data-ttu-id="cbb97-371">DateTime</span><span class="sxs-lookup"><span data-stu-id="cbb97-371">Datetime</span></span> |<span data-ttu-id="cbb97-372">DateTime</span><span class="sxs-lookup"><span data-stu-id="cbb97-372">DateTime</span></span> |
| <span data-ttu-id="cbb97-373">datetime2</span><span class="sxs-lookup"><span data-stu-id="cbb97-373">datetime2</span></span> |<span data-ttu-id="cbb97-374">DateTime</span><span class="sxs-lookup"><span data-stu-id="cbb97-374">DateTime</span></span> |
| <span data-ttu-id="cbb97-375">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="cbb97-375">Datetimeoffset</span></span> |<span data-ttu-id="cbb97-376">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="cbb97-376">DateTimeOffset</span></span> |
| <span data-ttu-id="cbb97-377">Decimal</span><span class="sxs-lookup"><span data-stu-id="cbb97-377">Decimal</span></span> |<span data-ttu-id="cbb97-378">Decimal</span><span class="sxs-lookup"><span data-stu-id="cbb97-378">Decimal</span></span> |
| <span data-ttu-id="cbb97-379">Atributo FILESTREAM (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="cbb97-379">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="cbb97-380">Byte[]</span><span class="sxs-lookup"><span data-stu-id="cbb97-380">Byte[]</span></span> |
| <span data-ttu-id="cbb97-381">Float</span><span class="sxs-lookup"><span data-stu-id="cbb97-381">Float</span></span> |<span data-ttu-id="cbb97-382">Duplo</span><span class="sxs-lookup"><span data-stu-id="cbb97-382">Double</span></span> |
| <span data-ttu-id="cbb97-383">imagem</span><span class="sxs-lookup"><span data-stu-id="cbb97-383">image</span></span> |<span data-ttu-id="cbb97-384">Byte[]</span><span class="sxs-lookup"><span data-stu-id="cbb97-384">Byte[]</span></span> |
| <span data-ttu-id="cbb97-385">int</span><span class="sxs-lookup"><span data-stu-id="cbb97-385">int</span></span> |<span data-ttu-id="cbb97-386">Int32</span><span class="sxs-lookup"><span data-stu-id="cbb97-386">Int32</span></span> |
| <span data-ttu-id="cbb97-387">money</span><span class="sxs-lookup"><span data-stu-id="cbb97-387">money</span></span> |<span data-ttu-id="cbb97-388">Decimal</span><span class="sxs-lookup"><span data-stu-id="cbb97-388">Decimal</span></span> |
| <span data-ttu-id="cbb97-389">nchar</span><span class="sxs-lookup"><span data-stu-id="cbb97-389">nchar</span></span> |<span data-ttu-id="cbb97-390">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="cbb97-390">String, Char[]</span></span> |
| <span data-ttu-id="cbb97-391">ntext</span><span class="sxs-lookup"><span data-stu-id="cbb97-391">ntext</span></span> |<span data-ttu-id="cbb97-392">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="cbb97-392">String, Char[]</span></span> |
| <span data-ttu-id="cbb97-393">numérico</span><span class="sxs-lookup"><span data-stu-id="cbb97-393">numeric</span></span> |<span data-ttu-id="cbb97-394">Decimal</span><span class="sxs-lookup"><span data-stu-id="cbb97-394">Decimal</span></span> |
| <span data-ttu-id="cbb97-395">nvarchar</span><span class="sxs-lookup"><span data-stu-id="cbb97-395">nvarchar</span></span> |<span data-ttu-id="cbb97-396">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="cbb97-396">String, Char[]</span></span> |
| <span data-ttu-id="cbb97-397">real</span><span class="sxs-lookup"><span data-stu-id="cbb97-397">real</span></span> |<span data-ttu-id="cbb97-398">Single</span><span class="sxs-lookup"><span data-stu-id="cbb97-398">Single</span></span> |
| <span data-ttu-id="cbb97-399">rowversion</span><span class="sxs-lookup"><span data-stu-id="cbb97-399">rowversion</span></span> |<span data-ttu-id="cbb97-400">Byte[]</span><span class="sxs-lookup"><span data-stu-id="cbb97-400">Byte[]</span></span> |
| <span data-ttu-id="cbb97-401">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="cbb97-401">smalldatetime</span></span> |<span data-ttu-id="cbb97-402">DateTime</span><span class="sxs-lookup"><span data-stu-id="cbb97-402">DateTime</span></span> |
| <span data-ttu-id="cbb97-403">smallint</span><span class="sxs-lookup"><span data-stu-id="cbb97-403">smallint</span></span> |<span data-ttu-id="cbb97-404">Int16</span><span class="sxs-lookup"><span data-stu-id="cbb97-404">Int16</span></span> |
| <span data-ttu-id="cbb97-405">smallmoney</span><span class="sxs-lookup"><span data-stu-id="cbb97-405">smallmoney</span></span> |<span data-ttu-id="cbb97-406">Decimal</span><span class="sxs-lookup"><span data-stu-id="cbb97-406">Decimal</span></span> |
| <span data-ttu-id="cbb97-407">sql_variant</span><span class="sxs-lookup"><span data-stu-id="cbb97-407">sql_variant</span></span> |<span data-ttu-id="cbb97-408">Objeto *</span><span class="sxs-lookup"><span data-stu-id="cbb97-408">Object *</span></span> |
| <span data-ttu-id="cbb97-409">texto</span><span class="sxs-lookup"><span data-stu-id="cbb97-409">text</span></span> |<span data-ttu-id="cbb97-410">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="cbb97-410">String, Char[]</span></span> |
| <span data-ttu-id="cbb97-411">tempo real</span><span class="sxs-lookup"><span data-stu-id="cbb97-411">time</span></span> |<span data-ttu-id="cbb97-412">timespan</span><span class="sxs-lookup"><span data-stu-id="cbb97-412">TimeSpan</span></span> |
| <span data-ttu-id="cbb97-413">timestamp</span><span class="sxs-lookup"><span data-stu-id="cbb97-413">timestamp</span></span> |<span data-ttu-id="cbb97-414">Byte[]</span><span class="sxs-lookup"><span data-stu-id="cbb97-414">Byte[]</span></span> |
| <span data-ttu-id="cbb97-415">tinyint</span><span class="sxs-lookup"><span data-stu-id="cbb97-415">tinyint</span></span> |<span data-ttu-id="cbb97-416">Byte</span><span class="sxs-lookup"><span data-stu-id="cbb97-416">Byte</span></span> |
| <span data-ttu-id="cbb97-417">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="cbb97-417">uniqueidentifier</span></span> |<span data-ttu-id="cbb97-418">Guid</span><span class="sxs-lookup"><span data-stu-id="cbb97-418">Guid</span></span> |
| <span data-ttu-id="cbb97-419">varbinary</span><span class="sxs-lookup"><span data-stu-id="cbb97-419">varbinary</span></span> |<span data-ttu-id="cbb97-420">Byte[]</span><span class="sxs-lookup"><span data-stu-id="cbb97-420">Byte[]</span></span> |
| <span data-ttu-id="cbb97-421">varchar</span><span class="sxs-lookup"><span data-stu-id="cbb97-421">varchar</span></span> |<span data-ttu-id="cbb97-422">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="cbb97-422">String, Char[]</span></span> |
| <span data-ttu-id="cbb97-423">xml</span><span class="sxs-lookup"><span data-stu-id="cbb97-423">xml</span></span> |<span data-ttu-id="cbb97-424">xml</span><span class="sxs-lookup"><span data-stu-id="cbb97-424">Xml</span></span> |

## <a name="mapping-source-to-sink-columns"></a><span data-ttu-id="cbb97-425">Mapear origem para colunas de coletor</span><span class="sxs-lookup"><span data-stu-id="cbb97-425">Mapping source to sink columns</span></span>
<span data-ttu-id="cbb97-426">Para mapear colunas de conjunto de dados de origem para colunas do conjunto de dados de coletor, confira [Mapeando colunas de conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="cbb97-426">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="cbb97-427">Cópia repetida</span><span class="sxs-lookup"><span data-stu-id="cbb97-427">Repeatable copy</span></span>
<span data-ttu-id="cbb97-428">Ao copiar dados para o Banco de Dados do SQL Server, a atividade de cópia acrescenta dados à tabela de coletor por padrão.</span><span class="sxs-lookup"><span data-stu-id="cbb97-428">When copying data to SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="cbb97-429">Para substituir isso pela execução de UPSERT, confira o artigo [Repeatable write to SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) (Gravação repetida no SqlSink).</span><span class="sxs-lookup"><span data-stu-id="cbb97-429">To perform an UPSERT instead,  See [Repeatable write to SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="cbb97-430">Ao copiar dados de armazenamentos de dados relacionais, lembre-se da capacidade de repetição para evitar resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="cbb97-430">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="cbb97-431">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="cbb97-431">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="cbb97-432">Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="cbb97-432">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="cbb97-433">Quando uma fatia é executada novamente, seja de que maneira for, você precisa garantir que os mesmos dados sejam lidos não importa quantas vezes uma fatia seja executada.</span><span class="sxs-lookup"><span data-stu-id="cbb97-433">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="cbb97-434">Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="cbb97-434">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="cbb97-435">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="cbb97-435">Performance and Tuning</span></span>
<span data-ttu-id="cbb97-436">Veja o [Guia de desempenho e ajuste da Atividade de Cópia](data-factory-copy-activity-performance.md) para saber mais sobre os principais fatores que afetam o desempenho da movimentação de dados (Atividade de Cópia) no Azure Data Factory, além de várias maneiras de otimizar esse processo.</span><span class="sxs-lookup"><span data-stu-id="cbb97-436">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
