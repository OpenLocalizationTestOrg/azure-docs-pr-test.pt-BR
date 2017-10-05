---
title: "Adicionar notificações por push ao aplicativo Xamarin Android | Microsoft Docs"
description: "Saiba como usar o Serviço de Aplicativo do Azure e os Hubs de notificação do Azure para enviar notificações por push para seu aplicativo Android.Xamarin"
services: app-service\mobile
documentationcenter: xamarin
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6f7e8517-e532-4559-9b07-874115f4c65b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: c3757d56fb1792092710740dc5ffbd64f18730cf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-xamarinandroid-app"></a><span data-ttu-id="1148d-103">Adicionar notificações por push ao aplicativo Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="1148d-103">Add push notifications to your Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="1148d-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="1148d-104">Overview</span></span>
<span data-ttu-id="1148d-105">Neste tutorial, você adicionará notificações por push ao projeto de [Início rápido do Xamarin.Android](app-service-mobile-windows-store-dotnet-get-started.md) de forma que sempre que um registro for inserido, uma notificação por push seja enviada.</span><span class="sxs-lookup"><span data-stu-id="1148d-105">In this tutorial, you add push notifications to the [Xamarin.Android quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="1148d-106">Se você não usar o projeto baixado do início rápido do servidor, deve adicionar o pacote de extensão de notificação por push ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="1148d-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="1148d-107">Confira [Trabalhar com o servidor back-end SDK do .NET para os Aplicativos Móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="1148d-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1148d-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1148d-108">Prerequisites</span></span>
<span data-ttu-id="1148d-109">Este tutorial exige o seguinte:</span><span class="sxs-lookup"><span data-stu-id="1148d-109">This tutorial requires the following:</span></span>

* <span data-ttu-id="1148d-110">Uma conta ativa do Google.</span><span class="sxs-lookup"><span data-stu-id="1148d-110">An active Google account.</span></span> <span data-ttu-id="1148d-111">Você pode se inscrever em uma conta do Google em [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="1148d-111">You can sign up for a Google account at [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>
* <span data-ttu-id="1148d-112">[Componente do cliente Google Cloud Messaging](http://components.xamarin.com/view/GCMClient/).</span><span class="sxs-lookup"><span data-stu-id="1148d-112">[Google Cloud Messaging Client Component](http://components.xamarin.com/view/GCMClient/).</span></span>

## <span data-ttu-id="1148d-113"><a name="configure-hub"></a>Configurar um novo Hub de Notificações</span><span class="sxs-lookup"><span data-stu-id="1148d-113"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="1148d-114"><a id="register"></a>Habilitar mensagens de nuvem Firebase</span><span class="sxs-lookup"><span data-stu-id="1148d-114"><a id="register"></a>Enable Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-to-send-push-requests"></a><span data-ttu-id="1148d-115">Configurar o Azure para enviar notificações por push</span><span class="sxs-lookup"><span data-stu-id="1148d-115">Configure Azure to send push requests</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <span data-ttu-id="1148d-116"><a id="update-server"></a>Atualizar o projeto de servidor para enviar notificações por push</span><span class="sxs-lookup"><span data-stu-id="1148d-116"><a id="update-server"></a>Update the server project to send push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="1148d-117"><a id="configure-app"></a>Configurar o projeto para notificações por push</span><span class="sxs-lookup"><span data-stu-id="1148d-117"><a id="configure-app"></a>Configure the client project for push notifications</span></span>
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <span data-ttu-id="1148d-118"><a id="add-push"></a>Adicionar código de notificações por push ao seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="1148d-118"><a id="add-push"></a>Add push notifications code to your app</span></span>
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <span data-ttu-id="1148d-119"><a name="test"></a>Testar notificações por push no seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="1148d-119"><a name="test"></a>Test push notifications in your app</span></span>
<span data-ttu-id="1148d-120">Você pode testar o aplicativo usando um dispositivo virtual no emulador.</span><span class="sxs-lookup"><span data-stu-id="1148d-120">You can test the app by using a virtual device in the emulator.</span></span> <span data-ttu-id="1148d-121">Há etapas de configuração adicionais exigidas durante a execução em um emulador.</span><span class="sxs-lookup"><span data-stu-id="1148d-121">There are additional configuration steps required when running on an emulator.</span></span>

1. <span data-ttu-id="1148d-122">Verifique se você está implantando ou depurando em um dispositivo virtual com APIs do Google definidas como destino, conforme mostrado abaixo no Gerenciador de AVD (dispositivo virtual Android).</span><span class="sxs-lookup"><span data-stu-id="1148d-122">Make sure that you are deploying to or debugging on a virtual device that has Google APIs set as the target, as shown below in the Android Virtual Device (AVD) manager.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. <span data-ttu-id="1148d-123">Adicione uma conta do Google para o dispositivo Android clicando em **Aplicativos** > **Configurações** > **Adicionar conta** e então siga os prompts.</span><span class="sxs-lookup"><span data-stu-id="1148d-123">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**, then follow the prompts.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. <span data-ttu-id="1148d-124">Execute o aplicativo todolist como feito anteriormente s e insira um novo item de tarefa pendente.</span><span class="sxs-lookup"><span data-stu-id="1148d-124">Run the todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="1148d-125">Dessa vez, um ícone de notificação é exibido na área de notificação.</span><span class="sxs-lookup"><span data-stu-id="1148d-125">This time, a notification icon is displayed in the notification area.</span></span> <span data-ttu-id="1148d-126">Você pode abrir a gaveta de notificações para exibir o texto completo da notificação.</span><span class="sxs-lookup"><span data-stu-id="1148d-126">You can open the notification drawer to view the full text of the notification.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
