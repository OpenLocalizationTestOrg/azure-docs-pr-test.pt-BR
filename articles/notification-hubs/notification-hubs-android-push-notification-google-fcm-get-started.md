---
title: "aaaSending tooAndroid de notificações por push com Hubs de notificação do Azure e mensagens de nuvem Firebase | Microsoft Docs"
description: "Neste tutorial, você aprenderá como toouse Hubs de notificação do Azure e mensagens de nuvem Firebase toopush notificações tooAndroid dispositivos."
services: notification-hubs
documentationcenter: android
keywords: "notificações por push, notificação por push, notificação por push do android, fcm, firebase cloud messaging"
author: ysxu
manager: erikre
editor: 
ms.assetid: 02298560-da61-4bbb-b07c-e79bd520e420
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 07/14/2016
ms.author: yuaxu
ms.openlocfilehash: d2e57437ac7b0ef77abf048f991043620621e58d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooandroid-with-azure-notification-hubs"></a><span data-ttu-id="79092-104">TooAndroid envio de notificações por push com Hubs de notificação do Azure</span><span class="sxs-lookup"><span data-stu-id="79092-104">Sending push notifications tooAndroid with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="79092-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="79092-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="79092-106">Este tópico demonstra as notificações por push com o Firebase Cloud Messaging (FCM) do Google.</span><span class="sxs-lookup"><span data-stu-id="79092-106">This topic demonstrates push notifications with Google Firebase Cloud Messaging (FCM).</span></span> <span data-ttu-id="79092-107">Se você ainda estiver usando o Google Cloud Messaging (GCM), consulte [tooAndroid de notificações do envio por push com Hubs de notificação do Azure e GCM](notification-hubs-android-push-notification-google-gcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="79092-107">If you are still using Google Cloud Messaging (GCM), see [Sending push notifications tooAndroid with Azure Notification Hubs and GCM](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

<span data-ttu-id="79092-108">Este tutorial mostra como toouse Hubs de notificação do Azure e mensagens de nuvem Firebase toosend envio aplicativo Android de tooan de notificações.</span><span class="sxs-lookup"><span data-stu-id="79092-108">This tutorial shows you how toouse Azure Notification Hubs and Firebase Cloud Messaging toosend push notifications tooan Android application.</span></span>
<span data-ttu-id="79092-109">Você criará um aplicativo para Android em branco que recebe notificações por push usando o Firebase Cloud Messaging (FCM).</span><span class="sxs-lookup"><span data-stu-id="79092-109">You'll create a blank Android app that receives push notifications by using Firebase Cloud Messaging (FCM).</span></span>

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="79092-110">código de saudação concluído para este tutorial pode ser baixado do GitHub [aqui](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase).</span><span class="sxs-lookup"><span data-stu-id="79092-110">hello completed code for this tutorial can be downloaded from GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79092-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="79092-111">Prerequisites</span></span>
> [!IMPORTANT]
> <span data-ttu-id="79092-112">toocomplete neste tutorial, você deve ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="79092-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="79092-113">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="79092-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="79092-114">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="79092-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span></span>
> 
> 

* <span data-ttu-id="79092-115">Além disso tooan conta ativa do Azure mencionado acima, este tutorial requer a versão mais recente de saudação do [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span><span class="sxs-lookup"><span data-stu-id="79092-115">In addition tooan active Azure account mentioned above, this tutorial requires hello latest version of [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span></span>
* <span data-ttu-id="79092-116">Android 2.3 ou superior para Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="79092-116">Android 2.3 or higher for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="79092-117">A revisão 27 ou superior do Repositório do Google é necessária para o Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="79092-117">Google Repository revision 27 or higher is required for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="79092-118">Google Play Services 9.0.2 ou superior para Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="79092-118">Google Play Services 9.0.2 or higher for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="79092-119">A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais sobre Hubs de Notificação para aplicativos Android.</span><span class="sxs-lookup"><span data-stu-id="79092-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Android apps.</span></span>

## <a name="create-a-new-android-studio-project"></a><span data-ttu-id="79092-120">Criar um novo Projeto Android Studio</span><span class="sxs-lookup"><span data-stu-id="79092-120">Create a new Android Studio Project</span></span>
1. <span data-ttu-id="79092-121">No Android Studio, inicie um novo projeto Android Studio.</span><span class="sxs-lookup"><span data-stu-id="79092-121">In Android Studio, start a new Android Studio project.</span></span>
   
       ![Android Studio - new project](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-new-project.png)
2. <span data-ttu-id="79092-122">Escolha Olá **telefone e Tablet** formulário fator e hello **mínimo SDK** que você deseja toosupport.</span><span class="sxs-lookup"><span data-stu-id="79092-122">Choose hello **Phone and Tablet** form factor and hello **Minimum SDK** that you want toosupport.</span></span> <span data-ttu-id="79092-123">Em seguida, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="79092-123">Then click **Next**.</span></span>
   
       ![Android Studio - project creation workflow](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-choose-form-factor.png)
3. <span data-ttu-id="79092-124">Escolha **atividade vazio** para a atividade principal da saudação, clique em **próximo**e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="79092-124">Choose **Empty Activity** for hello main activity, click **Next**, and then click **Finish**.</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="79092-125">Criar um projeto que ofereça suporte ao Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="79092-125">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a><span data-ttu-id="79092-126">Configurar um novo hub de notificação</span><span class="sxs-lookup"><span data-stu-id="79092-126">Configure a new notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="79092-127">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="79092-127">&emsp;&emsp;6.</span></span> <span data-ttu-id="79092-128">Em Olá **configurações** folha do seu hub de notificação, selecione **Notification Services** e **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="79092-128">In hello **Settings** blade of your notification hub, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="79092-129">Insira Olá FCM servidor chave copiados anteriormente da saudação [console Firebase](https://firebase.google.com/console/) e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="79092-129">Enter hello FCM server key you copied earlier from hello [Firebase console](https://firebase.google.com/console/) and click **Save**.</span></span>

&emsp;&emsp;![Hubs de Notificação do Azure - Google (GCM)](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-gcm-api.png)

<span data-ttu-id="79092-131">O hub de notificação agora está configurado toowork com Firebase Messagin de nuvem e você tem tooboth de cadeias de caracteres de conexão Olá registrar seu aplicativo tooreceive e enviar notificações por push.</span><span class="sxs-lookup"><span data-stu-id="79092-131">Your notification hub is now configured toowork with Firebase Cloud Messagin, and you have hello connection strings tooboth register your app tooreceive and send push notifications.</span></span>

## <span data-ttu-id="79092-132"><a id="connecting-app"></a>Conecte-se o seu hub de notificação do aplicativo toohello</span><span class="sxs-lookup"><span data-stu-id="79092-132"><a id="connecting-app"></a>Connect your app toohello notification hub</span></span>
### <a name="add-google-play-services-toohello-project"></a><span data-ttu-id="79092-133">Adicionar projeto de toohello de serviços do Google Play</span><span class="sxs-lookup"><span data-stu-id="79092-133">Add Google Play services toohello project</span></span>
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a><span data-ttu-id="79092-134">Como adicionar bibliotecas dos Hubs de Notificação do Azure</span><span class="sxs-lookup"><span data-stu-id="79092-134">Adding Azure Notification Hubs libraries</span></span>
1. <span data-ttu-id="79092-135">Em Olá `Build.Gradle` arquivo hello **aplicativo**, adicionar Olá Olá linhas a seguir **dependências** seção.</span><span class="sxs-lookup"><span data-stu-id="79092-135">In hello `Build.Gradle` file for hello **app**, add hello following lines in hello **dependencies** section.</span></span>
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. <span data-ttu-id="79092-136">Adicionar Olá repositório a seguir após Olá **dependências** seção.</span><span class="sxs-lookup"><span data-stu-id="79092-136">Add hello following repository after hello **dependencies** section.</span></span>
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-hello-androidmanifestxml"></a><span data-ttu-id="79092-137">Atualizando Olá AndroidManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="79092-137">Updating hello AndroidManifest.xml.</span></span>
1. <span data-ttu-id="79092-138">toosupport FCM, devemos implementar um serviço de escuta de ID de instância em nosso código que é usado muito[obter tokens de registro](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) usando [FirebaseInstanceId API do Google](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId).</span><span class="sxs-lookup"><span data-stu-id="79092-138">toosupport FCM, we must implement a Instance ID listener service in our code which is used too[obtain registration tokens](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) using [Google's FirebaseInstanceId API](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId).</span></span> <span data-ttu-id="79092-139">Neste tutorial, podemos nomeará classe Olá `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="79092-139">In this tutorial we will name hello class `MyInstanceIDService`.</span></span> 
   
    <span data-ttu-id="79092-140">Adicionar Olá após o serviço toohello AndroidManifest.xml arquivo de definição, dentro de saudação `<application>` marca.</span><span class="sxs-lookup"><span data-stu-id="79092-140">Add hello following service definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> 
   
        <service android:name=".MyInstanceIDService">
            <intent-filter>
                <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
            </intent-filter>
        </service>
2. <span data-ttu-id="79092-141">Depois que recebemos nosso token de registro FCM Olá FirebaseInstanceId API, iremos utilizá-lo muito[registrar com hello Hub de notificação do Azure](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="79092-141">Once we have received our FCM registration token from hello FirebaseInstanceId API, we will use it too[register with hello Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span></span> <span data-ttu-id="79092-142">Forneceremos suporte a esse registro Olá em segundo plano usando um `IntentService` chamado `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="79092-142">We will support this registration in hello background using an `IntentService` named `RegistrationIntentService`.</span></span> <span data-ttu-id="79092-143">Esse serviço também será responsável por atualizar nosso token de registro FCM.</span><span class="sxs-lookup"><span data-stu-id="79092-143">This service will also be responsible for refreshing our FCM registration token.</span></span>
   
    <span data-ttu-id="79092-144">Adicionar Olá após o serviço toohello AndroidManifest.xml arquivo de definição, dentro de saudação `<application>` marca.</span><span class="sxs-lookup"><span data-stu-id="79092-144">Add hello following service definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> 
   
        <service
            android:name=".RegistrationIntentService"
            android:exported="false">
        </service>
3. <span data-ttu-id="79092-145">Também definiremos notificações de tooreceive um destinatário.</span><span class="sxs-lookup"><span data-stu-id="79092-145">We will also define a receiver tooreceive notifications.</span></span> <span data-ttu-id="79092-146">Adicionar Olá seguir receptor toohello AndroidManifest.xml arquivo de definição, dentro de saudação `<application>` marca.</span><span class="sxs-lookup"><span data-stu-id="79092-146">Add hello following receiver definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> <span data-ttu-id="79092-147">Substituir saudação `<your package>` espaço reservado com hello seu nome de pacote real mostrado na parte superior de saudação do hello `AndroidManifest.xml` arquivo.</span><span class="sxs-lookup"><span data-stu-id="79092-147">Replace hello `<your package>` placeholder with hello your actual package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="79092-148">Adicionar Olá FCM necessária a seguir relacionadas permissões abaixo Olá `</application>` marca.</span><span class="sxs-lookup"><span data-stu-id="79092-148">Add hello following necessary FCM related permissions below hello  `</application>` tag.</span></span> <span data-ttu-id="79092-149">Certifique-se de que tooreplace `<your package>` com o nome do pacote hello mostrado na parte superior de saudação do hello `AndroidManifest.xml` arquivo.</span><span class="sxs-lookup"><span data-stu-id="79092-149">Make sure tooreplace `<your package>` with hello package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
    <span data-ttu-id="79092-150">Para obter mais informações sobre essas permissões, consulte [instalação de um aplicativo cliente GCM para Android](https://developers.google.com/cloud-messaging/android/client#manifest) e [migrar um aplicativo cliente do GCM para Android tooFirebase Cloud Messaging](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm).</span><span class="sxs-lookup"><span data-stu-id="79092-150">For more information on these permissions, see [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest) and [Migrate a GCM Client App for Android tooFirebase Cloud Messaging](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm).</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />

### <a name="adding-code"></a><span data-ttu-id="79092-151">Como adicionar um código</span><span class="sxs-lookup"><span data-stu-id="79092-151">Adding code</span></span>
1. <span data-ttu-id="79092-152">No hello exibição de projeto, expanda **aplicativo** > **src** > **principal** > **java**.</span><span class="sxs-lookup"><span data-stu-id="79092-152">In hello Project View, expand **app** > **src** > **main** > **java**.</span></span> <span data-ttu-id="79092-153">Clique na pasta do seu pacote em **java**, clique em **Novo** e então clique em **Classe Java**.</span><span class="sxs-lookup"><span data-stu-id="79092-153">Right-click your package folder under **java**, click **New**, and then click **Java Class**.</span></span> <span data-ttu-id="79092-154">Adicione uma nova classe denominada `NotificationSettings`.</span><span class="sxs-lookup"><span data-stu-id="79092-154">Add a new class named `NotificationSettings`.</span></span> 
   
    ![Android Studio - nova classe de Java](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hub-android-new-class.png)
   
    <span data-ttu-id="79092-156">Certifique-se de tooupdate Olá esses três espaços reservados em Olá seguindo o código para hello `NotificationSettings` classe:</span><span class="sxs-lookup"><span data-stu-id="79092-156">Make sure tooupdate hello these three placeholders in hello following code for hello `NotificationSettings` class:</span></span>
   
   * <span data-ttu-id="79092-157">**SenderId**: Olá Id do remetente obtido anteriormente em Olá **Cloud Messaging** guia das suas configurações de projeto em Olá [console Firebase](https://firebase.google.com/console/).</span><span class="sxs-lookup"><span data-stu-id="79092-157">**SenderId**: hello Sender Id you obtained earlier in hello **Cloud Messaging** tab of your project settings in hello [Firebase console](https://firebase.google.com/console/).</span></span>
   * <span data-ttu-id="79092-158">**HubListenConnectionString**: Olá **DefaultListenAccessSignature** cadeia de caracteres de conexão para o hub.</span><span class="sxs-lookup"><span data-stu-id="79092-158">**HubListenConnectionString**: hello **DefaultListenAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="79092-159">Você pode copiar essa cadeia de caracteres de conexão clicando em **políticas de acesso** em Olá **configurações** folha do seu hub no hello [Portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="79092-159">You can copy that connection string by clicking **Access Policies** on hello **Settings** blade of your hub on hello [Azure Portal].</span></span>
   * <span data-ttu-id="79092-160">**HubName**: Use o nome de saudação do hub de notificação que aparece na folha de hub Olá no hello [Portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="79092-160">**HubName**: Use hello name of your notification hub that appears in hello hub blade in hello [Azure Portal].</span></span>
     
     <span data-ttu-id="79092-161">`NotificationSettings` :</span><span class="sxs-lookup"><span data-stu-id="79092-161">`NotificationSettings` code:</span></span>
     
       <span data-ttu-id="79092-162">public class NotificationSettings {</span><span class="sxs-lookup"><span data-stu-id="79092-162">public class NotificationSettings {</span></span>
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Enter your DefaultListenSharedAccessSignature connection string>";
       <span data-ttu-id="79092-163">}</span><span class="sxs-lookup"><span data-stu-id="79092-163">}</span></span>
2. <span data-ttu-id="79092-164">Usando Olá etapas acima, adicione uma nova classe chamada `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="79092-164">Using hello steps above, add another new class named `MyInstanceIDService`.</span></span> <span data-ttu-id="79092-165">Essa será nossa implementação do serviço de escuta de ID da Instância.</span><span class="sxs-lookup"><span data-stu-id="79092-165">This will be our Instance ID listener service implementation.</span></span>
   
    <span data-ttu-id="79092-166">saudação de código para esta classe chamará nosso `IntentService` muito[atualização Olá FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) no plano de fundo de saudação.</span><span class="sxs-lookup"><span data-stu-id="79092-166">hello code for this class will call our `IntentService` too[refresh hello FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in hello background.</span></span>
   
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


1. <span data-ttu-id="79092-167">Adicione outro novo projeto de classe tooyour denominado `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="79092-167">Add another new class tooyour project named, `RegistrationIntentService`.</span></span> <span data-ttu-id="79092-168">Essa será a implementação de saudação para nosso `IntentService` que tratará [atualizando token FCM Olá](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) e [registrar com o hub de notificação de saudação](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="79092-168">This will be hello implementation for our `IntentService` that will handle [refreshing hello FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) and [registering with hello notification hub](notification-hubs-push-notification-registration-management.md).</span></span>
   
    <span data-ttu-id="79092-169">Use Olá seguindo o código para esta classe.</span><span class="sxs-lookup"><span data-stu-id="79092-169">Use hello following code for this class.</span></span>
   
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
   
                    // Storing hello registration id that indicates whether hello generated token has been
                    // sent tooyour server. If it is not stored, send hello token tooyour server,
                    // otherwise your server should have already received hello token.
                    if (((regID=sharedPreferences.getString("registrationID", null)) == null)){
   
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.d(TAG, "Attempting a new registration with NH using FCM token : " + FCM_token);
                        regID = hub.register(FCM_token).getRegistrationId();
   
                        // If you want toouse tags...
                        // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1,tag2").getRegistrationId();
   
                        resultString = "New NH Registration Successfully - RegId : " + regID;
                        Log.d(TAG, resultString);
   
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                        sharedPreferences.edit().putString("FCMtoken", FCM_token ).apply();
                    }
   
                    // Check if hello token may have been compromised and needs refreshing.
                    else if ((storedToken=sharedPreferences.getString("FCMtoken", "")) != FCM_token) {
   
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.d(TAG, "NH Registration refreshing with token : " + FCM_token);
                        regID = hub.register(FCM_token).getRegistrationId();
   
                        // If you want toouse tags...
                        // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
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
                    Log.e(TAG, resultString="Failed toocomplete registration", e);
                    // If an exception happens while fetching hello new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt hello update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. <span data-ttu-id="79092-170">No seu `MainActivity` de classe, adicione o seguinte Olá `import` instruções acima Olá declaração de classe.</span><span class="sxs-lookup"><span data-stu-id="79092-170">In your `MainActivity` class, add hello following `import` statements above hello class declaration.</span></span>
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.content.Intent;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. <span data-ttu-id="79092-171">Adicione Olá membros particulares na parte superior de saudação da classe Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="79092-171">Add hello following private members at hello top of hello class.</span></span> <span data-ttu-id="79092-172">Nós usaremos esses [verificar a disponibilidade de saudação do Google executar serviços como recomendado pelo Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span><span class="sxs-lookup"><span data-stu-id="79092-172">We will use these [check hello availability of Google Play Services as recommended by Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span></span>
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private static final String TAG = "MainActivity";
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. <span data-ttu-id="79092-173">No seu `MainActivity` classe, adicione Olá disponibilidade do método toohello do Google executar serviços a seguir.</span><span class="sxs-lookup"><span data-stu-id="79092-173">In your `MainActivity` class, add hello following method toohello availability of Google Play Services.</span></span> 
   
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
5. <span data-ttu-id="79092-174">No seu `MainActivity` de classe, adicione Olá seguindo o código que irá verificar para serviços do Google executar antes de chamar o `IntentService` tooget seu token de registro FCM e registrar com o hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="79092-174">In your `MainActivity` class, add hello following code that will check for Google Play Services before calling your `IntentService` tooget your FCM registration token and register with your notification hub.</span></span>
   
        public void registerWithNotificationHubs()
        {
            if (checkPlayServices()) {
                // Start IntentService tooregister this application with FCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. <span data-ttu-id="79092-175">Em Olá `OnCreate` método hello `MainActivity` classe, adicione Olá seguindo o processo de registro do código toostart hello quando a atividade é criada.</span><span class="sxs-lookup"><span data-stu-id="79092-175">In hello `OnCreate` method of hello `MainActivity` class, add hello following code toostart hello registration process when activity is created.</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. <span data-ttu-id="79092-176">Adicionar esses métodos adicionais toohello `MainActivity` tooverify estado e o relatório de status do aplicativo em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="79092-176">Add these additional methods toohello `MainActivity` tooverify app state and report status in your app.</span></span>
   
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
8. <span data-ttu-id="79092-177">Olá `ToastNotify` usa o método hello *"Hello World"* `TextView` controlar status tooreport e notificações de maneira persistente no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="79092-177">hello `ToastNotify` method uses hello *"Hello World"* `TextView` control tooreport status and notifications persistently in hello app.</span></span> <span data-ttu-id="79092-178">No layout do activity_main.xml, adicione Olá identificação para o controle a seguir.</span><span class="sxs-lookup"><span data-stu-id="79092-178">In your activity_main.xml layout, add hello following id for that control.</span></span>
   
       android:id="@+id/text_hello"
9. <span data-ttu-id="79092-179">Em seguida, vamos adicionar uma subclasse para nosso receptor que definimos no hello AndroidManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="79092-179">Next we will add a subclass for our receiver we defined in hello AndroidManifest.xml.</span></span> <span data-ttu-id="79092-180">Adicionar outro novo projeto de classe tooyour chamado `MyHandler`.</span><span class="sxs-lookup"><span data-stu-id="79092-180">Add another new class tooyour project named `MyHandler`.</span></span>
10. <span data-ttu-id="79092-181">Adicionar Olá seguindo as instruções de importação na parte superior de saudação do `MyHandler.java`:</span><span class="sxs-lookup"><span data-stu-id="79092-181">Add hello following import statements at hello top of `MyHandler.java`:</span></span>
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.media.RingtoneManager;
        import android.net.Uri;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. <span data-ttu-id="79092-182">Adicionar Olá seguindo o código para hello `MyHandler` classe tornando uma subclasse de `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span><span class="sxs-lookup"><span data-stu-id="79092-182">Add hello following code for hello `MyHandler` class making it a subclass of `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span></span>
    
    <span data-ttu-id="79092-183">Esse código substitui Olá `OnReceive` método, para o manipulador de saudação relatará notificações recebidas.</span><span class="sxs-lookup"><span data-stu-id="79092-183">This code overrides hello `OnReceive` method, so hello handler will report notifications that are received.</span></span> <span data-ttu-id="79092-184">manipulador de saudação também envia o Gerenciador de notificação Android Olá push notificação toohello usando Olá `sendNotification()` método.</span><span class="sxs-lookup"><span data-stu-id="79092-184">hello handler also sends hello push notification toohello Android notification manager by using hello `sendNotification()` method.</span></span> <span data-ttu-id="79092-185">Olá `sendNotification()` método deve ser executado quando o aplicativo hello não está em execução e uma notificação é recebida.</span><span class="sxs-lookup"><span data-stu-id="79092-185">hello `sendNotification()` method should be executed when hello app is not running and a notification is received.</span></span>
    
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
12. <span data-ttu-id="79092-186">No Android Studio na barra de menus do hello, clique em **criar** > **recompilar o projeto** toomake-se de que nenhum erro está presente em seu código.</span><span class="sxs-lookup"><span data-stu-id="79092-186">In Android Studio on hello menu bar, click **Build** > **Rebuild Project** toomake sure that no errors are present in your code.</span></span>
13. <span data-ttu-id="79092-187">Execute o aplicativo hello em seu dispositivo e verifique se que ele ser registrado com êxito com o hub de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="79092-187">Run hello app on your device and verify it registers successfully with hello notification hub.</span></span> 
    
    > [!NOTE]
    > <span data-ttu-id="79092-188">Registro poderá falhar na inicialização inicial Olá até Olá `onTokenRefresh()` é chamado de método de instância de serviço de Id.</span><span class="sxs-lookup"><span data-stu-id="79092-188">Registration may fail on hello initial launch until hello `onTokenRefresh()` method of instance Id service is called.</span></span> <span data-ttu-id="79092-189">atualização de saudação deve iniciar um registro bem-sucedido com o hub de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="79092-189">hello refresh should intiate a successful registration with hello notification hub.</span></span>
    > 
    > 

## <a name="sending-push-notifications"></a><span data-ttu-id="79092-190">Como enviar notificações por push</span><span class="sxs-lookup"><span data-stu-id="79092-190">Sending push notifications</span></span>
<span data-ttu-id="79092-191">Você pode testar a receber notificações por push em seu aplicativo ao enviá-las por meio de saudação [Portal do Azure] -procure Olá **solução de problemas** seção na folha de hub hello, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="79092-191">You can test receiving push notifications in your app by sending them via hello [Azure Portal] - look for hello **Troubleshooting** Section in hello hub blade, as shown below.</span></span>

![Hubs de notificação do Azure - Testar Enviar](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-hello-app"></a><span data-ttu-id="79092-193">(Opcional) Enviar notificações por push diretamente do aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="79092-193">(Optional) Send push notifications directly from hello app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="79092-194">Este exemplo de envio de notificações do aplicativo de cliente de saudação é fornecido para fins de aprendizado.</span><span class="sxs-lookup"><span data-stu-id="79092-194">This example of sending notifications from hello client app is provided for learning purposes only.</span></span> <span data-ttu-id="79092-195">Uma vez que isso exigirá Olá `DefaultFullSharedAccessSignature` toobe presente no aplicativo de cliente hello, ele expõe o risco de toohello do hub de notificação que um usuário pode obter acesso não autorizado de toosend notificações tooyour clientes.</span><span class="sxs-lookup"><span data-stu-id="79092-195">Since this will require hello `DefaultFullSharedAccessSignature` toobe present on hello client app, it exposes your notification hub toohello risk that a user may gain access toosend unauthorized notifications tooyour clients.</span></span>
> 
> 

<span data-ttu-id="79092-196">Normalmente, você enviaria notificações usando um servidor back-end.</span><span class="sxs-lookup"><span data-stu-id="79092-196">Normally, you would send notifications using a backend server.</span></span> <span data-ttu-id="79092-197">Em alguns casos, convém toobe toosend capaz de notificações de push diretamente do aplicativo de cliente hello.</span><span class="sxs-lookup"><span data-stu-id="79092-197">For some cases, you might want toobe able toosend push notifications directly from hello client application.</span></span> <span data-ttu-id="79092-198">Esta seção explica como toosend notificações do cliente usando uma saudação Olá [API de REST de Hub de notificação do Azure](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="79092-198">This section explains how toosend notifications from hello client using hello [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span></span>

1. <span data-ttu-id="79092-199">Na Exibição de Projeto do Android Studio, expanda **App** > **src** > **main** > **res** > **layout**.</span><span class="sxs-lookup"><span data-stu-id="79092-199">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **layout**.</span></span> <span data-ttu-id="79092-200">Olá abrir `activity_main.xml` layout de arquivo e clique em Olá **texto** guia tooupdate conteúdo de texto de saudação do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="79092-200">Open hello `activity_main.xml` layout file and click hello **Text** tab tooupdate hello text contents of hello file.</span></span> <span data-ttu-id="79092-201">Atualize-o com o código de saudação abaixo, que adiciona novos `Button` e `EditText` controles para enviar por push o hub de notificação de toohello de mensagens de notificação.</span><span class="sxs-lookup"><span data-stu-id="79092-201">Update it with hello code below, which adds new `Button` and `EditText` controls for sending push notification messages toohello notification hub.</span></span> <span data-ttu-id="79092-202">Adicione este código na parte inferior do hello, imediatamente antes `</RelativeLayout>`.</span><span class="sxs-lookup"><span data-stu-id="79092-202">Add this code at hello bottom, just before `</RelativeLayout>`.</span></span>
   
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
2. <span data-ttu-id="79092-203">Na Exibição de Projeto do Android Studio, expanda **App** > **src** > **main** > **res** > **values**.</span><span class="sxs-lookup"><span data-stu-id="79092-203">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **values**.</span></span> <span data-ttu-id="79092-204">Olá abrir `strings.xml` de arquivos e adicionar valores de cadeia de caracteres de saudação que são referenciados por Olá novo `Button` e `EditText` controles.</span><span class="sxs-lookup"><span data-stu-id="79092-204">Open hello `strings.xml` file and add hello string values that are referenced by hello new `Button` and `EditText` controls.</span></span> <span data-ttu-id="79092-205">Adicione estas na parte inferior de saudação do arquivo hello, imediatamente antes `</resources>`.</span><span class="sxs-lookup"><span data-stu-id="79092-205">Add these at hello bottom of hello file, just before `</resources>`.</span></span>
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. <span data-ttu-id="79092-206">No seu `NotificationSetting.java` de arquivo, adicione Olá toohello de configuração a seguir `NotificationSettings` classe.</span><span class="sxs-lookup"><span data-stu-id="79092-206">In your `NotificationSetting.java` file, add hello following setting toohello `NotificationSettings` class.</span></span>
   
    <span data-ttu-id="79092-207">Atualização `HubFullAccess` com hello **DefaultFullSharedAccessSignature** cadeia de caracteres de conexão para o hub.</span><span class="sxs-lookup"><span data-stu-id="79092-207">Update `HubFullAccess` with hello **DefaultFullSharedAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="79092-208">Essa cadeia de caracteres de conexão pode ser copiada de saudação [Portal do Azure] clicando **políticas de acesso** em Olá **configurações** folha para o hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="79092-208">This connection string can be copied from hello [Azure Portal] by clicking **Access Policies** on hello **Settings** blade for your notification hub.</span></span>
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccessSignature Connection string>";
4. <span data-ttu-id="79092-209">No seu `MainActivity.java` de arquivo, adicione o seguinte Olá `import` instruções acima Olá `MainActivity` classe.</span><span class="sxs-lookup"><span data-stu-id="79092-209">In your `MainActivity.java` file, add hello following `import` statements above hello `MainActivity` class.</span></span>
   
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
5. <span data-ttu-id="79092-210">No seu `MainActivity.java` de arquivo, adicione Olá seguintes membros na parte superior de saudação do hello `MainActivity` classe.</span><span class="sxs-lookup"><span data-stu-id="79092-210">In your `MainActivity.java` file, add hello following members at hello top of hello `MainActivity` class.</span></span>    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. <span data-ttu-id="79092-211">Você deve criar um hub de notificação POST solicitação toosend mensagens tooyour para um tooauthenticate de token de assinatura de acesso (SaS) do Software.</span><span class="sxs-lookup"><span data-stu-id="79092-211">You must create a Software Access Signature (SaS) token tooauthenticate a POST request toosend messages tooyour notification hub.</span></span> <span data-ttu-id="79092-212">Isso é feito pela análise de dados da chave de cadeia de caracteres de conexão Olá Olá e, em seguida, criando Olá token SaS, conforme mencionado em Olá [conceitos comuns](http://msdn.microsoft.com/library/azure/dn495627.aspx) referência da API REST.</span><span class="sxs-lookup"><span data-stu-id="79092-212">This is done by parsing hello key data from hello connection string and then creating hello SaS token, as mentioned in hello [Common Concepts](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API reference.</span></span> <span data-ttu-id="79092-213">saudação de código a seguir é um exemplo de implementação.</span><span class="sxs-lookup"><span data-stu-id="79092-213">hello following code is an example implementation.</span></span>
   
    <span data-ttu-id="79092-214">Em `MainActivity.java`, adicionar Olá após o método toohello `MainActivity` classe tooparse sua cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="79092-214">In `MainActivity.java`, add hello following method toohello `MainActivity` class tooparse your connection string.</span></span>
   
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
7. <span data-ttu-id="79092-215">Em `MainActivity.java`, adicionar Olá após o método toohello `MainActivity` toocreate classe um token de autenticação de SaS.</span><span class="sxs-lookup"><span data-stu-id="79092-215">In `MainActivity.java`, add hello following method toohello `MainActivity` class toocreate a SaS authentication token.</span></span>
   
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
8. <span data-ttu-id="79092-216">Em `MainActivity.java`, adicionar Olá toohello do método a seguir `MainActivity` Olá de toohandle classe **enviar notificação** clique de botão e enviar notificação por push Olá hub toohello de mensagens usando Olá internos API de REST.</span><span class="sxs-lookup"><span data-stu-id="79092-216">In `MainActivity.java`, add hello following method toohello `MainActivity` class toohandle hello **Send Notification** button click and send hello push notification message toohello hub by using hello built-in REST API.</span></span>
   
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

## <a name="testing-your-app"></a><span data-ttu-id="79092-217">Testando seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="79092-217">Testing your app</span></span>
#### <a name="push-notifications-in-hello-emulator"></a><span data-ttu-id="79092-218">Notificações por push no emulador Olá</span><span class="sxs-lookup"><span data-stu-id="79092-218">Push notifications in hello emulator</span></span>
<span data-ttu-id="79092-219">Se você quiser notificações de push tootest dentro de um emulador, certifique-se de que a imagem do emulador dá suporte ao nível de API do Google de saudação que você escolheu para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="79092-219">If you want tootest push notifications inside an emulator, make sure that your emulator image supports hello Google API level that you chose for your app.</span></span> <span data-ttu-id="79092-220">Se a imagem não dá suporte a APIs nativas do Google, você acabará com hello **SERVICE\_não\_disponível** exceção.</span><span class="sxs-lookup"><span data-stu-id="79092-220">If your image doesn't support native Google APIs, you will end up with hello **SERVICE\_NOT\_AVAILABLE** exception.</span></span>

<span data-ttu-id="79092-221">Além disso toohello acima, certifique-se de que você adicionou seu tooyour de conta do Google em execução no emulador de **configurações** > **contas**.</span><span class="sxs-lookup"><span data-stu-id="79092-221">In addition toohello above, ensure that you have added your Google account tooyour running emulator under **Settings** > **Accounts**.</span></span> <span data-ttu-id="79092-222">Caso contrário, o tooregister tentativas com GCM pode resultar em Olá **autenticação\_falha** exceção.</span><span class="sxs-lookup"><span data-stu-id="79092-222">Otherwise, your attempts tooregister with GCM may result in hello **AUTHENTICATION\_FAILED** exception.</span></span>

#### <a name="running-hello-application"></a><span data-ttu-id="79092-223">Executando o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="79092-223">Running hello application</span></span>
1. <span data-ttu-id="79092-224">Executar o aplicativo hello e observe a ID de registro de saudação é relatado como um registro foi bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="79092-224">Run hello app and notice that hello registration ID is reported for a successful registration.</span></span>
   
       ![Testing on Android - Channel registration](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-registered.png)
2. <span data-ttu-id="79092-225">Insira um toobe de mensagem de notificação enviada tooall dispositivos Android que foram registrados com o hub de saudação.</span><span class="sxs-lookup"><span data-stu-id="79092-225">Enter a notification message toobe sent tooall Android devices that have registered with hello hub.</span></span>
   
       ![Testing on Android - sending a message](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-set-message.png)
3. <span data-ttu-id="79092-226">Pressione **Enviar Notificação**.</span><span class="sxs-lookup"><span data-stu-id="79092-226">Press **Send Notification**.</span></span> <span data-ttu-id="79092-227">Os dispositivos que têm a execução do aplicativo hello mostrará um `AlertDialog` instância com a mensagem de notificação por push hello.</span><span class="sxs-lookup"><span data-stu-id="79092-227">Any devices that have hello app running will show an `AlertDialog` instance with hello push notification message.</span></span> <span data-ttu-id="79092-228">Dispositivos que não têm a execução do aplicativo hello, mas que foram registrados anteriormente para notificações por push receberá uma notificação no hello Gerenciador de notificação do Android.</span><span class="sxs-lookup"><span data-stu-id="79092-228">Devices that don't have hello app running but were previously registered for push notifications will receive a notification in hello Android Notification Manager.</span></span> <span data-ttu-id="79092-229">Aqueles podem ser exibidos passando do canto superior esquerdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="79092-229">Those can be viewed by swiping down from hello upper-left corner.</span></span>
   
       ![Testing on Android - notifications](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-received-message.png)

## <a name="next-steps"></a><span data-ttu-id="79092-230">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="79092-230">Next steps</span></span>
<span data-ttu-id="79092-231">É recomendável Olá [usar Hubs de notificação toopush notificações toousers] tutorial como a próxima etapa de saudação.</span><span class="sxs-lookup"><span data-stu-id="79092-231">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step.</span></span> <span data-ttu-id="79092-232">Ele lhe mostrará como toosend notificações de um back-end do ASP.NET usando marcas tootarget determinados usuários.</span><span class="sxs-lookup"><span data-stu-id="79092-232">It will show you how toosend notifications from an ASP.NET backend using tags tootarget specific users.</span></span>

<span data-ttu-id="79092-233">Se você quiser toosegment os usuários, grupos de interesse, confira Olá [toosend de Hubs de notificação de uso últimas notícias] tutorial.</span><span class="sxs-lookup"><span data-stu-id="79092-233">If you want toosegment your users by interest groups, check out hello [Use Notification Hubs toosend breaking news] tutorial.</span></span>

<span data-ttu-id="79092-234">toolearn obter mais informações sobre Hubs de notificação, consulte nosso [orientação de Hubs de notificação].</span><span class="sxs-lookup"><span data-stu-id="79092-234">toolearn more general information about Notification Hubs, see our [Notification Hubs Guidance].</span></span>

<!-- Images. -->



<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Azure Classic Portal]: https://manage.windowsazure.com/
[orientação de Hubs de notificação]: notification-hubs-push-notification-overview.md
[usar Hubs de notificação toopush notificações toousers]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md
[toosend de Hubs de notificação de uso últimas notícias]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md
[Portal do Azure]: https://portal.azure.com
