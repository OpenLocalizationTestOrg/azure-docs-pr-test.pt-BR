---
title: aaaAzure Service Bus emparelhado namespaces | Microsoft Docs
description: "Detalhes e custo de implementação do namespace emparelhado"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 2440c8d3-ed2e-47e0-93cf-ab7fbb855d2e
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: sethm
ms.openlocfilehash: 4c44b2b95d2228e1ad8075b52634d88a1593d3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="paired-namespace-implementation-details-and-cost-implications"></a>Detalhes e implicações de custo da implementação do namespace emparelhado
Olá [PairNamespaceAsync] [ PairNamespaceAsync] método, usando um [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] da instância, realiza tarefas visíveis em seu nome. Porque há questões de custo ao usar o recurso de Olá, é útil toounderstand as tarefas para que você espera que o comportamento de saudação quando isso acontece. Olá API emprega Olá seguinte comportamento automático em seu nome:

* Criação de filas de pendências.
* Criação de um [MessageSender] [ MessageSender] objeto que se comunica tooqueues ou tópicos.
* Quando uma entidade de mensagens se tornar indisponível, envia mensagens de ping toohello entidade em uma tentativa de toodetect quando essa entidade estará disponível novamente.
* Opcionalmente, cria um conjunto de "bombas de mensagens" mover as mensagens de Olá filas de lista de pendências toohello filas principais.
* Coordena o fechamento/falha de saudação primária e secundária [MessagingFactory] [ MessagingFactory] instâncias.

Em um nível alto, o recurso de saudação funciona da seguinte maneira: quando a entidade principal hello está íntegra, nenhuma alteração de comportamento ocorre. Olá quando [FailoverInterval] [ FailoverInterval] decorrer de duração, e entidade principal Olá não vê nenhum envia bem-sucedida após não transitório [MessagingException] [ MessagingException] ou um [TimeoutException][TimeoutException], Olá seguinte comportamento ocorre:

1. Envie operações toohello primário entidade são desabilitados e os pings de sistema Olá Olá entidade primária até que pings podem ser entregues com êxito.
2. Uma fila de pendências aleatória é selecionada.
3. [BrokeredMessage] [ BrokeredMessage] objetos são roteada toohello escolhido fila de pendências.
4. Se um toohello de operação de envio escolhida a fila de pendências falhar, essa fila é retirada da rotação hello e uma nova fila é selecionada. Todos os remetentes na Olá [MessagingFactory] [ MessagingFactory] instância saber de falha de saudação.

Olá figuras a seguir descrevem sequência hello. Primeiro, o remetente Olá envia mensagens.

![Namespaces emparelhados][0]

Após a falha toosend toohello fila primária remetente Olá começa a enviar mensagens tooa escolhido aleatoriamente a fila de pendências. Simultaneamente, ele inicia uma tarefa de ping.

![Namespaces emparelhados][1]

Nesse ponto, mensagens de saudação ainda estão na fila secundária hello e não tem sido entregue a fila primária toohello. Depois que a fila primária Olá estiver íntegra novamente, pelo menos um processo deve estar executando o sifão hello. Sifão Olá fornece mensagens de saudação Olá todas as pendências de várias entidades de destino adequadas de toohello filas (filas e tópicos).

![Namespaces emparelhados][2]

Olá restante deste tópico aborda detalhes específicos de saudação de como essas partes funcionam.

## <a name="creation-of-backlog-queues"></a>Criação de filas de pendências
Olá [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] objeto passado toohello [PairNamespaceAsync] [ PairNamespaceAsync] método indica Olá número de lista de pendências de filas que você deseja toouse. Cada fila de lista de pendências é criada com hello seguintes propriedades explicitamente definido (todos os outros valores são definidos toohello [QueueDescription] [ QueueDescription] padrões):

| Caminho | [namespace primário]/x-servicebus-transfer/[índice] no qual [índice] é um valor em [0, BacklogQueueCount) |
| --- | --- |
| MaxSizeInMegabytes |5120 |
| MaxDeliveryCount |int.MaxValue |
| DefaultMessageTimeToLive |TimeSpan.MaxValue |
| AutoDeleteOnIdle |TimeSpan.MaxValue |
| LockDuration |1 minuto |
| EnableDeadLetteringOnMessageExpiration |verdadeiro |
| EnableBatchedOperations |verdadeiro |

Por exemplo, a primeira fila de lista de pendências Olá criado para o namespace **contoso** chamado `contoso/x-servicebus-transfer/0`.

Ao criar filas hello, código de saudação primeiro verifica toosee se essa fila existe. Se a fila de saudação não existir, a fila Olá é criada. Olá código não limpa as filas de lista de pendências "extras". Especificamente, se hello aplicativo hello namespace primário **contoso** solicitar cinco filas de lista de pendências, mas uma fila de lista de pendências com caminho Olá `contoso/x-servicebus-transfer/7` existir, essa fila de pendências extra ainda está presente, mas não é usada. sistema de saudação explicitamente permite tooexist de filas de lista de pendências extras que não deve ser usado. Como proprietário do namespace Olá, você é responsável por limpar as filas de lista de pendências não utilizadas/indesejadas. Olá motivo essa decisão é que o barramento de serviço não é possível saber as finalidades existentes para todas as filas de saudação no seu namespace. Além disso, se uma fila existe com o nome hello, mas não atende Olá assumido [QueueDescription][QueueDescription], e seus motivos são seu próprios para alteração comportamento de padrão de saudação. Não há garantias para filas de lista de pendências de toohello modificações pelo seu código. Faça tootest-se de que as alterações completamente.

## <a name="custom-messagesender"></a>MessageSender personalizado
Ao enviar, todas as mensagens passam por meio de interno [MessageSender] [ MessageSender] objeto que se comporta normalmente quando tudo funciona e redireciona as filas de lista de pendências de toohello quando as coisas "quebra". Ao receber uma falha não transitória, um timer é iniciado. Após um [TimeSpan] [ TimeSpan] período consiste Olá [FailoverInterval] [ FailoverInterval] durante o qual nenhuma mensagem de êxito é enviadas de valor de propriedade , Olá failover for acionado. Neste ponto, hello acontecem estas coisas para cada entidade:

* Uma tarefa de ping executa cada [PingPrimaryInterval] [ PingPrimaryInterval] toocheck se Olá entidade está disponível. Se essa tarefa for bem-sucedida, todo o código do cliente que usa a entidade Olá imediatamente começa enviando novo namespace primário toohello de mensagens.
* As solicitações futuras toosend toothat mesma entidade de quaisquer outros remetentes resultará em Olá [BrokeredMessage] [ BrokeredMessage] enviados toobe modificado toosit na fila de lista de pendências de saudação. modificação de saudação remove algumas propriedades de saudação [BrokeredMessage] [ BrokeredMessage] do objeto e armazená-los em outro lugar. Olá propriedades a seguir são limpas e adicionadas em um novo alias, permitindo que o barramento de serviço e Olá mensagens do SDK tooprocess uniformemente:

| Nome antigo da propriedade | Novo nome da propriedade |
| --- | --- |
| SessionId |x-ms-sessionid |
| TimeToLive |x-ms-timetolive |
| ScheduledEnqueueTimeUtc |x-ms-path |

caminho de destino original Olá também é armazenado na mensagem de saudação como uma propriedade chamada x-ms-path. Esse design permite que mensagens para muitos toocoexist de entidades em uma fila única lista de pendências. Propriedades de saudação são traduzidas novamente pelo sifão hello.

Olá personalizado [MessageSender] [ MessageSender] objeto pode encontrar problemas quando as mensagens se aproximam limite de 256 KB hello e failover for acionado. Olá personalizado [MessageSender] [ MessageSender] objeto armazena as mensagens para todas as filas e tópicos juntos nas filas de lista de pendências de saudação. Esse objeto combina mensagens de vários principais juntos dentro de filas de lista de pendências de saudação. toohandle balanceamento de carga entre vários clientes que não souber cada outro, Olá SDK aleatoriamente escolhe uma fila de lista de pendências para cada [QueueClient] [ QueueClient] ou [TopicClient] [ TopicClient] criado no código.

## <a name="pings"></a>Pings
Uma mensagem de ping está vazio [BrokeredMessage] [ BrokeredMessage] com seus [ContentType] [ ContentType] propriedade definida tooapplication/vnd.ms-servicebus-ping e um [TimeToLive] [ TimeToLive] valor de 1 segundo. Esse ping tem uma característica especial no barramento de serviço: servidor de saudação nunca entrega um ping quando qualquer chamador solicita uma [BrokeredMessage][BrokeredMessage]. Assim, você nunca tiver toolearn como tooreceive e ignorar essas mensagens. Cada entidade (fila ou tópico exclusivo) por [MessagingFactory] [ MessagingFactory] instância por cliente executará ping quando eles são considerados toobe não está disponível. Por padrão, isso ocorre uma vez por minuto. Mensagens de ping são consideradas toobe regulares mensagens de barramento de serviço e podem resultar em encargos de largura de banda e mensagens. Assim que os clientes Olá detectam que o sistema hello está disponível, mensagens de saudação pararam.

## <a name="hello-syphon"></a>Sifão Olá
Pelo menos um programa executável no aplicativo hello deve estar ativamente executando sifão hello. Olá sifão realiza uma longa recepção de sondagem durante 15 minutos. Quando todas as entidades estão disponíveis e você tem 10 filas de lista de pendências, Olá aplicativo que hospeda a chamadas de sifão Olá Olá receber operação 40 vezes por hora, 960 vezes por dia e 28.800 vezes em 30 dias. Quando o sifão Olá move mensagens ativamente da fila primária do hello pendências toohello, cada mensagem passa por Olá encargos (encargos padrão para o tamanho da mensagem e largura de banda se aplica em todos os estágios) a seguir:

1. Envie a lista de pendências de toohello.
2. Receba da lista de pendências de saudação.
3. Envie toohello primário.
4. Receba Olá primário.

## <a name="closefault-behavior"></a>Comportamento de fechamento/falha
Dentro de um aplicativo que hospeda o sifão hello, uma vez Olá primário ou secundário [MessagingFactory] [ MessagingFactory] falha ou é fechada sem seu parceiro também sendo falha/fechamento e hello sifão detecta esse estado , sifão Olá atua. Se Olá outros [MessagingFactory] [ MessagingFactory] não for fechada dentro de 5 segundos, Olá sifão falha Olá ainda aberta [MessagingFactory] [ MessagingFactory] .

## <a name="next-steps"></a>Próximas etapas
Consulte [Padrões de sistema de mensagens assíncronas e alta disponibilidade][Asynchronous messaging patterns and high availability] para obter uma discussão detalhada da mensagem assíncrona do Barramento de Serviço. 

[PairNamespaceAsync]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PairNamespaceAsync_Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_
[SendAvailabilityPairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions
[MessageSender]: /dotnet/api/microsoft.servicebus.messaging.messagesender
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[FailoverInterval]: /dotnet/api/microsoft.servicebus.messaging.pairednamespaceoptions#Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_FailoverInterval
[MessagingException]: /dotnet/api/microsoft.servicebus.messaging.messagingexception
[TimeoutException]: https://msdn.microsoft.com/library/azure/system.timeoutexception.aspx
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[TimeSpan]: https://msdn.microsoft.com/library/azure/system.timespan.aspx
[PingPrimaryInterval]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_PingPrimaryInterval
[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[TopicClient]: /dotnet/api/microsoft.servicebus.messaging.topicclient
[ContentType]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ContentType
[TimeToLive]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive
[Asynchronous messaging patterns and high availability]: service-bus-async-messaging.md
[0]: ./media/service-bus-paired-namespaces/IC673405.png
[1]: ./media/service-bus-paired-namespaces/IC673406.png
[2]: ./media/service-bus-paired-namespaces/IC673407.png
