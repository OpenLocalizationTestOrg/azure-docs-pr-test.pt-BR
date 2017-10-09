---
title: "aaaStateful diagnóstico serviços confiáveis | Microsoft Docs"
description: "Funcionalidade de diagnóstico para Reliable Services com estado"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: ae0e8f99-69ab-4d45-896d-1fa80ed45659
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 6200800b858957c06039d9af062633b12a446318
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostic-functionality-for-stateful-reliable-services"></a>Funcionalidade de diagnóstico para Reliable Services com estado
Olá com monitoração de estado confiável dos serviços StatefulServiceBase classe emite [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) eventos que podem ser usado toodebug Olá serviço, forneça informações sobre como Olá runtime está funcionando e ajudar a solucionar problemas.

## <a name="eventsource-events"></a>Eventos EventSource
Olá EventSource nome hello classe StatefulServiceBase de serviços confiáveis com monitoração de estado é "Microsoft-ServiceFabric-Services". Eventos dessa origem de evento são exibidos no [eventos de diagnóstico](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md#view-service-fabric-system-events-in-visual-studio) janela quando o serviço hello está sendo [depurado no Visual Studio](service-fabric-debugging-your-application.md).

Exemplos de ferramentas e tecnologias que ajudam a coletar e/ou visualizar eventos EventSource são [PerfView](http://www.microsoft.com/download/details.aspx?id=28567), [Microsoft Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) e [Microsoft TraceEvent Library](http://www.nuget.org/packages/Microsoft.Diagnostics.Tracing.TraceEvent).

## <a name="events"></a>Eventos
| Nome do evento | ID do evento | Nível | Descrição do evento |
| --- | --- | --- | --- |
| StatefulRunAsyncInvocation |1 |Informativo |Emitido quando a tarefa RunAsync do serviço é iniciada |
| StatefulRunAsyncCancellation |2 |Informativo |Emitido quando a tarefa RunAsync do serviço é cancelada |
| StatefulRunAsyncCompletion |3 |Informativo |Emitido quando a tarefa RunAsync do serviço é concluída |
| StatefulRunAsyncSlowCancellation |4 |Aviso |Emitido quando a tarefa de serviço RunAsync leva muito toocomplete cancelamento |
| StatefulRunAsyncFailure |5 |Erro |Emitido quando a tarefa RunAsync do serviço lança uma exceção |

## <a name="interpret-events"></a>Interpretar eventos
Os eventos StatefulRunAsyncInvocation, StatefulRunAsyncCompletion e StatefulRunAsyncCancellation são ciclo de vida de toohello útil do serviço gravador toounderstand Olá de um serviço –, bem como intervalo hello quando um serviço é iniciado, cancelado ou concluído . Isso pode ser útil ao depurar problemas de serviço ou o ciclo de vida do serviço Noções básicas sobre hello.

Gravadores de serviço devem prestar atenção tooStatefulRunAsyncSlowCancellation e StatefulRunAsyncFailure eventos porque elas indicam problemas com o serviço de saudação.

StatefulRunAsyncFailure é emitido sempre que a tarefa de RunAsync() Olá serviço gera uma exceção. Normalmente, uma exceção lançada indica um erro ou um erro no serviço de saudação. Além disso, exceção Olá faz com que Olá toofail de serviço, é movido tooa outro nó. Isso pode ser uma operação dispendiosa e pode atrasar as solicitações de entrada enquanto o serviço de saudação é movido. Gravadores de serviço devem determinar a causa Olá da exceção de saudação e, se possível, resolvê-lo.

StatefulRunAsyncSlowCancellation é emitido sempre que uma solicitação de cancelamento de tarefa de RunAsync Olá demora mais do que quatro segundos. Quando um serviço leva o cancelamento toocomplete muito longo, ele afeta a capacidade Olá Olá serviço toobe rapidamente reiniciada em outro nó. Isso pode afetar Olá a disponibilidade geral do serviço de saudação.

## <a name="next-steps"></a>Próximas etapas
* [Provedores de EventSource no PerfView](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
