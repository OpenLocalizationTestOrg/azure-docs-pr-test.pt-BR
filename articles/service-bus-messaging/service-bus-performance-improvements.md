---
title: "práticas recomendadas de aaaBest para melhorar o desempenho usando o barramento de serviço do Azure | Microsoft Docs"
description: "Descreve como toouse durante a troca do barramento de serviço toooptimize desempenho orientado a mensagens."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e756c15d-31fc-45c0-8df4-0bca0da10bb2
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/10/2017
ms.author: sethm
ms.openlocfilehash: 52764d227757cbb11246675878933f21685817f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-performance-improvements-using-service-bus-messaging"></a>Práticas recomendadas para melhorias de desempenho usando o Sistema de Mensagens do Barramento de Serviço

Este artigo descreve como toouse [mensagens do barramento de serviço do Azure](https://azure.microsoft.com/services/service-bus/) toooptimize desempenho durante a troca de mensagens orientadas pelo. Olá primeira parte deste tópico descreve Olá diferentes mecanismos oferecidos toohelp aumentam o desempenho. segunda parte do Hello fornece orientação sobre como toouse barramento de serviço de forma que pode oferecer Olá melhor desempenho em um determinado cenário.

Ao longo deste tópico, o termo de hello "cliente" se refere a entidade tooany que acessa o barramento de serviço. Um cliente pode usar a função de saudação de um remetente ou destinatário. Olá termo "remetente" é usado para um cliente de fila ou tópico do barramento de serviço que envia mensagens tooa barramento de serviço fila ou tópico. termo Hello "destinatário" se refere a tooa barramento de serviço fila ou assinatura de cliente que recebe mensagens de uma fila do barramento de serviço ou a assinatura.

Estas seções apresentam vários conceitos que o barramento de serviço usa toohelp melhorar o desempenho.

## <a name="protocols"></a>Protocolos
Barramento de serviço permite que clientes toosend e recebam mensagens por meio de um dos três protocolos:

1. Advanced Message Queuing Protocol (AMQP)
2. Protocolo do sistema de mensagens do Barramento de Serviço (SBMP)
3. HTTP

AMQP e SBMP são mais eficientes, porque eles mantenham Olá conexão tooService barramento desde que a fábrica de mensagens de saudação existe. Ele também implementa o envio em lote e a pré-busca. A menos que mencionado explicitamente, todo o conteúdo deste tópico assume o uso de saudação do AMQP ou SBMP.

## <a name="reusing-factories-and-clients"></a>Reutilizando fábricas e clientes
Os objetos de cliente do Barramento de Serviço, como [QueueClient][QueueClient] ou [MessageSender][MessageSender], são criados por meio de um objeto [MessagingFactory][MessagingFactory], que também oferece gerenciamento interno de conexões. Você não deve fechar fábricas de mensagens ou fila, tópico e clientes de assinatura depois de enviar uma mensagem e, em seguida, recriá-las ao enviar mensagem de saudação do próxima. Fechar uma fábrica de mensagens exclui Olá conexão toohello serviço service Bus, e uma nova conexão é estabelecida ao recriar a fábrica de saudação. Estabelecer que uma conexão é uma operação cara que você pode evitar novamente usando Olá mesma fábrica e cliente objetos para várias operações. Você pode usar com segurança Olá [QueueClient] [ QueueClient] objeto para enviar mensagens de operações assíncronas simultâneas e de vários threads. 

## <a name="concurrent-operations"></a>Operações simultâneas
A execução de uma operação (enviar, receber, excluir etc.) leva algum tempo. Esse tempo inclui o processamento de Olá da operação de saudação pelo Olá barramento de serviço na latência de toohello de adição de solicitação de saudação e resposta de saudação. número de saudação tooincrease de operações por vez, as operações devem ser executadas simultaneamente. Você pode fazer isso de várias maneiras diferentes:

* **Operações assíncronas**: cliente Olá agenda operações realizando operações assíncronas. Olá próxima solicitação é iniciada antes da conclusão da solicitação anterior de saudação. Olá seguinte é um exemplo de uma operação de envio assíncrono:
  
 ```csharp
  BrokeredMessage m1 = new BrokeredMessage(body);
  BrokeredMessage m2 = new BrokeredMessage(body);
  
  Task send1 = queueClient.SendAsync(m1).ContinueWith((t) => 
    {
      Console.WriteLine("Sent message #1");
    });
  Task send2 = queueClient.SendAsync(m2).ContinueWith((t) => 
    {
      Console.WriteLine("Sent message #2");
    });
  Task.WaitAll(send1, send2);
  Console.WriteLine("All messages sent");
  ```
  
  Este é um exemplo de uma operação de recebimento assíncrono:
  
  ```csharp
  Task receive1 = queueClient.ReceiveAsync().ContinueWith(ProcessReceivedMessage);
  Task receive2 = queueClient.ReceiveAsync().ContinueWith(ProcessReceivedMessage);
  
  Task.WaitAll(receive1, receive2);
  Console.WriteLine("All messages received");
  
  async void ProcessReceivedMessage(Task<BrokeredMessage> t)
  {
    BrokeredMessage m = t.Result;
    Console.WriteLine("{0} received", m.Label);
    await m.CompleteAsync();
    Console.WriteLine("{0} complete", m.Label);
  }
  ```
* **Diversas fábricas**: todos os clientes (remetentes de adição tooreceivers) que são criados por Olá mesma fábrica compartilhamento um TCP conexão. taxa de transferência de máximo de mensagem de saudação é limitada pelo número de saudação de operações que podem passar por essa conexão TCP. taxa de transferência de saudação que pode ser obtida com uma única fábrica varia muito de acordo com os horários de ida e volta do TCP e o tamanho da mensagem. taxas de transferência mais altas tooobtain, você deve usar diversas fábricas de mensagens.

## <a name="receive-mode"></a>Modo de recebimento
Ao criar um cliente de fila ou de assinatura, você poderá especificar um modo de recebimento: *Bloqueio de pico* ou *Receber e Excluir*. modo de recebimento saudação padrão é [PeekLock][PeekLock]. Ao operar nesse modo, o cliente de saudação envia uma solicitação tooreceive uma mensagem do barramento de serviço. Depois de saudação cliente receber uma mensagem de saudação, ele envia uma mensagem de saudação do toocomplete de solicitação.

Quando definir Olá modo de recebimento muito[ReceiveAndDelete][ReceiveAndDelete], ambas as etapas são combinadas em uma única solicitação. Isso reduz o número geral das operações de saudação e pode melhorar Olá geral taxa de transferência de mensagem. O ganho de desempenho vem corre o risco de saudação de perda de mensagens.

O Barramento de Serviço não dá suporte a transações para operações de receber e excluir. Além disso, a semântica de bloqueio de inspeção é necessária para os cenários nos quais Olá cliente quer toodefer ou [mortas](service-bus-dead-letter-queues.md) uma mensagem.

## <a name="client-side-batching"></a>Envio em lote no lado do cliente
O envio em lote do lado do cliente permite que uma fila ou tópico cliente toodelay Olá envio de uma mensagem para um determinado período de tempo. Se o cliente Olá envia mensagens adicionais durante esse período, ele transmite mensagens de saudação em um único lote. O envio em lote do lado do cliente também faz com que um toobatch de cliente de fila ou assinatura vários **concluir** solicitações em uma única solicitação. O envio em lote está disponível apenas para operações **Enviar** e **Concluir** assíncronas. Operações síncronas são enviadas imediatamente toohello do barramento de serviço do serviço. O envio em lote não ocorre para as operações de pico ou de recebimento, e também não ocorre entre clientes.

Por padrão, um cliente usa um intervalo de lote de 20 ms. Você pode alterar o intervalo de lote de saudação por configuração Olá [BatchFlushInterval] [ BatchFlushInterval] Olá propriedade antes de criar a fábrica de mensagens. Essa configuração afeta todos os clientes criados por essa fábrica.

toodisable envio em lote, defina Olá [BatchFlushInterval] [ BatchFlushInterval] propriedade muito**TimeSpan**. Por exemplo:

```csharp
MessagingFactorySettings mfs = new MessagingFactorySettings();
mfs.TokenProvider = tokenProvider;
mfs.NetMessagingTransportSettings.BatchFlushInterval = TimeSpan.FromSeconds(0.05);
MessagingFactory messagingFactory = MessagingFactory.Create(namespaceUri, mfs);
```

Envio em lote não afeta o número de saudação de operações de mensagens faturáveis e está disponível apenas para Olá protocolo de cliente do barramento de serviço. Olá protocolo HTTP não dá suporte a envio em lote.

## <a name="batching-store-access"></a>Acesso ao repositório do envio em lote
taxa de transferência tooincrease Olá de fila, tópico ou assinatura, o barramento de serviço agrupa várias mensagens ao gravar repositório interno tooits. Se habilitada em uma fila ou tópico, gravar mensagens no repositório de saudação será agrupada. Se habilitada em uma fila ou assinatura, a exclusão de mensagens do repositório de saudação será agrupada. Se o acesso ao repositório em lote estiver habilitado para uma entidade, o barramento de serviço atrasa a uma operação de gravação do repositório em relação essa entidade por backup too20ms. Operações de armazenamento adicionais que ocorrem durante esse intervalo são adicionadas toohello lote. O acesso ao repositório em lote só afetará as operações **Enviar** e **Concluir**; as operações de receber não são afetadas. O acesso ao repositório em lote é uma propriedade em uma entidade. O envio em lote ocorrerá em todas as entidades que permitirem o acesso ao repositório em lote.

Quando uma nova fila, um novo tópico ou uma nova assinatura for criada, o acesso ao repositório em lote será habilitado por padrão. conjunto Olá acesso ao repositório em lote de toodisable [EnableBatchedOperations] [ EnableBatchedOperations] propriedade muito**false** antes de criar a entidade de saudação. Por exemplo:

```csharp
QueueDescription qd = new QueueDescription();
qd.EnableBatchedOperations = false;
Queue q = namespaceManager.CreateQueue(qd);
```

Acesso ao repositório em lote não afeta o número de saudação de operações de mensagens faturáveis e é uma propriedade de uma fila, tópico ou assinatura. É independente do hello receber modo e hello protocolo usado entre um cliente e hello barramento de serviço.

## <a name="prefetching"></a>Pré-busca
A pré-busca permite fila ou assinatura de cliente tooload adicionais mensagens de saudação do serviço de saudação quando ele executa uma operação de recebimento. cliente Olá armazena essas mensagens em um cache local. tamanho de saudação do cache de saudação é determinado pelo Olá [Prefetchcounté] [ QueueClient.PrefetchCount] ou [ubscriptionclient. Prefetchcount] [ SubscriptionClient.PrefetchCount] Propriedades. Cada cliente que permite a pré-busca mantém seu próprio cache. Um cache não é compartilhado entre os clientes. Se o cliente de saudação inicia uma operação de recebimento e o cache estiver vazio, o serviço de saudação transmite um lote de mensagens. Olá tamanho de lote de saudação é igual ao tamanho de saudação do cache de saudação ou 256 KB, o que for menor. Se o cliente Olá inicia uma operação de recebimento e cache de saudação contém uma mensagem, mensagem de saudação será removida do cache de saudação.

Quando uma mensagem passa por pré-busca, mensagem de saudação de bloqueios pré-busca serviço hello. Ao fazer isso, mensagem de pré-busca de saudação não pode ser recebida por um destinatário diferente. Se o destinatário Olá não pode concluir a mensagem de saudação antes de expira o bloqueio de Olá, mensagem de saudação torna-se receptores tooother disponíveis. cópia de pré-busca de saudação de mensagem de saudação permanece no cache de saudação. Olá receptor que consome Olá expirou em cache cópia receberá uma exceção quando ele tenta toocomplete essa mensagem. Por padrão, o bloqueio de mensagem de saudação expira após 60 segundos. Esse valor pode ser estendido too5 minutos. tooprevent o consumo de saudação de mensagens expiradas, tamanho do cache de saudação sempre deve ser menor que o número de saudação de mensagens que podem ser consumidos por um cliente dentro do intervalo de tempo limite de bloqueio de saudação.

Ao usar Olá expiração de bloqueio padrão de 60 segundos, um bom valor para [ubscriptionclient. Prefetchcount] [ SubscriptionClient.PrefetchCount] é 20 vezes Olá máximo taxas de processamento de todos os destinatários da fábrica de saudação. Por exemplo, uma fábrica cria 3 receptores e cada receptor pode processar as mensagens de too10 por segundo. Contagem de pré-busca de saudação não deve exceder 20 X 3 X 10 = 600. Por padrão, [Prefetchcounté] [ QueueClient.PrefetchCount] é too0 de conjunto, o que significa que não há mensagens adicionais buscadas do serviço de saudação.

Aumenta Olá produtividade geral para uma fila ou assinatura porque reduz Olá geral número de operações de mensagens ou viagens de ida e as mensagens de pré-busca. Busca a primeira mensagem de saudação, no entanto, levará mais tempo (devido toohello maior tamanho da mensagem). Receber mensagens de pré-busca será mais rápido porque essas mensagens já foram baixadas pelo cliente hello.

Olá time-to-live (TTL) propriedade de uma mensagem é verificada pelo servidor de saudação em tempo de saudação servidor Olá envia o cliente de toohello de mensagem de saudação. cliente de saudação não verifica a propriedade TTL da mensagem de saudação após o recebimento de mensagem de saudação. Em vez disso, mensagem de saudação pode ser recebida mesmo que o TTL da mensagem de saudação tenha passado enquanto a mensagem de saudação foi armazenado em cache pelo cliente de saudação.

A pré-busca não afeta o número de saudação de operações de mensagens faturáveis e está disponível apenas para Olá protocolo de cliente do barramento de serviço. Olá protocolo HTTP não oferece suporte a pré-busca. A pré-busca está disponível para as operações de recebimento síncrono e assíncrono.

## <a name="express-queues-and-topics"></a>Filas e tópicos expressos

Entidades expressas permitem cenários de redução da latência e alta taxa de transferência e têm suporte apenas na camada de mensagem padrão hello. Entidades criadas em [namespaces Premium](service-bus-premium-messaging.md) não oferecem suporte a opção express hello. Com entidades expressas, se uma mensagem é enviada tooa fila ou tópico, mensagem de saudação não é imediatamente armazenada no repositório de mensagens de saudação. Em vez disso, ela será armazenada em cache na memória. Se uma mensagem permanece na fila de saudação por mais de alguns segundos, é automaticamente gravada armazenamento toostable, protegendo contra perda de vencimento tooan interrupção. Armazenamento de mensagem de saudação do tempo de saudação gravar a mensagem de saudação em um cache de memória aumenta a taxa de transferência e reduz a latência porque não há nenhum toostable de acesso é enviado. As mensagens consumidas em alguns segundos não são gravadas toohello repositório de mensagens. saudação de exemplo a seguir cria um tópico expresso.

```csharp
TopicDescription td = new TopicDescription(TopicName);
td.EnableExpress = true;
namespaceManager.CreateTopic(td);
```

Se uma mensagem que contém informações importantes que não devem ser perdidas é enviada entidade expressa tooan, remetente Olá poderá forçar o barramento de serviço tooimmediately manter toostable armazenamento de mensagem de saudação, definindo Olá [ForcePersistence] [ ForcePersistence] propriedade muito**true**.

> [!NOTE]
> As entidades expressas não dão suporte a transações.

## <a name="use-of-partitioned-queues-or-topics"></a>Uso de filas ou tópicos particionados
Internamente, o barramento de serviço usa Olá mesmo nó e tooprocess do repositório de mensagens e armazena todas as mensagens de uma entidade de mensagens (fila ou tópico). Uma fila ou tópico particionado, em Olá outro lado, é distribuído em vários nós e repositórios de mensagens. As filas e tópicos particionados não só geram uma taxa de transferência mais alta do que as filas e os tópicos normais, como também exibem disponibilidade superior. toocreate uma entidade particionada, Olá conjunto [EnablePartitioning] [ EnablePartitioning] propriedade muito**true**, conforme mostrado no exemplo a seguir de saudação. Para obter mais informações sobre entidades particionadas, veja as [Entidades de Mensagens Particionadas][Partitioned messaging entities].

```csharp
// Create partitioned queue.
QueueDescription qd = new QueueDescription(QueueName);
qd.EnablePartitioning = true;
namespaceManager.CreateQueue(qd);
```

## <a name="use-of-multiple-queues"></a>Uso de várias filas

Se não for possível toouse que uma fila ou tópico ou particionado Olá esperado de carga não pode ser manipulada por uma única fila ou tópico particionados, você deve usar várias entidades de mensagens. Ao usar várias entidades, crie um cliente dedicado para cada entidade, em vez de usar Olá mesmo cliente para todas as entidades.

## <a name="development-and-testing-features"></a>Recursos de desenvolvimento e teste

O Barramento de Serviço tem um recurso usado especificamente para desenvolvimento que **nunca deve ser usado em configurações de produção**: [TopicDescription.EnableFilteringMessagesBeforePublishing][].

Quando novas regras ou os filtros são adicionados toohello tópico, você pode usar [TopicDescription.EnableFilteringMessagesBeforePublishing][] tooverify que Olá nova expressão de filtro está funcionando conforme o esperado.

## <a name="scenarios"></a>Cenários
Olá seções a seguir descrevem situações típicas de mensagens e descrevem configurações de barramento do serviço Olá preferido. As taxas de transferência são classificadas como pequena (menos de 1 mensagem/segundo), moderada (1 mensagem/segundo ou mais, mas menos de 100 mensagens por segundo) e alta (100 mensagens/segundo ou mais). Olá número de clientes é classificado como pequeno (5 ou menos), moderado (mais de 5 mas menor que ou igual too20) e grandes (mais de 20).

### <a name="high-throughput-queue"></a>Fila de alta taxa de transferência
Meta: Maximize a taxa de transferência de saudação de uma única fila. saudação de número de remetentes e destinatários é pequena.

* Use uma fila particionada para obter desempenho e disponibilidade aprimorados.
* saudação de tooincrease geral taxa de envio na fila de saudação, use vários remetentes de toocreate de fábricas de mensagens. Para cada remetente, use operações assíncronas ou vários threads.
* saudação de tooincrease geral taxa de recebimento da fila de hello, use vários receptores de toocreate de fábricas de mensagens.
* Use operações assíncronas tootake aproveitar o envio em lote do lado do cliente.
* Definir Olá intervalo too50ms tooreduce Olá o número de transmissões de protocolo de cliente do barramento de serviço de lote. Se forem usados vários remetentes, aumente Olá too100ms de intervalo de processamento em lotes.
* Deixe o acesso ao repositório em lote habilitado. Isso aumenta a saudação geral taxa na qual as mensagens podem ser gravadas na fila de saudação.
* Defina tempos de too20 de contagem de pré-busca de saudação taxas de processamento máximo de saudação de todos os destinatários de uma fábrica. Isso reduz o número de saudação de transmissões de protocolo de cliente do barramento de serviço.

### <a name="multiple-high-throughput-queues"></a>Várias filas de alta taxa de transferência
Meta: maximize a taxa de transferência geral de diversas filas. taxa de transferência de saudação de uma fila individual é moderada ou alta.

tooobtain taxa de transferência máxima em várias filas, usar Olá configurações descritas toomaximize taxa de transferência de saudação de uma única fila. Além disso, use os clientes toocreate de fábricas diferentes que enviar ou recebem de diferentes filas.

### <a name="low-latency-queue"></a>Fila de baixa latência
Meta: minimize a latência de ponta a ponta de uma fila ou um tópico. saudação de número de remetentes e destinatários é pequena. taxa de transferência de saudação da fila de saudação é pequena ou moderada.

* Use uma fila particionada para obter disponibilidade aprimorada.
* Desabilite o envio em lote no lado do cliente. cliente Olá envia imediatamente uma mensagem.
* Desabilite o acesso ao repositório em lote. serviço Olá grava imediatamente o repositório de toohello de mensagens de saudação.
* Se usar um único cliente, defina Olá pré-busca contagem too20 vezes Olá taxa de processamento do destinatário hello. Se várias mensagens chegarem à fila de saudação em Olá mesmo tempo, Olá protocolo de cliente do barramento de serviço transmite todas ao Olá simultaneamente. Quando Olá cliente recebe a mensagem de saudação do próxima, essa mensagem já está no cache local hello. Olá cache deve ser pequeno.
* Se o uso de vários clientes, defina Olá too0 de contagem de pré-busca. Ao fazer isso, a saudação segundo cliente pode receber mensagem de saudação do segundo, enquanto o cliente primeiro Olá ainda está processando a mensagem de saudação do primeiro.

### <a name="queue-with-a-large-number-of-senders"></a>Fila com um grande número de remetentes
Meta: maximizar a taxa de transferência de uma fila ou tópico com um grande número de remetentes. Cada remetente envia mensagens com uma taxa moderada. saudação de número de destinatários é pequena.

Barramento de serviço permite que o too1000 conexões simultâneas tooa entidade de mensagens (ou 5.000 usando AMQP). Esse limite é aplicado no nível de namespace hello e tópicos/filas/assinaturas são controladas pelo limite de saudação de conexões simultâneas por namespace. Para filas, esse número é compartilhado entre remetentes e receptores. Se todas as conexões de 1000 são necessárias para remetentes, substitua Olá fila com um tópico e uma única assinatura. Um tópico aceita too1000 de conexões simultâneas dos remetentes, enquanto a assinatura Olá aceita um 1000 adicionais conexões simultâneas dos destinatários. Se mais de 1000 remetentes simultâneos são necessários, remetentes Olá envie mensagens toohello protocolo de barramento de serviço por meio de HTTP.

taxa de transferência toomaximize, Olá a seguir:

* Use uma fila particionada para obter desempenho e disponibilidade aprimorados.
* Se cada remetente residir em um processo diferente, use somente uma única fábrica por processo.
* Use operações assíncronas tootake aproveitar o envio em lote do lado do cliente.
* Use padrão de saudação envio em lote de intervalo de 20 ms tooreduce Olá número de transmissões de protocolo de cliente do barramento de serviço.
* Deixe o acesso ao repositório em lote habilitado. Isso aumenta a saudação geral taxa na qual as mensagens podem ser gravadas para Olá fila ou tópico.
* Defina tempos de too20 de contagem de pré-busca de saudação taxas de processamento máximo de saudação de todos os destinatários de uma fábrica. Isso reduz o número de saudação de transmissões de protocolo de cliente do barramento de serviço.

### <a name="queue-with-a-large-number-of-receivers"></a>Fila com um grande número de receptores
Objetivo: Maximizar Olá receber a taxa de uma fila ou assinatura com um grande número de destinatários. Cada receptor recebe mensagens a uma taxa moderada. saudação de número de remetentes é pequena.

Barramento de serviço permite que a entidade de tooan too1000 conexões simultâneas. Se uma fila exigir mais de 1000 destinatários, substitua Olá fila com um tópico e várias assinaturas. Cada assinatura pode oferecer suporte a conexões simultâneas too1000. Como alternativa, os destinatários podem acessar fila Olá via Olá protocolo HTTP.

taxa de transferência toomaximize, Olá a seguir:

* Use uma fila particionada para obter desempenho e disponibilidade aprimorados.
* Se cada receptor residir em um processo diferente, use somente uma única fábrica por processo.
* Os receptores poderão usar operações síncronas ou assíncronas. Fornecido Olá moderada receber taxa de um destinatário individual, do lado do cliente em lotes de uma solicitação concluir não afetam a taxa de transferência do destinatário.
* Deixe o acesso ao repositório em lote habilitado. Isso reduz a saudação carga geral da entidade de saudação. Isso também reduz o hello taxa geral em que as mensagens podem ser gravadas em Olá fila ou tópico.
* Definir Olá pré-busca contagem tooa pequeno valor (por exemplo, PrefetchCount = 10). Isso impede que os receptores fiquem ociosos enquanto outros receptores tenham grandes quantidades de mensagens armazenadas em cache.

### <a name="topic-with-a-small-number-of-subscriptions"></a>Tópico com um pequeno número de assinaturas
Objetivo: Maximize a taxa de transferência de saudação de um tópico com um pequeno número de assinaturas. Uma mensagem é recebida por várias assinaturas, que significa Olá combinada de recebimento taxa por todas as assinaturas é maior do que a taxa de envio de saudação. saudação de número de remetentes é pequena. saudação de número de destinatários por assinatura é pequena.

taxa de transferência toomaximize, Olá a seguir:

* Use um tópico particionado para obter desempenho e disponibilidade aprimorados.
* saudação de tooincrease geral taxa de envio no tópico Olá, use vários remetentes de toocreate de fábricas de mensagens. Para cada remetente, use operações assíncronas ou vários threads.
* saudação de tooincrease geral taxa de recebimento de uma assinatura, use vários receptores de toocreate de fábricas de mensagens. Para cada receptor, use operações assíncronas ou vários threads.
* Use operações assíncronas tootake aproveitar o envio em lote do lado do cliente.
* Use padrão de saudação envio em lote de intervalo de 20 ms tooreduce Olá número de transmissões de protocolo de cliente do barramento de serviço.
* Deixe o acesso ao repositório em lote habilitado. Isso aumenta a saudação geral taxa em que as mensagens podem ser gravadas no tópico de saudação.
* Defina tempos de too20 de contagem de pré-busca de saudação taxas de processamento máximo de saudação de todos os destinatários de uma fábrica. Isso reduz o número de saudação de transmissões de protocolo de cliente do barramento de serviço.

### <a name="topic-with-a-large-number-of-subscriptions"></a>Tópico com um grande número de assinaturas
Objetivo: Maximize a taxa de transferência de saudação de um tópico com um grande número de assinaturas. Uma mensagem é recebida por várias assinaturas, que significa Olá combinada de recebimento taxa por todas as assinaturas é muito maior do que a taxa de envio de saudação. saudação de número de remetentes é pequena. saudação de número de destinatários por assinatura é pequena.

Tópicos com um grande número de assinaturas normalmente expõem um rendimento geral baixo se todas as mensagens são roteadas tooall assinaturas. Isso é causado pelo fato Olá cada mensagem é recebida várias vezes e todas as mensagens que estão contidas em um tópico e todas as suas assinaturas são armazenadas no hello mesmo repositório. Presume-se que o número de saudação de remetentes e número de destinatários por assinatura são pequenos. Barramento de serviço dá suporte para até too2, 000 assinaturas por tópico.

taxa de transferência toomaximize, Olá a seguir:

* Use um tópico particionado para obter desempenho e disponibilidade aprimorados.
* Use operações assíncronas tootake aproveitar o envio em lote do lado do cliente.
* Use padrão de saudação envio em lote de intervalo de 20 ms tooreduce Olá número de transmissões de protocolo de cliente do barramento de serviço.
* Deixe o acesso ao repositório em lote habilitado. Isso aumenta a saudação geral taxa em que as mensagens podem ser gravadas no tópico de saudação.
* Defina receber Olá esperado dos tempos de too20 de contagem Olá pré-busca de taxa em segundos. Isso reduz o número de saudação de transmissões de protocolo de cliente do barramento de serviço.

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre como otimizar o desempenho do barramento de serviço, consulte [particionada entidades de mensagens][Partitioned messaging entities].

[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[MessageSender]: /dotnet/api/microsoft.servicebus.messaging.messagesender
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[PeekLock]: /dotnet/api/microsoft.servicebus.messaging.receivemode
[ReceiveAndDelete]: /dotnet/api/microsoft.servicebus.messaging.receivemode
[BatchFlushInterval]: /dotnet/api/microsoft.servicebus.messaging.netmessagingtransportsettings.batchflushinterval#Microsoft_ServiceBus_Messaging_NetMessagingTransportSettings_BatchFlushInterval
[EnableBatchedOperations]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.enablebatchedoperations#Microsoft_ServiceBus_Messaging_QueueDescription_EnableBatchedOperations
[QueueClient.PrefetchCount]: /dotnet/api/microsoft.servicebus.messaging.queueclient.prefetchcount#Microsoft_ServiceBus_Messaging_QueueClient_PrefetchCount
[SubscriptionClient.PrefetchCount]: /dotnet/api/microsoft.servicebus.messaging.subscriptionclient.prefetchcount#Microsoft_ServiceBus_Messaging_SubscriptionClient_PrefetchCount
[ForcePersistence]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage.forcepersistence#Microsoft_ServiceBus_Messaging_BrokeredMessage_ForcePersistence
[EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.enablepartitioning#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning
[Partitioned messaging entities]: service-bus-partitioning.md
[TopicDescription.EnableFilteringMessagesBeforePublishing]: /dotnet/api/microsoft.servicebus.messaging.topicdescription.enablefilteringmessagesbeforepublishing#Microsoft_ServiceBus_Messaging_TopicDescription_EnableFilteringMessagesBeforePublishing
