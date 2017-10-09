1. <span data-ttu-id="ab43f-101">No seu **aplicativo** projeto, o arquivo hello abrir `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="ab43f-101">In your **app** project, open hello file `AndroidManifest.xml`.</span></span> <span data-ttu-id="ab43f-102">No código Olá Olá duas etapas seguir, substitua  *`**my_app_package**`*  com o nome de saudação do pacote de aplicativo hello para seu projeto.</span><span class="sxs-lookup"><span data-stu-id="ab43f-102">In hello code in hello next two steps, replace *`**my_app_package**`* with hello name of hello app package for your project.</span></span> <span data-ttu-id="ab43f-103">Este é o valor Olá Olá `package` atributo de saudação `manifest` marca.</span><span class="sxs-lookup"><span data-stu-id="ab43f-103">This is hello value of hello `package` attribute of hello `manifest` tag.</span></span>
2. <span data-ttu-id="ab43f-104">Adicionar Olá novas permissões a seguir após Olá existente `uses-permission` elemento:</span><span class="sxs-lookup"><span data-stu-id="ab43f-104">Add hello following new permissions after hello existing `uses-permission` element:</span></span>

        <permission android:name="**my_app_package**.permission.C2D_MESSAGE"
            android:protectionLevel="signature" />
        <uses-permission android:name="**my_app_package**.permission.C2D_MESSAGE" />
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="android.permission.GET_ACCOUNTS" />
        <uses-permission android:name="android.permission.WAKE_LOCK" />
3. <span data-ttu-id="ab43f-105">Adicionar Olá código a seguir após Olá `application` marca de abertura:</span><span class="sxs-lookup"><span data-stu-id="ab43f-105">Add hello following code after hello `application` opening tag:</span></span>

        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
                                         android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="**my_app_package**" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="ab43f-106">Arquivo hello abrir *ToDoActivity.java*e adicione Olá após a instrução de importação:</span><span class="sxs-lookup"><span data-stu-id="ab43f-106">Open hello file *ToDoActivity.java*, and add hello following import statement:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsManager;
5. <span data-ttu-id="ab43f-107">Adicione Olá toohello variável privada classe a seguir.</span><span class="sxs-lookup"><span data-stu-id="ab43f-107">Add hello following private variable toohello class.</span></span> <span data-ttu-id="ab43f-108">Substituir  *`<PROJECT_NUMBER>`*  com número de projeto de saudação atribuído pelo Google app tooyour Olá precede o procedimento.</span><span class="sxs-lookup"><span data-stu-id="ab43f-108">Replace *`<PROJECT_NUMBER>`* with hello project number assigned by Google tooyour app in hello preceding procedure.</span></span>

        public static final String SENDER_ID = "<PROJECT_NUMBER>";
6. <span data-ttu-id="ab43f-109">Alterar a definição de saudação do *MobileServiceClient* de **privada** muito**estático público**, portanto, ele agora esta aparência:</span><span class="sxs-lookup"><span data-stu-id="ab43f-109">Change hello definition of *MobileServiceClient* from **private** too**public static**, so it now looks like this:</span></span>

        public static MobileServiceClient mClient;
7. <span data-ttu-id="ab43f-110">Adicione um novo toohandle notificações da classe.</span><span class="sxs-lookup"><span data-stu-id="ab43f-110">Add a new class toohandle notifications.</span></span> <span data-ttu-id="ab43f-111">No Explorador de projeto, abra Olá **src** > **principal** > **java** nós e o nó de nome de pacote com o botão direito hello.</span><span class="sxs-lookup"><span data-stu-id="ab43f-111">In Project Explorer, open hello **src** > **main** > **java** nodes, and right-click hello package name node.</span></span> <span data-ttu-id="ab43f-112">Clique em **Novo** e em **Classe Java**.</span><span class="sxs-lookup"><span data-stu-id="ab43f-112">Click **New**, and then click **Java Class**.</span></span>
8. <span data-ttu-id="ab43f-113">Em **Nome**, digite `MyHandler` e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="ab43f-113">In **Name**, type `MyHandler`, and then click **OK**.</span></span>

    ![](./media/app-service-mobile-android-configure-push/android-studio-create-class.png)

9. <span data-ttu-id="ab43f-114">No arquivo de MyHandler hello, substitua declaração de classe Olá com:</span><span class="sxs-lookup"><span data-stu-id="ab43f-114">In hello MyHandler file, replace hello class declaration with:</span></span>

        public class MyHandler extends NotificationsHandler {
10. <span data-ttu-id="ab43f-115">Adicionar Olá seguindo as instruções de importação para Olá `MyHandler` classe:</span><span class="sxs-lookup"><span data-stu-id="ab43f-115">Add hello following import statements for hello `MyHandler` class:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsHandler;
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.AsyncTask;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
11. <span data-ttu-id="ab43f-116">Em seguida, adicione esse membro toohello `MyHandler` classe:</span><span class="sxs-lookup"><span data-stu-id="ab43f-116">Next add this member toohello `MyHandler` class:</span></span>

        public static final int NOTIFICATION_ID = 1;
12. <span data-ttu-id="ab43f-117">Em Olá `MyHandler` de classe, adicione Olá Olá de toooverride de código a seguir **onRegistered** método, que registra seu dispositivo com o hub de notificação de serviço móvel de saudação.</span><span class="sxs-lookup"><span data-stu-id="ab43f-117">In hello `MyHandler` class, add hello following code toooverride hello **onRegistered** method, which registers your device with hello mobile service notification hub.</span></span>

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
       <span data-ttu-id="ab43f-118">}</span><span class="sxs-lookup"><span data-stu-id="ab43f-118">}</span></span>
13. <span data-ttu-id="ab43f-119">Em Olá `MyHandler` de classe, adicione Olá Olá de toooverride de código a seguir **onReceive** método, o que faz com que o hello notificação toodisplay quando é recebido.</span><span class="sxs-lookup"><span data-stu-id="ab43f-119">In hello `MyHandler` class, add hello following code toooverride hello **onReceive** method, which causes hello notification toodisplay when it is received.</span></span>

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
       <span data-ttu-id="ab43f-120">}</span><span class="sxs-lookup"><span data-stu-id="ab43f-120">}</span></span>
14. <span data-ttu-id="ab43f-121">No arquivo de TodoActivity.java hello, atualizar Olá **onCreate** método hello *ToDoActivity* tooregister classe de manipulador de notificação de saudação de classe.</span><span class="sxs-lookup"><span data-stu-id="ab43f-121">Back in hello TodoActivity.java file, update hello **onCreate** method of hello *ToDoActivity* class tooregister hello notification handler class.</span></span> <span data-ttu-id="ab43f-122">Tornar tooadd-se de que esse código após Olá *MobileServiceClient* é instanciado.</span><span class="sxs-lookup"><span data-stu-id="ab43f-122">Make sure tooadd this code after hello *MobileServiceClient* is instantiated.</span></span>

        NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);

    <span data-ttu-id="ab43f-123">Seu aplicativo agora está atualizada toosupport notificações de envio.</span><span class="sxs-lookup"><span data-stu-id="ab43f-123">Your app is now updated toosupport push notifications.</span></span>
