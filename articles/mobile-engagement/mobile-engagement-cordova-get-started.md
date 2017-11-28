---
title: aaaGet iniciado com o Azure Mobile Engagement para Cordova/Phonegap
description: "Saiba como toouse Azure Mobile Engagement com análises e notificações por Push para aplicativos Cordova/Phonegap."
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
ms.openlocfilehash: e67dabbdf7886802bb058f38964e558d5ae6854c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-cordovaphonegap"></a><span data-ttu-id="d0e6f-103">Introdução ao Azure Mobile Engagement para Cordova/Phonegap</span><span class="sxs-lookup"><span data-stu-id="d0e6f-103">Get Started with Azure Mobile Engagement for Cordova/Phonegap</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="d0e6f-104">Este tópico mostra como toouse do Azure Mobile Engagement toounderstand seu aplicativo uso e enviar por push notificações toosegmented usuários para um aplicativo móvel desenvolvidos com o Cordova.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users for a mobile application developed with Cordova.</span></span>

<span data-ttu-id="d0e6f-105">Neste tutorial, criamos um aplicativo do Cordova em branco usando o Mac e integramos o SDK do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-105">In this tutorial, we will create a blank Cordova app using Mac and then integrate Mobile Engagement SDK.</span></span> <span data-ttu-id="d0e6f-106">Ele coleta dados de análise básica e recebe notificações por push usando o sistema de notificações de Push da Apple (APNS) para iOS e Google Cloud Messaging (GCM) para o Android.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-106">It collects basic analytics data and receives push notifications using Apple Push Notification System (APNS) for iOS and Google Cloud Messaging (GCM) for Android.</span></span> <span data-ttu-id="d0e6f-107">Podemos implantará essa tooan dispositivo iOS ou Android para teste.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-107">We will deploy this tooan iOS or Android device for testing.</span></span> 

> [!NOTE]
> <span data-ttu-id="d0e6f-108">toocomplete neste tutorial, você deve ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-108">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="d0e6f-109">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-109">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d0e6f-110">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).</span><span class="sxs-lookup"><span data-stu-id="d0e6f-110">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).</span></span>
> 
> 

<span data-ttu-id="d0e6f-111">Este tutorial requer o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="d0e6f-111">This tutorial requires hello following:</span></span>

* <span data-ttu-id="d0e6f-112">XCode, que você pode instalar da loja de aplicativos do Mac (para a implantação tooiOS)</span><span class="sxs-lookup"><span data-stu-id="d0e6f-112">XCode, which you can install from Mac App Store (for deploying tooiOS)</span></span>
* <span data-ttu-id="d0e6f-113">[Android SDK & emulador](http://developer.android.com/sdk/installing/index.html) (para a implantação tooAndroid)</span><span class="sxs-lookup"><span data-stu-id="d0e6f-113">[Android SDK & Emulator](http://developer.android.com/sdk/installing/index.html) (for deploying tooAndroid)</span></span>
* <span data-ttu-id="d0e6f-114">Certificado de notificação por push (.p12) que pode ser obtido no seu centro de desenvolvimento da Apple para APNS</span><span class="sxs-lookup"><span data-stu-id="d0e6f-114">Push notification certificate (.p12) that you can obtain from Apple Dev Center for APNS</span></span>
* <span data-ttu-id="d0e6f-115">Número do projeto do GCM que pode ser obtido seu Console de Desenvolvedor do Google para GCM</span><span class="sxs-lookup"><span data-stu-id="d0e6f-115">GCM Project number that you can obtain from your Google Developer Console for GCM</span></span>
* [<span data-ttu-id="d0e6f-116">Plug-in do Mobile Engagement Cordova</span><span class="sxs-lookup"><span data-stu-id="d0e6f-116">Mobile Engagement Cordova Plugin</span></span>](https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-engagement)

> [!NOTE]
> <span data-ttu-id="d0e6f-117">Você pode localizar o código-fonte hello e hello Leiame para o plug-in Cordova de saudação em [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span><span class="sxs-lookup"><span data-stu-id="d0e6f-117">You can find hello source code and hello ReadMe for hello Cordova plugin on [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span></span>
> 
> 

## <span data-ttu-id="d0e6f-118"><a id="setup-azme"></a>Configurar o Mobile Engagement para seu aplicativo Cordova</span><span class="sxs-lookup"><span data-stu-id="d0e6f-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Cordova app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="d0e6f-119"><a id="connecting-app"></a>Conectar seu back-end do aplicativo toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d0e6f-119"><a id="connecting-app"></a>Connecting your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="d0e6f-120">Este tutorial apresenta uma "integração básica" hello mínimo definido toocollect necessários dados e envia uma notificação por push.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-120">This tutorial presents a "basic integration" which is hello minimal set required toocollect data and send a push notification.</span></span> 

<span data-ttu-id="d0e6f-121">Vamos criar um aplicativo básico com a integração de saudação do Cordova toodemonstrate:</span><span class="sxs-lookup"><span data-stu-id="d0e6f-121">We will create a basic app with Cordova toodemonstrate hello integration:</span></span>

### <a name="create-a-new-cordova-project"></a><span data-ttu-id="d0e6f-122">Crie um novo projeto com Cordova</span><span class="sxs-lookup"><span data-stu-id="d0e6f-122">Create a new Cordova project</span></span>
1. <span data-ttu-id="d0e6f-123">Iniciar *Terminal* janela no seu Olá Mac máquina e o tipo que criará um novo projeto do Cordova do modelo de padrão de saudação a seguir.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-123">Launch *Terminal* window on your Mac machine and type hello following which will create a new Cordova project from hello default template.</span></span> <span data-ttu-id="d0e6f-124">Certifique-se de que a publicação Olá perfil você eventualmente use toodeploy seu aplicativo iOS está usando 'com.mycompany.myapp' como Olá ID do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-124">Make sure that hello publishing profile you eventually use toodeploy your iOS app is using 'com.mycompany.myapp' as hello App ID.</span></span> 
   
        $ cordova create azme-cordova com.mycompany.myapp
        $ cd azme-cordova
2. <span data-ttu-id="d0e6f-125">Executar Olá tooconfigure a seguir em seu projeto para **iOS** e executá-lo no simulador de iOS hello:</span><span class="sxs-lookup"><span data-stu-id="d0e6f-125">Execute hello following tooconfigure your project for **iOS** and run it in hello iOS Simulator:</span></span>
   
        $ cordova platform add ios 
        $ cordova run ios
3. <span data-ttu-id="d0e6f-126">Executar Olá tooconfigure a seguir em seu projeto para **Android** e executá-lo no emulador Android hello.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-126">Execute hello following tooconfigure your project for **Android** and run it in hello Android emulator.</span></span> <span data-ttu-id="d0e6f-127">Verifique se as configurações de emulador do Android SDK tem seu destino como APIs do Google (Google Inc.) com hello CPU / ABI como Google APIs ARM.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-127">Make sure that your Android SDK Emulator settings have its Target as Google APIs (Google Inc.) with hello CPU / ABI as Google APIs ARM.</span></span>  
   
        $ cordova platform add android
        $ cordova run android
4. <span data-ttu-id="d0e6f-128">Adicione Olá plug-in do Console do Cordova.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-128">Add hello Cordova Console plugin.</span></span> 

    ```
    $ cordova plugin add cordova-plugin-console
    ``` 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="d0e6f-129">Conectar seu back-end do aplicativo tooMobile contrato</span><span class="sxs-lookup"><span data-stu-id="d0e6f-129">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="d0e6f-130">Instale o plug-in do Azure Mobile Engagement Cordova Olá proporcionando Olá valores de variáveis tooconfigure Olá plug-in:</span><span class="sxs-lookup"><span data-stu-id="d0e6f-130">Install hello Azure Mobile Engagement Cordova plugin while providing hello variable values tooconfigure hello plugin:</span></span>
   
        cordova plugin add cordova-plugin-ms-azure-mobile-engagement    
             --variable AZME_IOS_CONNECTION_STRING=<iOS Connection String> 
            --variable AZME_IOS_REACH_ICON=... (icon name WITH extension) 
            --variable AZME_ANDROID_CONNECTION_STRING=<Android Connection String> 
            --variable AZME_ANDROID_REACH_ICON=... (icon name WITHOUT extension)       
            --variable AZME_ANDROID_GOOGLE_PROJECT_NUMBER=... (From your Google Cloud console for sending push notifications) 
            --variable AZME_ACTION_URL =... (URL scheme which triggers hello app for deep linking)
            --variable AZME_ENABLE_NATIVE_LOG=true|false
            --variable AZME_ENABLE_PLUGIN_LOG=true|false

<span data-ttu-id="d0e6f-131">*Ícone de alcançar Android* : deve ser o nome de saudação do recurso de saudação sem qualquer extensão, nem o prefixo drawable (ex: mynotificationicon), e o arquivo de ícone Olá deve ser copiado para o projeto android (plataformas/android/res/drawable)</span><span class="sxs-lookup"><span data-stu-id="d0e6f-131">*Android Reach Icon* : must be hello name of hello resource without any extension, nor drawable prefix (ex: mynotificationicon), and hello icon file must be copied into your android project (platforms/android/res/drawable)</span></span>

<span data-ttu-id="d0e6f-132">*iOS alcançar ícone* : deve ser o nome de saudação do recurso de saudação com a extensão (ex: mynotificationicon.png), e o arquivo de ícone de saudação deve ser adicionado ao seu projeto do iOS com o XCode (usando Olá adicionar arquivos Menu)</span><span class="sxs-lookup"><span data-stu-id="d0e6f-132">*iOS Reach Icon*  : must be hello name of hello resource with its extension (ex:  mynotificationicon.png), and hello icon file must be added into your iOS project with XCode (using hello Add Files Menu)</span></span>

## <span data-ttu-id="d0e6f-133"><a id="monitor"></a>Habilitar monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="d0e6f-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
1. <span data-ttu-id="d0e6f-134">No projeto do Cordova Olá - editar **www/js/index.js** tooadd chamada de saudação tooMobile contrato toodeclare uma nova atividade de uma vez Olá *deviceReady* evento é recebido.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-134">In hello Cordova project - edit **www/js/index.js** tooadd hello call tooMobile Engagement toodeclare a new activity once hello *deviceReady* event is received.</span></span>
   
         onDeviceReady: function() {
                Engagement.startActivity("myPage",{});
            }
2. <span data-ttu-id="d0e6f-135">Execute o aplicativo hello:</span><span class="sxs-lookup"><span data-stu-id="d0e6f-135">Run hello application:</span></span>
   
   * <span data-ttu-id="d0e6f-136">**Para iOS**</span><span class="sxs-lookup"><span data-stu-id="d0e6f-136">**For iOS**</span></span>
     
       <span data-ttu-id="d0e6f-137">Em `Terminal` janela inicie seu aplicativo em uma nova instância de simulador executando Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="d0e6f-137">In `Terminal` window launch your app in a new Simulator instance by executing hello following:</span></span>
     
           cordova run ios
   * <span data-ttu-id="d0e6f-138">**Para Android**</span><span class="sxs-lookup"><span data-stu-id="d0e6f-138">**For Android**</span></span>
     
       <span data-ttu-id="d0e6f-139">Em `Terminal` janela inicie seu aplicativo em uma nova instância do emulador executando Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="d0e6f-139">In `Terminal` window launch your app in a new emulator instance by executing hello following:</span></span>
     
           cordova run android
3. <span data-ttu-id="d0e6f-140">Você pode ver o seguinte Olá Olá logs do console:</span><span class="sxs-lookup"><span data-stu-id="d0e6f-140">You can see hello following in hello console logs:</span></span>
   
        [Engagement] Agent: Session started
        [Engagement] Agent: Activity 'myPage' started
        [Engagement] Connection: Established
        [Engagement] Connection: Sent: appInfo
        [Engagement] Connection: Sent: startSession
        [Engagement] Connection: Sent: activity name='myPage'

## <span data-ttu-id="d0e6f-141"><a id="monitor"></a>Conectar o aplicativo com monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="d0e6f-141"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="d0e6f-142"><a id="integrate-push"></a>Habilitar Notificações por Push e mensagens no aplicativo</span><span class="sxs-lookup"><span data-stu-id="d0e6f-142"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="d0e6f-143">Mobile Engagement permite que você toointeract com seus usuários usando notificações por Push e no aplicativo mensagens no contexto de saudação de campanhas.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-143">Mobile Engagement allows you toointeract with your users using Push Notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="d0e6f-144">Esse módulo é chamado alcance no portal do Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-144">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="d0e6f-145">Olá seções a seguir irá configurar seu aplicativo tooreceive-los.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-145">hello following sections will setup your app tooreceive them.</span></span>

### <a name="configure-push-credentials-for-mobile-engagement"></a><span data-ttu-id="d0e6f-146">Configure credenciais de Push para o Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d0e6f-146">Configure Push credentials for Mobile Engagement</span></span>
<span data-ttu-id="d0e6f-147">tooallow Mobile Engagement toosend notificações por Push em seu nome, é necessário toogrant acessar o certificado de iOS da Apple tooyour ou chave de API de servidor do GCM.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-147">tooallow Mobile Engagement toosend Push Notifications on your behalf, you need toogrant it access tooyour Apple iOS certificate or GCM Server API Key.</span></span> 

1. <span data-ttu-id="d0e6f-148">Navegue tooyour portal do compromisso de mobilidade.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-148">Navigate tooyour Mobile Engagement portal.</span></span> <span data-ttu-id="d0e6f-149">Verifique se você estiver no aplicativo hello podemos está usando para este projeto e, em seguida, clique em hello **Engage** botão na parte inferior da saudação:</span><span class="sxs-lookup"><span data-stu-id="d0e6f-149">Ensure you're in hello app we're using for this project and then click on hello **Engage** button at hello bottom:</span></span>
   
    ![][1]
2. <span data-ttu-id="d0e6f-150">Você fará com que apareça na página de configurações de saudação em seu Portal do compromisso.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-150">You will land in hello settings page in your Engagement Portal.</span></span> <span data-ttu-id="d0e6f-151">De lá, clique em Olá **Push nativo** seção:</span><span class="sxs-lookup"><span data-stu-id="d0e6f-151">From there click on hello **Native Push** section:</span></span>
   
    ![][2]
3. <span data-ttu-id="d0e6f-152">Configure o certificado do iOS/a chave da API do servidor de GCM </span><span class="sxs-lookup"><span data-stu-id="d0e6f-152">Configure iOS Certificate/GCM Server API Key</span></span>
   
    <span data-ttu-id="d0e6f-153">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="d0e6f-153">**[iOS]**</span></span>
   
    <span data-ttu-id="d0e6f-154">a.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-154">a.</span></span> <span data-ttu-id="d0e6f-155">Selecione seu .p12, carregue-o e digite sua senha:</span><span class="sxs-lookup"><span data-stu-id="d0e6f-155">Select your .p12, upload it and type your password:</span></span>
   
    ![][3]
   
    <span data-ttu-id="d0e6f-156">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="d0e6f-156">**[Android]**</span></span>
   
    <span data-ttu-id="d0e6f-157">a.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-157">a.</span></span> <span data-ttu-id="d0e6f-158">Clique em Editar saudação na frente do **chave API** na seção configurações do GCM de hello e Olá janela pop-up que aparece, cole a chave do servidor GCM de hello e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-158">Click hello edit icon in front of **API Key** in hello GCM Settings section and in hello popup which shows up, paste hello GCM Server Key and click **OK**.</span></span> 
   
    ![][4]

### <a name="enable-push-notifications-in-hello-cordova-app"></a><span data-ttu-id="d0e6f-159">Habilitar notificações por push no aplicativo Cordova de saudação</span><span class="sxs-lookup"><span data-stu-id="d0e6f-159">Enable push notifications in hello Cordova app</span></span>
<span data-ttu-id="d0e6f-160">Editar **www/js/index.js** tooadd Olá chamada tooMobile contrato toorequest notificações por push e declarar um manipulador:</span><span class="sxs-lookup"><span data-stu-id="d0e6f-160">Edit **www/js/index.js** tooadd hello call tooMobile Engagement toorequest push notifications and declare a handler:</span></span>

     onDeviceReady: function() {
           Engagement.initializeReach(  
                 // on OpenUrl  
                 function(_url) {   
                 alert(_url);   
                 });  
            Engagement.startActivity("myPage",{});  
        }

### <a name="run-hello-app"></a><span data-ttu-id="d0e6f-161">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="d0e6f-161">Run hello app</span></span>
<span data-ttu-id="d0e6f-162">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="d0e6f-162">**[iOS]**</span></span>

1. <span data-ttu-id="d0e6f-163">Vamos usar XCode toobuild e implantar o aplicativo hello em notificações por push do hello dispositivo tootest porque iOS permite apenas o dispositivo real de tooan de notificações de push.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-163">We will use XCode toobuild and deploy hello app on hello device tootest push notifications since iOS only allows push notifications tooan actual device.</span></span> <span data-ttu-id="d0e6f-164">Vá toohello local onde o projeto do Cordova é criado e navegue muito**...\platforms\ios** local.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-164">Go toohello location where your Cordova project is created and navigate too**...\platforms\ios** location.</span></span> <span data-ttu-id="d0e6f-165">Abra o arquivo de .xcodeproj nativo Olá no XCode.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-165">Open up hello native .xcodeproj file in XCode.</span></span> 
2. <span data-ttu-id="d0e6f-166">Criar e implantar Olá Cordova aplicativo toohello o dispositivo iOS usando conta Olá que tem Olá que contém o certificado Olá recém-carregado toohello portal do compromisso de mobilidade e hello Id do aplicativo que corresponde a saudação fornecido durante a criação de perfil de provisionamento Olá Cordova app.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-166">Build and deploy hello Cordova app toohello iOS device using hello account which has hello provisioning profile containing hello certificate you just uploaded toohello Mobile Engagement portal and hello App Id which matches hello one you provided while creating hello Cordova app.</span></span> <span data-ttu-id="d0e6f-167">Consulte Olá *identificador de pacote* no seu **recursos\*-Info. plist** arquivo no XCode toomatch-lo para cima.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-167">You can check out hello *Bundle identifier* in your **Resources\*-info.plist** file in XCode toomatch it up.</span></span> 
3. <span data-ttu-id="d0e6f-168">Você verá um pop-up do hello iOS padrão em seu dispositivo dizendo que o aplicativo hello solicita notificações de toosend de permissão.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-168">You will see hello standard iOS popup on your device saying that hello app requests permission toosend notifications.</span></span> <span data-ttu-id="d0e6f-169">Conceda permissão de saudação.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-169">Grant hello permission.</span></span> 

<span data-ttu-id="d0e6f-170">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="d0e6f-170">**[Android]**</span></span>

<span data-ttu-id="d0e6f-171">Você pode simplesmente usar o aplicativo Android do Olá Olá emulador toorun como notificações GCM têm suporte no emulador Android hello.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-171">You can simply use hello emulator toorun hello Android app as GCM notifications are supported on hello Android emulator.</span></span> 

    cordova run android

## <span data-ttu-id="d0e6f-172"><a id="send"></a>Enviar um aplicativo de tooyour de notificação</span><span class="sxs-lookup"><span data-stu-id="d0e6f-172"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="d0e6f-173">Agora, vamos criar uma campanha de notificação por Push simple que enviará um aplicativo de tooyour por push em execução no dispositivo hello:</span><span class="sxs-lookup"><span data-stu-id="d0e6f-173">We will now create a simple Push Notification campaign that will send a push tooyour app running on hello device:</span></span>

1. <span data-ttu-id="d0e6f-174">Navegue toohello **alcançar** no seu portal do compromisso de mobilidade</span><span class="sxs-lookup"><span data-stu-id="d0e6f-174">Navigate toohello **Reach** tab in your Mobile Engagement portal</span></span>
2. <span data-ttu-id="d0e6f-175">Clique em **novo comunicado** toocreate sua campanha de push</span><span class="sxs-lookup"><span data-stu-id="d0e6f-175">Click **New Announcement** toocreate your push campaign</span></span>
   
    ![][6]
3. <span data-ttu-id="d0e6f-176">Fornecer entradas toocreate sua campanha **[Android]**</span><span class="sxs-lookup"><span data-stu-id="d0e6f-176">Provide inputs toocreate your campaign **[Android]**</span></span>
   
   * <span data-ttu-id="d0e6f-177">Forneça um **Nome** para sua campanha.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-177">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="d0e6f-178">Selecione Olá **tipo de entrega** como *notificação do sistema* *simples*</span><span class="sxs-lookup"><span data-stu-id="d0e6f-178">Select hello **Delivery Type** as *System notification* *Simple*</span></span>
   * <span data-ttu-id="d0e6f-179">Selecione Olá **tempo de entrega** como *"Qualquer hora"*</span><span class="sxs-lookup"><span data-stu-id="d0e6f-179">Select hello **Delivery time** as *"Any Time"*</span></span>
   * <span data-ttu-id="d0e6f-180">Forneça um **título** para a notificação que será a primeira linha hello push hello.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-180">Provide a **Title** for your notification which will be hello first line in hello push.</span></span>
   * <span data-ttu-id="d0e6f-181">Forneça um **mensagem** para a notificação que servirá como o corpo da mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-181">Provide a **Message** for your notification which will serve as hello message body.</span></span> 
     
     ![][11]
4. <span data-ttu-id="d0e6f-182">Fornecer entradas toocreate sua campanha **[iOS]**</span><span class="sxs-lookup"><span data-stu-id="d0e6f-182">Provide inputs toocreate your campaign **[iOS]**</span></span>
   
   * <span data-ttu-id="d0e6f-183">Forneça um **Nome** para sua campanha.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-183">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="d0e6f-184">Selecione Olá **tempo de entrega** como *"fora do aplicativo"*</span><span class="sxs-lookup"><span data-stu-id="d0e6f-184">Select hello **Delivery time** as *"Out of app only"*</span></span>
   * <span data-ttu-id="d0e6f-185">Forneça um **título** para a notificação que será a primeira linha hello push hello.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-185">Provide a **Title** for your notification which will be hello first line in hello push.</span></span>
   * <span data-ttu-id="d0e6f-186">Forneça um **mensagem** para a notificação que servirá como o corpo da mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-186">Provide a **Message** for your notification which will serve as hello message body.</span></span> 
     
     ![][12]
5. <span data-ttu-id="d0e6f-187">Role para baixo e em Olá seção conteúda selecione **somente notificação**</span><span class="sxs-lookup"><span data-stu-id="d0e6f-187">Scroll down, and in hello content section select **Notification only**</span></span>
   
    ![][8]
6. <span data-ttu-id="d0e6f-188">[Opcional] Você também pode fornecer uma URL de ação.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-188">[Optional] You can also provide an Action URL.</span></span> <span data-ttu-id="d0e6f-189">Certifique-se de que ele usa um esquema de URL fornecido durante a configuração de saudação do plug-in **AZME\_REDIRECIONAR\_URL** variável, por exemplo, *myapp://test*.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-189">Make sure that it uses a URL scheme provided while configuring hello plugin's **AZME\_REDIRECT\_URL** variable e.g. *myapp://test*.</span></span>  
7. <span data-ttu-id="d0e6f-190">Você concluiu possíveis de campanha configuração hello mais básica.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-190">You're done setting hello most basic campaign possible.</span></span> <span data-ttu-id="d0e6f-191">Agora, role para baixo novamente e clique em Olá **criar** botão toosave sua campanha.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-191">Now scroll down again and click hello **Create** button toosave your campaign.</span></span>
8. <span data-ttu-id="d0e6f-192">Por fim, **Ative** sua campanha</span><span class="sxs-lookup"><span data-stu-id="d0e6f-192">Finally **Activate** your campaign</span></span>
   
    ![][10]
9. <span data-ttu-id="d0e6f-193">Agora você deve ver uma notificação por push em seu dispositivo ou emulador como parte desta campanha.</span><span class="sxs-lookup"><span data-stu-id="d0e6f-193">You should now see a push notification on your device or emulator as part of this campaign.</span></span> 

## <span data-ttu-id="d0e6f-194"><a id="next-steps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d0e6f-194"><a id="next-steps"></a>Next Steps</span></span>
[<span data-ttu-id="d0e6f-195">Visão geral de todos os métodos disponíveis no SDK do Cordova Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d0e6f-195">Overview of all methods available with Cordova Mobile Engagement SDK</span></span>](https://github.com/Azure/azure-mobile-engagement-cordova)

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

