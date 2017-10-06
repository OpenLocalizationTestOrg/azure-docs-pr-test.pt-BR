---
title: aaaMove tooand de dados do SQL Server | Microsoft Docs
description: "Saiba mais sobre como toomove dados do SQL Server/para o banco de dados que é local ou em uma VM do Azure usando o Azure Data Factory."
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
ms.openlocfilehash: f0cccf56a670e62ec893d75052a81eb26d562050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a><span data-ttu-id="41d57-103">Mover dados tooand do SQL Server local ou na IaaS (VM do Azure) usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="41d57-103">Move data tooand from SQL Server on-premises or on IaaS (Azure VM) using Azure Data Factory</span></span>
<span data-ttu-id="41d57-104">Este artigo explica como toouse hello atividade de cópia em dados do Azure Data Factory toomove de/para um banco de dados do SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="41d57-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from an on-premises SQL Server database.</span></span> <span data-ttu-id="41d57-105">Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="41d57-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="41d57-106">Cenários com suporte</span><span class="sxs-lookup"><span data-stu-id="41d57-106">Supported scenarios</span></span>
<span data-ttu-id="41d57-107">Você pode copiar dados **de um banco de dados do SQL Server** toohello repositórios de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="41d57-107">You can copy data **from a SQL Server database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="41d57-108">Você pode copiar dados de saudação armazenamentos de dados a seguir **banco de dados do SQL Server tooa**:</span><span class="sxs-lookup"><span data-stu-id="41d57-108">You can copy data from hello following data stores **tooa SQL Server database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a><span data-ttu-id="41d57-109">Versões do SQL Server com suporte</span><span class="sxs-lookup"><span data-stu-id="41d57-109">Supported SQL Server versions</span></span>
<span data-ttu-id="41d57-110">Esse suporte de conector do SQL Server copiar dados do / toohello versões de instância hospedada no local ou na IaaS do Azure usando a autenticação do SQL e a autenticação do Windows a seguir: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span><span class="sxs-lookup"><span data-stu-id="41d57-110">This SQL Server connector support copying data from/toohello following versions of instance hosted on-premises or in Azure IaaS using both SQL authentication and Windows authentication: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="41d57-111">Habilitando a conectividade</span><span class="sxs-lookup"><span data-stu-id="41d57-111">Enabling connectivity</span></span>
<span data-ttu-id="41d57-112">conceitos de saudação e as etapas necessárias para conectar-se com o SQL Server hospedado no local ou no Azure IaaS VMs (uma infraestrutura como serviço) são Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="41d57-112">hello concepts and steps needed for connecting with SQL Server hosted on-premises or in Azure IaaS (Infrastructure-as-a-Service) VMs are hello same.</span></span> <span data-ttu-id="41d57-113">Em ambos os casos, você precisa toouse Data Management Gateway para conectividade.</span><span class="sxs-lookup"><span data-stu-id="41d57-113">In both cases, you need toouse Data Management Gateway for connectivity.</span></span>

<span data-ttu-id="41d57-114">Consulte [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) toolearn artigo sobre o Gateway de gerenciamento de dados e instruções passo a passo sobre como configurar o gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="41d57-114">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="41d57-115">Configurar uma instância de gateway é um pré-requisito para a conexão com o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="41d57-115">Setting up a gateway instance is a pre-requisite for connecting with SQL Server.</span></span>

<span data-ttu-id="41d57-116">Embora você possa instalar o gateway Olá mesmo no local instância da máquina ou nuvem de VM como Olá do SQL Server para obter melhor desempenho, é recomendável instalá-los em computadores separados.</span><span class="sxs-lookup"><span data-stu-id="41d57-116">While you can install gateway on hello same on-premises machine or cloud VM instance as hello SQL Server for better performance, we recommended that you install them on separate machines.</span></span> <span data-ttu-id="41d57-117">Ter Olá gateway e o SQL Server em máquinas separadas reduz a contenção de recursos.</span><span class="sxs-lookup"><span data-stu-id="41d57-117">Having hello gateway and SQL Server on separate machines reduces resource contention.</span></span>

## <a name="getting-started"></a><span data-ttu-id="41d57-118">Introdução</span><span class="sxs-lookup"><span data-stu-id="41d57-118">Getting started</span></span>
<span data-ttu-id="41d57-119">Você pode criar um pipeline com atividade de cópia que move dados de/para um banco de dados SQL Server local por meio de ferramentas/APIs diferentes.</span><span class="sxs-lookup"><span data-stu-id="41d57-119">You can create a pipeline with a copy activity that moves data to/from an on-premises SQL Server database by using different tools/APIs.</span></span>

<span data-ttu-id="41d57-120">toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**.</span><span class="sxs-lookup"><span data-stu-id="41d57-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="41d57-121">Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.</span><span class="sxs-lookup"><span data-stu-id="41d57-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="41d57-122">Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="41d57-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="41d57-123">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="41d57-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="41d57-124">Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="41d57-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="41d57-125">Criar uma **data factory**.</span><span class="sxs-lookup"><span data-stu-id="41d57-125">Create a **data factory**.</span></span> <span data-ttu-id="41d57-126">Um data factory pode conter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="41d57-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="41d57-127">Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.</span><span class="sxs-lookup"><span data-stu-id="41d57-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="41d57-128">Por exemplo, se você estiver copiando dados de um banco de dados de SQL Server tooan armazenamento de BLOBs do Azure, você criar duas toolink de serviços vinculados seu banco de dados do SQL Server e a fábrica de dados de tooyour de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="41d57-128">For example, if you are copying data from a SQL Server database tooan Azure blob storage, you create two linked services toolink your SQL Server database and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="41d57-129">Para propriedades de serviço vinculado que banco de dados de servidor tooSQL específicos, consulte [vinculado propriedades do serviço](#linked-service-properties) seção.</span><span class="sxs-lookup"><span data-stu-id="41d57-129">For linked service properties that are specific tooSQL Server database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="41d57-130">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello.</span><span class="sxs-lookup"><span data-stu-id="41d57-130">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="41d57-131">No exemplo hello mencionado na última etapa do hello, você pode criar uma tabela do dataset toospecify Olá SQL no banco de dados do SQL Server que contém os dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="41d57-131">In hello example mentioned in hello last step, you create a dataset toospecify hello SQL table in your SQL Server database that contains hello input data.</span></span> <span data-ttu-id="41d57-132">E, criar outro contêiner de blob do conjunto de dados toospecify hello e pasta Olá que contém dados saudação copiados da saudação banco de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="41d57-132">And, you create another dataset toospecify hello blob container and hello folder that holds hello data copied from hello SQL Server database.</span></span> <span data-ttu-id="41d57-133">Para propriedades de conjunto de dados que são específicos tooSQL banco de dados do servidor, consulte [propriedades de conjunto de dados](#dataset-properties) seção.</span><span class="sxs-lookup"><span data-stu-id="41d57-133">For dataset properties that are specific tooSQL Server database, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="41d57-134">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="41d57-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="41d57-135">Exemplo hello mencionado anteriormente, você usar SqlSource como uma origem e BlobSink como um coletor de atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="41d57-135">In hello example mentioned earlier, you use SqlSource as a source and BlobSink as a sink for hello copy activity.</span></span> <span data-ttu-id="41d57-136">Da mesma forma, se você está copiando do armazenamento de BLOBs do Azure tooSQL banco de dados do servidor, use BlobSource e SqlSink na atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="41d57-136">Similarly, if you are copying from Azure Blob Storage tooSQL Server Database, you use BlobSource and SqlSink in hello copy activity.</span></span> <span data-ttu-id="41d57-137">Para propriedades de atividade de cópia que específico tooSQL banco de dados do servidor, consulte [copiar as propriedades de atividade](#copy-activity-properties) seção.</span><span class="sxs-lookup"><span data-stu-id="41d57-137">For copy activity properties that are specific tooSQL Server Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="41d57-138">Para obter detalhes sobre como toouse um repositório de dados como uma origem ou um coletor, clique em Olá link na seção anterior de saudação para seu armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="41d57-138">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span> 

<span data-ttu-id="41d57-139">Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="41d57-139">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="41d57-140">Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="41d57-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="41d57-141">Para obter exemplos com definições de JSON para entidades de fábrica de dados que são usados toocopy dados para/de um banco de dados do SQL Server local, consulte [exemplos JSON](#json-examples-for-copying-data-from-and-to-sql-server) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="41d57-141">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an on-premises SQL Server database, see [JSON examples](#json-examples-for-copying-data-from-and-to-sql-server) section of this article.</span></span> 

<span data-ttu-id="41d57-142">Olá seções a seguir fornece detalhes sobre as propriedades JSON que são usadas toodefine Data Factory entidades específica tooSQL Server:</span><span class="sxs-lookup"><span data-stu-id="41d57-142">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooSQL Server:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="41d57-143">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="41d57-143">Linked service properties</span></span>
<span data-ttu-id="41d57-144">Criar um serviço vinculado do tipo **OnPremisesSqlServer** toolink uma fábrica de dados tooa de banco de dados do local do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="41d57-144">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="41d57-145">Olá a tabela a seguir fornece uma descrição para o serviço vinculado do SQL Server do JSON elementos tooon local específico.</span><span class="sxs-lookup"><span data-stu-id="41d57-145">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="41d57-146">Olá, a tabela a seguir fornece uma descrição para o JSON de elementos específico tooSQL serviço do servidor vinculado.</span><span class="sxs-lookup"><span data-stu-id="41d57-146">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="41d57-147">Propriedade</span><span class="sxs-lookup"><span data-stu-id="41d57-147">Property</span></span> | <span data-ttu-id="41d57-148">Descrição</span><span class="sxs-lookup"><span data-stu-id="41d57-148">Description</span></span> | <span data-ttu-id="41d57-149">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="41d57-149">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="41d57-150">type</span><span class="sxs-lookup"><span data-stu-id="41d57-150">type</span></span> |<span data-ttu-id="41d57-151">propriedade de tipo Hello deve ser definida como: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="41d57-151">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="41d57-152">Sim</span><span class="sxs-lookup"><span data-stu-id="41d57-152">Yes</span></span> |
| <span data-ttu-id="41d57-153">connectionString</span><span class="sxs-lookup"><span data-stu-id="41d57-153">connectionString</span></span> |<span data-ttu-id="41d57-154">Especifica informações de connectionString necessárias tooconnect toohello no SQL Server banco de dados local usando a autenticação do Windows ou autenticação do SQL.</span><span class="sxs-lookup"><span data-stu-id="41d57-154">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="41d57-155">Sim</span><span class="sxs-lookup"><span data-stu-id="41d57-155">Yes</span></span> |
| <span data-ttu-id="41d57-156">gatewayName</span><span class="sxs-lookup"><span data-stu-id="41d57-156">gatewayName</span></span> |<span data-ttu-id="41d57-157">Nome do gateway Olá Olá serviço da fábrica de dados deve usar o banco de dados do tooconnect toohello no local do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="41d57-157">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="41d57-158">Sim</span><span class="sxs-lookup"><span data-stu-id="41d57-158">Yes</span></span> |
| <span data-ttu-id="41d57-159">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="41d57-159">username</span></span> |<span data-ttu-id="41d57-160">Especifique o nome de usuário se você estiver usando a Autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="41d57-160">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="41d57-161">Exemplo: **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="41d57-161">Example: **domainname\\username**.</span></span> |<span data-ttu-id="41d57-162">Não</span><span class="sxs-lookup"><span data-stu-id="41d57-162">No</span></span> |
| <span data-ttu-id="41d57-163">Senha</span><span class="sxs-lookup"><span data-stu-id="41d57-163">password</span></span> |<span data-ttu-id="41d57-164">Especifique a senha da conta de usuário de saudação especificado para nome de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="41d57-164">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="41d57-165">Não</span><span class="sxs-lookup"><span data-stu-id="41d57-165">No</span></span> |

<span data-ttu-id="41d57-166">Você pode criptografar credenciais usando Olá **New-AzureRmDataFactoryEncryptValue** cmdlet e usá-los na cadeia de caracteres de conexão hello, conforme mostrado no exemplo a seguir de saudação (**EncryptedCredential** propriedade):</span><span class="sxs-lookup"><span data-stu-id="41d57-166">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a><span data-ttu-id="41d57-167">Exemplos</span><span class="sxs-lookup"><span data-stu-id="41d57-167">Samples</span></span>
<span data-ttu-id="41d57-168">**JSON para usar Autenticação SQL**</span><span class="sxs-lookup"><span data-stu-id="41d57-168">**JSON for using SQL Authentication**</span></span>

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
<span data-ttu-id="41d57-169">**JSON para usar Autenticação Windows**</span><span class="sxs-lookup"><span data-stu-id="41d57-169">**JSON for using Windows Authentication**</span></span>

<span data-ttu-id="41d57-170">Gateway de gerenciamento de dados representará Olá especificado usuário conta tooconnect toohello no SQL Server banco de dados local.</span><span class="sxs-lookup"><span data-stu-id="41d57-170">Data Management Gateway will impersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> 

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

## <a name="dataset-properties"></a><span data-ttu-id="41d57-171">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="41d57-171">Dataset properties</span></span>
<span data-ttu-id="41d57-172">Exemplos de hello, você usou um conjunto de dados do tipo **SqlServerTable** toorepresent uma tabela em um banco de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="41d57-172">In hello samples, you have used a dataset of type **SqlServerTable** toorepresent a table in a SQL Server database.</span></span>  

<span data-ttu-id="41d57-173">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="41d57-173">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="41d57-174">Seções como estrutura, disponibilidade e política de um conjunto de dados JSON são semelhantes para todos os tipos de conjunto de dados (SQL Server, blob do Azure, tabela do Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="41d57-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (SQL Server, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="41d57-175">seção de typeProperties Olá é diferente para cada tipo de conjunto de dados e fornece informações sobre local de saudação de dados Olá no repositório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="41d57-175">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="41d57-176">Olá **typeProperties** seção de conjunto de dados de saudação do tipo **SqlServerTable** tem Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="41d57-176">hello **typeProperties** section for hello dataset of type **SqlServerTable** has hello following properties:</span></span>

| <span data-ttu-id="41d57-177">Propriedade</span><span class="sxs-lookup"><span data-stu-id="41d57-177">Property</span></span> | <span data-ttu-id="41d57-178">Descrição</span><span class="sxs-lookup"><span data-stu-id="41d57-178">Description</span></span> | <span data-ttu-id="41d57-179">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="41d57-179">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="41d57-180">tableName</span><span class="sxs-lookup"><span data-stu-id="41d57-180">tableName</span></span> |<span data-ttu-id="41d57-181">Nome da tabela de saudação ou exibição na instância de banco de dados do SQL Server Olá que serviço vinculado refere-se a.</span><span class="sxs-lookup"><span data-stu-id="41d57-181">Name of hello table or view in hello SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="41d57-182">Sim</span><span class="sxs-lookup"><span data-stu-id="41d57-182">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="41d57-183">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="41d57-183">Copy activity properties</span></span>
<span data-ttu-id="41d57-184">Se você estiver movendo dados de um banco de dados do SQL Server, você defina o tipo de fonte de saudação na atividade de cópia de saudação muito**SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="41d57-184">If you are moving data from a SQL Server database, you set hello source type in hello copy activity too**SqlSource**.</span></span> <span data-ttu-id="41d57-185">Da mesma forma, se você estiver movendo o banco de dados do SQL Server data tooa, você definir o tipo de coletor Olá na atividade de cópia de saudação muito**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="41d57-185">Similarly, if you are moving data tooa SQL Server database, you set hello sink type in hello copy activity too**SqlSink**.</span></span> <span data-ttu-id="41d57-186">Esta seção fornece uma lista das propriedades com suporte de SqlSource e SqlSink.</span><span class="sxs-lookup"><span data-stu-id="41d57-186">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

<span data-ttu-id="41d57-187">Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="41d57-187">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="41d57-188">As propriedades, como nome, descrição, tabelas de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="41d57-188">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="41d57-189">Hello atividade de cópia usa apenas uma entrada e produz apenas uma saída.</span><span class="sxs-lookup"><span data-stu-id="41d57-189">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="41d57-190">Por outro lado, as propriedades disponíveis na seção typeProperties hello atividade Olá variam com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="41d57-190">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="41d57-191">Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.</span><span class="sxs-lookup"><span data-stu-id="41d57-191">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="41d57-192">SqlSource</span><span class="sxs-lookup"><span data-stu-id="41d57-192">SqlSource</span></span>
<span data-ttu-id="41d57-193">Quando a fonte em uma atividade de cópia é do tipo **SqlSource**, Olá propriedades a seguir está disponível em **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="41d57-193">When source in a copy activity is of type **SqlSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="41d57-194">Propriedade</span><span class="sxs-lookup"><span data-stu-id="41d57-194">Property</span></span> | <span data-ttu-id="41d57-195">Descrição</span><span class="sxs-lookup"><span data-stu-id="41d57-195">Description</span></span> | <span data-ttu-id="41d57-196">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="41d57-196">Allowed values</span></span> | <span data-ttu-id="41d57-197">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="41d57-197">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="41d57-198">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="41d57-198">sqlReaderQuery</span></span> |<span data-ttu-id="41d57-199">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="41d57-199">Use hello custom query tooread data.</span></span> |<span data-ttu-id="41d57-200">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="41d57-200">SQL query string.</span></span> <span data-ttu-id="41d57-201">Por exemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="41d57-201">For example: select * from MyTable.</span></span> <span data-ttu-id="41d57-202">Pode fazer referência a várias tabelas de banco de dados de saudação referenciado pelo conjunto de dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="41d57-202">May reference multiple tables from hello database referenced by hello input dataset.</span></span> <span data-ttu-id="41d57-203">Se não for especificado, Olá instrução SQL executada: selecione MyTable.</span><span class="sxs-lookup"><span data-stu-id="41d57-203">If not specified, hello SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="41d57-204">Não</span><span class="sxs-lookup"><span data-stu-id="41d57-204">No</span></span> |
| <span data-ttu-id="41d57-205">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="41d57-205">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="41d57-206">Nome da saudação procedimento armazenado que lê dados da tabela de origem hello.</span><span class="sxs-lookup"><span data-stu-id="41d57-206">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="41d57-207">Nome da saudação de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="41d57-207">Name of hello stored procedure.</span></span> <span data-ttu-id="41d57-208">Olá a última instrução de SQL deve ser uma instrução SELECT no procedimento armazenado de saudação.</span><span class="sxs-lookup"><span data-stu-id="41d57-208">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="41d57-209">Não</span><span class="sxs-lookup"><span data-stu-id="41d57-209">No</span></span> |
| <span data-ttu-id="41d57-210">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="41d57-210">storedProcedureParameters</span></span> |<span data-ttu-id="41d57-211">Parâmetros de saudação de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="41d57-211">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="41d57-212">Pares de nome/valor.</span><span class="sxs-lookup"><span data-stu-id="41d57-212">Name/value pairs.</span></span> <span data-ttu-id="41d57-213">Nomes e o uso de maiusculas e minúsculas dos parâmetros devem corresponder a nomes de saudação e uso de maiusculas e minúsculas dos parâmetros de procedimento armazenado de saudação.</span><span class="sxs-lookup"><span data-stu-id="41d57-213">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="41d57-214">Não</span><span class="sxs-lookup"><span data-stu-id="41d57-214">No</span></span> |

<span data-ttu-id="41d57-215">Se hello **sqlReaderQuery** é especificada para Olá SqlSource, hello atividade de cópia executa esta consulta em relação aos dados de Olá Olá banco de dados do SQL Server fonte tooget.</span><span class="sxs-lookup"><span data-stu-id="41d57-215">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span>

<span data-ttu-id="41d57-216">Como alternativa, você pode especificar um procedimento armazenado especificando Olá **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello procedimento armazenado usa parâmetros).</span><span class="sxs-lookup"><span data-stu-id="41d57-216">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="41d57-217">Se você não especificar sqlReaderQuery ou sqlReaderStoredProcedureName, colunas de Olá definidas na seção de estrutura hello são usada toobuild toorun uma consulta select contra Olá banco de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="41d57-217">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="41d57-218">Se definição de conjunto de dados de saudação não tem estrutura Olá, todas as colunas da tabela de hello estão selecionadas.</span><span class="sxs-lookup"><span data-stu-id="41d57-218">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="41d57-219">Quando você usa **sqlReaderStoredProcedureName**, você ainda precisa toospecify um valor para Olá **tableName** propriedade no conjunto de dados Olá JSON.</span><span class="sxs-lookup"><span data-stu-id="41d57-219">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="41d57-220">Contudo, não há nenhuma validação executada nessa tabela.</span><span class="sxs-lookup"><span data-stu-id="41d57-220">There are no validations performed against this table though.</span></span>

### <a name="sqlsink"></a><span data-ttu-id="41d57-221">SqlSink</span><span class="sxs-lookup"><span data-stu-id="41d57-221">SqlSink</span></span>
<span data-ttu-id="41d57-222">**SqlSink** dá suporte a saudação propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="41d57-222">**SqlSink** supports hello following properties:</span></span>

| <span data-ttu-id="41d57-223">Propriedade</span><span class="sxs-lookup"><span data-stu-id="41d57-223">Property</span></span> | <span data-ttu-id="41d57-224">Descrição</span><span class="sxs-lookup"><span data-stu-id="41d57-224">Description</span></span> | <span data-ttu-id="41d57-225">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="41d57-225">Allowed values</span></span> | <span data-ttu-id="41d57-226">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="41d57-226">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="41d57-227">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="41d57-227">writeBatchTimeout</span></span> |<span data-ttu-id="41d57-228">Tempo de espera para Olá toocomplete de operação de inserção de lote antes de expirar.</span><span class="sxs-lookup"><span data-stu-id="41d57-228">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="41d57-229">timespan</span><span class="sxs-lookup"><span data-stu-id="41d57-229">timespan</span></span><br/><br/> <span data-ttu-id="41d57-230">Exemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="41d57-230">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="41d57-231">Não</span><span class="sxs-lookup"><span data-stu-id="41d57-231">No</span></span> |
| <span data-ttu-id="41d57-232">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="41d57-232">writeBatchSize</span></span> |<span data-ttu-id="41d57-233">Insere dados na tabela do SQL hello quando o tamanho do buffer de saudação atingir writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="41d57-233">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="41d57-234">Inteiro (número de linhas)</span><span class="sxs-lookup"><span data-stu-id="41d57-234">Integer (number of rows)</span></span> |<span data-ttu-id="41d57-235">Não (padrão: 10000)</span><span class="sxs-lookup"><span data-stu-id="41d57-235">No (default: 10000)</span></span> |
| <span data-ttu-id="41d57-236">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="41d57-236">sqlWriterCleanupScript</span></span> |<span data-ttu-id="41d57-237">Especifique a consulta para a atividade de cópia tooexecute, de modo que os dados de uma fatia específica é limpa.</span><span class="sxs-lookup"><span data-stu-id="41d57-237">Specify query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="41d57-238">Para obter mais informações, consulte a seção [Cópia repetida](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="41d57-238">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="41d57-239">Uma instrução de consulta.</span><span class="sxs-lookup"><span data-stu-id="41d57-239">A query statement.</span></span> |<span data-ttu-id="41d57-240">Não</span><span class="sxs-lookup"><span data-stu-id="41d57-240">No</span></span> |
| <span data-ttu-id="41d57-241">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="41d57-241">sliceIdentifierColumnName</span></span> |<span data-ttu-id="41d57-242">Especifique o nome de coluna para a atividade de cópia toofill com identificador de fatia gerado automaticamente, que é usado tooclean os dados de uma fatia específica quando executada novamente.</span><span class="sxs-lookup"><span data-stu-id="41d57-242">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="41d57-243">Para obter mais informações, consulte a seção [Cópia repetida](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="41d57-243">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="41d57-244">Nome de uma coluna com tipo de dados de binário (32).</span><span class="sxs-lookup"><span data-stu-id="41d57-244">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="41d57-245">Não</span><span class="sxs-lookup"><span data-stu-id="41d57-245">No</span></span> |
| <span data-ttu-id="41d57-246">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="41d57-246">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="41d57-247">Nome do hello procedimento armazenado dados upserts (atualizações/inserções) na tabela de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="41d57-247">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="41d57-248">Nome da saudação de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="41d57-248">Name of hello stored procedure.</span></span> |<span data-ttu-id="41d57-249">Não</span><span class="sxs-lookup"><span data-stu-id="41d57-249">No</span></span> |
| <span data-ttu-id="41d57-250">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="41d57-250">storedProcedureParameters</span></span> |<span data-ttu-id="41d57-251">Parâmetros de saudação de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="41d57-251">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="41d57-252">Pares de nome/valor.</span><span class="sxs-lookup"><span data-stu-id="41d57-252">Name/value pairs.</span></span> <span data-ttu-id="41d57-253">Nomes e o uso de maiusculas e minúsculas dos parâmetros devem corresponder a nomes de saudação e uso de maiusculas e minúsculas dos parâmetros de procedimento armazenado de saudação.</span><span class="sxs-lookup"><span data-stu-id="41d57-253">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="41d57-254">Não</span><span class="sxs-lookup"><span data-stu-id="41d57-254">No</span></span> |
| <span data-ttu-id="41d57-255">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="41d57-255">sqlWriterTableType</span></span> |<span data-ttu-id="41d57-256">Especifique toobe de nome de tipo de tabela usado no procedimento armazenado de saudação.</span><span class="sxs-lookup"><span data-stu-id="41d57-256">Specify table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="41d57-257">Atividade de cópia disponibiliza dados Olá movidos em uma tabela temporária com esse tipo de tabela.</span><span class="sxs-lookup"><span data-stu-id="41d57-257">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="41d57-258">Código do procedimento armazenado, em seguida, pode mesclar dados de saudação sejam copiados com os dados existentes.</span><span class="sxs-lookup"><span data-stu-id="41d57-258">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="41d57-259">Um nome de tipo de tabela.</span><span class="sxs-lookup"><span data-stu-id="41d57-259">A table type name.</span></span> |<span data-ttu-id="41d57-260">Não</span><span class="sxs-lookup"><span data-stu-id="41d57-260">No</span></span> |


## <a name="json-examples-for-copying-data-from-and-toosql-server"></a><span data-ttu-id="41d57-261">Exemplos JSON para copiar dados do e tooSQL Server</span><span class="sxs-lookup"><span data-stu-id="41d57-261">JSON examples for copying data from and tooSQL Server</span></span>
<span data-ttu-id="41d57-262">Olá, exemplos a seguir fornecem as definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="41d57-262">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="41d57-263">Olá seguintes exemplos mostram como toocopy tooand de dados do SQL Server e o armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="41d57-263">hello following samples show how toocopy data tooand from SQL Server and Azure Blob Storage.</span></span> <span data-ttu-id="41d57-264">No entanto, os dados podem ser copiados **diretamente** de qualquer uma das fontes tooany de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="41d57-264">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>     

## <a name="example-copy-data-from-sql-server-tooazure-blob"></a><span data-ttu-id="41d57-265">Exemplo: Copiar dados do SQL Server tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="41d57-265">Example: Copy data from SQL Server tooAzure Blob</span></span>
<span data-ttu-id="41d57-266">Olá mostra de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="41d57-266">hello following sample shows:</span></span>

1. <span data-ttu-id="41d57-267">Um serviço vinculado do tipo [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="41d57-267">A linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="41d57-268">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="41d57-268">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="41d57-269">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [SqlServerTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="41d57-269">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](#dataset-properties).</span></span>
4. <span data-ttu-id="41d57-270">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="41d57-270">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="41d57-271">Olá [pipeline](data-factory-create-pipelines.md) com atividade de cópia que usa [SqlSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="41d57-271">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="41d57-272">exemplo Hello copia dados de série temporal de um tooan de tabela do SQL Server BLOBs do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="41d57-272">hello sample copies time-series data from a SQL Server table tooan Azure blob every hour.</span></span> <span data-ttu-id="41d57-273">propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="41d57-273">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="41d57-274">Como uma primeira etapa, configure o gateway de gerenciamento de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="41d57-274">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="41d57-275">Olá instruções são Olá [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="41d57-275">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="41d57-276">**Serviço vinculado do SQL Server**</span><span class="sxs-lookup"><span data-stu-id="41d57-276">**SQL Server linked service**</span></span>
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
<span data-ttu-id="41d57-277">**Serviço vinculado do armazenamento de Blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="41d57-277">**Azure Blob storage linked service**</span></span>

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
<span data-ttu-id="41d57-278">**Conjunto de dados de entrada do SQL Server**</span><span class="sxs-lookup"><span data-stu-id="41d57-278">**SQL Server input dataset**</span></span>

<span data-ttu-id="41d57-279">exemplo Hello supõe que você criou uma tabela "MyTable" no SQL Server e contém uma coluna chamada "timestampcolumn" para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="41d57-279">hello sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="41d57-280">Você pode consultar em várias tabelas em Olá mesmo usando um único conjunto de dados, mas uma única tabela de banco de dados deve ser usado para typeProperty de tableName de saudação do dataset.</span><span class="sxs-lookup"><span data-stu-id="41d57-280">You can query over multiple tables within hello same database using a single dataset, but a single table must be used for hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="41d57-281">Definindo "externo": "verdadeiro" informa o serviço de fábrica de dados Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="41d57-281">Setting “external”: ”true” informs Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="41d57-282">**Conjunto de dados de saída de Blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="41d57-282">**Azure Blob output dataset**</span></span>

<span data-ttu-id="41d57-283">Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="41d57-283">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="41d57-284">caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="41d57-284">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="41d57-285">caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.</span><span class="sxs-lookup"><span data-stu-id="41d57-285">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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
<span data-ttu-id="41d57-286">**Pipeline com Atividade de cópia**</span><span class="sxs-lookup"><span data-stu-id="41d57-286">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="41d57-287">pipeline de saudação contém uma atividade de cópia que esteja configurado toouse esses conjuntos de dados de entrada e saídos e toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="41d57-287">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="41d57-288">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**SqlSource** e **coletor** tipo está definido muito**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="41d57-288">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="41d57-289">consulta SQL Olá especificada para Olá **SqlReaderQuery** propriedade seleciona dados Olá Olá após toocopy de hora.</span><span class="sxs-lookup"><span data-stu-id="41d57-289">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

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
<span data-ttu-id="41d57-290">Neste exemplo, **sqlReaderQuery** é especificado para Olá SqlSource.</span><span class="sxs-lookup"><span data-stu-id="41d57-290">In this example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="41d57-291">Hello atividade de cópia executa esta consulta Olá dados do banco de dados do SQL Server origem tooget hello.</span><span class="sxs-lookup"><span data-stu-id="41d57-291">hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span> <span data-ttu-id="41d57-292">Como alternativa, você pode especificar um procedimento armazenado especificando Olá **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello procedimento armazenado usa parâmetros).</span><span class="sxs-lookup"><span data-stu-id="41d57-292">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span> <span data-ttu-id="41d57-293">Olá sqlReaderQuery pode fazer referência a várias tabelas no banco de dados de saudação referenciado pelo conjunto de dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="41d57-293">hello sqlReaderQuery can reference multiple tables within hello database referenced by hello input dataset.</span></span> <span data-ttu-id="41d57-294">Ele não é limitado tooonly Olá definido como Olá typeProperty de tableName do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="41d57-294">It is not limited tooonly hello table set as hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="41d57-295">Se você não especificar sqlReaderQuery ou sqlReaderStoredProcedureName, colunas de Olá definidas na seção de estrutura hello são usada toobuild toorun uma consulta select contra Olá banco de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="41d57-295">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="41d57-296">Se definição de conjunto de dados de saudação não tem estrutura Olá, todas as colunas da tabela de hello estão selecionadas.</span><span class="sxs-lookup"><span data-stu-id="41d57-296">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="41d57-297">Consulte Olá [fonte Sql](#sqlsource) seção e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) para lista de saudação de propriedades com suporte SqlSource e BlobSink.</span><span class="sxs-lookup"><span data-stu-id="41d57-297">See hello [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSource and BlobSink.</span></span>

## <a name="example-copy-data-from-azure-blob-toosql-server"></a><span data-ttu-id="41d57-298">Exemplo: Copiar dados de Blob do Azure tooSQL Server</span><span class="sxs-lookup"><span data-stu-id="41d57-298">Example: Copy data from Azure Blob tooSQL Server</span></span>
<span data-ttu-id="41d57-299">Olá mostra de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="41d57-299">hello following sample shows:</span></span>

1. <span data-ttu-id="41d57-300">Olá vinculado de serviço do tipo [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="41d57-300">hello linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="41d57-301">Olá vinculado de serviço do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="41d57-301">hello linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="41d57-302">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="41d57-302">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="41d57-303">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="41d57-303">An output [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="41d57-304">Olá [pipeline](data-factory-create-pipelines.md) com atividade de cópia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [SqlSink](#sql-server-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="41d57-304">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#sql-server-copy-activity-type-properties).</span></span>

<span data-ttu-id="41d57-305">exemplo Hello copia dados de série de tempo de uma tabela do SQL Server tooa BLOBs do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="41d57-305">hello sample copies time-series data from an Azure blob tooa SQL Server table every hour.</span></span> <span data-ttu-id="41d57-306">propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="41d57-306">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="41d57-307">**Serviço vinculado do SQL Server**</span><span class="sxs-lookup"><span data-stu-id="41d57-307">**SQL Server linked service**</span></span>

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
<span data-ttu-id="41d57-308">**Serviço vinculado do armazenamento de Blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="41d57-308">**Azure Blob storage linked service**</span></span>

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
<span data-ttu-id="41d57-309">**Conjunto de dados de entrada de Blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="41d57-309">**Azure Blob input dataset**</span></span>

<span data-ttu-id="41d57-310">Os dados são coletados de um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="41d57-310">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="41d57-311">Olá pasta caminho e nome de arquivo para blob Olá são avaliados dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="41d57-311">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="41d57-312">caminho da pasta Olá usa year, month e parte do dia da hora de início da saudação e nome do arquivo usa a parte de hora Olá Olá da hora de início.</span><span class="sxs-lookup"><span data-stu-id="41d57-312">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="41d57-313">"externo": "verdadeira" configuração informa o serviço de fábrica de dados de Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="41d57-313">“external”: “true” setting informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="41d57-314">**Conjunto de dados de saída do SQL Server**</span><span class="sxs-lookup"><span data-stu-id="41d57-314">**SQL Server output dataset**</span></span>

<span data-ttu-id="41d57-315">exemplo Hello copiará a tabela de tooa de dados denominada "MyTable" no SQL Server.</span><span class="sxs-lookup"><span data-stu-id="41d57-315">hello sample copies data tooa table named “MyTable” in SQL Server.</span></span> <span data-ttu-id="41d57-316">Criar tabela Olá no SQL Server com hello mesmo número de colunas, conforme o esperado toocontain de arquivo CSV de Blob hello.</span><span class="sxs-lookup"><span data-stu-id="41d57-316">Create hello table in SQL Server with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="41d57-317">Novas linhas são adicionadas a tabela de toohello a cada hora.</span><span class="sxs-lookup"><span data-stu-id="41d57-317">New rows are added toohello table every hour.</span></span>

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
<span data-ttu-id="41d57-318">**Pipeline com Atividade de cópia**</span><span class="sxs-lookup"><span data-stu-id="41d57-318">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="41d57-319">pipeline de saudação contém uma atividade de cópia que esteja configurado toouse esses conjuntos de dados de entrada e saídos e toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="41d57-319">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="41d57-320">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**BlobSource** e **coletor** tipo está definido muito**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="41d57-320">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

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

## <a name="troubleshooting-connection-issues"></a><span data-ttu-id="41d57-321">Solucionar problemas de conexão</span><span class="sxs-lookup"><span data-stu-id="41d57-321">Troubleshooting connection issues</span></span>
1. <span data-ttu-id="41d57-322">Configure as conexões remotas de tooaccept do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="41d57-322">Configure your SQL Server tooaccept remote connections.</span></span> <span data-ttu-id="41d57-323">Inicie o **SQL Server Management Studio**, clique com o botão direito do mouse em **servidor** e clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="41d57-323">Launch **SQL Server Management Studio**, right-click **server**, and click **Properties**.</span></span> <span data-ttu-id="41d57-324">Selecione **conexões** na lista de saudação e seleção **server do permitir conexões remotas toohello**.</span><span class="sxs-lookup"><span data-stu-id="41d57-324">Select **Connections** from hello list and check **Allow remote connections toohello server**.</span></span>

    ![Habilitar conexões remotas](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    <span data-ttu-id="41d57-326">Consulte [configurar o acesso remoto de saudação opção de configuração do servidor](https://msdn.microsoft.com/library/ms191464.aspx) para obter etapas detalhadas.</span><span class="sxs-lookup"><span data-stu-id="41d57-326">See [Configure hello remote access Server Configuration Option](https://msdn.microsoft.com/library/ms191464.aspx) for detailed steps.</span></span>
2. <span data-ttu-id="41d57-327">Inicie o **SQL Server Configuration Manager**(Gerenciador de Configuração do SQL Server).</span><span class="sxs-lookup"><span data-stu-id="41d57-327">Launch **SQL Server Configuration Manager**.</span></span> <span data-ttu-id="41d57-328">Expanda **configuração de rede do SQL Server** para Olá instância você deseja e selecione **protocolos para MSSQLSERVER**.</span><span class="sxs-lookup"><span data-stu-id="41d57-328">Expand **SQL Server Network Configuration** for hello instance you want, and select **Protocols for MSSQLSERVER**.</span></span> <span data-ttu-id="41d57-329">Você deve ver os protocolos no painel direito de saudação.</span><span class="sxs-lookup"><span data-stu-id="41d57-329">You should see protocols in hello right-pane.</span></span> <span data-ttu-id="41d57-330">Habilite o TCP/IP clicando com o botão direito do mouse em **TCP/IP** e clicando em **Habilitar**.</span><span class="sxs-lookup"><span data-stu-id="41d57-330">Enable TCP/IP by right-clicking **TCP/IP** and clicking **Enable**.</span></span>

    ![Habilitar TCP/IP](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    <span data-ttu-id="41d57-332">Veja [Habilitar ou Desabilitar um Protocolo de Rede do Servidor](https://msdn.microsoft.com/library/ms191294.aspx) para ver detalhes e formas alternativas de habilitar um protocolo TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="41d57-332">See [Enable or Disable a Server Network Protocol](https://msdn.microsoft.com/library/ms191294.aspx) for details and alternate ways of enabling TCP/IP protocol.</span></span>
3. <span data-ttu-id="41d57-333">No hello mesma janela, clique duas vezes em **TCP/IP** toolaunch **propriedades de TCP/IP** janela.</span><span class="sxs-lookup"><span data-stu-id="41d57-333">In hello same window, double-click **TCP/IP** toolaunch **TCP/IP Properties** window.</span></span>
4. <span data-ttu-id="41d57-334">Alternar toohello **endereços IP** guia. Role para baixo toosee **IPAll** seção.</span><span class="sxs-lookup"><span data-stu-id="41d57-334">Switch toohello **IP Addresses** tab. Scroll down toosee **IPAll** section.</span></span> <span data-ttu-id="41d57-335">Anote hello * * porta TCP * * (o padrão é **1433**).</span><span class="sxs-lookup"><span data-stu-id="41d57-335">Note down hello **TCP Port **(default is **1433**).</span></span>
5. <span data-ttu-id="41d57-336">Criar um **regra de Firewall do Windows de saudação** no hello máquina tooallow tráfego de entrada por essa porta.</span><span class="sxs-lookup"><span data-stu-id="41d57-336">Create a **rule for hello Windows Firewall** on hello machine tooallow incoming traffic through this port.</span></span>  
6. <span data-ttu-id="41d57-337">**Verifique se a conexão**: tooconnect toohello SQL Server usando o nome totalmente qualificado, use o SQL Server Management Studio em uma máquina diferente.</span><span class="sxs-lookup"><span data-stu-id="41d57-337">**Verify connection**: tooconnect toohello SQL Server using fully qualified name, use SQL Server Management Studio from a different machine.</span></span> <span data-ttu-id="41d57-338">Por exemplo: “<machine><domain>.corp<company>.com,1433”.</span><span class="sxs-lookup"><span data-stu-id="41d57-338">For example: "<machine>.<domain>.corp.<company>.com,1433."</span></span>

   > [!IMPORTANT]

   > <span data-ttu-id="41d57-339">Consulte [mover dados entre fontes locais e na nuvem de saudação com Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) para obter informações detalhadas.</span><span class="sxs-lookup"><span data-stu-id="41d57-339">See [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for detailed information.</span></span>
   >
   > <span data-ttu-id="41d57-340">Consulte [Solucionar problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para ver dicas sobre como solucionar os problemas relacionados à conexão/gateway.</span><span class="sxs-lookup"><span data-stu-id="41d57-340">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>
   >
   >


## <a name="identity-columns-in-hello-target-database"></a><span data-ttu-id="41d57-341">Colunas de identidade no banco de dados de destino Olá</span><span class="sxs-lookup"><span data-stu-id="41d57-341">Identity columns in hello target database</span></span>
<span data-ttu-id="41d57-342">Esta seção fornece um exemplo que copia dados de uma tabela de origem com nenhuma tabela de destino identidade coluna tooa com uma coluna de identidade.</span><span class="sxs-lookup"><span data-stu-id="41d57-342">This section provides an example that copies data from a source table with no identity column tooa destination table with an identity column.</span></span>

<span data-ttu-id="41d57-343">**Tabela de origem:**</span><span class="sxs-lookup"><span data-stu-id="41d57-343">**Source table:**</span></span>

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="41d57-344">**Tabela de destino:**</span><span class="sxs-lookup"><span data-stu-id="41d57-344">**Destination table:**</span></span>

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

<span data-ttu-id="41d57-345">Observe que essa tabela de destino Olá tem uma coluna de identidade.</span><span class="sxs-lookup"><span data-stu-id="41d57-345">Notice that hello target table has an identity column.</span></span>

<span data-ttu-id="41d57-346">**Definição de JSON do conjunto de dados de origem**</span><span class="sxs-lookup"><span data-stu-id="41d57-346">**Source dataset JSON definition**</span></span>

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
<span data-ttu-id="41d57-347">**Definição de JSON do conjunto de dados de destino**</span><span class="sxs-lookup"><span data-stu-id="41d57-347">**Destination dataset JSON definition**</span></span>

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

<span data-ttu-id="41d57-348">Observe que sua tabela de origem e de destino têm um esquema diferente (a de destino tem uma coluna adicional com identidade).</span><span class="sxs-lookup"><span data-stu-id="41d57-348">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="41d57-349">Nesse cenário, você precisa toospecify **estrutura** propriedade na definição de conjunto de dados de destino hello, que não inclui a coluna de identidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="41d57-349">In this scenario, you need toospecify **structure** property in hello target dataset definition, which doesn’t include hello identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="41d57-350">Invocar o procedimento armazenado do coletor SQL</span><span class="sxs-lookup"><span data-stu-id="41d57-350">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="41d57-351">Para obter um exemplo de como invocar um procedimento armazenado do coletor SQL em uma atividade de cópia de um pipeline, confira o artigo [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) (Invocar procedimento armazenado para coletor SQL na atividade de cópia).</span><span class="sxs-lookup"><span data-stu-id="41d57-351">See [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article for an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline.</span></span>

## <a name="type-mapping-for-sql-server"></a><span data-ttu-id="41d57-352">Mapeamento de tipo para o SQL Server</span><span class="sxs-lookup"><span data-stu-id="41d57-352">Type mapping for SQL server</span></span>
<span data-ttu-id="41d57-353">Conforme mencionado em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, hello atividade de cópia executa conversões de tipo automática tipos toosink de tipos de origem com hello abordagem 2 etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="41d57-353">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="41d57-354">Converter nativo tipos too.NET do tipo de origem</span><span class="sxs-lookup"><span data-stu-id="41d57-354">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="41d57-355">Converter do tipo de coletor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="41d57-355">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="41d57-356">Quando a movimentação de dados muito & do SQL server, Olá mapeamentos a seguir são usados do tipo SQL de too.NET e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="41d57-356">When moving data too& from SQL server, hello following mappings are used from SQL type too.NET type and vice versa.</span></span>

<span data-ttu-id="41d57-357">mapeamento de saudação é igual a saudação mapeamento de tipo de dados do SQL Server do ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="41d57-357">hello mapping is same as hello SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="41d57-358">Tipo de mecanismo do Banco de Dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="41d57-358">SQL Server Database Engine type</span></span> | <span data-ttu-id="41d57-359">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="41d57-359">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="41d57-360">bigint</span><span class="sxs-lookup"><span data-stu-id="41d57-360">bigint</span></span> |<span data-ttu-id="41d57-361">Int64</span><span class="sxs-lookup"><span data-stu-id="41d57-361">Int64</span></span> |
| <span data-ttu-id="41d57-362">binário</span><span class="sxs-lookup"><span data-stu-id="41d57-362">binary</span></span> |<span data-ttu-id="41d57-363">Byte[]</span><span class="sxs-lookup"><span data-stu-id="41d57-363">Byte[]</span></span> |
| <span data-ttu-id="41d57-364">bit</span><span class="sxs-lookup"><span data-stu-id="41d57-364">bit</span></span> |<span data-ttu-id="41d57-365">Booliano</span><span class="sxs-lookup"><span data-stu-id="41d57-365">Boolean</span></span> |
| <span data-ttu-id="41d57-366">char</span><span class="sxs-lookup"><span data-stu-id="41d57-366">char</span></span> |<span data-ttu-id="41d57-367">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="41d57-367">String, Char[]</span></span> |
| <span data-ttu-id="41d57-368">data</span><span class="sxs-lookup"><span data-stu-id="41d57-368">date</span></span> |<span data-ttu-id="41d57-369">DateTime</span><span class="sxs-lookup"><span data-stu-id="41d57-369">DateTime</span></span> |
| <span data-ttu-id="41d57-370">DateTime</span><span class="sxs-lookup"><span data-stu-id="41d57-370">Datetime</span></span> |<span data-ttu-id="41d57-371">DateTime</span><span class="sxs-lookup"><span data-stu-id="41d57-371">DateTime</span></span> |
| <span data-ttu-id="41d57-372">datetime2</span><span class="sxs-lookup"><span data-stu-id="41d57-372">datetime2</span></span> |<span data-ttu-id="41d57-373">DateTime</span><span class="sxs-lookup"><span data-stu-id="41d57-373">DateTime</span></span> |
| <span data-ttu-id="41d57-374">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="41d57-374">Datetimeoffset</span></span> |<span data-ttu-id="41d57-375">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="41d57-375">DateTimeOffset</span></span> |
| <span data-ttu-id="41d57-376">Decimal</span><span class="sxs-lookup"><span data-stu-id="41d57-376">Decimal</span></span> |<span data-ttu-id="41d57-377">Decimal</span><span class="sxs-lookup"><span data-stu-id="41d57-377">Decimal</span></span> |
| <span data-ttu-id="41d57-378">Atributo FILESTREAM (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="41d57-378">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="41d57-379">Byte[]</span><span class="sxs-lookup"><span data-stu-id="41d57-379">Byte[]</span></span> |
| <span data-ttu-id="41d57-380">Float</span><span class="sxs-lookup"><span data-stu-id="41d57-380">Float</span></span> |<span data-ttu-id="41d57-381">Duplo</span><span class="sxs-lookup"><span data-stu-id="41d57-381">Double</span></span> |
| <span data-ttu-id="41d57-382">imagem</span><span class="sxs-lookup"><span data-stu-id="41d57-382">image</span></span> |<span data-ttu-id="41d57-383">Byte[]</span><span class="sxs-lookup"><span data-stu-id="41d57-383">Byte[]</span></span> |
| <span data-ttu-id="41d57-384">int</span><span class="sxs-lookup"><span data-stu-id="41d57-384">int</span></span> |<span data-ttu-id="41d57-385">Int32</span><span class="sxs-lookup"><span data-stu-id="41d57-385">Int32</span></span> |
| <span data-ttu-id="41d57-386">money</span><span class="sxs-lookup"><span data-stu-id="41d57-386">money</span></span> |<span data-ttu-id="41d57-387">Decimal</span><span class="sxs-lookup"><span data-stu-id="41d57-387">Decimal</span></span> |
| <span data-ttu-id="41d57-388">nchar</span><span class="sxs-lookup"><span data-stu-id="41d57-388">nchar</span></span> |<span data-ttu-id="41d57-389">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="41d57-389">String, Char[]</span></span> |
| <span data-ttu-id="41d57-390">ntext</span><span class="sxs-lookup"><span data-stu-id="41d57-390">ntext</span></span> |<span data-ttu-id="41d57-391">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="41d57-391">String, Char[]</span></span> |
| <span data-ttu-id="41d57-392">numérico</span><span class="sxs-lookup"><span data-stu-id="41d57-392">numeric</span></span> |<span data-ttu-id="41d57-393">Decimal</span><span class="sxs-lookup"><span data-stu-id="41d57-393">Decimal</span></span> |
| <span data-ttu-id="41d57-394">nvarchar</span><span class="sxs-lookup"><span data-stu-id="41d57-394">nvarchar</span></span> |<span data-ttu-id="41d57-395">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="41d57-395">String, Char[]</span></span> |
| <span data-ttu-id="41d57-396">real</span><span class="sxs-lookup"><span data-stu-id="41d57-396">real</span></span> |<span data-ttu-id="41d57-397">Single</span><span class="sxs-lookup"><span data-stu-id="41d57-397">Single</span></span> |
| <span data-ttu-id="41d57-398">rowversion</span><span class="sxs-lookup"><span data-stu-id="41d57-398">rowversion</span></span> |<span data-ttu-id="41d57-399">Byte[]</span><span class="sxs-lookup"><span data-stu-id="41d57-399">Byte[]</span></span> |
| <span data-ttu-id="41d57-400">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="41d57-400">smalldatetime</span></span> |<span data-ttu-id="41d57-401">DateTime</span><span class="sxs-lookup"><span data-stu-id="41d57-401">DateTime</span></span> |
| <span data-ttu-id="41d57-402">smallint</span><span class="sxs-lookup"><span data-stu-id="41d57-402">smallint</span></span> |<span data-ttu-id="41d57-403">Int16</span><span class="sxs-lookup"><span data-stu-id="41d57-403">Int16</span></span> |
| <span data-ttu-id="41d57-404">smallmoney</span><span class="sxs-lookup"><span data-stu-id="41d57-404">smallmoney</span></span> |<span data-ttu-id="41d57-405">Decimal</span><span class="sxs-lookup"><span data-stu-id="41d57-405">Decimal</span></span> |
| <span data-ttu-id="41d57-406">sql_variant</span><span class="sxs-lookup"><span data-stu-id="41d57-406">sql_variant</span></span> |<span data-ttu-id="41d57-407">Objeto *</span><span class="sxs-lookup"><span data-stu-id="41d57-407">Object *</span></span> |
| <span data-ttu-id="41d57-408">texto</span><span class="sxs-lookup"><span data-stu-id="41d57-408">text</span></span> |<span data-ttu-id="41d57-409">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="41d57-409">String, Char[]</span></span> |
| <span data-ttu-id="41d57-410">tempo real</span><span class="sxs-lookup"><span data-stu-id="41d57-410">time</span></span> |<span data-ttu-id="41d57-411">timespan</span><span class="sxs-lookup"><span data-stu-id="41d57-411">TimeSpan</span></span> |
| <span data-ttu-id="41d57-412">timestamp</span><span class="sxs-lookup"><span data-stu-id="41d57-412">timestamp</span></span> |<span data-ttu-id="41d57-413">Byte[]</span><span class="sxs-lookup"><span data-stu-id="41d57-413">Byte[]</span></span> |
| <span data-ttu-id="41d57-414">tinyint</span><span class="sxs-lookup"><span data-stu-id="41d57-414">tinyint</span></span> |<span data-ttu-id="41d57-415">Byte</span><span class="sxs-lookup"><span data-stu-id="41d57-415">Byte</span></span> |
| <span data-ttu-id="41d57-416">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="41d57-416">uniqueidentifier</span></span> |<span data-ttu-id="41d57-417">Guid</span><span class="sxs-lookup"><span data-stu-id="41d57-417">Guid</span></span> |
| <span data-ttu-id="41d57-418">varbinary</span><span class="sxs-lookup"><span data-stu-id="41d57-418">varbinary</span></span> |<span data-ttu-id="41d57-419">Byte[]</span><span class="sxs-lookup"><span data-stu-id="41d57-419">Byte[]</span></span> |
| <span data-ttu-id="41d57-420">varchar</span><span class="sxs-lookup"><span data-stu-id="41d57-420">varchar</span></span> |<span data-ttu-id="41d57-421">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="41d57-421">String, Char[]</span></span> |
| <span data-ttu-id="41d57-422">xml</span><span class="sxs-lookup"><span data-stu-id="41d57-422">xml</span></span> |<span data-ttu-id="41d57-423">xml</span><span class="sxs-lookup"><span data-stu-id="41d57-423">Xml</span></span> |

## <a name="mapping-source-toosink-columns"></a><span data-ttu-id="41d57-424">Mapeamento de colunas da fonte de toosink</span><span class="sxs-lookup"><span data-stu-id="41d57-424">Mapping source toosink columns</span></span>
<span data-ttu-id="41d57-425">colunas de toomap de toocolumns de conjunto de dados de origem do conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="41d57-425">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="41d57-426">Cópia repetida</span><span class="sxs-lookup"><span data-stu-id="41d57-426">Repeatable copy</span></span>
<span data-ttu-id="41d57-427">Ao copiar dados tooSQL banco de dados do servidor, atividade de cópia de saudação acrescenta a tabela de dados do coletor toohello por padrão.</span><span class="sxs-lookup"><span data-stu-id="41d57-427">When copying data tooSQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="41d57-428">em vez disso, consulte tooperform um UPSERT [tooSqlSink gravação Repeatable](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) artigo.</span><span class="sxs-lookup"><span data-stu-id="41d57-428">tooperform an UPSERT instead,  See [Repeatable write tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="41d57-429">Ao copiar dados de armazenamentos de dados relacional, manter a capacidade de repetição em mente tooavoid resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="41d57-429">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="41d57-430">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="41d57-430">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="41d57-431">Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="41d57-431">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="41d57-432">Quando uma fatia é executado novamente em qualquer modo, você precisa toomake-se de que Olá os mesmos dados é lido como não importa quantas vezes uma fatia é executada.</span><span class="sxs-lookup"><span data-stu-id="41d57-432">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="41d57-433">Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="41d57-433">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="41d57-434">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="41d57-434">Performance and Tuning</span></span>
<span data-ttu-id="41d57-435">Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.</span><span class="sxs-lookup"><span data-stu-id="41d57-435">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
