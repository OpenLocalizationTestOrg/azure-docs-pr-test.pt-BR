---
title: "Adicionar notificações por push ao aplicativo Apache Cordova com os Aplicativos Móveis do Azure | Microsoft Docs"
description: "Saiba como usar Aplicativos Móveis do Azure para enviar notificações por push para seu aplicativo Apache Cordova."
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
ms.openlocfilehash: dc3cab0a6a8b4a56ab0fba1a02e5bba9d0ed1b1f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-apache-cordova-app"></a><span data-ttu-id="e9107-103">Adicionar notificações por push ao seu aplicativo Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="e9107-103">Add push notifications to your Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="e9107-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="e9107-104">Overview</span></span>
<span data-ttu-id="e9107-105">Neste tutorial, você adicionará notificações por push ao projeto de [Início rápido do Apache Cordova] para que, sempre que um registro for inserido, uma notificação por push seja enviada.</span><span class="sxs-lookup"><span data-stu-id="e9107-105">In this tutorial, you add push notifications to the [Apache Cordova quick start] project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="e9107-106">Se você não usar o projeto baixado do início rápido do servidor, deverá adicionar o pacote de extensão de notificação por push ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="e9107-106">If you do not use the downloaded quick start server project, you need the push notification extension package.</span></span> <span data-ttu-id="e9107-107">Para saber mais, veja [Trabalhar com o SDK do servidor de back-end do .NET para Aplicativos Móveis do Azure][1].</span><span class="sxs-lookup"><span data-stu-id="e9107-107">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps][1].</span></span>

## <span data-ttu-id="e9107-108"><a name="prerequisites"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e9107-108"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="e9107-109">Este tutorial cobre um aplicativo Apache Cordova desenvolvido no Visual Studio 2015 e executado no Emulador do Google Android, em um dispositivo Android, em um dispositivo Windows e em um dispositivo iOS.</span><span class="sxs-lookup"><span data-stu-id="e9107-109">This tutorial covers an Apache Cordova application developed with Visual Studio 2015 that runs on the Google Android Emulator, an Android device, a Windows device, and an iOS device.</span></span>

<span data-ttu-id="e9107-110">Para concluir este tutorial, você precisará:</span><span class="sxs-lookup"><span data-stu-id="e9107-110">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="e9107-111">Um computador com o [Visual Studio Community 2015][2] ou versão posterior.</span><span class="sxs-lookup"><span data-stu-id="e9107-111">A PC with [Visual Studio Community 2015][2] or later versions.</span></span>
* <span data-ttu-id="e9107-112">[Ferramentas do Visual Studio para Apache Cordova][4].</span><span class="sxs-lookup"><span data-stu-id="e9107-112">[Visual Studio Tools for Apache Cordova][4].</span></span>
* <span data-ttu-id="e9107-113">Uma [conta ativa do Azure][3].</span><span class="sxs-lookup"><span data-stu-id="e9107-113">An [active Azure account][3].</span></span>
* <span data-ttu-id="e9107-114">Um projeto de [Início rápido do Apache Cordova][5] concluído.</span><span class="sxs-lookup"><span data-stu-id="e9107-114">A completed [Apache Cordova quick start][5] project.</span></span>
* <span data-ttu-id="e9107-115">(Android) Uma [Conta do Google][6] com um endereço de email confirmado.</span><span class="sxs-lookup"><span data-stu-id="e9107-115">(Android) A [Google account][6] with a verified email address.</span></span>
* <span data-ttu-id="e9107-116">(iOS) Uma [associação ao Programa de Desenvolvedores da Apple][7] e um dispositivo iOS (o simulador iOS não dá suporte a envio por push).</span><span class="sxs-lookup"><span data-stu-id="e9107-116">(iOS) An [Apple Developer Program membership][7] and an iOS device (iOS Simulator does not support push).</span></span>
* <span data-ttu-id="e9107-117">(Windows) Uma [conta de desenvolvedor da Windows Store][8] e um dispositivo com Windows 10.</span><span class="sxs-lookup"><span data-stu-id="e9107-117">(Windows) A [Windows Store Developer Account][8] and a Windows 10 device.</span></span>

## <span data-ttu-id="e9107-118"><a name="configure-hub"></a>Configurar um Hub de Notificação</span><span class="sxs-lookup"><span data-stu-id="e9107-118"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

<span data-ttu-id="e9107-119">[Assista a um vídeo mostrando as etapas nesta seção][9]</span><span class="sxs-lookup"><span data-stu-id="e9107-119">[Watch a video showing steps in this section][9]</span></span>

## <a name="update-the-server-project"></a><span data-ttu-id="e9107-120">Atualizar o projeto de servidor</span><span class="sxs-lookup"><span data-stu-id="e9107-120">Update the server project</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="e9107-121"><a name="add-push-to-app"></a>Modificar seu aplicativo Cordova</span><span class="sxs-lookup"><span data-stu-id="e9107-121"><a name="add-push-to-app"></a>Modify your Cordova app</span></span>
<span data-ttu-id="e9107-122">Verifique se seu projeto de aplicativo do Apache Cordova está pronto para lidar com notificações por push instalando o plug-in de envio por push do Cordova e outros serviços de envio por push específicos da plataforma.</span><span class="sxs-lookup"><span data-stu-id="e9107-122">Ensure your Apache Cordova app project is ready to handle push notifications by installing the Cordova push plugin plus any platform-specific push services.</span></span>

#### <a name="update-the-cordova-version-in-your-project"></a><span data-ttu-id="e9107-123">Atualize a versão do Cordova em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="e9107-123">Update the Cordova version in your project.</span></span>
<span data-ttu-id="e9107-124">Se seu projeto usar uma versão ao Apache Cordova anterior à v6.1.1, atualize o projeto do cliente.</span><span class="sxs-lookup"><span data-stu-id="e9107-124">If your project uses a version of Apache Cordova earlier than v6.1.1, update the client project.</span></span> <span data-ttu-id="e9107-125">Para atualizar o projeto:</span><span class="sxs-lookup"><span data-stu-id="e9107-125">To update the project:</span></span>

* <span data-ttu-id="e9107-126">Clique com o botão direito do mouse em `config.xml` para abrir o designer de configuração.</span><span class="sxs-lookup"><span data-stu-id="e9107-126">Right-click `config.xml` to open the configuration designer.</span></span>
* <span data-ttu-id="e9107-127">Selecione a guia Plataformas.</span><span class="sxs-lookup"><span data-stu-id="e9107-127">Select the Platforms tab.</span></span>
* <span data-ttu-id="e9107-128">Escolha 6.1.1 na caixa de texto **CLI do Cordova**.</span><span class="sxs-lookup"><span data-stu-id="e9107-128">Choose 6.1.1 in the **Cordova CLI** text box.</span></span>
* <span data-ttu-id="e9107-129">Escolha **Criar** e **Compilar Solução** para atualizar o projeto.</span><span class="sxs-lookup"><span data-stu-id="e9107-129">Choose **Build**, then **Build Solution** to update the project.</span></span>

#### <a name="install-the-push-plugin"></a><span data-ttu-id="e9107-130">Instalar o plug-in de push</span><span class="sxs-lookup"><span data-stu-id="e9107-130">Install the push plugin</span></span>
<span data-ttu-id="e9107-131">Os aplicativos Apache Cordova não manipulam recursos de rede ou do dispositivo de forma nativa.</span><span class="sxs-lookup"><span data-stu-id="e9107-131">Apache Cordova applications do not natively handle device or network capabilities.</span></span>  <span data-ttu-id="e9107-132">Essas funcionalidades são fornecidas por plug-ins publicados no [npm][10] ou no GitHub.</span><span class="sxs-lookup"><span data-stu-id="e9107-132">These capabilities are provided by plugins that are published either on [npm][10] or on GitHub.</span></span>  <span data-ttu-id="e9107-133">O plug-in `phonegap-plugin-push` é usado para manipular notificações por push de rede.</span><span class="sxs-lookup"><span data-stu-id="e9107-133">The `phonegap-plugin-push` plugin is used to handle network push notifications.</span></span>

<span data-ttu-id="e9107-134">É possível instalar o plug-in de push com uma das seguintes maneiras:</span><span class="sxs-lookup"><span data-stu-id="e9107-134">You can install the push plugin in one of these ways:</span></span>

<span data-ttu-id="e9107-135">**No prompt de comando:**</span><span class="sxs-lookup"><span data-stu-id="e9107-135">**From the command-prompt:**</span></span>

<span data-ttu-id="e9107-136">Execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="e9107-136">Execute the following command:</span></span>

    cordova plugin add phonegap-plugin-push

<span data-ttu-id="e9107-137">**No Visual Studio:**</span><span class="sxs-lookup"><span data-stu-id="e9107-137">**From within Visual Studio:**</span></span>

1. <span data-ttu-id="e9107-138">No Gerenciador de Soluções, abra o arquivo `config.xml`, clique em **Plug-ins** > **Personalizado**, selecione **Git** como a fonte de instalação e, depois, insira `https://github.com/phonegap/phonegap-plugin-push` como a fonte.</span><span class="sxs-lookup"><span data-stu-id="e9107-138">In Solution Explorer, open the `config.xml` file click **Plugins** > **Custom**, select **Git** as the  installation source, then enter `https://github.com/phonegap/phonegap-plugin-push` as the source.</span></span>

   ![][img1]

2. <span data-ttu-id="e9107-139">Clique na seta ao lado da fonte de instalação.</span><span class="sxs-lookup"><span data-stu-id="e9107-139">Click the arrow next to the installation source.</span></span>
3. <span data-ttu-id="e9107-140">Em **SENDER_ID**, se você já tiver uma ID numérica do projeto para o projeto de Console de Desenvolvedor do Google, poderá adicioná-la aqui.</span><span class="sxs-lookup"><span data-stu-id="e9107-140">In **SENDER_ID**, if you already have a numeric project ID for the Google Developer Console project, you can add it here.</span></span> <span data-ttu-id="e9107-141">Caso contrário, insira um valor de espaço reservado, como 777777.</span><span class="sxs-lookup"><span data-stu-id="e9107-141">Otherwise, enter a placeholder value, like 777777.</span></span>  <span data-ttu-id="e9107-142">Se estiver direcionando o projeto para o Android, atualize esse valor no arquivo config.xml mais tarde.</span><span class="sxs-lookup"><span data-stu-id="e9107-142">If you are targeting Android, you can update this value in config.xml later.</span></span>
4. <span data-ttu-id="e9107-143">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e9107-143">Click **Add**.</span></span>

<span data-ttu-id="e9107-144">O plug-in de push agora está instalado.</span><span class="sxs-lookup"><span data-stu-id="e9107-144">The push plugin is now installed.</span></span>

#### <a name="install-the-device-plugin"></a><span data-ttu-id="e9107-145">Instalar o plug-in do dispositivo</span><span class="sxs-lookup"><span data-stu-id="e9107-145">Install the device plugin</span></span>
<span data-ttu-id="e9107-146">Siga o mesmo procedimento usado para instalar o plug-in de push.</span><span class="sxs-lookup"><span data-stu-id="e9107-146">Follow the same procedure you used to install the push plugin.</span></span>  <span data-ttu-id="e9107-147">Adicionar o plug-in do Dispositivo na lista de plug-ins do Núcleo (clique em **Núcleo** > **de Plug-ins** para encontrá-lo).</span><span class="sxs-lookup"><span data-stu-id="e9107-147">Add the Device plugin from the Core plugins list (click **Plugins** > **Core** to find it).</span></span> <span data-ttu-id="e9107-148">Você precisa desse plug-in para obter o nome da plataforma.</span><span class="sxs-lookup"><span data-stu-id="e9107-148">You need this plugin to obtain the platform name.</span></span>

#### <a name="register-your-device-on-application-start-up"></a><span data-ttu-id="e9107-149">Registrar seu dispositivo na inicialização do aplicativo</span><span class="sxs-lookup"><span data-stu-id="e9107-149">Register your device on application start-up</span></span>
<span data-ttu-id="e9107-150">Inicialmente, incluiremos alguns códigos mínimos para o Android.</span><span class="sxs-lookup"><span data-stu-id="e9107-150">Initially, we include some minimal code for Android.</span></span> <span data-ttu-id="e9107-151">Posteriormente, modifique o aplicativo para ser executado no iOS ou Windows 10.</span><span class="sxs-lookup"><span data-stu-id="e9107-151">Later, modify the app to run on iOS or Windows 10.</span></span>

1. <span data-ttu-id="e9107-152">Adicione uma chamada para **registerForPushNotifications** durante o retorno de chamada para o processo de logon ou na parte inferior do método **onDeviceReady**:</span><span class="sxs-lookup"><span data-stu-id="e9107-152">Add a call to **registerForPushNotifications** during the callback for the login process, or at the bottom of  the **onDeviceReady** method:</span></span>

        // Login to the service.
        client.login('google')
            .then(function () {
                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh the todoItems
                refreshDisplay();

                // Wire up the UI Event Handler for the Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                    // Added to register for push notifications.
                registerForPushNotifications();

            }, handleError);

    <span data-ttu-id="e9107-153">Este exemplo mostra a chamada **registerForPushNotifications** após a autenticação bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="e9107-153">This example shows calling **registerForPushNotifications** after authentication succeeds.</span></span>  <span data-ttu-id="e9107-154">Você pode chamar `registerForPushNotifications()` sempre que precisar.</span><span class="sxs-lookup"><span data-stu-id="e9107-154">You can call `registerForPushNotifications()` as often as is required.</span></span>

2. <span data-ttu-id="e9107-155">Adicione o novo método **registerForPushNotifications** da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e9107-155">Add the new **registerForPushNotifications** method as follows:</span></span>

        // Register for Push Notifications. Requires that phonegap-plugin-push be installed.
        var pushRegistration = null;
        function registerForPushNotifications() {
          pushRegistration = PushNotification.init({
              android: { senderID: 'Your_Project_ID' },
              ios: { alert: 'true', badge: 'true', sound: 'true' },
              wns: {}
          });

        // Handle the registration event.
        pushRegistration.on('registration', function (data) {
          // Get the native platform of the device.
          var platform = device.platform;
          // Get the handle returned during registration.
          var handle = data.registrationId;
          // Set the device-specific message template.
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
3. <span data-ttu-id="e9107-156">(Android) No código anterior, substitua `Your_Project_ID` pela ID numérica do projeto do aplicativo no [Console do Desenvolvedor do Google][18].</span><span class="sxs-lookup"><span data-stu-id="e9107-156">(Android) In the preceding code, replace `Your_Project_ID` with the numeric project ID for your app from the  [Google Developer Console][18].</span></span>

## <a name="optional-configure-and-run-the-app-on-android"></a><span data-ttu-id="e9107-157">(Opcional) Configurar e executar o aplicativo no Android</span><span class="sxs-lookup"><span data-stu-id="e9107-157">(Optional) Configure and run the app on Android</span></span>
<span data-ttu-id="e9107-158">Conclua esta seção para habilitar notificações por push para o Android.</span><span class="sxs-lookup"><span data-stu-id="e9107-158">Complete this section to enable push notifications for Android.</span></span>

#### <span data-ttu-id="e9107-159"><a name="enable-gcm"></a>Habilitar mensagens de nuvem Firebase</span><span class="sxs-lookup"><span data-stu-id="e9107-159"><a name="enable-gcm"></a>Enable Firebase Cloud Messaging</span></span>
<span data-ttu-id="e9107-160">Como nosso alvo é a plataforma Google Android, primeiro você deve habilitar as mensagens de nuvem Firebase.</span><span class="sxs-lookup"><span data-stu-id="e9107-160">Since we are targeting the Google Android platform initially, you must enable Firebase Cloud Messaging.</span></span>

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <span data-ttu-id="e9107-161"><a name="configure-backend"></a>Configurar seu back-end de Aplicativo Móvel para enviar solicitações por push usando FCM</span><span class="sxs-lookup"><span data-stu-id="e9107-161"><a name="configure-backend"></a>Configure the Mobile App backend to send push requests using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a><span data-ttu-id="e9107-162">Configurar seu aplicativo Cordova para Android</span><span class="sxs-lookup"><span data-stu-id="e9107-162">Configure your Cordova app for Android</span></span>
<span data-ttu-id="e9107-163">Em seu aplicativo Cordova, abra o arquivo config.xml e substitua `Your_Project_ID` pelo valor numérico da ID de projeto para seu aplicativo no [Console de Desenvolvedor do Google][18].</span><span class="sxs-lookup"><span data-stu-id="e9107-163">In your Cordova app, open config.xml and replace `Your_Project_ID` with the numeric project ID for your app from the [Google Developer Console][18].</span></span>

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

<span data-ttu-id="e9107-164">Abra index.js e atualize o código para usar o valor numérico da ID do projeto.</span><span class="sxs-lookup"><span data-stu-id="e9107-164">Open index.js and update the code to use your numeric project ID.</span></span>

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <span data-ttu-id="e9107-165"><a name="configure-device"></a>Configurar seu dispositivo Android para depuração USB</span><span class="sxs-lookup"><span data-stu-id="e9107-165"><a name="configure-device"></a>Configure your Android device for USB debugging</span></span>
<span data-ttu-id="e9107-166">Antes de implantar seu aplicativo em seu dispositivo Android, você precisa habilitar a Depuração USB.</span><span class="sxs-lookup"><span data-stu-id="e9107-166">Before you can deploy your application to your Android Device, you need to enable USB Debugging.</span></span>  <span data-ttu-id="e9107-167">Execute as etapas a seguir em seu telefone com Android:</span><span class="sxs-lookup"><span data-stu-id="e9107-167">Perform the following steps on your Android phone:</span></span>

1. <span data-ttu-id="e9107-168">Acesse **Configurações** > **Sobre o telefone** e, depois, toque no **Número de build** até que o modo de desenvolvedor seja habilitado (cerca de sete vezes).</span><span class="sxs-lookup"><span data-stu-id="e9107-168">Go to **Settings** > **About phone**, then tap the **Build number** until developer mode is enabled  (about seven times).</span></span>
2. <span data-ttu-id="e9107-169">Novamente em **Configurações** > **Opções do Desenvolvedor**, habilite a **Depuração por USB** e, depois, conecte seu telefone Android ao computador de desenvolvimento com um Cabo USB.</span><span class="sxs-lookup"><span data-stu-id="e9107-169">Back in **Settings** > **Developer Options** enable **USB debugging**, then connect your Android phone  to your development PC with a USB Cable.</span></span>

<span data-ttu-id="e9107-170">Testamos isso usando um dispositivo Google Nexus 5X que executa o Android 6.0 (Marshmallow).</span><span class="sxs-lookup"><span data-stu-id="e9107-170">We tested this using a Google Nexus 5X device running Android 6.0 (Marshmallow).</span></span>  <span data-ttu-id="e9107-171">No entanto, as técnicas são comuns em qualquer versão moderna do Android.</span><span class="sxs-lookup"><span data-stu-id="e9107-171">However, the techniques are common across any modern Android release.</span></span>

#### <a name="install-google-play-services"></a><span data-ttu-id="e9107-172">Instalar os Serviços do Google Play</span><span class="sxs-lookup"><span data-stu-id="e9107-172">Install Google Play Services</span></span>
<span data-ttu-id="e9107-173">O plug-in de push depende dos Serviços do Google Play no Android para enviar notificações por push.</span><span class="sxs-lookup"><span data-stu-id="e9107-173">The push plugin relies on Android Google Play Services for push notifications.</span></span>

1. <span data-ttu-id="e9107-174">No Visual Studio, clique em **Ferramentas** > **Android** > **Gerenciador de SDK do Android**, expanda a pasta **Extras** e marque a caixa para garantir que cada um dos SDKs a seguir é instalado.</span><span class="sxs-lookup"><span data-stu-id="e9107-174">In Visual Studio, click **Tools** > **Android** > **Android SDK Manager**, expand the **Extras** folder and  check the box to make sure that each of the following SDKs is installed.</span></span>

   * <span data-ttu-id="e9107-175">Android 2.3 ou superior</span><span class="sxs-lookup"><span data-stu-id="e9107-175">Android 2.3 or higher</span></span>
   * <span data-ttu-id="e9107-176">Google Repository revisão 27 ou superior</span><span class="sxs-lookup"><span data-stu-id="e9107-176">Google Repository revision 27 or higher</span></span>
   * <span data-ttu-id="e9107-177">Serviços do Google Play 9.0.2 ou superior</span><span class="sxs-lookup"><span data-stu-id="e9107-177">Google Play Services 9.0.2 or higher</span></span>

2. <span data-ttu-id="e9107-178">Clique em **Instalar Pacotes** e aguarde a conclusão da instalação.</span><span class="sxs-lookup"><span data-stu-id="e9107-178">Click **Install Packages** and wait for the installation to complete.</span></span>

<span data-ttu-id="e9107-179">As bibliotecas exigidas atualmente estão listadas na [documentação de instalação do phonegap-plugin-push][19].</span><span class="sxs-lookup"><span data-stu-id="e9107-179">The current required libraries are listed in the [phonegap-plugin-push installation documentation][19].</span></span>

#### <a name="test-push-notifications-in-the-app-on-android"></a><span data-ttu-id="e9107-180">Testar notificações por push no aplicativo em Android</span><span class="sxs-lookup"><span data-stu-id="e9107-180">Test push notifications in the app on Android</span></span>
<span data-ttu-id="e9107-181">Agora é possível testar notificações por push executando o aplicativo e inserindo itens na tabela TodoItem.</span><span class="sxs-lookup"><span data-stu-id="e9107-181">You can now test push notifications by running the app and inserting items in the TodoItem table.</span></span> <span data-ttu-id="e9107-182">Você pode realizar o testo no mesmo dispositivo ou em um segundo dispositivo, desde que esteja usando o mesmo back-end.</span><span class="sxs-lookup"><span data-stu-id="e9107-182">You can test from the same device or from a second device, as long as you are using the same backend.</span></span> <span data-ttu-id="e9107-183">Teste seu aplicativo Cordova na plataforma Android usando uma das seguintes maneiras:</span><span class="sxs-lookup"><span data-stu-id="e9107-183">Test your Cordova app on the Android platform in one of the following ways:</span></span>

* <span data-ttu-id="e9107-184">**Em um dispositivo físico:** anexe seu dispositivo Android ao computador de desenvolvimento com um cabo USB.</span><span class="sxs-lookup"><span data-stu-id="e9107-184">**On a physical device:** Attach your Android device to your development computer with a USB cable.</span></span>  <span data-ttu-id="e9107-185">Em vez de **Emulador do Google Android**, selecione **Dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="e9107-185">Instead of **Google Android Emulator**, select **Device**.</span></span> <span data-ttu-id="e9107-186">O Visual Studio implanta o aplicativo no dispositivo e o executa.</span><span class="sxs-lookup"><span data-stu-id="e9107-186">Visual Studio deploys the application to the device and then runs the application.</span></span>  <span data-ttu-id="e9107-187">Em seguida, você poderá interagir com o aplicativo no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e9107-187">You can then interact with the application on the device.</span></span>

  <span data-ttu-id="e9107-188">Melhore a experiência de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="e9107-188">Improve your development experience.</span></span>  <span data-ttu-id="e9107-189">O compartilhamento de tela de aplicativos como o [Mobizen][20] pode ajudar a desenvolver um aplicativo Android.</span><span class="sxs-lookup"><span data-stu-id="e9107-189">Screen sharing applications such as [Mobizen][20] can assist you in developing an Android application.</span></span>  <span data-ttu-id="e9107-190">O Mobizen projeta sua tela Android para um navegador da Web em seu computador.</span><span class="sxs-lookup"><span data-stu-id="e9107-190">Mobizen projects your Android screen to a web browser on your PC.</span></span>

* <span data-ttu-id="e9107-191">**Em um emulador do Android**: há etapas de configuração adicionais exigidas durante a execução em um emulador.</span><span class="sxs-lookup"><span data-stu-id="e9107-191">**On an Android emulator:** There are additional configuration steps required when running on an emulator.</span></span>

    <span data-ttu-id="e9107-192">Verifique se você está implantando em um dispositivo virtual com as APIs do Google definidas como destino, conforme mostrado no Gerenciador de AVD (dispositivo virtual Android).</span><span class="sxs-lookup"><span data-stu-id="e9107-192">Make sure you are deploying to a virtual device that has Google APIs set as the target, as shown in the Android Virtual Device (AVD) manager.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    <span data-ttu-id="e9107-193">Se você quiser usar um emulador x86 mais rápido, [instale o driver HAXM][11] e configure o emulador para usá-lo.</span><span class="sxs-lookup"><span data-stu-id="e9107-193">If you want to use a faster x86 emulator, you [install the HAXM driver][11] and configure the emulator to use it.</span></span>

    <span data-ttu-id="e9107-194">Adicione uma conta do Google para o dispositivo Android clicando em **Aplicativos** > **Configurações** > **Adicionar conta** e então siga os prompts.</span><span class="sxs-lookup"><span data-stu-id="e9107-194">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**, then follow the prompts.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    <span data-ttu-id="e9107-195">Execute o aplicativo todolist como feito anteriormente s e insira um novo item de tarefa pendente.</span><span class="sxs-lookup"><span data-stu-id="e9107-195">Run the todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="e9107-196">Dessa vez, um ícone de notificação é exibido na área de notificação.</span><span class="sxs-lookup"><span data-stu-id="e9107-196">This time, a notification icon is displayed in the notification area.</span></span> <span data-ttu-id="e9107-197">Você pode abrir a gaveta de notificações para exibir o texto completo da notificação.</span><span class="sxs-lookup"><span data-stu-id="e9107-197">You can open the notification drawer to view the full text of the notification.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a><span data-ttu-id="e9107-198">(Opcional) Configurar e executar no iOS</span><span class="sxs-lookup"><span data-stu-id="e9107-198">(Optional) Configure and run on iOS</span></span>
<span data-ttu-id="e9107-199">Esta seção é para executar o projeto Cordova em dispositivos iOS.</span><span class="sxs-lookup"><span data-stu-id="e9107-199">This section is for running the Cordova project on iOS devices.</span></span> <span data-ttu-id="e9107-200">Se não estiver trabalhando com dispositivos iOS, você poderá ignorar esta seção.</span><span class="sxs-lookup"><span data-stu-id="e9107-200">If you are not working with iOS devices, you can skip this section.</span></span>

#### <a name="install-and-run-the-ios-remote-build-agent-on-a-mac-or-cloud-service"></a><span data-ttu-id="e9107-201">Instalar e executar o agente de build remoto do iOS em um Mac ou serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="e9107-201">Install and run the iOS remote build agent on a Mac or cloud service</span></span>
<span data-ttu-id="e9107-202">Antes de executar um aplicativo Cordova no iOS usando o Visual Studio, percorra as etapas no [Guia de configuração do iOS][12] para instalar e executar o agente de build remoto.</span><span class="sxs-lookup"><span data-stu-id="e9107-202">Before you can run a Cordova app on iOS using Visual Studio, go through the steps in the [iOS Setup Guide][12] to install and run the remote build agent.</span></span>

<span data-ttu-id="e9107-203">Verifique se que você pode criar o aplicativo para iOS.</span><span class="sxs-lookup"><span data-stu-id="e9107-203">Make sure you can build the app for iOS.</span></span> <span data-ttu-id="e9107-204">As etapas no guia de instalação são necessárias para criar para iOS no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e9107-204">The steps in the setup guide are required to build for iOS from Visual Studio.</span></span> <span data-ttu-id="e9107-205">Se você não tiver um Mac, poderá criar para iOS usando o agente de build remoto em um serviço como o MacInCloud.</span><span class="sxs-lookup"><span data-stu-id="e9107-205">If you do not have a Mac, you can build for iOS using the remote build agent on a service like MacInCloud.</span></span> <span data-ttu-id="e9107-206">Para saber mais, confira [Executar seu aplicativo iOS na nuvem][21].</span><span class="sxs-lookup"><span data-stu-id="e9107-206">For more info, see [Run your iOS app in the cloud][21].</span></span>

> [!NOTE]
> <span data-ttu-id="e9107-207">O XCode 7 ou superior é necessário para usar o plug-in de push no iOS.</span><span class="sxs-lookup"><span data-stu-id="e9107-207">XCode 7 or greater is required to use the push plugin on iOS.</span></span>

#### <a name="find-the-id-to-use-as-your-app-id"></a><span data-ttu-id="e9107-208">Localizar a ID a ser usada como a ID do aplicativo</span><span class="sxs-lookup"><span data-stu-id="e9107-208">Find the ID to use as your App ID</span></span>
<span data-ttu-id="e9107-209">Antes de registrar seu aplicativo para notificações por push, abra o config.xml em seu aplicativo Cordova, localize o valor de atributo `id` no elemento de widget e copie-o para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="e9107-209">Before you register your app for push notifications, open config.xml in your Cordova app, find the `id` attribute value in the widget element, and copy it for later use.</span></span> <span data-ttu-id="e9107-210">No XML a seguir, a ID é `io.cordova.myapp7777777`.</span><span class="sxs-lookup"><span data-stu-id="e9107-210">In the following XML, the ID is `io.cordova.myapp7777777`.</span></span>

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

<span data-ttu-id="e9107-211">Depois, use esse identificador ao criar uma ID de aplicativo no portal do desenvolvedor da Apple.</span><span class="sxs-lookup"><span data-stu-id="e9107-211">Later, use this identifier when you create an App ID on Apple's developer portal.</span></span> <span data-ttu-id="e9107-212">Se você criar uma ID do Aplicativo diferente no portal do desenvolvedor, deverá realizar algumas etapas adicionais posteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="e9107-212">If you create a different App ID on the developer portal, you must take a few extra steps later in this tutorial.</span></span> <span data-ttu-id="e9107-213">A ID no elemento de widget deve corresponder à ID do Aplicativo no portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="e9107-213">The ID in the widget element must match the App ID on the developer portal.</span></span>

#### <a name="register-the-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="e9107-214">Registrar o aplicativo nas notificações por push no portal do desenvolvedor da Apple</span><span class="sxs-lookup"><span data-stu-id="e9107-214">Register the app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[<span data-ttu-id="e9107-215">Assista a um vídeo que mostra etapas semelhantes</span><span class="sxs-lookup"><span data-stu-id="e9107-215">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-to-send-push-notifications"></a><span data-ttu-id="e9107-216">Configurar o Azure para enviar notificações por push</span><span class="sxs-lookup"><span data-stu-id="e9107-216">Configure Azure to send push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a><span data-ttu-id="e9107-217">Verifique se a ID do aplicativo corresponde ao aplicativo Cordova</span><span class="sxs-lookup"><span data-stu-id="e9107-217">Verify that your App ID matches your Cordova app</span></span>
<span data-ttu-id="e9107-218">Se a ID do aplicativo que criou na sua conta de desenvolvedor da Apple já corresponde à ID do elemento widget em config.xml, você pode ignorar esta etapa.</span><span class="sxs-lookup"><span data-stu-id="e9107-218">If the App ID you created in your Apple Developer Account already matches the ID of the widget element in config.xml, you can skip this step.</span></span> <span data-ttu-id="e9107-219">No entanto, se as IDs não correspondem, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="e9107-219">However, if the IDs don't match, take the following steps:</span></span>

1. <span data-ttu-id="e9107-220">Exclua a pasta plataformas do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="e9107-220">Delete the platforms folder from your project.</span></span>
2. <span data-ttu-id="e9107-221">Exclua a pasta plugins do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="e9107-221">Delete the plugins folder from your project.</span></span>
3. <span data-ttu-id="e9107-222">Exclua a pasta node_modules do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="e9107-222">Delete the node_modules folder from your project.</span></span>
4. <span data-ttu-id="e9107-223">Atualize a ID de atributo do elemento widget em config.xml para usar a ID do Aplicativo que você criou na sua Conta de Desenvolvedor da Apple.</span><span class="sxs-lookup"><span data-stu-id="e9107-223">Update the id attribute of the widget element in config.xml to use the App ID that you created in your  Apple Developer Account.</span></span>
5. <span data-ttu-id="e9107-224">Recompile o projeto.</span><span class="sxs-lookup"><span data-stu-id="e9107-224">Rebuild your project.</span></span>

##### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="e9107-225">Testar notificações por push em seu aplicativo iOS</span><span class="sxs-lookup"><span data-stu-id="e9107-225">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="e9107-226">No Visual Studio, verifique se **iOS** está selecionado como o destino da implantação e escolha **Dispositivo** para executar no dispositivo iOS conectado.</span><span class="sxs-lookup"><span data-stu-id="e9107-226">In Visual Studio, make sure that **iOS** is selected as the deployment target, and then choose **Device** to run on your connected iOS device.</span></span>

    <span data-ttu-id="e9107-227">Você pode executar em um dispositivo iOS conectado ao seu PC usando o iTunes.</span><span class="sxs-lookup"><span data-stu-id="e9107-227">You can run on an iOS device connected to your PC using iTunes.</span></span> <span data-ttu-id="e9107-228">O simulador do iOS não dá suporte a notificações por push.</span><span class="sxs-lookup"><span data-stu-id="e9107-228">The iOS Simulator does not support push notifications.</span></span>

2. <span data-ttu-id="e9107-229">Pressione o botão **Executar** ou **F5** no Visual Studio para compilar o projeto e iniciar o aplicativo em um dispositivo iOS. Em seguida, clique em **OK** para aceitar as notificações por push.</span><span class="sxs-lookup"><span data-stu-id="e9107-229">Press the **Run** button or **F5** in Visual Studio to build the project and start the app in an iOS  device, then click **OK** to accept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e9107-230">O aplicativo solicita confirmação para notificações por push durante a primeira execução.</span><span class="sxs-lookup"><span data-stu-id="e9107-230">The app requests confirmation for push notifications during the first run.</span></span>

3. <span data-ttu-id="e9107-231">No aplicativo, digite uma tarefa e, em seguida, clique no ícone do sinal de adição (+).</span><span class="sxs-lookup"><span data-stu-id="e9107-231">In the app, type a task, and then click the plus (+) icon.</span></span>
4. <span data-ttu-id="e9107-232">Verifique se uma notificação é recebida e clique em OK para ignorar a notificação.</span><span class="sxs-lookup"><span data-stu-id="e9107-232">Verify that a notification is received, then click OK to dismiss the notification.</span></span>

## <a name="optional-configure-and-run-on-windows"></a><span data-ttu-id="e9107-233">(Opcional) Configurar e executar no Windows</span><span class="sxs-lookup"><span data-stu-id="e9107-233">(Optional) Configure and run on Windows</span></span>
<span data-ttu-id="e9107-234">Esta seção é para executar o projeto de aplicativo do Apache Cordova em dispositivos com Windows 10 (o plug-in de notificação por push PhoneGap tem suporte no Windows 10).</span><span class="sxs-lookup"><span data-stu-id="e9107-234">This section is for running the Apache Cordova app project on Windows 10 devices (the PhoneGap push plugin is supported on Windows 10).</span></span> <span data-ttu-id="e9107-235">Se não estiver trabalhando com dispositivos Windows, você poderá ignorar esta seção.</span><span class="sxs-lookup"><span data-stu-id="e9107-235">If you are not working with Windows devices, you can skip this section.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a><span data-ttu-id="e9107-236">Registrar seu aplicativo Windows para notificações por push com WNS</span><span class="sxs-lookup"><span data-stu-id="e9107-236">Register your Windows app for push notifications with WNS</span></span>
<span data-ttu-id="e9107-237">Para usar as opções de Loja no Visual Studio, selecione um destino do Windows na lista Plataformas da Solução, como **Windows x64** ou **Windows x86** (evite **Windows AnyCPU** para notificações por push).</span><span class="sxs-lookup"><span data-stu-id="e9107-237">To use the Store options in Visual Studio, select a Windows target from the Solution Platforms list, like **Windows-x64** or **Windows-x86** (avoid **Windows-AnyCPU** for push notifications).</span></span>

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

<span data-ttu-id="e9107-238">[Assista a um vídeo que mostra etapas semelhantes][13]</span><span class="sxs-lookup"><span data-stu-id="e9107-238">[Watch a video showing similar steps][13]</span></span>

#### <a name="configure-the-notification-hub-for-wns"></a><span data-ttu-id="e9107-239">Configurar o hub de notificação para WNS</span><span class="sxs-lookup"><span data-stu-id="e9107-239">Configure the notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-to-support-windows-push-notifications"></a><span data-ttu-id="e9107-240">Configurar seu aplicativo Cordova para dar suporte a notificações por push do Windows</span><span class="sxs-lookup"><span data-stu-id="e9107-240">Configure your Cordova app to support Windows push notifications</span></span>
<span data-ttu-id="e9107-241">Abra o designer de configuração (clique com o botão direito do mouse no arquivo config.xml e selecione **Designer de Exibição**), selecione a guia **Windows** e escolha **Windows 10** em **Versão de Destino do Windows**.</span><span class="sxs-lookup"><span data-stu-id="e9107-241">Open the configuration designer (right-click on config.xml and select **View Designer**), select the **Windows** tab, and choose **Windows 10** under **Windows Target Version**.</span></span>

<span data-ttu-id="e9107-242">Para dar suporte a envio de notificações por push nas versões padrão, abra o arquivo build.json.</span><span class="sxs-lookup"><span data-stu-id="e9107-242">To support push notifications in your default (debug) builds, open build.json file.</span></span> <span data-ttu-id="e9107-243">Copie a configuração de "versão" em sua configuração de depuração.</span><span class="sxs-lookup"><span data-stu-id="e9107-243">Copy the "release" configuration to your debug configuration.</span></span>

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="e9107-244">Após a atualização, o build.json deve conter o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="e9107-244">After the update, the build.json should contain the following code:</span></span>

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

<span data-ttu-id="e9107-245">Compile o aplicativo e verifique se não há erros.</span><span class="sxs-lookup"><span data-stu-id="e9107-245">Build the app and verify that you have no errors.</span></span> <span data-ttu-id="e9107-246">Agora, o aplicativo cliente deve se registrar para notificações no back-end do Aplicativo Móvel.</span><span class="sxs-lookup"><span data-stu-id="e9107-246">Your client app should now register for the notifications from the Mobile App backend.</span></span> <span data-ttu-id="e9107-247">Repita esta seção para cada projeto do Windows em sua solução.</span><span class="sxs-lookup"><span data-stu-id="e9107-247">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="e9107-248">Testar as notificações por push em seu aplicativo para Windows</span><span class="sxs-lookup"><span data-stu-id="e9107-248">Test push notifications in your Windows app</span></span>
<span data-ttu-id="e9107-249">No Visual Studio, verifique se uma plataforma Windows está selecionada como o destino de implantação, como **Windows x64** ou **Windows x86**.</span><span class="sxs-lookup"><span data-stu-id="e9107-249">In Visual Studio, make sure that a Windows platform is selected as the deployment target, such as **Windows-x64** or **Windows-x86**.</span></span> <span data-ttu-id="e9107-250">Para executar o aplicativo em um PC com Windows 10 hospedando o Visual Studio, escolha **Computador Local**.</span><span class="sxs-lookup"><span data-stu-id="e9107-250">To run the app on a Windows 10 PC hosting Visual Studio, choose **Local Machine**.</span></span>

<span data-ttu-id="e9107-251">Pressione o botão Executar para compilar o projeto e iniciar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e9107-251">Press the Run button to build the project and start the app.</span></span>

<span data-ttu-id="e9107-252">No aplicativo, digite um nome para um novo todoitem e clique no ícone de adição (+) para realizar esta ação.</span><span class="sxs-lookup"><span data-stu-id="e9107-252">In the app, type a name for a new todoitem, and then click the plus (+) icon to add it.</span></span>

<span data-ttu-id="e9107-253">Verifique se uma notificação é recebida quando o item é adicionado.</span><span class="sxs-lookup"><span data-stu-id="e9107-253">Verify that a notification is received when the item is added.</span></span>

## <span data-ttu-id="e9107-254"><a name="next-steps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e9107-254"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="e9107-255">Leia sobre os [Hubs de Notificação][17] para saber mais sobre notificações por push.</span><span class="sxs-lookup"><span data-stu-id="e9107-255">Read about [Notification Hubs][17] to learn about push notifications.</span></span>
* <span data-ttu-id="e9107-256">Se você ainda não fez isso, continue o tutorial [Adicionando Autenticação][14] para o seu aplicativo Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="e9107-256">If you have not already done so, continue the tutorial by [Adding Authentication][14] to your Apache Cordova app.</span></span>

<span data-ttu-id="e9107-257">Saiba como usar os SDKs.</span><span class="sxs-lookup"><span data-stu-id="e9107-257">Learn how to use the SDKs.</span></span>

* <span data-ttu-id="e9107-258">[SDK do Apache Cordova][15]</span><span class="sxs-lookup"><span data-stu-id="e9107-258">[Apache Cordova SDK][15]</span></span>
* <span data-ttu-id="e9107-259">[SDK do Servidor ASP.NET][1]</span><span class="sxs-lookup"><span data-stu-id="e9107-259">[ASP.NET Server SDK][1]</span></span>
* <span data-ttu-id="e9107-260">[SDK do Servidor Node.js][16]</span><span class="sxs-lookup"><span data-stu-id="e9107-260">[Node.js Server SDK][16]</span></span>

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
