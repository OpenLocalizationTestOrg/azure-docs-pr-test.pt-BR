---
title: "aaaOverview de saudação do ciclo de vida de serviços do Azure Service Fabric confiáveis | Microsoft Docs"
description: "Saiba mais sobre eventos de ciclo de vida diferente Olá em serviços confiáveis do Service Fabric"
services: Service-Fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: 
ms.service: Service-Fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: pakunapa;
ms.openlocfilehash: 6d48c217d12bc5248c2da57b544aac747cecd872
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

* Durante a inicialização
  * Serviços são construídos
  * Eles têm uma oportunidade tooconstruct e retornam zero ou mais ouvintes
  * Todos os ouvintes retornados abertos, permitindo que a comunicação com o serviço de saudação
  * método de runAsync de saudação do serviço é chamado, permitindo Olá toodo do serviço de longa execução ou trabalho de plano de fundo
* Durante o desligamento
  * toorunAsync passado token de cancelamento Olá será cancelada e ouvintes de saudação são fechadas
  * Assim que estiver concluído, próprio objeto de serviço Olá é destruído

Há detalhes sobre Olá exata de ordenação desses eventos. Em particular, a ordem de saudação de eventos pode mudar um pouco dependendo se Olá serviço confiável é sem monitoração de estado ou de monitoração de estado. Além disso, para os serviços com monitoração de estado, temos toodeal com cenário de troca primário hello. Durante essa sequência, função hello principal é transferido tooanother réplica (ou voltar a ficar) sem o desligamento do serviço hello. Por fim, temos toothink sobre condições de erro ou falha.

## <a name="stateless-service-startup"></a>Inicialização de serviço sem estado
saudação de ciclo de vida de um serviço sem monitoração de estado é bastante simples. Aqui está a ordem de saudação de eventos:

1. Olá serviço é construído
2. Em seguida, ocorrem duas coisas em paralelo:
    - `StatelessService.createServiceInstanceListeners()` é invocado e todos os ouvintes retornados serão Abertos (`CommunicationListener.openAsync()` é chamado em cada ouvinte)
    - Olá runAsync método serviço (`StatelessService.runAsync()`) é chamado
3. Se estiver presente, o método de onOpenAsync hello do serviço é chamado (especificamente, `StatelessService.onOpenAsync()` é chamado. Esta é uma substituição incomum, mas está disponível).

É importante toonote que não há nenhuma ordem entre Olá chamadas toocreate e ouvintes de saudação aberto e runAsync. ouvintes de saudação podem abrir antes runAsync é iniciado. Da mesma forma, runAsync poderá acabar invocado antes de ouvintes de comunicação Olá estão abertas ou até mesmo foram construídos. Se nenhuma sincronização é necessária, ela será deixada como implementador de toohello um exercício. Soluções comuns:

* Algumas vezes os ouvintes não funcionam até que outras informações sejam criadas ou algum trabalho seja realizado. Para serviços sem monitoração de estado de trabalho geralmente pode ser feito no construtor do serviço hello, durante a saudação `createServiceInstanceListeners()` chamar, ou como parte da construção de saudação do ouvinte de saudação em si.
* Às vezes, hello código runAsync não quer toostart até ouvintes Olá estão abertas. Nesse caso, coordenação adicional será necessária. Uma solução comum é alguns sinalizador em ouvintes Olá indicando quando eles tem concluído, que é verificado no runAsync antes de continuar o trabalho de tooactual.

## <a name="stateless-service-shutdown"></a>Desligamento de serviço sem estado
Ao desligar um serviço sem monitoração de estado, Olá mesmo padrão é seguido apenas na ordem inversa:

1. Em paralelo
    - Todos os ouvintes abertos são Fechados (`CommunicationListener.closeAsync()` é chamado em cada ouvinte)
    - token de cancelamento Olá passado muito`runAsync()` foi cancelada (verificação de token de cancelamento a saudação `isCancelled` propriedade retorna true e se a chamada do token Olá `throwIfCancellationRequested` método lança um `CancellationException`)
2. Uma vez `closeAsync()` conclusão em cada ouvinte e `runAsync()` também completa do serviço Olá `StatelessService.onCloseAsync()` método é chamado, se estiver presente (novamente essa é uma substituição incomuns).
3. Depois de `StatelessService.onCloseAsync()` for concluído, o objeto de serviço Olá é destruído

## <a name="notes-on-service-lifecycle"></a>Observações sobre o ciclo de vida do serviço
* Ambos os Olá `runAsync()` método e hello `createServiceInstanceListeners` chamadas são opcionais. Um serviço pode ter um deles, ambos ou nenhum. Por exemplo, se o serviço de saudação faz seu trabalho em resposta toouser chamadas, não é necessário para que ele tooimplement `runAsync()`. É necessário apenas os ouvintes de comunicação hello e seu código associado. Da mesma forma, criando e retornando ouvintes de comunicação é opcional, pois o serviço Olá pode ter apenas em segundo plano toodo de trabalho e então só precisa tooimplement`runAsync()`
* Ele é válido para um serviço toocomplete `runAsync()` com êxito e retorno dele. Isso não é considerado uma condição de falha e pode representar o trabalho de plano de fundo Olá Olá serviço concluir. Para serviços confiáveis com monitoração de estado `runAsync()` será chamado novamente se o serviço Olá foram rebaixado do primário e, em seguida, promovida tooprimary voltar.
* Se um serviço sai do `runAsync()` lançando uma exceção inesperada, esta é uma falha e o objeto de serviço Olá é desligado e relatou um erro de integridade.
* Embora não haja nenhum limite de tempo no retorno de um desses métodos, você perde imediatamente Olá capacidade toowrite e, portanto, não pode concluir qualquer trabalho real. É recomendável que você retorne mais rápido possível após o recebimento da solicitação de cancelamento de saudação. Se o serviço não responder chamadas de API do toothese em um período razoável que do Service Fabric pode forçar cancelar seu serviço. Geralmente isso ocorre apenas durante atualizações de aplicativo ou quando um serviço está sendo excluído. Esse tempo limite é de 15 minutos por padrão.
* Falhas em Olá `onCloseAsync()` resultados de caminho em `onAbort()` sendo chamada que é uma oportunidade de melhor esforço de última chance de saudação serviço tooclean backup e liberar todos os recursos que eles já solicitou.

> [!NOTE]
> Ainda não há suporte para Reliable Services com monitoração de estado em java.
>
>

## <a name="next-steps"></a>Próximas etapas
* [Serviços de tooReliable de Introdução](service-fabric-reliable-services-introduction.md)
* [Início Rápido dos Serviços Confiáveis](service-fabric-reliable-services-quick-start.md)
* [Uso avançado de Reliable Services](service-fabric-reliable-services-advanced-usage.md)
