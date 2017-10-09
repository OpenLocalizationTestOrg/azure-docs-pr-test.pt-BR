---
title: "aaaSend notificações de push tooChrome aplicativos com Hubs de notificação do Azure | Microsoft Docs"
description: "Saiba como toouse Hubs de notificação do Azure toosend envio notificações tooa aplicativo Chrome."
services: notification-hubs
keywords: "notificações por push móveis,notificações por push,notificações por push,notificações por push do chrome"
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 75d4ff59-d04a-455f-bd44-0130a68e641f
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-chrome
ms.devlang: JavaScript
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 7dec8ab02622563bc3730a2e96820da8932d22f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="send-push-notifications-toochrome-apps-with-azure-notification-hubs"></a><span data-ttu-id="75b3d-104">Enviar por push notificações tooChrome aplicativos com Hubs de notificação do Azure</span><span class="sxs-lookup"><span data-stu-id="75b3d-104">Send push notifications tooChrome apps with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

<span data-ttu-id="75b3d-105">Este tópico mostra como toouse Hubs de notificação do Azure toosend envio notificações tooa aplicativo Chrome, que será exibido no contexto de saudação do hello navegador Google Chrome.</span><span class="sxs-lookup"><span data-stu-id="75b3d-105">This topic shows you how toouse Azure Notification Hubs toosend push notifications tooa Chrome App, which will be displayed within hello context of hello Google Chrome browser.</span></span> <span data-ttu-id="75b3d-106">Neste tutorial, criaremos um Aplicativo Chrome que recebe notificações por push usando o [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/).</span><span class="sxs-lookup"><span data-stu-id="75b3d-106">In this tutorial, we will create a Chrome app that receives push notifications by using [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/).</span></span> 

> [!NOTE]
> <span data-ttu-id="75b3d-107">toocomplete neste tutorial, você deve ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="75b3d-107">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="75b3d-108">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="75b3d-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="75b3d-109">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="75b3d-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="75b3d-110">tutorial de saudação orienta você por meio de notificações de push de tooenable essas etapas básicas:</span><span class="sxs-lookup"><span data-stu-id="75b3d-110">hello tutorial walks you through these basic steps tooenable push notifications:</span></span>

* [<span data-ttu-id="75b3d-111">Habilitar as mensagens em nuvem do Google</span><span class="sxs-lookup"><span data-stu-id="75b3d-111">Enable Google Cloud Messaging</span></span>](#register)
* [<span data-ttu-id="75b3d-112">Configurar seu Hub de Notificação</span><span class="sxs-lookup"><span data-stu-id="75b3d-112">Configure your notification hub</span></span>](#configure-hub)
* [<span data-ttu-id="75b3d-113">Conecte-se o seu hub de notificação do aplicativo Chrome toohello</span><span class="sxs-lookup"><span data-stu-id="75b3d-113">Connect your Chrome App toohello notification hub</span></span>](#connect-app)
* [<span data-ttu-id="75b3d-114">Enviar uma notificação de push tooyour aplicativo Chrome</span><span class="sxs-lookup"><span data-stu-id="75b3d-114">Send a push notification tooyour Chrome App</span></span>](#send)
* [<span data-ttu-id="75b3d-115">Funcionalidade e recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="75b3d-115">Additional functionality & capabilities</span></span>](#next-steps)

> [!NOTE]
> <span data-ttu-id="75b3d-116">Chrome as notificações de envio do aplicativo não genéricas notificações do navegador, eles são o modelo de extensibilidade de navegador específico toohello (consulte [visão geral de aplicativos do Chrome] para obter detalhes).</span><span class="sxs-lookup"><span data-stu-id="75b3d-116">Chrome app push notifications are not generic in-browser notifications - they are specific toohello browser extensibility model (see [Chrome Apps Overview] for details).</span></span> <span data-ttu-id="75b3d-117">Além disso toohello navegador de área de trabalho, Chrome aplicativos executados no dispositivo móvel (Android e iOS) por meio do Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="75b3d-117">In addition toohello desktop browser, Chrome apps run on mobile (Android and iOS) through Apache Cordova.</span></span> <span data-ttu-id="75b3d-118">Consulte [Chrome aplicativos móveis] toolearn mais.</span><span class="sxs-lookup"><span data-stu-id="75b3d-118">See [Chrome Apps on Mobile] toolearn more.</span></span>
> 
> 

<span data-ttu-id="75b3d-119">Configurar o GCM e Hubs de notificação do Azure é tooconfiguring idêntico para o Android, já que [Google Cloud Messaging cromo] foi preterido e Olá GCM mesmo agora dá suporte a dispositivos com Android e instâncias do Chrome.</span><span class="sxs-lookup"><span data-stu-id="75b3d-119">Configuring GCM and Azure Notification Hubs is identical tooconfiguring for Android, since [Google Cloud Messaging for Chrome] has been deprecated and hello same GCM now supports both Android devices and Chrome instances.</span></span>

## <span data-ttu-id="75b3d-120"><a id="register"></a>Habilitar as mensagens em nuvem do Google</span><span class="sxs-lookup"><span data-stu-id="75b3d-120"><a id="register"></a>Enable Google Cloud Messaging</span></span>
1. <span data-ttu-id="75b3d-121">Navegue toohello [Google nuvem Console] site da Web, entre com suas credenciais de conta do Google e clique em Olá **criar projeto** botão.</span><span class="sxs-lookup"><span data-stu-id="75b3d-121">Navigate toohello [Google Cloud Console] website, sign in with your Google account credentials, and then click hello **Create Project** button.</span></span> <span data-ttu-id="75b3d-122">Forneça um número apropriado **nome do projeto**e, em seguida, clique em Olá **criar** botão.</span><span class="sxs-lookup"><span data-stu-id="75b3d-122">Provide an appropriate **Project Name**, and then click hello **Create** button.</span></span>
   
       ![Google Cloud Console - Create Project][1]
2. <span data-ttu-id="75b3d-123">Anote Olá **projeto número** em Olá **projetos** página de projeto Olá que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="75b3d-123">Make a note of hello **Project Number** on hello **Projects** page for hello project that you just created.</span></span> <span data-ttu-id="75b3d-124">Você usará isso como Olá **ID do remetente GCM** em Olá Chrome aplicativo tooregister com GCM.</span><span class="sxs-lookup"><span data-stu-id="75b3d-124">You will use this as hello **GCM Sender ID** in hello Chrome App tooregister with GCM.</span></span>
   
       ![Google Cloud Console - Project Number][2]
3. <span data-ttu-id="75b3d-125">No painel esquerdo do hello, clique em **APIs & auth**e, em seguida, role para baixo e clique Olá alternância tooenable **Google Cloud Messaging para Android**.</span><span class="sxs-lookup"><span data-stu-id="75b3d-125">In hello left pane, click **APIs & auth**, and then scroll down and click hello toggle tooenable **Google Cloud Messaging for Android**.</span></span> <span data-ttu-id="75b3d-126">Você não tem tooenable **Google Cloud Messaging cromo**.</span><span class="sxs-lookup"><span data-stu-id="75b3d-126">You don't have tooenable **Google Cloud Messaging for Chrome**.</span></span>
   
       ![Google Cloud Console - Server Key][3]
4. <span data-ttu-id="75b3d-127">No painel esquerdo do hello, clique em **credenciais** > **criar nova chave** > **chave do servidor** > **criar**.</span><span class="sxs-lookup"><span data-stu-id="75b3d-127">In hello left pane, click **Credentials** > **Create New Key** > **Server Key** > **Create**.</span></span>
   
       ![Google Cloud Console - Credentials][4]
5. <span data-ttu-id="75b3d-128">Tome nota do servidor de saudação **chave API**.</span><span class="sxs-lookup"><span data-stu-id="75b3d-128">Make a note of hello server **API Key**.</span></span> <span data-ttu-id="75b3d-129">Você vai configurar isso em seu tooenable em seguida, do hub de notificação-toosend tooGCM de notificações de envio.</span><span class="sxs-lookup"><span data-stu-id="75b3d-129">You will configure this in your notification hub next, tooenable it toosend push notifications tooGCM.</span></span>
   
       ![Google Cloud Console - API Key][5]

## <span data-ttu-id="75b3d-130"><a id="configure-hub"></a>Configurar seu Hub de Notificação</span><span class="sxs-lookup"><span data-stu-id="75b3d-130"><a id="configure-hub"></a>Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="75b3d-131">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="75b3d-131">&emsp;&emsp;6.</span></span>   <span data-ttu-id="75b3d-132">Em Olá **configurações** folha, selecione **Notification Services** e **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="75b3d-132">In hello **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="75b3d-133">Insira a chave de API hello e salvar.</span><span class="sxs-lookup"><span data-stu-id="75b3d-133">Enter hello API key and save.</span></span>

&emsp;&emsp;![Hubs de Notificação do Azure - Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

## <span data-ttu-id="75b3d-135"><a id="connect-app"></a>Conecte-se o seu hub de notificação do aplicativo Chrome toohello</span><span class="sxs-lookup"><span data-stu-id="75b3d-135"><a id="connect-app"></a>Connect your Chrome App toohello notification hub</span></span>
<span data-ttu-id="75b3d-136">Hub de notificação está agora configurado toowork com GCM e ter tooregister de cadeias de caracteres de conexão Olá tooboth seu aplicativo para receber e enviar notificações por push.</span><span class="sxs-lookup"><span data-stu-id="75b3d-136">Your notification hub is now configured toowork with GCM, and you have hello connection strings tooregister your app tooboth receive and send push notifications.</span></span> <span data-ttu-id="75b3d-137">LK</span><span class="sxs-lookup"><span data-stu-id="75b3d-137">LK</span></span>

### <a name="create-a-new-chrome-app"></a><span data-ttu-id="75b3d-138">Criar um novo Aplicativo Chrome</span><span class="sxs-lookup"><span data-stu-id="75b3d-138">Create a new Chrome App</span></span>
<span data-ttu-id="75b3d-139">exemplo Hello abaixo se baseia Olá [Chrome aplicativo GCM exemplo] e usa Olá recomendado toocreate de maneira um aplicativo Chrome.</span><span class="sxs-lookup"><span data-stu-id="75b3d-139">hello sample below is based on hello [Chrome App GCM Sample] and uses hello recommended way toocreate a Chrome App.</span></span> <span data-ttu-id="75b3d-140">Vamos destacar Olá de etapas relacionadas especificamente tooAzure Hubs de notificação.</span><span class="sxs-lookup"><span data-stu-id="75b3d-140">We will highlight hello steps specifically related tooAzure Notification Hubs.</span></span> 

> [!NOTE]
> <span data-ttu-id="75b3d-141">É recomendável que você baixe fonte Olá para este aplicativo de cromo do [exemplo de Hub de notificação de aplicativo Chrome].</span><span class="sxs-lookup"><span data-stu-id="75b3d-141">We recommend that you download hello source for this Chrome App from [Chrome App Notification Hub Sample].</span></span>
> 
> 

<span data-ttu-id="75b3d-142">Olá Chrome aplicativo é criado por meio de JavaScript, e você pode usar qualquer um dos editores word preferencial para criá-lo.</span><span class="sxs-lookup"><span data-stu-id="75b3d-142">hello Chrome App is created via JavaScript, and you can use any of your preferred word editors for creating it.</span></span> <span data-ttu-id="75b3d-143">Abaixo, esta é a aparência desse aplicativo Chrome.</span><span class="sxs-lookup"><span data-stu-id="75b3d-143">Below is what this Chrome App will look like.</span></span>

![Aplicativo Google Chrome][15]

1. <span data-ttu-id="75b3d-145">Crie uma pasta e chame-a de `ChromePushApp`.</span><span class="sxs-lookup"><span data-stu-id="75b3d-145">Create a folder and name it `ChromePushApp`.</span></span> <span data-ttu-id="75b3d-146">Naturalmente, o nome de saudação é arbitrário - se você o nomear algo diferente, certifique-se de que substituir o caminho Olá em segmentos de código Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="75b3d-146">Of course, hello name is arbitrary - if you name it something different, make sure you substitute hello path in hello required code segments.</span></span>
2. <span data-ttu-id="75b3d-147">Baixar Olá [biblioteca de criptografia js] na pasta Olá criado na etapa segundo hello.</span><span class="sxs-lookup"><span data-stu-id="75b3d-147">Download hello [crypto-js library] in hello folder you created in hello second step.</span></span> <span data-ttu-id="75b3d-148">Essa pasta de biblioteca contém duas subpastas: `components` e `rollups`.</span><span class="sxs-lookup"><span data-stu-id="75b3d-148">This library folder will contain two subfolders: `components` and `rollups`.</span></span>
3. <span data-ttu-id="75b3d-149">Crie um arquivo do `manifest.json` .</span><span class="sxs-lookup"><span data-stu-id="75b3d-149">Create a `manifest.json` file.</span></span> <span data-ttu-id="75b3d-150">Todos os aplicativos de cromo contam com um arquivo de manifesto que contém metadados do aplicativo hello e, mais importante, todas as permissões que são concedidas toohello aplicativo quando o usuário Olá instala.</span><span class="sxs-lookup"><span data-stu-id="75b3d-150">All Chrome Apps are backed by a manifest file that contains hello app metadata and, most importantly, all permissions that are granted toohello app when hello user installs it.</span></span>
   
        {
          "name": "NH-GCM Notifications",
          "description": "Chrome platform app.",
          "manifest_version": 2,
          "version": "0.1",
          "app": {
            "background": {
              "scripts": ["background.js"]
            }
          },
          "permissions": ["gcm", "storage", "notifications", "https://*.servicebus.windows.net/*"],
          "icons": { "128": "gcm_128.png" }
        }
   
    <span data-ttu-id="75b3d-151">Saudação de aviso `permissions` elemento, que especifica que este aplicativo Chrome será capaz de tooreceive as notificações de envio do GCM.</span><span class="sxs-lookup"><span data-stu-id="75b3d-151">Notice hello `permissions` element, which specifies that this Chrome App will be able tooreceive push notifications from GCM.</span></span> <span data-ttu-id="75b3d-152">Ele também deve especificar Olá URI de Hubs de notificação do Azure onde Olá Chrome aplicativo fará um tooregister da chamada REST.</span><span class="sxs-lookup"><span data-stu-id="75b3d-152">It must also specify hello Azure Notification Hubs URI where hello Chrome App will make a REST call tooregister.</span></span>
    <span data-ttu-id="75b3d-153">Nosso aplicativo de exemplo também usa um arquivo de ícone, `gcm_128.png`, que você encontrará na fonte de saudação que é reutilizado de exemplo do hello original GCM.</span><span class="sxs-lookup"><span data-stu-id="75b3d-153">Our sample app also uses an icon file, `gcm_128.png`, that you will find at hello source that's reused from hello original GCM sample.</span></span> <span data-ttu-id="75b3d-154">Você pode substituí-lo para qualquer imagem que couber Olá [critérios de ícone](https://developer.chrome.com/apps/manifest/icons).</span><span class="sxs-lookup"><span data-stu-id="75b3d-154">You can substitute it for any image that fits hello [icon criteria](https://developer.chrome.com/apps/manifest/icons).</span></span>
4. <span data-ttu-id="75b3d-155">Crie um arquivo chamado `background.js` com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="75b3d-155">Create a file called `background.js` with hello following code:</span></span>
   
        // Returns a new notification ID used in hello notification.
        function getNotificationId() {
          var id = Math.floor(Math.random() * 9007199254740992) + 1;
          return id.toString();
        }
   
        function messageReceived(message) {
          // A message is an object with a data property that
          // consists of key-value pairs.
   
          // Concatenate all key-value pairs tooform a display string.
          var messageString = "";
          for (var key in message.data) {
            if (messageString != "")
              messageString += ", "
            messageString += key + ":" + message.data[key];
          }
          console.log("Message received: " + messageString);
   
          // Pop up a notification tooshow hello GCM message.
          chrome.notifications.create(getNotificationId(), {
            title: 'GCM Message',
            iconUrl: 'gcm_128.png',
            type: 'basic',
            message: messageString
          }, function() {});
        }
   
        var registerWindowCreated = false;
   
        function firstTimeRegistration() {
          chrome.storage.local.get("registered", function(result) {
   
            registerWindowCreated = true;
            chrome.app.window.create(
              "register.html",
              {  width: 520,
                 height: 500,
                 frame: 'chrome'
              },
              function(appWin) {}
            );
          });
        }
   
        // Set up a listener for GCM message event.
        chrome.gcm.onMessage.addListener(messageReceived);
   
        // Set up listeners tootrigger hello first-time registration.
        chrome.runtime.onInstalled.addListener(firstTimeRegistration);
        chrome.runtime.onStartup.addListener(firstTimeRegistration);
   
    <span data-ttu-id="75b3d-156">Este é o arquivo hello que aparecer a janela do aplicativo de cromo Olá HTML (**register.html**) e também define o manipulador de saudação **messageReceived** notificação toohandle Olá de entrada por push.</span><span class="sxs-lookup"><span data-stu-id="75b3d-156">This is hello file that pops up hello Chrome App window HTML (**register.html**) and also defines hello handler **messageReceived** toohandle hello incoming push notification.</span></span>
5. <span data-ttu-id="75b3d-157">Crie um arquivo chamado `register.html` -define Olá interface de usuário do hello aplicativo Chrome.</span><span class="sxs-lookup"><span data-stu-id="75b3d-157">Create a file called `register.html` - this defines hello UI of hello Chrome App.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="75b3d-158">Este exemplo usa **CryptoJS v3.1.2**.</span><span class="sxs-lookup"><span data-stu-id="75b3d-158">This sample uses **CryptoJS v3.1.2**.</span></span> <span data-ttu-id="75b3d-159">Se você baixou a outra versão da biblioteca de saudação, certifique-se de substituí-lo corretamente por versão Olá Olá `src` caminho.</span><span class="sxs-lookup"><span data-stu-id="75b3d-159">If you downloaded another version of hello library, make sure you properly substitute hello version in hello `src` path.</span></span>
   > 
   > 
   
        <html>
   
        <head>
        <title>GCM Registration</title>
        <script src="register.js"></script>
        <script src="CryptoJS v3.1.2/rollups/hmac-sha256.js"></script>
        <script src="CryptoJS v3.1.2/components/enc-base64-min.js"></script>
        </head>
   
        <body>
   
        Sender ID:<br/><input id="senderId" type="TEXT" size="20"><br/>
        <button id="registerWithGCM">Register with GCM</button>
        <br/>
        <br/>
        <br/>
   
        Notification Hub Name:<br/><input id="hubName" type="TEXT" style="width:400px"><br/><br/>
        Connection String:<br/><textarea id="connectionString" type="TEXT" style="width:400px;height:60px"></textarea>
   
        <br/>
   
        <button id="registerWithNH" disabled="true">Register with Azure Notification Hubs</button>
   
        <br/>
        <br/>
   
        <textarea id="console" type="TEXT" readonly style="width:500px;height:200px;background-color:#e5e5e5;padding:5px"></textarea>
   
        </body>
   
        </html>
6. <span data-ttu-id="75b3d-160">Crie um arquivo chamado `register.js` com código de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="75b3d-160">Create a file called `register.js` with hello code below.</span></span> <span data-ttu-id="75b3d-161">Esse arquivo Especifica o script hello atrás `register.html`.</span><span class="sxs-lookup"><span data-stu-id="75b3d-161">This file specifies hello script behind `register.html`.</span></span> <span data-ttu-id="75b3d-162">Chrome aplicativos não permitem execução embutida, permitindo toocreate um script de backup separado para a interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="75b3d-162">Chrome Apps do not allow inline execution, so you have toocreate a separate backing script for your UI.</span></span>
   
        var registrationId = "";
        var hubName        = "", connectionString = "";
        var originalUri    = "", targetUri = "", endpoint = "", sasKeyName = "", sasKeyValue = "", sasToken = "";
   
        window.onload = function() {
           document.getElementById("registerWithGCM").onclick = registerWithGCM;  
           document.getElementById("registerWithNH").onclick = registerWithNH;
           updateLog("You have not registered yet. Please provider sender ID and register with GCM and then with  Notification Hubs.");
        }
   
        function updateLog(status) {
          currentStatus = document.getElementById("console").innerHTML;
          if (currentStatus != "") {
            currentStatus = currentStatus + "\n\n";
          }
   
          document.getElementById("console").innerHTML = currentStatus  + status;
        }
   
        function registerWithGCM() {
          var senderId = document.getElementById("senderId").value.trim();
          chrome.gcm.register([senderId], registerCallback);
   
          // Prevent register button from being clicked again before hello registration finishes.
          document.getElementById("registerWithGCM").disabled = true;
        }
   
        function registerCallback(regId) {
          registrationId = regId;
          document.getElementById("registerWithGCM").disabled = false;
   
          if (chrome.runtime.lastError) {
            // When hello registration fails, handle hello error and retry the
            // registration later.
            updateLog("Registration failed: " + chrome.runtime.lastError.message);
            return;
          }
   
          updateLog("Registration with GCM succeeded.");
          document.getElementById("registerWithNH").disabled = false;
   
          // Mark that hello first-time registration is done.
          chrome.storage.local.set({registered: true});
        }
   
        function registerWithNH() {
          hubName = document.getElementById("hubName").value.trim();
          connectionString = document.getElementById("connectionString").value.trim();
          splitConnectionString();
          generateSaSToken();
          sendNHRegistrationRequest();
        }
   
        // From http://msdn.microsoft.com/library/dn495627.aspx
        function splitConnectionString()
        {
          var parts = connectionString.split(';');
          if (parts.length != 3)
          throw "Error parsing connection string";
   
          parts.forEach(function(part) {
            if (part.indexOf('Endpoint') == 0) {
            endpoint = 'https' + part.substring(11);
            } else if (part.indexOf('SharedAccessKeyName') == 0) {
            sasKeyName = part.substring(20);
            } else if (part.indexOf('SharedAccessKey') == 0) {
            sasKeyValue = part.substring(16);
            }
          });
   
          originalUri = endpoint + hubName;
        }
   
        function generateSaSToken()
        {
          targetUri = encodeURIComponent(originalUri.toLowerCase()).toLowerCase();
          var expiresInMins = 10; // 10 minute expiration
   
          // Set expiration in seconds.
          var expireOnDate = new Date();
          expireOnDate.setMinutes(expireOnDate.getMinutes() + expiresInMins);
          var expires = Date.UTC(expireOnDate.getUTCFullYear(), expireOnDate
            .getUTCMonth(), expireOnDate.getUTCDate(), expireOnDate
            .getUTCHours(), expireOnDate.getUTCMinutes(), expireOnDate
            .getUTCSeconds()) / 1000;
          var tosign = targetUri + '\n' + expires;
   
          // Using CryptoJS.
          var signature = CryptoJS.HmacSHA256(tosign, sasKeyValue);
          var base64signature = signature.toString(CryptoJS.enc.Base64);
          var base64UriEncoded = encodeURIComponent(base64signature);
   
          // Construct authorization string.
          sasToken = "SharedAccessSignature sr=" + targetUri + "&sig="
                          + base64UriEncoded + "&se=" + expires + "&skn=" + sasKeyName;
        }
   
        function sendNHRegistrationRequest()
        {
          var registrationPayload =
          "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
          "<entry xmlns=\"http://www.w3.org/2005/Atom\">" +
              "<content type=\"application/xml\">" +
                  "<GcmRegistrationDescription xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/netservices/2010/10/servicebus/connect\">" +
                      "<GcmRegistrationId>{GCMRegistrationId}</GcmRegistrationId>" +
                  "</GcmRegistrationDescription>" +
              "</content>" +
          "</entry>";
   
          // Update hello payload with hello registration ID obtained earlier.
          registrationPayload = registrationPayload.replace("{GCMRegistrationId}", registrationId);
   
          var url = originalUri + "/registrations/?api-version=2014-09";
          var client = new XMLHttpRequest();
   
          client.onload = function () {
            if (client.readyState == 4) {
              if (client.status == 200) {
                updateLog("Notification Hub Registration succesful!");
                updateLog(client.responseText);
              } else {
                updateLog("Notification Hub Registration did not succeed!");
                updateLog("HTTP Status: " + client.status + " : " + client.statusText);
                updateLog("HTTP Response: " + "\n" + client.responseText);
              }
            }
          };
   
          client.onerror = function () {
                updateLog("ERROR - Notification Hub Registration did not succeed!");
          }
   
          client.open("POST", url, true);
          client.setRequestHeader("Content-Type", "application/atom+xml;type=entry;charset=utf-8");
          client.setRequestHeader("Authorization", sasToken);
          client.setRequestHeader("x-ms-version", "2014-09");
   
          try {
              client.send(registrationPayload);
          }
          catch(err) {
              updateLog(err.message);
          }
        }
   
    <span data-ttu-id="75b3d-163">Olá acima script tem Olá parâmetros de chave a seguir:</span><span class="sxs-lookup"><span data-stu-id="75b3d-163">hello above script has hello following key parameters:</span></span>
   
   * <span data-ttu-id="75b3d-164">**OnLoad** define eventos de clique do botão Olá dos botões Olá dois Olá da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="75b3d-164">**window.onload** defines hello button-click events of hello two buttons on hello UI.</span></span> <span data-ttu-id="75b3d-165">Um registra GCM e Olá outros usa a ID de registro de saudação que é retornado após o registro com GCM tooregister com Hubs de notificação do Azure.</span><span class="sxs-lookup"><span data-stu-id="75b3d-165">One registers with GCM, and hello other uses hello registration ID that's returned after registration with GCM tooregister with Azure Notification Hubs.</span></span>
   * <span data-ttu-id="75b3d-166">**updateLog** é função hello que nos permite recursos de log simples de toohandle.</span><span class="sxs-lookup"><span data-stu-id="75b3d-166">**updateLog** is hello function that allows us toohandle simple logging capabilities.</span></span>
   * <span data-ttu-id="75b3d-167">**registerWithGCM** Olá primeiro clique do botão manipulador, que torna Olá `chrome.gcm.register` chamada tooGCM tooregister Olá atual aplicativo Chrome instância.</span><span class="sxs-lookup"><span data-stu-id="75b3d-167">**registerWithGCM** is hello first button-click handler, which makes hello `chrome.gcm.register` call tooGCM tooregister hello current Chrome App instance.</span></span>
   * <span data-ttu-id="75b3d-168">**registerCallback** é Olá função de retorno de chamada que é chamada quando a chamada de registro do GCM de hello retorna.</span><span class="sxs-lookup"><span data-stu-id="75b3d-168">**registerCallback** is hello callback function that gets called when hello GCM registration call returns.</span></span>
   * <span data-ttu-id="75b3d-169">**registerWithNH** Olá segundo clique do botão manipulador, que registra com Hubs de notificação.</span><span class="sxs-lookup"><span data-stu-id="75b3d-169">**registerWithNH** is hello second button-click handler, which registers with Notification Hubs.</span></span> <span data-ttu-id="75b3d-170">Ele obtém `hubName` e `connectionString` (especificou qual usuário Olá) e artesanatos Olá chamada à API de REST de registro de Hubs de notificação.</span><span class="sxs-lookup"><span data-stu-id="75b3d-170">It gets `hubName` and `connectionString` (which hello user has specified) and crafts hello Notification Hubs Registration REST API call.</span></span>
   * <span data-ttu-id="75b3d-171">**splitConnectionString** e **generateSaSToken** são auxiliares que representam a implementação de um processo de criação de token SaS, que deve ser usado em todas as chamadas da API REST JavaScript hello.</span><span class="sxs-lookup"><span data-stu-id="75b3d-171">**splitConnectionString** and **generateSaSToken** are helpers that represent hello JavaScript implementation of a SaS token creation process, that must be used in all REST API calls.</span></span> <span data-ttu-id="75b3d-172">Para saber mais, veja [Conceitos comuns](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="75b3d-172">For more information, see [Common Concepts](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
   * <span data-ttu-id="75b3d-173">**sendNHRegistrationRequest** é chamada de função de saudação que faz uma pausa de HTTP tooAzure Hubs de notificação.</span><span class="sxs-lookup"><span data-stu-id="75b3d-173">**sendNHRegistrationRequest** is hello function that makes a HTTP REST call tooAzure Notification Hubs.</span></span>
   * <span data-ttu-id="75b3d-174">**registrationPayload** define a carga XML de registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="75b3d-174">**registrationPayload** defines hello registration XML payload.</span></span> <span data-ttu-id="75b3d-175">Para obter mais informações, veja [Criar um registro da API REST NH].</span><span class="sxs-lookup"><span data-stu-id="75b3d-175">For more information, see [Create Registration NH REST API].</span></span> <span data-ttu-id="75b3d-176">Podemos atualizar ID do registro Olá nele com o que recebemos do GCM.</span><span class="sxs-lookup"><span data-stu-id="75b3d-176">We update hello registration ID in it with what we received from GCM.</span></span>
   * <span data-ttu-id="75b3d-177">**cliente** é uma instância de **XMLHttpRequest** que usamos solicitação de HTTP POST toomake hello.</span><span class="sxs-lookup"><span data-stu-id="75b3d-177">**client** is an instance of **XMLHttpRequest** that we use toomake hello HTTP POST request.</span></span> <span data-ttu-id="75b3d-178">Observe que podemos atualizar Olá `Authorization` cabeçalho com `sasToken`.</span><span class="sxs-lookup"><span data-stu-id="75b3d-178">Note that we update hello `Authorization` header with `sasToken`.</span></span> <span data-ttu-id="75b3d-179">A conclusão bem-sucedida dessa chamada registrará essa instância do aplicativo Chrome com os Hubs de notificação do Azure.</span><span class="sxs-lookup"><span data-stu-id="75b3d-179">Successful completion of this call will register this Chrome App instance with Azure Notification Hubs.</span></span>

<span data-ttu-id="75b3d-180">Olá geral estrutura de pasta para este projeto deve ser semelhante a esta: ![Google Chrome aplicativo - estrutura de pasta][21]</span><span class="sxs-lookup"><span data-stu-id="75b3d-180">hello overall folder structure for this project should resemble this: ![Google Chrome App - Folder Structure][21]</span></span>

### <a name="set-up-and-test-your-chrome-app"></a><span data-ttu-id="75b3d-181">Configurar e testar seu Aplicativo Chrome</span><span class="sxs-lookup"><span data-stu-id="75b3d-181">Set up and test your Chrome App</span></span>
1. <span data-ttu-id="75b3d-182">Abra seu navegador Chrome.</span><span class="sxs-lookup"><span data-stu-id="75b3d-182">Open your Chrome browser.</span></span> <span data-ttu-id="75b3d-183">Abra as **extensões do Chrome** e habilite o **Modo de desenvolvedor**.</span><span class="sxs-lookup"><span data-stu-id="75b3d-183">Open **Chrome extensions** and enable **Developer mode**.</span></span>
   
       ![Google Chrome - Enable Developer Mode][16]
2. <span data-ttu-id="75b3d-184">Clique em **carregar a extensão desempacotado** e navegue toohello pasta em que você criou arquivos hello.</span><span class="sxs-lookup"><span data-stu-id="75b3d-184">Click **Load unpacked extension** and navigate toohello folder where you created hello files.</span></span> <span data-ttu-id="75b3d-185">Você também pode usar o hello **aplicativos Chrome & ferramenta de desenvolvimento de extensões**.</span><span class="sxs-lookup"><span data-stu-id="75b3d-185">You can also optionally use hello **Chrome Apps & Extensions Developer Tool**.</span></span> <span data-ttu-id="75b3d-186">Essa ferramenta é um aplicativo de cromo em si (instalado da saudação cromo da Web repositório) e fornece recursos avançados de depuração para o desenvolvimento de aplicativos do Chrome.</span><span class="sxs-lookup"><span data-stu-id="75b3d-186">This tool is a Chrome App in itself (installed from hello Chrome Web Store) and provides advanced debugging capabilities for your Chrome App development.</span></span>
   
       ![Google Chrome - Load Unpacked Extension][17]
3. <span data-ttu-id="75b3d-187">Se Olá Chrome aplicativo é criado sem erros, em seguida, você verá seu aplicativo Chrome aparecem.</span><span class="sxs-lookup"><span data-stu-id="75b3d-187">If hello Chrome App is created without any errors, then you will see your Chrome App show up.</span></span>
   
       ![Google Chrome - Chrome App Display][18]
4. <span data-ttu-id="75b3d-188">Digite hello **projeto número** que você obteve anteriormente Olá **Google nuvem Console** como ID do remetente hello e clique em **registrar com GCM**.</span><span class="sxs-lookup"><span data-stu-id="75b3d-188">Enter hello **Project Number** that you got earlier from hello **Google Cloud Console** as hello sender ID, and click **Register with GCM**.</span></span> <span data-ttu-id="75b3d-189">Você deve ver uma mensagem de saudação **registro com êxito do GCM.**</span><span class="sxs-lookup"><span data-stu-id="75b3d-189">You must see hello message **Registration with GCM succeeded.**</span></span>
   
       ![Google Chrome - Chrome App Customization][19]
5. <span data-ttu-id="75b3d-190">Insira seu **nome do Hub de notificação** e hello **DefaultListenSharedAccessSignature** que você obteve no portal de saudação anteriormente e clique em **registrar com o Hub de notificação do Azure**.</span><span class="sxs-lookup"><span data-stu-id="75b3d-190">Enter your **Notification Hub Name** and hello **DefaultListenSharedAccessSignature** that you obtained from hello portal earlier, and click **Register with Azure Notification Hub**.</span></span> <span data-ttu-id="75b3d-191">Você deve ver uma mensagem de saudação **registro do Hub de notificação com êxito!**</span><span class="sxs-lookup"><span data-stu-id="75b3d-191">You must see hello message **Notification Hub Registration successful!**</span></span> <span data-ttu-id="75b3d-192">e a ID de detalhes de saudação da resposta de registro hello, que contém Olá registro de Hubs de notificação do Azure.</span><span class="sxs-lookup"><span data-stu-id="75b3d-192">and hello details of hello registration response, which contains hello Azure Notification Hubs registration ID.</span></span>
   
       ![Google Chrome - Specify Notification Hub Details][20]  

## <span data-ttu-id="75b3d-193"><a name="send"></a>Enviar uma notificação tooyour aplicativo Chrome</span><span class="sxs-lookup"><span data-stu-id="75b3d-193"><a name="send"></a>Send a notification tooyour Chrome App</span></span>
<span data-ttu-id="75b3d-194">Para fins de teste, enviaremos notificações por push do Chrome usando um aplicativo de console .NET.</span><span class="sxs-lookup"><span data-stu-id="75b3d-194">For testing purposes, we will send Chrome push notifications by using a .NET console application.</span></span> 

> [!NOTE]
> <span data-ttu-id="75b3d-195">Você pode enviar notificações por push com os Hubs de Notificação de qualquer back-end por meio da nossa <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">interface REST</a> pública.</span><span class="sxs-lookup"><span data-stu-id="75b3d-195">You can send push notifications with Notification Hubs from any backend via our public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="75b3d-196">Confira nosso [portal de documentação](https://azure.microsoft.com/documentation/services/notification-hubs/) para obter mais exemplos de plataforma cruzada.</span><span class="sxs-lookup"><span data-stu-id="75b3d-196">Check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/) for more cross-platform examples.</span></span>
> 
> 

1. <span data-ttu-id="75b3d-197">No Visual Studio, de saudação **arquivo** menu, selecione **novo** e **projeto**.</span><span class="sxs-lookup"><span data-stu-id="75b3d-197">In Visual Studio, from hello **File** menu, select **New** and then **Project**.</span></span> <span data-ttu-id="75b3d-198">No **Visual C#**, clique em **Windows** e em **Aplicativo do Console** e depois clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="75b3d-198">Under **Visual C#**, click **Windows** and **Console Application**, and then click **OK**.</span></span>  <span data-ttu-id="75b3d-199">Isso cria um novo projeto de aplicativo de console.</span><span class="sxs-lookup"><span data-stu-id="75b3d-199">This creates a new console application project.</span></span>
2. <span data-ttu-id="75b3d-200">De saudação **ferramentas** menu, clique em **Gerenciador de biblioteca de pacote** e **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="75b3d-200">From hello **Tools** menu, click **Library Package Manager** and then **Package Manager Console**.</span></span> <span data-ttu-id="75b3d-201">Isso exibe o saudação Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="75b3d-201">This displays hello Package Manager Console.</span></span>
3. <span data-ttu-id="75b3d-202">Na janela de console hello, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="75b3d-202">In hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
       This adds a reference toohello Azure Service Bus SDK with hello <a href="http://nuget.org/packages/  WindowsAzure.ServiceBus/">WindowsAzure.ServiceBus NuGet package</a>.
4. <span data-ttu-id="75b3d-203">Abra `Program.cs` e adicione o seguinte Olá `using` instrução:</span><span class="sxs-lookup"><span data-stu-id="75b3d-203">Open `Program.cs` and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="75b3d-204">Em Olá `Program` classe, adicione o seguinte método de saudação:</span><span class="sxs-lookup"><span data-stu-id="75b3d-204">In hello `Program` class, add hello following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            String message = "{\"data\":{\"message\":\"Hello Chrome from Azure Notification Hubs\"}}";
            await hub.SendGcmNativeNotificationAsync(message);
        }
   
       Make sure tooreplace hello `<hub name>` placeholder with hello name of hello notification hub that appears in hello [portal](https://portal.azure.com) in your Notification Hub blade. Also, replace hello connection string placeholder with hello connection string called `DefaultFullSharedAccessSignature` that you obtained in hello notification hub configuration section.
   
   > [!NOTE]
   > <span data-ttu-id="75b3d-205">Certifique-se de que você use a cadeia de caracteres de conexão de saudação com **completo** acessar, não **escutar** acesso.</span><span class="sxs-lookup"><span data-stu-id="75b3d-205">Make sure that you use hello connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="75b3d-206">Olá **escutar** cadeia de caracteres de conexão de acesso não concede permissões toosend notificações de envio.</span><span class="sxs-lookup"><span data-stu-id="75b3d-206">hello **Listen** access connection string does not grant permissions toosend push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="75b3d-207">Adicione a seguinte Olá chamadas em Olá `Main` método:</span><span class="sxs-lookup"><span data-stu-id="75b3d-207">Add hello following calls in hello `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="75b3d-208">Certifique-se de que está executando o Chrome e executar o aplicativo de console hello.</span><span class="sxs-lookup"><span data-stu-id="75b3d-208">Make sure that Chrome is running, and run hello console application.</span></span>
8. <span data-ttu-id="75b3d-209">Você deve ver Olá seguinte notificação pop-up na área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="75b3d-209">You should see hello following notification pop up on your desktop.</span></span>
   
       ![Google Chrome - Notification][13]
9. <span data-ttu-id="75b3d-210">Você também pode ver todas as notificações, usando a janela de cromo notificações de saudação na barra de tarefas da saudação (no Windows) quando o Chrome está em execução.</span><span class="sxs-lookup"><span data-stu-id="75b3d-210">You can also see all your notifications by using hello Chrome Notifications window in hello taskbar (in Windows) when Chrome is running.</span></span>
   
       ![Google Chrome - Notifications List][14]

> [!NOTE]
> <span data-ttu-id="75b3d-211">Você não precisa toohave Olá Chrome aplicativo em execução ou aberto no navegador de saudação (embora o próprio navegador de cromo Olá deve estar em execução).</span><span class="sxs-lookup"><span data-stu-id="75b3d-211">You don't need toohave hello Chrome App running or open in hello browser (though hello Chrome browser itself must be running).</span></span> <span data-ttu-id="75b3d-212">Você também pode obter uma visão consolidada de todas as notificações na janela de notificações de cromo hello.</span><span class="sxs-lookup"><span data-stu-id="75b3d-212">You also get a consolidated view of all your notifications in hello Chrome Notifications window.</span></span>
> 
> 

## <span data-ttu-id="75b3d-213"><a name="next-steps"> </a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="75b3d-213"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="75b3d-214">Saiba mais sobre os Hubs de Notificação em [Visão geral dos Hubs de Notificação].</span><span class="sxs-lookup"><span data-stu-id="75b3d-214">Learn more about Notification Hubs in [Notification Hubs Overview].</span></span>

<span data-ttu-id="75b3d-215">tootarget de usuários específicos, consulte toohello [notificar usuários de Hubs de notificação do Azure] tutorial.</span><span class="sxs-lookup"><span data-stu-id="75b3d-215">tootarget specific users, refer toohello [Azure Notification Hubs Notify Users] tutorial.</span></span> 

<span data-ttu-id="75b3d-216">Se você quiser toosegment os usuários, grupos de interesse, você pode seguir Olá [Hubs de notificação do Azure últimas notícias] tutorial.</span><span class="sxs-lookup"><span data-stu-id="75b3d-216">If you want toosegment your users by interest groups, you can follow hello [Azure Notification Hubs breaking news] tutorial.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-chrome-get-started/GoogleConsoleCreateProject.PNG
[2]: ./media/notification-hubs-chrome-get-started/GoogleProjectNumber.png
[3]: ./media/notification-hubs-chrome-get-started/EnableGCM.png
[4]: ./media/notification-hubs-chrome-get-started/CreateServerKey.png
[5]: ./media/notification-hubs-chrome-get-started/ServerKey.png
[6]: ./media/notification-hubs-chrome-get-started/CreateNH.png
[7]: ./media/notification-hubs-chrome-get-started/NHNamespace.png
[8]: ./media/notification-hubs-chrome-get-started/NamespaceConfigure.png
[9]: ./media/notification-hubs-chrome-get-started/NHConfigure.png
[10]: ./media/notification-hubs-chrome-get-started/NHConfigureGCM.png
[11]: ./media/notification-hubs-chrome-get-started/NHDashboard.png
[12]: ./media/notification-hubs-chrome-get-started/NHConnString.png
[13]: ./media/notification-hubs-chrome-get-started/ChromeNotification.png
[14]: ./media/notification-hubs-chrome-get-started/ChromeNotificationWindow.png
[15]: ./media/notification-hubs-chrome-get-started/ChromeApp.png
[16]: ./media/notification-hubs-chrome-get-started/ChromeExtensions.png
[17]: ./media/notification-hubs-chrome-get-started/ChromeLoadExtension.png
[18]: ./media/notification-hubs-chrome-get-started/ChromeAppLoaded.png
[19]: ./media/notification-hubs-chrome-get-started/ChromeAppGCM.png
[20]: ./media/notification-hubs-chrome-get-started/ChromeAppNH.png
[21]: ./media/notification-hubs-chrome-get-started/FinalFolderView.png

<!-- URLs. -->
[exemplo de Hub de notificação de aplicativo Chrome]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToChromeApps
[Google nuvem Console]: http://cloud.google.com/console
[Azure Classic Portal]: https://manage.windowsazure.com/
[Visão geral dos Hubs de Notificação]: notification-hubs-push-notification-overview.md
[visão geral de aplicativos do Chrome]: https://developer.chrome.com/apps/about_apps
[Chrome aplicativo GCM exemplo]: https://github.com/GoogleChrome/chrome-app-samples/tree/master/samples/gcm-notifications
[Installable Web Apps]: https://developers.google.com/chrome/apps/docs/
[Chrome aplicativos móveis]: https://developer.chrome.com/apps/chrome_apps_on_mobile
[Criar um registro da API REST NH]: http://msdn.microsoft.com/library/azure/dn223265.aspx
[biblioteca de criptografia js]: http://code.google.com/p/crypto-js/
[GCM with Chrome Apps]: https://developer.chrome.com/apps/cloudMessaging
[Google Cloud Messaging cromo]: https://developer.chrome.com/apps/cloudMessagingV1
[notificar usuários de Hubs de notificação do Azure]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Hubs de notificação do Azure últimas notícias]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
