---
title: "aaaGet iniciado com Hubs de notificação do Azure para aplicativos Kindle | Microsoft Docs"
description: "Neste tutorial, você aprenderá como o aplicativo de Kindle tooa notificações de envio toouse toosend de Hubs de notificação do Azure."
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
ms.openlocfilehash: 7c28d64372cd2d90bab9cd9bf818d333f3478f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a><span data-ttu-id="5b890-103">Introdução aos Hubs de Notificação para aplicativos do Kindle</span><span class="sxs-lookup"><span data-stu-id="5b890-103">Get started with Notification Hubs for Kindle apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="5b890-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="5b890-104">Overview</span></span>
<span data-ttu-id="5b890-105">Este tutorial mostra como o aplicativo de Kindle tooa notificações de envio toouse toosend de Hubs de notificação do Azure.</span><span class="sxs-lookup"><span data-stu-id="5b890-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Kindle application.</span></span>
<span data-ttu-id="5b890-106">Você deve criar um aplicativo Kindle em branco que recebe notificações por push usando Amazon Device Messaging (ADM).</span><span class="sxs-lookup"><span data-stu-id="5b890-106">You'll create a blank Kindle app that receives push notifications by using Amazon Device Messaging (ADM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b890-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5b890-107">Prerequisites</span></span>
<span data-ttu-id="5b890-108">Este tutorial requer o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="5b890-108">This tutorial requires hello following:</span></span>

* <span data-ttu-id="5b890-109">Obter Olá SDK do Android (vamos supor que você usará o Eclipse) do hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">site Android</a>.</span><span class="sxs-lookup"><span data-stu-id="5b890-109">Get hello Android SDK (we assume that you will use Eclipse) from hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a>.</span></span>
* <span data-ttu-id="5b890-110">Siga as etapas de saudação em <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">configuração a seu ambiente de desenvolvimento</a> tooset seu ambiente de desenvolvimento para Kindle.</span><span class="sxs-lookup"><span data-stu-id="5b890-110">Follow hello steps in <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">Setting Up Your Development Environment</a> tooset up your development environment for Kindle.</span></span>

## <a name="add-a-new-app-toohello-developer-portal"></a><span data-ttu-id="5b890-111">Adicionar um novo portal do desenvolvedor de toohello de aplicativo</span><span class="sxs-lookup"><span data-stu-id="5b890-111">Add a new app toohello developer portal</span></span>
1. <span data-ttu-id="5b890-112">Primeiro, crie um aplicativo no hello [portal do desenvolvedor do Amazon].</span><span class="sxs-lookup"><span data-stu-id="5b890-112">First, create an app in hello [Amazon developer portal].</span></span>
   
    ![][0]
2. <span data-ttu-id="5b890-113">Saudação de cópia **chave de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="5b890-113">Copy hello **Application Key**.</span></span>
   
    ![][1]
3. <span data-ttu-id="5b890-114">No portal de saudação, clique em nome de saudação do seu aplicativo e clique em Olá **Device Messaging** guia.</span><span class="sxs-lookup"><span data-stu-id="5b890-114">In hello portal, click hello name of your app, and then click hello **Device Messaging** tab.</span></span>
   
    ![][2]
4. <span data-ttu-id="5b890-115">Clique em **Criar um Novo Perfil de Segurança** e crie um novo perfil de segurança (por exemplo, **Perfil de segurança TestAdm**).</span><span class="sxs-lookup"><span data-stu-id="5b890-115">Click **Create a New Security Profile**, and then create a new security profile (for example, **TestAdm security profile**).</span></span> <span data-ttu-id="5b890-116">Em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="5b890-116">Then click **Save**.</span></span>
   
    ![][3]
5. <span data-ttu-id="5b890-117">Clique em **perfis de segurança** tooview perfil de segurança de saudação que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="5b890-117">Click **Security Profiles** tooview hello security profile that you just created.</span></span> <span data-ttu-id="5b890-118">Saudação de cópia **ID do cliente** e **segredo do cliente** valores para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="5b890-118">Copy hello **Client ID** and **Client Secret** values for later use.</span></span>
   
    ![][4]

## <a name="create-an-api-key"></a><span data-ttu-id="5b890-119">Criar uma chave para a API</span><span class="sxs-lookup"><span data-stu-id="5b890-119">Create an API key</span></span>
1. <span data-ttu-id="5b890-120">Abra uma prompt de comando com privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="5b890-120">Open a command prompt with administrator privileges.</span></span>
2. <span data-ttu-id="5b890-121">Navegue a pasta do SDK do Android toohello.</span><span class="sxs-lookup"><span data-stu-id="5b890-121">Navigate toohello Android SDK folder.</span></span>
3. <span data-ttu-id="5b890-122">Digite hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5b890-122">Enter hello following command:</span></span>
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. <span data-ttu-id="5b890-123">Para Olá **keystore** senha, digite **android**.</span><span class="sxs-lookup"><span data-stu-id="5b890-123">For hello **keystore** password, type **android**.</span></span>
5. <span data-ttu-id="5b890-124">Saudação de cópia **MD5** impressão digital.</span><span class="sxs-lookup"><span data-stu-id="5b890-124">Copy hello **MD5** fingerprint.</span></span>
6. <span data-ttu-id="5b890-125">Voltar no portal do desenvolvedor de hello, em Olá **mensagens** , clique em **Android/Kindle** e insira o nome de saudação do pacote de saudação para seu aplicativo (por exemplo, **com.sample.notificationhubtest**) e hello **MD5** valor e, em seguida, clique em **gerar chave de API**.</span><span class="sxs-lookup"><span data-stu-id="5b890-125">Back in hello developer portal, on hello **Messaging** tab, click **Android/Kindle** and enter hello name of hello package for your app (for example, **com.sample.notificationhubtest**) and hello **MD5** value, and then click **Generate API Key**.</span></span>

## <a name="add-credentials-toohello-hub"></a><span data-ttu-id="5b890-126">Adicionar credenciais toohello hub</span><span class="sxs-lookup"><span data-stu-id="5b890-126">Add credentials toohello hub</span></span>
<span data-ttu-id="5b890-127">No portal de hello, adicionar Olá cliente cliente e o segredo do ID toohello **configurar** guia do hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="5b890-127">In hello portal, add hello client secret and client ID toohello **Configure** tab of your notification hub.</span></span>

## <a name="set-up-your-application"></a><span data-ttu-id="5b890-128">Configurar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="5b890-128">Set up your application</span></span>
> [!NOTE]
> <span data-ttu-id="5b890-129">Ao criar um aplicativo, use pelo menos API de nível 17.</span><span class="sxs-lookup"><span data-stu-id="5b890-129">When you're creating an application, use at least API Level 17.</span></span>
> 
> 

<span data-ttu-id="5b890-130">Adicione projeto do Eclipse Olá ADM bibliotecas tooyour:</span><span class="sxs-lookup"><span data-stu-id="5b890-130">Add hello ADM libraries tooyour Eclipse project:</span></span>

1. <span data-ttu-id="5b890-131">biblioteca de ADM tooobtain Olá [baixar Olá SDK].</span><span class="sxs-lookup"><span data-stu-id="5b890-131">tooobtain hello ADM library, [download hello SDK].</span></span> <span data-ttu-id="5b890-132">Extraia o arquivo zip do hello SDK.</span><span class="sxs-lookup"><span data-stu-id="5b890-132">Extract hello SDK zip file.</span></span>
2. <span data-ttu-id="5b890-133">No Eclipse, clique com o botão direito do mouse em seu projeto e clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="5b890-133">In Eclipse, right-click your project, and then click **Properties**.</span></span> <span data-ttu-id="5b890-134">Selecione **caminho de compilação de Java** em saudação à esquerda e, em seguida, selecione hello * * bibliotecas * * guia na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="5b890-134">Select **Java Build Path** on hello left, and then select hello **Libraries **tab at hello top.</span></span> <span data-ttu-id="5b890-135">Clique em **Adicionar Jar externa**e selecione Olá arquivo `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` do diretório de saudação na qual você extraiu Olá Amazon SDK.</span><span class="sxs-lookup"><span data-stu-id="5b890-135">Click **Add External Jar**, and select hello file `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` from hello directory in which you extracted hello Amazon SDK.</span></span>
3. <span data-ttu-id="5b890-136">Baixe Olá SDK do Android hubs de notificação (link).</span><span class="sxs-lookup"><span data-stu-id="5b890-136">Download hello NotificationHubs Android SDK (link).</span></span>
4. <span data-ttu-id="5b890-137">Descompacte o pacote de saudação e, em seguida, arraste o arquivo hello `notification-hubs-sdk.jar` em Olá `libs` pasta no Eclipse.</span><span class="sxs-lookup"><span data-stu-id="5b890-137">Unzip hello package, and then drag hello file `notification-hubs-sdk.jar` into hello `libs` folder in Eclipse.</span></span>

<span data-ttu-id="5b890-138">Edite seu toosupport do manifesto de aplicativo ADM:</span><span class="sxs-lookup"><span data-stu-id="5b890-138">Edit your app manifest toosupport ADM:</span></span>

1. <span data-ttu-id="5b890-139">Adicione Olá Amazon namespace no elemento de manifesto de raiz de saudação:</span><span class="sxs-lookup"><span data-stu-id="5b890-139">Add hello Amazon namespace in hello root manifest element:</span></span>

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. <span data-ttu-id="5b890-140">Adicione permissões como primeiro o elemento no elemento manifesto Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="5b890-140">Add permissions as hello first element under hello manifest element.</span></span> <span data-ttu-id="5b890-141">Substituir **[seu nome de pacote]** com pacote hello usado toocreate seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5b890-141">Substitute **[YOUR PACKAGE NAME]** with hello package that you used toocreate your app.</span></span>
   
        <permission
         android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE"
         android:protectionLevel="signature" />
   
        <uses-permission android:name="android.permission.INTERNET"/>
   
        <uses-permission android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE" />
   
        <!-- This permission allows your app access tooreceive push notifications
        from ADM. -->
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE" />
   
        <!-- ADM uses WAKE_LOCK tookeep hello processor from sleeping when a message is received. -->
        <uses-permission android:name="android.permission.WAKE_LOCK" />
2. <span data-ttu-id="5b890-142">Inserir Olá após o elemento como o primeiro filho Olá Olá de elemento de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5b890-142">Insert hello following element as hello first child of hello application element.</span></span> <span data-ttu-id="5b890-143">Lembre-se de toosubstitute **[nome do seu serviço]** com nome de saudação do seu manipulador de mensagens ADM que você cria na próxima seção, hello (incluindo o pacote de saudação) e substitua **[seu nome de pacote]** com hello nome do pacote com a qual você criou seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5b890-143">Remember toosubstitute **[YOUR SERVICE NAME]** with hello name of your ADM message handler that you create in hello next section (including hello package), and replace **[YOUR PACKAGE NAME]** with hello package name with which you created your app.</span></span>
   
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
   
            <!-- toointeract with ADM, your app must listen for hello following intents. -->
            <intent-filter>
          <action android:name="com.amazon.device.messaging.intent.REGISTRATION" />
          <action android:name="com.amazon.device.messaging.intent.RECEIVE" />
   
          <!-- Replace hello name in hello category tag with your app's package name. -->
          <category android:name="[YOUR PACKAGE NAME]" />
            </intent-filter>
        </receiver>

## <a name="create-your-adm-message-handler"></a><span data-ttu-id="5b890-144">Crie o manipulador de mensagens do ADM:</span><span class="sxs-lookup"><span data-stu-id="5b890-144">Create your ADM message handler</span></span>
1. <span data-ttu-id="5b890-145">Criar uma nova classe que herda de `com.amazon.device.messaging.ADMMessageHandlerBase` e nomeie- `MyADMMessageHandler`, conforme mostrado na figura a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="5b890-145">Create a new class that inherits from `com.amazon.device.messaging.ADMMessageHandlerBase` and name it `MyADMMessageHandler`, as shown in hello following figure:</span></span>
   
    ![][6]
2. <span data-ttu-id="5b890-146">Adicione o seguinte Olá `import` instruções:</span><span class="sxs-lookup"><span data-stu-id="5b890-146">Add hello following `import` statements:</span></span>
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. <span data-ttu-id="5b890-147">Adicione Olá código na classe Olá que você criou a seguir.</span><span class="sxs-lookup"><span data-stu-id="5b890-147">Add hello following code in hello class that you created.</span></span> <span data-ttu-id="5b890-148">Lembre-se toosubstitute Olá hub nome e conexão cadeia de caracteres (escutar):</span><span class="sxs-lookup"><span data-stu-id="5b890-148">Remember toosubstitute hello hub name and connection string (listen):</span></span>
   
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
4. <span data-ttu-id="5b890-149">Adicionar Olá toohello de código a seguir `OnMessage()` método:</span><span class="sxs-lookup"><span data-stu-id="5b890-149">Add hello following code toohello `OnMessage()` method:</span></span>
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. <span data-ttu-id="5b890-150">Adicionar Olá toohello de código a seguir `OnRegistered` método:</span><span class="sxs-lookup"><span data-stu-id="5b890-150">Add hello following code toohello `OnRegistered` method:</span></span>
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. <span data-ttu-id="5b890-151">Adicionar Olá toohello de código a seguir `OnUnregistered` método:</span><span class="sxs-lookup"><span data-stu-id="5b890-151">Add hello following code toohello `OnUnregistered` method:</span></span>
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. <span data-ttu-id="5b890-152">Em Olá `MainActivity` método, adicione Olá após a instrução de importação:</span><span class="sxs-lookup"><span data-stu-id="5b890-152">In hello `MainActivity` method, add hello following import statement:</span></span>
   
        import com.amazon.device.messaging.ADM;
8. <span data-ttu-id="5b890-153">Adicionar Olá após código final Olá Olá `OnCreate` método:</span><span class="sxs-lookup"><span data-stu-id="5b890-153">Add hello following code at hello end of hello `OnCreate` method:</span></span>
   
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

## <a name="add-your-api-key-tooyour-app"></a><span data-ttu-id="5b890-154">Adicionar seu aplicativo tooyour chave de API</span><span class="sxs-lookup"><span data-stu-id="5b890-154">Add your API key tooyour app</span></span>
1. <span data-ttu-id="5b890-155">No Eclipse, crie um novo arquivo denominado **api_key.txt** em ativos de diretório de saudação do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="5b890-155">In Eclipse, create a new file named **api_key.txt** in hello directory assets of your project.</span></span>
2. <span data-ttu-id="5b890-156">Olá abrir arquivo e cópia Olá chave API geradas no portal do desenvolvedor do Amazon hello.</span><span class="sxs-lookup"><span data-stu-id="5b890-156">Open hello file and copy hello API key that you generated in hello Amazon developer portal.</span></span>

## <a name="run-hello-app"></a><span data-ttu-id="5b890-157">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="5b890-157">Run hello app</span></span>
1. <span data-ttu-id="5b890-158">Inicie o emulador de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b890-158">Start hello emulator.</span></span>
2. <span data-ttu-id="5b890-159">No emulador do Windows hello, deslize o dedo da parte superior do hello e clique em **configurações**e, em seguida, clique em **minha conta** e registrar com uma conta válida do Amazon.</span><span class="sxs-lookup"><span data-stu-id="5b890-159">In hello emulator, swipe from hello top and click **Settings**, and then click **My account** and register with a valid Amazon account.</span></span>
3. <span data-ttu-id="5b890-160">No Eclipse, execute o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="5b890-160">In Eclipse, run hello app.</span></span>

> [!NOTE]
> <span data-ttu-id="5b890-161">Se ocorrer um problema, verifique o tempo de saudação do emulador hello (ou dispositivo).</span><span class="sxs-lookup"><span data-stu-id="5b890-161">If a problem occurs, check hello time of hello emulator (or device).</span></span> <span data-ttu-id="5b890-162">valor de tempo de saudação deve ser preciso.</span><span class="sxs-lookup"><span data-stu-id="5b890-162">hello time value must be accurate.</span></span> <span data-ttu-id="5b890-163">tempo de saudação toochange do emulador de Kindle hello, você pode executar Olá seguinte comando do diretório de ferramentas da plataforma SDK do Android:</span><span class="sxs-lookup"><span data-stu-id="5b890-163">toochange hello time of hello Kindle emulator, you can run hello following command from your Android SDK platform-tools directory:</span></span>
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a><span data-ttu-id="5b890-164">Enviar uma mensagem</span><span class="sxs-lookup"><span data-stu-id="5b890-164">Send a message</span></span>
<span data-ttu-id="5b890-165">toosend uma mensagem usando .NET:</span><span class="sxs-lookup"><span data-stu-id="5b890-165">toosend a message by using .NET:</span></span>

        static void Main(string[] args)
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("[conn string]", "[hub name]");

            hub.SendAdmNativeNotificationAsync("{\"data\":{\"msg\" : \"Hello from .NET!\"}}").Wait();
        }

![][7]

<!-- URLs. -->
[portal do desenvolvedor do Amazon]: https://developer.amazon.com/home.html
[baixar Olá SDK]: https://developer.amazon.com/public/resources/development-tools/sdk

[0]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal1.png
[1]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal2.png
[2]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal3.png
[3]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal4.png
[4]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal5.png
[5]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-cmd-window.png
[6]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-new-java-class.png
[7]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-notification.png
