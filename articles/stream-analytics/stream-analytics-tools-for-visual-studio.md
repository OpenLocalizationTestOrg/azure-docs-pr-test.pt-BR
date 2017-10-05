---
title: Usar Ferramentas do Stream Analytics do Azure para Visual Studio | Microsoft Docs
description: "Tutorial de introdução para as Ferramentas do Stream Analytics do Azure para Visual Studio"
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
ms.openlocfilehash: 618c1055795a75e0ed71dacddba3e076f81f4946
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a><span data-ttu-id="29fc3-104">Usar Ferramentas do Stream Analytics do Azure para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="29fc3-104">Use Azure Stream Analytics Tools for Visual Studio</span></span>
## <a name="introduction"></a><span data-ttu-id="29fc3-105">Introdução</span><span class="sxs-lookup"><span data-stu-id="29fc3-105">Introduction</span></span>
<span data-ttu-id="29fc3-106">Neste tutorial, você aprenderá como usar as Ferramentas do Stream Analytics do Azure para Visual Studio para criar, testar localmente, gerenciar e depurar os trabalhos do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="29fc3-106">In this tutorial, you learn how to use Azure Stream Analytics Tools for Visual Studio to create, author, test locally, manage, and debug your Stream Analytics jobs.</span></span> 

<span data-ttu-id="29fc3-107">Depois de concluir este tutorial, você poderá:</span><span class="sxs-lookup"><span data-stu-id="29fc3-107">After completing this tutorial, you will be able to:</span></span>
* <span data-ttu-id="29fc3-108">Familiarize-se com as Ferramentas do Stream Analytics para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="29fc3-108">Familiarize yourself with Stream Analytics Tools for Visual Studio.</span></span>
* <span data-ttu-id="29fc3-109">Configurar e implantar um trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="29fc3-109">Configure and deploy a Stream Analytics job.</span></span>
* <span data-ttu-id="29fc3-110">Testar seu trabalho local com os dados de exemplo locais.</span><span class="sxs-lookup"><span data-stu-id="29fc3-110">Test your job locally with local sample data.</span></span>
* <span data-ttu-id="29fc3-111">Use o monitoramento para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="29fc3-111">Use monitoring to troubleshoot issues.</span></span>
* <span data-ttu-id="29fc3-112">Exportar os trabalhos existentes para projetos.</span><span class="sxs-lookup"><span data-stu-id="29fc3-112">Export existing jobs to projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29fc3-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="29fc3-113">Prerequisites</span></span>
<span data-ttu-id="29fc3-114">Para concluir este tutorial, você precisará dos seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="29fc3-114">To complete this tutorial, you need the following prerequisites:</span></span>
* <span data-ttu-id="29fc3-115">Conclua as etapas anteriores a "Criar um trabalho de Stream Analytics" no [tutorial Criar uma solução de IoT usando o Stream Analytics](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="29fc3-115">Finish the steps that precede "Create a Stream Analytics job" in the [Build an IoT solution by using Stream Analytics tutorial](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span></span> 
* <span data-ttu-id="29fc3-116">Use o Visual Studio 2015, Visual Studio 2013 Update 4 ou Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="29fc3-116">Use Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012.</span></span> <span data-ttu-id="29fc3-117">As edições Enterprise (Ultimate/Premium), Professional, Community têm suporte.</span><span class="sxs-lookup"><span data-stu-id="29fc3-117">Enterprise (Ultimate/Premium), Professional, and Community editions are supported.</span></span> <span data-ttu-id="29fc3-118">Não há suporte para a Edição Express.</span><span class="sxs-lookup"><span data-stu-id="29fc3-118">Express edition is not supported.</span></span> <span data-ttu-id="29fc3-119">O Visual Studio 2017 não tem suporte.</span><span class="sxs-lookup"><span data-stu-id="29fc3-119">Visual Studio 2017 is not supported.</span></span> 
* <span data-ttu-id="29fc3-120">Use o SDK do Azure para .NET versão 2.7.1 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="29fc3-120">Use the Azure SDK for .NET version 2.7.1 or later.</span></span> <span data-ttu-id="29fc3-121">Instale-o usando o [Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="29fc3-121">Install it by using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="29fc3-122">Instale as [Ferramentas do Stream Analytics para Visual Studio](http://aka.ms/asatoolsvs).</span><span class="sxs-lookup"><span data-stu-id="29fc3-122">Install the [Stream Analytics Tools for Visual Studio](http://aka.ms/asatoolsvs).</span></span>

## <a name="create-a-stream-analytics-project"></a><span data-ttu-id="29fc3-123">Criar um projeto do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="29fc3-123">Create a Stream Analytics project</span></span>
1. <span data-ttu-id="29fc3-124">No Visual Studio, clique no menu **Arquivo** e selecione **Novo Projeto**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-124">In Visual Studio, click the **File** menu and select **New Project**.</span></span> 

2. <span data-ttu-id="29fc3-125">Na lista de modelos à esquerda, selecione **Stream Analytics** e clique em **Aplicativo do Stream Analytics do Azure**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-125">In the templates list on the left, select **Stream Analytics** and then click **Azure Stream Analytics Application**.</span></span>

3. <span data-ttu-id="29fc3-126">Insira o **Nome** do projeto, a **Localização** e o **Nome da solução** na parte inferior, como faria para outros projetos.</span><span class="sxs-lookup"><span data-stu-id="29fc3-126">Enter the project **Name**, **Location**, and **Solution name** as you do for other projects.</span></span>

    ![Janela Novo Projeto](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    <span data-ttu-id="29fc3-128">Um projeto **Pedágio** é gerado no **Gerenciador de Soluções**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-128">A **Toll** project is generated in **Solution Explorer**.</span></span>

    ![Projeto Pedágio gerado no Gerenciador de Soluções](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-the-correct-subscription"></a><span data-ttu-id="29fc3-130">Escolha a assinatura correta</span><span class="sxs-lookup"><span data-stu-id="29fc3-130">Choose the correct subscription</span></span>
1. <span data-ttu-id="29fc3-131">No Visual Studio, clique em **Exibir** no menu e abra **Gerenciador de Servidores**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-131">In Visual Studio, click the **View** menu and open **Server Explorer**.</span></span>

2. <span data-ttu-id="29fc3-132">Entre com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="29fc3-132">Sign in with your Azure Account.</span></span> 

## <a name="define-the-input-sources"></a><span data-ttu-id="29fc3-133">Definir as fontes de entrada</span><span class="sxs-lookup"><span data-stu-id="29fc3-133">Define the input sources</span></span>
1.  <span data-ttu-id="29fc3-134">Em **Gerenciador de Soluções**, expanda o nó **Entradas** e renomeie **Input.json** para **EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-134">In **Solution Explorer**, expand the **Inputs** node and rename **Input.json** to **EntryStream.json**.</span></span> <span data-ttu-id="29fc3-135">Clique duas vezes em **EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-135">Double-click **EntryStream.json**.</span></span>
2.  <span data-ttu-id="29fc3-136">O **Alias de Entrada** agora é **EntryStream**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-136">The **Input Alias** is now **EntryStream**.</span></span> <span data-ttu-id="29fc3-137">O alias de entrada é usado no script de consulta.</span><span class="sxs-lookup"><span data-stu-id="29fc3-137">The input alias is used in the query script.</span></span> 
3.  <span data-ttu-id="29fc3-138">Em **Tipo de Origem**, selecione **Fluxo de Dados**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-138">In **Source Type**, select **Data Stream**.</span></span>
4.  <span data-ttu-id="29fc3-139">Em **Origem**, selecione **Hub de Eventos**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-139">In **Source**, select **Event Hub**.</span></span>
5.  <span data-ttu-id="29fc3-140">No **Namespace do Barramento de Serviço**, selecione a opção **TollData**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-140">In **Service Bus Namespace**, select the **TollData** option.</span></span>
6.  <span data-ttu-id="29fc3-141">Em **Nome do Hub de Eventos**, selecione **entrada**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-141">In **Event Hub Name**, select **entry**.</span></span>
7.  <span data-ttu-id="29fc3-142">Em **Nome da Política do Hub de Eventos**, selecione é **RootManageSharedAccessKey** (o valor padrão).</span><span class="sxs-lookup"><span data-stu-id="29fc3-142">In **Event Hub Policy Name**, select **RootManageSharedAccessKey** (the default value).</span></span>
8.  <span data-ttu-id="29fc3-143">Em **Formato de Serialização de Evento**, selecione **Json**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-143">In **Event Serialization Format**, select **Json**.</span></span> 
9.  <span data-ttu-id="29fc3-144">Em **Codificação**, selecione **UTF8**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-144">In **Encoding**, select **UTF8**.</span></span> <span data-ttu-id="29fc3-145">Suas configurações devem ter aparência semelhante à captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="29fc3-145">Your settings should look like the following screenshot:</span></span>

    ![Janela Entrada](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. <span data-ttu-id="29fc3-147">Para concluir o assistente, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-147">To finish the wizard, click **Save**.</span></span> <span data-ttu-id="29fc3-148">Agora você pode adicionar outra fonte de entrada para criar o fluxo de saída.</span><span class="sxs-lookup"><span data-stu-id="29fc3-148">Now you can add another input source to create the exit stream.</span></span> <span data-ttu-id="29fc3-149">Clique com o botão direito do mouse no nó **Entradas** e selecione **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-149">Right-click the **Inputs** node, and select **New Item**.</span></span>

    ![Novo Item](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. <span data-ttu-id="29fc3-151">Na janela exibida, selecione **Entrada do Stream Analytics do Azure** e altere o **Nome** para **ExitStream.json**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-151">In the window, select **Azure Stream Analytics Input**, and change the **Name** to **ExitStream.json**.</span></span> <span data-ttu-id="29fc3-152">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-152">Click **Add**.</span></span>

    ![Janela Adicionar Novo Item](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. <span data-ttu-id="29fc3-154">Clique duas vezes em **ExitStream.json** no projeto e siga as mesmas etapas usadas para o fluxo de entrada.</span><span class="sxs-lookup"><span data-stu-id="29fc3-154">Double-click **ExitStream.json** in the project, and follow the same steps as you did for the entry stream.</span></span> <span data-ttu-id="29fc3-155">Lembre-se de inserir **saída** para o **Nome do Hub de Eventos**, conforme mostrado na captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="29fc3-155">Be sure to enter **exit** for the **Event Hub Name** as shown in the following screenshot:</span></span>

    ![Janela ExitStream](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    <span data-ttu-id="29fc3-157">Agora você definiu dois fluxos de entrada:</span><span class="sxs-lookup"><span data-stu-id="29fc3-157">Now you have defined two input streams:</span></span>

    ![Fluxos de recebimento de entrada e saída](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    <span data-ttu-id="29fc3-159">Em seguida, adicione a entrada de dados de referência para o arquivo de blob que contém os dados de registro do carro.</span><span class="sxs-lookup"><span data-stu-id="29fc3-159">Next, add reference data input for the blob file that contains car registration data.</span></span>

13. <span data-ttu-id="29fc3-160">Clique com botão direito do mouse no nó **Entradas** no projeto e, em seguida, siga as mesmas etapas usadas para as entradas de fluxo.</span><span class="sxs-lookup"><span data-stu-id="29fc3-160">Right-click the **Inputs** node in the project, and then follow the same steps as you did for the stream inputs.</span></span> <span data-ttu-id="29fc3-161">Em **Alias de Entrada**, digite **Registro** e em **Tipo de Origem**, selecione **Dados de referência**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-161">In **Input Alias**, enter **Registration**, and in **Source Type**, select **Reference data**.</span></span>

    ![Janela Registro](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. <span data-ttu-id="29fc3-163">Em **Conta de Armazenamento**, selecione a opção **tolldata**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-163">In **Storage Account**, select the **tolldata** option.</span></span> <span data-ttu-id="29fc3-164">Em **Contêiner**, selecione **tolldata** e, em **Padrão de Caminho**, digite **registration.json**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-164">In **Container**, select **tolldata**, and in **Path Pattern**, enter **registration.json**.</span></span> <span data-ttu-id="29fc3-165">Este nome de arquivo diferencia maiúsculas de minúsculas e deve estar em minúsculas.</span><span class="sxs-lookup"><span data-stu-id="29fc3-165">This file name is case sensitive and should be lowercase.</span></span>
15. <span data-ttu-id="29fc3-166">Para concluir o assistente, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-166">To finish the wizard, click **Save**.</span></span>

<span data-ttu-id="29fc3-167">Agora, todas as entradas estão definidas.</span><span class="sxs-lookup"><span data-stu-id="29fc3-167">Now all the inputs are defined.</span></span>

## <a name="define-the-output"></a><span data-ttu-id="29fc3-168">Definir a saída</span><span class="sxs-lookup"><span data-stu-id="29fc3-168">Define the output</span></span>
1.  <span data-ttu-id="29fc3-169">No **Gerenciador de Soluções**, expanda o nó **Entradas** e clique duas vezes em **Output.json**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-169">In **Solution Explorer**, expand the **Inputs** node and double-click **Output.json**.</span></span>

2.  <span data-ttu-id="29fc3-170">Em **Alias de Saída**, digite **saída**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-170">In **Output Alias**, enter **output**.</span></span> 
3.  <span data-ttu-id="29fc3-171">Em **Coletor**, selecione **Banco de Dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-171">In **Sink**, select **SQL Database**.</span></span>
4.  <span data-ttu-id="29fc3-172">Em **Banco de Dados**, selecione **TollDataDB**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-172">In **Database**, select **TollDataDB**.</span></span>
5.  <span data-ttu-id="29fc3-173">Em **Nome de Usuário**, digite **tolladmin**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-173">In **User Name**, enter **tolladmin**.</span></span> 
6.  <span data-ttu-id="29fc3-174">Em **Senha**, digite **123toll!**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-174">In **Password**, enter **123toll!**.</span></span>
7.  <span data-ttu-id="29fc3-175">Em **Tabela**, digite **TollDataRefJoin**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-175">In **Table**, enter **TollDataRefJoin**.</span></span>
8.  <span data-ttu-id="29fc3-176">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-176">Click **Save**.</span></span>

    ![Janela de Saída](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a><span data-ttu-id="29fc3-178">Criar uma consulta do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="29fc3-178">Create a Stream Analytics query</span></span>
<span data-ttu-id="29fc3-179">Este tutorial tenta responder várias perguntas comerciais relacionadas a dados de pedágio.</span><span class="sxs-lookup"><span data-stu-id="29fc3-179">This tutorial attempts to answer several business questions that are related to toll data.</span></span> <span data-ttu-id="29fc3-180">Ele também constrói consultas do Stream Analytics que podem ser usadas no Stream Analytics para fornecer respostas relevantes.</span><span class="sxs-lookup"><span data-stu-id="29fc3-180">It also constructs Stream Analytics queries that can be used in Stream Analytics to provide relevant answers.</span></span>
<span data-ttu-id="29fc3-181">Antes de você começar seu primeiro trabalho do Stream Analytics, exploraremos um cenário simples e a sintaxe de consulta.</span><span class="sxs-lookup"><span data-stu-id="29fc3-181">Before you start your first Stream Analytics job, let’s explore a simple scenario and the query syntax.</span></span>

### <a name="introduction-to-the-stream-analytics-query-language"></a><span data-ttu-id="29fc3-182">Introdução à linguagem de consulta do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="29fc3-182">Introduction to the Stream Analytics query language</span></span>
<span data-ttu-id="29fc3-183">Digamos que você precise contar o número de veículos que entram em uma cabine de pedágio.</span><span class="sxs-lookup"><span data-stu-id="29fc3-183">Let’s say that you need to count the number of vehicles that enter a toll booth.</span></span> <span data-ttu-id="29fc3-184">Como este exemplo se trata de um fluxo contínuo de eventos, você precisa definir um período de tempo.</span><span class="sxs-lookup"><span data-stu-id="29fc3-184">Because this example is a continuous stream of events, you have to define a period of time.</span></span> <span data-ttu-id="29fc3-185">Modifique a pergunta para "Quantos veículos entram em uma cabine de pedágio a cada três minutos?"</span><span class="sxs-lookup"><span data-stu-id="29fc3-185">Modify the question to be “How many vehicles enter a toll booth every three minutes?”</span></span> <span data-ttu-id="29fc3-186">Esse modo de contar dados é conhecido como contagem em cascata.</span><span class="sxs-lookup"><span data-stu-id="29fc3-186">This way to count data is commonly referred to as the tumbling count.</span></span>

<span data-ttu-id="29fc3-187">Veja a consulta do Stream Analytics que responde a essa pergunta:</span><span class="sxs-lookup"><span data-stu-id="29fc3-187">Look at the Stream Analytics query that answers this question:</span></span>

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

<span data-ttu-id="29fc3-188">O Stream Analytics usa uma linguagem de consulta parecida com SQL e adiciona algumas extensões para especificar aspectos da consulta relacionados ao tempo.</span><span class="sxs-lookup"><span data-stu-id="29fc3-188">Stream Analytics uses a query language that's like SQL and adds a few extensions to specify time-related aspects of the query.</span></span>

<span data-ttu-id="29fc3-189">Para obter mais informações, veja as construções de [Gerenciamento de Tempo](https://msdn.microsoft.com/library/azure/mt582045.aspx) e de [Janela](https://msdn.microsoft.com/library/azure/dn835019.aspx) usadas na consulta no MSDN.</span><span class="sxs-lookup"><span data-stu-id="29fc3-189">For more information, see [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructs used in the query from MSDN.</span></span>

<span data-ttu-id="29fc3-190">Agora que você escreveu sua primeira consulta do Stream Analytics, é hora de testá-la.</span><span class="sxs-lookup"><span data-stu-id="29fc3-190">Now that you have written your first Stream Analytics query, it's time to test it.</span></span> <span data-ttu-id="29fc3-191">Use os arquivos de dados de exemplo localizados na pasta TollApp no seguinte caminho:</span><span class="sxs-lookup"><span data-stu-id="29fc3-191">Use the sample data files located in your TollApp folder in the following path:</span></span>

<span data-ttu-id="29fc3-192">..\TollApp\TollApp\Data</span><span class="sxs-lookup"><span data-stu-id="29fc3-192">..\TollApp\TollApp\Data</span></span>

<span data-ttu-id="29fc3-193">Esta pasta contém os seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="29fc3-193">This folder contains the following files:</span></span>
*   <span data-ttu-id="29fc3-194">Entry.json</span><span class="sxs-lookup"><span data-stu-id="29fc3-194">Entry.json</span></span>
*   <span data-ttu-id="29fc3-195">Exit.JSON</span><span class="sxs-lookup"><span data-stu-id="29fc3-195">Exit.json</span></span>
*   <span data-ttu-id="29fc3-196">registration.json</span><span class="sxs-lookup"><span data-stu-id="29fc3-196">Registration.json</span></span>

## <a name="count-the-number-of-vehicles-entering-a-toll-booth"></a><span data-ttu-id="29fc3-197">Contar o número de veículos que entram em uma cabine de pedágio</span><span class="sxs-lookup"><span data-stu-id="29fc3-197">Count the number of vehicles entering a toll booth</span></span>
<span data-ttu-id="29fc3-198">No projeto, clique duas vezes em **Script.asaql** para abrir o script no **Editor de Consultas**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-198">In the project, double-click **Script.asaql** to open the script in the **Query Editor**.</span></span> <span data-ttu-id="29fc3-199">Copie e cole o script na seção anterior no editor.</span><span class="sxs-lookup"><span data-stu-id="29fc3-199">Copy and paste the script in the previous section into the editor.</span></span> <span data-ttu-id="29fc3-200">O Editor de Consultas dá suporte ao IntelliSense, a uso de cores de sintaxe e ao marcador de erro.</span><span class="sxs-lookup"><span data-stu-id="29fc3-200">The Query Editor supports IntelliSense, syntax coloring, and the error marker.</span></span>

![Editor de Consultas](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a><span data-ttu-id="29fc3-202">Testar as consultas do Stream Analytics localmente</span><span class="sxs-lookup"><span data-stu-id="29fc3-202">Test Stream Analytics queries locally</span></span>

1. <span data-ttu-id="29fc3-203">Para compilar a consulta para ver se há algum erro de sintaxe, clique com o botão direito do mouse no projeto e selecione **Compilar**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-203">To compile the query to see if there is a syntax error, right-click the project and select **Build**.</span></span> 

2. <span data-ttu-id="29fc3-204">Para validar essa consulta em relação aos dados de exemplo, você pode usar dados de exemplo locais.</span><span class="sxs-lookup"><span data-stu-id="29fc3-204">To validate this query against sample data, you can use local sample data.</span></span> <span data-ttu-id="29fc3-205">Clique com o botão direito do mouse na entrada e selecione **Adicionar entrada local**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-205">Right-click the input, and select **Add local input**.</span></span>

    ![Adicionar entrada local](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. <span data-ttu-id="29fc3-207">Na janela pop-up, selecione os dados de exemplo do caminho local.</span><span class="sxs-lookup"><span data-stu-id="29fc3-207">In the pop-up window, select the sample data from your local path.</span></span> <span data-ttu-id="29fc3-208">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-208">Click **Save**.</span></span>

    ![Janela Adicionar entrada local](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    <span data-ttu-id="29fc3-210">Um arquivo chamado **local_EntryStream.json** é adicionado automaticamente à pasta de entradas.</span><span class="sxs-lookup"><span data-stu-id="29fc3-210">A file named **local_EntryStream.json** is automatically added to your inputs folder.</span></span>

    ![Arquivo adicionado à pasta de entradas](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. <span data-ttu-id="29fc3-212">No **Editor de Consultas**, clique em **Executar Localmente**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-212">In the **Query Editor**, click **Run Locally**.</span></span> <span data-ttu-id="29fc3-213">Ou você pode pressionar a tecla F5.</span><span class="sxs-lookup"><span data-stu-id="29fc3-213">Or you can press the F5 key.</span></span>

    ![Executar Localmente](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![Saída de execução local](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    <span data-ttu-id="29fc3-216">Pressione qualquer tecla para exibir a saída na janela **Resultado da Execução Local de ASA** no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="29fc3-216">Press any key to view the output in the **ASA Local Run Result** window in Visual Studio.</span></span> 

    ![Janela Resultado da Execução Local de ASA](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. <span data-ttu-id="29fc3-218">Clique em **Abrir a Pasta de Resultados** para verificar os arquivos de saída nos formatos CSV e JSON.</span><span class="sxs-lookup"><span data-stu-id="29fc3-218">Click **Open Result Folder** to check the output files both in CSV and JSON format.</span></span>

    ![Saída de Abrir a Pasta de Resultados](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-the-input-data"></a><span data-ttu-id="29fc3-220">Amostrar os dados de entrada</span><span class="sxs-lookup"><span data-stu-id="29fc3-220">Sample the input data</span></span>
<span data-ttu-id="29fc3-221">Você também pode realizar a amostragem de dados de entrada de fontes de entrada para um arquivo local.</span><span class="sxs-lookup"><span data-stu-id="29fc3-221">You can also sample input data from input sources to a local file.</span></span> 
1. <span data-ttu-id="29fc3-222">Clique com o botão direito do mouse no arquivo de configuração de entrada e selecione **Dados de Exemplo**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-222">Right-click the input config file, and select **Sample Data**.</span></span> 

   ![Dados de exemplo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    <span data-ttu-id="29fc3-224">Você pode fazer amostragem apenas do Hub de Eventos ou do Hub IoT, por enquanto.</span><span class="sxs-lookup"><span data-stu-id="29fc3-224">You can sample only event hub or IoT hub for now.</span></span> <span data-ttu-id="29fc3-225">Não há suporte para outras fontes de entrada.</span><span class="sxs-lookup"><span data-stu-id="29fc3-225">Other input sources are not supported.</span></span>

2. <span data-ttu-id="29fc3-226">Na janela pop-up, digite o caminho local usado para salvar os dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="29fc3-226">In the pop-up window, enter the local path used to save the sample data.</span></span> <span data-ttu-id="29fc3-227">Clique em **Exemplo**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-227">Click **Sample**.</span></span>

    ![Janela Dados de Exemplo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    <span data-ttu-id="29fc3-229">Você pode ver o andamento na janela de **Saída**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-229">You can see the progress in the **Output** window.</span></span> 

    ![Janela de Saída](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-to-azure"></a><span data-ttu-id="29fc3-231">Enviar uma consulta do Stream Analytics para o Azure</span><span class="sxs-lookup"><span data-stu-id="29fc3-231">Submit a Stream Analytics query to Azure</span></span>
1. <span data-ttu-id="29fc3-232">No **Editor de Consultas**, clique em **Enviar para o Azure** no editor de scripts.</span><span class="sxs-lookup"><span data-stu-id="29fc3-232">In the **Query Editor**, click **Submit To Azure** in the script editor.</span></span>

    ![Enviar para o Azure](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. <span data-ttu-id="29fc3-234">Selecione **Criar um Novo Trabalho do Stream Analytics do Azure**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-234">Select **Create a New Azure Stream Analytics Job**.</span></span> <span data-ttu-id="29fc3-235">Insira o **Nome do Trabalho** e selecione a **Assinatura** correta.</span><span class="sxs-lookup"><span data-stu-id="29fc3-235">Enter the **Job Name**, and select the correct **Subscription**.</span></span> <span data-ttu-id="29fc3-236">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-236">Click **Submit**.</span></span>

    ![Janela Enviar Trabalho](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a><span data-ttu-id="29fc3-238">Iniciar um trabalho</span><span class="sxs-lookup"><span data-stu-id="29fc3-238">Start a job</span></span>
<span data-ttu-id="29fc3-239">Agora que o trabalho foi criado, a exibição de trabalho é aberta automaticamente.</span><span class="sxs-lookup"><span data-stu-id="29fc3-239">Now that your job is created, the job view is automatically opened.</span></span> 
1. <span data-ttu-id="29fc3-240">Para iniciar o trabalho, clique no botão com a **seta verde**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-240">To start the job, click the **green arrow** button.</span></span>

    ![Iniciar um trabalho](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. <span data-ttu-id="29fc3-242">Selecione a configuração padrão e clique em **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-242">Select the default setting, and click **Start**.</span></span>
 
    ![Janela Iniciar Trabalho](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    <span data-ttu-id="29fc3-244">O **Status** do trabalho é alterado para **Em Execução** e **Eventos de Entrada** e **Eventos de Saída** aparecem.</span><span class="sxs-lookup"><span data-stu-id="29fc3-244">The job **Status** changes to **Running**, and **Input Events** and **Output Events** appear.</span></span>

    ![Status Em Execução no Resumo do Trabalho](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-the-results-in-visual-studio"></a><span data-ttu-id="29fc3-246">Verificar os resultados no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="29fc3-246">Check the results in Visual Studio</span></span>
1. <span data-ttu-id="29fc3-247">No Visual Studio, abra o **Gerenciador de Servidores** e clique com o botão direito do mouse na tabela **TollDataRefJoin**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-247">In Visual Studio, open **Server Explorer** and right-click the **TollDataRefJoin** table.</span></span>
2. <span data-ttu-id="29fc3-248">Selecione **Mostrar Dados da Tabela** para ver a saída do seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="29fc3-248">Select **Show Table Data** to see the output of your job.</span></span>
   
    ![Seleção de Mostrar Dados da Tabela no Gerenciador de Servidores](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-the-job-metrics"></a><span data-ttu-id="29fc3-250">Exibir as métricas de trabalho</span><span class="sxs-lookup"><span data-stu-id="29fc3-250">View the job metrics</span></span>
<span data-ttu-id="29fc3-251">Algumas estatísticas básicas de trabalho podem ser encontradas em **Métricas do Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-251">Some basic job statistics can be found in **Job Metrics**.</span></span> 

![Janela Métricas de Trabalho](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-the-job-in-server-explorer"></a><span data-ttu-id="29fc3-253">Listar o trabalho no Gerenciador de Servidores</span><span class="sxs-lookup"><span data-stu-id="29fc3-253">List the job in Server Explorer</span></span>
<span data-ttu-id="29fc3-254">No **Gerenciador de Servidores**, clique em **Trabalhos do Stream Analytics** e clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-254">In **Server Explorer**, click **Stream Analytics Jobs** and then click **Refresh**.</span></span> <span data-ttu-id="29fc3-255">O trabalho é exibido em **Trabalhos do Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-255">The job appears under **Stream Analytics jobs**.</span></span>

![Trabalhos do Stream Analytics listados no Gerenciador de Servidores](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-the-job-view"></a><span data-ttu-id="29fc3-257">Abrir a exibição do trabalho</span><span class="sxs-lookup"><span data-stu-id="29fc3-257">Open the job view</span></span>
<span data-ttu-id="29fc3-258">Para abrir a exibição de trabalho, expanda o nó do trabalho e clique duas vezes no nó **Exibição de Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-258">To open the job view, expand your job node and double-click the **Job View** node.</span></span>

![Nó Exibição de Trabalho](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-to-a-project"></a><span data-ttu-id="29fc3-260">Exportar um trabalho existente para um projeto</span><span class="sxs-lookup"><span data-stu-id="29fc3-260">Export an existing job to a project</span></span>
<span data-ttu-id="29fc3-261">Há duas maneiras que você pode usar para exportar um trabalho para um projeto.</span><span class="sxs-lookup"><span data-stu-id="29fc3-261">There are two ways you can export an existing job to a project.</span></span>

<span data-ttu-id="29fc3-262">No **Gerenciador de Servidores**, clique com o botão direito do mouse no nó de trabalho no nó **Trabalhos do Stream Analytics** e selecione **Exportar para um Novo Projeto do Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-262">In **Server Explorer**, right-click the job node in the **Stream Analytics Jobs** node and select **Export to New Stream Analytics Project**.</span></span>

![Exportar para um novo projeto do Stream Analytics](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

<span data-ttu-id="29fc3-264">O projeto é gerado no **Gerenciador de Soluções**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-264">The project is generated in **Solution Explorer**.</span></span>

![Projeto gerado no Gerenciador de Soluções](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
<span data-ttu-id="29fc3-266">Você também pode usar a exibição de trabalho e clicar em **Gerar Projeto**.</span><span class="sxs-lookup"><span data-stu-id="29fc3-266">You also can use the job view, and click **Generate Project**.</span></span>

![Gerar Projeto](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a><span data-ttu-id="29fc3-268">Problemas e limitações conhecidos</span><span class="sxs-lookup"><span data-stu-id="29fc3-268">Known issues and limitations</span></span>
 
- <span data-ttu-id="29fc3-269">Não há suporte para a saída do Power BI e a saída do Azure Date Lake Store.</span><span class="sxs-lookup"><span data-stu-id="29fc3-269">There is no support for Power BI output and Azure Date Lake Store output.</span></span>
- <span data-ttu-id="29fc3-270">Não há suporte do editor para adicionar ou alterar funções definidas pelo usuário de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="29fc3-270">There is no editor support for adding or changing JavaScript user-defined functions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29fc3-271">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="29fc3-271">Next steps</span></span>
* [<span data-ttu-id="29fc3-272">Introdução ao Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="29fc3-272">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="29fc3-273">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="29fc3-273">Get started by using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="29fc3-274">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="29fc3-274">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="29fc3-275">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="29fc3-275">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="29fc3-276">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="29fc3-276">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
