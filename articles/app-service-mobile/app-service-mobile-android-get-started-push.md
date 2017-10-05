---
title: "Adicionar notificações por push ao aplicativo Android com os Aplicativos Móveis | Microsoft Docs"
description: "Saiba como usar os Aplicativos Móveis para enviar notificações por push ao seu aplicativo Android."
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
ms.openlocfilehash: b89e9af55342d5d7473d848956996f846250b4b5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-android-app"></a><span data-ttu-id="52011-103">Adicionar notificações por push ao aplicativo Android</span><span class="sxs-lookup"><span data-stu-id="52011-103">Add push notifications to your Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="52011-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="52011-104">Overview</span></span>
<span data-ttu-id="52011-105">Neste tutorial, você adicionará notificações por push ao projeto de [início rápido do Android] para que, sempre que um registro for inserido, uma notificação por push seja enviada.</span><span class="sxs-lookup"><span data-stu-id="52011-105">In this tutorial, you add push notifications to the [Android quick start] project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="52011-106">Se você não usar o projeto baixado do início rápido do servidor, deverá adicionar o pacote de extensão de notificação por push ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="52011-106">If you do not use the downloaded quick start server project, you need the push notification extension package.</span></span> <span data-ttu-id="52011-107">Para saber mais, veja [Trabalhar com o SDK do servidor de back-end do .NET para Aplicativos Móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="52011-107">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52011-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="52011-108">Prerequisites</span></span>
<span data-ttu-id="52011-109">Você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="52011-109">You need the following:</span></span>

* <span data-ttu-id="52011-110">Uma IDE, dependendo do back-end do projeto:</span><span class="sxs-lookup"><span data-stu-id="52011-110">An IDE, depending on your project's back end:</span></span>

  * <span data-ttu-id="52011-111">[Android Studio](https://developer.android.com/sdk/index.html), se esse aplicativo tiver um back-end do Node.js.</span><span class="sxs-lookup"><span data-stu-id="52011-111">[Android Studio](https://developer.android.com/sdk/index.html) if this app has a Node.js back end.</span></span>
  * <span data-ttu-id="52011-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) ou posterior, se esse aplicativo tiver um back-end do Microsoft .NET.</span><span class="sxs-lookup"><span data-stu-id="52011-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) or later if this app has a Microsoft .NET back end.</span></span>
* <span data-ttu-id="52011-113">Android 2.3 ou posterior, Google Repository revisão 27 ou posterior e Google Play Services 9.0.2 ou posterior para o Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="52011-113">Android 2.3 or later, Google Repository revision 27 or later, and Google Play Services 9.0.2 or later for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="52011-114">Conclua o [início rápido do Android].</span><span class="sxs-lookup"><span data-stu-id="52011-114">Complete the [Android quick start].</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="52011-115">Criar um projeto que ofereça suporte ao Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="52011-115">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a><span data-ttu-id="52011-116">Configurar um hub de notificação</span><span class="sxs-lookup"><span data-stu-id="52011-116">Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="configure-azure-to-send-push-notifications"></a><span data-ttu-id="52011-117">Configurar o Azure para enviar notificações por push</span><span class="sxs-lookup"><span data-stu-id="52011-117">Configure Azure to send push notifications</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a name="enable-push-notifications-for-the-server-project"></a><span data-ttu-id="52011-118">Em seguida, habilite as notificações por push para o projeto de servidor</span><span class="sxs-lookup"><span data-stu-id="52011-118">Enable push notifications for the server project</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

## <a name="add-push-notifications-to-your-app"></a><span data-ttu-id="52011-119">Adicionar notificações de push para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="52011-119">Add push notifications to your app</span></span>
<span data-ttu-id="52011-120">Nesta seção, você atualizará seu aplicativo de cliente Android para manipular notificações por push.</span><span class="sxs-lookup"><span data-stu-id="52011-120">In this section, you update your client Android app to handle push notifications.</span></span>

### <a name="verify-android-sdk-version"></a><span data-ttu-id="52011-121">Verificar a versão do SDK do Android</span><span class="sxs-lookup"><span data-stu-id="52011-121">Verify Android SDK version</span></span>
[!INCLUDE [app-service-mobile-verify-android-sdk-version](../../includes/app-service-mobile-verify-android-sdk-version.md)]

<span data-ttu-id="52011-122">A próxima etapa é instalar os serviços do Google Play.</span><span class="sxs-lookup"><span data-stu-id="52011-122">Your next step is to install Google Play services.</span></span> <span data-ttu-id="52011-123">O Google Cloud Messaging tem alguns requisitos mínimos de nível de API para desenvolvimento e teste, com os quais a propriedade **minSdkVersion** no manifesto deve estar em conformidade.</span><span class="sxs-lookup"><span data-stu-id="52011-123">Google Cloud Messaging has some minimum API level requirements for development and testing, which the **minSdkVersion** property in the manifest must conform to.</span></span>

<span data-ttu-id="52011-124">Se estiver testando com um dispositivo mais antigo, consulte [Set Up Google Play Services SDK] (Configurar a SDK do Google Play Services) para determinar o mínimo que esse valor pode ser definido e defina-o de maneira apropriada.</span><span class="sxs-lookup"><span data-stu-id="52011-124">If you are testing with an older device, consult [Set Up Google Play Services SDK] to determine how low you can set this value, and set it appropriately.</span></span>

### <a name="add-google-play-services-to-the-project"></a><span data-ttu-id="52011-125">Adicionar serviços do Google Play ao projeto</span><span class="sxs-lookup"><span data-stu-id="52011-125">Add Google Play services to the project</span></span>
[!INCLUDE [Add Play Services](../../includes/app-service-mobile-add-google-play-services.md)]

### <a name="add-code"></a><span data-ttu-id="52011-126">Incluir código</span><span class="sxs-lookup"><span data-stu-id="52011-126">Add code</span></span>
[!INCLUDE [app-service-mobile-android-getting-started-with-push](../../includes/app-service-mobile-android-getting-started-with-push.md)]

## <a name="test-the-app-against-the-published-mobile-service"></a><span data-ttu-id="52011-127">Testar o aplicativo no serviço móvel publicado</span><span class="sxs-lookup"><span data-stu-id="52011-127">Test the app against the published mobile service</span></span>
<span data-ttu-id="52011-128">Você pode testar o aplicativo anexando um telefone Android com um cabo USB diretamente ou usando um dispositivo virtual no emulador.</span><span class="sxs-lookup"><span data-stu-id="52011-128">You can test the app by directly attaching an Android phone with a USB cable, or by using a virtual device in the emulator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52011-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="52011-129">Next steps</span></span>
<span data-ttu-id="52011-130">Agora que você concluiu este tutorial, considere continuar com um dos seguintes tutoriais:</span><span class="sxs-lookup"><span data-stu-id="52011-130">Now that you completed this tutorial, consider continuing on to one of the following tutorials:</span></span>

* <span data-ttu-id="52011-131">[Adicionar autenticação ao aplicativo Android](app-service-mobile-android-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="52011-131">[Add authentication to your Android app](app-service-mobile-android-get-started-users.md).</span></span>
  <span data-ttu-id="52011-132">Saiba como adicionar autenticação ao projeto de início rápido da lista de tarefas pendentes no Android usando um provedor de identidade com suporte.</span><span class="sxs-lookup"><span data-stu-id="52011-132">Learn how to add authentication to the todolist quickstart project on Android using a supported identity provider.</span></span>
* <span data-ttu-id="52011-133">[Habilitar a sincronização offline para o aplicativo móvel Android](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="52011-133">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="52011-134">Saiba como adicionar suporte offline ao aplicativo usando um back-end dos Aplicativos Móveis.</span><span class="sxs-lookup"><span data-stu-id="52011-134">Learn how to add offline support to your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="52011-135">Com a sincronização offline, os usuários podem interagir com um aplicativo móvel &mdash; exibindo, adicionando ou modificando dados &mdash; mesmo quando não há nenhuma conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="52011-135">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs -->
<span data-ttu-id="52011-136">[início rápido do Android]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="52011-136">[Android quick start]: app-service-mobile-android-get-started.md</span></span>

<span data-ttu-id="52011-137">[Set Up Google Play Services SDK]:https://developers.google.com/android/guides/setup</span><span class="sxs-lookup"><span data-stu-id="52011-137">[Set Up Google Play Services SDK]:https://developers.google.com/android/guides/setup</span></span>
