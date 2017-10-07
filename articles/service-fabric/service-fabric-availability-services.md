---
title: "aaaAvailability de serviços do Service Fabric | Microsoft Docs"
description: "Descreve a detecção de falhas, failover e recuperação para serviços"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 279ba4a4-f2ef-4e4e-b164-daefd10582e4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: c443aadfe31a1413359b08d34c4b7dd5db4edd16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="availability-of-service-fabric-services"></a>Disponibilidade dos serviços de malha do serviço
Este artigo fornece uma visão geral de como o Service Fabric mantém a disponibilidade de um serviço.

## <a name="availability-of-service-fabric-stateless-services"></a>Disponibilidade dos serviços de malha do serviço sem monitoração do estado
Os serviços do Service Fabric do Azure podem ser com ou sem estado. Um serviço sem monitoração de estado é um serviço de aplicativo que não tem nenhum [estado local](service-fabric-concepts-state.md) que precisa toobe altamente disponível ou confiável.

Criar um serviço sem estado requer a definição de uma `InstanceCount`. Contagem de instâncias de saudação define o número de saudação de instâncias do serviço sem monitoração de estado da saudação lógica de aplicativo que devem ser executados no cluster de saudação. Aumentar Olá número de instâncias é hello recomendado maneira de dimensionar um serviço sem monitoração de estado.

Quando uma instância de um sem monitoração de estado denominada serviço falha, uma nova instância é criada em algum nó qualificado no cluster de saudação. Por exemplo, uma instância de serviço sem estado pode falhar em Node1 e ser recriada em Node5.

## <a name="availability-of-service-fabric-stateful-services"></a>Disponibilidade dos serviços de malha do serviço com monitoração do estado
Um serviço com estado tem algum estado associado a ele. Na malha de serviço, um serviço com monitoração de estado é modelado como um conjunto de réplicas. Cada réplica é uma instância em execução de código de saudação do serviço de saudação que também tem uma cópia do estado de saudação para esse serviço. Operações de leitura e gravação são executadas em uma réplica (chamada hello primário). Toostate alterações de operações de gravação são *replicadas* toohello outras réplicas no conjunto de réplicas de saudação (chamado secundárias ativas) e aplicada. 

Pode haver apenas uma réplica Primária, mas pode haver várias réplicas Secundárias Ativas. saudação de número de réplicas secundárias ativas é configurável e um número maior de réplicas pode tolerar um maior número de falhas de hardware e software simultânea.

Se a réplica primária Olá cair, Service Fabric torna uma saudação secundário ativo réplicas Olá nova réplica primária. Esta réplica secundária ativa já tem a versão de hello atualizado do estado da saudação (via *replicação*), e pode continuar a processar leitura adicional e operações de gravação.

Esse conceito, de uma réplica que está sendo um primário ou secundário ativo, é conhecido como Olá função de réplica.

### <a name="replica-roles"></a>Funções de réplica
função Hello de uma réplica é toomanage usado Olá ciclo de vida do estado de saudação sendo gerenciado por que a réplica. Uma réplica cuja função é Primária atende a solicitações de leitura. Olá primário também trata todas as solicitações de gravação atualizando seu estado e replicar alterações de saudação. Essas alterações são secundárias ativas de toohello aplicado no conjunto de réplicas de saudação. trabalho de saudação de um secundário ativo é as alterações de estado tooreceive Olá a réplica primária foi replicado e atualizar a exibição do estado de saudação.

> [!NOTE]
> Modelos de programação de nível superior como [Reliable Actors](service-fabric-reliable-actors-introduction.md) e [serviços confiáveis](service-fabric-reliable-services-introduction.md) ocultar o conceito de saudação da função de réplica de desenvolvedor hello. Em atores, noção de saudação da função é desnecessária, ao mesmo tempo nos serviços em grande parte, ele é simplificado para a maioria dos cenários.
>

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre os conceitos de malha do serviço, consulte Olá artigos a seguir:

- [Dimensionando serviços do Service Fabric](service-fabric-concepts-scalability.md)
- [Particionando serviços da Malha do Serviço](service-fabric-concepts-partitioning.md)
- [Definindo e gerenciando o estado](service-fabric-concepts-state.md)
- [Reliable Services](service-fabric-reliable-services-introduction.md)
