---
title: "Introdução aos Hubs de Notificação do Azure para aplicativos do Kindle | Microsoft Docs"
description: "Neste tutorial, você aprende a usar os Hubs de Notificação do Azure para enviar notificações por push a um aplicativo Kindle."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 346fc8e5-294b-4e4f-9f27-7a82d9626e93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-kindle
ms.devlang: Java
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 7206f152ed7270abc62536a9ee164f7227833bcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a><span data-ttu-id="32187-103">Introdução aos Hubs de Notificação para aplicativos do Kindle</span><span class="sxs-lookup"><span data-stu-id="32187-103">Get started with Notification Hubs for Kindle apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="32187-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="32187-104">Overview</span></span>
<span data-ttu-id="32187-105">Este tutorial mostra como usar os Hubs de Notificação do Azure para enviar notificações por push para um aplicativo Kindle.</span><span class="sxs-lookup"><span data-stu-id="32187-105">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Kindle application.</span></span>
<span data-ttu-id="32187-106">Você deve criar um aplicativo Kindle em branco que recebe notificações por push usando Amazon Device Messaging (ADM).</span><span class="sxs-lookup"><span data-stu-id="32187-106">You'll create a blank Kindle app that receives push notifications by using Amazon Device Messaging (ADM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32187-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="32187-107">Prerequisites</span></span>
<span data-ttu-id="32187-108">Este tutorial exige o seguinte:</span><span class="sxs-lookup"><span data-stu-id="32187-108">This tutorial requires the following:</span></span>

* <span data-ttu-id="32187-109">Obtenha o SDK do Android (estamos supondo que você usará o Eclipse) no <a href="http://go.microsoft.com/fwlink/?LinkId=389797">site do Android</a>.</span><span class="sxs-lookup"><span data-stu-id="32187-109">Get the Android SDK (we assume that you will use Eclipse) from the <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a>.</span></span>
* <span data-ttu-id="32187-110">Siga as etapas em <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">Configurar seu ambiente de desenvolvimento</a> para configurar o ambiente de desenvolvimento para Kindle.</span><span class="sxs-lookup"><span data-stu-id="32187-110">Follow the steps in <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">Setting Up Your Development Environment</a> to set up your development environment for Kindle.</span></span>

## <a name="add-a-new-app-to-the-developer-portal"></a><span data-ttu-id="32187-111">Adicionar um novo aplicativo ao portal do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="32187-111">Add a new app to the developer portal</span></span>
1. <span data-ttu-id="32187-112">Primeiro, crie um aplicativo no [portal do desenvolvedor da Amazon].</span><span class="sxs-lookup"><span data-stu-id="32187-112">First, create an app in the [Amazon developer portal].</span></span>
   
    ![][0]
2. <span data-ttu-id="32187-113">Copie a **Chave do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="32187-113">Copy the **Application Key**.</span></span>
   
    ![][1]
3. <span data-ttu-id="32187-114">No portal, clique no nome do aplicativo e, em seguida, clique na guia **Mensagens de Dispositivos** .</span><span class="sxs-lookup"><span data-stu-id="32187-114">In the portal, click the name of your app, and then click the **Device Messaging** tab.</span></span>
   
    ![][2]
4. <span data-ttu-id="32187-115">Clique em **Criar um Novo Perfil de Segurança** e crie um novo perfil de segurança (por exemplo, **Perfil de segurança TestAdm**).</span><span class="sxs-lookup"><span data-stu-id="32187-115">Click **Create a New Security Profile**, and then create a new security profile (for example, **TestAdm security profile**).</span></span> <span data-ttu-id="32187-116">Em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="32187-116">Then click **Save**.</span></span>
   
    ![][3]
5. <span data-ttu-id="32187-117">Clique em **Perfis de Segurança** para exibir o perfil de segurança que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="32187-117">Click **Security Profiles** to view the security profile that you just created.</span></span> <span data-ttu-id="32187-118">Copie os valores de **ID do cliente** e **Segredo do Cliente** para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="32187-118">Copy the **Client ID** and **Client Secret** values for later use.</span></span>
   
    ![][4]

## <a name="create-an-api-key"></a><span data-ttu-id="32187-119">Criar uma chave para a API</span><span class="sxs-lookup"><span data-stu-id="32187-119">Create an API key</span></span>
1. <span data-ttu-id="32187-120">Abra uma prompt de comando com privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="32187-120">Open a command prompt with administrator privileges.</span></span>
2. <span data-ttu-id="32187-121">Navegue até a pasta Android SDK.</span><span class="sxs-lookup"><span data-stu-id="32187-121">Navigate to the Android SDK folder.</span></span>
3. <span data-ttu-id="32187-122">Digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="32187-122">Enter the following command:</span></span>
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. <span data-ttu-id="32187-123">Para a senha do **keystore**, digite **android**.</span><span class="sxs-lookup"><span data-stu-id="32187-123">For the **keystore** password, type **android**.</span></span>
5. <span data-ttu-id="32187-124">Copie a impressão digital **MD5** .</span><span class="sxs-lookup"><span data-stu-id="32187-124">Copy the **MD5** fingerprint.</span></span>
6. <span data-ttu-id="32187-125">De volta no portal do desenvolvedor, na guia **Mensagens**, clique em **Android/Kindle** e digite o nome do pacote para seu aplicativo (por exemplo, **com.sample.notificationhubtest**), o valor de **MD5** e clique em **Gerar a Chave de API**.</span><span class="sxs-lookup"><span data-stu-id="32187-125">Back in the developer portal, on the **Messaging** tab, click **Android/Kindle** and enter the name of the package for your app (for example, **com.sample.notificationhubtest**) and the **MD5** value, and then click **Generate API Key**.</span></span>

## <a name="add-credentials-to-the-hub"></a><span data-ttu-id="32187-126">Adicionar credenciais ao hub</span><span class="sxs-lookup"><span data-stu-id="32187-126">Add credentials to the hub</span></span>
<span data-ttu-id="32187-127">No portal, adicione o segredo do cliente e a ID do cliente à guia **Configurar** de seu hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="32187-127">In the portal, add the client secret and client ID to the **Configure** tab of your notification hub.</span></span>

## <a name="set-up-your-application"></a><span data-ttu-id="32187-128">Configurar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="32187-128">Set up your application</span></span>
> [!NOTE]
> <span data-ttu-id="32187-129">Ao criar um aplicativo, use pelo menos API de nível 17.</span><span class="sxs-lookup"><span data-stu-id="32187-129">When you're creating an application, use at least API Level 17.</span></span>
> 
> 

<span data-ttu-id="32187-130">Adicione as bibliotecas do ADM ao seu projeto Eclipse.</span><span class="sxs-lookup"><span data-stu-id="32187-130">Add the ADM libraries to your Eclipse project:</span></span>

1. <span data-ttu-id="32187-131">Para obter a biblioteca do ADM, [baixar o SDK].</span><span class="sxs-lookup"><span data-stu-id="32187-131">To obtain the ADM library, [download the SDK].</span></span> <span data-ttu-id="32187-132">Extraia o arquivo zip do SDK.</span><span class="sxs-lookup"><span data-stu-id="32187-132">Extract the SDK zip file.</span></span>
2. <span data-ttu-id="32187-133">No Eclipse, clique com o botão direito do mouse em seu projeto e clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="32187-133">In Eclipse, right-click your project, and then click **Properties**.</span></span> <span data-ttu-id="32187-134">Selecione **caminho de compilação de Java** à esquerda e, em seguida, selecione o * * bibliotecas * * guia na parte superior.</span><span class="sxs-lookup"><span data-stu-id="32187-134">Select **Java Build Path** on the left, and then select the **Libraries **tab at the top.</span></span> <span data-ttu-id="32187-135">Clique em **Adicionar Jar Externo** e selecione o arquivo `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` do diretório no qual você extraiu o SDK da Amazon.</span><span class="sxs-lookup"><span data-stu-id="32187-135">Click **Add External Jar**, and select the file `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` from the directory in which you extracted the Amazon SDK.</span></span>
3. <span data-ttu-id="32187-136">Baixe o SDK do Android NotificationHubs (link).</span><span class="sxs-lookup"><span data-stu-id="32187-136">Download the NotificationHubs Android SDK (link).</span></span>
4. <span data-ttu-id="32187-137">Descompacte o pacote e, em seguida, arraste o arquivo `notification-hubs-sdk.jar` na pasta `libs`no Eclipse.</span><span class="sxs-lookup"><span data-stu-id="32187-137">Unzip the package, and then drag the file `notification-hubs-sdk.jar` into the `libs` folder in Eclipse.</span></span>

<span data-ttu-id="32187-138">Edite seu manifesto de aplicativo para oferecer suporte ao ADM:</span><span class="sxs-lookup"><span data-stu-id="32187-138">Edit your app manifest to support ADM:</span></span>

1. <span data-ttu-id="32187-139">Adicione o namespace Amazon no elemento raiz do manifesto:</span><span class="sxs-lookup"><span data-stu-id="32187-139">Add the Amazon namespace in the root manifest element:</span></span>

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. <span data-ttu-id="32187-140">Adicione permissões como o primeiro elemento sob o elemento manifest.</span><span class="sxs-lookup"><span data-stu-id="32187-140">Add permissions as the first element under the manifest element.</span></span> <span data-ttu-id="32187-141">Substitua **[YOUR PACKAGE NAME]** pelo pacote usado para criar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="32187-141">Substitute **[YOUR PACKAGE NAME]** with the package that you used to create your app.</span></span>
   
        <permission
         android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE"
         android:protectionLevel="signature" />
   
        <uses-permission android:name="android.permission.INTERNET"/>
   
        <uses-permission android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE" />
   
        <!-- This permission allows your app access to receive push notifications
        from ADM. -->
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE" />
   
        <!-- ADM uses WAKE_LOCK to keep the processor from sleeping when a message is received. -->
        <uses-permission android:name="android.permission.WAKE_LOCK" />
2. <span data-ttu-id="32187-142">Insira o seguinte elemento como o primeiro filho do elemento application.</span><span class="sxs-lookup"><span data-stu-id="32187-142">Insert the following element as the first child of the application element.</span></span> <span data-ttu-id="32187-143">Lembre-se de substituir **YOUR SERVICE NAME** pelo nome do seu manipulador de mensagens do ADM que você criará na próxima seção (incluindo o pacote) e substitua **[YOUR PACKAGE NAME]** pelo nome do pacote com o qual você criou o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="32187-143">Remember to substitute **[YOUR SERVICE NAME]** with the name of your ADM message handler that you create in the next section (including the package), and replace **[YOUR PACKAGE NAME]** with the package name with which you created your app.</span></span>
   
        <amazon:enable-feature
              android:name="com.amazon.device.messaging"
                     android:required="true"/>
        <service
            android:name="[YOUR SERVICE NAME]"
            android:exported="false" />
   
        <receiver
            android:name="[YOUR SERVICE NAME]$Receiver" />
   
            <!-- This permission ensures that only ADM can send your app registration broadcasts. -->
            android:permission="com.amazon.device.messaging.permission.SEND" >
   
            <!-- To interact with ADM, your app must listen for the following intents. -->
            <intent-filter>
          <action android:name="com.amazon.device.messaging.intent.REGISTRATION" />
          <action android:name="com.amazon.device.messaging.intent.RECEIVE" />
   
          <!-- Replace the name in the category tag with your app's package name. -->
          <category android:name="[YOUR PACKAGE NAME]" />
            </intent-filter>
        </receiver>

## <a name="create-your-adm-message-handler"></a><span data-ttu-id="32187-144">Crie o manipulador de mensagens do ADM:</span><span class="sxs-lookup"><span data-stu-id="32187-144">Create your ADM message handler</span></span>
1. <span data-ttu-id="32187-145">Crie uma classe nova que herda do `com.amazon.device.messaging.ADMMessageHandlerBase` e nomeie-a `MyADMMessageHandler`, conforme mostrado na seguinte figura:</span><span class="sxs-lookup"><span data-stu-id="32187-145">Create a new class that inherits from `com.amazon.device.messaging.ADMMessageHandlerBase` and name it `MyADMMessageHandler`, as shown in the following figure:</span></span>
   
    ![][6]
2. <span data-ttu-id="32187-146">Adicione as seguintes declarações de `import` :</span><span class="sxs-lookup"><span data-stu-id="32187-146">Add the following `import` statements:</span></span>
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. <span data-ttu-id="32187-147">Adicione o seguinte código à classe criada.</span><span class="sxs-lookup"><span data-stu-id="32187-147">Add the following code in the class that you created.</span></span> <span data-ttu-id="32187-148">Lembre-se de substituir o nome e cadeia de conexão do hub (escuta):</span><span class="sxs-lookup"><span data-stu-id="32187-148">Remember to substitute the hub name and connection string (listen):</span></span>
   
        public static final int NOTIFICATION_ID = 1;
        private NotificationManager mNotificationManager;
        NotificationCompat.Builder builder;
          private static NotificationHub hub;
        public static NotificationHub getNotificationHub(Context context) {
            Log.v("com.wa.hellokindlefire", "getNotificationHub");
            if (hub == null) {
                hub = new NotificationHub("[hub name]", "[listen connection string]", context);
            }
            return hub;
        }
   
        public MyADMMessageHandler() {
                super("MyADMMessageHandler");
            }
   
            public static class Receiver extends ADMMessageReceiver
            {
                public Receiver()
                {
                    super(MyADMMessageHandler.class);
                }
            }
   
            private void sendNotification(String msg) {
                Context ctx = getApplicationContext();
   
                mNotificationManager = (NotificationManager)
                    ctx.getSystemService(Context.NOTIFICATION_SERVICE);
   
            PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                  new Intent(ctx, MainActivity.class), 0);
   
            NotificationCompat.Builder mBuilder =
                  new NotificationCompat.Builder(ctx)
                  .setSmallIcon(R.mipmap.ic_launcher)
                  .setContentTitle("Notification Hub Demo")
                  .setStyle(new NotificationCompat.BigTextStyle()
                         .bigText(msg))
                  .setContentText(msg);
   
             mBuilder.setContentIntent(contentIntent);
             mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
        }
4. <span data-ttu-id="32187-149">Adicione o seguinte código ao método `OnMessage()` :</span><span class="sxs-lookup"><span data-stu-id="32187-149">Add the following code to the `OnMessage()` method:</span></span>
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. <span data-ttu-id="32187-150">Adicione o seguinte código ao método `OnRegistered` :</span><span class="sxs-lookup"><span data-stu-id="32187-150">Add the following code to the `OnRegistered` method:</span></span>
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. <span data-ttu-id="32187-151">Adicione o seguinte código ao método `OnUnregistered` :</span><span class="sxs-lookup"><span data-stu-id="32187-151">Add the following code to the `OnUnregistered` method:</span></span>
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. <span data-ttu-id="32187-152">No método `MainActivity` , adicione a seguinte instrução de importação:</span><span class="sxs-lookup"><span data-stu-id="32187-152">In the `MainActivity` method, add the following import statement:</span></span>
   
        import com.amazon.device.messaging.ADM;
8. <span data-ttu-id="32187-153">Adicione o código a seguir no final do método `OnCreate` :</span><span class="sxs-lookup"><span data-stu-id="32187-153">Add the following code at the end of the `OnCreate` method:</span></span>
   
        final ADM adm = new ADM(this);
        if (adm.getRegistrationId() == null)
        {
           adm.startRegister();
        } else {
            new AsyncTask() {
                  @Override
                  protected Object doInBackground(Object... params) {
                     try {                         MyADMMessageHandler.getNotificationHub(getApplicationContext()).register(adm.getRegistrationId());
                     } catch (Exception e) {
                         Log.e("com.wa.hellokindlefire", "Failed registration with hub", e);
                         return e;
                     }
                     return null;
                 }
               }.execute(null, null, null);
        }

## <a name="add-your-api-key-to-your-app"></a><span data-ttu-id="32187-154">Adicione a chave de API ao seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="32187-154">Add your API key to your app</span></span>
1. <span data-ttu-id="32187-155">No Eclipse, crie um novo arquivo chamado **api_key.txt** no diretório assets de seu projeto.</span><span class="sxs-lookup"><span data-stu-id="32187-155">In Eclipse, create a new file named **api_key.txt** in the directory assets of your project.</span></span>
2. <span data-ttu-id="32187-156">Abra o arquivo e copie Chave da API gerada no portal do desenvolvedor da Amazon.</span><span class="sxs-lookup"><span data-stu-id="32187-156">Open the file and copy the API key that you generated in the Amazon developer portal.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="32187-157">Executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="32187-157">Run the app</span></span>
1. <span data-ttu-id="32187-158">Inicie o emulador.</span><span class="sxs-lookup"><span data-stu-id="32187-158">Start the emulator.</span></span>
2. <span data-ttu-id="32187-159">No emulador, passe o dedo de cima para baixo e clique em **Configurações**, em seguida, clique em **Minha conta** e registre-se com uma conta válida da Amazon.</span><span class="sxs-lookup"><span data-stu-id="32187-159">In the emulator, swipe from the top and click **Settings**, and then click **My account** and register with a valid Amazon account.</span></span>
3. <span data-ttu-id="32187-160">No Eclipse, execute o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="32187-160">In Eclipse, run the app.</span></span>

> [!NOTE]
> <span data-ttu-id="32187-161">Se ocorrer um problema, verifique a hora do emulador (ou dispositivo).</span><span class="sxs-lookup"><span data-stu-id="32187-161">If a problem occurs, check the time of the emulator (or device).</span></span> <span data-ttu-id="32187-162">O valor de hora deve ser preciso.</span><span class="sxs-lookup"><span data-stu-id="32187-162">The time value must be accurate.</span></span> <span data-ttu-id="32187-163">Para alterar a hora do emulador do Kindle, você pode executar o seguinte comando no diretório de ferramentas da plataforma do SDK do Android:</span><span class="sxs-lookup"><span data-stu-id="32187-163">To change the time of the Kindle emulator, you can run the following command from your Android SDK platform-tools directory:</span></span>
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a><span data-ttu-id="32187-164">Enviar uma mensagem</span><span class="sxs-lookup"><span data-stu-id="32187-164">Send a message</span></span>
<span data-ttu-id="32187-165">Para enviar uma mensagem usando o .NET:</span><span class="sxs-lookup"><span data-stu-id="32187-165">To send a message by using .NET:</span></span>

        static void Main(string[] args)
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("[conn string]", "[hub name]");

            hub.SendAdmNativeNotificationAsync("{\"data\":{\"msg\" : \"Hello from .NET!\"}}").Wait();
        }

![][7]

<!-- URLs. -->
<span data-ttu-id="32187-166">[portal do desenvolvedor da Amazon]: https://developer.amazon.com/home.html</span><span class="sxs-lookup"><span data-stu-id="32187-166">[Amazon developer portal]: https://developer.amazon.com/home.html</span></span>
<span data-ttu-id="32187-167">[baixar o SDK]: https://developer.amazon.com/public/resources/development-tools/sdk</span><span class="sxs-lookup"><span data-stu-id="32187-167">[download the SDK]: https://developer.amazon.com/public/resources/development-tools/sdk</span></span>

[0]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal1.png
[1]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal2.png
[2]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal3.png
[3]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal4.png
[4]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal5.png
[5]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-cmd-window.png
[6]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-new-java-class.png
[7]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-notification.png
