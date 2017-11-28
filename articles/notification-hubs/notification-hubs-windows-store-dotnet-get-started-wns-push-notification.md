---
title: "aaaGet de Introdução ao Azure notificação Hubs para aplicativos universais do Windows plataforma | Microsoft Docs"
description: "Neste tutorial, você aprenderá como toouse Hubs de notificação do Azure toopush notificações tooa aplicativo da plataforma Universal do Windows."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: erikre
ms.assetid: cf307cf3-8c58-4628-9c63-8751e6a0ef43
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 11056842d205522ed493dc61c76ecf78ebb5a363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-notification-hubs-for-windows-universal-platform-apps"></a><span data-ttu-id="c0952-103">Introdução aos Hubs de Notificação para aplicativos da Plataforma Universal do Windows</span><span class="sxs-lookup"><span data-stu-id="c0952-103">Getting started with Notification Hubs for Windows Universal Platform Apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="c0952-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="c0952-104">Overview</span></span>
<span data-ttu-id="c0952-105">Este tutorial mostra como aplicativo de Windows UWP (plataforma Universal) tooa notificações por push de toouse toosend de Hubs de notificação do Azure.</span><span class="sxs-lookup"><span data-stu-id="c0952-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Universal Windows Platform (UWP) app.</span></span>

<span data-ttu-id="c0952-106">Neste tutorial, você deve criar um aplicativo da Windows Store em branco que recebe notificações por push usando Olá Windows Push Notification Service (WNS).</span><span class="sxs-lookup"><span data-stu-id="c0952-106">In this tutorial, you create a blank Windows Store app that receives push notifications by using hello Windows Push Notification Service (WNS).</span></span> <span data-ttu-id="c0952-107">Quando você terminar, você será capaz de toouse sua toobroadcast de hub de notificação por push notificações tooall Olá a dispositivos que executam seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c0952-107">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c0952-108">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="c0952-108">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="c0952-109">código de saudação concluído para este tutorial pode ser encontrado no GitHub [aqui](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).</span><span class="sxs-lookup"><span data-stu-id="c0952-109">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0952-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c0952-110">Prerequisites</span></span>
<span data-ttu-id="c0952-111">Este tutorial requer o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="c0952-111">This tutorial requires hello following:</span></span>

* <span data-ttu-id="c0952-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) ou posterior</span><span class="sxs-lookup"><span data-stu-id="c0952-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) or later</span></span>
* [<span data-ttu-id="c0952-113">Ferramentas de Desenvolvimento de Aplicativos Universais do Windows instaladas</span><span class="sxs-lookup"><span data-stu-id="c0952-113">Universal Windows App Development Tools installed</span></span>](https://msdn.microsoft.com/windows/uwp/get-started/get-set-up)
* <span data-ttu-id="c0952-114">Uma conta ativa do Azure </span><span class="sxs-lookup"><span data-stu-id="c0952-114">An active Azure account</span></span> <br/><span data-ttu-id="c0952-115">Se não tiver uma conta, você poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="c0952-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c0952-116">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="c0952-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).</span></span>
* <span data-ttu-id="c0952-117">Uma conta ativa da Windows Store</span><span class="sxs-lookup"><span data-stu-id="c0952-117">An active Windows Store account</span></span>

<span data-ttu-id="c0952-118">A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais sobre Hubs de Notificação para aplicativos da Plataforma Universal do Windows.</span><span class="sxs-lookup"><span data-stu-id="c0952-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Universal Platform apps.</span></span>

## <a name="register-your-app-for-hello-windows-store"></a><span data-ttu-id="c0952-119">Registrar seu aplicativo para saudação da Windows Store</span><span class="sxs-lookup"><span data-stu-id="c0952-119">Register your app for hello Windows Store</span></span>
<span data-ttu-id="c0952-120">aplicativos de tooUWP de notificações de push toosend, você deve associar toohello seu aplicativo da Windows Store.</span><span class="sxs-lookup"><span data-stu-id="c0952-120">toosend push notifications tooUWP apps, you must associate your app toohello Windows Store.</span></span> <span data-ttu-id="c0952-121">Em seguida, você deve configurar sua toointegrate de hub de notificação com WNS.</span><span class="sxs-lookup"><span data-stu-id="c0952-121">You must then configure your notification hub toointegrate with WNS.</span></span>

1. <span data-ttu-id="c0952-122">Se você não estiver registrado seu aplicativo, navegar toohello [Centro de desenvolvimento do Windows](https://dev.windows.com/overview), entrar com sua conta da Microsoft e, em seguida, clique em **criar um novo aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="c0952-122">If you have not already registered your app, navigate toohello [Windows Dev Center](https://dev.windows.com/overview), sign in with your Microsoft account, and then click **Create a new app**.</span></span>

2. <span data-ttu-id="c0952-123">Digite um nome para seu aplicativo e clique em **Reservar nome do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="c0952-123">Type a name for your app and click **Reserve app name**.</span></span> <span data-ttu-id="c0952-124">Isso cria um novo registro da Windows Store para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c0952-124">This creates a new Windows Store registration for your app.</span></span>

3. <span data-ttu-id="c0952-125">No Visual Studio, crie um novo projeto do Visual c# aplicativos da Windows Store usando Olá Universal do Windows **aplicativo em branco** modelo e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="c0952-125">In Visual Studio, create a new Visual C# Store Apps project by using hello Windows Universal **Blank App** template and click **OK**.</span></span>

4. <span data-ttu-id="c0952-126">Aceite os padrões de saudação para destino hello e versões de plataforma mínimas.</span><span class="sxs-lookup"><span data-stu-id="c0952-126">Accept hello defaults for hello target and minimum platform versions.</span></span>

5. <span data-ttu-id="c0952-127">No Gerenciador de soluções, projeto de aplicativo da Windows Store com o botão direito hello, clique em **repositório**e, em seguida, clique em **associar aplicativo hello repositório...** . Olá **associar seu aplicativo com hello da Windows Store** assistente é exibido.</span><span class="sxs-lookup"><span data-stu-id="c0952-127">In Solution Explorer, right-click hello Windows Store app project, click **Store**, and then click **Associate App with hello Store...**. hello **Associate Your App with hello Windows Store** wizard appears.</span></span>

6. <span data-ttu-id="c0952-128">No Assistente de saudação, entre com sua conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c0952-128">In hello wizard, sign in with your Microsoft account.</span></span>

7. <span data-ttu-id="c0952-129">Clique em aplicativo hello que você registrou na etapa 2, clique em **próximo**e, em seguida, clique em **associar**.</span><span class="sxs-lookup"><span data-stu-id="c0952-129">Click hello app that you registered in step 2, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="c0952-130">Isso adiciona o manifesto do aplicativo hello necessárias da Windows Store registro informações toohello.</span><span class="sxs-lookup"><span data-stu-id="c0952-130">This adds hello required Windows Store registration information toohello application manifest.</span></span>

8. <span data-ttu-id="c0952-131">Em Olá [Centro de desenvolvimento do Windows](http://dev.windows.com/overview) para seu novo aplicativo, clique em **serviços**, clique em **notificações por Push**e, em seguida, clique em **WNS/MPNS**.</span><span class="sxs-lookup"><span data-stu-id="c0952-131">Back on hello [Windows Dev Center](http://dev.windows.com/overview) page for your new app, click **Services**, click **Push notifications**, and then click **WNS/MPNS**.</span></span>

9. <span data-ttu-id="c0952-132">Clique em **Nova Notificação**.</span><span class="sxs-lookup"><span data-stu-id="c0952-132">Click **New Notification**.</span></span>

10. <span data-ttu-id="c0952-133">Clique no modelo **Em branco (Notificação do sistema)** e depois clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c0952-133">Click **Blank (Toast)** template and then click **OK**.</span></span>

11. <span data-ttu-id="c0952-134">Insira um **Nome** para a notificação e uma mensagem de **Contexto** Visual.</span><span class="sxs-lookup"><span data-stu-id="c0952-134">Enter a notification **Name** and Visual **Context** message.</span></span> <span data-ttu-id="c0952-135">Em seguida, clique em **Salvar como rascunho**.</span><span class="sxs-lookup"><span data-stu-id="c0952-135">Then click **Save as draft**.</span></span>

12. <span data-ttu-id="c0952-136">Navegue toohello [Portal de registro de aplicativo](http://apps.dev.microsoft.com) e faça logon.</span><span class="sxs-lookup"><span data-stu-id="c0952-136">Navigate toohello [Application Registration Portal](http://apps.dev.microsoft.com) and log in.</span></span>

13. <span data-ttu-id="c0952-137">Clique no nome de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c0952-137">Click on your application name.</span></span> <span data-ttu-id="c0952-138">Anote Olá **segredo do aplicativo** senha e hello **identificador de segurança (SID) do pacote** localizado em Olá **da Windows Store** configurações da plataforma.</span><span class="sxs-lookup"><span data-stu-id="c0952-138">Make a note of hello **Application Secret** password and hello **Package security identifier (SID)** located in hello **Windows Store** platform settings.</span></span>

     > [AZURE.WARNING]
    <span data-ttu-id="c0952-139">SID de pacote e segredo do aplicativo Hello são credenciais de segurança importantes.</span><span class="sxs-lookup"><span data-stu-id="c0952-139">hello application secret and package SID are important security credentials.</span></span> <span data-ttu-id="c0952-140">Não compartilhe esses valores com ninguém nem os distribua com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c0952-140">Do not share these values with anyone or distribute them with your app.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="c0952-141">Configurar seu Hub de Notificação</span><span class="sxs-lookup"><span data-stu-id="c0952-141">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="c0952-142">Selecione Olá <b>Notification Services</b> opção e hello <b>Windows (WNS)</b> opção.</span><span class="sxs-lookup"><span data-stu-id="c0952-142">Select hello <b>Notification Services</b> option and hello <b>Windows (WNS)</b> option.</span></span> <span data-ttu-id="c0952-143">Em seguida, digite Olá <b>segredo do aplicativo</b> senha no hello <b>chave de segurança</b> campo.</span><span class="sxs-lookup"><span data-stu-id="c0952-143">Then enter hello <b>Application secret</b> password in hello <b>Security Key</b> field.</span></span> <span data-ttu-id="c0952-144">Insira seu <b>SID do pacote</b> valor que você obteve do WNS na seção anterior hello e, em seguida, clique em <b>salvar</b>.</span><span class="sxs-lookup"><span data-stu-id="c0952-144">Enter your <b>Package SID</b> value that you obtained from WNS in hello previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>

&emsp;&emsp;![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-configure-wns.png)

<span data-ttu-id="c0952-145">O hub de notificação agora é toowork configurado com WNS, e ter Olá tooregister de cadeias de caracteres de conexão de seu aplicativo e enviar notificações.</span><span class="sxs-lookup"><span data-stu-id="c0952-145">Your notification hub is now configured toowork with WNS, and you have hello connection strings tooregister your app and send notifications.</span></span>

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="c0952-146">Conecte-se o seu hub de notificação do aplicativo toohello</span><span class="sxs-lookup"><span data-stu-id="c0952-146">Connect your app toohello notification hub</span></span>
1. <span data-ttu-id="c0952-147">No Visual Studio, clique com botão direito solução hello e, em seguida, clique em **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="c0952-147">In Visual Studio, right-click hello solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="c0952-148">Isso exibe o saudação **gerenciar pacotes NuGet** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c0952-148">This displays hello **Manage NuGet Packages** dialog box.</span></span>
2. <span data-ttu-id="c0952-149">Procurar `WindowsAzure.Messaging.Managed` e clique em **instalar**e aceite os termos de uso do hello.</span><span class="sxs-lookup"><span data-stu-id="c0952-149">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and accept hello terms of use.</span></span>
   
    ![][20]
   
    <span data-ttu-id="c0952-150">Isso baixa, instala e adiciona uma biblioteca da referência toohello mensagens do Azure para Windows usando Olá <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">pacote WindowsAzure.Messaging.Managed NuGet</a>.</span><span class="sxs-lookup"><span data-stu-id="c0952-150">This downloads, installs, and adds a reference toohello Azure Messaging library for Windows by using hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
3. <span data-ttu-id="c0952-151">Abrir o arquivo de projeto do hello App.xaml.cs e adicione o seguinte Olá `using` instruções.</span><span class="sxs-lookup"><span data-stu-id="c0952-151">Open hello App.xaml.cs project file and add hello following `using` statements.</span></span> 
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.UI.Popups;
4. <span data-ttu-id="c0952-152">Também no App.xaml.cs, adicione a seguir Olá **InitNotificationsAsync** toohello de definição de método **aplicativo** classe:</span><span class="sxs-lookup"><span data-stu-id="c0952-152">Also in App.xaml.cs, add hello following **InitNotificationsAsync** method definition toohello **App** class:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("< your hub name>", "<Your DefaultListenSharedAccessSignature connection string>");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
   
        }
   
    <span data-ttu-id="c0952-153">Esse código recupera o URI do canal Olá para o aplicativo de saudação do WNS e, em seguida, registra esse URI de canal com seu hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="c0952-153">This code retrieves hello channel URI for hello app from WNS, and then registers that channel URI with your notification hub.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c0952-154">Verifique se tooreplace Olá espaço reservado de "o nome do hub" com o nome de saudação do hub de notificação de saudação que aparece no hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c0952-154">Make sure tooreplace hello "your hub name" placeholder with hello name of hello notification hub that appears in hello Azure Portal.</span></span> <span data-ttu-id="c0952-155">Também substitua espaço reservado de cadeia de caracteres de conexão Olá Olá **DefaultListenSharedAccessSignature** cadeia de caracteres de conexão que você obteve da saudação **políticas de acesso** página do Hub de notificação em um seção anterior.</span><span class="sxs-lookup"><span data-stu-id="c0952-155">Also replace hello connection string placeholder with hello **DefaultListenSharedAccessSignature** connection string that you obtained from hello **Access Polices** page of your Notification Hub in a previous section.</span></span>
   > 
   > 
5. <span data-ttu-id="c0952-156">Na parte superior de saudação do hello **OnLaunched** manipulador de eventos em App.xaml.cs, adicionar Olá chamada toohello novos a seguir **InitNotificationsAsync** método:</span><span class="sxs-lookup"><span data-stu-id="c0952-156">At hello top of hello **OnLaunched** event handler in App.xaml.cs, add hello following call toohello new **InitNotificationsAsync** method:</span></span>
   
        InitNotificationsAsync();
   
    <span data-ttu-id="c0952-157">Isso garante que esse canal Olá que URI é registrado no hub de notificação, que cada aplicativo de saudação do tempo é iniciado.</span><span class="sxs-lookup"><span data-stu-id="c0952-157">This guarantees that hello channel URI is registered in your notification hub each time hello application is launched.</span></span>
6. <span data-ttu-id="c0952-158">Olá pressione **F5** toorun chave Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c0952-158">Press hello **F5** key toorun hello app.</span></span> <span data-ttu-id="c0952-159">Uma caixa de diálogo pop-up que contém a chave de registro de saudação é exibida.</span><span class="sxs-lookup"><span data-stu-id="c0952-159">A pop-up dialog that contains hello registration key is displayed.</span></span>

<span data-ttu-id="c0952-160">Seu aplicativo agora está pronto tooreceive notificações do sistema.</span><span class="sxs-lookup"><span data-stu-id="c0952-160">Your app is now ready tooreceive toast notifications.</span></span>

## <a name="send-notifications"></a><span data-ttu-id="c0952-161">Enviar notificações</span><span class="sxs-lookup"><span data-stu-id="c0952-161">Send notifications</span></span>
<span data-ttu-id="c0952-162">Você pode testar rapidamente a receber notificações em seu aplicativo pelo envio de notificações em Olá [Portal do Azure](https://portal.azure.com/) usando Olá **teste enviar** botão no hub de notificação hello, conforme mostrado na tela hello abaixo.</span><span class="sxs-lookup"><span data-stu-id="c0952-162">You can quickly test receiving notifications in your app by sending notifications in hello [Azure Portal](https://portal.azure.com/) using hello **Test Send** button on hello notification hub, as shown in hello screen below.</span></span>

![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-test-send-wns.png)

<span data-ttu-id="c0952-163">Notificações por push normalmente são enviadas em um serviço de back-end como Serviços Móveis ou ASP.NET usando uma biblioteca compatível.</span><span class="sxs-lookup"><span data-stu-id="c0952-163">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="c0952-164">Você também pode usar o hello API REST diretamente as mensagens de notificação de toosend se uma biblioteca não está disponível para o back-end.</span><span class="sxs-lookup"><span data-stu-id="c0952-164">You can also use hello REST API directly toosend notification messages if a library is not available for your back-end.</span></span> 

<span data-ttu-id="c0952-165">Neste tutorial, nós manter a simplicidade e demonstrar a testar seu aplicativo de cliente por meio do envio de notificações usando Olá SDK .NET para hubs de notificação em um aplicativo de console, em vez de um serviço de back-end.</span><span class="sxs-lookup"><span data-stu-id="c0952-165">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using hello .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="c0952-166">É recomendável Olá [usar Hubs de notificação toopush notificações toousers] tutorial como a próxima etapa hello para enviar notificações de um back-end do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c0952-166">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="c0952-167">No entanto, a saudação abordagens a seguir pode ser usada para enviar notificações:</span><span class="sxs-lookup"><span data-stu-id="c0952-167">However, hello following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="c0952-168">**Interface REST**: você pode dar suporte à notificação em qualquer plataforma de back-end usando Olá [interface REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0952-168">**REST Interface**:  You can support notification on any backend platform using  hello [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="c0952-169">**SDK .NET de Hubs de notificação do Microsoft Azure**: em Olá Gerenciador de pacotes do Nuget para Visual Studio, execute [Microsoft.Azure.NotificationHubs Install-Package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="c0952-169">**Microsoft Azure Notification Hubs .NET SDK**: In hello Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="c0952-170">**Node.js** : [como toouse Hubs de notificação do Node. js](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="c0952-170">**Node.js** : [How toouse Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="c0952-171">**Aplicativos móveis do Azure**: para obter um exemplo de como toosend notificações de um aplicativo móvel do Azure que esteja integrado com Hubs de notificação, consulte [adicionar notificações de push para aplicativos móveis](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="c0952-171">**Azure Mobile Apps**: For an example of how toosend notifications from an Azure Mobile App that's integrated with Notification Hubs, see [Add push notifications for Mobile Apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="c0952-172">**Java / PHP**: para obter um exemplo de como as notificações de toosend usando Olá APIs REST, consulte "como toouse Hubs de notificação do Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="c0952-172">**Java / PHP**: For an example of how toosend notifications by using hello REST APIs, see "How toouse Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-console-app"></a><span data-ttu-id="c0952-173">(Opcional) Enviar notificações de um aplicativo de console</span><span class="sxs-lookup"><span data-stu-id="c0952-173">(Optional) Send notifications from a console app</span></span>
<span data-ttu-id="c0952-174">notificações de toosend usando um aplicativo de console .NET siga estas etapas.</span><span class="sxs-lookup"><span data-stu-id="c0952-174">toosend notifications by using a .NET console application follow these steps.</span></span> 

1. <span data-ttu-id="c0952-175">Solução de saudação com o botão direito, selecione **adicionar** e **novo projeto...** e, em seguida, em **Visual C#**, clique em **Windows** e **aplicativo de Console**e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="c0952-175">Right-click hello solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
    <span data-ttu-id="c0952-176">Isso adiciona uma novo Visual C# console toohello solução de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c0952-176">This adds a new Visual C# console application toohello solution.</span></span> <span data-ttu-id="c0952-177">Você também pode fazer isso em uma solução separada.</span><span class="sxs-lookup"><span data-stu-id="c0952-177">You can also do this in a separate solution.</span></span>

2. <span data-ttu-id="c0952-178">No Visual Studio, clique em **Ferramentas**, em **Gerenciador de Pacotes NuGet** e em **Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="c0952-178">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="c0952-179">Isso exibe o saudação Package Manager Console no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c0952-179">This displays hello Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="c0952-180">Olá janela do Console do Gerenciador de pacotes, definido Olá **projeto padrão** tooyour novo projeto de aplicativo de console e na janela de console hello, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c0952-180">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="c0952-181">Isso adiciona um toohello Referência SDK de Hubs de notificação do Azure usando Olá <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacote NuGet de Hubs Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="c0952-181">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="c0952-182">Abra o arquivo Program.cs de saudação e adicione o seguinte de saudação `using` instrução:</span><span class="sxs-lookup"><span data-stu-id="c0952-182">Open hello Program.cs file and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="c0952-183">Em Olá **programa** classe, adicione o seguinte método de saudação:</span><span class="sxs-lookup"><span data-stu-id="c0952-183">In hello **Program** class, add hello following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
            await hub.SendWindowsNativeNotificationAsync(toast);
        }
   
       Make sure tooreplace hello "hub name" placeholder with hello name of hello notification hub that as it appears in hello Azure Portal. Also, replace hello connection string placeholder with hello **DefaultFullSharedAccessSignature** connection string that you obtained from hello **Access Policies** page of your Notification Hub in hello section called "Configure your notification hub."
   
   > [!NOTE]
   > <span data-ttu-id="c0952-184">Certifique-se de que você use a cadeia de caracteres de conexão de saudação com **completo** acessar, não **escutar** acesso.</span><span class="sxs-lookup"><span data-stu-id="c0952-184">Make sure that you use hello connection string that has **Full** access, not **Listen** access.</span></span> <span data-ttu-id="c0952-185">cadeia de caracteres de acesso de escuta Olá não tem as notificações de toosend de permissões.</span><span class="sxs-lookup"><span data-stu-id="c0952-185">hello listen-access string does not have permissions toosend notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="c0952-186">Adicionar Olá Olá linhas a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="c0952-186">Add hello following lines in hello **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="c0952-187">Clique em projeto de aplicativo de console Olá no Visual Studio e clique em **definir como projeto de inicialização** tooset como projeto de inicialização de saudação.</span><span class="sxs-lookup"><span data-stu-id="c0952-187">Right-click hello console application project in Visual Studio, and click **Set as StartUp Project** tooset it as hello startup project.</span></span> <span data-ttu-id="c0952-188">Em seguida, pressione Olá **F5** aplicativo hello de toorun da chave.</span><span class="sxs-lookup"><span data-stu-id="c0952-188">Then press hello **F5** key toorun hello application.</span></span>
   
    <span data-ttu-id="c0952-189">Você receberá uma notificação do sistema em todos os dispositivos registrados.</span><span class="sxs-lookup"><span data-stu-id="c0952-189">You will receive a toast notification on all registered devices.</span></span> <span data-ttu-id="c0952-190">Faixa de notificação do sistema Olá clicando ou tocando carrega o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="c0952-190">Clicking or tapping hello toast banner loads hello app.</span></span>

<span data-ttu-id="c0952-191">Você pode encontrar todas as cargas de saudação com suporte no hello [catálogo de sistema], [catálogo bloco], e [visão geral de notificação] tópicos no MSDN.</span><span class="sxs-lookup"><span data-stu-id="c0952-191">You can find all hello supported payloads in hello [toast catalog], [tile catalog], and [badge overview] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0952-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c0952-192">Next steps</span></span>
<span data-ttu-id="c0952-193">Neste exemplo simples, você enviadas notificações difusão tooall seus dispositivos do Windows usando o portal de saudação ou um aplicativo de console.</span><span class="sxs-lookup"><span data-stu-id="c0952-193">In this simple example, you sent broadcast notifications tooall your Windows devices using hello portal or a console app.</span></span> <span data-ttu-id="c0952-194">É recomendável Olá [usar Hubs de notificação toopush notificações toousers] tutorial como a próxima etapa de saudação.</span><span class="sxs-lookup"><span data-stu-id="c0952-194">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step.</span></span> <span data-ttu-id="c0952-195">Ele lhe mostrará como toosend notificações de um back-end do ASP.NET usando marcas tootarget determinados usuários.</span><span class="sxs-lookup"><span data-stu-id="c0952-195">It will show you how toosend notifications from an ASP.NET backend using tags tootarget specific users.</span></span>

<span data-ttu-id="c0952-196">Se você quiser toosegment os usuários, grupos de interesse, consulte [toosend de Hubs de notificação de uso últimas notícias].</span><span class="sxs-lookup"><span data-stu-id="c0952-196">If you want toosegment your users by interest groups, see [Use Notification Hubs toosend breaking news].</span></span> 

<span data-ttu-id="c0952-197">toolearn obter mais informações sobre Hubs de notificação, consulte [orientação de Hubs de notificação](notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c0952-197">toolearn more general information about Notification Hubs, see [Notification Hubs Guidance](notification-hubs-push-notification-overview.md).</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-create-console-app.png
[14]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-toast.png
[19]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-reg.png
[20]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-universal-app-install-package.png

<!-- URLs. -->

[usar Hubs de notificação toopush notificações toousers]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[toosend de Hubs de notificação de uso últimas notícias]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md

[catálogo de sistema]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx
[catálogo bloco]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx
[visão geral de notificação]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx
