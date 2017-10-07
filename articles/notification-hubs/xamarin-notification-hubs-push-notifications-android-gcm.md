---
title: "aaaGet iniciado com Hubs de notificação para aplicativos xamarin | Microsoft Docs"
description: "Neste tutorial, você aprenderá como toouse Hubs de notificação do Azure toosend envio notificações tooa aplicativo Xamarin Android."
author: ysxu
manager: erikre
editor: 
services: notification-hubs
documentationcenter: xamarin
ms.assetid: 0be600fe-d5f3-43a5-9e5e-3135c9743e54
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c5c7ead9a9381ab9fb6bbe86e930a8a9254813d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-with-xamarin-for-android"></a>Introdução aos Hubs de Notificação com o Xamarin para Android
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Visão geral
Este tutorial mostra como o aplicativo de xamarin tooa notificações de envio toouse toosend de Hubs de notificação do Azure.
Você criará um aplicativo Xamarin.Android em branco que recebe notificações por push usando o GCM(Google Cloud Messaging). Quando você terminar, você será capaz de toouse sua toobroadcast de hub de notificação por push notificações tooall Olá a dispositivos que executam seu aplicativo. Olá código concluído está disponível no hello [aplicativo hubs de notificação] [ GitHub] exemplo.

Este tutorial demonstra um cenário de difusão simples hello usando Hubs de notificação.

## <a name="before-you-begin"></a>Antes de começar
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

código de saudação concluído para este tutorial pode ser encontrado no GitHub [aqui](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).

## <a name="prerequisites"></a>Pré-requisitos
Este tutorial requer o seguinte hello:

* Visual Studio com Xamarin no Windows ou Xamarin Studio no Mac OS X. Encontre instruções de instalação completas em [Configuração e instalação para Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).
* Conta ativa do Google
* [Componente de mensagens do Azure]
* [Componente de mensagens de nuvem do Google]

A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais sobre Hubs de Notificação para aplicativos Xamarin.Android.

> [!IMPORTANT]
> toocomplete neste tutorial, você deve ter uma conta ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).
> 
> 

## <a name="enable-google-cloud-messaging"></a>Habilitar o sistema de mensagens em nuvem do Google
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-your-notification-hub"></a>Configurar seu Hub de Notificação
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li><p>Clique em Olá <b>configurar</b> guia na parte superior do hello, digite Olá <b>chave API</b> valor obtido na seção anterior hello e, em seguida, clique em <b>salvar</b>.</p>
</li>
</ol>
&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)

Hub de notificação agora é toowork configurado com GCM e ter tooboth de cadeias de caracteres de conexão Olá registrar seu notificações do aplicativo tooreceive e notificações por push de toosend.

## <a name="connect-your-app-toohello-notification-hub"></a>Conecte-se o seu hub de notificação do aplicativo toohello
### <a name="create-a-new-project"></a>Criar um novo projeto
1. No Xamarin Studio, clique em **Nova Solução**, clique em **Aplicativo Android** e clique em **Avançar**.
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project1.png)

2. Insira o **Nome do Aplicativo** e o **Identificador**. Clique em Olá **destino Plaforms** desejado toosupport e, em seguida, clique em **próximo** e **criar**.
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project2.png)

    Isso cria um novo projeto Android.

1. Abra as propriedades do projeto de saudação clicando duas vezes o seu novo projeto em Olá exibição de solução e escolha **opções**. Selecione Olá **aplicativo Android** item Olá **criar** seção.
   
    Certifique-se de que primeira letra de saudação do seu **nome do pacote** letras minúsculas constantemente.
   
   > [!IMPORTANT]
   > primeira letra de saudação do nome do pacote de saudação deve estar em minúscula. Caso contrário, você receberá erros de manifesto do aplicativo ao registrar **BroadcastReceiver** e **IntentFilter** para as notificações por push abaixo.
   > 
   > 
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub--xamarin-android-app-options.png)
2. Opcionalmente, o conjunto Olá **versão do Android mínimo** tooanother nível de API.
3. Opcionalmente, o conjunto Olá **versão destino Android** toohello outra versão de API que você deseja tootarget (deve ser o nível de API 8 ou superior).

Clique em **Okey** e caixa de diálogo de opções de projeto Olá fechar.

### <a name="add-hello-required-components-tooyour-project"></a>Adicionar projeto de tooyour Olá componentes necessários
Olá Google nuvem mensagens cliente disponíveis na Olá armazenamento do componente Xamarin simplifica o processo de saudação de suporte para notificações por push xamarin.

1. Clique em pasta de componentes de saudação no aplicativo xamarin e escolha **obter mais componentes**.
2. Pesquise Olá **mensagens do Azure** componente e adicioná-lo toohello projeto.
3. Pesquise Olá **cliente de mensagens de nuvem do Google** componente e adicioná-lo toohello projeto.

### <a name="set-up-notification-hubs-in-your-project"></a>Configurar hubs de notificação em seu projeto
1. Reúna Olá informações para o hub de notificação e o aplicativo Android a seguir:
   
   * **GoogleProjectNumber**: obter esse valor de número do projeto da visão geral de saudação do seu aplicativo no Portal do desenvolvedor do Google de saudação. Você anotou anteriormente, esse valor quando você criou o aplicativo hello no portal de saudação.
   * **Escutar a cadeia de caracteres de conexão**: no painel de saudação do hello [Portal clássico do Azure], clique em **exibir cadeias de caracteres de conexão**. Saudação de cópia *DefaultListenSharedAccessSignature* cadeia de caracteres de conexão para esse valor.
   * **O nome do hub**: Este é o nome de saudação do seu hub de saudação [Portal clássico do Azure]. Por exemplo, *mynotificationhub2*.
     
     Criar um **Constants.cs** de classe para o seu projeto Xamarin e definir Olá valores constantes na classe Olá a seguir. Substitua os espaços reservados de saudação com seus valores.
     
       public static class Constants   {
     
           public const string SenderID = "<GoogleProjectNumber>"; // Google API Project Number
           public const string ListenConnectionString = "<Listen connection string>";
           public const string NotificationHubName = "<hub name>";
       }
2. Adicione Olá seguinte usando instruções muito**MainActivity.cs**:
   
        using Android.Util;
        using Gcm.Client;
3. Adicionar um toohello de variável de instância `MainActivity` classe que será usado tooshow uma caixa de diálogo alerta quando o aplicativo hello está em execução:
   
        public static MainActivity instance;
4. Criar hello seguinte método em Olá **MainActivity** classe:
   
        private void RegisterWithGCM()
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);
   
            // Register for push notifications
            Log.Info("MainActivity", "Registering...");
            GcmClient.Register(this, Constants.SenderID);
        }
5. Em Olá `OnCreate` método **MainActivity.cs**, inicializar Olá `instance` variável e adicionar uma chamada muito`RegisterWithGCM`:
   
        protected override void OnCreate (Bundle bundle)
        {
            instance = this;
   
            base.OnCreate (bundle);
   
            // Set your view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);
   
            // Get your button from hello layout resource,
            // and attach an event tooit
            Button button = FindViewById<Button> (Resource.Id.myButton);
   
            RegisterWithGCM();
        }
6. Crie uma nova classe, **MyBroadcastReceiver**.
   
   > [!NOTE]
   > Mostraremos a criação de uma classe **BroadcastReceiver** desde o início. No entanto, um toomanually alternativo rápido criar **MyBroadcastReceiver.cs** é toorefer toohello **GcmService.cs** arquivo encontrado no projeto de xamarin do exemplo hello incluído com hello [Exemplos de hubs de notificação][GitHub]. Duplicando **GcmService.cs** e alterando os nomes de classe pode ser também um toostart ótimo lugar.
   > 
   > 
7. Adicione Olá seguinte usando instruções muito**MyBroadcastReceiver.cs** (referência de assembly que você adicionou anteriormente e componente toohello):
   
        using System.Collections.Generic;
        using System.Text;
        using Android.App;
        using Android.Content;
        using Android.Util;
        using Gcm.Client;
        using WindowsAzure.Messaging;
8. Em **MyBroadcastReceiver.cs**, adicionar Olá solicitações de permissão a seguir entre hello **usando** instruções e hello **namespace** declaração:
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is needed only for Android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
9. Em **MyBroadcastReceiver.cs**, alterar Olá **MyBroadcastReceiver** classe a seguir Olá toomatch:
   
        [BroadcastReceiver(Permission=Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        public class MyBroadcastReceiver : GcmBroadcastReceiverBase<PushHandlerService>
        {
            public static string[] SENDER_IDS = new string[] { Constants.SenderID };
   
            public const string TAG = "MyBroadcastReceiver-GCM";
        }
10. Adicione outra classe a **MyBroadcastReceiver.cs** chamada **PushHandlerService**, que deriva de **GcmServiceBase**. Verifique se Olá de tooapply **Service** toohello classe de atributo:
    
         [Service] // Must use hello service tag
         public class PushHandlerService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }
             private NotificationHub Hub { get; set; }
    
             public PushHandlerService() : base(Constants.SenderID)
                {
                 Log.Info(MyBroadcastReceiver.TAG, "PushHandlerService() constructor");
             }
         }
11. **GcmServiceBase** implementa os métodos **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()** e **OnError()**. Nosso **PushHandlerService** classe de implementação deve substituir esses métodos, e esses métodos serão acionado em resposta toointeracting com hub de notificação de saudação.
12. Substituir saudação **OnRegistered()** método **PushHandlerService** usando Olá código a seguir:
    
         protected override void OnRegistered(Context context, string registrationId)
         {
             Log.Verbose(MyBroadcastReceiver.TAG, "GCM Registered: " + registrationId);
             RegistrationID = registrationId;
    
             createNotification("PushHandlerService-GCM Registered...",
                                 "hello device has been Registered!");
    
             Hub = new NotificationHub(Constants.NotificationHubName, Constants.ListenConnectionString,
                                         context);
             try
             {
                 Hub.UnregisterAll(registrationId);
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
    
             //var tags = new List<string>() { "falcons" }; // create tags if you want
             var tags = new List<string>() {};
    
             try
             {
                 var hubRegistration = Hub.Register(registrationId, tags.ToArray());
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
         }
    
    > [!NOTE]
    > Em Olá **OnRegistered()** código acima, você deve observar Olá capacidade toospecify marcas tooregister de canais de mensagens específicos.
    > 
    > 
13. Substituir saudação **OnMessage** método **PushHandlerService** usando Olá código a seguir:
    
        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info(MyBroadcastReceiver.TAG, "GCM Message Received!");
    
            var msg = new StringBuilder();
    
            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }
    
            string messageText = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty (messageText))
            {
                createNotification ("New hub message!", messageText);
            }
            else
            {
                createNotification ("Unknown message details", msg.ToString ());
            }
        }
14. Adicione o seguinte Olá **createNotification** e **dialogNotify** métodos muito**PushHandlerService** para notificar os usuários quando a notificação é recebida.
    
    > [!NOTE]
    > O design de notificação no Android versão 5.0 e posterior teve uma mudança significativa das versões anteriores. Se você testar no Android 5.0 ou posterior, o aplicativo de saudação precisará toobe executar notificação de saudação tooreceive. Para obter mais informações, consulte [Notificações do Android](http://go.microsoft.com/fwlink/?LinkId=615880).
    > 
    > 
    
        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;
    
            //Create an intent tooshow UI
            var uiIntent = new Intent(this, typeof(MainActivity));
    
            //Create hello notification
            var notification = new Notification(Android.Resource.Drawable.SymActionEmail, title);
    
            //Auto-cancel will remove hello notification once hello user touches it
            notification.Flags = NotificationFlags.AutoCancel;
    
            //Set hello notification info
            //we use hello pending intent, passing our ui intent over, which will get called
            //when hello notification is tapped.
            notification.SetLatestEventInfo(this, title, desc, PendingIntent.GetActivity(this, 0, uiIntent, 0));
    
            //Show hello notification
            notificationManager.Notify(1, notification);
            dialogNotify (title, desc);
        }
    
        protected void dialogNotify(String title, String message)
        {
    
            MainActivity.instance.RunOnUiThread(() => {
                AlertDialog.Builder dlg = new AlertDialog.Builder(MainActivity.instance);
                AlertDialog alert = dlg.Create();
                alert.SetTitle(title);
                alert.SetButton("Ok", delegate {
                    alert.Dismiss();
                });
                alert.SetMessage(message);
                alert.Show();
            });
        }
15. Substitua os membros abstratos **OnUnRegistered()**, **OnRecoverableError()** e **OnError()** para que o código seja compilado:
    
        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Verbose(MyBroadcastReceiver.TAG, "GCM Unregistered: " + registrationId);
    
            createNotification("GCM Unregistered...", "hello device has been unregistered!");
        }
    
        protected override bool OnRecoverableError(Context context, string errorId)
        {
            Log.Warn(MyBroadcastReceiver.TAG, "Recoverable Error: " + errorId);
    
            return base.OnRecoverableError (context, errorId);
        }
    
        protected override void OnError(Context context, string errorId)
        {
            Log.Error(MyBroadcastReceiver.TAG, "GCM Error: " + errorId);
        }

## <a name="run-your-app-in-hello-emulator"></a>Executar seu aplicativo no emulador Olá
Se você executar esse aplicativo no emulador hello, certifique-se de que você use um dispositivo Virtual Android (AVD) que oferece suporte a APIs do Google.

> [!IMPORTANT]
> Em notificações de push de tooreceive ordem, você deve configurar uma conta do Google em seu dispositivo Virtual Android. (No emulador do Windows hello, navegue muito**configurações** e clique em **adicionar conta**.) Além disso, certifique-se de que emulador Olá é toohello conectado à Internet.
> 
> [!NOTE]
> O design de notificação no Android versão 5.0 e posterior teve uma mudança significativa das versões anteriores. Para obter mais informações, consulte [Notificações do Android](http://go.microsoft.com/fwlink/?LinkId=615880).
> 
> 

1. Em **Ferramentas**, clique em **Abrir Gerenciador de Emulador do Android**, selecione seu dispositivo e clique em **Editar**.
   
      ![][18]
2. Selecione **APIs do Google**, em **Destino** e clique em **OK**.
   
      ![][19]
3. Na barra de ferramentas superior hello, clique em **executar**e, em seguida, selecione seu aplicativo. Isso inicia o emulador hello e executa o aplicativo hello.
   
   aplicativo Hello recupera Olá *registrationId* do GCM e registra com o hub de notificação hello.

## <a name="send-notifications-from-your-backend"></a>Enviar notificações de seu back-end
Você pode testar a receber notificações em seu aplicativo pelo envio de notificações em Olá [Portal clássico do Azure] via Olá guia depuração no hub de notificação hello, conforme mostrado na tela hello abaixo.

![][30]

Normalmente, as notificações por push são enviadas em um serviço de back-end como os Serviços Móveis ou ASP.NET por meio de uma biblioteca compatível. Você também pode usar o hello API REST diretamente as mensagens de notificação de toosend se uma biblioteca não está disponível para seu back-end.

Aqui está uma lista de alguns outros tutoriais que você talvez queira tooreview para enviar notificações:

* ASP.NET: Consulte [usar Hubs de notificação toopush notificações toousers].
* Java de Hubs de notificação do Azure SDK: consulte [como toouse Hubs de notificação do Java](notification-hubs-java-push-notification-tutorial.md) para enviar notificações de Java. Isso foi testado no Eclipse para desenvolvimento no Android.
* PHP: Consulte [como toouse Hubs de notificação do PHP](notification-hubs-php-push-notification-tutorial.md).

Nas subseções próximas de saudação tutorial Olá, enviar notificações por meio de um aplicativo de console do .NET e usando um serviço móvel por meio de um script de nó.

#### <a name="optional-send-notifications-by-using-a-net-app"></a>(Opcional) Enviar notificações usando um aplicativo .NET
Nesta seção, enviaremos as notificações usando um aplicativo de console .NET

1. Crie um novo aplicativo de console do Visual C#:
   
      ![][20]
2. No Visual Studio, clique em **Ferramentas**, em **Gerenciador de Pacotes NuGet** e em **Console do Gerenciador de Pacotes**.
   
    Isso exibe o saudação Package Manager Console no Visual Studio.
3. Olá janela do Console do Gerenciador de pacotes, definido Olá **projeto padrão** tooyour novo projeto de aplicativo de console e na janela de console hello, execute Olá comando a seguir:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Isso adiciona um toohello Referência SDK de Hubs de notificação do Azure usando Olá <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacote NuGet de Hubs Microsoft.Azure.Notification</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. Abra o arquivo Program.cs de saudação e adicione o seguinte de saudação `using` instrução:
   
        using Microsoft.Azure.NotificationHubs;
5. No seu `Program` classe, adicione o seguinte método de saudação. Atualizar o texto de espaço reservado de saudação com seu *DefaultFullSharedAccessSignature* nome de hub e de cadeia de caracteres de conexão de saudação [Portal clássico do Azure].
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            await hub.SendGcmNativeNotificationAsync("{ \"data\" : {\"message\":\"Hello from Azure!\"}}");
        }
6. Adicionar Olá seguintes linhas no seu **principal** método:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Pressione Olá F5 toorun chave Olá aplicativo. Você deve receber uma notificação no aplicativo hello.
   
      ![][21]

#### <a name="optional-send-notifications-by-using-a-mobile-service"></a>(Opcional) Enviar notificações usando um serviço móvel
1. Acompanhe [Introdução aos Serviços Móveis].
2. Entrar toohello [Portal clássico do Azure]e selecione seu serviço móvel.
3. Selecione Olá **Agendador** guia na parte superior da saudação.
   
      ![][22]
4. Crie um novo trabalho agendado, insira um nome e selecione **Sob demanda**.
   
      ![][23]
5. Quando o trabalho de saudação é criado, clique em nome do trabalho hello. Em seguida, clique em Olá **Script** guia na barra superior hello.
6. Inserir saudação script dentro de sua função de agendador a seguir. Verifique se tooreplace reservados Olá seu hub nome e hello conexão cadeia de notificação para *DefaultFullSharedAccessSignature* que você obteve anteriormente. Clique em **Salvar**.
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string>');
        notificationHubService.gcm.send(null,'{"data":{"message" : "Hello from Mobile Services!"}}',
          function (error)
          {
            if (!error) {
               console.warn("Notification successful");
            }
            else
            {
              console.warn("Notification failed" + error);
            }
          }
        );
7. Clique em **executar uma vez** na barra inferior de saudação. Você deve receber uma notificação do sistema.

## <a name="next-steps"></a>Próximas etapas
Neste exemplo simples, você transmitida notificações tooall seus dispositivos Android. Em ordem tootarget usuários específicos, consulte o tutorial toohello [usar Hubs de notificação toopush notificações toousers]. Se você desejar toosegment os usuários, grupos de interesse, você pode ler [toosend de Hubs de notificação de uso últimas notícias]. Saiba mais sobre como Hubs de notificação toouse [orientação de Hubs de notificação] e em Olá [Hubs de notificação como toofor Android].

<!-- Anchors. -->
[Enable Google Cloud Messaging]: #register
[Configure your Notification Hub]: #configure-hub
[Connecting your app toohello Notification Hub]: #connecting-app
[Run your app with hello emulator]: #run-app
[Send notifications from your back-end]: #send
[Next steps]:#next-steps

<!-- Images. -->

[11]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-configure-android.png

[13]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app1.png
[15]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app3.png

[18]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app7.png
[19]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app8.png

[20]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-android-toast.png
[22]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler2.png

[30]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png


<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Introdução aos Serviços Móveis]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[Portal clássico do Azure]: https://manage.windowsazure.com/
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[orientação de Hubs de notificação]: http://msdn.microsoft.com/library/jj927170.aspx
[Hubs de notificação como toofor Android]: http://msdn.microsoft.com/library/dn282661.aspx

[usar Hubs de notificação toopush notificações toousers]: /manage/services/notification-hubs/notify-users-aspnet
[toosend de Hubs de notificação de uso últimas notícias]: /manage/services/notification-hubs/breaking-news-dotnet
[GCMClient Component page]: http://components.xamarin.com/view/GCMClient
[Xamarin.NotificationHub GitHub page]: https://github.com/SaschaDittmann/Xamarin.NotificationHub
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Componente de mensagens de nuvem do Google]: http://components.xamarin.com/view/GCMClient/
[Componente de mensagens do Azure]: http://components.xamarin.com/view/azure-messaging
