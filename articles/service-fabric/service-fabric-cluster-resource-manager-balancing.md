---
title: aaaBalance o cluster do Azure Service Fabric | Microsoft Docs
description: "Uma introdução toobalancing seu cluster com hello Gerenciador de recursos de Cluster do serviço de malha."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 030b1465-6616-4c0b-8bc7-24ed47d054c0
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 5f7ad2f5cf4cfb3751a860f5293b03d2d5266d99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="balancing-your-service-fabric-cluster"></a>Balanceamento do cluster do Service Fabric
Olá Gerenciador de recursos de Cluster do serviço de malha dá suporte a alterações de carga dinâmico, reagindo tooadditions ou remoções de nós ou serviços. Ele também corrige automaticamente as violações de restrição e redistribui proativamente cluster hello. Mas com que frequência essas ações são executadas, e o que as dispara?

Há três categorias diferentes de trabalho que executa o Gerenciador de recursos de Cluster de saudação. Eles são:

1. Posicionamento – esse estágio lida com o posicionamento de réplicas com estado ou de instâncias sem estado que estejam ausentes. O posicionamento inclui os novos serviços e a manipulação de réplicas com estado ou de instâncias sem estado que falharam. A exclusão e o descarte de réplicas ou de instâncias são tratados aqui.
2. Verificações de restrição – neste estágio verifica e corrige violações de restrições de posicionamento diferentes hello (regras) no sistema de saudação. Os exemplos de regras são a garantia de que os nós não estão acima da capacidade e se as restrições de posicionamento do serviço estão sendo atendidas.
3. Balanceamento – neste estágio verifica toosee se rebalanceamento é necessário com base em Olá configurado desejado de nível de saldo para diferentes métricas. Nesse caso, ele tenta toofind que é de uma organização em Olá cluster mais balanceada.

## <a name="configuring-cluster-resource-manager-timers"></a>Configuração de temporizadores do Gerenciador de Recursos de Cluster
Olá primeiro conjunto de controles balanceamento são um conjunto de temporizadores. Esses temporizadores governam frequência hello Gerenciador de recursos de Cluster examina cluster hello e executa ações corretivas.

Cada um desses tipos diferentes de saudação correções Gerenciador de recursos de Cluster pode fazer é controlada por um timer diferente que rege sua frequência. Quando cada temporizador é acionado, Olá será agendada. Por padrão, Olá Gerenciador de recursos:

* verifica o estado e aplica atualizações (como gravação de um nó estiver inativo) cada 1/10 de segundo
* Define o sinalizador de verificação de posicionamento de saudação 
* Define o sinalizador de verificação de restrição de saudação por segundo
* Define Olá balanceamento sinalizador a cada cinco segundos.

A seguir estão exemplos de configuração de saudação que governam esses temporizadores:

ClusterManifest.xml:

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PLBRefreshGap" Value="0.1" />
            <Parameter Name="MinPlacementInterval" Value="1.0" />
            <Parameter Name="MinConstraintCheckInterval" Value="1.0" />
            <Parameter Name="MinLoadBalancingInterval" Value="5.0" />
        </Section>
```

via ClusterConfig.json para implantações Autônomas ou Template.json para clusters hospedados pelo Azure:

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "PLBRefreshGap",
          "value": "0.10"
      },
      {
          "name": "MinPlacementInterval",
          "value": "1.0"
      },
      {
          "name": "MinConstraintCheckInterval",
          "value": "1.0"
      },
      {
          "name": "MinLoadBalancingInterval",
          "value": "5.0"
      }
    ]
  }
]
```

Hoje Olá Gerenciador de recursos de Cluster só executa uma dessas ações ao mesmo tempo, em sequência. É por isso, consulte temporizadores toothese como "intervalos mínimo" e Olá ações serão direcionadas quando temporizadores Olá desligam como "sinalizadores de configuração". Por exemplo, Olá Gerenciador de recursos de Cluster se encarrega de pendente solicitações toocreate services antes de saudação cluster de balanceamento. Como você pode ver por intervalos de tempo padrão de saudação especificados, Olá Gerenciador de recursos de Cluster procura nada-toodo necessidades com frequência. Normalmente, isso significa que o conjunto de saudação das alterações feitas durante cada etapa é pequeno. Fazer pequenas alterações com frequência permite Olá toobe do Gerenciador de recursos de Cluster responsivo quando as coisas acontecem no cluster hello. Olá cronômetros padrão fornecem algumas envio em lote desde muitas Olá mesmo tipos de eventos tendem toooccur simultaneamente. 

Por exemplo, quando os nós falham, eles podem fazer com um domínio de falha inteiro por vez. Todas essas falhas são capturadas durante o próximo estado de saudação atualizar após Olá *PLBRefreshGap*. correções de saudação são determinadas durante a saudação posicionamento, verificação de restrição, a seguir e balanceamento é executado. Por saudação padrão Gerenciador de recursos de Cluster não é uma varredura horas das alterações no cluster de saudação e tentar tooaddress todas as alterações de uma vez. Isso levaria toobursts de variação.

Olá Gerenciador de recursos de Cluster também precisa toodetermine algumas informações adicionais se Olá cluster desequilibrados. Para isso, temos duas outras configurações: *Limites de Balanceamento* e *Limites de Atividade*.

## <a name="balancing-thresholds"></a>Limites de balanceamento
Um limite de balanceamento é controle principal de saudação para o disparo de rebalanceamento. Olá balanceamento limites para uma métrica é um _taxa_. Se carga Olá para uma métrica em hello mais carregado nó dividido pela quantidade de saudação de carga em Olá menos carregado nó excede essa métrica *BalancingThreshold*, cluster Olá é desequilibrado. Como resultado de balanceamento é disparada Olá hello do tempo Avançar verifica se o Gerenciador de recursos de Cluster. Olá *MinLoadBalancingInterval* timer define a frequência hello Gerenciador de recursos de Cluster deve verificar se o rebalanceamento é necessário. A verificação não significa que nada acontece. 

Os limites de balanceamento são definidos em uma base por métrica como parte da definição de cluster hello. Para saber mais sobre como fazer isso, leia [este artigo](service-fabric-cluster-resource-manager-metrics.md).

ClusterManifest.xml

```xml
    <Section Name="MetricBalancingThresholds">
      <Parameter Name="MetricName1" Value="2"/>
      <Parameter Name="MetricName2" Value="3.5"/>
    </Section>
```

via ClusterConfig.json para implantações Autônomas ou Template.json para clusters hospedados pelo Azure:

```json
"fabricSettings": [
  {
    "name": "MetricBalancingThresholds",
    "parameters": [
      {
          "name": "MetricName1",
          "value": "2"
      },
      {
          "name": "MetricName2",
          "value": "3.5"
      }
    ]
  }
]
```

<center>
![Exemplo de Limite de Balanceamento][Image1]
</center>

Neste exemplo, cada serviço está consumindo uma unidade de alguma métrica. No exemplo de superior hello, a carga máxima Olá em um nó é 5 e Olá mínimo é de dois. Digamos que Olá balanceamento limite para esta métrica é três. Desde que a taxa de saudação em cluster Olá é 5/2 = 2.5 e é inferior ao especificado de saudação balanceamento limite de três, cluster de saudação é equilibrada. Sem balanceamento é disparada quando verifica Olá Gerenciador de recursos de Cluster.

No exemplo do hello inferior, a carga máxima Olá em um nó é 10, enquanto o mínimo de saudação é dois, resultando em uma taxa de cinco. Cinco é maior que o limite de balanceamento designado Olá de três para métrica. Como resultado, uma execução rebalanceamento será agendado Avançar Olá de tempo balanceamento timer acionado. Em situações como essa alguma carga é tooNode3 normalmente distribuído. Como Olá Gerenciador de recursos de Cluster do serviço de malha não usa uma abordagem greedy, alguma carga também pode ser distribuídos tooNode2. 

<center>
![Ações de exemplo de Limite de Balanceamento][Image2]
</center>

> [!NOTE]
> O "Balanceamento" trata duas estratégias diferentes para gerenciar a carga em seu cluster. estratégia de padrão de Olá Olá usa o Gerenciador de recursos de Cluster é toodistribute carga em nós de saudação em cluster Olá. Olá outra estratégia é [desfragmentação](service-fabric-cluster-resource-manager-defragmentation-metrics.md). A desfragmentação é executada durante a saudação balanceamento mesma execução. Hello balanceamento e desfragmentação estratégias podem ser usadas para diferentes métricas em Olá mesmo cluster. Um serviço pode ter métricas de balanceamento e desfragmentação. Para métricas de desfragmentação, taxa de saudação do hello carrega em gatilhos de cluster Olá rebalanceamento quando é _abaixo_ Olá balanceamento de limite. 
>

Obtendo abaixo Olá balanceamento limite não é um objetivo explícito. Limites de Balanceamento são apenas um *gatilho*. Quando é executado de balanceamento, Olá Gerenciador de recursos de Cluster determina quais melhorias pode fazer, se houver. Só porque uma pesquisa de balanceamento é iniciada não significa que nada será movimentado. Às vezes hello cluster é toocorrect desequilibrado, mas muito restrita. Como alternativa, melhorias de saudação exigem movimentações são muito [cara](service-fabric-cluster-resource-manager-movement-cost.md)).

## <a name="activity-thresholds"></a>Limites de Atividade
Às vezes, embora nós são relativamente desequilibrados, Olá *total* quantidade de carga no cluster Olá é baixa. falta de saudação de carga pode ser um dip transitório, ou porque o cluster Olá é novo e apenas obtendo inicializar. Em ambos os casos, não convém toospend tempo balanceamento cluster Olá porque não há pouco toobe obtido. Se o cluster Olá sofreu balanceamento, você gastar rede e itens toomove recursos de computação sem fazer qualquer grande *absoluto* diferença. Move tooavoid desnecessária, há outro controle conhecido como limites de atividade. Limites de atividade permite que você toospecify alguns inferior absoluto associada para a atividade. Se nenhum nó está acima desse limite, balanceamento não é disparado mesmo se hello balanceamento limite é atingido.

Vamos supor que podemos manter nosso Limite de Balanceamento de três para essa métrica. Vamos supor também que temos um Limite de Atividade de 1536. No primeiro caso de Olá, enquanto o cluster Olá é desequilibrado por Olá balanceamento limite existe não é atende nenhum nó que esse limite de atividade, assim, nada acontece. No exemplo de inferior hello, Node1 está acima Olá limite de atividade. Como ambos Olá limite balanceamento e Olá limite de atividade de métrica de saudação são excedidos, balanceamento está agendado. Por exemplo, vamos examinar Olá diagrama a seguir: 

<center>
![Exemplo de limite de atividade][Image3]
</center>

Assim como os limites de balanceamento, limites de atividade são definidos por métrica por meio da definição de cluster hello:

ClusterManifest.xml

``` xml
    <Section Name="MetricActivityThresholds">
      <Parameter Name="Memory" Value="1536"/>
    </Section>
```

via ClusterConfig.json para implantações Autônomas ou Template.json para clusters hospedados pelo Azure:

```json
"fabricSettings": [
  {
    "name": "MetricActivityThresholds",
    "parameters": [
      {
          "name": "Memory",
          "value": "1536"
      }
    ]
  }
]
```

Limites de balanceamento e atividades são ambos métrica específica de tooa empatados - balanceamento é acionada somente se ambos Olá limite balanceamento e limite de atividade foi excedido para a saudação mesma métrica.

## <a name="balancing-services-together"></a>Balanceamento dos serviços em conjunto
Se o cluster de saudação é desequilibrado ou não é uma decisão de todo o cluster. No entanto, realizamos corrigi-lo de forma de saudação é mover instâncias ao redor e réplicas de serviço individual. Isso faz sentido, certo? Se a memória é empilhada em um nó, várias réplicas ou instâncias podem estar contribuindo tooit. Corrigindo desequilíbrio de saudação pode exigir a movimentação de qualquer uma das réplicas com monitoração de estado hello ou instâncias sem monitoração de estado que usam métrica desequilibrados hello.

Ocasionalmente, no entanto, um serviço que não estava em si desequilibrados foi movido (Lembre-se de discussão de saudação do local e global pondera anteriormente). Por que um serviço é movido quando todas as métricas desse serviço foram balanceadas? Vejamos um exemplo:

- Vamos supor que há quatro serviços, Service1, Service2, Service3 e Service4. 
- O Service1 relata as métricas Metric1 e Metric2. 
- O Service2 relata as métricas Metric2 e Metric3. 
- O Service3 relata as métricas Metric3 e Metric4.
- O Service4 relata a métrica Metric99. 

Certamente, você consegue ver onde queremos chegar: há uma cadeia! Realmente, não há quatro serviços independentes. Temos três serviços relacionados e um que está por conta própria.

<center>
![Balanceamento dos serviços em conjunto][Image4]
</center>

Devido a essa cadeia, é possível que um desequilíbrio em métricas de 1 a 4 pode causar réplicas ou as instâncias do tooservices toomove de 1 a 3 ao redor. Também sabemos que um desequilíbrio nas métricas de 1, 2 ou 3 não pode causar movimentos no Service4. Não deve haver nenhum ponto de mudança réplicas hello ou instâncias do tooService4 ao redor pode fazem absolutamente nada tooimpact saldo de saudação de métricas de 1 a 3.

Olá Gerenciador de recursos de Cluster automaticamente descobre quais serviços estão relacionados. Adição, remoção ou alteração métricas Olá para serviços podem afetar suas relações. Por exemplo, entre duas execuções de balanceamento gratuito2 pode ter sido o tooremove atualizado Metric2. Isso quebra a cadeia de saudação entre Service1 e gratuito2. Agora, em vez de dois grupos de serviços relacionados, há três:

<center>
![Balanceamento dos serviços em conjunto][Image5]
</center>

## <a name="next-steps"></a>Próximas etapas
* Métricas são como Olá Gerenciador de recursos de Cluster do serviço de malha gerencia capacidade em cluster hello e consumo. toolearn mais sobre as métricas e como tooconfigure-los, confira [neste artigo](service-fabric-cluster-resource-manager-metrics.md)
* O custo de movimento é uma forma de sinalização toohello Gerenciador de recursos de Cluster que determinados serviços são toomove mais caro do que outros. Para obter mais informações sobre o custo de movimento, consulte muito[neste artigo](service-fabric-cluster-resource-manager-movement-cost.md)
* Olá Gerenciador de recursos de Cluster tem várias limitações que você pode configurar tooslow para baixo da variação no cluster hello. Normalmente, eles não são necessários, mas você poderá aprender mais sobre eles [aqui](service-fabric-cluster-resource-manager-advanced-throttling.md)

[Image1]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resrouce-manager-balancing-thresholds.png
[Image2]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-threshold-triggered-results.png
[Image3]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-activity-thresholds.png
[Image4]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together1.png
[Image5]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together2.png
