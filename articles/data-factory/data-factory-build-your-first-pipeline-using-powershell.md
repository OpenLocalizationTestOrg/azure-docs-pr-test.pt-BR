---
title: "aaaBuild sua primeira fábrica de dados (PowerShell) | Microsoft Docs"
description: "Neste tutorial, você cria um pipeline de exemplo do Azure Data Factory usando o Azure PowerShell."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 22ec1236-ea86-4eb7-b903-0e79a58b90c7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 626260798b56d590577b3c4b24f7cf52873c9f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-powershell"></a><span data-ttu-id="950d2-103">Tutorial: Compilar seu primeiro data factory do Azure usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="950d2-103">Tutorial: Build your first Azure data factory using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="950d2-104">Visão geral e pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="950d2-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="950d2-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="950d2-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="950d2-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="950d2-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="950d2-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="950d2-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="950d2-108">Modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="950d2-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="950d2-109">API REST</span><span class="sxs-lookup"><span data-stu-id="950d2-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>

<span data-ttu-id="950d2-110">Neste artigo, você usa toocreate do PowerShell do Azure a primeira data factory do Azure.</span><span class="sxs-lookup"><span data-stu-id="950d2-110">In this article, you use Azure PowerShell toocreate your first Azure data factory.</span></span> <span data-ttu-id="950d2-111">tutorial de saudação toodo usando outras ferramentas/SDKs, selecione uma das opções de saudação da lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="950d2-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="950d2-112">pipeline de saudação neste tutorial tem uma atividade: **atividade Hive do HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="950d2-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="950d2-113">Essa atividade executa um script do hive em um cluster de HDInsight do Azure que transforma dados de saída de tooproduce de entrada.</span><span class="sxs-lookup"><span data-stu-id="950d2-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="950d2-114">pipeline de saudação é agendado toorun depois de um mês entre hello especificar horários de início e término.</span><span class="sxs-lookup"><span data-stu-id="950d2-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="950d2-115">pipeline de dados Olá neste tutorial transforma dados de saída de tooproduce de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="950d2-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="950d2-116">Ele não copia dados de um repositório de dados de destino fonte dados repositório tooa.</span><span class="sxs-lookup"><span data-stu-id="950d2-116">It does not copy data from a source data store tooa destination data store.</span></span> <span data-ttu-id="950d2-117">Para obter um tutorial sobre como toocopy dados usando a fábrica de dados do Azure, consulte [Tutorial: copiar dados de armazenamento de Blob tooSQL banco de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="950d2-117">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="950d2-118">Um pipeline pode ter mais de uma atividade.</span><span class="sxs-lookup"><span data-stu-id="950d2-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="950d2-119">E, é possível encadear duas atividades (executadas uma atividade após o outro), definindo Olá o conjunto de dados de saída de uma atividade Olá outra atividade de conjunto de dados de saudação de entrada.</span><span class="sxs-lookup"><span data-stu-id="950d2-119">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="950d2-120">Para saber mais, confira [Agendamento e execução no Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="950d2-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="950d2-121">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="950d2-121">Prerequisites</span></span>
* <span data-ttu-id="950d2-122">Leia [visão geral do Tutorial](data-factory-build-your-first-pipeline.md) artigo e hello completa **pré-requisito** etapas.</span><span class="sxs-lookup"><span data-stu-id="950d2-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="950d2-123">Siga as instruções em [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) artigo tooinstall versão mais recente do PowerShell do Azure no seu computador.</span><span class="sxs-lookup"><span data-stu-id="950d2-123">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="950d2-124">(opcional) Este artigo não aborda todos os cmdlets da fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="950d2-124">(optional) This article does not cover all hello Data Factory cmdlets.</span></span> <span data-ttu-id="950d2-125">Consulte [Referência de cmdlet de Data Factory](/powershell/module/azurerm.datafactories) para obter uma documentação abrangente sobre os cmdlets de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="950d2-125">See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on Data Factory cmdlets.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="950d2-126">Criar um data factory</span><span class="sxs-lookup"><span data-stu-id="950d2-126">Create data factory</span></span>
<span data-ttu-id="950d2-127">Nesta etapa, você usar o Azure PowerShell toocreate uma fábrica de dados do Azure denominado **FirstDataFactoryPSH**.</span><span class="sxs-lookup"><span data-stu-id="950d2-127">In this step, you use Azure PowerShell toocreate an Azure Data Factory named **FirstDataFactoryPSH**.</span></span> <span data-ttu-id="950d2-128">Uma fábrica de dados pode ter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="950d2-128">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="950d2-129">Um pipeline em um data factory pode ter uma ou mais atividades.</span><span class="sxs-lookup"><span data-stu-id="950d2-129">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="950d2-130">Por exemplo, dados de toocopy uma atividade de cópia de um repositório de dados de destino do código-fonte tooa e uma atividade de Hive do HDInsight toorun um tootransform de script do Hive dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="950d2-130">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data.</span></span> <span data-ttu-id="950d2-131">Vamos começar com a criação de fábrica de dados Olá nesta etapa.</span><span class="sxs-lookup"><span data-stu-id="950d2-131">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="950d2-132">Inicie o PowerShell do Azure e execute Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="950d2-132">Start Azure PowerShell and run hello following command.</span></span> <span data-ttu-id="950d2-133">Mantenha o Azure PowerShell aberta até o fim deste tutorial hello.</span><span class="sxs-lookup"><span data-stu-id="950d2-133">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="950d2-134">Se você fecha e reabrir, será necessário toorun esses comandos novamente.</span><span class="sxs-lookup"><span data-stu-id="950d2-134">If you close and reopen, you need toorun these commands again.</span></span>
   * <span data-ttu-id="950d2-135">Execute Olá comando a seguir e insira o nome de usuário de saudação e a senha que você use toosign em toohello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="950d2-135">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```    
   * <span data-ttu-id="950d2-136">Execute Olá tooview de comando a seguir todas as assinaturas de saudação para esta conta.</span><span class="sxs-lookup"><span data-stu-id="950d2-136">Run hello following command tooview all hello subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription 
    ```
   * <span data-ttu-id="950d2-137">Execute Olá assinatura de saudação do comando tooselect que você deseja toowork com a seguir.</span><span class="sxs-lookup"><span data-stu-id="950d2-137">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="950d2-138">Essa assinatura deve ser Olá mesmas Olá aquele que você usou no portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="950d2-138">This subscription should be hello same as hello one you used in hello Azure portal.</span></span>
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```     
2. <span data-ttu-id="950d2-139">Criar um grupo de recursos do Azure denominado **ADFTutorialResourceGroup** executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="950d2-139">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command:</span></span>
    
    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    <span data-ttu-id="950d2-140">Algumas das etapas de saudação neste tutorial presumem que você use o grupo de recursos de saudação chamado ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="950d2-140">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="950d2-141">Se você usar um grupo de recursos diferentes, será necessário toouse-lo no lugar de ADFTutorialResourceGroup neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="950d2-141">If you use a different resource group, you need toouse it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="950d2-142">Executar Olá **New-AzureRmDataFactory** cmdlet que cria uma fábrica de dados denominada **FirstDataFactoryPSH**.</span><span class="sxs-lookup"><span data-stu-id="950d2-142">Run hello **New-AzureRmDataFactory** cmdlet that creates a data factory named **FirstDataFactoryPSH**.</span></span>

    ```PowerShell
    New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH –Location "West US"
    ```
<span data-ttu-id="950d2-143">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="950d2-143">Note hello following points:</span></span>

* <span data-ttu-id="950d2-144">nome de saudação do hello Azure Data Factory deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="950d2-144">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="950d2-145">Se você receber o erro Olá **"FirstDataFactoryPSH" nome da fábrica de dados não está disponível**, alterar o nome da saudação (por exemplo, yournameFirstDataFactoryPSH).</span><span class="sxs-lookup"><span data-stu-id="950d2-145">If you receive hello error **Data factory name “FirstDataFactoryPSH” is not available**, change hello name (for example, yournameFirstDataFactoryPSH).</span></span> <span data-ttu-id="950d2-146">Use esse nome em vez de ADFTutorialFactoryPSH ao executar as etapas neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="950d2-146">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="950d2-147">Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="950d2-147">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="950d2-148">toocreate instâncias de fábrica de dados, você precisa toobe um colaborador/administrador de saudação assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="950d2-148">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="950d2-149">nome Olá Olá da fábrica de dados pode ser registrado como um nome DNS no hello futuro e, portanto, se tornarão visível publicamente.</span><span class="sxs-lookup"><span data-stu-id="950d2-149">hello name of hello data factory may be registered as a DNS name in hello future and hence become publically visible.</span></span>
* <span data-ttu-id="950d2-150">Se você receber o erro Olá: "**esta assinatura não está registrado toouse namespace DataFactory**", execute um dos seguintes hello e tente publicar novamente:</span><span class="sxs-lookup"><span data-stu-id="950d2-150">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span>

  * <span data-ttu-id="950d2-151">No Azure PowerShell, execute Olá provedor do comando tooregister Olá fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="950d2-151">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
      <span data-ttu-id="950d2-152">Você pode executar Olá tooconfirm de comando a seguir que Olá Data Factory provedor está registrado:</span><span class="sxs-lookup"><span data-stu-id="950d2-152">You can run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="950d2-153">Usando o logon Olá assinatura do Azure em Olá [portal do Azure](https://portal.azure.com) e navegue tooa folha de fábrica de dados (ou) criar uma fábrica de dados no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="950d2-153">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="950d2-154">Esta ação registra automaticamente o provedor de saudação para você.</span><span class="sxs-lookup"><span data-stu-id="950d2-154">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="950d2-155">Antes de criar um pipeline, é necessário toocreate algumas entidades da fábrica de dados pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="950d2-155">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="950d2-156">Você primeiro criar dados de toolink serviços vinculados repositórios/calcula tooyour dados armazenam, definem a entrada e saída de dados de entrada/saída toorepresent conjuntos de dados em repositórios de dados vinculados e, em seguida, criar o pipeline de saudação com uma atividade que usa esses conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="950d2-156">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent input/output data in linked data stores, and then create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="950d2-157">Criar serviços vinculados</span><span class="sxs-lookup"><span data-stu-id="950d2-157">Create linked services</span></span>
<span data-ttu-id="950d2-158">Nesta etapa, você pode vincular sua conta de armazenamento do Azure e uma fábrica de dados sob demanda do Azure HDInsight cluster tooyour.</span><span class="sxs-lookup"><span data-stu-id="950d2-158">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="950d2-159">Olá conta de armazenamento do Azure mantém Olá dados de entrada e saídos para o pipeline de saudação neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="950d2-159">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="950d2-160">Olá serviço vinculado do HDInsight é toorun usado um script de Hive especificado na atividade de saudação do pipeline de saudação neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="950d2-160">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span> <span data-ttu-id="950d2-161">Identificar quais dados repositório/computação serviços são usados em seu cenário e vincular a fábrica de dados desses serviços toohello criando serviços vinculados.</span><span class="sxs-lookup"><span data-stu-id="950d2-161">Identify what data store/compute services are used in your scenario and link those services toohello data factory by creating linked services.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="950d2-162">Criar o serviço vinculado do armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="950d2-162">Create Azure Storage linked service</span></span>
<span data-ttu-id="950d2-163">Nesta etapa, você vincular sua fábrica de dados de tooyour de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="950d2-163">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="950d2-164">Use Olá mesma conta de armazenamento do Azure, dados de entrada/saída toostore e hello HQL arquivo de script.</span><span class="sxs-lookup"><span data-stu-id="950d2-164">You use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="950d2-165">Crie um arquivo JSON chamado StorageLinkedService.json na pasta de C:\ADFGetStarted Olá com hello seguindo conteúdo.</span><span class="sxs-lookup"><span data-stu-id="950d2-165">Create a JSON file named StorageLinkedService.json in hello C:\ADFGetStarted folder with hello following content.</span></span> <span data-ttu-id="950d2-166">Crie pasta Olá ADFGetStarted se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="950d2-166">Create hello folder ADFGetStarted if it does not already exist.</span></span>

    ```json
    {
        "name": "StorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "description": "",
            "typeProperties": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        }
    }
    ```
    <span data-ttu-id="950d2-167">Substituir **nome da conta** com nome de saudação da sua conta de armazenamento do Azure e **chave de conta** com a chave de acesso de saudação do Olá conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="950d2-167">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="950d2-168">toolearn como tooget acessar o armazenamento de chave, consulte Olá informações sobre como tooview, copiar e armazenamento regenerar chaves de acesso em [gerenciar sua conta de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="950d2-168">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
2. <span data-ttu-id="950d2-169">No PowerShell do Azure, alterne toohello ADFGetStarted pasta.</span><span class="sxs-lookup"><span data-stu-id="950d2-169">In Azure PowerShell, switch toohello ADFGetStarted folder.</span></span>
3. <span data-ttu-id="950d2-170">Você pode usar o hello **AzureRmDataFactoryLinkedService novo** cmdlet que cria um serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="950d2-170">You can use hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates a linked service.</span></span> <span data-ttu-id="950d2-171">Esse cmdlet e outros cmdlets de fábrica de dados que você usar este tutorial requer que você toopass valores para Olá *ResourceGroupName* e *DataFactoryName* parâmetros.</span><span class="sxs-lookup"><span data-stu-id="950d2-171">This cmdlet and other Data Factory cmdlets you use in this tutorial requires you toopass values for hello *ResourceGroupName* and *DataFactoryName* parameters.</span></span> <span data-ttu-id="950d2-172">Como alternativa, você pode usar **Get-AzureRmDataFactory** tooget um **DataFactory** de objeto e passar o objeto de saudação sem digitar *ResourceGroupName* e  *DataFactoryName* cada vez que você executar um cmdlet.</span><span class="sxs-lookup"><span data-stu-id="950d2-172">Alternatively, you can use **Get-AzureRmDataFactory** tooget a **DataFactory** object and pass hello object without typing *ResourceGroupName* and *DataFactoryName* each time you run a cmdlet.</span></span> <span data-ttu-id="950d2-173">Comando a seguir de execução Olá tooassign saída Olá Olá **Get-AzureRmDataFactory** cmdlet tooa **$df** variável.</span><span class="sxs-lookup"><span data-stu-id="950d2-173">Run hello following command tooassign hello output of hello **Get-AzureRmDataFactory** cmdlet tooa **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
4. <span data-ttu-id="950d2-174">Agora, execute Olá **New-AzureRmDataFactoryLinkedService** cmdlet que cria Olá vinculado **StorageLinkedService** service.</span><span class="sxs-lookup"><span data-stu-id="950d2-174">Now, run hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates hello linked **StorageLinkedService** service.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="950d2-175">Se você não executar Olá **Get-AzureRmDataFactory** toohello de saída do cmdlet e hello atribuído **$df** variável, você teria toospecify valores hello *ResourceGroupName*e *DataFactoryName* parâmetros da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="950d2-175">If you hadn't run hello **Get-AzureRmDataFactory** cmdlet and assigned hello output toohello **$df** variable, you would have toospecify values for hello *ResourceGroupName* and *DataFactoryName* parameters as follows.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName FirstDataFactoryPSH -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="950d2-176">Se você fechar o Azure PowerShell no meio de saudação do tutorial hello, você tem Olá toorun **AzureRmDataFactory Get** próxima vez que iniciar o tutorial do Azure PowerShell toocomplete saudação do cmdlet.</span><span class="sxs-lookup"><span data-stu-id="950d2-176">If you close Azure PowerShell in hello middle of hello tutorial, you have toorun hello **Get-AzureRmDataFactory** cmdlet next time you start Azure PowerShell toocomplete hello tutorial.</span></span>

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="950d2-177">Criar o serviço vinculado do Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="950d2-177">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="950d2-178">Nesta etapa, você vincular uma fábrica de dados sob demanda HDInsight cluster tooyour.</span><span class="sxs-lookup"><span data-stu-id="950d2-178">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="950d2-179">cluster do HDInsight Olá é criado em tempo de execução e excluído após a conclusão ocioso e processamento para o período de tempo especificado Olá automaticamente.</span><span class="sxs-lookup"><span data-stu-id="950d2-179">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span> <span data-ttu-id="950d2-180">Você pode usar seu próprio cluster do HDInsight em vez de usar um cluster do HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="950d2-180">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="950d2-181">Veja [Serviços vinculados de computação](data-factory-compute-linked-services.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="950d2-181">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="950d2-182">Crie um arquivo JSON chamado **HDInsightOnDemandLinkedService**. JSON no hello **C:\ADFGetStarted** pasta com hello conteúdo a seguir.</span><span class="sxs-lookup"><span data-stu-id="950d2-182">Create a JSON file named **HDInsightOnDemandLinkedService**.json in hello **C:\ADFGetStarted** folder with hello following content.</span></span>

    ```json
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "StorageLinkedService"
            }
        }
    }
    ```
    <span data-ttu-id="950d2-183">Olá, tabela a seguir fornece descrições para propriedades JSON Olá usadas no trecho hello:</span><span class="sxs-lookup"><span data-stu-id="950d2-183">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="950d2-184">Propriedade</span><span class="sxs-lookup"><span data-stu-id="950d2-184">Property</span></span> | <span data-ttu-id="950d2-185">Descrição</span><span class="sxs-lookup"><span data-stu-id="950d2-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="950d2-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="950d2-186">ClusterSize</span></span> |<span data-ttu-id="950d2-187">Especifica o tamanho de saudação do cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="950d2-187">Specifies hello size of hello HDInsight cluster.</span></span> |
   | <span data-ttu-id="950d2-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="950d2-188">TimeToLive</span></span> |<span data-ttu-id="950d2-189">Especifica que Olá de tempo ocioso para um cluster do HDInsight hello, antes de ser excluído.</span><span class="sxs-lookup"><span data-stu-id="950d2-189">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="950d2-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="950d2-190">linkedServiceName</span></span> |<span data-ttu-id="950d2-191">Especifica a conta de armazenamento de saudação que é usado toostore logs de Olá gerados pelo HDInsight</span><span class="sxs-lookup"><span data-stu-id="950d2-191">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight</span></span> |

    <span data-ttu-id="950d2-192">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="950d2-192">Note hello following points:</span></span>

   * <span data-ttu-id="950d2-193">Olá fábrica de dados cria um **baseados em Linux** cluster HDInsight para você com hello JSON.</span><span class="sxs-lookup"><span data-stu-id="950d2-193">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello JSON.</span></span> <span data-ttu-id="950d2-194">Confira [Serviço vinculado do HDInsight sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="950d2-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="950d2-195">Você pode usar **seu próprio cluster do HDInsight** em vez de usar um cluster do HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="950d2-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="950d2-196">Confira [Serviço vinculado do HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="950d2-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="950d2-197">Olá HDInsight cluster cria um **contêiner padrão** no armazenamento de blob Olá especificado no hello JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="950d2-197">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="950d2-198">HDInsight não exclui esse contêiner quando Olá cluster é excluído.</span><span class="sxs-lookup"><span data-stu-id="950d2-198">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="950d2-199">Este comportamento ocorre por design.</span><span class="sxs-lookup"><span data-stu-id="950d2-199">This behavior is by design.</span></span> <span data-ttu-id="950d2-200">Com o serviço vinculado HDInsight sob demanda, um cluster HDInsight é criado sempre que uma fatia é processada, a menos que haja um cluster ativo existente (**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="950d2-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="950d2-201">cluster de saudação é excluído automaticamente quando Olá processamento é concluído.</span><span class="sxs-lookup"><span data-stu-id="950d2-201">hello cluster is automatically deleted when hello processing is done.</span></span>

       <span data-ttu-id="950d2-202">Quanto mais fatias forem processadas, você verá muitos contêineres no armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="950d2-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="950d2-203">Se não precisar para solução de problemas de trabalhos de saudação, talvez você queira toodelete-os custos de armazenamento do tooreduce hello.</span><span class="sxs-lookup"><span data-stu-id="950d2-203">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="950d2-204">nomes de saudação desses contêineres seguem um padrão: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="950d2-204">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="950d2-205">Use ferramentas como [Gerenciador de armazenamento do Microsoft](http://storageexplorer.com/) armazenamento de blobs de contêineres toodelete do Azure.</span><span class="sxs-lookup"><span data-stu-id="950d2-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="950d2-206">Confira [Serviço vinculado do HDInsight sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="950d2-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
2. <span data-ttu-id="950d2-207">Executar Olá **AzureRmDataFactoryLinkedService novo** cmdlet que cria Olá vinculado serviço chamado HDInsightOnDemandLinkedService.</span><span class="sxs-lookup"><span data-stu-id="950d2-207">Run hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates hello linked service called HDInsightOnDemandLinkedService.</span></span>
    
    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\HDInsightOnDemandLinkedService.json
    ```

## <a name="create-datasets"></a><span data-ttu-id="950d2-208">Criar conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="950d2-208">Create datasets</span></span>
<span data-ttu-id="950d2-209">Nesta etapa, você cria conjuntos de dados toorepresent Olá entrada e saída de dados para o processamento do Hive.</span><span class="sxs-lookup"><span data-stu-id="950d2-209">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="950d2-210">Esses conjuntos de dados Consulte toohello **StorageLinkedService** você tiver criado anteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="950d2-210">These datasets refer toohello **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="950d2-211">Olá tooan de pontos de serviço vinculado conta de armazenamento do Azure e conjuntos de dados especificam contêiner, pasta, nome do arquivo no armazenamento de saudação que contém a entrada e saída de dados.</span><span class="sxs-lookup"><span data-stu-id="950d2-211">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="950d2-212">Criar conjunto de dados de entrada</span><span class="sxs-lookup"><span data-stu-id="950d2-212">Create input dataset</span></span>
1. <span data-ttu-id="950d2-213">Crie um arquivo JSON chamado **InputTable.json** em Olá **C:\ADFGetStarted** pasta com hello conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="950d2-213">Create a JSON file named **InputTable.json** in hello **C:\ADFGetStarted** folder with hello following content:</span></span>

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "StorageLinkedService",
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
    <span data-ttu-id="950d2-214">Olá JSON define um conjunto de dados chamado **AzureBlobInput**, que representa dados de entrada de uma atividade no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="950d2-214">hello JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="950d2-215">Além disso, ele especifica que os dados de entrada hello estão localizados no contêiner de blob Olá chamado **adfgetstarted** e Olá pasta chamada **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="950d2-215">In addition, it specifies that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

    <span data-ttu-id="950d2-216">Olá, tabela a seguir fornece descrições para propriedades JSON Olá usadas no trecho hello:</span><span class="sxs-lookup"><span data-stu-id="950d2-216">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="950d2-217">Propriedade</span><span class="sxs-lookup"><span data-stu-id="950d2-217">Property</span></span> | <span data-ttu-id="950d2-218">Descrição</span><span class="sxs-lookup"><span data-stu-id="950d2-218">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="950d2-219">type</span><span class="sxs-lookup"><span data-stu-id="950d2-219">type</span></span> |<span data-ttu-id="950d2-220">propriedade de tipo de saudação é definida tooAzureBlob porque os dados residem no armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="950d2-220">hello type property is set tooAzureBlob because data resides in Azure blob storage.</span></span> |
   | <span data-ttu-id="950d2-221">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="950d2-221">linkedServiceName</span></span> |<span data-ttu-id="950d2-222">refere-se toohello StorageLinkedService criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="950d2-222">refers toohello StorageLinkedService you created earlier.</span></span> |
   | <span data-ttu-id="950d2-223">fileName</span><span class="sxs-lookup"><span data-stu-id="950d2-223">fileName</span></span> |<span data-ttu-id="950d2-224">Essa propriedade é opcional.</span><span class="sxs-lookup"><span data-stu-id="950d2-224">This property is optional.</span></span> <span data-ttu-id="950d2-225">Se você omitir essa propriedade, todos os arquivos de saudação do hello folderPath são escolhidos.</span><span class="sxs-lookup"><span data-stu-id="950d2-225">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="950d2-226">Nesse caso, somente Olá input.log é processado.</span><span class="sxs-lookup"><span data-stu-id="950d2-226">In this case, only hello input.log is processed.</span></span> |
   | <span data-ttu-id="950d2-227">type</span><span class="sxs-lookup"><span data-stu-id="950d2-227">type</span></span> |<span data-ttu-id="950d2-228">arquivos de log Olá estão no formato de texto, para que possamos usar TextFormat.</span><span class="sxs-lookup"><span data-stu-id="950d2-228">hello log files are in text format, so we use TextFormat.</span></span> |
   | <span data-ttu-id="950d2-229">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="950d2-229">columnDelimiter</span></span> |<span data-ttu-id="950d2-230">colunas em arquivos de log de saudação são delimitadas pelo caractere de vírgula hello (,).</span><span class="sxs-lookup"><span data-stu-id="950d2-230">columns in hello log files are delimited by hello comma character (,).</span></span> |
   | <span data-ttu-id="950d2-231">frequência/intervalo</span><span class="sxs-lookup"><span data-stu-id="950d2-231">frequency/interval</span></span> |<span data-ttu-id="950d2-232">frequência definida tooMonth e o intervalo é 1, o que significa que as fatias de entrada hello estarão disponíveis mensalmente.</span><span class="sxs-lookup"><span data-stu-id="950d2-232">frequency set tooMonth and interval is 1, which means that hello input slices are available monthly.</span></span> |
   | <span data-ttu-id="950d2-233">externo</span><span class="sxs-lookup"><span data-stu-id="950d2-233">external</span></span> |<span data-ttu-id="950d2-234">Essa propriedade é definida tootrue se os dados de entrada hello não são gerados pelo serviço da fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="950d2-234">this property is set tootrue if hello input data is not generated by hello Data Factory service.</span></span> |
2. <span data-ttu-id="950d2-235">Execute Olá comando no conjunto de dados do Azure PowerShell toocreate Olá fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="950d2-235">Run hello following command in Azure PowerShell toocreate hello Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\InputTable.json
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="950d2-236">Criar conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="950d2-236">Create output dataset</span></span>
<span data-ttu-id="950d2-237">Agora, você pode criar hello saída dataset toorepresent Olá saída dados armazenados em Olá armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="950d2-237">Now, you create hello output dataset toorepresent hello output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="950d2-238">Crie um arquivo JSON chamado **OutputTable.json** em Olá **C:\ADFGetStarted** pasta com hello conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="950d2-238">Create a JSON file named **OutputTable.json** in hello **C:\ADFGetStarted** folder with hello following content:</span></span>

    ```json
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
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
    <span data-ttu-id="950d2-239">Olá JSON define um conjunto de dados chamado **AzureBlobOutput**, que representa dados de saída para uma atividade no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="950d2-239">hello JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in hello pipeline.</span></span> <span data-ttu-id="950d2-240">Além disso, ele especifica que resultados Olá são armazenados no contêiner de blob Olá chamado **adfgetstarted** e Olá pasta chamada **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="950d2-240">In addition, it specifies that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="950d2-241">Olá **disponibilidade** seção especifica esse conjunto de dados de saída de saudação é produzido por mês.</span><span class="sxs-lookup"><span data-stu-id="950d2-241">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>
2. <span data-ttu-id="950d2-242">Execute Olá comando no conjunto de dados do Azure PowerShell toocreate Olá fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="950d2-242">Run hello following command in Azure PowerShell toocreate hello Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\OutputTable.json
    ```

## <a name="create-pipeline"></a><span data-ttu-id="950d2-243">Criar um pipeline</span><span class="sxs-lookup"><span data-stu-id="950d2-243">Create pipeline</span></span>
<span data-ttu-id="950d2-244">Nesta etapa, você cria seu primeiro pipeline com a atividade **HDInsightHive** .</span><span class="sxs-lookup"><span data-stu-id="950d2-244">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="950d2-245">Entrada fatia está disponível mensal (frequência: mês, intervalo: 1), fatias de saída é produzida mensal e Olá Agendador para a atividade de saudação é também definida toomonthly.</span><span class="sxs-lookup"><span data-stu-id="950d2-245">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="950d2-246">Olá configurações para o conjunto de dados de saída de hello e Agendador de atividade de saudação devem corresponder.</span><span class="sxs-lookup"><span data-stu-id="950d2-246">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="950d2-247">Atualmente, o conjunto de dados de saída é quais unidades Olá agendamento, então você deve criar um conjunto de dados de saída, mesmo que a atividade de saudação não produz nenhuma saída.</span><span class="sxs-lookup"><span data-stu-id="950d2-247">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="950d2-248">Se a atividade de saudação não tem nenhuma entrada, você poderá ignorar o dataset de entrada hello criando.</span><span class="sxs-lookup"><span data-stu-id="950d2-248">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="950d2-249">Propriedades de saudação usadas em Olá JSON a seguir são explicadas no final desta seção hello.</span><span class="sxs-lookup"><span data-stu-id="950d2-249">hello properties used in hello following JSON are explained at hello end of this section.</span></span>

1. <span data-ttu-id="950d2-250">Crie um arquivo JSON chamado MyFirstPipelinePSH.json na pasta de C:\ADFGetStarted Olá com hello seguindo conteúdo:</span><span class="sxs-lookup"><span data-stu-id="950d2-250">Create a JSON file named MyFirstPipelinePSH.json in hello C:\ADFGetStarted folder with hello following content:</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="950d2-251">Substituir **storageaccountname** com o nome da saudação de sua conta de armazenamento Olá JSON.</span><span class="sxs-lookup"><span data-stu-id="950d2-251">Replace **storageaccountname** with hello name of your storage account in hello JSON.</span></span>
   >
   >

    ```json
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "StorageLinkedService",
                        "defines": {
                            "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                            "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                        }
                    },
                    "inputs": [
                        {
                            "name": "AzureBlobInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobOutput"
                        }
                    ],
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
                }
            ],
            "start": "2017-07-01T00:00:00Z",
            "end": "2017-07-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```
    <span data-ttu-id="950d2-252">No trecho JSON a saudação, você está criando um pipeline que consiste em uma única atividade que usa o Hive tooprocess dados em um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="950d2-252">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="950d2-253">arquivo de script do Hive Hello, **partitionweblogs.hql**, é armazenado no hello conta de armazenamento do Azure (especificado por scriptLinkedService hello, chamado **StorageLinkedService**) e, na **script**  pasta no contêiner Olá **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="950d2-253">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **StorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

    <span data-ttu-id="950d2-254">Olá **define** seção é configurações de tempo de execução do hello toospecify usado ser passado script do hive toohello como valores de configuração do Hive (por exemplo ${hiveconf: inputtable}, ${hiveconf:partitionedtable}).</span><span class="sxs-lookup"><span data-stu-id="950d2-254">hello **defines** section is used toospecify hello runtime settings that be passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="950d2-255">Olá **iniciar** e **final** propriedades do pipeline de saudação especifica o período ativo de saudação do pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="950d2-255">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

    <span data-ttu-id="950d2-256">Atividade Olá JSON, você especificar esse script de Hive Olá é executado em computação Olá especificada pelo Olá **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="950d2-256">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="950d2-257">Consulte "JSON de Pipeline" [Pipelines e atividades do Azure Data Factory](data-factory-create-pipelines.md) para obter detalhes sobre as propriedades JSON que são usados no exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="950d2-257">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties that are used in hello example.</span></span>

2. <span data-ttu-id="950d2-258">Confirme que você vê Olá **input.log** arquivo hello **adfgetstarted/inputdata** pasta Olá armazenamento de BLOBs do Azure e execução Olá pipeline de saudação do comando toodeploy a seguir.</span><span class="sxs-lookup"><span data-stu-id="950d2-258">Confirm that you see hello **input.log** file in hello **adfgetstarted/inputdata** folder in hello Azure blob storage, and run hello following command toodeploy hello pipeline.</span></span> <span data-ttu-id="950d2-259">Desde Olá **iniciar** e **final** horários são definidos no hello anterior e **isPaused** é conjunto toofalse, pipeline Olá execuções (atividade no pipeline de saudação) imediatamente após a implantação.</span><span class="sxs-lookup"><span data-stu-id="950d2-259">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryPipeline $df -File .\MyFirstPipelinePSH.json
    ```
3. <span data-ttu-id="950d2-260">Parabéns, você criou com sucesso seu primeiro pipeline usando o Azure PowerShell!</span><span class="sxs-lookup"><span data-stu-id="950d2-260">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="950d2-261">Monitorar o pipeline</span><span class="sxs-lookup"><span data-stu-id="950d2-261">Monitor pipeline</span></span>
<span data-ttu-id="950d2-262">Nesta etapa, você use toomonitor do PowerShell do Azure que está acontecendo em uma fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="950d2-262">In this step, you use Azure PowerShell toomonitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="950d2-263">Executar **Get-AzureRmDataFactory** e atribuir Olá saída tooa **$df** variável.</span><span class="sxs-lookup"><span data-stu-id="950d2-263">Run **Get-AzureRmDataFactory** and assign hello output tooa **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
2. <span data-ttu-id="950d2-264">Executar **Get-AzureRmDataFactorySlice** tooget detalhes sobre todas as fatias de saudação **EmpSQLTable**, que é a tabela de saída de saudação do pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="950d2-264">Run **Get-AzureRmDataFactorySlice** tooget details about all slices of hello **EmpSQLTable**, which is hello output table of hello pipeline.</span></span>

    ```PowerShell
    Get-AzureRmDataFactorySlice $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```
    <span data-ttu-id="950d2-265">Observe que Olá StartDateTime que você especificar aqui é hello que mesma hora de início especificada no pipeline de saudação JSON.</span><span class="sxs-lookup"><span data-stu-id="950d2-265">Notice that hello StartDateTime you specify here is hello same start time specified in hello pipeline JSON.</span></span> <span data-ttu-id="950d2-266">Aqui está a saída de exemplo hello:</span><span class="sxs-lookup"><span data-stu-id="950d2-266">Here is hello sample output:</span></span>

    ```PowerShell
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : FirstDataFactoryPSH
    DatasetName       : AzureBlobOutput
    Start             : 7/1/2017 12:00:00 AM
    End               : 7/2/2017 12:00:00 AM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. <span data-ttu-id="950d2-267">Executar **Get-AzureRmDataFactoryRun** tooget detalhes de saudação da atividade é executada para uma fatia específica.</span><span class="sxs-lookup"><span data-stu-id="950d2-267">Run **Get-AzureRmDataFactoryRun** tooget hello details of activity runs for a specific slice.</span></span>

    ```PowerShell
    Get-AzureRmDataFactoryRun $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```

    <span data-ttu-id="950d2-268">Aqui está a saída de exemplo hello:</span><span class="sxs-lookup"><span data-stu-id="950d2-268">Here is hello sample output:</span></span> 

    ```PowerShell
    Id                  : 0f6334f2-d56c-4d48-b427-d4f0fb4ef883_635268096000000000_635292288000000000_AzureBlobOutput
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : FirstDataFactoryPSH
    DatasetName         : AzureBlobOutput
    ProcessingStartTime : 12/18/2015 4:50:33 AM
    ProcessingEndTime   : 12/31/9999 11:59:59 PM
    PercentComplete     : 0
    DataSliceStart      : 7/1/2017 12:00:00 AM
    DataSliceEnd        : 7/2/2017 12:00:00 AM
    Status              : AllocatingResources
    Timestamp           : 12/18/2015 4:50:33 AM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : RunSampleHiveActivity
    PipelineName        : MyFirstPipeline
    Type                : Script
    ```
    <span data-ttu-id="950d2-269">Pode manter executar este cmdlet até que você veja fatia Olá **pronto** estado ou **falha** estado.</span><span class="sxs-lookup"><span data-stu-id="950d2-269">You can keep running this cmdlet until you see hello slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="950d2-270">Quando a fatia hello está no estado pronto, verificar Olá **partitioneddata** pasta Olá **adfgetstarted** dados de saída do contêiner em seu armazenamento de blob para hello.</span><span class="sxs-lookup"><span data-stu-id="950d2-270">When hello slice is in Ready state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  <span data-ttu-id="950d2-271">A criação de um cluster do HDInsight sob demanda geralmente leva algum tempo.</span><span class="sxs-lookup"><span data-stu-id="950d2-271">Creation of an on-demand HDInsight cluster usually takes some time.</span></span>

    ![dados de saída](./media/data-factory-build-your-first-pipeline-using-powershell/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="950d2-273">A criação de um cluster do HDInsight sob demanda geralmente leva algum tempo (20 minutos, aproximadamente).</span><span class="sxs-lookup"><span data-stu-id="950d2-273">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="950d2-274">Portanto, espere Olá pipeline tootake **aproximadamente 30 minutos** tooprocess Olá fatia.</span><span class="sxs-lookup"><span data-stu-id="950d2-274">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
>
> <span data-ttu-id="950d2-275">arquivo de entrada Hello é excluído quando a fatia de saudação é processada com êxito.</span><span class="sxs-lookup"><span data-stu-id="950d2-275">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="950d2-276">Portanto, se você deseja toorerun Olá fatia ou Olá tutorial novamente, pasta de carregamento Olá arquivo de entrada (input.log) toohello inputdata do contêiner de adfgetstarted hello.</span><span class="sxs-lookup"><span data-stu-id="950d2-276">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

## <a name="summary"></a><span data-ttu-id="950d2-277">Resumo</span><span class="sxs-lookup"><span data-stu-id="950d2-277">Summary</span></span>
<span data-ttu-id="950d2-278">Neste tutorial, você criou um tooprocess dados da fábrica de dados do Azure executando o script do Hive em um cluster de hadoop de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="950d2-278">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="950d2-279">Você usou Olá Editor da fábrica de dados em Olá toodo portal do Azure Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="950d2-279">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>

1. <span data-ttu-id="950d2-280">Foi criada uma **data factory**do Azure.</span><span class="sxs-lookup"><span data-stu-id="950d2-280">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="950d2-281">Foram criados dois **serviços vinculados**:</span><span class="sxs-lookup"><span data-stu-id="950d2-281">Created two **linked services**:</span></span>
   1. <span data-ttu-id="950d2-282">**Armazenamento do Azure** vinculado serviço toolink seu armazenamento de BLOBs do Azure que contém a fábrica de dados de toohello de arquivos de entrada/saída.</span><span class="sxs-lookup"><span data-stu-id="950d2-282">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="950d2-283">**HDInsight do Azure** toolink de serviço vinculado sob demanda uma fábrica de dados sob demanda HDInsight Hadoop cluster toohello.</span><span class="sxs-lookup"><span data-stu-id="950d2-283">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="950d2-284">A fábrica de dados do Azure cria um HDInsight Hadoop dados de entrada do cluster tooprocess just-in-time e produzir dados de saída.</span><span class="sxs-lookup"><span data-stu-id="950d2-284">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="950d2-285">Criados dois **conjuntos de dados**, que descrevem os dados de entrada e saídos para a atividade de Hive do HDInsight no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="950d2-285">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="950d2-286">Foi criado um **pipeline** com uma atividade **Hive do HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="950d2-286">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="950d2-287">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="950d2-287">Next steps</span></span>
<span data-ttu-id="950d2-288">Neste artigo, você criou um pipeline com uma atividade de transformação (atividade do HDInsight) que executa um script Hive em um cluster do HDInsight do Azure sob demanda.</span><span class="sxs-lookup"><span data-stu-id="950d2-288">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="950d2-289">toosee como toouse dados de toocopy uma atividade de cópia de um tooAzure de BLOBs do Azure SQL, consulte [Tutorial: copiar dados de um tooAzure de BLOBs do Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="950d2-289">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="950d2-290">Consulte também</span><span class="sxs-lookup"><span data-stu-id="950d2-290">See Also</span></span>
| <span data-ttu-id="950d2-291">Tópico</span><span class="sxs-lookup"><span data-stu-id="950d2-291">Topic</span></span> | <span data-ttu-id="950d2-292">Descrição</span><span class="sxs-lookup"><span data-stu-id="950d2-292">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="950d2-293">Referência de cmdlet do Data Factory</span><span class="sxs-lookup"><span data-stu-id="950d2-293">Data Factory Cmdlet Reference</span></span>](/powershell/module/azurerm.datafactories) |<span data-ttu-id="950d2-294">Consulte a documentação abrangente sobre os cmdlets do Data Factory</span><span class="sxs-lookup"><span data-stu-id="950d2-294">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="950d2-295">Pipelines</span><span class="sxs-lookup"><span data-stu-id="950d2-295">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="950d2-296">Este artigo ajuda você a entender os pipelines e atividades do Azure Data Factory e como toouse-los tooconstruct ponta a ponta controladas por dados fluxos de trabalho para seu cenário ou business.</span><span class="sxs-lookup"><span data-stu-id="950d2-296">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="950d2-297">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="950d2-297">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="950d2-298">Este artigo o ajuda a entender os conjuntos de dados no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="950d2-298">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="950d2-299">Planejamento e execução</span><span class="sxs-lookup"><span data-stu-id="950d2-299">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="950d2-300">Este artigo explica os aspectos de programação e a execução de saudação do modelo de aplicativo do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="950d2-300">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="950d2-301">Monitorar e gerenciar pipelines usando o Aplicativo de Monitoramento</span><span class="sxs-lookup"><span data-stu-id="950d2-301">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="950d2-302">Este artigo descreve como toomonitor, gerenciar e depurar pipelines usando Olá monitoramento e gerenciamento de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="950d2-302">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
