---
title: "Tutorial: API de REST de uso toocreate um pipeline da fábrica de dados do Azure | Microsoft Docs"
description: "Neste tutorial, você usar a API REST toocreate um pipeline da fábrica de dados do Azure com um dado de toocopy de atividade de cópia de um armazenamento de BLOBs do Azure, um banco de dados do SQL Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1704cdf8-30ad-49bc-a71c-4057e26e7350
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: aa6c9b035101c4ff9acff90117ca6e3e7067f418
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-rest-api-toocreate-an-azure-data-factory-pipeline-toocopy-data"></a><span data-ttu-id="07533-103">Tutorial: API de REST de uso toocreate um Azure Data Factory pipeline toocopy de dados</span><span class="sxs-lookup"><span data-stu-id="07533-103">Tutorial: Use REST API toocreate an Azure Data Factory pipeline toocopy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="07533-104">Visão geral e pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="07533-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="07533-105">Assistente de Cópia</span><span class="sxs-lookup"><span data-stu-id="07533-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="07533-106">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="07533-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="07533-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="07533-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="07533-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="07533-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="07533-109">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="07533-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="07533-110">API REST</span><span class="sxs-lookup"><span data-stu-id="07533-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="07533-111">API do .NET</span><span class="sxs-lookup"><span data-stu-id="07533-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="07533-112">Neste artigo, você aprenderá como toouse REST API toocreate uma fábrica de dados com um pipeline que copia dados de um banco de dados de SQL do Azure de tooan do armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="07533-112">In this article, you learn how toouse REST API toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="07533-113">Se você estiver tooAzure nova fábrica de dados, leia Olá [tooAzure Introdução Data Factory](data-factory-introduction.md) artigo antes de fazer este tutorial.</span><span class="sxs-lookup"><span data-stu-id="07533-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="07533-114">Neste tutorial, você criará um pipeline com uma atividade: atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="07533-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="07533-115">Olá Copiar atividade copia dados de um repositório de dados com suporte de dados repositório tooa coletor com suporte.</span><span class="sxs-lookup"><span data-stu-id="07533-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="07533-116">Para obter uma lista de armazenamentos de dados com suporte como origens e coletores, confira [Armazenamentos de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="07533-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="07533-117">atividade de saudação é alimentada por um serviço disponível globalmente que pode copiar dados entre vários repositórios de dados de forma segura, confiável e escalonável.</span><span class="sxs-lookup"><span data-stu-id="07533-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="07533-118">Para obter mais informações sobre hello atividade de cópia, consulte [atividades de movimentação de dados](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="07533-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="07533-119">Um pipeline pode ter mais de uma atividade.</span><span class="sxs-lookup"><span data-stu-id="07533-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="07533-120">E, é possível encadear duas atividades (executadas uma atividade após o outro), definindo Olá o conjunto de dados de saída de uma atividade Olá outra atividade de conjunto de dados de saudação de entrada.</span><span class="sxs-lookup"><span data-stu-id="07533-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="07533-121">Para saber mais, confira [Várias atividades em um pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="07533-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> <span data-ttu-id="07533-122">Este artigo não aborda todos Olá API de REST de fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="07533-122">This article does not cover all hello Data Factory REST API.</span></span> <span data-ttu-id="07533-123">Confira [Referência de API REST do Data Factory](/rest/api/datafactory/) para obter uma documentação abrangente sobre os cmdlets de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="07533-123">See [Data Factory REST API Reference](/rest/api/datafactory/) for comprehensive documentation on Data Factory cmdlets.</span></span>
>  
> <span data-ttu-id="07533-124">pipeline de dados Olá neste tutorial copia dados de um repositório de dados de destino fonte dados repositório tooa.</span><span class="sxs-lookup"><span data-stu-id="07533-124">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="07533-125">Para obter um tutorial sobre como tootransform dados usando a fábrica de dados do Azure, consulte [Tutorial: Crie um pipeline de dados tootransform usando o cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="07533-125">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07533-126">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="07533-126">Prerequisites</span></span>
* <span data-ttu-id="07533-127">Passar [visão geral do Tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) e hello completa **pré-requisito** etapas.</span><span class="sxs-lookup"><span data-stu-id="07533-127">Go through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="07533-128">Instale o [Curl](https://curl.haxx.se/dlwiz/) em seu computador.</span><span class="sxs-lookup"><span data-stu-id="07533-128">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="07533-129">Use ferramenta de ondulação Olá com REST comandos toocreate uma fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="07533-129">You use hello Curl tool with REST commands toocreate a data factory.</span></span> 
* <span data-ttu-id="07533-130">Siga as instruções [deste artigo](../azure-resource-manager/resource-group-create-service-principal-portal.md) para:</span><span class="sxs-lookup"><span data-stu-id="07533-130">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span> 
  1. <span data-ttu-id="07533-131">Crie um aplicativo Web chamado **ADFCopyTutorialApp** no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="07533-131">Create a Web application named **ADFCopyTutorialApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="07533-132">Obtenha a **ID do cliente** e a **chave secreta**.</span><span class="sxs-lookup"><span data-stu-id="07533-132">Get **client ID** and **secret key**.</span></span> 
  3. <span data-ttu-id="07533-133">Obtenha a **ID do locatário**.</span><span class="sxs-lookup"><span data-stu-id="07533-133">Get **tenant ID**.</span></span> 
  4. <span data-ttu-id="07533-134">Atribuir Olá **ADFCopyTutorialApp** aplicativo toohello **colaborador da fábrica de dados** função.</span><span class="sxs-lookup"><span data-stu-id="07533-134">Assign hello **ADFCopyTutorialApp** application toohello **Data Factory Contributor** role.</span></span>  
* <span data-ttu-id="07533-135">Instale o [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="07533-135">Install [Azure PowerShell](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="07533-136">Iniciar **PowerShell** e Olá seguintes etapas.</span><span class="sxs-lookup"><span data-stu-id="07533-136">Launch **PowerShell** and do hello following steps.</span></span> <span data-ttu-id="07533-137">Mantenha o Azure PowerShell aberta até o fim deste tutorial hello.</span><span class="sxs-lookup"><span data-stu-id="07533-137">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="07533-138">Se você fecha e reabrir o, será necessário comandos de saudação toorun novamente.</span><span class="sxs-lookup"><span data-stu-id="07533-138">If you close and reopen, you need toorun hello commands again.</span></span>
  
  1. <span data-ttu-id="07533-139">Execute Olá comando a seguir e insira o nome de usuário de saudação e a senha que você use toosign em toohello portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="07533-139">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal:</span></span>
    
    ```PowerShell 
    Login-AzureRmAccount
    ```   
  2. <span data-ttu-id="07533-140">Execute todas as assinaturas de saudação para esta conta de Olá tooview de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="07533-140">Run hello following command tooview all hello subscriptions for this account:</span></span>

    ```PowerShell     
    Get-AzureRmSubscription
    ``` 
  3. <span data-ttu-id="07533-141">Execute Olá assinatura de saudação do comando tooselect que você deseja toowork com a seguir.</span><span class="sxs-lookup"><span data-stu-id="07533-141">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="07533-142">Substituir  **&lt;NameOfAzureSubscription** &gt; com o nome da saudação de sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="07533-142">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span> 
     
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
  4. <span data-ttu-id="07533-143">Criar um grupo de recursos do Azure denominado **ADFTutorialResourceGroup** executando Olá comando de saudação do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="07533-143">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell:</span></span>  

    ```PowerShell     
      New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
     
      <span data-ttu-id="07533-144">Se o grupo de recursos Olá já existe, especifique se tooupdate-lo (Y) ou mantê-lo como (N).</span><span class="sxs-lookup"><span data-stu-id="07533-144">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span> 
     
      <span data-ttu-id="07533-145">Algumas das etapas de saudação neste tutorial presumem que você use o grupo de recursos de saudação chamado ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="07533-145">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="07533-146">Se você usar um grupo de recursos diferentes, você precisa toouse nome de saudação do seu grupo de recursos no lugar de ADFTutorialResourceGroup neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="07533-146">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="07533-147">Criar definições JSON</span><span class="sxs-lookup"><span data-stu-id="07533-147">Create JSON definitions</span></span>
<span data-ttu-id="07533-148">Crie arquivos JSON na pasta Olá onde se encontra curl.exe a seguir.</span><span class="sxs-lookup"><span data-stu-id="07533-148">Create following JSON files in hello folder where curl.exe is located.</span></span> 

### <a name="datafactoryjson"></a><span data-ttu-id="07533-149">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="07533-149">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="07533-150">Nome deve ser globalmente exclusivo, portanto, talvez você queira tooprefix/sufixo ADFCopyTutorialDF toomake ele um nome exclusivo.</span><span class="sxs-lookup"><span data-stu-id="07533-150">Name must be globally unique, so you may want tooprefix/suffix ADFCopyTutorialDF toomake it a unique name.</span></span> 
> 
> 

```JSON
{  
    "name": "ADFCopyTutorialDF",  
    "location": "WestUS"
}  
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="07533-151">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="07533-151">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="07533-152">Substitua **nome da conta** e **chave da conta** pelo nome e pela chave da sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="07533-152">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="07533-153">toolearn como tooget seu armazenamento acessar chave, consulte [exibir, copiar e regenerar as contas de armazenamento de chaves de acesso](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="07533-153">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>

```JSON
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

<span data-ttu-id="07533-154">Para obter detalhes sobre as propriedades JSON, confira [Serviço vinculado do Armazenamento do Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span><span class="sxs-lookup"><span data-stu-id="07533-154">For details about JSON properties, see [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span></span>

### <a name="azuersqllinkedservicejson"></a><span data-ttu-id="07533-155">azuersqllinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="07533-155">azuersqllinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="07533-156">Substituir **servername**, **databasename**, **username**, e **senha** com o nome do seu servidor SQL Azure, o nome do banco de dados SQL, usuário conta e senha para conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="07533-156">Replace **servername**, **databasename**, **username**, and **password** with name of your Azure SQL server, name of SQL database, user account, and password for hello account.</span></span>  
> 
>

```JSON
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

<span data-ttu-id="07533-157">Para obter detalhes sobre as propriedades JSON, confira [Serviço vinculado do Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="07533-157">For details about JSON properties, see [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="07533-158">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="07533-158">inputdataset.json</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "structure": [
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "AzureStorageLinkedService",
    "typeProperties": {
      "folderPath": "adftutorial/",
      "fileName": "emp.txt",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ","
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="07533-159">Olá, tabela a seguir fornece descrições para propriedades JSON Olá usadas no trecho hello:</span><span class="sxs-lookup"><span data-stu-id="07533-159">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="07533-160">Propriedade</span><span class="sxs-lookup"><span data-stu-id="07533-160">Property</span></span> | <span data-ttu-id="07533-161">Descrição</span><span class="sxs-lookup"><span data-stu-id="07533-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="07533-162">type</span><span class="sxs-lookup"><span data-stu-id="07533-162">type</span></span> | <span data-ttu-id="07533-163">propriedade do tipo Hello está definida muito**AzureBlob** porque os dados residem em um armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="07533-163">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
| <span data-ttu-id="07533-164">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="07533-164">linkedServiceName</span></span> | <span data-ttu-id="07533-165">Refere-se toohello **AzureStorageLinkedService** que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="07533-165">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="07533-166">folderPath</span><span class="sxs-lookup"><span data-stu-id="07533-166">folderPath</span></span> | <span data-ttu-id="07533-167">Especifica o blob Olá **contêiner** e hello **pasta** que contém blobs de entrada.</span><span class="sxs-lookup"><span data-stu-id="07533-167">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="07533-168">Neste tutorial, adftutorial é o contêiner de blob hello e pasta é a pasta raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="07533-168">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
| <span data-ttu-id="07533-169">fileName</span><span class="sxs-lookup"><span data-stu-id="07533-169">fileName</span></span> | <span data-ttu-id="07533-170">Essa propriedade é opcional.</span><span class="sxs-lookup"><span data-stu-id="07533-170">This property is optional.</span></span> <span data-ttu-id="07533-171">Se você omitir essa propriedade, todos os arquivos de saudação folderPath são escolhidos.</span><span class="sxs-lookup"><span data-stu-id="07533-171">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="07533-172">Neste tutorial, **emp.txt** é especificado para hello fileName, portanto, somente esse arquivo é escolhida para processamento.</span><span class="sxs-lookup"><span data-stu-id="07533-172">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
| <span data-ttu-id="07533-173">formato -> tipo</span><span class="sxs-lookup"><span data-stu-id="07533-173">format -> type</span></span> |<span data-ttu-id="07533-174">arquivo de entrada Hello está no formato de texto de saudação, para que possamos usar **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="07533-174">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
| <span data-ttu-id="07533-175">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="07533-175">columnDelimiter</span></span> | <span data-ttu-id="07533-176">saudação de colunas no arquivo de entrada hello é delimitadas por **caractere de vírgula (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="07533-176">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
| <span data-ttu-id="07533-177">frequência/intervalo</span><span class="sxs-lookup"><span data-stu-id="07533-177">frequency/interval</span></span> | <span data-ttu-id="07533-178">frequência de saudação está definida muito**hora** e o intervalo é definido muito**1**, que significa que Olá entrada fatias estão disponíveis **por hora**.</span><span class="sxs-lookup"><span data-stu-id="07533-178">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="07533-179">Em outras palavras, Olá serviço da fábrica de dados procura por dados de entrada a cada hora na pasta raiz de saudação do contêiner de blob (**adftutorial**) especificado.</span><span class="sxs-lookup"><span data-stu-id="07533-179">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="07533-180">Ele procura os dados de saudação em Olá pipeline início e término vezes, não antes ou depois desses tempos.</span><span class="sxs-lookup"><span data-stu-id="07533-180">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
| <span data-ttu-id="07533-181">externo</span><span class="sxs-lookup"><span data-stu-id="07533-181">external</span></span> | <span data-ttu-id="07533-182">Essa propriedade é definida, muito**true** se os dados de saudação não são gerados por este pipeline.</span><span class="sxs-lookup"><span data-stu-id="07533-182">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="07533-183">dados de entrada Hello neste tutorial estão no arquivo de emp.txt hello, que não é gerado por este pipeline, portanto vamos definir essa propriedade tootrue.</span><span class="sxs-lookup"><span data-stu-id="07533-183">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

<span data-ttu-id="07533-184">Para saber mais sobre essas propriedades JSON, confira o [artigo sobre o conector do Blob do Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="07533-184">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>

### <a name="outputdatasetjson"></a><span data-ttu-id="07533-185">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="07533-185">outputdataset.json</span></span>

```JSON
{
  "name": "AzureSqlOutput",
  "properties": {
    "structure": [
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "emp"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="07533-186">Olá, tabela a seguir fornece descrições para propriedades JSON Olá usadas no trecho hello:</span><span class="sxs-lookup"><span data-stu-id="07533-186">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="07533-187">Propriedade</span><span class="sxs-lookup"><span data-stu-id="07533-187">Property</span></span> | <span data-ttu-id="07533-188">Descrição</span><span class="sxs-lookup"><span data-stu-id="07533-188">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="07533-189">type</span><span class="sxs-lookup"><span data-stu-id="07533-189">type</span></span> | <span data-ttu-id="07533-190">propriedade do tipo Hello está definida muito**AzureSqlTable** porque os dados são copiados tooa tabela em um banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="07533-190">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
| <span data-ttu-id="07533-191">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="07533-191">linkedServiceName</span></span> | <span data-ttu-id="07533-192">Refere-se toohello **AzureSqlLinkedService** que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="07533-192">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="07533-193">tableName</span><span class="sxs-lookup"><span data-stu-id="07533-193">tableName</span></span> | <span data-ttu-id="07533-194">Olá especificado **tabela** toowhich Olá dados são copiados.</span><span class="sxs-lookup"><span data-stu-id="07533-194">Specified hello **table** toowhich hello data is copied.</span></span> | 
| <span data-ttu-id="07533-195">frequência/intervalo</span><span class="sxs-lookup"><span data-stu-id="07533-195">frequency/interval</span></span> | <span data-ttu-id="07533-196">Olá frequência é definida muito**hora** e o intervalo é **1**, o que significa que Olá fatias de saída são produzidas **por hora** entre Olá pipeline início e término vezes, não antes ou Após esses horários.</span><span class="sxs-lookup"><span data-stu-id="07533-196">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

<span data-ttu-id="07533-197">Há três colunas – **ID**, **FirstName**, e **LastName** – na tabela de emp Olá no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="07533-197">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="07533-198">ID é uma coluna de identidade, portanto, você precisa apenas toospecify **FirstName** e **LastName** aqui.</span><span class="sxs-lookup"><span data-stu-id="07533-198">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

<span data-ttu-id="07533-199">Para saber mais sobre essas propriedades JSON, confira o [artigo sobre o conector do SQL](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="07533-199">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="07533-200">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="07533-200">pipeline.json</span></span>

```JSON
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "description": "Push Regional Effectiveness Campaign data tooAzure SQL database",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2017-05-11T00:00:00Z",
    "end": "2017-05-12T00:00:00Z"
  }
}
```

<span data-ttu-id="07533-201">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="07533-201">Note hello following points:</span></span>

- <span data-ttu-id="07533-202">Na seção de atividades hello, há apenas uma atividade cuja **tipo** está definido muito**cópia**.</span><span class="sxs-lookup"><span data-stu-id="07533-202">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="07533-203">Para obter mais informações sobre a atividade de cópia hello, consulte [atividades de movimentação de dados](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="07533-203">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="07533-204">Nas soluções de Data Factory, você também pode usar [atividades de transformação de dados](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="07533-204">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
- <span data-ttu-id="07533-205">Entrada para atividade de saudação é definida muito**AzureBlobInput** e de saída para o conjunto de hello atividade é muito**AzureSqlOutput**.</span><span class="sxs-lookup"><span data-stu-id="07533-205">Input for hello activity is set too**AzureBlobInput** and output for hello activity is set too**AzureSqlOutput**.</span></span> 
- <span data-ttu-id="07533-206">Em Olá **typeProperties** seção, **BlobSource** é especificado como tipo de fonte hello e **SqlSink** é especificado como tipo de coletor de saudação.</span><span class="sxs-lookup"><span data-stu-id="07533-206">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="07533-207">Para obter uma lista completa de armazenamentos de dados de atividade de cópia hello como origens e coletores com suporte, consulte [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="07533-207">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="07533-208">toolearn como toouse dados específicos com suporte são armazenados como um fonte/coletor, clique o link de saudação na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="07533-208">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
 
<span data-ttu-id="07533-209">Substituir valor Olá Olá **iniciar** propriedade com hello dia atual e **final** valor com hello dia seguinte.</span><span class="sxs-lookup"><span data-stu-id="07533-209">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="07533-210">Você pode especificar apenas parte da data hello e ignore a parte de hora de saudação da saudação data hora.</span><span class="sxs-lookup"><span data-stu-id="07533-210">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="07533-211">Por exemplo, "2017-02-03", que é o equivalente muito "2017-02-03T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="07533-211">For example, "2017-02-03", which is equivalent too"2017-02-03T00:00:00Z"</span></span>
 
<span data-ttu-id="07533-212">Ambos os valores de data/hora de início e de término devem estar no [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="07533-212">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="07533-213">Por exemplo: 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="07533-213">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="07533-214">Olá **final** tempo é opcional, mas usamos neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="07533-214">hello **end** time is optional, but we use it in this tutorial.</span></span> 
 
<span data-ttu-id="07533-215">Se você não especificar o valor para Olá **final** propriedade, ele é calculado como "**início + 48 horas**".</span><span class="sxs-lookup"><span data-stu-id="07533-215">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="07533-216">pipeline de saudação toorun indefinidamente, especifique **9999-09-09** como valor Olá Olá **final** propriedade.</span><span class="sxs-lookup"><span data-stu-id="07533-216">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
 
<span data-ttu-id="07533-217">Olá anterior de exemplo, há 24 fatias de dados como cada fatia de dados é produzida por hora.</span><span class="sxs-lookup"><span data-stu-id="07533-217">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

<span data-ttu-id="07533-218">Para obter descrições das propriedades JSON em uma definição de pipeline, consulte o artigo [Criar pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="07533-218">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="07533-219">Para obter descrições das propriedades JSON em uma definição de atividade de cópia, consulte [Atividades de movimentação de dados](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="07533-219">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="07533-220">Para obter descrições das propriedades JSON com suporte pelo BlobSource, consulte o [artigo sobre o conector de blobs do Azure](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="07533-220">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="07533-221">Para obter descrições das propriedades JSON com suporte pelo SqlSink, consulte o [artigo sobre o conector do Banco de Dados SQL](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="07533-221">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="set-global-variables"></a><span data-ttu-id="07533-222">Definir variáveis globais</span><span class="sxs-lookup"><span data-stu-id="07533-222">Set global variables</span></span>
<span data-ttu-id="07533-223">No Azure PowerShell, execute Olá comandos a seguir depois de substituir os valores hello com seu próprio:</span><span class="sxs-lookup"><span data-stu-id="07533-223">In Azure PowerShell, execute hello following commands after replacing hello values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07533-224">Veja a seção [Pré-requisitos](#prerequisites) para obter instruções sobre como obter a ID do cliente, o segredo do cliente, a ID do locatário e ID da assinatura.</span><span class="sxs-lookup"><span data-stu-id="07533-224">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>   
> 
> 

```JSON
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
```

<span data-ttu-id="07533-225">Olá executar comando a seguir depois de atualizar o nome da saudação Olá da fábrica de dados que você está usando:</span><span class="sxs-lookup"><span data-stu-id="07533-225">Run hello following command after updating hello name of hello data factory you are using:</span></span> 

```
$adf = "ADFCopyTutorialDF"
```

## <a name="authenticate-with-aad"></a><span data-ttu-id="07533-226">Autenticar com o AAD</span><span class="sxs-lookup"><span data-stu-id="07533-226">Authenticate with AAD</span></span>
<span data-ttu-id="07533-227">Execute Olá tooauthenticate de comando com o Azure Active Directory (AAD) a seguir:</span><span class="sxs-lookup"><span data-stu-id="07533-227">Run hello following command tooauthenticate with Azure Active Directory (AAD):</span></span> 

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken) 
```

## <a name="create-data-factory"></a><span data-ttu-id="07533-228">Criar um data factory</span><span class="sxs-lookup"><span data-stu-id="07533-228">Create data factory</span></span>
<span data-ttu-id="07533-229">Nesta etapa, você criará um Azure Data Factory chamado **ADFCopyTutorialDF**.</span><span class="sxs-lookup"><span data-stu-id="07533-229">In this step, you create an Azure Data Factory named **ADFCopyTutorialDF**.</span></span> <span data-ttu-id="07533-230">Uma fábrica de dados pode ter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="07533-230">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="07533-231">Um pipeline em um data factory pode ter uma ou mais atividades.</span><span class="sxs-lookup"><span data-stu-id="07533-231">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="07533-232">Por exemplo, armazenar dados de toocopy uma atividade de cópia de uma fonte de dados de destino tooa.</span><span class="sxs-lookup"><span data-stu-id="07533-232">For example, a Copy Activity toocopy data from a source tooa destination data store.</span></span> <span data-ttu-id="07533-233">Dados de saída de tooproduct de dados de entrada de uma atividade de Hive do HDInsight toorun um tootransform de script do Hive.</span><span class="sxs-lookup"><span data-stu-id="07533-233">A HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="07533-234">Execute Olá fábrica de dados de saudação de toocreate comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="07533-234">Run hello following commands toocreate hello data factory:</span></span> 

1. <span data-ttu-id="07533-235">Atribuir Olá comando toovariable chamado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="07533-235">Assign hello command toovariable named **cmd**.</span></span> 
   
    > [!IMPORTANT]
    > <span data-ttu-id="07533-236">Confirmar esse nome Olá Olá da fábrica de dados especificadas aqui (ADFCopyTutorialDF) correspondências Olá nome especificado no hello **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="07533-236">Confirm that hello name of hello data factory you specify here (ADFCopyTutorialDF) matches hello name specified in hello **datafactory.json**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/ADFCopyTutorialDF0411?api-version=2015-10-01};
    ```
2. <span data-ttu-id="07533-237">Execute o comando hello usando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="07533-237">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="07533-238">Exibir resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="07533-238">View hello results.</span></span> <span data-ttu-id="07533-239">Se a fábrica de dados Olá foi criada com êxito, você vê Olá JSON Olá fábrica de dados em Olá **resultados**; caso contrário, você verá uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="07533-239">If hello data factory has been successfully created, you see hello JSON for hello data factory in hello **results**; otherwise, you see an error message.</span></span>  
   
    ```
    Write-Host $results
    ```

<span data-ttu-id="07533-240">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="07533-240">Note hello following points:</span></span>

* <span data-ttu-id="07533-241">nome de saudação do hello Azure Data Factory deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="07533-241">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="07533-242">Se você vir o erro Olá nos resultados: **"ADFCopyTutorialDF" nome da fábrica de dados não está disponível**, Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="07533-242">If you see hello error in results: **Data factory name “ADFCopyTutorialDF” is not available**, do hello following steps:</span></span>  
  
  1. <span data-ttu-id="07533-243">Alterar nome da saudação (por exemplo, yournameADFCopyTutorialDF) em Olá **datafactory.json** arquivo.</span><span class="sxs-lookup"><span data-stu-id="07533-243">Change hello name (for example, yournameADFCopyTutorialDF) in hello **datafactory.json** file.</span></span>
  2. <span data-ttu-id="07533-244">No comando primeiro Olá Olá onde **$cmd** variável é atribuída a um valor, substitua ADFCopyTutorialDF pelo novo nome de saudação e execute o comando de saudação.</span><span class="sxs-lookup"><span data-stu-id="07533-244">In hello first command where hello **$cmd** variable is assigned a value, replace ADFCopyTutorialDF with hello new name and run hello command.</span></span> 
  3. <span data-ttu-id="07533-245">Execute Olá dois comandos tooinvoke Olá API REST toocreate Olá dados fábrica e impressão Olá resultados da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="07533-245">Run hello next two commands tooinvoke hello REST API toocreate hello data factory and print hello results of hello operation.</span></span> 
     
     <span data-ttu-id="07533-246">Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="07533-246">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="07533-247">toocreate instâncias de fábrica de dados, você precisa toobe um colaborador/administrador de saudação assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="07533-247">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="07533-248">nome Olá Olá da fábrica de dados pode ser registrado como um nome DNS no futuro de saudação e, portanto, se tornar publicamente visível.</span><span class="sxs-lookup"><span data-stu-id="07533-248">hello name of hello data factory may be registered as a DNS name in hello future and hence become publicly visible.</span></span>
* <span data-ttu-id="07533-249">Se você receber o erro Olá: "**esta assinatura não está registrado toouse namespace DataFactory**", execute um dos seguintes hello e tente publicar novamente:</span><span class="sxs-lookup"><span data-stu-id="07533-249">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span> 
  
  * <span data-ttu-id="07533-250">No Azure PowerShell, execute Olá provedor do comando tooregister Olá fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="07533-250">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="07533-251">Você pode executar Olá tooconfirm de comando a seguir que Olá Data Factory provedor está registrado.</span><span class="sxs-lookup"><span data-stu-id="07533-251">You can run hello following command tooconfirm that hello Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="07533-252">Usando o logon Olá assinatura do Azure em Olá [portal do Azure](https://portal.azure.com) e navegue tooa folha de fábrica de dados (ou) criar uma fábrica de dados no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="07533-252">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="07533-253">Esta ação registra automaticamente o provedor de saudação para você.</span><span class="sxs-lookup"><span data-stu-id="07533-253">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="07533-254">Antes de criar um pipeline, é necessário toocreate algumas entidades da fábrica de dados pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="07533-254">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="07533-255">Você primeiro criar a fonte de toolink serviços vinculados e dados de destino armazena dados tooyour armazenar.</span><span class="sxs-lookup"><span data-stu-id="07533-255">You first create linked services toolink source and destination data stores tooyour data store.</span></span> <span data-ttu-id="07533-256">Em seguida, defina conjuntos de dados de entrada e saída toorepresent dados em repositórios de dados vinculados.</span><span class="sxs-lookup"><span data-stu-id="07533-256">Then, define input and output datasets toorepresent data in linked data stores.</span></span> <span data-ttu-id="07533-257">Finalmente, crie o pipeline de saudação com uma atividade que usa esses conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="07533-257">Finally, create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="07533-258">Criar serviços vinculados</span><span class="sxs-lookup"><span data-stu-id="07533-258">Create linked services</span></span>
<span data-ttu-id="07533-259">Você pode criar serviços vinculados em um toolink de fábrica de dados seus dados, armazena e fábrica de dados toohello de serviços de computação.</span><span class="sxs-lookup"><span data-stu-id="07533-259">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="07533-260">Neste tutorial, você não usa serviços de computação, como o Azure HDInsight ou o Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="07533-260">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="07533-261">Você usa dois armazenamentos de dados do tipo Armazenamento do Azure (origem) e o banco de dados SQL (destino).</span><span class="sxs-lookup"><span data-stu-id="07533-261">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> <span data-ttu-id="07533-262">Portanto, você pode criar dois serviços vinculados, chamados AzureStorageLinkedService e AzureSqlLinkedService, dos tipos: AzureStorage e AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="07533-262">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="07533-263">Olá AzureStorageLinkedService vincula sua fábrica de dados de toohello de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="07533-263">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="07533-264">Esta conta de armazenamento é hello um no qual você criou um contêiner e carregou dados de saudação como parte do [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="07533-264">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="07533-265">AzureSqlLinkedService vincula sua fábrica de dados de toohello de banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="07533-265">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="07533-266">Olá dados são copiados do armazenamento de blob Olá são armazenados neste banco de dados.</span><span class="sxs-lookup"><span data-stu-id="07533-266">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="07533-267">Você criou tabela emp de saudação neste banco de dados como parte do [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="07533-267">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="07533-268">Criar o serviço vinculado do armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="07533-268">Create Azure Storage linked service</span></span>
<span data-ttu-id="07533-269">Nesta etapa, você vincular sua fábrica de dados de tooyour de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="07533-269">In this step, you link your Azure storage account tooyour data factory.</span></span> <span data-ttu-id="07533-270">Especifique o nome hello e a chave da sua conta de armazenamento do Azure nesta seção.</span><span class="sxs-lookup"><span data-stu-id="07533-270">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="07533-271">Consulte [serviço vinculado do armazenamento do Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) para obter detalhes sobre o JSON propriedades usadas toodefine um armazenamento do Azure serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="07533-271">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span>  

1. <span data-ttu-id="07533-272">Atribuir Olá comando toovariable chamado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="07533-272">Assign hello command toovariable named **cmd**.</span></span> 

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@azurestoragelinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="07533-273">Execute o comando hello usando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="07533-273">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="07533-274">Exibir resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="07533-274">View hello results.</span></span> <span data-ttu-id="07533-275">Se Olá vinculado serviço foi criado com êxito, consulte Olá JSON para o serviço de saudação vinculado no hello **resultados**; caso contrário, você verá uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="07533-275">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell   
    Write-Host $results
    ```

### <a name="create-azure-sql-linked-service"></a><span data-ttu-id="07533-276">Criar serviço vinculado do Azure SQL</span><span class="sxs-lookup"><span data-stu-id="07533-276">Create Azure SQL linked service</span></span>
<span data-ttu-id="07533-277">Nesta etapa, você vincular sua fábrica de dados de tooyour de banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="07533-277">In this step, you link your Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="07533-278">Especifique o nome do servidor SQL Azure Olá, nome do banco de dados, nome de usuário e senha de usuário nesta seção.</span><span class="sxs-lookup"><span data-stu-id="07533-278">You specify hello Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="07533-279">Consulte [serviço vinculado do SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties) para obter detalhes sobre o JSON propriedades usadas toodefine um SQL Azure serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="07533-279">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used toodefine an Azure SQL linked service.</span></span>

1. <span data-ttu-id="07533-280">Atribuir Olá comando toovariable chamado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="07533-280">Assign hello command toovariable named **cmd**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azuresqllinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureSqlLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="07533-281">Execute o comando hello usando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="07533-281">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="07533-282">Exibir resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="07533-282">View hello results.</span></span> <span data-ttu-id="07533-283">Se Olá vinculado serviço foi criado com êxito, consulte Olá JSON para o serviço de saudação vinculado no hello **resultados**; caso contrário, você verá uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="07533-283">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="07533-284">Criar conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="07533-284">Create datasets</span></span>
<span data-ttu-id="07533-285">Na etapa anterior de saudação, você criou serviços vinculados toolink sua conta de armazenamento do Azure e a fábrica de dados de tooyour de banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="07533-285">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="07533-286">Nesta etapa, você definirá dois conjuntos de dados denominados AzureBlobInput AzureSqlOutput que representam a entrada e saída dados e que são armazenados em repositórios de dados Olá referenciados por AzureStorageLinkedService e AzureSqlLinkedService, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="07533-286">In this step, you define two datasets named AzureBlobInput and AzureSqlOutput that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="07533-287">serviço de armazenamento do Azure vinculado Olá Especifica a cadeia de conexão de Olá usada pelo serviço de fábrica de dados em tempo de execução tooconnect tooyour conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="07533-287">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="07533-288">E, Olá o conjunto de dados de blob de entrada (AzureBlobInput) Especifica o contêiner de saudação e a pasta de saudação que contém os dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="07533-288">And, hello input blob dataset (AzureBlobInput) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="07533-289">Da mesma forma, Olá serviço de banco de dados do SQL Azure vinculado Especifica a cadeia de caracteres de conexão de saudação que usa o serviço de fábrica de dados no banco de dados SQL do Azure tooyour de tooconnect de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="07533-289">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="07533-290">E, Olá saída SQL o conjunto de dados de tabela (OututDataset) Especifica a tabela de saudação em Olá Olá de toowhich de banco de dados dados saudação do armazenamento de blob são copiados.</span><span class="sxs-lookup"><span data-stu-id="07533-290">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="07533-291">Criar conjunto de dados de entrada</span><span class="sxs-lookup"><span data-stu-id="07533-291">Create input dataset</span></span>
<span data-ttu-id="07533-292">Nesta etapa, você criar um conjunto de dados chamado AzureBlobInput que aponta o arquivo de blob tooa (emp.txt) na pasta raiz de saudação de um contêiner de blob (adftutorial) no hello representado por Olá AzureStorageLinkedService vinculado de serviço de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="07533-292">In this step, you create a dataset named AzureBlobInput that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="07533-293">Se você não especificar um valor para o nome de arquivo hello (ou ignorá-lo), dados de todos os blobs na pasta de entrada hello são copiados toohello destino.</span><span class="sxs-lookup"><span data-stu-id="07533-293">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="07533-294">Neste tutorial, você deve especificar um valor para o nome de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="07533-294">In this tutorial, you specify a value for hello fileName.</span></span> 

1. <span data-ttu-id="07533-295">Atribuir Olá comando toovariable chamado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="07533-295">Assign hello command toovariable named **cmd**.</span></span> 

    ```PowerSHell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="07533-296">Execute o comando hello usando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="07533-296">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="07533-297">Exibir resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="07533-297">View hello results.</span></span> <span data-ttu-id="07533-298">Se Olá conjunto de dados foi criado com êxito, você verá hello JSON para o conjunto de dados Olá Olá **resultados**; caso contrário, você verá uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="07533-298">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="07533-299">Criar conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="07533-299">Create output dataset</span></span>
<span data-ttu-id="07533-300">Olá serviço de banco de dados do SQL Azure vinculado Especifica a cadeia de caracteres de conexão de saudação que usa o serviço de fábrica de dados no banco de dados SQL do Azure tooyour de tooconnect de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="07533-300">hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="07533-301">Olá saída SQL tabela dataset (OututDataset) você criar nessa etapa Especifica a tabela Olá Olá toowhich Olá de banco de dados armazenamento de blob de saudação é copiada.</span><span class="sxs-lookup"><span data-stu-id="07533-301">hello output SQL table dataset (OututDataset) you create in this step specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>

1. <span data-ttu-id="07533-302">Atribuir Olá comando toovariable chamado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="07533-302">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureSqlOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="07533-303">Execute o comando hello usando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="07533-303">Run hello command by using **Invoke-Command**.</span></span>
    
    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="07533-304">Exibir resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="07533-304">View hello results.</span></span> <span data-ttu-id="07533-305">Se Olá conjunto de dados foi criado com êxito, você verá hello JSON para o conjunto de dados Olá Olá **resultados**; caso contrário, você verá uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="07533-305">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ``` 

## <a name="create-pipeline"></a><span data-ttu-id="07533-306">Criar um pipeline</span><span class="sxs-lookup"><span data-stu-id="07533-306">Create pipeline</span></span>
<span data-ttu-id="07533-307">Nesta etapa, você cria um pipeline com uma **atividade de cópia** que usa **AzureBlobInput** como uma entrada e **AzureSqlOutput** como uma saída.</span><span class="sxs-lookup"><span data-stu-id="07533-307">In this step, you create a pipeline with a **copy activity** that uses **AzureBlobInput** as an input and **AzureSqlOutput** as an output.</span></span>

<span data-ttu-id="07533-308">Atualmente, o conjunto de dados de saída é quais unidades Olá agenda.</span><span class="sxs-lookup"><span data-stu-id="07533-308">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="07533-309">Neste tutorial, o conjunto de dados de saída é configurado tooproduce uma fatia de uma vez por hora.</span><span class="sxs-lookup"><span data-stu-id="07533-309">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="07533-310">pipeline de saudação tem uma hora de início e a hora de término que são um dia de distância, que é de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="07533-310">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="07533-311">Portanto, 24 fatias de conjunto de dados de saída são produzidas pelo pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="07533-311">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 

1. <span data-ttu-id="07533-312">Atribuir Olá comando toovariable chamado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="07533-312">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="07533-313">Execute o comando hello usando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="07533-313">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="07533-314">Exibir resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="07533-314">View hello results.</span></span> <span data-ttu-id="07533-315">Se Olá conjunto de dados foi criado com êxito, você verá hello JSON para o conjunto de dados Olá Olá **resultados**; caso contrário, você verá uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="07533-315">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>  

    ```PowerShell   
    Write-Host $results
    ```

<span data-ttu-id="07533-316">**Parabéns!**</span><span class="sxs-lookup"><span data-stu-id="07533-316">**Congratulations!**</span></span> <span data-ttu-id="07533-317">Você criou com êxito uma fábrica de dados do Azure, com um pipeline que copia dados de banco de dados do SQL Azure Blob Storage tooAzure.</span><span class="sxs-lookup"><span data-stu-id="07533-317">You have successfully created an Azure data factory, with a pipeline that copies data from Azure Blob Storage tooAzure SQL database.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="07533-318">Monitorar o pipeline</span><span class="sxs-lookup"><span data-stu-id="07533-318">Monitor pipeline</span></span>
<span data-ttu-id="07533-319">Nesta etapa, você deve usar fatias de toomonitor de API de REST de fábrica de dados produzidas pelo pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="07533-319">In this step, you use Data Factory REST API toomonitor slices being produced by hello pipeline.</span></span>

```PowerShell
$ds ="AzureSqlOutput"
```

> [!IMPORTANT] 
> <span data-ttu-id="07533-320">Certifique-se de início de saudação e de término horas Olá especificado no seguinte comando correspondência Olá início e término do pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="07533-320">Make sure that hello start and end times specified in hello following command match hello start and end times of hello pipeline.</span></span> 

```PowerShell
$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=2017-05-11T00%3a00%3a00.0000000Z"&"end=2017-05-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};
```

```PowerShell
$results2 = Invoke-Command -scriptblock $cmd;
```

```PowerShell
IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

<span data-ttu-id="07533-321">Executar Olá Invoke-Command e hello outro até que você veja uma fatia em **pronto** estado ou **falha** estado.</span><span class="sxs-lookup"><span data-stu-id="07533-321">Run hello Invoke-Command and hello next one until you see a slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="07533-322">Quando a fatia hello está no estado pronto, verificar Olá **emp** tabela no banco de dados SQL do Azure para dados de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="07533-322">When hello slice is in Ready state, check hello **emp** table in your Azure SQL database for hello output data.</span></span> 

<span data-ttu-id="07533-323">Para cada fatia, duas linhas de dados do arquivo de origem de saudação são copiados toohello tabela de emp no banco de dados do SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="07533-323">For each slice, two rows of data from hello source file are copied toohello emp table in hello Azure SQL database.</span></span> <span data-ttu-id="07533-324">Portanto, você ver 24 novos registros na tabela de emp hello quando todas as fatias de saudação são processadas com êxito (no estado pronto).</span><span class="sxs-lookup"><span data-stu-id="07533-324">Therefore, you see 24 new records in hello emp table when all hello slices are successfully processed (in Ready state).</span></span> 

## <a name="summary"></a><span data-ttu-id="07533-325">Resumo</span><span class="sxs-lookup"><span data-stu-id="07533-325">Summary</span></span>
<span data-ttu-id="07533-326">Neste tutorial, você usou a API REST toocreate um Azure fábrica toocopy dados de um banco de dados do SQL Azure de tooan BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="07533-326">In this tutorial, you used REST API toocreate an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="07533-327">Aqui estão as etapas de alto nível Olá executada neste tutorial:</span><span class="sxs-lookup"><span data-stu-id="07533-327">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="07533-328">Foi criada uma **data factory**do Azure.</span><span class="sxs-lookup"><span data-stu-id="07533-328">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="07533-329">Foram criados **serviços vinculados**:</span><span class="sxs-lookup"><span data-stu-id="07533-329">Created **linked services**:</span></span>
   1. <span data-ttu-id="07533-330">Um armazenamento do Azure vinculada ao serviço toolink sua conta de armazenamento do Azure que contém dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="07533-330">An Azure Storage linked service toolink your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="07533-331">Um SQL Azure vinculado serviço toolink seu banco de dados SQL do Azure que contém dados de saída de saudação.</span><span class="sxs-lookup"><span data-stu-id="07533-331">An Azure SQL linked service toolink your Azure SQL database that holds hello output data.</span></span> 
3. <span data-ttu-id="07533-332">Foram criados **conjuntos de dados**que descrevem os dados de entrada e de saída para os pipelines.</span><span class="sxs-lookup"><span data-stu-id="07533-332">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="07533-333">Foi criado um **pipeline** com uma Atividade de Cópia com BlobSource como origem e SqlSink como coletor.</span><span class="sxs-lookup"><span data-stu-id="07533-333">Created a **pipeline** with a Copy Activity with BlobSource as source and SqlSink as sink.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="07533-334">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="07533-334">Next steps</span></span>
<span data-ttu-id="07533-335">Neste tutorial, você usou o armazenamento de blobs do Azure como um armazenamento de dados de origem e um banco de dados SQL do Azure como um armazenamento de dados de destino em uma operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="07533-335">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="07533-336">Olá tabela a seguir fornece uma lista de repositórios de dados com suporte como origens e destinos de atividade de cópia de saudação:</span><span class="sxs-lookup"><span data-stu-id="07533-336">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="07533-337">toolearn sobre como armazenam dados toocopy para/de uma data, clique o link Olá Olá repositório de dados na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="07533-337">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
