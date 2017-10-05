---
title: "Introdução aos Hubs de Notificação para aplicativos Xamarin.Android | Microsoft Docs"
description: "Neste tutorial, você aprende a usar os Hubs de Notificação do Azure para enviar notificações por push a um aplicativo Xamarin Android."
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
ms.openlocfilehash: e0ef1b006a2b202c08a71caaff4ef4d763d50d0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-notification-hubs-with-xamarin-for-android"></a><span data-ttu-id="57616-103">Introdução aos Hubs de Notificação com o Xamarin para Android</span><span class="sxs-lookup"><span data-stu-id="57616-103">Get started with Notification Hubs with Xamarin for Android</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="57616-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="57616-104">Overview</span></span>
<span data-ttu-id="57616-105">Este tutorial mostra como usar os Hubs de Notificação do Azure para enviar notificações por push para um aplicativo Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="57616-105">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Xamarin.Android application.</span></span>
<span data-ttu-id="57616-106">Você criará um aplicativo Xamarin.Android em branco que recebe notificações por push usando o GCM(Google Cloud Messaging).</span><span class="sxs-lookup"><span data-stu-id="57616-106">You'll create a blank Xamarin.Android app that receives push notifications by using Google Cloud Messaging (GCM).</span></span> <span data-ttu-id="57616-107">Ao finalizar, você poderá usar seu hub de notificação para transmitir notificações por push a todos os dispositivos que executam seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="57616-107">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span> <span data-ttu-id="57616-108">O código concluído está disponível na amostra do [aplicativo NotificationHubs][GitHub].</span><span class="sxs-lookup"><span data-stu-id="57616-108">The finished code is available in the [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="57616-109">Este tutorial demonstra o cenário de transmissão simples usando Hubs de Notificação.</span><span class="sxs-lookup"><span data-stu-id="57616-109">This tutorial demonstrates the simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="57616-110">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="57616-110">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="57616-111">O código completo para este tutorial pode ser encontrado no GitHub [aqui](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).</span><span class="sxs-lookup"><span data-stu-id="57616-111">The completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57616-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="57616-112">Prerequisites</span></span>
<span data-ttu-id="57616-113">Este tutorial exige o seguinte:</span><span class="sxs-lookup"><span data-stu-id="57616-113">This tutorial requires the following:</span></span>

* <span data-ttu-id="57616-114">Visual Studio com Xamarin no Windows ou Xamarin Studio no Mac OS X. Encontre instruções de instalação completas em [Configuração e instalação para Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="57616-114">Visual Studio with Xamarin on Windows or Xamarin Studio on Mac OS X. Complete installation instructions are on [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* <span data-ttu-id="57616-115">Conta ativa do Google</span><span class="sxs-lookup"><span data-stu-id="57616-115">Active Google account</span></span>
* <span data-ttu-id="57616-116">[Componente de mensagens do Azure]</span><span class="sxs-lookup"><span data-stu-id="57616-116">[Azure Messaging Component]</span></span>
* <span data-ttu-id="57616-117">[Componente de mensagens de nuvem do Google]</span><span class="sxs-lookup"><span data-stu-id="57616-117">[Google Cloud Messaging Client Component]</span></span>

<span data-ttu-id="57616-118">A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais sobre Hubs de Notificação para aplicativos Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="57616-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin.Android apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="57616-119">Para concluir este tutorial, você precisa ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="57616-119">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="57616-120">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="57616-120">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="57616-121">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="57616-121">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).</span></span>
> 
> 

## <a name="enable-google-cloud-messaging"></a><span data-ttu-id="57616-122">Habilitar o sistema de mensagens em nuvem do Google</span><span class="sxs-lookup"><span data-stu-id="57616-122">Enable Google Cloud Messaging</span></span>
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="57616-123">Configurar seu Hub de Notificação</span><span class="sxs-lookup"><span data-stu-id="57616-123">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li><p><span data-ttu-id="57616-124">Clique na guia <b>Configurar</b> na parte superior, digite o valor de <b>Chave de API</b> que você obteve na etapa anterior e clique em <b>Salvar</b>.</span><span class="sxs-lookup"><span data-stu-id="57616-124">Click the <b>Configure</b> tab at the top, enter the <b>API Key</b> value you obtained in the previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>
<span data-ttu-id="57616-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span><span class="sxs-lookup"><span data-stu-id="57616-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span></span>

<span data-ttu-id="57616-126">Agora, o seu hub de notificação está configurado para funcionar com o GCM e você tem as cadeias de conexão ao registrar seu aplicativo para receber notificações e enviar notificações por push.</span><span class="sxs-lookup"><span data-stu-id="57616-126">Your notification hub is now configured to work with GCM, and you have the connection strings to both register your app to receive notifications and to send push notifications.</span></span>

## <a name="connect-your-app-to-the-notification-hub"></a><span data-ttu-id="57616-127">Conectar seu aplicativo ao hub de notificação</span><span class="sxs-lookup"><span data-stu-id="57616-127">Connect your app to the notification hub</span></span>
### <a name="create-a-new-project"></a><span data-ttu-id="57616-128">Criar um novo projeto</span><span class="sxs-lookup"><span data-stu-id="57616-128">Create a new project</span></span>
1. <span data-ttu-id="57616-129">No Xamarin Studio, clique em **Nova Solução**, clique em **Aplicativo Android** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="57616-129">In Xamarin Studio, click **New Solution**, click **Android App**, and click **Next**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project1.png)

2. <span data-ttu-id="57616-130">Insira o **Nome do Aplicativo** e o **Identificador**.</span><span class="sxs-lookup"><span data-stu-id="57616-130">Enter your **App Name** and **Identifier**.</span></span> <span data-ttu-id="57616-131">Clique nas **Plataformas de Destino** às quais você deseja dar suporte e clique em **Avançar** e em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="57616-131">Click the **Target Plaforms** you want to support and then click **Next** and **Create**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project2.png)

    <span data-ttu-id="57616-132">Isso cria um novo projeto Android.</span><span class="sxs-lookup"><span data-stu-id="57616-132">This creates a new Android project.</span></span>

1. <span data-ttu-id="57616-133">Abra as propriedades do projeto clicando com o botão direito em seu novo projeto no modo de exibição Solução e escolha **Opções**.</span><span class="sxs-lookup"><span data-stu-id="57616-133">Open the project properties by right-clicking your new project in the Solution view and choosing **Options**.</span></span> <span data-ttu-id="57616-134">Selecione o item **Aplicativo Android** na seção **Build**.</span><span class="sxs-lookup"><span data-stu-id="57616-134">Select the **Android Application** item in the **Build** section.</span></span>
   
    <span data-ttu-id="57616-135">Certifique-se de que a primeira letra de seu **nome do pacote** esteja em minúscula.</span><span class="sxs-lookup"><span data-stu-id="57616-135">Ensure that the first letter of your **Package name** is lowercase.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="57616-136">A primeira letra do nome do pacote deve estar em minúscula.</span><span class="sxs-lookup"><span data-stu-id="57616-136">The first letter of the package name must be lowercase.</span></span> <span data-ttu-id="57616-137">Caso contrário, você receberá erros de manifesto do aplicativo ao registrar **BroadcastReceiver** e **IntentFilter** para as notificações por push abaixo.</span><span class="sxs-lookup"><span data-stu-id="57616-137">Otherwise, you will receive application manifest errors when you register your **BroadcastReceiver** and **IntentFilter** for push notifications below.</span></span>
   > 
   > 
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub--xamarin-android-app-options.png)
2. <span data-ttu-id="57616-138">Opcionalmente, defina a **Versão mínima do Android** como outro Nível de API.</span><span class="sxs-lookup"><span data-stu-id="57616-138">Optionally, set the **Minimum Android version** to another API Level.</span></span>
3. <span data-ttu-id="57616-139">Opcionalmente, defina a **Versão de destino do Android** para a outra versão de API que você gostaria de ter como destino (deve ser API nível 8 ou superior).</span><span class="sxs-lookup"><span data-stu-id="57616-139">Optionally, set the **Target Android version** to the another API version that you want to target (must be API level 8 or higher).</span></span>

<span data-ttu-id="57616-140">Clique em **OK** e feche a caixa de diálogo Opções do Projeto.</span><span class="sxs-lookup"><span data-stu-id="57616-140">Click **OK** and close the Project Options dialog.</span></span>

### <a name="add-the-required-components-to-your-project"></a><span data-ttu-id="57616-141">Adicionar os componentes necessários ao seu projeto</span><span class="sxs-lookup"><span data-stu-id="57616-141">Add the required components to your project</span></span>
<span data-ttu-id="57616-142">O cliente de mensagens de nuvem do Google disponível na loja de componentes Xamarin simplifica o processo de oferecer suporte de notificações por push no Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="57616-142">The Google Cloud Messaging Client available on the Xamarin Component Store simplifies the process of supporting push notifications in Xamarin.Android.</span></span>

1. <span data-ttu-id="57616-143">Clique com o botão direito do mouse na pasta Componentes no aplicativo Xamarin.Android e escolha **Obter Mais Componentes**.</span><span class="sxs-lookup"><span data-stu-id="57616-143">Right-click the Components folder in Xamarin.Android app and choose **Get More Components**.</span></span>
2. <span data-ttu-id="57616-144">Pesquise o componente **Mensagens do Azure** e adicione-o ao projeto.</span><span class="sxs-lookup"><span data-stu-id="57616-144">Search for the **Azure Messaging** component and add it to the project.</span></span>
3. <span data-ttu-id="57616-145">Pesquise o componente **Cliente de Mensagens de Nuvem do Azure** e adicione-o ao projeto.</span><span class="sxs-lookup"><span data-stu-id="57616-145">Search for the **Google Cloud Messaging Client** component and add it to the project.</span></span>

### <a name="set-up-notification-hubs-in-your-project"></a><span data-ttu-id="57616-146">Configurar hubs de notificação em seu projeto</span><span class="sxs-lookup"><span data-stu-id="57616-146">Set up notification hubs in your project</span></span>
1. <span data-ttu-id="57616-147">Colete as informações a seguir para o aplicativo Android e o hub de notificação:</span><span class="sxs-lookup"><span data-stu-id="57616-147">Gather the following information for your Android app and notification hub:</span></span>
   
   * <span data-ttu-id="57616-148">**GoogleProjectNumber**: obtenha o valor de Número do Projeto da visão geral do seu aplicativo no Google Developer Portal.</span><span class="sxs-lookup"><span data-stu-id="57616-148">**GoogleProjectNumber**:  Get this Project Number value from the overview of your app on the Google Developer Portal.</span></span> <span data-ttu-id="57616-149">Você anotou este valor anteriormente quando criou o aplicativo no portal.</span><span class="sxs-lookup"><span data-stu-id="57616-149">You made a note of this value earlier when you created the app on the portal.</span></span>
   * <span data-ttu-id="57616-150">**Cadeia de conexão de escuta**: no painel do [Portal Clássico do Azure], clique em **Exibir cadeias de conexão**.</span><span class="sxs-lookup"><span data-stu-id="57616-150">**Listen connection string**: On the dashboard in the [Azure Classic Portal], click **View connection strings**.</span></span> <span data-ttu-id="57616-151">Copiar a sequência de conexão *DefaultListenSharedAccessSignature* para esse valor.</span><span class="sxs-lookup"><span data-stu-id="57616-151">Copy the *DefaultListenSharedAccessSignature* connection string for this value.</span></span>
   * <span data-ttu-id="57616-152">**Nome do hub**: este é o nome do hub no [Portal Clássico do Azure].</span><span class="sxs-lookup"><span data-stu-id="57616-152">**Hub name**: This is the name of your hub from the [Azure Classic Portal].</span></span> <span data-ttu-id="57616-153">Por exemplo, *mynotificationhub2*.</span><span class="sxs-lookup"><span data-stu-id="57616-153">For example, *mynotificationhub2*.</span></span>
     
     <span data-ttu-id="57616-154">Crie uma classe **Constants.cs** para seu projeto de Xamarin e defina os valores de constantes a seguir na classe.</span><span class="sxs-lookup"><span data-stu-id="57616-154">Create a **Constants.cs** class for your Xamarin project and define the following constant values in the class.</span></span> <span data-ttu-id="57616-155">Substitua os espaços reservados pelos seus valores.</span><span class="sxs-lookup"><span data-stu-id="57616-155">Replace the placeholders with your values.</span></span>
     
       <span data-ttu-id="57616-156">public static class Constants   {</span><span class="sxs-lookup"><span data-stu-id="57616-156">public static class Constants   {</span></span>
     
           public const string SenderID = "<GoogleProjectNumber>"; // Google API Project Number
           public const string ListenConnectionString = "<Listen connection string>";
           public const string NotificationHubName = "<hub name>";
       <span data-ttu-id="57616-157">}</span><span class="sxs-lookup"><span data-stu-id="57616-157">}</span></span>
2. <span data-ttu-id="57616-158">Adicionar as seguintes instruções à **MainActivity.cs**:</span><span class="sxs-lookup"><span data-stu-id="57616-158">Add the following using statements to **MainActivity.cs**:</span></span>
   
        using Android.Util;
        using Gcm.Client;
3. <span data-ttu-id="57616-159">Adicione uma variável de instância à classe `MainActivity` que será usada para mostrar uma caixa de diálogo de alerta quando o aplicativo estiver em execução:</span><span class="sxs-lookup"><span data-stu-id="57616-159">Add an instance variable to the `MainActivity` class that will be used to show an alert dialog when the app is running:</span></span>
   
        public static MainActivity instance;
4. <span data-ttu-id="57616-160">Criar o seguinte método na classe **MainActivity** :</span><span class="sxs-lookup"><span data-stu-id="57616-160">Create the following method in the **MainActivity** class:</span></span>
   
        private void RegisterWithGCM()
        {
            // Check to ensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);
   
            // Register for push notifications
            Log.Info("MainActivity", "Registering...");
            GcmClient.Register(this, Constants.SenderID);
        }
5. <span data-ttu-id="57616-161">No método `OnCreate` de **MainActivity.cs**, inicialize a variável `instance` e adicione uma chamada para `RegisterWithGCM`:</span><span class="sxs-lookup"><span data-stu-id="57616-161">In the `OnCreate` method of **MainActivity.cs**, initialize the `instance` variable and add a call to `RegisterWithGCM`:</span></span>
   
        protected override void OnCreate (Bundle bundle)
        {
            instance = this;
   
            base.OnCreate (bundle);
   
            // Set your view from the "main" layout resource
            SetContentView (Resource.Layout.Main);
   
            // Get your button from the layout resource,
            // and attach an event to it
            Button button = FindViewById<Button> (Resource.Id.myButton);
   
            RegisterWithGCM();
        }
6. <span data-ttu-id="57616-162">Crie uma nova classe, **MyBroadcastReceiver**.</span><span class="sxs-lookup"><span data-stu-id="57616-162">Create a new class, **MyBroadcastReceiver**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="57616-163">Mostraremos a criação de uma classe **BroadcastReceiver** desde o início.</span><span class="sxs-lookup"><span data-stu-id="57616-163">We will walk through creating a **BroadcastReceiver** class from scratch below.</span></span> <span data-ttu-id="57616-164">No entanto, uma alternativa rápida para criar manualmente o **MyBroadcastReceiver.cs** é consultar o arquivo **GcmService.cs** encontrado na amostra do projeto Xamarin.Android incluído com os [exemplos do NotificationHubs][GitHub].</span><span class="sxs-lookup"><span data-stu-id="57616-164">However, a quick alternative to manually creating **MyBroadcastReceiver.cs** is to refer to the **GcmService.cs** file found in the sample Xamarin.Android project included with the [NotificationHubs samples][GitHub].</span></span> <span data-ttu-id="57616-165">Duplicar o **GcmService.cs** e alterar os nomes de classe pode ser uma ótima maneira de começar.</span><span class="sxs-lookup"><span data-stu-id="57616-165">Duplicating **GcmService.cs** and changing class names can be a great place to start as well.</span></span>
   > 
   > 
7. <span data-ttu-id="57616-166">Adicione as instruções using a seguir a **MyBroadcastReceiver.cs** (para se referir ao componente e ao assembly adicionados anteriormente):</span><span class="sxs-lookup"><span data-stu-id="57616-166">Add the following using statements to **MyBroadcastReceiver.cs** (referring to the component and assembly that you added earlier):</span></span>
   
        using System.Collections.Generic;
        using System.Text;
        using Android.App;
        using Android.Content;
        using Android.Util;
        using Gcm.Client;
        using WindowsAzure.Messaging;
8. <span data-ttu-id="57616-167">Em **MyBroadcastReceiver.cs**, adicione as seguintes solicitações de permissão entre as instruções **using** e a declaração de **namespace**:</span><span class="sxs-lookup"><span data-stu-id="57616-167">In **MyBroadcastReceiver.cs**, add the following permission requests between the **using** statements and the **namespace** declaration:</span></span>
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is needed only for Android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
9. <span data-ttu-id="57616-168">Em **MyBroadcastReceiver.cs**, altere a classe **MyBroadcastReceiver** para corresponder ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="57616-168">In **MyBroadcastReceiver.cs**, change the **MyBroadcastReceiver** class to match the following:</span></span>
   
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
10. <span data-ttu-id="57616-169">Adicione outra classe a **MyBroadcastReceiver.cs** chamada **PushHandlerService**, que deriva de **GcmServiceBase**.</span><span class="sxs-lookup"><span data-stu-id="57616-169">Add another class in **MyBroadcastReceiver.cs** named **PushHandlerService**, which derives from **GcmServiceBase**.</span></span> <span data-ttu-id="57616-170">Certifique-se de aplicar o atributo **Service** à classe:</span><span class="sxs-lookup"><span data-stu-id="57616-170">Make sure to apply the **Service** attribute to the class:</span></span>
    
         [Service] // Must use the service tag
         public class PushHandlerService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }
             private NotificationHub Hub { get; set; }
    
             public PushHandlerService() : base(Constants.SenderID)
                {
                 Log.Info(MyBroadcastReceiver.TAG, "PushHandlerService() constructor");
             }
         }
11. <span data-ttu-id="57616-171">**GcmServiceBase** implementa os métodos **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()** e **OnError()**.</span><span class="sxs-lookup"><span data-stu-id="57616-171">**GcmServiceBase** implements methods **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()**, and **OnError()**.</span></span> <span data-ttu-id="57616-172">Nossa classe de implementação **PushHandlerService** deve substituir esses métodos e esses métodos serão acionados em resposta à interação com o hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="57616-172">Our **PushHandlerService** implementation class must override these methods, and these methods will fire in response to interacting with the notification hub.</span></span>
12. <span data-ttu-id="57616-173">Substitua o método **OnRegistered()** em **PushHandlerService** usando o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="57616-173">Override the **OnRegistered()** method in **PushHandlerService** by using the following code:</span></span>
    
         protected override void OnRegistered(Context context, string registrationId)
         {
             Log.Verbose(MyBroadcastReceiver.TAG, "GCM Registered: " + registrationId);
             RegistrationID = registrationId;
    
             createNotification("PushHandlerService-GCM Registered...",
                                 "The device has been Registered!");
    
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
    > <span data-ttu-id="57616-174">No código **OnRegistered()** acima, você deve observar a capacidade de especificar marcas para se registrar em canais de mensagens específicos.</span><span class="sxs-lookup"><span data-stu-id="57616-174">In the **OnRegistered()** code above, you should note the ability to specify tags to register for specific messaging channels.</span></span>
    > 
    > 
13. <span data-ttu-id="57616-175">Substitua o método **OnMessage** em **PushHandlerService** usando o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="57616-175">Override the **OnMessage** method in **PushHandlerService** by using the following code:</span></span>
    
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
14. <span data-ttu-id="57616-176">Adicione os métodos **createNotification** e **dialogNotify** ao **PushHandlerService** para notificar os usuários quando a notificação for recebida.</span><span class="sxs-lookup"><span data-stu-id="57616-176">Add the following **createNotification** and **dialogNotify** methods to **PushHandlerService** for notifying users when a notification is received.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="57616-177">O design de notificação no Android versão 5.0 e posterior teve uma mudança significativa das versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="57616-177">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="57616-178">Se você testar isso no Android 5.0 ou posterior, o aplicativo precisará estar em execução para receber a notificação.</span><span class="sxs-lookup"><span data-stu-id="57616-178">If you test this on Android 5.0 or later, the app will need to be running to receive the notification.</span></span> <span data-ttu-id="57616-179">Para obter mais informações, consulte [Notificações do Android](http://go.microsoft.com/fwlink/?LinkId=615880).</span><span class="sxs-lookup"><span data-stu-id="57616-179">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
    > 
    > 
    
        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;
    
            //Create an intent to show UI
            var uiIntent = new Intent(this, typeof(MainActivity));
    
            //Create the notification
            var notification = new Notification(Android.Resource.Drawable.SymActionEmail, title);
    
            //Auto-cancel will remove the notification once the user touches it
            notification.Flags = NotificationFlags.AutoCancel;
    
            //Set the notification info
            //we use the pending intent, passing our ui intent over, which will get called
            //when the notification is tapped.
            notification.SetLatestEventInfo(this, title, desc, PendingIntent.GetActivity(this, 0, uiIntent, 0));
    
            //Show the notification
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
15. <span data-ttu-id="57616-180">Substitua os membros abstratos **OnUnRegistered()**, **OnRecoverableError()** e **OnError()** para que o código seja compilado:</span><span class="sxs-lookup"><span data-stu-id="57616-180">Override abstract members **OnUnRegistered()**, **OnRecoverableError()**, and **OnError()** so that your code compiles:</span></span>
    
        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Verbose(MyBroadcastReceiver.TAG, "GCM Unregistered: " + registrationId);
    
            createNotification("GCM Unregistered...", "The device has been unregistered!");
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

## <a name="run-your-app-in-the-emulator"></a><span data-ttu-id="57616-181">Executar o aplicativo no emulador</span><span class="sxs-lookup"><span data-stu-id="57616-181">Run your app in the emulator</span></span>
<span data-ttu-id="57616-182">Se você executar o aplicativo no emulador, certifique-se de usar um Android Virtual Device (AVD) que oferece suporte a APIs do Google.</span><span class="sxs-lookup"><span data-stu-id="57616-182">If you run this app in the emulator, make sure that you use an Android Virtual Device (AVD) that supports Google APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="57616-183">Para receber as notificações por push, você deve configurar uma conta do Google em seu Dispositivo Virtual Android.</span><span class="sxs-lookup"><span data-stu-id="57616-183">In order to receive push notifications, you must set up a Google account on your Android Virtual Device.</span></span> <span data-ttu-id="57616-184">(No emulador, navegue até **Configurações** e clique em **Adicionar Conta**). Além disso, certifique-se de que o emulador esteja conectado à Internet.</span><span class="sxs-lookup"><span data-stu-id="57616-184">(In the emulator, navigate to **Settings** and click **Add Account**.) Also, make sure that the emulator is connected to the Internet.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="57616-185">O design de notificação no Android versão 5.0 e posterior teve uma mudança significativa das versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="57616-185">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="57616-186">Para obter mais informações, consulte [Notificações do Android](http://go.microsoft.com/fwlink/?LinkId=615880).</span><span class="sxs-lookup"><span data-stu-id="57616-186">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
> 
> 

1. <span data-ttu-id="57616-187">Em **Ferramentas**, clique em **Abrir Gerenciador de Emulador do Android**, selecione seu dispositivo e clique em **Editar**.</span><span class="sxs-lookup"><span data-stu-id="57616-187">From **Tools**, click **Open Android Emulator Manager**, select your device, and then click **Edit**.</span></span>
   
      ![][18]
2. <span data-ttu-id="57616-188">Selecione **APIs do Google**, em **Destino** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="57616-188">Select **Google APIs** in **Target**, and then click **OK**.</span></span>
   
      ![][19]
3. <span data-ttu-id="57616-189">Na barra de ferramentas superior, clique em **Executar**e, em seguida, selecione seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="57616-189">On the top toolbar, click **Run**, and then select your app.</span></span> <span data-ttu-id="57616-190">Isso iniciará o emulador e executará o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="57616-190">This starts the emulator and runs the app.</span></span>
   
   <span data-ttu-id="57616-191">O aplicativo recupera o *registrationId* do GCM e registrará no Hub de Notificação.</span><span class="sxs-lookup"><span data-stu-id="57616-191">The app retrieves the *registrationId* from GCM and registers with the notification hub.</span></span>

## <a name="send-notifications-from-your-backend"></a><span data-ttu-id="57616-192">Enviar notificações de seu back-end</span><span class="sxs-lookup"><span data-stu-id="57616-192">Send notifications from your backend</span></span>
<span data-ttu-id="57616-193">Você pode testar o recebimento de notificações no aplicativo enviando notificações no [Portal Clássico do Azure] por meio da guia de depuração no hub de notificação, como mostrado na tela abaixo.</span><span class="sxs-lookup"><span data-stu-id="57616-193">You can test receiving notifications in your app by sending notifications in the [Azure Classic Portal] via the debug tab on the notification hub, as shown in the screen below.</span></span>

![][30]

<span data-ttu-id="57616-194">Normalmente, as notificações por push são enviadas em um serviço de back-end como os Serviços Móveis ou ASP.NET por meio de uma biblioteca compatível.</span><span class="sxs-lookup"><span data-stu-id="57616-194">Push notifications are normally sent in a backend service like Mobile Services or ASP.NET through a compatible library.</span></span> <span data-ttu-id="57616-195">Você também poderá usar a API REST diretamente para enviar mensagens de notificação se uma biblioteca não estiver disponível para o back-end.</span><span class="sxs-lookup"><span data-stu-id="57616-195">You can also use the REST API directly to send notification messages if a library is not available for your backend.</span></span>

<span data-ttu-id="57616-196">Veja a seguir uma lista de outros tutoriais que talvez você queira examinar para o envio de notificações:</span><span class="sxs-lookup"><span data-stu-id="57616-196">Here is a list of some other tutorials that you may want to review for sending notifications:</span></span>

* <span data-ttu-id="57616-197">ASP.NET: confira [Usar Hubs de Notificação para enviar notificações por push aos usuários].</span><span class="sxs-lookup"><span data-stu-id="57616-197">ASP.NET: See [Use Notification Hubs to push notifications to users].</span></span>
* <span data-ttu-id="57616-198">SDK do Java para Hubs de Notificação do Azure: confira [Como usar os Hubs de Notificação do Java](notification-hubs-java-push-notification-tutorial.md) para enviar notificações do Java.</span><span class="sxs-lookup"><span data-stu-id="57616-198">Azure Notification Hubs Java SDK: See [How to use Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) for sending notifications from Java.</span></span> <span data-ttu-id="57616-199">Isso foi testado no Eclipse para desenvolvimento no Android.</span><span class="sxs-lookup"><span data-stu-id="57616-199">This has been tested in Eclipse for Android Development.</span></span>
* <span data-ttu-id="57616-200">PHP: confira [Como usar Hubs de Notificação do PHP](notification-hubs-php-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="57616-200">PHP: See [How to use Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

<span data-ttu-id="57616-201">Nas próximas subseções do tutorial, você envia notificações usando um aplicativo de console .NET e um serviço móvel por meio de um script de nó.</span><span class="sxs-lookup"><span data-stu-id="57616-201">In the next subsections of the tutorial, you send notifications by using a .NET console app, and by using a mobile service through a node script.</span></span>

#### <a name="optional-send-notifications-by-using-a-net-app"></a><span data-ttu-id="57616-202">(Opcional) Enviar notificações usando um aplicativo .NET</span><span class="sxs-lookup"><span data-stu-id="57616-202">(Optional) Send notifications by using a .NET app</span></span>
<span data-ttu-id="57616-203">Nesta seção, enviaremos as notificações usando um aplicativo de console .NET</span><span class="sxs-lookup"><span data-stu-id="57616-203">In this section, we will send notifications by using a .NET console app</span></span>

1. <span data-ttu-id="57616-204">Crie um novo aplicativo de console do Visual C#:</span><span class="sxs-lookup"><span data-stu-id="57616-204">Create a new Visual C# console application:</span></span>
   
      ![][20]
2. <span data-ttu-id="57616-205">No Visual Studio, clique em **Ferramentas**, em **Gerenciador de Pacotes NuGet** e em **Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="57616-205">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="57616-206">Isso exibe o Console do Gerenciador de Pacotes no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="57616-206">This displays the Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="57616-207">Na janela do Console do Gerenciador de Pacotes, defina o **Projeto padrão** como o seu novo projeto de aplicativo do console e execute o seguinte comando na janela do console:</span><span class="sxs-lookup"><span data-stu-id="57616-207">In the Package Manager Console window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="57616-208">Isso adiciona uma referência ao SDK dos Hubs de Notificação do Azure usando o <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacote NuGet Microsoft.Azure.Notification Hubs</a>.</span><span class="sxs-lookup"><span data-stu-id="57616-208">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="57616-209">Abra o arquivo Program.cs e adicione a seguinte instrução `using` :</span><span class="sxs-lookup"><span data-stu-id="57616-209">Open the Program.cs file and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="57616-210">Em sua classe `Program`, adicione o seguinte método:</span><span class="sxs-lookup"><span data-stu-id="57616-210">In your `Program` class, add the following method.</span></span> <span data-ttu-id="57616-211">Atualize o texto do espaço reservado com sua cadeia de conexão do *DefaultFullSharedAccessSignature* e o nome do hub no [Portal Clássico do Azure].</span><span class="sxs-lookup"><span data-stu-id="57616-211">Update the placeholder text with your *DefaultFullSharedAccessSignature* connection string and hub name from the [Azure Classic Portal].</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            await hub.SendGcmNativeNotificationAsync("{ \"data\" : {\"message\":\"Hello from Azure!\"}}");
        }
6. <span data-ttu-id="57616-212">Adicione as seguintes linhas ao método **Main** :</span><span class="sxs-lookup"><span data-stu-id="57616-212">Add the following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="57616-213">Pressione a tecla F5 para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="57616-213">Press the F5 key to run the app.</span></span> <span data-ttu-id="57616-214">Você deve receber uma notificação no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="57616-214">You should receive a notification in the app.</span></span>
   
      ![][21]

#### <a name="optional-send-notifications-by-using-a-mobile-service"></a><span data-ttu-id="57616-215">(Opcional) Enviar notificações usando um serviço móvel</span><span class="sxs-lookup"><span data-stu-id="57616-215">(Optional) Send notifications by using a mobile service</span></span>
1. <span data-ttu-id="57616-216">Acompanhe [Introdução aos Serviços Móveis].</span><span class="sxs-lookup"><span data-stu-id="57616-216">Follow [Get started with Mobile Services].</span></span>
2. <span data-ttu-id="57616-217">Entre no [Portal Clássico do Azure]e selecione o serviço móvel.</span><span class="sxs-lookup"><span data-stu-id="57616-217">Sign in to the [Azure Classic Portal], and select your mobile service.</span></span>
3. <span data-ttu-id="57616-218">Selecione a guia **Agendador** na parte superior.</span><span class="sxs-lookup"><span data-stu-id="57616-218">Select the **Scheduler** tab on the top.</span></span>
   
      ![][22]
4. <span data-ttu-id="57616-219">Crie um novo trabalho agendado, insira um nome e selecione **Sob demanda**.</span><span class="sxs-lookup"><span data-stu-id="57616-219">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
      ![][23]
5. <span data-ttu-id="57616-220">Quando o trabalho for criado, clique no nome do trabalho.</span><span class="sxs-lookup"><span data-stu-id="57616-220">When the job is created, click the job name.</span></span> <span data-ttu-id="57616-221">Em seguida, clique na guia **Script** na barra superior.</span><span class="sxs-lookup"><span data-stu-id="57616-221">Then click the **Script** tab on the top bar.</span></span>
6. <span data-ttu-id="57616-222">Insira o script a seguir em sua função de Agendador.</span><span class="sxs-lookup"><span data-stu-id="57616-222">Insert the following script inside your scheduler function.</span></span> <span data-ttu-id="57616-223">Certifique-se de substituir os espaços reservados pelo nome de seu hub de notificação e pela cadeia de conexão para a *DefaultFullSharedAccessSignature* que você obteve anteriormente.</span><span class="sxs-lookup"><span data-stu-id="57616-223">Make sure to replace the placeholders with your notification hub name and the connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="57616-224">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="57616-224">Click **Save**.</span></span>
   
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
7. <span data-ttu-id="57616-225">Clique em **Executar uma vez** na barra inferior.</span><span class="sxs-lookup"><span data-stu-id="57616-225">Click **Run Once** on the bottom bar.</span></span> <span data-ttu-id="57616-226">Você deve receber uma notificação do sistema.</span><span class="sxs-lookup"><span data-stu-id="57616-226">You should receive a toast notification.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57616-227">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="57616-227">Next steps</span></span>
<span data-ttu-id="57616-228">Neste exemplo simples, você envia notificações para todos os seus dispositivos Android.</span><span class="sxs-lookup"><span data-stu-id="57616-228">In this simple example, you broadcasted notifications to all your Android devices.</span></span> <span data-ttu-id="57616-229">Para selecionar usuários de destino específicos, consulte o tutorial [Usar Hubs de Notificação para enviar notificações por push aos usuários].</span><span class="sxs-lookup"><span data-stu-id="57616-229">In order to target specific users, refer to the tutorial [Use Notification Hubs to push notifications to users].</span></span> <span data-ttu-id="57616-230">Se desejar segmentar os usuários por grupos de interesse, você poderá ler [Usar Hubs de Notificação para enviar notícias mais recentes].</span><span class="sxs-lookup"><span data-stu-id="57616-230">If you want to segment your users by interest groups, you can read [Use Notification Hubs to send breaking news].</span></span> <span data-ttu-id="57616-231">Saiba mais sobre como usar Hubs de Notificação em [Diretrizes dos Hubs de Notificação] e em [Instruções sobre Hubs de Notificação para Android].</span><span class="sxs-lookup"><span data-stu-id="57616-231">Learn more about how to use Notification Hubs in [Notification Hubs Guidance] and in the [Notification Hubs How-To for Android].</span></span>

<!-- Anchors. -->
[Enable Google Cloud Messaging]: #register
[Configure your Notification Hub]: #configure-hub
[Connecting your app to the Notification Hub]: #connecting-app
[Run your app with the emulator]: #run-app
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
<span data-ttu-id="57616-232">[Introdução aos Serviços Móveis]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service</span><span class="sxs-lookup"><span data-stu-id="57616-232">[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service</span></span>
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

<span data-ttu-id="57616-233">[Portal Clássico do Azure]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="57616-233">[Azure Classic Portal]: https://manage.windowsazure.com/</span></span>
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
<span data-ttu-id="57616-234">[Diretrizes dos Hubs de Notificação]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="57616-234">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
<span data-ttu-id="57616-235">[Instruções sobre Hubs de Notificação para Android]: http://msdn.microsoft.com/library/dn282661.aspx</span><span class="sxs-lookup"><span data-stu-id="57616-235">[Notification Hubs How-To for Android]: http://msdn.microsoft.com/library/dn282661.aspx</span></span>

<span data-ttu-id="57616-236">[Usar Hubs de Notificação para enviar notificações por push aos usuários]: /manage/services/notification-hubs/notify-users-aspnet</span><span class="sxs-lookup"><span data-stu-id="57616-236">[Use Notification Hubs to push notifications to users]: /manage/services/notification-hubs/notify-users-aspnet</span></span>
<span data-ttu-id="57616-237">[Usar Hubs de Notificação para enviar notícias mais recentes]: /manage/services/notification-hubs/breaking-news-dotnet</span><span class="sxs-lookup"><span data-stu-id="57616-237">[Use Notification Hubs to send breaking news]: /manage/services/notification-hubs/breaking-news-dotnet</span></span>
[GCMClient Component page]: http://components.xamarin.com/view/GCMClient
[Xamarin.NotificationHub GitHub page]: https://github.com/SaschaDittmann/Xamarin.NotificationHub
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
<span data-ttu-id="57616-238">[Componente de mensagens de nuvem do Google]: http://components.xamarin.com/view/GCMClient/</span><span class="sxs-lookup"><span data-stu-id="57616-238">[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/</span></span>
<span data-ttu-id="57616-239">[Componente de mensagens do Azure]: http://components.xamarin.com/view/azure-messaging</span><span class="sxs-lookup"><span data-stu-id="57616-239">[Azure Messaging Component]: http://components.xamarin.com/view/azure-messaging</span></span>
