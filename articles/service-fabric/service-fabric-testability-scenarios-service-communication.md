---
title: "Possibilidade de teste: comunicação de serviço | Microsoft Docs"
description: "As comunicação entre serviços é um ponto de integração essencial de um aplicativo da Malha do Serviço. Este artigo aborda as considerações de design e as técnicas de teste."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 017557df-fb59-4e4a-a65d-2732f29255b8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 4a8f941c1e8e641384a9ee3a1149dabaaf9983cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-testability-scenarios-service-communication"></a>Cenários de Possibilidade de Teste do Service Fabric: Comunicação do serviço
Os estilos de arquitetura orientada a serviços e microsserviços surgem naturalmente no Azure Service Fabric. Esses tipos de arquiteturas distribuídas, microsserviço em componentes de aplicativos normalmente são compostos de vários serviços que precisam tootalk tooeach outros. Em casos mais simples do mesmo hello, você geralmente tem pelo menos um serviço web sem monitoração de estado e um serviço de armazenamento de dados com monitoração de estado que precisam de toocommunicate.

Comunicação de serviços é um ponto de integração crítico de um aplicativo, pois cada serviço expõe um remoto tooother serviços da API. Trabalhar com um conjunto de limites de API que envolve E/S geralmente exige algum cuidado e uma boa quantidade de teste e validação.

Há inúmeros toomake de considerações sobre quando esses limites de serviço são conectados em um sistema distribuído:

* *Protocolo de transporte*. Você usará HTTP para maior interoperabilidade, ou um protocolo binário personalizado para taxa de transferência máxima?
* *Manipulação de erros*. Como os erros transitórios e permanentes serão tratados? O que acontecerá quando um serviço move tooa um nó diferente?
* *Tempos limite e latência*. Em aplicativos de várias camadas, como cada camada de serviço tratará latência por meio de usuário de pilha e toohello Olá?

Se você usar um dos componentes de comunicação de serviço interno Olá fornecidos pelo serviço de malha ou criar seu próprio, teste interações de saudação entre seus serviços é crítico tooensuring resiliência em seu aplicativo.

## <a name="prepare-for-services-toomove"></a>Preparar para serviços toomove
As instâncias do serviço podem se movimentar com o tempo. Isso acontece especialmente quando são configuradas com métricas de carga para balanceamento personalizado e ideal de recursos. Malha do serviço move o toomaximize de instâncias do serviço sua disponibilidade mesmo durante atualizações, failovers, expansão e outras situações que ocorrem em tempo de vida de saudação de um sistema distribuído.

Como serviços mover-se no cluster hello, seus clientes e outros serviços devem ser preparado toohandle dois cenários quando falam tooa serviço:

* réplica de partição ou instância de serviço Olá foi movido desde Olá falou tooit de hora. Esta é uma parte normal de um ciclo de vida do serviço e deve ser toohappen esperado durante a vida útil de saudação do seu aplicativo.
* réplica de partição ou instância de serviço Hello está no processo de saudação de movimentação. Embora o failover de um serviço tooanother de um nó ocorre rapidamente na malha do serviço, pode haver um atraso na disponibilidade se o componente de comunicação de saudação do seu serviço é toostart lenta.

A manipulação tranquila desses cenários é importante para um sistema em execução adequada. toodo, portanto, tenha em mente que:

* Cada serviço que pode ser conectado toohas um *endereço* que escuta (por exemplo, HTTP ou WebSockets). Quando uma instância de serviço ou partição se move, altera seu ponto de extremidade do endereço. (Ele move tooa outro nó com um endereço IP diferente.) Se você estiver usando componentes de comunicação interna hello, eles tratarão novamente resolvendo endereços de serviço para você.
* Pode haver um aumento temporário na latência de serviço como Olá serviço instância começa a escuta novamente. Isso depende de como serviço Olá abre rapidamente ouvinte Olá depois que a instância do serviço Olá é movida.
* Todas as conexões existentes necessário toobe fechado e reaberto depois que o serviço Olá é aberto em um novo nó. Um desligamento normal do nó ou reinicialização dá tempo para toobe de conexões existentes desligar normalmente.

### <a name="test-it-move-service-instances"></a>Teste: Mover instâncias do serviço
Usando ferramentas de capacidade de teste do Service Fabric, você pode criar um tootest de cenário de teste nessas situações de maneiras diferentes:

1. Mova a réplica primária de um serviço com estado.
   
    Olá réplica primária de uma partição de serviço com monitoração de estado pode ser movida por vários motivos. Use esta réplica primária de saudação tootarget de um toosee partição específica como seu toohello reagir de serviços para mover de uma maneira muito controlada.
   
    ```powershell
   
    PS > Move-ServiceFabricPrimaryReplica -PartitionId 6faa4ffa-521a-44e9-8351-dfca0f7e0466 -ServiceName fabric:/MyApplication/MyService
   
    ```
2. Parar um nó.
   
    Quando um nó é interrompido, Service Fabric move todos Olá service instâncias ou partições que estavam no tooone desse nó de Olá outros nós disponíveis no cluster hello. Use este tootest uma situação em que um nó for perdido do cluster e todas as instâncias de serviço hello e réplicas nesse nó tem toomove.
   
    Você pode interromper um nó usando Olá PowerShell **ServiceFabricNode Stop** cmdlet:
   
    ```powershell
   
    PS > Restart-ServiceFabricNode -NodeName Node_1
   
    ```

## <a name="maintain-service-availability"></a>Manter a disponibilidade do serviço
Como uma plataforma, o Service Fabric é projetado tooprovide alta disponibilidade de seus serviços. Em casos extremos, porém, os problemas de infraestrutura subjacentes ainda podem causar indisponibilidade. É muito importante tootest para esses cenários.

Serviços com monitoração de estado usam um estado do sistema baseado em quorum tooreplicate para alta disponibilidade. Isso significa que um quorum de réplicas precisa de operações de gravação do toobe tooperform disponíveis. Em casos raros, como em uma falha generalizada de hardware, talvez um quorum de réplicas não esteja disponível. Nesses casos, não será capaz de tooperform operações de gravação, mas ainda será capaz de tooperform operações de leitura.

### <a name="test-it-write-operation-unavailability"></a>Teste: Indisponibilidade da operação de gravação
Usando ferramentas de capacidade de teste de saudação na malha do serviço, você pode injetar uma falha que induz à perda de quorum como um teste. Embora esse cenário é raro, é importante que os clientes e serviços que dependem de um serviço com monitoração de estado são preparados toohandle situações em que eles não podem fazer tooit solicitações de gravação. Também é importante que o serviço de monitoração de estado Olá em si está ciente de que essa possibilidade e pode normalmente comunicá-la toocallers.

Você pode induzir a perda de quorum usando Olá PowerShell **ServiceFabricPartitionQuorumLoss Invoke** cmdlet:

```powershell

PS > Invoke-ServiceFabricPartitionQuorumLoss -ServiceName fabric:/Myapplication/MyService -QuorumLossMode QuorumReplicas -QuorumLossDurationInSeconds 20

```

Neste exemplo, vamos definir `QuorumLossMode` muito`QuorumReplicas` tooindicate que desejamos perda de quorum tooinduce sem interromper todas as réplicas. Dessa forma, as operações de leitura ainda são possíveis. tootest um cenário em que uma partição inteira estiver disponível, você pode definir essa opção muito`AllReplicas`.

## <a name="next-steps"></a>Próximas etapas
[Saiba mais sobre as ações de possibilidade de teste](service-fabric-testability-actions.md)

[Saiba mais sobre os cenários de possibilidade de teste](service-fabric-testability-scenarios.md)

