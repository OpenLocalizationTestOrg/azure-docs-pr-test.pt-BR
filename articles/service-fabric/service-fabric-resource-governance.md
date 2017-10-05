---
title: "Governança de recursos do Azure Service Fabric para contêineres e serviços | Microsoft Docs"
description: "O Azure Service Fabric permite especificar os limites de recurso para os serviços executados dentro ou fora de contêineres."
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
ms.openlocfilehash: 88d44953ad83f9e7401fd087a39842e4a3790124
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="resource-governance"></a><span data-ttu-id="ee256-103">Governança de recursos</span><span class="sxs-lookup"><span data-stu-id="ee256-103">Resource governance</span></span> 

<span data-ttu-id="ee256-104">Ao executar vários serviços no mesmo nó ou cluster, é possível que um serviço consuma mais recursos, privando outros serviços.</span><span class="sxs-lookup"><span data-stu-id="ee256-104">When running multiple services on the same node or cluster, it is possible that one service might consume more resources starving other services.</span></span> <span data-ttu-id="ee256-105">Esse problema é conhecido como o problema do vizinho barulhento.</span><span class="sxs-lookup"><span data-stu-id="ee256-105">This problem is referred to as the noisy-neighbor problem.</span></span> <span data-ttu-id="ee256-106">O Service Fabric permite que o desenvolvedor especifique reservas e limites por serviço para garantir recursos e também limitar seu uso de recursos.</span><span class="sxs-lookup"><span data-stu-id="ee256-106">Service Fabric allows the developer to specify reservations and limits per service to guarantee resources and also limit its resource usage.</span></span> 

## <a name="resource-governance-metrics"></a><span data-ttu-id="ee256-107">Métricas de governança de recursos</span><span class="sxs-lookup"><span data-stu-id="ee256-107">Resource governance metrics</span></span> 

<span data-ttu-id="ee256-108">Há suporte para a governança de recursos no Service Fabric por [Pacote de Serviço](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="ee256-108">Resource governance is supported in Service Fabric per [Service Package](service-fabric-application-model.md).</span></span> <span data-ttu-id="ee256-109">Os recursos que são atribuídos ao Pacote de Serviço podem ser subdivididos entre pacotes de códigos.</span><span class="sxs-lookup"><span data-stu-id="ee256-109">The resources that are assigned to Service Package can be further divided between code packages.</span></span> <span data-ttu-id="ee256-110">Os limites de recurso especificados também indicam a reserva dos recursos.</span><span class="sxs-lookup"><span data-stu-id="ee256-110">The resource limits specified also mean the reservation of the resources.</span></span> <span data-ttu-id="ee256-111">O Service Fabric dá suporte à especificação de CPU e Memória por pacote de serviço, usando duas [métricas](service-fabric-cluster-resource-manager-metrics.md) internas:</span><span class="sxs-lookup"><span data-stu-id="ee256-111">Service Fabric supports specifying CPU and Memory per service package, using two built-in [metrics](service-fabric-cluster-resource-manager-metrics.md):</span></span>

* <span data-ttu-id="ee256-112">CPU (nome da métrica `ServiceFabric:/_CpuCores`): um núcleo é um núcleo lógico que está disponível no computador host e todos os núcleos em todos os nós são ponderados da mesma forma.</span><span class="sxs-lookup"><span data-stu-id="ee256-112">CPU (metric name `ServiceFabric:/_CpuCores`): A core is a logical core that is available on the host machine, and all cores across all nodes are weighted the same.</span></span>
* <span data-ttu-id="ee256-113">Memória (nome da métrica `ServiceFabric:/_MemoryInMB`): a memória é expressa em megabytes e é mapeada para a memória física disponível no computador.</span><span class="sxs-lookup"><span data-stu-id="ee256-113">Memory (metric name `ServiceFabric:/_MemoryInMB`): Memory is expressed in megabytes, and it maps to physical memory that is available on the machine.</span></span>

<span data-ttu-id="ee256-114">São fornecidas apenas garantias de reserva flexível – o tempo de execução rejeita a abertura de novos pacotes de serviço quando os recursos disponíveis são excedidos.</span><span class="sxs-lookup"><span data-stu-id="ee256-114">Only soft reservation guarantees are provided - the runtime rejects opening of new service packages available resources are exceeded.</span></span> <span data-ttu-id="ee256-115">No entanto, se outro executável ou contêiner for colocado no nó, isso poderá violar as garantias de reserva originais.</span><span class="sxs-lookup"><span data-stu-id="ee256-115">However, if another executable or container is placed on the node, that may violate the original reservation guarantees.</span></span>

<span data-ttu-id="ee256-116">Para essas duas métricas, o [Gerenciador de Recursos do Cluster](service-fabric-cluster-resource-manager-cluster-description.md) controla a capacidade total do cluster, a carga em cada nó do cluster e os recursos restantes do cluster.</span><span class="sxs-lookup"><span data-stu-id="ee256-116">For these two metrics, the [Cluster Resource Manager](service-fabric-cluster-resource-manager-cluster-description.md) tracks total cluster capacity, the load on each node in the cluster, and, remaining resources in the cluster.</span></span> <span data-ttu-id="ee256-117">Essas duas métricas são equivalentes a qualquer outro usuário ou outra métrica personalizada e todos os recursos existentes podem ser usados com elas:</span><span class="sxs-lookup"><span data-stu-id="ee256-117">These two metrics are equivalent to any other user or custom metric and all existing features can be used with them:</span></span>
* <span data-ttu-id="ee256-118">O cluster pode ser [equilibrado](service-fabric-cluster-resource-manager-balancing.md) de acordo com essas duas métricas (comportamento padrão).</span><span class="sxs-lookup"><span data-stu-id="ee256-118">Cluster can be [balanced](service-fabric-cluster-resource-manager-balancing.md) according to these two metrics (default behavior).</span></span>
* <span data-ttu-id="ee256-119">O cluster pode ser [desfragmentado](service-fabric-cluster-resource-manager-defragmentation-metrics.md) de acordo com essas duas métricas.</span><span class="sxs-lookup"><span data-stu-id="ee256-119">Cluster can be [defragmented](service-fabric-cluster-resource-manager-defragmentation-metrics.md) according to these two metrics.</span></span>
* <span data-ttu-id="ee256-120">Ao [descrever um cluster](service-fabric-cluster-resource-manager-cluster-description.md), a capacidade armazenada em buffer pode ser definida para essas duas métricas.</span><span class="sxs-lookup"><span data-stu-id="ee256-120">When [describing a cluster](service-fabric-cluster-resource-manager-cluster-description.md), buffered capacity can be set for these two metrics.</span></span>

<span data-ttu-id="ee256-121">Não há suporte para [relatórios de cargas dinâmicas](service-fabric-cluster-resource-manager-metrics.md) nessas métricas e as cargas dessas métricas são definidas no momento da criação.</span><span class="sxs-lookup"><span data-stu-id="ee256-121">[Dynamic load reporting](service-fabric-cluster-resource-manager-metrics.md) is not supported for these metrics, and loads for these metrics are defined at creation time.</span></span>

## <a name="cluster-set-up-for-enabling-resource-governance"></a><span data-ttu-id="ee256-122">Configuração de cluster para habilitar a governança de recursos</span><span class="sxs-lookup"><span data-stu-id="ee256-122">Cluster set up for enabling resource governance</span></span>

<span data-ttu-id="ee256-123">A capacidade deve ser definida manualmente em cada tipo de nó do cluster da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="ee256-123">Capacity should be defined manually in each node type in the cluster as follows:</span></span>

```xml
    <NodeType Name="MyNodeType">
      <Capacities>
        <Capacity Name="ServiceFabric:/_CpuCores" Value="4"/>
        <Capacity Name="ServiceFabric:/_MemoryInMB" Value="2048"/>
      </Capacities>
    </NodeType>
```
 
<span data-ttu-id="ee256-124">A governança de recursos é permitida somente em serviços do usuário e não em qualquer serviço do sistema.</span><span class="sxs-lookup"><span data-stu-id="ee256-124">Resource governance is allowed only on user services and not on any system services.</span></span> <span data-ttu-id="ee256-125">Ao especificar a capacidade, alguns núcleos e uma parte da memória devem ser deixados não alocados para serviços do sistema.</span><span class="sxs-lookup"><span data-stu-id="ee256-125">When specifying capacity, some cores and memory must be left unallocated for system services.</span></span> <span data-ttu-id="ee256-126">Para obter o desempenho ideal, a seguinte configuração também deve ser ativada no manifesto do cluster:</span><span class="sxs-lookup"><span data-stu-id="ee256-126">For optimal performance, the following setting should also be turned on in the cluster manifest:</span></span> 

```xml
<Section Name="PlacementAndLoadBalancing">
    <Parameter Name="PreventTransientOvercommit" Value="true" /> 
    <Parameter Name="AllowConstraintCheckFixesDuringApplicationUpgrade" Value="true" />
</Section>
```


## <a name="specifying-resource-governance"></a><span data-ttu-id="ee256-127">Especificando a governança de recursos</span><span class="sxs-lookup"><span data-stu-id="ee256-127">Specifying resource governance</span></span> 

<span data-ttu-id="ee256-128">Os limites da governança de recursos são especificados no manifesto do aplicativo (seção ServiceManifestImport), conforme mostrado no seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="ee256-128">Resource governance limits are specified in the application manifest (ServiceManifestImport section) as shown in the following example:</span></span>

```xml
<?xml version='1.0' encoding='UTF-8'?>
<ApplicationManifest ApplicationTypeName='TestAppTC1' ApplicationTypeVersion='vTC1' xsi:schemaLocation='http://schemas.microsoft.com/2011/01/fabric ServiceFabricServiceModel.xsd' xmlns='http://schemas.microsoft.com/2011/01/fabric' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance'>
  <Parameters>
  </Parameters>
  <!--
  ServicePackageA has the number of CPU cores defined, but doesn't have the MemoryInMB defined.
  In this case, Service Fabric will sum the limits on code packages and uses the sum as 
  the overall ServicePackage limit.
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
  
<span data-ttu-id="ee256-129">Neste exemplo, o pacote de serviço ServicePackageA obtém um núcleo nos nós em que ele é colocado.</span><span class="sxs-lookup"><span data-stu-id="ee256-129">In this example, service package ServicePackageA gets one core on the nodes where it is placed.</span></span> <span data-ttu-id="ee256-130">Esse pacote de serviço contém dois pacotes de códigos (CodeA1 e CodeA2) e ambos especificam o parâmetro `CpuShares`.</span><span class="sxs-lookup"><span data-stu-id="ee256-130">This service package contains two code packages (CodeA1 and CodeA2), and both specify the `CpuShares` parameter.</span></span> <span data-ttu-id="ee256-131">A proporção de CpuShares 512:256 divide o núcleo entre os dois pacotes de códigos.</span><span class="sxs-lookup"><span data-stu-id="ee256-131">The proportion of CpuShares 512:256  divides the core across the two code packages.</span></span> <span data-ttu-id="ee256-132">Portanto, neste exemplo, CodeA1 obtém dois terços de um núcleo e CodeA2 obtém um terço de um núcleo (e uma reserva de garantia reversível do mesmo).</span><span class="sxs-lookup"><span data-stu-id="ee256-132">Thus, in this example, CodeA1 gets two-thirds of a core, and  CodeA2 gets one-third of a core (and a soft-guarantee reservation of the same).</span></span> <span data-ttu-id="ee256-133">Nos casos em que CpuShares não forem especificadas para pacotes de códigos, o Service Fabric dividirá os núcleos igualmente entre eles.</span><span class="sxs-lookup"><span data-stu-id="ee256-133">In case when CpuShares are not specified for code packages, Service Fabric divides the cores equally among them.</span></span>

<span data-ttu-id="ee256-134">Os limites de memória são absolutos e, portanto, os dois pacotes de códigos são limitados a 1.024 MB de memória (e a uma reserva de garantia reversível da mesma).</span><span class="sxs-lookup"><span data-stu-id="ee256-134">Memory limits are absolute, so both code packages are limited to 1024 MB of memory (and a soft-guarantee reservation of the same).</span></span> <span data-ttu-id="ee256-135">Os pacotes de códigos (contêineres ou processos) não podem alocar mais memória do que esse limite. A tentativa de fazer isso resultará em uma exceção de memória insuficiente.</span><span class="sxs-lookup"><span data-stu-id="ee256-135">Code packages (containers or processes) are not able to allocate more memory than this limit, and attempting to do so results in an out-of-memory exception.</span></span> <span data-ttu-id="ee256-136">Para que a imposição do limite de recursos funcione, todos os pacotes de códigos em um pacote de serviço devem ter limites de memória especificados.</span><span class="sxs-lookup"><span data-stu-id="ee256-136">For resource limit enforcement to work, all code packages within a service package should have memory limits specified.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ee256-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ee256-137">Next steps</span></span>
* <span data-ttu-id="ee256-138">Para saber mais sobre o Gerenciador de Recursos do Cluster, leia este [artigo](service-fabric-cluster-resource-manager-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ee256-138">To learn more about Cluster Resource Manager, read this [article](service-fabric-cluster-resource-manager-introduction.md).</span></span>
* <span data-ttu-id="ee256-139">Para saber mais sobre o modelo de aplicativo, pacotes de serviço, pacotes de códigos e como as réplicas são mapeadas para eles, leia este [artigo](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="ee256-139">To learn more about application model, service packages, code packages and how replicas map to them read this [article](service-fabric-application-model.md).</span></span>
