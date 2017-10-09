---
title: "aaaRouting e expressões de marca"
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
ms.openlocfilehash: c2c60500f7469f1cb1a73a5cf63c221a9ad6cbb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="routing-and-tag-expressions"></a><span data-ttu-id="d651f-103">Expressões de marca e roteamento</span><span class="sxs-lookup"><span data-stu-id="d651f-103">Routing and tag expressions</span></span>
## <a name="overview"></a><span data-ttu-id="d651f-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d651f-104">Overview</span></span>
<span data-ttu-id="d651f-105">Expressões de marcas permitem que você tootarget a conjuntos específicos de dispositivos, ou mais especificamente, registros, ao enviar uma notificação por push por meio de Hubs de notificação.</span><span class="sxs-lookup"><span data-stu-id="d651f-105">Tag expressions enable you tootarget specific sets of devices, or more specifically registrations, when sending a push notification through Notification Hubs.</span></span>

## <a name="targeting-specific-registrations"></a><span data-ttu-id="d651f-106">Como direcionar registros específicos</span><span class="sxs-lookup"><span data-stu-id="d651f-106">Targeting specific registrations</span></span>
<span data-ttu-id="d651f-107">Olá somente modo tootarget notificação específica registros é tooassociate marcas com eles, direcionar essas marcas.</span><span class="sxs-lookup"><span data-stu-id="d651f-107">hello only way tootarget specific notification registrations is tooassociate tags with them, then target those tags.</span></span> <span data-ttu-id="d651f-108">Conforme discutido em [gerenciamento de registro](notification-hubs-push-notification-registration-management.md), no envio do pedido tooreceive notificações de um aplicativo tem um dispositivo de tooregister tratar em um hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="d651f-108">As discussed in [Registration Management](notification-hubs-push-notification-registration-management.md), in order tooreceive push notifications an app has tooregister a device handle on a notification hub.</span></span> <span data-ttu-id="d651f-109">Quando um registro é criado em um hub de notificação, o back-end de aplicativo hello pode enviar tooit de notificações por push.</span><span class="sxs-lookup"><span data-stu-id="d651f-109">Once a registration is created on a notification hub, hello application backend can send push notifications tooit.</span></span>
<span data-ttu-id="d651f-110">back-end de aplicativo Hello pode escolher Olá registros tootarget com uma notificação específica Olá maneiras a seguir:</span><span class="sxs-lookup"><span data-stu-id="d651f-110">hello application backend can choose hello registrations tootarget with a specific notification in hello following ways:</span></span>

1. <span data-ttu-id="d651f-111">**Difusão**: todos os registros no hub de notificação de saudação recebem notificação hello.</span><span class="sxs-lookup"><span data-stu-id="d651f-111">**Broadcast**: all registrations in hello notification hub receive hello notification.</span></span>
2. <span data-ttu-id="d651f-112">**Marca**: todos os registros que contêm Olá especificado marca receber notificação hello.</span><span class="sxs-lookup"><span data-stu-id="d651f-112">**Tag**: all registrations that contain hello specified tag receive hello notification.</span></span>
3. <span data-ttu-id="d651f-113">**Expressão de marca**: todos os registros cujos conjuntos de correspondência de marcas Olá expressão especificada recebem notificação hello.</span><span class="sxs-lookup"><span data-stu-id="d651f-113">**Tag expression**: all registrations whose set of tags match hello specified expression receive hello notification.</span></span>

## <a name="tags"></a><span data-ttu-id="d651f-114">Marcas</span><span class="sxs-lookup"><span data-stu-id="d651f-114">Tags</span></span>
<span data-ttu-id="d651f-115">Uma marca pode ser qualquer cadeia de caracteres, too120 caracteres, contendo alfanuméricos e Olá seguintes caracteres não alfanuméricos: '_', ' @', '#', '. ',':', '-'.</span><span class="sxs-lookup"><span data-stu-id="d651f-115">A tag can be any string, up too120 characters, containing alphanumeric and hello following non-alphanumeric characters: ‘_’, ‘@’, ‘#’, ‘.’, ‘:’, ‘-’.</span></span> <span data-ttu-id="d651f-116">Olá, exemplo a seguir mostra um aplicativo do qual você pode receber notificações do sistema sobre grupos musicais específicos.</span><span class="sxs-lookup"><span data-stu-id="d651f-116">hello following example shows an application from which you can receive toast notifications about specific music groups.</span></span> <span data-ttu-id="d651f-117">Nesse cenário, as notificações de tooroute uma maneira simples é toolabel registros com marcas que representam Olá diferentes bandas, como na figura abaixo de saudação.</span><span class="sxs-lookup"><span data-stu-id="d651f-117">In this scenario, a simple way tooroute notifications is toolabel registrations with tags that represent hello different bands, as in hello following picture.</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags.png)

<span data-ttu-id="d651f-118">Nesta figura, a mensagem de saudação marcados **Beatles** atingir somente Olá tablet registrado com marca de saudação **Beatles**.</span><span class="sxs-lookup"><span data-stu-id="d651f-118">In this picture, hello message tagged **Beatles** reaches only hello tablet that registered with hello tag **Beatles**.</span></span>

<span data-ttu-id="d651f-119">Para mais informações sobre a criação de registros para marcas, consulte [Gerenciamento de registro](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="d651f-119">For more information about creating registrations for tags, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

<span data-ttu-id="d651f-120">Você pode enviar notificações tootags usando Olá enviar os métodos de notificações de saudação `Microsoft.Azure.NotificationHubs.NotificationHubClient` classe Olá [Hubs de notificação do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK.</span><span class="sxs-lookup"><span data-stu-id="d651f-120">You can send notifications tootags using hello send notifications methods of hello `Microsoft.Azure.NotificationHubs.NotificationHubClient` class in hello [Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK.</span></span> <span data-ttu-id="d651f-121">Você também pode usar Node.js ou Olá APIs de REST de notificações por Push.</span><span class="sxs-lookup"><span data-stu-id="d651f-121">You can also use Node.js, or hello Push Notifications REST APIs.</span></span>  <span data-ttu-id="d651f-122">Aqui está um exemplo de uso Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="d651f-122">Here's an example using hello SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You requested a Beatles notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Beatles");

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You requested a Wailers notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Wailers");




<span data-ttu-id="d651f-123">Marcas não possuem toobe previamente configurado e podem se referir a conceitos específicos do aplicativo de toomultiple.</span><span class="sxs-lookup"><span data-stu-id="d651f-123">Tags do not have toobe pre-provisioned and can refer toomultiple app-specific concepts.</span></span> <span data-ttu-id="d651f-124">Por exemplo, os usuários desse aplicativo de exemplo podem comentar sobre as faixas e deseja tooreceive notificações do sistema, não apenas para comentários de saudação em suas bandas favoritas, mas também para todos os comentários dos seus amigos, independentemente de banda Olá nos quais estão comentando.</span><span class="sxs-lookup"><span data-stu-id="d651f-124">For example, users of this example application can comment on bands and want tooreceive toasts, not only for hello comments on their favorite bands, but also for all comments from their friends, regardless of hello band on which they are commenting.</span></span> <span data-ttu-id="d651f-125">Olá figura abaixo mostra um exemplo desse cenário:</span><span class="sxs-lookup"><span data-stu-id="d651f-125">hello following picture shows an example of this scenario:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags2.png)

<span data-ttu-id="d651f-126">Nesta imagem, Alice está interessada em atualizações para Olá Beatles e Bob está interessado em atualizações para Olá Wailers.</span><span class="sxs-lookup"><span data-stu-id="d651f-126">In this picture, Alice is interested in updates for hello Beatles, and Bob is interested in updates for hello Wailers.</span></span> <span data-ttu-id="d651f-127">Bob também está interessado nos comentários de Charlie e Charlie está interessado nos Wailers hello.</span><span class="sxs-lookup"><span data-stu-id="d651f-127">Bob is also interested in Charlie’s comments, and Charlie is in interested in hello Wailers.</span></span> <span data-ttu-id="d651f-128">Quando uma notificação é enviada para o comentário de Charlie sobre Olá Beatles, Alice e Bob recebê-lo.</span><span class="sxs-lookup"><span data-stu-id="d651f-128">When a notification is sent for Charlie’s comment on hello Beatles, both Alice and Bob receive it.</span></span>

<span data-ttu-id="d651f-129">Embora você possa codificar vários interesses em marcas (por exemplo, “band_Beatles” ou “follows_Charlie”), as marcas são sequências de caracteres simples e não propriedades com valores.</span><span class="sxs-lookup"><span data-stu-id="d651f-129">While you can encode multiple concerns in tags (for example, “band_Beatles” or “follows_Charlie”), tags are simple strings and not properties with values.</span></span> <span data-ttu-id="d651f-130">Um registro é marcado somente na presença de saudação ou ausência de uma marca específica.</span><span class="sxs-lookup"><span data-stu-id="d651f-130">A registration is matched only on hello presence or absence of a specific tag.</span></span>

<span data-ttu-id="d651f-131">Para obter um tutorial passo a passo completo sobre como toouse marcas para envio toointerest grupos, consulte [últimas notícias](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span><span class="sxs-lookup"><span data-stu-id="d651f-131">For a full step-by-step tutorial on how toouse tags for sending toointerest groups, see [Breaking News](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span></span>

## <a name="using-tags-tootarget-users"></a><span data-ttu-id="d651f-132">Usando marcas tootarget usuários</span><span class="sxs-lookup"><span data-stu-id="d651f-132">Using tags tootarget users</span></span>
<span data-ttu-id="d651f-133">Toouse de outra forma de marcas é tooidentify todos os dispositivos de saudação de um usuário específico.</span><span class="sxs-lookup"><span data-stu-id="d651f-133">Another way toouse tags is tooidentify all hello devices of a particular user.</span></span> <span data-ttu-id="d651f-134">Os registros podem ser marcados com uma marca que contém uma id de usuário, como Olá figura abaixo:</span><span class="sxs-lookup"><span data-stu-id="d651f-134">Registrations can be tagged with a tag that contains a user id, as in hello following picture:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags3.png)

<span data-ttu-id="d651f-135">Nesta figura, UID: Alice marcada de mensagem de saudação atingir todos os registros marcados UID: Alice; Portanto, todos os dispositivos de Alice.</span><span class="sxs-lookup"><span data-stu-id="d651f-135">In this picture, hello message tagged uid:Alice reaches all registrations tagged uid:Alice; hence, all of Alice’s devices.</span></span>

## <a name="tag-expressions"></a><span data-ttu-id="d651f-136">Expressões de marca</span><span class="sxs-lookup"><span data-stu-id="d651f-136">Tag expressions</span></span>
<span data-ttu-id="d651f-137">Há casos em que uma notificação tem tootarget um conjunto de registros que é identificado não por uma única marca, mas por uma expressão booliana em marcas.</span><span class="sxs-lookup"><span data-stu-id="d651f-137">There are cases in which a notification has tootarget a set of registrations that is identified not by a single tag, but by a Boolean expression on tags.</span></span>

<span data-ttu-id="d651f-138">Considere um aplicativo de esportes que envia um lembrete tooeveryone em Boston sobre um jogo entre Olá Red Sox e o Cardinals.</span><span class="sxs-lookup"><span data-stu-id="d651f-138">Consider a sports application that sends a reminder tooeveryone in Boston about a game between hello Red Sox and Cardinals.</span></span> <span data-ttu-id="d651f-139">Se o aplicativo de cliente Olá registra marcas sobre interesse em equipes e localização, notificação Olá deve ser direcionada tooeveryone em Boston que se interessam Olá Red Sox ou Olá Cardinals.</span><span class="sxs-lookup"><span data-stu-id="d651f-139">If hello client app registers tags about interest in teams and location, then hello notification should be targeted tooeveryone in Boston who is interested in either hello Red Sox or hello Cardinals.</span></span> <span data-ttu-id="d651f-140">Essa condição pode ser expresso com hello expressão booleana a seguir:</span><span class="sxs-lookup"><span data-stu-id="d651f-140">This condition can be expressed with hello following Boolean expression:</span></span>

    (follows_RedSox || follows_Cardinals) && location_Boston


![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags4.png)

<span data-ttu-id="d651f-141">As expressões de marca podem conter todos os operadores boolianos, como E (&&), OU (||) e NÃO (!).</span><span class="sxs-lookup"><span data-stu-id="d651f-141">Tag expressions can contain all Boolean operators, such as AND (&&), OR (||), and NOT (!).</span></span> <span data-ttu-id="d651f-142">Eles também podem conter parênteses.</span><span class="sxs-lookup"><span data-stu-id="d651f-142">They can also contain parentheses.</span></span> <span data-ttu-id="d651f-143">Expressões de marca são limitadas too20 marcas se contiverem apenas ORs; Caso contrário, eles são marcas too6 limitado.</span><span class="sxs-lookup"><span data-stu-id="d651f-143">Tag expressions are limited too20 tags if they contain only ORs; otherwise they are limited too6 tags.</span></span>

<span data-ttu-id="d651f-144">Aqui está um exemplo de envio de notificações com expressões de marca usando Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="d651f-144">Here's an example for sending notifications with tag expressions using hello SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    String userTag = "(location_Boston && !follows_Cardinals)";    

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You want info on hello Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You want info on hello Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
