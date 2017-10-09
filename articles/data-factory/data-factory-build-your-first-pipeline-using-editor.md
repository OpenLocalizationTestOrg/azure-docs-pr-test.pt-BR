---
title: "aaaBuild sua primeira fábrica de dados (portal do Azure) | Microsoft Docs"
description: "Neste tutorial, você deve criar um pipeline do Azure Data Factory de exemplo usando o Editor de fábrica de dados em Olá portal do Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d5b14e9e-e358-45be-943c-5297435d402d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fc80776001b181a59c04d80d2e05c20b107a63f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-portal"></a><span data-ttu-id="c4e9e-103">Tutorial: Compilar sua primeira Azure Data Factory usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c4e9e-103">Tutorial: Build your first Azure data factory using Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c4e9e-104">Visão geral e pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c4e9e-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="c4e9e-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c4e9e-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="c4e9e-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c4e9e-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="c4e9e-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4e9e-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="c4e9e-108">Modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c4e9e-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="c4e9e-109">API REST</span><span class="sxs-lookup"><span data-stu-id="c4e9e-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)


<span data-ttu-id="c4e9e-110">Neste artigo, você aprenderá como toouse [portal do Azure](https://portal.azure.com/) toocreate sua primeira data factory do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-110">In this article, you learn how toouse [Azure portal](https://portal.azure.com/) toocreate your first Azure data factory.</span></span> <span data-ttu-id="c4e9e-111">tutorial de saudação toodo usando outras ferramentas/SDKs, selecione uma das opções de saudação da lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span> 

<span data-ttu-id="c4e9e-112">pipeline de saudação neste tutorial tem uma atividade: **atividade Hive do HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="c4e9e-113">Essa atividade executa um script do hive em um cluster de HDInsight do Azure que transforma dados de saída de tooproduce de entrada.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="c4e9e-114">pipeline de saudação é agendado toorun depois de um mês entre hello especificar horários de início e término.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="c4e9e-115">pipeline de dados Olá neste tutorial transforma dados de saída de tooproduce de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="c4e9e-116">Para obter um tutorial sobre como toocopy dados usando a fábrica de dados do Azure, consulte [Tutorial: copiar dados de armazenamento de Blob tooSQL banco de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c4e9e-116">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="c4e9e-117">Um pipeline pode ter mais de uma atividade.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="c4e9e-118">E, é possível encadear duas atividades (executadas uma atividade após o outro), definindo Olá o conjunto de dados de saída de uma atividade Olá outra atividade de conjunto de dados de saudação de entrada.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-118">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="c4e9e-119">Para saber mais, confira [Agendamento e execução no Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="c4e9e-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4e9e-120">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c4e9e-120">Prerequisites</span></span>
1. <span data-ttu-id="c4e9e-121">Leia [visão geral do Tutorial](data-factory-build-your-first-pipeline.md) artigo e hello completa **pré-requisito** etapas.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
2. <span data-ttu-id="c4e9e-122">Este artigo não fornece uma visão geral conceitual de saudação serviço do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-122">This article does not provide a conceptual overview of hello Azure Data Factory service.</span></span> <span data-ttu-id="c4e9e-123">É recomendável que você passe por [tooAzure Introdução Data Factory](data-factory-introduction.md) artigo para uma visão geral detalhada do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-123">We recommend that you go through [Introduction tooAzure Data Factory](data-factory-introduction.md) article for a detailed overview of hello service.</span></span>  

## <a name="create-data-factory"></a><span data-ttu-id="c4e9e-124">Criar um data factory</span><span class="sxs-lookup"><span data-stu-id="c4e9e-124">Create data factory</span></span>
<span data-ttu-id="c4e9e-125">Uma fábrica de dados pode ter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-125">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="c4e9e-126">Um pipeline em um data factory pode ter uma ou mais atividades.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-126">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="c4e9e-127">Por exemplo, dados de toocopy uma atividade de cópia de um repositório de dados de destino do código-fonte tooa e uma atividade de Hive do HDInsight toorun um tootransform de script do Hive dados de saída de tooproduct dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-127">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="c4e9e-128">Vamos começar com a criação de fábrica de dados Olá nesta etapa.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-128">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="c4e9e-129">Faça logon no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c4e9e-129">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c4e9e-130">Clique em **novo** no menu esquerdo Olá **dados + análise**e clique em **fábrica de dados**.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-130">Click **NEW** on hello left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>

   ![Folha Criar](./media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)
3. <span data-ttu-id="c4e9e-132">Em Olá **nova fábrica de dados** folha, digite **GetStartedDF** para Olá nome.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-132">In hello **New data factory** blade, enter **GetStartedDF** for hello Name.</span></span>

   ![Folha Nova data factory](./media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > <span data-ttu-id="c4e9e-134">nome de saudação do hello data factory do Azure deve ser **globalmente exclusivo**.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-134">hello name of hello Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="c4e9e-135">Se você receber o erro Olá: **"GetStartedDF" nome da fábrica de dados não está disponível**.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-135">If you receive hello error: **Data factory name “GetStartedDF” is not available**.</span></span> <span data-ttu-id="c4e9e-136">Alterar nome Olá Olá da fábrica de dados (por exemplo, yournameGetStartedDF) e tente criar novamente.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-136">Change hello name of hello data factory (for example, yournameGetStartedDF) and try creating again.</span></span> <span data-ttu-id="c4e9e-137">Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-137">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
   >
   > <span data-ttu-id="c4e9e-138">nome de Olá Olá da fábrica de dados pode ser registrado como um **DNS** nome no futuro hello e, portanto, se tornarão visíveis publicamente.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-138">hello name of hello data factory may be registered as a **DNS** name in hello future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="c4e9e-139">Selecione Olá **assinatura do Azure** onde você deseja Olá toobe de fábrica de dados criado.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-139">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="c4e9e-140">Selecione um **grupo de recursos** existente ou crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-140">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="c4e9e-141">Tutorial de hello, crie um grupo de recursos chamado: **ADFGetStartedRG**.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-141">For hello tutorial, create a resource group named: **ADFGetStartedRG**.</span></span>
6. <span data-ttu-id="c4e9e-142">Selecione Olá **local** Olá fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-142">Select hello **location** for hello data factory.</span></span> <span data-ttu-id="c4e9e-143">Somente regiões Olá serviço da fábrica de dados com suporte são mostrados na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-143">Only regions supported by hello Data Factory service are shown in hello drop-down list.</span></span>
7. <span data-ttu-id="c4e9e-144">Selecione **toodashboard Pin**.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-144">Select **Pin toodashboard**.</span></span> 
8. <span data-ttu-id="c4e9e-145">Clique em **criar** em Olá **nova fábrica de dados** folha.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-145">Click **Create** on hello **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="c4e9e-146">toocreate instâncias de fábrica de dados, você deve ser um membro da saudação [colaborador da fábrica de dados](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) função no nível do grupo de recursos de assinatura/hello.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-146">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="c4e9e-147">No painel hello, você vê Olá seguinte lado a lado com o status: Implantando fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-147">On hello dashboard, you see hello following tile with status: Deploying data factory.</span></span>    

   ![Status da criação da data factory](./media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)
8. <span data-ttu-id="c4e9e-149">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="c4e9e-149">Congratulations!</span></span> <span data-ttu-id="c4e9e-150">Você criou com êxito sua primeira data factory.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-150">You have successfully created your first data factory.</span></span> <span data-ttu-id="c4e9e-151">Depois de fábrica de dados Olá tiver sido criada com êxito, você ver a página de fábrica de dados hello, que mostra Olá conteúdo Olá da fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-151">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>     

    ![Folha Data Factory](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

<span data-ttu-id="c4e9e-153">Antes de criar um pipeline na fábrica de dados Olá, é necessário toocreate algumas entidades da fábrica de dados pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-153">Before creating a pipeline in hello data factory, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="c4e9e-154">Você primeiro criar dados de toolink serviços vinculados repositórios/calcula tooyour dados armazenam, definem a entrada e saída de dados de entrada/saída toorepresent conjuntos de dados em repositórios de dados vinculados e, em seguida, criar o pipeline de saudação com uma atividade que usa esses conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-154">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent input/output data in linked data stores, and then create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="c4e9e-155">Criar serviços vinculados</span><span class="sxs-lookup"><span data-stu-id="c4e9e-155">Create linked services</span></span>
<span data-ttu-id="c4e9e-156">Nesta etapa, você pode vincular sua conta de armazenamento do Azure e uma fábrica de dados sob demanda do Azure HDInsight cluster tooyour.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-156">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="c4e9e-157">Olá conta de armazenamento do Azure mantém Olá dados de entrada e saídos para o pipeline de saudação neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-157">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="c4e9e-158">Olá serviço vinculado do HDInsight é toorun usado um script de Hive especificado na atividade de saudação do pipeline de saudação neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-158">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span> <span data-ttu-id="c4e9e-159">Identificar o que [repositório de dados](data-factory-data-movement-activities.md)/[serviços de computação](data-factory-compute-linked-services.md) são usados em seu cenário e vincular a fábrica de dados desses serviços toohello criando serviços vinculados.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-159">Identify what [data store](data-factory-data-movement-activities.md)/[compute services](data-factory-compute-linked-services.md) are used in your scenario and link those services toohello data factory by creating linked services.</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="c4e9e-160">Criar o serviço vinculado do armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="c4e9e-160">Create Azure Storage linked service</span></span>
<span data-ttu-id="c4e9e-161">Nesta etapa, você vincular sua fábrica de dados de tooyour de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-161">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="c4e9e-162">Neste tutorial, você use Olá mesma conta de armazenamento do Azure, dados de entrada/saída toostore e hello HQL arquivo de script.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-162">In this tutorial, you use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="c4e9e-163">Clique em **autor e implantar** em Olá **DATA FACTORY** folha para **GetStartedDF**.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-163">Click **Author and deploy** on hello **DATA FACTORY** blade for **GetStartedDF**.</span></span> <span data-ttu-id="c4e9e-164">Você deve ver Olá Editor da fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-164">You should see hello Data Factory Editor.</span></span>

   ![Bloco Criar e implantar](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)
2. <span data-ttu-id="c4e9e-166">Clique em **Novo repositório de dados** e escolha **Armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-166">Click **New data store** and choose **Azure storage**.</span></span>

   ![Novo armazenamento de dados - Armazenamento do Azure - menu](./media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="c4e9e-168">Você deve ver Olá script JSON para a criação de um armazenamento do Azure vinculada serviço no editor de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-168">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>

   ![Serviço vinculado de armazenamento do Azure](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="c4e9e-170">Substituir **nome da conta** com nome de saudação da sua conta de armazenamento do Azure e **chave de conta** com a chave de acesso de saudação do Olá conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-170">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="c4e9e-171">toolearn como tooget acessar o armazenamento de chave, consulte Olá informações sobre como tooview, copiar e armazenamento regenerar chaves de acesso em [gerenciar sua conta de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="c4e9e-171">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="c4e9e-172">Clique em **implantar** no comando Olá barra toodeploy Olá vinculado serviço.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-172">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

    ![Botão Implantar](./media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   <span data-ttu-id="c4e9e-174">Depois de hello serviço vinculado foi implantado com êxito, Olá **rascunho 1** janela desaparecerá e você verá **AzureStorageLinkedService** na exibição de árvore Olá Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-174">After hello linked service is deployed successfully, hello **Draft-1** window should disappear and you see **AzureStorageLinkedService** in hello tree view on hello left.</span></span>

    ![Serviço Vinculado de Armazenamento no menu](./media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="c4e9e-176">Criar o serviço vinculado do Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c4e9e-176">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="c4e9e-177">Nesta etapa, você vincular uma fábrica de dados sob demanda HDInsight cluster tooyour.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-177">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="c4e9e-178">cluster do HDInsight Olá é criado em tempo de execução e excluído após a conclusão ocioso e processamento para o período de tempo especificado Olá automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-178">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span>

1. <span data-ttu-id="c4e9e-179">Em Olá **Editor da fábrica de dados**, clique em **... Mais**, clique em **Nova computação** e selecione **Cluster HDInsight sob demanda**.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-179">In hello **Data Factory Editor**, click **... More**, click **New compute**, and select **On-demand HDInsight cluster**.</span></span>

    ![Nova computação](./media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)
2. <span data-ttu-id="c4e9e-181">Copie e cole Olá toohello de trecho de código a seguir **rascunho 1** janela.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-181">Copy and paste hello following snippet toohello **Draft-1** window.</span></span> <span data-ttu-id="c4e9e-182">trecho JSON a saudação descreve propriedades Olá Olá toocreate usado cluster de HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-182">hello JSON snippet describes hello properties that are used toocreate hello HDInsight cluster on-demand.</span></span>

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

    <span data-ttu-id="c4e9e-183">Olá, tabela a seguir fornece descrições para propriedades JSON Olá usadas no trecho hello:</span><span class="sxs-lookup"><span data-stu-id="c4e9e-183">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="c4e9e-184">Propriedade</span><span class="sxs-lookup"><span data-stu-id="c4e9e-184">Property</span></span> | <span data-ttu-id="c4e9e-185">Descrição</span><span class="sxs-lookup"><span data-stu-id="c4e9e-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="c4e9e-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="c4e9e-186">ClusterSize</span></span> |<span data-ttu-id="c4e9e-187">Especifica o tamanho de saudação do cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-187">Specifies hello size of hello HDInsight cluster.</span></span> |
   | <span data-ttu-id="c4e9e-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="c4e9e-188">TimeToLive</span></span> | <span data-ttu-id="c4e9e-189">Especifica que Olá de tempo ocioso para um cluster do HDInsight hello, antes de ser excluído.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-189">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="c4e9e-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="c4e9e-190">linkedServiceName</span></span> | <span data-ttu-id="c4e9e-191">Especifica a conta de armazenamento de saudação que é usado toostore logs de Olá gerados pelo HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-191">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight.</span></span> |

    <span data-ttu-id="c4e9e-192">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4e9e-192">Note hello following points:</span></span>

   * <span data-ttu-id="c4e9e-193">Olá fábrica de dados cria um **baseados em Linux** cluster HDInsight para você com hello JSON.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-193">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello JSON.</span></span> <span data-ttu-id="c4e9e-194">Confira [Serviço vinculado do HDInsight sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="c4e9e-195">Você pode usar **seu próprio cluster do HDInsight** em vez de usar um cluster do HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="c4e9e-196">Confira [Serviço vinculado do HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="c4e9e-197">Olá HDInsight cluster cria um **contêiner padrão** no armazenamento de blob Olá especificado no hello JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="c4e9e-197">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="c4e9e-198">HDInsight não exclui esse contêiner quando Olá cluster é excluído.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-198">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="c4e9e-199">Este comportamento ocorre por design.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-199">This behavior is by design.</span></span> <span data-ttu-id="c4e9e-200">Com o serviço vinculado HDInsight sob demanda, um cluster HDInsight é criado sempre que uma fatia é processada, a menos que haja um cluster ativo existente (**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="c4e9e-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="c4e9e-201">cluster de saudação é excluído automaticamente quando Olá processamento é concluído.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-201">hello cluster is automatically deleted when hello processing is done.</span></span>

       <span data-ttu-id="c4e9e-202">Quanto mais fatias forem processadas, você verá muitos contêineres no armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="c4e9e-203">Se não precisar para solução de problemas de trabalhos de saudação, talvez você queira toodelete-os custos de armazenamento do tooreduce hello.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-203">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="c4e9e-204">nomes de saudação desses contêineres seguem um padrão: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="c4e9e-204">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="c4e9e-205">Use ferramentas como [Gerenciador de armazenamento do Microsoft](http://storageexplorer.com/) armazenamento de blobs de contêineres toodelete do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="c4e9e-206">Confira [Serviço vinculado do HDInsight sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
3. <span data-ttu-id="c4e9e-207">Clique em **implantar** no comando Olá barra toodeploy Olá vinculado serviço.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-207">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

    ![Implantar o serviço vinculado do HDInsight sob demanda](./media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)
4. <span data-ttu-id="c4e9e-209">Confirme que você vê ambos **AzureStorageLinkedService** e **HDInsightOnDemandLinkedService** na exibição de árvore Olá Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-209">Confirm that you see both **AzureStorageLinkedService** and **HDInsightOnDemandLinkedService** in hello tree view on hello left.</span></span>

    ![Modo de exibição de árvore com serviços vinculados](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a><span data-ttu-id="c4e9e-211">Criar conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="c4e9e-211">Create datasets</span></span>
<span data-ttu-id="c4e9e-212">Nesta etapa, você cria conjuntos de dados toorepresent Olá entrada e saída de dados para o processamento do Hive.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-212">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="c4e9e-213">Esses conjuntos de dados Consulte toohello **AzureStorageLinkedService** você tiver criado anteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-213">These datasets refer toohello **AzureStorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="c4e9e-214">Olá tooan de pontos de serviço vinculado conta de armazenamento do Azure e conjuntos de dados especificam contêiner, pasta, nome do arquivo no armazenamento de saudação que contém a entrada e saída de dados.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-214">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>   

### <a name="create-input-dataset"></a><span data-ttu-id="c4e9e-215">Criar conjunto de dados de entrada</span><span class="sxs-lookup"><span data-stu-id="c4e9e-215">Create input dataset</span></span>
1. <span data-ttu-id="c4e9e-216">Em Olá **Editor da fábrica de dados**, clique em **... Mais** na barra de comandos de saudação, clique em **novo conjunto de dados**e selecione **armazenamento de BLOBs do Azure**.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-216">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>

    ![Novo conjunto de dados](./media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)
2. <span data-ttu-id="c4e9e-218">Copie e cole Olá janela toohello rascunho-1 de trecho de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-218">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="c4e9e-219">No trecho JSON a saudação, você está criando um conjunto de dados chamado **AzureBlobInput** que representa dados de entrada de uma atividade no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-219">In hello JSON snippet, you are creating a dataset called **AzureBlobInput** that represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="c4e9e-220">Além disso, você especificar que os dados de entrada hello estão localizados no contêiner de blob Olá chamado **adfgetstarted** e Olá pasta chamada **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-220">In addition, you specify that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

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
    <span data-ttu-id="c4e9e-221">Olá, tabela a seguir fornece descrições para propriedades JSON Olá usadas no trecho hello:</span><span class="sxs-lookup"><span data-stu-id="c4e9e-221">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="c4e9e-222">Propriedade</span><span class="sxs-lookup"><span data-stu-id="c4e9e-222">Property</span></span> | <span data-ttu-id="c4e9e-223">Descrição</span><span class="sxs-lookup"><span data-stu-id="c4e9e-223">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="c4e9e-224">type</span><span class="sxs-lookup"><span data-stu-id="c4e9e-224">type</span></span> |<span data-ttu-id="c4e9e-225">propriedade do tipo Hello está definida muito**AzureBlob** porque os dados residem em um armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-225">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
   | <span data-ttu-id="c4e9e-226">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="c4e9e-226">linkedServiceName</span></span> |<span data-ttu-id="c4e9e-227">Refere-se toohello **AzureStorageLinkedService** criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-227">Refers toohello **AzureStorageLinkedService** you created earlier.</span></span> |
   | <span data-ttu-id="c4e9e-228">folderPath</span><span class="sxs-lookup"><span data-stu-id="c4e9e-228">folderPath</span></span> | <span data-ttu-id="c4e9e-229">Especifica o blob Olá **contêiner** e hello **pasta** que contém blobs de entrada.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-229">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> | 
   | <span data-ttu-id="c4e9e-230">fileName</span><span class="sxs-lookup"><span data-stu-id="c4e9e-230">fileName</span></span> |<span data-ttu-id="c4e9e-231">Essa propriedade é opcional.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-231">This property is optional.</span></span> <span data-ttu-id="c4e9e-232">Se você omitir essa propriedade, todos os arquivos de saudação do hello folderPath são escolhidos.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-232">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="c4e9e-233">Neste tutorial, apenas Olá **input.log** é processado.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-233">In this tutorial, only hello **input.log** is processed.</span></span> |
   | <span data-ttu-id="c4e9e-234">type</span><span class="sxs-lookup"><span data-stu-id="c4e9e-234">type</span></span> |<span data-ttu-id="c4e9e-235">arquivos de log de saudação estão no formato de texto, para que possamos usar **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-235">hello log files are in text format, so we use **TextFormat**.</span></span> |
   | <span data-ttu-id="c4e9e-236">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="c4e9e-236">columnDelimiter</span></span> |<span data-ttu-id="c4e9e-237">as colunas nos arquivos de log de saudação são delimitadas por **caractere de vírgula (`,`)**</span><span class="sxs-lookup"><span data-stu-id="c4e9e-237">columns in hello log files are delimited by **comma character (`,`)**</span></span> |
   | <span data-ttu-id="c4e9e-238">frequência/intervalo</span><span class="sxs-lookup"><span data-stu-id="c4e9e-238">frequency/interval</span></span> |<span data-ttu-id="c4e9e-239">frequência definida muito**mês** e o intervalo é **1**, que significa que Olá fatias estão disponíveis mensal de entrada.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-239">frequency set too**Month** and interval is **1**, which means that hello input slices are available monthly.</span></span> |
   | <span data-ttu-id="c4e9e-240">externo</span><span class="sxs-lookup"><span data-stu-id="c4e9e-240">external</span></span> | <span data-ttu-id="c4e9e-241">Essa propriedade é definida, muito**true** se os dados de entrada hello não foi gerados por este pipeline.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-241">This property is set too**true** if hello input data is not generated by this pipeline.</span></span> <span data-ttu-id="c4e9e-242">Neste tutorial, o arquivo de input.log de saudação não é gerado por este pipeline para definimos Olá tootrue de propriedade.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-242">In this tutorial, hello input.log file is not generated by this pipeline, so we set hello property tootrue.</span></span> |

    <span data-ttu-id="c4e9e-243">Para saber mais sobre essas propriedades JSON, confira o [artigo sobre o conector do Blob do Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c4e9e-243">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="c4e9e-244">Clique em **implantar** no comando Olá barra toodeploy Olá recém-criado dataset.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-244">Click **Deploy** on hello command bar toodeploy hello newly created dataset.</span></span> <span data-ttu-id="c4e9e-245">Você deve ver a saudação de conjunto de dados na exibição de árvore Olá Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-245">You should see hello dataset in hello tree view on hello left.</span></span>

### <a name="create-output-dataset"></a><span data-ttu-id="c4e9e-246">Criar conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="c4e9e-246">Create output dataset</span></span>
<span data-ttu-id="c4e9e-247">Agora, você pode criar hello saída dataset toorepresent Olá saída dados armazenados em Olá armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-247">Now, you create hello output dataset toorepresent hello output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="c4e9e-248">Em Olá **Editor da fábrica de dados**, clique em **... Mais** na barra de comandos de saudação, clique em **novo conjunto de dados**e selecione **armazenamento de BLOBs do Azure**.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-248">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="c4e9e-249">Copie e cole Olá janela toohello rascunho-1 de trecho de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-249">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="c4e9e-250">No trecho JSON a saudação, você está criando um conjunto de dados chamado **AzureBlobOutput**e especificar a estrutura de saudação de dados de saudação que são produzidos pelo script do Hive hello.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-250">In hello JSON snippet, you are creating a dataset called **AzureBlobOutput**, and specifying hello structure of hello data that is produced by hello Hive script.</span></span> <span data-ttu-id="c4e9e-251">Além disso, você especificar que os resultados de hello são armazenados no contêiner de blob Olá chamado **adfgetstarted** e Olá pasta chamada **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-251">In addition, you specify that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="c4e9e-252">Olá **disponibilidade** seção especifica esse conjunto de dados de saída de saudação é produzido por mês.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-252">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>

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
    <span data-ttu-id="c4e9e-253">Consulte **criar conjunto de dados de entrada hello** seção para obter descrições dessas propriedades.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-253">See **Create hello input dataset** section for descriptions of these properties.</span></span> <span data-ttu-id="c4e9e-254">Você não definir propriedade externa Olá em um conjunto de dados de saída como Olá dataset é produzido pelo serviço da fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-254">You do not set hello external property on an output dataset as hello dataset is produced by hello Data Factory service.</span></span>
3. <span data-ttu-id="c4e9e-255">Clique em **implantar** no comando Olá barra toodeploy Olá recém-criado dataset.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-255">Click **Deploy** on hello command bar toodeploy hello newly created dataset.</span></span>
4. <span data-ttu-id="c4e9e-256">Verifique se o que conjunto de dados Olá é criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-256">Verify that hello dataset is created successfully.</span></span>

    ![Modo de exibição de árvore com serviços vinculados](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-pipeline"></a><span data-ttu-id="c4e9e-258">Criar um pipeline</span><span class="sxs-lookup"><span data-stu-id="c4e9e-258">Create pipeline</span></span>
<span data-ttu-id="c4e9e-259">Nesta etapa, você cria seu primeiro pipeline com a atividade **HDInsightHive** .</span><span class="sxs-lookup"><span data-stu-id="c4e9e-259">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="c4e9e-260">Entrada fatia está disponível mensal (frequência: mês, intervalo: 1), fatias de saída é produzida mensal e Olá Agendador para a atividade de saudação é também definida toomonthly.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-260">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="c4e9e-261">Olá configurações para o conjunto de dados de saída de hello e Agendador de atividade de saudação devem corresponder.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-261">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="c4e9e-262">Atualmente, o conjunto de dados de saída é quais unidades Olá agendamento, então você deve criar um conjunto de dados de saída, mesmo que a atividade de saudação não produz nenhuma saída.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-262">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="c4e9e-263">Se a atividade de saudação não tem nenhuma entrada, você poderá ignorar o dataset de entrada hello criando.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-263">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="c4e9e-264">Propriedades de saudação usadas em Olá JSON a seguir são explicadas no final desta seção hello.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-264">hello properties used in hello following JSON are explained at hello end of this section.</span></span>

1. <span data-ttu-id="c4e9e-265">Em Olá **Editor da fábrica de dados**, clique em **reticências (...) Comandos mais** e, em seguida, clique em **novo pipeline**.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-265">In hello **Data Factory Editor**, click **Ellipsis (…) More commands** and then click **New pipeline**.</span></span>

    ![botão novo pipeline](./media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)
2. <span data-ttu-id="c4e9e-267">Copie e cole Olá janela toohello rascunho-1 de trecho de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-267">Copy and paste hello following snippet toohello Draft-1 window.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="c4e9e-268">Substituir **storageaccountname** com o nome da saudação de sua conta de armazenamento Olá JSON.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-268">Replace **storageaccountname** with hello name of your storage account in hello JSON.</span></span>
   >
   >

    ```JSON
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService",
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

    <span data-ttu-id="c4e9e-269">No trecho JSON a saudação, você está criando um pipeline que consiste em uma única atividade que usa o Hive tooprocess dados em um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-269">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="c4e9e-270">arquivo de script do Hive Hello, **partitionweblogs.hql**, é armazenado no hello conta de armazenamento do Azure (especificado por scriptLinkedService hello, chamado **AzureStorageLinkedService**) e em  **script** pasta no contêiner Olá **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-270">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

    <span data-ttu-id="c4e9e-271">Olá **define** seção é toospecify usadas configurações de tempo de execução de saudação que são passadas script do hive toohello como valores de configuração do Hive (por exemplo ${hiveconf: inputtable}, ${hiveconf:partitionedtable}).</span><span class="sxs-lookup"><span data-stu-id="c4e9e-271">hello **defines** section is used toospecify hello runtime settings that are passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="c4e9e-272">Olá **iniciar** e **final** propriedades do pipeline de saudação especifica o período ativo de saudação do pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-272">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

    <span data-ttu-id="c4e9e-273">Atividade Olá JSON, você especificar esse script de Hive Olá é executado em computação Olá especificada pelo Olá **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-273">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c4e9e-274">Consulte "JSON de Pipeline" [Pipelines e atividades do Azure Data Factory](data-factory-create-pipelines.md) para obter detalhes sobre as propriedades JSON usados no exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-274">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in hello example.</span></span>
   >
   >
3. <span data-ttu-id="c4e9e-275">Confirme a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="c4e9e-275">Confirm hello following:</span></span>

   1. <span data-ttu-id="c4e9e-276">**Input.log** arquivo existe no hello **inputdata** pasta da saudação **adfgetstarted** contêiner no hello armazenamento de BLOBs do Azure</span><span class="sxs-lookup"><span data-stu-id="c4e9e-276">**input.log** file exists in hello **inputdata** folder of hello **adfgetstarted** container in hello Azure blob storage</span></span>
   2. <span data-ttu-id="c4e9e-277">**partitionweblogs.HQL** arquivo existe no hello **script** pasta da saudação **adfgetstarted** contêiner no hello armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-277">**partitionweblogs.hql** file exists in hello **script** folder of hello **adfgetstarted** container in hello Azure blob storage.</span></span> <span data-ttu-id="c4e9e-278">Etapas de pré-requisito concluída Olá no hello [visão geral do Tutorial](data-factory-build-your-first-pipeline.md) se você não vir esses arquivos.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-278">Complete hello prerequisite steps in hello [Tutorial Overview](data-factory-build-your-first-pipeline.md) if you don't see these files.</span></span>
   3. <span data-ttu-id="c4e9e-279">Confirme que você substituiu **storageaccountname** com o nome da saudação de sua conta de armazenamento Olá JSON de pipeline.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-279">Confirm that you replaced **storageaccountname** with hello name of your storage account in hello pipeline JSON.</span></span>
4. <span data-ttu-id="c4e9e-280">Clique em **implantar** no pipeline de saudação toodeploy da barra de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-280">Click **Deploy** on hello command bar toodeploy hello pipeline.</span></span> <span data-ttu-id="c4e9e-281">Desde Olá **iniciar** e **final** horários são definidos no hello anterior e **isPaused** é conjunto toofalse, pipeline Olá execuções (atividade no pipeline de saudação) imediatamente após a implantação.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-281">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>
5. <span data-ttu-id="c4e9e-282">Confirme que você vê pipeline Olá Olá na exibição em árvore.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-282">Confirm that you see hello pipeline in hello tree view.</span></span>

    ![Modo de exibição de árvore com pipeline](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)
6. <span data-ttu-id="c4e9e-284">Parabéns, você criou com sucesso seu primeiro pipeline!</span><span class="sxs-lookup"><span data-stu-id="c4e9e-284">Congratulations, you have successfully created your first pipeline!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="c4e9e-285">Monitorar o pipeline</span><span class="sxs-lookup"><span data-stu-id="c4e9e-285">Monitor pipeline</span></span>
### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="c4e9e-286">Monitorar o pipeline usando a Exibição de Diagrama</span><span class="sxs-lookup"><span data-stu-id="c4e9e-286">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="c4e9e-287">Clique em **X** tooclose Editor da fábrica de dados folhas toonavigate fazer toohello folha de fábrica de dados e clique em **diagrama**.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-287">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory blade, and click **Diagram**.</span></span>

    ![Bloco do diagrama](./media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)
2. <span data-ttu-id="c4e9e-289">Saudação de exibição de diagrama, você verá uma visão geral dos pipelines hello e conjuntos de dados usados neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-289">In hello Diagram View, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>

    ![Exibição de diagrama](./media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)
3. <span data-ttu-id="c4e9e-291">tooview todas as atividades no pipeline hello, pipeline com o botão direito no hello diagrama e clique em Abrir Pipeline.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-291">tooview all activities in hello pipeline, right-click pipeline in hello diagram and click Open Pipeline.</span></span>

    ![Menu do pipeline aberto](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)
4. <span data-ttu-id="c4e9e-293">Confirme que você ver a atividade de HDInsightHive Olá no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-293">Confirm that you see hello HDInsightHive activity in hello pipeline.</span></span>

    ![Abrir a exibição do pipeline](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    <span data-ttu-id="c4e9e-295">toonavigate fazer toohello modo de exibição anterior, clique em **fábrica de dados** no menu de navegação estrutural Olá na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-295">toonavigate back toohello previous view, click **Data factory** in hello breadcrumb menu at hello top.</span></span>
5. <span data-ttu-id="c4e9e-296">Em Olá **exibição de diagrama**, clique duas vezes no conjunto de dados Olá **AzureBlobInput**.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-296">In hello **Diagram View**, double-click hello dataset **AzureBlobInput**.</span></span> <span data-ttu-id="c4e9e-297">Confirmar essa fatia hello está **pronto** estado.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-297">Confirm that hello slice is in **Ready** state.</span></span> <span data-ttu-id="c4e9e-298">Pode levar alguns minutos para Olá fatia tooshow até em estado pronto.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-298">It may take a couple of minutes for hello slice tooshow up in Ready state.</span></span> <span data-ttu-id="c4e9e-299">Se isso não acontece depois que você aguarde algum tempo, ver se há Olá arquivo de entrada (input.log) colocado no contêiner de saudação à direita (adfgetstarted) e na pasta (inputdata).</span><span class="sxs-lookup"><span data-stu-id="c4e9e-299">If it does not happen after you wait for sometime, see if you have hello input file (input.log) placed in hello right container (adfgetstarted) and folder (inputdata).</span></span>

   ![Fatia de entrada no estado pronto](./media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)
6. <span data-ttu-id="c4e9e-301">Clique em **X** tooclose **AzureBlobInput** folha.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-301">Click **X** tooclose **AzureBlobInput** blade.</span></span>
7. <span data-ttu-id="c4e9e-302">Em Olá **exibição de diagrama**, clique duas vezes no conjunto de dados Olá **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-302">In hello **Diagram View**, double-click hello dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="c4e9e-303">Você verá essa fatia Olá que está sendo processada atualmente.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-303">You see that hello slice that is currently being processed.</span></span>

   ![Conjunto de dados](./media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)
8. <span data-ttu-id="c4e9e-305">Quando o processamento é concluído, você verá fatia Olá **pronto** estado.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-305">When processing is done, you see hello slice in **Ready** state.</span></span>

   ![Conjunto de dados](./media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > <span data-ttu-id="c4e9e-307">A criação de um cluster do HDInsight sob demanda geralmente leva algum tempo (20 minutos, aproximadamente).</span><span class="sxs-lookup"><span data-stu-id="c4e9e-307">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="c4e9e-308">Portanto, espere pipeline Olá levar muito **aproximadamente 30 minutos** tooprocess Olá fatia.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-308">Therefore, expect hello pipeline too      take **approximately 30 minutes** tooprocess hello slice.</span></span>
   >
   >

9. <span data-ttu-id="c4e9e-309">Quando a fatia hello está em **pronto** de estado, verifique Olá **partitioneddata** pasta Olá **adfgetstarted** contêiner no seu armazenamento de blob para Olá dados de saída.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-309">When hello slice is in **Ready** state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  

   ![dados de saída](./media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)
10. <span data-ttu-id="c4e9e-311">Clique em Olá fatia toosee detalhes sobre ele em um **fatia de dados** folha.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-311">Click hello slice toosee details about it in a **Data slice** blade.</span></span>

   ![Detalhes da fatia de dados](./media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)  
11. <span data-ttu-id="c4e9e-313">Clique em uma saudação de execução da atividade **atividade é executada a lista** toosee detalhes sobre uma atividade de execução (atividade de Hive em nosso cenário) um **detalhes da execução de atividade** janela.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-313">Click an activity run in hello **Activity runs list** toosee details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span></span>   

   ![Detalhes da execução da atividade](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   <span data-ttu-id="c4e9e-315">Olá dos arquivos de log, você pode ver informações de status e de consulta de Hive Olá que foi executada.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-315">From hello log files, you can see hello Hive query that was executed and status information.</span></span> <span data-ttu-id="c4e9e-316">Esses logs são úteis para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-316">These logs are useful for troubleshooting any issues.</span></span>
   <span data-ttu-id="c4e9e-317">Confira o artigo [Monitorar e gerenciar pipelines usando as folhas do portal do Azure](data-factory-monitor-manage-pipelines.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-317">See [Monitor and manage pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) article for more details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c4e9e-318">arquivo de entrada Hello é excluído quando a fatia de saudação é processada com êxito.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-318">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="c4e9e-319">Portanto, se você deseja toorerun Olá fatia ou Olá tutorial novamente, pasta de carregamento Olá arquivo de entrada (input.log) toohello inputdata do contêiner de adfgetstarted hello.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-319">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="c4e9e-320">Monitorar o pipeline usando o aplicativo Monitorar e Gerenciar</span><span class="sxs-lookup"><span data-stu-id="c4e9e-320">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="c4e9e-321">Você também pode usar o Monitor de & Gerenciar aplicativo toomonitor seus pipelines.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-321">You can also use Monitor & Manage application toomonitor your pipelines.</span></span> <span data-ttu-id="c4e9e-322">Para obter informações detalhadas sobre como usar esse aplicativo, confira [Monitorar e gerenciar pipelines do Azure Data Factory usando o aplicativo Monitorar e Gerenciar](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="c4e9e-322">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="c4e9e-323">Clique em **monitorar e gerenciar** lado a lado na página inicial do hello sua fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-323">Click **Monitor & Manage** tile on hello home page for your data factory.</span></span>

    ![Bloco Monitorar e Gerenciar](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)
2. <span data-ttu-id="c4e9e-325">Você deve ver **Monitorar e Gerenciar aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-325">You should see **Monitor & Manage application**.</span></span> <span data-ttu-id="c4e9e-326">Saudação de alteração **hora de início** e **hora de término** toomatch início e término do pipeline e clique em **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-326">Change hello **Start time** and **End time** toomatch start and end times of your pipeline, and click **Apply**.</span></span>

    ![Aplicativo Monitorar e Gerenciar](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)
3. <span data-ttu-id="c4e9e-328">Selecione uma janela de atividade no hello **atividade Windows** lista toosee detalhes sobre ele.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-328">Select an activity window in hello **Activity Windows** list toosee details about it.</span></span>

    ![Detalhes da janela Atividade](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

## <a name="summary"></a><span data-ttu-id="c4e9e-330">Resumo</span><span class="sxs-lookup"><span data-stu-id="c4e9e-330">Summary</span></span>
<span data-ttu-id="c4e9e-331">Neste tutorial, você criou um tooprocess dados da fábrica de dados do Azure executando o script do Hive em um cluster de hadoop de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-331">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="c4e9e-332">Você usou Olá Editor da fábrica de dados em Olá toodo portal do Azure Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4e9e-332">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>  

1. <span data-ttu-id="c4e9e-333">Foi criada uma **data factory**do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-333">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="c4e9e-334">Foram criados dois **serviços vinculados**:</span><span class="sxs-lookup"><span data-stu-id="c4e9e-334">Created two **linked services**:</span></span>
   1. <span data-ttu-id="c4e9e-335">**Armazenamento do Azure** vinculado serviço toolink seu armazenamento de BLOBs do Azure que contém a fábrica de dados de toohello de arquivos de entrada/saída.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-335">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="c4e9e-336">**HDInsight do Azure** toolink de serviço vinculado sob demanda uma fábrica de dados sob demanda HDInsight Hadoop cluster toohello.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-336">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="c4e9e-337">A fábrica de dados do Azure cria um HDInsight Hadoop dados de entrada do cluster tooprocess just-in-time e produzir dados de saída.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-337">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="c4e9e-338">Criados dois **conjuntos de dados**, que descrevem os dados de entrada e saídos para a atividade de Hive do HDInsight no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-338">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="c4e9e-339">Foi criado um **pipeline** com uma atividade **Hive do HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-339">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4e9e-340">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c4e9e-340">Next Steps</span></span>
<span data-ttu-id="c4e9e-341">Neste artigo, você criou um pipeline com uma atividade de transformação (atividade do HDInsight) que executa um script Hive em um cluster do HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-341">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="c4e9e-342">toosee como toouse dados de toocopy uma atividade de cópia de um tooAzure de BLOBs do Azure SQL, consulte [Tutorial: copiar dados de um tooAzure de BLOBs do Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c4e9e-342">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="c4e9e-343">Consulte também</span><span class="sxs-lookup"><span data-stu-id="c4e9e-343">See Also</span></span>
| <span data-ttu-id="c4e9e-344">Tópico</span><span class="sxs-lookup"><span data-stu-id="c4e9e-344">Topic</span></span> | <span data-ttu-id="c4e9e-345">Descrição</span><span class="sxs-lookup"><span data-stu-id="c4e9e-345">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="c4e9e-346">Pipelines</span><span class="sxs-lookup"><span data-stu-id="c4e9e-346">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="c4e9e-347">Este artigo ajuda você a entender os pipelines e atividades do Azure Data Factory e como toouse-los tooconstruct ponta a ponta controladas por dados fluxos de trabalho para seu cenário ou business.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-347">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="c4e9e-348">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="c4e9e-348">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="c4e9e-349">Este artigo o ajuda a entender os conjuntos de dados no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-349">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="c4e9e-350">Agendamento e execução</span><span class="sxs-lookup"><span data-stu-id="c4e9e-350">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="c4e9e-351">Este artigo explica os aspectos de programação e a execução de saudação do modelo de aplicativo do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-351">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="c4e9e-352">Monitorar e gerenciar pipelines usando o Aplicativo de Monitoramento</span><span class="sxs-lookup"><span data-stu-id="c4e9e-352">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="c4e9e-353">Este artigo descreve como toomonitor, gerenciar e depurar pipelines usando Olá monitoramento e gerenciamento de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c4e9e-353">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
