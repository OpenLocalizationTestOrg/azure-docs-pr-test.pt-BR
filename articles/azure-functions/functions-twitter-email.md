---
title: "Criar uma função que se integra aos Aplicativos Lógicos do Azure | Microsoft Docs"
description: "Crie uma função que se integra com os Aplicativos Lógicos do Azure e os Serviços Cognitivos do Azure para categorizar o sentimento de tweet e enviar notificações quando o sentimento for fraco."
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
ms.openlocfilehash: 4a5dc668e21c5328b308c8f5852aaa922232374d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a><span data-ttu-id="08f8a-104">Criar uma função que se integra aos Aplicativos Lógicos do Azure</span><span class="sxs-lookup"><span data-stu-id="08f8a-104">Create a function that integrates with Azure Logic Apps</span></span>

<span data-ttu-id="08f8a-105">O Azure Functions integra-se aos Aplicativos Lógicos do Azure no Designer de Aplicativos Lógicos.</span><span class="sxs-lookup"><span data-stu-id="08f8a-105">Azure Functions integrates with Azure Logic Apps in the Logic Apps Designer.</span></span> <span data-ttu-id="08f8a-106">Essa integração permite usar o poder de computação do Functions em orquestrações com outros serviços de terceiros e do Azure.</span><span class="sxs-lookup"><span data-stu-id="08f8a-106">This integration lets you use the computing power of Functions in orchestrations with other Azure and third-party services.</span></span> 

<span data-ttu-id="08f8a-107">Este tutorial mostra como usar o Functions com Aplicativos Lógicos e Serviços Cognitivos do Azure para analisar o sentimento de postagens do Twitter.</span><span class="sxs-lookup"><span data-stu-id="08f8a-107">This tutorial shows you how to use Functions with Logic Apps and Azure Cognitive Services to analyze sentiment from Twitter posts.</span></span> <span data-ttu-id="08f8a-108">Uma função HTTP disparada categoriza tweets com cores verde, amarelo ou vermelho com base na pontuação de sentimento.</span><span class="sxs-lookup"><span data-stu-id="08f8a-108">An HTTP triggered function categorizes tweets as green, yellow, or red based on the sentiment score.</span></span> <span data-ttu-id="08f8a-109">Um email é enviado quando um sentimento inadequado é detectado.</span><span class="sxs-lookup"><span data-stu-id="08f8a-109">An email is sent when poor sentiment is detected.</span></span> 

![imagem dos dois primeiros passos do aplicativo no Designer de Aplicativos Lógicos](media/functions-twitter-email/designer1.png)

<span data-ttu-id="08f8a-111">Neste tutorial, você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="08f8a-111">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="08f8a-112">Criar uma conta dos Serviços Cognitivos.</span><span class="sxs-lookup"><span data-stu-id="08f8a-112">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="08f8a-113">Crie uma função que categorize o sentimento do tweet.</span><span class="sxs-lookup"><span data-stu-id="08f8a-113">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="08f8a-114">Crie um aplicativo lógico que se conecte ao Twitter.</span><span class="sxs-lookup"><span data-stu-id="08f8a-114">Create a logic app that connects to Twitter.</span></span>
> * <span data-ttu-id="08f8a-115">Adicione a detecção de sentimento ao aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="08f8a-115">Add sentiment detection to the logic app.</span></span> 
> * <span data-ttu-id="08f8a-116">Conecte o aplicativo lógico à função.</span><span class="sxs-lookup"><span data-stu-id="08f8a-116">Connect the logic app to the function.</span></span>
> * <span data-ttu-id="08f8a-117">Envie um email com base na resposta da função.</span><span class="sxs-lookup"><span data-stu-id="08f8a-117">Send an email based on the response from the function.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08f8a-118">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="08f8a-118">Prerequisites</span></span>

+ <span data-ttu-id="08f8a-119">Uma conta do [Twitter](https://twitter.com/) ativa.</span><span class="sxs-lookup"><span data-stu-id="08f8a-119">An active [Twitter](https://twitter.com/) account.</span></span> 
+ <span data-ttu-id="08f8a-120">Uma conta do [Outlook.com](https://outlook.com/) (para enviar notificações).</span><span class="sxs-lookup"><span data-stu-id="08f8a-120">An [Outlook.com](https://outlook.com/) account (for sending notifications).</span></span>
+ <span data-ttu-id="08f8a-121">Este tópico usa como ponto de partida os recursos criados em [Criar sua primeira função no portal do Azure](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="08f8a-121">This topic uses as its starting point the resources created in [Create your first function from the Azure portal](functions-create-first-azure-function.md).</span></span>  
<span data-ttu-id="08f8a-122">Se você ainda não fez isso, conclua estas etapas agora para criar seu aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="08f8a-122">If you haven't already done so, complete these steps now to create your function app.</span></span>

## <a name="create-a-cognitive-services-account"></a><span data-ttu-id="08f8a-123">Criar uma conta dos Serviços Cognitivos</span><span class="sxs-lookup"><span data-stu-id="08f8a-123">Create a Cognitive Services account</span></span>

<span data-ttu-id="08f8a-124">Uma conta dos Serviços Cognitivos é necessária para detectar o sentimento dos tweets sendo monitorados.</span><span class="sxs-lookup"><span data-stu-id="08f8a-124">A Cognitive Services account is required to detect the sentiment of tweets being monitored.</span></span>

1. <span data-ttu-id="08f8a-125">Entre no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="08f8a-125">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="08f8a-126">Clique no botão **Novo** no canto superior esquerdo do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="08f8a-126">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

3. <span data-ttu-id="08f8a-127">Clique em **Dados + Análise** > **Serviços Cognitivos**.</span><span class="sxs-lookup"><span data-stu-id="08f8a-127">Click **Data + Analytics** > **Cognitive  Services**.</span></span> <span data-ttu-id="08f8a-128">Em seguida, use as configurações conforme especificadas na tabela, aceite os termos e marque **Fixar no painel**.</span><span class="sxs-lookup"><span data-stu-id="08f8a-128">Then, use the settings as specified in the table, accept the terms, and check **Pin to dashboard**.</span></span>

    ![Criar folha de conta Cognitiva](media/functions-twitter-email/cog_svcs_account.png)

    | <span data-ttu-id="08f8a-130">Configuração</span><span class="sxs-lookup"><span data-stu-id="08f8a-130">Setting</span></span>      |  <span data-ttu-id="08f8a-131">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="08f8a-131">Suggested value</span></span>   | <span data-ttu-id="08f8a-132">Descrição</span><span class="sxs-lookup"><span data-stu-id="08f8a-132">Description</span></span>                                        |
    | --- | --- | --- |
    | <span data-ttu-id="08f8a-133">**Nome**</span><span class="sxs-lookup"><span data-stu-id="08f8a-133">**Name**</span></span> | <span data-ttu-id="08f8a-134">MyCognitiveServicesAccnt</span><span class="sxs-lookup"><span data-stu-id="08f8a-134">MyCognitiveServicesAccnt</span></span> | <span data-ttu-id="08f8a-135">Escolha um nome de conta exclusivo.</span><span class="sxs-lookup"><span data-stu-id="08f8a-135">Choose a unique account name.</span></span> |
    | <span data-ttu-id="08f8a-136">**Tipo de API**</span><span class="sxs-lookup"><span data-stu-id="08f8a-136">**API type**</span></span> | <span data-ttu-id="08f8a-137">API de Análise de Texto</span><span class="sxs-lookup"><span data-stu-id="08f8a-137">Text Analytics API</span></span> | <span data-ttu-id="08f8a-138">API usada para analisar texto.</span><span class="sxs-lookup"><span data-stu-id="08f8a-138">API used to analyze text.</span></span>  |
    | <span data-ttu-id="08f8a-139">**Localidade**</span><span class="sxs-lookup"><span data-stu-id="08f8a-139">**Location**</span></span> | <span data-ttu-id="08f8a-140">Oeste dos EUA</span><span class="sxs-lookup"><span data-stu-id="08f8a-140">West US</span></span> | <span data-ttu-id="08f8a-141">Atualmente, apenas o **Oeste dos EUA** está disponível para análise de texto.</span><span class="sxs-lookup"><span data-stu-id="08f8a-141">Currently, only **West US** is available for text analytics.</span></span> |
    | <span data-ttu-id="08f8a-142">**Tipo de preços**</span><span class="sxs-lookup"><span data-stu-id="08f8a-142">**Pricing tier**</span></span> | <span data-ttu-id="08f8a-143">F0</span><span class="sxs-lookup"><span data-stu-id="08f8a-143">F0</span></span> | <span data-ttu-id="08f8a-144">Comece com o nível mais baixo.</span><span class="sxs-lookup"><span data-stu-id="08f8a-144">Start with the lowest tier.</span></span> <span data-ttu-id="08f8a-145">Caso suas chamadas se esgotem, dimensione para uma camada mais elevada.</span><span class="sxs-lookup"><span data-stu-id="08f8a-145">If you run out of calls, scale to a higher tier.</span></span>|
    | <span data-ttu-id="08f8a-146">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="08f8a-146">**Resource group**</span></span> | <span data-ttu-id="08f8a-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="08f8a-147">myResourceGroup</span></span> | <span data-ttu-id="08f8a-148">Use o mesmo grupo de recursos para todos os serviços neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="08f8a-148">Use the same resource group for all services in this tutorial.</span></span>|

4. <span data-ttu-id="08f8a-149">Clique em **Criar** para criar a conta.</span><span class="sxs-lookup"><span data-stu-id="08f8a-149">Click **Create** to create your account.</span></span> <span data-ttu-id="08f8a-150">Depois que a conta for criada, clique na nova conta dos Serviços Cognitivos fixada no painel.</span><span class="sxs-lookup"><span data-stu-id="08f8a-150">After the account is created, click your new Cognitive Services account pinned to the dashboard.</span></span> 

5. <span data-ttu-id="08f8a-151">Na conta, clique em **Chaves**, copie o valor da **Chave 1** e salve-o.</span><span class="sxs-lookup"><span data-stu-id="08f8a-151">In the account, click **Keys**, and then copy the value of **Key 1** and save it.</span></span> <span data-ttu-id="08f8a-152">Você pode usar essa chave para conectar o aplicativo lógico à conta dos Serviços Cognitivos.</span><span class="sxs-lookup"><span data-stu-id="08f8a-152">You use this key to connect the logic app to your Cognitive Services account.</span></span> 
 
    ![simétricas](media/functions-twitter-email/keys.png)

## <a name="create-the-function"></a><span data-ttu-id="08f8a-154">Criar a função</span><span class="sxs-lookup"><span data-stu-id="08f8a-154">Create the function</span></span>

<span data-ttu-id="08f8a-155">O Functions fornece uma ótima maneira de descarregar tarefas de processamento em um fluxo de trabalho de aplicativos lógicos.</span><span class="sxs-lookup"><span data-stu-id="08f8a-155">Functions provides a great way to offload processing tasks in a logic apps workflow.</span></span> <span data-ttu-id="08f8a-156">Este tutorial usa uma função HTTP disparada para processar pontuações de sentimento de tweet dos Serviços Cognitivos e retornar um valor de categoria.</span><span class="sxs-lookup"><span data-stu-id="08f8a-156">This tutorial uses an HTTP triggered function to process tweet sentiment scores from Cognitive Services and return a category value.</span></span>  

1. <span data-ttu-id="08f8a-157">Expanda seu aplicativo de funções, clique no botão **+** ao lado de **Functions** e clique no modelo **HTTPTrigger**.</span><span class="sxs-lookup"><span data-stu-id="08f8a-157">Expand your function app, click the **+** button next to **Functions**, click the **HTTPTrigger** template.</span></span> <span data-ttu-id="08f8a-158">Digite `CategorizeSentiment` para a função **Nome** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="08f8a-158">Type `CategorizeSentiment` for the function **Name** and click **Create**.</span></span>

    ![Folha Aplicativos de Funções, Funções +](media/functions-twitter-email/add_fun.png)

2. <span data-ttu-id="08f8a-160">Substitua o conteúdo do arquivo run.csx pelo código abaixo e clique em **Salvar**:</span><span class="sxs-lookup"><span data-stu-id="08f8a-160">Replace the contents of the run.csx file with the following code, then click **Save**:</span></span>

    ```c#
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // The sentiment category defaults to 'GREEN'. 
        string category = "GREEN";
    
        // Get the sentiment score from the request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("The sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set the category based on the sentiment score.
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
    <span data-ttu-id="08f8a-161">Esse código de função retorna uma categoria de cor com base na pontuação de sentimento recebida na solicitação.</span><span class="sxs-lookup"><span data-stu-id="08f8a-161">This function code returns a color category based on the sentiment score received in the request.</span></span> 

3. <span data-ttu-id="08f8a-162">Para testar a função, clique em **Testar** na extremidade direita para expandir a guia Teste. Digite um valor de `0.2` para o **corpo da solicitação**e clique em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="08f8a-162">To test the function, click **Test** at the far right to expand the Test tab. Type a value of `0.2` for the **Request body**, and then click **Run**.</span></span> <span data-ttu-id="08f8a-163">Um valor **VERMELHO** é retornado no corpo da resposta.</span><span class="sxs-lookup"><span data-stu-id="08f8a-163">A value of **RED** is returned in the body of the response.</span></span> 

    ![Testar a função no portal do Azure](./media/functions-twitter-email/test.png)

<span data-ttu-id="08f8a-165">Agora você tem uma função que categoriza as pontuações de sentimento.</span><span class="sxs-lookup"><span data-stu-id="08f8a-165">Now you have a function that categorizes sentiment scores.</span></span> <span data-ttu-id="08f8a-166">Em seguida, você pode criar um aplicativo lógico que integra sua função às contas dos Serviços Cognitivos e do Twitter.</span><span class="sxs-lookup"><span data-stu-id="08f8a-166">Next, you create a logic app that integrates your function with your Twitter and Cognitive Services accounts.</span></span> 

## <a name="create-a-logic-app"></a><span data-ttu-id="08f8a-167">Criar um aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="08f8a-167">Create a logic app</span></span>   

1. <span data-ttu-id="08f8a-168">Clique no botão **Novo** no canto superior esquerdo do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="08f8a-168">In the Azure portal, click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="08f8a-169">Clique em **Integração de Empresas** > **Aplicativo Lógico**.</span><span class="sxs-lookup"><span data-stu-id="08f8a-169">Click **Enterprise Integration** > **Logic App**.</span></span> <span data-ttu-id="08f8a-170">Em seguida, use as configurações conforme especificadas na tabela, marque **Fixar no painel** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="08f8a-170">Then, use the settings as specified in the table, check **Pin to dashboard**, and click **Create**.</span></span>
 
4. <span data-ttu-id="08f8a-171">Em seguida, digite um **Nome** como `TweetSentiment`, use as configurações conforme especificadas na tabela, aceite os termos e marque **Fixar no painel**.</span><span class="sxs-lookup"><span data-stu-id="08f8a-171">Then, type a **Name** like `TweetSentiment`,  use the settings as specified in the table, accept the terms, and check **Pin to dashboard**.</span></span>

    ![Criar o aplicativo lógico no portal do Azure](./media/functions-twitter-email/new_logicApp.png)

    | <span data-ttu-id="08f8a-173">Configuração</span><span class="sxs-lookup"><span data-stu-id="08f8a-173">Setting</span></span>      |  <span data-ttu-id="08f8a-174">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="08f8a-174">Suggested value</span></span>   | <span data-ttu-id="08f8a-175">Descrição</span><span class="sxs-lookup"><span data-stu-id="08f8a-175">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="08f8a-176">**Nome**</span><span class="sxs-lookup"><span data-stu-id="08f8a-176">**Name**</span></span> | <span data-ttu-id="08f8a-177">TweetSentiment</span><span class="sxs-lookup"><span data-stu-id="08f8a-177">TweetSentiment</span></span> | <span data-ttu-id="08f8a-178">Escolha um nome apropriado para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="08f8a-178">Choose an appropriate name for your app.</span></span> |
    | <span data-ttu-id="08f8a-179">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="08f8a-179">**Resource group**</span></span> | <span data-ttu-id="08f8a-180">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="08f8a-180">myResourceGroup</span></span> | <span data-ttu-id="08f8a-181">API usada para analisar texto.</span><span class="sxs-lookup"><span data-stu-id="08f8a-181">API used to analyze text.</span></span>  |
    | <span data-ttu-id="08f8a-182">**Localidade**</span><span class="sxs-lookup"><span data-stu-id="08f8a-182">**Location**</span></span> | <span data-ttu-id="08f8a-183">Leste dos EUA</span><span class="sxs-lookup"><span data-stu-id="08f8a-183">East US</span></span> | <span data-ttu-id="08f8a-184">Escolha um local perto de você.</span><span class="sxs-lookup"><span data-stu-id="08f8a-184">Choose a location close to you.</span></span> |
    | <span data-ttu-id="08f8a-185">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="08f8a-185">**Resource group**</span></span> | <span data-ttu-id="08f8a-186">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="08f8a-186">myResourceGroup</span></span> | <span data-ttu-id="08f8a-187">Escolha o mesmo grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="08f8a-187">Choose the same existing resource group as before.</span></span>|

4. <span data-ttu-id="08f8a-188">Clique em **Criar** para criar seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="08f8a-188">Click **Create** to create your logic app.</span></span> <span data-ttu-id="08f8a-189">Depois que o aplicativo for criado, clique em seu novo aplicativo lógico fixado no painel.</span><span class="sxs-lookup"><span data-stu-id="08f8a-189">After the app is created, click your new logic app pinned to the dashboard.</span></span> <span data-ttu-id="08f8a-190">Em seguida, no Designer de Aplicativos Lógicos, role para baixo e clique no modelo **Aplicativo Lógico em Branco**.</span><span class="sxs-lookup"><span data-stu-id="08f8a-190">Then in the Logic Apps Designer, scroll down and click the **Blank Logic App** template.</span></span> 

    ![Modelo Aplicativo Lógico em Branco](media/functions-twitter-email/blank.png)

<span data-ttu-id="08f8a-192">Agora você pode usar o Designer de Aplicativos Lógicos para adicionar serviços e gatilhos ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="08f8a-192">You can now use the Logic Apps Designer to add services and triggers to your app.</span></span>

## <a name="connect-to-twitter"></a><span data-ttu-id="08f8a-193">Conectar-se ao Twitter</span><span class="sxs-lookup"><span data-stu-id="08f8a-193">Connect to Twitter</span></span>

<span data-ttu-id="08f8a-194">Primeiro, crie uma conexão para sua conta do Twitter.</span><span class="sxs-lookup"><span data-stu-id="08f8a-194">First, create a connection to your Twitter account.</span></span> <span data-ttu-id="08f8a-195">O aplicativo lógico sonda tweets, o que dispara a execução do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="08f8a-195">The logic app polls for tweets, which trigger the app to run.</span></span>

1. <span data-ttu-id="08f8a-196">No designer, clique no serviço **Twitter** e clique no gatilho **Quando um novo tweet é publicado**.</span><span class="sxs-lookup"><span data-stu-id="08f8a-196">In the designer, click the **Twitter** service, and click the **When a new tweet is posted** trigger.</span></span> <span data-ttu-id="08f8a-197">Entre na sua conta do Twitter e autorize os Aplicativos Lógicos a usar sua conta.</span><span class="sxs-lookup"><span data-stu-id="08f8a-197">Sign in to your Twitter account and authorize Logic Apps to use your account.</span></span>

2. <span data-ttu-id="08f8a-198">Use as configurações de gatilho do Twitter conforme especificado na tabela.</span><span class="sxs-lookup"><span data-stu-id="08f8a-198">Use the Twitter trigger settings as specified in the table.</span></span> 

    ![Configurações do conector do Twitter](media/functions-twitter-email/azure_tweet.png)

    | <span data-ttu-id="08f8a-200">Configuração</span><span class="sxs-lookup"><span data-stu-id="08f8a-200">Setting</span></span>      |  <span data-ttu-id="08f8a-201">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="08f8a-201">Suggested value</span></span>   | <span data-ttu-id="08f8a-202">Descrição</span><span class="sxs-lookup"><span data-stu-id="08f8a-202">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="08f8a-203">**Texto da pesquisa**</span><span class="sxs-lookup"><span data-stu-id="08f8a-203">**Search text**</span></span> | <span data-ttu-id="08f8a-204">#Azure</span><span class="sxs-lookup"><span data-stu-id="08f8a-204">#Azure</span></span> | <span data-ttu-id="08f8a-205">Use uma hashtag que seja popular o suficiente para gerar novos tweets no intervalo escolhido.</span><span class="sxs-lookup"><span data-stu-id="08f8a-205">Use a hashtag that is popular enough for to generate new tweets in the chosen interval.</span></span> <span data-ttu-id="08f8a-206">Quando você usa a camada gratuita e a hashtag é muito popular, é possível consumir as transações rapidamente na conta dos Serviços Cognitivos.</span><span class="sxs-lookup"><span data-stu-id="08f8a-206">When using the Free tier and your hashtag is too popular, you can quickly use up the transactions in your Cognitive Services account.</span></span> |
    | <span data-ttu-id="08f8a-207">**Frequência**</span><span class="sxs-lookup"><span data-stu-id="08f8a-207">**Frequency**</span></span> | <span data-ttu-id="08f8a-208">Minuto</span><span class="sxs-lookup"><span data-stu-id="08f8a-208">Minute</span></span> | <span data-ttu-id="08f8a-209">A unidade de frequência usada para sondar o Twitter.</span><span class="sxs-lookup"><span data-stu-id="08f8a-209">The frequency unit used for polling Twitter.</span></span>  |
    | <span data-ttu-id="08f8a-210">**Intervalo**</span><span class="sxs-lookup"><span data-stu-id="08f8a-210">**Interval**</span></span> | <span data-ttu-id="08f8a-211">15</span><span class="sxs-lookup"><span data-stu-id="08f8a-211">15</span></span> | <span data-ttu-id="08f8a-212">O tempo decorrido entre as solicitações do Twitter, em unidades de frequência.</span><span class="sxs-lookup"><span data-stu-id="08f8a-212">The time elapsed between Twitter requests, in frequency units.</span></span> |

3.  <span data-ttu-id="08f8a-213">Clique em **Salvar** para se conectar à conta do Twitter.</span><span class="sxs-lookup"><span data-stu-id="08f8a-213">Click **Save** to connect to your Twitter account.</span></span> 

<span data-ttu-id="08f8a-214">Agora, seu aplicativo está conectado ao Twitter.</span><span class="sxs-lookup"><span data-stu-id="08f8a-214">Now your app is connected to Twitter.</span></span> <span data-ttu-id="08f8a-215">Em seguida, conecte-se à análise de texto para detectar o sentimento dos tweets coletados.</span><span class="sxs-lookup"><span data-stu-id="08f8a-215">Next, you connect to text analytics to detect the sentiment of collected tweets.</span></span>

## <a name="add-sentiment-detection"></a><span data-ttu-id="08f8a-216">Adicionar detecção de sentimento</span><span class="sxs-lookup"><span data-stu-id="08f8a-216">Add sentiment detection</span></span>

1. <span data-ttu-id="08f8a-217">Clique em **Nova Etapa** e em **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="08f8a-217">Click **New Step**, and then **Add an action**.</span></span>

    ![Nova Etapa e, então, Adicionar uma ação](media/functions-twitter-email/new_step.png)

2. <span data-ttu-id="08f8a-219">Em **Escolher uma ação**, clique em **Análise de Texto**e clique na ação **Detectar sentimento**.</span><span class="sxs-lookup"><span data-stu-id="08f8a-219">In **Choose an action**, click **Text Analytics**, and then click the **Detect sentiment** action.</span></span>

    ![Detectar Sentimento](media/functions-twitter-email/detect_sent.png)

3. <span data-ttu-id="08f8a-221">Digite um nome de conexão como `MyCognitiveServicesConnection`, cole a chave da conta dos Serviços Cognitivos que você salvou e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="08f8a-221">Type a connection name such as `MyCognitiveServicesConnection`, paste the key for your Cognitive Services account that you saved, and click **Create**.</span></span>  

4. <span data-ttu-id="08f8a-222">Clique em **Texto para Analisar** > **Texto do tweet**e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="08f8a-222">Click **Text to analyze** > **Tweet text**, and then click **Save**.</span></span>  

    ![Detectar Sentimento](media/functions-twitter-email/ds_tta.png)

<span data-ttu-id="08f8a-224">Agora que a detecção de sentimento está configurada, você pode adicionar uma conexão à função que consome a saída da pontuação de sentimento.</span><span class="sxs-lookup"><span data-stu-id="08f8a-224">Now that sentiment detection is configured, you can add a connection to your function that consumes the sentiment score output.</span></span>

## <a name="connect-sentiment-output-to-your-function"></a><span data-ttu-id="08f8a-225">Conecte a saída de sentimento à função</span><span class="sxs-lookup"><span data-stu-id="08f8a-225">Connect sentiment output to your function</span></span>

1. <span data-ttu-id="08f8a-226">No Designer de Aplicativos Lógicos, clique em **Nova etapa** > **Adicionar uma ação**e clique em **Azure Functions**.</span><span class="sxs-lookup"><span data-stu-id="08f8a-226">In the Logic Apps Designer, click **New step** > **Add an action**, and then click **Azure Functions**.</span></span> 

2. <span data-ttu-id="08f8a-227">Clique em **Escolher uma função do Azure** e selecione a função **CategorizeSentiment** que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="08f8a-227">Click **Choose an Azure function**, select the **CategorizeSentiment** function you created earlier.</span></span>  

    ![Caixa de função do Azure mostrando "Escolher uma Função do Azure"](media/functions-twitter-email/choose_fun.png)

3. <span data-ttu-id="08f8a-229">Em **Corpo da Solicitação**, clique em **Pontuação** e em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="08f8a-229">In **Request Body**, click **Score** and then **Save**.</span></span>

    ![Pontuação](media/functions-twitter-email/trigger_score.png)

<span data-ttu-id="08f8a-231">Agora, sua função é disparada quando uma pontuação de sentimento é enviada do aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="08f8a-231">Now, your function is triggered when a sentiment score is sent from the logic app.</span></span> <span data-ttu-id="08f8a-232">Uma categoria com codificação de cores é retornada para o aplicativo lógico pela função.</span><span class="sxs-lookup"><span data-stu-id="08f8a-232">A color-coded category is returned to the logic app by the function.</span></span> <span data-ttu-id="08f8a-233">Em seguida, adicione uma notificação por email que é enviada quando um valor de sentimento **vermelho** é retornado pela função.</span><span class="sxs-lookup"><span data-stu-id="08f8a-233">Next, you add an email notification that is sent when a sentiment value of **RED** is returned from the function.</span></span> 

## <a name="add-email-notifications"></a><span data-ttu-id="08f8a-234">Adicionar notificações por email</span><span class="sxs-lookup"><span data-stu-id="08f8a-234">Add email notifications</span></span>

<span data-ttu-id="08f8a-235">A última parte do fluxo de trabalho é disparar um email quando o sentimento foi classificado como _VERMELHO_.</span><span class="sxs-lookup"><span data-stu-id="08f8a-235">The last part of the workflow is to trigger an email when the sentiment is scored as _RED_.</span></span> <span data-ttu-id="08f8a-236">Este tópico usa um conector do Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="08f8a-236">This topic uses an Outlook.com connector.</span></span> <span data-ttu-id="08f8a-237">Você pode executar etapas semelhantes para usar um conector Gmail ou Outlook do Office 365.</span><span class="sxs-lookup"><span data-stu-id="08f8a-237">You can perform similar steps to use a Gmail or Office 365 Outlook connector.</span></span>   

1. <span data-ttu-id="08f8a-238">No Designer de Aplicativos Lógicos, clique em **Nova etapa** > **Adicionar uma condição**.</span><span class="sxs-lookup"><span data-stu-id="08f8a-238">In the Logic Apps Designer, click **New step** > **Add a condition**.</span></span> 

2. <span data-ttu-id="08f8a-239">Clique em **Escolha um valor** e clique em **Corpo**.</span><span class="sxs-lookup"><span data-stu-id="08f8a-239">Click **Choose a value**, then click **Body**.</span></span> <span data-ttu-id="08f8a-240">Selecione **é igual a**, clique em **Escolha um valor**, digite `RED`e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="08f8a-240">Select **is equal to**, click **Choose a value** and type `RED`, and click **Save**.</span></span> 

    ![Adicionar uma condição ao aplicativo lógico.](media/functions-twitter-email/condition.png)

3. <span data-ttu-id="08f8a-242">Em **SE SIM, NÃO FAÇA NADA**, clique em **Adicionar uma ação**, procure `outlook.com`, clique em **Enviar um email**e entre sua conta do Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="08f8a-242">In **IF YES, DO NOTHING**, click **Add an action**, search for `outlook.com`, click **Send an email**, and sign in to your Outlook.com account.</span></span>
    
    ![Escolha uma ação para a condição.](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > <span data-ttu-id="08f8a-244">Se você não tiver uma conta do Outlook.com, poderá escolher outro conector, como Gmail ou Outlook do Office 365</span><span class="sxs-lookup"><span data-stu-id="08f8a-244">If you don't have an Outlook.com account, you can choose another connector, such as Gmail or Office 365 Outlook</span></span>

4. <span data-ttu-id="08f8a-245">Na ação **Enviar um email**, use as configurações de email conforme especificadas na tabela.</span><span class="sxs-lookup"><span data-stu-id="08f8a-245">In the **Send an email** action, use the email settings as specified in the table.</span></span> 

    ![Configure o email para enviar uma ação de email.](media/functions-twitter-email/sendemail.png)

    | <span data-ttu-id="08f8a-247">Configuração</span><span class="sxs-lookup"><span data-stu-id="08f8a-247">Setting</span></span>      |  <span data-ttu-id="08f8a-248">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="08f8a-248">Suggested value</span></span>   | <span data-ttu-id="08f8a-249">Descrição</span><span class="sxs-lookup"><span data-stu-id="08f8a-249">Description</span></span>  |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="08f8a-250">**Para**</span><span class="sxs-lookup"><span data-stu-id="08f8a-250">**To**</span></span> | <span data-ttu-id="08f8a-251">Digitar endereço de email</span><span class="sxs-lookup"><span data-stu-id="08f8a-251">Type your email address</span></span> | <span data-ttu-id="08f8a-252">O endereço de email que recebe a notificação.</span><span class="sxs-lookup"><span data-stu-id="08f8a-252">The email address that receives the notification.</span></span> |
    | <span data-ttu-id="08f8a-253">**Assunto**</span><span class="sxs-lookup"><span data-stu-id="08f8a-253">**Subject**</span></span> | <span data-ttu-id="08f8a-254">Sentimento de tweet negativo detectado</span><span class="sxs-lookup"><span data-stu-id="08f8a-254">Negative tweet sentiment detected</span></span>  | <span data-ttu-id="08f8a-255">A linha de assunto do email de notificação.</span><span class="sxs-lookup"><span data-stu-id="08f8a-255">The subject line of the email notification.</span></span>  |
    | <span data-ttu-id="08f8a-256">**Corpo**</span><span class="sxs-lookup"><span data-stu-id="08f8a-256">**Body**</span></span> | <span data-ttu-id="08f8a-257">Texto do Tweet, local</span><span class="sxs-lookup"><span data-stu-id="08f8a-257">Tweet text, Location</span></span> | <span data-ttu-id="08f8a-258">Clique nos parâmetros **Texto do tweet** e **Local**.</span><span class="sxs-lookup"><span data-stu-id="08f8a-258">Click the **Tweet text** and **Location** parameters.</span></span> |

5.  <span data-ttu-id="08f8a-259">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="08f8a-259">Click **Save**.</span></span>

<span data-ttu-id="08f8a-260">Agora que o fluxo de trabalho foi concluído, você poderá habilitar o aplicativo lógico e consultar a função em operação.</span><span class="sxs-lookup"><span data-stu-id="08f8a-260">Now that the workflow is complete, you can enable the logic app and see the function at work.</span></span>

## <a name="test-the-workflow"></a><span data-ttu-id="08f8a-261">Testar o fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="08f8a-261">Test the workflow</span></span>

1. <span data-ttu-id="08f8a-262">No Designer de Aplicativos Lógicos, clique em **Executar** para iniciar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="08f8a-262">In the Logic App Designer, click **Run** to start the app.</span></span>

2. <span data-ttu-id="08f8a-263">Na coluna à esquerda, clique em **Visão Geral** para ver o status do aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="08f8a-263">In the left column, click **Overview** to see the status of the logic app.</span></span> 
 
    ![Status de execução do aplicativo lógico](media/functions-twitter-email/over1.png)

3. <span data-ttu-id="08f8a-265">(Opcional) Clique em uma das execuções para ver os detalhes da execução.</span><span class="sxs-lookup"><span data-stu-id="08f8a-265">(Optional) Click one of the runs to see details of the execution.</span></span>

4. <span data-ttu-id="08f8a-266">Vá para sua função, exiba os logs e verifique se os valores de sentimento foram recebidos e processados.</span><span class="sxs-lookup"><span data-stu-id="08f8a-266">Go to your function, view the logs, and verify that sentiment values were received and processed.</span></span>
 
    ![Exibir os logs da função](media/functions-twitter-email/sent.png)

5. <span data-ttu-id="08f8a-268">Quando um sentimento potencialmente negativo é detectado, você recebe um email.</span><span class="sxs-lookup"><span data-stu-id="08f8a-268">When a potentially negative sentiment is detected, you receive an email.</span></span> <span data-ttu-id="08f8a-269">Se você ainda não recebeu um email, poderá alterar o código de função para retornar VERMELHO sempre que:</span><span class="sxs-lookup"><span data-stu-id="08f8a-269">If you haven't received an email, you can change the function code to return RED every time:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    <span data-ttu-id="08f8a-270">Depois de verificar as notificações por email, altere para o código original:</span><span class="sxs-lookup"><span data-stu-id="08f8a-270">After you have verified email notifications, change back to the original code:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > <span data-ttu-id="08f8a-271">Depois de concluir este tutorial, você deverá desabilitar o aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="08f8a-271">After you have completed this tutorial, you should disable the logic app.</span></span> <span data-ttu-id="08f8a-272">Ao desabilitar o aplicativo, você evita ser cobrado pelas execuções e não consome as transações em sua conta dos Serviços Cognitivos.</span><span class="sxs-lookup"><span data-stu-id="08f8a-272">By disabling the app, you avoid being charged for executions and using up the transactions in your Cognitive Services account.</span></span>

<span data-ttu-id="08f8a-273">Agora você viu como é fácil integrar o Functions a um fluxo de trabalho dos Aplicativos Lógicos.</span><span class="sxs-lookup"><span data-stu-id="08f8a-273">Now you have seen how easy it is to integrate Functions into a Logic Apps workflow.</span></span>

## <a name="disable-the-logic-app"></a><span data-ttu-id="08f8a-274">Desabilitar o aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="08f8a-274">Disable the logic app</span></span>

<span data-ttu-id="08f8a-275">Para desabilitar o aplicativo lógico, clique em **Visão Geral** e clique em **Desabilitar** na parte superior da tela.</span><span class="sxs-lookup"><span data-stu-id="08f8a-275">To disable the logic app, click **Overview** and then click **Disable** at the top of the screen.</span></span> <span data-ttu-id="08f8a-276">Isso impede que o aplicativo lógico seja executado e incorra em encargos sem excluir o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="08f8a-276">This stops the logic app from running and incurring charges without deleting the app.</span></span> 

![Logs da função](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a><span data-ttu-id="08f8a-278">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="08f8a-278">Next steps</span></span>

<span data-ttu-id="08f8a-279">Neste tutorial, você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="08f8a-279">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="08f8a-280">Criar uma conta dos Serviços Cognitivos.</span><span class="sxs-lookup"><span data-stu-id="08f8a-280">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="08f8a-281">Crie uma função que categorize o sentimento do tweet.</span><span class="sxs-lookup"><span data-stu-id="08f8a-281">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="08f8a-282">Crie um aplicativo lógico que se conecte ao Twitter.</span><span class="sxs-lookup"><span data-stu-id="08f8a-282">Create a logic app that connects to Twitter.</span></span>
> * <span data-ttu-id="08f8a-283">Adicione a detecção de sentimento ao aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="08f8a-283">Add sentiment detection to the logic app.</span></span> 
> * <span data-ttu-id="08f8a-284">Conecte o aplicativo lógico à função.</span><span class="sxs-lookup"><span data-stu-id="08f8a-284">Connect the logic app to the function.</span></span>
> * <span data-ttu-id="08f8a-285">Envie um email com base na resposta da função.</span><span class="sxs-lookup"><span data-stu-id="08f8a-285">Send an email based on the response from the function.</span></span>

<span data-ttu-id="08f8a-286">Vá para o próximo tutorial para aprender a criar uma API sem servidor para sua função.</span><span class="sxs-lookup"><span data-stu-id="08f8a-286">Advance to the next tutorial to learn how to create a serverless API for your function.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="08f8a-287">Criar uma API sem servidor usando o Azure Functions</span><span class="sxs-lookup"><span data-stu-id="08f8a-287">Create a serverless API using Azure Functions</span></span>](functions-create-serverless-api.md)

<span data-ttu-id="08f8a-288">Para saber mais sobre os Aplicativos Lógicos, consulte [Aplicativos Lógicos do Azure](../logic-apps/logic-apps-what-are-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="08f8a-288">To learn more about Logic Apps, see [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).</span></span>

