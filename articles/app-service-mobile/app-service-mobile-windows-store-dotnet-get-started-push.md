---
title: "Adicionar notificações por push ao seu aplicativo da UWP (Plataforma Universal do Windows) | Microsoft Docs"
description: "Saiba como usar os Aplicativos Móveis do Serviço de Aplicativo do Azure e Hubs de Notificação do Azure para enviar notificações por push para seu aplicativo da UWP (Plataforma Universal do Windows)."
services: app-service\mobile,notification-hubs
documentationcenter: windows
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6de1b9d4-bd28-43e4-8db4-94cd3b187aa3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: a14bb0320c1f6a563f766a6a0fad5cf556fe7b70
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-windows-app"></a><span data-ttu-id="cf8dd-103">Adicionar notificações por push ao seu aplicativo do Windows</span><span class="sxs-lookup"><span data-stu-id="cf8dd-103">Add push notifications to your Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="cf8dd-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="cf8dd-104">Overview</span></span>
<span data-ttu-id="cf8dd-105">Neste tutorial, você adicionará notificações por push ao projeto de [Início rápido do Windows](app-service-mobile-windows-store-dotnet-get-started.md) de forma que sempre que um registro for inserido, uma notificação por push seja enviada.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-105">In this tutorial, you add push notifications to the [Windows quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="cf8dd-106">Se você não usar o projeto baixado do início rápido do servidor, deve adicionar o pacote de extensão de notificação por push ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="cf8dd-107">Confira [Trabalhar com o servidor back-end SDK do .NET para os Aplicativos Móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <span data-ttu-id="cf8dd-108"><a name="configure-hub"></a>Configurar um novo Hub de Notificações</span><span class="sxs-lookup"><span data-stu-id="cf8dd-108"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="cf8dd-109">Registrar seu aplicativo para notificações por push</span><span class="sxs-lookup"><span data-stu-id="cf8dd-109">Register your app for push notifications</span></span>
<span data-ttu-id="cf8dd-110">Envie seu aplicativo na Windows Store e, em seguida, configure seu projeto de servidor para integrar com os Serviços de Notificação do Windows (WNS) para enviar por push.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-110">You need to submit your app to the Windows Store, then configure your server project to integrate with Windows Notification Services (WNS) to send push.</span></span>

1. <span data-ttu-id="cf8dd-111">No Gerenciador de Soluções do Visual Studio, clique com o botão direito do mouse no projeto do aplicativo da UWP, clique em **Loja** > **associar Aplicativo à Loja...**.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-111">In Visual Studio Solution Explorer, right-click the UWP app project, click **Store** > **Associate App with the Store...**.</span></span>

    ![Associar aplicativo com a Windows Store](./media/app-service-mobile-windows-store-dotnet-get-started-push/notification-hub-associate-uwp-app.png)
2. <span data-ttu-id="cf8dd-113">No assistente, clique em **Avançar**, entre com sua conta da Microsoft, digite um nome para seu aplicativo em **Reservar um novo nome de aplicativo** e clique em **Reservar**.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-113">In the wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="cf8dd-114">Depois que o registro do aplicativo for criado com êxito, selecione o novo nome do aplicativo, clique em **Avançar** e em **Associar**.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-114">After the app registration is successfully created, select the new app name, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="cf8dd-115">Isso adiciona as informações de registro necessárias da Windows Store para o manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-115">This adds the required Windows Store registration information to the application manifest.</span></span>  
4. <span data-ttu-id="cf8dd-116">Navegue até o [Centro de Desenvolvimento do Windows](https://dev.windows.com/en-us/overview), entre com sua conta da Microsoft, clique no registro do novo aplicativo em **Meus aplicativos** e expanda **Serviços** > **Notificações por push**.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-116">Navigate to the [Windows Dev Center](https://dev.windows.com/en-us/overview), sign-in with your Microsoft account, click the new app registration in **My apps**, then expand **Services** > **Push notifications**.</span></span>
5. <span data-ttu-id="cf8dd-117">Na página **Notificações por push**, clique em **Site dos Serviços ao Vivo** em **Serviços Móveis do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-117">In the **Push notifications** page, click **Live Services site** under **Microsoft Azure Mobile Services**.</span></span>
6. <span data-ttu-id="cf8dd-118">Na página de registro, anote o valor em **Segredos do aplicativo** e **SID do pacote**, que, em seguida, você usará para configurar o back-end do seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-118">In the registration page, make a note of the value under **Application secrets** and the **Package SID**, which you will next use to configure your mobile app backend.</span></span>

    ![Associar aplicativo com a Windows Store](./media/app-service-mobile-windows-store-dotnet-get-started-push/app-service-mobile-uwp-app-push-auth.png)

   > [!IMPORTANT]
   > <span data-ttu-id="cf8dd-120">O segredo do cliente e o SID do pacote são credenciais de segurança importantes.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-120">The client secret and package SID are important security credentials.</span></span> <span data-ttu-id="cf8dd-121">Não compartilhe esses valores com ninguém nem os distribua com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-121">Do not share these values with anyone or distribute them with your app.</span></span> <span data-ttu-id="cf8dd-122">A **ID do aplicativo** é usada com o segredo para configurar a autenticação da conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-122">The **Application Id** is used with the secret to configure Microsoft Account authentication.</span></span>
   >
   >

## <a name="configure-the-backend-to-send-push-notifications"></a><span data-ttu-id="cf8dd-123">Configurar o back-end para enviar notificações por push</span><span class="sxs-lookup"><span data-stu-id="cf8dd-123">Configure the backend to send push notifications</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

## <span data-ttu-id="cf8dd-124"><a id="update-service"></a>Atualizar o servidor para enviar notificações por push</span><span class="sxs-lookup"><span data-stu-id="cf8dd-124"><a id="update-service"></a>Update the server to send push notifications</span></span>
<span data-ttu-id="cf8dd-125">Use o procedimento abaixo, que corresponde ao seu tipo de projeto de back-end&mdash;, um [back-end .NET](#dotnet) ou [back-end Node.js](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="cf8dd-125">Use the procedure below that matches your backend project type&mdash;either [.NET backend](#dotnet) or [Node.js backend](#nodejs).</span></span>

### <span data-ttu-id="cf8dd-126"><a name="dotnet"></a>Projeto de back-end .NET</span><span class="sxs-lookup"><span data-stu-id="cf8dd-126"><a name="dotnet"></a>.NET backend project</span></span>
1. <span data-ttu-id="cf8dd-127">No Visual Studio, clique com o botão direito do mouse no projeto do servidor e clique em **Gerenciar Pacotes NuGet**, pesquise por Microsoft.Azure.NotificationHubs e então clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-127">In Visual Studio, right-click the server project and click **Manage NuGet Packages**, search for Microsoft.Azure.NotificationHubs, then click **Install**.</span></span> <span data-ttu-id="cf8dd-128">Isso instala a biblioteca de cliente de Hubs de notificação.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-128">This installs the Notification Hubs client library.</span></span>
2. <span data-ttu-id="cf8dd-129">Expanda **Controladores**, abra TodoItemController.cs e adicione os elementos a seguir usando instruções:</span><span class="sxs-lookup"><span data-stu-id="cf8dd-129">Expand **Controllers**, open TodoItemController.cs, and add the following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="cf8dd-130">No método **PostTodoItem**, adicione o seguinte código após a chamada para **InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="cf8dd-130">In the **PostTodoItem** method, add the following code after the call to **InsertAsync**:</span></span>

        // Get the settings for the server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get the Notification Hubs credentials for the Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create the notification hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Define a WNS payload
        var windowsToastPayload = @"<toast><visual><binding template=""ToastText01""><text id=""1"">"
                                + item.Text + @"</text></binding></visual></toast>";
        try
        {
            // Send the push notification.
            var result = await hub.SendWindowsNativeNotificationAsync(windowsToastPayload);

            // Write the success result to the logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write the failure result to the logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    <span data-ttu-id="cf8dd-131">Esse código informa o hub de notificação para enviar uma notificação por push após uma inserção de item nova.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-131">This code tells the notification hub to send a push notification after a new item is insertion.</span></span>
4. <span data-ttu-id="cf8dd-132">Republicar o projeto de servidor.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-132">Republish the server project.</span></span>

### <span data-ttu-id="cf8dd-133"><a name="nodejs"></a>Projeto de back-end Node.js</span><span class="sxs-lookup"><span data-stu-id="cf8dd-133"><a name="nodejs"></a>Node.js backend project</span></span>
1. <span data-ttu-id="cf8dd-134">Se você ainda não fez isso, [baixe o projeto de início rápido](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) ou, caso contrário, use o [editor online no Portal do Azure](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="cf8dd-134">If you haven't already done so, [download the quickstart project](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) or else use the [online editor in the Azure portal](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="cf8dd-135">Substitua o código existente no arquivo todoitem.js pelo código a seguir:</span><span class="sxs-lookup"><span data-stu-id="cf8dd-135">Replace the existing code in the todoitem.js file with the following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about the Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define the WNS payload that contains the new item Text.
        var payload = "<toast><visual><binding template=\ToastText01\><text id=\"1\">"
                                    + context.item.text + "</text></binding></visual></toast>";

        // Execute the insert.  The insert returns the results as a Promise,
        // Do the push as a post-execute action within the promise flow.
        return context.execute()
            .then(function (results) {
                // Only do the push if configured
                if (context.push) {
                    // Send a WNS native toast notification.
                    context.push.wns.sendToast(null, payload, function (error) {
                        if (error) {
                            logger.error('Error while sending push notification: ', error);
                        } else {
                            logger.info('Push notification sent successfully!');
                        }
                    });
                }
                // Don't forget to return the results from the context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;

    <span data-ttu-id="cf8dd-136">Isso envia uma notificação WNS que contém o item.text quando um novo item todo é inserido.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-136">This sends a WNS toast notification that contains the item.text when a new todo item is inserted.</span></span>
3. <span data-ttu-id="cf8dd-137">Ao editar o arquivo no seu computador local, republique o projeto do servidor.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-137">When editing the file on your local computer, republish the server project.</span></span>

## <span data-ttu-id="cf8dd-138"><a id="update-app"></a>Adicionar notificações de push para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="cf8dd-138"><a id="update-app"></a>Add push notifications to your app</span></span>
<span data-ttu-id="cf8dd-139">Em seguida, seu aplicativo deve se registrar para notificações por push na inicialização.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-139">Next, your app must register for push notifications on start-up.</span></span> <span data-ttu-id="cf8dd-140">Quando você já tiver habilitado a autenticação, certifique-se de que o usuário entre antes de tentar se registrar para receber notificações por push.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-140">When you have already enabled authentication, make sure that the user signs-in before trying to register for push notifications.</span></span>

1. <span data-ttu-id="cf8dd-141">Abra o arquivo de projeto **App.xaml.cs** e adicione as instruções `using` a seguir:</span><span class="sxs-lookup"><span data-stu-id="cf8dd-141">Open the **App.xaml.cs** project file and add the following `using` statements:</span></span>

        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
2. <span data-ttu-id="cf8dd-142">No mesmo arquivo, adicione a seguinte definição de método **InitNotificationsAsync** à classe de **aplicativo**:</span><span class="sxs-lookup"><span data-stu-id="cf8dd-142">In the same file, add the following **InitNotificationsAsync** method definition to the **App** class:</span></span>

        private async Task InitNotificationsAsync()
        {
            // Get a channel URI from WNS.
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            // Register the channel URI with Notification Hubs.
            await App.MobileService.GetPush().RegisterAsync(channel.Uri);
        }

    <span data-ttu-id="cf8dd-143">Esse código recupera o ChannelURI do aplicativo de WNS e registra esse ChannelURI com seu Aplicativo Móvel do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-143">This code retrieves the ChannelURI for the app from WNS, and then registers that ChannelURI with your App Service Mobile App.</span></span>
3. <span data-ttu-id="cf8dd-144">Na parte superior do manipulador de eventos **OnLaunched** no **App.xaml.cs**, adicione o modificador **async** à definição do método e adicione a seguinte chamada ao novo método **InitNotificationsAsync**, como mostrado no seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="cf8dd-144">At the top of the **OnLaunched** event handler in **App.xaml.cs**, add the **async** modifier to the method definition and add the following call to the new **InitNotificationsAsync** method, as in the following example:</span></span>

        protected async override void OnLaunched(LaunchActivatedEventArgs e)
        {
            await InitNotificationsAsync();

            // ...
        }

    <span data-ttu-id="cf8dd-145">Isso garante que o ChannelURI de curta duração seja registrado sempre que o aplicativo for iniciado.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-145">This guarantees that the short-lived ChannelURI is registered each time the application is launched.</span></span>
4. <span data-ttu-id="cf8dd-146">Recompile seu projeto de aplicativo da UWP.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-146">Rebuild your UWP app project.</span></span> <span data-ttu-id="cf8dd-147">Seu aplicativo agora está pronto para receber notificações do sistema.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-147">Your app is now ready to receive toast notifications.</span></span>

## <span data-ttu-id="cf8dd-148"><a id="test"></a>Testar notificações por push no seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="cf8dd-148"><a id="test"></a>Test push notifications in your app</span></span>
[!INCLUDE [app-service-mobile-windows-universal-test-push](../../includes/app-service-mobile-windows-universal-test-push.md)]

## <span data-ttu-id="cf8dd-149"><a id="more"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cf8dd-149"><a id="more"></a>Next steps</span></span>
<span data-ttu-id="cf8dd-150">Saiba mais sobre as notificações por push:</span><span class="sxs-lookup"><span data-stu-id="cf8dd-150">Learn more about push notifications:</span></span>

* [<span data-ttu-id="cf8dd-151">Como usar o cliente gerenciado para aplicativos móveis do Azure</span><span class="sxs-lookup"><span data-stu-id="cf8dd-151">How to use the managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications)  
  <span data-ttu-id="cf8dd-152">modelos oferecem flexibilidade para enviar envios de plataforma cruzada e pushes localizados.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-152">Templates give you flexibility to send cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="cf8dd-153">Saiba como registrar modelos.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-153">Learn how to register templates.</span></span>
* [<span data-ttu-id="cf8dd-154">Diagnosticar problemas com notificações por push</span><span class="sxs-lookup"><span data-stu-id="cf8dd-154">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="cf8dd-155">há vários motivos por que as notificações podem ser abandonadas ou não irem terminar nos dispositivos.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-155">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="cf8dd-156">Este tópico mostra como analisar e descobrir a causa de falhas de notificação por push.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-156">This topic shows you how to analyze and figure out the root cause of push notification failures.</span></span>

<span data-ttu-id="cf8dd-157">Considere a possibilidade de prosseguir com um dos seguintes tutoriais:</span><span class="sxs-lookup"><span data-stu-id="cf8dd-157">Consider continuing on to one of the following tutorials:</span></span>

* [<span data-ttu-id="cf8dd-158">Adicionar autenticação ao seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="cf8dd-158">Add authentication to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="cf8dd-159">Saiba como autenticar usuários de seu aplicativo com um provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-159">Learn how to authenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="cf8dd-160">Habilitar sincronização offline para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="cf8dd-160">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="cf8dd-161">Saiba como adicionar suporte offline ao seu aplicativo usando um back-end de Aplicativo Móvel.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-161">Learn how to add offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="cf8dd-162">Sincronização offline permite que os usuários finais interajam com um aplicativo móvel, &mdash;exibindo, adicionando ou modificando dados&mdash;, mesmo quando não há conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="cf8dd-162">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

<!-- Images. -->
