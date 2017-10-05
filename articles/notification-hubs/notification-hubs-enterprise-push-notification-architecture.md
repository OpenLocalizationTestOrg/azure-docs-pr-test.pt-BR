---
title: "Hubs de notificação - Arquitetura de Push Corporativo"
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
ms.openlocfilehash: ae7c1c9644ecfe7fe4ad6e332cc0683a3b5df22f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="enterprise-push-architectural-guidance"></a><span data-ttu-id="92f78-103">Orientação arquitetural do push corporativo</span><span class="sxs-lookup"><span data-stu-id="92f78-103">Enterprise push architectural guidance</span></span>
<span data-ttu-id="92f78-104">As empresas hoje estão gradualmente migrando para a criação de aplicativos móveis para os usuários finais (externos) ou para os funcionários (internos).</span><span class="sxs-lookup"><span data-stu-id="92f78-104">Enterprises today are gradually moving towards creating mobile applications for either their end users (external) or for the employees (internal).</span></span> <span data-ttu-id="92f78-105">Eles têm sistemas de back-end no local como mainframes ou alguns aplicativos LoB que devem ser integrados na arquitetura de aplicativos móveis.</span><span class="sxs-lookup"><span data-stu-id="92f78-105">They have existing backend systems in place be it mainframes or some LoB applications which must be integrated into the mobile application architecture.</span></span> <span data-ttu-id="92f78-106">Este guia falará sobre a melhor maneira de fazer essa integração recomendado a melhor solução para cenários comuns.</span><span class="sxs-lookup"><span data-stu-id="92f78-106">This guide will talk about how best to do this integration recommending possible solution to common scenarios.</span></span>

<span data-ttu-id="92f78-107">Um requisito frequente é enviar notificação por push para os usuários através de seus aplicativos móveis quando ocorre um evento de interesse nos sistemas de back-end.</span><span class="sxs-lookup"><span data-stu-id="92f78-107">A frequent requirement is for sending push notification to the users through their mobile application when an event of interest occurs in the backend systems.</span></span> <span data-ttu-id="92f78-108">Por exemplo</span><span class="sxs-lookup"><span data-stu-id="92f78-108">E.g.</span></span> <span data-ttu-id="92f78-109">Um cliente bancário que tenha o aplicativo de serviços bancários do banco em seu iPhone deseja ser notificado quando um débito fica acima de um determinado valor de sua conta ou um cenário de intranet em que um funcionário do departamento financeiro com um aplicativo de aprovação de orçamento em seu Windows Phone deseja ser notificado quando ele recebe uma solicitação de aprovação.</span><span class="sxs-lookup"><span data-stu-id="92f78-109">a bank customer who has the bank's banking app on her iPhone wants to be notified when a debit is made above a certain amount from her account or an intranet scenario where an employee from finance department who has a budget approval app on his Windows Phone wants to be notified when he gets an approval request.</span></span>

<span data-ttu-id="92f78-110">A conta bancária ou o processamento de aprovação provavelmente pode ser feito em algum sistema back-end que deve iniciar um envio por push para o usuário.</span><span class="sxs-lookup"><span data-stu-id="92f78-110">The bank account or approval processing is likely to be done in some backend system which must initiate a push to the user.</span></span> <span data-ttu-id="92f78-111">Poderá haver vários sistemas de back-end e todos deverão compilar o mesmo tipo de lógica para implementar push quando um evento disparar uma notificação.</span><span class="sxs-lookup"><span data-stu-id="92f78-111">There may be multiple such backend systems which must all build the same kind of logic to implement push when an event triggers a notification.</span></span> <span data-ttu-id="92f78-112">A complexidade aqui reside na integração de vários sistemas de back-end com sistemas individuais de envio por push, nos quais os usuários finais podem se inscrever para diferentes notificações e pode até mesmo haver vários aplicativos móveis, por exemplo, no caso de aplicativos móveis de intranet nos quais um aplicativo móvel talvez queira receber notificações de vários sistemas de back-end.</span><span class="sxs-lookup"><span data-stu-id="92f78-112">The complexity here lies in integrating several backend systems together with a single push system where the end users may have subscribed to different notifications and there may even be multiple mobile applications e.g. in the case of intranet mobile apps where one mobile application may want to receive notifications from multiple such backend systems.</span></span> <span data-ttu-id="92f78-113">Os sistemas de back-end não sabem nem precisam saber de tecnologia/semântica de push para que uma solução comum aqui tem sido tradicionalmente para introduzir um componente que controla os sistemas de back-end para todos os eventos de interesse e é responsável por enviar as mensagens por push para o cliente.</span><span class="sxs-lookup"><span data-stu-id="92f78-113">The backend systems do not know or need to know of push semantics/technology so a common solution here traditionally has been to introduce a component which polls the backend systems for any events of interest and is responsible for sending the push messages to the client.</span></span>
<span data-ttu-id="92f78-114">Aqui falaremos sobre uma solução ainda melhor usando o Barramento de Serviço do Azure - modelo de Tópico/Assinatura que reduzirá a complexidade, tornando a solução escalonável.</span><span class="sxs-lookup"><span data-stu-id="92f78-114">Here we will talk about an even better solution using Azure Service Bus - Topic/Subscription model which will reduce the complexity while making the solution scalable.</span></span>

<span data-ttu-id="92f78-115">Esta é a arquitetura geral da solução (generalizado com vários aplicativos móveis, mas igualmente aplicável quando há apenas um aplicativo móvel)</span><span class="sxs-lookup"><span data-stu-id="92f78-115">Here is the general architecture of the solution (generalized with multiple mobile apps but equally applicable when there is only one mobile app)</span></span>

## <a name="architecture"></a><span data-ttu-id="92f78-116">Arquitetura</span><span class="sxs-lookup"><span data-stu-id="92f78-116">Architecture</span></span>
![][1]

<span data-ttu-id="92f78-117">A parte mais importante neste diagrama de arquitetura é o Barramento de Serviço do Azure que fornece um modelo de programação de tópicos/assinaturas (falaremos mais sobre isso em [Programação Pub/Sub do Barramento de Serviço]).</span><span class="sxs-lookup"><span data-stu-id="92f78-117">The key piece in this architectural diagram is Azure Service Bus which provides a topics/subscriptions programming model (more on it at [Service Bus Pub/Sub programming]).</span></span> <span data-ttu-id="92f78-118">O receptor, que nesse caso, é o back-end móvel (normalment, [Serviço Móvel do Azure], que iniciará um envio por push para os aplicativos móveis) não recebe mensagens diretamente dos sistemas de back-end, mas em vez disso, temos uma camada de abstração intermediária fornecida pelo [Barramento de Serviço do Azure], que permite que o back-end móvel receba mensagens de um ou mais sistemas de back-end.</span><span class="sxs-lookup"><span data-stu-id="92f78-118">The receiver, which in this case, is the Mobile backend (typically [Azure Mobile Service], which will initiate a push to the mobile apps) does not receive messages directly from the backend systems but instead we have an intermediate abstraction layer provided by [Azure Service Bus] which enables mobile backend to receive messages from one or more backend systems.</span></span> <span data-ttu-id="92f78-119">Um Tópico do Barramento de Serviço precisa ser criada para cada um dos sistemas de back-end, por exemplo, Conta, RH, Finanças, que são basicamente "tópicos" de interesse que iniciarão o envio de mensagens como notificação por push.</span><span class="sxs-lookup"><span data-stu-id="92f78-119">A Service Bus Topic needs to be created for each of the backend systems e.g. Account, HR, Finance which are basically "topics" of interest which will initiate messages to be sent as push notification.</span></span> <span data-ttu-id="92f78-120">Os sistemas de back-end enviarão mensagens para esses tópicos.</span><span class="sxs-lookup"><span data-stu-id="92f78-120">The backend systems will send messages to these topics.</span></span> <span data-ttu-id="92f78-121">Um Back-end Móvel pode assinar um ou mais tópicos criando uma assinatura do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="92f78-121">A Mobile Backend can subscribe to one or more such topics by creating a Service Bus subscription.</span></span> <span data-ttu-id="92f78-122">Isso permitirá que o back-end móvel receba uma notificação do sistema de back-end correspondente.</span><span class="sxs-lookup"><span data-stu-id="92f78-122">This will entitle the mobile backend to receive a notification from the corresponding backend system.</span></span> <span data-ttu-id="92f78-123">O back-end móvel continua a escutar mensagens em suas assinaturas e, assim que uma mensagem chega, ela volta e é enviada como notificação para seu hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="92f78-123">Mobile backend continues to listen for messages on their subscriptions and as soon as a message arrives, it turns back and sends it as notification to its notification hub.</span></span> <span data-ttu-id="92f78-124">Os hubs de notificação eventualmente entregam a mensagem para o aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="92f78-124">Notification hubs then eventually delivers the message to the mobile app.</span></span> <span data-ttu-id="92f78-125">Portanto, para resumir os principais componentes, nós temos:</span><span class="sxs-lookup"><span data-stu-id="92f78-125">So to summarize the key components, we have:</span></span>

1. <span data-ttu-id="92f78-126">Sistemas de back-end (sistemas de LoB/herdados)</span><span class="sxs-lookup"><span data-stu-id="92f78-126">Backend systems (LoB/Legacy systems)</span></span>
   * <span data-ttu-id="92f78-127">Cria um tópico do barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="92f78-127">Creates Service Bus Topic</span></span>
   * <span data-ttu-id="92f78-128">Envia mensagem</span><span class="sxs-lookup"><span data-stu-id="92f78-128">Sends Message</span></span>
2. <span data-ttu-id="92f78-129">Back-end móvel</span><span class="sxs-lookup"><span data-stu-id="92f78-129">Mobile backend</span></span>
   * <span data-ttu-id="92f78-130">Cria a assinatura do serviço</span><span class="sxs-lookup"><span data-stu-id="92f78-130">Creates Service Subscription</span></span>
   * <span data-ttu-id="92f78-131">Recebe uma mensagem (do sistema de back-end)</span><span class="sxs-lookup"><span data-stu-id="92f78-131">Receives Message (from Backend system)</span></span>
   * <span data-ttu-id="92f78-132">Envia uma notificação para os clientes (via Hub de Notificação do Azure)</span><span class="sxs-lookup"><span data-stu-id="92f78-132">Sends notification to clients (via Azure Notification Hub)</span></span>
3. <span data-ttu-id="92f78-133">Aplicativo Móvel</span><span class="sxs-lookup"><span data-stu-id="92f78-133">Mobile Application</span></span>
   * <span data-ttu-id="92f78-134">Recebe e exibe a notificação</span><span class="sxs-lookup"><span data-stu-id="92f78-134">Receives and display notification</span></span>

### <a name="benefits"></a><span data-ttu-id="92f78-135">Benefícios:</span><span class="sxs-lookup"><span data-stu-id="92f78-135">Benefits:</span></span>
1. <span data-ttu-id="92f78-136">A separação entre o receptor (aplicativo/serviço móvel via Hub de Notificação) e o remetente (sistemas de back-end) permite que os sistemas de back-end adicionais sejam integrados com alterações mínimas.</span><span class="sxs-lookup"><span data-stu-id="92f78-136">The decoupling between the receiver (mobile app/service via Notification Hub) and sender (backend systems) enables additional backend systems being integrated with minimal change.</span></span>
2. <span data-ttu-id="92f78-137">Isso também torna o cenário de vários aplicativos móveis, sendo capaz de receber eventos de um ou mais sistemas de back-end.</span><span class="sxs-lookup"><span data-stu-id="92f78-137">This also makes the scenario of multiple mobile apps being able to receive events from one or more backend systems.</span></span>  

## <a name="sample"></a><span data-ttu-id="92f78-138">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="92f78-138">Sample:</span></span>
### <a name="prerequisites"></a><span data-ttu-id="92f78-139">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="92f78-139">Prerequisites</span></span>
<span data-ttu-id="92f78-140">Você deve concluir os tutoriais a seguir para se familiarizar com os conceitos, bem como etapas de criação e configuração comuns:</span><span class="sxs-lookup"><span data-stu-id="92f78-140">You should complete the following tutorials to familiarize with the concepts as well as common creation & configuration steps:</span></span>

1. <span data-ttu-id="92f78-141">[Programação Pub/Sub do Barramento de Serviço] - explica os detalhes de como trabalhar com Tópicos/Assinaturas do Barramento de Serviço, como criar um namespace para conter tópicos/assinaturas e como enviar e receber mensagens deles.</span><span class="sxs-lookup"><span data-stu-id="92f78-141">[Service Bus Pub/Sub programming] - This explains the details of working with Service Bus Topics/Subscriptions, how to create a namespace to contain topics/subscriptions, how to send & receive messages from them.</span></span>
2. <span data-ttu-id="92f78-142">[Hubs de Notificação - tutorial do Windows Universal] - isso explica como configurar um aplicativo da Windows Store e usar Hubs de Notificação para se registrar e receber notificações.</span><span class="sxs-lookup"><span data-stu-id="92f78-142">[Notification Hubs - Windows Universal tutorial] - This explains how to set up a Windows Store app and use Notification Hubs to register and then receive notifications.</span></span>

### <a name="sample-code"></a><span data-ttu-id="92f78-143">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="92f78-143">Sample code</span></span>
<span data-ttu-id="92f78-144">O código de exemplo completo está disponível em [Exemplos do Hub de Notificação].</span><span class="sxs-lookup"><span data-stu-id="92f78-144">The full sample code is available at [Notification Hub Samples].</span></span> <span data-ttu-id="92f78-145">Ele é dividido em três componentes:</span><span class="sxs-lookup"><span data-stu-id="92f78-145">It is split into three components:</span></span>

1. <span data-ttu-id="92f78-146">**EnterprisePushBackendSystem**</span><span class="sxs-lookup"><span data-stu-id="92f78-146">**EnterprisePushBackendSystem**</span></span>
   
    <span data-ttu-id="92f78-147">a.</span><span class="sxs-lookup"><span data-stu-id="92f78-147">a.</span></span> <span data-ttu-id="92f78-148">Esse projeto usa o pacote *WindowsAzure.ServiceBus* do Nuget e é baseado na [Programação Pub/Sub do Barramento de Serviço].</span><span class="sxs-lookup"><span data-stu-id="92f78-148">This project uses the *WindowsAzure.ServiceBus* Nuget package and is  based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="92f78-149">b.</span><span class="sxs-lookup"><span data-stu-id="92f78-149">b.</span></span> <span data-ttu-id="92f78-150">Isso é um console de aplicativo em C# simples para simular um sistema LoB que inicia a mensagem a ser entregue ao aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="92f78-150">This is a simple C# console app to simulate an LoB system which initiates the message to be delivered to the mobile app.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create the topic where we will send notifications
            CreateTopic(connectionString);
   
            // Send message
            SendMessage(connectionString);
        }
   
    <span data-ttu-id="92f78-151">c.</span><span class="sxs-lookup"><span data-stu-id="92f78-151">c.</span></span> <span data-ttu-id="92f78-152">`CreateTopic` é usado para criar o tópico do Barramento de Serviço, no qual poderemos enviar mensagens.</span><span class="sxs-lookup"><span data-stu-id="92f78-152">`CreateTopic` is used to create the Service Bus topic where we will send messages.</span></span>
   
        public static void CreateTopic(string connectionString)
        {
            // Create the topic if it does not exist already
   
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.TopicExists(sampleTopic))
            {
                namespaceManager.CreateTopic(sampleTopic);
            }
        }
   
    <span data-ttu-id="92f78-153">d.</span><span class="sxs-lookup"><span data-stu-id="92f78-153">d.</span></span> <span data-ttu-id="92f78-154">`SendMessage` é usado para enviar as mensagens para esse Tópico do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="92f78-154">`SendMessage` is used to send the messages to this Service Bus Topic.</span></span> <span data-ttu-id="92f78-155">Aqui podemos simplesmente enviar um conjunto de mensagens aleatórias para o tópico periodicamente para fins de exemplo.</span><span class="sxs-lookup"><span data-stu-id="92f78-155">Here we are simply sending a set of random messages to the topic periodically for the purpose of the sample.</span></span> <span data-ttu-id="92f78-156">Normalmente haverá um sistema de back-end que enviará mensagens quando ocorre um evento.</span><span class="sxs-lookup"><span data-stu-id="92f78-156">Normally there will be a backend system which will send messages when an event occurs.</span></span>
   
        public static void SendMessage(string connectionString)
        {
            TopicClient client =
                TopicClient.CreateFromConnectionString(connectionString, sampleTopic);
   
            // Sends random messages every 10 seconds to the topic
            string[] messages =
            {
                "Employee Id '{0}' has joined.",
                "Employee Id '{0}' has left.",
                "Employee Id '{0}' has switched to a different team."
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
2. <span data-ttu-id="92f78-157">**ReceiveAndSendNotification**</span><span class="sxs-lookup"><span data-stu-id="92f78-157">**ReceiveAndSendNotification**</span></span>
   
    <span data-ttu-id="92f78-158">a.</span><span class="sxs-lookup"><span data-stu-id="92f78-158">a.</span></span> <span data-ttu-id="92f78-159">Esse projeto usa os pacotes *WindowsAzure.ServiceBus* e *Microsoft.Web.WebJobs.Publish* do Nuget e se baseia na [Programação Pub/Sub do Barramento de Serviço].</span><span class="sxs-lookup"><span data-stu-id="92f78-159">This project uses the *WindowsAzure.ServiceBus* and *Microsoft.Web.WebJobs.Publish* Nuget packages and is based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="92f78-160">b.</span><span class="sxs-lookup"><span data-stu-id="92f78-160">b.</span></span> <span data-ttu-id="92f78-161">Esse é outro console aplicativo em C# que podemos executar como um [Trabalho Web do Azure] porque ele precisa ser executado continuamente para ouvir mensagens dos sistemas LoB/back-end.</span><span class="sxs-lookup"><span data-stu-id="92f78-161">This is another C# console app which we will run as an [Azure WebJob] since it has to run continuously to listen for messages from the LoB/backend systems.</span></span> <span data-ttu-id="92f78-162">Isso fará parte do back-end do celular.</span><span class="sxs-lookup"><span data-stu-id="92f78-162">This will be part of your Mobile backend.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                     CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create the subscription which will receive messages
            CreateSubscription(connectionString);
   
            // Receive message
            ReceiveMessageAndSendNotification(connectionString);
        }
   
    <span data-ttu-id="92f78-163">c.</span><span class="sxs-lookup"><span data-stu-id="92f78-163">c.</span></span> <span data-ttu-id="92f78-164">`CreateSubscription` é usado para criar uma assinatura do Barramento de Serviço para o tópico onde o sistema de back-end enviará mensagens.</span><span class="sxs-lookup"><span data-stu-id="92f78-164">`CreateSubscription` is used to create a Service Bus subscription for the topic where the backend system will send messages.</span></span> <span data-ttu-id="92f78-165">Dependendo do cenário de negócios, esse componente criará uma ou mais assinaturas para tópicos correspondentes (por exemplo, alguns podem estar recebendo mensagens do sistema de RH, parte do sistema de Finanças e assim por diante)</span><span class="sxs-lookup"><span data-stu-id="92f78-165">Depending on the business scenario, this component will create one or more subscriptions to corresponding topics (e.g. some may be receiving messages from HR system, some from Finance system, and so on)</span></span>
   
        static void CreateSubscription(string connectionString)
        {
            // Create the subscription if it does not exist already
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.SubscriptionExists(sampleTopic, sampleSubscription))
            {
                namespaceManager.CreateSubscription(sampleTopic, sampleSubscription);
            }
        }
   
    <span data-ttu-id="92f78-166">d.</span><span class="sxs-lookup"><span data-stu-id="92f78-166">d.</span></span> <span data-ttu-id="92f78-167">ReceiveMessageAndSendNotification é usado para ler a mensagem do tópico usando sua assinatura e se a leitura for bem-sucedida, em seguida, criar uma notificação (no cenário de exemplo uma notificação nativa do Windows) para ser enviado para o aplicativo móvel usando os Hubs de Notificação do Azure.</span><span class="sxs-lookup"><span data-stu-id="92f78-167">ReceiveMessageAndSendNotification is used to read the message from the topic using its subscription and if the read is successful then craft a notification (in the sample scenario a Windows native toast notification) to be sent to the mobile application using Azure Notification Hubs.</span></span>
   
        static void ReceiveMessageAndSendNotification(string connectionString)
        {
            // Initialize the Notification Hub
            string hubConnectionString = CloudConfigurationManager.GetSetting
                    ("Microsoft.NotificationHub.ConnectionString");
            hub = NotificationHubClient.CreateClientFromConnectionString
                    (hubConnectionString, "enterprisepushservicehub");
   
            SubscriptionClient Client =
                SubscriptionClient.CreateFromConnectionString
                        (connectionString, sampleTopic, sampleSubscription);
   
            Client.Receive();
   
            // Continuously process messages received from the subscription
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
   
    <span data-ttu-id="92f78-168">e.</span><span class="sxs-lookup"><span data-stu-id="92f78-168">e.</span></span> <span data-ttu-id="92f78-169">Para publicar isso como um **Trabalho Web**, clique com o botão direito na solução no Visual Studio e selecione **Publicar como Trabalho Web**</span><span class="sxs-lookup"><span data-stu-id="92f78-169">For publishing this as a **WebJob**, right click on the solution in Visual Studio and select **Publish as WebJob**</span></span>
   
    ![][2]
   
    <span data-ttu-id="92f78-170">f.</span><span class="sxs-lookup"><span data-stu-id="92f78-170">f.</span></span> <span data-ttu-id="92f78-171">Selecione o perfil de publicação e crie um novo site do Azure, se ele ainda não existir, que hospedará esse Trabalho Web e, quando tiver o site, **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="92f78-171">Select your publishing profile and create a new Azure WebSite if it doesnt exist already which will host this WebJob and once you have the WebSite then **Publish**.</span></span>
   
    ![][3]
   
    <span data-ttu-id="92f78-172">g.</span><span class="sxs-lookup"><span data-stu-id="92f78-172">g.</span></span> <span data-ttu-id="92f78-173">Configure o trabalho para ser “Executado Continuamente” para que, quando fizer logon no [Portal Clássico do Azure] , você veja algo semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="92f78-173">Configure the job to be "Run Continuously" so that when you log in to the [Azure Classic Portal] you should see something like the following:</span></span>
   
    ![][4]
3. <span data-ttu-id="92f78-174">**EnterprisePushMobileApp**</span><span class="sxs-lookup"><span data-stu-id="92f78-174">**EnterprisePushMobileApp**</span></span>
   
    <span data-ttu-id="92f78-175">a.</span><span class="sxs-lookup"><span data-stu-id="92f78-175">a.</span></span> <span data-ttu-id="92f78-176">Isso é um aplicativo da Windows Store que receberá notificações do WebJob em execução como parte do back-end Móvel e exibi-lo.</span><span class="sxs-lookup"><span data-stu-id="92f78-176">This is a Windows Store application which will receive toast notifications from the WebJob running as part of your Mobile backend and display it.</span></span> <span data-ttu-id="92f78-177">Isso se baseia em [Hubs de Notificação - tutorial do Windows Universal].</span><span class="sxs-lookup"><span data-stu-id="92f78-177">This is based on [Notification Hubs - Windows Universal tutorial].</span></span>  
   
    <span data-ttu-id="92f78-178">b.</span><span class="sxs-lookup"><span data-stu-id="92f78-178">b.</span></span> <span data-ttu-id="92f78-179">Certifique-se de que seu aplicativo está habilitado para receber notificações do sistema.</span><span class="sxs-lookup"><span data-stu-id="92f78-179">Ensure that your application is enabled to receive toast notifications.</span></span>
   
    <span data-ttu-id="92f78-180">c.</span><span class="sxs-lookup"><span data-stu-id="92f78-180">c.</span></span> <span data-ttu-id="92f78-181">Verifique se o seguinte código de registro de Hubs de Notificação está sendo chamado no aplicativo de inicialização (depois de substituir *HubName* e *DefaultListenSharedAccessSignature*:</span><span class="sxs-lookup"><span data-stu-id="92f78-181">Ensure that the following Notification Hubs registration code is being called at the App start up (after replacing the *HubName* and *DefaultListenSharedAccessSignature*:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("[HubName]", "[DefaultListenSharedAccessSignature]");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays the registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

### <a name="running-sample"></a><span data-ttu-id="92f78-182">Exemplo de execução:</span><span class="sxs-lookup"><span data-stu-id="92f78-182">Running sample:</span></span>
1. <span data-ttu-id="92f78-183">Certifique-se de que seu WebJob está em execução com êxito e programado para "Executar Continuamente".</span><span class="sxs-lookup"><span data-stu-id="92f78-183">Ensure that your WebJob is running successfully and scheduled to "Run Continuously".</span></span>
2. <span data-ttu-id="92f78-184">Execute o **EnterprisePushMobileApp** que iniciará o aplicativo da Windows Store.</span><span class="sxs-lookup"><span data-stu-id="92f78-184">Run the **EnterprisePushMobileApp** which will start the Windows Store app.</span></span>
3. <span data-ttu-id="92f78-185">Execute o aplicativo de console **EnterprisePushBackendSystem** que simulará o back-end do LoB e começará a enviar mensagens e você deverá ver notificações do sistema que aparecem como o seguinte:</span><span class="sxs-lookup"><span data-stu-id="92f78-185">Run the **EnterprisePushBackendSystem** console application which will simulate the LoB backend and will start sending messages and you should see toast notifications appearing like the following:</span></span>
   
    ![][5]
4. <span data-ttu-id="92f78-186">Originalmente, as mensagens foram enviadas para os tópicos do Barramento de Serviço que estava sendo monitorado por assinaturas do Barramento de Serviço no seu WebJob.</span><span class="sxs-lookup"><span data-stu-id="92f78-186">The messages were originally sent to Service Bus topics which was being monitored by Service Bus subscriptions in your Web Job.</span></span> <span data-ttu-id="92f78-187">Depois que uma mensagem foi recebida, uma notificação foi criada e enviada ao aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="92f78-187">Once a message was received, a notification was created and sent to the mobile app.</span></span> <span data-ttu-id="92f78-188">Você pode verificar os logs do WebJob para confirmar o processamento quando for para o link Logs no [Portal Clássico do Azure] para seu WebJob:</span><span class="sxs-lookup"><span data-stu-id="92f78-188">You can look through the WebJob logs to confirm the processing when you go to the Logs link in [Azure Classic Portal] for your Web Job:</span></span>
   
    ![][6]

<!-- Images -->
[1]: ./media/notification-hubs-enterprise-push-architecture/architecture.png
[2]: ./media/notification-hubs-enterprise-push-architecture/WebJobsContextMenu.png
[3]: ./media/notification-hubs-enterprise-push-architecture/PublishAsWebJob.png
[4]: ./media/notification-hubs-enterprise-push-architecture/WebJob.png
[5]: ./media/notification-hubs-enterprise-push-architecture/Notifications.png
[6]: ./media/notification-hubs-enterprise-push-architecture/WebJobsLog.png

<!-- Links -->
<span data-ttu-id="92f78-189">[Exemplos do Hub de Notificação]: https://github.com/Azure/azure-notificationhubs-samples</span><span class="sxs-lookup"><span data-stu-id="92f78-189">[Notification Hub Samples]: https://github.com/Azure/azure-notificationhubs-samples</span></span>
<span data-ttu-id="92f78-190">[Serviço Móvel do Azure]: http://azure.microsoft.com/documentation/services/mobile-services/</span><span class="sxs-lookup"><span data-stu-id="92f78-190">[Azure Mobile Service]: http://azure.microsoft.com/documentation/services/mobile-services/</span></span>
<span data-ttu-id="92f78-191">[Barramento de Serviço do Azure]: http://azure.microsoft.com/documentation/articles/fundamentals-service-bus-hybrid-solutions/</span><span class="sxs-lookup"><span data-stu-id="92f78-191">[Azure Service Bus]: http://azure.microsoft.com/documentation/articles/fundamentals-service-bus-hybrid-solutions/</span></span>
<span data-ttu-id="92f78-192">[Programação Pub/Sub do Barramento de Serviço]: http://azure.microsoft.com/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/</span><span class="sxs-lookup"><span data-stu-id="92f78-192">[Service Bus Pub/Sub programming]: http://azure.microsoft.com/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/</span></span>
<span data-ttu-id="92f78-193">[Trabalho Web do Azure]: http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/</span><span class="sxs-lookup"><span data-stu-id="92f78-193">[Azure WebJob]: http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/</span></span>
<span data-ttu-id="92f78-194">[Hubs de Notificação - tutorial do Windows Universal]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span><span class="sxs-lookup"><span data-stu-id="92f78-194">[Notification Hubs - Windows Universal tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span></span>
<span data-ttu-id="92f78-195">[Portal Clássico do Azure]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="92f78-195">[Azure Classic Portal]: https://manage.windowsazure.com/</span></span>
