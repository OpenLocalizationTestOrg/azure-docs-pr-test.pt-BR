---
title: "Enviar notificações por push com os Hubs de Notificação do Azure e o Node.js"
description: "Saiba como usar os Hubs de notificação para enviar notificações por push de um aplicativo do Node. js."
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
ms.openlocfilehash: dc4987b16b2e930641c6c90eff8b65c1bf8d573c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a><span data-ttu-id="2483d-104">Enviar notificações por push com os Hubs de Notificação do Azure e o Node.js</span><span class="sxs-lookup"><span data-stu-id="2483d-104">Sending push notifications with Azure Notification Hubs and Node.js</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a><span data-ttu-id="2483d-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="2483d-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2483d-106">Para concluir este tutorial, você precisa ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="2483d-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="2483d-107">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="2483d-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="2483d-108">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span><span class="sxs-lookup"><span data-stu-id="2483d-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span></span>
> 
> 

<span data-ttu-id="2483d-109">Este guia mostra como enviar notificações por push com a ajuda dos Hubs de Notificação do Azure diretamente de um aplicativo Node.js.</span><span class="sxs-lookup"><span data-stu-id="2483d-109">This guide will show you how to send push notifications with the help of Azure Notification Hubs directly from a Node.js application.</span></span> 

<span data-ttu-id="2483d-110">Os cenários abordados incluem o envio de notificações por push para aplicativos nas seguintes plataformas:</span><span class="sxs-lookup"><span data-stu-id="2483d-110">The scenarios covered include sending push notifications to applications on the following platforms:</span></span>

* <span data-ttu-id="2483d-111">Android</span><span class="sxs-lookup"><span data-stu-id="2483d-111">Android</span></span>
* <span data-ttu-id="2483d-112">iOS</span><span class="sxs-lookup"><span data-stu-id="2483d-112">iOS</span></span>
* <span data-ttu-id="2483d-113">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="2483d-113">Windows Phone</span></span>
* <span data-ttu-id="2483d-114">Plataforma Universal do Windows</span><span class="sxs-lookup"><span data-stu-id="2483d-114">Universal Windows Platform</span></span> 

<span data-ttu-id="2483d-115">Para obter mais informações sobre Hubs de Notificação, consulte a seção [Próximas etapas](#next) .</span><span class="sxs-lookup"><span data-stu-id="2483d-115">For more information on notification hubs, see the [Next Steps](#next) section.</span></span>

## <a name="what-are-notification-hubs"></a><span data-ttu-id="2483d-116">O que são Hubs de Notificação?</span><span class="sxs-lookup"><span data-stu-id="2483d-116">What are Notification Hubs?</span></span>
<span data-ttu-id="2483d-117">Os Hubs de Notificação do Azure fornecem uma infraestrutura de várias plataformas escalonáveis e fáceis de usar para o envio de notificações por push para dispositivos móveis.</span><span class="sxs-lookup"><span data-stu-id="2483d-117">Azure Notification Hubs provide an easy-to-use, multi-platform, scalable infrastructure for sending push notifications to mobile devices.</span></span> <span data-ttu-id="2483d-118">Para obter detalhes sobre a infraestrutura de serviço, confira a página [Hubs de Notificação do Azure](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) .</span><span class="sxs-lookup"><span data-stu-id="2483d-118">For details on the service infrastructure, see the [Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) page.</span></span>

## <a name="create-a-nodejs-application"></a><span data-ttu-id="2483d-119">Criar um aplicativo Node.js</span><span class="sxs-lookup"><span data-stu-id="2483d-119">Create a Node.js Application</span></span>
<span data-ttu-id="2483d-120">A primeira etapa deste tutorial é a criação de um novo aplicativo Node. js em branco.</span><span class="sxs-lookup"><span data-stu-id="2483d-120">The first step in this tutorial is creating a new blank Node.js application.</span></span> <span data-ttu-id="2483d-121">Para obter instruções sobre como criar um aplicativo Node.js, consulte [Criar e implantar um aplicativo Node.js em um Site do Azure][nodejswebsite], [Serviço de Nuvem do Node.js][Node.js Cloud Service] usando o Windows PowerShell ou [Site com o WebMatrix].</span><span class="sxs-lookup"><span data-stu-id="2483d-121">For instructions on creating a Node.js application, see [Create and deploy a Node.js application to Azure Web Site][nodejswebsite], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or [Web Site with WebMatrix].</span></span>

## <a name="configure-your-application-to-use-notification-hubs"></a><span data-ttu-id="2483d-122">Configurar seu aplicativo para usar os Hubs de Notificação</span><span class="sxs-lookup"><span data-stu-id="2483d-122">Configure Your Application to Use Notification Hubs</span></span>
<span data-ttu-id="2483d-123">Para usar os Hubs de Notificação do Azure, você precisa baixar e usar o [pacote azure](https://www.npmjs.com/package/azure)do Node.js, que inclui um conjunto interno de bibliotecas auxiliares que se comunicam com os serviços REST de notificação por push.</span><span class="sxs-lookup"><span data-stu-id="2483d-123">To use Azure Notification Hubs, you need to download and use the Node.js [azure package](https://www.npmjs.com/package/azure), which includes a built-in set of helper libraries that communicate with the push notification REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="2483d-124">Usar o NPM (gerenciador de pacotes de nós) para obter o pacote</span><span class="sxs-lookup"><span data-stu-id="2483d-124">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="2483d-125">Use uma interface de linha de comando, como **PowerShell** (Windows), **Terminal** (Mac) ou **Bash** (Unix) e navegue até a pasta em que você criou o aplicativo em branco.</span><span class="sxs-lookup"><span data-stu-id="2483d-125">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Linux) and navigate to the folder where you created your blank application.</span></span>
2. <span data-ttu-id="2483d-126">Digite **npm install azure-sb** na janela de comando.</span><span class="sxs-lookup"><span data-stu-id="2483d-126">Type **npm install azure-sb** in the command window.</span></span>
3. <span data-ttu-id="2483d-127">Você pode executar o comando **ls** ou **dir** manualmente para verificar se uma pasta **node\_modules** foi criada.</span><span class="sxs-lookup"><span data-stu-id="2483d-127">You can manually run the **ls** or **dir** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="2483d-128">Dentro dessa pasta, você encontrará o pacote **azure** , que contém as bibliotecas necessárias para acessar o Hub de Notificação.</span><span class="sxs-lookup"><span data-stu-id="2483d-128">Inside that folder, find the **azure** package, which contains the libraries you need to access the Notification Hub.</span></span>

> [!NOTE]
> <span data-ttu-id="2483d-129">Saiba mais sobre a instalação do NPM no [blog oficial do NPM](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span><span class="sxs-lookup"><span data-stu-id="2483d-129">You can learn more about installing NPM on the official [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span></span> 
> 
> 

### <a name="import-the-module"></a><span data-ttu-id="2483d-130">Importar o módulo</span><span class="sxs-lookup"><span data-stu-id="2483d-130">Import the module</span></span>
<span data-ttu-id="2483d-131">Usando um editor de texto, adicione o seguinte à parte superior do arquivo **server.js** do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="2483d-131">Using a text editor, add the following to the top of the **server.js** file of the application:</span></span>

    var azure = require('azure');

### <a name="setup-an-azure-notification-hub-connection"></a><span data-ttu-id="2483d-132">Instalar uma conexão do hub de notificação do Azure</span><span class="sxs-lookup"><span data-stu-id="2483d-132">Setup an Azure Notification Hub connection</span></span>
<span data-ttu-id="2483d-133">O objeto **NotificationHubService** permite trabalhar com Hubs de Notificação.</span><span class="sxs-lookup"><span data-stu-id="2483d-133">The **NotificationHubService** object lets you work with notification hubs.</span></span> <span data-ttu-id="2483d-134">O código a seguir cria um objeto **NotificationHubService** para o Hub de Notificação chamado **hubname**.</span><span class="sxs-lookup"><span data-stu-id="2483d-134">The following code creates a **NotificationHubService** object for the nofication hub named **hubname**.</span></span> <span data-ttu-id="2483d-135">Adicione-o próximo ao início do arquivo **server.js** , após a instrução de importação do módulo Azure:</span><span class="sxs-lookup"><span data-stu-id="2483d-135">Add it near the top of the **server.js** file, after the statement to import the azure module:</span></span>

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

<span data-ttu-id="2483d-136">O valor da conexão **connectionstring** pode ser obtido no [Portal do Azure] por meio da execução das seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2483d-136">The connection **connectionstring** value can be obtained from the [Azure Portal] by performing the following steps:</span></span>

1. <span data-ttu-id="2483d-137">No painel de navegação esquerdo, clique em **Procurar**.</span><span class="sxs-lookup"><span data-stu-id="2483d-137">In the left navigation pane, click **Browse**.</span></span>
2. <span data-ttu-id="2483d-138">Selecione **Hubs de Notificação**e localize o hub que você deseja usar no exemplo.</span><span class="sxs-lookup"><span data-stu-id="2483d-138">Select **Notification Hubs**, and then find the hub you wish to use for the sample.</span></span> <span data-ttu-id="2483d-139">Você poderá consultar o [tutorial Introdução da Windows Store](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) se precisar de ajuda para criar um novo Hub de Notificação.</span><span class="sxs-lookup"><span data-stu-id="2483d-139">You can refer to the [Windows Store Getting Started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) if you need help creating a new Notification Hub.</span></span>
3. <span data-ttu-id="2483d-140">Escolha a opção **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="2483d-140">Select **Settings**.</span></span>
4. <span data-ttu-id="2483d-141">Clique em **Políticas de Acesso**.</span><span class="sxs-lookup"><span data-stu-id="2483d-141">Click on **Access Policies**.</span></span> <span data-ttu-id="2483d-142">Você verá as duas cadeias de conexão de acesso compartilhado e completo.</span><span class="sxs-lookup"><span data-stu-id="2483d-142">You will see both shared and full access connection strings.</span></span>

![Portal do Azure - Hubs de Notificação](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> <span data-ttu-id="2483d-144">Você também pode recuperar a cadeia de conexão usando o cmdlet **Get-AzureSbNamespace** fornecido pelo [Azure PowerShell](/powershell/azureps-cmdlets-docs) ou o comando **azure sb namespace show** com a [Interface de Linha de Comando do Azure (CLI do Azure)](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="2483d-144">You can also retrieve the connection string using the **Get-AzureSbNamespace** cmdlet provided by [Azure PowerShell](/powershell/azureps-cmdlets-docs) or the **azure sb namespace show** command with the [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md).</span></span>
> 
> 

## <a name="general-architecture"></a><span data-ttu-id="2483d-145">Arquitetura geral</span><span class="sxs-lookup"><span data-stu-id="2483d-145">General architecture</span></span>
<span data-ttu-id="2483d-146">O objeto **NotificationHubService** expõe as seguintes instâncias de objeto para o envio de notificações por push a dispositivos e aplicativos específicos:</span><span class="sxs-lookup"><span data-stu-id="2483d-146">The **NotificationHubService** object exposes the following object instances for sending push notifications to specific devices and applications:</span></span>

* <span data-ttu-id="2483d-147">**Android** - use o objeto **GcmService**, que está disponível em **notificationHubService.gcm**</span><span class="sxs-lookup"><span data-stu-id="2483d-147">**Android** - use the **GcmService** object, which is available at **notificationHubService.gcm**</span></span>
* <span data-ttu-id="2483d-148">**iOS** - use o objeto **ApnsService**, que está disponível em **notificationHubService.apns**</span><span class="sxs-lookup"><span data-stu-id="2483d-148">**iOS** - use the **ApnsService** object, which is accessible at **notificationHubService.apns**</span></span>
* <span data-ttu-id="2483d-149">**Windows Phone** - use o objeto **MpnsService**, que está disponível em **notificationHubService.mpns**</span><span class="sxs-lookup"><span data-stu-id="2483d-149">**Windows Phone** - use the **MpnsService** object, which is available at **notificationHubService.mpns**</span></span>
* <span data-ttu-id="2483d-150">**Plataforma Universal do Windows**: use o objeto **WnsService**, que está disponível em **notificationHubService.wns**</span><span class="sxs-lookup"><span data-stu-id="2483d-150">**Universal Windows Platform** - use the **WnsService** object, which is available at **notificationHubService.wns**</span></span>

### <a name="how-to-send-push-notifications-to-android-applications"></a><span data-ttu-id="2483d-151">Como enviar notificações para aplicativos Android</span><span class="sxs-lookup"><span data-stu-id="2483d-151">How to: Send push notifications to Android applications</span></span>
<span data-ttu-id="2483d-152">O objeto **GcmService** fornece um método **send** que pode ser usado para enviar notificações por push aos aplicativos Android.</span><span class="sxs-lookup"><span data-stu-id="2483d-152">The **GcmService** object provides a **send** method that can be used to send push notifications to Android applications.</span></span> <span data-ttu-id="2483d-153">O método **send** aceita os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="2483d-153">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="2483d-154">**Tags** : o identificador da etiqueta.</span><span class="sxs-lookup"><span data-stu-id="2483d-154">**Tags** - the tag identifier.</span></span> <span data-ttu-id="2483d-155">Se nenhuma marca for fornecida, a notificação será enviada a todos os clientes.</span><span class="sxs-lookup"><span data-stu-id="2483d-155">If no tag is provided, the notification will be sent to all clients.</span></span>
* <span data-ttu-id="2483d-156">**Payload** : o JSON ou o conteúdo bruto de cadeia de caracteres da mensagem.</span><span class="sxs-lookup"><span data-stu-id="2483d-156">**Payload** - the message's JSON or raw string payload.</span></span>
* <span data-ttu-id="2483d-157">**Callback** : a função de retorno de chamada.</span><span class="sxs-lookup"><span data-stu-id="2483d-157">**Callback** - the callback function.</span></span>

<span data-ttu-id="2483d-158">Para saber mais sobre o formato do conteúdo, consulte a seção **Conteúdo** do documento [Implementando o servidor GCM](http://developer.android.com/google/gcm/server.html#payload) .</span><span class="sxs-lookup"><span data-stu-id="2483d-158">For more information on the payload format, see the **Payload** section of the [Implementing GCM Server](http://developer.android.com/google/gcm/server.html#payload) document.</span></span>

<span data-ttu-id="2483d-159">O código a seguir usa a instância **GcmService** exposta pelo **NotificationHubService** para enviar uma notificação por push a todos os clientes registrados.</span><span class="sxs-lookup"><span data-stu-id="2483d-159">The following code uses the **GcmService** instance exposed by the **NotificationHubService** to send a push notification to all registered clients.</span></span>

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

### <a name="how-to-send-push-notifications-to-ios-applications"></a><span data-ttu-id="2483d-160">Como enviar notificações por push para aplicativos iOS</span><span class="sxs-lookup"><span data-stu-id="2483d-160">How to: Send push notifications to iOS applications</span></span>
<span data-ttu-id="2483d-161">Da mesma forma como ocorre com os aplicativos Android descritos acima, o objeto **ApnsService** fornece um método **send** que pode ser usado para enviar notificações por push aos aplicativos iOS.</span><span class="sxs-lookup"><span data-stu-id="2483d-161">Same as with Android applications described above, the **ApnsService** object provides a **send** method that can be used to send push notifications to iOS applications.</span></span> <span data-ttu-id="2483d-162">O método **send** aceita os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="2483d-162">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="2483d-163">**Tags** : o identificador da etiqueta.</span><span class="sxs-lookup"><span data-stu-id="2483d-163">**Tags** - the tag identifier.</span></span> <span data-ttu-id="2483d-164">Se nenhuma marca for fornecida, a notificação será enviada a todos os clientes.</span><span class="sxs-lookup"><span data-stu-id="2483d-164">If no tag is provided, the notification will be sent to all clients.</span></span>
* <span data-ttu-id="2483d-165">**Payload** : o JSON ou o conteúdo de cadeia de caracteres da mensagem.</span><span class="sxs-lookup"><span data-stu-id="2483d-165">**Payload** - the message's JSON or string payload.</span></span>
* <span data-ttu-id="2483d-166">**Callback** : a função de retorno de chamada.</span><span class="sxs-lookup"><span data-stu-id="2483d-166">**Callback** - the callback function.</span></span>

<span data-ttu-id="2483d-167">Para saber mais sobre o formato do conteúdo, veja a seção **Conteúdo de notificação** do documento [Guia de programação de notificações locais e por push](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) .</span><span class="sxs-lookup"><span data-stu-id="2483d-167">For more information the payload format, see The **Notification Payload** section of the [Local and Push Notification Programming Guide](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) document.</span></span>

<span data-ttu-id="2483d-168">O código a seguir usa a instância **ApnsService** exposta por **NotificationHubService** para enviar uma mensagem de alerta a todos os clientes:</span><span class="sxs-lookup"><span data-stu-id="2483d-168">The following code uses the **ApnsService** instance exposed by the **NotificationHubService** to send an alert message to all clients:</span></span>

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-to-windows-phone-applications"></a><span data-ttu-id="2483d-169">Como enviar notificações por push para aplicativos do Windows Phone</span><span class="sxs-lookup"><span data-stu-id="2483d-169">How to: Send push notifications to Windows Phone applications</span></span>
<span data-ttu-id="2483d-170">O objeto **MpnsService** fornece um método **send** que pode ser usado para enviar notificações por push aos aplicativos do Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="2483d-170">The **MpnsService** object provides a **send** method that can be used to send push notifications to Windows Phone applications.</span></span> <span data-ttu-id="2483d-171">O método **send** aceita os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="2483d-171">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="2483d-172">**Tags** : o identificador da etiqueta.</span><span class="sxs-lookup"><span data-stu-id="2483d-172">**Tags** - the tag identifier.</span></span> <span data-ttu-id="2483d-173">Se nenhuma marca for fornecida, a notificação será enviada a todos os clientes.</span><span class="sxs-lookup"><span data-stu-id="2483d-173">If no tag is provided, the notification will be sent to all clients.</span></span>
* <span data-ttu-id="2483d-174">**Payload** : o conteúdo XML da mensagem.</span><span class="sxs-lookup"><span data-stu-id="2483d-174">**Payload** - the message's XML payload.</span></span>
* <span data-ttu-id="2483d-175">**TargetName** - `toast` para notificações ‘toast’.</span><span class="sxs-lookup"><span data-stu-id="2483d-175">**TargetName** - `toast` for toast notifications.</span></span> <span data-ttu-id="2483d-176">`token` para notificações de bloco.</span><span class="sxs-lookup"><span data-stu-id="2483d-176">`token` for tile notifications.</span></span>
* <span data-ttu-id="2483d-177">**NotificationClass** : a prioridade da notificação.</span><span class="sxs-lookup"><span data-stu-id="2483d-177">**NotificationClass** - The priority of the notification.</span></span> <span data-ttu-id="2483d-178">Veja a seção **Elementos de cabeçalhos HTTP** do documento [Notificações por push de um servidor](http://msdn.microsoft.com/library/hh221551.aspx) para obter os valores válidos.</span><span class="sxs-lookup"><span data-stu-id="2483d-178">See the **HTTP Header Elements** section of the [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) document for valid values.</span></span>
* <span data-ttu-id="2483d-179">**Options** : cabeçalhos de solicitação opcionais.</span><span class="sxs-lookup"><span data-stu-id="2483d-179">**Options** - optional request headers.</span></span>
* <span data-ttu-id="2483d-180">**Callback** : a função de retorno de chamada.</span><span class="sxs-lookup"><span data-stu-id="2483d-180">**Callback** - the callback function.</span></span>

<span data-ttu-id="2483d-181">Para obter uma lista de opções válidas de **TargetName**, de **NotificationClass** e de cabeçalho, confira a página [Notificações por push de um servidor](http://msdn.microsoft.com/library/hh221551.aspx).</span><span class="sxs-lookup"><span data-stu-id="2483d-181">For a list of valid **TargetName**, **NotificationClass** and header options, check out the [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) page.</span></span>

<span data-ttu-id="2483d-182">O código de exemplo a seguir usa a instância **MpnsService** exposta pelo **NotificationHubService** para enviar uma notificação do sistema por push:</span><span class="sxs-lookup"><span data-stu-id="2483d-182">The following sample code uses the **MpnsService** instance exposed by the **NotificationHubService** to send a toast push notification:</span></span>

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-to-universal-windows-platform-uwp-applications"></a><span data-ttu-id="2483d-183">Como enviar notificações por push para aplicativos da UWP (Plataforma Universal do Windows)</span><span class="sxs-lookup"><span data-stu-id="2483d-183">How to: Send push notifications to Universal Windows Platform (UWP) applications</span></span>
<span data-ttu-id="2483d-184">O objeto **WnsService** fornece um método **send** que pode ser usado para enviar notificações por push aos aplicativos da Plataforma Universal do Windows.</span><span class="sxs-lookup"><span data-stu-id="2483d-184">The **WnsService** object provides a **send** method that can be used to send push notifications to Universal Windows Platform applications.</span></span>  <span data-ttu-id="2483d-185">O método **send** aceita os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="2483d-185">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="2483d-186">**Tags** : o identificador da etiqueta.</span><span class="sxs-lookup"><span data-stu-id="2483d-186">**Tags** - the tag identifier.</span></span> <span data-ttu-id="2483d-187">Se nenhuma marca for fornecida, a notificação será enviada a todos os clientes registrados.</span><span class="sxs-lookup"><span data-stu-id="2483d-187">If no tag is provided, the notification will be sent to all registered clients.</span></span>
* <span data-ttu-id="2483d-188">**Payload** : a carga da mensagem XML.</span><span class="sxs-lookup"><span data-stu-id="2483d-188">**Payload** - the XML message payload.</span></span>
* <span data-ttu-id="2483d-189">**Type** : o tipo de notificação.</span><span class="sxs-lookup"><span data-stu-id="2483d-189">**Type** - the notification type.</span></span>
* <span data-ttu-id="2483d-190">**Options** : cabeçalhos de solicitação opcionais.</span><span class="sxs-lookup"><span data-stu-id="2483d-190">**Options** - optional request headers.</span></span>
* <span data-ttu-id="2483d-191">**Callback** : a função de retorno de chamada.</span><span class="sxs-lookup"><span data-stu-id="2483d-191">**Callback** - the callback function.</span></span>

<span data-ttu-id="2483d-192">Para obter uma lista de tipos e de cabeçalhos de solicitação válidos, veja [Solicitação de serviço e cabeçalhos de resposta de notificação por push](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span><span class="sxs-lookup"><span data-stu-id="2483d-192">For a list of valid types and request headers, see [Push notification service request and response headers](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span></span>

<span data-ttu-id="2483d-193">O código a seguir usa a instância **WnsService** exposta pelo **NotificationHubService** para enviar uma notificação do sistema por push para um aplicativo da UWP:</span><span class="sxs-lookup"><span data-stu-id="2483d-193">The following code uses the **WnsService** instance exposed by the **NotificationHubService** to send a toast push notification to a UWP app:</span></span>

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a><span data-ttu-id="2483d-194">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2483d-194">Next Steps</span></span>
<span data-ttu-id="2483d-195">Os trechos de código de exemplo acima permitem que você crie com facilidade a infraestrutura de serviço para enviar notificações por push para uma ampla variedade de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="2483d-195">The sample snippets above allow you to easily build service infrastructure to deliver push notifications to a wide variety of devices.</span></span> <span data-ttu-id="2483d-196">Agora que você aprendeu os conceitos básicos do uso de Hubs de Notificação com o node.js, siga estes links para saber mais sobre como é possível estender ainda mais esses recursos.</span><span class="sxs-lookup"><span data-stu-id="2483d-196">Now that you've learned the basics of using Notification Hubs with node.js, follow these links to learn more about how you can extend these capabilities further.</span></span>

* <span data-ttu-id="2483d-197">Veja a Referência do MSDN para os [Hubs de Notificação do Azure](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span><span class="sxs-lookup"><span data-stu-id="2483d-197">See the MSDN Reference for [Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span></span>
* <span data-ttu-id="2483d-198">Visite o repositório [SDK do Azure para o Node] no GitHub para obter mais exemplos e detalhes de implementação.</span><span class="sxs-lookup"><span data-stu-id="2483d-198">Visit the [Azure SDK for Node] repository on GitHub for more samples and implementation details.</span></span>

<span data-ttu-id="2483d-199">[SDK do Azure para o Node]: https://github.com/WindowsAzure/azure-sdk-for-node</span><span class="sxs-lookup"><span data-stu-id="2483d-199">[Azure SDK for Node]: https://github.com/WindowsAzure/azure-sdk-for-node</span></span>
[Next Steps]: #nextsteps
[What are Service Bus Topics and Subscriptions?]: #what-are-service-bus-topics
[Create a Service Namespace]: #create-a-service-namespace
[Obtain the Default Management Credentials for the Namespace]: #obtain-default-credentials
[Create a Node.js Application]: #Create_a_Nodejs_Application
[Configure Your Application to Use Service Bus]: #Configure_Your_Application_to_Use_Service_Bus
[How to: Create a Topic]: #How_to_Create_a_Topic
[How to: Create Subscriptions]: #How_to_Create_Subscriptions
[How to: Send Messages to a Topic]: #How_to_Send_Messages_to_a_Topic
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
<span data-ttu-id="2483d-200">[Site com o WebMatrix]: /develop/nodejs/tutorials/web-site-with-webmatrix/</span><span class="sxs-lookup"><span data-stu-id="2483d-200">[Web Site with WebMatrix]: /develop/nodejs/tutorials/web-site-with-webmatrix/</span></span>
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Previous Management Portal]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/previous-portal.png
[nodejswebsite]: /develop/nodejs/tutorials/create-a-website-(mac)/
[Node.js Cloud Service with Storage]: /develop/nodejs/tutorials/web-app-with-storage/
[Node.js Web Application with Storage]: /develop/nodejs/tutorials/web-site-with-storage/
<span data-ttu-id="2483d-201">[Portal do Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="2483d-201">[Azure Portal]: https://portal.azure.com</span></span>
