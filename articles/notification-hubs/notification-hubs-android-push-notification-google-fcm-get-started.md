---
title: "Introdução aos hubs de notificação do Azure para aplicativos Android e Firebase Cloud Messaging | Microsoft Docs"
description: "Neste tutorial, você aprende a usar os Hubs de Notificação do Azure e o Firebase Cloud Messaging para enviar notificações por push a dispositivos Android."
services: notification-hubs
documentationcenter: android
keywords: "notificações por push, notificação por push, notificação por push do android, fcm, firebase cloud messaging"
author: jwhitedev
manager: kpiteira
editor: 
ms.assetid: 02298560-da61-4bbb-b07c-e79bd520e420
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 12/22/2017
ms.author: jawh
ms.openlocfilehash: 2cac554be145c3bb9ec2c71ef893bba947104a2d
ms.sourcegitcommit: 85012dbead7879f1f6c2965daa61302eb78bd366
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="get-started-with-azure-notification-hubs-for-android-apps-and-firebase-cloud-messaging"></a>Introdução aos hubs de notificação do Azure para aplicativos Android e Firebase Cloud Messaging
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Visão geral
> [!IMPORTANT]
> Este artigo demonstra as notificações por push no FCM (Firebase Cloud Messaging) do Google. Se você ainda estiver usando o Google Cloud Messaging (GCM), veja [Como enviar notificações por push para Android com Hubs de Notificação do Azure e GCM](notification-hubs-android-push-notification-google-gcm-get-started.md).
> 
> 

Este tutorial mostra como usar os Hubs de Notificação do Azure e o Firebase Cloud Messaging para enviar notificações por push a um aplicativo Android. Neste tutorial, você cria um aplicativo Android em branco que recebe notificações por push usando o FCM.

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

O código completo para este tutorial pode ser baixado no GitHub [clicando aqui](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase).

## <a name="prerequisites"></a>pré-requisitos
> [!IMPORTANT]
> Para concluir este tutorial, você precisa ter uma conta ativa do Azure. Se não tiver uma conta, você poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).
> 
> 

* Além de uma conta ativa do Azure mencionada acima, este tutorial requer a última versão do [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).
* Android 2.3 ou superior para Firebase Cloud Messaging.
* A revisão 27 ou superior do Repositório do Google é necessária para o Firebase Cloud Messaging.
* Google Play Services 9.0.2 ou superior para Firebase Cloud Messaging.
* A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais sobre Hubs de Notificação para aplicativos Android.

## <a name="create-a-new-android-studio-project"></a>Criar um novo Projeto Android Studio
1. No Android Studio, inicie um novo projeto Android Studio.
   
    ![Android Studio - novo projeto](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-new-project.png)
2. Escolha o fator forma **Telefone e Tablet** e o **SDK Mínimo** ao qual você deseja oferecer suporte. Em seguida, clique em **Próximo**.
   
    ![Android Studio - fluxo de trabalho de criação de projeto](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-choose-form-factor.png)
3. Escolha **Atividade Vazia** para a atividade principal, clique em **Avançar** e em **Concluir**.

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a>Criar um projeto que ofereça suporte ao Firebase Cloud Messaging
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a>Configurar um novo hub de notificação
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

&emsp;&emsp;6. Em **Serviços de Notificação** selecione **Google (GCM)**. Insira a chave de servidor FCM copiada anteriormente do [Console Firebase](https://firebase.google.com/console/) e clique em **Salvar**.

&emsp;&emsp;![Hubs de Notificação do Azure - Google (GCM)](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-gcm-api.png)

Agora, o hub de notificação está configurado para funcionar com o Firebase Cloud Messaging, e você tem as cadeias de conexão para registrar o aplicativo para receber e enviar notificações por push.

## <a id="connecting-app"></a>Conectar seu aplicativo ao hub de notificação
### <a name="add-google-play-services-to-the-project"></a>Adicionar serviços do Google Play ao projeto
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a>Como adicionar bibliotecas dos Hubs de Notificação do Azure
1. No arquivo `Build.Gradle` para o **aplicativo**, adicione as linhas a seguir à seção **dependencies**.
   
    ```java
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
    ```

2. Adicione o seguinte repositório após a seção **dependências** .
   
    ```java
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }
    ```

### <a name="updating-the-androidmanifestxml"></a>Atualização do arquivo AndroidManifest.xml.
1. Para dar suporte ao FCM, implemente um serviço de escuta de ID da Instância em seu código, que será usado para [obter tokens do registro](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) usando a [API FirebaseInstanceId do Google](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId). Neste tutorial, o nome da classe é `MyInstanceIDService`. 
   
    Adicione a seguinte definição de serviço ao arquivo Androidmanifest.xml, dentro da marcação `<application>` . 
   
    ```xml
        <service android:name=".MyInstanceIDService">
            <intent-filter>
                <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
            </intent-filter>
        </service>
    ```

2. Depois de receber seu token de registro FCM da API FirebaseInstanceId, use-o para [registrar com o Hub de Notificação do Azure](notification-hubs-push-notification-registration-management.md). Você dará suporte a esse registro em segundo plano usando um `IntentService` nomeado `RegistrationIntentService`. Esse serviço também será responsável por atualizar o token de registro do FCM.
   
    Adicione a seguinte definição de serviço ao arquivo Androidmanifest.xml, dentro da marcação `<application>` . 
   
    ```xml
        <service
            android:name=".RegistrationIntentService"
            android:exported="false">
        </service>
    ```

3. Defina também um receptor para receber notificações. Adicione a seguinte definição do receptor ao arquivo AndroidManifest.xml, dentro da marcação `<application>` . Substitua o espaço reservado `<your package>` pelo nome do pacote real mostrado na parte superior do arquivo `AndroidManifest.xml`.

    ```xml
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
    ```

4. Adicione as seguintes permissões necessárias relacionadas ao FCM abaixo da marca `</application>`. Substitua `<your package>` pelo nome do pacote mostrado na parte superior do arquivo `AndroidManifest.xml`.
   
    Para saber mais sobre essas permissões, confira [Configurar um aplicativo de Cliente GCM para Android](https://developers.google.com/cloud-messaging/android/client#manifest) e [Migrar um aplicativo de Cliente GCM para Android para o Firebase Cloud Messaging](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm).
   
    ```xml
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
    ```

### <a name="adding-code"></a>Como adicionar um código
1. Na Exibição de Projeto, expanda **app** > **src** > **main** > **java**. Clique na pasta do seu pacote em **java**, clique em **Novo** e então clique em **Classe Java**. Adicione uma nova classe denominada `NotificationSettings`. 
   
    ![Android Studio - nova classe de Java](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hub-android-new-class.png)
   
    Atualize esses três espaços reservados no código a seguir para a classe `NotificationSettings`:
   
   * **SenderId**: a ID de Remetente obtida anteriormente na guia **Cloud Messaging** de configurações do projeto no [console Firebase](https://firebase.google.com/console/).
   * **HubListenConnectionString**: a cadeia de conexão **DefaultListenAccessSignature** para o hub. Copie essa cadeia de conexão clicando em **Políticas de Acesso** no hub no [portal do Azure].
   * **HubName**: use o nome do hub de notificação que aparece na folha do hub no [portal do Azure].
     
     `NotificationSettings` :
     
    ```java
       public class NotificationSettings {
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Enter your DefaultListenSharedAccessSignature connection string>";
       }
    ```

2. Usando as etapas precedentes, adicione outra classe nova denominada `MyInstanceIDService`. Essa é sua implementação do serviço de escuta de ID da Instância.
   
    O código para essa classe chama `IntentService` para [atualizar o token FCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) em segundo plano.
   
    ```java
        import android.content.Intent;
        import android.util.Log;
        import com.google.firebase.iid.FirebaseInstanceIdService;

        public class MyInstanceIDService extends FirebaseInstanceIdService {

            private static final String TAG = "MyInstanceIDService";

            @Override
            public void onTokenRefresh() {

                Log.d(TAG, "Refreshing GCM Registration Token");

                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        };
    ```

1. Adicione outra classe nova ao projeto denominada `RegistrationIntentService`. Essa é a implementação do seu `IntentService` que processa a [atualização do token FCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) e o [registro no hub de notificação](notification-hubs-push-notification-registration-management.md).
   
    Use o código a seguir para essa classe.
   
    ```java
        import android.app.IntentService;
        import android.content.Intent;
        import android.content.SharedPreferences;
        import android.preference.PreferenceManager;
        import android.util.Log;        
        import com.google.firebase.iid.FirebaseInstanceId;
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
                String storedToken = null;
   
                try {
                    String FCM_token = FirebaseInstanceId.getInstance().getToken();
                    Log.d(TAG, "FCM Registration Token: " + FCM_token);
   
                    // Storing the registration ID that indicates whether the generated token has been
                    // sent to your server. If it is not stored, send the token to your server,
                    // otherwise your server should have already received the token.
                    if (((regID=sharedPreferences.getString("registrationID", null)) == null)){
   
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.d(TAG, "Attempting a new registration with NH using FCM token : " + FCM_token);
                        regID = hub.register(FCM_token).getRegistrationId();
   
                        // If you want to use tags...
                        // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1,tag2").getRegistrationId();
   
                        resultString = "New NH Registration Successfully - RegId : " + regID;
                        Log.d(TAG, resultString);
   
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                        sharedPreferences.edit().putString("FCMtoken", FCM_token ).apply();
                    }
   
                    // Check if the token may have been compromised and needs refreshing.
                    else if ((storedToken=sharedPreferences.getString("FCMtoken", "")) != FCM_token) {
   
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.d(TAG, "NH Registration refreshing with token : " + FCM_token);
                        regID = hub.register(FCM_token).getRegistrationId();
   
                        // If you want to use tags...
                        // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1,tag2").getRegistrationId();
   
                        resultString = "New NH Registration Successfully - RegId : " + regID;
                        Log.d(TAG, resultString);
   
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                        sharedPreferences.edit().putString("FCMtoken", FCM_token ).apply();
                    }
   
                    else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed to complete registration", e);
                    // If an exception happens while fetching the new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt the update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
    ```

2. Em sua classe `MainActivity`, adicione as seguintes instruções `import` acima da declaração da classe.
   
    ```java
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.content.Intent;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
    ```

3. Adicione os seguintes membros privados na parte superior da classe. Use isso para [verificar a disponibilidade do Google Play Services, conforme recomendado pelo Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).
   
    ```java
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private static final String TAG = "MainActivity";
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
    ```

4. Em sua classe `MainActivity` , adicione o seguinte método à disponibilidade dos Serviços do Google Play. 
   
    ```java
        /**
        * Check the device to make sure it has the Google Play Services APK. If
        * it doesn't, display a dialog that allows users to download the APK from
        * the Google Play Store or enable it in the device's system settings.
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
    ```

5. Na classe `MainActivity`, adicione o seguinte código que verifica o Google Play Services antes de chamar o `IntentService` para obter seu token de registro do FCM e registrá-lo com o hub de notificação.
   
    ```java
        public void registerWithNotificationHubs()
        {
            if (checkPlayServices()) {
                // Start IntentService to register this application with FCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
    ```

6. No método `OnCreate` da classe `MainActivity`, adicione o código a seguir para começar o processo de registro quando a atividade for criada.
   
    ```java
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
    ```

7. Para verificar o estado do aplicativo e informar o status em seu aplicativo, adicione esses métodos adicionais a `MainActivity`.
   
    ```java
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
    ```

8. O método `ToastNotify` usa o controle *"Hello World"* `TextView` para informar de forma persistente o status e as notificações no aplicativo. No layout activity_main.xml, adicione a seguinte ID para esse controle.
   
    ```java
       android:id="@+id/text_hello"
    ```

9. Em seguida, adicione uma subclasse para o receptor que você definiu no AndroidManifest.xml. Adicione outra classe nova ao projeto denominada `MyHandler`.
10. Adicione as seguintes instruções de importação na parte superior de `MyHandler.java`:
    
    ```java
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.media.RingtoneManager;
        import android.net.Uri;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
    ```

11. Adicione o código a seguir à classe `MyHandler`, tornando-a uma subclasse de `com.microsoft.windowsazure.notifications.NotificationsHandler`.
    
    Esse código substitui o método `OnReceive` para que o manipulador informe as notificações recebidas. O manipulador também envia a notificação por push ao gerenciador de notificações do Android usando o método `sendNotification()` . O método `sendNotification()` deve ser executado quando o aplicativo não está em execução e uma notificação é recebida.
    
    ```java
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
    ```

12. No Android Studio, na barra de menus, clique em **Compilar** > **Recompilar Projeto** para garantir que não haja erros presentes no código.
13. Execute o aplicativo em seu dispositivo e verifique se ele se registra com êxito no hub de notificação. 
    
    > [!NOTE]
    > O registro poderá falhar na primeira inicialização até que o método `onTokenRefresh()` do serviço de ID da instância seja chamado. A atualização deve iniciar um registro bem-sucedido com o hub de notificação.
    > 
    > 

## <a name="sending-push-notifications"></a>Como enviar notificações por push
Você pode testar o recebimento de notificações por push no aplicativo enviando-as pelo [portal do Azure]. Procure a seção **Solução de problemas** no hub, conforme mostrado abaixo.

![Hubs de notificação do Azure - Testar Enviar](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]


## <a name="testing-your-app"></a>Testando seu aplicativo
#### <a name="push-notifications-in-the-emulator"></a>Notificações por push no emulador
Para testar notificações por push em um emulador, verifique se a imagem de emulador dá suporte ao nível de API do Google que você escolheu para o aplicativo. Se sua imagem não for compatível com as APIs nativas do Google, você verá a exceção **SERVICE\_NOT\_AVAILABLE**.

Além disso, verifique se você adicionou a conta do Google ao emulador em execução em **Configurações** > **Contas**. Caso contrário, suas tentativas de se registrar no GCM podem resultar na exceção **AUTHENTICATION\_FAILED**.

#### <a name="running-the-application"></a>Executando o aplicativo
1. Execute o aplicativo e observe que a ID de registro é relatada para um registro bem-sucedido.
   
    ![Como testar no Android - registro de canal](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-registered.png)
2. Insira uma mensagem de notificação a ser enviada para todos os dispositivos Android registrados no hub.
   
    ![Como testar no Android - envio de uma mensagem](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-set-message.png)
3. Pressione **Enviar Notificação**. Qualquer dispositivo com o aplicativo em execução mostrará uma instância de `AlertDialog` com a mensagem de notificação por push. Dispositivos que não tiverem o aplicativo em execução, mas foram registrados anteriormente para notificações por push, receberão uma notificação no Gerenciador de Notificações do Android. Para exibi-las, passe o dedo do canto superior esquerdo para baixo.
   
    ![Como testar no Android - notificações](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-received-message.png)

## <a name="next-steps"></a>Próximas etapas
Recomendamos o tutorial [Usar os Hubs de Notificação para enviar notificações por push aos usuários] como a próxima etapa. Ele demonstra como enviar notificações de um back-end do ASP.NET usando marcas para ter como alvo usuários específicos.


Se você quiser segmentar os usuários por grupos de interesse, verifique o tutorial [Usar Hubs de Notificação para enviar as notícias mais recentes] .

Para saber mais sobre os Hubs de Notificação, consulte nossas [Diretrizes dos Hubs de Notificação].

<!-- Images. -->



<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Diretrizes dos Hubs de Notificação]: notification-hubs-push-notification-overview.md
[Usar os Hubs de Notificação para enviar notificações por push aos usuários]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md
[Usar Hubs de Notificação para enviar as notícias mais recentes]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md
[portal do Azure]: https://portal.azure.com
