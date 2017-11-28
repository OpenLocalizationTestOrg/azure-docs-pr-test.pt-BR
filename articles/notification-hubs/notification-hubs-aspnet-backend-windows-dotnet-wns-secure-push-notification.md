---
title: "aaaAzure notificação Hubs seguro Push"
description: "Saiba como toosend segura notificações por push no Azure. Exemplos de código escritos em c# usando Olá API .NET."
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
ms.openlocfilehash: b6fe16c96d28d75ff698278409fb012472ba6396
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="f0598-104">Push Seguro dos Hubs de Notificação do Azure</span><span class="sxs-lookup"><span data-stu-id="f0598-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f0598-105">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="f0598-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="f0598-106">iOS</span><span class="sxs-lookup"><span data-stu-id="f0598-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="f0598-107">Android</span><span class="sxs-lookup"><span data-stu-id="f0598-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="f0598-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="f0598-108">Overview</span></span>
<span data-ttu-id="f0598-109">Suporte de notificação por push no Microsoft Azure permite que você tooaccess uma infraestrutura de push de fácil de usar, multiplataforma, dimensionável, que simplifica bastante a implementação de saudação de notificações por push para aplicativos de consumidor e empresariais para dispositivos móveis plataformas.</span><span class="sxs-lookup"><span data-stu-id="f0598-109">Push notification support in Microsoft Azure enables you tooaccess an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="f0598-110">Devido a restrições de segurança ou tooregulatory, às vezes, um aplicativo pode ser conveniente tooinclude algo na notificação de saudação que não pode ser transmitida por meio da infraestrutura de notificação por push padrão hello.</span><span class="sxs-lookup"><span data-stu-id="f0598-110">Due tooregulatory or security constraints, sometimes an application might want tooinclude something in hello notification that cannot be transmitted through hello standard push notification infrastructure.</span></span> <span data-ttu-id="f0598-111">Este tutorial descreve como tooachieve Olá a mesma experiência, enviando informações confidenciais por meio de uma conexão segura e autenticada entre o dispositivo de cliente hello e back-end de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="f0598-111">This tutorial describes how tooachieve hello same experience by sending sensitive information through a secure, authenticated connection between hello client device and hello app backend.</span></span>

<span data-ttu-id="f0598-112">Em um nível alto, o fluxo de saudação é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f0598-112">At a high level, hello flow is as follows:</span></span>

1. <span data-ttu-id="f0598-113">Olá aplicativo back-end:</span><span class="sxs-lookup"><span data-stu-id="f0598-113">hello app back-end:</span></span>
   * <span data-ttu-id="f0598-114">Armazena uma carga segura no banco de dados de back-end.</span><span class="sxs-lookup"><span data-stu-id="f0598-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="f0598-115">Envia a ID de saudação do dispositivo toohello notificação (nenhuma informação de segurança é enviada).</span><span class="sxs-lookup"><span data-stu-id="f0598-115">Sends hello ID of this notification toohello device (no secure information is sent).</span></span>
2. <span data-ttu-id="f0598-116">Olá o aplicativo no dispositivo hello, ao receber a notificação de saudação:</span><span class="sxs-lookup"><span data-stu-id="f0598-116">hello app on hello device, when receiving hello notification:</span></span>
   * <span data-ttu-id="f0598-117">dispositivo Olá contata Olá back-end solicitante Olá carga de segurança.</span><span class="sxs-lookup"><span data-stu-id="f0598-117">hello device contacts hello back-end requesting hello secure payload.</span></span>
   * <span data-ttu-id="f0598-118">aplicativo Hello pode mostrar carga hello como uma notificação no dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0598-118">hello app can show hello payload as a notification on hello device.</span></span>

<span data-ttu-id="f0598-119">É importante toonote em Olá anterior fluxo (e, neste tutorial), vamos supor que o dispositivo Olá armazena um token de autenticação no armazenamento local, depois Olá usuário fizer logon.</span><span class="sxs-lookup"><span data-stu-id="f0598-119">It is important toonote that in hello preceding flow (and in this tutorial), we assume that hello device stores an authentication token in local storage, after hello user logs in.</span></span> <span data-ttu-id="f0598-120">Isso garante uma experiência completamente, como dispositivo Olá pode recuperar a carga de segurança da notificação hello usando este token.</span><span class="sxs-lookup"><span data-stu-id="f0598-120">This guarantees a completely seamless experience, as hello device can retrieve hello notification’s secure payload using this token.</span></span> <span data-ttu-id="f0598-121">Se seu aplicativo não armazenar os tokens de autenticação no dispositivo hello, ou se esses tokens podem ser expirados, hello aplicativo de dispositivo, ao receber a notificação de saudação deve exibir uma notificação genérica solicitando Olá usuário toolaunch Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f0598-121">If your application does not store authentication tokens on hello device, or if these tokens can be expired, hello device app, upon receiving hello notification should display a generic notification prompting hello user toolaunch hello app.</span></span> <span data-ttu-id="f0598-122">aplicativo Hello, em seguida, autentica o usuário hello e mostra a carga de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0598-122">hello app then authenticates hello user and shows hello notification payload.</span></span>

<span data-ttu-id="f0598-123">Este tutorial seguro Push mostra como toosend uma notificação por push com segurança.</span><span class="sxs-lookup"><span data-stu-id="f0598-123">This Secure Push tutorial shows how toosend a push notification securely.</span></span> <span data-ttu-id="f0598-124">Olá tutorial baseia-se em Olá [notificar usuários](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial, portanto você deve concluir as etapas de saudação neste tutorial primeiro.</span><span class="sxs-lookup"><span data-stu-id="f0598-124">hello tutorial builds on hello [Notify Users](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial, so you should complete hello steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="f0598-125">Este tutorial presume que você criou e configurou seu hub de notificação conforme descrito em [Introdução aos Hubs de Notificação (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span><span class="sxs-lookup"><span data-stu-id="f0598-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span></span>
> <span data-ttu-id="f0598-126">Além disso, observe que o Windows Phone 8.1 requer credenciais do Windows (não Windows Phone) e tarefas em segundo plano não funcionam no Windows Phone 8.0 ou Silverlight 8.1.</span><span class="sxs-lookup"><span data-stu-id="f0598-126">Also, note that Windows Phone 8.1 requires Windows (not Windows Phone) credentials, and that background tasks do not work on Windows Phone 8.0 or Silverlight 8.1.</span></span> <span data-ttu-id="f0598-127">Para aplicativos da Windows Store, você pode receber notificações por meio de uma tarefa em segundo plano apenas se o aplicativo hello está habilitada na tela de bloqueio (clique na caixa de seleção Olá Olá Appmanifest).</span><span class="sxs-lookup"><span data-stu-id="f0598-127">For Windows Store applications, you can receive notifications via a background task only if hello app is lock-screen enabled (click hello checkbox in hello Appmanifest).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-windows-phone-project"></a><span data-ttu-id="f0598-128">Modificar Olá projeto do Windows Phone</span><span class="sxs-lookup"><span data-stu-id="f0598-128">Modify hello Windows Phone Project</span></span>
1. <span data-ttu-id="f0598-129">Em Olá **NotifyUserWindowsPhone** de projeto, adicione Olá tarefa em segundo plano por push de saudação do código tooApp.xaml.cs tooregister a seguir.</span><span class="sxs-lookup"><span data-stu-id="f0598-129">In hello **NotifyUserWindowsPhone** project, add hello following code tooApp.xaml.cs tooregister hello push background task.</span></span> <span data-ttu-id="f0598-130">Adicionar Olá a seguinte linha de código final Olá Olá `OnLaunched()` método:</span><span class="sxs-lookup"><span data-stu-id="f0598-130">Add hello following line of code at hello end of hello `OnLaunched()` method:</span></span>
   
        RegisterBackgroundTask();
2. <span data-ttu-id="f0598-131">Ainda em App.xaml.cs, adicionar Olá código a seguir imediatamente após Olá `OnLaunched()` método:</span><span class="sxs-lookup"><span data-stu-id="f0598-131">Still in App.xaml.cs, add hello following code immediately after hello `OnLaunched()` method:</span></span>
   
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
3. <span data-ttu-id="f0598-132">Adicione o seguinte Olá `using` instruções no topo de saudação do arquivo App.xaml.cs-Olá:</span><span class="sxs-lookup"><span data-stu-id="f0598-132">Add hello following `using` statements at hello top of hello App.xaml.cs file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Windows.ApplicationModel.Background;
4. <span data-ttu-id="f0598-133">De saudação **arquivo** no Visual Studio, clique em **Salvar tudo**.</span><span class="sxs-lookup"><span data-stu-id="f0598-133">From hello **File** menu in Visual Studio, click **Save All**.</span></span>

## <a name="create-hello-push-background-component"></a><span data-ttu-id="f0598-134">Criar hello Push componente do plano de fundo</span><span class="sxs-lookup"><span data-stu-id="f0598-134">Create hello Push Background Component</span></span>
<span data-ttu-id="f0598-135">Olá próxima etapa é o componente de plano de fundo toocreate Olá por push.</span><span class="sxs-lookup"><span data-stu-id="f0598-135">hello next step is toocreate hello push background component.</span></span>

1. <span data-ttu-id="f0598-136">No Gerenciador de soluções, clique com botão direito nó de nível superior de saudação de solução de saudação (**solução SecurePush** nesse caso), em seguida, clique em **adicionar**, em seguida, clique em **novo projeto**.</span><span class="sxs-lookup"><span data-stu-id="f0598-136">In Solution Explorer, right-click hello top-level node of hello solution (**Solution SecurePush** in this case), then click **Add**, then click **New Project**.</span></span>
2. <span data-ttu-id="f0598-137">Expanda **Aplicativos da Loja** e clique em **Aplicativos do Windows Phone** e em **Componente do Tempo de Execução do Windows (Windows Phone)**.</span><span class="sxs-lookup"><span data-stu-id="f0598-137">Expand **Store Apps**, then click **Windows Phone Apps**, then click **Windows Runtime Component (Windows Phone)**.</span></span> <span data-ttu-id="f0598-138">Projeto de saudação do nome **PushBackgroundComponent**e, em seguida, clique em **Okey** toocreate projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0598-138">Name hello project **PushBackgroundComponent**, and then click **OK** toocreate hello project.</span></span>
   
    ![][12]
3. <span data-ttu-id="f0598-139">No Gerenciador de soluções, clique com botão direito Olá **PushBackgroundComponent (Windows Phone 8.1)** projeto e, em seguida, clique em **adicionar**, em seguida, clique em **classe**.</span><span class="sxs-lookup"><span data-stu-id="f0598-139">In Solution Explorer, right-click hello **PushBackgroundComponent (Windows Phone 8.1)** project, then click **Add**, then click **Class**.</span></span> <span data-ttu-id="f0598-140">Nomeie a nova classe de saudação **PushBackgroundTask.cs**.</span><span class="sxs-lookup"><span data-stu-id="f0598-140">Name hello new class **PushBackgroundTask.cs**.</span></span> <span data-ttu-id="f0598-141">Clique em **adicionar** toogenerate classe de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0598-141">Click **Add** toogenerate hello class.</span></span>
4. <span data-ttu-id="f0598-142">Substitua todo o conteúdo do Olá Olá **PushBackgroundComponent** definição de namespace com hello código a seguir, substituindo o espaço reservado de saudação `{back-end endpoint}` com ponto de extremidade do back-end Olá obtido ao implantar o back-end:</span><span class="sxs-lookup"><span data-stu-id="f0598-142">Replace hello entire contents of hello **PushBackgroundComponent** namespace definition with hello following code, substituting hello placeholder `{back-end endpoint}` with hello back-end endpoint obtained while deploying your back-end:</span></span>
   
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
                    // Store hello content received from hello notification so it can be retrieved from hello UI.
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
5. <span data-ttu-id="f0598-143">No Gerenciador de soluções, clique com botão direito Olá **PushBackgroundComponent (Windows Phone 8.1)** do projeto e, em seguida, clique em **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f0598-143">In Solution Explorer, right-click hello **PushBackgroundComponent (Windows Phone 8.1)** project and then click **Manage NuGet Packages**.</span></span>
6. <span data-ttu-id="f0598-144">No lado esquerdo do hello, clique em **Online**.</span><span class="sxs-lookup"><span data-stu-id="f0598-144">On hello left-hand side, click **Online**.</span></span>
7. <span data-ttu-id="f0598-145">Em Olá **pesquisa** , digite **cliente Http**.</span><span class="sxs-lookup"><span data-stu-id="f0598-145">In hello **Search** box, type **Http Client**.</span></span>
8. <span data-ttu-id="f0598-146">Na lista de resultados de saudação, clique em **bibliotecas de cliente HTTP Microsoft**e, em seguida, clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="f0598-146">In hello results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="f0598-147">Concluir a instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0598-147">Complete hello installation.</span></span>
9. <span data-ttu-id="f0598-148">Em Olá NuGet **pesquisa** , digite **Json.net**.</span><span class="sxs-lookup"><span data-stu-id="f0598-148">Back in hello NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="f0598-149">Instalar Olá **Json.NET** pacote e a janela do Gerenciador de pacotes do NuGet Olá fechar.</span><span class="sxs-lookup"><span data-stu-id="f0598-149">Install hello **Json.NET** package, then close hello NuGet Package Manager window.</span></span>
10. <span data-ttu-id="f0598-150">Adicione o seguinte Olá `using` instruções na parte superior de saudação do hello **PushBackgroundTask.cs** arquivo:</span><span class="sxs-lookup"><span data-stu-id="f0598-150">Add hello following `using` statements at hello top of hello **PushBackgroundTask.cs** file:</span></span>
    
        using Windows.ApplicationModel.Background;
        using Windows.Networking.PushNotifications;
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Newtonsoft.Json;
        using Windows.UI.Notifications;
        using Windows.Data.Xml.Dom;
11. <span data-ttu-id="f0598-151">No Solution Explorer, no hello **NotifyUserWindowsPhone (Windows Phone 8.1)** de projeto, clique no **referências**, em seguida, clique em **adicionar referência...** . Na caixa de diálogo de Gerenciador de referências hello, caixa de seleção Olá Avançar muito**PushBackgroundComponent**e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="f0598-151">In Solution Explorer, in hello **NotifyUserWindowsPhone (Windows Phone 8.1)** project, right-click **References**, then click **Add Reference...**. In hello Reference Manager dialog, check hello box next too**PushBackgroundComponent**, and then click **OK**.</span></span>
12. <span data-ttu-id="f0598-152">No Solution Explorer, clique duas vezes em **Package. appxmanifest** em Olá **NotifyUserWindowsPhone (Windows Phone 8.1)** projeto.</span><span class="sxs-lookup"><span data-stu-id="f0598-152">In Solution Explorer, double-click **Package.appxmanifest** in hello **NotifyUserWindowsPhone (Windows Phone 8.1)** project.</span></span> <span data-ttu-id="f0598-153">Em **notificações**, defina **compatíveis com notificação do sistema** muito**Sim**.</span><span class="sxs-lookup"><span data-stu-id="f0598-153">Under **Notifications**, set **Toast Capable** too**Yes**.</span></span>
    
    ![][3]
13. <span data-ttu-id="f0598-154">Ainda no **Package. appxmanifest**, clique em Olá **declarações** menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="f0598-154">Still in **Package.appxmanifest**, click hello **Declarations** menu near hello top.</span></span> <span data-ttu-id="f0598-155">Em Olá **Available Declarations** lista suspensa, clique em **tarefas em segundo plano**e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f0598-155">In hello **Available Declarations** dropdown, click **Background Tasks**, and then click **Add**.</span></span>
14. <span data-ttu-id="f0598-156">Em **Package.appxmanifest**, em **Propriedades**, marque **Notificação por push**.</span><span class="sxs-lookup"><span data-stu-id="f0598-156">In **Package.appxmanifest**, under **Properties**, check **Push notification**.</span></span>
15. <span data-ttu-id="f0598-157">Em **Package. appxmanifest**, em **configurações do aplicativo**, tipo **PushBackgroundComponent.PushBackgroundTask** em Olá **ponto de entrada** campo.</span><span class="sxs-lookup"><span data-stu-id="f0598-157">In **Package.appxmanifest**, under **App Settings**, type **PushBackgroundComponent.PushBackgroundTask** in hello **Entry Point** field.</span></span>
    
    ![][13]
16. <span data-ttu-id="f0598-158">De saudação **arquivo** menu, clique em **Salvar tudo**.</span><span class="sxs-lookup"><span data-stu-id="f0598-158">From hello **File** menu, click **Save All**.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="f0598-159">Executar Olá aplicativo</span><span class="sxs-lookup"><span data-stu-id="f0598-159">Run hello Application</span></span>
<span data-ttu-id="f0598-160">toorun Olá aplicativo, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="f0598-160">toorun hello application, do hello following:</span></span>

1. <span data-ttu-id="f0598-161">No Visual Studio, executar Olá **AppBackend** aplicativo de API da Web.</span><span class="sxs-lookup"><span data-stu-id="f0598-161">In Visual Studio, run hello **AppBackend** Web API application.</span></span> <span data-ttu-id="f0598-162">Uma página da Web do ASP.NET é exibida.</span><span class="sxs-lookup"><span data-stu-id="f0598-162">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="f0598-163">No Visual Studio, executar Olá **NotifyUserWindowsPhone (Windows Phone 8.1)** aplicativo do Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="f0598-163">In Visual Studio, run hello **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone app.</span></span> <span data-ttu-id="f0598-164">emulador do Windows Phone Olá é executado e carrega o aplicativo hello automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f0598-164">hello Windows Phone emulator runs and loads hello app automatically.</span></span>
3. <span data-ttu-id="f0598-165">Em Olá **NotifyUserWindowsPhone** aplicativo da interface do usuário, insira um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="f0598-165">In hello **NotifyUserWindowsPhone** app UI, enter a username and password.</span></span> <span data-ttu-id="f0598-166">Eles podem ser qualquer cadeia de caracteres, mas eles devem ser Olá o mesmo valor.</span><span class="sxs-lookup"><span data-stu-id="f0598-166">These can be any string, but they must be hello same value.</span></span>
4. <span data-ttu-id="f0598-167">Em Olá **NotifyUserWindowsPhone** aplicativo da interface do usuário, clique em **efetuar login e registrar**.</span><span class="sxs-lookup"><span data-stu-id="f0598-167">In hello **NotifyUserWindowsPhone** app UI, click **Log in and register**.</span></span> <span data-ttu-id="f0598-168">Em seguida, clique em **Enviar push**.</span><span class="sxs-lookup"><span data-stu-id="f0598-168">Then click **Send push**.</span></span>

[3]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push3.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push13.png
