---
title: aaaGet iniciado com o Azure Mobile Engagement para xamarin
description: "Saiba como toouse Azure Mobile Engagement com análises e notificações por Push para aplicativos xamarin."
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0448209e-fff6-47bd-985c-2cf074bac12f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 02340a744753dcc5cd1b6888a5fa87628be47b68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinios-apps"></a><span data-ttu-id="870b8-103">Introdução ao Azure Mobile Engagement para aplicativos Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="870b8-103">Get Started with Azure Mobile Engagement for Xamarin.iOS Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="870b8-104">Este tópico mostra como toouse do Azure Mobile Engagement toounderstand seu uso do aplicativo e enviar por push os usuários toosegmented de notificações em um aplicativo xamarin.</span><span class="sxs-lookup"><span data-stu-id="870b8-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users in a Xamarin.iOS application.</span></span>
<span data-ttu-id="870b8-105">Neste tutorial, você cria um aplicativo Xamarin.iOS em branco que coleta dados básicos e recebe notificações por push usando o Sistema de Notificação por Push da Apple (APNS).</span><span class="sxs-lookup"><span data-stu-id="870b8-105">In this tutorial, you create a blank Xamarin.iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

> [!NOTE]
> <span data-ttu-id="870b8-106">serviço do Azure Mobile Engagement Olá será descontinuado de 2018 março e está apenas disponível tooexisting clientes.</span><span class="sxs-lookup"><span data-stu-id="870b8-106">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="870b8-107">Para saber mais, confira [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="870b8-107">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="870b8-108">Este tutorial requer o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="870b8-108">This tutorial requires hello following:</span></span>

* <span data-ttu-id="870b8-109">[Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="870b8-109">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="870b8-110">Você também pode usar o Visual Studio com Xamarin, mas este tutorial usa o Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="870b8-110">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="870b8-111">Para obter instruções de instalação, confira [Instalar e configurar para Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="870b8-111">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span> 
* [<span data-ttu-id="870b8-112">SDK do Xamarin do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="870b8-112">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="870b8-113">toocomplete neste tutorial, você deve ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="870b8-113">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="870b8-114">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="870b8-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="870b8-115">Para obter detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="870b8-115">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).</span></span>
> 
> 

## <span data-ttu-id="870b8-116"><a id="setup-azme"></a>Configurar o Mobile Engagement para seu aplicativo iOS</span><span class="sxs-lookup"><span data-stu-id="870b8-116"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="870b8-117"><a id="connecting-app"></a>Conectar seu back-end do aplicativo toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="870b8-117"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="870b8-118">Este tutorial apresenta uma "integração básica" hello mínimo definido toocollect necessários dados e envia uma notificação por push.</span><span class="sxs-lookup"><span data-stu-id="870b8-118">This tutorial presents a "basic integration" which is hello minimal set required toocollect data and send a push notification.</span></span>

<span data-ttu-id="870b8-119">Vamos criar um aplicativo básico com a integração de saudação do Xamarin toodemonstrate:</span><span class="sxs-lookup"><span data-stu-id="870b8-119">We will create a basic app with Xamarin toodemonstrate hello integration:</span></span>

### <a name="create-a-new-xamarinios-project"></a><span data-ttu-id="870b8-120">Criar um novo projeto do Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="870b8-120">Create a new Xamarin.iOS project</span></span>
1. <span data-ttu-id="870b8-121">Inicie o Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="870b8-121">Launch Xamarin Studio.</span></span> <span data-ttu-id="870b8-122">Vá muito**arquivo** -> **novo** -> **solução**</span><span class="sxs-lookup"><span data-stu-id="870b8-122">Go too**File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="870b8-123">Selecione **único aplicativo de exibição**, certifique-se de idioma Olá selecionado é **c#** e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="870b8-123">Select **Single View App**, make sure hello selected language is **C#** and then click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="870b8-124">Preencha Olá **nome do aplicativo** e hello **identificador de organização** e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="870b8-124">Fill in hello **App Name** and hello **Organization Identifier** and then click **Next**.</span></span> 
   
    ![][3]
   
   > [!IMPORTANT]
   > <span data-ttu-id="870b8-125">Certifique-se de que Olá você eventualmente usar toodeploy que seu aplicativo iOS está usando uma ID de aplicativo que corresponda exatamente com hello aqui de identificador de pacote de perfil de publicação.</span><span class="sxs-lookup"><span data-stu-id="870b8-125">Make sure that hello publishing profile you eventually use toodeploy your iOS app is using an App ID which matches exactly with hello Bundle Identifier you have here.</span></span> 
   > 
   > 
4. <span data-ttu-id="870b8-126">Saudação de atualização **nome do projeto**, **nome da solução** e **local** se necessário e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="870b8-126">Update hello **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="870b8-127">Xamarin Studio criará o aplicativo de demonstração de Olá no qual integraremos Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="870b8-127">Xamarin Studio will create hello demo app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="870b8-128">Conectar seu back-end do aplicativo tooMobile contrato</span><span class="sxs-lookup"><span data-stu-id="870b8-128">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="870b8-129">Clique com botão direito Olá **pacotes** pasta no windows de solução hello e selecione **adicionar pacotes de...**</span><span class="sxs-lookup"><span data-stu-id="870b8-129">Right click hello **Packages** folder in hello Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="870b8-130">Pesquise Olá **SDK do Microsoft Azure Mobile Engagement Xamarin** e adicioná-lo tooyour solução.</span><span class="sxs-lookup"><span data-stu-id="870b8-130">Search for hello **Microsoft Azure Mobile Engagement Xamarin SDK** and add it tooyour solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="870b8-131">Abra **appdelegate. CS** e adicione o seguinte hello usando a instrução:</span><span class="sxs-lookup"><span data-stu-id="870b8-131">Open **AppDelegate.cs** and add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Xamarin;
4. <span data-ttu-id="870b8-132">Em Olá **FinishedLaunching** método, adicione Olá após a conexão de saudação tooinitialize com back-end do compromisso de mobilidade.</span><span class="sxs-lookup"><span data-stu-id="870b8-132">In hello **FinishedLaunching** method, add hello following tooinitialize hello connection with Mobile Engagement backend.</span></span> <span data-ttu-id="870b8-133">Certifique-se de que tooadd seu **ConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="870b8-133">Make sure tooadd your **ConnectionString**.</span></span> <span data-ttu-id="870b8-134">Esse código também usa uma cópia **NotificationIcon** que é adicionada por Olá SDK do Mobile Engagement que talvez você queira tooreplace.</span><span class="sxs-lookup"><span data-stu-id="870b8-134">This code also uses a dummy **NotificationIcon** which is added by hello Mobile Engagement SDK which you may want tooreplace.</span></span> 
   
        EngagementConfiguration config = new EngagementConfiguration {
                        ConnectionString = "YourConnectionStringFromAzurePortal",
                        NotificationIcon = UIImage.FromBundle("close")
                    };
        EngagementAgent.Init (config);

## <span data-ttu-id="870b8-135"><a id="monitor"></a>Habilitar monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="870b8-135"><a id="monitor"></a>Enabling real-time monitoring</span></span>
<span data-ttu-id="870b8-136">Em ordem toostart enviar dados e garantir que os usuários de saudação estão ativos, você deve enviar pelo menos uma tela toohello Mobile Engagement backend.</span><span class="sxs-lookup"><span data-stu-id="870b8-136">In order toostart sending data and ensuring hello users are active, you must send at least one screen toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="870b8-137">Abra **ViewController.cs** e adicione o seguinte hello usando a instrução:</span><span class="sxs-lookup"><span data-stu-id="870b8-137">Open **ViewController.cs** and add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Xamarin;
2. <span data-ttu-id="870b8-138">Substitua a classe de saudação do qual `ViewController` herda de `UIViewController` muito`EngagementViewController`.</span><span class="sxs-lookup"><span data-stu-id="870b8-138">Replace hello class from which `ViewController` inherits from `UIViewController` too`EngagementViewController`.</span></span> 

## <span data-ttu-id="870b8-139"><a id="monitor"></a>Conectar o aplicativo com monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="870b8-139"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="870b8-140"><a id="integrate-push"></a>Habilitar notificações por push e mensagens no aplicativo</span><span class="sxs-lookup"><span data-stu-id="870b8-140"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="870b8-141">Mobile Engagement permite toointeract com os usuários e o alcance com notificações por push e no aplicativo mensagens no contexto de saudação de campanhas.</span><span class="sxs-lookup"><span data-stu-id="870b8-141">Mobile Engagement allows you toointeract with your users and REACH with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="870b8-142">Esse módulo é chamado alcance no portal do Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="870b8-142">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="870b8-143">Olá seções a seguir configurar seu aplicativo tooreceive-los.</span><span class="sxs-lookup"><span data-stu-id="870b8-143">hello following sections set up your app tooreceive them.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="870b8-144">Modifique seu Representante do Aplicativo</span><span class="sxs-lookup"><span data-stu-id="870b8-144">Modify your Application Delegate</span></span>
1. <span data-ttu-id="870b8-145">Olá abrir **appdelegate. CS** e adicione o seguinte hello usando a instrução:</span><span class="sxs-lookup"><span data-stu-id="870b8-145">Open hello **AppDelegate.cs** and add hello following using statement:</span></span>
   
        using System; 
2. <span data-ttu-id="870b8-146">Agora dentro Olá `FinishedLaunching` método, adicione Olá tooregister para mensagens de envio após a seguir`EngagementAgent.init(...)`</span><span class="sxs-lookup"><span data-stu-id="870b8-146">Now inside hello `FinishedLaunching` method, add hello following tooregister for push messages after `EngagementAgent.init(...)`</span></span>
   
        if (UIDevice.CurrentDevice.CheckSystemVersion(8,0))
        {
            var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                (UIUserNotificationType.Badge |
                    UIUserNotificationType.Sound |
                    UIUserNotificationType.Alert),
                null);
            UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications ();
        }
        else
        {
            UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (
                UIRemoteNotificationType.Badge |
                UIRemoteNotificationType.Sound |
                UIRemoteNotificationType.Alert);
        }
3. <span data-ttu-id="870b8-147">Por fim - atualizar ou adicionar Olá métodos a seguir:</span><span class="sxs-lookup"><span data-stu-id="870b8-147">Finally - update or add hello following methods:</span></span>
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, 
            Action<UIBackgroundFetchResult> completionHandler)
        {
            EngagementAgent.ApplicationDidReceiveRemoteNotification(userInfo, completionHandler);
        }
   
        public override void RegisteredForRemoteNotifications (UIApplication application, NSData deviceToken)
        {
            // Register device token on Engagement
            EngagementAgent.RegisterDeviceToken(deviceToken);
        }
   
        public override void FailedToRegisterForRemoteNotifications(UIApplication application, NSError error)
        {
            Console.WriteLine("Failed tooregister for remote notifications: Error '{0}'", error);
        }
4. <span data-ttu-id="870b8-148">No seu **Info. plist** na solução de saudação do arquivo, confirme que Olá **identificador de pacote** corresponde à saudação **ID do aplicativo** você tem em seu perfil de provisionamento Olá desenvolvimento da Apple Centro.</span><span class="sxs-lookup"><span data-stu-id="870b8-148">In your **Info.plist** file in hello solution, confirm that hello **Bundle Identifier** matches with hello **App ID** you have in your provisioning profile in hello Apple Dev Center.</span></span> 
   
    ![][7]
5. <span data-ttu-id="870b8-149">Em Olá mesmo **Info. plist** de arquivos, certifique-se de que você verificou Olá **habilitar modos de segundo plano** e **notificações remoto**.</span><span class="sxs-lookup"><span data-stu-id="870b8-149">In hello same **Info.plist** file, make sure that you have checked hello **Enable Background Modes** and **Remote Notifications**.</span></span> 
   
     ![][8]
6. <span data-ttu-id="870b8-150">Execute o aplicativo de saudação no dispositivo Olá associada a este perfil de publicação.</span><span class="sxs-lookup"><span data-stu-id="870b8-150">Run hello app on hello device you have associated with this publishing profile.</span></span> 

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[1]: ./media/mobile-engagement-xamarin-ios-get-started/new-solution.png
[2]: ./media/mobile-engagement-xamarin-ios-get-started/app-type.png
[3]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-name.png
[4]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-confirm.png
[5]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget.png
[6]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget-azme.png
[7]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-confirm-bundle.png
[8]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-configure-push.png
