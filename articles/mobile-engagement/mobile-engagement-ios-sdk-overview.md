---
title: "aaaAzure iOS Mobile Engagement visão geral do SDK | Microsoft Docs"
description: "Atualizações e procedimentos mais recentes para o SDK do iOS para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3a03bbd6-bcf8-436c-9775-5a8188629252
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 38f0da2f84df9c62f8fbca233bfda8b9936fdc0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="ios-sdk-for-azure-mobile-engagement"></a>SDK do iOS para o Azure Mobile Engagement
Iniciar aqui tooget todos os detalhes de saudação em como toointegrate do Azure Mobile Engagement em um aplicativo iOS. Se você quiser toogive ele tentar primeiro, verifique se você fazer nossa [tutorial de 15 minutos](mobile-engagement-ios-get-started.md).

Clique em toosee Olá [conteúdo do SDK](mobile-engagement-ios-sdk-content.md)

## <a name="integration-procedures"></a>Procedimentos de integração
1. Comece aqui: [como toointegrate Mobile Engagement em seu aplicativo iOS](mobile-engagement-ios-integrate-engagement.md)
2. Para notificações: [como toointegrate alcance (notificações) em seu aplicativo iOS](mobile-engagement-ios-integrate-engagement-reach.md)
3. Marca o plano de implementação: [como toouse Olá avançado Mobile Engagement marcação API em seu aplicativo iOS](mobile-engagement-ios-use-engagement-api.md)

## <a name="release-notes"></a>Notas de versão
### <a name="410-07172017"></a>4.1.0 (07/17/2017)
* Corrigidas as notificações apagadas na tela de fundo.
* Corrigidos os avisos no XCode 9 sobre as APIs não chamadas na fila principal.
* Corrigida uma perda de memória em pesquisas Reach.
* Removido o suporte para iOS 6.X. A partir do destino de implantação de saudação essa versão do seu aplicativo deve ter pelo menos o iOS 7.

Para a versão anterior, consulte Olá [concluir notas de versão](mobile-engagement-ios-release-notes.md)

## <a name="upgrade-procedures"></a>Procedimentos de atualização
Se você já tiver integrado uma versão mais antiga do contrato em seu aplicativo, você tem Olá tooconsider pontos a seguir ao atualizar Olá SDK.

Você pode ter toofollow vários procedimentos se perdeu várias versões do hello SDK consulte Olá completa [procedimentos de atualização](mobile-engagement-ios-upgrade-procedure.md).

Para cada nova versão do SDK do hello primeiro você deve substituir (remover e importar novamente no xcode) Olá pastas EngagementSDK e EngagementReach.

### <a name="from-300-too400"></a>De 3.0.0 too4.0.0
### <a name="xcode-8"></a>XCode 8
8 XCode é obrigatório a partir da versão 4.0.0 de saudação SDK.

> [!NOTE]
> Se você realmente depende XCode 7, você pode usar o hello [iOS SDK Engagement v3.2.4](https://aka.ms/r6oouh). Há um bug conhecido no módulo de alcance Olá desta versão anterior durante a execução em dispositivos iOS 10: notificações do sistema não são acionadas. toofix isso você terá tooimplement Olá preterido API `application:didReceiveRemoteNotification:` em seu aplicativo delegar da seguinte maneira:
>
>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> **Não recomendamos essa solução alternativa** pois esse comportamento pode alterar qualquer atualização da versão futura iOS (até mesmo pequenas) porque esta API do iOS foi preterida. Você deve alternar tooXCode 8 assim que possível.
>
>

#### <a name="usernotifications-framework"></a>Estrutura UserNotifications
Você precisa Olá tooadd `UserNotifications` framework em fases de compilação.

no Explorador de projeto hello, abra o painel de projeto e selecione o destino correto hello. Em seguida, abra Olá **"Fases de compilação"** guia e em Olá **"Binário com bibliotecas de vínculo"** menu, adicionar framework `UserNotifications.framework` -definir Olá link como`Optional`

#### <a name="application-push-capability"></a>Capacidade de envio por push do aplicativo
8 XCode pode redefinir seu aplicativo push capacidade,. Verifique novamente em Olá `capability` guia de destino selecionado.

#### <a name="add-hello-new-ios-10-notification-registration-code"></a>Adicione código de registro do hello novo iOS notificação 10
Olá antigos código trecho tooregister Olá aplicativo toonotifications ainda funciona, mas está usando preterido APIs durante a execução no iOS 10.

Saudação de importação `User Notification` framework:

        #import <UserNotifications/UserNotifications.h>

No seu método representante do aplicativo `application:didFinishLaunchingWithOptions` , substitua:

        if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
            [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
            [application registerForRemoteNotifications];
        }
        else {

            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }

por:

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

#### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a>Resolver conflitos de delegado UNUserNotificationCenter

*Se o aplicativo nem uma das bibliotecas de terceiros implementar um `UNUserNotificationCenterDelegate`, ignore esta parte.*

Um `UNUserNotificationCenter` delegado é usado pelo ciclo de vida de Olá Olá SDK toomonitor de notificações de compromisso em dispositivos que executam o iOS 10 ou superior. Olá SDK tem sua própria implementação de saudação `UNUserNotificationCenterDelegate` de protocolo, mas pode haver apenas um `UNUserNotificationCenter` delegar por aplicativo. Qualquer outro representante adicionado toohello `UNUserNotificationCenter` objeto está em conflito com hello contrato um. Se Olá SDK detectar delegado do seu ou qualquer outra parte, em seguida, ele não usará sua própria implementação toogive você tooresolve uma chance Olá conflitos. Você terá tooadd Olá contrato lógica tooyour possui delegado em ordem tooresolve conflitos de saudação.

Há dois tooachieve de maneiras isso.

Proposta 1, encaminhando o delegado chama toohello SDK:

    #import <UIKit/UIKit.h>
    #import "EngagementAgent.h"
    #import <UserNotifications/UserNotifications.h>


    @interface MyAppDelegate : NSObject <UIApplicationDelegate, UNUserNotificationCenterDelegate>
    @end

    @implementation MyAppDelegate

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterWillPresentNotification:notification withCompletionHandler:completionHandler]
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterDidReceiveNotificationResponse:response withCompletionHandler:completionHandler]
    }
    @end

Ou proposta 2, herdando de saudação `AEUserNotificationHandler` classe

    #import "AEUserNotificationHandler.h"
    #import "EngagementAgent.h"

    @interface CustomUserNotificationHandler :AEUserNotificationHandler
    @end

    @implementation CustomUserNotificationHandler

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center willPresentNotification:notification withCompletionHandler:completionHandler];
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse: UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center didReceiveNotificationResponse:response withCompletionHandler:completionHandler];
    }

    @end

> [!NOTE]
> Você pode determinar se uma notificação de contrato ou não passando seus `userInfo` toohello dicionário agente `isEngagementPushPayload:` método de classe.

Certifique-se de que Olá `UNUserNotificationCenter` representante do objeto é definido tooyour delegado em qualquer Olá `application:willFinishLaunchingWithOptions:` ou hello `application:didFinishLaunchingWithOptions:` método do seu representante de aplicativo.
Por exemplo, se você tiver implementado Olá acima proposta 1:

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }
