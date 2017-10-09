1. Olá abrir Gerenciador de SDK do Android Olá ícone na barra de ferramentas de saudação do Android Studio ou clicando em **ferramentas** -> **Android** -> **Manager SDK**no menu de saudação. Localize a versão de destino de saudação do hello SDK do Android que é usado em seu projeto, abra-o clicando em **Mostrar detalhes do pacote**e escolha **APIs do Google**, se ainda não estiver instalado.
2. Clique em Olá **ferramentas SDK** guia. Se você ainda não tiver instalado o Serviço do Google Play, clique em **Serviços do Google Play** , conforme mostrado abaixo. Em seguida, clique em **aplicar** tooinstall. 
   
    Observe o caminho do SDK hello, para uso em uma etapa posterior. 
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-sdk-manager.png)
3. Olá abrir **gradle** arquivo no diretório de aplicativo hello.
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-add-google-play-dependency.png)
4. Adicione esta linha em *dependências*: 
   
           compile 'com.google.android.gms:play-services-gcm:9.2.0'
5. Clique em Olá **projeto de sincronização com arquivos Gradle** ícone na barra de ferramentas de saudação.
6. Abra **AndroidManifest.xml** e adicione essa marca toohello *aplicativo* marca.
   
        <meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

