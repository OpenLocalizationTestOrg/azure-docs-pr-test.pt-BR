---
title: "aaaGet iniciado com Hubs de notificação para aplicativos xamarin | Microsoft Docs"
description: "Neste tutorial, você aprenderá como toouse Hubs de notificação do Azure toosend envio notificações tooa aplicativo Xamarin Android."
author: ysxu
manager: erikre
editor: 
services: notification-hubs
documentationcenter: xamarin
ms.assetid: 0be600fe-d5f3-43a5-9e5e-3135c9743e54
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c5c7ead9a9381ab9fb6bbe86e930a8a9254813d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-with-xamarin-for-android"></a><span data-ttu-id="26995-103">Introdução aos Hubs de Notificação com o Xamarin para Android</span><span class="sxs-lookup"><span data-stu-id="26995-103">Get started with Notification Hubs with Xamarin for Android</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="26995-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="26995-104">Overview</span></span>
<span data-ttu-id="26995-105">Este tutorial mostra como o aplicativo de xamarin tooa notificações de envio toouse toosend de Hubs de notificação do Azure.</span><span class="sxs-lookup"><span data-stu-id="26995-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Xamarin.Android application.</span></span>
<span data-ttu-id="26995-106">Você criará um aplicativo Xamarin.Android em branco que recebe notificações por push usando o GCM(Google Cloud Messaging).</span><span class="sxs-lookup"><span data-stu-id="26995-106">You'll create a blank Xamarin.Android app that receives push notifications by using Google Cloud Messaging (GCM).</span></span> <span data-ttu-id="26995-107">Quando você terminar, você será capaz de toouse sua toobroadcast de hub de notificação por push notificações tooall Olá a dispositivos que executam seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26995-107">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span> <span data-ttu-id="26995-108">Olá código concluído está disponível no hello [aplicativo hubs de notificação] [ GitHub] exemplo.</span><span class="sxs-lookup"><span data-stu-id="26995-108">hello finished code is available in hello [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="26995-109">Este tutorial demonstra um cenário de difusão simples hello usando Hubs de notificação.</span><span class="sxs-lookup"><span data-stu-id="26995-109">This tutorial demonstrates hello simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="26995-110">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="26995-110">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="26995-111">código de saudação concluído para este tutorial pode ser encontrado no GitHub [aqui](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).</span><span class="sxs-lookup"><span data-stu-id="26995-111">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26995-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="26995-112">Prerequisites</span></span>
<span data-ttu-id="26995-113">Este tutorial requer o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="26995-113">This tutorial requires hello following:</span></span>

* <span data-ttu-id="26995-114">Visual Studio com Xamarin no Windows ou Xamarin Studio no Mac OS X. Encontre instruções de instalação completas em [Configuração e instalação para Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="26995-114">Visual Studio with Xamarin on Windows or Xamarin Studio on Mac OS X. Complete installation instructions are on [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* <span data-ttu-id="26995-115">Conta ativa do Google</span><span class="sxs-lookup"><span data-stu-id="26995-115">Active Google account</span></span>
* <span data-ttu-id="26995-116">[Componente de mensagens do Azure]</span><span class="sxs-lookup"><span data-stu-id="26995-116">[Azure Messaging Component]</span></span>
* <span data-ttu-id="26995-117">[Componente de mensagens de nuvem do Google]</span><span class="sxs-lookup"><span data-stu-id="26995-117">[Google Cloud Messaging Client Component]</span></span>

<span data-ttu-id="26995-118">A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais sobre Hubs de Notificação para aplicativos Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="26995-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin.Android apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="26995-119">toocomplete neste tutorial, você deve ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="26995-119">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="26995-120">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="26995-120">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="26995-121">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="26995-121">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).</span></span>
> 
> 

## <a name="enable-google-cloud-messaging"></a><span data-ttu-id="26995-122">Habilitar o sistema de mensagens em nuvem do Google</span><span class="sxs-lookup"><span data-stu-id="26995-122">Enable Google Cloud Messaging</span></span>
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="26995-123">Configurar seu Hub de Notificação</span><span class="sxs-lookup"><span data-stu-id="26995-123">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li><p><span data-ttu-id="26995-124">Clique em Olá <b>configurar</b> guia na parte superior do hello, digite Olá <b>chave API</b> valor obtido na seção anterior hello e, em seguida, clique em <b>salvar</b>.</span><span class="sxs-lookup"><span data-stu-id="26995-124">Click hello <b>Configure</b> tab at hello top, enter hello <b>API Key</b> value you obtained in hello previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>
<span data-ttu-id="26995-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span><span class="sxs-lookup"><span data-stu-id="26995-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span></span>

<span data-ttu-id="26995-126">Hub de notificação agora é toowork configurado com GCM e ter tooboth de cadeias de caracteres de conexão Olá registrar seu notificações do aplicativo tooreceive e notificações por push de toosend.</span><span class="sxs-lookup"><span data-stu-id="26995-126">Your notification hub is now configured toowork with GCM, and you have hello connection strings tooboth register your app tooreceive notifications and toosend push notifications.</span></span>

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="26995-127">Conecte-se o seu hub de notificação do aplicativo toohello</span><span class="sxs-lookup"><span data-stu-id="26995-127">Connect your app toohello notification hub</span></span>
### <a name="create-a-new-project"></a><span data-ttu-id="26995-128">Criar um novo projeto</span><span class="sxs-lookup"><span data-stu-id="26995-128">Create a new project</span></span>
1. <span data-ttu-id="26995-129">No Xamarin Studio, clique em **Nova Solução**, clique em **Aplicativo Android** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="26995-129">In Xamarin Studio, click **New Solution**, click **Android App**, and click **Next**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project1.png)

2. <span data-ttu-id="26995-130">Insira o **Nome do Aplicativo** e o **Identificador**.</span><span class="sxs-lookup"><span data-stu-id="26995-130">Enter your **App Name** and **Identifier**.</span></span> <span data-ttu-id="26995-131">Clique em Olá **destino Plaforms** desejado toosupport e, em seguida, clique em **próximo** e **criar**.</span><span class="sxs-lookup"><span data-stu-id="26995-131">Click hello **Target Plaforms** you want toosupport and then click **Next** and **Create**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project2.png)

    <span data-ttu-id="26995-132">Isso cria um novo projeto Android.</span><span class="sxs-lookup"><span data-stu-id="26995-132">This creates a new Android project.</span></span>

1. <span data-ttu-id="26995-133">Abra as propriedades do projeto de saudação clicando duas vezes o seu novo projeto em Olá exibição de solução e escolha **opções**.</span><span class="sxs-lookup"><span data-stu-id="26995-133">Open hello project properties by right-clicking your new project in hello Solution view and choosing **Options**.</span></span> <span data-ttu-id="26995-134">Selecione Olá **aplicativo Android** item Olá **criar** seção.</span><span class="sxs-lookup"><span data-stu-id="26995-134">Select hello **Android Application** item in hello **Build** section.</span></span>
   
    <span data-ttu-id="26995-135">Certifique-se de que primeira letra de saudação do seu **nome do pacote** letras minúsculas constantemente.</span><span class="sxs-lookup"><span data-stu-id="26995-135">Ensure that hello first letter of your **Package name** is lowercase.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="26995-136">primeira letra de saudação do nome do pacote de saudação deve estar em minúscula.</span><span class="sxs-lookup"><span data-stu-id="26995-136">hello first letter of hello package name must be lowercase.</span></span> <span data-ttu-id="26995-137">Caso contrário, você receberá erros de manifesto do aplicativo ao registrar **BroadcastReceiver** e **IntentFilter** para as notificações por push abaixo.</span><span class="sxs-lookup"><span data-stu-id="26995-137">Otherwise, you will receive application manifest errors when you register your **BroadcastReceiver** and **IntentFilter** for push notifications below.</span></span>
   > 
   > 
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub--xamarin-android-app-options.png)
2. <span data-ttu-id="26995-138">Opcionalmente, o conjunto Olá **versão do Android mínimo** tooanother nível de API.</span><span class="sxs-lookup"><span data-stu-id="26995-138">Optionally, set hello **Minimum Android version** tooanother API Level.</span></span>
3. <span data-ttu-id="26995-139">Opcionalmente, o conjunto Olá **versão destino Android** toohello outra versão de API que você deseja tootarget (deve ser o nível de API 8 ou superior).</span><span class="sxs-lookup"><span data-stu-id="26995-139">Optionally, set hello **Target Android version** toohello another API version that you want tootarget (must be API level 8 or higher).</span></span>

<span data-ttu-id="26995-140">Clique em **Okey** e caixa de diálogo de opções de projeto Olá fechar.</span><span class="sxs-lookup"><span data-stu-id="26995-140">Click **OK** and close hello Project Options dialog.</span></span>

### <a name="add-hello-required-components-tooyour-project"></a><span data-ttu-id="26995-141">Adicionar projeto de tooyour Olá componentes necessários</span><span class="sxs-lookup"><span data-stu-id="26995-141">Add hello required components tooyour project</span></span>
<span data-ttu-id="26995-142">Olá Google nuvem mensagens cliente disponíveis na Olá armazenamento do componente Xamarin simplifica o processo de saudação de suporte para notificações por push xamarin.</span><span class="sxs-lookup"><span data-stu-id="26995-142">hello Google Cloud Messaging Client available on hello Xamarin Component Store simplifies hello process of supporting push notifications in Xamarin.Android.</span></span>

1. <span data-ttu-id="26995-143">Clique em pasta de componentes de saudação no aplicativo xamarin e escolha **obter mais componentes**.</span><span class="sxs-lookup"><span data-stu-id="26995-143">Right-click hello Components folder in Xamarin.Android app and choose **Get More Components**.</span></span>
2. <span data-ttu-id="26995-144">Pesquise Olá **mensagens do Azure** componente e adicioná-lo toohello projeto.</span><span class="sxs-lookup"><span data-stu-id="26995-144">Search for hello **Azure Messaging** component and add it toohello project.</span></span>
3. <span data-ttu-id="26995-145">Pesquise Olá **cliente de mensagens de nuvem do Google** componente e adicioná-lo toohello projeto.</span><span class="sxs-lookup"><span data-stu-id="26995-145">Search for hello **Google Cloud Messaging Client** component and add it toohello project.</span></span>

### <a name="set-up-notification-hubs-in-your-project"></a><span data-ttu-id="26995-146">Configurar hubs de notificação em seu projeto</span><span class="sxs-lookup"><span data-stu-id="26995-146">Set up notification hubs in your project</span></span>
1. <span data-ttu-id="26995-147">Reúna Olá informações para o hub de notificação e o aplicativo Android a seguir:</span><span class="sxs-lookup"><span data-stu-id="26995-147">Gather hello following information for your Android app and notification hub:</span></span>
   
   * <span data-ttu-id="26995-148">**GoogleProjectNumber**: obter esse valor de número do projeto da visão geral de saudação do seu aplicativo no Portal do desenvolvedor do Google de saudação.</span><span class="sxs-lookup"><span data-stu-id="26995-148">**GoogleProjectNumber**:  Get this Project Number value from hello overview of your app on hello Google Developer Portal.</span></span> <span data-ttu-id="26995-149">Você anotou anteriormente, esse valor quando você criou o aplicativo hello no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="26995-149">You made a note of this value earlier when you created hello app on hello portal.</span></span>
   * <span data-ttu-id="26995-150">**Escutar a cadeia de caracteres de conexão**: no painel de saudação do hello [Portal clássico do Azure], clique em **exibir cadeias de caracteres de conexão**.</span><span class="sxs-lookup"><span data-stu-id="26995-150">**Listen connection string**: On hello dashboard in hello [Azure Classic Portal], click **View connection strings**.</span></span> <span data-ttu-id="26995-151">Saudação de cópia *DefaultListenSharedAccessSignature* cadeia de caracteres de conexão para esse valor.</span><span class="sxs-lookup"><span data-stu-id="26995-151">Copy hello *DefaultListenSharedAccessSignature* connection string for this value.</span></span>
   * <span data-ttu-id="26995-152">**O nome do hub**: Este é o nome de saudação do seu hub de saudação [Portal clássico do Azure].</span><span class="sxs-lookup"><span data-stu-id="26995-152">**Hub name**: This is hello name of your hub from hello [Azure Classic Portal].</span></span> <span data-ttu-id="26995-153">Por exemplo, *mynotificationhub2*.</span><span class="sxs-lookup"><span data-stu-id="26995-153">For example, *mynotificationhub2*.</span></span>
     
     <span data-ttu-id="26995-154">Criar um **Constants.cs** de classe para o seu projeto Xamarin e definir Olá valores constantes na classe Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="26995-154">Create a **Constants.cs** class for your Xamarin project and define hello following constant values in hello class.</span></span> <span data-ttu-id="26995-155">Substitua os espaços reservados de saudação com seus valores.</span><span class="sxs-lookup"><span data-stu-id="26995-155">Replace hello placeholders with your values.</span></span>
     
       <span data-ttu-id="26995-156">public static class Constants   {</span><span class="sxs-lookup"><span data-stu-id="26995-156">public static class Constants   {</span></span>
     
           public const string SenderID = "<GoogleProjectNumber>"; // Google API Project Number
           public const string ListenConnectionString = "<Listen connection string>";
           public const string NotificationHubName = "<hub name>";
       <span data-ttu-id="26995-157">}</span><span class="sxs-lookup"><span data-stu-id="26995-157">}</span></span>
2. <span data-ttu-id="26995-158">Adicione Olá seguinte usando instruções muito**MainActivity.cs**:</span><span class="sxs-lookup"><span data-stu-id="26995-158">Add hello following using statements too**MainActivity.cs**:</span></span>
   
        using Android.Util;
        using Gcm.Client;
3. <span data-ttu-id="26995-159">Adicionar um toohello de variável de instância `MainActivity` classe que será usado tooshow uma caixa de diálogo alerta quando o aplicativo hello está em execução:</span><span class="sxs-lookup"><span data-stu-id="26995-159">Add an instance variable toohello `MainActivity` class that will be used tooshow an alert dialog when hello app is running:</span></span>
   
        public static MainActivity instance;
4. <span data-ttu-id="26995-160">Criar hello seguinte método em Olá **MainActivity** classe:</span><span class="sxs-lookup"><span data-stu-id="26995-160">Create hello following method in hello **MainActivity** class:</span></span>
   
        private void RegisterWithGCM()
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);
   
            // Register for push notifications
            Log.Info("MainActivity", "Registering...");
            GcmClient.Register(this, Constants.SenderID);
        }
5. <span data-ttu-id="26995-161">Em Olá `OnCreate` método **MainActivity.cs**, inicializar Olá `instance` variável e adicionar uma chamada muito`RegisterWithGCM`:</span><span class="sxs-lookup"><span data-stu-id="26995-161">In hello `OnCreate` method of **MainActivity.cs**, initialize hello `instance` variable and add a call too`RegisterWithGCM`:</span></span>
   
        protected override void OnCreate (Bundle bundle)
        {
            instance = this;
   
            base.OnCreate (bundle);
   
            // Set your view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);
   
            // Get your button from hello layout resource,
            // and attach an event tooit
            Button button = FindViewById<Button> (Resource.Id.myButton);
   
            RegisterWithGCM();
        }
6. <span data-ttu-id="26995-162">Crie uma nova classe, **MyBroadcastReceiver**.</span><span class="sxs-lookup"><span data-stu-id="26995-162">Create a new class, **MyBroadcastReceiver**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="26995-163">Mostraremos a criação de uma classe **BroadcastReceiver** desde o início.</span><span class="sxs-lookup"><span data-stu-id="26995-163">We will walk through creating a **BroadcastReceiver** class from scratch below.</span></span> <span data-ttu-id="26995-164">No entanto, um toomanually alternativo rápido criar **MyBroadcastReceiver.cs** é toorefer toohello **GcmService.cs** arquivo encontrado no projeto de xamarin do exemplo hello incluído com hello [Exemplos de hubs de notificação][GitHub].</span><span class="sxs-lookup"><span data-stu-id="26995-164">However, a quick alternative toomanually creating **MyBroadcastReceiver.cs** is toorefer toohello **GcmService.cs** file found in hello sample Xamarin.Android project included with hello [NotificationHubs samples][GitHub].</span></span> <span data-ttu-id="26995-165">Duplicando **GcmService.cs** e alterando os nomes de classe pode ser também um toostart ótimo lugar.</span><span class="sxs-lookup"><span data-stu-id="26995-165">Duplicating **GcmService.cs** and changing class names can be a great place toostart as well.</span></span>
   > 
   > 
7. <span data-ttu-id="26995-166">Adicione Olá seguinte usando instruções muito**MyBroadcastReceiver.cs** (referência de assembly que você adicionou anteriormente e componente toohello):</span><span class="sxs-lookup"><span data-stu-id="26995-166">Add hello following using statements too**MyBroadcastReceiver.cs** (referring toohello component and assembly that you added earlier):</span></span>
   
        using System.Collections.Generic;
        using System.Text;
        using Android.App;
        using Android.Content;
        using Android.Util;
        using Gcm.Client;
        using WindowsAzure.Messaging;
8. <span data-ttu-id="26995-167">Em **MyBroadcastReceiver.cs**, adicionar Olá solicitações de permissão a seguir entre hello **usando** instruções e hello **namespace** declaração:</span><span class="sxs-lookup"><span data-stu-id="26995-167">In **MyBroadcastReceiver.cs**, add hello following permission requests between hello **using** statements and hello **namespace** declaration:</span></span>
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is needed only for Android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
9. <span data-ttu-id="26995-168">Em **MyBroadcastReceiver.cs**, alterar Olá **MyBroadcastReceiver** classe a seguir Olá toomatch:</span><span class="sxs-lookup"><span data-stu-id="26995-168">In **MyBroadcastReceiver.cs**, change hello **MyBroadcastReceiver** class toomatch hello following:</span></span>
   
        [BroadcastReceiver(Permission=Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        public class MyBroadcastReceiver : GcmBroadcastReceiverBase<PushHandlerService>
        {
            public static string[] SENDER_IDS = new string[] { Constants.SenderID };
   
            public const string TAG = "MyBroadcastReceiver-GCM";
        }
10. <span data-ttu-id="26995-169">Adicione outra classe a **MyBroadcastReceiver.cs** chamada **PushHandlerService**, que deriva de **GcmServiceBase**.</span><span class="sxs-lookup"><span data-stu-id="26995-169">Add another class in **MyBroadcastReceiver.cs** named **PushHandlerService**, which derives from **GcmServiceBase**.</span></span> <span data-ttu-id="26995-170">Verifique se Olá de tooapply **Service** toohello classe de atributo:</span><span class="sxs-lookup"><span data-stu-id="26995-170">Make sure tooapply hello **Service** attribute toohello class:</span></span>
    
         [Service] // Must use hello service tag
         public class PushHandlerService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }
             private NotificationHub Hub { get; set; }
    
             public PushHandlerService() : base(Constants.SenderID)
                {
                 Log.Info(MyBroadcastReceiver.TAG, "PushHandlerService() constructor");
             }
         }
11. <span data-ttu-id="26995-171">**GcmServiceBase** implementa os métodos **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()** e **OnError()**.</span><span class="sxs-lookup"><span data-stu-id="26995-171">**GcmServiceBase** implements methods **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()**, and **OnError()**.</span></span> <span data-ttu-id="26995-172">Nosso **PushHandlerService** classe de implementação deve substituir esses métodos, e esses métodos serão acionado em resposta toointeracting com hub de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="26995-172">Our **PushHandlerService** implementation class must override these methods, and these methods will fire in response toointeracting with hello notification hub.</span></span>
12. <span data-ttu-id="26995-173">Substituir saudação **OnRegistered()** método **PushHandlerService** usando Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="26995-173">Override hello **OnRegistered()** method in **PushHandlerService** by using hello following code:</span></span>
    
         protected override void OnRegistered(Context context, string registrationId)
         {
             Log.Verbose(MyBroadcastReceiver.TAG, "GCM Registered: " + registrationId);
             RegistrationID = registrationId;
    
             createNotification("PushHandlerService-GCM Registered...",
                                 "hello device has been Registered!");
    
             Hub = new NotificationHub(Constants.NotificationHubName, Constants.ListenConnectionString,
                                         context);
             try
             {
                 Hub.UnregisterAll(registrationId);
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
    
             //var tags = new List<string>() { "falcons" }; // create tags if you want
             var tags = new List<string>() {};
    
             try
             {
                 var hubRegistration = Hub.Register(registrationId, tags.ToArray());
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
         }
    
    > [!NOTE]
    > <span data-ttu-id="26995-174">Em Olá **OnRegistered()** código acima, você deve observar Olá capacidade toospecify marcas tooregister de canais de mensagens específicos.</span><span class="sxs-lookup"><span data-stu-id="26995-174">In hello **OnRegistered()** code above, you should note hello ability toospecify tags tooregister for specific messaging channels.</span></span>
    > 
    > 
13. <span data-ttu-id="26995-175">Substituir saudação **OnMessage** método **PushHandlerService** usando Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="26995-175">Override hello **OnMessage** method in **PushHandlerService** by using hello following code:</span></span>
    
        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info(MyBroadcastReceiver.TAG, "GCM Message Received!");
    
            var msg = new StringBuilder();
    
            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }
    
            string messageText = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty (messageText))
            {
                createNotification ("New hub message!", messageText);
            }
            else
            {
                createNotification ("Unknown message details", msg.ToString ());
            }
        }
14. <span data-ttu-id="26995-176">Adicione o seguinte Olá **createNotification** e **dialogNotify** métodos muito**PushHandlerService** para notificar os usuários quando a notificação é recebida.</span><span class="sxs-lookup"><span data-stu-id="26995-176">Add hello following **createNotification** and **dialogNotify** methods too**PushHandlerService** for notifying users when a notification is received.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="26995-177">O design de notificação no Android versão 5.0 e posterior teve uma mudança significativa das versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="26995-177">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="26995-178">Se você testar no Android 5.0 ou posterior, o aplicativo de saudação precisará toobe executar notificação de saudação tooreceive.</span><span class="sxs-lookup"><span data-stu-id="26995-178">If you test this on Android 5.0 or later, hello app will need toobe running tooreceive hello notification.</span></span> <span data-ttu-id="26995-179">Para obter mais informações, consulte [Notificações do Android](http://go.microsoft.com/fwlink/?LinkId=615880).</span><span class="sxs-lookup"><span data-stu-id="26995-179">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
    > 
    > 
    
        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;
    
            //Create an intent tooshow UI
            var uiIntent = new Intent(this, typeof(MainActivity));
    
            //Create hello notification
            var notification = new Notification(Android.Resource.Drawable.SymActionEmail, title);
    
            //Auto-cancel will remove hello notification once hello user touches it
            notification.Flags = NotificationFlags.AutoCancel;
    
            //Set hello notification info
            //we use hello pending intent, passing our ui intent over, which will get called
            //when hello notification is tapped.
            notification.SetLatestEventInfo(this, title, desc, PendingIntent.GetActivity(this, 0, uiIntent, 0));
    
            //Show hello notification
            notificationManager.Notify(1, notification);
            dialogNotify (title, desc);
        }
    
        protected void dialogNotify(String title, String message)
        {
    
            MainActivity.instance.RunOnUiThread(() => {
                AlertDialog.Builder dlg = new AlertDialog.Builder(MainActivity.instance);
                AlertDialog alert = dlg.Create();
                alert.SetTitle(title);
                alert.SetButton("Ok", delegate {
                    alert.Dismiss();
                });
                alert.SetMessage(message);
                alert.Show();
            });
        }
15. <span data-ttu-id="26995-180">Substitua os membros abstratos **OnUnRegistered()**, **OnRecoverableError()** e **OnError()** para que o código seja compilado:</span><span class="sxs-lookup"><span data-stu-id="26995-180">Override abstract members **OnUnRegistered()**, **OnRecoverableError()**, and **OnError()** so that your code compiles:</span></span>
    
        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Verbose(MyBroadcastReceiver.TAG, "GCM Unregistered: " + registrationId);
    
            createNotification("GCM Unregistered...", "hello device has been unregistered!");
        }
    
        protected override bool OnRecoverableError(Context context, string errorId)
        {
            Log.Warn(MyBroadcastReceiver.TAG, "Recoverable Error: " + errorId);
    
            return base.OnRecoverableError (context, errorId);
        }
    
        protected override void OnError(Context context, string errorId)
        {
            Log.Error(MyBroadcastReceiver.TAG, "GCM Error: " + errorId);
        }

## <a name="run-your-app-in-hello-emulator"></a><span data-ttu-id="26995-181">Executar seu aplicativo no emulador Olá</span><span class="sxs-lookup"><span data-stu-id="26995-181">Run your app in hello emulator</span></span>
<span data-ttu-id="26995-182">Se você executar esse aplicativo no emulador hello, certifique-se de que você use um dispositivo Virtual Android (AVD) que oferece suporte a APIs do Google.</span><span class="sxs-lookup"><span data-stu-id="26995-182">If you run this app in hello emulator, make sure that you use an Android Virtual Device (AVD) that supports Google APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="26995-183">Em notificações de push de tooreceive ordem, você deve configurar uma conta do Google em seu dispositivo Virtual Android.</span><span class="sxs-lookup"><span data-stu-id="26995-183">In order tooreceive push notifications, you must set up a Google account on your Android Virtual Device.</span></span> <span data-ttu-id="26995-184">(No emulador do Windows hello, navegue muito**configurações** e clique em **adicionar conta**.) Além disso, certifique-se de que emulador Olá é toohello conectado à Internet.</span><span class="sxs-lookup"><span data-stu-id="26995-184">(In hello emulator, navigate too**Settings** and click **Add Account**.) Also, make sure that hello emulator is connected toohello Internet.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="26995-185">O design de notificação no Android versão 5.0 e posterior teve uma mudança significativa das versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="26995-185">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="26995-186">Para obter mais informações, consulte [Notificações do Android](http://go.microsoft.com/fwlink/?LinkId=615880).</span><span class="sxs-lookup"><span data-stu-id="26995-186">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
> 
> 

1. <span data-ttu-id="26995-187">Em **Ferramentas**, clique em **Abrir Gerenciador de Emulador do Android**, selecione seu dispositivo e clique em **Editar**.</span><span class="sxs-lookup"><span data-stu-id="26995-187">From **Tools**, click **Open Android Emulator Manager**, select your device, and then click **Edit**.</span></span>
   
      ![][18]
2. <span data-ttu-id="26995-188">Selecione **APIs do Google**, em **Destino** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="26995-188">Select **Google APIs** in **Target**, and then click **OK**.</span></span>
   
      ![][19]
3. <span data-ttu-id="26995-189">Na barra de ferramentas superior hello, clique em **executar**e, em seguida, selecione seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26995-189">On hello top toolbar, click **Run**, and then select your app.</span></span> <span data-ttu-id="26995-190">Isso inicia o emulador hello e executa o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="26995-190">This starts hello emulator and runs hello app.</span></span>
   
   <span data-ttu-id="26995-191">aplicativo Hello recupera Olá *registrationId* do GCM e registra com o hub de notificação hello.</span><span class="sxs-lookup"><span data-stu-id="26995-191">hello app retrieves hello *registrationId* from GCM and registers with hello notification hub.</span></span>

## <a name="send-notifications-from-your-backend"></a><span data-ttu-id="26995-192">Enviar notificações de seu back-end</span><span class="sxs-lookup"><span data-stu-id="26995-192">Send notifications from your backend</span></span>
<span data-ttu-id="26995-193">Você pode testar a receber notificações em seu aplicativo pelo envio de notificações em Olá [Portal clássico do Azure] via Olá guia depuração no hub de notificação hello, conforme mostrado na tela hello abaixo.</span><span class="sxs-lookup"><span data-stu-id="26995-193">You can test receiving notifications in your app by sending notifications in hello [Azure Classic Portal] via hello debug tab on hello notification hub, as shown in hello screen below.</span></span>

![][30]

<span data-ttu-id="26995-194">Normalmente, as notificações por push são enviadas em um serviço de back-end como os Serviços Móveis ou ASP.NET por meio de uma biblioteca compatível.</span><span class="sxs-lookup"><span data-stu-id="26995-194">Push notifications are normally sent in a backend service like Mobile Services or ASP.NET through a compatible library.</span></span> <span data-ttu-id="26995-195">Você também pode usar o hello API REST diretamente as mensagens de notificação de toosend se uma biblioteca não está disponível para seu back-end.</span><span class="sxs-lookup"><span data-stu-id="26995-195">You can also use hello REST API directly toosend notification messages if a library is not available for your backend.</span></span>

<span data-ttu-id="26995-196">Aqui está uma lista de alguns outros tutoriais que você talvez queira tooreview para enviar notificações:</span><span class="sxs-lookup"><span data-stu-id="26995-196">Here is a list of some other tutorials that you may want tooreview for sending notifications:</span></span>

* <span data-ttu-id="26995-197">ASP.NET: Consulte [usar Hubs de notificação toopush notificações toousers].</span><span class="sxs-lookup"><span data-stu-id="26995-197">ASP.NET: See [Use Notification Hubs toopush notifications toousers].</span></span>
* <span data-ttu-id="26995-198">Java de Hubs de notificação do Azure SDK: consulte [como toouse Hubs de notificação do Java](notification-hubs-java-push-notification-tutorial.md) para enviar notificações de Java.</span><span class="sxs-lookup"><span data-stu-id="26995-198">Azure Notification Hubs Java SDK: See [How toouse Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) for sending notifications from Java.</span></span> <span data-ttu-id="26995-199">Isso foi testado no Eclipse para desenvolvimento no Android.</span><span class="sxs-lookup"><span data-stu-id="26995-199">This has been tested in Eclipse for Android Development.</span></span>
* <span data-ttu-id="26995-200">PHP: Consulte [como toouse Hubs de notificação do PHP](notification-hubs-php-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="26995-200">PHP: See [How toouse Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

<span data-ttu-id="26995-201">Nas subseções próximas de saudação tutorial Olá, enviar notificações por meio de um aplicativo de console do .NET e usando um serviço móvel por meio de um script de nó.</span><span class="sxs-lookup"><span data-stu-id="26995-201">In hello next subsections of hello tutorial, you send notifications by using a .NET console app, and by using a mobile service through a node script.</span></span>

#### <a name="optional-send-notifications-by-using-a-net-app"></a><span data-ttu-id="26995-202">(Opcional) Enviar notificações usando um aplicativo .NET</span><span class="sxs-lookup"><span data-stu-id="26995-202">(Optional) Send notifications by using a .NET app</span></span>
<span data-ttu-id="26995-203">Nesta seção, enviaremos as notificações usando um aplicativo de console .NET</span><span class="sxs-lookup"><span data-stu-id="26995-203">In this section, we will send notifications by using a .NET console app</span></span>

1. <span data-ttu-id="26995-204">Crie um novo aplicativo de console do Visual C#:</span><span class="sxs-lookup"><span data-stu-id="26995-204">Create a new Visual C# console application:</span></span>
   
      ![][20]
2. <span data-ttu-id="26995-205">No Visual Studio, clique em **Ferramentas**, em **Gerenciador de Pacotes NuGet** e em **Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="26995-205">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="26995-206">Isso exibe o saudação Package Manager Console no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="26995-206">This displays hello Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="26995-207">Olá janela do Console do Gerenciador de pacotes, definido Olá **projeto padrão** tooyour novo projeto de aplicativo de console e na janela de console hello, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="26995-207">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="26995-208">Isso adiciona um toohello Referência SDK de Hubs de notificação do Azure usando Olá <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacote NuGet de Hubs Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="26995-208">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="26995-209">Abra o arquivo Program.cs de saudação e adicione o seguinte de saudação `using` instrução:</span><span class="sxs-lookup"><span data-stu-id="26995-209">Open hello Program.cs file and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="26995-210">No seu `Program` classe, adicione o seguinte método de saudação.</span><span class="sxs-lookup"><span data-stu-id="26995-210">In your `Program` class, add hello following method.</span></span> <span data-ttu-id="26995-211">Atualizar o texto de espaço reservado de saudação com seu *DefaultFullSharedAccessSignature* nome de hub e de cadeia de caracteres de conexão de saudação [Portal clássico do Azure].</span><span class="sxs-lookup"><span data-stu-id="26995-211">Update hello placeholder text with your *DefaultFullSharedAccessSignature* connection string and hub name from hello [Azure Classic Portal].</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            await hub.SendGcmNativeNotificationAsync("{ \"data\" : {\"message\":\"Hello from Azure!\"}}");
        }
6. <span data-ttu-id="26995-212">Adicionar Olá seguintes linhas no seu **principal** método:</span><span class="sxs-lookup"><span data-stu-id="26995-212">Add hello following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="26995-213">Pressione Olá F5 toorun chave Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26995-213">Press hello F5 key toorun hello app.</span></span> <span data-ttu-id="26995-214">Você deve receber uma notificação no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="26995-214">You should receive a notification in hello app.</span></span>
   
      ![][21]

#### <a name="optional-send-notifications-by-using-a-mobile-service"></a><span data-ttu-id="26995-215">(Opcional) Enviar notificações usando um serviço móvel</span><span class="sxs-lookup"><span data-stu-id="26995-215">(Optional) Send notifications by using a mobile service</span></span>
1. <span data-ttu-id="26995-216">Acompanhe [Introdução aos Serviços Móveis].</span><span class="sxs-lookup"><span data-stu-id="26995-216">Follow [Get started with Mobile Services].</span></span>
2. <span data-ttu-id="26995-217">Entrar toohello [Portal clássico do Azure]e selecione seu serviço móvel.</span><span class="sxs-lookup"><span data-stu-id="26995-217">Sign in toohello [Azure Classic Portal], and select your mobile service.</span></span>
3. <span data-ttu-id="26995-218">Selecione Olá **Agendador** guia na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="26995-218">Select hello **Scheduler** tab on hello top.</span></span>
   
      ![][22]
4. <span data-ttu-id="26995-219">Crie um novo trabalho agendado, insira um nome e selecione **Sob demanda**.</span><span class="sxs-lookup"><span data-stu-id="26995-219">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
      ![][23]
5. <span data-ttu-id="26995-220">Quando o trabalho de saudação é criado, clique em nome do trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="26995-220">When hello job is created, click hello job name.</span></span> <span data-ttu-id="26995-221">Em seguida, clique em Olá **Script** guia na barra superior hello.</span><span class="sxs-lookup"><span data-stu-id="26995-221">Then click hello **Script** tab on hello top bar.</span></span>
6. <span data-ttu-id="26995-222">Inserir saudação script dentro de sua função de agendador a seguir.</span><span class="sxs-lookup"><span data-stu-id="26995-222">Insert hello following script inside your scheduler function.</span></span> <span data-ttu-id="26995-223">Verifique se tooreplace reservados Olá seu hub nome e hello conexão cadeia de notificação para *DefaultFullSharedAccessSignature* que você obteve anteriormente.</span><span class="sxs-lookup"><span data-stu-id="26995-223">Make sure tooreplace hello placeholders with your notification hub name and hello connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="26995-224">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="26995-224">Click **Save**.</span></span>
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string>');
        notificationHubService.gcm.send(null,'{"data":{"message" : "Hello from Mobile Services!"}}',
          function (error)
          {
            if (!error) {
               console.warn("Notification successful");
            }
            else
            {
              console.warn("Notification failed" + error);
            }
          }
        );
7. <span data-ttu-id="26995-225">Clique em **executar uma vez** na barra inferior de saudação.</span><span class="sxs-lookup"><span data-stu-id="26995-225">Click **Run Once** on hello bottom bar.</span></span> <span data-ttu-id="26995-226">Você deve receber uma notificação do sistema.</span><span class="sxs-lookup"><span data-stu-id="26995-226">You should receive a toast notification.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26995-227">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="26995-227">Next steps</span></span>
<span data-ttu-id="26995-228">Neste exemplo simples, você transmitida notificações tooall seus dispositivos Android.</span><span class="sxs-lookup"><span data-stu-id="26995-228">In this simple example, you broadcasted notifications tooall your Android devices.</span></span> <span data-ttu-id="26995-229">Em ordem tootarget usuários específicos, consulte o tutorial toohello [usar Hubs de notificação toopush notificações toousers].</span><span class="sxs-lookup"><span data-stu-id="26995-229">In order tootarget specific users, refer toohello tutorial [Use Notification Hubs toopush notifications toousers].</span></span> <span data-ttu-id="26995-230">Se você desejar toosegment os usuários, grupos de interesse, você pode ler [toosend de Hubs de notificação de uso últimas notícias].</span><span class="sxs-lookup"><span data-stu-id="26995-230">If you want toosegment your users by interest groups, you can read [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="26995-231">Saiba mais sobre como Hubs de notificação toouse [orientação de Hubs de notificação] e em Olá [Hubs de notificação como toofor Android].</span><span class="sxs-lookup"><span data-stu-id="26995-231">Learn more about how toouse Notification Hubs in [Notification Hubs Guidance] and in hello [Notification Hubs How-toofor Android].</span></span>

<!-- Anchors. -->
[Enable Google Cloud Messaging]: #register
[Configure your Notification Hub]: #configure-hub
[Connecting your app toohello Notification Hub]: #connecting-app
[Run your app with hello emulator]: #run-app
[Send notifications from your back-end]: #send
[Next steps]:#next-steps

<!-- Images. -->

[11]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-configure-android.png

[13]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app1.png
[15]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app3.png

[18]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app7.png
[19]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app8.png

[20]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-android-toast.png
[22]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler2.png

[30]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png


<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Introdução aos Serviços Móveis]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[Portal clássico do Azure]: https://manage.windowsazure.com/
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[orientação de Hubs de notificação]: http://msdn.microsoft.com/library/jj927170.aspx
[Hubs de notificação como toofor Android]: http://msdn.microsoft.com/library/dn282661.aspx

[usar Hubs de notificação toopush notificações toousers]: /manage/services/notification-hubs/notify-users-aspnet
[toosend de Hubs de notificação de uso últimas notícias]: /manage/services/notification-hubs/breaking-news-dotnet
[GCMClient Component page]: http://components.xamarin.com/view/GCMClient
[Xamarin.NotificationHub GitHub page]: https://github.com/SaschaDittmann/Xamarin.NotificationHub
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Componente de mensagens de nuvem do Google]: http://components.xamarin.com/view/GCMClient/
[Componente de mensagens do Azure]: http://components.xamarin.com/view/azure-messaging
