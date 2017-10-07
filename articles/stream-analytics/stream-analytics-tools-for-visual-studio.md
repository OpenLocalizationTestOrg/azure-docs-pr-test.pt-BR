---
title: "aaaUse ferramentas de análise de fluxo do Azure para Visual Studio | Microsoft Docs"
description: "Tutorial de Introdução para Olá ferramentas de análise de fluxo do Azure para Visual Studio"
keywords: visual studio
documentationcenter: 
services: stream-analytics
author: 
manager: 
editor: 
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 
ms.author: 
ms.openlocfilehash: bda8e548040509a6f29f1b713268bc38f73228fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a><span data-ttu-id="5eb1d-104">Usar Ferramentas do Stream Analytics do Azure para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5eb1d-104">Use Azure Stream Analytics Tools for Visual Studio</span></span>
## <a name="introduction"></a><span data-ttu-id="5eb1d-105">Introdução</span><span class="sxs-lookup"><span data-stu-id="5eb1d-105">Introduction</span></span>
<span data-ttu-id="5eb1d-106">Neste tutorial, você aprenderá como toouse ferramentas de análise de fluxo do Azure para Visual Studio toocreate, criar, testar localmente, gerenciar e depurar os trabalhos do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-106">In this tutorial, you learn how toouse Azure Stream Analytics Tools for Visual Studio toocreate, author, test locally, manage, and debug your Stream Analytics jobs.</span></span> 

<span data-ttu-id="5eb1d-107">Depois de concluir este tutorial, você poderá:</span><span class="sxs-lookup"><span data-stu-id="5eb1d-107">After completing this tutorial, you will be able to:</span></span>
* <span data-ttu-id="5eb1d-108">Familiarize-se com as Ferramentas do Stream Analytics para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-108">Familiarize yourself with Stream Analytics Tools for Visual Studio.</span></span>
* <span data-ttu-id="5eb1d-109">Configurar e implantar um trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-109">Configure and deploy a Stream Analytics job.</span></span>
* <span data-ttu-id="5eb1d-110">Testar seu trabalho local com os dados de exemplo locais.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-110">Test your job locally with local sample data.</span></span>
* <span data-ttu-id="5eb1d-111">Use tootroubleshoot problemas de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-111">Use monitoring tootroubleshoot issues.</span></span>
* <span data-ttu-id="5eb1d-112">Exporte tooprojects de trabalhos existente.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-112">Export existing jobs tooprojects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5eb1d-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5eb1d-113">Prerequisites</span></span>
<span data-ttu-id="5eb1d-114">toocomplete neste tutorial, você precisa Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="5eb1d-114">toocomplete this tutorial, you need hello following prerequisites:</span></span>
* <span data-ttu-id="5eb1d-115">Conclua as etapas de saudação que precedem "Criar um trabalho de análise de fluxo" em Olá [criar uma solução de IoT usando o tutorial de análise de fluxo](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="5eb1d-115">Finish hello steps that precede "Create a Stream Analytics job" in hello [Build an IoT solution by using Stream Analytics tutorial](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span></span> 
* <span data-ttu-id="5eb1d-116">Use o Visual Studio 2015, Visual Studio 2013 Update 4 ou Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-116">Use Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012.</span></span> <span data-ttu-id="5eb1d-117">As edições Enterprise (Ultimate/Premium), Professional, Community têm suporte.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-117">Enterprise (Ultimate/Premium), Professional, and Community editions are supported.</span></span> <span data-ttu-id="5eb1d-118">Não há suporte para a Edição Express.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-118">Express edition is not supported.</span></span> <span data-ttu-id="5eb1d-119">O Visual Studio 2017 não tem suporte.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-119">Visual Studio 2017 is not supported.</span></span> 
* <span data-ttu-id="5eb1d-120">Saudação de uso do Azure SDK para .NET versão 2.7.1 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-120">Use hello Azure SDK for .NET version 2.7.1 or later.</span></span> <span data-ttu-id="5eb1d-121">Instalá-lo usando Olá [instalador de plataforma da Web](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="5eb1d-121">Install it by using hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="5eb1d-122">Instalar Olá [ferramentas de análise de fluxo para o Visual Studio](http://aka.ms/asatoolsvs).</span><span class="sxs-lookup"><span data-stu-id="5eb1d-122">Install hello [Stream Analytics Tools for Visual Studio](http://aka.ms/asatoolsvs).</span></span>

## <a name="create-a-stream-analytics-project"></a><span data-ttu-id="5eb1d-123">Criar um projeto do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5eb1d-123">Create a Stream Analytics project</span></span>
1. <span data-ttu-id="5eb1d-124">No Visual Studio, clique em Olá **arquivo** menu e selecione **novo projeto**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-124">In Visual Studio, click hello **File** menu and select **New Project**.</span></span> 

2. <span data-ttu-id="5eb1d-125">Na lista de modelos Olá Olá esquerda, selecione **do Stream Analytics** e, em seguida, clique em **aplicativo do Azure Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-125">In hello templates list on hello left, select **Stream Analytics** and then click **Azure Stream Analytics Application**.</span></span>

3. <span data-ttu-id="5eb1d-126">Insira o projeto Olá **nome**, **local**, e **nome da solução** como é feito para outros projetos.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-126">Enter hello project **Name**, **Location**, and **Solution name** as you do for other projects.</span></span>

    ![Janela Novo Projeto](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    <span data-ttu-id="5eb1d-128">Um projeto **Pedágio** é gerado no **Gerenciador de Soluções**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-128">A **Toll** project is generated in **Solution Explorer**.</span></span>

    ![Projeto Pedágio gerado no Gerenciador de Soluções](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-hello-correct-subscription"></a><span data-ttu-id="5eb1d-130">Escolha a assinatura correta Olá</span><span class="sxs-lookup"><span data-stu-id="5eb1d-130">Choose hello correct subscription</span></span>
1. <span data-ttu-id="5eb1d-131">No Visual Studio, clique em Olá **exibição** menu e abra **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-131">In Visual Studio, click hello **View** menu and open **Server Explorer**.</span></span>

2. <span data-ttu-id="5eb1d-132">Entre com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-132">Sign in with your Azure Account.</span></span> 

## <a name="define-hello-input-sources"></a><span data-ttu-id="5eb1d-133">Definir fontes de entrada hello</span><span class="sxs-lookup"><span data-stu-id="5eb1d-133">Define hello input sources</span></span>
1.  <span data-ttu-id="5eb1d-134">Em **Solution Explorer**, expanda Olá **entradas** nó e renomear **Input.json** muito**EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-134">In **Solution Explorer**, expand hello **Inputs** node and rename **Input.json** too**EntryStream.json**.</span></span> <span data-ttu-id="5eb1d-135">Clique duas vezes em **EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-135">Double-click **EntryStream.json**.</span></span>
2.  <span data-ttu-id="5eb1d-136">Olá **Alias de entrada** agora é **EntryStream**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-136">hello **Input Alias** is now **EntryStream**.</span></span> <span data-ttu-id="5eb1d-137">saudação de entrada alias é usada no script de consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-137">hello input alias is used in hello query script.</span></span> 
3.  <span data-ttu-id="5eb1d-138">Em **Tipo de Origem**, selecione **Fluxo de Dados**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-138">In **Source Type**, select **Data Stream**.</span></span>
4.  <span data-ttu-id="5eb1d-139">Em **Origem**, selecione **Hub de Eventos**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-139">In **Source**, select **Event Hub**.</span></span>
5.  <span data-ttu-id="5eb1d-140">Em **Namespace de barramento de serviço**, selecione Olá **TollData** opção.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-140">In **Service Bus Namespace**, select hello **TollData** option.</span></span>
6.  <span data-ttu-id="5eb1d-141">Em **Nome do Hub de Eventos**, selecione **entrada**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-141">In **Event Hub Name**, select **entry**.</span></span>
7.  <span data-ttu-id="5eb1d-142">Em **nome de política do Hub de evento**, selecione **RootManageSharedAccessKey** (Olá valor padrão).</span><span class="sxs-lookup"><span data-stu-id="5eb1d-142">In **Event Hub Policy Name**, select **RootManageSharedAccessKey** (hello default value).</span></span>
8.  <span data-ttu-id="5eb1d-143">Em **Formato de Serialização de Evento**, selecione **Json**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-143">In **Event Serialization Format**, select **Json**.</span></span> 
9.  <span data-ttu-id="5eb1d-144">Em **Codificação**, selecione **UTF8**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-144">In **Encoding**, select **UTF8**.</span></span> <span data-ttu-id="5eb1d-145">As configurações devem ser semelhantes Olá captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="5eb1d-145">Your settings should look like hello following screenshot:</span></span>

    ![Janela Entrada](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. <span data-ttu-id="5eb1d-147">Assistente de saudação toofinish, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-147">toofinish hello wizard, click **Save**.</span></span> <span data-ttu-id="5eb1d-148">Agora você pode adicionar outro fluxo de saída do hello toocreate de fonte de entrada.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-148">Now you can add another input source toocreate hello exit stream.</span></span> <span data-ttu-id="5eb1d-149">Saudação de atalho **entradas** nó e selecione **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-149">Right-click hello **Inputs** node, and select **New Item**.</span></span>

    ![Novo Item](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. <span data-ttu-id="5eb1d-151">Na janela de saudação, selecione **entrada do Azure Stream Analytics**e alterar Olá **nome** muito**ExitStream.json**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-151">In hello window, select **Azure Stream Analytics Input**, and change hello **Name** too**ExitStream.json**.</span></span> <span data-ttu-id="5eb1d-152">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-152">Click **Add**.</span></span>

    ![Janela Adicionar Novo Item](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. <span data-ttu-id="5eb1d-154">Clique duas vezes em **ExitStream.json** no projeto hello e siga Olá mesmas etapas de fluxo de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-154">Double-click **ExitStream.json** in hello project, and follow hello same steps as you did for hello entry stream.</span></span> <span data-ttu-id="5eb1d-155">Ser tooenter se **sair** para Olá **nome do Hub de evento** conforme Olá captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="5eb1d-155">Be sure tooenter **exit** for hello **Event Hub Name** as shown in hello following screenshot:</span></span>

    ![Janela ExitStream](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    <span data-ttu-id="5eb1d-157">Agora você definiu dois fluxos de entrada:</span><span class="sxs-lookup"><span data-stu-id="5eb1d-157">Now you have defined two input streams:</span></span>

    ![Fluxos de recebimento de entrada e saída](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    <span data-ttu-id="5eb1d-159">Em seguida, adicione a entrada de dados de referência para o arquivo de blob de saudação que contém dados de registro de carro.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-159">Next, add reference data input for hello blob file that contains car registration data.</span></span>

13. <span data-ttu-id="5eb1d-160">Saudação de atalho **entradas** nó no projeto de saudação e, em seguida, siga Olá mesmas etapas de entradas de fluxo de saudação.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-160">Right-click hello **Inputs** node in hello project, and then follow hello same steps as you did for hello stream inputs.</span></span> <span data-ttu-id="5eb1d-161">Em **Alias de Entrada**, digite **Registro** e em **Tipo de Origem**, selecione **Dados de referência**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-161">In **Input Alias**, enter **Registration**, and in **Source Type**, select **Reference data**.</span></span>

    ![Janela Registro](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. <span data-ttu-id="5eb1d-163">Em **conta de armazenamento**, selecione Olá **tolldata** opção.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-163">In **Storage Account**, select hello **tolldata** option.</span></span> <span data-ttu-id="5eb1d-164">Em **Contêiner**, selecione **tolldata** e, em **Padrão de Caminho**, digite **registration.json**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-164">In **Container**, select **tolldata**, and in **Path Pattern**, enter **registration.json**.</span></span> <span data-ttu-id="5eb1d-165">Este nome de arquivo diferencia maiúsculas de minúsculas e deve estar em minúsculas.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-165">This file name is case sensitive and should be lowercase.</span></span>
15. <span data-ttu-id="5eb1d-166">Assistente de saudação toofinish, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-166">toofinish hello wizard, click **Save**.</span></span>

<span data-ttu-id="5eb1d-167">Agora, todas as entradas de saudação são definidas.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-167">Now all hello inputs are defined.</span></span>

## <a name="define-hello-output"></a><span data-ttu-id="5eb1d-168">Definir a saída de hello</span><span class="sxs-lookup"><span data-stu-id="5eb1d-168">Define hello output</span></span>
1.  <span data-ttu-id="5eb1d-169">Em **Solution Explorer**, expanda Olá **entradas** nó e clique duas vezes em **Output.json**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-169">In **Solution Explorer**, expand hello **Inputs** node and double-click **Output.json**.</span></span>

2.  <span data-ttu-id="5eb1d-170">Em **Alias de Saída**, digite **saída**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-170">In **Output Alias**, enter **output**.</span></span> 
3.  <span data-ttu-id="5eb1d-171">Em **Coletor**, selecione **Banco de Dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-171">In **Sink**, select **SQL Database**.</span></span>
4.  <span data-ttu-id="5eb1d-172">Em **Banco de Dados**, selecione **TollDataDB**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-172">In **Database**, select **TollDataDB**.</span></span>
5.  <span data-ttu-id="5eb1d-173">Em **Nome de Usuário**, digite **tolladmin**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-173">In **User Name**, enter **tolladmin**.</span></span> 
6.  <span data-ttu-id="5eb1d-174">Em **Senha**, digite **123toll!**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-174">In **Password**, enter **123toll!**.</span></span>
7.  <span data-ttu-id="5eb1d-175">Em **Tabela**, digite **TollDataRefJoin**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-175">In **Table**, enter **TollDataRefJoin**.</span></span>
8.  <span data-ttu-id="5eb1d-176">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-176">Click **Save**.</span></span>

    ![Janela de Saída](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a><span data-ttu-id="5eb1d-178">Criar uma consulta do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5eb1d-178">Create a Stream Analytics query</span></span>
<span data-ttu-id="5eb1d-179">Este tutorial tentativas tooanswer várias questões comerciais que são dados tootoll relacionados.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-179">This tutorial attempts tooanswer several business questions that are related tootoll data.</span></span> <span data-ttu-id="5eb1d-180">Ele também cria consultas de análise de fluxo que podem ser usadas em respostas relevantes do Stream Analytics tooprovide.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-180">It also constructs Stream Analytics queries that can be used in Stream Analytics tooprovide relevant answers.</span></span>
<span data-ttu-id="5eb1d-181">Antes de iniciar o trabalho do Stream Analytics primeiro, vamos explorar uma sintaxe de consulta simple do cenário e hello.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-181">Before you start your first Stream Analytics job, let’s explore a simple scenario and hello query syntax.</span></span>

### <a name="introduction-toohello-stream-analytics-query-language"></a><span data-ttu-id="5eb1d-182">Introdução toohello linguagem de consulta do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5eb1d-182">Introduction toohello Stream Analytics query language</span></span>
<span data-ttu-id="5eb1d-183">Digamos que você precisa que o número de saudação toocount dos veículos que insere um pedágio.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-183">Let’s say that you need toocount hello number of vehicles that enter a toll booth.</span></span> <span data-ttu-id="5eb1d-184">Como este exemplo é um fluxo contínuo de eventos, é preciso toodefine um período de tempo.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-184">Because this example is a continuous stream of events, you have toodefine a period of time.</span></span> <span data-ttu-id="5eb1d-185">Modificar Olá pergunta toobe "quantos veículos inserir um pedágio a cada três minutos?"</span><span class="sxs-lookup"><span data-stu-id="5eb1d-185">Modify hello question toobe “How many vehicles enter a toll booth every three minutes?”</span></span> <span data-ttu-id="5eb1d-186">Este toocount de maneira dados geralmente são chamado tooas Olá em cascata de contagem.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-186">This way toocount data is commonly referred tooas hello tumbling count.</span></span>

<span data-ttu-id="5eb1d-187">Examine a consulta de análise de fluxo de saudação que responde a essa pergunta:</span><span class="sxs-lookup"><span data-stu-id="5eb1d-187">Look at hello Stream Analytics query that answers this question:</span></span>

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

<span data-ttu-id="5eb1d-188">O Stream Analytics usa uma linguagem de consulta como SQL e adiciona algumas extensões toospecify tempo aspectos relacionados à consulta hello.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-188">Stream Analytics uses a query language that's like SQL and adds a few extensions toospecify time-related aspects of hello query.</span></span>

<span data-ttu-id="5eb1d-189">Para obter mais informações, consulte [gerenciamento de tempo](https://msdn.microsoft.com/library/azure/mt582045.aspx) e [janelas](https://msdn.microsoft.com/library/azure/dn835019.aspx) construções usadas na consulta de saudação do MSDN.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-189">For more information, see [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructs used in hello query from MSDN.</span></span>

<span data-ttu-id="5eb1d-190">Agora que você escreveu a primeira consulta de análise de fluxo, é hora tootest-lo.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-190">Now that you have written your first Stream Analytics query, it's time tootest it.</span></span> <span data-ttu-id="5eb1d-191">Use arquivos de dados de exemplo hello localizados na pasta TollApp no Olá que caminho a seguir:</span><span class="sxs-lookup"><span data-stu-id="5eb1d-191">Use hello sample data files located in your TollApp folder in hello following path:</span></span>

<span data-ttu-id="5eb1d-192">..\TollApp\TollApp\Data</span><span class="sxs-lookup"><span data-stu-id="5eb1d-192">..\TollApp\TollApp\Data</span></span>

<span data-ttu-id="5eb1d-193">Esta pasta contém Olá seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="5eb1d-193">This folder contains hello following files:</span></span>
*   <span data-ttu-id="5eb1d-194">Entry.json</span><span class="sxs-lookup"><span data-stu-id="5eb1d-194">Entry.json</span></span>
*   <span data-ttu-id="5eb1d-195">Exit.JSON</span><span class="sxs-lookup"><span data-stu-id="5eb1d-195">Exit.json</span></span>
*   <span data-ttu-id="5eb1d-196">registration.json</span><span class="sxs-lookup"><span data-stu-id="5eb1d-196">Registration.json</span></span>

## <a name="count-hello-number-of-vehicles-entering-a-toll-booth"></a><span data-ttu-id="5eb1d-197">Número de saudação de contagem de veículos inserindo um pedágio</span><span class="sxs-lookup"><span data-stu-id="5eb1d-197">Count hello number of vehicles entering a toll booth</span></span>
<span data-ttu-id="5eb1d-198">No projeto de saudação, clique duas vezes em **Script.asaql** tooopen script Olá Olá **Editor de consultas**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-198">In hello project, double-click **Script.asaql** tooopen hello script in hello **Query Editor**.</span></span> <span data-ttu-id="5eb1d-199">Copie e cole o script hello na seção anterior Olá no editor de hello.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-199">Copy and paste hello script in hello previous section into hello editor.</span></span> <span data-ttu-id="5eb1d-200">Olá Editor de consultas oferece suporte a IntelliSense, a coloração de sintaxe e marcador de saudação de erro.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-200">hello Query Editor supports IntelliSense, syntax coloring, and hello error marker.</span></span>

![Editor de Consultas](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a><span data-ttu-id="5eb1d-202">Testar as consultas do Stream Analytics localmente</span><span class="sxs-lookup"><span data-stu-id="5eb1d-202">Test Stream Analytics queries locally</span></span>

1. <span data-ttu-id="5eb1d-203">toocompile Olá consulta toosee se houver um erro de sintaxe, clique com botão direito hello e selecione **criar**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-203">toocompile hello query toosee if there is a syntax error, right-click hello project and select **Build**.</span></span> 

2. <span data-ttu-id="5eb1d-204">toovalidate esta consulta em relação a dados de exemplo, você pode usar dados de exemplo do local.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-204">toovalidate this query against sample data, you can use local sample data.</span></span> <span data-ttu-id="5eb1d-205">Entrada hello e selecione **Adicionar entrada local**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-205">Right-click hello input, and select **Add local input**.</span></span>

    ![Adicionar entrada local](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. <span data-ttu-id="5eb1d-207">Na janela pop-up do hello, selecione os dados de exemplo hello do caminho local.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-207">In hello pop-up window, select hello sample data from your local path.</span></span> <span data-ttu-id="5eb1d-208">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-208">Click **Save**.</span></span>

    ![Janela Adicionar entrada local](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    <span data-ttu-id="5eb1d-210">Um arquivo chamado **local_EntryStream.json** é adicionada automaticamente a pasta de entradas de tooyour.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-210">A file named **local_EntryStream.json** is automatically added tooyour inputs folder.</span></span>

    ![Pasta do arquivo de inclusão tooinputs](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. <span data-ttu-id="5eb1d-212">Em Olá **Editor de consultas**, clique em **executado localmente**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-212">In hello **Query Editor**, click **Run Locally**.</span></span> <span data-ttu-id="5eb1d-213">Ou você pode pressionar a tecla F5 de saudação.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-213">Or you can press hello F5 key.</span></span>

    ![Executar Localmente](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![Saída de execução local](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    <span data-ttu-id="5eb1d-216">Pressione qualquer saída de hello tooview chave no hello **resultados de execução Local ASA** janela no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-216">Press any key tooview hello output in hello **ASA Local Run Result** window in Visual Studio.</span></span> 

    ![Janela Resultado da Execução Local de ASA](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. <span data-ttu-id="5eb1d-218">Clique em **Abrir pasta resultado** arquivos de saída de hello toocheck ambos no formato CSV e JSON.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-218">Click **Open Result Folder** toocheck hello output files both in CSV and JSON format.</span></span>

    ![Saída de Abrir a Pasta de Resultados](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-hello-input-data"></a><span data-ttu-id="5eb1d-220">Dados de entrada do exemplo hello</span><span class="sxs-lookup"><span data-stu-id="5eb1d-220">Sample hello input data</span></span>
<span data-ttu-id="5eb1d-221">Você também pode dados de entrada de exemplo do arquivo local de tooa de fontes de entrada.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-221">You can also sample input data from input sources tooa local file.</span></span> 
1. <span data-ttu-id="5eb1d-222">Arquivo de configuração de entrada hello e selecione **dados de exemplo**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-222">Right-click hello input config file, and select **Sample Data**.</span></span> 

   ![Dados de exemplo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    <span data-ttu-id="5eb1d-224">Você pode fazer amostragem apenas do Hub de Eventos ou do Hub IoT, por enquanto.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-224">You can sample only event hub or IoT hub for now.</span></span> <span data-ttu-id="5eb1d-225">Não há suporte para outras fontes de entrada.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-225">Other input sources are not supported.</span></span>

2. <span data-ttu-id="5eb1d-226">Na janela pop-up do hello, inserir dados de exemplo de saudação do hello caminho local usado toosave.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-226">In hello pop-up window, enter hello local path used toosave hello sample data.</span></span> <span data-ttu-id="5eb1d-227">Clique em **Exemplo**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-227">Click **Sample**.</span></span>

    ![Janela Dados de Exemplo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    <span data-ttu-id="5eb1d-229">Você pode ver o progresso de saudação em Olá **saída** janela.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-229">You can see hello progress in hello **Output** window.</span></span> 

    ![Janela de Saída](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-tooazure"></a><span data-ttu-id="5eb1d-231">Enviar um tooAzure de consulta do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5eb1d-231">Submit a Stream Analytics query tooAzure</span></span>
1. <span data-ttu-id="5eb1d-232">Em Olá **Editor de consultas**, clique em **enviar tooAzure** no editor de script hello.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-232">In hello **Query Editor**, click **Submit tooAzure** in hello script editor.</span></span>

    ![Enviar tooAzure](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. <span data-ttu-id="5eb1d-234">Selecione **Criar um Novo Trabalho do Stream Analytics do Azure**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-234">Select **Create a New Azure Stream Analytics Job**.</span></span> <span data-ttu-id="5eb1d-235">Digite hello **nome do trabalho**e selecione hello correto **assinatura**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-235">Enter hello **Job Name**, and select hello correct **Subscription**.</span></span> <span data-ttu-id="5eb1d-236">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-236">Click **Submit**.</span></span>

    ![Janela Enviar Trabalho](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a><span data-ttu-id="5eb1d-238">Iniciar um trabalho</span><span class="sxs-lookup"><span data-stu-id="5eb1d-238">Start a job</span></span>
<span data-ttu-id="5eb1d-239">Agora que o trabalho é criado, exibição de trabalho Olá é aberta automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-239">Now that your job is created, hello job view is automatically opened.</span></span> 
1. <span data-ttu-id="5eb1d-240">Olá toostart de trabalho, clique em Olá **seta verde** botão.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-240">toostart hello job, click hello **green arrow** button.</span></span>

    ![Iniciar um trabalho](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. <span data-ttu-id="5eb1d-242">Selecione a configuração padrão de saudação e, em seguida, clique em **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-242">Select hello default setting, and click **Start**.</span></span>
 
    ![Janela Iniciar Trabalho](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    <span data-ttu-id="5eb1d-244">trabalho de saudação **Status** muda muito**executando**, e **eventos de entrada** e **eventos de saída** aparecer.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-244">hello job **Status** changes too**Running**, and **Input Events** and **Output Events** appear.</span></span>

    ![Status Em Execução no Resumo do Trabalho](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-hello-results-in-visual-studio"></a><span data-ttu-id="5eb1d-246">Resultados da verificação Olá no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5eb1d-246">Check hello results in Visual Studio</span></span>
1. <span data-ttu-id="5eb1d-247">No Visual Studio, abra **Server Explorer** e com o botão direito hello **TollDataRefJoin** tabela.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-247">In Visual Studio, open **Server Explorer** and right-click hello **TollDataRefJoin** table.</span></span>
2. <span data-ttu-id="5eb1d-248">Selecione **Mostrar dados da tabela** toosee saída de saudação do seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-248">Select **Show Table Data** toosee hello output of your job.</span></span>
   
    ![Seleção de Mostrar Dados da Tabela no Gerenciador de Servidores](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-hello-job-metrics"></a><span data-ttu-id="5eb1d-250">Exibição Olá trabalho métricas</span><span class="sxs-lookup"><span data-stu-id="5eb1d-250">View hello job metrics</span></span>
<span data-ttu-id="5eb1d-251">Algumas estatísticas básicas de trabalho podem ser encontradas em **Métricas do Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-251">Some basic job statistics can be found in **Job Metrics**.</span></span> 

![Janela Métricas de Trabalho](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-hello-job-in-server-explorer"></a><span data-ttu-id="5eb1d-253">Trabalho de saudação de lista no Gerenciador de servidores</span><span class="sxs-lookup"><span data-stu-id="5eb1d-253">List hello job in Server Explorer</span></span>
<span data-ttu-id="5eb1d-254">No **Gerenciador de Servidores**, clique em **Trabalhos do Stream Analytics** e clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-254">In **Server Explorer**, click **Stream Analytics Jobs** and then click **Refresh**.</span></span> <span data-ttu-id="5eb1d-255">trabalho de saudação aparece sob **trabalhos do Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-255">hello job appears under **Stream Analytics jobs**.</span></span>

![Trabalhos do Stream Analytics listados no Gerenciador de Servidores](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-hello-job-view"></a><span data-ttu-id="5eb1d-257">Exibição de trabalho Olá aberto</span><span class="sxs-lookup"><span data-stu-id="5eb1d-257">Open hello job view</span></span>
<span data-ttu-id="5eb1d-258">exibição de trabalho Olá tooopen, expanda o nó do trabalho e clique duas vezes Olá **exibição trabalho** nó.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-258">tooopen hello job view, expand your job node and double-click hello **Job View** node.</span></span>

![Nó Exibição de Trabalho](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-tooa-project"></a><span data-ttu-id="5eb1d-260">Exportar um projeto existente de tooa de trabalho</span><span class="sxs-lookup"><span data-stu-id="5eb1d-260">Export an existing job tooa project</span></span>
<span data-ttu-id="5eb1d-261">Há duas maneiras que você pode exportar um projeto de tooa de trabalho existente.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-261">There are two ways you can export an existing job tooa project.</span></span>

<span data-ttu-id="5eb1d-262">Em **Server Explorer**, nó de trabalho de saudação com o botão direito no hello **trabalhos do Stream Analytics** nó e selecione **exportar tooNew projeto de análise de fluxo**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-262">In **Server Explorer**, right-click hello job node in hello **Stream Analytics Jobs** node and select **Export tooNew Stream Analytics Project**.</span></span>

![Exportar tooNew projeto de análise de fluxo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

<span data-ttu-id="5eb1d-264">projeto de saudação é gerado no **Gerenciador de soluções**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-264">hello project is generated in **Solution Explorer**.</span></span>

![Projeto gerado no Gerenciador de Soluções](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
<span data-ttu-id="5eb1d-266">Você também pode usar o modo de exibição do hello trabalho e clique em **projeto gerar**.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-266">You also can use hello job view, and click **Generate Project**.</span></span>

![Gerar Projeto](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a><span data-ttu-id="5eb1d-268">Problemas e limitações conhecidos</span><span class="sxs-lookup"><span data-stu-id="5eb1d-268">Known issues and limitations</span></span>
 
- <span data-ttu-id="5eb1d-269">Não há suporte para a saída do Power BI e a saída do Azure Date Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-269">There is no support for Power BI output and Azure Date Lake Store output.</span></span>
- <span data-ttu-id="5eb1d-270">Não há suporte do editor para adicionar ou alterar funções definidas pelo usuário de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5eb1d-270">There is no editor support for adding or changing JavaScript user-defined functions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5eb1d-271">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5eb1d-271">Next steps</span></span>
* [<span data-ttu-id="5eb1d-272">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5eb1d-272">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="5eb1d-273">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="5eb1d-273">Get started by using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="5eb1d-274">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="5eb1d-274">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="5eb1d-275">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="5eb1d-275">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="5eb1d-276">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5eb1d-276">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
