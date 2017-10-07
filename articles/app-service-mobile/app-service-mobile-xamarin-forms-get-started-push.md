---
title: "aaaAdd push notificações tooyour xamarin. Forms aplicativo | Microsoft Docs"
description: "Saiba como toouse do Azure services toosend push multiplataforma notificações tooyour xamarin. Forms aplicativos."
services: app-service\mobile
documentationcenter: xamarin
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: d9b1ba9a-b3f2-4d12-affc-2ee34311538b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: 9133a0b6dd99c01def525607c20ce5a9c19b9502
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinforms-app"></a>Adicionar aplicativo do envio notificações tooyour xamarin. Forms
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Visão geral
Neste tutorial, você adicionar projetos Olá de tooall de notificações de envio que resultaram de saudação [início rápido do xamarin. Forms](app-service-mobile-xamarin-forms-get-started.md). Isso significa que uma notificação por push é enviada a clientes de plataforma cruzada tooall toda vez que um registro é inserido.

Se você não usar Olá baixar o projeto de servidor de início rápido, será necessário Olá o pacote de extensão de notificação por push. Para obter mais informações, consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="prerequisites"></a>Pré-requisitos
Para o iOS, você precisará de uma [associação ao Programa do Desenvolvedor da Apple](https://developer.apple.com/programs/ios/) e um dispositivo iOS físico. Olá [simulador iOS não dá suporte a notificações por push](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).

## <a name="configure-hub"></a>Configurar um Hub de Notificação
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a>Olá servidor projeto toosend push notificações de atualização
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-and-run-hello-android-project-optional"></a>Configurar e executar o projeto Android da saudação (opcional)
Conclua esta seção tooenable as notificações por push para Olá xamarin. Forms Droid projeto para o Android.

### <a name="enable-firebase-cloud-messaging-fcm"></a>Habilitar FCM (mensagens de nuvem Firebase)
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

### <a name="configure-hello-mobile-apps-back-end-toosend-push-requests-by-using-fcm"></a>Configurar solicitações de envio por push do hello aplicativos móveis back-end toosend usando FCM
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

### <a name="add-push-notifications-toohello-android-project"></a>Adicionar notificações de push toohello projeto Android
Com hello back-end configurada com FCM, você pode adicionar componentes e códigos de toohello tooregister de cliente com FCM. Você também pode registrar para notificações de push com Hubs de notificação do Azure por meio de saudação novamente os aplicativos móveis terminar e receber notificações.

1. Em Olá **Droid** de projeto, clique com botão direito Olá **componentes** pasta e clique em **obter mais componentes...** . Em seguida, procure Olá **cliente de mensagens de nuvem do Google** componente e adicioná-lo toohello projeto. Esse componente oferece suporte a notificações por push para um projeto Android Xamarin.
2. Abrir o arquivo de projeto MainActivity.cs hello e adicione Olá após a instrução na parte superior de saudação do arquivo hello:

        using Gcm.Client;
3. Adicionar Olá toohello de código a seguir **OnCreate** muito da chamada do método após Olá**LoadApplication**:

        try
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);

            // Register for push notifications
            System.Diagnostics.Debug.WriteLine("Registering...");
            GcmClient.Register(this, PushHandlerBroadcastReceiver.SENDER_IDS);
        }
        catch (Java.Net.MalformedURLException)
        {
            CreateAndShowDialog("There was an error creating hello client. Verify hello URL.", "Error");
        }
        catch (Exception e)
        {
            CreateAndShowDialog(e.Message, "Error");
        }
4. Adicione um novo método auxiliar **CreateAndShowDialog** , desta maneira:

        private void CreateAndShowDialog(String message, String title)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);

            builder.SetMessage (message);
            builder.SetTitle (title);
            builder.Create().Show ();
        }
5. Adicionar Olá toohello de código a seguir **MainActivity** classe:

        // Create a new instance field for this activity.
        static MainActivity instance = null;

        // Return hello current activity instance.
        public static MainActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }

    Isso expõe Olá atual **MainActivity** instância, portanto, pode ser executado no thread de interface do usuário principal de saudação.
6. Inicializar Olá `instance` variável no início de saudação do hello **OnCreate** método, da seguinte maneira.

        // Set hello current instance of MainActivity.
        instance = this;
7. Adicionar um novo arquivo toohello da classe **Droid** projeto chamado `GcmService.cs`e certifique-se de seguir de Olá **usando** instruções estão presentes na parte superior de saudação do arquivo hello:

        using Android.App;
        using Android.Content;
        using Android.Media;
        using Android.Support.V4.App;
        using Android.Util;
        using Gcm.Client;
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Text;
8. Adicionar Olá seguindo as solicitações de permissão na parte superior de saudação do arquivo hello, após a saudação **usando** instruções e antes de saudação **namespace** declaração.

        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
9. Adicione Olá toohello namespace de definição de classe a seguir.

       [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, Categories = new string[] { "@PACKAGE_NAME@" })]
       public class PushHandlerBroadcastReceiver : GcmBroadcastReceiverBase<GcmService>
       {
           public static string[] SENDER_IDS = new string[] { "<PROJECT_NUMBER>" };
       }

   > [!NOTE]
   > Substitua **<PROJECT_NUMBER>** pelo número do projeto que você anotou anteriormente.    
   >
   >
10. Substituir saudação vazia **GcmService** classe com hello código que usa o receptor de difusão novo Olá a seguir:

         [Service]
         public class GcmService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }

             public GcmService()
                 : base(PushHandlerBroadcastReceiver.SENDER_IDS){}
         }
11. Adicionar Olá toohello de código a seguir **GcmService** classe. Isso substitui Olá **OnRegistered** manipulador de eventos e implementa uma **registrar** método.

        protected override void OnRegistered(Context context, string registrationId)
        {
            Log.Verbose("PushHandlerBroadcastReceiver", "GCM Registered: " + registrationId);
            RegistrationID = registrationId;

            var push = TodoItemManager.DefaultManager.CurrentClient.GetPush();

            MainActivity.CurrentActivity.RunOnUiThread(() => Register(push, null));
        }

        public async void Register(Microsoft.WindowsAzure.MobileServices.Push push, IEnumerable<string> tags)
        {
            try
            {
                const string templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";

                JObject templates = new JObject();
                templates["genericMessage"] = new JObject
                {
                    {"body", templateBodyGCM}
                };

                await push.RegisterAsync(RegistrationID, templates);
                Log.Info("Push Installation Id", push.InstallationId.ToString());
            }
            catch (Exception ex)
            {
                System.Diagnostics.Debug.WriteLine(ex.Message);
                Debugger.Break();
            }
        }

    Observe que esse código usa Olá `messageParam` parâmetro no registro do modelo de saudação.
12. Adicionar Olá código que implementa a seguir **OnMessage**:

        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info("PushHandlerBroadcastReceiver", "GCM Message Received!");

            var msg = new StringBuilder();

            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }

            //Store hello message
            var prefs = GetSharedPreferences(context.PackageName, FileCreationMode.Private);
            var edit = prefs.Edit();
            edit.PutString("last_msg", msg.ToString());
            edit.Commit();

            string message = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty(message))
            {
                createNotification("New todo item!", "Todo item: " + message);
                return;
            }

            string msg2 = intent.Extras.GetString("msg");
            if (!string.IsNullOrEmpty(msg2))
            {
                createNotification("New hub message!", msg2);
                return;
            }

            createNotification("Unknown message details", msg.ToString());
        }

        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;

            //Create an intent tooshow ui
            var uiIntent = new Intent(this, typeof(MainActivity));

            //Use Notification Builder
            NotificationCompat.Builder builder = new NotificationCompat.Builder(this);

            //Create hello notification
            //we use hello pending intent, passing our ui intent over which will get called
            //when hello notification is tapped.
            var notification = builder.SetContentIntent(PendingIntent.GetActivity(this, 0, uiIntent, 0))
                    .SetSmallIcon(Android.Resource.Drawable.SymActionEmail)
                    .SetTicker(title)
                    .SetContentTitle(title)
                    .SetContentText(desc)

                    //Set hello notification sound
                    .SetSound(RingtoneManager.GetDefaultUri(RingtoneType.Notification))

                    //Auto cancel will remove hello notification once hello user touches it
                    .SetAutoCancel(true).Build();

            //Show hello notification
            notificationManager.Notify(1, notification);
        }

    Isso controla notificações recebidas e as envia toohello toobe de Gerenciador de notificação exibida.
13. **GcmServiceBase** também requer que você Olá tooimplement **OnUnRegistered** e **OnError** métodos do manipulador, que pode ser feito da seguinte maneira:

        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "Unregistered RegisterationId : " + registrationId);
        }

        protected override void OnError(Context context, string errorId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "GCM Error: " + errorId);
        }

Agora, você está pronto teste notificações por push no aplicativo hello em execução em um dispositivo Android ou Olá emulador.

### <a name="test-push-notifications-in-your-android-app"></a>Testar notificações por push em seu aplicativo Android
Olá primeiras duas etapas são necessárias somente quando você estiver testando em um emulador.

1. Certifique-se de que você está implantando tooor depuração em um dispositivo virtual que tem a APIs do Google definido como destino hello, conforme mostrado abaixo no Gerenciador de dispositivo Virtual Android hello.
2. Adicionar um dispositivo Android do Google conta toohello clicando **aplicativos** > **configurações** > **adicionar conta**. Em seguida, siga Olá prompts tooadd um dispositivo de toohello de conta existente do Google ou toocreate um novo.
3. No Visual Studio ou no Xamarin Studio, clique com botão direito Olá **Droid** do projeto e clique em **definir como projeto de inicialização**.
4. Clique em **executar** toobuild Olá projeto e iniciar o aplicativo hello no emulador ou dispositivo Android.
5. No aplicativo hello, digite uma tarefa e, em seguida, clique em Olá adição (**+**) ícone.
6. Verifique se uma notificação é recebida quando um item é adicionado.

## <a name="configure-and-run-hello-ios-project-optional"></a>Configurar e executar o projeto iOS da saudação (opcional)
Esta seção é para executar o projeto do hello Xamarin iOS para dispositivos iOS. Você poderá ignorá-la se não estiver trabalhando com dispositivos iOS.

[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

#### <a name="configure-hello-notification-hub-for-apns"></a>Configurar o hub de notificação de saudação APNS
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

Em seguida, você irá configurar a configuração de projeto do iOS de saudação no Xamarin Studio ou Visual Studio.

[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

#### <a name="add-push-notifications-tooyour-ios-app"></a>Adicionar aplicativo do iOS de tooyour de notificações de push
1. Em Olá **iOS** de projeto, abra appdelegate. cs e adicionar Olá superior de toohello instrução saudação do arquivo de código a seguir.

        using Newtonsoft.Json.Linq;
2. Em Olá **AppDelegate** da classe, adicione uma substituição para Olá **RegisteredForRemoteNotifications** tooregister de eventos para notificações:

        public override void RegisteredForRemoteNotifications(UIApplication application,
            NSData deviceToken)
        {
            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
                {
                  {"body", templateBodyAPNS}
                };

            // Register for push with your mobile app
            Push push = TodoItemManager.DefaultManager.CurrentClient.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }
3. Em **AppDelegate**, também adicionar Olá após a substituição de saudação **DidReceiveRemoteNotification** manipulador de eventos:

        public override void DidReceiveRemoteNotification(UIApplication application,
            NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;

            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps[new NSString("alert")] as NSString).ToString();

            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

    Esse método manipula notificações recebidas enquanto o aplicativo hello está sendo executado.
4. Em Olá **AppDelegate** de classe, adicione Olá toohello de código a seguir **FinishedLaunching** método:

        // Register for push notifications.
        var settings = UIUserNotificationSettings.GetSettingsForTypes(
            UIUserNotificationType.Alert
            | UIUserNotificationType.Badge
            | UIUserNotificationType.Sound,
            new NSSet());

        UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
        UIApplication.SharedApplication.RegisterForRemoteNotifications();

    Isso habilita o suporte para notificações remotas e solicitações de registro por push.

Seu aplicativo agora está atualizada toosupport notificações de envio.

#### <a name="test-push-notifications-in-your-ios-app"></a>Testar notificações por push em seu aplicativo iOS
1. Clique com botão direito Olá iOS e, em seguida, clique em **definir como projeto de inicialização**.
2. Olá pressione **executar** botão ou **F5** no Visual Studio toobuild Olá projeto e iniciar o aplicativo hello em um dispositivo iOS. Em seguida, clique em **Okey** tooaccept as notificações de envio.

   > [!NOTE]
   > Você deve aceitar explicitamente as notificações por push do seu aplicativo. Essa solicitação ocorre apenas Olá Olá aplicativo será executado pela primeira vez.
   >
   >
3. No aplicativo hello, digite uma tarefa e, em seguida, clique em Olá adição (**+**) ícone.
4. Verifique se uma notificação é recebida e, em seguida, clique em **Okey** toodismiss Olá notificação.

## <a name="configure-and-run-windows-projects-optional"></a>Configurar e executar projetos do Windows (opcional)
Esta seção é para executar Olá WinApp xamarin. Forms e WinPhone81 projetos para dispositivos Windows. Estas etapas também oferecem suporte a projetos da Plataforma Universal do Windows (UWP). Você poderá ignorá-la se não estiver trabalhando com dispositivos Windows.

#### <a name="register-your-windows-app-for-push-notifications-with-windows-notification-service-wns"></a>Registrar o aplicativo Windows para receber notificações por push com o WNS (Serviço de Notificação do Windows)
[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

#### <a name="configure-hello-notification-hub-for-wns"></a>Configurar o hub de notificação Olá para o WNS
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="add-push-notifications-tooyour-windows-app"></a>Adicionar aplicativo do Windows de tooyour de notificações de push
1. No Visual Studio, abra **App.xaml.cs** em uma janela do projeto e adicionar Olá instruções a seguir.

        using Newtonsoft.Json.Linq;
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
        using <your_TodoItemManager_portable_class_namespace>;

    Substituir `<your_TodoItemManager_portable_class_namespace>` com o namespace de saudação do seu projeto portátil que contém Olá `TodoItemManager` classe.
2. Em App.xaml.cs, adicione o seguinte de saudação **InitNotificationsAsync** método:

        private async Task InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            const string templateBodyWNS =
                "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";

            JObject headers = new JObject();
            headers["X-WNS-Type"] = "wns/toast";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyWNS},
                {"headers", headers} // Needed for WNS.
            };

            await TodoItemManager.DefaultManager.CurrentClient.GetPush()
                .RegisterAsync(channel.Uri, templates);
        }

    Esse método obtém o canal de notificação por push hello e registra as notificações de modelo de tooreceive um modelo de hub de notificação. Uma notificação de modelo que oferece suporte a *messageParam* toothis cliente será entregue.
3. Em App.xaml.cs, atualizar Olá **OnLaunched** definição de método de manipulador de eventos adicionando Olá `async` modificador. Em seguida, adicione Olá a seguinte linha de código no final de saudação do método hello:

        await InitNotificationsAsync();

    Isso garante que o registro de notificação por push Olá é criado ou atualizado sempre que o aplicativo hello é iniciado. É importante toodo este tooguarantee que Olá WNS push canal está sempre ativa.  
4. No Gerenciador de soluções do Visual Studio, abra Olá **Package. appxmanifest** arquivo e defina **compatíveis com notificação do sistema** muito**Sim** em **notificações**.
5. Criar aplicativo hello e verifique se que você tem sem erros. Seu aplicativo cliente agora deve registrar para notificações do modelo de saudação do hello que terminar de volta a aplicativos móveis. Repita esta seção para cada projeto do Windows em sua solução.

#### <a name="test-push-notifications-in-your-windows-app"></a>Testar as notificações por push em seu aplicativo para Windows
1. No Visual Studio, clique com o botão direito do mouse no projeto do Windows e clique em **Definir como projeto de inicialização**.
2. Olá pressione **executar** botão projeto de saudação toobuild e iniciar o aplicativo hello.
3. No aplicativo hello, digite um nome para um novo todoitem e, em seguida, clique em Olá adição (**+**) ícone tooadd-lo.
4. Verifique se que uma notificação é recebida quando Olá item é adicionado.

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre as notificações por push:

* [Diagnosticar problemas com notificações por push](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  há vários motivos por que as notificações podem ser abandonadas ou não irem terminar nos dispositivos. Este tópico mostra como tooanalyze e descobrir raiz Olá causam falhas de notificação por push.

Você também pode continuar em tooone de saudação tutoriais a seguir:

* [Adicionar autenticação tooyour aplicativo](app-service-mobile-xamarin-forms-get-started-users.md)  
  Saiba como tooauthenticate usuários do seu aplicativo com um provedor de identidade.
* [Habilitar sincronização offline para seu aplicativo](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  Saiba como tooadd de suporte off-line para seu aplicativo usando um aplicativos móveis do back-end. Com a sincronização offline, os usuários podem interagir com um aplicativo móvel &mdash; exibindo, adicionando ou modificando dados &mdash; mesmo quando não há nenhuma conexão de rede.

<!-- Images. -->

<!-- URLs. -->
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Xcode]: https://go.microsoft.com/fwLink/?LinkID=266532
[apns object]: http://go.microsoft.com/fwlink/p/?LinkId=272333
