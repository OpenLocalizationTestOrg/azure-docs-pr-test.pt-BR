---
title: aaaCreate um hub de eventos do Azure | Microsoft Docs
description: "Criar um namespace de Hubs de eventos do Azure e um hub de eventos usando Olá portal do Azure"
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
ms.openlocfilehash: 9a8b7711e2ca7d112e24be19353d43c365ff6935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-hello-azure-portal"></a><span data-ttu-id="25893-103">Criar um namespace de Hubs de eventos e um hub de eventos usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="25893-103">Create an Event Hubs namespace and an event hub using hello Azure portal</span></span>

## <a name="create-an-event-hubs-namespace"></a><span data-ttu-id="25893-104">Criar um namespace de Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="25893-104">Create an Event Hubs namespace</span></span>
1. <span data-ttu-id="25893-105">Faça logon no toohello [portal do Azure][Azure portal]e clique em **novo** em Olá superior esquerda da tela hello.</span><span class="sxs-lookup"><span data-stu-id="25893-105">Log on toohello [Azure portal][Azure portal], and click **New** at hello top left of hello screen.</span></span>
1. <span data-ttu-id="25893-106">Clique em **Internet das Coisas** e, em seguida, clique em **Hubs de Eventos**.</span><span class="sxs-lookup"><span data-stu-id="25893-106">Click **Internet of Things**, and then click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub9.png)
1. <span data-ttu-id="25893-107">Em Olá **criar namespace** folha, insira um nome de namespace.</span><span class="sxs-lookup"><span data-stu-id="25893-107">In hello **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="25893-108">sistema de saudação imediatamente verifica toosee se Olá nome está disponível.</span><span class="sxs-lookup"><span data-stu-id="25893-108">hello system immediately checks toosee if hello name is available.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub1.png)
1. <span data-ttu-id="25893-109">Depois de fazer o nome do namespace Olá-se de que está disponível, escolha Olá preço (básico ou padrão).</span><span class="sxs-lookup"><span data-stu-id="25893-109">After making sure hello namespace name is available, choose hello pricing tier (Basic or Standard).</span></span> <span data-ttu-id="25893-110">Além disso, escolha uma assinatura do Azure, o grupo de recursos e o local no qual recurso de saudação toocreate.</span><span class="sxs-lookup"><span data-stu-id="25893-110">Also, choose an Azure subscription, resource group, and location in which toocreate hello resource.</span></span> 
1. <span data-ttu-id="25893-111">Clique em **criar** toocreate Olá namespace.</span><span class="sxs-lookup"><span data-stu-id="25893-111">Click **Create** toocreate hello namespace.</span></span> <span data-ttu-id="25893-112">Você pode ter toowait alguns minutos Olá toofully provisionar Olá para recursos do sistema.</span><span class="sxs-lookup"><span data-stu-id="25893-112">You may have toowait a few minutes for hello system toofully provision hello resources.</span></span>
2. <span data-ttu-id="25893-113">Na lista de portal de saudação de namespaces, clique Olá recém-criado namespace.</span><span class="sxs-lookup"><span data-stu-id="25893-113">In hello portal list of namespaces, click hello newly created namespace.</span></span>
2. <span data-ttu-id="25893-114">Clique em **Políticas de acesso compartilhado** e, em seguida, clique em **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="25893-114">Click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub7.png)

3. <span data-ttu-id="25893-115">Clique em Olá Olá de toocopy do botão de cópia **RootManageSharedAccessKey** transferência de toohello de cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="25893-115">Click hello copy button toocopy hello **RootManageSharedAccessKey** connection string toohello clipboard.</span></span> <span data-ttu-id="25893-116">Salve esta cadeia de caracteres de conexão em um local temporário, como o bloco de notas, toouse mais tarde.</span><span class="sxs-lookup"><span data-stu-id="25893-116">Save this connection string in a temporary location, such as Notepad, toouse later.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub8.png)

## <a name="create-an-event-hub"></a><span data-ttu-id="25893-117">Criar um Hub de Evento</span><span class="sxs-lookup"><span data-stu-id="25893-117">Create an event hub</span></span>

1. <span data-ttu-id="25893-118">Na lista de namespace de Hubs de eventos Olá, clique em namespace Olá recém-criado.</span><span class="sxs-lookup"><span data-stu-id="25893-118">In hello Event Hubs namespace list, click hello newly created namespace.</span></span>      
   
    ![](./media/event-hubs-create/create-event-hub2.png) 

2. <span data-ttu-id="25893-119">Na folha de namespace hello, clique em **Hubs de eventos**.</span><span class="sxs-lookup"><span data-stu-id="25893-119">In hello namespace blade, click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub3.png)

1. <span data-ttu-id="25893-120">Na parte superior de saudação da folha de saudação, clique em **adicionar Hub de eventos**.</span><span class="sxs-lookup"><span data-stu-id="25893-120">At hello top of hello blade, click **Add Event Hub**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub4.png)
1. <span data-ttu-id="25893-121">Digite um nome para seu hub de eventos e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="25893-121">Type a name for your event hub, then click **Create**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub5.png)

<span data-ttu-id="25893-122">O hub de eventos é criado, e você tem Olá cadeias de conexão necessárias toosend e receber eventos.</span><span class="sxs-lookup"><span data-stu-id="25893-122">Your event hub is now created, and you have hello connection strings you need toosend and receive events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25893-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="25893-123">Next steps</span></span>
<span data-ttu-id="25893-124">toolearn mais sobre Hubs de eventos, consulte estes links:</span><span class="sxs-lookup"><span data-stu-id="25893-124">toolearn more about Event Hubs, visit these links:</span></span>

* [<span data-ttu-id="25893-125">Visão Geral dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="25893-125">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="25893-126">Visão geral de API de Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="25893-126">Event Hubs API overview</span></span>](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/