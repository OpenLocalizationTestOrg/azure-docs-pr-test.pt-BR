---
title: "Introdução ao Azure Mobile Engagement para Xamarin.Android"
description: "Saiba como usar o Azure Mobile Engagement com análises e notificações por push para aplicativos Xamarin.Android."
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: fb68cf98-08a2-41b5-8e59-757469de3fe7
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/16/2016
ms.author: piyushjo
ms.openlocfilehash: 7b3d01b32c2d5a40448fc22861cd45f612238f2f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinandroid-apps"></a><span data-ttu-id="6b991-103">Introdução ao Azure Mobile Engagement para aplicativos Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="6b991-103">Get Started with Azure Mobile Engagement for Xamarin.Android Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="6b991-104">Este tópico mostra como usar o Azure Mobile Engagement para entender o uso do aplicativo e como enviar notificações por push para usuários segmentados de um aplicativo Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="6b991-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of a Xamarin.Android application.</span></span>
<span data-ttu-id="6b991-105">Esse tutorial demonstra um cenário de transmissão simples usando o Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="6b991-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="6b991-106">Nele, você cria um aplicativo Xamarin.Android em branco que coleta dados básicos e recebe notificações por push usando o GCM (Google Cloud Messaging).</span><span class="sxs-lookup"><span data-stu-id="6b991-106">In it, you create a blank Xamarin.Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

> [!NOTE]
> <span data-ttu-id="6b991-107">O serviço Azure Mobile Engagement será desativado em março de 2018 e, no momento, está disponível somente para os clientes existentes.</span><span class="sxs-lookup"><span data-stu-id="6b991-107">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="6b991-108">Para saber mais, confira [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="6b991-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="6b991-109">Este tutorial exige o seguinte:</span><span class="sxs-lookup"><span data-stu-id="6b991-109">This tutorial requires the following:</span></span>

* <span data-ttu-id="6b991-110">[Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="6b991-110">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="6b991-111">Você também pode usar o Visual Studio com Xamarin, mas este tutorial usa o Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="6b991-111">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="6b991-112">Para obter instruções de instalação, confira [Instalar e configurar para Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="6b991-112">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* [<span data-ttu-id="6b991-113">SDK do Xamarin do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="6b991-113">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="6b991-114">Para concluir este tutorial, você precisa ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="6b991-114">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="6b991-115">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="6b991-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="6b991-116">Para obter detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="6b991-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="6b991-117"><a id="setup-azme"></a>Configuração do Mobile Engagement para seu aplicativo Android</span><span class="sxs-lookup"><span data-stu-id="6b991-117"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="6b991-118"><a id="connecting-app"></a>Conecte o seu aplicativo ao back-end do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="6b991-118"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="6b991-119">Este tutorial apresenta uma "integração básica" que é o conjunto mínimo exigido para coletar dados e enviar uma notificação por push.</span><span class="sxs-lookup"><span data-stu-id="6b991-119">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> 

<span data-ttu-id="6b991-120">Criaremos um aplicativo básico com o Xamarin Studio para demonstrar a integração.</span><span class="sxs-lookup"><span data-stu-id="6b991-120">We will create a basic app with Xamarin Studio to demonstrate the integration.</span></span>

### <a name="create-a-new-xamarinandroid-project"></a><span data-ttu-id="6b991-121">Criar um novo projeto Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="6b991-121">Create a new Xamarin.Android project</span></span>
1. <span data-ttu-id="6b991-122">Inicie o **Xamarin Studio** Vá para **Arquivo** -> **ovo** -> **Solução**</span><span class="sxs-lookup"><span data-stu-id="6b991-122">Launch **Xamarin Studio** Go to **File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="6b991-123">Selecione **Aplicativo Android** em seguida, verifique se a linguagem selecionada é **C#** e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="6b991-123">Select **Android App** then make sure the selected language is **C#** and click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="6b991-124">Preencha o **Nome do Aplicativo** e o **Identificador da Organização**.</span><span class="sxs-lookup"><span data-stu-id="6b991-124">Fill in the **App Name** and the **Organization Identifier**.</span></span> <span data-ttu-id="6b991-125">Marque **Serviços do Google Play**, em seguida, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="6b991-125">Make sure to checkmark **Google Play Services** and then click **Next**.</span></span> 
   
    ![][3]
4. <span data-ttu-id="6b991-126">Atualize o **Nome do Projeto**, o **Nome da Solução** e o **Localização**, se necessário, e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6b991-126">Update the **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="6b991-127">O Xamarin Studio criará o aplicativo, ao qual integraremos o Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="6b991-127">Xamarin Studio will create the app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="6b991-128">Conecte seu aplicativo ao back-end do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="6b991-128">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="6b991-129">Clique com o botão direito do mouse na pasta **Pacotes** na janela Solução e escolha **Adicionar Pacotes...**</span><span class="sxs-lookup"><span data-stu-id="6b991-129">Right click the **Packages** folder in the Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="6b991-130">Pesquise o **SDK do Xamarin do Microsoft Azure Mobile Engagement** e adicione-o à solução.</span><span class="sxs-lookup"><span data-stu-id="6b991-130">Search for the **Microsoft Azure Mobile Engagement Xamarin SDK** and add it to your solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="6b991-131">Abra **MainActivity.cs** e adicione as seguintes instruções using:</span><span class="sxs-lookup"><span data-stu-id="6b991-131">Open **MainActivity.cs** and add the following using statements:</span></span>
   
        using Microsoft.Azure.Engagement;
        using Microsoft.Azure.Engagement.Activity;
4. <span data-ttu-id="6b991-132">No método `OnCreate` , adicione o seguinte para inicializar a conexão com o back-end do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="6b991-132">In the `OnCreate` method, add the following to initialize the connection with Mobile Engagement backend.</span></span> <span data-ttu-id="6b991-133">Adicione a **ConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="6b991-133">Make sure to add your **ConnectionString**.</span></span> 
   
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.ConnectionString = "YourConnectionStringFromAzurePortal";
        EngagementAgent.Init(engagementConfiguration);

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="6b991-134">Adicionar permissões e uma declaração de serviço</span><span class="sxs-lookup"><span data-stu-id="6b991-134">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="6b991-135">Abra o arquivo **Manifest.xm** na pasta Propriedades.</span><span class="sxs-lookup"><span data-stu-id="6b991-135">Open up the **Manifest.xml** file under the Properties folder.</span></span> <span data-ttu-id="6b991-136">Selecione a guia Fonte para que você atualize diretamente o código-fonte XML.</span><span class="sxs-lookup"><span data-stu-id="6b991-136">Select Source tab so that you directly update the XML source.</span></span>
2. <span data-ttu-id="6b991-137">Adicione essas permissões ao Manifest.xml (que pode ser encontrado na pasta **Propriedades**) do seu projeto antes ou logo após da marcação `<application>`:</span><span class="sxs-lookup"><span data-stu-id="6b991-137">Add these permissions to the Manifest.xml (which can be found under the **Properties** folder) of your project immediately before or after the `<application>` tag:</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
3. <span data-ttu-id="6b991-138">Adicione o seguinte entre as marcas `<application>` e `</application>` para declarar o serviço do agente:</span><span class="sxs-lookup"><span data-stu-id="6b991-138">Add the following between the `<application>` and `</application>` tags to declare the agent service:</span></span>
   
        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
4. <span data-ttu-id="6b991-139">No código que você acabou de colar, substitua `"<Your application name>"` no rótulo.</span><span class="sxs-lookup"><span data-stu-id="6b991-139">In the code you just pasted, replace `"<Your application name>"` in the label.</span></span> <span data-ttu-id="6b991-140">Isso é exibido no menu **Configurações** , em que os usuários podem ver os serviços em execução no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6b991-140">This is displayed in the **Settings** menu where users can see services running on the device.</span></span> <span data-ttu-id="6b991-141">Você pode adicionar a palavra "Serviço" desse rótulo por exemplo.</span><span class="sxs-lookup"><span data-stu-id="6b991-141">You can add the word "Service" in that label for example.</span></span>

### <a name="send-a-screen-to-mobile-engagement"></a><span data-ttu-id="6b991-142">Enviar uma tela ao Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="6b991-142">Send a screen to Mobile Engagement</span></span>
<span data-ttu-id="6b991-143">Para iniciar o envio de dados e assegurar que os usuários estejam ativos, você deve enviar pelo menos uma tela ao back-end do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="6b991-143">In order to start sending data and ensuring the users are active, you must send at least one screen to the Mobile Engagement backend.</span></span> <span data-ttu-id="6b991-144">Para fazer isso, verifique se `MainActivity` herda de `EngagementActivity`, em vez de `Activity`.</span><span class="sxs-lookup"><span data-stu-id="6b991-144">For doing this - ensure that the `MainActivity` inherits from `EngagementActivity` instead of `Activity`.</span></span>

    public class MainActivity : EngagementActivity

<span data-ttu-id="6b991-145">Como alternativa, se você não puder herdar de `EngagementActivity`, então, deverá adicionar os métodos `.StartActivity` e `.EndActivity` em `OnResume` e `OnPause`, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="6b991-145">Alternatively, if you cannot inherit from `EngagementActivity` then you must add `.StartActivity` and `.EndActivity` methods in `OnResume` and `OnPause` respectively.</span></span>  

        protected override void OnResume()
            {
                EngagementAgent.StartActivity(EngagementAgentUtils.BuildEngagementActivityName(Java.Lang.Class.FromType(this.GetType())), null);
                base.OnResume();             
            }

            protected override void OnPause()
            {
                EngagementAgent.EndActivity();
                base.OnPause();            
            }

## <span data-ttu-id="6b991-146"><a id="monitor"></a>Conectar o aplicativo com monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="6b991-146"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="6b991-147"><a id="integrate-push"></a>Habilitar notificações por push e mensagens no aplicativo</span><span class="sxs-lookup"><span data-stu-id="6b991-147"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="6b991-148">O Mobile Engagement permite a você interagir e entrar em contato com seus usuários com notificações por push e mensagens no aplicativo no contexto de campanhas.</span><span class="sxs-lookup"><span data-stu-id="6b991-148">Mobile Engagement allows you to interact with and REACH your users with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="6b991-149">Esse módulo é chamado de REACH no portal do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="6b991-149">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="6b991-150">As seções a seguir configuram seu aplicativo para recebê-las.</span><span class="sxs-lookup"><span data-stu-id="6b991-150">The following sections sets up your app to receive them.</span></span>

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[1]: ./media/mobile-engagement-xamarin-android-get-started/1.png
[2]: ./media/mobile-engagement-xamarin-android-get-started/2.png
[3]: ./media/mobile-engagement-xamarin-android-get-started/3.png
[4]: ./media/mobile-engagement-xamarin-android-get-started/4.png
[5]: ./media/mobile-engagement-xamarin-android-get-started/5.png
[6]: ./media/mobile-engagement-xamarin-android-get-started/6.png
