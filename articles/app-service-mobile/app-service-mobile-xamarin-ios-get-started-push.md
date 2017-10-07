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
# <a name="add-push-notifications-tooyour-xamarinios-app"></a>Adicionar notificações de push tooyour Xamarin.iOS App
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Visão geral
Neste tutorial, você adiciona toohello de notificações por push [início rápido do xamarin](app-service-mobile-xamarin-ios-get-started.md) de projeto para que uma notificação por push seja enviada toohello dispositivo toda vez que um registro é inserido.

Se você não usar Olá baixar o projeto de servidor de início rápido, será necessário Olá o pacote de extensão de notificação por push. Consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para obter mais informações.

## <a name="prerequisites"></a>Pré-requisitos
* Olá completa [xamarin quickstart](app-service-mobile-xamarin-ios-get-started.md) tutorial.
* Um dispositivo físico iOS. Não há suporte para notificações por push pelo simulador de iOS hello.

## <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a>Registrar aplicativo hello para notificações por push no portal do desenvolvedor da Apple
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-your-mobile-app-toosend-push-notifications"></a>Configurar as notificações de push de toosend de aplicativo móvel
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a>Olá servidor projeto toosend push notificações de atualização
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-your-xamarinios-project"></a>Configure seu projeto do Xamarin.iOS
[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

## <a name="add-push-notifications-tooyour-app"></a>Adicionar aplicativo de tooyour de notificações por push
1. Em **QSTodoService**, adicionar Olá propriedade a seguir para que **AppDelegate** pode adquirir cliente móvel hello:
   
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
2. Adicione o seguinte Olá `using` superior de toohello de instrução de saudação **appdelegate. CS** arquivo.
   
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. Em **AppDelegate**, substituir Olá **FinishedLaunching** evento:
   
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
4. Em Olá mesmo arquivo, substitua Olá **RegisteredForRemoteNotifications** eventos. Nesse código, você está registrando para uma notificação de modelo simples que será enviada em todas as plataformas com suporte pelo servidor de saudação.
   
    Para saber mais sobre modelos com os Hubs de Notificação, confira [Modelos](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).

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


1. Em seguida, substituir Olá **DidReceivedRemoteNotification** evento:
   
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

Seu aplicativo agora está atualizada toosupport notificações de envio.

## <a name="test"></a>Testar notificações por push no seu aplicativo
1. Olá pressione **executar** toobuild projeto de saudação e iniciar o aplicativo hello em um dispositivo compatível com iOS e clique em **Okey** tooaccept as notificações de envio.
   
   > [!NOTE]
   > Você deve aceitar explicitamente as notificações por push do seu aplicativo. Essa solicitação ocorre apenas Olá Olá aplicativo será executado pela primeira vez.
   > 
   > 
2. No aplicativo hello, digite uma tarefa e, em seguida, clique em Olá adição (**+**) ícone.
3. Verifique se que uma notificação é recebida, e clique em **Okey** toodismiss Olá notificação.
4. Repita a etapa 2 e fechar imediatamente Olá aplicativo e verifique se uma notificação é mostrada.

Este tutorial foi concluído com êxito.

<!-- Images. -->

<!-- URLs. -->



