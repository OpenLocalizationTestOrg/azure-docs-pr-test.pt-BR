---
title: "Criar sua primeira função no Portal do Azure | Microsoft Docs"
description: "Aprenda a criar sua primeira Função do Azure para a execução sem servidor usando o Portal do Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 96cf87b9-8db6-41a8-863a-abb828e3d06d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/07/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 3ec1f278f21d89782137625aff200f07f15fd9fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-function-in-the-azure-portal"></a><span data-ttu-id="c27e9-103">Criar sua primeira função no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c27e9-103">Create your first function in the Azure portal</span></span>

<span data-ttu-id="c27e9-104">O Azure Functions lhe permite executar seu código em um ambiente sem servidor sem que seja preciso primeiro criar uma VM ou publicar um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="c27e9-104">Azure Functions lets you execute your code in a serverless environment without having to first create a VM or publish a web application.</span></span> <span data-ttu-id="c27e9-105">Neste tópico, aprenda a usar o Functions para criar uma função "Olá, Mundo" no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c27e9-105">In this topic, learn how to use Functions to create a "hello world" function in the Azure portal.</span></span>

![Criar um aplicativo de funções no portal do Azure](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-to-azure"></a><span data-ttu-id="c27e9-107">Fazer logon no Azure</span><span class="sxs-lookup"><span data-stu-id="c27e9-107">Log in to Azure</span></span>

<span data-ttu-id="c27e9-108">Faça logon no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c27e9-108">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="c27e9-109">Criar um aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="c27e9-109">Create a function app</span></span>

<span data-ttu-id="c27e9-110">Você deve ter um aplicativo de funções para hospedar a execução de suas funções.</span><span class="sxs-lookup"><span data-stu-id="c27e9-110">You must have a function app to host the execution of your functions.</span></span> <span data-ttu-id="c27e9-111">Um aplicativo de funções permite a você agrupar funções como uma unidade lógica para facilitar o gerenciamento, implantação e compartilhamento de recursos.</span><span class="sxs-lookup"><span data-stu-id="c27e9-111">A function app lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

<span data-ttu-id="c27e9-112">Em seguida, crie uma nova função no novo aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="c27e9-112">Next, you create a function in the new function app.</span></span>

## <span data-ttu-id="c27e9-113"><a name="create-function"></a>Criar uma função disparada por HTTP</span><span class="sxs-lookup"><span data-stu-id="c27e9-113"><a name="create-function"></a>Create an HTTP triggered function</span></span>

1. <span data-ttu-id="c27e9-114">Expanda seu novo aplicativo de funções, depois clique no botão **+** ao lado de **Functions**.</span><span class="sxs-lookup"><span data-stu-id="c27e9-114">Expand your new function app, then click the **+** button next to **Functions**.</span></span>

2.  <span data-ttu-id="c27e9-115">Na página **Início rápido**, selecione **WebHook + API**, **Escolha uma linguagem** para sua função e clique em **Criar esta função**.</span><span class="sxs-lookup"><span data-stu-id="c27e9-115">In the **Get started quickly** page, select **WebHook + API**, **Choose a language** for your function, and click **Create this function**.</span></span> 
   
    ![Início rápido de funções no Portal do Azure.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

<span data-ttu-id="c27e9-117">Uma função é criada na linguagem escolhida por você usando o modelo de uma função disparada por HTTP.</span><span class="sxs-lookup"><span data-stu-id="c27e9-117">A function is created in your chosen language using the template for an HTTP triggered function.</span></span> <span data-ttu-id="c27e9-118">Você pode executar a nova função enviando uma solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="c27e9-118">You can run the new function by sending an HTTP request.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="c27e9-119">Testar a função</span><span class="sxs-lookup"><span data-stu-id="c27e9-119">Test the function</span></span>

1. <span data-ttu-id="c27e9-120">Em sua nova função, clique em **</> Obter URL da função**, selecione **padrão (Tecla de função)** e clique em **Copiar**.</span><span class="sxs-lookup"><span data-stu-id="c27e9-120">In your new function, click **</> Get function URL**, select **default (Function key)**, and then click **Copy**.</span></span> 

    ![Copiar a URL da função do Portal do Azure](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. <span data-ttu-id="c27e9-122">Cole a URL de função na barra de endereços do navegador.</span><span class="sxs-lookup"><span data-stu-id="c27e9-122">Paste the function URL into your browser's address bar.</span></span> <span data-ttu-id="c27e9-123">Acrescente a cadeia de caracteres de consulta `&name=<yourname>` a esta URL e pressione `Enter` em seu teclado para executar a solicitação.</span><span class="sxs-lookup"><span data-stu-id="c27e9-123">Append the query string `&name=<yourname>` to this URL and press the `Enter` key on your keyboard to execute the request.</span></span> <span data-ttu-id="c27e9-124">A seguir, um exemplo de resposta retornada pela função no navegador Edge:</span><span class="sxs-lookup"><span data-stu-id="c27e9-124">The following is an example of the response returned by the function in the Edge browser:</span></span>

    ![Resposta da função no navegador.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    <span data-ttu-id="c27e9-126">A URL da solicitação inclui uma chave que é necessária, por padrão, para acessar sua função via HTTP.</span><span class="sxs-lookup"><span data-stu-id="c27e9-126">The request URL includes a key that is required, by default, to access your function over HTTP.</span></span>   

3. <span data-ttu-id="c27e9-127">Quando a função é executada, informações de rastreamento são gravadas nos logs.</span><span class="sxs-lookup"><span data-stu-id="c27e9-127">When your function runs, trace information is written to the logs.</span></span> <span data-ttu-id="c27e9-128">Para ver a saída do rastreamento da execução anterior, volte para sua função no portal e clique na seta para cima na parte inferior da tela para expandir **Logs**.</span><span class="sxs-lookup"><span data-stu-id="c27e9-128">To see the trace output from the previous execution, return to your function in the portal and click the up arrow at the bottom of the screen to expand **Logs**.</span></span> 

   ![Visualizador de log de função no Portal do Azure.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="c27e9-130">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="c27e9-130">Clean up resources</span></span>

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="c27e9-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c27e9-131">Next steps</span></span>

<span data-ttu-id="c27e9-132">Você criou um aplicativo de funções com uma função simples disparada por HTTP.</span><span class="sxs-lookup"><span data-stu-id="c27e9-132">You have created a function app with a simple HTTP triggered function.</span></span>  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="c27e9-133">Para obter mais informações, consulte [Associações HTTP e de webhook do Azure Functions](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="c27e9-133">For more information, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>



