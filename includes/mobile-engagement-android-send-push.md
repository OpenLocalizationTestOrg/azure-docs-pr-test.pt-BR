
### <a name="update-manifest-file-tooenable-notifications"></a><span data-ttu-id="36b58-101">Arquivo de manifesto tooenable notificações de atualização</span><span class="sxs-lookup"><span data-stu-id="36b58-101">Update manifest file tooenable notifications</span></span>
<span data-ttu-id="36b58-102">Copiar recursos de mensagens no aplicativo hello abaixo para seu manifest entre hello `<application>` e `</application>` marcas.</span><span class="sxs-lookup"><span data-stu-id="36b58-102">Copy hello in-app messaging resources below into your Manifest.xml between hello `<application>` and `</application>` tags.</span></span>

        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/plain" />
              </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/html" />
            </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity" android:theme="@android:style/Theme.Dialog" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
                <category android:name="android.intent.category.DEFAULT"/>
            </intent-filter>
        </activity>
        <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver" android:exported="false">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
            </intent-filter>
        </receiver>
        <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachDownloadReceiver">
            <intent-filter>
                <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
            </intent-filter>
        </receiver>

### <a name="specify-an-icon-for-notifications"></a><span data-ttu-id="36b58-103">Especifique um ícone para notificações</span><span class="sxs-lookup"><span data-stu-id="36b58-103">Specify an icon for notifications</span></span>
<span data-ttu-id="36b58-104">Saudação de colar seguindo o trecho XML em seu manifest entre hello `<application>` e `</application>` marcas.</span><span class="sxs-lookup"><span data-stu-id="36b58-104">Paste hello following XML snippet in your Manifest.xml between hello `<application>` and `</application>` tags.</span></span>

        <meta-data android:name="engagement:reach:notification:icon" android:value="engagement_close"/>

<span data-ttu-id="36b58-105">Isso define o ícone de saudação que é exibido no sistema e notificações no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="36b58-105">This defines hello icon that is displayed both in system and in-app notifications.</span></span> <span data-ttu-id="36b58-106">Embora ele seja opcional para notificações no aplicativo, é obrigatório para notificações do sistema.</span><span class="sxs-lookup"><span data-stu-id="36b58-106">It is optional for in-app notifications however mandatory for system notifications.</span></span> <span data-ttu-id="36b58-107">O Android rejeita as notificações do sistema com ícones inválidos.</span><span class="sxs-lookup"><span data-stu-id="36b58-107">Android will rejects system notifications with invalid icons.</span></span>

<span data-ttu-id="36b58-108">Verifique se você estiver usando um ícone que existe em uma saudação **drawable** pastas (como ``engagement_close.png``).</span><span class="sxs-lookup"><span data-stu-id="36b58-108">Make sure you are using an icon that exists in one of hello **drawable** folders (like ``engagement_close.png``).</span></span> <span data-ttu-id="36b58-109">**mipmap** .</span><span class="sxs-lookup"><span data-stu-id="36b58-109">**mipmap** folder isn't supported.</span></span>

> [!NOTE]
> <span data-ttu-id="36b58-110">Você não deve usar o hello **iniciador** ícone.</span><span class="sxs-lookup"><span data-stu-id="36b58-110">You should not use hello **launcher** icon.</span></span> <span data-ttu-id="36b58-111">Ele tem uma resolução diferente e é geralmente em pastas de mipmap hello, que não há suporte.</span><span class="sxs-lookup"><span data-stu-id="36b58-111">It has a different resolution and is usually in hello mipmap folders, which we don't support.</span></span>
> 
> 

<span data-ttu-id="36b58-112">Para os aplicativos reais, você poderá usar um ícone adequado para notificações conforme as [diretrizes de design do Android](http://developer.android.com/design/patterns/notifications.html).</span><span class="sxs-lookup"><span data-stu-id="36b58-112">For real apps, you can use an icon that is suitable for notifications per [Android design guidelines](http://developer.android.com/design/patterns/notifications.html).</span></span>

> [!TIP]
> <span data-ttu-id="36b58-113">toouse-se de toobe correto resoluções de ícone, você pode examinar [esses exemplos](https://www.google.com/design/icons).</span><span class="sxs-lookup"><span data-stu-id="36b58-113">toobe sure toouse correct icon resolutions, you can look at [these examples](https://www.google.com/design/icons).</span></span>
> <span data-ttu-id="36b58-114">Role para baixo toohello **notificação** seção, clique em um ícone e, em seguida, clique em `PNGS` toodownload Olá ícone drawable definido.</span><span class="sxs-lookup"><span data-stu-id="36b58-114">Scroll down toohello **Notification** section, click an icon, and then click `PNGS` toodownload hello icon drawable set.</span></span> <span data-ttu-id="36b58-115">Você pode ver quais pastas drawable com qual toouse de resolução para cada versão do ícone de saudação.</span><span class="sxs-lookup"><span data-stu-id="36b58-115">You can see what drawable folders with which resolution toouse for each version of hello icon.</span></span>
> 
> 

### <a name="enable-your-app-tooreceive-gcm-push-notifications"></a><span data-ttu-id="36b58-116">Habilitar as notificações de envio por push do aplicativo tooreceive GCM</span><span class="sxs-lookup"><span data-stu-id="36b58-116">Enable your app tooreceive GCM push notifications</span></span>
1. <span data-ttu-id="36b58-117">Cole a seguinte Olá seu manifest entre hello `<application>` e `</application>` marcas depois de substituir Olá **ID do remetente** obtido do console do projeto Firebase.</span><span class="sxs-lookup"><span data-stu-id="36b58-117">Paste hello following into your Manifest.xml between hello `<application>` and `</application>` tags after replacing hello **Sender ID** obtained from your Firebase project console.</span></span> <span data-ttu-id="36b58-118">Olá \n é intencional então certifique-se de que você encerrar o projeto de saudação número com ele.</span><span class="sxs-lookup"><span data-stu-id="36b58-118">hello \n is intentional so make sure that you end hello project number with it.</span></span>
   
        <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
2. <span data-ttu-id="36b58-119">Cole o código de saudação abaixo em seu manifest entre hello `<application>` e `</application>` marcas.</span><span class="sxs-lookup"><span data-stu-id="36b58-119">Paste hello code below into your Manifest.xml between hello `<application>` and `</application>` tags.</span></span> <span data-ttu-id="36b58-120">Substitua o nome do pacote de saudação <Your package name>.</span><span class="sxs-lookup"><span data-stu-id="36b58-120">Replace hello package name <Your package name>.</span></span>
   
        <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
        android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver" android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<Your package name>" />
            </intent-filter>
        </receiver>
3. <span data-ttu-id="36b58-121">Adicionar último conjunto de saudação de permissões que são realçados antes Olá `<application>` marca.</span><span class="sxs-lookup"><span data-stu-id="36b58-121">Add hello last set of permissions that are highlighted before hello `<application>` tag.</span></span> <span data-ttu-id="36b58-122">Substitua `<Your package name>` pelo nome do pacote real de saudação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="36b58-122">Replace `<Your package name>` by hello actual package name of your application.</span></span>
   
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="<Your package name>.permission.C2D_MESSAGE" />
        <permission android:name="<Your package name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

