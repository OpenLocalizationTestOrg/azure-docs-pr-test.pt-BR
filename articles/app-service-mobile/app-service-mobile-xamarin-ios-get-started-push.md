---
title: "aaaAdd push notificações tooyour xamarin aplicativo com o serviço de aplicativo do Azure"
description: "Saiba como aplicativo de xamarin tooyour notificações por push de toouse toosend de serviço de aplicativo do Azure"
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
ms.openlocfilehash: 3e6439aee4f3fe0f60b9786d0bbfd74c4f5e52d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinios-app"></a><span data-ttu-id="697ff-103">Adicionar notificações de push tooyour Xamarin.iOS App</span><span class="sxs-lookup"><span data-stu-id="697ff-103">Add push notifications tooyour Xamarin.iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="697ff-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="697ff-104">Overview</span></span>
<span data-ttu-id="697ff-105">Neste tutorial, você adiciona toohello de notificações por push [início rápido do xamarin](app-service-mobile-xamarin-ios-get-started.md) de projeto para que uma notificação por push seja enviada toohello dispositivo toda vez que um registro é inserido.</span><span class="sxs-lookup"><span data-stu-id="697ff-105">In this tutorial, you add push notifications toohello [Xamarin.iOS quick start](app-service-mobile-xamarin-ios-get-started.md) project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="697ff-106">Se você não usar Olá baixar o projeto de servidor de início rápido, será necessário Olá o pacote de extensão de notificação por push.</span><span class="sxs-lookup"><span data-stu-id="697ff-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="697ff-107">Consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="697ff-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="697ff-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="697ff-108">Prerequisites</span></span>
* <span data-ttu-id="697ff-109">Olá completa [xamarin quickstart](app-service-mobile-xamarin-ios-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="697ff-109">Complete hello [Xamarin.iOS quickstart](app-service-mobile-xamarin-ios-get-started.md) tutorial.</span></span>
* <span data-ttu-id="697ff-110">Um dispositivo físico iOS.</span><span class="sxs-lookup"><span data-stu-id="697ff-110">A physical iOS device.</span></span> <span data-ttu-id="697ff-111">Não há suporte para notificações por push pelo simulador de iOS hello.</span><span class="sxs-lookup"><span data-stu-id="697ff-111">Push notifications are not supported by hello iOS simulator.</span></span>

## <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="697ff-112">Registrar aplicativo hello para notificações por push no portal do desenvolvedor da Apple</span><span class="sxs-lookup"><span data-stu-id="697ff-112">Register hello app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-your-mobile-app-toosend-push-notifications"></a><span data-ttu-id="697ff-113">Configurar as notificações de push de toosend de aplicativo móvel</span><span class="sxs-lookup"><span data-stu-id="697ff-113">Configure your Mobile App toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a><span data-ttu-id="697ff-114">Olá servidor projeto toosend push notificações de atualização</span><span class="sxs-lookup"><span data-stu-id="697ff-114">Update hello server project toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-your-xamarinios-project"></a><span data-ttu-id="697ff-115">Configure seu projeto do Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="697ff-115">Configure your Xamarin.iOS project</span></span>
[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

## <a name="add-push-notifications-tooyour-app"></a><span data-ttu-id="697ff-116">Adicionar aplicativo de tooyour de notificações por push</span><span class="sxs-lookup"><span data-stu-id="697ff-116">Add push notifications tooyour app</span></span>
1. <span data-ttu-id="697ff-117">Em **QSTodoService**, adicionar Olá propriedade a seguir para que **AppDelegate** pode adquirir cliente móvel hello:</span><span class="sxs-lookup"><span data-stu-id="697ff-117">In **QSTodoService**, add hello following property so that **AppDelegate** can acquire hello mobile client:</span></span>
   
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
2. <span data-ttu-id="697ff-118">Adicione o seguinte Olá `using` superior de toohello de instrução de saudação **appdelegate. CS** arquivo.</span><span class="sxs-lookup"><span data-stu-id="697ff-118">Add hello following `using` statement toohello top of hello **AppDelegate.cs** file.</span></span>
   
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. <span data-ttu-id="697ff-119">Em **AppDelegate**, substituir Olá **FinishedLaunching** evento:</span><span class="sxs-lookup"><span data-stu-id="697ff-119">In **AppDelegate**, override hello **FinishedLaunching** event:</span></span>
   
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
4. <span data-ttu-id="697ff-120">Em Olá mesmo arquivo, substitua Olá **RegisteredForRemoteNotifications** eventos.</span><span class="sxs-lookup"><span data-stu-id="697ff-120">In hello same file, override hello **RegisteredForRemoteNotifications** event.</span></span> <span data-ttu-id="697ff-121">Nesse código, você está registrando para uma notificação de modelo simples que será enviada em todas as plataformas com suporte pelo servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="697ff-121">In this code you are registering for a simple template notification that will be sent across all supported platforms by hello server.</span></span>
   
    <span data-ttu-id="697ff-122">Para saber mais sobre modelos com os Hubs de Notificação, confira [Modelos](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="697ff-122">For more information on templates with Notification Hubs, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>

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


1. <span data-ttu-id="697ff-123">Em seguida, substituir Olá **DidReceivedRemoteNotification** evento:</span><span class="sxs-lookup"><span data-stu-id="697ff-123">Then, override hello **DidReceivedRemoteNotification** event:</span></span>
   
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

<span data-ttu-id="697ff-124">Seu aplicativo agora está atualizada toosupport notificações de envio.</span><span class="sxs-lookup"><span data-stu-id="697ff-124">Your app is now updated toosupport push notifications.</span></span>

## <span data-ttu-id="697ff-125"><a name="test"></a>Testar notificações por push no seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="697ff-125"><a name="test"></a>Test push notifications in your app</span></span>
1. <span data-ttu-id="697ff-126">Olá pressione **executar** toobuild projeto de saudação e iniciar o aplicativo hello em um dispositivo compatível com iOS e clique em **Okey** tooaccept as notificações de envio.</span><span class="sxs-lookup"><span data-stu-id="697ff-126">Press hello **Run** button toobuild hello project and start hello app in an iOS capable device, then click **OK** tooaccept push notifications.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="697ff-127">Você deve aceitar explicitamente as notificações por push do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="697ff-127">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="697ff-128">Essa solicitação ocorre apenas Olá Olá aplicativo será executado pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="697ff-128">This request only occurs hello first time that hello app runs.</span></span>
   > 
   > 
2. <span data-ttu-id="697ff-129">No aplicativo hello, digite uma tarefa e, em seguida, clique em Olá adição (**+**) ícone.</span><span class="sxs-lookup"><span data-stu-id="697ff-129">In hello app, type a task, and then click hello plus (**+**) icon.</span></span>
3. <span data-ttu-id="697ff-130">Verifique se que uma notificação é recebida, e clique em **Okey** toodismiss Olá notificação.</span><span class="sxs-lookup"><span data-stu-id="697ff-130">Verify that a notification is received, then click **OK** toodismiss hello notification.</span></span>
4. <span data-ttu-id="697ff-131">Repita a etapa 2 e fechar imediatamente Olá aplicativo e verifique se uma notificação é mostrada.</span><span class="sxs-lookup"><span data-stu-id="697ff-131">Repeat step 2 and immediately close hello app, then verify that a notification is shown.</span></span>

<span data-ttu-id="697ff-132">Este tutorial foi concluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="697ff-132">You have successfully completed this tutorial.</span></span>

<!-- Images. -->

<!-- URLs. -->



