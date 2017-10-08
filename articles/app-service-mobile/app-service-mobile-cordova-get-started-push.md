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
# <a name="add-push-notifications-tooyour-apache-cordova-app"></a>Adicionar aplicativo do envio notificações tooyour Apache Cordova
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Visão geral
Neste tutorial, você deve adicionar um projeto de toohello [início rápido do Apache Cordova] notificações por push para que uma notificação por push seja enviada toohello dispositivo toda vez que um registro é inserido.

Se você não usar Olá baixar o projeto de servidor de início rápido, precisa Olá pacote de extensão de notificação por push. Para obter mais informações, consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure][1].

## <a name="prerequisites"></a>Pré-requisitos
Este tutorial aborda um aplicativo do Apache Cordova desenvolvido com o Visual Studio 2015 que é executado em um dispositivo iOS, um dispositivo Android, um dispositivo do Windows e Olá emulador Android da Google.

toocomplete neste tutorial, você precisa:

* Um computador com o [Visual Studio Community 2015][2] ou versão posterior.
* [Ferramentas do Visual Studio para Apache Cordova][4].
* Uma [conta ativa do Azure][3].
* Um projeto de [Início rápido do Apache Cordova][5] concluído.
* (Android) Uma [Conta do Google][6] com um endereço de email confirmado.
* (iOS) Uma [associação ao Programa de Desenvolvedores da Apple][7] e um dispositivo iOS (o simulador iOS não dá suporte a envio por push).
* (Windows) Uma [conta de desenvolvedor da Windows Store][8] e um dispositivo com Windows 10.

## <a name="configure-hub"></a>Configurar um Hub de Notificação
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

[Assista a um vídeo mostrando as etapas nesta seção][9]

## <a name="update-hello-server-project"></a>Atualizar o projeto do servidor de saudação
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="add-push-to-app"></a>Modificar seu aplicativo Cordova
Certifique-se de que seu projeto de aplicativo do Apache Cordova está pronto toohandle notificações de push pelo plug-in por push do Cordova do hello instalar mais todos os serviços específicos de plataforma push.

#### <a name="update-hello-cordova-version-in-your-project"></a>Atualize a versão do Cordova Olá em seu projeto.
Se seu projeto usa uma versão anterior ao v6.1.1 do Apache Cordova, atualize o projeto de cliente de saudação. projeto de saudação tooupdate:

* Clique com botão direito `config.xml` tooopen designer de configuração de saudação.
* Selecione a guia de plataformas de saudação.
* Escolher 6.1.1 Olá **Cordova CLI** caixa de texto.
* Escolha **criar**, em seguida, **compilar solução** tooupdate projeto de saudação.

#### <a name="install-hello-push-plugin"></a>Instalar o plug-in de push Olá
Os aplicativos Apache Cordova não manipulam recursos de rede ou do dispositivo de forma nativa.  Essas funcionalidades são fornecidas por plug-ins publicados no [npm][10] ou no GitHub.  Olá `phonegap-plugin-push` plug-in é usado toohandle notificações de envio de rede.

Você pode instalar o plug-in de envio de saudação em uma das seguintes maneiras:

**De saudação do prompt de comando:**

Execute Olá comando a seguir:

    cordova plugin add phonegap-plugin-push

**No Visual Studio:**

1. No Gerenciador de soluções, abra Olá `config.xml` arquivo clique **plug-ins** > **personalizado**, selecione **Git** como a origem de instalação, digite `https://github.com/phonegap/phonegap-plugin-push`como fonte de saudação.

   ![][img1]

2. Clique em Olá seta Avançar toohello origem da instalação.
3. Em **SENDER_ID**, se você já tiver uma ID de projeto numérico para o projeto de Console de desenvolvedor do Google hello, você pode adicioná-lo aqui. Caso contrário, insira um valor de espaço reservado, como 777777.  Se estiver direcionando o projeto para o Android, atualize esse valor no arquivo config.xml mais tarde.
4. Clique em **Adicionar**.

plug-in de push Olá agora está instalado.

#### <a name="install-hello-device-plugin"></a>Instalar o plug-in de dispositivo Olá
Siga Olá mesmo procedimento usado tooinstall Olá push plugin.  Adicionar plug-in do hello dispositivo na lista de plug-ins do núcleo hello (clique **plug-ins** > **Core** toofind-lo). É necessário que esse nome de plataforma do plug-in tooobtain hello.

#### <a name="register-your-device-on-application-start-up"></a>Registrar seu dispositivo na inicialização do aplicativo
Inicialmente, incluiremos alguns códigos mínimos para o Android. Mais tarde, modificar Olá aplicativo toorun em iOS ou Windows 10.

1. Adicionar uma chamada muito**registerForPushNotifications** durante a saudação de retorno de chamada para o processo de logon hello, ou final Olá Olá **onDeviceReady** método:

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

    Este exemplo mostra a chamada **registerForPushNotifications** após a autenticação bem-sucedida.  Você pode chamar `registerForPushNotifications()` sempre que precisar.

2. Adicionar Olá novo **registerForPushNotifications** método da seguinte maneira:

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
3. (Android) Olá anterior do código, substitua `Your_Project_ID` com numérica Olá ID do projeto para o aplicativo do [Console de desenvolvedor do Google][18].

## <a name="optional-configure-and-run-hello-app-on-android"></a>(Opcional) Configurar e executar o aplicativo hello no Android
Conclua as notificações de push de tooenable esta seção para Android.

#### <a name="enable-gcm"></a>Habilitar mensagens de nuvem Firebase
Como pretendemos Olá plataforma Google Android inicialmente, você deve habilitar Firebase Cloud Messaging.

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <a name="configure-backend"></a>Configurar Olá aplicativo móvel back-end toosend push solicitações usando FCM
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a>Configurar seu aplicativo Cordova para Android
Em seu aplicativo Cordova, abra config.xml e substitua `Your_Project_ID` com numérica Olá ID do projeto para o aplicativo de saudação [Console de desenvolvedor do Google][18].

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

Abrir js e atualizar Olá código toouse sua ID do projeto numérico.

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <a name="configure-device"></a>Configurar seu dispositivo Android para depuração USB
Antes de implantar seu aplicativo tooyour dispositivo Android, você precisa tooenable depuração de USB.  Execute as etapas a seguir em seu telefone com Android:

1. Vá muito**configurações** > **sobre o telefone**, em seguida, toque em Olá **número da compilação** até que o modo de desenvolvedor está habilitado (cerca de sete vezes).
2. Em **configurações** > **opções do desenvolvedor** habilitar **depuração de USB**, em seguida, conecte-se seu PC de desenvolvimento tooyour telefone Android com um cabo USB.

Testamos isso usando um dispositivo Google Nexus 5X que executa o Android 6.0 (Marshmallow).  No entanto, as técnicas de saudação são comuns em qualquer versão do Android moderno.

#### <a name="install-google-play-services"></a>Instalar os Serviços do Google Play
plug-in de envio de saudação se baseia em Android Google executar serviços para notificações por push.

1. No Visual Studio, clique em **ferramentas** > **Android** > **Gerenciador de SDK do Android**, expanda Olá **Extras** pasta e seleção Olá caixa toomake-se de que cada um dos seguintes SDKs de saudação está instalada.

   * Android 2.3 ou superior
   * Google Repository revisão 27 ou superior
   * Serviços do Google Play 9.0.2 ou superior

2. Clique em **instalar pacotes** e aguarde Olá toocomplete de instalação.

Hello atual necessário bibliotecas são listadas na Olá [documentação de instalação de push de plug-in de phonegap][19].

#### <a name="test-push-notifications-in-hello-app-on-android"></a>Notificações por push de teste no aplicativo hello no Android
Você pode agora as notificações por push de teste executando Olá aplicativo e inserindo itens na tabela TodoItem de saudação. Você pode testar no hello mesmo dispositivo ou de um segundo dispositivo, enquanto você estiver usando Olá mesmo back-end. Teste seu aplicativo Cordova na plataforma Android Olá em uma saudação maneiras a seguir:

* **Em um dispositivo físico:** anexar seu computador de desenvolvimento do dispositivo Android tooyour com um cabo USB.  Em vez de **Emulador do Google Android**, selecione **Dispositivo**. Visual Studio implanta o dispositivo de toohello aplicativo hello e, em seguida, executa o aplicativo hello.  Você pode interagir com o aplicativo hello no dispositivo de saudação.

  Melhore a experiência de desenvolvimento.  O compartilhamento de tela de aplicativos como o [Mobizen][20] pode ajudar a desenvolver um aplicativo Android.  Mobizen projeta o navegador da web Android tela tooa em seu computador.

* **Em um emulador do Android**: há etapas de configuração adicionais exigidas durante a execução em um emulador.

    Verifique se que você está implantando tooa dispositivo virtual que tem a APIs do Google definido como destino hello, conforme mostrado no Gerenciador de dispositivo Virtual Android (AVD) hello.

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    Se você quiser que um mais rápido x86 toouse emulador, você [instalar Olá HAXM driver] [ 11] e configurar Olá emulador toouse-lo.

    Adicionar um dispositivo Android do Google conta toohello clicando **aplicativos** > **configurações** > **adicionar conta**, em seguida, siga os prompts de saudação.

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    Executar aplicativo de lista de tarefas pendentes hello como antes e inserir um novo item de tarefas. Neste momento, um ícone de notificação é exibido na área de notificação de saudação. Você pode abrir Olá notificação gaveta tooview Olá texto completo da notificação de saudação.

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a>(Opcional) Configurar e executar no iOS
Esta seção é para executar o projeto do Cordova Olá em dispositivos iOS. Se não estiver trabalhando com dispositivos iOS, você poderá ignorar esta seção.

#### <a name="install-and-run-hello-ios-remote-build-agent-on-a-mac-or-cloud-service"></a>Instalação e execução Olá iOS remota de agente de compilação em um serviço de nuvem ou Mac
Antes de executar um aplicativo Cordova no iOS usando o Visual Studio, passar por etapas Olá Olá [guia de instalação do iOS] [ 12] tooinstall e Olá execução remota de agente de compilação.

Verifique se que você pode criar o aplicativo hello para iOS. Hello etapas no guia de instalação de saudação são toobuild necessária para iOS do Visual Studio. Se você não tiver um Mac, você pode criar para iOS usando o agente de compilação remota Olá em um serviço como MacInCloud. Para obter mais informações, consulte [executar seu aplicativo iOS na nuvem Olá][21].

> [!NOTE]
> XCode 7 ou superior é necessário toouse Olá push plug-in no iOS.

#### <a name="find-hello-id-toouse-as-your-app-id"></a>Localizar Olá ID toouse como sua ID do aplicativo
Antes de registrar seu aplicativo para notificações de push, abra config em seu aplicativo Cordova, localize Olá `id` valor no elemento de widget de saudação do atributo e copiá-lo para uso posterior. Olá XML a seguir, Olá ID é `io.cordova.myapp7777777`.

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

Depois, use esse identificador ao criar uma ID de aplicativo no portal do desenvolvedor da Apple. Se você criar uma ID de aplicativo diferente no portal do desenvolvedor hello, você deve tomar algumas etapas adicionais posteriormente neste tutorial. Olá ID no elemento widget deve corresponder Olá ID do aplicativo no portal do desenvolvedor de saudação.

#### <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a>Registrar aplicativo hello para notificações por push no portal do desenvolvedor da Apple
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[Assista a um vídeo que mostra etapas semelhantes](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-toosend-push-notifications"></a>Configurar notificações por push de toosend do Azure
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a>Verifique se a ID do aplicativo corresponde ao aplicativo Cordova
Se Olá ID do aplicativo criado na sua conta de desenvolvedor da Apple já corresponder a ID de saudação do elemento de widget de saudação config, você pode ignorar esta etapa. No entanto, se Olá IDs não corresponderem, execute Olá etapas a seguir:

1. Exclua a pasta de plataformas de saudação do seu projeto.
2. Exclua a pasta de plug-ins de saudação do seu projeto.
3. Exclua pasta node_modules de saudação do seu projeto.
4. Atualize atributo de id de saudação do elemento de widget de saudação em config.xml toouse Olá ID do aplicativo que você criou na sua conta de desenvolvedor da Apple.
5. Recompile o projeto.

##### <a name="test-push-notifications-in-your-ios-app"></a>Testar notificações por push em seu aplicativo iOS
1. No Visual Studio, verifique se **iOS** é selecionado como destino de implantação hello e, em seguida, escolha **dispositivo** toorun em seu dispositivo iOS conectado.

    Você pode executar em um dispositivo conectado de iOS tooyour PC usando o iTunes. Olá simulador de iOS não dá suporte a notificações por push.

2. Olá pressione **executar** botão ou **F5** no Visual Studio toobuild projeto saudação inicial Olá aplicativo em um dispositivo iOS e clique em **Okey** tooaccept as notificações de envio.

   > [!NOTE]
   > Olá aplicativo solicita a confirmação para notificações por push durante a saudação executado pela primeira vez.

3. No aplicativo hello, digite uma tarefa e clique em hello mais (+) ícone.
4. Verifique se uma notificação é recebida e clique toodismiss Okey Olá notificação.

## <a name="optional-configure-and-run-on-windows"></a>(Opcional) Configurar e executar no Windows
Esta seção é para executar o projeto de aplicativo do Apache Cordova Olá em dispositivos Windows 10 (plug-in do hello PhoneGap push tem suporte no Windows 10). Se não estiver trabalhando com dispositivos Windows, você poderá ignorar esta seção.

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a>Registrar seu aplicativo Windows para notificações por push com WNS
Opções de armazenamento de saudação toouse no Visual Studio, selecione um destino do Windows na lista de plataformas de solução hello, como **Windows x64** ou **Windows x86** (evitar **Windows AnyCPU** para notificações por push).

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

[Assista a um vídeo que mostra etapas semelhantes][13]

#### <a name="configure-hello-notification-hub-for-wns"></a>Configurar o hub de notificação Olá para o WNS
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-toosupport-windows-push-notifications"></a>Configurar as notificações de push Cordova app toosupport Windows
Designer de configuração Olá aberto (com o botão direito em config.xml e selecione **View Designer**), selecione Olá **Windows** guia e escolha **Windows 10** em **Versão de destino do windows**.

compilações de notificações por push de toosupport no padrão (depuração), build.json abrir arquivo. Copie a configuração de depuração "versão" tooyour de configuração.

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

Após a atualização de Olá, Olá build.json devem conter Olá código a seguir:

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

Compile o aplicativo hello e verifique se nenhum erro. Seu aplicativo cliente agora deve registrar para notificações de saudação do back-end de aplicativo móvel hello. Repita esta seção para cada projeto do Windows em sua solução.

#### <a name="test-push-notifications-in-your-windows-app"></a>Testar as notificações por push em seu aplicativo para Windows
No Visual Studio, certifique-se de que uma plataforma Windows é selecionada como destino de implantação hello, como **Windows x64** ou **Windows x86**. aplicativo de saudação toorun em um PC com Windows 10 hospeda o Visual Studio, escolha **Máquina Local**.

Olá pressione executar botão toobuild Olá projeto e inicie o aplicativo hello.

No aplicativo hello, digite um nome para um todoitem novo e clique em hello mais (+) ícone tooadd-lo.

Verifique se que uma notificação é recebida quando Olá item é adicionado.

## <a name="next-steps"></a>Próximas etapas
* Leia sobre [Hubs de notificação] [ 17] toolearn sobre notificações por push.
* Se você ainda não tiver feito isso, continuar tutorial Olá por [adicionar autenticação] [ 14] tooyour Apache Cordova app.

Saiba como toouse Olá SDKs.

* [SDK do Apache Cordova][15]
* [SDK do Servidor ASP.NET][1]
* [SDK do Servidor Node.js][16]

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
