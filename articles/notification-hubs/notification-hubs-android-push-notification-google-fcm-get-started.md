---
title: "Como enviar notificações por push para Android com Hubs de Notificação do Azure e Firebase Cloud Messaging | Microsoft Docs"
description: "Neste tutorial, você aprende a usar os Hubs de Notificação do Azure e o Firebase Cloud Messaging para enviar notificações por push a dispositivos Android."
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
ms.openlocfilehash: 45a3fa5c7190e039fd637c78a41eeb3f6ede9bc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-to-android-with-azure-notification-hubs"></a><span data-ttu-id="91ea7-104">Como enviar notificações por push para Android com Hubs de Notificação do Azure</span><span class="sxs-lookup"><span data-stu-id="91ea7-104">Sending push notifications to Android with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="91ea7-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="91ea7-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="91ea7-106">Este tópico demonstra as notificações por push com o Firebase Cloud Messaging (FCM) do Google.</span><span class="sxs-lookup"><span data-stu-id="91ea7-106">This topic demonstrates push notifications with Google Firebase Cloud Messaging (FCM).</span></span> <span data-ttu-id="91ea7-107">Se você ainda estiver usando o Google Cloud Messaging (GCM), veja [Como enviar notificações por push para Android com Hubs de Notificação do Azure e GCM](notification-hubs-android-push-notification-google-gcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="91ea7-107">If you are still using Google Cloud Messaging (GCM), see [Sending push notifications to Android with Azure Notification Hubs and GCM](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

<span data-ttu-id="91ea7-108">Este tutorial mostra como usar os Hubs de Notificação do Azure e o Firebase Cloud Messaging para enviar notificações por push a um aplicativo Android.</span><span class="sxs-lookup"><span data-stu-id="91ea7-108">This tutorial shows you how to use Azure Notification Hubs and Firebase Cloud Messaging to send push notifications to an Android application.</span></span>
<span data-ttu-id="91ea7-109">Você criará um aplicativo para Android em branco que recebe notificações por push usando o Firebase Cloud Messaging (FCM).</span><span class="sxs-lookup"><span data-stu-id="91ea7-109">You'll create a blank Android app that receives push notifications by using Firebase Cloud Messaging (FCM).</span></span>

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="91ea7-110">O código completo para este tutorial pode ser baixado no GitHub [clicando aqui](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase).</span><span class="sxs-lookup"><span data-stu-id="91ea7-110">The completed code for this tutorial can be downloaded from GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91ea7-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="91ea7-111">Prerequisites</span></span>
> [!IMPORTANT]
> <span data-ttu-id="91ea7-112">Para concluir este tutorial, você precisa ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="91ea7-112">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="91ea7-113">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="91ea7-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="91ea7-114">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="91ea7-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span></span>
> 
> 

* <span data-ttu-id="91ea7-115">Além de uma conta ativa do Azure mencionada acima, este tutorial requer a última versão do [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span><span class="sxs-lookup"><span data-stu-id="91ea7-115">In addition to an active Azure account mentioned above, this tutorial requires the latest version of [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span></span>
* <span data-ttu-id="91ea7-116">Android 2.3 ou superior para Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="91ea7-116">Android 2.3 or higher for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="91ea7-117">A revisão 27 ou superior do Repositório do Google é necessária para o Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="91ea7-117">Google Repository revision 27 or higher is required for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="91ea7-118">Google Play Services 9.0.2 ou superior para Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="91ea7-118">Google Play Services 9.0.2 or higher for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="91ea7-119">A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais sobre Hubs de Notificação para aplicativos Android.</span><span class="sxs-lookup"><span data-stu-id="91ea7-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Android apps.</span></span>

## <a name="create-a-new-android-studio-project"></a><span data-ttu-id="91ea7-120">Criar um novo Projeto Android Studio</span><span class="sxs-lookup"><span data-stu-id="91ea7-120">Create a new Android Studio Project</span></span>
1. <span data-ttu-id="91ea7-121">No Android Studio, inicie um novo projeto Android Studio.</span><span class="sxs-lookup"><span data-stu-id="91ea7-121">In Android Studio, start a new Android Studio project.</span></span>
   
       ![Android Studio - new project](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-new-project.png)
2. <span data-ttu-id="91ea7-122">Escolha o fator forma **Telefone e Tablet** e o **SDK Mínimo** ao qual você deseja oferecer suporte.</span><span class="sxs-lookup"><span data-stu-id="91ea7-122">Choose the **Phone and Tablet** form factor and the **Minimum SDK** that you want to support.</span></span> <span data-ttu-id="91ea7-123">Em seguida, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="91ea7-123">Then click **Next**.</span></span>
   
       ![Android Studio - project creation workflow](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-choose-form-factor.png)
3. <span data-ttu-id="91ea7-124">Escolha **Atividade Vazia** para a atividade principal, clique em **Avançar** e em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="91ea7-124">Choose **Empty Activity** for the main activity, click **Next**, and then click **Finish**.</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="91ea7-125">Criar um projeto que ofereça suporte ao Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="91ea7-125">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a><span data-ttu-id="91ea7-126">Configurar um novo hub de notificação</span><span class="sxs-lookup"><span data-stu-id="91ea7-126">Configure a new notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="91ea7-127">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="91ea7-127">&emsp;&emsp;6.</span></span> <span data-ttu-id="91ea7-128">Na folha **Configurações** do hub de notificação, selecione **Serviços de Notificação** e **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="91ea7-128">In the **Settings** blade of your notification hub, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="91ea7-129">Insira a chave de servidor FCM copiada anteriormente do [Console Firebase](https://firebase.google.com/console/) e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="91ea7-129">Enter the FCM server key you copied earlier from the [Firebase console](https://firebase.google.com/console/) and click **Save**.</span></span>

&emsp;&emsp;![Hubs de Notificação do Azure - Google (GCM)](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-gcm-api.png)

<span data-ttu-id="91ea7-131">Agora, o hub de notificação está configurado para funcionar com o Firebase Cloud Messaging, e você tem as cadeias de conexão para registrar seu aplicativo para receber e enviar notificações por push.</span><span class="sxs-lookup"><span data-stu-id="91ea7-131">Your notification hub is now configured to work with Firebase Cloud Messagin, and you have the connection strings to both register your app to receive and send push notifications.</span></span>

## <span data-ttu-id="91ea7-132"><a id="connecting-app"></a>Conectar seu aplicativo ao hub de notificação</span><span class="sxs-lookup"><span data-stu-id="91ea7-132"><a id="connecting-app"></a>Connect your app to the notification hub</span></span>
### <a name="add-google-play-services-to-the-project"></a><span data-ttu-id="91ea7-133">Adicionar serviços do Google Play ao projeto</span><span class="sxs-lookup"><span data-stu-id="91ea7-133">Add Google Play services to the project</span></span>
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a><span data-ttu-id="91ea7-134">Como adicionar bibliotecas dos Hubs de Notificação do Azure</span><span class="sxs-lookup"><span data-stu-id="91ea7-134">Adding Azure Notification Hubs libraries</span></span>
1. <span data-ttu-id="91ea7-135">No arquivo `Build.Gradle` para o **aplicativo**, adicione as linhas a seguir à seção **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="91ea7-135">In the `Build.Gradle` file for the **app**, add the following lines in the **dependencies** section.</span></span>
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. <span data-ttu-id="91ea7-136">Adicione o seguinte repositório após a seção **dependências** .</span><span class="sxs-lookup"><span data-stu-id="91ea7-136">Add the following repository after the **dependencies** section.</span></span>
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-the-androidmanifestxml"></a><span data-ttu-id="91ea7-137">Atualização do arquivo AndroidManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="91ea7-137">Updating the AndroidManifest.xml.</span></span>
1. <span data-ttu-id="91ea7-138">Para oferecer suporte ao FCM, devemos implementar um serviço de escuta de ID da Instância em nosso código que será usado para [obter os tokens do registro](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) usando a [API FirebaseInstanceId do Google](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId).</span><span class="sxs-lookup"><span data-stu-id="91ea7-138">To support FCM, we must implement a Instance ID listener service in our code which is used to [obtain registration tokens](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) using [Google's FirebaseInstanceId API](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId).</span></span> <span data-ttu-id="91ea7-139">Neste tutorial, daremos à classe o nome `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="91ea7-139">In this tutorial we will name the class `MyInstanceIDService`.</span></span> 
   
    <span data-ttu-id="91ea7-140">Adicione a seguinte definição de serviço ao arquivo Androidmanifest.xml, dentro da marcação `<application>` .</span><span class="sxs-lookup"><span data-stu-id="91ea7-140">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> 
   
        <service android:name=".MyInstanceIDService">
            <intent-filter>
                <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
            </intent-filter>
        </service>
2. <span data-ttu-id="91ea7-141">Após recebermos nosso token de registro FCM da API FirebaseInstanceId, iremos usá-lo para nos [registrar no Hub de Notificação do Azure](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="91ea7-141">Once we have received our FCM registration token from the FirebaseInstanceId API, we will use it to [register with the Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span></span> <span data-ttu-id="91ea7-142">Ofereceremos suporte a esse registro em segundo plano usando um `IntentService` chamado `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="91ea7-142">We will support this registration in the background using an `IntentService` named `RegistrationIntentService`.</span></span> <span data-ttu-id="91ea7-143">Esse serviço também será responsável por atualizar nosso token de registro FCM.</span><span class="sxs-lookup"><span data-stu-id="91ea7-143">This service will also be responsible for refreshing our FCM registration token.</span></span>
   
    <span data-ttu-id="91ea7-144">Adicione a seguinte definição de serviço ao arquivo Androidmanifest.xml, dentro da marcação `<application>` .</span><span class="sxs-lookup"><span data-stu-id="91ea7-144">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> 
   
        <service
            android:name=".RegistrationIntentService"
            android:exported="false">
        </service>
3. <span data-ttu-id="91ea7-145">Também definiremos um receptor para receber as notificações.</span><span class="sxs-lookup"><span data-stu-id="91ea7-145">We will also define a receiver to receive notifications.</span></span> <span data-ttu-id="91ea7-146">Adicione a seguinte definição do receptor ao arquivo AndroidManifest.xml, dentro da marcação `<application>` .</span><span class="sxs-lookup"><span data-stu-id="91ea7-146">Add the following receiver definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> <span data-ttu-id="91ea7-147">Substitua o espaço reservado `<your package>` pelo nome do pacote real mostrado na parte superior do arquivo `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="91ea7-147">Replace the `<your package>` placeholder with the your actual package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="91ea7-148">Adicione as seguintes permissões necessárias relacionadas ao FCM abaixo da marca `</application>` .</span><span class="sxs-lookup"><span data-stu-id="91ea7-148">Add the following necessary FCM related permissions below the  `</application>` tag.</span></span> <span data-ttu-id="91ea7-149">Substitua `<your package>` pelo nome do pacote mostrado na parte superior do arquivo `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="91ea7-149">Make sure to replace `<your package>` with the package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
    <span data-ttu-id="91ea7-150">Para saber mais sobre essas permissões, confira [Configurar um aplicativo de Cliente GCM para Android](https://developers.google.com/cloud-messaging/android/client#manifest) e [Migrar um aplicativo de Cliente GCM para Android para o Firebase Cloud Messaging](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm).</span><span class="sxs-lookup"><span data-stu-id="91ea7-150">For more information on these permissions, see [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest) and [Migrate a GCM Client App for Android to Firebase Cloud Messaging](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm).</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />

### <a name="adding-code"></a><span data-ttu-id="91ea7-151">Como adicionar um código</span><span class="sxs-lookup"><span data-stu-id="91ea7-151">Adding code</span></span>
1. <span data-ttu-id="91ea7-152">Na Exibição de Projeto, expanda **app** > **src** > **main** > **java**.</span><span class="sxs-lookup"><span data-stu-id="91ea7-152">In the Project View, expand **app** > **src** > **main** > **java**.</span></span> <span data-ttu-id="91ea7-153">Clique na pasta do seu pacote em **java**, clique em **Novo** e então clique em **Classe Java**.</span><span class="sxs-lookup"><span data-stu-id="91ea7-153">Right-click your package folder under **java**, click **New**, and then click **Java Class**.</span></span> <span data-ttu-id="91ea7-154">Adicione uma nova classe denominada `NotificationSettings`.</span><span class="sxs-lookup"><span data-stu-id="91ea7-154">Add a new class named `NotificationSettings`.</span></span> 
   
    ![Android Studio - nova classe de Java](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hub-android-new-class.png)
   
    <span data-ttu-id="91ea7-156">Atualize esses três espaços reservados no código a seguir para a classe `NotificationSettings` :</span><span class="sxs-lookup"><span data-stu-id="91ea7-156">Make sure to update the these three placeholders in the following code for the `NotificationSettings` class:</span></span>
   
   * <span data-ttu-id="91ea7-157">**SenderId**: a ID de Remetente obtida anteriormente na guia **Cloud Messaging** de configurações de seu projeto no [console Firebase](https://firebase.google.com/console/).</span><span class="sxs-lookup"><span data-stu-id="91ea7-157">**SenderId**: The Sender Id you obtained earlier in the **Cloud Messaging** tab of your project settings in the [Firebase console](https://firebase.google.com/console/).</span></span>
   * <span data-ttu-id="91ea7-158">**HubListenConnectionString**: a cadeia de conexão **DefaultListenAccessSignature** para o hub.</span><span class="sxs-lookup"><span data-stu-id="91ea7-158">**HubListenConnectionString**: The **DefaultListenAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="91ea7-159">Você pode copiar essa cadeia de conexão clicando em **Políticas de Acesso** na folha **Configurações** do hub no [Portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="91ea7-159">You can copy that connection string by clicking **Access Policies** on the **Settings** blade of your hub on the [Azure Portal].</span></span>
   * <span data-ttu-id="91ea7-160">**HubName**: use o nome do hub de notificação que aparece na folha do hub no [Portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="91ea7-160">**HubName**: Use the name of your notification hub that appears in the hub blade in the [Azure Portal].</span></span>
     
     <span data-ttu-id="91ea7-161">`NotificationSettings` :</span><span class="sxs-lookup"><span data-stu-id="91ea7-161">`NotificationSettings` code:</span></span>
     
       <span data-ttu-id="91ea7-162">public class NotificationSettings {</span><span class="sxs-lookup"><span data-stu-id="91ea7-162">public class NotificationSettings {</span></span>
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Enter your DefaultListenSharedAccessSignature connection string>";
       <span data-ttu-id="91ea7-163">}</span><span class="sxs-lookup"><span data-stu-id="91ea7-163">}</span></span>
2. <span data-ttu-id="91ea7-164">Usando as etapas acima, adicione outra classe nova denominada `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="91ea7-164">Using the steps above, add another new class named `MyInstanceIDService`.</span></span> <span data-ttu-id="91ea7-165">Essa será nossa implementação do serviço de escuta de ID da Instância.</span><span class="sxs-lookup"><span data-stu-id="91ea7-165">This will be our Instance ID listener service implementation.</span></span>
   
    <span data-ttu-id="91ea7-166">O código para essa classe chamará nosso `IntentService` para [atualizar o token FCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="91ea7-166">The code for this class will call our `IntentService` to [refresh the FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in the background.</span></span>
   
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


1. <span data-ttu-id="91ea7-167">Adicione outra classe nova ao projeto denominada `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="91ea7-167">Add another new class to your project named, `RegistrationIntentService`.</span></span> <span data-ttu-id="91ea7-168">Será a implementação de nosso `IntentService` que lidará com a [atualização do token FCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) e o [registro no hub de notificação](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="91ea7-168">This will be the implementation for our `IntentService` that will handle [refreshing the FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) and [registering with the notification hub](notification-hubs-push-notification-registration-management.md).</span></span>
   
    <span data-ttu-id="91ea7-169">Use o código a seguir para essa classe.</span><span class="sxs-lookup"><span data-stu-id="91ea7-169">Use the following code for this class.</span></span>
   
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
   
                    // Storing the registration id that indicates whether the generated token has been
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
2. <span data-ttu-id="91ea7-170">Em sua classe `MainActivity`, adicione as seguintes instruções `import` acima da declaração da classe.</span><span class="sxs-lookup"><span data-stu-id="91ea7-170">In your `MainActivity` class, add the following `import` statements above the class declaration.</span></span>
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.content.Intent;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. <span data-ttu-id="91ea7-171">Adicione os seguintes membros privados na parte superior da classe.</span><span class="sxs-lookup"><span data-stu-id="91ea7-171">Add the following private members at the top of the class.</span></span> <span data-ttu-id="91ea7-172">Usaremos isto para [verificar a disponibilidade dos Serviços do Google Play, conforme recomendado pela Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span><span class="sxs-lookup"><span data-stu-id="91ea7-172">We will use these [check the availability of Google Play Services as recommended by Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span></span>
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private static final String TAG = "MainActivity";
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. <span data-ttu-id="91ea7-173">Em sua classe `MainActivity` , adicione o seguinte método à disponibilidade dos Serviços do Google Play.</span><span class="sxs-lookup"><span data-stu-id="91ea7-173">In your `MainActivity` class, add the following method to the availability of Google Play Services.</span></span> 
   
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
5. <span data-ttu-id="91ea7-174">Em sua classe `MainActivity`, adicione o seguinte código que verificará os Serviços do Google Play antes de chamar o `IntentService` para você obter seu token de registro FCM e registrar-se no hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="91ea7-174">In your `MainActivity` class, add the following code that will check for Google Play Services before calling your `IntentService` to get your FCM registration token and register with your notification hub.</span></span>
   
        public void registerWithNotificationHubs()
        {
            if (checkPlayServices()) {
                // Start IntentService to register this application with FCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. <span data-ttu-id="91ea7-175">No método `OnCreate` da classe `MainActivity`, adicione o código a seguir para começar o processo de registro quando a atividade for criada.</span><span class="sxs-lookup"><span data-stu-id="91ea7-175">In the `OnCreate` method of the `MainActivity` class, add the following code to start the registration process when activity is created.</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. <span data-ttu-id="91ea7-176">Adicione estes outros métodos a `MainActivity` para verificar o estado do aplicativo e informar o status em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91ea7-176">Add these additional methods to the `MainActivity` to verify app state and report status in your app.</span></span>
   
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
8. <span data-ttu-id="91ea7-177">O método `ToastNotify` usa o controle *"Hello World"* `TextView` para informar de forma persistente o status e as notificações no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91ea7-177">The `ToastNotify` method uses the *"Hello World"* `TextView` control to report status and notifications persistently in the app.</span></span> <span data-ttu-id="91ea7-178">Em seu layout activity_main.xml, adicione a seguinte identificação para esse controle.</span><span class="sxs-lookup"><span data-stu-id="91ea7-178">In your activity_main.xml layout, add the following id for that control.</span></span>
   
       android:id="@+id/text_hello"
9. <span data-ttu-id="91ea7-179">Em seguida, adicionaremos uma subclasse para o receptor que definimos em AndroidManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="91ea7-179">Next we will add a subclass for our receiver we defined in the AndroidManifest.xml.</span></span> <span data-ttu-id="91ea7-180">Adicione outra classe nova ao projeto denominada `MyHandler`.</span><span class="sxs-lookup"><span data-stu-id="91ea7-180">Add another new class to your project named `MyHandler`.</span></span>
10. <span data-ttu-id="91ea7-181">Adicione as seguintes instruções de importação na parte superior de `MyHandler.java`:</span><span class="sxs-lookup"><span data-stu-id="91ea7-181">Add the following import statements at the top of `MyHandler.java`:</span></span>
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.media.RingtoneManager;
        import android.net.Uri;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. <span data-ttu-id="91ea7-182">Adicione o código a seguir à classe `MyHandler`, tornando-a uma subclasse de `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span><span class="sxs-lookup"><span data-stu-id="91ea7-182">Add the following code for the `MyHandler` class making it a subclass of `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span></span>
    
    <span data-ttu-id="91ea7-183">Esse código substitui o método `OnReceive` para que o manipulador informe as notificações recebidas.</span><span class="sxs-lookup"><span data-stu-id="91ea7-183">This code overrides the `OnReceive` method, so the handler will report notifications that are received.</span></span> <span data-ttu-id="91ea7-184">O manipulador também envia a notificação por push ao gerenciador de notificações do Android usando o método `sendNotification()` .</span><span class="sxs-lookup"><span data-stu-id="91ea7-184">The handler also sends the push notification to the Android notification manager by using the `sendNotification()` method.</span></span> <span data-ttu-id="91ea7-185">O método `sendNotification()` deve ser executado quando o aplicativo não está em execução e uma notificação é recebida.</span><span class="sxs-lookup"><span data-stu-id="91ea7-185">The `sendNotification()` method should be executed when the app is not running and a notification is received.</span></span>
    
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
12. <span data-ttu-id="91ea7-186">No Android Studio, na barra de menus, clique em **Compilar** > **Recompilar Projeto** para garantir que não haja erros presentes no código.</span><span class="sxs-lookup"><span data-stu-id="91ea7-186">In Android Studio on the menu bar, click **Build** > **Rebuild Project** to make sure that no errors are present in your code.</span></span>
13. <span data-ttu-id="91ea7-187">Execute o aplicativo em seu dispositivo e verifique se ele se registra com êxito no hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="91ea7-187">Run the app on your device and verify it registers successfully with the notification hub.</span></span> 
    
    > [!NOTE]
    > <span data-ttu-id="91ea7-188">O registro poderá falhar na primeira inicialização até o método `onTokenRefresh()` do serviço de identificação da instância ser chamado.</span><span class="sxs-lookup"><span data-stu-id="91ea7-188">Registration may fail on the initial launch until the `onTokenRefresh()` method of instance Id service is called.</span></span> <span data-ttu-id="91ea7-189">A atualização deve iniciar um registro bem-sucedido no hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="91ea7-189">The refresh should intiate a successful registration with the notification hub.</span></span>
    > 
    > 

## <a name="sending-push-notifications"></a><span data-ttu-id="91ea7-190">Como enviar notificações por push</span><span class="sxs-lookup"><span data-stu-id="91ea7-190">Sending push notifications</span></span>
<span data-ttu-id="91ea7-191">Você pode testar o recebimento de notificações por push no aplicativo enviando-as por meio do [Portal do Azure] - procure a seção **Solução de problemas** na folha do hub, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="91ea7-191">You can test receiving push notifications in your app by sending them via the [Azure Portal] - look for the **Troubleshooting** Section in the hub blade, as shown below.</span></span>

![Hubs de notificação do Azure - Testar Enviar](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-the-app"></a><span data-ttu-id="91ea7-193">(Opcional) Enviar notificações por push diretamente do aplicativo</span><span class="sxs-lookup"><span data-stu-id="91ea7-193">(Optional) Send push notifications directly from the app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="91ea7-194">Este exemplo de envio de notificações do aplicativo cliente é fornecido somente para fins de aprendizado.</span><span class="sxs-lookup"><span data-stu-id="91ea7-194">This example of sending notifications from the client app is provided for learning purposes only.</span></span> <span data-ttu-id="91ea7-195">Como o exemplo exigirá a presença da `DefaultFullSharedAccessSignature` no aplicativo cliente, ele expõe seu hub de notificação ao risco de um usuário obter acesso para enviar notificações não autorizadas aos seus clientes.</span><span class="sxs-lookup"><span data-stu-id="91ea7-195">Since this will require the `DefaultFullSharedAccessSignature` to be present on the client app, it exposes your notification hub to the risk that a user may gain access to send unauthorized notifications to your clients.</span></span>
> 
> 

<span data-ttu-id="91ea7-196">Normalmente, você enviaria notificações usando um servidor back-end.</span><span class="sxs-lookup"><span data-stu-id="91ea7-196">Normally, you would send notifications using a backend server.</span></span> <span data-ttu-id="91ea7-197">Em alguns casos, talvez você queira ser capaz de enviar notificações por push diretamente do aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="91ea7-197">For some cases, you might want to be able to send push notifications directly from the client application.</span></span> <span data-ttu-id="91ea7-198">Esta seção explica como enviar as notificações a partir do cliente usando a [API REST do Hub de Notificação do Azure](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="91ea7-198">This section explains how to send notifications from the client using the [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span></span>

1. <span data-ttu-id="91ea7-199">Na Exibição de Projeto do Android Studio, expanda **App** > **src** > **main** > **res** > **layout**.</span><span class="sxs-lookup"><span data-stu-id="91ea7-199">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **layout**.</span></span> <span data-ttu-id="91ea7-200">Abra o arquivo de layout `activity_main.xml` e clique na guia **Texto** para atualizar o conteúdo de texto do arquivo.</span><span class="sxs-lookup"><span data-stu-id="91ea7-200">Open the `activity_main.xml` layout file and click the **Text** tab to update the text contents of the file.</span></span> <span data-ttu-id="91ea7-201">Atualize-o com o código abaixo, que adiciona novos controles `Button` e `EditText` para enviar as mensagens de notificação por push ao hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="91ea7-201">Update it with the code below, which adds new `Button` and `EditText` controls for sending push notification messages to the notification hub.</span></span> <span data-ttu-id="91ea7-202">Adicione este código à parte inferior imediatamente antes de `</RelativeLayout>`.</span><span class="sxs-lookup"><span data-stu-id="91ea7-202">Add this code at the bottom, just before `</RelativeLayout>`.</span></span>
   
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
2. <span data-ttu-id="91ea7-203">Na Exibição de Projeto do Android Studio, expanda **App** > **src** > **main** > **res** > **values**.</span><span class="sxs-lookup"><span data-stu-id="91ea7-203">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **values**.</span></span> <span data-ttu-id="91ea7-204">Abra o arquivo `strings.xml` e adicione os valores da cadeia de caracteres referenciados pelos novos controles `Button` e `EditText`.</span><span class="sxs-lookup"><span data-stu-id="91ea7-204">Open the `strings.xml` file and add the string values that are referenced by the new `Button` and `EditText` controls.</span></span> <span data-ttu-id="91ea7-205">Adicione-os à parte inferior do arquivo imediatamente antes de `</resources>`.</span><span class="sxs-lookup"><span data-stu-id="91ea7-205">Add these at the bottom of the file, just before `</resources>`.</span></span>
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. <span data-ttu-id="91ea7-206">Em seu arquivo `NotificationSetting.java`, adicione a seguinte configuração à classe `NotificationSettings`.</span><span class="sxs-lookup"><span data-stu-id="91ea7-206">In your `NotificationSetting.java` file, add the following setting to the `NotificationSettings` class.</span></span>
   
    <span data-ttu-id="91ea7-207">Atualize `HubFullAccess` com a cadeia de conexão **DefaultFullSharedAccessSignature** para o hub.</span><span class="sxs-lookup"><span data-stu-id="91ea7-207">Update `HubFullAccess` with the **DefaultFullSharedAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="91ea7-208">Essa cadeia de conexão pode ser copiada do [Portal do Azure] clicando em **Políticas de Acesso** na folha **Configurações** do hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="91ea7-208">This connection string can be copied from the [Azure Portal] by clicking **Access Policies** on the **Settings** blade for your notification hub.</span></span>
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccessSignature Connection string>";
4. <span data-ttu-id="91ea7-209">No arquivo `MainActivity.java`, adicione as instruções `import` a seguir acima da classe `MainActivity`.</span><span class="sxs-lookup"><span data-stu-id="91ea7-209">In your `MainActivity.java` file, add the following `import` statements above the `MainActivity` class.</span></span>
   
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
5. <span data-ttu-id="91ea7-210">No arquivo `MainActivity.java`, adicione os membros a seguir na parte superior da classe `MainActivity`.</span><span class="sxs-lookup"><span data-stu-id="91ea7-210">In your `MainActivity.java` file, add the following members at the top of the `MainActivity` class.</span></span>    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. <span data-ttu-id="91ea7-211">Você deve criar um token SaS (Software Access Signature) para autenticar uma solicitação POST para o envio de mensagens para o seu hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="91ea7-211">You must create a Software Access Signature (SaS) token to authenticate a POST request to send messages to your notification hub.</span></span> <span data-ttu-id="91ea7-212">Isso é feito analisando os principais dados da cadeia de conexão e criando o token SaS, como mencionado na referência da API REST [Conceitos comuns](http://msdn.microsoft.com/library/azure/dn495627.aspx) .</span><span class="sxs-lookup"><span data-stu-id="91ea7-212">This is done by parsing the key data from the connection string and then creating the SaS token, as mentioned in the [Common Concepts](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API reference.</span></span> <span data-ttu-id="91ea7-213">O código a seguir é um exemplo de implementação.</span><span class="sxs-lookup"><span data-stu-id="91ea7-213">The following code is an example implementation.</span></span>
   
    <span data-ttu-id="91ea7-214">Em `MainActivity.java`, adicione o método a seguir à classe `MainActivity` para analisar a cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="91ea7-214">In `MainActivity.java`, add the following method to the `MainActivity` class to parse your connection string.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx
         * to parse the connection string so a SaS authentication token can be
         * constructed.
         *
         * @param connectionString This must be the DefaultFullSharedAccess connection
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
7. <span data-ttu-id="91ea7-215">Em `MainActivity.java`, adicione o método a seguir à classe `MainActivity` para criar um token de autenticação SaS.</span><span class="sxs-lookup"><span data-stu-id="91ea7-215">In `MainActivity.java`, add the following method to the `MainActivity` class to create a SaS authentication token.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx to
         * construct a SaS token from the access key to authenticate a request.
         *
         * @param uri The unencoded resource URI string for this operation. The resource
         *            URI is the full URI of the Service Bus resource to which access is
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
   
                // Get an hmac_sha1 key from the raw key bytes
                byte[] keyBytes = HubSasKeyValue.getBytes("UTF-8");
                SecretKeySpec signingKey = new SecretKeySpec(keyBytes, "HmacSHA256");
   
                // Get an hmac_sha1 Mac instance and initialize with the signing key
                Mac mac = Mac.getInstance("HmacSHA256");
                mac.init(signingKey);
   
                // Compute the hmac on input data bytes
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
8. <span data-ttu-id="91ea7-216">No `MainActivity.java`, adicione o método a seguir à classe `MainActivity` para lidar com o clique no botão **Enviar Notificação** e enviar a mensagem de notificação por push ao hub usando a API REST interna.</span><span class="sxs-lookup"><span data-stu-id="91ea7-216">In `MainActivity.java`, add the following method to the `MainActivity` class to handle the **Send Notification** button click and send the push notification message to the hub by using the built-in REST API.</span></span>
   
        /**
         * Send Notification button click handler. This method parses the
         * DefaultFullSharedAccess connection string and generates a SaS token. The
         * token is added to the Authorization header on the POST request to the
         * notification hub. The text in the editTextNotificationMessage control
         * is added as the JSON body for the request to add a GCM message to the hub.
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
   
                            // Authenticate the POST request with the SaS token
                            urlConnection.setRequestProperty("Authorization", 
                                generateSasToken(url.toString()));
   
                            // Notification format should be GCM
                            urlConnection.setRequestProperty("ServiceBusNotification-Format", "gcm");
   
                            // Include any tags
                            // Example below targets 3 specific tags
                            // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
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

## <a name="testing-your-app"></a><span data-ttu-id="91ea7-217">Testando seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="91ea7-217">Testing your app</span></span>
#### <a name="push-notifications-in-the-emulator"></a><span data-ttu-id="91ea7-218">Notificações por push no emulador</span><span class="sxs-lookup"><span data-stu-id="91ea7-218">Push notifications in the emulator</span></span>
<span data-ttu-id="91ea7-219">Para testar notificações por push em um emulador, verifique se a imagem de emulador dá suporte ao nível de API do Google que você escolheu para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="91ea7-219">If you want to test push notifications inside an emulator, make sure that your emulator image supports the Google API level that you chose for your app.</span></span> <span data-ttu-id="91ea7-220">Se sua imagem não der suporte às APIs nativas do Google, você verá a exceção **SERVICE\_NOT\_AVAILABLE**.</span><span class="sxs-lookup"><span data-stu-id="91ea7-220">If your image doesn't support native Google APIs, you will end up with the **SERVICE\_NOT\_AVAILABLE** exception.</span></span>

<span data-ttu-id="91ea7-221">Além disso, verifique se você adicionou a conta do Google ao emulador em execução em **Configurações** > **Contas**.</span><span class="sxs-lookup"><span data-stu-id="91ea7-221">In addition to the above, ensure that you have added your Google account to your running emulator under **Settings** > **Accounts**.</span></span> <span data-ttu-id="91ea7-222">Caso contrário, suas tentativas de se registrar no GCM podem resultar na exceção **AUTHENTICATION\_FAILED**.</span><span class="sxs-lookup"><span data-stu-id="91ea7-222">Otherwise, your attempts to register with GCM may result in the **AUTHENTICATION\_FAILED** exception.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="91ea7-223">Executando o aplicativo</span><span class="sxs-lookup"><span data-stu-id="91ea7-223">Running the application</span></span>
1. <span data-ttu-id="91ea7-224">Execute o aplicativo e observe que a ID de registro é relatada para um registro bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="91ea7-224">Run the app and notice that the registration ID is reported for a successful registration.</span></span>
   
       ![Testing on Android - Channel registration](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-registered.png)
2. <span data-ttu-id="91ea7-225">Insira uma mensagem de notificação a ser enviada para todos os dispositivos Android registrados no hub.</span><span class="sxs-lookup"><span data-stu-id="91ea7-225">Enter a notification message to be sent to all Android devices that have registered with the hub.</span></span>
   
       ![Testing on Android - sending a message](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-set-message.png)
3. <span data-ttu-id="91ea7-226">Pressione **Enviar Notificação**.</span><span class="sxs-lookup"><span data-stu-id="91ea7-226">Press **Send Notification**.</span></span> <span data-ttu-id="91ea7-227">Qualquer dispositivo que tiver o aplicativo em execução mostrará uma instância de `AlertDialog` com a mensagem de notificação por push.</span><span class="sxs-lookup"><span data-stu-id="91ea7-227">Any devices that have the app running will show an `AlertDialog` instance with the push notification message.</span></span> <span data-ttu-id="91ea7-228">Os dispositivos que não tiverem o aplicativo em execução, mas tiverem sido registrados anteriormente para notificações por push, receberão uma notificação no Gerenciador de Notificação do Android.</span><span class="sxs-lookup"><span data-stu-id="91ea7-228">Devices that don't have the app running but were previously registered for push notifications will receive a notification in the Android Notification Manager.</span></span> <span data-ttu-id="91ea7-229">Para exibi-las, passe o dedo do canto superior esquerdo para baixo.</span><span class="sxs-lookup"><span data-stu-id="91ea7-229">Those can be viewed by swiping down from the upper-left corner.</span></span>
   
       ![Testing on Android - notifications](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-received-message.png)

## <a name="next-steps"></a><span data-ttu-id="91ea7-230">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="91ea7-230">Next steps</span></span>
<span data-ttu-id="91ea7-231">Recomendamos o tutorial [Usar os Hubs de Notificação para enviar notificações por push aos usuários] como a próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="91ea7-231">We recommend the [Use Notification Hubs to push notifications to users] tutorial as the next step.</span></span> <span data-ttu-id="91ea7-232">Ele mostra como enviar notificações de um back-end do ASP.NET usando marcas para direcionar usuários específicos.</span><span class="sxs-lookup"><span data-stu-id="91ea7-232">It will show you how to send notifications from an ASP.NET backend using tags to target specific users.</span></span>

<span data-ttu-id="91ea7-233">Se você quiser segmentar os usuários por grupos de interesse, verifique o tutorial [Usar Hubs de Notificação para enviar as notícias mais recentes] .</span><span class="sxs-lookup"><span data-stu-id="91ea7-233">If you want to segment your users by interest groups, check out the [Use Notification Hubs to send breaking news] tutorial.</span></span>

<span data-ttu-id="91ea7-234">Para saber mais sobre os Hubs de Notificação, consulte nossas [Diretrizes dos Hubs de Notificação].</span><span class="sxs-lookup"><span data-stu-id="91ea7-234">To learn more general information about Notification Hubs, see our [Notification Hubs Guidance].</span></span>

<!-- Images. -->



<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Azure Classic Portal]: https://manage.windowsazure.com/
<span data-ttu-id="91ea7-235">[Diretrizes dos Hubs de Notificação]: notification-hubs-push-notification-overview.md</span><span class="sxs-lookup"><span data-stu-id="91ea7-235">[Notification Hubs Guidance]: notification-hubs-push-notification-overview.md</span></span>
<span data-ttu-id="91ea7-236">[Usar os Hubs de Notificação para enviar notificações por push aos usuários]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md</span><span class="sxs-lookup"><span data-stu-id="91ea7-236">[Use Notification Hubs to push notifications to users]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md</span></span>
<span data-ttu-id="91ea7-237">[Usar Hubs de Notificação para enviar as notícias mais recentes]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="91ea7-237">[Use Notification Hubs to send breaking news]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md</span></span>
<span data-ttu-id="91ea7-238">[Portal do Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="91ea7-238">[Azure Portal]: https://portal.azure.com</span></span>
