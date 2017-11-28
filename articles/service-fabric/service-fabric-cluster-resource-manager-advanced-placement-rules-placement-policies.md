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
# <a name="placement-policies-for-service-fabric-services"></a><span data-ttu-id="e38ec-103">Políticas de posicionamento para serviços do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e38ec-103">Placement policies for service fabric services</span></span>
<span data-ttu-id="e38ec-104">Políticas de posicionamento são regras adicionais que podem ser usados toogovern posicionamento do serviço em alguns cenários específicos, menos comuns.</span><span class="sxs-lookup"><span data-stu-id="e38ec-104">Placement policies are additional rules that can be used toogovern service placement in some specific, less-common scenarios.</span></span> <span data-ttu-id="e38ec-105">Alguns exemplos desses cenários são:</span><span class="sxs-lookup"><span data-stu-id="e38ec-105">Some examples of those scenarios are:</span></span>

- <span data-ttu-id="e38ec-106">O cluster do Service Fabric engloba distâncias geográficas, como vários datacenters locais ou regiões do Azure</span><span class="sxs-lookup"><span data-stu-id="e38ec-106">Your Service Fabric cluster spans geographic distances, such as multiple on-premises datacenters or across Azure regions</span></span>
- <span data-ttu-id="e38ec-107">Seu ambiente abrange várias áreas de controle geopolíticas ou legal ou algum outro caso em que os limites de política você precisa tooenforce</span><span class="sxs-lookup"><span data-stu-id="e38ec-107">Your environment spans multiple areas of geopolitical or legal control, or some other case where you have policy boundaries you need tooenforce</span></span>
- <span data-ttu-id="e38ec-108">Há considerações de desempenho ou a latência de comunicação devido distâncias toolarge ou o uso de links de rede mais lento ou menos confiável</span><span class="sxs-lookup"><span data-stu-id="e38ec-108">There are communication performance or latency considerations due toolarge distances or use of slower or less reliable network links</span></span>
- <span data-ttu-id="e38ec-109">Você precisa tookeep determinada cargas de trabalho colocada como um melhor esforço, com outras cargas de trabalho ou em proximidade toocustomers</span><span class="sxs-lookup"><span data-stu-id="e38ec-109">You need tookeep certain workloads collocated as a best effort, either with other workloads or in proximity toocustomers</span></span>

<span data-ttu-id="e38ec-110">A maioria desses requisitos alinha com o layout físico de saudação do cluster hello, representado como Olá domínios de falha de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="e38ec-110">Most of these requirements align with hello physical layout of hello cluster, represented as hello fault domains of hello cluster.</span></span> 

<span data-ttu-id="e38ec-111">Olá avançadas de políticas de posicionamento que ajudam a solucionar que esses cenários são:</span><span class="sxs-lookup"><span data-stu-id="e38ec-111">hello advanced placement policies that help address these scenarios are:</span></span>

1. <span data-ttu-id="e38ec-112">Domínios inválidos</span><span class="sxs-lookup"><span data-stu-id="e38ec-112">Invalid domains</span></span>
2. <span data-ttu-id="e38ec-113">Domínios necessários</span><span class="sxs-lookup"><span data-stu-id="e38ec-113">Required domains</span></span>
3. <span data-ttu-id="e38ec-114">Domínios preferenciais</span><span class="sxs-lookup"><span data-stu-id="e38ec-114">Preferred domains</span></span>
4. <span data-ttu-id="e38ec-115">Desativação de empacotamento de réplica</span><span class="sxs-lookup"><span data-stu-id="e38ec-115">Disallowing replica packing</span></span>

<span data-ttu-id="e38ec-116">A maioria das Olá controles a seguir pode ser configurada por meio de propriedades de nó e restrições de posicionamento, mas alguns são mais complicados.</span><span class="sxs-lookup"><span data-stu-id="e38ec-116">Most of hello following controls could be configured via node properties and placement constraints, but some are more complicated.</span></span> <span data-ttu-id="e38ec-117">coisas toomake mais simples, Olá Gerenciador de recursos de Cluster do serviço de malha fornece essas políticas de posicionamento adicional.</span><span class="sxs-lookup"><span data-stu-id="e38ec-117">toomake things simpler, hello Service Fabric Cluster Resource Manager provides these additional placement policies.</span></span> <span data-ttu-id="e38ec-118">As políticas de posicionamento são configuradas de acordo com uma instância de serviço nomeada.</span><span class="sxs-lookup"><span data-stu-id="e38ec-118">Placement policies are configured on a per-named service instance basis.</span></span> <span data-ttu-id="e38ec-119">Elas também podem ser atualizadas dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="e38ec-119">They can also be updated dynamically.</span></span>

## <a name="specifying-invalid-domains"></a><span data-ttu-id="e38ec-120">Especificando domínios inválidos</span><span class="sxs-lookup"><span data-stu-id="e38ec-120">Specifying invalid domains</span></span>
<span data-ttu-id="e38ec-121">Olá **InvalidDomain** posicionamento política permite que você toospecify que um determinado domínio de falha é inválido para um serviço específico.</span><span class="sxs-lookup"><span data-stu-id="e38ec-121">hello **InvalidDomain** placement policy allows you toospecify that a particular Fault Domain is invalid for a specific service.</span></span> <span data-ttu-id="e38ec-122">Essa política garante que um serviço específico nunca seja executado em uma determinada área, por exemplo, por motivos de política corporativa ou geopolíticos.</span><span class="sxs-lookup"><span data-stu-id="e38ec-122">This policy ensures that a particular service never runs in a particular area, for example for geopolitical or corporate policy reasons.</span></span> <span data-ttu-id="e38ec-123">Vários domínios inválidos podem ser especificados através de diferentes políticas.</span><span class="sxs-lookup"><span data-stu-id="e38ec-123">Multiple invalid domains may be specified via separate policies.</span></span>

<span data-ttu-id="e38ec-124"><center>
![Exemplo de domínio inválido][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="e38ec-124"><center>
![Invalid Domain Example][Image1]
</center></span></span>

<span data-ttu-id="e38ec-125">Código:</span><span class="sxs-lookup"><span data-stu-id="e38ec-125">Code:</span></span>

```csharp
ServicePlacementInvalidDomainPolicyDescription invalidDomain = new ServicePlacementInvalidDomainPolicyDescription();
invalidDomain.DomainName = "fd:/DCEast"; //regulations prohibit this workload here
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

<span data-ttu-id="e38ec-126">Powershell:</span><span class="sxs-lookup"><span data-stu-id="e38ec-126">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("InvalidDomain,fd:/DCEast”)
```
## <a name="specifying-required-domains"></a><span data-ttu-id="e38ec-127">Especificando domínios necessários</span><span class="sxs-lookup"><span data-stu-id="e38ec-127">Specifying required domains</span></span>
<span data-ttu-id="e38ec-128">Olá necessário política de substituição de domínio requer que o serviço de saudação está presente somente no domínio especificado hello.</span><span class="sxs-lookup"><span data-stu-id="e38ec-128">hello required domain placement policy requires that hello service is present only in hello specified domain.</span></span> <span data-ttu-id="e38ec-129">Vários domínios necessários podem ser especificados através de diferentes políticas.</span><span class="sxs-lookup"><span data-stu-id="e38ec-129">Multiple required domains can be specified via separate policies.</span></span>

<span data-ttu-id="e38ec-130"><center>
![Exemplo de domínio necessário][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="e38ec-130"><center>
![Required Domain Example][Image2]
</center></span></span>

<span data-ttu-id="e38ec-131">Código:</span><span class="sxs-lookup"><span data-stu-id="e38ec-131">Code:</span></span>

```csharp
ServicePlacementRequiredDomainPolicyDescription requiredDomain = new ServicePlacementRequiredDomainPolicyDescription();
requiredDomain.DomainName = "fd:/DC01/RK03/BL2";
serviceDescription.PlacementPolicies.Add(requiredDomain);
```

<span data-ttu-id="e38ec-132">Powershell:</span><span class="sxs-lookup"><span data-stu-id="e38ec-132">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomain,fd:/DC01/RK03/BL2")
```

## <a name="specifying-a-preferred-domain-for-hello-primary-replicas-of-a-stateful-service"></a><span data-ttu-id="e38ec-133">Especificar um domínio preferencial para réplicas primárias de saudação de um serviço com monitoração de estado</span><span class="sxs-lookup"><span data-stu-id="e38ec-133">Specifying a preferred domain for hello primary replicas of a stateful service</span></span>
<span data-ttu-id="e38ec-134">Domínio primário preferencial Hello Especifica tooplace de domínio de falha de Olá Olá principal no.</span><span class="sxs-lookup"><span data-stu-id="e38ec-134">hello Preferred Primary Domain specifies hello fault domain tooplace hello Primary in.</span></span> <span data-ttu-id="e38ec-135">Olá primário termina nesse domínio quando tudo está íntegro.</span><span class="sxs-lookup"><span data-stu-id="e38ec-135">hello Primary ends up in this domain when everything is healthy.</span></span> <span data-ttu-id="e38ec-136">Se domínio Olá ou a réplica primária Olá falha ou desligado, Olá primário move toosome outro local, idealmente em Olá mesmo domínio.</span><span class="sxs-lookup"><span data-stu-id="e38ec-136">If hello domain or hello Primary replica fails or shuts down, hello Primary moves toosome other location, ideally in hello same domain.</span></span> <span data-ttu-id="e38ec-137">Se o novo local não está no domínio preferencial hello, Olá Gerenciador de recursos de Cluster move-o novamente domínio preferencial toohello assim que possível.</span><span class="sxs-lookup"><span data-stu-id="e38ec-137">If this new location isn't in hello preferred domain, hello Cluster Resource Manager moves it back toohello preferred domain as soon as possible.</span></span> <span data-ttu-id="e38ec-138">Obviamente, essa configuração só faz sentido para serviços com estado.</span><span class="sxs-lookup"><span data-stu-id="e38ec-138">Naturally this setting only makes sense for stateful services.</span></span> <span data-ttu-id="e38ec-139">Essa política é mais útil em clusters que estão distribuídos em regiões do Azure ou em vários datacenters, mas têm serviços que preferem o posicionamento em um determinado local.</span><span class="sxs-lookup"><span data-stu-id="e38ec-139">This policy is most useful in clusters that are spanned across Azure regions or multiple datacenters but have services that prefer placement in a certain location.</span></span> <span data-ttu-id="e38ec-140">Mantendo primárias fechar tootheir usuários ou outros serviços ajuda a fornecer a latência mais baixa, especialmente para leituras, que são tratadas por primários por padrão.</span><span class="sxs-lookup"><span data-stu-id="e38ec-140">Keeping Primaries close tootheir users or other services helps provide lower latency, especially for reads, which are handled by Primaries by default.</span></span>

<span data-ttu-id="e38ec-141"><center>
![Domínios primários preferenciais e failover][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="e38ec-141"><center>
![Preferred Primary Domains and Failover][Image3]
</center></span></span>

```csharp
ServicePlacementPreferPrimaryDomainPolicyDescription primaryDomain = new ServicePlacementPreferPrimaryDomainPolicyDescription();
primaryDomain.DomainName = "fd:/EastUS/";
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

<span data-ttu-id="e38ec-142">Powershell:</span><span class="sxs-lookup"><span data-stu-id="e38ec-142">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("PreferredPrimaryDomain,fd:/EastUS")
```

## <a name="requiring-replica-distribution-and-disallowing-packing"></a><span data-ttu-id="e38ec-143">Exigindo a distribuição de réplica e desabilitando o empacotamento</span><span class="sxs-lookup"><span data-stu-id="e38ec-143">Requiring replica distribution and disallowing packing</span></span>
<span data-ttu-id="e38ec-144">As réplicas são _normalmente_ distribuídos entre domínios de falha e atualização quando Olá cluster está íntegro.</span><span class="sxs-lookup"><span data-stu-id="e38ec-144">Replicas are _normally_ distributed across fault and upgrade domains when hello cluster is healthy.</span></span> <span data-ttu-id="e38ec-145">No entanto, há casos em que mais de uma réplica para uma determinada partição podem acabar temporariamente empacotadas em uma único domínio.</span><span class="sxs-lookup"><span data-stu-id="e38ec-145">However, there are cases where more than one replica for a given partition may end up temporarily packed into a single domain.</span></span> <span data-ttu-id="e38ec-146">Por exemplo, digamos que esse cluster Olá tem nove nós em três domínios de falha, fd: 0, fd: / 1 e fd: / 2.</span><span class="sxs-lookup"><span data-stu-id="e38ec-146">For example, let's say that hello cluster has nine nodes in three fault domains, fd:/0, fd:/1, and fd:/2.</span></span> <span data-ttu-id="e38ec-147">Digamos também que o serviço tem três réplicas.</span><span class="sxs-lookup"><span data-stu-id="e38ec-147">Let's also say that your service has three replicas.</span></span> <span data-ttu-id="e38ec-148">Digamos que Olá nós que estavam sendo usados para as réplicas no fd: / 1 e fd: / 2 foi desativado.</span><span class="sxs-lookup"><span data-stu-id="e38ec-148">Let's say that hello nodes that were being used for those replicas in fd:/1 and fd:/2 went down.</span></span> <span data-ttu-id="e38ec-149">Normalmente, Olá Gerenciador de recursos de Cluster prefere outros nós os mesmos domínios de falha.</span><span class="sxs-lookup"><span data-stu-id="e38ec-149">Normally hello Cluster Resource Manager would prefer other nodes in those same fault domains.</span></span> <span data-ttu-id="e38ec-150">Nesse caso, vamos supor que devido a problemas de toocapacity nenhum da saudação outros nós nesses domínios eram válidos.</span><span class="sxs-lookup"><span data-stu-id="e38ec-150">In this case, let's say due toocapacity issues none of hello other nodes in those domains were valid.</span></span> <span data-ttu-id="e38ec-151">Se Olá Gerenciador de recursos de Cluster de compilações de substituições para essas réplicas, ele teria toochoose nós fd: 0.</span><span class="sxs-lookup"><span data-stu-id="e38ec-151">If hello Cluster Resource Manager builds replacements for those replicas, it would have toochoose nodes in fd:/0.</span></span> <span data-ttu-id="e38ec-152">No entanto, fazer _que_ criará uma situação onde Olá restrição de domínio de falha for violada.</span><span class="sxs-lookup"><span data-stu-id="e38ec-152">However, doing _that_ creates a situation where hello Fault Domain constraint is violated.</span></span> <span data-ttu-id="e38ec-153">Aumenta de réplicas de remessa chance de Olá Olá conjunto inteiro de réplica pode ir para baixo ou serão perdidos.</span><span class="sxs-lookup"><span data-stu-id="e38ec-153">Packing replicas increases hello chance that hello whole replica set could go down or be lost.</span></span> 

> [!NOTE]
> <span data-ttu-id="e38ec-154">Para obter mais informações sobre restrições e prioridades de restrições em geral, confira [este tópico](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).</span><span class="sxs-lookup"><span data-stu-id="e38ec-154">For more information on constraints and constraint priorities generally, check out [this topic](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).</span></span>
>

<span data-ttu-id="e38ec-155">Se você já viu uma mensagem de integridade, como "`hello Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating hello Constraint: FaultDomain`", você atingiu essa condição ou algo parecido.</span><span class="sxs-lookup"><span data-stu-id="e38ec-155">If you've ever seen a health message such as "`hello Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating hello Constraint: FaultDomain`", then you've hit this condition or something like it.</span></span> <span data-ttu-id="e38ec-156">Normalmente, apenas uma ou duas réplicas são empacotadas juntas temporariamente.</span><span class="sxs-lookup"><span data-stu-id="e38ec-156">Usually only one or two replicas are packed together temporarily.</span></span> <span data-ttu-id="e38ec-157">Enquanto houver menos de um quorum de réplicas em um determinado domínio, você estará seguro.</span><span class="sxs-lookup"><span data-stu-id="e38ec-157">So long as there are fewer than a quorum of replicas in a given domain, you're safe.</span></span> <span data-ttu-id="e38ec-158">Remessa é rara, mas isso pode acontecer e geralmente essas situações são transitórias como nós de saudação voltar.</span><span class="sxs-lookup"><span data-stu-id="e38ec-158">Packing is rare, but it can happen, and usually these situations are transient since hello nodes come back.</span></span> <span data-ttu-id="e38ec-159">Se nós Olá fiquem para baixo e Olá Gerenciador de recursos de Cluster precisa toobuild substituições, geralmente há outros nós disponíveis em domínios de falha ideal de saudação.</span><span class="sxs-lookup"><span data-stu-id="e38ec-159">If hello nodes do stay down and hello Cluster Resource Manager needs toobuild replacements, usually there are other nodes available in hello ideal fault domains.</span></span>

<span data-ttu-id="e38ec-160">Algumas cargas de trabalho prefere ter sempre o número de destino de saudação de réplicas, mesmo se eles são incluídos em menos domínios.</span><span class="sxs-lookup"><span data-stu-id="e38ec-160">Some workloads would prefer always having hello target number of replicas, even if they are packed into fewer domains.</span></span> <span data-ttu-id="e38ec-161">Essas cargas de trabalho apostam contra falhas de domínio permanentes simultâneas totais e normalmente podem recuperar o estado local.</span><span class="sxs-lookup"><span data-stu-id="e38ec-161">These workloads are betting against total simultaneous permanent domain failures and can usually recover local state.</span></span> <span data-ttu-id="e38ec-162">Outras cargas de trabalho em vez disso, seriam necessário tempo de inatividade Olá anteriores a exatidão de risco ou perda de dados.</span><span class="sxs-lookup"><span data-stu-id="e38ec-162">Other workloads would rather take hello downtime earlier than risk correctness or loss of data.</span></span> <span data-ttu-id="e38ec-163">A maioria das cargas de trabalho de produção é executada com mais de três réplicas, mais de três domínios de falha e muitos nós válidos por domínio de falha.</span><span class="sxs-lookup"><span data-stu-id="e38ec-163">Most production workloads run with more than three replicas, more than three fault domains, and many valid nodes per fault domain.</span></span> <span data-ttu-id="e38ec-164">Por isso, comportamento padrão de saudação permite que a remessa de domínio por padrão.</span><span class="sxs-lookup"><span data-stu-id="e38ec-164">Because of this, hello default behavior allows domain packing by default.</span></span> <span data-ttu-id="e38ec-165">saudação padrão comportamento permite que balanceamento normal e failover toohandle esses casos extremos, mesmo que isso significa que o empacotamento de domínio temporário.</span><span class="sxs-lookup"><span data-stu-id="e38ec-165">hello default behavior allows normal balancing and failover toohandle these extreme cases, even if that means temporary domain packing.</span></span>

<span data-ttu-id="e38ec-166">Se você quiser toodisable tal remessa para uma determinada carga de trabalho, você pode especificar Olá `RequireDomainDistribution` política no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="e38ec-166">If you want toodisable such packing for a given workload, you can specify hello `RequireDomainDistribution` policy on hello service.</span></span> <span data-ttu-id="e38ec-167">Quando essa política está definida, Olá Gerenciador de recursos de Cluster garante que não existam duas réplicas da mesma partição executados em Olá mesmo falha ou domínio de atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="e38ec-167">When this policy is set, hello Cluster Resource Manager ensures no two replicas from hello same partition run in hello same fault or upgrade domain.</span></span>

<span data-ttu-id="e38ec-168">Código:</span><span class="sxs-lookup"><span data-stu-id="e38ec-168">Code:</span></span>

```csharp
ServicePlacementRequireDomainDistributionPolicyDescription distributeDomain = new ServicePlacementRequireDomainDistributionPolicyDescription();
serviceDescription.PlacementPolicies.Add(distributeDomain);
```

<span data-ttu-id="e38ec-169">Powershell:</span><span class="sxs-lookup"><span data-stu-id="e38ec-169">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomainDistribution")
```

<span data-ttu-id="e38ec-170">Agora, é que ele seja possível toouse essas configurações para serviços em um cluster que não foi estendido geograficamente?</span><span class="sxs-lookup"><span data-stu-id="e38ec-170">Now, would it be possible toouse these configurations for services in a cluster that was not geographically spanned?</span></span> <span data-ttu-id="e38ec-171">Seria, mas também não há um bom motivo para isso.</span><span class="sxs-lookup"><span data-stu-id="e38ec-171">You could, but there’s not a great reason too.</span></span> <span data-ttu-id="e38ec-172">Hello configurações de domínio necessários, inválido e preferencial devem ser evitadas, a menos que exigem cenários Olá-los.</span><span class="sxs-lookup"><span data-stu-id="e38ec-172">hello required, invalid, and preferred domain configurations should be avoided unless hello scenarios require them.</span></span> <span data-ttu-id="e38ec-173">Não faz qualquer tooforce de tootry sentido toorun uma determinada carga de trabalho em um único rack ou tooprefer algum segmento do cluster em detrimento de outro local.</span><span class="sxs-lookup"><span data-stu-id="e38ec-173">It doesn't make any sense tootry tooforce a given workload toorun in a single rack, or tooprefer some segment of your local cluster over another.</span></span> <span data-ttu-id="e38ec-174">Diferentes configurações de hardware devem ser distribuídas entre domínios de falha e manipuladas por propriedades de nó e restrições de posicionamento normais.</span><span class="sxs-lookup"><span data-stu-id="e38ec-174">Different hardware configurations should be spread across fault domains and handled via normal placement constraints and node properties.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e38ec-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e38ec-175">Next steps</span></span>
- <span data-ttu-id="e38ec-176">Para saber mais sobre como configurar os serviços, [Saiba mais sobre como configurar serviços](service-fabric-cluster-resource-manager-configure-services.md)</span><span class="sxs-lookup"><span data-stu-id="e38ec-176">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-invalid-placement-domain.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-required-placement-domain.png
[Image3]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-preferred-primary-domain.png
