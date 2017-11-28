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
# <a name="service-movement-cost"></a><span data-ttu-id="ce1f7-103">Custo do movimentação de serviços</span><span class="sxs-lookup"><span data-stu-id="ce1f7-103">Service movement cost</span></span>
<span data-ttu-id="ce1f7-104">Um fator que Olá Gerenciador de recursos de Cluster do serviço de malha considera ao tentar toodetermine o cluster de tooa toomake alterações é o custo de saudação essas alterações.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-104">A factor that hello Service Fabric Cluster Resource Manager considers when trying toodetermine what changes toomake tooa cluster is hello cost of those changes.</span></span> <span data-ttu-id="ce1f7-105">noção de saudação de "custo" foi negociada desativado em cluster quanto Olá pode ser melhorado.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-105">hello notion of "cost" is traded off against how much hello cluster can be improved.</span></span> <span data-ttu-id="ce1f7-106">O custo é considerado ao mover serviços para balanceamento, desfragmentação e outros requisitos.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-106">Cost is factored in when moving services for balancing, defragmentation, and other requirements.</span></span> <span data-ttu-id="ce1f7-107">meta de saudação é toomeet requisitos Olá Olá forma menos de interrupção ou cara.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-107">hello goal is toomeet hello requirements in hello least disruptive or expensive way.</span></span> 

<span data-ttu-id="ce1f7-108">Movimentar serviços custa, no mínimo, tempo de CPU e largura de banda de rede.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-108">Moving services costs CPU time and network bandwidth at a minimum.</span></span> <span data-ttu-id="ce1f7-109">Para serviços com monitoração de estado, ele exige copiando estado Olá desses serviços, consumo de disco e memória adicional.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-109">For stateful services, it requires copying hello state of those services, consuming additional memory and disk.</span></span> <span data-ttu-id="ce1f7-110">Minimizar os custos de saudação de soluções que Olá Gerenciador de recursos de Cluster do Azure Service Fabric é fornecido com ajuda a garantir que os recursos do cluster Olá não são gastou desnecessariamente.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-110">Minimizing hello cost of solutions that hello Azure Service Fabric Cluster Resource Manager comes up with helps ensure that hello cluster's resources aren't spent unnecessarily.</span></span> <span data-ttu-id="ce1f7-111">No entanto, você também não quiser tooignore soluções que podem melhorar significativamente o alocação Olá de recursos em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-111">However, you also don’t want tooignore solutions that would significantly improve hello allocation of resources in hello cluster.</span></span>

<span data-ttu-id="ce1f7-112">Olá Gerenciador de recursos de Cluster tem duas formas de custos de computação e limitando-los enquanto ele tenta toomanage cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-112">hello Cluster Resource Manager has two ways of computing costs and limiting them while it tries toomanage hello cluster.</span></span> <span data-ttu-id="ce1f7-113">mecanismo primeiro Olá simplesmente está contando a cada mudança que seria.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-113">hello first mechanism is simply counting every move that it would make.</span></span> <span data-ttu-id="ce1f7-114">Se duas soluções são geradas com sobre Olá mesmo saldo (pontuação), em seguida, Olá Gerenciador de recursos de Cluster prefere Olá um com hello custo mais baixo (número total de movimentações).</span><span class="sxs-lookup"><span data-stu-id="ce1f7-114">If two solutions are generated with about hello same balance (score), then hello Cluster Resource Manager prefers hello one with hello lowest cost (total number of moves).</span></span>

<span data-ttu-id="ce1f7-115">Esta estratégia funciona bem.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-115">This strategy works well.</span></span> <span data-ttu-id="ce1f7-116">Mas, como ocorre com cargas estáticas ou padrão, é improvável em qualquer sistema complexo que todas as mudanças sejam iguais.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-116">But as with default or static loads, it's unlikely in any complex system that all moves are equal.</span></span> <span data-ttu-id="ce1f7-117">Alguns são provavelmente toobe muito mais caro.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-117">Some are likely toobe much more expensive.</span></span>

## <a name="setting-move-costs"></a><span data-ttu-id="ce1f7-118">Definindo custos de movimentação</span><span class="sxs-lookup"><span data-stu-id="ce1f7-118">Setting Move Costs</span></span> 
<span data-ttu-id="ce1f7-119">Você pode especificar o custo de mudança saudação padrão para um serviço quando ele é criado:</span><span class="sxs-lookup"><span data-stu-id="ce1f7-119">You can specify hello default move cost for a service when it is created:</span></span>

<span data-ttu-id="ce1f7-120">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ce1f7-120">PowerShell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -DefaultMoveCost Medium
```

<span data-ttu-id="ce1f7-121">C#:</span><span class="sxs-lookup"><span data-stu-id="ce1f7-121">C#:</span></span> 

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
//set up hello rest of hello ServiceDescription
serviceDescription.DefaultMoveCost = MoveCost.Medium;
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

<span data-ttu-id="ce1f7-122">Você também pode especificar ou atualizar MoveCost dinamicamente de um serviço após a criação do serviço de saudação:</span><span class="sxs-lookup"><span data-stu-id="ce1f7-122">You can also specify or update MoveCost dynamically for a service after hello service has been created:</span></span> 

<span data-ttu-id="ce1f7-123">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ce1f7-123">PowerShell:</span></span> 

```posh
Update-ServiceFabricService -Stateful -ServiceName "fabric:/AppName/ServiceName" -DefaultMoveCost High
```

<span data-ttu-id="ce1f7-124">C#:</span><span class="sxs-lookup"><span data-stu-id="ce1f7-124">C#:</span></span>

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.DefaultMoveCost = MoveCost.High;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/AppName/ServiceName"), updateDescription);
```

## <a name="dynamically-specifying-move-cost-on-a-per-replica-basis"></a><span data-ttu-id="ce1f7-125">Especificando dinamicamente o custo de movimentação por réplica</span><span class="sxs-lookup"><span data-stu-id="ce1f7-125">Dynamically specifying move cost on a per-replica basis</span></span>

<span data-ttu-id="ce1f7-126">Olá trechos de código anteriores são todos para especificar MoveCost para um serviço todo uma vez do próprio serviço Olá externa.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-126">hello preceding snippets are all for specifying MoveCost for a whole service at once from outside hello service itself.</span></span> <span data-ttu-id="ce1f7-127">No entanto, mover o custo é mais útil é quando muda de custo de mudança de saudação de um objeto de serviço específico com o seu tempo de vida.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-127">However, move cost is most useful is when hello move cost of a specific service object changes over its lifespan.</span></span> <span data-ttu-id="ce1f7-128">Como Olá serviços próprios provavelmente ter ideia melhor de saudação de cara como eles são toomove um determinado momento, há uma API para serviços tooreport seu próprios Mover individual de custo durante o tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-128">Since hello services themselves probably have hello best idea of how costly they are toomove a given time, there's an API for services tooreport their own individual move cost during runtime.</span></span> 

<span data-ttu-id="ce1f7-129">C#:</span><span class="sxs-lookup"><span data-stu-id="ce1f7-129">C#:</span></span>

```csharp
this.Partition.ReportMoveCost(MoveCost.Medium);
```

## <a name="impact-of-move-cost"></a><span data-ttu-id="ce1f7-130">Impacto do custo de movimentação</span><span class="sxs-lookup"><span data-stu-id="ce1f7-130">Impact of move cost</span></span>
<span data-ttu-id="ce1f7-131">O MoveCost tem quatro níveis: Zero, Baixo, Médio e Alto.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-131">MoveCost has four levels: Zero, Low, Medium, and High.</span></span> <span data-ttu-id="ce1f7-132">MoveCosts são relativo tooeach outro, com exceção de Zero.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-132">MoveCosts are relative tooeach other, except for Zero.</span></span> <span data-ttu-id="ce1f7-133">Custo zero move significa que o movimento é gratuito e não deve contar com pontuação de saudação de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-133">Zero move cost means that movement is free and should not count against hello score of hello solution.</span></span> <span data-ttu-id="ce1f7-134">Configuração da mudança custo tooHigh *não* garante que a réplica Olá permanece em um único local.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-134">Setting your move cost tooHigh does *not* guarantee that hello replica stays in one place.</span></span>

<span data-ttu-id="ce1f7-135"><center>
![O custo de movimentação como um fator na seleção de réplicas para movimentação][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="ce1f7-135"><center>
![Move cost as a factor in selecting replicas for movement][Image1]
</center></span></span>

<span data-ttu-id="ce1f7-136">MoveCost ajuda você a encontrar soluções Olá que causa Olá geral o mínimo de interrupções e é tooachieve mais fácil ao mesmo tempo, ainda que chegam ao saldo equivalente.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-136">MoveCost helps you find hello solutions that cause hello least disruption overall and are easiest tooachieve while still arriving at equivalent balance.</span></span> <span data-ttu-id="ce1f7-137">Noção de um serviço de custo pode ser relativo toomany coisas.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-137">A service’s notion of cost can be relative toomany things.</span></span> <span data-ttu-id="ce1f7-138">Olá fatores mais comuns para calcular o custo de movimento são:</span><span class="sxs-lookup"><span data-stu-id="ce1f7-138">hello most common factors in calculating your move cost are:</span></span>

- <span data-ttu-id="ce1f7-139">saudação de estado ou dados Olá serviço tem toomove.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-139">hello amount of state or data that hello service has toomove.</span></span>
- <span data-ttu-id="ce1f7-140">custo de saudação de desconexão de clientes.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-140">hello cost of disconnection of clients.</span></span> <span data-ttu-id="ce1f7-141">Mover uma réplica primária é geralmente mais caro do que o custo de saudação da movimentação de uma réplica secundária.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-141">Moving a primary replica is usually more costly than hello cost of moving a secondary replica.</span></span>
- <span data-ttu-id="ce1f7-142">custo de saudação de interromper uma operação em andamento.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-142">hello cost of interrupting an in-flight operation.</span></span> <span data-ttu-id="ce1f7-143">Nível de armazenamento de algumas operações em dados saudação ou operações executadas na chamada de cliente tooa resposta são caras.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-143">Some operations at hello data store level or operations performed in response tooa client call are costly.</span></span> <span data-ttu-id="ce1f7-144">Após um certo ponto, você não deseja toostop-los, se você não precisa.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-144">After a certain point, you don’t want toostop them if you don’t have to.</span></span> <span data-ttu-id="ce1f7-145">Portanto enquanto a operação de saudação está acontecendo, aumentar custo de mudança de saudação de probabilidade Olá de tooreduce de objeto este serviço que ele se move.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-145">So while hello operation is going on, you increase hello move cost of this service object tooreduce hello likelihood that it moves.</span></span> <span data-ttu-id="ce1f7-146">Quando a operação de saudação é feita, você pode definir Olá custo back toonormal.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-146">When hello operation is done, you set hello cost back toonormal.</span></span>

## <a name="enabling-move-cost-in-your-cluster"></a><span data-ttu-id="ce1f7-147">Habilitando o custo de movimentação em seu cluster</span><span class="sxs-lookup"><span data-stu-id="ce1f7-147">Enabling move cost in your cluster</span></span>
<span data-ttu-id="ce1f7-148">Para que hello mais granular toobe MoveCosts levada em conta, MoveCost deverá ser habilitada no cluster.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-148">In order for hello more granular MoveCosts toobe taken into account, MoveCost must be enabled in your cluster.</span></span> <span data-ttu-id="ce1f7-149">Sem essa configuração, modo padrão de saudação de movimentações de contagem é usado para calcular MoveCost e MoveCost relatórios serão ignorados.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-149">Without this setting, hello default mode of counting moves is used for calculating MoveCost, and MoveCost reports are ignored.</span></span>


<span data-ttu-id="ce1f7-150">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="ce1f7-150">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="UseMoveCostReports" Value="true" />
        </Section>
```

<span data-ttu-id="ce1f7-151">via ClusterConfig.json para implantações autônomas ou Template.json para clusters hospedados pelo Azure:</span><span class="sxs-lookup"><span data-stu-id="ce1f7-151">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ce1f7-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ce1f7-152">Next steps</span></span>
- <span data-ttu-id="ce1f7-153">Gerenciador de recursos de Cluster do serviço de malha usa o consumo de toomanage de métricas e a capacidade em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ce1f7-153">Service Fabric Cluster Resource Manger uses metrics toomanage consumption and capacity in hello cluster.</span></span> <span data-ttu-id="ce1f7-154">toolearn mais sobre as métricas e como tooconfigure-los, confira [consumo de recursos de gerenciamento e de carga na malha do serviço com métricas](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="ce1f7-154">toolearn more about metrics and how tooconfigure them, check out [Managing resource consumption and load in Service Fabric with metrics](service-fabric-cluster-resource-manager-metrics.md).</span></span>
- <span data-ttu-id="ce1f7-155">toolearn sobre como Olá Gerenciador de recursos de Cluster gerencia e equilibra a carga no cluster Olá, confira [sua malha do serviço de cluster de balanceamento](service-fabric-cluster-resource-manager-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="ce1f7-155">toolearn about how hello Cluster Resource Manager manages and balances load in hello cluster, check out [Balancing your Service Fabric cluster](service-fabric-cluster-resource-manager-balancing.md).</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-movement-cost/service-most-cost-example.png
