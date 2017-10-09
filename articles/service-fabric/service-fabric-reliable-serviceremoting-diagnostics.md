---
title: "aaaAzure ServiceFabric diagnóstico e monitoramento | Microsoft Docs"
description: "Este artigo descreve os recursos de monitoramento de desempenho de saudação do Olá ServiceRemoting confiável de malha de serviço em tempo de execução, como contadores de desempenho emitidos por ela."
services: service-fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: suchiagicha
ms.assetid: 1c229923-670a-4634-ad59-468ff781ad18
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: suchiagicha
ms.openlocfilehash: 64db9a890bd59a1326e587d14b89c007b71a9059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-performance-monitoring-for-reliable-service-remoting"></a>Diagnóstico e monitoramento de desempenho para Reliable Service Remoting
tempo de execução do Hello ServiceRemoting confiável emite [contadores de desempenho](https://msdn.microsoft.com/library/system.diagnostics.performancecounter.aspx). Esses fornecem ideias sobre como Olá ServiceRemoting está funcionando e ajudá-lo com solução de problemas e monitoramento do desempenho.


## <a name="performance-counters"></a>Contadores de desempenho
tempo de execução do Hello ServiceRemoting confiável define Olá categorias de contador de desempenho a seguir:

| Categoria | Descrição |
| --- | --- |
| Serviço do Service Fabric |Contadores específico tooAzure comunicação remota do serviço de malha de serviço, por exemplo, tooprocess de tempo médio de solicitação |
| Método de Serviço do Service Fabric |Toomethods específico contadores implementado por exemplo, pelo serviço de comunicação remota do serviço de malha, quantas vezes um método de serviço é invocado |

Cada saudação anterior categorias tem um ou mais contadores.

Olá [o Monitor de desempenho do Windows](https://technet.microsoft.com/library/cc749249.aspx) aplicativo que está disponível por padrão no sistema de operacional do Windows hello pode ser usados dados de contador de desempenho de toocollect e modo de exibição. [Diagnóstico do Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) é outra opção para coletar dados do contador de desempenho e carregá-lo tooAzure tabelas.

### <a name="performance-counter-instance-names"></a>Nomes da instância do contador de desempenho
Um cluster que tem um grande número de serviços do ServiceRemoting ou partições tem um grande número de instâncias do contador de desempenho. instância do contador de desempenho Olá nomes podem ajudar a identificar a partição específica hello e método de serviço (se aplicável) essa instância do contador de desempenho hello está associada.

#### <a name="service-fabric-service-category"></a>Categoria de Serviço do Service Fabric
Categoria de saudação `Service Fabric Service`, nomes de instância de contador Olá estão em Olá formato a seguir:

`ServiceFabricPartitionID_ServiceReplicaOrInstanceId_ServiceRuntimeInternalID`

*ServiceFabricPartitionID* é a representação de cadeia de caracteres de saudação de saudação ID de partição de malha do serviço que Olá a instância do contador de desempenho está associado. Olá ID de partição é um GUID e sua representação de cadeia de caracteres é gerada por meio de saudação [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) método com especificador de formato "D".

*ServiceReplicaOrInstanceId* é a representação de cadeia de caracteres de saudação do hello ID de instância/réplica malha do serviço que Olá a instância do contador de desempenho está associado.

*ServiceRuntimeInternalID* é a representação de cadeia de caracteres de saudação de um inteiro de 64 bits que é gerado pelo tempo de execução do serviço de malha Olá para seu uso interno. Isso está incluído na instância do contador de desempenho Olá nome tooensure sua exclusividade e evitar conflitos com outros nomes de instância do contador de desempenho. Os usuários não devem tentar toointerpret esta parte do nome de instância do contador de desempenho de saudação.

Olá, a seguir é um exemplo de um nome de instância do contador para um contador que pertence a toohello `Service Fabric Service` categoria:

`2740af29-78aa-44bc-a20b-7e60fb783264_635650083799324046_5008379932`

Em Olá anterior como exemplo, `2740af29-78aa-44bc-a20b-7e60fb783264` é a representação de cadeia de caracteres de saudação do ID de partição do Service Fabric Olá, `635650083799324046` é a representação de cadeia de caracteres da réplica/InstanceId e `5008379932` é Olá ID de 64 bits que é gerado para tempo de execução Olá interno Use.

#### <a name="service-fabric-service-method-category"></a>Categoria Método de Serviço do Service Fabric
Categoria de saudação `Service Fabric Service Method`, nomes de instância de contador Olá estão em Olá formato a seguir:

`MethodName_ServiceRuntimeMethodId_ServiceFabricPartitionID_ServiceReplicaOrInstanceId_ServiceRuntimeInternalID`

*MethodName* é o nome de saudação do método de serviço de Olá Olá a instância do contador de desempenho está associado. formato de saudação do nome do método hello é determinado com base em alguma lógica em tempo de execução de serviço de malha de saudação que equilibra a legibilidade de saudação do nome de saudação com restrições no tamanho máximo de saudação de nomes de instância do contador de desempenho de saudação no Windows.

*ServiceRuntimeMethodId* é a representação de cadeia de caracteres de saudação de um inteiro de 32 bits que é gerado pelo tempo de execução do serviço de malha Olá para seu uso interno. Isso está incluído na instância do contador de desempenho Olá nome tooensure sua exclusividade e evitar conflitos com outros nomes de instância do contador de desempenho. Os usuários não devem tentar toointerpret esta parte do nome de instância do contador de desempenho de saudação.

*ServiceFabricPartitionID* é a representação de cadeia de caracteres de saudação de saudação ID de partição de malha do serviço que Olá a instância do contador de desempenho está associado. Olá ID de partição é um GUID e sua representação de cadeia de caracteres é gerada por meio de saudação [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) método com especificador de formato "D".

*ServiceReplicaOrInstanceId* é a representação de cadeia de caracteres de saudação do hello ID de instância/réplica malha do serviço que Olá a instância do contador de desempenho está associado.

*ServiceRuntimeInternalID* é a representação de cadeia de caracteres de saudação de um inteiro de 64 bits que é gerado pelo tempo de execução do serviço de malha Olá para seu uso interno. Isso está incluído na instância do contador de desempenho Olá nome tooensure sua exclusividade e evitar conflitos com outros nomes de instância do contador de desempenho. Os usuários não devem tentar toointerpret esta parte do nome de instância do contador de desempenho de saudação.

Olá, a seguir é um exemplo de um nome de instância do contador para um contador que pertence a toohello `Service Fabric Service Method` categoria:

`ivoicemailboxservice.leavemessageasync_2_89383d32-e57e-4a9b-a6ad-57c6792aa521_635650083804480486_5008380`

Em Olá anterior como exemplo, `ivoicemailboxservice.leavemessageasync` é o nome do método hello, `2` é hello usar a ID de 32 bits para interno do tempo de execução de saudação, `89383d32-e57e-4a9b-a6ad-57c6792aa521` é a representação de cadeia de caracteres de saudação do ID de partição do Service Fabric Olá,`635650083804480486` é a cadeia de caracteres de saudação representação de saudação ID de instância/réplica de malha do serviço e `5008380` é usar o ID de 64 bits Olá gerado para interno do tempo de execução de saudação.

## <a name="list-of-performance-counters"></a>Lista de Contadores de desempenho
### <a name="service-method-performance-counters"></a>Contadores de desempenho do método de serviço

tempo de execução de um serviço confiável Olá publica Olá após a execução de toohello relacionados de contadores de desempenho de métodos de serviço.

| Nome da categoria | Nome do contador | Descrição |
| --- | --- | --- |
| Método de Serviço do Service Fabric |Invocação/s |Número de vezes que o método de serviço hello é invocado por segundo |
| Método de Serviço do Service Fabric |Média de milissegundos por invocação |Tempo decorrido do método de serviço tooexecute hello em milissegundos |
| Método de Serviço do Service Fabric |Exceções lançadas/s |Número de vezes que Olá método serviço lançou uma exceção por segundo |

### <a name="service-request-processing-performance-counters"></a>Solicitação de serviço processando contadores de desempenho
Quando um cliente invoca um método por meio de um objeto de proxy de serviço, isso resulta em uma mensagem de solicitação a ser enviada através do serviço de comunicação remota do hello rede toohello. serviço de saudação processa a mensagem de solicitação de saudação e envia uma resposta toohello back cliente. tempo de execução do Hello ServiceRemoting confiável publica Olá processamento de solicitação de tooservice relacionados de contadores de desempenho a seguir.

| Nome da categoria | Nome do contador | Descrição |
| --- | --- | --- |
| Serviço do Service Fabric |nº de solicitações pendentes |Número de solicitações sendo processadas no serviço Olá |
| Serviço do Service Fabric |Média de milissegundos por solicitação |Tempo (em milissegundos) Olá serviço tooprocess uma solicitação |
| Serviço do Service Fabric |Média de milissegundos para desserialização de solicitação |Tempo toodeserialize feito (em milissegundos) serviço mensagem de solicitação quando ela é recebida no serviço Olá |
| Serviço do Service Fabric |Média de milissegundos para serialização de resposta |Mensagem de resposta do serviço do tempo tooserialize feito (em milissegundos) Olá no serviço Olá antes do envio toohello cliente de resposta de saudação |

## <a name="next-steps"></a>Próximas etapas
* [Exemplo de código](https://github.com/Azure/servicefabric-samples)
* [Provedores de EventSource no PerfView](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
