---
title: "aaaiOS notificações por Push com Hubs de notificação para aplicativos Xamarin | Microsoft Docs"
description: "Neste tutorial, você aprenderá como toouse Hubs de notificação do Azure toosend enviar por push o aplicativo do iOS notificações tooa Xamarin."
services: notification-hubs
keywords: "notificações por push do IOS, mensagens por push, notificações por push, mensagem por push"
documentationcenter: xamarin
author: ysxu
manager: erikre
editor: 
ms.assetid: 4d4dfd42-c5a5-4360-9d70-7812f96924d2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 8db60338047dd53074b4d3d4bb127aa6d9f13a25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="ios-push-notifications-with-notification-hubs-for-xamarin-apps"></a><span data-ttu-id="89b32-104">Notificações por push do iOS com Hubs de Notificação para aplicativos Xamarin</span><span class="sxs-lookup"><span data-stu-id="89b32-104">iOS Push Notifications with Notification Hubs for Xamarin apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="89b32-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="89b32-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="89b32-106">toocomplete neste tutorial, você deve ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="89b32-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="89b32-107">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="89b32-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="89b32-108">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="89b32-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="89b32-109">Este tutorial mostra como o aplicativo do iOS tooan notificações de envio toouse toosend de Hubs de notificação do Azure.</span><span class="sxs-lookup"><span data-stu-id="89b32-109">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooan iOS application.</span></span>
<span data-ttu-id="89b32-110">Você criará um aplicativo xamarin em branco que recebe notificações por push usando Olá [Apple Push Notification Service (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span><span class="sxs-lookup"><span data-stu-id="89b32-110">You'll create a blank Xamarin.iOS app that receives push notifications by using hello [Apple Push Notification Service (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span></span> <span data-ttu-id="89b32-111">Quando você terminar, você será capaz de toouse sua toobroadcast de hub de notificação por push notificações tooall Olá a dispositivos que executam seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="89b32-111">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span> <span data-ttu-id="89b32-112">Olá código concluído está disponível no hello [aplicativo hubs de notificação] [ GitHub] exemplo.</span><span class="sxs-lookup"><span data-stu-id="89b32-112">hello finished code is available in hello [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="89b32-113">Este tutorial demonstra push simples Olá cenário difusão de mensagem com Hubs de notificação.</span><span class="sxs-lookup"><span data-stu-id="89b32-113">This tutorial demonstrates hello simple push message broadcast scenario with Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89b32-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="89b32-114">Prerequisites</span></span>
<span data-ttu-id="89b32-115">Este tutorial requer o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="89b32-115">This tutorial requires hello following:</span></span>

* <span data-ttu-id="89b32-116">[Xcode 6.0][Install Xcode]</span><span class="sxs-lookup"><span data-stu-id="89b32-116">[Xcode 6.0][Install Xcode]</span></span>
* <span data-ttu-id="89b32-117">Um dispositivo compatível com o iOS 7.0 (ou versão posterior)</span><span class="sxs-lookup"><span data-stu-id="89b32-117">An iOS 7.0 (or later version) compatible device</span></span>
* <span data-ttu-id="89b32-118">Associação no Programa de Desenvolvedores de iOS</span><span class="sxs-lookup"><span data-stu-id="89b32-118">iOS Developer Program membership</span></span>
* <span data-ttu-id="89b32-119">[Xamarin Studio]</span><span class="sxs-lookup"><span data-stu-id="89b32-119">[Xamarin Studio]</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="89b32-120">Devido aos requisitos de configuração para notificações de push do iOS, você deve implantar e testar o aplicativo de exemplo hello em um dispositivo físico iOS (iPhone ou iPad) em vez de no simulador Olá.</span><span class="sxs-lookup"><span data-stu-id="89b32-120">Because of configuration requirements for iOS push notifications, you must deploy and test hello sample application on a physical iOS device (iPhone or iPad) instead of in hello simulator.</span></span>
  > 
  > 

<span data-ttu-id="89b32-121">A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais sobre Hubs de Notificação para aplicativos Xamarin iOS.</span><span class="sxs-lookup"><span data-stu-id="89b32-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="89b32-122">Configurar seu Hub de Notificação</span><span class="sxs-lookup"><span data-stu-id="89b32-122">Configure your notification hub</span></span>
<span data-ttu-id="89b32-123">Esta seção orienta você pela criação de um novo hub de notificação e configurar a autenticação com APNS usando Olá **. p12** certificado de push que você criou.</span><span class="sxs-lookup"><span data-stu-id="89b32-123">This section walks you through creating a new notification hub and configuring authentication with APNS using hello **.p12** push certificate that you created.</span></span> <span data-ttu-id="89b32-124">Se você quiser toouse um hub de notificação que você já tiver criado, você poderá ignorar toostep 5.</span><span class="sxs-lookup"><span data-stu-id="89b32-124">If you want toouse a notification hub that you have already created, you can skip toostep 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li>

<p><span data-ttu-id="89b32-125">Como queremos que a conexão de APNS tooconfigure hello, em Olá Portal do Azure, abra as configurações do Hub de notificação, clique ande em <b>Notification Services</b>e, em seguida, clique em Olá <b>Apple (APNS)</b> item na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="89b32-125">As we want tooconfigure hello APNS connection, in hello Azure Portal, open your Notification Hub settings, ande click on <b>Notification Services</b>, and then click hello <b>Apple (APNS)</b> item in hello list.</span></span> <span data-ttu-id="89b32-126">Quando terminar, clique em <b>carregar certificado</b> e selecione hello <b>. p12</b> certificado que você exportou anteriormente, bem como a senha Olá certificado hello.</span><span class="sxs-lookup"><span data-stu-id="89b32-126">Once done, click on <b>Upload Certificate</b> and select hello <b>.p12</b> certificate that you exported earlier, as well as hello password for hello certificate.</span></span></p>

<p><span data-ttu-id="89b32-127">Certifique-se de que tooselect <b>Sandbox</b> modo desde que você está enviando por push as mensagens em um ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="89b32-127">Make sure tooselect <b>Sandbox</b> mode since you will be sending push messages in a development environment.</span></span> <span data-ttu-id="89b32-128">Somente use Olá <b>produção</b> configuração se quiser toosend toousers de notificações de envio que já compraram o aplicativo da loja de saudação.</span><span class="sxs-lookup"><span data-stu-id="89b32-128">Only use hello <b>Production</b> setting if you want toosend push notifications toousers who already purchased your app from hello store.</span></span></p>
</li>
</ol>
<span data-ttu-id="89b32-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span><span class="sxs-lookup"><span data-stu-id="89b32-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span></span>

&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-sandbox.png)

<span data-ttu-id="89b32-130">O hub de notificação agora está configurado toowork com APNS e ter Olá tooregister de cadeias de caracteres de conexão de seu aplicativo e enviar notificações por push.</span><span class="sxs-lookup"><span data-stu-id="89b32-130">Your notification hub is now configured toowork with APNS, and you have hello connection strings tooregister your app and send push notifications.</span></span>

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="89b32-131">Conecte-se o seu hub de notificação do aplicativo toohello</span><span class="sxs-lookup"><span data-stu-id="89b32-131">Connect your app toohello notification hub</span></span>
#### <a name="create-a-new-project"></a><span data-ttu-id="89b32-132">Criar um novo projeto</span><span class="sxs-lookup"><span data-stu-id="89b32-132">Create a new project</span></span>
1. <span data-ttu-id="89b32-133">No Xamarin Studio, crie um novo projeto de iOS e selecione Olá **API unificada** > **único aplicativo de exibição** modelo.</span><span class="sxs-lookup"><span data-stu-id="89b32-133">In Xamarin Studio, create a new iOS project and select hello **Unified API** > **Single View Application** template.</span></span>
   
     ![Xamarin Studio - selecionar o tipo de aplicativo][31]
2. <span data-ttu-id="89b32-135">Adicione um componente de mensagens do Azure de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="89b32-135">Add a reference toohello Azure Messaging component.</span></span> <span data-ttu-id="89b32-136">Em Olá solução exibir, clique com botão direito Olá **componentes** pasta do seu projeto e escolha **obter mais componentes**.</span><span class="sxs-lookup"><span data-stu-id="89b32-136">In hello Solution view, right-click hello **Components** folder for your project and choose **Get More Components**.</span></span> <span data-ttu-id="89b32-137">Pesquise Olá **mensagens do Azure** componente e adicionar Olá componente tooyour projeto.</span><span class="sxs-lookup"><span data-stu-id="89b32-137">Search for hello **Azure Messaging** component and add hello component tooyour project.</span></span>
3. <span data-ttu-id="89b32-138">Em **appdelegate. CS**, adicione o seguinte Olá usando a instrução:</span><span class="sxs-lookup"><span data-stu-id="89b32-138">In **AppDelegate.cs**, add hello following using statement:</span></span>
   
        using WindowsAzure.Messaging;
4. <span data-ttu-id="89b32-139">Declarar uma instância de **SBNotificationHub**:</span><span class="sxs-lookup"><span data-stu-id="89b32-139">Declare an instance of **SBNotificationHub**:</span></span>
   
        private SBNotificationHub Hub { get; set; }
5. <span data-ttu-id="89b32-140">Criar um **Constants.cs** classe com hello variáveis a seguir:</span><span class="sxs-lookup"><span data-stu-id="89b32-140">Create a **Constants.cs** class with hello following variables:</span></span>
   
        // Azure app-specific connection string and hub path
        public const string ConnectionString = "<Azure connection string>";
        public const string NotificationHubPath = "<Azure hub path>";
6. <span data-ttu-id="89b32-141">Em **appdelegate. CS**, atualizar **FinishedLaunching()** toomatch a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="89b32-141">In **AppDelegate.cs**, update **FinishedLaunching()** toomatch hello following:</span></span>
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            if (UIDevice.CurrentDevice.CheckSystemVersion (8, 0)) {
                var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                       UIUserNotificationType.Alert | UIUserNotificationType.Badge | UIUserNotificationType.Sound,
                       new NSSet ());
   
                UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
                UIApplication.SharedApplication.RegisterForRemoteNotifications ();
            } else {
                UIRemoteNotificationType notificationTypes = UIRemoteNotificationType.Alert | UIRemoteNotificationType.Badge | UIRemoteNotificationType.Sound;
                UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (notificationTypes);
            }
   
            return true;
        }
7. <span data-ttu-id="89b32-142">Substituir saudação **RegisteredForRemoteNotifications()** método **appdelegate. CS**:</span><span class="sxs-lookup"><span data-stu-id="89b32-142">Override hello **RegisteredForRemoteNotifications()** method in **AppDelegate.cs**:</span></span>
   
        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            Hub = new SBNotificationHub(Constants.ConnectionString, Constants.NotificationHubPath);
   
            Hub.UnregisterAllAsync (deviceToken, (error) => {
                if (error != null)
                {
                    Console.WriteLine("Error calling Unregister: {0}", error.ToString());
                    return;
                }
   
                NSSet tags = null; // create tags if you want
                Hub.RegisterNativeAsync(deviceToken, tags, (errorCallback) => {
                    if (errorCallback != null)
                        Console.WriteLine("RegisterNativeAsync error: " + errorCallback.ToString());
                });
            });
        }
8. <span data-ttu-id="89b32-143">Substituir saudação **ReceivedRemoteNotification()** método **appdelegate. CS**:</span><span class="sxs-lookup"><span data-stu-id="89b32-143">Override hello **ReceivedRemoteNotification()** method in **AppDelegate.cs**:</span></span>
   
        public override void ReceivedRemoteNotification(UIApplication application, NSDictionary userInfo)
        {
            ProcessNotification(userInfo, false);
        }
9. <span data-ttu-id="89b32-144">Crie seguinte Olá **ProcessNotification()** método **appdelegate. CS**:</span><span class="sxs-lookup"><span data-stu-id="89b32-144">Create hello following **ProcessNotification()** method in **AppDelegate.cs**:</span></span>
   
        void ProcessNotification(NSDictionary options, bool fromFinishedLaunching)
        {
            // Check toosee if hello dictionary has hello aps key.  This is hello notification payload you would have sent
            if (null != options && options.ContainsKey(new NSString("aps")))
            {
                //Get hello aps dictionary
                NSDictionary aps = options.ObjectForKey(new NSString("aps")) as NSDictionary;
   
                string alert = string.Empty;
   
                //Extract hello alert text
                // NOTE: If you're using hello simple alert by just specifying
                // "  aps:{alert:"alert msg here"}  ", this will work fine.
                // But if you're using a complex alert with Localization keys, etc.,
                // your "alert" object from hello aps dictionary will be another NSDictionary.
                // Basically hello JSON gets dumped right into a NSDictionary,
                // so keep that in mind.
                if (aps.ContainsKey(new NSString("alert")))
                    alert = (aps [new NSString("alert")] as NSString).ToString();
   
                //If this came from hello ReceivedRemoteNotification while hello app was running,
                // we of course need toomanually process things like hello sound, badge, and alert.
                if (!fromFinishedLaunching)
                {
                    //Manually show an alert
                    if (!string.IsNullOrEmpty(alert))
                    {
                        UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                        avAlert.Show();
                    }
                }
            }
        }
   
   > [!NOTE]
   > <span data-ttu-id="89b32-145">Você pode escolher toooverride **FailedToRegisterForRemoteNotifications()** toohandle situações como nenhuma conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="89b32-145">You can choose toooverride **FailedToRegisterForRemoteNotifications()** toohandle situations such as no network connection.</span></span> <span data-ttu-id="89b32-146">Isso é especialmente importante onde usuário Olá pode iniciar o aplicativo no modo offline (por exemplo, avião) e desejar push toohandle cenários específicos tooyour aplicativo de mensagens.</span><span class="sxs-lookup"><span data-stu-id="89b32-146">This is especially important where hello user might start your application in offline mode (e.g. Airplane) and you want toohandle push messaging scenarios specific tooyour app.</span></span>
   > 
   > 
10. <span data-ttu-id="89b32-147">Execute o aplicativo hello em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="89b32-147">Run hello app on your device.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="89b32-148">Como enviar notificações por push</span><span class="sxs-lookup"><span data-stu-id="89b32-148">Sending Push Notifications</span></span>
<span data-ttu-id="89b32-149">Você pode testar o recebimento de notificações por push em seu aplicativo pelo envio de notificações em Olá [Portal do Azure] via Olá **teste enviar** recurso Olá **solução de problemas** conjunto de ferramentas, à direita na página de hub de notificação hello, conforme mostrado na saudação de tela abaixo.</span><span class="sxs-lookup"><span data-stu-id="89b32-149">You can test receiving push notifications in your app by sending notifications in hello [Azure Portal] via hello **Test Send** capability in hello **Troubleshooting** toolset, right in hello notification hub page, as shown in hello screen below.</span></span>

![](./media/notification-hubs-ios-get-started/notification-hubs-test-send.png)

<span data-ttu-id="89b32-150">As notificações por push normalmente são enviadas por meio de um serviço de back-end como Serviços Móveis ou ASP.NET usando uma biblioteca compatível.</span><span class="sxs-lookup"><span data-stu-id="89b32-150">Push notifications are normally sent through a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="89b32-151">Você também pode usar o hello API REST diretamente toosend push mensagens se uma biblioteca não está disponível em seu cenário.</span><span class="sxs-lookup"><span data-stu-id="89b32-151">You can also use hello REST API directly toosend push messages if a library is not available in your scenario.</span></span> 

<span data-ttu-id="89b32-152">Neste tutorial, nós manter a simplicidade e demonstrar a testar seu aplicativo de cliente por meio do envio de notificações usando Olá SDK .NET para hubs de notificação em um aplicativo de console, em vez de um serviço de back-end.</span><span class="sxs-lookup"><span data-stu-id="89b32-152">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using hello .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="89b32-153">É recomendável Olá [usar Hubs de notificação toopush notificações toousers](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial como a próxima etapa hello para enviar notificações de um back-end do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="89b32-153">We recommend hello [Use Notification Hubs toopush notifications toousers](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial as hello next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="89b32-154">No entanto, a saudação abordagens a seguir pode ser usada para enviar notificações:</span><span class="sxs-lookup"><span data-stu-id="89b32-154">However, hello following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="89b32-155">**Interface REST**: você pode dar suporte a notificação por push em qualquer plataforma de back-end usando Olá [interface REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="89b32-155">**REST Interface**:  You can support push notification on any backend platform using  hello [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="89b32-156">**SDK .NET de Hubs de notificação do Microsoft Azure**: em Olá Gerenciador de pacotes do Nuget para Visual Studio, execute [Microsoft.Azure.NotificationHubs Install-Package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="89b32-156">**Microsoft Azure Notification Hubs .NET SDK**: In hello Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="89b32-157">**Node.js** : [como toouse Hubs de notificação do Node. js](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="89b32-157">**Node.js** : [How toouse Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>

<span data-ttu-id="89b32-158">**Aplicativos móveis**: para obter um exemplo de como toosend notificações de um back-end aplicativos de celular do serviço de aplicativo do Azure que esteja integrado com Hubs de notificação, consulte [aplicativo móvel de tooyour adicionar de notificações por push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="89b32-158">**Mobile Apps**: For an example of how toosend notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications tooyour mobile app](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>

* <span data-ttu-id="89b32-159">**Java / PHP**: para obter um exemplo de como as notificações por push de toosend usando Olá APIs REST, consulte "como toouse Hubs de notificação do Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="89b32-159">**Java / PHP**: For an example of how toosend push notifications by using hello REST APIs, see "How toouse Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

#### <a name="optional-send-push-notifications-from-a-net-console-app"></a><span data-ttu-id="89b32-160">(Opcional) Enviar notificações por push de um Aplicativo de Console do .NET.</span><span class="sxs-lookup"><span data-stu-id="89b32-160">(Optional) Send Push Notifications from a .NET Console App</span></span>
<span data-ttu-id="89b32-161">Nesta seção, enviaremos as notificações por push usando um aplicativo de console .NET simples</span><span class="sxs-lookup"><span data-stu-id="89b32-161">In this section, we will send push notifications by using a simple .NET console app.</span></span> <span data-ttu-id="89b32-162">Para fins de saudação deste exemplo, nós iremos mudar tooa ambiente de desenvolvimento de Windows que tenha o Visual Studio já instalado.</span><span class="sxs-lookup"><span data-stu-id="89b32-162">For hello purposes of this example, we will switch tooa Windows development environment that has Visual Studio already installed.</span></span>

1. <span data-ttu-id="89b32-163">No Visual Studio, crie um novo aplicativo de console em Visual C#:</span><span class="sxs-lookup"><span data-stu-id="89b32-163">In Visual Studio, create a new Visual C# console application:</span></span>
   
       ![Visual Studio - Create a new console application][213]
2. <span data-ttu-id="89b32-164">No Visual Studio, clique em **Ferramentas**, em **Gerenciador de Pacotes NuGet** e em **Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="89b32-164">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="89b32-165">console do Gerenciador de pacote de saudação deve aparecer encaixada toohello inferior do espaço de trabalho do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="89b32-165">hello package manager console should appear docked toohello bottom of your Visual Studio workspace.</span></span>
3. <span data-ttu-id="89b32-166">Olá janela do Console do Gerenciador de pacotes, definido Olá **projeto padrão** tooyour novo projeto de aplicativo de console e na janela de console hello, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="89b32-166">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="89b32-167">Isso adiciona um toohello Referência SDK de Hubs de notificação do Azure usando Olá <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacote NuGet de Hubs Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="89b32-167">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="89b32-168">Olá abrir `Program.cs` de arquivo e adicione o seguinte Olá `using` instrução, garantindo que podemos usar classes do Azure e funções em sua classe principal:</span><span class="sxs-lookup"><span data-stu-id="89b32-168">Open hello `Program.cs` file and add hello following `using` statement, ensuring that we can use Azure classes and functions within your main class:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="89b32-169">No seu `Program` classe, adicione o seguinte método de saudação (não se esqueça de saudação tooreplace **cadeia de caracteres de conexão** e **nome do hub**):</span><span class="sxs-lookup"><span data-stu-id="89b32-169">In your `Program` class, add hello following method (don't forget tooreplace hello **connection string** and **hub name**):</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var alert = "{\"aps\":{\"alert\":\"Hello from .NET!\"}}";
            await hub.SendAppleNativeNotificationAsync(alert);
        }
6. <span data-ttu-id="89b32-170">Adicionar Olá seguintes linhas no seu `Main` método:</span><span class="sxs-lookup"><span data-stu-id="89b32-170">Add hello following lines in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="89b32-171">Pressione Olá F5 toorun chave Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="89b32-171">Press hello F5 key toorun hello app.</span></span> <span data-ttu-id="89b32-172">Em segundos, você verá uma notificação por push em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="89b32-172">Within seconds, you should see a push notification appear on your device.</span></span> <span data-ttu-id="89b32-173">Se você estiver usando o Wi-Fi ou uma rede de dados de celular, certifique-se de que você tenha uma conexão de internet ativa no dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="89b32-173">Whether you are using Wi-Fi or a cellular data network, make sure that you have an active internet connection on hello device.</span></span>

<span data-ttu-id="89b32-174">Você encontrará todas as cargas de possíveis Olá Olá Apple [Local e o guia de programação de notificação por Push].</span><span class="sxs-lookup"><span data-stu-id="89b32-174">You can find all hello possible payloads in hello Apple [Local and Push Notification Programming Guide].</span></span>

#### <a name="optional-send-notifications-from-a-mobile-service"></a><span data-ttu-id="89b32-175">(Opcional) Enviar Notificações de um Serviço Móvel</span><span class="sxs-lookup"><span data-stu-id="89b32-175">(Optional) Send Notifications from a Mobile Service</span></span>
<span data-ttu-id="89b32-176">Nesta seção, enviaremos notificações por push usando um serviço móvel por meio de um script de nó.</span><span class="sxs-lookup"><span data-stu-id="89b32-176">In this section, we will send push notifications using a mobile service through a node script.</span></span>

<span data-ttu-id="89b32-177">toosend uma notificação por meio de um serviço móvel, siga [Introdução aos serviços móveis]e, em seguida:</span><span class="sxs-lookup"><span data-stu-id="89b32-177">toosend a notification by using a mobile service, follow [Get started with Mobile Services], and then:</span></span>

1. <span data-ttu-id="89b32-178">Entrar toohello [Portal clássico do Azure]e selecione seu serviço móvel.</span><span class="sxs-lookup"><span data-stu-id="89b32-178">Sign in toohello [Azure Classic Portal], and select your mobile service.</span></span>
2. <span data-ttu-id="89b32-179">Selecione Olá **Agendador** guia na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="89b32-179">Select hello **Scheduler** tab on hello top.</span></span>
   
       ![Azure Classic Portal - Scheduler][215]
3. <span data-ttu-id="89b32-180">Crie um novo trabalho agendado, insira um nome e selecione **Sob demanda**.</span><span class="sxs-lookup"><span data-stu-id="89b32-180">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
       ![Azure Classic Portal - Create new job][216]
4. <span data-ttu-id="89b32-181">Quando o trabalho de saudação é criado, clique em nome do trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="89b32-181">When hello job is created, click hello job name.</span></span> <span data-ttu-id="89b32-182">Em seguida, clique em Olá **Script** guia na barra superior hello.</span><span class="sxs-lookup"><span data-stu-id="89b32-182">Then click hello **Script** tab on hello top bar.</span></span>
5. <span data-ttu-id="89b32-183">Inserir saudação script dentro de sua função de agendador a seguir.</span><span class="sxs-lookup"><span data-stu-id="89b32-183">Insert hello following script inside your scheduler function.</span></span> <span data-ttu-id="89b32-184">Verifique se tooreplace reservados Olá seu hub nome e hello conexão cadeia de notificação para *DefaultFullSharedAccessSignature* que você obteve anteriormente.</span><span class="sxs-lookup"><span data-stu-id="89b32-184">Make sure tooreplace hello placeholders with your notification hub name and hello connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="89b32-185">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="89b32-185">Click **Save**.</span></span>
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<Hubname>', '<SAS Full access >');
        notificationHubService.apns.send(
            null,
            {"aps":
                {
                  "alert": "Hello from Mobile Services!"
                }
            },
            function (error)
            {
                if (!error) {
                    console.warn("Notification successful");
                }
            }
        );
6. <span data-ttu-id="89b32-186">Clique em **executar uma vez** na barra inferior de saudação.</span><span class="sxs-lookup"><span data-stu-id="89b32-186">Click **Run Once** on hello bottom bar.</span></span> <span data-ttu-id="89b32-187">Você deverá receber um alerta em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="89b32-187">You should receive an alert on your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89b32-188">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="89b32-188">Next steps</span></span>
<span data-ttu-id="89b32-189">Neste exemplo simples, você transmitida tooall de notificações por push seus dispositivos iOS.</span><span class="sxs-lookup"><span data-stu-id="89b32-189">In this simple example, you broadcasted push notifications tooall your iOS devices.</span></span> <span data-ttu-id="89b32-190">Em ordem tootarget usuários específicos, consulte o tutorial toohello [usar Hubs de notificação toopush notificações toousers].</span><span class="sxs-lookup"><span data-stu-id="89b32-190">In order tootarget specific users, refer toohello tutorial [Use Notification Hubs toopush notifications toousers].</span></span> <span data-ttu-id="89b32-191">Se você desejar toosegment os usuários, grupos de interesse, você pode ler [toosend de Hubs de notificação de uso últimas notícias].</span><span class="sxs-lookup"><span data-stu-id="89b32-191">If you want toosegment your users by interest groups, you can read [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="89b32-192">Saiba mais sobre como Hubs de notificação toouse [orientação de Hubs de notificação] e em Olá [iOS Hubs de notificação como-toofor].</span><span class="sxs-lookup"><span data-stu-id="89b32-192">Learn more about how toouse Notification Hubs in [Notification Hubs Guidance] and in hello [Notification Hubs How-toofor iOS].</span></span>

<!-- Images. -->

[213]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-console-app.png

[215]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler1.png
[216]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler2.png


[31]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-ios-app.png




<!-- URLs. -->
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Introdução aos serviços móveis]: /develop/mobile/tutorials/get-started-xamarin-ios
[Portal clássico do Azure]: https://manage.windowsazure.com/
[orientação de Hubs de notificação]: http://msdn.microsoft.com/library/jj927170.aspx
[iOS Hubs de notificação como-toofor]: http://msdn.microsoft.com/library/jj927168.aspx
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[usar Hubs de notificação toopush notificações toousers]: /manage/services/notification-hubs/notify-users-aspnet
[toosend de Hubs de notificação de uso últimas notícias]: /manage/services/notification-hubs/breaking-news-dotnet

[Local e o guia de programação de notificação por Push]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1
[Apple Push Notification Service]: http://go.microsoft.com/fwlink/p/?LinkId=272584

[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Xamarin Studio]: http://xamarin.com/download
[WindowsAzure.Messaging]: https://github.com/infosupport/WindowsAzure.Messaging.iOS
[Portal do Azure]: https://portal.azure.com
