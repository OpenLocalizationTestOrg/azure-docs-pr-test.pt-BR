---
title: "aaaCreate uma função no Azure acionado por um webhook GitHub | Microsoft Docs"
description: "Use funções do Azure toocreate uma função sem servidor que é invocada por um webhook GitHub."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 36ef34b8-3729-4940-86d2-cb8e176fcc06
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 8ffcde82c9310d749159ed53eab113658e38a030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-a-github-webhook"></a><span data-ttu-id="19369-103">Criar uma função disparada pelo webhook do GitHub</span><span class="sxs-lookup"><span data-stu-id="19369-103">Create a function triggered by a GitHub webhook</span></span>

<span data-ttu-id="19369-104">Saiba como toocreate uma função que é disparada por uma solicitação de webhook HTTP com uma carga específica do GitHub.</span><span class="sxs-lookup"><span data-stu-id="19369-104">Learn how toocreate a function that is triggered by an HTTP webhook request with a GitHub-specific payload.</span></span>

![GitHub Webhook disparado função hello portal do Azure](./media/functions-create-github-webhook-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="19369-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="19369-106">Prerequisites</span></span>

+ <span data-ttu-id="19369-107">Uma conta do GitHub com pelo menos um projeto.</span><span class="sxs-lookup"><span data-stu-id="19369-107">A GitHub account with at least one project.</span></span>
+ <span data-ttu-id="19369-108">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="19369-108">An Azure subscription.</span></span> <span data-ttu-id="19369-109">Se você não tiver uma, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="19369-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="19369-110">Criar um Aplicativo de funções do Azure</span><span class="sxs-lookup"><span data-stu-id="19369-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Aplicativo de funções criado com êxito.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="19369-112">Em seguida, crie uma função no novo aplicativo de função hello.</span><span class="sxs-lookup"><span data-stu-id="19369-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-github-webhook-triggered-function"></a><span data-ttu-id="19369-113">Criar uma função disparada pelo webhook do GitHub</span><span class="sxs-lookup"><span data-stu-id="19369-113">Create a GitHub webhook triggered function</span></span>

1. <span data-ttu-id="19369-114">Expanda seu aplicativo de função e clique em Olá  **+**  botão Avançar muito**funções**.</span><span class="sxs-lookup"><span data-stu-id="19369-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="19369-115">Se esta for a primeira função hello em seu aplicativo de função, selecione **função personalizada**.</span><span class="sxs-lookup"><span data-stu-id="19369-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="19369-116">Isso exibe o conjunto completo de saudação de modelos de função.</span><span class="sxs-lookup"><span data-stu-id="19369-116">This displays hello complete set of function templates.</span></span>

    ![Página de início rápido de funções no hello portal do Azure](./media/functions-create-github-webhook-triggered-function/add-first-function.png)

2. <span data-ttu-id="19369-118">Selecione Olá **GitHub WebHook** modelo para o idioma desejado.</span><span class="sxs-lookup"><span data-stu-id="19369-118">Select hello **GitHub WebHook** template for your desired language.</span></span> <span data-ttu-id="19369-119">**Nomeie sua função** e então selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="19369-119">**Name your function**, then select **Create**.</span></span>

     ![Criar uma função de webhook disparado GitHub em Olá portal do Azure](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger.png) 

3. <span data-ttu-id="19369-121">Em sua nova função, clique em **<> / Get função URL**, em seguida, copiar e salvar valores hello.</span><span class="sxs-lookup"><span data-stu-id="19369-121">In your new function, click **</> Get function URL**, then copy and save hello values.</span></span> <span data-ttu-id="19369-122">Olá para a mesma coisa **<> / obter GitHub segredo**.</span><span class="sxs-lookup"><span data-stu-id="19369-122">Do hello same thing for **</> Get GitHub secret**.</span></span> <span data-ttu-id="19369-123">Você pode usar essas webhook de saudação tooconfigure valores no GitHub.</span><span class="sxs-lookup"><span data-stu-id="19369-123">You use these values tooconfigure hello webhook in GitHub.</span></span>

    ![Examine o código de função hello](./media/functions-create-github-webhook-triggered-function/functions-copy-function-url-github-secret.png)

<span data-ttu-id="19369-125">Em seguida, você cria o webhook no repositório GitHub.</span><span class="sxs-lookup"><span data-stu-id="19369-125">Next, you create a webhook in your GitHub repository.</span></span>

## <a name="configure-hello-webhook"></a><span data-ttu-id="19369-126">Configurar Olá webhook</span><span class="sxs-lookup"><span data-stu-id="19369-126">Configure hello webhook</span></span>

1. <span data-ttu-id="19369-127">No GitHub, navegue tooa repositório que você possui.</span><span class="sxs-lookup"><span data-stu-id="19369-127">In GitHub, navigate tooa repository that you own.</span></span> <span data-ttu-id="19369-128">Você também pode usar qualquer repositório que você tenha bifurcado.</span><span class="sxs-lookup"><span data-stu-id="19369-128">You can also use any repository that you have forked.</span></span> <span data-ttu-id="19369-129">Se você precisar toofork um repositório, use <https://github.com/Azure-Samples/functions-quickstart>.</span><span class="sxs-lookup"><span data-stu-id="19369-129">If you need toofork a repository, use <https://github.com/Azure-Samples/functions-quickstart>.</span></span>

1. <span data-ttu-id="19369-130">Clique em **Configurações**, em seguida, clique em **Webhooks**, e **Adicionar webhook**.</span><span class="sxs-lookup"><span data-stu-id="19369-130">Click **Settings**, then click **Webhooks**, and  **Add webhook**.</span></span>

    ![Adicionar um webhook do GitHub](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-2.png)

1. <span data-ttu-id="19369-132">Use as configurações conforme especificado na tabela Olá, e clique em **adicionar webhook**.</span><span class="sxs-lookup"><span data-stu-id="19369-132">Use settings as specified in hello table, then click **Add webhook**.</span></span>

    ![Definir a URL do webhook hello e o segredo](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-3.png)

| <span data-ttu-id="19369-134">Configuração</span><span class="sxs-lookup"><span data-stu-id="19369-134">Setting</span></span> | <span data-ttu-id="19369-135">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="19369-135">Suggested value</span></span> | <span data-ttu-id="19369-136">Descrição</span><span class="sxs-lookup"><span data-stu-id="19369-136">Description</span></span> |
|---|---|---|
| <span data-ttu-id="19369-137">**URL do conteúdo**</span><span class="sxs-lookup"><span data-stu-id="19369-137">**Payload URL**</span></span> | <span data-ttu-id="19369-138">Valor copiado</span><span class="sxs-lookup"><span data-stu-id="19369-138">Copied value</span></span> | <span data-ttu-id="19369-139">Usar valor Olá retornado pela **<> / Get função URL**.</span><span class="sxs-lookup"><span data-stu-id="19369-139">Use hello value returned by  **</> Get function URL**.</span></span> |
| <span data-ttu-id="19369-140">**Segredo**</span><span class="sxs-lookup"><span data-stu-id="19369-140">**Secret**</span></span>   | <span data-ttu-id="19369-141">Valor copiado</span><span class="sxs-lookup"><span data-stu-id="19369-141">Copied value</span></span> | <span data-ttu-id="19369-142">Usar valor Olá retornado pela **<> / obter GitHub segredo**.</span><span class="sxs-lookup"><span data-stu-id="19369-142">Use hello value returned by  **</> Get GitHub secret**.</span></span> |
| <span data-ttu-id="19369-143">**Tipo de conteúdo**</span><span class="sxs-lookup"><span data-stu-id="19369-143">**Content type**</span></span> | <span data-ttu-id="19369-144">aplicativo/json</span><span class="sxs-lookup"><span data-stu-id="19369-144">application/json</span></span> | <span data-ttu-id="19369-145">função Hello espera uma carga JSON.</span><span class="sxs-lookup"><span data-stu-id="19369-145">hello function expects a JSON payload.</span></span> |
| <span data-ttu-id="19369-146">Gatilhos de evento</span><span class="sxs-lookup"><span data-stu-id="19369-146">Event triggers</span></span> | <span data-ttu-id="19369-147">Deixe-me selecionar eventos individuais</span><span class="sxs-lookup"><span data-stu-id="19369-147">Let me select individual events</span></span> | <span data-ttu-id="19369-148">Como só queremos tootrigger em eventos de comentário do problema.</span><span class="sxs-lookup"><span data-stu-id="19369-148">We only want tootrigger on issue comment events.</span></span>  |
| | <span data-ttu-id="19369-149">Comentário do problema</span><span class="sxs-lookup"><span data-stu-id="19369-149">Issue comment</span></span> |  |

<span data-ttu-id="19369-150">Agora, Olá webhook é configurado tootrigger sua função quando um novo comentário de problema é adicionado.</span><span class="sxs-lookup"><span data-stu-id="19369-150">Now, hello webhook is configured tootrigger your function when a new issue comment is added.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="19369-151">Função de saudação do teste</span><span class="sxs-lookup"><span data-stu-id="19369-151">Test hello function</span></span>

1. <span data-ttu-id="19369-152">No seu repositório GitHub, abra Olá **problemas** guia em uma nova janela do navegador.</span><span class="sxs-lookup"><span data-stu-id="19369-152">In your GitHub repository, open hello **Issues** tab in a new browser window.</span></span>

1. <span data-ttu-id="19369-153">Na nova janela de hello, clique em **novo problema**, digite um título e, em seguida, clique em **enviar novo problema**.</span><span class="sxs-lookup"><span data-stu-id="19369-153">In hello new window, click **New Issue**, type a title, and then click **Submit new issue**.</span></span>

1. <span data-ttu-id="19369-154">Edição de hello, digite um comentário e clique em **comentário**.</span><span class="sxs-lookup"><span data-stu-id="19369-154">In hello issue, type a comment and click **Comment**.</span></span>

    ![Adicione um comentário de problema do GitHub.](./media/functions-create-github-webhook-triggered-function/functions-github-webhook-add-comment.png)

1. <span data-ttu-id="19369-156">Voltar toohello portal e exibir logs de saudação.</span><span class="sxs-lookup"><span data-stu-id="19369-156">Go back toohello portal and view hello logs.</span></span> <span data-ttu-id="19369-157">Você deve ver uma entrada de rastreamento com o novo texto de comentário hello.</span><span class="sxs-lookup"><span data-stu-id="19369-157">You should see a trace entry with hello new comment text.</span></span>

     ![Exibir o texto de comentário hello nos logs de saudação.](./media/functions-create-github-webhook-triggered-function/function-app-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="19369-159">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="19369-159">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="19369-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="19369-160">Next steps</span></span>

<span data-ttu-id="19369-161">Você criou uma função que é executada quando uma solicitação é recebida de um webhook do GitHub.</span><span class="sxs-lookup"><span data-stu-id="19369-161">You have created a function that runs when a request is received from a GitHub webhook.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="19369-162">Para saber mais sobre gatilhos do webhook, veja [Associações HTTP e de webhook do Azure Functions](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="19369-162">For more information about webhook triggers, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>
