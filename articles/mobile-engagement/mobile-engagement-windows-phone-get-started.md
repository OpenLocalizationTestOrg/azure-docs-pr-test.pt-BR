---
title: "Introdução ao Azure Mobile Engagement para aplicativos do Windows Phone Silverlight"
description: "Saiba como usar o Azure Mobile Engagement com análises e notificações por push para aplicativos do Windows Phone Silverlight."
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
ms.openlocfilehash: d2334a59d83c90bdd02c4fa29261d36aad292892
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-phone-silverlight-apps"></a><span data-ttu-id="88878-103">Introdução ao Azure Mobile Engagement para aplicativos do Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="88878-103">Get started with Azure Mobile Engagement for Windows Phone Silverlight apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="88878-104">Este tópico mostra como usar o Azure Mobile Engagement para entender o uso do aplicativo e enviar notificações por push para usuários segmentados de um aplicativo do Windows Phone Silverlight.</span><span class="sxs-lookup"><span data-stu-id="88878-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users of a Windows Phone Silverlight application.</span></span>
<span data-ttu-id="88878-105">Esse tutorial demonstra um cenário de transmissão simples usando o Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="88878-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="88878-106">Nele, você cria um aplicativo do Windows Phone Silverlight em branco que coleta dados básicos e recebe notificações por push usando o Serviço de Notificação por Push da Microsoft (MPNS).</span><span class="sxs-lookup"><span data-stu-id="88878-106">In it, you create a blank Windows Phone Silverlight app that collects basic data and receives push notifications using Microsoft Push Notification Service (MPNS).</span></span>

> [!NOTE]
> <span data-ttu-id="88878-107">O serviço Azure Mobile Engagement será desativado em março de 2018 e, no momento, está disponível somente para os clientes existentes.</span><span class="sxs-lookup"><span data-stu-id="88878-107">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="88878-108">Para saber mais, confira [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="88878-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

> [!NOTE]
> <span data-ttu-id="88878-109">Não há suporte para projetos do Windows Phone 8.1 e versões anteriores no Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="88878-109">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="88878-110">Para saber mais, confira [Direcionamento e compatibilidade da plataforma Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="88878-110">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="88878-111">Se você estiver almejando o Windows Phone 8.1 (não Silverlight), consulte o [tutorial do Windows Universal](mobile-engagement-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="88878-111">If you are targeting Windows Phone 8.1 (non-Silverlight), refer to the [Windows Universal tutorial](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>
> 
> 

<span data-ttu-id="88878-112">Este tutorial exige o seguinte:</span><span class="sxs-lookup"><span data-stu-id="88878-112">This tutorial requires the following:</span></span>

* <span data-ttu-id="88878-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="88878-113">Visual Studio 2013</span></span>
* <span data-ttu-id="88878-114">[MicrosoftAzure.MobileEngagement] </span><span class="sxs-lookup"><span data-stu-id="88878-114">[MicrosoftAzure.MobileEngagement] Nuget package</span></span>

> [!NOTE]
> <span data-ttu-id="88878-115">Para concluir este tutorial, você precisa ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="88878-115">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="88878-116">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="88878-116">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="88878-117">Para obter detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).</span><span class="sxs-lookup"><span data-stu-id="88878-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).</span></span>
> 
> 

## <span data-ttu-id="88878-118"><a id="setup-azme"></a>Configurar o Mobile Engagement para aplicativos do Windows Phone</span><span class="sxs-lookup"><span data-stu-id="88878-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Windows Phone app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="88878-119"><a id="connecting-app"></a>Conecte o seu aplicativo ao back-end do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="88878-119"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="88878-120">Este tutorial apresenta uma "integração básica" que é o conjunto mínimo exigido para coletar dados e enviar uma notificação por push.</span><span class="sxs-lookup"><span data-stu-id="88878-120">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="88878-121">A documentação de integração completa pode ser encontrada na [integração do SDK do Windows Phone para o Mobile Engagement](mobile-engagement-windows-phone-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="88878-121">The complete integration documentation can be found in the [Mobile Engagement Windows Phone SDK integration](mobile-engagement-windows-phone-sdk-overview.md)</span></span>

<span data-ttu-id="88878-122">Criaremos um aplicativo básico com o Visual Studio para demonstrar a integração.</span><span class="sxs-lookup"><span data-stu-id="88878-122">We will create a basic app with Visual Studio to demonstrate the integration.</span></span>

### <a name="create-a-new-windows-phone-silverlight-project"></a><span data-ttu-id="88878-123">Criação de um novo projeto do Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="88878-123">Create a new Windows Phone Silverlight project</span></span>
<span data-ttu-id="88878-124">As etapas a seguir pressupõem o uso do Visual Studio 2015, embora as etapas sejam semelhantes em versões anteriores do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="88878-124">The following steps assume the use of Visual Studio 2015 though the steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="88878-125">Inicie o Visual Studio e na tela **Início**, selecione **Novo Projeto**.</span><span class="sxs-lookup"><span data-stu-id="88878-125">Start Visual Studio, and in the **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="88878-126">No menu pop-up, selecione **Windows 8** -> **Windows Phone** -> **Aplicativo em Branco (Windows Phone Silverlight)**.</span><span class="sxs-lookup"><span data-stu-id="88878-126">In the pop-up, select **Windows 8** -> **Windows Phone** -> **Blank App (Windows Phone Silverlight)**.</span></span> <span data-ttu-id="88878-127">Preencha o **Nome** e o **Nome da solução** do aplicativo, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="88878-127">Fill in the app **Name** and **Solution name**, and then click **OK**.</span></span>
   
    ![][1]
3. <span data-ttu-id="88878-128">Você pode escolher como destino **Windows Phone 8.0** ou **Windows Phone 8.1**.</span><span class="sxs-lookup"><span data-stu-id="88878-128">You can choose to target either **Windows Phone 8.0** or **Windows Phone 8.1**.</span></span>

<span data-ttu-id="88878-129">Você agora criou um novo aplicativo do Windows Phone Silverlight no qual integraremos o SDK do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="88878-129">You have now created a new Windows Phone Silverlight app into which we will integrate the Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-to-the-mobile-engagement-backend"></a><span data-ttu-id="88878-130">Conecte o seu aplicativo ao back-end do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="88878-130">Connect your app to the Mobile Engagement backend</span></span>
1. <span data-ttu-id="88878-131">Instale o pacote do nuget [MicrosoftAzure.MobileEngagement] em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="88878-131">Install the [MicrosoftAzure.MobileEngagement] nuget package in your project.</span></span>
2. <span data-ttu-id="88878-132">Abra `WMAppManifest.xml` (na pasta Propriedades) e verifique se os itens a seguir estão declarados (adicione caso não estejam) na marca `<Capabilities />`:</span><span class="sxs-lookup"><span data-stu-id="88878-132">Open `WMAppManifest.xml` (under the Properties folder) and make sure the following are declared (add them if they are not) in the `<Capabilities />` tag:</span></span>
   
        <Capability Name="ID_CAP_NETWORKING" />
        <Capability Name="ID_CAP_IDENTITY_DEVICE" />
   
    ![][2]
3. <span data-ttu-id="88878-133">Agora cole a cadeia de conexão que você copiou anteriormente para o seu aplicativo do Mobile Engagement e cole no arquivo `Resources\EngagementConfiguration.xml` entre as marcas `<connectionString>` e `</connectionString>`:</span><span class="sxs-lookup"><span data-stu-id="88878-133">Now paste the connection string that you copied earlier for your Mobile Engagement app and paste it in the `Resources\EngagementConfiguration.xml` file, between the `<connectionString>` and `</connectionString>` tags:</span></span>
   
    ![][3]
4. <span data-ttu-id="88878-134">No arquivo `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="88878-134">In the `App.xaml.cs` file:</span></span>
   
    <span data-ttu-id="88878-135">a.</span><span class="sxs-lookup"><span data-stu-id="88878-135">a.</span></span> <span data-ttu-id="88878-136">Adicione a instrução `using`:</span><span class="sxs-lookup"><span data-stu-id="88878-136">Add the `using` statement:</span></span>
   
            using Microsoft.Azure.Engagement;
   
    <span data-ttu-id="88878-137">b.</span><span class="sxs-lookup"><span data-stu-id="88878-137">b.</span></span> <span data-ttu-id="88878-138">Inicializar o SDK no método `Application_Launching`:</span><span class="sxs-lookup"><span data-stu-id="88878-138">Initialize the SDK in the `Application_Launching` method:</span></span>
   
            private void Application_Launching(object sender, LaunchingEventArgs e)
            {
              EngagementAgent.Instance.Init();
            }
   
    <span data-ttu-id="88878-139">c.</span><span class="sxs-lookup"><span data-stu-id="88878-139">c.</span></span> <span data-ttu-id="88878-140">Insira o seguinte em `Application_Activated`:</span><span class="sxs-lookup"><span data-stu-id="88878-140">Insert the following in the `Application_Activated`:</span></span>
   
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
               EngagementAgent.Instance.OnActivated(e);
            }

## <span data-ttu-id="88878-141"><a id="monitor"></a>Habilitar monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="88878-141"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="88878-142">Para iniciar o envio de dados e assegurar que os usuários estejam ativos, você deve enviar pelo menos uma tela (Atividade) para o back-end do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="88878-142">In order to start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="88878-143">Em MainPage.xaml.cs, adicione a instrução `using`:</span><span class="sxs-lookup"><span data-stu-id="88878-143">In the MainPage.xaml.cs, add the `using` statement:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="88878-144">Substitua a classe base **MainPage**, que fica antes de **PhoneApplicationPage**, por **EngagementPage**.</span><span class="sxs-lookup"><span data-stu-id="88878-144">Replace the base class of **MainPage**, which is before **PhoneApplicationPage**, with **EngagementPage**.</span></span>
   
        class MainPage : EngagementPage 
3. <span data-ttu-id="88878-145">No arquivo `MainPage.xml`:</span><span class="sxs-lookup"><span data-stu-id="88878-145">In your `MainPage.xml` file:</span></span>
   
    <span data-ttu-id="88878-146">a.</span><span class="sxs-lookup"><span data-stu-id="88878-146">a.</span></span> <span data-ttu-id="88878-147">Adicione às suas declarações de namespaces:</span><span class="sxs-lookup"><span data-stu-id="88878-147">Add to your namespaces declarations:</span></span>
   
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
   
    <span data-ttu-id="88878-148">b.</span><span class="sxs-lookup"><span data-stu-id="88878-148">b.</span></span> <span data-ttu-id="88878-149">Substitua `phone:PhoneApplicationPage` no nome da marca XML por `engagement:EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="88878-149">Replace `phone:PhoneApplicationPage` in the XML tag name with `engagement:EngagementPage`.</span></span>

## <span data-ttu-id="88878-150"><a id="monitor"></a>Conectar o aplicativo com monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="88878-150"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="88878-151"><a id="integrate-push"></a>Habilitar notificações por push e mensagens no aplicativo</span><span class="sxs-lookup"><span data-stu-id="88878-151"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="88878-152">O Mobile Engagement permite interagir e entrar em contato com usuários com notificações por push e mensagens no aplicativo no contexto de campanhas.</span><span class="sxs-lookup"><span data-stu-id="88878-152">Mobile Engagement allows you to interact and reach your users with Push Notifications and in-app Messaging in the context of campaigns.</span></span> <span data-ttu-id="88878-153">Esse módulo é chamado de REACH no portal do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="88878-153">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="88878-154">As seções a seguir configuram seu aplicativo para recebê-las.</span><span class="sxs-lookup"><span data-stu-id="88878-154">The following sections set up your app to receive them.</span></span>

### <a name="enable-your-app-to-receive-mpns-push-notifications"></a><span data-ttu-id="88878-155">Habilitar o aplicativo para receber Notificações por Push do MPNS</span><span class="sxs-lookup"><span data-stu-id="88878-155">Enable your app to receive MPNS Push Notifications</span></span>
<span data-ttu-id="88878-156">Adicionar novos recursos ao arquivo `WMAppManifest.xml` :</span><span class="sxs-lookup"><span data-stu-id="88878-156">Add new Capabilities to your `WMAppManifest.xml` file:</span></span>

        ID_CAP_PUSH_NOTIFICATION
        ID_CAP_WEBBROWSERCOMPONENT

   ![][5]

### <a name="initialize-the-reach-sdk"></a><span data-ttu-id="88878-157">Inicializar o SDK do REACH</span><span class="sxs-lookup"><span data-stu-id="88878-157">Initialize the REACH SDK</span></span>
1. <span data-ttu-id="88878-158">Em `App.xaml.cs`, chame `EngagementReach.Instance.Init();` na função **Application_Launching**, logo após a inicialização do agente:</span><span class="sxs-lookup"><span data-stu-id="88878-158">In `App.xaml.cs`, call `EngagementReach.Instance.Init();` in the **Application_Launching** function, right after the agent initialization:</span></span>
   
        private void Application_Launching(object sender, LaunchingEventArgs e)
        {
           EngagementAgent.Instance.Init();
           EngagementReach.Instance.Init();
        }
2. <span data-ttu-id="88878-159">Em `App.xaml.cs`, chame `EngagementReach.Instance.OnActivated(e);` na função **Application_Activated** logo após a inicialização do agente:</span><span class="sxs-lookup"><span data-stu-id="88878-159">In `App.xaml.cs`, call `EngagementReach.Instance.OnActivated(e);` in the **Application_Activated** function, right after the agent initialization:</span></span>
   
        private void Application_Activated(object sender, ActivatedEventArgs e)
        {
           EngagementAgent.Instance.OnActivated(e);
           EngagementReach.Instance.OnActivated(e);
        }

<span data-ttu-id="88878-160">Você está pronto.</span><span class="sxs-lookup"><span data-stu-id="88878-160">You're all set.</span></span> <span data-ttu-id="88878-161">Agora vamos verificar se você criou corretamente essa integração básica.</span><span class="sxs-lookup"><span data-stu-id="88878-161">Now we will verify that you have correctly cried out this basic integration.</span></span>

## <span data-ttu-id="88878-162"><a id="send"></a>Envie uma notificação para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="88878-162"><a id="send"></a>Send a notification to your app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="88878-163">Você agora verá uma notificação em seu dispositivo que será exibida como uma notificação no aplicativo, se o aplicativo estiver aberto como uma notificação do sistema semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="88878-163">You should now see a notification on your device which will show up as an in-app notification if the app is open otherwise as a toast notification like the following:</span></span> 

![][6]

<!-- URLs. -->
<span data-ttu-id="88878-164">[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664</span><span class="sxs-lookup"><span data-stu-id="88878-164">[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664</span></span>
[Mobile Engagement Windows Phone SDK documentation]: ../mobile-engagement-windows-phone-integrate-engagement/

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-phone-get-started/project-properties.png
[2]: ./media/mobile-engagement-windows-phone-get-started/wmappmanifest-capabilities.png
[3]: ./media/mobile-engagement-windows-phone-get-started/add-connection-string.png
[5]: ./media/mobile-engagement-windows-phone-get-started/reach-capabilities.png
[6]: ./media/mobile-engagement-windows-phone-get-started/push-screenshot.png
