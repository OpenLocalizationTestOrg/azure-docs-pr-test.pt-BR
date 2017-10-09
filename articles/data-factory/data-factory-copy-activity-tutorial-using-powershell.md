---
title: 'Tutorial: Criar um pipeline de dados de toomove usando o PowerShell do Azure | Microsoft Docs'
description: "Neste tutorial, você cria um pipeline do Azure Data Factory com uma Atividade de Cópia usando o Azure PowerShell."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 71087349-9365-4e95-9847-170658216ed8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 21406d7dfaa0c555b2538fbb52839d761c140fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-pipeline-that-moves-data-by-using-azure-powershell"></a><span data-ttu-id="74710-103">Tutorial: criar um pipeline do Data Factory que move os dados usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="74710-103">Tutorial: Create a Data Factory pipeline that moves data by using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="74710-104">Visão geral e pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="74710-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="74710-105">Assistente de Cópia</span><span class="sxs-lookup"><span data-stu-id="74710-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="74710-106">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="74710-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="74710-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="74710-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="74710-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="74710-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="74710-109">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="74710-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="74710-110">API REST</span><span class="sxs-lookup"><span data-stu-id="74710-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="74710-111">API do .NET</span><span class="sxs-lookup"><span data-stu-id="74710-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
>
>

<span data-ttu-id="74710-112">Neste artigo, você aprenderá como toouse PowerShell toocreate uma fábrica de dados com um pipeline que copia dados de um banco de dados de SQL do Azure de tooan do armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="74710-112">In this article, you learn how toouse PowerShell toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="74710-113">Se você estiver tooAzure nova fábrica de dados, leia Olá [tooAzure Introdução Data Factory](data-factory-introduction.md) artigo antes de fazer este tutorial.</span><span class="sxs-lookup"><span data-stu-id="74710-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="74710-114">Neste tutorial, você criará um pipeline com uma atividade: atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="74710-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="74710-115">Olá Copiar atividade copia dados de um repositório de dados com suporte de dados repositório tooa coletor com suporte.</span><span class="sxs-lookup"><span data-stu-id="74710-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="74710-116">Para obter uma lista de armazenamentos de dados com suporte como origens e coletores, confira [Armazenamentos de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="74710-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="74710-117">atividade de saudação é alimentada por um serviço disponível globalmente que pode copiar dados entre vários repositórios de dados de forma segura, confiável e escalonável.</span><span class="sxs-lookup"><span data-stu-id="74710-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="74710-118">Para obter mais informações sobre hello atividade de cópia, consulte [atividades de movimentação de dados](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="74710-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="74710-119">Um pipeline pode ter mais de uma atividade.</span><span class="sxs-lookup"><span data-stu-id="74710-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="74710-120">E, é possível encadear duas atividades (executadas uma atividade após o outro), definindo Olá o conjunto de dados de saída de uma atividade Olá outra atividade de conjunto de dados de saudação de entrada.</span><span class="sxs-lookup"><span data-stu-id="74710-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="74710-121">Para saber mais, confira [Várias atividades em um pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="74710-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> <span data-ttu-id="74710-122">Este artigo não aborda todos os cmdlets da fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="74710-122">This article does not cover all hello Data Factory cmdlets.</span></span> <span data-ttu-id="74710-123">Consulte a [Referência de Cmdlet do Data Factory](/powershell/module/azurerm.datafactories) para ter uma documentação completa sobre esses cmdlets.</span><span class="sxs-lookup"><span data-stu-id="74710-123">See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on these cmdlets.</span></span>
> 
> <span data-ttu-id="74710-124">pipeline de dados Olá neste tutorial copia dados de um repositório de dados de destino fonte dados repositório tooa.</span><span class="sxs-lookup"><span data-stu-id="74710-124">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="74710-125">Para obter um tutorial sobre como tootransform dados usando a fábrica de dados do Azure, consulte [Tutorial: Crie um pipeline de dados tootransform usando o cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="74710-125">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74710-126">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="74710-126">Prerequisites</span></span>
- <span data-ttu-id="74710-127">Conclua os pré-requisitos listados em Olá [pré-requisitos do tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="74710-127">Complete prerequisites listed in hello [tutorial prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article.</span></span>
- <span data-ttu-id="74710-128">Instale o **Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="74710-128">Install **Azure PowerShell**.</span></span> <span data-ttu-id="74710-129">Siga as instruções de saudação em [como tooinstall e configurar o Azure PowerShell](../powershell-install-configure.md).</span><span class="sxs-lookup"><span data-stu-id="74710-129">Follow hello instructions in [How tooinstall and configure Azure PowerShell](../powershell-install-configure.md).</span></span>

## <a name="steps"></a><span data-ttu-id="74710-130">Etapas</span><span class="sxs-lookup"><span data-stu-id="74710-130">Steps</span></span>
<span data-ttu-id="74710-131">Aqui estão as etapas Olá que fazem parte deste tutorial:</span><span class="sxs-lookup"><span data-stu-id="74710-131">Here are hello steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="74710-132">Crie um **data factory** do Azure.</span><span class="sxs-lookup"><span data-stu-id="74710-132">Create an Azure **data factory**.</span></span> <span data-ttu-id="74710-133">Nesta etapa, você cria um data factory denominado ADFTutorialDataFactoryPSH.</span><span class="sxs-lookup"><span data-stu-id="74710-133">In this step, you create a data factory named ADFTutorialDataFactoryPSH.</span></span> 
2. <span data-ttu-id="74710-134">Criar **serviços vinculados** na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="74710-134">Create **linked services** in hello data factory.</span></span> <span data-ttu-id="74710-135">Nesta etapa, você criará dois serviços vinculados de tipos: banco de dados SQL e armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="74710-135">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="74710-136">Olá AzureStorageLinkedService vincula sua fábrica de dados de toohello de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="74710-136">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="74710-137">Você criou um contêiner e carregados conta de armazenamento toothis dados como parte de [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="74710-137">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="74710-138">AzureSqlLinkedService vincula sua fábrica de dados de toohello de banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="74710-138">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="74710-139">Olá dados são copiados do armazenamento de blob Olá são armazenados neste banco de dados.</span><span class="sxs-lookup"><span data-stu-id="74710-139">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="74710-140">Você criou uma tabela SQL no banco de dados como parte dos [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="74710-140">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   
3. <span data-ttu-id="74710-141">Criar a entrada e saída **conjuntos de dados** na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="74710-141">Create input and output **datasets** in hello data factory.</span></span>  
    
    <span data-ttu-id="74710-142">serviço de armazenamento do Azure vinculado Olá Especifica a cadeia de conexão de Olá usada pelo serviço de fábrica de dados em tempo de execução tooconnect tooyour conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="74710-142">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="74710-143">E, conjunto de dados de blob de entrada hello Especifica o contêiner de saudação e a pasta de saudação que contém os dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="74710-143">And, hello input blob dataset specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="74710-144">Da mesma forma, Olá serviço de banco de dados do SQL Azure vinculado Especifica a cadeia de caracteres de conexão de saudação que usa o serviço de fábrica de dados no banco de dados SQL do Azure tooyour de tooconnect de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="74710-144">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="74710-145">Além disso, conjunto de dados da tabela SQL Olá saída Especifica a tabela Olá Olá toowhich Olá de banco de dados armazenamento de blob Olá é copiada.</span><span class="sxs-lookup"><span data-stu-id="74710-145">And, hello output SQL table dataset specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>
4. <span data-ttu-id="74710-146">Criar um **pipeline** na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="74710-146">Create a **pipeline** in hello data factory.</span></span> <span data-ttu-id="74710-147">Nesta etapa, você cria um pipeline com a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="74710-147">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="74710-148">Olá Copiar atividade copia dados de um blob na tabela de tooa de armazenamento de BLOBs do Azure de Olá no banco de dados do SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="74710-148">hello copy activity copies data from a blob in hello Azure blob storage tooa table in hello Azure SQL database.</span></span> <span data-ttu-id="74710-149">Você pode usar uma atividade de cópia em um pipeline toocopy os dados de qualquer destino tooany suportada de origem com suporte.</span><span class="sxs-lookup"><span data-stu-id="74710-149">You can use a copy activity in a pipeline toocopy data from any supported source tooany supported destination.</span></span> <span data-ttu-id="74710-150">Para obter uma lista de armazenamentos de dados com suporte, confira o artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="74710-150">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
5. <span data-ttu-id="74710-151">Pipeline de saudação do monitor.</span><span class="sxs-lookup"><span data-stu-id="74710-151">Monitor hello pipeline.</span></span> <span data-ttu-id="74710-152">Nesta etapa, você **monitor** Olá fatias de conjuntos de dados de entrada e saídas usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="74710-152">In this step, you **monitor** hello slices of input and output datasets by using PowerShell.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="74710-153">Criar uma data factory</span><span class="sxs-lookup"><span data-stu-id="74710-153">Create a data factory</span></span>
> [!IMPORTANT]
> <span data-ttu-id="74710-154">Concluída [pré-requisitos para o tutorial Olá](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) se você ainda não tiver feito isso.</span><span class="sxs-lookup"><span data-stu-id="74710-154">Complete [prerequisites for hello tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) if you haven't already done so.</span></span>   

<span data-ttu-id="74710-155">Uma fábrica de dados pode ter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="74710-155">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="74710-156">Um pipeline em um data factory pode ter uma ou mais atividades.</span><span class="sxs-lookup"><span data-stu-id="74710-156">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="74710-157">Por exemplo, dados de toocopy uma atividade de cópia de um repositório de dados de destino do código-fonte tooa e uma atividade de Hive do HDInsight toorun um tootransform de script do Hive dados de saída de tooproduct dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="74710-157">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="74710-158">Vamos começar com a criação de fábrica de dados Olá nesta etapa.</span><span class="sxs-lookup"><span data-stu-id="74710-158">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="74710-159">Inicie o **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="74710-159">Launch **PowerShell**.</span></span> <span data-ttu-id="74710-160">Mantenha o Azure PowerShell aberta até o fim deste tutorial hello.</span><span class="sxs-lookup"><span data-stu-id="74710-160">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="74710-161">Se você fecha e reabrir o, será necessário comandos de saudação toorun novamente.</span><span class="sxs-lookup"><span data-stu-id="74710-161">If you close and reopen, you need toorun hello commands again.</span></span>

    <span data-ttu-id="74710-162">Execute Olá comando a seguir e insira o nome de usuário de saudação e a senha que você use toosign em toohello portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="74710-162">Run hello following command, and enter hello user name and password that you use toosign in toohello Azure portal:</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```   
   
    <span data-ttu-id="74710-163">Execute todas as assinaturas de saudação para esta conta de Olá tooview de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="74710-163">Run hello following command tooview all hello subscriptions for this account:</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="74710-164">Execute Olá assinatura de saudação do comando tooselect que você deseja toowork com a seguir.</span><span class="sxs-lookup"><span data-stu-id="74710-164">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="74710-165">Substituir  **&lt;NameOfAzureSubscription** &gt; com o nome da saudação de sua assinatura do Azure:</span><span class="sxs-lookup"><span data-stu-id="74710-165">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription:</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
2. <span data-ttu-id="74710-166">Criar um grupo de recursos do Azure denominado **ADFTutorialResourceGroup** executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="74710-166">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    
    <span data-ttu-id="74710-167">Algumas das etapas neste tutorial Olá pressupõem que você use o grupo de recursos de saudação chamado **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="74710-167">Some of hello steps in this tutorial assume that you use hello resource group named **ADFTutorialResourceGroup**.</span></span> <span data-ttu-id="74710-168">Se você usar um grupo de recursos diferentes, será necessário toouse-lo no lugar de ADFTutorialResourceGroup neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="74710-168">If you use a different resource group, you need toouse it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="74710-169">Executar Olá **New-AzureRmDataFactory** toocreate cmdlet uma fábrica de dados denominada **ADFTutorialDataFactoryPSH**:</span><span class="sxs-lookup"><span data-stu-id="74710-169">Run hello **New-AzureRmDataFactory** cmdlet toocreate a data factory named **ADFTutorialDataFactoryPSH**:</span></span>  

    ```PowerShell
    $df=New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH –Location "West US"
    ```
    <span data-ttu-id="74710-170">Esse nome pode já ter sido usado.</span><span class="sxs-lookup"><span data-stu-id="74710-170">This name may already have been taken.</span></span> <span data-ttu-id="74710-171">Portanto, tornar nome Olá Olá da fábrica de dados exclusivo, adicionando um prefixo ou sufixo (por exemplo: ADFTutorialDataFactoryPSH05152017) e execute novamente o comando hello.</span><span class="sxs-lookup"><span data-stu-id="74710-171">Therefore, make hello name of hello data factory unique by adding a prefix or suffix (for example: ADFTutorialDataFactoryPSH05152017) and run hello command again.</span></span>  

<span data-ttu-id="74710-172">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="74710-172">Note hello following points:</span></span>

* <span data-ttu-id="74710-173">nome de Olá Olá do Azure da fábrica de dados deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="74710-173">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="74710-174">Se você receber Olá erro a seguir, altere o nome de saudação (por exemplo, yournameADFTutorialDataFactoryPSH).</span><span class="sxs-lookup"><span data-stu-id="74710-174">If you receive hello following error, change hello name (for example, yournameADFTutorialDataFactoryPSH).</span></span> <span data-ttu-id="74710-175">Use esse nome em vez de ADFTutorialFactoryPSH ao executar as etapas neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="74710-175">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="74710-176">Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver os artefatos do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="74710-176">See [Data Factory - Naming Rules](data-factory-naming-rules.md) for Data Factory artifacts.</span></span>

    ```
    Data factory name “ADFTutorialDataFactoryPSH” is not available
    ```
* <span data-ttu-id="74710-177">toocreate instâncias de fábrica de dados, você deve ser um colaborador ou o administrador de saudação assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="74710-177">toocreate Data Factory instances, you must be a contributor or administrator of hello Azure subscription.</span></span>
* <span data-ttu-id="74710-178">nome Olá Olá da fábrica de dados pode ser registrado como um nome DNS no hello futuro e, portanto, se tornar publicamente visível.</span><span class="sxs-lookup"><span data-stu-id="74710-178">hello name of hello data factory may be registered as a DNS name in hello future, and hence become publicly visible.</span></span>
* <span data-ttu-id="74710-179">Você pode receber Olá erro a seguir: "**esta assinatura não está registrado toouse namespace DataFactory.**"</span><span class="sxs-lookup"><span data-stu-id="74710-179">You may receive hello following error: "**This subscription is not registered toouse namespace Microsoft.DataFactory.**"</span></span> <span data-ttu-id="74710-180">Execute um dos seguintes hello e tente publicar novamente:</span><span class="sxs-lookup"><span data-stu-id="74710-180">Do one of hello following, and try publishing again:</span></span>

  * <span data-ttu-id="74710-181">No Azure PowerShell, execute Olá provedor do comando tooregister Olá fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="74710-181">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

    <span data-ttu-id="74710-182">Olá execução tooconfirm de comando que Olá provedor de fábrica de dados a seguir está registrado:</span><span class="sxs-lookup"><span data-stu-id="74710-182">Run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="74710-183">Entrar usando Olá assinatura do Azure toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="74710-183">Sign in by using hello Azure subscription toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="74710-184">Vá tooa folha de fábrica de dados ou criar uma fábrica de dados no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="74710-184">Go tooa Data Factory blade, or create a data factory in hello Azure portal.</span></span> <span data-ttu-id="74710-185">Esta ação registra automaticamente o provedor de saudação para você.</span><span class="sxs-lookup"><span data-stu-id="74710-185">This action automatically registers hello provider for you.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="74710-186">Criar serviços vinculados</span><span class="sxs-lookup"><span data-stu-id="74710-186">Create linked services</span></span>
<span data-ttu-id="74710-187">Você pode criar serviços vinculados em um toolink de fábrica de dados seus dados, armazena e fábrica de dados toohello de serviços de computação.</span><span class="sxs-lookup"><span data-stu-id="74710-187">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="74710-188">Neste tutorial, você não usa serviços de computação, como o Azure HDInsight ou o Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="74710-188">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="74710-189">Você usa dois armazenamentos de dados do tipo Armazenamento do Azure (origem) e o banco de dados SQL (destino).</span><span class="sxs-lookup"><span data-stu-id="74710-189">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="74710-190">Portanto, você pode criar dois serviços vinculados, chamados AzureStorageLinkedService e AzureSqlLinkedService, dos tipos: AzureStorage e AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="74710-190">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="74710-191">Olá AzureStorageLinkedService vincula sua fábrica de dados de toohello de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="74710-191">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="74710-192">Esta conta de armazenamento é hello um no qual você criou um contêiner e carregou dados de saudação como parte do [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="74710-192">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="74710-193">AzureSqlLinkedService vincula sua fábrica de dados de toohello de banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="74710-193">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="74710-194">Olá dados são copiados do armazenamento de blob Olá são armazenados neste banco de dados.</span><span class="sxs-lookup"><span data-stu-id="74710-194">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="74710-195">Você criou tabela emp de saudação neste banco de dados como parte do [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="74710-195">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="create-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="74710-196">Criar um serviço vinculado para uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="74710-196">Create a linked service for an Azure storage account</span></span>
<span data-ttu-id="74710-197">Nesta etapa, você vincular sua fábrica de dados de tooyour de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="74710-197">In this step, you link your Azure storage account tooyour data factory.</span></span>

1. <span data-ttu-id="74710-198">Crie um arquivo JSON chamado **AzureStorageLinkedService.json** na **C:\ADFGetStartedPSH** pasta com hello conteúdo a seguir: (criar hello pasta ADFGetStartedPSH se ele ainda não existir.)</span><span class="sxs-lookup"><span data-stu-id="74710-198">Create a JSON file named **AzureStorageLinkedService.json** in **C:\ADFGetStartedPSH** folder with hello following content: (Create hello folder ADFGetStartedPSH if it does not already exist.)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="74710-199">Substituir &lt;accountname&gt; e &lt;accountkey&gt; com o nome e a chave da sua conta de armazenamento do Azure antes de salvar o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="74710-199">Replace &lt;accountname&gt; and &lt;accountkey&gt; with name and key of your Azure storage account before saving hello file.</span></span> 

    ```json
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
2. <span data-ttu-id="74710-200">Em **Azure PowerShell**, alternar toohello **ADFGetStartedPSH** pasta.</span><span class="sxs-lookup"><span data-stu-id="74710-200">In **Azure PowerShell**, switch toohello **ADFGetStartedPSH** folder.</span></span>
4. <span data-ttu-id="74710-201">Executar Olá **New-AzureRmDataFactoryLinkedService** serviço vinculado do cmdlet toocreate Olá: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="74710-201">Run hello **New-AzureRmDataFactoryLinkedService** cmdlet toocreate hello linked service: **AzureStorageLinkedService**.</span></span> <span data-ttu-id="74710-202">Esse cmdlet e outros cmdlets de fábrica de dados que você usar este tutorial requer que você toopass valores para Olá **ResourceGroupName** e **DataFactoryName** parâmetros.</span><span class="sxs-lookup"><span data-stu-id="74710-202">This cmdlet, and other Data Factory cmdlets you use in this tutorial requires you toopass values for hello **ResourceGroupName** and **DataFactoryName** parameters.</span></span> <span data-ttu-id="74710-203">Como alternativa, você pode passar o objeto de DataFactory de saudação retornado o cmdlet New-AzureRmDataFactory Olá sem digitar ResourceGroupName e DataFactoryName toda vez que você executar um cmdlet.</span><span class="sxs-lookup"><span data-stu-id="74710-203">Alternatively, you can pass hello DataFactory object returned by hello New-AzureRmDataFactory cmdlet without typing ResourceGroupName and DataFactoryName each time you run a cmdlet.</span></span> 

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureStorageLinkedService.json
    ```
    <span data-ttu-id="74710-204">Aqui está a saída de exemplo hello:</span><span class="sxs-lookup"><span data-stu-id="74710-204">Here is hello sample output:</span></span>

    ```
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ``` 

    <span data-ttu-id="74710-205">Outra maneira de criar esse serviço vinculado é toospecify nome do grupo de recursos e o nome da fábrica de dados em vez de especificar o objeto de DataFactory hello.</span><span class="sxs-lookup"><span data-stu-id="74710-205">Other way of creating this linked service is toospecify resource group name and data factory name instead of specifying hello DataFactory object.</span></span>  

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName <Name of your data factory> -File .\AzureStorageLinkedService.json
    ```

### <a name="create-a-linked-service-for-an-azure-sql-database"></a><span data-ttu-id="74710-206">Criar um serviço vinculado para um banco de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="74710-206">Create a linked service for an Azure SQL database</span></span>
<span data-ttu-id="74710-207">Nesta etapa, você vincular sua fábrica de dados de tooyour de banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="74710-207">In this step, you link your Azure SQL database tooyour data factory.</span></span>

1. <span data-ttu-id="74710-208">Crie um arquivo JSON chamado AzureSqlLinkedService.json na pasta C:\ADFGetStartedPSH com hello seguindo conteúdo:</span><span class="sxs-lookup"><span data-stu-id="74710-208">Create a JSON file named AzureSqlLinkedService.json in C:\ADFGetStartedPSH folder with hello following content:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="74710-209">Substitua &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt; e &lt;password&gt; pelos nomes de seu servidor SQL do Azure, banco de dados, conta de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="74710-209">Replace &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt;, and &lt;password&gt; with names of your Azure SQL server, database, user account, and password.</span></span>
    
    ```json
    {
        "name": "AzureSqlLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": "Server=tcp:<server>.database.windows.net,1433;Database=<databasename>;User ID=<user>@<server>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        }
     }
    ```
2. <span data-ttu-id="74710-210">Execute um serviço vinculado de saudação toocreate de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="74710-210">Run hello following command toocreate a linked service:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureSqlLinkedService.json
    ```
    
    <span data-ttu-id="74710-211">Aqui está a saída de exemplo hello:</span><span class="sxs-lookup"><span data-stu-id="74710-211">Here is hello sample output:</span></span>

    ```
    LinkedServiceName : AzureSqlLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ```

   <span data-ttu-id="74710-212">Confirme se **permitir acesso a serviços tooAzure** configuração está ativada para o servidor de banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="74710-212">Confirm that **Allow access tooAzure services** setting is turned on for your SQL database server.</span></span> <span data-ttu-id="74710-213">tooverify e ativá-lo, Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="74710-213">tooverify and turn it on, do hello following steps:</span></span>

    1. <span data-ttu-id="74710-214">Faça logon no toohello [portal do Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="74710-214">Log in toohello [Azure portal](https://portal.azure.com)</span></span>
    2. <span data-ttu-id="74710-215">Clique em **mais serviços >** Olá esquerda e clique em **servidores SQL** em Olá **bancos de dados** categoria.</span><span class="sxs-lookup"><span data-stu-id="74710-215">Click **More services >** on hello left, and click **SQL servers** in hello **DATABASES** category.</span></span>
    3. <span data-ttu-id="74710-216">Selecione o servidor na lista de saudação de SQL servers.</span><span class="sxs-lookup"><span data-stu-id="74710-216">Select your server in hello list of SQL servers.</span></span>
    4. <span data-ttu-id="74710-217">Na folha saudação do SQL server, clique em **Mostrar configurações de firewall** link.</span><span class="sxs-lookup"><span data-stu-id="74710-217">On hello SQL server blade, click **Show firewall settings** link.</span></span>
    5. <span data-ttu-id="74710-218">Em Olá **configurações de Firewall** folha, clique em **ON** para **permitir acesso a serviços tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="74710-218">In hello **Firewall settings** blade, click **ON** for **Allow access tooAzure services**.</span></span>
    6. <span data-ttu-id="74710-219">Clique em **salvar** na barra de ferramentas de saudação.</span><span class="sxs-lookup"><span data-stu-id="74710-219">Click **Save** on hello toolbar.</span></span> 

## <a name="create-datasets"></a><span data-ttu-id="74710-220">Criar conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="74710-220">Create datasets</span></span>
<span data-ttu-id="74710-221">Na etapa anterior de saudação, você criou serviços vinculados toolink sua conta de armazenamento do Azure e a fábrica de dados de tooyour de banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="74710-221">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="74710-222">Nesta etapa, você definirá dois conjuntos de dados denominados InputDataset OutputDataset que representam a entrada e saída dados e que são armazenados em repositórios de dados Olá referenciados por AzureStorageLinkedService e AzureSqlLinkedService, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="74710-222">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="74710-223">serviço de armazenamento do Azure vinculado Olá Especifica a cadeia de conexão de Olá usada pelo serviço de fábrica de dados em tempo de execução tooconnect tooyour conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="74710-223">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="74710-224">E, Olá o conjunto de dados de blob de entrada (InputDataset) Especifica o contêiner de saudação e a pasta de saudação que contém os dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="74710-224">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="74710-225">Da mesma forma, Olá serviço de banco de dados do SQL Azure vinculado Especifica a cadeia de caracteres de conexão de saudação que usa o serviço de fábrica de dados no banco de dados SQL do Azure tooyour de tooconnect de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="74710-225">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="74710-226">E, Olá saída SQL o conjunto de dados de tabela (OututDataset) Especifica a tabela de saudação em Olá Olá de toowhich de banco de dados dados saudação do armazenamento de blob são copiados.</span><span class="sxs-lookup"><span data-stu-id="74710-226">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-an-input-dataset"></a><span data-ttu-id="74710-227">Criar um conjunto de dados de entrada</span><span class="sxs-lookup"><span data-stu-id="74710-227">Create an input dataset</span></span>
<span data-ttu-id="74710-228">Nesta etapa, você criar um conjunto de dados chamado InputDataset que aponta o arquivo de blob tooa (emp.txt) na pasta raiz de saudação de um contêiner de blob (adftutorial) no hello representado por Olá AzureStorageLinkedService vinculado de serviço de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="74710-228">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="74710-229">Se você não especificar um valor para o nome de arquivo hello (ou ignorá-lo), dados de todos os blobs na pasta de entrada hello são copiados toohello destino.</span><span class="sxs-lookup"><span data-stu-id="74710-229">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="74710-230">Neste tutorial, você deve especificar um valor para o nome de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="74710-230">In this tutorial, you specify a value for hello fileName.</span></span>  

1. <span data-ttu-id="74710-231">Crie um arquivo JSON chamado **InputDataset.json** em Olá **C:\ADFGetStartedPSH** pasta com hello conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="74710-231">Create a JSON file named **InputDataset.json** in hello **C:\ADFGetStartedPSH** folder, with hello following content:</span></span>

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
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "emp.txt",
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

    <span data-ttu-id="74710-232">Olá, tabela a seguir fornece descrições para propriedades JSON Olá usadas no trecho hello:</span><span class="sxs-lookup"><span data-stu-id="74710-232">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="74710-233">Propriedade</span><span class="sxs-lookup"><span data-stu-id="74710-233">Property</span></span> | <span data-ttu-id="74710-234">Descrição</span><span class="sxs-lookup"><span data-stu-id="74710-234">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="74710-235">type</span><span class="sxs-lookup"><span data-stu-id="74710-235">type</span></span> | <span data-ttu-id="74710-236">propriedade do tipo Hello está definida muito**AzureBlob** porque os dados residem em um armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="74710-236">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="74710-237">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="74710-237">linkedServiceName</span></span> | <span data-ttu-id="74710-238">Refere-se toohello **AzureStorageLinkedService** que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="74710-238">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="74710-239">folderPath</span><span class="sxs-lookup"><span data-stu-id="74710-239">folderPath</span></span> | <span data-ttu-id="74710-240">Especifica o blob Olá **contêiner** e hello **pasta** que contém blobs de entrada.</span><span class="sxs-lookup"><span data-stu-id="74710-240">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="74710-241">Neste tutorial, adftutorial é o contêiner de blob hello e pasta é a pasta raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="74710-241">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
    | <span data-ttu-id="74710-242">fileName</span><span class="sxs-lookup"><span data-stu-id="74710-242">fileName</span></span> | <span data-ttu-id="74710-243">Essa propriedade é opcional.</span><span class="sxs-lookup"><span data-stu-id="74710-243">This property is optional.</span></span> <span data-ttu-id="74710-244">Se você omitir essa propriedade, todos os arquivos de saudação folderPath são escolhidos.</span><span class="sxs-lookup"><span data-stu-id="74710-244">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="74710-245">Neste tutorial, **emp.txt** é especificado para hello fileName, portanto, somente esse arquivo é escolhida para processamento.</span><span class="sxs-lookup"><span data-stu-id="74710-245">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="74710-246">formato -> tipo</span><span class="sxs-lookup"><span data-stu-id="74710-246">format -> type</span></span> |<span data-ttu-id="74710-247">arquivo de entrada Hello está no formato de texto de saudação, para que possamos usar **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="74710-247">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="74710-248">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="74710-248">columnDelimiter</span></span> | <span data-ttu-id="74710-249">saudação de colunas no arquivo de entrada hello é delimitadas por **caractere de vírgula (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="74710-249">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="74710-250">frequência/intervalo</span><span class="sxs-lookup"><span data-stu-id="74710-250">frequency/interval</span></span> | <span data-ttu-id="74710-251">frequência de saudação está definida muito**hora** e o intervalo é definido muito**1**, que significa que Olá entrada fatias estão disponíveis **por hora**.</span><span class="sxs-lookup"><span data-stu-id="74710-251">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="74710-252">Em outras palavras, Olá serviço da fábrica de dados procura por dados de entrada a cada hora na pasta raiz de saudação do contêiner de blob (**adftutorial**) especificado.</span><span class="sxs-lookup"><span data-stu-id="74710-252">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="74710-253">Ele procura os dados de saudação em Olá pipeline início e término vezes, não antes ou depois desses tempos.</span><span class="sxs-lookup"><span data-stu-id="74710-253">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="74710-254">externo</span><span class="sxs-lookup"><span data-stu-id="74710-254">external</span></span> | <span data-ttu-id="74710-255">Essa propriedade é definida, muito**true** se os dados de saudação não são gerados por este pipeline.</span><span class="sxs-lookup"><span data-stu-id="74710-255">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="74710-256">dados de entrada Hello neste tutorial estão no arquivo de emp.txt hello, que não é gerado por este pipeline, portanto vamos definir essa propriedade tootrue.</span><span class="sxs-lookup"><span data-stu-id="74710-256">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

    <span data-ttu-id="74710-257">Para saber mais sobre essas propriedades JSON, confira o [artigo sobre o conector do Blob do Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="74710-257">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
2. <span data-ttu-id="74710-258">Execute Olá o conjunto de dados do comando toocreate Olá fábrica de dados a seguir.</span><span class="sxs-lookup"><span data-stu-id="74710-258">Run hello following command toocreate hello Data Factory dataset.</span></span>

    ```PowerShell  
    New-AzureRmDataFactoryDataset $df -File .\InputDataset.json
    ```
    <span data-ttu-id="74710-259">Aqui está a saída de exemplo hello:</span><span class="sxs-lookup"><span data-stu-id="74710-259">Here is hello sample output:</span></span>

    ```
    DatasetName       : InputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureBlobDataset
    Policy            : Microsoft.Azure.Management.DataFactories.Common.Models.Policy
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

### <a name="create-an-output-dataset"></a><span data-ttu-id="74710-260">Criar um conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="74710-260">Create an output dataset</span></span>
<span data-ttu-id="74710-261">Nesta parte da etapa hello, você cria um conjunto de dados de saída denominado **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="74710-261">In this part of hello step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="74710-262">Este conjunto de dados aponta tooa SQL tabela no banco de dados do SQL Azure Olá representado por **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="74710-262">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService**.</span></span> 

1. <span data-ttu-id="74710-263">Crie um arquivo JSON chamado **OutputDataset.json** em Olá **C:\ADFGetStartedPSH** pasta com hello conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="74710-263">Create a JSON file named **OutputDataset.json** in hello **C:\ADFGetStartedPSH** folder with hello following content:</span></span>

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

    <span data-ttu-id="74710-264">Olá, tabela a seguir fornece descrições para propriedades JSON Olá usadas no trecho hello:</span><span class="sxs-lookup"><span data-stu-id="74710-264">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="74710-265">Propriedade</span><span class="sxs-lookup"><span data-stu-id="74710-265">Property</span></span> | <span data-ttu-id="74710-266">Descrição</span><span class="sxs-lookup"><span data-stu-id="74710-266">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="74710-267">type</span><span class="sxs-lookup"><span data-stu-id="74710-267">type</span></span> | <span data-ttu-id="74710-268">propriedade do tipo Hello está definida muito**AzureSqlTable** porque os dados são copiados tooa tabela em um banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="74710-268">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="74710-269">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="74710-269">linkedServiceName</span></span> | <span data-ttu-id="74710-270">Refere-se toohello **AzureSqlLinkedService** que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="74710-270">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="74710-271">tableName</span><span class="sxs-lookup"><span data-stu-id="74710-271">tableName</span></span> | <span data-ttu-id="74710-272">Olá especificado **tabela** toowhich Olá dados são copiados.</span><span class="sxs-lookup"><span data-stu-id="74710-272">Specified hello **table** toowhich hello data is copied.</span></span> | 
    | <span data-ttu-id="74710-273">frequência/intervalo</span><span class="sxs-lookup"><span data-stu-id="74710-273">frequency/interval</span></span> | <span data-ttu-id="74710-274">Olá frequência é definida muito**hora** e o intervalo é **1**, o que significa que Olá fatias de saída são produzidas **por hora** entre Olá pipeline início e término vezes, não antes ou Após esses horários.</span><span class="sxs-lookup"><span data-stu-id="74710-274">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="74710-275">Há três colunas – **ID**, **FirstName**, e **LastName** – na tabela de emp Olá no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="74710-275">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="74710-276">ID é uma coluna de identidade, portanto, você precisa apenas toospecify **FirstName** e **LastName** aqui.</span><span class="sxs-lookup"><span data-stu-id="74710-276">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="74710-277">Para saber mais sobre essas propriedades JSON, confira o [artigo sobre o conector do SQL](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="74710-277">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
2. <span data-ttu-id="74710-278">Execute Olá comando toocreate Olá dados fábrica conjunto de dados a seguir.</span><span class="sxs-lookup"><span data-stu-id="74710-278">Run hello following command toocreate hello data factory dataset.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryDataset $df -File .\OutputDataset.json
    ```

    <span data-ttu-id="74710-279">Aqui está a saída de exemplo hello:</span><span class="sxs-lookup"><span data-stu-id="74710-279">Here is hello sample output:</span></span>

    ```
    DatasetName       : OutputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureSqlTableDataset
    Policy            :
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

## <a name="create-a-pipeline"></a><span data-ttu-id="74710-280">Criar uma pipeline</span><span class="sxs-lookup"><span data-stu-id="74710-280">Create a pipeline</span></span>
<span data-ttu-id="74710-281">Nesta etapa, você cria um pipeline com uma **atividade de cópia** que usa **InputDataset** como entrada e **OutputDataset** como saída.</span><span class="sxs-lookup"><span data-stu-id="74710-281">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="74710-282">Atualmente, o conjunto de dados de saída é quais unidades Olá agenda.</span><span class="sxs-lookup"><span data-stu-id="74710-282">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="74710-283">Neste tutorial, o conjunto de dados de saída é configurado tooproduce uma fatia de uma vez por hora.</span><span class="sxs-lookup"><span data-stu-id="74710-283">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="74710-284">pipeline de saudação tem uma hora de início e a hora de término que são um dia de distância, que é de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="74710-284">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="74710-285">Portanto, 24 fatias de conjunto de dados de saída são produzidas pelo pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="74710-285">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 


1. <span data-ttu-id="74710-286">Crie um arquivo JSON chamado **ADFTutorialPipeline.json** em Olá **C:\ADFGetStartedPSH** pasta com hello conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="74710-286">Create a JSON file named **ADFTutorialPipeline.json** in hello **C:\ADFGetStartedPSH** folder, with hello following content:</span></span>

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
    <span data-ttu-id="74710-287">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="74710-287">Note hello following points:</span></span>
   
    - <span data-ttu-id="74710-288">Na seção de atividades hello, há apenas uma atividade cuja **tipo** está definido muito**cópia**.</span><span class="sxs-lookup"><span data-stu-id="74710-288">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="74710-289">Para obter mais informações sobre a atividade de cópia hello, consulte [atividades de movimentação de dados](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="74710-289">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="74710-290">Nas soluções de Data Factory, você também pode usar [atividades de transformação de dados](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="74710-290">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="74710-291">Entrada para atividade de saudação é definida muito**InputDataset** e de saída para o conjunto de hello atividade é muito**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="74710-291">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="74710-292">Em Olá **typeProperties** seção, **BlobSource** é especificado como tipo de fonte hello e **SqlSink** é especificado como tipo de coletor de saudação.</span><span class="sxs-lookup"><span data-stu-id="74710-292">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="74710-293">Para obter uma lista completa de armazenamentos de dados de atividade de cópia hello como origens e coletores com suporte, consulte [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="74710-293">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="74710-294">toolearn como toouse dados específicos com suporte são armazenados como um fonte/coletor, clique o link de saudação na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="74710-294">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
     
    <span data-ttu-id="74710-295">Substituir valor Olá Olá **iniciar** propriedade com hello dia atual e **final** valor com hello dia seguinte.</span><span class="sxs-lookup"><span data-stu-id="74710-295">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="74710-296">Você pode especificar apenas parte da data hello e ignore a parte de hora de saudação da saudação data hora.</span><span class="sxs-lookup"><span data-stu-id="74710-296">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="74710-297">Por exemplo, "2016-02-03", que é o equivalente muito "2016-02-03T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="74710-297">For example, "2016-02-03", which is equivalent too"2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="74710-298">Ambos os valores de data/hora de início e de término devem estar no [formato ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="74710-298">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="74710-299">Por exemplo: 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="74710-299">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="74710-300">Olá **final** tempo é opcional, mas usamos neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="74710-300">hello **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="74710-301">Se você não especificar o valor para Olá **final** propriedade, ele é calculado como "**início + 48 horas**".</span><span class="sxs-lookup"><span data-stu-id="74710-301">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="74710-302">pipeline de saudação toorun indefinidamente, especifique **9999-09-09** como valor Olá Olá **final** propriedade.</span><span class="sxs-lookup"><span data-stu-id="74710-302">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
     
    <span data-ttu-id="74710-303">Olá anterior de exemplo, há 24 fatias de dados como cada fatia de dados é produzida por hora.</span><span class="sxs-lookup"><span data-stu-id="74710-303">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="74710-304">Para obter descrições das propriedades JSON em uma definição de pipeline, consulte o artigo [Criar pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="74710-304">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="74710-305">Para obter descrições das propriedades JSON em uma definição de atividade de cópia, consulte [Atividades de movimentação de dados](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="74710-305">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="74710-306">Para obter descrições das propriedades JSON com suporte pelo BlobSource, consulte o [artigo sobre o conector de blobs do Azure](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="74710-306">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="74710-307">Para obter descrições das propriedades JSON com suporte pelo SqlSink, consulte o [artigo sobre o conector do Banco de Dados SQL](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="74710-307">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>
2. <span data-ttu-id="74710-308">Execute Olá comando toocreate Olá dados fábrica a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="74710-308">Run hello following command toocreate hello data factory table.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryPipeline $df -File .\ADFTutorialPipeline.json
    ```

    <span data-ttu-id="74710-309">Aqui está a saída de exemplo hello:</span><span class="sxs-lookup"><span data-stu-id="74710-309">Here is hello sample output:</span></span> 

    ```
    PipelineName      : ADFTutorialPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.PipelinePropertie
    ProvisioningState : Succeeded
    ```

<span data-ttu-id="74710-310">**Parabéns!**</span><span class="sxs-lookup"><span data-stu-id="74710-310">**Congratulations!**</span></span> <span data-ttu-id="74710-311">Você criou com êxito uma fábrica de dados do Azure com um pipeline toocopy os dados de um banco de dados de SQL do Azure de tooan do armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="74710-311">You have successfully created an Azure data factory with a pipeline toocopy data from an Azure blob storage tooan Azure SQL database.</span></span> 

## <a name="monitor-hello-pipeline"></a><span data-ttu-id="74710-312">Pipeline de saudação do monitor</span><span class="sxs-lookup"><span data-stu-id="74710-312">Monitor hello pipeline</span></span>
<span data-ttu-id="74710-313">Nesta etapa, você use toomonitor do PowerShell do Azure que está acontecendo em uma fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="74710-313">In this step, you use Azure PowerShell toomonitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="74710-314">Substituir &lt;DataFactoryName&gt; com o nome da saudação de fábrica de dados e executar **Get-AzureRmDataFactory**e atribuir Olá saída tooa $df variável.</span><span class="sxs-lookup"><span data-stu-id="74710-314">Replace &lt;DataFactoryName&gt; with hello name of your data factory and run **Get-AzureRmDataFactory**, and assign hello output tooa variable $df.</span></span>

    ```PowerShell  
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name <DataFactoryName>
    ```

    <span data-ttu-id="74710-315">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="74710-315">For example:</span></span>
    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH0516
    ```
    
    <span data-ttu-id="74710-316">Em seguida, execute o conteúdo Olá impressão $df toosee Olá saída a seguir:</span><span class="sxs-lookup"><span data-stu-id="74710-316">Then, run print hello contents of $df toosee hello following output:</span></span> 
    
    ```
    PS C:\ADFGetStartedPSH> $df
    
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DataFactoryId     : 6f194b34-03b3-49ab-8f03-9f8a7b9d3e30
    ResourceGroupName : ADFTutorialResourceGroup
    Location          : West US
    Tags              : {}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DataFactoryProperties
    ProvisioningState : Succeeded
    ```
2. <span data-ttu-id="74710-317">Executar **Get-AzureRmDataFactorySlice** tooget detalhes sobre todas as fatias de saudação **OutputDataset**, que é o conjunto de dados de saída de saudação do pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="74710-317">Run **Get-AzureRmDataFactorySlice** tooget details about all slices of hello **OutputDataset**, which is hello output dataset of hello pipeline.</span></span>  

    ```PowerShell   
    Get-AzureRmDataFactorySlice $df -DatasetName OutputDataset -StartDateTime 2017-05-11T00:00:00Z
    ```

   <span data-ttu-id="74710-318">Essa configuração deve corresponder a saudação **iniciar** valor em JSON de pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="74710-318">This setting should match hello **Start** value in hello pipeline JSON.</span></span> <span data-ttu-id="74710-319">Você deve ver 24 fatias, uma para cada hora de 12 AM de saudação dia atual too12 estou de saudação dia seguinte.</span><span class="sxs-lookup"><span data-stu-id="74710-319">You should see 24 slices, one for each hour from 12 AM of hello current day too12 AM of hello next day.</span></span>

   <span data-ttu-id="74710-320">Aqui estão os três intervalos de exemplo de saída de hello:</span><span class="sxs-lookup"><span data-stu-id="74710-320">Here are three sample slices from hello output:</span></span> 

    ``` 
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 11:00:00 PM
    End               : 5/12/2017 12:00:00 AM
    RetryCount        : 0
    State             : Ready
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 9:00:00 PM
    End               : 5/11/2017 10:00:00 PM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0   

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 8:00:00 PM
    End               : 5/11/2017 9:00:00 PM
    RetryCount        : 0
    State             : Waiting
    SubState          : ConcurrencyLimit
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. <span data-ttu-id="74710-321">Executar **Get-AzureRmDataFactoryRun** tooget detalhes de saudação da atividade for executada por um **específico** fatia.</span><span class="sxs-lookup"><span data-stu-id="74710-321">Run **Get-AzureRmDataFactoryRun** tooget hello details of activity runs for a **specific** slice.</span></span> <span data-ttu-id="74710-322">Copie o valor de data e hora de saudação da saída Olá Olá comando toospecify Olá valor anterior para o parâmetro de StartDateTime hello.</span><span class="sxs-lookup"><span data-stu-id="74710-322">Copy hello date-time value from hello output of hello previous command toospecify hello value for hello StartDateTime parameter.</span></span> 

    ```PowerShell  
    Get-AzureRmDataFactoryRun $df -DatasetName OutputDataset -StartDateTime "5/11/2017 09:00:00 PM"
    ```

   <span data-ttu-id="74710-323">Aqui está a saída de exemplo hello:</span><span class="sxs-lookup"><span data-stu-id="74710-323">Here is hello sample output:</span></span> 

    ```
    Id                  : c0ddbd75-d0c7-4816-a775-704bbd7c7eab_636301332000000000_636301368000000000_OutputDataset
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : ADFTutorialDataFactoryPSH0516
    DatasetName         : OutputDataset
    ProcessingStartTime : 5/16/2017 8:00:33 PM
    ProcessingEndTime   : 5/16/2017 8:01:36 PM
    PercentComplete     : 100
    DataSliceStart      : 5/11/2017 9:00:00 PM
    DataSliceEnd        : 5/11/2017 10:00:00 PM
    Status              : Succeeded
    Timestamp           : 5/16/2017 8:00:33 PM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : CopyFromBlobToSQL
    PipelineName        : ADFTutorialPipeline
    Type                : Copy  
    ```

<span data-ttu-id="74710-324">Para obter uma documentação abrangente sobre os cmdlets de Data Factory, consulte [Referência de cmdlet de Data Factory](/powershell/module/azurerm.datafactories).</span><span class="sxs-lookup"><span data-stu-id="74710-324">For comprehensive documentation on Data Factory cmdlets, see [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories).</span></span>

## <a name="summary"></a><span data-ttu-id="74710-325">Resumo</span><span class="sxs-lookup"><span data-stu-id="74710-325">Summary</span></span>
<span data-ttu-id="74710-326">Neste tutorial, você criou um Azure fábrica toocopy dados de um banco de dados do SQL Azure de tooan BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="74710-326">In this tutorial, you created an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="74710-327">Você usou a fábrica de dados do PowerShell toocreate hello, serviços vinculados, conjuntos de dados e um pipeline.</span><span class="sxs-lookup"><span data-stu-id="74710-327">You used PowerShell toocreate hello data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="74710-328">Aqui estão as etapas de alto nível Olá executada neste tutorial:</span><span class="sxs-lookup"><span data-stu-id="74710-328">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="74710-329">Foi criada uma **data factory**do Azure.</span><span class="sxs-lookup"><span data-stu-id="74710-329">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="74710-330">Foram criados **serviços vinculados**:</span><span class="sxs-lookup"><span data-stu-id="74710-330">Created **linked services**:</span></span>

   <span data-ttu-id="74710-331">a.</span><span class="sxs-lookup"><span data-stu-id="74710-331">a.</span></span> <span data-ttu-id="74710-332">Um **armazenamento do Azure** vinculado serviço toolink sua conta de armazenamento do Azure que contém dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="74710-332">An **Azure Storage** linked service toolink your Azure storage account that holds input data.</span></span>     
   <span data-ttu-id="74710-333">b.</span><span class="sxs-lookup"><span data-stu-id="74710-333">b.</span></span> <span data-ttu-id="74710-334">Um **SQL Azure** vinculado serviço toolink banco de dados SQL que contém dados de saída de saudação.</span><span class="sxs-lookup"><span data-stu-id="74710-334">An **Azure SQL** linked service toolink your SQL database that holds hello output data.</span></span>
3. <span data-ttu-id="74710-335">Foram criados **conjuntos de dados** que descrevem os dados de entrada e de saída para os pipelines.</span><span class="sxs-lookup"><span data-stu-id="74710-335">Created **datasets** that describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="74710-336">Criado um **pipeline** com **atividade de cópia**, com **BlobSource** como origem hello e **SqlSink** como coletor hello.</span><span class="sxs-lookup"><span data-stu-id="74710-336">Created a **pipeline** with **Copy Activity**, with **BlobSource** as hello source and **SqlSink** as hello sink.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74710-337">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="74710-337">Next steps</span></span>
<span data-ttu-id="74710-338">Neste tutorial, você usou o armazenamento de blobs do Azure como um armazenamento de dados de origem e um banco de dados SQL do Azure como um armazenamento de dados de destino em uma operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="74710-338">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="74710-339">Olá tabela a seguir fornece uma lista de repositórios de dados com suporte como origens e destinos de atividade de cópia de saudação:</span><span class="sxs-lookup"><span data-stu-id="74710-339">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="74710-340">toolearn sobre como armazenam dados toocopy para/de uma data, clique o link Olá Olá repositório de dados na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="74710-340">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span> 

