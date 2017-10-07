---
title: "Governança de recursos de malha do serviço para contêineres e os serviços de aaaAzure | Microsoft Docs"
description: "Malha do serviço do Azure permite que você toospecify limites de recursos para serviços executados dentro ou fora contêineres."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 34e368211d98ff6b5b294c9c8b3af5ca30eeb20c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-governance"></a>Governança de recursos 

Quando a execução de vários serviços em hello mesmo nó ou cluster, é possível que um serviço pode consumir mais recursos privar outros serviços. Esse problema é chamado tooas Olá vizinho barulhento. Service Fabric permite Olá desenvolvedor toospecify as reservas e limites por recursos de tooguarantee de serviço e também limitar o uso de recursos. 

## <a name="resource-governance-metrics"></a>Métricas de governança de recursos 

Há suporte para a governança de recursos no Service Fabric por [Pacote de Serviço](service-fabric-application-model.md). recursos de saudação que são atribuídos tooService pacote podem ser divididos entre os pacotes de código. limites de recurso Olá especificados também significam reserva Olá dos recursos de saudação. O Service Fabric dá suporte à especificação de CPU e Memória por pacote de serviço, usando duas [métricas](service-fabric-cluster-resource-manager-metrics.md) internas:

* CPU (nome da métrica `ServiceFabric:/_CpuCores`): um núcleo é um núcleo lógico que está disponível na máquina de host hello e todos os núcleos em todos os nós são ponderados Olá mesmo.
* Memória (nome da métrica `ServiceFabric:/_MemoryInMB`): memória é expressa em megabytes, e ele mapeia toophysical memória disponível no computador de saudação.

Somente as garantias de reserva flexível são fornecidas - tempo de execução de saudação rejeita a abertura de um novo serviço de recursos de pacotes disponíveis são excedidos. No entanto, se outro executável ou contêiner é colocado no nó hello, que possam violar garantias de reserva Olá original.

Para essas duas métricas, Olá [Gerenciador de recursos de Cluster](service-fabric-cluster-resource-manager-cluster-description.md) controla a capacidade total do cluster, Olá carga em cada nó no cluster Olá, e restantes recursos no cluster hello. Essas duas métricas é equivalente tooany outro usuário ou a métrica personalizada e todos os recursos existentes podem ser usados com eles:
* Cluster pode ser [balanceada](service-fabric-cluster-resource-manager-balancing.md) de acordo com as métricas de toothese dois (comportamento padrão).
* Cluster pode ser [desfragmentados](service-fabric-cluster-resource-manager-defragmentation-metrics.md) de acordo com as métricas de toothese dois.
* Ao [descrever um cluster](service-fabric-cluster-resource-manager-cluster-description.md), a capacidade armazenada em buffer pode ser definida para essas duas métricas.

Não há suporte para [relatórios de cargas dinâmicas](service-fabric-cluster-resource-manager-metrics.md) nessas métricas e as cargas dessas métricas são definidas no momento da criação.

## <a name="cluster-set-up-for-enabling-resource-governance"></a>Configuração de cluster para habilitar a governança de recursos

Capacidade deve ser definida manualmente em cada tipo de nó no cluster de saudação da seguinte maneira:

```xml
    <NodeType Name="MyNodeType">
      <Capacities>
        <Capacity Name="ServiceFabric:/_CpuCores" Value="4"/>
        <Capacity Name="ServiceFabric:/_MemoryInMB" Value="2048"/>
      </Capacities>
    </NodeType>
```
 
A governança de recursos é permitida somente em serviços do usuário e não em qualquer serviço do sistema. Ao especificar a capacidade, alguns núcleos e uma parte da memória devem ser deixados não alocados para serviços do sistema. Para otimizar o desempenho, Olá configuração a seguir deve também ser ativado no manifesto do cluster hello: 

```xml
<Section Name="PlacementAndLoadBalancing">
    <Parameter Name="PreventTransientOvercommit" Value="true" /> 
    <Parameter Name="AllowConstraintCheckFixesDuringApplicationUpgrade" Value="true" />
</Section>
```


## <a name="specifying-resource-governance"></a>Especificando a governança de recursos 

Limites de governança de recursos são especificados no manifesto de aplicativo hello (seção servicemanifestimport ao) conforme mostrado no exemplo a seguir de saudação:

```xml
<?xml version='1.0' encoding='UTF-8'?>
<ApplicationManifest ApplicationTypeName='TestAppTC1' ApplicationTypeVersion='vTC1' xsi:schemaLocation='http://schemas.microsoft.com/2011/01/fabric ServiceFabricServiceModel.xsd' xmlns='http://schemas.microsoft.com/2011/01/fabric' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance'>
  <Parameters>
  </Parameters>
  <!--
  ServicePackageA has hello number of CPU cores defined, but doesn't have hello MemoryInMB defined.
  In this case, Service Fabric will sum hello limits on code packages and uses hello sum as 
  hello overall ServicePackage limit.
  -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName='ServicePackageA' ServiceManifestVersion='v1'/>
    <Policies>
      <ServicePackageResourceGovernancePolicy CpuCores="1"/>
      <ResourceGovernancePolicy CodePackageRef="CodeA1" CpuShares="512" MemoryInMB="1000" />
      <ResourceGovernancePolicy CodePackageRef="CodeA2" CpuShares="256" MemoryInMB="1000" />
    </Policies>
  </ServiceManifestImport>
```
  
Neste exemplo, o pacote de serviço ServicePackageA obtém um núcleo em nós Olá onde ele é colocado. Este pacote de serviço contém dois pacotes de código (CodeA1 e CodeA2) e especificar Olá `CpuShares` parâmetro. proporção de saudação do CpuShares 512:256 divide core Olá entre os dois pacotes de código hello. Portanto, neste exemplo, CodeA1 obtém dois terços de um núcleo e CodeA2 obtém um terço de um núcleo (e uma reserva de garantia de software de Olá mesmo). No caso de quando CpuShares não são especificados para os pacotes de código, o Service Fabric divide núcleos Olá igualmente entre eles.

Limites de memória serão absolutos, ambos os pacotes de código são limitados too1024 MB de memória (e uma reserva de garantia de software de Olá mesmo). Pacotes de código (contêineres ou processos) não são tooallocate capaz de mais memória do que esse limite e tentar toodo pode resultar em uma exceção de falta de memória. Para toowork de imposição de limite de recursos, todos os pacotes de código dentro de um pacote de serviço devem ter limites de memória especificados.


## <a name="next-steps"></a>Próximas etapas
* toolearn mais sobre o recurso Gerenciador de Cluster, leia este [artigo](service-fabric-cluster-resource-manager-introduction.md).
* toolearn mais sobre o modelo de aplicativo, pacotes de serviço, os pacotes de código e como réplicas mapeiam toothem ler este [artigo](service-fabric-application-model.md).
