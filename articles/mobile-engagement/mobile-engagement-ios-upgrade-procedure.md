---
title: "Procedimento de atualização do SDK para iOS do Azure Mobile Engagement | Microsoft Docs"
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
ms.openlocfilehash: 37c7f133d079186f828d58cabce0d2a259efd085
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="e8c1a-103">Procedimentos de atualização</span><span class="sxs-lookup"><span data-stu-id="e8c1a-103">Upgrade procedures</span></span>
<span data-ttu-id="e8c1a-104">Se você já tiver integrado uma versão anterior do Engagement no seu aplicativo, você deve considerar os seguintes pontos ao atualizar o SDK.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-104">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="e8c1a-105">Para cada nova versão do SDK, você deve primeiro substituir (remover e importar novamente no xcode) as pastas EngagementSDK e EngagementReach.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-105">For each new version of the SDK you must first replace (remove and re-import in xcode) the EngagementSDK and EngagementReach folders.</span></span>

## <a name="from-300-to-400"></a><span data-ttu-id="e8c1a-106">De 3.0.0 a 4.0.0</span><span class="sxs-lookup"><span data-stu-id="e8c1a-106">From 3.0.0 to 4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="e8c1a-107">XCode 8</span><span class="sxs-lookup"><span data-stu-id="e8c1a-107">XCode 8</span></span>
<span data-ttu-id="e8c1a-108">O XCode 8 é obrigatório desde a versão 4.0.0 do SDK.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-108">XCode 8 is mandatory starting from version 4.0.0 of the SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="e8c1a-109">Se você realmente depende do XCode 7, pode usar o [SDK do iOS Engagement v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="e8c1a-109">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="e8c1a-110">Há um bug conhecido no módulo de alcance nesta versão anterior durante a execução em dispositivos como iOS 10: as notificações de sistema não são acionadas.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-110">There is a known bug on the reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="e8c1a-111">Para corrigir isso, você terá que implementar a API desaprovada `application:didReceiveRemoteNotification:` no representante do aplicativo da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e8c1a-111">To fix this you will have to implement the deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
> 
> 

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="e8c1a-112">**Não recomendamos essa solução alternativa** pois esse comportamento pode alterar qualquer atualização da versão futura iOS (até mesmo pequenas) porque esta API do iOS foi preterida.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-112">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="e8c1a-113">Você deve mudar para o XCode 8 assim que possível.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-113">You should switch to XCode 8 as soon as possible.</span></span>
> 
> 

### <a name="usernotifications-framework"></a><span data-ttu-id="e8c1a-114">Estrutura UserNotifications</span><span class="sxs-lookup"><span data-stu-id="e8c1a-114">UserNotifications framework</span></span>
<span data-ttu-id="e8c1a-115">Você precisa adicionar a estrutura `UserNotifications` em suas fases de build.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-115">You need to add the `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="e8c1a-116">no Explorador de projeto, abra o painel de projeto e selecione o destino correto.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-116">in the project explorer, open your project pane and select the correct target.</span></span> <span data-ttu-id="e8c1a-117">Em seguida, abra a guia **"Compilar fases"** e, no menu **"Link binário com bibliotecas"**, adicione a estrutura `UserNotifications.framework` – defina o link como `Optional`</span><span class="sxs-lookup"><span data-stu-id="e8c1a-117">Then, open the **"Build phases"** tab and in the **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set the link as `Optional`</span></span>

### <a name="application-push-capability"></a><span data-ttu-id="e8c1a-118">Capacidade de envio por push do aplicativo</span><span class="sxs-lookup"><span data-stu-id="e8c1a-118">Application push capability</span></span>
<span data-ttu-id="e8c1a-119">O XCode 8 pode redefinir a capacidade de envio por push do aplicativo. Verifique isso novamente na guia `capability` do destino selecionado.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-119">XCode 8 may reset your app push capability, please double check it in the `capability` tab of your selected target.</span></span>

### <a name="add-the-new-ios-10-notification-registration-code"></a><span data-ttu-id="e8c1a-120">Adicionar o novo código de registro de notificação do iOS 10</span><span class="sxs-lookup"><span data-stu-id="e8c1a-120">Add the new iOS 10 notification registration code</span></span>
<span data-ttu-id="e8c1a-121">O trecho de código anterior para registrar o aplicativo para as notificações ainda funciona, mas está usando as APIs desaprovadas durante a execução no iOS 10.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-121">The older code snippet to register the app to notifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="e8c1a-122">Importe a estrutura `User Notification` :</span><span class="sxs-lookup"><span data-stu-id="e8c1a-122">Import the `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h> 

<span data-ttu-id="e8c1a-123">No seu método representante do aplicativo `application:didFinishLaunchingWithOptions` , substitua:</span><span class="sxs-lookup"><span data-stu-id="e8c1a-123">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

    if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
        [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
        [application registerForRemoteNotifications];
    }
    else {

        [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
    }

<span data-ttu-id="e8c1a-124">por:</span><span class="sxs-lookup"><span data-stu-id="e8c1a-124">by :</span></span>

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="e8c1a-125">Resolver conflitos de delegado UNUserNotificationCenter</span><span class="sxs-lookup"><span data-stu-id="e8c1a-125">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="e8c1a-126">*Se o aplicativo nem uma das bibliotecas de terceiros implementar um `UNUserNotificationCenterDelegate`, ignore esta parte.*</span><span class="sxs-lookup"><span data-stu-id="e8c1a-126">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="e8c1a-127">Um delegado `UNUserNotificationCenter` é usado pelo SDK para monitorar o ciclo de vida das notificações do Engagement em dispositivos que executam o iOS 10 ou superior.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-127">A `UNUserNotificationCenter` delegate is used by the SDK to monitor the life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="e8c1a-128">O SDK tem sua própria implementação do protocolo `UNUserNotificationCenterDelegate`, mas pode haver apenas um delegado `UNUserNotificationCenter` por aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-128">The SDK has its own implementation of the `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="e8c1a-129">Qualquer outro delegado adicionado ao objeto `UNUserNotificationCenter` entrará em conflito com o do Engagement.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-129">Any other delegate added to the `UNUserNotificationCenter` object will conflict with the Engagement one.</span></span> <span data-ttu-id="e8c1a-130">Se o SDK detectar seu delegado ou qualquer delegado de terceiros, ele não usará sua própria implementação, para lhe dar uma chance para resolver os conflitos.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-130">If the SDK detects your or any other third party's delegate then it will not use its own implementation to give you a chance to resolve the conflicts.</span></span> <span data-ttu-id="e8c1a-131">Você precisará adicionar a lógica do Engagement ao seu próprio delegado para resolver os conflitos.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-131">You will have to add the Engagement logic to your own delegate in order to resolve the conflicts.</span></span>

<span data-ttu-id="e8c1a-132">Há duas maneiras de fazer isso.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-132">There are two ways to achieve this.</span></span>

<span data-ttu-id="e8c1a-133">Proposta 1: apenas encaminhando as chamadas do delegado para o SDK:</span><span class="sxs-lookup"><span data-stu-id="e8c1a-133">Proposal 1, simply by forwarding your delegate calls to the SDK:</span></span>

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

<span data-ttu-id="e8c1a-134">Ou proposta 2: herdando da classe `AEUserNotificationHandler`</span><span class="sxs-lookup"><span data-stu-id="e8c1a-134">Or proposal 2, by inheriting from the `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="e8c1a-135">Você pode determinar se uma notificação vem do Engagement ou não passando seu dicionário `userInfo` para o método da classe `isEngagementPushPayload:` do Agent.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-135">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary to the Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="e8c1a-136">Verifique se o delegado do objeto `UNUserNotificationCenter` é definido como seu delegado no método `application:willFinishLaunchingWithOptions:` ou `application:didFinishLaunchingWithOptions:` do delegado do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-136">Make sure that the `UNUserNotificationCenter` object's delegate is set to your delegate within either the `application:willFinishLaunchingWithOptions:` or the `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="e8c1a-137">Por exemplo, se você implementou a proposta 1 acima:</span><span class="sxs-lookup"><span data-stu-id="e8c1a-137">For instance, if you implemented the above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code
  
        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="from-200-to-300"></a><span data-ttu-id="e8c1a-138">De 2.0.0 a 3.0.0</span><span class="sxs-lookup"><span data-stu-id="e8c1a-138">From 2.0.0 to 3.0.0</span></span>
<span data-ttu-id="e8c1a-139">Suporte removido para iOS 4.X.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-139">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="e8c1a-140">A partir de esta versão, o destino da implantação do seu aplicativo deve ter pelo menos o iOS 6.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-140">Starting from this version the deployment target of your application must be at least iOS 6.</span></span>

<span data-ttu-id="e8c1a-141">Se você estiver usando o Reach em seu aplicativo, deverá adicionar o valor `remote-notification` à matriz `UIBackgroundModes` no arquivo Info.plist para receber notificações remotas.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-141">If you are using Reach in your application, you must add `remote-notification` value to the `UIBackgroundModes` array in your Info.plist file in order to receive remote notifications.</span></span>

<span data-ttu-id="e8c1a-142">O método `application:didReceiveRemoteNotification:` precisa ser substituído pelo `application:didReceiveRemoteNotification:fetchCompletionHandler:` em seu representante de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-142">The method `application:didReceiveRemoteNotification:` needs to be replaced by `application:didReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate.</span></span>

<span data-ttu-id="e8c1a-143">"AEPushDelegate.h" é uma interface preterida e você precisa remover todas as referências.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-143">"AEPushDelegate.h" is deprecated interface and you need to remove all references.</span></span> <span data-ttu-id="e8c1a-144">Isso inclui remover o `[[EngagementAgent shared] setPushDelegate:self]` e os métodos representantes do seu representante de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="e8c1a-144">This includes removing `[[EngagementAgent shared] setPushDelegate:self]` and the delegate methods from your application delegate:</span></span>

    -(void)willRetrieveLaunchMessage;
    -(void)didFailToRetrieveLaunchMessage;
    -(void)didReceiveLaunchMessage:(AEPushMessage*)launchMessage;

## <a name="from-1160-to-200"></a><span data-ttu-id="e8c1a-145">De 1.16.0 a 2.0.0</span><span class="sxs-lookup"><span data-stu-id="e8c1a-145">From 1.16.0 to 2.0.0</span></span>
<span data-ttu-id="e8c1a-146">O seguinte descreve como migrar uma integração do SDK do serviço Capptain oferecido pelo Capptain SAS em um aplicativo acionado pelo Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-146">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span>
<span data-ttu-id="e8c1a-147">Se você estiver migrando de uma versão anterior, consulte o site do Capptain para migrar primeiro para a 1.16 e depois aplicar o procedimento a seguir</span><span class="sxs-lookup"><span data-stu-id="e8c1a-147">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.16 first then apply the following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8c1a-148">O Capptain e o Mobile Engagement não são os mesmos serviços e o procedimento fornecido abaixo destaca apenas como migrar o aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-148">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="e8c1a-149">Migrar o SDK no aplicativo NÃO migrará os dados dos servidores Capptain para os servidores do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="e8c1a-149">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span></span>
> 
> 

### <a name="agent"></a><span data-ttu-id="e8c1a-150">Agente</span><span class="sxs-lookup"><span data-stu-id="e8c1a-150">Agent</span></span>
<span data-ttu-id="e8c1a-151">O método `registerApp:` foi substituído pelo novo método `init:`.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-151">The method `registerApp:` has been replaced by the new method `init:`.</span></span> <span data-ttu-id="e8c1a-152">Seu representante de aplicativo deve ser atualizado de acordo e usar a cadeia de conexão:</span><span class="sxs-lookup"><span data-stu-id="e8c1a-152">Your application delegate must be updated accordingly and use connection string:</span></span>

            - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
            {
              [...]
              [EngagementAgent init:@"YOUR_CONNECTION_STRING"];
              [...]
            }

<span data-ttu-id="e8c1a-153">O rastreamento de SmartAd foi removido do SDK, você só precisa remover todas as instâncias da classe `AETrackModule`</span><span class="sxs-lookup"><span data-stu-id="e8c1a-153">SmartAd tracking has been removed from SDK you just have to remove all instances of `AETrackModule` class</span></span>

### <a name="class-name-changes"></a><span data-ttu-id="e8c1a-154">Alterações de nome de classe</span><span class="sxs-lookup"><span data-stu-id="e8c1a-154">Class Name Changes</span></span>
<span data-ttu-id="e8c1a-155">Como parte da renovação de marca, há alguns nomes de classe/arquivos que precisam ser alterados.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-155">As part of the rebranding, there are couple of class/file names that need to be changed.</span></span>

<span data-ttu-id="e8c1a-156">Todas as classes prefixadas com “CP” foram renomeadas com o prefixo “AE”.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-156">All classes prefixed with "CP" are renamed with "AE" prefix.</span></span>

<span data-ttu-id="e8c1a-157">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e8c1a-157">Example:</span></span>

* <span data-ttu-id="e8c1a-158">`CPModule.h` foi renomeado para `AEModule.h`.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-158">`CPModule.h` is renamed to `AEModule.h`.</span></span>

<span data-ttu-id="e8c1a-159">Todas as classes prefixadas com “Capptain” foram renomeadas com o prefixo “Engagement”.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-159">All classes prefixed with "Capptain" are renamed with "Engagement" prefix.</span></span>

<span data-ttu-id="e8c1a-160">Exemplos:</span><span class="sxs-lookup"><span data-stu-id="e8c1a-160">Examples:</span></span>

* <span data-ttu-id="e8c1a-161">A classe `CapptainAgent` foi renomeada para `EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-161">The class `CapptainAgent` is renamed to `EngagementAgent`.</span></span>
* <span data-ttu-id="e8c1a-162">A classe `CapptainTableViewController` foi renomeada para `EngagementTableViewController`.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-162">The class `CapptainTableViewController` is renamed to `EngagementTableViewController`.</span></span>
* <span data-ttu-id="e8c1a-163">A classe `CapptainUtils` foi renomeada para `EngagementUtils`.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-163">The class `CapptainUtils` is renamed to `EngagementUtils`.</span></span>
* <span data-ttu-id="e8c1a-164">A classe `CapptainViewController` foi renomeada para `EngagementViewController`.</span><span class="sxs-lookup"><span data-stu-id="e8c1a-164">The class `CapptainViewController` is renamed to `EngagementViewController`.</span></span>

