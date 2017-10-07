---
title: aaaGet iniciado com o Azure Mobile Engagement para iOS em Objective C | Microsoft Docs
description: "Saiba como toouse do Azure Mobile Engagement com notificações de análise e enviar por push para aplicativos iOS."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 117b5742-522b-41de-98c5-f432da2d98f8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 51a5013f23d2d04a7b9b30c83b47017898b2bb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-objective-c"></a>Introdução ao Azure Mobile Engagement para aplicativos iOS em Objective C
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Este tópico mostra como toouse do Azure Mobile Engagement toounderstand seu uso do aplicativo e enviar por push o aplicativo do iOS notificações toosegmented usuários tooan.
Neste tutorial, você cria um aplicativo iOS em branco que coleta dados básicos e recebe notificações por push usando o Sistema de Notificação por Push da Apple (APNS).

Este tutorial requer o seguinte hello:

* XCode 8, que pode ser instalado a partir da MAC App Store
* Olá [SDK do Mobile Engagement iOS]

A conclusão desse tutorial é um pré-requisito para todos os outros tutoriais do Mobile Engagement para os aplicativos iOS.

> [!NOTE]
> toocomplete neste tutorial, você deve ter uma conta ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).
>
>

## <a id="setup-azme"></a>Configurar o Mobile Engagement para seu aplicativo iOS
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Conectar seu back-end do aplicativo toohello Mobile Engagement
Este tutorial apresenta uma "integração básica", que é Olá mínimo definido toocollect necessários dados e envia uma notificação por push. documentação de integração completa Olá pode ser encontrada no hello [integração do SDK do Mobile Engagement iOS](mobile-engagement-ios-sdk-overview.md)

Vamos criar um aplicativo básico com a integração do XCode toodemonstrate hello.

### <a name="create-a-new-ios-project"></a>Crie um novo projeto iOS
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a>Conectar seu back-end do aplicativo toohello Mobile Engagement
1. Baixar Olá [SDK do Mobile Engagement iOS].
2. Extrair hello. gz arquivo tooa pasta no seu computador.
3. Clique com botão direito hello e, em seguida, selecione **adicionar arquivos ao**.

    ![][1]
4. Navegue toohello pasta onde você extraiu Olá SDK, selecione Olá `EngagementSDK` pasta, clique em **opções** na Olá canto inferior esquerdo e verifique se essa caixa de seleção Olá **copiar itens se necessário** e hello caixa de seleção para o seu destino são verificados e pressione **Okey**.

    ![][2]
5. Olá abrir **fases de compilação** guia e em hello **Link binário com bibliotecas** menu Adicionar estruturas de hello, conforme mostrado abaixo:

    ![][3]
6. Voltar toohello portal do Azure em seu aplicativo **informações de Conexão** página e copie a cadeia de conexão hello.

    ![][4]
7. Adicionar Olá a seguinte linha de código no seu **appdelegate. M** arquivo.

        #import "EngagementAgent.h"
8. Agora cole a cadeia de caracteres de conexão de saudação em Olá `didFinishLaunchingWithOptions` delegate.

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
              [...]   
              [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
              [...]
        }
9. `setTestLogEnabled`é uma instrução opcional que permite que os logs do SDK para você tooidentify problemas.

## <a id="monitor"></a>Habilitar monitoramento em tempo real
Em ordem toostart enviar dados e garantir que os usuários de saudação estão ativos, você deve enviar pelo menos uma tela (atividade) toohello Mobile Engagement backend.

1. Olá abrir **ViewController.h** de arquivo e importar **EngagementViewController.h**:

    `#import "EngagementViewController.h"`
2. Agora substitua superclasse Olá de saudação **ViewController** interface por `EngagementViewController`:

    `@interface ViewController : EngagementViewController`

## <a id="monitor"></a>Conectar o aplicativo com monitoramento em tempo real
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Habilitar notificações por push e mensagens no aplicativo
Mobile Engagement permite toointeract com os usuários e o alcance com notificações por push e no aplicativo mensagens no contexto de saudação de campanhas. Esse módulo é chamado alcance no portal do Mobile Engagement hello.
Olá seções a seguir configurar seu aplicativo tooreceive-los.

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>Habilitar seu aplicativo tooreceive silenciosa notificações por Push
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a>Adicionar Olá alcance biblioteca tooyour projeto
1. Clique com o botão direito em seu projeto.
2. Selecione **Adicionar arquivo a**.
3. Navegue toohello pasta onde você extraiu Olá SDK.
4. Selecione Olá `EngagementReach` pasta.
5. Clique em **Adicionar**.

### <a name="modify-your-application-delegate"></a>Modifique seu Representante do Aplicativo
1. Em **AppDeletegate.m** de arquivos, importar Olá contrato alcançar módulo.

        #import "AEReachModule.h"
        #import <UserNotifications/UserNotifications.h>
2. Olá interna `application:didFinishLaunchingWithOptions` método, crie um módulo de alcance e passá-lo tooyour linha de inicialização contrato existente:

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
            AEReachModule * reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
            [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
            [...]
            return YES;
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a>Habilitar seu aplicativo tooreceive notificações por Push do APNS
1. Adicionar Olá toohello linha a seguir `application:didFinishLaunchingWithOptions` método:

        if (NSFoundationVersionNumber >= NSFoundationVersionNumber_iOS_8_0)
        {
            if (NSFoundationVersionNumber > NSFoundationVersionNumber_iOS_9_x_Max)
            {
                [UNUserNotificationCenter.currentNotificationCenter requestAuthorizationWithOptions:(UNAuthorizationOptionBadge | UNAuthorizationOptionSound | UNAuthorizationOptionAlert) completionHandler:^(BOOL granted, NSError * _Nullable error) {}];
            }else
            {
                [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)   categories:nil]];
            }
            [application registerForRemoteNotifications];
        }
        else
        {
            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }
2. Adicionar Olá `application:didRegisterForRemoteNotificationsWithDeviceToken` método da seguinte maneira:

        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
        {
             [[EngagementAgent shared] registerDeviceToken:deviceToken];
            NSLog(@"Registered Token: %@", deviceToken);
        }
3. Adicionar Olá `didFailToRegisterForRemoteNotificationsWithError` método da seguinte maneira:

        - (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error
        {
           NSLog(@"Failed tooget token, error: %@", error);
        }
4. Adicionar Olá `didReceiveRemoteNotification:fetchCompletionHandler` método da seguinte maneira:

        - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
        {
            [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[SDK do Mobile Engagement iOS]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
