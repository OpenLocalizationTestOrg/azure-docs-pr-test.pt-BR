---
title: "Adicionar notificações por push ao aplicativo Xamarin.Forms | Microsoft Docs"
description: "Aprenda a usar os serviços do Azure para enviar notificações por push aos aplicativos Xamarin.Forms."
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
ms.openlocfilehash: 912367636f1b26b3b07fbd5fe3fe8ed053218fd5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-xamarinforms-app"></a><span data-ttu-id="a8e96-103">Adicionar notificações por push ao aplicativo Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="a8e96-103">Add push notifications to your Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="a8e96-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a8e96-104">Overview</span></span>
<span data-ttu-id="a8e96-105">Neste tutorial, você adiciona notificações por push a todos os projetos resultantes do [início rápido do Xamarin.Forms](app-service-mobile-xamarin-forms-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a8e96-105">In this tutorial, you add push notifications to all the projects that resulted from the [Xamarin.Forms quick start](app-service-mobile-xamarin-forms-get-started.md).</span></span> <span data-ttu-id="a8e96-106">Isso significa que uma notificação por push é enviada para todos os clientes de plataforma cruzada sempre que um registro é inserido.</span><span class="sxs-lookup"><span data-stu-id="a8e96-106">This means that a push notification is sent to all cross-platform clients every time a record is inserted.</span></span>

<span data-ttu-id="a8e96-107">Se você não usar o projeto baixado do início rápido do servidor, deve adicionar o pacote de extensão de notificação por push ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="a8e96-107">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="a8e96-108">Para saber mais, veja [Trabalhar com o SDK do servidor de back-end do .NET para Aplicativos Móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="a8e96-108">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8e96-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a8e96-109">Prerequisites</span></span>
<span data-ttu-id="a8e96-110">Para o iOS, você precisará de uma [associação ao Programa do Desenvolvedor da Apple](https://developer.apple.com/programs/ios/) e um dispositivo iOS físico.</span><span class="sxs-lookup"><span data-stu-id="a8e96-110">For iOS, you will need an [Apple Developer Program membership](https://developer.apple.com/programs/ios/) and a physical iOS device.</span></span> <span data-ttu-id="a8e96-111">O [simulador do iOS não dá suporte a notificações por push](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="a8e96-111">The [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span>

## <span data-ttu-id="a8e96-112"><a name="configure-hub"></a>Configurar um Hub de Notificação</span><span class="sxs-lookup"><span data-stu-id="a8e96-112"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="update-the-server-project-to-send-push-notifications"></a><span data-ttu-id="a8e96-113">Atualizar o projeto de servidor para enviar notificações por push</span><span class="sxs-lookup"><span data-stu-id="a8e96-113">Update the server project to send push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-and-run-the-android-project-optional"></a><span data-ttu-id="a8e96-114">Configurar e executar o projeto do Android (opcional)</span><span class="sxs-lookup"><span data-stu-id="a8e96-114">Configure and run the Android project (optional)</span></span>
<span data-ttu-id="a8e96-115">Conclua esta seção para habilitar notificações por push para o projeto Droid Xamarin.Forms para Android.</span><span class="sxs-lookup"><span data-stu-id="a8e96-115">Complete this section to enable push notifications for the Xamarin.Forms Droid project for Android.</span></span>

### <a name="enable-firebase-cloud-messaging-fcm"></a><span data-ttu-id="a8e96-116">Habilitar FCM (mensagens de nuvem Firebase)</span><span class="sxs-lookup"><span data-stu-id="a8e96-116">Enable Firebase Cloud Messaging (FCM)</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

### <a name="configure-the-mobile-apps-back-end-to-send-push-requests-by-using-fcm"></a><span data-ttu-id="a8e96-117">Configurar o back-end dos Aplicativos Móveis para enviar solicitações por push usando o FCM</span><span class="sxs-lookup"><span data-stu-id="a8e96-117">Configure the Mobile Apps back end to send push requests by using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

### <a name="add-push-notifications-to-the-android-project"></a><span data-ttu-id="a8e96-118">Adicionar notificações por push ao projeto Droid</span><span class="sxs-lookup"><span data-stu-id="a8e96-118">Add push notifications to the Android project</span></span>
<span data-ttu-id="a8e96-119">Com o back-end configurado com o FCM, é possível adicionar componentes e códigos ao cliente para registrá-lo no FCM.</span><span class="sxs-lookup"><span data-stu-id="a8e96-119">With the back end configured with FCM, you can add components and codes to the client to register with FCM.</span></span> <span data-ttu-id="a8e96-120">Também é possível se registrar para receber notificações por push com os Hubs de Notificação do Azure por meio do back-end dos Aplicativos Móveis e receber as notificações.</span><span class="sxs-lookup"><span data-stu-id="a8e96-120">You can also register for push notifications with Azure Notification Hubs through the Mobile Apps back end, and receive notifications.</span></span>

1. <span data-ttu-id="a8e96-121">No projeto **Droid**, clique com o botão direito do mouse na pasta **Componentes** e clique em **Obter Mais Componentes...**.</span><span class="sxs-lookup"><span data-stu-id="a8e96-121">In the **Droid** project, right-click the **Components** folder, and click **Get More Components...**.</span></span> <span data-ttu-id="a8e96-122">Depois, pesquise o componente **Cliente do Google Cloud Messaging** e adicione-o ao projeto.</span><span class="sxs-lookup"><span data-stu-id="a8e96-122">Then search for the **Google Cloud Messaging Client** component and add it to the project.</span></span> <span data-ttu-id="a8e96-123">Esse componente oferece suporte a notificações por push para um projeto Android Xamarin.</span><span class="sxs-lookup"><span data-stu-id="a8e96-123">This component supports push notifications for a Xamarin Android project.</span></span>
2. <span data-ttu-id="a8e96-124">Abra o arquivo de projeto MainActivity.cs e adicione a seguinte instrução à parte superior do arquivo:</span><span class="sxs-lookup"><span data-stu-id="a8e96-124">Open the MainActivity.cs project file, and add the following statement at the top of the file:</span></span>

        using Gcm.Client;
3. <span data-ttu-id="a8e96-125">Adicione o código a seguir ao método **OnCreate**, após a chamada a **LoadApplication**:</span><span class="sxs-lookup"><span data-stu-id="a8e96-125">Add the following code to the **OnCreate** method after the call to **LoadApplication**:</span></span>

        try
        {
            // Check to ensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);

            // Register for push notifications
            System.Diagnostics.Debug.WriteLine("Registering...");
            GcmClient.Register(this, PushHandlerBroadcastReceiver.SENDER_IDS);
        }
        catch (Java.Net.MalformedURLException)
        {
            CreateAndShowDialog("There was an error creating the client. Verify the URL.", "Error");
        }
        catch (Exception e)
        {
            CreateAndShowDialog(e.Message, "Error");
        }
4. <span data-ttu-id="a8e96-126">Adicione um novo método auxiliar **CreateAndShowDialog** , desta maneira:</span><span class="sxs-lookup"><span data-stu-id="a8e96-126">Add a new **CreateAndShowDialog** helper method, as follows:</span></span>

        private void CreateAndShowDialog(String message, String title)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);

            builder.SetMessage (message);
            builder.SetTitle (title);
            builder.Create().Show ();
        }
5. <span data-ttu-id="a8e96-127">Adicione o código a seguir à classe **MainActivity** :</span><span class="sxs-lookup"><span data-stu-id="a8e96-127">Add the following code to the **MainActivity** class:</span></span>

        // Create a new instance field for this activity.
        static MainActivity instance = null;

        // Return the current activity instance.
        public static MainActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }

    <span data-ttu-id="a8e96-128">Isso expõe a instância **MainActivity** atual e, portanto, podemos executar no thread principal da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="a8e96-128">This exposes the current **MainActivity** instance, so we can execute on the main UI thread.</span></span>
6. <span data-ttu-id="a8e96-129">Inicialize a variável `instance` no início do método **OnCreate** como mostrado a seguir.</span><span class="sxs-lookup"><span data-stu-id="a8e96-129">Initialize the `instance` variable at the beginning of the **OnCreate** method, as follows.</span></span>

        // Set the current instance of MainActivity.
        instance = this;
7. <span data-ttu-id="a8e96-130">Adicione um novo arquivo de classe ao projeto **Droid** chamado `GcmService.cs` e verifique se as instruções **using** a seguir estão presentes na parte superior do arquivo:</span><span class="sxs-lookup"><span data-stu-id="a8e96-130">Add a new class file to the **Droid** project named `GcmService.cs`, and make sure the following **using** statements are present at the top of the file:</span></span>

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
8. <span data-ttu-id="a8e96-131">Adicione as seguintes solicitações de permissão na parte superior do arquivo, após as instruções **using** e antes da declaração **namespace**.</span><span class="sxs-lookup"><span data-stu-id="a8e96-131">Add the following permission requests at the top of the file, after the **using** statements and before the **namespace** declaration.</span></span>

        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
9. <span data-ttu-id="a8e96-132">Adicione a seguinte definição de classe ao namespace.</span><span class="sxs-lookup"><span data-stu-id="a8e96-132">Add the following class definition to the namespace.</span></span>

       [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, Categories = new string[] { "@PACKAGE_NAME@" })]
       public class PushHandlerBroadcastReceiver : GcmBroadcastReceiverBase<GcmService>
       {
           public static string[] SENDER_IDS = new string[] { "<PROJECT_NUMBER>" };
       }

   > [!NOTE]
   > <span data-ttu-id="a8e96-133">Substitua **<PROJECT_NUMBER>** pelo número do projeto que você anotou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a8e96-133">Replace **<PROJECT_NUMBER>** with your project number you noted earlier.</span></span>    
   >
   >
10. <span data-ttu-id="a8e96-134">Substitua a classe **GcmService** vazia pelo código a seguir, que usa o novo receptor de difusão:</span><span class="sxs-lookup"><span data-stu-id="a8e96-134">Replace the empty **GcmService** class with the following code, which uses the new broadcast receiver:</span></span>

         [Service]
         public class GcmService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }

             public GcmService()
                 : base(PushHandlerBroadcastReceiver.SENDER_IDS){}
         }
11. <span data-ttu-id="a8e96-135">Adicione o código a seguir à classe **GcmService**.</span><span class="sxs-lookup"><span data-stu-id="a8e96-135">Add the following code to the **GcmService** class.</span></span> <span data-ttu-id="a8e96-136">Isso substitui o manipulador de eventos **OnRegistered** e implementa um método **Register**.</span><span class="sxs-lookup"><span data-stu-id="a8e96-136">This overrides the **OnRegistered** event handler and implements a **Register** method.</span></span>

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

    <span data-ttu-id="a8e96-137">Observe que esse código usa o parâmetro `messageParam` no registro do modelo.</span><span class="sxs-lookup"><span data-stu-id="a8e96-137">Note that this code uses the `messageParam` parameter in the template registration.</span></span>
12. <span data-ttu-id="a8e96-138">Adicione o seguinte código que implementa **OnMessage**:</span><span class="sxs-lookup"><span data-stu-id="a8e96-138">Add the following code that implements **OnMessage**:</span></span>

        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info("PushHandlerBroadcastReceiver", "GCM Message Received!");

            var msg = new StringBuilder();

            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }

            //Store the message
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

            //Create an intent to show ui
            var uiIntent = new Intent(this, typeof(MainActivity));

            //Use Notification Builder
            NotificationCompat.Builder builder = new NotificationCompat.Builder(this);

            //Create the notification
            //we use the pending intent, passing our ui intent over which will get called
            //when the notification is tapped.
            var notification = builder.SetContentIntent(PendingIntent.GetActivity(this, 0, uiIntent, 0))
                    .SetSmallIcon(Android.Resource.Drawable.SymActionEmail)
                    .SetTicker(title)
                    .SetContentTitle(title)
                    .SetContentText(desc)

                    //Set the notification sound
                    .SetSound(RingtoneManager.GetDefaultUri(RingtoneType.Notification))

                    //Auto cancel will remove the notification once the user touches it
                    .SetAutoCancel(true).Build();

            //Show the notification
            notificationManager.Notify(1, notification);
        }

    <span data-ttu-id="a8e96-139">Isso manipula as notificações recebidas e as envia para o gerenciador de notificações a ser exibido.</span><span class="sxs-lookup"><span data-stu-id="a8e96-139">This handles incoming notifications and sends them to the notification manager to be displayed.</span></span>
13. <span data-ttu-id="a8e96-140">**GcmServiceBase** também exige que você implemente os métodos de manipulador **OnUnRegistered** e **OnError**, o que pode ser feito da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="a8e96-140">**GcmServiceBase** also requires you to implement the **OnUnRegistered** and **OnError** handler methods, which you can do as follows:</span></span>

        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "Unregistered RegisterationId : " + registrationId);
        }

        protected override void OnError(Context context, string errorId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "GCM Error: " + errorId);
        }

<span data-ttu-id="a8e96-141">Agora, você está pronto para testar as notificações por push no aplicativo em execução em um dispositivo ou no emulador Android.</span><span class="sxs-lookup"><span data-stu-id="a8e96-141">Now, you are ready test push notifications in the app running on an Android device or the emulator.</span></span>

### <a name="test-push-notifications-in-your-android-app"></a><span data-ttu-id="a8e96-142">Testar notificações por push em seu aplicativo Android</span><span class="sxs-lookup"><span data-stu-id="a8e96-142">Test push notifications in your Android app</span></span>
<span data-ttu-id="a8e96-143">As duas primeiras etapas serão necessárias apenas quando o teste estiver sendo feito em um emulador.</span><span class="sxs-lookup"><span data-stu-id="a8e96-143">The first two steps are required only when you're testing on an emulator.</span></span>

1. <span data-ttu-id="a8e96-144">Verifique se você está implantando ou depurando em um dispositivo virtual que tem as APIs do Google definidas como o destino, como mostrado abaixo no gerenciador de Dispositivo Virtual do Android.</span><span class="sxs-lookup"><span data-stu-id="a8e96-144">Make sure that you are deploying to or debugging on a virtual device that has Google APIs set as the target, as shown below in the Android Virtual Device manager.</span></span>
2. <span data-ttu-id="a8e96-145">Adicione uma conta do Google ao dispositivo Android clicando em **Aplicativos** > **Configurações** > **Adicionar conta**.</span><span class="sxs-lookup"><span data-stu-id="a8e96-145">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**.</span></span> <span data-ttu-id="a8e96-146">Depois, siga os prompts para adicionar uma conta existente do Google ao dispositivo ou para criar uma nova.</span><span class="sxs-lookup"><span data-stu-id="a8e96-146">Then follow the prompts to add an existing Google account to the device, or to create a new one.</span></span>
3. <span data-ttu-id="a8e96-147">No Visual Studio ou Xamarin Studio, clique com o botão direito do mouse no projeto **Droid** e clique em **Definir como projeto de inicialização**.</span><span class="sxs-lookup"><span data-stu-id="a8e96-147">In Visual Studio or Xamarin Studio, right-click the **Droid** project and click **Set as startup project**.</span></span>
4. <span data-ttu-id="a8e96-148">Clique em **Executar** para criar o projeto e iniciar o aplicativo no emulador ou no dispositivo Android.</span><span class="sxs-lookup"><span data-stu-id="a8e96-148">Click **Run** to build the project and start the app on your Android device or emulator.</span></span>
5. <span data-ttu-id="a8e96-149">No aplicativo, digite uma tarefa e clique no ícone do sinal de adição (**+**).</span><span class="sxs-lookup"><span data-stu-id="a8e96-149">In the app, type a task, and then click the plus (**+**) icon.</span></span>
6. <span data-ttu-id="a8e96-150">Verifique se uma notificação é recebida quando um item é adicionado.</span><span class="sxs-lookup"><span data-stu-id="a8e96-150">Verify that a notification is received when an item is added.</span></span>

## <a name="configure-and-run-the-ios-project-optional"></a><span data-ttu-id="a8e96-151">Configurar e executar o projeto do iOS (opcional)</span><span class="sxs-lookup"><span data-stu-id="a8e96-151">Configure and run the iOS project (optional)</span></span>
<span data-ttu-id="a8e96-152">Esta seção trata da execução do projeto do iOS Xamarin para dispositivos iOS.</span><span class="sxs-lookup"><span data-stu-id="a8e96-152">This section is for running the Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="a8e96-153">Você poderá ignorá-la se não estiver trabalhando com dispositivos iOS.</span><span class="sxs-lookup"><span data-stu-id="a8e96-153">You can skip this section if you are not working with iOS devices.</span></span>

[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

#### <a name="configure-the-notification-hub-for-apns"></a><span data-ttu-id="a8e96-154">Configurar o hub de notificação para APNS</span><span class="sxs-lookup"><span data-stu-id="a8e96-154">Configure the notification hub for APNS</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

<span data-ttu-id="a8e96-155">A seguir, você definirá a configuração do projeto do iOS no Xamarin Studio ou Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a8e96-155">Next, you will configure the iOS project setting in Xamarin Studio or Visual Studio.</span></span>

[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

#### <a name="add-push-notifications-to-your-ios-app"></a><span data-ttu-id="a8e96-156">Adicionar as notificações por push ao seu aplicativo iOS</span><span class="sxs-lookup"><span data-stu-id="a8e96-156">Add push notifications to your iOS app</span></span>
1. <span data-ttu-id="a8e96-157">No projeto **iOS**, abra AppDelegate.cs e adicione a instrução a seguir à parte superior do arquivo de código.</span><span class="sxs-lookup"><span data-stu-id="a8e96-157">In the **iOS** project, open AppDelegate.cs and add the following statement to the top of the code file.</span></span>

        using Newtonsoft.Json.Linq;
2. <span data-ttu-id="a8e96-158">Na classe **AppDelegate**, adicione também uma substituição ao evento **RegisteredForRemoteNotifications** a fim de registrar para o recebimento notificações:</span><span class="sxs-lookup"><span data-stu-id="a8e96-158">In the **AppDelegate** class, add an override for the **RegisteredForRemoteNotifications** event to register for notifications:</span></span>

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
3. <span data-ttu-id="a8e96-159">Em **AppDelegate**, adicione também a seguinte substituição para o manipulador de eventos **DidReceiveRemoteNotification**:</span><span class="sxs-lookup"><span data-stu-id="a8e96-159">In **AppDelegate**, also add the following override for the **DidReceiveRemoteNotification** event handler:</span></span>

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

    <span data-ttu-id="a8e96-160">Este método trata as notificações recebidas enquanto o aplicativo está em execução.</span><span class="sxs-lookup"><span data-stu-id="a8e96-160">This method handles incoming notifications while the app is running.</span></span>
4. <span data-ttu-id="a8e96-161">Na classe **AppDelegate**, adicione o seguinte código ao método **FinishedLaunching**:</span><span class="sxs-lookup"><span data-stu-id="a8e96-161">In the **AppDelegate** class, add the following code to the **FinishedLaunching** method:</span></span>

        // Register for push notifications.
        var settings = UIUserNotificationSettings.GetSettingsForTypes(
            UIUserNotificationType.Alert
            | UIUserNotificationType.Badge
            | UIUserNotificationType.Sound,
            new NSSet());

        UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
        UIApplication.SharedApplication.RegisterForRemoteNotifications();

    <span data-ttu-id="a8e96-162">Isso habilita o suporte para notificações remotas e solicitações de registro por push.</span><span class="sxs-lookup"><span data-stu-id="a8e96-162">This enables support for remote notifications and requests push registration.</span></span>

<span data-ttu-id="a8e96-163">Seu aplicativo foi atualizado para oferecer suporte a notificações de push.</span><span class="sxs-lookup"><span data-stu-id="a8e96-163">Your app is now updated to support push notifications.</span></span>

#### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="a8e96-164">Testar notificações por push em seu aplicativo iOS</span><span class="sxs-lookup"><span data-stu-id="a8e96-164">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="a8e96-165">Clique com o botão direito do mouse no projeto do iOS e, depois, clique em **Definir como Projeto de Inicialização**.</span><span class="sxs-lookup"><span data-stu-id="a8e96-165">Right-click the iOS project, and click **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="a8e96-166">Pressione o botão **Executar** ou **F5** no Visual Studio para criar o projeto e iniciar o aplicativo em um dispositivo iOS.</span><span class="sxs-lookup"><span data-stu-id="a8e96-166">Press the **Run** button or **F5** in Visual Studio to build the project and start the app in an iOS device.</span></span> <span data-ttu-id="a8e96-167">Em seguida, clique em **OK** para aceitar as notificações por push.</span><span class="sxs-lookup"><span data-stu-id="a8e96-167">Then click **OK** to accept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a8e96-168">Você deve aceitar explicitamente as notificações por push do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a8e96-168">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="a8e96-169">Essa solicitação ocorrerá apenas na primeira vez que o aplicativo for executado.</span><span class="sxs-lookup"><span data-stu-id="a8e96-169">This request only occurs the first time that the app runs.</span></span>
   >
   >
3. <span data-ttu-id="a8e96-170">No aplicativo, digite uma tarefa e clique no ícone do sinal de adição (**+**).</span><span class="sxs-lookup"><span data-stu-id="a8e96-170">In the app, type a task, and then click the plus (**+**) icon.</span></span>
4. <span data-ttu-id="a8e96-171">Verifique se uma notificação é recebida e clique em **OK** para ignorar a notificação.</span><span class="sxs-lookup"><span data-stu-id="a8e96-171">Verify that a notification is received, and then click **OK** to dismiss the notification.</span></span>

## <a name="configure-and-run-windows-projects-optional"></a><span data-ttu-id="a8e96-172">Configurar e executar projetos do Windows (opcional)</span><span class="sxs-lookup"><span data-stu-id="a8e96-172">Configure and run Windows projects (optional)</span></span>
<span data-ttu-id="a8e96-173">Esta seção trata da execução dos projetos WinApp e WinPhone81 de Xamarin.Forms para dispositivos Windows.</span><span class="sxs-lookup"><span data-stu-id="a8e96-173">This section is for running the Xamarin.Forms WinApp and WinPhone81 projects for Windows devices.</span></span> <span data-ttu-id="a8e96-174">Estas etapas também oferecem suporte a projetos da Plataforma Universal do Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="a8e96-174">These steps also support Universal Windows Platform (UWP) projects.</span></span> <span data-ttu-id="a8e96-175">Você poderá ignorá-la se não estiver trabalhando com dispositivos Windows.</span><span class="sxs-lookup"><span data-stu-id="a8e96-175">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-windows-notification-service-wns"></a><span data-ttu-id="a8e96-176">Registrar o aplicativo Windows para receber notificações por push com o WNS (Serviço de Notificação do Windows)</span><span class="sxs-lookup"><span data-stu-id="a8e96-176">Register your Windows app for push notifications with Windows Notification Service (WNS)</span></span>
[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

#### <a name="configure-the-notification-hub-for-wns"></a><span data-ttu-id="a8e96-177">Configurar o hub de notificação para WNS</span><span class="sxs-lookup"><span data-stu-id="a8e96-177">Configure the notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="add-push-notifications-to-your-windows-app"></a><span data-ttu-id="a8e96-178">Adicionar notificações por push ao seu aplicativo do Windows</span><span class="sxs-lookup"><span data-stu-id="a8e96-178">Add push notifications to your Windows app</span></span>
1. <span data-ttu-id="a8e96-179">No Visual Studio, abra **App.xaml.cs** em um projeto do Windows e adicione as instruções a seguir.</span><span class="sxs-lookup"><span data-stu-id="a8e96-179">In Visual Studio, open **App.xaml.cs** in a Windows project, and add the following statements.</span></span>

        using Newtonsoft.Json.Linq;
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
        using <your_TodoItemManager_portable_class_namespace>;

    <span data-ttu-id="a8e96-180">Substitua `<your_TodoItemManager_portable_class_namespace>` pelo namespace do projeto portátil que contém a classe `TodoItemManager`.</span><span class="sxs-lookup"><span data-stu-id="a8e96-180">Replace `<your_TodoItemManager_portable_class_namespace>` with the namespace of your portable project that contains the `TodoItemManager` class.</span></span>
2. <span data-ttu-id="a8e96-181">No App.xaml.cs, adicione o seguinte método **InitNotificationsAsync**:</span><span class="sxs-lookup"><span data-stu-id="a8e96-181">In App.xaml.cs, add the following **InitNotificationsAsync** method:</span></span>

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

    <span data-ttu-id="a8e96-182">Esse método obtém o canal de notificação por push e registra um modelo para receber as notificações de modelo do hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="a8e96-182">This method gets the push notification channel, and registers a template to receive template notifications from your notification hub.</span></span> <span data-ttu-id="a8e96-183">Uma notificação de modelo que oferece suporte a *messageParam* será entregue a esse cliente.</span><span class="sxs-lookup"><span data-stu-id="a8e96-183">A template notification that supports *messageParam* will be delivered to this client.</span></span>
3. <span data-ttu-id="a8e96-184">No App.xaml.cs, atualize a definição de método do manipulador de eventos **OnLaunched** adicionando o modificador `async`.</span><span class="sxs-lookup"><span data-stu-id="a8e96-184">In App.xaml.cs, update the **OnLaunched** event handler method definition by adding the `async` modifier.</span></span> <span data-ttu-id="a8e96-185">Depois, adicione a seguinte linha de código ao final do método:</span><span class="sxs-lookup"><span data-stu-id="a8e96-185">Then add the following line of code at the end of the method:</span></span>

        await InitNotificationsAsync();

    <span data-ttu-id="a8e96-186">Isso garante que o registro de notificação por push é criado ou atualizado sempre que o aplicativo é iniciado.</span><span class="sxs-lookup"><span data-stu-id="a8e96-186">This ensures that the push notification registration is created or refreshed every time the app is launched.</span></span> <span data-ttu-id="a8e96-187">É importante fazer isso para garantir que o canal de notificação por push WNS esteja sempre ativo.</span><span class="sxs-lookup"><span data-stu-id="a8e96-187">It's important to do this to guarantee that the WNS push channel is always active.</span></span>  
4. <span data-ttu-id="a8e96-188">No Gerenciador de Soluções do Visual Studio, abra o arquivo **Package.appxmanifest** e defina **Compatível com Notificação do Sistema** como **Sim** em **Notificações**.</span><span class="sxs-lookup"><span data-stu-id="a8e96-188">In Solution Explorer for Visual Studio, open the **Package.appxmanifest** file, and set **Toast Capable** to **Yes** under **Notifications**.</span></span>
5. <span data-ttu-id="a8e96-189">Compile o aplicativo e verifique se não há erros.</span><span class="sxs-lookup"><span data-stu-id="a8e96-189">Build the app and verify you have no errors.</span></span> <span data-ttu-id="a8e96-190">O aplicativo cliente agora deve se registrar para receber notificações de modelo do back-end dos Aplicativos Móveis.</span><span class="sxs-lookup"><span data-stu-id="a8e96-190">Your client app should now register for the template notifications from the Mobile Apps back end.</span></span> <span data-ttu-id="a8e96-191">Repita esta seção para cada projeto do Windows em sua solução.</span><span class="sxs-lookup"><span data-stu-id="a8e96-191">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="a8e96-192">Testar as notificações por push em seu aplicativo para Windows</span><span class="sxs-lookup"><span data-stu-id="a8e96-192">Test push notifications in your Windows app</span></span>
1. <span data-ttu-id="a8e96-193">No Visual Studio, clique com o botão direito do mouse no projeto do Windows e clique em **Definir como projeto de inicialização**.</span><span class="sxs-lookup"><span data-stu-id="a8e96-193">In Visual Studio, right-click a Windows project, and click **Set as startup project**.</span></span>
2. <span data-ttu-id="a8e96-194">Pressione o botão **Executar** para compilar o projeto e iniciar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a8e96-194">Press the **Run** button to build the project and start the app.</span></span>
3. <span data-ttu-id="a8e96-195">No aplicativo, digite um nome para um novo todoitem e, em seguida, clique no ícone de adição (**+**) para adicioná-lo.</span><span class="sxs-lookup"><span data-stu-id="a8e96-195">In the app, type a name for a new todoitem, and then click the plus (**+**) icon to add it.</span></span>
4. <span data-ttu-id="a8e96-196">Verifique se uma notificação é recebida quando o item é adicionado.</span><span class="sxs-lookup"><span data-stu-id="a8e96-196">Verify that a notification is received when the item is added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8e96-197">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a8e96-197">Next steps</span></span>
<span data-ttu-id="a8e96-198">Saiba mais sobre as notificações por push:</span><span class="sxs-lookup"><span data-stu-id="a8e96-198">You can learn more about push notifications:</span></span>

* [<span data-ttu-id="a8e96-199">Diagnosticar problemas com notificações por push</span><span class="sxs-lookup"><span data-stu-id="a8e96-199">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="a8e96-200">há vários motivos por que as notificações podem ser abandonadas ou não irem terminar nos dispositivos.</span><span class="sxs-lookup"><span data-stu-id="a8e96-200">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="a8e96-201">Este tópico mostra como analisar e descobrir a causa de falhas de notificação por push.</span><span class="sxs-lookup"><span data-stu-id="a8e96-201">This topic shows you how to analyze and figure out the root cause of push notification failures.</span></span>

<span data-ttu-id="a8e96-202">Continue também com um dos seguintes tutoriais:</span><span class="sxs-lookup"><span data-stu-id="a8e96-202">You can also continue on to one of the following tutorials:</span></span>

* [<span data-ttu-id="a8e96-203">Adicionar autenticação ao seu aplicativo </span><span class="sxs-lookup"><span data-stu-id="a8e96-203">Add authentication to your app </span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="a8e96-204">Saiba como autenticar os usuários do aplicativo com um provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="a8e96-204">Learn how to authenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="a8e96-205">Habilitar sincronização offline para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="a8e96-205">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="a8e96-206">Saiba como adicionar suporte offline para o aplicativo usando um back-end dos Aplicativos Móveis.</span><span class="sxs-lookup"><span data-stu-id="a8e96-206">Learn how to add offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="a8e96-207">Com a sincronização offline, os usuários podem interagir com um aplicativo móvel &mdash; exibindo, adicionando ou modificando dados &mdash; mesmo quando não há nenhuma conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="a8e96-207">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Xcode]: https://go.microsoft.com/fwLink/?LinkID=266532
[apns object]: http://go.microsoft.com/fwlink/p/?LinkId=272333
