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
# <a name="balancing-your-service-fabric-cluster"></a><span data-ttu-id="b6438-103">Balanceamento do cluster do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b6438-103">Balancing your service fabric cluster</span></span>
<span data-ttu-id="b6438-104">Olá Gerenciador de recursos de Cluster do serviço de malha dá suporte a alterações de carga dinâmico, reagindo tooadditions ou remoções de nós ou serviços.</span><span class="sxs-lookup"><span data-stu-id="b6438-104">hello Service Fabric Cluster Resource Manager supports dynamic load changes, reacting tooadditions or removals of nodes or services.</span></span> <span data-ttu-id="b6438-105">Ele também corrige automaticamente as violações de restrição e redistribui proativamente cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b6438-105">It also automatically corrects constraint violations, and proactively rebalances hello cluster.</span></span> <span data-ttu-id="b6438-106">Mas com que frequência essas ações são executadas, e o que as dispara?</span><span class="sxs-lookup"><span data-stu-id="b6438-106">But how often are these actions taken, and what triggers them?</span></span>

<span data-ttu-id="b6438-107">Há três categorias diferentes de trabalho que executa o Gerenciador de recursos de Cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="b6438-107">There are three different categories of work that hello Cluster Resource Manager performs.</span></span> <span data-ttu-id="b6438-108">Eles são:</span><span class="sxs-lookup"><span data-stu-id="b6438-108">They are:</span></span>

1. <span data-ttu-id="b6438-109">Posicionamento – esse estágio lida com o posicionamento de réplicas com estado ou de instâncias sem estado que estejam ausentes.</span><span class="sxs-lookup"><span data-stu-id="b6438-109">Placement – this stage deals with placing any stateful replicas or stateless instances that are missing.</span></span> <span data-ttu-id="b6438-110">O posicionamento inclui os novos serviços e a manipulação de réplicas com estado ou de instâncias sem estado que falharam.</span><span class="sxs-lookup"><span data-stu-id="b6438-110">Placement includes both new services and handling stateful replicas or stateless instances that have failed.</span></span> <span data-ttu-id="b6438-111">A exclusão e o descarte de réplicas ou de instâncias são tratados aqui.</span><span class="sxs-lookup"><span data-stu-id="b6438-111">Deleting and dropping replicas or instances are handled here.</span></span>
2. <span data-ttu-id="b6438-112">Verificações de restrição – neste estágio verifica e corrige violações de restrições de posicionamento diferentes hello (regras) no sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="b6438-112">Constraint Checks – this stage checks for and corrects violations of hello different placement constraints (rules) within hello system.</span></span> <span data-ttu-id="b6438-113">Os exemplos de regras são a garantia de que os nós não estão acima da capacidade e se as restrições de posicionamento do serviço estão sendo atendidas.</span><span class="sxs-lookup"><span data-stu-id="b6438-113">Examples of rules are things like ensuring that nodes are not over capacity and that a service’s placement constraints are met.</span></span>
3. <span data-ttu-id="b6438-114">Balanceamento – neste estágio verifica toosee se rebalanceamento é necessário com base em Olá configurado desejado de nível de saldo para diferentes métricas.</span><span class="sxs-lookup"><span data-stu-id="b6438-114">Balancing – this stage checks toosee if rebalancing is necessary based on hello configured desired level of balance for different metrics.</span></span> <span data-ttu-id="b6438-115">Nesse caso, ele tenta toofind que é de uma organização em Olá cluster mais balanceada.</span><span class="sxs-lookup"><span data-stu-id="b6438-115">If so it attempts toofind an arrangement in hello cluster that is more balanced.</span></span>

## <a name="configuring-cluster-resource-manager-timers"></a><span data-ttu-id="b6438-116">Configuração de temporizadores do Gerenciador de Recursos de Cluster</span><span class="sxs-lookup"><span data-stu-id="b6438-116">Configuring Cluster Resource Manager Timers</span></span>
<span data-ttu-id="b6438-117">Olá primeiro conjunto de controles balanceamento são um conjunto de temporizadores.</span><span class="sxs-lookup"><span data-stu-id="b6438-117">hello first set of controls around balancing are a set of timers.</span></span> <span data-ttu-id="b6438-118">Esses temporizadores governam frequência hello Gerenciador de recursos de Cluster examina cluster hello e executa ações corretivas.</span><span class="sxs-lookup"><span data-stu-id="b6438-118">These timers govern how often hello Cluster Resource Manager examines hello cluster and takes corrective actions.</span></span>

<span data-ttu-id="b6438-119">Cada um desses tipos diferentes de saudação correções Gerenciador de recursos de Cluster pode fazer é controlada por um timer diferente que rege sua frequência.</span><span class="sxs-lookup"><span data-stu-id="b6438-119">Each of these different types of corrections hello Cluster Resource Manager can make is controlled by a different timer that governs its frequency.</span></span> <span data-ttu-id="b6438-120">Quando cada temporizador é acionado, Olá será agendada.</span><span class="sxs-lookup"><span data-stu-id="b6438-120">When each timer fires, hello task is scheduled.</span></span> <span data-ttu-id="b6438-121">Por padrão, Olá Gerenciador de recursos:</span><span class="sxs-lookup"><span data-stu-id="b6438-121">By default hello Resource Manager:</span></span>

* <span data-ttu-id="b6438-122">verifica o estado e aplica atualizações (como gravação de um nó estiver inativo) cada 1/10 de segundo</span><span class="sxs-lookup"><span data-stu-id="b6438-122">scans its state and applies updates (like recording that a node is down) every 1/10th of a second</span></span>
* <span data-ttu-id="b6438-123">Define o sinalizador de verificação de posicionamento de saudação</span><span class="sxs-lookup"><span data-stu-id="b6438-123">sets hello placement check flag</span></span> 
* <span data-ttu-id="b6438-124">Define o sinalizador de verificação de restrição de saudação por segundo</span><span class="sxs-lookup"><span data-stu-id="b6438-124">sets hello constraint check flag every second</span></span>
* <span data-ttu-id="b6438-125">Define Olá balanceamento sinalizador a cada cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="b6438-125">sets hello balancing flag every five seconds.</span></span>

<span data-ttu-id="b6438-126">A seguir estão exemplos de configuração de saudação que governam esses temporizadores:</span><span class="sxs-lookup"><span data-stu-id="b6438-126">Examples of hello configuration governing these timers are below:</span></span>

<span data-ttu-id="b6438-127">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="b6438-127">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PLBRefreshGap" Value="0.1" />
            <Parameter Name="MinPlacementInterval" Value="1.0" />
            <Parameter Name="MinConstraintCheckInterval" Value="1.0" />
            <Parameter Name="MinLoadBalancingInterval" Value="5.0" />
        </Section>
```

<span data-ttu-id="b6438-128">via ClusterConfig.json para implantações Autônomas ou Template.json para clusters hospedados pelo Azure:</span><span class="sxs-lookup"><span data-stu-id="b6438-128">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="b6438-129">Hoje Olá Gerenciador de recursos de Cluster só executa uma dessas ações ao mesmo tempo, em sequência.</span><span class="sxs-lookup"><span data-stu-id="b6438-129">Today hello Cluster Resource Manager only performs one of these actions at a time, sequentially.</span></span> <span data-ttu-id="b6438-130">É por isso, consulte temporizadores toothese como "intervalos mínimo" e Olá ações serão direcionadas quando temporizadores Olá desligam como "sinalizadores de configuração".</span><span class="sxs-lookup"><span data-stu-id="b6438-130">This is why we refer toothese timers as “minimum intervals” and hello actions that get taken when hello timers go off as "setting flags".</span></span> <span data-ttu-id="b6438-131">Por exemplo, Olá Gerenciador de recursos de Cluster se encarrega de pendente solicitações toocreate services antes de saudação cluster de balanceamento.</span><span class="sxs-lookup"><span data-stu-id="b6438-131">For example, hello Cluster Resource Manager takes care of pending requests toocreate services before balancing hello cluster.</span></span> <span data-ttu-id="b6438-132">Como você pode ver por intervalos de tempo padrão de saudação especificados, Olá Gerenciador de recursos de Cluster procura nada-toodo necessidades com frequência.</span><span class="sxs-lookup"><span data-stu-id="b6438-132">As you can see by hello default time intervals specified, hello Cluster Resource Manager scans for anything it needs toodo frequently.</span></span> <span data-ttu-id="b6438-133">Normalmente, isso significa que o conjunto de saudação das alterações feitas durante cada etapa é pequeno.</span><span class="sxs-lookup"><span data-stu-id="b6438-133">Normally this means that hello set of changes made during each step is small.</span></span> <span data-ttu-id="b6438-134">Fazer pequenas alterações com frequência permite Olá toobe do Gerenciador de recursos de Cluster responsivo quando as coisas acontecem no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b6438-134">Making small changes frequently allows hello Cluster Resource Manager toobe responsive when things happen in hello cluster.</span></span> <span data-ttu-id="b6438-135">Olá cronômetros padrão fornecem algumas envio em lote desde muitas Olá mesmo tipos de eventos tendem toooccur simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="b6438-135">hello default timers provide some batching since many of hello same types of events tend toooccur simultaneously.</span></span> 

<span data-ttu-id="b6438-136">Por exemplo, quando os nós falham, eles podem fazer com um domínio de falha inteiro por vez.</span><span class="sxs-lookup"><span data-stu-id="b6438-136">For example, when nodes fail they can do so entire fault domains at a time.</span></span> <span data-ttu-id="b6438-137">Todas essas falhas são capturadas durante o próximo estado de saudação atualizar após Olá *PLBRefreshGap*.</span><span class="sxs-lookup"><span data-stu-id="b6438-137">All these failures are captured during hello next state update after hello *PLBRefreshGap*.</span></span> <span data-ttu-id="b6438-138">correções de saudação são determinadas durante a saudação posicionamento, verificação de restrição, a seguir e balanceamento é executado.</span><span class="sxs-lookup"><span data-stu-id="b6438-138">hello corrections are determined during hello following placement, constraint check, and balancing runs.</span></span> <span data-ttu-id="b6438-139">Por saudação padrão Gerenciador de recursos de Cluster não é uma varredura horas das alterações no cluster de saudação e tentar tooaddress todas as alterações de uma vez.</span><span class="sxs-lookup"><span data-stu-id="b6438-139">By default hello Cluster Resource Manager is not scanning through hours of changes in hello cluster and trying tooaddress all changes at once.</span></span> <span data-ttu-id="b6438-140">Isso levaria toobursts de variação.</span><span class="sxs-lookup"><span data-stu-id="b6438-140">Doing so would lead toobursts of churn.</span></span>

<span data-ttu-id="b6438-141">Olá Gerenciador de recursos de Cluster também precisa toodetermine algumas informações adicionais se Olá cluster desequilibrados.</span><span class="sxs-lookup"><span data-stu-id="b6438-141">hello Cluster Resource Manager also needs some additional information toodetermine if hello cluster imbalanced.</span></span> <span data-ttu-id="b6438-142">Para isso, temos duas outras configurações: *Limites de Balanceamento* e *Limites de Atividade*.</span><span class="sxs-lookup"><span data-stu-id="b6438-142">For that we have two other pieces of configuration: *BalancingThresholds* and *ActivityThresholds*.</span></span>

## <a name="balancing-thresholds"></a><span data-ttu-id="b6438-143">Limites de balanceamento</span><span class="sxs-lookup"><span data-stu-id="b6438-143">Balancing thresholds</span></span>
<span data-ttu-id="b6438-144">Um limite de balanceamento é controle principal de saudação para o disparo de rebalanceamento.</span><span class="sxs-lookup"><span data-stu-id="b6438-144">A Balancing Threshold is hello main control for triggering rebalancing.</span></span> <span data-ttu-id="b6438-145">Olá balanceamento limites para uma métrica é um _taxa_.</span><span class="sxs-lookup"><span data-stu-id="b6438-145">hello Balancing Threshold for a metric is a _ratio_.</span></span> <span data-ttu-id="b6438-146">Se carga Olá para uma métrica em hello mais carregado nó dividido pela quantidade de saudação de carga em Olá menos carregado nó excede essa métrica *BalancingThreshold*, cluster Olá é desequilibrado.</span><span class="sxs-lookup"><span data-stu-id="b6438-146">If hello load for a metric on hello most loaded node divided by hello amount of load on hello least loaded node exceeds that metric's *BalancingThreshold*, then hello cluster is imbalanced.</span></span> <span data-ttu-id="b6438-147">Como resultado de balanceamento é disparada Olá hello do tempo Avançar verifica se o Gerenciador de recursos de Cluster.</span><span class="sxs-lookup"><span data-stu-id="b6438-147">As a result balancing is triggered hello next time hello Cluster Resource Manager checks.</span></span> <span data-ttu-id="b6438-148">Olá *MinLoadBalancingInterval* timer define a frequência hello Gerenciador de recursos de Cluster deve verificar se o rebalanceamento é necessário.</span><span class="sxs-lookup"><span data-stu-id="b6438-148">hello *MinLoadBalancingInterval* timer defines how often hello Cluster Resource Manager should check if rebalancing is necessary.</span></span> <span data-ttu-id="b6438-149">A verificação não significa que nada acontece.</span><span class="sxs-lookup"><span data-stu-id="b6438-149">Checking doesn't mean that anything happens.</span></span> 

<span data-ttu-id="b6438-150">Os limites de balanceamento são definidos em uma base por métrica como parte da definição de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b6438-150">Balancing Thresholds are defined on a per-metric basis as a part of hello cluster definition.</span></span> <span data-ttu-id="b6438-151">Para saber mais sobre como fazer isso, leia [este artigo](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="b6438-151">For more information on metrics, check out [this article](service-fabric-cluster-resource-manager-metrics.md).</span></span>

<span data-ttu-id="b6438-152">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="b6438-152">ClusterManifest.xml</span></span>

```xml
    <Section Name="MetricBalancingThresholds">
      <Parameter Name="MetricName1" Value="2"/>
      <Parameter Name="MetricName2" Value="3.5"/>
    </Section>
```

<span data-ttu-id="b6438-153">via ClusterConfig.json para implantações Autônomas ou Template.json para clusters hospedados pelo Azure:</span><span class="sxs-lookup"><span data-stu-id="b6438-153">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="b6438-154"><center>
![Exemplo de Limite de Balanceamento][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="b6438-154"><center>
![Balancing Threshold Example][Image1]
</center></span></span>

<span data-ttu-id="b6438-155">Neste exemplo, cada serviço está consumindo uma unidade de alguma métrica.</span><span class="sxs-lookup"><span data-stu-id="b6438-155">In this example, each service is consuming one unit of some metric.</span></span> <span data-ttu-id="b6438-156">No exemplo de superior hello, a carga máxima Olá em um nó é 5 e Olá mínimo é de dois.</span><span class="sxs-lookup"><span data-stu-id="b6438-156">In hello top example, hello maximum load on a node is five and hello minimum is two.</span></span> <span data-ttu-id="b6438-157">Digamos que Olá balanceamento limite para esta métrica é três.</span><span class="sxs-lookup"><span data-stu-id="b6438-157">Let’s say that hello balancing threshold for this metric is three.</span></span> <span data-ttu-id="b6438-158">Desde que a taxa de saudação em cluster Olá é 5/2 = 2.5 e é inferior ao especificado de saudação balanceamento limite de três, cluster de saudação é equilibrada.</span><span class="sxs-lookup"><span data-stu-id="b6438-158">Since hello ratio in hello cluster is 5/2 = 2.5 and that is less than hello specified balancing threshold of three, hello cluster is balanced.</span></span> <span data-ttu-id="b6438-159">Sem balanceamento é disparada quando verifica Olá Gerenciador de recursos de Cluster.</span><span class="sxs-lookup"><span data-stu-id="b6438-159">No balancing is triggered when hello Cluster Resource Manager checks.</span></span>

<span data-ttu-id="b6438-160">No exemplo do hello inferior, a carga máxima Olá em um nó é 10, enquanto o mínimo de saudação é dois, resultando em uma taxa de cinco.</span><span class="sxs-lookup"><span data-stu-id="b6438-160">In hello bottom example, hello maximum load on a node is 10, while hello minimum is two, resulting in a ratio of five.</span></span> <span data-ttu-id="b6438-161">Cinco é maior que o limite de balanceamento designado Olá de três para métrica.</span><span class="sxs-lookup"><span data-stu-id="b6438-161">Five is greater than hello designated balancing threshold of three for that metric.</span></span> <span data-ttu-id="b6438-162">Como resultado, uma execução rebalanceamento será agendado Avançar Olá de tempo balanceamento timer acionado.</span><span class="sxs-lookup"><span data-stu-id="b6438-162">As a result, a rebalancing run will be scheduled next time hello balancing timer fires.</span></span> <span data-ttu-id="b6438-163">Em situações como essa alguma carga é tooNode3 normalmente distribuído.</span><span class="sxs-lookup"><span data-stu-id="b6438-163">In a situation like this some load is usually distributed tooNode3.</span></span> <span data-ttu-id="b6438-164">Como Olá Gerenciador de recursos de Cluster do serviço de malha não usa uma abordagem greedy, alguma carga também pode ser distribuídos tooNode2.</span><span class="sxs-lookup"><span data-stu-id="b6438-164">Because hello Service Fabric Cluster Resource Manager doesn't use a greedy approach, some load could also be distributed tooNode2.</span></span> 

<span data-ttu-id="b6438-165"><center>
![Ações de exemplo de Limite de Balanceamento][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="b6438-165"><center>
![Balancing Threshold Example Actions][Image2]
</center></span></span>

> [!NOTE]
> <span data-ttu-id="b6438-166">O "Balanceamento" trata duas estratégias diferentes para gerenciar a carga em seu cluster.</span><span class="sxs-lookup"><span data-stu-id="b6438-166">"Balancing" handles two different strategies for managing load in your cluster.</span></span> <span data-ttu-id="b6438-167">estratégia de padrão de Olá Olá usa o Gerenciador de recursos de Cluster é toodistribute carga em nós de saudação em cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="b6438-167">hello default strategy that hello Cluster Resource Manager uses is toodistribute load across hello nodes in hello cluster.</span></span> <span data-ttu-id="b6438-168">Olá outra estratégia é [desfragmentação](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="b6438-168">hello other strategy is [defragmentation](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span></span> <span data-ttu-id="b6438-169">A desfragmentação é executada durante a saudação balanceamento mesma execução.</span><span class="sxs-lookup"><span data-stu-id="b6438-169">Defragmentation is performed during hello same balancing run.</span></span> <span data-ttu-id="b6438-170">Hello balanceamento e desfragmentação estratégias podem ser usadas para diferentes métricas em Olá mesmo cluster.</span><span class="sxs-lookup"><span data-stu-id="b6438-170">hello balancing and defragmentation strategies can be used for different metrics within hello same cluster.</span></span> <span data-ttu-id="b6438-171">Um serviço pode ter métricas de balanceamento e desfragmentação.</span><span class="sxs-lookup"><span data-stu-id="b6438-171">A service can have both balancing and defragmentation metrics.</span></span> <span data-ttu-id="b6438-172">Para métricas de desfragmentação, taxa de saudação do hello carrega em gatilhos de cluster Olá rebalanceamento quando é _abaixo_ Olá balanceamento de limite.</span><span class="sxs-lookup"><span data-stu-id="b6438-172">For defragmentation metrics, hello ratio of hello loads in hello cluster triggers rebalancing when it is _below_ hello balancing threshold.</span></span> 
>

<span data-ttu-id="b6438-173">Obtendo abaixo Olá balanceamento limite não é um objetivo explícito.</span><span class="sxs-lookup"><span data-stu-id="b6438-173">Getting below hello balancing threshold is not an explicit goal.</span></span> <span data-ttu-id="b6438-174">Limites de Balanceamento são apenas um *gatilho*.</span><span class="sxs-lookup"><span data-stu-id="b6438-174">Balancing Thresholds are just a *trigger*.</span></span> <span data-ttu-id="b6438-175">Quando é executado de balanceamento, Olá Gerenciador de recursos de Cluster determina quais melhorias pode fazer, se houver.</span><span class="sxs-lookup"><span data-stu-id="b6438-175">When balancing runs, hello Cluster Resource Manager determines what improvements it can make, if any.</span></span> <span data-ttu-id="b6438-176">Só porque uma pesquisa de balanceamento é iniciada não significa que nada será movimentado.</span><span class="sxs-lookup"><span data-stu-id="b6438-176">Just because a balancing search is kicked off doesn't mean anything moves.</span></span> <span data-ttu-id="b6438-177">Às vezes hello cluster é toocorrect desequilibrado, mas muito restrita.</span><span class="sxs-lookup"><span data-stu-id="b6438-177">Sometimes hello cluster is imbalanced but too constrained toocorrect.</span></span> <span data-ttu-id="b6438-178">Como alternativa, melhorias de saudação exigem movimentações são muito [cara](service-fabric-cluster-resource-manager-movement-cost.md)).</span><span class="sxs-lookup"><span data-stu-id="b6438-178">Alternatively, hello improvements require movements that are too [costly](service-fabric-cluster-resource-manager-movement-cost.md)).</span></span>

## <a name="activity-thresholds"></a><span data-ttu-id="b6438-179">Limites de Atividade</span><span class="sxs-lookup"><span data-stu-id="b6438-179">Activity thresholds</span></span>
<span data-ttu-id="b6438-180">Às vezes, embora nós são relativamente desequilibrados, Olá *total* quantidade de carga no cluster Olá é baixa.</span><span class="sxs-lookup"><span data-stu-id="b6438-180">Sometimes, although nodes are relatively imbalanced, hello *total* amount of load in hello cluster is low.</span></span> <span data-ttu-id="b6438-181">falta de saudação de carga pode ser um dip transitório, ou porque o cluster Olá é novo e apenas obtendo inicializar.</span><span class="sxs-lookup"><span data-stu-id="b6438-181">hello lack of load could be a transient dip, or because hello cluster is new and just getting bootstrapped.</span></span> <span data-ttu-id="b6438-182">Em ambos os casos, não convém toospend tempo balanceamento cluster Olá porque não há pouco toobe obtido.</span><span class="sxs-lookup"><span data-stu-id="b6438-182">In either case, you may not want toospend time balancing hello cluster because there’s little toobe gained.</span></span> <span data-ttu-id="b6438-183">Se o cluster Olá sofreu balanceamento, você gastar rede e itens toomove recursos de computação sem fazer qualquer grande *absoluto* diferença.</span><span class="sxs-lookup"><span data-stu-id="b6438-183">If hello cluster underwent balancing, you’d spend network and compute resources toomove things around without making any large *absolute* difference.</span></span> <span data-ttu-id="b6438-184">Move tooavoid desnecessária, há outro controle conhecido como limites de atividade.</span><span class="sxs-lookup"><span data-stu-id="b6438-184">tooavoid unnecessary moves, there’s another control known as Activity Thresholds.</span></span> <span data-ttu-id="b6438-185">Limites de atividade permite que você toospecify alguns inferior absoluto associada para a atividade.</span><span class="sxs-lookup"><span data-stu-id="b6438-185">Activity Thresholds allows you toospecify some absolute lower bound for activity.</span></span> <span data-ttu-id="b6438-186">Se nenhum nó está acima desse limite, balanceamento não é disparado mesmo se hello balanceamento limite é atingido.</span><span class="sxs-lookup"><span data-stu-id="b6438-186">If no node is over this threshold, balancing isn't triggered even if hello Balancing Threshold is met.</span></span>

<span data-ttu-id="b6438-187">Vamos supor que podemos manter nosso Limite de Balanceamento de três para essa métrica.</span><span class="sxs-lookup"><span data-stu-id="b6438-187">Let’s say that we retain our Balancing Threshold of three for this metric.</span></span> <span data-ttu-id="b6438-188">Vamos supor também que temos um Limite de Atividade de 1536.</span><span class="sxs-lookup"><span data-stu-id="b6438-188">Let's also say we have an Activity Threshold of 1536.</span></span> <span data-ttu-id="b6438-189">No primeiro caso de Olá, enquanto o cluster Olá é desequilibrado por Olá balanceamento limite existe não é atende nenhum nó que esse limite de atividade, assim, nada acontece.</span><span class="sxs-lookup"><span data-stu-id="b6438-189">In hello first case, while hello cluster is imbalanced per hello Balancing Threshold there's no node meets that Activity Threshold, so nothing happens.</span></span> <span data-ttu-id="b6438-190">No exemplo de inferior hello, Node1 está acima Olá limite de atividade.</span><span class="sxs-lookup"><span data-stu-id="b6438-190">In hello bottom example, Node1 is over hello Activity Threshold.</span></span> <span data-ttu-id="b6438-191">Como ambos Olá limite balanceamento e Olá limite de atividade de métrica de saudação são excedidos, balanceamento está agendado.</span><span class="sxs-lookup"><span data-stu-id="b6438-191">Since both hello Balancing Threshold and hello Activity Threshold for hello metric are exceeded, balancing is scheduled.</span></span> <span data-ttu-id="b6438-192">Por exemplo, vamos examinar Olá diagrama a seguir:</span><span class="sxs-lookup"><span data-stu-id="b6438-192">As an example, let's look at hello following diagram:</span></span> 

<span data-ttu-id="b6438-193"><center>
![Exemplo de limite de atividade][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="b6438-193"><center>
![Activity Threshold Example][Image3]
</center></span></span>

<span data-ttu-id="b6438-194">Assim como os limites de balanceamento, limites de atividade são definidos por métrica por meio da definição de cluster hello:</span><span class="sxs-lookup"><span data-stu-id="b6438-194">Just like Balancing Thresholds, Activity Thresholds are defined per-metric via hello cluster definition:</span></span>

<span data-ttu-id="b6438-195">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="b6438-195">ClusterManifest.xml</span></span>

``` xml
    <Section Name="MetricActivityThresholds">
      <Parameter Name="Memory" Value="1536"/>
    </Section>
```

<span data-ttu-id="b6438-196">via ClusterConfig.json para implantações Autônomas ou Template.json para clusters hospedados pelo Azure:</span><span class="sxs-lookup"><span data-stu-id="b6438-196">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="b6438-197">Limites de balanceamento e atividades são ambos métrica específica de tooa empatados - balanceamento é acionada somente se ambos Olá limite balanceamento e limite de atividade foi excedido para a saudação mesma métrica.</span><span class="sxs-lookup"><span data-stu-id="b6438-197">Balancing and activity thresholds are both tied tooa specific metric - balancing is triggered only if both hello Balancing Threshold and Activity Threshold is exceeded for hello same metric.</span></span>

## <a name="balancing-services-together"></a><span data-ttu-id="b6438-198">Balanceamento dos serviços em conjunto</span><span class="sxs-lookup"><span data-stu-id="b6438-198">Balancing services together</span></span>
<span data-ttu-id="b6438-199">Se o cluster de saudação é desequilibrado ou não é uma decisão de todo o cluster.</span><span class="sxs-lookup"><span data-stu-id="b6438-199">Whether hello cluster is imbalanced or not is a cluster-wide decision.</span></span> <span data-ttu-id="b6438-200">No entanto, realizamos corrigi-lo de forma de saudação é mover instâncias ao redor e réplicas de serviço individual.</span><span class="sxs-lookup"><span data-stu-id="b6438-200">However, hello way we go about fixing it is moving individual service replicas and instances around.</span></span> <span data-ttu-id="b6438-201">Isso faz sentido, certo?</span><span class="sxs-lookup"><span data-stu-id="b6438-201">This makes sense, right?</span></span> <span data-ttu-id="b6438-202">Se a memória é empilhada em um nó, várias réplicas ou instâncias podem estar contribuindo tooit.</span><span class="sxs-lookup"><span data-stu-id="b6438-202">If memory is stacked up on one node, multiple replicas or instances could be contributing tooit.</span></span> <span data-ttu-id="b6438-203">Corrigindo desequilíbrio de saudação pode exigir a movimentação de qualquer uma das réplicas com monitoração de estado hello ou instâncias sem monitoração de estado que usam métrica desequilibrados hello.</span><span class="sxs-lookup"><span data-stu-id="b6438-203">Fixing hello imbalance could require moving any of hello stateful replicas or stateless instances that use hello imbalanced metric.</span></span>

<span data-ttu-id="b6438-204">Ocasionalmente, no entanto, um serviço que não estava em si desequilibrados foi movido (Lembre-se de discussão de saudação do local e global pondera anteriormente).</span><span class="sxs-lookup"><span data-stu-id="b6438-204">Occasionally though, a service that wasn’t itself imbalanced gets moved (remember hello discussion of local and global weights earlier).</span></span> <span data-ttu-id="b6438-205">Por que um serviço é movido quando todas as métricas desse serviço foram balanceadas?</span><span class="sxs-lookup"><span data-stu-id="b6438-205">Why would a service get moved when all that service’s metrics were balanced?</span></span> <span data-ttu-id="b6438-206">Vejamos um exemplo:</span><span class="sxs-lookup"><span data-stu-id="b6438-206">Let’s see an example:</span></span>

- <span data-ttu-id="b6438-207">Vamos supor que há quatro serviços, Service1, Service2, Service3 e Service4.</span><span class="sxs-lookup"><span data-stu-id="b6438-207">Let's say there are four services, Service1, Service2, Service3, and Service4.</span></span> 
- <span data-ttu-id="b6438-208">O Service1 relata as métricas Metric1 e Metric2.</span><span class="sxs-lookup"><span data-stu-id="b6438-208">Service1 reports metrics Metric1 and Metric2.</span></span> 
- <span data-ttu-id="b6438-209">O Service2 relata as métricas Metric2 e Metric3.</span><span class="sxs-lookup"><span data-stu-id="b6438-209">Service2 reports metrics Metric2 and Metric3.</span></span> 
- <span data-ttu-id="b6438-210">O Service3 relata as métricas Metric3 e Metric4.</span><span class="sxs-lookup"><span data-stu-id="b6438-210">Service3 reports metrics Metric3 and Metric4.</span></span>
- <span data-ttu-id="b6438-211">O Service4 relata a métrica Metric99.</span><span class="sxs-lookup"><span data-stu-id="b6438-211">Service4 reports metric Metric99.</span></span> 

<span data-ttu-id="b6438-212">Certamente, você consegue ver onde queremos chegar: há uma cadeia!</span><span class="sxs-lookup"><span data-stu-id="b6438-212">Surely you can see where we’re going here: There's a chain!</span></span> <span data-ttu-id="b6438-213">Realmente, não há quatro serviços independentes. Temos três serviços relacionados e um que está por conta própria.</span><span class="sxs-lookup"><span data-stu-id="b6438-213">We don’t really have four independent services, we have three services that are related and one that is off on its own.</span></span>

<span data-ttu-id="b6438-214"><center>
![Balanceamento dos serviços em conjunto][Image4]
</center></span><span class="sxs-lookup"><span data-stu-id="b6438-214"><center>
![Balancing Services Together][Image4]
</center></span></span>

<span data-ttu-id="b6438-215">Devido a essa cadeia, é possível que um desequilíbrio em métricas de 1 a 4 pode causar réplicas ou as instâncias do tooservices toomove de 1 a 3 ao redor.</span><span class="sxs-lookup"><span data-stu-id="b6438-215">Because of this chain, it's possible that an imbalance in metrics 1-4 can cause replicas or instances belonging tooservices 1-3 toomove around.</span></span> <span data-ttu-id="b6438-216">Também sabemos que um desequilíbrio nas métricas de 1, 2 ou 3 não pode causar movimentos no Service4.</span><span class="sxs-lookup"><span data-stu-id="b6438-216">We also know that an imbalance in Metrics 1, 2, or 3 can't cause movements in Service4.</span></span> <span data-ttu-id="b6438-217">Não deve haver nenhum ponto de mudança réplicas hello ou instâncias do tooService4 ao redor pode fazem absolutamente nada tooimpact saldo de saudação de métricas de 1 a 3.</span><span class="sxs-lookup"><span data-stu-id="b6438-217">There would be no point since moving hello replicas or instances belonging tooService4 around can do absolutely nothing tooimpact hello balance of Metrics 1-3.</span></span>

<span data-ttu-id="b6438-218">Olá Gerenciador de recursos de Cluster automaticamente descobre quais serviços estão relacionados.</span><span class="sxs-lookup"><span data-stu-id="b6438-218">hello Cluster Resource Manager automatically figures out what services are related.</span></span> <span data-ttu-id="b6438-219">Adição, remoção ou alteração métricas Olá para serviços podem afetar suas relações.</span><span class="sxs-lookup"><span data-stu-id="b6438-219">Adding, removing, or changing hello metrics for services can impact their relationships.</span></span> <span data-ttu-id="b6438-220">Por exemplo, entre duas execuções de balanceamento gratuito2 pode ter sido o tooremove atualizado Metric2.</span><span class="sxs-lookup"><span data-stu-id="b6438-220">For example, between two runs of balancing Service2 may have been updated tooremove Metric2.</span></span> <span data-ttu-id="b6438-221">Isso quebra a cadeia de saudação entre Service1 e gratuito2.</span><span class="sxs-lookup"><span data-stu-id="b6438-221">This breaks hello chain between Service1 and Service2.</span></span> <span data-ttu-id="b6438-222">Agora, em vez de dois grupos de serviços relacionados, há três:</span><span class="sxs-lookup"><span data-stu-id="b6438-222">Now instead of two groups of related services, there are three:</span></span>

<span data-ttu-id="b6438-223"><center>
![Balanceamento dos serviços em conjunto][Image5]
</center></span><span class="sxs-lookup"><span data-stu-id="b6438-223"><center>
![Balancing Services Together][Image5]
</center></span></span>

## <a name="next-steps"></a><span data-ttu-id="b6438-224">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b6438-224">Next steps</span></span>
* <span data-ttu-id="b6438-225">Métricas são como Olá Gerenciador de recursos de Cluster do serviço de malha gerencia capacidade em cluster hello e consumo.</span><span class="sxs-lookup"><span data-stu-id="b6438-225">Metrics are how hello Service Fabric Cluster Resource Manger manages consumption and capacity in hello cluster.</span></span> <span data-ttu-id="b6438-226">toolearn mais sobre as métricas e como tooconfigure-los, confira [neste artigo](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="b6438-226">toolearn more about metrics and how tooconfigure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>
* <span data-ttu-id="b6438-227">O custo de movimento é uma forma de sinalização toohello Gerenciador de recursos de Cluster que determinados serviços são toomove mais caro do que outros.</span><span class="sxs-lookup"><span data-stu-id="b6438-227">Movement Cost is one way of signaling toohello Cluster Resource Manager that certain services are more expensive toomove than others.</span></span> <span data-ttu-id="b6438-228">Para obter mais informações sobre o custo de movimento, consulte muito[neste artigo](service-fabric-cluster-resource-manager-movement-cost.md)</span><span class="sxs-lookup"><span data-stu-id="b6438-228">For more about movement cost, refer too[this article](service-fabric-cluster-resource-manager-movement-cost.md)</span></span>
* <span data-ttu-id="b6438-229">Olá Gerenciador de recursos de Cluster tem várias limitações que você pode configurar tooslow para baixo da variação no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b6438-229">hello Cluster Resource Manager has several throttles that you can configure tooslow down churn in hello cluster.</span></span> <span data-ttu-id="b6438-230">Normalmente, eles não são necessários, mas você poderá aprender mais sobre eles [aqui](service-fabric-cluster-resource-manager-advanced-throttling.md)</span><span class="sxs-lookup"><span data-stu-id="b6438-230">They're not normally necessary, but if you need them you can learn about them [here](service-fabric-cluster-resource-manager-advanced-throttling.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resrouce-manager-balancing-thresholds.png
[Image2]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-threshold-triggered-results.png
[Image3]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-activity-thresholds.png
[Image4]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together1.png
[Image5]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together2.png
