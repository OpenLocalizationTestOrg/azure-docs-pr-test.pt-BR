---
title: "análise de sentimento do Twitter aaaReal tempo com o Azure Stream Analytics | Microsoft Docs"
description: "Saiba como toouse do Stream Analytics para análise de sentimento do Twitter em tempo real. Orientações passo a passo de toodata de geração de eventos em um painel ativo."
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
ms.openlocfilehash: 157790caa7ea6f5570dd9c9d3bd9694d437eb4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-twitter-sentiment-analysis-in-azure-stream-analytics"></a><span data-ttu-id="cc58d-105">Análise de sentimento do Twitter em tempo real no Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="cc58d-105">Real-time Twitter sentiment analysis in Azure Stream Analytics</span></span>

<span data-ttu-id="cc58d-106">Saiba como uma solução de análise de sentimento para análise de mídia social, colocando em tempo real de toobuild Twitter eventos para Hubs de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc58d-106">Learn how toobuild a sentiment analysis solution for social media analytics by bringing real-time Twitter events into Azure Event Hubs.</span></span> <span data-ttu-id="cc58d-107">Em seguida, você pode escrever um Stream Analytics do Azure consultar tooanalyze Olá dados e um repositório Olá resultados para uso posterior ou use um painel e [Power BI](https://powerbi.com/) tooprovide insights em tempo real.</span><span class="sxs-lookup"><span data-stu-id="cc58d-107">You can then write an Azure Stream Analytics query tooanalyze hello data and either store hello results for later use or use a dashboard and [Power BI](https://powerbi.com/) tooprovide insights in real time.</span></span>

<span data-ttu-id="cc58d-108">As ferramentas de análise de mídias sociais ajudam as organizações a compreender os tópicos mais populares.</span><span class="sxs-lookup"><span data-stu-id="cc58d-108">Social media analytics tools help organizations understand trending topics.</span></span> <span data-ttu-id="cc58d-109">Os tópicos mais populares são entidades e atitudes com um alto volume de postagens em mídia social.</span><span class="sxs-lookup"><span data-stu-id="cc58d-109">Trending topics are subjects and attitudes that have a high volume of posts in social media.</span></span> <span data-ttu-id="cc58d-110">Análise de sentimento, que também é chamado *mineração opinião*, usa posturas de toodetermine de ferramentas de análise de mídia social para um produto, ideia e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="cc58d-110">Sentiment analysis, which is also called *opinion mining*, uses social media analytics tools toodetermine attitudes toward a product, idea, and so on.</span></span> 

<span data-ttu-id="cc58d-111">Análise de tendência do Twitter em tempo real é um ótimo exemplo de uma ferramenta de análise, porque o modelo de assinatura de hashtag Olá permite que você toolisten toospecific palavras-chave (hashtags) e desenvolver a análise de sentimento de saudação feed.</span><span class="sxs-lookup"><span data-stu-id="cc58d-111">Real-time Twitter trend analysis is a great example of an analytics tool, because hello hashtag subscription model enables you toolisten toospecific keywords (hashtags) and develop sentiment analysis of hello feed.</span></span>

## <a name="scenario-social-media-sentiment-analysis-in-real-time"></a><span data-ttu-id="cc58d-112">Cenário: Análise de sentimento de mídia social em tempo real</span><span class="sxs-lookup"><span data-stu-id="cc58d-112">Scenario: Social media sentiment analysis in real time</span></span>

<span data-ttu-id="cc58d-113">Uma empresa que tem um site de mídia está interessa em obter uma vantagem sobre a concorrência apresentando o conteúdo do site que está imediatamente relevantes tooits leitores.</span><span class="sxs-lookup"><span data-stu-id="cc58d-113">A company that has a news media website is interested in gaining an advantage over its competitors by featuring site content that is immediately relevant tooits readers.</span></span> <span data-ttu-id="cc58d-114">empresa de saudação usa análise de mídia social sobre tópicos que são relevantes tooreaders ao fazer a análise de sentimento em tempo real dos dados do Twitter.</span><span class="sxs-lookup"><span data-stu-id="cc58d-114">hello company uses social media analysis on topics that are relevant tooreaders by doing real-time sentiment analysis of Twitter data.</span></span>

<span data-ttu-id="cc58d-115">tópicos de análise de tendências de tooidentify em tempo real no Twitter, Olá necessidades de empresa análise em tempo real sobre volume de tweet hello e sentimento tópicos chave.</span><span class="sxs-lookup"><span data-stu-id="cc58d-115">tooidentify trending topics in real time on Twitter, hello company needs real-time analytics about hello tweet volume and sentiment for key topics.</span></span> <span data-ttu-id="cc58d-116">Em outras palavras, a necessidade de saudação é um mecanismo de análise de análise de sentimento que se baseia a esta mídia social feed.</span><span class="sxs-lookup"><span data-stu-id="cc58d-116">In other words, hello need is a sentiment analysis analytics engine that's based on this social media feed.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc58d-117">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cc58d-117">Prerequisites</span></span>
<span data-ttu-id="cc58d-118">Neste tutorial, você deve usar um aplicativo cliente que se conecta tooTwitter e procura tweets com determinados hashtags (que pode ser definida).</span><span class="sxs-lookup"><span data-stu-id="cc58d-118">In this tutorial, you use a client application that connects tooTwitter and looks for tweets that have certain hashtags (which you can set).</span></span> <span data-ttu-id="cc58d-119">Em ordem toorun Olá aplicativo e analisar Olá tweets usando a análise de fluxo do Azure, você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="cc58d-119">In order toorun hello application and analyze hello tweets using Azure Streaming Analytics, you must have hello following:</span></span>

* <span data-ttu-id="cc58d-120">Uma assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="cc58d-120">An Azure subscription</span></span>
* <span data-ttu-id="cc58d-121">Uma conta do Twitter</span><span class="sxs-lookup"><span data-stu-id="cc58d-121">A Twitter account</span></span> 
* <span data-ttu-id="cc58d-122">Um aplicativo do Twitter e hello [token de acesso OAuth](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cc58d-122">A Twitter application, and hello [OAuth access token](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) for that application.</span></span> <span data-ttu-id="cc58d-123">Podemos fornecer instruções de alto nível sobre como toocreate um aplicativo do Twitter mais tarde.</span><span class="sxs-lookup"><span data-stu-id="cc58d-123">We provide high-level instructions for how toocreate a Twitter application later.</span></span>
* <span data-ttu-id="cc58d-124">aplicativo de TwitterWPFClient Hello, que lê Olá Twitter feed.</span><span class="sxs-lookup"><span data-stu-id="cc58d-124">hello TwitterWPFClient application, which reads hello Twitter feed.</span></span> <span data-ttu-id="cc58d-125">tooget esse aplicativo, o download Olá [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) do GitHub de arquivo e, em seguida, descompacte o pacote de saudação em uma pasta no seu computador.</span><span class="sxs-lookup"><span data-stu-id="cc58d-125">tooget this application, download hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) file from GitHub and then unzip hello package into a folder on your computer.</span></span> <span data-ttu-id="cc58d-126">Se desejar que o código-fonte toosee hello e executar o aplicativo hello em um depurador, você pode obter o código-fonte Olá de [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator).</span><span class="sxs-lookup"><span data-stu-id="cc58d-126">If you want toosee hello source code and run hello application in a debugger, you can get hello source code from [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator).</span></span> 

## <a name="create-an-event-hub-for-streaming-analytics-input"></a><span data-ttu-id="cc58d-127">Criar um hub de eventos para entrada do Streaming Analytics</span><span class="sxs-lookup"><span data-stu-id="cc58d-127">Create an event hub for Streaming Analytics input</span></span>

<span data-ttu-id="cc58d-128">aplicativo de exemplo Hello gera eventos e envia-os tooan hub de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc58d-128">hello sample application generates events and pushes them tooan Azure event hub.</span></span> <span data-ttu-id="cc58d-129">Hubs de eventos do Azure são método hello preferido de inclusão de eventos para análise de fluxo.</span><span class="sxs-lookup"><span data-stu-id="cc58d-129">Azure event hubs are hello preferred method of event ingestion for Stream Analytics.</span></span> <span data-ttu-id="cc58d-130">Para obter mais informações, consulte Olá [documentação de Hubs de eventos do Azure](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="cc58d-130">For more information, see hello [Azure Event Hubs documentation](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>


### <a name="create-an-event-hub-namespace-and-event-hub"></a><span data-ttu-id="cc58d-131">Criar um namespace de hub de eventos e um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="cc58d-131">Create an event hub namespace and event hub</span></span>
<span data-ttu-id="cc58d-132">Neste procedimento, você primeiro criar um namespace de hub de eventos e, em seguida, você pode adicionar um namespace de toothat do hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="cc58d-132">In this procedure, you first create an event hub namespace, and then you add an event hub toothat namespace.</span></span> <span data-ttu-id="cc58d-133">Namespaces do hub de eventos são usados toologically grupo relacionadas a instâncias de barramento de eventos.</span><span class="sxs-lookup"><span data-stu-id="cc58d-133">Event hub namespaces are used toologically group related event bus instances.</span></span> 

1. <span data-ttu-id="cc58d-134">Faça logon no portal do Azure de toohello e clique em **novo** > **Internet das coisas** > **Hub de eventos**.</span><span class="sxs-lookup"><span data-stu-id="cc58d-134">Log  in toohello Azure portal and click **New** > **Internet of Things** > **Event Hub**.</span></span> 

2. <span data-ttu-id="cc58d-135">Em Olá **criar namespace** folha, insira um nome de namespace como `<yourname>-socialtwitter-eh-ns`.</span><span class="sxs-lookup"><span data-stu-id="cc58d-135">In hello **Create namespace** blade, enter a namespace name such as `<yourname>-socialtwitter-eh-ns`.</span></span> <span data-ttu-id="cc58d-136">Você pode usar qualquer nome de namespace hello, mas nome hello deve ser válido para uma URL e deve ser exclusivo no Azure.</span><span class="sxs-lookup"><span data-stu-id="cc58d-136">You can use any name for hello namespace, but hello name must be valid for a URL and it must be unique across Azure.</span></span> 
    
3. <span data-ttu-id="cc58d-137">Selecione uma assinatura e crie ou escolha um grupo de recursos e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="cc58d-137">Select a subscription and create or choose a resource group, then click **Create**.</span></span> 

    ![Criar um namespace do hub de eventos](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-namespace.png)
 
4. <span data-ttu-id="cc58d-139">Ao namespace Olá terminou de implantação, encontre hello namespace de hub de eventos na lista de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="cc58d-139">When hello namespace has finished deploying, find hello event hub namespace in your list of Azure resources.</span></span> 

5. <span data-ttu-id="cc58d-140">Clique em novo namespace de saudação e na folha de namespace hello, clique em  **+ &nbsp;Hub de eventos**.</span><span class="sxs-lookup"><span data-stu-id="cc58d-140">Click hello new namespace, and in hello namespace blade, click **+&nbsp;Event Hub**.</span></span> 

    ![<span data-ttu-id="cc58d-141">botão de adicionar o Hub de eventos Olá para criar um novo hub de eventos</span><span class="sxs-lookup"><span data-stu-id="cc58d-141">hello Add Event Hub button for creating a new event hub</span></span> ](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-button.png)    
 
6. <span data-ttu-id="cc58d-142">Nome hello novo hub de eventos `socialtwitter-eh`.</span><span class="sxs-lookup"><span data-stu-id="cc58d-142">Name hello new event hub `socialtwitter-eh`.</span></span> <span data-ttu-id="cc58d-143">Você pode usar um nome diferente.</span><span class="sxs-lookup"><span data-stu-id="cc58d-143">You can use a different name.</span></span> <span data-ttu-id="cc58d-144">Se você fizer isso, anote-lo, porque você precisa de nome hello mais tarde.</span><span class="sxs-lookup"><span data-stu-id="cc58d-144">If you do, make a note of it, because you need hello name later.</span></span> <span data-ttu-id="cc58d-145">Você não precisa tooset quaisquer outras opções para o hub de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="cc58d-145">You don't need tooset any other options for hello event hub.</span></span>

    ![Folha para a criação de um novo hub de eventos](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub.png)
 
7. <span data-ttu-id="cc58d-147">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="cc58d-147">Click **Create**.</span></span>


### <a name="grant-access-toohello-event-hub"></a><span data-ttu-id="cc58d-148">Hub de eventos de toohello conceder acesso</span><span class="sxs-lookup"><span data-stu-id="cc58d-148">Grant access toohello event hub</span></span>

<span data-ttu-id="cc58d-149">Antes de um processo pode enviar o hub de eventos de tooan de dados, o hub de eventos Olá deve ter uma política que permite o acesso apropriado.</span><span class="sxs-lookup"><span data-stu-id="cc58d-149">Before a process can send data tooan event hub, hello event hub must have a policy that allows appropriate access.</span></span> <span data-ttu-id="cc58d-150">política de acesso de saudação produz uma cadeia de caracteres de conexão que inclui informações de autorização.</span><span class="sxs-lookup"><span data-stu-id="cc58d-150">hello access policy produces a connection string that includes authorization information.</span></span>

1.  <span data-ttu-id="cc58d-151">Na folha de namespace do evento hello, clique em **Hubs de eventos** e, em seguida, clique em nome de saudação do seu novo hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="cc58d-151">In hello event namespace blade, click **Event Hubs** and then click hello name of your new event hub.</span></span>

2.  <span data-ttu-id="cc58d-152">Na folha de hub de evento hello, clique em **políticas de acesso compartilhado** e, em seguida, clique em  **+ &nbsp;adicionar**.</span><span class="sxs-lookup"><span data-stu-id="cc58d-152">In hello event hub blade, click **Shared access policies** and then click **+&nbsp;Add**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="cc58d-153">Verifique se que você estiver trabalhando com o hub de eventos hello, não Olá namespace de hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="cc58d-153">Make sure you're working with hello event hub, not hello event hub namespace.</span></span>

3.  <span data-ttu-id="cc58d-154">Adicione uma política chamada `socialtwitter-access` e para **Declaração**, selecione **Gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="cc58d-154">Add a policy named `socialtwitter-access` and for **Claim**, select **Manage**.</span></span>

    ![Folha para a criação de uma nova política de acesso de hub de eventos](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-shared-access-policy-manage.png)
 
4.  <span data-ttu-id="cc58d-156">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="cc58d-156">Click **Create**.</span></span>

5.  <span data-ttu-id="cc58d-157">Após a implantação de política de saudação, clique na lista de saudação de políticas de acesso compartilhado.</span><span class="sxs-lookup"><span data-stu-id="cc58d-157">After hello policy has been deployed, click it in hello list of shared access policies.</span></span>

6.  <span data-ttu-id="cc58d-158">Caixa de saudação localizar **chave primária de cadeia de caracteres de conexão** e clique em cadeia de conexão do hello cópia botão Avançar toohello.</span><span class="sxs-lookup"><span data-stu-id="cc58d-158">Find hello box labeled **CONNECTION STRING-PRIMARY KEY** and click hello copy button next toohello connection string.</span></span> 
    
    ![Copiar a chave de cadeia de caracteres de conexão primária de saudação da política de acesso de saudação](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-shared-access-policy-copy-connection-string.png)
 
7.  <span data-ttu-id="cc58d-160">Cole a cadeia de caracteres de conexão de saudação em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="cc58d-160">Paste hello connection string into a text editor.</span></span> <span data-ttu-id="cc58d-161">É necessário essa cadeia de caracteres de conexão para a próxima seção de hello, depois de fazer algumas pequenas edições tooit.</span><span class="sxs-lookup"><span data-stu-id="cc58d-161">You need this connection string for hello next section, after you make some small edits tooit.</span></span>

    <span data-ttu-id="cc58d-162">cadeia de caracteres de conexão Olá tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="cc58d-162">hello connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=;EntityPath=socialtwitter-eh

    <span data-ttu-id="cc58d-163">Observe que a cadeia de caracteres de conexão Olá contém vários pares de chave-valor, separados por ponto e vírgula: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, e `EntityPath`.</span><span class="sxs-lookup"><span data-stu-id="cc58d-163">Notice that hello connection string contains multiple key-value pairs, separated with semicolons: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, and `EntityPath`.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="cc58d-164">Para segurança, partes da cadeia de conexão Olá no exemplo hello foram removidos.</span><span class="sxs-lookup"><span data-stu-id="cc58d-164">For security, parts of hello connection string in hello example have been removed.</span></span>

8.  <span data-ttu-id="cc58d-165">No editor de texto de saudação, remover Olá `EntityPath` par de cadeia de caracteres de conexão de saudação (não se esqueça de tooremove Olá-e-vírgula anterior).</span><span class="sxs-lookup"><span data-stu-id="cc58d-165">In hello text editor, remove hello `EntityPath` pair from hello connection string (don't forget tooremove hello semicolon that precedes it).</span></span> <span data-ttu-id="cc58d-166">Quando terminar, cadeia de caracteres de conexão Olá terá esta aparência:</span><span class="sxs-lookup"><span data-stu-id="cc58d-166">When you're done, hello connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=


## <a name="configure-and-start-hello-twitter-client-application"></a><span data-ttu-id="cc58d-167">Configurar e iniciar o aplicativo de cliente do Twitter hello</span><span class="sxs-lookup"><span data-stu-id="cc58d-167">Configure and start hello Twitter client application</span></span>
<span data-ttu-id="cc58d-168">aplicativo de cliente Hello obtém eventos tweet diretamente do Twitter.</span><span class="sxs-lookup"><span data-stu-id="cc58d-168">hello client application gets tweet events directly from Twitter.</span></span> <span data-ttu-id="cc58d-169">Em ordem toodo isso, é necessário Olá toocall de permissão do Twitter APIs de Streaming.</span><span class="sxs-lookup"><span data-stu-id="cc58d-169">In order toodo so, it needs permission toocall hello Twitter Streaming APIs.</span></span> <span data-ttu-id="cc58d-170">tooconfigure que permissão, você cria um aplicativo no Twitter, que gera as credenciais exclusivas (por exemplo, um token de OAuth).</span><span class="sxs-lookup"><span data-stu-id="cc58d-170">tooconfigure that permission, you create an application in Twitter, which generates unique credentials (such as an OAuth token).</span></span> <span data-ttu-id="cc58d-171">Você pode configurar toouse de aplicativo cliente Olá essas credenciais ao fazer chamadas de API.</span><span class="sxs-lookup"><span data-stu-id="cc58d-171">You can then configure hello client application toouse these credentials when it makes API calls.</span></span> 

### <a name="create-a-twitter-application"></a><span data-ttu-id="cc58d-172">Criar um aplicativo do Twitter</span><span class="sxs-lookup"><span data-stu-id="cc58d-172">Create a Twitter application</span></span>
<span data-ttu-id="cc58d-173">Se você ainda não tiver um aplicativo do Twitter que você possa usar para este tutorial, você pode criar um.</span><span class="sxs-lookup"><span data-stu-id="cc58d-173">If you do not already have a Twitter application that you can use for this tutorial, you can create one.</span></span> <span data-ttu-id="cc58d-174">Você já deve ter uma conta do Twitter.</span><span class="sxs-lookup"><span data-stu-id="cc58d-174">You must already have a Twitter account.</span></span>

> [!NOTE]
> <span data-ttu-id="cc58d-175">exato do processo no Twitter para criar um aplicativo e obter o token, segredos e chaves de Olá Olá pode ser alterado.</span><span class="sxs-lookup"><span data-stu-id="cc58d-175">hello exact process in Twitter for creating an application and getting hello keys, secrets, and token might change.</span></span> <span data-ttu-id="cc58d-176">Se essas instruções não corresponderem, o que você vê no site do Twitter Olá, consulte a documentação do desenvolvedor do Twitter toohello.</span><span class="sxs-lookup"><span data-stu-id="cc58d-176">If these instructions don't match what you see on hello Twitter site, refer toohello Twitter developer documentation.</span></span>

1. <span data-ttu-id="cc58d-177">Vá toohello [página de gerenciamento de aplicativo do Twitter](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="cc58d-177">Go toohello [Twitter application management page](https://apps.twitter.com/).</span></span> 

2. <span data-ttu-id="cc58d-178">Crie um aplicativo novo.</span><span class="sxs-lookup"><span data-stu-id="cc58d-178">Create a new application.</span></span> 

    * <span data-ttu-id="cc58d-179">Para a URL do site hello, especifique uma URL válida.</span><span class="sxs-lookup"><span data-stu-id="cc58d-179">For hello website URL, specify a valid URL.</span></span> <span data-ttu-id="cc58d-180">Ele não tem toobe um site ativo.</span><span class="sxs-lookup"><span data-stu-id="cc58d-180">It does not have toobe a live site.</span></span> <span data-ttu-id="cc58d-181">(Você não pode especificar apenas `localhost`.)</span><span class="sxs-lookup"><span data-stu-id="cc58d-181">(You can't specify just `localhost`.)</span></span>
    * <span data-ttu-id="cc58d-182">Deixe o campo de retorno de chamada de saudação em branco.</span><span class="sxs-lookup"><span data-stu-id="cc58d-182">Leave hello callback field blank.</span></span> <span data-ttu-id="cc58d-183">aplicativo de cliente Hello que usar para este tutorial não requer retornos de chamada.</span><span class="sxs-lookup"><span data-stu-id="cc58d-183">hello client application you use for this tutorial doesn't require callbacks.</span></span>

    ![Criando um aplicativo no Twitter](./media/stream-analytics-twitter-sentiment-analysis-trends/create-twitter-application.png)

3. <span data-ttu-id="cc58d-185">Opcionalmente, altere as permissões do aplicativo hello somente tooread.</span><span class="sxs-lookup"><span data-stu-id="cc58d-185">Optionally, change hello application's permissions tooread-only.</span></span>

4. <span data-ttu-id="cc58d-186">Quando o aplicativo hello é criado, acesse toohello **chaves e Tokens de acesso** página.</span><span class="sxs-lookup"><span data-stu-id="cc58d-186">When hello application is created, go toohello **Keys and Access Tokens** page.</span></span>

5. <span data-ttu-id="cc58d-187">Clique em Olá botão toogenerate um token de acesso e o segredo do token de acesso.</span><span class="sxs-lookup"><span data-stu-id="cc58d-187">Click hello button toogenerate an access token and access token secret.</span></span>

<span data-ttu-id="cc58d-188">Mantenha essas informações úteis, pois você precisará no procedimento a seguir hello.</span><span class="sxs-lookup"><span data-stu-id="cc58d-188">Keep this information handy, because you will need it in hello next procedure.</span></span>

>[!NOTE]
><span data-ttu-id="cc58d-189">chaves de saudação e segredos do aplicativo do Twitter hello fornecem acesso tooyour Twitter conta.</span><span class="sxs-lookup"><span data-stu-id="cc58d-189">hello keys and secrets for hello Twitter application provide access tooyour Twitter account.</span></span> <span data-ttu-id="cc58d-190">Tratar essas informações como confidenciais, Olá mesmo como fazer sua senha do Twitter.</span><span class="sxs-lookup"><span data-stu-id="cc58d-190">Treat this information as sensitive, hello same as you do your Twitter password.</span></span> <span data-ttu-id="cc58d-191">Por exemplo, não insira essas informações em um aplicativo que você forneça tooothers.</span><span class="sxs-lookup"><span data-stu-id="cc58d-191">For example, don't embed this information in an application that you give tooothers.</span></span> 


### <a name="configure-hello-client-application"></a><span data-ttu-id="cc58d-192">Configurar o aplicativo de cliente hello</span><span class="sxs-lookup"><span data-stu-id="cc58d-192">Configure hello client application</span></span>
<span data-ttu-id="cc58d-193">Criamos um aplicativo cliente que se conecta tooTwitter dados usando [APIs de Streaming do Twitter](https://dev.twitter.com/streaming/overview) toocollect eventos de tweet sobre um conjunto específico de tópicos.</span><span class="sxs-lookup"><span data-stu-id="cc58d-193">We've created a client application that connects tooTwitter data using [Twitter's Streaming APIs](https://dev.twitter.com/streaming/overview) toocollect tweet events about a specific set of topics.</span></span> <span data-ttu-id="cc58d-194">usa o aplicativo Hello Olá [Sentiment140](http://help.sentiment140.com/) ferramenta de software livre, que atribui Olá tweet de tooeach do valor de sensibilidade a seguir:</span><span class="sxs-lookup"><span data-stu-id="cc58d-194">hello application uses hello [Sentiment140](http://help.sentiment140.com/) open source tool, which assigns hello following sentiment value tooeach tweet:</span></span>

* <span data-ttu-id="cc58d-195">0 = negativo</span><span class="sxs-lookup"><span data-stu-id="cc58d-195">0 = negative</span></span>
* <span data-ttu-id="cc58d-196">2 = neutro</span><span class="sxs-lookup"><span data-stu-id="cc58d-196">2 = neutral</span></span>
* <span data-ttu-id="cc58d-197">4 = positivo</span><span class="sxs-lookup"><span data-stu-id="cc58d-197">4 = positive</span></span>

<span data-ttu-id="cc58d-198">Depois de eventos de tweet Olá atribuiu um valor de sensibilidade, eles são enviados por push toohello hub de eventos que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cc58d-198">After hello tweet events have been assigned a sentiment value, they are pushed toohello event hub that you created earlier.</span></span>

<span data-ttu-id="cc58d-199">Antes que o aplicativo hello é executado, ele requer certas informações, como chaves de Twitter hello e cadeia de conexão de hub de evento hello.</span><span class="sxs-lookup"><span data-stu-id="cc58d-199">Before hello application runs, it requires certain information from you, like hello Twitter keys and hello event hub connection string.</span></span> <span data-ttu-id="cc58d-200">Você pode fornecer informações de configuração de saudação das seguintes maneiras:</span><span class="sxs-lookup"><span data-stu-id="cc58d-200">You can provide hello configuration information in these ways:</span></span>

* <span data-ttu-id="cc58d-201">Executar o aplicativo hello e use do aplicativo hello da interface do usuário tooenter Olá chaves, segredos e cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="cc58d-201">Run hello application, and then use hello application's UI tooenter hello keys, secrets, and connection string.</span></span> <span data-ttu-id="cc58d-202">Se você fizer isso, as informações de configuração de saudação são usadas para a sessão atual, mas não serão salvas.</span><span class="sxs-lookup"><span data-stu-id="cc58d-202">If you do this, hello configuration information is used for your current session, but it isn't saved.</span></span>
* <span data-ttu-id="cc58d-203">Edite o arquivo. config do aplicativo hello e conjunto de valores de saudação nela.</span><span class="sxs-lookup"><span data-stu-id="cc58d-203">Edit hello application's .config file and set hello values there.</span></span> <span data-ttu-id="cc58d-204">Essa abordagem persiste nas informações de configuração hello, mas isso também significa que essas informações potencialmente confidenciais e são armazenadas em texto sem formatação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="cc58d-204">This approach persists hello configuration information, but it also means that this potentially sensitive information is stored in plain text on your computer.</span></span>

<span data-ttu-id="cc58d-205">Olá procedimento a seguir documenta as duas abordagens.</span><span class="sxs-lookup"><span data-stu-id="cc58d-205">hello following procedure documents both approaches.</span></span> 

1. <span data-ttu-id="cc58d-206">Verifique se você baixou e descompactado Olá [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) aplicativo, conforme listado na pré-requisitos hello.</span><span class="sxs-lookup"><span data-stu-id="cc58d-206">Make sure you've downloaded and unzipped hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) application, as listed in hello prerequisites.</span></span>

2. <span data-ttu-id="cc58d-207">tooset Olá valores em tempo de execução (e apenas Olá sessão atual), execute Olá `TwitterWPFClient.exe` aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cc58d-207">tooset hello values at run time (and only for hello current session), run hello `TwitterWPFClient.exe` application.</span></span> <span data-ttu-id="cc58d-208">Quando o aplicativo hello solicita, digite Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="cc58d-208">When hello application prompts you, enter hello following values:</span></span>

    * <span data-ttu-id="cc58d-209">Olá chave do consumidor do Twitter (chave de API).</span><span class="sxs-lookup"><span data-stu-id="cc58d-209">hello Twitter Consumer Key (API Key).</span></span>
    * <span data-ttu-id="cc58d-210">Olá segredo de consumidor no Twitter (segredo de API).</span><span class="sxs-lookup"><span data-stu-id="cc58d-210">hello Twitter Consumer Secret (API Secret).</span></span>
    * <span data-ttu-id="cc58d-211">saudação do Token de acesso do Twitter.</span><span class="sxs-lookup"><span data-stu-id="cc58d-211">hello Twitter Access Token.</span></span>
    * <span data-ttu-id="cc58d-212">Olá Twitter segredo do Token de acesso.</span><span class="sxs-lookup"><span data-stu-id="cc58d-212">hello Twitter Access Token Secret.</span></span>
    * <span data-ttu-id="cc58d-213">Olá conexão informações da cadeia que você salvou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cc58d-213">hello connection string information that you saved earlier.</span></span> <span data-ttu-id="cc58d-214">Certifique-se de que você use a cadeia de caracteres de conexão de saudação que você removeu Olá `EntityPath` par chave-valor do.</span><span class="sxs-lookup"><span data-stu-id="cc58d-214">Make sure that you use hello connection string that you removed hello `EntityPath` key-value pair from.</span></span>
    * <span data-ttu-id="cc58d-215">Olá Twitter palavras-chave que você deseja que o sentimento toodetermine para.</span><span class="sxs-lookup"><span data-stu-id="cc58d-215">hello Twitter keywords that you want toodetermine sentiment for.</span></span>

   ![Aplicativo TwitterWpfClient em execução, mostrando as configurações obscuras](./media/stream-analytics-twitter-sentiment-analysis-trends/wpfclientlines.png)

3. <span data-ttu-id="cc58d-217">os valores hello tooset persistente, usam um texto editor tooopen Olá TwitterWpfClient.exe.config.</span><span class="sxs-lookup"><span data-stu-id="cc58d-217">tooset hello values persistently, use a text editor tooopen hello TwitterWpfClient.exe.config file.</span></span> <span data-ttu-id="cc58d-218">Em seguida, em Olá `<appSettings>` elemento, fazer isso:</span><span class="sxs-lookup"><span data-stu-id="cc58d-218">Then in hello `<appSettings>` element, do this:</span></span>

    * <span data-ttu-id="cc58d-219">Definir `oauth_consumer_key` toohello chave do consumidor do Twitter (chave de API).</span><span class="sxs-lookup"><span data-stu-id="cc58d-219">Set `oauth_consumer_key` toohello Twitter Consumer Key (API Key).</span></span> 
    * <span data-ttu-id="cc58d-220">Definir `oauth_consumer_secret` toohello segredo de consumidor no Twitter (segredo de API).</span><span class="sxs-lookup"><span data-stu-id="cc58d-220">Set `oauth_consumer_secret` toohello Twitter Consumer Secret (API Secret).</span></span>
    * <span data-ttu-id="cc58d-221">Definir `oauth_token` toohello Token de acesso do Twitter.</span><span class="sxs-lookup"><span data-stu-id="cc58d-221">Set `oauth_token` toohello Twitter Access Token.</span></span>
    * <span data-ttu-id="cc58d-222">Definir `oauth_token_secret` toohello Twitter segredo do Token de acesso.</span><span class="sxs-lookup"><span data-stu-id="cc58d-222">Set `oauth_token_secret` toohello Twitter Access Token Secret.</span></span>

    <span data-ttu-id="cc58d-223">Mais adiante Olá `<appSettings>` elemento, fazer essas alterações:</span><span class="sxs-lookup"><span data-stu-id="cc58d-223">Later in hello `<appSettings>` element, make these changes:</span></span>

    * <span data-ttu-id="cc58d-224">Definir `EventHubName` toohello nome do hub de evento (ou seja, o valor de toohello do caminho de entidade Olá).</span><span class="sxs-lookup"><span data-stu-id="cc58d-224">Set `EventHubName` toohello event hub name (that is, toohello value of hello entity path).</span></span>
    * <span data-ttu-id="cc58d-225">Definir `EventHubNameConnectionString` toohello cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="cc58d-225">Set `EventHubNameConnectionString` toohello connection string.</span></span> <span data-ttu-id="cc58d-226">Certifique-se de que você use a cadeia de caracteres de conexão de saudação que você removeu Olá `EntityPath` par chave-valor do.</span><span class="sxs-lookup"><span data-stu-id="cc58d-226">Make sure that you use hello connection string that you removed hello `EntityPath` key-value pair from.</span></span>

    <span data-ttu-id="cc58d-227">Olá `<appSettings>` seção aparência Olá exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="cc58d-227">hello `<appSettings>` section looks like hello following example.</span></span> <span data-ttu-id="cc58d-228">(Para maior clareza e segurança, nós encapsulamos algumas linhas e removemos alguns caracteres.)</span><span class="sxs-lookup"><span data-stu-id="cc58d-228">(For clarity and security, we wrapped some lines and removed some characters.)</span></span>

    ![Arquivo de configuração de aplicativo TwitterWpfClient em um editor de texto, mostrando as chaves do Twitter hello e segredos e informações de cadeia de caracteres de conexão de hub do hello evento](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-tiwtter-app-config.png)
 
4. <span data-ttu-id="cc58d-230">Se você já não iniciar o aplicativo hello, execute TwitterWpfClient.exe agora.</span><span class="sxs-lookup"><span data-stu-id="cc58d-230">If you didn't already start hello application, run TwitterWpfClient.exe now.</span></span> 

5. <span data-ttu-id="cc58d-231">Clique em sentimento social de toocollect Olá de botão Verde Iniciar.</span><span class="sxs-lookup"><span data-stu-id="cc58d-231">Click hello green start button toocollect social sentiment.</span></span> <span data-ttu-id="cc58d-232">Consulte eventos Tweet com hello **criadona**, **tópico**, e **SentimentScore** valores que estão sendo enviados tooyour hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="cc58d-232">You see Tweet events with hello **CreatedAt**, **Topic**, and **SentimentScore** values being sent tooyour event hub.</span></span>

    ![Aplicativo TwitterWpfClient em execução, mostrando as listagem de tweets](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-app-listing.png)

    >[!NOTE]
    ><span data-ttu-id="cc58d-234">Se você encontrar erros, e você não vir um fluxo de tweets exibido na parte inferior de saudação da janela hello, verifique novamente os segredos e chaves de saudação.</span><span class="sxs-lookup"><span data-stu-id="cc58d-234">If you see errors, and you don't see a stream of tweets displayed in hello lower part of hello window, double-check hello keys and secrets.</span></span> <span data-ttu-id="cc58d-235">Verifique também a cadeia de caracteres de conexão de saudação (certifique-se de que ele não inclui Olá `EntityPath` chave e valor.)</span><span class="sxs-lookup"><span data-stu-id="cc58d-235">Also check hello connection string (make sure that it does not include hello `EntityPath` key and value.)</span></span>


## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="cc58d-236">Criar um trabalho de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cc58d-236">Create a Stream Analytics job</span></span>

<span data-ttu-id="cc58d-237">Agora que os eventos tweet são streaming em tempo real do Twitter, você pode configurar um tooanalyze de trabalho do Stream Analytics esses eventos em tempo real.</span><span class="sxs-lookup"><span data-stu-id="cc58d-237">Now that tweet events are streaming in real time from Twitter, you can set up a Stream Analytics job tooanalyze these events in real time.</span></span>

1. <span data-ttu-id="cc58d-238">No portal do Azure de Olá, clique em **novo** > **Internet das coisas** > **trabalho do Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="cc58d-238">In hello Azure portal, click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>

2. <span data-ttu-id="cc58d-239">Nome do trabalho Olá `socialtwitter-sa-job` e especificar uma assinatura, o grupo de recursos e o local.</span><span class="sxs-lookup"><span data-stu-id="cc58d-239">Name hello job `socialtwitter-sa-job` and specify a subscription, resource group, and location.</span></span>

    <span data-ttu-id="cc58d-240">É uma boa ideia tooplace Olá trabalho e hello hub de evento Olá mesma região para melhor desempenho e, portanto, que não é necessário pagar tootransfer dados entre regiões.</span><span class="sxs-lookup"><span data-stu-id="cc58d-240">It's a good idea tooplace hello job and hello event hub in hello same region for best performance and so that you don't pay tootransfer data between regions.</span></span>

    ![Criando um novo trabalho do Stream Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/newjob.png)

3. <span data-ttu-id="cc58d-242">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="cc58d-242">Click **Create**.</span></span>

    <span data-ttu-id="cc58d-243">Olá trabalho é criado e o portal de saudação exibe detalhes do trabalho.</span><span class="sxs-lookup"><span data-stu-id="cc58d-243">hello job is created and hello portal displays job details.</span></span>


## <a name="specify-hello-job-input"></a><span data-ttu-id="cc58d-244">Especificar a entrada de trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="cc58d-244">Specify hello job input</span></span>

1. <span data-ttu-id="cc58d-245">Em seu trabalho de análise de fluxo, em **trabalho topologia** no meio de saudação da folha de trabalho hello, clique em **entradas**.</span><span class="sxs-lookup"><span data-stu-id="cc58d-245">In your Stream Analytics job, under **Job Topology** in hello middle of hello job blade, click **Inputs**.</span></span> 

2. <span data-ttu-id="cc58d-246">Em Olá **entradas** folha, clique em  **+ &nbsp;adicionar** e, em seguida, preencha a folha Olá com estes valores:</span><span class="sxs-lookup"><span data-stu-id="cc58d-246">In hello **Inputs** blade, click **+&nbsp;Add** and then fill out hello blade with these values:</span></span>

    * <span data-ttu-id="cc58d-247">**Alias de entrada**: Use o nome de saudação `TwitterStream`.</span><span class="sxs-lookup"><span data-stu-id="cc58d-247">**Input alias**: Use hello name `TwitterStream`.</span></span> <span data-ttu-id="cc58d-248">Se você usar um nome diferente, anote-o porque você precisará dele depois.</span><span class="sxs-lookup"><span data-stu-id="cc58d-248">If you use a different name, make a note of it because you need it later.</span></span>
    * <span data-ttu-id="cc58d-249">**Tipo de Origem**: Selecione **Fluxo de Dados**.</span><span class="sxs-lookup"><span data-stu-id="cc58d-249">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="cc58d-250">**Origem**: Selecione **Hub de Eventos**.</span><span class="sxs-lookup"><span data-stu-id="cc58d-250">**Source**: Select **Event hub**.</span></span>
    * <span data-ttu-id="cc58d-251">**Opção de importação**: Selecione **Usar hub de evento da assinatura atual**.</span><span class="sxs-lookup"><span data-stu-id="cc58d-251">**Import option**: Select **Use event hub from current subscription**.</span></span> 
    * <span data-ttu-id="cc58d-252">**Namespace de barramento de serviço**: selecione Olá namespace de hub de eventos que você criou anteriormente (`<yourname>-socialtwitter-eh-ns`).</span><span class="sxs-lookup"><span data-stu-id="cc58d-252">**Service bus namespace**: Select hello event hub namespace that you created earlier (`<yourname>-socialtwitter-eh-ns`).</span></span>
    * <span data-ttu-id="cc58d-253">**Hub de eventos**: hub de eventos Olá selecione que você criou anteriormente (`socialtwitter-eh`).</span><span class="sxs-lookup"><span data-stu-id="cc58d-253">**Event hub**: Select hello event hub that you created earlier (`socialtwitter-eh`).</span></span>
    * <span data-ttu-id="cc58d-254">**Nome de política do hub de evento**: selecione a política de acesso de saudação que você criou anteriormente (`socialtwitter-access`).</span><span class="sxs-lookup"><span data-stu-id="cc58d-254">**Event hub policy name**: Select hello access policy that you created earlier (`socialtwitter-access`).</span></span>

    ![Criar nova entrada para o trabalho de Streaming Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-new-input.png)

3. <span data-ttu-id="cc58d-256">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="cc58d-256">Click **Create**.</span></span>


## <a name="specify-hello-job-query"></a><span data-ttu-id="cc58d-257">Especifique a consulta de trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="cc58d-257">Specify hello job query</span></span>

<span data-ttu-id="cc58d-258">O Stream Analytics dá suporte a um modelo de consulta simples e declarativo que descreve as transformações.</span><span class="sxs-lookup"><span data-stu-id="cc58d-258">Stream Analytics supports a simple, declarative query model that describes transformations.</span></span> <span data-ttu-id="cc58d-259">toolearn mais sobre a linguagem hello, consulte Olá [referência de linguagem do Azure Stream Analytics consulta](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span><span class="sxs-lookup"><span data-stu-id="cc58d-259">toolearn more about hello language, see hello [Azure Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>  <span data-ttu-id="cc58d-260">Este tutorial ajuda você a criar e testar várias consultas sobre dados do Twitter.</span><span class="sxs-lookup"><span data-stu-id="cc58d-260">This tutorial helps you author and test several queries over Twitter data.</span></span>

<span data-ttu-id="cc58d-261">número de saudação do toocompare de menções entre tópicos, você pode usar um [janela em cascata](https://msdn.microsoft.com/library/azure/dn835055.aspx) tooget contagem de saudação do menções por tópico cada cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="cc58d-261">toocompare hello number of mentions among topics, you can use a [Tumbling window](https://msdn.microsoft.com/library/azure/dn835055.aspx) tooget hello count of mentions by topic every five seconds.</span></span>

1. <span data-ttu-id="cc58d-262">Olá fechar **entradas** folha se ainda não o fez.</span><span class="sxs-lookup"><span data-stu-id="cc58d-262">Close hello **Inputs** blade if you haven't already.</span></span>

2. <span data-ttu-id="cc58d-263">Na folha de trabalho hello, clique em Olá **consulta** caixa.</span><span class="sxs-lookup"><span data-stu-id="cc58d-263">In hello job blade, click hello **Query** box.</span></span> <span data-ttu-id="cc58d-264">Azure lista entradas hello e saídas que são configuradas para trabalho hello e permite que você crie uma consulta que permite transform o fluxo de entrada hello como saída toohello é enviado.</span><span class="sxs-lookup"><span data-stu-id="cc58d-264">Azure lists hello inputs and outputs that are configured for hello job, and lets you create a query that lets you transform hello input stream as it is sent toohello output.</span></span>

3. <span data-ttu-id="cc58d-265">Certifique-se de que Olá TwitterWpfClient aplicativo está em execução.</span><span class="sxs-lookup"><span data-stu-id="cc58d-265">Make sure that hello TwitterWpfClient application is running.</span></span> 

3. <span data-ttu-id="cc58d-266">Em hello **consulta** folha, clique em Olá pontos próximo toohello `TwitterStream` de entrada e, em seguida, selecione **dados de entrada de exemplo**.</span><span class="sxs-lookup"><span data-stu-id="cc58d-266">In hello **Query** blade, click hello dots next toohello `TwitterStream` input and then select **Sample data from input**.</span></span>

    ![Dados de exemplo do menu Opções toouse para Olá análise de fluxo de trabalho da entrada, "Dados de exemplo de entrada" selecionados](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-sample-data-from-input.png)

    <span data-ttu-id="cc58d-268">Isso abrirá uma folha que permite que você especifique a quantidade tooget de dados de exemplo, definida em termos de quanto tempo o fluxo de entrada hello tooread.</span><span class="sxs-lookup"><span data-stu-id="cc58d-268">This opens a blade that lets you specify how much sample data tooget, defined in terms of how long tooread hello input stream.</span></span>

4. <span data-ttu-id="cc58d-269">Definir **minutos** too3 e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="cc58d-269">Set **Minutes** too3 and then click **OK**.</span></span> 
    
    ![Opções de amostragem de fluxo de entrada hello, com "3 minutos" selecionados.](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-input-create-sample-data.png)

    <span data-ttu-id="cc58d-271">O Azure amostras de amostra de dados de fluxo de entrada hello de 3 minutos e notifica você quando os dados de exemplo hello estão prontos.</span><span class="sxs-lookup"><span data-stu-id="cc58d-271">Azure samples 3 minutes' worth of data from hello input stream and notifies you when hello sample data is ready.</span></span> <span data-ttu-id="cc58d-272">(Isso pode levar um tempo.)</span><span class="sxs-lookup"><span data-stu-id="cc58d-272">(This takes a short while.)</span></span> 

    <span data-ttu-id="cc58d-273">dados de exemplo Hello são armazenados temporariamente e estão disponíveis enquanto janela de consulta Olá aberto.</span><span class="sxs-lookup"><span data-stu-id="cc58d-273">hello sample data is stored temporarily and is available while you have hello query window open.</span></span> <span data-ttu-id="cc58d-274">Se você fechar a janela de consulta Olá, dados de exemplo hello serão descartados e você tiver toocreate um novo conjunto de dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="cc58d-274">If you close hello query window, hello sample data is discarded, and you have toocreate a new set of sample data.</span></span> 

5. <span data-ttu-id="cc58d-275">Alterar consulta Olá Olá código editor toohello seguinte:</span><span class="sxs-lookup"><span data-stu-id="cc58d-275">Change hello query in hello code editor toohello following:</span></span>

    ```
    SELECT System.Timestamp as Time, Topic, COUNT(*)
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY TUMBLINGWINDOW(s, 5), Topic
    ```

    <span data-ttu-id="cc58d-276">Se não usar `TwitterStream` como Olá alias de entrada hello, substitua o alias para `TwitterStream` na consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="cc58d-276">If didn't use `TwitterStream` as hello alias for hello input, substitute your alias for `TwitterStream` in hello query.</span></span>  

    <span data-ttu-id="cc58d-277">Essa consulta usa Olá **TIMESTAMP BY** toospecify de palavra-chave um campo de carimbo de hora no hello carga toobe usado no cálculo temporal hello.</span><span class="sxs-lookup"><span data-stu-id="cc58d-277">This query uses hello **TIMESTAMP BY** keyword toospecify a timestamp field in hello payload toobe used in hello temporal computation.</span></span> <span data-ttu-id="cc58d-278">Se esse campo não for especificado, a operação de janelas de saudação é executada usando o tempo de saudação que cada evento chegou ao hub de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="cc58d-278">If this field isn't specified, hello windowing operation is performed by using hello time that each event arrived at hello event hub.</span></span> <span data-ttu-id="cc58d-279">Saiba mais na seção hello "tempo de chegada vs hora do aplicativo" [referência de consulta do Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span><span class="sxs-lookup"><span data-stu-id="cc58d-279">Learn more in hello "Arrival Time vs Application Time" section of [Stream Analytics Query Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>

    <span data-ttu-id="cc58d-280">Essa consulta também acessa um carimbo de hora de término hello de cada janela usando Olá **timestamp** propriedade.</span><span class="sxs-lookup"><span data-stu-id="cc58d-280">This query also accesses a timestamp for hello end of each window by using hello **System.Timestamp** property.</span></span>

5. <span data-ttu-id="cc58d-281">Clique em **Testar**.</span><span class="sxs-lookup"><span data-stu-id="cc58d-281">Click **Test**.</span></span> <span data-ttu-id="cc58d-282">consulta de saudação é executada em relação aos dados Olá você de amostra.</span><span class="sxs-lookup"><span data-stu-id="cc58d-282">hello query runs against hello data that you sampled.</span></span>
    
6. <span data-ttu-id="cc58d-283">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="cc58d-283">Click **Save**.</span></span> <span data-ttu-id="cc58d-284">Isso economiza consulta hello como parte do trabalho de análise de fluxo contínuo de saudação.</span><span class="sxs-lookup"><span data-stu-id="cc58d-284">This saves hello query as part of hello Streaming Analytics job.</span></span> <span data-ttu-id="cc58d-285">(Ele não salva os dados de exemplo hello.)</span><span class="sxs-lookup"><span data-stu-id="cc58d-285">(It doesn't save hello sample data.)</span></span>


## <a name="experiment-using-different-fields-from-hello-stream"></a><span data-ttu-id="cc58d-286">Experimente usar diferentes campos de fluxo de saudação</span><span class="sxs-lookup"><span data-stu-id="cc58d-286">Experiment using different fields from hello stream</span></span> 

<span data-ttu-id="cc58d-287">Olá tabela a seguir lista os campos de saudação que fazem parte da saudação fluxo de dados JSON.</span><span class="sxs-lookup"><span data-stu-id="cc58d-287">hello following table lists hello fields that are part of hello JSON streaming data.</span></span> <span data-ttu-id="cc58d-288">Sinta-se livre tooexperiment no editor de consultas de saudação.</span><span class="sxs-lookup"><span data-stu-id="cc58d-288">Feel free tooexperiment in hello query editor.</span></span>

|<span data-ttu-id="cc58d-289">Propriedade JSON</span><span class="sxs-lookup"><span data-stu-id="cc58d-289">JSON property</span></span> | <span data-ttu-id="cc58d-290">Definição</span><span class="sxs-lookup"><span data-stu-id="cc58d-290">Definition</span></span>|
|--- | ---|
|<span data-ttu-id="cc58d-291">CreatedAt</span><span class="sxs-lookup"><span data-stu-id="cc58d-291">CreatedAt</span></span> | <span data-ttu-id="cc58d-292">tempo de saudação que tweet Olá foi criado</span><span class="sxs-lookup"><span data-stu-id="cc58d-292">hello time that hello tweet was created</span></span>|
|<span data-ttu-id="cc58d-293">Tópico</span><span class="sxs-lookup"><span data-stu-id="cc58d-293">Topic</span></span> | <span data-ttu-id="cc58d-294">tópico de saudação que corresponde a saudação especificado palavra-chave</span><span class="sxs-lookup"><span data-stu-id="cc58d-294">hello topic that matches hello specified keyword</span></span>|
|<span data-ttu-id="cc58d-295">SentimentScore</span><span class="sxs-lookup"><span data-stu-id="cc58d-295">SentimentScore</span></span> | <span data-ttu-id="cc58d-296">pontuação de sensibilidade de saudação do Sentiment140</span><span class="sxs-lookup"><span data-stu-id="cc58d-296">hello sentiment score from Sentiment140</span></span>|
|<span data-ttu-id="cc58d-297">Autor</span><span class="sxs-lookup"><span data-stu-id="cc58d-297">Author</span></span> | <span data-ttu-id="cc58d-298">Identificador do Twitter Olá que enviou tweet Olá</span><span class="sxs-lookup"><span data-stu-id="cc58d-298">hello Twitter handle that sent hello tweet</span></span>|
|<span data-ttu-id="cc58d-299">Texto</span><span class="sxs-lookup"><span data-stu-id="cc58d-299">Text</span></span> | <span data-ttu-id="cc58d-300">corpo completo de saudação do tweet Olá</span><span class="sxs-lookup"><span data-stu-id="cc58d-300">hello full body of hello tweet</span></span>|


## <a name="create-an-output-sink"></a><span data-ttu-id="cc58d-301">Criar um coletor de saída</span><span class="sxs-lookup"><span data-stu-id="cc58d-301">Create an output sink</span></span>

<span data-ttu-id="cc58d-302">Agora você definiu um fluxo de eventos, uma entrada tooingest do hub de eventos e uma consulta tooperform uma transformação em fluxo hello.</span><span class="sxs-lookup"><span data-stu-id="cc58d-302">You have now defined an event stream, an event hub input tooingest events, and a query tooperform a transformation over hello stream.</span></span> <span data-ttu-id="cc58d-303">Olá última etapa é toodefine um coletor de saída para o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="cc58d-303">hello last step is toodefine an output sink for hello job.</span></span>  

<span data-ttu-id="cc58d-304">Neste tutorial, você pode escrever Olá agregado tweet eventos da saudação trabalho consulta tooAzure armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="cc58d-304">In this tutorial, you write hello aggregated tweet events from hello job query tooAzure Blob storage.</span></span>  <span data-ttu-id="cc58d-305">Você também pode enviar seu resultados tooAzure banco de dados SQL, armazenamento de tabela do Azure, os Hubs de eventos, ou Power BI, dependendo do seu aplicativo precisa.</span><span class="sxs-lookup"><span data-stu-id="cc58d-305">You can also push your results tooAzure SQL Database, Azure Table storage, Event Hubs, or Power BI, depending on your application needs.</span></span>

## <a name="specify-hello-job-output"></a><span data-ttu-id="cc58d-306">Especifique a saída do trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="cc58d-306">Specify hello job output</span></span>

1. <span data-ttu-id="cc58d-307">Em Olá **trabalho topologia** seção, clique em Olá **saída** caixa.</span><span class="sxs-lookup"><span data-stu-id="cc58d-307">In hello **Job Topology** section, click hello **Output** box.</span></span> 

2. <span data-ttu-id="cc58d-308">Em Olá **saídas** folha, clique em  **+ &nbsp;adicionar** e, em seguida, preencha a folha Olá com estes valores:</span><span class="sxs-lookup"><span data-stu-id="cc58d-308">In hello **Outputs** blade, click **+&nbsp;Add** and then fill out hello blade with these values:</span></span>

    * <span data-ttu-id="cc58d-309">**Alias de saída**: Use o nome de saudação `TwitterStream-Output`.</span><span class="sxs-lookup"><span data-stu-id="cc58d-309">**Output alias**: Use hello name `TwitterStream-Output`.</span></span> 
    * <span data-ttu-id="cc58d-310">**Coletor**: selecione **Armazenamento de blobs**.</span><span class="sxs-lookup"><span data-stu-id="cc58d-310">**Sink**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="cc58d-311">**Opções de importação**: Selecione **Usar armazenamento de blobs da assinatura atual**.</span><span class="sxs-lookup"><span data-stu-id="cc58d-311">**Import options**: Select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="cc58d-312">**Conta de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="cc58d-312">**Storage account**.</span></span> <span data-ttu-id="cc58d-313">Selecione **Criar uma nova conta de armazenamento.**</span><span class="sxs-lookup"><span data-stu-id="cc58d-313">Select **Create a new storage account.**</span></span>
    * <span data-ttu-id="cc58d-314">**Conta de armazenamento** (segunda caixa).</span><span class="sxs-lookup"><span data-stu-id="cc58d-314">**Storage account** (second box).</span></span> <span data-ttu-id="cc58d-315">Digite `YOURNAMEsa`, onde `YOURNAME` é o seu nome ou outra cadeia de caracteres exclusiva.</span><span class="sxs-lookup"><span data-stu-id="cc58d-315">Enter `YOURNAMEsa`, where `YOURNAME` is your name or another unique string.</span></span> <span data-ttu-id="cc58d-316">nome de saudação pode usar apenas letras minúsculas e números e deve ser exclusivo no Azure.</span><span class="sxs-lookup"><span data-stu-id="cc58d-316">hello name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 
    * <span data-ttu-id="cc58d-317">**Contêiner**.</span><span class="sxs-lookup"><span data-stu-id="cc58d-317">**Container**.</span></span> <span data-ttu-id="cc58d-318">Digite `socialtwitter`.</span><span class="sxs-lookup"><span data-stu-id="cc58d-318">Enter `socialtwitter`.</span></span>
    <span data-ttu-id="cc58d-319">nome de conta de armazenamento Hello e o nome do contêiner são tooprovide usado junto um URI para o armazenamento de blob hello, como este:</span><span class="sxs-lookup"><span data-stu-id="cc58d-319">hello storage account name and container name are used together tooprovide a URI for hello blob storage, like this:</span></span> 

    `http://YOURNAMEsa.blob.core.windows.net/socialtwitter/...`
    
    ![Folha "Nova saída" para trabalho do Stream Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-output-blob-storage.png)
    
4. <span data-ttu-id="cc58d-321">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="cc58d-321">Click **Create**.</span></span> 

    <span data-ttu-id="cc58d-322">Azure cria a conta de armazenamento hello e gera uma chave automaticamente.</span><span class="sxs-lookup"><span data-stu-id="cc58d-322">Azure creates hello storage account and generates a key automatically.</span></span> 

5. <span data-ttu-id="cc58d-323">Olá fechar **saídas** folha.</span><span class="sxs-lookup"><span data-stu-id="cc58d-323">Close hello **Outputs** blade.</span></span> 


## <a name="start-hello-job"></a><span data-ttu-id="cc58d-324">Iniciar trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="cc58d-324">Start hello job</span></span>

<span data-ttu-id="cc58d-325">Uma entrada de trabalho, uma consulta e uma saída são especificadas.</span><span class="sxs-lookup"><span data-stu-id="cc58d-325">A job input, query, and output are specified.</span></span> <span data-ttu-id="cc58d-326">Você está pronto toostart Olá Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="cc58d-326">You are ready toostart hello Stream Analytics job.</span></span>

1. <span data-ttu-id="cc58d-327">Certifique-se de que Olá TwitterWpfClient aplicativo está em execução.</span><span class="sxs-lookup"><span data-stu-id="cc58d-327">Make sure that hello TwitterWpfClient application is running.</span></span> 

2. <span data-ttu-id="cc58d-328">Na folha de trabalho hello, clique em **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="cc58d-328">In hello job blade, click **Start**.</span></span>

    ![Iniciar o trabalho de análise de fluxo de saudação](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-output.png)

3. <span data-ttu-id="cc58d-330">Em Olá **Iniciar trabalho** folha, para **hora de início da saída de trabalho**, selecione **agora** e, em seguida, clique em **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="cc58d-330">In hello **Start job** blade, for **Job output start time**, select **Now** and then click **Start**.</span></span> 

    ![Folha "Iniciar o trabalho" para o trabalho de análise de fluxo de saudação](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-job-blade.png)

    <span data-ttu-id="cc58d-332">Azure notifica quando o trabalho Olá foi iniciado e, na folha de trabalho hello, status de saudação é exibido como **executando**.</span><span class="sxs-lookup"><span data-stu-id="cc58d-332">Azure notifies you when hello job has started, and in hello job blade, hello status is displayed as **Running**.</span></span>

    ![Trabalho em execução](./media/stream-analytics-twitter-sentiment-analysis-trends/jobrunning.png)

## <a name="view-output-for-sentiment-analysis"></a><span data-ttu-id="cc58d-334">Exibir saída para análise sentimento</span><span class="sxs-lookup"><span data-stu-id="cc58d-334">View output for sentiment analysis</span></span>

<span data-ttu-id="cc58d-335">Depois que seu trabalho inicia a execução e processamento de fluxo em tempo real de Twitter hello, você pode exibir a saída de saudação para análise de sentimento.</span><span class="sxs-lookup"><span data-stu-id="cc58d-335">After your job has started running and is processing hello real-time Twitter stream, you can view hello output for sentiment analysis.</span></span>

<span data-ttu-id="cc58d-336">Você pode usar uma ferramenta como [Azure Storage Explorer](https://http://storageexplorer.com/) ou [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction) tooview seu trabalho de saída em tempo real.</span><span class="sxs-lookup"><span data-stu-id="cc58d-336">You can use a tool like [Azure Storage Explorer](https://http://storageexplorer.com/) or [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction) tooview your job output in real time.</span></span> <span data-ttu-id="cc58d-337">A partir daqui, você pode usar [Power BI](https://powerbi.com/) tooextend tooinclude seu aplicativo um painel personalizado, como Olá mostrada na Olá captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="cc58d-337">From here, you can use [Power BI](https://powerbi.com/) tooextend your application tooinclude a customized dashboard like hello one shown in hello following screenshot:</span></span>

![Power BI](./media/stream-analytics-twitter-sentiment-analysis-trends/power-bi.png)


## <a name="create-another-query-tooidentify-trending-topics"></a><span data-ttu-id="cc58d-339">Criar outra consulta tooidentify tópicos de análise de tendências</span><span class="sxs-lookup"><span data-stu-id="cc58d-339">Create another query tooidentify trending topics</span></span>

<span data-ttu-id="cc58d-340">Outra consulta, você pode usar o sentimento do Twitter toounderstand baseia-se em uma [janela deslizante](https://msdn.microsoft.com/library/azure/dn835051.aspx).</span><span class="sxs-lookup"><span data-stu-id="cc58d-340">Another query you can use toounderstand Twitter sentiment is based on a [Sliding Window](https://msdn.microsoft.com/library/azure/dn835051.aspx).</span></span> <span data-ttu-id="cc58d-341">tópicos de análise de tendências tooidentify, pesquisar tópicos que entre um valor de limite para menções em um período de tempo especificado.</span><span class="sxs-lookup"><span data-stu-id="cc58d-341">tooidentify trending topics, you look for topics that cross a threshold value for mentions in a specified amount of time.</span></span>

<span data-ttu-id="cc58d-342">Para fins de saudação deste tutorial, você deve verificar tópicos mencionados mais de 20 vezes Olá últimos 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="cc58d-342">For hello purposes of this tutorial, you check for topics that are mentioned more than 20 times in hello last 5 seconds.</span></span>

1. <span data-ttu-id="cc58d-343">Na folha de trabalho hello, clique em **parar** toostop trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="cc58d-343">In hello job blade, click **Stop** toostop hello job.</span></span> 

2. <span data-ttu-id="cc58d-344">Em Olá **trabalho topologia** seção, clique em Olá **consulta** caixa.</span><span class="sxs-lookup"><span data-stu-id="cc58d-344">In hello **Job Topology** section, click hello **Query** box.</span></span> 

3. <span data-ttu-id="cc58d-345">Alterar a seguir Olá consulta toohello:</span><span class="sxs-lookup"><span data-stu-id="cc58d-345">Change hello query toohello following:</span></span>

    ```    
    SELECT System.Timestamp as Time, Topic, COUNT(*) as Mentions
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY SLIDINGWINDOW(s, 5), topic
    HAVING COUNT(*) > 20
    ```

4. <span data-ttu-id="cc58d-346">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="cc58d-346">Click **Save**.</span></span>

5. <span data-ttu-id="cc58d-347">Certifique-se de que Olá TwitterWpfClient aplicativo está em execução.</span><span class="sxs-lookup"><span data-stu-id="cc58d-347">Make sure that hello TwitterWpfClient application is running.</span></span> 

6. <span data-ttu-id="cc58d-348">Clique em **iniciar** toorestart Olá trabalho nova consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="cc58d-348">Click **Start** toorestart hello job using hello new query.</span></span>


## <a name="get-support"></a><span data-ttu-id="cc58d-349">Obtenha suporte</span><span class="sxs-lookup"><span data-stu-id="cc58d-349">Get support</span></span>
<span data-ttu-id="cc58d-350">Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="cc58d-350">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc58d-351">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cc58d-351">Next steps</span></span>
* [<span data-ttu-id="cc58d-352">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cc58d-352">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="cc58d-353">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="cc58d-353">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="cc58d-354">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="cc58d-354">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="cc58d-355">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="cc58d-355">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="cc58d-356">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cc58d-356">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
