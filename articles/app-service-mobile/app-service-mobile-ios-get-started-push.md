---
title: "aaaAdd tooiOS de notificações por Push o aplicativo com aplicativos móveis do Azure"
description: "Saiba como aplicativo de iOS tooyour notificações por push de toosend do toouse os aplicativos móveis do Azure."
services: app-service\mobile
documentationcenter: ios
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: fa503833-d23e-4925-8d93-341bb3fbab7d
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/10/2016
ms.author: glenga
ms.openlocfilehash: 11588c56bc8987a71257dbad4fcdebf1b3209b1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-ios-app"></a>Adicionar aplicativo do iOS de tooyour notificações por Push
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Visão geral
Neste tutorial, você adiciona toohello de notificações por push [início rápido do iOS] projeto para que uma notificação por push seja enviada toohello dispositivo toda vez que um registro é inserido.

Se você não usar Olá baixar o projeto de servidor de início rápido, será necessário Olá o pacote de extensão de notificação por push. Consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para obter mais informações.

Olá [simulador iOS não dá suporte a notificações por push](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html). Você precisa de um dispositivo iOS físico e uma [Associação de programa para desenvolvedores da Apple](https://developer.apple.com/programs/ios/).

## <a name="configure-hub"></a>Configurar Hub de Notificações
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a id="register"></a>Registre o aplicativo para obter notificações por push
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-azure-toosend-push-notifications"></a>Configurar notificações por push de toosend do Azure
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a id="update-server"></a>Atualizar as notificações por push de toosend de back-end
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-apns](../../includes/app-service-mobile-dotnet-backend-configure-push-apns.md)]

## <a id="add-push"></a>Adicionar tooapp de notificações por push
[!INCLUDE [app-service-mobile-add-push-notifications-to-ios-app.md](../../includes/app-service-mobile-add-push-notifications-to-ios-app.md)]

## <a id="test"></a>Testar notificações por push
[!INCLUDE [Test Push Notifications in App](../../includes/test-push-notifications-in-app.md)]

## <a id="more"></a>Mais
* Modelos oferecem envios de plataforma cruzada toosend flexibilidade e envios localizados. [Como tooUse iOS biblioteca de cliente para aplicativos móveis do Azure](app-service-mobile-ios-how-to-use-client-library.md#templates) mostra como tooregister modelos.

<!-- Anchors.  -->

<!-- Images. -->

<!-- URLs. -->
[início rápido do iOS]: app-service-mobile-ios-get-started.md
