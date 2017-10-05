---
title: Criar seu primeiro data factory (Visual Studio) | Microsoft Docs
description: "Neste tutorial, você cria um pipeline de exemplo do Azure Data Factory usando o Visual Studio."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7398c0c9-7a03-4628-94b3-f2aaef4a72c5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 77042219cbe698a33ab9447aa952586772897241
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-create-a-data-factory-by-using-visual-studio"></a><span data-ttu-id="86084-103">Tutorial: Como criar uma data factory usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="86084-103">Tutorial: Create a data factory by using Visual Studio</span></span>
> [!div class="op_single_selector" title="Tools/SDKs"]
> * [<span data-ttu-id="86084-104">Visão geral e pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="86084-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="86084-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="86084-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="86084-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="86084-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="86084-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="86084-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="86084-108">Modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="86084-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="86084-109">API REST</span><span class="sxs-lookup"><span data-stu-id="86084-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)

<span data-ttu-id="86084-110">Este tutorial mostra como criar um Azure data factory usando o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="86084-110">This tutorial shows you how to create an Azure data factory by using Visual Studio.</span></span> <span data-ttu-id="86084-111">Crie um projeto do Visual Studio usando o modelo de projeto de Data Factory, defina as entidades da Data Factory (serviços vinculados, conjuntos de dados e pipeline) no formato JSON e, em seguida, publique/implante essas entidades à nuvem.</span><span class="sxs-lookup"><span data-stu-id="86084-111">You create a Visual Studio project using the Data Factory project template, define Data Factory entities (linked services, datasets, and pipeline) in JSON format, and then publish/deploy these entities to the cloud.</span></span> 

<span data-ttu-id="86084-112">O pipeline neste tutorial tem uma atividade: **atividade hive do HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="86084-112">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="86084-113">Esta atividade executa um script de hive em um cluster do HDInsight do Azure que transforma os dados de entrada para gerar dados de saída.</span><span class="sxs-lookup"><span data-stu-id="86084-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="86084-114">O pipeline é agendado para ser executado uma vez por mês entre os horários de início e término especificados.</span><span class="sxs-lookup"><span data-stu-id="86084-114">The pipeline is scheduled to run once a month between the specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="86084-115">Este tutorial não mostra como copiar dados usando Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="86084-115">This tutorial does not show how copy data by using Azure Data Factory.</span></span> <span data-ttu-id="86084-116">Para obter um tutorial sobre como copiar dados usando o Azure Data Factory, confira [Tutorial: copiar dados do armazenamento de blobs para um banco de dados SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="86084-116">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="86084-117">Um pipeline pode ter mais de uma atividade.</span><span class="sxs-lookup"><span data-stu-id="86084-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="86084-118">E você pode encadear duas atividades (executar uma atividade após a outra) definindo o conjunto de dados de saída de uma atividade como o conjunto de dados de entrada da outra atividade.</span><span class="sxs-lookup"><span data-stu-id="86084-118">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="86084-119">Para saber mais, confira [Agendamento e execução no Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="86084-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>


## <a name="walkthrough-create-and-publish-data-factory-entities"></a><span data-ttu-id="86084-120">Passo a passo: Como criar e publicar as entidades da Data Factory</span><span class="sxs-lookup"><span data-stu-id="86084-120">Walkthrough: Create and publish Data Factory entities</span></span>
<span data-ttu-id="86084-121">Eis as etapas executadas como parte deste tutorial:</span><span class="sxs-lookup"><span data-stu-id="86084-121">Here are the steps you perform as part of this walkthrough:</span></span>

1. <span data-ttu-id="86084-122">Crie dois serviços vinculados: **AzureStorageLinkedService1** e **HDInsightOnDemandLinkedService1**.</span><span class="sxs-lookup"><span data-stu-id="86084-122">Create two linked services: **AzureStorageLinkedService1** and **HDInsightOnDemandLinkedService1**.</span></span> 
   
    <span data-ttu-id="86084-123">Neste tutorial, os dados de entrada e saída da atividade de hive estão no mesmo armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="86084-123">In this tutorial, both input and output data for the hive activity are in the same Azure Blob Storage.</span></span> <span data-ttu-id="86084-124">Você pode usar um cluster do HDInsight sob demanda para processar dados de entrada existentes para gerar dados de saída.</span><span class="sxs-lookup"><span data-stu-id="86084-124">You use an on-demand HDInsight cluster to process existing input data to produce output data.</span></span> <span data-ttu-id="86084-125">O cluster do HDInsight sob demanda é criado automaticamente para você pela Azure Data Factory em tempo de execução quando os dados de entrada estão prontos para serem processados.</span><span class="sxs-lookup"><span data-stu-id="86084-125">The on-demand HDInsight cluster is automatically created for you by Azure Data Factory at run time when the input data is ready to be processed.</span></span> <span data-ttu-id="86084-126">Você deve vincular seus armazenamentos de dados ou computadores à data factory para que o serviço Data Factory possa se conectar com eles durante tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="86084-126">You need to link your data stores or computes to your data factory so that the Data Factory service can connect to them at runtime.</span></span> <span data-ttu-id="86084-127">Ou seja, vincule sua conta de armazenamento do Azure à data factory usando o AzureStorageLinkedService1, e um cluster do HDInsight sob demanda com o HDInsightOnDemandLinkedService1.</span><span class="sxs-lookup"><span data-stu-id="86084-127">Therefore, you link your Azure Storage Account to the data factory by using the AzureStorageLinkedService1, and link an on-demand HDInsight cluster by using the HDInsightOnDemandLinkedService1.</span></span> <span data-ttu-id="86084-128">Ao publicar, especifique o nome da data factory a ser criado ou existente.</span><span class="sxs-lookup"><span data-stu-id="86084-128">When publishing, you specify the name for the data factory to be created or an existing data factory.</span></span>  
2. <span data-ttu-id="86084-129">Crie dois conjuntos de dados: **InputDataset** e **OutputDataset**, que representam os dados de entrada/saída armazenados no armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="86084-129">Create two datasets: **InputDataset** and **OutputDataset**, which represent the input/output data that is stored in the Azure blob storage.</span></span> 
   
    <span data-ttu-id="86084-130">Essas definições de conjunto de dados se referem ao serviço vinculado do armazenamento do Azure que você criou na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="86084-130">These dataset definitions refer to the Azure Storage linked service you created in the previous step.</span></span> <span data-ttu-id="86084-131">Para o InputDataset, você pode especificar o contêiner de blobs (adfgetstarted) e a pasta (inptutdata) que contém um blob com os dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="86084-131">For the InputDataset, you specify the blob container (adfgetstarted) and the folder (inptutdata) that contains a blob with the input data.</span></span> <span data-ttu-id="86084-132">Para o OutputDataset, você pode especificar o contêiner de blobs (adfgetstarted) e a pasta (partitioneddata) que contém os dados de saída.</span><span class="sxs-lookup"><span data-stu-id="86084-132">For the OutputDataset, you specify the blob container (adfgetstarted) and the folder (partitioneddata) that holds the output data.</span></span> <span data-ttu-id="86084-133">Você também pode especificar outras propriedades, como estrutura, disponibilidade e política.</span><span class="sxs-lookup"><span data-stu-id="86084-133">You also specify other properties such as structure, availability, and policy.</span></span>
3. <span data-ttu-id="86084-134">Crie um pipeline chamado **MyFirstPipeline**.</span><span class="sxs-lookup"><span data-stu-id="86084-134">Create a pipeline named **MyFirstPipeline**.</span></span> 
  
    <span data-ttu-id="86084-135">Neste passo a passo, o pipeline tem apenas uma atividade: **atividade de Hive do HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="86084-135">In this walkthrough, the pipeline has only one activity: **HDInsight Hive Activity**.</span></span> <span data-ttu-id="86084-136">Essa atividade transforma dados de entrada para gerar dados de saída ao executar um script de hive em um cluster do HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="86084-136">This activity transform input data to produce output data by running a hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="86084-137">Para saber mais sobre a atividade de hive, confira [Atividade de Hive](data-factory-hive-activity.md)</span><span class="sxs-lookup"><span data-stu-id="86084-137">To learn more about hive activity, see [Hive Activity](data-factory-hive-activity.md)</span></span> 
4. <span data-ttu-id="86084-138">Crie uma data factory denominada **DataFactoryUsingVS**.</span><span class="sxs-lookup"><span data-stu-id="86084-138">Create a data factory named **DataFactoryUsingVS**.</span></span> <span data-ttu-id="86084-139">Implante o data factory e todas as entidades de Data Factory (serviços vinculados, tabelas e pipeline).</span><span class="sxs-lookup"><span data-stu-id="86084-139">Deploy the data factory and all Data Factory entities (linked services, tables, and the pipeline).</span></span>
5. <span data-ttu-id="86084-140">Depois de publicar, use as folhas do portal do Azure e aplicativos de gerenciamento e monitoramento para monitorar o pipeline.</span><span class="sxs-lookup"><span data-stu-id="86084-140">After you publish, you use Azure portal blades and Monitoring & Management App to monitor the pipeline.</span></span> 
  
### <a name="prerequisites"></a><span data-ttu-id="86084-141">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="86084-141">Prerequisites</span></span>
1. <span data-ttu-id="86084-142">Leia o artigo [Visão geral do tutorial](data-factory-build-your-first-pipeline.md) e concluir as etapas de **pré-requisito** .</span><span class="sxs-lookup"><span data-stu-id="86084-142">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span> <span data-ttu-id="86084-143">Você também pode selecionar a opção **Visão geral e Pré-requisitos** na lista suspensa, na parte superior, para alternar para o artigo.</span><span class="sxs-lookup"><span data-stu-id="86084-143">You can also select the **Overview and prerequisites** option in the drop-down list at the top to switch to the article.</span></span> <span data-ttu-id="86084-144">Depois de concluir os pré-requisitos, alterne de volta para este artigo, selecionando a opção **Visual Studio** na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="86084-144">After you complete the prerequisites, switch back to this article by selecting **Visual Studio** option in the drop-down list.</span></span>
2. <span data-ttu-id="86084-145">Para criar instâncias de Data Factory, você deve ser um membro da função [Colaborador de Data Factory](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) no nível de assinatura/grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="86084-145">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>  
3. <span data-ttu-id="86084-146">Você deve ter os seguintes itens instalados no seu computador:</span><span class="sxs-lookup"><span data-stu-id="86084-146">You must have the following installed on your computer:</span></span>
   * <span data-ttu-id="86084-147">Visual Studio 2013 ou Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="86084-147">Visual Studio 2013 or Visual Studio 2015</span></span>
   * <span data-ttu-id="86084-148">Baixe o SDK do Azure para Visual Studio 2013 ou Visual Studio de 2015.</span><span class="sxs-lookup"><span data-stu-id="86084-148">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="86084-149">Navegue até a [Página de Download do Azure](https://azure.microsoft.com/downloads/) e clique em **VS 2013** ou **VS 2015** na seção **.NET**.</span><span class="sxs-lookup"><span data-stu-id="86084-149">Navigate to [Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in the **.NET** section.</span></span>
   * <span data-ttu-id="86084-150">Baixe o plug-in Azure Data Factory para o Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) ou [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span><span class="sxs-lookup"><span data-stu-id="86084-150">Download the latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="86084-151">Você também pode atualizar o plug-in, executando as seguintes etapas: no menu, clique em **Ferramentas** -> **Extensões e Atualizações** -> **Online** -> **Galeria do Visual Studio** -> **Ferramentas do Microsoft Azure Data Factory** -> **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="86084-151">You can also update the plugin by doing the following steps: On the menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

<span data-ttu-id="86084-152">Agora, vamos usar o Visual Studio para criar um data factory do Azure.</span><span class="sxs-lookup"><span data-stu-id="86084-152">Now, let's use Visual Studio to create an Azure data factory.</span></span>

### <a name="create-visual-studio-project"></a><span data-ttu-id="86084-153">Criar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="86084-153">Create Visual Studio project</span></span>
1. <span data-ttu-id="86084-154">Inicie o **Visual Studio 2013** ou o **Visual Studio 2015**.</span><span class="sxs-lookup"><span data-stu-id="86084-154">Launch **Visual Studio 2013** or **Visual Studio 2015**.</span></span> <span data-ttu-id="86084-155">Clique em **Arquivo**, aponte para **Novo** e clique em **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="86084-155">Click **File**, point to **New**, and click **Project**.</span></span> <span data-ttu-id="86084-156">Você deverá ver a caixa de diálogo **Novo Projeto** .</span><span class="sxs-lookup"><span data-stu-id="86084-156">You should see the **New Project** dialog box.</span></span>  
2. <span data-ttu-id="86084-157">Na caixa de diálogo **Novo Projeto**, selecione o modelo **DataFactory** e clique em **Projeto Vazio de Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="86084-157">In the **New Project** dialog, select the **DataFactory** template, and click **Empty Data Factory Project**.</span></span>   

    ![Caixa de diálogo Novo projeto](./media/data-factory-build-your-first-pipeline-using-vs/new-project-dialog.png)
3. <span data-ttu-id="86084-159">Insira um **nome** para o projeto, o **local**, um nome para a **solução** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="86084-159">Enter a **name** for the project, **location**, and a name for the **solution**, and click **OK**.</span></span>

    ![Gerenciador de Soluções](./media/data-factory-build-your-first-pipeline-using-vs/solution-explorer.png)

### <a name="create-linked-services"></a><span data-ttu-id="86084-161">Criar serviços vinculados</span><span class="sxs-lookup"><span data-stu-id="86084-161">Create linked services</span></span>
<span data-ttu-id="86084-162">Nesta etapa, você criará dois serviços vinculados: **Armazenamento do Azure** e **HDInsight sob demanda**.</span><span class="sxs-lookup"><span data-stu-id="86084-162">In this step, you create two linked services: **Azure Storage** and **HDInsight on-demand**.</span></span> 

<span data-ttu-id="86084-163">O serviço vinculado ao armazenamento do Azure vincula sua conta de armazenamento do Azure à data factory, fornecendo as informações de conexão.</span><span class="sxs-lookup"><span data-stu-id="86084-163">The Azure Storage linked service links your Azure Storage account to the data factory by providing the connection information.</span></span> <span data-ttu-id="86084-164">O serviço Data Factory usa a cadeia de conexão da configuração de serviço vinculado para se conectar ao armazenamento do Azure em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="86084-164">Data Factory service uses the connection string from the linked service setting to connect to the Azure storage at runtime.</span></span> <span data-ttu-id="86084-165">Esse armazenamento possui dados de entrada e saída para o pipeline e o arquivo de script do hive usado pela atividade de hive.</span><span class="sxs-lookup"><span data-stu-id="86084-165">This storage holds input and output data for the pipeline, and the hive script file used by the hive activity.</span></span> 

<span data-ttu-id="86084-166">Com o serviço vinculado HDInsight sob demanda, o cluster do HDInsight é criado automaticamente em tempo de execução quando os dados de entrada estão prontos para serem processados.</span><span class="sxs-lookup"><span data-stu-id="86084-166">With on-demand HDInsight linked service, The HDInsight cluster is automatically created at runtime when the input data is ready to processed.</span></span> <span data-ttu-id="86084-167">O cluster é excluído após a conclusão do processamento e se mantém ocioso durante o período especificado.</span><span class="sxs-lookup"><span data-stu-id="86084-167">The cluster is deleted after it is done processing and idle for the specified amount of time.</span></span> 

> [!NOTE]
> <span data-ttu-id="86084-168">Você pode criar um data factory, especificando seu nome e as configurações no momento da publicação da solução da sua Data Factory.</span><span class="sxs-lookup"><span data-stu-id="86084-168">You create a data factory by specifying its name and settings at the time of publishing your Data Factory solution.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="86084-169">Criar o serviço vinculado do armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="86084-169">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="86084-170">Clique com o botão direito do mouse em **Serviços Vinculados** no Gerenciador de Soluções, aponte para **Adicionar** e clique em **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="86084-170">Right-click **Linked Services** in the solution explorer, point to **Add**, and click **New Item**.</span></span>      
2. <span data-ttu-id="86084-171">Na caixa de diálogo **Adicionar Novo Item**, selecione **Serviço Vinculado de Armazenamento do Azure** na lista e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="86084-171">In the **Add New Item** dialog box, select **Azure Storage Linked Service** from the list, and click **Add**.</span></span>
    <span data-ttu-id="86084-172">![Serviço vinculado de armazenamento do Azure](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)</span><span class="sxs-lookup"><span data-stu-id="86084-172">![Azure Storage Linked Service](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)</span></span>
3. <span data-ttu-id="86084-173">Substitua `<accountname>` e `<accountkey>` pelo nome e chave da conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="86084-173">Replace `<accountname>` and `<accountkey>` with the name of your Azure storage account and its key.</span></span> <span data-ttu-id="86084-174">Para saber como conseguir sua chave de acesso de armazenamento, consulte as informações sobre como exibir, copiar e regenerar chaves de acesso de armazenamento em [Gerenciar sua conta de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="86084-174">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
    <span data-ttu-id="86084-175">![Serviço vinculado de armazenamento do Azure](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)</span><span class="sxs-lookup"><span data-stu-id="86084-175">![Azure Storage Linked Service](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)</span></span>
4. <span data-ttu-id="86084-176">Salve o arquivo **AzureStorageLinkedService1.json** .</span><span class="sxs-lookup"><span data-stu-id="86084-176">Save the **AzureStorageLinkedService1.json** file.</span></span>

#### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="86084-177">Criar o serviço vinculado do Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="86084-177">Create Azure HDInsight linked service</span></span>
1. <span data-ttu-id="86084-178">No **Gerenciador de Soluções**, clique com botão direito em **Serviços Vinculados**, aponte para **Adicionar** e clique em **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="86084-178">In the **Solution Explorer**, right-click **Linked Services**, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="86084-179">Selecione **erviço Vinculado Sob Demanda do HDInsight**  e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="86084-179">Select **HDInsight On Demand Linked Service**, and click **Add**.</span></span>
3. <span data-ttu-id="86084-180">Substitua o **JSON** pelo seguinte JSON:</span><span class="sxs-lookup"><span data-stu-id="86084-180">Replace the **JSON** with the following JSON:</span></span>

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
                "linkedServiceName": "AzureStorageLinkedService1"
            }
        }
    }
    ```

    <span data-ttu-id="86084-181">A tabela a seguir fornece descrições das propriedades de JSON usadas no trecho de código:</span><span class="sxs-lookup"><span data-stu-id="86084-181">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    <span data-ttu-id="86084-182">Propriedade</span><span class="sxs-lookup"><span data-stu-id="86084-182">Property</span></span> | <span data-ttu-id="86084-183">Descrição</span><span class="sxs-lookup"><span data-stu-id="86084-183">Description</span></span>
    -------- | ----------- 
    <span data-ttu-id="86084-184">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="86084-184">ClusterSize</span></span> | <span data-ttu-id="86084-185">Especifica o tamanho do cluster do HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="86084-185">Specifies the size of the HDInsight Hadoop cluster.</span></span>
    <span data-ttu-id="86084-186">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="86084-186">TimeToLive</span></span> | <span data-ttu-id="86084-187">Especifica que o tempo ocioso do cluster HDInsight antes de ser excluído.</span><span class="sxs-lookup"><span data-stu-id="86084-187">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span></span>
    <span data-ttu-id="86084-188">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="86084-188">linkedServiceName</span></span> | <span data-ttu-id="86084-189">Especifica a conta de armazenamento usada para armazenar os logs gerados pelo cluster do HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="86084-189">Specifies the storage account that is used to store the logs that are generated by HDInsight Hadoop cluster.</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="86084-190">O cluster do HDInsight cria um **contêiner padrão** no armazenamento de blobs especificado no JSON (linkedServiceName).</span><span class="sxs-lookup"><span data-stu-id="86084-190">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (linkedServiceName).</span></span> <span data-ttu-id="86084-191">O HDInsight não exclui esse contêiner quando o cluster é excluído.</span><span class="sxs-lookup"><span data-stu-id="86084-191">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="86084-192">Este comportamento ocorre por design.</span><span class="sxs-lookup"><span data-stu-id="86084-192">This behavior is by design.</span></span> <span data-ttu-id="86084-193">Com o serviço vinculado HDInsight sob demanda, um cluster do HDInsight é criado sempre que uma fatia é processada, a menos que haja um cluster ativo existente (timeToLive).</span><span class="sxs-lookup"><span data-stu-id="86084-193">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (timeToLive).</span></span> <span data-ttu-id="86084-194">O cluster será excluído automaticamente quando o processamento for concluído.</span><span class="sxs-lookup"><span data-stu-id="86084-194">The cluster is automatically deleted when the processing is done.</span></span>
    > 
    > <span data-ttu-id="86084-195">Quanto mais fatias forem processadas, você verá muitos contêineres no armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="86084-195">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="86084-196">Se você não precisa deles para solução de problemas dos trabalhos, convém excluí-los para reduzir o custo de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="86084-196">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="86084-197">Os nomes desses contêineres seguem um padrão: `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="86084-197">The names of these containers follow a pattern: `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp`.</span></span> <span data-ttu-id="86084-198">Use ferramentas como o [Gerenciador de Armazenamento da Microsoft](http://storageexplorer.com/) para excluir contêineres do armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="86084-198">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

    <span data-ttu-id="86084-199">Para obter mais informações sobre as propriedades JSON, confira o artigo [Serviços vinculados de computação](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="86084-199">For more information about JSON properties, see [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article.</span></span> 
4. <span data-ttu-id="86084-200">Salve o arquivo **HDInsightOnDemandLinkedService1.json** .</span><span class="sxs-lookup"><span data-stu-id="86084-200">Save the **HDInsightOnDemandLinkedService1.json** file.</span></span>

### <a name="create-datasets"></a><span data-ttu-id="86084-201">Criar conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="86084-201">Create datasets</span></span>
<span data-ttu-id="86084-202">Nesta etapa, você cria conjuntos de dados para representar dados de entrada e de saída para o processamento do Hive.</span><span class="sxs-lookup"><span data-stu-id="86084-202">In this step, you create datasets to represent the input and output data for Hive processing.</span></span> <span data-ttu-id="86084-203">Esses conjuntos de dados fazem referência ao **StorageLinkedService1** que você criou anteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="86084-203">These datasets refer to the **AzureStorageLinkedService1** you have created earlier in this tutorial.</span></span> <span data-ttu-id="86084-204">O serviço vinculado aponta para uma conta do Armazenamento do Azure e os conjuntos de dados especificam o contêiner, a pasta e o nome do arquivo no armazenamento que contém os dados de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="86084-204">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span></span>   

#### <a name="create-input-dataset"></a><span data-ttu-id="86084-205">Criar conjunto de dados de entrada</span><span class="sxs-lookup"><span data-stu-id="86084-205">Create input dataset</span></span>
1. <span data-ttu-id="86084-206">No **Gerenciador de Soluções**, clique com botão direito em **Tabelas**, aponte para **Adicionar**e clique em **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="86084-206">In the **Solution Explorer**, right-click **Tables**, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="86084-207">Selecione o **Blob do Azure** na lista, altere o nome do arquivo para **InputDataSet.json** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="86084-207">Select **Azure Blob** from the list, change the name of the file to **InputDataSet.json**, and click **Add**.</span></span>
3. <span data-ttu-id="86084-208">Substitua o **JSON** no editor pelo seguinte trecho de código JSON:</span><span class="sxs-lookup"><span data-stu-id="86084-208">Replace the **JSON** in the editor with the following JSON snippet:</span></span>

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
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
    <span data-ttu-id="86084-209">Este trecho de JSON define um conjunto de dados chamado **AzureBlobInput** que representa dados de entrada para a atividade de hive no pipeline.</span><span class="sxs-lookup"><span data-stu-id="86084-209">This JSON snippet defines a dataset called **AzureBlobInput** that represents input data for the hive activity in the pipeline.</span></span> <span data-ttu-id="86084-210">Além disso, você especifica que os dados de entrada estão localizados no contêiner de blobs chamado `adfgetstarted` e na pasta chamada `inputdata`.</span><span class="sxs-lookup"><span data-stu-id="86084-210">You specify that the input data is located in the blob container called `adfgetstarted` and the folder called `inputdata`.</span></span>

    <span data-ttu-id="86084-211">A tabela a seguir fornece descrições das propriedades de JSON usadas no trecho de código:</span><span class="sxs-lookup"><span data-stu-id="86084-211">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    <span data-ttu-id="86084-212">Propriedade</span><span class="sxs-lookup"><span data-stu-id="86084-212">Property</span></span> | <span data-ttu-id="86084-213">Descrição</span><span class="sxs-lookup"><span data-stu-id="86084-213">Description</span></span> |
    -------- | ----------- |
    <span data-ttu-id="86084-214">type</span><span class="sxs-lookup"><span data-stu-id="86084-214">type</span></span> |<span data-ttu-id="86084-215">A propriedade de tipo é definida como **AzureBlob** porque os dados residem no armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="86084-215">The type property is set to **AzureBlob** because data resides in Azure Blob Storage.</span></span>
    <span data-ttu-id="86084-216">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="86084-216">linkedServiceName</span></span> | <span data-ttu-id="86084-217">Refere-se ao AzureStorageLinkedService1 que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="86084-217">Refers to the AzureStorageLinkedService1 you created earlier.</span></span>
    <span data-ttu-id="86084-218">fileName</span><span class="sxs-lookup"><span data-stu-id="86084-218">fileName</span></span> |<span data-ttu-id="86084-219">Essa propriedade é opcional.</span><span class="sxs-lookup"><span data-stu-id="86084-219">This property is optional.</span></span> <span data-ttu-id="86084-220">Se você omitir essa propriedade, todos os arquivos de folderPath serão selecionados.</span><span class="sxs-lookup"><span data-stu-id="86084-220">If you omit this property, all the files from the folderPath are picked.</span></span> <span data-ttu-id="86084-221">Nesse caso, somente o input.log será processado.</span><span class="sxs-lookup"><span data-stu-id="86084-221">In this case, only the input.log is processed.</span></span>
    <span data-ttu-id="86084-222">type</span><span class="sxs-lookup"><span data-stu-id="86084-222">type</span></span> | <span data-ttu-id="86084-223">Os arquivos de log estão em formato de texto, então utilizaremos TextFormat.</span><span class="sxs-lookup"><span data-stu-id="86084-223">The log files are in text format, so we use TextFormat.</span></span> |
    <span data-ttu-id="86084-224">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="86084-224">columnDelimiter</span></span> | <span data-ttu-id="86084-225">as colunas nos arquivos de log são delimitadas pelo caractere de vírgula (`,`)</span><span class="sxs-lookup"><span data-stu-id="86084-225">columns in the log files are delimited by the comma character (`,`)</span></span>
    <span data-ttu-id="86084-226">frequência/intervalo</span><span class="sxs-lookup"><span data-stu-id="86084-226">frequency/interval</span></span> | <span data-ttu-id="86084-227">a frequência é definida como Mês e o intervalo como 1, o que significa que as fatias de entrada estão disponíveis mensalmente.</span><span class="sxs-lookup"><span data-stu-id="86084-227">frequency set to Month and interval is 1, which means that the input slices are available monthly.</span></span>
    <span data-ttu-id="86084-228">externo</span><span class="sxs-lookup"><span data-stu-id="86084-228">external</span></span> | <span data-ttu-id="86084-229">Se os dados de entrada para a atividade não forem gerados pelo pipeline, essa propriedade será definida como verdadeira.</span><span class="sxs-lookup"><span data-stu-id="86084-229">This property is set to true if the input data for the activity is not generated by the pipeline.</span></span> <span data-ttu-id="86084-230">Essa propriedade só é especificada em conjuntos de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="86084-230">This property is only specified on input datasets.</span></span> <span data-ttu-id="86084-231">O conjunto de dados de entrada da primeira atividade sempre será definido como verdadeiro.</span><span class="sxs-lookup"><span data-stu-id="86084-231">For the input dataset of the first activity, always set it to true.</span></span>
4. <span data-ttu-id="86084-232">Salve o arquivo **InputDataset.json** .</span><span class="sxs-lookup"><span data-stu-id="86084-232">Save the **InputDataset.json** file.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="86084-233">Criar conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="86084-233">Create output dataset</span></span>
<span data-ttu-id="86084-234">Agora, você cria o conjunto de dados de saída para representar os dados de saída armazenados no armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="86084-234">Now, you create the output dataset to represent output data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="86084-235">No **Gerenciador de Soluções**, clique com botão direito em **Tabelas**, aponte para **Adicionar**e clique em **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="86084-235">In the **Solution Explorer**, right-click **tables**, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="86084-236">Selecione **Blob do Azure** na lista, altere o nome do arquivo para **OutputDataset.json** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="86084-236">Select **Azure Blob** from the list, change the name of the file to **OutputDataset.json**, and click **Add**.</span></span>
3. <span data-ttu-id="86084-237">Substitua o **JSON** no editor pelo seguinte JSON:</span><span class="sxs-lookup"><span data-stu-id="86084-237">Replace the **JSON** in the editor with the following JSON:</span></span>
    
    ```json
    {
        "name": "AzureBlobOutput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
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
    <span data-ttu-id="86084-238">O trecho JSON define um conjunto de dados chamado **AzureBlobOutput** que representa os dados de saída produzidos pela atividade de hive no pipeline.</span><span class="sxs-lookup"><span data-stu-id="86084-238">The JSON snippet defines a dataset called **AzureBlobOutput** that represents output data produced by the hive activity in the pipeline.</span></span> <span data-ttu-id="86084-239">Você especifica que os dados de saída produzidos pela atividade de hive são colocados no contêiner de blobs `adfgetstarted` e na pasta `partitioneddata`.</span><span class="sxs-lookup"><span data-stu-id="86084-239">You specify that the output data is produced by the hive activity is placed in the blob container called `adfgetstarted` and the folder called `partitioneddata`.</span></span> 
    
    <span data-ttu-id="86084-240">A seção **availability** especifica que o conjunto de dados de saída é produzido mensalmente.</span><span class="sxs-lookup"><span data-stu-id="86084-240">The **availability** section specifies that the output dataset is produced on a monthly basis.</span></span> <span data-ttu-id="86084-241">O conjunto de dados de saída conduzem a agenda do pipeline.</span><span class="sxs-lookup"><span data-stu-id="86084-241">The output dataset drives the schedule of the pipeline.</span></span> <span data-ttu-id="86084-242">O pipeline é executado mensalmente entre suas horas de início e término.</span><span class="sxs-lookup"><span data-stu-id="86084-242">The pipeline runs monthly between its start and end times.</span></span> 

    <span data-ttu-id="86084-243">Consulte a seção **Criar o conjunto de dados de entrada** para obter descrições dessas propriedades.</span><span class="sxs-lookup"><span data-stu-id="86084-243">See **Create the input dataset** section for descriptions of these properties.</span></span> <span data-ttu-id="86084-244">Você não define a propriedade externa em um conjunto de dados de saída porque o conjunto de dados é produzido pelo pipeline.</span><span class="sxs-lookup"><span data-stu-id="86084-244">You do not set the external property on an output dataset as the dataset is produced by the pipeline.</span></span>
4. <span data-ttu-id="86084-245">Salve o arquivo **OutputDataset.json** .</span><span class="sxs-lookup"><span data-stu-id="86084-245">Save the **OutputDataset.json** file.</span></span>

### <a name="create-pipeline"></a><span data-ttu-id="86084-246">Criar um pipeline</span><span class="sxs-lookup"><span data-stu-id="86084-246">Create pipeline</span></span>
<span data-ttu-id="86084-247">Até o momento, você criou o serviço vinculado do armazenamento do Azure e conjuntos de dados de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="86084-247">You have created the Azure Storage linked service, and input and output datasets so far.</span></span> <span data-ttu-id="86084-248">Agora, você pode criar um pipeline com uma atividade **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="86084-248">Now, you create a pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="86084-249">A **entrada** para a atividade de hive é definida como **AzureBlobInput** e a**saída**, como **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="86084-249">The **input** for the hive activity is set to **AzureBlobInput** and **output** is set to **AzureBlobOutput**.</span></span> <span data-ttu-id="86084-250">Uma fatia de um conjunto de dados de entrada e de saída são disponibilizados mensalmente (frequência: mês, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="86084-250">A slice of an input dataset is available monthly (frequency: Month, interval: 1), and the output slice is produced monthly too.</span></span> 

1. <span data-ttu-id="86084-251">No **Gerenciador de Soluções**, clique com botão direito em **Pipelines**, aponte para **Adicionar** e clique em **Novo Item.**</span><span class="sxs-lookup"><span data-stu-id="86084-251">In the **Solution Explorer**, right-click **Pipelines**, point to **Add**, and click **New Item.**</span></span>
2. <span data-ttu-id="86084-252">Selecione **Pipeline de Transformação do Hive** na lista e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="86084-252">Select **Hive Transformation Pipeline** from the list, and click **Add**.</span></span>
3. <span data-ttu-id="86084-253">Substitua o **JSON** pelo trecho a seguir:</span><span class="sxs-lookup"><span data-stu-id="86084-253">Replace the **JSON** with the following snippet:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="86084-254">Substitua `<storageaccountname>` com o nome da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="86084-254">Replace `<storageaccountname>` with the name of your storage account.</span></span>

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
                        "scriptLinkedService": "AzureStorageLinkedService1",
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
            "start": "2016-04-01T00:00:00Z",
            "end": "2016-04-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="86084-255">Substitua `<storageaccountname>` com o nome da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="86084-255">Replace `<storageaccountname>` with the name of your storage account.</span></span>

    <span data-ttu-id="86084-256">O trecho JSON define um pipeline que consiste em uma única atividade (atividade de hive).</span><span class="sxs-lookup"><span data-stu-id="86084-256">The JSON snippet defines a pipeline that consists of a single activity (Hive Activity).</span></span> <span data-ttu-id="86084-257">Esta atividade executa um script de hive para processar dados de entrada em um cluster do HDInsight sob demanda para gerar dados de saída.</span><span class="sxs-lookup"><span data-stu-id="86084-257">This activity runs a Hive script to process input data on an on-demand HDInsight cluster to produce output data.</span></span> <span data-ttu-id="86084-258">Na seção de atividades do pipeline JSON, você verá apenas uma atividade na matriz com o tipo definido como **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="86084-258">In the activities section of the pipeline JSON, you see only one activity in the array with type set to **HDInsightHive**.</span></span> 

    <span data-ttu-id="86084-259">Nas propriedades de tipo especificados para a atividade de Hive do HDInsight, você especifica o caminho, os parâmetros e qual serviço vinculado de armazenamento do Azure tem o arquivo de script do hive.</span><span class="sxs-lookup"><span data-stu-id="86084-259">In the type properties that are specific to HDInsight Hive activity, you specify what Azure Storage linked service has the hive script file, the path to the script file, and parameters to the script file.</span></span> 

    <span data-ttu-id="86084-260">O arquivo de script do Hive, **partitionweblogs.hql**, é armazenado na conta de armazenamento do Azure (especificada pelo scriptLinkedService) e na pasta `script` no contêiner `adfgetstarted`.</span><span class="sxs-lookup"><span data-stu-id="86084-260">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService), and in the `script` folder in the container `adfgetstarted`.</span></span>

    <span data-ttu-id="86084-261">A seção `defines` é usada para especificar as configurações de tempo de execução passadas para o script do hive como valores de configuração de Hive (por exemplo, `${hiveconf:inputtable}`, `${hiveconf:partitionedtable})`).</span><span class="sxs-lookup"><span data-stu-id="86084-261">The `defines` section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable})`.</span></span>

    <span data-ttu-id="86084-262">As propriedades **start** e **end** do pipeline especificam o período ativo do pipeline.</span><span class="sxs-lookup"><span data-stu-id="86084-262">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span></span> <span data-ttu-id="86084-263">Você configurou o conjunto de dados a ser produzido mensalmente, portanto, apenas uma fatia será produzida pelo pipeline (porque o mês é o mesmo nas datas de início e término).</span><span class="sxs-lookup"><span data-stu-id="86084-263">You configured the dataset to be produced monthly, therefore, only once slice is produced by the pipeline (because the month is same in start and end dates).</span></span>

    <span data-ttu-id="86084-264">Na atividade do JSON, você especifica que o script do Hive é executado na máquina especificada pelo **nomeServiçoVinculado** – **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="86084-264">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>
4. <span data-ttu-id="86084-265">Salve o arquivo **HiveActivity1.json** .</span><span class="sxs-lookup"><span data-stu-id="86084-265">Save the **HiveActivity1.json** file.</span></span>

### <a name="add-partitionweblogshql-and-inputlog-as-a-dependency"></a><span data-ttu-id="86084-266">Adicionar partitionweblogs.hql e input.log como uma dependência</span><span class="sxs-lookup"><span data-stu-id="86084-266">Add partitionweblogs.hql and input.log as a dependency</span></span>
1. <span data-ttu-id="86084-267">Clique com botão direito em **Dependências** na janela do **Gerenciador de Soluções**, aponte para **Adicionar**e clique em **Item Existente**.</span><span class="sxs-lookup"><span data-stu-id="86084-267">Right-click **Dependencies** in the **Solution Explorer** window, point to **Add**, and click **Existing Item**.</span></span>  
2. <span data-ttu-id="86084-268">Navegue até **C:\ADFGettingStarted** e selecione os arquivos **partitionweblogs.hql** e **input.log**, e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="86084-268">Navigate to the **C:\ADFGettingStarted** and select **partitionweblogs.hql**, **input.log** files, and click **Add**.</span></span> <span data-ttu-id="86084-269">Você criou esses dois arquivos como parte dos pré-requisitos da [Visão Geral do Tutorial](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="86084-269">You created these two files as part of prerequisites from the [Tutorial Overview](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="86084-270">Quando você publicar a solução na próxima etapa, o arquivo **partitionweblogs.hql** será carregado para a pasta de **script** no contêiner de blobs `adfgetstarted`.</span><span class="sxs-lookup"><span data-stu-id="86084-270">When you publish the solution in the next step, the **partitionweblogs.hql** file is uploaded to the **script** folder in the `adfgetstarted` blob container.</span></span>   

### <a name="publishdeploy-data-factory-entities"></a><span data-ttu-id="86084-271">Publicar/implantar entidades de data factory</span><span class="sxs-lookup"><span data-stu-id="86084-271">Publish/deploy Data Factory entities</span></span>
<span data-ttu-id="86084-272">Nesta etapa, você pode publicar as entidades da Data Factory (serviços vinculados, conjuntos de dados e pipeline) no seu projeto para o serviço Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="86084-272">In this step, you publish the Data Factory entities (linked services, datasets, and pipeline) in your project to the Azure Data Factory service.</span></span> <span data-ttu-id="86084-273">No processo de publicação, você deve especificar o nome da sua data factory.</span><span class="sxs-lookup"><span data-stu-id="86084-273">In the process of publishing, you specify the name for your data factory.</span></span> 

1. <span data-ttu-id="86084-274">No Gerenciador de Soluções, clique com o botão direito do mouse no projeto e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="86084-274">Right-click project in the Solution Explorer, and click **Publish**.</span></span>
2. <span data-ttu-id="86084-275">Se a caixa de diálogo **Entrar na sua conta da Microsoft** for exibida, insira as credenciais da conta com a assinatura do Azure e clique em **entrar**.</span><span class="sxs-lookup"><span data-stu-id="86084-275">If you see **Sign in to your Microsoft account** dialog box, enter your credentials for the account that has Azure subscription, and click **sign in**.</span></span>
3. <span data-ttu-id="86084-276">Você deve ver a caixa de diálogo a seguir:</span><span class="sxs-lookup"><span data-stu-id="86084-276">You should see the following dialog box:</span></span>

   ![Caixa de diálogo Publicar](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
4. <span data-ttu-id="86084-278">Na página **Configurar data factory**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="86084-278">In the **Configure data factory** page, do the following steps:</span></span>

    ![Publicação - configurações da nova data factory](media/data-factory-build-your-first-pipeline-using-vs/publish-new-data-factory.png)

   1. <span data-ttu-id="86084-280">Selecione a opção **Criar Nova Data Factory** .</span><span class="sxs-lookup"><span data-stu-id="86084-280">select **Create New Data Factory** option.</span></span>
   2. <span data-ttu-id="86084-281">Insira um **nome** exclusivo para o armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="86084-281">Enter a unique **name** for the data factory.</span></span> <span data-ttu-id="86084-282">Por exemplo: **DataFactoryUsingVS09152016**.</span><span class="sxs-lookup"><span data-stu-id="86084-282">For example: **DataFactoryUsingVS09152016**.</span></span> <span data-ttu-id="86084-283">O nome deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="86084-283">The name must be globally unique.</span></span>
   3. <span data-ttu-id="86084-284">Selecione a assinatura certa para o campo **Assinatura** .</span><span class="sxs-lookup"><span data-stu-id="86084-284">Select the right subscription for the **Subscription** field.</span></span> 
        > [!IMPORTANT]
        > <span data-ttu-id="86084-285">Se você não vir nenhuma assinatura, verifique se está conectado usando uma conta que seja administrador ou coadministrador da assinatura.</span><span class="sxs-lookup"><span data-stu-id="86084-285">If you do not see any subscription, ensure that you logged in using an account that is an admin or co-admin of the subscription.</span></span>
   4. <span data-ttu-id="86084-286">Selecione o **grupo de recursos** para o data factory a ser criado.</span><span class="sxs-lookup"><span data-stu-id="86084-286">Select the **resource group** for the data factory to be created.</span></span>
   5. <span data-ttu-id="86084-287">Selecione a **região** do data factory.</span><span class="sxs-lookup"><span data-stu-id="86084-287">Select the **region** for the data factory.</span></span>
   6. <span data-ttu-id="86084-288">Clique em **Avançar** para alternar para a página **Publicar Itens**.</span><span class="sxs-lookup"><span data-stu-id="86084-288">Click **Next** to switch to the **Publish Items** page.</span></span> <span data-ttu-id="86084-289">(Pressione **TAB** para sair do campo Nome se o botão **Avançar** estiver desabilitado).</span><span class="sxs-lookup"><span data-stu-id="86084-289">(Press **TAB** to move out of the Name field to if the **Next** button is disabled.)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="86084-290">Se você receber o erro **O nome da data factory “DataFactoryUsingVS” não está disponível** durante a publicação, altere o nome (por exemplo, yournameDataFactoryUsingVS).</span><span class="sxs-lookup"><span data-stu-id="86084-290">If you receive the error **Data factory name “DataFactoryUsingVS” is not available** when publishing, change the name (for example, yournameDataFactoryUsingVS).</span></span> <span data-ttu-id="86084-291">Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="86084-291">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>   
1. <span data-ttu-id="86084-292">Na página **Publicar Itens**, verifique se todas as entidades de Data Factories estão selecionadas e clique em **Avançar** para alternar para a página **Resumo**.</span><span class="sxs-lookup"><span data-stu-id="86084-292">In the **Publish Items** page, ensure that all the Data Factories entities are selected, and click **Next** to switch to the **Summary** page.</span></span>

    ![Publicar página de item](media/data-factory-build-your-first-pipeline-using-vs/publish-items-page.png)     
2. <span data-ttu-id="86084-294">Examine o resumo e clique em **Avançar** para iniciar o processo de implantação e exibir o **Status da Implantação**.</span><span class="sxs-lookup"><span data-stu-id="86084-294">Review the summary and click **Next** to start the deployment process and view the **Deployment Status**.</span></span>

    ![Página Resumo](media/data-factory-build-your-first-pipeline-using-vs/summary-page.png)
3. <span data-ttu-id="86084-296">Na página **Status da Implantação** , você deve ver o status do processo de implantação.</span><span class="sxs-lookup"><span data-stu-id="86084-296">In the **Deployment Status** page, you should see the status of the deployment process.</span></span> <span data-ttu-id="86084-297">Clique em Concluir depois que a implantação tiver terminado.</span><span class="sxs-lookup"><span data-stu-id="86084-297">Click Finish after the deployment is done.</span></span>

<span data-ttu-id="86084-298">Pontos importantes a serem considerados:</span><span class="sxs-lookup"><span data-stu-id="86084-298">Important points to note:</span></span>

- <span data-ttu-id="86084-299">Se você receber o erro: **Esta assinatura não está registrada para usar o namespace Microsoft.DataFactory**, siga um desses procedimentos e tente publicar novamente:</span><span class="sxs-lookup"><span data-stu-id="86084-299">If you receive the error: **This subscription is not registered to use namespace Microsoft.DataFactory**, do one of the following and try publishing again:</span></span>
    - <span data-ttu-id="86084-300">No Azure PowerShell, execute o comando a seguir para registrar o provedor do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="86084-300">In Azure PowerShell, run the following command to register the Data Factory provider.</span></span>
        ```PowerShell   
        Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
        ```
        <span data-ttu-id="86084-301">Você pode executar o comando a seguir para confirmar se o provedor do Data Factory está registrado.</span><span class="sxs-lookup"><span data-stu-id="86084-301">You can run the following command to confirm that the Data Factory provider is registered.</span></span>

        ```PowerShell
        Get-AzureRmResourceProvider
        ```
    - <span data-ttu-id="86084-302">Faça logon no [portal do Azure](https://portal.azure.com) usando a assinatura do Azure e navegue até uma folha do Data Factory (ou) crie um data factory no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="86084-302">Login using the Azure subscription in to the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="86084-303">Essa ação registra automaticamente o provedor para você.</span><span class="sxs-lookup"><span data-stu-id="86084-303">This action automatically registers the provider for you.</span></span>
- <span data-ttu-id="86084-304">O nome do data factory pode ser registrado futuramente como um nome DNS e tornar-se publicamente visível.</span><span class="sxs-lookup"><span data-stu-id="86084-304">The name of the data factory may be registered as a DNS name in the future and hence become publically visible.</span></span>
- <span data-ttu-id="86084-305">Para criar instâncias do Data Factory, você precisa ser administrador ou coadministrador da assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="86084-305">To create Data Factory instances, you need to be an admin or co-admin of the Azure subscription</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="86084-306">Monitorar o pipeline</span><span class="sxs-lookup"><span data-stu-id="86084-306">Monitor pipeline</span></span>
<span data-ttu-id="86084-307">Nesta etapa, você deve monitorar o pipeline usando o modo de exibição de diagrama da data factory.</span><span class="sxs-lookup"><span data-stu-id="86084-307">In this step, you monitor the pipeline using Diagram View of the data factory.</span></span> 

#### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="86084-308">Monitorar o pipeline usando a Exibição de Diagrama</span><span class="sxs-lookup"><span data-stu-id="86084-308">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="86084-309">Faça logon no [portal do Azure](https://portal.azure.com/), siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="86084-309">Log in to the [Azure portal](https://portal.azure.com/), do the following steps:</span></span>
   1. <span data-ttu-id="86084-310">Clique em **Mais serviços** e **Data factories**.</span><span class="sxs-lookup"><span data-stu-id="86084-310">Click **More services** and click **Data factories**.</span></span>
       
        ![Procurar data factories](./media/data-factory-build-your-first-pipeline-using-vs/browse-datafactories.png)
   2. <span data-ttu-id="86084-312">Selecione o nome da sua data factory (por exemplo: **DataFactoryUsingVS09152016**) da lista de data factories.</span><span class="sxs-lookup"><span data-stu-id="86084-312">Select the name of your data factory (for example: **DataFactoryUsingVS09152016**) from the list of data factories.</span></span>
   
       ![Selecionar o data factory](./media/data-factory-build-your-first-pipeline-using-vs/select-first-data-factory.png)
2. <span data-ttu-id="86084-314">Na home page do seu data factory, clique em **Diagrama**.</span><span class="sxs-lookup"><span data-stu-id="86084-314">In the home page for your data factory, click **Diagram**.</span></span>

    ![Bloco do diagrama](./media/data-factory-build-your-first-pipeline-using-vs/diagram-tile.png)
3. <span data-ttu-id="86084-316">Na Exibição de Diagrama, você tem uma visão geral dos pipelines e dos conjuntos de dados usados neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="86084-316">In the Diagram View, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>

    ![Exibição de diagrama](./media/data-factory-build-your-first-pipeline-using-vs/diagram-view-2.png)
4. <span data-ttu-id="86084-318">Para exibir todas as atividades no pipeline, clique com o botão direito do mouse no pipeline no diagrama e clique em Abrir Pipeline.</span><span class="sxs-lookup"><span data-stu-id="86084-318">To view all activities in the pipeline, right-click pipeline in the diagram and click Open Pipeline.</span></span>

    ![Menu do pipeline aberto](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-menu.png)
5. <span data-ttu-id="86084-320">Confirme que você vê a atividade HDInsightHive no pipeline.</span><span class="sxs-lookup"><span data-stu-id="86084-320">Confirm that you see the HDInsightHive activity in the pipeline.</span></span>

    ![Abrir a exibição do pipeline](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-view.png)

    <span data-ttu-id="86084-322">Para navegar de volta ao modo de exibição anterior, clique em **Data factory** no menu de atalho na parte superior.</span><span class="sxs-lookup"><span data-stu-id="86084-322">To navigate back to the previous view, click **Data factory** in the breadcrumb menu at the top.</span></span>
6. <span data-ttu-id="86084-323">Na **Exibição do Diagrama**, clique duas vezes no conjunto de dados **AzureBlobInput**.</span><span class="sxs-lookup"><span data-stu-id="86084-323">In the **Diagram View**, double-click the dataset **AzureBlobInput**.</span></span> <span data-ttu-id="86084-324">Confirme se a fatia está no estado **Pronto** .</span><span class="sxs-lookup"><span data-stu-id="86084-324">Confirm that the slice is in **Ready** state.</span></span> <span data-ttu-id="86084-325">Pode levar alguns minutos para que a fatia apareça no estado Pronto.</span><span class="sxs-lookup"><span data-stu-id="86084-325">It may take a couple of minutes for the slice to show up in Ready state.</span></span> <span data-ttu-id="86084-326">Se isso não acontecer depois de algum tempo, veja se o arquivo de entrada (input.log) está posicionado no contêiner à direita (`adfgetstarted`) e na pasta (`inputdata`).</span><span class="sxs-lookup"><span data-stu-id="86084-326">If it does not happen after you wait for sometime, see if you have the input file (input.log) placed in the right container (`adfgetstarted`) and folder (`inputdata`).</span></span> <span data-ttu-id="86084-327">E confira se a propriedade **externa** no conjunto de dados de entrada está definida como **verdadeira**.</span><span class="sxs-lookup"><span data-stu-id="86084-327">And, make sure that the **external** property on the input dataset is set to **true**.</span></span> 

   ![Fatia de entrada no estado pronto](./media/data-factory-build-your-first-pipeline-using-vs/input-slice-ready.png)
7. <span data-ttu-id="86084-329">Clique em **X** para fechar a folha **AzureBlobInput**.</span><span class="sxs-lookup"><span data-stu-id="86084-329">Click **X** to close **AzureBlobInput** blade.</span></span>
8. <span data-ttu-id="86084-330">Na **Exibição do Diagrama**, clique duas vezes no conjunto de dados **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="86084-330">In the **Diagram View**, double-click the dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="86084-331">Você verá a fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="86084-331">You see that the slice that is currently being processed.</span></span>

   ![Conjunto de dados](./media/data-factory-build-your-first-pipeline-using-vs/dataset-blade.png)
9. <span data-ttu-id="86084-333">Quando o processamento for concluído, você verá a fatia no estado **Pronto** .</span><span class="sxs-lookup"><span data-stu-id="86084-333">When processing is done, you see the slice in **Ready** state.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="86084-334">A criação de um cluster do HDInsight sob demanda geralmente leva algum tempo (20 minutos, aproximadamente).</span><span class="sxs-lookup"><span data-stu-id="86084-334">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="86084-335">Portanto, espere que o pipeline demore **cerca de 30 minutos** para processar a fatia.</span><span class="sxs-lookup"><span data-stu-id="86084-335">Therefore, expect the pipeline to take **approximately 30 minutes** to process the slice.</span></span>  
   
    ![Conjunto de dados](./media/data-factory-build-your-first-pipeline-using-vs/dataset-slice-ready.png)    
10. <span data-ttu-id="86084-337">Quando a fatia estiver no estado **Pronto**, verifique a pasta `partitioneddata` no contêiner `adfgetstarted` em seu armazenamento de blobs para os dados de saída.</span><span class="sxs-lookup"><span data-stu-id="86084-337">When the slice is in **Ready** state, check the `partitioneddata` folder in the `adfgetstarted` container in your blob storage for the output data.</span></span>  

    ![dados de saída](./media/data-factory-build-your-first-pipeline-using-vs/three-ouptut-files.png)
11. <span data-ttu-id="86084-339">Clique na fatia para ver detalhes sobre ela em uma folha **Fatia de dados** .</span><span class="sxs-lookup"><span data-stu-id="86084-339">Click the slice to see details about it in a **Data slice** blade.</span></span>

    ![Detalhes da fatia de dados](./media/data-factory-build-your-first-pipeline-using-vs/data-slice-details.png)  
12. <span data-ttu-id="86084-341">Clique em uma execução da atividade na **Lista de execuções da atividade** para ver detalhes sobre uma execução da atividade (atividade de Hive em nosso cenário) em uma janela **Detalhes de execução da atividade**.</span><span class="sxs-lookup"><span data-stu-id="86084-341">Click an activity run in the **Activity runs list** to see details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span></span> 
  
    ![Detalhes da execução da atividade](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-blade.png)    

    <span data-ttu-id="86084-343">Nos arquivos de log, você pode ver a consulta do Hive executada e as informações de status.</span><span class="sxs-lookup"><span data-stu-id="86084-343">From the log files, you can see the Hive query that was executed and status information.</span></span> <span data-ttu-id="86084-344">Esses logs são úteis para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="86084-344">These logs are useful for troubleshooting any issues.</span></span>  

<span data-ttu-id="86084-345">Confira [Monitorar os conjuntos de dados e o pipeline](data-factory-monitor-manage-pipelines.md) para obter instruções sobre como usar o Portal do Azure para monitorar o pipeline e os conjuntos de dados que você criou neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="86084-345">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how to use the Azure portal to monitor the pipeline and datasets you have created in this tutorial.</span></span>

#### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="86084-346">Monitorar o pipeline usando o aplicativo Monitorar e Gerenciar</span><span class="sxs-lookup"><span data-stu-id="86084-346">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="86084-347">Você também pode usar o aplicativo Monitorar e Gerenciar para monitorar os pipelines.</span><span class="sxs-lookup"><span data-stu-id="86084-347">You can also use Monitor & Manage application to monitor your pipelines.</span></span> <span data-ttu-id="86084-348">Para obter informações detalhadas sobre como usar esse aplicativo, veja [Monitorar e gerenciar confira do Azure Data Factory usando o aplicativo Monitorar e Gerenciar](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="86084-348">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="86084-349">Clique no bloco Monitorar e Gerenciar.</span><span class="sxs-lookup"><span data-stu-id="86084-349">Click Monitor & Manage tile.</span></span>

    ![Bloco Monitorar e Gerenciar](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-tile.png)
2. <span data-ttu-id="86084-351">Você deve ver o aplicativo Monitorar e Gerenciar.</span><span class="sxs-lookup"><span data-stu-id="86084-351">You should see Monitor & Manage application.</span></span> <span data-ttu-id="86084-352">Altere a **Hora de início** e a **Hora de término** para coincidir com o início (04-01-2016 12:00 AM) e o término (04-02-2016 12:00 AM) do seu pipeline, e clique **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="86084-352">Change the **Start time** and **End time** to match start (04-01-2016 12:00 AM) and end times (04-02-2016 12:00 AM) of your pipeline, and click **Apply**.</span></span>

    ![Aplicativo Monitorar e Gerenciar](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-app.png)
3. <span data-ttu-id="86084-354">Para ver detalhes sobre uma janela de atividade, selecione-a na **Lista de janela de atividade**.</span><span class="sxs-lookup"><span data-stu-id="86084-354">To see details about an activity window, select it in the **Activity Windows list** to see details about it.</span></span>
    <span data-ttu-id="86084-355">![Detalhes da janela Atividade](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)</span><span class="sxs-lookup"><span data-stu-id="86084-355">![Activity window details](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="86084-356">O arquivo de entrada é excluído quando a fatia é processada com êxito.</span><span class="sxs-lookup"><span data-stu-id="86084-356">The input file gets deleted when the slice is processed successfully.</span></span> <span data-ttu-id="86084-357">Portanto, se você quiser executar novamente a fatia ou fazer o tutorial novamente, carregue o arquivo de entrada (input.log) na pasta `inputdata` do contêiner `adfgetstarted`.</span><span class="sxs-lookup"><span data-stu-id="86084-357">Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the `inputdata` folder of the `adfgetstarted` container.</span></span>

### <a name="additional-notes"></a><span data-ttu-id="86084-358">Observações adicionais</span><span class="sxs-lookup"><span data-stu-id="86084-358">Additional notes</span></span>
- <span data-ttu-id="86084-359">Uma fábrica de dados pode ter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="86084-359">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="86084-360">Um pipeline em um data factory pode ter uma ou mais atividades.</span><span class="sxs-lookup"><span data-stu-id="86084-360">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="86084-361">Por exemplo, uma Atividade de Cópia para copiar dados de um armazenamento de dados de origem para um de destino e uma atividade do Hive do HDInsight para executar um script do Hive para transformar dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="86084-361">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data.</span></span> <span data-ttu-id="86084-362">Confira [repositórios de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats) para ver todas as fontes e coletores com suporte da Atividade de Cópia.</span><span class="sxs-lookup"><span data-stu-id="86084-362">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all the sources and sinks supported by the Copy Activity.</span></span> <span data-ttu-id="86084-363">Confira os [serviços vinculados de computação](data-factory-compute-linked-services.md) para ver uma lista dos serviços de computação com suporte do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="86084-363">See [compute linked services](data-factory-compute-linked-services.md) for the list of compute services supported by Data Factory.</span></span>
- <span data-ttu-id="86084-364">Serviços vinculados vinculam armazenamentos de dados ou serviços de computação para uma data factory do Azure.</span><span class="sxs-lookup"><span data-stu-id="86084-364">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="86084-365">Confira [repositórios de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats) para ver todas as fontes e coletores com suporte da Atividade de Cópia.</span><span class="sxs-lookup"><span data-stu-id="86084-365">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all the sources and sinks supported by the Copy Activity.</span></span> <span data-ttu-id="86084-366">Confira os [Serviços vinculados de computação](data-factory-compute-linked-services.md) para obter a lista de serviços de computação com suporte pela Data Factory e as [Atividades de transformação](data-factory-data-transformation-activities.md) que podem ser executadas neles.</span><span class="sxs-lookup"><span data-stu-id="86084-366">See [compute linked services](data-factory-compute-linked-services.md) for the list of compute services supported by Data Factory and [transformation activities](data-factory-data-transformation-activities.md) that can run on them.</span></span>
- <span data-ttu-id="86084-367">Confira [Como mover dados de/para Blobs do Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) para obter detalhes sobre as propriedades JSON usadas no armazenamento do Azure vinculado à definição de serviço.</span><span class="sxs-lookup"><span data-stu-id="86084-367">See [Move data from/to Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used in the Azure Storage linked service definition.</span></span>
- <span data-ttu-id="86084-368">Você pode usar seu próprio cluster do HDInsight em vez de usar um cluster do HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="86084-368">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="86084-369">Veja [Serviços vinculados de computação](data-factory-compute-linked-services.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="86084-369">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>
-  <span data-ttu-id="86084-370">O Data Factory cria um cluster HDInsight **baseado no Linux** para você com o JSON anterior.</span><span class="sxs-lookup"><span data-stu-id="86084-370">The Data Factory creates a **Linux-based** HDInsight cluster for you with the preceding JSON.</span></span> <span data-ttu-id="86084-371">Confira [Serviço vinculado do HDInsight sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="86084-371">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
- <span data-ttu-id="86084-372">O cluster do HDInsight cria um **contêiner padrão** no armazenamento de blobs especificado no JSON (linkedServiceName).</span><span class="sxs-lookup"><span data-stu-id="86084-372">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (linkedServiceName).</span></span> <span data-ttu-id="86084-373">O HDInsight não exclui esse contêiner quando o cluster é excluído.</span><span class="sxs-lookup"><span data-stu-id="86084-373">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="86084-374">Este comportamento ocorre por design.</span><span class="sxs-lookup"><span data-stu-id="86084-374">This behavior is by design.</span></span> <span data-ttu-id="86084-375">Com o serviço vinculado HDInsight sob demanda, um cluster do HDInsight é criado sempre que uma fatia é processada, a menos que haja um cluster ativo existente (timeToLive).</span><span class="sxs-lookup"><span data-stu-id="86084-375">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (timeToLive).</span></span> <span data-ttu-id="86084-376">O cluster será excluído automaticamente quando o processamento for concluído.</span><span class="sxs-lookup"><span data-stu-id="86084-376">The cluster is automatically deleted when the processing is done.</span></span>
    
    <span data-ttu-id="86084-377">Quanto mais fatias forem processadas, você verá muitos contêineres no armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="86084-377">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="86084-378">Se você não precisa deles para solução de problemas dos trabalhos, convém excluí-los para reduzir o custo de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="86084-378">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="86084-379">Os nomes desses contêineres seguem um padrão: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="86084-379">The names of these containers follow a pattern: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`.</span></span> <span data-ttu-id="86084-380">Use ferramentas como o [Gerenciador de Armazenamento da Microsoft](http://storageexplorer.com/) para excluir contêineres do armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="86084-380">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>
- <span data-ttu-id="86084-381">Atualmente, o conjunto de dados de saída é o que aciona a agenda, então você deve criar um conjunto de dados de saída, mesmo que a atividade não produza qualquer saída.</span><span class="sxs-lookup"><span data-stu-id="86084-381">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="86084-382">Se a atividade não receber entradas, ignore a criação de conjunto de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="86084-382">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> 
- <span data-ttu-id="86084-383">Este tutorial não mostra como copiar dados usando Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="86084-383">This tutorial does not show how copy data by using Azure Data Factory.</span></span> <span data-ttu-id="86084-384">Para obter um tutorial sobre como copiar dados usando o Azure Data Factory, confira [Tutorial: copiar dados do armazenamento de blobs para um banco de dados SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="86084-384">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>


## <a name="use-server-explorer-to-view-data-factories"></a><span data-ttu-id="86084-385">Usar o Gerenciador de Servidores para exibir os data factories</span><span class="sxs-lookup"><span data-stu-id="86084-385">Use Server Explorer to view data factories</span></span>
1. <span data-ttu-id="86084-386">No **Visual Studio**, clique em **Exibir** no menu e em **Gerenciador de Servidores**.</span><span class="sxs-lookup"><span data-stu-id="86084-386">In **Visual Studio**, click **View** on the menu, and click **Server Explorer**.</span></span>
2. <span data-ttu-id="86084-387">Na janela Gerenciador de Servidores, expanda **Azure** e expanda **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="86084-387">In the Server Explorer window, expand **Azure** and expand **Data Factory**.</span></span> <span data-ttu-id="86084-388">Se **Entrar no Visual Studio** for exibido, insira a **conta** associada à sua assinatura do Azure e clique em **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="86084-388">If you see **Sign in to Visual Studio**, enter the **account** associated with your Azure subscription and click **Continue**.</span></span> <span data-ttu-id="86084-389">Insira a **senha** e clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="86084-389">Enter **password**, and click **Sign in**.</span></span> <span data-ttu-id="86084-390">O Visual Studio tenta obter informações sobre todos os data factories do Azure em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="86084-390">Visual Studio tries to get information about all Azure data factories in your subscription.</span></span> <span data-ttu-id="86084-391">Você verá o status da operação na janela **Lista de Tarefas de Data Factory** .</span><span class="sxs-lookup"><span data-stu-id="86084-391">You see the status of this operation in the **Data Factory Task List** window.</span></span>

    ![Gerenciador de Servidores](./media/data-factory-build-your-first-pipeline-using-vs/server-explorer.png)
3. <span data-ttu-id="86084-393">Clique com o botão direito em um data factory e selecione **Exportar Fábrica de Dados para Novo Projeto** para criar um projeto do Visual Studio com base em um data factory existente.</span><span class="sxs-lookup"><span data-stu-id="86084-393">You can right-click a data factory, and select **Export Data Factory to New Project** to create a Visual Studio project based on an existing data factory.</span></span>

    ![Exportar data factory](./media/data-factory-build-your-first-pipeline-using-vs/export-data-factory-menu.png)

## <a name="update-data-factory-tools-for-visual-studio"></a><span data-ttu-id="86084-395">Atualizar ferramentas de data factory para o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="86084-395">Update Data Factory tools for Visual Studio</span></span>
<span data-ttu-id="86084-396">Para atualizar as ferramentas da Azure Data Factory para o Visual Studio, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="86084-396">To update Azure Data Factory tools for Visual Studio, do the following steps:</span></span>

1. <span data-ttu-id="86084-397">Clique em **Ferramentas** no menu e selecione **Extensões e Atualizações**.</span><span class="sxs-lookup"><span data-stu-id="86084-397">Click **Tools** on the menu and select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="86084-398">Selecione **Atualizações** no painel esquerdo e selecione **Galeria do Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="86084-398">Select **Updates** in the left pane and then select **Visual Studio Gallery**.</span></span>
3. <span data-ttu-id="86084-399">Selecione **Ferramentas do Azure Data Factory para Visual Studio** e clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="86084-399">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span></span> <span data-ttu-id="86084-400">Se você não vir essa entrada, você já tem a versão mais recente das ferramentas.</span><span class="sxs-lookup"><span data-stu-id="86084-400">If you do not see this entry, you already have the latest version of the tools.</span></span>

## <a name="use-configuration-files"></a><span data-ttu-id="86084-401">Usar arquivos de configuração</span><span class="sxs-lookup"><span data-stu-id="86084-401">Use configuration files</span></span>
<span data-ttu-id="86084-402">Você pode usar arquivos de configuração no Visual Studio para configurar propriedades de serviços/tabelas/pipelines vinculados de forma diferente para cada ambiente.</span><span class="sxs-lookup"><span data-stu-id="86084-402">You can use configuration files in Visual Studio to configure properties for linked services/tables/pipelines differently for each environment.</span></span>

<span data-ttu-id="86084-403">Considere a definição de JSON a seguir para um serviço de Armazenamento do Azure vinculado.</span><span class="sxs-lookup"><span data-stu-id="86084-403">Consider the following JSON definition for an Azure Storage linked service.</span></span> <span data-ttu-id="86084-404">Para especificar a **connectionString** com valores diferentes para accountname e accountkey com base no ambiente (Desenvolvimento/Teste/Produção) no qual você está implantando entidades do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="86084-404">To specify **connectionString** with different values for accountname and accountkey based on the environment (Dev/Test/Production) to which you are deploying Data Factory entities.</span></span> <span data-ttu-id="86084-405">Você pode obter esse comportamento usando um arquivo de configuração separado para cada ambiente.</span><span class="sxs-lookup"><span data-stu-id="86084-405">You can achieve this behavior by using separate configuration file for each environment.</span></span>

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

### <a name="add-a-configuration-file"></a><span data-ttu-id="86084-406">Adicionar um arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="86084-406">Add a configuration file</span></span>
<span data-ttu-id="86084-407">Adicione um arquivo de configuração para cada ambiente executando as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="86084-407">Add a configuration file for each environment by performing the following steps:</span></span>   

1. <span data-ttu-id="86084-408">Clique com botão direito no projeto do Data Factory em sua solução do Visual Studio, aponte para **Adicionar** e clique em **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="86084-408">Right-click the Data Factory project in your Visual Studio solution, point to **Add**, and click **New item**.</span></span>
2. <span data-ttu-id="86084-409">Selecione **Config** na lista de modelos instalados no lado esquerdo, selecione **Arquivo de Configuração**, insira um **nome** para o arquivo de configuração e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="86084-409">Select **Config** from the list of installed templates on the left, select **Configuration File**, enter a **name** for the configuration file, and click **Add**.</span></span>

    ![Adicionar arquivo de configuração](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. <span data-ttu-id="86084-411">Adicione parâmetros de configuração e seus valores no formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="86084-411">Add configuration parameters and their values in the following format:</span></span>

    ```json
    {
        "$schema": "http://datafactories.schema.management.azure.com/vsschemas/V1/Microsoft.DataFactory.Config.json",
        "AzureStorageLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        ],
        "AzureSqlLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value":  "Server=tcp:spsqlserver.database.windows.net,1433;Database=spsqldb;User ID=spelluru;Password=Sowmya123;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        ]
    }
    ```

    <span data-ttu-id="86084-412">Este exemplo configura a propriedade connectionString de um serviço de Armazenamento do Azure vinculado e um serviço vinculado do Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="86084-412">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span></span> <span data-ttu-id="86084-413">Observe que a sintaxe para especificar o nome é [JsonPath](http://goessner.net/articles/JsonPath/).</span><span class="sxs-lookup"><span data-stu-id="86084-413">Notice that the syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span></span>   

    <span data-ttu-id="86084-414">Se o JSON tiver uma propriedade que tenha uma matriz de valores como mostrado no código a seguir:</span><span class="sxs-lookup"><span data-stu-id="86084-414">If JSON has a property that has an array of values as shown in the following code:</span></span>  

    ```json
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
    ```

    <span data-ttu-id="86084-415">Configure as propriedades como mostrado no seguinte arquivo de configuração (use a indexação baseada zero):</span><span class="sxs-lookup"><span data-stu-id="86084-415">Configure properties as shown in the following configuration file (use zero-based indexing):</span></span>

    ```json
    {
        "name": "$.properties.structure[0].name",
        "value": "FirstName"
    }
    {
        "name": "$.properties.structure[0].type",
        "value": "String"
    }
    {
        "name": "$.properties.structure[1].name",
        "value": "LastName"
    }
    {
        "name": "$.properties.structure[1].type",
        "value": "String"
    }
    ```

### <a name="property-names-with-spaces"></a><span data-ttu-id="86084-416">Nomes de propriedade com espaços</span><span class="sxs-lookup"><span data-stu-id="86084-416">Property names with spaces</span></span>
<span data-ttu-id="86084-417">Se um nome de propriedade tiver espaços, use os colchetes como mostrado no exemplo a seguir (nome do servidor de banco de dados):</span><span class="sxs-lookup"><span data-stu-id="86084-417">If a property name has spaces in it, use square brackets as shown in the following example (Database server name):</span></span>

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a><span data-ttu-id="86084-418">Implantar a solução usando uma configuração</span><span class="sxs-lookup"><span data-stu-id="86084-418">Deploy solution using a configuration</span></span>
<span data-ttu-id="86084-419">Ao publicar entidades do Azure Data Factory no VS, você pode especificar a configuração que deseja usar para essa operação de publicação.</span><span class="sxs-lookup"><span data-stu-id="86084-419">When you are publishing Azure Data Factory entities in VS, you can specify the configuration that you want to use for that publishing operation.</span></span>

<span data-ttu-id="86084-420">Para publicar as entidades em um projeto do Azure Data Factory usando o arquivo de configuração:</span><span class="sxs-lookup"><span data-stu-id="86084-420">To publish entities in an Azure Data Factory project using configuration file:</span></span>   

1. <span data-ttu-id="86084-421">Clique com o botão direito no projeto do Data Factory e clique em **Publicar** para ver a caixa de diálogo **Publicar Itens**.</span><span class="sxs-lookup"><span data-stu-id="86084-421">Right-click Data Factory project and click **Publish** to see the **Publish Items** dialog box.</span></span>
2. <span data-ttu-id="86084-422">Selecione um data factory existente ou especifique valores para a criação de um na página **Configurar data factory**, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="86084-422">Select an existing data factory or specify values for creating a data factory on the **Configure data factory** page, and click **Next**.</span></span>   
3. <span data-ttu-id="86084-423">Na página **Publicar Itens**: você vê uma lista suspensa com as configurações disponíveis para o campo **Selecionar Configuração de Implantação**.</span><span class="sxs-lookup"><span data-stu-id="86084-423">On the **Publish Items** page: you see a drop-down list with available configurations for the **Select Deployment Config** field.</span></span>

    ![Selecionar arquivo de configuração](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. <span data-ttu-id="86084-425">Selecione o **arquivo de configuração** que você deseja usar e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="86084-425">Select the **configuration file** that you would like to use and click **Next**.</span></span>
5. <span data-ttu-id="86084-426">Confirme se você vê o nome do arquivo JSON na página **Resumo** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="86084-426">Confirm that you see the name of JSON file in the **Summary** page and click **Next**.</span></span>
6. <span data-ttu-id="86084-427">Clique em **Concluir** depois que a operação de implantação for concluída.</span><span class="sxs-lookup"><span data-stu-id="86084-427">Click **Finish** after the deployment operation is finished.</span></span>

<span data-ttu-id="86084-428">Quando você implantar, os valores do arquivo de configuração serão usados para definir valores de propriedades nos arquivos JSON antes que as entidades sejam implantadas no serviço Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="86084-428">When you deploy, the values from the configuration file are used to set values for properties in the JSON files before the entities are deployed to Azure Data Factory service.</span></span>   

## <a name="use-azure-key-vault"></a><span data-ttu-id="86084-429">Usar o Cofre de Chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="86084-429">Use Azure Key Vault</span></span>
<span data-ttu-id="86084-430">Não é aconselhável e costuma ser contra a política de segurança confirmar dados confidenciais, como cadeias de conexão, para o repositório de código.</span><span class="sxs-lookup"><span data-stu-id="86084-430">It is not advisable and often against security policy to commit sensitive data such as connection strings to the code repository.</span></span> <span data-ttu-id="86084-431">Confira o exemplo [Secure Publish de ADF](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) no GitHub para saber mais sobre como armazenar informações confidenciais no Azure Key Vault e usá-lo durante a publicação de entidades do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="86084-431">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub to learn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span></span> <span data-ttu-id="86084-432">A extensão Secure Publish para Visual Studio permite que os segredos sejam armazenados no Key Vault e apenas referências a eles sejam especificadas em serviços vinculados/configurações de implantação.</span><span class="sxs-lookup"><span data-stu-id="86084-432">The Secure Publish extension for Visual Studio allows the secrets to be stored in Key Vault and only references to them are specified in linked services/ deployment configurations.</span></span> <span data-ttu-id="86084-433">Essas referências são resolvidas quando você publica as entidades do Data Factory do Azure.</span><span class="sxs-lookup"><span data-stu-id="86084-433">These references are resolved when you publish Data Factory entities to Azure.</span></span> <span data-ttu-id="86084-434">Em seguida, esses arquivos podem ser confirmados para o repositório de origem sem expor nenhum segredo.</span><span class="sxs-lookup"><span data-stu-id="86084-434">These files can then be committed to source repository without exposing any secrets.</span></span>

## <a name="summary"></a><span data-ttu-id="86084-435">Resumo</span><span class="sxs-lookup"><span data-stu-id="86084-435">Summary</span></span>
<span data-ttu-id="86084-436">Neste tutorial, você criou uma data factory do Azure para processar dados ao executar o script Hive em um cluster hadoop do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="86084-436">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="86084-437">Você usou o Data Factory Editor no portal do Azure para executar as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="86084-437">You used the Data Factory Editor in the Azure portal to do the following steps:</span></span>  

1. <span data-ttu-id="86084-438">Foi criada uma **data factory**do Azure.</span><span class="sxs-lookup"><span data-stu-id="86084-438">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="86084-439">Foram criados dois **serviços vinculados**:</span><span class="sxs-lookup"><span data-stu-id="86084-439">Created two **linked services**:</span></span>
   1. <span data-ttu-id="86084-440">**Armazenamento do Azure** para vincular seu armazenamento de blobs do Azure que contém os arquivos de entrada/saída para a data factory.</span><span class="sxs-lookup"><span data-stu-id="86084-440">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span></span>
   2. <span data-ttu-id="86084-441">**Azure HDInsight** sob demanda para vincular um cluster Hadoop do HDInsight sob demanda à data factory.</span><span class="sxs-lookup"><span data-stu-id="86084-441">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span></span> <span data-ttu-id="86084-442">O Azure Data Factory cria um cluster Hadoop do HDInsight just-in-time para processar dados de entrada e gerar dados de saída.</span><span class="sxs-lookup"><span data-stu-id="86084-442">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span></span>
3. <span data-ttu-id="86084-443">Foram criados dois **conjuntos de dados**que descrevem dados de entrada e de saída para a atividade Hive do HDInsight no pipeline.</span><span class="sxs-lookup"><span data-stu-id="86084-443">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span></span>
4. <span data-ttu-id="86084-444">Foi criado um **pipeline** com uma atividade **Hive do HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="86084-444">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="86084-445">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="86084-445">Next Steps</span></span>
<span data-ttu-id="86084-446">Neste artigo, você criou um pipeline com uma atividade de transformação (atividade do HDInsight) que executa um script Hive em um cluster do HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="86084-446">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="86084-447">Para saber como usar uma Atividade de Cópia para copiar dados de um Blob do Azure para o SQL do Azure, confira [Tutorial: Copiar dados de um blob do Azure para o SQL do Azure](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="86084-447">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="86084-448">É possível encadear duas atividades (executar uma atividade após a outra) definindo o conjunto de dados de saída de uma atividade como o conjunto de dados de entrada da outra atividade.</span><span class="sxs-lookup"><span data-stu-id="86084-448">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="86084-449">Veja [Agendamento e execução no Data Factory](data-factory-scheduling-and-execution.md) para obter informações detalhadas.</span><span class="sxs-lookup"><span data-stu-id="86084-449">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 


## <a name="see-also"></a><span data-ttu-id="86084-450">Consulte também</span><span class="sxs-lookup"><span data-stu-id="86084-450">See Also</span></span>
| <span data-ttu-id="86084-451">Tópico</span><span class="sxs-lookup"><span data-stu-id="86084-451">Topic</span></span> | <span data-ttu-id="86084-452">Descrição</span><span class="sxs-lookup"><span data-stu-id="86084-452">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="86084-453">Pipelines</span><span class="sxs-lookup"><span data-stu-id="86084-453">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="86084-454">Este artigo o ajuda a compreender pipelines e atividades no Azure Data Factory e como usá-los para construir fluxos de trabalho orientados a dados para o seu cenário ou negócio.</span><span class="sxs-lookup"><span data-stu-id="86084-454">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="86084-455">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="86084-455">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="86084-456">Este artigo o ajuda a entender os conjuntos de dados no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="86084-456">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="86084-457">Atividades de transformação de dados</span><span class="sxs-lookup"><span data-stu-id="86084-457">Data Transformation Activities</span></span>](data-factory-data-transformation-activities.md) |<span data-ttu-id="86084-458">Este artigo fornece uma lista de atividades de transformação de dados (como a transformação do Hive do HDInsight usado neste tutorial) com suporte do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="86084-458">This article provides a list of data transformation activities (such as HDInsight Hive transformation you used in this tutorial) supported by Azure Data Factory.</span></span> |
| [<span data-ttu-id="86084-459">Agendamento e execução</span><span class="sxs-lookup"><span data-stu-id="86084-459">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="86084-460">Este artigo explica os aspectos de agendamento e execução do modelo de aplicativo do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="86084-460">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="86084-461">Monitorar e gerenciar pipelines usando o Aplicativo de Monitoramento</span><span class="sxs-lookup"><span data-stu-id="86084-461">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="86084-462">Este artigo descreve como monitorar, gerenciar e depurar seus pipelines usando o Aplicativo de Monitoramento e Gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="86084-462">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |
