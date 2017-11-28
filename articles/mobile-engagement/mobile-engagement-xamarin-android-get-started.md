---
title: aaaGet iniciado com o Azure Mobile Engagement para xamarin
description: "Saiba como toouse Azure Mobile Engagement com análises e notificações por Push para aplicativos xamarin."
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
ms.openlocfilehash: 9d584fea8e8153d511258cf9b6f87f31dac6aeca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinandroid-apps"></a><span data-ttu-id="9bc39-103">Introdução ao Azure Mobile Engagement para aplicativos Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="9bc39-103">Get Started with Azure Mobile Engagement for Xamarin.Android Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="9bc39-104">Este tópico mostra como toouse do Azure Mobile Engagement toounderstand o uso do aplicativo e como toosend envio usuários de toosegmented de notificações de um aplicativo xamarin.</span><span class="sxs-lookup"><span data-stu-id="9bc39-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Xamarin.Android application.</span></span>
<span data-ttu-id="9bc39-105">Este tutorial demonstra Olá cenário difusão simples usando o Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="9bc39-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="9bc39-106">Nele, você cria um aplicativo Xamarin.Android em branco que coleta dados básicos e recebe notificações por push usando o GCM (Google Cloud Messaging).</span><span class="sxs-lookup"><span data-stu-id="9bc39-106">In it, you create a blank Xamarin.Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

> [!NOTE]
> <span data-ttu-id="9bc39-107">serviço do Azure Mobile Engagement Olá será descontinuado de 2018 março e está apenas disponível tooexisting clientes.</span><span class="sxs-lookup"><span data-stu-id="9bc39-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="9bc39-108">Para saber mais, confira [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="9bc39-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="9bc39-109">Este tutorial requer o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="9bc39-109">This tutorial requires hello following:</span></span>

* <span data-ttu-id="9bc39-110">[Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="9bc39-110">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="9bc39-111">Você também pode usar o Visual Studio com Xamarin, mas este tutorial usa o Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="9bc39-111">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="9bc39-112">Para obter instruções de instalação, confira [Instalar e configurar para Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="9bc39-112">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* [<span data-ttu-id="9bc39-113">SDK do Xamarin do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="9bc39-113">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="9bc39-114">toocomplete neste tutorial, você deve ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="9bc39-114">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="9bc39-115">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="9bc39-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="9bc39-116">Para obter detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="9bc39-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="9bc39-117"><a id="setup-azme"></a>Configuração do Mobile Engagement para seu aplicativo Android</span><span class="sxs-lookup"><span data-stu-id="9bc39-117"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="9bc39-118"><a id="connecting-app"></a>Conectar seu back-end do aplicativo toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="9bc39-118"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="9bc39-119">Este tutorial apresenta uma "integração básica", que é Olá mínimo definido toocollect necessários dados e envia uma notificação por push.</span><span class="sxs-lookup"><span data-stu-id="9bc39-119">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> 

<span data-ttu-id="9bc39-120">Vamos criar um aplicativo básico com a integração de saudação toodemonstrate Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="9bc39-120">We will create a basic app with Xamarin Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-new-xamarinandroid-project"></a><span data-ttu-id="9bc39-121">Criar um novo projeto Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="9bc39-121">Create a new Xamarin.Android project</span></span>
1. <span data-ttu-id="9bc39-122">Iniciar **Xamarin Studio** ir muito**arquivo** -> **novo** -> **solução**</span><span class="sxs-lookup"><span data-stu-id="9bc39-122">Launch **Xamarin Studio** Go too**File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="9bc39-123">Selecione **aplicativo Android** , em seguida, certifique-se de idioma Olá selecionado é **c#** e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="9bc39-123">Select **Android App** then make sure hello selected language is **C#** and click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="9bc39-124">Preencha Olá **nome do aplicativo** e hello **identificador de organização**.</span><span class="sxs-lookup"><span data-stu-id="9bc39-124">Fill in hello **App Name** and hello **Organization Identifier**.</span></span> <span data-ttu-id="9bc39-125">Certifique-se de que toocheckmark **Google executar serviços** e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="9bc39-125">Make sure toocheckmark **Google Play Services** and then click **Next**.</span></span> 
   
    ![][3]
4. <span data-ttu-id="9bc39-126">Saudação de atualização **nome do projeto**, **nome da solução** e **local** se necessário e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="9bc39-126">Update hello **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="9bc39-127">Xamarin Studio criará o aplicativo hello no qual integraremos Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="9bc39-127">Xamarin Studio will create hello app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="9bc39-128">Conectar seu back-end do aplicativo tooMobile contrato</span><span class="sxs-lookup"><span data-stu-id="9bc39-128">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="9bc39-129">Clique com botão direito Olá **pacotes** pasta no windows de solução hello e selecione **adicionar pacotes de...**</span><span class="sxs-lookup"><span data-stu-id="9bc39-129">Right click hello **Packages** folder in hello Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="9bc39-130">Pesquise Olá **SDK do Microsoft Azure Mobile Engagement Xamarin** e adicioná-lo tooyour solução.</span><span class="sxs-lookup"><span data-stu-id="9bc39-130">Search for hello **Microsoft Azure Mobile Engagement Xamarin SDK** and add it tooyour solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="9bc39-131">Abra **MainActivity.cs** e adicione Olá seguinte usando instruções:</span><span class="sxs-lookup"><span data-stu-id="9bc39-131">Open **MainActivity.cs** and add hello following using statements:</span></span>
   
        using Microsoft.Azure.Engagement;
        using Microsoft.Azure.Engagement.Activity;
4. <span data-ttu-id="9bc39-132">Em Olá `OnCreate` método, adicione Olá após a conexão de saudação tooinitialize com back-end do compromisso de mobilidade.</span><span class="sxs-lookup"><span data-stu-id="9bc39-132">In hello `OnCreate` method, add hello following tooinitialize hello connection with Mobile Engagement backend.</span></span> <span data-ttu-id="9bc39-133">Certifique-se de que tooadd seu **ConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="9bc39-133">Make sure tooadd your **ConnectionString**.</span></span> 
   
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.ConnectionString = "YourConnectionStringFromAzurePortal";
        EngagementAgent.Init(engagementConfiguration);

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="9bc39-134">Adicionar permissões e uma declaração de serviço</span><span class="sxs-lookup"><span data-stu-id="9bc39-134">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="9bc39-135">Olá, abra **Manifest.xml** arquivo na pasta de propriedades de saudação.</span><span class="sxs-lookup"><span data-stu-id="9bc39-135">Open up hello **Manifest.xml** file under hello Properties folder.</span></span> <span data-ttu-id="9bc39-136">Selecione a guia fonte para que você atualizar o código-fonte Olá XML diretamente.</span><span class="sxs-lookup"><span data-stu-id="9bc39-136">Select Source tab so that you directly update hello XML source.</span></span>
2. <span data-ttu-id="9bc39-137">Adicionar toohello essas permissões manifest (que podem ser encontrado em Olá **propriedades** pasta) do projeto imediatamente antes ou após Olá `<application>` marca:</span><span class="sxs-lookup"><span data-stu-id="9bc39-137">Add these permissions toohello Manifest.xml (which can be found under hello **Properties** folder) of your project immediately before or after hello `<application>` tag:</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
3. <span data-ttu-id="9bc39-138">Adicione a seguinte Olá entre hello `<application>` e `</application>` marcas de serviço de agente toodeclare hello:</span><span class="sxs-lookup"><span data-stu-id="9bc39-138">Add hello following between hello `<application>` and `</application>` tags toodeclare hello agent service:</span></span>
   
        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
4. <span data-ttu-id="9bc39-139">No código de saudação que você acabou de colar, substitua `"<Your application name>"` no rótulo de saudação.</span><span class="sxs-lookup"><span data-stu-id="9bc39-139">In hello code you just pasted, replace `"<Your application name>"` in hello label.</span></span> <span data-ttu-id="9bc39-140">Isso é exibido no hello **configurações** onde os usuários podem ver os serviços em execução no dispositivo de saudação do menu.</span><span class="sxs-lookup"><span data-stu-id="9bc39-140">This is displayed in hello **Settings** menu where users can see services running on hello device.</span></span> <span data-ttu-id="9bc39-141">Por exemplo você pode adicionar palavra hello "Serviço" nesse rótulo.</span><span class="sxs-lookup"><span data-stu-id="9bc39-141">You can add hello word "Service" in that label for example.</span></span>

### <a name="send-a-screen-toomobile-engagement"></a><span data-ttu-id="9bc39-142">Enviar um tooMobile tela Contrato</span><span class="sxs-lookup"><span data-stu-id="9bc39-142">Send a screen tooMobile Engagement</span></span>
<span data-ttu-id="9bc39-143">Em ordem toostart enviar dados e garantir que os usuários de saudação estão ativos, você deve enviar pelo menos uma tela toohello Mobile Engagement backend.</span><span class="sxs-lookup"><span data-stu-id="9bc39-143">In order toostart sending data and ensuring hello users are active, you must send at least one screen toohello Mobile Engagement backend.</span></span> <span data-ttu-id="9bc39-144">Para fazer isso-certifique-se de que Olá `MainActivity` herda de `EngagementActivity` em vez de `Activity`.</span><span class="sxs-lookup"><span data-stu-id="9bc39-144">For doing this - ensure that hello `MainActivity` inherits from `EngagementActivity` instead of `Activity`.</span></span>

    public class MainActivity : EngagementActivity

<span data-ttu-id="9bc39-145">Como alternativa, se você não puder herdar de `EngagementActivity`, então, deverá adicionar os métodos `.StartActivity` e `.EndActivity` em `OnResume` e `OnPause`, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="9bc39-145">Alternatively, if you cannot inherit from `EngagementActivity` then you must add `.StartActivity` and `.EndActivity` methods in `OnResume` and `OnPause` respectively.</span></span>  

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

## <span data-ttu-id="9bc39-146"><a id="monitor"></a>Conectar o aplicativo com monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="9bc39-146"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="9bc39-147"><a id="integrate-push"></a>Habilitar notificações por push e mensagens no aplicativo</span><span class="sxs-lookup"><span data-stu-id="9bc39-147"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="9bc39-148">Mobile Engagement permite toointeract com e alcançar os usuários com as notificações por push e no aplicativo mensagens no contexto de saudação de campanhas.</span><span class="sxs-lookup"><span data-stu-id="9bc39-148">Mobile Engagement allows you toointeract with and REACH your users with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="9bc39-149">Esse módulo é chamado alcance no portal do Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="9bc39-149">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="9bc39-150">Olá seções a seguir define o seu aplicativo tooreceive-los.</span><span class="sxs-lookup"><span data-stu-id="9bc39-150">hello following sections sets up your app tooreceive them.</span></span>

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
