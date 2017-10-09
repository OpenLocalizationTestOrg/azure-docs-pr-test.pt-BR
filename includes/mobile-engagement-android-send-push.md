
### <a name="update-manifest-file-tooenable-notifications"></a>Arquivo de manifesto tooenable notificações de atualização
Copiar recursos de mensagens no aplicativo hello abaixo para seu manifest entre hello `<application>` e `</application>` marcas.

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

### <a name="specify-an-icon-for-notifications"></a>Especifique um ícone para notificações
Saudação de colar seguindo o trecho XML em seu manifest entre hello `<application>` e `</application>` marcas.

        <meta-data android:name="engagement:reach:notification:icon" android:value="engagement_close"/>

Isso define o ícone de saudação que é exibido no sistema e notificações no aplicativo. Embora ele seja opcional para notificações no aplicativo, é obrigatório para notificações do sistema. O Android rejeita as notificações do sistema com ícones inválidos.

Verifique se você estiver usando um ícone que existe em uma saudação **drawable** pastas (como ``engagement_close.png``). **mipmap** .

> [!NOTE]
> Você não deve usar o hello **iniciador** ícone. Ele tem uma resolução diferente e é geralmente em pastas de mipmap hello, que não há suporte.
> 
> 

Para os aplicativos reais, você poderá usar um ícone adequado para notificações conforme as [diretrizes de design do Android](http://developer.android.com/design/patterns/notifications.html).

> [!TIP]
> toouse-se de toobe correto resoluções de ícone, você pode examinar [esses exemplos](https://www.google.com/design/icons).
> Role para baixo toohello **notificação** seção, clique em um ícone e, em seguida, clique em `PNGS` toodownload Olá ícone drawable definido. Você pode ver quais pastas drawable com qual toouse de resolução para cada versão do ícone de saudação.
> 
> 

### <a name="enable-your-app-tooreceive-gcm-push-notifications"></a>Habilitar as notificações de envio por push do aplicativo tooreceive GCM
1. Cole a seguinte Olá seu manifest entre hello `<application>` e `</application>` marcas depois de substituir Olá **ID do remetente** obtido do console do projeto Firebase. Olá \n é intencional então certifique-se de que você encerrar o projeto de saudação número com ele.
   
        <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
2. Cole o código de saudação abaixo em seu manifest entre hello `<application>` e `</application>` marcas. Substitua o nome do pacote de saudação <Your package name>.
   
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
3. Adicionar último conjunto de saudação de permissões que são realçados antes Olá `<application>` marca. Substitua `<Your package name>` pelo nome do pacote real de saudação do seu aplicativo.
   
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="<Your package name>.permission.C2D_MESSAGE" />
        <permission android:name="<Your package name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

