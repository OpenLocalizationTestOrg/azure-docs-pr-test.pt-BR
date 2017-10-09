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
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a>Introdução aos Hubs de Notificação para aplicativos do Kindle
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Visão geral
Este tutorial mostra como o aplicativo de Kindle tooa notificações de envio toouse toosend de Hubs de notificação do Azure.
Você deve criar um aplicativo Kindle em branco que recebe notificações por push usando Amazon Device Messaging (ADM).

## <a name="prerequisites"></a>Pré-requisitos
Este tutorial requer o seguinte hello:

* Obter Olá SDK do Android (vamos supor que você usará o Eclipse) do hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">site Android</a>.
* Siga as etapas de saudação em <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">configuração a seu ambiente de desenvolvimento</a> tooset seu ambiente de desenvolvimento para Kindle.

## <a name="add-a-new-app-toohello-developer-portal"></a>Adicionar um novo portal do desenvolvedor de toohello de aplicativo
1. Primeiro, crie um aplicativo no hello [portal do desenvolvedor do Amazon].
   
    ![][0]
2. Saudação de cópia **chave de aplicativo**.
   
    ![][1]
3. No portal de saudação, clique em nome de saudação do seu aplicativo e clique em Olá **Device Messaging** guia.
   
    ![][2]
4. Clique em **Criar um Novo Perfil de Segurança** e crie um novo perfil de segurança (por exemplo, **Perfil de segurança TestAdm**). Em seguida, clique em **Salvar**.
   
    ![][3]
5. Clique em **perfis de segurança** tooview perfil de segurança de saudação que você acabou de criar. Saudação de cópia **ID do cliente** e **segredo do cliente** valores para uso posterior.
   
    ![][4]

## <a name="create-an-api-key"></a>Criar uma chave para a API
1. Abra uma prompt de comando com privilégios de administrador.
2. Navegue a pasta do SDK do Android toohello.
3. Digite hello comando a seguir:
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. Para Olá **keystore** senha, digite **android**.
5. Saudação de cópia **MD5** impressão digital.
6. Voltar no portal do desenvolvedor de hello, em Olá **mensagens** , clique em **Android/Kindle** e insira o nome de saudação do pacote de saudação para seu aplicativo (por exemplo, **com.sample.notificationhubtest**) e hello **MD5** valor e, em seguida, clique em **gerar chave de API**.

## <a name="add-credentials-toohello-hub"></a>Adicionar credenciais toohello hub
No portal de hello, adicionar Olá cliente cliente e o segredo do ID toohello **configurar** guia do hub de notificação.

## <a name="set-up-your-application"></a>Configurar o aplicativo
> [!NOTE]
> Ao criar um aplicativo, use pelo menos API de nível 17.
> 
> 

Adicione projeto do Eclipse Olá ADM bibliotecas tooyour:

1. biblioteca de ADM tooobtain Olá [baixar Olá SDK]. Extraia o arquivo zip do hello SDK.
2. No Eclipse, clique com o botão direito do mouse em seu projeto e clique em **Propriedades**. Selecione **caminho de compilação de Java** em saudação à esquerda e, em seguida, selecione hello * * bibliotecas * * guia na parte superior da saudação. Clique em **Adicionar Jar externa**e selecione Olá arquivo `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` do diretório de saudação na qual você extraiu Olá Amazon SDK.
3. Baixe Olá SDK do Android hubs de notificação (link).
4. Descompacte o pacote de saudação e, em seguida, arraste o arquivo hello `notification-hubs-sdk.jar` em Olá `libs` pasta no Eclipse.

Edite seu toosupport do manifesto de aplicativo ADM:

1. Adicione Olá Amazon namespace no elemento de manifesto de raiz de saudação:

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. Adicione permissões como primeiro o elemento no elemento manifesto Olá Olá. Substituir **[seu nome de pacote]** com pacote hello usado toocreate seu aplicativo.
   
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
2. Inserir Olá após o elemento como o primeiro filho Olá Olá de elemento de aplicativo. Lembre-se de toosubstitute **[nome do seu serviço]** com nome de saudação do seu manipulador de mensagens ADM que você cria na próxima seção, hello (incluindo o pacote de saudação) e substitua **[seu nome de pacote]** com hello nome do pacote com a qual você criou seu aplicativo.
   
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

## <a name="create-your-adm-message-handler"></a>Crie o manipulador de mensagens do ADM:
1. Criar uma nova classe que herda de `com.amazon.device.messaging.ADMMessageHandlerBase` e nomeie- `MyADMMessageHandler`, conforme mostrado na figura a seguir de saudação:
   
    ![][6]
2. Adicione o seguinte Olá `import` instruções:
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. Adicione Olá código na classe Olá que você criou a seguir. Lembre-se toosubstitute Olá hub nome e conexão cadeia de caracteres (escutar):
   
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
4. Adicionar Olá toohello de código a seguir `OnMessage()` método:
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. Adicionar Olá toohello de código a seguir `OnRegistered` método:
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. Adicionar Olá toohello de código a seguir `OnUnregistered` método:
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. Em Olá `MainActivity` método, adicione Olá após a instrução de importação:
   
        import com.amazon.device.messaging.ADM;
8. Adicionar Olá após código final Olá Olá `OnCreate` método:
   
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

## <a name="add-your-api-key-tooyour-app"></a>Adicionar seu aplicativo tooyour chave de API
1. No Eclipse, crie um novo arquivo denominado **api_key.txt** em ativos de diretório de saudação do seu projeto.
2. Olá abrir arquivo e cópia Olá chave API geradas no portal do desenvolvedor do Amazon hello.

## <a name="run-hello-app"></a>Executar o aplicativo hello
1. Inicie o emulador de saudação.
2. No emulador do Windows hello, deslize o dedo da parte superior do hello e clique em **configurações**e, em seguida, clique em **minha conta** e registrar com uma conta válida do Amazon.
3. No Eclipse, execute o aplicativo hello.

> [!NOTE]
> Se ocorrer um problema, verifique o tempo de saudação do emulador hello (ou dispositivo). valor de tempo de saudação deve ser preciso. tempo de saudação toochange do emulador de Kindle hello, você pode executar Olá seguinte comando do diretório de ferramentas da plataforma SDK do Android:
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a>Enviar uma mensagem
toosend uma mensagem usando .NET:

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
