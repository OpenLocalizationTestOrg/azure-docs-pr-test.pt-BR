---
title: "aaaThrottling no Gerenciador de recursos de cluster Olá Service Fabric | Microsoft Docs"
description: "Saiba mais Aceleradores de saudação tooconfigure fornecidos pelo Gerenciador de recursos de Cluster do serviço de malha de saudação."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4a44678b-a5aa-4d30-958f-dc4332ebfb63
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: f418536911d3e3814e78a4d9f057dfb867ca7c63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-hello-service-fabric-cluster-resource-manager"></a>Olá limitação Gerenciador de recursos de Cluster do serviço de malha
Mesmo se você configurou corretamente o hello Gerenciador de recursos de Cluster, cluster Olá pode obter interrompida. Por exemplo, pode haver falha e nó de domínio falhas simultâneas - o que aconteceria se o que ocorreu durante uma atualização? Olá Gerenciador de recursos de Cluster sempre tenta toofix tudo, consumindo recursos do cluster Olá tentar tooreorganize e correção de cluster de saudação. Limitadores ajudam a fornecer uma barreira para que o cluster Olá pode usar recursos toostabilize - nós Olá voltar, partições de rede Olá reparar, corrigidos bits implantados.

toohelp com esses tipos de situações, Olá Gerenciador de recursos de Cluster do serviço de malha inclui várias limitações. Essas restrições são exigências razoavelmente grandes. Em geral, elas não devem ser alteradas sem planejamento e teste cuidadosos.

Se você alterar Aceleradores do Gerenciador de recursos do Cluster hello, você deverá ajustá-las carga real esperado de tooyour. Você pode determinar que você precisa toohave alguns limita em vigor, mesmo se isso significar cluster Olá leva mais tempo toostabilize em algumas situações. O teste é necessário toodetermine Olá correto valores limitadores. Limitadores precisam toobe tooallow alta o suficiente Olá cluster toorespond toochanges em um período de tempo razoável e baixo suficiente tooactually impedir muito o consumo de recursos. 

A maioria dos que vimos clientes de tempo de saudação usa limitadores foi porque já estavam em um ambiente de recurso restrito. Alguns exemplos seriam largura de banda de rede limitada para nós individuais ou discos que não são toobuild capaz de várias réplicas com monitoração de estado em paralelo devido a limitações de toothroughput. Sem limitações, as operações podem sobrecarregar esses recursos, fazendo com que as operações toofail ou lenta. Nessas situações clientes usado limitadores em soubessem que eles foram estendendo a quantidade de saudação do tempo gasto Olá cluster tooreach um estado estável. Os clientes também entendiam que poderiam acabar executando com uma confiabilidade geral menor enquanto estivessem restritos.


## <a name="configuring-hello-throttles"></a>Configurando Olá limita

Serviço de malha possui dois mecanismos para limitação do número de saudação de movimentações de réplica. mecanismo de padrão de saudação que existia antes do serviço de malha 5.7 representa limitação como um número absoluto de movimentações permitido. Isso não funciona para clusters de todos os tamanhos. Em particular, para o padrão de saudação grandes clusters valor pode ser muito pequeno, diminuir significativamente balanceamento mesmo quando é necessário, embora não tenha nenhum efeito em clusters menores. Esse mecanismo anterior foi substituído pelo baseadas em porcentagens de limitação, que oferece melhor escalabilidade com clusters dinâmicos no qual número de saudação de serviços e nós alteram regularmente.

Olá limitadores baseiam-se em uma porcentagem do número de saudação de réplicas em clusters de saudação. Percetage com base em limitadores Habilitar regra de saudação expressar: "não mova mais de 10% das réplicas em um intervalo de 10 minutos", por exemplo.

Olá as configurações baseadas em porcentagens limitação estão:

  - GlobalMovementThrottleThresholdPercentage - o número máximo de movimentações permitido no cluster a qualquer momento, expresso como porcentagem do número total de réplicas em cluster hello. 0 indica nenhum limite. valor padrão de saudação é 0. Se essa configuração e o GlobalMovementThrottleThreshold forem especificados, em seguida, hello limite mais conservador é usado.
  - GlobalMovementThrottleThresholdPercentageForPlacement - o número máximo de movimentações permitido durante a fase de posicionamento hello, expresso como porcentagem do número total de réplicas em cluster hello. 0 indica nenhum limite. valor padrão de saudação é 0. Se essa configuração e o GlobalMovementThrottleThresholdForPlacement forem especificados, em seguida, hello limite mais conservador é usado.
  - GlobalMovementThrottleThresholdPercentageForBalancing - o número máximo de movimentações permitido durante a saudação balanceamento fase, expressada como porcentagem do número total de réplicas em cluster hello. 0 indica nenhum limite. valor padrão de saudação é 0. Se essa configuração e o GlobalMovementThrottleThresholdForBalancing forem especificados, em seguida, hello limite mais conservador é usado.

Ao especificar o percentual de acelerador hello, você deve especificar % 5 como 0,05. intervalo de saudação nos quais essas limitações são governadas é hello GlobalMovementThrottleCountingInterval, que é especificado em segundos.


``` xml
<Section Name="PlacementAndLoadBalancing">
     <Parameter Name="GlobalMovementThrottleThresholdPercentage" Value="0" />
     <Parameter Name="GlobalMovementThrottleThresholdPercentageForPlacement" Value="0" />
     <Parameter Name="GlobalMovementThrottleThresholdPercentageForBalancing" Value="0" />
     <Parameter Name="GlobalMovementThrottleCountingInterval" Value="600" />
</Section>
```

via ClusterConfig.json para implantações Autônomas ou Template.json para clusters hospedados pelo Azure:

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "GlobalMovementThrottleThresholdPercentage",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleThresholdPercentageForPlacement",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleThresholdPercentageForBalancing",
          "value": "0.0"
      },
      {
          "name": "GlobalMovementThrottleCountingInterval",
          "value": "600"
      }
    ]
  }
]
```

### <a name="default-count-based-throttles"></a>Restrições baseadas em contagem padrão
Essas informações são fornecidas para o caso em que você tenha clusters mais antigos ou ainda retenha essas configurações em clusters que foram atualizados desde então. Em geral, é recomendável que elas são substituídas com aceleradores de baseadas em porcentagens do hello acima. Desde que baseadas em porcentagens de limitação é desabilitada por padrão, essas limitações permanecem Olá aceleradores de padrão para um cluster até que eles estão desabilitados e substituídos por limitadores baseadas em porcentagens de saudação. 

  - GlobalMovementThrottleThreshold – essa configuração controla o número total de saudação de movimentações de cluster Olá por algum tempo. tempo total de saudação é especificado em segundos como Olá GlobalMovementThrottleCountingInterval. valor padrão Olá Olá GlobalMovementThrottleThreshold é 1000 e valor padrão Olá Olá GlobalMovementThrottleCountingInterval é 600.
  - MovementPerPartitionThrottleThreshold – essa configuração controla o número total de saudação de movimentações de qualquer partição de serviço por algum tempo. tempo total de saudação é especificado em segundos como Olá MovementPerPartitionThrottleCountingInterval. valor padrão Olá Olá MovementPerPartitionThrottleThreshold é 50 e valor padrão Olá Olá MovementPerPartitionThrottleCountingInterval é 600.

configuração de saudação para esses Aceleradores segue Olá mesmo padrão como Olá baseadas em porcentagens de limitação.

## <a name="next-steps"></a>Próximas etapas
- toofind out sobre como Olá Gerenciador de recursos de Cluster gerencia e equilibra a carga no cluster hello, check-out artigo Olá em [balanceamento de carga](service-fabric-cluster-resource-manager-balancing.md)
- Olá Gerenciador de recursos de Cluster tem muitas opções para descrever o cluster hello. toofind mais sobre eles, leia este artigo em [que descreve um cluster do Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)
