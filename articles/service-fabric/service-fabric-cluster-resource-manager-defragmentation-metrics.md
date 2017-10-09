---
title: "aaaDefragmentation de métricas no Azure Service Fabric | Microsoft Docs"
description: "Uma visão geral do uso de desfragmentação ou como uma estratégia de métricas no Service Fabric"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: e5ebfae5-c8f7-4d6c-9173-3e22a9730552
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: d09045a6cf196d2771f1a0794637f4579d3eb96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="defragmentation-of-metrics-and-load-in-service-fabric"></a>Desfragmentação de métricas e carga no Service Fabric
estratégia de padrão de saudação malha Cluster recursos do Service Manager para gerenciar as métricas de carga no cluster Olá tem a carga de saudação do toodistribute. Garantindo que nós sejam utilizados uniformemente evita pontos altos e baixos que levam a contenção de tooboth e desperdício de recursos. Distribuir cargas de trabalho no cluster Olá também é hello mais segura em termos de sobreviventes falhas porque garante que uma falha não tem um grande percentual de uma determinada carga de trabalho. 

Olá Gerenciador de recursos de Cluster do serviço de malha dá suporte a uma estratégia diferente para o gerenciamento de carga, que é a desfragmentação. Desfragmentação significa que, em vez de tentar toodistribute utilização de saudação de uma métrica em cluster hello, ele é consolidado. A consolidação é apenas uma inversão do padrão de saudação balanceamento estratégia – em vez de minimizando Olá desvio médio de padrão de métrica de carga, Olá Gerenciador de recursos de Cluster tenta tooincrease-lo.

## <a name="when-toouse-defragmentation"></a>Quando a desfragmentação toouse
Distribuindo a carga no cluster Olá consome alguns dos recursos de saudação em cada nó. Algumas cargas de trabalho criam serviços que são excepcionalmente grandes e consomem a maior parte de um nó. Nesses casos, é possível que quando houver grandes cargas de trabalho obtendo criadas que não há suficiente espaço em qualquer nó toorun-los. Grandes cargas de trabalho não são um problema na malha do serviço; Olá esses casos Gerenciador de recursos de Cluster determina que ele precisa tooreorganize Olá cluster toomake espaço grande carga de trabalho. No entanto, Olá enquanto isso carga de trabalho tem toobe toowait agendado no cluster hello.

Se houver muitos serviços e estado toomove ao redor, em seguida, pode levar muito tempo para Olá grande carga de trabalho toobe colocado em cluster hello. Isso é mais provável se outras cargas de trabalho no cluster Olá também são grandes e reserve tooreorganize mais. equipe do Service Fabric Olá medido tempo de criação no simulações deste cenário. Descobrimos que a criação de serviços grandes passou a demorar muito mais assim que a utilização do cluster atingiu entre 30% e 50%. toohandle neste cenário, apresentamos desfragmentação como uma estratégia de balanceamento. Descobrimos que para grandes cargas de trabalho, especialmente aqueles em que a hora de criação foi importante, desfragmentação realmente ajudou a essas novas cargas de trabalho seja agendadas em cluster hello.

Você pode configurar a desfragmentação métricas toohave Olá carga de saudação do tooproactively do Gerenciador de recursos de Cluster tente toocondense dos serviços de saudação em menos nós. Isso ajuda a garantir que quase sempre há espaço para serviços grandes sem reorganizar cluster hello. Não tem o cluster de saudação tooreorganize permite a criação de grandes cargas de trabalho rapidamente.

A maioria das pessoas não precisa da desfragmentação. Os serviços são geralmente ser pequena, para que não seja espaço toofind disco rígido para eles no cluster de saudação. Quando reorganização é possível, ela ocorre rapidamente, novamente porque a maioria dos serviços são pequenos e podem ser movidos rapidamente e em paralelo. No entanto, se você tiver serviços grandes e necessário criado rapidamente Olá estratégia de desfragmentação é para você. Vamos discutir as compensações de saudação do uso de desfragmentação em seguida. 

## <a name="defragmentation-tradeoffs"></a>Vantagens e desvantagens da desfragmentação
A desfragmentação pode aumentar o impacto das falhas, já que mais serviços estão em execução nos nós que falham. A desfragmentação também pode aumentar os custos, como recursos no cluster Olá devem ser mantidos em reserva, aguardando a criação de saudação de grandes cargas de trabalho.

Olá diagrama a seguir fornece uma representação visual dos dois clusters, um que é desfragmentado e que não é. 

<center>
![Comparando clusters balanceados e desfragmentados][Image1]
</center>

No caso de Olá balanceada, considere o número de Olá de movimentações que seria necessário tooplace uma saudação maior de objetos de serviço. No cluster de desfragmentado hello, grande carga de trabalho de saudação pode ser colocada em nós quatro ou cinco sem ter que toowait para quaisquer outros serviços toomove.

## <a name="defragmentation-pros-and-cons"></a>Prós e contras da desfragmentação
Quais são as outras compensações conceituais? Aqui está uma tabela rápida de coisas toothink sobre:

| Vantagens da desfragmentação | Desvantagens da desfragmentação |
| --- | --- |
| Agiliza a criação de serviços grandes |Concentra a carga em menos nós, aumentando a contenção |
| Permite a redução da movimentação de dados durante a criação |Falhas podem afetar mais serviços e causar mais variação |
| Permite a descrição detalhada dos requisitos e a recuperação de espaço |Configuração geral mais complexa do Gerenciamento de Recursos |

Você pode combinar desfragmentado e métricas normais no hello mesmo cluster. Olá Gerenciador de recursos de Cluster tentativas tooconsolidate Olá desfragmentação métricas tanto quanto possível ao propagar Olá outras pessoas. resultados de saudação de uma combinação de desfragmentação e balanceamento estratégias depende de vários fatores, incluindo:
  - número de saudação do balanceamento de métricas versus o número de saudação de métricas de desfragmentação
  - Se algum serviço usar os dois tipos de métricas 
  - pesos de métrica Olá
  - as cargas da métrica atual
  
Experimentação é necessário toodetermine Olá exata configuração necessária. Recomendamos fazer uma medição completa de suas cargas de trabalho antes de habilitar as métricas de desfragmentação na produção. Isso é especialmente verdadeiro quando a combinação de desfragmentação e métricas equilibradas em Olá mesmo serviço. 

## <a name="configuring-defragmentation-metrics"></a>Configurando métricas de desfragmentação
Configurar métricas de desfragmentação é uma decisão global no cluster hello e métricas individuais podem ser selecionadas para desfragmentação. Olá config trechos de código a seguir mostra como tooconfigure métricas para desfragmentação. Nesse caso, "Metric1" é configurado como uma métrica de desfragmentação, enquanto "Metric2" continuará toobe balanceada normalmente. 

ClusterManifest.xml:

```xml
<Section Name="DefragmentationMetrics">
    <Parameter Name="Metric1" Value="true" />
    <Parameter Name="Metric2" Value="false" />
</Section>
```

via ClusterConfig.json para implantações autônomas ou Template.json para clusters hospedados pelo Azure:

```json
"fabricSettings": [
  {
    "name": "DefragmentationMetrics",
    "parameters": [
      {
          "name": "Metric1",
          "value": "true"
      },
      {
          "name": "Metric2",
          "value": "false"
      }
    ]
  }
]
```


## <a name="next-steps"></a>Próximas etapas
- Olá Gerenciador de recursos de Cluster tem opções de man para descrever o cluster hello. toofind mais sobre eles, leia este artigo em [que descreve um cluster do Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)
- Métricas são como Olá Gerenciador de recursos de Cluster do serviço de malha gerencia capacidade em cluster hello e consumo. toolearn mais sobre as métricas e como tooconfigure-los, confira [neste artigo](service-fabric-cluster-resource-manager-metrics.md)

[Image1]:./media/service-fabric-cluster-resource-manager-defragmentation-metrics/balancing-defrag-compared.png
