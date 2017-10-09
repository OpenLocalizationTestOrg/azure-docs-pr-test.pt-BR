---
title: "aaaAzure integração da Stream Analytics e aprendizado de máquina | Microsoft Docs"
description: "Como toouse uma função definida pelo usuário e o aprendizado de máquina em um trabalho de análise de fluxo"
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: cfced01f-ccaa-4bc6-81e2-c03d1470a7a2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/06/2017
ms.author: jeffstok
ms.openlocfilehash: e1ba7ab51ece80719839793e1320a7666cfc4181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="performing-sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a><span data-ttu-id="d5ccc-103">Como realizar uma análise de sentimento usando o Azure Stream Analytics e o Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d5ccc-103">Performing sentiment analysis by using Azure Stream Analytics and Azure Machine Learning</span></span>
<span data-ttu-id="d5ccc-104">Este artigo descreve como definir tooquickly um trabalho do Stream Analytics do Azure simples que se integra ao aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-104">This article describes how tooquickly set up a simple Azure Stream Analytics job that integrates Azure Machine Learning.</span></span> <span data-ttu-id="d5ccc-105">Use um modelo de análise de sentimento de aprendizado de máquina do Olá dados de streaming texto Cortana Intelligence Galeria tooanalyze e determinar a pontuação de sensibilidade de saudação em tempo real.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-105">You use a Machine Learning sentiment analytics model from hello Cortana Intelligence Gallery tooanalyze streaming text data and determine hello sentiment score in real time.</span></span> <span data-ttu-id="d5ccc-106">Usar Olá Cortana Intelligence Suite permite realizar essa tarefa sem se preocupar com as complexidades de saudação da criação de um modelo de análise de sentimento.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-106">Using hello Cortana Intelligence Suite lets you accomplish this task without worrying about hello intricacies of building a sentiment analytics model.</span></span>

<span data-ttu-id="d5ccc-107">Você pode aplicar a você saber de tooscenarios este artigo como estes:</span><span class="sxs-lookup"><span data-stu-id="d5ccc-107">You can apply what you learn from this article tooscenarios such as these:</span></span>

* <span data-ttu-id="d5ccc-108">Analisar sentimento em tempo real no streaming de dados do Twitter.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-108">Analyzing real-time sentiment on streaming Twitter data.</span></span>
* <span data-ttu-id="d5ccc-109">Analisar registros de conversas do cliente com a equipe de suporte.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-109">Analyzing records of customer chats with support staff.</span></span>
* <span data-ttu-id="d5ccc-110">Avaliar comentários em fóruns, blogs e vídeos.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-110">Evaluating comments on forums, blogs, and videos.</span></span> 
* <span data-ttu-id="d5ccc-111">Muitos outros cenários de pontuação preditiva em tempo real.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-111">Many other real-time, predictive scoring scenarios.</span></span>

<span data-ttu-id="d5ccc-112">Em um cenário do mundo real, você obterá dados saudação diretamente a partir de um fluxo de dados do Twitter.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-112">In a real-world scenario, you would get hello data directly from a Twitter data stream.</span></span> <span data-ttu-id="d5ccc-113">tutorial de saudação toosimplify, escrevemos-lo para que hello trabalho de análise de fluxo contínuo obtém tweets de um arquivo CSV no armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-113">toosimplify hello tutorial, we've written it so that hello Streaming Analytics job gets tweets from a CSV file in Azure Blob storage.</span></span> <span data-ttu-id="d5ccc-114">Você pode criar seu próprio arquivo CSV, ou você pode usar um arquivo CSV de exemplo, conforme mostrado no Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="d5ccc-114">You can create your own CSV file, or you can use a sample CSV file, as shown in hello following image:</span></span>

![tweets de exemplo em um arquivo CSV](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

<span data-ttu-id="d5ccc-116">trabalho de análise de fluxo contínuo de saudação que você criar aplica modelo de análise de sentimento hello como uma função definida pelo usuário (UDF) em dados de texto de exemplo hello do repositório de blob hello.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-116">hello Streaming Analytics job that you create applies hello sentiment analytics model as a user-defined function (UDF) on hello sample text data from hello blob store.</span></span> <span data-ttu-id="d5ccc-117">saída de Hello (resultado Olá de análise de sentimento Olá) é gravada toohello mesmo repositório de blob em um arquivo CSV diferente.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-117">hello output (hello result of hello sentiment analysis) is written toohello same blob store in a different CSV file.</span></span> 

<span data-ttu-id="d5ccc-118">Olá figura a seguir demonstra essa configuração.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-118">hello following figure demonstrates this configuration.</span></span> <span data-ttu-id="d5ccc-119">Conforme observado, para um cenário mais realista, você pode substituir o armazenamento de blobs pelo streaming de dados do Twitter de uma entrada de Hubs de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-119">As noted, for a more realistic scenario, you can replace blob storage with streaming Twitter data from an Azure Event Hubs input.</span></span> <span data-ttu-id="d5ccc-120">Além disso, você pode criar um [Microsoft Power BI](https://powerbi.microsoft.com/) visualização em tempo real de sentimento agregação hello.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-120">Additionally, you could build a [Microsoft Power BI](https://powerbi.microsoft.com/) real-time visualization of hello aggregate sentiment.</span></span>    

![Visão geral de integração do Machine Learning do Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a><span data-ttu-id="d5ccc-122">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d5ccc-122">Prerequisites</span></span>
<span data-ttu-id="d5ccc-123">Antes de começar, verifique se que você tem o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="d5ccc-123">Before you start, make sure you have hello following:</span></span>

* <span data-ttu-id="d5ccc-124">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-124">An active Azure subscription.</span></span>
* <span data-ttu-id="d5ccc-125">Um arquivo CSV com alguns dados.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-125">A CSV file with some data in it.</span></span> <span data-ttu-id="d5ccc-126">Você pode baixar o arquivo hello mostrado anteriormente do [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), ou você pode criar seu próprio arquivo.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-126">You can download hello file shown earlier from [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), or you can create your own file.</span></span> <span data-ttu-id="d5ccc-127">Neste artigo, vamos supor que você está usando o arquivo de saudação do GitHub.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-127">For this article, we assume that you're using hello file from GitHub.</span></span>

<span data-ttu-id="d5ccc-128">Em um nível alto, tarefas de saudação do toocomplete demonstradas neste artigo, você Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="d5ccc-128">At a high level, toocomplete hello tasks demonstrated in this article, you do hello following:</span></span>

1. <span data-ttu-id="d5ccc-129">Criar uma conta de armazenamento do Azure e um contêiner de armazenamento de blob e carregar um contêiner de toohello do arquivo de entrada formato CSV.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-129">Create an Azure storage account and a blob storage container, and upload a CSV-formatted input file toohello container.</span></span>
3. <span data-ttu-id="d5ccc-130">Adicionar um modelo de análise de sentimento do espaço de trabalho do hello Cortana Intelligence Galeria tooyour aprendizado de máquina do Azure e implantar este modelo como um serviço web no espaço de trabalho de aprendizado de máquina hello.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-130">Add a sentiment analytics model from hello Cortana Intelligence Gallery tooyour Azure Machine Learning workspace and deploy this model as a web service in hello Machine Learning workspace.</span></span>
5. <span data-ttu-id="d5ccc-131">Crie um trabalho do Stream Analytics que chama esse serviço da web como uma função no sentimento de toodetermine ordem para entrada de texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-131">Create a Stream Analytics job that calls this web service as a function in order toodetermine sentiment for hello text input.</span></span>
6. <span data-ttu-id="d5ccc-132">Iniciar o trabalho de análise de fluxo de saudação e verifique a saída de hello.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-132">Start hello Stream Analytics job and check hello output.</span></span>

## <a name="create-a-storage-container-and-upload-hello-csv-input-file"></a><span data-ttu-id="d5ccc-133">Criar um contêiner de armazenamento e carregar o arquivo de entrada hello CSV</span><span class="sxs-lookup"><span data-stu-id="d5ccc-133">Create a storage container and upload hello CSV input file</span></span>
<span data-ttu-id="d5ccc-134">Nesta etapa, você pode usar qualquer arquivo CSV, como Olá disponível do GitHub.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-134">For this step, you can use any CSV file, such as hello one available from GitHub.</span></span>

1. <span data-ttu-id="d5ccc-135">No portal do Azure de Olá, clique em **novo** &gt; **armazenamento** &gt; **conta de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-135">In hello Azure portal, click **New** &gt; **Storage** &gt; **Storage account**.</span></span>

   ![criar nova conta de armazenamento](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-create-storage-account.png)

2. <span data-ttu-id="d5ccc-137">Forneça um nome (`samldemo` no exemplo hello).</span><span class="sxs-lookup"><span data-stu-id="d5ccc-137">Provide a name (`samldemo` in hello example).</span></span> <span data-ttu-id="d5ccc-138">nome de saudação pode usar apenas letras minúsculas e números e deve ser exclusivo no Azure.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-138">hello name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 

3. <span data-ttu-id="d5ccc-139">Especifique um grupo de recursos existente e um local.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-139">Specify an existing resource group and specify a location.</span></span> <span data-ttu-id="d5ccc-140">Para o local, é recomendável que todos os recursos de saudação criados neste tutorial usam Olá mesmo local.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-140">For location, we recommend that all hello resources created in this tutorial use hello same location.</span></span>

    ![informe os detalhes da conta de armazenamento](./media/stream-analytics-machine-learning-integration-tutorial/create-sa1.png)

4. <span data-ttu-id="d5ccc-142">No portal do Azure de Olá, selecione a conta de armazenamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-142">In hello Azure portal, select hello storage account.</span></span> <span data-ttu-id="d5ccc-143">Na folha de conta de armazenamento hello, clique em **contêineres** e, em seguida, clique em  **+ &nbsp;contêiner** toocreate o armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-143">In hello storage account blade, click **Containers** and then click **+&nbsp;Container** toocreate blob storage.</span></span>

    ![criar contêiner de blobs](./media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

5. <span data-ttu-id="d5ccc-145">Forneça um nome para o contêiner de saudação (`azuresamldemoblob` no exemplo hello) e verifique **tipo de acesso** está definido muito**Blob**.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-145">Provide a name for hello container (`azuresamldemoblob` in hello example) and verify that **Access type** is set too**Blob**.</span></span> <span data-ttu-id="d5ccc-146">Quando terminar, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-146">When you're done, click **OK**.</span></span>

    ![especifique os detalhes do contêiner de blob](./media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

6. <span data-ttu-id="d5ccc-148">Em Olá **contêineres** folha, selecione Olá novo contêiner, que abre a folha de saudação para o contêiner.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-148">In hello **Containers** blade, select hello new container, which opens hello blade for that container.</span></span>

7. <span data-ttu-id="d5ccc-149">Clique em **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-149">Click **Upload**.</span></span>

    ![Botão “Carregar” para um contêiner](./media/stream-analytics-machine-learning-integration-tutorial/create-sa-upload-button.png)

8. <span data-ttu-id="d5ccc-151">Em Olá **carregar blob** folha, especifique o arquivo CSV de saudação que você deseja toouse para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-151">In hello **Upload blob** blade, specify hello CSV file that you want toouse for this tutorial.</span></span> <span data-ttu-id="d5ccc-152">Para **tipo de Blob**, selecione **blob de blocos** e blocos de saudação do conjunto de tamanho too4 MB, que é suficiente para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-152">For **Blob type**, select **Block blob** and set hello block size too4 MB, which is sufficient for this tutorial.</span></span>

    ![carregar arquivo de blob](./media/stream-analytics-machine-learning-integration-tutorial/create-sa4.png)

9. <span data-ttu-id="d5ccc-154">Clique em Olá **carregar** botão na parte inferior da saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-154">Click hello **Upload** button at hello bottom of hello blade.</span></span>

## <a name="add-hello-sentiment-analytics-model-from-hello-cortana-intelligence-gallery"></a><span data-ttu-id="d5ccc-155">Adicionar modelo de análise de sentimento de saudação do hello Cortana Intelligence Galeria</span><span class="sxs-lookup"><span data-stu-id="d5ccc-155">Add hello sentiment analytics model from hello Cortana Intelligence Gallery</span></span>

<span data-ttu-id="d5ccc-156">Agora que os dados de exemplo hello estão em um blob, você pode habilitar o modelo de análise de sentimento Olá na Galeria de inteligência do Cortana.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-156">Now that hello sample data is in a blob, you can enable hello sentiment analysis model in Cortana Intelligence Gallery.</span></span>

1. <span data-ttu-id="d5ccc-157">Vá toohello [modelo de análise preditiva sentimento](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) página Olá Cortana Intelligence Galeria.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-157">Go toohello [predictive sentiment analytics model](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) page in hello Cortana Intelligence Gallery.</span></span>  

2. <span data-ttu-id="d5ccc-158">Clique em **Abrir no Studio**.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-158">Click **Open in Studio**.</span></span>  
   
   ![Machine Learning do Stream Analytics, abrir o Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. <span data-ttu-id="d5ccc-160">Entrar no espaço de trabalho do toogo toohello.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-160">Sign in toogo toohello workspace.</span></span> <span data-ttu-id="d5ccc-161">Selecione um local.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-161">Select a location.</span></span>

4. <span data-ttu-id="d5ccc-162">Clique em **executar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-162">Click **Run** at hello bottom of hello page.</span></span> <span data-ttu-id="d5ccc-163">processo de saudação é executado, que leva cerca de um minuto.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-163">hello process runs, which takes about a minute.</span></span>

   ![executar experimento no Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-run-experiment.png)  

5. <span data-ttu-id="d5ccc-165">Depois que o processo de saudação foi executada com êxito, selecione **implantar o serviço da Web** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-165">After hello process has run successfully, select **Deploy Web Service** at hello bottom of hello page.</span></span>

   ![implantar experimento no Machine Learning Studio como um serviço Web](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-deploy-web-service.png)  

6. <span data-ttu-id="d5ccc-167">toovalidate que Olá sentimento modelo de análise é toouse pronto, clique em Olá **teste** botão.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-167">toovalidate that hello sentiment analytics model is ready toouse, click hello **Test** button.</span></span> <span data-ttu-id="d5ccc-168">Forneça entrada de texto, como "Eu amo a Microsoft".</span><span class="sxs-lookup"><span data-stu-id="d5ccc-168">Provide text input such as "I love Microsoft".</span></span> 

   ![testar experimento no Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test.png)  

    <span data-ttu-id="d5ccc-170">Se o teste Olá funciona, você verá um toohello semelhante resultado exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="d5ccc-170">If hello test works, you see a result similar toohello following example:</span></span>

   ![testar os resultados no Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test-results.png)  

7. <span data-ttu-id="d5ccc-172">Em Olá **aplicativos** coluna, clique em Olá **Excel 2010 ou pasta de trabalho anterior** toodownload link uma pasta de trabalho do Excel.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-172">In hello **Apps** column, click hello **Excel 2010 or earlier workbook** link toodownload an Excel workbook.</span></span> <span data-ttu-id="d5ccc-173">pasta de trabalho Olá contém a chave de uma API de saudação e Olá URL que você precisa posterior tooset Olá análise de fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-173">hello workbook contains hello an API key and hello URL that you need later tooset up hello Stream Analytics job.</span></span>

    ![Machine Learning do Stream Analytics, visão rápida](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  


## <a name="create-a-stream-analytics-job-that-uses-hello-machine-learning-model"></a><span data-ttu-id="d5ccc-175">Criar um trabalho do Stream Analytics que usa o modelo de aprendizado de máquina Olá</span><span class="sxs-lookup"><span data-stu-id="d5ccc-175">Create a Stream Analytics job that uses hello Machine Learning model</span></span>

<span data-ttu-id="d5ccc-176">Agora você pode criar um trabalho do Stream Analytics que lê Olá exemplo tweets de arquivo CSV de saudação no armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-176">You can now create a Stream Analytics job that reads hello sample tweets from hello CSV file in blob storage.</span></span> 

### <a name="create-hello-job"></a><span data-ttu-id="d5ccc-177">Criar trabalho de saudação</span><span class="sxs-lookup"><span data-stu-id="d5ccc-177">Create hello job</span></span>

1. <span data-ttu-id="d5ccc-178">Vá toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d5ccc-178">Go toohello [Azure portal](https://portal.azure.com).</span></span>  

2. <span data-ttu-id="d5ccc-179">Clique em **Novo** > **Internet das Coisas** > **Trabalho do Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-179">Click **New** > **Internet of Things** > **Stream Analytics job**.</span></span> 

   ![Caminho do portal do Azure para obter um novo trabalho de análise de fluxo tooa](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-new-iot-sa-job.png)
   
3. <span data-ttu-id="d5ccc-181">Nome do trabalho Olá `azure-sa-ml-demo`, especifique uma assinatura, especifique um grupo de recursos existente ou crie um novo e selecione Olá local para o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-181">Name hello job `azure-sa-ml-demo`, specify a subscription, specify an existing resource group or create a new one, and select hello location for hello job.</span></span>

   ![especifique as configurações para o novo trabalho do Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   

### <a name="configure-hello-job-input"></a><span data-ttu-id="d5ccc-183">Configurar entrada de trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="d5ccc-183">Configure hello job input</span></span>
<span data-ttu-id="d5ccc-184">trabalho de saudação obtém sua entrada de arquivo CSV de saudação que você carregou o armazenamento de tooblob anterior.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-184">hello job gets its input from hello CSV file that you uploaded earlier tooblob storage.</span></span>

1. <span data-ttu-id="d5ccc-185">Depois que o trabalho Olá foi criado, em **trabalho topologia** na folha de trabalho hello, clique em hello **entradas** caixa.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-185">After hello job has been created, under **Job Topology** in hello job blade, click hello **Inputs** box.</span></span>  
   
   ![Caixa “Entradas” na folha do trabalho do Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input.png)  

2. <span data-ttu-id="d5ccc-187">Em Olá **entradas** folha, clique em **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-187">In hello **Inputs** blade, click **+ Add**.</span></span>

   ![Botão para adicionar um trabalho de análise de fluxo de entrada toohello 'add'](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input-button.png)  

3. <span data-ttu-id="d5ccc-189">Preencha Olá **nova entrada** folha com estes valores:</span><span class="sxs-lookup"><span data-stu-id="d5ccc-189">Fill out hello **New input** blade with these values:</span></span>

    * <span data-ttu-id="d5ccc-190">**Alias de entrada**: Use o nome de saudação `datainput`.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-190">**Input alias**: Use hello name `datainput`.</span></span>
    * <span data-ttu-id="d5ccc-191">**Tipo de Origem**: Selecione **Fluxo de Dados**.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-191">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="d5ccc-192">**Fontes**: selecione **Armazenamento de blobs**.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-192">**Source**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="d5ccc-193">**Opção de importação**: selecione **Usar armazenamento de blobs da assinatura atual**.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-193">**Import option**: Select **Use blob storage from current subscription**.</span></span> 
    * <span data-ttu-id="d5ccc-194">**Conta de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-194">**Storage account**.</span></span> <span data-ttu-id="d5ccc-195">Selecione a conta de armazenamento de saudação criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-195">Select hello storage account you created earlier.</span></span>
    * <span data-ttu-id="d5ccc-196">**Contêiner**.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-196">**Container**.</span></span> <span data-ttu-id="d5ccc-197">Contêiner de saudação selecione criado anteriormente (`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="d5ccc-197">Select hello container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="d5ccc-198">**Formato de serialização do evento**.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-198">**Event serialization format**.</span></span> <span data-ttu-id="d5ccc-199">Selecione **CSV**.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-199">Select **CSV**.</span></span>

    ![Configurações para a nova entrada de trabalho](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-create-sa-input-new-portal.png)

4. <span data-ttu-id="d5ccc-201">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-201">Click **Create**.</span></span>

### <a name="configure-hello-job-output"></a><span data-ttu-id="d5ccc-202">Configurar saída de trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="d5ccc-202">Configure hello job output</span></span>
<span data-ttu-id="d5ccc-203">Olá trabalho envia resultados toohello mesmo onde ele obtém a entrada de armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-203">hello job sends results toohello same blob storage where it gets input.</span></span> 

1. <span data-ttu-id="d5ccc-204">Em **trabalho topologia** na folha de trabalho hello, clique em Olá **saídas** caixa.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-204">Under **Job Topology** in hello job blade, click hello **Outputs** box.</span></span>  
  
   ![Criar nova saída para o trabalho do Streaming Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-output.png)  

2. <span data-ttu-id="d5ccc-206">Em Olá **saídas** folha, clique em **+ adicionar**e, em seguida, adicione uma saída com alias Olá `datamloutput`.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-206">In hello **Outputs** blade, click **+ Add**, and then add an output with hello alias `datamloutput`.</span></span> 

3. <span data-ttu-id="d5ccc-207">Para **Coletor**, selecione **Armazenamento de blobs**.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-207">For **Sink**, select **Blob storage**.</span></span> <span data-ttu-id="d5ccc-208">Em seguida, preencha restante Olá Olá saída configurações usando Olá mesmos valores que você usou para o armazenamento de blob Olá para entrada:</span><span class="sxs-lookup"><span data-stu-id="d5ccc-208">Then fill in hello rest of hello output settings using hello same values that you used for hello blob storage for input:</span></span>

    * <span data-ttu-id="d5ccc-209">**Conta de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-209">**Storage account**.</span></span> <span data-ttu-id="d5ccc-210">Selecione a conta de armazenamento de saudação criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-210">Select hello storage account you created earlier.</span></span>
    * <span data-ttu-id="d5ccc-211">**Contêiner**.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-211">**Container**.</span></span> <span data-ttu-id="d5ccc-212">Contêiner de saudação selecione criado anteriormente (`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="d5ccc-212">Select hello container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="d5ccc-213">**Formato de serialização do evento**.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-213">**Event serialization format**.</span></span> <span data-ttu-id="d5ccc-214">Selecione **CSV**.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-214">Select **CSV**.</span></span>

   ![Configurações para a nova saída de trabalho](./media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

4. <span data-ttu-id="d5ccc-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-216">Click **Create**.</span></span>   


### <a name="add-hello-machine-learning-function"></a><span data-ttu-id="d5ccc-217">Adicionar função de aprendizado de máquina hello</span><span class="sxs-lookup"><span data-stu-id="d5ccc-217">Add hello Machine Learning function</span></span> 
<span data-ttu-id="d5ccc-218">Anteriormente, você publicou um serviço web de tooa de modelo de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-218">Earlier you published a Machine Learning model tooa web service.</span></span> <span data-ttu-id="d5ccc-219">Em nosso cenário, quando o trabalho de análise de fluxo de saudação é executado, ele envia tweet cada exemplo do serviço de web de entrada toohello Olá para análise de sentimento.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-219">In our scenario, when hello Stream Analysis job runs, it sends each sample tweet from hello input toohello web service for sentiment analysis.</span></span> <span data-ttu-id="d5ccc-220">Olá serviço web de aprendizado de máquina retorna um sentimento (`positive`, `neutral`, ou `negative`) e a probabilidade de tweet Olá sendo positivo.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-220">hello Machine Learning web service returns a sentiment (`positive`, `neutral`, or `negative`) and a probability of hello tweet being positive.</span></span> 

<span data-ttu-id="d5ccc-221">Nesta seção do tutorial hello, você deve definir uma função no trabalho de análise de fluxo de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-221">In this section of hello tutorial, you define a function in hello Stream Analysis job.</span></span> <span data-ttu-id="d5ccc-222">função Hello pode ser invocado toosend um serviço de web toohello tweet e voltar a resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-222">hello function can be invoked toosend a tweet toohello web service and get hello response back.</span></span> 

1. <span data-ttu-id="d5ccc-223">Certifique-se de que ter Olá URL e a API de chave de serviço web que você baixou anteriormente na pasta de trabalho do Excel hello.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-223">Make sure you have hello web service URL and API key that you downloaded earlier in hello Excel workbook.</span></span>

2. <span data-ttu-id="d5ccc-224">Folha de visão geral do trabalho de retorno toohello.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-224">Return toohello job overview blade.</span></span>

3. <span data-ttu-id="d5ccc-225">Em **Configurações**, selecione **Funções** e, em seguida, clique em **+ Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-225">Under **Settings**, select **Functions** and then click **+ Add**.</span></span>

   ![Adicionar um trabalho de análise de fluxo de toohello de função](./media/stream-analytics-machine-learning-integration-tutorial/create-function1.png) 

4. <span data-ttu-id="d5ccc-227">Digite `sentiment` como Olá função alias e preencha o restante de saudação da folha de saudação usando esses valores:</span><span class="sxs-lookup"><span data-stu-id="d5ccc-227">Enter `sentiment` as hello function alias and fill out hello rest of hello blade using these values:</span></span>

    * <span data-ttu-id="d5ccc-228">**Tipo de função**: selecione **Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-228">**Function type**: Select **Azure ML**.</span></span>
    * <span data-ttu-id="d5ccc-229">**Opção de importação**: selecione **Importar de outra assinatura**.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-229">**Import option**: Select **Import from a different subscription**.</span></span> <span data-ttu-id="d5ccc-230">Isso fornece uma oportunidade tooenter Olá URL e a chave.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-230">This gives you a chance tooenter hello URL and key.</span></span>
    * <span data-ttu-id="d5ccc-231">**URL**: colar na URL do serviço web hello.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-231">**URL**: Paste in hello web service URL.</span></span>
    * <span data-ttu-id="d5ccc-232">**Chave**: colar na chave de API de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-232">**Key**: Paste in hello API key.</span></span>
  
    ![Configurações para a adição de um trabalho de análise de fluxo de toohello de função de aprendizado de máquina](./media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  
    
5. <span data-ttu-id="d5ccc-234">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-234">Click **Create**.</span></span>

### <a name="create-a-query-tootransform-hello-data"></a><span data-ttu-id="d5ccc-235">Criar uma consulta tootransform Olá de dados</span><span class="sxs-lookup"><span data-stu-id="d5ccc-235">Create a query tootransform hello data</span></span>

<span data-ttu-id="d5ccc-236">Análise de fluxo usa uma entrada de saudação tooexamine consulta declarativa baseado em SQL e processá-la.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-236">Stream Analytics uses a declarative, SQL-based query tooexamine hello input and process it.</span></span> <span data-ttu-id="d5ccc-237">Nesta seção, você deve criar uma consulta que lê cada tweet de entrada e, em seguida, invoca a análise de sentimento Olá aprendizado de máquina função tooperform.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-237">In this section, you create a query that reads each tweet from input and then invokes hello Machine Learning function tooperform sentiment analysis.</span></span> <span data-ttu-id="d5ccc-238">consulta de saudação envia Olá toohello de resultados de saída que você definiu (armazenamento de blob).</span><span class="sxs-lookup"><span data-stu-id="d5ccc-238">hello query then sends hello result toohello output that you defined (blob storage).</span></span>

1. <span data-ttu-id="d5ccc-239">Folha de visão geral do trabalho de retorno toohello.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-239">Return toohello job overview blade.</span></span>

2.  <span data-ttu-id="d5ccc-240">Em **trabalho topologia**, clique em Olá **consulta** caixa.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-240">Under **Job Topology**, click hello **Query** box.</span></span>

    ![Criar uma consulta para o trabalho de Análise de Streaming](./media/stream-analytics-machine-learning-integration-tutorial/create-query.png)  

3. <span data-ttu-id="d5ccc-242">Digite hello consulta a seguir:</span><span class="sxs-lookup"><span data-stu-id="d5ccc-242">Enter hello following query:</span></span>

    ```
    WITH sentiment AS (  
    SELECT text, sentiment(text) as result from datainput  
    )  

    Select text, result.[Score]  
    Into datamloutput
    From sentiment  
    ```    

    <span data-ttu-id="d5ccc-243">consulta Olá invoca a função de saudação criado anteriormente (`sentiment`) na análise de sentimento ordem tooperform em cada tweet na entrada hello.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-243">hello query invokes hello function you created earlier (`sentiment`) in order tooperform sentiment analysis on each tweet in hello input.</span></span> 

4. <span data-ttu-id="d5ccc-244">Clique em **salvar** toosave consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-244">Click **Save** toosave hello query.</span></span>


## <a name="start-hello-stream-analytics-job-and-check-hello-output"></a><span data-ttu-id="d5ccc-245">Iniciar o trabalho de análise de fluxo de saudação e verifique a saída de hello</span><span class="sxs-lookup"><span data-stu-id="d5ccc-245">Start hello Stream Analytics job and check hello output</span></span>

<span data-ttu-id="d5ccc-246">Agora você pode iniciar o trabalho de análise de fluxo de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-246">You can now start hello Stream Analytics job.</span></span>

### <a name="start-hello-job"></a><span data-ttu-id="d5ccc-247">Iniciar trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="d5ccc-247">Start hello job</span></span>
1. <span data-ttu-id="d5ccc-248">Folha de visão geral do trabalho de retorno toohello.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-248">Return toohello job overview blade.</span></span>

2. <span data-ttu-id="d5ccc-249">Clique em **iniciar** na parte superior de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-249">Click **Start** at hello top of hello blade.</span></span>

    ![Criar uma consulta para o trabalho de Análise de Streaming](./media/stream-analytics-machine-learning-integration-tutorial/start-job.png)  

3. <span data-ttu-id="d5ccc-251">Em Olá **Iniciar trabalho**, selecione **personalizado**e, em seguida, selecione um dia toowhen anterior que você carregou o armazenamento de tooblob de arquivos CSV hello.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-251">In hello **Start job**, select **Custom**, and then select one day prior toowhen you uploaded hello CSV file tooblob storage.</span></span> <span data-ttu-id="d5ccc-252">Quando terminar, clique em **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-252">When you're done, click **Start**.</span></span>  


### <a name="check-hello-output"></a><span data-ttu-id="d5ccc-253">Verifique a saída de hello</span><span class="sxs-lookup"><span data-stu-id="d5ccc-253">Check hello output</span></span>
1. <span data-ttu-id="d5ccc-254">Trabalho Olá permitem executar alguns minutos até que você veja a atividade no hello **monitoramento** caixa.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-254">Let hello job run for a few minutes until you see activity in hello **Monitoring** box.</span></span> 

2. <span data-ttu-id="d5ccc-255">Se você tiver uma ferramenta que você normalmente usa tooexamine conteúdo de saudação do armazenamento de blob, use esse Olá de tooexamine ferramenta `azuresamldemoblob` contêiner.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-255">If you have a tool that you normally use tooexamine hello contents of blob storage, use that tool tooexamine hello `azuresamldemoblob` container.</span></span> <span data-ttu-id="d5ccc-256">Como alternativa, Olá etapas Olá portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="d5ccc-256">Alternatively, do hello following steps in hello Azure portal:</span></span>

    1. <span data-ttu-id="d5ccc-257">No portal de hello, localize Olá `samldemo` armazenamento de conta e na conta hello, localize Olá `azuresamldemoblob` contêiner.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-257">In hello portal, find hello `samldemo` storage account, and within hello account, find hello `azuresamldemoblob` container.</span></span> <span data-ttu-id="d5ccc-258">Você ver dois arquivos no contêiner Olá: Olá arquivo que contém a saudação tweets de exemplo e um arquivo CSV gerado pelo trabalho de análise de fluxo de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-258">You see two files in hello container: hello file that contains hello sample tweets and a CSV file generated by hello Stream Analytics job.</span></span>
    2. <span data-ttu-id="d5ccc-259">Arquivo hello gerado e, em seguida, selecione **baixar**.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-259">Right-click hello generated file and then select **Download**.</span></span> 

   ![Baixar a saída do trabalho CSV do armazenamento de blobs](./media/stream-analytics-machine-learning-integration-tutorial/download-output-csv-file.png)  

3. <span data-ttu-id="d5ccc-261">Abra Olá gerado arquivo CSV.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-261">Open hello generated CSV file.</span></span> <span data-ttu-id="d5ccc-262">Você verá algo parecido com hello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="d5ccc-262">You see something like hello following example:</span></span>  
   
   ![Machine Learning do Stream Analytics, exibição de CSV](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  


### <a name="view-metrics"></a><span data-ttu-id="d5ccc-264">Métricas de exibição</span><span class="sxs-lookup"><span data-stu-id="d5ccc-264">View metrics</span></span>
<span data-ttu-id="d5ccc-265">Você também pode exibir as métricas relacionadas à função de Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-265">You also can view Azure Machine Learning function-related metrics.</span></span> <span data-ttu-id="d5ccc-266">Olá métricas relacionadas à função a seguir é exibido no hello **monitoramento** caixa na folha de trabalho hello:</span><span class="sxs-lookup"><span data-stu-id="d5ccc-266">hello following function-related metrics are displayed in hello **Monitoring** box in hello job blade:</span></span>

* <span data-ttu-id="d5ccc-267">**Função solicitações** indica o número de saudação de solicitações enviadas tooa serviço web de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-267">**Function Requests** indicates hello number of requests sent tooa Machine Learning web service.</span></span>  
* <span data-ttu-id="d5ccc-268">**Função eventos** indica Olá número de eventos na solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-268">**Function Events** indicates hello number of events in hello request.</span></span> <span data-ttu-id="d5ccc-269">Por padrão, cada serviço web de aprendizado de máquina do tooa de solicitação contém too1, 000 eventos de backup.</span><span class="sxs-lookup"><span data-stu-id="d5ccc-269">By default, each request tooa Machine Learning web service contains up too1,000 events.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="d5ccc-270">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d5ccc-270">Next steps</span></span>

* [<span data-ttu-id="d5ccc-271">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d5ccc-271">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="d5ccc-272">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="d5ccc-272">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="d5ccc-273">Integrar API REST e Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d5ccc-273">Integrate REST API and Machine Learning</span></span>](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)
* [<span data-ttu-id="d5ccc-274">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d5ccc-274">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)



