---
title: "Criar uma função no Azure disparada por mensagens na fila | Microsoft Docs"
description: "Use o Azure Functions para criar uma função sem servidor que é invocada por uma mensagem enviada para uma fila do Armazenamento do Azure."
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
ms.openlocfilehash: 92a03154bf5a8945e2de9606afd138803c76fafe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-triggered-by-azure-queue-storage"></a><span data-ttu-id="96668-103">Criar uma função disparada pelo Armazenamento de Filas do Azure</span><span class="sxs-lookup"><span data-stu-id="96668-103">Create a function triggered by Azure Queue storage</span></span>

<span data-ttu-id="96668-104">Saiba como criar uma função disparada quando as mensagens são enviadas para uma fila do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="96668-104">Learn how to create a function triggered when messages are submitted to an Azure Storage queue.</span></span>

![Exiba a mensagem nos logs.](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="96668-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="96668-106">Prerequisites</span></span>

- <span data-ttu-id="96668-107">Baixe e instale o [Gerenciador de Armazenamento do Microsoft Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="96668-107">Download and install the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

- <span data-ttu-id="96668-108">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="96668-108">An Azure subscription.</span></span> <span data-ttu-id="96668-109">Se você não tiver uma, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="96668-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="96668-110">Criar um Aplicativo de funções do Azure</span><span class="sxs-lookup"><span data-stu-id="96668-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Aplicativo de funções criado com êxito.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="96668-112">Em seguida, crie uma nova função no novo aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="96668-112">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a><span data-ttu-id="96668-113">Criar uma função disparada por Filas</span><span class="sxs-lookup"><span data-stu-id="96668-113">Create a Queue triggered function</span></span>

1. <span data-ttu-id="96668-114">Expanda seu aplicativo de funções e clique no botão **+** ao lado de **Functions**.</span><span class="sxs-lookup"><span data-stu-id="96668-114">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="96668-115">Se essa for a primeira função em seu aplicativo de funções, selecione **Função personalizada**.</span><span class="sxs-lookup"><span data-stu-id="96668-115">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="96668-116">Exibe o conjunto completo de modelos de função.</span><span class="sxs-lookup"><span data-stu-id="96668-116">This displays the complete set of function templates.</span></span>

    ![Página de início rápido de funções no portal do Azure](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. <span data-ttu-id="96668-118">Selecione o modelo **QueueTrigger** para o idioma desejado e use as configurações especificadas na tabela.</span><span class="sxs-lookup"><span data-stu-id="96668-118">Select the **QueueTrigger** template for your desired language, and  use the settings as specified in the table.</span></span>

    ![Crie a função disparada por filas de armazenamento.](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)
    
    | <span data-ttu-id="96668-120">Configuração</span><span class="sxs-lookup"><span data-stu-id="96668-120">Setting</span></span> | <span data-ttu-id="96668-121">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="96668-121">Suggested value</span></span> | <span data-ttu-id="96668-122">Descrição</span><span class="sxs-lookup"><span data-stu-id="96668-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="96668-123">**Nome da fila**</span><span class="sxs-lookup"><span data-stu-id="96668-123">**Queue name**</span></span>   | <span data-ttu-id="96668-124">myqueue-items</span><span class="sxs-lookup"><span data-stu-id="96668-124">myqueue-items</span></span>    | <span data-ttu-id="96668-125">Nome da fila à qual se conectar em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="96668-125">Name of the queue to connect to in your Storage account.</span></span> |
    | <span data-ttu-id="96668-126">**Conexão da conta de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="96668-126">**Storage account connection**</span></span> | <span data-ttu-id="96668-127">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="96668-127">AzureWebJobStorage</span></span> | <span data-ttu-id="96668-128">Você pode usar a conexão da conta de armazenamento que já está sendo usada por seu aplicativo de funções ou criar uma nova.</span><span class="sxs-lookup"><span data-stu-id="96668-128">You can use the storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="96668-129">**Nomeie sua função**</span><span class="sxs-lookup"><span data-stu-id="96668-129">**Name your function**</span></span> | <span data-ttu-id="96668-130">Exclusivo no aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="96668-130">Unique in your function app</span></span> | <span data-ttu-id="96668-131">O nome dessa função disparada por filas.</span><span class="sxs-lookup"><span data-stu-id="96668-131">Name of this queue triggered function.</span></span> |

3. <span data-ttu-id="96668-132">Clique em **Criar** para criar a função.</span><span class="sxs-lookup"><span data-stu-id="96668-132">Click **Create** to create your function.</span></span>

<span data-ttu-id="96668-133">Em seguida, você pode se conectar à sua conta de armazenamento do Azure e criar a fila de armazenamento **myqueue-items**.</span><span class="sxs-lookup"><span data-stu-id="96668-133">Next, you connect to your Azure Storage account and create the **myqueue-items** storage queue.</span></span>

## <a name="create-the-queue"></a><span data-ttu-id="96668-134">Criar a fila</span><span class="sxs-lookup"><span data-stu-id="96668-134">Create the queue</span></span>

1. <span data-ttu-id="96668-135">Em sua função, clique em **Integrar**, expanda **Documentação**e copie **Nome da conta** e **Chave de conta**.</span><span class="sxs-lookup"><span data-stu-id="96668-135">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="96668-136">Você usa essas credenciais para conectar-se à conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="96668-136">You use these credentials to connect to the storage account.</span></span> <span data-ttu-id="96668-137">Se você já tiver se conectado à conta de armazenamento, vá para a etapa 4.</span><span class="sxs-lookup"><span data-stu-id="96668-137">If you have already connected your storage account, skip to step 4.</span></span>

    ![Obtenha as credenciais de conexão da conta de armazenamento.](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)<span data-ttu-id="96668-139">v</span><span class="sxs-lookup"><span data-stu-id="96668-139">v</span></span>

1. <span data-ttu-id="96668-140">Execute a ferramenta [Gerenciador de Armazenamento do Microsoft Azure](http://storageexplorer.com/), clique no ícone conectar-se à esquerda, escolha **Usar um nome e chave de conta de armazenamento** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="96668-140">Run the [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click the connect icon on the left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Execute a ferramenta Gerenciador de Conta de Armazenamento.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="96668-142">Insira o **Nome da conta** e **Chave de conta** da etapa 1, clique em **Avançar** e em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="96668-142">Enter the **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span>

    ![Insira as credenciais de armazenamento e conecte-se.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="96668-144">Expanda a conta de armazenamento anexada, clique com o botão direito do mouse em **Filas**, clique em **Criar fila**, digite `myqueue-items` e pressione enter.</span><span class="sxs-lookup"><span data-stu-id="96668-144">Expand the attached storage account, right-click **Queues**, click **Create queue**, type `myqueue-items`, and then press enter.</span></span>

    ![Crie uma fila de armazenamento.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

<span data-ttu-id="96668-146">Agora que você tem uma fila de armazenamento, você pode testar a função adicionando uma mensagem à fila.</span><span class="sxs-lookup"><span data-stu-id="96668-146">Now that you have a storage queue, you can test the function by adding a message to the queue.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="96668-147">Testar a função</span><span class="sxs-lookup"><span data-stu-id="96668-147">Test the function</span></span>

1. <span data-ttu-id="96668-148">De volta ao Portal do Azure, navegue até sua função, expanda os **Logs** na parte inferior da página e verifique se o streaming de log não está em pausa.</span><span class="sxs-lookup"><span data-stu-id="96668-148">Back in the Azure portal, browse to your function expand the **Logs** at the bottom of the page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="96668-149">No Gerenciador de Armazenamento, expanda sua conta de armazenamento, **Filas** e **myqueue-items**; em seguida, clique em **Adicionar mensagem**.</span><span class="sxs-lookup"><span data-stu-id="96668-149">In Storage Explorer, expand your storage account, **Queues**, and **myqueue-items**, then click **Add message**.</span></span>

    ![Adicione uma mensagem à fila.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. <span data-ttu-id="96668-151">Digite sua mensagem "Olá, Mundo!"</span><span class="sxs-lookup"><span data-stu-id="96668-151">Type your "Hello World!"</span></span> <span data-ttu-id="96668-152">em **Texto da mensagem** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="96668-152">message in **Message text** and click **OK**.</span></span>

1. <span data-ttu-id="96668-153">Aguarde alguns segundos, depois volte para seus logs de função e verifique se a nova mensagem foi lida da fila.</span><span class="sxs-lookup"><span data-stu-id="96668-153">Wait for a few seconds, then go back to your function logs and verify that the new message has been read from the queue.</span></span>

    ![Exiba a mensagem nos logs.](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. <span data-ttu-id="96668-155">No Gerenciador de Armazenamento, clique em **Atualizar** e verifique se a mensagem foi processada e se não está mais na fila.</span><span class="sxs-lookup"><span data-stu-id="96668-155">Back in Storage Explorer, click **Refresh** and verify that the message has been processed and is no longer in the queue.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="96668-156">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="96668-156">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="96668-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="96668-157">Next steps</span></span>

<span data-ttu-id="96668-158">Você criou uma função que é executada quando uma mensagem é adicionada a uma fila de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="96668-158">You have created a function that runs when a message is added to a storage queue.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="96668-159">Para obter mais informações sobre gatilhos de Armazenamento de Filas, consulte [Associações de fila do Armazenamento do Azure Functions](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="96668-159">For more information about Queue storage triggers, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span>