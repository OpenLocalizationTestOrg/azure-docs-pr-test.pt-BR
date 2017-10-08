---
title: "aaaCreate sua primeira função da saudação Portal do Azure | Microsoft Docs"
description: "Saiba como toocreate do Azure a primeira função para a execução sem servidor usando Olá portal do Azure."
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
ms.openlocfilehash: 84283d7d4bc6015061946af4589f9a70ae61f36b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-in-hello-azure-portal"></a><span data-ttu-id="3f83b-103">Criar sua primeira função em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3f83b-103">Create your first function in hello Azure portal</span></span>

<span data-ttu-id="3f83b-104">As funções do Azure permite que você execute seu código em um ambiente sem servidor sem ter que toofirst criar uma VM ou publicar um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="3f83b-104">Azure Functions lets you execute your code in a serverless environment without having toofirst create a VM or publish a web application.</span></span> <span data-ttu-id="3f83b-105">Neste tópico, Aprenda como toouse funções toocreate uma função de "hello world" hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3f83b-105">In this topic, learn how toouse Functions toocreate a "hello world" function in hello Azure portal.</span></span>

![Criar aplicativo de função em Olá portal do Azure](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-tooazure"></a><span data-ttu-id="3f83b-107">Faça logon no tooAzure</span><span class="sxs-lookup"><span data-stu-id="3f83b-107">Log in tooAzure</span></span>

<span data-ttu-id="3f83b-108">Faça logon no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3f83b-108">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="3f83b-109">Criar um aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="3f83b-109">Create a function app</span></span>

<span data-ttu-id="3f83b-110">Você deve ter uma função aplicativo toohost Olá a execução das funções.</span><span class="sxs-lookup"><span data-stu-id="3f83b-110">You must have a function app toohost hello execution of your functions.</span></span> <span data-ttu-id="3f83b-111">Um aplicativo de funções permite a você agrupar funções como uma unidade lógica para facilitar o gerenciamento, implantação e compartilhamento de recursos.</span><span class="sxs-lookup"><span data-stu-id="3f83b-111">A function app lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

<span data-ttu-id="3f83b-112">Em seguida, crie uma função no novo aplicativo de função hello.</span><span class="sxs-lookup"><span data-stu-id="3f83b-112">Next, you create a function in hello new function app.</span></span>

## <span data-ttu-id="3f83b-113"><a name="create-function"></a>Criar uma função disparada por HTTP</span><span class="sxs-lookup"><span data-stu-id="3f83b-113"><a name="create-function"></a>Create an HTTP triggered function</span></span>

1. <span data-ttu-id="3f83b-114">Expanda seu novo aplicativo de função, clique em Olá  **+**  botão Avançar muito**funções**.</span><span class="sxs-lookup"><span data-stu-id="3f83b-114">Expand your new function app, then click hello **+** button next too**Functions**.</span></span>

2.  <span data-ttu-id="3f83b-115">Em Olá **começar rapidamente** página, selecione **WebHook + API**, **escolher um idioma** para sua função e clique em **criar esta função** .</span><span class="sxs-lookup"><span data-stu-id="3f83b-115">In hello **Get started quickly** page, select **WebHook + API**, **Choose a language** for your function, and click **Create this function**.</span></span> 
   
    ![Início rápido de funções em Olá portal do Azure.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

<span data-ttu-id="3f83b-117">Uma função é criada no seu idioma escolhido usando o modelo de saudação para uma função HTTP disparado.</span><span class="sxs-lookup"><span data-stu-id="3f83b-117">A function is created in your chosen language using hello template for an HTTP triggered function.</span></span> <span data-ttu-id="3f83b-118">Você pode executar uma nova função de saudação enviando uma solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="3f83b-118">You can run hello new function by sending an HTTP request.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="3f83b-119">Função de saudação do teste</span><span class="sxs-lookup"><span data-stu-id="3f83b-119">Test hello function</span></span>

1. <span data-ttu-id="3f83b-120">Em sua nova função, clique em **</> Obter URL da função**, selecione **padrão (Tecla de função)** e clique em **Copiar**.</span><span class="sxs-lookup"><span data-stu-id="3f83b-120">In your new function, click **</> Get function URL**, select **default (Function key)**, and then click **Copy**.</span></span> 

    ![Copiar URL da função de saudação do hello portal do Azure](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. <span data-ttu-id="3f83b-122">Cole Olá função URL na barra de endereços do navegador.</span><span class="sxs-lookup"><span data-stu-id="3f83b-122">Paste hello function URL into your browser's address bar.</span></span> <span data-ttu-id="3f83b-123">Acrescente a cadeia de caracteres de consulta de saudação `&name=<yourname>` Olá de URL e pressione toothis `Enter` chave em sua solicitação de saudação do teclado tooexecute.</span><span class="sxs-lookup"><span data-stu-id="3f83b-123">Append hello query string `&name=<yourname>` toothis URL and press hello `Enter` key on your keyboard tooexecute hello request.</span></span> <span data-ttu-id="3f83b-124">a seguir Olá é um exemplo de resposta Olá retornado pela função hello no navegador de borda hello:</span><span class="sxs-lookup"><span data-stu-id="3f83b-124">hello following is an example of hello response returned by hello function in hello Edge browser:</span></span>

    ![Resposta de função no navegador de saudação.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    <span data-ttu-id="3f83b-126">solicitação de saudação URL inclui uma chave que é necessário, por padrão, tooaccess sua função via HTTP.</span><span class="sxs-lookup"><span data-stu-id="3f83b-126">hello request URL includes a key that is required, by default, tooaccess your function over HTTP.</span></span>   

3. <span data-ttu-id="3f83b-127">Quando a função é executada, informações de rastreamento são gravadas toohello logs.</span><span class="sxs-lookup"><span data-stu-id="3f83b-127">When your function runs, trace information is written toohello logs.</span></span> <span data-ttu-id="3f83b-128">saída de rastreamento de saudação toosee de execução anterior do hello, retornar tooyour função no portal de saudação e clique em Olá a seta na parte inferior de saudação do hello tela tooexpand **Logs**.</span><span class="sxs-lookup"><span data-stu-id="3f83b-128">toosee hello trace output from hello previous execution, return tooyour function in hello portal and click hello up arrow at hello bottom of hello screen tooexpand **Logs**.</span></span> 

   ![Visualizador de log de funções no portal do Azure de saudação.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="3f83b-130">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="3f83b-130">Clean up resources</span></span>

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="3f83b-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3f83b-131">Next steps</span></span>

<span data-ttu-id="3f83b-132">Você criou um aplicativo de funções com uma função simples disparada por HTTP.</span><span class="sxs-lookup"><span data-stu-id="3f83b-132">You have created a function app with a simple HTTP triggered function.</span></span>  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="3f83b-133">Para obter mais informações, consulte [Associações HTTP e de webhook do Azure Functions](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="3f83b-133">For more information, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>



