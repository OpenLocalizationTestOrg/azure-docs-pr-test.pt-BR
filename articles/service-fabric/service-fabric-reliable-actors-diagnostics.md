---
title: "aaaActors diagnóstico e monitoramento | Microsoft Docs"
description: "Este artigo descreve os diagnósticos de hello e recursos no tempo de execução de serviço malha Reliable Actors de saudação, incluindo eventos de saudação e contadores de desempenho emitidos por ela de monitoramento de desempenho."
services: service-fabric
documentationcenter: .net
author: abhishekram
manager: timlt
editor: vturecek
ms.assetid: 1c229923-670a-4634-ad59-468ff781ad18
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: abhisram
ms.openlocfilehash: 5b266d67875722feef5c5be8861bda6d8132a7d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-performance-monitoring-for-reliable-actors"></a>Diagnóstico e monitoramento de desempenho para Reliable Actors
tempo de execução do Hello Reliable Actors emite [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) eventos e [contadores de desempenho](https://msdn.microsoft.com/library/system.diagnostics.performancecounter.aspx). Esses fornecem ideias sobre como o tempo de execução hello está funcionando e ajudá-lo com solução de problemas e monitoramento do desempenho.

## <a name="eventsource-events"></a>Eventos EventSource
nome do provedor de EventSource Olá Olá Reliable Actors Runtime é "Microsoft-ServiceFabric-atores". Eventos dessa origem de evento são exibidos em Olá [eventos de diagnóstico](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md#view-service-fabric-system-events-in-visual-studio) janela quando o aplicativo de ator hello está sendo [depurado no Visual Studio](service-fabric-debugging-your-application.md).

São exemplos de ferramentas e tecnologias que ajudam a coletar e/ou visualizando eventos EventSource [PerfView](http://www.microsoft.com/download/details.aspx?id=28567), [diagnóstico do Azure](../cloud-services/cloud-services-dotnet-diagnostics.md), [log semântica](https://msdn.microsoft.com/library/dn774980.aspx)e hello [ Biblioteca do Microsoft TraceEvent](http://www.nuget.org/packages/Microsoft.Diagnostics.Tracing.TraceEvent).

### <a name="keywords"></a>Palavras-chave
Todos os eventos que pertencem a toohello confiável EventSource de atores são associados com uma ou mais palavras-chave. Isso permite a filtragem dos eventos que são coletados. Olá bits de palavra-chave a seguir é definida.

| Bit | Descrição |
| --- | --- |
| 0x1 |Conjunto de eventos importantes que resumem a operação de saudação do tempo de execução de malha atores hello. |
| 0x2 |Conjunto de eventos que descrevem as chamadas de método do ator. Para obter mais informações, consulte Olá [tópico introdutório em atores](service-fabric-reliable-actors-introduction.md). |
| 0x4 |Conjunto de eventos relacionados tooactor estado. Para obter mais informações, consulte o tópico de saudação sobre [gerenciamento de estado de ator](service-fabric-reliable-actors-state-management.md). |
| 0x8 |Conjunto de simultaneidade eventos com base em tooturn relacionados na ator hello. Para obter mais informações, consulte o tópico de saudação sobre [simultaneidade](service-fabric-reliable-actors-introduction.md#concurrency). |

## <a name="performance-counters"></a>Contadores de desempenho
tempo de execução do Hello Reliable Actors define Olá categorias de contador de desempenho a seguir.

| Categoria | Descrição |
| --- | --- |
| Ator da Malha do Serviço |Contadores específicos tooAzure atores de malha do serviço, por exemplo, tempo toosave estado de ator |
| Método de ator da Malha do Serviço |Contadores específicos toomethods implementado por atores de malha do serviço, por exemplo, quantas vezes um método de ator é invocado |

Cada Olá acima categorias tem um ou mais contadores.

Olá [o Monitor de desempenho do Windows](https://technet.microsoft.com/library/cc749249.aspx) aplicativo que está disponível por padrão no sistema de operacional do Windows hello pode ser usados dados de contador de desempenho de toocollect e modo de exibição. [Diagnóstico do Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) é outra opção para coletar dados do contador de desempenho e carregá-lo tooAzure tabelas.

### <a name="performance-counter-instance-names"></a>Nomes da instância do contador de desempenho
Um cluster que tem um grande número de serviços de ator ou partições de serviço de ator terá um grande número de instâncias do contador de desempenho de ator. Olá nomes de instância do contador de desempenho podem ajudar a identificar Olá específico [partição](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors) e método de ator (se aplicável) essa instância do contador de desempenho hello está associada.

#### <a name="service-fabric-actor-category"></a>Categoria de ator do Service Fabric
Categoria de saudação `Service Fabric Actor`, nomes de instância de contador Olá estão em Olá formato a seguir:

`ServiceFabricPartitionID_ActorsRuntimeInternalID`

*ServiceFabricPartitionID* é a representação de cadeia de caracteres de saudação de saudação ID de partição de malha do serviço que Olá a instância do contador de desempenho está associado. Olá ID de partição é um GUID e sua representação de cadeia de caracteres é gerada por meio de saudação [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) método com especificador de formato "D".

*ActorRuntimeInternalID* é a representação de cadeia de caracteres de saudação de um inteiro de 64 bits que é gerado pelo tempo de execução do hello atores de malha para uso interno. Isso está incluído na instância do contador de desempenho Olá nome tooensure sua exclusividade e evitar conflitos com outros nomes de instância do contador de desempenho. Os usuários não devem tentar toointerpret esta parte do nome de instância do contador de desempenho de saudação.

Olá, a seguir é um exemplo de um nome de instância do contador para um contador que pertence a toohello `Service Fabric Actor` categoria:

`2740af29-78aa-44bc-a20b-7e60fb783264_635650083799324046`

No exemplo acima, a saudação `2740af29-78aa-44bc-a20b-7e60fb783264` é a representação de cadeia de caracteres de saudação do ID de partição do Service Fabric Olá, e `635650083799324046` é usar o hello ID de 64 bits que é gerado para interno do tempo de execução de saudação.

#### <a name="service-fabric-actor-method-category"></a>Categoria do método de ator do Service Fabric
Categoria de saudação `Service Fabric Actor Method`, nomes de instância de contador Olá estão em Olá formato a seguir:

`MethodName_ActorsRuntimeMethodId_ServiceFabricPartitionID_ActorsRuntimeInternalID`

*MethodName* é o nome de saudação do método de ator Olá Olá a instância do contador de desempenho está associado. formato de saudação do nome do método hello é determinado com base em alguma lógica no tempo de execução de atores de malha de saudação que equilibra a legibilidade de saudação do nome de saudação com restrições no tamanho máximo de saudação de nomes de instância do contador de desempenho de saudação no Windows.

*ActorsRuntimeMethodId* é a representação de cadeia de caracteres de saudação de um inteiro de 32 bits que é gerado pelo tempo de execução do hello atores de malha para uso interno. Isso está incluído na instância do contador de desempenho Olá nome tooensure sua exclusividade e evitar conflitos com outros nomes de instância do contador de desempenho. Os usuários não devem tentar toointerpret esta parte do nome de instância do contador de desempenho de saudação.

*ServiceFabricPartitionID* é a representação de cadeia de caracteres de saudação de saudação ID de partição de malha do serviço que Olá a instância do contador de desempenho está associado. Olá ID de partição é um GUID e sua representação de cadeia de caracteres é gerada por meio de saudação [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) método com especificador de formato "D".

*ActorRuntimeInternalID* é a representação de cadeia de caracteres de saudação de um inteiro de 64 bits que é gerado pelo tempo de execução do hello atores de malha para uso interno. Isso está incluído na instância do contador de desempenho Olá nome tooensure sua exclusividade e evitar conflitos com outros nomes de instância do contador de desempenho. Os usuários não devem tentar toointerpret esta parte do nome de instância do contador de desempenho de saudação.

Olá, a seguir é um exemplo de um nome de instância do contador para um contador que pertence a toohello `Service Fabric Actor Method` categoria:

`ivoicemailboxactor.leavemessageasync_2_89383d32-e57e-4a9b-a6ad-57c6792aa521_635650083804480486`

No exemplo acima, a saudação `ivoicemailboxactor.leavemessageasync` é o nome do método hello, `2` é hello usar a ID de 32 bits para interno do tempo de execução de saudação, `89383d32-e57e-4a9b-a6ad-57c6792aa521` é a representação de cadeia de caracteres de saudação do ID de partição do Service Fabric Olá, e `635650083804480486` é Olá ID de 64 bits gerado para uso interno de saudação do runtime.

## <a name="list-of-events-and-performance-counters"></a>Lista de eventos e contadores de desempenho
### <a name="actor-method-events-and-performance-counters"></a>Eventos e contadores de desempeno do método de ator
tempo de execução confiável atores Hello emite Olá eventos relacionados muito a seguir[métodos de ator](service-fabric-reliable-actors-introduction.md).

| Nome do evento | ID do evento | Nível | Palavra-chave | Descrição |
| --- | --- | --- | --- | --- |
| ActorMethodStart |7 |Detalhado |0x2 |Tempo de execução de atores é sobre tooinvoke um método de ator. |
| ActorMethodStop |8 |Detalhado |0x2 |Um método de ator finalizou a execução. Ou seja, o método de ator do tempo de execução Olá chamada assíncrona toohello retornou e concluiu a tarefa Olá retornada pelo método de ator hello. |
| ActorMethodThrewException |9 |Aviso |0x3 |Uma exceção foi lançada durante a execução de um método de ator, Olá durante o método de ator do tempo de execução Olá chamada assíncrona toohello ou durante a execução de saudação da tarefa Olá retornado pelo método de ator do hello. Esse evento indica que algum tipo de falha no código de ator Olá que precisa de investigação. |

tempo de execução do Hello Reliable Actors publica Olá após a execução de toohello relacionados de contadores de desempenho dos métodos de ator.

| Nome da categoria | Nome do contador | Descrição |
| --- | --- | --- |
| Método de ator da Malha do Serviço |Invocação/s |Número de vezes que o método de saudação do serviço de ator é invocado por segundo |
| Método de ator da Malha do Serviço |Média de milissegundos por invocação |Método de serviço de ator do tempo gasto tooexecute hello em milissegundos |
| Método de ator da Malha do Serviço |Exceções lançadas/s |Número de vezes que Olá o método de serviço de ator lançou uma exceção por segundo |

### <a name="concurrency-events-and-performance-counters"></a>Contadores de desempenho e eventos simultâneos
tempo de execução confiável atores Hello emite Olá eventos relacionados muito a seguir[simultaneidade](service-fabric-reliable-actors-introduction.md#concurrency).

| Nome do evento | ID do evento | Nível | Palavra-chave | Descrição |
| --- | --- | --- | --- | --- |
| ActorMethodCallsWaitingForLock |12 |Detalhado |0x8 |Esse evento será gravado no início de saudação de cada vez novo em um ator. Contém o número de saudação do pendente chamadas do ator que estão esperando tooacquire saudação do bloqueio por ator que impõe a simultaneidade baseada em Ativar. |

tempo de execução do Hello Reliable Actors publica Olá tooconcurrency relacionados de contadores de desempenho a seguir.

| Nome da categoria | Nome do contador | Descrição |
| --- | --- | --- |
| Ator da Malha do Serviço |nº de chamadas do ator aguardando o bloqueio |Número de pendentes aguardando tooacquire saudação do bloqueio por ator que impõe a simultaneidade baseada em vez de chamadas de ator |
| Ator da Malha do Serviço |Média de milissegundos por espera de bloqueio |Tempo tooacquire feito (em milissegundos) saudação do bloqueio por ator que impõe a simultaneidade baseada em Ativar |
| Ator da Malha do Serviço |Média de milissegundos de manutenção de bloqueio do ator |Tempo (em milissegundos) para o qual Olá bloqueio por ator é mantido |

### <a name="actor-state-management-events-and-performance-counters"></a>Contadores de desempenho e eventos do gerenciamento de estado do ator
tempo de execução confiável atores Hello emite Olá eventos relacionados muito a seguir[gerenciamento de estado de ator](service-fabric-reliable-actors-state-management.md).

| Nome do evento | ID do evento | Nível | Palavra-chave | Descrição |
| --- | --- | --- | --- | --- |
| ActorSaveStateStart |10 |Detalhado |0x4 |Tempo de execução de atores é sobre o estado de ator toosave hello. |
| ActorSaveStateStop |11 |Detalhado |0x4 |Tempo de execução de atores terminou de salvar o estado de ator hello. |

tempo de execução do Hello Reliable Actors publica Olá gerenciamento de estado de tooactor relacionados de contadores de desempenho a seguir.

| Nome da categoria | Nome do contador | Descrição |
| --- | --- | --- |
| Ator da Malha do Serviço |Milissegundos em média por operação de salvamento do estado |Tempo gasto toosave estado de ator em milissegundos |
| Ator da Malha do Serviço |Média de milissegundos por operação de carregar estado |Tempo gasto estado de ator tooload em milissegundos |

### <a name="events-related-tooactor-replicas"></a>Eventos relacionados tooactor réplicas
tempo de execução confiável atores Hello emite Olá eventos relacionados muito a seguir[réplicas ator](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors).

| Nome do evento | ID do evento | Nível | Palavra-chave | Descrição |
| --- | --- | --- | --- | --- |
| ReplicaChangeRoleToPrimary |1 |Informativo |0x1 |Réplica de ator alterado tooPrimary de função. Isso implica que atores Olá para essa partição serão criados dentro desta réplica. |
| ReplicaChangeRoleFromPrimary |2 |Informativo |0x1 |Réplica de ator alterado função toonon primário. Isso implica que os atores Olá para essa partição não serão criados dentro desta réplica. Nenhuma nova solicitação será entregue tooactors já criado dentro desta réplica. atores Hello serão destruídos após todas as solicitações em andamento. |

### <a name="actor-activation-and-deactivation-events-and-performance-counters"></a>Eventos de ativação e desativação do ator e contadores de desempenho
tempo de execução confiável atores Hello emite Olá eventos relacionados muito a seguir[ator ativação e desativação](service-fabric-reliable-actors-lifecycle.md).

| Nome do evento | ID do evento | Nível | Palavra-chave | Descrição |
| --- | --- | --- | --- | --- |
| ActorActivated |5 |Informativo |0x1 |Um ator foi ativado. |
| ActorDeactivated |6 |Informativo |0x1 |Um ator foi desativado. |

tempo de execução do Hello Reliable Actors publica Olá contadores de desempenho a seguir relacionadas tooactor ativação e desativação.

| Nome da categoria | Nome do contador | Descrição |
| --- | --- | --- |
| Ator da Malha do Serviço |Média de milissegundos para OnActivateAsync |Tempo tooexecute o método OnActivateAsync em milissegundos |

### <a name="actor-request-processing-performance-counters"></a>Solicitação do ator processando contadores de desempenho
Quando um cliente invoca um método por meio de um objeto de proxy de ator, resulta em uma mensagem de solicitação a ser enviada através do serviço de ator Olá rede toohello. serviço de saudação processa a mensagem de solicitação de saudação e envia uma resposta toohello back cliente. tempo de execução do Hello Reliable Actors publica Olá processamento de solicitação de tooactor relacionados de contadores de desempenho a seguir.

| Nome da categoria | Nome do contador | Descrição |
| --- | --- | --- |
| Ator da Malha do Serviço |nº de solicitações pendentes |Número de solicitações sendo processadas no serviço Olá |
| Ator da Malha do Serviço |Média de milissegundos por solicitação |Tempo (em milissegundos) Olá serviço tooprocess uma solicitação |
| Ator da Malha do Serviço |Média de milissegundos para desserialização de solicitação |Tempo toodeserialize feito (em milissegundos) ator mensagem de solicitação quando ela é recebida no serviço Olá |
| Ator da Malha do Serviço |Média de milissegundos para serialização de resposta |Mensagem de resposta de ator tempo tooserialize feito (em milissegundos) Olá no serviço Olá antes do envio toohello cliente de resposta de saudação |

## <a name="next-steps"></a>Próximas etapas
* [Como Reliable Actors usar plataforma do Service Fabric Olá](service-fabric-reliable-actors-platform.md)
* [Documentação de referência da API do Ator](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [Exemplo de código](https://github.com/Azure/servicefabric-samples)
* [Provedores de EventSource no PerfView](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
