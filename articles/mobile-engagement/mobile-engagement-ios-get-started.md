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
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-objective-c"></a><span data-ttu-id="a0882-103">Introdução ao Azure Mobile Engagement para aplicativos iOS em Objective C</span><span class="sxs-lookup"><span data-stu-id="a0882-103">Get Started with Azure Mobile Engagement for iOS apps in Objective C</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="a0882-104">Este tópico mostra como toouse do Azure Mobile Engagement toounderstand seu uso do aplicativo e enviar por push o aplicativo do iOS notificações toosegmented usuários tooan.</span><span class="sxs-lookup"><span data-stu-id="a0882-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users tooan iOS application.</span></span>
<span data-ttu-id="a0882-105">Neste tutorial, você cria um aplicativo iOS em branco que coleta dados básicos e recebe notificações por push usando o Sistema de Notificação por Push da Apple (APNS).</span><span class="sxs-lookup"><span data-stu-id="a0882-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="a0882-106">Este tutorial requer o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="a0882-106">This tutorial requires hello following:</span></span>

* <span data-ttu-id="a0882-107">XCode 8, que pode ser instalado a partir da MAC App Store</span><span class="sxs-lookup"><span data-stu-id="a0882-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="a0882-108">Olá [SDK do Mobile Engagement iOS]</span><span class="sxs-lookup"><span data-stu-id="a0882-108">hello [Mobile Engagement iOS SDK]</span></span>

<span data-ttu-id="a0882-109">A conclusão desse tutorial é um pré-requisito para todos os outros tutoriais do Mobile Engagement para os aplicativos iOS.</span><span class="sxs-lookup"><span data-stu-id="a0882-109">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="a0882-110">toocomplete neste tutorial, você deve ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0882-110">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="a0882-111">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="a0882-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a0882-112">Para obter detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="a0882-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span></span>
>
>

## <span data-ttu-id="a0882-113"><a id="setup-azme"></a>Configurar o Mobile Engagement para seu aplicativo iOS</span><span class="sxs-lookup"><span data-stu-id="a0882-113"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="a0882-114"><a id="connecting-app"></a>Conectar seu back-end do aplicativo toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="a0882-114"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="a0882-115">Este tutorial apresenta uma "integração básica", que é Olá mínimo definido toocollect necessários dados e envia uma notificação por push.</span><span class="sxs-lookup"><span data-stu-id="a0882-115">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="a0882-116">documentação de integração completa Olá pode ser encontrada no hello [integração do SDK do Mobile Engagement iOS](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a0882-116">hello complete integration documentation can be found in hello [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="a0882-117">Vamos criar um aplicativo básico com a integração do XCode toodemonstrate hello.</span><span class="sxs-lookup"><span data-stu-id="a0882-117">We will create a basic app with XCode toodemonstrate hello integration.</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="a0882-118">Crie um novo projeto iOS</span><span class="sxs-lookup"><span data-stu-id="a0882-118">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a><span data-ttu-id="a0882-119">Conectar seu back-end do aplicativo toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="a0882-119">Connect your app toohello Mobile Engagement backend</span></span>
1. <span data-ttu-id="a0882-120">Baixar Olá [SDK do Mobile Engagement iOS].</span><span class="sxs-lookup"><span data-stu-id="a0882-120">Download hello [Mobile Engagement iOS SDK].</span></span>
2. <span data-ttu-id="a0882-121">Extrair hello. gz arquivo tooa pasta no seu computador.</span><span class="sxs-lookup"><span data-stu-id="a0882-121">Extract hello .tar.gz file tooa folder in your computer.</span></span>
3. <span data-ttu-id="a0882-122">Clique com botão direito hello e, em seguida, selecione **adicionar arquivos ao**.</span><span class="sxs-lookup"><span data-stu-id="a0882-122">Right-click hello project, and then select **Add files to**.</span></span>

    ![][1]
4. <span data-ttu-id="a0882-123">Navegue toohello pasta onde você extraiu Olá SDK, selecione Olá `EngagementSDK` pasta, clique em **opções** na Olá canto inferior esquerdo e verifique se essa caixa de seleção Olá **copiar itens se necessário** e hello caixa de seleção para o seu destino são verificados e pressione **Okey**.</span><span class="sxs-lookup"><span data-stu-id="a0882-123">Navigate toohello folder where you extracted hello SDK, select hello `EngagementSDK` folder, click **Options** on hello bottom left corner and make sure that hello checkbox **Copy items if needed** and hello checkbox for your target are checked then press **OK**.</span></span>

    ![][2]
5. <span data-ttu-id="a0882-124">Olá abrir **fases de compilação** guia e em hello **Link binário com bibliotecas** menu Adicionar estruturas de hello, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="a0882-124">Open hello **Build Phases** tab, and in hello **Link Binary With Libraries** menu, add hello frameworks as shown below:</span></span>

    ![][3]
6. <span data-ttu-id="a0882-125">Voltar toohello portal do Azure em seu aplicativo **informações de Conexão** página e copie a cadeia de conexão hello.</span><span class="sxs-lookup"><span data-stu-id="a0882-125">Go back toohello Azure portal in your app's **Connection Info** page and copy hello connection string.</span></span>

    ![][4]
7. <span data-ttu-id="a0882-126">Adicionar Olá a seguinte linha de código no seu **appdelegate. M** arquivo.</span><span class="sxs-lookup"><span data-stu-id="a0882-126">Add hello following line of code in your **AppDelegate.m** file.</span></span>

        #import "EngagementAgent.h"
8. <span data-ttu-id="a0882-127">Agora cole a cadeia de caracteres de conexão de saudação em Olá `didFinishLaunchingWithOptions` delegate.</span><span class="sxs-lookup"><span data-stu-id="a0882-127">Now paste hello connection string in hello `didFinishLaunchingWithOptions` delegate.</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
              [...]   
              [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
              [...]
        }
9. <span data-ttu-id="a0882-128">`setTestLogEnabled`é uma instrução opcional que permite que os logs do SDK para você tooidentify problemas.</span><span class="sxs-lookup"><span data-stu-id="a0882-128">`setTestLogEnabled` is an optional statement which enables SDK logs for you tooidentify issues.</span></span>

## <span data-ttu-id="a0882-129"><a id="monitor"></a>Habilitar monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="a0882-129"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="a0882-130">Em ordem toostart enviar dados e garantir que os usuários de saudação estão ativos, você deve enviar pelo menos uma tela (atividade) toohello Mobile Engagement backend.</span><span class="sxs-lookup"><span data-stu-id="a0882-130">In order toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="a0882-131">Olá abrir **ViewController.h** de arquivo e importar **EngagementViewController.h**:</span><span class="sxs-lookup"><span data-stu-id="a0882-131">Open hello **ViewController.h** file and import **EngagementViewController.h**:</span></span>

    `#import "EngagementViewController.h"`
2. <span data-ttu-id="a0882-132">Agora substitua superclasse Olá de saudação **ViewController** interface por `EngagementViewController`:</span><span class="sxs-lookup"><span data-stu-id="a0882-132">Now replace hello super class of hello **ViewController** interface by `EngagementViewController`:</span></span>

    `@interface ViewController : EngagementViewController`

## <span data-ttu-id="a0882-133"><a id="monitor"></a>Conectar o aplicativo com monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="a0882-133"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="a0882-134"><a id="integrate-push"></a>Habilitar notificações por push e mensagens no aplicativo</span><span class="sxs-lookup"><span data-stu-id="a0882-134"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="a0882-135">Mobile Engagement permite toointeract com os usuários e o alcance com notificações por push e no aplicativo mensagens no contexto de saudação de campanhas.</span><span class="sxs-lookup"><span data-stu-id="a0882-135">Mobile Engagement allows you toointeract with your users and REACH with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="a0882-136">Esse módulo é chamado alcance no portal do Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="a0882-136">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="a0882-137">Olá seções a seguir configurar seu aplicativo tooreceive-los.</span><span class="sxs-lookup"><span data-stu-id="a0882-137">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="a0882-138">Habilitar seu aplicativo tooreceive silenciosa notificações por Push</span><span class="sxs-lookup"><span data-stu-id="a0882-138">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a><span data-ttu-id="a0882-139">Adicionar Olá alcance biblioteca tooyour projeto</span><span class="sxs-lookup"><span data-stu-id="a0882-139">Add hello Reach library tooyour project</span></span>
1. <span data-ttu-id="a0882-140">Clique com o botão direito em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="a0882-140">Right-click your project.</span></span>
2. <span data-ttu-id="a0882-141">Selecione **Adicionar arquivo a**.</span><span class="sxs-lookup"><span data-stu-id="a0882-141">Select **Add file to**.</span></span>
3. <span data-ttu-id="a0882-142">Navegue toohello pasta onde você extraiu Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="a0882-142">Navigate toohello folder where you extracted hello SDK.</span></span>
4. <span data-ttu-id="a0882-143">Selecione Olá `EngagementReach` pasta.</span><span class="sxs-lookup"><span data-stu-id="a0882-143">Select hello `EngagementReach` folder.</span></span>
5. <span data-ttu-id="a0882-144">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a0882-144">Click **Add**.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="a0882-145">Modifique seu Representante do Aplicativo</span><span class="sxs-lookup"><span data-stu-id="a0882-145">Modify your Application Delegate</span></span>
1. <span data-ttu-id="a0882-146">Em **AppDeletegate.m** de arquivos, importar Olá contrato alcançar módulo.</span><span class="sxs-lookup"><span data-stu-id="a0882-146">Back in **AppDeletegate.m** file, import hello Engagement Reach module.</span></span>

        #import "AEReachModule.h"
        #import <UserNotifications/UserNotifications.h>
2. <span data-ttu-id="a0882-147">Olá interna `application:didFinishLaunchingWithOptions` método, crie um módulo de alcance e passá-lo tooyour linha de inicialização contrato existente:</span><span class="sxs-lookup"><span data-stu-id="a0882-147">Inside hello `application:didFinishLaunchingWithOptions` method, create a Reach module and pass it tooyour existing Engagement initialization line:</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
            AEReachModule * reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
            [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
            [...]
            return YES;
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a><span data-ttu-id="a0882-148">Habilitar seu aplicativo tooreceive notificações por Push do APNS</span><span class="sxs-lookup"><span data-stu-id="a0882-148">Enable your app tooreceive APNS Push Notifications</span></span>
1. <span data-ttu-id="a0882-149">Adicionar Olá toohello linha a seguir `application:didFinishLaunchingWithOptions` método:</span><span class="sxs-lookup"><span data-stu-id="a0882-149">Add hello following line toohello `application:didFinishLaunchingWithOptions` method:</span></span>

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
2. <span data-ttu-id="a0882-150">Adicionar Olá `application:didRegisterForRemoteNotificationsWithDeviceToken` método da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="a0882-150">Add hello `application:didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>

        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
        {
             [[EngagementAgent shared] registerDeviceToken:deviceToken];
            NSLog(@"Registered Token: %@", deviceToken);
        }
3. <span data-ttu-id="a0882-151">Adicionar Olá `didFailToRegisterForRemoteNotificationsWithError` método da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="a0882-151">Add hello `didFailToRegisterForRemoteNotificationsWithError` method as follows:</span></span>

        - (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error
        {
           NSLog(@"Failed tooget token, error: %@", error);
        }
4. <span data-ttu-id="a0882-152">Adicionar Olá `didReceiveRemoteNotification:fetchCompletionHandler` método da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="a0882-152">Add hello `didReceiveRemoteNotification:fetchCompletionHandler` method as follows:</span></span>

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
