---
title: "Notificar usuários nos Hubs de Notificação do Azure com o back-end do .NET"
description: "Saiba como enviar notificações por push seguro no Azure. Amostras de código escrito em C# usando a API .NET."
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
ms.openlocfilehash: c0b963ef661612b1a176dd8e5f01d56e61eb5acb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-notify-users-with-net-backend"></a><span data-ttu-id="da013-104">Notificar usuários nos Hubs de Notificação do Azure com o back-end do .NET</span><span class="sxs-lookup"><span data-stu-id="da013-104">Azure Notification Hubs Notify Users with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="da013-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="da013-105">Overview</span></span>
<span data-ttu-id="da013-106">O suporte à notificação por push no Azure permite que você acesse uma infraestrutura de envio por push fácil de usar, multiplataforma e expansível que simplifica em muito a implementação de notificações por push para aplicativos de consumidor e empresariais para plataformas móveis.</span><span class="sxs-lookup"><span data-stu-id="da013-106">Push notification support in Azure enables you to access an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="da013-107">Este tutorial mostra como usar os Hubs de Notificação do Azure para enviar notificações por push a um usuário específico do aplicativo em um dispositivo específico.</span><span class="sxs-lookup"><span data-stu-id="da013-107">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a specific app user on a specific device.</span></span> <span data-ttu-id="da013-108">Um back-end de WebAPI do ASP.NET é usado para autenticar clientes.</span><span class="sxs-lookup"><span data-stu-id="da013-108">An ASP.NET WebAPI backend is used to authenticate clients.</span></span> <span data-ttu-id="da013-109">Usando o usuário cliente autenticado e a marca será automaticamente adicionada pelo back-end para o registro de notificação.</span><span class="sxs-lookup"><span data-stu-id="da013-109">Using the authenticated client user, and tag will be automatically added by the backend to notification registration.</span></span> <span data-ttu-id="da013-110">Essa marca será usada para enviar pelo back-end para gerar notificações para um usuário específico.</span><span class="sxs-lookup"><span data-stu-id="da013-110">This tag will be used to send by the backend to generate notifications for a specific user.</span></span> <span data-ttu-id="da013-111">Para obter mais informações sobre como se registrar para receber notificações usando um back-end do aplicativo, consulte o tópico de diretrizes [Registrando-se por meio do back-end do aplicativo](http://msdn.microsoft.com/library/dn743807.aspx).</span><span class="sxs-lookup"><span data-stu-id="da013-111">For more information on registering for notifications using an app backend, see the guidance topic [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="da013-112">Este tutorial baseia-se no hub de notificação que você criou no tutorial [Introdução aos Hubs de Notificação] .</span><span class="sxs-lookup"><span data-stu-id="da013-112">This tutorial builds on the notification hub and project that you created in the [Get started with Notification Hubs] tutorial.</span></span>

<span data-ttu-id="da013-113">Este tutorial também é um pré-requisito para o tutorial [Push Seguro] .</span><span class="sxs-lookup"><span data-stu-id="da013-113">This tutorial is also the prerequisite to the [Secure Push] tutorial.</span></span> <span data-ttu-id="da013-114">Depois de concluir as etapas deste tutorial, você pode prosseguir para o tutorial [Push Seguro] , que mostra como modificar o código neste tutorial para enviar uma notificação por push com segurança.</span><span class="sxs-lookup"><span data-stu-id="da013-114">After you have completed the steps in this tutorial, you can proceed to the [Secure Push] tutorial, which shows how to modify the code in this tutorial to send a push notification securely.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="da013-115">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="da013-115">Before you begin</span></span>
<span data-ttu-id="da013-116">Levamos seus comentários a sério.</span><span class="sxs-lookup"><span data-stu-id="da013-116">We do take your feedback seriously.</span></span> <span data-ttu-id="da013-117">Se você tiver alguma dificuldade para concluir este tópico ou recomendações para melhorar este conteúdo, apreciaremos seus comentários na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="da013-117">If you have any difficulties completing this topic, or recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span>

<span data-ttu-id="da013-118">O código completo para este tutorial pode ser encontrado no GitHub [aqui](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span><span class="sxs-lookup"><span data-stu-id="da013-118">The completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="da013-119">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="da013-119">Prerequisites</span></span>
<span data-ttu-id="da013-120">Antes de iniciar este tutorial, você já deve ter concluído estes tutoriais dos Serviços Móveis:</span><span class="sxs-lookup"><span data-stu-id="da013-120">Before you start this tutorial, you must have already completed these Mobile Services tutorials:</span></span>

* <span data-ttu-id="da013-121">[Introdução aos Hubs de Notificação]</span><span class="sxs-lookup"><span data-stu-id="da013-121">[Get started with Notification Hubs]</span></span><br/><span data-ttu-id="da013-122">Você cria seu hub de notificação, reserva o nome do aplicativo e se registra para receber notificações nesse tutorial.</span><span class="sxs-lookup"><span data-stu-id="da013-122">You create your notification hub and reserve the app name and register to receive notifications in this tutorial.</span></span> <span data-ttu-id="da013-123">Este tutorial presume que você já concluiu essas etapas.</span><span class="sxs-lookup"><span data-stu-id="da013-123">This tutorial assumes you have already completed these steps.</span></span> <span data-ttu-id="da013-124">Do contrário, siga as etapas descritas em [Introdução aos Hubs de Notificação (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); especificamente, as seções [Registrar seu aplicativo para a Windows Store](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) e [Configurar seu Hub de Notificação](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span><span class="sxs-lookup"><span data-stu-id="da013-124">If not, please follow the steps in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); specifically, the sections [Register your app for the Windows Store](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) and [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="da013-125">Especificamente, não se esqueça de inserir os valores de **SID do Pacote** e **Segredo do Cliente** no portal, na guia **Configurar** de seu hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="da013-125">In particular, make sure that you have entered the **Package SID** and **Client Secret** values in the portal, in the **Configure** tab for your notification hub.</span></span> <span data-ttu-id="da013-126">Esse procedimento de configuração é descrito na seção [Configurar seu Hub de Notificação](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span><span class="sxs-lookup"><span data-stu-id="da013-126">This configuration procedure is described in the section [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="da013-127">Esta é uma etapa importante: se as credenciais no portal não corresponderem àquelas especificadas para o nome do aplicativo escolhido, a notificação por push não será bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="da013-127">This is an important step: if the credentials on the portal do not match those specified for the app name you choose, the push notification will not succeed.</span></span>

> [!NOTE]
> <span data-ttu-id="da013-128">Se você estiver usando Aplicativos Móveis no Serviço de Aplicativo do Azure como serviço de back-end, consulte a [versão dos Aplicativos Móveis](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="da013-128">If you are using Mobile Apps in Azure App Service as your backend service, see the [Mobile Apps version](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) of this tutorial.</span></span>
> 
> 

&nbsp;

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="update-the-code-for-the-client-project"></a><span data-ttu-id="da013-129">Atualizar o código para o projeto cliente</span><span class="sxs-lookup"><span data-stu-id="da013-129">Update the code for the client project</span></span>
<span data-ttu-id="da013-130">Nesta seção, você atualiza o código no projeto concluído no tutorial [Introdução aos Hubs de Notificação] .</span><span class="sxs-lookup"><span data-stu-id="da013-130">In this section, you update the code in the project you completed for the [Get started with Notification Hubs] tutorial.</span></span> <span data-ttu-id="da013-131">Ele já deve estar associado à loja e configurado para o hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="da013-131">The should already be associated with the store and configured for your notification hub.</span></span> <span data-ttu-id="da013-132">Nesta seção, você adicionará código para chamar o novo back-end da WebAPI e o usará para se registrar e enviar notificações.</span><span class="sxs-lookup"><span data-stu-id="da013-132">In this section, you will add code to call the new WebAPI backend and use it for registering and sending notifications.</span></span>

1. <span data-ttu-id="da013-133">No Visual Studio, abra a solução criada no tutorial [Introdução aos Hubs de Notificação] .</span><span class="sxs-lookup"><span data-stu-id="da013-133">In Visual Studio, open the the solution you created for the [Get started with Notification Hubs] tutorial.</span></span>
2. <span data-ttu-id="da013-134">No Gerenciador de Soluções, clique com o botão direito do mouse no projeto **(Windows 8.1)** e clique em **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="da013-134">In Solution Explorer, right-click the **(Windows 8.1)** project and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="da013-135">No lado esquerdo, clique em **Online**.</span><span class="sxs-lookup"><span data-stu-id="da013-135">On the left-hand side, click **Online**.</span></span>
4. <span data-ttu-id="da013-136">Na caixa **Pesquisar**, digite **Http Client**.</span><span class="sxs-lookup"><span data-stu-id="da013-136">In the **Search** box, type **Http Client**.</span></span>
5. <span data-ttu-id="da013-137">Na lista de resultados, clique em **Bibliotecas de Cliente HTTP da Microsoft** e em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="da013-137">In the results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="da013-138">Conclua a instalação.</span><span class="sxs-lookup"><span data-stu-id="da013-138">Complete the installation.</span></span>
6. <span data-ttu-id="da013-139">De volta à caixa **Pesquisar** do NuGet, digite **Json.net**.</span><span class="sxs-lookup"><span data-stu-id="da013-139">Back in the NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="da013-140">Instale o pacote **Json.NET** e feche a janela do Gerenciador de Pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="da013-140">Install the **Json.NET** package, and then close the NuGet Package Manager window.</span></span>
7. <span data-ttu-id="da013-141">Repita as etapas acima para o projeto **(Windows Phone 8.1)** para instalar o pacote NuGet **JSON.NET** para o projeto do Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="da013-141">Repeat the steps above for the **(Windows Phone 8.1)** project to install the **JSON.NET** NuGet package for the Windows Phone project.</span></span>
8. <span data-ttu-id="da013-142">No Gerenciador de Soluções, no projeto **(Windows Phone 8.1)**, clique duas vezes em **MainPage.xaml** para abri-lo no editor do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="da013-142">In Solution Explorer, in the **(Windows 8.1)** project, double-click **MainPage.xaml** to open it in the Visual Studio editor.</span></span>
9. <span data-ttu-id="da013-143">No código de XML de **MainPage.xaml**, substitua a seção `<Grid>` pelo código a seguir.</span><span class="sxs-lookup"><span data-stu-id="da013-143">In the **MainPage.xaml** XML code, replace the `<Grid>` section with the following code.</span></span> <span data-ttu-id="da013-144">Este código adiciona uma caixa de texto de nome de usuário e de senha com as quais o usuário irá autenticar.</span><span class="sxs-lookup"><span data-stu-id="da013-144">This code adds a username and password textbox that the user will authenticate with.</span></span> <span data-ttu-id="da013-145">Ele também adiciona caixas de texto para a mensagem de notificação e a marca de nome de usuário que deve receber a notificação:</span><span class="sxs-lookup"><span data-stu-id="da013-145">It also adds textboxes for the notification message and the username tag that should receive the notification:</span></span>
   
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
   
                    <TextBlock Grid.Row="6" Grid.ColumnSpan="3" Text="Username Tag To Send To" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="ToUserTagTextBox" Grid.Row="7" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <TextBlock Grid.Row="8" Grid.ColumnSpan="3" Text="Enter Notification Message" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="NotificationMessageTextBox" Grid.Row="9" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <Button Grid.Row="10" Grid.ColumnSpan="3" HorizontalAlignment="Center" Content="2. Send push" Click="PushClick" Name="SendPushButton" />
                </Grid>
            </StackPanel>
        </Grid>
10. <span data-ttu-id="da013-146">No Gerenciador de Soluções, no projeto **(Windows Phone 8.1)**, abra **MainPage.xaml** e substitua a seção Windows Phone 8.1 `<Grid>` com esse mesmo código acima.</span><span class="sxs-lookup"><span data-stu-id="da013-146">In Solution Explorer, in the **(Windows Phone 8.1)** project, open **MainPage.xaml** and replace the Windows Phone 8.1 `<Grid>` section with that same code above.</span></span> <span data-ttu-id="da013-147">A interface deve ser semelhante ao que está mostrado a seguir.</span><span class="sxs-lookup"><span data-stu-id="da013-147">The interface should look similar to whats shown below.</span></span>
    
    ![][13]
11. <span data-ttu-id="da013-148">No Gerenciador de Soluções, abra o arquivo **MainPage.xaml.cs** para os projetos **(Windows 8.1)** e **(Windows Phone 8.1)**.</span><span class="sxs-lookup"><span data-stu-id="da013-148">In Solution Explorer, open the **MainPage.xaml.cs** file for the **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span> <span data-ttu-id="da013-149">Adicione as seguintes instruções `using` na parte superior dos dois arquivos:</span><span class="sxs-lookup"><span data-stu-id="da013-149">Add the following `using` statements at the top of both files:</span></span>
    
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Windows.Networking.PushNotifications;
        using Windows.UI.Popups;
        using System.Threading.Tasks;
12. <span data-ttu-id="da013-150">Em **MainPage.xaml.cs** para os projetos **(Windows 8.1)** e **(Windows Phone 8.1)**, adicione o membro a seguir para a classe `MainPage`.</span><span class="sxs-lookup"><span data-stu-id="da013-150">In **MainPage.xaml.cs** for the **(Windows 8.1)** and **(Windows Phone 8.1)** projects, add the following member to the `MainPage` class.</span></span> <span data-ttu-id="da013-151">Substitua `<Enter Your Backend Endpoint>` pelo ponto de extremidade de back-end real obtido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="da013-151">Be sure to replace `<Enter Your Backend Endpoint>` with the your actual backend endpoint obtained previously.</span></span> <span data-ttu-id="da013-152">Por exemplo: `http://mybackend.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="da013-152">For example, `http://mybackend.azurewebsites.net`.</span></span>
    
        private static string BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";
13. <span data-ttu-id="da013-153">Adicione o código a seguir à classe MainPage em **MainPage.xaml.cs** para os projetos **(Windows 8.1)** e **(Windows Phone 8.1)**.</span><span class="sxs-lookup"><span data-stu-id="da013-153">Add the code below to the MainPage class in **MainPage.xaml.cs** for the **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span>
    
    <span data-ttu-id="da013-154">O método `PushClick` é o manipulador de cliques para o botão **Enviar por Push** .</span><span class="sxs-lookup"><span data-stu-id="da013-154">The `PushClick` method is the click handler for the **Send Push** button.</span></span> <span data-ttu-id="da013-155">Ele chama o back-end para disparar uma notificação para todos os dispositivos com uma marca de nome de usuário que corresponde ao parâmetro `to_tag` .</span><span class="sxs-lookup"><span data-stu-id="da013-155">It calls the backend to trigger a notification to all devices with a username tag that matches the `to_tag` parameter.</span></span> <span data-ttu-id="da013-156">A mensagem de notificação é enviada como conteúdo JSON no corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="da013-156">The notification message is sent as JSON content in the request body.</span></span>
    
    <span data-ttu-id="da013-157">O método `LoginAndRegisterClick` é o manipulador de cliques para o botão **Fazer logon e registrar** .</span><span class="sxs-lookup"><span data-stu-id="da013-157">The `LoginAndRegisterClick` method is the click handler for the **Log in and register** button.</span></span> <span data-ttu-id="da013-158">Ele armazena o token de autenticação básica localmente (observe que isso representa qualquer token usado pelo seu esquema de autenticação) e utiliza `RegisterClient` para o registro de notificações usando o back-end.</span><span class="sxs-lookup"><span data-stu-id="da013-158">It stores the basic authentication token in local storage (note that this represents any token your authentication scheme uses), then uses `RegisterClient` to register for notifications using the backend.</span></span>

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
                    MessageDialog alert = new MessageDialog(ex.Message, "Failed to send " + pns + " message");
                    alert.ShowAsync();
                }
            }
        }

        private async void LoginAndRegisterClick(object sender, RoutedEventArgs e)
        {
            SetAuthenticationTokenInLocalStorage();

            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

            // The "username:<user name>" tag gets automatically added by the message handler in the backend.
            // The tag passed here can be whatever other tags you may want to use.
            try
            {
                // The device handle used will be different depending on the device and PNS. 
                // Windows devices use the channel uri as the PNS handle.
                await new RegisterClient(BACKEND_ENDPOINT).RegisterAsync(channel.Uri, new string[] { "myTag" });

                var dialog = new MessageDialog("Registered as: " + UsernameTextBox.Text);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
                SendPushButton.IsEnabled = true;
            }
            catch (Exception ex)
            {
                MessageDialog alert = new MessageDialog(ex.Message, "Failed to register with RegisterClient");
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



1. <span data-ttu-id="da013-159">No Gerenciador de Soluções, sob o projeto **Compartilhado**, abra o arquivo **App.xaml.cs**.</span><span class="sxs-lookup"><span data-stu-id="da013-159">In Solution Explorer, under the **Shared** project, open the **App.xaml.cs** file.</span></span> <span data-ttu-id="da013-160">Localize a chamada para `InitNotificationsAsync()` in the `OnLaunched()` .</span><span class="sxs-lookup"><span data-stu-id="da013-160">Find the call to `InitNotificationsAsync()` in the `OnLaunched()` event handler.</span></span> <span data-ttu-id="da013-161">Comentar ou excluir a chamada para `InitNotificationsAsync()`.</span><span class="sxs-lookup"><span data-stu-id="da013-161">Comment out or delete the call to `InitNotificationsAsync()`.</span></span> <span data-ttu-id="da013-162">O manipulador do botão adicionado acima irá inicializar os registros de notificação.</span><span class="sxs-lookup"><span data-stu-id="da013-162">The button handler added above will initialize notification registrations.</span></span>

        protected override void OnLaunched(LaunchActivatedEventArgs e)
        {
            //InitNotificationsAsync();


1. <span data-ttu-id="da013-163">No Gerenciador de Soluções, clique com o botão direito do mouse no projeto **Compartilhado**, clique em **Adicionar** e em **Classe**.</span><span class="sxs-lookup"><span data-stu-id="da013-163">In Solution Explorer, right-click the **Shared** project, then click **Add**, and then click **Class**.</span></span> <span data-ttu-id="da013-164">Nomeie a classe como **RegisterClient.cs** e clique em **OK** para gerar a classe.</span><span class="sxs-lookup"><span data-stu-id="da013-164">Name the class **RegisterClient.cs**, then click **OK** to generate the class.</span></span>
   
   <span data-ttu-id="da013-165">Essa classe irá encapsular as chamadas do REST necessárias para entrar em contato com o back-end do aplicativo de modo a se registrar para as notificações por push.</span><span class="sxs-lookup"><span data-stu-id="da013-165">This class will wrap the REST calls required to contact the app backend, in order to register for push notifications.</span></span> <span data-ttu-id="da013-166">Ele também armazena localmente os *registrationIds* criados pelo Hub de Notificação, conforme detalhado em [Registrando-se por meio do back-end do aplicativo](http://msdn.microsoft.com/library/dn743807.aspx).</span><span class="sxs-lookup"><span data-stu-id="da013-166">It also locally stores the *registrationIds* created by the Notification Hub as detailed in [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="da013-167">Observe que ele usa um token de autorização armazenado localmente quando você clica no botão **Fazer logon e registrar-se** .</span><span class="sxs-lookup"><span data-stu-id="da013-167">Note that it uses an authorization token stored in local storage when you click the **Log in and register** button.</span></span>
2. <span data-ttu-id="da013-168">Adicione as seguintes instruções `using` à parte superior do arquivo RegisterClient.cs:</span><span class="sxs-lookup"><span data-stu-id="da013-168">Add the following `using` statements at the top of the RegisterClient.cs file:</span></span>
   
       using Windows.Storage;
       using System.Net;
       using System.Net.Http;
       using System.Net.Http.Headers;
       using Newtonsoft.Json;
       using System.Threading.Tasks;
       using System.Linq;
3. <span data-ttu-id="da013-169">Adicione o código a seguir à definição de classe `RegisterClient` .</span><span class="sxs-lookup"><span data-stu-id="da013-169">Add the following code inside the `RegisterClient` class definition.</span></span>
   
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
4. <span data-ttu-id="da013-170">Salve todas as alterações.</span><span class="sxs-lookup"><span data-stu-id="da013-170">Save all your changes.</span></span>

## <a name="testing-the-application"></a><span data-ttu-id="da013-171">Testando o aplicativo</span><span class="sxs-lookup"><span data-stu-id="da013-171">Testing the Application</span></span>
1. <span data-ttu-id="da013-172">Inicie o aplicativo no Windows 8.1 e no Windows Phone 8.1.</span><span class="sxs-lookup"><span data-stu-id="da013-172">Launch the application on both Windows 8.1 and Windows Phone 8.1.</span></span> <span data-ttu-id="da013-173">Para o Windows Phone 8.1, você pode executar a instância no emulador ou em um dispositivo real.</span><span class="sxs-lookup"><span data-stu-id="da013-173">For Windows Phone 8.1 you can run the instance in the emulator or an actual device.</span></span>
2. <span data-ttu-id="da013-174">Na instância Windows 8.1 do aplicativo, insira um **Nome de Usuário** e **Senha** conforme mostrado na tela abaixo.</span><span class="sxs-lookup"><span data-stu-id="da013-174">In the Windows 8.1 instance of the app, enter a **Username** and **Password** as shown in the screen below.</span></span> <span data-ttu-id="da013-175">Eles devem diferir do nome de usuário e senha que você insere no Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="da013-175">It should differ from the user name and password you enter on Windows Phone.</span></span>
3. <span data-ttu-id="da013-176">Clique em **Fazer logon e registrar** e verifique se um diálogo mostra que você fez logon.</span><span class="sxs-lookup"><span data-stu-id="da013-176">Click **Log in and register** and verify a dialog shows that you have logged in.</span></span> <span data-ttu-id="da013-177">Isso também habilitará o botão **Enviar por Push** .</span><span class="sxs-lookup"><span data-stu-id="da013-177">This will also enable the **Send Push** button.</span></span>
   
    ![][14]
4. <span data-ttu-id="da013-178">Na instância do Windows Phone 8.1, insira uma cadeia de caracteres de nome de usuário nos campos **nome de usuário** e **senha** e clique em **Fazer logon e registrar**.</span><span class="sxs-lookup"><span data-stu-id="da013-178">On the Windows Phone 8.1 instance, enter a user name string in both the **Username** and **Password** fields then click **Login and register**.</span></span>
5. <span data-ttu-id="da013-179">Em seguida, no campo **Marca de Nome de Usuário do Destinatário** , insira o nome de usuário registrado no Windows 8.1.</span><span class="sxs-lookup"><span data-stu-id="da013-179">Then in the **Recipient Username Tag** field, enter the user name registered on Windows 8.1.</span></span> <span data-ttu-id="da013-180">Digite uma mensagem de notificação e clique em **Enviar notificação por push**.</span><span class="sxs-lookup"><span data-stu-id="da013-180">Enter a notification message and click **Send Push**.</span></span>
   
    ![][16]
6. <span data-ttu-id="da013-181">Apenas os dispositivos que foram registrados com o nome de usuário correspondente recebem a mensagem de notificação.</span><span class="sxs-lookup"><span data-stu-id="da013-181">Only the devices that have registered with the matching username tag receive the notification message.</span></span>
   
    ![][15]

## <a name="next-steps"></a><span data-ttu-id="da013-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="da013-182">Next Steps</span></span>
* <span data-ttu-id="da013-183">Se desejar segmentar os usuários por grupos de interesse, você poderá ler [Usar Hubs de Notificação para enviar notícias mais recentes].</span><span class="sxs-lookup"><span data-stu-id="da013-183">If you want to segment your users by interest groups, see [Use Notification Hubs to send breaking news].</span></span>
* <span data-ttu-id="da013-184">Para saber mais sobre como usar Hubs de Notificação, consulte [Diretrizes dos Hubs de Notificação].</span><span class="sxs-lookup"><span data-stu-id="da013-184">To learn more about how to use Notification Hubs, see [Notification Hubs Guidance].</span></span>

[9]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push9.png
[10]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push10.png
[11]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push11.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-ui.png
[14]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-windows-instance-username.png
[15]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-notification-received.png
[16]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-send-message.png



<!-- URLs. -->
<span data-ttu-id="da013-185">[Introdução aos Hubs de Notificação]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="da013-185">[Get started with Notification Hubs]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md</span></span>
<span data-ttu-id="da013-186">[Push Seguro]: notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="da013-186">[Secure Push]: notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md</span></span>
<span data-ttu-id="da013-187">[Usar Hubs de Notificação para enviar notícias mais recentes]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span><span class="sxs-lookup"><span data-stu-id="da013-187">[Use Notification Hubs to send breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span></span>
<span data-ttu-id="da013-188">[Diretrizes dos Hubs de Notificação]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="da013-188">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
