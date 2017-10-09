---
title: "aaaCreate aplicativos que usam tópicos do barramento de serviço do Azure e assinaturas | Microsoft Docs"
description: "Introdução toohello publicação / assinatura oferecidos por assinaturas e tópicos do barramento de serviço."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a48fc9b0-b7b0-464e-8187-a517bf8b4eb4
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: sethm
ms.openlocfilehash: f6d7de46ace7bd5b49de612db213ced789308d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-applications-that-use-service-bus-topics-and-subscriptions"></a>Criar aplicativos que usam os tópicos e as assinaturas do Barramento de Serviço
O Barramento de Serviço do Azure oferece suporte a um conjunto de tecnologias middleware orientado a mensagens, baseado em nuvem, incluindo o serviço de enfileiramento de mensagens confiável e o sistema de mensagens de publicação/assinatura durável. Este artigo aproveita informações Olá fornecidas nos [criar aplicativos que usam filas do barramento de serviço](service-bus-create-queues.md) e oferece uma introdução toohello recursos de publicação/assinatura oferecidos por tópicos do barramento de serviço.

## <a name="evolving-retail-scenario"></a>Cenário de varejo em evolução
Este artigo continua o cenário de varejo Olá usado em [criar aplicativos que usam filas do barramento de serviço](service-bus-create-queues.md). Lembre-se de que os dados de vendas dos terminais de ponto de venda (PDV) individuais de devem ser roteada tooan sistema de gerenciamento de estoque que usa esse toodetermine dados quando deve toobe ocorrer a reposição do estoque. Cada terminal de POS transmite seus dados de vendas enviando mensagens toohello **DataCollectionQueue** fila, onde permanecem até que sejam recebidos pelo sistema de gerenciamento de estoque hello, conforme mostrado aqui:

![Barramento de Serviço 1](./media/service-bus-create-topics-subscriptions/IC657161.gif)

tooevolve neste cenário, um novo requisito foi adicionado toohello sistema: proprietário da loja Olá quer toobe toomonitor capaz de desempenho do armazenamento de saudação em tempo real.

tooaddress esse requisito, sistema hello ", pressione" fora do fluxo de dados de vendas de saudação. Ainda desejamos que cada mensagem enviada por toobe de terminais de POS Olá enviada do sistema de gerenciamento de estoque toohello como antes, mas queremos outra cópia de cada mensagem que podemos usar o proprietário do repositório de toohello toopresent Olá painel exibição.

Em qualquer situação como essa, em que você precisa cada toobe mensagem consumida por várias partes, você pode usar o barramento de serviço *tópicos*. Tópicos de fornecem um padrão de publicação/assinatura em que cada mensagem publicada é feita tooone disponível ou mais assinaturas registrado com o tópico de saudação. Por outro lado, com as filas, cada mensagem é recebida por um único consumidor.

As mensagens são enviadas tooa tópico em Olá mesma maneira que eles enviem tooa fila. No entanto, as mensagens não são recebidas do tópico Olá diretamente; elas são recebidas nas assinaturas. Você pode pensar em um tópico de tooa assinatura como uma fila virtual que recebe cópias das mensagens de saudação enviadas toothat tópico. As mensagens são recebidas de uma assinatura Olá mesma maneira que elas são recebidas de uma fila.

Voltando toohello cenário de varejo, fila de saudação é substituída por um tópico e uma assinatura é adicionada, pode usar o componente do sistema Olá inventário gerenciamento. sistema de saudação agora aparece da seguinte maneira:

![Barramento de Serviço 2](./media/service-bus-create-topics-subscriptions/IC657165.gif)

configuração de saudação aqui funciona de forma idêntica toohello anterior com base em fila design. Ou seja, as mensagens enviadas toohello tópico são roteada toohello **inventário** assinatura, do qual Olá **sistema de gerenciamento de estoque** consome-los.

No painel de gerenciamento do pedido toosupport hello, criamos uma segunda assinatura no tópico hello, conforme mostrado aqui:

![Barramento de Serviço 3](./media/service-bus-create-topics-subscriptions/IC657166.gif)

Com essa configuração, cada mensagem dos terminais de POS da saudação de fica disponível tooboth Olá **painel** e **inventário** assinaturas.

## <a name="show-me-hello-code"></a>Mostre-me Olá código
artigo Olá [criar aplicativos que usam filas do barramento de serviço](service-bus-create-queues.md) descreve como toosign para uma conta do Azure e criar um namespace de serviço. dependências de barramento de serviço do Hello mais fácil maneira tooreference é tooinstall Olá barramento de serviço [pacote Nuget](https://www.nuget.org/packages/WindowsAzure.ServiceBus/). Você também pode encontrar hello bibliotecas de barramento de serviço como parte de saudação do SDK do Azure. Olá download está disponível na Olá [página de download do SDK do Azure](https://azure.microsoft.com/downloads/).

### <a name="create-hello-topic-and-subscriptions"></a>Criar tópico hello e assinaturas
Operações de gerenciamento para entidades de mensagens (filas e a publicação/assinatura tópicos) são executadas por meio de saudação do barramento de serviço [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) classe. São necessárias credenciais apropriadas em ordem toocreate um **NamespaceManager** instância para um namespace específico. O Barramento de Serviço usa um modelo de segurança baseado na [Assinatura de Acesso Compartilhado (SAS)](service-bus-sas.md). Olá [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) classe representa um provedor de token de segurança com métodos de fábrica interna retornando alguns provedores de token bem conhecidos. Usaremos uma [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) credenciais do método toohold Olá SAS. Olá [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) instância é construída com o endereço base Olá Olá namespace de barramento de serviço e o provedor de token de saudação.

Olá [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) classe fornece métodos toocreate, enumerar e excluir entidades de mensagens. Olá código mostrado aqui mostra como Olá **NamespaceManager** instância é criada e usada toocreate Olá **DataCollectionTopic** tópico.

```csharp
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", "test-blog", string.Empty);
string name = "RootManageSharedAccessKey";
string key = "abcdefghijklmopqrstuvwxyz";

TokenProvider tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(name, key);
NamespaceManager namespaceManager = new NamespaceManager(uri, tokenProvider);

namespaceManager.CreateTopic("DataCollectionTopic");
```

Observe que há sobrecargas de saudação [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) método que permitem que você tooset propriedades do tópico hello. Por exemplo, você pode definir Olá time-to-live (TTL) valor padrão para mensagens enviadas toohello tópico. Em seguida, adicione Olá **inventário** e **painel** assinaturas.

```csharp
namespaceManager.CreateSubscription("DataCollectionTopic", "Inventory");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard");
```

### <a name="send-messages-toohello-topic"></a>Enviar tópico toohello de mensagens
Para operações de tempo de execução em entidades do Barramento de Serviço; por exemplo, para enviar e receber mensagens, primeiro um aplicativo deverá criar um objeto [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#microsoft_servicebus_messaging_messagingfactory). Semelhante toohello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) classe hello **MessagingFactory** instância é criada a partir do endereço de base de saudação do hello namespace de serviço e o provedor de token de saudação.

```
MessagingFactory factory = MessagingFactory.Create(uri, tokenProvider);
```

As mensagens enviadas tooand recebida de tópicos do barramento de serviço, são instâncias da saudação [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) classe. Essa classe consiste em um conjunto de propriedades padrão (como [rótulo](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) e [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), um dicionário que é usado toohold propriedades do aplicativo e um corpo de dados arbitrários do aplicativo. Um aplicativo pode definir corpo Olá passando qualquer objeto serializável (hello exemplo a seguir passa um **SalesData** objeto que representa os dados de vendas de saudação do terminal de POS da saudação), que usará Olá [ DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx) tooserialize objeto de saudação. Como alternativa, poderá ser fornecido um objeto [Stream](https://msdn.microsoft.com/library/system.io.stream.aspx).

```csharp
BrokeredMessage bm = new BrokeredMessage(salesData);
bm.Label = "SalesReport";
bm.Properties["StoreName"] = "Redmond";
bm.Properties["MachineID"] = "POS_1";
```

Olá mais fácil maneira toosend mensagens toohello tópico é toouse [CreateMessageSender](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageSender_System_String_) toocreate um [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) objeto diretamente a partir de saudação [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) instância:

```csharp
MessageSender sender = factory.CreateMessageSender("DataCollectionTopic");
sender.Send(bm);
```

### <a name="receive-messages-from-a-subscription"></a>Receber mensagens de uma assinatura
Filas de toousing semelhante, tooreceive mensagens de uma assinatura que você pode usar um [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) objeto que criar diretamente de saudação [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) usando [ CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_). Você pode usar um de saudação dois modos de recebimento (**ReceiveAndDelete** e **PeekLock**), conforme discutido em [criar aplicativos que usam filas do barramento de serviço](service-bus-create-queues.md).

Observe que, quando você cria um **MessageReceiver** para assinaturas, Olá *entityPath* parâmetro é do formato de saudação `topicPath/subscriptions/subscriptionName`. Portanto, toocreate um **MessageReceiver** para Olá **inventário** assinatura de saudação **DataCollectionTopic** tópico *entityPath*deve ser definido muito`DataCollectionTopic/subscriptions/Inventory`. código de saudação aparece da seguinte maneira:

```csharp
MessageReceiver receiver = factory.CreateMessageReceiver("DataCollectionTopic/subscriptions/Inventory");
BrokeredMessage receivedMessage = receiver.Receive();
try
{
    ProcessMessage(receivedMessage);
    receivedMessage.Complete();
}
catch (Exception e)
{
    receivedMessage.Abandon();
}
```

## <a name="subscription-filters"></a>Filtros de assinatura
Neste cenário até agora, todas as mensagens enviadas toohello tópico ficam assinaturas disponíveis tooall registrado. Olá frase-chave aqui é "disponibilizada". Enquanto as assinaturas do barramento de serviço vejam todas as mensagens enviadas toohello tópico, você pode copiar apenas um subconjunto da fila de assinatura virtual de toohello mensagens. Isso é feito usando *filtros* de assinatura. Quando você cria uma assinatura, você pode fornecer uma expressão de filtro na forma de saudação de um predicado de estilo SQL92 que opera nas propriedades de saudação de mensagem de saudação, ambos Olá propriedades do sistema (por exemplo, [rótulo](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label)) e o aplicativo hello propriedades, como **StoreName** no exemplo anterior de saudação.

Olá cenário tooillustrate evoluindo isso, uma segunda loja é cenário de varejo toobe tooour adicionado. Dados de vendas de todos os terminais de POS da saudação ambos os armazenamentos de ainda têm o sistema de gerenciamento de estoque toobe roteada toohello centralizado, mas um Gerenciador de armazenamento usando a ferramenta de painel Olá só está interessado no desempenho de saudação do repositório. Você pode usar a filtragem tooachieve isso de assinatura. Observe que, quando os terminais de POS da saudação publicam mensagens, eles definido Olá **StoreName** propriedade na mensagem de saudação de aplicativo. Considerando duas lojas, por exemplo **Redmond** e **Seattle**, terminais de POS da saudação Olá Redmond armazenam carimbo mensagens de seus dados de vendas com um **StoreName** igual muito **Redmond**, enquanto Olá Seattle armazenar o uso de terminais de POS um **StoreName** igual muito**Seattle**. Gerenciador de repositório de saudação do hello Redmond armazenar apenas deseja toosee dados de seus terminais de POS. sistema de saudação aparece da seguinte maneira:

![Service-Bus4](./media/service-bus-create-topics-subscriptions/IC657167.gif)

tooset o este roteamento, você cria Olá **painel** assinatura da seguinte maneira:

```csharp
SqlFilter dashboardFilter = new SqlFilter("StoreName = 'Redmond'");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard", dashboardFilter);
```

Com isso [filtro de assinatura](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), somente as mensagens com hello **StoreName** propriedade definida muito**Redmond** será copiado toohello fila virtual Olá **Painel** assinatura. Há muito mais toosubscription filtragem, no entanto. Os aplicativos podem ter várias regras de filtro por assinatura em adição toohello capacidade toomodify Olá propriedades de uma mensagem conforme ele passa a fila virtual tooa da assinatura.

## <a name="summary"></a>Resumo
Todas Olá motivos toouse enfileiramento descritas [criar aplicativos que usam filas do barramento de serviço](service-bus-create-queues.md) também se aplicam tootopics, especificamente:

* Desacoplamento temporal: mensagem produtores e consumidores não têm toobe online em Olá simultaneamente.
* Nivelamento de carga – picos de carga são amenizados pelo tópico Olá habilitando consumo toobe aplicativos provisionado para carga média em vez de picos de carga.
* Balanceamento de carga – fila tooa semelhante, você pode ter vários consumidores concorrentes ouvindo em uma única assinatura, com cada mensagem entregue tooonly de consumidores hello, resultando no balanceamento de carga.
* Acoplamento flexível: você pode evoluir Olá mensagens rede sem afetar os pontos de extremidade existentes; Por exemplo, adicionando assinaturas ou alterando filtros tooa tópico tooallow novos consumidores.

## <a name="next-steps"></a>Próximas etapas

Consulte [criar aplicativos que usam filas do barramento de serviço](service-bus-create-queues.md) para obter informações sobre como toouse filas no cenário de varejo Olá POS.

