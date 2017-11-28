---
title: Criar seu primeiro data factory (portal do Azure) | Microsoft Docs
description: "Neste tutorial, você cria um pipeline de exemplo do Azure Data Factory usando o Data Factory Editor no portal do Azure."
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
ms.openlocfilehash: 9c958aecb841fa02349c6b9e5e1984f6ba4fb611
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-portal"></a><span data-ttu-id="dd180-103">Tutorial: Compilar sua primeira Azure Data Factory usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="dd180-103">Tutorial: Build your first Azure data factory using Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dd180-104">Visão geral e pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="dd180-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="dd180-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="dd180-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="dd180-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dd180-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="dd180-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd180-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="dd180-108">Modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dd180-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="dd180-109">API REST</span><span class="sxs-lookup"><span data-stu-id="dd180-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)


<span data-ttu-id="dd180-110">Neste artigo, você aprende a usar o [portal do Azure](https://portal.azure.com/) para criar seu primeiro data factory do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd180-110">In this article, you learn how to use [Azure portal](https://portal.azure.com/) to create your first Azure data factory.</span></span> <span data-ttu-id="dd180-111">Para fazer o tutorial usando outras ferramentas/SDKs, selecione uma das opções da lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="dd180-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span></span> 

<span data-ttu-id="dd180-112">O pipeline neste tutorial tem uma atividade: **atividade hive do HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="dd180-112">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="dd180-113">Esta atividade executa um script de hive em um cluster do HDInsight do Azure que transforma os dados de entrada para gerar dados de saída.</span><span class="sxs-lookup"><span data-stu-id="dd180-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="dd180-114">O pipeline é agendado para ser executado uma vez por mês entre os horários de início e término especificados.</span><span class="sxs-lookup"><span data-stu-id="dd180-114">The pipeline is scheduled to run once a month between the specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="dd180-115">O pipeline de dados neste tutorial transforma os dados de entrada para gerar dados de saída.</span><span class="sxs-lookup"><span data-stu-id="dd180-115">The data pipeline in this tutorial transforms input data to produce output data.</span></span> <span data-ttu-id="dd180-116">Para obter um tutorial sobre como copiar dados usando o Azure Data Factory, confira [Tutorial: copiar dados do armazenamento de blobs para um banco de dados SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="dd180-116">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="dd180-117">Um pipeline pode ter mais de uma atividade.</span><span class="sxs-lookup"><span data-stu-id="dd180-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="dd180-118">E você pode encadear duas atividades (executar uma atividade após a outra) definindo o conjunto de dados de saída de uma atividade como o conjunto de dados de entrada da outra atividade.</span><span class="sxs-lookup"><span data-stu-id="dd180-118">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="dd180-119">Para saber mais, confira [Agendamento e execução no Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="dd180-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd180-120">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="dd180-120">Prerequisites</span></span>
1. <span data-ttu-id="dd180-121">Leia o artigo [Visão geral do tutorial](data-factory-build-your-first-pipeline.md) e concluir as etapas de **pré-requisito** .</span><span class="sxs-lookup"><span data-stu-id="dd180-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span>
2. <span data-ttu-id="dd180-122">Este artigo não fornece uma visão geral conceitual do serviço Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="dd180-122">This article does not provide a conceptual overview of the Azure Data Factory service.</span></span> <span data-ttu-id="dd180-123">Nós recomendamos que você veja o artigo [Introdução ao Azure Data Factory](data-factory-introduction.md) para obter uma visão geral detalhada do serviço.</span><span class="sxs-lookup"><span data-stu-id="dd180-123">We recommend that you go through [Introduction to Azure Data Factory](data-factory-introduction.md) article for a detailed overview of the service.</span></span>  

## <a name="create-data-factory"></a><span data-ttu-id="dd180-124">Criar um data factory</span><span class="sxs-lookup"><span data-stu-id="dd180-124">Create data factory</span></span>
<span data-ttu-id="dd180-125">Uma fábrica de dados pode ter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="dd180-125">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="dd180-126">Um pipeline em um data factory pode ter uma ou mais atividades.</span><span class="sxs-lookup"><span data-stu-id="dd180-126">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="dd180-127">Por exemplo, uma Atividade de Cópia para copiar dados de um armazenamento de dados de origem para um de destino e uma atividade do Hive do HDInsight para executar um script do Hive para transformar os dados de entrada em dados de saída do produto.</span><span class="sxs-lookup"><span data-stu-id="dd180-127">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data to product output data.</span></span> <span data-ttu-id="dd180-128">Vamos começar com a criação do data factory nesta etapa.</span><span class="sxs-lookup"><span data-stu-id="dd180-128">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="dd180-129">Faça logon no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="dd180-129">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="dd180-130">Clique em **NOVO** no menu à esquerda, clique em **Dados + Analytics** e clique em **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="dd180-130">Click **NEW** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>

   ![Folha Criar](./media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)
3. <span data-ttu-id="dd180-132">Na folha **Novo data factory**, insira **GetStartedDF** como o Nome.</span><span class="sxs-lookup"><span data-stu-id="dd180-132">In the **New data factory** blade, enter **GetStartedDF** for the Name.</span></span>

   ![Folha Nova data factory](./media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > <span data-ttu-id="dd180-134">O nome do Azure Data Factory deve ser **globalmente exclusivo**.</span><span class="sxs-lookup"><span data-stu-id="dd180-134">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="dd180-135">Se você receber o erro: **O nome do data factory "GetStartedDF" não está disponível**.</span><span class="sxs-lookup"><span data-stu-id="dd180-135">If you receive the error: **Data factory name “GetStartedDF” is not available**.</span></span> <span data-ttu-id="dd180-136">Altere o nome do data factory (por exemplo, seunomeGetStartedDF) e tente criar novamente.</span><span class="sxs-lookup"><span data-stu-id="dd180-136">Change the name of the data factory (for example, yournameGetStartedDF) and try creating again.</span></span> <span data-ttu-id="dd180-137">Veja o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="dd180-137">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
   >
   > <span data-ttu-id="dd180-138">O nome do data factory pode ser registrado futuramente como um nome **DNS** e tornar-se publicamente visível.</span><span class="sxs-lookup"><span data-stu-id="dd180-138">The name of the data factory may be registered as a **DNS** name in the future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="dd180-139">Escolha a **assinatura do Azure** onde você deseja que o data factory seja criado.</span><span class="sxs-lookup"><span data-stu-id="dd180-139">Select the **Azure subscription** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="dd180-140">Selecione um **grupo de recursos** existente ou crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="dd180-140">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="dd180-141">Para o tutorial, crie um grupo de recursos chamado: **ADFGetStartedRG**.</span><span class="sxs-lookup"><span data-stu-id="dd180-141">For the tutorial, create a resource group named: **ADFGetStartedRG**.</span></span>
6. <span data-ttu-id="dd180-142">Selecione o **local** do data factory.</span><span class="sxs-lookup"><span data-stu-id="dd180-142">Select the **location** for the data factory.</span></span> <span data-ttu-id="dd180-143">Apenas as regiões com suporte pelo serviço Data Factory são mostradas na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="dd180-143">Only regions supported by the Data Factory service are shown in the drop-down list.</span></span>
7. <span data-ttu-id="dd180-144">Selecione **Fixar no painel**.</span><span class="sxs-lookup"><span data-stu-id="dd180-144">Select **Pin to dashboard**.</span></span> 
8. <span data-ttu-id="dd180-145">Clique em **Criar** na folha **Novo data factory**.</span><span class="sxs-lookup"><span data-stu-id="dd180-145">Click **Create** on the **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="dd180-146">Para criar instâncias de Data Factory, você deve ser um membro da função [Colaborador de Data Factory](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) no nível de assinatura/grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="dd180-146">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="dd180-147">No painel, você vê o seguinte bloco com status: Implantando data factory.</span><span class="sxs-lookup"><span data-stu-id="dd180-147">On the dashboard, you see the following tile with status: Deploying data factory.</span></span>    

   ![Status da criação da data factory](./media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)
8. <span data-ttu-id="dd180-149">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="dd180-149">Congratulations!</span></span> <span data-ttu-id="dd180-150">Você criou com êxito sua primeira data factory.</span><span class="sxs-lookup"><span data-stu-id="dd180-150">You have successfully created your first data factory.</span></span> <span data-ttu-id="dd180-151">Após o data factory ter sido criado com êxito, você verá a página do data factory, que exibe seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="dd180-151">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span>     

    ![Folha Data Factory](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

<span data-ttu-id="dd180-153">Antes de criar um pipeline no data factory, primeiro você precisará criar algumas entidades do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="dd180-153">Before creating a pipeline in the data factory, you need to create a few Data Factory entities first.</span></span> <span data-ttu-id="dd180-154">Primeiro você cria serviços vinculados para vincular serviços de armazenamento/computação de dados ao seu armazenamento de dados, define conjuntos de dados de entrada/saída para representar os dados em armazenamentos de dados vinculados e, em seguida, cria o pipeline com uma atividade que utilize esses conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="dd180-154">You first create linked services to link data stores/computes to your data store, define input and output datasets to represent input/output data in linked data stores, and then create the pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="dd180-155">Criar serviços vinculados</span><span class="sxs-lookup"><span data-stu-id="dd180-155">Create linked services</span></span>
<span data-ttu-id="dd180-156">Nesta etapa, você vinculará sua conta do Armazenamento do Azure e um cluster do HDInsight do Azure sob demanda ao data factory.</span><span class="sxs-lookup"><span data-stu-id="dd180-156">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster to your data factory.</span></span> <span data-ttu-id="dd180-157">A conta do Armazenamento do Azure manterá os dados de entrada e de saída para o pipeline neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="dd180-157">The Azure Storage account holds the input and output data for the pipeline in this sample.</span></span> <span data-ttu-id="dd180-158">O serviço vinculado do HDInsight é usado para executar um script do Hive especificado na atividade do pipeline neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="dd180-158">The HDInsight linked service is used to run a Hive script specified in the activity of the pipeline in this sample.</span></span> <span data-ttu-id="dd180-159">Identifique quais [repositórios de dados](data-factory-data-movement-activities.md)/[serviços de computação](data-factory-compute-linked-services.md) serão usados em seu cenário e vincular esses serviços ao data factory criando serviços vinculados.</span><span class="sxs-lookup"><span data-stu-id="dd180-159">Identify what [data store](data-factory-data-movement-activities.md)/[compute services](data-factory-compute-linked-services.md) are used in your scenario and link those services to the data factory by creating linked services.</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="dd180-160">Criar o serviço vinculado do armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="dd180-160">Create Azure Storage linked service</span></span>
<span data-ttu-id="dd180-161">Nesta etapa, você vincula a conta do Armazenamento do Azure ao data factory.</span><span class="sxs-lookup"><span data-stu-id="dd180-161">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="dd180-162">Neste tutorial, use a mesma conta do Armazenamento do Azure para armazenar dados de entrada/saída e o arquivo do script do HQL.</span><span class="sxs-lookup"><span data-stu-id="dd180-162">In this tutorial, you use the same Azure Storage account to store input/output data and the HQL script file.</span></span>

1. <span data-ttu-id="dd180-163">Clique em **Criar e implantar** na folha **DATA FACTORY** para **GetStartedDF**.</span><span class="sxs-lookup"><span data-stu-id="dd180-163">Click **Author and deploy** on the **DATA FACTORY** blade for **GetStartedDF**.</span></span> <span data-ttu-id="dd180-164">Você deverá ver o Data Factory Editor.</span><span class="sxs-lookup"><span data-stu-id="dd180-164">You should see the Data Factory Editor.</span></span>

   ![Bloco Criar e implantar](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)
2. <span data-ttu-id="dd180-166">Clique em **Novo repositório de dados** e escolha **Armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="dd180-166">Click **New data store** and choose **Azure storage**.</span></span>

   ![Novo armazenamento de dados - Armazenamento do Azure - menu](./media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="dd180-168">Você deve ver o script JSON para criar um serviço de armazenamento vinculado do Azure no editor.</span><span class="sxs-lookup"><span data-stu-id="dd180-168">You should see the JSON script for creating an Azure Storage linked service in the editor.</span></span>

   ![Serviço vinculado de armazenamento do Azure](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="dd180-170">Substitua o **nome da conta** pelo nome da conta do Armazenamento do Azure e a **chave de conta** pela chave de acesso da sua conta do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd180-170">Replace **account name** with the name of your Azure storage account and **account key** with the access key of the Azure storage account.</span></span> <span data-ttu-id="dd180-171">Para saber como conseguir sua chave de acesso de armazenamento, consulte as informações sobre como exibir, copiar e regenerar chaves de acesso de armazenamento em [Gerenciar sua conta de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="dd180-171">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="dd180-172">Clique em **Implantar** na barra de comandos para implantar o serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="dd180-172">Click **Deploy** on the command bar to deploy the linked service.</span></span>

    ![Botão Implantar](./media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   <span data-ttu-id="dd180-174">Depois que o serviço vinculado for implantado com êxito, a janela **Rascunho-1** desaparecerá e você verá **AzureStorageLinkedService** no modo de exibição de árvore à esquerda.</span><span class="sxs-lookup"><span data-stu-id="dd180-174">After the linked service is deployed successfully, the **Draft-1** window should disappear and you see **AzureStorageLinkedService** in the tree view on the left.</span></span>

    ![Serviço Vinculado de Armazenamento no menu](./media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="dd180-176">Criar o serviço vinculado do Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="dd180-176">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="dd180-177">Nesta etapa, você vincula um cluster do HDInsight sob demanda ao seu data factory.</span><span class="sxs-lookup"><span data-stu-id="dd180-177">In this step, you link an on-demand HDInsight cluster to your data factory.</span></span> <span data-ttu-id="dd180-178">O cluster do HDInsight é automaticamente criado no tempo de execução e excluído após a conclusão do processamento, ficando ocioso durante o período especificado.</span><span class="sxs-lookup"><span data-stu-id="dd180-178">The HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for the specified amount of time.</span></span>

1. <span data-ttu-id="dd180-179">No **Editor de Data Factory**, clique em **... Mais**, clique em **Nova computação** e selecione **Cluster HDInsight sob demanda**.</span><span class="sxs-lookup"><span data-stu-id="dd180-179">In the **Data Factory Editor**, click **... More**, click **New compute**, and select **On-demand HDInsight cluster**.</span></span>

    ![Nova computação](./media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)
2. <span data-ttu-id="dd180-181">Copie e cole o trecho a seguir na janela de **Rascunho-1** .</span><span class="sxs-lookup"><span data-stu-id="dd180-181">Copy and paste the following snippet to the **Draft-1** window.</span></span> <span data-ttu-id="dd180-182">O trecho JSON descreve as propriedades usadas para criar o cluster do HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="dd180-182">The JSON snippet describes the properties that are used to create the HDInsight cluster on-demand.</span></span>

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

    <span data-ttu-id="dd180-183">A tabela a seguir fornece descrições das propriedades de JSON usadas no trecho de código:</span><span class="sxs-lookup"><span data-stu-id="dd180-183">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

   | <span data-ttu-id="dd180-184">Propriedade</span><span class="sxs-lookup"><span data-stu-id="dd180-184">Property</span></span> | <span data-ttu-id="dd180-185">Descrição</span><span class="sxs-lookup"><span data-stu-id="dd180-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="dd180-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="dd180-186">ClusterSize</span></span> |<span data-ttu-id="dd180-187">Especifica o tamanho do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dd180-187">Specifies the size of the HDInsight cluster.</span></span> |
   | <span data-ttu-id="dd180-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="dd180-188">TimeToLive</span></span> | <span data-ttu-id="dd180-189">Especifica que o tempo ocioso do cluster HDInsight antes de ser excluído.</span><span class="sxs-lookup"><span data-stu-id="dd180-189">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="dd180-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="dd180-190">linkedServiceName</span></span> | <span data-ttu-id="dd180-191">Especifica a conta de armazenamento usada para armazenar os logs gerados pelo HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dd180-191">Specifies the storage account that is used to store the logs that are generated by HDInsight.</span></span> |

    <span data-ttu-id="dd180-192">Observe os seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="dd180-192">Note the following points:</span></span>

   * <span data-ttu-id="dd180-193">O Data Factory cria um cluster HDInsight **baseado no Linux** para você com o JSON.</span><span class="sxs-lookup"><span data-stu-id="dd180-193">The Data Factory creates a **Linux-based** HDInsight cluster for you with the JSON.</span></span> <span data-ttu-id="dd180-194">Confira [Serviço vinculado do HDInsight sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="dd180-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="dd180-195">Você pode usar **seu próprio cluster do HDInsight** em vez de usar um cluster do HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="dd180-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="dd180-196">Confira [Serviço vinculado do HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="dd180-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="dd180-197">O cluster HDInsight cria um **contêiner padrão** no armazenamento de blobs especificado no JSON (**nomeServiçoVinculado**).</span><span class="sxs-lookup"><span data-stu-id="dd180-197">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="dd180-198">O HDInsight não exclui esse contêiner quando o cluster é excluído.</span><span class="sxs-lookup"><span data-stu-id="dd180-198">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="dd180-199">Este comportamento ocorre por design.</span><span class="sxs-lookup"><span data-stu-id="dd180-199">This behavior is by design.</span></span> <span data-ttu-id="dd180-200">Com o serviço vinculado HDInsight sob demanda, um cluster HDInsight é criado sempre que uma fatia é processada, a menos que haja um cluster ativo existente (**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="dd180-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="dd180-201">O cluster será excluído automaticamente quando o processamento for concluído.</span><span class="sxs-lookup"><span data-stu-id="dd180-201">The cluster is automatically deleted when the processing is done.</span></span>

       <span data-ttu-id="dd180-202">Quanto mais fatias forem processadas, você verá muitos contêineres no armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd180-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="dd180-203">Se você não precisa deles para solução de problemas dos trabalhos, convém excluí-los para reduzir o custo de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="dd180-203">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="dd180-204">Os nomes desses contêineres seguem um padrão: "adf**nomeseudatafactory**-**nomeserviçovinculado**- carimbodatahora".</span><span class="sxs-lookup"><span data-stu-id="dd180-204">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="dd180-205">Use ferramentas como o [Gerenciador de Armazenamento da Microsoft](http://storageexplorer.com/) para excluir contêineres do armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd180-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="dd180-206">Confira [Serviço vinculado do HDInsight sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="dd180-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
3. <span data-ttu-id="dd180-207">Clique em **Implantar** na barra de comandos para implantar o serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="dd180-207">Click **Deploy** on the command bar to deploy the linked service.</span></span>

    ![Implantar o serviço vinculado do HDInsight sob demanda](./media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)
4. <span data-ttu-id="dd180-209">Confirme que você vê **AzureStorageLinkedService** e **HDInsightOnDemandLinkedService** no modo de exibição de árvore à esquerda.</span><span class="sxs-lookup"><span data-stu-id="dd180-209">Confirm that you see both **AzureStorageLinkedService** and **HDInsightOnDemandLinkedService** in the tree view on the left.</span></span>

    ![Modo de exibição de árvore com serviços vinculados](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a><span data-ttu-id="dd180-211">Criar conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="dd180-211">Create datasets</span></span>
<span data-ttu-id="dd180-212">Nesta etapa, você cria conjuntos de dados para representar dados de entrada e de saída para o processamento do Hive.</span><span class="sxs-lookup"><span data-stu-id="dd180-212">In this step, you create datasets to represent the input and output data for Hive processing.</span></span> <span data-ttu-id="dd180-213">Esses conjuntos de dados fazem referência ao **AzureStorageLinkedService** que você criou anteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="dd180-213">These datasets refer to the **AzureStorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="dd180-214">O serviço vinculado aponta para uma conta do Armazenamento do Azure e os conjuntos de dados especificam o contêiner, a pasta e o nome do arquivo no armazenamento que contém os dados de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="dd180-214">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span></span>   

### <a name="create-input-dataset"></a><span data-ttu-id="dd180-215">Criar conjunto de dados de entrada</span><span class="sxs-lookup"><span data-stu-id="dd180-215">Create input dataset</span></span>
1. <span data-ttu-id="dd180-216">No **Editor de Data Factory**, clique em **... Mais** na barra de comandos, clique em **Novo conjunto de dados** e selecione **Armazenamento de Blobs do Azure**.</span><span class="sxs-lookup"><span data-stu-id="dd180-216">In the **Data Factory Editor**, click **... More** on the command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>

    ![Novo conjunto de dados](./media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)
2. <span data-ttu-id="dd180-218">Copie e cole o trecho a seguir na janela de Rascunho-1.</span><span class="sxs-lookup"><span data-stu-id="dd180-218">Copy and paste the following snippet to the Draft-1 window.</span></span> <span data-ttu-id="dd180-219">No trecho JSON, você está criando um conjunto de dados chamado **AzureBlobInput** que representa dados de entrada para uma atividade no pipeline.</span><span class="sxs-lookup"><span data-stu-id="dd180-219">In the JSON snippet, you are creating a dataset called **AzureBlobInput** that represents input data for an activity in the pipeline.</span></span> <span data-ttu-id="dd180-220">Além disso, você especifica que os dados de entrada estão localizados no contêiner de blobs denominado **adfgetstarted** e na pasta denominada **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="dd180-220">In addition, you specify that the input data is located in the blob container called **adfgetstarted** and the folder called **inputdata**.</span></span>

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
    <span data-ttu-id="dd180-221">A tabela a seguir fornece descrições das propriedades de JSON usadas no trecho de código:</span><span class="sxs-lookup"><span data-stu-id="dd180-221">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

   | <span data-ttu-id="dd180-222">Propriedade</span><span class="sxs-lookup"><span data-stu-id="dd180-222">Property</span></span> | <span data-ttu-id="dd180-223">Descrição</span><span class="sxs-lookup"><span data-stu-id="dd180-223">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="dd180-224">type</span><span class="sxs-lookup"><span data-stu-id="dd180-224">type</span></span> |<span data-ttu-id="dd180-225">A propriedade type é definida como **AzureBlob** porque os dados residem no armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd180-225">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span></span> |
   | <span data-ttu-id="dd180-226">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="dd180-226">linkedServiceName</span></span> |<span data-ttu-id="dd180-227">Refere-se ao **AzureStorageLinkedService** que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="dd180-227">Refers to the **AzureStorageLinkedService** you created earlier.</span></span> |
   | <span data-ttu-id="dd180-228">folderPath</span><span class="sxs-lookup"><span data-stu-id="dd180-228">folderPath</span></span> | <span data-ttu-id="dd180-229">Especifica o **contêiner** e a **pasta** de blob que contém blobs de entrada.</span><span class="sxs-lookup"><span data-stu-id="dd180-229">Specifies the blob **container** and the **folder** that contains input blobs.</span></span> | 
   | <span data-ttu-id="dd180-230">fileName</span><span class="sxs-lookup"><span data-stu-id="dd180-230">fileName</span></span> |<span data-ttu-id="dd180-231">Essa propriedade é opcional.</span><span class="sxs-lookup"><span data-stu-id="dd180-231">This property is optional.</span></span> <span data-ttu-id="dd180-232">Se você omitir essa propriedade, todos os arquivos de folderPath serão selecionados.</span><span class="sxs-lookup"><span data-stu-id="dd180-232">If you omit this property, all the files from the folderPath are picked.</span></span> <span data-ttu-id="dd180-233">Neste tutorial, somente o **input.log** é processado.</span><span class="sxs-lookup"><span data-stu-id="dd180-233">In this tutorial, only the **input.log** is processed.</span></span> |
   | <span data-ttu-id="dd180-234">type</span><span class="sxs-lookup"><span data-stu-id="dd180-234">type</span></span> |<span data-ttu-id="dd180-235">Os arquivos de log estão em formato de texto, então utilizaremos **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="dd180-235">The log files are in text format, so we use **TextFormat**.</span></span> |
   | <span data-ttu-id="dd180-236">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="dd180-236">columnDelimiter</span></span> |<span data-ttu-id="dd180-237">as colunas nos arquivos de log são delimitadas pelo **caractere de vírgula (`,`)**</span><span class="sxs-lookup"><span data-stu-id="dd180-237">columns in the log files are delimited by **comma character (`,`)**</span></span> |
   | <span data-ttu-id="dd180-238">frequência/intervalo</span><span class="sxs-lookup"><span data-stu-id="dd180-238">frequency/interval</span></span> |<span data-ttu-id="dd180-239">a frequência é definida como **Mês** e o intervalo como **1**, o que significa que as fatias de entrada estão disponíveis mensalmente.</span><span class="sxs-lookup"><span data-stu-id="dd180-239">frequency set to **Month** and interval is **1**, which means that the input slices are available monthly.</span></span> |
   | <span data-ttu-id="dd180-240">externo</span><span class="sxs-lookup"><span data-stu-id="dd180-240">external</span></span> | <span data-ttu-id="dd180-241">Essa propriedade será definida como **true** se os dados não forem gerados por esse pipeline.</span><span class="sxs-lookup"><span data-stu-id="dd180-241">This property is set to **true** if the input data is not generated by this pipeline.</span></span> <span data-ttu-id="dd180-242">Neste tutorial, o arquivo input.log não é gerado por esse pipeline, portanto, definimos a propriedade como true.</span><span class="sxs-lookup"><span data-stu-id="dd180-242">In this tutorial, the input.log file is not generated by this pipeline, so we set the property to true.</span></span> |

    <span data-ttu-id="dd180-243">Para saber mais sobre essas propriedades JSON, confira o [artigo sobre o conector do Blob do Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="dd180-243">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="dd180-244">Clique em **Implantar** na barra de comandos para implantar o conjunto de dados recém-criado.</span><span class="sxs-lookup"><span data-stu-id="dd180-244">Click **Deploy** on the command bar to deploy the newly created dataset.</span></span> <span data-ttu-id="dd180-245">Você deverá ver o conjunto de dados no modo de exibição de árvore à esquerda.</span><span class="sxs-lookup"><span data-stu-id="dd180-245">You should see the dataset in the tree view on the left.</span></span>

### <a name="create-output-dataset"></a><span data-ttu-id="dd180-246">Criar conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="dd180-246">Create output dataset</span></span>
<span data-ttu-id="dd180-247">Agora, você cria o conjunto de dados de saída para representar os dados de saída armazenados no armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd180-247">Now, you create the output dataset to represent the output data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="dd180-248">No **Editor de Data Factory**, clique em **... Mais** na barra de comandos, clique em **Novo conjunto de dados** e selecione **Armazenamento de Blobs do Azure**.</span><span class="sxs-lookup"><span data-stu-id="dd180-248">In the **Data Factory Editor**, click **... More** on the command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="dd180-249">Copie e cole o trecho a seguir na janela de Rascunho-1.</span><span class="sxs-lookup"><span data-stu-id="dd180-249">Copy and paste the following snippet to the Draft-1 window.</span></span> <span data-ttu-id="dd180-250">No trecho JSON, você está criando um conjunto de dados chamado **AzureBlobOutput**e especificando a estrutura dos dados produzidos pelo script do Hive.</span><span class="sxs-lookup"><span data-stu-id="dd180-250">In the JSON snippet, you are creating a dataset called **AzureBlobOutput**, and specifying the structure of the data that is produced by the Hive script.</span></span> <span data-ttu-id="dd180-251">Além disso, você especifica que os resultados estão armazenados no contêiner de blobs denominado **adfgetstarted** e na pasta denominada **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="dd180-251">In addition, you specify that the results are stored in the blob container called **adfgetstarted** and the folder called **partitioneddata**.</span></span> <span data-ttu-id="dd180-252">A seção **availability** especifica que o conjunto de dados de saída é produzido mensalmente.</span><span class="sxs-lookup"><span data-stu-id="dd180-252">The **availability** section specifies that the output dataset is produced on a monthly basis.</span></span>

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
    <span data-ttu-id="dd180-253">Consulte a seção **Criar o conjunto de dados de entrada** para obter descrições dessas propriedades.</span><span class="sxs-lookup"><span data-stu-id="dd180-253">See **Create the input dataset** section for descriptions of these properties.</span></span> <span data-ttu-id="dd180-254">Você não define a propriedade externa em um conjunto de dados de saída porque o conjunto de dados é produzido pelo serviço Data Factory.</span><span class="sxs-lookup"><span data-stu-id="dd180-254">You do not set the external property on an output dataset as the dataset is produced by the Data Factory service.</span></span>
3. <span data-ttu-id="dd180-255">Clique em **Implantar** na barra de comandos para implantar o conjunto de dados recém-criado.</span><span class="sxs-lookup"><span data-stu-id="dd180-255">Click **Deploy** on the command bar to deploy the newly created dataset.</span></span>
4. <span data-ttu-id="dd180-256">Verifique se o conjunto de dados foi criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="dd180-256">Verify that the dataset is created successfully.</span></span>

    ![Modo de exibição de árvore com serviços vinculados](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-pipeline"></a><span data-ttu-id="dd180-258">Criar um pipeline</span><span class="sxs-lookup"><span data-stu-id="dd180-258">Create pipeline</span></span>
<span data-ttu-id="dd180-259">Nesta etapa, você cria seu primeiro pipeline com a atividade **HDInsightHive** .</span><span class="sxs-lookup"><span data-stu-id="dd180-259">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="dd180-260">A fatia de entrada está disponível mensalmente (frequência: mês, intervalo: 1), a fatia de saída é produzida mensalmente e a propriedade do agendador para a atividade também é definida como mensal.</span><span class="sxs-lookup"><span data-stu-id="dd180-260">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and the scheduler property for the activity is also set to monthly.</span></span> <span data-ttu-id="dd180-261">As configurações para o conjunto de dados de saída e o agendador de atividades devem corresponder.</span><span class="sxs-lookup"><span data-stu-id="dd180-261">The settings for the output dataset and the activity scheduler must match.</span></span> <span data-ttu-id="dd180-262">Atualmente, o conjunto de dados de saída é o que aciona a agenda, então você deve criar um conjunto de dados de saída, mesmo que a atividade não produza qualquer saída.</span><span class="sxs-lookup"><span data-stu-id="dd180-262">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="dd180-263">Se a atividade não receber entradas, ignore a criação de conjunto de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="dd180-263">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> <span data-ttu-id="dd180-264">As propriedades usadas no JSON a seguir são explicadas no final desta seção.</span><span class="sxs-lookup"><span data-stu-id="dd180-264">The properties used in the following JSON are explained at the end of this section.</span></span>

1. <span data-ttu-id="dd180-265">No **Editor de Data Factory**, clique em **Reticências (...) Mais comandos** e em **Novo pipeline**.</span><span class="sxs-lookup"><span data-stu-id="dd180-265">In the **Data Factory Editor**, click **Ellipsis (…) More commands** and then click **New pipeline**.</span></span>

    ![botão novo pipeline](./media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)
2. <span data-ttu-id="dd180-267">Copie e cole o trecho a seguir na janela de Rascunho-1.</span><span class="sxs-lookup"><span data-stu-id="dd180-267">Copy and paste the following snippet to the Draft-1 window.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="dd180-268">Substitua **storageaccountname** pelo nome da sua conta de armazenamento no JSON.</span><span class="sxs-lookup"><span data-stu-id="dd180-268">Replace **storageaccountname** with the name of your storage account in the JSON.</span></span>
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

    <span data-ttu-id="dd180-269">No trecho de JSON, você cria um pipeline que consiste de uma única atividade que usa o Hive para processar dados em um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dd180-269">In the JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive to process Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="dd180-270">O arquivo de script do Hive, **partitionweblogs.hql**, é armazenado na conta de armazenamento do Azure (especificada pelo scriptLinkedService chamado **AzureStorageLinkedService**) e na pasta **script** no contêiner **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="dd180-270">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>

    <span data-ttu-id="dd180-271">A seção **defines** é usada para especificar as configurações de tempo de execução passadas para o script do hive como valores de configuração do Hive (por exemplo, ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span><span class="sxs-lookup"><span data-stu-id="dd180-271">The **defines** section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="dd180-272">As propriedades **start** e **end** do pipeline especificam o período ativo do pipeline.</span><span class="sxs-lookup"><span data-stu-id="dd180-272">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span></span>

    <span data-ttu-id="dd180-273">Na atividade do JSON, você especifica que o script do Hive é executado na máquina especificada pelo **nomeServiçoVinculado** – **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="dd180-273">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dd180-274">Consulte "Pipeline JSON" [Pipelines e atividades no Azure Data Factory](data-factory-create-pipelines.md) para obter detalhes sobre as propriedades JSON usadas no exemplo.</span><span class="sxs-lookup"><span data-stu-id="dd180-274">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in the example.</span></span>
   >
   >
3. <span data-ttu-id="dd180-275">Confirme o seguinte:</span><span class="sxs-lookup"><span data-stu-id="dd180-275">Confirm the following:</span></span>

   1. <span data-ttu-id="dd180-276">O arquivo **input.log** existe na pasta **inputdata** do contêiner **adfgetstarted** no armazenamento de blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="dd180-276">**input.log** file exists in the **inputdata** folder of the **adfgetstarted** container in the Azure blob storage</span></span>
   2. <span data-ttu-id="dd180-277">O arquivo **partitionweblogs.hql** existe na pasta **script** do contêiner **adfgetstarted** no armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd180-277">**partitionweblogs.hql** file exists in the **script** folder of the **adfgetstarted** container in the Azure blob storage.</span></span> <span data-ttu-id="dd180-278">Conclua as etapas de pré-requisito na [Visão geral do tutorial](data-factory-build-your-first-pipeline.md) se você não vir esses arquivos.</span><span class="sxs-lookup"><span data-stu-id="dd180-278">Complete the prerequisite steps in the [Tutorial Overview](data-factory-build-your-first-pipeline.md) if you don't see these files.</span></span>
   3. <span data-ttu-id="dd180-279">Confirme se você substituiu **storageaccountname** pelo nome da sua conta de armazenamento no JSON.</span><span class="sxs-lookup"><span data-stu-id="dd180-279">Confirm that you replaced **storageaccountname** with the name of your storage account in the pipeline JSON.</span></span>
4. <span data-ttu-id="dd180-280">Clique em **Implantar** na barra de comandos para implantar o pipeline.</span><span class="sxs-lookup"><span data-stu-id="dd180-280">Click **Deploy** on the command bar to deploy the pipeline.</span></span> <span data-ttu-id="dd180-281">Como as horas de **início** e de **término** são definidas no passado e **isPaused** está definido como false, o pipeline (a atividade no pipeline) é imediatamente executado após a implantação.</span><span class="sxs-lookup"><span data-stu-id="dd180-281">Since the **start** and **end** times are set in the past and **isPaused** is set to false, the pipeline (activity in the pipeline) runs immediately after you deploy.</span></span>
5. <span data-ttu-id="dd180-282">Confirme que você vê o pipeline no modo de exibição de árvore.</span><span class="sxs-lookup"><span data-stu-id="dd180-282">Confirm that you see the pipeline in the tree view.</span></span>

    ![Modo de exibição de árvore com pipeline](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)
6. <span data-ttu-id="dd180-284">Parabéns, você criou com sucesso seu primeiro pipeline!</span><span class="sxs-lookup"><span data-stu-id="dd180-284">Congratulations, you have successfully created your first pipeline!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="dd180-285">Monitorar o pipeline</span><span class="sxs-lookup"><span data-stu-id="dd180-285">Monitor pipeline</span></span>
### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="dd180-286">Monitorar o pipeline usando a Exibição de Diagrama</span><span class="sxs-lookup"><span data-stu-id="dd180-286">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="dd180-287">Clique em **X** para fechar as folhas do Editor da Fábrica de Dados e para navegar de volta à folha Fábrica de Dados e clique em **Diagrama**.</span><span class="sxs-lookup"><span data-stu-id="dd180-287">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory blade, and click **Diagram**.</span></span>

    ![Bloco do diagrama](./media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)
2. <span data-ttu-id="dd180-289">Na Exibição de Diagrama, você tem uma visão geral dos pipelines e dos conjuntos de dados usados neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="dd180-289">In the Diagram View, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>

    ![Exibição de diagrama](./media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)
3. <span data-ttu-id="dd180-291">Para exibir todas as atividades no pipeline, clique com o botão direito do mouse no pipeline no diagrama e clique em Abrir Pipeline.</span><span class="sxs-lookup"><span data-stu-id="dd180-291">To view all activities in the pipeline, right-click pipeline in the diagram and click Open Pipeline.</span></span>

    ![Menu do pipeline aberto](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)
4. <span data-ttu-id="dd180-293">Confirme que você vê a atividade HDInsightHive no pipeline.</span><span class="sxs-lookup"><span data-stu-id="dd180-293">Confirm that you see the HDInsightHive activity in the pipeline.</span></span>

    ![Abrir a exibição do pipeline](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    <span data-ttu-id="dd180-295">Para navegar de volta ao modo de exibição anterior, clique em **Data factory** no menu de atalho na parte superior.</span><span class="sxs-lookup"><span data-stu-id="dd180-295">To navigate back to the previous view, click **Data factory** in the breadcrumb menu at the top.</span></span>
5. <span data-ttu-id="dd180-296">Na **Exibição do Diagrama**, clique duas vezes no conjunto de dados **AzureBlobInput**.</span><span class="sxs-lookup"><span data-stu-id="dd180-296">In the **Diagram View**, double-click the dataset **AzureBlobInput**.</span></span> <span data-ttu-id="dd180-297">Confirme se a fatia está no estado **Pronto** .</span><span class="sxs-lookup"><span data-stu-id="dd180-297">Confirm that the slice is in **Ready** state.</span></span> <span data-ttu-id="dd180-298">Pode levar alguns minutos para que a fatia apareça no estado Pronto.</span><span class="sxs-lookup"><span data-stu-id="dd180-298">It may take a couple of minutes for the slice to show up in Ready state.</span></span> <span data-ttu-id="dd180-299">Se isso não acontecer depois de algum tempo, veja se o arquivo de entrada (input.log) está posicionado no contêiner à direita (adfgetstarted) e na pasta (inputdata).</span><span class="sxs-lookup"><span data-stu-id="dd180-299">If it does not happen after you wait for sometime, see if you have the input file (input.log) placed in the right container (adfgetstarted) and folder (inputdata).</span></span>

   ![Fatia de entrada no estado pronto](./media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)
6. <span data-ttu-id="dd180-301">Clique em **X** para fechar a folha **AzureBlobInput**.</span><span class="sxs-lookup"><span data-stu-id="dd180-301">Click **X** to close **AzureBlobInput** blade.</span></span>
7. <span data-ttu-id="dd180-302">Na **Exibição do Diagrama**, clique duas vezes no conjunto de dados **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="dd180-302">In the **Diagram View**, double-click the dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="dd180-303">Você verá a fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="dd180-303">You see that the slice that is currently being processed.</span></span>

   ![Conjunto de dados](./media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)
8. <span data-ttu-id="dd180-305">Quando o processamento for concluído, você verá a fatia no estado **Pronto** .</span><span class="sxs-lookup"><span data-stu-id="dd180-305">When processing is done, you see the slice in **Ready** state.</span></span>

   ![Conjunto de dados](./media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > <span data-ttu-id="dd180-307">A criação de um cluster do HDInsight sob demanda geralmente leva algum tempo (20 minutos, aproximadamente).</span><span class="sxs-lookup"><span data-stu-id="dd180-307">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="dd180-308">Portanto, espere que o pipeline demore **cerca de 30 minutos** para processar a fatia.</span><span class="sxs-lookup"><span data-stu-id="dd180-308">Therefore, expect the pipeline to       take **approximately 30 minutes** to process the slice.</span></span>
   >
   >

9. <span data-ttu-id="dd180-309">Quando a fatia estiver no estado **Pronto**, verifique a pasta **partitioneddata** no contêiner **adfgetstarted** em seu armazenamento de blobs para os dados de saída.</span><span class="sxs-lookup"><span data-stu-id="dd180-309">When the slice is in **Ready** state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span></span>  

   ![dados de saída](./media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)
10. <span data-ttu-id="dd180-311">Clique na fatia para ver detalhes sobre ela em uma folha **Fatia de dados** .</span><span class="sxs-lookup"><span data-stu-id="dd180-311">Click the slice to see details about it in a **Data slice** blade.</span></span>

   ![Detalhes da fatia de dados](./media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)  
11. <span data-ttu-id="dd180-313">Clique em uma execução da atividade na **Lista de execuções da atividade** para ver detalhes sobre uma execução da atividade (atividade de Hive em nosso cenário) em uma janela **Detalhes de execução da atividade**.</span><span class="sxs-lookup"><span data-stu-id="dd180-313">Click an activity run in the **Activity runs list** to see details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span></span>   

   ![Detalhes da execução da atividade](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   <span data-ttu-id="dd180-315">Nos arquivos de log, você pode ver a consulta do Hive executada e as informações de status.</span><span class="sxs-lookup"><span data-stu-id="dd180-315">From the log files, you can see the Hive query that was executed and status information.</span></span> <span data-ttu-id="dd180-316">Esses logs são úteis para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="dd180-316">These logs are useful for troubleshooting any issues.</span></span>
   <span data-ttu-id="dd180-317">Confira o artigo [Monitorar e gerenciar pipelines usando as folhas do portal do Azure](data-factory-monitor-manage-pipelines.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="dd180-317">See [Monitor and manage pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) article for more details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dd180-318">O arquivo de entrada é excluído quando a fatia é processada com êxito.</span><span class="sxs-lookup"><span data-stu-id="dd180-318">The input file gets deleted when the slice is processed successfully.</span></span> <span data-ttu-id="dd180-319">Portanto, se você quiser executar novamente a fatia ou fazer o tutorial novamente, carregue o arquivo de entrada (input.log) na pasta inputdata do contêiner adfgetstarted.</span><span class="sxs-lookup"><span data-stu-id="dd180-319">Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the inputdata folder of the adfgetstarted container.</span></span>
>
>

### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="dd180-320">Monitorar o pipeline usando o aplicativo Monitorar e Gerenciar</span><span class="sxs-lookup"><span data-stu-id="dd180-320">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="dd180-321">Você também pode usar o aplicativo Monitorar e Gerenciar para monitorar os pipelines.</span><span class="sxs-lookup"><span data-stu-id="dd180-321">You can also use Monitor & Manage application to monitor your pipelines.</span></span> <span data-ttu-id="dd180-322">Para obter informações detalhadas sobre como usar esse aplicativo, confira [Monitorar e gerenciar pipelines do Azure Data Factory usando o aplicativo Monitorar e Gerenciar](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="dd180-322">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="dd180-323">Clique no bloco **Monitorar e Gerenciar** na home page do seu data factory.</span><span class="sxs-lookup"><span data-stu-id="dd180-323">Click **Monitor & Manage** tile on the home page for your data factory.</span></span>

    ![Bloco Monitorar e Gerenciar](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)
2. <span data-ttu-id="dd180-325">Você deve ver **Monitorar e Gerenciar aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="dd180-325">You should see **Monitor & Manage application**.</span></span> <span data-ttu-id="dd180-326">Altere a **Hora de início** e a **Hora de término** para coincidir com o início e o término do seu pipeline, e clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="dd180-326">Change the **Start time** and **End time** to match start and end times of your pipeline, and click **Apply**.</span></span>

    ![Aplicativo Monitorar e Gerenciar](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)
3. <span data-ttu-id="dd180-328">Selecione uma janela de atividade na lista de **Janelas de Atividade** para ver detalhes sobre ela.</span><span class="sxs-lookup"><span data-stu-id="dd180-328">Select an activity window in the **Activity Windows** list to see details about it.</span></span>

    ![Detalhes da janela Atividade](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

## <a name="summary"></a><span data-ttu-id="dd180-330">Resumo</span><span class="sxs-lookup"><span data-stu-id="dd180-330">Summary</span></span>
<span data-ttu-id="dd180-331">Neste tutorial, você criou uma data factory do Azure para processar dados ao executar o script Hive em um cluster hadoop do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dd180-331">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="dd180-332">Você usou o Data Factory Editor no portal do Azure para executar as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="dd180-332">You used the Data Factory Editor in the Azure portal to do the following steps:</span></span>  

1. <span data-ttu-id="dd180-333">Foi criada uma **data factory**do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd180-333">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="dd180-334">Foram criados dois **serviços vinculados**:</span><span class="sxs-lookup"><span data-stu-id="dd180-334">Created two **linked services**:</span></span>
   1. <span data-ttu-id="dd180-335">**Armazenamento do Azure** para vincular seu armazenamento de blobs do Azure que contém os arquivos de entrada/saída para a data factory.</span><span class="sxs-lookup"><span data-stu-id="dd180-335">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span></span>
   2. <span data-ttu-id="dd180-336">**Azure HDInsight** sob demanda para vincular um cluster Hadoop do HDInsight sob demanda à data factory.</span><span class="sxs-lookup"><span data-stu-id="dd180-336">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span></span> <span data-ttu-id="dd180-337">O Azure Data Factory cria um cluster Hadoop do HDInsight just-in-time para processar dados de entrada e gerar dados de saída.</span><span class="sxs-lookup"><span data-stu-id="dd180-337">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span></span>
3. <span data-ttu-id="dd180-338">Foram criados dois **conjuntos de dados**que descrevem dados de entrada e de saída para a atividade Hive do HDInsight no pipeline.</span><span class="sxs-lookup"><span data-stu-id="dd180-338">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span></span>
4. <span data-ttu-id="dd180-339">Foi criado um **pipeline** com uma atividade **Hive do HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="dd180-339">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd180-340">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dd180-340">Next Steps</span></span>
<span data-ttu-id="dd180-341">Neste artigo, você criou um pipeline com uma atividade de transformação (atividade do HDInsight) que executa um script Hive em um cluster do HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="dd180-341">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="dd180-342">Para saber como usar uma Atividade de Cópia para copiar dados de um Blob do Azure para o SQL do Azure, confira [Tutorial: Copiar dados de um blob do Azure para o SQL do Azure](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="dd180-342">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="dd180-343">Consulte também</span><span class="sxs-lookup"><span data-stu-id="dd180-343">See Also</span></span>
| <span data-ttu-id="dd180-344">Tópico</span><span class="sxs-lookup"><span data-stu-id="dd180-344">Topic</span></span> | <span data-ttu-id="dd180-345">Descrição</span><span class="sxs-lookup"><span data-stu-id="dd180-345">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="dd180-346">Pipelines</span><span class="sxs-lookup"><span data-stu-id="dd180-346">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="dd180-347">Este artigo o ajuda a compreender pipelines e atividades no Azure Data Factory e como usá-los para construir fluxos de trabalho orientados a dados de ponta a ponta para seu cenário ou negócio.</span><span class="sxs-lookup"><span data-stu-id="dd180-347">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="dd180-348">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="dd180-348">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="dd180-349">Este artigo o ajuda a entender os conjuntos de dados no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="dd180-349">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="dd180-350">Agendamento e execução</span><span class="sxs-lookup"><span data-stu-id="dd180-350">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="dd180-351">Este artigo explica os aspectos de agendamento e execução do modelo de aplicativo do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="dd180-351">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="dd180-352">Monitorar e gerenciar pipelines usando o Aplicativo de Monitoramento</span><span class="sxs-lookup"><span data-stu-id="dd180-352">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="dd180-353">Este artigo descreve como monitorar, gerenciar e depurar seus pipelines usando o Aplicativo de Monitoramento e Gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="dd180-353">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |
