---
title: "Adicionar notificações por push a seu aplicativo Xamarin iOS com o Serviço de Aplicativo do Azure"
description: "Aprenda a usar o Serviço de Aplicativo do Azure para enviar notificações por push para o aplicativo Xamarin.iOS"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 2921214a-49f8-45e1-a306-a85ce21defca
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: bf922e49c4c92d0065817a5dd6c7d10a04737304
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-xamarinios-app"></a><span data-ttu-id="f23c1-103">Adicionar notificações por push a seu aplicativo Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="f23c1-103">Add push notifications to your Xamarin.iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="f23c1-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="f23c1-104">Overview</span></span>
<span data-ttu-id="f23c1-105">Neste tutorial, você adicionará notificações por push ao projeto de [início rápido do Xamarin.iOS](app-service-mobile-xamarin-ios-get-started.md) de forma que sempre que um registro for inserido, uma notificação por push seja enviada.</span><span class="sxs-lookup"><span data-stu-id="f23c1-105">In this tutorial, you add push notifications to the [Xamarin.iOS quick start](app-service-mobile-xamarin-ios-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="f23c1-106">Se você não usar o projeto baixado do início rápido do servidor, deve adicionar o pacote de extensão de notificação por push ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="f23c1-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="f23c1-107">Confira [Trabalhar com o servidor back-end SDK do .NET para os Aplicativos Móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="f23c1-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f23c1-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f23c1-108">Prerequisites</span></span>
* <span data-ttu-id="f23c1-109">Conclua o tutorial [Criar um aplicativo Xamarin.iOS](app-service-mobile-xamarin-ios-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="f23c1-109">Complete the [Xamarin.iOS quickstart](app-service-mobile-xamarin-ios-get-started.md) tutorial.</span></span>
* <span data-ttu-id="f23c1-110">Um dispositivo físico iOS.</span><span class="sxs-lookup"><span data-stu-id="f23c1-110">A physical iOS device.</span></span> <span data-ttu-id="f23c1-111">Não há suporte para notificações por push pelo simulador do iOS.</span><span class="sxs-lookup"><span data-stu-id="f23c1-111">Push notifications are not supported by the iOS simulator.</span></span>

## <a name="register-the-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="f23c1-112">Registrar o aplicativo nas notificações por push no portal do desenvolvedor da Apple</span><span class="sxs-lookup"><span data-stu-id="f23c1-112">Register the app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-your-mobile-app-to-send-push-notifications"></a><span data-ttu-id="f23c1-113">Configurar o seu aplicativo móvel para enviar notificações por push</span><span class="sxs-lookup"><span data-stu-id="f23c1-113">Configure your Mobile App to send push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a name="update-the-server-project-to-send-push-notifications"></a><span data-ttu-id="f23c1-114">Atualizar o projeto de servidor para enviar notificações por push</span><span class="sxs-lookup"><span data-stu-id="f23c1-114">Update the server project to send push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-your-xamarinios-project"></a><span data-ttu-id="f23c1-115">Configure seu projeto do Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="f23c1-115">Configure your Xamarin.iOS project</span></span>
[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

## <a name="add-push-notifications-to-your-app"></a><span data-ttu-id="f23c1-116">Adicionar notificações de push para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="f23c1-116">Add push notifications to your app</span></span>
1. <span data-ttu-id="f23c1-117">Em **QSTodoService**, adicione a seguinte propriedade para que o **AppDelegate** possa adquirir o cliente móvel:</span><span class="sxs-lookup"><span data-stu-id="f23c1-117">In **QSTodoService**, add the following property so that **AppDelegate** can acquire the mobile client:</span></span>
   
            public MobileServiceClient GetClient {
            get
            {
                return client;
            }
            private set
            {
                client = value;
            }
        }
2. <span data-ttu-id="f23c1-118">Adicione a seguinte declaração `using` ao topo do arquivo **AppDelegate.cs** .</span><span class="sxs-lookup"><span data-stu-id="f23c1-118">Add the following `using` statement to the top of the **AppDelegate.cs** file.</span></span>
   
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. <span data-ttu-id="f23c1-119">Em **AppDelegate**, substitua o evento **FinishedLaunching**:</span><span class="sxs-lookup"><span data-stu-id="f23c1-119">In **AppDelegate**, override the **FinishedLaunching** event:</span></span>
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            // registers for push for iOS8
            var settings = UIUserNotificationSettings.GetSettingsForTypes(
                UIUserNotificationType.Alert
                | UIUserNotificationType.Badge
                | UIUserNotificationType.Sound,
                new NSSet());
   
            UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications();
   
            return true;
        }
4. <span data-ttu-id="f23c1-120">No mesmo arquivo, substitua o evento **RegisteredForRemoteNotifications**.</span><span class="sxs-lookup"><span data-stu-id="f23c1-120">In the same file, override the **RegisteredForRemoteNotifications** event.</span></span> <span data-ttu-id="f23c1-121">Nesse código, você está se registrando para uma notificação de modelo simples que será enviada em todas as plataformas com suporte do servidor.</span><span class="sxs-lookup"><span data-stu-id="f23c1-121">In this code you are registering for a simple template notification that will be sent across all supported platforms by the server.</span></span>
   
    <span data-ttu-id="f23c1-122">Para saber mais sobre modelos com os Hubs de Notificação, confira [Modelos](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="f23c1-122">For more information on templates with Notification Hubs, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>

        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            MobileServiceClient client = QSTodoService.DefaultService.GetClient;

            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyAPNS}
            };

            // Register for push with your mobile app
            var push = client.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }


1. <span data-ttu-id="f23c1-123">Então substitua o evento **DidReceivedRemoteNotification** :</span><span class="sxs-lookup"><span data-stu-id="f23c1-123">Then, override the **DidReceivedRemoteNotification** event:</span></span>
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;
   
            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps [new NSString("alert")] as NSString).ToString();
   
            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

<span data-ttu-id="f23c1-124">Seu aplicativo foi atualizado para oferecer suporte a notificações de push.</span><span class="sxs-lookup"><span data-stu-id="f23c1-124">Your app is now updated to support push notifications.</span></span>

## <span data-ttu-id="f23c1-125"><a name="test"></a>Testar notificações por push no seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="f23c1-125"><a name="test"></a>Test push notifications in your app</span></span>
1. <span data-ttu-id="f23c1-126">Pressione o botão **Executar** para compilar o projeto e iniciar o aplicativo em um dispositivo compatível com iOS; em seguida, clique em **OK** para aceitar as notificações por push.</span><span class="sxs-lookup"><span data-stu-id="f23c1-126">Press the **Run** button to build the project and start the app in an iOS capable device, then click **OK** to accept push notifications.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f23c1-127">Você deve aceitar explicitamente as notificações por push do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f23c1-127">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="f23c1-128">Essa solicitação ocorrerá apenas na primeira vez que o aplicativo for executado.</span><span class="sxs-lookup"><span data-stu-id="f23c1-128">This request only occurs the first time that the app runs.</span></span>
   > 
   > 
2. <span data-ttu-id="f23c1-129">No aplicativo, digite uma tarefa e clique no ícone do sinal de adição (**+**).</span><span class="sxs-lookup"><span data-stu-id="f23c1-129">In the app, type a task, and then click the plus (**+**) icon.</span></span>
3. <span data-ttu-id="f23c1-130">Verifique se uma notificação é recebida e clique em **OK** para ignorar a notificação.</span><span class="sxs-lookup"><span data-stu-id="f23c1-130">Verify that a notification is received, then click **OK** to dismiss the notification.</span></span>
4. <span data-ttu-id="f23c1-131">Repita a etapa 2 e imediatamente feche o aplicativo e verifique se uma notificação é exibida.</span><span class="sxs-lookup"><span data-stu-id="f23c1-131">Repeat step 2 and immediately close the app, then verify that a notification is shown.</span></span>

<span data-ttu-id="f23c1-132">Este tutorial foi concluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="f23c1-132">You have successfully completed this tutorial.</span></span>

<!-- Images. -->

<!-- URLs. -->



