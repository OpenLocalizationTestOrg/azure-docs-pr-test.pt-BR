---
title: "aaaBuild sua fábrica de dados primeiro (REST) | Microsoft Docs"
description: "Neste tutorial, você cria um pipeline de exemplo do Azure Data Factory usando a API REST do Data Factory."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7e0a2465-2d85-4143-a4bb-42e03c273097
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 5d8e39bd598cca35f91d501bad74e8a8436f8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-data-factory-rest-api"></a><span data-ttu-id="fc17b-103">Tutorial: Criar seu primeiro data factory do Azure usando a API REST do Data Factory</span><span class="sxs-lookup"><span data-stu-id="fc17b-103">Tutorial: Build your first Azure data factory using Data Factory REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fc17b-104">Visão geral e pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fc17b-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="fc17b-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="fc17b-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="fc17b-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fc17b-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="fc17b-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fc17b-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="fc17b-108">Modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fc17b-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="fc17b-109">API REST</span><span class="sxs-lookup"><span data-stu-id="fc17b-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>


<span data-ttu-id="fc17b-110">Neste artigo, você usar a API de REST de fábrica de dados toocreate sua primeira data factory do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc17b-110">In this article, you use Data Factory REST API toocreate your first Azure data factory.</span></span> <span data-ttu-id="fc17b-111">tutorial de saudação toodo usando outras ferramentas/SDKs, selecione uma das opções de saudação da lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc17b-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="fc17b-112">pipeline de saudação neste tutorial tem uma atividade: **atividade Hive do HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="fc17b-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="fc17b-113">Essa atividade executa um script do hive em um cluster de HDInsight do Azure que transforma dados de saída de tooproduce de entrada.</span><span class="sxs-lookup"><span data-stu-id="fc17b-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="fc17b-114">pipeline de saudação é agendado toorun depois de um mês entre hello especificar horários de início e término.</span><span class="sxs-lookup"><span data-stu-id="fc17b-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span>

> [!NOTE]
> <span data-ttu-id="fc17b-115">Este artigo não aborda todos os Olá API REST.</span><span class="sxs-lookup"><span data-stu-id="fc17b-115">This article does not cover all hello REST API.</span></span> <span data-ttu-id="fc17b-116">Para obter uma documentação abrangente sobre a API REST, confira a [referência da API REST do Data Factory](/rest/api/datafactory/).</span><span class="sxs-lookup"><span data-stu-id="fc17b-116">For comprehensive documentation on REST API, see [Data Factory REST API Reference](/rest/api/datafactory/).</span></span>
> 
> <span data-ttu-id="fc17b-117">Um pipeline pode ter mais de uma atividade.</span><span class="sxs-lookup"><span data-stu-id="fc17b-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="fc17b-118">E, é possível encadear duas atividades (executadas uma atividade após o outro), definindo Olá o conjunto de dados de saída de uma atividade Olá outra atividade de conjunto de dados de saudação de entrada.</span><span class="sxs-lookup"><span data-stu-id="fc17b-118">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="fc17b-119">Para saber mais, confira [Agendamento e execução no Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="fc17b-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="fc17b-120">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fc17b-120">Prerequisites</span></span>
* <span data-ttu-id="fc17b-121">Leia [visão geral do Tutorial](data-factory-build-your-first-pipeline.md) artigo e hello completa **pré-requisito** etapas.</span><span class="sxs-lookup"><span data-stu-id="fc17b-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="fc17b-122">Instale o [Curl](https://curl.haxx.se/dlwiz/) em seu computador.</span><span class="sxs-lookup"><span data-stu-id="fc17b-122">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="fc17b-123">Use ferramenta de ONDULAÇÃO Olá com REST comandos toocreate uma fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="fc17b-123">You use hello CURL tool with REST commands toocreate a data factory.</span></span>
* <span data-ttu-id="fc17b-124">Siga as instruções [deste artigo](../azure-resource-manager/resource-group-create-service-principal-portal.md) para:</span><span class="sxs-lookup"><span data-stu-id="fc17b-124">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span>
  1. <span data-ttu-id="fc17b-125">Crie um aplicativo Web chamado **ADFGetStartedApp** no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fc17b-125">Create a Web application named **ADFGetStartedApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="fc17b-126">Obtenha a **ID do cliente** e a **chave secreta**.</span><span class="sxs-lookup"><span data-stu-id="fc17b-126">Get **client ID** and **secret key**.</span></span>
  3. <span data-ttu-id="fc17b-127">Obtenha a **ID do locatário**.</span><span class="sxs-lookup"><span data-stu-id="fc17b-127">Get **tenant ID**.</span></span>
  4. <span data-ttu-id="fc17b-128">Atribuir Olá **ADFGetStartedApp** aplicativo toohello **colaborador da fábrica de dados** função.</span><span class="sxs-lookup"><span data-stu-id="fc17b-128">Assign hello **ADFGetStartedApp** application toohello **Data Factory Contributor** role.</span></span>
* <span data-ttu-id="fc17b-129">Instale o [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fc17b-129">Install [Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="fc17b-130">Iniciar **PowerShell** e execução Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="fc17b-130">Launch **PowerShell** and run hello following command.</span></span> <span data-ttu-id="fc17b-131">Mantenha o Azure PowerShell aberta até o fim deste tutorial hello.</span><span class="sxs-lookup"><span data-stu-id="fc17b-131">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="fc17b-132">Se você fecha e reabrir o, será necessário comandos de saudação toorun novamente.</span><span class="sxs-lookup"><span data-stu-id="fc17b-132">If you close and reopen, you need toorun hello commands again.</span></span>
  1. <span data-ttu-id="fc17b-133">Executar **AzureRmAccount Login** e insira o nome de usuário de saudação e a senha que você use toosign em toohello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc17b-133">Run **Login-AzureRmAccount** and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
  2. <span data-ttu-id="fc17b-134">Executar **Get-AzureRmSubscription** tooview todos Olá assinaturas para esta conta.</span><span class="sxs-lookup"><span data-stu-id="fc17b-134">Run **Get-AzureRmSubscription** tooview all hello subscriptions for this account.</span></span>
  3. <span data-ttu-id="fc17b-135">Executar **AzureRmSubscription Get - SubscriptionName NameOfAzureSubscription | Conjunto AzureRmContext** assinatura de saudação tooselect que você deseja toowork com.</span><span class="sxs-lookup"><span data-stu-id="fc17b-135">Run **Get-AzureRmSubscription -SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="fc17b-136">Substituir **NameOfAzureSubscription** com o nome da saudação de sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc17b-136">Replace **NameOfAzureSubscription** with hello name of your Azure subscription.</span></span>
* <span data-ttu-id="fc17b-137">Criar um grupo de recursos do Azure denominado **ADFTutorialResourceGroup** executando Olá comando de saudação do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="fc17b-137">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

   <span data-ttu-id="fc17b-138">Algumas das etapas de saudação neste tutorial presumem que você use o grupo de recursos de saudação chamado ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="fc17b-138">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="fc17b-139">Se você usar um grupo de recursos diferentes, você precisa toouse nome de saudação do seu grupo de recursos no lugar de ADFTutorialResourceGroup neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="fc17b-139">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="fc17b-140">Criar definições JSON</span><span class="sxs-lookup"><span data-stu-id="fc17b-140">Create JSON definitions</span></span>
<span data-ttu-id="fc17b-141">Crie arquivos JSON na pasta Olá onde se encontra curl.exe a seguir.</span><span class="sxs-lookup"><span data-stu-id="fc17b-141">Create following JSON files in hello folder where curl.exe is located.</span></span>

### <a name="datafactoryjson"></a><span data-ttu-id="fc17b-142">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="fc17b-142">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fc17b-143">Nome deve ser globalmente exclusivo, portanto, talvez você queira tooprefix/sufixo ADFCopyTutorialDF toomake ele um nome exclusivo.</span><span class="sxs-lookup"><span data-stu-id="fc17b-143">Name must be globally unique, so you may want tooprefix/suffix ADFCopyTutorialDF toomake it a unique name.</span></span>
>
>

```JSON
{
    "name": "FirstDataFactoryREST",
    "location": "WestUS"
}
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="fc17b-144">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="fc17b-144">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fc17b-145">Substitua **nome da conta** e **chave da conta** pelo nome e pela chave da sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc17b-145">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="fc17b-146">toolearn como tooget acessar o armazenamento de chave, consulte Olá informações sobre como tooview, copiar e armazenamento regenerar chaves de acesso em [gerenciar sua conta de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="fc17b-146">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
>
>

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

### <a name="hdinsightondemandlinkedservicejson"></a><span data-ttu-id="fc17b-147">hdinsightondemandlinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="fc17b-147">hdinsightondemandlinkedservice.json</span></span>

```JSON
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "AzureStorageLinkedService"
        }
    }
}
```

<span data-ttu-id="fc17b-148">Olá, tabela a seguir fornece descrições para propriedades JSON Olá usadas no trecho hello:</span><span class="sxs-lookup"><span data-stu-id="fc17b-148">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="fc17b-149">Propriedade</span><span class="sxs-lookup"><span data-stu-id="fc17b-149">Property</span></span> | <span data-ttu-id="fc17b-150">Descrição</span><span class="sxs-lookup"><span data-stu-id="fc17b-150">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="fc17b-151">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="fc17b-151">ClusterSize</span></span> |<span data-ttu-id="fc17b-152">Tamanho do cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="fc17b-152">Size of hello HDInsight cluster.</span></span> |
| <span data-ttu-id="fc17b-153">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="fc17b-153">TimeToLive</span></span> |<span data-ttu-id="fc17b-154">Especifica que Olá de tempo ocioso para um cluster do HDInsight hello, antes de ser excluído.</span><span class="sxs-lookup"><span data-stu-id="fc17b-154">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
| <span data-ttu-id="fc17b-155">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="fc17b-155">linkedServiceName</span></span> |<span data-ttu-id="fc17b-156">Especifica a conta de armazenamento de saudação que é usado toostore logs de Olá gerados pelo HDInsight</span><span class="sxs-lookup"><span data-stu-id="fc17b-156">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight</span></span> |

<span data-ttu-id="fc17b-157">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="fc17b-157">Note hello following points:</span></span>

* <span data-ttu-id="fc17b-158">Olá fábrica de dados cria um **baseados em Linux** cluster HDInsight para você com hello acima JSON.</span><span class="sxs-lookup"><span data-stu-id="fc17b-158">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello above JSON.</span></span> <span data-ttu-id="fc17b-159">Confira [Serviço vinculado do HDInsight sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="fc17b-159">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
* <span data-ttu-id="fc17b-160">Você pode usar **seu próprio cluster do HDInsight** em vez de usar um cluster do HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="fc17b-160">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="fc17b-161">Confira [Serviço vinculado do HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="fc17b-161">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="fc17b-162">Olá HDInsight cluster cria um **contêiner padrão** no armazenamento de blob Olá especificado no hello JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="fc17b-162">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="fc17b-163">HDInsight não exclui esse contêiner quando Olá cluster é excluído.</span><span class="sxs-lookup"><span data-stu-id="fc17b-163">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="fc17b-164">Este comportamento ocorre por design.</span><span class="sxs-lookup"><span data-stu-id="fc17b-164">This behavior is by design.</span></span> <span data-ttu-id="fc17b-165">Com o serviço de vinculado do HDInsight sob demanda, um cluster HDInsight é criado sempre que uma fatia é processada, a menos que haja um cluster existente de ao vivo (**timeToLive**) e é excluído quando Olá processamento é concluído.</span><span class="sxs-lookup"><span data-stu-id="fc17b-165">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>

    <span data-ttu-id="fc17b-166">Quanto mais fatias forem processadas, você verá muitos contêineres no armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc17b-166">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="fc17b-167">Se não precisar para solução de problemas de trabalhos de saudação, talvez você queira toodelete-os custos de armazenamento do tooreduce hello.</span><span class="sxs-lookup"><span data-stu-id="fc17b-167">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="fc17b-168">nomes de saudação desses contêineres seguem um padrão: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="fc17b-168">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="fc17b-169">Use ferramentas como [Gerenciador de armazenamento do Microsoft](http://storageexplorer.com/) armazenamento de blobs de contêineres toodelete do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc17b-169">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

<span data-ttu-id="fc17b-170">Confira [Serviço vinculado do HDInsight sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="fc17b-170">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="fc17b-171">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="fc17b-171">inputdataset.json</span></span>

```JSON
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

<span data-ttu-id="fc17b-172">Olá JSON define um conjunto de dados chamado **AzureBlobInput**, que representa dados de entrada de uma atividade no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc17b-172">hello JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="fc17b-173">Além disso, ele especifica que os dados de entrada hello estão localizados no contêiner de blob Olá chamado **adfgetstarted** e Olá pasta chamada **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="fc17b-173">In addition, it specifies that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

<span data-ttu-id="fc17b-174">Olá, tabela a seguir fornece descrições para propriedades JSON Olá usadas no trecho hello:</span><span class="sxs-lookup"><span data-stu-id="fc17b-174">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="fc17b-175">Propriedade</span><span class="sxs-lookup"><span data-stu-id="fc17b-175">Property</span></span> | <span data-ttu-id="fc17b-176">Descrição</span><span class="sxs-lookup"><span data-stu-id="fc17b-176">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="fc17b-177">type</span><span class="sxs-lookup"><span data-stu-id="fc17b-177">type</span></span> |<span data-ttu-id="fc17b-178">propriedade de tipo de saudação é definida tooAzureBlob porque os dados residem no armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc17b-178">hello type property is set tooAzureBlob because data resides in Azure blob storage.</span></span> |
| <span data-ttu-id="fc17b-179">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="fc17b-179">linkedServiceName</span></span> |<span data-ttu-id="fc17b-180">refere-se toohello StorageLinkedService criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fc17b-180">refers toohello StorageLinkedService you created earlier.</span></span> |
| <span data-ttu-id="fc17b-181">fileName</span><span class="sxs-lookup"><span data-stu-id="fc17b-181">fileName</span></span> |<span data-ttu-id="fc17b-182">Essa propriedade é opcional.</span><span class="sxs-lookup"><span data-stu-id="fc17b-182">This property is optional.</span></span> <span data-ttu-id="fc17b-183">Se você omitir essa propriedade, todos os arquivos de saudação do hello folderPath são escolhidos.</span><span class="sxs-lookup"><span data-stu-id="fc17b-183">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="fc17b-184">Nesse caso, somente Olá input.log é processado.</span><span class="sxs-lookup"><span data-stu-id="fc17b-184">In this case, only hello input.log is processed.</span></span> |
| <span data-ttu-id="fc17b-185">type</span><span class="sxs-lookup"><span data-stu-id="fc17b-185">type</span></span> |<span data-ttu-id="fc17b-186">arquivos de log Olá estão no formato de texto, para que possamos usar TextFormat.</span><span class="sxs-lookup"><span data-stu-id="fc17b-186">hello log files are in text format, so we use TextFormat.</span></span> |
| <span data-ttu-id="fc17b-187">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="fc17b-187">columnDelimiter</span></span> |<span data-ttu-id="fc17b-188">as colunas nos arquivos de log de saudação são delimitadas por um caractere de vírgula ()</span><span class="sxs-lookup"><span data-stu-id="fc17b-188">columns in hello log files are delimited by a comma character (,)</span></span> |
| <span data-ttu-id="fc17b-189">frequência/intervalo</span><span class="sxs-lookup"><span data-stu-id="fc17b-189">frequency/interval</span></span> |<span data-ttu-id="fc17b-190">frequência definida tooMonth e o intervalo é 1, o que significa que as fatias de entrada hello estarão disponíveis mensalmente.</span><span class="sxs-lookup"><span data-stu-id="fc17b-190">frequency set tooMonth and interval is 1, which means that hello input slices are available monthly.</span></span> |
| <span data-ttu-id="fc17b-191">externo</span><span class="sxs-lookup"><span data-stu-id="fc17b-191">external</span></span> |<span data-ttu-id="fc17b-192">Essa propriedade é definida tootrue se os dados de entrada hello não são gerados pelo serviço da fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="fc17b-192">this property is set tootrue if hello input data is not generated by hello Data Factory service.</span></span> |

### <a name="outputdatasetjson"></a><span data-ttu-id="fc17b-193">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="fc17b-193">outputdataset.json</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "adfgetstarted/partitioneddata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="fc17b-194">Olá JSON define um conjunto de dados chamado **AzureBlobOutput**, que representa dados de saída para uma atividade no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc17b-194">hello JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in hello pipeline.</span></span> <span data-ttu-id="fc17b-195">Além disso, ele especifica que resultados Olá são armazenados no contêiner de blob Olá chamado **adfgetstarted** e Olá pasta chamada **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="fc17b-195">In addition, it specifies that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="fc17b-196">Olá **disponibilidade** seção especifica esse conjunto de dados de saída de saudação é produzido por mês.</span><span class="sxs-lookup"><span data-stu-id="fc17b-196">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="fc17b-197">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="fc17b-197">pipeline.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fc17b-198">Substitua **storageaccountname** pelo nome da sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc17b-198">Replace **storageaccountname** with name of your Azure storage account.</span></span>
>
>

```JSON
{
    "name": "MyFirstPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [{
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                "scriptLinkedService": "AzureStorageLinkedService",
                "defines": {
                    "inputtable": "wasb://adfgetstarted@<stroageaccountname>.blob.core.windows.net/inputdata",
                    "partitionedtable": "wasb://adfgetstarted@<stroageaccountname>t.blob.core.windows.net/partitioneddata"
                }
            },
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "policy": {
                "concurrency": 1,
                "retry": 3
            },
            "scheduler": {
                "frequency": "Month",
                "interval": 1
            },
            "name": "RunSampleHiveActivity",
            "linkedServiceName": "HDInsightOnDemandLinkedService"
        }],
        "start": "2017-07-10T00:00:00Z",
        "end": "2017-07-11T00:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="fc17b-199">No trecho JSON a saudação, você está criando um pipeline que consiste em uma única atividade que usa dados de tooprocess do Hive em um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fc17b-199">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess data on a HDInsight cluster.</span></span>

<span data-ttu-id="fc17b-200">arquivo de script do Hive Hello, **partitionweblogs.hql**, é armazenado no hello conta de armazenamento do Azure (especificado por scriptLinkedService hello, chamado **StorageLinkedService**) e, na **script**  pasta no contêiner Olá **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="fc17b-200">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **StorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

<span data-ttu-id="fc17b-201">Olá **define** seção especifica as configurações de tempo de execução que são passadas script do hive toohello como valores de configuração do Hive (por exemplo ${hiveconf: inputtable}, ${hiveconf:partitionedtable}).</span><span class="sxs-lookup"><span data-stu-id="fc17b-201">hello **defines** section specifies runtime settings that are passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

<span data-ttu-id="fc17b-202">Olá **iniciar** e **final** propriedades do pipeline de saudação especifica o período ativo de saudação do pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc17b-202">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

<span data-ttu-id="fc17b-203">Atividade Olá JSON, você especificar esse script de Hive Olá é executado em computação Olá especificada pelo Olá **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="fc17b-203">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

> [!NOTE]
> <span data-ttu-id="fc17b-204">Consulte "JSON de Pipeline" [Pipelines e atividades do Azure Data Factory](data-factory-create-pipelines.md) para obter detalhes sobre as propriedades JSON usados em Olá anterior de exemplo.</span><span class="sxs-lookup"><span data-stu-id="fc17b-204">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in hello preceding example.</span></span>
>
>

## <a name="set-global-variables"></a><span data-ttu-id="fc17b-205">Definir variáveis globais</span><span class="sxs-lookup"><span data-stu-id="fc17b-205">Set global variables</span></span>
<span data-ttu-id="fc17b-206">No Azure PowerShell, execute Olá comandos a seguir depois de substituir os valores hello com seu próprio:</span><span class="sxs-lookup"><span data-stu-id="fc17b-206">In Azure PowerShell, execute hello following commands after replacing hello values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fc17b-207">Veja a seção [Pré-requisitos](#prerequisites) para obter instruções sobre como obter a ID do cliente, o segredo do cliente, a ID do locatário e ID da assinatura.</span><span class="sxs-lookup"><span data-stu-id="fc17b-207">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>
>
>

```PowerShell
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
$adf = "FirstDataFactoryREST"
```


## <a name="authenticate-with-aad"></a><span data-ttu-id="fc17b-208">Autenticar com o AAD</span><span class="sxs-lookup"><span data-stu-id="fc17b-208">Authenticate with AAD</span></span>

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken)
```


## <a name="create-data-factory"></a><span data-ttu-id="fc17b-209">Criar um data factory</span><span class="sxs-lookup"><span data-stu-id="fc17b-209">Create data factory</span></span>
<span data-ttu-id="fc17b-210">Nesta etapa, você criará um Azure Data Factory chamado **FirstDataFactoryREST**.</span><span class="sxs-lookup"><span data-stu-id="fc17b-210">In this step, you create an Azure Data Factory named **FirstDataFactoryREST**.</span></span> <span data-ttu-id="fc17b-211">Uma fábrica de dados pode ter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="fc17b-211">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="fc17b-212">Um pipeline em um data factory pode ter uma ou mais atividades.</span><span class="sxs-lookup"><span data-stu-id="fc17b-212">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="fc17b-213">Por exemplo, um atividade de cópia toocopy dados de um repositório de dados de destino do código-fonte tooa e uma atividade de Hive do HDInsight toorun os dados de um Hive script tootransform.</span><span class="sxs-lookup"><span data-stu-id="fc17b-213">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform data.</span></span> <span data-ttu-id="fc17b-214">Execute Olá fábrica de dados de saudação de toocreate comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="fc17b-214">Run hello following commands toocreate hello data factory:</span></span>

1. <span data-ttu-id="fc17b-215">Atribuir Olá comando toovariable chamado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="fc17b-215">Assign hello command toovariable named **cmd**.</span></span>

    <span data-ttu-id="fc17b-216">Confirmar esse nome Olá Olá da fábrica de dados especificadas aqui (ADFCopyTutorialDF) correspondências Olá nome especificado no hello **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="fc17b-216">Confirm that hello name of hello data factory you specify here (ADFCopyTutorialDF) matches hello name specified in hello **datafactory.json**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/FirstDataFactoryREST?api-version=2015-10-01};
    ```
2. <span data-ttu-id="fc17b-217">Execute o comando hello usando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="fc17b-217">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="fc17b-218">Exibir resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc17b-218">View hello results.</span></span> <span data-ttu-id="fc17b-219">Se a fábrica de dados Olá foi criada com êxito, você vê Olá JSON Olá fábrica de dados em Olá **resultados**; caso contrário, você verá uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="fc17b-219">If hello data factory has been successfully created, you see hello JSON for hello data factory in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

<span data-ttu-id="fc17b-220">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="fc17b-220">Note hello following points:</span></span>

* <span data-ttu-id="fc17b-221">nome de saudação do hello Azure Data Factory deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="fc17b-221">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="fc17b-222">Se você vir o erro Olá nos resultados: **"FirstDataFactoryREST" nome da fábrica de dados não está disponível**, Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="fc17b-222">If you see hello error in results: **Data factory name “FirstDataFactoryREST” is not available**, do hello following steps:</span></span>
  1. <span data-ttu-id="fc17b-223">Alterar nome da saudação (por exemplo, yournameFirstDataFactoryREST) em Olá **datafactory.json** arquivo.</span><span class="sxs-lookup"><span data-stu-id="fc17b-223">Change hello name (for example, yournameFirstDataFactoryREST) in hello **datafactory.json** file.</span></span> <span data-ttu-id="fc17b-224">Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="fc17b-224">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
  2. <span data-ttu-id="fc17b-225">No comando primeiro Olá Olá onde **$cmd** variável é atribuída a um valor, substitua FirstDataFactoryREST pelo novo nome de saudação e execute o comando de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc17b-225">In hello first command where hello **$cmd** variable is assigned a value, replace FirstDataFactoryREST with hello new name and run hello command.</span></span>
  3. <span data-ttu-id="fc17b-226">Execute Olá dois comandos tooinvoke Olá API REST toocreate Olá dados fábrica e impressão Olá resultados da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc17b-226">Run hello next two commands tooinvoke hello REST API toocreate hello data factory and print hello results of hello operation.</span></span>
* <span data-ttu-id="fc17b-227">toocreate instâncias de fábrica de dados, você precisa toobe um colaborador/administrador de saudação assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="fc17b-227">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="fc17b-228">nome Olá Olá da fábrica de dados pode ser registrado como um nome DNS no futuro de saudação e, portanto, se tornar publicamente visível.</span><span class="sxs-lookup"><span data-stu-id="fc17b-228">hello name of hello data factory may be registered as a DNS name in hello future and hence become publicly visible.</span></span>
* <span data-ttu-id="fc17b-229">Se você receber o erro Olá: "**esta assinatura não está registrado toouse namespace DataFactory**", execute um dos seguintes hello e tente publicar novamente:</span><span class="sxs-lookup"><span data-stu-id="fc17b-229">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span>

  * <span data-ttu-id="fc17b-230">No Azure PowerShell, execute Olá provedor do comando tooregister Olá fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="fc17b-230">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

      <span data-ttu-id="fc17b-231">Você pode executar Olá tooconfirm de comando a seguir que Olá Data Factory provedor está registrado:</span><span class="sxs-lookup"><span data-stu-id="fc17b-231">You can run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="fc17b-232">Usando o logon Olá assinatura do Azure em Olá [portal do Azure](https://portal.azure.com) e navegue tooa folha de fábrica de dados (ou) criar uma fábrica de dados no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc17b-232">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="fc17b-233">Esta ação registra automaticamente o provedor de saudação para você.</span><span class="sxs-lookup"><span data-stu-id="fc17b-233">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="fc17b-234">Antes de criar um pipeline, é necessário toocreate algumas entidades da fábrica de dados pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="fc17b-234">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="fc17b-235">Você primeiro criar dados de toolink serviços vinculados repositórios/calcula tooyour dados armazenam, definem a entrada e saída de dados de toorepresent de conjuntos de dados em repositórios de dados vinculados.</span><span class="sxs-lookup"><span data-stu-id="fc17b-235">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent data in linked data stores.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="fc17b-236">Criar serviços vinculados</span><span class="sxs-lookup"><span data-stu-id="fc17b-236">Create linked services</span></span>
<span data-ttu-id="fc17b-237">Nesta etapa, você pode vincular sua conta de armazenamento do Azure e uma fábrica de dados sob demanda do Azure HDInsight cluster tooyour.</span><span class="sxs-lookup"><span data-stu-id="fc17b-237">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="fc17b-238">Olá conta de armazenamento do Azure mantém Olá dados de entrada e saídos para o pipeline de saudação neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="fc17b-238">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="fc17b-239">Olá serviço vinculado do HDInsight é toorun usado um script de Hive especificado na atividade de saudação do pipeline de saudação neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="fc17b-239">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="fc17b-240">Criar o serviço vinculado do armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="fc17b-240">Create Azure Storage linked service</span></span>
<span data-ttu-id="fc17b-241">Nesta etapa, você vincular sua fábrica de dados de tooyour de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc17b-241">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="fc17b-242">Com este tutorial, você usar Olá mesma conta de armazenamento do Azure, dados de entrada/saída toostore e hello HQL arquivo de script.</span><span class="sxs-lookup"><span data-stu-id="fc17b-242">With this tutorial, you use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="fc17b-243">Atribuir Olá comando toovariable chamado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="fc17b-243">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azurestoragelinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="fc17b-244">Execute o comando hello usando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="fc17b-244">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="fc17b-245">Exibir resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc17b-245">View hello results.</span></span> <span data-ttu-id="fc17b-246">Se Olá vinculado serviço foi criado com êxito, consulte Olá JSON para o serviço de saudação vinculado no hello **resultados**; caso contrário, você verá uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="fc17b-246">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="fc17b-247">Criar o serviço vinculado do Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="fc17b-247">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="fc17b-248">Nesta etapa, você vincular uma fábrica de dados sob demanda HDInsight cluster tooyour.</span><span class="sxs-lookup"><span data-stu-id="fc17b-248">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="fc17b-249">cluster do HDInsight Olá é criado em tempo de execução e excluído após a conclusão ocioso e processamento para o período de tempo especificado Olá automaticamente.</span><span class="sxs-lookup"><span data-stu-id="fc17b-249">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span> <span data-ttu-id="fc17b-250">Você pode usar seu próprio cluster do HDInsight em vez de usar um cluster do HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="fc17b-250">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="fc17b-251">Veja [Serviços vinculados de computação](data-factory-compute-linked-services.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="fc17b-251">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="fc17b-252">Atribuir Olá comando toovariable chamado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="fc17b-252">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@hdinsightondemandlinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/hdinsightondemandlinkedservice?api-version=2015-10-01};
    ```
2. <span data-ttu-id="fc17b-253">Execute o comando hello usando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="fc17b-253">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="fc17b-254">Exibir resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc17b-254">View hello results.</span></span> <span data-ttu-id="fc17b-255">Se Olá vinculado serviço foi criado com êxito, consulte Olá JSON para o serviço de saudação vinculado no hello **resultados**; caso contrário, você verá uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="fc17b-255">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="fc17b-256">Criar conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="fc17b-256">Create datasets</span></span>
<span data-ttu-id="fc17b-257">Nesta etapa, você cria conjuntos de dados toorepresent Olá entrada e saída de dados para o processamento do Hive.</span><span class="sxs-lookup"><span data-stu-id="fc17b-257">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="fc17b-258">Esses conjuntos de dados Consulte toohello **StorageLinkedService** você tiver criado anteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="fc17b-258">These datasets refer toohello **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="fc17b-259">Olá tooan de pontos de serviço vinculado conta de armazenamento do Azure e conjuntos de dados especificam contêiner, pasta, nome do arquivo no armazenamento de saudação que contém a entrada e saída de dados.</span><span class="sxs-lookup"><span data-stu-id="fc17b-259">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="fc17b-260">Criar conjunto de dados de entrada</span><span class="sxs-lookup"><span data-stu-id="fc17b-260">Create input dataset</span></span>
<span data-ttu-id="fc17b-261">Nesta etapa, você deve criar hello conjunto de dados de entrada toorepresent entrada dados armazenados no armazenamento de BLOBs do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="fc17b-261">In this step, you create hello input dataset toorepresent input data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="fc17b-262">Atribuir Olá comando toovariable chamado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="fc17b-262">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="fc17b-263">Execute o comando hello usando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="fc17b-263">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="fc17b-264">Exibir resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc17b-264">View hello results.</span></span> <span data-ttu-id="fc17b-265">Se Olá conjunto de dados foi criado com êxito, você verá hello JSON para o conjunto de dados Olá Olá **resultados**; caso contrário, você verá uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="fc17b-265">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="fc17b-266">Criar conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="fc17b-266">Create output dataset</span></span>
<span data-ttu-id="fc17b-267">Nesta etapa, você deve criar Olá saída conjunto toorepresent saída de dados armazenados em Olá armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc17b-267">In this step, you create hello output dataset toorepresent output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="fc17b-268">Atribuir Olá comando toovariable chamado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="fc17b-268">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="fc17b-269">Execute o comando hello usando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="fc17b-269">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="fc17b-270">Exibir resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc17b-270">View hello results.</span></span> <span data-ttu-id="fc17b-271">Se Olá conjunto de dados foi criado com êxito, você verá hello JSON para o conjunto de dados Olá Olá **resultados**; caso contrário, você verá uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="fc17b-271">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-pipeline"></a><span data-ttu-id="fc17b-272">Criar um pipeline</span><span class="sxs-lookup"><span data-stu-id="fc17b-272">Create pipeline</span></span>
<span data-ttu-id="fc17b-273">Nesta etapa, você cria seu primeiro pipeline com a atividade **HDInsightHive** .</span><span class="sxs-lookup"><span data-stu-id="fc17b-273">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="fc17b-274">Entrada fatia está disponível mensal (frequência: mês, intervalo: 1), fatias de saída é produzida mensal e Olá Agendador para a atividade de saudação é também definida toomonthly.</span><span class="sxs-lookup"><span data-stu-id="fc17b-274">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="fc17b-275">Olá configurações para o conjunto de dados de saída de hello e Agendador de atividade de saudação devem corresponder.</span><span class="sxs-lookup"><span data-stu-id="fc17b-275">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="fc17b-276">Atualmente, o conjunto de dados de saída é quais unidades Olá agendamento, então você deve criar um conjunto de dados de saída, mesmo que a atividade de saudação não produz nenhuma saída.</span><span class="sxs-lookup"><span data-stu-id="fc17b-276">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="fc17b-277">Se a atividade de saudação não tem nenhuma entrada, você poderá ignorar o dataset de entrada hello criando.</span><span class="sxs-lookup"><span data-stu-id="fc17b-277">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span>

<span data-ttu-id="fc17b-278">Confirme que você vê Olá **input.log** arquivo hello **adfgetstarted/inputdata** pasta Olá armazenamento de BLOBs do Azure e execução Olá pipeline de saudação do comando toodeploy a seguir.</span><span class="sxs-lookup"><span data-stu-id="fc17b-278">Confirm that you see hello **input.log** file in hello **adfgetstarted/inputdata** folder in hello Azure blob storage, and run hello following command toodeploy hello pipeline.</span></span> <span data-ttu-id="fc17b-279">Desde Olá **iniciar** e **final** horários são definidos no hello anterior e **isPaused** é conjunto toofalse, pipeline Olá execuções (atividade no pipeline de saudação) imediatamente após a implantação.</span><span class="sxs-lookup"><span data-stu-id="fc17b-279">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>

1. <span data-ttu-id="fc17b-280">Atribuir Olá comando toovariable chamado **cmd**.</span><span class="sxs-lookup"><span data-stu-id="fc17b-280">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="fc17b-281">Execute o comando hello usando **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="fc17b-281">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="fc17b-282">Exibir resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc17b-282">View hello results.</span></span> <span data-ttu-id="fc17b-283">Se Olá conjunto de dados foi criado com êxito, você verá hello JSON para o conjunto de dados Olá Olá **resultados**; caso contrário, você verá uma mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="fc17b-283">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```
4. <span data-ttu-id="fc17b-284">Parabéns, você criou com sucesso seu primeiro pipeline usando o Azure PowerShell!</span><span class="sxs-lookup"><span data-stu-id="fc17b-284">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="fc17b-285">Monitorar o pipeline</span><span class="sxs-lookup"><span data-stu-id="fc17b-285">Monitor pipeline</span></span>
<span data-ttu-id="fc17b-286">Nesta etapa, você deve usar fatias de toomonitor de API de REST de fábrica de dados produzidas pelo pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc17b-286">In this step, you use Data Factory REST API toomonitor slices being produced by hello pipeline.</span></span>

```PowerShell
$ds ="AzureBlobOutput"

$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=1970-01-01T00%3a00%3a00.0000000Z"&"end=2016-08-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};

$results2 = Invoke-Command -scriptblock $cmd;

IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

> [!IMPORTANT]
> <span data-ttu-id="fc17b-287">A criação de um cluster do HDInsight sob demanda geralmente leva algum tempo (20 minutos, aproximadamente).</span><span class="sxs-lookup"><span data-stu-id="fc17b-287">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="fc17b-288">Portanto, espere Olá pipeline tootake **aproximadamente 30 minutos** tooprocess Olá fatia.</span><span class="sxs-lookup"><span data-stu-id="fc17b-288">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
>
>

<span data-ttu-id="fc17b-289">Executar Olá Invoke-Command e hello próximo até que você veja fatia Olá **pronto** estado ou **falha** estado.</span><span class="sxs-lookup"><span data-stu-id="fc17b-289">Run hello Invoke-Command and hello next one until you see hello slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="fc17b-290">Quando a fatia hello está no estado pronto, verificar Olá **partitioneddata** pasta Olá **adfgetstarted** dados de saída do contêiner em seu armazenamento de blob para hello.</span><span class="sxs-lookup"><span data-stu-id="fc17b-290">When hello slice is in Ready state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  <span data-ttu-id="fc17b-291">a criação de um cluster do HDInsight sob demanda Olá normalmente leva algum tempo.</span><span class="sxs-lookup"><span data-stu-id="fc17b-291">hello creation of an on-demand HDInsight cluster usually takes some time.</span></span>

![dados de saída](./media/data-factory-build-your-first-pipeline-using-rest-api/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="fc17b-293">arquivo de entrada Hello é excluído quando a fatia de saudação é processada com êxito.</span><span class="sxs-lookup"><span data-stu-id="fc17b-293">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="fc17b-294">Portanto, se você deseja toorerun Olá fatia ou Olá tutorial novamente, pasta de carregamento Olá arquivo de entrada (input.log) toohello inputdata do contêiner de adfgetstarted hello.</span><span class="sxs-lookup"><span data-stu-id="fc17b-294">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

<span data-ttu-id="fc17b-295">Você também pode usar fatias toomonitor portal do Azure e solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="fc17b-295">You can also use Azure portal toomonitor slices and troubleshoot any issues.</span></span> <span data-ttu-id="fc17b-296">Veja os detalhes em [Monitorar pipelines usando o portal do Azure](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) .</span><span class="sxs-lookup"><span data-stu-id="fc17b-296">See [Monitor pipelines using Azure portal](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) details.</span></span>

## <a name="summary"></a><span data-ttu-id="fc17b-297">Resumo</span><span class="sxs-lookup"><span data-stu-id="fc17b-297">Summary</span></span>
<span data-ttu-id="fc17b-298">Neste tutorial, você criou um tooprocess dados da fábrica de dados do Azure executando o script do Hive em um cluster de hadoop de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fc17b-298">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="fc17b-299">Você usou Olá Editor da fábrica de dados em Olá toodo portal do Azure Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fc17b-299">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>

1. <span data-ttu-id="fc17b-300">Foi criada uma **data factory**do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc17b-300">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="fc17b-301">Foram criados dois **serviços vinculados**:</span><span class="sxs-lookup"><span data-stu-id="fc17b-301">Created two **linked services**:</span></span>
   1. <span data-ttu-id="fc17b-302">**Armazenamento do Azure** vinculado serviço toolink seu armazenamento de BLOBs do Azure que contém a fábrica de dados de toohello de arquivos de entrada/saída.</span><span class="sxs-lookup"><span data-stu-id="fc17b-302">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="fc17b-303">**HDInsight do Azure** toolink de serviço vinculado sob demanda uma fábrica de dados sob demanda HDInsight Hadoop cluster toohello.</span><span class="sxs-lookup"><span data-stu-id="fc17b-303">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="fc17b-304">A fábrica de dados do Azure cria um HDInsight Hadoop dados de entrada do cluster tooprocess just-in-time e produzir dados de saída.</span><span class="sxs-lookup"><span data-stu-id="fc17b-304">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="fc17b-305">Criados dois **conjuntos de dados**, que descrevem os dados de entrada e saídos para a atividade de Hive do HDInsight no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc17b-305">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="fc17b-306">Foi criado um **pipeline** com uma atividade **Hive do HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="fc17b-306">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc17b-307">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fc17b-307">Next steps</span></span>
<span data-ttu-id="fc17b-308">Neste artigo, você criou um pipeline com uma atividade de transformação (atividade do HDInsight) que executa um script Hive em um cluster do HDInsight do Azure sob demanda.</span><span class="sxs-lookup"><span data-stu-id="fc17b-308">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="fc17b-309">toosee como toouse dados de toocopy uma atividade de cópia de um tooAzure de BLOBs do Azure SQL, consulte [Tutorial: copiar dados de um tooAzure de BLOBs do Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="fc17b-309">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="fc17b-310">Consulte também</span><span class="sxs-lookup"><span data-stu-id="fc17b-310">See Also</span></span>
| <span data-ttu-id="fc17b-311">Tópico</span><span class="sxs-lookup"><span data-stu-id="fc17b-311">Topic</span></span> | <span data-ttu-id="fc17b-312">Descrição</span><span class="sxs-lookup"><span data-stu-id="fc17b-312">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="fc17b-313">Referência de API REST do Data Factory</span><span class="sxs-lookup"><span data-stu-id="fc17b-313">Data Factory REST API Reference</span></span>](/rest/api/datafactory/) |<span data-ttu-id="fc17b-314">Consulte a documentação abrangente sobre os cmdlets do Data Factory</span><span class="sxs-lookup"><span data-stu-id="fc17b-314">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="fc17b-315">Pipelines</span><span class="sxs-lookup"><span data-stu-id="fc17b-315">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="fc17b-316">Este artigo ajuda você a entender os pipelines e atividades do Azure Data Factory e como toouse-los tooconstruct ponta a ponta controladas por dados fluxos de trabalho para seu cenário ou business.</span><span class="sxs-lookup"><span data-stu-id="fc17b-316">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="fc17b-317">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="fc17b-317">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="fc17b-318">Este artigo o ajuda a entender os conjuntos de dados no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="fc17b-318">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="fc17b-319">Planejamento e execução</span><span class="sxs-lookup"><span data-stu-id="fc17b-319">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="fc17b-320">Este artigo explica os aspectos de programação e a execução de saudação do modelo de aplicativo do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="fc17b-320">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="fc17b-321">Monitorar e gerenciar pipelines usando o Aplicativo de Monitoramento</span><span class="sxs-lookup"><span data-stu-id="fc17b-321">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="fc17b-322">Este artigo descreve como toomonitor, gerenciar e depurar pipelines usando Olá monitoramento e gerenciamento de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fc17b-322">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
