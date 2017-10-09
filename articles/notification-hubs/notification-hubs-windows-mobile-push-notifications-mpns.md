---
title: "notificações de push aaaSending com Hubs de notificação do Azure no Windows Phone | Microsoft Docs"
description: "Neste tutorial, você aprenderá como notificações de toopush de Hubs de notificação do Azure toouse tooa Windows Phone 8 ou o aplicativo do Windows Phone 8.1 Silverlight."
services: notification-hubs
documentationcenter: windows
keywords: "notificação por push,notificação por push,envio por push do windows phone"
author: ysxu
manager: erikre
editor: erikre
ms.assetid: d872d8dc-4658-4d65-9e71-fa8e34fae96e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 1a0ad238fe7788ae2e4f47f02d113391af03dd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-on-windows-phone"></a><span data-ttu-id="a739b-104">Enviar notificações por push com os Hubs de Notificação do Azure no Windows Phone</span><span class="sxs-lookup"><span data-stu-id="a739b-104">Sending push notifications with Azure Notification Hubs on Windows Phone</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="a739b-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a739b-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="a739b-106">toocomplete neste tutorial, você deve ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="a739b-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="a739b-107">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="a739b-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a739b-108">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="a739b-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="a739b-109">Este tutorial mostra como aplicativo de Windows Phone 8 ou Windows Phone 8.1 Silverlight tooa notificações de envio de toouse toosend de Hubs de notificação do Azure.</span><span class="sxs-lookup"><span data-stu-id="a739b-109">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Windows Phone 8 or Windows Phone 8.1 Silverlight application.</span></span> <span data-ttu-id="a739b-110">Se você estiver direcionando o Windows Phone 8.1 (não Silverlight), consulte toohello [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) versão.</span><span class="sxs-lookup"><span data-stu-id="a739b-110">If you are targeting Windows Phone 8.1 (non-Silverlight), then refer toohello [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) version.</span></span>
<span data-ttu-id="a739b-111">Neste tutorial, você deve criar um aplicativo do Windows Phone 8 em branco que recebe notificações por push usando Olá Microsoft Push Notification Service (MPNS).</span><span class="sxs-lookup"><span data-stu-id="a739b-111">In this tutorial, you create a blank Windows Phone 8 app that receives push notifications by using hello Microsoft Push Notification Service (MPNS).</span></span> <span data-ttu-id="a739b-112">Quando você terminar, você será capaz de toouse sua toobroadcast de hub de notificação por push notificações tooall Olá a dispositivos que executam seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a739b-112">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

> [!NOTE]
> <span data-ttu-id="a739b-113">Olá notificação Hubs Windows Phone SDK não dá suporte ao uso Olá Windows Push Notification Service (WNS) com aplicativos do Windows Phone 8.1 Silverlight.</span><span class="sxs-lookup"><span data-stu-id="a739b-113">hello Notification Hubs Windows Phone SDK does not support using hello Windows Push Notification Service (WNS) with Windows Phone 8.1 Silverlight apps.</span></span> <span data-ttu-id="a739b-114">toouse WNS (em vez de MPNS) com aplicativos do Windows Phone 8.1 Silverlight, siga Olá [Hubs de notificação - Windows Phone Silverlight tutorial], que usa APIs REST.</span><span class="sxs-lookup"><span data-stu-id="a739b-114">toouse WNS (instead of MPNS) with Windows Phone 8.1 Silverlight apps, follow hello [Notification Hubs - Windows Phone Silverlight tutorial], which uses REST APIs.</span></span>
> 
> 

<span data-ttu-id="a739b-115">tutorial de saudação demonstra o cenário de difusão simples hello usando Hubs de notificação.</span><span class="sxs-lookup"><span data-stu-id="a739b-115">hello tutorial demonstrates hello simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a739b-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a739b-116">Prerequisites</span></span>
<span data-ttu-id="a739b-117">Este tutorial requer o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="a739b-117">This tutorial requires hello following:</span></span>

* <span data-ttu-id="a739b-118">[Visual Studio 2012 Express para Windows Phone]ou uma versão posterior.</span><span class="sxs-lookup"><span data-stu-id="a739b-118">[Visual Studio 2012 Express for Windows Phone], or a later version.</span></span>

<span data-ttu-id="a739b-119">A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais sobre Hubs de Notificação para aplicativos Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="a739b-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Phone 8 apps.</span></span>

## <a name="create-your-notification-hub"></a><span data-ttu-id="a739b-120">Criar seu Hub de Notificação</span><span class="sxs-lookup"><span data-stu-id="a739b-120">Create your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="a739b-121">Clique em Olá <b>Notification Services</b> seção (dentro de <i>configurações</i>), clique em <b>Windows Phone (MPNS)</b> e, em seguida, clique em hello <b>habilitar por push não autenticadas </b> caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="a739b-121">Click hello <b>Notification Services</b> section (within <i>Settings</i>), click on <b>Windows Phone (MPNS)</b> and then click hello <b>Enable unauthenticated push</b> check box.</span></span></p>
</li>
</ol>

&emsp;&emsp;![Portal do Azure - habilitar notificações por push não autenticadas](./media/notification-hubs-windows-phone-get-started/azure-portal-unauth.png)

<span data-ttu-id="a739b-123">O hub é agora notificação toosend criado e configurado não autenticado para Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="a739b-123">Your hub is now created and configured toosend unauthenticated notification for Windows Phone.</span></span>

> [!NOTE]
> <span data-ttu-id="a739b-124">Este tutorial usa MPNS no modo não autenticado.</span><span class="sxs-lookup"><span data-stu-id="a739b-124">This tutorial uses MPNS in unauthenticated mode.</span></span> <span data-ttu-id="a739b-125">Modo não autenticado MPNS vem com restrições em que você pode enviar tooeach canal de notificações.</span><span class="sxs-lookup"><span data-stu-id="a739b-125">MPNS unauthenticated mode comes with restrictions on notifications that you can send tooeach channel.</span></span> <span data-ttu-id="a739b-126">Oferece suporte a Hubs de notificação [MPNS autenticado modo](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) , permitindo-lhe tooupload seu certificado.</span><span class="sxs-lookup"><span data-stu-id="a739b-126">Notification Hubs supports [MPNS authenticated mode](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) by allowing you tooupload your certificate.</span></span>
> 
> 

## <a name="connecting-your-app-toohello-notification-hub"></a><span data-ttu-id="a739b-127">Conectando o hub de notificação do aplicativo toohello</span><span class="sxs-lookup"><span data-stu-id="a739b-127">Connecting your app toohello notification hub</span></span>
1. <span data-ttu-id="a739b-128">No Visual Studio, crie um novo aplicativo de console do Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="a739b-128">In Visual Studio, create a new Windows Phone 8 application.</span></span>
   
       ![Visual Studio - New Project - Windows Phone App][13]
   
    <span data-ttu-id="a739b-129">No Visual Studio 2013 Atualização 2 ou posterior, você cria um aplicativo do Windows Phone Silverlight.</span><span class="sxs-lookup"><span data-stu-id="a739b-129">In Visual Studio 2013 Update 2 or later, you instead create a Windows Phone Silverlight application.</span></span>
   
    ![Visual Studio - Novo Projeto - Aplicativo em branco - Windows Phone Silverlight][11]
2. <span data-ttu-id="a739b-131">No Visual Studio, clique com botão direito solução hello e, em seguida, clique em **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="a739b-131">In Visual Studio, right-click hello solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="a739b-132">Isso exibe o saudação **gerenciar pacotes NuGet** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a739b-132">This displays hello **Manage NuGet Packages** dialog box.</span></span>
3. <span data-ttu-id="a739b-133">Procurar `WindowsAzure.Messaging.Managed` e clique em **instalar**e aceite os termos de uso do hello.</span><span class="sxs-lookup"><span data-stu-id="a739b-133">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and then accept hello terms of use.</span></span>
   
    ![Visual Studio - Gerenciador de Pacotes do NuGet][20]
   
    <span data-ttu-id="a739b-135">Isso baixa, instala e adiciona uma biblioteca da referência toohello mensagens do Azure para Windows usando Olá <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">pacote WindowsAzure.Messaging.Managed NuGet</a>.</span><span class="sxs-lookup"><span data-stu-id="a739b-135">This downloads, installs, and adds a reference toohello Azure Messaging library for Windows by using hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
4. <span data-ttu-id="a739b-136">Abra o arquivo de saudação App.xaml.cs e adicione o seguinte Olá `using` instruções:</span><span class="sxs-lookup"><span data-stu-id="a739b-136">Open hello file App.xaml.cs and add hello following `using` statements:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
5. <span data-ttu-id="a739b-137">Adicionar Olá seguinte código na parte superior de saudação do **Application_Launching** método em App.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="a739b-137">Add hello following code at hello top of **Application_Launching** method in App.xaml.cs:</span></span>
   
        var channel = HttpNotificationChannel.Find("MyPushChannel");
        if (channel == null)
        {
            channel = new HttpNotificationChannel("MyPushChannel");
            channel.Open();
            channel.BindToShellToast();
        }
   
        channel.ChannelUriUpdated += new EventHandler<NotificationChannelUriEventArgs>(async (o, args) =>
        {
            var hub = new NotificationHub("<hub name>", "<connection string>");
            var result = await hub.RegisterNativeAsync(args.ChannelUri.ToString());
   
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
            {
                MessageBox.Show("Registration :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
            });
        });
   
   > [!NOTE]
   > <span data-ttu-id="a739b-138">Olá valor **MyPushChannel** é um índice que é usado toolookup um canal existente no hello [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) coleção.</span><span class="sxs-lookup"><span data-stu-id="a739b-138">hello value **MyPushChannel** is an index that is used toolookup an existing channel in hello [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) collection.</span></span> <span data-ttu-id="a739b-139">Se não houver uma, crie uma nova entrada com esse nome.</span><span class="sxs-lookup"><span data-stu-id="a739b-139">If there isn't one there, create a new entry with that name.</span></span>
   > 
   > 
   
    <span data-ttu-id="a739b-140">Certifique-se de tooinsert Olá nome de sua cadeia de conexão de hub e hello chamado **DefaultListenSharedAccessSignature** que você obteve na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="a739b-140">Make sure tooinsert hello name of your hub and hello connection string called **DefaultListenSharedAccessSignature** that you obtained in hello previous section.</span></span>
    <span data-ttu-id="a739b-141">Esse código recupera o URI do canal Olá para o aplicativo de saudação do MPNS e, em seguida, registra esse URI de canal com seu hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="a739b-141">This code retrieves hello channel URI for hello app from MPNS, and then registers that channel URI with your notification hub.</span></span> <span data-ttu-id="a739b-142">Ela também garante que esse canal Olá que URI é registrado no hub de notificação, que cada aplicativo de saudação do tempo é iniciado.</span><span class="sxs-lookup"><span data-stu-id="a739b-142">It also guarantees that hello channel URI is registered in your notification hub each time hello application is launched.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a739b-143">Este tutorial envia um dispositivo de toohello de notificação do sistema.</span><span class="sxs-lookup"><span data-stu-id="a739b-143">This tutorial sends a toast notification toohello device.</span></span> <span data-ttu-id="a739b-144">Quando você enviar uma notificação de bloco, em vez disso, você deve chamar hello **BindToShellTile** método no canal de saudação.</span><span class="sxs-lookup"><span data-stu-id="a739b-144">When you send a tile notification, you must instead call hello **BindToShellTile** method on hello channel.</span></span> <span data-ttu-id="a739b-145">toosupport notificações de notificação do sistema e lado a lado, chamar **BindToShellTile** e **BindToShellToast**.</span><span class="sxs-lookup"><span data-stu-id="a739b-145">toosupport both toast and tile notifications, call both **BindToShellTile** and  **BindToShellToast**.</span></span>
   > 
   > 
6. <span data-ttu-id="a739b-146">No Gerenciador de soluções, expanda **propriedades**, abra Olá `WMAppManifest.xml` de arquivo, clique em Olá **recursos** guia e certifique-se de que Olá **ID_CAP_PUSH_NOTIFICATION** recurso é verificado.</span><span class="sxs-lookup"><span data-stu-id="a739b-146">In Solution Explorer, expand **Properties**, open hello `WMAppManifest.xml` file, click hello **Capabilities** tab, and make sure that hello **ID_CAP_PUSH_NOTIFICATION** capability is checked.</span></span>
   
       ![Visual Studio - Windows Phone App Capabilities][14]
   
       This ensures that your app can receive push notifications. Without it, any attempt toosend a push notification toohello app will fail.
7. <span data-ttu-id="a739b-147">Olá pressione `F5` toorun chave Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a739b-147">Press hello `F5` key toorun hello app.</span></span>
   
    <span data-ttu-id="a739b-148">Será exibida uma mensagem de registro no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="a739b-148">A registration message is displayed in hello app.</span></span>
8. <span data-ttu-id="a739b-149">Aplicativo hello fechar.</span><span class="sxs-lookup"><span data-stu-id="a739b-149">Close hello app.</span></span>  
   
   > [!NOTE]
   > <span data-ttu-id="a739b-150">tooreceive uma notificação por push do sistema, o aplicativo hello não deve estar executando em primeiro plano da saudação.</span><span class="sxs-lookup"><span data-stu-id="a739b-150">tooreceive a toast push notification, hello application must not be running in hello foreground.</span></span>
   > 
   > 

## <a name="send-push-notifications-from-your-backend"></a><span data-ttu-id="a739b-151">Enviar notificações por push de seu back-end</span><span class="sxs-lookup"><span data-stu-id="a739b-151">Send push notifications from your backend</span></span>
<span data-ttu-id="a739b-152">Você pode enviar notificações por push usando os Hubs de notificação de qualquer back-end por meio de saudação público <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">interface REST</a>.</span><span class="sxs-lookup"><span data-stu-id="a739b-152">You can send push notifications by using Notification Hubs from any backend via hello public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="a739b-153">Neste tutorial, você envia notificações por push usando um aplicativo de console .NET.</span><span class="sxs-lookup"><span data-stu-id="a739b-153">In this tutorial, you send push notifications using a .NET console application.</span></span> 

<span data-ttu-id="a739b-154">Para obter um exemplo de como toosend notificações por push de um back-end ASP.NET WebAPI integrado com Hubs de notificação, consulte [notificação Hubs notificar os usuários do Azure com o back-end .NET](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).</span><span class="sxs-lookup"><span data-stu-id="a739b-154">For an example of how toosend push notifications from an ASP.NET WebAPI backend that's integrated with Notification Hubs, see [Azure Notification Hubs Notify Users with .NET backend](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).</span></span>  

<span data-ttu-id="a739b-155">Para obter um exemplo de como as notificações por push de toosend usando Olá [APIs REST](https://msdn.microsoft.com/library/azure/dn223264.aspx), check-out [como toouse Hubs de notificação do Java](notification-hubs-java-push-notification-tutorial.md) e [como toouse Hubs de notificação do PHP](notification-hubs-php-push-notification-tutorial.md) .</span><span class="sxs-lookup"><span data-stu-id="a739b-155">For an example of how toosend push notifications by using hello [REST APIs](https://msdn.microsoft.com/library/azure/dn223264.aspx), check out [How toouse Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) and [How toouse Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

1. <span data-ttu-id="a739b-156">Solução de saudação com o botão direito, selecione **adicionar** e **novo projeto...** e, em seguida, em **Visual C#**, clique em **Windows** e **aplicativo de Console**e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="a739b-156">Right-click hello solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
       ![Visual Studio - New Project - Console Application][6]
   
    <span data-ttu-id="a739b-157">Isso adiciona uma novo Visual C# console toohello solução de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a739b-157">This adds a new Visual C# console application toohello solution.</span></span> <span data-ttu-id="a739b-158">Você também pode fazer isso em uma solução separada.</span><span class="sxs-lookup"><span data-stu-id="a739b-158">You can also do this in a separate solution.</span></span>
2. <span data-ttu-id="a739b-159">Clique em **Ferramentas**, em **Gerenciador de Pacotes da Biblioteca** e em **Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="a739b-159">Click **Tools**, click **Library Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="a739b-160">Isso exibe o saudação Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="a739b-160">This displays hello Package Manager Console.</span></span>
3. <span data-ttu-id="a739b-161">Em hello **Package Manager Console** janela, Olá do conjunto **projeto padrão** tooyour novo projeto de aplicativo de console e na janela de console hello, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a739b-161">In hello **Package Manager Console** window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
       Install-Package Microsoft.Azure.NotificationHubs
   
   <span data-ttu-id="a739b-162">Isso adiciona um toohello Referência SDK de Hubs de notificação do Azure usando Olá <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacote NuGet de Hubs Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="a739b-162">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="a739b-163">Olá abrir `Program.cs` de arquivo e adicione o seguinte Olá `using` instrução:</span><span class="sxs-lookup"><span data-stu-id="a739b-163">Open hello `Program.cs` file and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="a739b-164">Em Olá `Program` classe, adicione o seguinte método de saudação:</span><span class="sxs-lookup"><span data-stu-id="a739b-164">In hello `Program` class, add hello following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            string toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                "<wp:Notification xmlns:wp=\"WPNotification\">" +
                   "<wp:Toast>" +
                        "<wp:Text1>Hello from a .NET App!</wp:Text1>" +
                   "</wp:Toast> " +
                "</wp:Notification>";
            await hub.SendMpnsNativeNotificationAsync(toast);
        }
   
    <span data-ttu-id="a739b-165">Verifique se Olá de tooreplace `<hub name>` espaço reservado com o nome de saudação do hub de notificação de saudação que aparece no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="a739b-165">Make sure tooreplace hello `<hub name>` placeholder with hello name of hello notification hub that appears in hello portal.</span></span> <span data-ttu-id="a739b-166">Além disso, substitua espaço reservado de cadeia de caracteres de conexão Olá Olá cadeia de conexão chamada **DefaultFullSharedAccessSignature** que você obteve na seção hello "Configurar seu hub de notificação".</span><span class="sxs-lookup"><span data-stu-id="a739b-166">Also, replace hello connection string placeholder with hello connection string called **DefaultFullSharedAccessSignature** that you obtained in hello section "Configure your notification hub."</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a739b-167">Certifique-se de que você use a cadeia de caracteres de conexão de saudação com **completo** acessar, não **escutar** acesso.</span><span class="sxs-lookup"><span data-stu-id="a739b-167">Make sure that you use hello connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="a739b-168">cadeia de caracteres de acesso de escuta Olá não tem as notificações por push de toosend de permissões.</span><span class="sxs-lookup"><span data-stu-id="a739b-168">hello listen-access string does not have permissions toosend push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="a739b-169">Adicionar Olá a seguinte linha no seu `Main` método:</span><span class="sxs-lookup"><span data-stu-id="a739b-169">Add hello following line in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="a739b-170">Com o Windows Phone emulador em execução e seu projeto de aplicativo de console do aplicativo hello fechado, defina como saudação padrão o projeto de inicialização em pressione Olá `F5` toorun chave Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a739b-170">With your Windows Phone emulator running and your app closed, set hello console application project as hello default startup project, and then press hello `F5` key toorun hello app.</span></span>
   
    <span data-ttu-id="a739b-171">Você receberá uma notificação do sistema por push.</span><span class="sxs-lookup"><span data-stu-id="a739b-171">You will receive a toast push notification.</span></span> <span data-ttu-id="a739b-172">Tocando em faixa de notificação do sistema Olá carrega o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="a739b-172">Tapping hello toast banner loads hello app.</span></span>

<span data-ttu-id="a739b-173">Você encontrará todas as cargas de possíveis Olá Olá [catálogo de sistema] e [catálogo bloco] tópicos no MSDN.</span><span class="sxs-lookup"><span data-stu-id="a739b-173">You can find all hello possible payloads in hello [toast catalog] and [tile catalog] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a739b-174">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a739b-174">Next steps</span></span>
<span data-ttu-id="a739b-175">Neste exemplo simples, você transmitida tooall de notificações por push seus dispositivos Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="a739b-175">In this simple example, you broadcasted push notifications tooall your Windows Phone 8 devices.</span></span> 

<span data-ttu-id="a739b-176">Em ordem tootarget usuários específicos, consulte toohello [usar Hubs de notificação toopush notificações toousers] tutorial.</span><span class="sxs-lookup"><span data-stu-id="a739b-176">In order tootarget specific users, refer toohello [Use Notification Hubs toopush notifications toousers] tutorial.</span></span> 

<span data-ttu-id="a739b-177">Se você desejar toosegment os usuários, grupos de interesse, você pode ler [toosend de Hubs de notificação de uso últimas notícias].</span><span class="sxs-lookup"><span data-stu-id="a739b-177">If you want toosegment your users by interest groups, you can read [Use Notification Hubs toosend breaking news].</span></span> 

<span data-ttu-id="a739b-178">Saiba mais sobre como Hubs de notificação toouse [orientação de Hubs de notificação].</span><span class="sxs-lookup"><span data-stu-id="a739b-178">Learn more about how toouse Notification Hubs in [Notification Hubs Guidance].</span></span>

<!-- Images. -->
[6]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png
[7]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal.png
[8]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal2.png
[9]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal.png
[10]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal2.png
[11]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-silverlight-app.png
[12]: ./media/notification-hubs-windows-phone-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-app.png
[14]: ./media/notification-hubs-windows-phone-get-started/mobile-app-enable-push-wp8.png
[15]: ./media/notification-hubs-windows-phone-get-started/notification-hub-pushauth.png
[20]: ./media/notification-hubs-windows-phone-get-started/notification-hub-windows-universal-app-install-package.png
[213]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png





<!-- URLs. -->
[Visual Studio 2012 Express para Windows Phone]: https://go.microsoft.com/fwLink/p/?LinkID=268374
[orientação de Hubs de notificação]: http://msdn.microsoft.com/library/jj927170.aspx
[MPNS authenticated mode]: http://msdn.microsoft.com/library/windowsphone/develop/ff941099(v=vs.105).aspx
[usar Hubs de notificação toopush notificações toousers]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[toosend de Hubs de notificação de uso últimas notícias]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md
[catálogo de sistema]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx
[catálogo bloco]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx
[Hubs de notificação - Windows Phone Silverlight tutorial]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp

