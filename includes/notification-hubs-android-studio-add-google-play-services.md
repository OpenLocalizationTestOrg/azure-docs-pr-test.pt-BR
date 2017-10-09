1. <span data-ttu-id="e8f9d-101">Olá abrir Gerenciador de SDK do Android Olá ícone na barra de ferramentas de saudação do Android Studio ou clicando em **ferramentas** -> **Android** -> **Manager SDK**no menu de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8f9d-101">Open hello Android SDK Manager by clicking hello icon on hello toolbar of Android Studio or by clicking **Tools** -> **Android** -> **SDK Manager** on hello menu.</span></span> <span data-ttu-id="e8f9d-102">Localize a versão de destino de saudação do hello SDK do Android que é usado em seu projeto, abra-o clicando em **Mostrar detalhes do pacote**e escolha **APIs do Google**, se ainda não estiver instalado.</span><span class="sxs-lookup"><span data-stu-id="e8f9d-102">Locate hello target version of hello Android SDK that is used in your project , open it by clicking **Show Package Details**, and choose **Google APIs**, if it is not already installed.</span></span>
2. <span data-ttu-id="e8f9d-103">Clique em Olá **ferramentas SDK** guia. Se você ainda não tiver instalado o Serviço do Google Play, clique em **Serviços do Google Play** , conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="e8f9d-103">Click hello **SDK Tools** tab. If you haven't already installed Google Play Service, click **Google Play Services** as shown below.</span></span> <span data-ttu-id="e8f9d-104">Em seguida, clique em **aplicar** tooinstall.</span><span class="sxs-lookup"><span data-stu-id="e8f9d-104">Then click **Apply** tooinstall.</span></span> 
   
    <span data-ttu-id="e8f9d-105">Observe o caminho do SDK hello, para uso em uma etapa posterior.</span><span class="sxs-lookup"><span data-stu-id="e8f9d-105">Note hello SDK path, for use in a later step.</span></span> 
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-sdk-manager.png)
3. <span data-ttu-id="e8f9d-106">Olá abrir **gradle** arquivo no diretório de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="e8f9d-106">Open hello **build.gradle** file in hello app directory.</span></span>
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-add-google-play-dependency.png)
4. <span data-ttu-id="e8f9d-107">Adicione esta linha em *dependências*:</span><span class="sxs-lookup"><span data-stu-id="e8f9d-107">Add this line under *dependencies*:</span></span> 
   
           compile 'com.google.android.gms:play-services-gcm:9.2.0'
5. <span data-ttu-id="e8f9d-108">Clique em Olá **projeto de sincronização com arquivos Gradle** ícone na barra de ferramentas de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8f9d-108">Click hello **Sync Project with Gradle Files** icon in hello tool bar.</span></span>
6. <span data-ttu-id="e8f9d-109">Abra **AndroidManifest.xml** e adicione essa marca toohello *aplicativo* marca.</span><span class="sxs-lookup"><span data-stu-id="e8f9d-109">Open **AndroidManifest.xml** and add this tag toohello *application* tag.</span></span>
   
        <meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

