---
title: "Criar uma função no Azure disparada pelo Armazenamento de Blobs | Microsoft Docs"
description: "Use o Azure Functions para criar uma função sem servidor que é invocada por itens adicionados ao Armazenamento de Blobs do Azure."
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
ms.openlocfilehash: 1ddd056903b1a2f973a58bd7054ea2b8281607c3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-triggered-by-azure-blob-storage"></a><span data-ttu-id="fe0e0-103">Criar uma função disparada pelo Armazenamento de Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="fe0e0-103">Create a function triggered by Azure Blob storage</span></span>

<span data-ttu-id="fe0e0-104">Saiba como criar uma função disparada quando arquivos são carregados ou atualizados no Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-104">Learn how to create a function triggered when files are uploaded to or updated in Azure Blob storage.</span></span>

![Exiba a mensagem nos logs.](./media/functions-create-storage-blob-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="fe0e0-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fe0e0-106">Prerequisites</span></span>

+ <span data-ttu-id="fe0e0-107">Baixe e instale o [Gerenciador de Armazenamento do Microsoft Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="fe0e0-107">Download and install the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
+ <span data-ttu-id="fe0e0-108">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-108">An Azure subscription.</span></span> <span data-ttu-id="fe0e0-109">Se você não tiver uma, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="fe0e0-110">Criar um Aplicativo de funções do Azure</span><span class="sxs-lookup"><span data-stu-id="fe0e0-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Aplicativo de funções criado com êxito.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="fe0e0-112">Em seguida, crie uma nova função no novo aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-112">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-blob-storage-triggered-function"></a><span data-ttu-id="fe0e0-113">Criar uma função disparada pelo Armazenamento de Blobs</span><span class="sxs-lookup"><span data-stu-id="fe0e0-113">Create a Blob storage triggered function</span></span>

1. <span data-ttu-id="fe0e0-114">Expanda seu aplicativo de funções e clique no botão **+** ao lado de **Functions**.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-114">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="fe0e0-115">Se essa for a primeira função em seu aplicativo de funções, selecione **Função personalizada**.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-115">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="fe0e0-116">Exibe o conjunto completo de modelos de função.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-116">This displays the complete set of function templates.</span></span>

    ![Página de início rápido de funções no portal do Azure](./media/functions-create-storage-blob-triggered-function/add-first-function.png)

2. <span data-ttu-id="fe0e0-118">Selecione o modelo **BlobTrigger** para o idioma desejado e use as configurações especificadas na tabela.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-118">Select the **BlobTrigger** template for your desired language, and use the settings as specified in the table.</span></span>

    ![Crie a função disparada pelo Armazenamento de Blobs.](./media/functions-create-storage-blob-triggered-function/functions-create-blob-storage-trigger-portal.png)

    | <span data-ttu-id="fe0e0-120">Configuração</span><span class="sxs-lookup"><span data-stu-id="fe0e0-120">Setting</span></span> | <span data-ttu-id="fe0e0-121">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="fe0e0-121">Suggested value</span></span> | <span data-ttu-id="fe0e0-122">Descrição</span><span class="sxs-lookup"><span data-stu-id="fe0e0-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="fe0e0-123">**Caminho**</span><span class="sxs-lookup"><span data-stu-id="fe0e0-123">**Path**</span></span>   | <span data-ttu-id="fe0e0-124">mycontainer/{name}</span><span class="sxs-lookup"><span data-stu-id="fe0e0-124">mycontainer/{name}</span></span>    | <span data-ttu-id="fe0e0-125">Local no Armazenamento de Blobs que está sendo monitorada.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-125">Location in Blob storage being monitored.</span></span> <span data-ttu-id="fe0e0-126">O nome do arquivo do blob é passado na associação como o parâmetro _name_.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-126">The file name of the blob is passed in the binding as the _name_ parameter.</span></span>  |
    | <span data-ttu-id="fe0e0-127">**Conexão da conta de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="fe0e0-127">**Storage account connection**</span></span> | <span data-ttu-id="fe0e0-128">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="fe0e0-128">AzureWebJobStorage</span></span> | <span data-ttu-id="fe0e0-129">Você pode usar a conexão da conta de armazenamento que já está sendo usada por seu aplicativo de funções ou criar uma nova.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-129">You can use the storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="fe0e0-130">**Nomeie sua função**</span><span class="sxs-lookup"><span data-stu-id="fe0e0-130">**Name your function**</span></span> | <span data-ttu-id="fe0e0-131">Exclusivo no aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="fe0e0-131">Unique in your function app</span></span> | <span data-ttu-id="fe0e0-132">O nome dessa função disparada pelo blob.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-132">Name of this blob triggered function.</span></span> |

3. <span data-ttu-id="fe0e0-133">Clique em **Criar** para criar a função.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-133">Click **Create** to create your function.</span></span>

<span data-ttu-id="fe0e0-134">Em seguida, você pode se conectar à sua conta de armazenamento do Azure e criar o contêiner **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-134">Next, you connect to your Azure Storage account and create the **mycontainer** container.</span></span>

## <a name="create-the-container"></a><span data-ttu-id="fe0e0-135">Criar o contêiner</span><span class="sxs-lookup"><span data-stu-id="fe0e0-135">Create the container</span></span>

1. <span data-ttu-id="fe0e0-136">Em sua função, clique em **Integrar**, expanda **Documentação**e copie **Nome da conta** e **Chave de conta**.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-136">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="fe0e0-137">Você usa essas credenciais para conectar-se à conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-137">You use these credentials to connect to the storage account.</span></span> <span data-ttu-id="fe0e0-138">Se você já tiver se conectado à conta de armazenamento, vá para a etapa 4.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-138">If you have already connected your storage account, skip to step 4.</span></span>

    ![Obtenha as credenciais de conexão da conta de armazenamento.](./media/functions-create-storage-blob-triggered-function/functions-storage-account-connection.png)

1. <span data-ttu-id="fe0e0-140">Execute a ferramenta [Gerenciador de Armazenamento do Microsoft Azure](http://storageexplorer.com/), clique no ícone conectar-se à esquerda, escolha **Usar um nome e chave de conta de armazenamento** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-140">Run the [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click the connect icon on the left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Execute a ferramenta Gerenciador de Conta de Armazenamento.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="fe0e0-142">Insira o **Nome da conta** e **Chave de conta** da etapa 1, clique em **Avançar** e em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-142">Enter the **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span> 

    ![Insira as credenciais de armazenamento e conecte-se.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="fe0e0-144">Expanda a conta de armazenamento anexada, clique com o botão direito do mouse em **Contêineres de blob**, clique em **Criar contêiner de blob**, digite `mycontainer` e pressione enter.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-144">Expand the attached storage account, right-click **Blob containers**, click **Create blob container**, type `mycontainer`, and then press enter.</span></span>

    ![Crie uma fila de armazenamento.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-create-blob-container.png)

<span data-ttu-id="fe0e0-146">Agora que você tem um contêiner de blob, você pode testar a função carregando um arquivo para o contêiner.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-146">Now that you have a blob container, you can test the function by uploading a file to the container.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="fe0e0-147">Testar a função</span><span class="sxs-lookup"><span data-stu-id="fe0e0-147">Test the function</span></span>

1. <span data-ttu-id="fe0e0-148">De volta ao Portal do Azure, navegue até sua função, expanda os **Logs** na parte inferior da página e verifique se o streaming de log não está em pausa.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-148">Back in the Azure portal, browse to your function expand the **Logs** at the bottom of the page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="fe0e0-149">No Gerenciador de Armazenamento, expanda sua conta de armazenamento, **Contêineres de blob** e **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-149">In Storage Explorer, expand your storage account, **Blob containers**, and **mycontainer**.</span></span> <span data-ttu-id="fe0e0-150">Clique em **Carregar** e depois em **Carregar arquivos...**.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-150">Click **Upload** and then **Upload files...**.</span></span>

    ![Carregue um arquivo para o contêiner de blob.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-upload-file-blob.png)

1. <span data-ttu-id="fe0e0-152">Na caixa de diálogo **Carregar arquivos**, clique no campo **Arquivos**.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-152">In the **Upload files** dialog box, click the **Files** field.</span></span> <span data-ttu-id="fe0e0-153">Navegue até um arquivo em seu computador local, por exemplo, um arquivo de imagem, selecione-o e clique em **Abrir** e depois em **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-153">Browse to a file on your local computer, such as an image file, select it and click **Open** and then **Upload**.</span></span>

1. <span data-ttu-id="fe0e0-154">Volte para os logs de função e verifique se o blob foi lido.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-154">Go back to your function logs and verify that the blob has been read.</span></span>

   ![Exiba a mensagem nos logs.](./media/functions-create-storage-blob-triggered-function/functions-blob-storage-trigger-view-logs.png)

    >[!NOTE]
    > <span data-ttu-id="fe0e0-156">Quando seu aplicativo de funções é executado no plano de consumo padrão, pode haver um atraso de até vários minutos entre o blob que está sendo adicionado ou atualizado e a função sendo disparada.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-156">When your function app runs in the default Consumption plan, there may be a delay of up to several minutes between the blob being added or updated and the function being triggered.</span></span> <span data-ttu-id="fe0e0-157">Se você precisar de baixa latência em suas funções disparadas por blob, considere executar seu aplicativo de funções em um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-157">If you need low latency in your blob triggered functions, consider running your function app in an App Service plan.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="fe0e0-158">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="fe0e0-158">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="fe0e0-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fe0e0-159">Next steps</span></span>

<span data-ttu-id="fe0e0-160">Você criou uma função que é executada quando um blob é adicionado a um Armazenamento de Blobs ou atualizado nele.</span><span class="sxs-lookup"><span data-stu-id="fe0e0-160">You have created a function that runs when a blob is added to or updated in Blob storage.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="fe0e0-161">Para obter mais informações sobre gatilhos de armazenamento de blobs, consulte [Associações de Armazenamento de Blobs do Azure Functions](functions-bindings-storage-blob.md).</span><span class="sxs-lookup"><span data-stu-id="fe0e0-161">For more information about Blob storage triggers, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md).</span></span>
