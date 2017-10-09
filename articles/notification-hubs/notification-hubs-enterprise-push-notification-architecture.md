---
title: aaaNotification Hubs - arquitetura de Push
description: "Orientação sobre como usar os Hubs de Notificação do Azure em um ambiente corporativo"
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 903023e9-9347-442a-924b-663af85e05c6
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c3afb83de1ba0882bf99e10f38cca40cb42d07a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-push-architectural-guidance"></a><span data-ttu-id="dc005-103">Orientação arquitetural do push corporativo</span><span class="sxs-lookup"><span data-stu-id="dc005-103">Enterprise push architectural guidance</span></span>
<span data-ttu-id="dc005-104">As empresas hoje estão gradualmente migrando para a criação de aplicativos móveis para ambos os usuários finais (externo) ou para os funcionários de saudação (internos).</span><span class="sxs-lookup"><span data-stu-id="dc005-104">Enterprises today are gradually moving towards creating mobile applications for either their end users (external) or for hello employees (internal).</span></span> <span data-ttu-id="dc005-105">Eles têm sistemas de back-end existentes in-loco seja mainframes ou Olá de alguns aplicativos de LoB que devem ser integrados em arquitetura de aplicativos móveis.</span><span class="sxs-lookup"><span data-stu-id="dc005-105">They have existing backend systems in place be it mainframes or some LoB applications which must be integrated into hello mobile application architecture.</span></span> <span data-ttu-id="dc005-106">Este guia abordaremos a melhor maneira de toodo essa integração recomendando toocommon cenários de solução possível.</span><span class="sxs-lookup"><span data-stu-id="dc005-106">This guide will talk about how best toodo this integration recommending possible solution toocommon scenarios.</span></span>

<span data-ttu-id="dc005-107">É um requisito frequente para enviar por push usuários de toohello de notificação por meio de seu aplicativo móvel quando ocorre um evento de interesse em sistemas de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="dc005-107">A frequent requirement is for sending push notification toohello users through their mobile application when an event of interest occurs in hello backend systems.</span></span> <span data-ttu-id="dc005-108">Por exemplo</span><span class="sxs-lookup"><span data-stu-id="dc005-108">E.g.</span></span> <span data-ttu-id="dc005-109">um cliente do banco que tem o aplicativo de serviços bancários do banco de saudação em seu iPhone quer toobe notificado quando um débito fica acima de um determinado valor de sua conta ou um cenário de intranet onde quer que um funcionário do departamento de finanças que tem um aplicativo de aprovação de orçamento no seu Windows Phone toobe notificado quando ele recebe uma solicitação de aprovação.</span><span class="sxs-lookup"><span data-stu-id="dc005-109">a bank customer who has hello bank's banking app on her iPhone wants toobe notified when a debit is made above a certain amount from her account or an intranet scenario where an employee from finance department who has a budget approval app on his Windows Phone wants toobe notified when he gets an approval request.</span></span>

<span data-ttu-id="dc005-110">conta bancária de saudação ou processamento de aprovação é provavelmente toobe feita em algum sistema back-end que deve iniciar um usuário de toohello por push.</span><span class="sxs-lookup"><span data-stu-id="dc005-110">hello bank account or approval processing is likely toobe done in some backend system which must initiate a push toohello user.</span></span> <span data-ttu-id="dc005-111">Pode haver vários tal back-end sistemas que todos os devem criar hello mesmo tipo de envio por push tooimplement de lógica quando um evento dispara uma notificação.</span><span class="sxs-lookup"><span data-stu-id="dc005-111">There may be multiple such backend systems which must all build hello same kind of logic tooimplement push when an event triggers a notification.</span></span> <span data-ttu-id="dc005-112">complexidade de saudação aqui está na integração de vários sistemas de back-end junto com um sistema de envio por push único onde hello, os usuários finais podem se inscreveu toodifferent notificações e pode até mesmo ser vários aplicativos móveis, por exemplo, no caso de saudação de aplicativos móveis da intranet em que um aplicativo móvel pode ser tooreceive notificações de vários esses sistemas de back-end.</span><span class="sxs-lookup"><span data-stu-id="dc005-112">hello complexity here lies in integrating several backend systems together with a single push system where hello end users may have subscribed toodifferent notifications and there may even be multiple mobile applications e.g. in hello case of intranet mobile apps where one mobile application may want tooreceive notifications from multiple such backend systems.</span></span> <span data-ttu-id="dc005-113">sistemas de back-end Olá desconhecida ou não seja necessário tooknow semântica/tecnologia de envio por push para que uma solução comum aqui tradicionalmente toointroduce um componente que controla os sistemas de back-end Olá para todos os eventos de interesse e é responsável por enviar mensagens de saudação do envio cliente de toohello.</span><span class="sxs-lookup"><span data-stu-id="dc005-113">hello backend systems do not know or need tooknow of push semantics/technology so a common solution here traditionally has been toointroduce a component which polls hello backend systems for any events of interest and is responsible for sending hello push messages toohello client.</span></span>
<span data-ttu-id="dc005-114">Aqui, falaremos sobre uma solução ainda mais usando o barramento de serviço do Azure - modelo de tópico/assinatura que reduzirá a complexidade de saudação ao fazer a solução Olá escalonável.</span><span class="sxs-lookup"><span data-stu-id="dc005-114">Here we will talk about an even better solution using Azure Service Bus - Topic/Subscription model which will reduce hello complexity while making hello solution scalable.</span></span>

<span data-ttu-id="dc005-115">Aqui está a arquitetura geral Olá de solução de saudação (generalizado com vários aplicativos móveis mas igualmente aplicáveis quando há apenas um aplicativo móvel)</span><span class="sxs-lookup"><span data-stu-id="dc005-115">Here is hello general architecture of hello solution (generalized with multiple mobile apps but equally applicable when there is only one mobile app)</span></span>

## <a name="architecture"></a><span data-ttu-id="dc005-116">Arquitetura</span><span class="sxs-lookup"><span data-stu-id="dc005-116">Architecture</span></span>
![][1]

<span data-ttu-id="dc005-117">informação de chave de saudação neste diagrama de arquitetura é barramento de serviço do Azure que fornece um modelo de programação de tópicos/assinaturas (mais informações sobre ele no [programação do barramento de serviço Pub/Sub]).</span><span class="sxs-lookup"><span data-stu-id="dc005-117">hello key piece in this architectural diagram is Azure Service Bus which provides a topics/subscriptions programming model (more on it at [Service Bus Pub/Sub programming]).</span></span> <span data-ttu-id="dc005-118">destinatário Hello, que nesse caso, é o back-end de saudação móvel (normalmente [serviço móvel do Azure], que iniciará um push toohello os aplicativos móveis) não receber mensagens diretamente de sistemas de back-end hello, mas em vez disso, temos um camada de abstração intermediário fornecida pelo [Azure Service Bus] que permite que as mensagens de tooreceive móvel de back-end de um ou mais sistemas de back-end.</span><span class="sxs-lookup"><span data-stu-id="dc005-118">hello receiver, which in this case, is hello Mobile backend (typically [Azure Mobile Service], which will initiate a push toohello mobile apps) does not receive messages directly from hello backend systems but instead we have an intermediate abstraction layer provided by [Azure Service Bus] which enables mobile backend tooreceive messages from one or more backend systems.</span></span> <span data-ttu-id="dc005-119">Um tópico do barramento de serviço precisa toobe criado para cada Olá sistemas back-end, por exemplo, a conta, h, finanças, que são basicamente "tópicos" de interesse que iniciará toobe mensagens enviada como notificação por push.</span><span class="sxs-lookup"><span data-stu-id="dc005-119">A Service Bus Topic needs toobe created for each of hello backend systems e.g. Account, HR, Finance which are basically "topics" of interest which will initiate messages toobe sent as push notification.</span></span> <span data-ttu-id="dc005-120">sistemas de back-end Olá enviará mensagens tópicos toothese.</span><span class="sxs-lookup"><span data-stu-id="dc005-120">hello backend systems will send messages toothese topics.</span></span> <span data-ttu-id="dc005-121">Um back-end móveis podem se inscrever tooone ou mais tópicos criando uma assinatura do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="dc005-121">A Mobile Backend can subscribe tooone or more such topics by creating a Service Bus subscription.</span></span> <span data-ttu-id="dc005-122">Isso será intitular Olá móvel de back-end tooreceive uma notificação do sistema de back-end correspondente hello.</span><span class="sxs-lookup"><span data-stu-id="dc005-122">This will entitle hello mobile backend tooreceive a notification from hello corresponding backend system.</span></span> <span data-ttu-id="dc005-123">Back-end móvel continua toolisten para mensagens em suas assinaturas e assim que uma mensagem chega, ativa novamente e a envia como o hub de notificação de tooits de notificação.</span><span class="sxs-lookup"><span data-stu-id="dc005-123">Mobile backend continues toolisten for messages on their subscriptions and as soon as a message arrives, it turns back and sends it as notification tooits notification hub.</span></span> <span data-ttu-id="dc005-124">Hubs de notificação, em seguida, eventualmente a entrega de mensagem de saudação toohello aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="dc005-124">Notification hubs then eventually delivers hello message toohello mobile app.</span></span> <span data-ttu-id="dc005-125">Para componentes-chave toosummarize hello, temos:</span><span class="sxs-lookup"><span data-stu-id="dc005-125">So toosummarize hello key components, we have:</span></span>

1. <span data-ttu-id="dc005-126">Sistemas de back-end (sistemas de LoB/herdados)</span><span class="sxs-lookup"><span data-stu-id="dc005-126">Backend systems (LoB/Legacy systems)</span></span>
   * <span data-ttu-id="dc005-127">Cria um tópico do barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="dc005-127">Creates Service Bus Topic</span></span>
   * <span data-ttu-id="dc005-128">Envia mensagem</span><span class="sxs-lookup"><span data-stu-id="dc005-128">Sends Message</span></span>
2. <span data-ttu-id="dc005-129">Back-end móvel</span><span class="sxs-lookup"><span data-stu-id="dc005-129">Mobile backend</span></span>
   * <span data-ttu-id="dc005-130">Cria a assinatura do serviço</span><span class="sxs-lookup"><span data-stu-id="dc005-130">Creates Service Subscription</span></span>
   * <span data-ttu-id="dc005-131">Recebe uma mensagem (do sistema de back-end)</span><span class="sxs-lookup"><span data-stu-id="dc005-131">Receives Message (from Backend system)</span></span>
   * <span data-ttu-id="dc005-132">Envia notificação tooclients (por meio do Hub de notificação do Azure)</span><span class="sxs-lookup"><span data-stu-id="dc005-132">Sends notification tooclients (via Azure Notification Hub)</span></span>
3. <span data-ttu-id="dc005-133">Aplicativo Móvel</span><span class="sxs-lookup"><span data-stu-id="dc005-133">Mobile Application</span></span>
   * <span data-ttu-id="dc005-134">Recebe e exibe a notificação</span><span class="sxs-lookup"><span data-stu-id="dc005-134">Receives and display notification</span></span>

### <a name="benefits"></a><span data-ttu-id="dc005-135">Benefícios:</span><span class="sxs-lookup"><span data-stu-id="dc005-135">Benefits:</span></span>
1. <span data-ttu-id="dc005-136">Olá desacoplamento entre receptor hello (aplicativo/serviço móvel por meio do Hub de notificação) e o remetente (sistemas de back-end) permite que os sistemas de back-end adicionais sendo integrados com o mínimo de alterações.</span><span class="sxs-lookup"><span data-stu-id="dc005-136">hello decoupling between hello receiver (mobile app/service via Notification Hub) and sender (backend systems) enables additional backend systems being integrated with minimal change.</span></span>
2. <span data-ttu-id="dc005-137">Isso também facilita o cenário de saudação de vários aplicativos móveis sendo tooreceive capaz de eventos de um ou mais sistemas de back-end.</span><span class="sxs-lookup"><span data-stu-id="dc005-137">This also makes hello scenario of multiple mobile apps being able tooreceive events from one or more backend systems.</span></span>  

## <a name="sample"></a><span data-ttu-id="dc005-138">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="dc005-138">Sample:</span></span>
### <a name="prerequisites"></a><span data-ttu-id="dc005-139">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="dc005-139">Prerequisites</span></span>
<span data-ttu-id="dc005-140">Você deve concluir Olá tutoriais toofamiliarize com conceitos de hello, bem como etapas comuns de criação e configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="dc005-140">You should complete hello following tutorials toofamiliarize with hello concepts as well as common creation & configuration steps:</span></span>

1. <span data-ttu-id="dc005-141">[programação do barramento de serviço Pub/Sub] -explica detalhes de saudação do trabalho com assinaturas/tópicos do barramento do serviço, como um namespace de toocreate toocontain tópicos/assinaturas, como toosend & receber mensagens dela.</span><span class="sxs-lookup"><span data-stu-id="dc005-141">[Service Bus Pub/Sub programming] - This explains hello details of working with Service Bus Topics/Subscriptions, how toocreate a namespace toocontain topics/subscriptions, how toosend & receive messages from them.</span></span>
2. <span data-ttu-id="dc005-142">[Hubs de notificação - Windows Universal tutorial] -explica como tooset um aplicativo da Windows Store e usar tooregister de Hubs de notificação e, em seguida, receber notificações.</span><span class="sxs-lookup"><span data-stu-id="dc005-142">[Notification Hubs - Windows Universal tutorial] - This explains how tooset up a Windows Store app and use Notification Hubs tooregister and then receive notifications.</span></span>

### <a name="sample-code"></a><span data-ttu-id="dc005-143">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="dc005-143">Sample code</span></span>
<span data-ttu-id="dc005-144">Olá código de exemplo completo está disponível em [exemplos de Hub de notificação].</span><span class="sxs-lookup"><span data-stu-id="dc005-144">hello full sample code is available at [Notification Hub Samples].</span></span> <span data-ttu-id="dc005-145">Ele é dividido em três componentes:</span><span class="sxs-lookup"><span data-stu-id="dc005-145">It is split into three components:</span></span>

1. <span data-ttu-id="dc005-146">**EnterprisePushBackendSystem**</span><span class="sxs-lookup"><span data-stu-id="dc005-146">**EnterprisePushBackendSystem**</span></span>
   
    <span data-ttu-id="dc005-147">a.</span><span class="sxs-lookup"><span data-stu-id="dc005-147">a.</span></span> <span data-ttu-id="dc005-148">Este projeto usa Olá *windowsazure. ServiceBus* pacote Nuget e é baseada em [programação do barramento de serviço Pub/Sub].</span><span class="sxs-lookup"><span data-stu-id="dc005-148">This project uses hello *WindowsAzure.ServiceBus* Nuget package and is  based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="dc005-149">b.</span><span class="sxs-lookup"><span data-stu-id="dc005-149">b.</span></span> <span data-ttu-id="dc005-150">Este é um simples c# console aplicativo toosimulate um sistema LoB, que inicia toobe de mensagem de saudação entregue o aplicativo móvel toohello.</span><span class="sxs-lookup"><span data-stu-id="dc005-150">This is a simple C# console app toosimulate an LoB system which initiates hello message toobe delivered toohello mobile app.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello topic where we will send notifications
            CreateTopic(connectionString);
   
            // Send message
            SendMessage(connectionString);
        }
   
    <span data-ttu-id="dc005-151">c.</span><span class="sxs-lookup"><span data-stu-id="dc005-151">c.</span></span> <span data-ttu-id="dc005-152">`CreateTopic`é o tópico de barramento de serviço Olá toocreate usado onde podemos enviará mensagens.</span><span class="sxs-lookup"><span data-stu-id="dc005-152">`CreateTopic` is used toocreate hello Service Bus topic where we will send messages.</span></span>
   
        public static void CreateTopic(string connectionString)
        {
            // Create hello topic if it does not exist already
   
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.TopicExists(sampleTopic))
            {
                namespaceManager.CreateTopic(sampleTopic);
            }
        }
   
    <span data-ttu-id="dc005-153">d.</span><span class="sxs-lookup"><span data-stu-id="dc005-153">d.</span></span> <span data-ttu-id="dc005-154">`SendMessage`é usado toosend Olá mensagens toothis tópico do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="dc005-154">`SendMessage` is used toosend hello messages toothis Service Bus Topic.</span></span> <span data-ttu-id="dc005-155">Aqui, simplesmente está enviando um conjunto de tópico de toohello mensagens aleatória periodicamente para finalidade de saudação do exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="dc005-155">Here we are simply sending a set of random messages toohello topic periodically for hello purpose of hello sample.</span></span> <span data-ttu-id="dc005-156">Normalmente haverá um sistema de back-end que enviará mensagens quando ocorre um evento.</span><span class="sxs-lookup"><span data-stu-id="dc005-156">Normally there will be a backend system which will send messages when an event occurs.</span></span>
   
        public static void SendMessage(string connectionString)
        {
            TopicClient client =
                TopicClient.CreateFromConnectionString(connectionString, sampleTopic);
   
            // Sends random messages every 10 seconds toohello topic
            string[] messages =
            {
                "Employee Id '{0}' has joined.",
                "Employee Id '{0}' has left.",
                "Employee Id '{0}' has switched tooa different team."
            };
   
            while (true)
            {
                Random rnd = new Random();
                string employeeId = rnd.Next(10000, 99999).ToString();
                string notification = String.Format(messages[rnd.Next(0,messages.Length)], employeeId);
   
                // Send Notification
                BrokeredMessage message = new BrokeredMessage(notification);
                client.Send(message);
   
                Console.WriteLine("{0} Message sent - '{1}'", DateTime.Now, notification);
   
                System.Threading.Thread.Sleep(new TimeSpan(0, 0, 10));
            }
        }
2. <span data-ttu-id="dc005-157">**ReceiveAndSendNotification**</span><span class="sxs-lookup"><span data-stu-id="dc005-157">**ReceiveAndSendNotification**</span></span>
   
    <span data-ttu-id="dc005-158">a.</span><span class="sxs-lookup"><span data-stu-id="dc005-158">a.</span></span> <span data-ttu-id="dc005-159">Este projeto usa Olá *windowsazure. ServiceBus* e *Microsoft.Web.WebJobs.Publish* Nuget pacotes e é baseada em [programação do barramento de serviço Pub/Sub].</span><span class="sxs-lookup"><span data-stu-id="dc005-159">This project uses hello *WindowsAzure.ServiceBus* and *Microsoft.Web.WebJobs.Publish* Nuget packages and is based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="dc005-160">b.</span><span class="sxs-lookup"><span data-stu-id="dc005-160">b.</span></span> <span data-ttu-id="dc005-161">Este é outro console aplicativo c# que iremos executar como um [Azure WebJob] porque ele tem toorun continuamente toolisten para mensagens de sistemas de LoB/back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="dc005-161">This is another C# console app which we will run as an [Azure WebJob] since it has toorun continuously toolisten for messages from hello LoB/backend systems.</span></span> <span data-ttu-id="dc005-162">Isso fará parte do back-end do celular.</span><span class="sxs-lookup"><span data-stu-id="dc005-162">This will be part of your Mobile backend.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                     CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello subscription which will receive messages
            CreateSubscription(connectionString);
   
            // Receive message
            ReceiveMessageAndSendNotification(connectionString);
        }
   
    <span data-ttu-id="dc005-163">c.</span><span class="sxs-lookup"><span data-stu-id="dc005-163">c.</span></span> <span data-ttu-id="dc005-164">`CreateSubscription`é usado toocreate uma assinatura do barramento de serviço para o tópico Olá onde o sistema de back-end Olá enviará mensagens.</span><span class="sxs-lookup"><span data-stu-id="dc005-164">`CreateSubscription` is used toocreate a Service Bus subscription for hello topic where hello backend system will send messages.</span></span> <span data-ttu-id="dc005-165">Dependendo do cenário de negócios hello, esse componente criará uma ou mais assinaturas tópicos toocorresponding (por exemplo, alguns podem receber mensagens do sistema de RH, alguns a partir do sistema de finanças e assim por diante)</span><span class="sxs-lookup"><span data-stu-id="dc005-165">Depending on hello business scenario, this component will create one or more subscriptions toocorresponding topics (e.g. some may be receiving messages from HR system, some from Finance system, and so on)</span></span>
   
        static void CreateSubscription(string connectionString)
        {
            // Create hello subscription if it does not exist already
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.SubscriptionExists(sampleTopic, sampleSubscription))
            {
                namespaceManager.CreateSubscription(sampleTopic, sampleSubscription);
            }
        }
   
    <span data-ttu-id="dc005-166">d.</span><span class="sxs-lookup"><span data-stu-id="dc005-166">d.</span></span> <span data-ttu-id="dc005-167">ReceiveMessageAndSendNotification é tooread usado a mensagem de saudação do tópico hello usando sua assinatura e se Olá leitura for bem-sucedida, em seguida, criar um toohello toobe enviado de notificação (no cenário de exemplo hello uma notificação de sistema nativo do Windows) móvel aplicativo usando os Hubs de notificação do Azure.</span><span class="sxs-lookup"><span data-stu-id="dc005-167">ReceiveMessageAndSendNotification is used tooread hello message from hello topic using its subscription and if hello read is successful then craft a notification (in hello sample scenario a Windows native toast notification) toobe sent toohello mobile application using Azure Notification Hubs.</span></span>
   
        static void ReceiveMessageAndSendNotification(string connectionString)
        {
            // Initialize hello Notification Hub
            string hubConnectionString = CloudConfigurationManager.GetSetting
                    ("Microsoft.NotificationHub.ConnectionString");
            hub = NotificationHubClient.CreateClientFromConnectionString
                    (hubConnectionString, "enterprisepushservicehub");
   
            SubscriptionClient Client =
                SubscriptionClient.CreateFromConnectionString
                        (connectionString, sampleTopic, sampleSubscription);
   
            Client.Receive();
   
            // Continuously process messages received from hello subscription
            while (true)
            {
                BrokeredMessage message = Client.Receive();
                var toastMessage = @"<toast><visual><binding template=""ToastText01""><text id=""1"">{messagepayload}</text></binding></visual></toast>";
   
                if (message != null)
                {
                    try
                    {
                        Console.WriteLine(message.MessageId);
                        Console.WriteLine(message.SequenceNumber);
                        string messageBody = message.GetBody<string>();
                        Console.WriteLine("Body: " + messageBody + "\n");
   
                        toastMessage = toastMessage.Replace("{messagepayload}", messageBody);
                        SendNotificationAsync(toastMessage);
   
                        // Remove message from subscription
                        message.Complete();
                    }
                    catch (Exception)
                    {
                        // Indicate a problem, unlock message in subscription
                        message.Abandon();
                    }
                }
            }
        }
        static async void SendNotificationAsync(string message)
        {
            await hub.SendWindowsNativeNotificationAsync(message);
        }
   
    <span data-ttu-id="dc005-168">e.</span><span class="sxs-lookup"><span data-stu-id="dc005-168">e.</span></span> <span data-ttu-id="dc005-169">Para publicar como uma **WebJob**, clique com o botão direito na solução Olá no Visual Studio e selecione **Publicar como WebJob**</span><span class="sxs-lookup"><span data-stu-id="dc005-169">For publishing this as a **WebJob**, right click on hello solution in Visual Studio and select **Publish as WebJob**</span></span>
   
    ![][2]
   
    <span data-ttu-id="dc005-170">f.</span><span class="sxs-lookup"><span data-stu-id="dc005-170">f.</span></span> <span data-ttu-id="dc005-171">Selecione o perfil de publicação e criar um novo site do Azure, se ele não existir já que irá hospedar esse trabalho Web e uma vez que o site de hello, em seguida, **publicar**.</span><span class="sxs-lookup"><span data-stu-id="dc005-171">Select your publishing profile and create a new Azure WebSite if it doesnt exist already which will host this WebJob and once you have hello WebSite then **Publish**.</span></span>
   
    ![][3]
   
    <span data-ttu-id="dc005-172">g.</span><span class="sxs-lookup"><span data-stu-id="dc005-172">g.</span></span> <span data-ttu-id="dc005-173">Configurar hello "Executar continuamente" toobe de trabalho de forma que ao fazer logon em toohello [Portal clássico do Azure] você verá algo parecido com hello seguinte:</span><span class="sxs-lookup"><span data-stu-id="dc005-173">Configure hello job toobe "Run Continuously" so that when you log in toohello [Azure Classic Portal] you should see something like hello following:</span></span>
   
    ![][4]
3. <span data-ttu-id="dc005-174">**EnterprisePushMobileApp**</span><span class="sxs-lookup"><span data-stu-id="dc005-174">**EnterprisePushMobileApp**</span></span>
   
    <span data-ttu-id="dc005-175">a.</span><span class="sxs-lookup"><span data-stu-id="dc005-175">a.</span></span> <span data-ttu-id="dc005-176">Este é um aplicativo da Windows Store que vai receber notificações do sistema de execução do trabalho Web hello como parte do seu back-end móvel e exibi-lo.</span><span class="sxs-lookup"><span data-stu-id="dc005-176">This is a Windows Store application which will receive toast notifications from hello WebJob running as part of your Mobile backend and display it.</span></span> <span data-ttu-id="dc005-177">Isso se baseia em [Hubs de notificação - Windows Universal tutorial].</span><span class="sxs-lookup"><span data-stu-id="dc005-177">This is based on [Notification Hubs - Windows Universal tutorial].</span></span>  
   
    <span data-ttu-id="dc005-178">b.</span><span class="sxs-lookup"><span data-stu-id="dc005-178">b.</span></span> <span data-ttu-id="dc005-179">Certifique-se de que seu aplicativo está habilitado tooreceive notificações do sistema.</span><span class="sxs-lookup"><span data-stu-id="dc005-179">Ensure that your application is enabled tooreceive toast notifications.</span></span>
   
    <span data-ttu-id="dc005-180">c.</span><span class="sxs-lookup"><span data-stu-id="dc005-180">c.</span></span> <span data-ttu-id="dc005-181">Certifique-se de que Olá após o código de registro de Hubs de notificação está sendo chamado em Olá aplicativo Iniciar backup (depois de substituir Olá *HubName* e *DefaultListenSharedAccessSignature*:</span><span class="sxs-lookup"><span data-stu-id="dc005-181">Ensure that hello following Notification Hubs registration code is being called at hello App start up (after replacing hello *HubName* and *DefaultListenSharedAccessSignature*:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("[HubName]", "[DefaultListenSharedAccessSignature]");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

### <a name="running-sample"></a><span data-ttu-id="dc005-182">Exemplo de execução:</span><span class="sxs-lookup"><span data-stu-id="dc005-182">Running sample:</span></span>
1. <span data-ttu-id="dc005-183">Certifique-se de que seu trabalho Web está em execução com êxito e agendado muito "executar continuamente".</span><span class="sxs-lookup"><span data-stu-id="dc005-183">Ensure that your WebJob is running successfully and scheduled too"Run Continuously".</span></span>
2. <span data-ttu-id="dc005-184">Executar Olá **EnterprisePushMobileApp** que iniciará o aplicativo da Windows Store hello.</span><span class="sxs-lookup"><span data-stu-id="dc005-184">Run hello **EnterprisePushMobileApp** which will start hello Windows Store app.</span></span>
3. <span data-ttu-id="dc005-185">Executar Olá **EnterprisePushBackendSystem** aplicativo de console que simulará back-end de LoB hello e começar a enviar mensagens e você deverá ver notificações do sistema que aparecem como Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="dc005-185">Run hello **EnterprisePushBackendSystem** console application which will simulate hello LoB backend and will start sending messages and you should see toast notifications appearing like hello following:</span></span>
   
    ![][5]
4. <span data-ttu-id="dc005-186">mensagens de saudação foram enviadas originalmente tópicos do barramento tooService que estava sendo monitorado por assinaturas do barramento de serviço no seu trabalho Web.</span><span class="sxs-lookup"><span data-stu-id="dc005-186">hello messages were originally sent tooService Bus topics which was being monitored by Service Bus subscriptions in your Web Job.</span></span> <span data-ttu-id="dc005-187">Depois que uma mensagem foi recebida, uma notificação foi criada e enviada toohello aplicativos para dispositivos móveis.</span><span class="sxs-lookup"><span data-stu-id="dc005-187">Once a message was received, a notification was created and sent toohello mobile app.</span></span> <span data-ttu-id="dc005-188">Examinar Olá WebJob logs tooconfirm Olá processamento quando você for toohello Logs link no [Portal clássico do Azure] para seu trabalho Web:</span><span class="sxs-lookup"><span data-stu-id="dc005-188">You can look through hello WebJob logs tooconfirm hello processing when you go toohello Logs link in [Azure Classic Portal] for your Web Job:</span></span>
   
    ![][6]

<!-- Images -->
[1]: ./media/notification-hubs-enterprise-push-architecture/architecture.png
[2]: ./media/notification-hubs-enterprise-push-architecture/WebJobsContextMenu.png
[3]: ./media/notification-hubs-enterprise-push-architecture/PublishAsWebJob.png
[4]: ./media/notification-hubs-enterprise-push-architecture/WebJob.png
[5]: ./media/notification-hubs-enterprise-push-architecture/Notifications.png
[6]: ./media/notification-hubs-enterprise-push-architecture/WebJobsLog.png

<!-- Links -->
[exemplos de Hub de notificação]: https://github.com/Azure/azure-notificationhubs-samples
[serviço móvel do Azure]: http://azure.microsoft.com/documentation/services/mobile-services/
[Azure Service Bus]: http://azure.microsoft.com/documentation/articles/fundamentals-service-bus-hybrid-solutions/
[programação do barramento de serviço Pub/Sub]: http://azure.microsoft.com/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/
[Azure WebJob]: http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/
[Hubs de notificação - Windows Universal tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/
[Portal clássico do Azure]: https://manage.windowsazure.com/
