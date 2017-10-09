---
title: "aaaService do barramento do sistema de mensagens assíncronas | Microsoft Docs"
description: "Descrição da mensagem assíncrona do Barramento de Serviço do Azure."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f1435549-e1f2-40cb-a280-64ea07b39fc7
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: sethm
ms.openlocfilehash: 5ab6ddf052155a9dd975b413cfaf393119c1999d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="asynchronous-messaging-patterns-and-high-availability"></a>Padrões de mensagens assíncronas e alta disponibilidade

O serviço de mensagens assíncrono pode ser implementado de diversas maneiras diferentes. Com filas, tópicos e assinaturas, o Barramento de Serviço do Azure dá suporte ao assincronismo por meio de um mecanismo de encaminhamento e repositório. Em operação (síncrona) normal, enviar mensagens tooqueues e tópicos e receber mensagens de filas e assinaturas. Os aplicativos escritos por você dependem de essas entidades estarem sempre disponíveis. Quando alterado de integridade de entidade Olá, devido tooa várias circunstâncias, é necessário um tooprovide de maneira uma entidade de reduzir a capacidade que pode satisfazer a maioria das necessidades.

Aplicativos geralmente usam tooenable mensagens padrões assíncronas vários cenários de comunicação. Você pode criar aplicativos no qual os clientes podem enviar mensagens tooservices, mesmo quando o serviço Olá não está em execução. Para aplicativos que apresentam picos de comunicações, uma fila pode ajudar Olá nível de carga, fornecendo uma comunicação de toobuffer local. Por fim, você pode obter uma carga simple, porém efetiva mensagens de toodistribute balanceador em vários computadores.

Disponibilidade de toomaintain de ordem de qualquer uma dessas entidades, considere um número de diferentes maneiras em que essas entidades podem aparecer indisponíveis para um sistema de mensagens durável. Em geral, podemos ver entidade Olá se tornar indisponível tooapplications que gravamos Olá diferentes maneiras a seguir:

* Não é possível toosend mensagens.
* Não é possível tooreceive mensagens.
* Não é possível toomanage entidades (criar, recuperar, atualizar ou excluir entidades).
* Serviço de saudação toocontact não é possível.

Para cada uma dessas falhas, existe modos de falhas diferentes que permitem que um trabalho do aplicativo toocontinue tooperform em algum nível de capacidade reduzida. Por exemplo, um sistema que pode enviar mensagens, mas não recebê-las, ainda pode receber pedidos de clientes, mas não pode processar esses pedidos. Este tópico aborda problemas potenciais que podem ocorrer e como eles são atenuados. Barramento de serviço introduziu um número de mitigações que você deve aceitar e este tópico também discute Olá regras que administram Olá usam essas opções de atenuantes.

## <a name="reliability-in-service-bus"></a>Confiabilidade no Barramento de Serviço
Há várias maneiras de problemas de mensagem e entidade toohandle e há diretrizes que regem o uso de saudação apropriado dessas atenuantes. diretrizes de saudação toounderstand, você deve compreender o que pode falhar no barramento de serviço. Devido a toohello design dos sistemas do Azure, todos esses problemas tendem toobe curta duração. Em um nível alto, diferentes causas Olá de indisponibilidade aparecem da seguinte maneira:

* A limitação de um sistema externo do qual o Barramento de Serviço depende. A limitação ocorre devido a interações com os recursos de computação e armazenamento.
* Problema para um sistema do qual o Barramento de Serviço depende. Por exemplo, determinado armazenamento pode encontrar problemas.
* Falha do Barramento de Serviço em um único subsistema. Nessa situação, um nó de computação pode entrar em um estado inconsistente e deve reiniciar sozinho, fazendo com que todas as entidades serve saldo tooload tooother nós. Por sua vez, isso pode causar um curto período de processamento de mensagens lento.
* Falha do Barramento de Serviço em um datacenter do Azure. Este é uma "Falha catastrófica" durante o qual o sistema hello está inacessível por vários minutos ou algumas horas.

> [!NOTE]
> termo Olá **armazenamento** pode significar o armazenamento do Azure e SQL Azure.
> 
> 

O Barramento de Serviço contém várias mitigações para esses problemas. Olá seções a seguir discutem cada problema e as respectivas atenuantes.

### <a name="throttling"></a>Limitação
Com o Barramento de Serviço, a limitação possibilita o gerenciamento cooperativo de taxa de mensagens. Cada nó individual do Barramento de Serviço hospeda várias entidades. Cada uma dessas entidades exige Olá sistema em termos de CPU, memória, armazenamento e outras facetas. Quando qualquer um desses aspectos detecta uso que excede os limites definidos, o Barramento de Serviço pode negar determinada solicitação. Olá chamador recebe um [ServerBusyException] [ ServerBusyException] e recupera após 10 segundos.

Como uma mitigação código Olá deve Olá erro de leitura e parar qualquer recuperação da mensagem de saudação pelo menos 10 segundos. Como Olá erro pode ocorrer em pedaços do aplicativo de cliente hello, espera-se que cada pedaço execute independentemente uma lógica de repetição de saudação. código de saudação pode reduzir a probabilidade de saudação do que está sendo limitado ao ativar particionamento em uma fila ou tópico.

### <a name="issue-for-an-azure-dependency"></a>Problema para uma dependência do Azure
Ocasionalmente, outros componentes do Azure podem ter problemas de serviço. Por exemplo, quando um sistema que usa o Barramento de Serviço está sendo atualizado, esse sistema pode ter os recursos reduzidos temporariamente. toowork com esses tipos de problemas, Service Bus regularmente investiga e implementa atenuantes. Ocorrem efeitos colaterais dessas mitigações. Por exemplo, toohandle transitório problemas com armazenamento, barramento de serviço implementa um sistema que permite toowork de operações de envio de mensagem de forma consistente. Devido a natureza toohello mitigação Olá, uma mensagem enviada pode levar até too15 minutos tooappear na fila de saudação afetada ou assinatura e esteja pronto para uma operação de recebimento. Em termos gerais, a maioria das entidades não enfrentará esse problema. No entanto, dado o número de saudação de entidades no barramento de serviço no Azure, essa atenuação às vezes é necessária para um pequeno subconjunto de clientes do barramento de serviço.

### <a name="service-bus-failure-on-a-single-subsystem"></a>Falha do Barramento de Serviço em um único subsistema
Com qualquer aplicativo, circunstâncias podem fazer um componente interno do barramento de serviço toobecome inconsistente. Quando o barramento de serviço detecta isso, ele coleta dados de saudação aplicativo tooaid diagnosticar o que aconteceu. Depois de saudação os dados são coletados, o aplicativo hello é reiniciado em uma tentativa de tooreturn-estado consistente de tooa. Esse processo acontece muito rapidamente e resulta em uma entidade aparecendo toobe não está disponível para backup tooa alguns minutos, embora típico para baixo vezes é mais curtos.

Nesses casos, o aplicativo de cliente hello gera um [System. TimeoutException] [ System.TimeoutException] ou [MessagingException] [ MessagingException] exceção. Barramento de serviço contém uma atenuante para esse problema na forma de saudação de lógica de repetição automatizada de cliente. Depois de saudação período esgota e mensagem de saudação não for entregue, você pode explorar usando outros recursos, como [emparelhado namespaces][paired namespaces]. Namespaces emparelhados têm outras restrições que são abordadas neste artigo.

### <a name="failure-of-service-bus-within-an-azure-datacenter"></a>Falha do Barramento de Serviço em um datacenter do Azure
a razão mais provável saudação de uma falha em um datacenter do Azure é uma implantação de atualização com falha do barramento de serviço ou um sistema dependente. Como plataforma Olá amadureceu, probabilidade Olá desse tipo de falha é reduzida. Uma falha de datacenter pode também acontecer por razões que incluem hello seguinte:

* Falta de energia (a fonte de energia e a geração de energia ficam indisponíveis).
* Conectividade (interrupção da Internet entre o cliente e o Azure).

Em ambos os casos, um desastre natural ou humano causou o problema de saudação. toowork esse problema e certifique-se de que você ainda pode enviar mensagens, você pode usar [emparelhado namespaces] [ paired namespaces] tooenable mensagens enviada de toobe tooa segundo local enquanto Olá primeira localização torna íntegra novamente. Para saber mais, confira [Práticas recomendadas para isolar aplicativos contra interrupções e desastres do Barramento de Serviço][Best practices for insulating applications against Service Bus outages and disasters].

## <a name="paired-namespaces"></a>Namespaces emparelhados
Olá [emparelhado namespaces] [ paired namespaces] recurso dá suporte a cenários em que uma entidade de barramento de serviço ou uma implantação em um data center torna-se indisponível. Enquanto esse evento ocorra raramente, sistemas distribuídos ainda devem ser preparados toohandle piores cenários. Normalmente, esse evento acontece porque algum elemento dos quais o Barramento de Serviço depende está enfrentando um problema de curto prazo. disponibilidade de aplicativos toomaintain durante uma interrupção, a usuários de barramento de serviço podem usar dois namespaces separados, preferencialmente em data centers separados, toohost suas entidades de mensagens. restante desta seção Olá usa Olá terminologia a seguir:

* Namespace primário: Olá namespace ao qual seu aplicativo interage, para enviar e receber operações.
* Namespace secundário: Olá namespace que atua como um namespace primário toohello backup. A lógica de aplicativo não interage com esse namespace.
* Intervalo de failover: quantidade de saudação de falhas normais de tooaccept de tempo antes do aplicativo hello alterna do namespace secundário do toohello Olá namespace primário.

Namespaces emparelhados dão suporte à *disponibilidade de envio*. Envie mensagens de saudação do toosend capacidade preserva a disponibilidade. disponibilidade de envio toouse, seu aplicativo deve atender aos Olá requisitos a seguir:

1. As mensagens são recebidas apenas do namespace primário hello.
2. As mensagens enviadas tooa fila ou tópico determinado pode chegar fora de ordem.
3. As mensagens em uma sessão podem chegar fora de ordem. Essa é uma falha de funcionalidade normal das sessões. Isso significa que o aplicativo usa mensagens de grupo de toologically de sessões.
4. Estado da sessão é mantido somente no namespace primário hello.
5. fila primária Olá pode ficar online e começar a aceitar mensagens antes de fila secundária Olá apresenta todas as mensagens em fila primária hello.

Olá seções a seguir discutem Olá APIs, como Olá APIs são implementadas e código de exemplo mostra que usa o recurso de saudação. Observe que há implicações de cobranças associadas a esse recurso.

### <a name="hello-messagingfactorypairnamespaceasync-api"></a>Olá API messagingfactory. Pairnamespaceasync
inclui o recurso dos namespaces emparelhados Olá Olá [PairNamespaceAsync] [ PairNamespaceAsync] método hello [Microsoft.ServiceBus.Messaging.MessagingFactory] [ Microsoft.ServiceBus.Messaging.MessagingFactory] classe:

```csharp
public Task PairNamespaceAsync(PairedNamespaceOptions options);
```

Quando concluir a tarefa hello, Olá emparelhamento de namespace também é concluído e pronto tooact após para qualquer [MessageReceiver][MessageReceiver], [QueueClient] [ QueueClient], ou [TopicClient] [ TopicClient] criado com hello [MessagingFactory] [ MessagingFactory] instância. [Microsoft.ServiceBus.Messaging.PairedNamespaceOptions] [ Microsoft.ServiceBus.Messaging.PairedNamespaceOptions] é a classe base Olá para hello diferentes tipos de emparelhamento que estão disponíveis com um [MessagingFactory] [ MessagingFactory] objeto. Atualmente, Olá somente a classe derivada é uma chamada [SendAvailabilityPairedNamespaceOptions][SendAvailabilityPairedNamespaceOptions], que implementa os requisitos de disponibilidade de envio de saudação. [SendAvailabilityPairedNamespaceOptions][SendAvailabilityPairedNamespaceOptions] tem um conjunto de construtores que se baseiam uns nos outros. Procurando no construtor de saudação com hello a maioria dos parâmetros, você pode entender Olá comportamento de saudação outros construtores.

```csharp
public SendAvailabilityPairedNamespaceOptions(
    NamespaceManager secondaryNamespaceManager,
    MessagingFactory messagingFactory,
    int backlogQueueCount,
    TimeSpan failoverInterval,
    bool enableSyphon)
```

Esses parâmetros têm Olá significados a seguir:

* *secondaryNamespaceManager*: uma inicializado [NamespaceManager] [ NamespaceManager] instância para o namespace secundário Olá que Olá [PairNamespaceAsync] [ PairNamespaceAsync] método pode usar tooset o namespace secundário hello. Gerenciador de namespace de saudação é a lista de saudação de tooobtain usado de filas no namespace hello e toomake-se de que existam filas de lista de pendências de Olá necessário. Se essas filas não existirem, elas serão criadas. [NamespaceManager] [ NamespaceManager] requer Olá capacidade toocreate um token com hello **gerenciar** de declaração.
* *messagingFactory*: Olá [MessagingFactory] [ MessagingFactory] instância para o namespace secundário hello. Olá [MessagingFactory] [ MessagingFactory] objeto é toosend usado e, se hello [EnableSyphon] [ EnableSyphon] propriedade for definida muito**true** , receber mensagens de filas de lista de pendências de saudação.
* *backlogQueueCount*: número de saudação da lista de pendências filas toocreate. Esse valor deve ser pelo menos 1. Ao enviar a lista de pendências de toohello de mensagens, uma dessas filas é escolhida aleatoriamente. Se você definir Olá valor too1, somente uma fila nunca pode ser usada. Quando isso acontece e fila de registros acumulados hello gera erros, o cliente de Olá não é capaz de tootry uma fila de registros acumulados diferente e pode falhar toosend sua mensagem. É recomendável definir este valor toosome maior valor e padrão Olá valor too10. Você pode alterar esse tooa superior ou o valor mais baixo dependendo de quantos dados o aplicativo envia por dia. Cada fila de registros acumulados pode manter a too5 GB de mensagens.
* *failoverInterval*: Olá quantidade de tempo durante o qual você irá aceitar falhas no namespace primário Olá antes de alterar qualquer entidade única em um namespace secundário toohello. Os failovers ocorrem em entidades individuais. Entidades em um único namespace frequentemente estão em nós diferentes no Barramento de Serviço. Uma falha em uma entidade não implica falha em outra. Você pode definir esse valor muito[System.TimeSpan.Zero] [ System.TimeSpan.Zero] toofailover toohello secundário imediatamente após a falha em primeiro lugar, não transitório. Falhas que acionam o timer do failover Olá são qualquer [MessagingException] [ MessagingException] no qual Olá [IsTransient] [ IsTransient] propriedade é false, ou um [System. TimeoutException][System.TimeoutException]. Outras exceções, como [UnauthorizedAccessException] [ UnauthorizedAccessException] não causam o failover, pois elas indicam que o cliente hello está configurado incorretamente. Um [ServerBusyException] [ ServerBusyException] não causa failover porque o padrão correto Olá é toowait 10 segundos, em seguida, envia mensagem de saudação novamente.
* *enableSyphon*: indica que um emparelhamento particular deve também tirar com sifão mensagens de saudação secundário toohello back principal de namespace. Em geral, os aplicativos que enviam mensagens devem definir esse valor muito**false**; aplicativos que recebem mensagens devem definir esse valor muito**true**. motivo Olá para isso é frequentemente, há menos receptores de mensagens que remetentes de mensagens. Dependendo do número de saudação de destinatários, você pode escolher tarefas de sifão um único aplicativo instância identificador Olá toohave. Usar muitos receptores tem implicações de cobranças para cada fila de lista de pendências.

toouse Olá código, crie um primário [MessagingFactory] [ MessagingFactory] instância, um secundário [MessagingFactory] [ MessagingFactory] instância, um secundário [NamespaceManager] [ NamespaceManager] instância e um [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] instância. chamada de saudação pode ser tão simple quanto a seguir hello:

```csharp
SendAvailabilityPairedNamespaceOptions sendAvailabilityOptions = new SendAvailabilityPairedNamespaceOptions(secondaryNamespaceManager, secondary);
primary.PairNamespaceAsync(sendAvailabilityOptions).Wait();
```

Olá quando a tarefa retornada por Olá [PairNamespaceAsync] [ PairNamespaceAsync] método é concluído, tudo está configurado e pronto toouse. Antes de tarefa Olá é retornada, você pode não concluiu todo o trabalho de plano de fundo de saudação necessário para Olá emparelhamento toowork direita. Como resultado, você não comece a enviar mensagens até que a tarefa de saudação retorna. Se nenhuma falha ocorrer, como credenciais incorretas ou filas de pendências da saudação falha toocreate, essas exceções serão lançadas após a conclusão da tarefa de saudação. Depois que a tarefa Olá retorna, verifique se filas Olá foram encontradas ou criadas por meio do exame Olá [BacklogQueueCount] [ BacklogQueueCount] propriedade em seu [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] instância. Para Olá precede o código, a operação aparece da seguinte maneira:

```csharp
if (sendAvailabilityOptions.BacklogQueueCount < 1)
{
    // Handle case where no queues were created.
}
```

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas de saudação do sistema de mensagens assíncronas no barramento de serviço, leia mais detalhes sobre [emparelhado namespaces][paired namespaces].

[ServerBusyException]: /dotnet/api/microsoft.servicebus.messaging.serverbusyexception
[System.TimeoutException]: https://msdn.microsoft.com/library/system.timeoutexception.aspx
[MessagingException]: /dotnet/api/microsoft.servicebus.messaging.messagingexception
[Best practices for insulating applications against Service Bus outages and disasters]: service-bus-outages-disasters.md
[Microsoft.ServiceBus.Messaging.MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[MessageReceiver]: /dotnet/api/microsoft.servicebus.messaging.messagereceiver
[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[TopicClient]: /dotnet/api/microsoft.servicebus.messaging.topicclient
[Microsoft.ServiceBus.Messaging.PairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.pairednamespaceoptions
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[SendAvailabilityPairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions
[NamespaceManager]: /dotnet/api/microsoft.servicebus.namespacemanager
[PairNamespaceAsync]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PairNamespaceAsync_Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_
[EnableSyphon]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_EnableSyphon
[System.TimeSpan.Zero]: https://msdn.microsoft.com/library/system.timespan.zero.aspx
[IsTransient]: /dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient
[UnauthorizedAccessException]: https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx
[BacklogQueueCount]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions?redirectedfrom=MSDN#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_BacklogQueueCount
[paired namespaces]: service-bus-paired-namespaces.md
