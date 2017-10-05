---
title: Painel do Power BI no Stream Analytics do Azure | Microsoft Docs
description: "Use um painel de Power BI de transmissão em tempo real para reunir inteligência comercial e analisar grandes volumes de dados de um trabalho de Stream Analytics."
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
ms.openlocfilehash: 874d9b8701a24deb3cc21aa74cb51870155c7c9c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="stream-analytics-and-power-bi-a-real-time-analytics-dashboard-for-streaming-data"></a><span data-ttu-id="37533-104">Stream Analytics e Power BI: um painel de análise em tempo real para dados de streaming</span><span class="sxs-lookup"><span data-stu-id="37533-104">Stream Analytics and Power BI: A real-time analytics dashboard for streaming data</span></span>
<span data-ttu-id="37533-105">O Stream Analytics do Azure permite aproveitar uma das principais ferramentas de business intelligence, o [Microsoft Power BI](https://powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="37533-105">Azure Stream Analytics enables you to take advantage of one of the leading business intelligence tools, [Microsoft Power BI](https://powerbi.com/).</span></span> <span data-ttu-id="37533-106">Neste artigo, você saberá como criar ferramentas de business intelligence usando o Power BI como uma saída de seus trabalhos do Stream Analytics do Azure.</span><span class="sxs-lookup"><span data-stu-id="37533-106">In this article, you learn how create business intelligence tools by using Power BI as an output for your Azure Stream Analytics jobs.</span></span> <span data-ttu-id="37533-107">Você também aprenderá a criar e usar um painel em tempo real.</span><span class="sxs-lookup"><span data-stu-id="37533-107">You also learn how to create and use a real-time dashboard.</span></span>

<span data-ttu-id="37533-108">Este artigo continua no tutorial [Detecção de fraude em tempo real](stream-analytics-real-time-fraud-detection.md) do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="37533-108">This article continues from the Stream Analytics [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="37533-109">Ele amplia o fluxo de trabalho criado neste tutorial e adiciona uma saída do Power BI para que você pode visualizar chamadas telefônicas fraudulentas que são detectadas por um trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="37533-109">It builds on the workflow created in that tutorial and adds a Power BI output so that you can visualize fraudulent phone calls that are detected by a Streaming Analytics job.</span></span> 

<span data-ttu-id="37533-110">Você pode assistir a [um vídeo](https://www.youtube.com/watch?v=SGUpT-a99MA) que ilustra esse cenário.</span><span class="sxs-lookup"><span data-stu-id="37533-110">You can watch [a video](https://www.youtube.com/watch?v=SGUpT-a99MA)  that illustrates this scenario.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="37533-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="37533-111">Prerequisites</span></span>

<span data-ttu-id="37533-112">Antes de começar, verifique se você tem o seguinte:</span><span class="sxs-lookup"><span data-stu-id="37533-112">Before you start, make sure you have the following:</span></span>

* <span data-ttu-id="37533-113">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="37533-113">An Azure account.</span></span>
* <span data-ttu-id="37533-114">Uma conta para o Power BI.</span><span class="sxs-lookup"><span data-stu-id="37533-114">An account for Power BI.</span></span> <span data-ttu-id="37533-115">Você pode usar uma conta corporativa ou de estudante.</span><span class="sxs-lookup"><span data-stu-id="37533-115">You can use a work account or a school account.</span></span>
* <span data-ttu-id="37533-116">Uma versão concluída do tutorial [Detecção de fraudes em tempo real](stream-analytics-real-time-fraud-detection.md).</span><span class="sxs-lookup"><span data-stu-id="37533-116">A completed version of the [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="37533-117">O tutorial inclui um aplicativo que gera metadados de chamada telefônica fictícios.</span><span class="sxs-lookup"><span data-stu-id="37533-117">The tutorial includes an app that generates fictitious telephone-call metadata.</span></span> <span data-ttu-id="37533-118">No tutorial, você cria um hub de eventos e envia os dados de streaming de chamada telefônica para o hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="37533-118">In the tutorial, you create an event hub and send the streaming phone call data to the event hub.</span></span> <span data-ttu-id="37533-119">Você escreve uma consulta que detecta chamadas fraudulentas (chamadas simultâneas do mesmo número em diferentes locais).</span><span class="sxs-lookup"><span data-stu-id="37533-119">You write a query that detects fraudulent calls (calls from the same number at the same time in different locations).</span></span> 


## <a name="add-power-bi-output"></a><span data-ttu-id="37533-120">Adicionar saída do Power BI</span><span class="sxs-lookup"><span data-stu-id="37533-120">Add Power BI output</span></span>
<span data-ttu-id="37533-121">No tutorial de detecção de fraudes em tempo real, a saída é enviada para o Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="37533-121">In the real-time fraud detection tutorial, the output is sent to Azure Blob storage.</span></span> <span data-ttu-id="37533-122">Nesta seção, você deve adicionar uma saída que envia informações ao Power BI.</span><span class="sxs-lookup"><span data-stu-id="37533-122">In this section, you add an output that sends information to Power BI.</span></span>

1. <span data-ttu-id="37533-123">No Portal do Azure, abra o trabalho do Stream Analytics criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="37533-123">In the Azure portal, open the Streaming Analytics job that you created earlier.</span></span> <span data-ttu-id="37533-124">Se você usou o nome sugerido, o trabalho é nomeado `sa_frauddetection_job_demo`.</span><span class="sxs-lookup"><span data-stu-id="37533-124">If you used the suggested name, the job is named `sa_frauddetection_job_demo`.</span></span>

2. <span data-ttu-id="37533-125">Marque a caixa **Saídas** no meio do painel do trabalho e então selecione **+ Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="37533-125">Select the **Outputs** box in the middle of the job dashboard and then select **+ Add**.</span></span>

3. <span data-ttu-id="37533-126">Para **Alias de Saída**, digite `CallStream-PowerBI`.</span><span class="sxs-lookup"><span data-stu-id="37533-126">For **Output Alias**, enter `CallStream-PowerBI`.</span></span> <span data-ttu-id="37533-127">Você pode usar um nome diferente.</span><span class="sxs-lookup"><span data-stu-id="37533-127">You can use a different name.</span></span> <span data-ttu-id="37533-128">Se você fizer isso, anote-o, pois você precisará desse nome mais tarde.</span><span class="sxs-lookup"><span data-stu-id="37533-128">If you do, make a note of it, because you need the name later.</span></span> 

4. <span data-ttu-id="37533-129">Em **Coletor**, selecione **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="37533-129">Under **Sink**, select **Power BI**.</span></span>

   ![Criar uma saída para o Power BI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut.png)

5. <span data-ttu-id="37533-131">Clique em **Autorizar**.</span><span class="sxs-lookup"><span data-stu-id="37533-131">Click **Authorize**.</span></span>

    <span data-ttu-id="37533-132">É aberta uma janela em que você pode fornecer suas credenciais do Azure para uma conta corporativa ou de estudante.</span><span class="sxs-lookup"><span data-stu-id="37533-132">A window opens where you can provide your Azure credentials for a work or school account.</span></span> 

    ![Insira as credenciais para acesso ao Power BI](./media/stream-analytics-power-bi-dashboard/authorize-area.png)

6. <span data-ttu-id="37533-134">Insira suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="37533-134">Enter your credentials.</span></span> <span data-ttu-id="37533-135">Lembre-se que quando você inserir suas credenciais, você também estará concedendo permissão para o trabalho do Stream Analytics para acessar a área do Power BI.</span><span class="sxs-lookup"><span data-stu-id="37533-135">Be aware then when you enter your credentials, you're also giving permission to the Streaming Analytics job to access your Power BI area.</span></span>

7. <span data-ttu-id="37533-136">Quando você retornar para a folha **Nova saída**, insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="37533-136">When you're returned to the **New output** blade, enter the following information:</span></span>

    * <span data-ttu-id="37533-137">**Espaço de Trabalho de Grupo**: selecione um espaço de trabalho no seu locatário do Power BI em que você deseja criar o conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="37533-137">**Group Workspace**: Select a workspace in your Power BI tenant where you want to create the dataset.</span></span>
    * <span data-ttu-id="37533-138">**Nome do Conjunto de Dados**: insira `sa-dataset`.</span><span class="sxs-lookup"><span data-stu-id="37533-138">**Dataset Name**:  Enter `sa-dataset`.</span></span> <span data-ttu-id="37533-139">Você pode usar um nome diferente.</span><span class="sxs-lookup"><span data-stu-id="37533-139">You can use a different name.</span></span> <span data-ttu-id="37533-140">Se você fizer isso, anote-o para mais tarde.</span><span class="sxs-lookup"><span data-stu-id="37533-140">If you do, make a note of it for later.</span></span>
    * <span data-ttu-id="37533-141">**Nome da Tabela**: insira `fraudulent-calls`.</span><span class="sxs-lookup"><span data-stu-id="37533-141">**Table Name**: Enter `fraudulent-calls`.</span></span> <span data-ttu-id="37533-142">Atualmente, a saída do Power BI de trabalhos do Stream Analytics só podem ter uma tabela em um conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="37533-142">Currently, Power BI output from Stream Analytics jobs can have only one table in a dataset.</span></span>

    ![Espaço de trabalho de PBI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut-with-dataset-table.png)

    > [!WARNING]
    > <span data-ttu-id="37533-144">Se o Power BI tem um conjunto de dados e uma tabela que tem os mesmo nomes daquelas especificadas por você no trabalho do Stream Analytics, os existentes são substituídos.</span><span class="sxs-lookup"><span data-stu-id="37533-144">If Power BI has a dataset and table that have the same names as the ones that you specify in the Stream Analytics job, the existing ones are overwritten.</span></span>
    > <span data-ttu-id="37533-145">Recomendamos que você não crie explicitamente esse conjunto de dados e a tabela em sua conta do Power BI.</span><span class="sxs-lookup"><span data-stu-id="37533-145">We recommend that you do not explicitly create this dataset and table in your Power BI account.</span></span> <span data-ttu-id="37533-146">Ele serão automaticamente criados quando você iniciar o trabalho do Stream Analytics e ele começar a enviar saídas para o Power BI.</span><span class="sxs-lookup"><span data-stu-id="37533-146">They are automatically created when you start your Stream Analytics job and the job starts pumping output into Power BI.</span></span> <span data-ttu-id="37533-147">Se a consulta de trabalho não gerar resultados, o conjunto de dados e a tabela não serão criados.</span><span class="sxs-lookup"><span data-stu-id="37533-147">If your job query doesn't return any results, the dataset and table are not  created.</span></span>
    >

8. <span data-ttu-id="37533-148">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="37533-148">Click **Create**.</span></span>

<span data-ttu-id="37533-149">O conjunto de dados é criado com as seguintes configurações:</span><span class="sxs-lookup"><span data-stu-id="37533-149">The dataset is created with the following settings:</span></span>

* <span data-ttu-id="37533-150">**defaultRetentionPolicy: BasicFIFO**: os dados são FIFO, no máximo com 200 mil linhas.</span><span class="sxs-lookup"><span data-stu-id="37533-150">**defaultRetentionPolicy: BasicFIFO**: Data is FIFO, with a maximum of 200,000 rows.</span></span>
* <span data-ttu-id="37533-151">**defaultMode: pushStreaming**: o conjunto de dados dá suporte aos blocos de streaming e visuais com base em relatórios tradicionais (também conhecido como</span><span class="sxs-lookup"><span data-stu-id="37533-151">**defaultMode: pushStreaming**: The dataset supports both streaming tiles and traditional report-based visuals (a.k.a.</span></span> <span data-ttu-id="37533-152">push).</span><span class="sxs-lookup"><span data-stu-id="37533-152">push).</span></span>

<span data-ttu-id="37533-153">Atualmente, não é possível criar conjuntos de dados com outros sinalizadores.</span><span class="sxs-lookup"><span data-stu-id="37533-153">Currently, you can't create datasets with other flags.</span></span>

<span data-ttu-id="37533-154">Para saber mais sobre conjuntos de dados do Power BI, consulte a referência à [API REST do Power BI](https://msdn.microsoft.com/library/mt203562.aspx).</span><span class="sxs-lookup"><span data-stu-id="37533-154">For more information about Power BI datasets, see the [Power BI REST API](https://msdn.microsoft.com/library/mt203562.aspx) reference.</span></span>


## <a name="write-the-query"></a><span data-ttu-id="37533-155">Gravar a consulta</span><span class="sxs-lookup"><span data-stu-id="37533-155">Write the query</span></span>

1. <span data-ttu-id="37533-156">Feche a folha **Saídas** e retorne para a folha de trabalho.</span><span class="sxs-lookup"><span data-stu-id="37533-156">Close the **Outputs** blade and return to the job blade.</span></span>

2. <span data-ttu-id="37533-157">Clique na caixa **Consulta**.</span><span class="sxs-lookup"><span data-stu-id="37533-157">Click the **Query** box.</span></span> 

3. <span data-ttu-id="37533-158">Insira a consulta a seguir.</span><span class="sxs-lookup"><span data-stu-id="37533-158">Enter the following query.</span></span> <span data-ttu-id="37533-159">Essa consulta é semelhante à consulta de autojunção que você criou no tutorial de detecção de fraudes.</span><span class="sxs-lookup"><span data-stu-id="37533-159">This query is similar to the self-join query you created in the fraud-detection tutorial.</span></span> <span data-ttu-id="37533-160">A diferença é que essa consulta envia resultados para a nova saída criada por você (`CallStream-PowerBI`).</span><span class="sxs-lookup"><span data-stu-id="37533-160">The difference is that this query sends results to the new output you created (`CallStream-PowerBI`).</span></span> 

    >[!NOTE]
    ><span data-ttu-id="37533-161">Se você não nomear a entrada `CallStream` no tutorial de detecção de fraudes, substitua o seu nome para `CallStream` nas cláusulas **FROM** e **JOIN** na consulta.</span><span class="sxs-lookup"><span data-stu-id="37533-161">If you did not name the input `CallStream` in the fraud-detection tutorial, substitute your name for `CallStream` in the **FROM** and **JOIN** clauses in the query.</span></span>

        /* Our criteria for fraud:
        Calls made from the same caller to two phone switches in different locations (for example, Australia and Europe) within five seconds */

        SELECT System.Timestamp AS WindowEnd, COUNT(*) AS FraudulentCalls
        INTO "CallStream-PowerBI"
        FROM "CallStream" CS1 TIMESTAMP BY CallRecTime
        JOIN "CallStream" CS2 TIMESTAMP BY CallRecTime

        /* Where the caller is the same, as indicated by IMSI (International Mobile Subscriber Identity) */
        ON CS1.CallingIMSI = CS2.CallingIMSI

        /* ...and date between CS1 and CS2 is between one and five seconds */
        AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5

        /* Where the switch location is different */
        WHERE CS1.SwitchNum != CS2.SwitchNum
        GROUP BY TumblingWindow(Duration(second, 1))

4. <span data-ttu-id="37533-162">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="37533-162">Click **Save**.</span></span>


## <a name="test-the-query"></a><span data-ttu-id="37533-163">Testar a consulta</span><span class="sxs-lookup"><span data-stu-id="37533-163">Test the query</span></span>
<span data-ttu-id="37533-164">Esta etapa é opcional, mas recomendada.</span><span class="sxs-lookup"><span data-stu-id="37533-164">This section is optional, but recommended.</span></span> 

1. <span data-ttu-id="37533-165">Se o aplicativo TelcoStreaming não estiver em execução, inicie-o seguindo estas etapas:</span><span class="sxs-lookup"><span data-stu-id="37533-165">If the TelcoStreaming app is not currently running, start it by following these steps:</span></span>

    * <span data-ttu-id="37533-166">Abra uma janela de comando.</span><span class="sxs-lookup"><span data-stu-id="37533-166">Open a command window.</span></span>
    * <span data-ttu-id="37533-167">Vá para a pasta em que os arquivos telcodatagen.exe.config e telcogenerator.exe.config modificado estão.</span><span class="sxs-lookup"><span data-stu-id="37533-167">Go to the folder where the telcogenerator.exe and modified telcodatagen.exe.config files are.</span></span>
    * <span data-ttu-id="37533-168">Execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="37533-168">Run the following command:</span></span>

            telcodatagen.exe 1000 .2 2

2. <span data-ttu-id="37533-169">Na folha **Consulta**, clique nos pontos ao lado da entrada `CallStream` e, em seguida, selecione **Dados de exemplo da entrada**.</span><span class="sxs-lookup"><span data-stu-id="37533-169">In the **Query** blade, click the dots next to the `CallStream` input and then select **Sample data from input**.</span></span>

3. <span data-ttu-id="37533-170">Especifique que você deseja dados equivalentes a três minutos e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="37533-170">Specify that you want three minutes' worth of data and click **OK**.</span></span> <span data-ttu-id="37533-171">Aguarde até ser notificado de que a amostragem dos dados foi realizada.</span><span class="sxs-lookup"><span data-stu-id="37533-171">Wait until you're notified that the data has been sampled.</span></span>

4. <span data-ttu-id="37533-172">Clique em **Teste** e verifique se você está obtendo resultados.</span><span class="sxs-lookup"><span data-stu-id="37533-172">Click **Test** and make sure you're getting results.</span></span>


## <a name="run-the-job"></a><span data-ttu-id="37533-173">Executar o trabalho</span><span class="sxs-lookup"><span data-stu-id="37533-173">Run the job</span></span>

1. <span data-ttu-id="37533-174">Verifique se o aplicativo TelcoStreaming está em execução.</span><span class="sxs-lookup"><span data-stu-id="37533-174">Make sure that the TelcoStreaming app is running.</span></span>

2. <span data-ttu-id="37533-175">Feche a folha **Consulta**.</span><span class="sxs-lookup"><span data-stu-id="37533-175">Close the **Query** blade.</span></span>

3. <span data-ttu-id="37533-176">Na folha do trabalho, clique em **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="37533-176">In the job blade, click **Start**.</span></span>

    ![Iniciar o trabalho do Stream Analytics](./media/stream-analytics-power-bi-dashboard/stream-analytics-sa-job-start-output.png)

<span data-ttu-id="37533-178">O trabalho do Stream Analytics começa procurando chamadas fraudulentas no fluxo de entrada.</span><span class="sxs-lookup"><span data-stu-id="37533-178">Your Streaming Analytics job starts looking for fraudulent calls in the incoming stream.</span></span> <span data-ttu-id="37533-179">O trabalho também cria o conjunto de dados e a tabela no Power BI e começa a enviar dados sobre as chamadas fraudulentas para eles.</span><span class="sxs-lookup"><span data-stu-id="37533-179">The job also creates the dataset and table in Power BI and starts sending data about the fraudulent calls to them.</span></span>


## <a name="create-the-dashboard-in-power-bi"></a><span data-ttu-id="37533-180">Criar o painel no Power BI</span><span class="sxs-lookup"><span data-stu-id="37533-180">Create the dashboard in Power BI</span></span>

1. <span data-ttu-id="37533-181">Acesse [Powerbi.com](https://powerbi.com) e entre com a sua conta corporativa ou de estudante.</span><span class="sxs-lookup"><span data-stu-id="37533-181">Go to [Powerbi.com](https://powerbi.com) and sign in with your work or school account.</span></span> <span data-ttu-id="37533-182">Se a consulta do trabalho do Stream Analytics gera resultados como saída, você vê que o conjunto de dados já está criado:</span><span class="sxs-lookup"><span data-stu-id="37533-182">If the Stream Analytics job query outputs results, you see that your dataset is already created:</span></span>

    ![Conjunto de dados de streaming no Power BI](./media/stream-analytics-power-bi-dashboard/streaming-dataset.png)

2. <span data-ttu-id="37533-184">No espaço de trabalho, clique em **+&nbsp;Criar**.</span><span class="sxs-lookup"><span data-stu-id="37533-184">In your workspace, click **+&nbsp;Create**.</span></span>

    ![O botão Criar no espaço de trabalho do Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard.png)

3. <span data-ttu-id="37533-186">Crie um novo painel e nomeie-o `Fraudulent Calls`.</span><span class="sxs-lookup"><span data-stu-id="37533-186">Create a new dashboard and name it `Fraudulent Calls`.</span></span>

    ![Crie um painel e dê a ele um nome no espaço de trabalho do Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard-name.png)

4. <span data-ttu-id="37533-188">Na parte superior da janela, clique em **Adicionar bloco**, selecione **DADOS DE STREAMING PERSONALIZADOS** e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="37533-188">At the top of the window, click **Add tile**, select **CUSTOM STREAMING DATA**, and then click **Next**.</span></span>

    ![Conjunto de dados de streaming personalizado](./media/stream-analytics-power-bi-dashboard/custom-streaming-data.png)

5. <span data-ttu-id="37533-190">Em **SEUS CONJUNTOS DE DADOS**, selecione o conjunto de dados e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="37533-190">Under **YOUR DATSETS**, select your dataset and then click **Next**.</span></span>

    ![Seu conjunto de dados de streaming](./media/stream-analytics-power-bi-dashboard/your-streaming-dataset.png)

6. <span data-ttu-id="37533-192">Em **Tipo de Visualização**, selecione **Cartão** e, em seguida, na lista **Campos**, selecione **fraudulentcalls**.</span><span class="sxs-lookup"><span data-stu-id="37533-192">Under **Visualization Type**, select **Card**, and then in the **Fields** list, select **fraudulentcalls**.</span></span>

    ![Detalhes da visualização para o novo bloco](./media/stream-analytics-power-bi-dashboard/add-fraud.png)

7. <span data-ttu-id="37533-194">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="37533-194">Click **Next**.</span></span>

8. <span data-ttu-id="37533-195">Preencha os detalhes do bloco, tais como um título e subtítulo.</span><span class="sxs-lookup"><span data-stu-id="37533-195">Fill in tile details like a title and subtitle.</span></span>

    ![Título e subtítulo para o novo bloco](./media/stream-analytics-power-bi-dashboard/pbi-new-tile-details.png)

9. <span data-ttu-id="37533-197">Clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="37533-197">Click **Apply**.</span></span>

    <span data-ttu-id="37533-198">Agora você tem um contador de fraudes!</span><span class="sxs-lookup"><span data-stu-id="37533-198">Now you have a fraud counter!</span></span>

    ![Contador de fraudes](./media/stream-analytics-power-bi-dashboard/fraud-counter.png)

8. <span data-ttu-id="37533-200">Siga as etapas novamente para adicionar um bloco (começando pela etapa 4).</span><span class="sxs-lookup"><span data-stu-id="37533-200">Follow the steps again to add a tile (starting with step 4).</span></span> <span data-ttu-id="37533-201">Dessa vez, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="37533-201">This time, do the following:</span></span>

    * <span data-ttu-id="37533-202">Quando você chegar em **Tipo de Visualização**, selecione **Gráfico de linhas**.</span><span class="sxs-lookup"><span data-stu-id="37533-202">When you get to **Visualization Type**, select **Line chart**.</span></span> 
    * <span data-ttu-id="37533-203">Adicionar um eixo e selecione **windowend**.</span><span class="sxs-lookup"><span data-stu-id="37533-203">Add an axis and select **windowend**.</span></span> 
    * <span data-ttu-id="37533-204">Adicione um valor e selecione **fraudulentcalls**.</span><span class="sxs-lookup"><span data-stu-id="37533-204">Add a value and select **fraudulentcalls**.</span></span>
    * <span data-ttu-id="37533-205">Para **Janela de tempo para exibir**, selecione os últimos 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="37533-205">For **Time window to display**, select the last 10 minutes.</span></span>

    ![Criar um bloco para o gráfico de linhas](./media/stream-analytics-power-bi-dashboard/pbi-create-tile-line-chart.png)

9. <span data-ttu-id="37533-207">Clique em **Avançar**, adicione um título e subtítulo e clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="37533-207">Click **Next**, add a title and subtitle, and click **Apply**.</span></span>

    <span data-ttu-id="37533-208">O painel do Power BI agora oferece dois modos de exibição de dados sobre chamadas fraudulentas conforme detectado nos dados de streaming.</span><span class="sxs-lookup"><span data-stu-id="37533-208">The Power BI dashboard now gives you two views of data about fraudulent calls as detected in the streaming data.</span></span>

    ![O painel do Power BI foi concluído mostrando dois blocos para chamadas fraudulentas](./media/stream-analytics-power-bi-dashboard/pbi-dashboard-fraudulent-calls-finished.png)


## <a name="learn-more-about-power-bi"></a><span data-ttu-id="37533-210">Saiba mais sobre o Power BI</span><span class="sxs-lookup"><span data-stu-id="37533-210">Learn more about Power BI</span></span>

<span data-ttu-id="37533-211">Este tutorial demonstra como criar somente alguns tipos de visualizações para um conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="37533-211">This tutorial demonstrates how to create only a few kinds of visualizations for a dataset.</span></span> <span data-ttu-id="37533-212">O Power BI pode ajudá-lo a criar outras ferramentas de cliente business intelligence para sua organização.</span><span class="sxs-lookup"><span data-stu-id="37533-212">Power BI can help you create other customer business intelligence tools for your organization.</span></span> <span data-ttu-id="37533-213">Para obter mais ideias, consulte os recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="37533-213">For more ideas, see the following resources:</span></span>

* <span data-ttu-id="37533-214">Para obter outro exemplo de um painel do Power BI, assista ao vídeo [Introdução ao Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) .</span><span class="sxs-lookup"><span data-stu-id="37533-214">For another example of a Power BI dashboard, watch the [Getting Started with Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) video.</span></span>
* <span data-ttu-id="37533-215">Para obter mais informações sobre como configurar uma saída do trabalho do Stream Analytics para o Power BI e usar grupos do Power BI, examine a seção [Power BI](stream-analytics-define-outputs.md#power-bi) do artigo [Saídas do Stream Analytics](stream-analytics-define-outputs.md).</span><span class="sxs-lookup"><span data-stu-id="37533-215">For more information about configuring Streaming Analytics job output to Power BI and using Power BI groups, review the [Power BI](stream-analytics-define-outputs.md#power-bi) section of the [Stream Analytics outputs](stream-analytics-define-outputs.md) article.</span></span> 
* <span data-ttu-id="37533-216">Para obter informações sobre como usar o Power BI em geral, consulte [Painéis no Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span><span class="sxs-lookup"><span data-stu-id="37533-216">For information about using Power BI generally, see [Dashboards in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span></span>


## <a name="learn-about-limitations-and-best-practices"></a><span data-ttu-id="37533-217">Saiba mais sobre limitações e práticas recomendadas</span><span class="sxs-lookup"><span data-stu-id="37533-217">Learn about limitations and best practices</span></span>
<span data-ttu-id="37533-218">Atualmente, o Power BI pode ser chamado aproximadamente uma vez por segundo.</span><span class="sxs-lookup"><span data-stu-id="37533-218">Currently, Power BI can be called roughly once per second.</span></span> <span data-ttu-id="37533-219">A transmissão de elementos visuais oferece suporte a pacotes de 15 KB.</span><span class="sxs-lookup"><span data-stu-id="37533-219">Streaming visuals support packets of 15 KB.</span></span> <span data-ttu-id="37533-220">Além disso, o streaming de elementos visuais falha (mas o push continua a funcionar).</span><span class="sxs-lookup"><span data-stu-id="37533-220">Beyond that, streaming visuals fail (but push continues to work).</span></span> <span data-ttu-id="37533-221">Por causa dessas limitações, o Power BI se ajusta bem mais naturalmente nos casos em que a Stream Analytics do Azure faz uma significativa redução de carga de dados.</span><span class="sxs-lookup"><span data-stu-id="37533-221">Because of these limitations, Power BI lends itself most naturally to cases where Azure Stream Analytics does a significant data load reduction.</span></span> <span data-ttu-id="37533-222">É recomendável usar uma janela em cascata ou janela de salto para garantir que o push de dados seja de no máximo um push por segundo e também que sua consulta esteja dentro dos requisitos de produtividade.</span><span class="sxs-lookup"><span data-stu-id="37533-222">We recommend using a Tumbling window or Hopping window to ensure that data push is at most one push per second, and that your query lands within the throughput requirements.</span></span>

<span data-ttu-id="37533-223">Você pode usar a seguinte equação para calcular o valor em segundos dar sua janela:</span><span class="sxs-lookup"><span data-stu-id="37533-223">You can use the following equation to compute the value to give your window in seconds:</span></span>

![Equação1](./media/stream-analytics-power-bi-dashboard/equation1.png)  

<span data-ttu-id="37533-225">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="37533-225">For example:</span></span>

* <span data-ttu-id="37533-226">Você tem 1.000 dispositivos que enviam dados em intervalos de um segundo.</span><span class="sxs-lookup"><span data-stu-id="37533-226">You have 1,000 devices sending data at one-second intervals.</span></span>
* <span data-ttu-id="37533-227">Você está usando o SKU do Power BI Pro que dá suporte a 1.000.000 linhas por hora.</span><span class="sxs-lookup"><span data-stu-id="37533-227">You are using the Power BI Pro SKU that supports 1,000,000 rows per hour.</span></span>
* <span data-ttu-id="37533-228">Você deseja publicar a quantidade de dados médios por dispositivo no Power BI.</span><span class="sxs-lookup"><span data-stu-id="37533-228">You want to publish the amount of average data per device to Power BI.</span></span>

<span data-ttu-id="37533-229">Como resultado, a equação torna-se:</span><span class="sxs-lookup"><span data-stu-id="37533-229">As a result, the equation becomes:</span></span>

![Equação2](./media/stream-analytics-power-bi-dashboard/equation2.png)  

<span data-ttu-id="37533-231">Dada essa configuração, você pode alterar a consulta original para o seguinte:</span><span class="sxs-lookup"><span data-stu-id="37533-231">Given this configuration, you can change the original query to the following:</span></span>

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


### <a name="renew-authorization"></a><span data-ttu-id="37533-232">Renovar autorização</span><span class="sxs-lookup"><span data-stu-id="37533-232">Renew authorization</span></span>
<span data-ttu-id="37533-233">Caso sua senha tenha sido alterada depois de seu trabalho ser criado ou autenticado pela última vez, será necessário autenticar novamente sua conta do Power BI.</span><span class="sxs-lookup"><span data-stu-id="37533-233">If the password has changed since your job was created or last authenticated, you need to reauthenticate your Power BI account.</span></span> <span data-ttu-id="37533-234">Se a Autenticação Multifator estiver configurada no locatário do Azure Active Directory (Azure AD) também será necessário renovar a autorização do Power BI a cada duas semanas.</span><span class="sxs-lookup"><span data-stu-id="37533-234">If Azure Multi-Factor Authentication is configured on your Azure Active Directory (Azure AD) tenant, you also need to renew Power BI authorization every two weeks.</span></span> <span data-ttu-id="37533-235">Se você não renovar, você poderá ver os sintomas, como falta de saída do trabalho ou um `Authenticate user error` nos logs de operação.</span><span class="sxs-lookup"><span data-stu-id="37533-235">If you don't renew, you could see symptoms such as a lack of job output or an `Authenticate user error` in the operation logs.</span></span>

<span data-ttu-id="37533-236">De modo similar, se um trabalho iniciar depois que o token tiver expirado, ocorrerá um erro e o trabalho falhará.</span><span class="sxs-lookup"><span data-stu-id="37533-236">Similarly, if a job starts after the token has expired, an error occurs and the job fails.</span></span> <span data-ttu-id="37533-237">Para resolver esse problema, pare o trabalho em execução e vá para a saída do Power BI.</span><span class="sxs-lookup"><span data-stu-id="37533-237">To resolve this issue, stop the job that's running and go to your Power BI output.</span></span> <span data-ttu-id="37533-238">Para evitar a perda de dados, selecione **Renovar autorização** e reinicie o trabalho a partir da Hora da **Última Interrupção**.</span><span class="sxs-lookup"><span data-stu-id="37533-238">To avoid data loss, select the **Renew authorization** link, and then restart your job from the **Last Stopped Time**.</span></span>

<span data-ttu-id="37533-239">Depois que a autorização foi atualizada com o Power BI, um alerta verde é exibida na área de autorização para refletir se o problema foi resolvido.</span><span class="sxs-lookup"><span data-stu-id="37533-239">After the authorization has been refreshed with Power BI, a green alert appears in the authorization area to reflect that the issue has been resolved.</span></span>

## <a name="get-help"></a><span data-ttu-id="37533-240">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="37533-240">Get help</span></span>
<span data-ttu-id="37533-241">Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="37533-241">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="37533-242">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="37533-242">Next steps</span></span>
* [<span data-ttu-id="37533-243">Introdução ao Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="37533-243">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="37533-244">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="37533-244">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="37533-245">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="37533-245">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="37533-246">Referência de linguagem de consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="37533-246">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="37533-247">Referência da API REST do Gerenciamento do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="37533-247">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
