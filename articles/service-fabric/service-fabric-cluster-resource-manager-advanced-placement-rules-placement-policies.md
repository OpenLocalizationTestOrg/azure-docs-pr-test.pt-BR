---
title: "aaaService Gerenciador de recursos de Cluster de malha - políticas de posicionamento | Microsoft Docs"
description: "Visão geral das políticas de posicionamento adicionais e das regras para os Serviços do Service Fabric"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 5c2d19c6-dd40-4c4b-abd3-5c5ec0abed38
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: bb58642520085ab3000f3929cf9aea7a8f6e3070
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="placement-policies-for-service-fabric-services"></a>Políticas de posicionamento para serviços do Service Fabric
Políticas de posicionamento são regras adicionais que podem ser usados toogovern posicionamento do serviço em alguns cenários específicos, menos comuns. Alguns exemplos desses cenários são:

- O cluster do Service Fabric engloba distâncias geográficas, como vários datacenters locais ou regiões do Azure
- Seu ambiente abrange várias áreas de controle geopolíticas ou legal ou algum outro caso em que os limites de política você precisa tooenforce
- Há considerações de desempenho ou a latência de comunicação devido distâncias toolarge ou o uso de links de rede mais lento ou menos confiável
- Você precisa tookeep determinada cargas de trabalho colocada como um melhor esforço, com outras cargas de trabalho ou em proximidade toocustomers

A maioria desses requisitos alinha com o layout físico de saudação do cluster hello, representado como Olá domínios de falha de cluster de saudação. 

Olá avançadas de políticas de posicionamento que ajudam a solucionar que esses cenários são:

1. Domínios inválidos
2. Domínios necessários
3. Domínios preferenciais
4. Desativação de empacotamento de réplica

A maioria das Olá controles a seguir pode ser configurada por meio de propriedades de nó e restrições de posicionamento, mas alguns são mais complicados. coisas toomake mais simples, Olá Gerenciador de recursos de Cluster do serviço de malha fornece essas políticas de posicionamento adicional. As políticas de posicionamento são configuradas de acordo com uma instância de serviço nomeada. Elas também podem ser atualizadas dinamicamente.

## <a name="specifying-invalid-domains"></a>Especificando domínios inválidos
Olá **InvalidDomain** posicionamento política permite que você toospecify que um determinado domínio de falha é inválido para um serviço específico. Essa política garante que um serviço específico nunca seja executado em uma determinada área, por exemplo, por motivos de política corporativa ou geopolíticos. Vários domínios inválidos podem ser especificados através de diferentes políticas.

<center>
![Exemplo de domínio inválido][Image1]
</center>

Código:

```csharp
ServicePlacementInvalidDomainPolicyDescription invalidDomain = new ServicePlacementInvalidDomainPolicyDescription();
invalidDomain.DomainName = "fd:/DCEast"; //regulations prohibit this workload here
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("InvalidDomain,fd:/DCEast”)
```
## <a name="specifying-required-domains"></a>Especificando domínios necessários
Olá necessário política de substituição de domínio requer que o serviço de saudação está presente somente no domínio especificado hello. Vários domínios necessários podem ser especificados através de diferentes políticas.

<center>
![Exemplo de domínio necessário][Image2]
</center>

Código:

```csharp
ServicePlacementRequiredDomainPolicyDescription requiredDomain = new ServicePlacementRequiredDomainPolicyDescription();
requiredDomain.DomainName = "fd:/DC01/RK03/BL2";
serviceDescription.PlacementPolicies.Add(requiredDomain);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomain,fd:/DC01/RK03/BL2")
```

## <a name="specifying-a-preferred-domain-for-hello-primary-replicas-of-a-stateful-service"></a>Especificar um domínio preferencial para réplicas primárias de saudação de um serviço com monitoração de estado
Domínio primário preferencial Hello Especifica tooplace de domínio de falha de Olá Olá principal no. Olá primário termina nesse domínio quando tudo está íntegro. Se domínio Olá ou a réplica primária Olá falha ou desligado, Olá primário move toosome outro local, idealmente em Olá mesmo domínio. Se o novo local não está no domínio preferencial hello, Olá Gerenciador de recursos de Cluster move-o novamente domínio preferencial toohello assim que possível. Obviamente, essa configuração só faz sentido para serviços com estado. Essa política é mais útil em clusters que estão distribuídos em regiões do Azure ou em vários datacenters, mas têm serviços que preferem o posicionamento em um determinado local. Mantendo primárias fechar tootheir usuários ou outros serviços ajuda a fornecer a latência mais baixa, especialmente para leituras, que são tratadas por primários por padrão.

<center>
![Domínios primários preferenciais e failover][Image3]
</center>

```csharp
ServicePlacementPreferPrimaryDomainPolicyDescription primaryDomain = new ServicePlacementPreferPrimaryDomainPolicyDescription();
primaryDomain.DomainName = "fd:/EastUS/";
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("PreferredPrimaryDomain,fd:/EastUS")
```

## <a name="requiring-replica-distribution-and-disallowing-packing"></a>Exigindo a distribuição de réplica e desabilitando o empacotamento
As réplicas são _normalmente_ distribuídos entre domínios de falha e atualização quando Olá cluster está íntegro. No entanto, há casos em que mais de uma réplica para uma determinada partição podem acabar temporariamente empacotadas em uma único domínio. Por exemplo, digamos que esse cluster Olá tem nove nós em três domínios de falha, fd: 0, fd: / 1 e fd: / 2. Digamos também que o serviço tem três réplicas. Digamos que Olá nós que estavam sendo usados para as réplicas no fd: / 1 e fd: / 2 foi desativado. Normalmente, Olá Gerenciador de recursos de Cluster prefere outros nós os mesmos domínios de falha. Nesse caso, vamos supor que devido a problemas de toocapacity nenhum da saudação outros nós nesses domínios eram válidos. Se Olá Gerenciador de recursos de Cluster de compilações de substituições para essas réplicas, ele teria toochoose nós fd: 0. No entanto, fazer _que_ criará uma situação onde Olá restrição de domínio de falha for violada. Aumenta de réplicas de remessa chance de Olá Olá conjunto inteiro de réplica pode ir para baixo ou serão perdidos. 

> [!NOTE]
> Para obter mais informações sobre restrições e prioridades de restrições em geral, confira [este tópico](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).
>

Se você já viu uma mensagem de integridade, como "`hello Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating hello Constraint: FaultDomain`", você atingiu essa condição ou algo parecido. Normalmente, apenas uma ou duas réplicas são empacotadas juntas temporariamente. Enquanto houver menos de um quorum de réplicas em um determinado domínio, você estará seguro. Remessa é rara, mas isso pode acontecer e geralmente essas situações são transitórias como nós de saudação voltar. Se nós Olá fiquem para baixo e Olá Gerenciador de recursos de Cluster precisa toobuild substituições, geralmente há outros nós disponíveis em domínios de falha ideal de saudação.

Algumas cargas de trabalho prefere ter sempre o número de destino de saudação de réplicas, mesmo se eles são incluídos em menos domínios. Essas cargas de trabalho apostam contra falhas de domínio permanentes simultâneas totais e normalmente podem recuperar o estado local. Outras cargas de trabalho em vez disso, seriam necessário tempo de inatividade Olá anteriores a exatidão de risco ou perda de dados. A maioria das cargas de trabalho de produção é executada com mais de três réplicas, mais de três domínios de falha e muitos nós válidos por domínio de falha. Por isso, comportamento padrão de saudação permite que a remessa de domínio por padrão. saudação padrão comportamento permite que balanceamento normal e failover toohandle esses casos extremos, mesmo que isso significa que o empacotamento de domínio temporário.

Se você quiser toodisable tal remessa para uma determinada carga de trabalho, você pode especificar Olá `RequireDomainDistribution` política no serviço de saudação. Quando essa política está definida, Olá Gerenciador de recursos de Cluster garante que não existam duas réplicas da mesma partição executados em Olá mesmo falha ou domínio de atualização de saudação.

Código:

```csharp
ServicePlacementRequireDomainDistributionPolicyDescription distributeDomain = new ServicePlacementRequireDomainDistributionPolicyDescription();
serviceDescription.PlacementPolicies.Add(distributeDomain);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomainDistribution")
```

Agora, é que ele seja possível toouse essas configurações para serviços em um cluster que não foi estendido geograficamente? Seria, mas também não há um bom motivo para isso. Hello configurações de domínio necessários, inválido e preferencial devem ser evitadas, a menos que exigem cenários Olá-los. Não faz qualquer tooforce de tootry sentido toorun uma determinada carga de trabalho em um único rack ou tooprefer algum segmento do cluster em detrimento de outro local. Diferentes configurações de hardware devem ser distribuídas entre domínios de falha e manipuladas por propriedades de nó e restrições de posicionamento normais.

## <a name="next-steps"></a>Próximas etapas
- Para saber mais sobre como configurar os serviços, [Saiba mais sobre como configurar serviços](service-fabric-cluster-resource-manager-configure-services.md)

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-invalid-placement-domain.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-required-placement-domain.png
[Image3]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-preferred-primary-domain.png
