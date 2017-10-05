---
title: Invocar programas Spark do Azure Data Factory | Microsoft Docs
description: Aprenda a invocar programas Spark de uma Azure Data Factory usando a atividade MapReduce.
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
ms.openlocfilehash: 57894bbdd9208f8c32eb65e29f04e2ae723780ca
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a><span data-ttu-id="ae782-103">Invocar programas Spark dos pipelines do Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="ae782-103">Invoke Spark programs from Azure Data Factory pipelines</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="ae782-104">Atividade de Hive</span><span class="sxs-lookup"><span data-stu-id="ae782-104">Hive Activity</span></span>](data-factory-hive-activity.md)
> * [<span data-ttu-id="ae782-105">Atividade Pig</span><span class="sxs-lookup"><span data-stu-id="ae782-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="ae782-106">Atividade MapReduce</span><span class="sxs-lookup"><span data-stu-id="ae782-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="ae782-107">Atividade de Transmissão do Hadoop</span><span class="sxs-lookup"><span data-stu-id="ae782-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="ae782-108">Atividade do Spark</span><span class="sxs-lookup"><span data-stu-id="ae782-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="ae782-109">Atividade de Execução em Lote do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="ae782-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="ae782-110">Atividade do Recurso de Atualização do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="ae782-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="ae782-111">Atividade de Procedimento Armazenado</span><span class="sxs-lookup"><span data-stu-id="ae782-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="ae782-112">Atividade do U-SQL do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="ae782-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="ae782-113">Atividade Personalizada do .NET</span><span class="sxs-lookup"><span data-stu-id="ae782-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="ae782-114">Introdução</span><span class="sxs-lookup"><span data-stu-id="ae782-114">Introduction</span></span>
<span data-ttu-id="ae782-115">A atividade do Spark é uma das [atividades de transformação de dados](data-factory-data-transformation-activities.md) com suporte pelo Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ae782-115">Spark Activity is one of the [data transformation activities](data-factory-data-transformation-activities.md) supported by Azure Data Factory.</span></span> <span data-ttu-id="ae782-116">Esta atividade executa o programa do Spark especificado no cluster do Apache Spark no Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ae782-116">This activity runs the specified Spark program on your Apache Spark cluster in Azure HDInsight.</span></span>    

> [!IMPORTANT]
> - <span data-ttu-id="ae782-117">A atividade do Spark não oferece suporte a clusters HDInsight Spark que usam um Azure Data Lake Store como armazenamento primário.</span><span class="sxs-lookup"><span data-stu-id="ae782-117">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
> - <span data-ttu-id="ae782-118">A atividade do Spark dá suporte apenas a clusters HDInsight Spark existentes (seus próprios).</span><span class="sxs-lookup"><span data-stu-id="ae782-118">Spark Activity supports only existing (your own) HDInsight Spark clusters.</span></span> <span data-ttu-id="ae782-119">Ele não dá suporte a serviço vinculado ao HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="ae782-119">It does not support an on-demand HDInsight linked service.</span></span>

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a><span data-ttu-id="ae782-120">Passo a passo: criar um pipeline com atividade do Spark</span><span class="sxs-lookup"><span data-stu-id="ae782-120">Walkthrough: create a pipeline with Spark activity</span></span>
<span data-ttu-id="ae782-121">Aqui estão as etapas típicas para criar um pipeline do Data Factory com uma Atividade do Spark.</span><span class="sxs-lookup"><span data-stu-id="ae782-121">Here are the typical steps to create a Data Factory pipeline with a Spark activity.</span></span>  

1. <span data-ttu-id="ae782-122">Criar uma fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="ae782-122">Create a data factory.</span></span>
2. <span data-ttu-id="ae782-123">Crie um serviço vinculado ao Armazenamento do Azure para vincular seu armazenamento do Azure que está associado ao cluster HDInsight Spark para o data factory.</span><span class="sxs-lookup"><span data-stu-id="ae782-123">Create an Azure Storage linked service to link your Azure storage that is associated with your HDInsight Spark cluster to the data factory.</span></span>     
2. <span data-ttu-id="ae782-124">Crie um serviço vinculado ao Azure HDInsight para vincular o cluster do Apache Spark no Azure HDInsight ao data factory.</span><span class="sxs-lookup"><span data-stu-id="ae782-124">Create an Azure HDInsight linked service to link your Apache Spark cluster in Azure HDInsight to the data factory.</span></span>
3. <span data-ttu-id="ae782-125">Crie um conjunto de dados que se refere ao serviço vinculado do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae782-125">Create a dataset that refers to the Azure Storage linked service.</span></span> <span data-ttu-id="ae782-126">No momento, você deve especificar um conjunto de dados de saída para uma atividade mesmo que não exista nenhuma saída sendo produzida.</span><span class="sxs-lookup"><span data-stu-id="ae782-126">Currently, you must specify an output dataset for an activity even if there is no output being produced.</span></span>  
4. <span data-ttu-id="ae782-127">Crie um pipeline com atividade do Spark que se refere ao serviço vinculado ao HDInsight criado na etapa 2.</span><span class="sxs-lookup"><span data-stu-id="ae782-127">Create a pipeline with Spark activity that refers to the HDInsight linked service created in #2.</span></span> <span data-ttu-id="ae782-128">A atividade está configurada com o conjunto de dados que você criou na etapa anterior como um conjunto de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="ae782-128">The activity is configured with the dataset you created in the previous step as an output dataset.</span></span> <span data-ttu-id="ae782-129">O conjunto de dados de saída é o que conduz a agenda (por hora, diariamente, etc.).</span><span class="sxs-lookup"><span data-stu-id="ae782-129">The output dataset is what drives the schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="ae782-130">Portanto, você deve especificar o conjunto de dados de saída mesmo que a atividade não produza efetivamente uma saída.</span><span class="sxs-lookup"><span data-stu-id="ae782-130">Therefore, you must specify the output dataset even though the activity does not really produce an output.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="ae782-131">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ae782-131">Prerequisites</span></span>
1. <span data-ttu-id="ae782-132">Criar uma **conta do Armazenamento do Azure para fins gerais** seguindo as instruções no passo a passo: [Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="ae782-132">Create a **general-purpose Azure Storage Account** by following instructions in the walkthrough: [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
2. <span data-ttu-id="ae782-133">Crie um **cluster do Apache Spark no Azure HDInsight** seguindo as instruções no tutorial: [Criar cluster do Apache Spark no Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="ae782-133">Create an **Apache Spark cluster in Azure HDInsight** by following instructions in the tutorial: [Create Apache Spark cluster in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="ae782-134">Associe a conta de armazenamento do Azure que você criou na etapa 1 a este cluster.</span><span class="sxs-lookup"><span data-stu-id="ae782-134">Associate the Azure storage account you created in step #1 with this cluster.</span></span>  
3. <span data-ttu-id="ae782-135">Baixe e leia o arquivo de script de python **test.py** localizado em: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span><span class="sxs-lookup"><span data-stu-id="ae782-135">Download and review the python script file **test.py** located at: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span></span>  
3.  <span data-ttu-id="ae782-136">Carregue **test.py** para a pasta **pyFiles** no contêiner **adfspark** em seu armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae782-136">Upload **test.py** to the **pyFiles** folder in the **adfspark** container in your Azure Blob storage.</span></span> <span data-ttu-id="ae782-137">Crie o contêiner e a pasta se eles não existirem.</span><span class="sxs-lookup"><span data-stu-id="ae782-137">Create the container and the folder if they do not exist.</span></span>

### <a name="create-data-factory"></a><span data-ttu-id="ae782-138">Criar um data factory</span><span class="sxs-lookup"><span data-stu-id="ae782-138">Create data factory</span></span>
<span data-ttu-id="ae782-139">Vamos começar com a criação do data factory nesta etapa.</span><span class="sxs-lookup"><span data-stu-id="ae782-139">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="ae782-140">Faça logon no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ae782-140">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ae782-141">Clique em **NOVO** no menu à esquerda, clique em **Dados + Analytics** e clique em **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="ae782-141">Click **NEW** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="ae782-142">Na folha **Novo data factory**, insira **SparkDF** como o Nome.</span><span class="sxs-lookup"><span data-stu-id="ae782-142">In the **New data factory** blade, enter **SparkDF** for the Name.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="ae782-143">O nome do Azure Data Factory deve ser **globalmente exclusivo**.</span><span class="sxs-lookup"><span data-stu-id="ae782-143">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="ae782-144">Se você vir o erro: **O nome do data factory "SparkDF" não está disponível**.</span><span class="sxs-lookup"><span data-stu-id="ae782-144">If you see the error: **Data factory name “SparkDF” is not available**.</span></span> <span data-ttu-id="ae782-145">Altere o nome do data factory (por exemplo, seunomeSparkDF) e tente criar novamente.</span><span class="sxs-lookup"><span data-stu-id="ae782-145">Change the name of the data factory (for example, yournameSparkDFdate, and try creating again.</span></span> <span data-ttu-id="ae782-146">Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ae782-146">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>   
4. <span data-ttu-id="ae782-147">Escolha a **assinatura do Azure** onde você deseja que o data factory seja criado.</span><span class="sxs-lookup"><span data-stu-id="ae782-147">Select the **Azure subscription** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="ae782-148">Selecione um **grupo de recursos** existente ou crie um grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae782-148">Select an existing **resource group** or create an Azure resource group.</span></span>
6. <span data-ttu-id="ae782-149">Selecione a opção **Fixar no painel**.</span><span class="sxs-lookup"><span data-stu-id="ae782-149">Select **Pin to dashboard** option.</span></span>  
6. <span data-ttu-id="ae782-150">Clique em **Criar** na folha **Novo data factory**.</span><span class="sxs-lookup"><span data-stu-id="ae782-150">Click **Create** on the **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="ae782-151">Para criar instâncias de Data Factory, você deve ser um membro da função [Colaborador de Data Factory](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) no nível de assinatura/grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ae782-151">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
7. <span data-ttu-id="ae782-152">Você verá o data factory que está sendo criado no **painel** do portal do Azure da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="ae782-152">You see the data factory being created in the **dashboard** of the Azure portal as follows:</span></span>   
8. <span data-ttu-id="ae782-153">Após o data factory ter sido criado com êxito, você verá a página do data factory, que exibe seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="ae782-153">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span> <span data-ttu-id="ae782-154">Se você não vir a página do data factory, clique no bloco da sua data factory no painel.</span><span class="sxs-lookup"><span data-stu-id="ae782-154">If you do not see the data factory page, click the tile for your data factory on the dashboard.</span></span>

    ![Folha Data Factory](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a><span data-ttu-id="ae782-156">Criar serviços vinculados</span><span class="sxs-lookup"><span data-stu-id="ae782-156">Create linked services</span></span>
<span data-ttu-id="ae782-157">Nesta etapa, você deve criar dois serviços vinculados, um para vincular seu cluster do Spark a sua data factory e outro para vincular seu armazenamento do Azure a sua data factory.</span><span class="sxs-lookup"><span data-stu-id="ae782-157">In this step, you create two linked services, one to link your Spark cluster to your data factory, and the other to link your Azure storage to your data factory.</span></span>  

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="ae782-158">Criar o serviço vinculado do armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ae782-158">Create Azure Storage linked service</span></span>
<span data-ttu-id="ae782-159">Nesta etapa, você vincula a conta do Armazenamento do Azure ao data factory.</span><span class="sxs-lookup"><span data-stu-id="ae782-159">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="ae782-160">Um conjunto de dados que você cria em uma etapa posterior neste passo a passo refere-se a esse serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="ae782-160">A dataset you create in a step later in this walkthrough refers to this linked service.</span></span> <span data-ttu-id="ae782-161">O serviço vinculado HDInsight que você define na próxima etapa também se refere a esse serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="ae782-161">The HDInsight linked service that you define in the next step refers to this linked service too.</span></span>  

1. <span data-ttu-id="ae782-162">Clique em **Criar e implantar** na folha **Data Factory** para seu data factory.</span><span class="sxs-lookup"><span data-stu-id="ae782-162">Click **Author and deploy** on the **Data Factory** blade for your data factory.</span></span> <span data-ttu-id="ae782-163">Você deverá ver o Data Factory Editor.</span><span class="sxs-lookup"><span data-stu-id="ae782-163">You should see the Data Factory Editor.</span></span>
2. <span data-ttu-id="ae782-164">Clique em **Novo repositório de dados** e escolha **Armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="ae782-164">Click **New data store** and choose **Azure storage**.</span></span>

   ![Novo armazenamento de dados - Armazenamento do Azure - menu](./media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="ae782-166">Você deve ver o **script JSON** para criar um serviço de armazenamento vinculado do Azure no editor.</span><span class="sxs-lookup"><span data-stu-id="ae782-166">You should see the **JSON script** for creating an Azure Storage linked service in the editor.</span></span>

   ![Serviço vinculado de armazenamento do Azure](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="ae782-168">Substitua **accountname** e **accountkey** pelo nome e pela chave de acesso da sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae782-168">Replace **account name** and **account key** with the name and access key of your Azure storage account.</span></span> <span data-ttu-id="ae782-169">Para saber como conseguir sua chave de acesso de armazenamento, consulte as informações sobre como exibir, copiar e regenerar chaves de acesso de armazenamento em [Gerenciar sua conta de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="ae782-169">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="ae782-170">Clique em **Implantar** na barra de comandos para implantar o serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="ae782-170">To deploy the linked service, click **Deploy** on the command bar.</span></span> <span data-ttu-id="ae782-171">Depois que o serviço vinculado for implantado com êxito, a janela **Rascunho-1** desaparecerá e você verá **AzureStorageLinkedService** no modo de exibição de árvore à esquerda.</span><span class="sxs-lookup"><span data-stu-id="ae782-171">After the linked service is deployed successfully, the **Draft-1** window should disappear and you see **AzureStorageLinkedService** in the tree view on the left.</span></span>

#### <a name="create-hdinsight-linked-service"></a><span data-ttu-id="ae782-172">Criar o serviço vinculado ao HDInsight</span><span class="sxs-lookup"><span data-stu-id="ae782-172">Create HDInsight linked service</span></span>
<span data-ttu-id="ae782-173">Nesta etapa, você cria um serviço vinculado ao Azure HDInsight para vincular seu cluster do HDInsight Spark ao data factory.</span><span class="sxs-lookup"><span data-stu-id="ae782-173">In this step, you create Azure HDInsight linked service to link your HDInsight Spark cluster to the data factory.</span></span> <span data-ttu-id="ae782-174">O cluster do HDInsight é usado para executar o programa especificado do Spark na atividade do Spark neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="ae782-174">The HDInsight cluster is used to run the Spark program specified in the Spark activity of the pipeline in this sample.</span></span>  

1. <span data-ttu-id="ae782-175">Clique em **... Mais** na barra de ferramentas, clique em **Nova computação** e, em seguida, clique em **Cluster do HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="ae782-175">Click **... More** on the toolbar, click **New compute**, and then click **HDInsight cluster**.</span></span>

    ![Criar o serviço vinculado ao HDInsight](media/data-factory-spark/new-hdinsight-linked-service.png)
2. <span data-ttu-id="ae782-177">Copie e cole o trecho a seguir na janela de **Rascunho-1** .</span><span class="sxs-lookup"><span data-stu-id="ae782-177">Copy and paste the following snippet to the **Draft-1** window.</span></span> <span data-ttu-id="ae782-178">No Editor JSON, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="ae782-178">In the JSON editor, do the following steps:</span></span>
    1. <span data-ttu-id="ae782-179">Especifique o **URI** para o cluster do HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="ae782-179">Specify the **URI** for the HDInsight Spark cluster.</span></span> <span data-ttu-id="ae782-180">Por exemplo: `https://<sparkclustername>.azurehdinsight.net/`.</span><span class="sxs-lookup"><span data-stu-id="ae782-180">For example: `https://<sparkclustername>.azurehdinsight.net/`.</span></span>
    2. <span data-ttu-id="ae782-181">Especifique o nome do **usuário** que tem acesso ao cluster do Spark.</span><span class="sxs-lookup"><span data-stu-id="ae782-181">Specify the name of the **user** who has access to the Spark cluster.</span></span>
    3. <span data-ttu-id="ae782-182">Especifique a **senha** para o usuário.</span><span class="sxs-lookup"><span data-stu-id="ae782-182">Specify the **password** for user.</span></span>
    4. <span data-ttu-id="ae782-183">Especifique o **serviço vinculado ao Armazenamento do Azure** que está associado ao cluster do HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="ae782-183">Specify the **Azure Storage linked service** that is associated with the HDInsight Spark cluster.</span></span> <span data-ttu-id="ae782-184">Neste exemplo, é: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="ae782-184">In this example, it is: **AzureStorageLinkedService**.</span></span>

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
    > - <span data-ttu-id="ae782-185">A atividade do Spark não oferece suporte a clusters HDInsight Spark que usam um Azure Data Lake Store como armazenamento primário.</span><span class="sxs-lookup"><span data-stu-id="ae782-185">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
    > - <span data-ttu-id="ae782-186">A atividade do Spark dá suporte apenas ao cluster HDInsight Spark existente (seu próprio).</span><span class="sxs-lookup"><span data-stu-id="ae782-186">Spark Activity supports only existing (your own) HDInsight Spark cluster.</span></span> <span data-ttu-id="ae782-187">Ele não dá suporte a serviço vinculado ao HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="ae782-187">It does not support an on-demand HDInsight linked service.</span></span>

    <span data-ttu-id="ae782-188">Consulte [Serviço vinculado ao HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) para obter detalhes sobre o serviço vinculado ao HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ae782-188">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details about the HDInsight linked service.</span></span>
3.  <span data-ttu-id="ae782-189">Clique em **Implantar** na barra de comandos para implantar o serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="ae782-189">To deploy the linked service, click **Deploy** on the command bar.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="ae782-190">Criar conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="ae782-190">Create output dataset</span></span>
<span data-ttu-id="ae782-191">O conjunto de dados de saída é o que conduz a agenda (por hora, diariamente, etc.).</span><span class="sxs-lookup"><span data-stu-id="ae782-191">The output dataset is what drives the schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="ae782-192">Portanto, você deve especificar um conjunto de dados de saída para a atividade do Spark embora a atividade não produza efetivamente uma saída.</span><span class="sxs-lookup"><span data-stu-id="ae782-192">Therefore, you must specify an output dataset for the spark activity in the pipeline even though the activity does not really produce any output.</span></span> <span data-ttu-id="ae782-193">Especificar um conjunto de dados de entrada para a atividade é opcional.</span><span class="sxs-lookup"><span data-stu-id="ae782-193">Specifying an input dataset for the activity is optional.</span></span>

1. <span data-ttu-id="ae782-194">No **Editor de Data Factory**, clique em **... Mais** na barra de comandos, clique em **Novo conjunto de dados** e selecione **Armazenamento de Blobs do Azure**.</span><span class="sxs-lookup"><span data-stu-id="ae782-194">In the **Data Factory Editor**, click **... More** on the command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="ae782-195">Copie e cole o trecho a seguir na janela de Rascunho-1.</span><span class="sxs-lookup"><span data-stu-id="ae782-195">Copy and paste the following snippet to the Draft-1 window.</span></span> <span data-ttu-id="ae782-196">O trecho JSON define um conjunto de dados chamado **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="ae782-196">The JSON snippet defines a dataset called **OutputDataset**.</span></span> <span data-ttu-id="ae782-197">Além disso, você especifica que os resultados estão armazenados no contêiner de blobs denominado **adfspark** e na pasta denominada **pyFiles/output**.</span><span class="sxs-lookup"><span data-stu-id="ae782-197">In addition, you specify that the results are stored in the blob container called **adfspark** and the folder called **pyFiles/output**.</span></span> <span data-ttu-id="ae782-198">Como mencionado anteriormente, esse conjunto de dados é fictício.</span><span class="sxs-lookup"><span data-stu-id="ae782-198">As mentioned earlier, this dataset is a dummy dataset.</span></span> <span data-ttu-id="ae782-199">O programa Spark neste exemplo não produz saída.</span><span class="sxs-lookup"><span data-stu-id="ae782-199">The Spark program in this example does not produce any output.</span></span> <span data-ttu-id="ae782-200">A seção **availability** especifica que o conjunto de dados de saída é produzido diariamente.</span><span class="sxs-lookup"><span data-stu-id="ae782-200">The **availability** section specifies that the output dataset is produced daily.</span></span>  

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
3. <span data-ttu-id="ae782-201">Clique em **Implantar** na barra de comandos para implantar o conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="ae782-201">To deploy the dataset, click **Deploy** on the command bar.</span></span>


### <a name="create-pipeline"></a><span data-ttu-id="ae782-202">Criar um pipeline</span><span class="sxs-lookup"><span data-stu-id="ae782-202">Create pipeline</span></span>
<span data-ttu-id="ae782-203">Nesta etapa, você cria um pipeline com a atividade **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="ae782-203">In this step, you create a pipeline with a **HDInsightSpark** activity.</span></span> <span data-ttu-id="ae782-204">Atualmente, o conjunto de dados de saída é o que aciona a agenda, então você deve criar um conjunto de dados de saída, mesmo que a atividade não produza qualquer saída.</span><span class="sxs-lookup"><span data-stu-id="ae782-204">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="ae782-205">Se a atividade não receber entradas, ignore a criação de conjunto de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="ae782-205">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> <span data-ttu-id="ae782-206">Portanto, nenhum conjunto de dados de entrada é especificado neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="ae782-206">Therefore, no input dataset is specified in this example.</span></span>

1. <span data-ttu-id="ae782-207">No **Editor de Data Factory**, clique em **... Mais** na barra de comandos e, em seguida, clique em **Novo pipeline**.</span><span class="sxs-lookup"><span data-stu-id="ae782-207">In the **Data Factory Editor**, click **… More** on the command bar, and then click **New pipeline**.</span></span>
2. <span data-ttu-id="ae782-208">Substitua o script na janela de Rascunho-1 pelo seguinte script:</span><span class="sxs-lookup"><span data-stu-id="ae782-208">Replace the script in the Draft-1 window with the following script:</span></span>

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
    <span data-ttu-id="ae782-209">Observe os seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="ae782-209">Note the following points:</span></span>
    - <span data-ttu-id="ae782-210">A propriedade **type** é definida como **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="ae782-210">The **type** property is set to **HDInsightSpark**.</span></span>
    - <span data-ttu-id="ae782-211">O **rootPath** é definido como **adfspark\\pyFiles**, onde adfspark é o contêiner de Blob do Azure e pyFiles é a pasta de arquivos nesse contêiner.</span><span class="sxs-lookup"><span data-stu-id="ae782-211">The **rootPath** is set to **adfspark\\pyFiles** where adfspark is the Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="ae782-212">Neste exemplo, o Armazenamento de Blobs do Azure é aquele que está associado ao cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="ae782-212">In this example, the Azure Blob Storage is the one that is associated with the Spark cluster.</span></span> <span data-ttu-id="ae782-213">Você pode carregar o arquivo em um Armazenamento do Azure diferente.</span><span class="sxs-lookup"><span data-stu-id="ae782-213">You can upload the file to a different Azure Storage.</span></span> <span data-ttu-id="ae782-214">Se você fizer isso, crie um serviço vinculado do Armazenamento do Azure para vincular essa conta de armazenamento ao data factory.</span><span class="sxs-lookup"><span data-stu-id="ae782-214">If you do so, create an Azure Storage linked service to link that storage account to the data factory.</span></span> <span data-ttu-id="ae782-215">Em seguida, especifique o nome do serviço vinculado como um valor para a propriedade **sparkJobLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="ae782-215">Then, specify the name of the linked service as a value for the **sparkJobLinkedService** property.</span></span> <span data-ttu-id="ae782-216">Consulte [Propriedades de Atividade Spark](#spark-activity-properties) para obter detalhes sobre essa propriedade e outras propriedades às quais a atividade Spark dá suporte.</span><span class="sxs-lookup"><span data-stu-id="ae782-216">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by the Spark Activity.</span></span>  
    - <span data-ttu-id="ae782-217">O **entryFilePath** é definido como **test.py**, que é o arquivo Python.</span><span class="sxs-lookup"><span data-stu-id="ae782-217">The **entryFilePath** is set to the **test.py**, which is the python file.</span></span>
    - <span data-ttu-id="ae782-218">A propriedade **getDebugInfo** é definida como **Always**, o que significa que os arquivos de log são gerados sempre (êxito ou falha).</span><span class="sxs-lookup"><span data-stu-id="ae782-218">The **getDebugInfo** property is set to **Always**, which means the log files are always generated (success or failure).</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="ae782-219">É recomendável que você não defina essa propriedade como `Always` em um ambiente de produção a menos que você esteja solucionando um problema.</span><span class="sxs-lookup"><span data-stu-id="ae782-219">We recommend that you do not set this property to `Always` in a production environment unless you are troubleshooting an issue.</span></span>
    - <span data-ttu-id="ae782-220">A seção de **saídas** tem um conjunto de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="ae782-220">The **outputs** section has one output dataset.</span></span> <span data-ttu-id="ae782-221">Você deve especificar um conjunto de dados de saída mesmo que o programa spark não produza nenhuma saída.</span><span class="sxs-lookup"><span data-stu-id="ae782-221">You must specify an output dataset even if the spark program does not produce any output.</span></span> <span data-ttu-id="ae782-222">O conjunto de dados de saída conduz a agenda para o pipeline (por hora, diariamente, etc.).</span><span class="sxs-lookup"><span data-stu-id="ae782-222">The output dataset drives the schedule for the pipeline (hourly, daily, etc.).</span></span>  

        <span data-ttu-id="ae782-223">Para obter detalhes sobre as propriedades com suporte pela atividade do Spark, veja a seção [Propriedades da atividade do Spark](#spark-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ae782-223">For details about the properties supported by Spark activity, see [Spark activity properties](#spark-activity-properties) section.</span></span>
3. <span data-ttu-id="ae782-224">Para implantar o pipeline, clique em **Implantar** na barra de comando.</span><span class="sxs-lookup"><span data-stu-id="ae782-224">To deploy the pipeline, click **Deploy** on the command bar.</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="ae782-225">Monitorar o pipeline</span><span class="sxs-lookup"><span data-stu-id="ae782-225">Monitor pipeline</span></span>
1. <span data-ttu-id="ae782-226">Clique em **X** para fechar as folhas do Editor da Fábrica de Dados e para navegar de volta à página inicial da Fábrica de Dados.</span><span class="sxs-lookup"><span data-stu-id="ae782-226">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory home page.</span></span> <span data-ttu-id="ae782-227">Clique em **Monitorar e Gerenciar** para iniciar o aplicativo de monitoramento em outra guia.</span><span class="sxs-lookup"><span data-stu-id="ae782-227">Click **Monitor and Manage** to launch the monitoring application in another tab.</span></span>

    ![Bloco Monitorar e Gerenciar](media/data-factory-spark/monitor-and-manage-tile.png)
2. <span data-ttu-id="ae782-229">Altere o filtro **Hora de início** na parte superior para **1/2/2017** e clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="ae782-229">Change the **Start time** filter at the top to **2/1/2017**, and click **Apply**.</span></span>
3. <span data-ttu-id="ae782-230">Você verá apenas uma janela de atividade porque há apenas um dia entre a hora de início (2017-02-01) e a final (2017-02-02) do pipeline.</span><span class="sxs-lookup"><span data-stu-id="ae782-230">You should see only one activity window as there is only one day between the start (2017-02-01) and end times (2017-02-02) of the pipeline.</span></span> <span data-ttu-id="ae782-231">Confirme se a fatia de dados está no estado **Pronto**.</span><span class="sxs-lookup"><span data-stu-id="ae782-231">Confirm that the data slice is in **ready** state.</span></span>

    ![Monitorar o Pipeline](media/data-factory-spark/monitor-and-manage-app.png)    
4. <span data-ttu-id="ae782-233">Selecione a **janela de atividade** para ver detalhes sobre a execução da atividade.</span><span class="sxs-lookup"><span data-stu-id="ae782-233">Select the **activity window** to see details about the activity run.</span></span> <span data-ttu-id="ae782-234">Se houver um erro, você verá detalhes sobre ele no painel à direita.</span><span class="sxs-lookup"><span data-stu-id="ae782-234">If there is an error, you see details about it in the right pane.</span></span>

### <a name="verify-the-results"></a><span data-ttu-id="ae782-235">Verifique os resultados</span><span class="sxs-lookup"><span data-stu-id="ae782-235">Verify the results</span></span>

1. <span data-ttu-id="ae782-236">Inicie o **Notebook Jupyter** para seu cluster do HDInsight Spark, navegando até: https://NOMEDOCLUSTER.azurehdinsight.net/jupyter.</span><span class="sxs-lookup"><span data-stu-id="ae782-236">Launch **Jupyter notebook** for your HDInsight Spark cluster by navigating to: https://CLUSTERNAME.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="ae782-237">Você pode também iniciar o painel do cluster para o cluster do HDInsight Spark e, em seguida, iniciar **Notebook Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="ae782-237">You can also launch cluster dashboard for your HDInsight Spark cluster, and then launch **Jupyter Notebook**.</span></span>
2. <span data-ttu-id="ae782-238">Clique em **Novo** -> **PySpark** para iniciar um novo notebook.</span><span class="sxs-lookup"><span data-stu-id="ae782-238">Click **New** -> **PySpark** to start a new notebook.</span></span>

    ![Novo notebook Jupyter](media/data-factory-spark/jupyter-new-book.png)
3. <span data-ttu-id="ae782-240">Execute o seguinte comando copiando/colando o texto e pressionando **SHIFT + ENTER** no final da segunda instrução.</span><span class="sxs-lookup"><span data-stu-id="ae782-240">Run the following command by copy/pasting the text and pressing **SHIFT + ENTER** at the end of the second statement.</span></span>  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. <span data-ttu-id="ae782-241">Confirme que você vê os dados da tabela de hvac:</span><span class="sxs-lookup"><span data-stu-id="ae782-241">Confirm that you see the data from the hvac table:</span></span>  

    ![Resultados da consulta do Jupyter](media/data-factory-spark/jupyter-notebook-results.png)

<span data-ttu-id="ae782-243">Veja a seção [Executar uma consulta SQL do Spark](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) para obter instruções detalhadas.</span><span class="sxs-lookup"><span data-stu-id="ae782-243">See [Run a Spark SQL query](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) section for detailed instructions.</span></span> 

### <a name="troubleshooting"></a><span data-ttu-id="ae782-244">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="ae782-244">Troubleshooting</span></span>
<span data-ttu-id="ae782-245">Como você define **getDebugInfo** para **Sempre**, verá uma subpasta **log** na pasta **pyFiles** em seu contêiner de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae782-245">Since you set **getDebugInfo** to **Always**, you see a **log** subfolder in the **pyFiles** folder in your Azure Blob container.</span></span> <span data-ttu-id="ae782-246">O arquivo de log na pasta de log fornece detalhes adicionais.</span><span class="sxs-lookup"><span data-stu-id="ae782-246">The log file in the log folder provides additional details.</span></span> <span data-ttu-id="ae782-247">Esse arquivo de log é especialmente útil quando há um erro.</span><span class="sxs-lookup"><span data-stu-id="ae782-247">This log file is especially useful when there is an error.</span></span> <span data-ttu-id="ae782-248">Em um ambiente de produção, convém defini-lo como **Falha**.</span><span class="sxs-lookup"><span data-stu-id="ae782-248">In a production environment, you may want to set it to **Failure**.</span></span>

<span data-ttu-id="ae782-249">Para solução de problemas adicionais, siga as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ae782-249">For further troubleshooting, do the following steps:</span></span>


1. <span data-ttu-id="ae782-250">Navegue até `https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span><span class="sxs-lookup"><span data-stu-id="ae782-250">Navigate to `https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span></span>

    ![Aplicativo de interface do usuário do YARN](media/data-factory-spark/yarnui-application.png)  
2. <span data-ttu-id="ae782-252">Clique em **Logs** para uma das tentativas de execução.</span><span class="sxs-lookup"><span data-stu-id="ae782-252">Click **Logs** for one of the run attempts.</span></span>

    ![Página do aplicativo](media/data-factory-spark/yarn-applications.png)
3. <span data-ttu-id="ae782-254">Você deve ver as informações de erro adicionais na página de logs.</span><span class="sxs-lookup"><span data-stu-id="ae782-254">You should see additional error information in the log page.</span></span>

    ![Log de erros](media/data-factory-spark/yarnui-application-error.png)

<span data-ttu-id="ae782-256">As seções a seguir fornecem informações sobre entidades de Data Factory para usar o cluster do Apache Spark e atividade do Spark na data factory.</span><span class="sxs-lookup"><span data-stu-id="ae782-256">The following sections provide information about Data Factory entities to use Apache Spark cluster and Spark Activity in your data factory.</span></span>

## <a name="spark-activity-properties"></a><span data-ttu-id="ae782-257">Propriedades da Atividade do Spark</span><span class="sxs-lookup"><span data-stu-id="ae782-257">Spark activity properties</span></span>
<span data-ttu-id="ae782-258">Esta é a definição JSON de exemplo de um pipeline com atividade do Spark:</span><span class="sxs-lookup"><span data-stu-id="ae782-258">Here is the sample JSON definition of a pipeline with Spark Activity:</span></span>    

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
                "description": "This activity invokes the Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

<span data-ttu-id="ae782-259">A tabela a seguir descreve as propriedades JSON usadas na definição de JSON:</span><span class="sxs-lookup"><span data-stu-id="ae782-259">The following table describes the JSON properties used in the JSON definition:</span></span>

| <span data-ttu-id="ae782-260">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ae782-260">Property</span></span> | <span data-ttu-id="ae782-261">Descrição</span><span class="sxs-lookup"><span data-stu-id="ae782-261">Description</span></span> | <span data-ttu-id="ae782-262">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ae782-262">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="ae782-263">name</span><span class="sxs-lookup"><span data-stu-id="ae782-263">name</span></span> | <span data-ttu-id="ae782-264">Nome da atividade no pipeline.</span><span class="sxs-lookup"><span data-stu-id="ae782-264">Name of the activity in the pipeline.</span></span> | <span data-ttu-id="ae782-265">Sim</span><span class="sxs-lookup"><span data-stu-id="ae782-265">Yes</span></span> |
| <span data-ttu-id="ae782-266">description</span><span class="sxs-lookup"><span data-stu-id="ae782-266">description</span></span> | <span data-ttu-id="ae782-267">Texto que descreve o que a atividade faz.</span><span class="sxs-lookup"><span data-stu-id="ae782-267">Text describing what the activity does.</span></span> | <span data-ttu-id="ae782-268">Não</span><span class="sxs-lookup"><span data-stu-id="ae782-268">No</span></span> |
| <span data-ttu-id="ae782-269">type</span><span class="sxs-lookup"><span data-stu-id="ae782-269">type</span></span> | <span data-ttu-id="ae782-270">Essa propriedade deve ser definida como HDInsightSpark.</span><span class="sxs-lookup"><span data-stu-id="ae782-270">This property must be set to HDInsightSpark.</span></span> | <span data-ttu-id="ae782-271">Sim</span><span class="sxs-lookup"><span data-stu-id="ae782-271">Yes</span></span> |
| <span data-ttu-id="ae782-272">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="ae782-272">linkedServiceName</span></span> | <span data-ttu-id="ae782-273">Nome do serviço vinculado do HDInsight no qual o programa Spark é executado.</span><span class="sxs-lookup"><span data-stu-id="ae782-273">Name of the HDInsight linked service on which the Spark program runs.</span></span> | <span data-ttu-id="ae782-274">Sim</span><span class="sxs-lookup"><span data-stu-id="ae782-274">Yes</span></span> |
| <span data-ttu-id="ae782-275">rootPath</span><span class="sxs-lookup"><span data-stu-id="ae782-275">rootPath</span></span> | <span data-ttu-id="ae782-276">O contêiner de Blob do Azure e a pasta que contém o arquivo Spark.</span><span class="sxs-lookup"><span data-stu-id="ae782-276">The Azure Blob container and folder that contains the Spark file.</span></span> <span data-ttu-id="ae782-277">O nome do arquivo diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="ae782-277">The file name is case-sensitive.</span></span> | <span data-ttu-id="ae782-278">Sim</span><span class="sxs-lookup"><span data-stu-id="ae782-278">Yes</span></span> |
| <span data-ttu-id="ae782-279">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="ae782-279">entryFilePath</span></span> | <span data-ttu-id="ae782-280">Caminho relativo à pasta raiz do código/pacote Spark.</span><span class="sxs-lookup"><span data-stu-id="ae782-280">Relative path to the root folder of the Spark code/package.</span></span> | <span data-ttu-id="ae782-281">Sim</span><span class="sxs-lookup"><span data-stu-id="ae782-281">Yes</span></span> |
| <span data-ttu-id="ae782-282">className</span><span class="sxs-lookup"><span data-stu-id="ae782-282">className</span></span> | <span data-ttu-id="ae782-283">Classe principal de Java/Spark do aplicativo</span><span class="sxs-lookup"><span data-stu-id="ae782-283">Application's Java/Spark main class</span></span> | <span data-ttu-id="ae782-284">Não</span><span class="sxs-lookup"><span data-stu-id="ae782-284">No</span></span> |
| <span data-ttu-id="ae782-285">argumentos</span><span class="sxs-lookup"><span data-stu-id="ae782-285">arguments</span></span> | <span data-ttu-id="ae782-286">Uma lista de argumentos de linha de comando para o programa Spark.</span><span class="sxs-lookup"><span data-stu-id="ae782-286">A list of command-line arguments to the Spark program.</span></span> | <span data-ttu-id="ae782-287">Não</span><span class="sxs-lookup"><span data-stu-id="ae782-287">No</span></span> |
| <span data-ttu-id="ae782-288">proxyUser</span><span class="sxs-lookup"><span data-stu-id="ae782-288">proxyUser</span></span> | <span data-ttu-id="ae782-289">A conta de usuário a ser representada para execução do programa Spark</span><span class="sxs-lookup"><span data-stu-id="ae782-289">The user account to impersonate to execute the Spark program</span></span> | <span data-ttu-id="ae782-290">Não</span><span class="sxs-lookup"><span data-stu-id="ae782-290">No</span></span> |
| <span data-ttu-id="ae782-291">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="ae782-291">sparkConfig</span></span> | <span data-ttu-id="ae782-292">Especifique valores para propriedades de configuração do Spark listadas no tópico: [Configuração do Spark – Propriedades de aplicativo](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span><span class="sxs-lookup"><span data-stu-id="ae782-292">Specify values for Spark configuration properties listed in the topic: [Spark Configuration - Application properties](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span></span> | <span data-ttu-id="ae782-293">Não</span><span class="sxs-lookup"><span data-stu-id="ae782-293">No</span></span> |
| <span data-ttu-id="ae782-294">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="ae782-294">getDebugInfo</span></span> | <span data-ttu-id="ae782-295">Especifica quando os arquivos de log do Spark são copiados no armazenamento do Azure usado pelo cluster HDInsight (ou) especificado por sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="ae782-295">Specifies when the Spark log files are copied to the Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="ae782-296">Valores permitidos: Nenhum, Sempre ou Falha.</span><span class="sxs-lookup"><span data-stu-id="ae782-296">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="ae782-297">Valor padrão: Nenhum.</span><span class="sxs-lookup"><span data-stu-id="ae782-297">Default value: None.</span></span> | <span data-ttu-id="ae782-298">Não</span><span class="sxs-lookup"><span data-stu-id="ae782-298">No</span></span> |
| <span data-ttu-id="ae782-299">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="ae782-299">sparkJobLinkedService</span></span> | <span data-ttu-id="ae782-300">O serviço vinculado ao Armazenamento do Azure que contém o arquivo de trabalho, dependências e os logs do Spark.</span><span class="sxs-lookup"><span data-stu-id="ae782-300">The Azure Storage linked service that holds the Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="ae782-301">Se você não especificar um valor para essa propriedade, o armazenamento associado ao cluster HDInsight será usado.</span><span class="sxs-lookup"><span data-stu-id="ae782-301">If you do not specify a value for this property, the storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="ae782-302">Não</span><span class="sxs-lookup"><span data-stu-id="ae782-302">No</span></span> |

## <a name="folder-structure"></a><span data-ttu-id="ae782-303">Estrutura de pastas</span><span class="sxs-lookup"><span data-stu-id="ae782-303">Folder structure</span></span>
<span data-ttu-id="ae782-304">A atividade do Spark não oferece suporte a um script em linha, como o fazem as atividades do Pig e do Hive.</span><span class="sxs-lookup"><span data-stu-id="ae782-304">The Spark activity does not support an in-line script as Pig and Hive activities do.</span></span> <span data-ttu-id="ae782-305">Os trabalhos do Spark também são mais extensíveis do que trabalhos do Pig/Hive.</span><span class="sxs-lookup"><span data-stu-id="ae782-305">Spark jobs are also more extensible than Pig/Hive jobs.</span></span> <span data-ttu-id="ae782-306">Para trabalhos do Spark, você pode fornecer várias dependências, como pacotes jar (colocados no CLASSPATH de java), arquivos do python (colocados no PYTHONPATH) e outros arquivos.</span><span class="sxs-lookup"><span data-stu-id="ae782-306">For Spark jobs, you can provide multiple dependencies such as jar packages (placed in the java CLASSPATH), python files (placed on the PYTHONPATH), and any other files.</span></span>

<span data-ttu-id="ae782-307">Crie a seguinte estrutura de pastas no armazenamento de Blobs do Azure referenciado pelo serviço vinculado ao HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ae782-307">Create the following folder structure in the Azure Blob storage referenced by the HDInsight linked service.</span></span> <span data-ttu-id="ae782-308">Depois, carregue os arquivos dependentes nas subpastas apropriadas na pasta raiz, representada por **entryFilePath**.</span><span class="sxs-lookup"><span data-stu-id="ae782-308">Then, upload dependent files to the appropriate sub folders in the root folder represented by **entryFilePath**.</span></span> <span data-ttu-id="ae782-309">Por exemplo, carregue arquivos do python na subpasta pyFiles e os arquivos jar na subpasta jars da pasta raiz.</span><span class="sxs-lookup"><span data-stu-id="ae782-309">For example, upload python files to the pyFiles subfolder and jar files to the jars subfolder of the root folder.</span></span> <span data-ttu-id="ae782-310">Em tempo de execução, o serviço Data Factory espera a seguinte estrutura de pastas no Armazenamento de Blobs do Azure:</span><span class="sxs-lookup"><span data-stu-id="ae782-310">At runtime, Data Factory service expects the following folder structure in the Azure Blob storage:</span></span>     

| <span data-ttu-id="ae782-311">Caminho</span><span class="sxs-lookup"><span data-stu-id="ae782-311">Path</span></span> | <span data-ttu-id="ae782-312">Descrição</span><span class="sxs-lookup"><span data-stu-id="ae782-312">Description</span></span> | <span data-ttu-id="ae782-313">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ae782-313">Required</span></span> | <span data-ttu-id="ae782-314">Tipo</span><span class="sxs-lookup"><span data-stu-id="ae782-314">Type</span></span> |
| ---- | ----------- | -------- | ---- |
| <span data-ttu-id="ae782-315">.</span><span class="sxs-lookup"><span data-stu-id="ae782-315">.</span></span> | <span data-ttu-id="ae782-316">O caminho raiz do trabalho do Spark no serviço vinculado ao armazenamento</span><span class="sxs-lookup"><span data-stu-id="ae782-316">The root path of the Spark job in the storage linked service</span></span>  | <span data-ttu-id="ae782-317">Sim</span><span class="sxs-lookup"><span data-stu-id="ae782-317">Yes</span></span> | <span data-ttu-id="ae782-318">Pasta</span><span class="sxs-lookup"><span data-stu-id="ae782-318">Folder</span></span> |
| <span data-ttu-id="ae782-319">&lt;definido pelo usuário&gt;</span><span class="sxs-lookup"><span data-stu-id="ae782-319">&lt;user defined &gt;</span></span> | <span data-ttu-id="ae782-320">O caminho que aponta para o arquivo de entrada do trabalho do Spark</span><span class="sxs-lookup"><span data-stu-id="ae782-320">The path pointing to the entry file of the Spark job</span></span> | <span data-ttu-id="ae782-321">Sim</span><span class="sxs-lookup"><span data-stu-id="ae782-321">Yes</span></span> | <span data-ttu-id="ae782-322">Arquivo</span><span class="sxs-lookup"><span data-stu-id="ae782-322">File</span></span> |
| <span data-ttu-id="ae782-323">./jars</span><span class="sxs-lookup"><span data-stu-id="ae782-323">./jars</span></span> | <span data-ttu-id="ae782-324">Todos os arquivos nessa pasta são carregados e colocados no classpath de java do cluster</span><span class="sxs-lookup"><span data-stu-id="ae782-324">All files under this folder are uploaded and placed on the java classpath of the cluster</span></span> | <span data-ttu-id="ae782-325">Não</span><span class="sxs-lookup"><span data-stu-id="ae782-325">No</span></span> | <span data-ttu-id="ae782-326">Pasta</span><span class="sxs-lookup"><span data-stu-id="ae782-326">Folder</span></span> |
| <span data-ttu-id="ae782-327">./pyFiles</span><span class="sxs-lookup"><span data-stu-id="ae782-327">./pyFiles</span></span> | <span data-ttu-id="ae782-328">Todos os arquivos nessa pasta são carregados e colocados no PYTHONPATH do cluster</span><span class="sxs-lookup"><span data-stu-id="ae782-328">All files under this folder are uploaded and placed on the PYTHONPATH of the cluster</span></span> | <span data-ttu-id="ae782-329">Não</span><span class="sxs-lookup"><span data-stu-id="ae782-329">No</span></span> | <span data-ttu-id="ae782-330">Pasta</span><span class="sxs-lookup"><span data-stu-id="ae782-330">Folder</span></span> |
| <span data-ttu-id="ae782-331">./files</span><span class="sxs-lookup"><span data-stu-id="ae782-331">./files</span></span> | <span data-ttu-id="ae782-332">Todos os arquivos nessa pasta são carregados e colocados no diretório de trabalho executor</span><span class="sxs-lookup"><span data-stu-id="ae782-332">All files under this folder are uploaded and placed on executor working directory</span></span> | <span data-ttu-id="ae782-333">Não</span><span class="sxs-lookup"><span data-stu-id="ae782-333">No</span></span> | <span data-ttu-id="ae782-334">Pasta</span><span class="sxs-lookup"><span data-stu-id="ae782-334">Folder</span></span> |
| <span data-ttu-id="ae782-335">./archives</span><span class="sxs-lookup"><span data-stu-id="ae782-335">./archives</span></span> | <span data-ttu-id="ae782-336">Todos os arquivos nessa pasta são descompactados</span><span class="sxs-lookup"><span data-stu-id="ae782-336">All files under this folder are uncompressed</span></span> | <span data-ttu-id="ae782-337">Não</span><span class="sxs-lookup"><span data-stu-id="ae782-337">No</span></span> | <span data-ttu-id="ae782-338">Pasta</span><span class="sxs-lookup"><span data-stu-id="ae782-338">Folder</span></span> |
| <span data-ttu-id="ae782-339">./logs</span><span class="sxs-lookup"><span data-stu-id="ae782-339">./logs</span></span> | <span data-ttu-id="ae782-340">A pasta onde os logs do cluster Spark são armazenados.</span><span class="sxs-lookup"><span data-stu-id="ae782-340">The folder where logs from the Spark cluster are stored.</span></span>| <span data-ttu-id="ae782-341">Não</span><span class="sxs-lookup"><span data-stu-id="ae782-341">No</span></span> | <span data-ttu-id="ae782-342">Pasta</span><span class="sxs-lookup"><span data-stu-id="ae782-342">Folder</span></span> |

<span data-ttu-id="ae782-343">Veja um exemplo de um armazenamento que contém dois arquivos de trabalho do Spark no Armazenamento de Blobs do Azure referenciado pelo serviço vinculado ao HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ae782-343">Here is an example for a storage containing two Spark job files in the Azure Blob Storage referenced by the HDInsight linked service.</span></span>

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
