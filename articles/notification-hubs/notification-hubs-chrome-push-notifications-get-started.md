---
title: "Enviar notificações por push para aplicativos Chrome com os Hubs de Notificação do Azure | Microsoft Docs"
description: "Saiba como usar os Hubs de Notificação do Azure para enviar notificações por push para um Aplicativo Chrome."
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
ms.openlocfilehash: 600b1b7e5f3987c9a0acc33b7049f7118442b931
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="send-push-notifications-to-chrome-apps-with-azure-notification-hubs"></a><span data-ttu-id="9037c-104">Enviar notificações por push para aplicativos Chrome com os Hubs de Notificação do Azure</span><span class="sxs-lookup"><span data-stu-id="9037c-104">Send push notifications to Chrome apps with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

<span data-ttu-id="9037c-105">Este tópico mostra como usar os Hubs de Notificação do Azure para enviar notificações por push para um Aplicativo Chrome, que será exibido dentro do contexto do navegador Google Chrome.</span><span class="sxs-lookup"><span data-stu-id="9037c-105">This topic shows you how to use Azure Notification Hubs to send push notifications to a Chrome App, which will be displayed within the context of the Google Chrome browser.</span></span> <span data-ttu-id="9037c-106">Neste tutorial, criaremos um Aplicativo Chrome que recebe notificações por push usando o [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/).</span><span class="sxs-lookup"><span data-stu-id="9037c-106">In this tutorial, we will create a Chrome app that receives push notifications by using [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/).</span></span> 

> [!NOTE]
> <span data-ttu-id="9037c-107">Para concluir este tutorial, você precisa ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="9037c-107">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="9037c-108">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="9037c-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="9037c-109">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="9037c-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="9037c-110">O tutorial explica as seguintes etapas básicas para habilitar as notificações por push:</span><span class="sxs-lookup"><span data-stu-id="9037c-110">The tutorial walks you through these basic steps to enable push notifications:</span></span>

* [<span data-ttu-id="9037c-111">Habilitar as mensagens em nuvem do Google</span><span class="sxs-lookup"><span data-stu-id="9037c-111">Enable Google Cloud Messaging</span></span>](#register)
* [<span data-ttu-id="9037c-112">Configurar seu Hub de Notificação</span><span class="sxs-lookup"><span data-stu-id="9037c-112">Configure your notification hub</span></span>](#configure-hub)
* [<span data-ttu-id="9037c-113">Conectar seu Aplicativo Chrome ao hub de notificação</span><span class="sxs-lookup"><span data-stu-id="9037c-113">Connect your Chrome App to the notification hub</span></span>](#connect-app)
* [<span data-ttu-id="9037c-114">Enviar uma notificação por push para seu Aplicativo Chrome</span><span class="sxs-lookup"><span data-stu-id="9037c-114">Send a push notification to your Chrome App</span></span>](#send)
* [<span data-ttu-id="9037c-115">Funcionalidade e recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9037c-115">Additional functionality & capabilities</span></span>](#next-steps)

> [!NOTE]
> <span data-ttu-id="9037c-116">As notificações por push do aplicativo Chrome não são notificações genéricas do navegador - elas são específicas do modelo de extensibilidade do navegador (veja [Visão geral de aplicativos Chrome] para obter detalhes).</span><span class="sxs-lookup"><span data-stu-id="9037c-116">Chrome app push notifications are not generic in-browser notifications - they are specific to the browser extensibility model (see [Chrome Apps Overview] for details).</span></span> <span data-ttu-id="9037c-117">Além do navegador da área de trabalho, os aplicativos Chrome são executados em celulares (Android e iOS) por meio do Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="9037c-117">In addition to the desktop browser, Chrome apps run on mobile (Android and iOS) through Apache Cordova.</span></span> <span data-ttu-id="9037c-118">Consulte [Aplicativos do Chrome em Dispositivos móveis] para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="9037c-118">See [Chrome Apps on Mobile] to learn more.</span></span>
> 
> 

<span data-ttu-id="9037c-119">A configuração do GCM e dos Hubs de Notificação do Azure é idêntica à configuração para o Android, já que o [Google Cloud Messaging para Chrome] foi substituído e o mesmo GCM agora dá suporte a dispositivos Android e a instâncias do Chrome.</span><span class="sxs-lookup"><span data-stu-id="9037c-119">Configuring GCM and Azure Notification Hubs is identical to configuring for Android, since [Google Cloud Messaging for Chrome] has been deprecated and the same GCM now supports both Android devices and Chrome instances.</span></span>

## <span data-ttu-id="9037c-120"><a id="register"></a>Habilitar as mensagens em nuvem do Google</span><span class="sxs-lookup"><span data-stu-id="9037c-120"><a id="register"></a>Enable Google Cloud Messaging</span></span>
1. <span data-ttu-id="9037c-121">Navegue até o site [Console do Google Cloud] , conecte-se com as credenciais de sua conta do Google e clique no botão **Criar Projeto** .</span><span class="sxs-lookup"><span data-stu-id="9037c-121">Navigate to the [Google Cloud Console] website, sign in with your Google account credentials, and then click the **Create Project** button.</span></span> <span data-ttu-id="9037c-122">Forneça um **Nome de Projeto** apropriado e clique no botão **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9037c-122">Provide an appropriate **Project Name**, and then click the **Create** button.</span></span>
   
       ![Google Cloud Console - Create Project][1]
2. <span data-ttu-id="9037c-123">Anote o **Número do Projeto** na página **Projetos** do projeto que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="9037c-123">Make a note of the **Project Number** on the **Projects** page for the project that you just created.</span></span> <span data-ttu-id="9037c-124">Você o usará como a **ID de Remetente do GCM** no Aplicativo Chrome para se registrar no GCM.</span><span class="sxs-lookup"><span data-stu-id="9037c-124">You will use this as the **GCM Sender ID** in the Chrome App to register with GCM.</span></span>
   
       ![Google Cloud Console - Project Number][2]
3. <span data-ttu-id="9037c-125">No painel à esquerda, clique em **APIs e autorização**, role para baixo e clique no botão de alternância para habilitar o **Google Cloud Messaging para Android**.</span><span class="sxs-lookup"><span data-stu-id="9037c-125">In the left pane, click **APIs & auth**, and then scroll down and click the toggle to enable **Google Cloud Messaging for Android**.</span></span> <span data-ttu-id="9037c-126">Você não precisa habilitar o **Google Cloud Messaging para Chrome**.</span><span class="sxs-lookup"><span data-stu-id="9037c-126">You don't have to enable **Google Cloud Messaging for Chrome**.</span></span>
   
       ![Google Cloud Console - Server Key][3]
4. <span data-ttu-id="9037c-127">No painel esquerdo, clique em **Credenciais** > **Criar Nova Chave** > **Chave do Servidor** > **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9037c-127">In the left pane, click **Credentials** > **Create New Key** > **Server Key** > **Create**.</span></span>
   
       ![Google Cloud Console - Credentials][4]
5. <span data-ttu-id="9037c-128">Anote a **Chave de API**do servidor.</span><span class="sxs-lookup"><span data-stu-id="9037c-128">Make a note of the server **API Key**.</span></span> <span data-ttu-id="9037c-129">Em seguida, você a configurará em seu hub de notificação para habilitá-lo a enviar notificações por push para o GCM.</span><span class="sxs-lookup"><span data-stu-id="9037c-129">You will configure this in your notification hub next, to enable it to send push notifications to GCM.</span></span>
   
       ![Google Cloud Console - API Key][5]

## <span data-ttu-id="9037c-130"><a id="configure-hub"></a>Configurar seu Hub de Notificação</span><span class="sxs-lookup"><span data-stu-id="9037c-130"><a id="configure-hub"></a>Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="9037c-131">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="9037c-131">&emsp;&emsp;6.</span></span>   <span data-ttu-id="9037c-132">Na folha **Configurações**, selecione **Serviços de Notificação** e **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="9037c-132">In the **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="9037c-133">Insira a chave de API e salve.</span><span class="sxs-lookup"><span data-stu-id="9037c-133">Enter the API key and save.</span></span>

&emsp;&emsp;![Hubs de Notificação do Azure - Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

## <span data-ttu-id="9037c-135"><a id="connect-app"></a>Conectar seu Aplicativo Chrome ao hub de notificação</span><span class="sxs-lookup"><span data-stu-id="9037c-135"><a id="connect-app"></a>Connect your Chrome App to the notification hub</span></span>
<span data-ttu-id="9037c-136">Agora, o hub de notificação está configurado para funcionar com o GCM, e você tem as cadeias de conexão para registrar seu aplicativo para receber e enviar notificações por push.</span><span class="sxs-lookup"><span data-stu-id="9037c-136">Your notification hub is now configured to work with GCM, and you have the connection strings to register your app to both receive and send push notifications.</span></span> <span data-ttu-id="9037c-137">LK</span><span class="sxs-lookup"><span data-stu-id="9037c-137">LK</span></span>

### <a name="create-a-new-chrome-app"></a><span data-ttu-id="9037c-138">Criar um novo Aplicativo Chrome</span><span class="sxs-lookup"><span data-stu-id="9037c-138">Create a new Chrome App</span></span>
<span data-ttu-id="9037c-139">O exemplo a seguir é baseado no [Exemplo do GCM do Aplicativo Chrome] e usa a maneira recomendada para criar um Aplicativo Chrome.</span><span class="sxs-lookup"><span data-stu-id="9037c-139">The sample below is based on the [Chrome App GCM Sample] and uses the recommended way to create a Chrome App.</span></span> <span data-ttu-id="9037c-140">Nós destacaremos as etapas relacionadas especificamente aos Hubs de Notificação do Azure.</span><span class="sxs-lookup"><span data-stu-id="9037c-140">We will highlight the steps specifically related to Azure Notification Hubs.</span></span> 

> [!NOTE]
> <span data-ttu-id="9037c-141">Recomendamos que você baixe a fonte deste Aplicativo Chrome do [Exemplo de Hub de Notificação do Aplicativo Chrome].</span><span class="sxs-lookup"><span data-stu-id="9037c-141">We recommend that you download the source for this Chrome App from [Chrome App Notification Hub Sample].</span></span>
> 
> 

<span data-ttu-id="9037c-142">O Aplicativo Chrome é criado por meio do JavaScript, e você pode usar um de seus editores de texto preferidos para criá-lo.</span><span class="sxs-lookup"><span data-stu-id="9037c-142">The Chrome App is created via JavaScript, and you can use any of your preferred word editors for creating it.</span></span> <span data-ttu-id="9037c-143">Abaixo, esta é a aparência desse aplicativo Chrome.</span><span class="sxs-lookup"><span data-stu-id="9037c-143">Below is what this Chrome App will look like.</span></span>

![Aplicativo Google Chrome][15]

1. <span data-ttu-id="9037c-145">Crie uma pasta e chame-a de `ChromePushApp`.</span><span class="sxs-lookup"><span data-stu-id="9037c-145">Create a folder and name it `ChromePushApp`.</span></span> <span data-ttu-id="9037c-146">Obviamente, o nome é arbitrário - se você chamá-la de algo diferente, substitua o caminho nos segmentos de código necessários.</span><span class="sxs-lookup"><span data-stu-id="9037c-146">Of course, the name is arbitrary - if you name it something different, make sure you substitute the path in the required code segments.</span></span>
2. <span data-ttu-id="9037c-147">Baixe a [biblioteca crypto-js] na pasta criada na segunda etapa.</span><span class="sxs-lookup"><span data-stu-id="9037c-147">Download the [crypto-js library] in the folder you created in the second step.</span></span> <span data-ttu-id="9037c-148">Essa pasta de biblioteca contém duas subpastas: `components` e `rollups`.</span><span class="sxs-lookup"><span data-stu-id="9037c-148">This library folder will contain two subfolders: `components` and `rollups`.</span></span>
3. <span data-ttu-id="9037c-149">Crie um arquivo do `manifest.json` .</span><span class="sxs-lookup"><span data-stu-id="9037c-149">Create a `manifest.json` file.</span></span> <span data-ttu-id="9037c-150">Todos os Aplicativos Chrome são apoiados por um arquivo de manifesto que contém os metadados do aplicativo e, mais importante, todas as permissões concedidas ao aplicativo quando o usuário o instala.</span><span class="sxs-lookup"><span data-stu-id="9037c-150">All Chrome Apps are backed by a manifest file that contains the app metadata and, most importantly, all permissions that are granted to the app when the user installs it.</span></span>
   
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
   
    <span data-ttu-id="9037c-151">Observe o elemento `permissions` , que especifica que esse Aplicativo Chrome poderá receber notificações por push do GCM.</span><span class="sxs-lookup"><span data-stu-id="9037c-151">Notice the `permissions` element, which specifies that this Chrome App will be able to receive push notifications from GCM.</span></span> <span data-ttu-id="9037c-152">Ele também deve especificar o URI dos Hubs de Notificação do Azure nos quais o Aplicativo Chrome fará uma chamada REST para o registro.</span><span class="sxs-lookup"><span data-stu-id="9037c-152">It must also specify the Azure Notification Hubs URI where the Chrome App will make a REST call to register.</span></span>
    <span data-ttu-id="9037c-153">Nosso aplicativo de exemplo também usa um arquivo de ícone, `gcm_128.png`, que você encontrará na fonte reutilizada por meio do exemplo original do GCM.</span><span class="sxs-lookup"><span data-stu-id="9037c-153">Our sample app also uses an icon file, `gcm_128.png`, that you will find at the source that's reused from the original GCM sample.</span></span> <span data-ttu-id="9037c-154">Você poderá substituí-lo por qualquer imagem que se ajuste a [critérios de ícone](https://developer.chrome.com/apps/manifest/icons).</span><span class="sxs-lookup"><span data-stu-id="9037c-154">You can substitute it for any image that fits the [icon criteria](https://developer.chrome.com/apps/manifest/icons).</span></span>
4. <span data-ttu-id="9037c-155">Crie um arquivo chamado `background.js` com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="9037c-155">Create a file called `background.js` with the following code:</span></span>
   
        // Returns a new notification ID used in the notification.
        function getNotificationId() {
          var id = Math.floor(Math.random() * 9007199254740992) + 1;
          return id.toString();
        }
   
        function messageReceived(message) {
          // A message is an object with a data property that
          // consists of key-value pairs.
   
          // Concatenate all key-value pairs to form a display string.
          var messageString = "";
          for (var key in message.data) {
            if (messageString != "")
              messageString += ", "
            messageString += key + ":" + message.data[key];
          }
          console.log("Message received: " + messageString);
   
          // Pop up a notification to show the GCM message.
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
   
        // Set up listeners to trigger the first-time registration.
        chrome.runtime.onInstalled.addListener(firstTimeRegistration);
        chrome.runtime.onStartup.addListener(firstTimeRegistration);
   
    <span data-ttu-id="9037c-156">Este é o arquivo que abre o HTML da janela do Aplicativo Chrome (**register.html**) e também define o manipulador **messageReceived** para manipular a notificação por push recebida.</span><span class="sxs-lookup"><span data-stu-id="9037c-156">This is the file that pops up the Chrome App window HTML (**register.html**) and also defines the handler **messageReceived** to handle the incoming push notification.</span></span>
5. <span data-ttu-id="9037c-157">Crie um arquivo chamado `register.html` - isso define a interface do usuário do Aplicativo Chrome.</span><span class="sxs-lookup"><span data-stu-id="9037c-157">Create a file called `register.html` - this defines the UI of the Chrome App.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="9037c-158">Este exemplo usa **CryptoJS v3.1.2**.</span><span class="sxs-lookup"><span data-stu-id="9037c-158">This sample uses **CryptoJS v3.1.2**.</span></span> <span data-ttu-id="9037c-159">Se você tiver baixado outra versão da biblioteca, verifique se você substituiu corretamente a versão no caminho do `src` .</span><span class="sxs-lookup"><span data-stu-id="9037c-159">If you downloaded another version of the library, make sure you properly substitute the version in the `src` path.</span></span>
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
6. <span data-ttu-id="9037c-160">Crie um arquivo chamado `register.js` com o código abaixo.</span><span class="sxs-lookup"><span data-stu-id="9037c-160">Create a file called `register.js` with the code below.</span></span> <span data-ttu-id="9037c-161">Esse arquivo especifica o script por trás de `register.html`.</span><span class="sxs-lookup"><span data-stu-id="9037c-161">This file specifies the script behind `register.html`.</span></span> <span data-ttu-id="9037c-162">Os Aplicativos Chrome não permitem a execução embutida, por isso é necessário criar um script de backup separado para a sua interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="9037c-162">Chrome Apps do not allow inline execution, so you have to create a separate backing script for your UI.</span></span>
   
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
   
          // Prevent register button from being clicked again before the registration finishes.
          document.getElementById("registerWithGCM").disabled = true;
        }
   
        function registerCallback(regId) {
          registrationId = regId;
          document.getElementById("registerWithGCM").disabled = false;
   
          if (chrome.runtime.lastError) {
            // When the registration fails, handle the error and retry the
            // registration later.
            updateLog("Registration failed: " + chrome.runtime.lastError.message);
            return;
          }
   
          updateLog("Registration with GCM succeeded.");
          document.getElementById("registerWithNH").disabled = false;
   
          // Mark that the first-time registration is done.
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
   
          // Update the payload with the registration ID obtained earlier.
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
   
    <span data-ttu-id="9037c-163">O script acima tem os seguintes argumentos principais:</span><span class="sxs-lookup"><span data-stu-id="9037c-163">The above script has the following key parameters:</span></span>
   
   * <span data-ttu-id="9037c-164">**window.onload** define os eventos de clique de botão dos dois botões na interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="9037c-164">**window.onload** defines the button-click events of the two buttons on the UI.</span></span> <span data-ttu-id="9037c-165">Um realiza o registro com o GCM e o outro usa a ID de registro retornada após o registro com o GCM para fazer o registro nos Hubs de Notificação do Azure.</span><span class="sxs-lookup"><span data-stu-id="9037c-165">One registers with GCM, and the other uses the registration ID that's returned after registration with GCM to register with Azure Notification Hubs.</span></span>
   * <span data-ttu-id="9037c-166">**updateLog** é a função que permite manipular recursos de log simples.</span><span class="sxs-lookup"><span data-stu-id="9037c-166">**updateLog** is the function that allows us to handle simple logging capabilities.</span></span>
   * <span data-ttu-id="9037c-167">**registerWithGCM** é o primeiro manipulador de clique de botão, que faz a chamada `chrome.gcm.register` para o GCM para registrar essa instância do Aplicativo Chrome.</span><span class="sxs-lookup"><span data-stu-id="9037c-167">**registerWithGCM** is the first button-click handler, which makes the `chrome.gcm.register` call to GCM to register the current Chrome App instance.</span></span>
   * <span data-ttu-id="9037c-168">**registerCallback** é a função de retorno de chamada que é chamada quando a chamada de registro do GCM acima é retornada.</span><span class="sxs-lookup"><span data-stu-id="9037c-168">**registerCallback** is the callback function that gets called when the GCM registration call returns.</span></span>
   * <span data-ttu-id="9037c-169">**registerWithNH** é o segundo manipulador de clique de botão, que faz o registro nos Hubs de Notificação.</span><span class="sxs-lookup"><span data-stu-id="9037c-169">**registerWithNH** is the second button-click handler, which registers with Notification Hubs.</span></span> <span data-ttu-id="9037c-170">Obtém `hubName` e `connectionString` (que o usuário especificou) e cria a chamada da API REST de Registro de Hubs de Notificação.</span><span class="sxs-lookup"><span data-stu-id="9037c-170">It gets `hubName` and `connectionString` (which the user has specified) and crafts the Notification Hubs Registration REST API call.</span></span>
   * <span data-ttu-id="9037c-171">**splitConnectionString** e **generateSaSToken** são os auxiliares que representam a implementação de JavaScript da criação de um token SaS que deve ser enviado em todas as chamadas da API REST.</span><span class="sxs-lookup"><span data-stu-id="9037c-171">**splitConnectionString** and **generateSaSToken** are helpers that represent the JavaScript implementation of a SaS token creation process, that must be used in all REST API calls.</span></span> <span data-ttu-id="9037c-172">Para saber mais, veja [Conceitos comuns](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="9037c-172">For more information, see [Common Concepts](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
   * <span data-ttu-id="9037c-173">**sendNHRegistrationRequest** é a função que faz uma chamada HTTP REST para os Hubs de Notificação do Azure.</span><span class="sxs-lookup"><span data-stu-id="9037c-173">**sendNHRegistrationRequest** is the function that makes a HTTP REST call to Azure Notification Hubs.</span></span>
   * <span data-ttu-id="9037c-174">**registrationPayload** define a carga XML do registro.</span><span class="sxs-lookup"><span data-stu-id="9037c-174">**registrationPayload** defines the registration XML payload.</span></span> <span data-ttu-id="9037c-175">Para obter mais informações, veja [Criar um registro da API REST NH].</span><span class="sxs-lookup"><span data-stu-id="9037c-175">For more information, see [Create Registration NH REST API].</span></span> <span data-ttu-id="9037c-176">Atualizamos a ID do registro com o que recebemos do GCM.</span><span class="sxs-lookup"><span data-stu-id="9037c-176">We update the registration ID in it with what we received from GCM.</span></span>
   * <span data-ttu-id="9037c-177">**client** é uma instância de **XMLHttpRequest** usada para fazer a solicitação HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="9037c-177">**client** is an instance of **XMLHttpRequest** that we use to make the HTTP POST request.</span></span> <span data-ttu-id="9037c-178">Observe que atualizamos o cabeçalho `Authorization` com `sasToken`.</span><span class="sxs-lookup"><span data-stu-id="9037c-178">Note that we update the `Authorization` header with `sasToken`.</span></span> <span data-ttu-id="9037c-179">A conclusão bem-sucedida dessa chamada registrará essa instância do aplicativo Chrome com os Hubs de notificação do Azure.</span><span class="sxs-lookup"><span data-stu-id="9037c-179">Successful completion of this call will register this Chrome App instance with Azure Notification Hubs.</span></span>

<span data-ttu-id="9037c-180">A estrutura geral da pasta para este projeto deve ter esta aparência: ![Aplicativo do Google Chrome - Estrutura da Pasta][21]</span><span class="sxs-lookup"><span data-stu-id="9037c-180">The overall folder structure for this project should resemble this: ![Google Chrome App - Folder Structure][21]</span></span>

### <a name="set-up-and-test-your-chrome-app"></a><span data-ttu-id="9037c-181">Configurar e testar seu Aplicativo Chrome</span><span class="sxs-lookup"><span data-stu-id="9037c-181">Set up and test your Chrome App</span></span>
1. <span data-ttu-id="9037c-182">Abra seu navegador Chrome.</span><span class="sxs-lookup"><span data-stu-id="9037c-182">Open your Chrome browser.</span></span> <span data-ttu-id="9037c-183">Abra as **extensões do Chrome** e habilite o **Modo de desenvolvedor**.</span><span class="sxs-lookup"><span data-stu-id="9037c-183">Open **Chrome extensions** and enable **Developer mode**.</span></span>
   
       ![Google Chrome - Enable Developer Mode][16]
2. <span data-ttu-id="9037c-184">Clique em **Carregar extensão descompactada** e navegue até a pasta na qual você criou os arquivos.</span><span class="sxs-lookup"><span data-stu-id="9037c-184">Click **Load unpacked extension** and navigate to the folder where you created the files.</span></span> <span data-ttu-id="9037c-185">Você também pode usar a **Ferramenta de desenvolvimento de extensões e Aplicativos Chrome**.</span><span class="sxs-lookup"><span data-stu-id="9037c-185">You can also optionally use the **Chrome Apps & Extensions Developer Tool**.</span></span> <span data-ttu-id="9037c-186">Essa ferramenta é um Aplicativo Chrome por si só (instalada por meio do Chrome Web Store) e fornece recursos avançados de depuração para o desenvolvimento do seu Aplicativo Chrome.</span><span class="sxs-lookup"><span data-stu-id="9037c-186">This tool is a Chrome App in itself (installed from the Chrome Web Store) and provides advanced debugging capabilities for your Chrome App development.</span></span>
   
       ![Google Chrome - Load Unpacked Extension][17]
3. <span data-ttu-id="9037c-187">Se o Aplicativo Chrome for criado sem erros, você o verá sendo exibido.</span><span class="sxs-lookup"><span data-stu-id="9037c-187">If the Chrome App is created without any errors, then you will see your Chrome App show up.</span></span>
   
       ![Google Chrome - Chrome App Display][18]
4. <span data-ttu-id="9037c-188">Insira o **Número do Projeto** obtido anteriormente do **Console do Google Cloud**, bem como a ID do remetente, e clique em **Registrar no GCM**.</span><span class="sxs-lookup"><span data-stu-id="9037c-188">Enter the **Project Number** that you got earlier from the **Google Cloud Console** as the sender ID, and click **Register with GCM**.</span></span> <span data-ttu-id="9037c-189">Você deve ver a mensagem **Registro no GCM concluído com êxito.**</span><span class="sxs-lookup"><span data-stu-id="9037c-189">You must see the message **Registration with GCM succeeded.**</span></span>
   
       ![Google Chrome - Chrome App Customization][19]
5. <span data-ttu-id="9037c-190">Insira o **Nome do Hub de Notificação** e a **DefaultListenSharedAccessSignature** obtidos anteriormente do portal e clique em **Registrar no Hub de Notificação do Azure**.</span><span class="sxs-lookup"><span data-stu-id="9037c-190">Enter your **Notification Hub Name** and the **DefaultListenSharedAccessSignature** that you obtained from the portal earlier, and click **Register with Azure Notification Hub**.</span></span> <span data-ttu-id="9037c-191">Você deve ver a mensagem **Registro no Hub de Notificação concluído com êxito!**</span><span class="sxs-lookup"><span data-stu-id="9037c-191">You must see the message **Notification Hub Registration successful!**</span></span> <span data-ttu-id="9037c-192">e os detalhes da resposta do registro, que contém a ID de Registro nos Hubs de Notificação do Azure.</span><span class="sxs-lookup"><span data-stu-id="9037c-192">and the details of the registration response, which contains the Azure Notification Hubs registration ID.</span></span>
   
       ![Google Chrome - Specify Notification Hub Details][20]  

## <span data-ttu-id="9037c-193"><a name="send"></a>Enviar uma notificação por push para seu Aplicativo Chrome</span><span class="sxs-lookup"><span data-stu-id="9037c-193"><a name="send"></a>Send a notification to your Chrome App</span></span>
<span data-ttu-id="9037c-194">Para fins de teste, enviaremos notificações por push do Chrome usando um aplicativo de console .NET.</span><span class="sxs-lookup"><span data-stu-id="9037c-194">For testing purposes, we will send Chrome push notifications by using a .NET console application.</span></span> 

> [!NOTE]
> <span data-ttu-id="9037c-195">Você pode enviar notificações por push com os Hubs de Notificação de qualquer back-end por meio da nossa <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">interface REST</a> pública.</span><span class="sxs-lookup"><span data-stu-id="9037c-195">You can send push notifications with Notification Hubs from any backend via our public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="9037c-196">Confira nosso [portal de documentação](https://azure.microsoft.com/documentation/services/notification-hubs/) para obter mais exemplos de plataforma cruzada.</span><span class="sxs-lookup"><span data-stu-id="9037c-196">Check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/) for more cross-platform examples.</span></span>
> 
> 

1. <span data-ttu-id="9037c-197">No Visual Studio, no menu **Arquivo**, selecione **Novo** e **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="9037c-197">In Visual Studio, from the **File** menu, select **New** and then **Project**.</span></span> <span data-ttu-id="9037c-198">No **Visual C#**, clique em **Windows** e em **Aplicativo do Console** e depois clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9037c-198">Under **Visual C#**, click **Windows** and **Console Application**, and then click **OK**.</span></span>  <span data-ttu-id="9037c-199">Isso cria um novo projeto de aplicativo de console.</span><span class="sxs-lookup"><span data-stu-id="9037c-199">This creates a new console application project.</span></span>
2. <span data-ttu-id="9037c-200">No menu **Ferramentas**, clique em **Gerenciador de Pacotes de Biblioteca** e selecione **Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="9037c-200">From the **Tools** menu, click **Library Package Manager** and then **Package Manager Console**.</span></span> <span data-ttu-id="9037c-201">Isso exibe a Console do Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="9037c-201">This displays the Package Manager Console.</span></span>
3. <span data-ttu-id="9037c-202">Na janela da console, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="9037c-202">In the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
       This adds a reference to the Azure Service Bus SDK with the <a href="http://nuget.org/packages/  WindowsAzure.ServiceBus/">WindowsAzure.ServiceBus NuGet package</a>.
4. <span data-ttu-id="9037c-203">Abra `Program.cs` e adicione a seguinte instrução `using`:</span><span class="sxs-lookup"><span data-stu-id="9037c-203">Open `Program.cs` and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="9037c-204">Na classe `Program` , adicione o seguinte método:</span><span class="sxs-lookup"><span data-stu-id="9037c-204">In the `Program` class, add the following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            String message = "{\"data\":{\"message\":\"Hello Chrome from Azure Notification Hubs\"}}";
            await hub.SendGcmNativeNotificationAsync(message);
        }
   
       Make sure to replace the `<hub name>` placeholder with the name of the notification hub that appears in the [portal](https://portal.azure.com) in your Notification Hub blade. Also, replace the connection string placeholder with the connection string called `DefaultFullSharedAccessSignature` that you obtained in the notification hub configuration section.
   
   > [!NOTE]
   > <span data-ttu-id="9037c-205">Verifique se você está usando a cadeia de conexão com acesso **Completo**, não com acesso para **Escutar**.</span><span class="sxs-lookup"><span data-stu-id="9037c-205">Make sure that you use the connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="9037c-206">A cadeia de conexão de acesso **Escutar** não concede permissões para enviar notificações por push.</span><span class="sxs-lookup"><span data-stu-id="9037c-206">The **Listen** access connection string does not grant permissions to send push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="9037c-207">Adicione as seguintes chamadas ao método `Main` :</span><span class="sxs-lookup"><span data-stu-id="9037c-207">Add the following calls in the `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="9037c-208">Verifique se o Chrome está em execução e execute o aplicativo de console.</span><span class="sxs-lookup"><span data-stu-id="9037c-208">Make sure that Chrome is running, and run the console application.</span></span>
8. <span data-ttu-id="9037c-209">Você deve ver a pop-up de notificação abaixo na área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9037c-209">You should see the following notification pop up on your desktop.</span></span>
   
       ![Google Chrome - Notification][13]
9. <span data-ttu-id="9037c-210">Você também pode ver todas as notificações usando a janela de Notificações do Chrome na barra de tarefas (no Windows) quando o Chrome estiver em execução.</span><span class="sxs-lookup"><span data-stu-id="9037c-210">You can also see all your notifications by using the Chrome Notifications window in the taskbar (in Windows) when Chrome is running.</span></span>
   
       ![Google Chrome - Notifications List][14]

> [!NOTE]
> <span data-ttu-id="9037c-211">Você não precisa executar o Aplicativo Chrome ou abrir o navegador (embora o próprio navegador Chrome precise estar em execução).</span><span class="sxs-lookup"><span data-stu-id="9037c-211">You don't need to have the Chrome App running or open in the browser (though the Chrome browser itself must be running).</span></span> <span data-ttu-id="9037c-212">Você também pode obter uma exibição consolidada de todas as suas notificações na janela de notificações do Chrome.</span><span class="sxs-lookup"><span data-stu-id="9037c-212">You also get a consolidated view of all your notifications in the Chrome Notifications window.</span></span>
> 
> 

## <span data-ttu-id="9037c-213"><a name="next-steps"> </a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9037c-213"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="9037c-214">Saiba mais sobre os Hubs de Notificação em [Visão geral dos Hubs de Notificação].</span><span class="sxs-lookup"><span data-stu-id="9037c-214">Learn more about Notification Hubs in [Notification Hubs Overview].</span></span>

<span data-ttu-id="9037c-215">Para ter como alvo usuários específicos, consulte o tutorial [Notificação de usuários nos Hubs de Notificação do Azure] .</span><span class="sxs-lookup"><span data-stu-id="9037c-215">To target specific users, refer to the [Azure Notification Hubs Notify Users] tutorial.</span></span> 

<span data-ttu-id="9037c-216">Se desejar segmentar os usuários por grupos de interesse, você poderá seguir o tutorial [Notícias mais recentes dos Hubs de Notificação do Azure] .</span><span class="sxs-lookup"><span data-stu-id="9037c-216">If you want to segment your users by interest groups, you can follow the [Azure Notification Hubs breaking news] tutorial.</span></span>

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
<span data-ttu-id="9037c-217">[Exemplo de Hub de Notificação do Aplicativo Chrome]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToChromeApps</span><span class="sxs-lookup"><span data-stu-id="9037c-217">[Chrome App Notification Hub Sample]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToChromeApps</span></span>
<span data-ttu-id="9037c-218">[Console do Google Cloud]: http://cloud.google.com/console</span><span class="sxs-lookup"><span data-stu-id="9037c-218">[Google Cloud Console]: http://cloud.google.com/console</span></span>
[Azure Classic Portal]: https://manage.windowsazure.com/
<span data-ttu-id="9037c-219">[Visão geral dos Hubs de Notificação]: notification-hubs-push-notification-overview.md</span><span class="sxs-lookup"><span data-stu-id="9037c-219">[Notification Hubs Overview]: notification-hubs-push-notification-overview.md</span></span>
<span data-ttu-id="9037c-220">[Visão geral de aplicativos Chrome]: https://developer.chrome.com/apps/about_apps</span><span class="sxs-lookup"><span data-stu-id="9037c-220">[Chrome Apps Overview]: https://developer.chrome.com/apps/about_apps</span></span>
<span data-ttu-id="9037c-221">[Exemplo do GCM do Aplicativo Chrome]: https://github.com/GoogleChrome/chrome-app-samples/tree/master/samples/gcm-notifications</span><span class="sxs-lookup"><span data-stu-id="9037c-221">[Chrome App GCM Sample]: https://github.com/GoogleChrome/chrome-app-samples/tree/master/samples/gcm-notifications</span></span>
[Installable Web Apps]: https://developers.google.com/chrome/apps/docs/
<span data-ttu-id="9037c-222">[Aplicativos do Chrome em Dispositivos móveis]: https://developer.chrome.com/apps/chrome_apps_on_mobile</span><span class="sxs-lookup"><span data-stu-id="9037c-222">[Chrome Apps on Mobile]: https://developer.chrome.com/apps/chrome_apps_on_mobile</span></span>
<span data-ttu-id="9037c-223">[Criar um registro da API REST NH]: http://msdn.microsoft.com/library/azure/dn223265.aspx</span><span class="sxs-lookup"><span data-stu-id="9037c-223">[Create Registration NH REST API]: http://msdn.microsoft.com/library/azure/dn223265.aspx</span></span>
<span data-ttu-id="9037c-224">[biblioteca crypto-js]: http://code.google.com/p/crypto-js/</span><span class="sxs-lookup"><span data-stu-id="9037c-224">[crypto-js library]: http://code.google.com/p/crypto-js/</span></span>
[GCM with Chrome Apps]: https://developer.chrome.com/apps/cloudMessaging
<span data-ttu-id="9037c-225">[Google Cloud Messaging para Chrome]: https://developer.chrome.com/apps/cloudMessagingV1</span><span class="sxs-lookup"><span data-stu-id="9037c-225">[Google Cloud Messaging for Chrome]: https://developer.chrome.com/apps/cloudMessagingV1</span></span>
<span data-ttu-id="9037c-226">[Notificação de usuários nos Hubs de Notificação do Azure]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span><span class="sxs-lookup"><span data-stu-id="9037c-226">[Azure Notification Hubs Notify Users]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span></span>
<span data-ttu-id="9037c-227">[Notícias mais recentes dos Hubs de Notificação do Azure]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span><span class="sxs-lookup"><span data-stu-id="9037c-227">[Azure Notification Hubs breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span></span>
