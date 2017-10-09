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
# <a name="send-push-notifications-toochrome-apps-with-azure-notification-hubs"></a>Enviar por push notificações tooChrome aplicativos com Hubs de notificação do Azure
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

Este tópico mostra como toouse Hubs de notificação do Azure toosend envio notificações tooa aplicativo Chrome, que será exibido no contexto de saudação do hello navegador Google Chrome. Neste tutorial, criaremos um Aplicativo Chrome que recebe notificações por push usando o [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/). 

> [!NOTE]
> toocomplete neste tutorial, você deve ter uma conta ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).
> 
> 

tutorial de saudação orienta você por meio de notificações de push de tooenable essas etapas básicas:

* [Habilitar as mensagens em nuvem do Google](#register)
* [Configurar seu Hub de Notificação](#configure-hub)
* [Conecte-se o seu hub de notificação do aplicativo Chrome toohello](#connect-app)
* [Enviar uma notificação de push tooyour aplicativo Chrome](#send)
* [Funcionalidade e recursos adicionais](#next-steps)

> [!NOTE]
> Chrome as notificações de envio do aplicativo não genéricas notificações do navegador, eles são o modelo de extensibilidade de navegador específico toohello (consulte [visão geral de aplicativos do Chrome] para obter detalhes). Além disso toohello navegador de área de trabalho, Chrome aplicativos executados no dispositivo móvel (Android e iOS) por meio do Apache Cordova. Consulte [Chrome aplicativos móveis] toolearn mais.
> 
> 

Configurar o GCM e Hubs de notificação do Azure é tooconfiguring idêntico para o Android, já que [Google Cloud Messaging cromo] foi preterido e Olá GCM mesmo agora dá suporte a dispositivos com Android e instâncias do Chrome.

## <a id="register"></a>Habilitar as mensagens em nuvem do Google
1. Navegue toohello [Google nuvem Console] site da Web, entre com suas credenciais de conta do Google e clique em Olá **criar projeto** botão. Forneça um número apropriado **nome do projeto**e, em seguida, clique em Olá **criar** botão.
   
       ![Google Cloud Console - Create Project][1]
2. Anote Olá **projeto número** em Olá **projetos** página de projeto Olá que você acabou de criar. Você usará isso como Olá **ID do remetente GCM** em Olá Chrome aplicativo tooregister com GCM.
   
       ![Google Cloud Console - Project Number][2]
3. No painel esquerdo do hello, clique em **APIs & auth**e, em seguida, role para baixo e clique Olá alternância tooenable **Google Cloud Messaging para Android**. Você não tem tooenable **Google Cloud Messaging cromo**.
   
       ![Google Cloud Console - Server Key][3]
4. No painel esquerdo do hello, clique em **credenciais** > **criar nova chave** > **chave do servidor** > **criar**.
   
       ![Google Cloud Console - Credentials][4]
5. Tome nota do servidor de saudação **chave API**. Você vai configurar isso em seu tooenable em seguida, do hub de notificação-toosend tooGCM de notificações de envio.
   
       ![Google Cloud Console - API Key][5]

## <a id="configure-hub"></a>Configurar seu Hub de Notificação
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

&emsp;&emsp;6.   Em Olá **configurações** folha, selecione **Notification Services** e **Google (GCM)**. Insira a chave de API hello e salvar.

&emsp;&emsp;![Hubs de Notificação do Azure - Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

## <a id="connect-app"></a>Conecte-se o seu hub de notificação do aplicativo Chrome toohello
Hub de notificação está agora configurado toowork com GCM e ter tooregister de cadeias de caracteres de conexão Olá tooboth seu aplicativo para receber e enviar notificações por push. LK

### <a name="create-a-new-chrome-app"></a>Criar um novo Aplicativo Chrome
exemplo Hello abaixo se baseia Olá [Chrome aplicativo GCM exemplo] e usa Olá recomendado toocreate de maneira um aplicativo Chrome. Vamos destacar Olá de etapas relacionadas especificamente tooAzure Hubs de notificação. 

> [!NOTE]
> É recomendável que você baixe fonte Olá para este aplicativo de cromo do [exemplo de Hub de notificação de aplicativo Chrome].
> 
> 

Olá Chrome aplicativo é criado por meio de JavaScript, e você pode usar qualquer um dos editores word preferencial para criá-lo. Abaixo, esta é a aparência desse aplicativo Chrome.

![Aplicativo Google Chrome][15]

1. Crie uma pasta e chame-a de `ChromePushApp`. Naturalmente, o nome de saudação é arbitrário - se você o nomear algo diferente, certifique-se de que substituir o caminho Olá em segmentos de código Olá necessário.
2. Baixar Olá [biblioteca de criptografia js] na pasta Olá criado na etapa segundo hello. Essa pasta de biblioteca contém duas subpastas: `components` e `rollups`.
3. Crie um arquivo do `manifest.json` . Todos os aplicativos de cromo contam com um arquivo de manifesto que contém metadados do aplicativo hello e, mais importante, todas as permissões que são concedidas toohello aplicativo quando o usuário Olá instala.
   
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
   
    Saudação de aviso `permissions` elemento, que especifica que este aplicativo Chrome será capaz de tooreceive as notificações de envio do GCM. Ele também deve especificar Olá URI de Hubs de notificação do Azure onde Olá Chrome aplicativo fará um tooregister da chamada REST.
    Nosso aplicativo de exemplo também usa um arquivo de ícone, `gcm_128.png`, que você encontrará na fonte de saudação que é reutilizado de exemplo do hello original GCM. Você pode substituí-lo para qualquer imagem que couber Olá [critérios de ícone](https://developer.chrome.com/apps/manifest/icons).
4. Crie um arquivo chamado `background.js` com hello código a seguir:
   
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
   
    Este é o arquivo hello que aparecer a janela do aplicativo de cromo Olá HTML (**register.html**) e também define o manipulador de saudação **messageReceived** notificação toohandle Olá de entrada por push.
5. Crie um arquivo chamado `register.html` -define Olá interface de usuário do hello aplicativo Chrome. 
   
   > [!NOTE]
   > Este exemplo usa **CryptoJS v3.1.2**. Se você baixou a outra versão da biblioteca de saudação, certifique-se de substituí-lo corretamente por versão Olá Olá `src` caminho.
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
6. Crie um arquivo chamado `register.js` com código de saudação abaixo. Esse arquivo Especifica o script hello atrás `register.html`. Chrome aplicativos não permitem execução embutida, permitindo toocreate um script de backup separado para a interface do usuário.
   
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
   
    Olá acima script tem Olá parâmetros de chave a seguir:
   
   * **OnLoad** define eventos de clique do botão Olá dos botões Olá dois Olá da interface do usuário. Um registra GCM e Olá outros usa a ID de registro de saudação que é retornado após o registro com GCM tooregister com Hubs de notificação do Azure.
   * **updateLog** é função hello que nos permite recursos de log simples de toohandle.
   * **registerWithGCM** Olá primeiro clique do botão manipulador, que torna Olá `chrome.gcm.register` chamada tooGCM tooregister Olá atual aplicativo Chrome instância.
   * **registerCallback** é Olá função de retorno de chamada que é chamada quando a chamada de registro do GCM de hello retorna.
   * **registerWithNH** Olá segundo clique do botão manipulador, que registra com Hubs de notificação. Ele obtém `hubName` e `connectionString` (especificou qual usuário Olá) e artesanatos Olá chamada à API de REST de registro de Hubs de notificação.
   * **splitConnectionString** e **generateSaSToken** são auxiliares que representam a implementação de um processo de criação de token SaS, que deve ser usado em todas as chamadas da API REST JavaScript hello. Para saber mais, veja [Conceitos comuns](http://msdn.microsoft.com/library/dn495627.aspx).
   * **sendNHRegistrationRequest** é chamada de função de saudação que faz uma pausa de HTTP tooAzure Hubs de notificação.
   * **registrationPayload** define a carga XML de registro de saudação. Para obter mais informações, veja [Criar um registro da API REST NH]. Podemos atualizar ID do registro Olá nele com o que recebemos do GCM.
   * **cliente** é uma instância de **XMLHttpRequest** que usamos solicitação de HTTP POST toomake hello. Observe que podemos atualizar Olá `Authorization` cabeçalho com `sasToken`. A conclusão bem-sucedida dessa chamada registrará essa instância do aplicativo Chrome com os Hubs de notificação do Azure.

Olá geral estrutura de pasta para este projeto deve ser semelhante a esta: ![Google Chrome aplicativo - estrutura de pasta][21]

### <a name="set-up-and-test-your-chrome-app"></a>Configurar e testar seu Aplicativo Chrome
1. Abra seu navegador Chrome. Abra as **extensões do Chrome** e habilite o **Modo de desenvolvedor**.
   
       ![Google Chrome - Enable Developer Mode][16]
2. Clique em **carregar a extensão desempacotado** e navegue toohello pasta em que você criou arquivos hello. Você também pode usar o hello **aplicativos Chrome & ferramenta de desenvolvimento de extensões**. Essa ferramenta é um aplicativo de cromo em si (instalado da saudação cromo da Web repositório) e fornece recursos avançados de depuração para o desenvolvimento de aplicativos do Chrome.
   
       ![Google Chrome - Load Unpacked Extension][17]
3. Se Olá Chrome aplicativo é criado sem erros, em seguida, você verá seu aplicativo Chrome aparecem.
   
       ![Google Chrome - Chrome App Display][18]
4. Digite hello **projeto número** que você obteve anteriormente Olá **Google nuvem Console** como ID do remetente hello e clique em **registrar com GCM**. Você deve ver uma mensagem de saudação **registro com êxito do GCM.**
   
       ![Google Chrome - Chrome App Customization][19]
5. Insira seu **nome do Hub de notificação** e hello **DefaultListenSharedAccessSignature** que você obteve no portal de saudação anteriormente e clique em **registrar com o Hub de notificação do Azure**. Você deve ver uma mensagem de saudação **registro do Hub de notificação com êxito!** e a ID de detalhes de saudação da resposta de registro hello, que contém Olá registro de Hubs de notificação do Azure.
   
       ![Google Chrome - Specify Notification Hub Details][20]  

## <a name="send"></a>Enviar uma notificação tooyour aplicativo Chrome
Para fins de teste, enviaremos notificações por push do Chrome usando um aplicativo de console .NET. 

> [!NOTE]
> Você pode enviar notificações por push com os Hubs de Notificação de qualquer back-end por meio da nossa <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">interface REST</a> pública. Confira nosso [portal de documentação](https://azure.microsoft.com/documentation/services/notification-hubs/) para obter mais exemplos de plataforma cruzada.
> 
> 

1. No Visual Studio, de saudação **arquivo** menu, selecione **novo** e **projeto**. No **Visual C#**, clique em **Windows** e em **Aplicativo do Console** e depois clique em **OK**.  Isso cria um novo projeto de aplicativo de console.
2. De saudação **ferramentas** menu, clique em **Gerenciador de biblioteca de pacote** e **Package Manager Console**. Isso exibe o saudação Package Manager Console.
3. Na janela de console hello, execute Olá comando a seguir:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
       This adds a reference toohello Azure Service Bus SDK with hello <a href="http://nuget.org/packages/  WindowsAzure.ServiceBus/">WindowsAzure.ServiceBus NuGet package</a>.
4. Abra `Program.cs` e adicione o seguinte Olá `using` instrução:
   
        using Microsoft.Azure.NotificationHubs;
5. Em Olá `Program` classe, adicione o seguinte método de saudação:
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            String message = "{\"data\":{\"message\":\"Hello Chrome from Azure Notification Hubs\"}}";
            await hub.SendGcmNativeNotificationAsync(message);
        }
   
       Make sure tooreplace hello `<hub name>` placeholder with hello name of hello notification hub that appears in hello [portal](https://portal.azure.com) in your Notification Hub blade. Also, replace hello connection string placeholder with hello connection string called `DefaultFullSharedAccessSignature` that you obtained in hello notification hub configuration section.
   
   > [!NOTE]
   > Certifique-se de que você use a cadeia de caracteres de conexão de saudação com **completo** acessar, não **escutar** acesso. Olá **escutar** cadeia de caracteres de conexão de acesso não concede permissões toosend notificações de envio.
   > 
   > 
6. Adicione a seguinte Olá chamadas em Olá `Main` método:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Certifique-se de que está executando o Chrome e executar o aplicativo de console hello.
8. Você deve ver Olá seguinte notificação pop-up na área de trabalho.
   
       ![Google Chrome - Notification][13]
9. Você também pode ver todas as notificações, usando a janela de cromo notificações de saudação na barra de tarefas da saudação (no Windows) quando o Chrome está em execução.
   
       ![Google Chrome - Notifications List][14]

> [!NOTE]
> Você não precisa toohave Olá Chrome aplicativo em execução ou aberto no navegador de saudação (embora o próprio navegador de cromo Olá deve estar em execução). Você também pode obter uma visão consolidada de todas as notificações na janela de notificações de cromo hello.
> 
> 

## <a name="next-steps"> </a>Próximas etapas
Saiba mais sobre os Hubs de Notificação em [Visão geral dos Hubs de Notificação].

tootarget de usuários específicos, consulte toohello [notificar usuários de Hubs de notificação do Azure] tutorial. 

Se você quiser toosegment os usuários, grupos de interesse, você pode seguir Olá [Hubs de notificação do Azure últimas notícias] tutorial.

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
