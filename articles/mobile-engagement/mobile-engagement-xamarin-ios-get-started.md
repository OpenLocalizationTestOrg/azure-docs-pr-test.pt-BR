---
title: aaaGet iniciado com o Azure Mobile Engagement para xamarin
description: "Saiba como toouse Azure Mobile Engagement com análises e notificações por Push para aplicativos xamarin."
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0448209e-fff6-47bd-985c-2cf074bac12f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 02340a744753dcc5cd1b6888a5fa87628be47b68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinios-apps"></a>Introdução ao Azure Mobile Engagement para aplicativos Xamarin.iOS
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Este tópico mostra como toouse do Azure Mobile Engagement toounderstand seu uso do aplicativo e enviar por push os usuários toosegmented de notificações em um aplicativo xamarin.
Neste tutorial, você cria um aplicativo Xamarin.iOS em branco que coleta dados básicos e recebe notificações por push usando o Sistema de Notificação por Push da Apple (APNS).

> [!NOTE]
> serviço do Azure Mobile Engagement Olá será descontinuado de 2018 março e está apenas disponível tooexisting clientes. Para saber mais, confira [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Este tutorial requer o seguinte hello:

* [Xamarin Studio](http://xamarin.com/studio). Você também pode usar o Visual Studio com Xamarin, mas este tutorial usa o Xamarin Studio. Para obter instruções de instalação, confira [Instalar e configurar para Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx). 
* [SDK do Xamarin do Mobile Engagement](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> toocomplete neste tutorial, você deve ter uma conta ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).
> 
> 

## <a id="setup-azme"></a>Configurar o Mobile Engagement para seu aplicativo iOS
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Conectar seu back-end do aplicativo toohello Mobile Engagement
Este tutorial apresenta uma "integração básica" hello mínimo definido toocollect necessários dados e envia uma notificação por push.

Vamos criar um aplicativo básico com a integração de saudação do Xamarin toodemonstrate:

### <a name="create-a-new-xamarinios-project"></a>Criar um novo projeto do Xamarin.iOS
1. Inicie o Xamarin Studio. Vá muito**arquivo** -> **novo** -> **solução** 
   
    ![][1]
2. Selecione **único aplicativo de exibição**, certifique-se de idioma Olá selecionado é **c#** e, em seguida, clique em **próximo**.
   
    ![][2]
3. Preencha Olá **nome do aplicativo** e hello **identificador de organização** e, em seguida, clique em **próximo**. 
   
    ![][3]
   
   > [!IMPORTANT]
   > Certifique-se de que Olá você eventualmente usar toodeploy que seu aplicativo iOS está usando uma ID de aplicativo que corresponda exatamente com hello aqui de identificador de pacote de perfil de publicação. 
   > 
   > 
4. Saudação de atualização **nome do projeto**, **nome da solução** e **local** se necessário e clique em **criar**.
   
    ![][4]

Xamarin Studio criará o aplicativo de demonstração de Olá no qual integraremos Mobile Engagement. 

### <a name="connect-your-app-toomobile-engagement-backend"></a>Conectar seu back-end do aplicativo tooMobile contrato
1. Clique com botão direito Olá **pacotes** pasta no windows de solução hello e selecione **adicionar pacotes de...**
   
    ![][5]
2. Pesquise Olá **SDK do Microsoft Azure Mobile Engagement Xamarin** e adicioná-lo tooyour solução.  
   
    ![][6]
3. Abra **appdelegate. CS** e adicione o seguinte hello usando a instrução:
   
        using Microsoft.Azure.Engagement.Xamarin;
4. Em Olá **FinishedLaunching** método, adicione Olá após a conexão de saudação tooinitialize com back-end do compromisso de mobilidade. Certifique-se de que tooadd seu **ConnectionString**. Esse código também usa uma cópia **NotificationIcon** que é adicionada por Olá SDK do Mobile Engagement que talvez você queira tooreplace. 
   
        EngagementConfiguration config = new EngagementConfiguration {
                        ConnectionString = "YourConnectionStringFromAzurePortal",
                        NotificationIcon = UIImage.FromBundle("close")
                    };
        EngagementAgent.Init (config);

## <a id="monitor"></a>Habilitar monitoramento em tempo real
Em ordem toostart enviar dados e garantir que os usuários de saudação estão ativos, você deve enviar pelo menos uma tela toohello Mobile Engagement backend.

1. Abra **ViewController.cs** e adicione o seguinte hello usando a instrução:
   
        using Microsoft.Azure.Engagement.Xamarin;
2. Substitua a classe de saudação do qual `ViewController` herda de `UIViewController` muito`EngagementViewController`. 

## <a id="monitor"></a>Conectar o aplicativo com monitoramento em tempo real
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Habilitar notificações por push e mensagens no aplicativo
Mobile Engagement permite toointeract com os usuários e o alcance com notificações por push e no aplicativo mensagens no contexto de saudação de campanhas. Esse módulo é chamado alcance no portal do Mobile Engagement hello.
Olá seções a seguir configurar seu aplicativo tooreceive-los.

### <a name="modify-your-application-delegate"></a>Modifique seu Representante do Aplicativo
1. Olá abrir **appdelegate. CS** e adicione o seguinte hello usando a instrução:
   
        using System; 
2. Agora dentro Olá `FinishedLaunching` método, adicione Olá tooregister para mensagens de envio após a seguir`EngagementAgent.init(...)`
   
        if (UIDevice.CurrentDevice.CheckSystemVersion(8,0))
        {
            var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                (UIUserNotificationType.Badge |
                    UIUserNotificationType.Sound |
                    UIUserNotificationType.Alert),
                null);
            UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications ();
        }
        else
        {
            UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (
                UIRemoteNotificationType.Badge |
                UIRemoteNotificationType.Sound |
                UIRemoteNotificationType.Alert);
        }
3. Por fim - atualizar ou adicionar Olá métodos a seguir:
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, 
            Action<UIBackgroundFetchResult> completionHandler)
        {
            EngagementAgent.ApplicationDidReceiveRemoteNotification(userInfo, completionHandler);
        }
   
        public override void RegisteredForRemoteNotifications (UIApplication application, NSData deviceToken)
        {
            // Register device token on Engagement
            EngagementAgent.RegisterDeviceToken(deviceToken);
        }
   
        public override void FailedToRegisterForRemoteNotifications(UIApplication application, NSError error)
        {
            Console.WriteLine("Failed tooregister for remote notifications: Error '{0}'", error);
        }
4. No seu **Info. plist** na solução de saudação do arquivo, confirme que Olá **identificador de pacote** corresponde à saudação **ID do aplicativo** você tem em seu perfil de provisionamento Olá desenvolvimento da Apple Centro. 
   
    ![][7]
5. Em Olá mesmo **Info. plist** de arquivos, certifique-se de que você verificou Olá **habilitar modos de segundo plano** e **notificações remoto**. 
   
     ![][8]
6. Execute o aplicativo de saudação no dispositivo Olá associada a este perfil de publicação. 

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[1]: ./media/mobile-engagement-xamarin-ios-get-started/new-solution.png
[2]: ./media/mobile-engagement-xamarin-ios-get-started/app-type.png
[3]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-name.png
[4]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-confirm.png
[5]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget.png
[6]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget-azme.png
[7]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-confirm-bundle.png
[8]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-configure-push.png
