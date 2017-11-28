---
title: "aplicativo do Windows UWP (plataforma Universal) do aaaAdd push notificações tooyour | Microsoft Docs"
description: "Saiba como toouse aplicativos de celular do serviço de aplicativo do Azure e Hubs de notificação do Azure toosend aplicativo por push notificações tooyour Windows UWP (plataforma Universal)."
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
ms.openlocfilehash: 378ce59cab974830c0a3801108b24b30a21ae5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-windows-app"></a><span data-ttu-id="d8978-103">Adicionar aplicativo do Windows de tooyour de notificações de push</span><span class="sxs-lookup"><span data-stu-id="d8978-103">Add push notifications tooyour Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="d8978-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d8978-104">Overview</span></span>
<span data-ttu-id="d8978-105">Neste tutorial, você adiciona toohello de notificações por push [início rápido do Windows](app-service-mobile-windows-store-dotnet-get-started.md) de projeto para que uma notificação por push seja enviada toohello dispositivo toda vez que um registro é inserido.</span><span class="sxs-lookup"><span data-stu-id="d8978-105">In this tutorial, you add push notifications toohello [Windows quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="d8978-106">Se você não usar Olá baixar o projeto de servidor de início rápido, será necessário Olá o pacote de extensão de notificação por push.</span><span class="sxs-lookup"><span data-stu-id="d8978-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="d8978-107">Consulte [funcionam com o servidor de back-end .NET Olá SDK para aplicativos móveis do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="d8978-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <span data-ttu-id="d8978-108"><a name="configure-hub"></a>Configurar um novo Hub de Notificações</span><span class="sxs-lookup"><span data-stu-id="d8978-108"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="d8978-109">Registrar seu aplicativo para notificações por push</span><span class="sxs-lookup"><span data-stu-id="d8978-109">Register your app for push notifications</span></span>
<span data-ttu-id="d8978-110">Você precisa toosubmit toohello seu aplicativo da Windows Store e configurar sua toointegrate de projeto de servidor com serviços de notificação do Windows (WNS) toosend push.</span><span class="sxs-lookup"><span data-stu-id="d8978-110">You need toosubmit your app toohello Windows Store, then configure your server project toointegrate with Windows Notification Services (WNS) toosend push.</span></span>

1. <span data-ttu-id="d8978-111">No Visual Studio Solution Explorer, projeto de aplicativo UWP de saudação com o botão direito, clique em **repositório** > **associar aplicativo hello repositório...** .</span><span class="sxs-lookup"><span data-stu-id="d8978-111">In Visual Studio Solution Explorer, right-click hello UWP app project, click **Store** > **Associate App with hello Store...**.</span></span>

    ![Associar aplicativo com a Windows Store](./media/app-service-mobile-windows-store-dotnet-get-started-push/notification-hub-associate-uwp-app.png)
2. <span data-ttu-id="d8978-113">No Assistente de saudação, clique em **próximo**, entrar com sua conta da Microsoft, digite um nome para seu aplicativo na **reservar um novo nome de aplicativo**, em seguida, clique em **reserva**.</span><span class="sxs-lookup"><span data-stu-id="d8978-113">In hello wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="d8978-114">Após o registro do aplicativo hello novo nome de aplicativo criado com êxito, selecione hello, clique em **próximo**e, em seguida, clique em **associar**.</span><span class="sxs-lookup"><span data-stu-id="d8978-114">After hello app registration is successfully created, select hello new app name, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="d8978-115">Isso adiciona o manifesto do aplicativo hello necessárias da Windows Store registro informações toohello.</span><span class="sxs-lookup"><span data-stu-id="d8978-115">This adds hello required Windows Store registration information toohello application manifest.</span></span>  
4. <span data-ttu-id="d8978-116">Navegue toohello [Centro de desenvolvimento do Windows](https://dev.windows.com/en-us/overview), entrar com sua conta da Microsoft, clique em novo registro de aplicativo hello em **meus aplicativos**, em seguida, expanda **serviços**  >  **Notificações por push**.</span><span class="sxs-lookup"><span data-stu-id="d8978-116">Navigate toohello [Windows Dev Center](https://dev.windows.com/en-us/overview), sign-in with your Microsoft account, click hello new app registration in **My apps**, then expand **Services** > **Push notifications**.</span></span>
5. <span data-ttu-id="d8978-117">Em Olá **notificações por Push** , clique em **site de serviços do Live** em **serviços móveis do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="d8978-117">In hello **Push notifications** page, click **Live Services site** under **Microsoft Azure Mobile Services**.</span></span>
6. <span data-ttu-id="d8978-118">Na página de registro hello, tome nota do valor de saudação em **segredos do aplicativo** e hello **SID do pacote**, que é seguida usará tooconfigure seu back-end do aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="d8978-118">In hello registration page, make a note of hello value under **Application secrets** and hello **Package SID**, which you will next use tooconfigure your mobile app backend.</span></span>

    ![Associar aplicativo com a Windows Store](./media/app-service-mobile-windows-store-dotnet-get-started-push/app-service-mobile-uwp-app-push-auth.png)

   > [!IMPORTANT]
   > <span data-ttu-id="d8978-120">SID de pacote e segredo de saudação do cliente são credenciais de segurança importantes.</span><span class="sxs-lookup"><span data-stu-id="d8978-120">hello client secret and package SID are important security credentials.</span></span> <span data-ttu-id="d8978-121">Não compartilhe esses valores com ninguém nem os distribua com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d8978-121">Do not share these values with anyone or distribute them with your app.</span></span> <span data-ttu-id="d8978-122">Olá **Id do aplicativo** é usado com a autenticação do hello secreta tooconfigure Account da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d8978-122">hello **Application Id** is used with hello secret tooconfigure Microsoft Account authentication.</span></span>
   >
   >

## <a name="configure-hello-backend-toosend-push-notifications"></a><span data-ttu-id="d8978-123">Configurar notificações por push do hello back-end toosend</span><span class="sxs-lookup"><span data-stu-id="d8978-123">Configure hello backend toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

## <span data-ttu-id="d8978-124"><a id="update-service"></a>Olá server toosend push notificações de atualização</span><span class="sxs-lookup"><span data-stu-id="d8978-124"><a id="update-service"></a>Update hello server toosend push notifications</span></span>
<span data-ttu-id="d8978-125">Use o procedimento de saudação abaixo que corresponde ao tipo de projeto de back-end&mdash;ou [back-end .NET](#dotnet) ou [Node. js back-end](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="d8978-125">Use hello procedure below that matches your backend project type&mdash;either [.NET backend](#dotnet) or [Node.js backend](#nodejs).</span></span>

### <span data-ttu-id="d8978-126"><a name="dotnet"></a>Projeto de back-end .NET</span><span class="sxs-lookup"><span data-stu-id="d8978-126"><a name="dotnet"></a>.NET backend project</span></span>
1. <span data-ttu-id="d8978-127">No Visual Studio, clique com botão direito Olá servidor e clique em **gerenciar pacotes NuGet**, procure Microsoft.Azure.NotificationHubs e clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="d8978-127">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**, search for Microsoft.Azure.NotificationHubs, then click **Install**.</span></span> <span data-ttu-id="d8978-128">Isso instala a biblioteca de cliente Olá Hubs de notificação.</span><span class="sxs-lookup"><span data-stu-id="d8978-128">This installs hello Notification Hubs client library.</span></span>
2. <span data-ttu-id="d8978-129">Expanda **controladores**, abra TodoItemController.cs e adicione Olá seguinte usando instruções:</span><span class="sxs-lookup"><span data-stu-id="d8978-129">Expand **Controllers**, open TodoItemController.cs, and add hello following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="d8978-130">Em Olá **PostTodoItem** método, adicione Olá código a seguir após a chamada de saudação muito**InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="d8978-130">In hello **PostTodoItem** method, add hello following code after hello call too**InsertAsync**:</span></span>

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create hello notification hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Define a WNS payload
        var windowsToastPayload = @"<toast><visual><binding template=""ToastText01""><text id=""1"">"
                                + item.Text + @"</text></binding></visual></toast>";
        try
        {
            // Send hello push notification.
            var result = await hub.SendWindowsNativeNotificationAsync(windowsToastPayload);

            // Write hello success result toohello logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write hello failure result toohello logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    <span data-ttu-id="d8978-131">Esse código informa toosend de hub de notificação Olá uma notificação por push após um novo item de inserção.</span><span class="sxs-lookup"><span data-stu-id="d8978-131">This code tells hello notification hub toosend a push notification after a new item is insertion.</span></span>
4. <span data-ttu-id="d8978-132">Republicar o projeto do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8978-132">Republish hello server project.</span></span>

### <span data-ttu-id="d8978-133"><a name="nodejs"></a>Projeto de back-end Node.js</span><span class="sxs-lookup"><span data-stu-id="d8978-133"><a name="nodejs"></a>Node.js backend project</span></span>
1. <span data-ttu-id="d8978-134">Se você ainda não fez isso, [baixar o projeto de início rápido de saudação](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) ou use outro Olá [editor online no portal do Azure de saudação](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="d8978-134">If you haven't already done so, [download hello quickstart project](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) or else use hello [online editor in hello Azure portal](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="d8978-135">Substitua o código existente de saudação no arquivo de todoitem.js Olá com os seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="d8978-135">Replace hello existing code in hello todoitem.js file with hello following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello WNS payload that contains hello new item Text.
        var payload = "<toast><visual><binding template=\ToastText01\><text id=\"1\">"
                                    + context.item.text + "</text></binding></visual></toast>";

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
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
                // Don't forget tooreturn hello results from hello context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;

    <span data-ttu-id="d8978-136">Envia uma notificação WNS do sistema que contém item.text hello quando um novo item de tarefas é inserido.</span><span class="sxs-lookup"><span data-stu-id="d8978-136">This sends a WNS toast notification that contains hello item.text when a new todo item is inserted.</span></span>
3. <span data-ttu-id="d8978-137">Ao editar o arquivo hello no computador local, republicar o projeto do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8978-137">When editing hello file on your local computer, republish hello server project.</span></span>

## <span data-ttu-id="d8978-138"><a id="update-app"></a>Adicionar aplicativo de tooyour de notificações por push</span><span class="sxs-lookup"><span data-stu-id="d8978-138"><a id="update-app"></a>Add push notifications tooyour app</span></span>
<span data-ttu-id="d8978-139">Em seguida, seu aplicativo deve se registrar para notificações por push na inicialização.</span><span class="sxs-lookup"><span data-stu-id="d8978-139">Next, your app must register for push notifications on start-up.</span></span> <span data-ttu-id="d8978-140">Quando você já habilitou a autenticação, certifique-se de que o usuário Olá entrar antes de tentar tooregister para notificações por push.</span><span class="sxs-lookup"><span data-stu-id="d8978-140">When you have already enabled authentication, make sure that hello user signs-in before trying tooregister for push notifications.</span></span>

1. <span data-ttu-id="d8978-141">Olá abrir **App.xaml.cs** arquivo de projeto e adicione o seguinte Olá `using` instruções:</span><span class="sxs-lookup"><span data-stu-id="d8978-141">Open hello **App.xaml.cs** project file and add hello following `using` statements:</span></span>

        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
2. <span data-ttu-id="d8978-142">Em Olá mesmo arquivo, adicione o seguinte Olá **InitNotificationsAsync** toohello de definição de método **aplicativo** classe:</span><span class="sxs-lookup"><span data-stu-id="d8978-142">In hello same file, add hello following **InitNotificationsAsync** method definition toohello **App** class:</span></span>

        private async Task InitNotificationsAsync()
        {
            // Get a channel URI from WNS.
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            // Register hello channel URI with Notification Hubs.
            await App.MobileService.GetPush().RegisterAsync(channel.Uri);
        }

    <span data-ttu-id="d8978-143">Esse código recupera Olá ChannelURI para o aplicativo de saudação do WNS e registra esse ChannelURI com seu aplicativo do aplicativo do serviço móvel.</span><span class="sxs-lookup"><span data-stu-id="d8978-143">This code retrieves hello ChannelURI for hello app from WNS, and then registers that ChannelURI with your App Service Mobile App.</span></span>
3. <span data-ttu-id="d8978-144">Na parte superior de saudação do hello **OnLaunched** manipulador de eventos **App.xaml.cs**, adicionar Olá **async** definição de método modificador toohello e adicione a seguinte Olá chamar novotoohello **InitNotificationsAsync** método, como no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="d8978-144">At hello top of hello **OnLaunched** event handler in **App.xaml.cs**, add hello **async** modifier toohello method definition and add hello following call toohello new **InitNotificationsAsync** method, as in hello following example:</span></span>

        protected async override void OnLaunched(LaunchActivatedEventArgs e)
        {
            await InitNotificationsAsync();

            // ...
        }

    <span data-ttu-id="d8978-145">Isso garante que Olá que channeluri curta duração é registrado sempre que o aplicativo hello é iniciado.</span><span class="sxs-lookup"><span data-stu-id="d8978-145">This guarantees that hello short-lived ChannelURI is registered each time hello application is launched.</span></span>
4. <span data-ttu-id="d8978-146">Recompile seu projeto de aplicativo da UWP.</span><span class="sxs-lookup"><span data-stu-id="d8978-146">Rebuild your UWP app project.</span></span> <span data-ttu-id="d8978-147">Seu aplicativo agora está pronto tooreceive notificações do sistema.</span><span class="sxs-lookup"><span data-stu-id="d8978-147">Your app is now ready tooreceive toast notifications.</span></span>

## <span data-ttu-id="d8978-148"><a id="test"></a>Testar notificações por push no seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="d8978-148"><a id="test"></a>Test push notifications in your app</span></span>
[!INCLUDE [app-service-mobile-windows-universal-test-push](../../includes/app-service-mobile-windows-universal-test-push.md)]

## <span data-ttu-id="d8978-149"><a id="more"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d8978-149"><a id="more"></a>Next steps</span></span>
<span data-ttu-id="d8978-150">Saiba mais sobre as notificações por push:</span><span class="sxs-lookup"><span data-stu-id="d8978-150">Learn more about push notifications:</span></span>

* [<span data-ttu-id="d8978-151">Como toouse Olá gerenciada do cliente para aplicativos móveis do Azure</span><span class="sxs-lookup"><span data-stu-id="d8978-151">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications)  
  <span data-ttu-id="d8978-152">Modelos oferecem envios de plataforma cruzada toosend flexibilidade e envios localizados.</span><span class="sxs-lookup"><span data-stu-id="d8978-152">Templates give you flexibility toosend cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="d8978-153">Saiba como tooregister modelos.</span><span class="sxs-lookup"><span data-stu-id="d8978-153">Learn how tooregister templates.</span></span>
* [<span data-ttu-id="d8978-154">Diagnosticar problemas com notificações por push</span><span class="sxs-lookup"><span data-stu-id="d8978-154">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="d8978-155">há vários motivos por que as notificações podem ser abandonadas ou não irem terminar nos dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d8978-155">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="d8978-156">Este tópico mostra como tooanalyze e descobrir raiz Olá causam falhas de notificação por push.</span><span class="sxs-lookup"><span data-stu-id="d8978-156">This topic shows you how tooanalyze and figure out hello root cause of push notification failures.</span></span>

<span data-ttu-id="d8978-157">Considere a possibilidade de continuar tooone de saudação tutoriais a seguir:</span><span class="sxs-lookup"><span data-stu-id="d8978-157">Consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="d8978-158">Adicionar autenticação tooyour aplicativo</span><span class="sxs-lookup"><span data-stu-id="d8978-158">Add authentication tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="d8978-159">Saiba como tooauthenticate usuários do seu aplicativo com um provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="d8978-159">Learn how tooauthenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="d8978-160">Habilitar sincronização offline para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="d8978-160">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="d8978-161">Saiba como off-line tooadd dão suporte ao seu aplicativo usar um back-end do aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="d8978-161">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="d8978-162">Sincronização offline permite que os usuários finais toointeract com um aplicativo móvel&mdash;exibindo, adicionando ou modificando dados&mdash;mesmo quando não há nenhuma conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="d8978-162">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

<!-- Images. -->
