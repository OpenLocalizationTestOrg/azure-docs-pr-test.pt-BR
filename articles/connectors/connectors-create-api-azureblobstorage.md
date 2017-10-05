---
title: "Adicionar o Conector do armazenamento de blobs do Azure a seus Aplicativos Lógicos | Microsoft Docs"
description: "Introdução e configuração do conector do armazenamento de blobs do Azure em um aplicativo lógico"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b5dc3f75-6bea-420b-b250-183668d2848d
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/02/2017
ms.author: mandia; ladocs
ms.openlocfilehash: bc7908868828bd1628633cf9e57f8c44f8000827
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-azure-blob-storage-connector-in-a-logic-app"></a><span data-ttu-id="004f1-103">Usar o conector do armazenamento de blobs do Azure em um aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="004f1-103">Use the Azure blob storage connector in a logic app</span></span>
<span data-ttu-id="004f1-104">Use o conector do armazenamento de Blobs do Azure para carregar, atualizar, obter e excluir blobs de sua conta de armazenamento, tudo em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="004f1-104">Use the Azure Blob storage connector to upload, update, get, and delete blobs in your storage account, all within a logic app.</span></span>  

<span data-ttu-id="004f1-105">Com o armazenamento de blobs do Azure, você:</span><span class="sxs-lookup"><span data-stu-id="004f1-105">With Azure blob storage, you:</span></span>

* <span data-ttu-id="004f1-106">Crie seu fluxo de trabalho carregando novos projetos ou obtendo arquivos que foram atualizados recentemente.</span><span class="sxs-lookup"><span data-stu-id="004f1-106">Build your workflow by uploading new projects, or getting files that have been recently updated.</span></span>
* <span data-ttu-id="004f1-107">Use as ações para obter metadados do arquivo, excluir um arquivo, copiar arquivos e muito mais.</span><span class="sxs-lookup"><span data-stu-id="004f1-107">Use actions to get file metadata, delete a file, copy files, and more.</span></span> <span data-ttu-id="004f1-108">Por exemplo, quando uma ferramenta é atualizada em um site do Azure (um gatilho), em seguida, um arquivo é atualizado no armazenamento de blobs (uma ação).</span><span class="sxs-lookup"><span data-stu-id="004f1-108">For example, when a tool is updated in an Azure web site (a trigger), then update a file in blob storage (an action).</span></span> 

<span data-ttu-id="004f1-109">Este tópico mostra como usar o conector do armazenamento de blobs em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="004f1-109">This topic shows you how to use the blob storage connector in a logic app.</span></span>

<span data-ttu-id="004f1-110">Para saber mais sobre os Aplicativos Lógicos, consulte [O que são aplicativos lógicos](../logic-apps/logic-apps-what-are-logic-apps.md) e [Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="004f1-110">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<span data-ttu-id="004f1-111">Para saber mais sobre os Aplicativos Lógicos, consulte [O que são aplicativos lógicos](../logic-apps/logic-apps-what-are-logic-apps.md) e [Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="004f1-111">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-azure-blob-storage"></a><span data-ttu-id="004f1-112">Conectar o armazenamento de blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="004f1-112">Connect to Azure blob storage</span></span>
<span data-ttu-id="004f1-113">Antes do aplicativo lógico poder acessar qualquer serviço, primeiro crie uma *conexão* com o serviço.</span><span class="sxs-lookup"><span data-stu-id="004f1-113">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="004f1-114">Uma conexão fornece uma conectividade entre um aplicativo lógico e outro serviço.</span><span class="sxs-lookup"><span data-stu-id="004f1-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="004f1-115">Por exemplo, para se conectar a uma conta de armazenamento, você primeiro cria uma *conexão* de armazenamento de blobs.</span><span class="sxs-lookup"><span data-stu-id="004f1-115">For example, to connect to a storage account, you first create a blob storage *connection*.</span></span> <span data-ttu-id="004f1-116">Para criar uma conexão, insira as credenciais que você normalmente usa para acessar o serviço ao qual está se conectando.</span><span class="sxs-lookup"><span data-stu-id="004f1-116">To create a connection, enter the credentials you normally use to access the service you are connecting to.</span></span> <span data-ttu-id="004f1-117">Assim, com o armazenamento do Azure, insira as credenciais de sua conta de armazenamento para criar a conexão.</span><span class="sxs-lookup"><span data-stu-id="004f1-117">So with Azure storage, enter the credentials to your storage account to create the connection.</span></span> 

#### <a name="create-the-connection"></a><span data-ttu-id="004f1-118">Criar a conexão</span><span class="sxs-lookup"><span data-stu-id="004f1-118">Create the connection</span></span>
> [!INCLUDE [Create a connection to Azure blob storage](../../includes/connectors-create-api-azureblobstorage.md)]

## <a name="use-a-trigger"></a><span data-ttu-id="004f1-119">Usar um gatilho</span><span class="sxs-lookup"><span data-stu-id="004f1-119">Use a trigger</span></span>
<span data-ttu-id="004f1-120">Esse conector não tem gatilhos.</span><span class="sxs-lookup"><span data-stu-id="004f1-120">This connector does not have any triggers.</span></span> <span data-ttu-id="004f1-121">Use outros gatilhos para iniciar o aplicativo lógico, como um gatilho de Recorrência, um gatilho de Webhook HTTP, gatilhos disponíveis com outros conectores e muito mais.</span><span class="sxs-lookup"><span data-stu-id="004f1-121">Use other triggers to start the logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="004f1-122">[Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md) fornece um exemplo.</span><span class="sxs-lookup"><span data-stu-id="004f1-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="004f1-123">Usar uma ação</span><span class="sxs-lookup"><span data-stu-id="004f1-123">Use an action</span></span>
<span data-ttu-id="004f1-124">Uma ação é uma operação executada pelo fluxo de trabalho definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="004f1-124">An action is an operation carried out by the workflow defined in a logic app.</span></span>

1. <span data-ttu-id="004f1-125">Selecione o sinal de mais.</span><span class="sxs-lookup"><span data-stu-id="004f1-125">Select the plus sign.</span></span> <span data-ttu-id="004f1-126">Você tem várias opções: **adicionar uma ação**, **adicionar uma condição** ou uma das opções **Mais**.</span><span class="sxs-lookup"><span data-stu-id="004f1-126">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/add-action.png)
2. <span data-ttu-id="004f1-127">Escolha **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="004f1-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="004f1-128">Na caixa de texto, digite "blob" para obter uma lista de todas as ações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="004f1-128">In the text box, type “blob” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/actions.png) 
4. <span data-ttu-id="004f1-129">Em nosso exemplo, escolha **AzureBlob – Obter metadados do arquivo usando o caminho**.</span><span class="sxs-lookup"><span data-stu-id="004f1-129">In our example, choose **AzureBlob - Get file metadata using path**.</span></span> <span data-ttu-id="004f1-130">Se já existir uma conexão, selecione **...** Botão (Mostrar Seletor) para selecionar um arquivo.</span><span class="sxs-lookup"><span data-stu-id="004f1-130">If a connection already exists, then select the **...** (Show Picker) button to select a file.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/sample-file.png)
   
    <span data-ttu-id="004f1-131">Se as informações de conexão forem solicitadas, insira os detalhes para criar a conexão.</span><span class="sxs-lookup"><span data-stu-id="004f1-131">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="004f1-132">[Criar a conexão](connectors-create-api-azureblobstorage.md#create-the-connection) neste tópico descreve estas propriedades.</span><span class="sxs-lookup"><span data-stu-id="004f1-132">[Create the connection](connectors-create-api-azureblobstorage.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="004f1-133">Neste exemplo, obtemos os metadados de um arquivo.</span><span class="sxs-lookup"><span data-stu-id="004f1-133">In this example, we get the metadata of a file.</span></span> <span data-ttu-id="004f1-134">Para ver os metadados, adicione outra ação que cria um novo arquivo usando outro conector.</span><span class="sxs-lookup"><span data-stu-id="004f1-134">To see the metadata, add another action that creates a new file using another connector.</span></span> <span data-ttu-id="004f1-135">Por exemplo, adicione uma ação do OneDrive que cria um novo arquivo de "teste" com base nos metadados.</span><span class="sxs-lookup"><span data-stu-id="004f1-135">For example, add a OneDrive action that creates a new "test" file based on the metadata.</span></span> 


5. <span data-ttu-id="004f1-136">**Salve** as alterações (canto superior esquerdo da barra de ferramentas).</span><span class="sxs-lookup"><span data-stu-id="004f1-136">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="004f1-137">Seu aplicativo lógico é salvo e pode ser habilitado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="004f1-137">Your logic app is saved and may be automatically enabled.</span></span>

> [!TIP]
> <span data-ttu-id="004f1-138">O [Gerenciador de Armazenamento](http://storageexplorer.com/) é uma excelente ferramenta para gerenciar várias contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="004f1-138">[Storage Explorer](http://storageexplorer.com/) is a great tool to  manage multiple storage accounts.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="004f1-139">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="004f1-139">Connector-specific details</span></span>

<span data-ttu-id="004f1-140">Exiba os gatilhos e ações definidos no swagger e também os limites nos [detalhes do conector](/connectors/azureblobconnector/).</span><span class="sxs-lookup"><span data-stu-id="004f1-140">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/azureblobconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="004f1-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="004f1-141">Next steps</span></span>
<span data-ttu-id="004f1-142">[Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="004f1-142">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="004f1-143">Explore os outros conectores disponíveis nos Aplicativos Lógicos em nossa [lista de APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="004f1-143">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

