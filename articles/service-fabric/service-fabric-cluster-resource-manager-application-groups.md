---
title: aaaService Gerenciador de recursos de Cluster de malha - grupos de aplicativos | Microsoft Docs
description: "Visão geral da funcionalidade de grupo de aplicativos no Gerenciador de recursos de Cluster do serviço de malha de saudação do hello"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4cae2370-77b3-49ce-bf40-030400c4260d
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: b4f068862d962b53a0b3ea813b89bb13ee395681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapplication-groups"></a><span data-ttu-id="2ad90-103">Grupos de tooApplication de Introdução</span><span class="sxs-lookup"><span data-stu-id="2ad90-103">Introduction tooApplication Groups</span></span>
<span data-ttu-id="2ad90-104">Gerenciador de recursos de Cluster do Service Fabric normalmente gerencia os recursos de cluster, distribuindo a carga de saudação (representado por [métricas](service-fabric-cluster-resource-manager-metrics.md)) uniformemente em todo o cluster hello.</span><span class="sxs-lookup"><span data-stu-id="2ad90-104">Service Fabric's Cluster Resource Manager typically manages cluster resources by spreading hello load (represented via [Metrics](service-fabric-cluster-resource-manager-metrics.md)) evenly throughout hello cluster.</span></span> <span data-ttu-id="2ad90-105">Service Fabric gerencia a capacidade de saudação de nós Olá Olá cluster e hello como um todo via [capacidade](service-fabric-cluster-resource-manager-cluster-description.md).</span><span class="sxs-lookup"><span data-stu-id="2ad90-105">Service Fabric manages hello capacity of hello nodes in hello cluster and hello cluster as a whole via [capacity](service-fabric-cluster-resource-manager-cluster-description.md).</span></span> <span data-ttu-id="2ad90-106">As métricas e a capacidade funcionam muito bem para muitas cargas de trabalho, mas padrões que fazem uso intenso de diferentes Instâncias de Aplicativos do Service Fabric às vezes trazem requisitos adicionais.</span><span class="sxs-lookup"><span data-stu-id="2ad90-106">Metrics and capacity work great for many workloads, but patterns that make heavy use of different Service Fabric Application Instances sometimes bring in additional requirements.</span></span> <span data-ttu-id="2ad90-107">Por exemplo, você pode querer:</span><span class="sxs-lookup"><span data-stu-id="2ad90-107">For example you may want to:</span></span>

- <span data-ttu-id="2ad90-108">Reservar alguma capacidade em nós cluster Olá Olá para serviços de saudação dentro de algumas instâncias de aplicativo nomeada</span><span class="sxs-lookup"><span data-stu-id="2ad90-108">Reserve some capacity on hello nodes in hello cluster for hello services within some named application instance</span></span>
- <span data-ttu-id="2ad90-109">Limitar Olá o número total de nós Olá serviços dentro de uma instância de aplicativo nomeada são executados (em vez de propagação-los em todo o cluster Olá)</span><span class="sxs-lookup"><span data-stu-id="2ad90-109">Limit hello total number of nodes that hello services within a named application instance run on (instead of spreading them out over hello entire cluster)</span></span>
- <span data-ttu-id="2ad90-110">Definir capacidades na própria instância de aplicativo nomeada Olá número de saudação do toolimit serviços ou o total de consumo de recursos dos serviços de saudação dentro dele</span><span class="sxs-lookup"><span data-stu-id="2ad90-110">Define capacities on hello named application instance itself toolimit hello number of services or total resource consumption of hello services inside it</span></span>

<span data-ttu-id="2ad90-111">toomeet esses requisitos, Olá Gerenciador de recursos de Cluster do serviço de malha dá suporte a um recurso chamado de grupos de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="2ad90-111">toomeet these requirements, hello Service Fabric Cluster Resource Manager supports a feature called Application Groups.</span></span>

## <a name="limiting-hello-maximum-number-of-nodes"></a><span data-ttu-id="2ad90-112">Limitar o número máximo de saudação de nós</span><span class="sxs-lookup"><span data-stu-id="2ad90-112">Limiting hello maximum number of nodes</span></span>
<span data-ttu-id="2ad90-113">caso de uso mais simples Olá para capacidade de aplicativo é quando uma instância do aplicativo precisa toobe limitado tooa determinado número máximo de nós.</span><span class="sxs-lookup"><span data-stu-id="2ad90-113">hello simplest use case for Application capacity is when an application instance needs toobe limited tooa certain maximum number of nodes.</span></span> <span data-ttu-id="2ad90-114">Isso consolida todos os serviços na instância de aplicativo para um determinado número de máquinas.</span><span class="sxs-lookup"><span data-stu-id="2ad90-114">This consolidates all services within that application instance onto a set number of machines.</span></span> <span data-ttu-id="2ad90-115">A consolidação é útil quando você estiver tentando toopredict ou limitar o uso de recursos físicos pelos serviços de saudação na instância nomeada do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2ad90-115">Consolidation is useful when you're trying toopredict or cap physical resource use by hello services within that named application instance.</span></span> 

<span data-ttu-id="2ad90-116">Olá imagem a seguir mostra uma instância do aplicativo com e sem um número máximo de nós definidos:</span><span class="sxs-lookup"><span data-stu-id="2ad90-116">hello following image shows an application instance with and without a maximum number of nodes defined:</span></span>

<span data-ttu-id="2ad90-117"><center>
![Instância do aplicativo definindo o número máximo de nós][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="2ad90-117"><center>
![Application Instance Defining Maximum Number of Nodes][Image1]
</center></span></span>

<span data-ttu-id="2ad90-118">No exemplo à esquerda do hello, aplicativo hello não tem um número máximo de nós definidos e tem três serviços.</span><span class="sxs-lookup"><span data-stu-id="2ad90-118">In hello left example, hello application doesn’t have a maximum number of nodes defined, and it has three services.</span></span> <span data-ttu-id="2ad90-119">Olá Gerenciador de recursos de Cluster tem espalhados todas as réplicas em seis nós disponíveis tooachieve Olá melhor equilíbrio em cluster hello (comportamento padrão de saudação).</span><span class="sxs-lookup"><span data-stu-id="2ad90-119">hello Cluster Resource Manager has spread out all replicas across six available nodes tooachieve hello best balance in hello cluster (hello default behavior).</span></span> <span data-ttu-id="2ad90-120">Exemplo de direito hello, vemos Olá mesmo aplicativo limitado toothree nós.</span><span class="sxs-lookup"><span data-stu-id="2ad90-120">In hello right example, we see hello same application limited toothree nodes.</span></span>

<span data-ttu-id="2ad90-121">parâmetro Hello que controla esse comportamento é chamado de MaximumNodes.</span><span class="sxs-lookup"><span data-stu-id="2ad90-121">hello parameter that controls this behavior is called MaximumNodes.</span></span> <span data-ttu-id="2ad90-122">Esse parâmetro pode ser definido durante a criação do aplicativo ou atualizado para uma instância do aplicativo que já estava em execução.</span><span class="sxs-lookup"><span data-stu-id="2ad90-122">This parameter can be set during application creation, or updated for an application instance that was already running.</span></span>

<span data-ttu-id="2ad90-123">Powershell</span><span class="sxs-lookup"><span data-stu-id="2ad90-123">Powershell</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MaximumNodes 3
Update-ServiceFabricApplication –Name fabric:/AppName –MaximumNodes 5
```

<span data-ttu-id="2ad90-124">C#</span><span class="sxs-lookup"><span data-stu-id="2ad90-124">C#</span></span>

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MaximumNodes = 3;
await fc.ApplicationManager.CreateApplicationAsync(ad);

ApplicationUpdateDescription adUpdate = new ApplicationUpdateDescription(new Uri("fabric:/AppName"));
adUpdate.MaximumNodes = 5;
await fc.ApplicationManager.UpdateApplicationAsync(adUpdate);

```

<span data-ttu-id="2ad90-125">Em conjunto de saudação de nós, Olá Gerenciador de recursos de Cluster não garante que objetos de serviço serão colocados juntos ou quais nós são usados.</span><span class="sxs-lookup"><span data-stu-id="2ad90-125">Within hello set of nodes, hello Cluster Resource Manager doesn't guarantee which service objects get placed together or which nodes get used.</span></span>

## <a name="application-metrics-load-and-capacity"></a><span data-ttu-id="2ad90-126">Métrica, carga e capacidade do aplicativo</span><span class="sxs-lookup"><span data-stu-id="2ad90-126">Application Metrics, Load, and Capacity</span></span>
<span data-ttu-id="2ad90-127">Grupos de aplicativos também permitem que você toodefine métricas associadas a uma instância de determinado aplicativo nomeado e a capacidade dessa instância aplicativo para essas métricas.</span><span class="sxs-lookup"><span data-stu-id="2ad90-127">Application Groups also allow you toodefine metrics associated with a given named application instance, and that application instance's capacity for those metrics.</span></span> <span data-ttu-id="2ad90-128">Métricas de aplicativo permitem que você tootrack, reservar e limitar o consumo de recursos Olá dos serviços de saudação dentro dessa instância do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2ad90-128">Application metrics allow you tootrack, reserve, and limit hello resource consumption of hello services inside that application instance.</span></span>

<span data-ttu-id="2ad90-129">Para cada métrica do aplicativo, há dois valores que podem ser definidos:</span><span class="sxs-lookup"><span data-stu-id="2ad90-129">For each application metric, there are two values that can be set:</span></span>

- <span data-ttu-id="2ad90-130">**Capacidade de aplicativo total** – esta configuração representa a capacidade total de saudação do aplicativo hello para uma métrica específica.</span><span class="sxs-lookup"><span data-stu-id="2ad90-130">**Total Application Capacity** – This setting represents hello total capacity of hello application for a particular metric.</span></span> <span data-ttu-id="2ad90-131">Olá Gerenciador de recursos de Cluster não permite a criação de saudação de quaisquer novos serviços nessa instância de aplicativo que cause a carga total tooexceed esse valor.</span><span class="sxs-lookup"><span data-stu-id="2ad90-131">hello Cluster Resource Manager disallows hello creation of any new services within this application instance that would cause total load tooexceed this value.</span></span> <span data-ttu-id="2ad90-132">Por exemplo, digamos que instância de aplicativo hello tinha uma capacidade de 10 e já tinha a carga de cinco.</span><span class="sxs-lookup"><span data-stu-id="2ad90-132">For example, let's say hello application instance had a capacity of 10 and already had load of five.</span></span> <span data-ttu-id="2ad90-133">criação de saudação do serviço com uma carga total padrão de 10 será desativada.</span><span class="sxs-lookup"><span data-stu-id="2ad90-133">hello creation of a service with a total default load of 10 would be disallowed.</span></span>
- <span data-ttu-id="2ad90-134">**Capacidade máxima do nó** – essa configuração especifica Olá máximo total de carga para o aplicativo hello em um único nó.</span><span class="sxs-lookup"><span data-stu-id="2ad90-134">**Maximum Node Capacity** – This setting specifies hello maximum total load for hello application on a single node.</span></span> <span data-ttu-id="2ad90-135">Se a carga será essa capacidade, Olá Gerenciador de recursos de Cluster move nós de tooother de réplicas de modo que hello carga diminui.</span><span class="sxs-lookup"><span data-stu-id="2ad90-135">If load goes over this capacity, hello Cluster Resource Manager moves replicas tooother nodes so that hello load decreases.</span></span>


<span data-ttu-id="2ad90-136">Powershell:</span><span class="sxs-lookup"><span data-stu-id="2ad90-136">Powershell:</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -Metrics @("MetricName:Metric1,MaximumNodeCapacity:100,MaximumApplicationCapacity:1000")
```

<span data-ttu-id="2ad90-137">C#:</span><span class="sxs-lookup"><span data-stu-id="2ad90-137">C#:</span></span>

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.TotalApplicationCapacity = 1000;
appMetric.MaximumNodeCapacity = 100;
ad.Metrics.Add(appMetric);
await fc.ApplicationManager.CreateApplicationAsync(ad);
```

## <a name="reserving-capacity"></a><span data-ttu-id="2ad90-138">Reserva de capacidade</span><span class="sxs-lookup"><span data-stu-id="2ad90-138">Reserving Capacity</span></span>
<span data-ttu-id="2ad90-139">Outro uso comum de grupos de aplicativos é tooensure recursos em Olá cluster são reservados para uma instância de determinado aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2ad90-139">Another common use for application groups is tooensure that resources within hello cluster are reserved for a given application instance.</span></span> <span data-ttu-id="2ad90-140">espaço de saudação é sempre reservado quando a instância do aplicativo hello é criada.</span><span class="sxs-lookup"><span data-stu-id="2ad90-140">hello space is always reserved when hello application instance is created.</span></span>

<span data-ttu-id="2ad90-141">A reserva de espaço em cluster Olá para o aplicativo hello acontece imediatamente, mesmo quando:</span><span class="sxs-lookup"><span data-stu-id="2ad90-141">Reserving space in hello cluster for hello application happens immediately even when:</span></span>
- <span data-ttu-id="2ad90-142">instância do aplicativo Hello é criada, mas ainda não tiver todos os serviços dentro dele</span><span class="sxs-lookup"><span data-stu-id="2ad90-142">hello application instance is created but doesn't have any services within it yet</span></span>
- <span data-ttu-id="2ad90-143">número de saudação de serviços na instância do aplicativo hello muda sempre</span><span class="sxs-lookup"><span data-stu-id="2ad90-143">hello number of services within hello application instance changes every time</span></span> 
- <span data-ttu-id="2ad90-144">Serviços de saudação existem mas não estão consumindo recursos Olá</span><span class="sxs-lookup"><span data-stu-id="2ad90-144">hello services exist but aren't consuming hello resources</span></span> 

<span data-ttu-id="2ad90-145">Reservar recursos para uma instância de aplicativo requer especificar dois parâmetros adicionais: *MinimumNodes* e *NodeReservationCapacity*</span><span class="sxs-lookup"><span data-stu-id="2ad90-145">Reserving resources for an application instance requires specifying two additional parameters: *MinimumNodes* and *NodeReservationCapacity*</span></span>

- <span data-ttu-id="2ad90-146">**MinimumNodes** -define o número mínimo de saudação de nós que Olá aplicativo instância deve ser executada.</span><span class="sxs-lookup"><span data-stu-id="2ad90-146">**MinimumNodes** - Defines hello minimum number of nodes that hello application instance should run on.</span></span>  
- <span data-ttu-id="2ad90-147">**NodeReservationCapacity** -essa configuração é por métrica para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2ad90-147">**NodeReservationCapacity** - This setting is per metric for hello application.</span></span> <span data-ttu-id="2ad90-148">valor de saudação é Olá métrica reservada para o aplicativo hello em qualquer nó onde Olá serviços nesse aplicativo executar.</span><span class="sxs-lookup"><span data-stu-id="2ad90-148">hello value is hello amount of that metric reserved for hello application on any node where that hello services in that application run.</span></span>

<span data-ttu-id="2ad90-149">Combinando **MinimumNodes** e **NodeReservationCapacity** garante uma reserva de carga mínima para o aplicativo hello em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="2ad90-149">Combining **MinimumNodes** and **NodeReservationCapacity** guarantees a minimum load reservation for hello application within hello cluster.</span></span> <span data-ttu-id="2ad90-150">Se houver menos restantes capacidade em Olá cluster reserva total de saudação necessários, falha na criação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2ad90-150">If there's less remaining capacity in hello cluster than hello total reservation required, creation of hello application fails.</span></span> 

<span data-ttu-id="2ad90-151">Vejamos um exemplo de reserva de capacidade:</span><span class="sxs-lookup"><span data-stu-id="2ad90-151">Let's look at an example of capacity reservation:</span></span>

<span data-ttu-id="2ad90-152"><center>
Instâncias do aplicativo definindo a capacidade reservada![][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="2ad90-152"><center>
![Application Instances Defining Reserved Capacity][Image2]
</center></span></span>

<span data-ttu-id="2ad90-153">No exemplo à esquerda do hello, os aplicativos não têm qualquer capacidade de aplicativo definidas.</span><span class="sxs-lookup"><span data-stu-id="2ad90-153">In hello left example, applications do not have any Application Capacity defined.</span></span> <span data-ttu-id="2ad90-154">Olá Gerenciador de recursos de Cluster de balanceamento de tudo de acordo com as regras de toonormal.</span><span class="sxs-lookup"><span data-stu-id="2ad90-154">hello Cluster Resource Manager balances everything according toonormal rules.</span></span>

<span data-ttu-id="2ad90-155">No exemplo hello saudação à direita, digamos que Application1 foi criado com hello configurações a seguir:</span><span class="sxs-lookup"><span data-stu-id="2ad90-155">In hello example on hello right, let's say that Application1 was created with hello following settings:</span></span>

- <span data-ttu-id="2ad90-156">Conjunto de MinimumNodes tootwo</span><span class="sxs-lookup"><span data-stu-id="2ad90-156">MinimumNodes set tootwo</span></span>
- <span data-ttu-id="2ad90-157">Uma métrica de aplicativo definida com</span><span class="sxs-lookup"><span data-stu-id="2ad90-157">An application Metric defined with</span></span>
  - <span data-ttu-id="2ad90-158">NodeReservationCapacity de 20</span><span class="sxs-lookup"><span data-stu-id="2ad90-158">NodeReservationCapacity of 20</span></span>

<span data-ttu-id="2ad90-159">Powershell</span><span class="sxs-lookup"><span data-stu-id="2ad90-159">Powershell</span></span>

 ``` posh
 New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MinimumNodes 2 -Metrics @("MetricName:Metric1,NodeReservationCapacity:20")
 ```

<span data-ttu-id="2ad90-160">C#</span><span class="sxs-lookup"><span data-stu-id="2ad90-160">C#</span></span>

 ``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MinimumNodes = 2;

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.NodeReservationCapacity = 20;

ad.Metrics.Add(appMetric);

await fc.ApplicationManager.CreateApplicationAsync(ad);
```

<span data-ttu-id="2ad90-161">Malha do serviço de reserva a capacidade em dois nós para Application1 e não permitir que os serviços de tooconsume Application2 essa capacidade mesmo se não houver que nenhuma carga está sendo consumida pelos serviços de saudação dentro Application1 no tempo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ad90-161">Service Fabric reserves capacity on two nodes for Application1, and doesn't allow services from Application2 tooconsume that capacity even if there are no load is being consumed by hello services inside Application1 at hello time.</span></span> <span data-ttu-id="2ad90-162">Essa capacidade reservada do aplicativo será considerada consumido e contagens contra Olá capacidade nesse nó e o cluster Olá restante.</span><span class="sxs-lookup"><span data-stu-id="2ad90-162">This reserved application capacity is considered consumed  and counts against hello remaining capacity on that node and within hello cluster.</span></span>  <span data-ttu-id="2ad90-163">reserva de saudação é deduzida do hello restantes capacidade cluster imediatamente, mas Olá reservado consumo é deduzido da capacidade de saudação de um nó específico somente quando o objeto de pelo menos um serviço é colocado sobre ele.</span><span class="sxs-lookup"><span data-stu-id="2ad90-163">hello reservation is deducted from hello remaining cluster capacity immediately, however hello reserved consumption is deducted from hello capacity of a specific node only when at least one service object is placed on it.</span></span> <span data-ttu-id="2ad90-164">Essa reserva posterior permite flexibilidade e melhor utilização de recursos já que os recursos são reservados nos nós apenas quando necessário.</span><span class="sxs-lookup"><span data-stu-id="2ad90-164">This later reservation allows for flexibility and better resource utilization since resources are only reserved on nodes when needed.</span></span>

## <a name="obtaining-hello-application-load-information"></a><span data-ttu-id="2ad90-165">Obtendo informações de carga do aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="2ad90-165">Obtaining hello application load information</span></span>
<span data-ttu-id="2ad90-166">Para cada aplicativo que tem uma capacidade de aplicativo definidas para uma ou mais métricas, você pode obter informações de saudação sobre carga de agregação Olá relatada pelas réplicas de seus serviços.</span><span class="sxs-lookup"><span data-stu-id="2ad90-166">For each application that has an Application Capacity defined for one or more metrics you can obtain hello information about hello aggregate load reported by replicas of its services.</span></span>

<span data-ttu-id="2ad90-167">Powershell:</span><span class="sxs-lookup"><span data-stu-id="2ad90-167">Powershell:</span></span>

``` posh
Get-ServiceFabricApplicationLoad –ApplicationName fabric:/MyApplication1
```

<span data-ttu-id="2ad90-168">C#</span><span class="sxs-lookup"><span data-stu-id="2ad90-168">C#</span></span>

``` csharp
var v = await fc.QueryManager.GetApplicationLoadInformationAsync("fabric:/MyApplication1");
var metrics = v.ApplicationLoadMetricInformation;
foreach (ApplicationLoadMetricInformation metric in metrics)
{
    Console.WriteLine(metric.ApplicationCapacity);  //total capacity for this metric in this application instance
    Console.WriteLine(metric.ReservationCapacity);  //reserved capacity for this metric in this application instance
    Console.WriteLine(metric.ApplicationLoad);  //current load for this metric in this application instance
}
```

<span data-ttu-id="2ad90-169">consulta de ApplicationLoad Olá retorna as informações básicas sobre a capacidade do aplicativo que foi especificado para o aplicativo hello Olá.</span><span class="sxs-lookup"><span data-stu-id="2ad90-169">hello ApplicationLoad query returns hello basic information about Application Capacity that was specified for hello application.</span></span> <span data-ttu-id="2ad90-170">Essas informações incluem informações de nós de mínimo e máximo de saudação e número de saudação aplicativo hello no momento atual.</span><span class="sxs-lookup"><span data-stu-id="2ad90-170">This information includes hello Minimum Nodes and Maximum Nodes info, and hello number that hello application is currently occupying.</span></span> <span data-ttu-id="2ad90-171">Elas também incluem informações sobre cada métrica de carga do aplicativo, incluindo:</span><span class="sxs-lookup"><span data-stu-id="2ad90-171">It also includes information about each application load metric, including:</span></span>

* <span data-ttu-id="2ad90-172">Nome da métrica: O nome da métrica de saudação.</span><span class="sxs-lookup"><span data-stu-id="2ad90-172">Metric Name: Name of hello metric.</span></span>
* <span data-ttu-id="2ad90-173">Capacidade de reserva: Capacidade de Cluster que está reservada no cluster Olá para este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2ad90-173">Reservation Capacity: Cluster Capacity that is reserved in hello cluster for this Application.</span></span>
* <span data-ttu-id="2ad90-174">Carga do Aplicativo: a Carga Total de réplicas filho deste Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2ad90-174">Application Load: Total Load of this Application’s child replicas.</span></span>
* <span data-ttu-id="2ad90-175">Capacidade do Aplicativo: valor máximo permitido de Carga do Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2ad90-175">Application Capacity: Maximum permitted value of Application Load.</span></span>

## <a name="removing-application-capacity"></a><span data-ttu-id="2ad90-176">Removendo a capacidade do aplicativo</span><span class="sxs-lookup"><span data-stu-id="2ad90-176">Removing Application Capacity</span></span>
<span data-ttu-id="2ad90-177">Depois de definir parâmetros de capacidade do aplicativo hello para um aplicativo, eles podem ser removidos usando APIs do aplicativo de atualização ou cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2ad90-177">Once hello Application Capacity parameters are set for an application, they can be removed using Update Application APIs or PowerShell cmdlets.</span></span> <span data-ttu-id="2ad90-178">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="2ad90-178">For example:</span></span>

``` posh
Update-ServiceFabricApplication –Name fabric:/MyApplication1 –RemoveApplicationCapacity

```

<span data-ttu-id="2ad90-179">Este comando remove todos os parâmetros de gerenciamento de capacidade de aplicativo de instância de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2ad90-179">This command removes all Application capacity management parameters from hello application instance.</span></span> <span data-ttu-id="2ad90-180">Isso inclui MinimumNodes, MaximumNodes e métricas de saudação do aplicativo, se houver.</span><span class="sxs-lookup"><span data-stu-id="2ad90-180">This includes MinimumNodes, MaximumNodes, and hello Application's metrics, if any.</span></span> <span data-ttu-id="2ad90-181">efeito de saudação do comando de saudação é imediato.</span><span class="sxs-lookup"><span data-stu-id="2ad90-181">hello effect of hello command is immediate.</span></span> <span data-ttu-id="2ad90-182">Depois que esse comando for concluído, Olá Gerenciador de recursos de Cluster usa o comportamento padrão de saudação para gerenciamento de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="2ad90-182">After this command completes, hello Cluster Resource Manager uses hello default behavior for managing applications.</span></span> <span data-ttu-id="2ad90-183">Os parâmetros de capacidade do aplicativo podem ser especificados novamente por meio de `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span><span class="sxs-lookup"><span data-stu-id="2ad90-183">Application Capacity parameters can be specified again via `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span></span>

### <a name="restrictions-on-application-capacity"></a><span data-ttu-id="2ad90-184">Restrições à capacidade do aplicativo</span><span class="sxs-lookup"><span data-stu-id="2ad90-184">Restrictions on Application Capacity</span></span>
<span data-ttu-id="2ad90-185">Há várias restrições aos parâmetros de Capacidade de Aplicativo que devem ser respeitadas.</span><span class="sxs-lookup"><span data-stu-id="2ad90-185">There are several restrictions on Application Capacity parameters that must be respected.</span></span> <span data-ttu-id="2ad90-186">Se houver erros de validação, nenhuma alteração será feita.</span><span class="sxs-lookup"><span data-stu-id="2ad90-186">If there are validation errors no changes take place.</span></span>

- <span data-ttu-id="2ad90-187">Todos os parâmetros de inteiro devem ser números não negativos.</span><span class="sxs-lookup"><span data-stu-id="2ad90-187">All integer parameters must be non-negative numbers.</span></span>
- <span data-ttu-id="2ad90-188">MinimumNodes nunca deve ser maior que MaximumNodes.</span><span class="sxs-lookup"><span data-stu-id="2ad90-188">MinimumNodes must never be greater than MaximumNodes.</span></span>
- <span data-ttu-id="2ad90-189">Se as capacidades de uma métrica de carga forem definidas, elas deverão seguir estas regras:</span><span class="sxs-lookup"><span data-stu-id="2ad90-189">If capacities for a load metric are defined, then they must follow these rules:</span></span>
  - <span data-ttu-id="2ad90-190">A Capacidade de Reserva do Nó não deve ser maior que a Capacidade Máxima do Nó.</span><span class="sxs-lookup"><span data-stu-id="2ad90-190">Node Reservation Capacity must not be greater than Maximum Node Capacity.</span></span> <span data-ttu-id="2ad90-191">Por exemplo, você não pode limitar a capacidade de saudação de métrica hello "CPU" em unidades de tootwo nó hello e tente tooreserve três unidades em cada nó.</span><span class="sxs-lookup"><span data-stu-id="2ad90-191">For example, you cannot limit hello capacity for hello metric “CPU” on hello node tootwo units and try tooreserve three units on each node.</span></span>
  - <span data-ttu-id="2ad90-192">Se MaximumNodes for especificado, em seguida, Olá produto de MaximumNodes e a capacidade máxima do nó deve não ser maior capacidade Total do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2ad90-192">If MaximumNodes is specified, then hello product of MaximumNodes and Maximum Node Capacity must not be greater than Total Application Capacity.</span></span> <span data-ttu-id="2ad90-193">Por exemplo, digamos que Olá capacidade máxima do nó de métrica de carga "CPU" é definido tooeight.</span><span class="sxs-lookup"><span data-stu-id="2ad90-193">For example, let's say hello Maximum Node Capacity for load metric “CPU” is set tooeight.</span></span> <span data-ttu-id="2ad90-194">Digamos que também definir Olá too10 máximo de nós.</span><span class="sxs-lookup"><span data-stu-id="2ad90-194">Let's also say you set hello Maximum Nodes too10.</span></span> <span data-ttu-id="2ad90-195">Nesse caso, a Capacidade Total do Aplicativo deve ser maior do que 80 para esta métrica de carga.</span><span class="sxs-lookup"><span data-stu-id="2ad90-195">In this case, Total Application Capacity must be greater than 80 for this load metric.</span></span>

<span data-ttu-id="2ad90-196">restrições de saudação são aplicadas tanto durante a criação de aplicativos e atualizações.</span><span class="sxs-lookup"><span data-stu-id="2ad90-196">hello restrictions are enforced both during application creation and updates.</span></span>

## <a name="how-not-toouse-application-capacity"></a><span data-ttu-id="2ad90-197">Como toouse capacidade de aplicativo</span><span class="sxs-lookup"><span data-stu-id="2ad90-197">How not toouse Application Capacity</span></span>
- <span data-ttu-id="2ad90-198">Não tente toouse Olá grupo de aplicativos recursos tooconstrain Olá aplicativo tooa _específico_ subconjunto de nós.</span><span class="sxs-lookup"><span data-stu-id="2ad90-198">Do not try toouse hello Application Group features tooconstrain hello application tooa _specific_ subset of nodes.</span></span> <span data-ttu-id="2ad90-199">Em outras palavras, você pode especificar que o aplicativo hello é executado no máximo cinco nós, mas não quais cinco nós específicos no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="2ad90-199">In other words, you can specify that hello application runs on at most five nodes, but not which specific five nodes in hello cluster.</span></span> <span data-ttu-id="2ad90-200">A restrição de um aplicativo toospecific nós podem ser realizados usando restrições de posicionamento para serviços.</span><span class="sxs-lookup"><span data-stu-id="2ad90-200">Constraining an application toospecific nodes can be achieved using placement constraints for services.</span></span>
- <span data-ttu-id="2ad90-201">Não tente toouse Olá capacidade do aplicativo tooensure dois serviços da saudação mesmo aplicativo são colocadas em Olá mesmos nós.</span><span class="sxs-lookup"><span data-stu-id="2ad90-201">Do not try toouse hello Application Capacity tooensure that two services from hello same application are placed on hello same nodes.</span></span> <span data-ttu-id="2ad90-202">Em vez disso, use [afinidade](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) ou [restrições de posicionamento](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span><span class="sxs-lookup"><span data-stu-id="2ad90-202">Instead use [affinity](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) or [placement constraints](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ad90-203">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2ad90-203">Next steps</span></span>
- <span data-ttu-id="2ad90-204">Para saber mais sobre como configurar os serviços, [Saiba mais sobre como configurar serviços](service-fabric-cluster-resource-manager-configure-services.md)</span><span class="sxs-lookup"><span data-stu-id="2ad90-204">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>
- <span data-ttu-id="2ad90-205">toofind out sobre como Olá Gerenciador de recursos de Cluster gerencia e equilibra a carga no cluster hello, check-out artigo Olá em [balanceamento de carga](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="2ad90-205">toofind out about how hello Cluster Resource Manager manages and balances load in hello cluster, check out hello article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>
- <span data-ttu-id="2ad90-206">Desde o início de saudação e [obter uma introdução toohello Gerenciador de recursos de Cluster do serviço de malha](service-fabric-cluster-resource-manager-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="2ad90-206">Start from hello beginning and [get an Introduction toohello Service Fabric Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span></span>
- <span data-ttu-id="2ad90-207">Para obter mais informações sobre como as métricas funcionam em geral, leia sobre [Métricas de Carga do Service Fabric](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="2ad90-207">For more information on how metrics work generally, read up on [Service Fabric Load Metrics](service-fabric-cluster-resource-manager-metrics.md)</span></span>
- <span data-ttu-id="2ad90-208">Olá Gerenciador de recursos de Cluster tem muitas opções para descrever o cluster hello.</span><span class="sxs-lookup"><span data-stu-id="2ad90-208">hello Cluster Resource Manager has many options for describing hello cluster.</span></span> <span data-ttu-id="2ad90-209">toofind mais sobre eles, leia este artigo em [que descreve um cluster do Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)</span><span class="sxs-lookup"><span data-stu-id="2ad90-209">toofind out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-max-nodes.png
[Image2]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-reserved-capacity.png
