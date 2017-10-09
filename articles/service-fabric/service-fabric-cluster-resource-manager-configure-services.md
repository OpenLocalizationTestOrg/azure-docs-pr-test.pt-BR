---
title: "configurações de métrica e o posicionamento de aaaSpecify no microservices do Azure | Microsoft Docs"
description: "Descrição de um serviço do Service Fabric especificando métricas, restrições de posicionamento e outras políticas de posicionamento."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 16e135c1-a00a-4c6f-9302-6651a090571a
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: c633518b5dbf0c7b84e0d46c06bf1f92365d184d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-cluster-resource-manager-settings-for-service-fabric-services"></a>Configurando as definições do gerenciador de recursos de cluster para serviços do Service Fabric
Olá Gerenciador de recursos de Cluster do serviço de malha permite controle refinado sobre regras de saudação que controlam a cada chamada de serviço. Cada serviço nomeado pode especificar regras para como deve ser alocado no cluster hello. Cada serviço nomeado também pode definir o conjunto de saudação de métricas que ele deseja tooreport, incluindo como importantes são toothat serviço. A configuração de serviços é dividida em três tarefas diferentes:

1. Configurando restrições de posicionamento
2. Configurando métricas
3. Configuração de políticas de posicionamento avançado e outras regras (menos comuns)

## <a name="placement-constraints"></a>Restrições de posicionamento
Restrições de posicionamento são usada toocontrol quais nós no cluster Olá um serviço, na verdade, pode executar em. Normalmente uma determinada chamada instância de serviço ou todos os serviços de toorun um tipo de dado restringido em um determinado tipo de nó. Restrições de posicionamento são extensíveis. É possível definir qualquer conjunto de propriedades por tipo de nó e, em seguida, selecioná-los com restrições durante a criação de serviços. Também é possível alterar as restrições de posicionamento do serviço enquanto ele está em execução. Isso permite que você toochanges toorespond em cluster hello ou requisitos de saudação do serviço de saudação. Propriedades de saudação de um determinado nó também podem ser atualizadas dinamicamente em cluster hello. Para obter mais informações sobre restrições de posicionamento e como tooconfigure-los podem ser encontrados no [neste artigo](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints)

## <a name="metrics"></a>Métricas
Métricas são o conjunto de saudação de recursos que precisa de um determinado serviço nomeado. Uma configuração do serviço métrica inclui a quantidade do recurso consome cada instância sem monitoração de estado de serviço ou réplica com monitoração de estado por padrão. Métricas também incluem um peso que indica quão importante balanceamento métrica é o serviço de toothat, caso compensações são necessárias.

## <a name="advanced-placement-rules"></a>Regras de posicionamento avançadas
Há outros tipos de regras de posicionamento que são úteis em cenários menos comuns. Alguns exemplos incluem:
- Restrições que ajudam com clusters distribuídos geograficamente
- Determinadas arquiteturas de aplicativo

Outras regras de posicionamento são configuradas por meio de Correlações ou Políticas.

## <a name="next-steps"></a>Próximas etapas
- Métricas são como Olá Gerenciador de recursos de Cluster do serviço de malha gerencia capacidade em cluster hello e consumo. toolearn mais sobre as métricas e como tooconfigure-los, confira [neste artigo](service-fabric-cluster-resource-manager-metrics.md)
- A afinidade é um modo de configurar seus serviços. Ela não é comum, mas se precisar dela, você poderá saber mais [aqui](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)
- Há muitas regras de posicionamento diferentes que podem ser configuradas em seus cenários adicionais de toohandle do serviço. Você pode obter informações sobre essas diferentes políticas de posicionamento [aqui](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md)
- Desde o início de saudação e [obter uma introdução toohello Gerenciador de recursos de Cluster do serviço de malha](service-fabric-cluster-resource-manager-introduction.md)
- toofind out sobre como Olá Gerenciador de recursos de Cluster gerencia e equilibra a carga no cluster hello, check-out artigo Olá em [balanceamento de carga](service-fabric-cluster-resource-manager-balancing.md)
- Olá Gerenciador de recursos de Cluster tem muitas opções para descrever o cluster hello. toofind mais sobre eles, leia este artigo em [que descreve um cluster do Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)
