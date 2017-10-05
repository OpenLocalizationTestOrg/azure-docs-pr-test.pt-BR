---
title: "Análise de Sentimento do Twitter em tempo real com o Stream Analytics do Azure | Microsoft Docs"
description: "Saiba como usar a Stream Analytics para análise de sentimento Twitter em tempo real. Orientações passo a passo de geração de eventos aos dados em um painel em tempo real."
keywords: "análise de tendência do twitter em tempo real, análise de sentimento, análise de mídia social, exemplo de análise de tendência"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42068691-074b-4c3b-a527-acafa484fda2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: jeffstok
ms.openlocfilehash: 8de6850964700f5b3f71d144b40af927f2e52d7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="real-time-twitter-sentiment-analysis-in-azure-stream-analytics"></a><span data-ttu-id="e3bd6-105">Análise de sentimento do Twitter em tempo real no Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="e3bd6-105">Real-time Twitter sentiment analysis in Azure Stream Analytics</span></span>

<span data-ttu-id="e3bd6-106">Aprenda a compilar uma solução de análise de sentimento para análise de mídia social colocando os eventos em tempo real do Twitter nos Hubs de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-106">Learn how to build a sentiment analysis solution for social media analytics by bringing real-time Twitter events into Azure Event Hubs.</span></span> <span data-ttu-id="e3bd6-107">Você pode então gravar uma consulta Azure Stream Analytics para analisar os dados e ou armazenar os resultados para uso posterior ou usar um painel e [Power BI](https://powerbi.com/) para fornecer insights em tempo real.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-107">You can then write an Azure Stream Analytics query to analyze the data and either store the results for later use or use a dashboard and [Power BI](https://powerbi.com/) to provide insights in real time.</span></span>

<span data-ttu-id="e3bd6-108">As ferramentas de análise de mídias sociais ajudam as organizações a compreender os tópicos mais populares.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-108">Social media analytics tools help organizations understand trending topics.</span></span> <span data-ttu-id="e3bd6-109">Os tópicos mais populares são entidades e atitudes com um alto volume de postagens em mídia social.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-109">Trending topics are subjects and attitudes that have a high volume of posts in social media.</span></span> <span data-ttu-id="e3bd6-110">A análise de sentimento, também chamada de *mineração opinião*, usa as ferramentas de análise de mídia social para determinar as atitudes em direção a um produto, ideia e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-110">Sentiment analysis, which is also called *opinion mining*, uses social media analytics tools to determine attitudes toward a product, idea, and so on.</span></span> 

<span data-ttu-id="e3bd6-111">A análise de tendência do Twitter em tempo real é um ótimo exemplo de uma ferramenta analítica, porque o modelo de assinatura com hashtag permite que você escute palavras-chave específicas (hashtags) e desenvolva a análise de sentimento no feed.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-111">Real-time Twitter trend analysis is a great example of an analytics tool, because the hashtag subscription model enables you to listen to specific keywords (hashtags) and develop sentiment analysis of the feed.</span></span>

## <a name="scenario-social-media-sentiment-analysis-in-real-time"></a><span data-ttu-id="e3bd6-112">Cenário: Análise de sentimento de mídia social em tempo real</span><span class="sxs-lookup"><span data-stu-id="e3bd6-112">Scenario: Social media sentiment analysis in real time</span></span>

<span data-ttu-id="e3bd6-113">Uma empresa com um site de mídia de notícias está interessada em obter uma vantagem sobre seus concorrentes apresentando conteúdo do site imediatamente relevante para seus leitores.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-113">A company that has a news media website is interested in gaining an advantage over its competitors by featuring site content that is immediately relevant to its readers.</span></span> <span data-ttu-id="e3bd6-114">A empresa usa a análise de mídia social sobre os tópicos relevantes para seus leitores, fazendo uma análise de sentimento em tempo real nos dados do Twitter.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-114">The company uses social media analysis on topics that are relevant to readers by doing real-time sentiment analysis of Twitter data.</span></span>

<span data-ttu-id="e3bd6-115">Para identificar os tópicos em destaque em tempo real no Twitter, a empresa precisa de análise em tempo real sobre o volume de tweets e de sentimento para os tópicos principais.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-115">To identify trending topics in real time on Twitter, the company needs real-time analytics about the tweet volume and sentiment for key topics.</span></span> <span data-ttu-id="e3bd6-116">Em outras palavras, eles precisam de um mecanismo de análise para análise de sentimento baseado nesse feed de mídia social.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-116">In other words, the need is a sentiment analysis analytics engine that's based on this social media feed.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3bd6-117">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e3bd6-117">Prerequisites</span></span>
<span data-ttu-id="e3bd6-118">Neste tutorial, você deve usar um aplicativo cliente que se conecta ao Twitter e procura tweets com determinados hashtags (que podem ser definidos).</span><span class="sxs-lookup"><span data-stu-id="e3bd6-118">In this tutorial, you use a client application that connects to Twitter and looks for tweets that have certain hashtags (which you can set).</span></span> <span data-ttu-id="e3bd6-119">Para executar o aplicativo e analisar os tweets usando o Azure Streaming Analytics, você deve ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e3bd6-119">In order to run the application and analyze the tweets using Azure Streaming Analytics, you must have the following:</span></span>

* <span data-ttu-id="e3bd6-120">Uma assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="e3bd6-120">An Azure subscription</span></span>
* <span data-ttu-id="e3bd6-121">Uma conta do Twitter</span><span class="sxs-lookup"><span data-stu-id="e3bd6-121">A Twitter account</span></span> 
* <span data-ttu-id="e3bd6-122">Um aplicativo do Twitter e o [token de acesso OAuth](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-122">A Twitter application, and the [OAuth access token](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) for that application.</span></span> <span data-ttu-id="e3bd6-123">Nós fornecemos instruções de alto nível sobre como criar um aplicativo do Twitter mais tarde.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-123">We provide high-level instructions for how to create a Twitter application later.</span></span>
* <span data-ttu-id="e3bd6-124">O aplicativo TwitterWPFClient, que lê o feed do Twitter.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-124">The TwitterWPFClient application, which reads the Twitter feed.</span></span> <span data-ttu-id="e3bd6-125">Para obter esse aplicativo, baixe o arquivo [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) do GitHub e, em seguida, descompacte o pacote em uma pasta no seu computador.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-125">To get this application, download the [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) file from GitHub and then unzip the package into a folder on your computer.</span></span> <span data-ttu-id="e3bd6-126">Se você quiser ver código-fonte e executar o aplicativo em um depurador, você pode obter o código-fonte do [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator).</span><span class="sxs-lookup"><span data-stu-id="e3bd6-126">If you want to see the source code and run the application in a debugger, you can get the source code from [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator).</span></span> 

## <a name="create-an-event-hub-for-streaming-analytics-input"></a><span data-ttu-id="e3bd6-127">Criar um hub de eventos para entrada do Streaming Analytics</span><span class="sxs-lookup"><span data-stu-id="e3bd6-127">Create an event hub for Streaming Analytics input</span></span>

<span data-ttu-id="e3bd6-128">O aplicativo de exemplo gera eventos e empurra eles para um hub de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-128">The sample application generates events and pushes them to an Azure event hub.</span></span> <span data-ttu-id="e3bd6-129">Os Hubs de Eventos do Azure são o método preferencial de ingestão de eventos para Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-129">Azure event hubs are the preferred method of event ingestion for Stream Analytics.</span></span> <span data-ttu-id="e3bd6-130">Para obter mais informações, consulte a [documentação dos Hubs de Evento do Azure](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="e3bd6-130">For more information, see the [Azure Event Hubs documentation](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>


### <a name="create-an-event-hub-namespace-and-event-hub"></a><span data-ttu-id="e3bd6-131">Criar um namespace de hub de eventos e um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="e3bd6-131">Create an event hub namespace and event hub</span></span>
<span data-ttu-id="e3bd6-132">Neste procedimento, você primeiro cria um namespace de hub de eventos e, em seguida, adiciona um hub de eventos para esse namespace.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-132">In this procedure, you first create an event hub namespace, and then you add an event hub to that namespace.</span></span> <span data-ttu-id="e3bd6-133">Namespaces do hub de evento são usados para agrupar logicamente instâncias de barramento de evento relacionadas.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-133">Event hub namespaces are used to logically group related event bus instances.</span></span> 

1. <span data-ttu-id="e3bd6-134">Registre-se no Portal do Azure e clique em **Novo** > **Internet das Coisas** > **Hub de Evento**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-134">Log  in to the Azure portal and click **New** > **Internet of Things** > **Event Hub**.</span></span> 

2. <span data-ttu-id="e3bd6-135">Na folha **Criar um namespace**, insira um nome de namespace como `<yourname>-socialtwitter-eh-ns`.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-135">In the **Create namespace** blade, enter a namespace name such as `<yourname>-socialtwitter-eh-ns`.</span></span> <span data-ttu-id="e3bd6-136">Você pode usar qualquer nome para o namespace, mas o nome deve ser válido para uma URL e deve ser exclusivo no Azure.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-136">You can use any name for the namespace, but the name must be valid for a URL and it must be unique across Azure.</span></span> 
    
3. <span data-ttu-id="e3bd6-137">Selecione uma assinatura e crie ou escolha um grupo de recursos e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-137">Select a subscription and create or choose a resource group, then click **Create**.</span></span> 

    ![Criar um namespace do hub de eventos](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-namespace.png)
 
4. <span data-ttu-id="e3bd6-139">Quando o namespace acabar a implementação, localize o namespace de hub de eventos na lista de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-139">When the namespace has finished deploying, find the event hub namespace in your list of Azure resources.</span></span> 

5. <span data-ttu-id="e3bd6-140">Clique em novo namespace e, na folha do namespace, clique em **+&nbsp;Hub de eventos**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-140">Click the new namespace, and in the namespace blade, click **+&nbsp;Event Hub**.</span></span> 

    ![<span data-ttu-id="e3bd6-141">Botão Adicionar Hub de Eventos para criar um novo hub de eventos</span><span class="sxs-lookup"><span data-stu-id="e3bd6-141">The Add Event Hub button for creating a new event hub</span></span> ](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-button.png)    
 
6. <span data-ttu-id="e3bd6-142">Nomeie o novo hub de evento `socialtwitter-eh`.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-142">Name the new event hub `socialtwitter-eh`.</span></span> <span data-ttu-id="e3bd6-143">Você pode usar um nome diferente.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-143">You can use a different name.</span></span> <span data-ttu-id="e3bd6-144">Se você fizer isso, anote-o, pois você precisará desse nome mais tarde.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-144">If you do, make a note of it, because you need the name later.</span></span> <span data-ttu-id="e3bd6-145">Você não precisa definir outras opções para o hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-145">You don't need to set any other options for the event hub.</span></span>

    ![Folha para a criação de um novo hub de eventos](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub.png)
 
7. <span data-ttu-id="e3bd6-147">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-147">Click **Create**.</span></span>


### <a name="grant-access-to-the-event-hub"></a><span data-ttu-id="e3bd6-148">Conceder acesso para o hub de eventos</span><span class="sxs-lookup"><span data-stu-id="e3bd6-148">Grant access to the event hub</span></span>

<span data-ttu-id="e3bd6-149">Antes que um processo possa enviar dados para um hub de eventos, o hub de eventos deve ter uma política que permita o acesso apropriado.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-149">Before a process can send data to an event hub, the event hub must have a policy that allows appropriate access.</span></span> <span data-ttu-id="e3bd6-150">A política de acesso produz uma cadeia de conexão que inclui informações de autorização.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-150">The access policy produces a connection string that includes authorization information.</span></span>

1.  <span data-ttu-id="e3bd6-151">Na folha de namespace de evento, clique em **Hubs de Eventos** e, em seguida, clique no nome do seu novo Hub de Eventos.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-151">In the event namespace blade, click **Event Hubs** and then click the name of your new event hub.</span></span>

2.  <span data-ttu-id="e3bd6-152">Na folha de Hub de Eventos, clique em **Políticas de acesso compartilhado** e depois em **+&nbsp;Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-152">In the event hub blade, click **Shared access policies** and then click **+&nbsp;Add**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="e3bd6-153">Verifique se você está trabalhando com o hub de eventos, não com o namespace de hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-153">Make sure you're working with the event hub, not the event hub namespace.</span></span>

3.  <span data-ttu-id="e3bd6-154">Adicione uma política chamada `socialtwitter-access` e para **Declaração**, selecione **Gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-154">Add a policy named `socialtwitter-access` and for **Claim**, select **Manage**.</span></span>

    ![Folha para a criação de uma nova política de acesso de hub de eventos](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-shared-access-policy-manage.png)
 
4.  <span data-ttu-id="e3bd6-156">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-156">Click **Create**.</span></span>

5.  <span data-ttu-id="e3bd6-157">Depois que a política for implementada, clique na lista de políticas de acesso compartilhado.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-157">After the policy has been deployed, click it in the list of shared access policies.</span></span>

6.  <span data-ttu-id="e3bd6-158">Localize a caixa rotulada **CHAVE PRIMÁRIA DA CADEIA DE CONEXÃO** e clique no botão de cópia próximo à cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-158">Find the box labeled **CONNECTION STRING-PRIMARY KEY** and click the copy button next to the connection string.</span></span> 
    
    ![Copiando a chave de cadeia de cadeia de conexão primária da política de acesso](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-shared-access-policy-copy-connection-string.png)
 
7.  <span data-ttu-id="e3bd6-160">Cole a cadeia de conexão em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-160">Paste the connection string into a text editor.</span></span> <span data-ttu-id="e3bd6-161">Você precisa dessa cadeia de conexão para a próxima seção, depois que você fizer algumas pequenas modificações.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-161">You need this connection string for the next section, after you make some small edits to it.</span></span>

    <span data-ttu-id="e3bd6-162">A cadeia de conexão tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="e3bd6-162">The connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=;EntityPath=socialtwitter-eh

    <span data-ttu-id="e3bd6-163">Observe que a cadeia de conexão contém vários pares de chave-valor, separados por ponto e vírgula: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, e `EntityPath`.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-163">Notice that the connection string contains multiple key-value pairs, separated with semicolons: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, and `EntityPath`.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="e3bd6-164">Por segurança, partes da cadeia de conexão do exemplo foram removidas.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-164">For security, parts of the connection string in the example have been removed.</span></span>

8.  <span data-ttu-id="e3bd6-165">No editor de texto, remova o `EntityPath` par da cadeia de conexão (não se esqueça de remover o ponto e vírgula anterior).</span><span class="sxs-lookup"><span data-stu-id="e3bd6-165">In the text editor, remove the `EntityPath` pair from the connection string (don't forget to remove the semicolon that precedes it).</span></span> <span data-ttu-id="e3bd6-166">Quando você terminar, a cadeia de conexão terá esta aparência:</span><span class="sxs-lookup"><span data-stu-id="e3bd6-166">When you're done, the connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=


## <a name="configure-and-start-the-twitter-client-application"></a><span data-ttu-id="e3bd6-167">Configurar e iniciar o aplicativo de cliente do Twitter</span><span class="sxs-lookup"><span data-stu-id="e3bd6-167">Configure and start the Twitter client application</span></span>
<span data-ttu-id="e3bd6-168">O aplicativo cliente obtém eventos de tweet diretamente do Twitter.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-168">The client application gets tweet events directly from Twitter.</span></span> <span data-ttu-id="e3bd6-169">Para fazer isso, ele precisa de permissão para chamar as APIs de Streaming do Twitter.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-169">In order to do so, it needs permission to call the Twitter Streaming APIs.</span></span> <span data-ttu-id="e3bd6-170">Para configurar essa permissão, você pode criar um aplicativo no Twitter que gere as credenciais exclusivas (por exemplo, um token OAuth).</span><span class="sxs-lookup"><span data-stu-id="e3bd6-170">To configure that permission, you create an application in Twitter, which generates unique credentials (such as an OAuth token).</span></span> <span data-ttu-id="e3bd6-171">Você pode configurar o aplicativo de cliente para usar essas credenciais ao fazer chamadas à API.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-171">You can then configure the client application to use these credentials when it makes API calls.</span></span> 

### <a name="create-a-twitter-application"></a><span data-ttu-id="e3bd6-172">Criar um aplicativo do Twitter</span><span class="sxs-lookup"><span data-stu-id="e3bd6-172">Create a Twitter application</span></span>
<span data-ttu-id="e3bd6-173">Se você ainda não tiver um aplicativo do Twitter que você possa usar para este tutorial, você pode criar um.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-173">If you do not already have a Twitter application that you can use for this tutorial, you can create one.</span></span> <span data-ttu-id="e3bd6-174">Você já deve ter uma conta do Twitter.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-174">You must already have a Twitter account.</span></span>

> [!NOTE]
> <span data-ttu-id="e3bd6-175">O processo exato no Twitter para criar um aplicativo e obter o token, as chaves e segredos pode mudar.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-175">The exact process in Twitter for creating an application and getting the keys, secrets, and token might change.</span></span> <span data-ttu-id="e3bd6-176">Se essas instruções não corresponderem ao que você vê no site do Twitter, consulte a documentação do desenvolvedor do Twitter.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-176">If these instructions don't match what you see on the Twitter site, refer to the Twitter developer documentation.</span></span>

1. <span data-ttu-id="e3bd6-177">Vá para a [página de gerenciamento de aplicativo do Twitter](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="e3bd6-177">Go to the [Twitter application management page](https://apps.twitter.com/).</span></span> 

2. <span data-ttu-id="e3bd6-178">Crie um aplicativo novo.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-178">Create a new application.</span></span> 

    * <span data-ttu-id="e3bd6-179">Para a URL do site, especifique uma URL válida.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-179">For the website URL, specify a valid URL.</span></span> <span data-ttu-id="e3bd6-180">Ele não precisa ser um site ativo.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-180">It does not have to be a live site.</span></span> <span data-ttu-id="e3bd6-181">(Você não pode especificar apenas `localhost`.)</span><span class="sxs-lookup"><span data-stu-id="e3bd6-181">(You can't specify just `localhost`.)</span></span>
    * <span data-ttu-id="e3bd6-182">Deixe o campo de retorno de chamada em branco.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-182">Leave the callback field blank.</span></span> <span data-ttu-id="e3bd6-183">O aplicativo cliente que você usar para este tutorial não requer retornos de chamada.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-183">The client application you use for this tutorial doesn't require callbacks.</span></span>

    ![Criando um aplicativo no Twitter](./media/stream-analytics-twitter-sentiment-analysis-trends/create-twitter-application.png)

3. <span data-ttu-id="e3bd6-185">Opcionalmente, altere as permissões do aplicativo para somente leitura.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-185">Optionally, change the application's permissions to read-only.</span></span>

4. <span data-ttu-id="e3bd6-186">Quando o aplicativo for criado, clique na página **Chaves e Tokens de acesso**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-186">When the application is created, go to the **Keys and Access Tokens** page.</span></span>

5. <span data-ttu-id="e3bd6-187">Clique no botão para gerar um token de acesso e um segredo de token de acesso.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-187">Click the button to generate an access token and access token secret.</span></span>

<span data-ttu-id="e3bd6-188">Mantenha essas informações em mãos, pois você precisará delas no próximo procedimento.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-188">Keep this information handy, because you will need it in the next procedure.</span></span>

>[!NOTE]
><span data-ttu-id="e3bd6-189">As chaves e segredos do aplicativo Twitter fornecem acesso à sua conta do Twitter.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-189">The keys and secrets for the Twitter application provide access to your Twitter account.</span></span> <span data-ttu-id="e3bd6-190">Trate essas informações como confidenciais, o mesmo faça com sua senha do Twitter.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-190">Treat this information as sensitive, the same as you do your Twitter password.</span></span> <span data-ttu-id="e3bd6-191">Por exemplo, não insira essas informações em um aplicativo que você forneça a outras pessoas.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-191">For example, don't embed this information in an application that you give to others.</span></span> 


### <a name="configure-the-client-application"></a><span data-ttu-id="e3bd6-192">Configurar o aplicativo do cliente</span><span class="sxs-lookup"><span data-stu-id="e3bd6-192">Configure the client application</span></span>
<span data-ttu-id="e3bd6-193">Nós criamos um aplicativo de cliente que se conecta aos dados do Twitter por meio das [APIs de Streaming do Twitter](https://dev.twitter.com/streaming/overview) para coletar eventos de Tweets sobre um conjunto específico de tópicos.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-193">We've created a client application that connects to Twitter data using [Twitter's Streaming APIs](https://dev.twitter.com/streaming/overview) to collect tweet events about a specific set of topics.</span></span> <span data-ttu-id="e3bd6-194">O aplicativo usa a ferramenta de código aberto [Sentiment140](http://help.sentiment140.com/), que atribui o seguinte valor de sentimento para cada tweet:</span><span class="sxs-lookup"><span data-stu-id="e3bd6-194">The application uses the [Sentiment140](http://help.sentiment140.com/) open source tool, which assigns the following sentiment value to each tweet:</span></span>

* <span data-ttu-id="e3bd6-195">0 = negativo</span><span class="sxs-lookup"><span data-stu-id="e3bd6-195">0 = negative</span></span>
* <span data-ttu-id="e3bd6-196">2 = neutro</span><span class="sxs-lookup"><span data-stu-id="e3bd6-196">2 = neutral</span></span>
* <span data-ttu-id="e3bd6-197">4 = positivo</span><span class="sxs-lookup"><span data-stu-id="e3bd6-197">4 = positive</span></span>

<span data-ttu-id="e3bd6-198">Depois que um valor de sentimento foi atribuído aos eventos de tweet, eles são enviados para o hub de eventos que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-198">After the tweet events have been assigned a sentiment value, they are pushed to the event hub that you created earlier.</span></span>

<span data-ttu-id="e3bd6-199">Antes do aplicativo ser executado, ele requer certas informações, como as chaves do Twitter e a cadeia de conexão de hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-199">Before the application runs, it requires certain information from you, like the Twitter keys and the event hub connection string.</span></span> <span data-ttu-id="e3bd6-200">Você pode fornecer as informações de configuração das seguintes maneiras:</span><span class="sxs-lookup"><span data-stu-id="e3bd6-200">You can provide the configuration information in these ways:</span></span>

* <span data-ttu-id="e3bd6-201">Execute o aplicativo e, em seguida, use a interface de usuário do aplicativo para inserir a cadeia de conexão, as chaves e os segredos.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-201">Run the application, and then use the application's UI to enter the keys, secrets, and connection string.</span></span> <span data-ttu-id="e3bd6-202">Se você fizer isso, as informações de configuração são usadas para a sessão atual, mas não serão salvas.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-202">If you do this, the configuration information is used for your current session, but it isn't saved.</span></span>
* <span data-ttu-id="e3bd6-203">Edite o arquivo de configuração do aplicativo e defina os valores de lá.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-203">Edit the application's .config file and set the values there.</span></span> <span data-ttu-id="e3bd6-204">Essa abordagem persiste as informações de configuração, mas isso também significa que essas informações potencialmente confidenciais são armazenadas em texto sem formatação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-204">This approach persists the configuration information, but it also means that this potentially sensitive information is stored in plain text on your computer.</span></span>

<span data-ttu-id="e3bd6-205">O procedimento a seguir documenta as duas abordagens.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-205">The following procedure documents both approaches.</span></span> 

1. <span data-ttu-id="e3bd6-206">Verifique se você baixou e descompactou o aplicativo [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip), conforme listado nos pré-requisitos.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-206">Make sure you've downloaded and unzipped the [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) application, as listed in the prerequisites.</span></span>

2. <span data-ttu-id="e3bd6-207">Para definir os valores em tempo de execução (e apenas para a sessão atual), execute o `TwitterWPFClient.exe` aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-207">To set the values at run time (and only for the current session), run the `TwitterWPFClient.exe` application.</span></span> <span data-ttu-id="e3bd6-208">Quando o aplicativo solicitar, insira os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="e3bd6-208">When the application prompts you, enter the following values:</span></span>

    * <span data-ttu-id="e3bd6-209">A chave do consumidor do Twitter (chave de API).</span><span class="sxs-lookup"><span data-stu-id="e3bd6-209">The Twitter Consumer Key (API Key).</span></span>
    * <span data-ttu-id="e3bd6-210">A segredo do consumidor do Twitter (segredo de API).</span><span class="sxs-lookup"><span data-stu-id="e3bd6-210">The Twitter Consumer Secret (API Secret).</span></span>
    * <span data-ttu-id="e3bd6-211">O Token de acesso do Twitter.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-211">The Twitter Access Token.</span></span>
    * <span data-ttu-id="e3bd6-212">O Segredo do Token de acesso do Twitter.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-212">The Twitter Access Token Secret.</span></span>
    * <span data-ttu-id="e3bd6-213">As informações de cadeia de conexão que você salvou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-213">The connection string information that you saved earlier.</span></span> <span data-ttu-id="e3bd6-214">Certifique-se de que você use a cadeia de conexão do qual você removeu o `EntityPath` par chave-valor.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-214">Make sure that you use the connection string that you removed the `EntityPath` key-value pair from.</span></span>
    * <span data-ttu-id="e3bd6-215">As palavras-chave do Twitter que você deseja determinar o sentimento.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-215">The Twitter keywords that you want to determine sentiment for.</span></span>

   ![Aplicativo TwitterWpfClient em execução, mostrando as configurações obscuras](./media/stream-analytics-twitter-sentiment-analysis-trends/wpfclientlines.png)

3. <span data-ttu-id="e3bd6-217">Para definir os valores de maneira persistente, use um editor de texto para abrir o arquivo de configuração TwitterWpfClient.exe.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-217">To set the values persistently, use a text editor to open the TwitterWpfClient.exe.config file.</span></span> <span data-ttu-id="e3bd6-218">Em seguida, no elemento `<appSettings>`, faça isso:</span><span class="sxs-lookup"><span data-stu-id="e3bd6-218">Then in the `<appSettings>` element, do this:</span></span>

    * <span data-ttu-id="e3bd6-219">Defina `oauth_consumer_key` a chave do consumidor do Twitter (chave de API).</span><span class="sxs-lookup"><span data-stu-id="e3bd6-219">Set `oauth_consumer_key` to the Twitter Consumer Key (API Key).</span></span> 
    * <span data-ttu-id="e3bd6-220">Defina `oauth_consumer_secret` o segredo do consumidor do Twitter (segredo de API).</span><span class="sxs-lookup"><span data-stu-id="e3bd6-220">Set `oauth_consumer_secret` to the Twitter Consumer Secret (API Secret).</span></span>
    * <span data-ttu-id="e3bd6-221">Defina `oauth_token` o Token de acesso do Twitter.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-221">Set `oauth_token` to the Twitter Access Token.</span></span>
    * <span data-ttu-id="e3bd6-222">Defina `oauth_token_secret` o Segredo do Token de acesso do Twitter.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-222">Set `oauth_token_secret` to the Twitter Access Token Secret.</span></span>

    <span data-ttu-id="e3bd6-223">Mais adiante no elemento `<appSettings>`, faça essas alterações:</span><span class="sxs-lookup"><span data-stu-id="e3bd6-223">Later in the `<appSettings>` element, make these changes:</span></span>

    * <span data-ttu-id="e3bd6-224">Defina `EventHubName` para o nome do hub de evento (ou seja, o valor do caminho da entidade).</span><span class="sxs-lookup"><span data-stu-id="e3bd6-224">Set `EventHubName` to the event hub name (that is, to the value of the entity path).</span></span>
    * <span data-ttu-id="e3bd6-225">Defina `EventHubNameConnectionString` a cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-225">Set `EventHubNameConnectionString` to the connection string.</span></span> <span data-ttu-id="e3bd6-226">Certifique-se de que você use a cadeia de conexão do qual você removeu o `EntityPath` par chave-valor.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-226">Make sure that you use the connection string that you removed the `EntityPath` key-value pair from.</span></span>

    <span data-ttu-id="e3bd6-227">A `<appSettings>` seção se parece com o seguinte exemplo.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-227">The `<appSettings>` section looks like the following example.</span></span> <span data-ttu-id="e3bd6-228">(Para maior clareza e segurança, nós encapsulamos algumas linhas e removemos alguns caracteres.)</span><span class="sxs-lookup"><span data-stu-id="e3bd6-228">(For clarity and security, we wrapped some lines and removed some characters.)</span></span>

    ![Arquivo de configuração de aplicativo TwitterWpfClient em um editor de texto, mostrando as chaves e segredos do Twitter e as informações de cadeia de conexão de hub de eventos](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-tiwtter-app-config.png)
 
4. <span data-ttu-id="e3bd6-230">Se você ainda não iniciou o aplicativo, execute o TwitterWpfClient.exe agora.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-230">If you didn't already start the application, run TwitterWpfClient.exe now.</span></span> 

5. <span data-ttu-id="e3bd6-231">Selecione o botão iniciar verde para coletar sentimento social.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-231">Click the green start button to collect social sentiment.</span></span> <span data-ttu-id="e3bd6-232">Você vê eventos de Tweet com os valores **CreatedAt**, **Topic** e **SentimentScore** sendo enviados ao hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-232">You see Tweet events with the **CreatedAt**, **Topic**, and **SentimentScore** values being sent to your event hub.</span></span>

    ![Aplicativo TwitterWpfClient em execução, mostrando as listagem de tweets](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-app-listing.png)

    >[!NOTE]
    ><span data-ttu-id="e3bd6-234">Se você encontrar erros, e você não vir um fluxo de tweets exibido na parte inferior da janela, verifique novamente as chaves e segredos.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-234">If you see errors, and you don't see a stream of tweets displayed in the lower part of the window, double-check the keys and secrets.</span></span> <span data-ttu-id="e3bd6-235">Além disso, verifique a cadeia de conexão (certifique-se de que ela não inclui o `EntityPath` chave e valor.)</span><span class="sxs-lookup"><span data-stu-id="e3bd6-235">Also check the connection string (make sure that it does not include the `EntityPath` key and value.)</span></span>


## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="e3bd6-236">Criar um trabalho de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="e3bd6-236">Create a Stream Analytics job</span></span>

<span data-ttu-id="e3bd6-237">Agora que os eventos de Tweets estão sendo transmitidos em tempo real do Twitter, você pode configurar um trabalho de Stream Analytics para analisar esses eventos em tempo real.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-237">Now that tweet events are streaming in real time from Twitter, you can set up a Stream Analytics job to analyze these events in real time.</span></span>

1. <span data-ttu-id="e3bd6-238">No portal do Azure, clique em **Novo** > **Internet das Coisas** > **Trabalho do Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-238">In the Azure portal, click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>

2. <span data-ttu-id="e3bd6-239">Selecione o trabalho `socialtwitter-sa-job` e especifique uma assinatura, um grupo de recursos e um local.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-239">Name the job `socialtwitter-sa-job` and specify a subscription, resource group, and location.</span></span>

    <span data-ttu-id="e3bd6-240">É aconselhável colocar o trabalho e o hub de eventos na mesma região para melhor desempenho e para que não seja necessário pagar para transferir dados entre regiões.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-240">It's a good idea to place the job and the event hub in the same region for best performance and so that you don't pay to transfer data between regions.</span></span>

    ![Criando um novo trabalho do Stream Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/newjob.png)

3. <span data-ttu-id="e3bd6-242">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-242">Click **Create**.</span></span>

    <span data-ttu-id="e3bd6-243">O trabalho é criado e o portal exibe detalhes do trabalho.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-243">The job is created and the portal displays job details.</span></span>


## <a name="specify-the-job-input"></a><span data-ttu-id="e3bd6-244">Especificar a entrada de trabalho</span><span class="sxs-lookup"><span data-stu-id="e3bd6-244">Specify the job input</span></span>

1. <span data-ttu-id="e3bd6-245">No trabalho do Stream Analytics, em **Topologia do Trabalho**, no meio da folha de trabalho, selecione **Entradas**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-245">In your Stream Analytics job, under **Job Topology** in the middle of the job blade, click **Inputs**.</span></span> 

2. <span data-ttu-id="e3bd6-246">Na folha **Entradas**, clique em **+&nbsp;Adicionar** e, em seguida, preencha a folha com estes valores:</span><span class="sxs-lookup"><span data-stu-id="e3bd6-246">In the **Inputs** blade, click **+&nbsp;Add** and then fill out the blade with these values:</span></span>

    * <span data-ttu-id="e3bd6-247">**Alias de entrada**: Use o nome `TwitterStream`.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-247">**Input alias**: Use the name `TwitterStream`.</span></span> <span data-ttu-id="e3bd6-248">Se você usar um nome diferente, anote-o porque você precisará dele depois.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-248">If you use a different name, make a note of it because you need it later.</span></span>
    * <span data-ttu-id="e3bd6-249">**Tipo de Origem**: Selecione **Fluxo de Dados**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-249">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="e3bd6-250">**Origem**: Selecione **Hub de Eventos**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-250">**Source**: Select **Event hub**.</span></span>
    * <span data-ttu-id="e3bd6-251">**Opção de importação**: Selecione **Usar hub de evento da assinatura atual**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-251">**Import option**: Select **Use event hub from current subscription**.</span></span> 
    * <span data-ttu-id="e3bd6-252">**Namespace de barramento de serviço**: Selecione o namespace de hub de eventos que você criou anteriormente (`<yourname>-socialtwitter-eh-ns`).</span><span class="sxs-lookup"><span data-stu-id="e3bd6-252">**Service bus namespace**: Select the event hub namespace that you created earlier (`<yourname>-socialtwitter-eh-ns`).</span></span>
    * <span data-ttu-id="e3bd6-253">**Hub de eventos**: Selecione o hub de eventos que você criou anteriormente (`socialtwitter-eh`).</span><span class="sxs-lookup"><span data-stu-id="e3bd6-253">**Event hub**: Select the event hub that you created earlier (`socialtwitter-eh`).</span></span>
    * <span data-ttu-id="e3bd6-254">**Nome de política do hub de eventos**: Selecione a política de acesso que você criou anteriormente (`socialtwitter-access`).</span><span class="sxs-lookup"><span data-stu-id="e3bd6-254">**Event hub policy name**: Select the access policy that you created earlier (`socialtwitter-access`).</span></span>

    ![Criar nova entrada para o trabalho de Streaming Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-new-input.png)

3. <span data-ttu-id="e3bd6-256">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-256">Click **Create**.</span></span>


## <a name="specify-the-job-query"></a><span data-ttu-id="e3bd6-257">Especificar a consulta de trabalho</span><span class="sxs-lookup"><span data-stu-id="e3bd6-257">Specify the job query</span></span>

<span data-ttu-id="e3bd6-258">O Stream Analytics dá suporte a um modelo de consulta simples e declarativo que descreve as transformações.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-258">Stream Analytics supports a simple, declarative query model that describes transformations.</span></span> <span data-ttu-id="e3bd6-259">Para saber mais sobre a linguagem, consulte a [Referência de linguagem de consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span><span class="sxs-lookup"><span data-stu-id="e3bd6-259">To learn more about the language, see the [Azure Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>  <span data-ttu-id="e3bd6-260">Este tutorial ajuda você a criar e testar várias consultas sobre dados do Twitter.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-260">This tutorial helps you author and test several queries over Twitter data.</span></span>

<span data-ttu-id="e3bd6-261">Para comparar o número de menções entre tópicos, você pode usar uma [Janela em Cascata](https://msdn.microsoft.com/library/azure/dn835055.aspx) para obter a contagem de menções por tópico a cada cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-261">To compare the number of mentions among topics, you can use a [Tumbling window](https://msdn.microsoft.com/library/azure/dn835055.aspx) to get the count of mentions by topic every five seconds.</span></span>

1. <span data-ttu-id="e3bd6-262">Feche a folha de **entradas** se ainda não o fez.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-262">Close the **Inputs** blade if you haven't already.</span></span>

2. <span data-ttu-id="e3bd6-263">Na folha do trabalho, clique na caixa **Consulta**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-263">In the job blade, click the **Query** box.</span></span> <span data-ttu-id="e3bd6-264">Azure lista as entradas e saídas que são configuradas para o trabalho e permite que você crie uma consulta que permite transformar o fluxo de entrada como ela é enviada para a saída.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-264">Azure lists the inputs and outputs that are configured for the job, and lets you create a query that lets you transform the input stream as it is sent to the output.</span></span>

3. <span data-ttu-id="e3bd6-265">Certifique-se de que o aplicativo TwitterWpfClient está em execução.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-265">Make sure that the TwitterWpfClient application is running.</span></span> 

3. <span data-ttu-id="e3bd6-266">Na folha **Consulta**, clique nos pontos ao lado da `TwitterStream` entrada e, em seguida, selecione **Dados de exemplo da entrada**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-266">In the **Query** blade, click the dots next to the `TwitterStream` input and then select **Sample data from input**.</span></span>

    ![Opções de menu para usar dados de exemplo para a entrada de trabalho de Streaming Analytics, com "Dados de exemplo de entrada" selecionados](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-sample-data-from-input.png)

    <span data-ttu-id="e3bd6-268">Isso abrirá uma folha que permite que você especifique quantos dados de exemplo obter definido em termos de quanto tempo necessário para ler o fluxo de entrada.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-268">This opens a blade that lets you specify how much sample data to get, defined in terms of how long to read the input stream.</span></span>

4. <span data-ttu-id="e3bd6-269">Defina **Minutos** para 3 e, em seguida, clique em **Ok**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-269">Set **Minutes** to 3 and then click **OK**.</span></span> 
    
    ![Opções de amostragem de fluxo de entrada, com "3 minutos" selecionados.](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-input-create-sample-data.png)

    <span data-ttu-id="e3bd6-271">O Azure prova dados do fluxo de entrada de 3 minutos e notifica quando os dados de exemplo estão prontos.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-271">Azure samples 3 minutes' worth of data from the input stream and notifies you when the sample data is ready.</span></span> <span data-ttu-id="e3bd6-272">(Isso pode levar um tempo.)</span><span class="sxs-lookup"><span data-stu-id="e3bd6-272">(This takes a short while.)</span></span> 

    <span data-ttu-id="e3bd6-273">Os dados de exemplo são armazenados temporariamente e estão disponíveis enquanto a janela de consulta estiver aberta.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-273">The sample data is stored temporarily and is available while you have the query window open.</span></span> <span data-ttu-id="e3bd6-274">Se você fechar a janela de consulta, os dados de exemplo serão descartados e você terá que criar um novo conjunto de dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-274">If you close the query window, the sample data is discarded, and you have to create a new set of sample data.</span></span> 

5. <span data-ttu-id="e3bd6-275">Altere a consulta no editor de código para:</span><span class="sxs-lookup"><span data-stu-id="e3bd6-275">Change the query in the code editor to the following:</span></span>

    ```
    SELECT System.Timestamp as Time, Topic, COUNT(*)
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY TUMBLINGWINDOW(s, 5), Topic
    ```

    <span data-ttu-id="e3bd6-276">Se não usar `TwitterStream` como o alias para a entrada, substitua o alias para `TwitterStream` na consulta.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-276">If didn't use `TwitterStream` as the alias for the input, substitute your alias for `TwitterStream` in the query.</span></span>  

    <span data-ttu-id="e3bd6-277">Essa consulta usa a palavra-chave **TIMESTAMP BY** para especificar um campo de carimbo de data/hora na carga a ser usada na computação temporal.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-277">This query uses the **TIMESTAMP BY** keyword to specify a timestamp field in the payload to be used in the temporal computation.</span></span> <span data-ttu-id="e3bd6-278">Se esse campo não for especificado, a operação em janela será realizada usando a hora em que cada evento chegou ao hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-278">If this field isn't specified, the windowing operation is performed by using the time that each event arrived at the event hub.</span></span> <span data-ttu-id="e3bd6-279">Saiba mais na seção “Hora de chegada versus tempo de aplicação” na [Referência de consulta do Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span><span class="sxs-lookup"><span data-stu-id="e3bd6-279">Learn more in the "Arrival Time vs Application Time" section of [Stream Analytics Query Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>

    <span data-ttu-id="e3bd6-280">A consulta também acessa um carimbo de data/hora para o final de cada janela usando a propriedade **System.Timestamp**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-280">This query also accesses a timestamp for the end of each window by using the **System.Timestamp** property.</span></span>

5. <span data-ttu-id="e3bd6-281">Clique em **Testar**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-281">Click **Test**.</span></span> <span data-ttu-id="e3bd6-282">A consulta é executada em relação aos dados que você amostrou.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-282">The query runs against the data that you sampled.</span></span>
    
6. <span data-ttu-id="e3bd6-283">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-283">Click **Save**.</span></span> <span data-ttu-id="e3bd6-284">Isso salva a consulta como parte do trabalho de Streaming Analytics.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-284">This saves the query as part of the Streaming Analytics job.</span></span> <span data-ttu-id="e3bd6-285">(Ele não salva os dados de exemplo.)</span><span class="sxs-lookup"><span data-stu-id="e3bd6-285">(It doesn't save the sample data.)</span></span>


## <a name="experiment-using-different-fields-from-the-stream"></a><span data-ttu-id="e3bd6-286">Experimente usar diferentes campos do fluxo</span><span class="sxs-lookup"><span data-stu-id="e3bd6-286">Experiment using different fields from the stream</span></span> 

<span data-ttu-id="e3bd6-287">A tabela a seguir lista os campos que fazem parte do fluxo de dados JSON.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-287">The following table lists the fields that are part of the JSON streaming data.</span></span> <span data-ttu-id="e3bd6-288">Fique à vontade para fazer experiências no editor de consultas.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-288">Feel free to experiment in the query editor.</span></span>

|<span data-ttu-id="e3bd6-289">Propriedade JSON</span><span class="sxs-lookup"><span data-stu-id="e3bd6-289">JSON property</span></span> | <span data-ttu-id="e3bd6-290">Definição</span><span class="sxs-lookup"><span data-stu-id="e3bd6-290">Definition</span></span>|
|--- | ---|
|<span data-ttu-id="e3bd6-291">CreatedAt</span><span class="sxs-lookup"><span data-stu-id="e3bd6-291">CreatedAt</span></span> | <span data-ttu-id="e3bd6-292">A hora em que foi criado o tweet</span><span class="sxs-lookup"><span data-stu-id="e3bd6-292">The time that the tweet was created</span></span>|
|<span data-ttu-id="e3bd6-293">Tópico</span><span class="sxs-lookup"><span data-stu-id="e3bd6-293">Topic</span></span> | <span data-ttu-id="e3bd6-294">O tópico que corresponde à palavra-chave especificada</span><span class="sxs-lookup"><span data-stu-id="e3bd6-294">The topic that matches the specified keyword</span></span>|
|<span data-ttu-id="e3bd6-295">SentimentScore</span><span class="sxs-lookup"><span data-stu-id="e3bd6-295">SentimentScore</span></span> | <span data-ttu-id="e3bd6-296">A pontuação de sentimento do Sentiment140</span><span class="sxs-lookup"><span data-stu-id="e3bd6-296">The sentiment score from Sentiment140</span></span>|
|<span data-ttu-id="e3bd6-297">Autor</span><span class="sxs-lookup"><span data-stu-id="e3bd6-297">Author</span></span> | <span data-ttu-id="e3bd6-298">O identificador do Twitter que enviou o tweet</span><span class="sxs-lookup"><span data-stu-id="e3bd6-298">The Twitter handle that sent the tweet</span></span>|
|<span data-ttu-id="e3bd6-299">Texto</span><span class="sxs-lookup"><span data-stu-id="e3bd6-299">Text</span></span> | <span data-ttu-id="e3bd6-300">O corpo completo do tweet</span><span class="sxs-lookup"><span data-stu-id="e3bd6-300">The full body of the tweet</span></span>|


## <a name="create-an-output-sink"></a><span data-ttu-id="e3bd6-301">Criar um coletor de saída</span><span class="sxs-lookup"><span data-stu-id="e3bd6-301">Create an output sink</span></span>

<span data-ttu-id="e3bd6-302">Agora você definiu um fluxo de eventos, uma entrada de hub de eventos para a ingestão de eventos e uma consulta para executar uma transformação no fluxo.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-302">You have now defined an event stream, an event hub input to ingest events, and a query to perform a transformation over the stream.</span></span> <span data-ttu-id="e3bd6-303">A última etapa é definir um coletor de saída para o trabalho.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-303">The last step is to define an output sink for the job.</span></span>  

<span data-ttu-id="e3bd6-304">Neste tutorial, você gravou os eventos de tweets agregados de nossa consulta de trabalho para o armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-304">In this tutorial, you write the aggregated tweet events from the job query to Azure Blob storage.</span></span>  <span data-ttu-id="e3bd6-305">Você também pode enviar por push os resultados para um Banco de Dados SQL do Azure, um armazenamento de Tabelas do Azure, para Hubs de Eventos ou Power BI, dependendo das suas necessidades de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-305">You can also push your results to Azure SQL Database, Azure Table storage, Event Hubs, or Power BI, depending on your application needs.</span></span>

## <a name="specify-the-job-output"></a><span data-ttu-id="e3bd6-306">Especificar a saída de trabalho</span><span class="sxs-lookup"><span data-stu-id="e3bd6-306">Specify the job output</span></span>

1. <span data-ttu-id="e3bd6-307">Na seção **Trabalho de Topologia**, clique na caixa **Saída**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-307">In the **Job Topology** section, click the **Output** box.</span></span> 

2. <span data-ttu-id="e3bd6-308">Na folha **Saídas**, clique em **+&nbsp;Adicionar** e, em seguida, preencha a folha com estes valores:</span><span class="sxs-lookup"><span data-stu-id="e3bd6-308">In the **Outputs** blade, click **+&nbsp;Add** and then fill out the blade with these values:</span></span>

    * <span data-ttu-id="e3bd6-309">**Alias de saída**: Use o nome `TwitterStream-Output`.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-309">**Output alias**: Use the name `TwitterStream-Output`.</span></span> 
    * <span data-ttu-id="e3bd6-310">**Coletor**: selecione **Armazenamento de blobs**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-310">**Sink**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="e3bd6-311">**Opções de importação**: Selecione **Usar armazenamento de blobs da assinatura atual**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-311">**Import options**: Select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="e3bd6-312">**Conta de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-312">**Storage account**.</span></span> <span data-ttu-id="e3bd6-313">Selecione **Criar uma nova conta de armazenamento.**</span><span class="sxs-lookup"><span data-stu-id="e3bd6-313">Select **Create a new storage account.**</span></span>
    * <span data-ttu-id="e3bd6-314">**Conta de armazenamento** (segunda caixa).</span><span class="sxs-lookup"><span data-stu-id="e3bd6-314">**Storage account** (second box).</span></span> <span data-ttu-id="e3bd6-315">Digite `YOURNAMEsa`, onde `YOURNAME` é o seu nome ou outra cadeia de caracteres exclusiva.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-315">Enter `YOURNAMEsa`, where `YOURNAME` is your name or another unique string.</span></span> <span data-ttu-id="e3bd6-316">O nome pode ter apenas letras minúsculas e números e deve ser exclusivo no Azure.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-316">The name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 
    * <span data-ttu-id="e3bd6-317">**Contêiner**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-317">**Container**.</span></span> <span data-ttu-id="e3bd6-318">Digite `socialtwitter`.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-318">Enter `socialtwitter`.</span></span>
    <span data-ttu-id="e3bd6-319">O nome da conta de armazenamento e o nome do contêiner são usados juntos para fornecer um URI para o armazenamento de blobs, como este:</span><span class="sxs-lookup"><span data-stu-id="e3bd6-319">The storage account name and container name are used together to provide a URI for the blob storage, like this:</span></span> 

    `http://YOURNAMEsa.blob.core.windows.net/socialtwitter/...`
    
    ![Folha "Nova saída" para trabalho do Stream Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-output-blob-storage.png)
    
4. <span data-ttu-id="e3bd6-321">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-321">Click **Create**.</span></span> 

    <span data-ttu-id="e3bd6-322">Azure cria a conta de armazenamento e gera uma chave automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-322">Azure creates the storage account and generates a key automatically.</span></span> 

5. <span data-ttu-id="e3bd6-323">Feche a folha **Saída**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-323">Close the **Outputs** blade.</span></span> 


## <a name="start-the-job"></a><span data-ttu-id="e3bd6-324">Iniciar o trabalho</span><span class="sxs-lookup"><span data-stu-id="e3bd6-324">Start the job</span></span>

<span data-ttu-id="e3bd6-325">Uma entrada de trabalho, uma consulta e uma saída são especificadas.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-325">A job input, query, and output are specified.</span></span> <span data-ttu-id="e3bd6-326">Você está pronto para iniciar o trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-326">You are ready to start the Stream Analytics job.</span></span>

1. <span data-ttu-id="e3bd6-327">Certifique-se de que o aplicativo TwitterWpfClient está em execução.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-327">Make sure that the TwitterWpfClient application is running.</span></span> 

2. <span data-ttu-id="e3bd6-328">Na folha do trabalho, clique em **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-328">In the job blade, click **Start**.</span></span>

    ![Iniciar o trabalho do Stream Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-output.png)

3. <span data-ttu-id="e3bd6-330">Na folha **Iniciar trabalho**, para **Hora de início de trabalho**, selecione **Agora** e, em seguida, clique em **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-330">In the **Start job** blade, for **Job output start time**, select **Now** and then click **Start**.</span></span> 

    ![Folha "Começar trabalho" para trabalho do Stream Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-job-blade.png)

    <span data-ttu-id="e3bd6-332">O Azure notifica você quando o trabalho for iniciado e, na folha de trabalho, o status é exibido como **Executando**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-332">Azure notifies you when the job has started, and in the job blade, the status is displayed as **Running**.</span></span>

    ![Trabalho em execução](./media/stream-analytics-twitter-sentiment-analysis-trends/jobrunning.png)

## <a name="view-output-for-sentiment-analysis"></a><span data-ttu-id="e3bd6-334">Exibir saída para análise sentimento</span><span class="sxs-lookup"><span data-stu-id="e3bd6-334">View output for sentiment analysis</span></span>

<span data-ttu-id="e3bd6-335">Depois que o trabalho tiver sido iniciado e estiver processando o fluxo do Twitter em tempo real, escolha como você deseja exibir a saída para análise de sentimento.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-335">After your job has started running and is processing the real-time Twitter stream, you can view the output for sentiment analysis.</span></span>

<span data-ttu-id="e3bd6-336">Use uma ferramenta como o [Azure Storage Explorer](https://http://storageexplorer.com/) ou o [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction) para exibir a saída do trabalho em tempo real.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-336">You can use a tool like [Azure Storage Explorer](https://http://storageexplorer.com/) or [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction) to view your job output in real time.</span></span> <span data-ttu-id="e3bd6-337">Daqui, você pode usar o [Power BI](https://powerbi.com/) para estender seu aplicativo para incluir um painel personalizado como o demonstrado na seguinte captura de tela:</span><span class="sxs-lookup"><span data-stu-id="e3bd6-337">From here, you can use [Power BI](https://powerbi.com/) to extend your application to include a customized dashboard like the one shown in the following screenshot:</span></span>

![Power BI](./media/stream-analytics-twitter-sentiment-analysis-trends/power-bi.png)


## <a name="create-another-query-to-identify-trending-topics"></a><span data-ttu-id="e3bd6-339">Criar outra consulta para identificar os tópicos mais populares</span><span class="sxs-lookup"><span data-stu-id="e3bd6-339">Create another query to identify trending topics</span></span>

<span data-ttu-id="e3bd6-340">Outra consulta que você pode usar para entender o sentimento do Twitter baseia-se em uma [Janela Deslizante](https://msdn.microsoft.com/library/azure/dn835051.aspx).</span><span class="sxs-lookup"><span data-stu-id="e3bd6-340">Another query you can use to understand Twitter sentiment is based on a [Sliding Window](https://msdn.microsoft.com/library/azure/dn835051.aspx).</span></span> <span data-ttu-id="e3bd6-341">Para identificar os tópicos mais populares, procuraremos tópicos que ultrapassem um valor limite de menções em determinado período de tempo.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-341">To identify trending topics, you look for topics that cross a threshold value for mentions in a specified amount of time.</span></span>

<span data-ttu-id="e3bd6-342">Para as finalidades deste tutorial, verificaremos os tópicos mencionados mais de 20 vezes nos últimos 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-342">For the purposes of this tutorial, you check for topics that are mentioned more than 20 times in the last 5 seconds.</span></span>

1. <span data-ttu-id="e3bd6-343">Na folha de trabalho, clique em **Parar** para interromper o trabalho.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-343">In the job blade, click **Stop** to stop the job.</span></span> 

2. <span data-ttu-id="e3bd6-344">Na seção **Trabalho de Topologia**, clique na caixa **Saída**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-344">In the **Job Topology** section, click the **Query** box.</span></span> 

3. <span data-ttu-id="e3bd6-345">Mude a consulta para o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e3bd6-345">Change the query to the following:</span></span>

    ```    
    SELECT System.Timestamp as Time, Topic, COUNT(*) as Mentions
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY SLIDINGWINDOW(s, 5), topic
    HAVING COUNT(*) > 20
    ```

4. <span data-ttu-id="e3bd6-346">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-346">Click **Save**.</span></span>

5. <span data-ttu-id="e3bd6-347">Certifique-se de que o aplicativo TwitterWpfClient está em execução.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-347">Make sure that the TwitterWpfClient application is running.</span></span> 

6. <span data-ttu-id="e3bd6-348">Clique em **Iniciar** para reiniciar o trabalho usando a nova consulta.</span><span class="sxs-lookup"><span data-stu-id="e3bd6-348">Click **Start** to restart the job using the new query.</span></span>


## <a name="get-support"></a><span data-ttu-id="e3bd6-349">Obtenha suporte</span><span class="sxs-lookup"><span data-stu-id="e3bd6-349">Get support</span></span>
<span data-ttu-id="e3bd6-350">Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="e3bd6-350">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3bd6-351">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e3bd6-351">Next steps</span></span>
* [<span data-ttu-id="e3bd6-352">Introdução ao Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="e3bd6-352">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="e3bd6-353">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="e3bd6-353">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="e3bd6-354">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="e3bd6-354">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="e3bd6-355">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="e3bd6-355">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="e3bd6-356">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="e3bd6-356">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
