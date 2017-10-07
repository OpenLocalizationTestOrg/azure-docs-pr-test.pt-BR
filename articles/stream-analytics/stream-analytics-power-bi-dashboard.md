---
title: Painel de BI aaaPower no Azure Stream Analytics | Microsoft Docs
description: Use um em tempo real streaming Power BI painel toogather de business intelligence e analisar dados de alto volume de um trabalho do Stream Analytics.
keywords: "painel de análise, painel em tempo real"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: fe8db732-4397-4e58-9313-fec9537aa2ad
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: jeffstok
ms.openlocfilehash: cb9127576230e9d327b437b674f31cc23869bfff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-and-power-bi-a-real-time-analytics-dashboard-for-streaming-data"></a><span data-ttu-id="9850d-104">Stream Analytics e Power BI: um painel de análise em tempo real para dados de streaming</span><span class="sxs-lookup"><span data-stu-id="9850d-104">Stream Analytics and Power BI: A real-time analytics dashboard for streaming data</span></span>
<span data-ttu-id="9850d-105">Análise de fluxo do Azure permite que você tootake aproveitar uma saudação principais ferramentas de business intelligence, [Microsoft Power BI](https://powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="9850d-105">Azure Stream Analytics enables you tootake advantage of one of hello leading business intelligence tools, [Microsoft Power BI](https://powerbi.com/).</span></span> <span data-ttu-id="9850d-106">Neste artigo, você saberá como criar ferramentas de business intelligence usando o Power BI como uma saída de seus trabalhos do Stream Analytics do Azure.</span><span class="sxs-lookup"><span data-stu-id="9850d-106">In this article, you learn how create business intelligence tools by using Power BI as an output for your Azure Stream Analytics jobs.</span></span> <span data-ttu-id="9850d-107">Você também aprenderá como toocreate e use um dashboard em tempo real.</span><span class="sxs-lookup"><span data-stu-id="9850d-107">You also learn how toocreate and use a real-time dashboard.</span></span>

<span data-ttu-id="9850d-108">Este artigo dá continuidade de saudação do Stream Analytics [detecção de fraudes em tempo real](stream-analytics-real-time-fraud-detection.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="9850d-108">This article continues from hello Stream Analytics [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="9850d-109">Ele se baseia no fluxo de trabalho de saudação criado neste tutorial e adiciona um Power BI para que você pode visualizar fraudulentas chamadas telefônicas que são detectadas por um trabalho de análise de fluxo de saída.</span><span class="sxs-lookup"><span data-stu-id="9850d-109">It builds on hello workflow created in that tutorial and adds a Power BI output so that you can visualize fraudulent phone calls that are detected by a Streaming Analytics job.</span></span> 

<span data-ttu-id="9850d-110">Você pode assistir a [um vídeo](https://www.youtube.com/watch?v=SGUpT-a99MA) que ilustra esse cenário.</span><span class="sxs-lookup"><span data-stu-id="9850d-110">You can watch [a video](https://www.youtube.com/watch?v=SGUpT-a99MA)  that illustrates this scenario.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="9850d-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9850d-111">Prerequisites</span></span>

<span data-ttu-id="9850d-112">Antes de começar, verifique se que você tem o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="9850d-112">Before you start, make sure you have hello following:</span></span>

* <span data-ttu-id="9850d-113">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="9850d-113">An Azure account.</span></span>
* <span data-ttu-id="9850d-114">Uma conta para o Power BI.</span><span class="sxs-lookup"><span data-stu-id="9850d-114">An account for Power BI.</span></span> <span data-ttu-id="9850d-115">Você pode usar uma conta corporativa ou de estudante.</span><span class="sxs-lookup"><span data-stu-id="9850d-115">You can use a work account or a school account.</span></span>
* <span data-ttu-id="9850d-116">Uma versão completa do hello [detecção de fraudes em tempo real](stream-analytics-real-time-fraud-detection.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="9850d-116">A completed version of hello [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="9850d-117">tutorial de saudação inclui um aplicativo que gera metadados fictícios de chamada telefônica.</span><span class="sxs-lookup"><span data-stu-id="9850d-117">hello tutorial includes an app that generates fictitious telephone-call metadata.</span></span> <span data-ttu-id="9850d-118">Tutorial Olá, crie um hub de eventos e enviar Olá streaming hub de eventos de toohello de dados de chamada telefônica.</span><span class="sxs-lookup"><span data-stu-id="9850d-118">In hello tutorial, you create an event hub and send hello streaming phone call data toohello event hub.</span></span> <span data-ttu-id="9850d-119">Você escrever uma consulta que detecta chamadas fraudulentas (chamadas de saudação mesmo número no Olá a mesma hora em diferentes locais).</span><span class="sxs-lookup"><span data-stu-id="9850d-119">You write a query that detects fraudulent calls (calls from hello same number at hello same time in different locations).</span></span> 


## <a name="add-power-bi-output"></a><span data-ttu-id="9850d-120">Adicionar saída do Power BI</span><span class="sxs-lookup"><span data-stu-id="9850d-120">Add Power BI output</span></span>
<span data-ttu-id="9850d-121">Tutorial de detecção de fraudes em tempo real de hello, saída de saudação é enviada tooAzure armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="9850d-121">In hello real-time fraud detection tutorial, hello output is sent tooAzure Blob storage.</span></span> <span data-ttu-id="9850d-122">Nesta seção, você deve adicionar uma saída que envia informações tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="9850d-122">In this section, you add an output that sends information tooPower BI.</span></span>

1. <span data-ttu-id="9850d-123">Olá portal do Azure, abra o trabalho de análise de fluxo contínuo de saudação que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9850d-123">In hello Azure portal, open hello Streaming Analytics job that you created earlier.</span></span> <span data-ttu-id="9850d-124">Se você usou o nome sugerido hello, Olá trabalho é chamado de `sa_frauddetection_job_demo`.</span><span class="sxs-lookup"><span data-stu-id="9850d-124">If you used hello suggested name, hello job is named `sa_frauddetection_job_demo`.</span></span>

2. <span data-ttu-id="9850d-125">Selecione Olá **saídas** caixa no meio de saudação do painel de trabalho hello e, em seguida, selecione **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9850d-125">Select hello **Outputs** box in hello middle of hello job dashboard and then select **+ Add**.</span></span>

3. <span data-ttu-id="9850d-126">Para **Alias de Saída**, digite `CallStream-PowerBI`.</span><span class="sxs-lookup"><span data-stu-id="9850d-126">For **Output Alias**, enter `CallStream-PowerBI`.</span></span> <span data-ttu-id="9850d-127">Você pode usar um nome diferente.</span><span class="sxs-lookup"><span data-stu-id="9850d-127">You can use a different name.</span></span> <span data-ttu-id="9850d-128">Se você fizer isso, anote-lo, porque você precisa de nome hello mais tarde.</span><span class="sxs-lookup"><span data-stu-id="9850d-128">If you do, make a note of it, because you need hello name later.</span></span> 

4. <span data-ttu-id="9850d-129">Em **Coletor**, selecione **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="9850d-129">Under **Sink**, select **Power BI**.</span></span>

   ![Criar uma saída para o Power BI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut.png)

5. <span data-ttu-id="9850d-131">Clique em **Autorizar**.</span><span class="sxs-lookup"><span data-stu-id="9850d-131">Click **Authorize**.</span></span>

    <span data-ttu-id="9850d-132">É aberta uma janela em que você pode fornecer suas credenciais do Azure para uma conta corporativa ou de estudante.</span><span class="sxs-lookup"><span data-stu-id="9850d-132">A window opens where you can provide your Azure credentials for a work or school account.</span></span> 

    ![Insira as credenciais para acesso tooPower BI](./media/stream-analytics-power-bi-dashboard/authorize-area.png)

6. <span data-ttu-id="9850d-134">Insira suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="9850d-134">Enter your credentials.</span></span> <span data-ttu-id="9850d-135">Lembre-se, em seguida, quando você inserir suas credenciais, você está também concedendo permissão toohello análise de fluxo de trabalho tooaccess sua área de Power BI.</span><span class="sxs-lookup"><span data-stu-id="9850d-135">Be aware then when you enter your credentials, you're also giving permission toohello Streaming Analytics job tooaccess your Power BI area.</span></span>

7. <span data-ttu-id="9850d-136">Quando você retornar toohello **nova saída** folha, digite Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="9850d-136">When you're returned toohello **New output** blade, enter hello following information:</span></span>

    * <span data-ttu-id="9850d-137">**Espaço de trabalho de grupo**: selecione um espaço de trabalho em seu locatário do Power BI em que você deseja toocreate Olá dataset.</span><span class="sxs-lookup"><span data-stu-id="9850d-137">**Group Workspace**: Select a workspace in your Power BI tenant where you want toocreate hello dataset.</span></span>
    * <span data-ttu-id="9850d-138">**Nome do Conjunto de Dados**: insira `sa-dataset`.</span><span class="sxs-lookup"><span data-stu-id="9850d-138">**Dataset Name**:  Enter `sa-dataset`.</span></span> <span data-ttu-id="9850d-139">Você pode usar um nome diferente.</span><span class="sxs-lookup"><span data-stu-id="9850d-139">You can use a different name.</span></span> <span data-ttu-id="9850d-140">Se você fizer isso, anote-o para mais tarde.</span><span class="sxs-lookup"><span data-stu-id="9850d-140">If you do, make a note of it for later.</span></span>
    * <span data-ttu-id="9850d-141">**Nome da Tabela**: insira `fraudulent-calls`.</span><span class="sxs-lookup"><span data-stu-id="9850d-141">**Table Name**: Enter `fraudulent-calls`.</span></span> <span data-ttu-id="9850d-142">Atualmente, a saída do Power BI de trabalhos do Stream Analytics só podem ter uma tabela em um conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="9850d-142">Currently, Power BI output from Stream Analytics jobs can have only one table in a dataset.</span></span>

    ![Espaço de trabalho de PBI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut-with-dataset-table.png)

    > [!WARNING]
    > <span data-ttu-id="9850d-144">Se o Power BI tem um conjunto de dados e tabela Olá mesmos nomes de saudação aquelas que você especificar no trabalho do Stream Analytics hello, Olá existentes é substituído.</span><span class="sxs-lookup"><span data-stu-id="9850d-144">If Power BI has a dataset and table that have hello same names as hello ones that you specify in hello Stream Analytics job, hello existing ones are overwritten.</span></span>
    > <span data-ttu-id="9850d-145">Recomendamos que você não crie explicitamente esse conjunto de dados e a tabela em sua conta do Power BI.</span><span class="sxs-lookup"><span data-stu-id="9850d-145">We recommend that you do not explicitly create this dataset and table in your Power BI account.</span></span> <span data-ttu-id="9850d-146">Eles são criados automaticamente quando você iniciar o trabalho do Stream Analytics e Olá inicia bombeamento de saída para o Power BI.</span><span class="sxs-lookup"><span data-stu-id="9850d-146">They are automatically created when you start your Stream Analytics job and hello job starts pumping output into Power BI.</span></span> <span data-ttu-id="9850d-147">Se sua consulta de trabalho não retornar nenhum resultado, tabela e conjunto de dados de saudação não são criados.</span><span class="sxs-lookup"><span data-stu-id="9850d-147">If your job query doesn't return any results, hello dataset and table are not  created.</span></span>
    >

8. <span data-ttu-id="9850d-148">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9850d-148">Click **Create**.</span></span>

<span data-ttu-id="9850d-149">saudação de conjunto de dados é criado com hello configurações a seguir:</span><span class="sxs-lookup"><span data-stu-id="9850d-149">hello dataset is created with hello following settings:</span></span>

* <span data-ttu-id="9850d-150">**defaultRetentionPolicy: BasicFIFO**: os dados são FIFO, no máximo com 200 mil linhas.</span><span class="sxs-lookup"><span data-stu-id="9850d-150">**defaultRetentionPolicy: BasicFIFO**: Data is FIFO, with a maximum of 200,000 rows.</span></span>
* <span data-ttu-id="9850d-151">**defaultMode: pushStreaming**: Olá conjunto de dados oferece suporte a streaming blocos e visuais tradicionais baseado no relatório (também conhecido como</span><span class="sxs-lookup"><span data-stu-id="9850d-151">**defaultMode: pushStreaming**: hello dataset supports both streaming tiles and traditional report-based visuals (a.k.a.</span></span> <span data-ttu-id="9850d-152">push).</span><span class="sxs-lookup"><span data-stu-id="9850d-152">push).</span></span>

<span data-ttu-id="9850d-153">Atualmente, não é possível criar conjuntos de dados com outros sinalizadores.</span><span class="sxs-lookup"><span data-stu-id="9850d-153">Currently, you can't create datasets with other flags.</span></span>

<span data-ttu-id="9850d-154">Para obter mais informações sobre conjuntos de dados do Power BI, consulte Olá [API REST do Power BI](https://msdn.microsoft.com/library/mt203562.aspx) referência.</span><span class="sxs-lookup"><span data-stu-id="9850d-154">For more information about Power BI datasets, see hello [Power BI REST API](https://msdn.microsoft.com/library/mt203562.aspx) reference.</span></span>


## <a name="write-hello-query"></a><span data-ttu-id="9850d-155">Gravar consulta Olá</span><span class="sxs-lookup"><span data-stu-id="9850d-155">Write hello query</span></span>

1. <span data-ttu-id="9850d-156">Olá fechar **saídas** folha e retorno toohello folha de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9850d-156">Close hello **Outputs** blade and return toohello job blade.</span></span>

2. <span data-ttu-id="9850d-157">Clique em Olá **consulta** caixa.</span><span class="sxs-lookup"><span data-stu-id="9850d-157">Click hello **Query** box.</span></span> 

3. <span data-ttu-id="9850d-158">Digite hello consulta a seguir.</span><span class="sxs-lookup"><span data-stu-id="9850d-158">Enter hello following query.</span></span> <span data-ttu-id="9850d-159">Essa consulta é semelhante toohello autojunção consulta que você criou no tutorial de detecção de fraudes hello.</span><span class="sxs-lookup"><span data-stu-id="9850d-159">This query is similar toohello self-join query you created in hello fraud-detection tutorial.</span></span> <span data-ttu-id="9850d-160">Olá diferença é que essa consulta envia resultados toohello nova saída criada (`CallStream-PowerBI`).</span><span class="sxs-lookup"><span data-stu-id="9850d-160">hello difference is that this query sends results toohello new output you created (`CallStream-PowerBI`).</span></span> 

    >[!NOTE]
    ><span data-ttu-id="9850d-161">Se você não nome de entrada hello `CallStream` no tutorial de detecção de fraudes hello, substitua o seu nome para `CallStream` em Olá **FROM** e **INGRESSAR** cláusulas na consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="9850d-161">If you did not name hello input `CallStream` in hello fraud-detection tutorial, substitute your name for `CallStream` in hello **FROM** and **JOIN** clauses in hello query.</span></span>

        /* Our criteria for fraud:
        Calls made from hello same caller tootwo phone switches in different locations (for example, Australia and Europe) within five seconds */

        SELECT System.Timestamp AS WindowEnd, COUNT(*) AS FraudulentCalls
        INTO "CallStream-PowerBI"
        FROM "CallStream" CS1 TIMESTAMP BY CallRecTime
        JOIN "CallStream" CS2 TIMESTAMP BY CallRecTime

        /* Where hello caller is hello same, as indicated by IMSI (International Mobile Subscriber Identity) */
        ON CS1.CallingIMSI = CS2.CallingIMSI

        /* ...and date between CS1 and CS2 is between one and five seconds */
        AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5

        /* Where hello switch location is different */
        WHERE CS1.SwitchNum != CS2.SwitchNum
        GROUP BY TumblingWindow(Duration(second, 1))

4. <span data-ttu-id="9850d-162">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="9850d-162">Click **Save**.</span></span>


## <a name="test-hello-query"></a><span data-ttu-id="9850d-163">Consulta de saudação do teste</span><span class="sxs-lookup"><span data-stu-id="9850d-163">Test hello query</span></span>
<span data-ttu-id="9850d-164">Esta etapa é opcional, mas recomendada.</span><span class="sxs-lookup"><span data-stu-id="9850d-164">This section is optional, but recommended.</span></span> 

1. <span data-ttu-id="9850d-165">Se Olá TelcoStreaming app não estiver em execução, inicie-o seguindo estas etapas:</span><span class="sxs-lookup"><span data-stu-id="9850d-165">If hello TelcoStreaming app is not currently running, start it by following these steps:</span></span>

    * <span data-ttu-id="9850d-166">Abra uma janela de comando.</span><span class="sxs-lookup"><span data-stu-id="9850d-166">Open a command window.</span></span>
    * <span data-ttu-id="9850d-167">Vá toohello pasta onde Olá telcogenerator.exe e arquivos telcodatagen.exe.config modificado.</span><span class="sxs-lookup"><span data-stu-id="9850d-167">Go toohello folder where hello telcogenerator.exe and modified telcodatagen.exe.config files are.</span></span>
    * <span data-ttu-id="9850d-168">Execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9850d-168">Run hello following command:</span></span>

            telcodatagen.exe 1000 .2 2

2. <span data-ttu-id="9850d-169">Em hello **consulta** folha, clique em Olá pontos próximo toohello `CallStream` de entrada e, em seguida, selecione **dados de entrada de exemplo**.</span><span class="sxs-lookup"><span data-stu-id="9850d-169">In hello **Query** blade, click hello dots next toohello `CallStream` input and then select **Sample data from input**.</span></span>

3. <span data-ttu-id="9850d-170">Especifique que você deseja dados equivalentes a três minutos e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9850d-170">Specify that you want three minutes' worth of data and click **OK**.</span></span> <span data-ttu-id="9850d-171">Aguarde até que você é notificado de que dados saudação foram amostrados.</span><span class="sxs-lookup"><span data-stu-id="9850d-171">Wait until you're notified that hello data has been sampled.</span></span>

4. <span data-ttu-id="9850d-172">Clique em **Teste** e verifique se você está obtendo resultados.</span><span class="sxs-lookup"><span data-stu-id="9850d-172">Click **Test** and make sure you're getting results.</span></span>


## <a name="run-hello-job"></a><span data-ttu-id="9850d-173">Executar trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="9850d-173">Run hello job</span></span>

1. <span data-ttu-id="9850d-174">Certifique-se de que o aplicativo TelcoStreaming hello está em execução.</span><span class="sxs-lookup"><span data-stu-id="9850d-174">Make sure that hello TelcoStreaming app is running.</span></span>

2. <span data-ttu-id="9850d-175">Olá fechar **consulta** folha.</span><span class="sxs-lookup"><span data-stu-id="9850d-175">Close hello **Query** blade.</span></span>

3. <span data-ttu-id="9850d-176">Na folha de trabalho hello, clique em **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="9850d-176">In hello job blade, click **Start**.</span></span>

    ![Iniciar o trabalho de análise de fluxo de saudação](./media/stream-analytics-power-bi-dashboard/stream-analytics-sa-job-start-output.png)

<span data-ttu-id="9850d-178">O trabalho de análise de fluxo inicia procurando fraudulentas chamadas no fluxo de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="9850d-178">Your Streaming Analytics job starts looking for fraudulent calls in hello incoming stream.</span></span> <span data-ttu-id="9850d-179">trabalho de saudação também cria Olá conjunto de dados e tabela no Power BI e começa a enviar dados sobre Olá fraudulentas chamadas toothem.</span><span class="sxs-lookup"><span data-stu-id="9850d-179">hello job also creates hello dataset and table in Power BI and starts sending data about hello fraudulent calls toothem.</span></span>


## <a name="create-hello-dashboard-in-power-bi"></a><span data-ttu-id="9850d-180">Criar um painel Olá no Power BI</span><span class="sxs-lookup"><span data-stu-id="9850d-180">Create hello dashboard in Power BI</span></span>

1. <span data-ttu-id="9850d-181">Vá muito[Powerbi.com](https://powerbi.com) e entre com sua conta corporativa ou escolar.</span><span class="sxs-lookup"><span data-stu-id="9850d-181">Go too[Powerbi.com](https://powerbi.com) and sign in with your work or school account.</span></span> <span data-ttu-id="9850d-182">Se a consulta de trabalho do Stream Analytics hello gera resultados, verá que o conjunto de dados já foi criado:</span><span class="sxs-lookup"><span data-stu-id="9850d-182">If hello Stream Analytics job query outputs results, you see that your dataset is already created:</span></span>

    ![Conjunto de dados de streaming no Power BI](./media/stream-analytics-power-bi-dashboard/streaming-dataset.png)

2. <span data-ttu-id="9850d-184">No espaço de trabalho, clique em **+&nbsp;Criar**.</span><span class="sxs-lookup"><span data-stu-id="9850d-184">In your workspace, click **+&nbsp;Create**.</span></span>

    ![botão de criar Olá no espaço de trabalho do Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard.png)

3. <span data-ttu-id="9850d-186">Crie um novo painel e nomeie-o `Fraudulent Calls`.</span><span class="sxs-lookup"><span data-stu-id="9850d-186">Create a new dashboard and name it `Fraudulent Calls`.</span></span>

    ![Crie um painel e dê a ele um nome no espaço de trabalho do Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard-name.png)

4. <span data-ttu-id="9850d-188">Na parte superior de saudação da janela de saudação, clique em **Adicionar bloco**, selecione **fluxo de dados personalizado**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="9850d-188">At hello top of hello window, click **Add tile**, select **CUSTOM STREAMING DATA**, and then click **Next**.</span></span>

    ![Conjunto de dados de streaming personalizado](./media/stream-analytics-power-bi-dashboard/custom-streaming-data.png)

5. <span data-ttu-id="9850d-190">Em **SEUS CONJUNTOS DE DADOS**, selecione o conjunto de dados e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="9850d-190">Under **YOUR DATSETS**, select your dataset and then click **Next**.</span></span>

    ![Seu conjunto de dados de streaming](./media/stream-analytics-power-bi-dashboard/your-streaming-dataset.png)

6. <span data-ttu-id="9850d-192">Em **tipo de visualização**, selecione **cartão**e, em seguida, em Olá **campos** lista, selecione **fraudulentcalls**.</span><span class="sxs-lookup"><span data-stu-id="9850d-192">Under **Visualization Type**, select **Card**, and then in hello **Fields** list, select **fraudulentcalls**.</span></span>

    ![Detalhes da visualização para o novo bloco](./media/stream-analytics-power-bi-dashboard/add-fraud.png)

7. <span data-ttu-id="9850d-194">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="9850d-194">Click **Next**.</span></span>

8. <span data-ttu-id="9850d-195">Preencha os detalhes do bloco, tais como um título e subtítulo.</span><span class="sxs-lookup"><span data-stu-id="9850d-195">Fill in tile details like a title and subtitle.</span></span>

    ![Título e subtítulo para o novo bloco](./media/stream-analytics-power-bi-dashboard/pbi-new-tile-details.png)

9. <span data-ttu-id="9850d-197">Clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="9850d-197">Click **Apply**.</span></span>

    <span data-ttu-id="9850d-198">Agora você tem um contador de fraudes!</span><span class="sxs-lookup"><span data-stu-id="9850d-198">Now you have a fraud counter!</span></span>

    ![Contador de fraudes](./media/stream-analytics-power-bi-dashboard/fraud-counter.png)

8. <span data-ttu-id="9850d-200">Olá siga etapas novamente tooadd um bloco (começando com a etapa 4).</span><span class="sxs-lookup"><span data-stu-id="9850d-200">Follow hello steps again tooadd a tile (starting with step 4).</span></span> <span data-ttu-id="9850d-201">Neste momento, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="9850d-201">This time, do hello following:</span></span>

    * <span data-ttu-id="9850d-202">Quando você obtém muito**tipo de visualização**, selecione **gráfico de linhas**.</span><span class="sxs-lookup"><span data-stu-id="9850d-202">When you get too**Visualization Type**, select **Line chart**.</span></span> 
    * <span data-ttu-id="9850d-203">Adicionar um eixo e selecione **windowend**.</span><span class="sxs-lookup"><span data-stu-id="9850d-203">Add an axis and select **windowend**.</span></span> 
    * <span data-ttu-id="9850d-204">Adicione um valor e selecione **fraudulentcalls**.</span><span class="sxs-lookup"><span data-stu-id="9850d-204">Add a value and select **fraudulentcalls**.</span></span>
    * <span data-ttu-id="9850d-205">Para **toodisplay da janela de tempo**, selecione Olá últimos 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="9850d-205">For **Time window toodisplay**, select hello last 10 minutes.</span></span>

    ![Criar um bloco para o gráfico de linhas](./media/stream-analytics-power-bi-dashboard/pbi-create-tile-line-chart.png)

9. <span data-ttu-id="9850d-207">Clique em **Avançar**, adicione um título e subtítulo e clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="9850d-207">Click **Next**, add a title and subtitle, and click **Apply**.</span></span>

    <span data-ttu-id="9850d-208">painel do Power BI Olá agora oferece dois modos de exibição de dados sobre chamadas fraudulentas conforme detectado no hello fluxo de dados.</span><span class="sxs-lookup"><span data-stu-id="9850d-208">hello Power BI dashboard now gives you two views of data about fraudulent calls as detected in hello streaming data.</span></span>

    ![O painel do Power BI foi concluído mostrando dois blocos para chamadas fraudulentas](./media/stream-analytics-power-bi-dashboard/pbi-dashboard-fraudulent-calls-finished.png)


## <a name="learn-more-about-power-bi"></a><span data-ttu-id="9850d-210">Saiba mais sobre o Power BI</span><span class="sxs-lookup"><span data-stu-id="9850d-210">Learn more about Power BI</span></span>

<span data-ttu-id="9850d-211">Este tutorial demonstra como toocreate apenas alguns tipos de visualizações de um conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="9850d-211">This tutorial demonstrates how toocreate only a few kinds of visualizations for a dataset.</span></span> <span data-ttu-id="9850d-212">O Power BI pode ajudá-lo a criar outras ferramentas de cliente business intelligence para sua organização.</span><span class="sxs-lookup"><span data-stu-id="9850d-212">Power BI can help you create other customer business intelligence tools for your organization.</span></span> <span data-ttu-id="9850d-213">Para obter mais ideias, consulte Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="9850d-213">For more ideas, see hello following resources:</span></span>

* <span data-ttu-id="9850d-214">Outro exemplo de um painel do Power BI, assista a saudação [guia de Introdução ao Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) vídeo.</span><span class="sxs-lookup"><span data-stu-id="9850d-214">For another example of a Power BI dashboard, watch hello [Getting Started with Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) video.</span></span>
* <span data-ttu-id="9850d-215">Para obter mais informações sobre como configurar a análise de fluxo de trabalho saída tooPower BI e usando grupos do Power BI, examine a saudação [Power BI](stream-analytics-define-outputs.md#power-bi) seção Olá [do Stream Analytics gera](stream-analytics-define-outputs.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="9850d-215">For more information about configuring Streaming Analytics job output tooPower BI and using Power BI groups, review hello [Power BI](stream-analytics-define-outputs.md#power-bi) section of hello [Stream Analytics outputs](stream-analytics-define-outputs.md) article.</span></span> 
* <span data-ttu-id="9850d-216">Para obter informações sobre como usar o Power BI em geral, consulte [Painéis no Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span><span class="sxs-lookup"><span data-stu-id="9850d-216">For information about using Power BI generally, see [Dashboards in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span></span>


## <a name="learn-about-limitations-and-best-practices"></a><span data-ttu-id="9850d-217">Saiba mais sobre limitações e práticas recomendadas</span><span class="sxs-lookup"><span data-stu-id="9850d-217">Learn about limitations and best practices</span></span>
<span data-ttu-id="9850d-218">Atualmente, o Power BI pode ser chamado aproximadamente uma vez por segundo.</span><span class="sxs-lookup"><span data-stu-id="9850d-218">Currently, Power BI can be called roughly once per second.</span></span> <span data-ttu-id="9850d-219">A transmissão de elementos visuais oferece suporte a pacotes de 15 KB.</span><span class="sxs-lookup"><span data-stu-id="9850d-219">Streaming visuals support packets of 15 KB.</span></span> <span data-ttu-id="9850d-220">Além disso, falham de streaming visuais (mas push continua toowork).</span><span class="sxs-lookup"><span data-stu-id="9850d-220">Beyond that, streaming visuals fail (but push continues toowork).</span></span> <span data-ttu-id="9850d-221">Devido a essas limitações, Power BI Preste mais naturalmente toocases onde Stream Analytics do Azure reduz uma quantidade significativa de dados de carga.</span><span class="sxs-lookup"><span data-stu-id="9850d-221">Because of these limitations, Power BI lends itself most naturally toocases where Azure Stream Analytics does a significant data load reduction.</span></span> <span data-ttu-id="9850d-222">É recomendável usar uma janela em cascata ou Hopping janela tooensure dados por push está no máximo um envio por segundo, e se sua consulta cair dentro dos requisitos de taxa de transferência de saudação.</span><span class="sxs-lookup"><span data-stu-id="9850d-222">We recommend using a Tumbling window or Hopping window tooensure that data push is at most one push per second, and that your query lands within hello throughput requirements.</span></span>

<span data-ttu-id="9850d-223">Você pode usar o hello seguinte equação toocompute Olá valor toogive a janela em segundos:</span><span class="sxs-lookup"><span data-stu-id="9850d-223">You can use hello following equation toocompute hello value toogive your window in seconds:</span></span>

![Equação1](./media/stream-analytics-power-bi-dashboard/equation1.png)  

<span data-ttu-id="9850d-225">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9850d-225">For example:</span></span>

* <span data-ttu-id="9850d-226">Você tem 1.000 dispositivos que enviam dados em intervalos de um segundo.</span><span class="sxs-lookup"><span data-stu-id="9850d-226">You have 1,000 devices sending data at one-second intervals.</span></span>
* <span data-ttu-id="9850d-227">Você está usando Olá Power BI SKU Pro que suporta 1.000.000 linhas por hora.</span><span class="sxs-lookup"><span data-stu-id="9850d-227">You are using hello Power BI Pro SKU that supports 1,000,000 rows per hour.</span></span>
* <span data-ttu-id="9850d-228">Você deseja toopublish quantidade de saudação da média de dados por dispositivo tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="9850d-228">You want toopublish hello amount of average data per device tooPower BI.</span></span>

<span data-ttu-id="9850d-229">Como resultado, a equação de saudação se torna:</span><span class="sxs-lookup"><span data-stu-id="9850d-229">As a result, hello equation becomes:</span></span>

![Equação2](./media/stream-analytics-power-bi-dashboard/equation2.png)  

<span data-ttu-id="9850d-231">Dada essa configuração, você pode alterar a seguir original de toohello consulta hello:</span><span class="sxs-lookup"><span data-stu-id="9850d-231">Given this configuration, you can change hello original query toohello following:</span></span>

    SELECT
        MAX(hmdt) AS hmdt,
        MAX(temp) AS temp,
        System.TimeStamp AS time,
        dspl
    INTO "CallStream-PowerBI"
    FROM
        Input TIMESTAMP BY time
    GROUP BY
        TUMBLINGWINDOW(ss,4),
        dspl


### <a name="renew-authorization"></a><span data-ttu-id="9850d-232">Renovar autorização</span><span class="sxs-lookup"><span data-stu-id="9850d-232">Renew authorization</span></span>
<span data-ttu-id="9850d-233">Se Olá senha alterada desde que o trabalho foi criado ou última autenticado, será necessário tooreauthenticate sua conta do Power BI.</span><span class="sxs-lookup"><span data-stu-id="9850d-233">If hello password has changed since your job was created or last authenticated, you need tooreauthenticate your Power BI account.</span></span> <span data-ttu-id="9850d-234">Se o Azure multi-Factor Authentication está configurado no seu locatário do Azure Active Directory (AD do Azure), você também precisará autorização do Power BI de toorenew a cada duas semanas.</span><span class="sxs-lookup"><span data-stu-id="9850d-234">If Azure Multi-Factor Authentication is configured on your Azure Active Directory (Azure AD) tenant, you also need toorenew Power BI authorization every two weeks.</span></span> <span data-ttu-id="9850d-235">Se você não renovar, você pode ver os sintomas como falta de saída de trabalho ou um `Authenticate user error` nos logs de operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9850d-235">If you don't renew, you could see symptoms such as a lack of job output or an `Authenticate user error` in hello operation logs.</span></span>

<span data-ttu-id="9850d-236">Da mesma forma, se um trabalho é iniciado depois Olá token tiver expirado, ocorrerá um erro e Olá trabalho falhar.</span><span class="sxs-lookup"><span data-stu-id="9850d-236">Similarly, if a job starts after hello token has expired, an error occurs and hello job fails.</span></span> <span data-ttu-id="9850d-237">tooresolve esse problema, parar trabalho Olá que está em execução e ir tooyour Power BI de saída.</span><span class="sxs-lookup"><span data-stu-id="9850d-237">tooresolve this issue, stop hello job that's running and go tooyour Power BI output.</span></span> <span data-ttu-id="9850d-238">tooavoid perda de dados, selecione Olá **renovar autorização** link e, em seguida, reinicie o trabalho de saudação **hora da última interrupção**.</span><span class="sxs-lookup"><span data-stu-id="9850d-238">tooavoid data loss, select hello **Renew authorization** link, and then restart your job from hello **Last Stopped Time**.</span></span>

<span data-ttu-id="9850d-239">Após a autorização Olá foi atualizada com o Power BI, um alerta verde é exibida em Olá autorização área tooreflect que problema Olá foi resolvido.</span><span class="sxs-lookup"><span data-stu-id="9850d-239">After hello authorization has been refreshed with Power BI, a green alert appears in hello authorization area tooreflect that hello issue has been resolved.</span></span>

## <a name="get-help"></a><span data-ttu-id="9850d-240">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="9850d-240">Get help</span></span>
<span data-ttu-id="9850d-241">Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="9850d-241">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9850d-242">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9850d-242">Next steps</span></span>
* [<span data-ttu-id="9850d-243">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9850d-243">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="9850d-244">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="9850d-244">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="9850d-245">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="9850d-245">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="9850d-246">Referência de linguagem de consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="9850d-246">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="9850d-247">Referência da API REST do Gerenciamento do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="9850d-247">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
