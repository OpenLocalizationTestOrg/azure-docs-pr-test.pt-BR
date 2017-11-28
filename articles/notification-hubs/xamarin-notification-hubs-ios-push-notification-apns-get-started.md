---
title: "Notificações por push do iOS com Hubs de Notificação para aplicativos Xamarin| Microsoft Docs"
description: "Neste tutorial, você aprende a usar os Hubs de Notificação do Azure para enviar notificações por push a um aplicativo Xamarin iOS."
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
ms.openlocfilehash: 72a81fa0deb34ace77b8fb9b1a4e6b24ee164b35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="ios-push-notifications-with-notification-hubs-for-xamarin-apps"></a><span data-ttu-id="2fc49-104">Notificações por push do iOS com Hubs de Notificação para aplicativos Xamarin</span><span class="sxs-lookup"><span data-stu-id="2fc49-104">iOS Push Notifications with Notification Hubs for Xamarin apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="2fc49-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="2fc49-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2fc49-106">Para concluir este tutorial, você precisa ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="2fc49-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="2fc49-107">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="2fc49-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="2fc49-108">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="2fc49-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="2fc49-109">Este tutorial mostra como usar os Hubs de Notificação do Azure para enviar notificações por push para um aplicativo iOS.</span><span class="sxs-lookup"><span data-stu-id="2fc49-109">This tutorial shows you how to use Azure Notification Hubs to send push notifications to an iOS application.</span></span>
<span data-ttu-id="2fc49-110">Neste tutorial, você cria um aplicativo Xamarin.iOS em branco que recebe notificações por push usando o [Apple Push Notification Service (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span><span class="sxs-lookup"><span data-stu-id="2fc49-110">You'll create a blank Xamarin.iOS app that receives push notifications by using the [Apple Push Notification Service (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span></span> <span data-ttu-id="2fc49-111">Ao finalizar, você poderá usar seu hub de notificação para transmitir notificações por push a todos os dispositivos que executam seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2fc49-111">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span> <span data-ttu-id="2fc49-112">O código concluído está disponível na amostra do [aplicativo NotificationHubs][GitHub].</span><span class="sxs-lookup"><span data-stu-id="2fc49-112">The finished code is available in the [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="2fc49-113">Este tutorial demonstra o cenário de transmissão de mensagens por push simples com Hubs de Notificação.</span><span class="sxs-lookup"><span data-stu-id="2fc49-113">This tutorial demonstrates the simple push message broadcast scenario with Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2fc49-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2fc49-114">Prerequisites</span></span>
<span data-ttu-id="2fc49-115">Este tutorial exige o seguinte:</span><span class="sxs-lookup"><span data-stu-id="2fc49-115">This tutorial requires the following:</span></span>

* <span data-ttu-id="2fc49-116">[Xcode 6.0][Install Xcode]</span><span class="sxs-lookup"><span data-stu-id="2fc49-116">[Xcode 6.0][Install Xcode]</span></span>
* <span data-ttu-id="2fc49-117">Um dispositivo compatível com o iOS 7.0 (ou versão posterior)</span><span class="sxs-lookup"><span data-stu-id="2fc49-117">An iOS 7.0 (or later version) compatible device</span></span>
* <span data-ttu-id="2fc49-118">Associação no Programa de Desenvolvedores de iOS</span><span class="sxs-lookup"><span data-stu-id="2fc49-118">iOS Developer Program membership</span></span>
* <span data-ttu-id="2fc49-119">[Xamarin Studio]</span><span class="sxs-lookup"><span data-stu-id="2fc49-119">[Xamarin Studio]</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="2fc49-120">Devido aos requisitos de configuração das notificações por push do iOS, você deve implantar e testar o aplicativo de exemplo em um dispositivo iOS físico (iPhone ou iPad) em vez do simulador.</span><span class="sxs-lookup"><span data-stu-id="2fc49-120">Because of configuration requirements for iOS push notifications, you must deploy and test the sample application on a physical iOS device (iPhone or iPad) instead of in the simulator.</span></span>
  > 
  > 

<span data-ttu-id="2fc49-121">A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais sobre Hubs de Notificação para aplicativos Xamarin iOS.</span><span class="sxs-lookup"><span data-stu-id="2fc49-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="2fc49-122">Configurar seu Hub de Notificação</span><span class="sxs-lookup"><span data-stu-id="2fc49-122">Configure your notification hub</span></span>
<span data-ttu-id="2fc49-123">Esta seção mostra a criação de um novo hub de notificação e a configuração da autenticação com APNS usando o certificado push **.p12** que você criou.</span><span class="sxs-lookup"><span data-stu-id="2fc49-123">This section walks you through creating a new notification hub and configuring authentication with APNS using the **.p12** push certificate that you created.</span></span> <span data-ttu-id="2fc49-124">Se você quiser usar um hub de notificação já criado, ignore a etapa 5.</span><span class="sxs-lookup"><span data-stu-id="2fc49-124">If you want to use a notification hub that you have already created, you can skip to step 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li>

<p><span data-ttu-id="2fc49-125">Como queremos configurar a conexão APNS, no Portal do Azure, abra as configurações do Hub de Notificação, clique em <b>Serviços de Notificação</b> e clique no item <b>Apple (APNS)</b> na lista.</span><span class="sxs-lookup"><span data-stu-id="2fc49-125">As we want to configure the APNS connection, in the Azure Portal, open your Notification Hub settings, ande click on <b>Notification Services</b>, and then click the <b>Apple (APNS)</b> item in the list.</span></span> <span data-ttu-id="2fc49-126">Quando terminar, clique em <b>Carregar Certificado</b> e selecione o certificado <b>.p12</b> exportado anteriormente, bem como a respectiva senha.</span><span class="sxs-lookup"><span data-stu-id="2fc49-126">Once done, click on <b>Upload Certificate</b> and select the <b>.p12</b> certificate that you exported earlier, as well as the password for the certificate.</span></span></p>

<p><span data-ttu-id="2fc49-127">Selecione o modo <b>Área Restrita</b>, pois você enviará mensagens por push em um ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="2fc49-127">Make sure to select <b>Sandbox</b> mode since you will be sending push messages in a development environment.</span></span> <span data-ttu-id="2fc49-128">Use a configuração <b>Produção</b> apenas se quiser enviar notificações por push aos usuários que já adquiriram seu aplicativo na loja.</span><span class="sxs-lookup"><span data-stu-id="2fc49-128">Only use the <b>Production</b> setting if you want to send push notifications to users who already purchased your app from the store.</span></span></p>
</li>
</ol>
<span data-ttu-id="2fc49-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span><span class="sxs-lookup"><span data-stu-id="2fc49-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span></span>

&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-sandbox.png)

<span data-ttu-id="2fc49-130">Seu hub de notificação agora está configurado para funcionar com o APNS e você tem as cadeias de conexão para registrar seu aplicativo e enviar notificações por push.</span><span class="sxs-lookup"><span data-stu-id="2fc49-130">Your notification hub is now configured to work with APNS, and you have the connection strings to register your app and send push notifications.</span></span>

## <a name="connect-your-app-to-the-notification-hub"></a><span data-ttu-id="2fc49-131">Conectar seu aplicativo ao hub de notificação</span><span class="sxs-lookup"><span data-stu-id="2fc49-131">Connect your app to the notification hub</span></span>
#### <a name="create-a-new-project"></a><span data-ttu-id="2fc49-132">Criar um novo projeto</span><span class="sxs-lookup"><span data-stu-id="2fc49-132">Create a new project</span></span>
1. <span data-ttu-id="2fc49-133">No Xamarin Studio, crie um novo projeto iOS e selecione o modelo **API Unificada** > **Aplicativo de Modo de Exibição Único**.</span><span class="sxs-lookup"><span data-stu-id="2fc49-133">In Xamarin Studio, create a new iOS project and select the **Unified API** > **Single View Application** template.</span></span>
   
     ![Xamarin Studio - selecionar o tipo de aplicativo][31]
2. <span data-ttu-id="2fc49-135">Adicione uma referência ao componentes de Mensagens do Azure.</span><span class="sxs-lookup"><span data-stu-id="2fc49-135">Add a reference to the Azure Messaging component.</span></span> <span data-ttu-id="2fc49-136">No modo de exibição Solução, clique com botão direito do mouse na pasta **Componentes** do seu projeto e escolha **Obter Mais Componentes**.</span><span class="sxs-lookup"><span data-stu-id="2fc49-136">In the Solution view, right-click the **Components** folder for your project and choose **Get More Components**.</span></span> <span data-ttu-id="2fc49-137">Pesquise o componente **Mensagens do Azure** e adicione o componente ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="2fc49-137">Search for the **Azure Messaging** component and add the component to your project.</span></span>
3. <span data-ttu-id="2fc49-138">Em **AppDelegate.cs**, adicione a seguinte instrução using:</span><span class="sxs-lookup"><span data-stu-id="2fc49-138">In **AppDelegate.cs**, add the following using statement:</span></span>
   
        using WindowsAzure.Messaging;
4. <span data-ttu-id="2fc49-139">Declarar uma instância de **SBNotificationHub**:</span><span class="sxs-lookup"><span data-stu-id="2fc49-139">Declare an instance of **SBNotificationHub**:</span></span>
   
        private SBNotificationHub Hub { get; set; }
5. <span data-ttu-id="2fc49-140">Criar uma classe **Constants.cs** com as seguintes variáveis:</span><span class="sxs-lookup"><span data-stu-id="2fc49-140">Create a **Constants.cs** class with the following variables:</span></span>
   
        // Azure app-specific connection string and hub path
        public const string ConnectionString = "<Azure connection string>";
        public const string NotificationHubPath = "<Azure hub path>";
6. <span data-ttu-id="2fc49-141">Em **AppDelegate.cs** atualize **FinishedLaunching()** para que ele corresponda ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="2fc49-141">In **AppDelegate.cs**, update **FinishedLaunching()** to match the following:</span></span>
   
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
7. <span data-ttu-id="2fc49-142">Substituir o método **RegisteredForRemoteNotifications()** em **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="2fc49-142">Override the **RegisteredForRemoteNotifications()** method in **AppDelegate.cs**:</span></span>
   
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
8. <span data-ttu-id="2fc49-143">Substituir o método **ReceivedRemoteNotification()** em **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="2fc49-143">Override the **ReceivedRemoteNotification()** method in **AppDelegate.cs**:</span></span>
   
        public override void ReceivedRemoteNotification(UIApplication application, NSDictionary userInfo)
        {
            ProcessNotification(userInfo, false);
        }
9. <span data-ttu-id="2fc49-144">Criar o seguinte método **ProcessNotification()** em **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="2fc49-144">Create the following **ProcessNotification()** method in **AppDelegate.cs**:</span></span>
   
        void ProcessNotification(NSDictionary options, bool fromFinishedLaunching)
        {
            // Check to see if the dictionary has the aps key.  This is the notification payload you would have sent
            if (null != options && options.ContainsKey(new NSString("aps")))
            {
                //Get the aps dictionary
                NSDictionary aps = options.ObjectForKey(new NSString("aps")) as NSDictionary;
   
                string alert = string.Empty;
   
                //Extract the alert text
                // NOTE: If you're using the simple alert by just specifying
                // "  aps:{alert:"alert msg here"}  ", this will work fine.
                // But if you're using a complex alert with Localization keys, etc.,
                // your "alert" object from the aps dictionary will be another NSDictionary.
                // Basically the JSON gets dumped right into a NSDictionary,
                // so keep that in mind.
                if (aps.ContainsKey(new NSString("alert")))
                    alert = (aps [new NSString("alert")] as NSString).ToString();
   
                //If this came from the ReceivedRemoteNotification while the app was running,
                // we of course need to manually process things like the sound, badge, and alert.
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
   > <span data-ttu-id="2fc49-145">Você pode optar por substituir **FailedToRegisterForRemoteNotifications()** para lidar com situações como a falta de conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="2fc49-145">You can choose to override **FailedToRegisterForRemoteNotifications()** to handle situations such as no network connection.</span></span> <span data-ttu-id="2fc49-146">Isso é particularmente importante quando o usuário pode iniciar o aplicativo no modo offline (por exemplo, Avião) e você deseja manipular cenários de envio de mensagens por push específicos para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2fc49-146">This is especially important where the user might start your application in offline mode (e.g. Airplane) and you want to handle push messaging scenarios specific to your app.</span></span>
   > 
   > 
10. <span data-ttu-id="2fc49-147">Execute o aplicativo em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2fc49-147">Run the app on your device.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="2fc49-148">Como enviar notificações por push</span><span class="sxs-lookup"><span data-stu-id="2fc49-148">Sending Push Notifications</span></span>
<span data-ttu-id="2fc49-149">Você pode testar o recebimento de notificações por push em seu aplicativo enviando notificações pelo [Portal do Azure] por meio do recurso **Testar Enviar** no conjunto de ferramentas **Solução de Problemas**, diretamente na página do hub de notificação, conforme mostrado na tela abaixo.</span><span class="sxs-lookup"><span data-stu-id="2fc49-149">You can test receiving push notifications in your app by sending notifications in the [Azure Portal] via the **Test Send** capability in the **Troubleshooting** toolset, right in the notification hub page, as shown in the screen below.</span></span>

![](./media/notification-hubs-ios-get-started/notification-hubs-test-send.png)

<span data-ttu-id="2fc49-150">As notificações por push normalmente são enviadas por meio de um serviço de back-end como Serviços Móveis ou ASP.NET usando uma biblioteca compatível.</span><span class="sxs-lookup"><span data-stu-id="2fc49-150">Push notifications are normally sent through a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="2fc49-151">Você também poderá usar a API REST diretamente para enviar mensagens por push se uma biblioteca não estiver disponível em seu cenário.</span><span class="sxs-lookup"><span data-stu-id="2fc49-151">You can also use the REST API directly to send push messages if a library is not available in your scenario.</span></span> 

<span data-ttu-id="2fc49-152">Neste tutorial, optamos pela simplicidade e só demonstraremos os testes do aplicativo cliente enviando notificações usando o SDK do .NET para hubs de notificação em um aplicativo de console em vez de um serviço de back-end.</span><span class="sxs-lookup"><span data-stu-id="2fc49-152">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using the .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="2fc49-153">Recomendamos o tutorial [Usar Hubs de Notificação para enviar notificações por push aos usuários](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) como a próxima etapa de envio de notificações de back-end do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2fc49-153">We recommend the [Use Notification Hubs to push notifications to users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial as the next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="2fc49-154">No entanto, as abordagens a seguir podem ser usadas para o envio de notificações:</span><span class="sxs-lookup"><span data-stu-id="2fc49-154">However, the following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="2fc49-155">**Interface REST**: você pode dar suporte à notificação por push em qualquer plataforma de back-end usando a [interface REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="2fc49-155">**REST Interface**:  You can support push notification on any backend platform using  the [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="2fc49-156">**SDK do .NET dos Hubs de Notificações do Microsoft Azure**: no Gerenciador de Pacotes do Nuget para o Visual Studio, execute [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="2fc49-156">**Microsoft Azure Notification Hubs .NET SDK**: In the Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="2fc49-157">**Node.js** : [Como usar os Hubs de Notificação de Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="2fc49-157">**Node.js** : [How to use Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>

<span data-ttu-id="2fc49-158">**Aplicativos móveis**: para obter um exemplo de como enviar notificações de um back-end dos Aplicativos Móveis do Serviço de Aplicativo do Azure que esteja integrado com Hubs de notificação, confira [Adicionar notificação por push para seu aplicativo móvel](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="2fc49-158">**Mobile Apps**: For an example of how to send notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications to your mobile app](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>

* <span data-ttu-id="2fc49-159">**Java/PHP**: para obter um exemplo de como enviar notificações por push usando as APIs REST, confira "Como usar os Hubs de Notificação do Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="2fc49-159">**Java / PHP**: For an example of how to send push notifications by using the REST APIs, see "How to use Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

#### <a name="optional-send-push-notifications-from-a-net-console-app"></a><span data-ttu-id="2fc49-160">(Opcional) Enviar notificações por push de um Aplicativo de Console do .NET.</span><span class="sxs-lookup"><span data-stu-id="2fc49-160">(Optional) Send Push Notifications from a .NET Console App</span></span>
<span data-ttu-id="2fc49-161">Nesta seção, enviaremos as notificações por push usando um aplicativo de console .NET simples</span><span class="sxs-lookup"><span data-stu-id="2fc49-161">In this section, we will send push notifications by using a simple .NET console app.</span></span> <span data-ttu-id="2fc49-162">Para os fins deste exemplo, vamos mudar para um ambiente de desenvolvimento do Windows que tem o Visual Studio já instalada.</span><span class="sxs-lookup"><span data-stu-id="2fc49-162">For the purposes of this example, we will switch to a Windows development environment that has Visual Studio already installed.</span></span>

1. <span data-ttu-id="2fc49-163">No Visual Studio, crie um novo aplicativo de console em Visual C#:</span><span class="sxs-lookup"><span data-stu-id="2fc49-163">In Visual Studio, create a new Visual C# console application:</span></span>
   
       ![Visual Studio - Create a new console application][213]
2. <span data-ttu-id="2fc49-164">No Visual Studio, clique em **Ferramentas**, em **Gerenciador de Pacotes NuGet** e em **Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="2fc49-164">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="2fc49-165">O console do gerenciador de pacotes deve aparecer encaixado na parte inferior de seu espaço de trabalho do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2fc49-165">The package manager console should appear docked to the bottom of your Visual Studio workspace.</span></span>
3. <span data-ttu-id="2fc49-166">Na janela do Console do Gerenciador de Pacotes, defina o **Projeto padrão** como o seu novo projeto de aplicativo do console e execute o seguinte comando na janela do console:</span><span class="sxs-lookup"><span data-stu-id="2fc49-166">In the Package Manager Console window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="2fc49-167">Isso adiciona uma referência ao SDK dos Hubs de Notificação do Azure usando o <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacote NuGet Microsoft.Azure.Notification Hubs</a>.</span><span class="sxs-lookup"><span data-stu-id="2fc49-167">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="2fc49-168">Abra o arquivo `Program.cs` e adicione a seguinte declaração `using`, garantindo que podemos usar classes e funções do Azure em sua classe principal:</span><span class="sxs-lookup"><span data-stu-id="2fc49-168">Open the `Program.cs` file and add the following `using` statement, ensuring that we can use Azure classes and functions within your main class:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="2fc49-169">Na classe `Program`, adicione o seguinte método (não se esqueça de substituir a **cadeia de conexão** e o **nome do hub**):</span><span class="sxs-lookup"><span data-stu-id="2fc49-169">In your `Program` class, add the following method (don't forget to replace the **connection string** and **hub name**):</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var alert = "{\"aps\":{\"alert\":\"Hello from .NET!\"}}";
            await hub.SendAppleNativeNotificationAsync(alert);
        }
6. <span data-ttu-id="2fc49-170">Adicione as seguintes linhas em seu método `Main` :</span><span class="sxs-lookup"><span data-stu-id="2fc49-170">Add the following lines in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="2fc49-171">Pressione a tecla F5 para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2fc49-171">Press the F5 key to run the app.</span></span> <span data-ttu-id="2fc49-172">Em segundos, você verá uma notificação por push em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2fc49-172">Within seconds, you should see a push notification appear on your device.</span></span> <span data-ttu-id="2fc49-173">Se você estiver usando Wi-Fi ou uma rede de dados de celular, verifique se tem uma conexão de Internet ativa no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2fc49-173">Whether you are using Wi-Fi or a cellular data network, make sure that you have an active internet connection on the device.</span></span>

<span data-ttu-id="2fc49-174">Você encontrará todas as cargas possíveis no [Guia de Programação Local e de Notificação por Push]da Apple.</span><span class="sxs-lookup"><span data-stu-id="2fc49-174">You can find all the possible payloads in the Apple [Local and Push Notification Programming Guide].</span></span>

#### <a name="optional-send-notifications-from-a-mobile-service"></a><span data-ttu-id="2fc49-175">(Opcional) Enviar Notificações de um Serviço Móvel</span><span class="sxs-lookup"><span data-stu-id="2fc49-175">(Optional) Send Notifications from a Mobile Service</span></span>
<span data-ttu-id="2fc49-176">Nesta seção, enviaremos notificações por push usando um serviço móvel por meio de um script de nó.</span><span class="sxs-lookup"><span data-stu-id="2fc49-176">In this section, we will send push notifications using a mobile service through a node script.</span></span>

<span data-ttu-id="2fc49-177">Para enviar uma notificação usando um serviço móvel, acompanhe [Introdução aos Serviços Móveis]e:</span><span class="sxs-lookup"><span data-stu-id="2fc49-177">To send a notification by using a mobile service, follow [Get started with Mobile Services], and then:</span></span>

1. <span data-ttu-id="2fc49-178">Entre no [Portal Clássico do Azure]e selecione o serviço móvel.</span><span class="sxs-lookup"><span data-stu-id="2fc49-178">Sign in to the [Azure Classic Portal], and select your mobile service.</span></span>
2. <span data-ttu-id="2fc49-179">Selecione a guia **Agendador** na parte superior.</span><span class="sxs-lookup"><span data-stu-id="2fc49-179">Select the **Scheduler** tab on the top.</span></span>
   
       ![Azure Classic Portal - Scheduler][215]
3. <span data-ttu-id="2fc49-180">Crie um novo trabalho agendado, insira um nome e selecione **Sob demanda**.</span><span class="sxs-lookup"><span data-stu-id="2fc49-180">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
       ![Azure Classic Portal - Create new job][216]
4. <span data-ttu-id="2fc49-181">Quando o trabalho for criado, clique no nome do trabalho.</span><span class="sxs-lookup"><span data-stu-id="2fc49-181">When the job is created, click the job name.</span></span> <span data-ttu-id="2fc49-182">Em seguida, clique na guia **Script** na barra superior.</span><span class="sxs-lookup"><span data-stu-id="2fc49-182">Then click the **Script** tab on the top bar.</span></span>
5. <span data-ttu-id="2fc49-183">Insira o script a seguir em sua função de Agendador.</span><span class="sxs-lookup"><span data-stu-id="2fc49-183">Insert the following script inside your scheduler function.</span></span> <span data-ttu-id="2fc49-184">Certifique-se de substituir os espaços reservados pelo nome de seu hub de notificação e pela cadeia de conexão para a *DefaultFullSharedAccessSignature* que você obteve anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2fc49-184">Make sure to replace the placeholders with your notification hub name and the connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="2fc49-185">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2fc49-185">Click **Save**.</span></span>
   
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
6. <span data-ttu-id="2fc49-186">Clique em **Executar uma vez** na barra inferior.</span><span class="sxs-lookup"><span data-stu-id="2fc49-186">Click **Run Once** on the bottom bar.</span></span> <span data-ttu-id="2fc49-187">Você deverá receber um alerta em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2fc49-187">You should receive an alert on your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2fc49-188">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2fc49-188">Next steps</span></span>
<span data-ttu-id="2fc49-189">Neste exemplo simples, você envia notificações por push para todos os seus dispositivos iOS.</span><span class="sxs-lookup"><span data-stu-id="2fc49-189">In this simple example, you broadcasted push notifications to all your iOS devices.</span></span> <span data-ttu-id="2fc49-190">Para selecionar usuários de destino específicos, consulte o tutorial [Usar Hubs de Notificação para enviar notificações por push aos usuários].</span><span class="sxs-lookup"><span data-stu-id="2fc49-190">In order to target specific users, refer to the tutorial [Use Notification Hubs to push notifications to users].</span></span> <span data-ttu-id="2fc49-191">Se desejar segmentar os usuários por grupos de interesse, você poderá ler [Usar Hubs de Notificação para enviar notícias mais recentes].</span><span class="sxs-lookup"><span data-stu-id="2fc49-191">If you want to segment your users by interest groups, you can read [Use Notification Hubs to send breaking news].</span></span> <span data-ttu-id="2fc49-192">Saiba mais sobre como usar os Hubs de Notificação em [Diretrizes dos Hubs de Notificação] e em [Instruções sobre Hubs de Notificação para iOS].</span><span class="sxs-lookup"><span data-stu-id="2fc49-192">Learn more about how to use Notification Hubs in [Notification Hubs Guidance] and in the [Notification Hubs How-To for iOS].</span></span>

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

<span data-ttu-id="2fc49-193">[Introdução aos Serviços Móveis]: /develop/mobile/tutorials/get-started-xamarin-ios</span><span class="sxs-lookup"><span data-stu-id="2fc49-193">[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-ios</span></span>
<span data-ttu-id="2fc49-194">[Portal Clássico do Azure]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="2fc49-194">[Azure Classic Portal]: https://manage.windowsazure.com/</span></span>
<span data-ttu-id="2fc49-195">[Diretrizes dos Hubs de Notificação]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="2fc49-195">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
<span data-ttu-id="2fc49-196">[Instruções sobre Hubs de Notificação para iOS]: http://msdn.microsoft.com/library/jj927168.aspx</span><span class="sxs-lookup"><span data-stu-id="2fc49-196">[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx</span></span>
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

<span data-ttu-id="2fc49-197">[Usar Hubs de Notificação para enviar notificações por push aos usuários]: /manage/services/notification-hubs/notify-users-aspnet</span><span class="sxs-lookup"><span data-stu-id="2fc49-197">[Use Notification Hubs to push notifications to users]: /manage/services/notification-hubs/notify-users-aspnet</span></span>
<span data-ttu-id="2fc49-198">[Usar Hubs de Notificação para enviar notícias mais recentes]: /manage/services/notification-hubs/breaking-news-dotnet</span><span class="sxs-lookup"><span data-stu-id="2fc49-198">[Use Notification Hubs to send breaking news]: /manage/services/notification-hubs/breaking-news-dotnet</span></span>

<span data-ttu-id="2fc49-199">[Guia de Programação Local e de Notificação por Push]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1</span><span class="sxs-lookup"><span data-stu-id="2fc49-199">[Local and Push Notification Programming Guide]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1</span></span>
[Apple Push Notification Service]: http://go.microsoft.com/fwlink/p/?LinkId=272584

[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
<span data-ttu-id="2fc49-200">[Xamarin Studio]: http://xamarin.com/download</span><span class="sxs-lookup"><span data-stu-id="2fc49-200">[Xamarin Studio]: http://xamarin.com/download</span></span>
[WindowsAzure.Messaging]: https://github.com/infosupport/WindowsAzure.Messaging.iOS
<span data-ttu-id="2fc49-201">[Portal do Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="2fc49-201">[Azure Portal]: https://portal.azure.com</span></span>
