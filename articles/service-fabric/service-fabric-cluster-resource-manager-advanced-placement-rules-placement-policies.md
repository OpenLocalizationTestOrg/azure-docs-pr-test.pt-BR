---
title: "Resource Manager de Cluster do Service Fabric – políticas de posicionamento | Microsoft Docs"
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
ms.openlocfilehash: 6c11d49d5fdb3148b0534c9448f815358fa8cab3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="placement-policies-for-service-fabric-services"></a><span data-ttu-id="4633d-103">Políticas de posicionamento para serviços do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4633d-103">Placement policies for service fabric services</span></span>
<span data-ttu-id="4633d-104">As políticas de posicionamento são regras adicionais que podem ser usadas para administrar o posicionamento de serviço em alguns cenários específicos, menos comuns.</span><span class="sxs-lookup"><span data-stu-id="4633d-104">Placement policies are additional rules that can be used to govern service placement in some specific, less-common scenarios.</span></span> <span data-ttu-id="4633d-105">Alguns exemplos desses cenários são:</span><span class="sxs-lookup"><span data-stu-id="4633d-105">Some examples of those scenarios are:</span></span>

- <span data-ttu-id="4633d-106">O cluster do Service Fabric engloba distâncias geográficas, como vários datacenters locais ou regiões do Azure</span><span class="sxs-lookup"><span data-stu-id="4633d-106">Your Service Fabric cluster spans geographic distances, such as multiple on-premises datacenters or across Azure regions</span></span>
- <span data-ttu-id="4633d-107">O ambiente abrange várias áreas de controle geopolítico ou legal, ou algum outro caso em que você tem limites políticos que precisa impor</span><span class="sxs-lookup"><span data-stu-id="4633d-107">Your environment spans multiple areas of geopolitical or legal control, or some other case where you have policy boundaries you need to enforce</span></span>
- <span data-ttu-id="4633d-108">Há considerações de latência ou desempenho de comunicação devido a grandes distâncias ou uso de links de rede mais lentos ou menos confiáveis</span><span class="sxs-lookup"><span data-stu-id="4633d-108">There are communication performance or latency considerations due to large distances or use of slower or less reliable network links</span></span>
- <span data-ttu-id="4633d-109">Você precisa manter determinadas cargas de trabalho colocadas como um melhor esforço, seja com outras cargas de trabalho, seja na proximidade dos clientes</span><span class="sxs-lookup"><span data-stu-id="4633d-109">You need to keep certain workloads collocated as a best effort, either with other workloads or in proximity to customers</span></span>

<span data-ttu-id="4633d-110">A maioria desses requisitos se alinha ao layout físico do cluster, representado como os domínios de falha do cluster.</span><span class="sxs-lookup"><span data-stu-id="4633d-110">Most of these requirements align with the physical layout of the cluster, represented as the fault domains of the cluster.</span></span> 

<span data-ttu-id="4633d-111">As políticas de posicionamento avançado que ajudam a resolver esses cenários são:</span><span class="sxs-lookup"><span data-stu-id="4633d-111">The advanced placement policies that help address these scenarios are:</span></span>

1. <span data-ttu-id="4633d-112">Domínios inválidos</span><span class="sxs-lookup"><span data-stu-id="4633d-112">Invalid domains</span></span>
2. <span data-ttu-id="4633d-113">Domínios necessários</span><span class="sxs-lookup"><span data-stu-id="4633d-113">Required domains</span></span>
3. <span data-ttu-id="4633d-114">Domínios preferenciais</span><span class="sxs-lookup"><span data-stu-id="4633d-114">Preferred domains</span></span>
4. <span data-ttu-id="4633d-115">Desativação de empacotamento de réplica</span><span class="sxs-lookup"><span data-stu-id="4633d-115">Disallowing replica packing</span></span>

<span data-ttu-id="4633d-116">A maioria dos controles a seguir pode ser configurada por meio das propriedades de nó e de restrições de posicionamento, mas algumas são mais complicadas.</span><span class="sxs-lookup"><span data-stu-id="4633d-116">Most of the following controls could be configured via node properties and placement constraints, but some are more complicated.</span></span> <span data-ttu-id="4633d-117">Para simplificar, o Cluster Resource Manager do Service Fabric fornece essas políticas de posicionamento adicionais.</span><span class="sxs-lookup"><span data-stu-id="4633d-117">To make things simpler, the Service Fabric Cluster Resource Manager provides these additional placement policies.</span></span> <span data-ttu-id="4633d-118">As políticas de posicionamento são configuradas de acordo com uma instância de serviço nomeada.</span><span class="sxs-lookup"><span data-stu-id="4633d-118">Placement policies are configured on a per-named service instance basis.</span></span> <span data-ttu-id="4633d-119">Elas também podem ser atualizadas dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="4633d-119">They can also be updated dynamically.</span></span>

## <a name="specifying-invalid-domains"></a><span data-ttu-id="4633d-120">Especificando domínios inválidos</span><span class="sxs-lookup"><span data-stu-id="4633d-120">Specifying invalid domains</span></span>
<span data-ttu-id="4633d-121">A política de posicionamento **InvalidDomain** permite especificar que um determinado Domínio de Falha é inválido para um serviço específico.</span><span class="sxs-lookup"><span data-stu-id="4633d-121">The **InvalidDomain** placement policy allows you to specify that a particular Fault Domain is invalid for a specific service.</span></span> <span data-ttu-id="4633d-122">Essa política garante que um serviço específico nunca seja executado em uma determinada área, por exemplo, por motivos de política corporativa ou geopolíticos.</span><span class="sxs-lookup"><span data-stu-id="4633d-122">This policy ensures that a particular service never runs in a particular area, for example for geopolitical or corporate policy reasons.</span></span> <span data-ttu-id="4633d-123">Vários domínios inválidos podem ser especificados através de diferentes políticas.</span><span class="sxs-lookup"><span data-stu-id="4633d-123">Multiple invalid domains may be specified via separate policies.</span></span>

<span data-ttu-id="4633d-124"><center>
![Exemplo de domínio inválido][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="4633d-124"><center>
![Invalid Domain Example][Image1]
</center></span></span>

<span data-ttu-id="4633d-125">Código:</span><span class="sxs-lookup"><span data-stu-id="4633d-125">Code:</span></span>

```csharp
ServicePlacementInvalidDomainPolicyDescription invalidDomain = new ServicePlacementInvalidDomainPolicyDescription();
invalidDomain.DomainName = "fd:/DCEast"; //regulations prohibit this workload here
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

<span data-ttu-id="4633d-126">Powershell:</span><span class="sxs-lookup"><span data-stu-id="4633d-126">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("InvalidDomain,fd:/DCEast”)
```
## <a name="specifying-required-domains"></a><span data-ttu-id="4633d-127">Especificando domínios necessários</span><span class="sxs-lookup"><span data-stu-id="4633d-127">Specifying required domains</span></span>
<span data-ttu-id="4633d-128">A política de posicionamento de domínio necessário requer que o serviço esteja presente somente no domínio especificado.</span><span class="sxs-lookup"><span data-stu-id="4633d-128">The required domain placement policy requires that the service is present only in the specified domain.</span></span> <span data-ttu-id="4633d-129">Vários domínios necessários podem ser especificados através de diferentes políticas.</span><span class="sxs-lookup"><span data-stu-id="4633d-129">Multiple required domains can be specified via separate policies.</span></span>

<span data-ttu-id="4633d-130"><center>
![Exemplo de domínio necessário][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="4633d-130"><center>
![Required Domain Example][Image2]
</center></span></span>

<span data-ttu-id="4633d-131">Código:</span><span class="sxs-lookup"><span data-stu-id="4633d-131">Code:</span></span>

```csharp
ServicePlacementRequiredDomainPolicyDescription requiredDomain = new ServicePlacementRequiredDomainPolicyDescription();
requiredDomain.DomainName = "fd:/DC01/RK03/BL2";
serviceDescription.PlacementPolicies.Add(requiredDomain);
```

<span data-ttu-id="4633d-132">Powershell:</span><span class="sxs-lookup"><span data-stu-id="4633d-132">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomain,fd:/DC01/RK03/BL2")
```

## <a name="specifying-a-preferred-domain-for-the-primary-replicas-of-a-stateful-service"></a><span data-ttu-id="4633d-133">Especificando um domínio preferido para as réplicas primárias de um serviço com estado</span><span class="sxs-lookup"><span data-stu-id="4633d-133">Specifying a preferred domain for the primary replicas of a stateful service</span></span>
<span data-ttu-id="4633d-134">O Domínio Primário Preferencial especifica o domínio de falha no qual colocar o primário.</span><span class="sxs-lookup"><span data-stu-id="4633d-134">The Preferred Primary Domain specifies the fault domain to place the Primary in.</span></span> <span data-ttu-id="4633d-135">O primário é encerrado nesse domínio quando tudo está íntegro.</span><span class="sxs-lookup"><span data-stu-id="4633d-135">The Primary ends up in this domain when everything is healthy.</span></span> <span data-ttu-id="4633d-136">Se o domínio ou a réplica primária falhar ou desligar, o primário move-se para algum outro local. De modo ideal, no mesmo domínio.</span><span class="sxs-lookup"><span data-stu-id="4633d-136">If the domain or the Primary replica fails or shuts down, the Primary moves to some other location, ideally in the same domain.</span></span> <span data-ttu-id="4633d-137">Se essa nova localização não estiver no domínio preferencial, o Cluster Resource Manager vai movê-lo de volta ao domínio preferencial assim que possível.</span><span class="sxs-lookup"><span data-stu-id="4633d-137">If this new location isn't in the preferred domain, the Cluster Resource Manager moves it back to the preferred domain as soon as possible.</span></span> <span data-ttu-id="4633d-138">Obviamente, essa configuração só faz sentido para serviços com estado.</span><span class="sxs-lookup"><span data-stu-id="4633d-138">Naturally this setting only makes sense for stateful services.</span></span> <span data-ttu-id="4633d-139">Essa política é mais útil em clusters que estão distribuídos em regiões do Azure ou em vários datacenters, mas têm serviços que preferem o posicionamento em um determinado local.</span><span class="sxs-lookup"><span data-stu-id="4633d-139">This policy is most useful in clusters that are spanned across Azure regions or multiple datacenters but have services that prefer placement in a certain location.</span></span> <span data-ttu-id="4633d-140">Manter os primários próximos aos seus usuários ou outros serviços ajudam a fornecer latência menor, especialmente para leituras, que são tratadas pelos primários por padrão.</span><span class="sxs-lookup"><span data-stu-id="4633d-140">Keeping Primaries close to their users or other services helps provide lower latency, especially for reads, which are handled by Primaries by default.</span></span>

<span data-ttu-id="4633d-141"><center>
![Domínios primários preferenciais e failover][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="4633d-141"><center>
![Preferred Primary Domains and Failover][Image3]
</center></span></span>

```csharp
ServicePlacementPreferPrimaryDomainPolicyDescription primaryDomain = new ServicePlacementPreferPrimaryDomainPolicyDescription();
primaryDomain.DomainName = "fd:/EastUS/";
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

<span data-ttu-id="4633d-142">Powershell:</span><span class="sxs-lookup"><span data-stu-id="4633d-142">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("PreferredPrimaryDomain,fd:/EastUS")
```

## <a name="requiring-replica-distribution-and-disallowing-packing"></a><span data-ttu-id="4633d-143">Exigindo a distribuição de réplica e desabilitando o empacotamento</span><span class="sxs-lookup"><span data-stu-id="4633d-143">Requiring replica distribution and disallowing packing</span></span>
<span data-ttu-id="4633d-144">As réplicas _normalmente_ são distribuídas entre domínios de falha e upgrade quando o cluster está íntegro.</span><span class="sxs-lookup"><span data-stu-id="4633d-144">Replicas are _normally_ distributed across fault and upgrade domains when the cluster is healthy.</span></span> <span data-ttu-id="4633d-145">No entanto, há casos em que mais de uma réplica para uma determinada partição podem acabar temporariamente empacotadas em uma único domínio.</span><span class="sxs-lookup"><span data-stu-id="4633d-145">However, there are cases where more than one replica for a given partition may end up temporarily packed into a single domain.</span></span> <span data-ttu-id="4633d-146">Por exemplo, digamos que o cluster tenha nove nós em três domínios de falha, fd:/0, fd:/1 e fd:/2.</span><span class="sxs-lookup"><span data-stu-id="4633d-146">For example, let's say that the cluster has nine nodes in three fault domains, fd:/0, fd:/1, and fd:/2.</span></span> <span data-ttu-id="4633d-147">Digamos também que o serviço tem três réplicas.</span><span class="sxs-lookup"><span data-stu-id="4633d-147">Let's also say that your service has three replicas.</span></span> <span data-ttu-id="4633d-148">Digamos que os nós que estavam sendo usados para as réplicas em fd:/1 e fd:/2 foram desativados.</span><span class="sxs-lookup"><span data-stu-id="4633d-148">Let's say that the nodes that were being used for those replicas in fd:/1 and fd:/2 went down.</span></span> <span data-ttu-id="4633d-149">Normalmente, o Gerenciador de Recursos de Cluster prefere outros nós nos mesmos domínios de falha.</span><span class="sxs-lookup"><span data-stu-id="4633d-149">Normally the Cluster Resource Manager would prefer other nodes in those same fault domains.</span></span> <span data-ttu-id="4633d-150">Nesse caso, digamos que devido a problemas de capacidade nenhum dos outros nós nesses domínios era válido.</span><span class="sxs-lookup"><span data-stu-id="4633d-150">In this case, let's say due to capacity issues none of the other nodes in those domains were valid.</span></span> <span data-ttu-id="4633d-151">Se o Cluster Resource Manager criasse substituições para essas réplicas, ele precisaria escolher nós em fd:/0.</span><span class="sxs-lookup"><span data-stu-id="4633d-151">If the Cluster Resource Manager builds replacements for those replicas, it would have to choose nodes in fd:/0.</span></span> <span data-ttu-id="4633d-152">No entanto, fazer _isso_ cria uma situação em que a restrição de Domínio de Falha é violada.</span><span class="sxs-lookup"><span data-stu-id="4633d-152">However, doing _that_ creates a situation where the Fault Domain constraint is violated.</span></span> <span data-ttu-id="4633d-153">Empacotar réplicas aumenta as chances de que o conjunto inteiro de réplicas possa ser desativado ou roubado.</span><span class="sxs-lookup"><span data-stu-id="4633d-153">Packing replicas increases the chance that the whole replica set could go down or be lost.</span></span> 

> [!NOTE]
> <span data-ttu-id="4633d-154">Para obter mais informações sobre restrições e prioridades de restrições em geral, confira [este tópico](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).</span><span class="sxs-lookup"><span data-stu-id="4633d-154">For more information on constraints and constraint priorities generally, check out [this topic](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).</span></span>
>

<span data-ttu-id="4633d-155">Se você já viu uma mensagem de integridade, como "`The Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating the Constraint: FaultDomain`", você atingiu essa condição ou algo parecido.</span><span class="sxs-lookup"><span data-stu-id="4633d-155">If you've ever seen a health message such as "`The Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating the Constraint: FaultDomain`", then you've hit this condition or something like it.</span></span> <span data-ttu-id="4633d-156">Normalmente, apenas uma ou duas réplicas são empacotadas juntas temporariamente.</span><span class="sxs-lookup"><span data-stu-id="4633d-156">Usually only one or two replicas are packed together temporarily.</span></span> <span data-ttu-id="4633d-157">Enquanto houver menos de um quorum de réplicas em um determinado domínio, você estará seguro.</span><span class="sxs-lookup"><span data-stu-id="4633d-157">So long as there are fewer than a quorum of replicas in a given domain, you're safe.</span></span> <span data-ttu-id="4633d-158">O empacotamento é raro, mas pode acontecer e, geralmente, essas situações são transitórias, uma vez que os nós voltam.</span><span class="sxs-lookup"><span data-stu-id="4633d-158">Packing is rare, but it can happen, and usually these situations are transient since the nodes come back.</span></span> <span data-ttu-id="4633d-159">Se os nós permanecem inativos e o Cluster Resource Manager precisa criar substituições, normalmente haverá outros nós disponíveis nos domínios de falha ideais.</span><span class="sxs-lookup"><span data-stu-id="4633d-159">If the nodes do stay down and the Cluster Resource Manager needs to build replacements, usually there are other nodes available in the ideal fault domains.</span></span>

<span data-ttu-id="4633d-160">Algumas cargas de trabalho sempre preferirão ter o número de destino de réplicas, mesmo se elas forem empacotadas em menos domínios.</span><span class="sxs-lookup"><span data-stu-id="4633d-160">Some workloads would prefer always having the target number of replicas, even if they are packed into fewer domains.</span></span> <span data-ttu-id="4633d-161">Essas cargas de trabalho apostam contra falhas de domínio permanentes simultâneas totais e normalmente podem recuperar o estado local.</span><span class="sxs-lookup"><span data-stu-id="4633d-161">These workloads are betting against total simultaneous permanent domain failures and can usually recover local state.</span></span> <span data-ttu-id="4633d-162">Outras cargas de trabalho preferem passar logo pelo tempo de inatividade do que arriscar a correção ou a perda de dados.</span><span class="sxs-lookup"><span data-stu-id="4633d-162">Other workloads would rather take the downtime earlier than risk correctness or loss of data.</span></span> <span data-ttu-id="4633d-163">A maioria das cargas de trabalho de produção é executada com mais de três réplicas, mais de três domínios de falha e muitos nós válidos por domínio de falha.</span><span class="sxs-lookup"><span data-stu-id="4633d-163">Most production workloads run with more than three replicas, more than three fault domains, and many valid nodes per fault domain.</span></span> <span data-ttu-id="4633d-164">Por isso, o comportamento padrão permite o empacotamento de domínio por padrão.</span><span class="sxs-lookup"><span data-stu-id="4633d-164">Because of this, the default behavior allows domain packing by default.</span></span> <span data-ttu-id="4633d-165">O comportamento padrão permite balanceamento normal e failover para tratar desses casos extremos, mesmo que isso signifique empacotamento de domínio temporário.</span><span class="sxs-lookup"><span data-stu-id="4633d-165">The default behavior allows normal balancing and failover to handle these extreme cases, even if that means temporary domain packing.</span></span>

<span data-ttu-id="4633d-166">Se desejar desabilitar esse empacotamento para uma determinada carga de trabalho, você poderá especificar a política `RequireDomainDistribution` no serviço.</span><span class="sxs-lookup"><span data-stu-id="4633d-166">If you want to disable such packing for a given workload, you can specify the `RequireDomainDistribution` policy on the service.</span></span> <span data-ttu-id="4633d-167">Quando essa política é definida, o Gerenciador de Recursos de Cluster garante que duas réplicas da mesma partição não seja executadas no mesmo domínio de falha ou upgrade.</span><span class="sxs-lookup"><span data-stu-id="4633d-167">When this policy is set, the Cluster Resource Manager ensures no two replicas from the same partition run in the same fault or upgrade domain.</span></span>

<span data-ttu-id="4633d-168">Código:</span><span class="sxs-lookup"><span data-stu-id="4633d-168">Code:</span></span>

```csharp
ServicePlacementRequireDomainDistributionPolicyDescription distributeDomain = new ServicePlacementRequireDomainDistributionPolicyDescription();
serviceDescription.PlacementPolicies.Add(distributeDomain);
```

<span data-ttu-id="4633d-169">Powershell:</span><span class="sxs-lookup"><span data-stu-id="4633d-169">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomainDistribution")
```

<span data-ttu-id="4633d-170">Agora, seria possível usar essas configurações para serviços em um cluster que não tenha sido distribuído geograficamente?</span><span class="sxs-lookup"><span data-stu-id="4633d-170">Now, would it be possible to use these configurations for services in a cluster that was not geographically spanned?</span></span> <span data-ttu-id="4633d-171">Seria, mas também não há um bom motivo para isso.</span><span class="sxs-lookup"><span data-stu-id="4633d-171">You could, but there’s not a great reason too.</span></span> <span data-ttu-id="4633d-172">As configurações de domínio obrigatórias, inválidas e preferenciais devem ser evitadas, a menos que os cenários as exijam.</span><span class="sxs-lookup"><span data-stu-id="4633d-172">The required, invalid, and preferred domain configurations should be avoided unless the scenarios require them.</span></span> <span data-ttu-id="4633d-173">Não faz sentido tentar forçar uma determinada carga de trabalho a ser executada em um único rack ou preferir algum segmento do seu cluster local em vez de outro.</span><span class="sxs-lookup"><span data-stu-id="4633d-173">It doesn't make any sense to try to force a given workload to run in a single rack, or to prefer some segment of your local cluster over another.</span></span> <span data-ttu-id="4633d-174">Diferentes configurações de hardware devem ser distribuídas entre domínios de falha e manipuladas por propriedades de nó e restrições de posicionamento normais.</span><span class="sxs-lookup"><span data-stu-id="4633d-174">Different hardware configurations should be spread across fault domains and handled via normal placement constraints and node properties.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4633d-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4633d-175">Next steps</span></span>
- <span data-ttu-id="4633d-176">Para saber mais sobre como configurar os serviços, [Saiba mais sobre como configurar serviços](service-fabric-cluster-resource-manager-configure-services.md)</span><span class="sxs-lookup"><span data-stu-id="4633d-176">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-invalid-placement-domain.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-required-placement-domain.png
[Image3]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-preferred-primary-domain.png
