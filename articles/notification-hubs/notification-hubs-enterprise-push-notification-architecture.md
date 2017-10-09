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
# <a name="enterprise-push-architectural-guidance"></a>Orientação arquitetural do push corporativo
As empresas hoje estão gradualmente migrando para a criação de aplicativos móveis para ambos os usuários finais (externo) ou para os funcionários de saudação (internos). Eles têm sistemas de back-end existentes in-loco seja mainframes ou Olá de alguns aplicativos de LoB que devem ser integrados em arquitetura de aplicativos móveis. Este guia abordaremos a melhor maneira de toodo essa integração recomendando toocommon cenários de solução possível.

É um requisito frequente para enviar por push usuários de toohello de notificação por meio de seu aplicativo móvel quando ocorre um evento de interesse em sistemas de back-end de saudação. Por exemplo um cliente do banco que tem o aplicativo de serviços bancários do banco de saudação em seu iPhone quer toobe notificado quando um débito fica acima de um determinado valor de sua conta ou um cenário de intranet onde quer que um funcionário do departamento de finanças que tem um aplicativo de aprovação de orçamento no seu Windows Phone toobe notificado quando ele recebe uma solicitação de aprovação.

conta bancária de saudação ou processamento de aprovação é provavelmente toobe feita em algum sistema back-end que deve iniciar um usuário de toohello por push. Pode haver vários tal back-end sistemas que todos os devem criar hello mesmo tipo de envio por push tooimplement de lógica quando um evento dispara uma notificação. complexidade de saudação aqui está na integração de vários sistemas de back-end junto com um sistema de envio por push único onde hello, os usuários finais podem se inscreveu toodifferent notificações e pode até mesmo ser vários aplicativos móveis, por exemplo, no caso de saudação de aplicativos móveis da intranet em que um aplicativo móvel pode ser tooreceive notificações de vários esses sistemas de back-end. sistemas de back-end Olá desconhecida ou não seja necessário tooknow semântica/tecnologia de envio por push para que uma solução comum aqui tradicionalmente toointroduce um componente que controla os sistemas de back-end Olá para todos os eventos de interesse e é responsável por enviar mensagens de saudação do envio cliente de toohello.
Aqui, falaremos sobre uma solução ainda mais usando o barramento de serviço do Azure - modelo de tópico/assinatura que reduzirá a complexidade de saudação ao fazer a solução Olá escalonável.

Aqui está a arquitetura geral Olá de solução de saudação (generalizado com vários aplicativos móveis mas igualmente aplicáveis quando há apenas um aplicativo móvel)

## <a name="architecture"></a>Arquitetura
![][1]

informação de chave de saudação neste diagrama de arquitetura é barramento de serviço do Azure que fornece um modelo de programação de tópicos/assinaturas (mais informações sobre ele no [programação do barramento de serviço Pub/Sub]). destinatário Hello, que nesse caso, é o back-end de saudação móvel (normalmente [serviço móvel do Azure], que iniciará um push toohello os aplicativos móveis) não receber mensagens diretamente de sistemas de back-end hello, mas em vez disso, temos um camada de abstração intermediário fornecida pelo [Azure Service Bus] que permite que as mensagens de tooreceive móvel de back-end de um ou mais sistemas de back-end. Um tópico do barramento de serviço precisa toobe criado para cada Olá sistemas back-end, por exemplo, a conta, h, finanças, que são basicamente "tópicos" de interesse que iniciará toobe mensagens enviada como notificação por push. sistemas de back-end Olá enviará mensagens tópicos toothese. Um back-end móveis podem se inscrever tooone ou mais tópicos criando uma assinatura do barramento de serviço. Isso será intitular Olá móvel de back-end tooreceive uma notificação do sistema de back-end correspondente hello. Back-end móvel continua toolisten para mensagens em suas assinaturas e assim que uma mensagem chega, ativa novamente e a envia como o hub de notificação de tooits de notificação. Hubs de notificação, em seguida, eventualmente a entrega de mensagem de saudação toohello aplicativo móvel. Para componentes-chave toosummarize hello, temos:

1. Sistemas de back-end (sistemas de LoB/herdados)
   * Cria um tópico do barramento de serviço
   * Envia mensagem
2. Back-end móvel
   * Cria a assinatura do serviço
   * Recebe uma mensagem (do sistema de back-end)
   * Envia notificação tooclients (por meio do Hub de notificação do Azure)
3. Aplicativo Móvel
   * Recebe e exibe a notificação

### <a name="benefits"></a>Benefícios:
1. Olá desacoplamento entre receptor hello (aplicativo/serviço móvel por meio do Hub de notificação) e o remetente (sistemas de back-end) permite que os sistemas de back-end adicionais sendo integrados com o mínimo de alterações.
2. Isso também facilita o cenário de saudação de vários aplicativos móveis sendo tooreceive capaz de eventos de um ou mais sistemas de back-end.  

## <a name="sample"></a>Exemplo:
### <a name="prerequisites"></a>Pré-requisitos
Você deve concluir Olá tutoriais toofamiliarize com conceitos de hello, bem como etapas comuns de criação e configuração a seguir:

1. [programação do barramento de serviço Pub/Sub] -explica detalhes de saudação do trabalho com assinaturas/tópicos do barramento do serviço, como um namespace de toocreate toocontain tópicos/assinaturas, como toosend & receber mensagens dela.
2. [Hubs de notificação - Windows Universal tutorial] -explica como tooset um aplicativo da Windows Store e usar tooregister de Hubs de notificação e, em seguida, receber notificações.

### <a name="sample-code"></a>Exemplo de código
Olá código de exemplo completo está disponível em [exemplos de Hub de notificação]. Ele é dividido em três componentes:

1. **EnterprisePushBackendSystem**
   
    a. Este projeto usa Olá *windowsazure. ServiceBus* pacote Nuget e é baseada em [programação do barramento de serviço Pub/Sub].
   
    b. Este é um simples c# console aplicativo toosimulate um sistema LoB, que inicia toobe de mensagem de saudação entregue o aplicativo móvel toohello.
   
        static void Main(string[] args)
        {
            string connectionString =
                CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello topic where we will send notifications
            CreateTopic(connectionString);
   
            // Send message
            SendMessage(connectionString);
        }
   
    c. `CreateTopic`é o tópico de barramento de serviço Olá toocreate usado onde podemos enviará mensagens.
   
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
   
    d. `SendMessage`é usado toosend Olá mensagens toothis tópico do barramento de serviço. Aqui, simplesmente está enviando um conjunto de tópico de toohello mensagens aleatória periodicamente para finalidade de saudação do exemplo hello. Normalmente haverá um sistema de back-end que enviará mensagens quando ocorre um evento.
   
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
2. **ReceiveAndSendNotification**
   
    a. Este projeto usa Olá *windowsazure. ServiceBus* e *Microsoft.Web.WebJobs.Publish* Nuget pacotes e é baseada em [programação do barramento de serviço Pub/Sub].
   
    b. Este é outro console aplicativo c# que iremos executar como um [Azure WebJob] porque ele tem toorun continuamente toolisten para mensagens de sistemas de LoB/back-end de saudação. Isso fará parte do back-end do celular.
   
        static void Main(string[] args)
        {
            string connectionString =
                     CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello subscription which will receive messages
            CreateSubscription(connectionString);
   
            // Receive message
            ReceiveMessageAndSendNotification(connectionString);
        }
   
    c. `CreateSubscription`é usado toocreate uma assinatura do barramento de serviço para o tópico Olá onde o sistema de back-end Olá enviará mensagens. Dependendo do cenário de negócios hello, esse componente criará uma ou mais assinaturas tópicos toocorresponding (por exemplo, alguns podem receber mensagens do sistema de RH, alguns a partir do sistema de finanças e assim por diante)
   
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
   
    d. ReceiveMessageAndSendNotification é tooread usado a mensagem de saudação do tópico hello usando sua assinatura e se Olá leitura for bem-sucedida, em seguida, criar um toohello toobe enviado de notificação (no cenário de exemplo hello uma notificação de sistema nativo do Windows) móvel aplicativo usando os Hubs de notificação do Azure.
   
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
   
    e. Para publicar como uma **WebJob**, clique com o botão direito na solução Olá no Visual Studio e selecione **Publicar como WebJob**
   
    ![][2]
   
    f. Selecione o perfil de publicação e criar um novo site do Azure, se ele não existir já que irá hospedar esse trabalho Web e uma vez que o site de hello, em seguida, **publicar**.
   
    ![][3]
   
    g. Configurar hello "Executar continuamente" toobe de trabalho de forma que ao fazer logon em toohello [Portal clássico do Azure] você verá algo parecido com hello seguinte:
   
    ![][4]
3. **EnterprisePushMobileApp**
   
    a. Este é um aplicativo da Windows Store que vai receber notificações do sistema de execução do trabalho Web hello como parte do seu back-end móvel e exibi-lo. Isso se baseia em [Hubs de notificação - Windows Universal tutorial].  
   
    b. Certifique-se de que seu aplicativo está habilitado tooreceive notificações do sistema.
   
    c. Certifique-se de que Olá após o código de registro de Hubs de notificação está sendo chamado em Olá aplicativo Iniciar backup (depois de substituir Olá *HubName* e *DefaultListenSharedAccessSignature*:
   
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

### <a name="running-sample"></a>Exemplo de execução:
1. Certifique-se de que seu trabalho Web está em execução com êxito e agendado muito "executar continuamente".
2. Executar Olá **EnterprisePushMobileApp** que iniciará o aplicativo da Windows Store hello.
3. Executar Olá **EnterprisePushBackendSystem** aplicativo de console que simulará back-end de LoB hello e começar a enviar mensagens e você deverá ver notificações do sistema que aparecem como Olá seguinte:
   
    ![][5]
4. mensagens de saudação foram enviadas originalmente tópicos do barramento tooService que estava sendo monitorado por assinaturas do barramento de serviço no seu trabalho Web. Depois que uma mensagem foi recebida, uma notificação foi criada e enviada toohello aplicativos para dispositivos móveis. Examinar Olá WebJob logs tooconfirm Olá processamento quando você for toohello Logs link no [Portal clássico do Azure] para seu trabalho Web:
   
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
