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
# <a name="resource-governance"></a><span data-ttu-id="65329-103">Governança de recursos</span><span class="sxs-lookup"><span data-stu-id="65329-103">Resource governance</span></span> 

<span data-ttu-id="65329-104">Quando a execução de vários serviços em hello mesmo nó ou cluster, é possível que um serviço pode consumir mais recursos privar outros serviços.</span><span class="sxs-lookup"><span data-stu-id="65329-104">When running multiple services on hello same node or cluster, it is possible that one service might consume more resources starving other services.</span></span> <span data-ttu-id="65329-105">Esse problema é chamado tooas Olá vizinho barulhento.</span><span class="sxs-lookup"><span data-stu-id="65329-105">This problem is referred tooas hello noisy-neighbor problem.</span></span> <span data-ttu-id="65329-106">Service Fabric permite Olá desenvolvedor toospecify as reservas e limites por recursos de tooguarantee de serviço e também limitar o uso de recursos.</span><span class="sxs-lookup"><span data-stu-id="65329-106">Service Fabric allows hello developer toospecify reservations and limits per service tooguarantee resources and also limit its resource usage.</span></span> 

## <a name="resource-governance-metrics"></a><span data-ttu-id="65329-107">Métricas de governança de recursos</span><span class="sxs-lookup"><span data-stu-id="65329-107">Resource governance metrics</span></span> 

<span data-ttu-id="65329-108">Há suporte para a governança de recursos no Service Fabric por [Pacote de Serviço](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="65329-108">Resource governance is supported in Service Fabric per [Service Package](service-fabric-application-model.md).</span></span> <span data-ttu-id="65329-109">recursos de saudação que são atribuídos tooService pacote podem ser divididos entre os pacotes de código.</span><span class="sxs-lookup"><span data-stu-id="65329-109">hello resources that are assigned tooService Package can be further divided between code packages.</span></span> <span data-ttu-id="65329-110">limites de recurso Olá especificados também significam reserva Olá dos recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="65329-110">hello resource limits specified also mean hello reservation of hello resources.</span></span> <span data-ttu-id="65329-111">O Service Fabric dá suporte à especificação de CPU e Memória por pacote de serviço, usando duas [métricas](service-fabric-cluster-resource-manager-metrics.md) internas:</span><span class="sxs-lookup"><span data-stu-id="65329-111">Service Fabric supports specifying CPU and Memory per service package, using two built-in [metrics](service-fabric-cluster-resource-manager-metrics.md):</span></span>

* <span data-ttu-id="65329-112">CPU (nome da métrica `ServiceFabric:/_CpuCores`): um núcleo é um núcleo lógico que está disponível na máquina de host hello e todos os núcleos em todos os nós são ponderados Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="65329-112">CPU (metric name `ServiceFabric:/_CpuCores`): A core is a logical core that is available on hello host machine, and all cores across all nodes are weighted hello same.</span></span>
* <span data-ttu-id="65329-113">Memória (nome da métrica `ServiceFabric:/_MemoryInMB`): memória é expressa em megabytes, e ele mapeia toophysical memória disponível no computador de saudação.</span><span class="sxs-lookup"><span data-stu-id="65329-113">Memory (metric name `ServiceFabric:/_MemoryInMB`): Memory is expressed in megabytes, and it maps toophysical memory that is available on hello machine.</span></span>

<span data-ttu-id="65329-114">Somente as garantias de reserva flexível são fornecidas - tempo de execução de saudação rejeita a abertura de um novo serviço de recursos de pacotes disponíveis são excedidos.</span><span class="sxs-lookup"><span data-stu-id="65329-114">Only soft reservation guarantees are provided - hello runtime rejects opening of new service packages available resources are exceeded.</span></span> <span data-ttu-id="65329-115">No entanto, se outro executável ou contêiner é colocado no nó hello, que possam violar garantias de reserva Olá original.</span><span class="sxs-lookup"><span data-stu-id="65329-115">However, if another executable or container is placed on hello node, that may violate hello original reservation guarantees.</span></span>

<span data-ttu-id="65329-116">Para essas duas métricas, Olá [Gerenciador de recursos de Cluster](service-fabric-cluster-resource-manager-cluster-description.md) controla a capacidade total do cluster, Olá carga em cada nó no cluster Olá, e restantes recursos no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="65329-116">For these two metrics, hello [Cluster Resource Manager](service-fabric-cluster-resource-manager-cluster-description.md) tracks total cluster capacity, hello load on each node in hello cluster, and, remaining resources in hello cluster.</span></span> <span data-ttu-id="65329-117">Essas duas métricas é equivalente tooany outro usuário ou a métrica personalizada e todos os recursos existentes podem ser usados com eles:</span><span class="sxs-lookup"><span data-stu-id="65329-117">These two metrics are equivalent tooany other user or custom metric and all existing features can be used with them:</span></span>
* <span data-ttu-id="65329-118">Cluster pode ser [balanceada](service-fabric-cluster-resource-manager-balancing.md) de acordo com as métricas de toothese dois (comportamento padrão).</span><span class="sxs-lookup"><span data-stu-id="65329-118">Cluster can be [balanced](service-fabric-cluster-resource-manager-balancing.md) according toothese two metrics (default behavior).</span></span>
* <span data-ttu-id="65329-119">Cluster pode ser [desfragmentados](service-fabric-cluster-resource-manager-defragmentation-metrics.md) de acordo com as métricas de toothese dois.</span><span class="sxs-lookup"><span data-stu-id="65329-119">Cluster can be [defragmented](service-fabric-cluster-resource-manager-defragmentation-metrics.md) according toothese two metrics.</span></span>
* <span data-ttu-id="65329-120">Ao [descrever um cluster](service-fabric-cluster-resource-manager-cluster-description.md), a capacidade armazenada em buffer pode ser definida para essas duas métricas.</span><span class="sxs-lookup"><span data-stu-id="65329-120">When [describing a cluster](service-fabric-cluster-resource-manager-cluster-description.md), buffered capacity can be set for these two metrics.</span></span>

<span data-ttu-id="65329-121">Não há suporte para [relatórios de cargas dinâmicas](service-fabric-cluster-resource-manager-metrics.md) nessas métricas e as cargas dessas métricas são definidas no momento da criação.</span><span class="sxs-lookup"><span data-stu-id="65329-121">[Dynamic load reporting](service-fabric-cluster-resource-manager-metrics.md) is not supported for these metrics, and loads for these metrics are defined at creation time.</span></span>

## <a name="cluster-set-up-for-enabling-resource-governance"></a><span data-ttu-id="65329-122">Configuração de cluster para habilitar a governança de recursos</span><span class="sxs-lookup"><span data-stu-id="65329-122">Cluster set up for enabling resource governance</span></span>

<span data-ttu-id="65329-123">Capacidade deve ser definida manualmente em cada tipo de nó no cluster de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="65329-123">Capacity should be defined manually in each node type in hello cluster as follows:</span></span>

```xml
    <NodeType Name="MyNodeType">
      <Capacities>
        <Capacity Name="ServiceFabric:/_CpuCores" Value="4"/>
        <Capacity Name="ServiceFabric:/_MemoryInMB" Value="2048"/>
      </Capacities>
    </NodeType>
```
 
<span data-ttu-id="65329-124">A governança de recursos é permitida somente em serviços do usuário e não em qualquer serviço do sistema.</span><span class="sxs-lookup"><span data-stu-id="65329-124">Resource governance is allowed only on user services and not on any system services.</span></span> <span data-ttu-id="65329-125">Ao especificar a capacidade, alguns núcleos e uma parte da memória devem ser deixados não alocados para serviços do sistema.</span><span class="sxs-lookup"><span data-stu-id="65329-125">When specifying capacity, some cores and memory must be left unallocated for system services.</span></span> <span data-ttu-id="65329-126">Para otimizar o desempenho, Olá configuração a seguir deve também ser ativado no manifesto do cluster hello:</span><span class="sxs-lookup"><span data-stu-id="65329-126">For optimal performance, hello following setting should also be turned on in hello cluster manifest:</span></span> 

```xml
<Section Name="PlacementAndLoadBalancing">
    <Parameter Name="PreventTransientOvercommit" Value="true" /> 
    <Parameter Name="AllowConstraintCheckFixesDuringApplicationUpgrade" Value="true" />
</Section>
```


## <a name="specifying-resource-governance"></a><span data-ttu-id="65329-127">Especificando a governança de recursos</span><span class="sxs-lookup"><span data-stu-id="65329-127">Specifying resource governance</span></span> 

<span data-ttu-id="65329-128">Limites de governança de recursos são especificados no manifesto de aplicativo hello (seção servicemanifestimport ao) conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="65329-128">Resource governance limits are specified in hello application manifest (ServiceManifestImport section) as shown in hello following example:</span></span>

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
  
<span data-ttu-id="65329-129">Neste exemplo, o pacote de serviço ServicePackageA obtém um núcleo em nós Olá onde ele é colocado.</span><span class="sxs-lookup"><span data-stu-id="65329-129">In this example, service package ServicePackageA gets one core on hello nodes where it is placed.</span></span> <span data-ttu-id="65329-130">Este pacote de serviço contém dois pacotes de código (CodeA1 e CodeA2) e especificar Olá `CpuShares` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="65329-130">This service package contains two code packages (CodeA1 and CodeA2), and both specify hello `CpuShares` parameter.</span></span> <span data-ttu-id="65329-131">proporção de saudação do CpuShares 512:256 divide core Olá entre os dois pacotes de código hello.</span><span class="sxs-lookup"><span data-stu-id="65329-131">hello proportion of CpuShares 512:256  divides hello core across hello two code packages.</span></span> <span data-ttu-id="65329-132">Portanto, neste exemplo, CodeA1 obtém dois terços de um núcleo e CodeA2 obtém um terço de um núcleo (e uma reserva de garantia de software de Olá mesmo).</span><span class="sxs-lookup"><span data-stu-id="65329-132">Thus, in this example, CodeA1 gets two-thirds of a core, and  CodeA2 gets one-third of a core (and a soft-guarantee reservation of hello same).</span></span> <span data-ttu-id="65329-133">No caso de quando CpuShares não são especificados para os pacotes de código, o Service Fabric divide núcleos Olá igualmente entre eles.</span><span class="sxs-lookup"><span data-stu-id="65329-133">In case when CpuShares are not specified for code packages, Service Fabric divides hello cores equally among them.</span></span>

<span data-ttu-id="65329-134">Limites de memória serão absolutos, ambos os pacotes de código são limitados too1024 MB de memória (e uma reserva de garantia de software de Olá mesmo).</span><span class="sxs-lookup"><span data-stu-id="65329-134">Memory limits are absolute, so both code packages are limited too1024 MB of memory (and a soft-guarantee reservation of hello same).</span></span> <span data-ttu-id="65329-135">Pacotes de código (contêineres ou processos) não são tooallocate capaz de mais memória do que esse limite e tentar toodo pode resultar em uma exceção de falta de memória.</span><span class="sxs-lookup"><span data-stu-id="65329-135">Code packages (containers or processes) are not able tooallocate more memory than this limit, and attempting toodo so results in an out-of-memory exception.</span></span> <span data-ttu-id="65329-136">Para toowork de imposição de limite de recursos, todos os pacotes de código dentro de um pacote de serviço devem ter limites de memória especificados.</span><span class="sxs-lookup"><span data-stu-id="65329-136">For resource limit enforcement toowork, all code packages within a service package should have memory limits specified.</span></span>


## <a name="next-steps"></a><span data-ttu-id="65329-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="65329-137">Next steps</span></span>
* <span data-ttu-id="65329-138">toolearn mais sobre o recurso Gerenciador de Cluster, leia este [artigo](service-fabric-cluster-resource-manager-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="65329-138">toolearn more about Cluster Resource Manager, read this [article](service-fabric-cluster-resource-manager-introduction.md).</span></span>
* <span data-ttu-id="65329-139">toolearn mais sobre o modelo de aplicativo, pacotes de serviço, os pacotes de código e como réplicas mapeiam toothem ler este [artigo](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="65329-139">toolearn more about application model, service packages, code packages and how replicas map toothem read this [article](service-fabric-application-model.md).</span></span>
