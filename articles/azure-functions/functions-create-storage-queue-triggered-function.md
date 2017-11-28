---
title: "uma função no Azure acionado por mensagens da fila de aaaCreate | Microsoft Docs"
description: "Use funções do Azure toocreate uma função sem servidor que é invocada por uma mensagem enviada tooan fila de armazenamento do Azure."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361da2a4-15d1-4903-bdc4-cc4b27fc3ff4
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: e9501ed336b502eaeee3fa62ec4ae085c76de0ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-queue-storage"></a><span data-ttu-id="48d2d-103">Criar uma função disparada pelo Armazenamento de Filas do Azure</span><span class="sxs-lookup"><span data-stu-id="48d2d-103">Create a function triggered by Azure Queue storage</span></span>

<span data-ttu-id="48d2d-104">Saiba como toocreate uma função disparada quando mensagens são enviadas tooan fila de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="48d2d-104">Learn how toocreate a function triggered when messages are submitted tooan Azure Storage queue.</span></span>

![Exibir mensagem nos logs de saudação.](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="48d2d-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="48d2d-106">Prerequisites</span></span>

- <span data-ttu-id="48d2d-107">Baixe e instale Olá [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="48d2d-107">Download and install hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

- <span data-ttu-id="48d2d-108">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="48d2d-108">An Azure subscription.</span></span> <span data-ttu-id="48d2d-109">Se você não tiver uma, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="48d2d-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="48d2d-110">Criar um Aplicativo de funções do Azure</span><span class="sxs-lookup"><span data-stu-id="48d2d-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Aplicativo de funções criado com êxito.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="48d2d-112">Em seguida, crie uma função no novo aplicativo de função hello.</span><span class="sxs-lookup"><span data-stu-id="48d2d-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a><span data-ttu-id="48d2d-113">Criar uma função disparada por Filas</span><span class="sxs-lookup"><span data-stu-id="48d2d-113">Create a Queue triggered function</span></span>

1. <span data-ttu-id="48d2d-114">Expanda seu aplicativo de função e clique em Olá  **+**  botão Avançar muito**funções**.</span><span class="sxs-lookup"><span data-stu-id="48d2d-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="48d2d-115">Se esta for a primeira função hello em seu aplicativo de função, selecione **função personalizada**.</span><span class="sxs-lookup"><span data-stu-id="48d2d-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="48d2d-116">Isso exibe o conjunto completo de saudação de modelos de função.</span><span class="sxs-lookup"><span data-stu-id="48d2d-116">This displays hello complete set of function templates.</span></span>

    ![Página de início rápido de funções no hello portal do Azure](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. <span data-ttu-id="48d2d-118">Selecione Olá **QueueTrigger** modelo para o idioma desejado e usar configurações de saudação conforme especificado na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="48d2d-118">Select hello **QueueTrigger** template for your desired language, and  use hello settings as specified in hello table.</span></span>

    ![Crie função de fila disparada armazenamento hello.](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)
    
    | <span data-ttu-id="48d2d-120">Configuração</span><span class="sxs-lookup"><span data-stu-id="48d2d-120">Setting</span></span> | <span data-ttu-id="48d2d-121">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="48d2d-121">Suggested value</span></span> | <span data-ttu-id="48d2d-122">Descrição</span><span class="sxs-lookup"><span data-stu-id="48d2d-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="48d2d-123">**Nome da fila**</span><span class="sxs-lookup"><span data-stu-id="48d2d-123">**Queue name**</span></span>   | <span data-ttu-id="48d2d-124">myqueue-items</span><span class="sxs-lookup"><span data-stu-id="48d2d-124">myqueue-items</span></span>    | <span data-ttu-id="48d2d-125">Nome da saudação fila tooconnect tooin sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="48d2d-125">Name of hello queue tooconnect tooin your Storage account.</span></span> |
    | <span data-ttu-id="48d2d-126">**Conexão da conta de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="48d2d-126">**Storage account connection**</span></span> | <span data-ttu-id="48d2d-127">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="48d2d-127">AzureWebJobStorage</span></span> | <span data-ttu-id="48d2d-128">Você pode usar a conexão de conta de armazenamento Olá já está sendo usado pelo seu aplicativo de função ou criar um novo.</span><span class="sxs-lookup"><span data-stu-id="48d2d-128">You can use hello storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="48d2d-129">**Nomeie sua função**</span><span class="sxs-lookup"><span data-stu-id="48d2d-129">**Name your function**</span></span> | <span data-ttu-id="48d2d-130">Exclusivo no aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="48d2d-130">Unique in your function app</span></span> | <span data-ttu-id="48d2d-131">O nome dessa função disparada por filas.</span><span class="sxs-lookup"><span data-stu-id="48d2d-131">Name of this queue triggered function.</span></span> |

3. <span data-ttu-id="48d2d-132">Clique em **criar** toocreate sua função.</span><span class="sxs-lookup"><span data-stu-id="48d2d-132">Click **Create** toocreate your function.</span></span>

<span data-ttu-id="48d2d-133">Em seguida, conecte-se a conta de armazenamento do Azure tooyour e criar hello **myqueue itens** fila de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="48d2d-133">Next, you connect tooyour Azure Storage account and create hello **myqueue-items** storage queue.</span></span>

## <a name="create-hello-queue"></a><span data-ttu-id="48d2d-134">Criar fila Olá</span><span class="sxs-lookup"><span data-stu-id="48d2d-134">Create hello queue</span></span>

1. <span data-ttu-id="48d2d-135">Em sua função, clique em **Integrar**, expanda **Documentação**e copie **Nome da conta** e **Chave de conta**.</span><span class="sxs-lookup"><span data-stu-id="48d2d-135">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="48d2d-136">Você usar a conta de armazenamento essas credenciais tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="48d2d-136">You use these credentials tooconnect toohello storage account.</span></span> <span data-ttu-id="48d2d-137">Se você já se conectou a sua conta de armazenamento, ignore toostep 4.</span><span class="sxs-lookup"><span data-stu-id="48d2d-137">If you have already connected your storage account, skip toostep 4.</span></span>

    ![Obter credenciais de conexão de conta de armazenamento hello.](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)<span data-ttu-id="48d2d-139">v</span><span class="sxs-lookup"><span data-stu-id="48d2d-139">v</span></span>

1. <span data-ttu-id="48d2d-140">Executar Olá [Microsoft Azure Storage Explorer](http://storageexplorer.com/) ferramenta, clique em Olá conectar ícone Olá esquerda, escolha **usar um nome de conta de armazenamento e chave**e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="48d2d-140">Run hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click hello connect icon on hello left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Execute a ferramenta de Gerenciador de conta de armazenamento de saudação.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="48d2d-142">Digite hello **nome da conta** e **chave de conta** da etapa 1, clique em **próximo** e, em seguida, **conectar**.</span><span class="sxs-lookup"><span data-stu-id="48d2d-142">Enter hello **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span>

    ![Insira as credenciais de armazenamento hello e conecte-se.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="48d2d-144">Expanda a conta de armazenamento Olá anexado, clique no **filas**, clique em **criar fila**, tipo `myqueue-items`, e pressione enter.</span><span class="sxs-lookup"><span data-stu-id="48d2d-144">Expand hello attached storage account, right-click **Queues**, click **Create queue**, type `myqueue-items`, and then press enter.</span></span>

    ![Crie uma fila de armazenamento.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

<span data-ttu-id="48d2d-146">Agora que você tem uma fila de armazenamento, você pode testar a função hello, adicionando uma fila de mensagens toohello.</span><span class="sxs-lookup"><span data-stu-id="48d2d-146">Now that you have a storage queue, you can test hello function by adding a message toohello queue.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="48d2d-147">Função de saudação do teste</span><span class="sxs-lookup"><span data-stu-id="48d2d-147">Test hello function</span></span>

1. <span data-ttu-id="48d2d-148">Em Olá portal do Azure, procurar tooyour função expanda Olá **Logs** na parte inferior da saudação da página de saudação e verifique se esse fluxo de log não está em pausa.</span><span class="sxs-lookup"><span data-stu-id="48d2d-148">Back in hello Azure portal, browse tooyour function expand hello **Logs** at hello bottom of hello page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="48d2d-149">No Gerenciador de Armazenamento, expanda sua conta de armazenamento, **Filas** e **myqueue-items**; em seguida, clique em **Adicionar mensagem**.</span><span class="sxs-lookup"><span data-stu-id="48d2d-149">In Storage Explorer, expand your storage account, **Queues**, and **myqueue-items**, then click **Add message**.</span></span>

    ![Adicione uma fila de mensagens toohello.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. <span data-ttu-id="48d2d-151">Digite sua mensagem "Olá, Mundo!"</span><span class="sxs-lookup"><span data-stu-id="48d2d-151">Type your "Hello World!"</span></span> <span data-ttu-id="48d2d-152">em **Texto da mensagem** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="48d2d-152">message in **Message text** and click **OK**.</span></span>

1. <span data-ttu-id="48d2d-153">Espere alguns segundos, em seguida, voltar tooyour função logs e verifique se que essa nova mensagem de saudação foi lida da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="48d2d-153">Wait for a few seconds, then go back tooyour function logs and verify that hello new message has been read from hello queue.</span></span>

    ![Exibir mensagem nos logs de saudação.](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. <span data-ttu-id="48d2d-155">No Gerenciador de armazenamento, clique em **atualização** e verifique se essa mensagem de saudação foi processada e não está mais na fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="48d2d-155">Back in Storage Explorer, click **Refresh** and verify that hello message has been processed and is no longer in hello queue.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="48d2d-156">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="48d2d-156">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="48d2d-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="48d2d-157">Next steps</span></span>

<span data-ttu-id="48d2d-158">Você criou uma função que é executada quando uma mensagem é adicionada tooa fila de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="48d2d-158">You have created a function that runs when a message is added tooa storage queue.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="48d2d-159">Para obter mais informações sobre gatilhos de Armazenamento de Filas, consulte [Associações de fila do Armazenamento do Azure Functions](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="48d2d-159">For more information about Queue storage triggers, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span>