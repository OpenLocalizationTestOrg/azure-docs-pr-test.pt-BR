---
title: "aaaAzure monitoramento de desempenho do serviço de malha | Microsoft Docs"
description: "Saiba mais sobre os contadores de desempenho para o monitoramento e diagnóstico de clusters do Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 54d4c62b7250a1f70b0898ba07ae5a37716f4cf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-metrics"></a>Métricas de desempenho

Métricas devem ser coletados toounderstand Olá desempenho do cluster, bem como Olá aplicativos em execução. Para clusters de malha do serviço, recomendamos coletar Olá contadores de desempenho a seguir.

## <a name="nodes"></a>Nós

Para máquinas de saudação no seu cluster, considere coletando Olá toobetter entender Olá carga em cada computador e fazer cluster apropriados dimensionamento decisões de contadores de desempenho a seguir.

| Categoria do Contador | Nome do contador |
| --- | --- |
| PhysicalDisk(per Disco) | Média Tamanho de Fila de Leitura de Disco |
| PhysicalDisk(per Disco) | Média Tamanho de Fila de Gravação de Disco |
| PhysicalDisk(per Disco) | Média de segundos/Leitura do Disco |
| PhysicalDisk(per Disco) | Média de segundos/Gravação do Disco |
| PhysicalDisk(per Disco) | Leituras de Disco/s  |
| PhysicalDisk(per Disco) | Bytes Lidos no Disco/s  |
| PhysicalDisk(per Disco) | Gravações de Disco/s |
| PhysicalDisk(per Disco) | Bytes Gravados no Disco/s |
| Memória | MBytes Disponíveis |
| PagingFile | % Uso |
| Processo(Total) | % Tempo do Processador |
| Processo (por serviço) | % Tempo do Processador |
| Processo (por serviço) | ID do Processo |
| Processo (por serviço) | Bytes Particulares |
| Processo (por serviço) | Contagem de Threads |
| Processo (por serviço) | Bytes Virtuais |
| Processo (por serviço) | Conjunto de Trabalho |
| Processo (por serviço) | Conjunto de Trabalho - Particular |

## <a name="net-applications-and-services"></a>Aplicativos e serviços de .NET

Olá coletar contadores a seguir se você estiver implantando o .NET de serviços de cluster tooyour. 

| Categoria do Contador | Nome do contador |
| --- | --- |
| Memória CLR .NET (por serviço) | ID do Processo |
| Memória CLR .NET (por serviço) | Nº Total de Bytes confirmados |
| Memória CLR .NET (por serviço) | N º Total de Bytes reservados |
| Memória CLR .NET (por serviço) | N º de Bytes em todos os Heaps |
| Memória CLR .NET (por serviço) | Nº de Coleções Geração 0 |
| Memória CLR .NET (por serviço) | Nº de Coleções Geração 1 |
| Memória CLR .NET (por serviço) | Nº de Coleções Geração 2 |
| Memória CLR .NET (por serviço) | % de Tempo na GC |

### <a name="service-fabrics-custom-performance-counters"></a>Contadores de desempenho personalizados do Service Fabric

O Service Fabric gera uma quantidade significativa de contadores de desempenho personalizados. Se você tiver Olá SDK instalado, você pode ver lista abrangente de saudação em seu computador Windows em seu aplicativo do Monitor de desempenho (Iniciar > Monitor de desempenho). 

Em aplicativos de saudação você está implantando tooyour cluster, se você estiver usando Reliable Actors, adicione countes de `Service Fabric Actor` e `Service Fabric Actor Method` categorias (consulte [Service Fabric confiável atores diagnóstico](service-fabric-reliable-actors-diagnostics.md)).

Se você usar os Reliable Services, teremos as categorias de contadores `Service Fabric Service` e `Service Fabric Service Method` das quais você deverá coletar contadores. 

Se você usar coleções confiável, é recomendável adicionar Olá `Avg. Transaction ms/Commit` de saudação `Service Fabric Transactional Replicator` toocollect latência de confirmação média Olá por métrica da transação.


## <a name="next-steps"></a>Próximas etapas

* Saiba mais sobre [geração de eventos no nível de plataforma Olá](service-fabric-diagnostics-event-generation-infra.md) na malha do serviço
* Coletar métricas de desempenho por meio dos [Diagnóstico do Azure](service-fabric-diagnostics-event-aggregation-wad.md)
