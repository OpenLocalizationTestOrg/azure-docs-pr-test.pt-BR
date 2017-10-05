---
title: "Introdução ao Azure Mobile Engagement para iOS em Swift | Microsoft Docs"
description: "Aprenda a usar o Azure Mobile Engagement com Análises e Notificações por Push para Aplicativos iOS."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 196c282d-6f2f-4cbc-aeee-6517c5ad866d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: swift
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: piyushjo
ms.openlocfilehash: 1011b9823333e79a52cd2d187df4f8d063b1f799
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-swift"></a><span data-ttu-id="2d830-103">Introdução ao Azure Mobile Engagement para Aplicativos iOS em Swift</span><span class="sxs-lookup"><span data-stu-id="2d830-103">Get Started with Azure Mobile Engagement for iOS Apps in Swift</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="2d830-104">Este tópico mostra como usar o Azure Mobile Engagement para entender o uso do aplicativo e enviar notificações por push para usuários segmentados para um aplicativo iOS.</span><span class="sxs-lookup"><span data-stu-id="2d830-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users to an iOS application.</span></span>
<span data-ttu-id="2d830-105">Neste tutorial, você cria um aplicativo iOS em branco que coleta dados básicos e recebe notificações por push usando o Sistema de Notificação por Push da Apple (APNS).</span><span class="sxs-lookup"><span data-stu-id="2d830-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="2d830-106">Este tutorial exige o seguinte:</span><span class="sxs-lookup"><span data-stu-id="2d830-106">This tutorial requires the following:</span></span>

* <span data-ttu-id="2d830-107">XCode 8, que pode ser instalado a partir da MAC App Store</span><span class="sxs-lookup"><span data-stu-id="2d830-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="2d830-108">o [SKD do Mobile Engagement iOS]</span><span class="sxs-lookup"><span data-stu-id="2d830-108">the [Mobile Engagement iOS SDK]</span></span>
* <span data-ttu-id="2d830-109">Certificado de notificação por push (. p12), que pode ser obtido no centro de desenvolvimento da Apple</span><span class="sxs-lookup"><span data-stu-id="2d830-109">Push notification certificate (.p12) that you can obtain on your Apple Dev Center</span></span>

> [!NOTE]
> <span data-ttu-id="2d830-110">Este tutorial usa o Swift versão 3.0.</span><span class="sxs-lookup"><span data-stu-id="2d830-110">This tutorial uses Swift version 3.0.</span></span> 
> 
> 

<span data-ttu-id="2d830-111">A conclusão desse tutorial é um pré-requisito para todos os outros tutoriais do Mobile Engagement para os aplicativos iOS.</span><span class="sxs-lookup"><span data-stu-id="2d830-111">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="2d830-112">Para concluir este tutorial, você precisa ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="2d830-112">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="2d830-113">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="2d830-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="2d830-114">Para obter detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).</span><span class="sxs-lookup"><span data-stu-id="2d830-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).</span></span>
> 
> 

## <span data-ttu-id="2d830-115"><a id="setup-azme"></a>Configurar o Mobile Engagement para seu aplicativo iOS</span><span class="sxs-lookup"><span data-stu-id="2d830-115"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="2d830-116"><a id="connecting-app"></a>Conecte o seu aplicativo ao back-end do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="2d830-116"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="2d830-117">Este tutorial apresenta uma "integração básica" que é o conjunto mínimo exigido para coletar dados e enviar uma notificação por push.</span><span class="sxs-lookup"><span data-stu-id="2d830-117">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="2d830-118">A documentação de integração completa pode ser encontrada na [Integração do SDK do iOS no Mobile Engagement](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="2d830-118">The complete integration documentation can be found in the [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="2d830-119">Criaremos um aplicativo básico com XCode para demonstrar a integração:</span><span class="sxs-lookup"><span data-stu-id="2d830-119">We will create a basic app with XCode to demonstrate the integration:</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="2d830-120">Crie um novo projeto iOS</span><span class="sxs-lookup"><span data-stu-id="2d830-120">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="2d830-121">Conecte seu aplicativo ao back-end do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="2d830-121">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="2d830-122">Faça o download do [SKD do Mobile Engagement iOS]</span><span class="sxs-lookup"><span data-stu-id="2d830-122">Download the [Mobile Engagement iOS SDK]</span></span>
2. <span data-ttu-id="2d830-123">Extraia arquivo o arquivo .tar.gz para uma pasta no seu computador</span><span class="sxs-lookup"><span data-stu-id="2d830-123">Extract the .tar.gz file to a folder in your computer</span></span>
3. <span data-ttu-id="2d830-124">Clique com botão direito no projeto e selecione "Adicionar arquivos a..."</span><span class="sxs-lookup"><span data-stu-id="2d830-124">Right click the project and select "Add files to ..."</span></span>
   
    ![][1]
4. <span data-ttu-id="2d830-125">Navegue até a pasta onde você extraiu o SDK e selecione a `EngagementSDK` pasta, então, pressione OK.</span><span class="sxs-lookup"><span data-stu-id="2d830-125">Navigate to the folder where you extracted the SDK and select the `EngagementSDK` folder then press OK.</span></span>
   
    ![][2]
5. <span data-ttu-id="2d830-126">Abra a guia `Build Phases` e no menu `Link Binary With Libraries`, adicione as estruturas, como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="2d830-126">Open the `Build Phases` tab and in the `Link Binary With Libraries` menu add the frameworks as shown below:</span></span>
   
    ![][3]
6. <span data-ttu-id="2d830-127">Crie um cabeçalho Bridging para poder usar as APIs do Objective C do SDK escolhendo Arquivo > Novo > Arquivo > iOS > Fonte > Arquivo de Cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="2d830-127">Create a Bridging header to be able to use the SDK's Objective C APIs by choosing File > New > File > iOS > Source > Header File.</span></span>
   
    ![][4]
7. <span data-ttu-id="2d830-128">Edite o arquivo de cabeçalho ponte para expor o código em Objective-C do Mobile Engagement para o código Swift e adicione as seguintes importações:</span><span class="sxs-lookup"><span data-stu-id="2d830-128">Edit the bridging header file to expose Mobile Engagement Objective-C code to your Swift code, add the following imports :</span></span>
   
        /* Mobile Engagement Agent */
        #import "AEModule.h"
        #import "AEPushMessage.h"
        #import "AEStorage.h"
        #import "EngagementAgent.h"
        #import "EngagementTableViewController.h"
        #import "EngagementViewController.h"
        #import "AEUserNotificationHandler.h"
        #import "AEIdfaProvider.h"
8. <span data-ttu-id="2d830-129">Em Configurações de Compilação, verifique se a definição da compilação do Bridging Header do Objective C em Compilador Swift - Geração de Código tem um caminho para esse cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="2d830-129">Under Build Settings, make sure the Objective-C Bridging Header build setting under Swift Compiler - Code Generation has a path to this header.</span></span> <span data-ttu-id="2d830-130">Aqui está um exemplo de caminho: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (dependendo do caminho)**</span><span class="sxs-lookup"><span data-stu-id="2d830-130">Here is a path example: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (depending on the path)**</span></span>
   
   ![][6]
9. <span data-ttu-id="2d830-131">Volte para o portal do Azure na página *Informações de Conexão* de seu aplicativo e copie a Cadeia de Conexão</span><span class="sxs-lookup"><span data-stu-id="2d830-131">Go back to the Azure portal in your app's *Connection Info* page and copy the Connection String</span></span>
   
   ![][5]
10. <span data-ttu-id="2d830-132">Agora, cole a cadeia de conexão em `didFinishLaunchingWithOptions` delegar</span><span class="sxs-lookup"><span data-stu-id="2d830-132">Now paste the connection string in the `didFinishLaunchingWithOptions` delegate</span></span>
    
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool
        {
              [...]
                EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}")
              [...]
        }

## <span data-ttu-id="2d830-133"><a id="monitor"></a>Habilitar monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="2d830-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
<span data-ttu-id="2d830-134">Para iniciar o envio de dados e assegurar que os usuários estejam ativos, você deve enviar pelo menos uma tela (Atividade) para o back-end do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="2d830-134">In order to start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="2d830-135">Abra o arquivo **ViewController.swift** e substitua a classe base **ViewController** para ser **EngagementViewController**:</span><span class="sxs-lookup"><span data-stu-id="2d830-135">Open the **ViewController.swift** file and replace the base class of **ViewController** to be **EngagementViewController**:</span></span>
   
    `class ViewController : EngagementViewController {`

## <span data-ttu-id="2d830-136"><a id="monitor"></a>Conectar o aplicativo com monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="2d830-136"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="2d830-137"><a id="integrate-push"></a>Habilitar Notificações por Push e mensagens no aplicativo</span><span class="sxs-lookup"><span data-stu-id="2d830-137"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="2d830-138">O Mobile Engagement permite interagir e ENTRAR EM CONTATO com seus usuários com Notificações por Push e Mensagens no Aplicativo no contexto de campanhas.</span><span class="sxs-lookup"><span data-stu-id="2d830-138">Mobile Engagement allows you to interact and REACH with your users with Push Notifications and In-app Messaging in the context of campaigns.</span></span> <span data-ttu-id="2d830-139">Esse módulo é chamado de REACH no portal do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="2d830-139">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="2d830-140">As seções a seguir irão configurar o aplicativo para recebê-los.</span><span class="sxs-lookup"><span data-stu-id="2d830-140">The following sections will setup your app to receive them.</span></span>

### <a name="enable-your-app-to-receive-silent-push-notifications"></a><span data-ttu-id="2d830-141">Habilitar seu aplicativo para receber Notificações por push silenciosas</span><span class="sxs-lookup"><span data-stu-id="2d830-141">Enable your app to receive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-the-reach-library-to-your-project"></a><span data-ttu-id="2d830-142">Adicionar a biblioteca Reach ao seu projeto</span><span class="sxs-lookup"><span data-stu-id="2d830-142">Add the Reach library to your project</span></span>
1. <span data-ttu-id="2d830-143">Clique com botão direito no projeto</span><span class="sxs-lookup"><span data-stu-id="2d830-143">Right click your project</span></span>
2. <span data-ttu-id="2d830-144">Selecione `Add file to ...`</span><span class="sxs-lookup"><span data-stu-id="2d830-144">Select `Add file to ...`</span></span>
3. <span data-ttu-id="2d830-145">Navegue até a pasta onde você extraiu o SDK</span><span class="sxs-lookup"><span data-stu-id="2d830-145">Navigate to the folder where you extracted the SDK</span></span>
4. <span data-ttu-id="2d830-146">Selecione a pasta `EngagementReach`</span><span class="sxs-lookup"><span data-stu-id="2d830-146">Select the `EngagementReach` folder</span></span>
5. <span data-ttu-id="2d830-147">Clique em Adicionar</span><span class="sxs-lookup"><span data-stu-id="2d830-147">Click Add</span></span>
6. <span data-ttu-id="2d830-148">Edite o arquivo de cabeçalho ponte para expor os cabeçalhos de Acesso em Objective-C do Mobile Engagement e adicione as seguintes importações:</span><span class="sxs-lookup"><span data-stu-id="2d830-148">Edit the bridging header file to expose Mobile Engagement Objective-C Reach headers and add the following imports :</span></span>
   
        /* Mobile Engagement Reach */
        #import "AEAnnouncementViewController.h"
        #import "AEAutorotateView.h"
        #import "AEContentViewController.h"
        #import "AEDefaultAnnouncementViewController.h"
        #import "AEDefaultNotifier.h"
        #import "AEDefaultPollViewController.h"
        #import "AEInteractiveContent.h"
        #import "AENotificationView.h"
        #import "AENotifier.h"
        #import "AEPollViewController.h"
        #import "AEReachAbstractAnnouncement.h"
        #import "AEReachAnnouncement.h"
        #import "AEReachContent.h"
        #import "AEReachDataPush.h"
        #import "AEReachDataPushDelegate.h"
        #import "AEReachModule.h"
        #import "AEReachNotifAnnouncement.h"
        #import "AEReachPoll.h"
        #import "AEReachPollQuestion.h"
        #import "AEViewControllerUtil.h"
        #import "AEWebAnnouncementJsBridge.h"

### <a name="modify-your-application-delegate"></a><span data-ttu-id="2d830-149">Modifique seu Representante do Aplicativo</span><span class="sxs-lookup"><span data-stu-id="2d830-149">Modify your Application Delegate</span></span>
1. <span data-ttu-id="2d830-150">Em `didFinishLaunchingWithOptions` - crie um módulo de alcance e transmita-o para a linha de inicialização do Engagement existente:</span><span class="sxs-lookup"><span data-stu-id="2d830-150">Inside  the `didFinishLaunchingWithOptions` -  create a reach module and pass it to your existing Engagement initialization line:</span></span>
   
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool 
        {
            let reach = AEReachModule.module(withNotificationIcon: UIImage(named:"icon.png")) as! AEReachModule
            EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}", modulesArray:[reach])
            [...]
            return true
        }

### <a name="enable-your-app-to-receive-apns-push-notifications"></a><span data-ttu-id="2d830-151">Habilite seu aplicativo para receber Notificações por Push do APNS</span><span class="sxs-lookup"><span data-stu-id="2d830-151">Enable your app to receive APNS Push Notifications</span></span>
1. <span data-ttu-id="2d830-152">Adicione a seguinte linha ao método `didFinishLaunchingWithOptions`:</span><span class="sxs-lookup"><span data-stu-id="2d830-152">Add the following line to the `didFinishLaunchingWithOptions` method:</span></span>
   
        if #available(iOS 8.0, *)
        {
            if #available(iOS 10.0, *)
            {
                UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .badge, .sound]) { (granted, error) in }
            }else
            {
                let settings = UIUserNotificationSettings(types: [.alert, .badge, .sound], categories: nil)
                application.registerUserNotificationSettings(settings)
            }
            application.registerForRemoteNotifications()
        }
        else
        {
            application.registerForRemoteNotifications(matching: [.alert, .badge, .sound])
        }
2. <span data-ttu-id="2d830-153">Adicione o método `didRegisterForRemoteNotificationsWithDeviceToken` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="2d830-153">Add the `didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>
   
        func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
            EngagementAgent.shared().registerDeviceToken(deviceToken)
        }
3. <span data-ttu-id="2d830-154">Adicione o método `didReceiveRemoteNotification:fetchCompletionHandler:` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="2d830-154">Add the `didReceiveRemoteNotification:fetchCompletionHandler:` method as follows:</span></span>
   
        func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
            EngagementAgent.shared().applicationDidReceiveRemoteNotification(userInfo, fetchCompletionHandler:completionHandler)
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
<span data-ttu-id="2d830-155">[SKD do Mobile Engagement iOS]: http://aka.ms/qk2rnj</span><span class="sxs-lookup"><span data-stu-id="2d830-155">[Mobile Engagement iOS SDK]: http://aka.ms/qk2rnj</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-swift-get-started/add-header-file.png
[5]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
[6]: ./media/mobile-engagement-ios-swift-get-started/add-bridging-header.png
