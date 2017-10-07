---
title: "Tutorial: Criar um pipeline com a Atividade de Cópia usando o Visual Studio | Microsoft Docs"
description: "Neste tutorial, você cria um pipeline do Azure Data Factory com uma Atividade de Cópia usando o Visual Studio."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1751185b-ce0a-4ab2-a9c3-e37b4d149ca3
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: d99d8875807bab41f5122ab95a09f83f82923529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-visual-studio"></a><span data-ttu-id="67ebc-103">Tutorial: Criar um pipeline com a Atividade de Cópia usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="67ebc-103">Tutorial: Create a pipeline with Copy Activity using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="67ebc-104">Visão geral e pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="67ebc-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="67ebc-105">Assistente de Cópia</span><span class="sxs-lookup"><span data-stu-id="67ebc-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="67ebc-106">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="67ebc-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="67ebc-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="67ebc-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="67ebc-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="67ebc-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="67ebc-109">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="67ebc-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="67ebc-110">API REST</span><span class="sxs-lookup"><span data-stu-id="67ebc-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="67ebc-111">API do .NET</span><span class="sxs-lookup"><span data-stu-id="67ebc-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="67ebc-112">Neste artigo, você aprenderá como toouse Olá toocreate do Microsoft Visual Studio uma fábrica de dados com um pipeline que copia dados de um banco de dados de SQL do Azure de tooan do armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="67ebc-112">In this article, you learn how toouse hello Microsoft Visual Studio toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="67ebc-113">Se você estiver tooAzure nova fábrica de dados, leia Olá [tooAzure Introdução Data Factory](data-factory-introduction.md) artigo antes de fazer este tutorial.</span><span class="sxs-lookup"><span data-stu-id="67ebc-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="67ebc-114">Neste tutorial, você criará um pipeline com uma atividade: atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="67ebc-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="67ebc-115">Olá Copiar atividade copia dados de um repositório de dados com suporte de dados repositório tooa coletor com suporte.</span><span class="sxs-lookup"><span data-stu-id="67ebc-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="67ebc-116">Para obter uma lista de armazenamentos de dados com suporte como origens e coletores, confira [Armazenamentos de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="67ebc-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="67ebc-117">atividade de saudação é alimentada por um serviço disponível globalmente que pode copiar dados entre vários repositórios de dados de forma segura, confiável e escalonável.</span><span class="sxs-lookup"><span data-stu-id="67ebc-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="67ebc-118">Para obter mais informações sobre hello atividade de cópia, consulte [atividades de movimentação de dados](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="67ebc-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="67ebc-119">Um pipeline pode ter mais de uma atividade.</span><span class="sxs-lookup"><span data-stu-id="67ebc-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="67ebc-120">E, é possível encadear duas atividades (executadas uma atividade após o outro), definindo Olá o conjunto de dados de saída de uma atividade Olá outra atividade de conjunto de dados de saudação de entrada.</span><span class="sxs-lookup"><span data-stu-id="67ebc-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="67ebc-121">Para saber mais, confira [Várias atividades em um pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="67ebc-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE] 
> <span data-ttu-id="67ebc-122">pipeline de dados Olá neste tutorial copia dados de um repositório de dados de destino fonte dados repositório tooa.</span><span class="sxs-lookup"><span data-stu-id="67ebc-122">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="67ebc-123">Para obter um tutorial sobre como tootransform dados usando a fábrica de dados do Azure, consulte [Tutorial: Crie um pipeline de dados tootransform usando o cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="67ebc-123">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67ebc-124">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="67ebc-124">Prerequisites</span></span>
1. <span data-ttu-id="67ebc-125">Leia [visão geral do Tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) artigo e hello completa **pré-requisito** etapas.</span><span class="sxs-lookup"><span data-stu-id="67ebc-125">Read through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article and complete hello **prerequisite** steps.</span></span>       
2. <span data-ttu-id="67ebc-126">toocreate instâncias de fábrica de dados, você deve ser um membro da saudação [colaborador da fábrica de dados](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) função no nível do grupo de recursos de assinatura/hello.</span><span class="sxs-lookup"><span data-stu-id="67ebc-126">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
3. <span data-ttu-id="67ebc-127">Você deve ter o seguinte Olá instalado em seu computador:</span><span class="sxs-lookup"><span data-stu-id="67ebc-127">You must have hello following installed on your computer:</span></span> 
   * <span data-ttu-id="67ebc-128">Visual Studio 2013 ou Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="67ebc-128">Visual Studio 2013 or Visual Studio 2015</span></span>
   * <span data-ttu-id="67ebc-129">Baixe o SDK do Azure para Visual Studio 2013 ou Visual Studio de 2015.</span><span class="sxs-lookup"><span data-stu-id="67ebc-129">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="67ebc-130">Navegue muito[página de Download do Azure](https://azure.microsoft.com/downloads/) e clique em **VS 2013** ou **VS 2015** em Olá **.NET** seção.</span><span class="sxs-lookup"><span data-stu-id="67ebc-130">Navigate too[Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in hello **.NET** section.</span></span>
   * <span data-ttu-id="67ebc-131">Baixar hello mais recente do Azure Data Factory plug-in para Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) ou [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span><span class="sxs-lookup"><span data-stu-id="67ebc-131">Download hello latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="67ebc-132">Você também pode atualizar plug-in de saudação fazendo Olá etapas a seguir: Olá menu, clique em **ferramentas** -> **extensões e atualizações** -> **Online**  ->  **Galeria do visual Studio** -> **ferramentas de fábrica de dados do Microsoft Azure para Visual Studio** -> **atualização**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-132">You can also update hello plugin by doing hello following steps: On hello menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

## <a name="steps"></a><span data-ttu-id="67ebc-133">Etapas</span><span class="sxs-lookup"><span data-stu-id="67ebc-133">Steps</span></span>
<span data-ttu-id="67ebc-134">Aqui estão as etapas Olá que fazem parte deste tutorial:</span><span class="sxs-lookup"><span data-stu-id="67ebc-134">Here are hello steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="67ebc-135">Criar **serviços vinculados** na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="67ebc-135">Create **linked services** in hello data factory.</span></span> <span data-ttu-id="67ebc-136">Nesta etapa, você criará dois serviços vinculados de tipos: banco de dados SQL e armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="67ebc-136">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="67ebc-137">Olá AzureStorageLinkedService vincula sua fábrica de dados de toohello de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="67ebc-137">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="67ebc-138">Você criou um contêiner e carregados conta de armazenamento toothis dados como parte de [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="67ebc-138">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="67ebc-139">AzureSqlLinkedService vincula sua fábrica de dados de toohello de banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="67ebc-139">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="67ebc-140">Olá dados são copiados do armazenamento de blob Olá são armazenados neste banco de dados.</span><span class="sxs-lookup"><span data-stu-id="67ebc-140">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="67ebc-141">Você criou uma tabela SQL no banco de dados como parte dos [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="67ebc-141">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>     
2. <span data-ttu-id="67ebc-142">Criar a entrada e saída **conjuntos de dados** na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="67ebc-142">Create input and output **datasets** in hello data factory.</span></span>  
    
    <span data-ttu-id="67ebc-143">serviço de armazenamento do Azure vinculado Olá Especifica a cadeia de conexão de Olá usada pelo serviço de fábrica de dados em tempo de execução tooconnect tooyour conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="67ebc-143">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="67ebc-144">E, conjunto de dados de blob de entrada hello Especifica o contêiner de saudação e a pasta de saudação que contém os dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="67ebc-144">And, hello input blob dataset specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="67ebc-145">Da mesma forma, Olá serviço de banco de dados do SQL Azure vinculado Especifica a cadeia de caracteres de conexão de saudação que usa o serviço de fábrica de dados no banco de dados SQL do Azure tooyour de tooconnect de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="67ebc-145">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="67ebc-146">Além disso, conjunto de dados da tabela SQL Olá saída Especifica a tabela Olá Olá toowhich Olá de banco de dados armazenamento de blob Olá é copiada.</span><span class="sxs-lookup"><span data-stu-id="67ebc-146">And, hello output SQL table dataset specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>
3. <span data-ttu-id="67ebc-147">Criar um **pipeline** na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="67ebc-147">Create a **pipeline** in hello data factory.</span></span> <span data-ttu-id="67ebc-148">Nesta etapa, você cria um pipeline com a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="67ebc-148">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="67ebc-149">Olá Copiar atividade copia dados de um blob na tabela de tooa de armazenamento de BLOBs do Azure de Olá no banco de dados do SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="67ebc-149">hello copy activity copies data from a blob in hello Azure blob storage tooa table in hello Azure SQL database.</span></span> <span data-ttu-id="67ebc-150">Você pode usar uma atividade de cópia em um pipeline toocopy os dados de qualquer destino tooany suportada de origem com suporte.</span><span class="sxs-lookup"><span data-stu-id="67ebc-150">You can use a copy activity in a pipeline toocopy data from any supported source tooany supported destination.</span></span> <span data-ttu-id="67ebc-151">Para obter uma lista de armazenamentos de dados com suporte, confira o artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="67ebc-151">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
4. <span data-ttu-id="67ebc-152">Crie um **data factory** do Azure ao implantar entidades de Data Factory (serviços vinculados, conjuntos de dados/tabelas e pipelines).</span><span class="sxs-lookup"><span data-stu-id="67ebc-152">Create an Azure **data factory** when deploying Data Factory entities (linked services, datasets/tables, and pipelines).</span></span> 

## <a name="create-visual-studio-project"></a><span data-ttu-id="67ebc-153">Criar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="67ebc-153">Create Visual Studio project</span></span>
1. <span data-ttu-id="67ebc-154">Inicie o **Visual Studio 2015**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-154">Launch **Visual Studio 2015**.</span></span> <span data-ttu-id="67ebc-155">Clique em **arquivo**, ponto muito**novo**e clique em **projeto**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-155">Click **File**, point too**New**, and click **Project**.</span></span> <span data-ttu-id="67ebc-156">Você deve ver Olá **novo projeto** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="67ebc-156">You should see hello **New Project** dialog box.</span></span>  
2. <span data-ttu-id="67ebc-157">Em Olá **novo projeto** caixa de diálogo, selecione Olá **DataFactory** modelo e clique em **projeto vazio de fábrica de dados**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-157">In hello **New Project** dialog, select hello **DataFactory** template, and click **Empty Data Factory Project**.</span></span>  
   
    ![Caixa de diálogo Novo projeto](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-project-dialog.png)
3. <span data-ttu-id="67ebc-159">Especifique o nome de saudação do projeto hello, local para a solução de saudação e nome da solução hello e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-159">Specify hello name of hello project, location for hello solution, and name of hello solution, and then click **OK**.</span></span>
   
    ![Gerenciador de Soluções](./media/data-factory-copy-activity-tutorial-using-visual-studio/solution-explorer.png)    

## <a name="create-linked-services"></a><span data-ttu-id="67ebc-161">Criar serviços vinculados</span><span class="sxs-lookup"><span data-stu-id="67ebc-161">Create linked services</span></span>
<span data-ttu-id="67ebc-162">Você pode criar serviços vinculados em um toolink de fábrica de dados seus dados, armazena e fábrica de dados toohello de serviços de computação.</span><span class="sxs-lookup"><span data-stu-id="67ebc-162">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="67ebc-163">Neste tutorial, você não usa serviços de computação, como o Azure HDInsight ou o Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="67ebc-163">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="67ebc-164">Você usa dois armazenamentos de dados do tipo Armazenamento do Azure (origem) e o banco de dados SQL (destino).</span><span class="sxs-lookup"><span data-stu-id="67ebc-164">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="67ebc-165">Portanto, você pode criar dois serviços vinculados de tipos: AzureStorage e AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="67ebc-165">Therefore, you create two linked services of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="67ebc-166">saudação de armazenamento do Azure vinculada links de serviço sua fábrica de dados de toohello de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="67ebc-166">hello Azure Storage linked service links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="67ebc-167">Esta conta de armazenamento é hello um no qual você criou um contêiner e carregou dados de saudação como parte do [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="67ebc-167">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="67ebc-168">SQL Azure vinculado links serviço sua fábrica de dados de toohello de banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="67ebc-168">Azure SQL linked service links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="67ebc-169">Olá dados são copiados do armazenamento de blob Olá são armazenados neste banco de dados.</span><span class="sxs-lookup"><span data-stu-id="67ebc-169">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="67ebc-170">Você criou tabela emp de saudação neste banco de dados como parte do [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="67ebc-170">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="67ebc-171">Serviços vinculados vincular armazenamentos de dados ou de computação serviços tooan data factory do Azure.</span><span class="sxs-lookup"><span data-stu-id="67ebc-171">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="67ebc-172">Consulte [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) para todos os Olá fontes e coletores suportados pelas hello atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="67ebc-172">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all hello sources and sinks supported by hello Copy Activity.</span></span> <span data-ttu-id="67ebc-173">Consulte [serviços vinculados de computação](data-factory-compute-linked-services.md) para lista de saudação de serviços de computação com suporte pela fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="67ebc-173">See [compute linked services](data-factory-compute-linked-services.md) for hello list of compute services supported by Data Factory.</span></span> <span data-ttu-id="67ebc-174">Neste tutorial, você não usa nenhum serviço de computação.</span><span class="sxs-lookup"><span data-stu-id="67ebc-174">In this tutorial, you do not use any compute service.</span></span> 

### <a name="create-hello-azure-storage-linked-service"></a><span data-ttu-id="67ebc-175">Criar serviço de armazenamento do Azure vinculada Olá</span><span class="sxs-lookup"><span data-stu-id="67ebc-175">Create hello Azure Storage linked service</span></span>
1. <span data-ttu-id="67ebc-176">Em **Solution Explorer**, clique com botão direito **serviços vinculados**, ponto muito**adicionar**e clique em **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-176">In **Solution Explorer**, right-click **Linked Services**, point too**Add**, and click **New Item**.</span></span>      
2. <span data-ttu-id="67ebc-177">Em Olá **Adicionar Novo Item** caixa de diálogo, selecione **serviço vinculado do armazenamento do Azure** Olá lista e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-177">In hello **Add New Item** dialog box, select **Azure Storage Linked Service** from hello list, and click **Add**.</span></span> 
   
    ![Novo serviço vinculado](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-linked-service-dialog.png)
3. <span data-ttu-id="67ebc-179">Substituir `<accountname>` e `<accountkey>`* com nome de saudação da sua conta de armazenamento do Azure e sua chave.</span><span class="sxs-lookup"><span data-stu-id="67ebc-179">Replace `<accountname>` and `<accountkey>`* with hello name of your Azure storage account and its key.</span></span> 
   
    ![Serviço vinculado de armazenamento do Azure](./media/data-factory-copy-activity-tutorial-using-visual-studio/azure-storage-linked-service.png)
4. <span data-ttu-id="67ebc-181">Salvar Olá **AzureStorageLinkedService1.json** arquivo.</span><span class="sxs-lookup"><span data-stu-id="67ebc-181">Save hello **AzureStorageLinkedService1.json** file.</span></span>

    <span data-ttu-id="67ebc-182">Para obter mais informações sobre as propriedades JSON na definição de serviço Olá vinculado, consulte [conector de armazenamento de BLOBs do Azure](data-factory-azure-blob-connector.md#linked-service-properties) artigo.</span><span class="sxs-lookup"><span data-stu-id="67ebc-182">For more information about JSON properties in hello linked service definition, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span>

### <a name="create-hello-azure-sql-linked-service"></a><span data-ttu-id="67ebc-183">Criar serviço vinculado do SQL Azure de saudação</span><span class="sxs-lookup"><span data-stu-id="67ebc-183">Create hello Azure SQL linked service</span></span>
1. <span data-ttu-id="67ebc-184">Clique duas vezes em **serviços vinculados** nó Olá **Solution Explorer** novamente, aponte muito**adicionar**e clique em **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-184">Right-click on **Linked Services** node in hello **Solution Explorer** again, point too**Add**, and click **New Item**.</span></span> 
2. <span data-ttu-id="67ebc-185">Desta vez, selecione **Serviço Vinculado SQL do Azure** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-185">This time, select **Azure SQL Linked Service**, and click **Add**.</span></span> 
3. <span data-ttu-id="67ebc-186">Em Olá **AzureSqlLinkedService1.json arquivo**, substitua `<servername>`, `<databasename>`, `<username@servername>`, e `<password>` com nomes de seu servidor SQL Azure, banco de dados, conta de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="67ebc-186">In hello **AzureSqlLinkedService1.json file**, replace `<servername>`, `<databasename>`, `<username@servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password.</span></span>    
4. <span data-ttu-id="67ebc-187">Salvar Olá **AzureSqlLinkedService1.json** arquivo.</span><span class="sxs-lookup"><span data-stu-id="67ebc-187">Save hello **AzureSqlLinkedService1.json** file.</span></span> 
    
    <span data-ttu-id="67ebc-188">Para saber mais sobre essas propriedades JSON, confira o [Conector do Banco de Dados SQL](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="67ebc-188">For more information about these JSON properties, see [Azure SQL Database connector](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>


## <a name="create-datasets"></a><span data-ttu-id="67ebc-189">Criar conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="67ebc-189">Create datasets</span></span>
<span data-ttu-id="67ebc-190">Na etapa anterior de saudação, você criou serviços vinculados toolink sua conta de armazenamento do Azure e a fábrica de dados de tooyour de banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="67ebc-190">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="67ebc-191">Nesta etapa, você definirá dois conjuntos de dados denominados InputDataset OutputDataset que representam a entrada e saída dados e que são armazenados em repositórios de dados Olá referenciados por AzureStorageLinkedService1 e AzureSqlLinkedService1, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="67ebc-191">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService1 and AzureSqlLinkedService1 respectively.</span></span>

<span data-ttu-id="67ebc-192">serviço de armazenamento do Azure vinculado Olá Especifica a cadeia de conexão de Olá usada pelo serviço de fábrica de dados em tempo de execução tooconnect tooyour conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="67ebc-192">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="67ebc-193">E, Olá o conjunto de dados de blob de entrada (InputDataset) Especifica o contêiner de saudação e a pasta de saudação que contém os dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="67ebc-193">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="67ebc-194">Da mesma forma, Olá serviço de banco de dados do SQL Azure vinculado Especifica a cadeia de caracteres de conexão de saudação que usa o serviço de fábrica de dados no banco de dados SQL do Azure tooyour de tooconnect de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="67ebc-194">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="67ebc-195">E, Olá saída SQL o conjunto de dados de tabela (OututDataset) Especifica a tabela de saudação em Olá Olá de toowhich de banco de dados dados saudação do armazenamento de blob são copiados.</span><span class="sxs-lookup"><span data-stu-id="67ebc-195">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="67ebc-196">Criar conjunto de dados de entrada</span><span class="sxs-lookup"><span data-stu-id="67ebc-196">Create input dataset</span></span>
<span data-ttu-id="67ebc-197">Nesta etapa, você criar um conjunto de dados chamado InputDataset que aponta o arquivo de blob tooa (emp.txt) na pasta raiz de saudação de um contêiner de blob (adftutorial) no hello representado por Olá AzureStorageLinkedService1 vinculado de serviço de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="67ebc-197">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService1 linked service.</span></span> <span data-ttu-id="67ebc-198">Se você não especificar um valor para o nome de arquivo hello (ou ignorá-lo), dados de todos os blobs na pasta de entrada hello são copiados toohello destino.</span><span class="sxs-lookup"><span data-stu-id="67ebc-198">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="67ebc-199">Neste tutorial, você deve especificar um valor para o nome de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="67ebc-199">In this tutorial, you specify a value for hello fileName.</span></span> 

<span data-ttu-id="67ebc-200">Aqui, você usa o termo hello "tabelas" em vez de "conjuntos de dados".</span><span class="sxs-lookup"><span data-stu-id="67ebc-200">Here, you use hello term "tables" rather than "datasets".</span></span> <span data-ttu-id="67ebc-201">Uma tabela é um conjunto de dados retangular e Olá único tipo de conjunto de dados com suporte no momento.</span><span class="sxs-lookup"><span data-stu-id="67ebc-201">A table is a rectangular dataset and is hello only type of dataset supported right now.</span></span> 

1. <span data-ttu-id="67ebc-202">Clique com botão direito **tabelas** em Olá **Solution Explorer**, ponto muito**adicionar**e clique em **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-202">Right-click **Tables** in hello **Solution Explorer**, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="67ebc-203">Em Olá **Adicionar Novo Item** caixa de diálogo, selecione **BLOBs do Azure**e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-203">In hello **Add New Item** dialog box, select **Azure Blob**, and click **Add**.</span></span>   
3. <span data-ttu-id="67ebc-204">Substituir texto JSON de Olá Olá texto a seguir e salve Olá **AzureBlobLocation1.json** arquivo.</span><span class="sxs-lookup"><span data-stu-id="67ebc-204">Replace hello JSON text with hello following text and save hello **AzureBlobLocation1.json** file.</span></span> 

  ```json   
  {
    "name": "InputDataset",
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
      "linkedServiceName": "AzureStorageLinkedService1",
      "typeProperties": {
        "folderPath": "adftutorial/",
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
    <span data-ttu-id="67ebc-205">Olá, tabela a seguir fornece descrições para propriedades JSON Olá usadas no trecho hello:</span><span class="sxs-lookup"><span data-stu-id="67ebc-205">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="67ebc-206">Propriedade</span><span class="sxs-lookup"><span data-stu-id="67ebc-206">Property</span></span> | <span data-ttu-id="67ebc-207">Descrição</span><span class="sxs-lookup"><span data-stu-id="67ebc-207">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="67ebc-208">type</span><span class="sxs-lookup"><span data-stu-id="67ebc-208">type</span></span> | <span data-ttu-id="67ebc-209">propriedade do tipo Hello está definida muito**AzureBlob** porque os dados residem em um armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="67ebc-209">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="67ebc-210">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="67ebc-210">linkedServiceName</span></span> | <span data-ttu-id="67ebc-211">Refere-se toohello **AzureStorageLinkedService** que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="67ebc-211">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="67ebc-212">folderPath</span><span class="sxs-lookup"><span data-stu-id="67ebc-212">folderPath</span></span> | <span data-ttu-id="67ebc-213">Especifica o blob Olá **contêiner** e hello **pasta** que contém blobs de entrada.</span><span class="sxs-lookup"><span data-stu-id="67ebc-213">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="67ebc-214">Neste tutorial, adftutorial é o contêiner de blob hello e pasta é a pasta raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="67ebc-214">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
    | <span data-ttu-id="67ebc-215">fileName</span><span class="sxs-lookup"><span data-stu-id="67ebc-215">fileName</span></span> | <span data-ttu-id="67ebc-216">Essa propriedade é opcional.</span><span class="sxs-lookup"><span data-stu-id="67ebc-216">This property is optional.</span></span> <span data-ttu-id="67ebc-217">Se você omitir essa propriedade, todos os arquivos de saudação folderPath são escolhidos.</span><span class="sxs-lookup"><span data-stu-id="67ebc-217">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="67ebc-218">Neste tutorial, **emp.txt** é especificado para hello fileName, portanto, somente esse arquivo é escolhida para processamento.</span><span class="sxs-lookup"><span data-stu-id="67ebc-218">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="67ebc-219">formato -> tipo</span><span class="sxs-lookup"><span data-stu-id="67ebc-219">format -> type</span></span> |<span data-ttu-id="67ebc-220">arquivo de entrada Hello está no formato de texto de saudação, para que possamos usar **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-220">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="67ebc-221">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="67ebc-221">columnDelimiter</span></span> | <span data-ttu-id="67ebc-222">saudação de colunas no arquivo de entrada hello é delimitadas por **caractere de vírgula (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-222">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="67ebc-223">frequência/intervalo</span><span class="sxs-lookup"><span data-stu-id="67ebc-223">frequency/interval</span></span> | <span data-ttu-id="67ebc-224">frequência de saudação está definida muito**hora** e o intervalo é definido muito**1**, que significa que Olá entrada fatias estão disponíveis **por hora**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-224">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="67ebc-225">Em outras palavras, Olá serviço da fábrica de dados procura por dados de entrada a cada hora na pasta raiz de saudação do contêiner de blob (**adftutorial**) especificado.</span><span class="sxs-lookup"><span data-stu-id="67ebc-225">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="67ebc-226">Ele procura os dados de saudação em Olá pipeline início e término vezes, não antes ou depois desses tempos.</span><span class="sxs-lookup"><span data-stu-id="67ebc-226">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="67ebc-227">externo</span><span class="sxs-lookup"><span data-stu-id="67ebc-227">external</span></span> | <span data-ttu-id="67ebc-228">Essa propriedade é definida, muito**true** se os dados de saudação não são gerados por este pipeline.</span><span class="sxs-lookup"><span data-stu-id="67ebc-228">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="67ebc-229">dados de entrada Hello neste tutorial estão no arquivo de emp.txt hello, que não é gerado por este pipeline, portanto vamos definir essa propriedade tootrue.</span><span class="sxs-lookup"><span data-stu-id="67ebc-229">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

    <span data-ttu-id="67ebc-230">Para saber mais sobre essas propriedades JSON, confira o [artigo sobre o conector do Blob do Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="67ebc-230">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>   

### <a name="create-output-dataset"></a><span data-ttu-id="67ebc-231">Criar conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="67ebc-231">Create output dataset</span></span>
<span data-ttu-id="67ebc-232">Nesta etapa, você cria um conjunto de dados de saída denominado **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-232">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="67ebc-233">Este conjunto de dados aponta tooa SQL tabela no banco de dados do SQL Azure Olá representado por **AzureSqlLinkedService1**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-233">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService1**.</span></span> 

1. <span data-ttu-id="67ebc-234">Clique com botão direito **tabelas** em Olá **Solution Explorer** novamente, aponte muito**adicionar**e clique em **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-234">Right-click **Tables** in hello **Solution Explorer** again, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="67ebc-235">Em Olá **Adicionar Novo Item** caixa de diálogo, selecione **SQL Azure**e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-235">In hello **Add New Item** dialog box, select **Azure SQL**, and click **Add**.</span></span> 
3. <span data-ttu-id="67ebc-236">Substituir texto JSON de Olá Olá JSON a seguir e salve Olá **AzureSqlTableLocation1.json** arquivo.</span><span class="sxs-lookup"><span data-stu-id="67ebc-236">Replace hello JSON text with hello following JSON and save hello **AzureSqlTableLocation1.json** file.</span></span>

  ```json
    {
     "name": "OutputDataset",
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
       "linkedServiceName": "AzureSqlLinkedService1",
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
    <span data-ttu-id="67ebc-237">Olá, tabela a seguir fornece descrições para propriedades JSON Olá usadas no trecho hello:</span><span class="sxs-lookup"><span data-stu-id="67ebc-237">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="67ebc-238">Propriedade</span><span class="sxs-lookup"><span data-stu-id="67ebc-238">Property</span></span> | <span data-ttu-id="67ebc-239">Descrição</span><span class="sxs-lookup"><span data-stu-id="67ebc-239">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="67ebc-240">type</span><span class="sxs-lookup"><span data-stu-id="67ebc-240">type</span></span> | <span data-ttu-id="67ebc-241">propriedade do tipo Hello está definida muito**AzureSqlTable** porque os dados são copiados tooa tabela em um banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="67ebc-241">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="67ebc-242">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="67ebc-242">linkedServiceName</span></span> | <span data-ttu-id="67ebc-243">Refere-se toohello **AzureSqlLinkedService** que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="67ebc-243">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="67ebc-244">tableName</span><span class="sxs-lookup"><span data-stu-id="67ebc-244">tableName</span></span> | <span data-ttu-id="67ebc-245">Olá especificado **tabela** toowhich Olá dados são copiados.</span><span class="sxs-lookup"><span data-stu-id="67ebc-245">Specified hello **table** toowhich hello data is copied.</span></span> | 
    | <span data-ttu-id="67ebc-246">frequência/intervalo</span><span class="sxs-lookup"><span data-stu-id="67ebc-246">frequency/interval</span></span> | <span data-ttu-id="67ebc-247">Olá frequência é definida muito**hora** e o intervalo é **1**, o que significa que Olá fatias de saída são produzidas **por hora** entre Olá pipeline início e término vezes, não antes ou Após esses horários.</span><span class="sxs-lookup"><span data-stu-id="67ebc-247">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="67ebc-248">Há três colunas – **ID**, **FirstName**, e **LastName** – na tabela de emp Olá no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="67ebc-248">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="67ebc-249">ID é uma coluna de identidade, portanto, você precisa apenas toospecify **FirstName** e **LastName** aqui.</span><span class="sxs-lookup"><span data-stu-id="67ebc-249">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="67ebc-250">Para saber mais sobre essas propriedades JSON, confira o [artigo sobre o conector do SQL](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="67ebc-250">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

## <a name="create-pipeline"></a><span data-ttu-id="67ebc-251">Criar um pipeline</span><span class="sxs-lookup"><span data-stu-id="67ebc-251">Create pipeline</span></span>
<span data-ttu-id="67ebc-252">Nesta etapa, você cria um pipeline com uma **atividade de cópia** que usa **InputDataset** como entrada e **OutputDataset** como saída.</span><span class="sxs-lookup"><span data-stu-id="67ebc-252">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="67ebc-253">Atualmente, o conjunto de dados de saída é quais unidades Olá agenda.</span><span class="sxs-lookup"><span data-stu-id="67ebc-253">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="67ebc-254">Neste tutorial, o conjunto de dados de saída é configurado tooproduce uma fatia de uma vez por hora.</span><span class="sxs-lookup"><span data-stu-id="67ebc-254">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="67ebc-255">pipeline de saudação tem uma hora de início e a hora de término que são um dia de distância, que é de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="67ebc-255">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="67ebc-256">Portanto, 24 fatias de conjunto de dados de saída são produzidas pelo pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="67ebc-256">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 

1. <span data-ttu-id="67ebc-257">Clique com botão direito **Pipelines** em Olá **Solution Explorer**, ponto muito**adicionar**e clique em **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-257">Right-click **Pipelines** in hello **Solution Explorer**, point too**Add**, and click **New Item**.</span></span>  
2. <span data-ttu-id="67ebc-258">Selecione **Pipeline de dados de cópia** em Olá **Adicionar Novo Item** caixa de diálogo e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-258">Select **Copy Data Pipeline** in hello **Add New Item** dialog box and click **Add**.</span></span> 
3. <span data-ttu-id="67ebc-259">Substitua Olá JSON Olá JSON a seguir e salve Olá **CopyActivity1.json** arquivo.</span><span class="sxs-lookup"><span data-stu-id="67ebc-259">Replace hello JSON with hello following JSON and save hello **CopyActivity1.json** file.</span></span>

  ```json   
    {
     "name": "ADFTutorialPipeline",
     "properties": {
       "description": "Copy data from a blob tooAzure SQL table",
       "activities": [
         {
           "name": "CopyFromBlobToSQL",
           "type": "Copy",
           "inputs": [
             {
               "name": "InputDataset"
             }
           ],
           "outputs": [
             {
               "name": "OutputDataset"
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
             "style": "StartOfInterval",
             "retry": 0,
             "timeout": "01:00:00"
           }
         }
       ],
       "start": "2017-05-11T00:00:00Z",
       "end": "2017-05-12T00:00:00Z",
       "isPaused": false
     }
    }
    ```   
    - <span data-ttu-id="67ebc-260">Na seção de atividades hello, há apenas uma atividade cuja **tipo** está definido muito**cópia**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-260">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="67ebc-261">Para obter mais informações sobre a atividade de cópia hello, consulte [atividades de movimentação de dados](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="67ebc-261">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="67ebc-262">Nas soluções de Data Factory, você também pode usar [atividades de transformação de dados](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="67ebc-262">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="67ebc-263">Entrada para atividade de saudação é definida muito**InputDataset** e de saída para o conjunto de hello atividade é muito**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-263">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="67ebc-264">Em Olá **typeProperties** seção, **BlobSource** é especificado como tipo de fonte hello e **SqlSink** é especificado como tipo de coletor de saudação.</span><span class="sxs-lookup"><span data-stu-id="67ebc-264">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="67ebc-265">Para obter uma lista completa de armazenamentos de dados de atividade de cópia hello como origens e coletores com suporte, consulte [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="67ebc-265">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="67ebc-266">toolearn como toouse dados específicos com suporte são armazenados como um fonte/coletor, clique o link de saudação na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="67ebc-266">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
     
    <span data-ttu-id="67ebc-267">Substituir valor Olá Olá **iniciar** propriedade com hello dia atual e **final** valor com hello dia seguinte.</span><span class="sxs-lookup"><span data-stu-id="67ebc-267">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="67ebc-268">Você pode especificar apenas parte da data hello e ignore a parte de hora de saudação da saudação data hora.</span><span class="sxs-lookup"><span data-stu-id="67ebc-268">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="67ebc-269">Por exemplo, "2016-02-03", que é o equivalente muito "2016-02-03T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="67ebc-269">For example, "2016-02-03", which is equivalent too"2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="67ebc-270">Ambos os valores de data/hora de início e de término devem estar no [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="67ebc-270">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="67ebc-271">Por exemplo: 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="67ebc-271">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="67ebc-272">Olá **final** tempo é opcional, mas usamos neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="67ebc-272">hello **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="67ebc-273">Se você não especificar o valor para Olá **final** propriedade, ele é calculado como "**início + 48 horas**".</span><span class="sxs-lookup"><span data-stu-id="67ebc-273">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="67ebc-274">pipeline de saudação toorun indefinidamente, especifique **9999-09-09** como valor Olá Olá **final** propriedade.</span><span class="sxs-lookup"><span data-stu-id="67ebc-274">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
     
    <span data-ttu-id="67ebc-275">Olá anterior de exemplo, há 24 fatias de dados como cada fatia de dados é produzida por hora.</span><span class="sxs-lookup"><span data-stu-id="67ebc-275">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="67ebc-276">Para obter descrições das propriedades JSON em uma definição de pipeline, consulte o artigo [Criar pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="67ebc-276">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="67ebc-277">Para obter descrições das propriedades JSON em uma definição de atividade de cópia, consulte [Atividades de movimentação de dados](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="67ebc-277">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="67ebc-278">Para obter descrições das propriedades JSON com suporte pelo BlobSource, consulte o [artigo sobre o conector de blobs do Azure](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="67ebc-278">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="67ebc-279">Para obter descrições das propriedades JSON com suporte pelo SqlSink, consulte o [artigo sobre o conector do Banco de Dados SQL](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="67ebc-279">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="publishdeploy-data-factory-entities"></a><span data-ttu-id="67ebc-280">Publicar/implantar entidades de data factory</span><span class="sxs-lookup"><span data-stu-id="67ebc-280">Publish/deploy Data Factory entities</span></span>
<span data-ttu-id="67ebc-281">Nesta etapa, você publica as entidades de Data Factory (serviços vinculados, conjuntos de dados e pipeline) criadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="67ebc-281">In this step, you publish Data Factory entities (linked services, datasets, and pipeline) you created earlier.</span></span> <span data-ttu-id="67ebc-282">Você também especificar o nome de saudação do hello novos dados fábrica toobe criado toohold essas entidades.</span><span class="sxs-lookup"><span data-stu-id="67ebc-282">You also specify hello name of hello new data factory toobe created toohold these entities.</span></span>  

1. <span data-ttu-id="67ebc-283">Clique com botão direito no Gerenciador de soluções do hello e, em seguida, clique em **publicar**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-283">Right-click project in hello Solution Explorer, and click **Publish**.</span></span> 
2. <span data-ttu-id="67ebc-284">Se você vir **entrar na conta da Microsoft de tooyour** caixa de diálogo, insira suas credenciais de conta de saudação que tenha a assinatura do Azure e clique em **entrar**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-284">If you see **Sign in tooyour Microsoft account** dialog box, enter your credentials for hello account that has Azure subscription, and click **sign in**.</span></span>
3. <span data-ttu-id="67ebc-285">Você deve ver Olá caixa de diálogo a seguir:</span><span class="sxs-lookup"><span data-stu-id="67ebc-285">You should see hello following dialog box:</span></span>
   
   ![Caixa de diálogo Publicar](./media/data-factory-copy-activity-tutorial-using-visual-studio/publish.png)
4. <span data-ttu-id="67ebc-287">Na página de fábrica de dados de configurar Olá, Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="67ebc-287">In hello Configure data factory page, do hello following steps:</span></span> 
   
   1. <span data-ttu-id="67ebc-288">Selecione a opção **Criar Nova Data Factory** .</span><span class="sxs-lookup"><span data-stu-id="67ebc-288">select **Create New Data Factory** option.</span></span>
   2. <span data-ttu-id="67ebc-289">Digite **VSTutorialFactory** para **Nome**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-289">Enter **VSTutorialFactory** for **Name**.</span></span>  
      
      > [!IMPORTANT]
      > <span data-ttu-id="67ebc-290">nome de Olá Olá do Azure da fábrica de dados deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="67ebc-290">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="67ebc-291">Se você receber um erro sobre nome de saudação da fábrica de dados durante a publicação, altere o nome de saudação da fábrica de dados da saudação (por exemplo, yournameVSTutorialFactory) e tente publicar novamente.</span><span class="sxs-lookup"><span data-stu-id="67ebc-291">If you receive an error about hello name of data factory when publishing, change hello name of hello data factory (for example, yournameVSTutorialFactory) and try publishing again.</span></span> <span data-ttu-id="67ebc-292">Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="67ebc-292">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>        
      > 
      > 
   3. <span data-ttu-id="67ebc-293">Selecione sua assinatura do Azure para Olá **assinatura** campo.</span><span class="sxs-lookup"><span data-stu-id="67ebc-293">Select your Azure subscription for hello **Subscription** field.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="67ebc-294">Se você não vir nenhuma assinatura, certifique-se de que você fez logon usando uma conta que seja um administrador ou coadministrador da assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="67ebc-294">If you do not see any subscription, ensure that you logged in using an account that is an admin or co-admin of hello subscription.</span></span>  
      > 
      > 
   4. <span data-ttu-id="67ebc-295">Selecione Olá **grupo de recursos** para Olá toobe de fábrica de dados criado.</span><span class="sxs-lookup"><span data-stu-id="67ebc-295">Select hello **resource group** for hello data factory toobe created.</span></span> 
   5. <span data-ttu-id="67ebc-296">Selecione Olá **região** Olá fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="67ebc-296">Select hello **region** for hello data factory.</span></span> <span data-ttu-id="67ebc-297">Somente regiões Olá serviço da fábrica de dados com suporte são mostrados na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="67ebc-297">Only regions supported by hello Data Factory service are shown in hello drop-down list.</span></span>
   6. <span data-ttu-id="67ebc-298">Clique em **próximo** tooswitch toohello **publicar itens** página.</span><span class="sxs-lookup"><span data-stu-id="67ebc-298">Click **Next** tooswitch toohello **Publish Items** page.</span></span>
      
       ![Configurar página de data factory](media/data-factory-copy-activity-tutorial-using-visual-studio/configure-data-factory-page.png)   
5. <span data-ttu-id="67ebc-300">Em Olá **publicar itens** página, certifique-se de que todos os Olá fábricas de dados de entidades são selecionadas e clique em **próximo** tooswitch toohello **resumo** página.</span><span class="sxs-lookup"><span data-stu-id="67ebc-300">In hello **Publish Items** page, ensure that all hello Data Factories entities are selected, and click **Next** tooswitch toohello **Summary** page.</span></span>
   
   ![Publicar página de item](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-items-page.png)     
6. <span data-ttu-id="67ebc-302">Revise o resumo de saudação e clique em **próximo** Olá de processo e o modo de exibição de implantação de saudação do toostart **Status da implantação**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-302">Review hello summary and click **Next** toostart hello deployment process and view hello **Deployment Status**.</span></span>
   
   ![Publicar página de resumo](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-summary-page.png)
7. <span data-ttu-id="67ebc-304">Em Olá **Status da implantação** página, você deve ver o status de Olá Olá do processo de implantação.</span><span class="sxs-lookup"><span data-stu-id="67ebc-304">In hello **Deployment Status** page, you should see hello status of hello deployment process.</span></span> <span data-ttu-id="67ebc-305">Após a conclusão da implantação de saudação, clique em Concluir.</span><span class="sxs-lookup"><span data-stu-id="67ebc-305">Click Finish after hello deployment is done.</span></span>
 
   ![Página Status da implantação](media/data-factory-copy-activity-tutorial-using-visual-studio/deployment-status.png)

<span data-ttu-id="67ebc-307">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="67ebc-307">Note hello following points:</span></span> 

* <span data-ttu-id="67ebc-308">Se você receber o erro Olá: "Esta assinatura não está registrado toouse namespace DataFactory", execute um dos seguintes hello e tente publicar novamente:</span><span class="sxs-lookup"><span data-stu-id="67ebc-308">If you receive hello error: "This subscription is not registered toouse namespace Microsoft.DataFactory", do one of hello following and try publishing again:</span></span> 
  
  * <span data-ttu-id="67ebc-309">No Azure PowerShell, execute Olá provedor do comando tooregister Olá fábrica de dados a seguir.</span><span class="sxs-lookup"><span data-stu-id="67ebc-309">In Azure PowerShell, run hello following command tooregister hello Data Factory provider.</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="67ebc-310">Você pode executar Olá tooconfirm de comando a seguir que Olá Data Factory provedor está registrado.</span><span class="sxs-lookup"><span data-stu-id="67ebc-310">You can run hello following command tooconfirm that hello Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="67ebc-311">Usando o logon Olá assinatura do Azure em Olá [portal do Azure](https://portal.azure.com) e navegue tooa folha de fábrica de dados (ou) criar uma fábrica de dados no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="67ebc-311">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="67ebc-312">Esta ação registra automaticamente o provedor de saudação para você.</span><span class="sxs-lookup"><span data-stu-id="67ebc-312">This action automatically registers hello provider for you.</span></span>
* <span data-ttu-id="67ebc-313">nome Olá Olá da fábrica de dados pode ser registrado como um nome DNS no hello futuro e, portanto, se tornarão visível publicamente.</span><span class="sxs-lookup"><span data-stu-id="67ebc-313">hello name of hello data factory may be registered as a DNS name in hello future and hence become publically visible.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="67ebc-314">toocreate instâncias de fábrica de dados, você precisa toobe um administrador/coadministrador da saudação assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="67ebc-314">toocreate Data Factory instances, you need toobe a admin/co-admin of hello Azure subscription</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="67ebc-315">Monitorar o pipeline</span><span class="sxs-lookup"><span data-stu-id="67ebc-315">Monitor pipeline</span></span>
<span data-ttu-id="67ebc-316">Navegue até a página inicial de toohello sua fábrica de dados:</span><span class="sxs-lookup"><span data-stu-id="67ebc-316">Navigate toohello home page for your data factory:</span></span>

1. <span data-ttu-id="67ebc-317">Faça logon no muito[portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="67ebc-317">Log in too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="67ebc-318">Clique em **mais serviços** Olá menus à esquerda e clique em **fábricas de dados**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-318">Click **More services** on hello left menu, and click **Data factories**.</span></span>

    ![Procurar data factories](media/data-factory-copy-activity-tutorial-using-visual-studio/browse-data-factories.png)
3. <span data-ttu-id="67ebc-320">Comece a digitar nome de saudação da sua fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="67ebc-320">Start typing hello name of your data factory.</span></span>

    ![Nome do data factory](media/data-factory-copy-activity-tutorial-using-visual-studio/enter-data-factory-name.png) 
4. <span data-ttu-id="67ebc-322">Clique em sua fábrica de dados em Olá resultados lista toosee Olá home page de sua fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="67ebc-322">Click your data factory in hello results list toosee hello home page for your data factory.</span></span>

    ![Página inicial da data factory](media/data-factory-copy-activity-tutorial-using-visual-studio/data-factory-home-page.png)
5. <span data-ttu-id="67ebc-324">Siga as instruções de [monitorar conjuntos de dados e pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) pipeline de saudação toomonitor e conjuntos de dados, você criou neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="67ebc-324">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="67ebc-325">Atualmente, o Visual Studio não dá suporte a monitoramento de pipelines do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="67ebc-325">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span> 

## <a name="summary"></a><span data-ttu-id="67ebc-326">Resumo</span><span class="sxs-lookup"><span data-stu-id="67ebc-326">Summary</span></span>
<span data-ttu-id="67ebc-327">Neste tutorial, você criou um Azure fábrica toocopy dados de um banco de dados do SQL Azure de tooan BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="67ebc-327">In this tutorial, you created an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="67ebc-328">Você usou a fábrica de dados do Visual Studio toocreate hello, serviços vinculados, conjuntos de dados e um pipeline.</span><span class="sxs-lookup"><span data-stu-id="67ebc-328">You used Visual Studio toocreate hello data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="67ebc-329">Aqui estão as etapas de alto nível Olá executada neste tutorial:</span><span class="sxs-lookup"><span data-stu-id="67ebc-329">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="67ebc-330">Foi criada uma **data factory**do Azure.</span><span class="sxs-lookup"><span data-stu-id="67ebc-330">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="67ebc-331">Foram criados **serviços vinculados**:</span><span class="sxs-lookup"><span data-stu-id="67ebc-331">Created **linked services**:</span></span>
   1. <span data-ttu-id="67ebc-332">Um **armazenamento do Azure** vinculado serviço toolink sua conta de armazenamento do Azure que contém dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="67ebc-332">An **Azure Storage** linked service toolink your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="67ebc-333">Um **SQL Azure** vinculado serviço toolink seu banco de dados SQL do Azure que contém dados de saída de saudação.</span><span class="sxs-lookup"><span data-stu-id="67ebc-333">An **Azure SQL** linked service toolink your Azure SQL database that holds hello output data.</span></span> 
3. <span data-ttu-id="67ebc-334">Foram criados **conjuntos de dados**que descrevem os dados de entrada e de saída para os pipelines.</span><span class="sxs-lookup"><span data-stu-id="67ebc-334">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="67ebc-335">Foi criado um **pipeline** com uma **Atividade de Cópia** com **BlobSource** como origem e **SqlSink** como coletor.</span><span class="sxs-lookup"><span data-stu-id="67ebc-335">Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.</span></span> 

<span data-ttu-id="67ebc-336">toosee como toouse dados de tootransform uma atividade de Hive do HDInsight usando o cluster HDInsight do Azure, consulte [ Tutorial: Crie sua primeira pipeline tootransform de dados usando o cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="67ebc-336">toosee how toouse a HDInsight Hive Activity tootransform data by using Azure HDInsight cluster, see [ Tutorial: Build your first pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="67ebc-337">É possível encadear duas atividades (executadas uma atividade após o outro), definindo Olá o conjunto de dados de saída de uma atividade Olá outra atividade de conjunto de dados de saudação de entrada.</span><span class="sxs-lookup"><span data-stu-id="67ebc-337">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="67ebc-338">Veja [Agendamento e execução no Data Factory](data-factory-scheduling-and-execution.md) para obter informações detalhadas.</span><span class="sxs-lookup"><span data-stu-id="67ebc-338">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 

## <a name="view-all-data-factories-in-server-explorer"></a><span data-ttu-id="67ebc-339">Exibir todos os data factories no Gerenciador de Servidores</span><span class="sxs-lookup"><span data-stu-id="67ebc-339">View all data factories in Server Explorer</span></span>
<span data-ttu-id="67ebc-340">Esta seção descreve como toouse Olá Server Explorer no Visual Studio tooview todas as fábricas de dados de saudação em sua assinatura do Azure e criar um projeto do Visual Studio com base em uma fábrica de dados existente.</span><span class="sxs-lookup"><span data-stu-id="67ebc-340">This section describes how toouse hello Server Explorer in Visual Studio tooview all hello data factories in your Azure subscription and create a Visual Studio project based on an existing data factory.</span></span> 

1. <span data-ttu-id="67ebc-341">Em **Visual Studio**, clique em **exibição** Olá menu e clique em **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-341">In **Visual Studio**, click **View** on hello menu, and click **Server Explorer**.</span></span>
2. <span data-ttu-id="67ebc-342">Na janela do Gerenciador de servidores hello, expanda **Azure** e expanda **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-342">In hello Server Explorer window, expand **Azure** and expand **Data Factory**.</span></span> <span data-ttu-id="67ebc-343">Se você vir **entrar tooVisual Studio**, digite Olá **conta** associado à sua assinatura do Azure e clique em **continuar**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-343">If you see **Sign in tooVisual Studio**, enter hello **account** associated with your Azure subscription and click **Continue**.</span></span> <span data-ttu-id="67ebc-344">Insira a **senha** e clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-344">Enter **password**, and click **Sign in**.</span></span> <span data-ttu-id="67ebc-345">O Visual Studio tenta tooget informações sobre todas as fábricas de dados do Azure em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="67ebc-345">Visual Studio tries tooget information about all Azure data factories in your subscription.</span></span> <span data-ttu-id="67ebc-346">Consulte status Olá dessa operação no hello **lista de tarefas de fábrica de dados** janela.</span><span class="sxs-lookup"><span data-stu-id="67ebc-346">You see hello status of this operation in hello **Data Factory Task List** window.</span></span>

    ![Gerenciador de Servidores](./media/data-factory-copy-activity-tutorial-using-visual-studio/server-explorer.png)

## <a name="create-a-visual-studio-project-for-an-existing-data-factory"></a><span data-ttu-id="67ebc-348">Criar um projeto do Visual Studio para um data factory existente</span><span class="sxs-lookup"><span data-stu-id="67ebc-348">Create a Visual Studio project for an existing data factory</span></span>

- <span data-ttu-id="67ebc-349">Uma fábrica de dados no Gerenciador de servidores e selecione **tooNew exportar Data Factory projeto** toocreate um projeto do Visual Studio com base em uma fábrica de dados existente.</span><span class="sxs-lookup"><span data-stu-id="67ebc-349">Right-click a data factory in Server Explorer, and select **Export Data Factory tooNew Project** toocreate a Visual Studio project based on an existing data factory.</span></span>

    ![Exportar dados fábrica tooa VS projeto](./media/data-factory-copy-activity-tutorial-using-visual-studio/export-data-factory-menu.png)  

## <a name="update-data-factory-tools-for-visual-studio"></a><span data-ttu-id="67ebc-351">Atualizar ferramentas de data factory para o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="67ebc-351">Update Data Factory tools for Visual Studio</span></span>
<span data-ttu-id="67ebc-352">ferramentas do Azure Data Factory tooupdate para Visual Studio, Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="67ebc-352">tooupdate Azure Data Factory tools for Visual Studio, do hello following steps:</span></span>

1. <span data-ttu-id="67ebc-353">Clique em **ferramentas** no menu hello e selecione **extensões e atualizações**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-353">Click **Tools** on hello menu and select **Extensions and Updates**.</span></span> 
2. <span data-ttu-id="67ebc-354">Selecione **atualizações** Olá painel esquerdo e, em seguida, selecione **Galeria do Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-354">Select **Updates** in hello left pane and then select **Visual Studio Gallery**.</span></span>
3. <span data-ttu-id="67ebc-355">Selecione **Ferramentas do Azure Data Factory para Visual Studio** e clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-355">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span></span> <span data-ttu-id="67ebc-356">Se você não vir essa entrada, você já tem a versão mais recente Olá das ferramentas de saudação.</span><span class="sxs-lookup"><span data-stu-id="67ebc-356">If you do not see this entry, you already have hello latest version of hello tools.</span></span> 

## <a name="use-configuration-files"></a><span data-ttu-id="67ebc-357">Usar arquivos de configuração</span><span class="sxs-lookup"><span data-stu-id="67ebc-357">Use configuration files</span></span>
<span data-ttu-id="67ebc-358">Você pode usar arquivos de configuração nas propriedades do Visual Studio tooconfigure para serviços/tabelas/pipelines vinculados diferentes para cada ambiente.</span><span class="sxs-lookup"><span data-stu-id="67ebc-358">You can use configuration files in Visual Studio tooconfigure properties for linked services/tables/pipelines differently for each environment.</span></span>

<span data-ttu-id="67ebc-359">Considere Olá após a definição de JSON para um serviço vinculado do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="67ebc-359">Consider hello following JSON definition for an Azure Storage linked service.</span></span> <span data-ttu-id="67ebc-360">toospecify **connectionString** com valores diferentes para accountname e accountkey com base em Olá toowhich de ambiente (desenvolvimento/teste/produção), você está implantando entidades da fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="67ebc-360">toospecify **connectionString** with different values for accountname and accountkey based on hello environment (Dev/Test/Production) toowhich you are deploying Data Factory entities.</span></span> <span data-ttu-id="67ebc-361">Você pode obter esse comportamento usando um arquivo de configuração separado para cada ambiente.</span><span class="sxs-lookup"><span data-stu-id="67ebc-361">You can achieve this behavior by using separate configuration file for each environment.</span></span>

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

### <a name="add-a-configuration-file"></a><span data-ttu-id="67ebc-362">Adicionar um arquivo de configuração</span><span class="sxs-lookup"><span data-stu-id="67ebc-362">Add a configuration file</span></span>
<span data-ttu-id="67ebc-363">Adiciona um arquivo de configuração para cada ambiente executando Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="67ebc-363">Add a configuration file for each environment by performing hello following steps:</span></span>   

1. <span data-ttu-id="67ebc-364">Clique com botão direito Olá fábrica de dados em sua solução do Visual Studio, aponte muito**adicionar**e clique em **novo item**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-364">Right-click hello Data Factory project in your Visual Studio solution, point too**Add**, and click **New item**.</span></span>
2. <span data-ttu-id="67ebc-365">Selecione **Config** na lista de saudação de modelos instalados Olá esquerda, selecione **arquivo de configuração**, insira um **nome** para a configuração de saudação do arquivo e, em seguida, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-365">Select **Config** from hello list of installed templates on hello left, select **Configuration File**, enter a **name** for hello configuration file, and click **Add**.</span></span>

    ![Adicionar arquivo de configuração](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. <span data-ttu-id="67ebc-367">Adicione os parâmetros de configuração e seus valores hello formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="67ebc-367">Add configuration parameters and their values in hello following format:</span></span>

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

    <span data-ttu-id="67ebc-368">Este exemplo configura a propriedade connectionString de um serviço de Armazenamento do Azure vinculado e um serviço vinculado do Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="67ebc-368">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span></span> <span data-ttu-id="67ebc-369">Observe que a sintaxe de saudação para especificar o nome é [JsonPath](http://goessner.net/articles/JsonPath/).</span><span class="sxs-lookup"><span data-stu-id="67ebc-369">Notice that hello syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span></span>   

    <span data-ttu-id="67ebc-370">Se o JSON tem uma propriedade que tem uma matriz de valores, conforme mostrado na saudação de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="67ebc-370">If JSON has a property that has an array of values as shown in hello following code:</span></span>  

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

    <span data-ttu-id="67ebc-371">Configure as propriedades conforme mostrado no hello (use indexação com base em zero) do arquivo de configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="67ebc-371">Configure properties as shown in hello following configuration file (use zero-based indexing):</span></span>

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

### <a name="property-names-with-spaces"></a><span data-ttu-id="67ebc-372">Nomes de propriedade com espaços</span><span class="sxs-lookup"><span data-stu-id="67ebc-372">Property names with spaces</span></span>
<span data-ttu-id="67ebc-373">Se um nome de propriedade tiver espaços, use colchetes, conforme mostrado no hello (nome do servidor de banco de dados) de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="67ebc-373">If a property name has spaces in it, use square brackets as shown in hello following example (Database server name):</span></span>

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a><span data-ttu-id="67ebc-374">Implantar a solução usando uma configuração</span><span class="sxs-lookup"><span data-stu-id="67ebc-374">Deploy solution using a configuration</span></span>
<span data-ttu-id="67ebc-375">Quando você estiver publicando entidades do Azure Data Factory no VS, você pode especificar a configuração de saudação que você deseja toouse para essa operação de publicação.</span><span class="sxs-lookup"><span data-stu-id="67ebc-375">When you are publishing Azure Data Factory entities in VS, you can specify hello configuration that you want toouse for that publishing operation.</span></span>

<span data-ttu-id="67ebc-376">toopublish entidades em um projeto do Azure Data Factory usando arquivo de configuração:</span><span class="sxs-lookup"><span data-stu-id="67ebc-376">toopublish entities in an Azure Data Factory project using configuration file:</span></span>   

1. <span data-ttu-id="67ebc-377">Clique com botão direito fábrica de dados e clique em **publicar** toosee Olá **publicar itens** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="67ebc-377">Right-click Data Factory project and click **Publish** toosee hello **Publish Items** dialog box.</span></span>
2. <span data-ttu-id="67ebc-378">Selecione uma fábrica de dados existente ou especificar valores para a criação de uma fábrica de dados em Olá **fábrica de dados configurar** página e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-378">Select an existing data factory or specify values for creating a data factory on hello **Configure data factory** page, and click **Next**.</span></span>   
3. <span data-ttu-id="67ebc-379">Em Olá **publicar itens** página: você verá uma lista suspensa com as configurações disponíveis para Olá **Selecionar configuração de implantação** campo.</span><span class="sxs-lookup"><span data-stu-id="67ebc-379">On hello **Publish Items** page: you see a drop-down list with available configurations for hello **Select Deployment Config** field.</span></span>

    ![Selecionar arquivo de configuração](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. <span data-ttu-id="67ebc-381">Selecione Olá **arquivo de configuração** que deseja toouse e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-381">Select hello **configuration file** that you would like toouse and click **Next**.</span></span>
5. <span data-ttu-id="67ebc-382">Confirme que você vê o nome de saudação do arquivo JSON Olá **resumo** página e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="67ebc-382">Confirm that you see hello name of JSON file in hello **Summary** page and click **Next**.</span></span>
6. <span data-ttu-id="67ebc-383">Clique em **concluir** após a operação de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="67ebc-383">Click **Finish** after hello deployment operation is finished.</span></span>

<span data-ttu-id="67ebc-384">Quando você implanta, valores de saudação do arquivo de configuração de saudação são tooset usados valores para as propriedades nos arquivos de JSON Olá antes entidades Olá tooAzure implantado o serviço de fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="67ebc-384">When you deploy, hello values from hello configuration file are used tooset values for properties in hello JSON files before hello entities are deployed tooAzure Data Factory service.</span></span>   

## <a name="use-azure-key-vault"></a><span data-ttu-id="67ebc-385">Usar o Cofre de Chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="67ebc-385">Use Azure Key Vault</span></span>
<span data-ttu-id="67ebc-386">Não é aconselhável e em relação a dados confidenciais de segurança política toocommit como repositório de código de toohello de cadeias de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="67ebc-386">It is not advisable and often against security policy toocommit sensitive data such as connection strings toohello code repository.</span></span> <span data-ttu-id="67ebc-387">Consulte [ADF seguro publicar](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) no GitHub toolearn sobre como armazenar informações confidenciais no cofre de chaves do Azure e usá-lo durante a publicação de entidades da fábrica de dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="67ebc-387">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub toolearn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span></span> <span data-ttu-id="67ebc-388">Olá seguro publicar a extensão do Visual Studio permite Olá toobe de segredos armazenada no cofre de chave e somente referências toothem são especificados em serviços vinculados / configurações de implantação.</span><span class="sxs-lookup"><span data-stu-id="67ebc-388">hello Secure Publish extension for Visual Studio allows hello secrets toobe stored in Key Vault and only references toothem are specified in linked services/ deployment configurations.</span></span> <span data-ttu-id="67ebc-389">Essas referências são resolvidas quando você publica tooAzure de entidades da fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="67ebc-389">These references are resolved when you publish Data Factory entities tooAzure.</span></span> <span data-ttu-id="67ebc-390">Esses arquivos podem ser confirmadas toosource repositório sem expor nenhum segredo.</span><span class="sxs-lookup"><span data-stu-id="67ebc-390">These files can then be committed toosource repository without exposing any secrets.</span></span>


## <a name="next-steps"></a><span data-ttu-id="67ebc-391">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="67ebc-391">Next steps</span></span>
<span data-ttu-id="67ebc-392">Neste tutorial, você usou o armazenamento de blobs do Azure como um armazenamento de dados de origem e um banco de dados SQL do Azure como um armazenamento de dados de destino em uma operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="67ebc-392">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="67ebc-393">Olá tabela a seguir fornece uma lista de repositórios de dados com suporte como origens e destinos de atividade de cópia de saudação:</span><span class="sxs-lookup"><span data-stu-id="67ebc-393">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="67ebc-394">toolearn sobre como armazenam dados toocopy para/de uma data, clique o link Olá Olá repositório de dados na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="67ebc-394">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
