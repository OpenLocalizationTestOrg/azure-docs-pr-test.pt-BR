---
title: "aaaCreate particionada tópicos e filas do barramento de serviço do Azure | Microsoft Docs"
description: "Descreve como os agentes toopartition filas de barramento de serviço e tópicos usando mensagens múltiplas."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a0c7d5a2-4876-42cb-8344-a1fc988746e7
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;hillaryc
ms.openlocfilehash: 6d42556a0714d6a012dc319f662521c8b0bb958b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="partitioned-queues-and-topics"></a>Filas e tópicos particionados
O Azure Service Bus emprega agentes de várias mensagens tooprocess mensagens e várias mensagens armazena mensagens toostore. Uma fila ou um tópico convencional é manipulado por um único agente de mensagem e armazenado em um repositório de mensagens. Barramento de serviço *partições* habilitar as filas e tópicos, ou *entidades de mensagens*, toobe particionado entre diversos agentes e repositórios de mensagens. Isso significa que Olá taxa de transferência geral de uma entidade particionada não é limitada pelo desempenho de saudação de um único agente de mensagens ou repositório de mensagens. Além disso, uma interrupção temporária de um repositório de mensagens não torna uma fila ou um tópico particionado indisponível. Filas e tópicos particionados podem conter todos os recursos avançados do Barramento de Serviço, como o suporte a transações e sessões.

Para obter informações sobre recursos internos do barramento de serviço, consulte Olá [arquitetura de barramento de serviço] [ Service Bus architecture] artigo.

O particionamento é habilitado por padrão na criação da entidade em todos os tópicos e filas de mensagens Standard e Premium. Você pode criar entidades da camada de mensagens Standard sem particionamento, mas filas e tópicos em um namespace Premium são sempre particionados; essa opção não pode ser desabilitada. 

Não é possível toochange Olá particionamento opção em uma fila ou tópico existentes nas camadas Standard ou Premium, você só pode definir opção hello quando você criar entidade hello.

## <a name="how-it-works"></a>Como ele funciona

Cada fila ou tópico particionado consiste em vários fragmentos. Cada fragmento é armazenado em um repositório de mensagens diferente e manipulado por um agente de mensagens diferente. Quando uma mensagem é enviada tooa fila ou tópico particionado, o barramento de serviço atribui tooone de mensagem de saudação de fragmentos de saudação. seleção de saudação é feita aleatoriamente pelo barramento de serviço ou usando uma chave de partição que Olá remetente pode especificar.

Quando um cliente deseja tooreceive uma mensagem de uma fila particionada, ou de um tópico particionado tooa da assinatura, o barramento de serviço consulta todos os fragmentos de mensagens, retorna a primeira mensagem de saudação obtidos de qualquer um dos repositórios toohello receptor de mensagens de saudação. Barramento de serviço caches Olá outras mensagens e retorna-las quando ele recebe adicionais recebem solicitações. Um cliente de recebimento não está ciente do particionamento Olá; Olá voltada para o cliente o comportamento de uma fila ou tópico particionado (por exemplo, ler, concluir, adiar, mensagem morta, pré-busca) é idêntica toohello o comportamento de uma entidade normal.

Não há custo adicional ao enviar ou receber uma mensagem de uma fila ou um tópico particionado.

## <a name="enable-partitioning"></a>Habilitar particionamento

toouse particionada filas e tópicos de barramento de serviço do Azure, use hello Azure SDK versão 2.2 ou posterior, ou especifique `api-version=2013-10` em suas solicitações HTTP.

### <a name="standard"></a>Standard

Na camada de mensagem de saudação padrão, você pode criar filas do barramento de serviço e os tópicos em tamanhos de 1, 2, 3, 4 ou 5 GB (o padrão de saudação é de 1 GB). Com o particionamento habilitado, o barramento de serviço cria 16 cópias (16 partições) da entidade Olá para cada GB que você especificar. Dessa forma, se você criar uma fila que é de 5 GB de tamanho, com 16 partições tamanho máximo da fila de saudação torna-se (5 \* 16) = 80 GB. Você pode ver o tamanho máximo de saudação de sua fila ou tópico particionado examinando sua entrada no hello [portal do Azure][Azure portal], em Olá **visão geral** folha para essa entidade.

### <a name="premium"></a>Premium

Em um namespace de camada Premium, você pode criar filas do barramento de serviço e os tópicos em tamanhos de 1, 2, 3, 4, 5, 10, 20, 40 ou 80 GB (o padrão de saudação é de 1 GB). Com o particionamento habilitado por padrão, o Barramento de Serviço cria duas partições por entidade. Você pode ver o tamanho máximo de saudação de sua fila ou tópico particionado examinando sua entrada no hello [portal do Azure][Azure portal], em Olá **visão geral** folha para essa entidade.

Para obter mais informações sobre particionamento na camada de mensagens de Premium Olá, consulte [Premium do barramento de serviço e níveis de mensagens padrão](service-bus-premium-messaging.md). 

### <a name="create-a-partitioned-entity"></a>Criar uma entidade particionada

Há várias maneiras toocreate uma fila particionada ou tópico. Quando você cria Olá fila ou tópico do seu aplicativo, você pode habilitar o particionamento para Olá fila ou tópico por respectivamente Olá de configuração [QueueDescription.EnablePartitioning] [ QueueDescription.EnablePartitioning] ou [TopicDescription.EnablePartitioning] [ TopicDescription.EnablePartitioning] propriedade muito**true**. Essas propriedades devem ser definidas em Olá tempo Olá fila ou tópico é criado. Conforme mencionado anteriormente, é toochange não é possível essas propriedades em uma fila ou tópico existentes. Por exemplo:

```csharp
// Create partitioned topic
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

Como alternativa, você pode criar uma fila ou tópico particionado no hello [portal do Azure] [ Azure portal] ou no Visual Studio. Quando você cria uma fila ou tópico no portal de hello, Olá **ativar particionamento** opção Olá fila ou tópico **criar** folha é marcada por padrão. Você só pode desabilitar essa opção em uma entidade de camada padrão; no hello particionamento de camada Premium está sempre habilitado. No Visual Studio, clique em Olá **ativar particionamento** caixa de seleção no hello **nova fila** ou **novo tópico** caixa de diálogo.

## <a name="use-of-partition-keys"></a>Uso de chaves de partição
Quando uma mensagem é colocada em uma fila ou tópico particionado, barramento de serviço verifica a presença saudação de uma chave de partição. Se ele encontrar um, ele seleciona o fragmento de saudação com base na chave. Se não encontrar uma chave de partição, ele seleciona o fragmento de saudação com base em um algoritmo interno.

### <a name="using-a-partition-key"></a>Usando uma chave de partição
Alguns cenários, como sessões ou transações, exigem toobe mensagens armazenada em um fragmento específico. Todos esses cenários exigem o uso de saudação de uma chave de partição. Todas as mensagens que Olá de uso são atribuídos a mesma chave de partição toohello mesmo fragmento. Se o fragmento de saudação está temporariamente indisponível, o barramento de serviço retornará um erro.

Dependendo do cenário de hello, diferentes propriedades de mensagem são usadas como uma chave de partição:

**SessionId**: se uma mensagem de saudação [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] propriedade definida, em seguida, barramento de serviço usa essa propriedade como chave de partição hello. Dessa forma, todas as mensagens que pertencem a toohello mesma sessão são manipuladas pelo Olá mesmo agente de mensagens. Isso permite que mensagens do barramento de serviço tooguarantee ordenação, bem como a consistência de saudação de estados de sessão.

**PartitionKey**: se uma mensagem de saudação [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] propriedade, mas não Olá [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] propriedade definida, em seguida, o barramento de serviço usa Olá [PartitionKey] [ PartitionKey] propriedade como chave de partição hello. Se a mensagem de saudação tem dois Olá [SessionId] [ SessionId] e hello [PartitionKey] [ PartitionKey] propriedades definidas, ambas as propriedades devem ser idênticas. Se hello [PartitionKey] [ PartitionKey] propriedade está definida tooa valor diferente Olá [SessionId] [ SessionId] retorna de propriedade, barramento de serviço inválido exceção de operação. Olá [PartitionKey] [ PartitionKey] propriedade deve ser usada se um remetente envia mensagens transacionais cientes de sessão não. Olá chave de partição garante que todas as mensagens são enviadas em uma transação são manipuladas pelo Olá mesmo agente de mensagens.

**MessageId**: se Olá fila ou tópico tiver Olá [QueueDescription.RequiresDuplicateDetection] [ QueueDescription.RequiresDuplicateDetection] propriedade definida muito**true** e hello [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] ou [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] propriedades não estão definidas, em seguida, Olá [BrokeredMessage.MessageId] [ BrokeredMessage.MessageId] propriedade serve como chave de partição hello. (Observe que bibliotecas Microsoft .NET e AMQP do hello atribuir automaticamente uma ID de mensagem se o aplicativo de envio de saudação não). Nesse caso, todas as cópias da saudação mesma mensagem são manipuladas pelo Olá mesmo agente de mensagens. Isso permite que o barramento de serviço toodetect e elimine mensagens duplicadas. Se hello [QueueDescription.RequiresDuplicateDetection] [ QueueDescription.RequiresDuplicateDetection] propriedade não está definida muito**true**, barramento de serviço não considera Olá [MessageId] [ MessageId] a propriedade como uma chave de partição.

### <a name="not-using-a-partition-key"></a>Não usando uma chave de partição
Na ausência de saudação de uma chave de partição, o barramento de serviço distribui mensagens em um fragmentos de saudação tooall rodízio de saudação fila ou tópico particionados. Se o fragmento de saudação escolhido não estiver disponível, barramento de serviço atribui fragmento diferente de tooa de mensagem de saudação. Dessa forma, a operação de envio de saudação for bem-sucedida apesar da indisponibilidade temporária de saudação de um repositório de mensagens. No entanto, você não obterá Olá garantida de ordenação que fornece uma chave de partição.

Para obter uma discussão mais detalhada de compensação Olá entre disponibilidade (nenhuma chave de partição) e a consistência (usando uma chave de partição), consulte [neste artigo](../event-hubs/event-hubs-availability-and-consistency.md). Essas informações se aplicam igualmente entidades do barramento de serviço toopartitioned e partições de Hubs de eventos.

toogive serviço de barramento de mensagem de saudação suficiente tempo tooenqueue em um fragmento diferente, hello [MessagingFactorySettings.OperationTimeout] [ MessagingFactorySettings.OperationTimeout] valor especificado pelo cliente de saudação que envia a mensagem de saudação deve ser maior que 15 segundos. É recomendável que você defina Olá [OperationTimeout] [ OperationTimeout] valor padrão da propriedade toohello de 60 segundos.

Observe que uma chave de partição "fixa" um fragmento específico de tooa de mensagem. Se o repositório de mensagens de saudação que contém este fragmento estiver indisponível, o barramento de serviço retornará um erro. Na ausência de saudação de uma chave de partição, barramento de serviço pode escolher um fragmento diferente e Olá operação for bem-sucedida. Portanto, é recomendável que você não forneça uma chave de partição, a menos que seja necessário.

## <a name="advanced-topics-use-transactions-with-partitioned-entities"></a>Tópicos avançados: usar transações com entidades particionadas
As mensagens enviadas como parte de uma transação devem especificar uma chave de partição. Isso pode ser uma das seguintes propriedades de saudação: [BrokeredMessage.SessionId][BrokeredMessage.SessionId], [BrokeredMessage.PartitionKey][BrokeredMessage.PartitionKey], ou [ BrokeredMessage.MessageId][BrokeredMessage.MessageId]. Todas as mensagens são enviadas como parte da saudação deve especificar a mesma transação Olá a mesma chave de partição. Se você tentar toosend uma mensagem sem uma chave de partição em uma transação, o barramento de serviço retorna uma exceção de operação inválido. Se você tentar toosend várias mensagens em Olá mesma transação que têm diferentes chaves de partição, barramento de serviço retorna uma exceção de operação inválido. Por exemplo:

```csharp
CommittableTransaction committableTransaction = new CommittableTransaction();
using (TransactionScope ts = new TransactionScope(committableTransaction))
{
    BrokeredMessage msg = new BrokeredMessage("This is a message");
    msg.PartitionKey = "myPartitionKey";
    messageSender.Send(msg); 
    ts.Complete();
}
committableTransaction.Commit();
```

Se qualquer uma das propriedades de saudação que serve como uma chave de partição são definidas, pins de barramento de serviço Olá fragmento específico de tooa de mensagem. Esse comportamento ocorre quer uma transação seja usada ou não. É recomendável que você não especifique uma chave de partição se isso não for necessário.

## <a name="using-sessions-with-partitioned-entities"></a>Usando sessões com entidades particionadas
toosend um tópico de reconhecimento de sessão tooa mensagem transacional ou fila, a mensagem de saudação deve ter Olá [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] conjunto de propriedades. Se hello [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] propriedade também for especificada, ele deve ser idêntico toohello [SessionId] [ SessionId] propriedade. Caso elas sejam diferentes, o Barramento de Serviço retornará uma exceção de operação inválida.

Diferentemente de (não particionada) filas ou tópicos comuns, não é possível toouse toosend uma única transação várias sessões de toodifferent de mensagens. Se você tentar fazer isso, o Barramento de Serviço retornará uma exceção de operação inválida. Por exemplo:

```csharp
CommittableTransaction committableTransaction = new CommittableTransaction();
using (TransactionScope ts = new TransactionScope(committableTransaction))
{
    BrokeredMessage msg = new BrokeredMessage("This is a message");
    msg.SessionId = "mySession";
    messageSender.Send(msg); 
    ts.Complete();
}
committableTransaction.Commit();
```

## <a name="automatic-message-forwarding-with-partitioned-entities"></a>Encaminhamento automático de mensagens com entidades particionadas
O Barramento de Serviço dá suporte ao encaminhamento automático de mensagens de, para ou entre entidades particionadas. tooenable automático encaminhamento de mensagens, defina Olá [QueueDescription.ForwardTo] [ QueueDescription.ForwardTo] propriedade na fila de origem hello ou assinatura. Se a mensagem de saudação especifica uma chave de partição ([SessionId][SessionId], [PartitionKey][PartitionKey], ou [MessageId] [ MessageId]), essa chave de partição é usada para a entidade de destino hello.

## <a name="considerations-and-guidelines"></a>Considerações e diretrizes
* **Recursos de alta consistência**: se uma entidade usa recursos, como sessões, detecção de duplicidades ou controle explícito de chave de particionamento, operações de mensagens de saudação sempre são roteadas toospecific fragmentos. Se qualquer um dos fragmentos de saudação experiência de alto tráfego ou armazenamento subjacente Olá não está íntegro, essas operações falham e disponibilidade é reduzida. Em geral, a consistência de saudação é ainda muito maior do que entidades não particionado; apenas um subconjunto de tráfego está apresentando problemas, como tráfego de saudação tooall contrário. Para obter mais informações, consulte esta [discussão sobre disponibilidade e consistência](../event-hubs/event-hubs-availability-and-consistency.md).
* **Gerenciamento**: operações como criar, atualizar e excluir devem ser executadas em todos os fragmentos de saudação da entidade de saudação. Se qualquer fragmento não estiver íntegro, isso poderá resultar em falhas para essas operações. Para a operação de obtenção de Olá, informações como o número de mensagens devem ser agregadas de todos os fragmentos. Se qualquer fragmento não está íntegro, status de disponibilidade da entidade Olá é relatado como limitado.
* **Cenários de mensagem do volume de baixa**: para esses cenários, especialmente ao usar o protocolo de saudação HTTP, você pode ter tooperform várias operações de recebimento em ordem tooobtain todas as mensagens de saudação. Para receber solicitações, front-end Olá executa um recebimento em todos os fragmentos de saudação e armazena em cache todas as respostas de saudação recebidas. Uma solicitação de recebimento subsequente Olá conexão mesmo seria aproveitar esse cache e receber as latências será menor. No entanto, se você tiver várias conexões ou se usar HTTP, isso estabelecerá uma nova conexão para cada solicitação. Como tal, não há nenhuma garantia de que ele acabaria na Olá mesmo nó. Se todas as mensagens existentes são bloqueadas e armazenados em cache no outro front-end, Olá receber operação retorna **nulo**. As mensagens eventualmente expiram e você pode recebê-las novamente. O keep-alive de HTTP é recomendável.
* **Procurar/inspecionar mensagens**: [PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) sempre não retornar o número de saudação de mensagens especificadas no hello [MessageCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MessageCount) propriedade. Há duas razões comuns para isso. Uma razão é que Olá tamanho agregado de coleção de saudação de mensagens excede o tamanho de máximo de saudação de 256KB. Outro motivo é que, se Olá fila ou tópico tiver Olá [EnablePartitioning propriedade](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning) definido muito**true**, uma partição pode não ter suficiente mensagens toocomplete Olá solicitou o número de mensagens. Em geral, se um aplicativo deseja tooreceive um número específico de mensagens, é necessário chamar [PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) repetidamente até que ele obtém o número de mensagens ou não há nenhum mais toopeek de mensagens. Para obter mais informações, incluindo exemplos de código, confira [QueueClient.PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) ou [SubscriptionClient.PeekBatch](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient#Microsoft_ServiceBus_Messaging_SubscriptionClient_PeekBatch_System_Int32_).

## <a name="latest-added-features"></a>Últimos recursos adicionados
* Agora há suporte para adicionar ou remover regras com entidades particionadas. Diferentes de entidades não particionadas, essas operações não têm suporte em transações. 
* Agora há suporte para AMQP para enviar e receber mensagens tooand de uma entidade particionada.
* Agora há suporte para AMQP para Olá seguintes operações: [enviar lote](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_BrokeredMessage__), [lote receber](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_ReceiveBatch_System_Int32_), [receber pelo número de sequência](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_Receive_System_Int64_), [inspecionar](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_Peek), [ Renovar bloqueio](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_RenewMessageLock_System_Guid_), [agendar mensagem](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_ScheduleMessageAsync_Microsoft_ServiceBus_Messaging_BrokeredMessage_System_DateTimeOffset_), [Cancelar mensagem agendada](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_CancelScheduledMessageAsync_System_Int64_), [Adicionar regra](/dotnet/api/microsoft.servicebus.messaging.ruledescription), [remover regra](/dotnet/api/microsoft.servicebus.messaging.ruledescription), [Sessão renovar bloqueio](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_RenewLock), [definir estado de sessão](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_SetState_System_IO_Stream_), [obter o estado de sessão](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_GetState), e [enumerar sessões](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_GetMessageSessionsAsync).

## <a name="partitioned-entities-limitations"></a>Limitações das entidades particionadas
Atualmente o barramento de serviço impõe Olá seguintes limitações em filas e tópicos particionados:

* Filas e tópicos particionados não dão suporte para envio de mensagens que pertence a toodifferent sessões em uma única transação.
* Atualmente, o barramento de serviço permite too100 particionada filas ou tópicos por namespace. Cada fila ou tópico particionados conta para a cota de saudação de 10.000 entidades por namespace (não aplicar a camada de tooPremium).

## <a name="next-steps"></a>Próximas etapas
Consulte a discussão de saudação do [suporte a AMQP 1.0 para o barramento de serviço particionado filas e tópicos] [ AMQP 1.0 support for Service Bus partitioned queues and topics] toolearn mais sobre o particionamento de entidades de mensagens. 

[Service Bus architecture]: service-bus-architecture.md
[Azure portal]: https://portal.azure.com
[QueueDescription.EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning
[TopicDescription.EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.topicdescription#Microsoft_ServiceBus_Messaging_TopicDescription_EnablePartitioning
[BrokeredMessage.SessionId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId
[BrokeredMessage.PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_PartitionKey
[SessionId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId
[PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_PartitionKey
[QueueDescription.RequiresDuplicateDetection]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_RequiresDuplicateDetection
[BrokeredMessage.MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[MessagingFactorySettings.OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[AMQP 1.0 support for Service Bus partitioned queues and topics]: service-bus-partitioned-queues-and-topics-amqp-overview.md
