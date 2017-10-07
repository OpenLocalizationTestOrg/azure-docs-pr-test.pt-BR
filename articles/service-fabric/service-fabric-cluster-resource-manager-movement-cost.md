---
title: 'Gerenciador de Recursos de Cluster do Service Fabric: custo de movimento | Microsoft Docs'
description: "Visão geral do custo dos movimentos de serviços do Service Fabric"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f022f258-7bc0-4db4-aa85-8c6c8344da32
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 65d4ac73efffcf7b25b1e95da6f9012a9238cb75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-movement-cost"></a>Custo do movimentação de serviços
Um fator que Olá Gerenciador de recursos de Cluster do serviço de malha considera ao tentar toodetermine o cluster de tooa toomake alterações é o custo de saudação essas alterações. noção de saudação de "custo" foi negociada desativado em cluster quanto Olá pode ser melhorado. O custo é considerado ao mover serviços para balanceamento, desfragmentação e outros requisitos. meta de saudação é toomeet requisitos Olá Olá forma menos de interrupção ou cara. 

Movimentar serviços custa, no mínimo, tempo de CPU e largura de banda de rede. Para serviços com monitoração de estado, ele exige copiando estado Olá desses serviços, consumo de disco e memória adicional. Minimizar os custos de saudação de soluções que Olá Gerenciador de recursos de Cluster do Azure Service Fabric é fornecido com ajuda a garantir que os recursos do cluster Olá não são gastou desnecessariamente. No entanto, você também não quiser tooignore soluções que podem melhorar significativamente o alocação Olá de recursos em cluster hello.

Olá Gerenciador de recursos de Cluster tem duas formas de custos de computação e limitando-los enquanto ele tenta toomanage cluster de saudação. mecanismo primeiro Olá simplesmente está contando a cada mudança que seria. Se duas soluções são geradas com sobre Olá mesmo saldo (pontuação), em seguida, Olá Gerenciador de recursos de Cluster prefere Olá um com hello custo mais baixo (número total de movimentações).

Esta estratégia funciona bem. Mas, como ocorre com cargas estáticas ou padrão, é improvável em qualquer sistema complexo que todas as mudanças sejam iguais. Alguns são provavelmente toobe muito mais caro.

## <a name="setting-move-costs"></a>Definindo custos de movimentação 
Você pode especificar o custo de mudança saudação padrão para um serviço quando ele é criado:

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -DefaultMoveCost Medium
```

C#: 

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
//set up hello rest of hello ServiceDescription
serviceDescription.DefaultMoveCost = MoveCost.Medium;
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

Você também pode especificar ou atualizar MoveCost dinamicamente de um serviço após a criação do serviço de saudação: 

PowerShell: 

```posh
Update-ServiceFabricService -Stateful -ServiceName "fabric:/AppName/ServiceName" -DefaultMoveCost High
```

C#:

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.DefaultMoveCost = MoveCost.High;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/AppName/ServiceName"), updateDescription);
```

## <a name="dynamically-specifying-move-cost-on-a-per-replica-basis"></a>Especificando dinamicamente o custo de movimentação por réplica

Olá trechos de código anteriores são todos para especificar MoveCost para um serviço todo uma vez do próprio serviço Olá externa. No entanto, mover o custo é mais útil é quando muda de custo de mudança de saudação de um objeto de serviço específico com o seu tempo de vida. Como Olá serviços próprios provavelmente ter ideia melhor de saudação de cara como eles são toomove um determinado momento, há uma API para serviços tooreport seu próprios Mover individual de custo durante o tempo de execução. 

C#:

```csharp
this.Partition.ReportMoveCost(MoveCost.Medium);
```

## <a name="impact-of-move-cost"></a>Impacto do custo de movimentação
O MoveCost tem quatro níveis: Zero, Baixo, Médio e Alto. MoveCosts são relativo tooeach outro, com exceção de Zero. Custo zero move significa que o movimento é gratuito e não deve contar com pontuação de saudação de solução de saudação. Configuração da mudança custo tooHigh *não* garante que a réplica Olá permanece em um único local.

<center>
![O custo de movimentação como um fator na seleção de réplicas para movimentação][Image1]
</center>

MoveCost ajuda você a encontrar soluções Olá que causa Olá geral o mínimo de interrupções e é tooachieve mais fácil ao mesmo tempo, ainda que chegam ao saldo equivalente. Noção de um serviço de custo pode ser relativo toomany coisas. Olá fatores mais comuns para calcular o custo de movimento são:

- saudação de estado ou dados Olá serviço tem toomove.
- custo de saudação de desconexão de clientes. Mover uma réplica primária é geralmente mais caro do que o custo de saudação da movimentação de uma réplica secundária.
- custo de saudação de interromper uma operação em andamento. Nível de armazenamento de algumas operações em dados saudação ou operações executadas na chamada de cliente tooa resposta são caras. Após um certo ponto, você não deseja toostop-los, se você não precisa. Portanto enquanto a operação de saudação está acontecendo, aumentar custo de mudança de saudação de probabilidade Olá de tooreduce de objeto este serviço que ele se move. Quando a operação de saudação é feita, você pode definir Olá custo back toonormal.

## <a name="enabling-move-cost-in-your-cluster"></a>Habilitando o custo de movimentação em seu cluster
Para que hello mais granular toobe MoveCosts levada em conta, MoveCost deverá ser habilitada no cluster. Sem essa configuração, modo padrão de saudação de movimentações de contagem é usado para calcular MoveCost e MoveCost relatórios serão ignorados.


ClusterManifest.xml:

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="UseMoveCostReports" Value="true" />
        </Section>
```

via ClusterConfig.json para implantações autônomas ou Template.json para clusters hospedados pelo Azure:

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "UseMoveCostReports",
          "value": "true"
      }
    ]
  }
]
```

## <a name="next-steps"></a>Próximas etapas
- Gerenciador de recursos de Cluster do serviço de malha usa o consumo de toomanage de métricas e a capacidade em cluster hello. toolearn mais sobre as métricas e como tooconfigure-los, confira [consumo de recursos de gerenciamento e de carga na malha do serviço com métricas](service-fabric-cluster-resource-manager-metrics.md).
- toolearn sobre como Olá Gerenciador de recursos de Cluster gerencia e equilibra a carga no cluster Olá, confira [sua malha do serviço de cluster de balanceamento](service-fabric-cluster-resource-manager-balancing.md).

[Image1]:./media/service-fabric-cluster-resource-manager-movement-cost/service-most-cost-example.png
