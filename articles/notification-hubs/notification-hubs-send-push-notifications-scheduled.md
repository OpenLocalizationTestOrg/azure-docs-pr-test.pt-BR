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
# <a name="how-to-send-scheduled-notifications"></a>Como enviar notificações agendadas
## <a name="overview"></a>Visão geral
Se você tiver um cenário no qual você deseja toosend uma notificação em algum ponto Olá futura, mas não têm uma maneira fácil de toowake a notificação de saudação de toosend seu código de back-end. Camada padrão dos Hubs de notificação dá suporte a um recurso que permite a você notificações tooschedule backup too7 dias Olá futuras.

Ao enviar uma notificação, simplesmente usar Olá [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) classe no hello SDK de Hubs de notificação, conforme mostrado no exemplo a seguir de saudação:

    Notification notification = new AppleNotification("{\"aps\":{\"alert\":\"Happy birthday!\"}}");
    var scheduled = await hub.ScheduleNotificationAsync(notification, new DateTime(2014, 7, 19, 0, 0, 0));

Além disso, você pode cancelar uma notificação previamente agendada usando essa notificationId:

    await hub.CancelNotificationAsync(scheduled.ScheduledNotificationId);

Não há nenhum limite no número de saudação de notificações agendadas que você pode enviar.

