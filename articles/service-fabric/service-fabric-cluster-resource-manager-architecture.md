---
title: Arquitetura do Gerenciador de aaaResource | Microsoft Docs
description: "Uma visão geral da arquitetura do Gerenciador de Recursos de Cluster do Service Fabric."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 6c4421f9-834b-450c-939f-1cb4ff456b9b
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 9ea80273d0566a2ac25143ada3662875656b57b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="cluster-resource-manager-architecture-overview"></a>Visão geral da arquitetura do Gerenciador de Recursos de Cluster
Olá Gerenciador de recursos de Cluster do serviço de malha é um serviço central que é executado no cluster hello. Ele gerencia o estado de saudação desejado de serviços de saudação em cluster hello, particularmente com respeito tooresource consumo e todas as regras de posicionamento. 

recursos de saudação toomanage no cluster, Olá Gerenciador de recursos de Cluster do serviço de malha deve ter várias partes de informações:

- Quais serviços existem atualmente
- O consumo de recursos atual (ou padrão) de cada serviço 
- capacidade restante de cluster Olá 
- capacidade de saudação de nós de saudação do cluster de saudação 
- quantidade de saudação de recursos consumidos em cada nó

consumo de recursos de saudação de um determinado serviço pode alterar ao longo do tempo, e serviços importam geralmente mais de um tipo de recurso. Em serviços diferentes, pode haver recursos físicos e físicos reais que estão sendo medidos. Os serviços podem rastrear métricas físicas, como consumo de disco e memória. Com mais frequência, os serviços podem considerar métricas lógicas — como "WorkQueueDepth" ou "TotalRequests". Métricas lógicas e físicas podem ser usadas em Olá mesmo cluster. As métricas podem ser compartilhadas entre vários serviços ou ser tooa específico determinado serviço.

## <a name="other-considerations"></a>Outras considerações
Olá proprietários e operadores de cluster Olá podem ser diferentes do hello autores de serviço e aplicativos ou em um mínimo são Olá mesmo pessoas usando funções diferentes. Quando desenvolve seu aplicativo, você sabe quais são algumas das coisas que ele requer. Você tem uma estimativa da saudação consumirá de recursos e serviços diferentes devem ser implantados. Por exemplo, a camada da web de saudação precisa toorun em toohello nós expostos à Internet, enquanto os serviços de banco de dados de saudação não devem. Como outro exemplo, os serviços da web hello provavelmente são restritas por CPU e de rede, enquanto o cuidado de serviços de camada Olá dados mais sobre o consumo de memória e disco. No entanto, pessoa Olá tratamento de um incidente de site em tempo real para esse serviço em produção, ou que está gerenciando um serviço de atualização toohello tem toodo um trabalho diferente e requer ferramentas diferentes. 

Cluster hello e serviços são dinâmicos:

- número de saudação de nós no cluster Olá pode aumentar ou reduzir
- Nós de diferentes tamanhos e tipos podem entrar e sair
- Serviços podem ser criados, removidos e podem alterar as respectivas alocações de recursos e regras de posicionamento desejadas
- Atualizações ou outras operações de gerenciamento podem reverter cluster Olá no aplicativo hello nos níveis de infraestrutura
- Falhas podem ocorrer a qualquer momento.

## <a name="cluster-resource-manager-components-and-data-flow"></a>Componentes e fluxo de dados do Gerenciador de Recursos de Cluster
Olá Gerenciador de recursos de Cluster tem requisitos de saudação do tootrack de cada serviço e hello o consumo de recursos por cada objeto de serviço nesses serviços. Olá Gerenciador de recursos de Cluster tem duas partes conceituais: agentes executados em cada nó e um serviço tolerante a falhas. agentes de Olá em cada nó de carga de rastrear relatórios de serviços, agregação-los e relatá-los periodicamente. Olá serviço Gerenciador de recursos de Cluster agrega todas as informações de saudação de agentes local hello e reage com base em sua configuração atual.

Vejamos Olá diagrama a seguir:

<center>
![Arquitetura do Balanceador de Recursos][Image1]
</center>

No tempo de execução, muitas alterações poderiam acontecer. Por exemplo, digamos que a quantidade de saudação de recursos de alguns serviços consumam alterações, algumas falhas de serviços, e alguns nós entram e saem cluster hello. Todas as alterações de saudação em um nó são agregadas e enviadas periodicamente toohello Gerenciador de recursos de Cluster service (1,2) em que eles são agregados novamente, analisados e armazenados. Em alguns segundos em que serviço examina Olá alterações e determina se as ações são necessárias (3). Ele pode, por exemplo, observe que alguns nós vazios foram adicionados toohello cluster. Como resultado, decide toomove alguns nós toothose de serviços. Olá Gerenciador de recursos de Cluster foi Observe também que um nó específico está sobrecarregado ou que determinados serviços têm falhou ou foi excluídos, liberando recursos em outro lugar.

Vamos examinar Olá diagrama a seguir e veja o que acontece em seguida. Vamos dizer que Olá Gerenciador de recursos de Cluster determina que são necessárias alterações. Ele coordena com outras alterações necessárias do sistema services (em determinado Olá Gerenciador de Failover) toomake hello. Em seguida, comandos necessários Olá são enviados toohello apropriado nós (4). Por exemplo, digamos que Olá Gerenciador de recursos notado que Nó5 estava sobrecarregado e então decidir toomove serviço B de tooNode4 Nó5. Final de saudação de reconfiguração da saudação (5), cluster Olá tem esta aparência:

<center>
![Arquitetura do Balanceador de Recursos][Image2]
</center>

## <a name="next-steps"></a>Próximas etapas
- Olá Gerenciador de recursos de Cluster tem muitas opções para descrever o cluster hello. toofind mais sobre eles, leia este artigo em [que descreve um cluster do Service Fabric](./service-fabric-cluster-resource-manager-cluster-description.md)
- tarefas de principal do Gerenciador de recursos do Cluster Olá são rebalanceamento cluster hello e impor regras de posicionamento. Para obter mais informações sobre como configurar esses comportamentos, consulte [Balanceamento do cluster do Service Fabric](./service-fabric-cluster-resource-manager-balancing.md)

[Image1]:./media/service-fabric-cluster-resource-manager-architecture/Service-Fabric-Resource-Manager-Architecture-Activity-1.png
[Image2]:./media/service-fabric-cluster-resource-manager-architecture/Service-Fabric-Resource-Manager-Architecture-Activity-2.png
