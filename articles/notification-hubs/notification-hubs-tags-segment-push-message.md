---
title: "Expressões de marca e roteamento"
description: "Este tópico explica as expressões de marca e roteamento para hubs de notificação do Azure."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: 0fffb3bb-8ed8-4e0f-89e8-0de24a47f644
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 18faa88641623e1248d6a33bc2d87099e1c9f624
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="routing-and-tag-expressions"></a><span data-ttu-id="45d73-103">Expressões de marca e roteamento</span><span class="sxs-lookup"><span data-stu-id="45d73-103">Routing and tag expressions</span></span>
## <a name="overview"></a><span data-ttu-id="45d73-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="45d73-104">Overview</span></span>
<span data-ttu-id="45d73-105">As expressões de marcas permitem que você direcione conjuntos específicos de dispositivos, ou mais especificamente, registros, ao enviar uma notificação por push por meio de Hubs de notificação.</span><span class="sxs-lookup"><span data-stu-id="45d73-105">Tag expressions enable you to target specific sets of devices, or more specifically registrations, when sending a push notification through Notification Hubs.</span></span>

## <a name="targeting-specific-registrations"></a><span data-ttu-id="45d73-106">Como direcionar registros específicos</span><span class="sxs-lookup"><span data-stu-id="45d73-106">Targeting specific registrations</span></span>
<span data-ttu-id="45d73-107">A única maneira de direcionar registros de notificações específicos é associar marcas a eles e, então, direcionar essas marcas.</span><span class="sxs-lookup"><span data-stu-id="45d73-107">The only way to target specific notification registrations is to associate tags with them, then target those tags.</span></span> <span data-ttu-id="45d73-108">Conforme discutido em [Gerenciamento de registro](notification-hubs-push-notification-registration-management.md), para receber notificações por push, um aplicativo precisa registrar um dispositivo em um hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="45d73-108">As discussed in [Registration Management](notification-hubs-push-notification-registration-management.md), in order to receive push notifications an app has to register a device handle on a notification hub.</span></span> <span data-ttu-id="45d73-109">Quando um registro é criado em um hub de notificação, o back-end do aplicativo pode enviar notificações por push para ele.</span><span class="sxs-lookup"><span data-stu-id="45d73-109">Once a registration is created on a notification hub, the application backend can send push notifications to it.</span></span>
<span data-ttu-id="45d73-110">O back-end do aplicativo pode escolher os registros para direcionar uma notificação específica das seguintes maneiras:</span><span class="sxs-lookup"><span data-stu-id="45d73-110">The application backend can choose the registrations to target with a specific notification in the following ways:</span></span>

1. <span data-ttu-id="45d73-111">**Difusão**: todos os registros no hub de notificação recebem a notificação.</span><span class="sxs-lookup"><span data-stu-id="45d73-111">**Broadcast**: all registrations in the notification hub receive the notification.</span></span>
2. <span data-ttu-id="45d73-112">**Marca**: todos os registros que contêm a marca especificada recebem a notificação.</span><span class="sxs-lookup"><span data-stu-id="45d73-112">**Tag**: all registrations that contain the specified tag receive the notification.</span></span>
3. <span data-ttu-id="45d73-113">**Expressão de marca**: todos os registros cujos conjuntos de marcas correspondem à expressão especificada recebem a notificação.</span><span class="sxs-lookup"><span data-stu-id="45d73-113">**Tag expression**: all registrations whose set of tags match the specified expression receive the notification.</span></span>

## <a name="tags"></a><span data-ttu-id="45d73-114">Marcas</span><span class="sxs-lookup"><span data-stu-id="45d73-114">Tags</span></span>
<span data-ttu-id="45d73-115">Uma marca pode ser qualquer cadeia de caracteres, até 120 caracteres que contenha caracteres alfanuméricos e os seguintes caracteres não alfanuméricos: '_', ' @', '#', '. ',':', '-'.</span><span class="sxs-lookup"><span data-stu-id="45d73-115">A tag can be any string, up to 120 characters, containing alphanumeric and the following non-alphanumeric characters: ‘_’, ‘@’, ‘#’, ‘.’, ‘:’, ‘-’.</span></span> <span data-ttu-id="45d73-116">O exemplo a seguir mostra um aplicativo do qual você pode receber notificações de aviso sobre grupos musicais específicos.</span><span class="sxs-lookup"><span data-stu-id="45d73-116">The following example shows an application from which you can receive toast notifications about specific music groups.</span></span> <span data-ttu-id="45d73-117">Nesse cenário, uma maneira simples de direcionar as notificações é rotular os registros com marcas que representem as diferentes bandas, como na seguinte imagem.</span><span class="sxs-lookup"><span data-stu-id="45d73-117">In this scenario, a simple way to route notifications is to label registrations with tags that represent the different bands, as in the following picture.</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags.png)

<span data-ttu-id="45d73-118">Nesta figura, a mensagem marcada como **Beatles** atinge somente o tablet que estiver registrado com a marca **Beatles**.</span><span class="sxs-lookup"><span data-stu-id="45d73-118">In this picture, the message tagged **Beatles** reaches only the tablet that registered with the tag **Beatles**.</span></span>

<span data-ttu-id="45d73-119">Para mais informações sobre a criação de registros para marcas, consulte [Gerenciamento de registro](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="45d73-119">For more information about creating registrations for tags, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

<span data-ttu-id="45d73-120">Você pode enviar notificações para marcas usando os métodos de notificações de envio da classe `Microsoft.Azure.NotificationHubs.NotificationHubClient` no SDK dos [Hubs de Notificação do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="45d73-120">You can send notifications to tags using the send notifications methods of the `Microsoft.Azure.NotificationHubs.NotificationHubClient` class in the [Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK.</span></span> <span data-ttu-id="45d73-121">Você também pode usar o Node. js ou as APIs de REST de notificações por push.</span><span class="sxs-lookup"><span data-stu-id="45d73-121">You can also use Node.js, or the Push Notifications REST APIs.</span></span>  <span data-ttu-id="45d73-122">Aqui está um exemplo usando o SDK.</span><span class="sxs-lookup"><span data-stu-id="45d73-122">Here's an example using the SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You requested a Beatles notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Beatles");

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You requested a Wailers notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Wailers");




<span data-ttu-id="45d73-123">As marcas não precisam ser pré-configuradas e podem se referir a vários conceitos específicos do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="45d73-123">Tags do not have to be pre-provisioned and can refer to multiple app-specific concepts.</span></span> <span data-ttu-id="45d73-124">Por exemplo, os usuários deste aplicativo de exemplo podem comentar sobre as bandas e desejar receber notificações do sistema, não apenas dos comentários sobre suas bandas favoritas, mas também de todos os comentários dos seus amigos, independentemente da banda sobre a qual eles estão comentando.</span><span class="sxs-lookup"><span data-stu-id="45d73-124">For example, users of this example application can comment on bands and want to receive toasts, not only for the comments on their favorite bands, but also for all comments from their friends, regardless of the band on which they are commenting.</span></span> <span data-ttu-id="45d73-125">A figura a seguir mostra um exemplo desse cenário:</span><span class="sxs-lookup"><span data-stu-id="45d73-125">The following picture shows an example of this scenario:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags2.png)

<span data-ttu-id="45d73-126">Nesta imagem, Alice está interessada em atualizações dos Beatles e Fábio está interessado em atualizações dos Wailers.</span><span class="sxs-lookup"><span data-stu-id="45d73-126">In this picture, Alice is interested in updates for the Beatles, and Bob is interested in updates for the Wailers.</span></span> <span data-ttu-id="45d73-127">Fábio também está interessado nos comentários de Carlos e Carlos está interessado nos Wailers.</span><span class="sxs-lookup"><span data-stu-id="45d73-127">Bob is also interested in Charlie’s comments, and Charlie is in interested in the Wailers.</span></span> <span data-ttu-id="45d73-128">Quando uma notificação é enviada para o comentário de Carlos sobre os Beatles, Alice e Fábio o recebem.</span><span class="sxs-lookup"><span data-stu-id="45d73-128">When a notification is sent for Charlie’s comment on the Beatles, both Alice and Bob receive it.</span></span>

<span data-ttu-id="45d73-129">Embora você possa codificar vários interesses em marcas (por exemplo, “band_Beatles” ou “follows_Charlie”), as marcas são sequências de caracteres simples e não propriedades com valores.</span><span class="sxs-lookup"><span data-stu-id="45d73-129">While you can encode multiple concerns in tags (for example, “band_Beatles” or “follows_Charlie”), tags are simple strings and not properties with values.</span></span> <span data-ttu-id="45d73-130">Um registro é marcado somente na presença ou ausência de uma marca específica.</span><span class="sxs-lookup"><span data-stu-id="45d73-130">A registration is matched only on the presence or absence of a specific tag.</span></span>

<span data-ttu-id="45d73-131">Para obter um tutorial passo a passo completo sobre como usar marcas para enviar para grupos de interesse, consulte as [Últimas notícias](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span><span class="sxs-lookup"><span data-stu-id="45d73-131">For a full step-by-step tutorial on how to use tags for sending to interest groups, see [Breaking News](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span></span>

## <a name="using-tags-to-target-users"></a><span data-ttu-id="45d73-132">Como usar marcas para usuários de destino</span><span class="sxs-lookup"><span data-stu-id="45d73-132">Using tags to target users</span></span>
<span data-ttu-id="45d73-133">Outra maneira de usar marcas é identificar todos os dispositivos de um usuário específico.</span><span class="sxs-lookup"><span data-stu-id="45d73-133">Another way to use tags is to identify all the devices of a particular user.</span></span> <span data-ttu-id="45d73-134">Os registros podem ser marcados com uma marca que contenha uma ID de usuário, como na seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="45d73-134">Registrations can be tagged with a tag that contains a user id, as in the following picture:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags3.png)

<span data-ttu-id="45d73-135">Nesta figura, a UID de mensagem marcada:Alice atinge todas as UIDs de registros marcados:Alice; portanto, todos os dispositivos de Alice.</span><span class="sxs-lookup"><span data-stu-id="45d73-135">In this picture, the message tagged uid:Alice reaches all registrations tagged uid:Alice; hence, all of Alice’s devices.</span></span>

## <a name="tag-expressions"></a><span data-ttu-id="45d73-136">Expressões de marca</span><span class="sxs-lookup"><span data-stu-id="45d73-136">Tag expressions</span></span>
<span data-ttu-id="45d73-137">Há casos em que uma notificação tem como destino um conjunto de registros identificados não por uma única marca, mas por uma expressão booliana nas marcas.</span><span class="sxs-lookup"><span data-stu-id="45d73-137">There are cases in which a notification has to target a set of registrations that is identified not by a single tag, but by a Boolean expression on tags.</span></span>

<span data-ttu-id="45d73-138">Considere um aplicativo de esportes que envia um lembrete para todos em Boston sobre um jogo entre o Red Sox e o Cardinals.</span><span class="sxs-lookup"><span data-stu-id="45d73-138">Consider a sports application that sends a reminder to everyone in Boston about a game between the Red Sox and Cardinals.</span></span> <span data-ttu-id="45d73-139">Se o aplicativo cliente registrar marcas sobre interesse em times e localização, a notificação deverá ser direcionada para todos em Boston interessados no Red Sox ou no Cardinals.</span><span class="sxs-lookup"><span data-stu-id="45d73-139">If the client app registers tags about interest in teams and location, then the notification should be targeted to everyone in Boston who is interested in either the Red Sox or the Cardinals.</span></span> <span data-ttu-id="45d73-140">Essa condição pode ser expressada com a seguinte expressão booliana:</span><span class="sxs-lookup"><span data-stu-id="45d73-140">This condition can be expressed with the following Boolean expression:</span></span>

    (follows_RedSox || follows_Cardinals) && location_Boston


![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags4.png)

<span data-ttu-id="45d73-141">As expressões de marca podem conter todos os operadores boolianos, como E (&&), OU (||) e NÃO (!).</span><span class="sxs-lookup"><span data-stu-id="45d73-141">Tag expressions can contain all Boolean operators, such as AND (&&), OR (||), and NOT (!).</span></span> <span data-ttu-id="45d73-142">Eles também podem conter parênteses.</span><span class="sxs-lookup"><span data-stu-id="45d73-142">They can also contain parentheses.</span></span> <span data-ttu-id="45d73-143">As expressões de marca são limitadas a 20 marcas se contiverem apenas ORs; caso contrário, elas são limitadas a seis marcas.</span><span class="sxs-lookup"><span data-stu-id="45d73-143">Tag expressions are limited to 20 tags if they contain only ORs; otherwise they are limited to 6 tags.</span></span>

<span data-ttu-id="45d73-144">Aqui está um exemplo de envio de notificações com expressões de marca usando o SDK.</span><span class="sxs-lookup"><span data-stu-id="45d73-144">Here's an example for sending notifications with tag expressions using the SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    String userTag = "(location_Boston && !follows_Cardinals)";    

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You want info on the Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You want info on the Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
