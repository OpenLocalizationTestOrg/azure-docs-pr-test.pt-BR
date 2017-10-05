---
title: "Push Seguro dos Hubs de Notificação do Azure"
description: "Saiba como enviar notificações por push seguro no Azure. Amostras de código escrito em C# usando a API .NET."
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 5aef50f4-80b3-460e-a9a7-7435001273bd
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 9c626ec1534c4899588150a58c0da57b9d963f6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="cf8e2-104">Push Seguro dos Hubs de Notificação do Azure</span><span class="sxs-lookup"><span data-stu-id="cf8e2-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cf8e2-105">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="cf8e2-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="cf8e2-106">iOS</span><span class="sxs-lookup"><span data-stu-id="cf8e2-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="cf8e2-107">Android</span><span class="sxs-lookup"><span data-stu-id="cf8e2-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="cf8e2-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="cf8e2-108">Overview</span></span>
<span data-ttu-id="cf8e2-109">O suporte à notificação por push no Microsoft Azure permite que você acesse uma infraestrutura de envio por push fácil de usar, multiplataforma e expansível que simplifica em muito a implementação de notificações por push para aplicativos de consumidor e empresariais para plataformas móveis.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-109">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="cf8e2-110">Devido a restrições regulatórias ou de segurança, às vezes, um aplicativo pode querer incluir algo na notificação que não pode ser transmitido por meio da infraestrutura de notificação por push padrão.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-110">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span></span> <span data-ttu-id="cf8e2-111">Este tutorial descreve como obter a mesma experiência ao enviar informações confidenciais por meio de uma conexão segura e autenticada entre o dispositivo cliente e o back-end do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-111">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client device and the app backend.</span></span>

<span data-ttu-id="cf8e2-112">Em um nível superior, o fluxo é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="cf8e2-112">At a high level, the flow is as follows:</span></span>

1. <span data-ttu-id="cf8e2-113">O back-end do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="cf8e2-113">The app back-end:</span></span>
   * <span data-ttu-id="cf8e2-114">Armazena uma carga segura no banco de dados de back-end.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="cf8e2-115">Envia a ID dessa notificação ao dispositivo (nenhuma informação segura é enviada).</span><span class="sxs-lookup"><span data-stu-id="cf8e2-115">Sends the ID of this notification to the device (no secure information is sent).</span></span>
2. <span data-ttu-id="cf8e2-116">O dispositivo no aplicativo, ao receber a notificação:</span><span class="sxs-lookup"><span data-stu-id="cf8e2-116">The app on the device, when receiving the notification:</span></span>
   * <span data-ttu-id="cf8e2-117">O dispositivo entra em contato com o back-end solicitando a carga segura.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-117">The device contacts the back-end requesting the secure payload.</span></span>
   * <span data-ttu-id="cf8e2-118">O aplicativo pode mostrar a carga como uma notificação no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-118">The app can show the payload as a notification on the device.</span></span>

<span data-ttu-id="cf8e2-119">É importante observar que no fluxo anterior (e neste tutorial), pressupomos que o dispositivo armazena um token de autenticação no armazenamento local depois que o usuário faz logon.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-119">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span></span> <span data-ttu-id="cf8e2-120">Isso garante uma experiência perfeita  já que o dispositivo pode recuperar a carga de segurança da notificação usando este token.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-120">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span></span> <span data-ttu-id="cf8e2-121">Se o seu aplicativo não armazenar tokens de autenticação no dispositivo, ou se esses tokens puderem expirar, o aplicativo do dispositivo, após receber a notificação, deve exibir uma notificação genérica solicitando que o usuário inicie o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-121">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the notification should display a generic notification prompting the user to launch the app.</span></span> <span data-ttu-id="cf8e2-122">Dessa forma, o aplicativo autentica o usuário e mostra a carga de notificação.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-122">The app then authenticates the user and shows the notification payload.</span></span>

<span data-ttu-id="cf8e2-123">Este tutorial de Push Seguro mostra como enviar uma notificação por push de maneira segura.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-123">This Secure Push tutorial shows how to send a push notification securely.</span></span> <span data-ttu-id="cf8e2-124">O tutorial baseia-se no tutorial [Notificação de usuários](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) , por isso, você deve concluir as etapas nesse tutorial primeiro.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-124">The tutorial builds on the [Notify Users](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial, so you should complete the steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="cf8e2-125">Este tutorial presume que você criou e configurou seu hub de notificação conforme descrito em [Introdução aos Hubs de Notificação (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span><span class="sxs-lookup"><span data-stu-id="cf8e2-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span></span>
> <span data-ttu-id="cf8e2-126">Além disso, observe que o Windows Phone 8.1 requer credenciais do Windows (não Windows Phone) e tarefas em segundo plano não funcionam no Windows Phone 8.0 ou Silverlight 8.1.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-126">Also, note that Windows Phone 8.1 requires Windows (not Windows Phone) credentials, and that background tasks do not work on Windows Phone 8.0 or Silverlight 8.1.</span></span> <span data-ttu-id="cf8e2-127">Para aplicativos da Windows Store, você pode receber notificações por meio de uma tarefa de segundo plano somente se o aplicativo estiver com o bloqueio de tela habilitado (clique na caixa de seleção em Appmanifest).</span><span class="sxs-lookup"><span data-stu-id="cf8e2-127">For Windows Store applications, you can receive notifications via a background task only if the app is lock-screen enabled (click the checkbox in the Appmanifest).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-the-windows-phone-project"></a><span data-ttu-id="cf8e2-128">Modificar o projeto do Windows Phone</span><span class="sxs-lookup"><span data-stu-id="cf8e2-128">Modify the Windows Phone Project</span></span>
1. <span data-ttu-id="cf8e2-129">No projeto **NotifyUserWindowsPhone** , adicione o código a seguir em App.xaml.cs para registrar a tarefa de segundo plano de push.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-129">In the **NotifyUserWindowsPhone** project, add the following code to App.xaml.cs to register the push background task.</span></span> <span data-ttu-id="cf8e2-130">Adicione a seguinte linha de código ao final do método `OnLaunched()` :</span><span class="sxs-lookup"><span data-stu-id="cf8e2-130">Add the following line of code at the end of the `OnLaunched()` method:</span></span>
   
        RegisterBackgroundTask();
2. <span data-ttu-id="cf8e2-131">Ainda no App.xaml.cs, adicione o código a abaixo imediatamente após o método `OnLaunched()` :</span><span class="sxs-lookup"><span data-stu-id="cf8e2-131">Still in App.xaml.cs, add the following code immediately after the `OnLaunched()` method:</span></span>
   
        private async void RegisterBackgroundTask()
        {
            if (!Windows.ApplicationModel.Background.BackgroundTaskRegistration.AllTasks.Any(i => i.Value.Name == "PushBackgroundTask"))
            {
                var result = await BackgroundExecutionManager.RequestAccessAsync();
                var builder = new BackgroundTaskBuilder();
   
                builder.Name = "PushBackgroundTask";
                builder.TaskEntryPoint = typeof(PushBackgroundComponent.PushBackgroundTask).FullName;
                builder.SetTrigger(new Windows.ApplicationModel.Background.PushNotificationTrigger());
                BackgroundTaskRegistration task = builder.Register();
            }
        }
3. <span data-ttu-id="cf8e2-132">Adicione as seguintes instruções `using` na parte superior do arquivo App.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="cf8e2-132">Add the following `using` statements at the top of the App.xaml.cs file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Windows.ApplicationModel.Background;
4. <span data-ttu-id="cf8e2-133">No menu **Arquivo** no Visual Studio, clique em **Salvar Tudo**.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-133">From the **File** menu in Visual Studio, click **Save All**.</span></span>

## <a name="create-the-push-background-component"></a><span data-ttu-id="cf8e2-134">Criar o componente de segundo plano de push</span><span class="sxs-lookup"><span data-stu-id="cf8e2-134">Create the Push Background Component</span></span>
<span data-ttu-id="cf8e2-135">A próxima etapa é criar o componente de segundo plano de push.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-135">The next step is to create the push background component.</span></span>

1. <span data-ttu-id="cf8e2-136">No Gerenciador de Soluções, clique com o botão direito do mouse no nó do nível superior da solução (**Solução SecurePush** nesse caso) e clique em **Adicionar** e em **Novo Projeto**.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-136">In Solution Explorer, right-click the top-level node of the solution (**Solution SecurePush** in this case), then click **Add**, then click **New Project**.</span></span>
2. <span data-ttu-id="cf8e2-137">Expanda **Aplicativos da Loja** e clique em **Aplicativos do Windows Phone** e em **Componente do Tempo de Execução do Windows (Windows Phone)**.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-137">Expand **Store Apps**, then click **Windows Phone Apps**, then click **Windows Runtime Component (Windows Phone)**.</span></span> <span data-ttu-id="cf8e2-138">Nomeie o projeto **PushBackgroundComponent** e clique em **OK** para criar o projeto.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-138">Name the project **PushBackgroundComponent**, and then click **OK** to create the project.</span></span>
   
    ![][12]
3. <span data-ttu-id="cf8e2-139">No Gerenciador de Soluções, clique com o botão direito do mouse no projeto **PushBackgroundComponent (Windows Phone 8.1)** e clique em **Adicionar** e em **Classe**.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-139">In Solution Explorer, right-click the **PushBackgroundComponent (Windows Phone 8.1)** project, then click **Add**, then click **Class**.</span></span> <span data-ttu-id="cf8e2-140">Nomeie a nova classe como **PushBackgroundTask.cs**.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-140">Name the new class **PushBackgroundTask.cs**.</span></span> <span data-ttu-id="cf8e2-141">Clique em **Adicionar** para gerar a classe.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-141">Click **Add** to generate the class.</span></span>
4. <span data-ttu-id="cf8e2-142">Substitua todo o conteúdo da definição do namespace **PushBackgroundComponent** pelo código a seguir, substituindo o espaço reservado `{back-end endpoint}` pelo ponto de extremidade do back-end obtido ao implantar o back-end:</span><span class="sxs-lookup"><span data-stu-id="cf8e2-142">Replace the entire contents of the **PushBackgroundComponent** namespace definition with the following code, substituting the placeholder `{back-end endpoint}` with the back-end endpoint obtained while deploying your back-end:</span></span>
   
        public sealed class Notification
            {
                public int Id { get; set; }
                public string Payload { get; set; }
                public bool Read { get; set; }
            }
   
            public sealed class PushBackgroundTask : IBackgroundTask
            {
                private string GET_URL = "{back-end endpoint}/api/notifications/";
   
                async void IBackgroundTask.Run(IBackgroundTaskInstance taskInstance)
                {
                    // Store the content received from the notification so it can be retrieved from the UI.
                    RawNotification raw = (RawNotification)taskInstance.TriggerDetails;
                    var notificationId = raw.Content;
   
                    // retrieve content
                    BackgroundTaskDeferral deferral = taskInstance.GetDeferral();
                    var httpClient = new HttpClient();
                    var settings = ApplicationData.Current.LocalSettings.Values;
                    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                    var notificationString = await httpClient.GetStringAsync(GET_URL + notificationId);
   
                    var notification = JsonConvert.DeserializeObject<Notification>(notificationString);
   
                    ShowToast(notification);
   
                    deferral.Complete();
                }
   
                private void ShowToast(Notification notification)
                {
                    ToastTemplateType toastTemplate = ToastTemplateType.ToastText01;
                    XmlDocument toastXml = ToastNotificationManager.GetTemplateContent(toastTemplate);
                    XmlNodeList toastTextElements = toastXml.GetElementsByTagName("text");
                    toastTextElements[0].AppendChild(toastXml.CreateTextNode(notification.Payload));
                    ToastNotification toast = new ToastNotification(toastXml);
                    ToastNotificationManager.CreateToastNotifier().Show(toast);
                }
            }
5. <span data-ttu-id="cf8e2-143">No Gerenciador de Soluções, clique com o botão direito do mouse no projeto **PushBackgroundComponent (Windows Phone 8.1)** e em **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-143">In Solution Explorer, right-click the **PushBackgroundComponent (Windows Phone 8.1)** project and then click **Manage NuGet Packages**.</span></span>
6. <span data-ttu-id="cf8e2-144">No lado esquerdo, clique em **Online**.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-144">On the left-hand side, click **Online**.</span></span>
7. <span data-ttu-id="cf8e2-145">Na caixa **Pesquisar**, digite **Http Client**.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-145">In the **Search** box, type **Http Client**.</span></span>
8. <span data-ttu-id="cf8e2-146">Na lista de resultados, clique em **Bibliotecas de Cliente HTTP da Microsoft** e em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-146">In the results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="cf8e2-147">Conclua a instalação.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-147">Complete the installation.</span></span>
9. <span data-ttu-id="cf8e2-148">De volta à caixa **Pesquisar** do NuGet, digite **Json.net**.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-148">Back in the NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="cf8e2-149">Instale o pacote **Json.NET** e feche a janela do Gerenciador de Pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-149">Install the **Json.NET** package, then close the NuGet Package Manager window.</span></span>
10. <span data-ttu-id="cf8e2-150">Adicione as seguintes instruções `using` na parte superior do arquivo **PushBackgroundTask.cs** :</span><span class="sxs-lookup"><span data-stu-id="cf8e2-150">Add the following `using` statements at the top of the **PushBackgroundTask.cs** file:</span></span>
    
        using Windows.ApplicationModel.Background;
        using Windows.Networking.PushNotifications;
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Newtonsoft.Json;
        using Windows.UI.Notifications;
        using Windows.Data.Xml.Dom;
11. <span data-ttu-id="cf8e2-151">No Gerenciador de Soluções, no projeto **NotifyUserWindowsPhone (Windows Phone 8.1)**, clique com o botão direito do mouse em **Referências** e em **Adicionar Referência...**.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-151">In Solution Explorer, in the **NotifyUserWindowsPhone (Windows Phone 8.1)** project, right-click **References**, then click **Add Reference...**.</span></span> <span data-ttu-id="cf8e2-152">Na caixa de diálogo Gerenciador de Referências, marque a caixa próxima a **PushBackgroundComponent** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-152">In the Reference Manager dialog, check the box next to **PushBackgroundComponent**, and then click **OK**.</span></span>
12. <span data-ttu-id="cf8e2-153">No Gerenciador de Soluções, clique duas vezes em **Package.appxmanifest** no projeto **NotifyUserWindowsPhone (Windows Phone 8.1)**.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-153">In Solution Explorer, double-click **Package.appxmanifest** in the **NotifyUserWindowsPhone (Windows Phone 8.1)** project.</span></span> <span data-ttu-id="cf8e2-154">Em **Notificações**, defina **Compatível com Toast** como **Sim**.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-154">Under **Notifications**, set **Toast Capable** to **Yes**.</span></span>
    
    ![][3]
13. <span data-ttu-id="cf8e2-155">Ainda em **Package.appxmanifest**, clique no menu **Declarações** próximo à parte superior.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-155">Still in **Package.appxmanifest**, click the **Declarations** menu near the top.</span></span> <span data-ttu-id="cf8e2-156">Na lista suspensa **Declarações Disponíveis**, clique em **Tarefas de Segundo Plano** e em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-156">In the **Available Declarations** dropdown, click **Background Tasks**, and then click **Add**.</span></span>
14. <span data-ttu-id="cf8e2-157">Em **Package.appxmanifest**, em **Propriedades**, marque **Notificação por push**.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-157">In **Package.appxmanifest**, under **Properties**, check **Push notification**.</span></span>
15. <span data-ttu-id="cf8e2-158">Em **Package.appxmanifest**, em **Configurações do Aplicativo**, digite **PushBackgroundComponent.PushBackgroundTask** no campo **Ponto de Entrada**.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-158">In **Package.appxmanifest**, under **App Settings**, type **PushBackgroundComponent.PushBackgroundTask** in the **Entry Point** field.</span></span>
    
    ![][13]
16. <span data-ttu-id="cf8e2-159">No menu **Arquivo**, clique em **Salvar Tudo**.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-159">From the **File** menu, click **Save All**.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="cf8e2-160">Executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="cf8e2-160">Run the Application</span></span>
<span data-ttu-id="cf8e2-161">Para executar o aplicativo, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="cf8e2-161">To run the application, do the following:</span></span>

1. <span data-ttu-id="cf8e2-162">No Visual Studio, execute o aplicativo da API Web **AppBackend** .</span><span class="sxs-lookup"><span data-stu-id="cf8e2-162">In Visual Studio, run the **AppBackend** Web API application.</span></span> <span data-ttu-id="cf8e2-163">Uma página da Web do ASP.NET é exibida.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-163">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="cf8e2-164">No Visual Studio, execute o aplicativo do Windows Phone **NotifyUserWindowsPhone (Windows Phone 8.1)** .</span><span class="sxs-lookup"><span data-stu-id="cf8e2-164">In Visual Studio, run the **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone app.</span></span> <span data-ttu-id="cf8e2-165">O emulador do Windows Phone executa e carrega o aplicativo automaticamente.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-165">The Windows Phone emulator runs and loads the app automatically.</span></span>
3. <span data-ttu-id="cf8e2-166">Na interface do usuário do aplicativo **NotifyUserWindowsPhone** , insira um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-166">In the **NotifyUserWindowsPhone** app UI, enter a username and password.</span></span> <span data-ttu-id="cf8e2-167">Pode ser qualquer cadeia de caracteres, mas elas devem ter o mesmo valor.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-167">These can be any string, but they must be the same value.</span></span>
4. <span data-ttu-id="cf8e2-168">Na interface do usuário do aplicativo **NotifyUserWindowsPhone**, clique em **Fazer logon e registrar-se**.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-168">In the **NotifyUserWindowsPhone** app UI, click **Log in and register**.</span></span> <span data-ttu-id="cf8e2-169">Em seguida, clique em **Enviar push**.</span><span class="sxs-lookup"><span data-stu-id="cf8e2-169">Then click **Send push**.</span></span>

[3]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push3.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push13.png
