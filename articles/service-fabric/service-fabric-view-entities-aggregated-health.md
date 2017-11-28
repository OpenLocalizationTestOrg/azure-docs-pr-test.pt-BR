---
title: Como exibir a integridade agregada das entidades do Azure Service Fabric | Microsoft Docs
description: Descreve como consultar, exibir e avaliar a integridade agregada das entidades do Azure Service Fabric, por meio de consultas de integridade e consultas gerais.
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: fa34c52d-3a74-4b90-b045-ad67afa43fe5
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: b97972b1bdc28a17fb9c3a0e997738f5bd0b5d15
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="view-service-fabric-health-reports"></a><span data-ttu-id="8cdd6-103">Como exibir relatórios de integridade do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8cdd6-103">View Service Fabric health reports</span></span>
<span data-ttu-id="8cdd6-104">O Azure Service Fabric apresenta um [modelo de integridade](service-fabric-health-introduction.md) com entidades de integridade nas quais os componentes do sistema e watchdogs podem relatar condições locais que estão monitorando.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-104">Azure Service Fabric introduces a [health model](service-fabric-health-introduction.md) with health entities on which system components and watchdogs can report local conditions that they are monitoring.</span></span> <span data-ttu-id="8cdd6-105">O [repositório de integridade](service-fabric-health-introduction.md#health-store) agrega todos os dados de integridade para determinar se as entidades estão íntegras.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-105">The [health store](service-fabric-health-introduction.md#health-store) aggregates all health data to determine whether entities are healthy.</span></span>

<span data-ttu-id="8cdd6-106">O cluster é populado automaticamente com relatórios de integridade enviados pelos componentes do sistema.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-106">The cluster is automatically populated with health reports sent by the system components.</span></span> <span data-ttu-id="8cdd6-107">Leia mais em [Usar relatórios de integridade do sistema para solução de problemas](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-107">Read more at [Use system health reports to troubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span></span>

<span data-ttu-id="8cdd6-108">O Service Fabric fornece várias maneiras de obter a integridade agregada de entidades:</span><span class="sxs-lookup"><span data-stu-id="8cdd6-108">Service Fabric provides multiple ways to get the aggregated health of the entities:</span></span>

* <span data-ttu-id="8cdd6-109">[Gerenciador de Malha do Serviço](service-fabric-visualizing-your-cluster.md) ou outras ferramentas de visualização</span><span class="sxs-lookup"><span data-stu-id="8cdd6-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) or other visualization tools</span></span>
* <span data-ttu-id="8cdd6-110">Consultas de integridade (por meio do PowerShell, da API ou de REST)</span><span class="sxs-lookup"><span data-stu-id="8cdd6-110">Health queries (through PowerShell, API, or REST)</span></span>
* <span data-ttu-id="8cdd6-111">Consultas gerais que retornam uma lista de entidades que têm a integridade como uma das propriedades (por meio do PowerShell, da API ou de REST)</span><span class="sxs-lookup"><span data-stu-id="8cdd6-111">General queries that return a list of entities that have health as one of the properties (through PowerShell, API, or REST)</span></span>

<span data-ttu-id="8cdd6-112">Para demonstrar essas opções, vamos usar um cluster local com cinco nós e o [aplicativo fabric:/WordCount](http://aka.ms/servicefabric-wordcountapp).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-112">To demonstrate these options, let's use a local cluster with five nodes and the [fabric:/WordCount application](http://aka.ms/servicefabric-wordcountapp).</span></span> <span data-ttu-id="8cdd6-113">O aplicativo **fabric:/WordCount** contém dois serviços de padrão, um serviço com estado do tipo `WordCountServiceType`e um serviço sem estado do tipo `WordCountWebServiceType`.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-113">The **fabric:/WordCount** application contains two default services, a stateful service of type `WordCountServiceType`, and a stateless service of type `WordCountWebServiceType`.</span></span> <span data-ttu-id="8cdd6-114">Alterei o `ApplicationManifest.xml` para exigir sete réplicas de destino para o serviço com estado e uma partição.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-114">I changed the `ApplicationManifest.xml` to require seven target replicas for the stateful service and one partition.</span></span> <span data-ttu-id="8cdd6-115">Como há apenas cinco nós no cluster, os componentes do sistema relatam um aviso na partição de serviço, pois ele está abaixo da contagem exigida.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-115">Because there are only five nodes in the cluster, the system components report a warning on the service partition because it is below the target count.</span></span>

```xml
<Service Name="WordCountService">
<<<<<<< HEAD
    <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="3">
      <UniformInt64Partition PartitionCount="1" LowKey="1" HighKey="26" />
    </StatefulService>
=======
  <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="2">
    <UniformInt64Partition PartitionCount="[WordCountService_PartitionCount]" LowKey="1" HighKey="26" />
  </StatefulService>
>>>>>>> 5e84dbdd8e45a5d6b36f435a550b7433b873bf11
</Service>
```

## <a name="health-in-service-fabric-explorer"></a><span data-ttu-id="8cdd6-116">Integridade no Gerenciador da Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="8cdd6-116">Health in Service Fabric Explorer</span></span>
<span data-ttu-id="8cdd6-117">O Gerenciador da Malha do Serviço fornece uma exibição visual do cluster.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-117">Service Fabric Explorer provides a visual view of the cluster.</span></span> <span data-ttu-id="8cdd6-118">Na imagem abaixo, você pode ver que:</span><span class="sxs-lookup"><span data-stu-id="8cdd6-118">In the image below, you can see that:</span></span>

* <span data-ttu-id="8cdd6-119">O aplicativo **fabric:/WordCount** está vermelho (em erro) porque ele tem um evento de erro relatado por **MyWatchdog** para a propriedade **Disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-119">The application **fabric:/WordCount** is red (in error) because it has an error event reported by **MyWatchdog** for the property **Availability**.</span></span>
* <span data-ttu-id="8cdd6-120">Um de seus serviços, **fabric:/WordCount/WordCountService** está amarelo (em aviso).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-120">One of its services, **fabric:/WordCount/WordCountService** is yellow (in warning).</span></span> <span data-ttu-id="8cdd6-121">O serviço está configurado com sete réplicas e o cluster tem cinco nós, ou seja, duas repicas não têm lugar.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-121">The service is configured with seven replicas and the cluster has five nodes, so two repicas can't be placed.</span></span> <span data-ttu-id="8cdd6-122">Embora não seja mostrado aqui, a partição de serviço está amarela porque o relatório do sistema `System.FM` indica `Partition is below target replica or instance count`.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-122">Although it's not shown here, the service partition is yellow because of a system report from `System.FM` saying that `Partition is below target replica or instance count`.</span></span> <span data-ttu-id="8cdd6-123">A partição amarela dispara o serviço amarelo.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-123">The yellow partition triggers the yellow service.</span></span>
* <span data-ttu-id="8cdd6-124">O cluster está vermelho devido ao aplicativo vermelho.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-124">The cluster is red because of the red application.</span></span>

<span data-ttu-id="8cdd6-125">A avaliação usa políticas padrão do manifesto do cluster e do manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-125">The evaluation uses default policies from the cluster manifest and application manifest.</span></span> <span data-ttu-id="8cdd6-126">Elas são políticas rígidas e não toleram falhas.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-126">They are strict policies and do not tolerate any failure.</span></span>

<span data-ttu-id="8cdd6-127">Visualização do cluster com o Gerenciador do Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="8cdd6-127">View of the cluster with Service Fabric Explorer:</span></span>

![Visualização do cluster com o Gerenciador do Service Fabric.][1]

[1]: ./media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> <span data-ttu-id="8cdd6-129">Leia mais sobre o [Gerenciador da Malha do Serviço](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-129">Read more about [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

## <a name="health-queries"></a><span data-ttu-id="8cdd6-130">Consultas de integridade</span><span class="sxs-lookup"><span data-stu-id="8cdd6-130">Health queries</span></span>
<span data-ttu-id="8cdd6-131">A Malha do Serviço expõe consultas de integridade para cada um dos [tipos de entidade](service-fabric-health-introduction.md#health-entities-and-hierarchy)com suporte.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-131">Service Fabric exposes health queries for each of the supported [entity types](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span></span> <span data-ttu-id="8cdd6-132">Elas podem ser acessados pela API usando métodos de [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), por cmdlets do PowerShell e por REST.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-132">They can be accessed through the API, using methods on [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="8cdd6-133">Essas consultas retornam informações de integridade completas sobre a entidade: o estado de integridade agregada, eventos de integridade da entidade, estados de integridade dos filhos (quando aplicável), avaliações não íntegras (quando a entidade não está íntegra) e estatísticas sobre a integridade dos filhos (quando aplicável).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-133">These queries return complete health information about the entity: the aggregated health state, entity health events, child health states (when applicable), unhealthy evaluations (when the entity is not healthy), and children health statistics (when applicable).</span></span>

> [!NOTE]
> <span data-ttu-id="8cdd6-134">Uma entidade de integridade retorna para o usuário quando ela é totalmente populada no repositório de integridade.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-134">A health entity is returned when it is fully populated in the health store.</span></span> <span data-ttu-id="8cdd6-135">A entidade deve estar ativa (não excluída) e ter um relatório do sistema.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-135">The entity must be active (not deleted) and have a system report.</span></span> <span data-ttu-id="8cdd6-136">Suas entidades pai na cadeia hierárquica também devem ter relatórios do sistema.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-136">Its parent entities on the hierarchy chain must also have system reports.</span></span> <span data-ttu-id="8cdd6-137">Se alguma dessas condições não for atendida, as consultas de integridade retornam um [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) com [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` que mostra por que a entidade não é retornada.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-137">If any of these conditions are not satisfied, the health queries return a [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) with [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` that shows why the entity is not returned.</span></span>
>
>

<span data-ttu-id="8cdd6-138">As consultas de integridade devem passar pelo identificador da entidade, que depende do tipo de entidade.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-138">The health queries must pass in the entity identifier, which depends on the entity type.</span></span> <span data-ttu-id="8cdd6-139">As consultas aceitam parâmetros opcionais da política de integridade.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-139">The queries accept optional health policy parameters.</span></span> <span data-ttu-id="8cdd6-140">Se nenhuma política de integridade for especificada, as [políticas de integridade](service-fabric-health-introduction.md#health-policies) do manifesto do cluster ou do aplicativo serão usadas para avaliação.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-140">If no health policies are specified, the [health policies](service-fabric-health-introduction.md#health-policies) from the cluster or application manifest are used for evaluation.</span></span> <span data-ttu-id="8cdd6-141">Se os manifestos não contêm uma definição para políticas de integridade, as políticas de integridade padrão são usadas para avaliação.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-141">If the manifests don't contain a definition for health policies, the default health policies are used for evaluation.</span></span> <span data-ttu-id="8cdd6-142">As políticas de integridade padrão não toleram falhas.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-142">The default health policies do not tolerate any failures.</span></span> <span data-ttu-id="8cdd6-143">As consultas também aceitam filtros para retornar apenas eventos ou filhos parciais; aqueles que respeitarem os filtros especificados.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-143">The queries also accept filters for returning only partial children or events--the ones that respect the specified filters.</span></span> <span data-ttu-id="8cdd6-144">Outro filtro permite a exclusão das estatísticas de filhos.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-144">Another filter allows excluding the children statistics.</span></span>

> [!NOTE]
> <span data-ttu-id="8cdd6-145">Os filtros de saída são aplicados no lado do servidor, de modo que o tamanho da resposta da mensagem é reduzido.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-145">The output filters are applied on the server side, so the message reply size is reduced.</span></span> <span data-ttu-id="8cdd6-146">Recomendamos o uso dos filtros de saída para limitar os dados retornados, em vez de aplicar filtros no lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-146">We recommended that you use the output filters to limit the data returned, rather than apply filters on the client side.</span></span>
>
>

<span data-ttu-id="8cdd6-147">A integridade da entidade contém:</span><span class="sxs-lookup"><span data-stu-id="8cdd6-147">An entity's health contains:</span></span>

* <span data-ttu-id="8cdd6-148">O estado da integridade agregada da entidade.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-148">The aggregated health state of the entity.</span></span> <span data-ttu-id="8cdd6-149">Ele é calculado pelo repositório de integridade com base nos relatórios de integridade da entidade, pelos estados da integridade dos filhos (quando aplicável) e por políticas de integridade.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-149">Computed by the health store based on entity health reports, child health states (when applicable), and health policies.</span></span> <span data-ttu-id="8cdd6-150">Leia mais sobre [Avaliação de integridade da entidade](service-fabric-health-introduction.md#health-evaluation).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-150">Read more about [entity health evaluation](service-fabric-health-introduction.md#health-evaluation).</span></span>  
* <span data-ttu-id="8cdd6-151">Os eventos de integridade da entidade.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-151">The health events on the entity.</span></span>
* <span data-ttu-id="8cdd6-152">A coleção de estados de integridade de todos os filhos das entidades que podem ter filhos.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-152">The collection of health states of all children for the entities that can have children.</span></span> <span data-ttu-id="8cdd6-153">Os estados da integridade contêm identificadores de entidade e o estado da integridade agregada.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-153">The health states contain entity identifiers and the aggregated health state.</span></span> <span data-ttu-id="8cdd6-154">Para obter toda a integridade de um filho, chame a integridade de consulta do tipo de entidade filho e passe o identificador do filho.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-154">To get complete health for a child, call the query health for the child entity type and pass in the child identifier.</span></span>
* <span data-ttu-id="8cdd6-155">As avaliações não íntegras que apontam para o relatório que disparou o estado da entidade, se a entidade não estiver íntegra.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-155">The unhealthy evaluations that point to the report that triggered the state of the entity, if the entity is not healthy.</span></span> <span data-ttu-id="8cdd6-156">As avaliações são recursivas, contendo as avaliações de integridade de filhos que dispararam o estado de integridade atual.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-156">The evaluations are recursive, containing the children health evaluations that triggered current health state.</span></span> <span data-ttu-id="8cdd6-157">Por exemplo, um watchdog relatou um erro em uma réplica.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-157">For example, a watchdog reported an error against a replica.</span></span> <span data-ttu-id="8cdd6-158">A integridade do aplicativo mostra uma avaliação não íntegra devido a um serviço não íntegro; o serviço não está íntegro devido a uma partição com erro; a partição não está íntegra devido a uma réplica com erro; a réplica não está íntegra devido ao relatório de integridade do watchdog com erro.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-158">The application health shows an unhealthy evaluation due to an unhealthy service; the service is unhealthy due to a partition in error; the partition is unhealthy due to a replica in error; the replica is unhealthy due to the watchdog error health report.</span></span>
* <span data-ttu-id="8cdd6-159">As estatísticas de integridade para todos os tipos de filho de entidades que têm filhos.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-159">The health statistics for all children types of the entities that have children.</span></span> <span data-ttu-id="8cdd6-160">Por exemplo, a integridade do cluster mostra o número total de aplicativos, serviços, partições, réplicas e entidades implantadas no cluster.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-160">For example, cluster health shows the total number of applications, services, partitions, replicas, and deployed entities in the cluster.</span></span> <span data-ttu-id="8cdd6-161">A integridade do serviço mostra o número total de partições e réplicas no serviço especificado.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-161">Service health shows the total number of partitions and replicas under the specified service.</span></span>

## <a name="get-cluster-health"></a><span data-ttu-id="8cdd6-162">Obter integridade do cluster</span><span class="sxs-lookup"><span data-stu-id="8cdd6-162">Get cluster health</span></span>
<span data-ttu-id="8cdd6-163">Retorna a integridade da entidade do cluster e contém os estados da integridade de aplicativos e nós (filhos do cluster).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-163">Returns the health of the cluster entity and contains the health states of applications and nodes (children of the cluster).</span></span> <span data-ttu-id="8cdd6-164">Entrada:</span><span class="sxs-lookup"><span data-stu-id="8cdd6-164">Input:</span></span>

* <span data-ttu-id="8cdd6-165">[Opcional] A política de integridade do cluster usada para avaliar os nós e os eventos de cluster.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-165">[Optional] The cluster health policy used to evaluate the nodes and the cluster events.</span></span>
* <span data-ttu-id="8cdd6-166">[Opcional] Mapa da política de integridade do aplicativo, com políticas de integridade usadas para substituir as políticas do manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-166">[Optional] The application health policy map, with the health policies used to override the application manifest policies.</span></span>
* <span data-ttu-id="8cdd6-167">[Opcional] Filtros de eventos, nós e aplicativos que especificam quais entradas são interessantes e devem retornar nos resultados (por exemplo, apenas erros ou avisos e erros).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-167">[Optional] Filters for events, nodes, and applications that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="8cdd6-168">Todos os eventos, nós e aplicativos são usados para avaliar a integridade agregada da entidade, independentemente do filtro.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-168">All events, nodes, and applications are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="8cdd6-169">[Opcional] Filtrar para excluir as estatísticas de integridade.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-169">[Optional] Filter to exclude health statistics.</span></span>
* <span data-ttu-id="8cdd6-170">[Opcional] Filtrar para incluir as estatísticas de integridade do fabric:/System nas estatísticas de integridade.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-170">[Optional] Filter to include fabric:/System health statistics in the health statistics.</span></span> <span data-ttu-id="8cdd6-171">Aplicável somente quando as estatísticas de integridade não são excluídas.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-171">Only applicable when the health statistics are not excluded.</span></span> <span data-ttu-id="8cdd6-172">Por padrão, as estatísticas de integridade incluem somente as estatísticas de aplicativos de usuário e não o aplicativo System.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-172">By default, the health statistics include only statistics for user applications and not the System application.</span></span>

### <a name="api"></a><span data-ttu-id="8cdd6-173">API</span><span class="sxs-lookup"><span data-stu-id="8cdd6-173">API</span></span>
<span data-ttu-id="8cdd6-174">Para obter a integridade do cluster, crie um `FabricClient` e chame o método [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) em seu **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-174">To get cluster health, create a `FabricClient` and call the [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) method on its **HealthManager**.</span></span>

<span data-ttu-id="8cdd6-175">A chamada a seguir obtém a integridade do cluster:</span><span class="sxs-lookup"><span data-stu-id="8cdd6-175">The following call gets the cluster health:</span></span>

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

<span data-ttu-id="8cdd6-176">O código a seguir obtém a integridade do cluster usando política de integridade de cluster personalizada para nós e aplicativos.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-176">The following code gets the cluster health by using a custom cluster health policy and filters for nodes and applications.</span></span> <span data-ttu-id="8cdd6-177">Especifica que as estatísticas de integridade incluem as estatísticas de fabric:/System.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-177">It specifies that the health statistics include the fabric:/System statistics.</span></span> <span data-ttu-id="8cdd6-178">Ele cria [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), que contém as informações de entrada.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-178">It creates [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), which contains the input information.</span></span>

```csharp
var policy = new ClusterHealthPolicy()
{
    MaxPercentUnhealthyNodes = 20
};
var nodesFilter = new NodeHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error | HealthStateFilter.Warning
};
var applicationsFilter = new ApplicationHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error
};
var healthStatisticsFilter = new ClusterHealthStatisticsFilter()
{
    ExcludeHealthStatistics = false,
    IncludeSystemApplicationHealthStatistics = true
};
var queryDescription = new ClusterHealthQueryDescription()
{
    HealthPolicy = policy,
    ApplicationsFilter = applicationsFilter,
    NodesFilter = nodesFilter,
    HealthStatisticsFilter = healthStatisticsFilter
};

ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="8cdd6-179">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8cdd6-179">PowerShell</span></span>
<span data-ttu-id="8cdd6-180">O cmdlet para obter a integridade do cluster é [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-180">The cmdlet to get the cluster health is [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span></span> <span data-ttu-id="8cdd6-181">Primeiro, conecte-se ao cluster usando o cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="8cdd6-181">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="8cdd6-182">Estado do cluster é de cinco nós, o aplicativo do sistema e fabric:/WordCount configurados conforme descrito.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-182">The state of the cluster is five nodes, the system application, and fabric:/WordCount configured as described.</span></span>

<span data-ttu-id="8cdd6-183">O cmdlet a seguir obtém a integridade do cluster usando políticas de integridade padrão.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-183">The following cmdlet gets cluster health by using default health policies.</span></span> <span data-ttu-id="8cdd6-184">O estado de integridade agregada é de aviso, pois o aplicativo fabric:/WordCount está em aviso.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-184">The aggregated health state is warning, because the fabric:/WordCount application is in warning.</span></span> <span data-ttu-id="8cdd6-185">Observe como as avaliações não íntegras mostram com detalhes a condição que disparou a integridade agregada.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-185">Note how the unhealthy evaluations provide details on the conditions that triggered the aggregated health.</span></span>

```xml
PS D:\ServiceFabric> Get-ServiceFabricClusterHealth


AggregatedHealthState   : Warning
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Warning'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                          
                          
NodeHealthStates        : 
                          NodeName              : _Node_4
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_3
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_2
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_1
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_0
                          AggregatedHealthState : Ok
                          
ApplicationHealthStates : 
                          ApplicationName       : fabric:/System
                          AggregatedHealthState : Ok
                          
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Warning
                          
HealthEvents            : None
HealthStatistics        : 
                          Node                  : 5 Ok, 0 Warning, 0 Error
                          Replica               : 6 Ok, 0 Warning, 0 Error
                          Partition             : 1 Ok, 1 Warning, 0 Error
                          Service               : 1 Ok, 1 Warning, 0 Error
                          DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                          DeployedApplication   : 5 Ok, 0 Warning, 0 Error
                          Application           : 0 Ok, 1 Warning, 0 Error
```

<span data-ttu-id="8cdd6-186">O cmdlet do PowerShell a seguir obtém a integridade do cluster usando uma política de aplicativo personalizada.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-186">The following PowerShell cmdlet gets the health of the cluster by using a custom application policy.</span></span> <span data-ttu-id="8cdd6-187">Ele filtra os resultados para obter apenas os aplicativos e nós com erro ou aviso.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-187">It filters results to get only applications and nodes in error or warning.</span></span> <span data-ttu-id="8cdd6-188">Como resultado nenhum nó é retornado, pois todos estão íntegros.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-188">As a result, no nodes are returned, as they are all healthy.</span></span> <span data-ttu-id="8cdd6-189">Somente o aplicativo fabric:/WordCount respeita o filtro de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-189">Only the fabric:/WordCount application respects the applications filter.</span></span> <span data-ttu-id="8cdd6-190">Como a política personalizada especifica a consideração de avisos como erros para o aplicativo fabric:/WordCount, o aplicativo é avaliado como em estado de erro, assim como o cluster.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-190">Because the custom policy specifies to consider warnings as errors for the fabric:/WordCount application, the application is evaluated as in error, and so is the cluster.</span></span>

```powershell
PS D:\ServiceFabric> $appHealthPolicy = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicy
$appHealthPolicy.ConsiderWarningAsError = $true
$appHealthPolicyMap = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicyMap
$appUri1 = New-Object -TypeName System.Uri -ArgumentList "fabric:/WordCount"
$appHealthPolicyMap.Add($appUri1, $appHealthPolicy)
Get-ServiceFabricClusterHealth -ApplicationHealthPolicyMap $appHealthPolicyMap -ApplicationsFilter "Warning,Error" -NodesFilter "Warning,Error" -ExcludeHealthStatistics


AggregatedHealthState   : Error
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Error'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                          
                          
NodeHealthStates        : None
ApplicationHealthStates : 
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Error
                          
HealthEvents            : None
```

### <a name="rest"></a><span data-ttu-id="8cdd6-191">REST</span><span class="sxs-lookup"><span data-stu-id="8cdd6-191">REST</span></span>
<span data-ttu-id="8cdd6-192">Você pode obter a integridade do cluster com uma [solicitação GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) ou uma [solicitação POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy), que inclui as políticas de integridade descritas no corpo.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-192">You can get cluster health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-node-health"></a><span data-ttu-id="8cdd6-193">Obter integridade do nó</span><span class="sxs-lookup"><span data-stu-id="8cdd6-193">Get node health</span></span>
<span data-ttu-id="8cdd6-194">Retorna a integridade de uma entidade de nó e contém os eventos de integridade reportados no nó.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-194">Returns the health of a node entity and contains the health events reported on the node.</span></span> <span data-ttu-id="8cdd6-195">Entrada:</span><span class="sxs-lookup"><span data-stu-id="8cdd6-195">Input:</span></span>

* <span data-ttu-id="8cdd6-196">[Obrigatório] O nome do nó que identifica o nó.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-196">[Required] The node name that identifies the node.</span></span>
* <span data-ttu-id="8cdd6-197">[Opcional] As configurações da política de integridade do cluster usadas para avaliar a integridade.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-197">[Optional] The cluster health policy settings used to evaluate health.</span></span>
* <span data-ttu-id="8cdd6-198">[Opcional] Filtros de eventos que especificam quais entradas são interessantes e devem retornar nos resultados (por exemplo, apenas erros ou avisos e erros).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-198">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="8cdd6-199">Todos os eventos são usados para avaliar a integridade agregada da entidade, independentemente do filtro.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-199">All events are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="8cdd6-200">API</span><span class="sxs-lookup"><span data-stu-id="8cdd6-200">API</span></span>
<span data-ttu-id="8cdd6-201">Para obter a integridade do nó por meio da API, crie um `FabricClient` e chame o método [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) em seu HealthManager.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-201">To get node health through the API, create a `FabricClient` and call the [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="8cdd6-202">O código a seguir obtém a integridade de nó para o nome de nó especificado:</span><span class="sxs-lookup"><span data-stu-id="8cdd6-202">The following code gets the node health for the specified node name:</span></span>

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

<span data-ttu-id="8cdd6-203">O código a seguir obtém a integridade de nó para o nome do nó especificado e passa um filtro de eventos e política personalizada por meio de [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="8cdd6-203">The following code gets the node health for the specified node name and passes in events filter and custom policy through [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span></span>

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="8cdd6-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8cdd6-204">PowerShell</span></span>
<span data-ttu-id="8cdd6-205">O cmdlet para obter a integridade do nó é [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-205">The cmdlet to get the node health is [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span></span> <span data-ttu-id="8cdd6-206">Primeiro, conecte-se ao cluster usando o cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="8cdd6-206">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>
<span data-ttu-id="8cdd6-207">O cmdlet a seguir obtém a integridade do nó usando políticas de integridade padrão:</span><span class="sxs-lookup"><span data-stu-id="8cdd6-207">The following cmdlet gets the node health by using default health policies:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNodeHealth _Node_1


NodeName              : _Node_1
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 3
                        SentAt                : 7/13/2017 4:39:23 PM
                        ReceivedAt            : 7/13/2017 4:40:47 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 4:40:47 PM, LastWarning = 1/1/0001 12:00:00 AM
```

<span data-ttu-id="8cdd6-208">O cmdlet a seguir obtém a integridade de todos os nós no cluster.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-208">The following cmdlet gets the health of all nodes in the cluster:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNode | Get-ServiceFabricNodeHealth | select NodeName, AggregatedHealthState | ft -AutoSize

NodeName AggregatedHealthState
-------- ---------------------
_Node_4                     Ok
_Node_3                     Ok
_Node_2                     Ok
_Node_1                     Ok
_Node_0                     Ok
```

### <a name="rest"></a><span data-ttu-id="8cdd6-209">REST</span><span class="sxs-lookup"><span data-stu-id="8cdd6-209">REST</span></span>
<span data-ttu-id="8cdd6-210">Você pode obter a integridade do nó com uma [solicitação GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) ou uma [solicitação POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy), que inclui as políticas de integridade descritas no corpo.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-210">You can get node health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-application-health"></a><span data-ttu-id="8cdd6-211">Obter integridade do aplicativo</span><span class="sxs-lookup"><span data-stu-id="8cdd6-211">Get application health</span></span>
<span data-ttu-id="8cdd6-212">Retorna a integridade de uma entidade de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-212">Returns the health of an application entity.</span></span> <span data-ttu-id="8cdd6-213">Contém os estados de integridade do aplicativo implantado e filhos de serviço.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-213">It contains the health states of the deployed application and service children.</span></span> <span data-ttu-id="8cdd6-214">Entrada:</span><span class="sxs-lookup"><span data-stu-id="8cdd6-214">Input:</span></span>

* <span data-ttu-id="8cdd6-215">[Obrigatório] O nome do aplicativo (URI) que identifica o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-215">[Required] The application name (URI) that identifies the application.</span></span>
* <span data-ttu-id="8cdd6-216">[Opcional] A política de integridade do aplicativo usada para substituir as políticas do manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-216">[Optional] The application health policy used to override the application manifest policies.</span></span>
* <span data-ttu-id="8cdd6-217">[Opcional] Filtros de eventos, serviços e aplicativos implantados que especificam quais entradas são interessantes e devem retornar nos resultados (por exemplo, apenas erros ou avisos e erros).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-217">[Optional] Filters for events, services, and deployed applications that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="8cdd6-218">Todos os eventos, serviços e aplicativos implantados são usados para avaliar a integridade agregada da entidade, independentemente do filtro.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-218">All events, services, and deployed applications are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="8cdd6-219">[Opcional] Filtrar para excluir as estatísticas de integridade.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-219">[Optional] Filter to exclude the health statistics.</span></span> <span data-ttu-id="8cdd6-220">Se não for especificado, as estatísticas de integridade incluem a contagem de OK, avisos e erros para todos os filhos do aplicativo: serviços, partições, réplicas, aplicativos implantados e pacotes de serviço implantados.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-220">If not specified, the health statistics include the ok, warning, and error count for all application children: services, partitions, replicas, deployed applications, and deployed service packages.</span></span>

### <a name="api"></a><span data-ttu-id="8cdd6-221">API</span><span class="sxs-lookup"><span data-stu-id="8cdd6-221">API</span></span>
<span data-ttu-id="8cdd6-222">Para obter a integridade do aplicativo, crie um `FabricClient` e chame o método [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) em seu HealthManager.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-222">To get application health, create a `FabricClient` and call the [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="8cdd6-223">O código a seguir obtém a integridade do aplicativo para o nome do aplicativo especificado (URI):</span><span class="sxs-lookup"><span data-stu-id="8cdd6-223">The following code gets the application health for the specified application name (URI):</span></span>

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

<span data-ttu-id="8cdd6-224">O código a seguir obtém a integridade do aplicativo para o nome do aplicativo especificado (URI), com filtros e políticas personalizadas especificadas por meio de [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-224">The following code gets the application health for the specified application name (URI), with filters and custom policies specified via [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span></span>

```csharp
HealthStateFilter warningAndErrors = HealthStateFilter.Error | HealthStateFilter.Warning;
var serviceTypePolicy = new ServiceTypeHealthPolicy()
{
    MaxPercentUnhealthyPartitionsPerService = 0,
    MaxPercentUnhealthyReplicasPerPartition = 5,
    MaxPercentUnhealthyServices = 0,
};
var policy = new ApplicationHealthPolicy()
{
    ConsiderWarningAsError = false,
    DefaultServiceTypeHealthPolicy = serviceTypePolicy,
    MaxPercentUnhealthyDeployedApplications = 0,
};

var queryDescription = new ApplicationHealthQueryDescription(applicationName)
{
    HealthPolicy = policy,
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = warningAndErrors },
    ServicesFilter = new ServiceHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
    DeployedApplicationsFilter = new DeployedApplicationHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
};

ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="8cdd6-225">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8cdd6-225">PowerShell</span></span>
<span data-ttu-id="8cdd6-226">O cmdlet para obter a integridade do aplicativos é [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-226">The cmdlet to get the application health is [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="8cdd6-227">Primeiro, conecte-se ao cluster usando o cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="8cdd6-227">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="8cdd6-228">O cmdlet a seguir retorna a integridade do aplicativo **fabric:/WordCount** :</span><span class="sxs-lookup"><span data-stu-id="8cdd6-228">The following cmdlet returns the health of the **fabric:/WordCount** application:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Warning
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok
                                  
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Warning
                                  
DeployedApplicationHealthStates : 
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok
                                  
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/13/2017 5:57:05 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
                                  
HealthStatistics                : 
                                  Replica               : 6 Ok, 0 Warning, 0 Error
                                  Partition             : 1 Ok, 1 Warning, 0 Error
                                  Service               : 1 Ok, 1 Warning, 0 Error
                                  DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                                  DeployedApplication   : 5 Ok, 0 Warning, 0 Error
```

<span data-ttu-id="8cdd6-229">O cmdlet do PowerShell a seguir passa políticas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-229">The following PowerShell cmdlet passes in custom policies.</span></span> <span data-ttu-id="8cdd6-230">Ele também filtra filhos e eventos.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-230">It also filters children and events.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth -ApplicationName fabric:/WordCount -ConsiderWarningAsError $true -ServicesFilter Error -EventsFilter Error -DeployedApplicationsFilter Error -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error
                                  
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

### <a name="rest"></a><span data-ttu-id="8cdd6-231">REST</span><span class="sxs-lookup"><span data-stu-id="8cdd6-231">REST</span></span>
<span data-ttu-id="8cdd6-232">Você pode obter a integridade do aplicativo com uma [solicitação GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) ou uma [solicitação POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy), que inclui as políticas de integridade descritas no corpo.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-232">You can get application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-service-health"></a><span data-ttu-id="8cdd6-233">Obter integridade do serviço</span><span class="sxs-lookup"><span data-stu-id="8cdd6-233">Get service health</span></span>
<span data-ttu-id="8cdd6-234">Retorna a integridade de uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-234">Returns the health of a service entity.</span></span> <span data-ttu-id="8cdd6-235">Além disso, contém os estados de integridade da partição.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-235">It contains the partition health states.</span></span> <span data-ttu-id="8cdd6-236">Entrada:</span><span class="sxs-lookup"><span data-stu-id="8cdd6-236">Input:</span></span>

* <span data-ttu-id="8cdd6-237">[Obrigatório] O nome de serviço (URI) que identifica o serviço.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-237">[Required] The service name (URI) that identifies the service.</span></span>
* <span data-ttu-id="8cdd6-238">[Opcional] A política de integridade do aplicativo usada para substituir a política do manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-238">[Optional] The application health policy used to override the application manifest policy.</span></span>
* <span data-ttu-id="8cdd6-239">[Opcional] Filtros de eventos e partições que especificam quais entradas são interessantes e devem retornar nos resultados (por exemplo, apenas erros ou avisos e erros).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-239">[Optional] Filters for events and partitions that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="8cdd6-240">Todos os eventos e partições são usados para avaliar a integridade agregada da entidade, independentemente do filtro.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-240">All events and partitions are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="8cdd6-241">[Opcional] Filtrar para excluir as estatísticas de integridade.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-241">[Optional] Filter to exclude health statistics.</span></span> <span data-ttu-id="8cdd6-242">Se não for especificado, as estatísticas de integridade mostram a contagem de OK, avisos e erros de todas as partições e réplicas do serviço.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-242">If not specified, the health statistics show the ok, warning, and error count for all partitions and replicas of the service.</span></span>

### <a name="api"></a><span data-ttu-id="8cdd6-243">API</span><span class="sxs-lookup"><span data-stu-id="8cdd6-243">API</span></span>
<span data-ttu-id="8cdd6-244">Para obter a integridade do serviço por meio de API, crie um `FabricClient` e chame o método [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) em seu HealthManager.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-244">To get service health through the API, create a `FabricClient` and call the [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="8cdd6-245">O exemplo a seguir obtém a integridade de um serviço com o nome do serviço especificado (URI):</span><span class="sxs-lookup"><span data-stu-id="8cdd6-245">The following example gets the health of a service with specified service name (URI):</span></span>

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

<span data-ttu-id="8cdd6-246">O código a seguir obtém a integridade do serviço para o nome do serviço especificado (URI), especificando filtros e política personalizada por meio de [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="8cdd6-246">The following code gets the service health for the specified service name (URI), specifying filters and custom policy via [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span></span>

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="8cdd6-247">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8cdd6-247">PowerShell</span></span>
<span data-ttu-id="8cdd6-248">O cmdlet para obter a integridade do serviço é [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-248">The cmdlet to get the service health is [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span></span> <span data-ttu-id="8cdd6-249">Primeiro, conecte-se ao cluster usando o cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="8cdd6-249">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="8cdd6-250">O cmdlet a seguir obtém a integridade do serviço usando políticas de integridade padrão:</span><span class="sxs-lookup"><span data-stu-id="8cdd6-250">The following cmdlet gets the service health by using default health policies:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricServiceHealth -ServiceName fabric:/WordCount/WordCountService


ServiceName           : fabric:/WordCount/WordCountService
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                        
                        Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                        
                            Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
PartitionHealthStates : 
                        PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                        AggregatedHealthState : Warning
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 15
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
                        Partition             : 0 Ok, 1 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="8cdd6-251">REST</span><span class="sxs-lookup"><span data-stu-id="8cdd6-251">REST</span></span>
<span data-ttu-id="8cdd6-252">Você pode obter a integridade do serviço com uma [solicitação GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) ou uma [solicitação POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy), que inclui as políticas de integridade descritas no corpo.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-252">You can get service health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-partition-health"></a><span data-ttu-id="8cdd6-253">Obter integridade da partição</span><span class="sxs-lookup"><span data-stu-id="8cdd6-253">Get partition health</span></span>
<span data-ttu-id="8cdd6-254">Retorna a integridade de uma entidade de partição.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-254">Returns the health of a partition entity.</span></span> <span data-ttu-id="8cdd6-255">Além disso, contém os estados de integridade da réplica.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-255">It contains the replica health states.</span></span> <span data-ttu-id="8cdd6-256">Entrada:</span><span class="sxs-lookup"><span data-stu-id="8cdd6-256">Input:</span></span>

* <span data-ttu-id="8cdd6-257">[Obrigatório] A ID de partição (GUID) que identifica a partição.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-257">[Required] The partition ID (GUID) that identifies the partition.</span></span>
* <span data-ttu-id="8cdd6-258">[Opcional] A política de integridade do aplicativo usada para substituir a política do manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-258">[Optional] The application health policy used to override the application manifest policy.</span></span>
* <span data-ttu-id="8cdd6-259">[Opcional] Filtros para eventos e réplicas que especificam quais entradas são interessantes e devem retornar nos resultados (por exemplo, apenas erros ou avisos e erros).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-259">[Optional] Filters for events and replicas that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="8cdd6-260">Todos os eventos e réplicas são usados para avaliar a integridade agregada da entidade, independentemente do filtro.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-260">All events and replicas are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="8cdd6-261">[Opcional] Filtrar para excluir as estatísticas de integridade.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-261">[Optional] Filter to exclude health statistics.</span></span> <span data-ttu-id="8cdd6-262">Se não for especificado, as estatísticas de integridade mostram quantas réplicas estão nos estados OK, aviso e erro.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-262">If not specified, the health statistics show how many replicas are in ok, warning, and error states.</span></span>

### <a name="api"></a><span data-ttu-id="8cdd6-263">API</span><span class="sxs-lookup"><span data-stu-id="8cdd6-263">API</span></span>
<span data-ttu-id="8cdd6-264">Para obter a integridade da partição por meio de API, crie um `FabricClient` e chame o método [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) em seu HealthManager.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-264">To get partition health through the API, create a `FabricClient` and call the [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="8cdd6-265">Para especificar parâmetros opcionais, crie [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-265">To specify optional parameters, create [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span></span>

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a><span data-ttu-id="8cdd6-266">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8cdd6-266">PowerShell</span></span>
<span data-ttu-id="8cdd6-267">O cmdlet para obter a integridade da partição é [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-267">The cmdlet to get the partition health is [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span></span> <span data-ttu-id="8cdd6-268">Primeiro, conecte-se ao cluster usando o cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="8cdd6-268">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="8cdd6-269">O cmdlet a seguir obtém a integridade de todas as partições do serviço **fabric:/WordCount/WordCountService** e filtra excluindo os estados de integridade replicados:</span><span class="sxs-lookup"><span data-stu-id="8cdd6-269">The following cmdlet gets the health for all partitions of the **fabric:/WordCount/WordCountService** service and filters out replica health states:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 72
                        SentAt                : 7/13/2017 5:57:29 PM
                        ReceivedAt            : 7/13/2017 5:57:48 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/P RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/S RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Ok->Warning = 7/13/2017 5:57:48 PM, LastError = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131444445174851664
                        SentAt                : 7/13/2017 6:35:17 PM
                        ReceivedAt            : 7/13/2017 6:35:18 PM
                        TTL                   : 00:01:05
                        Description           : The Load Balancer was unable to find a placement for one or more of the Service's Replicas:
                        Secondary replica could not be placed due to the following constraints and properties:  
                        TargetReplicaSetSize: 7
                        Placement Constraint: N/A
                        Parent Service: N/A
                        
                        Constraint Elimination Sequence:
                        Existing Secondary Replicas eliminated 4 possible node(s) for placement -- 1/5 node(s) remain.
                        Existing Primary Replica eliminated 1 possible node(s) for placement -- 0/5 node(s) remain.
                        
                        Nodes Eliminated By Constraints:
                        
                        Existing Secondary Replicas -- Nodes with Partition's Existing Secondary Replicas/Instances:
                        --
                        FaultDomain:fd:/4 NodeName:_Node_4 NodeType:NodeType4 UpgradeDomain:4 UpgradeDomain: ud:/4 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/3 NodeName:_Node_3 NodeType:NodeType3 UpgradeDomain:3 UpgradeDomain: ud:/3 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/13/2017 5:57:48 PM, LastOk = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="8cdd6-270">REST</span><span class="sxs-lookup"><span data-stu-id="8cdd6-270">REST</span></span>
<span data-ttu-id="8cdd6-271">Você pode obter a integridade da partição com uma [solicitação GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) ou uma [solicitação POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy), que inclui as políticas de integridade descritas no corpo.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-271">You can get partition health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-replica-health"></a><span data-ttu-id="8cdd6-272">Obter integridade da réplica</span><span class="sxs-lookup"><span data-stu-id="8cdd6-272">Get replica health</span></span>
<span data-ttu-id="8cdd6-273">Retorna a integridade de uma réplica de serviço com estado ou uma instância de serviço sem estado.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-273">Returns the health of a stateful service replica or a stateless service instance.</span></span> <span data-ttu-id="8cdd6-274">Entrada:</span><span class="sxs-lookup"><span data-stu-id="8cdd6-274">Input:</span></span>

* <span data-ttu-id="8cdd6-275">[Obrigatório] A ID da partição (GUID) e a ID da réplica que identifica a réplica.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-275">[Required] The partition ID (GUID) and replica ID that identifies the replica.</span></span>
* <span data-ttu-id="8cdd6-276">[Opcional] Os parâmetros da política de integridade do aplicativo usados para substituir as políticas de manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-276">[Optional] The application health policy parameters used to override the application manifest policies.</span></span>
* <span data-ttu-id="8cdd6-277">[Opcional] Filtros de eventos que especificam quais entradas são interessantes e devem retornar nos resultados (por exemplo, apenas erros ou avisos e erros).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-277">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="8cdd6-278">Todos os eventos são usados para avaliar a integridade agregada da entidade, independentemente do filtro.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-278">All events are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="8cdd6-279">API</span><span class="sxs-lookup"><span data-stu-id="8cdd6-279">API</span></span>
<span data-ttu-id="8cdd6-280">Para obter a integridade da réplica por meio de API, crie um `FabricClient` e chame o método [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) em seu HealthManager.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-280">To get the replica health through the API, create a `FabricClient` and call the [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) method on its HealthManager.</span></span> <span data-ttu-id="8cdd6-281">Para especificar parâmetros avançados, use [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-281">To specify advanced parameters, use [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span></span>

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a><span data-ttu-id="8cdd6-282">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8cdd6-282">PowerShell</span></span>
<span data-ttu-id="8cdd6-283">O cmdlet para obter a integridade da réplica é [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-283">The cmdlet to get the replica health is [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span></span> <span data-ttu-id="8cdd6-284">Primeiro, conecte-se ao cluster usando o cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="8cdd6-284">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="8cdd6-285">O cmdlet a seguir obtém a integridade da réplica primária para todas as partições do serviço.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-285">The following cmdlet gets the health of the primary replica for all partitions of the service:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="8cdd6-286">REST</span><span class="sxs-lookup"><span data-stu-id="8cdd6-286">REST</span></span>
<span data-ttu-id="8cdd6-287">Você pode obter a integridade da réplica com uma [solicitação GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) ou uma [solicitação POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy), que inclui as políticas de integridade descritas no corpo.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-287">You can get replica health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-deployed-application-health"></a><span data-ttu-id="8cdd6-288">Obter integridade do aplicativo implantado</span><span class="sxs-lookup"><span data-stu-id="8cdd6-288">Get deployed application health</span></span>
<span data-ttu-id="8cdd6-289">Retorna a integridade de um aplicativo implantado em uma entidade de nó.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-289">Returns the health of an application deployed on a node entity.</span></span> <span data-ttu-id="8cdd6-290">Além disso, contém os estados de integridade do pacote de serviço implantado.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-290">It contains the deployed service package health states.</span></span> <span data-ttu-id="8cdd6-291">Entrada:</span><span class="sxs-lookup"><span data-stu-id="8cdd6-291">Input:</span></span>

* <span data-ttu-id="8cdd6-292">[Obrigatório] O nome do aplicativo (URI) e o nome do nó (cadeia de caracteres) que identificam o aplicativo implantado</span><span class="sxs-lookup"><span data-stu-id="8cdd6-292">[Required] The application name (URI) and node name (string) that identify the deployed application.</span></span>
* <span data-ttu-id="8cdd6-293">[Opcional] A política de integridade do aplicativo usada para substituir as políticas do manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-293">[Optional] The application health policy used to override the application manifest policies.</span></span>
* <span data-ttu-id="8cdd6-294">[Opcional] Filtros de eventos e pacotes de serviço implantados que especificam quais entradas são interessantes e devem retornar nos resultados (por exemplo, apenas erros ou avisos e erros).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-294">[Optional] Filters for events and deployed service packages that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="8cdd6-295">Todos os eventos e pacotes de serviço implantados são usados para avaliar a integridade agregada da entidade, independentemente do filtro.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-295">All events and deployed service packages are used to evaluate the entity aggregated health, regardless of the filter.</span></span>
* <span data-ttu-id="8cdd6-296">[Opcional] Filtrar para excluir as estatísticas de integridade.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-296">[Optional] Filter to exclude health statistics.</span></span> <span data-ttu-id="8cdd6-297">Se não for especificado, as estatísticas de integridade mostram a quantidade de pacotes de serviço implantados nos estados de integridade OK, aviso e erro.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-297">If not specified, the health statistics show the number of deployed service packages in ok, warning, and error health states.</span></span>

### <a name="api"></a><span data-ttu-id="8cdd6-298">API</span><span class="sxs-lookup"><span data-stu-id="8cdd6-298">API</span></span>
<span data-ttu-id="8cdd6-299">Para obter a integridade de um aplicativo implantado em um nó por meio de API, crie um `FabricClient` e chame o método [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) em seu HealthManager.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-299">To get the health of an application deployed on a node through the API, create a `FabricClient` and call the [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="8cdd6-300">Para especificar parâmetros opcionais, use [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-300">To specify optional parameters, use [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span></span>

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a><span data-ttu-id="8cdd6-301">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8cdd6-301">PowerShell</span></span>
<span data-ttu-id="8cdd6-302">O cmdlet para obter a integridade do aplicativo implantado é [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-302">The cmdlet to get the deployed application health is [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="8cdd6-303">Primeiro, conecte-se ao cluster usando o cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="8cdd6-303">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="8cdd6-304">Para descobrir onde um aplicativo está implantado, execute [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) e observe os filhos do aplicativo implantado.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-304">To find out where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at the deployed application children.</span></span>

<span data-ttu-id="8cdd6-305">O cmdlet a seguir obtém a integridade do aplicativo **fabric:/WordCount** implantado em **_Node_2**.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-305">The following cmdlet gets the health of the **fabric:/WordCount** application deployed on **_Node_2**.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplicationHealth -ApplicationName fabric:/WordCount -NodeName _Node_0


ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_0
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
                                     ServiceManifestName   : WordCountWebServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131444422261848308
                                     SentAt                : 7/13/2017 5:57:06 PM
                                     ReceivedAt            : 7/13/2017 5:57:17 PM
                                     TTL                   : Infinite
                                     Description           : The application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/13/2017 5:57:17 PM, LastWarning = 1/1/0001 12:00:00 AM
                                     
HealthStatistics                   : 
                                     DeployedServicePackage : 2 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="8cdd6-306">REST</span><span class="sxs-lookup"><span data-stu-id="8cdd6-306">REST</span></span>
<span data-ttu-id="8cdd6-307">Você pode obter a integridade do aplicativo implantado com uma [solicitação GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) ou uma [solicitação POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy), que inclui as políticas de integridade descritas no corpo.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-307">You can get deployed application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="get-deployed-service-package-health"></a><span data-ttu-id="8cdd6-308">Obter integridade do pacote de serviço implantado</span><span class="sxs-lookup"><span data-stu-id="8cdd6-308">Get deployed service package health</span></span>
<span data-ttu-id="8cdd6-309">Retorna a integridade de uma entidade de pacote de serviço implantada.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-309">Returns the health of a deployed service package entity.</span></span> <span data-ttu-id="8cdd6-310">Entrada:</span><span class="sxs-lookup"><span data-stu-id="8cdd6-310">Input:</span></span>

* <span data-ttu-id="8cdd6-311">[Obrigatório] O nome do aplicativo (URI), nome do nó (cadeia de caracteres) e nome do manifesto do serviço (cadeia de caracteres) que identificam o pacote de serviço implantado</span><span class="sxs-lookup"><span data-stu-id="8cdd6-311">[Required] The application name (URI), node name (string), and service manifest name (string) that identify the deployed service package.</span></span>
* <span data-ttu-id="8cdd6-312">[Opcional] A política de integridade do aplicativo usada para substituir a política do manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-312">[Optional] The application health policy used to override the application manifest policy.</span></span>
* <span data-ttu-id="8cdd6-313">[Opcional] Filtros de eventos que especificam quais entradas são interessantes e devem retornar nos resultados (por exemplo, apenas erros ou avisos e erros).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-313">[Optional] Filters for events that specify which entries are of interest and should be returned in the result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="8cdd6-314">Todos os eventos são usados para avaliar a integridade agregada da entidade, independentemente do filtro.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-314">All events are used to evaluate the entity aggregated health, regardless of the filter.</span></span>

### <a name="api"></a><span data-ttu-id="8cdd6-315">API</span><span class="sxs-lookup"><span data-stu-id="8cdd6-315">API</span></span>
<span data-ttu-id="8cdd6-316">Para obter a integridade de um pacote de serviço implantado por meio de API, crie um `FabricClient` e chame o método [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) em seu HealthManager.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-316">To get the health of a deployed service package through the API, create a `FabricClient` and call the [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) method on its HealthManager.</span></span> <span data-ttu-id="8cdd6-317">Para especificar parâmetros opcionais, use [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-317">To specify optional parameters, use [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span></span>

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a><span data-ttu-id="8cdd6-318">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8cdd6-318">PowerShell</span></span>
<span data-ttu-id="8cdd6-319">O cmdlet para obter a integridade do pacote de serviço implantado é [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-319">The cmdlet to get the deployed service package health is [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span></span> <span data-ttu-id="8cdd6-320">Primeiro, conecte-se ao cluster usando o cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="8cdd6-320">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="8cdd6-321">Para descobrir onde um aplicativo está implantado, execute [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) e observe os aplicativos implantados.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-321">To see where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at the deployed applications.</span></span> <span data-ttu-id="8cdd6-322">Para ver quais pacotes de serviço estão em um aplicativo, observe os filhos do pacote de serviço implantado na saída de [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="8cdd6-322">To see which service packages are in an application, look at the deployed service package children in the [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) output.</span></span>

<span data-ttu-id="8cdd6-323">O cmdlet a seguir obtém a integridade do pacote de serviço **WordCountServicePkg** do aplicativo **fabric:/WordCount** implantado em **_Node_2**.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-323">The following cmdlet gets the health of the **WordCountServicePkg** service package of the **fabric:/WordCount** application deployed on **_Node_2**.</span></span> <span data-ttu-id="8cdd6-324">A entidade tem relatórios **System.Hosting** para ativação bem-sucedida do pacote de serviço e do ponto de entrada e registro bem-sucedido do tipo de serviço.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-324">The entity has **System.Hosting** reports for successful service-package and entry-point activation, and successful service-type registration.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplication -ApplicationName fabric:/WordCount -NodeName _Node_2 | Get-ServiceFabricDeployedServicePackageHealth -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_2
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131444422267693359
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : The ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131444422267903345
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : The CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131444422272458374
                             SentAt                : 7/13/2017 5:57:07 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : The ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="8cdd6-325">REST</span><span class="sxs-lookup"><span data-stu-id="8cdd6-325">REST</span></span>
<span data-ttu-id="8cdd6-326">Você pode obter a integridade do pacote de serviço implantado com uma [solicitação GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) ou uma [solicitação POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy), que inclui as políticas de integridade descritas no corpo.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-326">You can get deployed service package health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) that includes health policies described in the body.</span></span>

## <a name="health-chunk-queries"></a><span data-ttu-id="8cdd6-327">Consultas de integridade em blocos</span><span class="sxs-lookup"><span data-stu-id="8cdd6-327">Health chunk queries</span></span>
<span data-ttu-id="8cdd6-328">As consultas de integridade em bloco podem retornar os filhos de cluster em vários níveis (recursivamente), de acordo com os filtros de entrada.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-328">The health chunk queries can return multi-level cluster children (recursively), per input filters.</span></span> <span data-ttu-id="8cdd6-329">Elas dão suporte a filtros avançados que permitem uma grande flexibilidade na escolha dos filhos a serem retornados.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-329">It supports advanced filters that allow a lot of flexibility in choosing the children to be returned.</span></span> <span data-ttu-id="8cdd6-330">Os filtros podem especificar filhos pelo identificador exclusivo ou por outros identificadores de grupo e/ou os estados de integridade.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-330">The filters can specify children by the unique identifier or by other group identifiers and/or health states.</span></span> <span data-ttu-id="8cdd6-331">Por padrão, nenhum filho é incluído, ao contrário dos comandos de integridade que incluem sempre o filho de primeiro nível.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-331">By default, no children are included, as opposed to health commands that always include first-level children.</span></span>

<span data-ttu-id="8cdd6-332">As [consultas de integridade](service-fabric-view-entities-aggregated-health.md#health-queries) retornam apenas os filhos de primeiro nível da entidade especificada, de acordo com os filtros necessários.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-332">The [health queries](service-fabric-view-entities-aggregated-health.md#health-queries) return only first-level children of the specified entity per required filters.</span></span> <span data-ttu-id="8cdd6-333">Para obter os filhos dos filhos, você deve chamar outras APIs de integridade para cada entidade de interesse.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-333">To get the children of the children, you must call additional health APIs for each entity of interest.</span></span> <span data-ttu-id="8cdd6-334">Da mesma forma, para obter a integridade de entidades específicas, você deve chamar uma API e integridade para cada entidade desejada.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-334">Similarly, to get the health of specific entities, you must call one health API for each desired entity.</span></span> <span data-ttu-id="8cdd6-335">A filtragem avançada da consulta em bloco permite a você solicitar vários itens de interesse em uma consulta, reduzindo o tamanho da mensagem e o número de mensagens.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-335">The chunk query advanced filtering allows you to request multiple items of interest in one query, minimizing the message size and the number of messages.</span></span>

<span data-ttu-id="8cdd6-336">O valor da consulta em blocos é que você pode obter o estado da integridade para mais entidades de cluster (potencialmente todas as entidades de cluster começando na raiz exigida) em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-336">The value of the chunk query is that you can get health state for more cluster entities (potentially all cluster entities starting at required root) in one call.</span></span> <span data-ttu-id="8cdd6-337">Você pode expressar uma consulta de integridade complexa da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="8cdd6-337">You can express complex health query such as:</span></span>

* <span data-ttu-id="8cdd6-338">Retorne apenas os aplicativos com erro e, para esses aplicativos, inclua todos os serviços em aviso|erro.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-338">Return only applications in error, and for those applications include all services in warning or error.</span></span> <span data-ttu-id="8cdd6-339">Para os serviços retornados, inclua todas as partições.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-339">For returned services, include all partitions.</span></span>
* <span data-ttu-id="8cdd6-340">Retorne apenas a integridade dos quatro aplicativos, especificados por seus nomes.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-340">Return only the health of four applications, specified by their names.</span></span>
* <span data-ttu-id="8cdd6-341">Retorne apenas a integridade dos aplicativos de um tipo de aplicativo desejado.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-341">Return only the health of applications of a desired application type.</span></span>
* <span data-ttu-id="8cdd6-342">Retorne todas as entidades implantadas em um nó.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-342">Return all deployed entities on a node.</span></span> <span data-ttu-id="8cdd6-343">Retorna todos os aplicativos, todos os aplicativos implantados no nó especificado e todos os pacotes de serviço implantados nesse nó.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-343">Returns all applications, all deployed applications on the specified node and all the deployed service packages on that node.</span></span>
* <span data-ttu-id="8cdd6-344">Retorna todas as réplicas com erro.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-344">Return all replicas in error.</span></span> <span data-ttu-id="8cdd6-345">Retorna todos os aplicativos, serviços, partições e somente réplicas com erro.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-345">Returns all applications, services, partitions, and only replicas in error.</span></span>
* <span data-ttu-id="8cdd6-346">Retorna todos os aplicativos.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-346">Return all applications.</span></span> <span data-ttu-id="8cdd6-347">Para um serviço específico, inclua todas as partições.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-347">For a specified service, include all partitions.</span></span>

<span data-ttu-id="8cdd6-348">Atualmente, a consulta de integridade em blocos é exposta somente para a entidade do cluster.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-348">Currently, the health chunk query is exposed only for the cluster entity.</span></span> <span data-ttu-id="8cdd6-349">Ela retorna uma parte da integridade do cluster, que contém:</span><span class="sxs-lookup"><span data-stu-id="8cdd6-349">It returns a cluster health chunk, which contains:</span></span>

* <span data-ttu-id="8cdd6-350">O estado de integridade agregado do cluster.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-350">The cluster aggregated health state.</span></span>
* <span data-ttu-id="8cdd6-351">A lista de nós da parte de estado de integridade que respeita os filtros de entrada.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-351">The health state chunk list of nodes that respect input filters.</span></span>
* <span data-ttu-id="8cdd6-352">A lista de aplicativos da parte de estado de integridade que respeita os filtros de entrada.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-352">The health state chunk list of applications that respect input filters.</span></span> <span data-ttu-id="8cdd6-353">Cada parte do estado de integridade do aplicativo contém uma lista com todos os serviços que respeitam os filtros de entrada e uma lista com todos os aplicativos implantados que respeitam os filtros.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-353">Each application health state chunk contains a chunk list with all services that respect input filters and a chunk list with all deployed applications that respect the filters.</span></span> <span data-ttu-id="8cdd6-354">O mesmo vale para os filhos dos serviços e aplicativos implantados.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-354">Same for the children of services and deployed applications.</span></span> <span data-ttu-id="8cdd6-355">Dessa forma, todas as entidades no cluster podem retornar caso solicitado, de uma maneira hierárquica.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-355">This way, all entities in the cluster can be potentially returned if requested, in a hierarchical fashion.</span></span>

### <a name="cluster-health-chunk-query"></a><span data-ttu-id="8cdd6-356">Consulta em bloco sobre a integridade do cluster</span><span class="sxs-lookup"><span data-stu-id="8cdd6-356">Cluster health chunk query</span></span>
<span data-ttu-id="8cdd6-357">Retorna a integridade da entidade do cluster e contém as partes hierárquicas do estado de integridade dos filhos necessários.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-357">Returns the health of the cluster entity and contains the hierarchical health state chunks of required children.</span></span> <span data-ttu-id="8cdd6-358">Entrada:</span><span class="sxs-lookup"><span data-stu-id="8cdd6-358">Input:</span></span>

* <span data-ttu-id="8cdd6-359">[Opcional] A política de integridade do cluster usada para avaliar os nós e os eventos de cluster.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-359">[Optional] The cluster health policy used to evaluate the nodes and the cluster events.</span></span>
* <span data-ttu-id="8cdd6-360">[Opcional] Mapa da política de integridade do aplicativo, com políticas de integridade usadas para substituir as políticas do manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-360">[Optional] The application health policy map, with the health policies used to override the application manifest policies.</span></span>
* <span data-ttu-id="8cdd6-361">[Opcional] Filtros de eventos, nós e aplicativos que especificam quais entradas são interessantes e devem retornar no resultado.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-361">[Optional] Filters for nodes and applications that specify which entries are of interest and should be returned in the result.</span></span> <span data-ttu-id="8cdd6-362">Os filtros são específicos a uma entidade/grupo de entidades ou são aplicáveis a todas as entidades nesse nível.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-362">The filters are specific to an entity/group of entities or are applicable to all entities at that level.</span></span> <span data-ttu-id="8cdd6-363">A lista de filtros pode conter um filtro geral e/ou filtros para identificadores específicos, a fim de refinar as entidades retornadas pela consulta.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-363">The list of filters can contain one general filter and/or filters for specific identifiers to fine-grain entities returned by the query.</span></span> <span data-ttu-id="8cdd6-364">Se estiver vazia, os filhos não retornarão por padrão.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-364">If empty, the children are not returned by default.</span></span>
  <span data-ttu-id="8cdd6-365">Leia mais sobre os filtros em [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) e [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-365">Read more about the filters at [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) and [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span></span> <span data-ttu-id="8cdd6-366">O filtros de aplicativo pode especificar de forma recursiva os filtros avançados para os filhos.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-366">The application filters can recursively specify advanced filters for children.</span></span>

<span data-ttu-id="8cdd6-367">O resultado da parte inclui os filhos que respeitam os filtros.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-367">The chunk result includes the children that respect the filters.</span></span>

<span data-ttu-id="8cdd6-368">Atualmente, a consulta em bloco não retorna avaliações não íntegras ou eventos de entidade.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-368">Currently, the chunk query does not return unhealthy evaluations or entity events.</span></span> <span data-ttu-id="8cdd6-369">Essas informações extras podem ser obtidas com a consulta de integridade de cluster existente.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-369">That extra information can be obtained using the existing cluster health query.</span></span>

### <a name="api"></a><span data-ttu-id="8cdd6-370">API</span><span class="sxs-lookup"><span data-stu-id="8cdd6-370">API</span></span>
<span data-ttu-id="8cdd6-371">Para obter a parte da integridade do cluster, crie um `FabricClient` e chame o método [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) em seu **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-371">To get cluster health chunk, create a `FabricClient` and call the [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) method on its **HealthManager**.</span></span> <span data-ttu-id="8cdd6-372">Você pode passar [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) para descrever as políticas de integridade e os filtros avançados.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-372">You can pass in [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) to describe health policies and advanced filters.</span></span>

<span data-ttu-id="8cdd6-373">O código a seguir obtém parte da integridade do cluster com filtros avançados.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-373">The following code gets cluster health chunk with advanced filters.</span></span>

```csharp
var queryDescription = new ClusterHealthChunkQueryDescription();
queryDescription.ApplicationFilters.Add(new ApplicationHealthStateFilter()
    {
        // Return applications only if they are in error
        HealthStateFilter = HealthStateFilter.Error
    });

// Return all replicas
var wordCountServiceReplicaFilter = new ReplicaHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };

// Return all replicas and all partitions
var wordCountServicePartitionFilter = new PartitionHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };
wordCountServicePartitionFilter.ReplicaFilters.Add(wordCountServiceReplicaFilter);

// For specific service, return all partitions and all replicas
var wordCountServiceFilter = new ServiceHealthStateFilter()
{
    ServiceNameFilter = new Uri("fabric:/WordCount/WordCountService"),
};
wordCountServiceFilter.PartitionFilters.Add(wordCountServicePartitionFilter);

// Application filter: for specific application, return no services except the ones of interest
var wordCountApplicationFilter = new ApplicationHealthStateFilter()
    {
        // Always return fabric:/WordCount application
        ApplicationNameFilter = new Uri("fabric:/WordCount"),
    };
wordCountApplicationFilter.ServiceFilters.Add(wordCountServiceFilter);

queryDescription.ApplicationFilters.Add(wordCountApplicationFilter);

var result = await fabricClient.HealthManager.GetClusterHealthChunkAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="8cdd6-374">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8cdd6-374">PowerShell</span></span>
<span data-ttu-id="8cdd6-375">O cmdlet para obter a integridade do cluster é [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-375">The cmdlet to get the cluster health is [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span></span> <span data-ttu-id="8cdd6-376">Primeiro, conecte-se ao cluster usando o cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="8cdd6-376">First, connect to the cluster by using the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="8cdd6-377">O código a seguir obterá nós apenas se eles apresentarem Erro, exceto para um nó específico, que sempre deverá ser retornado.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-377">The following code gets nodes only if they are in Error except for a specific node, which should always be returned.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$nodeFilter1 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{HealthStateFilter=$errorFilter}
$nodeFilter2 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{NodeNameFilter="_Node_1";HealthStateFilter=$allFilter}
# Create node filter list that will be passed in the cmdlet
$nodeFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.NodeHealthStateFilter]
$nodeFilters.Add($nodeFilter1)
$nodeFilters.Add($nodeFilter2)

Get-ServiceFabricClusterHealthChunk -NodeFilters $nodeFilters


HealthState                  : Warning
NodeHealthStateChunks        : 
                               TotalCount            : 1
                               
                               NodeName              : _Node_1
                               HealthState           : Ok
                               
ApplicationHealthStateChunks : None
```

<span data-ttu-id="8cdd6-378">O cmdlet a seguir obtém parte do cluster com os filtros de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-378">The following cmdlet gets cluster chunk with application filters.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

# All replicas
$replicaFilter = New-Object System.Fabric.Health.ReplicaHealthStateFilter -Property @{HealthStateFilter=$allFilter}

# All partitions
$partitionFilter = New-Object System.Fabric.Health.PartitionHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$partitionFilter.ReplicaFilters.Add($replicaFilter)

# For WordCountService, return all partitions and all replicas
$svcFilter1 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{ServiceNameFilter="fabric:/WordCount/WordCountService"}
$svcFilter1.PartitionFilters.Add($partitionFilter)

$svcFilter2 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{HealthStateFilter=$errorFilter}

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{ApplicationNameFilter="fabric:/WordCount"}
$appFilter.ServiceFilters.Add($svcFilter1)
$appFilter.ServiceFilters.Add($svcFilter2)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)

Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 1
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               ServiceHealthStateChunks : 
                                TotalCount            : 1
                               
                                ServiceName           : fabric:/WordCount/WordCountService
                                HealthState           : Error
                                PartitionHealthStateChunks : 
                                    TotalCount            : 1
                               
                                    PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                                    HealthState           : Error
                                    ReplicaHealthStateChunks : 
                                        TotalCount            : 5
                               
                                        ReplicaOrInstanceId   : 131444422293118720
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293118721
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113678
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113679
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422260002646
                                        HealthState           : Error
```

<span data-ttu-id="8cdd6-379">O cmdlet a seguir retorna todas as entidades implantadas em um nó.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-379">The following cmdlet returns all deployed entities on a node.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$dspFilter = New-Object System.Fabric.Health.DeployedServicePackageHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$daFilter =  New-Object System.Fabric.Health.DeployedApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter;NodeNameFilter="_Node_2"}
$daFilter.DeployedServicePackageFilters.Add($dspFilter)

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$appFilter.DeployedApplicationFilters.Add($daFilter)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)
Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 2
                               
                               ApplicationName       : fabric:/System
                               HealthState           : Ok
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : FAS
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
                               
                               
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : WordCountServicePkg
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
```

### <a name="rest"></a><span data-ttu-id="8cdd6-380">REST</span><span class="sxs-lookup"><span data-stu-id="8cdd6-380">REST</span></span>
<span data-ttu-id="8cdd6-381">Você pode obter parte da integridade do cluster com uma [solicitação GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) ou uma [solicitação POST](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster), que inclui os filtros avançados e políticas de integridade descritos no corpo.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-381">You can get cluster health chunk with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) that includes health policies and advanced filters described in the body.</span></span>

## <a name="general-queries"></a><span data-ttu-id="8cdd6-382">Consultas gerais</span><span class="sxs-lookup"><span data-stu-id="8cdd6-382">General queries</span></span>
<span data-ttu-id="8cdd6-383">As consultas gerais retornam a lista de entidades do Service Fabric de um tipo especificado.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-383">General queries return a list of Service Fabric entities of a specified type.</span></span> <span data-ttu-id="8cdd6-384">Elas são expostas por meio da API (métodos em **FabricClient.QueryManager**), dos cmdlets do PowerShell e da REST.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-384">They are exposed through the API (via the methods on **FabricClient.QueryManager**), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="8cdd6-385">Essas consultas agregam subconsultas de vários componentes.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-385">These queries aggregate subqueries from multiple components.</span></span> <span data-ttu-id="8cdd6-386">Um deles é o [Repositório de Integridade](service-fabric-health-introduction.md#health-store), que preenche o estado de integridade agregada para cada resultado da consulta.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-386">One of them is the [health store](service-fabric-health-introduction.md#health-store), which populates the aggregated health state for each query result.</span></span>  

> [!NOTE]
> <span data-ttu-id="8cdd6-387">As consultas gerais retornam o estado da integridade da entidade agregada e não contêm dados de integridade avançados.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-387">General queries return the aggregated health state of the entity and do not contain rich health data.</span></span> <span data-ttu-id="8cdd6-388">Se uma entidade não estiver íntegra, você poderá acompanhá-la com consultas de integridade a fim de obter todas as informações de integridade, incluindo eventos, estados da integridade dos filhos e avaliações não íntegras.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-388">If an entity is not healthy, you can follow up with health queries to get all its health information, including events, child health states, and unhealthy evaluations.</span></span>
>
>

<span data-ttu-id="8cdd6-389">Se as consultas gerais retornarem um estado de integridade desconhecido para uma entidade, talvez o repositório de integridade não tenha dados completos sobre a entidade.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-389">If general queries return an unknown health state for an entity, it's possible that the health store doesn't have complete data about the entity.</span></span> <span data-ttu-id="8cdd6-390">Também é possível que uma subconsulta ao repositório de integridade não tenha êxito (por exemplo, ocorreu um erro de comunicação ou repositório de integridade apresentava alguma restrição).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-390">It's also possible that a subquery to the health store wasn't successful (for example, there was a communication error, or the health store was throttled).</span></span> <span data-ttu-id="8cdd6-391">Acompanhe uma consulta de integridade da entidade.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-391">Follow up with a health query for the entity.</span></span> <span data-ttu-id="8cdd6-392">Se a subconsulta tiver encontrado erros transitórios, como problemas de rede, essa consulta de acompanhamento poderá ser bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-392">If the subquery encountered transient errors, such as network issues, this follow-up query may succeed.</span></span> <span data-ttu-id="8cdd6-393">Ela também pode fornecer mais detalhes, com base no repositório de integridade, sobre o motivo de a entidade não ser exposta.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-393">It may also give you more details from the health store about why the entity is not exposed.</span></span>

<span data-ttu-id="8cdd6-394">As consultas que contêm **HealthState** para entidades são:</span><span class="sxs-lookup"><span data-stu-id="8cdd6-394">The queries that contain **HealthState** for entities are:</span></span>

* <span data-ttu-id="8cdd6-395">Lista de nós: retorna os nós da lista no cluster (paginados).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-395">Node list: Returns the list nodes in the cluster (paged).</span></span>
  * <span data-ttu-id="8cdd6-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span><span class="sxs-lookup"><span data-stu-id="8cdd6-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span></span>
  * <span data-ttu-id="8cdd6-397">PowerShell: Get-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="8cdd6-397">PowerShell: Get-ServiceFabricNode</span></span>
* <span data-ttu-id="8cdd6-398">Lista de aplicativos: retorna a lista de aplicativos no cluster (paginados).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-398">Application list: Returns the list of applications in the cluster (paged).</span></span>
  * <span data-ttu-id="8cdd6-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="8cdd6-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span></span>
  * <span data-ttu-id="8cdd6-400">PowerShell: Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="8cdd6-400">PowerShell: Get-ServiceFabricApplication</span></span>
* <span data-ttu-id="8cdd6-401">Lista de serviços: retorna a lista de serviços em um aplicativo (paginados).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-401">Service list: Returns the list of services in an application (paged).</span></span>
  * <span data-ttu-id="8cdd6-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span><span class="sxs-lookup"><span data-stu-id="8cdd6-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span></span>
  * <span data-ttu-id="8cdd6-403">PowerShell: Get-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="8cdd6-403">PowerShell: Get-ServiceFabricService</span></span>
* <span data-ttu-id="8cdd6-404">Lista de partições: retorna a lista de partições em um serviço (paginadas).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-404">Partition list: Returns the list of partitions in a service (paged).</span></span>
  * <span data-ttu-id="8cdd6-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span><span class="sxs-lookup"><span data-stu-id="8cdd6-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span></span>
  * <span data-ttu-id="8cdd6-406">PowerShell: Get-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="8cdd6-406">PowerShell: Get-ServiceFabricPartition</span></span>
* <span data-ttu-id="8cdd6-407">Lista de réplicas: retorna a lista de réplicas em uma partição (paginadas).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-407">Replica list: Returns the list of replicas in a partition (paged).</span></span>
  * <span data-ttu-id="8cdd6-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span><span class="sxs-lookup"><span data-stu-id="8cdd6-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span></span>
  * <span data-ttu-id="8cdd6-409">PowerShell: Get-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="8cdd6-409">PowerShell: Get-ServiceFabricReplica</span></span>
* <span data-ttu-id="8cdd6-410">Lista de aplicativos implantados: retorna a lista de aplicativos implantados em um nó.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-410">Deployed application list: Returns the list of deployed applications on a node.</span></span>
  * <span data-ttu-id="8cdd6-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="8cdd6-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span></span>
  * <span data-ttu-id="8cdd6-412">PowerShell: Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="8cdd6-412">PowerShell: Get-ServiceFabricDeployedApplication</span></span>
* <span data-ttu-id="8cdd6-413">Lista de pacotes de serviço implantados: retorna a lista de pacotes de serviço em um aplicativo implantado.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-413">Deployed service package list: Returns the list of service packages in a deployed application.</span></span>
  * <span data-ttu-id="8cdd6-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span><span class="sxs-lookup"><span data-stu-id="8cdd6-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span></span>
  * <span data-ttu-id="8cdd6-415">PowerShell: Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="8cdd6-415">PowerShell: Get-ServiceFabricDeployedApplication</span></span>

> [!NOTE]
> <span data-ttu-id="8cdd6-416">Algumas das consultas retornam resultados paginados.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-416">Some of the queries return paged results.</span></span> <span data-ttu-id="8cdd6-417">O retorno dessas consultas é uma lista derivada de [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-417">The return of these queries is a list derived from [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span></span> <span data-ttu-id="8cdd6-418">Se os resultados não couberem em uma mensagem, serão retornados apenas uma página e um ContinuationToken que acompanha onde a enumeração parou.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-418">If the results do not fit a message, only a page is returned and a ContinuationToken that tracks where enumeration stopped.</span></span> <span data-ttu-id="8cdd6-419">Continue a chamar a mesma consulta e a passar o token de continuação da consulta anterior a fim de obter os próximos resultados.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-419">Continue to call the same query and pass in the continuation token from the previous query to get next results.</span></span>
>
>

### <a name="examples"></a><span data-ttu-id="8cdd6-420">Exemplos</span><span class="sxs-lookup"><span data-stu-id="8cdd6-420">Examples</span></span>
<span data-ttu-id="8cdd6-421">O código a seguir obtém os aplicativos não íntegros no cluster:</span><span class="sxs-lookup"><span data-stu-id="8cdd6-421">The following code gets the unhealthy applications in the cluster:</span></span>

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

<span data-ttu-id="8cdd6-422">O cmdlet a seguir obtém detalhes de aplicativo para o aplicativo fabric:/WordCount.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-422">The following cmdlet gets the application details for the fabric:/WordCount application.</span></span> <span data-ttu-id="8cdd6-423">Observe que o estado de integridade é de aviso.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-423">Notice that health state is at warning.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplication -ApplicationName fabric:/WordCount

ApplicationName        : fabric:/WordCount
ApplicationTypeName    : WordCount
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Warning
ApplicationParameters  : { "WordCountWebService_InstanceCount" = "1";
                         "_WFDebugParams_" = "[{"ServiceManifestName":"WordCountWebServicePkg","CodePackageName":"Code","EntryPointType":"Main","Debug
                         ExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {74f7e5d5-71a9-47e2-a8cd-1878ec4734f1} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"},{"ServiceManifestName":"WordCountServicePkg","CodeP
                         ackageName":"Code","EntryPointType":"Main","DebugExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {2ab462e6-e0d1-4fda-a844-972f561fe751} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"}]" }
```

<span data-ttu-id="8cdd6-424">O cmdlet abaixo obtém os serviços com o estado de integridade de erro:</span><span class="sxs-lookup"><span data-stu-id="8cdd6-424">The following cmdlet gets the services with a health state of error:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplication | Get-ServiceFabricService | where {$_.HealthState -eq "Error"}


ServiceName            : fabric:/WordCount/WordCountService
ServiceKind            : Stateful
ServiceTypeName        : WordCountServiceType
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
HasPersistedState      : True
ServiceStatus          : Active
HealthState            : Error
```

## <a name="cluster-and-application-upgrades"></a><span data-ttu-id="8cdd6-425">Atualização de cluster e aplicativo</span><span class="sxs-lookup"><span data-stu-id="8cdd6-425">Cluster and application upgrades</span></span>
<span data-ttu-id="8cdd6-426">Durante a atualização monitorada do cluster e do aplicativo, o Service Fabric verifica a integridade para garantir que tudo esteja íntegro e permaneça assim.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-426">During a monitored upgrade of the cluster and application, Service Fabric checks health to ensure that everything remains healthy.</span></span> <span data-ttu-id="8cdd6-427">Se uma entidade não estiver íntegra, conforme avaliação por meio de políticas de integridade, a atualização aplica políticas específicas à atualização para determinar a próxima ação.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-427">If an entity is unhealthy as evaluated by using configured health policies, the upgrade applies upgrade-specific policies to determine the next action.</span></span> <span data-ttu-id="8cdd6-428">A atualização pode ser pausada para permitir a interação do usuário (por exemplo, corrigir condições de erro ou alterar políticas), ou pode ser revertida automaticamente para a versão anterior em boa qualidade.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-428">The upgrade may be paused to allow user interaction (such as fixing error conditions or changing policies), or it may automatically roll back to the previous good version.</span></span>

<span data-ttu-id="8cdd6-429">Durante uma atualização de *cluster* , você pode obter o status de atualização do cluster.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-429">During a *cluster* upgrade, you can get the cluster upgrade status.</span></span> <span data-ttu-id="8cdd6-430">O status de atualização inclui quaisquer avaliações não íntegras, que apontam para o que não está íntegro no cluster.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-430">The upgrade status includes unhealthy evaluations, which point to what is unhealthy in the cluster.</span></span> <span data-ttu-id="8cdd6-431">Se a atualização for revertida devido a problemas de integridade, o status da atualização se lembrará dos últimos motivos não íntegros.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-431">If the upgrade is rolled back due to health issues, the upgrade status remembers the last unhealthy reasons.</span></span> <span data-ttu-id="8cdd6-432">Essas informações podem ajudar os administradores a investigar o que deu errado após a atualização ser revertida ou interrompida.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-432">This information can help administrators investigate what went wrong after the upgrade rolled back or stopped.</span></span>

<span data-ttu-id="8cdd6-433">Da mesma forma, durante uma atualização do *aplicativo* , quaisquer avaliações não íntegras ficam contidas no status de atualização do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-433">Similarly, during an *application* upgrade, any unhealthy evaluations are contained in the application upgrade status.</span></span>

<span data-ttu-id="8cdd6-434">O exemplo a seguir mostra o status da atualização do aplicativo para um aplicativo fabric:/WordCount modificado.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-434">The following shows the application upgrade status for a modified fabric:/WordCount application.</span></span> <span data-ttu-id="8cdd6-435">Um watchdog relatou um erro em uma de suas réplicas.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-435">A watchdog reported an error on one of its replicas.</span></span> <span data-ttu-id="8cdd6-436">A atualização está sendo revertida porque as verificações de integridade não são respeitadas.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-436">The upgrade is rolling back because the health checks are not respected.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationUpgrade fabric:/WordCount

ApplicationName               : fabric:/WordCount
ApplicationTypeName           : WordCount
TargetApplicationTypeVersion  : 1.0.0.0
ApplicationParameters         : {}
StartTimestampUtc             : 4/21/2017 5:23:26 PM
FailureTimestampUtc           : 4/21/2017 5:23:37 PM
FailureReason                 : HealthCheck
UpgradeState                  : RollingBackInProgress
UpgradeDuration               : 00:00:23
CurrentUpgradeDomainDuration  : 00:00:00
CurrentUpgradeDomainProgress  : UD1

                                NodeName            : _Node_1
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_2
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_3
                                UpgradePhase        : PreUpgradeSafetyCheck
                                PendingSafetyChecks :
                                EnsurePartitionQuorum - PartitionId: 30db5be6-4e20-4698-8185-4bd7ca744020
NextUpgradeDomain             : UD2
UpgradeDomainsStatus          : { "UD1" = "Completed";
                                "UD2" = "Pending";
                                "UD3" = "Pending";
                                "UD4" = "Pending" }
UnhealthyEvaluations          :
                                Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.

                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.

                                      Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                      Unhealthy partition: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b', AggregatedHealthState='Error'.

                                          Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.

                                          Unhealthy replica: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b',
                                  ReplicaOrInstanceId='131031502346844058', AggregatedHealthState='Error'.

                                              Error event: SourceId='DiskWatcher', Property='Disk'.

UpgradeKind                   : Rolling
RollingUpgradeMode            : UnmonitoredAuto
ForceRestart                  : False
UpgradeReplicaSetCheckTimeout : 00:15:00
```

<span data-ttu-id="8cdd6-437">Leia mais sobre a [Atualização de aplicativo do Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="8cdd6-437">Read more about the [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="use-health-evaluations-to-troubleshoot"></a><span data-ttu-id="8cdd6-438">Usar avaliações de integridade para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="8cdd6-438">Use health evaluations to troubleshoot</span></span>
<span data-ttu-id="8cdd6-439">Sempre que houver um problema no cluster ou aplicativo, observe a integridade do cluster ou do aplicativo para identificar o que está errado.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-439">Whenever there is an issue with the cluster or an application, look at the cluster or application health to pinpoint what is wrong.</span></span> <span data-ttu-id="8cdd6-440">As avaliações não íntegras mostram detalhes sobre o que disparou o estado não íntegro atual.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-440">The unhealthy evaluations provide details about what triggered the current unhealthy state.</span></span> <span data-ttu-id="8cdd6-441">Se for necessário, você poderá analisar entidades filho não íntegras para identificar a causa raiz.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-441">If you need to, you can drill down into unhealthy child entities to identify the root cause.</span></span>

<span data-ttu-id="8cdd6-442">Por exemplo, pense em um aplicativo não íntegro porque há um relatório de erros em uma de suas réplicas.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-442">For example, consider an application unhealthy because there is an error report on one of its replicas.</span></span> <span data-ttu-id="8cdd6-443">O seguinte cmdlet do Powershell mostra as avaliações não íntegras:</span><span class="sxs-lookup"><span data-stu-id="8cdd6-443">The following Powershell cmdlet shows the unhealthy evaluations:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount -EventsFilter None -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.
                                  
                                        Unhealthy replica: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', ReplicaOrInstanceId='131444422260002646', AggregatedHealthState='Error'.
                                  
                                            Error event: SourceId='MyWatchdog', Property='Memory'.
                                  
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

<span data-ttu-id="8cdd6-444">Você pode examinar a réplica para saber mais:</span><span class="sxs-lookup"><span data-stu-id="8cdd6-444">You can look at the replica to get more information:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricReplicaHealth -ReplicaOrInstanceId 131444422260002646 -PartitionId af2e3e44-a8f8-45ac-9f31-4093eb897600


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Error
UnhealthyEvaluations  : 
                        Error event: SourceId='MyWatchdog', Property='Memory'.
                        
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
                        SourceId              : MyWatchdog
                        Property              : Memory
                        HealthState           : Error
                        SequenceNumber        : 131444451657749403
                        SentAt                : 7/13/2017 6:46:05 PM
                        ReceivedAt            : 7/13/2017 6:46:05 PM
                        TTL                   : Infinite
                        Description           : 
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 7/13/2017 6:46:05 PM, LastOk = 1/1/0001 12:00:00 AM
```

> [!NOTE]
> <span data-ttu-id="8cdd6-445">As avaliações não íntegras mostram o primeiro motivo pelo qual a entidade é avaliada com o estado de integridade atual.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-445">The unhealthy evaluations show the first reason the entity is evaluated to current health state.</span></span> <span data-ttu-id="8cdd6-446">Pode haver vários outros eventos que disparam esse estado, mas eles não são mostrados nas avaliações.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-446">There may be multiple other events that trigger this state, but they are not be reflected in the evaluations.</span></span> <span data-ttu-id="8cdd6-447">Para obter mais informações, faça uma busca detalhada das entidades de integridade para descobrir todos os relatórios não íntegros no cluster.</span><span class="sxs-lookup"><span data-stu-id="8cdd6-447">To get more information, drill down into the health entities to figure out all the unhealthy reports in the cluster.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="8cdd6-448">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8cdd6-448">Next steps</span></span>
[<span data-ttu-id="8cdd6-449">Usar relatórios de integridade do sistema para solução de problemas</span><span class="sxs-lookup"><span data-stu-id="8cdd6-449">Use system health reports to troubleshoot</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[<span data-ttu-id="8cdd6-450">Adicionar relatórios de integridade personalizados do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8cdd6-450">Add custom Service Fabric health reports</span></span>](service-fabric-report-health.md)

[<span data-ttu-id="8cdd6-451">Como relatar e verificar a integridade do serviço</span><span class="sxs-lookup"><span data-stu-id="8cdd6-451">How to report and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="8cdd6-452">Monitorar e diagnosticar serviços localmente</span><span class="sxs-lookup"><span data-stu-id="8cdd6-452">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="8cdd6-453">Atualização de aplicativos do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8cdd6-453">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
