---
title: "Gerenciador de Recursos de Cluster do Service Fabric – Grupos de Aplicativos | Microsoft Docs"
description: "Visão geral da funcionalidade de Grupo de Aplicativos no Gerenciador de Recursos de Cluster do Service Fabric"
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
ms.openlocfilehash: 7fc61731c8df2a0c3dc5b77ae718b41c240f9233
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="introduction-to-application-groups"></a><span data-ttu-id="d2943-103">Introdução aos grupos de aplicativos</span><span class="sxs-lookup"><span data-stu-id="d2943-103">Introduction to Application Groups</span></span>
<span data-ttu-id="d2943-104">O Cluster Resource Manager do Service Fabric geralmente gerencia os recursos de cluster distribuindo a carga (representada por meio de [Métricas](service-fabric-cluster-resource-manager-metrics.md)) uniformemente em todo o cluster.</span><span class="sxs-lookup"><span data-stu-id="d2943-104">Service Fabric's Cluster Resource Manager typically manages cluster resources by spreading the load (represented via [Metrics](service-fabric-cluster-resource-manager-metrics.md)) evenly throughout the cluster.</span></span> <span data-ttu-id="d2943-105">O Service Fabric gerencia a capacidade dos nós no cluster e o cluster como um todo por meio da [capacidade](service-fabric-cluster-resource-manager-cluster-description.md).</span><span class="sxs-lookup"><span data-stu-id="d2943-105">Service Fabric manages the capacity of the nodes in the cluster and the cluster as a whole via [capacity](service-fabric-cluster-resource-manager-cluster-description.md).</span></span> <span data-ttu-id="d2943-106">As métricas e a capacidade funcionam muito bem para muitas cargas de trabalho, mas padrões que fazem uso intenso de diferentes Instâncias de Aplicativos do Service Fabric às vezes trazem requisitos adicionais.</span><span class="sxs-lookup"><span data-stu-id="d2943-106">Metrics and capacity work great for many workloads, but patterns that make heavy use of different Service Fabric Application Instances sometimes bring in additional requirements.</span></span> <span data-ttu-id="d2943-107">Por exemplo, você pode querer:</span><span class="sxs-lookup"><span data-stu-id="d2943-107">For example you may want to:</span></span>

- <span data-ttu-id="d2943-108">Reservar alguma capacidade em nós do cluster para os serviços em algumas instâncias nomeadas de aplicativo</span><span class="sxs-lookup"><span data-stu-id="d2943-108">Reserve some capacity on the nodes in the cluster for the services within some named application instance</span></span>
- <span data-ttu-id="d2943-109">Limitar o número total de nós em que os serviços em uma instância nomeada de aplicativo são executados (em vez de propagá-los por todo o cluster)</span><span class="sxs-lookup"><span data-stu-id="d2943-109">Limit the total number of nodes that the services within a named application instance run on (instead of spreading them out over the entire cluster)</span></span>
- <span data-ttu-id="d2943-110">Definir as capacidades na instância nomeada do aplicativo em si para limitar o número de serviços ou o consumo de recursos total dos serviços dentro dele</span><span class="sxs-lookup"><span data-stu-id="d2943-110">Define capacities on the named application instance itself to limit the number of services or total resource consumption of the services inside it</span></span>

<span data-ttu-id="d2943-111">Para atender a esses requisitos, o Service Fabric Cluster Resource Manager dá suporte a um recurso chamado Grupos de Aplicativos.</span><span class="sxs-lookup"><span data-stu-id="d2943-111">To meet these requirements, the Service Fabric Cluster Resource Manager supports a feature called Application Groups.</span></span>

## <a name="limiting-the-maximum-number-of-nodes"></a><span data-ttu-id="d2943-112">Limitando o número máximo de nós</span><span class="sxs-lookup"><span data-stu-id="d2943-112">Limiting the maximum number of nodes</span></span>
<span data-ttu-id="d2943-113">O caso de uso mais simples para capacidade do Aplicativo é quando uma instancia de aplicativo precisa ser limitada a um determinado número máximo de nós.</span><span class="sxs-lookup"><span data-stu-id="d2943-113">The simplest use case for Application capacity is when an application instance needs to be limited to a certain maximum number of nodes.</span></span> <span data-ttu-id="d2943-114">Isso consolida todos os serviços na instância de aplicativo para um determinado número de máquinas.</span><span class="sxs-lookup"><span data-stu-id="d2943-114">This consolidates all services within that application instance onto a set number of machines.</span></span> <span data-ttu-id="d2943-115">A consolidação é útil quando você está tentando prever ou limitar o uso de recursos físicos, os serviços na instância nomeada do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d2943-115">Consolidation is useful when you're trying to predict or cap physical resource use by the services within that named application instance.</span></span> 

<span data-ttu-id="d2943-116">A imagem a seguir mostra uma instância de aplicativo com e sem um número máximo de nós definido:</span><span class="sxs-lookup"><span data-stu-id="d2943-116">The following image shows an application instance with and without a maximum number of nodes defined:</span></span>

<span data-ttu-id="d2943-117"><center>
![Instância do aplicativo definindo o número máximo de nós][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="d2943-117"><center>
![Application Instance Defining Maximum Number of Nodes][Image1]
</center></span></span>

<span data-ttu-id="d2943-118">No exemplo à esquerda, o aplicativo não tem um número máximo de nós definidos, e ele tem três serviços.</span><span class="sxs-lookup"><span data-stu-id="d2943-118">In the left example, the application doesn’t have a maximum number of nodes defined, and it has three services.</span></span> <span data-ttu-id="d2943-119">O Cluster Resource Manager distribuiu todas as réplicas em seis nós disponíveis para obter o melhor equilíbrio no cluster (o comportamento padrão).</span><span class="sxs-lookup"><span data-stu-id="d2943-119">The Cluster Resource Manager has spread out all replicas across six available nodes to achieve the best balance in the cluster (the default behavior).</span></span> <span data-ttu-id="d2943-120">No exemplo à direita, vemos o mesmo aplicativo limitado a três nós.</span><span class="sxs-lookup"><span data-stu-id="d2943-120">In the right example, we see the same application limited to three nodes.</span></span>

<span data-ttu-id="d2943-121">O parâmetro que controla esse comportamento é chamado de MaximumNodes.</span><span class="sxs-lookup"><span data-stu-id="d2943-121">The parameter that controls this behavior is called MaximumNodes.</span></span> <span data-ttu-id="d2943-122">Esse parâmetro pode ser definido durante a criação do aplicativo ou atualizado para uma instância do aplicativo que já estava em execução.</span><span class="sxs-lookup"><span data-stu-id="d2943-122">This parameter can be set during application creation, or updated for an application instance that was already running.</span></span>

<span data-ttu-id="d2943-123">Powershell</span><span class="sxs-lookup"><span data-stu-id="d2943-123">Powershell</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MaximumNodes 3
Update-ServiceFabricApplication –Name fabric:/AppName –MaximumNodes 5
```

<span data-ttu-id="d2943-124">C#</span><span class="sxs-lookup"><span data-stu-id="d2943-124">C#</span></span>

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

<span data-ttu-id="d2943-125">Dentro do conjunto de nós, o Gerenciador de Recursos de Cluster não garante que objetos de serviço serão colocados juntos ou quais nós são usados.</span><span class="sxs-lookup"><span data-stu-id="d2943-125">Within the set of nodes, the Cluster Resource Manager doesn't guarantee which service objects get placed together or which nodes get used.</span></span>

## <a name="application-metrics-load-and-capacity"></a><span data-ttu-id="d2943-126">Métrica, carga e capacidade do aplicativo</span><span class="sxs-lookup"><span data-stu-id="d2943-126">Application Metrics, Load, and Capacity</span></span>
<span data-ttu-id="d2943-127">Os grupos de aplicativos também permitem definir métricas associadas a uma determinada instância nomeado do aplicativo e a capacidade da instância do aplicativo para essas métricas.</span><span class="sxs-lookup"><span data-stu-id="d2943-127">Application Groups also allow you to define metrics associated with a given named application instance, and that application instance's capacity for those metrics.</span></span> <span data-ttu-id="d2943-128">As métricas de aplicativo permitem controlar, reservar e limitar o consumo de recursos dos serviços dentro dessa instância do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d2943-128">Application metrics allow you to track, reserve, and limit the resource consumption of the services inside that application instance.</span></span>

<span data-ttu-id="d2943-129">Para cada métrica do aplicativo, há dois valores que podem ser definidos:</span><span class="sxs-lookup"><span data-stu-id="d2943-129">For each application metric, there are two values that can be set:</span></span>

- <span data-ttu-id="d2943-130">**Capacidade Total do Aplicativo** – essa configuração representa a capacidade total do aplicativo para uma determinada métrica.</span><span class="sxs-lookup"><span data-stu-id="d2943-130">**Total Application Capacity** – This setting represents the total capacity of the application for a particular metric.</span></span> <span data-ttu-id="d2943-131">O Cluster Resource Manager não permite a criação de quaisquer novos serviços dentro dessa instância do aplicativo que fariam com que esse valor fosse excedido.</span><span class="sxs-lookup"><span data-stu-id="d2943-131">The Cluster Resource Manager disallows the creation of any new services within this application instance that would cause total load to exceed this value.</span></span> <span data-ttu-id="d2943-132">Por exemplo, digamos que a instância do aplicativo tinha a capacidade de 10 e já tinha a carga de cinco.</span><span class="sxs-lookup"><span data-stu-id="d2943-132">For example, let's say the application instance had a capacity of 10 and already had load of five.</span></span> <span data-ttu-id="d2943-133">A criação de um serviço com uma carga padrão total de 10 não deve ser permitida.</span><span class="sxs-lookup"><span data-stu-id="d2943-133">The creation of a service with a total default load of 10 would be disallowed.</span></span>
- <span data-ttu-id="d2943-134">**Capacidade Máxima do Nó** – essa configuração especifica a carga total máxima para o aplicativo em um único nó.</span><span class="sxs-lookup"><span data-stu-id="d2943-134">**Maximum Node Capacity** – This setting specifies the maximum total load for the application on a single node.</span></span> <span data-ttu-id="d2943-135">Se a carga ultrapassar essa capacidade, o Gerenciador de Recursos de Cluster move réplicas para outros nós de forma que a carga diminua.</span><span class="sxs-lookup"><span data-stu-id="d2943-135">If load goes over this capacity, the Cluster Resource Manager moves replicas to other nodes so that the load decreases.</span></span>


<span data-ttu-id="d2943-136">Powershell:</span><span class="sxs-lookup"><span data-stu-id="d2943-136">Powershell:</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -Metrics @("MetricName:Metric1,MaximumNodeCapacity:100,MaximumApplicationCapacity:1000")
```

<span data-ttu-id="d2943-137">C#:</span><span class="sxs-lookup"><span data-stu-id="d2943-137">C#:</span></span>

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

## <a name="reserving-capacity"></a><span data-ttu-id="d2943-138">Reserva de capacidade</span><span class="sxs-lookup"><span data-stu-id="d2943-138">Reserving Capacity</span></span>
<span data-ttu-id="d2943-139">Outro uso comum de grupos de aplicativos é para garantir que os recursos dentro do cluster sejam reservados para uma determinada instância do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d2943-139">Another common use for application groups is to ensure that resources within the cluster are reserved for a given application instance.</span></span> <span data-ttu-id="d2943-140">O espaço é sempre reservado quando a instância do aplicativo é criada.</span><span class="sxs-lookup"><span data-stu-id="d2943-140">The space is always reserved when the application instance is created.</span></span>

<span data-ttu-id="d2943-141">A reserva do espaço no cluster para o aplicativo acontece imediatamente, mesmo quando:</span><span class="sxs-lookup"><span data-stu-id="d2943-141">Reserving space in the cluster for the application happens immediately even when:</span></span>
- <span data-ttu-id="d2943-142">a instância do aplicativo é criada, mas ainda não tem todos os serviços dentro dela</span><span class="sxs-lookup"><span data-stu-id="d2943-142">the application instance is created but doesn't have any services within it yet</span></span>
- <span data-ttu-id="d2943-143">o número de serviços na instância do aplicativo é alterado sempre</span><span class="sxs-lookup"><span data-stu-id="d2943-143">the number of services within the application instance changes every time</span></span> 
- <span data-ttu-id="d2943-144">os serviços existem, mas não estão consumindo os recursos</span><span class="sxs-lookup"><span data-stu-id="d2943-144">the services exist but aren't consuming the resources</span></span> 

<span data-ttu-id="d2943-145">Reservar recursos para uma instância de aplicativo requer especificar dois parâmetros adicionais: *MinimumNodes* e *NodeReservationCapacity*</span><span class="sxs-lookup"><span data-stu-id="d2943-145">Reserving resources for an application instance requires specifying two additional parameters: *MinimumNodes* and *NodeReservationCapacity*</span></span>

- <span data-ttu-id="d2943-146">**MinimumNodes** - define o número mínimo de nós que deve ser executados na instância do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d2943-146">**MinimumNodes** - Defines the minimum number of nodes that the application instance should run on.</span></span>  
- <span data-ttu-id="d2943-147">**NodeReservationCapacity** - essa configuração é por métrica para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d2943-147">**NodeReservationCapacity** - This setting is per metric for the application.</span></span> <span data-ttu-id="d2943-148">O valor é a quantidade de métrica reservada para o aplicativo em qualquer nó onde os serviços do aplicativo são executados.</span><span class="sxs-lookup"><span data-stu-id="d2943-148">The value is the amount of that metric reserved for the application on any node where that the services in that application run.</span></span>

<span data-ttu-id="d2943-149">A combinação de **MinimumNodes** e **NodeReservationCapacity** garante uma reserva de carga mínima para o aplicativo no cluster.</span><span class="sxs-lookup"><span data-stu-id="d2943-149">Combining **MinimumNodes** and **NodeReservationCapacity** guarantees a minimum load reservation for the application within the cluster.</span></span> <span data-ttu-id="d2943-150">Se houver menos capacidade restante no cluster do que a reserva total necessária, a criação do aplicativo falhará.</span><span class="sxs-lookup"><span data-stu-id="d2943-150">If there's less remaining capacity in the cluster than the total reservation required, creation of the application fails.</span></span> 

<span data-ttu-id="d2943-151">Vejamos um exemplo de reserva de capacidade:</span><span class="sxs-lookup"><span data-stu-id="d2943-151">Let's look at an example of capacity reservation:</span></span>

<span data-ttu-id="d2943-152"><center>
Instâncias do aplicativo definindo a capacidade reservada![][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="d2943-152"><center>
![Application Instances Defining Reserved Capacity][Image2]
</center></span></span>

<span data-ttu-id="d2943-153">No exemplo à esquerda, os aplicativos não têm nenhuma Capacidade de Aplicativo definida.</span><span class="sxs-lookup"><span data-stu-id="d2943-153">In the left example, applications do not have any Application Capacity defined.</span></span> <span data-ttu-id="d2943-154">O Cluster Resource Manager equilibra tudo de acordo com as regras normais.</span><span class="sxs-lookup"><span data-stu-id="d2943-154">The Cluster Resource Manager balances everything according to normal rules.</span></span>

<span data-ttu-id="d2943-155">No exemplo à direita, digamos que o Application1 foi criado com as seguintes configurações:</span><span class="sxs-lookup"><span data-stu-id="d2943-155">In the example on the right, let's say that Application1 was created with the following settings:</span></span>

- <span data-ttu-id="d2943-156">MinimumNodes definido como dois</span><span class="sxs-lookup"><span data-stu-id="d2943-156">MinimumNodes set to two</span></span>
- <span data-ttu-id="d2943-157">Uma métrica de aplicativo definida com</span><span class="sxs-lookup"><span data-stu-id="d2943-157">An application Metric defined with</span></span>
  - <span data-ttu-id="d2943-158">NodeReservationCapacity de 20</span><span class="sxs-lookup"><span data-stu-id="d2943-158">NodeReservationCapacity of 20</span></span>

<span data-ttu-id="d2943-159">Powershell</span><span class="sxs-lookup"><span data-stu-id="d2943-159">Powershell</span></span>

 ``` posh
 New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MinimumNodes 2 -Metrics @("MetricName:Metric1,NodeReservationCapacity:20")
 ```

<span data-ttu-id="d2943-160">C#</span><span class="sxs-lookup"><span data-stu-id="d2943-160">C#</span></span>

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

<span data-ttu-id="d2943-161">O Service Fabric reserva a capacidade em dois nós para Application1 e não permite que os serviços de Application2 consumam essa capacidade, mesmo se não houver nenhuma carga sendo consumida pelos serviços em Application1 no momento.</span><span class="sxs-lookup"><span data-stu-id="d2943-161">Service Fabric reserves capacity on two nodes for Application1, and doesn't allow services from Application2 to consume that capacity even if there are no load is being consumed by the services inside Application1 at the time.</span></span> <span data-ttu-id="d2943-162">Essa capacidade reservada do aplicativo é considerada consumida e conta em relação à capacidade restante naquele nó e dentro do cluster.</span><span class="sxs-lookup"><span data-stu-id="d2943-162">This reserved application capacity is considered consumed  and counts against the remaining capacity on that node and within the cluster.</span></span>  <span data-ttu-id="d2943-163">A reserva é deduzida da capacidade restante do cluster imediatamente, mas o consumo reservado é deduzido da capacidade de um nó específico somente quando pelo menos um objeto de serviço é colocado nele.</span><span class="sxs-lookup"><span data-stu-id="d2943-163">The reservation is deducted from the remaining cluster capacity immediately, however the reserved consumption is deducted from the capacity of a specific node only when at least one service object is placed on it.</span></span> <span data-ttu-id="d2943-164">Essa reserva posterior permite flexibilidade e melhor utilização de recursos já que os recursos são reservados nos nós apenas quando necessário.</span><span class="sxs-lookup"><span data-stu-id="d2943-164">This later reservation allows for flexibility and better resource utilization since resources are only reserved on nodes when needed.</span></span>

## <a name="obtaining-the-application-load-information"></a><span data-ttu-id="d2943-165">Obtendo as informações de carga do aplicativo</span><span class="sxs-lookup"><span data-stu-id="d2943-165">Obtaining the application load information</span></span>
<span data-ttu-id="d2943-166">Para cada aplicativo que tem capacidade de aplicativos definida por uma ou mais métricas que você pode obter as informações sobre a carga de agregada relatada por réplicas de seus serviços.</span><span class="sxs-lookup"><span data-stu-id="d2943-166">For each application that has an Application Capacity defined for one or more metrics you can obtain the information about the aggregate load reported by replicas of its services.</span></span>

<span data-ttu-id="d2943-167">Powershell:</span><span class="sxs-lookup"><span data-stu-id="d2943-167">Powershell:</span></span>

``` posh
Get-ServiceFabricApplicationLoad –ApplicationName fabric:/MyApplication1
```

<span data-ttu-id="d2943-168">C#</span><span class="sxs-lookup"><span data-stu-id="d2943-168">C#</span></span>

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

<span data-ttu-id="d2943-169">A consulta ApplicationLoad retorna as informações básicas sobre a Capacidade do Aplicativo que foi especificada para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d2943-169">The ApplicationLoad query returns the basic information about Application Capacity that was specified for the application.</span></span> <span data-ttu-id="d2943-170">Essas informações incluem as informações de Nós Mínimos e Nós Máximos e o número que o aplicativo está ocupando atualmente.</span><span class="sxs-lookup"><span data-stu-id="d2943-170">This information includes the Minimum Nodes and Maximum Nodes info, and the number that the application is currently occupying.</span></span> <span data-ttu-id="d2943-171">Elas também incluem informações sobre cada métrica de carga do aplicativo, incluindo:</span><span class="sxs-lookup"><span data-stu-id="d2943-171">It also includes information about each application load metric, including:</span></span>

* <span data-ttu-id="d2943-172">Nome da Métrica: o nome da métrica.</span><span class="sxs-lookup"><span data-stu-id="d2943-172">Metric Name: Name of the metric.</span></span>
* <span data-ttu-id="d2943-173">Capacidade de Reserva: a Capacidade do Cluster reservada no cluster para esse Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d2943-173">Reservation Capacity: Cluster Capacity that is reserved in the cluster for this Application.</span></span>
* <span data-ttu-id="d2943-174">Carga do Aplicativo: a Carga Total de réplicas filho deste Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d2943-174">Application Load: Total Load of this Application’s child replicas.</span></span>
* <span data-ttu-id="d2943-175">Capacidade do Aplicativo: valor máximo permitido de Carga do Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d2943-175">Application Capacity: Maximum permitted value of Application Load.</span></span>

## <a name="removing-application-capacity"></a><span data-ttu-id="d2943-176">Removendo a capacidade do aplicativo</span><span class="sxs-lookup"><span data-stu-id="d2943-176">Removing Application Capacity</span></span>
<span data-ttu-id="d2943-177">Depois que os parâmetros de Capacidade do Aplicativo estão definidos para um aplicativo, eles podem ser removidos usando cmdlets de Atualizar APIs de Aplicativo ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d2943-177">Once the Application Capacity parameters are set for an application, they can be removed using Update Application APIs or PowerShell cmdlets.</span></span> <span data-ttu-id="d2943-178">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="d2943-178">For example:</span></span>

``` posh
Update-ServiceFabricApplication –Name fabric:/MyApplication1 –RemoveApplicationCapacity

```

<span data-ttu-id="d2943-179">Esse comando remove todos os parâmetros de gerenciamento de capacidade do Aplicativo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d2943-179">This command removes all Application capacity management parameters from the application instance.</span></span> <span data-ttu-id="d2943-180">Isso inclui MinimumNodes, MaximumNodes e métricas do aplicativo, se houver.</span><span class="sxs-lookup"><span data-stu-id="d2943-180">This includes MinimumNodes, MaximumNodes, and the Application's metrics, if any.</span></span> <span data-ttu-id="d2943-181">O efeito do comando é imediato.</span><span class="sxs-lookup"><span data-stu-id="d2943-181">The effect of the command is immediate.</span></span> <span data-ttu-id="d2943-182">Após a conclusão do comando, o Cluster Resource Manager usa o comportamento padrão para o gerenciamento de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="d2943-182">After this command completes, the Cluster Resource Manager uses the default behavior for managing applications.</span></span> <span data-ttu-id="d2943-183">Os parâmetros de capacidade do aplicativo podem ser especificados novamente por meio de `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span><span class="sxs-lookup"><span data-stu-id="d2943-183">Application Capacity parameters can be specified again via `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span></span>

### <a name="restrictions-on-application-capacity"></a><span data-ttu-id="d2943-184">Restrições à capacidade do aplicativo</span><span class="sxs-lookup"><span data-stu-id="d2943-184">Restrictions on Application Capacity</span></span>
<span data-ttu-id="d2943-185">Há várias restrições aos parâmetros de Capacidade de Aplicativo que devem ser respeitadas.</span><span class="sxs-lookup"><span data-stu-id="d2943-185">There are several restrictions on Application Capacity parameters that must be respected.</span></span> <span data-ttu-id="d2943-186">Se houver erros de validação, nenhuma alteração será feita.</span><span class="sxs-lookup"><span data-stu-id="d2943-186">If there are validation errors no changes take place.</span></span>

- <span data-ttu-id="d2943-187">Todos os parâmetros de inteiro devem ser números não negativos.</span><span class="sxs-lookup"><span data-stu-id="d2943-187">All integer parameters must be non-negative numbers.</span></span>
- <span data-ttu-id="d2943-188">MinimumNodes nunca deve ser maior que MaximumNodes.</span><span class="sxs-lookup"><span data-stu-id="d2943-188">MinimumNodes must never be greater than MaximumNodes.</span></span>
- <span data-ttu-id="d2943-189">Se as capacidades de uma métrica de carga forem definidas, elas deverão seguir estas regras:</span><span class="sxs-lookup"><span data-stu-id="d2943-189">If capacities for a load metric are defined, then they must follow these rules:</span></span>
  - <span data-ttu-id="d2943-190">A Capacidade de Reserva do Nó não deve ser maior que a Capacidade Máxima do Nó.</span><span class="sxs-lookup"><span data-stu-id="d2943-190">Node Reservation Capacity must not be greater than Maximum Node Capacity.</span></span> <span data-ttu-id="d2943-191">Por exemplo, você não pode limitar a capacidade para a "CPU" métrica no nó a duas unidades e tentar reservar três unidades em cada nó.</span><span class="sxs-lookup"><span data-stu-id="d2943-191">For example, you cannot limit the capacity for the metric “CPU” on the node to two units and try to reserve three units on each node.</span></span>
  - <span data-ttu-id="d2943-192">Se MaximumNodes for especificado, o produto de MaximumNodes e a Capacidade Máxima do Nó não deverão ser maiores que a Capacidade Total do Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d2943-192">If MaximumNodes is specified, then the product of MaximumNodes and Maximum Node Capacity must not be greater than Total Application Capacity.</span></span> <span data-ttu-id="d2943-193">Por exemplo, digamos que a Capacidade Máxima do Nó da métrica de carga "CPU" seja definida como oito.</span><span class="sxs-lookup"><span data-stu-id="d2943-193">For example, let's say the Maximum Node Capacity for load metric “CPU” is set to eight.</span></span> <span data-ttu-id="d2943-194">Digamos também que você defina os Nós Máximos como 10.</span><span class="sxs-lookup"><span data-stu-id="d2943-194">Let's also say you set the Maximum Nodes to 10.</span></span> <span data-ttu-id="d2943-195">Nesse caso, a Capacidade Total do Aplicativo deve ser maior do que 80 para esta métrica de carga.</span><span class="sxs-lookup"><span data-stu-id="d2943-195">In this case, Total Application Capacity must be greater than 80 for this load metric.</span></span>

<span data-ttu-id="d2943-196">As restrições são aplicadas durante a criação e a atualização de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="d2943-196">The restrictions are enforced both during application creation and updates.</span></span>

## <a name="how-not-to-use-application-capacity"></a><span data-ttu-id="d2943-197">Como não usar a Capacidade do Aplicativo</span><span class="sxs-lookup"><span data-stu-id="d2943-197">How not to use Application Capacity</span></span>
- <span data-ttu-id="d2943-198">Não tente usar os recursos de Grupo de Aplicativos para restringir o aplicativo a um subconjunto de nós _específico_.</span><span class="sxs-lookup"><span data-stu-id="d2943-198">Do not try to use the Application Group features to constrain the application to a _specific_ subset of nodes.</span></span> <span data-ttu-id="d2943-199">Em outras palavras, você pode especificar que o aplicativo seja executado em no máximo cinco nós, mas não quais cinco nós específicos no cluster.</span><span class="sxs-lookup"><span data-stu-id="d2943-199">In other words, you can specify that the application runs on at most five nodes, but not which specific five nodes in the cluster.</span></span> <span data-ttu-id="d2943-200">A restrição de um aplicativo a nós específicos pode ser obtida usando restrições de posicionamento para os serviços.</span><span class="sxs-lookup"><span data-stu-id="d2943-200">Constraining an application to specific nodes can be achieved using placement constraints for services.</span></span>
- <span data-ttu-id="d2943-201">Não tente usar a Capacidade do Aplicativo para garantir que dois serviços do mesmo aplicativo sejam colocados nos mesmos nós.</span><span class="sxs-lookup"><span data-stu-id="d2943-201">Do not try to use the Application Capacity to ensure that two services from the same application are placed on the same nodes.</span></span> <span data-ttu-id="d2943-202">Em vez disso, use [afinidade](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) ou [restrições de posicionamento](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span><span class="sxs-lookup"><span data-stu-id="d2943-202">Instead use [affinity](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) or [placement constraints](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2943-203">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d2943-203">Next steps</span></span>
- <span data-ttu-id="d2943-204">Para saber mais sobre como configurar os serviços, [Saiba mais sobre como configurar serviços](service-fabric-cluster-resource-manager-configure-services.md)</span><span class="sxs-lookup"><span data-stu-id="d2943-204">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>
- <span data-ttu-id="d2943-205">Para descobrir como o Gerenciador de Recursos de Cluster gerencia e balanceia carga no cluster, confira o artigo sobre [como balancear carga](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="d2943-205">To find out about how the Cluster Resource Manager manages and balances load in the cluster, check out the article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>
- <span data-ttu-id="d2943-206">Comece do princípio e [veja uma introdução ao Gerenciador de Recursos de Cluster do Service Fabric](service-fabric-cluster-resource-manager-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="d2943-206">Start from the beginning and [get an Introduction to the Service Fabric Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span></span>
- <span data-ttu-id="d2943-207">Para obter mais informações sobre como as métricas funcionam em geral, leia sobre [Métricas de Carga do Service Fabric](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="d2943-207">For more information on how metrics work generally, read up on [Service Fabric Load Metrics](service-fabric-cluster-resource-manager-metrics.md)</span></span>
- <span data-ttu-id="d2943-208">O Cluster Resource Manager tem muitas opções para descrever o cluster.</span><span class="sxs-lookup"><span data-stu-id="d2943-208">The Cluster Resource Manager has many options for describing the cluster.</span></span> <span data-ttu-id="d2943-209">Para saber mais sobre elas, confira este artigo sobre a [descrição de um cluster do Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)</span><span class="sxs-lookup"><span data-stu-id="d2943-209">To find out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-max-nodes.png
[Image2]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-reserved-capacity.png
