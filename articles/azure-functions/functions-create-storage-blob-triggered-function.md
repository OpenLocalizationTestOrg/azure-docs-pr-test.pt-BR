---
title: "uma função no Azure disparado pelo armazenamento de Blob de aaaCreate | Microsoft Docs"
description: "Use funções do Azure toocreate uma função sem servidor que é invocada por itens adicionados tooAzure armazenamento de Blob."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: d6bff41c-a624-40c1-bbc7-80590df29ded
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: acb7d29abb07a22da11d0e65d2ed54591f8e3f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-blob-storage"></a><span data-ttu-id="e44b2-103">Criar uma função disparada pelo Armazenamento de Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="e44b2-103">Create a function triggered by Azure Blob storage</span></span>

<span data-ttu-id="e44b2-104">Saiba como toocreate uma função disparada quando os arquivos são carregados tooor atualizado no armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="e44b2-104">Learn how toocreate a function triggered when files are uploaded tooor updated in Azure Blob storage.</span></span>

![Exibir mensagem nos logs de saudação.](./media/functions-create-storage-blob-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="e44b2-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e44b2-106">Prerequisites</span></span>

+ <span data-ttu-id="e44b2-107">Baixe e instale Olá [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="e44b2-107">Download and install hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
+ <span data-ttu-id="e44b2-108">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e44b2-108">An Azure subscription.</span></span> <span data-ttu-id="e44b2-109">Se você não tiver uma, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="e44b2-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="e44b2-110">Criar um Aplicativo de funções do Azure</span><span class="sxs-lookup"><span data-stu-id="e44b2-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Aplicativo de funções criado com êxito.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="e44b2-112">Em seguida, crie uma função no novo aplicativo de função hello.</span><span class="sxs-lookup"><span data-stu-id="e44b2-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-blob-storage-triggered-function"></a><span data-ttu-id="e44b2-113">Criar uma função disparada pelo Armazenamento de Blobs</span><span class="sxs-lookup"><span data-stu-id="e44b2-113">Create a Blob storage triggered function</span></span>

1. <span data-ttu-id="e44b2-114">Expanda seu aplicativo de função e clique em Olá  **+**  botão Avançar muito**funções**.</span><span class="sxs-lookup"><span data-stu-id="e44b2-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="e44b2-115">Se esta for a primeira função hello em seu aplicativo de função, selecione **função personalizada**.</span><span class="sxs-lookup"><span data-stu-id="e44b2-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="e44b2-116">Isso exibe o conjunto completo de saudação de modelos de função.</span><span class="sxs-lookup"><span data-stu-id="e44b2-116">This displays hello complete set of function templates.</span></span>

    ![Página de início rápido de funções no hello portal do Azure](./media/functions-create-storage-blob-triggered-function/add-first-function.png)

2. <span data-ttu-id="e44b2-118">Selecione Olá **BlobTrigger** modelo para o idioma desejado e usar configurações de saudação conforme especificado na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="e44b2-118">Select hello **BlobTrigger** template for your desired language, and use hello settings as specified in hello table.</span></span>

    ![Crie função de armazenamento disparado Blob hello.](./media/functions-create-storage-blob-triggered-function/functions-create-blob-storage-trigger-portal.png)

    | <span data-ttu-id="e44b2-120">Configuração</span><span class="sxs-lookup"><span data-stu-id="e44b2-120">Setting</span></span> | <span data-ttu-id="e44b2-121">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="e44b2-121">Suggested value</span></span> | <span data-ttu-id="e44b2-122">Descrição</span><span class="sxs-lookup"><span data-stu-id="e44b2-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="e44b2-123">**Caminho**</span><span class="sxs-lookup"><span data-stu-id="e44b2-123">**Path**</span></span>   | <span data-ttu-id="e44b2-124">mycontainer/{name}</span><span class="sxs-lookup"><span data-stu-id="e44b2-124">mycontainer/{name}</span></span>    | <span data-ttu-id="e44b2-125">Local no Armazenamento de Blobs que está sendo monitorada.</span><span class="sxs-lookup"><span data-stu-id="e44b2-125">Location in Blob storage being monitored.</span></span> <span data-ttu-id="e44b2-126">nome do arquivo de saudação do blob Olá é passado na associação de saudação como Olá _nome_ parâmetro.</span><span class="sxs-lookup"><span data-stu-id="e44b2-126">hello file name of hello blob is passed in hello binding as hello _name_ parameter.</span></span>  |
    | <span data-ttu-id="e44b2-127">**Conexão da conta de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="e44b2-127">**Storage account connection**</span></span> | <span data-ttu-id="e44b2-128">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="e44b2-128">AzureWebJobStorage</span></span> | <span data-ttu-id="e44b2-129">Você pode usar a conexão de conta de armazenamento Olá já está sendo usado pelo seu aplicativo de função ou criar um novo.</span><span class="sxs-lookup"><span data-stu-id="e44b2-129">You can use hello storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="e44b2-130">**Nomeie sua função**</span><span class="sxs-lookup"><span data-stu-id="e44b2-130">**Name your function**</span></span> | <span data-ttu-id="e44b2-131">Exclusivo no aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="e44b2-131">Unique in your function app</span></span> | <span data-ttu-id="e44b2-132">O nome dessa função disparada pelo blob.</span><span class="sxs-lookup"><span data-stu-id="e44b2-132">Name of this blob triggered function.</span></span> |

3. <span data-ttu-id="e44b2-133">Clique em **criar** toocreate sua função.</span><span class="sxs-lookup"><span data-stu-id="e44b2-133">Click **Create** toocreate your function.</span></span>

<span data-ttu-id="e44b2-134">Em seguida, conecte-se a conta de armazenamento do Azure tooyour e criar hello **mycontainer** contêiner.</span><span class="sxs-lookup"><span data-stu-id="e44b2-134">Next, you connect tooyour Azure Storage account and create hello **mycontainer** container.</span></span>

## <a name="create-hello-container"></a><span data-ttu-id="e44b2-135">Criar contêiner Olá</span><span class="sxs-lookup"><span data-stu-id="e44b2-135">Create hello container</span></span>

1. <span data-ttu-id="e44b2-136">Em sua função, clique em **Integrar**, expanda **Documentação**e copie **Nome da conta** e **Chave de conta**.</span><span class="sxs-lookup"><span data-stu-id="e44b2-136">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="e44b2-137">Você usar a conta de armazenamento essas credenciais tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="e44b2-137">You use these credentials tooconnect toohello storage account.</span></span> <span data-ttu-id="e44b2-138">Se você já se conectou a sua conta de armazenamento, ignore toostep 4.</span><span class="sxs-lookup"><span data-stu-id="e44b2-138">If you have already connected your storage account, skip toostep 4.</span></span>

    ![Obter credenciais de conexão de conta de armazenamento hello.](./media/functions-create-storage-blob-triggered-function/functions-storage-account-connection.png)

1. <span data-ttu-id="e44b2-140">Executar Olá [Microsoft Azure Storage Explorer](http://storageexplorer.com/) ferramenta, clique em Olá conectar ícone Olá esquerda, escolha **usar um nome de conta de armazenamento e chave**e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="e44b2-140">Run hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click hello connect icon on hello left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Execute a ferramenta de Gerenciador de conta de armazenamento de saudação.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="e44b2-142">Digite hello **nome da conta** e **chave de conta** da etapa 1, clique em **próximo** e, em seguida, **conectar**.</span><span class="sxs-lookup"><span data-stu-id="e44b2-142">Enter hello **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span> 

    ![Insira as credenciais de armazenamento hello e conecte-se.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="e44b2-144">Expanda a conta de armazenamento Olá anexado, clique no **contêineres de Blob**, clique em **criar contêiner de blob**, tipo `mycontainer`, e pressione enter.</span><span class="sxs-lookup"><span data-stu-id="e44b2-144">Expand hello attached storage account, right-click **Blob containers**, click **Create blob container**, type `mycontainer`, and then press enter.</span></span>

    ![Crie uma fila de armazenamento.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-create-blob-container.png)

<span data-ttu-id="e44b2-146">Agora que você tem um contêiner de blob, você pode testar a função hello carregando um contêiner de toohello do arquivo.</span><span class="sxs-lookup"><span data-stu-id="e44b2-146">Now that you have a blob container, you can test hello function by uploading a file toohello container.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="e44b2-147">Função de saudação do teste</span><span class="sxs-lookup"><span data-stu-id="e44b2-147">Test hello function</span></span>

1. <span data-ttu-id="e44b2-148">Em Olá portal do Azure, procurar tooyour função expanda Olá **Logs** na parte inferior da saudação da página de saudação e verifique se esse fluxo de log não está em pausa.</span><span class="sxs-lookup"><span data-stu-id="e44b2-148">Back in hello Azure portal, browse tooyour function expand hello **Logs** at hello bottom of hello page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="e44b2-149">No Gerenciador de Armazenamento, expanda sua conta de armazenamento, **Contêineres de blob** e **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="e44b2-149">In Storage Explorer, expand your storage account, **Blob containers**, and **mycontainer**.</span></span> <span data-ttu-id="e44b2-150">Clique em **Carregar** e depois em **Carregar arquivos...**.</span><span class="sxs-lookup"><span data-stu-id="e44b2-150">Click **Upload** and then **Upload files...**.</span></span>

    ![Carregar um contêiner de blob de toohello do arquivo.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-upload-file-blob.png)

1. <span data-ttu-id="e44b2-152">Em Olá **carregar arquivos** caixa de diálogo, clique em Olá **arquivos** campo.</span><span class="sxs-lookup"><span data-stu-id="e44b2-152">In hello **Upload files** dialog box, click hello **Files** field.</span></span> <span data-ttu-id="e44b2-153">Procurar arquivo tooa no computador local, como um arquivo de imagem, selecione-o e clique em **abrir** e **carregar**.</span><span class="sxs-lookup"><span data-stu-id="e44b2-153">Browse tooa file on your local computer, such as an image file, select it and click **Open** and then **Upload**.</span></span>

1. <span data-ttu-id="e44b2-154">Voltar tooyour função logs e verifique se que esse blob Olá foi lido.</span><span class="sxs-lookup"><span data-stu-id="e44b2-154">Go back tooyour function logs and verify that hello blob has been read.</span></span>

   ![Exibir mensagem nos logs de saudação.](./media/functions-create-storage-blob-triggered-function/functions-blob-storage-trigger-view-logs.png)

    >[!NOTE]
    > <span data-ttu-id="e44b2-156">Quando seu aplicativo de função é executado no plano de consumo saudação padrão, pode haver um atraso de backup tooseveral minutos entre Olá blob que está sendo adicionado ou atualizado e Olá de função que está sendo disparado.</span><span class="sxs-lookup"><span data-stu-id="e44b2-156">When your function app runs in hello default Consumption plan, there may be a delay of up tooseveral minutes between hello blob being added or updated and hello function being triggered.</span></span> <span data-ttu-id="e44b2-157">Se você precisar de baixa latência em suas funções disparadas por blob, considere executar seu aplicativo de funções em um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e44b2-157">If you need low latency in your blob triggered functions, consider running your function app in an App Service plan.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="e44b2-158">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="e44b2-158">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="e44b2-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e44b2-159">Next steps</span></span>

<span data-ttu-id="e44b2-160">Você criou uma função que é executada quando um blob é adicionado tooor atualizado no armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="e44b2-160">You have created a function that runs when a blob is added tooor updated in Blob storage.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="e44b2-161">Para obter mais informações sobre gatilhos de armazenamento de blobs, consulte [Associações de Armazenamento de Blobs do Azure Functions](functions-bindings-storage-blob.md).</span><span class="sxs-lookup"><span data-stu-id="e44b2-161">For more information about Blob storage triggers, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md).</span></span>
