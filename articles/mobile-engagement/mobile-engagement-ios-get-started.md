---
title: "Introdução ao Azure Mobile Engagement para iOS em Objective C | Microsoft Docs"
description: "Aprenda a usar o Azure Mobile Engagement com análises e notificações por push para aplicativos iOS."
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
ms.openlocfilehash: 1b87a2ebb35b31ee3d3139ecead6267e62eb1033
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-objective-c"></a><span data-ttu-id="8939f-103">Introdução ao Azure Mobile Engagement para aplicativos iOS em Objective C</span><span class="sxs-lookup"><span data-stu-id="8939f-103">Get Started with Azure Mobile Engagement for iOS apps in Objective C</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="8939f-104">Este tópico mostra como usar o Azure Mobile Engagement para entender o uso do aplicativo e enviar notificações por push para usuários segmentados para um aplicativo iOS.</span><span class="sxs-lookup"><span data-stu-id="8939f-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users to an iOS application.</span></span>
<span data-ttu-id="8939f-105">Neste tutorial, você cria um aplicativo iOS em branco que coleta dados básicos e recebe notificações por push usando o Sistema de Notificação por Push da Apple (APNS).</span><span class="sxs-lookup"><span data-stu-id="8939f-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="8939f-106">Este tutorial exige o seguinte:</span><span class="sxs-lookup"><span data-stu-id="8939f-106">This tutorial requires the following:</span></span>

* <span data-ttu-id="8939f-107">XCode 8, que pode ser instalado a partir da MAC App Store</span><span class="sxs-lookup"><span data-stu-id="8939f-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="8939f-108">o [SKD do Mobile Engagement iOS]</span><span class="sxs-lookup"><span data-stu-id="8939f-108">the [Mobile Engagement iOS SDK]</span></span>

<span data-ttu-id="8939f-109">A conclusão desse tutorial é um pré-requisito para todos os outros tutoriais do Mobile Engagement para os aplicativos iOS.</span><span class="sxs-lookup"><span data-stu-id="8939f-109">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="8939f-110">Para concluir este tutorial, você precisa ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="8939f-110">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="8939f-111">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="8939f-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="8939f-112">Para obter detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="8939f-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span></span>
>
>

## <span data-ttu-id="8939f-113"><a id="setup-azme"></a>Configurar o Mobile Engagement para seu aplicativo iOS</span><span class="sxs-lookup"><span data-stu-id="8939f-113"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="8939f-114"><a id="connecting-app"></a>Conecte o seu aplicativo ao back-end do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="8939f-114"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="8939f-115">Este tutorial apresenta uma "integração básica" que é o conjunto mínimo exigido para coletar dados e enviar uma notificação por push.</span><span class="sxs-lookup"><span data-stu-id="8939f-115">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="8939f-116">A documentação de integração completa pode ser encontrada na [integração do SDK do iOS do Mobile Engagement](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="8939f-116">The complete integration documentation can be found in the [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="8939f-117">Criaremos um aplicativo básico com XCode para demonstrar a integração.</span><span class="sxs-lookup"><span data-stu-id="8939f-117">We will create a basic app with XCode to demonstrate the integration.</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="8939f-118">Crie um novo projeto iOS</span><span class="sxs-lookup"><span data-stu-id="8939f-118">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-to-the-mobile-engagement-backend"></a><span data-ttu-id="8939f-119">Conecte o seu aplicativo ao back-end do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="8939f-119">Connect your app to the Mobile Engagement backend</span></span>
1. <span data-ttu-id="8939f-120">Faça o download do [SKD do Mobile Engagement iOS].</span><span class="sxs-lookup"><span data-stu-id="8939f-120">Download the [Mobile Engagement iOS SDK].</span></span>
2. <span data-ttu-id="8939f-121">Extraia o arquivo .tar.gz para uma pasta no seu computador.</span><span class="sxs-lookup"><span data-stu-id="8939f-121">Extract the .tar.gz file to a folder in your computer.</span></span>
3. <span data-ttu-id="8939f-122">Clique com o botão direito do mouse no projeto e selecione **Adicionar arquivos a**.</span><span class="sxs-lookup"><span data-stu-id="8939f-122">Right-click the project, and then select **Add files to**.</span></span>

    ![][1]
4. <span data-ttu-id="8939f-123">Navegue até a pasta onde você extraiu o SDK, selecione a pasta `EngagementSDK`, clique em **Opções** no canto inferior esquerdo e verifique se a caixa de seleção **Copiar itens se necessário** e a caixa de seleção para o seu destino são verificadas e, em seguida, pressione **Ok**.</span><span class="sxs-lookup"><span data-stu-id="8939f-123">Navigate to the folder where you extracted the SDK, select the `EngagementSDK` folder, click **Options** on the bottom left corner and make sure that the checkbox **Copy items if needed** and the checkbox for your target are checked then press **OK**.</span></span>

    ![][2]
5. <span data-ttu-id="8939f-124">Abra a guia **Fases da Compilação** e no menu **Vincular Binário a Bibliotecas**, adicione as estruturas, como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="8939f-124">Open the **Build Phases** tab, and in the **Link Binary With Libraries** menu, add the frameworks as shown below:</span></span>

    ![][3]
6. <span data-ttu-id="8939f-125">Volte para o portal do Azure na página **Informações de Conexão** de seu aplicativo e copie a cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="8939f-125">Go back to the Azure portal in your app's **Connection Info** page and copy the connection string.</span></span>

    ![][4]
7. <span data-ttu-id="8939f-126">Adicione a linha de código a seguir a seu arquivo **AppDelegate.m** .</span><span class="sxs-lookup"><span data-stu-id="8939f-126">Add the following line of code in your **AppDelegate.m** file.</span></span>

        #import "EngagementAgent.h"
8. <span data-ttu-id="8939f-127">Agora, cole a cadeia de conexão no representante `didFinishLaunchingWithOptions` .</span><span class="sxs-lookup"><span data-stu-id="8939f-127">Now paste the connection string in the `didFinishLaunchingWithOptions` delegate.</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
              [...]   
              [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
              [...]
        }
9. <span data-ttu-id="8939f-128">`setTestLogEnabled` é uma instrução opcional que habilita os logs do SDK para que você possa identificar problemas.</span><span class="sxs-lookup"><span data-stu-id="8939f-128">`setTestLogEnabled` is an optional statement which enables SDK logs for you to identify issues.</span></span>

## <span data-ttu-id="8939f-129"><a id="monitor"></a>Habilitar monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="8939f-129"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="8939f-130">Para iniciar o envio de dados e assegurar que os usuários estejam ativos, você deve enviar pelo menos uma tela (Atividade) para o back-end do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="8939f-130">In order to start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="8939f-131">Abra o arquivo **viewcontroller.h** e importe **EngagementViewController.h**:</span><span class="sxs-lookup"><span data-stu-id="8939f-131">Open the **ViewController.h** file and import **EngagementViewController.h**:</span></span>

    `#import "EngagementViewController.h"`
2. <span data-ttu-id="8939f-132">Agora, substitua a superclasse da interface **ViewController** por `EngagementViewController`:</span><span class="sxs-lookup"><span data-stu-id="8939f-132">Now replace the super class of the **ViewController** interface by `EngagementViewController`:</span></span>

    `@interface ViewController : EngagementViewController`

## <span data-ttu-id="8939f-133"><a id="monitor"></a>Conectar o aplicativo com monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="8939f-133"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="8939f-134"><a id="integrate-push"></a>Habilitar notificações por push e mensagens no aplicativo</span><span class="sxs-lookup"><span data-stu-id="8939f-134"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="8939f-135">O Mobile Engagement permite interagir com seus usuários e o REACH com notificações por push e mensagens no aplicativo no contexto das campanhas.</span><span class="sxs-lookup"><span data-stu-id="8939f-135">Mobile Engagement allows you to interact with your users and REACH with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="8939f-136">Esse módulo é chamado de REACH no portal do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="8939f-136">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="8939f-137">As seções a seguir configuram seu aplicativo para recebê-las.</span><span class="sxs-lookup"><span data-stu-id="8939f-137">The following sections set up your app to receive them.</span></span>

### <a name="enable-your-app-to-receive-silent-push-notifications"></a><span data-ttu-id="8939f-138">Habilitar seu aplicativo para receber Notificações por push silenciosas</span><span class="sxs-lookup"><span data-stu-id="8939f-138">Enable your app to receive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-the-reach-library-to-your-project"></a><span data-ttu-id="8939f-139">Adicionar a biblioteca Reach ao seu projeto</span><span class="sxs-lookup"><span data-stu-id="8939f-139">Add the Reach library to your project</span></span>
1. <span data-ttu-id="8939f-140">Clique com o botão direito em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="8939f-140">Right-click your project.</span></span>
2. <span data-ttu-id="8939f-141">Selecione **Adicionar arquivo a**.</span><span class="sxs-lookup"><span data-stu-id="8939f-141">Select **Add file to**.</span></span>
3. <span data-ttu-id="8939f-142">Navegue até a pasta onde você extraiu o SDK.</span><span class="sxs-lookup"><span data-stu-id="8939f-142">Navigate to the folder where you extracted the SDK.</span></span>
4. <span data-ttu-id="8939f-143">Selecione a pasta `EngagementReach` .</span><span class="sxs-lookup"><span data-stu-id="8939f-143">Select the `EngagementReach` folder.</span></span>
5. <span data-ttu-id="8939f-144">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8939f-144">Click **Add**.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="8939f-145">Modifique seu Representante do Aplicativo</span><span class="sxs-lookup"><span data-stu-id="8939f-145">Modify your Application Delegate</span></span>
1. <span data-ttu-id="8939f-146">De volta ao arquivo **AppDeletegate.m** , importe o módulo Engagement Reach.</span><span class="sxs-lookup"><span data-stu-id="8939f-146">Back in **AppDeletegate.m** file, import the Engagement Reach module.</span></span>

        #import "AEReachModule.h"
        #import <UserNotifications/UserNotifications.h>
2. <span data-ttu-id="8939f-147">No método `application:didFinishLaunchingWithOptions` , crie um módulo Reach e passe-o para sua linha de inicialização do Engagement existente:</span><span class="sxs-lookup"><span data-stu-id="8939f-147">Inside the `application:didFinishLaunchingWithOptions` method, create a Reach module and pass it to your existing Engagement initialization line:</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
            AEReachModule * reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
            [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
            [...]
            return YES;
        }

### <a name="enable-your-app-to-receive-apns-push-notifications"></a><span data-ttu-id="8939f-148">Habilite seu aplicativo para receber Notificações por Push do APNS</span><span class="sxs-lookup"><span data-stu-id="8939f-148">Enable your app to receive APNS Push Notifications</span></span>
1. <span data-ttu-id="8939f-149">Adicione a seguinte linha ao método `application:didFinishLaunchingWithOptions`:</span><span class="sxs-lookup"><span data-stu-id="8939f-149">Add the following line to the `application:didFinishLaunchingWithOptions` method:</span></span>

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
2. <span data-ttu-id="8939f-150">Adicione o método `application:didRegisterForRemoteNotificationsWithDeviceToken` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="8939f-150">Add the `application:didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>

        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
        {
             [[EngagementAgent shared] registerDeviceToken:deviceToken];
            NSLog(@"Registered Token: %@", deviceToken);
        }
3. <span data-ttu-id="8939f-151">Adicione o método `didFailToRegisterForRemoteNotificationsWithError` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="8939f-151">Add the `didFailToRegisterForRemoteNotificationsWithError` method as follows:</span></span>

        - (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error
        {
           NSLog(@"Failed to get token, error: %@", error);
        }
4. <span data-ttu-id="8939f-152">Adicione o método `didReceiveRemoteNotification:fetchCompletionHandler` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="8939f-152">Add the `didReceiveRemoteNotification:fetchCompletionHandler` method as follows:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
        {
            [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
<span data-ttu-id="8939f-153">[SKD do Mobile Engagement iOS]: http://aka.ms/qk2rnj</span><span class="sxs-lookup"><span data-stu-id="8939f-153">[Mobile Engagement iOS SDK]: http://aka.ms/qk2rnj</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
