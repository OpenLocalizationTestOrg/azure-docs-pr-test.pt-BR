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
# <a name="upgrade-procedures"></a><span data-ttu-id="6c8e1-103">Procedimentos de atualização</span><span class="sxs-lookup"><span data-stu-id="6c8e1-103">Upgrade procedures</span></span>
<span data-ttu-id="6c8e1-104">Se você já tiver integrado uma versão mais antiga do contrato em seu aplicativo, você tem Olá tooconsider pontos a seguir ao atualizar Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-104">If you already have integrated an older version of Engagement into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="6c8e1-105">Para cada nova versão do SDK do hello primeiro você deve substituir (remover e importar novamente no xcode) Olá pastas EngagementSDK e EngagementReach.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-105">For each new version of hello SDK you must first replace (remove and re-import in xcode) hello EngagementSDK and EngagementReach folders.</span></span>

## <a name="from-300-too400"></a><span data-ttu-id="6c8e1-106">De 3.0.0 too4.0.0</span><span class="sxs-lookup"><span data-stu-id="6c8e1-106">From 3.0.0 too4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="6c8e1-107">XCode 8</span><span class="sxs-lookup"><span data-stu-id="6c8e1-107">XCode 8</span></span>
<span data-ttu-id="6c8e1-108">8 XCode é obrigatório a partir da versão 4.0.0 de saudação SDK.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-108">XCode 8 is mandatory starting from version 4.0.0 of hello SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="6c8e1-109">Se você realmente depende XCode 7, você pode usar o hello [iOS SDK Engagement v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="6c8e1-109">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="6c8e1-110">Há um bug conhecido no módulo de alcance Olá desta versão anterior durante a execução em dispositivos iOS 10: notificações do sistema não são acionadas.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-110">There is a known bug on hello reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="6c8e1-111">toofix isso você terá tooimplement Olá preterido API `application:didReceiveRemoteNotification:` em seu aplicativo delegar da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="6c8e1-111">toofix this you will have tooimplement hello deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
> 
> 

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="6c8e1-112">**Não recomendamos essa solução alternativa** pois esse comportamento pode alterar qualquer atualização da versão futura iOS (até mesmo pequenas) porque esta API do iOS foi preterida.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-112">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="6c8e1-113">Você deve alternar tooXCode 8 assim que possível.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-113">You should switch tooXCode 8 as soon as possible.</span></span>
> 
> 

### <a name="usernotifications-framework"></a><span data-ttu-id="6c8e1-114">Estrutura UserNotifications</span><span class="sxs-lookup"><span data-stu-id="6c8e1-114">UserNotifications framework</span></span>
<span data-ttu-id="6c8e1-115">Você precisa Olá tooadd `UserNotifications` framework em fases de compilação.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-115">You need tooadd hello `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="6c8e1-116">no Explorador de projeto hello, abra o painel de projeto e selecione o destino correto hello.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-116">in hello project explorer, open your project pane and select hello correct target.</span></span> <span data-ttu-id="6c8e1-117">Em seguida, abra Olá **"Fases de compilação"** guia e em Olá **"Binário com bibliotecas de vínculo"** menu, adicionar framework `UserNotifications.framework` -definir Olá link como`Optional`</span><span class="sxs-lookup"><span data-stu-id="6c8e1-117">Then, open hello **"Build phases"** tab and in hello **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set hello link as `Optional`</span></span>

### <a name="application-push-capability"></a><span data-ttu-id="6c8e1-118">Capacidade de envio por push do aplicativo</span><span class="sxs-lookup"><span data-stu-id="6c8e1-118">Application push capability</span></span>
<span data-ttu-id="6c8e1-119">8 XCode pode redefinir seu aplicativo push capacidade,. Verifique novamente em Olá `capability` guia de destino selecionado.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-119">XCode 8 may reset your app push capability, please double check it in hello `capability` tab of your selected target.</span></span>

### <a name="add-hello-new-ios-10-notification-registration-code"></a><span data-ttu-id="6c8e1-120">Adicione código de registro do hello novo iOS notificação 10</span><span class="sxs-lookup"><span data-stu-id="6c8e1-120">Add hello new iOS 10 notification registration code</span></span>
<span data-ttu-id="6c8e1-121">Olá antigos código trecho tooregister Olá aplicativo toonotifications ainda funciona, mas está usando preterido APIs durante a execução no iOS 10.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-121">hello older code snippet tooregister hello app toonotifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="6c8e1-122">Saudação de importação `User Notification` framework:</span><span class="sxs-lookup"><span data-stu-id="6c8e1-122">Import hello `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h> 

<span data-ttu-id="6c8e1-123">No seu método representante do aplicativo `application:didFinishLaunchingWithOptions` , substitua:</span><span class="sxs-lookup"><span data-stu-id="6c8e1-123">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

    if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
        [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
        [application registerForRemoteNotifications];
    }
    else {

        [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
    }

<span data-ttu-id="6c8e1-124">por:</span><span class="sxs-lookup"><span data-stu-id="6c8e1-124">by :</span></span>

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="6c8e1-125">Resolver conflitos de delegado UNUserNotificationCenter</span><span class="sxs-lookup"><span data-stu-id="6c8e1-125">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="6c8e1-126">*Se o aplicativo nem uma das bibliotecas de terceiros implementar um `UNUserNotificationCenterDelegate`, ignore esta parte.*</span><span class="sxs-lookup"><span data-stu-id="6c8e1-126">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="6c8e1-127">Um `UNUserNotificationCenter` delegado é usado pelo ciclo de vida de Olá Olá SDK toomonitor de notificações de compromisso em dispositivos que executam o iOS 10 ou superior.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-127">A `UNUserNotificationCenter` delegate is used by hello SDK toomonitor hello life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="6c8e1-128">Olá SDK tem sua própria implementação de saudação `UNUserNotificationCenterDelegate` de protocolo, mas pode haver apenas um `UNUserNotificationCenter` delegar por aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-128">hello SDK has its own implementation of hello `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="6c8e1-129">Qualquer outro representante adicionado toohello `UNUserNotificationCenter` objeto está em conflito com hello contrato um.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-129">Any other delegate added toohello `UNUserNotificationCenter` object will conflict with hello Engagement one.</span></span> <span data-ttu-id="6c8e1-130">Se Olá SDK detectar delegado do seu ou qualquer outra parte, em seguida, ele não usará sua própria implementação toogive você tooresolve uma chance Olá conflitos.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-130">If hello SDK detects your or any other third party's delegate then it will not use its own implementation toogive you a chance tooresolve hello conflicts.</span></span> <span data-ttu-id="6c8e1-131">Você terá tooadd Olá contrato lógica tooyour possui delegado em ordem tooresolve conflitos de saudação.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-131">You will have tooadd hello Engagement logic tooyour own delegate in order tooresolve hello conflicts.</span></span>

<span data-ttu-id="6c8e1-132">Há dois tooachieve de maneiras isso.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-132">There are two ways tooachieve this.</span></span>

<span data-ttu-id="6c8e1-133">Proposta 1, encaminhando o delegado chama toohello SDK:</span><span class="sxs-lookup"><span data-stu-id="6c8e1-133">Proposal 1, simply by forwarding your delegate calls toohello SDK:</span></span>

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

<span data-ttu-id="6c8e1-134">Ou proposta 2, herdando de saudação `AEUserNotificationHandler` classe</span><span class="sxs-lookup"><span data-stu-id="6c8e1-134">Or proposal 2, by inheriting from hello `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="6c8e1-135">Você pode determinar se uma notificação de contrato ou não passando seus `userInfo` toohello dicionário agente `isEngagementPushPayload:` método de classe.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-135">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary toohello Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="6c8e1-136">Certifique-se de que Olá `UNUserNotificationCenter` representante do objeto é definido tooyour delegado em qualquer Olá `application:willFinishLaunchingWithOptions:` ou hello `application:didFinishLaunchingWithOptions:` método do seu representante de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-136">Make sure that hello `UNUserNotificationCenter` object's delegate is set tooyour delegate within either hello `application:willFinishLaunchingWithOptions:` or hello `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="6c8e1-137">Por exemplo, se você tiver implementado Olá acima proposta 1:</span><span class="sxs-lookup"><span data-stu-id="6c8e1-137">For instance, if you implemented hello above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code
  
        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="from-200-too300"></a><span data-ttu-id="6c8e1-138">De 2.0.0 too3.0.0</span><span class="sxs-lookup"><span data-stu-id="6c8e1-138">From 2.0.0 too3.0.0</span></span>
<span data-ttu-id="6c8e1-139">Suporte removido para iOS 4.X.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-139">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="6c8e1-140">A partir do destino de implantação de saudação essa versão do seu aplicativo deve ter pelo menos 6 do iOS.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-140">Starting from this version hello deployment target of your application must be at least iOS 6.</span></span>

<span data-ttu-id="6c8e1-141">Se você estiver usando o alcance do seu aplicativo, você deve adicionar `remote-notification` toohello valor `UIBackgroundModes` matriz em seu arquivo Info. plist em notificações remoto de tooreceive de ordem.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-141">If you are using Reach in your application, you must add `remote-notification` value toohello `UIBackgroundModes` array in your Info.plist file in order tooreceive remote notifications.</span></span>

<span data-ttu-id="6c8e1-142">Olá método `application:didReceiveRemoteNotification:` precisa toobe substituído por `application:didReceiveRemoteNotification:fetchCompletionHandler:` em seu representante do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-142">hello method `application:didReceiveRemoteNotification:` needs toobe replaced by `application:didReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate.</span></span>

<span data-ttu-id="6c8e1-143">"AEPushDelegate.h" foi preterido e interface precisa tooremove todas as referências.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-143">"AEPushDelegate.h" is deprecated interface and you need tooremove all references.</span></span> <span data-ttu-id="6c8e1-144">Isso inclui a remoção `[[EngagementAgent shared] setPushDelegate:self]` e hello delegar métodos do seu representante do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="6c8e1-144">This includes removing `[[EngagementAgent shared] setPushDelegate:self]` and hello delegate methods from your application delegate:</span></span>

    -(void)willRetrieveLaunchMessage;
    -(void)didFailToRetrieveLaunchMessage;
    -(void)didReceiveLaunchMessage:(AEPushMessage*)launchMessage;

## <a name="from-1160-too200"></a><span data-ttu-id="6c8e1-145">De 1.16.0 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="6c8e1-145">From 1.16.0 too2.0.0</span></span>
<span data-ttu-id="6c8e1-146">Olá a seguir descrevem como toomigrate uma integração SDK da saudação Capptain serviço oferecido pelo Capptain SAS em um aplicativo da plataforma do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-146">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span>
<span data-ttu-id="6c8e1-147">Se você estiver migrando de uma versão anterior,. Consulte Olá Capptain site da web toomigrate too1.16 primeiro, em seguida, aplicar Olá procedimento a seguir.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-147">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.16 first then apply hello following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c8e1-148">Capptain e o compromisso de mobilidade não são Olá mesmos serviços e procedimento Olá indicado abaixo só destaca como toomigrate Olá aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-148">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="6c8e1-149">Migrando Olá SDK no aplicativo hello não vai migrar seus dados do hello Capptain toohello Mobile Engagement de servidores</span><span class="sxs-lookup"><span data-stu-id="6c8e1-149">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

### <a name="agent"></a><span data-ttu-id="6c8e1-150">Agente</span><span class="sxs-lookup"><span data-stu-id="6c8e1-150">Agent</span></span>
<span data-ttu-id="6c8e1-151">Olá método `registerApp:` foi substituído pelo novo método de saudação `init:`.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-151">hello method `registerApp:` has been replaced by hello new method `init:`.</span></span> <span data-ttu-id="6c8e1-152">Seu representante de aplicativo deve ser atualizado de acordo e usar a cadeia de conexão:</span><span class="sxs-lookup"><span data-stu-id="6c8e1-152">Your application delegate must be updated accordingly and use connection string:</span></span>

            - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
            {
              [...]
              [EngagementAgent init:@"YOUR_CONNECTION_STRING"];
              [...]
            }

<span data-ttu-id="6c8e1-153">Controle de SmartAd foi removido do SDK apenas tiver tooremove todas as instâncias de `AETrackModule` classe</span><span class="sxs-lookup"><span data-stu-id="6c8e1-153">SmartAd tracking has been removed from SDK you just have tooremove all instances of `AETrackModule` class</span></span>

### <a name="class-name-changes"></a><span data-ttu-id="6c8e1-154">Alterações de nome de classe</span><span class="sxs-lookup"><span data-stu-id="6c8e1-154">Class Name Changes</span></span>
<span data-ttu-id="6c8e1-155">Como parte da saudação rebranding, há alguns nomes de classe/arquivos que precisam de toobe alterado.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-155">As part of hello rebranding, there are couple of class/file names that need toobe changed.</span></span>

<span data-ttu-id="6c8e1-156">Todas as classes prefixadas com “CP” foram renomeadas com o prefixo “AE”.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-156">All classes prefixed with "CP" are renamed with "AE" prefix.</span></span>

<span data-ttu-id="6c8e1-157">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="6c8e1-157">Example:</span></span>

* <span data-ttu-id="6c8e1-158">`CPModule.h`é renomeado muito`AEModule.h`.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-158">`CPModule.h` is renamed too`AEModule.h`.</span></span>

<span data-ttu-id="6c8e1-159">Todas as classes prefixadas com “Capptain” foram renomeadas com o prefixo “Engagement”.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-159">All classes prefixed with "Capptain" are renamed with "Engagement" prefix.</span></span>

<span data-ttu-id="6c8e1-160">Exemplos:</span><span class="sxs-lookup"><span data-stu-id="6c8e1-160">Examples:</span></span>

* <span data-ttu-id="6c8e1-161">Olá classe `CapptainAgent` é renomeado muito`EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-161">hello class `CapptainAgent` is renamed too`EngagementAgent`.</span></span>
* <span data-ttu-id="6c8e1-162">Olá classe `CapptainTableViewController` é renomeado muito`EngagementTableViewController`.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-162">hello class `CapptainTableViewController` is renamed too`EngagementTableViewController`.</span></span>
* <span data-ttu-id="6c8e1-163">Olá classe `CapptainUtils` é renomeado muito`EngagementUtils`.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-163">hello class `CapptainUtils` is renamed too`EngagementUtils`.</span></span>
* <span data-ttu-id="6c8e1-164">Olá classe `CapptainViewController` é renomeado muito`EngagementViewController`.</span><span class="sxs-lookup"><span data-stu-id="6c8e1-164">hello class `CapptainViewController` is renamed too`EngagementViewController`.</span></span>

