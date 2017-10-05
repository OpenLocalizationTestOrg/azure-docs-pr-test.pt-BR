---
title: Criar um hub de eventos do Azure | Microsoft Docs
description: Criar um namespace de Hubs de Eventos do Azure e um hub de eventos usando o Portal do Azure
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: ff99e327-c8db-4354-9040-9c60c51a2191
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: sethm
ms.openlocfilehash: 816bf1426704d3391550e80c0700f1b011683a94
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-the-azure-portal"></a><span data-ttu-id="5bc91-103">Criar um namespace de Hubs de Eventos e um hub de eventos usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5bc91-103">Create an Event Hubs namespace and an event hub using the Azure portal</span></span>

## <a name="create-an-event-hubs-namespace"></a><span data-ttu-id="5bc91-104">Criar um namespace de Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="5bc91-104">Create an Event Hubs namespace</span></span>
1. <span data-ttu-id="5bc91-105">Faça logon no [portal do Azure][Azure portal] e clique em **Novo** na parte superior esquerda da tela.</span><span class="sxs-lookup"><span data-stu-id="5bc91-105">Log on to the [Azure portal][Azure portal], and click **New** at the top left of the screen.</span></span>
1. <span data-ttu-id="5bc91-106">Clique em **Internet das Coisas** e, em seguida, clique em **Hubs de Eventos**.</span><span class="sxs-lookup"><span data-stu-id="5bc91-106">Click **Internet of Things**, and then click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub9.png)
1. <span data-ttu-id="5bc91-107">Na folha **Criar um namespace** , insira um nome de namespace.</span><span class="sxs-lookup"><span data-stu-id="5bc91-107">In the **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="5bc91-108">O sistema imediatamente verifica para ver se o nome está disponível.</span><span class="sxs-lookup"><span data-stu-id="5bc91-108">The system immediately checks to see if the name is available.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub1.png)
1. <span data-ttu-id="5bc91-109">Depois de verificar se o nome do namespace está disponível, escolha o tipo de preço (Básico ou Standard).</span><span class="sxs-lookup"><span data-stu-id="5bc91-109">After making sure the namespace name is available, choose the pricing tier (Basic or Standard).</span></span> <span data-ttu-id="5bc91-110">Além disso, escolha uma assinatura do Azure, o grupo de recursos e o local no qual o recurso será criado.</span><span class="sxs-lookup"><span data-stu-id="5bc91-110">Also, choose an Azure subscription, resource group, and location in which to create the resource.</span></span> 
1. <span data-ttu-id="5bc91-111">Clique em **Criar** para criar o namespace.</span><span class="sxs-lookup"><span data-stu-id="5bc91-111">Click **Create** to create the namespace.</span></span> <span data-ttu-id="5bc91-112">Talvez você precise aguardar alguns minutos para o sistema provisionar totalmente os recursos.</span><span class="sxs-lookup"><span data-stu-id="5bc91-112">You may have to wait a few minutes for the system to fully provision the resources.</span></span>
2. <span data-ttu-id="5bc91-113">Na lista de namespaces do portal, clique no namespace recém-criado.</span><span class="sxs-lookup"><span data-stu-id="5bc91-113">In the portal list of namespaces, click the newly created namespace.</span></span>
2. <span data-ttu-id="5bc91-114">Clique em **Políticas de acesso compartilhado** e, em seguida, clique em **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="5bc91-114">Click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub7.png)

3. <span data-ttu-id="5bc91-115">Clique no botão de cópia para copiar a cadeia de conexão **RootManageSharedAccessKey** na área de transferência.</span><span class="sxs-lookup"><span data-stu-id="5bc91-115">Click the copy button to copy the **RootManageSharedAccessKey** connection string to the clipboard.</span></span> <span data-ttu-id="5bc91-116">Salve esta cadeia de conexão em um local temporário, como o Bloco de Notas, para uso futuro.</span><span class="sxs-lookup"><span data-stu-id="5bc91-116">Save this connection string in a temporary location, such as Notepad, to use later.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub8.png)

## <a name="create-an-event-hub"></a><span data-ttu-id="5bc91-117">Criar um Hub de Evento</span><span class="sxs-lookup"><span data-stu-id="5bc91-117">Create an event hub</span></span>

1. <span data-ttu-id="5bc91-118">Na lista de namespaces dos Hubs de Eventos, clique no namespace recém-criado.</span><span class="sxs-lookup"><span data-stu-id="5bc91-118">In the Event Hubs namespace list, click the newly created namespace.</span></span>      
   
    ![](./media/event-hubs-create/create-event-hub2.png) 

2. <span data-ttu-id="5bc91-119">Na folha do namespace, clique em **Hubs de Eventos**.</span><span class="sxs-lookup"><span data-stu-id="5bc91-119">In the namespace blade, click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub3.png)

1. <span data-ttu-id="5bc91-120">Na parte superior da folha, clique em **Adicionar Hub de Eventos**.</span><span class="sxs-lookup"><span data-stu-id="5bc91-120">At the top of the blade, click **Add Event Hub**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub4.png)
1. <span data-ttu-id="5bc91-121">Digite um nome para seu hub de eventos e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5bc91-121">Type a name for your event hub, then click **Create**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub5.png)

<span data-ttu-id="5bc91-122">Seu hub de eventos foi criado, e você tem as cadeias de conexão que precisa para enviar e receber eventos.</span><span class="sxs-lookup"><span data-stu-id="5bc91-122">Your event hub is now created, and you have the connection strings you need to send and receive events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5bc91-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5bc91-123">Next steps</span></span>
<span data-ttu-id="5bc91-124">Para saber mais sobre os Hubs de Eventos, consulte estes links:</span><span class="sxs-lookup"><span data-stu-id="5bc91-124">To learn more about Event Hubs, visit these links:</span></span>

* [<span data-ttu-id="5bc91-125">Visão Geral dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="5bc91-125">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="5bc91-126">Visão geral de API de Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="5bc91-126">Event Hubs API overview</span></span>](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/