---
title: "Adicionar notificações por push ao aplicativo iOS com aplicativos móveis do Azure"
description: "Saiba como usar aplicativos móveis do Azure para enviar notificações por push para seu aplicativo iOS."
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
ms.openlocfilehash: 08a8c35b89386bd0dbe7bba406a6985a5a0d7eb8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-ios-app"></a><span data-ttu-id="23e57-103">Adicionar as notificações por push ao seu aplicativo iOS</span><span class="sxs-lookup"><span data-stu-id="23e57-103">Add Push Notifications to your iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="23e57-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="23e57-104">Overview</span></span>
<span data-ttu-id="23e57-105">Neste tutorial, você adicionará notificações por push ao projeto de [Início rápido do iOS] de forma que sempre que um registro for inserido, uma notificação por push seja enviada.</span><span class="sxs-lookup"><span data-stu-id="23e57-105">In this tutorial, you add push notifications to the [iOS quick start] project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="23e57-106">Se você não usar o projeto baixado do início rápido do servidor, deve adicionar o pacote de extensão de notificação por push ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="23e57-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="23e57-107">Confira [Trabalhar com o servidor back-end SDK do .NET para os Aplicativos Móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="23e57-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

<span data-ttu-id="23e57-108">O [simulador do iOS não dá suporte a notificações por push](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="23e57-108">The [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span> <span data-ttu-id="23e57-109">Você precisa de um dispositivo iOS físico e uma [Associação de programa para desenvolvedores da Apple](https://developer.apple.com/programs/ios/).</span><span class="sxs-lookup"><span data-stu-id="23e57-109">You need a physical iOS device and an [Apple Developer Program membership](https://developer.apple.com/programs/ios/).</span></span>

## <span data-ttu-id="23e57-110"><a name="configure-hub"></a>Configurar Hub de Notificações</span><span class="sxs-lookup"><span data-stu-id="23e57-110"><a name="configure-hub"></a>Configure Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="23e57-111"><a id="register"></a>Registre o aplicativo para obter notificações por push</span><span class="sxs-lookup"><span data-stu-id="23e57-111"><a id="register"></a>Register app for push notifications</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-azure-to-send-push-notifications"></a><span data-ttu-id="23e57-112">Configurar o Azure para enviar notificações por push</span><span class="sxs-lookup"><span data-stu-id="23e57-112">Configure Azure to send push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <span data-ttu-id="23e57-113"><a id="update-server"></a>Atualizar back-end para enviar notificações por push</span><span class="sxs-lookup"><span data-stu-id="23e57-113"><a id="update-server"></a>Update backend to send push notifications</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-apns](../../includes/app-service-mobile-dotnet-backend-configure-push-apns.md)]

## <span data-ttu-id="23e57-114"><a id="add-push"></a>Adicionar notificações por push ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="23e57-114"><a id="add-push"></a>Add push notifications to app</span></span>
[!INCLUDE [app-service-mobile-add-push-notifications-to-ios-app.md](../../includes/app-service-mobile-add-push-notifications-to-ios-app.md)]

## <span data-ttu-id="23e57-115"><a id="test"></a>Testar notificações por push</span><span class="sxs-lookup"><span data-stu-id="23e57-115"><a id="test"></a>Test push notifications</span></span>
[!INCLUDE [Test Push Notifications in App](../../includes/test-push-notifications-in-app.md)]

## <span data-ttu-id="23e57-116"><a id="more"></a>Mais</span><span class="sxs-lookup"><span data-stu-id="23e57-116"><a id="more"></a>More</span></span>
* <span data-ttu-id="23e57-117">Os modelos fornecem a flexibilidade para enviar pushes de plataforma cruzada e pushes localizados.</span><span class="sxs-lookup"><span data-stu-id="23e57-117">Templates give you flexibility to send cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="23e57-118">[Como usar a biblioteca de cliente do iOS para aplicativos móveis do Azure](app-service-mobile-ios-how-to-use-client-library.md#templates) mostra como registrar os modelos.</span><span class="sxs-lookup"><span data-stu-id="23e57-118">[How to Use iOS Client Library for Azure Mobile Apps](app-service-mobile-ios-how-to-use-client-library.md#templates) shows you how to register templates.</span></span>

<!-- Anchors.  -->

<!-- Images. -->

<!-- URLs. -->
<span data-ttu-id="23e57-119">[Início rápido do iOS]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="23e57-119">[iOS quick start]: app-service-mobile-ios-get-started.md</span></span>
