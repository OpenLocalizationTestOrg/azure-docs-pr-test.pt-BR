---
title: "aaaOverview de saudação do ciclo de vida de serviços do Azure Service Fabric confiáveis | Microsoft Docs"
description: "Saiba mais sobre eventos de ciclo de vida diferente Olá em serviços confiáveis do Service Fabric"
services: Service-Fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: vturecek;
ms.assetid: 
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 0d75ed5ee7cda85ac9af6a02e160727277804a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-lifecycle-overview"></a>Visão geral do ciclo de vida do Reliable Services
> [!div class="op_single_selector"]
> * [C# em Windows](service-fabric-reliable-services-lifecycle.md)
> * [Java no Linux](service-fabric-reliable-services-lifecycle-java.md)
>
>

Ao pensar Olá ciclos de vida de serviços confiáveis, Noções básicas de saudação do ciclo de vida de saudação são hello mais importante. Em geral:

- Durante a inicialização
  - Serviços são construídos
  - Eles têm uma oportunidade tooconstruct e retornam zero ou mais ouvintes
  - Todos os ouvintes retornados abertos, permitindo que a comunicação com o serviço de saudação
  - RunAsync saudação do serviço método é chamado, permitindo Olá toodo de longa execução do serviço ou trabalho de plano de fundo
- Durante o desligamento
  - tooRunAsync passado token de cancelamento Olá será cancelada e ouvintes de saudação são fechadas
  - Assim que estiver concluído, próprio objeto de serviço Olá é destruído

Há detalhes sobre Olá exata de ordenação desses eventos. Em particular, a ordem de saudação de eventos pode mudar um pouco dependendo se Olá serviço confiável é sem monitoração de estado ou de monitoração de estado. Além disso, para os serviços com monitoração de estado, temos toodeal com cenário de troca primário hello. Durante essa sequência, função hello principal é transferido tooanother réplica (ou voltar a ficar) sem o desligamento do serviço hello. Por fim, temos toothink sobre condições de erro ou falha.

## <a name="stateless-service-startup"></a>Inicialização de serviço sem estado
saudação de ciclo de vida de um serviço sem monitoração de estado é bastante simples. Aqui está a ordem de saudação de eventos:

1. Olá serviço é construído
2. Em seguida, ocorrem duas coisas em paralelo:
    - `StatelessService.CreateServiceInstanceListeners()` é invocado e todos os ouvintes retornados são Abertos. `ICommunicationListener.OpenAsync()` é chamado em cada ouvinte
    - Olá do serviço `StatelessService.RunAsync()` é chamado de método
3. Se estiver presente, Olá do serviço `StatelessService.OnOpenAsync()` método é chamado. Essa não é uma substituição comum, mas está disponível.

É importante toonote que não há nenhuma ordem entre Olá chamadas toocreate e ouvintes de saudação aberto e RunAsync. ouvintes de saudação podem abrir antes RunAsync é iniciado. Da mesma forma, RunAsync poderá acabar invocado antes de ouvintes de comunicação Olá estão abertas ou até mesmo foram construídos. Se nenhuma sincronização é necessária, ela será deixada como implementador de toohello um exercício. Soluções comuns:

  - Algumas vezes os ouvintes não funcionam até que outras informações sejam criadas ou algum trabalho seja realizado. Para serviços sem estado, esse trabalho geralmente pode ser feito em outros locais, como: 
    - no construtor do serviço Olá
    - durante a saudação `CreateServiceInstanceListeners()` chamar
    - como parte da construção de saudação do ouvinte Olá próprio
  - Às vezes, hello código RunAsync não quer toostart até ouvintes Olá estão abertas. Nesse caso, coordenação adicional será necessária. Uma solução comum é alguns sinalizador em ouvintes Olá indicando quando eles forem concluídas. Este sinalizador será verificado em RunAsync antes de continuar o trabalho de tooactual.

## <a name="stateless-service-shutdown"></a>Desligamento de serviço sem estado
Ao desligar um serviço sem monitoração de estado, Olá mesmo padrão é seguido apenas na ordem inversa:

1. Em paralelo
    - Todos os ouvintes abertos são Fechados. `ICommunicationListener.CloseAsync()` é chamado em cada ouvinte.
    - o token de cancelamento Olá passado muito`RunAsync()` é cancelada. Do token de cancelamento de saudação verificando `IsCancellationRequested` propriedade retorna true e se a chamada do token Olá `ThrowIfCancellationRequested` método lança um `OperationCanceledException`.
2. Uma vez `CloseAsync()` conclusão em cada ouvinte e `RunAsync()` também completa do serviço Olá `StatelessService.OnCloseAsync()` método é chamado, se presente. É comum toooverride `StatelessService.OnCloseAsync()`.
3. Depois de `StatelessService.OnCloseAsync()` for concluído, o objeto de serviço Olá é destruído

## <a name="stateful-service-startup"></a>Inicialização de serviço com estado
Serviços com monitoração de estado tem serviços um toostateless padrão semelhantes, com poucas alterações. Ao iniciar o serviço com monitoração de estado, a ordem de saudação de eventos é o seguinte:

1. Olá serviço é construído
2. `StatefulServiceBase.OnOpenAsync()` é chamado. Isso é substituído uncommonly no serviço de saudação.
3. Olá acontecem estas coisas em paralelo
    - `StatefulServiceBase.CreateServiceReplicaListeners()` é invocado 
      - Se o serviço Olá é primária todos os ouvintes retornados são abertos. `ICommunicationListener.OpenAsync()` é chamado em cada ouvinte.
      - Se o serviço de saudação um secundário, somente esses ouvintes marcado como `ListenOnSecondary = true` estão abertas. Ter ouvintes que estão abertos em Secundários é menos comum.
    - Olá se Olá serviço atualmente é um serviço de saudação primário, `StatefulServiceBase.RunAsync()` é chamado de método
4. Depois que todos os Olá do ouvinte de réplica `OpenAsync()` concluir chamadas e `RunAsync()` é chamado, `StatefulServiceBase.OnChangeRoleAsync()` é chamado. Isso é substituído uncommonly no serviço de saudação.

Serviços de toostateless da mesma forma, não há nenhum coordenação entre ordem Olá no qual Olá ouvintes são criados e abertos e quando RunAsync é chamado. Se você precisar de coordenação, soluções Olá são muito Olá mesmo. Há um caso adicional: diga Olá chamadas que chegam ao ouvintes de comunicação Olá exigem informações mantidas dentro de alguns [coleções confiável](service-fabric-reliable-services-reliable-collections.md). Porque os ouvintes de comunicação Olá foi aberto antes de coleções de saudação confiável serão de leitura ou gravável e antes de RunAsync pode iniciar, alguns coordenação adicional é necessária. solução mais simples e mais comum de saudação é para tooreturn de ouvintes de comunicação Olá algum código de erro que Olá Olá a solicitação do cliente usa tooknow tooretry.

## <a name="stateful-service-shutdown"></a>Desligamento de serviço com estado
Da mesma forma tooStateless serviços, eventos de ciclo de vida de saudação durante o desligamento são Olá mesmo como durante a inicialização, mas revertidas. Quando um serviço com monitoração de estado está sendo desligado, hello seguintes eventos ocorrem:

1. Em paralelo
    - Todos os ouvintes abertos são Fechados. `ICommunicationListener.CloseAsync()` é chamado em cada ouvinte.
    - o token de cancelamento Olá passado muito`RunAsync()` é cancelada. Do token de cancelamento de saudação verificando `IsCancellationRequested` propriedade retorna true e se a chamada do token Olá `ThrowIfCancellationRequested` método lança um `OperationCanceledException`.
2. Uma vez `CloseAsync()` conclusão em cada ouvinte e `RunAsync()` também completa do serviço Olá `StatefulServiceBase.OnChangeRoleAsync()` é chamado. (Isso é uncommonly substituído no serviço hello.)
    - Aguardando RunAsync toocomplete só é necessária se esta réplica de serviço primária.
3. Uma vez Olá `StatefulServiceBase.OnChangeRoleAsync()` método é concluído, hello `StatefulServiceBase.OnCloseAsync()` método é chamado. Essa não é uma substituição comum, mas está disponível.
3. Depois de `StatefulServiceBase.OnCloseAsync()` for concluído, o objeto de serviço Olá é destruído.

## <a name="stateful-service-primary-swaps"></a>Trocas de primária do serviço com estado
Durante a execução de um serviço com monitoração de estado, só hello réplicas primárias do que os serviços com monitoração de estado tem seus ouvintes de comunicação abertos e seu método RunAsync chamado. Secundárias são construídas, mas não recebem chamadas. Enquanto um serviço com monitoração de estado é executado no entanto, qual réplica está Olá primário pode alterar. O que isso significa em termos de eventos de ciclo de vida de saudação pode ver uma réplica? Olá comportamento Olá réplica com monitoração de estado vê depende se ela é réplica Olá sendo rebaixada ou promovida durante a troca de saudação.

### <a name="for-hello-primary-being-demoted"></a>Para Olá primário que está sendo rebaixado
Service Fabric precisa este toostop réplica processamento de mensagens e feche qualquer trabalho em segundo plano que está fazendo. Como resultado, essa etapa parece semelhante toowhen Olá serviço está sendo desligado. Uma diferença é que hello serviço não é destruído ou fechado, pois ele permanece como um secundário. é chamada de saudação APIs a seguir:

1. Em paralelo
    - Todos os ouvintes abertos são Fechados. `ICommunicationListener.CloseAsync()` é chamado em cada ouvinte.
    - o token de cancelamento Olá passado muito`RunAsync()` é cancelada. Do token de cancelamento de saudação verificando `IsCancellationRequested` propriedade retorna true e se a chamada do token Olá `ThrowIfCancellationRequested` método lança um `OperationCanceledException`.
2. Uma vez `CloseAsync()` conclusão em cada ouvinte e `RunAsync()` também completa do serviço Olá `StatefulServiceBase.OnChangeRoleAsync()` é chamado. Isso é substituído uncommonly no serviço de saudação.

### <a name="for-hello-secondary-being-promoted"></a>Para Olá secundária que está sendo promovido
Da mesma forma, do Service Fabric precisa este toostart réplica ouvindo mensagens percurso hello e iniciar as tarefas em segundo plano são importantes. Como resultado, essa parece processo serviço de saudação toowhen semelhante é criado, exceto que a réplica Olá em si já existe. é chamada de saudação APIs a seguir:

1. Em paralelo
    - `StatefulServiceBase.CreateServiceReplicaListeners()` é invocado e todos os ouvintes retornados são Abertos. `ICommunicationListener.OpenAsync()` é chamado em cada ouvinte.
    - Olá do serviço `StatefulServiceBase.RunAsync()` é chamado de método
2. Depois que todos os Olá do ouvinte de réplica `OpenAsync()` concluir chamadas e `RunAsync()` foi chamado, `StatefulServiceBase.OnChangeRoleAsync()` é chamado. Isso é substituído uncommonly no serviço de saudação.

### <a name="common-issues-during-stateful-service-shutdown-and-primary-demotion"></a>Problemas comuns durante o desligamento do serviço com estado e rebaixamento do primário
Alterações do Service Fabric Olá primário de um serviço com monitoração de estado para uma variedade de razões. Hello mais comuns são [cluster rebalanceamento](service-fabric-cluster-resource-manager-balancing.md) e [atualização de aplicativo](service-fabric-application-upgrade.md). Durante essas operações (bem como durante o desligamento normal do serviço, como você veria se o serviço de saudação foi excluído), é importante que Olá Olá de relação serviço `CancellationToken`. Os serviços que não tratarem o cancelamento corretamente enfrentarão vários problemas. Em particular, essas operações será lentas pois Service Fabric aguarda Olá serviços toostop normalmente. Isso pode levar toofailed atualizações esse tempo limite e revertê-lo, por fim. Token de cancelamento falha toohonor Olá também pode causar clusters desequilibrados porque nós obtém ativos, mas não podem ser balanceados serviços Olá desde que demora muito toomove-los em outro lugar. 

Como os serviços de saudação com monitoração de estado, também é provável que estão usando Olá [coleções confiável](service-fabric-reliable-services-reliable-collections.md). Na malha do serviço, quando primário é rebaixado, uma saudação coisas mais importantes que acontece é que o estado do acesso de gravação toohello subjacente é revogado. Isso leva tooa segundo conjunto de problemas que podem afetar o ciclo de vida de serviço hello. coleções de saudação retorno exceções com base no tempo de saudação e se a réplica hello está sendo movida ou desligar. Essas exceções devem ser tratadas corretamente. As exceções geradas pelo Service Fabric se classificam nas categorias permanentes [(`FabricException`)](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabricexception?view=azure-dotnet) e transitórias [(`FabricTransientException`)](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabrictransientexception?view=azure-dotnet). Exceções permanentes devem ser registradas e lançadas ao exceções transitórias Olá podem ser repetidas com base em alguma lógica de repetição.

Tratamento de exceções de saudação que vêm do uso de saudação `ReliableCollections` em conjunto com eventos de ciclo de vida do serviço é uma parte importante de teste e validação de um serviço confiável. Olá recomendação é sempre toorun seu serviço sob carga durante a execução de atualizações e [caos teste](service-fabric-controlled-chaos.md) antes de implantar nunca tooproduction. Essas etapas básicas ajudam a garantir que o serviço seja implementado corretamente, além de tratar os eventos do ciclo de vida corretamente.


## <a name="notes-on-service-lifecycle"></a>Observações sobre o ciclo de vida do serviço
  - Ambos os Olá `RunAsync()` método e hello `CreateServiceReplicaListeners/CreateServiceInstanceListeners` chamadas são opcionais. Um serviço pode ter um deles, ambos ou nenhum. Por exemplo, se o serviço de saudação faz seu trabalho em resposta toouser chamadas, não é necessário para que ele tooimplement `RunAsync()`. É necessário apenas os ouvintes de comunicação hello e seu código associado. Da mesma forma, criando e retornando ouvintes de comunicação é opcional, pois o serviço Olá pode ter apenas em segundo plano toodo de trabalho e então só precisa tooimplement`RunAsync()`
  - Ele é válido para um serviço toocomplete `RunAsync()` com êxito e retorno dele. A conclusão não é uma condição de falha. Concluindo `RunAsync()` indica que o trabalho em segundo plano de saudação do serviço de saudação foi concluída. Para serviços confiáveis com monitoração de estado, `RunAsync()` é chamado novamente se a réplica Olá foram rebaixada de tooSecondary primária e, em seguida, promovida tooPrimary voltar.
  - Se um serviço sair de `RunAsync()` lançando uma exceção inesperada, isso constituirá uma falha. o objeto de serviço Olá é desligado e relatou um erro de integridade.
  - Embora não haja nenhum limite de tempo no retorno de um desses métodos, você perde imediatamente Olá capacidade toowrite tooReliable coleções e, portanto, não pode concluir qualquer trabalho real. É recomendável que você retorne mais rápido possível após o recebimento da solicitação de cancelamento de saudação. Se o serviço não responder chamadas de API do toothese em um período razoável que do Service Fabric pode forçar cancelar seu serviço. Geralmente isso ocorre apenas durante atualizações de aplicativo ou quando um serviço está sendo excluído. Esse tempo limite é de 15 minutos por padrão.
  - Falhas em Olá `OnCloseAsync()` resultados de caminho em `OnAbort()` sendo chamada que é uma oportunidade de melhor esforço de última chance de saudação serviço tooclean backup e liberar todos os recursos que eles já solicitou.

## <a name="next-steps"></a>Próximas etapas
- [Serviços de tooReliable de Introdução](service-fabric-reliable-services-introduction.md)
- [Início Rápido dos Serviços Confiáveis](service-fabric-reliable-services-quick-start.md)
- [Uso avançado de Reliable Services](service-fabric-reliable-services-advanced-usage.md)
