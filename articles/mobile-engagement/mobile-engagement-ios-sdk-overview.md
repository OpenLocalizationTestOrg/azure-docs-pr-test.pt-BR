---
title: "Visão geral do SDK para iOS do Azure Mobile Engagement | Microsoft Docs"
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
ms.openlocfilehash: 6acd343782a3ee07750e27ec3022ff81cedfadee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="ios-sdk-for-azure-mobile-engagement"></a><span data-ttu-id="e5942-103">SDK do iOS para o Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="e5942-103">iOS SDK for Azure Mobile Engagement</span></span>
<span data-ttu-id="e5942-104">Comece aqui obter todos os detalhes sobre como integrar o Azure Mobile Engagement em um aplicativo iOS.</span><span class="sxs-lookup"><span data-stu-id="e5942-104">Start here to get all the details on how to integrate Azure Mobile Engagement in an iOS App.</span></span> <span data-ttu-id="e5942-105">Se você gostaria de experimentá-lo primeiro, faça nosso [tutorial de 15 minutos](mobile-engagement-ios-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e5942-105">If you'd like to give it a try first, make sure you do our [15 minutes tutorial](mobile-engagement-ios-get-started.md).</span></span>

<span data-ttu-id="e5942-106">Clique para ver o [Conteúdo do SDK](mobile-engagement-ios-sdk-content.md)</span><span class="sxs-lookup"><span data-stu-id="e5942-106">Click to see the [SDK Content](mobile-engagement-ios-sdk-content.md)</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="e5942-107">Procedimentos de integração</span><span class="sxs-lookup"><span data-stu-id="e5942-107">Integration procedures</span></span>
1. <span data-ttu-id="e5942-108">Comece aqui: [Como integrar o Mobile Engagement em seu aplicativo iOS](mobile-engagement-ios-integrate-engagement.md)</span><span class="sxs-lookup"><span data-stu-id="e5942-108">Start here: [How to integrate Mobile Engagement in your iOS app](mobile-engagement-ios-integrate-engagement.md)</span></span>
2. <span data-ttu-id="e5942-109">Para Notificações: [Como integrar o Reach (Notificações) em seu aplicativo iOS](mobile-engagement-ios-integrate-engagement-reach.md)</span><span class="sxs-lookup"><span data-stu-id="e5942-109">For Notifications: [How to integrate Reach (Notifications) in your iOS app](mobile-engagement-ios-integrate-engagement-reach.md)</span></span>
3. <span data-ttu-id="e5942-110">Implementação do plano de marcação: [Como usar a API de marcação avançada do Mobile Engagement em seu aplicativo iOS](mobile-engagement-ios-use-engagement-api.md)</span><span class="sxs-lookup"><span data-stu-id="e5942-110">Tag plan implementation: [How to use the advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md)</span></span>

## <a name="release-notes"></a><span data-ttu-id="e5942-111">Notas de versão</span><span class="sxs-lookup"><span data-stu-id="e5942-111">Release notes</span></span>
### <a name="410-07172017"></a><span data-ttu-id="e5942-112">4.1.0 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="e5942-112">4.1.0 (07/17/2017)</span></span>
* <span data-ttu-id="e5942-113">Corrigidas as notificações apagadas na tela de fundo.</span><span class="sxs-lookup"><span data-stu-id="e5942-113">Fixed badges cleared in background.</span></span>
* <span data-ttu-id="e5942-114">Corrigidos os avisos no XCode 9 sobre as APIs não chamadas na fila principal.</span><span class="sxs-lookup"><span data-stu-id="e5942-114">Fixed warnings on XCode 9 about APIs not called in main queue.</span></span>
* <span data-ttu-id="e5942-115">Corrigida uma perda de memória em pesquisas Reach.</span><span class="sxs-lookup"><span data-stu-id="e5942-115">Fixed a memory leak in Reach polls.</span></span>
* <span data-ttu-id="e5942-116">Removido o suporte para iOS 6.X.</span><span class="sxs-lookup"><span data-stu-id="e5942-116">Dropped support for iOS 6.X.</span></span> <span data-ttu-id="e5942-117">Desta versão em diante, o destino da implantação do seu aplicativo deverá ser pelo menos o iOS 7.</span><span class="sxs-lookup"><span data-stu-id="e5942-117">Starting from this version the deployment target of your application must be at least iOS 7.</span></span>

<span data-ttu-id="e5942-118">Para a versão anterior, consulte as [notas de versão completas](mobile-engagement-ios-release-notes.md)</span><span class="sxs-lookup"><span data-stu-id="e5942-118">For earlier version please see the [complete release notes](mobile-engagement-ios-release-notes.md)</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="e5942-119">Procedimentos de atualização</span><span class="sxs-lookup"><span data-stu-id="e5942-119">Upgrade procedures</span></span>
<span data-ttu-id="e5942-120">Se você já tiver integrado uma versão anterior do Engagement no seu aplicativo, você deve considerar os seguintes pontos ao atualizar o SDK.</span><span class="sxs-lookup"><span data-stu-id="e5942-120">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="e5942-121">Talvez você precise seguir vários procedimentos se perdeu várias versões do SDK consulte os [Procedimentos de atualização](mobile-engagement-ios-upgrade-procedure.md)completos.</span><span class="sxs-lookup"><span data-stu-id="e5942-121">You may have to follow several procedures if you missed several versions of the SDK see the complete [Upgrade Procedures](mobile-engagement-ios-upgrade-procedure.md).</span></span>

<span data-ttu-id="e5942-122">Para cada nova versão do SDK, você deve primeiro substituir (remover e importar novamente no xcode) as pastas EngagementSDK e EngagementReach.</span><span class="sxs-lookup"><span data-stu-id="e5942-122">For each new version of the SDK you must first replace (remove and re-import in xcode) the EngagementSDK and EngagementReach folders.</span></span>

### <a name="from-300-to-400"></a><span data-ttu-id="e5942-123">De 3.0.0 a 4.0.0</span><span class="sxs-lookup"><span data-stu-id="e5942-123">From 3.0.0 to 4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="e5942-124">XCode 8</span><span class="sxs-lookup"><span data-stu-id="e5942-124">XCode 8</span></span>
<span data-ttu-id="e5942-125">O XCode 8 é obrigatório desde a versão 4.0.0 do SDK.</span><span class="sxs-lookup"><span data-stu-id="e5942-125">XCode 8 is mandatory starting from version 4.0.0 of the SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="e5942-126">Se você realmente depende do XCode 7, pode usar o [SDK do iOS Engagement v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="e5942-126">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="e5942-127">Há um bug conhecido no módulo de alcance nesta versão anterior durante a execução em dispositivos como iOS 10: as notificações de sistema não são acionadas.</span><span class="sxs-lookup"><span data-stu-id="e5942-127">There is a known bug on the reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="e5942-128">Para corrigir isso, você terá que implementar a API desaprovada `application:didReceiveRemoteNotification:` no representante do aplicativo da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e5942-128">To fix this you will have to implement the deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
>
>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="e5942-129">**Não recomendamos essa solução alternativa** pois esse comportamento pode alterar qualquer atualização da versão futura iOS (até mesmo pequenas) porque esta API do iOS foi preterida.</span><span class="sxs-lookup"><span data-stu-id="e5942-129">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="e5942-130">Você deve mudar para o XCode 8 assim que possível.</span><span class="sxs-lookup"><span data-stu-id="e5942-130">You should switch to XCode 8 as soon as possible.</span></span>
>
>

#### <a name="usernotifications-framework"></a><span data-ttu-id="e5942-131">Estrutura UserNotifications</span><span class="sxs-lookup"><span data-stu-id="e5942-131">UserNotifications framework</span></span>
<span data-ttu-id="e5942-132">Você precisa adicionar a estrutura `UserNotifications` em suas fases de build.</span><span class="sxs-lookup"><span data-stu-id="e5942-132">You need to add the `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="e5942-133">no Explorador de projeto, abra o painel de projeto e selecione o destino correto.</span><span class="sxs-lookup"><span data-stu-id="e5942-133">in the project explorer, open your project pane and select the correct target.</span></span> <span data-ttu-id="e5942-134">Em seguida, abra a guia **"Compilar fases"** e, no menu **"Link binário com bibliotecas"**, adicione a estrutura `UserNotifications.framework` – defina o link como `Optional`</span><span class="sxs-lookup"><span data-stu-id="e5942-134">Then, open the **"Build phases"** tab and in the **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set the link as `Optional`</span></span>

#### <a name="application-push-capability"></a><span data-ttu-id="e5942-135">Capacidade de envio por push do aplicativo</span><span class="sxs-lookup"><span data-stu-id="e5942-135">Application push capability</span></span>
<span data-ttu-id="e5942-136">O XCode 8 pode redefinir a capacidade de envio por push do aplicativo. Verifique isso novamente na guia `capability` do destino selecionado.</span><span class="sxs-lookup"><span data-stu-id="e5942-136">XCode 8 may reset your app push capability, please double check it in the `capability` tab of your selected target.</span></span>

#### <a name="add-the-new-ios-10-notification-registration-code"></a><span data-ttu-id="e5942-137">Adicionar o novo código de registro de notificação do iOS 10</span><span class="sxs-lookup"><span data-stu-id="e5942-137">Add the new iOS 10 notification registration code</span></span>
<span data-ttu-id="e5942-138">O trecho de código anterior para registrar o aplicativo para as notificações ainda funciona, mas está usando as APIs desaprovadas durante a execução no iOS 10.</span><span class="sxs-lookup"><span data-stu-id="e5942-138">The older code snippet to register the app to notifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="e5942-139">Importe a estrutura `User Notification` :</span><span class="sxs-lookup"><span data-stu-id="e5942-139">Import the `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h>

<span data-ttu-id="e5942-140">No seu método representante do aplicativo `application:didFinishLaunchingWithOptions` , substitua:</span><span class="sxs-lookup"><span data-stu-id="e5942-140">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

        if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
            [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
            [application registerForRemoteNotifications];
        }
        else {

            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }

<span data-ttu-id="e5942-141">por:</span><span class="sxs-lookup"><span data-stu-id="e5942-141">by :</span></span>

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

#### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="e5942-142">Resolver conflitos de delegado UNUserNotificationCenter</span><span class="sxs-lookup"><span data-stu-id="e5942-142">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="e5942-143">*Se o aplicativo nem uma das bibliotecas de terceiros implementar um `UNUserNotificationCenterDelegate`, ignore esta parte.*</span><span class="sxs-lookup"><span data-stu-id="e5942-143">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="e5942-144">Um delegado `UNUserNotificationCenter` é usado pelo SDK para monitorar o ciclo de vida das notificações do Engagement em dispositivos que executam o iOS 10 ou superior.</span><span class="sxs-lookup"><span data-stu-id="e5942-144">A `UNUserNotificationCenter` delegate is used by the SDK to monitor the life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="e5942-145">O SDK tem sua própria implementação do protocolo `UNUserNotificationCenterDelegate`, mas pode haver apenas um delegado `UNUserNotificationCenter` por aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e5942-145">The SDK has its own implementation of the `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="e5942-146">Qualquer outro delegado adicionado ao objeto `UNUserNotificationCenter` entrará em conflito com o do Engagement.</span><span class="sxs-lookup"><span data-stu-id="e5942-146">Any other delegate added to the `UNUserNotificationCenter` object will conflict with the Engagement one.</span></span> <span data-ttu-id="e5942-147">Se o SDK detectar seu delegado ou qualquer delegado de terceiros, ele não usará sua própria implementação, para lhe dar uma chance para resolver os conflitos.</span><span class="sxs-lookup"><span data-stu-id="e5942-147">If the SDK detects your or any other third party's delegate then it will not use its own implementation to give you a chance to resolve the conflicts.</span></span> <span data-ttu-id="e5942-148">Você precisará adicionar a lógica do Engagement ao seu próprio delegado para resolver os conflitos.</span><span class="sxs-lookup"><span data-stu-id="e5942-148">You will have to add the Engagement logic to your own delegate in order to resolve the conflicts.</span></span>

<span data-ttu-id="e5942-149">Há duas maneiras de fazer isso.</span><span class="sxs-lookup"><span data-stu-id="e5942-149">There are two ways to achieve this.</span></span>

<span data-ttu-id="e5942-150">Proposta 1: apenas encaminhando as chamadas do delegado para o SDK:</span><span class="sxs-lookup"><span data-stu-id="e5942-150">Proposal 1, simply by forwarding your delegate calls to the SDK:</span></span>

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

<span data-ttu-id="e5942-151">Ou proposta 2: herdando da classe `AEUserNotificationHandler`</span><span class="sxs-lookup"><span data-stu-id="e5942-151">Or proposal 2, by inheriting from the `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="e5942-152">Você pode determinar se uma notificação vem do Engagement ou não passando seu dicionário `userInfo` para o método da classe `isEngagementPushPayload:` do Agent.</span><span class="sxs-lookup"><span data-stu-id="e5942-152">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary to the Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="e5942-153">Verifique se o delegado do objeto `UNUserNotificationCenter` é definido como seu delegado no método `application:willFinishLaunchingWithOptions:` ou `application:didFinishLaunchingWithOptions:` do delegado do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e5942-153">Make sure that the `UNUserNotificationCenter` object's delegate is set to your delegate within either the `application:willFinishLaunchingWithOptions:` or the `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="e5942-154">Por exemplo, se você implementou a proposta 1 acima:</span><span class="sxs-lookup"><span data-stu-id="e5942-154">For instance, if you implemented the above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }
