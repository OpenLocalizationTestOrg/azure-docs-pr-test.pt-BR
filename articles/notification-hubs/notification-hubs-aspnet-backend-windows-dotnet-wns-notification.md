---
title: "aaaAzure notificar usuários de Hubs de notificação com o back-end .NET"
description: "Saiba como toosend segura notificações por push no Azure. Exemplos de código escritos em c# usando Olá API .NET."
documentationcenter: windows
author: ysxu
manager: erikre
services: notification-hubs
editor: 
ms.assetid: 012529f2-fdbc-43c4-8634-2698164b5880
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: a366181faa81e78adf4de61435ef2790c3aa29d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-with-net-backend"></a><span data-ttu-id="58e1c-104">Notificar usuários nos Hubs de Notificação do Azure com o back-end do .NET</span><span class="sxs-lookup"><span data-stu-id="58e1c-104">Azure Notification Hubs Notify Users with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="58e1c-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="58e1c-105">Overview</span></span>
<span data-ttu-id="58e1c-106">Suporte de notificação por push no Azure permite que você tooaccess uma fácil de usar, multiplatform e infraestrutura de envio expandido, o que simplifica bastante a implementação de saudação de notificações por push para aplicativos de consumidor e empresariais para dispositivos móveis plataformas.</span><span class="sxs-lookup"><span data-stu-id="58e1c-106">Push notification support in Azure enables you tooaccess an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="58e1c-107">Este tutorial mostra como toouse Hubs de notificação do Azure toosend envio usuário de aplicativo específico de tooa notificações em um dispositivo específico.</span><span class="sxs-lookup"><span data-stu-id="58e1c-107">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa specific app user on a specific device.</span></span> <span data-ttu-id="58e1c-108">Um back-end ASP.NET WebAPI é usado tooauthenticate clientes.</span><span class="sxs-lookup"><span data-stu-id="58e1c-108">An ASP.NET WebAPI backend is used tooauthenticate clients.</span></span> <span data-ttu-id="58e1c-109">Usar Olá autenticou o usuário do cliente e marca será adicionada automaticamente pelo registro de toonotification Olá back-end.</span><span class="sxs-lookup"><span data-stu-id="58e1c-109">Using hello authenticated client user, and tag will be automatically added by hello backend toonotification registration.</span></span> <span data-ttu-id="58e1c-110">Essa marca será toosend usado por notificações de toogenerate Olá back-end para um usuário específico.</span><span class="sxs-lookup"><span data-stu-id="58e1c-110">This tag will be used toosend by hello backend toogenerate notifications for a specific user.</span></span> <span data-ttu-id="58e1c-111">Para obter mais informações sobre como registrar para notificações de usar um back-end do aplicativo, consulte o tópico de orientação de saudação [registro do seu back-end do aplicativo](http://msdn.microsoft.com/library/dn743807.aspx).</span><span class="sxs-lookup"><span data-stu-id="58e1c-111">For more information on registering for notifications using an app backend, see hello guidance topic [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="58e1c-112">Este tutorial baseia-se no projeto que você criou no hello e hub de notificação Olá [começar com Hubs de notificação] tutorial.</span><span class="sxs-lookup"><span data-stu-id="58e1c-112">This tutorial builds on hello notification hub and project that you created in hello [Get started with Notification Hubs] tutorial.</span></span>

<span data-ttu-id="58e1c-113">Este tutorial também é toohello pré-requisito Olá [proteger Push] tutorial.</span><span class="sxs-lookup"><span data-stu-id="58e1c-113">This tutorial is also hello prerequisite toohello [Secure Push] tutorial.</span></span> <span data-ttu-id="58e1c-114">Depois de concluir as etapas de saudação neste tutorial, você poderá toohello [proteger Push] tutorial, que mostra como toomodify Olá código neste tutorial toosend uma notificação por push com segurança.</span><span class="sxs-lookup"><span data-stu-id="58e1c-114">After you have completed hello steps in this tutorial, you can proceed toohello [Secure Push] tutorial, which shows how toomodify hello code in this tutorial toosend a push notification securely.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="58e1c-115">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="58e1c-115">Before you begin</span></span>
<span data-ttu-id="58e1c-116">Levamos seus comentários a sério.</span><span class="sxs-lookup"><span data-stu-id="58e1c-116">We do take your feedback seriously.</span></span> <span data-ttu-id="58e1c-117">Se você tiver dificuldade para concluir este tópico ou recomendações para melhorar este conteúdo, Apreciamos seus comentários na parte inferior da saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="58e1c-117">If you have any difficulties completing this topic, or recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span>

<span data-ttu-id="58e1c-118">código de saudação concluído para este tutorial pode ser encontrado no GitHub [aqui](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span><span class="sxs-lookup"><span data-stu-id="58e1c-118">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="58e1c-119">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="58e1c-119">Prerequisites</span></span>
<span data-ttu-id="58e1c-120">Antes de iniciar este tutorial, você já deve ter concluído estes tutoriais dos Serviços Móveis:</span><span class="sxs-lookup"><span data-stu-id="58e1c-120">Before you start this tutorial, you must have already completed these Mobile Services tutorials:</span></span>

* <span data-ttu-id="58e1c-121">[começar com Hubs de notificação]</span><span class="sxs-lookup"><span data-stu-id="58e1c-121">[Get started with Notification Hubs]</span></span><br/><span data-ttu-id="58e1c-122">Criar seu hub de notificação e reservar nome do aplicativo hello e registrar notificações tooreceive neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="58e1c-122">You create your notification hub and reserve hello app name and register tooreceive notifications in this tutorial.</span></span> <span data-ttu-id="58e1c-123">Este tutorial presume que você já concluiu essas etapas.</span><span class="sxs-lookup"><span data-stu-id="58e1c-123">This tutorial assumes you have already completed these steps.</span></span> <span data-ttu-id="58e1c-124">Se não estiver, siga as etapas de saudação em [Introdução aos Hubs de notificação (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); especificamente, Olá seções [registrar seu aplicativo para saudação da Windows Store](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) e [configurar o Hub de notificação](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span><span class="sxs-lookup"><span data-stu-id="58e1c-124">If not, please follow hello steps in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); specifically, hello sections [Register your app for hello Windows Store](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) and [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="58e1c-125">Em particular, certifique-se de que você inseriu Olá **SID do pacote** e **segredo do cliente** valores no portal de saudação em hello **configurar** guia hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="58e1c-125">In particular, make sure that you have entered hello **Package SID** and **Client Secret** values in hello portal, in hello **Configure** tab for your notification hub.</span></span> <span data-ttu-id="58e1c-126">Este procedimento de configuração é descrito na seção de saudação [configurar seu Hub de notificação](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span><span class="sxs-lookup"><span data-stu-id="58e1c-126">This configuration procedure is described in hello section [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="58e1c-127">Essa é uma etapa importante: se credenciais Olá no portal de saudação não correspondem àquelas especificadas para o nome do aplicativo hello escolhido, notificação por push de saudação não terá êxito.</span><span class="sxs-lookup"><span data-stu-id="58e1c-127">This is an important step: if hello credentials on hello portal do not match those specified for hello app name you choose, hello push notification will not succeed.</span></span>

> [!NOTE]
> <span data-ttu-id="58e1c-128">Se você estiver usando aplicativos móveis no serviço de aplicativo do Azure como seu serviço de back-end, consulte Olá [versão de aplicativos móveis](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="58e1c-128">If you are using Mobile Apps in Azure App Service as your backend service, see hello [Mobile Apps version](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) of this tutorial.</span></span>
> 
> 

&nbsp;

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="update-hello-code-for-hello-client-project"></a><span data-ttu-id="58e1c-129">Atualizar o código de saudação do projeto de cliente de saudação</span><span class="sxs-lookup"><span data-stu-id="58e1c-129">Update hello code for hello client project</span></span>
<span data-ttu-id="58e1c-130">Nesta seção, você atualizar o código de saudação no projeto Olá concluída para Olá [começar com Hubs de notificação] tutorial.</span><span class="sxs-lookup"><span data-stu-id="58e1c-130">In this section, you update hello code in hello project you completed for hello [Get started with Notification Hubs] tutorial.</span></span> <span data-ttu-id="58e1c-131">Olá já deve ser associado com o repositório de saudação e configurado para o hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="58e1c-131">hello should already be associated with hello store and configured for your notification hub.</span></span> <span data-ttu-id="58e1c-132">Nesta seção, você irá adicionar código toocall Olá novo WebAPI back-end e usá-lo para registrar e enviar notificações.</span><span class="sxs-lookup"><span data-stu-id="58e1c-132">In this section, you will add code toocall hello new WebAPI backend and use it for registering and sending notifications.</span></span>

1. <span data-ttu-id="58e1c-133">No Visual Studio, abra a solução de saudação de saudação criada para Olá [começar com Hubs de notificação] tutorial.</span><span class="sxs-lookup"><span data-stu-id="58e1c-133">In Visual Studio, open hello hello solution you created for hello [Get started with Notification Hubs] tutorial.</span></span>
2. <span data-ttu-id="58e1c-134">No Gerenciador de soluções, clique com botão direito Olá **(Windows 8.1)** do projeto e, em seguida, clique em **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="58e1c-134">In Solution Explorer, right-click hello **(Windows 8.1)** project and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="58e1c-135">No lado esquerdo do hello, clique em **Online**.</span><span class="sxs-lookup"><span data-stu-id="58e1c-135">On hello left-hand side, click **Online**.</span></span>
4. <span data-ttu-id="58e1c-136">Em Olá **pesquisa** , digite **cliente Http**.</span><span class="sxs-lookup"><span data-stu-id="58e1c-136">In hello **Search** box, type **Http Client**.</span></span>
5. <span data-ttu-id="58e1c-137">Na lista de resultados de saudação, clique em **bibliotecas de cliente HTTP Microsoft**e, em seguida, clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="58e1c-137">In hello results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="58e1c-138">Concluir a instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="58e1c-138">Complete hello installation.</span></span>
6. <span data-ttu-id="58e1c-139">Em Olá NuGet **pesquisa** , digite **Json.net**.</span><span class="sxs-lookup"><span data-stu-id="58e1c-139">Back in hello NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="58e1c-140">Instalar Olá **Json.NET** pacote e feche Olá NuGet Package Manager janela.</span><span class="sxs-lookup"><span data-stu-id="58e1c-140">Install hello **Json.NET** package, and then close hello NuGet Package Manager window.</span></span>
7. <span data-ttu-id="58e1c-141">Repita as etapas de saudação acima para Olá **(Windows Phone 8.1)** saudação do projeto tooinstall **JSON.NET** pacote NuGet para o projeto do Windows Phone hello.</span><span class="sxs-lookup"><span data-stu-id="58e1c-141">Repeat hello steps above for hello **(Windows Phone 8.1)** project tooinstall hello **JSON.NET** NuGet package for hello Windows Phone project.</span></span>
8. <span data-ttu-id="58e1c-142">No Solution Explorer, no hello **(Windows 8.1)** de projeto, clique duas vezes em **MainPage. XAML** tooopen-lo no editor do Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="58e1c-142">In Solution Explorer, in hello **(Windows 8.1)** project, double-click **MainPage.xaml** tooopen it in hello Visual Studio editor.</span></span>
9. <span data-ttu-id="58e1c-143">Em Olá **MainPage. XAML** código XML, substitua Olá `<Grid>` seção com hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="58e1c-143">In hello **MainPage.xaml** XML code, replace hello `<Grid>` section with hello following code.</span></span> <span data-ttu-id="58e1c-144">Esse código adiciona uma caixa de texto nome de usuário e senha que Olá usuário será autenticado com.</span><span class="sxs-lookup"><span data-stu-id="58e1c-144">This code adds a username and password textbox that hello user will authenticate with.</span></span> <span data-ttu-id="58e1c-145">Ele também adiciona caixas de texto de mensagem de notificação de saudação e marca de nome de usuário de saudação que deve receber a notificação de saudação:</span><span class="sxs-lookup"><span data-stu-id="58e1c-145">It also adds textboxes for hello notification message and hello username tag that should receive hello notification:</span></span>
   
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition Height="Auto"/>
                <RowDefinition Height="*"/>
            </Grid.RowDefinitions>
   
            <TextBlock Grid.Row="0" Text="Notify Users" HorizontalAlignment="Center" FontSize="48"/>
   
            <StackPanel Grid.Row="1" VerticalAlignment="Center">
                <Grid>
                    <Grid.RowDefinitions>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                    </Grid.RowDefinitions>
                    <Grid.ColumnDefinitions>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                    </Grid.ColumnDefinitions>
                    <TextBlock Grid.Row="0" Grid.ColumnSpan="3" Text="Username" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="UsernameTextBox" Grid.Row="1" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
                    <TextBlock Grid.Row="2" Grid.ColumnSpan="3" Text="Password" FontSize="24" Margin="20,0,20,0" />
                    <PasswordBox Name="PasswordTextBox" Grid.Row="3" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
   
                    <Button Grid.Row="4" Grid.ColumnSpan="3" HorizontalAlignment="Center" VerticalAlignment="Center"
                                Content="1. Login and register" Click="LoginAndRegisterClick" Margin="0,0,0,20"/>
   
                    <ToggleButton Name="toggleWNS" Grid.Row="5" Grid.Column="0" HorizontalAlignment="Right" Content="WNS" IsChecked="True" />
                    <ToggleButton Name="toggleGCM" Grid.Row="5" Grid.Column="1" HorizontalAlignment="Center" Content="GCM" />
                    <ToggleButton Name="toggleAPNS" Grid.Row="5" Grid.Column="2" HorizontalAlignment="Left" Content="APNS" />
   
                    <TextBlock Grid.Row="6" Grid.ColumnSpan="3" Text="Username Tag tooSend To" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="ToUserTagTextBox" Grid.Row="7" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <TextBlock Grid.Row="8" Grid.ColumnSpan="3" Text="Enter Notification Message" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="NotificationMessageTextBox" Grid.Row="9" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <Button Grid.Row="10" Grid.ColumnSpan="3" HorizontalAlignment="Center" Content="2. Send push" Click="PushClick" Name="SendPushButton" />
                </Grid>
            </StackPanel>
        </Grid>
10. <span data-ttu-id="58e1c-146">No Solution Explorer, no hello **(Windows Phone 8.1)** projeto, abra **MainPage. XAML** e substitua Olá Windows Phone 8.1 `<Grid>` seção com esse mesmo código acima.</span><span class="sxs-lookup"><span data-stu-id="58e1c-146">In Solution Explorer, in hello **(Windows Phone 8.1)** project, open **MainPage.xaml** and replace hello Windows Phone 8.1 `<Grid>` section with that same code above.</span></span> <span data-ttu-id="58e1c-147">interface Olá deve ter aparência semelhante toowhats mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="58e1c-147">hello interface should look similar toowhats shown below.</span></span>
    
    ![][13]
11. <span data-ttu-id="58e1c-148">No Gerenciador de soluções, abra Olá **MainPage.xaml.cs** arquivo hello **(Windows 8.1)** e **(Windows Phone 8.1)** projetos.</span><span class="sxs-lookup"><span data-stu-id="58e1c-148">In Solution Explorer, open hello **MainPage.xaml.cs** file for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span> <span data-ttu-id="58e1c-149">Adicione o seguinte Olá `using` instruções na parte superior da saudação dos dois arquivos:</span><span class="sxs-lookup"><span data-stu-id="58e1c-149">Add hello following `using` statements at hello top of both files:</span></span>
    
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Windows.Networking.PushNotifications;
        using Windows.UI.Popups;
        using System.Threading.Tasks;
12. <span data-ttu-id="58e1c-150">Em **MainPage.xaml.cs** para Olá **(Windows 8.1)** e **(Windows Phone 8.1)** projetos, adicionar Olá toohello membro a seguir `MainPage` classe.</span><span class="sxs-lookup"><span data-stu-id="58e1c-150">In **MainPage.xaml.cs** for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects, add hello following member toohello `MainPage` class.</span></span> <span data-ttu-id="58e1c-151">Ser tooreplace se `<Enter Your Backend Endpoint>` com hello seu ponto de extremidade de back-end real obtido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="58e1c-151">Be sure tooreplace `<Enter Your Backend Endpoint>` with hello your actual backend endpoint obtained previously.</span></span> <span data-ttu-id="58e1c-152">Por exemplo: `http://mybackend.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="58e1c-152">For example, `http://mybackend.azurewebsites.net`.</span></span>
    
        private static string BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";
13. <span data-ttu-id="58e1c-153">Adicione código Olá abaixo classe MainPage toohello **MainPage.xaml.cs** para Olá **(Windows 8.1)** e **(Windows Phone 8.1)** projetos.</span><span class="sxs-lookup"><span data-stu-id="58e1c-153">Add hello code below toohello MainPage class in **MainPage.xaml.cs** for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span>
    
    <span data-ttu-id="58e1c-154">Olá `PushClick` método é hello manipulador de clique do hello **enviar por Push** botão.</span><span class="sxs-lookup"><span data-stu-id="58e1c-154">hello `PushClick` method is hello click handler for hello **Send Push** button.</span></span> <span data-ttu-id="58e1c-155">Chama Olá back-end tootrigger tooall uma notificação dispositivos com uma marca de nome de usuário que corresponde a saudação `to_tag` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="58e1c-155">It calls hello backend tootrigger a notification tooall devices with a username tag that matches hello `to_tag` parameter.</span></span> <span data-ttu-id="58e1c-156">mensagem de notificação de saudação é enviada como conteúdo JSON no corpo da solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="58e1c-156">hello notification message is sent as JSON content in hello request body.</span></span>
    
    <span data-ttu-id="58e1c-157">Olá `LoginAndRegisterClick` método é hello manipulador de clique do hello **efetuar login e registrar** botão.</span><span class="sxs-lookup"><span data-stu-id="58e1c-157">hello `LoginAndRegisterClick` method is hello click handler for hello **Log in and register** button.</span></span> <span data-ttu-id="58e1c-158">Ele armazena Olá basic, em seguida, usa o token de autenticação no armazenamento local (Observe que isso representa qualquer token usa o esquema de autenticação), `RegisterClient` tooregister para notificações usando Olá back-end.</span><span class="sxs-lookup"><span data-stu-id="58e1c-158">It stores hello basic authentication token in local storage (note that this represents any token your authentication scheme uses), then uses `RegisterClient` tooregister for notifications using hello backend.</span></span>

        private async void PushClick(object sender, RoutedEventArgs e)
        {
            if (toggleWNS.IsChecked.Value)
            {
                await sendPush("wns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleGCM.IsChecked.Value)
            {
                await sendPush("gcm", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleAPNS.IsChecked.Value)
            {
                await sendPush("apns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);

            }
        }

        private async Task sendPush(string pns, string userTag, string message)
        {
            var POST_URL = BACKEND_ENDPOINT + "/api/notifications?pns=" +
                pns + "&to_tag=" + userTag;

            using (var httpClient = new HttpClient())
            {
                var settings = ApplicationData.Current.LocalSettings.Values;
                httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);

                try
                {
                    await httpClient.PostAsync(POST_URL, new StringContent("\"" + message + "\"",
                        System.Text.Encoding.UTF8, "application/json"));
                }
                catch (Exception ex)
                {
                    MessageDialog alert = new MessageDialog(ex.Message, "Failed toosend " + pns + " message");
                    alert.ShowAsync();
                }
            }
        }

        private async void LoginAndRegisterClick(object sender, RoutedEventArgs e)
        {
            SetAuthenticationTokenInLocalStorage();

            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

            // hello "username:<user name>" tag gets automatically added by hello message handler in hello backend.
            // hello tag passed here can be whatever other tags you may want toouse.
            try
            {
                // hello device handle used will be different depending on hello device and PNS. 
                // Windows devices use hello channel uri as hello PNS handle.
                await new RegisterClient(BACKEND_ENDPOINT).RegisterAsync(channel.Uri, new string[] { "myTag" });

                var dialog = new MessageDialog("Registered as: " + UsernameTextBox.Text);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
                SendPushButton.IsEnabled = true;
            }
            catch (Exception ex)
            {
                MessageDialog alert = new MessageDialog(ex.Message, "Failed tooregister with RegisterClient");
                alert.ShowAsync();
            }
        }

        private void SetAuthenticationTokenInLocalStorage()
        {
            string username = UsernameTextBox.Text;
            string password = PasswordTextBox.Password;

            var token = Convert.ToBase64String(System.Text.Encoding.UTF8.GetBytes(username + ":" + password));
            ApplicationData.Current.LocalSettings.Values["AuthenticationToken"] = token;
        }



1. <span data-ttu-id="58e1c-159">No Gerenciador de soluções, em Olá **compartilhado** projeto, abra Olá **App.xaml.cs** arquivo.</span><span class="sxs-lookup"><span data-stu-id="58e1c-159">In Solution Explorer, under hello **Shared** project, open hello **App.xaml.cs** file.</span></span> <span data-ttu-id="58e1c-160">Localizar chamada hello muito`InitNotificationsAsync()` em Olá `OnLaunched()` manipulador de eventos.</span><span class="sxs-lookup"><span data-stu-id="58e1c-160">Find hello call too`InitNotificationsAsync()` in hello `OnLaunched()` event handler.</span></span> <span data-ttu-id="58e1c-161">Comentar ou excluir chamada hello muito`InitNotificationsAsync()`.</span><span class="sxs-lookup"><span data-stu-id="58e1c-161">Comment out or delete hello call too`InitNotificationsAsync()`.</span></span> <span data-ttu-id="58e1c-162">manipulador de saudação do botão adicionado acima inicializará registros de notificação.</span><span class="sxs-lookup"><span data-stu-id="58e1c-162">hello button handler added above will initialize notification registrations.</span></span>

        protected override void OnLaunched(LaunchActivatedEventArgs e)
        {
            //InitNotificationsAsync();


1. <span data-ttu-id="58e1c-163">No Gerenciador de soluções, clique com botão direito Olá **compartilhado** projeto e, em seguida, clique em **adicionar**e, em seguida, clique em **classe**.</span><span class="sxs-lookup"><span data-stu-id="58e1c-163">In Solution Explorer, right-click hello **Shared** project, then click **Add**, and then click **Class**.</span></span> <span data-ttu-id="58e1c-164">Nome de classe Olá **RegisterClient.cs**, em seguida, clique em **Okey** toogenerate classe de saudação.</span><span class="sxs-lookup"><span data-stu-id="58e1c-164">Name hello class **RegisterClient.cs**, then click **OK** toogenerate hello class.</span></span>
   
   <span data-ttu-id="58e1c-165">Essa classe será ajustado Olá REST chamadas toocontact necessário Olá aplicativo back-end, em ordem tooregister para notificações por push.</span><span class="sxs-lookup"><span data-stu-id="58e1c-165">This class will wrap hello REST calls required toocontact hello app backend, in order tooregister for push notifications.</span></span> <span data-ttu-id="58e1c-166">Também localmente armazena Olá *registrationIds* criado pelo Olá Hub de notificação, conforme detalhado no [registro do seu back-end do aplicativo](http://msdn.microsoft.com/library/dn743807.aspx).</span><span class="sxs-lookup"><span data-stu-id="58e1c-166">It also locally stores hello *registrationIds* created by hello Notification Hub as detailed in [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="58e1c-167">Observe que ele usa um token de autorização armazenado no armazenamento local quando você clica em Olá **efetuar login e registrar** botão.</span><span class="sxs-lookup"><span data-stu-id="58e1c-167">Note that it uses an authorization token stored in local storage when you click hello **Log in and register** button.</span></span>
2. <span data-ttu-id="58e1c-168">Adicione o seguinte Olá `using` instruções na parte superior de saudação do arquivo de RegisterClient.cs hello:</span><span class="sxs-lookup"><span data-stu-id="58e1c-168">Add hello following `using` statements at hello top of hello RegisterClient.cs file:</span></span>
   
       using Windows.Storage;
       using System.Net;
       using System.Net.Http;
       using System.Net.Http.Headers;
       using Newtonsoft.Json;
       using System.Threading.Tasks;
       using System.Linq;
3. <span data-ttu-id="58e1c-169">Adicionar Olá seguindo o código dentro de saudação `RegisterClient` definição da classe.</span><span class="sxs-lookup"><span data-stu-id="58e1c-169">Add hello following code inside hello `RegisterClient` class definition.</span></span>
   
       private string POST_URL;
   
       private class DeviceRegistration
       {
           public string Platform { get; set; }
           public string Handle { get; set; }
           public string[] Tags { get; set; }
       }
   
       public RegisterClient(string backendEndpoint)
       {
           POST_URL = backendEndpoint + "/api/register";
       }
   
       public async Task RegisterAsync(string handle, IEnumerable<string> tags)
       {
           var regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
   
           var deviceRegistration = new DeviceRegistration
           {
               Platform = "wns",
               Handle = handle,
               Tags = tags.ToArray<string>()
           };
   
           var statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
   
           if (statusCode == HttpStatusCode.Gone)
           {
               // regId is expired, deleting from local storage & recreating
               var settings = ApplicationData.Current.LocalSettings.Values;
               settings.Remove("__NHRegistrationId");
               regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
               statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
           }
   
           if (statusCode != HttpStatusCode.Accepted)
           {
               // log or throw
               throw new System.Net.WebException(statusCode.ToString());
           }
       }
   
       private async Task<HttpStatusCode> UpdateRegistrationAsync(string regId, DeviceRegistration deviceRegistration)
       {
           using (var httpClient = new HttpClient())
           {
               var settings = ApplicationData.Current.LocalSettings.Values;
               httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string) settings["AuthenticationToken"]);
   
               var putUri = POST_URL + "/" + regId;
   
               string json = JsonConvert.SerializeObject(deviceRegistration);
                               var response = await httpClient.PutAsync(putUri, new StringContent(json, Encoding.UTF8, "application/json"));
               return response.StatusCode;
           }
       }
   
       private async Task<string> RetrieveRegistrationIdOrRequestNewOneAsync()
       {
           var settings = ApplicationData.Current.LocalSettings.Values;
           if (!settings.ContainsKey("__NHRegistrationId"))
           {
               using (var httpClient = new HttpClient())
               {
                   httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                   var response = await httpClient.PostAsync(POST_URL, new StringContent(""));
                   if (response.IsSuccessStatusCode)
                   {
                       string regId = await response.Content.ReadAsStringAsync();
                       regId = regId.Substring(1, regId.Length - 2);
                       settings.Add("__NHRegistrationId", regId);
                   }
                   else
                   {
                       throw new System.Net.WebException(response.StatusCode.ToString());
                   }
               }
           }
           return (string)settings["__NHRegistrationId"];
   
       }
4. <span data-ttu-id="58e1c-170">Salve todas as alterações.</span><span class="sxs-lookup"><span data-stu-id="58e1c-170">Save all your changes.</span></span>

## <a name="testing-hello-application"></a><span data-ttu-id="58e1c-171">Aplicativo em teste</span><span class="sxs-lookup"><span data-stu-id="58e1c-171">Testing hello Application</span></span>
1. <span data-ttu-id="58e1c-172">Inicie o aplicativo hello no Windows 8.1 e Windows Phone 8.1.</span><span class="sxs-lookup"><span data-stu-id="58e1c-172">Launch hello application on both Windows 8.1 and Windows Phone 8.1.</span></span> <span data-ttu-id="58e1c-173">Para Windows Phone 8.1, você pode executar instância Olá no emulador de saudação ou um dispositivo real.</span><span class="sxs-lookup"><span data-stu-id="58e1c-173">For Windows Phone 8.1 you can run hello instance in hello emulator or an actual device.</span></span>
2. <span data-ttu-id="58e1c-174">Na instância de saudação do Windows 8.1 do aplicativo hello, insira um **Username** e **senha** conforme mostrado na tela hello abaixo.</span><span class="sxs-lookup"><span data-stu-id="58e1c-174">In hello Windows 8.1 instance of hello app, enter a **Username** and **Password** as shown in hello screen below.</span></span> <span data-ttu-id="58e1c-175">Ele deve diferir de saudação nome e a senha que você inserir no Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="58e1c-175">It should differ from hello user name and password you enter on Windows Phone.</span></span>
3. <span data-ttu-id="58e1c-176">Clique em **Fazer logon e registrar** e verifique se um diálogo mostra que você fez logon.</span><span class="sxs-lookup"><span data-stu-id="58e1c-176">Click **Log in and register** and verify a dialog shows that you have logged in.</span></span> <span data-ttu-id="58e1c-177">Isso também permitirá Olá **enviar por Push** botão.</span><span class="sxs-lookup"><span data-stu-id="58e1c-177">This will also enable hello **Send Push** button.</span></span>
   
    ![][14]
4. <span data-ttu-id="58e1c-178">Na instância de saudação Windows Phone 8.1, insira uma cadeia de caracteres de nome de usuário em ambos os Olá **Username** e **senha** campos, em seguida, clique em **logon e registrar**.</span><span class="sxs-lookup"><span data-stu-id="58e1c-178">On hello Windows Phone 8.1 instance, enter a user name string in both hello **Username** and **Password** fields then click **Login and register**.</span></span>
5. <span data-ttu-id="58e1c-179">Em seguida, em Olá **marca de nome de usuário do destinatário** , digite o nome de usuário Olá registrado no Windows 8.1.</span><span class="sxs-lookup"><span data-stu-id="58e1c-179">Then in hello **Recipient Username Tag** field, enter hello user name registered on Windows 8.1.</span></span> <span data-ttu-id="58e1c-180">Digite uma mensagem de notificação e clique em **Enviar notificação por push**.</span><span class="sxs-lookup"><span data-stu-id="58e1c-180">Enter a notification message and click **Send Push**.</span></span>
   
    ![][16]
6. <span data-ttu-id="58e1c-181">Somente os dispositivos de saudação que foram registrados com marca de nome de usuário correspondente Olá recebem a mensagem de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="58e1c-181">Only hello devices that have registered with hello matching username tag receive hello notification message.</span></span>
   
    ![][15]

## <a name="next-steps"></a><span data-ttu-id="58e1c-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="58e1c-182">Next Steps</span></span>
* <span data-ttu-id="58e1c-183">Se você quiser toosegment os usuários, grupos de interesse, consulte [toosend de Hubs de notificação de uso últimas notícias].</span><span class="sxs-lookup"><span data-stu-id="58e1c-183">If you want toosegment your users by interest groups, see [Use Notification Hubs toosend breaking news].</span></span>
* <span data-ttu-id="58e1c-184">toolearn mais informações sobre como toouse Hubs de notificação, consulte [orientação de Hubs de notificação].</span><span class="sxs-lookup"><span data-stu-id="58e1c-184">toolearn more about how toouse Notification Hubs, see [Notification Hubs Guidance].</span></span>

[9]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push9.png
[10]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push10.png
[11]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push11.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-ui.png
[14]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-windows-instance-username.png
[15]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-notification-received.png
[16]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-send-message.png



<!-- URLs. -->
[começar com Hubs de notificação]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[proteger Push]: notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md
[toosend de Hubs de notificação de uso últimas notícias]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[orientação de Hubs de notificação]: http://msdn.microsoft.com/library/jj927170.aspx
