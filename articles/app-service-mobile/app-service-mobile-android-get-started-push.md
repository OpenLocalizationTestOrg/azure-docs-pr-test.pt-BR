---
title: "aaaAdd push notificações tooyour aplicativo Android com aplicativos móveis | Microsoft Docs"
description: "Saiba como aplicativo Android do tooyour notificações por push de toouse toosend de aplicativos móveis."
services: app-service\mobile
documentationcenter: android
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: 9058ed6d-e871-4179-86af-0092d0ca09d3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: dcfb8463b395904b4bd0bf9bde2f71f259894066
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-android-app"></a><span data-ttu-id="88967-103">Adicionar notificações de push tooyour aplicativo Android</span><span class="sxs-lookup"><span data-stu-id="88967-103">Add push notifications tooyour Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="88967-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="88967-104">Overview</span></span>
<span data-ttu-id="88967-105">Neste tutorial, você adiciona toohello de notificações por push [início rápido do Android] projeto para que uma notificação por push seja enviada toohello dispositivo toda vez que um registro é inserido.</span><span class="sxs-lookup"><span data-stu-id="88967-105">In this tutorial, you add push notifications toohello [Android quick start] project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="88967-106">Se você não usar Olá baixar o projeto de servidor de início rápido, precisa Olá pacote de extensão de notificação por push.</span><span class="sxs-lookup"><span data-stu-id="88967-106">If you do not use hello downloaded quick start server project, you need hello push notification extension package.</span></span> <span data-ttu-id="88967-107">Para obter mais informações, consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="88967-107">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88967-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="88967-108">Prerequisites</span></span>
<span data-ttu-id="88967-109">Você precisa Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="88967-109">You need hello following:</span></span>

* <span data-ttu-id="88967-110">Uma IDE, dependendo do back-end do projeto:</span><span class="sxs-lookup"><span data-stu-id="88967-110">An IDE, depending on your project's back end:</span></span>

  * <span data-ttu-id="88967-111">[Android Studio](https://developer.android.com/sdk/index.html), se esse aplicativo tiver um back-end do Node.js.</span><span class="sxs-lookup"><span data-stu-id="88967-111">[Android Studio](https://developer.android.com/sdk/index.html) if this app has a Node.js back end.</span></span>
  * <span data-ttu-id="88967-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) ou posterior, se esse aplicativo tiver um back-end do Microsoft .NET.</span><span class="sxs-lookup"><span data-stu-id="88967-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) or later if this app has a Microsoft .NET back end.</span></span>
* <span data-ttu-id="88967-113">Android 2.3 ou posterior, Google Repository revisão 27 ou posterior e Google Play Services 9.0.2 ou posterior para o Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="88967-113">Android 2.3 or later, Google Repository revision 27 or later, and Google Play Services 9.0.2 or later for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="88967-114">Olá completa [início rápido do Android].</span><span class="sxs-lookup"><span data-stu-id="88967-114">Complete hello [Android quick start].</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="88967-115">Criar um projeto que ofereça suporte ao Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="88967-115">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a><span data-ttu-id="88967-116">Configurar um hub de notificação</span><span class="sxs-lookup"><span data-stu-id="88967-116">Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="configure-azure-toosend-push-notifications"></a><span data-ttu-id="88967-117">Configurar notificações por push de toosend do Azure</span><span class="sxs-lookup"><span data-stu-id="88967-117">Configure Azure toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a name="enable-push-notifications-for-hello-server-project"></a><span data-ttu-id="88967-118">Habilitar notificações por push para o projeto do servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="88967-118">Enable push notifications for hello server project</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

## <a name="add-push-notifications-tooyour-app"></a><span data-ttu-id="88967-119">Adicionar aplicativo de tooyour de notificações por push</span><span class="sxs-lookup"><span data-stu-id="88967-119">Add push notifications tooyour app</span></span>
<span data-ttu-id="88967-120">Nesta seção, você deve atualizar as notificações de push do cliente aplicativo Android toohandle.</span><span class="sxs-lookup"><span data-stu-id="88967-120">In this section, you update your client Android app toohandle push notifications.</span></span>

### <a name="verify-android-sdk-version"></a><span data-ttu-id="88967-121">Verificar a versão do SDK do Android</span><span class="sxs-lookup"><span data-stu-id="88967-121">Verify Android SDK version</span></span>
[!INCLUDE [app-service-mobile-verify-android-sdk-version](../../includes/app-service-mobile-verify-android-sdk-version.md)]

<span data-ttu-id="88967-122">A próxima etapa é tooinstall serviços do Google Play.</span><span class="sxs-lookup"><span data-stu-id="88967-122">Your next step is tooinstall Google Play services.</span></span> <span data-ttu-id="88967-123">Google Cloud Messaging tem alguns requisitos de nível de API mínimos para desenvolvimento e teste, quais Olá **minSdkVersion** propriedade no manifesto de saudação deve estar de acordo com.</span><span class="sxs-lookup"><span data-stu-id="88967-123">Google Cloud Messaging has some minimum API level requirements for development and testing, which hello **minSdkVersion** property in hello manifest must conform to.</span></span>

<span data-ttu-id="88967-124">Se você estiver testando com um dispositivo mais antigo, consulte [definir o Google reproduzir SDK dos serviços] toodetermine baixa como você pode definir esse valor e defini-lo apropriadamente.</span><span class="sxs-lookup"><span data-stu-id="88967-124">If you are testing with an older device, consult [Set Up Google Play Services SDK] toodetermine how low you can set this value, and set it appropriately.</span></span>

### <a name="add-google-play-services-toohello-project"></a><span data-ttu-id="88967-125">Adicionar projeto de toohello de serviços do Google Play</span><span class="sxs-lookup"><span data-stu-id="88967-125">Add Google Play services toohello project</span></span>
[!INCLUDE [Add Play Services](../../includes/app-service-mobile-add-google-play-services.md)]

### <a name="add-code"></a><span data-ttu-id="88967-126">Incluir código</span><span class="sxs-lookup"><span data-stu-id="88967-126">Add code</span></span>
[!INCLUDE [app-service-mobile-android-getting-started-with-push](../../includes/app-service-mobile-android-getting-started-with-push.md)]

## <a name="test-hello-app-against-hello-published-mobile-service"></a><span data-ttu-id="88967-127">Aplicativo de teste de saudação contra Olá publicado serviço móvel</span><span class="sxs-lookup"><span data-stu-id="88967-127">Test hello app against hello published mobile service</span></span>
<span data-ttu-id="88967-128">Você pode testar o aplicativo hello anexando diretamente um telefone Android com um cabo USB, ou usando um dispositivo virtual no emulador de saudação.</span><span class="sxs-lookup"><span data-stu-id="88967-128">You can test hello app by directly attaching an Android phone with a USB cable, or by using a virtual device in hello emulator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88967-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="88967-129">Next steps</span></span>
<span data-ttu-id="88967-130">Agora que você concluiu este tutorial, considere a possibilidade de continuar tooone de saudação tutoriais a seguir:</span><span class="sxs-lookup"><span data-stu-id="88967-130">Now that you completed this tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* <span data-ttu-id="88967-131">[Adicionar aplicativo do Android autenticação tooyour](app-service-mobile-android-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="88967-131">[Add authentication tooyour Android app](app-service-mobile-android-get-started-users.md).</span></span>
  <span data-ttu-id="88967-132">Saiba como guia de início rápido tooadd autenticação toohello todolist projeto Android usando um provedor de identidade com suporte.</span><span class="sxs-lookup"><span data-stu-id="88967-132">Learn how tooadd authentication toohello todolist quickstart project on Android using a supported identity provider.</span></span>
* <span data-ttu-id="88967-133">[Habilitar a sincronização offline para o aplicativo móvel Android](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="88967-133">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="88967-134">Saiba como o tooadd offline dão suporte ao aplicativo tooyour usando um back-end de aplicativos móveis.</span><span class="sxs-lookup"><span data-stu-id="88967-134">Learn how tooadd offline support tooyour app by using a Mobile Apps back end.</span></span> <span data-ttu-id="88967-135">Com a sincronização offline, os usuários podem interagir com um aplicativo móvel &mdash; exibindo, adicionando ou modificando dados &mdash; mesmo quando não há nenhuma conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="88967-135">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs -->
[início rápido do Android]: app-service-mobile-android-get-started.md

[definir o Google reproduzir SDK dos serviços]:https://developers.google.com/android/guides/setup
