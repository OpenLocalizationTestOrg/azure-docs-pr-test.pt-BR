---
title: "aaaAzure Mobile Engagement iOS SDK do procedimento de atualização | Microsoft Docs"
description: "Atualizações e procedimentos mais recentes para o SDK do iOS para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 72a9e493-3f14-4e52-b6e2-0490fd04b184
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 5a81bcaaec72aec665b3334e6400d520454d56a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-procedures"></a>Procedimentos de atualização
Se você já tiver integrado uma versão mais antiga do contrato em seu aplicativo, você tem Olá tooconsider pontos a seguir ao atualizar Olá SDK.

Para cada nova versão do SDK do hello primeiro você deve substituir (remover e importar novamente no xcode) Olá pastas EngagementSDK e EngagementReach.

## <a name="from-300-too400"></a>De 3.0.0 too4.0.0
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

### <a name="usernotifications-framework"></a>Estrutura UserNotifications
Você precisa Olá tooadd `UserNotifications` framework em fases de compilação.

no Explorador de projeto hello, abra o painel de projeto e selecione o destino correto hello. Em seguida, abra Olá **"Fases de compilação"** guia e em Olá **"Binário com bibliotecas de vínculo"** menu, adicionar framework `UserNotifications.framework` -definir Olá link como`Optional`

### <a name="application-push-capability"></a>Capacidade de envio por push do aplicativo
8 XCode pode redefinir seu aplicativo push capacidade,. Verifique novamente em Olá `capability` guia de destino selecionado.

### <a name="add-hello-new-ios-10-notification-registration-code"></a>Adicione código de registro do hello novo iOS notificação 10
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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a>Resolver conflitos de delegado UNUserNotificationCenter

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

## <a name="from-200-too300"></a>De 2.0.0 too3.0.0
Suporte removido para iOS 4.X. A partir do destino de implantação de saudação essa versão do seu aplicativo deve ter pelo menos 6 do iOS.

Se você estiver usando o alcance do seu aplicativo, você deve adicionar `remote-notification` toohello valor `UIBackgroundModes` matriz em seu arquivo Info. plist em notificações remoto de tooreceive de ordem.

Olá método `application:didReceiveRemoteNotification:` precisa toobe substituído por `application:didReceiveRemoteNotification:fetchCompletionHandler:` em seu representante do aplicativo.

"AEPushDelegate.h" foi preterido e interface precisa tooremove todas as referências. Isso inclui a remoção `[[EngagementAgent shared] setPushDelegate:self]` e hello delegar métodos do seu representante do aplicativo:

    -(void)willRetrieveLaunchMessage;
    -(void)didFailToRetrieveLaunchMessage;
    -(void)didReceiveLaunchMessage:(AEPushMessage*)launchMessage;

## <a name="from-1160-too200"></a>De 1.16.0 too2.0.0
Olá a seguir descrevem como toomigrate uma integração SDK da saudação Capptain serviço oferecido pelo Capptain SAS em um aplicativo da plataforma do Azure Mobile Engagement.
Se você estiver migrando de uma versão anterior,. Consulte Olá Capptain site da web toomigrate too1.16 primeiro, em seguida, aplicar Olá procedimento a seguir.

> [!IMPORTANT]
> Capptain e o compromisso de mobilidade não são Olá mesmos serviços e procedimento Olá indicado abaixo só destaca como toomigrate Olá aplicativo cliente. Migrando Olá SDK no aplicativo hello não vai migrar seus dados do hello Capptain toohello Mobile Engagement de servidores
> 
> 

### <a name="agent"></a>Agente
Olá método `registerApp:` foi substituído pelo novo método de saudação `init:`. Seu representante de aplicativo deve ser atualizado de acordo e usar a cadeia de conexão:

            - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
            {
              [...]
              [EngagementAgent init:@"YOUR_CONNECTION_STRING"];
              [...]
            }

Controle de SmartAd foi removido do SDK apenas tiver tooremove todas as instâncias de `AETrackModule` classe

### <a name="class-name-changes"></a>Alterações de nome de classe
Como parte da saudação rebranding, há alguns nomes de classe/arquivos que precisam de toobe alterado.

Todas as classes prefixadas com “CP” foram renomeadas com o prefixo “AE”.

Exemplo:

* `CPModule.h`é renomeado muito`AEModule.h`.

Todas as classes prefixadas com “Capptain” foram renomeadas com o prefixo “Engagement”.

Exemplos:

* Olá classe `CapptainAgent` é renomeado muito`EngagementAgent`.
* Olá classe `CapptainTableViewController` é renomeado muito`EngagementTableViewController`.
* Olá classe `CapptainUtils` é renomeado muito`EngagementUtils`.
* Olá classe `CapptainViewController` é renomeado muito`EngagementViewController`.

