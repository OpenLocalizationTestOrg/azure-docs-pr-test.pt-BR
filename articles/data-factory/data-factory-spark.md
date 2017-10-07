---
title: programas aaaInvoke Spark do Azure Data Factory | Microsoft Docs
description: "Saiba como programas de Spark tooinvoke de uma fábrica de dados do Azure usando hello atividade MapReduce."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: fd98931c-cab5-4d66-97cb-4c947861255c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: f88943ece7ee3d21dedbd857609f1b2713b62741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a><span data-ttu-id="9c105-103">Invocar programas Spark dos pipelines do Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9c105-103">Invoke Spark programs from Azure Data Factory pipelines</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="9c105-104">Atividade de Hive</span><span class="sxs-lookup"><span data-stu-id="9c105-104">Hive Activity</span></span>](data-factory-hive-activity.md)
> * [<span data-ttu-id="9c105-105">Atividade Pig</span><span class="sxs-lookup"><span data-stu-id="9c105-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="9c105-106">Atividade MapReduce</span><span class="sxs-lookup"><span data-stu-id="9c105-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="9c105-107">Atividade de Transmissão do Hadoop</span><span class="sxs-lookup"><span data-stu-id="9c105-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="9c105-108">Atividade do Spark</span><span class="sxs-lookup"><span data-stu-id="9c105-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="9c105-109">Atividade de Execução em Lote do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9c105-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="9c105-110">Atividade do Recurso de Atualização do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9c105-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="9c105-111">Atividade de Procedimento Armazenado</span><span class="sxs-lookup"><span data-stu-id="9c105-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="9c105-112">Atividade do U-SQL do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="9c105-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="9c105-113">Atividade Personalizada do .NET</span><span class="sxs-lookup"><span data-stu-id="9c105-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="9c105-114">Introdução</span><span class="sxs-lookup"><span data-stu-id="9c105-114">Introduction</span></span>
<span data-ttu-id="9c105-115">Atividade do Spark é uma saudação [atividades de transformação de dados](data-factory-data-transformation-activities.md) com suporte do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="9c105-115">Spark Activity is one of hello [data transformation activities](data-factory-data-transformation-activities.md) supported by Azure Data Factory.</span></span> <span data-ttu-id="9c105-116">Esta atividade é executada Olá especificado programa Spark no cluster do Apache Spark no HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c105-116">This activity runs hello specified Spark program on your Apache Spark cluster in Azure HDInsight.</span></span>    

> [!IMPORTANT]
> - <span data-ttu-id="9c105-117">A atividade do Spark não oferece suporte a clusters HDInsight Spark que usam um Azure Data Lake Store como armazenamento primário.</span><span class="sxs-lookup"><span data-stu-id="9c105-117">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
> - <span data-ttu-id="9c105-118">A atividade do Spark dá suporte apenas a clusters HDInsight Spark existentes (seus próprios).</span><span class="sxs-lookup"><span data-stu-id="9c105-118">Spark Activity supports only existing (your own) HDInsight Spark clusters.</span></span> <span data-ttu-id="9c105-119">Ele não dá suporte a serviço vinculado ao HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="9c105-119">It does not support an on-demand HDInsight linked service.</span></span>

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a><span data-ttu-id="9c105-120">Passo a passo: criar um pipeline com atividade do Spark</span><span class="sxs-lookup"><span data-stu-id="9c105-120">Walkthrough: create a pipeline with Spark activity</span></span>
<span data-ttu-id="9c105-121">Aqui estão as etapas típicas de saudação toocreate um pipeline da fábrica de dados com uma atividade Spark.</span><span class="sxs-lookup"><span data-stu-id="9c105-121">Here are hello typical steps toocreate a Data Factory pipeline with a Spark activity.</span></span>  

1. <span data-ttu-id="9c105-122">Criar uma fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="9c105-122">Create a data factory.</span></span>
2. <span data-ttu-id="9c105-123">Crie um toolink de serviço vinculado do armazenamento do Azure o armazenamento do Azure que está associado a sua fábrica de dados de toohello de cluster do HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="9c105-123">Create an Azure Storage linked service toolink your Azure storage that is associated with your HDInsight Spark cluster toohello data factory.</span></span>     
2. <span data-ttu-id="9c105-124">Crie um toolink de serviço vinculado do Azure HDInsight cluster Apache Spark na fábrica de dados do Azure HDInsight toohello.</span><span class="sxs-lookup"><span data-stu-id="9c105-124">Create an Azure HDInsight linked service toolink your Apache Spark cluster in Azure HDInsight toohello data factory.</span></span>
3. <span data-ttu-id="9c105-125">Crie um conjunto de dados refere-se o serviço de armazenamento do Azure vinculada toohello.</span><span class="sxs-lookup"><span data-stu-id="9c105-125">Create a dataset that refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="9c105-126">No momento, você deve especificar um conjunto de dados de saída para uma atividade mesmo que não exista nenhuma saída sendo produzida.</span><span class="sxs-lookup"><span data-stu-id="9c105-126">Currently, you must specify an output dataset for an activity even if there is no output being produced.</span></span>  
4. <span data-ttu-id="9c105-127">Crie um pipeline com atividades Spark que refere-se o serviço vinculado do HDInsight de toohello criado no #2.</span><span class="sxs-lookup"><span data-stu-id="9c105-127">Create a pipeline with Spark activity that refers toohello HDInsight linked service created in #2.</span></span> <span data-ttu-id="9c105-128">Hello atividade está configurada com conjunto de dados de saudação que você criou na etapa anterior, Olá como um conjunto de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="9c105-128">hello activity is configured with hello dataset you created in hello previous step as an output dataset.</span></span> <span data-ttu-id="9c105-129">conjunto de dados de saída de saudação é quais unidades Olá agenda (por hora, diariamente, etc.).</span><span class="sxs-lookup"><span data-stu-id="9c105-129">hello output dataset is what drives hello schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="9c105-130">Portanto, você deve especificar o conjunto de dados de saída de hello mesmo que a atividade de saudação realmente não produzir uma saída.</span><span class="sxs-lookup"><span data-stu-id="9c105-130">Therefore, you must specify hello output dataset even though hello activity does not really produce an output.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="9c105-131">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9c105-131">Prerequisites</span></span>
1. <span data-ttu-id="9c105-132">Criar um **conta de armazenamento do Azure para fins gerais** seguindo as instruções passo a passo de saudação: [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="9c105-132">Create a **general-purpose Azure Storage Account** by following instructions in hello walkthrough: [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
2. <span data-ttu-id="9c105-133">Criar um **cluster Apache Spark no Azure HDInsight** seguindo as instruções no tutorial Olá: [cluster criar Apache Spark no Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="9c105-133">Create an **Apache Spark cluster in Azure HDInsight** by following instructions in hello tutorial: [Create Apache Spark cluster in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="9c105-134">Associe conta de armazenamento do Azure Olá criado na etapa &#1; com este cluster.</span><span class="sxs-lookup"><span data-stu-id="9c105-134">Associate hello Azure storage account you created in step #1 with this cluster.</span></span>  
3. <span data-ttu-id="9c105-135">Baixe e leia o arquivo de script de python Olá **test.py** localizado em: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span><span class="sxs-lookup"><span data-stu-id="9c105-135">Download and review hello python script file **test.py** located at: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span></span>  
3.  <span data-ttu-id="9c105-136">Carregar **test.py** toohello **pyFiles** pasta Olá **adfspark** contêiner no seu armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c105-136">Upload **test.py** toohello **pyFiles** folder in hello **adfspark** container in your Azure Blob storage.</span></span> <span data-ttu-id="9c105-137">Crie contêiner de saudação e a pasta de saudação se não existirem.</span><span class="sxs-lookup"><span data-stu-id="9c105-137">Create hello container and hello folder if they do not exist.</span></span>

### <a name="create-data-factory"></a><span data-ttu-id="9c105-138">Criar um data factory</span><span class="sxs-lookup"><span data-stu-id="9c105-138">Create data factory</span></span>
<span data-ttu-id="9c105-139">Vamos começar com a criação de fábrica de dados Olá nesta etapa.</span><span class="sxs-lookup"><span data-stu-id="9c105-139">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="9c105-140">Faça logon no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9c105-140">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9c105-141">Clique em **novo** no menu esquerdo Olá **dados + análise**e clique em **fábrica de dados**.</span><span class="sxs-lookup"><span data-stu-id="9c105-141">Click **NEW** on hello left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="9c105-142">Em Olá **nova fábrica de dados** folha, digite **SparkDF** para Olá nome.</span><span class="sxs-lookup"><span data-stu-id="9c105-142">In hello **New data factory** blade, enter **SparkDF** for hello Name.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="9c105-143">nome de saudação do hello data factory do Azure deve ser **globalmente exclusivo**.</span><span class="sxs-lookup"><span data-stu-id="9c105-143">hello name of hello Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="9c105-144">Se você vir o erro Olá: **"SparkDF" nome da fábrica de dados não está disponível**.</span><span class="sxs-lookup"><span data-stu-id="9c105-144">If you see hello error: **Data factory name “SparkDF” is not available**.</span></span> <span data-ttu-id="9c105-145">Alterar nome Olá Olá da fábrica de dados (por exemplo, yournameSparkDFdate e tente criar novamente.</span><span class="sxs-lookup"><span data-stu-id="9c105-145">Change hello name of hello data factory (for example, yournameSparkDFdate, and try creating again.</span></span> <span data-ttu-id="9c105-146">Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="9c105-146">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>   
4. <span data-ttu-id="9c105-147">Selecione Olá **assinatura do Azure** onde você deseja Olá toobe de fábrica de dados criado.</span><span class="sxs-lookup"><span data-stu-id="9c105-147">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="9c105-148">Selecione um **grupo de recursos** existente ou crie um grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c105-148">Select an existing **resource group** or create an Azure resource group.</span></span>
6. <span data-ttu-id="9c105-149">Selecione **toodashboard Pin** opção.</span><span class="sxs-lookup"><span data-stu-id="9c105-149">Select **Pin toodashboard** option.</span></span>  
6. <span data-ttu-id="9c105-150">Clique em **criar** em Olá **nova fábrica de dados** folha.</span><span class="sxs-lookup"><span data-stu-id="9c105-150">Click **Create** on hello **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="9c105-151">toocreate instâncias de fábrica de dados, você deve ser um membro da saudação [colaborador da fábrica de dados](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) função no nível do grupo de recursos de assinatura/hello.</span><span class="sxs-lookup"><span data-stu-id="9c105-151">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
7. <span data-ttu-id="9c105-152">Você verá a fábrica de dados hello está sendo criada no hello **painel** de saudação portal do Azure da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="9c105-152">You see hello data factory being created in hello **dashboard** of hello Azure portal as follows:</span></span>   
8. <span data-ttu-id="9c105-153">Depois de fábrica de dados Olá tiver sido criada com êxito, você ver a página de fábrica de dados hello, que mostra Olá conteúdo Olá da fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="9c105-153">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span> <span data-ttu-id="9c105-154">Se você não vir a página de fábrica de dados hello, clique em lado a lado para sua fábrica de dados no painel de Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="9c105-154">If you do not see hello data factory page, click hello tile for your data factory on hello dashboard.</span></span>

    ![Folha Data Factory](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a><span data-ttu-id="9c105-156">Criar serviços vinculados</span><span class="sxs-lookup"><span data-stu-id="9c105-156">Create linked services</span></span>
<span data-ttu-id="9c105-157">Nesta etapa, você cria dois serviços vinculados, um toolink sua fábrica de dados Spark cluster tooyour e Olá outros toolink sua fábrica de dados do armazenamento do Azure tooyour.</span><span class="sxs-lookup"><span data-stu-id="9c105-157">In this step, you create two linked services, one toolink your Spark cluster tooyour data factory, and hello other toolink your Azure storage tooyour data factory.</span></span>  

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="9c105-158">Criar o serviço vinculado do armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="9c105-158">Create Azure Storage linked service</span></span>
<span data-ttu-id="9c105-159">Nesta etapa, você vincular sua fábrica de dados de tooyour de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c105-159">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="9c105-160">Um conjunto de dados que você criar em uma etapa posterior neste passo a passo refere-se o serviço toothis vinculado.</span><span class="sxs-lookup"><span data-stu-id="9c105-160">A dataset you create in a step later in this walkthrough refers toothis linked service.</span></span> <span data-ttu-id="9c105-161">Olá serviço vinculado do HDInsight que você define na próxima etapa do hello se refere a serviço toothis vinculado.</span><span class="sxs-lookup"><span data-stu-id="9c105-161">hello HDInsight linked service that you define in hello next step refers toothis linked service too.</span></span>  

1. <span data-ttu-id="9c105-162">Clique em **autor e implantar** em Olá **Data Factory** folha sua fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="9c105-162">Click **Author and deploy** on hello **Data Factory** blade for your data factory.</span></span> <span data-ttu-id="9c105-163">Você deve ver Olá Editor da fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="9c105-163">You should see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="9c105-164">Clique em **Novo repositório de dados** e escolha **Armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="9c105-164">Click **New data store** and choose **Azure storage**.</span></span>

   ![Novo armazenamento de dados - Armazenamento do Azure - menu](./media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="9c105-166">Você deve ver Olá **script JSON** para a criação de um armazenamento do Azure serviço no editor de saudação vinculado.</span><span class="sxs-lookup"><span data-stu-id="9c105-166">You should see hello **JSON script** for creating an Azure Storage linked service in hello editor.</span></span>

   ![Serviço vinculado de armazenamento do Azure](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="9c105-168">Substituir **nome da conta** e **chave de conta** com hello nome e chave de acesso da sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c105-168">Replace **account name** and **account key** with hello name and access key of your Azure storage account.</span></span> <span data-ttu-id="9c105-169">toolearn como tooget acessar o armazenamento de chave, consulte Olá informações sobre como tooview, copiar e armazenamento regenerar chaves de acesso em [gerenciar sua conta de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="9c105-169">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="9c105-170">toodeploy Olá serviço vinculado, clique em **implantar** na barra de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="9c105-170">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="9c105-171">Depois de hello serviço vinculado foi implantado com êxito, Olá **rascunho 1** janela desaparecerá e você verá **AzureStorageLinkedService** na exibição de árvore Olá Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="9c105-171">After hello linked service is deployed successfully, hello **Draft-1** window should disappear and you see **AzureStorageLinkedService** in hello tree view on hello left.</span></span>

#### <a name="create-hdinsight-linked-service"></a><span data-ttu-id="9c105-172">Criar o serviço vinculado ao HDInsight</span><span class="sxs-lookup"><span data-stu-id="9c105-172">Create HDInsight linked service</span></span>
<span data-ttu-id="9c105-173">Nesta etapa, você criará toolink de serviço vinculado do Azure HDInsight sua fábrica de dados de toohello de cluster do HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="9c105-173">In this step, you create Azure HDInsight linked service toolink your HDInsight Spark cluster toohello data factory.</span></span> <span data-ttu-id="9c105-174">cluster do HDInsight Olá é programa de Spark de saudação toorun usado especificado na atividade de Spark saudação do pipeline de saudação neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="9c105-174">hello HDInsight cluster is used toorun hello Spark program specified in hello Spark activity of hello pipeline in this sample.</span></span>  

1. <span data-ttu-id="9c105-175">Clique em **... Mais** na barra de ferramentas hello, clique em **nova computação**e, em seguida, clique em **cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="9c105-175">Click **... More** on hello toolbar, click **New compute**, and then click **HDInsight cluster**.</span></span>

    ![Criar o serviço vinculado ao HDInsight](media/data-factory-spark/new-hdinsight-linked-service.png)
2. <span data-ttu-id="9c105-177">Copie e cole Olá toohello de trecho de código a seguir **rascunho 1** janela.</span><span class="sxs-lookup"><span data-stu-id="9c105-177">Copy and paste hello following snippet toohello **Draft-1** window.</span></span> <span data-ttu-id="9c105-178">No editor de JSON de Olá Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c105-178">In hello JSON editor, do hello following steps:</span></span>
    1. <span data-ttu-id="9c105-179">Especifique a saudação **URI** para Olá HDInsight Spark do cluster.</span><span class="sxs-lookup"><span data-stu-id="9c105-179">Specify hello **URI** for hello HDInsight Spark cluster.</span></span> <span data-ttu-id="9c105-180">Por exemplo: `https://<sparkclustername>.azurehdinsight.net/`.</span><span class="sxs-lookup"><span data-stu-id="9c105-180">For example: `https://<sparkclustername>.azurehdinsight.net/`.</span></span>
    2. <span data-ttu-id="9c105-181">Especificar nome de saudação do hello **usuário** quem possui o cluster do Spark toohello acesso.</span><span class="sxs-lookup"><span data-stu-id="9c105-181">Specify hello name of hello **user** who has access toohello Spark cluster.</span></span>
    3. <span data-ttu-id="9c105-182">Especifique a saudação **senha** do usuário.</span><span class="sxs-lookup"><span data-stu-id="9c105-182">Specify hello **password** for user.</span></span>
    4. <span data-ttu-id="9c105-183">Especifique a saudação **serviço vinculado do armazenamento do Azure** associada à saudação cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="9c105-183">Specify hello **Azure Storage linked service** that is associated with hello HDInsight Spark cluster.</span></span> <span data-ttu-id="9c105-184">Neste exemplo, é: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="9c105-184">In this example, it is: **AzureStorageLinkedService**.</span></span>

    ```json
    {
        "name": "HDInsightLinkedService",
        "properties": {
            "type": "HDInsight",
            "typeProperties": {
                "clusterUri": "https://<sparkclustername>.azurehdinsight.net/",
                "userName": "admin",
                "password": "**********",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    > [!IMPORTANT]
    > - <span data-ttu-id="9c105-185">A atividade do Spark não oferece suporte a clusters HDInsight Spark que usam um Azure Data Lake Store como armazenamento primário.</span><span class="sxs-lookup"><span data-stu-id="9c105-185">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
    > - <span data-ttu-id="9c105-186">A atividade do Spark dá suporte apenas ao cluster HDInsight Spark existente (seu próprio).</span><span class="sxs-lookup"><span data-stu-id="9c105-186">Spark Activity supports only existing (your own) HDInsight Spark cluster.</span></span> <span data-ttu-id="9c105-187">Ele não dá suporte a serviço vinculado ao HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="9c105-187">It does not support an on-demand HDInsight linked service.</span></span>

    <span data-ttu-id="9c105-188">Consulte [serviço vinculado HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) para obter detalhes sobre Olá HDInsight serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="9c105-188">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details about hello HDInsight linked service.</span></span>
3.  <span data-ttu-id="9c105-189">toodeploy Olá serviço vinculado, clique em **implantar** na barra de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="9c105-189">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="9c105-190">Criar conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="9c105-190">Create output dataset</span></span>
<span data-ttu-id="9c105-191">conjunto de dados de saída de saudação é quais unidades Olá agenda (por hora, diariamente, etc.).</span><span class="sxs-lookup"><span data-stu-id="9c105-191">hello output dataset is what drives hello schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="9c105-192">Portanto, você deve especificar um conjunto de dados de saída para a atividade do spark Olá no pipeline de saudação mesmo que a atividade de saudação realmente não produzir qualquer saída.</span><span class="sxs-lookup"><span data-stu-id="9c105-192">Therefore, you must specify an output dataset for hello spark activity in hello pipeline even though hello activity does not really produce any output.</span></span> <span data-ttu-id="9c105-193">A especificação de um conjunto de dados de entrada para a atividade de saudação é opcional.</span><span class="sxs-lookup"><span data-stu-id="9c105-193">Specifying an input dataset for hello activity is optional.</span></span>

1. <span data-ttu-id="9c105-194">Em Olá **Editor da fábrica de dados**, clique em **... Mais** na barra de comandos de saudação, clique em **novo conjunto de dados**e selecione **armazenamento de BLOBs do Azure**.</span><span class="sxs-lookup"><span data-stu-id="9c105-194">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="9c105-195">Copie e cole Olá janela toohello rascunho-1 de trecho de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="9c105-195">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="9c105-196">trecho JSON a saudação define um conjunto de dados chamado **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="9c105-196">hello JSON snippet defines a dataset called **OutputDataset**.</span></span> <span data-ttu-id="9c105-197">Além disso, você especificar que os resultados de hello são armazenados no contêiner de blob Olá chamado **adfspark** e Olá pasta chamada **pyFiles/saída**.</span><span class="sxs-lookup"><span data-stu-id="9c105-197">In addition, you specify that hello results are stored in hello blob container called **adfspark** and hello folder called **pyFiles/output**.</span></span> <span data-ttu-id="9c105-198">Como mencionado anteriormente, esse conjunto de dados é fictício.</span><span class="sxs-lookup"><span data-stu-id="9c105-198">As mentioned earlier, this dataset is a dummy dataset.</span></span> <span data-ttu-id="9c105-199">programa Spark Olá neste exemplo não gera nenhuma saída.</span><span class="sxs-lookup"><span data-stu-id="9c105-199">hello Spark program in this example does not produce any output.</span></span> <span data-ttu-id="9c105-200">Olá **disponibilidade** seção especifica esse conjunto de dados de saída de saudação é produzido diariamente.</span><span class="sxs-lookup"><span data-stu-id="9c105-200">hello **availability** section specifies that hello output dataset is produced daily.</span></span>  

    ```json
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "sparkoutput.txt",
                "folderPath": "adfspark/pyFiles/output",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": "\t"
                }
            },
            "availability": {
                "frequency": "Day",
                "interval": 1
            }
        }
    }
    ```
3. <span data-ttu-id="9c105-201">toodeploy Olá conjunto de dados, clique em **implantar** na barra de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="9c105-201">toodeploy hello dataset, click **Deploy** on hello command bar.</span></span>


### <a name="create-pipeline"></a><span data-ttu-id="9c105-202">Criar um pipeline</span><span class="sxs-lookup"><span data-stu-id="9c105-202">Create pipeline</span></span>
<span data-ttu-id="9c105-203">Nesta etapa, você cria um pipeline com a atividade **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="9c105-203">In this step, you create a pipeline with a **HDInsightSpark** activity.</span></span> <span data-ttu-id="9c105-204">Atualmente, o conjunto de dados de saída é quais unidades Olá agendamento, então você deve criar um conjunto de dados de saída, mesmo que a atividade de saudação não produz nenhuma saída.</span><span class="sxs-lookup"><span data-stu-id="9c105-204">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="9c105-205">Se a atividade de saudação não tem nenhuma entrada, você poderá ignorar o dataset de entrada hello criando.</span><span class="sxs-lookup"><span data-stu-id="9c105-205">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="9c105-206">Portanto, nenhum conjunto de dados de entrada é especificado neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="9c105-206">Therefore, no input dataset is specified in this example.</span></span>

1. <span data-ttu-id="9c105-207">Em Olá **Editor da fábrica de dados**, clique em **... Mais** Olá barra de comandos e, em seguida, clique em **novo pipeline**.</span><span class="sxs-lookup"><span data-stu-id="9c105-207">In hello **Data Factory Editor**, click **… More** on hello command bar, and then click **New pipeline**.</span></span>
2. <span data-ttu-id="9c105-208">Substitua script hello na janela Olá rascunho-1 com hello script a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c105-208">Replace hello script in hello Draft-1 window with hello following script:</span></span>

    ```json
    {
        "name": "SparkPipeline",
        "properties": {
            "activities": [
                {
                    "type": "HDInsightSpark",
                    "typeProperties": {
                        "rootPath": "adfspark\\pyFiles",
                        "entryFilePath": "test.py",
                        "getDebugInfo": "Always"
                    },
                    "outputs": [
                        {
                            "name": "OutputDataset"
                        }
                    ],
                    "name": "MySparkActivity",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-02-05T00:00:00Z",
            "end": "2017-02-06T00:00:00Z"
        }
    }
    ```
    <span data-ttu-id="9c105-209">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c105-209">Note hello following points:</span></span>
    - <span data-ttu-id="9c105-210">Olá **tipo** propriedade for definida muito**HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="9c105-210">hello **type** property is set too**HDInsightSpark**.</span></span>
    - <span data-ttu-id="9c105-211">Olá **rootPath** está definido muito**adfspark\\pyFiles** onde adfspark é o contêiner de BLOBs do Azure hello e pyFiles é a pasta bem no contêiner.</span><span class="sxs-lookup"><span data-stu-id="9c105-211">hello **rootPath** is set too**adfspark\\pyFiles** where adfspark is hello Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="9c105-212">Neste exemplo, Olá armazenamento de BLOBs do Azure é hello que está associado ao cluster do Spark hello.</span><span class="sxs-lookup"><span data-stu-id="9c105-212">In this example, hello Azure Blob Storage is hello one that is associated with hello Spark cluster.</span></span> <span data-ttu-id="9c105-213">Você pode carregar Olá arquivo tooa armazenamento do Azure diferente.</span><span class="sxs-lookup"><span data-stu-id="9c105-213">You can upload hello file tooa different Azure Storage.</span></span> <span data-ttu-id="9c105-214">Se você fizer isso, crie um toolink de serviço vinculado do armazenamento do Azure essa fábrica de dados de toohello de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9c105-214">If you do so, create an Azure Storage linked service toolink that storage account toohello data factory.</span></span> <span data-ttu-id="9c105-215">Em seguida, especifique o nome de Olá de serviço de Olá vinculado como um valor para Olá **sparkJobLinkedService** propriedade.</span><span class="sxs-lookup"><span data-stu-id="9c105-215">Then, specify hello name of hello linked service as a value for hello **sparkJobLinkedService** property.</span></span> <span data-ttu-id="9c105-216">Consulte [propriedades da atividade Spark](#spark-activity-properties) para obter detalhes sobre essa propriedade e outras propriedades com suporte hello atividade Spark.</span><span class="sxs-lookup"><span data-stu-id="9c105-216">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by hello Spark Activity.</span></span>  
    - <span data-ttu-id="9c105-217">Olá **entryFilePath** está definida toohello **test.py**, que é o arquivo de python hello.</span><span class="sxs-lookup"><span data-stu-id="9c105-217">hello **entryFilePath** is set toohello **test.py**, which is hello python file.</span></span>
    - <span data-ttu-id="9c105-218">Olá **getDebugInfo** propriedade for definida muito**sempre**, que significa que os arquivos de log Olá sempre são gerados (sucesso ou falha).</span><span class="sxs-lookup"><span data-stu-id="9c105-218">hello **getDebugInfo** property is set too**Always**, which means hello log files are always generated (success or failure).</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="9c105-219">É recomendável que você não defina essa propriedade muito`Always` em um ambiente de produção, a menos que você estiver solucionando um problema.</span><span class="sxs-lookup"><span data-stu-id="9c105-219">We recommend that you do not set this property too`Always` in a production environment unless you are troubleshooting an issue.</span></span>
    - <span data-ttu-id="9c105-220">Olá **gera** seção tem um conjunto de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="9c105-220">hello **outputs** section has one output dataset.</span></span> <span data-ttu-id="9c105-221">Você deve especificar um conjunto de dados de saída, mesmo que o programa de spark Olá não produz nenhuma saída.</span><span class="sxs-lookup"><span data-stu-id="9c105-221">You must specify an output dataset even if hello spark program does not produce any output.</span></span> <span data-ttu-id="9c105-222">Olá dataset unidades Olá agenda para o pipeline de saudação (por hora, diariamente, etc.).</span><span class="sxs-lookup"><span data-stu-id="9c105-222">hello output dataset drives hello schedule for hello pipeline (hourly, daily, etc.).</span></span>  

        <span data-ttu-id="9c105-223">Para obter detalhes sobre as propriedades de hello atividade Spark com suporte, consulte [despertar propriedades da atividade](#spark-activity-properties) seção.</span><span class="sxs-lookup"><span data-stu-id="9c105-223">For details about hello properties supported by Spark activity, see [Spark activity properties](#spark-activity-properties) section.</span></span>
3. <span data-ttu-id="9c105-224">pipeline de saudação toodeploy, clique em **implantar** na barra de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="9c105-224">toodeploy hello pipeline, click **Deploy** on hello command bar.</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="9c105-225">Monitorar o pipeline</span><span class="sxs-lookup"><span data-stu-id="9c105-225">Monitor pipeline</span></span>
1. <span data-ttu-id="9c105-226">Clique em **X** tooclose folhas de Editor de fábrica de dados e toonavigate home page do toohello fábrica de dados de volta.</span><span class="sxs-lookup"><span data-stu-id="9c105-226">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory home page.</span></span> <span data-ttu-id="9c105-227">Clique em **monitorar e gerenciar** toolaunch Olá monitoramento do aplicativo em outra guia.</span><span class="sxs-lookup"><span data-stu-id="9c105-227">Click **Monitor and Manage** toolaunch hello monitoring application in another tab.</span></span>

    ![Bloco Monitorar e Gerenciar](media/data-factory-spark/monitor-and-manage-tile.png)
2. <span data-ttu-id="9c105-229">Saudação de alteração **hora de início** filtrar na parte superior da saudação muito**1/2/2017**e clique em **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="9c105-229">Change hello **Start time** filter at hello top too**2/1/2017**, and click **Apply**.</span></span>
3. <span data-ttu-id="9c105-230">Como há somente um dia entre hello (2017-02-01) de início e término (2017-02-02) do pipeline Olá, você verá somente uma janela de atividade.</span><span class="sxs-lookup"><span data-stu-id="9c105-230">You should see only one activity window as there is only one day between hello start (2017-02-01) and end times (2017-02-02) of hello pipeline.</span></span> <span data-ttu-id="9c105-231">Confirmar que a fatia de dados hello está **pronto** estado.</span><span class="sxs-lookup"><span data-stu-id="9c105-231">Confirm that hello data slice is in **ready** state.</span></span>

    ![Pipeline de saudação do monitor](media/data-factory-spark/monitor-and-manage-app.png)    
4. <span data-ttu-id="9c105-233">Selecione Olá **janela de atividade** toosee detalhes sobre a atividade de saudação executar.</span><span class="sxs-lookup"><span data-stu-id="9c105-233">Select hello **activity window** toosee details about hello activity run.</span></span> <span data-ttu-id="9c105-234">Se houver um erro, você pode ver detalhes sobre ele no painel direito da saudação.</span><span class="sxs-lookup"><span data-stu-id="9c105-234">If there is an error, you see details about it in hello right pane.</span></span>

### <a name="verify-hello-results"></a><span data-ttu-id="9c105-235">Verificar os resultados de saudação</span><span class="sxs-lookup"><span data-stu-id="9c105-235">Verify hello results</span></span>

1. <span data-ttu-id="9c105-236">Inicie o **Notebook Jupyter** para seu cluster do HDInsight Spark, navegando até: https://NOMEDOCLUSTER.azurehdinsight.net/jupyter.</span><span class="sxs-lookup"><span data-stu-id="9c105-236">Launch **Jupyter notebook** for your HDInsight Spark cluster by navigating to: https://CLUSTERNAME.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="9c105-237">Você pode também iniciar o painel do cluster para o cluster do HDInsight Spark e, em seguida, iniciar **Notebook Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="9c105-237">You can also launch cluster dashboard for your HDInsight Spark cluster, and then launch **Jupyter Notebook**.</span></span>
2. <span data-ttu-id="9c105-238">Clique em **novo** -> **PySpark** toostart um novo bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="9c105-238">Click **New** -> **PySpark** toostart a new notebook.</span></span>

    ![Novo notebook Jupyter](media/data-factory-spark/jupyter-new-book.png)
3. <span data-ttu-id="9c105-240">Execução hello seguinte comando copiar/colar o texto de saudação e pressionando **SHIFT + ENTER** final Olá da segunda instrução de saudação.</span><span class="sxs-lookup"><span data-stu-id="9c105-240">Run hello following command by copy/pasting hello text and pressing **SHIFT + ENTER** at hello end of hello second statement.</span></span>  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. <span data-ttu-id="9c105-241">Certifique-se de que você vê dados saudação da tabela de hvac hello:</span><span class="sxs-lookup"><span data-stu-id="9c105-241">Confirm that you see hello data from hello hvac table:</span></span>  

    ![Resultados da consulta do Jupyter](media/data-factory-spark/jupyter-notebook-results.png)

<span data-ttu-id="9c105-243">Veja a seção [Executar uma consulta SQL do Spark](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) para obter instruções detalhadas.</span><span class="sxs-lookup"><span data-stu-id="9c105-243">See [Run a Spark SQL query](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) section for detailed instructions.</span></span> 

### <a name="troubleshooting"></a><span data-ttu-id="9c105-244">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="9c105-244">Troubleshooting</span></span>
<span data-ttu-id="9c105-245">Desde que você definir **getDebugInfo** muito**sempre**, você verá um **log** subpasta Olá **pyFiles** pasta em seu contêiner de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c105-245">Since you set **getDebugInfo** too**Always**, you see a **log** subfolder in hello **pyFiles** folder in your Azure Blob container.</span></span> <span data-ttu-id="9c105-246">arquivo de log de saudação na pasta de log Olá fornece detalhes adicionais.</span><span class="sxs-lookup"><span data-stu-id="9c105-246">hello log file in hello log folder provides additional details.</span></span> <span data-ttu-id="9c105-247">Esse arquivo de log é especialmente útil quando há um erro.</span><span class="sxs-lookup"><span data-stu-id="9c105-247">This log file is especially useful when there is an error.</span></span> <span data-ttu-id="9c105-248">Em um ambiente de produção, convém tooset-muito**falha**.</span><span class="sxs-lookup"><span data-stu-id="9c105-248">In a production environment, you may want tooset it too**Failure**.</span></span>

<span data-ttu-id="9c105-249">Para solução de problemas, Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c105-249">For further troubleshooting, do hello following steps:</span></span>


1. <span data-ttu-id="9c105-250">Navegue muito`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span><span class="sxs-lookup"><span data-stu-id="9c105-250">Navigate too`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span></span>

    ![Aplicativo de interface do usuário do YARN](media/data-factory-spark/yarnui-application.png)  
2. <span data-ttu-id="9c105-252">Clique em **Logs** para uma saudação executar tentativas.</span><span class="sxs-lookup"><span data-stu-id="9c105-252">Click **Logs** for one of hello run attempts.</span></span>

    ![Página do aplicativo](media/data-factory-spark/yarn-applications.png)
3. <span data-ttu-id="9c105-254">Você deve ver as informações de erro adicionais na página de registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="9c105-254">You should see additional error information in hello log page.</span></span>

    ![Log de erros](media/data-factory-spark/yarnui-application-error.png)

<span data-ttu-id="9c105-256">Olá seções a seguir fornece informações sobre o cluster do Data Factory entidades toouse Apache Spark e atividade do Spark sua fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="9c105-256">hello following sections provide information about Data Factory entities toouse Apache Spark cluster and Spark Activity in your data factory.</span></span>

## <a name="spark-activity-properties"></a><span data-ttu-id="9c105-257">Propriedades da Atividade do Spark</span><span class="sxs-lookup"><span data-stu-id="9c105-257">Spark activity properties</span></span>
<span data-ttu-id="9c105-258">Aqui está a definição de JSON de exemplo hello de um pipeline com Spark atividade:</span><span class="sxs-lookup"><span data-stu-id="9c105-258">Here is hello sample JSON definition of a pipeline with Spark Activity:</span></span>    

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "arguments": [ "arg1", "arg2" ],
                    "sparkConfig": {
                        "spark.python.worker.memory": "512m"
                    }
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "description": "This activity invokes hello Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

<span data-ttu-id="9c105-259">Olá tabela a seguir descreve as propriedades JSON Olá usadas na definição JSON da saudação:</span><span class="sxs-lookup"><span data-stu-id="9c105-259">hello following table describes hello JSON properties used in hello JSON definition:</span></span>

| <span data-ttu-id="9c105-260">Propriedade</span><span class="sxs-lookup"><span data-stu-id="9c105-260">Property</span></span> | <span data-ttu-id="9c105-261">Descrição</span><span class="sxs-lookup"><span data-stu-id="9c105-261">Description</span></span> | <span data-ttu-id="9c105-262">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="9c105-262">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="9c105-263">name</span><span class="sxs-lookup"><span data-stu-id="9c105-263">name</span></span> | <span data-ttu-id="9c105-264">Nome da atividade de saudação no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="9c105-264">Name of hello activity in hello pipeline.</span></span> | <span data-ttu-id="9c105-265">Sim</span><span class="sxs-lookup"><span data-stu-id="9c105-265">Yes</span></span> |
| <span data-ttu-id="9c105-266">description</span><span class="sxs-lookup"><span data-stu-id="9c105-266">description</span></span> | <span data-ttu-id="9c105-267">Texto que descreve quais atividade Olá faz.</span><span class="sxs-lookup"><span data-stu-id="9c105-267">Text describing what hello activity does.</span></span> | <span data-ttu-id="9c105-268">Não</span><span class="sxs-lookup"><span data-stu-id="9c105-268">No</span></span> |
| <span data-ttu-id="9c105-269">type</span><span class="sxs-lookup"><span data-stu-id="9c105-269">type</span></span> | <span data-ttu-id="9c105-270">Essa propriedade deve ser definida como tooHDInsightSpark.</span><span class="sxs-lookup"><span data-stu-id="9c105-270">This property must be set tooHDInsightSpark.</span></span> | <span data-ttu-id="9c105-271">Sim</span><span class="sxs-lookup"><span data-stu-id="9c105-271">Yes</span></span> |
| <span data-ttu-id="9c105-272">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="9c105-272">linkedServiceName</span></span> | <span data-ttu-id="9c105-273">Nome do hello HDInsight vinculado no qual Olá Spark executa o programa de serviço.</span><span class="sxs-lookup"><span data-stu-id="9c105-273">Name of hello HDInsight linked service on which hello Spark program runs.</span></span> | <span data-ttu-id="9c105-274">Sim</span><span class="sxs-lookup"><span data-stu-id="9c105-274">Yes</span></span> |
| <span data-ttu-id="9c105-275">rootPath</span><span class="sxs-lookup"><span data-stu-id="9c105-275">rootPath</span></span> | <span data-ttu-id="9c105-276">contêiner de BLOBs do Azure Hello e pasta que contém o arquivo do Spark hello.</span><span class="sxs-lookup"><span data-stu-id="9c105-276">hello Azure Blob container and folder that contains hello Spark file.</span></span> <span data-ttu-id="9c105-277">nome do arquivo Hello diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="9c105-277">hello file name is case-sensitive.</span></span> | <span data-ttu-id="9c105-278">Sim</span><span class="sxs-lookup"><span data-stu-id="9c105-278">Yes</span></span> |
| <span data-ttu-id="9c105-279">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="9c105-279">entryFilePath</span></span> | <span data-ttu-id="9c105-280">Pasta de raiz de toohello de caminho relativo da saudação Spark/pacote de código.</span><span class="sxs-lookup"><span data-stu-id="9c105-280">Relative path toohello root folder of hello Spark code/package.</span></span> | <span data-ttu-id="9c105-281">Sim</span><span class="sxs-lookup"><span data-stu-id="9c105-281">Yes</span></span> |
| <span data-ttu-id="9c105-282">className</span><span class="sxs-lookup"><span data-stu-id="9c105-282">className</span></span> | <span data-ttu-id="9c105-283">Classe principal de Java/Spark do aplicativo</span><span class="sxs-lookup"><span data-stu-id="9c105-283">Application's Java/Spark main class</span></span> | <span data-ttu-id="9c105-284">Não</span><span class="sxs-lookup"><span data-stu-id="9c105-284">No</span></span> |
| <span data-ttu-id="9c105-285">argumentos</span><span class="sxs-lookup"><span data-stu-id="9c105-285">arguments</span></span> | <span data-ttu-id="9c105-286">Uma lista de programas de Spark toohello argumentos de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="9c105-286">A list of command-line arguments toohello Spark program.</span></span> | <span data-ttu-id="9c105-287">Não</span><span class="sxs-lookup"><span data-stu-id="9c105-287">No</span></span> |
| <span data-ttu-id="9c105-288">proxyUser</span><span class="sxs-lookup"><span data-stu-id="9c105-288">proxyUser</span></span> | <span data-ttu-id="9c105-289">programa de saudação usuário conta tooimpersonate tooexecute Olá Spark</span><span class="sxs-lookup"><span data-stu-id="9c105-289">hello user account tooimpersonate tooexecute hello Spark program</span></span> | <span data-ttu-id="9c105-290">Não</span><span class="sxs-lookup"><span data-stu-id="9c105-290">No</span></span> |
| <span data-ttu-id="9c105-291">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="9c105-291">sparkConfig</span></span> | <span data-ttu-id="9c105-292">Especificar valores para propriedades de configuração do Spark listados no tópico Olá: [Spark configuração - propriedades de aplicativo](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span><span class="sxs-lookup"><span data-stu-id="9c105-292">Specify values for Spark configuration properties listed in hello topic: [Spark Configuration - Application properties](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span></span> | <span data-ttu-id="9c105-293">Não</span><span class="sxs-lookup"><span data-stu-id="9c105-293">No</span></span> |
| <span data-ttu-id="9c105-294">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="9c105-294">getDebugInfo</span></span> | <span data-ttu-id="9c105-295">Especifica quando arquivos de log do Spark Olá são copiado toohello usado pelo cluster do HDInsight de armazenamento do Azure (ou) especificado por sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="9c105-295">Specifies when hello Spark log files are copied toohello Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="9c105-296">Valores permitidos: Nenhum, Sempre ou Falha.</span><span class="sxs-lookup"><span data-stu-id="9c105-296">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="9c105-297">Valor padrão: Nenhum.</span><span class="sxs-lookup"><span data-stu-id="9c105-297">Default value: None.</span></span> | <span data-ttu-id="9c105-298">Não</span><span class="sxs-lookup"><span data-stu-id="9c105-298">No</span></span> |
| <span data-ttu-id="9c105-299">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="9c105-299">sparkJobLinkedService</span></span> | <span data-ttu-id="9c105-300">Olá serviço vinculado do armazenamento do Azure que contém o arquivo de trabalho do Spark hello, dependências e logs.</span><span class="sxs-lookup"><span data-stu-id="9c105-300">hello Azure Storage linked service that holds hello Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="9c105-301">Se você não especificar um valor para essa propriedade, armazenamento de saudação associado com o cluster HDInsight é usado.</span><span class="sxs-lookup"><span data-stu-id="9c105-301">If you do not specify a value for this property, hello storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="9c105-302">Não</span><span class="sxs-lookup"><span data-stu-id="9c105-302">No</span></span> |

## <a name="folder-structure"></a><span data-ttu-id="9c105-303">Estrutura de pastas</span><span class="sxs-lookup"><span data-stu-id="9c105-303">Folder structure</span></span>
<span data-ttu-id="9c105-304">Hello atividade Spark não oferece suporte a um script em linha como o Pig e Hive atividades realizar.</span><span class="sxs-lookup"><span data-stu-id="9c105-304">hello Spark activity does not support an in-line script as Pig and Hive activities do.</span></span> <span data-ttu-id="9c105-305">Os trabalhos do Spark também são mais extensíveis do que trabalhos do Pig/Hive.</span><span class="sxs-lookup"><span data-stu-id="9c105-305">Spark jobs are also more extensible than Pig/Hive jobs.</span></span> <span data-ttu-id="9c105-306">Para trabalhos de Spark, você pode fornecer várias dependências, como jar pacotes (colocados em java Olá CLASSPATH), arquivos de python (colocados nos Olá PYTHONPATH) e outros arquivos.</span><span class="sxs-lookup"><span data-stu-id="9c105-306">For Spark jobs, you can provide multiple dependencies such as jar packages (placed in hello java CLASSPATH), python files (placed on hello PYTHONPATH), and any other files.</span></span>

<span data-ttu-id="9c105-307">Crie hello seguindo a estrutura de pastas no hello referenciado por Olá serviço vinculado do HDInsight de armazenamento de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c105-307">Create hello following folder structure in hello Azure Blob storage referenced by hello HDInsight linked service.</span></span> <span data-ttu-id="9c105-308">Em seguida, carregue os arquivos dependentes toohello apropriado subpastas na pasta raiz de saudação representado por **entryFilePath**.</span><span class="sxs-lookup"><span data-stu-id="9c105-308">Then, upload dependent files toohello appropriate sub folders in hello root folder represented by **entryFilePath**.</span></span> <span data-ttu-id="9c105-309">Por exemplo, carregar subpasta do python arquivos toohello pyFiles e jar arquivos toohello jars subpasta da pasta raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="9c105-309">For example, upload python files toohello pyFiles subfolder and jar files toohello jars subfolder of hello root folder.</span></span> <span data-ttu-id="9c105-310">Em tempo de execução, o serviço de fábrica de dados espera Olá seguindo a estrutura de pastas no hello armazenamento de BLOBs do Azure:</span><span class="sxs-lookup"><span data-stu-id="9c105-310">At runtime, Data Factory service expects hello following folder structure in hello Azure Blob storage:</span></span>     

| <span data-ttu-id="9c105-311">Caminho</span><span class="sxs-lookup"><span data-stu-id="9c105-311">Path</span></span> | <span data-ttu-id="9c105-312">Descrição</span><span class="sxs-lookup"><span data-stu-id="9c105-312">Description</span></span> | <span data-ttu-id="9c105-313">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="9c105-313">Required</span></span> | <span data-ttu-id="9c105-314">Tipo</span><span class="sxs-lookup"><span data-stu-id="9c105-314">Type</span></span> |
| ---- | ----------- | -------- | ---- |
| <span data-ttu-id="9c105-315">.</span><span class="sxs-lookup"><span data-stu-id="9c105-315">.</span></span> | <span data-ttu-id="9c105-316">caminho de raiz de saudação do trabalho do Spark Olá no serviço vinculado de armazenamento de saudação</span><span class="sxs-lookup"><span data-stu-id="9c105-316">hello root path of hello Spark job in hello storage linked service</span></span>    | <span data-ttu-id="9c105-317">Sim</span><span class="sxs-lookup"><span data-stu-id="9c105-317">Yes</span></span> | <span data-ttu-id="9c105-318">Pasta</span><span class="sxs-lookup"><span data-stu-id="9c105-318">Folder</span></span> |
| <span data-ttu-id="9c105-319">&lt;definido pelo usuário&gt;</span><span class="sxs-lookup"><span data-stu-id="9c105-319">&lt;user defined &gt;</span></span> | <span data-ttu-id="9c105-320">caminho de saudação apontando toohello arquivo de entrada do trabalho de Spark Olá</span><span class="sxs-lookup"><span data-stu-id="9c105-320">hello path pointing toohello entry file of hello Spark job</span></span> | <span data-ttu-id="9c105-321">Sim</span><span class="sxs-lookup"><span data-stu-id="9c105-321">Yes</span></span> | <span data-ttu-id="9c105-322">Arquivo</span><span class="sxs-lookup"><span data-stu-id="9c105-322">File</span></span> |
| <span data-ttu-id="9c105-323">./jars</span><span class="sxs-lookup"><span data-stu-id="9c105-323">./jars</span></span> | <span data-ttu-id="9c105-324">Todos os arquivos nesta pasta são carregados e colocados no classpath java de saudação do cluster de saudação</span><span class="sxs-lookup"><span data-stu-id="9c105-324">All files under this folder are uploaded and placed on hello java classpath of hello cluster</span></span> | <span data-ttu-id="9c105-325">Não</span><span class="sxs-lookup"><span data-stu-id="9c105-325">No</span></span> | <span data-ttu-id="9c105-326">Pasta</span><span class="sxs-lookup"><span data-stu-id="9c105-326">Folder</span></span> |
| <span data-ttu-id="9c105-327">./pyFiles</span><span class="sxs-lookup"><span data-stu-id="9c105-327">./pyFiles</span></span> | <span data-ttu-id="9c105-328">Todos os arquivos nesta pasta são carregados e colocados em Olá PYTHONPATH de cluster Olá</span><span class="sxs-lookup"><span data-stu-id="9c105-328">All files under this folder are uploaded and placed on hello PYTHONPATH of hello cluster</span></span> | <span data-ttu-id="9c105-329">Não</span><span class="sxs-lookup"><span data-stu-id="9c105-329">No</span></span> | <span data-ttu-id="9c105-330">Pasta</span><span class="sxs-lookup"><span data-stu-id="9c105-330">Folder</span></span> |
| <span data-ttu-id="9c105-331">./files</span><span class="sxs-lookup"><span data-stu-id="9c105-331">./files</span></span> | <span data-ttu-id="9c105-332">Todos os arquivos nessa pasta são carregados e colocados no diretório de trabalho executor</span><span class="sxs-lookup"><span data-stu-id="9c105-332">All files under this folder are uploaded and placed on executor working directory</span></span> | <span data-ttu-id="9c105-333">Não</span><span class="sxs-lookup"><span data-stu-id="9c105-333">No</span></span> | <span data-ttu-id="9c105-334">Pasta</span><span class="sxs-lookup"><span data-stu-id="9c105-334">Folder</span></span> |
| <span data-ttu-id="9c105-335">./archives</span><span class="sxs-lookup"><span data-stu-id="9c105-335">./archives</span></span> | <span data-ttu-id="9c105-336">Todos os arquivos nessa pasta são descompactados</span><span class="sxs-lookup"><span data-stu-id="9c105-336">All files under this folder are uncompressed</span></span> | <span data-ttu-id="9c105-337">Não</span><span class="sxs-lookup"><span data-stu-id="9c105-337">No</span></span> | <span data-ttu-id="9c105-338">Pasta</span><span class="sxs-lookup"><span data-stu-id="9c105-338">Folder</span></span> |
| <span data-ttu-id="9c105-339">./logs</span><span class="sxs-lookup"><span data-stu-id="9c105-339">./logs</span></span> | <span data-ttu-id="9c105-340">pasta Olá onde os logs de cluster do Spark Olá são armazenados.</span><span class="sxs-lookup"><span data-stu-id="9c105-340">hello folder where logs from hello Spark cluster are stored.</span></span>| <span data-ttu-id="9c105-341">Não</span><span class="sxs-lookup"><span data-stu-id="9c105-341">No</span></span> | <span data-ttu-id="9c105-342">Pasta</span><span class="sxs-lookup"><span data-stu-id="9c105-342">Folder</span></span> |

<span data-ttu-id="9c105-343">Aqui está um exemplo de um armazenamento que contém dois arquivos de trabalho do Spark no hello armazenamento de BLOBs do Azure referenciada por Olá serviço vinculado do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9c105-343">Here is an example for a storage containing two Spark job files in hello Azure Blob Storage referenced by hello HDInsight linked service.</span></span>

```
SparkJob1
    main.jar
    files
        input1.txt
        input2.txt
    jars
        package1.jar
        package2.jar
    logs

SparkJob2
    main.py
    pyFiles
        scrip1.py
        script2.py
    logs
```
