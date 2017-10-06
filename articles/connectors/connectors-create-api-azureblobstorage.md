---
title: "Olá aaaAdd Connector em seus aplicativos de lógica de armazenamento de BLOBs do Azure | Microsoft Docs"
description: "Comece a usar e configurar o conector de armazenamento de BLOBs do Azure Olá em um aplicativo de lógica"
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
ms.openlocfilehash: add61287ef1b2228ef9d3f54ce082807bad6858b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-blob-storage-connector-in-a-logic-app"></a><span data-ttu-id="f851d-103">Usar o conector de armazenamento de BLOBs do Azure Olá em um aplicativo de lógica</span><span class="sxs-lookup"><span data-stu-id="f851d-103">Use hello Azure blob storage connector in a logic app</span></span>
<span data-ttu-id="f851d-104">Tooupload de conector do armazenamento de BLOBs do Azure de Olá usar, atualizar, obter e excluir blobs na conta de armazenamento, tudo dentro de um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="f851d-104">Use hello Azure Blob storage connector tooupload, update, get, and delete blobs in your storage account, all within a logic app.</span></span>  

<span data-ttu-id="f851d-105">Com o armazenamento de blobs do Azure, você:</span><span class="sxs-lookup"><span data-stu-id="f851d-105">With Azure blob storage, you:</span></span>

* <span data-ttu-id="f851d-106">Crie seu fluxo de trabalho carregando novos projetos ou obtendo arquivos que foram atualizados recentemente.</span><span class="sxs-lookup"><span data-stu-id="f851d-106">Build your workflow by uploading new projects, or getting files that have been recently updated.</span></span>
* <span data-ttu-id="f851d-107">Use ações tooget metadados de arquivo, excluir um arquivo, copiar os arquivos e muito mais.</span><span class="sxs-lookup"><span data-stu-id="f851d-107">Use actions tooget file metadata, delete a file, copy files, and more.</span></span> <span data-ttu-id="f851d-108">Por exemplo, quando uma ferramenta é atualizada em um site do Azure (um gatilho), em seguida, um arquivo é atualizado no armazenamento de blobs (uma ação).</span><span class="sxs-lookup"><span data-stu-id="f851d-108">For example, when a tool is updated in an Azure web site (a trigger), then update a file in blob storage (an action).</span></span> 

<span data-ttu-id="f851d-109">Este tópico mostra como toouse Olá blob conector de armazenamento em um aplicativo de lógica.</span><span class="sxs-lookup"><span data-stu-id="f851d-109">This topic shows you how toouse hello blob storage connector in a logic app.</span></span>

<span data-ttu-id="f851d-110">toolearn mais sobre aplicativos lógicos, consulte [quais são os aplicativos lógicos](../logic-apps/logic-apps-what-are-logic-apps.md) e [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f851d-110">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<span data-ttu-id="f851d-111">toolearn mais sobre aplicativos lógicos, consulte [quais são os aplicativos lógicos](../logic-apps/logic-apps-what-are-logic-apps.md) e [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f851d-111">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooazure-blob-storage"></a><span data-ttu-id="f851d-112">Conectar o armazenamento de blob tooAzure</span><span class="sxs-lookup"><span data-stu-id="f851d-112">Connect tooAzure blob storage</span></span>
<span data-ttu-id="f851d-113">Antes de sua lógica de aplicativo pode acessar qualquer serviço, você primeiro crie um *conexão* toohello service.</span><span class="sxs-lookup"><span data-stu-id="f851d-113">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="f851d-114">Uma conexão fornece uma conectividade entre um aplicativo lógico e outro serviço.</span><span class="sxs-lookup"><span data-stu-id="f851d-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="f851d-115">Por exemplo, conta de armazenamento do tooconnect tooa, você primeiro crie um armazenamento de blob *conexão*.</span><span class="sxs-lookup"><span data-stu-id="f851d-115">For example, tooconnect tooa storage account, you first create a blob storage *connection*.</span></span> <span data-ttu-id="f851d-116">toocreate uma conexão, insira as credenciais de saudação você normalmente usa o serviço de saudação tooaccess você está se conectando.</span><span class="sxs-lookup"><span data-stu-id="f851d-116">toocreate a connection, enter hello credentials you normally use tooaccess hello service you are connecting to.</span></span> <span data-ttu-id="f851d-117">Portanto, com o armazenamento do Azure, insira conexão de saudação do hello credenciais tooyour armazenamento conta toocreate.</span><span class="sxs-lookup"><span data-stu-id="f851d-117">So with Azure storage, enter hello credentials tooyour storage account toocreate hello connection.</span></span> 

#### <a name="create-hello-connection"></a><span data-ttu-id="f851d-118">Criar conexão Olá</span><span class="sxs-lookup"><span data-stu-id="f851d-118">Create hello connection</span></span>
> [!INCLUDE [Create a connection tooAzure blob storage](../../includes/connectors-create-api-azureblobstorage.md)]

## <a name="use-a-trigger"></a><span data-ttu-id="f851d-119">Usar um gatilho</span><span class="sxs-lookup"><span data-stu-id="f851d-119">Use a trigger</span></span>
<span data-ttu-id="f851d-120">Esse conector não tem gatilhos.</span><span class="sxs-lookup"><span data-stu-id="f851d-120">This connector does not have any triggers.</span></span> <span data-ttu-id="f851d-121">Use outros gatilhos toostart Olá lógica aplicativo, como um disparador de recorrência, um gatilho de HTTP Webhook, disparadores disponíveis com outros conectores e muito mais.</span><span class="sxs-lookup"><span data-stu-id="f851d-121">Use other triggers toostart hello logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="f851d-122">[Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md) fornece um exemplo.</span><span class="sxs-lookup"><span data-stu-id="f851d-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="f851d-123">Usar uma ação</span><span class="sxs-lookup"><span data-stu-id="f851d-123">Use an action</span></span>
<span data-ttu-id="f851d-124">Uma ação é uma operação executada pelo fluxo de trabalho Olá definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="f851d-124">An action is an operation carried out by hello workflow defined in a logic app.</span></span>

1. <span data-ttu-id="f851d-125">Selecione o sinal de adição hello.</span><span class="sxs-lookup"><span data-stu-id="f851d-125">Select hello plus sign.</span></span> <span data-ttu-id="f851d-126">Consulte várias opções: **adicionar uma ação**, **adicionar uma condição**, ou uma saudação **mais** opções.</span><span class="sxs-lookup"><span data-stu-id="f851d-126">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/add-action.png)
2. <span data-ttu-id="f851d-127">Escolha **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="f851d-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="f851d-128">Na caixa de texto de saudação, digite "blob" tooget uma lista de todas as ações disponíveis de saudação.</span><span class="sxs-lookup"><span data-stu-id="f851d-128">In hello text box, type “blob” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/actions.png) 
4. <span data-ttu-id="f851d-129">Em nosso exemplo, escolha **AzureBlob – Obter metadados do arquivo usando o caminho**.</span><span class="sxs-lookup"><span data-stu-id="f851d-129">In our example, choose **AzureBlob - Get file metadata using path**.</span></span> <span data-ttu-id="f851d-130">Se uma conexão já existir, selecione Olá **...** (Mostrar seletor) botão tooselect um arquivo.</span><span class="sxs-lookup"><span data-stu-id="f851d-130">If a connection already exists, then select hello **...** (Show Picker) button tooselect a file.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/sample-file.png)
   
    <span data-ttu-id="f851d-131">Se você for solicitado para obter informações de conexão do hello, digite conexão de Olá Olá detalhes toocreate.</span><span class="sxs-lookup"><span data-stu-id="f851d-131">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="f851d-132">[Criar conexão Olá](connectors-create-api-azureblobstorage.md#create-the-connection) neste tópico descreve essas propriedades.</span><span class="sxs-lookup"><span data-stu-id="f851d-132">[Create hello connection](connectors-create-api-azureblobstorage.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="f851d-133">Neste exemplo, obtemos Olá metadados de um arquivo.</span><span class="sxs-lookup"><span data-stu-id="f851d-133">In this example, we get hello metadata of a file.</span></span> <span data-ttu-id="f851d-134">toosee Olá metadados, adicione outra ação que cria um novo arquivo usando outro conector.</span><span class="sxs-lookup"><span data-stu-id="f851d-134">toosee hello metadata, add another action that creates a new file using another connector.</span></span> <span data-ttu-id="f851d-135">Por exemplo, adicione uma ação de OneDrive que cria um novo arquivo de "teste" com base nos metadados de saudação.</span><span class="sxs-lookup"><span data-stu-id="f851d-135">For example, add a OneDrive action that creates a new "test" file based on hello metadata.</span></span> 


5. <span data-ttu-id="f851d-136">**Salvar** as alterações (canto superior esquerdo da barra de ferramentas de saudação).</span><span class="sxs-lookup"><span data-stu-id="f851d-136">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="f851d-137">Seu aplicativo lógico é salvo e pode ser habilitado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f851d-137">Your logic app is saved and may be automatically enabled.</span></span>

> [!TIP]
> <span data-ttu-id="f851d-138">[Gerenciador de armazenamento](http://storageexplorer.com/) é uma excelente ferramenta muito gerenciar várias contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f851d-138">[Storage Explorer](http://storageexplorer.com/) is a great tool too manage multiple storage accounts.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="f851d-139">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="f851d-139">Connector-specific details</span></span>

<span data-ttu-id="f851d-140">Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/azureblobconnector/).</span><span class="sxs-lookup"><span data-stu-id="f851d-140">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/azureblobconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f851d-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f851d-141">Next steps</span></span>
<span data-ttu-id="f851d-142">[Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f851d-142">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="f851d-143">Explorar Olá outros conectores disponíveis na lógica de aplicativos no nosso [lista APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="f851d-143">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

