---
title: "Introdução ao Azure Mobile Engagement para Cordova/Phonegap"
description: "Aprenda a usar o Azure Mobile Engagement com Análises e Notificações por Push para Aplicativos Cordova/Phonegap."
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 54fe9113-e239-4ed7-9fd1-a502d7ac7f47
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-phonegap
ms.devlang: js
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d7a761310782faab1dda023785f93cf90742e2ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-cordovaphonegap"></a><span data-ttu-id="c8f49-103">Introdução ao Azure Mobile Engagement para Cordova/Phonegap</span><span class="sxs-lookup"><span data-stu-id="c8f49-103">Get Started with Azure Mobile Engagement for Cordova/Phonegap</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="c8f49-104">Este tópico mostra como usar o Azure Mobile Engagement para entender o uso do aplicativo e enviar notificações por push para usuários segmentados para um aplicativo móvel desenvolvido com Cordova.</span><span class="sxs-lookup"><span data-stu-id="c8f49-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users for a mobile application developed with Cordova.</span></span>

<span data-ttu-id="c8f49-105">Neste tutorial, criamos um aplicativo do Cordova em branco usando o Mac e integramos o SDK do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="c8f49-105">In this tutorial, we will create a blank Cordova app using Mac and then integrate Mobile Engagement SDK.</span></span> <span data-ttu-id="c8f49-106">Ele coleta dados de análise básica e recebe notificações por push usando o sistema de notificações de Push da Apple (APNS) para iOS e Google Cloud Messaging (GCM) para o Android.</span><span class="sxs-lookup"><span data-stu-id="c8f49-106">It collects basic analytics data and receives push notifications using Apple Push Notification System (APNS) for iOS and Google Cloud Messaging (GCM) for Android.</span></span> <span data-ttu-id="c8f49-107">Nós implantaremos em um dispositivo iOS ou Android para teste.</span><span class="sxs-lookup"><span data-stu-id="c8f49-107">We will deploy this to an iOS or Android device for testing.</span></span> 

> [!NOTE]
> <span data-ttu-id="c8f49-108">Para concluir este tutorial, você precisa ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="c8f49-108">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="c8f49-109">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="c8f49-109">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c8f49-110">Para obter detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).</span><span class="sxs-lookup"><span data-stu-id="c8f49-110">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).</span></span>
> 
> 

<span data-ttu-id="c8f49-111">Este tutorial exige o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c8f49-111">This tutorial requires the following:</span></span>

* <span data-ttu-id="c8f49-112">Xcode, que pode ser instalado em seu Mac App Store (para implantação no iOS)</span><span class="sxs-lookup"><span data-stu-id="c8f49-112">XCode, which you can install from Mac App Store (for deploying to iOS)</span></span>
* <span data-ttu-id="c8f49-113">[SDK do Android e Emulador](http://developer.android.com/sdk/installing/index.html) (para a implantação no Android)</span><span class="sxs-lookup"><span data-stu-id="c8f49-113">[Android SDK & Emulator](http://developer.android.com/sdk/installing/index.html) (for deploying to Android)</span></span>
* <span data-ttu-id="c8f49-114">Certificado de notificação por push (.p12) que pode ser obtido no seu centro de desenvolvimento da Apple para APNS</span><span class="sxs-lookup"><span data-stu-id="c8f49-114">Push notification certificate (.p12) that you can obtain from Apple Dev Center for APNS</span></span>
* <span data-ttu-id="c8f49-115">Número do projeto do GCM que pode ser obtido seu Console de Desenvolvedor do Google para GCM</span><span class="sxs-lookup"><span data-stu-id="c8f49-115">GCM Project number that you can obtain from your Google Developer Console for GCM</span></span>
* [<span data-ttu-id="c8f49-116">Plug-in do Mobile Engagement Cordova</span><span class="sxs-lookup"><span data-stu-id="c8f49-116">Mobile Engagement Cordova Plugin</span></span>](https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-engagement)

> [!NOTE]
> <span data-ttu-id="c8f49-117">Você pode encontrar o código-fonte e o arquivo ReadMe do plug-in Cordova no [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span><span class="sxs-lookup"><span data-stu-id="c8f49-117">You can find the source code and the ReadMe for the Cordova plugin on [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span></span>
> 
> 

## <span data-ttu-id="c8f49-118"><a id="setup-azme"></a>Configurar o Mobile Engagement para seu aplicativo Cordova</span><span class="sxs-lookup"><span data-stu-id="c8f49-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Cordova app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="c8f49-119"><a id="connecting-app"></a>Conectando seu aplicativo ao back-end do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="c8f49-119"><a id="connecting-app"></a>Connecting your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="c8f49-120">Este tutorial apresenta uma "integração básica" que é o conjunto mínimo exigido para coletar dados e enviar uma notificação por push.</span><span class="sxs-lookup"><span data-stu-id="c8f49-120">This tutorial presents a "basic integration" which is the minimal set required to collect data and send a push notification.</span></span> 

<span data-ttu-id="c8f49-121">Criaremos um aplicativo básico com Cordova para demonstrar a integração:</span><span class="sxs-lookup"><span data-stu-id="c8f49-121">We will create a basic app with Cordova to demonstrate the integration:</span></span>

### <a name="create-a-new-cordova-project"></a><span data-ttu-id="c8f49-122">Crie um novo projeto com Cordova</span><span class="sxs-lookup"><span data-stu-id="c8f49-122">Create a new Cordova project</span></span>
1. <span data-ttu-id="c8f49-123">Inicie a janela *Terminal* no seu computador Mac e digite o seguinte que criará um novo projeto Cordova por meio do modelo padrão.</span><span class="sxs-lookup"><span data-stu-id="c8f49-123">Launch *Terminal* window on your Mac machine and type the following which will create a new Cordova project from the default template.</span></span> <span data-ttu-id="c8f49-124">Certifique-se de que o perfil de publicação que você usará para implantar seu aplicativo iOS esteja usando “com.mycompany.myapp” como o ID do aplicativo</span><span class="sxs-lookup"><span data-stu-id="c8f49-124">Make sure that the publishing profile you eventually use to deploy your iOS app is using 'com.mycompany.myapp' as the App ID.</span></span> 
   
        $ cordova create azme-cordova com.mycompany.myapp
        $ cd azme-cordova
2. <span data-ttu-id="c8f49-125">Execute o seguinte para configurar seu projeto para **iOS** e executá-lo no simulador do iOS:</span><span class="sxs-lookup"><span data-stu-id="c8f49-125">Execute the following to configure your project for **iOS** and run it in the iOS Simulator:</span></span>
   
        $ cordova platform add ios 
        $ cordova run ios
3. <span data-ttu-id="c8f49-126">Execute o seguinte para configurar seu projeto para o **Android** e execute no emulador do Android.</span><span class="sxs-lookup"><span data-stu-id="c8f49-126">Execute the following to configure your project for **Android** and run it in the Android emulator.</span></span> <span data-ttu-id="c8f49-127">Certifique-se de que as configurações de emulador do Android SDK têm seu destino como APIs do Google (Google Inc.) com a CPU / ABI como APIs Google ARM.</span><span class="sxs-lookup"><span data-stu-id="c8f49-127">Make sure that your Android SDK Emulator settings have its Target as Google APIs (Google Inc.) with the CPU / ABI as Google APIs ARM.</span></span>  
   
        $ cordova platform add android
        $ cordova run android
4. <span data-ttu-id="c8f49-128">Adicione o plug-in do Console do Cordova.</span><span class="sxs-lookup"><span data-stu-id="c8f49-128">Add the Cordova Console plugin.</span></span> 

    ```
    $ cordova plugin add cordova-plugin-console
    ``` 

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="c8f49-129">Conecte seu aplicativo ao back-end do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="c8f49-129">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="c8f49-130">Instale o plug-in do Azure Mobile Engagement Cordova e forneça os valores de variáveis para configurar o plug-in:</span><span class="sxs-lookup"><span data-stu-id="c8f49-130">Install the Azure Mobile Engagement Cordova plugin while providing the variable values to configure the plugin:</span></span>
   
        cordova plugin add cordova-plugin-ms-azure-mobile-engagement    
             --variable AZME_IOS_CONNECTION_STRING=<iOS Connection String> 
            --variable AZME_IOS_REACH_ICON=... (icon name WITH extension) 
            --variable AZME_ANDROID_CONNECTION_STRING=<Android Connection String> 
            --variable AZME_ANDROID_REACH_ICON=... (icon name WITHOUT extension)       
            --variable AZME_ANDROID_GOOGLE_PROJECT_NUMBER=... (From your Google Cloud console for sending push notifications) 
            --variable AZME_ACTION_URL =... (URL scheme which triggers the app for deep linking)
            --variable AZME_ENABLE_NATIVE_LOG=true|false
            --variable AZME_ENABLE_PLUGIN_LOG=true|false

<span data-ttu-id="c8f49-131">*Ícone de Alcance do Android* : deve ser o nome do recurso sem qualquer extensão, nem o prefixo drawable (ex: mynotificationicon), e o arquivo de ícone deve ser copiado no seu projeto Android (plataforms/android/res/drawable)</span><span class="sxs-lookup"><span data-stu-id="c8f49-131">*Android Reach Icon* : must be the name of the resource without any extension, nor drawable prefix (ex: mynotificationicon), and the icon file must be copied into your android project (platforms/android/res/drawable)</span></span>

<span data-ttu-id="c8f49-132">*Ícone de Alcance do iOS*: deve ser o nome do recurso com a extensão (ex: meuiconenotificação.png) e o arquivo de ícone deve ser adicionado ao seu projeto do iOS com XCode (usando o Menu Adicionar Arquivos)</span><span class="sxs-lookup"><span data-stu-id="c8f49-132">*iOS Reach Icon*  : must be the name of the resource with its extension (ex:  mynotificationicon.png), and the icon file must be added into your iOS project with XCode (using the Add Files Menu)</span></span>

## <span data-ttu-id="c8f49-133"><a id="monitor"></a>Habilitar monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="c8f49-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
1. <span data-ttu-id="c8f49-134">No projeto Cordova - edite **www/js/index.js** para adicionar a chamada para o Mobile Engagement para declarar uma nova atividade uma vez que o evento *deviceReady* é recebido.</span><span class="sxs-lookup"><span data-stu-id="c8f49-134">In the Cordova project - edit **www/js/index.js** to add the call to Mobile Engagement to declare a new activity once the *deviceReady* event is received.</span></span>
   
         onDeviceReady: function() {
                Engagement.startActivity("myPage",{});
            }
2. <span data-ttu-id="c8f49-135">Executar o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="c8f49-135">Run the application:</span></span>
   
   * <span data-ttu-id="c8f49-136">**Para iOS**</span><span class="sxs-lookup"><span data-stu-id="c8f49-136">**For iOS**</span></span>
     
       <span data-ttu-id="c8f49-137">Na janela `Terminal` , inicie seu aplicativo em uma nova instância do simulador, executando o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c8f49-137">In `Terminal` window launch your app in a new Simulator instance by executing the following:</span></span>
     
           cordova run ios
   * <span data-ttu-id="c8f49-138">**Para Android**</span><span class="sxs-lookup"><span data-stu-id="c8f49-138">**For Android**</span></span>
     
       <span data-ttu-id="c8f49-139">Na janela `Terminal` , inicie seu aplicativo em uma nova instância do emulador, executando o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c8f49-139">In `Terminal` window launch your app in a new emulator instance by executing the following:</span></span>
     
           cordova run android
3. <span data-ttu-id="c8f49-140">Você pode ver o seguinte nos logs do console:</span><span class="sxs-lookup"><span data-stu-id="c8f49-140">You can see the following in the console logs:</span></span>
   
        [Engagement] Agent: Session started
        [Engagement] Agent: Activity 'myPage' started
        [Engagement] Connection: Established
        [Engagement] Connection: Sent: appInfo
        [Engagement] Connection: Sent: startSession
        [Engagement] Connection: Sent: activity name='myPage'

## <span data-ttu-id="c8f49-141"><a id="monitor"></a>Conectar o aplicativo com monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="c8f49-141"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="c8f49-142"><a id="integrate-push"></a>Habilitar Notificações por Push e mensagens no aplicativo</span><span class="sxs-lookup"><span data-stu-id="c8f49-142"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="c8f49-143">O Mobile Engagement permite a você interagir com seus usuários com Notificações por Push e Mensagens no Aplicativo no contexto de campanhas.</span><span class="sxs-lookup"><span data-stu-id="c8f49-143">Mobile Engagement allows you to interact with your users using Push Notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="c8f49-144">Esse módulo é chamado de REACH no portal do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="c8f49-144">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="c8f49-145">As seções a seguir irão configurar o aplicativo para recebê-los.</span><span class="sxs-lookup"><span data-stu-id="c8f49-145">The following sections will setup your app to receive them.</span></span>

### <a name="configure-push-credentials-for-mobile-engagement"></a><span data-ttu-id="c8f49-146">Configure credenciais de Push para o Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="c8f49-146">Configure Push credentials for Mobile Engagement</span></span>
<span data-ttu-id="c8f49-147">Para permitir que o Mobile Engagement envie notificações por Push em seu nome, você precisa conceder acesso ao certificado Apple iOS ou à chave da API do servidor de GCM.</span><span class="sxs-lookup"><span data-stu-id="c8f49-147">To allow Mobile Engagement to send Push Notifications on your behalf, you need to grant it access to your Apple iOS certificate or GCM Server API Key.</span></span> 

1. <span data-ttu-id="c8f49-148">Navegue até o portal do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="c8f49-148">Navigate to your Mobile Engagement portal.</span></span> <span data-ttu-id="c8f49-149">Verifique se você está no aplicativo que estamos usando para este projeto e, em seguida, clique no botão **Engajar** na parte inferior:</span><span class="sxs-lookup"><span data-stu-id="c8f49-149">Ensure you're in the app we're using for this project and then click on the **Engage** button at the bottom:</span></span>
   
    ![][1]
2. <span data-ttu-id="c8f49-150">Você será levado para a página de configurações no Portal do Engagement.</span><span class="sxs-lookup"><span data-stu-id="c8f49-150">You will land in the settings page in your Engagement Portal.</span></span> <span data-ttu-id="c8f49-151">Nele, clique na seção **Push Nativo** :</span><span class="sxs-lookup"><span data-stu-id="c8f49-151">From there click on the **Native Push** section:</span></span>
   
    ![][2]
3. <span data-ttu-id="c8f49-152">Configure o certificado do iOS/a chave da API do servidor de GCM </span><span class="sxs-lookup"><span data-stu-id="c8f49-152">Configure iOS Certificate/GCM Server API Key</span></span>
   
    <span data-ttu-id="c8f49-153">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="c8f49-153">**[iOS]**</span></span>
   
    <span data-ttu-id="c8f49-154">a.</span><span class="sxs-lookup"><span data-stu-id="c8f49-154">a.</span></span> <span data-ttu-id="c8f49-155">Selecione seu .p12, carregue-o e digite sua senha:</span><span class="sxs-lookup"><span data-stu-id="c8f49-155">Select your .p12, upload it and type your password:</span></span>
   
    ![][3]
   
    <span data-ttu-id="c8f49-156">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="c8f49-156">**[Android]**</span></span>
   
    <span data-ttu-id="c8f49-157">a.</span><span class="sxs-lookup"><span data-stu-id="c8f49-157">a.</span></span> <span data-ttu-id="c8f49-158">Clique no ícone para editar na frente da **Chave de API** na seção Configurações do GCM e no pop-up que aparece, cole a chave do Servidor GCM e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c8f49-158">Click the edit icon in front of **API Key** in the GCM Settings section and in the popup which shows up, paste the GCM Server Key and click **OK**.</span></span> 
   
    ![][4]

### <a name="enable-push-notifications-in-the-cordova-app"></a><span data-ttu-id="c8f49-159">Habilitar notificações por push no aplicativo Cordova</span><span class="sxs-lookup"><span data-stu-id="c8f49-159">Enable push notifications in the Cordova app</span></span>
<span data-ttu-id="c8f49-160">Edite **www/js/index.js** para adicionar a chamada para o Mobile Engagement para solicitar notificações por push e declarar um manipulador:</span><span class="sxs-lookup"><span data-stu-id="c8f49-160">Edit **www/js/index.js** to add the call to Mobile Engagement to request push notifications and declare a handler:</span></span>

     onDeviceReady: function() {
           Engagement.initializeReach(  
                 // on OpenUrl  
                 function(_url) {   
                 alert(_url);   
                 });  
            Engagement.startActivity("myPage",{});  
        }

### <a name="run-the-app"></a><span data-ttu-id="c8f49-161">Execute o aplicativo</span><span class="sxs-lookup"><span data-stu-id="c8f49-161">Run the app</span></span>
<span data-ttu-id="c8f49-162">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="c8f49-162">**[iOS]**</span></span>

1. <span data-ttu-id="c8f49-163">Nós usaremos o XCode para criar e implantar o aplicativo no dispositivo para testar as notificações por push já que o iOS permite apenas notificações por push para um dispositivo real.</span><span class="sxs-lookup"><span data-stu-id="c8f49-163">We will use XCode to build and deploy the app on the device to test push notifications since iOS only allows push notifications to an actual device.</span></span> <span data-ttu-id="c8f49-164">Vá para o local no qual o projeto Cordova é criado e navegue até **...\platforms\ios**.</span><span class="sxs-lookup"><span data-stu-id="c8f49-164">Go to the location where your Cordova project is created and navigate to **...\platforms\ios** location.</span></span> <span data-ttu-id="c8f49-165">Abra o arquivo .xcodeproj nativo no XCode.</span><span class="sxs-lookup"><span data-stu-id="c8f49-165">Open up the native .xcodeproj file in XCode.</span></span> 
2. <span data-ttu-id="c8f49-166">Crie e implante o aplicativo Cordova para o dispositivo iOS usando a conta que tem o perfil de provisionamento que contém o certificado que você acabou de carregar para o portal do Mobile Engagement e a Id do aplicativo que corresponde à que você forneceu ao criar o aplicativo Cordova.</span><span class="sxs-lookup"><span data-stu-id="c8f49-166">Build and deploy the Cordova app to the iOS device using the account which has the provisioning profile containing the certificate you just uploaded to the Mobile Engagement portal and the App Id which matches the one you provided while creating the Cordova app.</span></span> <span data-ttu-id="c8f49-167">Você pode conferir o *Identificador do pacote* no arquivo **Resources\*-info.plist** no XCode para ter uma correspondência.</span><span class="sxs-lookup"><span data-stu-id="c8f49-167">You can check out the *Bundle identifier* in your **Resources\*-info.plist** file in XCode to match it up.</span></span> 
3. <span data-ttu-id="c8f49-168">Você verá o popup iOS padrão em seu dispositivo dizendo que o aplicativo solicita de permissão para enviar notificações.</span><span class="sxs-lookup"><span data-stu-id="c8f49-168">You will see the standard iOS popup on your device saying that the app requests permission to send notifications.</span></span> <span data-ttu-id="c8f49-169">Conceder permissão.</span><span class="sxs-lookup"><span data-stu-id="c8f49-169">Grant the permission.</span></span> 

<span data-ttu-id="c8f49-170">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="c8f49-170">**[Android]**</span></span>

<span data-ttu-id="c8f49-171">Você pode simplesmente usar o emulador para executar o aplicativo Android, já que as notificações GCM têm suporte no emulador do Android.</span><span class="sxs-lookup"><span data-stu-id="c8f49-171">You can simply use the emulator to run the Android app as GCM notifications are supported on the Android emulator.</span></span> 

    cordova run android

## <span data-ttu-id="c8f49-172"><a id="send"></a>Envie uma notificação para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="c8f49-172"><a id="send"></a>Send a notification to your app</span></span>
<span data-ttu-id="c8f49-173">Agora, vamos criar uma campanha de notificação por push simples que enviará um push para seu aplicativo executando o dispositivo:</span><span class="sxs-lookup"><span data-stu-id="c8f49-173">We will now create a simple Push Notification campaign that will send a push to your app running on the device:</span></span>

1. <span data-ttu-id="c8f49-174">Navegue até a guia **Reach** em seu portal do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="c8f49-174">Navigate to the **Reach** tab in your Mobile Engagement portal</span></span>
2. <span data-ttu-id="c8f49-175">Clique em **Novo Comunicado** para criar sua campanha de push.</span><span class="sxs-lookup"><span data-stu-id="c8f49-175">Click **New Announcement** to create your push campaign</span></span>
   
    ![][6]
3. <span data-ttu-id="c8f49-176">Forneça entradas para criar sua campanha do **[Android]**</span><span class="sxs-lookup"><span data-stu-id="c8f49-176">Provide inputs to create your campaign **[Android]**</span></span>
   
   * <span data-ttu-id="c8f49-177">Forneça um **Nome** para sua campanha.</span><span class="sxs-lookup"><span data-stu-id="c8f49-177">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="c8f49-178">Selecione o **Tipo de Entrega** como *Sistema de notificação* *Simples*</span><span class="sxs-lookup"><span data-stu-id="c8f49-178">Select the **Delivery Type** as *System notification* *Simple*</span></span>
   * <span data-ttu-id="c8f49-179">Selecione o **horário de entrega** como *"A Qualquer Momento"*</span><span class="sxs-lookup"><span data-stu-id="c8f49-179">Select the **Delivery time** as *"Any Time"*</span></span>
   * <span data-ttu-id="c8f49-180">Forneça um **Título** para a notificação que será a primeira linha no envio por push.</span><span class="sxs-lookup"><span data-stu-id="c8f49-180">Provide a **Title** for your notification which will be the first line in the push.</span></span>
   * <span data-ttu-id="c8f49-181">Forneça uma **Mensagem** para a notificação, que servirá como o corpo da mensagem.</span><span class="sxs-lookup"><span data-stu-id="c8f49-181">Provide a **Message** for your notification which will serve as the message body.</span></span> 
     
     ![][11]
4. <span data-ttu-id="c8f49-182">Forneça entradas para criar sua campanha do **[iOS]**</span><span class="sxs-lookup"><span data-stu-id="c8f49-182">Provide inputs to create your campaign **[iOS]**</span></span>
   
   * <span data-ttu-id="c8f49-183">Forneça um **Nome** para sua campanha.</span><span class="sxs-lookup"><span data-stu-id="c8f49-183">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="c8f49-184">Selecione o **horário de entrega** como *"Somente fora do aplicativo"*</span><span class="sxs-lookup"><span data-stu-id="c8f49-184">Select the **Delivery time** as *"Out of app only"*</span></span>
   * <span data-ttu-id="c8f49-185">Forneça um **Título** para a notificação que será a primeira linha no envio por push.</span><span class="sxs-lookup"><span data-stu-id="c8f49-185">Provide a **Title** for your notification which will be the first line in the push.</span></span>
   * <span data-ttu-id="c8f49-186">Forneça uma **Mensagem** para a notificação, que servirá como o corpo da mensagem.</span><span class="sxs-lookup"><span data-stu-id="c8f49-186">Provide a **Message** for your notification which will serve as the message body.</span></span> 
     
     ![][12]
5. <span data-ttu-id="c8f49-187">Role para baixo e, na seção Conteúdo, selecione **Somente notificação**</span><span class="sxs-lookup"><span data-stu-id="c8f49-187">Scroll down, and in the content section select **Notification only**</span></span>
   
    ![][8]
6. <span data-ttu-id="c8f49-188">[Opcional] Você também pode fornecer uma URL de ação.</span><span class="sxs-lookup"><span data-stu-id="c8f49-188">[Optional] You can also provide an Action URL.</span></span> <span data-ttu-id="c8f49-189">Verifique se ele usa um esquema de URL fornecido ao configurar a variável **AZME\_REDIRECT\_URL** do plug-in, por exemplo, *myapp://test*.</span><span class="sxs-lookup"><span data-stu-id="c8f49-189">Make sure that it uses a URL scheme provided while configuring the plugin's **AZME\_REDIRECT\_URL** variable e.g. *myapp://test*.</span></span>  
7. <span data-ttu-id="c8f49-190">Você concluiu a configuração da campanha mais básica possível.</span><span class="sxs-lookup"><span data-stu-id="c8f49-190">You're done setting the most basic campaign possible.</span></span> <span data-ttu-id="c8f49-191">Agora role para baixo novamente e clique no botão **Criar** para salvar sua campanha.</span><span class="sxs-lookup"><span data-stu-id="c8f49-191">Now scroll down again and click the **Create** button to save your campaign.</span></span>
8. <span data-ttu-id="c8f49-192">Por fim, **Ative** sua campanha</span><span class="sxs-lookup"><span data-stu-id="c8f49-192">Finally **Activate** your campaign</span></span>
   
    ![][10]
9. <span data-ttu-id="c8f49-193">Agora você deve ver uma notificação por push em seu dispositivo ou emulador como parte desta campanha.</span><span class="sxs-lookup"><span data-stu-id="c8f49-193">You should now see a push notification on your device or emulator as part of this campaign.</span></span> 

## <span data-ttu-id="c8f49-194"><a id="next-steps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c8f49-194"><a id="next-steps"></a>Next Steps</span></span>
[<span data-ttu-id="c8f49-195">Visão geral de todos os métodos disponíveis no SDK do Cordova Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="c8f49-195">Overview of all methods available with Cordova Mobile Engagement SDK</span></span>](https://github.com/Azure/azure-mobile-engagement-cordova)

<!-- Images. -->

[1]: ./media/mobile-engagement-cordova-get-started/engage-button.png
[2]: ./media/mobile-engagement-cordova-get-started/engagement-portal.png
[3]: ./media/mobile-engagement-cordova-get-started/native-push-settings.png
[4]: ./media/mobile-engagement-cordova-get-started/api-key.png
[6]: ./media/mobile-engagement-cordova-get-started/new-announcement.png
[8]: ./media/mobile-engagement-cordova-get-started/campaign-content.png
[10]: ./media/mobile-engagement-cordova-get-started/campaign-activate.png
[11]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-android.png
[12]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-ios.png

