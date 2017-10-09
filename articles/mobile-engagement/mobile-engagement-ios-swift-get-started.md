---
title: aaaGet iniciado com o Azure Mobile Engagement para iOS no Swift | Microsoft Docs
description: "Saiba como toouse Azure Mobile Engagement com análises e notificações por Push para aplicativos do iOS."
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
ms.openlocfilehash: 9a3841d305745f8b80c6b0c86aabe18e0c7c0e59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-swift"></a><span data-ttu-id="40616-103">Introdução ao Azure Mobile Engagement para Aplicativos iOS em Swift</span><span class="sxs-lookup"><span data-stu-id="40616-103">Get Started with Azure Mobile Engagement for iOS Apps in Swift</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="40616-104">Este tópico mostra como toouse do Azure Mobile Engagement toounderstand seu uso do aplicativo e enviar por push o aplicativo do iOS notificações toosegmented usuários tooan.</span><span class="sxs-lookup"><span data-stu-id="40616-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users tooan iOS application.</span></span>
<span data-ttu-id="40616-105">Neste tutorial, você cria um aplicativo iOS em branco que coleta dados básicos e recebe notificações por push usando o Sistema de Notificação por Push da Apple (APNS).</span><span class="sxs-lookup"><span data-stu-id="40616-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="40616-106">Este tutorial requer o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="40616-106">This tutorial requires hello following:</span></span>

* <span data-ttu-id="40616-107">XCode 8, que pode ser instalado a partir da MAC App Store</span><span class="sxs-lookup"><span data-stu-id="40616-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="40616-108">Olá [SDK do Mobile Engagement iOS]</span><span class="sxs-lookup"><span data-stu-id="40616-108">hello [Mobile Engagement iOS SDK]</span></span>
* <span data-ttu-id="40616-109">Certificado de notificação por push (. p12), que pode ser obtido no centro de desenvolvimento da Apple</span><span class="sxs-lookup"><span data-stu-id="40616-109">Push notification certificate (.p12) that you can obtain on your Apple Dev Center</span></span>

> [!NOTE]
> <span data-ttu-id="40616-110">Este tutorial usa o Swift versão 3.0.</span><span class="sxs-lookup"><span data-stu-id="40616-110">This tutorial uses Swift version 3.0.</span></span> 
> 
> 

<span data-ttu-id="40616-111">A conclusão desse tutorial é um pré-requisito para todos os outros tutoriais do Mobile Engagement para os aplicativos iOS.</span><span class="sxs-lookup"><span data-stu-id="40616-111">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="40616-112">toocomplete neste tutorial, você deve ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="40616-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="40616-113">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="40616-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="40616-114">Para obter detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).</span><span class="sxs-lookup"><span data-stu-id="40616-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).</span></span>
> 
> 

## <span data-ttu-id="40616-115"><a id="setup-azme"></a>Configurar o Mobile Engagement para seu aplicativo iOS</span><span class="sxs-lookup"><span data-stu-id="40616-115"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="40616-116"><a id="connecting-app"></a>Conectar seu back-end do aplicativo toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="40616-116"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="40616-117">Este tutorial apresenta uma "integração básica", que é Olá mínimo definido toocollect necessários dados e envia uma notificação por push.</span><span class="sxs-lookup"><span data-stu-id="40616-117">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="40616-118">documentação de integração completa Olá pode ser encontrada no hello [integração do SDK do Mobile Engagement iOS](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="40616-118">hello complete integration documentation can be found in hello [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="40616-119">Vamos criar um aplicativo básico com a integração de saudação do XCode toodemonstrate:</span><span class="sxs-lookup"><span data-stu-id="40616-119">We will create a basic app with XCode toodemonstrate hello integration:</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="40616-120">Crie um novo projeto iOS</span><span class="sxs-lookup"><span data-stu-id="40616-120">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="40616-121">Conectar seu back-end do aplicativo tooMobile contrato</span><span class="sxs-lookup"><span data-stu-id="40616-121">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="40616-122">Baixar Olá [SDK do Mobile Engagement iOS]</span><span class="sxs-lookup"><span data-stu-id="40616-122">Download hello [Mobile Engagement iOS SDK]</span></span>
2. <span data-ttu-id="40616-123">Extrair hello. gz arquivo tooa pasta no seu computador</span><span class="sxs-lookup"><span data-stu-id="40616-123">Extract hello .tar.gz file tooa folder in your computer</span></span>
3. <span data-ttu-id="40616-124">Projeto Olá clique com botão direito e selecione "Adicionar arquivos muito..."</span><span class="sxs-lookup"><span data-stu-id="40616-124">Right click hello project and select "Add files too..."</span></span>
   
    ![][1]
4. <span data-ttu-id="40616-125">Navegue toohello pasta onde você extraiu hello SDK e selecione Olá `EngagementSDK` pasta e pressione Okey.</span><span class="sxs-lookup"><span data-stu-id="40616-125">Navigate toohello folder where you extracted hello SDK and select hello `EngagementSDK` folder then press OK.</span></span>
   
    ![][2]
5. <span data-ttu-id="40616-126">Olá abrir `Build Phases` guia e na Olá `Link Binary With Libraries` menu Adicionar estruturas de hello, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="40616-126">Open hello `Build Phases` tab and in hello `Link Binary With Libraries` menu add hello frameworks as shown below:</span></span>
   
    ![][3]
6. <span data-ttu-id="40616-127">Criar um ponte de cabeçalho toobe toouse capaz de saudação do objetivo C APIs do SDK escolhendo Arquivo > Novo > arquivo > iOS > fonte > arquivo de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="40616-127">Create a Bridging header toobe able toouse hello SDK's Objective C APIs by choosing File > New > File > iOS > Source > Header File.</span></span>
   
    ![][4]
7. <span data-ttu-id="40616-128">Editar saudação ponte cabeçalho arquivo tooexpose Mobile Engagement Objective-C código tooyour código Swift, adicione Olá importa a seguir:</span><span class="sxs-lookup"><span data-stu-id="40616-128">Edit hello bridging header file tooexpose Mobile Engagement Objective-C code tooyour Swift code, add hello following imports :</span></span>
   
        /* Mobile Engagement Agent */
        #import "AEModule.h"
        #import "AEPushMessage.h"
        #import "AEStorage.h"
        #import "EngagementAgent.h"
        #import "EngagementTableViewController.h"
        #import "EngagementViewController.h"
        #import "AEUserNotificationHandler.h"
        #import "AEIdfaProvider.h"
8. <span data-ttu-id="40616-129">Em configurações da compilação, certifique-se de saudação configuração em compilador Swift - geração de código de compilação de cabeçalho de ponte Objective-C tem um cabeçalho de toothis de caminho.</span><span class="sxs-lookup"><span data-stu-id="40616-129">Under Build Settings, make sure hello Objective-C Bridging Header build setting under Swift Compiler - Code Generation has a path toothis header.</span></span> <span data-ttu-id="40616-130">Aqui está um exemplo de caminho: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (dependendo do caminho de saudação)**</span><span class="sxs-lookup"><span data-stu-id="40616-130">Here is a path example: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (depending on hello path)**</span></span>
   
   ![][6]
9. <span data-ttu-id="40616-131">Voltar toohello portal do Azure em seu aplicativo *informações de Conexão* Olá página e copie a cadeia de caracteres de Conexão</span><span class="sxs-lookup"><span data-stu-id="40616-131">Go back toohello Azure portal in your app's *Connection Info* page and copy hello Connection String</span></span>
   
   ![][5]
10. <span data-ttu-id="40616-132">Agora cole a cadeia de caracteres de conexão de saudação em Olá `didFinishLaunchingWithOptions` delegar</span><span class="sxs-lookup"><span data-stu-id="40616-132">Now paste hello connection string in hello `didFinishLaunchingWithOptions` delegate</span></span>
    
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool
        {
              [...]
                EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}")
              [...]
        }

## <span data-ttu-id="40616-133"><a id="monitor"></a>Habilitar monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="40616-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
<span data-ttu-id="40616-134">Em ordem toostart enviar dados e garantir que os usuários de saudação estão ativos, você deve enviar pelo menos uma tela (atividade) toohello Mobile Engagement backend.</span><span class="sxs-lookup"><span data-stu-id="40616-134">In order toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="40616-135">Olá abrir **ViewController.swift** de arquivo e substitua a classe base Olá de **ViewController** toobe **EngagementViewController**:</span><span class="sxs-lookup"><span data-stu-id="40616-135">Open hello **ViewController.swift** file and replace hello base class of **ViewController** toobe **EngagementViewController**:</span></span>
   
    `class ViewController : EngagementViewController {`

## <span data-ttu-id="40616-136"><a id="monitor"></a>Conectar o aplicativo com monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="40616-136"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="40616-137"><a id="integrate-push"></a>Habilitar Notificações por Push e mensagens no aplicativo</span><span class="sxs-lookup"><span data-stu-id="40616-137"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="40616-138">Mobile Engagement permite toointeract e alcance com os usuários com notificações por Push e no aplicativo de mensagens no contexto de saudação de campanhas.</span><span class="sxs-lookup"><span data-stu-id="40616-138">Mobile Engagement allows you toointeract and REACH with your users with Push Notifications and In-app Messaging in hello context of campaigns.</span></span> <span data-ttu-id="40616-139">Esse módulo é chamado alcance no portal do Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="40616-139">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="40616-140">Olá seções a seguir irá configurar seu aplicativo tooreceive-los.</span><span class="sxs-lookup"><span data-stu-id="40616-140">hello following sections will setup your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="40616-141">Habilitar seu aplicativo tooreceive silenciosa notificações por Push</span><span class="sxs-lookup"><span data-stu-id="40616-141">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a><span data-ttu-id="40616-142">Adicionar Olá alcance biblioteca tooyour projeto</span><span class="sxs-lookup"><span data-stu-id="40616-142">Add hello Reach library tooyour project</span></span>
1. <span data-ttu-id="40616-143">Clique com botão direito no projeto</span><span class="sxs-lookup"><span data-stu-id="40616-143">Right click your project</span></span>
2. <span data-ttu-id="40616-144">Selecione `Add file too...`</span><span class="sxs-lookup"><span data-stu-id="40616-144">Select `Add file too...`</span></span>
3. <span data-ttu-id="40616-145">Navegue toohello pasta onde você extraiu Olá SDK</span><span class="sxs-lookup"><span data-stu-id="40616-145">Navigate toohello folder where you extracted hello SDK</span></span>
4. <span data-ttu-id="40616-146">Selecione Olá `EngagementReach` pasta</span><span class="sxs-lookup"><span data-stu-id="40616-146">Select hello `EngagementReach` folder</span></span>
5. <span data-ttu-id="40616-147">Clique em Adicionar</span><span class="sxs-lookup"><span data-stu-id="40616-147">Click Add</span></span>
6. <span data-ttu-id="40616-148">Editar saudação ponte cabeçalhos de alcance do Mobile Engagement Objective-C do cabeçalho arquivo tooexpose e adicione Olá importa a seguir:</span><span class="sxs-lookup"><span data-stu-id="40616-148">Edit hello bridging header file tooexpose Mobile Engagement Objective-C Reach headers and add hello following imports :</span></span>
   
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

### <a name="modify-your-application-delegate"></a><span data-ttu-id="40616-149">Modifique seu Representante do Aplicativo</span><span class="sxs-lookup"><span data-stu-id="40616-149">Modify your Application Delegate</span></span>
1. <span data-ttu-id="40616-150">Olá interna `didFinishLaunchingWithOptions` - criar um módulo de alcance e passá-lo tooyour linha de inicialização contrato existente:</span><span class="sxs-lookup"><span data-stu-id="40616-150">Inside  hello `didFinishLaunchingWithOptions` -  create a reach module and pass it tooyour existing Engagement initialization line:</span></span>
   
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool 
        {
            let reach = AEReachModule.module(withNotificationIcon: UIImage(named:"icon.png")) as! AEReachModule
            EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}", modulesArray:[reach])
            [...]
            return true
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a><span data-ttu-id="40616-151">Habilitar seu aplicativo tooreceive notificações por Push do APNS</span><span class="sxs-lookup"><span data-stu-id="40616-151">Enable your app tooreceive APNS Push Notifications</span></span>
1. <span data-ttu-id="40616-152">Adicionar Olá toohello linha a seguir `didFinishLaunchingWithOptions` método:</span><span class="sxs-lookup"><span data-stu-id="40616-152">Add hello following line toohello `didFinishLaunchingWithOptions` method:</span></span>
   
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
2. <span data-ttu-id="40616-153">Adicionar Olá `didRegisterForRemoteNotificationsWithDeviceToken` método da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="40616-153">Add hello `didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>
   
        func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
            EngagementAgent.shared().registerDeviceToken(deviceToken)
        }
3. <span data-ttu-id="40616-154">Adicionar Olá `didReceiveRemoteNotification:fetchCompletionHandler:` método da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="40616-154">Add hello `didReceiveRemoteNotification:fetchCompletionHandler:` method as follows:</span></span>
   
        func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
            EngagementAgent.shared().applicationDidReceiveRemoteNotification(userInfo, fetchCompletionHandler:completionHandler)
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[SDK do Mobile Engagement iOS]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-swift-get-started/add-header-file.png
[5]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
[6]: ./media/mobile-engagement-ios-swift-get-started/add-bridging-header.png
