1. No seu **aplicativo** projeto, o arquivo hello abrir `AndroidManifest.xml`. No código Olá Olá duas etapas seguir, substitua  *`**my_app_package**`*  com o nome de saudação do pacote de aplicativo hello para seu projeto. Este é o valor Olá Olá `package` atributo de saudação `manifest` marca.
2. Adicionar Olá novas permissões a seguir após Olá existente `uses-permission` elemento:

        <permission android:name="**my_app_package**.permission.C2D_MESSAGE"
            android:protectionLevel="signature" />
        <uses-permission android:name="**my_app_package**.permission.C2D_MESSAGE" />
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="android.permission.GET_ACCOUNTS" />
        <uses-permission android:name="android.permission.WAKE_LOCK" />
3. Adicionar Olá código a seguir após Olá `application` marca de abertura:

        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
                                         android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="**my_app_package**" />
            </intent-filter>
        </receiver>
4. Arquivo hello abrir *ToDoActivity.java*e adicione Olá após a instrução de importação:

        import com.microsoft.windowsazure.notifications.NotificationsManager;
5. Adicione Olá toohello variável privada classe a seguir. Substituir  *`<PROJECT_NUMBER>`*  com número de projeto de saudação atribuído pelo Google app tooyour Olá precede o procedimento.

        public static final String SENDER_ID = "<PROJECT_NUMBER>";
6. Alterar a definição de saudação do *MobileServiceClient* de **privada** muito**estático público**, portanto, ele agora esta aparência:

        public static MobileServiceClient mClient;
7. Adicione um novo toohandle notificações da classe. No Explorador de projeto, abra Olá **src** > **principal** > **java** nós e o nó de nome de pacote com o botão direito hello. Clique em **Novo** e em **Classe Java**.
8. Em **Nome**, digite `MyHandler` e clique em **OK**.

    ![](./media/app-service-mobile-android-configure-push/android-studio-create-class.png)

9. No arquivo de MyHandler hello, substitua declaração de classe Olá com:

        public class MyHandler extends NotificationsHandler {
10. Adicionar Olá seguindo as instruções de importação para Olá `MyHandler` classe:

        import com.microsoft.windowsazure.notifications.NotificationsHandler;
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.AsyncTask;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
11. Em seguida, adicione esse membro toohello `MyHandler` classe:

        public static final int NOTIFICATION_ID = 1;
12. Em Olá `MyHandler` de classe, adicione Olá Olá de toooverride de código a seguir **onRegistered** método, que registra seu dispositivo com o hub de notificação de serviço móvel de saudação.

        @Override
        public void onRegistered(Context context,  final String gcmRegistrationId) {
           super.onRegistered(context, gcmRegistrationId);

           new AsyncTask<Void, Void, Void>() {

               protected Void doInBackground(Void... params) {
                   try {
                       ToDoActivity.mClient.getPush().register(gcmRegistrationId);
                       return null;
                   }
                   catch(Exception e) {
                       // handle error                
                   }
                   return null;              
               }
           }.execute();
       }
13. Em Olá `MyHandler` de classe, adicione Olá Olá de toooverride de código a seguir **onReceive** método, o que faz com que o hello notificação toodisplay quando é recebido.

        @Override
        public void onReceive(Context context, Bundle bundle) {
               String msg = bundle.getString("message");

               PendingIntent contentIntent = PendingIntent.getActivity(context,
                       0, // requestCode
                       new Intent(context, ToDoActivity.class),
                       0); // flags

               Notification notification = new NotificationCompat.Builder(context)
                       .setSmallIcon(R.drawable.ic_launcher)
                       .setContentTitle("Notification Hub Demo")
                       .setStyle(new NotificationCompat.BigTextStyle().bigText(msg))
                       .setContentText(msg)
                       .setContentIntent(contentIntent)
                       .build();

               NotificationManager notificationManager = (NotificationManager)
                       context.getSystemService(Context.NOTIFICATION_SERVICE);
               notificationManager.notify(NOTIFICATION_ID, notification);
       }
14. No arquivo de TodoActivity.java hello, atualizar Olá **onCreate** método hello *ToDoActivity* tooregister classe de manipulador de notificação de saudação de classe. Tornar tooadd-se de que esse código após Olá *MobileServiceClient* é instanciado.

        NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);

    Seu aplicativo agora está atualizada toosupport notificações de envio.
