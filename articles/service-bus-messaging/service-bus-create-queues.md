---
title: "aaaWrite aplicativos que usam filas do barramento de serviço do Azure | Microsoft Docs"
description: "Como toowrite um aplicativo simple baseado em fila que usa o barramento de serviço do Azure."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 754d91b3-1426-405e-84b4-fd36d65b114a
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: 93b75902a06becd6e33e05298e09f5669d0e2aef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-applications-that-use-service-bus-queues"></a>Criar aplicativos que usem as filas do Barramento de Serviço
Este tópico descreve as filas do barramento de serviço e mostra como toowrite um aplicativo simple baseado em fila que usa o barramento de serviço.

Considere um cenário de Olá mundo de varejo em que os dados de vendas de individuais Point-of-Sale (POS) terminais devem ser roteados tooan sistema de gerenciamento de estoque que usa Olá dados toodetermine quando deve toobe ocorrer a reposição do estoque. Esta solução usa o barramento de serviço do sistema de mensagens para comunicação de saudação entre terminais hello e sistema de gerenciamento de estoque hello, conforme ilustrado na figura a seguir de saudação:

![Filas de Barramento de Serviço imagem 1](./media/service-bus-create-queues/IC657161.gif)

Cada terminal de POS transmite seus dados de vendas enviando mensagens toohello **DataCollectionQueue**. Essas mensagens permanecem nessa fila até que eles são recuperados pelo sistema de gerenciamento de estoque hello. Esse padrão é geralmente denominado *mensagens assíncronas*, porque o terminal de POS da saudação não tem toowait por uma resposta do processamento de toocontinue de sistema do gerenciamento de estoque hello.

## <a name="why-queuing"></a>Por que usar filas?
Antes de examinarmos o código Olá tooset necessária a esse aplicativo, considere as vantagens de saudação do uso de uma fila nesse cenário, em vez de ter os terminais de POS da saudação falar diretamente (de forma síncrona) toohello inventário de sistema de gerenciamento.

### <a name="temporal-decoupling"></a>Desacoplamento temporal
Com o padrão de mensagens assíncronas hello, produtores e consumidores não há toobe online Olá simultaneamente. infraestrutura de mensagens de saudação confiável armazena as mensagens até a parte consumidora Olá é tooreceive pronto-los. Isso significa que componentes de saudação do aplicativo hello distribuída podem ser desconectados, ou voluntariamente; Por exemplo, para manutenção ou devido a falha do componente tooa, sem afetar o sistema inteiro hello. Além disso, Olá consumindo o aplicativo pode ter somente toobe online durante determinadas horas do dia de saudação. Por exemplo, no cenário de varejo, sistema de gerenciamento de estoque Olá pode ter somente toocome online após o término de saudação do dia de trabalho de saudação.

### <a name="load-leveling"></a>Nivelamento de carga
Em muitos aplicativos de carga do sistema varia ao longo do tempo, enquanto que o tempo de processamento de saudação necessário para cada unidade de trabalho é normalmente constante. A intermediação mensagem produtores e consumidores com um meio de fila que Olá aplicativo de consumo (trabalho Olá) tem apenas toobe provisionados tooservice uma média de carga em vez de uma carga de pico. profundidade de saudação da fila de saudação crescerão e contrato como Olá carga de entrada varia. Isso economiza o dinheiro diretamente com valor de toohello considerar a infraestrutura necessária tooservice Olá de carregamento de aplicativo.

![Filas de Barramento de Serviço imagem 2](./media/service-bus-create-queues/IC657162.gif)

### <a name="load-balancing"></a>Balanceamento de carga
Como Olá carga aumenta, mais processos de trabalho podem ser adicionado tooread da fila de trabalho hello. Cada mensagem é processada por apenas um dos processos de trabalho hello. Além disso, esse balanceamento de carga baseado em pull permite o uso otimizado dos computadores de trabalho Olá mesmo que Olá computadores tenham diferentes com capacidade de tooprocessing de relação, como eles efetuarão pull das mensagens em sua própria velocidade máxima. Esse padrão é geralmente denominado padrão de consumidor concorrente hello.

![Filas de Barramento de Serviço imagem 3](./media/service-bus-create-queues/IC657163.gif)

### <a name="loose-coupling"></a>Acoplamento flexível
Usar toointermediate enfileiramento de mensagens entre os consumidores e produtores de mensagens fornece um acoplamento flexível intrínseco entre os componentes de saudação. Como produtores e consumidores não têm conhecimento uns dos outros, um consumidor pode ser atualizado sem causar qualquer impacto produtor hello. Além disso, Olá topologia de mensagens poderá evoluir sem afetar a pontos de extremidade existentes hello. Discutiremos um pouco mais desse assunto quando falarmos sobre publicação/assinatura.

## <a name="show-me-hello-code"></a>Mostre-me Olá código
Olá a seguinte seção mostra como toobuild do barramento de serviço toouse este aplicativo.

### <a name="sign-up-for-an-azure-account"></a>Inscrever-se em uma conta do Azure
Você precisará de uma conta do Azure em ordem toostart trabalhando com o barramento de serviço. Se você ainda não tiver uma assinatura, poderá se inscrever em uma conta gratuita [aqui](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).

### <a name="create-a-namespace"></a>Criar um namespace
Quando tiver uma assinatura, você poderá [criar um novo namespace](service-bus-create-namespace-portal.md). Cada namespace age como um contêiner de escopo para um conjunto de entidades do Barramento de Serviço. Dê um nome exclusivo ao seu novo namespace em todas as contas do Barramento de Serviço. 

### <a name="install-hello-nuget-package"></a>Instalar o pacote do NuGet Olá
namespace de barramento de serviço do toouse hello, um aplicativo deve fazer referência a saudação assembly do barramento de serviço, especificamente o Microsoft.ServiceBus.dll. Você pode encontrar esse assembly como parte do SDK do Microsoft Azure de saudação e download de saudação está disponível na Olá [página de download do SDK do Azure](https://azure.microsoft.com/downloads/). No entanto, Olá [pacote NuGet do barramento de serviço](https://www.nuget.org/packages/WindowsAzure.ServiceBus) é Olá mais fácil maneira tooget Olá API do barramento de serviço e tooconfigure seu aplicativo com todas as dependências de barramento de serviço hello.

### <a name="create-hello-queue"></a>Criar fila Olá
Operações de gerenciamento para entidades de mensagens (filas e a publicação/assinatura tópicos) são executadas por meio de saudação do barramento de serviço [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) classe. O Barramento de Serviço usa um modelo de segurança baseado na [Assinatura de Acesso Compartilhado (SAS)](service-bus-sas.md). Olá [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) classe representa um provedor de token de segurança com métodos de fábrica interna retornando alguns provedores de token bem conhecidos. Usaremos uma [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) credenciais do método toohold Olá SAS. Olá [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) instância é construída com o endereço base Olá Olá namespace de barramento de serviço e o provedor de token de saudação.

Olá [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) classe fornece métodos toocreate, enumerar e excluir entidades de mensagens. Olá código mostrado aqui mostra como Olá [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) instância é criada e usada toocreate Olá **DataCollectionQueue** fila.

```csharp
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", 
                "test-blog", string.Empty);
string name = "RootManageSharedAccessKey";
string key = "abcdefghijklmopqrstuvwxyz";

TokenProvider tokenProvider = 
    TokenProvider.CreateSharedAccessSignatureTokenProvider(name, key);
NamespaceManager namespaceManager = 
    new NamespaceManager(uri, tokenProvider);
namespaceManager.CreateQueue("DataCollectionQueue");
```

Observe que há sobrecargas de saudação [CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) método que permitem que propriedades de saudação fila toobe ajustadas. Por exemplo, você pode definir Olá time-to-live (TTL) valor padrão para mensagens enviadas da fila de toohello.

### <a name="send-messages-toohello-queue"></a>Mensagens toohello fila de envio
Para operações de tempo de execução em entidades do Barramento de Serviço; por exemplo, para enviar e receber mensagens, primeiro um aplicativo deverá criar um objeto [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory). Semelhante toohello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) classe hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) instância é criada a partir do endereço de base de saudação do hello namespace de serviço e o provedor de token de saudação.

```csharp
 BrokeredMessage bm = new BrokeredMessage(salesData);
 bm.Label = "SalesReport";
 bm.Properties["StoreName"] = "Redmond";
 bm.Properties["MachineID"] = "POS_1";
```

As mensagens enviadas para e recebidas do barramento de serviço filas são instâncias da saudação [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) classe. Essa classe consiste em um conjunto de propriedades padrão (como [rótulo](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) e [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), um dicionário que é usado toohold propriedades do aplicativo e um corpo de dados arbitrários do aplicativo. Um aplicativo pode definir corpo Olá passando qualquer objeto serializável (hello exemplo a seguir passa um **SalesData** objeto que representa os dados de vendas de saudação do terminal de POS da saudação), que usará Olá [ DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx) tooserialize objeto de saudação. Como alternativa, poderá ser fornecido um objeto [Stream](https://msdn.microsoft.com/library/system.io.stream.aspx).

Olá mais fácil maneira toosend mensagens tooa fornecido fila, no nosso caso Olá **DataCollectionQueue**, é toouse [CreateMessageSender](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageSender_System_String_) toocreate um [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) objeto diretamente da saudação [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) instância.

```csharp
MessageSender sender = factory.CreateMessageSender("DataCollectionQueue");
sender.Send(bm);
```

### <a name="receiving-messages-from-hello-queue"></a>Receber mensagens da fila de saudação
tooreceive mensagens da fila de saudação, você pode usar um [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) objeto que criar diretamente de saudação [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) usando [CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_). Os receptores da mensagem poderão trabalhar em dois modos diferentes: **ReceiveAndDelete** e **PeekLock**. Olá [ReceiveMode](/dotnet/api/microsoft.servicebus.messaging.receivemode) é definido quando o destinatário da mensagem de saudação é criado, como um parâmetro toohello [CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory?redirectedfrom=MSDN#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_Microsoft_ServiceBus_Messaging_ReceiveMode_) chamar.

Ao usar o hello **ReceiveAndDelete** modo, Olá recebe é uma operação única etapa; ou seja, quando o barramento de serviço recebe a solicitação de hello, ele marca a mensagem de saudação como sendo consumida e retorna-toohello aplicativo. **ReceiveAndDelete** modo é o modelo mais simples de saudação e funciona melhor para cenários nos quais Olá aplicativo pode tolerar não processar uma mensagem se uma falha de toooccur. toounderstand isso, considere um cenário em que problemas do consumidor Olá Olá receber a solicitação e falha antes de processá-lo. Desde que o barramento de serviço marcado como mensagem de saudação como sendo consumida, quando reiniciar o aplicativo hello e começa a consumir mensagens novamente, ele terá perdido mensagem de saudação consumido antes da falha de saudação.

Em **PeekLock** receber de saudação do modo, torna-se uma operação de dois estágios, o que torna possível toosupport aplicativos que não podem tolerar mensagens ausentes. Quando o barramento de serviço recebe a solicitação de hello, ele localiza Olá próxima mensagem toobe consumida, boqueia-tooprevent outros consumidores a recebam e retorna toohello aplicativo. Depois que o aplicativo hello termina de processar a mensagem de saudação (ou armazena com segurança para processamento futuro), ele conclui Olá segunda etapa de saudação processo de recebimento chamando [concluir](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) na mensagem recebida. Quando o Service Bus vê Olá [concluir](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) chamada, ele marca a mensagem de saudação como sendo consumida.

Dois outros resultados são possíveis. Primeiro, se o aplicativo hello não puder tooprocess Olá mensagem por algum motivo, ele pode chamar [abandonar](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) na mensagem recebida (em vez de [concluir](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)). Isso faz com que a mensagem de saudação do barramento de serviço toounlock e torná-lo disponível toobe recebida novamente, pelo Olá mesmo consumidor ou por outro consumidor de conclusão. Segundo, há um tempo limite associado Olá bloqueio e se o aplicativo hello não é possível processar a mensagem de saudação antes Olá bloqueio tempo limite expirar (por exemplo, se o aplicativo hello falhar), e o barramento de serviço desbloquear Olá mensagem e torná-lo disponível toobe recebida novamente (basicamente a realização de uma [abandonar](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) operação por padrão).

Observe que, se hello aplicativo falhar após processar a mensagem de saudação, mas antes de saudação [concluir](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) solicitação foi emitida, a mensagem será entregue novamente toohello aplicativo quando ele for reiniciado. Isso é geralmente denominado * pelo menos uma vez * processamento. Isso significa que cada mensagem será processada pelo menos uma vez, mas em certo Olá situações mesma mensagem pode ser entregue novamente. Se o cenário de saudação não puder tolerar o processamento duplicado, lógica adicional será necessária em duplicatas de toodetect aplicativo hello. Isso pode ser feito com base em Olá [MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) propriedade de mensagem de saudação. valor Olá dessa propriedade permanece constante entre tentativas de entrega. Isso é conhecido como processamento *Exatamente Uma Vez*.

Olá código mostrado aqui recebe e processa uma mensagem usando Olá **PeekLock** modo, o que é o padrão de saudação se nenhum [ReceiveMode](/dotnet/api/microsoft.servicebus.messaging.receivemode) valor é explicitamente fornecido.

```csharp
MessageReceiver receiver = factory.CreateMessageReceiver("DataCollectionQueue");
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

### <a name="use-hello-queue-client"></a>Usar o cliente de fila Olá
Olá exemplos anteriormente nesta seção criado [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) e [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) objetos diretamente da saudação [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) toosend e receber mensagens da fila de hello, respectivamente. Uma abordagem alternativa é toouse uma [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) objeto, que oferece suporte para enviar e receber operações em adição toomore recursos avançados, como sessões.

```csharp
QueueClient queueClient = factory.CreateQueueClient("DataCollectionQueue");
queueClient.Send(bm);

BrokeredMessage message = queueClient.Receive();

try
{
    ProcessMessage(message);
    message.Complete();
}
catch (Exception e)
{
    message.Abandon();
} 
```

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas de saudação de filas, consulte [criar aplicativos que usam tópicos do barramento de serviço e as assinaturas](service-bus-create-topics-subscriptions.md) toocontinue esta discussão usando recursos de publicação/assinatura Olá dos tópicos do barramento de serviço e assinaturas.

