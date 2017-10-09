---
title: "aaaAzure Mobile Engagement iOS SDK alcançar integração | Microsoft Docs"
description: "Atualizações e procedimentos mais recentes para o SDK do iOS para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1f5f5857-867c-40c5-9d76-675a343a0296
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 40c9bfbdb475ab0b97bdbc9cea798a59cb8a71ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-ios"></a><span data-ttu-id="91a37-103">Como tooIntegrate contrato alcançam no iOS</span><span class="sxs-lookup"><span data-stu-id="91a37-103">How tooIntegrate Engagement Reach on iOS</span></span>
<span data-ttu-id="91a37-104">Você deve seguir Olá integração procedimento descrito em Olá [como tooIntegrate contrato no documento de iOS](mobile-engagement-ios-integrate-engagement.md) antes de seguir este guia.</span><span class="sxs-lookup"><span data-stu-id="91a37-104">You must follow hello integration procedure described in hello [How tooIntegrate Engagement on iOS document](mobile-engagement-ios-integrate-engagement.md) before following this guide.</span></span>

<span data-ttu-id="91a37-105">Esta documentação requer o XCode 8.</span><span class="sxs-lookup"><span data-stu-id="91a37-105">This documentation requires XCode 8.</span></span> <span data-ttu-id="91a37-106">Se você realmente depende XCode 7, você pode usar o hello [iOS SDK Engagement v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="91a37-106">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="91a37-107">Há um bug conhecido nesta versão anterior durante a execução em dispositivos com iOS 10: as notificações de sistema não são acionadas.</span><span class="sxs-lookup"><span data-stu-id="91a37-107">There is a known bug on this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="91a37-108">toofix isso você terá tooimplement Olá preterido API `application:didReceiveRemoteNotification:` em seu aplicativo delegar da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="91a37-108">toofix this you will have tooimplement hello deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="91a37-109">**Não recomendamos essa solução alternativa** pois esse comportamento pode alterar qualquer atualização da versão futura iOS (até mesmo pequenas) porque esta API do iOS foi preterida.</span><span class="sxs-lookup"><span data-stu-id="91a37-109">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="91a37-110">Você deve alternar tooXCode 8 assim que possível.</span><span class="sxs-lookup"><span data-stu-id="91a37-110">You should switch tooXCode 8 as soon as possible.</span></span>
>
>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="91a37-111">Habilitar seu aplicativo tooreceive silenciosa notificações por Push</span><span class="sxs-lookup"><span data-stu-id="91a37-111">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

## <a name="integration-steps"></a><span data-ttu-id="91a37-112">Etapas de integração</span><span class="sxs-lookup"><span data-stu-id="91a37-112">Integration steps</span></span>
### <a name="embed-hello-engagement-reach-sdk-into-your-ios-project"></a><span data-ttu-id="91a37-113">Inserir saudação SDK do Reach contrato em seu projeto do iOS</span><span class="sxs-lookup"><span data-stu-id="91a37-113">Embed hello Engagement Reach SDK into your iOS project</span></span>
* <span data-ttu-id="91a37-114">Adicione o sdk de alcance Olá no seu projeto Xcode.</span><span class="sxs-lookup"><span data-stu-id="91a37-114">Add hello Reach sdk in your Xcode project.</span></span> <span data-ttu-id="91a37-115">No Xcode, vá muito**projeto \> adicionar tooproject** e escolha Olá `EngagementReach` pasta.</span><span class="sxs-lookup"><span data-stu-id="91a37-115">In Xcode, go too**Project \> Add tooproject** and choose hello `EngagementReach` folder.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="91a37-116">Modifique seu Representante do Aplicativo</span><span class="sxs-lookup"><span data-stu-id="91a37-116">Modify your Application Delegate</span></span>
* <span data-ttu-id="91a37-117">Na parte superior de saudação do seu arquivo de implementação, importe o módulo de alcance do contrato de hello:</span><span class="sxs-lookup"><span data-stu-id="91a37-117">At hello top of your implementation file, import hello Engagement Reach module:</span></span>

      [...]
      #import "AEReachModule.h"
* <span data-ttu-id="91a37-118">No método `applicationDidFinishLaunching:` ou `application:didFinishLaunchingWithOptions:`, crie um módulo de alcance e passá-lo tooyour linha de inicialização contrato existente:</span><span class="sxs-lookup"><span data-stu-id="91a37-118">Inside method `applicationDidFinishLaunching:` or `application:didFinishLaunchingWithOptions:`, create a reach module and pass it tooyour existing Engagement initialization line:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
        [...]

        return YES;
      }
* <span data-ttu-id="91a37-119">Modificar **'icon.png'** cadeia de caracteres com o nome da imagem Olá desejado como o ícone de notificação.</span><span class="sxs-lookup"><span data-stu-id="91a37-119">Modify **'icon.png'** string with hello image name you want as your notification icon.</span></span>
* <span data-ttu-id="91a37-120">Se você quiser toouse Olá opção *valor de notificação de atualização* em campanhas de alcance ou se você quiser que o push nativo toouse \<API/campanha de SaaS/alcance formato/nativo Push\> campanhas, você deve permitir que o módulo de alcance Olá gerenciar Olá ícone de notificação em si (ele será limpa automaticamente a notificação de aplicativo hello e também redefinir o valor de saudação armazenado pelo contrato sempre que o aplicativo hello é iniciado ou foregrounded).</span><span class="sxs-lookup"><span data-stu-id="91a37-120">If you want toouse hello option *Update badge value* in Reach campaigns or if you want toouse native push \</SaaS/Reach API/Campaign format/Native Push\> campaigns, you must let hello Reach module manage hello badge icon itself (it will automatically clear hello application badge and also reset hello value stored by Engagement every time hello application is started or foregrounded).</span></span> <span data-ttu-id="91a37-121">Isso é feito adicionando Olá seguinte linha após a inicialização do módulo de alcance:</span><span class="sxs-lookup"><span data-stu-id="91a37-121">This is done by adding hello following line after Reach module initialization:</span></span>

      [reach setAutoBadgeEnabled:YES];
* <span data-ttu-id="91a37-122">Se você quiser toohandle alcance dados por push, você deverá permitir que seu representante do aplicativo está de acordo com toohello `AEReachDataPushDelegate` protocolo.</span><span class="sxs-lookup"><span data-stu-id="91a37-122">If you want toohandle Reach data push, you must let your Application delegate conform toohello `AEReachDataPushDelegate` protocol.</span></span> <span data-ttu-id="91a37-123">Adicione Olá seguinte linha após a inicialização do módulo de alcance:</span><span class="sxs-lookup"><span data-stu-id="91a37-123">Add hello following line after Reach module initialization:</span></span>

      [reach setDataPushDelegate:self];
* <span data-ttu-id="91a37-124">Em seguida, você pode implementar métodos Olá `onDataPushStringReceived:` e `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` em seu representante do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="91a37-124">Then you can implement hello methods `onDataPushStringReceived:` and `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` in your application delegate:</span></span>

      -(BOOL)didReceiveStringDataPushWithCategory:(NSString*)category body:(NSString*)body
      {
         NSLog(@"String data push message with category <%@> received: %@", category, body);
         return YES;
      }

      -(BOOL)didReceiveBase64DataPushWithCategory:(NSString*)category decodedBody:(NSData *)decodedBody encodedBody:(NSString *)encodedBody
      {
         NSLog(@"Base64 data push message with category <%@> received: %@", category, encodedBody);
         // Do something useful with decodedBody like updating an image view
         return YES;
      }

### <a name="category"></a><span data-ttu-id="91a37-125">Categoria</span><span class="sxs-lookup"><span data-stu-id="91a37-125">Category</span></span>
<span data-ttu-id="91a37-126">o parâmetro de categoria Olá é opcional quando você criar uma campanha de envio de dados e permite que você toofilter dados envia.</span><span class="sxs-lookup"><span data-stu-id="91a37-126">hello category parameter is optional when you create a Data Push campaign and allows you toofilter data pushes.</span></span> <span data-ttu-id="91a37-127">Isso é útil se você quiser toopush diferentes tipos de `Base64` tooidentify de dados e desejar que seu tipo antes da análise-los.</span><span class="sxs-lookup"><span data-stu-id="91a37-127">This is useful if you want toopush different kinds of `Base64` data and want tooidentify their type before parsing them.</span></span>

<span data-ttu-id="91a37-128">**Seu aplicativo está agora pronto tooreceive e exibição acessar conteúdo!**</span><span class="sxs-lookup"><span data-stu-id="91a37-128">**Your application is now ready tooreceive and display reach contents!**</span></span>

## <a name="how-tooreceive-announcements-and-polls-at-any-time"></a><span data-ttu-id="91a37-129">Como tooreceive anúncios e controla a qualquer momento</span><span class="sxs-lookup"><span data-stu-id="91a37-129">How tooreceive announcements and polls at any time</span></span>
<span data-ttu-id="91a37-130">Contrato pode enviar notificações de alcançar os usuários finais de tooyour a qualquer momento usando Olá Apple Push Notification Service.</span><span class="sxs-lookup"><span data-stu-id="91a37-130">Engagement can send Reach notifications tooyour end users at any time by using hello Apple Push Notification Service.</span></span>

<span data-ttu-id="91a37-131">tooenable essa funcionalidade, será tooprepare seu aplicativo para notificações de push da Apple e modificar seu representante do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91a37-131">tooenable this functionality, you'll have tooprepare your application for Apple push notifications and modify your application delegate.</span></span>

### <a name="prepare-your-application-for-apple-push-notifications"></a><span data-ttu-id="91a37-132">Preparar seu aplicativo para notificações de push da Apple</span><span class="sxs-lookup"><span data-stu-id="91a37-132">Prepare your application for Apple push notifications</span></span>
<span data-ttu-id="91a37-133">Siga o guia de saudação: [como tooPrepare seu aplicativo para notificações de Push da Apple](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span><span class="sxs-lookup"><span data-stu-id="91a37-133">Please follow hello guide : [How tooPrepare your Application for Apple Push Notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

### <a name="add-hello-necessary-client-code"></a><span data-ttu-id="91a37-134">Adicione código de cliente necessário Olá</span><span class="sxs-lookup"><span data-stu-id="91a37-134">Add hello necessary client code</span></span>
<span data-ttu-id="91a37-135">*Agora seu aplicativo deve ter um certificado do Apple push registrado no front-end Olá contrato.*</span><span class="sxs-lookup"><span data-stu-id="91a37-135">*At this point your application should have a registered Apple push certificate in hello Engagement frontend.*</span></span>

<span data-ttu-id="91a37-136">Se ele não ainda tiver feito isso, você precisa tooregister suas notificações de push de tooreceive do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91a37-136">If it's not done already, you need tooregister your application tooreceive push notifications.</span></span>

* <span data-ttu-id="91a37-137">Saudação de importação `User Notification` framework:</span><span class="sxs-lookup"><span data-stu-id="91a37-137">Import hello `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h>
* <span data-ttu-id="91a37-138">Adicionar Olá linha a seguir na inicialização do aplicativo (normalmente em `application:didFinishLaunchingWithOptions:`):</span><span class="sxs-lookup"><span data-stu-id="91a37-138">Add hello following line when your application starts (typically in `application:didFinishLaunchingWithOptions:`):</span></span>

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

<span data-ttu-id="91a37-139">Em seguida, você precisa de token do dispositivo tooprovide tooEngagement hello retornada pelos servidores da Apple.</span><span class="sxs-lookup"><span data-stu-id="91a37-139">Then, You need tooprovide tooEngagement hello device token returned by Apple servers.</span></span> <span data-ttu-id="91a37-140">Isso é feito no método hello chamado `application:didRegisterForRemoteNotificationsWithDeviceToken:` em seu representante do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="91a37-140">This is done in hello method named `application:didRegisterForRemoteNotificationsWithDeviceToken:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
        [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

<span data-ttu-id="91a37-141">Por fim, você tem tooinform Olá SDK Engagement quando seu aplicativo recebe uma notificação remota.</span><span class="sxs-lookup"><span data-stu-id="91a37-141">Finally, you have tooinform hello Engagement SDK when your application receives a remote notification.</span></span> <span data-ttu-id="91a37-142">toodo que chamam Olá método `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` em seu representante do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="91a37-142">toodo that, call hello method `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didReceiveRemoteNotification:(NSDictionary*)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

> [!IMPORTANT]
> <span data-ttu-id="91a37-143">Por padrão, o contrato alcançar controles completionHandler hello.</span><span class="sxs-lookup"><span data-stu-id="91a37-143">By default, Engagement Reach controls hello completionHandler.</span></span> <span data-ttu-id="91a37-144">Se você quiser toomanually responder toohello `handler` bloco no seu código, você pode passar nulo para Olá `handler` argumento e controle de conclusão de saudação bloquear por conta própria.</span><span class="sxs-lookup"><span data-stu-id="91a37-144">If you want toomanually respond toohello `handler` block in your code, you can pass nil for hello `handler` argument and control hello completion block yourself.</span></span> <span data-ttu-id="91a37-145">Consulte Olá `UIBackgroundFetchResult` tipo para obter uma lista de valores possíveis.</span><span class="sxs-lookup"><span data-stu-id="91a37-145">See hello `UIBackgroundFetchResult` type for a list of possible values.</span></span>
>
>

### <a name="full-example"></a><span data-ttu-id="91a37-146">Exemplo completo</span><span class="sxs-lookup"><span data-stu-id="91a37-146">Full example</span></span>
<span data-ttu-id="91a37-147">Aqui está um exemplo completo de integração:</span><span class="sxs-lookup"><span data-stu-id="91a37-147">Here is a full example of integration:</span></span>

    #pragma mark -
    #pragma mark Application lifecycle

    - (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions
    {
      /* Reach module */
      AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
      [reach setAutoBadgeEnabled:YES];

      /* Engagement initialization */
      [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
      [[EngagementAgent shared] setPushDelegate:self];

      /* Views */
      [window addSubview:[tabBarController view]];
      [window makeKeyAndVisible];

      [application registerForRemoteNotificationTypes:UIRemoteNotificationTypeAlert|UIRemoteNotificationTypeBadge|UIRemoteNotificationTypeSound];
      return YES;
    }

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
      [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

    - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="91a37-148">Resolver conflitos de delegado UNUserNotificationCenter</span><span class="sxs-lookup"><span data-stu-id="91a37-148">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="91a37-149">*Se o aplicativo nem uma das bibliotecas de terceiros implementar um `UNUserNotificationCenterDelegate`, ignore esta parte.*</span><span class="sxs-lookup"><span data-stu-id="91a37-149">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="91a37-150">Um `UNUserNotificationCenter` delegado é usado pelo ciclo de vida de Olá Olá SDK toomonitor de notificações de compromisso em dispositivos que executam o iOS 10 ou superior.</span><span class="sxs-lookup"><span data-stu-id="91a37-150">A `UNUserNotificationCenter` delegate is used by hello SDK toomonitor hello life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="91a37-151">Olá SDK tem sua própria implementação de saudação `UNUserNotificationCenterDelegate` de protocolo, mas pode haver apenas um `UNUserNotificationCenter` delegar por aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91a37-151">hello SDK has its own implementation of hello `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="91a37-152">Qualquer outro representante adicionado toohello `UNUserNotificationCenter` objeto está em conflito com hello contrato um.</span><span class="sxs-lookup"><span data-stu-id="91a37-152">Any other delegate added toohello `UNUserNotificationCenter` object will conflict with hello Engagement one.</span></span> <span data-ttu-id="91a37-153">Se Olá SDK detectar delegado do seu ou qualquer outra parte, em seguida, ele não usará sua própria implementação toogive você tooresolve uma chance Olá conflitos.</span><span class="sxs-lookup"><span data-stu-id="91a37-153">If hello SDK detects your or any other third party's delegate then it will not use its own implementation toogive you a chance tooresolve hello conflicts.</span></span> <span data-ttu-id="91a37-154">Você terá tooadd Olá contrato lógica tooyour possui delegado em ordem tooresolve conflitos de saudação.</span><span class="sxs-lookup"><span data-stu-id="91a37-154">You will have tooadd hello Engagement logic tooyour own delegate in order tooresolve hello conflicts.</span></span>

<span data-ttu-id="91a37-155">Há dois tooachieve de maneiras isso.</span><span class="sxs-lookup"><span data-stu-id="91a37-155">There are two ways tooachieve this.</span></span>

<span data-ttu-id="91a37-156">Proposta 1, encaminhando o delegado chama toohello SDK:</span><span class="sxs-lookup"><span data-stu-id="91a37-156">Proposal 1, simply by forwarding your delegate calls toohello SDK:</span></span>

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

<span data-ttu-id="91a37-157">Ou proposta 2, herdando de saudação `AEUserNotificationHandler` classe</span><span class="sxs-lookup"><span data-stu-id="91a37-157">Or proposal 2, by inheriting from hello `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="91a37-158">Você pode determinar se uma notificação de contrato ou não passando seus `userInfo` toohello dicionário agente `isEngagementPushPayload:` método de classe.</span><span class="sxs-lookup"><span data-stu-id="91a37-158">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary toohello Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="91a37-159">Certifique-se de que Olá `UNUserNotificationCenter` representante do objeto é definido tooyour delegado em qualquer Olá `application:willFinishLaunchingWithOptions:` ou hello `application:didFinishLaunchingWithOptions:` método do seu representante de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91a37-159">Make sure that hello `UNUserNotificationCenter` object's delegate is set tooyour delegate within either hello `application:willFinishLaunchingWithOptions:` or hello `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="91a37-160">Por exemplo, se você tiver implementado Olá acima proposta 1:</span><span class="sxs-lookup"><span data-stu-id="91a37-160">For instance, if you implemented hello above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="how-toocustomize-campaigns"></a><span data-ttu-id="91a37-161">Como campanhas toocustomize</span><span class="sxs-lookup"><span data-stu-id="91a37-161">How toocustomize campaigns</span></span>
### <a name="notifications"></a><span data-ttu-id="91a37-162">Notificações</span><span class="sxs-lookup"><span data-stu-id="91a37-162">Notifications</span></span>
<span data-ttu-id="91a37-163">Há dois tipos de notificações: notificações de sistema e no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91a37-163">There are two types of notifications: system and in-app notifications.</span></span>

<span data-ttu-id="91a37-164">As notificações do sistema são tratadas pelo iOS e não podem ser personalizadas.</span><span class="sxs-lookup"><span data-stu-id="91a37-164">System notifications are handled by iOS, and cannot be customized.</span></span>

<span data-ttu-id="91a37-165">Notificações no aplicativo são feitas de um modo de exibição que é adicionado dinamicamente toohello janela atual do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91a37-165">In-app notifications are made of a view that is dynamically added toohello current application window.</span></span> <span data-ttu-id="91a37-166">Isso é chamado uma sobreposição de notificação.</span><span class="sxs-lookup"><span data-stu-id="91a37-166">This is called a notification overlay.</span></span> <span data-ttu-id="91a37-167">Sobreposições de notificação são ótimas para uma integração rápida porque eles não requerem que você toomodify qualquer exibição em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91a37-167">Notification overlays are great for a fast integration because they does not require you toomodify any view in your application.</span></span>

#### <a name="layout"></a><span data-ttu-id="91a37-168">Layout</span><span class="sxs-lookup"><span data-stu-id="91a37-168">Layout</span></span>
<span data-ttu-id="91a37-169">aparência de saudação toomodify das suas notificações no aplicativo, você pode modificar simplesmente arquivo hello `AENotificationView.xib` tooyour precisa, como manter valores de marca hello e tipos de sub-visualizações existente hello.</span><span class="sxs-lookup"><span data-stu-id="91a37-169">toomodify hello look of your in-app notifications, you can simply modify hello file `AENotificationView.xib` tooyour needs, as long as you keep hello tag values and types of hello existing subviews.</span></span>

<span data-ttu-id="91a37-170">Por padrão, as notificações no aplicativo são apresentadas na parte inferior da saudação da tela hello.</span><span class="sxs-lookup"><span data-stu-id="91a37-170">By default, in-app notifications are presented at hello bottom of hello screen.</span></span> <span data-ttu-id="91a37-171">Se você preferir toodisplay-los na parte superior de saudação da tela, editar Olá fornecido `AENotificationView.xib` e alterar Olá `AutoSizing` propriedade do modo de exibição de saudação principal para que ele pode ser mantido na parte superior de saudação da sua visão ampla do.</span><span class="sxs-lookup"><span data-stu-id="91a37-171">If you prefer toodisplay them at hello top of screen, edit hello provided `AENotificationView.xib` and change hello `AutoSizing` property of hello main view so it can be kept at hello top of its superview.</span></span>

#### <a name="categories"></a><span data-ttu-id="91a37-172">Categorias</span><span class="sxs-lookup"><span data-stu-id="91a37-172">Categories</span></span>
<span data-ttu-id="91a37-173">Quando você modifica Olá fornecido layout, você modificar a aparência de saudação de todas as notificações.</span><span class="sxs-lookup"><span data-stu-id="91a37-173">When you modify hello provided layout, you modify hello look of all your notifications.</span></span> <span data-ttu-id="91a37-174">As categorias permitem que toodefine que vários direcionados parece (possivelmente comportamentos) para notificações.</span><span class="sxs-lookup"><span data-stu-id="91a37-174">Categories allow you toodefine various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="91a37-175">Uma categoria pode ser especificada quando você cria uma campanha de Reach.</span><span class="sxs-lookup"><span data-stu-id="91a37-175">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="91a37-176">Tenha em mente que categorias também permitem personalizar anúncios e pesquisas, como está descrito mais adiante neste documento.</span><span class="sxs-lookup"><span data-stu-id="91a37-176">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="91a37-177">tooregister um manipulador de categoria para as notificações, você precisa tooadd uma chamada quando Olá alcançar o módulo é inicializada.</span><span class="sxs-lookup"><span data-stu-id="91a37-177">tooregister a category handler for your notifications, you need tooadd a call once hello reach module is initialized.</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:@"my_category"];
    ...

<span data-ttu-id="91a37-178">`myNotifier`deve ser uma instância de um objeto que está em conformidade com o protocolo toohello `AENotifier`.</span><span class="sxs-lookup"><span data-stu-id="91a37-178">`myNotifier` must be an instance of an object that conforms toohello protocol `AENotifier`.</span></span>

<span data-ttu-id="91a37-179">Você pode implementar métodos de protocolo hello sozinho ou você pode escolher uma classe existente de saudação tooreimplement `AEDefaultNotifier` que já executa a maioria do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="91a37-179">You can implement hello protocol methods by yourself or you can choose tooreimplement hello existing class `AEDefaultNotifier` which already performs most of hello work.</span></span>

<span data-ttu-id="91a37-180">Por exemplo, se você quiser tooredefine exibição de notificação de saudação para uma categoria específica, você pode seguir este exemplo:</span><span class="sxs-lookup"><span data-stu-id="91a37-180">For example, if you want tooredefine hello notification view for a specific category, you can follow this example:</span></span>

    #import "AEDefaultNotifier.h"
    #import "AENotificationView.h"
    @interface MyNotifier : AEDefaultNotifier
    @end

    @implementation MyNotifier

    -(NSString*)nibNameForCategory:(NSString*)category
    {
      return "MyNotificationView";
    }

    @end

<span data-ttu-id="91a37-181">Esse exemplo simples de categoria pressupõem que você tenha um arquivo chamado `MyNotificationView.xib` no pacote de aplicativo principal.</span><span class="sxs-lookup"><span data-stu-id="91a37-181">This simple example of category assume that you have a file named `MyNotificationView.xib` in your main application bundle.</span></span> <span data-ttu-id="91a37-182">Se o método hello não é capaz de toofind correspondente `.xib`, notificação de saudação não será exibida e contrato produzirá uma mensagem no console de saudação.</span><span class="sxs-lookup"><span data-stu-id="91a37-182">If hello method is not able toofind a corresponding `.xib`, hello notification will not be displayed and Engagement will output a message in hello console.</span></span>

<span data-ttu-id="91a37-183">Olá fornecido nib arquivo deve respeitar Olá regras a seguir:</span><span class="sxs-lookup"><span data-stu-id="91a37-183">hello provided nib file should respect hello following rules:</span></span>

* <span data-ttu-id="91a37-184">Ele deve conter apenas um modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="91a37-184">It should only contain one view.</span></span>
* <span data-ttu-id="91a37-185">Sub-visualizações devem ser de saudação mesmo tipos como Olá aquelas dentro Olá fornecido nib arquivo chamado`AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="91a37-185">Subviews should be of hello same types as hello ones inside hello provided nib file named `AENotificationView.xib`</span></span>
* <span data-ttu-id="91a37-186">Sub-visualizações devem ter Olá mesmo marcas como Olá aquelas dentro Olá fornecido nib arquivo chamado`AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="91a37-186">Subviews should have hello same tags as hello ones inside hello provided nib file named `AENotificationView.xib`</span></span>

> [!TIP]
> <span data-ttu-id="91a37-187">Apenas copie o arquivo de ponta de Olá fornecido, denominado `AENotificationView.xib`e começar a trabalhar a partir daí.</span><span class="sxs-lookup"><span data-stu-id="91a37-187">Just copy hello provided nib file, named `AENotificationView.xib`, and start working from there.</span></span> <span data-ttu-id="91a37-188">Mas tenha cuidado, Olá exibição dentro desse arquivo nib é associada a classe toohello `AENotificationView`.</span><span class="sxs-lookup"><span data-stu-id="91a37-188">But be careful, hello view inside this nib file is associated toohello class `AENotificationView`.</span></span> <span data-ttu-id="91a37-189">Essa classe redefinido método hello `layoutSubViews` toomove e redimensione seus sub-visualizações toocontext de acordo com.</span><span class="sxs-lookup"><span data-stu-id="91a37-189">This class redefined hello method `layoutSubViews` toomove and resize its subviews according toocontext.</span></span> <span data-ttu-id="91a37-190">Talvez você queira tooreplace-lo com um `UIView` ou classe do modo de exibição personalizado.</span><span class="sxs-lookup"><span data-stu-id="91a37-190">You may want tooreplace it with an `UIView` or you custom view class.</span></span>
>
>

<span data-ttu-id="91a37-191">Se você precisar de personalização mais profunda das suas notificações (se você desejar para a instância tooload sua exibição diretamente no código de saudação), é recomendável tootake examinar Olá fornecida documentação de código e a classe de origem de `Protocol ReferencesDefaultNotifier` e `AENotifier`.</span><span class="sxs-lookup"><span data-stu-id="91a37-191">If you need deeper customization of your notifications(if you want for instance tooload your view directly from hello code), it is recommended tootake a look at hello provided source code and class documentation of `Protocol ReferencesDefaultNotifier` and `AENotifier`.</span></span>

<span data-ttu-id="91a37-192">Observe que você pode usar Olá Notificador mesmo para várias categorias.</span><span class="sxs-lookup"><span data-stu-id="91a37-192">Note that you can use hello same notifier for multiple categories.</span></span>

<span data-ttu-id="91a37-193">Você pode Notificador de padrão de saudação também redefinido como este:</span><span class="sxs-lookup"><span data-stu-id="91a37-193">You can also redefined hello default notifier like this:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:kAEReachDefaultCategory];

##### <a name="notification-handling"></a><span data-ttu-id="91a37-194">Tratamento de notificação</span><span class="sxs-lookup"><span data-stu-id="91a37-194">Notification handling</span></span>
<span data-ttu-id="91a37-195">Ao usar a categoria de padrão de saudação, alguns métodos de ciclo de vida são chamados em Olá `AEReachContent` tooreport estatísticas e atualização Olá campanha o estado do objeto:</span><span class="sxs-lookup"><span data-stu-id="91a37-195">When using hello default category, some life cycle methods are called on hello `AEReachContent` object tooreport statistics and update hello campaign state:</span></span>

* <span data-ttu-id="91a37-196">Quando a notificação de saudação é exibida no aplicativo, Olá `displayNotification` método é chamado (que relata estatísticas) por `AEReachModule` se `handleNotification:` retorna `YES`.</span><span class="sxs-lookup"><span data-stu-id="91a37-196">When hello notification is displayed in application, hello `displayNotification` method is called (which reports statistics) by `AEReachModule` if `handleNotification:` returns `YES`.</span></span>
* <span data-ttu-id="91a37-197">Se a notificação de saudação é ignorada, Olá `exitNotification` método é chamado, a estatística é relatada e campanhas Avançar agora podem ser processadas.</span><span class="sxs-lookup"><span data-stu-id="91a37-197">If hello notification is dismissed, hello `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="91a37-198">Se a notificação de saudação é clicada, `actionNotification` é chamado, a estatística é relatada e Olá associado ação é executada.</span><span class="sxs-lookup"><span data-stu-id="91a37-198">If hello notification is clicked, `actionNotification` is called, statistic is reported and hello associated action is performed.</span></span>

<span data-ttu-id="91a37-199">Se sua implementação de `AENotifier` bypasses Olá comportamento padrão, você terá que toocall esses métodos de ciclo de vida por si mesmo.</span><span class="sxs-lookup"><span data-stu-id="91a37-199">If your implementation of `AENotifier` bypasses hello default behavior, you have toocall these life cycle methods by yourself.</span></span> <span data-ttu-id="91a37-200">Olá exemplos a seguir ilustra alguns casos em que o comportamento padrão de saudação é ignorado:</span><span class="sxs-lookup"><span data-stu-id="91a37-200">hello following examples illustrate some cases where hello default behavior is bypassed:</span></span>

* <span data-ttu-id="91a37-201">Você não precisa estender `AEDefaultNotifier`, por exemplo, você implementou o tratamento de categoria a partir do zero.</span><span class="sxs-lookup"><span data-stu-id="91a37-201">You don't extend `AEDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="91a37-202">Você substitui `prepareNotificationView:forContent:`, ser toomap-se de que pelo menos `onNotificationActioned` ou `onNotificationExited` tooone dos controles U.I.</span><span class="sxs-lookup"><span data-stu-id="91a37-202">You overrode `prepareNotificationView:forContent:`, be sure toomap at least `onNotificationActioned` or `onNotificationExited` tooone of your U.I controls.</span></span>

> [!WARNING]
> <span data-ttu-id="91a37-203">Se `handleNotification:` lançará uma exceção, Olá conteúdo será excluído e `drop` é chamado, isso é relatado nas estatísticas e campanhas Avançar agora podem ser processadas.</span><span class="sxs-lookup"><span data-stu-id="91a37-203">If `handleNotification:` throws an exception, hello content is deleted and `drop` is called, this is reported in statistics and next campaigns can now be processed.</span></span>
>
>

#### <a name="include-notification-as-part-of-an-existing-view"></a><span data-ttu-id="91a37-204">Incluir notificação como parte de uma exibição existente</span><span class="sxs-lookup"><span data-stu-id="91a37-204">Include notification as part of an existing view</span></span>
<span data-ttu-id="91a37-205">Sobreposições são ótimas para uma integração rápida, mas podem não ser convenientes algumas vezes ou podem ter efeitos colaterais indesejados.</span><span class="sxs-lookup"><span data-stu-id="91a37-205">Overlays are great for a fast integration but can be sometimes not convenient, or can have unwanted side effects.</span></span>

<span data-ttu-id="91a37-206">Se você não estiver satisfeito com o sistema de sobreposição de saudação em alguns dos seus modos de exibição, você pode personalizá-lo para esses modos de exibição.</span><span class="sxs-lookup"><span data-stu-id="91a37-206">If you're not satisfied with hello overlay system in some of your views, you can customize it for these views.</span></span>

<span data-ttu-id="91a37-207">Você pode decidir tooinclude nosso layout de notificação em exibições existentes.</span><span class="sxs-lookup"><span data-stu-id="91a37-207">You can decide tooinclude our notification layout in your existing views.</span></span> <span data-ttu-id="91a37-208">toodo assim, há dois estilos de implementação:</span><span class="sxs-lookup"><span data-stu-id="91a37-208">toodo so, there is two implementation styles:</span></span>

1. <span data-ttu-id="91a37-209">Adicionar exibição de notificação hello usando o construtor de interface</span><span class="sxs-lookup"><span data-stu-id="91a37-209">Add hello notification view using interface builder</span></span>

   * <span data-ttu-id="91a37-210">Abra o *Interface Builder*</span><span class="sxs-lookup"><span data-stu-id="91a37-210">Open *Interface Builder*</span></span>
   * <span data-ttu-id="91a37-211">Insere um 320 x 60 (ou 60 x 768 se você estiver no iPad) `UIView` onde você deseja Olá notificação tooappear</span><span class="sxs-lookup"><span data-stu-id="91a37-211">Place a 320x60 (or 768x60 if you are on iPad) `UIView` where you want hello notification tooappear</span></span>
   * <span data-ttu-id="91a37-212">Defina o valor de marca de saudação para esta exibição muito: **36822491**</span><span class="sxs-lookup"><span data-stu-id="91a37-212">Set hello Tag value for this view too: **36822491**</span></span>
2. <span data-ttu-id="91a37-213">Adicione exibição de notificação Olá programaticamente.</span><span class="sxs-lookup"><span data-stu-id="91a37-213">Add hello notification view programmatically.</span></span> <span data-ttu-id="91a37-214">Basta adicione Olá código a seguir quando o modo de exibição foi inicializado:</span><span class="sxs-lookup"><span data-stu-id="91a37-214">Just add hello following code when your view has been initialized:</span></span>

       UIView* notificationView = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 60)]; //Replace x and y coordinate values tooyour needs.
       notificationView.tag = NOTIFICATION_AREA_VIEW_TAG;
       [self.view addSubview:notificationView];

<span data-ttu-id="91a37-215">A macro `NOTIFICATION_AREA_VIEW_TAG` pode ser encontrada em `AEDefaultNotifier.h`.</span><span class="sxs-lookup"><span data-stu-id="91a37-215">`NOTIFICATION_AREA_VIEW_TAG` macro can be found in `AEDefaultNotifier.h`.</span></span>

> [!NOTE]
> <span data-ttu-id="91a37-216">Notificador de padrão de saudação detecta automaticamente o layout de notificação que Olá incluído nessa exibição e não adicionará uma sobreposição para ele.</span><span class="sxs-lookup"><span data-stu-id="91a37-216">hello default notifier automatically detects that hello notification layout is included in this view and will not add an overlay for it.</span></span>
>
>

### <a name="announcements-and-polls"></a><span data-ttu-id="91a37-217">Anúncios e pesquisas</span><span class="sxs-lookup"><span data-stu-id="91a37-217">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="91a37-218">Layouts</span><span class="sxs-lookup"><span data-stu-id="91a37-218">Layouts</span></span>
<span data-ttu-id="91a37-219">Você pode modificar arquivos Olá `AEDefaultAnnouncementView.xib` e `AEDefaultPollView.xib` como manter valores de marca hello e tipos de sub-visualizações existente hello.</span><span class="sxs-lookup"><span data-stu-id="91a37-219">You can modify hello files `AEDefaultAnnouncementView.xib` and `AEDefaultPollView.xib` as long as you keep hello tag values and types of hello existing subviews.</span></span>

#### <a name="categories"></a><span data-ttu-id="91a37-220">Categorias</span><span class="sxs-lookup"><span data-stu-id="91a37-220">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="91a37-221">Layouts alternativos</span><span class="sxs-lookup"><span data-stu-id="91a37-221">Alternate layouts</span></span>
<span data-ttu-id="91a37-222">Como as notificações, categoria da campanha Olá pode ser usado toohave de layouts alternativos para suas notificações e pesquisas.</span><span class="sxs-lookup"><span data-stu-id="91a37-222">Like notifications, hello campaign's category can be used toohave alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="91a37-223">toocreate uma categoria para um aviso, você deve estender **AEAnnouncementViewController** e registrá-lo depois que o módulo de alcance Olá foi inicializado:</span><span class="sxs-lookup"><span data-stu-id="91a37-223">toocreate a category for an announcement, you must extend **AEAnnouncementViewController** and register it once hello reach module has been initialized:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:@"my_category"];

> [!NOTE]
> <span data-ttu-id="91a37-224">Cada vez que um usuário clique em uma notificação para um aviso com a categoria de hello "meu\_categoria", o controlador de exibição registrados (nesse caso `MyCustomAnnouncementViewController`) será inicializado chamando o método hello `initWithAnnouncement:` e modo de exibição de saudação adicionado toohello a janela atual do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91a37-224">Each time a user will click on a notification for an announcement with hello category "my\_category", your registered view controller (in that case `MyCustomAnnouncementViewController`) will be initialized by calling hello method `initWithAnnouncement:` and hello view will be added toohello current application window.</span></span>
>
>

<span data-ttu-id="91a37-225">Na implementação de saudação `AEAnnouncementViewController` classe, você terá a propriedade de saudação tooread `announcement` tooinitialize seu sub-visualizações.</span><span class="sxs-lookup"><span data-stu-id="91a37-225">In your implementation of hello `AEAnnouncementViewController` class you will have tooread hello property `announcement` tooinitialize your subviews.</span></span> <span data-ttu-id="91a37-226">Considere o exemplo hello abaixo, onde dois rótulos são inicializados usando `title` e `body` propriedades de saudação `AEReachAnnouncement` classe:</span><span class="sxs-lookup"><span data-stu-id="91a37-226">Consider hello example below, where two labels are initialized using `title` and `body` properties of hello `AEReachAnnouncement` class:</span></span>

    -(void)loadView
    {
        [super loadView];

        UILabel* titleLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        titleLabel.font = [UIFont systemFontOfSize:32.0];
        titleLabel.text = self.announcement.title;

        UILabel* bodyLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        bodyLabel.font = [UIFont systemFontOfSize:24.0];
        bodyLabel.text = self.announcement.body;

        [self.view addSubview:titleLabel];
        [self.view addSubview:bodyLabel];
    }

<span data-ttu-id="91a37-227">Se você não deseja tooload suas exibições sozinho, mas você quiser apenas o layout de exibição do tooreuse saudação padrão comunicado, você pode simplesmente fazer seu controlador de modo de exibição personalizado estende classe Olá fornecido `AEDefaultAnnouncementViewController`.</span><span class="sxs-lookup"><span data-stu-id="91a37-227">If you don't want tooload your views by yourself but you just want tooreuse hello default announcement view layout, you can simply make your custom view controller extends hello provided class `AEDefaultAnnouncementViewController`.</span></span> <span data-ttu-id="91a37-228">Duplicar nesse caso, o arquivo de ponta de saudação `AEDefaultAnnouncementView.xib` e renomeá-lo para que possam ser carregados pelo controlador de modo de exibição personalizado (para um controlador chamado `CustomAnnouncementViewController`, você deve chamar o arquivo nib `CustomAnnouncementView.xib`).</span><span class="sxs-lookup"><span data-stu-id="91a37-228">In that case, duplicate hello nib file `AEDefaultAnnouncementView.xib` and rename it so it can be loaded by your custom view controller (for a controller named `CustomAnnouncementViewController`, you should call your nib file `CustomAnnouncementView.xib`).</span></span>

<span data-ttu-id="91a37-229">categoria de padrão de saudação tooreplace de anúncios, simplesmente registrar controlador de modo de exibição personalizado para categoria Olá definido em `kAEReachDefaultCategory`:</span><span class="sxs-lookup"><span data-stu-id="91a37-229">tooreplace hello default category of announcements, simply register your custom view controller for hello category defined in `kAEReachDefaultCategory`:</span></span>

    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:kAEReachDefaultCategory];

<span data-ttu-id="91a37-230">Pesquisas podem ser personalizado Olá mesma maneira:</span><span class="sxs-lookup"><span data-stu-id="91a37-230">Polls can be customized hello same way :</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerPollController:[MyCustomPollViewController class] forCategory:@"my_category"];

<span data-ttu-id="91a37-231">Esse tempo, Olá fornecido `MyCustomPollViewController` deve estender `AEPollViewController`.</span><span class="sxs-lookup"><span data-stu-id="91a37-231">This time, hello provided `MyCustomPollViewController` must extend `AEPollViewController`.</span></span> <span data-ttu-id="91a37-232">Ou você pode escolher tooextend do controlador de padrão de saudação: `AEDefaultPollViewController`.</span><span class="sxs-lookup"><span data-stu-id="91a37-232">Or you can choose tooextend from hello default controller: `AEDefaultPollViewController`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="91a37-233">Não se esqueça de toocall ou `action` (`submitAnswers:` para controladores de exibição de pesquisa personalizada) ou `exit` método antes de controlador de exibição de saudação é descartada.</span><span class="sxs-lookup"><span data-stu-id="91a37-233">Don't forget toocall either `action` (`submitAnswers:` for custom poll view controllers) or `exit` method before hello view controller is dismissed.</span></span> <span data-ttu-id="91a37-234">Caso contrário, as estatísticas não serão enviadas (ou seja, nenhuma análise campanha Olá) e mais importante Avançar campanhas não serão notificadas até que o processo de aplicativo hello seja reiniciado.</span><span class="sxs-lookup"><span data-stu-id="91a37-234">Otherwise, statistics won't be sent (i.e. no analytics on hello campaign) and more importantly next campaigns will not be notified until hello application process is restarted.</span></span>
>
>

##### <a name="implementation-example"></a><span data-ttu-id="91a37-235">Exemplo de implementação</span><span class="sxs-lookup"><span data-stu-id="91a37-235">Implementation example</span></span>
<span data-ttu-id="91a37-236">Essa implementação de exibição de notificação personalizada Olá é carregada de um arquivo externo xib.</span><span class="sxs-lookup"><span data-stu-id="91a37-236">In this implementation hello custom announcement view is loaded from an external xib file.</span></span>

<span data-ttu-id="91a37-237">Como personalização avançada de notificação, é recomendável toolook no código-fonte da implementação padrão Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="91a37-237">Like for advanced notification customization, it is recommended toolook at hello source code of hello standard implementation.</span></span>

`CustomAnnouncementViewController.h`

    //Interface
    @interface CustomAnnouncementViewController : AEAnnouncementViewController {
      UILabel* titleLabel;
      UITextView* descTextView;
      UIWebView* htmlWebView;
      UIButton* okButton;
      UIButton* cancelButton;
    }

    @property (nonatomic, retain) IBOutlet UILabel* titleLabel;
    @property (nonatomic, retain) IBOutlet UITextView* descTextView;
    @property (nonatomic, retain) IBOutlet UIWebView* htmlWebView;
    @property (nonatomic, retain) IBOutlet UIButton* okButton;
    @property (nonatomic, retain) IBOutlet UIButton* cancelButton;

    -(IBAction)okButtonClicked:(id)sender;
    -(IBAction)cancelButtonClicked:(id)sender;

`CustomAnnouncementViewController.m`

    //Implementation
    @implementation CustomAnnouncementViewController
    @synthesize titleLabel;
    @synthesize descTextView;
    @synthesize htmlWebView;
    @synthesize okButton;
    @synthesize cancelButton;

    -(id)initWithAnnouncement:(AEReachAnnouncement*)anAnnouncement
    {
      self = [super initWithNibName:@"CustomAnnouncementViewController" bundle:nil];
      if (self != nil) {
        self.announcement = anAnnouncement;
      }
      return self;
    }

    - (void) dealloc
    {
      [titleLabel release];
      [descTextView release];
      [htmlWebView release];
      [okButton release];
      [cancelButton release];
      [super dealloc];
    }

    - (void)viewDidLoad {
      [super viewDidLoad];

      /* Init announcement title */
      titleLabel.text = self.announcement.title;

      /* Init announcement body */
      if(self.announcement.type == AEAnnouncementTypeHtml)
      {
        titleLabel.hidden = YES;
        htmlWebView.hidden = NO;
        [htmlWebView loadHTMLString:self.announcement.body baseURL:[NSURL URLWithString:@"http://localhost/"]];
      }
      else
      {
        titleLabel.hidden = NO;
        htmlWebView.hidden = YES;
        descTextView.text = self.announcement.body;
      }

      /* Set action button label */
      if([self.announcement.actionLabel length] > 0)
        [okButton setTitle:self.announcement.actionLabel forState:UIControlStateNormal];

      /* Set exit button label */
      if([self.announcement.exitLabel length] > 0)
        [cancelButton setTitle:self.announcement.exitLabel forState:UIControlStateNormal];
    }

    #pragma mark Actions

    -(IBAction)okButtonClicked:(id)sender
    {
        [self action];
    }

    -(IBAction)cancelButtonClicked:(id)sender
    {
        [self exit];
    }

    @end
