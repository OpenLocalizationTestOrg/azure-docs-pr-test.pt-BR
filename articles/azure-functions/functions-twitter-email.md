---
title: "aaaCreate uma função que se integra com aplicativos de lógica do Azure | Microsoft Docs"
description: "Criar uma função que integra o sentimento de tweet toocategorize Azure lógica de aplicativos e serviços cognitivas do Azure e enviar notificações quando o sentimento é ruim."
services: functions, logic-apps, cognitive-services
keywords: "fluxo de trabalho, aplicativos de nuvem, serviços de nuvem, processos de negócios, integração de sistemas, integração de aplicativos empresariais, EAI"
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
ms.assetid: 60495cc5-1638-4bf0-8174-52786d227734
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: e176bd946af9a3684b3ad0e4b1bed1c3ee344019
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a><span data-ttu-id="5bd8c-104">Criar uma função que se integra aos Aplicativos Lógicos do Azure</span><span class="sxs-lookup"><span data-stu-id="5bd8c-104">Create a function that integrates with Azure Logic Apps</span></span>

<span data-ttu-id="5bd8c-105">As funções do Azure integra os aplicativos lógicos do Azure Olá lógica do Designer de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-105">Azure Functions integrates with Azure Logic Apps in hello Logic Apps Designer.</span></span> <span data-ttu-id="5bd8c-106">Essa integração permite que você usar Olá computando a energia de funções em orquestrações com outros serviços de terceiros e o Azure.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-106">This integration lets you use hello computing power of Functions in orchestrations with other Azure and third-party services.</span></span> 

<span data-ttu-id="5bd8c-107">Este tutorial mostra como toouse funciona com lógica de aplicativos e serviços cognitivas Azure sentimento tooanalyze de postagens no Twitter.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-107">This tutorial shows you how toouse Functions with Logic Apps and Azure Cognitive Services tooanalyze sentiment from Twitter posts.</span></span> <span data-ttu-id="5bd8c-108">Uma função HTTP disparado categoriza tweets como verde, amarelo ou vermelho com base na classificação de sentimento hello.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-108">An HTTP triggered function categorizes tweets as green, yellow, or red based on hello sentiment score.</span></span> <span data-ttu-id="5bd8c-109">Um email é enviado quando um sentimento inadequado é detectado.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-109">An email is sent when poor sentiment is detected.</span></span> 

![imagem dos dois primeiros passos do aplicativo no Designer de Aplicativos Lógicos](media/functions-twitter-email/designer1.png)

<span data-ttu-id="5bd8c-111">Neste tutorial, você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="5bd8c-111">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5bd8c-112">Criar uma conta dos Serviços Cognitivos.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-112">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="5bd8c-113">Crie uma função que categorize o sentimento do tweet.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-113">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="5bd8c-114">Crie um aplicativo lógico que se conecta tooTwitter.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-114">Create a logic app that connects tooTwitter.</span></span>
> * <span data-ttu-id="5bd8c-115">Adicione aplicativo de lógica de toohello de detecção sensibilidade.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-115">Add sentiment detection toohello logic app.</span></span> 
> * <span data-ttu-id="5bd8c-116">Conecte-se a função de toohello de aplicativo hello lógica.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-116">Connect hello logic app toohello function.</span></span>
> * <span data-ttu-id="5bd8c-117">Envie um email com base na resposta de saudação do função hello.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-117">Send an email based on hello response from hello function.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5bd8c-118">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5bd8c-118">Prerequisites</span></span>

+ <span data-ttu-id="5bd8c-119">Uma conta do [Twitter](https://twitter.com/) ativa.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-119">An active [Twitter](https://twitter.com/) account.</span></span> 
+ <span data-ttu-id="5bd8c-120">Uma conta do [Outlook.com](https://outlook.com/) (para enviar notificações).</span><span class="sxs-lookup"><span data-stu-id="5bd8c-120">An [Outlook.com](https://outlook.com/) account (for sending notifications).</span></span>
+ <span data-ttu-id="5bd8c-121">Este tópico usa como seus recursos de saudação ponto inicial criados no [criar sua primeira função da saudação portal do Azure](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="5bd8c-121">This topic uses as its starting point hello resources created in [Create your first function from hello Azure portal](functions-create-first-azure-function.md).</span></span>  
<span data-ttu-id="5bd8c-122">Se você ainda não fez isso, conclua toocreate de agora essas etapas seu aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-122">If you haven't already done so, complete these steps now toocreate your function app.</span></span>

## <a name="create-a-cognitive-services-account"></a><span data-ttu-id="5bd8c-123">Criar uma conta dos Serviços Cognitivos</span><span class="sxs-lookup"><span data-stu-id="5bd8c-123">Create a Cognitive Services account</span></span>

<span data-ttu-id="5bd8c-124">Uma conta de serviços Cognitivos é necessário toodetect Olá sentimento de tweets que está sendo monitorado.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-124">A Cognitive Services account is required toodetect hello sentiment of tweets being monitored.</span></span>

1. <span data-ttu-id="5bd8c-125">Entrar toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5bd8c-125">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="5bd8c-126">Clique em Olá **novo** botão localizado no canto superior esquerdo de saudação do hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-126">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

3. <span data-ttu-id="5bd8c-127">Clique em **Dados + Análise** > **Serviços Cognitivos**.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-127">Click **Data + Analytics** > **Cognitive  Services**.</span></span> <span data-ttu-id="5bd8c-128">Em seguida, usar Olá configurações como especificado na tabela Olá, aceite os termos de hello e verificar **toodashboard Pin**.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-128">Then, use hello settings as specified in hello table, accept hello terms, and check **Pin toodashboard**.</span></span>

    ![Criar folha de conta Cognitiva](media/functions-twitter-email/cog_svcs_account.png)

    | <span data-ttu-id="5bd8c-130">Configuração</span><span class="sxs-lookup"><span data-stu-id="5bd8c-130">Setting</span></span>      |  <span data-ttu-id="5bd8c-131">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="5bd8c-131">Suggested value</span></span>   | <span data-ttu-id="5bd8c-132">Descrição</span><span class="sxs-lookup"><span data-stu-id="5bd8c-132">Description</span></span>                                        |
    | --- | --- | --- |
    | <span data-ttu-id="5bd8c-133">**Nome**</span><span class="sxs-lookup"><span data-stu-id="5bd8c-133">**Name**</span></span> | <span data-ttu-id="5bd8c-134">MyCognitiveServicesAccnt</span><span class="sxs-lookup"><span data-stu-id="5bd8c-134">MyCognitiveServicesAccnt</span></span> | <span data-ttu-id="5bd8c-135">Escolha um nome de conta exclusivo.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-135">Choose a unique account name.</span></span> |
    | <span data-ttu-id="5bd8c-136">**Tipo de API**</span><span class="sxs-lookup"><span data-stu-id="5bd8c-136">**API type**</span></span> | <span data-ttu-id="5bd8c-137">API de Análise de Texto</span><span class="sxs-lookup"><span data-stu-id="5bd8c-137">Text Analytics API</span></span> | <span data-ttu-id="5bd8c-138">A API usada tooanalyze texto.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-138">API used tooanalyze text.</span></span>  |
    | <span data-ttu-id="5bd8c-139">**Localidade**</span><span class="sxs-lookup"><span data-stu-id="5bd8c-139">**Location**</span></span> | <span data-ttu-id="5bd8c-140">Oeste dos EUA</span><span class="sxs-lookup"><span data-stu-id="5bd8c-140">West US</span></span> | <span data-ttu-id="5bd8c-141">Atualmente, apenas o **Oeste dos EUA** está disponível para análise de texto.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-141">Currently, only **West US** is available for text analytics.</span></span> |
    | <span data-ttu-id="5bd8c-142">**Tipo de preços**</span><span class="sxs-lookup"><span data-stu-id="5bd8c-142">**Pricing tier**</span></span> | <span data-ttu-id="5bd8c-143">F0</span><span class="sxs-lookup"><span data-stu-id="5bd8c-143">F0</span></span> | <span data-ttu-id="5bd8c-144">Inicie com o nível mais baixo de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-144">Start with hello lowest tier.</span></span> <span data-ttu-id="5bd8c-145">Se você executar fora de chamadas, dimensione a camada superior tooa.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-145">If you run out of calls, scale tooa higher tier.</span></span>|
    | <span data-ttu-id="5bd8c-146">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="5bd8c-146">**Resource group**</span></span> | <span data-ttu-id="5bd8c-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5bd8c-147">myResourceGroup</span></span> | <span data-ttu-id="5bd8c-148">Use Olá mesmo grupo de recursos para todos os serviços neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-148">Use hello same resource group for all services in this tutorial.</span></span>|

4. <span data-ttu-id="5bd8c-149">Clique em **criar** toocreate sua conta.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-149">Click **Create** toocreate your account.</span></span> <span data-ttu-id="5bd8c-150">Depois de saudação conta é criada, clique em seu novo painel de toohello fixados da conta de serviços Cognitivos.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-150">After hello account is created, click your new Cognitive Services account pinned toohello dashboard.</span></span> 

5. <span data-ttu-id="5bd8c-151">Na conta de saudação, clique em **chaves**e, em seguida, copie o valor de saudação do **chave 1** e salvá-lo.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-151">In hello account, click **Keys**, and then copy hello value of **Key 1** and save it.</span></span> <span data-ttu-id="5bd8c-152">Você usa essa chave tooconnect Olá lógica aplicativo tooyour conta de serviços Cognitivos.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-152">You use this key tooconnect hello logic app tooyour Cognitive Services account.</span></span> 
 
    ![simétricas](media/functions-twitter-email/keys.png)

## <a name="create-hello-function"></a><span data-ttu-id="5bd8c-154">Criar função hello</span><span class="sxs-lookup"><span data-stu-id="5bd8c-154">Create hello function</span></span>

<span data-ttu-id="5bd8c-155">Funções fornece toooffload uma ótima maneira de tarefas de processamento em um fluxo de trabalho de aplicativos de lógica.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-155">Functions provides a great way toooffload processing tasks in a logic apps workflow.</span></span> <span data-ttu-id="5bd8c-156">Este tutorial usa um pontuações HTTP disparado função tooprocess tweet sentimento de serviços Cognitivos e retornar um valor de categoria.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-156">This tutorial uses an HTTP triggered function tooprocess tweet sentiment scores from Cognitive Services and return a category value.</span></span>  

1. <span data-ttu-id="5bd8c-157">Expanda seu aplicativo de função, clique em Olá  **+**  botão Avançar muito**funções**, clique em Olá **HTTPTrigger** modelo.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-157">Expand your function app, click hello **+** button next too**Functions**, click hello **HTTPTrigger** template.</span></span> <span data-ttu-id="5bd8c-158">Tipo `CategorizeSentiment` para a função hello **nome** e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-158">Type `CategorizeSentiment` for hello function **Name** and click **Create**.</span></span>

    ![Folha Aplicativos de Funções, Funções +](media/functions-twitter-email/add_fun.png)

2. <span data-ttu-id="5bd8c-160">Substituir o conteúdo de saudação do arquivo de run.csx de saudação com hello código a seguir e, em seguida, clique em **salvar**:</span><span class="sxs-lookup"><span data-stu-id="5bd8c-160">Replace hello contents of hello run.csx file with hello following code, then click **Save**:</span></span>

    ```c#
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // hello sentiment category defaults too'GREEN'. 
        string category = "GREEN";
    
        // Get hello sentiment score from hello request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("hello sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set hello category based on hello sentiment score.
        if (score < .3)
        {
            category = "RED";
        }
        else if (score < .6)
        {
            category = "YELLOW";
        }
        return req.CreateResponse(HttpStatusCode.OK, category);
    }
    ```
    <span data-ttu-id="5bd8c-161">Esse código de função retorna uma categoria de cor com base em Olá sentimento pontuação recebida na solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-161">This function code returns a color category based on hello sentiment score received in hello request.</span></span> 

3. <span data-ttu-id="5bd8c-162">função de saudação tootest, clique em **teste** no guia de teste de Olá Olá tooexpand extrema direita. Digite um valor de `0.2` para Olá **corpo da solicitação**e, em seguida, clique em **executar**.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-162">tootest hello function, click **Test** at hello far right tooexpand hello Test tab. Type a value of `0.2` for hello **Request body**, and then click **Run**.</span></span> <span data-ttu-id="5bd8c-163">Um valor de **vermelho** é retornado no corpo de saudação da resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-163">A value of **RED** is returned in hello body of hello response.</span></span> 

    ![Testar função hello em Olá portal do Azure](./media/functions-twitter-email/test.png)

<span data-ttu-id="5bd8c-165">Agora você tem uma função que categoriza as pontuações de sentimento.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-165">Now you have a function that categorizes sentiment scores.</span></span> <span data-ttu-id="5bd8c-166">Em seguida, você pode criar um aplicativo lógico que integra sua função às contas dos Serviços Cognitivos e do Twitter.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-166">Next, you create a logic app that integrates your function with your Twitter and Cognitive Services accounts.</span></span> 

## <a name="create-a-logic-app"></a><span data-ttu-id="5bd8c-167">Criar um aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="5bd8c-167">Create a logic app</span></span>   

1. <span data-ttu-id="5bd8c-168">Em Olá portal do Azure, clique em Olá **novo** botão localizado no canto superior esquerdo de saudação do hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-168">In hello Azure portal, click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="5bd8c-169">Clique em **Integração de Empresas** > **Aplicativo Lógico**.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-169">Click **Enterprise Integration** > **Logic App**.</span></span> <span data-ttu-id="5bd8c-170">Em seguida, usar configurações de saudação como especificado na tabela Olá, verifique **Pin toodashboard**e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-170">Then, use hello settings as specified in hello table, check **Pin toodashboard**, and click **Create**.</span></span>
 
4. <span data-ttu-id="5bd8c-171">Em seguida, digite um **nome** como `TweetSentiment`, usar configurações de saudação conforme especificado na tabela de saudação, aceite os termos de saudação e verificar **toodashboard Pin**.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-171">Then, type a **Name** like `TweetSentiment`,  use hello settings as specified in hello table, accept hello terms, and check **Pin toodashboard**.</span></span>

    ![Criar aplicativo lógico no hello portal do Azure](./media/functions-twitter-email/new_logicApp.png)

    | <span data-ttu-id="5bd8c-173">Configuração</span><span class="sxs-lookup"><span data-stu-id="5bd8c-173">Setting</span></span>      |  <span data-ttu-id="5bd8c-174">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="5bd8c-174">Suggested value</span></span>   | <span data-ttu-id="5bd8c-175">Descrição</span><span class="sxs-lookup"><span data-stu-id="5bd8c-175">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="5bd8c-176">**Nome**</span><span class="sxs-lookup"><span data-stu-id="5bd8c-176">**Name**</span></span> | <span data-ttu-id="5bd8c-177">TweetSentiment</span><span class="sxs-lookup"><span data-stu-id="5bd8c-177">TweetSentiment</span></span> | <span data-ttu-id="5bd8c-178">Escolha um nome apropriado para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-178">Choose an appropriate name for your app.</span></span> |
    | <span data-ttu-id="5bd8c-179">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="5bd8c-179">**Resource group**</span></span> | <span data-ttu-id="5bd8c-180">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5bd8c-180">myResourceGroup</span></span> | <span data-ttu-id="5bd8c-181">A API usada tooanalyze texto.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-181">API used tooanalyze text.</span></span>  |
    | <span data-ttu-id="5bd8c-182">**Localidade**</span><span class="sxs-lookup"><span data-stu-id="5bd8c-182">**Location**</span></span> | <span data-ttu-id="5bd8c-183">Leste dos EUA</span><span class="sxs-lookup"><span data-stu-id="5bd8c-183">East US</span></span> | <span data-ttu-id="5bd8c-184">Escolha um tooyou fechar do local.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-184">Choose a location close tooyou.</span></span> |
    | <span data-ttu-id="5bd8c-185">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="5bd8c-185">**Resource group**</span></span> | <span data-ttu-id="5bd8c-186">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5bd8c-186">myResourceGroup</span></span> | <span data-ttu-id="5bd8c-187">Escolha Olá mesmo grupo de recursos existente como antes.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-187">Choose hello same existing resource group as before.</span></span>|

4. <span data-ttu-id="5bd8c-188">Clique em **criar** toocreate seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-188">Click **Create** toocreate your logic app.</span></span> <span data-ttu-id="5bd8c-189">Depois que o aplicativo hello for criado, clique em seu novo painel toohello fixados de aplicativo lógica.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-189">After hello app is created, click your new logic app pinned toohello dashboard.</span></span> <span data-ttu-id="5bd8c-190">Em seguida, no hello lógica do Designer de aplicativos, role para baixo e clique em Olá **aplicativo lógica em branco** modelo.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-190">Then in hello Logic Apps Designer, scroll down and click hello **Blank Logic App** template.</span></span> 

    ![Modelo Aplicativo Lógico em Branco](media/functions-twitter-email/blank.png)

<span data-ttu-id="5bd8c-192">Agora você pode usar o hello lógica aplicativos tooadd serviços e disparadores tooyour aplicativo Designer.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-192">You can now use hello Logic Apps Designer tooadd services and triggers tooyour app.</span></span>

## <a name="connect-tootwitter"></a><span data-ttu-id="5bd8c-193">Conecte-se tooTwitter</span><span class="sxs-lookup"><span data-stu-id="5bd8c-193">Connect tooTwitter</span></span>

<span data-ttu-id="5bd8c-194">Primeiro, crie um conta do Twitter do tooyour de conexão.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-194">First, create a connection tooyour Twitter account.</span></span> <span data-ttu-id="5bd8c-195">Olá lógica aplicativo sonda tweets, que disparam Olá toorun de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-195">hello logic app polls for tweets, which trigger hello app toorun.</span></span>

1. <span data-ttu-id="5bd8c-196">No designer de saudação, clique em Olá **Twitter** de serviço e, em seguida, clique em Olá **quando um novo tweet for lançado** gatilho.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-196">In hello designer, click hello **Twitter** service, and click hello **When a new tweet is posted** trigger.</span></span> <span data-ttu-id="5bd8c-197">Entrar tooyour conta do Twitter e autorizar aplicativos lógicos toouse sua conta.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-197">Sign in tooyour Twitter account and authorize Logic Apps toouse your account.</span></span>

2. <span data-ttu-id="5bd8c-198">Use configurações de gatilho do Twitter Olá conforme especificado na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-198">Use hello Twitter trigger settings as specified in hello table.</span></span> 

    ![Configurações do conector do Twitter](media/functions-twitter-email/azure_tweet.png)

    | <span data-ttu-id="5bd8c-200">Configuração</span><span class="sxs-lookup"><span data-stu-id="5bd8c-200">Setting</span></span>      |  <span data-ttu-id="5bd8c-201">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="5bd8c-201">Suggested value</span></span>   | <span data-ttu-id="5bd8c-202">Descrição</span><span class="sxs-lookup"><span data-stu-id="5bd8c-202">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="5bd8c-203">**Texto da pesquisa**</span><span class="sxs-lookup"><span data-stu-id="5bd8c-203">**Search text**</span></span> | <span data-ttu-id="5bd8c-204">#Azure</span><span class="sxs-lookup"><span data-stu-id="5bd8c-204">#Azure</span></span> | <span data-ttu-id="5bd8c-205">Use um hashtag que é popular para toogenerate tweets de novo no intervalo de saudação escolhida.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-205">Use a hashtag that is popular enough for toogenerate new tweets in hello chosen interval.</span></span> <span data-ttu-id="5bd8c-206">Ao usar a camada gratuita hello e seu hashtag é muito popular, você pode rapidamente usar transações Olá em sua conta de serviços Cognitivos.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-206">When using hello Free tier and your hashtag is too popular, you can quickly use up hello transactions in your Cognitive Services account.</span></span> |
    | <span data-ttu-id="5bd8c-207">**Frequência**</span><span class="sxs-lookup"><span data-stu-id="5bd8c-207">**Frequency**</span></span> | <span data-ttu-id="5bd8c-208">Minuto</span><span class="sxs-lookup"><span data-stu-id="5bd8c-208">Minute</span></span> | <span data-ttu-id="5bd8c-209">unidade de frequência Olá usada para sondagem Twitter.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-209">hello frequency unit used for polling Twitter.</span></span>  |
    | <span data-ttu-id="5bd8c-210">**Intervalo**</span><span class="sxs-lookup"><span data-stu-id="5bd8c-210">**Interval**</span></span> | <span data-ttu-id="5bd8c-211">15</span><span class="sxs-lookup"><span data-stu-id="5bd8c-211">15</span></span> | <span data-ttu-id="5bd8c-212">tempo de saudação decorrido entre as solicitações do Twitter, em unidades de frequência.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-212">hello time elapsed between Twitter requests, in frequency units.</span></span> |

3.  <span data-ttu-id="5bd8c-213">Clique em **salvar** tooconnect tooyour conta do Twitter.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-213">Click **Save** tooconnect tooyour Twitter account.</span></span> 

<span data-ttu-id="5bd8c-214">Agora o seu aplicativo é tooTwitter conectado.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-214">Now your app is connected tooTwitter.</span></span> <span data-ttu-id="5bd8c-215">Em seguida, conecte-se sentimento de saudação do tootext análise toodetect de tweets coletados.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-215">Next, you connect tootext analytics toodetect hello sentiment of collected tweets.</span></span>

## <a name="add-sentiment-detection"></a><span data-ttu-id="5bd8c-216">Adicionar detecção de sentimento</span><span class="sxs-lookup"><span data-stu-id="5bd8c-216">Add sentiment detection</span></span>

1. <span data-ttu-id="5bd8c-217">Clique em **Nova Etapa** e em **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-217">Click **New Step**, and then **Add an action**.</span></span>

    ![Nova Etapa e, então, Adicionar uma ação](media/functions-twitter-email/new_step.png)

2. <span data-ttu-id="5bd8c-219">Em **escolher uma ação**, clique em **análises de texto**e, em seguida, clique em Olá **detectar sentimento** ação.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-219">In **Choose an action**, click **Text Analytics**, and then click hello **Detect sentiment** action.</span></span>

    ![Detectar Sentimento](media/functions-twitter-email/detect_sent.png)

3. <span data-ttu-id="5bd8c-221">Digite um nome de conexão como `MyCognitiveServicesConnection`, cole a chave de saudação para seus serviços Cognitivos conta que você salvou e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-221">Type a connection name such as `MyCognitiveServicesConnection`, paste hello key for your Cognitive Services account that you saved, and click **Create**.</span></span>  

4. <span data-ttu-id="5bd8c-222">Clique em **texto tooanalyze** > **Tweet texto**e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-222">Click **Text tooanalyze** > **Tweet text**, and then click **Save**.</span></span>  

    ![Detectar Sentimento](media/functions-twitter-email/ds_tta.png)

<span data-ttu-id="5bd8c-224">Detecção sensibilidade já está configurado, você pode adicionar uma função de tooyour de conexão que consome a saída de pontuação de sensibilidade hello.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-224">Now that sentiment detection is configured, you can add a connection tooyour function that consumes hello sentiment score output.</span></span>

## <a name="connect-sentiment-output-tooyour-function"></a><span data-ttu-id="5bd8c-225">Conecte-se a função de tooyour de saída de sentimento</span><span class="sxs-lookup"><span data-stu-id="5bd8c-225">Connect sentiment output tooyour function</span></span>

1. <span data-ttu-id="5bd8c-226">No hello lógica do Designer de aplicativos, clique em **nova etapa** > **adicionar uma ação**e, em seguida, clique em **funções do Azure**.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-226">In hello Logic Apps Designer, click **New step** > **Add an action**, and then click **Azure Functions**.</span></span> 

2. <span data-ttu-id="5bd8c-227">Clique em **escolher uma função do Azure**, selecione Olá **CategorizeSentiment** função que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-227">Click **Choose an Azure function**, select hello **CategorizeSentiment** function you created earlier.</span></span>  

    ![Caixa de função do Azure mostrando "Escolher uma Função do Azure"](media/functions-twitter-email/choose_fun.png)

3. <span data-ttu-id="5bd8c-229">Em **Corpo da Solicitação**, clique em **Pontuação** e em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-229">In **Request Body**, click **Score** and then **Save**.</span></span>

    ![Pontuação](media/functions-twitter-email/trigger_score.png)

<span data-ttu-id="5bd8c-231">Agora, sua função é disparada quando uma pontuação de sensibilidade é enviada do aplicativo lógico de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-231">Now, your function is triggered when a sentiment score is sent from hello logic app.</span></span> <span data-ttu-id="5bd8c-232">Uma categoria com codificação de cores é retornada toohello lógica aplicativo por função hello.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-232">A color-coded category is returned toohello logic app by hello function.</span></span> <span data-ttu-id="5bd8c-233">Em seguida, você adiciona uma notificação por email é enviada quando um valor de sensibilidade de **vermelho** é retornado da função hello.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-233">Next, you add an email notification that is sent when a sentiment value of **RED** is returned from hello function.</span></span> 

## <a name="add-email-notifications"></a><span data-ttu-id="5bd8c-234">Adicionar notificações por email</span><span class="sxs-lookup"><span data-stu-id="5bd8c-234">Add email notifications</span></span>

<span data-ttu-id="5bd8c-235">Olá última parte do fluxo de trabalho de saudação é tootrigger um email quando o sentimento Olá foi classificado como _vermelho_.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-235">hello last part of hello workflow is tootrigger an email when hello sentiment is scored as _RED_.</span></span> <span data-ttu-id="5bd8c-236">Este tópico usa um conector do Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-236">This topic uses an Outlook.com connector.</span></span> <span data-ttu-id="5bd8c-237">Você pode executar semelhante etapas toouse um conector Gmail ou Outlook do Office 365.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-237">You can perform similar steps toouse a Gmail or Office 365 Outlook connector.</span></span>   

1. <span data-ttu-id="5bd8c-238">No hello lógica do Designer de aplicativos, clique em **nova etapa** > **adicionar uma condição**.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-238">In hello Logic Apps Designer, click **New step** > **Add a condition**.</span></span> 

2. <span data-ttu-id="5bd8c-239">Clique em **Escolha um valor** e clique em **Corpo**.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-239">Click **Choose a value**, then click **Body**.</span></span> <span data-ttu-id="5bd8c-240">Selecione **é igual a**, clique em **Escolha um valor**, digite `RED`e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-240">Select **is equal to**, click **Choose a value** and type `RED`, and click **Save**.</span></span> 

    ![Adicione um aplicativo de lógica de toohello de condição.](media/functions-twitter-email/condition.png)

3. <span data-ttu-id="5bd8c-242">Em **se Sim, não faça NADA**, clique em **adicionar uma ação**, procurar `outlook.com`, clique em **enviar um email**e entre tooyour conta do Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-242">In **IF YES, DO NOTHING**, click **Add an action**, search for `outlook.com`, click **Send an email**, and sign in tooyour Outlook.com account.</span></span>
    
    ![Escolha uma ação para a condição de saudação.](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > <span data-ttu-id="5bd8c-244">Se você não tiver uma conta do Outlook.com, poderá escolher outro conector, como Gmail ou Outlook do Office 365</span><span class="sxs-lookup"><span data-stu-id="5bd8c-244">If you don't have an Outlook.com account, you can choose another connector, such as Gmail or Office 365 Outlook</span></span>

4. <span data-ttu-id="5bd8c-245">Em Olá **enviar um email** ação, usar configurações de email hello como especificado na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-245">In hello **Send an email** action, use hello email settings as specified in hello table.</span></span> 

    ![Configure o email de hello para enviar Olá uma ação de email.](media/functions-twitter-email/sendemail.png)

    | <span data-ttu-id="5bd8c-247">Configuração</span><span class="sxs-lookup"><span data-stu-id="5bd8c-247">Setting</span></span>      |  <span data-ttu-id="5bd8c-248">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="5bd8c-248">Suggested value</span></span>   | <span data-ttu-id="5bd8c-249">Descrição</span><span class="sxs-lookup"><span data-stu-id="5bd8c-249">Description</span></span>  |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="5bd8c-250">**Para**</span><span class="sxs-lookup"><span data-stu-id="5bd8c-250">**To**</span></span> | <span data-ttu-id="5bd8c-251">Digitar endereço de email</span><span class="sxs-lookup"><span data-stu-id="5bd8c-251">Type your email address</span></span> | <span data-ttu-id="5bd8c-252">endereço de email de saudação que recebe a notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-252">hello email address that receives hello notification.</span></span> |
    | <span data-ttu-id="5bd8c-253">**Assunto**</span><span class="sxs-lookup"><span data-stu-id="5bd8c-253">**Subject**</span></span> | <span data-ttu-id="5bd8c-254">Sentimento de tweet negativo detectado</span><span class="sxs-lookup"><span data-stu-id="5bd8c-254">Negative tweet sentiment detected</span></span>  | <span data-ttu-id="5bd8c-255">Olá assunto da notificação por email hello.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-255">hello subject line of hello email notification.</span></span>  |
    | <span data-ttu-id="5bd8c-256">**Corpo**</span><span class="sxs-lookup"><span data-stu-id="5bd8c-256">**Body**</span></span> | <span data-ttu-id="5bd8c-257">Texto do Tweet, local</span><span class="sxs-lookup"><span data-stu-id="5bd8c-257">Tweet text, Location</span></span> | <span data-ttu-id="5bd8c-258">Clique em Olá **Tweet texto** e **local** parâmetros.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-258">Click hello **Tweet text** and **Location** parameters.</span></span> |

5.  <span data-ttu-id="5bd8c-259">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-259">Click **Save**.</span></span>

<span data-ttu-id="5bd8c-260">Agora que o fluxo de trabalho de saudação for concluído, você pode habilitar Olá lógica aplicativo e consulte função hello no trabalho.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-260">Now that hello workflow is complete, you can enable hello logic app and see hello function at work.</span></span>

## <a name="test-hello-workflow"></a><span data-ttu-id="5bd8c-261">Fluxo de trabalho de saudação de teste</span><span class="sxs-lookup"><span data-stu-id="5bd8c-261">Test hello workflow</span></span>

1. <span data-ttu-id="5bd8c-262">No hello lógica de aplicativo Designer, clique em **executar** toostart Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-262">In hello Logic App Designer, click **Run** toostart hello app.</span></span>

2. <span data-ttu-id="5bd8c-263">Na coluna esquerda da saudação, clique em **visão geral** toosee status de saudação do aplicativo de lógica de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-263">In hello left column, click **Overview** toosee hello status of hello logic app.</span></span> 
 
    ![Status de execução do aplicativo lógico](media/functions-twitter-email/over1.png)

3. <span data-ttu-id="5bd8c-265">(Opcional) Clique em uma saudação executa toosee detalhes da execução de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-265">(Optional) Click one of hello runs toosee details of hello execution.</span></span>

4. <span data-ttu-id="5bd8c-266">Vá função tooyour, exibir logs hello e verificar que os valores de sentimento foram recebidos e processados.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-266">Go tooyour function, view hello logs, and verify that sentiment values were received and processed.</span></span>
 
    ![Exibir os logs da função](media/functions-twitter-email/sent.png)

5. <span data-ttu-id="5bd8c-268">Quando um sentimento potencialmente negativo é detectado, você recebe um email.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-268">When a potentially negative sentiment is detected, you receive an email.</span></span> <span data-ttu-id="5bd8c-269">Se você ainda não recebeu um email, você pode alterar a saudação função código tooreturn vermelho sempre:</span><span class="sxs-lookup"><span data-stu-id="5bd8c-269">If you haven't received an email, you can change hello function code tooreturn RED every time:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    <span data-ttu-id="5bd8c-270">Depois que você verificou as notificações por email, altere código de retorno toohello original:</span><span class="sxs-lookup"><span data-stu-id="5bd8c-270">After you have verified email notifications, change back toohello original code:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > <span data-ttu-id="5bd8c-271">Depois de concluir este tutorial, você deve desabilitar o aplicativo lógico de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-271">After you have completed this tutorial, you should disable hello logic app.</span></span> <span data-ttu-id="5bd8c-272">Ao desabilitar o aplicativo hello, você evitar que está sendo carregada para execuções e usar transações Olá em sua conta de serviços Cognitivos.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-272">By disabling hello app, you avoid being charged for executions and using up hello transactions in your Cognitive Services account.</span></span>

<span data-ttu-id="5bd8c-273">Agora você viu como é fácil toointegrate funções em um fluxo de trabalho de aplicativos lógicos.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-273">Now you have seen how easy it is toointegrate Functions into a Logic Apps workflow.</span></span>

## <a name="disable-hello-logic-app"></a><span data-ttu-id="5bd8c-274">Desabilitar o aplicativo de lógica de saudação</span><span class="sxs-lookup"><span data-stu-id="5bd8c-274">Disable hello logic app</span></span>

<span data-ttu-id="5bd8c-275">aplicativo de lógica de saudação toodisable, clique em **visão geral** e, em seguida, clique em **desabilitar** na parte superior de saudação da tela hello.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-275">toodisable hello logic app, click **Overview** and then click **Disable** at hello top of hello screen.</span></span> <span data-ttu-id="5bd8c-276">Isso interrompe o aplicativo lógico de saudação em execução e incorrer em encargos sem excluir o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-276">This stops hello logic app from running and incurring charges without deleting hello app.</span></span> 

![Logs da função](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a><span data-ttu-id="5bd8c-278">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5bd8c-278">Next steps</span></span>

<span data-ttu-id="5bd8c-279">Neste tutorial, você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="5bd8c-279">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5bd8c-280">Criar uma conta dos Serviços Cognitivos.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-280">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="5bd8c-281">Crie uma função que categorize o sentimento do tweet.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-281">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="5bd8c-282">Crie um aplicativo lógico que se conecta tooTwitter.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-282">Create a logic app that connects tooTwitter.</span></span>
> * <span data-ttu-id="5bd8c-283">Adicione aplicativo de lógica de toohello de detecção sensibilidade.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-283">Add sentiment detection toohello logic app.</span></span> 
> * <span data-ttu-id="5bd8c-284">Conecte-se a função de toohello de aplicativo hello lógica.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-284">Connect hello logic app toohello function.</span></span>
> * <span data-ttu-id="5bd8c-285">Envie um email com base na resposta de saudação do função hello.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-285">Send an email based on hello response from hello function.</span></span>

<span data-ttu-id="5bd8c-286">Avançar toolearn tutorial do próximo toohello como toocreate uma API sem servidor de sua função.</span><span class="sxs-lookup"><span data-stu-id="5bd8c-286">Advance toohello next tutorial toolearn how toocreate a serverless API for your function.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="5bd8c-287">Criar uma API sem servidor usando o Azure Functions</span><span class="sxs-lookup"><span data-stu-id="5bd8c-287">Create a serverless API using Azure Functions</span></span>](functions-create-serverless-api.md)

<span data-ttu-id="5bd8c-288">toolearn mais sobre aplicativos lógicos, consulte [aplicativos do Azure lógica](../logic-apps/logic-apps-what-are-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="5bd8c-288">toolearn more about Logic Apps, see [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).</span></span>

