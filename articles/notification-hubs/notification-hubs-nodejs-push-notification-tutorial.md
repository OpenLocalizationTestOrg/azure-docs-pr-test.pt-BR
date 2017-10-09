---
title: "notificações de push aaaSending com Hubs de notificação do Azure e Node. js"
description: "Saiba como toouse Hubs de notificação toosend notificações por push de um aplicativo Node. js."
keywords: "notificação por push, notificações por push,push do node.js,push do ios"
services: notification-hubs
documentationcenter: nodejs
author: ysxu
manager: erikre
editor: 
ms.assetid: ded4749c-6c39-4ff8-b2cf-1927b3e92f93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 10/25/2016
ms.author: yuaxu
ms.openlocfilehash: 151d224fa6dd07e4acdc3a4887c4e95ee03168c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a><span data-ttu-id="954ff-104">Enviar notificações por push com os Hubs de Notificação do Azure e o Node.js</span><span class="sxs-lookup"><span data-stu-id="954ff-104">Sending push notifications with Azure Notification Hubs and Node.js</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a><span data-ttu-id="954ff-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="954ff-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="954ff-106">toocomplete neste tutorial, você deve ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="954ff-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="954ff-107">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="954ff-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="954ff-108">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span><span class="sxs-lookup"><span data-stu-id="954ff-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span></span>
> 
> 

<span data-ttu-id="954ff-109">Este guia mostrará como toosend notificações por push com ajuda Olá hubs de notificação do Azure diretamente de um aplicativo Node. js.</span><span class="sxs-lookup"><span data-stu-id="954ff-109">This guide will show you how toosend push notifications with hello help of Azure Notification Hubs directly from a Node.js application.</span></span> 

<span data-ttu-id="954ff-110">cenários de saudação abordados incluem a remessa tooapplications de notificações por push em Olá plataformas a seguir:</span><span class="sxs-lookup"><span data-stu-id="954ff-110">hello scenarios covered include sending push notifications tooapplications on hello following platforms:</span></span>

* <span data-ttu-id="954ff-111">Android</span><span class="sxs-lookup"><span data-stu-id="954ff-111">Android</span></span>
* <span data-ttu-id="954ff-112">iOS</span><span class="sxs-lookup"><span data-stu-id="954ff-112">iOS</span></span>
* <span data-ttu-id="954ff-113">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="954ff-113">Windows Phone</span></span>
* <span data-ttu-id="954ff-114">Plataforma Universal do Windows</span><span class="sxs-lookup"><span data-stu-id="954ff-114">Universal Windows Platform</span></span> 

<span data-ttu-id="954ff-115">Para obter mais informações sobre hubs de notificação, consulte Olá [próximas etapas](#next) seção.</span><span class="sxs-lookup"><span data-stu-id="954ff-115">For more information on notification hubs, see hello [Next Steps](#next) section.</span></span>

## <a name="what-are-notification-hubs"></a><span data-ttu-id="954ff-116">O que são Hubs de Notificação?</span><span class="sxs-lookup"><span data-stu-id="954ff-116">What are Notification Hubs?</span></span>
<span data-ttu-id="954ff-117">Hubs de notificação do Azure oferecem uma infraestrutura fácil de usar, multiplataforma e dimensionável para enviar por push a dispositivos de toomobile de notificações.</span><span class="sxs-lookup"><span data-stu-id="954ff-117">Azure Notification Hubs provide an easy-to-use, multi-platform, scalable infrastructure for sending push notifications toomobile devices.</span></span> <span data-ttu-id="954ff-118">Para obter detalhes sobre a infraestrutura de serviço hello, consulte Olá [Hubs de notificação do Azure](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) página.</span><span class="sxs-lookup"><span data-stu-id="954ff-118">For details on hello service infrastructure, see hello [Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) page.</span></span>

## <a name="create-a-nodejs-application"></a><span data-ttu-id="954ff-119">Criar um aplicativo Node.js</span><span class="sxs-lookup"><span data-stu-id="954ff-119">Create a Node.js Application</span></span>
<span data-ttu-id="954ff-120">a primeira etapa Olá neste tutorial está criando um novo aplicativo Node. js em branco.</span><span class="sxs-lookup"><span data-stu-id="954ff-120">hello first step in this tutorial is creating a new blank Node.js application.</span></span> <span data-ttu-id="954ff-121">Para obter instruções sobre como criar um aplicativo Node. js, consulte [criar e implantar um aplicativo de Node. js tooAzure Site da Web][nodejswebsite], [serviço de nuvem do Node. js] [ Node.js Cloud Service] usando o Windows PowerShell, ou [Site com WebMatrix].</span><span class="sxs-lookup"><span data-stu-id="954ff-121">For instructions on creating a Node.js application, see [Create and deploy a Node.js application tooAzure Web Site][nodejswebsite], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or [Web Site with WebMatrix].</span></span>

## <a name="configure-your-application-toouse-notification-hubs"></a><span data-ttu-id="954ff-122">Configurar seu aplicativo tooUse os Hubs de notificação</span><span class="sxs-lookup"><span data-stu-id="954ff-122">Configure Your Application tooUse Notification Hubs</span></span>
<span data-ttu-id="954ff-123">toouse Hubs de notificação do Azure, você precisa toodownload e use Olá Node. js [pacote do azure](https://www.npmjs.com/package/azure), que inclui um conjunto interno de bibliotecas auxiliar que se comunicam com serviços da REST Olá push notificação.</span><span class="sxs-lookup"><span data-stu-id="954ff-123">toouse Azure Notification Hubs, you need toodownload and use hello Node.js [azure package](https://www.npmjs.com/package/azure), which includes a built-in set of helper libraries that communicate with hello push notification REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="954ff-124">Usar o pacote de saudação do Gerenciador de pacote de nó (NPM) tooobtain</span><span class="sxs-lookup"><span data-stu-id="954ff-124">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="954ff-125">Use uma interface de linha de comando como **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Linux) e navegue toohello pasta em que você criou seu aplicativo em branco .</span><span class="sxs-lookup"><span data-stu-id="954ff-125">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Linux) and navigate toohello folder where you created your blank application.</span></span>
2. <span data-ttu-id="954ff-126">Tipo **npm instalar azure sb** na janela de comando hello.</span><span class="sxs-lookup"><span data-stu-id="954ff-126">Type **npm install azure-sb** in hello command window.</span></span>
3. <span data-ttu-id="954ff-127">Você pode executar manualmente Olá **ls** ou **dir** tooverify de comando que um **nó\_módulos** pasta foi criada.</span><span class="sxs-lookup"><span data-stu-id="954ff-127">You can manually run hello **ls** or **dir** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="954ff-128">Dentro dessa pasta, localize Olá **azure** pacote, que contém as bibliotecas de saudação necessário tooaccess Olá Hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="954ff-128">Inside that folder, find hello **azure** package, which contains hello libraries you need tooaccess hello Notification Hub.</span></span>

> [!NOTE]
> <span data-ttu-id="954ff-129">Você pode aprender mais sobre a instalação de NPM em oficial Olá [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span><span class="sxs-lookup"><span data-stu-id="954ff-129">You can learn more about installing NPM on hello official [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span></span> 
> 
> 

### <a name="import-hello-module"></a><span data-ttu-id="954ff-130">Módulo de saudação de importação</span><span class="sxs-lookup"><span data-stu-id="954ff-130">Import hello module</span></span>
<span data-ttu-id="954ff-131">Usando um editor de texto, adicionar Olá após toohello superior de saudação **server.js** arquivo de aplicativo hello:</span><span class="sxs-lookup"><span data-stu-id="954ff-131">Using a text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

    var azure = require('azure');

### <a name="setup-an-azure-notification-hub-connection"></a><span data-ttu-id="954ff-132">Instalar uma conexão do hub de notificação do Azure</span><span class="sxs-lookup"><span data-stu-id="954ff-132">Setup an Azure Notification Hub connection</span></span>
<span data-ttu-id="954ff-133">Olá **NotificationHubService** objeto permite que você trabalhe com hubs de notificação.</span><span class="sxs-lookup"><span data-stu-id="954ff-133">hello **NotificationHubService** object lets you work with notification hubs.</span></span> <span data-ttu-id="954ff-134">Olá código a seguir cria um **NotificationHubService** objeto para o hub de nofication Olá denominado **hubname**.</span><span class="sxs-lookup"><span data-stu-id="954ff-134">hello following code creates a **NotificationHubService** object for hello nofication hub named **hubname**.</span></span> <span data-ttu-id="954ff-135">Adicioná-lo superior de saudação do hello **server.js** arquivo depois de módulo de saudação do azure Olá instrução tooimport:</span><span class="sxs-lookup"><span data-stu-id="954ff-135">Add it near hello top of hello **server.js** file, after hello statement tooimport hello azure module:</span></span>

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

<span data-ttu-id="954ff-136">Olá conexão **connectionstring** valor pode ser obtido da saudação [Portal do Azure] executando Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="954ff-136">hello connection **connectionstring** value can be obtained from hello [Azure Portal] by performing hello following steps:</span></span>

1. <span data-ttu-id="954ff-137">No painel de navegação esquerdo hello, clique em **procurar**.</span><span class="sxs-lookup"><span data-stu-id="954ff-137">In hello left navigation pane, click **Browse**.</span></span>
2. <span data-ttu-id="954ff-138">Selecione **Hubs de notificação**e, em seguida, localizar Olá hub de desejar toouse para exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="954ff-138">Select **Notification Hubs**, and then find hello hub you wish toouse for hello sample.</span></span> <span data-ttu-id="954ff-139">Você pode consultar toohello [tutorial guia de Introdução do Windows Store](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) se precisar de ajuda para criar um novo Hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="954ff-139">You can refer toohello [Windows Store Getting Started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) if you need help creating a new Notification Hub.</span></span>
3. <span data-ttu-id="954ff-140">Escolha a opção **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="954ff-140">Select **Settings**.</span></span>
4. <span data-ttu-id="954ff-141">Clique em **Políticas de Acesso**.</span><span class="sxs-lookup"><span data-stu-id="954ff-141">Click on **Access Policies**.</span></span> <span data-ttu-id="954ff-142">Você verá as duas cadeias de conexão de acesso compartilhado e completo.</span><span class="sxs-lookup"><span data-stu-id="954ff-142">You will see both shared and full access connection strings.</span></span>

![Portal do Azure - Hubs de Notificação](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> <span data-ttu-id="954ff-144">Você também pode recuperar a cadeia de caracteres de conexão de saudação usando Olá **Get-AzureSbNamespace** cmdlet fornecido pelo [Azure PowerShell](/powershell/azureps-cmdlets-docs) ou hello **sb azure namespace Mostrar** com Olá [Azure Interface de linha de comando (CLI do Azure)](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="954ff-144">You can also retrieve hello connection string using hello **Get-AzureSbNamespace** cmdlet provided by [Azure PowerShell](/powershell/azureps-cmdlets-docs) or hello **azure sb namespace show** command with hello [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md).</span></span>
> 
> 

## <a name="general-architecture"></a><span data-ttu-id="954ff-145">Arquitetura geral</span><span class="sxs-lookup"><span data-stu-id="954ff-145">General architecture</span></span>
<span data-ttu-id="954ff-146">Olá **NotificationHubService** objeto expõe Olá instâncias de objeto para enviar por push notificações toospecific dispositivos e aplicativos a seguir:</span><span class="sxs-lookup"><span data-stu-id="954ff-146">hello **NotificationHubService** object exposes hello following object instances for sending push notifications toospecific devices and applications:</span></span>

* <span data-ttu-id="954ff-147">**Android** -usar Olá **GcmService** objeto, que está disponível em **notificationHubService.gcm**</span><span class="sxs-lookup"><span data-stu-id="954ff-147">**Android** - use hello **GcmService** object, which is available at **notificationHubService.gcm**</span></span>
* <span data-ttu-id="954ff-148">**iOS** -usar Olá **ApnsService** objeto, que é acessível no **notificationHubService.apns**</span><span class="sxs-lookup"><span data-stu-id="954ff-148">**iOS** - use hello **ApnsService** object, which is accessible at **notificationHubService.apns**</span></span>
* <span data-ttu-id="954ff-149">**Windows Phone** -usar Olá **MpnsService** objeto, que está disponível em **notificationHubService.mpns**</span><span class="sxs-lookup"><span data-stu-id="954ff-149">**Windows Phone** - use hello **MpnsService** object, which is available at **notificationHubService.mpns**</span></span>
* <span data-ttu-id="954ff-150">**Plataforma universal do Windows** -usar Olá **WnsService** objeto, que está disponível em **notificationHubService.wns**</span><span class="sxs-lookup"><span data-stu-id="954ff-150">**Universal Windows Platform** - use hello **WnsService** object, which is available at **notificationHubService.wns**</span></span>

### <a name="how-to-send-push-notifications-tooandroid-applications"></a><span data-ttu-id="954ff-151">Como: enviar por push a aplicativos de tooAndroid de notificações</span><span class="sxs-lookup"><span data-stu-id="954ff-151">How to: Send push notifications tooAndroid applications</span></span>
<span data-ttu-id="954ff-152">Olá **GcmService** objeto fornece um **enviar** método que pode ser usado toosend push notificações tooAndroid aplicativos.</span><span class="sxs-lookup"><span data-stu-id="954ff-152">hello **GcmService** object provides a **send** method that can be used toosend push notifications tooAndroid applications.</span></span> <span data-ttu-id="954ff-153">Olá **enviar** método aceita Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="954ff-153">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="954ff-154">**Marcas** -Olá identificador de marca.</span><span class="sxs-lookup"><span data-stu-id="954ff-154">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="954ff-155">Se nenhuma marca for fornecida, notificação de saudação será enviada tooall clientes.</span><span class="sxs-lookup"><span data-stu-id="954ff-155">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="954ff-156">**Carga** -Olá carga brutos da cadeia de caracteres ou JSON da mensagem.</span><span class="sxs-lookup"><span data-stu-id="954ff-156">**Payload** - hello message's JSON or raw string payload.</span></span>
* <span data-ttu-id="954ff-157">**Retorno de chamada** -Olá a função de retorno de chamada.</span><span class="sxs-lookup"><span data-stu-id="954ff-157">**Callback** - hello callback function.</span></span>

<span data-ttu-id="954ff-158">Para obter mais informações sobre o formato de carga hello, consulte Olá **carga** seção Olá [implementando GCM Server](http://developer.android.com/google/gcm/server.html#payload) documento.</span><span class="sxs-lookup"><span data-stu-id="954ff-158">For more information on hello payload format, see hello **Payload** section of hello [Implementing GCM Server](http://developer.android.com/google/gcm/server.html#payload) document.</span></span>

<span data-ttu-id="954ff-159">Olá, código a seguir usa Olá **GcmService** instância exposta pelo Olá **NotificationHubService** toosend um tooall de notificação por push registrado clientes.</span><span class="sxs-lookup"><span data-stu-id="954ff-159">hello following code uses hello **GcmService** instance exposed by hello **NotificationHubService** toosend a push notification tooall registered clients.</span></span>

    var payload = {
      data: {
        message: 'Hello!'
      }
    };
    notificationHubService.gcm.send(null, payload, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-tooios-applications"></a><span data-ttu-id="954ff-160">Como: enviar por push a aplicativos de tooiOS de notificações</span><span class="sxs-lookup"><span data-stu-id="954ff-160">How to: Send push notifications tooiOS applications</span></span>
<span data-ttu-id="954ff-161">Mesmo assim como acontece com aplicativos do Android descrito acima, Olá **ApnsService** objeto fornece um **enviar** método que pode ser usado toosend push notificações tooiOS aplicativos.</span><span class="sxs-lookup"><span data-stu-id="954ff-161">Same as with Android applications described above, hello **ApnsService** object provides a **send** method that can be used toosend push notifications tooiOS applications.</span></span> <span data-ttu-id="954ff-162">Olá **enviar** método aceita Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="954ff-162">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="954ff-163">**Marcas** -Olá identificador de marca.</span><span class="sxs-lookup"><span data-stu-id="954ff-163">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="954ff-164">Se nenhuma marca for fornecida, notificação de saudação será enviada tooall clientes.</span><span class="sxs-lookup"><span data-stu-id="954ff-164">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="954ff-165">**Carga** - Olá JSON da mensagem ou carga da cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="954ff-165">**Payload** - hello message's JSON or string payload.</span></span>
* <span data-ttu-id="954ff-166">**Retorno de chamada** -Olá a função de retorno de chamada.</span><span class="sxs-lookup"><span data-stu-id="954ff-166">**Callback** - hello callback function.</span></span>

<span data-ttu-id="954ff-167">Para o formato de carga de saudação de mais informações, consulte Olá **carga de notificação** seção Olá [Local e o guia de programação de notificação por Push](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) documento.</span><span class="sxs-lookup"><span data-stu-id="954ff-167">For more information hello payload format, see hello **Notification Payload** section of hello [Local and Push Notification Programming Guide](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) document.</span></span>

<span data-ttu-id="954ff-168">Olá, código a seguir usa Olá **ApnsService** instância exposta pelo Olá **NotificationHubService** toosend um alerta de mensagem tooall clientes:</span><span class="sxs-lookup"><span data-stu-id="954ff-168">hello following code uses hello **ApnsService** instance exposed by hello **NotificationHubService** toosend an alert message tooall clients:</span></span>

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-toowindows-phone-applications"></a><span data-ttu-id="954ff-169">Como: enviar por push a aplicativos de telefone tooWindows notificações</span><span class="sxs-lookup"><span data-stu-id="954ff-169">How to: Send push notifications tooWindows Phone applications</span></span>
<span data-ttu-id="954ff-170">Olá **MpnsService** objeto fornece um **enviar** método que pode ser usado toosend push notificações tooWindows aplicativos de telefone.</span><span class="sxs-lookup"><span data-stu-id="954ff-170">hello **MpnsService** object provides a **send** method that can be used toosend push notifications tooWindows Phone applications.</span></span> <span data-ttu-id="954ff-171">Olá **enviar** método aceita Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="954ff-171">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="954ff-172">**Marcas** -Olá identificador de marca.</span><span class="sxs-lookup"><span data-stu-id="954ff-172">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="954ff-173">Se nenhuma marca for fornecida, notificação de saudação será enviada tooall clientes.</span><span class="sxs-lookup"><span data-stu-id="954ff-173">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="954ff-174">**Carga** -Olá carga XML da mensagem.</span><span class="sxs-lookup"><span data-stu-id="954ff-174">**Payload** - hello message's XML payload.</span></span>
* <span data-ttu-id="954ff-175">**TargetName** - `toast` para notificações ‘toast’.</span><span class="sxs-lookup"><span data-stu-id="954ff-175">**TargetName** - `toast` for toast notifications.</span></span> <span data-ttu-id="954ff-176">`token` para notificações de bloco.</span><span class="sxs-lookup"><span data-stu-id="954ff-176">`token` for tile notifications.</span></span>
* <span data-ttu-id="954ff-177">**NotificationClass** -Olá prioridade de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="954ff-177">**NotificationClass** - hello priority of hello notification.</span></span> <span data-ttu-id="954ff-178">Consulte Olá **elementos de cabeçalho HTTP** seção Olá [notificações por Push de um servidor](http://msdn.microsoft.com/library/hh221551.aspx) documento para obter valores válidos.</span><span class="sxs-lookup"><span data-stu-id="954ff-178">See hello **HTTP Header Elements** section of hello [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) document for valid values.</span></span>
* <span data-ttu-id="954ff-179">**Options** : cabeçalhos de solicitação opcionais.</span><span class="sxs-lookup"><span data-stu-id="954ff-179">**Options** - optional request headers.</span></span>
* <span data-ttu-id="954ff-180">**Retorno de chamada** -Olá a função de retorno de chamada.</span><span class="sxs-lookup"><span data-stu-id="954ff-180">**Callback** - hello callback function.</span></span>

<span data-ttu-id="954ff-181">Para obter uma lista de válido **TargetName**, **NotificationClass** e opções de cabeçalho, confira Olá [notificações por Push de um servidor](http://msdn.microsoft.com/library/hh221551.aspx) página.</span><span class="sxs-lookup"><span data-stu-id="954ff-181">For a list of valid **TargetName**, **NotificationClass** and header options, check out hello [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) page.</span></span>

<span data-ttu-id="954ff-182">Olá, código de exemplo a seguir usa Olá **MpnsService** instância exposta pelo Olá **NotificationHubService** toosend uma notificação por push do sistema:</span><span class="sxs-lookup"><span data-stu-id="954ff-182">hello following sample code uses hello **MpnsService** instance exposed by hello **NotificationHubService** toosend a toast push notification:</span></span>

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-toouniversal-windows-platform-uwp-applications"></a><span data-ttu-id="954ff-183">Como: enviar por push a aplicativos de plataforma do Windows (UWP) tooUniversal notificações</span><span class="sxs-lookup"><span data-stu-id="954ff-183">How to: Send push notifications tooUniversal Windows Platform (UWP) applications</span></span>
<span data-ttu-id="954ff-184">Olá **WnsService** objeto fornece um **enviar** método que pode ser usados toosend push notificações tooUniversal plataforma Windows aplicativos.</span><span class="sxs-lookup"><span data-stu-id="954ff-184">hello **WnsService** object provides a **send** method that can be used toosend push notifications tooUniversal Windows Platform applications.</span></span>  <span data-ttu-id="954ff-185">Olá **enviar** método aceita Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="954ff-185">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="954ff-186">**Marcas** -Olá identificador de marca.</span><span class="sxs-lookup"><span data-stu-id="954ff-186">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="954ff-187">Se nenhuma marca for fornecida, notificação de saudação será enviada clientes tooall registrado.</span><span class="sxs-lookup"><span data-stu-id="954ff-187">If no tag is provided, hello notification will be sent tooall registered clients.</span></span>
* <span data-ttu-id="954ff-188">**Carga** -carga da mensagem XML hello.</span><span class="sxs-lookup"><span data-stu-id="954ff-188">**Payload** - hello XML message payload.</span></span>
* <span data-ttu-id="954ff-189">**Tipo** -Olá tipo de notificação.</span><span class="sxs-lookup"><span data-stu-id="954ff-189">**Type** - hello notification type.</span></span>
* <span data-ttu-id="954ff-190">**Options** : cabeçalhos de solicitação opcionais.</span><span class="sxs-lookup"><span data-stu-id="954ff-190">**Options** - optional request headers.</span></span>
* <span data-ttu-id="954ff-191">**Retorno de chamada** -Olá a função de retorno de chamada.</span><span class="sxs-lookup"><span data-stu-id="954ff-191">**Callback** - hello callback function.</span></span>

<span data-ttu-id="954ff-192">Para obter uma lista de tipos e de cabeçalhos de solicitação válidos, veja [Solicitação de serviço e cabeçalhos de resposta de notificação por push](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span><span class="sxs-lookup"><span data-stu-id="954ff-192">For a list of valid types and request headers, see [Push notification service request and response headers](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span></span>

<span data-ttu-id="954ff-193">Olá, código a seguir usa Olá **WnsService** instância exposta pelo Olá **NotificationHubService** toosend um aplicativo UWP tooa de notificação do sistema por push:</span><span class="sxs-lookup"><span data-stu-id="954ff-193">hello following code uses hello **WnsService** instance exposed by hello **NotificationHubService** toosend a toast push notification tooa UWP app:</span></span>

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a><span data-ttu-id="954ff-194">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="954ff-194">Next Steps</span></span>
<span data-ttu-id="954ff-195">trechos de código de exemplo do Hello acima permitem que você tooeasily compilação serviço infraestrutura toodeliver push notificações tooa ampla variedade de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="954ff-195">hello sample snippets above allow you tooeasily build service infrastructure toodeliver push notifications tooa wide variety of devices.</span></span> <span data-ttu-id="954ff-196">Agora que você aprendeu as Noções básicas de saudação do uso de Hubs de notificação com Node. js, siga essas toolearn links mais informações sobre como você pode estender esses recursos adicionais.</span><span class="sxs-lookup"><span data-stu-id="954ff-196">Now that you've learned hello basics of using Notification Hubs with node.js, follow these links toolearn more about how you can extend these capabilities further.</span></span>

* <span data-ttu-id="954ff-197">Consulte Olá referência do MSDN para [Hubs de notificação do Azure](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span><span class="sxs-lookup"><span data-stu-id="954ff-197">See hello MSDN Reference for [Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span></span>
* <span data-ttu-id="954ff-198">Visite Olá [SDK do Azure para o nó] repositório no GitHub para obter mais exemplos e detalhes de implementação.</span><span class="sxs-lookup"><span data-stu-id="954ff-198">Visit hello [Azure SDK for Node] repository on GitHub for more samples and implementation details.</span></span>

[SDK do Azure para o nó]: https://github.com/WindowsAzure/azure-sdk-for-node
[Next Steps]: #nextsteps
[What are Service Bus Topics and Subscriptions?]: #what-are-service-bus-topics
[Create a Service Namespace]: #create-a-service-namespace
[Obtain hello Default Management Credentials for hello Namespace]: #obtain-default-credentials
[Create a Node.js Application]: #Create_a_Nodejs_Application
[Configure Your Application tooUse Service Bus]: #Configure_Your_Application_to_Use_Service_Bus
[How to: Create a Topic]: #How_to_Create_a_Topic
[How to: Create Subscriptions]: #How_to_Create_Subscriptions
[How to: Send Messages tooa Topic]: #How_to_Send_Messages_to_a_Topic
[How to: Receive Messages from a Subscription]: #How_to_Receive_Messages_from_a_Subscription
[How to: Handle Application Crashes and Unreadable Messages]: #How_to_Handle_Application_Crashes_and_Unreadable_Messages
[How to: Delete Topics and Subscriptions]: #How_to_Delete_Topics_and_Subscriptions
[1]: #Next_Steps
[Topic Concepts]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-topics-01.png
[Azure Classic Portal]: http://manage.windowsazure.com
[image]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-03.png
[2]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-04.png
[3]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-05.png
[4]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-06.png
[5]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-07.png
[SqlFilter.SqlExpression]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.sqlexpression.aspx
[Azure Service Bus Notification Hubs]: http://msdn.microsoft.com/library/windowsazure/jj927170.aspx
[SqlFilter]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.aspx
[Site com WebMatrix]: /develop/nodejs/tutorials/web-site-with-webmatrix/
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Previous Management Portal]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/previous-portal.png
[nodejswebsite]: /develop/nodejs/tutorials/create-a-website-(mac)/
[Node.js Cloud Service with Storage]: /develop/nodejs/tutorials/web-app-with-storage/
[Node.js Web Application with Storage]: /develop/nodejs/tutorials/web-site-with-storage/
[Portal do Azure]: https://portal.azure.com
