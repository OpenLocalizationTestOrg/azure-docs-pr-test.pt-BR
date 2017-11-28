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
# <a name="add-push-notifications-tooyour-ios-app"></a><span data-ttu-id="6af49-103">Adicionar aplicativo do iOS de tooyour notificações por Push</span><span class="sxs-lookup"><span data-stu-id="6af49-103">Add Push Notifications tooyour iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="6af49-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="6af49-104">Overview</span></span>
<span data-ttu-id="6af49-105">Neste tutorial, você adiciona toohello de notificações por push [início rápido do iOS] projeto para que uma notificação por push seja enviada toohello dispositivo toda vez que um registro é inserido.</span><span class="sxs-lookup"><span data-stu-id="6af49-105">In this tutorial, you add push notifications toohello [iOS quick start] project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="6af49-106">Se você não usar Olá baixar o projeto de servidor de início rápido, será necessário Olá o pacote de extensão de notificação por push.</span><span class="sxs-lookup"><span data-stu-id="6af49-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="6af49-107">Consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="6af49-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

<span data-ttu-id="6af49-108">Olá [simulador iOS não dá suporte a notificações por push](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="6af49-108">hello [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span> <span data-ttu-id="6af49-109">Você precisa de um dispositivo iOS físico e uma [Associação de programa para desenvolvedores da Apple](https://developer.apple.com/programs/ios/).</span><span class="sxs-lookup"><span data-stu-id="6af49-109">You need a physical iOS device and an [Apple Developer Program membership](https://developer.apple.com/programs/ios/).</span></span>

## <span data-ttu-id="6af49-110"><a name="configure-hub"></a>Configurar Hub de Notificações</span><span class="sxs-lookup"><span data-stu-id="6af49-110"><a name="configure-hub"></a>Configure Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="6af49-111"><a id="register"></a>Registre o aplicativo para obter notificações por push</span><span class="sxs-lookup"><span data-stu-id="6af49-111"><a id="register"></a>Register app for push notifications</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-azure-toosend-push-notifications"></a><span data-ttu-id="6af49-112">Configurar notificações por push de toosend do Azure</span><span class="sxs-lookup"><span data-stu-id="6af49-112">Configure Azure toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <span data-ttu-id="6af49-113"><a id="update-server"></a>Atualizar as notificações por push de toosend de back-end</span><span class="sxs-lookup"><span data-stu-id="6af49-113"><a id="update-server"></a>Update backend toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-apns](../../includes/app-service-mobile-dotnet-backend-configure-push-apns.md)]

## <span data-ttu-id="6af49-114"><a id="add-push"></a>Adicionar tooapp de notificações por push</span><span class="sxs-lookup"><span data-stu-id="6af49-114"><a id="add-push"></a>Add push notifications tooapp</span></span>
[!INCLUDE [app-service-mobile-add-push-notifications-to-ios-app.md](../../includes/app-service-mobile-add-push-notifications-to-ios-app.md)]

## <span data-ttu-id="6af49-115"><a id="test"></a>Testar notificações por push</span><span class="sxs-lookup"><span data-stu-id="6af49-115"><a id="test"></a>Test push notifications</span></span>
[!INCLUDE [Test Push Notifications in App](../../includes/test-push-notifications-in-app.md)]

## <span data-ttu-id="6af49-116"><a id="more"></a>Mais</span><span class="sxs-lookup"><span data-stu-id="6af49-116"><a id="more"></a>More</span></span>
* <span data-ttu-id="6af49-117">Modelos oferecem envios de plataforma cruzada toosend flexibilidade e envios localizados.</span><span class="sxs-lookup"><span data-stu-id="6af49-117">Templates give you flexibility toosend cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="6af49-118">[Como tooUse iOS biblioteca de cliente para aplicativos móveis do Azure](app-service-mobile-ios-how-to-use-client-library.md#templates) mostra como tooregister modelos.</span><span class="sxs-lookup"><span data-stu-id="6af49-118">[How tooUse iOS Client Library for Azure Mobile Apps](app-service-mobile-ios-how-to-use-client-library.md#templates) shows you how tooregister templates.</span></span>

<!-- Anchors.  -->

<!-- Images. -->

<!-- URLs. -->
[início rápido do iOS]: app-service-mobile-ios-get-started.md
