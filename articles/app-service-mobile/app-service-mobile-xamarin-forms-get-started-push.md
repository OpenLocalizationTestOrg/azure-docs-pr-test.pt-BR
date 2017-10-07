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
# <a name="add-push-notifications-tooyour-xamarinforms-app"></a><span data-ttu-id="68048-103">Adicionar aplicativo do envio notificações tooyour xamarin. Forms</span><span class="sxs-lookup"><span data-stu-id="68048-103">Add push notifications tooyour Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="68048-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="68048-104">Overview</span></span>
<span data-ttu-id="68048-105">Neste tutorial, você adicionar projetos Olá de tooall de notificações de envio que resultaram de saudação [início rápido do xamarin. Forms](app-service-mobile-xamarin-forms-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="68048-105">In this tutorial, you add push notifications tooall hello projects that resulted from hello [Xamarin.Forms quick start](app-service-mobile-xamarin-forms-get-started.md).</span></span> <span data-ttu-id="68048-106">Isso significa que uma notificação por push é enviada a clientes de plataforma cruzada tooall toda vez que um registro é inserido.</span><span class="sxs-lookup"><span data-stu-id="68048-106">This means that a push notification is sent tooall cross-platform clients every time a record is inserted.</span></span>

<span data-ttu-id="68048-107">Se você não usar Olá baixar o projeto de servidor de início rápido, será necessário Olá o pacote de extensão de notificação por push.</span><span class="sxs-lookup"><span data-stu-id="68048-107">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="68048-108">Para obter mais informações, consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="68048-108">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68048-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="68048-109">Prerequisites</span></span>
<span data-ttu-id="68048-110">Para o iOS, você precisará de uma [associação ao Programa do Desenvolvedor da Apple](https://developer.apple.com/programs/ios/) e um dispositivo iOS físico.</span><span class="sxs-lookup"><span data-stu-id="68048-110">For iOS, you will need an [Apple Developer Program membership](https://developer.apple.com/programs/ios/) and a physical iOS device.</span></span> <span data-ttu-id="68048-111">Olá [simulador iOS não dá suporte a notificações por push](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="68048-111">hello [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span>

## <span data-ttu-id="68048-112"><a name="configure-hub"></a>Configurar um Hub de Notificação</span><span class="sxs-lookup"><span data-stu-id="68048-112"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a><span data-ttu-id="68048-113">Olá servidor projeto toosend push notificações de atualização</span><span class="sxs-lookup"><span data-stu-id="68048-113">Update hello server project toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-and-run-hello-android-project-optional"></a><span data-ttu-id="68048-114">Configurar e executar o projeto Android da saudação (opcional)</span><span class="sxs-lookup"><span data-stu-id="68048-114">Configure and run hello Android project (optional)</span></span>
<span data-ttu-id="68048-115">Conclua esta seção tooenable as notificações por push para Olá xamarin. Forms Droid projeto para o Android.</span><span class="sxs-lookup"><span data-stu-id="68048-115">Complete this section tooenable push notifications for hello Xamarin.Forms Droid project for Android.</span></span>

### <a name="enable-firebase-cloud-messaging-fcm"></a><span data-ttu-id="68048-116">Habilitar FCM (mensagens de nuvem Firebase)</span><span class="sxs-lookup"><span data-stu-id="68048-116">Enable Firebase Cloud Messaging (FCM)</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

### <a name="configure-hello-mobile-apps-back-end-toosend-push-requests-by-using-fcm"></a><span data-ttu-id="68048-117">Configurar solicitações de envio por push do hello aplicativos móveis back-end toosend usando FCM</span><span class="sxs-lookup"><span data-stu-id="68048-117">Configure hello Mobile Apps back end toosend push requests by using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

### <a name="add-push-notifications-toohello-android-project"></a><span data-ttu-id="68048-118">Adicionar notificações de push toohello projeto Android</span><span class="sxs-lookup"><span data-stu-id="68048-118">Add push notifications toohello Android project</span></span>
<span data-ttu-id="68048-119">Com hello back-end configurada com FCM, você pode adicionar componentes e códigos de toohello tooregister de cliente com FCM.</span><span class="sxs-lookup"><span data-stu-id="68048-119">With hello back end configured with FCM, you can add components and codes toohello client tooregister with FCM.</span></span> <span data-ttu-id="68048-120">Você também pode registrar para notificações de push com Hubs de notificação do Azure por meio de saudação novamente os aplicativos móveis terminar e receber notificações.</span><span class="sxs-lookup"><span data-stu-id="68048-120">You can also register for push notifications with Azure Notification Hubs through hello Mobile Apps back end, and receive notifications.</span></span>

1. <span data-ttu-id="68048-121">Em Olá **Droid** de projeto, clique com botão direito Olá **componentes** pasta e clique em **obter mais componentes...** . Em seguida, procure Olá **cliente de mensagens de nuvem do Google** componente e adicioná-lo toohello projeto.</span><span class="sxs-lookup"><span data-stu-id="68048-121">In hello **Droid** project, right-click hello **Components** folder, and click **Get More Components...**. Then search for hello **Google Cloud Messaging Client** component and add it toohello project.</span></span> <span data-ttu-id="68048-122">Esse componente oferece suporte a notificações por push para um projeto Android Xamarin.</span><span class="sxs-lookup"><span data-stu-id="68048-122">This component supports push notifications for a Xamarin Android project.</span></span>
2. <span data-ttu-id="68048-123">Abrir o arquivo de projeto MainActivity.cs hello e adicione Olá após a instrução na parte superior de saudação do arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="68048-123">Open hello MainActivity.cs project file, and add hello following statement at hello top of hello file:</span></span>

        using Gcm.Client;
3. <span data-ttu-id="68048-124">Adicionar Olá toohello de código a seguir **OnCreate** muito da chamada do método após Olá**LoadApplication**:</span><span class="sxs-lookup"><span data-stu-id="68048-124">Add hello following code toohello **OnCreate** method after hello call too**LoadApplication**:</span></span>

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
4. <span data-ttu-id="68048-125">Adicione um novo método auxiliar **CreateAndShowDialog** , desta maneira:</span><span class="sxs-lookup"><span data-stu-id="68048-125">Add a new **CreateAndShowDialog** helper method, as follows:</span></span>

        private void CreateAndShowDialog(String message, String title)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);

            builder.SetMessage (message);
            builder.SetTitle (title);
            builder.Create().Show ();
        }
5. <span data-ttu-id="68048-126">Adicionar Olá toohello de código a seguir **MainActivity** classe:</span><span class="sxs-lookup"><span data-stu-id="68048-126">Add hello following code toohello **MainActivity** class:</span></span>

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

    <span data-ttu-id="68048-127">Isso expõe Olá atual **MainActivity** instância, portanto, pode ser executado no thread de interface do usuário principal de saudação.</span><span class="sxs-lookup"><span data-stu-id="68048-127">This exposes hello current **MainActivity** instance, so we can execute on hello main UI thread.</span></span>
6. <span data-ttu-id="68048-128">Inicializar Olá `instance` variável no início de saudação do hello **OnCreate** método, da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="68048-128">Initialize hello `instance` variable at hello beginning of hello **OnCreate** method, as follows.</span></span>

        // Set hello current instance of MainActivity.
        instance = this;
7. <span data-ttu-id="68048-129">Adicionar um novo arquivo toohello da classe **Droid** projeto chamado `GcmService.cs`e certifique-se de seguir de Olá **usando** instruções estão presentes na parte superior de saudação do arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="68048-129">Add a new class file toohello **Droid** project named `GcmService.cs`, and make sure hello following **using** statements are present at hello top of hello file:</span></span>

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
8. <span data-ttu-id="68048-130">Adicionar Olá seguindo as solicitações de permissão na parte superior de saudação do arquivo hello, após a saudação **usando** instruções e antes de saudação **namespace** declaração.</span><span class="sxs-lookup"><span data-stu-id="68048-130">Add hello following permission requests at hello top of hello file, after hello **using** statements and before hello **namespace** declaration.</span></span>

        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
9. <span data-ttu-id="68048-131">Adicione Olá toohello namespace de definição de classe a seguir.</span><span class="sxs-lookup"><span data-stu-id="68048-131">Add hello following class definition toohello namespace.</span></span>

       [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, Categories = new string[] { "@PACKAGE_NAME@" })]
       public class PushHandlerBroadcastReceiver : GcmBroadcastReceiverBase<GcmService>
       {
           public static string[] SENDER_IDS = new string[] { "<PROJECT_NUMBER>" };
       }

   > [!NOTE]
   > <span data-ttu-id="68048-132">Substitua **<PROJECT_NUMBER>** pelo número do projeto que você anotou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="68048-132">Replace **<PROJECT_NUMBER>** with your project number you noted earlier.</span></span>    
   >
   >
10. <span data-ttu-id="68048-133">Substituir saudação vazia **GcmService** classe com hello código que usa o receptor de difusão novo Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="68048-133">Replace hello empty **GcmService** class with hello following code, which uses hello new broadcast receiver:</span></span>

         [Service]
         public class GcmService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }

             public GcmService()
                 : base(PushHandlerBroadcastReceiver.SENDER_IDS){}
         }
11. <span data-ttu-id="68048-134">Adicionar Olá toohello de código a seguir **GcmService** classe.</span><span class="sxs-lookup"><span data-stu-id="68048-134">Add hello following code toohello **GcmService** class.</span></span> <span data-ttu-id="68048-135">Isso substitui Olá **OnRegistered** manipulador de eventos e implementa uma **registrar** método.</span><span class="sxs-lookup"><span data-stu-id="68048-135">This overrides hello **OnRegistered** event handler and implements a **Register** method.</span></span>

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

    <span data-ttu-id="68048-136">Observe que esse código usa Olá `messageParam` parâmetro no registro do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="68048-136">Note that this code uses hello `messageParam` parameter in hello template registration.</span></span>
12. <span data-ttu-id="68048-137">Adicionar Olá código que implementa a seguir **OnMessage**:</span><span class="sxs-lookup"><span data-stu-id="68048-137">Add hello following code that implements **OnMessage**:</span></span>

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

    <span data-ttu-id="68048-138">Isso controla notificações recebidas e as envia toohello toobe de Gerenciador de notificação exibida.</span><span class="sxs-lookup"><span data-stu-id="68048-138">This handles incoming notifications and sends them toohello notification manager toobe displayed.</span></span>
13. <span data-ttu-id="68048-139">**GcmServiceBase** também requer que você Olá tooimplement **OnUnRegistered** e **OnError** métodos do manipulador, que pode ser feito da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="68048-139">**GcmServiceBase** also requires you tooimplement hello **OnUnRegistered** and **OnError** handler methods, which you can do as follows:</span></span>

        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "Unregistered RegisterationId : " + registrationId);
        }

        protected override void OnError(Context context, string errorId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "GCM Error: " + errorId);
        }

<span data-ttu-id="68048-140">Agora, você está pronto teste notificações por push no aplicativo hello em execução em um dispositivo Android ou Olá emulador.</span><span class="sxs-lookup"><span data-stu-id="68048-140">Now, you are ready test push notifications in hello app running on an Android device or hello emulator.</span></span>

### <a name="test-push-notifications-in-your-android-app"></a><span data-ttu-id="68048-141">Testar notificações por push em seu aplicativo Android</span><span class="sxs-lookup"><span data-stu-id="68048-141">Test push notifications in your Android app</span></span>
<span data-ttu-id="68048-142">Olá primeiras duas etapas são necessárias somente quando você estiver testando em um emulador.</span><span class="sxs-lookup"><span data-stu-id="68048-142">hello first two steps are required only when you're testing on an emulator.</span></span>

1. <span data-ttu-id="68048-143">Certifique-se de que você está implantando tooor depuração em um dispositivo virtual que tem a APIs do Google definido como destino hello, conforme mostrado abaixo no Gerenciador de dispositivo Virtual Android hello.</span><span class="sxs-lookup"><span data-stu-id="68048-143">Make sure that you are deploying tooor debugging on a virtual device that has Google APIs set as hello target, as shown below in hello Android Virtual Device manager.</span></span>
2. <span data-ttu-id="68048-144">Adicionar um dispositivo Android do Google conta toohello clicando **aplicativos** > **configurações** > **adicionar conta**.</span><span class="sxs-lookup"><span data-stu-id="68048-144">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**.</span></span> <span data-ttu-id="68048-145">Em seguida, siga Olá prompts tooadd um dispositivo de toohello de conta existente do Google ou toocreate um novo.</span><span class="sxs-lookup"><span data-stu-id="68048-145">Then follow hello prompts tooadd an existing Google account toohello device, or toocreate a new one.</span></span>
3. <span data-ttu-id="68048-146">No Visual Studio ou no Xamarin Studio, clique com botão direito Olá **Droid** do projeto e clique em **definir como projeto de inicialização**.</span><span class="sxs-lookup"><span data-stu-id="68048-146">In Visual Studio or Xamarin Studio, right-click hello **Droid** project and click **Set as startup project**.</span></span>
4. <span data-ttu-id="68048-147">Clique em **executar** toobuild Olá projeto e iniciar o aplicativo hello no emulador ou dispositivo Android.</span><span class="sxs-lookup"><span data-stu-id="68048-147">Click **Run** toobuild hello project and start hello app on your Android device or emulator.</span></span>
5. <span data-ttu-id="68048-148">No aplicativo hello, digite uma tarefa e, em seguida, clique em Olá adição (**+**) ícone.</span><span class="sxs-lookup"><span data-stu-id="68048-148">In hello app, type a task, and then click hello plus (**+**) icon.</span></span>
6. <span data-ttu-id="68048-149">Verifique se uma notificação é recebida quando um item é adicionado.</span><span class="sxs-lookup"><span data-stu-id="68048-149">Verify that a notification is received when an item is added.</span></span>

## <a name="configure-and-run-hello-ios-project-optional"></a><span data-ttu-id="68048-150">Configurar e executar o projeto iOS da saudação (opcional)</span><span class="sxs-lookup"><span data-stu-id="68048-150">Configure and run hello iOS project (optional)</span></span>
<span data-ttu-id="68048-151">Esta seção é para executar o projeto do hello Xamarin iOS para dispositivos iOS.</span><span class="sxs-lookup"><span data-stu-id="68048-151">This section is for running hello Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="68048-152">Você poderá ignorá-la se não estiver trabalhando com dispositivos iOS.</span><span class="sxs-lookup"><span data-stu-id="68048-152">You can skip this section if you are not working with iOS devices.</span></span>

[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

#### <a name="configure-hello-notification-hub-for-apns"></a><span data-ttu-id="68048-153">Configurar o hub de notificação de saudação APNS</span><span class="sxs-lookup"><span data-stu-id="68048-153">Configure hello notification hub for APNS</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

<span data-ttu-id="68048-154">Em seguida, você irá configurar a configuração de projeto do iOS de saudação no Xamarin Studio ou Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="68048-154">Next, you will configure hello iOS project setting in Xamarin Studio or Visual Studio.</span></span>

[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

#### <a name="add-push-notifications-tooyour-ios-app"></a><span data-ttu-id="68048-155">Adicionar aplicativo do iOS de tooyour de notificações de push</span><span class="sxs-lookup"><span data-stu-id="68048-155">Add push notifications tooyour iOS app</span></span>
1. <span data-ttu-id="68048-156">Em Olá **iOS** de projeto, abra appdelegate. cs e adicionar Olá superior de toohello instrução saudação do arquivo de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="68048-156">In hello **iOS** project, open AppDelegate.cs and add hello following statement toohello top of hello code file.</span></span>

        using Newtonsoft.Json.Linq;
2. <span data-ttu-id="68048-157">Em Olá **AppDelegate** da classe, adicione uma substituição para Olá **RegisteredForRemoteNotifications** tooregister de eventos para notificações:</span><span class="sxs-lookup"><span data-stu-id="68048-157">In hello **AppDelegate** class, add an override for hello **RegisteredForRemoteNotifications** event tooregister for notifications:</span></span>

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
3. <span data-ttu-id="68048-158">Em **AppDelegate**, também adicionar Olá após a substituição de saudação **DidReceiveRemoteNotification** manipulador de eventos:</span><span class="sxs-lookup"><span data-stu-id="68048-158">In **AppDelegate**, also add hello following override for hello **DidReceiveRemoteNotification** event handler:</span></span>

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

    <span data-ttu-id="68048-159">Esse método manipula notificações recebidas enquanto o aplicativo hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="68048-159">This method handles incoming notifications while hello app is running.</span></span>
4. <span data-ttu-id="68048-160">Em Olá **AppDelegate** de classe, adicione Olá toohello de código a seguir **FinishedLaunching** método:</span><span class="sxs-lookup"><span data-stu-id="68048-160">In hello **AppDelegate** class, add hello following code toohello **FinishedLaunching** method:</span></span>

        // Register for push notifications.
        var settings = UIUserNotificationSettings.GetSettingsForTypes(
            UIUserNotificationType.Alert
            | UIUserNotificationType.Badge
            | UIUserNotificationType.Sound,
            new NSSet());

        UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
        UIApplication.SharedApplication.RegisterForRemoteNotifications();

    <span data-ttu-id="68048-161">Isso habilita o suporte para notificações remotas e solicitações de registro por push.</span><span class="sxs-lookup"><span data-stu-id="68048-161">This enables support for remote notifications and requests push registration.</span></span>

<span data-ttu-id="68048-162">Seu aplicativo agora está atualizada toosupport notificações de envio.</span><span class="sxs-lookup"><span data-stu-id="68048-162">Your app is now updated toosupport push notifications.</span></span>

#### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="68048-163">Testar notificações por push em seu aplicativo iOS</span><span class="sxs-lookup"><span data-stu-id="68048-163">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="68048-164">Clique com botão direito Olá iOS e, em seguida, clique em **definir como projeto de inicialização**.</span><span class="sxs-lookup"><span data-stu-id="68048-164">Right-click hello iOS project, and click **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="68048-165">Olá pressione **executar** botão ou **F5** no Visual Studio toobuild Olá projeto e iniciar o aplicativo hello em um dispositivo iOS.</span><span class="sxs-lookup"><span data-stu-id="68048-165">Press hello **Run** button or **F5** in Visual Studio toobuild hello project and start hello app in an iOS device.</span></span> <span data-ttu-id="68048-166">Em seguida, clique em **Okey** tooaccept as notificações de envio.</span><span class="sxs-lookup"><span data-stu-id="68048-166">Then click **OK** tooaccept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="68048-167">Você deve aceitar explicitamente as notificações por push do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="68048-167">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="68048-168">Essa solicitação ocorre apenas Olá Olá aplicativo será executado pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="68048-168">This request only occurs hello first time that hello app runs.</span></span>
   >
   >
3. <span data-ttu-id="68048-169">No aplicativo hello, digite uma tarefa e, em seguida, clique em Olá adição (**+**) ícone.</span><span class="sxs-lookup"><span data-stu-id="68048-169">In hello app, type a task, and then click hello plus (**+**) icon.</span></span>
4. <span data-ttu-id="68048-170">Verifique se uma notificação é recebida e, em seguida, clique em **Okey** toodismiss Olá notificação.</span><span class="sxs-lookup"><span data-stu-id="68048-170">Verify that a notification is received, and then click **OK** toodismiss hello notification.</span></span>

## <a name="configure-and-run-windows-projects-optional"></a><span data-ttu-id="68048-171">Configurar e executar projetos do Windows (opcional)</span><span class="sxs-lookup"><span data-stu-id="68048-171">Configure and run Windows projects (optional)</span></span>
<span data-ttu-id="68048-172">Esta seção é para executar Olá WinApp xamarin. Forms e WinPhone81 projetos para dispositivos Windows.</span><span class="sxs-lookup"><span data-stu-id="68048-172">This section is for running hello Xamarin.Forms WinApp and WinPhone81 projects for Windows devices.</span></span> <span data-ttu-id="68048-173">Estas etapas também oferecem suporte a projetos da Plataforma Universal do Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="68048-173">These steps also support Universal Windows Platform (UWP) projects.</span></span> <span data-ttu-id="68048-174">Você poderá ignorá-la se não estiver trabalhando com dispositivos Windows.</span><span class="sxs-lookup"><span data-stu-id="68048-174">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-windows-notification-service-wns"></a><span data-ttu-id="68048-175">Registrar o aplicativo Windows para receber notificações por push com o WNS (Serviço de Notificação do Windows)</span><span class="sxs-lookup"><span data-stu-id="68048-175">Register your Windows app for push notifications with Windows Notification Service (WNS)</span></span>
[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

#### <a name="configure-hello-notification-hub-for-wns"></a><span data-ttu-id="68048-176">Configurar o hub de notificação Olá para o WNS</span><span class="sxs-lookup"><span data-stu-id="68048-176">Configure hello notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="add-push-notifications-tooyour-windows-app"></a><span data-ttu-id="68048-177">Adicionar aplicativo do Windows de tooyour de notificações de push</span><span class="sxs-lookup"><span data-stu-id="68048-177">Add push notifications tooyour Windows app</span></span>
1. <span data-ttu-id="68048-178">No Visual Studio, abra **App.xaml.cs** em uma janela do projeto e adicionar Olá instruções a seguir.</span><span class="sxs-lookup"><span data-stu-id="68048-178">In Visual Studio, open **App.xaml.cs** in a Windows project, and add hello following statements.</span></span>

        using Newtonsoft.Json.Linq;
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
        using <your_TodoItemManager_portable_class_namespace>;

    <span data-ttu-id="68048-179">Substituir `<your_TodoItemManager_portable_class_namespace>` com o namespace de saudação do seu projeto portátil que contém Olá `TodoItemManager` classe.</span><span class="sxs-lookup"><span data-stu-id="68048-179">Replace `<your_TodoItemManager_portable_class_namespace>` with hello namespace of your portable project that contains hello `TodoItemManager` class.</span></span>
2. <span data-ttu-id="68048-180">Em App.xaml.cs, adicione o seguinte de saudação **InitNotificationsAsync** método:</span><span class="sxs-lookup"><span data-stu-id="68048-180">In App.xaml.cs, add hello following **InitNotificationsAsync** method:</span></span>

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

    <span data-ttu-id="68048-181">Esse método obtém o canal de notificação por push hello e registra as notificações de modelo de tooreceive um modelo de hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="68048-181">This method gets hello push notification channel, and registers a template tooreceive template notifications from your notification hub.</span></span> <span data-ttu-id="68048-182">Uma notificação de modelo que oferece suporte a *messageParam* toothis cliente será entregue.</span><span class="sxs-lookup"><span data-stu-id="68048-182">A template notification that supports *messageParam* will be delivered toothis client.</span></span>
3. <span data-ttu-id="68048-183">Em App.xaml.cs, atualizar Olá **OnLaunched** definição de método de manipulador de eventos adicionando Olá `async` modificador.</span><span class="sxs-lookup"><span data-stu-id="68048-183">In App.xaml.cs, update hello **OnLaunched** event handler method definition by adding hello `async` modifier.</span></span> <span data-ttu-id="68048-184">Em seguida, adicione Olá a seguinte linha de código no final de saudação do método hello:</span><span class="sxs-lookup"><span data-stu-id="68048-184">Then add hello following line of code at hello end of hello method:</span></span>

        await InitNotificationsAsync();

    <span data-ttu-id="68048-185">Isso garante que o registro de notificação por push Olá é criado ou atualizado sempre que o aplicativo hello é iniciado.</span><span class="sxs-lookup"><span data-stu-id="68048-185">This ensures that hello push notification registration is created or refreshed every time hello app is launched.</span></span> <span data-ttu-id="68048-186">É importante toodo este tooguarantee que Olá WNS push canal está sempre ativa.</span><span class="sxs-lookup"><span data-stu-id="68048-186">It's important toodo this tooguarantee that hello WNS push channel is always active.</span></span>  
4. <span data-ttu-id="68048-187">No Gerenciador de soluções do Visual Studio, abra Olá **Package. appxmanifest** arquivo e defina **compatíveis com notificação do sistema** muito**Sim** em **notificações**.</span><span class="sxs-lookup"><span data-stu-id="68048-187">In Solution Explorer for Visual Studio, open hello **Package.appxmanifest** file, and set **Toast Capable** too**Yes** under **Notifications**.</span></span>
5. <span data-ttu-id="68048-188">Criar aplicativo hello e verifique se que você tem sem erros.</span><span class="sxs-lookup"><span data-stu-id="68048-188">Build hello app and verify you have no errors.</span></span> <span data-ttu-id="68048-189">Seu aplicativo cliente agora deve registrar para notificações do modelo de saudação do hello que terminar de volta a aplicativos móveis.</span><span class="sxs-lookup"><span data-stu-id="68048-189">Your client app should now register for hello template notifications from hello Mobile Apps back end.</span></span> <span data-ttu-id="68048-190">Repita esta seção para cada projeto do Windows em sua solução.</span><span class="sxs-lookup"><span data-stu-id="68048-190">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="68048-191">Testar as notificações por push em seu aplicativo para Windows</span><span class="sxs-lookup"><span data-stu-id="68048-191">Test push notifications in your Windows app</span></span>
1. <span data-ttu-id="68048-192">No Visual Studio, clique com o botão direito do mouse no projeto do Windows e clique em **Definir como projeto de inicialização**.</span><span class="sxs-lookup"><span data-stu-id="68048-192">In Visual Studio, right-click a Windows project, and click **Set as startup project**.</span></span>
2. <span data-ttu-id="68048-193">Olá pressione **executar** botão projeto de saudação toobuild e iniciar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="68048-193">Press hello **Run** button toobuild hello project and start hello app.</span></span>
3. <span data-ttu-id="68048-194">No aplicativo hello, digite um nome para um novo todoitem e, em seguida, clique em Olá adição (**+**) ícone tooadd-lo.</span><span class="sxs-lookup"><span data-stu-id="68048-194">In hello app, type a name for a new todoitem, and then click hello plus (**+**) icon tooadd it.</span></span>
4. <span data-ttu-id="68048-195">Verifique se que uma notificação é recebida quando Olá item é adicionado.</span><span class="sxs-lookup"><span data-stu-id="68048-195">Verify that a notification is received when hello item is added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68048-196">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="68048-196">Next steps</span></span>
<span data-ttu-id="68048-197">Saiba mais sobre as notificações por push:</span><span class="sxs-lookup"><span data-stu-id="68048-197">You can learn more about push notifications:</span></span>

* [<span data-ttu-id="68048-198">Diagnosticar problemas com notificações por push</span><span class="sxs-lookup"><span data-stu-id="68048-198">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="68048-199">há vários motivos por que as notificações podem ser abandonadas ou não irem terminar nos dispositivos.</span><span class="sxs-lookup"><span data-stu-id="68048-199">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="68048-200">Este tópico mostra como tooanalyze e descobrir raiz Olá causam falhas de notificação por push.</span><span class="sxs-lookup"><span data-stu-id="68048-200">This topic shows you how tooanalyze and figure out hello root cause of push notification failures.</span></span>

<span data-ttu-id="68048-201">Você também pode continuar em tooone de saudação tutoriais a seguir:</span><span class="sxs-lookup"><span data-stu-id="68048-201">You can also continue on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="68048-202">Adicionar autenticação tooyour aplicativo</span><span class="sxs-lookup"><span data-stu-id="68048-202">Add authentication tooyour app </span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="68048-203">Saiba como tooauthenticate usuários do seu aplicativo com um provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="68048-203">Learn how tooauthenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="68048-204">Habilitar sincronização offline para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="68048-204">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="68048-205">Saiba como tooadd de suporte off-line para seu aplicativo usando um aplicativos móveis do back-end.</span><span class="sxs-lookup"><span data-stu-id="68048-205">Learn how tooadd offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="68048-206">Com a sincronização offline, os usuários podem interagir com um aplicativo móvel &mdash; exibindo, adicionando ou modificando dados &mdash; mesmo quando não há nenhuma conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="68048-206">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Xcode]: https://go.microsoft.com/fwLink/?LinkID=266532
[apns object]: http://go.microsoft.com/fwlink/p/?LinkId=272333
