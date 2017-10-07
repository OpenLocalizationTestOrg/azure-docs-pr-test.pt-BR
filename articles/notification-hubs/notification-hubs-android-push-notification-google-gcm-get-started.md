---
title: "aaaSending tooAndroid de notificações por push com Hubs de notificação do Azure | Microsoft Docs"
description: "Neste tutorial, você aprenderá como dispositivos de tooAndroid toouse Hubs de notificação do Azure toopush notificações."
services: notification-hubs
documentationcenter: android
keywords: "notificações por push, notificação por push, notificação por push do android"
author: ysxu
manager: erikre
editor: 
ms.assetid: 8268c6ef-af63-433c-b14e-a20b04a0342a
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 07/05/2016
ms.author: yuaxu
ms.openlocfilehash: 6b15a477d86cf1e6efffb21c5bcef0de7761af79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooandroid-with-azure-notification-hubs"></a>TooAndroid envio de notificações por push com Hubs de notificação do Azure
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Visão geral
> [!IMPORTANT]
> Este tópico demonstra as notificações por push com o Google Cloud Messaging (GCM). Se você estiver usando mensagens de nuvem de Firebase (FCM do Google), consulte [tooAndroid de notificações do envio por push com Hubs de notificação do Azure e FCM](notification-hubs-android-push-notification-google-fcm-get-started.md).
> 
> 

Este tutorial mostra como o aplicativo Android do tooan notificações de envio toouse toosend de Hubs de notificação do Azure.
Você criará um aplicativo para Android em branco que recebe notificações por push usando o GCM(Google Cloud Messaging).

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

código de saudação concluído para este tutorial pode ser baixado do GitHub [aqui](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted).

## <a name="prerequisites"></a>Pré-requisitos
> [!IMPORTANT]
> toocomplete neste tutorial, você deve ter uma conta ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).
> 
> 

Além disso tooan conta ativa do Azure mencionado acima, este tutorial requer apenas a versão mais recente de saudação do [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).

A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais sobre Hubs de Notificação para aplicativos Android.

## <a name="creating-a-project-that-supports-google-cloud-messaging"></a>Como criar um projeto que dê suporte ao Google Cloud Messaging
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a>Configurar um novo hub de notificação
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

&emsp;&emsp;6.   Em Olá **configurações** folha, selecione **Notification Services** e **Google (GCM)**. Insira a chave de API de saudação e clique em **salvar**.

&emsp;&emsp;![Hubs de Notificação do Azure - Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

Hub de notificação agora é configurado toowork com GCM e ter tooboth de cadeias de caracteres de conexão Olá registrar seu aplicativo tooreceive e enviar notificações por push.

## <a id="connecting-app"></a>Conecte-se o seu hub de notificação do aplicativo toohello
### <a name="create-a-new-android-project"></a>Criar um novo aplicativo Android
1. No Android Studio, inicie um novo projeto Android Studio.
   
   ![Android Studio - novo projeto][13]
2. Escolha Olá **telefone e Tablet** formulário fator e hello **mínimo SDK** que você deseja toosupport. Em seguida, clique em **Próximo**.
   
   ![Android Studio - fluxo de trabalho de criação de projeto][14]
3. Escolha **atividade vazio** para a atividade principal da saudação, clique em **próximo**e, em seguida, clique em **concluir**.

### <a name="add-google-play-services-toohello-project"></a>Adicionar projeto de toohello de serviços do Google Play
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a>Como adicionar bibliotecas dos Hubs de Notificação do Azure
1. Em Olá `Build.Gradle` arquivo hello **aplicativo**, adicionar Olá Olá linhas a seguir **dependências** seção.
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. Adicionar Olá repositório a seguir após Olá **dependências** seção.
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-hello-androidmanifestxml"></a>Atualizando Olá AndroidManifest.xml.
1. toosupport GCM, devemos implementar um serviço de escuta de ID de instância em nosso código que é usado muito[obter tokens de registro](https://developers.google.com/cloud-messaging/android/client#sample-register) usando [API de ID de instância do Google](https://developers.google.com/instance-id/). Neste tutorial, podemos nomeará classe Olá `MyInstanceIDService`. 
   
    Adicionar Olá após o serviço toohello AndroidManifest.xml arquivo de definição, dentro de saudação `<application>` marca. Substituir saudação `<your package>` espaço reservado com hello seu nome de pacote real mostrado na parte superior de saudação do hello `AndroidManifest.xml` arquivo.
   
        <service android:name="<your package>.MyInstanceIDService" android:exported="false">
            <intent-filter>
                <action android:name="com.google.android.gms.iid.InstanceID"/>
            </intent-filter>
        </service>
2. Depois que recebemos nosso token de registro do GCM Olá API de ID de instância, ele será usado muito[registrar com hello Hub de notificação do Azure](notification-hubs-push-notification-registration-management.md). Forneceremos suporte a esse registro Olá em segundo plano usando um `IntentService` chamado `RegistrationIntentService`. Esse serviço também será responsável por [atualizar nosso token de registro GCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens).
   
    Adicionar Olá após o serviço toohello AndroidManifest.xml arquivo de definição, dentro de saudação `<application>` marca. Substituir saudação `<your package>` espaço reservado com hello seu nome de pacote real mostrado na parte superior de saudação do hello `AndroidManifest.xml` arquivo. 
   
        <service
            android:name="<your package>.RegistrationIntentService"
            android:exported="false">
        </service>
3. Também definiremos notificações de tooreceive um destinatário. Adicionar Olá seguir receptor toohello AndroidManifest.xml arquivo de definição, dentro de saudação `<application>` marca. Substituir saudação `<your package>` espaço reservado com hello seu nome de pacote real mostrado na parte superior de saudação do hello `AndroidManifest.xml` arquivo.
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. Adicionar Olá GCM necessária a seguir relacionadas permissões abaixo Olá `</application>` marca. Certifique-se de que tooreplace `<your package>` com o nome do pacote hello mostrado na parte superior de saudação do hello `AndroidManifest.xml` arquivo.
   
    Para ter mais informações sobre essas permissões, consulte [Configurar um aplicativo Cliente GCM para o Android](https://developers.google.com/cloud-messaging/android/client#manifest).
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
   
        <permission android:name="<your package>.permission.C2D_MESSAGE" android:protectionLevel="signature" />
        <uses-permission android:name="<your package>.permission.C2D_MESSAGE"/>

### <a name="adding-code"></a>Como adicionar um código
1. No hello exibição de projeto, expanda **aplicativo** > **src** > **principal** > **java**. Clique na pasta do seu pacote em **java**, clique em **Novo** e então clique em **Classe Java**. Adicione uma nova classe denominada `NotificationSettings`. 
   
    ![Android Studio - nova classe de Java][6]
   
    Certifique-se de tooupdate Olá esses três espaços reservados em Olá seguindo o código para hello `NotificationSettings` classe:
   
   * **SenderId**: Olá projeto número obtido anteriormente em Olá [Google nuvem Console](http://cloud.google.com/console).
   * **HubListenConnectionString**: Olá **DefaultListenAccessSignature** cadeia de caracteres de conexão para o hub. Você pode copiar essa cadeia de caracteres de conexão clicando em **políticas de acesso** em Olá **configurações** folha do seu hub no hello [Portal do Azure].
   * **HubName**: Use o nome de saudação do hub de notificação que aparece na folha de hub Olá no hello [Portal do Azure].
     
     `NotificationSettings` :
     
       public class NotificationSettings {
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Your default listen connection string>";
       }
2. Usando Olá etapas acima, adicione uma nova classe chamada `MyInstanceIDService`. Essa será nossa implementação do serviço de escuta de ID da Instância.
   
    saudação de código para esta classe chamará nosso `IntentService` muito[atualização Olá GCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) no plano de fundo de saudação.
   
        import android.content.Intent;
        import android.util.Log;
        import com.google.android.gms.iid.InstanceIDListenerService;

        public class MyInstanceIDService extends InstanceIDListenerService {

            private static final String TAG = "MyInstanceIDService";

            @Override
            public void onTokenRefresh() {

                Log.i(TAG, "Refreshing GCM Registration Token");

                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        };


1. Adicione outro novo projeto de classe tooyour denominado `RegistrationIntentService`. Essa será a implementação de saudação para nosso `IntentService` que tratará [atualização token GCM de hello](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) e [registrar com o hub de notificação de saudação](notification-hubs-push-notification-registration-management.md).
   
    Use Olá seguindo o código para esta classe.
   
        import android.app.IntentService;
        import android.content.Intent;
        import android.content.SharedPreferences;
        import android.preference.PreferenceManager;
        import android.util.Log;
   
        import com.google.android.gms.gcm.GoogleCloudMessaging;
        import com.google.android.gms.iid.InstanceID;
        import com.microsoft.windowsazure.messaging.NotificationHub;
   
        public class RegistrationIntentService extends IntentService {
   
            private static final String TAG = "RegIntentService";
   
            private NotificationHub hub;
   
            public RegistrationIntentService() {
                super(TAG);
            }
   
            @Override
            protected void onHandleIntent(Intent intent) {        
                SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(this);
                String resultString = null;
                String regID = null;
   
                try {
                    InstanceID instanceID = InstanceID.getInstance(this);
                    String token = instanceID.getToken(NotificationSettings.SenderId,
                            GoogleCloudMessaging.INSTANCE_ID_SCOPE);        
                    Log.i(TAG, "Got GCM Registration Token: " + token);
   
                    // Storing hello registration id that indicates whether hello generated token has been
                    // sent tooyour server. If it is not stored, send hello token tooyour server,
                    // otherwise your server should have already received hello token.
                    if ((regID=sharedPreferences.getString("registrationID", null)) == null) {        
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.i(TAG, "Attempting tooregister with NH using token : " + token);
   
                        regID = hub.register(token).getRegistrationId();
   
                        // If you want toouse tags...
                        // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1", "tag2").getRegistrationId();
   
                        resultString = "Registered Successfully - RegId : " + regID;
                        Log.i(TAG, resultString);        
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                    } else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed toocomplete token refresh", e);
                    // If an exception happens while fetching hello new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt hello update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. No seu `MainActivity` de classe, adicione o seguinte Olá `import` instruções acima Olá declaração de classe.
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.google.android.gms.gcm.*;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. Adicione Olá membros particulares na parte superior de saudação da classe Olá a seguir. Nós usaremos esses [verificar a disponibilidade de saudação do Google executar serviços como recomendado pelo Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private GoogleCloudMessaging gcm;
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. No seu `MainActivity` classe, adicione Olá disponibilidade do método toohello do Google executar serviços a seguir. 
   
        /**
         * Check hello device toomake sure it has hello Google Play Services APK. If
         * it doesn't, display a dialog that allows users toodownload hello APK from
         * hello Google Play Store or enable it in hello device's system settings.
         */
        private boolean checkPlayServices() {
            GoogleApiAvailability apiAvailability = GoogleApiAvailability.getInstance();
            int resultCode = apiAvailability.isGooglePlayServicesAvailable(this);
            if (resultCode != ConnectionResult.SUCCESS) {
                if (apiAvailability.isUserResolvableError(resultCode)) {
                    apiAvailability.getErrorDialog(this, resultCode, PLAY_SERVICES_RESOLUTION_REQUEST)
                            .show();
                } else {
                    Log.i(TAG, "This device is not supported by Google Play Services.");
                    ToastNotify("This device is not supported by Google Play Services.");
                    finish();
                }
                return false;
            }
            return true;
        }
5. No seu `MainActivity` de classe, adicione Olá seguindo o código que irá verificar para serviços do Google executar antes de chamar o `IntentService` tooget seu token de registro do GCM e registrar com o hub de notificação.
   
        public void registerWithNotificationHubs()
        {
            Log.i(TAG, " Registering with Notification Hubs");
   
            if (checkPlayServices()) {
                // Start IntentService tooregister this application with GCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. Em Olá `OnCreate` método hello `MainActivity` classe, adicione Olá seguindo o processo de registro do código toostart hello quando a atividade é criada.
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. Adicionar esses métodos adicionais toohello `MainActivity` tooverify estado e o relatório de status do aplicativo em seu aplicativo.
   
        @Override
        protected void onStart() {
            super.onStart();
            isVisible = true;
        }
   
        @Override
        protected void onPause() {
            super.onPause();
            isVisible = false;
        }
   
        @Override
        protected void onResume() {
            super.onResume();
            isVisible = true;
        }
   
        @Override
        protected void onStop() {
            super.onStop();
            isVisible = false;
        }
   
        public void ToastNotify(final String notificationMessage) {
            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    Toast.makeText(MainActivity.this, notificationMessage, Toast.LENGTH_LONG).show();
                    TextView helloText = (TextView) findViewById(R.id.text_hello);
                    helloText.setText(notificationMessage);
                }
            });
        }
8. Olá `ToastNotify` usa o método hello *"Hello World"* `TextView` controlar status tooreport e notificações de maneira persistente no aplicativo hello. No layout do activity_main.xml, adicione Olá identificação para o controle a seguir.
   
       android:id="@+id/text_hello"
9. Em seguida, vamos adicionar uma subclasse para nosso receptor que definimos no hello AndroidManifest.xml. Adicionar outro novo projeto de classe tooyour chamado `MyHandler`.
10. Adicionar Olá seguindo as instruções de importação na parte superior de saudação do `MyHandler.java`:
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. Adicionar Olá seguindo o código para hello `MyHandler` classe tornando uma subclasse de `com.microsoft.windowsazure.notifications.NotificationsHandler`.
    
    Esse código substitui Olá `OnReceive` método, para o manipulador de saudação relatará notificações recebidas. manipulador de saudação também envia o Gerenciador de notificação Android Olá push notificação toohello usando Olá `sendNotification()` método. Olá `sendNotification()` método deve ser executado quando o aplicativo hello não está em execução e uma notificação é recebida.
    
        public class MyHandler extends NotificationsHandler {
            public static final int NOTIFICATION_ID = 1;
            private NotificationManager mNotificationManager;
            NotificationCompat.Builder builder;
            Context ctx;
    
            @Override
            public void onReceive(Context context, Bundle bundle) {
                ctx = context;
                String nhMessage = bundle.getString("message");
                sendNotification(nhMessage);
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(nhMessage);
                }
            }
    
            private void sendNotification(String msg) {
    
                Intent intent = new Intent(ctx, MainActivity.class);
                intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
    
                mNotificationManager = (NotificationManager)
                        ctx.getSystemService(Context.NOTIFICATION_SERVICE);
    
                PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                        intent, PendingIntent.FLAG_ONE_SHOT);
    
                Uri defaultSoundUri = RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION);
                NotificationCompat.Builder mBuilder =
                        new NotificationCompat.Builder(ctx)
                                .setSmallIcon(R.mipmap.ic_launcher)
                                .setContentTitle("Notification Hub Demo")
                                .setStyle(new NotificationCompat.BigTextStyle()
                                        .bigText(msg))
                                .setSound(defaultSoundUri)
                                .setContentText(msg);
    
                mBuilder.setContentIntent(contentIntent);
                mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
            }
        }
12. No Android Studio na barra de menus do hello, clique em **criar** > **recompilar o projeto** toomake-se de que nenhum erro está presente em seu código.

## <a name="sending-push-notifications"></a>Como enviar notificações por push
Você pode testar a receber notificações por push em seu aplicativo ao enviá-las por meio de saudação [Portal do Azure] -procure Olá **solução de problemas** seção na folha de hub hello, conforme mostrado abaixo.

![Hubs de notificação do Azure - Testar Enviar](./media/notification-hubs-android-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-hello-app"></a>(Opcional) Enviar notificações por push diretamente do aplicativo hello
Normalmente, você enviaria notificações usando um servidor back-end. Em alguns casos, convém toobe toosend capaz de notificações de push diretamente do aplicativo de cliente hello. Esta seção explica como toosend notificações do cliente usando uma saudação Olá [API de REST de Hub de notificação do Azure](https://msdn.microsoft.com/library/azure/dn223264.aspx).

1. Na Exibição de Projeto do Android Studio, expanda **App** > **src** > **main** > **res** > **layout**. Olá abrir `activity_main.xml` layout de arquivo e clique em Olá **texto** guia tooupdate conteúdo de texto de saudação do arquivo hello. Atualize-o com o código de saudação abaixo, que adiciona novos `Button` e `EditText` controles para enviar por push o hub de notificação de toohello de mensagens de notificação. Adicione este código na parte inferior do hello, imediatamente antes `</RelativeLayout>`.
   
        <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/send_button"
        android:id="@+id/sendbutton"
        android:layout_centerVertical="true"
        android:layout_centerHorizontal="true"
        android:onClick="sendNotificationButtonOnClick" />
   
        <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/editTextNotificationMessage"
        android:layout_above="@+id/sendbutton"
        android:layout_centerHorizontal="true"
        android:layout_marginBottom="42dp"
        android:hint="@string/notification_message_hint" />
2. Na Exibição de Projeto do Android Studio, expanda **App** > **src** > **main** > **res** > **values**. Olá abrir `strings.xml` de arquivos e adicionar valores de cadeia de caracteres de saudação que são referenciados por Olá novo `Button` e `EditText` controles. Adicione estas na parte inferior de saudação do arquivo hello, imediatamente antes `</resources>`.
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. No seu `NotificationSetting.java` de arquivo, adicione Olá toohello de configuração a seguir `NotificationSettings` classe.
   
    Atualização `HubFullAccess` com hello **DefaultFullSharedAccessSignature** cadeia de caracteres de conexão para o hub. Essa cadeia de caracteres de conexão pode ser copiada de saudação [Portal do Azure] clicando **políticas de acesso** em Olá **configurações** folha para o hub de notificação.
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccess Connection string>";
4. No seu `MainActivity.java` de arquivo, adicione o seguinte Olá `import` instruções acima Olá `MainActivity` classe.
   
        import java.io.BufferedOutputStream;
        import java.io.BufferedReader;
        import java.io.InputStreamReader;
        import java.io.OutputStream;
        import java.net.HttpURLConnection;
        import java.net.URL;
        import java.net.URLEncoder;
        import javax.crypto.Mac;
        import javax.crypto.spec.SecretKeySpec;
        import android.util.Base64;
        import android.view.View;
        import android.widget.EditText;
5. No seu `MainActivity.java` de arquivo, adicione Olá seguintes membros na parte superior de saudação do hello `MainActivity` classe.    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. Você deve criar um hub de notificação POST solicitação toosend mensagens tooyour para um tooauthenticate de token de assinatura de acesso (SaS) do Software. Isso é feito pela análise de dados da chave de cadeia de caracteres de conexão Olá Olá e, em seguida, criando Olá token SaS, conforme mencionado em Olá [conceitos comuns](http://msdn.microsoft.com/library/azure/dn495627.aspx) referência da API REST. saudação de código a seguir é um exemplo de implementação.
   
    Em `MainActivity.java`, adicionar Olá após o método toohello `MainActivity` classe tooparse sua cadeia de caracteres de conexão.
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx
         * tooparse hello connection string so a SaS authentication token can be
         * constructed.
         *
         * @param connectionString This must be hello DefaultFullSharedAccess connection
         *                         string for this example.
         */
        private void ParseConnectionString(String connectionString)
        {
            String[] parts = connectionString.split(";");
            if (parts.length != 3)
                throw new RuntimeException("Error parsing connection string: "
                        + connectionString);
   
            for (int i = 0; i < parts.length; i++) {
                if (parts[i].startsWith("Endpoint")) {
                    this.HubEndpoint = "https" + parts[i].substring(11);
                } else if (parts[i].startsWith("SharedAccessKeyName")) {
                    this.HubSasKeyName = parts[i].substring(20);
                } else if (parts[i].startsWith("SharedAccessKey")) {
                    this.HubSasKeyValue = parts[i].substring(16);
                }
            }
        }
7. Em `MainActivity.java`, adicionar Olá após o método toohello `MainActivity` toocreate classe um token de autenticação de SaS.
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx to
         * construct a SaS token from hello access key tooauthenticate a request.
         *
         * @param uri hello unencoded resource URI string for this operation. hello resource
         *            URI is hello full URI of hello Service Bus resource toowhich access is
         *            claimed. For example,
         *            "http://<namespace>.servicebus.windows.net/<hubName>"
         */
        private String generateSasToken(String uri) {
   
            String targetUri;
            String token = null;
            try {
                targetUri = URLEncoder
                        .encode(uri.toString().toLowerCase(), "UTF-8")
                        .toLowerCase();
   
                long expiresOnDate = System.currentTimeMillis();
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60 * 1000;
                long expires = expiresOnDate / 1000;
                String toSign = targetUri + "\n" + expires;
   
                // Get an hmac_sha1 key from hello raw key bytes
                byte[] keyBytes = HubSasKeyValue.getBytes("UTF-8");
                SecretKeySpec signingKey = new SecretKeySpec(keyBytes, "HmacSHA256");
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                Mac mac = Mac.getInstance("HmacSHA256");
                mac.init(signingKey);
   
                // Compute hello hmac on input data bytes
                byte[] rawHmac = mac.doFinal(toSign.getBytes("UTF-8"));
   
                // Using android.util.Base64 for Android Studio instead of
                // Apache commons codec
                String signature = URLEncoder.encode(
                        Base64.encodeToString(rawHmac, Base64.NO_WRAP).toString(), "UTF-8");
   
                // Construct authorization string
                token = "SharedAccessSignature sr=" + targetUri + "&sig="
                        + signature + "&se=" + expires + "&skn=" + HubSasKeyName;
            } catch (Exception e) {
                if (isVisible) {
                    ToastNotify("Exception Generating SaS : " + e.getMessage().toString());
                }
            }
   
            return token;
        }
8. Em `MainActivity.java`, adicionar Olá toohello do método a seguir `MainActivity` Olá de toohandle classe **enviar notificação** clique de botão e enviar notificação por push Olá hub toohello de mensagens usando Olá internos API de REST.
   
        /**
         * Send Notification button click handler. This method parses the
         * DefaultFullSharedAccess connection string and generates a SaS token. The
         * token is added toohello Authorization header on hello POST request toothe
         * notification hub. hello text in hello editTextNotificationMessage control
         * is added as hello JSON body for hello request tooadd a GCM message toohello hub.
         *
         * @param v
         */
        public void sendNotificationButtonOnClick(View v) {
            EditText notificationText = (EditText) findViewById(R.id.editTextNotificationMessage);
            final String json = "{\"data\":{\"message\":\"" + notificationText.getText().toString() + "\"}}";
   
            new Thread()
            {
                public void run()
                {
                    try
                    {
                        // Based on reference documentation...
                        // http://msdn.microsoft.com/library/azure/dn223273.aspx
                        ParseConnectionString(NotificationSettings.HubFullAccess);
                        URL url = new URL(HubEndpoint + NotificationSettings.HubName +
                                "/messages/?api-version=2015-01");
   
                        HttpURLConnection urlConnection = (HttpURLConnection)url.openConnection();
   
                        try {
                            // POST request
                            urlConnection.setDoOutput(true);
   
                            // Authenticate hello POST request with hello SaS token
                            urlConnection.setRequestProperty("Authorization", 
                                generateSasToken(url.toString()));
   
                            // Notification format should be GCM
                            urlConnection.setRequestProperty("ServiceBusNotification-Format", "gcm");
   
                            // Include any tags
                            // Example below targets 3 specific tags
                            // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                            // urlConnection.setRequestProperty("ServiceBusNotification-Tags", 
                            //        "tag1 || tag2 || tag3");
   
                            // Send notification message
                            urlConnection.setFixedLengthStreamingMode(json.length());
                            OutputStream bodyStream = new BufferedOutputStream(urlConnection.getOutputStream());
                            bodyStream.write(json.getBytes());
                            bodyStream.close();
   
                            // Get reponse
                            urlConnection.connect();
                            int responseCode = urlConnection.getResponseCode();
                            if ((responseCode != 200) && (responseCode != 201)) {
                                BufferedReader br = new BufferedReader(new InputStreamReader((urlConnection.getErrorStream())));
                                String line;
                                StringBuilder builder = new StringBuilder("Send Notification returned " +
                                        responseCode + " : ")  ;
                                while ((line = br.readLine()) != null) {
                                    builder.append(line);
                                }
   
                                ToastNotify(builder.toString());
                            }
                        } finally {
                            urlConnection.disconnect();
                        }
                    }
                    catch(Exception e)
                    {
                        if (isVisible) {
                            ToastNotify("Exception Sending Notification : " + e.getMessage().toString());
                        }
                    }
                }
            }.start();
        }

## <a name="testing-your-app"></a>Testando seu aplicativo
#### <a name="push-notifications-in-hello-emulator"></a>Notificações por push no emulador Olá
Se você quiser notificações de push tootest dentro de um emulador, certifique-se de que a imagem do emulador dá suporte ao nível de API do Google de saudação que você escolheu para seu aplicativo. Se a imagem não dá suporte a APIs nativas do Google, você acabará com hello **SERVICE\_não\_disponível** exceção.

Além disso toohello acima, certifique-se de que você adicionou seu tooyour de conta do Google em execução no emulador de **configurações** > **contas**. Caso contrário, o tooregister tentativas com GCM pode resultar em Olá **autenticação\_falha** exceção.

#### <a name="running-hello-application"></a>Executando o aplicativo hello
1. Executar o aplicativo hello e observe a ID de registro de saudação é relatado como um registro foi bem-sucedido.
   
      ![Como testar no Android - registro de canal][18]
2. Insira um toobe de mensagem de notificação enviada tooall dispositivos Android que foram registrados com o hub de saudação.
   
      ![Como testar no Android - envio de uma mensagem][19]

3. Pressione **Enviar Notificação**. Os dispositivos que têm a execução do aplicativo hello mostrará um `AlertDialog` instância com a mensagem de notificação por push hello. Dispositivos que não têm a execução do aplicativo hello, mas que foram registrados anteriormente para notificações por push receberá uma notificação no hello Gerenciador de notificação do Android. Aqueles podem ser exibidos passando do canto superior esquerdo de saudação.
   
      ![Como testar no Android - notificações][21]

## <a name="next-steps"></a>Próximas etapas
É recomendável Olá [usar Hubs de notificação toopush notificações toousers] tutorial como a próxima etapa de saudação. Ele lhe mostrará como toosend notificações de um back-end do ASP.NET usando marcas tootarget determinados usuários.

Se você quiser toosegment os usuários, grupos de interesse, confira Olá [toosend de Hubs de notificação de uso últimas notícias] tutorial.

toolearn obter mais informações sobre Hubs de notificação, consulte nosso [orientação de Hubs de notificação].

<!-- Images. -->
[6]: ./media/notification-hubs-android-get-started/notification-hub-android-new-class.png

[12]: ./media/notification-hubs-android-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-new-project.png
[14]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-choose-form-factor.png
[15]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app4.png
[16]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app5.png
[17]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app6.png

[18]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-registered.png
[19]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-set-message.png

[20]: ./media/notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-received-message.png
[22]: ./media/notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/notification-hubs-android-get-started/notification-hub-scheduler2.png
[29]: ./media/mobile-services-android-get-started-push/mobile-eclipse-import-Play-library.png

[30]: ./media/notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png

[31]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-add-ui.png


<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Azure Classic Portal]: https://manage.windowsazure.com/
[orientação de Hubs de notificação]: http://msdn.microsoft.com/library/jj927170.aspx
[usar Hubs de notificação toopush notificações toousers]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md
[toosend de Hubs de notificação de uso últimas notícias]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md
[Portal do Azure]: https://portal.azure.com
