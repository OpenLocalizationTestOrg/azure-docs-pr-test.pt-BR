---
title: "Notificações por Push de aaaAdd tooApache Cordova App com aplicativos móveis do Azure | Microsoft Docs"
description: "Saiba como toouse os aplicativos móveis do Azure toosend envio notificações tooyour Apache Cordova app."
services: app-service\mobile
documentationcenter: javascript
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: 92c596a9-875c-4840-b0e1-69198817576f
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 8e1b23d6145b446b6f01599337b677e2f2b31d7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-apache-cordova-app"></a><span data-ttu-id="cee99-103">Adicionar aplicativo do envio notificações tooyour Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="cee99-103">Add push notifications tooyour Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="cee99-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="cee99-104">Overview</span></span>
<span data-ttu-id="cee99-105">Neste tutorial, você deve adicionar um projeto de toohello [início rápido do Apache Cordova] notificações por push para que uma notificação por push seja enviada toohello dispositivo toda vez que um registro é inserido.</span><span class="sxs-lookup"><span data-stu-id="cee99-105">In this tutorial, you add push notifications toohello [Apache Cordova quick start] project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="cee99-106">Se você não usar Olá baixar o projeto de servidor de início rápido, precisa Olá pacote de extensão de notificação por push.</span><span class="sxs-lookup"><span data-stu-id="cee99-106">If you do not use hello downloaded quick start server project, you need hello push notification extension package.</span></span> <span data-ttu-id="cee99-107">Para obter mais informações, consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure][1].</span><span class="sxs-lookup"><span data-stu-id="cee99-107">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps][1].</span></span>

## <span data-ttu-id="cee99-108"><a name="prerequisites"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cee99-108"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="cee99-109">Este tutorial aborda um aplicativo do Apache Cordova desenvolvido com o Visual Studio 2015 que é executado em um dispositivo iOS, um dispositivo Android, um dispositivo do Windows e Olá emulador Android da Google.</span><span class="sxs-lookup"><span data-stu-id="cee99-109">This tutorial covers an Apache Cordova application developed with Visual Studio 2015 that runs on hello Google Android Emulator, an Android device, a Windows device, and an iOS device.</span></span>

<span data-ttu-id="cee99-110">toocomplete neste tutorial, você precisa:</span><span class="sxs-lookup"><span data-stu-id="cee99-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="cee99-111">Um computador com o [Visual Studio Community 2015][2] ou versão posterior.</span><span class="sxs-lookup"><span data-stu-id="cee99-111">A PC with [Visual Studio Community 2015][2] or later versions.</span></span>
* <span data-ttu-id="cee99-112">[Ferramentas do Visual Studio para Apache Cordova][4].</span><span class="sxs-lookup"><span data-stu-id="cee99-112">[Visual Studio Tools for Apache Cordova][4].</span></span>
* <span data-ttu-id="cee99-113">Uma [conta ativa do Azure][3].</span><span class="sxs-lookup"><span data-stu-id="cee99-113">An [active Azure account][3].</span></span>
* <span data-ttu-id="cee99-114">Um projeto de [Início rápido do Apache Cordova][5] concluído.</span><span class="sxs-lookup"><span data-stu-id="cee99-114">A completed [Apache Cordova quick start][5] project.</span></span>
* <span data-ttu-id="cee99-115">(Android) Uma [Conta do Google][6] com um endereço de email confirmado.</span><span class="sxs-lookup"><span data-stu-id="cee99-115">(Android) A [Google account][6] with a verified email address.</span></span>
* <span data-ttu-id="cee99-116">(iOS) Uma [associação ao Programa de Desenvolvedores da Apple][7] e um dispositivo iOS (o simulador iOS não dá suporte a envio por push).</span><span class="sxs-lookup"><span data-stu-id="cee99-116">(iOS) An [Apple Developer Program membership][7] and an iOS device (iOS Simulator does not support push).</span></span>
* <span data-ttu-id="cee99-117">(Windows) Uma [conta de desenvolvedor da Windows Store][8] e um dispositivo com Windows 10.</span><span class="sxs-lookup"><span data-stu-id="cee99-117">(Windows) A [Windows Store Developer Account][8] and a Windows 10 device.</span></span>

## <span data-ttu-id="cee99-118"><a name="configure-hub"></a>Configurar um Hub de Notificação</span><span class="sxs-lookup"><span data-stu-id="cee99-118"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

<span data-ttu-id="cee99-119">[Assista a um vídeo mostrando as etapas nesta seção][9]</span><span class="sxs-lookup"><span data-stu-id="cee99-119">[Watch a video showing steps in this section][9]</span></span>

## <a name="update-hello-server-project"></a><span data-ttu-id="cee99-120">Atualizar o projeto do servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="cee99-120">Update hello server project</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="cee99-121"><a name="add-push-to-app"></a>Modificar seu aplicativo Cordova</span><span class="sxs-lookup"><span data-stu-id="cee99-121"><a name="add-push-to-app"></a>Modify your Cordova app</span></span>
<span data-ttu-id="cee99-122">Certifique-se de que seu projeto de aplicativo do Apache Cordova está pronto toohandle notificações de push pelo plug-in por push do Cordova do hello instalar mais todos os serviços específicos de plataforma push.</span><span class="sxs-lookup"><span data-stu-id="cee99-122">Ensure your Apache Cordova app project is ready toohandle push notifications by installing hello Cordova push plugin plus any platform-specific push services.</span></span>

#### <a name="update-hello-cordova-version-in-your-project"></a><span data-ttu-id="cee99-123">Atualize a versão do Cordova Olá em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="cee99-123">Update hello Cordova version in your project.</span></span>
<span data-ttu-id="cee99-124">Se seu projeto usa uma versão anterior ao v6.1.1 do Apache Cordova, atualize o projeto de cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="cee99-124">If your project uses a version of Apache Cordova earlier than v6.1.1, update hello client project.</span></span> <span data-ttu-id="cee99-125">projeto de saudação tooupdate:</span><span class="sxs-lookup"><span data-stu-id="cee99-125">tooupdate hello project:</span></span>

* <span data-ttu-id="cee99-126">Clique com botão direito `config.xml` tooopen designer de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="cee99-126">Right-click `config.xml` tooopen hello configuration designer.</span></span>
* <span data-ttu-id="cee99-127">Selecione a guia de plataformas de saudação.</span><span class="sxs-lookup"><span data-stu-id="cee99-127">Select hello Platforms tab.</span></span>
* <span data-ttu-id="cee99-128">Escolher 6.1.1 Olá **Cordova CLI** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="cee99-128">Choose 6.1.1 in hello **Cordova CLI** text box.</span></span>
* <span data-ttu-id="cee99-129">Escolha **criar**, em seguida, **compilar solução** tooupdate projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="cee99-129">Choose **Build**, then **Build Solution** tooupdate hello project.</span></span>

#### <a name="install-hello-push-plugin"></a><span data-ttu-id="cee99-130">Instalar o plug-in de push Olá</span><span class="sxs-lookup"><span data-stu-id="cee99-130">Install hello push plugin</span></span>
<span data-ttu-id="cee99-131">Os aplicativos Apache Cordova não manipulam recursos de rede ou do dispositivo de forma nativa.</span><span class="sxs-lookup"><span data-stu-id="cee99-131">Apache Cordova applications do not natively handle device or network capabilities.</span></span>  <span data-ttu-id="cee99-132">Essas funcionalidades são fornecidas por plug-ins publicados no [npm][10] ou no GitHub.</span><span class="sxs-lookup"><span data-stu-id="cee99-132">These capabilities are provided by plugins that are published either on [npm][10] or on GitHub.</span></span>  <span data-ttu-id="cee99-133">Olá `phonegap-plugin-push` plug-in é usado toohandle notificações de envio de rede.</span><span class="sxs-lookup"><span data-stu-id="cee99-133">hello `phonegap-plugin-push` plugin is used toohandle network push notifications.</span></span>

<span data-ttu-id="cee99-134">Você pode instalar o plug-in de envio de saudação em uma das seguintes maneiras:</span><span class="sxs-lookup"><span data-stu-id="cee99-134">You can install hello push plugin in one of these ways:</span></span>

<span data-ttu-id="cee99-135">**De saudação do prompt de comando:**</span><span class="sxs-lookup"><span data-stu-id="cee99-135">**From hello command-prompt:**</span></span>

<span data-ttu-id="cee99-136">Execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="cee99-136">Execute hello following command:</span></span>

    cordova plugin add phonegap-plugin-push

<span data-ttu-id="cee99-137">**No Visual Studio:**</span><span class="sxs-lookup"><span data-stu-id="cee99-137">**From within Visual Studio:**</span></span>

1. <span data-ttu-id="cee99-138">No Gerenciador de soluções, abra Olá `config.xml` arquivo clique **plug-ins** > **personalizado**, selecione **Git** como a origem de instalação, digite `https://github.com/phonegap/phonegap-plugin-push`como fonte de saudação.</span><span class="sxs-lookup"><span data-stu-id="cee99-138">In Solution Explorer, open hello `config.xml` file click **Plugins** > **Custom**, select **Git** as the  installation source, then enter `https://github.com/phonegap/phonegap-plugin-push` as hello source.</span></span>

   ![][img1]

2. <span data-ttu-id="cee99-139">Clique em Olá seta Avançar toohello origem da instalação.</span><span class="sxs-lookup"><span data-stu-id="cee99-139">Click hello arrow next toohello installation source.</span></span>
3. <span data-ttu-id="cee99-140">Em **SENDER_ID**, se você já tiver uma ID de projeto numérico para o projeto de Console de desenvolvedor do Google hello, você pode adicioná-lo aqui.</span><span class="sxs-lookup"><span data-stu-id="cee99-140">In **SENDER_ID**, if you already have a numeric project ID for hello Google Developer Console project, you can add it here.</span></span> <span data-ttu-id="cee99-141">Caso contrário, insira um valor de espaço reservado, como 777777.</span><span class="sxs-lookup"><span data-stu-id="cee99-141">Otherwise, enter a placeholder value, like 777777.</span></span>  <span data-ttu-id="cee99-142">Se estiver direcionando o projeto para o Android, atualize esse valor no arquivo config.xml mais tarde.</span><span class="sxs-lookup"><span data-stu-id="cee99-142">If you are targeting Android, you can update this value in config.xml later.</span></span>
4. <span data-ttu-id="cee99-143">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="cee99-143">Click **Add**.</span></span>

<span data-ttu-id="cee99-144">plug-in de push Olá agora está instalado.</span><span class="sxs-lookup"><span data-stu-id="cee99-144">hello push plugin is now installed.</span></span>

#### <a name="install-hello-device-plugin"></a><span data-ttu-id="cee99-145">Instalar o plug-in de dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="cee99-145">Install hello device plugin</span></span>
<span data-ttu-id="cee99-146">Siga Olá mesmo procedimento usado tooinstall Olá push plugin.</span><span class="sxs-lookup"><span data-stu-id="cee99-146">Follow hello same procedure you used tooinstall hello push plugin.</span></span>  <span data-ttu-id="cee99-147">Adicionar plug-in do hello dispositivo na lista de plug-ins do núcleo hello (clique **plug-ins** > **Core** toofind-lo).</span><span class="sxs-lookup"><span data-stu-id="cee99-147">Add hello Device plugin from hello Core plugins list (click **Plugins** > **Core** toofind it).</span></span> <span data-ttu-id="cee99-148">É necessário que esse nome de plataforma do plug-in tooobtain hello.</span><span class="sxs-lookup"><span data-stu-id="cee99-148">You need this plugin tooobtain hello platform name.</span></span>

#### <a name="register-your-device-on-application-start-up"></a><span data-ttu-id="cee99-149">Registrar seu dispositivo na inicialização do aplicativo</span><span class="sxs-lookup"><span data-stu-id="cee99-149">Register your device on application start-up</span></span>
<span data-ttu-id="cee99-150">Inicialmente, incluiremos alguns códigos mínimos para o Android.</span><span class="sxs-lookup"><span data-stu-id="cee99-150">Initially, we include some minimal code for Android.</span></span> <span data-ttu-id="cee99-151">Mais tarde, modificar Olá aplicativo toorun em iOS ou Windows 10.</span><span class="sxs-lookup"><span data-stu-id="cee99-151">Later, modify hello app toorun on iOS or Windows 10.</span></span>

1. <span data-ttu-id="cee99-152">Adicionar uma chamada muito**registerForPushNotifications** durante a saudação de retorno de chamada para o processo de logon hello, ou final Olá Olá **onDeviceReady** método:</span><span class="sxs-lookup"><span data-stu-id="cee99-152">Add a call too**registerForPushNotifications** during hello callback for hello login process, or at hello bottom of  hello **onDeviceReady** method:</span></span>

        // Login toohello service.
        client.login('google')
            .then(function () {
                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                    // Added tooregister for push notifications.
                registerForPushNotifications();

            }, handleError);

    <span data-ttu-id="cee99-153">Este exemplo mostra a chamada **registerForPushNotifications** após a autenticação bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="cee99-153">This example shows calling **registerForPushNotifications** after authentication succeeds.</span></span>  <span data-ttu-id="cee99-154">Você pode chamar `registerForPushNotifications()` sempre que precisar.</span><span class="sxs-lookup"><span data-stu-id="cee99-154">You can call `registerForPushNotifications()` as often as is required.</span></span>

2. <span data-ttu-id="cee99-155">Adicionar Olá novo **registerForPushNotifications** método da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="cee99-155">Add hello new **registerForPushNotifications** method as follows:</span></span>

        // Register for Push Notifications. Requires that phonegap-plugin-push be installed.
        var pushRegistration = null;
        function registerForPushNotifications() {
          pushRegistration = PushNotification.init({
              android: { senderID: 'Your_Project_ID' },
              ios: { alert: 'true', badge: 'true', sound: 'true' },
              wns: {}
          });

        // Handle hello registration event.
        pushRegistration.on('registration', function (data) {
          // Get hello native platform of hello device.
          var platform = device.platform;
          // Get hello handle returned during registration.
          var handle = data.registrationId;
          // Set hello device-specific message template.
          if (platform == 'android' || platform == 'Android') {
              // Register for GCM notifications.
              client.push.register('gcm', handle, {
                  mytemplate: { body: { data: { message: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'iOS') {
              // Register for notifications.
              client.push.register('apns', handle, {
                  mytemplate: { body: { aps: { alert: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'windows') {
              // Register for WNS notifications.
              client.push.register('wns', handle, {
                  myTemplate: {
                      body: '<toast><visual><binding template="ToastText01"><text id="1">$(messageParam)</text></binding></visual></toast>',
                      headers: { 'X-WNS-Type': 'wns/toast' } }
              });
          }
        });

        pushRegistration.on('notification', function (data, d2) {
          alert('Push Received: ' + data.message);
        });

        pushRegistration.on('error', handleError);
        }
3. <span data-ttu-id="cee99-156">(Android) Olá anterior do código, substitua `Your_Project_ID` com numérica Olá ID do projeto para o aplicativo do [Console de desenvolvedor do Google][18].</span><span class="sxs-lookup"><span data-stu-id="cee99-156">(Android) In hello preceding code, replace `Your_Project_ID` with hello numeric project ID for your app from the  [Google Developer Console][18].</span></span>

## <a name="optional-configure-and-run-hello-app-on-android"></a><span data-ttu-id="cee99-157">(Opcional) Configurar e executar o aplicativo hello no Android</span><span class="sxs-lookup"><span data-stu-id="cee99-157">(Optional) Configure and run hello app on Android</span></span>
<span data-ttu-id="cee99-158">Conclua as notificações de push de tooenable esta seção para Android.</span><span class="sxs-lookup"><span data-stu-id="cee99-158">Complete this section tooenable push notifications for Android.</span></span>

#### <span data-ttu-id="cee99-159"><a name="enable-gcm"></a>Habilitar mensagens de nuvem Firebase</span><span class="sxs-lookup"><span data-stu-id="cee99-159"><a name="enable-gcm"></a>Enable Firebase Cloud Messaging</span></span>
<span data-ttu-id="cee99-160">Como pretendemos Olá plataforma Google Android inicialmente, você deve habilitar Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="cee99-160">Since we are targeting hello Google Android platform initially, you must enable Firebase Cloud Messaging.</span></span>

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <span data-ttu-id="cee99-161"><a name="configure-backend"></a>Configurar Olá aplicativo móvel back-end toosend push solicitações usando FCM</span><span class="sxs-lookup"><span data-stu-id="cee99-161"><a name="configure-backend"></a>Configure hello Mobile App backend toosend push requests using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a><span data-ttu-id="cee99-162">Configurar seu aplicativo Cordova para Android</span><span class="sxs-lookup"><span data-stu-id="cee99-162">Configure your Cordova app for Android</span></span>
<span data-ttu-id="cee99-163">Em seu aplicativo Cordova, abra config.xml e substitua `Your_Project_ID` com numérica Olá ID do projeto para o aplicativo de saudação [Console de desenvolvedor do Google][18].</span><span class="sxs-lookup"><span data-stu-id="cee99-163">In your Cordova app, open config.xml and replace `Your_Project_ID` with hello numeric project ID for your app from hello [Google Developer Console][18].</span></span>

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

<span data-ttu-id="cee99-164">Abrir js e atualizar Olá código toouse sua ID do projeto numérico.</span><span class="sxs-lookup"><span data-stu-id="cee99-164">Open index.js and update hello code toouse your numeric project ID.</span></span>

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <span data-ttu-id="cee99-165"><a name="configure-device"></a>Configurar seu dispositivo Android para depuração USB</span><span class="sxs-lookup"><span data-stu-id="cee99-165"><a name="configure-device"></a>Configure your Android device for USB debugging</span></span>
<span data-ttu-id="cee99-166">Antes de implantar seu aplicativo tooyour dispositivo Android, você precisa tooenable depuração de USB.</span><span class="sxs-lookup"><span data-stu-id="cee99-166">Before you can deploy your application tooyour Android Device, you need tooenable USB Debugging.</span></span>  <span data-ttu-id="cee99-167">Execute as etapas a seguir em seu telefone com Android:</span><span class="sxs-lookup"><span data-stu-id="cee99-167">Perform the following steps on your Android phone:</span></span>

1. <span data-ttu-id="cee99-168">Vá muito**configurações** > **sobre o telefone**, em seguida, toque em Olá **número da compilação** até que o modo de desenvolvedor está habilitado (cerca de sete vezes).</span><span class="sxs-lookup"><span data-stu-id="cee99-168">Go too**Settings** > **About phone**, then tap hello **Build number** until developer mode is enabled  (about seven times).</span></span>
2. <span data-ttu-id="cee99-169">Em **configurações** > **opções do desenvolvedor** habilitar **depuração de USB**, em seguida, conecte-se seu PC de desenvolvimento tooyour telefone Android com um cabo USB.</span><span class="sxs-lookup"><span data-stu-id="cee99-169">Back in **Settings** > **Developer Options** enable **USB debugging**, then connect your Android phone  tooyour development PC with a USB Cable.</span></span>

<span data-ttu-id="cee99-170">Testamos isso usando um dispositivo Google Nexus 5X que executa o Android 6.0 (Marshmallow).</span><span class="sxs-lookup"><span data-stu-id="cee99-170">We tested this using a Google Nexus 5X device running Android 6.0 (Marshmallow).</span></span>  <span data-ttu-id="cee99-171">No entanto, as técnicas de saudação são comuns em qualquer versão do Android moderno.</span><span class="sxs-lookup"><span data-stu-id="cee99-171">However, hello techniques are common across any modern Android release.</span></span>

#### <a name="install-google-play-services"></a><span data-ttu-id="cee99-172">Instalar os Serviços do Google Play</span><span class="sxs-lookup"><span data-stu-id="cee99-172">Install Google Play Services</span></span>
<span data-ttu-id="cee99-173">plug-in de envio de saudação se baseia em Android Google executar serviços para notificações por push.</span><span class="sxs-lookup"><span data-stu-id="cee99-173">hello push plugin relies on Android Google Play Services for push notifications.</span></span>

1. <span data-ttu-id="cee99-174">No Visual Studio, clique em **ferramentas** > **Android** > **Gerenciador de SDK do Android**, expanda Olá **Extras** pasta e seleção Olá caixa toomake-se de que cada um dos seguintes SDKs de saudação está instalada.</span><span class="sxs-lookup"><span data-stu-id="cee99-174">In Visual Studio, click **Tools** > **Android** > **Android SDK Manager**, expand hello **Extras** folder and  check hello box toomake sure that each of hello following SDKs is installed.</span></span>

   * <span data-ttu-id="cee99-175">Android 2.3 ou superior</span><span class="sxs-lookup"><span data-stu-id="cee99-175">Android 2.3 or higher</span></span>
   * <span data-ttu-id="cee99-176">Google Repository revisão 27 ou superior</span><span class="sxs-lookup"><span data-stu-id="cee99-176">Google Repository revision 27 or higher</span></span>
   * <span data-ttu-id="cee99-177">Serviços do Google Play 9.0.2 ou superior</span><span class="sxs-lookup"><span data-stu-id="cee99-177">Google Play Services 9.0.2 or higher</span></span>

2. <span data-ttu-id="cee99-178">Clique em **instalar pacotes** e aguarde Olá toocomplete de instalação.</span><span class="sxs-lookup"><span data-stu-id="cee99-178">Click **Install Packages** and wait for hello installation toocomplete.</span></span>

<span data-ttu-id="cee99-179">Hello atual necessário bibliotecas são listadas na Olá [documentação de instalação de push de plug-in de phonegap][19].</span><span class="sxs-lookup"><span data-stu-id="cee99-179">hello current required libraries are listed in hello [phonegap-plugin-push installation documentation][19].</span></span>

#### <a name="test-push-notifications-in-hello-app-on-android"></a><span data-ttu-id="cee99-180">Notificações por push de teste no aplicativo hello no Android</span><span class="sxs-lookup"><span data-stu-id="cee99-180">Test push notifications in hello app on Android</span></span>
<span data-ttu-id="cee99-181">Você pode agora as notificações por push de teste executando Olá aplicativo e inserindo itens na tabela TodoItem de saudação.</span><span class="sxs-lookup"><span data-stu-id="cee99-181">You can now test push notifications by running hello app and inserting items in hello TodoItem table.</span></span> <span data-ttu-id="cee99-182">Você pode testar no hello mesmo dispositivo ou de um segundo dispositivo, enquanto você estiver usando Olá mesmo back-end.</span><span class="sxs-lookup"><span data-stu-id="cee99-182">You can test from hello same device or from a second device, as long as you are using hello same backend.</span></span> <span data-ttu-id="cee99-183">Teste seu aplicativo Cordova na plataforma Android Olá em uma saudação maneiras a seguir:</span><span class="sxs-lookup"><span data-stu-id="cee99-183">Test your Cordova app on hello Android platform in one of hello following ways:</span></span>

* <span data-ttu-id="cee99-184">**Em um dispositivo físico:** anexar seu computador de desenvolvimento do dispositivo Android tooyour com um cabo USB.</span><span class="sxs-lookup"><span data-stu-id="cee99-184">**On a physical device:** Attach your Android device tooyour development computer with a USB cable.</span></span>  <span data-ttu-id="cee99-185">Em vez de **Emulador do Google Android**, selecione **Dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="cee99-185">Instead of **Google Android Emulator**, select **Device**.</span></span> <span data-ttu-id="cee99-186">Visual Studio implanta o dispositivo de toohello aplicativo hello e, em seguida, executa o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="cee99-186">Visual Studio deploys hello application toohello device and then runs hello application.</span></span>  <span data-ttu-id="cee99-187">Você pode interagir com o aplicativo hello no dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="cee99-187">You can then interact with hello application on hello device.</span></span>

  <span data-ttu-id="cee99-188">Melhore a experiência de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="cee99-188">Improve your development experience.</span></span>  <span data-ttu-id="cee99-189">O compartilhamento de tela de aplicativos como o [Mobizen][20] pode ajudar a desenvolver um aplicativo Android.</span><span class="sxs-lookup"><span data-stu-id="cee99-189">Screen sharing applications such as [Mobizen][20] can assist you in developing an Android application.</span></span>  <span data-ttu-id="cee99-190">Mobizen projeta o navegador da web Android tela tooa em seu computador.</span><span class="sxs-lookup"><span data-stu-id="cee99-190">Mobizen projects your Android screen tooa web browser on your PC.</span></span>

* <span data-ttu-id="cee99-191">**Em um emulador do Android**: há etapas de configuração adicionais exigidas durante a execução em um emulador.</span><span class="sxs-lookup"><span data-stu-id="cee99-191">**On an Android emulator:** There are additional configuration steps required when running on an emulator.</span></span>

    <span data-ttu-id="cee99-192">Verifique se que você está implantando tooa dispositivo virtual que tem a APIs do Google definido como destino hello, conforme mostrado no Gerenciador de dispositivo Virtual Android (AVD) hello.</span><span class="sxs-lookup"><span data-stu-id="cee99-192">Make sure you are deploying tooa virtual device that has Google APIs set as hello target, as shown in hello Android Virtual Device (AVD) manager.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    <span data-ttu-id="cee99-193">Se você quiser que um mais rápido x86 toouse emulador, você [instalar Olá HAXM driver] [ 11] e configurar Olá emulador toouse-lo.</span><span class="sxs-lookup"><span data-stu-id="cee99-193">If you want toouse a faster x86 emulator, you [install hello HAXM driver][11] and configure hello emulator toouse it.</span></span>

    <span data-ttu-id="cee99-194">Adicionar um dispositivo Android do Google conta toohello clicando **aplicativos** > **configurações** > **adicionar conta**, em seguida, siga os prompts de saudação.</span><span class="sxs-lookup"><span data-stu-id="cee99-194">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**, then follow hello prompts.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    <span data-ttu-id="cee99-195">Executar aplicativo de lista de tarefas pendentes hello como antes e inserir um novo item de tarefas.</span><span class="sxs-lookup"><span data-stu-id="cee99-195">Run hello todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="cee99-196">Neste momento, um ícone de notificação é exibido na área de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="cee99-196">This time, a notification icon is displayed in hello notification area.</span></span> <span data-ttu-id="cee99-197">Você pode abrir Olá notificação gaveta tooview Olá texto completo da notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="cee99-197">You can open hello notification drawer tooview hello full text of hello notification.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a><span data-ttu-id="cee99-198">(Opcional) Configurar e executar no iOS</span><span class="sxs-lookup"><span data-stu-id="cee99-198">(Optional) Configure and run on iOS</span></span>
<span data-ttu-id="cee99-199">Esta seção é para executar o projeto do Cordova Olá em dispositivos iOS.</span><span class="sxs-lookup"><span data-stu-id="cee99-199">This section is for running hello Cordova project on iOS devices.</span></span> <span data-ttu-id="cee99-200">Se não estiver trabalhando com dispositivos iOS, você poderá ignorar esta seção.</span><span class="sxs-lookup"><span data-stu-id="cee99-200">If you are not working with iOS devices, you can skip this section.</span></span>

#### <a name="install-and-run-hello-ios-remote-build-agent-on-a-mac-or-cloud-service"></a><span data-ttu-id="cee99-201">Instalação e execução Olá iOS remota de agente de compilação em um serviço de nuvem ou Mac</span><span class="sxs-lookup"><span data-stu-id="cee99-201">Install and run hello iOS remote build agent on a Mac or cloud service</span></span>
<span data-ttu-id="cee99-202">Antes de executar um aplicativo Cordova no iOS usando o Visual Studio, passar por etapas Olá Olá [guia de instalação do iOS] [ 12] tooinstall e Olá execução remota de agente de compilação.</span><span class="sxs-lookup"><span data-stu-id="cee99-202">Before you can run a Cordova app on iOS using Visual Studio, go through hello steps in hello [iOS Setup Guide][12] tooinstall and run hello remote build agent.</span></span>

<span data-ttu-id="cee99-203">Verifique se que você pode criar o aplicativo hello para iOS.</span><span class="sxs-lookup"><span data-stu-id="cee99-203">Make sure you can build hello app for iOS.</span></span> <span data-ttu-id="cee99-204">Hello etapas no guia de instalação de saudação são toobuild necessária para iOS do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cee99-204">hello steps in hello setup guide are required toobuild for iOS from Visual Studio.</span></span> <span data-ttu-id="cee99-205">Se você não tiver um Mac, você pode criar para iOS usando o agente de compilação remota Olá em um serviço como MacInCloud.</span><span class="sxs-lookup"><span data-stu-id="cee99-205">If you do not have a Mac, you can build for iOS using hello remote build agent on a service like MacInCloud.</span></span> <span data-ttu-id="cee99-206">Para obter mais informações, consulte [executar seu aplicativo iOS na nuvem Olá][21].</span><span class="sxs-lookup"><span data-stu-id="cee99-206">For more info, see [Run your iOS app in hello cloud][21].</span></span>

> [!NOTE]
> <span data-ttu-id="cee99-207">XCode 7 ou superior é necessário toouse Olá push plug-in no iOS.</span><span class="sxs-lookup"><span data-stu-id="cee99-207">XCode 7 or greater is required toouse hello push plugin on iOS.</span></span>

#### <a name="find-hello-id-toouse-as-your-app-id"></a><span data-ttu-id="cee99-208">Localizar Olá ID toouse como sua ID do aplicativo</span><span class="sxs-lookup"><span data-stu-id="cee99-208">Find hello ID toouse as your App ID</span></span>
<span data-ttu-id="cee99-209">Antes de registrar seu aplicativo para notificações de push, abra config em seu aplicativo Cordova, localize Olá `id` valor no elemento de widget de saudação do atributo e copiá-lo para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="cee99-209">Before you register your app for push notifications, open config.xml in your Cordova app, find hello `id` attribute value in hello widget element, and copy it for later use.</span></span> <span data-ttu-id="cee99-210">Olá XML a seguir, Olá ID é `io.cordova.myapp7777777`.</span><span class="sxs-lookup"><span data-stu-id="cee99-210">In hello following XML, hello ID is `io.cordova.myapp7777777`.</span></span>

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

<span data-ttu-id="cee99-211">Depois, use esse identificador ao criar uma ID de aplicativo no portal do desenvolvedor da Apple.</span><span class="sxs-lookup"><span data-stu-id="cee99-211">Later, use this identifier when you create an App ID on Apple's developer portal.</span></span> <span data-ttu-id="cee99-212">Se você criar uma ID de aplicativo diferente no portal do desenvolvedor hello, você deve tomar algumas etapas adicionais posteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="cee99-212">If you create a different App ID on hello developer portal, you must take a few extra steps later in this tutorial.</span></span> <span data-ttu-id="cee99-213">Olá ID no elemento widget deve corresponder Olá ID do aplicativo no portal do desenvolvedor de saudação.</span><span class="sxs-lookup"><span data-stu-id="cee99-213">hello ID in the widget element must match hello App ID on hello developer portal.</span></span>

#### <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="cee99-214">Registrar aplicativo hello para notificações por push no portal do desenvolvedor da Apple</span><span class="sxs-lookup"><span data-stu-id="cee99-214">Register hello app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[<span data-ttu-id="cee99-215">Assista a um vídeo que mostra etapas semelhantes</span><span class="sxs-lookup"><span data-stu-id="cee99-215">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-toosend-push-notifications"></a><span data-ttu-id="cee99-216">Configurar notificações por push de toosend do Azure</span><span class="sxs-lookup"><span data-stu-id="cee99-216">Configure Azure toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a><span data-ttu-id="cee99-217">Verifique se a ID do aplicativo corresponde ao aplicativo Cordova</span><span class="sxs-lookup"><span data-stu-id="cee99-217">Verify that your App ID matches your Cordova app</span></span>
<span data-ttu-id="cee99-218">Se Olá ID do aplicativo criado na sua conta de desenvolvedor da Apple já corresponder a ID de saudação do elemento de widget de saudação config, você pode ignorar esta etapa.</span><span class="sxs-lookup"><span data-stu-id="cee99-218">If hello App ID you created in your Apple Developer Account already matches hello ID of hello widget element in config.xml, you can skip this step.</span></span> <span data-ttu-id="cee99-219">No entanto, se Olá IDs não corresponderem, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="cee99-219">However, if hello IDs don't match, take hello following steps:</span></span>

1. <span data-ttu-id="cee99-220">Exclua a pasta de plataformas de saudação do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="cee99-220">Delete hello platforms folder from your project.</span></span>
2. <span data-ttu-id="cee99-221">Exclua a pasta de plug-ins de saudação do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="cee99-221">Delete hello plugins folder from your project.</span></span>
3. <span data-ttu-id="cee99-222">Exclua pasta node_modules de saudação do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="cee99-222">Delete hello node_modules folder from your project.</span></span>
4. <span data-ttu-id="cee99-223">Atualize atributo de id de saudação do elemento de widget de saudação em config.xml toouse Olá ID do aplicativo que você criou na sua conta de desenvolvedor da Apple.</span><span class="sxs-lookup"><span data-stu-id="cee99-223">Update hello id attribute of hello widget element in config.xml toouse hello App ID that you created in your  Apple Developer Account.</span></span>
5. <span data-ttu-id="cee99-224">Recompile o projeto.</span><span class="sxs-lookup"><span data-stu-id="cee99-224">Rebuild your project.</span></span>

##### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="cee99-225">Testar notificações por push em seu aplicativo iOS</span><span class="sxs-lookup"><span data-stu-id="cee99-225">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="cee99-226">No Visual Studio, verifique se **iOS** é selecionado como destino de implantação hello e, em seguida, escolha **dispositivo** toorun em seu dispositivo iOS conectado.</span><span class="sxs-lookup"><span data-stu-id="cee99-226">In Visual Studio, make sure that **iOS** is selected as hello deployment target, and then choose **Device** toorun on your connected iOS device.</span></span>

    <span data-ttu-id="cee99-227">Você pode executar em um dispositivo conectado de iOS tooyour PC usando o iTunes.</span><span class="sxs-lookup"><span data-stu-id="cee99-227">You can run on an iOS device connected tooyour PC using iTunes.</span></span> <span data-ttu-id="cee99-228">Olá simulador de iOS não dá suporte a notificações por push.</span><span class="sxs-lookup"><span data-stu-id="cee99-228">hello iOS Simulator does not support push notifications.</span></span>

2. <span data-ttu-id="cee99-229">Olá pressione **executar** botão ou **F5** no Visual Studio toobuild projeto saudação inicial Olá aplicativo em um dispositivo iOS e clique em **Okey** tooaccept as notificações de envio.</span><span class="sxs-lookup"><span data-stu-id="cee99-229">Press hello **Run** button or **F5** in Visual Studio toobuild hello project and start hello app in an iOS  device, then click **OK** tooaccept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cee99-230">Olá aplicativo solicita a confirmação para notificações por push durante a saudação executado pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="cee99-230">hello app requests confirmation for push notifications during hello first run.</span></span>

3. <span data-ttu-id="cee99-231">No aplicativo hello, digite uma tarefa e clique em hello mais (+) ícone.</span><span class="sxs-lookup"><span data-stu-id="cee99-231">In hello app, type a task, and then click hello plus (+) icon.</span></span>
4. <span data-ttu-id="cee99-232">Verifique se uma notificação é recebida e clique toodismiss Okey Olá notificação.</span><span class="sxs-lookup"><span data-stu-id="cee99-232">Verify that a notification is received, then click OK toodismiss hello notification.</span></span>

## <a name="optional-configure-and-run-on-windows"></a><span data-ttu-id="cee99-233">(Opcional) Configurar e executar no Windows</span><span class="sxs-lookup"><span data-stu-id="cee99-233">(Optional) Configure and run on Windows</span></span>
<span data-ttu-id="cee99-234">Esta seção é para executar o projeto de aplicativo do Apache Cordova Olá em dispositivos Windows 10 (plug-in do hello PhoneGap push tem suporte no Windows 10).</span><span class="sxs-lookup"><span data-stu-id="cee99-234">This section is for running hello Apache Cordova app project on Windows 10 devices (hello PhoneGap push plugin is supported on Windows 10).</span></span> <span data-ttu-id="cee99-235">Se não estiver trabalhando com dispositivos Windows, você poderá ignorar esta seção.</span><span class="sxs-lookup"><span data-stu-id="cee99-235">If you are not working with Windows devices, you can skip this section.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a><span data-ttu-id="cee99-236">Registrar seu aplicativo Windows para notificações por push com WNS</span><span class="sxs-lookup"><span data-stu-id="cee99-236">Register your Windows app for push notifications with WNS</span></span>
<span data-ttu-id="cee99-237">Opções de armazenamento de saudação toouse no Visual Studio, selecione um destino do Windows na lista de plataformas de solução hello, como **Windows x64** ou **Windows x86** (evitar **Windows AnyCPU** para notificações por push).</span><span class="sxs-lookup"><span data-stu-id="cee99-237">toouse hello Store options in Visual Studio, select a Windows target from hello Solution Platforms list, like **Windows-x64** or **Windows-x86** (avoid **Windows-AnyCPU** for push notifications).</span></span>

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

<span data-ttu-id="cee99-238">[Assista a um vídeo que mostra etapas semelhantes][13]</span><span class="sxs-lookup"><span data-stu-id="cee99-238">[Watch a video showing similar steps][13]</span></span>

#### <a name="configure-hello-notification-hub-for-wns"></a><span data-ttu-id="cee99-239">Configurar o hub de notificação Olá para o WNS</span><span class="sxs-lookup"><span data-stu-id="cee99-239">Configure hello notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-toosupport-windows-push-notifications"></a><span data-ttu-id="cee99-240">Configurar as notificações de push Cordova app toosupport Windows</span><span class="sxs-lookup"><span data-stu-id="cee99-240">Configure your Cordova app toosupport Windows push notifications</span></span>
<span data-ttu-id="cee99-241">Designer de configuração Olá aberto (com o botão direito em config.xml e selecione **View Designer**), selecione Olá **Windows** guia e escolha **Windows 10** em **Versão de destino do windows**.</span><span class="sxs-lookup"><span data-stu-id="cee99-241">Open hello configuration designer (right-click on config.xml and select **View Designer**), select hello **Windows** tab, and choose **Windows 10** under **Windows Target Version**.</span></span>

<span data-ttu-id="cee99-242">compilações de notificações por push de toosupport no padrão (depuração), build.json abrir arquivo.</span><span class="sxs-lookup"><span data-stu-id="cee99-242">toosupport push notifications in your default (debug) builds, open build.json file.</span></span> <span data-ttu-id="cee99-243">Copie a configuração de depuração "versão" tooyour de configuração.</span><span class="sxs-lookup"><span data-stu-id="cee99-243">Copy the "release" configuration tooyour debug configuration.</span></span>

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="cee99-244">Após a atualização de Olá, Olá build.json devem conter Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="cee99-244">After hello update, hello build.json should contain hello following code:</span></span>

    "windows": {
        "release": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            },
        "debug": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="cee99-245">Compile o aplicativo hello e verifique se nenhum erro.</span><span class="sxs-lookup"><span data-stu-id="cee99-245">Build hello app and verify that you have no errors.</span></span> <span data-ttu-id="cee99-246">Seu aplicativo cliente agora deve registrar para notificações de saudação do back-end de aplicativo móvel hello.</span><span class="sxs-lookup"><span data-stu-id="cee99-246">Your client app should now register for hello notifications from hello Mobile App backend.</span></span> <span data-ttu-id="cee99-247">Repita esta seção para cada projeto do Windows em sua solução.</span><span class="sxs-lookup"><span data-stu-id="cee99-247">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="cee99-248">Testar as notificações por push em seu aplicativo para Windows</span><span class="sxs-lookup"><span data-stu-id="cee99-248">Test push notifications in your Windows app</span></span>
<span data-ttu-id="cee99-249">No Visual Studio, certifique-se de que uma plataforma Windows é selecionada como destino de implantação hello, como **Windows x64** ou **Windows x86**.</span><span class="sxs-lookup"><span data-stu-id="cee99-249">In Visual Studio, make sure that a Windows platform is selected as hello deployment target, such as **Windows-x64** or **Windows-x86**.</span></span> <span data-ttu-id="cee99-250">aplicativo de saudação toorun em um PC com Windows 10 hospeda o Visual Studio, escolha **Máquina Local**.</span><span class="sxs-lookup"><span data-stu-id="cee99-250">toorun hello app on a Windows 10 PC hosting Visual Studio, choose **Local Machine**.</span></span>

<span data-ttu-id="cee99-251">Olá pressione executar botão toobuild Olá projeto e inicie o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="cee99-251">Press hello Run button toobuild hello project and start hello app.</span></span>

<span data-ttu-id="cee99-252">No aplicativo hello, digite um nome para um todoitem novo e clique em hello mais (+) ícone tooadd-lo.</span><span class="sxs-lookup"><span data-stu-id="cee99-252">In hello app, type a name for a new todoitem, and then click hello plus (+) icon tooadd it.</span></span>

<span data-ttu-id="cee99-253">Verifique se que uma notificação é recebida quando Olá item é adicionado.</span><span class="sxs-lookup"><span data-stu-id="cee99-253">Verify that a notification is received when hello item is added.</span></span>

## <span data-ttu-id="cee99-254"><a name="next-steps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cee99-254"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="cee99-255">Leia sobre [Hubs de notificação] [ 17] toolearn sobre notificações por push.</span><span class="sxs-lookup"><span data-stu-id="cee99-255">Read about [Notification Hubs][17] toolearn about push notifications.</span></span>
* <span data-ttu-id="cee99-256">Se você ainda não tiver feito isso, continuar tutorial Olá por [adicionar autenticação] [ 14] tooyour Apache Cordova app.</span><span class="sxs-lookup"><span data-stu-id="cee99-256">If you have not already done so, continue hello tutorial by [Adding Authentication][14] tooyour Apache Cordova app.</span></span>

<span data-ttu-id="cee99-257">Saiba como toouse Olá SDKs.</span><span class="sxs-lookup"><span data-stu-id="cee99-257">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="cee99-258">[SDK do Apache Cordova][15]</span><span class="sxs-lookup"><span data-stu-id="cee99-258">[Apache Cordova SDK][15]</span></span>
* <span data-ttu-id="cee99-259">[SDK do Servidor ASP.NET][1]</span><span class="sxs-lookup"><span data-stu-id="cee99-259">[ASP.NET Server SDK][1]</span></span>
* <span data-ttu-id="cee99-260">[SDK do Servidor Node.js][16]</span><span class="sxs-lookup"><span data-stu-id="cee99-260">[Node.js Server SDK][16]</span></span>

<!-- Images -->
[img1]: ./media/app-service-mobile-cordova-get-started-push/add-push-plugin.png

<!-- URLs -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: http://www.visualstudio.com/
[3]: https://azure.microsoft.com/pricing/free-trial/
[4]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[5]: app-service-mobile-cordova-get-started.md
[6]: http://go.microsoft.com/fwlink/p/?LinkId=268302
[7]: https://developer.apple.com/programs/
[8]: https://developer.microsoft.com/en-us/store/register
[9]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-3-Create-azure-notification-hub
[10]: https://www.npmjs.com/
[11]: https://taco.visualstudio.com/en-us/docs/run-app-apache/#HAXM
[12]: http://taco.visualstudio.com/en-us/docs/ios-guide/
[13]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-6-Set-up-wns-for-push
[14]: app-service-mobile-cordova-get-started-users.md
[15]: app-service-mobile-cordova-how-to-use-client-library.md
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[17]: ../notification-hubs/notification-hubs-push-notification-overview.md
[18]: https://console.developers.google.com/home/dashboard
[19]: https://github.com/phonegap/phonegap-plugin-push/blob/master/docs/INSTALLATION.md
[20]: https://www.mobizen.com/
[21]: http://taco.visualstudio.com/en-us/docs/build_ios_cloud/
