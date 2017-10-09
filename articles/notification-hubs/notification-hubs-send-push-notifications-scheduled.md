---
title: "aaaHow toosend agendado notificações | Microsoft Docs"
description: "Este tópico descreve como usar as Notificações Agendadas com os Hubs de Notificação do Azure."
services: notification-hubs
documentationcenter: .net
keywords: "notificações por push, notificação por push, agendando notificações por push"
author: ysxu
manager: erikre
editor: 
ms.assetid: 6b718c75-75dd-4c99-aee3-db1288235c1a
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 9b3ba715dad6f5d824a615e83f2863b0db47b533
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-send-scheduled-notifications"></a><span data-ttu-id="0a8fb-104">Como enviar notificações agendadas</span><span class="sxs-lookup"><span data-stu-id="0a8fb-104">How To: Send scheduled notifications</span></span>
## <a name="overview"></a><span data-ttu-id="0a8fb-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="0a8fb-105">Overview</span></span>
<span data-ttu-id="0a8fb-106">Se você tiver um cenário no qual você deseja toosend uma notificação em algum ponto Olá futura, mas não têm uma maneira fácil de toowake a notificação de saudação de toosend seu código de back-end.</span><span class="sxs-lookup"><span data-stu-id="0a8fb-106">If you have a scenario in which you want toosend a notification at some point in hello future, but do not have an easy way toowake up your back-end code toosend hello notification.</span></span> <span data-ttu-id="0a8fb-107">Camada padrão dos Hubs de notificação dá suporte a um recurso que permite a você notificações tooschedule backup too7 dias Olá futuras.</span><span class="sxs-lookup"><span data-stu-id="0a8fb-107">Standard tier Notification Hubs supports a feature that enables you tooschedule notifications up too7 days in hello future.</span></span>

<span data-ttu-id="0a8fb-108">Ao enviar uma notificação, simplesmente usar Olá [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) classe no hello SDK de Hubs de notificação, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="0a8fb-108">When sending a notification, simply use hello [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) class in hello Notification Hubs SDK as shown in hello following example:</span></span>

    Notification notification = new AppleNotification("{\"aps\":{\"alert\":\"Happy birthday!\"}}");
    var scheduled = await hub.ScheduleNotificationAsync(notification, new DateTime(2014, 7, 19, 0, 0, 0));

<span data-ttu-id="0a8fb-109">Além disso, você pode cancelar uma notificação previamente agendada usando essa notificationId:</span><span class="sxs-lookup"><span data-stu-id="0a8fb-109">Also, you can cancel a previously scheduled notification using its notificationId:</span></span>

    await hub.CancelNotificationAsync(scheduled.ScheduledNotificationId);

<span data-ttu-id="0a8fb-110">Não há nenhum limite no número de saudação de notificações agendadas que você pode enviar.</span><span class="sxs-lookup"><span data-stu-id="0a8fb-110">There are no limits on hello number of scheduled notifications you can send.</span></span>

