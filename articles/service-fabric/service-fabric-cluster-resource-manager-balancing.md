---
title: Equilibrar seu cluster do Azure Service Fabric | Microsoft Docs
description: "Uma introdução ao balanceamento de cluster com o Gerenciador de Recursos de Cluster do Service Fabric."
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
ms.openlocfilehash: 34eacb29f324025c1d2803c9690600227d3ec457
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="balancing-your-service-fabric-cluster"></a><span data-ttu-id="009b8-103">Balanceamento do cluster do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="009b8-103">Balancing your service fabric cluster</span></span>
<span data-ttu-id="009b8-104">O Gerenciador de Recursos de Cluster do Service Fabric oferece suporte a alterações de carga dinâmico, reagindo a inclusões ou remoções de nós ou serviços.</span><span class="sxs-lookup"><span data-stu-id="009b8-104">The Service Fabric Cluster Resource Manager supports dynamic load changes, reacting to additions or removals of nodes or services.</span></span> <span data-ttu-id="009b8-105">Ele também corrige automaticamente as violações de restrição e, proativamente, balanceia novamente o cluster.</span><span class="sxs-lookup"><span data-stu-id="009b8-105">It also automatically corrects constraint violations, and proactively rebalances the cluster.</span></span> <span data-ttu-id="009b8-106">Mas com que frequência essas ações são executadas, e o que as dispara?</span><span class="sxs-lookup"><span data-stu-id="009b8-106">But how often are these actions taken, and what triggers them?</span></span>

<span data-ttu-id="009b8-107">Há três categorias diferentes de trabalho executadas pelo Gerenciador de Recursos de Cluster.</span><span class="sxs-lookup"><span data-stu-id="009b8-107">There are three different categories of work that the Cluster Resource Manager performs.</span></span> <span data-ttu-id="009b8-108">Eles são:</span><span class="sxs-lookup"><span data-stu-id="009b8-108">They are:</span></span>

1. <span data-ttu-id="009b8-109">Posicionamento – esse estágio lida com o posicionamento de réplicas com estado ou de instâncias sem estado que estejam ausentes.</span><span class="sxs-lookup"><span data-stu-id="009b8-109">Placement – this stage deals with placing any stateful replicas or stateless instances that are missing.</span></span> <span data-ttu-id="009b8-110">O posicionamento inclui os novos serviços e a manipulação de réplicas com estado ou de instâncias sem estado que falharam.</span><span class="sxs-lookup"><span data-stu-id="009b8-110">Placement includes both new services and handling stateful replicas or stateless instances that have failed.</span></span> <span data-ttu-id="009b8-111">A exclusão e o descarte de réplicas ou de instâncias são tratados aqui.</span><span class="sxs-lookup"><span data-stu-id="009b8-111">Deleting and dropping replicas or instances are handled here.</span></span>
2. <span data-ttu-id="009b8-112">Verificações de Restrição – esse estágio verifica e corrige violações das restrições (regras) de posicionamento no sistema.</span><span class="sxs-lookup"><span data-stu-id="009b8-112">Constraint Checks – this stage checks for and corrects violations of the different placement constraints (rules) within the system.</span></span> <span data-ttu-id="009b8-113">Os exemplos de regras são a garantia de que os nós não estão acima da capacidade e se as restrições de posicionamento do serviço estão sendo atendidas.</span><span class="sxs-lookup"><span data-stu-id="009b8-113">Examples of rules are things like ensuring that nodes are not over capacity and that a service’s placement constraints are met.</span></span>
3. <span data-ttu-id="009b8-114">Balanceamento – este estágio verifica se o rebalanceamento é necessário com base no nível desejado de saldo para métricas diferentes configurado.</span><span class="sxs-lookup"><span data-stu-id="009b8-114">Balancing – this stage checks to see if rebalancing is necessary based on the configured desired level of balance for different metrics.</span></span> <span data-ttu-id="009b8-115">Nesse caso, ele tenta localizar uma organização em cluster que é mais equilibrado.</span><span class="sxs-lookup"><span data-stu-id="009b8-115">If so it attempts to find an arrangement in the cluster that is more balanced.</span></span>

## <a name="configuring-cluster-resource-manager-timers"></a><span data-ttu-id="009b8-116">Configuração de temporizadores do Gerenciador de Recursos de Cluster</span><span class="sxs-lookup"><span data-stu-id="009b8-116">Configuring Cluster Resource Manager Timers</span></span>
<span data-ttu-id="009b8-117">O primeiro conjunto de controles de balanceamento são um conjunto de temporizadores.</span><span class="sxs-lookup"><span data-stu-id="009b8-117">The first set of controls around balancing are a set of timers.</span></span> <span data-ttu-id="009b8-118">Esses temporizadores determinam a frequência com que o Gerenciador de Recursos de Cluster examina o cluster e executa as ações corretivas.</span><span class="sxs-lookup"><span data-stu-id="009b8-118">These timers govern how often the Cluster Resource Manager examines the cluster and takes corrective actions.</span></span>

<span data-ttu-id="009b8-119">Cada um desses tipos diferentes de correções que o Gerenciador de Recursos de Cluster pode fazer é controlado por um temporizador diferente que rege sua frequência.</span><span class="sxs-lookup"><span data-stu-id="009b8-119">Each of these different types of corrections the Cluster Resource Manager can make is controlled by a different timer that governs its frequency.</span></span> <span data-ttu-id="009b8-120">Quando cada temporizador é acionado, a tarefa é agendada.</span><span class="sxs-lookup"><span data-stu-id="009b8-120">When each timer fires, the task is scheduled.</span></span> <span data-ttu-id="009b8-121">Por padrão, o Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="009b8-121">By default the Resource Manager:</span></span>

* <span data-ttu-id="009b8-122">verifica o estado e aplica atualizações (como gravação de um nó estiver inativo) cada 1/10 de segundo</span><span class="sxs-lookup"><span data-stu-id="009b8-122">scans its state and applies updates (like recording that a node is down) every 1/10th of a second</span></span>
* <span data-ttu-id="009b8-123">define o sinalizador de verificação de posicionamento</span><span class="sxs-lookup"><span data-stu-id="009b8-123">sets the placement check flag</span></span> 
* <span data-ttu-id="009b8-124">define o sinalizador de verificação de restrição a cada segundo</span><span class="sxs-lookup"><span data-stu-id="009b8-124">sets the constraint check flag every second</span></span>
* <span data-ttu-id="009b8-125">Define o sinalizador de balanceamento a cada cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="009b8-125">sets the balancing flag every five seconds.</span></span>

<span data-ttu-id="009b8-126">Veja a seguir exemplos de configuração que governam esses temporizadores:</span><span class="sxs-lookup"><span data-stu-id="009b8-126">Examples of the configuration governing these timers are below:</span></span>

<span data-ttu-id="009b8-127">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="009b8-127">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PLBRefreshGap" Value="0.1" />
            <Parameter Name="MinPlacementInterval" Value="1.0" />
            <Parameter Name="MinConstraintCheckInterval" Value="1.0" />
            <Parameter Name="MinLoadBalancingInterval" Value="5.0" />
        </Section>
```

<span data-ttu-id="009b8-128">via ClusterConfig.json para implantações Autônomas ou Template.json para clusters hospedados pelo Azure:</span><span class="sxs-lookup"><span data-stu-id="009b8-128">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="009b8-129">Atualmente o Resource Manager de Cluster executa apenas uma dessas ações ao mesmo tempo, sequencialmente.</span><span class="sxs-lookup"><span data-stu-id="009b8-129">Today the Cluster Resource Manager only performs one of these actions at a time, sequentially.</span></span> <span data-ttu-id="009b8-130">É por isso que fazemos referência a esses temporizadores como "intervalos mínimos" e as ações realizadas quando os temporizadores desligam como "sinalizadores de configuração".</span><span class="sxs-lookup"><span data-stu-id="009b8-130">This is why we refer to these timers as “minimum intervals” and the actions that get taken when the timers go off as "setting flags".</span></span> <span data-ttu-id="009b8-131">Por exemplo, o Resource Manager de Cluster se encarrega de solicitações pendentes para criar serviços antes do cluster de balanceamento.</span><span class="sxs-lookup"><span data-stu-id="009b8-131">For example, the Cluster Resource Manager takes care of pending requests to create services before balancing the cluster.</span></span> <span data-ttu-id="009b8-132">Como você pode ver, os intervalos de tempo padrão especificados, o Gerenciador de Recursos de Cluster examina se há qualquer coisa que precisa ser feito com frequência.</span><span class="sxs-lookup"><span data-stu-id="009b8-132">As you can see by the default time intervals specified, the Cluster Resource Manager scans for anything it needs to do frequently.</span></span> <span data-ttu-id="009b8-133">Normalmente, isso significa que o conjunto de alterações feitas durante cada etapa é pequeno.</span><span class="sxs-lookup"><span data-stu-id="009b8-133">Normally this means that the set of changes made during each step is small.</span></span> <span data-ttu-id="009b8-134">Fazer pequenas alterações frequentemente faz com que o Gerenciador de Recursos de Cluster responda às coisas que acontecem no cluster.</span><span class="sxs-lookup"><span data-stu-id="009b8-134">Making small changes frequently allows the Cluster Resource Manager to be responsive when things happen in the cluster.</span></span> <span data-ttu-id="009b8-135">Os temporizadores padrão oferecem algum lote, já que muitos dos mesmos tipos de eventos tendem a ocorrer simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="009b8-135">The default timers provide some batching since many of the same types of events tend to occur simultaneously.</span></span> 

<span data-ttu-id="009b8-136">Por exemplo, quando os nós falham, eles podem fazer com um domínio de falha inteiro por vez.</span><span class="sxs-lookup"><span data-stu-id="009b8-136">For example, when nodes fail they can do so entire fault domains at a time.</span></span> <span data-ttu-id="009b8-137">Todas essas falhas são capturadas durante a próxima atualização de estado após o *PLBRefreshGap*.</span><span class="sxs-lookup"><span data-stu-id="009b8-137">All these failures are captured during the next state update after the *PLBRefreshGap*.</span></span> <span data-ttu-id="009b8-138">As correções são determinadas durante as seguintes execuções de posicionamento, verificação de restrição e balanceamento.</span><span class="sxs-lookup"><span data-stu-id="009b8-138">The corrections are determined during the following placement, constraint check, and balancing runs.</span></span> <span data-ttu-id="009b8-139">Por padrão o Resource Manager de Cluster não é uma varredura horas de alterações no cluster e tentando resolver todas as alterações ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="009b8-139">By default the Cluster Resource Manager is not scanning through hours of changes in the cluster and trying to address all changes at once.</span></span> <span data-ttu-id="009b8-140">Isso levaria a picos de variação.</span><span class="sxs-lookup"><span data-stu-id="009b8-140">Doing so would lead to bursts of churn.</span></span>

<span data-ttu-id="009b8-141">O Resource Manager de Cluster também precisa de algumas informações adicionais para determinar se o cluster desequilibrado.</span><span class="sxs-lookup"><span data-stu-id="009b8-141">The Cluster Resource Manager also needs some additional information to determine if the cluster imbalanced.</span></span> <span data-ttu-id="009b8-142">Para isso, temos duas outras configurações: *Limites de Balanceamento* e *Limites de Atividade*.</span><span class="sxs-lookup"><span data-stu-id="009b8-142">For that we have two other pieces of configuration: *BalancingThresholds* and *ActivityThresholds*.</span></span>

## <a name="balancing-thresholds"></a><span data-ttu-id="009b8-143">Limites de balanceamento</span><span class="sxs-lookup"><span data-stu-id="009b8-143">Balancing thresholds</span></span>
<span data-ttu-id="009b8-144">Um Limite de Balanceamento é o controle principal que dispara o rebalanceamento.</span><span class="sxs-lookup"><span data-stu-id="009b8-144">A Balancing Threshold is the main control for triggering rebalancing.</span></span> <span data-ttu-id="009b8-145">O Limite de Balanceamento para uma métrica é uma _razão_.</span><span class="sxs-lookup"><span data-stu-id="009b8-145">The Balancing Threshold for a metric is a _ratio_.</span></span> <span data-ttu-id="009b8-146">Se a carga de uma métrica no nó mais carregado dividido pela quantidade de carga no nó menos carregado excede o *Limite de Balanceamento* dessa métrica, o cluster é desequilibrado.</span><span class="sxs-lookup"><span data-stu-id="009b8-146">If the load for a metric on the most loaded node divided by the amount of load on the least loaded node exceeds that metric's *BalancingThreshold*, then the cluster is imbalanced.</span></span> <span data-ttu-id="009b8-147">Como resultado de balanceamento é disparada na próxima vez que o Resource Manager de Cluster verifica.</span><span class="sxs-lookup"><span data-stu-id="009b8-147">As a result balancing is triggered the next time the Cluster Resource Manager checks.</span></span> <span data-ttu-id="009b8-148">O temporizador *MinLoadBalancingInterval* define a frequência com que o Gerenciador de Recursos de Cluster deve verificar se o rebalanceamento é necessário.</span><span class="sxs-lookup"><span data-stu-id="009b8-148">The *MinLoadBalancingInterval* timer defines how often the Cluster Resource Manager should check if rebalancing is necessary.</span></span> <span data-ttu-id="009b8-149">A verificação não significa que nada acontece.</span><span class="sxs-lookup"><span data-stu-id="009b8-149">Checking doesn't mean that anything happens.</span></span> 

<span data-ttu-id="009b8-150">Os Limites de Balanceamento são definidos baseados em cada métrica, como parte da definição do cluster.</span><span class="sxs-lookup"><span data-stu-id="009b8-150">Balancing Thresholds are defined on a per-metric basis as a part of the cluster definition.</span></span> <span data-ttu-id="009b8-151">Para saber mais sobre como fazer isso, leia [este artigo](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="009b8-151">For more information on metrics, check out [this article](service-fabric-cluster-resource-manager-metrics.md).</span></span>

<span data-ttu-id="009b8-152">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="009b8-152">ClusterManifest.xml</span></span>

```xml
    <Section Name="MetricBalancingThresholds">
      <Parameter Name="MetricName1" Value="2"/>
      <Parameter Name="MetricName2" Value="3.5"/>
    </Section>
```

<span data-ttu-id="009b8-153">via ClusterConfig.json para implantações Autônomas ou Template.json para clusters hospedados pelo Azure:</span><span class="sxs-lookup"><span data-stu-id="009b8-153">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="009b8-154"><center>
![Exemplo de Limite de Balanceamento][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="009b8-154"><center>
![Balancing Threshold Example][Image1]
</center></span></span>

<span data-ttu-id="009b8-155">Neste exemplo, cada serviço está consumindo uma unidade de alguma métrica.</span><span class="sxs-lookup"><span data-stu-id="009b8-155">In this example, each service is consuming one unit of some metric.</span></span> <span data-ttu-id="009b8-156">No exemplo superior, a carga máxima em um nó é cinco e o mínimo é dois.</span><span class="sxs-lookup"><span data-stu-id="009b8-156">In the top example, the maximum load on a node is five and the minimum is two.</span></span> <span data-ttu-id="009b8-157">Digamos que o limite de balanceamento para esta métrica seja três.</span><span class="sxs-lookup"><span data-stu-id="009b8-157">Let’s say that the balancing threshold for this metric is three.</span></span> <span data-ttu-id="009b8-158">Como a proporção do cluster é 5/2 = 2,5 e é menor do que o especificado balanceamento de limite de três, o cluster é equilibrado.</span><span class="sxs-lookup"><span data-stu-id="009b8-158">Since the ratio in the cluster is 5/2 = 2.5 and that is less than the specified balancing threshold of three, the cluster is balanced.</span></span> <span data-ttu-id="009b8-159">Nenhum balanceamento é disparada quando verifica se o Resource Manager de Cluster.</span><span class="sxs-lookup"><span data-stu-id="009b8-159">No balancing is triggered when the Cluster Resource Manager checks.</span></span>

<span data-ttu-id="009b8-160">No exemplo inferior, a carga máxima em um nó é dez, enquanto o mínimo é dois, resultando em uma taxa de cinco.</span><span class="sxs-lookup"><span data-stu-id="009b8-160">In the bottom example, the maximum load on a node is 10, while the minimum is two, resulting in a ratio of five.</span></span> <span data-ttu-id="009b8-161">Cinco é maior que o limite de balanceamento designado de três para métrica.</span><span class="sxs-lookup"><span data-stu-id="009b8-161">Five is greater than the designated balancing threshold of three for that metric.</span></span> <span data-ttu-id="009b8-162">Como resultado, uma execução de rebalanceamento será agendada na próxima vez em que o temporizador de balanceamento for acionado.</span><span class="sxs-lookup"><span data-stu-id="009b8-162">As a result, a rebalancing run will be scheduled next time the balancing timer fires.</span></span> <span data-ttu-id="009b8-163">Em uma situação como essa, alguma carga normalmente é distribuída para Node3.</span><span class="sxs-lookup"><span data-stu-id="009b8-163">In a situation like this some load is usually distributed to Node3.</span></span> <span data-ttu-id="009b8-164">Como o Gerenciador de Recursos de Cluster do Service Fabric não usa uma abordagem egoísta, alguma carga também pode ser distribuída para Node2.</span><span class="sxs-lookup"><span data-stu-id="009b8-164">Because the Service Fabric Cluster Resource Manager doesn't use a greedy approach, some load could also be distributed to Node2.</span></span> 

<span data-ttu-id="009b8-165"><center>
![Ações de exemplo de Limite de Balanceamento][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="009b8-165"><center>
![Balancing Threshold Example Actions][Image2]
</center></span></span>

> [!NOTE]
> <span data-ttu-id="009b8-166">O "Balanceamento" trata duas estratégias diferentes para gerenciar a carga em seu cluster.</span><span class="sxs-lookup"><span data-stu-id="009b8-166">"Balancing" handles two different strategies for managing load in your cluster.</span></span> <span data-ttu-id="009b8-167">É a estratégia padrão que o Gerenciador de Recursos de Cluster usa para distribuir a carga entre os nós no cluster.</span><span class="sxs-lookup"><span data-stu-id="009b8-167">The default strategy that the Cluster Resource Manager uses is to distribute load across the nodes in the cluster.</span></span> <span data-ttu-id="009b8-168">A outra estratégia é [desfragmentação](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="009b8-168">The other strategy is [defragmentation](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span></span> <span data-ttu-id="009b8-169">A desfragmentação é executada durante a mesma execução de balanceamento.</span><span class="sxs-lookup"><span data-stu-id="009b8-169">Defragmentation is performed during the same balancing run.</span></span> <span data-ttu-id="009b8-170">As estratégias de balanceamento e desfragmentação podem ser usadas para métricas diferentes dentro do mesmo cluster.</span><span class="sxs-lookup"><span data-stu-id="009b8-170">The balancing and defragmentation strategies can be used for different metrics within the same cluster.</span></span> <span data-ttu-id="009b8-171">Um serviço pode ter métricas de balanceamento e desfragmentação.</span><span class="sxs-lookup"><span data-stu-id="009b8-171">A service can have both balancing and defragmentation metrics.</span></span> <span data-ttu-id="009b8-172">Para métricas de desfragmentação, a taxa de cargas no cluster dispara o rebalanceamento quando ele estiver _abaixo_ do limite de balanceamento.</span><span class="sxs-lookup"><span data-stu-id="009b8-172">For defragmentation metrics, the ratio of the loads in the cluster triggers rebalancing when it is _below_ the balancing threshold.</span></span> 
>

<span data-ttu-id="009b8-173">Obtendo abaixo do limite de balanceamento não é um objetivo explícito.</span><span class="sxs-lookup"><span data-stu-id="009b8-173">Getting below the balancing threshold is not an explicit goal.</span></span> <span data-ttu-id="009b8-174">Limites de Balanceamento são apenas um *gatilho*.</span><span class="sxs-lookup"><span data-stu-id="009b8-174">Balancing Thresholds are just a *trigger*.</span></span> <span data-ttu-id="009b8-175">Quando balanceamento é executado, o Gerenciador de Recursos de Cluster determina quais melhorias ele pode fazer, se houver alguma.</span><span class="sxs-lookup"><span data-stu-id="009b8-175">When balancing runs, the Cluster Resource Manager determines what improvements it can make, if any.</span></span> <span data-ttu-id="009b8-176">Só porque uma pesquisa de balanceamento é iniciada não significa que nada será movimentado.</span><span class="sxs-lookup"><span data-stu-id="009b8-176">Just because a balancing search is kicked off doesn't mean anything moves.</span></span> <span data-ttu-id="009b8-177">Às vezes, o cluster é desequilibrado, mas fica muito restrito para corrigir.</span><span class="sxs-lookup"><span data-stu-id="009b8-177">Sometimes the cluster is imbalanced but too constrained to correct.</span></span> <span data-ttu-id="009b8-178">Como alternativa, os aprimoramentos exigem movimentações muito [dispendiosas](service-fabric-cluster-resource-manager-movement-cost.md)).</span><span class="sxs-lookup"><span data-stu-id="009b8-178">Alternatively, the improvements require movements that are too [costly](service-fabric-cluster-resource-manager-movement-cost.md)).</span></span>

## <a name="activity-thresholds"></a><span data-ttu-id="009b8-179">Limites de Atividade</span><span class="sxs-lookup"><span data-stu-id="009b8-179">Activity thresholds</span></span>
<span data-ttu-id="009b8-180">Às vezes, embora os nós estejam relativamente desequilibrados, a quantidade *total* de carga no cluster é baixa.</span><span class="sxs-lookup"><span data-stu-id="009b8-180">Sometimes, although nodes are relatively imbalanced, the *total* amount of load in the cluster is low.</span></span> <span data-ttu-id="009b8-181">A falta de carga pode ser um dip transitório, ou porque o cluster é novo e está apenas começando a ser inicializado.</span><span class="sxs-lookup"><span data-stu-id="009b8-181">The lack of load could be a transient dip, or because the cluster is new and just getting bootstrapped.</span></span> <span data-ttu-id="009b8-182">Em ambos os casos, talvez não queira gastar tempo o cluster de balanceamento porque não há muito a ser obtido.</span><span class="sxs-lookup"><span data-stu-id="009b8-182">In either case, you may not want to spend time balancing the cluster because there’s little to be gained.</span></span> <span data-ttu-id="009b8-183">Se o cluster passou por balanceamento, você gastaria recursos de rede e computação para mover as coisas sem fazer uma diferença *absoluta*.</span><span class="sxs-lookup"><span data-stu-id="009b8-183">If the cluster underwent balancing, you’d spend network and compute resources to move things around without making any large *absolute* difference.</span></span> <span data-ttu-id="009b8-184">Para evitar movimentações desnecessárias, há outro controle conhecido como Limites de Atividade.</span><span class="sxs-lookup"><span data-stu-id="009b8-184">To avoid unnecessary moves, there’s another control known as Activity Thresholds.</span></span> <span data-ttu-id="009b8-185">Limites de atividade permite que você especifique algum limite inferior absoluto para a atividade.</span><span class="sxs-lookup"><span data-stu-id="009b8-185">Activity Thresholds allows you to specify some absolute lower bound for activity.</span></span> <span data-ttu-id="009b8-186">Se nenhum nó está acima desse limite, balanceamento não é disparado mesmo se o limite de balanceamento é atingido.</span><span class="sxs-lookup"><span data-stu-id="009b8-186">If no node is over this threshold, balancing isn't triggered even if the Balancing Threshold is met.</span></span>

<span data-ttu-id="009b8-187">Vamos supor que podemos manter nosso Limite de Balanceamento de três para essa métrica.</span><span class="sxs-lookup"><span data-stu-id="009b8-187">Let’s say that we retain our Balancing Threshold of three for this metric.</span></span> <span data-ttu-id="009b8-188">Vamos supor também que temos um Limite de Atividade de 1536.</span><span class="sxs-lookup"><span data-stu-id="009b8-188">Let's also say we have an Activity Threshold of 1536.</span></span> <span data-ttu-id="009b8-189">No primeiro caso, embora o cluster esteja desequilibrado pelo Limite de Balanceamento, nenhum nó atende ao Limite de Atividade e, portanto, nada acontece.</span><span class="sxs-lookup"><span data-stu-id="009b8-189">In the first case, while the cluster is imbalanced per the Balancing Threshold there's no node meets that Activity Threshold, so nothing happens.</span></span> <span data-ttu-id="009b8-190">No exemplo inferior, Node1 está acima do limite de atividade.</span><span class="sxs-lookup"><span data-stu-id="009b8-190">In the bottom example, Node1 is over the Activity Threshold.</span></span> <span data-ttu-id="009b8-191">Como o Limite de Balanceamento e o Limite de Atividade para a métrica foram ultrapassados, o balanceamento é agendado.</span><span class="sxs-lookup"><span data-stu-id="009b8-191">Since both the Balancing Threshold and the Activity Threshold for the metric are exceeded, balancing is scheduled.</span></span> <span data-ttu-id="009b8-192">Por exemplo, vamos examinar o diagrama a seguir:</span><span class="sxs-lookup"><span data-stu-id="009b8-192">As an example, let's look at the following diagram:</span></span> 

<span data-ttu-id="009b8-193"><center>
![Exemplo de limite de atividade][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="009b8-193"><center>
![Activity Threshold Example][Image3]
</center></span></span>

<span data-ttu-id="009b8-194">Assim como os Limites de Balanceamento, os Limites de Atividade são definidos por métrica por meio da definição do cluster:</span><span class="sxs-lookup"><span data-stu-id="009b8-194">Just like Balancing Thresholds, Activity Thresholds are defined per-metric via the cluster definition:</span></span>

<span data-ttu-id="009b8-195">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="009b8-195">ClusterManifest.xml</span></span>

``` xml
    <Section Name="MetricActivityThresholds">
      <Parameter Name="Memory" Value="1536"/>
    </Section>
```

<span data-ttu-id="009b8-196">via ClusterConfig.json para implantações Autônomas ou Template.json para clusters hospedados pelo Azure:</span><span class="sxs-lookup"><span data-stu-id="009b8-196">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="009b8-197">Limites de balanceamento e atividade estão ambos vinculados a uma métrica específica - balanceamento é disparado somente se o limite de balanceamento e atividade limite é excedido para a mesma métrica.</span><span class="sxs-lookup"><span data-stu-id="009b8-197">Balancing and activity thresholds are both tied to a specific metric - balancing is triggered only if both the Balancing Threshold and Activity Threshold is exceeded for the same metric.</span></span>

## <a name="balancing-services-together"></a><span data-ttu-id="009b8-198">Balanceamento dos serviços em conjunto</span><span class="sxs-lookup"><span data-stu-id="009b8-198">Balancing services together</span></span>
<span data-ttu-id="009b8-199">Se o cluster estiver desequilibrado ou não for uma decisão de todo o cluster.</span><span class="sxs-lookup"><span data-stu-id="009b8-199">Whether the cluster is imbalanced or not is a cluster-wide decision.</span></span> <span data-ttu-id="009b8-200">No entanto, a maneira como nós vamos corrigi-lo é mover réplicas de serviço individuais e instâncias.</span><span class="sxs-lookup"><span data-stu-id="009b8-200">However, the way we go about fixing it is moving individual service replicas and instances around.</span></span> <span data-ttu-id="009b8-201">Isso faz sentido, certo?</span><span class="sxs-lookup"><span data-stu-id="009b8-201">This makes sense, right?</span></span> <span data-ttu-id="009b8-202">Se a memória é empilhada em um nó, várias réplicas ou instâncias podem contribuir para ela.</span><span class="sxs-lookup"><span data-stu-id="009b8-202">If memory is stacked up on one node, multiple replicas or instances could be contributing to it.</span></span> <span data-ttu-id="009b8-203">Corrigir o desequilíbrio pode exigir a movimentação de qualquer uma das réplicas com monitoração de estado ou instâncias sem monitoração de estado que usam a métrica desequilibrada.</span><span class="sxs-lookup"><span data-stu-id="009b8-203">Fixing the imbalance could require moving any of the stateful replicas or stateless instances that use the imbalanced metric.</span></span>

<span data-ttu-id="009b8-204">Ocasionalmente, no entanto, um serviço que não estava desequilibrado é movido (lembre-se da discussão sobre pesos local e global anteriormente).</span><span class="sxs-lookup"><span data-stu-id="009b8-204">Occasionally though, a service that wasn’t itself imbalanced gets moved (remember the discussion of local and global weights earlier).</span></span> <span data-ttu-id="009b8-205">Por que um serviço é movido quando todas as métricas desse serviço foram balanceadas?</span><span class="sxs-lookup"><span data-stu-id="009b8-205">Why would a service get moved when all that service’s metrics were balanced?</span></span> <span data-ttu-id="009b8-206">Vejamos um exemplo:</span><span class="sxs-lookup"><span data-stu-id="009b8-206">Let’s see an example:</span></span>

- <span data-ttu-id="009b8-207">Vamos supor que há quatro serviços, Service1, Service2, Service3 e Service4.</span><span class="sxs-lookup"><span data-stu-id="009b8-207">Let's say there are four services, Service1, Service2, Service3, and Service4.</span></span> 
- <span data-ttu-id="009b8-208">O Service1 relata as métricas Metric1 e Metric2.</span><span class="sxs-lookup"><span data-stu-id="009b8-208">Service1 reports metrics Metric1 and Metric2.</span></span> 
- <span data-ttu-id="009b8-209">O Service2 relata as métricas Metric2 e Metric3.</span><span class="sxs-lookup"><span data-stu-id="009b8-209">Service2 reports metrics Metric2 and Metric3.</span></span> 
- <span data-ttu-id="009b8-210">O Service3 relata as métricas Metric3 e Metric4.</span><span class="sxs-lookup"><span data-stu-id="009b8-210">Service3 reports metrics Metric3 and Metric4.</span></span>
- <span data-ttu-id="009b8-211">O Service4 relata a métrica Metric99.</span><span class="sxs-lookup"><span data-stu-id="009b8-211">Service4 reports metric Metric99.</span></span> 

<span data-ttu-id="009b8-212">Certamente, você consegue ver onde queremos chegar: há uma cadeia!</span><span class="sxs-lookup"><span data-stu-id="009b8-212">Surely you can see where we’re going here: There's a chain!</span></span> <span data-ttu-id="009b8-213">Realmente, não há quatro serviços independentes. Temos três serviços relacionados e um que está por conta própria.</span><span class="sxs-lookup"><span data-stu-id="009b8-213">We don’t really have four independent services, we have three services that are related and one that is off on its own.</span></span>

<span data-ttu-id="009b8-214"><center>
![Balanceamento dos serviços em conjunto][Image4]
</center></span><span class="sxs-lookup"><span data-stu-id="009b8-214"><center>
![Balancing Services Together][Image4]
</center></span></span>

<span data-ttu-id="009b8-215">Devido a essa cadeia, é possível que um desequilíbrio nas métricas 1 a 4 possa mover as réplicas ou instâncias pertencentes aos serviços 1 a 3.</span><span class="sxs-lookup"><span data-stu-id="009b8-215">Because of this chain, it's possible that an imbalance in metrics 1-4 can cause replicas or instances belonging to services 1-3 to move around.</span></span> <span data-ttu-id="009b8-216">Também sabemos que um desequilíbrio nas métricas de 1, 2 ou 3 não pode causar movimentos no Service4.</span><span class="sxs-lookup"><span data-stu-id="009b8-216">We also know that an imbalance in Metrics 1, 2, or 3 can't cause movements in Service4.</span></span> <span data-ttu-id="009b8-217">Não haveria nenhum ponto desde movendo as réplicas ou instâncias pertencentes a Serviço4 ao redor podem fazer absolutamente nada para afetar o saldo das métricas de 1 a 3.</span><span class="sxs-lookup"><span data-stu-id="009b8-217">There would be no point since moving the replicas or instances belonging to Service4 around can do absolutely nothing to impact the balance of Metrics 1-3.</span></span>

<span data-ttu-id="009b8-218">O Gerenciador de Recursos de Cluster descobre automaticamente quais serviços estão relacionados.</span><span class="sxs-lookup"><span data-stu-id="009b8-218">The Cluster Resource Manager automatically figures out what services are related.</span></span> <span data-ttu-id="009b8-219">A adição, remoção ou alteração das métrica para esses serviços pode afetar suas relações.</span><span class="sxs-lookup"><span data-stu-id="009b8-219">Adding, removing, or changing the metrics for services can impact their relationships.</span></span> <span data-ttu-id="009b8-220">Por exemplo, entre duas execuções de balanceamento, o Service2 pode ter sido atualizado para remover Metric2.</span><span class="sxs-lookup"><span data-stu-id="009b8-220">For example, between two runs of balancing Service2 may have been updated to remove Metric2.</span></span> <span data-ttu-id="009b8-221">Isso interromperá a cadeia entre Service1 e Service2.</span><span class="sxs-lookup"><span data-stu-id="009b8-221">This breaks the chain between Service1 and Service2.</span></span> <span data-ttu-id="009b8-222">Agora, em vez de dois grupos de serviços relacionados, há três:</span><span class="sxs-lookup"><span data-stu-id="009b8-222">Now instead of two groups of related services, there are three:</span></span>

<span data-ttu-id="009b8-223"><center>
![Balanceamento dos serviços em conjunto][Image5]
</center></span><span class="sxs-lookup"><span data-stu-id="009b8-223"><center>
![Balancing Services Together][Image5]
</center></span></span>

## <a name="next-steps"></a><span data-ttu-id="009b8-224">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="009b8-224">Next steps</span></span>
* <span data-ttu-id="009b8-225">As métricas são como o Gerenciador de Recursos de Cluster do Service Fabric gerencia o consumo e a capacidade no cluster.</span><span class="sxs-lookup"><span data-stu-id="009b8-225">Metrics are how the Service Fabric Cluster Resource Manger manages consumption and capacity in the cluster.</span></span> <span data-ttu-id="009b8-226">Para saber mais sobre as métricas e como configurá-las, confira [este artigo](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="009b8-226">To learn more about metrics and how to configure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>
* <span data-ttu-id="009b8-227">O Custo de Movimento é uma forma de sinalizar para o Gerenciador de Recursos de Cluster que a movimentação de determinados serviços é mais cara do que para outros.</span><span class="sxs-lookup"><span data-stu-id="009b8-227">Movement Cost is one way of signaling to the Cluster Resource Manager that certain services are more expensive to move than others.</span></span> <span data-ttu-id="009b8-228">Para saber mais sobre o custo de movimento, consulte [este artigo](service-fabric-cluster-resource-manager-movement-cost.md)</span><span class="sxs-lookup"><span data-stu-id="009b8-228">For more about movement cost, refer to [this article](service-fabric-cluster-resource-manager-movement-cost.md)</span></span>
* <span data-ttu-id="009b8-229">O Resource Manager do Cluster tem várias limitações que você pode configurar para diminuir a variação no cluster.</span><span class="sxs-lookup"><span data-stu-id="009b8-229">The Cluster Resource Manager has several throttles that you can configure to slow down churn in the cluster.</span></span> <span data-ttu-id="009b8-230">Normalmente, eles não são necessários, mas você poderá aprender mais sobre eles [aqui](service-fabric-cluster-resource-manager-advanced-throttling.md)</span><span class="sxs-lookup"><span data-stu-id="009b8-230">They're not normally necessary, but if you need them you can learn about them [here](service-fabric-cluster-resource-manager-advanced-throttling.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resrouce-manager-balancing-thresholds.png
[Image2]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-threshold-triggered-results.png
[Image3]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-activity-thresholds.png
[Image4]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together1.png
[Image5]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together2.png
