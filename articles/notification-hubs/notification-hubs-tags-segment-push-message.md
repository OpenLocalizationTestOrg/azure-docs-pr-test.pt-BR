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
# <a name="routing-and-tag-expressions"></a>Expressões de marca e roteamento
## <a name="overview"></a>Visão geral
Expressões de marcas permitem que você tootarget a conjuntos específicos de dispositivos, ou mais especificamente, registros, ao enviar uma notificação por push por meio de Hubs de notificação.

## <a name="targeting-specific-registrations"></a>Como direcionar registros específicos
Olá somente modo tootarget notificação específica registros é tooassociate marcas com eles, direcionar essas marcas. Conforme discutido em [gerenciamento de registro](notification-hubs-push-notification-registration-management.md), no envio do pedido tooreceive notificações de um aplicativo tem um dispositivo de tooregister tratar em um hub de notificação. Quando um registro é criado em um hub de notificação, o back-end de aplicativo hello pode enviar tooit de notificações por push.
back-end de aplicativo Hello pode escolher Olá registros tootarget com uma notificação específica Olá maneiras a seguir:

1. **Difusão**: todos os registros no hub de notificação de saudação recebem notificação hello.
2. **Marca**: todos os registros que contêm Olá especificado marca receber notificação hello.
3. **Expressão de marca**: todos os registros cujos conjuntos de correspondência de marcas Olá expressão especificada recebem notificação hello.

## <a name="tags"></a>Marcas
Uma marca pode ser qualquer cadeia de caracteres, too120 caracteres, contendo alfanuméricos e Olá seguintes caracteres não alfanuméricos: '_', ' @', '#', '. ',':', '-'. Olá, exemplo a seguir mostra um aplicativo do qual você pode receber notificações do sistema sobre grupos musicais específicos. Nesse cenário, as notificações de tooroute uma maneira simples é toolabel registros com marcas que representam Olá diferentes bandas, como na figura abaixo de saudação.

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags.png)

Nesta figura, a mensagem de saudação marcados **Beatles** atingir somente Olá tablet registrado com marca de saudação **Beatles**.

Para mais informações sobre a criação de registros para marcas, consulte [Gerenciamento de registro](notification-hubs-push-notification-registration-management.md).

Você pode enviar notificações tootags usando Olá enviar os métodos de notificações de saudação `Microsoft.Azure.NotificationHubs.NotificationHubClient` classe Olá [Hubs de notificação do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK. Você também pode usar Node.js ou Olá APIs de REST de notificações por Push.  Aqui está um exemplo de uso Olá SDK.

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You requested a Beatles notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Beatles");

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You requested a Wailers notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Wailers");




Marcas não possuem toobe previamente configurado e podem se referir a conceitos específicos do aplicativo de toomultiple. Por exemplo, os usuários desse aplicativo de exemplo podem comentar sobre as faixas e deseja tooreceive notificações do sistema, não apenas para comentários de saudação em suas bandas favoritas, mas também para todos os comentários dos seus amigos, independentemente de banda Olá nos quais estão comentando. Olá figura abaixo mostra um exemplo desse cenário:

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags2.png)

Nesta imagem, Alice está interessada em atualizações para Olá Beatles e Bob está interessado em atualizações para Olá Wailers. Bob também está interessado nos comentários de Charlie e Charlie está interessado nos Wailers hello. Quando uma notificação é enviada para o comentário de Charlie sobre Olá Beatles, Alice e Bob recebê-lo.

Embora você possa codificar vários interesses em marcas (por exemplo, “band_Beatles” ou “follows_Charlie”), as marcas são sequências de caracteres simples e não propriedades com valores. Um registro é marcado somente na presença de saudação ou ausência de uma marca específica.

Para obter um tutorial passo a passo completo sobre como toouse marcas para envio toointerest grupos, consulte [últimas notícias](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).

## <a name="using-tags-tootarget-users"></a>Usando marcas tootarget usuários
Toouse de outra forma de marcas é tooidentify todos os dispositivos de saudação de um usuário específico. Os registros podem ser marcados com uma marca que contém uma id de usuário, como Olá figura abaixo:

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags3.png)

Nesta figura, UID: Alice marcada de mensagem de saudação atingir todos os registros marcados UID: Alice; Portanto, todos os dispositivos de Alice.

## <a name="tag-expressions"></a>Expressões de marca
Há casos em que uma notificação tem tootarget um conjunto de registros que é identificado não por uma única marca, mas por uma expressão booliana em marcas.

Considere um aplicativo de esportes que envia um lembrete tooeveryone em Boston sobre um jogo entre Olá Red Sox e o Cardinals. Se o aplicativo de cliente Olá registra marcas sobre interesse em equipes e localização, notificação Olá deve ser direcionada tooeveryone em Boston que se interessam Olá Red Sox ou Olá Cardinals. Essa condição pode ser expresso com hello expressão booleana a seguir:

    (follows_RedSox || follows_Cardinals) && location_Boston


![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags4.png)

As expressões de marca podem conter todos os operadores boolianos, como E (&&), OU (||) e NÃO (!). Eles também podem conter parênteses. Expressões de marca são limitadas too20 marcas se contiverem apenas ORs; Caso contrário, eles são marcas too6 limitado.

Aqui está um exemplo de envio de notificações com expressões de marca usando Olá SDK.

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
