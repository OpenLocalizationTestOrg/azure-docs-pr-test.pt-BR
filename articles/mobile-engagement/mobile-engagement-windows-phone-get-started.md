---
title: "aaaGet Introdução aos aplicativos do Azure Mobile Engagement para Windows Phone Silverlight"
description: "Saiba como toouse do Azure Mobile Engagement com notificações de análise e enviar por push para aplicativos do Windows Phone Silverlight."
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: aa34692f-87f7-47c6-a20c-a1972750bc25
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b39a838ab03217b2dc845cbf59d7bf8b094dac1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-phone-silverlight-apps"></a><span data-ttu-id="cd214-103">Introdução ao Azure Mobile Engagement para aplicativos do Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="cd214-103">Get started with Azure Mobile Engagement for Windows Phone Silverlight apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="cd214-104">Este tópico mostra como toouse do Azure Mobile Engagement toounderstand seu uso do aplicativo e enviar por push usuários de toosegmented de notificações de um aplicativo do Windows Phone Silverlight.</span><span class="sxs-lookup"><span data-stu-id="cd214-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users of a Windows Phone Silverlight application.</span></span>
<span data-ttu-id="cd214-105">Este tutorial demonstra Olá cenário difusão simples usando o Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="cd214-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="cd214-106">Nele, você cria um aplicativo do Windows Phone Silverlight em branco que coleta dados básicos e recebe notificações por push usando o Serviço de Notificação por Push da Microsoft (MPNS).</span><span class="sxs-lookup"><span data-stu-id="cd214-106">In it, you create a blank Windows Phone Silverlight app that collects basic data and receives push notifications using Microsoft Push Notification Service (MPNS).</span></span>

> [!NOTE]
> <span data-ttu-id="cd214-107">serviço do Azure Mobile Engagement Olá será descontinuado de 2018 março e está apenas disponível tooexisting clientes.</span><span class="sxs-lookup"><span data-stu-id="cd214-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="cd214-108">Para saber mais, confira [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="cd214-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

> [!NOTE]
> <span data-ttu-id="cd214-109">Não há suporte para projetos do Windows Phone 8.1 e versões anteriores no Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="cd214-109">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="cd214-110">Para saber mais, confira [Direcionamento e compatibilidade da plataforma Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="cd214-110">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="cd214-111">Se você estiver direcionando o Windows Phone 8.1 (não Silverlight), consulte toohello [tutorial Windows Universal](mobile-engagement-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cd214-111">If you are targeting Windows Phone 8.1 (non-Silverlight), refer toohello [Windows Universal tutorial](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>
> 
> 

<span data-ttu-id="cd214-112">Este tutorial requer o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="cd214-112">This tutorial requires hello following:</span></span>

* <span data-ttu-id="cd214-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="cd214-113">Visual Studio 2013</span></span>
* <span data-ttu-id="cd214-114">[MicrosoftAzure.MobileEngagement] </span><span class="sxs-lookup"><span data-stu-id="cd214-114">[MicrosoftAzure.MobileEngagement] Nuget package</span></span>

> [!NOTE]
> <span data-ttu-id="cd214-115">toocomplete neste tutorial, você deve ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="cd214-115">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="cd214-116">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="cd214-116">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="cd214-117">Para obter detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).</span><span class="sxs-lookup"><span data-stu-id="cd214-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).</span></span>
> 
> 

## <span data-ttu-id="cd214-118"><a id="setup-azme"></a>Configurar o Mobile Engagement para aplicativos do Windows Phone</span><span class="sxs-lookup"><span data-stu-id="cd214-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Windows Phone app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="cd214-119"><a id="connecting-app"></a>Conectar seu back-end do aplicativo toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="cd214-119"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="cd214-120">Este tutorial apresenta uma "integração básica", que é Olá mínimo definido toocollect necessários dados e envia uma notificação por push.</span><span class="sxs-lookup"><span data-stu-id="cd214-120">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="cd214-121">documentação de integração completa Olá pode ser encontrada no hello [integração do SDK do Mobile Engagement Windows Phone](mobile-engagement-windows-phone-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="cd214-121">hello complete integration documentation can be found in hello [Mobile Engagement Windows Phone SDK integration](mobile-engagement-windows-phone-sdk-overview.md)</span></span>

<span data-ttu-id="cd214-122">Vamos criar um aplicativo básico com a integração do Visual Studio toodemonstrate hello.</span><span class="sxs-lookup"><span data-stu-id="cd214-122">We will create a basic app with Visual Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-new-windows-phone-silverlight-project"></a><span data-ttu-id="cd214-123">Criação de um novo projeto do Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="cd214-123">Create a new Windows Phone Silverlight project</span></span>
<span data-ttu-id="cd214-124">Olá etapas a seguir pressupõem uso de saudação do Visual Studio 2015 que etapas Olá são semelhantes em versões anteriores do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cd214-124">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="cd214-125">Inicie o Visual Studio e em Olá **início** tela, selecione **novo projeto**.</span><span class="sxs-lookup"><span data-stu-id="cd214-125">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="cd214-126">No pop-up hello, selecione **Windows 8** -> **do Windows Phone** -> **aplicativo em branco (Windows Phone Silverlight)**.</span><span class="sxs-lookup"><span data-stu-id="cd214-126">In hello pop-up, select **Windows 8** -> **Windows Phone** -> **Blank App (Windows Phone Silverlight)**.</span></span> <span data-ttu-id="cd214-127">Preencha o aplicativo hello **nome** e **nome da solução**e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="cd214-127">Fill in hello app **Name** and **Solution name**, and then click **OK**.</span></span>
   
    ![][1]
3. <span data-ttu-id="cd214-128">Você pode escolher tootarget ou **Windows Phone 8.0** ou **Windows Phone 8.1**.</span><span class="sxs-lookup"><span data-stu-id="cd214-128">You can choose tootarget either **Windows Phone 8.0** or **Windows Phone 8.1**.</span></span>

<span data-ttu-id="cd214-129">Você criou um novo aplicativo do Windows Phone Silverlight para o qual integraremos Olá SDK do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="cd214-129">You have now created a new Windows Phone Silverlight app into which we will integrate hello Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a><span data-ttu-id="cd214-130">Conectar seu back-end do aplicativo toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="cd214-130">Connect your app toohello Mobile Engagement backend</span></span>
1. <span data-ttu-id="cd214-131">Instalar Olá [MicrosoftAzure.MobileEngagement] pacote nuget em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="cd214-131">Install hello [MicrosoftAzure.MobileEngagement] nuget package in your project.</span></span>
2. <span data-ttu-id="cd214-132">Abra `WMAppManifest.xml` (na pasta de propriedades de saudação) e certifique-se de seguir Olá é declarados (adicionado se eles não são) em Olá `<Capabilities />` marca:</span><span class="sxs-lookup"><span data-stu-id="cd214-132">Open `WMAppManifest.xml` (under hello Properties folder) and make sure hello following are declared (add them if they are not) in hello `<Capabilities />` tag:</span></span>
   
        <Capability Name="ID_CAP_NETWORKING" />
        <Capability Name="ID_CAP_IDENTITY_DEVICE" />
   
    ![][2]
3. <span data-ttu-id="cd214-133">Cole a cadeia de caracteres de conexão de saudação que você copiou anteriormente para seu aplicativo do Mobile Engagement agora e colá-lo em Olá `Resources\EngagementConfiguration.xml` arquivo entre hello `<connectionString>` e `</connectionString>` marcas:</span><span class="sxs-lookup"><span data-stu-id="cd214-133">Now paste hello connection string that you copied earlier for your Mobile Engagement app and paste it in hello `Resources\EngagementConfiguration.xml` file, between hello `<connectionString>` and `</connectionString>` tags:</span></span>
   
    ![][3]
4. <span data-ttu-id="cd214-134">Em Olá `App.xaml.cs` arquivo:</span><span class="sxs-lookup"><span data-stu-id="cd214-134">In hello `App.xaml.cs` file:</span></span>
   
    <span data-ttu-id="cd214-135">a.</span><span class="sxs-lookup"><span data-stu-id="cd214-135">a.</span></span> <span data-ttu-id="cd214-136">Adicionar Olá `using` instrução:</span><span class="sxs-lookup"><span data-stu-id="cd214-136">Add hello `using` statement:</span></span>
   
            using Microsoft.Azure.Engagement;
   
    <span data-ttu-id="cd214-137">b.</span><span class="sxs-lookup"><span data-stu-id="cd214-137">b.</span></span> <span data-ttu-id="cd214-138">Inicializar Olá SDK no hello `Application_Launching` método:</span><span class="sxs-lookup"><span data-stu-id="cd214-138">Initialize hello SDK in hello `Application_Launching` method:</span></span>
   
            private void Application_Launching(object sender, LaunchingEventArgs e)
            {
              EngagementAgent.Instance.Init();
            }
   
    <span data-ttu-id="cd214-139">c.</span><span class="sxs-lookup"><span data-stu-id="cd214-139">c.</span></span> <span data-ttu-id="cd214-140">Inserir o seguinte Olá em hello `Application_Activated`:</span><span class="sxs-lookup"><span data-stu-id="cd214-140">Insert hello following in hello `Application_Activated`:</span></span>
   
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
               EngagementAgent.Instance.OnActivated(e);
            }

## <span data-ttu-id="cd214-141"><a id="monitor"></a>Habilitar monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="cd214-141"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="cd214-142">Em ordem toostart enviar dados e garantir que os usuários de saudação estão ativos, você deve enviar pelo menos uma tela (atividade) toohello Mobile Engagement backend.</span><span class="sxs-lookup"><span data-stu-id="cd214-142">In order toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="cd214-143">Olá MainPage.xaml.cs, adiciona Olá `using` instrução:</span><span class="sxs-lookup"><span data-stu-id="cd214-143">In hello MainPage.xaml.cs, add hello `using` statement:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="cd214-144">Substitua a classe base Olá de **MainPage**, que é antes do **PhoneApplicationPage**, com **EngagementPage**.</span><span class="sxs-lookup"><span data-stu-id="cd214-144">Replace hello base class of **MainPage**, which is before **PhoneApplicationPage**, with **EngagementPage**.</span></span>
   
        class MainPage : EngagementPage 
3. <span data-ttu-id="cd214-145">No arquivo `MainPage.xml`:</span><span class="sxs-lookup"><span data-stu-id="cd214-145">In your `MainPage.xml` file:</span></span>
   
    <span data-ttu-id="cd214-146">a.</span><span class="sxs-lookup"><span data-stu-id="cd214-146">a.</span></span> <span data-ttu-id="cd214-147">Adicione declarações de namespaces tooyour:</span><span class="sxs-lookup"><span data-stu-id="cd214-147">Add tooyour namespaces declarations:</span></span>
   
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
   
    <span data-ttu-id="cd214-148">b.</span><span class="sxs-lookup"><span data-stu-id="cd214-148">b.</span></span> <span data-ttu-id="cd214-149">Substituir `phone:PhoneApplicationPage` no nome da marca XML Olá com `engagement:EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="cd214-149">Replace `phone:PhoneApplicationPage` in hello XML tag name with `engagement:EngagementPage`.</span></span>

## <span data-ttu-id="cd214-150"><a id="monitor"></a>Conectar o aplicativo com monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="cd214-150"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="cd214-151"><a id="integrate-push"></a>Habilitar notificações por push e mensagens no aplicativo</span><span class="sxs-lookup"><span data-stu-id="cd214-151"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="cd214-152">Mobile Engagement permite toointeract e alcançar seus usuários com notificações por Push e no aplicativo de mensagens do contexto de saudação de campanhas.</span><span class="sxs-lookup"><span data-stu-id="cd214-152">Mobile Engagement allows you toointeract and reach your users with Push Notifications and in-app Messaging in hello context of campaigns.</span></span> <span data-ttu-id="cd214-153">Esse módulo é chamado alcance no portal do Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="cd214-153">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="cd214-154">Olá seções a seguir configurar seu aplicativo tooreceive-los.</span><span class="sxs-lookup"><span data-stu-id="cd214-154">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-mpns-push-notifications"></a><span data-ttu-id="cd214-155">Habilitar seu aplicativo tooreceive notificações por Push do MPNS</span><span class="sxs-lookup"><span data-stu-id="cd214-155">Enable your app tooreceive MPNS Push Notifications</span></span>
<span data-ttu-id="cd214-156">Adicionar novo tooyour de recursos `WMAppManifest.xml` arquivo:</span><span class="sxs-lookup"><span data-stu-id="cd214-156">Add new Capabilities tooyour `WMAppManifest.xml` file:</span></span>

        ID_CAP_PUSH_NOTIFICATION
        ID_CAP_WEBBROWSERCOMPONENT

   ![][5]

### <a name="initialize-hello-reach-sdk"></a><span data-ttu-id="cd214-157">Inicializar Olá SDK do REACH</span><span class="sxs-lookup"><span data-stu-id="cd214-157">Initialize hello REACH SDK</span></span>
1. <span data-ttu-id="cd214-158">Em `App.xaml.cs`, chame `EngagementReach.Instance.Init();` em Olá **Application_Launching** função logo após a inicialização do agente de saudação:</span><span class="sxs-lookup"><span data-stu-id="cd214-158">In `App.xaml.cs`, call `EngagementReach.Instance.Init();` in hello **Application_Launching** function, right after hello agent initialization:</span></span>
   
        private void Application_Launching(object sender, LaunchingEventArgs e)
        {
           EngagementAgent.Instance.Init();
           EngagementReach.Instance.Init();
        }
2. <span data-ttu-id="cd214-159">Em `App.xaml.cs`, chame `EngagementReach.Instance.OnActivated(e);` em Olá **Application_Activated** função logo após a inicialização do agente de saudação:</span><span class="sxs-lookup"><span data-stu-id="cd214-159">In `App.xaml.cs`, call `EngagementReach.Instance.OnActivated(e);` in hello **Application_Activated** function, right after hello agent initialization:</span></span>
   
        private void Application_Activated(object sender, ActivatedEventArgs e)
        {
           EngagementAgent.Instance.OnActivated(e);
           EngagementReach.Instance.OnActivated(e);
        }

<span data-ttu-id="cd214-160">Você está pronto.</span><span class="sxs-lookup"><span data-stu-id="cd214-160">You're all set.</span></span> <span data-ttu-id="cd214-161">Agora vamos verificar se você criou corretamente essa integração básica.</span><span class="sxs-lookup"><span data-stu-id="cd214-161">Now we will verify that you have correctly cried out this basic integration.</span></span>

## <span data-ttu-id="cd214-162"><a id="send"></a>Enviar um aplicativo de tooyour de notificação</span><span class="sxs-lookup"><span data-stu-id="cd214-162"><a id="send"></a>Send a notification tooyour app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="cd214-163">Agora você verá uma notificação no seu dispositivo que serão exibidos como uma notificação no aplicativo se o aplicativo hello está aberto como uma notificação do sistema como Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="cd214-163">You should now see a notification on your device which will show up as an in-app notification if hello app is open otherwise as a toast notification like hello following:</span></span> 

![][6]

<!-- URLs. -->
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664
[Mobile Engagement Windows Phone SDK documentation]: ../mobile-engagement-windows-phone-integrate-engagement/

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-phone-get-started/project-properties.png
[2]: ./media/mobile-engagement-windows-phone-get-started/wmappmanifest-capabilities.png
[3]: ./media/mobile-engagement-windows-phone-get-started/add-connection-string.png
[5]: ./media/mobile-engagement-windows-phone-get-started/reach-capabilities.png
[6]: ./media/mobile-engagement-windows-phone-get-started/push-screenshot.png
