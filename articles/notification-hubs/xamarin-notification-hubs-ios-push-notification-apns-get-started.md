---
title: "aaaiOS notificações por Push com Hubs de notificação para aplicativos Xamarin | Microsoft Docs"
description: "Neste tutorial, você aprenderá como toouse Hubs de notificação do Azure toosend enviar por push o aplicativo do iOS notificações tooa Xamarin."
services: notification-hubs
keywords: "notificações por push do IOS, mensagens por push, notificações por push, mensagem por push"
documentationcenter: xamarin
author: ysxu
manager: erikre
editor: 
ms.assetid: 4d4dfd42-c5a5-4360-9d70-7812f96924d2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 8db60338047dd53074b4d3d4bb127aa6d9f13a25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="ios-push-notifications-with-notification-hubs-for-xamarin-apps"></a>Notificações por push do iOS com Hubs de Notificação para aplicativos Xamarin
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Visão geral
> [!IMPORTANT]
> toocomplete neste tutorial, você deve ter uma conta ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).
> 
> 

Este tutorial mostra como o aplicativo do iOS tooan notificações de envio toouse toosend de Hubs de notificação do Azure.
Você criará um aplicativo xamarin em branco que recebe notificações por push usando Olá [Apple Push Notification Service (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html). Quando você terminar, você será capaz de toouse sua toobroadcast de hub de notificação por push notificações tooall Olá a dispositivos que executam seu aplicativo. Olá código concluído está disponível no hello [aplicativo hubs de notificação] [ GitHub] exemplo.

Este tutorial demonstra push simples Olá cenário difusão de mensagem com Hubs de notificação.

## <a name="prerequisites"></a>Pré-requisitos
Este tutorial requer o seguinte hello:

* [Xcode 6.0][Install Xcode]
* Um dispositivo compatível com o iOS 7.0 (ou versão posterior)
* Associação no Programa de Desenvolvedores de iOS
* [Xamarin Studio]
  
  > [!NOTE]
  > Devido aos requisitos de configuração para notificações de push do iOS, você deve implantar e testar o aplicativo de exemplo hello em um dispositivo físico iOS (iPhone ou iPad) em vez de no simulador Olá.
  > 
  > 

A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais sobre Hubs de Notificação para aplicativos Xamarin iOS.

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub"></a>Configurar seu Hub de Notificação
Esta seção orienta você pela criação de um novo hub de notificação e configurar a autenticação com APNS usando Olá **. p12** certificado de push que você criou. Se você quiser toouse um hub de notificação que você já tiver criado, você poderá ignorar toostep 5.

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li>

<p>Como queremos que a conexão de APNS tooconfigure hello, em Olá Portal do Azure, abra as configurações do Hub de notificação, clique ande em <b>Notification Services</b>e, em seguida, clique em Olá <b>Apple (APNS)</b> item na lista de saudação. Quando terminar, clique em <b>carregar certificado</b> e selecione hello <b>. p12</b> certificado que você exportou anteriormente, bem como a senha Olá certificado hello.</p>

<p>Certifique-se de que tooselect <b>Sandbox</b> modo desde que você está enviando por push as mensagens em um ambiente de desenvolvimento. Somente use Olá <b>produção</b> configuração se quiser toosend toousers de notificações de envio que já compraram o aplicativo da loja de saudação.</p>
</li>
</ol>
&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)

&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-sandbox.png)

O hub de notificação agora está configurado toowork com APNS e ter Olá tooregister de cadeias de caracteres de conexão de seu aplicativo e enviar notificações por push.

## <a name="connect-your-app-toohello-notification-hub"></a>Conecte-se o seu hub de notificação do aplicativo toohello
#### <a name="create-a-new-project"></a>Criar um novo projeto
1. No Xamarin Studio, crie um novo projeto de iOS e selecione Olá **API unificada** > **único aplicativo de exibição** modelo.
   
     ![Xamarin Studio - selecionar o tipo de aplicativo][31]
2. Adicione um componente de mensagens do Azure de toohello de referência. Em Olá solução exibir, clique com botão direito Olá **componentes** pasta do seu projeto e escolha **obter mais componentes**. Pesquise Olá **mensagens do Azure** componente e adicionar Olá componente tooyour projeto.
3. Em **appdelegate. CS**, adicione o seguinte Olá usando a instrução:
   
        using WindowsAzure.Messaging;
4. Declarar uma instância de **SBNotificationHub**:
   
        private SBNotificationHub Hub { get; set; }
5. Criar um **Constants.cs** classe com hello variáveis a seguir:
   
        // Azure app-specific connection string and hub path
        public const string ConnectionString = "<Azure connection string>";
        public const string NotificationHubPath = "<Azure hub path>";
6. Em **appdelegate. CS**, atualizar **FinishedLaunching()** toomatch a seguir hello:
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            if (UIDevice.CurrentDevice.CheckSystemVersion (8, 0)) {
                var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                       UIUserNotificationType.Alert | UIUserNotificationType.Badge | UIUserNotificationType.Sound,
                       new NSSet ());
   
                UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
                UIApplication.SharedApplication.RegisterForRemoteNotifications ();
            } else {
                UIRemoteNotificationType notificationTypes = UIRemoteNotificationType.Alert | UIRemoteNotificationType.Badge | UIRemoteNotificationType.Sound;
                UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (notificationTypes);
            }
   
            return true;
        }
7. Substituir saudação **RegisteredForRemoteNotifications()** método **appdelegate. CS**:
   
        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            Hub = new SBNotificationHub(Constants.ConnectionString, Constants.NotificationHubPath);
   
            Hub.UnregisterAllAsync (deviceToken, (error) => {
                if (error != null)
                {
                    Console.WriteLine("Error calling Unregister: {0}", error.ToString());
                    return;
                }
   
                NSSet tags = null; // create tags if you want
                Hub.RegisterNativeAsync(deviceToken, tags, (errorCallback) => {
                    if (errorCallback != null)
                        Console.WriteLine("RegisterNativeAsync error: " + errorCallback.ToString());
                });
            });
        }
8. Substituir saudação **ReceivedRemoteNotification()** método **appdelegate. CS**:
   
        public override void ReceivedRemoteNotification(UIApplication application, NSDictionary userInfo)
        {
            ProcessNotification(userInfo, false);
        }
9. Crie seguinte Olá **ProcessNotification()** método **appdelegate. CS**:
   
        void ProcessNotification(NSDictionary options, bool fromFinishedLaunching)
        {
            // Check toosee if hello dictionary has hello aps key.  This is hello notification payload you would have sent
            if (null != options && options.ContainsKey(new NSString("aps")))
            {
                //Get hello aps dictionary
                NSDictionary aps = options.ObjectForKey(new NSString("aps")) as NSDictionary;
   
                string alert = string.Empty;
   
                //Extract hello alert text
                // NOTE: If you're using hello simple alert by just specifying
                // "  aps:{alert:"alert msg here"}  ", this will work fine.
                // But if you're using a complex alert with Localization keys, etc.,
                // your "alert" object from hello aps dictionary will be another NSDictionary.
                // Basically hello JSON gets dumped right into a NSDictionary,
                // so keep that in mind.
                if (aps.ContainsKey(new NSString("alert")))
                    alert = (aps [new NSString("alert")] as NSString).ToString();
   
                //If this came from hello ReceivedRemoteNotification while hello app was running,
                // we of course need toomanually process things like hello sound, badge, and alert.
                if (!fromFinishedLaunching)
                {
                    //Manually show an alert
                    if (!string.IsNullOrEmpty(alert))
                    {
                        UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                        avAlert.Show();
                    }
                }
            }
        }
   
   > [!NOTE]
   > Você pode escolher toooverride **FailedToRegisterForRemoteNotifications()** toohandle situações como nenhuma conexão de rede. Isso é especialmente importante onde usuário Olá pode iniciar o aplicativo no modo offline (por exemplo, avião) e desejar push toohandle cenários específicos tooyour aplicativo de mensagens.
   > 
   > 
10. Execute o aplicativo hello em seu dispositivo.

## <a name="sending-push-notifications"></a>Como enviar notificações por push
Você pode testar o recebimento de notificações por push em seu aplicativo pelo envio de notificações em Olá [Portal do Azure] via Olá **teste enviar** recurso Olá **solução de problemas** conjunto de ferramentas, à direita na página de hub de notificação hello, conforme mostrado na saudação de tela abaixo.

![](./media/notification-hubs-ios-get-started/notification-hubs-test-send.png)

As notificações por push normalmente são enviadas por meio de um serviço de back-end como Serviços Móveis ou ASP.NET usando uma biblioteca compatível. Você também pode usar o hello API REST diretamente toosend push mensagens se uma biblioteca não está disponível em seu cenário. 

Neste tutorial, nós manter a simplicidade e demonstrar a testar seu aplicativo de cliente por meio do envio de notificações usando Olá SDK .NET para hubs de notificação em um aplicativo de console, em vez de um serviço de back-end. É recomendável Olá [usar Hubs de notificação toopush notificações toousers](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial como a próxima etapa hello para enviar notificações de um back-end do ASP.NET. No entanto, a saudação abordagens a seguir pode ser usada para enviar notificações:

* **Interface REST**: você pode dar suporte a notificação por push em qualquer plataforma de back-end usando Olá [interface REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).
* **SDK .NET de Hubs de notificação do Microsoft Azure**: em Olá Gerenciador de pacotes do Nuget para Visual Studio, execute [Microsoft.Azure.NotificationHubs Install-Package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).
* **Node.js** : [como toouse Hubs de notificação do Node. js](notification-hubs-nodejs-push-notification-tutorial.md).

**Aplicativos móveis**: para obter um exemplo de como toosend notificações de um back-end aplicativos de celular do serviço de aplicativo do Azure que esteja integrado com Hubs de notificação, consulte [aplicativo móvel de tooyour adicionar de notificações por push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).

* **Java / PHP**: para obter um exemplo de como as notificações por push de toosend usando Olá APIs REST, consulte "como toouse Hubs de notificação do Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

#### <a name="optional-send-push-notifications-from-a-net-console-app"></a>(Opcional) Enviar notificações por push de um Aplicativo de Console do .NET.
Nesta seção, enviaremos as notificações por push usando um aplicativo de console .NET simples Para fins de saudação deste exemplo, nós iremos mudar tooa ambiente de desenvolvimento de Windows que tenha o Visual Studio já instalado.

1. No Visual Studio, crie um novo aplicativo de console em Visual C#:
   
       ![Visual Studio - Create a new console application][213]
2. No Visual Studio, clique em **Ferramentas**, em **Gerenciador de Pacotes NuGet** e em **Console do Gerenciador de Pacotes**.
   
    console do Gerenciador de pacote de saudação deve aparecer encaixada toohello inferior do espaço de trabalho do Visual Studio.
3. Olá janela do Console do Gerenciador de pacotes, definido Olá **projeto padrão** tooyour novo projeto de aplicativo de console e na janela de console hello, execute Olá comando a seguir:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Isso adiciona um toohello Referência SDK de Hubs de notificação do Azure usando Olá <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacote NuGet de Hubs Microsoft.Azure.Notification</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. Olá abrir `Program.cs` de arquivo e adicione o seguinte Olá `using` instrução, garantindo que podemos usar classes do Azure e funções em sua classe principal:
   
        using Microsoft.Azure.NotificationHubs;
5. No seu `Program` classe, adicione o seguinte método de saudação (não se esqueça de saudação tooreplace **cadeia de caracteres de conexão** e **nome do hub**):
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var alert = "{\"aps\":{\"alert\":\"Hello from .NET!\"}}";
            await hub.SendAppleNativeNotificationAsync(alert);
        }
6. Adicionar Olá seguintes linhas no seu `Main` método:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Pressione Olá F5 toorun chave Olá aplicativo. Em segundos, você verá uma notificação por push em seu dispositivo. Se você estiver usando o Wi-Fi ou uma rede de dados de celular, certifique-se de que você tenha uma conexão de internet ativa no dispositivo de saudação.

Você encontrará todas as cargas de possíveis Olá Olá Apple [Local e o guia de programação de notificação por Push].

#### <a name="optional-send-notifications-from-a-mobile-service"></a>(Opcional) Enviar Notificações de um Serviço Móvel
Nesta seção, enviaremos notificações por push usando um serviço móvel por meio de um script de nó.

toosend uma notificação por meio de um serviço móvel, siga [Introdução aos serviços móveis]e, em seguida:

1. Entrar toohello [Portal clássico do Azure]e selecione seu serviço móvel.
2. Selecione Olá **Agendador** guia na parte superior da saudação.
   
       ![Azure Classic Portal - Scheduler][215]
3. Crie um novo trabalho agendado, insira um nome e selecione **Sob demanda**.
   
       ![Azure Classic Portal - Create new job][216]
4. Quando o trabalho de saudação é criado, clique em nome do trabalho hello. Em seguida, clique em Olá **Script** guia na barra superior hello.
5. Inserir saudação script dentro de sua função de agendador a seguir. Verifique se tooreplace reservados Olá seu hub nome e hello conexão cadeia de notificação para *DefaultFullSharedAccessSignature* que você obteve anteriormente. Clique em **Salvar**.
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<Hubname>', '<SAS Full access >');
        notificationHubService.apns.send(
            null,
            {"aps":
                {
                  "alert": "Hello from Mobile Services!"
                }
            },
            function (error)
            {
                if (!error) {
                    console.warn("Notification successful");
                }
            }
        );
6. Clique em **executar uma vez** na barra inferior de saudação. Você deverá receber um alerta em seu dispositivo.

## <a name="next-steps"></a>Próximas etapas
Neste exemplo simples, você transmitida tooall de notificações por push seus dispositivos iOS. Em ordem tootarget usuários específicos, consulte o tutorial toohello [usar Hubs de notificação toopush notificações toousers]. Se você desejar toosegment os usuários, grupos de interesse, você pode ler [toosend de Hubs de notificação de uso últimas notícias]. Saiba mais sobre como Hubs de notificação toouse [orientação de Hubs de notificação] e em Olá [iOS Hubs de notificação como-toofor].

<!-- Images. -->

[213]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-console-app.png

[215]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler1.png
[216]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler2.png


[31]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-ios-app.png




<!-- URLs. -->
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Introdução aos serviços móveis]: /develop/mobile/tutorials/get-started-xamarin-ios
[Portal clássico do Azure]: https://manage.windowsazure.com/
[orientação de Hubs de notificação]: http://msdn.microsoft.com/library/jj927170.aspx
[iOS Hubs de notificação como-toofor]: http://msdn.microsoft.com/library/jj927168.aspx
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[usar Hubs de notificação toopush notificações toousers]: /manage/services/notification-hubs/notify-users-aspnet
[toosend de Hubs de notificação de uso últimas notícias]: /manage/services/notification-hubs/breaking-news-dotnet

[Local e o guia de programação de notificação por Push]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1
[Apple Push Notification Service]: http://go.microsoft.com/fwlink/p/?LinkId=272584

[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Xamarin Studio]: http://xamarin.com/download
[WindowsAzure.Messaging]: https://github.com/infosupport/WindowsAzure.Messaging.iOS
[Portal do Azure]: https://portal.azure.com
