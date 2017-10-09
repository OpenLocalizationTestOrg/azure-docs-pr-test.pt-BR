---
title: entidades do Azure Service Fabric aaaHow tooview agregado de integridade | Microsoft Docs
description: Descreve como tooquery, exibir e avaliar a integridade agregada de entidades do Azure Service Fabric, por meio de consultas de integridade e consultas gerais.
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
ms.openlocfilehash: add810551cac26d2b4ff81b57d94ddd780c2cc2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="view-service-fabric-health-reports"></a><span data-ttu-id="f5ea0-103">Como exibir relatórios de integridade do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f5ea0-103">View Service Fabric health reports</span></span>
<span data-ttu-id="f5ea0-104">O Azure Service Fabric apresenta um [modelo de integridade](service-fabric-health-introduction.md) com entidades de integridade nas quais os componentes do sistema e watchdogs podem relatar condições locais que estão monitorando.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-104">Azure Service Fabric introduces a [health model](service-fabric-health-introduction.md) with health entities on which system components and watchdogs can report local conditions that they are monitoring.</span></span> <span data-ttu-id="f5ea0-105">Olá [repositório de integridade](service-fabric-health-introduction.md#health-store) agrega todos os toodetermine de dados de integridade se entidades estão íntegros.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-105">hello [health store](service-fabric-health-introduction.md#health-store) aggregates all health data toodetermine whether entities are healthy.</span></span>

<span data-ttu-id="f5ea0-106">cluster de saudação é preenchida automaticamente com os relatórios de integridade enviados pelos componentes do sistema hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-106">hello cluster is automatically populated with health reports sent by hello system components.</span></span> <span data-ttu-id="f5ea0-107">Leia mais em [relatórios de integridade do sistema de uso do tootroubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-107">Read more at [Use system health reports tootroubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span></span>

<span data-ttu-id="f5ea0-108">Serviço de malha fornece várias maneiras tooget Olá agregado integridade de entidades de saudação:</span><span class="sxs-lookup"><span data-stu-id="f5ea0-108">Service Fabric provides multiple ways tooget hello aggregated health of hello entities:</span></span>

* <span data-ttu-id="f5ea0-109">[Gerenciador de Malha do Serviço](service-fabric-visualizing-your-cluster.md) ou outras ferramentas de visualização</span><span class="sxs-lookup"><span data-stu-id="f5ea0-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) or other visualization tools</span></span>
* <span data-ttu-id="f5ea0-110">Consultas de integridade (por meio do PowerShell, da API ou de REST)</span><span class="sxs-lookup"><span data-stu-id="f5ea0-110">Health queries (through PowerShell, API, or REST)</span></span>
* <span data-ttu-id="f5ea0-111">Geral consultas que retornam uma lista de entidades que têm integridade como uma das propriedades de saudação (por meio do PowerShell, API ou REST)</span><span class="sxs-lookup"><span data-stu-id="f5ea0-111">General queries that return a list of entities that have health as one of hello properties (through PowerShell, API, or REST)</span></span>

<span data-ttu-id="f5ea0-112">toodemonstrate essas opções, vamos usar um cluster local com cinco nós e hello [fabric: / aplicativo WordCount](http://aka.ms/servicefabric-wordcountapp).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-112">toodemonstrate these options, let's use a local cluster with five nodes and hello [fabric:/WordCount application](http://aka.ms/servicefabric-wordcountapp).</span></span> <span data-ttu-id="f5ea0-113">Olá **fabric: / WordCount** aplicativo contém dois serviços de padrão, um serviço com monitoração de estado do tipo `WordCountServiceType`e um serviço sem monitoração de estado do tipo `WordCountWebServiceType`.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-113">hello **fabric:/WordCount** application contains two default services, a stateful service of type `WordCountServiceType`, and a stateless service of type `WordCountWebServiceType`.</span></span> <span data-ttu-id="f5ea0-114">Alterei Olá `ApplicationManifest.xml` toorequire sete réplicas de destino para o serviço com monitoração de estado hello e uma partição.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-114">I changed hello `ApplicationManifest.xml` toorequire seven target replicas for hello stateful service and one partition.</span></span> <span data-ttu-id="f5ea0-115">Porque há apenas cinco nós no cluster hello, componentes do sistema Olá relatam um aviso na partição de serviço Olá porque ele está abaixo da contagem de destino hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-115">Because there are only five nodes in hello cluster, hello system components report a warning on hello service partition because it is below hello target count.</span></span>

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

## <a name="health-in-service-fabric-explorer"></a><span data-ttu-id="f5ea0-116">Integridade no Gerenciador da Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="f5ea0-116">Health in Service Fabric Explorer</span></span>
<span data-ttu-id="f5ea0-117">Service Fabric Explorer fornece uma exibição visual de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-117">Service Fabric Explorer provides a visual view of hello cluster.</span></span> <span data-ttu-id="f5ea0-118">Na imagem de saudação abaixo, você pode ver que:</span><span class="sxs-lookup"><span data-stu-id="f5ea0-118">In hello image below, you can see that:</span></span>

* <span data-ttu-id="f5ea0-119">Olá aplicativo **fabric: / WordCount** é vermelho (erro) porque ele tem um evento de erro relatado pelo **MyWatchdog** para a propriedade Olá **disponibilidade**.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-119">hello application **fabric:/WordCount** is red (in error) because it has an error event reported by **MyWatchdog** for hello property **Availability**.</span></span>
* <span data-ttu-id="f5ea0-120">Um de seus serviços, **fabric:/WordCount/WordCountService** está amarelo (em aviso).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-120">One of its services, **fabric:/WordCount/WordCountService** is yellow (in warning).</span></span> <span data-ttu-id="f5ea0-121">Olá serviço está configurado com sete réplicas e cluster Olá tem cinco nós, duas repicas não pode ser colocados.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-121">hello service is configured with seven replicas and hello cluster has five nodes, so two repicas can't be placed.</span></span> <span data-ttu-id="f5ea0-122">Embora não seja mostrado aqui, partição de serviço Olá estiver amarela devido a um relatório do sistema de `System.FM` dizendo que `Partition is below target replica or instance count`.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-122">Although it's not shown here, hello service partition is yellow because of a system report from `System.FM` saying that `Partition is below target replica or instance count`.</span></span> <span data-ttu-id="f5ea0-123">gatilhos de partição amarelo Olá Olá serviço amarelo.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-123">hello yellow partition triggers hello yellow service.</span></span>
* <span data-ttu-id="f5ea0-124">cluster de saudação é vermelho devido ao aplicativo hello vermelho.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-124">hello cluster is red because of hello red application.</span></span>

<span data-ttu-id="f5ea0-125">avaliação de saudação usa políticas de padrão de manifesto do cluster hello e o manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-125">hello evaluation uses default policies from hello cluster manifest and application manifest.</span></span> <span data-ttu-id="f5ea0-126">Elas são políticas rígidas e não toleram falhas.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-126">They are strict policies and do not tolerate any failure.</span></span>

<span data-ttu-id="f5ea0-127">Exibição do cluster Olá Service Fabric Explorer de:</span><span class="sxs-lookup"><span data-stu-id="f5ea0-127">View of hello cluster with Service Fabric Explorer:</span></span>

![Exibição de cluster Olá com Gerenciador do Service Fabric.][1]

[1]: ./media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> <span data-ttu-id="f5ea0-129">Leia mais sobre o [Gerenciador da Malha do Serviço](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-129">Read more about [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

## <a name="health-queries"></a><span data-ttu-id="f5ea0-130">Consultas de integridade</span><span class="sxs-lookup"><span data-stu-id="f5ea0-130">Health queries</span></span>
<span data-ttu-id="f5ea0-131">Malha do serviço expõe consultas de integridade para cada Olá suportada [tipos de entidade](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-131">Service Fabric exposes health queries for each of hello supported [entity types](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span></span> <span data-ttu-id="f5ea0-132">Eles podem ser acessados por meio de saudação API, usando métodos em [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), cmdlets do PowerShell e REST.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-132">They can be accessed through hello API, using methods on [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="f5ea0-133">Essas consultas retornam informações de integridade completa sobre entidade Olá: Olá agregado estado de integridade, eventos de integridade de entidade, os estados de integridade filho (quando aplicável), avaliações não íntegras (quando a entidade de saudação não está íntegra) e estatísticas de integridade de filhos (quando aplicável).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-133">These queries return complete health information about hello entity: hello aggregated health state, entity health events, child health states (when applicable), unhealthy evaluations (when hello entity is not healthy), and children health statistics (when applicable).</span></span>

> [!NOTE]
> <span data-ttu-id="f5ea0-134">Uma entidade de integridade é retornada quando está completamente populada no repositório de integridade de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-134">A health entity is returned when it is fully populated in hello health store.</span></span> <span data-ttu-id="f5ea0-135">entidade Olá deve ser ativo (não excluído) e ter um relatório do sistema.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-135">hello entity must be active (not deleted) and have a system report.</span></span> <span data-ttu-id="f5ea0-136">Suas entidades pai na cadeia de hierarquia Olá também devem ter os relatórios do sistema.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-136">Its parent entities on hello hierarchy chain must also have system reports.</span></span> <span data-ttu-id="f5ea0-137">Se alguma dessas condições não forem atendidas, integridade Olá consultas retornam um [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) com [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` que mostra por que a entidade Olá não é retornada.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-137">If any of these conditions are not satisfied, hello health queries return a [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) with [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` that shows why hello entity is not returned.</span></span>
>
>

<span data-ttu-id="f5ea0-138">consultas de integridade Olá devem passar no identificador da entidade hello, dependendo do tipo de entidade hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-138">hello health queries must pass in hello entity identifier, which depends on hello entity type.</span></span> <span data-ttu-id="f5ea0-139">consultas de saudação aceitam parâmetros de política de integridade opcional.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-139">hello queries accept optional health policy parameters.</span></span> <span data-ttu-id="f5ea0-140">Se nenhuma política de integridade forem especificada, Olá [políticas de integridade](service-fabric-health-introduction.md#health-policies) do manifesto de cluster ou o aplicativo hello são usadas para avaliação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-140">If no health policies are specified, hello [health policies](service-fabric-health-introduction.md#health-policies) from hello cluster or application manifest are used for evaluation.</span></span> <span data-ttu-id="f5ea0-141">Se os manifestos de saudação não contém uma definição para políticas de integridade, diretivas de integridade saudação padrão são usadas para avaliação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-141">If hello manifests don't contain a definition for health policies, hello default health policies are used for evaluation.</span></span> <span data-ttu-id="f5ea0-142">diretivas de integridade padrão Olá não tolerar falhas.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-142">hello default health policies do not tolerate any failures.</span></span> <span data-ttu-id="f5ea0-143">consultas de saudação também aceitam filtros para retornar somente os filhos parciais ou eventos – Olá aqueles que respeitam Olá filtros especificados.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-143">hello queries also accept filters for returning only partial children or events--hello ones that respect hello specified filters.</span></span> <span data-ttu-id="f5ea0-144">Outro filtro permite a exclusão de estatísticas de filhos de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-144">Another filter allows excluding hello children statistics.</span></span>

> [!NOTE]
> <span data-ttu-id="f5ea0-145">Olá filtros de saída são aplicados no lado do servidor de saudação, para que o tamanho de resposta de mensagem de saudação é reduzido.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-145">hello output filters are applied on hello server side, so hello message reply size is reduced.</span></span> <span data-ttu-id="f5ea0-146">É recomendável que você use filtros de saída Olá toolimit Olá dados retornam, em vez de aplicam filtros no lado do cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-146">We recommended that you use hello output filters toolimit hello data returned, rather than apply filters on hello client side.</span></span>
>
>

<span data-ttu-id="f5ea0-147">A integridade da entidade contém:</span><span class="sxs-lookup"><span data-stu-id="f5ea0-147">An entity's health contains:</span></span>

* <span data-ttu-id="f5ea0-148">Olá estado de integridade agregado da entidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-148">hello aggregated health state of hello entity.</span></span> <span data-ttu-id="f5ea0-149">Calculado pelo repositório de integridade de saudação com base em relatórios de integridade de entidade, filho estados de integridade (quando aplicável) e políticas de integridade.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-149">Computed by hello health store based on entity health reports, child health states (when applicable), and health policies.</span></span> <span data-ttu-id="f5ea0-150">Leia mais sobre [Avaliação de integridade da entidade](service-fabric-health-introduction.md#health-evaluation).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-150">Read more about [entity health evaluation](service-fabric-health-introduction.md#health-evaluation).</span></span>  
* <span data-ttu-id="f5ea0-151">eventos de integridade Olá na entidade hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-151">hello health events on hello entity.</span></span>
* <span data-ttu-id="f5ea0-152">coleção de saudação de estados de integridade de todos os filhos de entidades de saudação que podem ter filhos.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-152">hello collection of health states of all children for hello entities that can have children.</span></span> <span data-ttu-id="f5ea0-153">estados de integridade de saudação contêm os identificadores de entidade e Olá estado de integridade agregada.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-153">hello health states contain entity identifiers and hello aggregated health state.</span></span> <span data-ttu-id="f5ea0-154">tooget toda a integridade de um filho, chame integridade de consulta Olá Olá filho tipo de entidade e passe no identificador de filho hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-154">tooget complete health for a child, call hello query health for hello child entity type and pass in hello child identifier.</span></span>
* <span data-ttu-id="f5ea0-155">avaliações não íntegras de saudação toohello esse ponto de relatório que disparado estado Olá da entidade de saudação se Olá entidade não está íntegra.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-155">hello unhealthy evaluations that point toohello report that triggered hello state of hello entity, if hello entity is not healthy.</span></span> <span data-ttu-id="f5ea0-156">avaliações de saudação são recursivas, contendo as avaliações de integridade do hello filhos que disparou o estado de integridade atual.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-156">hello evaluations are recursive, containing hello children health evaluations that triggered current health state.</span></span> <span data-ttu-id="f5ea0-157">Por exemplo, um watchdog relatou um erro em uma réplica.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-157">For example, a watchdog reported an error against a replica.</span></span> <span data-ttu-id="f5ea0-158">integridade do aplicativo Hello mostra uma avaliação não íntegro devido tooan de serviço não íntegro; serviço de saudação não está íntegro devido a partição tooa com erro; partição de saudação não está íntegra devido a réplica tooa com erro; réplica de saudação não está íntegra toohello relatório de integridade de erro de watchdog de conclusão.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-158">hello application health shows an unhealthy evaluation due tooan unhealthy service; hello service is unhealthy due tooa partition in error; hello partition is unhealthy due tooa replica in error; hello replica is unhealthy due toohello watchdog error health report.</span></span>
* <span data-ttu-id="f5ea0-159">estatísticas de integridade Olá para todos os tipos de filhos de entidades de saudação que têm filhos.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-159">hello health statistics for all children types of hello entities that have children.</span></span> <span data-ttu-id="f5ea0-160">Por exemplo, a integridade do cluster mostra o número total de saudação de aplicativos, serviços, partições, as réplicas e implantado entidades no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-160">For example, cluster health shows hello total number of applications, services, partitions, replicas, and deployed entities in hello cluster.</span></span> <span data-ttu-id="f5ea0-161">Integridade do serviço mostra o número total de saudação de partições e réplicas em Olá especificado serviço.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-161">Service health shows hello total number of partitions and replicas under hello specified service.</span></span>

## <a name="get-cluster-health"></a><span data-ttu-id="f5ea0-162">Obter integridade do cluster</span><span class="sxs-lookup"><span data-stu-id="f5ea0-162">Get cluster health</span></span>
<span data-ttu-id="f5ea0-163">Retorna Olá integridade da entidade de cluster hello e contém Olá estados de integridade de aplicativos e nós (filhos do cluster Olá).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-163">Returns hello health of hello cluster entity and contains hello health states of applications and nodes (children of hello cluster).</span></span> <span data-ttu-id="f5ea0-164">Entrada:</span><span class="sxs-lookup"><span data-stu-id="f5ea0-164">Input:</span></span>

* <span data-ttu-id="f5ea0-165">Política de integridade de cluster Olá [opcional] usado tooevaluate nós de Olá Olá eventos e clusters.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-165">[Optional] hello cluster health policy used tooevaluate hello nodes and hello cluster events.</span></span>
* <span data-ttu-id="f5ea0-166">Mapa de política de integridade de aplicativo hello [opcional], com as políticas de integridade Olá usado diretivas do manifesto de aplicativo toooverride hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-166">[Optional] hello application health policy map, with hello health policies used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="f5ea0-167">[Opcional] Filtros de eventos, nós e aplicativos que especificam quais entradas são de interesse e devem ser retornadas no resultado da saudação (por exemplo, apenas os erros ou avisos e erros).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-167">[Optional] Filters for events, nodes, and applications that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="f5ea0-168">Todos os eventos, nós e aplicativos são usados tooevaluate Olá agregado da entidade integridade, independentemente de filtro de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-168">All events, nodes, and applications are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="f5ea0-169">[Opcional] Filtre tooexclude estatísticas de integridade.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-169">[Optional] Filter tooexclude health statistics.</span></span>
* <span data-ttu-id="f5ea0-170">[Opcional] Filtrar tooinclude fabric: / estatísticas de integridade do sistema em Olá estatísticas de integridade.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-170">[Optional] Filter tooinclude fabric:/System health statistics in hello health statistics.</span></span> <span data-ttu-id="f5ea0-171">Aplicável somente quando as estatísticas de integridade de saudação não são excluídas.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-171">Only applicable when hello health statistics are not excluded.</span></span> <span data-ttu-id="f5ea0-172">Por padrão, estatísticas de integridade de saudação incluem somente as estatísticas para aplicativos de usuário e o aplicativo de sistema do hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-172">By default, hello health statistics include only statistics for user applications and not hello System application.</span></span>

### <a name="api"></a><span data-ttu-id="f5ea0-173">API</span><span class="sxs-lookup"><span data-stu-id="f5ea0-173">API</span></span>
<span data-ttu-id="f5ea0-174">tooget integridade de cluster, crie um `FabricClient` e chamada hello [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) método no seu **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-174">tooget cluster health, create a `FabricClient` and call hello [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) method on its **HealthManager**.</span></span>

<span data-ttu-id="f5ea0-175">Olá, chamada a seguir obtém a integridade do cluster hello:</span><span class="sxs-lookup"><span data-stu-id="f5ea0-175">hello following call gets hello cluster health:</span></span>

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

<span data-ttu-id="f5ea0-176">Olá código a seguir obtém a integridade do cluster hello usando uma política de integridade de cluster personalizado e filtros para nós e aplicativos.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-176">hello following code gets hello cluster health by using a custom cluster health policy and filters for nodes and applications.</span></span> <span data-ttu-id="f5ea0-177">Especifica estatísticas de integridade Olá incluem malha Olá: / estatísticas do sistema.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-177">It specifies that hello health statistics include hello fabric:/System statistics.</span></span> <span data-ttu-id="f5ea0-178">Ele cria [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), que contém informações de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-178">It creates [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), which contains hello input information.</span></span>

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

### <a name="powershell"></a><span data-ttu-id="f5ea0-179">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5ea0-179">PowerShell</span></span>
<span data-ttu-id="f5ea0-180">integridade de cluster de saudação do Hello cmdlet tooget [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-180">hello cmdlet tooget hello cluster health is [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span></span> <span data-ttu-id="f5ea0-181">Primeiro, conecte o cluster toohello usando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-181">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="f5ea0-182">Olá estado do cluster de saudação é cinco nós, o aplicativo do sistema hello e fabric: / WordCount configurado conforme descrito.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-182">hello state of hello cluster is five nodes, hello system application, and fabric:/WordCount configured as described.</span></span>

<span data-ttu-id="f5ea0-183">Olá cmdlet a seguir obtém a integridade do cluster usando diretivas de integridade padrão.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-183">hello following cmdlet gets cluster health by using default health policies.</span></span> <span data-ttu-id="f5ea0-184">Olá estado de integridade agregada é um aviso, porque Olá fabric: / aplicativo WordCount estiver em um aviso.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-184">hello aggregated health state is warning, because hello fabric:/WordCount application is in warning.</span></span> <span data-ttu-id="f5ea0-185">Observe como o avaliações não íntegras Olá fornecem detalhes sobre condições de saudação que disparou Olá agregado de integridade.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-185">Note how hello unhealthy evaluations provide details on hello conditions that triggered hello aggregated health.</span></span>

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

<span data-ttu-id="f5ea0-186">Olá seguinte cmdlet do PowerShell obtém Olá integridade de cluster hello usando uma política de aplicativo personalizado.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-186">hello following PowerShell cmdlet gets hello health of hello cluster by using a custom application policy.</span></span> <span data-ttu-id="f5ea0-187">Ele filtra somente aplicativos de tooget de resultados e nós em erro ou aviso.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-187">It filters results tooget only applications and nodes in error or warning.</span></span> <span data-ttu-id="f5ea0-188">Como resultado nenhum nó é retornado, pois todos estão íntegros.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-188">As a result, no nodes are returned, as they are all healthy.</span></span> <span data-ttu-id="f5ea0-189">Olá somente fabric: / aplicativo WordCount respeita o filtro de aplicativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-189">Only hello fabric:/WordCount application respects hello applications filter.</span></span> <span data-ttu-id="f5ea0-190">Porque a política personalizada de saudação especifica tooconsider avisos como erros de malha Olá: / aplicativo WordCount, o aplicativo hello é avaliado como em erro, e então é cluster hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-190">Because hello custom policy specifies tooconsider warnings as errors for hello fabric:/WordCount application, hello application is evaluated as in error, and so is hello cluster.</span></span>

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

### <a name="rest"></a><span data-ttu-id="f5ea0-191">REST</span><span class="sxs-lookup"><span data-stu-id="f5ea0-191">REST</span></span>
<span data-ttu-id="f5ea0-192">Você pode obter a integridade do cluster com um [solicitação GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) ou um [solicitação POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) que inclui as políticas de integridade descritas no corpo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-192">You can get cluster health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-node-health"></a><span data-ttu-id="f5ea0-193">Obter integridade do nó</span><span class="sxs-lookup"><span data-stu-id="f5ea0-193">Get node health</span></span>
<span data-ttu-id="f5ea0-194">Retorna Olá integridade de uma entidade de nó e contém eventos de integridade de saudação relatados no nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-194">Returns hello health of a node entity and contains hello health events reported on hello node.</span></span> <span data-ttu-id="f5ea0-195">Entrada:</span><span class="sxs-lookup"><span data-stu-id="f5ea0-195">Input:</span></span>

* <span data-ttu-id="f5ea0-196">Nome do nó Olá [obrigatório] que identifica o nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-196">[Required] hello node name that identifies hello node.</span></span>
* <span data-ttu-id="f5ea0-197">Configurações de política de integridade de cluster [opcional] Olá usado tooevaluate integridade.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-197">[Optional] hello cluster health policy settings used tooevaluate health.</span></span>
* <span data-ttu-id="f5ea0-198">[Opcional] Os filtros de eventos que especifiquem as entradas são de interesse e devem ser retornados no resultado da saudação (por exemplo, apenas os erros ou avisos e erros).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-198">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="f5ea0-199">Todos os eventos são usados tooevaluate Olá agregado da entidade integridade, independentemente de filtro de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-199">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="f5ea0-200">API</span><span class="sxs-lookup"><span data-stu-id="f5ea0-200">API</span></span>
<span data-ttu-id="f5ea0-201">integridade do nó tooget por meio de saudação API, crie um `FabricClient` e chamada hello [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) método no seu HealthManager.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-201">tooget node health through hello API, create a `FabricClient` and call hello [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="f5ea0-202">Olá código a seguir obtém integridade do nó Olá para o nome do nó especificado hello:</span><span class="sxs-lookup"><span data-stu-id="f5ea0-202">hello following code gets hello node health for hello specified node name:</span></span>

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

<span data-ttu-id="f5ea0-203">Olá código a seguir obtém integridade do nó Olá para Olá especificado o nome do nó e passa no filtro de eventos e uma política personalizada por meio de [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="f5ea0-203">hello following code gets hello node health for hello specified node name and passes in events filter and custom policy through [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span></span>

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="f5ea0-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5ea0-204">PowerShell</span></span>
<span data-ttu-id="f5ea0-205">integridade do nó do Hello cmdlet tooget Olá [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-205">hello cmdlet tooget hello node health is [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span></span> <span data-ttu-id="f5ea0-206">Primeiro, conecte o cluster toohello usando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-206">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>
<span data-ttu-id="f5ea0-207">Olá cmdlet a seguir obtém a integridade do nó hello usando diretivas de integridade padrão:</span><span class="sxs-lookup"><span data-stu-id="f5ea0-207">hello following cmdlet gets hello node health by using default health policies:</span></span>

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

<span data-ttu-id="f5ea0-208">Olá cmdlet a seguir obtém Olá integridade de todos os nós no cluster hello:</span><span class="sxs-lookup"><span data-stu-id="f5ea0-208">hello following cmdlet gets hello health of all nodes in hello cluster:</span></span>

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

### <a name="rest"></a><span data-ttu-id="f5ea0-209">REST</span><span class="sxs-lookup"><span data-stu-id="f5ea0-209">REST</span></span>
<span data-ttu-id="f5ea0-210">Você pode obter a integridade do nó com um [solicitação GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) ou um [solicitação POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) que inclui as políticas de integridade descritas no corpo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-210">You can get node health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-application-health"></a><span data-ttu-id="f5ea0-211">Obter integridade do aplicativo</span><span class="sxs-lookup"><span data-stu-id="f5ea0-211">Get application health</span></span>
<span data-ttu-id="f5ea0-212">Retorna a integridade de uma entidade de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-212">Returns hello health of an application entity.</span></span> <span data-ttu-id="f5ea0-213">Ele contém os estados de integridade de saudação do aplicativo hello implantado e filhos de serviço.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-213">It contains hello health states of hello deployed application and service children.</span></span> <span data-ttu-id="f5ea0-214">Entrada:</span><span class="sxs-lookup"><span data-stu-id="f5ea0-214">Input:</span></span>

* <span data-ttu-id="f5ea0-215">Olá [obrigatório] nome do aplicativo (URI) que identifica o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-215">[Required] hello application name (URI) that identifies hello application.</span></span>
* <span data-ttu-id="f5ea0-216">Política de integridade de aplicativo hello [opcional] usado diretivas do manifesto de aplicativo toooverride hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-216">[Optional] hello application health policy used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="f5ea0-217">[Opcional] Os filtros de eventos, serviços e aplicativos implantados que especificam quais entradas são de interesse e devem ser retornados no resultado da saudação (por exemplo, apenas os erros ou avisos e erros).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-217">[Optional] Filters for events, services, and deployed applications that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="f5ea0-218">Todos os eventos, serviços e aplicativos implantados são usados tooevaluate Olá agregado da entidade integridade, independentemente de filtro de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-218">All events, services, and deployed applications are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="f5ea0-219">[Opcional] Estatísticas de integridade de saudação tooexclude de filtro.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-219">[Optional] Filter tooexclude hello health statistics.</span></span> <span data-ttu-id="f5ea0-220">Se não for especificado, as estatísticas de integridade de saudação incluem okey hello, de aviso e de contagem de erros para todos os filhos do aplicativo: serviços, partições, réplicas, aplicativos implantados e pacotes de serviço implantados.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-220">If not specified, hello health statistics include hello ok, warning, and error count for all application children: services, partitions, replicas, deployed applications, and deployed service packages.</span></span>

### <a name="api"></a><span data-ttu-id="f5ea0-221">API</span><span class="sxs-lookup"><span data-stu-id="f5ea0-221">API</span></span>
<span data-ttu-id="f5ea0-222">integridade do aplicativo tooget, criar um `FabricClient` e chamada hello [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) método no seu HealthManager.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-222">tooget application health, create a `FabricClient` and call hello [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="f5ea0-223">Olá, código a seguir obtém Olá integridade de aplicativo para o nome do aplicativo especificado hello (URI):</span><span class="sxs-lookup"><span data-stu-id="f5ea0-223">hello following code gets hello application health for hello specified application name (URI):</span></span>

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

<span data-ttu-id="f5ea0-224">Olá código a seguir obtém Olá aplicativo integridade para o nome do aplicativo especificado hello (URI), com filtros e políticas personalizadas especificado via [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-224">hello following code gets hello application health for hello specified application name (URI), with filters and custom policies specified via [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span></span>

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

### <a name="powershell"></a><span data-ttu-id="f5ea0-225">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5ea0-225">PowerShell</span></span>
<span data-ttu-id="f5ea0-226">integridade do aplicativo Hello cmdlet tooget Olá é [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-226">hello cmdlet tooget hello application health is [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="f5ea0-227">Primeiro, conecte o cluster toohello usando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-227">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="f5ea0-228">Hello, cmdlet a seguir retorna integridade de saudação do hello **fabric: / WordCount** aplicativo:</span><span class="sxs-lookup"><span data-stu-id="f5ea0-228">hello following cmdlet returns hello health of hello **fabric:/WordCount** application:</span></span>

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

<span data-ttu-id="f5ea0-229">Olá seguindo os passos de cmdlet do PowerShell em políticas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-229">hello following PowerShell cmdlet passes in custom policies.</span></span> <span data-ttu-id="f5ea0-230">Ele também filtra filhos e eventos.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-230">It also filters children and events.</span></span>

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

### <a name="rest"></a><span data-ttu-id="f5ea0-231">REST</span><span class="sxs-lookup"><span data-stu-id="f5ea0-231">REST</span></span>
<span data-ttu-id="f5ea0-232">Você pode obter a integridade do aplicativo com um [solicitação GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) ou um [solicitação POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) que inclui as políticas de integridade descritas no corpo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-232">You can get application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-service-health"></a><span data-ttu-id="f5ea0-233">Obter integridade do serviço</span><span class="sxs-lookup"><span data-stu-id="f5ea0-233">Get service health</span></span>
<span data-ttu-id="f5ea0-234">Retorna a integridade de saudação de uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-234">Returns hello health of a service entity.</span></span> <span data-ttu-id="f5ea0-235">Ele contém Olá estados de integridade de partição.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-235">It contains hello partition health states.</span></span> <span data-ttu-id="f5ea0-236">Entrada:</span><span class="sxs-lookup"><span data-stu-id="f5ea0-236">Input:</span></span>

* <span data-ttu-id="f5ea0-237">Olá [obrigatório] nome do serviço (URI) que identifica o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-237">[Required] hello service name (URI) that identifies hello service.</span></span>
* <span data-ttu-id="f5ea0-238">Política de integridade de aplicativo hello [opcional] usado diretiva do manifesto de aplicativo toooverride hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-238">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="f5ea0-239">[Opcional] Filtros de eventos e partições que especificam quais entradas são de interesse e devem ser retornadas no resultado da saudação (por exemplo, apenas os erros ou avisos e erros).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-239">[Optional] Filters for events and partitions that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="f5ea0-240">Todos os eventos e as partições são usadas tooevaluate Olá agregado da entidade integridade, independentemente de filtro de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-240">All events and partitions are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="f5ea0-241">[Opcional] Filtre tooexclude estatísticas de integridade.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-241">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="f5ea0-242">Se não for especificado, Olá integridade estatísticas Mostrar Olá okey, aviso e erro de contagem de todas as partições e réplicas do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-242">If not specified, hello health statistics show hello ok, warning, and error count for all partitions and replicas of hello service.</span></span>

### <a name="api"></a><span data-ttu-id="f5ea0-243">API</span><span class="sxs-lookup"><span data-stu-id="f5ea0-243">API</span></span>
<span data-ttu-id="f5ea0-244">integridade do serviço tooget por meio de saudação API, crie um `FabricClient` e chamada hello [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) método no seu HealthManager.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-244">tooget service health through hello API, create a `FabricClient` and call hello [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="f5ea0-245">Olá, exemplo a seguir obtém Olá integridade de um serviço com o nome de serviço especificado (URI):</span><span class="sxs-lookup"><span data-stu-id="f5ea0-245">hello following example gets hello health of a service with specified service name (URI):</span></span>

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

<span data-ttu-id="f5ea0-246">Olá, código a seguir obtém Olá a integridade do serviço para nome de serviço especificado da saudação (URI), especificando filtros e uma política personalizada por meio de [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="f5ea0-246">hello following code gets hello service health for hello specified service name (URI), specifying filters and custom policy via [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span></span>

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="f5ea0-247">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5ea0-247">PowerShell</span></span>
<span data-ttu-id="f5ea0-248">integridade do serviço do Hello cmdlet tooget Olá [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-248">hello cmdlet tooget hello service health is [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span></span> <span data-ttu-id="f5ea0-249">Primeiro, conecte o cluster toohello usando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-249">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="f5ea0-250">Olá cmdlet a seguir obtém a integridade do serviço hello usando diretivas de integridade padrão:</span><span class="sxs-lookup"><span data-stu-id="f5ea0-250">hello following cmdlet gets hello service health by using default health policies:</span></span>

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

### <a name="rest"></a><span data-ttu-id="f5ea0-251">REST</span><span class="sxs-lookup"><span data-stu-id="f5ea0-251">REST</span></span>
<span data-ttu-id="f5ea0-252">Você pode obter a integridade do serviço com um [solicitação GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) ou um [solicitação POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) que inclui as políticas de integridade descritas no corpo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-252">You can get service health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-partition-health"></a><span data-ttu-id="f5ea0-253">Obter integridade da partição</span><span class="sxs-lookup"><span data-stu-id="f5ea0-253">Get partition health</span></span>
<span data-ttu-id="f5ea0-254">Retorna a integridade de saudação de uma entidade de partição.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-254">Returns hello health of a partition entity.</span></span> <span data-ttu-id="f5ea0-255">Ele contém Olá estados de integridade de réplica.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-255">It contains hello replica health states.</span></span> <span data-ttu-id="f5ea0-256">Entrada:</span><span class="sxs-lookup"><span data-stu-id="f5ea0-256">Input:</span></span>

* <span data-ttu-id="f5ea0-257">Partição de saudação [obrigatório] ID (GUID) que identifica a partição de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-257">[Required] hello partition ID (GUID) that identifies hello partition.</span></span>
* <span data-ttu-id="f5ea0-258">Política de integridade de aplicativo hello [opcional] usado diretiva do manifesto de aplicativo toooverride hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-258">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="f5ea0-259">[Opcional] Filtros de eventos e as réplicas que especificam quais entradas são de interesse e devem ser retornadas no resultado da saudação (por exemplo, apenas os erros ou avisos e erros).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-259">[Optional] Filters for events and replicas that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="f5ea0-260">Todos os eventos e as réplicas são usadas tooevaluate Olá agregado da entidade integridade, independentemente de filtro de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-260">All events and replicas are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="f5ea0-261">[Opcional] Filtre tooexclude estatísticas de integridade.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-261">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="f5ea0-262">Se não for especificado, as estatísticas de integridade de Olá mostram quantas réplicas estão em okey, aviso e erro estados.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-262">If not specified, hello health statistics show how many replicas are in ok, warning, and error states.</span></span>

### <a name="api"></a><span data-ttu-id="f5ea0-263">API</span><span class="sxs-lookup"><span data-stu-id="f5ea0-263">API</span></span>
<span data-ttu-id="f5ea0-264">integridade da partição tooget por meio de saudação API, crie um `FabricClient` e chamada hello [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) método no seu HealthManager.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-264">tooget partition health through hello API, create a `FabricClient` and call hello [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="f5ea0-265">criar parâmetros opcionais de toospecify, [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-265">toospecify optional parameters, create [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span></span>

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a><span data-ttu-id="f5ea0-266">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5ea0-266">PowerShell</span></span>
<span data-ttu-id="f5ea0-267">integridade da partição Olá Olá cmdlet tooget é [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-267">hello cmdlet tooget hello partition health is [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span></span> <span data-ttu-id="f5ea0-268">Primeiro, conecte o cluster toohello usando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-268">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="f5ea0-269">Olá, cmdlet a seguir obtém Olá integridade de todas as partições de saudação **fabric: / WordCount/WordCountService** serviço e filtra os estados de integridade da réplica:</span><span class="sxs-lookup"><span data-stu-id="f5ea0-269">hello following cmdlet gets hello health for all partitions of hello **fabric:/WordCount/WordCountService** service and filters out replica health states:</span></span>

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
                        Description           : hello Load Balancer was unable toofind a placement for one or more of hello Service's Replicas:
                        Secondary replica could not be placed due toohello following constraints and properties:  
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

### <a name="rest"></a><span data-ttu-id="f5ea0-270">REST</span><span class="sxs-lookup"><span data-stu-id="f5ea0-270">REST</span></span>
<span data-ttu-id="f5ea0-271">Você pode obter a integridade da partição com um [solicitação GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) ou um [solicitação POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) que inclui as políticas de integridade descritas no corpo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-271">You can get partition health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-replica-health"></a><span data-ttu-id="f5ea0-272">Obter integridade da réplica</span><span class="sxs-lookup"><span data-stu-id="f5ea0-272">Get replica health</span></span>
<span data-ttu-id="f5ea0-273">Retorna a integridade de saudação de uma réplica de serviço com monitoração de estado ou uma instância de serviço sem monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-273">Returns hello health of a stateful service replica or a stateless service instance.</span></span> <span data-ttu-id="f5ea0-274">Entrada:</span><span class="sxs-lookup"><span data-stu-id="f5ea0-274">Input:</span></span>

* <span data-ttu-id="f5ea0-275">[Obrigatório] Olá partição ID (GUID) e réplica ID que identifica réplica hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-275">[Required] hello partition ID (GUID) and replica ID that identifies hello replica.</span></span>
* <span data-ttu-id="f5ea0-276">Parâmetros de política de integridade de aplicativo hello [opcional] usado diretivas do manifesto de aplicativo toooverride hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-276">[Optional] hello application health policy parameters used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="f5ea0-277">[Opcional] Os filtros de eventos que especifiquem as entradas são de interesse e devem ser retornados no resultado da saudação (por exemplo, apenas os erros ou avisos e erros).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-277">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="f5ea0-278">Todos os eventos são usados tooevaluate Olá agregado da entidade integridade, independentemente de filtro de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-278">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="f5ea0-279">API</span><span class="sxs-lookup"><span data-stu-id="f5ea0-279">API</span></span>
<span data-ttu-id="f5ea0-280">integridade da réplica Olá tooget por meio de saudação API, crie um `FabricClient` e chamada hello [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) método no seu HealthManager.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-280">tooget hello replica health through hello API, create a `FabricClient` and call hello [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) method on its HealthManager.</span></span> <span data-ttu-id="f5ea0-281">use parâmetros avançados de toospecify [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-281">toospecify advanced parameters, use [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span></span>

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a><span data-ttu-id="f5ea0-282">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5ea0-282">PowerShell</span></span>
<span data-ttu-id="f5ea0-283">integridade da réplica Olá Olá cmdlet tooget é [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-283">hello cmdlet tooget hello replica health is [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span></span> <span data-ttu-id="f5ea0-284">Primeiro, conecte o cluster toohello usando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-284">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="f5ea0-285">Olá, cmdlet a seguir obtém Olá integridade da réplica primária de saudação para todas as partições do serviço de saudação:</span><span class="sxs-lookup"><span data-stu-id="f5ea0-285">hello following cmdlet gets hello health of hello primary replica for all partitions of hello service:</span></span>

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

### <a name="rest"></a><span data-ttu-id="f5ea0-286">REST</span><span class="sxs-lookup"><span data-stu-id="f5ea0-286">REST</span></span>
<span data-ttu-id="f5ea0-287">Você pode obter a integridade da réplica com um [solicitação GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) ou um [solicitação POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) que inclui as políticas de integridade descritas no corpo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-287">You can get replica health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-deployed-application-health"></a><span data-ttu-id="f5ea0-288">Obter integridade do aplicativo implantado</span><span class="sxs-lookup"><span data-stu-id="f5ea0-288">Get deployed application health</span></span>
<span data-ttu-id="f5ea0-289">Retorna Olá integridade de um aplicativo implantado em uma entidade do nó.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-289">Returns hello health of an application deployed on a node entity.</span></span> <span data-ttu-id="f5ea0-290">Ele contém os estados de integridade de pacote de serviço Olá implantado.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-290">It contains hello deployed service package health states.</span></span> <span data-ttu-id="f5ea0-291">Entrada:</span><span class="sxs-lookup"><span data-stu-id="f5ea0-291">Input:</span></span>

* <span data-ttu-id="f5ea0-292">Nome do aplicativo hello [obrigatório] (URI) e o nome de nó (string) que identificam Olá implantado o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-292">[Required] hello application name (URI) and node name (string) that identify hello deployed application.</span></span>
* <span data-ttu-id="f5ea0-293">Política de integridade de aplicativo hello [opcional] usado diretivas do manifesto de aplicativo toooverride hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-293">[Optional] hello application health policy used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="f5ea0-294">[Opcional] Os filtros de eventos e pacotes de serviço implantado que especificam quais entradas são de interesse e devem ser retornados no resultado da saudação (por exemplo, apenas os erros ou avisos e erros).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-294">[Optional] Filters for events and deployed service packages that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="f5ea0-295">Todos os eventos e pacotes de serviços implantados são usados tooevaluate Olá agregado da entidade integridade, independentemente de filtro de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-295">All events and deployed service packages are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="f5ea0-296">[Opcional] Filtre tooexclude estatísticas de integridade.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-296">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="f5ea0-297">Se não for especificado, o hello estatísticas de integridade mostram o número de saudação de pacotes de serviço implantado nos Estados de integridade okey, aviso e erro.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-297">If not specified, hello health statistics show hello number of deployed service packages in ok, warning, and error health states.</span></span>

### <a name="api"></a><span data-ttu-id="f5ea0-298">API</span><span class="sxs-lookup"><span data-stu-id="f5ea0-298">API</span></span>
<span data-ttu-id="f5ea0-299">integridade de saudação tooget de um aplicativo implantado em um nó por meio de saudação API, crie um `FabricClient` e chamada hello [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) método no seu HealthManager.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-299">tooget hello health of an application deployed on a node through hello API, create a `FabricClient` and call hello [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="f5ea0-300">parâmetros opcionais de toospecify, use [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-300">toospecify optional parameters, use [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span></span>

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a><span data-ttu-id="f5ea0-301">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5ea0-301">PowerShell</span></span>
<span data-ttu-id="f5ea0-302">Olá cmdlet tooget Olá implantado integridade do aplicativo é [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-302">hello cmdlet tooget hello deployed application health is [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="f5ea0-303">Primeiro, conecte o cluster toohello usando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-303">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="f5ea0-304">toofind limite em que um aplicativo é implantado, execute [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) e examinar Olá implantado filhos do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-304">toofind out where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at hello deployed application children.</span></span>

<span data-ttu-id="f5ea0-305">Hello, cmdlet a seguir obtém Olá integridade de saudação **fabric: / WordCount** aplicativo implantado em **_Node_2**.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-305">hello following cmdlet gets hello health of hello **fabric:/WordCount** application deployed on **_Node_2**.</span></span>

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
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/13/2017 5:57:17 PM, LastWarning = 1/1/0001 12:00:00 AM
                                     
HealthStatistics                   : 
                                     DeployedServicePackage : 2 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="f5ea0-306">REST</span><span class="sxs-lookup"><span data-stu-id="f5ea0-306">REST</span></span>
<span data-ttu-id="f5ea0-307">Você pode obter a integridade do aplicativo implantado com um [solicitação GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) ou um [solicitação POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) que inclui as políticas de integridade descritas no corpo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-307">You can get deployed application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-deployed-service-package-health"></a><span data-ttu-id="f5ea0-308">Obter integridade do pacote de serviço implantado</span><span class="sxs-lookup"><span data-stu-id="f5ea0-308">Get deployed service package health</span></span>
<span data-ttu-id="f5ea0-309">Retorna Olá integridade de uma entidade de pacote de serviço implantado.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-309">Returns hello health of a deployed service package entity.</span></span> <span data-ttu-id="f5ea0-310">Entrada:</span><span class="sxs-lookup"><span data-stu-id="f5ea0-310">Input:</span></span>

* <span data-ttu-id="f5ea0-311">Nome do aplicativo hello [obrigatório] (URI), nome do nó (string) e o nome manifesto do serviço (string) que identificam Olá implantadas pacote de serviço.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-311">[Required] hello application name (URI), node name (string), and service manifest name (string) that identify hello deployed service package.</span></span>
* <span data-ttu-id="f5ea0-312">Política de integridade de aplicativo hello [opcional] usado diretiva do manifesto de aplicativo toooverride hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-312">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="f5ea0-313">[Opcional] Os filtros de eventos que especifiquem as entradas são de interesse e devem ser retornados no resultado da saudação (por exemplo, apenas os erros ou avisos e erros).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-313">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="f5ea0-314">Todos os eventos são usados tooevaluate Olá agregado da entidade integridade, independentemente de filtro de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-314">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="f5ea0-315">API</span><span class="sxs-lookup"><span data-stu-id="f5ea0-315">API</span></span>
<span data-ttu-id="f5ea0-316">integridade de saudação tooget de um pacote de serviço implantado por meio de saudação API, crie um `FabricClient` e chamada hello [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) método no seu HealthManager.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-316">tooget hello health of a deployed service package through hello API, create a `FabricClient` and call hello [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) method on its HealthManager.</span></span> <span data-ttu-id="f5ea0-317">parâmetros opcionais de toospecify, use [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-317">toospecify optional parameters, use [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span></span>

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a><span data-ttu-id="f5ea0-318">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5ea0-318">PowerShell</span></span>
<span data-ttu-id="f5ea0-319">Olá integridade do pacote de serviço do cmdlet tooget Olá implantado é [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-319">hello cmdlet tooget hello deployed service package health is [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span></span> <span data-ttu-id="f5ea0-320">Primeiro, conecte o cluster toohello usando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-320">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="f5ea0-321">executar toosee onde um aplicativo é implantado, [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) e analisar os aplicativos implantado de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-321">toosee where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at hello deployed applications.</span></span> <span data-ttu-id="f5ea0-322">toosee que os pacotes de serviço estão em um aplicativo, procure no hello implantado filhos de pacote de serviço em Olá [ServiceFabricDeployedApplicationHealth Get](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) saída.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-322">toosee which service packages are in an application, look at hello deployed service package children in hello [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) output.</span></span>

<span data-ttu-id="f5ea0-323">Hello, cmdlet a seguir obtém Olá integridade de saudação **WordCountServicePkg** pacote de serviço do hello **fabric: / WordCount** aplicativo implantado em **_Node_2**.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-323">hello following cmdlet gets hello health of hello **WordCountServicePkg** service package of hello **fabric:/WordCount** application deployed on **_Node_2**.</span></span> <span data-ttu-id="f5ea0-324">Olá entidade tem **System.Hosting** relatórios de ativação bem-sucedida do pacote de serviço e o ponto de entrada e o registro bem-sucedido do tipo de serviço.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-324">hello entity has **System.Hosting** reports for successful service-package and entry-point activation, and successful service-type registration.</span></span>

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
                             Description           : hello ServicePackage was activated successfully.
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
                             Description           : hello CodePackage was activated successfully.
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
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="f5ea0-325">REST</span><span class="sxs-lookup"><span data-stu-id="f5ea0-325">REST</span></span>
<span data-ttu-id="f5ea0-326">Você pode obter a integridade do pacote de serviço implantado com um [solicitação GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) ou um [solicitação POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) que inclui as políticas de integridade descritas no corpo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-326">You can get deployed service package health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="health-chunk-queries"></a><span data-ttu-id="f5ea0-327">Consultas de integridade em blocos</span><span class="sxs-lookup"><span data-stu-id="f5ea0-327">Health chunk queries</span></span>
<span data-ttu-id="f5ea0-328">consultas de parte de integridade de saudação podem retornar os filhos de cluster de vários níveis (recursivamente), por filtros de entrada.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-328">hello health chunk queries can return multi-level cluster children (recursively), per input filters.</span></span> <span data-ttu-id="f5ea0-329">Ele dá suporte a filtros avançados que permitem que uma grande flexibilidade na escolha de filhos Olá toobe retornado.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-329">It supports advanced filters that allow a lot of flexibility in choosing hello children toobe returned.</span></span> <span data-ttu-id="f5ea0-330">filtros de saudação podem especificar filhos por identificador exclusivo da saudação ou outros identificadores de grupo e/ou os estados de integridade.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-330">hello filters can specify children by hello unique identifier or by other group identifiers and/or health states.</span></span> <span data-ttu-id="f5ea0-331">Por padrão, nenhum filho é incluído, como comandos toohealth contrário que incluem sempre o primeiro nível filhos.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-331">By default, no children are included, as opposed toohealth commands that always include first-level children.</span></span>

<span data-ttu-id="f5ea0-332">Olá [consultas de integridade](service-fabric-view-entities-aggregated-health.md#health-queries) retorno filhos apenas de primeiro nível de saudação especificado entidade por filtros necessários.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-332">hello [health queries](service-fabric-view-entities-aggregated-health.md#health-queries) return only first-level children of hello specified entity per required filters.</span></span> <span data-ttu-id="f5ea0-333">tooget Olá filhos filhos hello, você deve chamar APIs de integridade adicional para cada entidade de interesse.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-333">tooget hello children of hello children, you must call additional health APIs for each entity of interest.</span></span> <span data-ttu-id="f5ea0-334">Da mesma forma, integridade de saudação tooget de entidades específicas, você deve chamar integridade de uma API para cada entidade desejada.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-334">Similarly, tooget hello health of specific entities, you must call one health API for each desired entity.</span></span> <span data-ttu-id="f5ea0-335">Olá parte consulta filtragem avançada permite que você toorequest vários itens de interesse em uma consulta, reduzindo o tamanho de mensagem de saudação e número de saudação de mensagens.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-335">hello chunk query advanced filtering allows you toorequest multiple items of interest in one query, minimizing hello message size and hello number of messages.</span></span>

<span data-ttu-id="f5ea0-336">valor de saudação de consulta de parte de saudação é que você pode obter o estado de integridade para mais entidades de cluster (potencialmente todos os cluster entidades começando na raiz necessário) em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-336">hello value of hello chunk query is that you can get health state for more cluster entities (potentially all cluster entities starting at required root) in one call.</span></span> <span data-ttu-id="f5ea0-337">Você pode expressar uma consulta de integridade complexa da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f5ea0-337">You can express complex health query such as:</span></span>

* <span data-ttu-id="f5ea0-338">Retorne apenas os aplicativos com erro e, para esses aplicativos, inclua todos os serviços em aviso|erro.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-338">Return only applications in error, and for those applications include all services in warning or error.</span></span> <span data-ttu-id="f5ea0-339">Para os serviços retornados, inclua todas as partições.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-339">For returned services, include all partitions.</span></span>
* <span data-ttu-id="f5ea0-340">Retorne apenas integridade de saudação de quatro aplicativos, especificado por seus nomes.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-340">Return only hello health of four applications, specified by their names.</span></span>
* <span data-ttu-id="f5ea0-341">Retorne apenas integridade de saudação de aplicativos de um tipo de aplicativo desejado.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-341">Return only hello health of applications of a desired application type.</span></span>
* <span data-ttu-id="f5ea0-342">Retorne todas as entidades implantadas em um nó.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-342">Return all deployed entities on a node.</span></span> <span data-ttu-id="f5ea0-343">Retorna todos os aplicativos, implantados todos os aplicativos no nó especificado hello e todos os pacotes de serviço Olá implantado naquele nó.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-343">Returns all applications, all deployed applications on hello specified node and all hello deployed service packages on that node.</span></span>
* <span data-ttu-id="f5ea0-344">Retorna todas as réplicas com erro.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-344">Return all replicas in error.</span></span> <span data-ttu-id="f5ea0-345">Retorna todos os aplicativos, serviços, partições e somente réplicas com erro.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-345">Returns all applications, services, partitions, and only replicas in error.</span></span>
* <span data-ttu-id="f5ea0-346">Retorna todos os aplicativos.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-346">Return all applications.</span></span> <span data-ttu-id="f5ea0-347">Para um serviço específico, inclua todas as partições.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-347">For a specified service, include all partitions.</span></span>

<span data-ttu-id="f5ea0-348">Atualmente, consulta de parte de integridade de saudação é exposta somente para a entidade de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-348">Currently, hello health chunk query is exposed only for hello cluster entity.</span></span> <span data-ttu-id="f5ea0-349">Ela retorna uma parte da integridade do cluster, que contém:</span><span class="sxs-lookup"><span data-stu-id="f5ea0-349">It returns a cluster health chunk, which contains:</span></span>

* <span data-ttu-id="f5ea0-350">estado de integridade do cluster agregado Hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-350">hello cluster aggregated health state.</span></span>
* <span data-ttu-id="f5ea0-351">Olá integridade estado parte lista de nós que respeitar os filtros de entrada.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-351">hello health state chunk list of nodes that respect input filters.</span></span>
* <span data-ttu-id="f5ea0-352">Olá integridade estado parte lista de aplicativos que respeitar os filtros de entrada.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-352">hello health state chunk list of applications that respect input filters.</span></span> <span data-ttu-id="f5ea0-353">Cada bloco de estado de integridade do aplicativo contém uma lista de partes com todos os serviços que respeitam os filtros de entrada e uma lista de partes com todos os aplicativos implantados que respeita filtros hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-353">Each application health state chunk contains a chunk list with all services that respect input filters and a chunk list with all deployed applications that respect hello filters.</span></span> <span data-ttu-id="f5ea0-354">Mesmo para os filhos de saudação de serviços e aplicativos implantados.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-354">Same for hello children of services and deployed applications.</span></span> <span data-ttu-id="f5ea0-355">Dessa forma, todas as entidades no cluster Olá podem ser potencialmente retornadas se solicitado, de maneira hierárquica.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-355">This way, all entities in hello cluster can be potentially returned if requested, in a hierarchical fashion.</span></span>

### <a name="cluster-health-chunk-query"></a><span data-ttu-id="f5ea0-356">Consulta em bloco sobre a integridade do cluster</span><span class="sxs-lookup"><span data-stu-id="f5ea0-356">Cluster health chunk query</span></span>
<span data-ttu-id="f5ea0-357">Retorna Olá integridade da entidade de cluster hello e contém partes de estado de integridade hierárquica Olá dos filhos necessários.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-357">Returns hello health of hello cluster entity and contains hello hierarchical health state chunks of required children.</span></span> <span data-ttu-id="f5ea0-358">Entrada:</span><span class="sxs-lookup"><span data-stu-id="f5ea0-358">Input:</span></span>

* <span data-ttu-id="f5ea0-359">Política de integridade de cluster Olá [opcional] usado tooevaluate nós de Olá Olá eventos e clusters.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-359">[Optional] hello cluster health policy used tooevaluate hello nodes and hello cluster events.</span></span>
* <span data-ttu-id="f5ea0-360">Mapa de política de integridade de aplicativo hello [opcional], com as políticas de integridade Olá usado diretivas do manifesto de aplicativo toooverride hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-360">[Optional] hello application health policy map, with hello health policies used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="f5ea0-361">[Opcional] Os filtros para nós e os aplicativos que especificam quais entradas são de interesse e devem ser retornados no resultado de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-361">[Optional] Filters for nodes and applications that specify which entries are of interest and should be returned in hello result.</span></span> <span data-ttu-id="f5ea0-362">filtros de saudação são tooan específico/grupo de entidades de entidades ou são aplicáveis tooall entidades nesse nível.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-362">hello filters are specific tooan entity/group of entities or are applicable tooall entities at that level.</span></span> <span data-ttu-id="f5ea0-363">saudação de filtros pode conter um filtro geral e/ou filtros para entidades de granularidade toofine identificadores específicos retornados pela consulta hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-363">hello list of filters can contain one general filter and/or filters for specific identifiers toofine-grain entities returned by hello query.</span></span> <span data-ttu-id="f5ea0-364">Se estiver vazio, os filhos de saudação não são retornados por padrão.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-364">If empty, hello children are not returned by default.</span></span>
  <span data-ttu-id="f5ea0-365">Leia mais sobre filtros de saudação [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) e [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-365">Read more about hello filters at [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) and [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span></span> <span data-ttu-id="f5ea0-366">Olá aplicativo filtros pode recursivamente especificar filtros avançados para filhos.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-366">hello application filters can recursively specify advanced filters for children.</span></span>

<span data-ttu-id="f5ea0-367">resultados de fragmento de saudação incluem filhos Olá respeitam os filtros de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-367">hello chunk result includes hello children that respect hello filters.</span></span>

<span data-ttu-id="f5ea0-368">No momento, a consulta de parte de saudação não retorna avaliações não íntegras ou eventos de entidade.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-368">Currently, hello chunk query does not return unhealthy evaluations or entity events.</span></span> <span data-ttu-id="f5ea0-369">Essas informações adicionais podem ser obtidas usando a consulta de integridade do cluster existente hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-369">That extra information can be obtained using hello existing cluster health query.</span></span>

### <a name="api"></a><span data-ttu-id="f5ea0-370">API</span><span class="sxs-lookup"><span data-stu-id="f5ea0-370">API</span></span>
<span data-ttu-id="f5ea0-371">integridade do cluster tooget parte, crie um `FabricClient` e chamada hello [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) método no seu **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-371">tooget cluster health chunk, create a `FabricClient` and call hello [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) method on its **HealthManager**.</span></span> <span data-ttu-id="f5ea0-372">Você pode passar de [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe diretivas de integridade e filtros avançados.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-372">You can pass in [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe health policies and advanced filters.</span></span>

<span data-ttu-id="f5ea0-373">Olá código a seguir obtém o fragmento de integridade do cluster com filtros avançados.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-373">hello following code gets cluster health chunk with advanced filters.</span></span>

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

// Application filter: for specific application, return no services except hello ones of interest
var wordCountApplicationFilter = new ApplicationHealthStateFilter()
    {
        // Always return fabric:/WordCount application
        ApplicationNameFilter = new Uri("fabric:/WordCount"),
    };
wordCountApplicationFilter.ServiceFilters.Add(wordCountServiceFilter);

queryDescription.ApplicationFilters.Add(wordCountApplicationFilter);

var result = await fabricClient.HealthManager.GetClusterHealthChunkAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="f5ea0-374">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5ea0-374">PowerShell</span></span>
<span data-ttu-id="f5ea0-375">integridade de cluster de saudação do Hello cmdlet tooget [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-375">hello cmdlet tooget hello cluster health is [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span></span> <span data-ttu-id="f5ea0-376">Primeiro, conecte o cluster toohello usando Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-376">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="f5ea0-377">Olá código a seguir obtém nós apenas se estiverem em erro, exceto de um nó específico, que sempre deve ser retornado.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-377">hello following code gets nodes only if they are in Error except for a specific node, which should always be returned.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$nodeFilter1 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{HealthStateFilter=$errorFilter}
$nodeFilter2 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{NodeNameFilter="_Node_1";HealthStateFilter=$allFilter}
# Create node filter list that will be passed in hello cmdlet
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

<span data-ttu-id="f5ea0-378">Olá cmdlet a seguir obtém a parte do cluster com filtros de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-378">hello following cmdlet gets cluster chunk with application filters.</span></span>

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

<span data-ttu-id="f5ea0-379">Olá cmdlet a seguir retorna implantadas todas as entidades em um nó.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-379">hello following cmdlet returns all deployed entities on a node.</span></span>

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

### <a name="rest"></a><span data-ttu-id="f5ea0-380">REST</span><span class="sxs-lookup"><span data-stu-id="f5ea0-380">REST</span></span>
<span data-ttu-id="f5ea0-381">Você pode obter parte de integridade de cluster com um [solicitação GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) ou um [solicitação POST](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) que inclui políticas de integridade e descritos no corpo de saudação de filtros avançados.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-381">You can get cluster health chunk with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) that includes health policies and advanced filters described in hello body.</span></span>

## <a name="general-queries"></a><span data-ttu-id="f5ea0-382">Consultas gerais</span><span class="sxs-lookup"><span data-stu-id="f5ea0-382">General queries</span></span>
<span data-ttu-id="f5ea0-383">As consultas gerais retornam a lista de entidades do Service Fabric de um tipo especificado.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-383">General queries return a list of Service Fabric entities of a specified type.</span></span> <span data-ttu-id="f5ea0-384">Eles são expostos por meio da API de saudação (por meio de métodos de saudação em **FabricClient.QueryManager**), cmdlets do PowerShell e REST.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-384">They are exposed through hello API (via hello methods on **FabricClient.QueryManager**), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="f5ea0-385">Essas consultas agregam subconsultas de vários componentes.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-385">These queries aggregate subqueries from multiple components.</span></span> <span data-ttu-id="f5ea0-386">Um deles é hello [repositório de integridade](service-fabric-health-introduction.md#health-store), que preenche Olá agregado estado de integridade para cada resultado da consulta.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-386">One of them is hello [health store](service-fabric-health-introduction.md#health-store), which populates hello aggregated health state for each query result.</span></span>  

> [!NOTE]
> <span data-ttu-id="f5ea0-387">Consultas gerais retornam Olá agregado estado de integridade da entidade hello e não contêm dados de integridade avançados.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-387">General queries return hello aggregated health state of hello entity and do not contain rich health data.</span></span> <span data-ttu-id="f5ea0-388">Se uma entidade não está íntegra, você pode acompanhar com integridade consultas tooget todas as suas informações de integridade, incluindo eventos, estados de integridade do filho e avaliações não íntegras.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-388">If an entity is not healthy, you can follow up with health queries tooget all its health information, including events, child health states, and unhealthy evaluations.</span></span>
>
>

<span data-ttu-id="f5ea0-389">Se consultas gerais retornam um estado de integridade desconhecido para uma entidade, é possível que repositório integridade Olá não tem dados completos sobre entidade hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-389">If general queries return an unknown health state for an entity, it's possible that hello health store doesn't have complete data about hello entity.</span></span> <span data-ttu-id="f5ea0-390">Também é possível que um repositório de integridade toohello subconsulta não foi bem-sucedida (por exemplo, ocorreu um erro de comunicação ou armazenamento de integridade Olá foi restringido).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-390">It's also possible that a subquery toohello health store wasn't successful (for example, there was a communication error, or hello health store was throttled).</span></span> <span data-ttu-id="f5ea0-391">O acompanhamento com uma consulta de integridade de entidade hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-391">Follow up with a health query for hello entity.</span></span> <span data-ttu-id="f5ea0-392">Se a subconsulta Olá encontrou erros transitórios, como problemas de rede, poderá ter êxito, esta consulta de acompanhamento.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-392">If hello subquery encountered transient errors, such as network issues, this follow-up query may succeed.</span></span> <span data-ttu-id="f5ea0-393">Ele pode também fornecer mais detalhes do repositório de integridade Olá sobre por que a entidade Olá não está exposta.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-393">It may also give you more details from hello health store about why hello entity is not exposed.</span></span>

<span data-ttu-id="f5ea0-394">Olá consultas que contêm **HealthState** para entidades são:</span><span class="sxs-lookup"><span data-stu-id="f5ea0-394">hello queries that contain **HealthState** for entities are:</span></span>

* <span data-ttu-id="f5ea0-395">Lista de nós: retorna nós de lista de Olá Olá cluster (via paginada).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-395">Node list: Returns hello list nodes in hello cluster (paged).</span></span>
  * <span data-ttu-id="f5ea0-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span><span class="sxs-lookup"><span data-stu-id="f5ea0-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span></span>
  * <span data-ttu-id="f5ea0-397">PowerShell: Get-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="f5ea0-397">PowerShell: Get-ServiceFabricNode</span></span>
* <span data-ttu-id="f5ea0-398">Lista de aplicativos: lista de saudação retorna de aplicativos em cluster hello (via paginada).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-398">Application list: Returns hello list of applications in hello cluster (paged).</span></span>
  * <span data-ttu-id="f5ea0-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="f5ea0-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span></span>
  * <span data-ttu-id="f5ea0-400">PowerShell: Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="f5ea0-400">PowerShell: Get-ServiceFabricApplication</span></span>
* <span data-ttu-id="f5ea0-401">Lista de serviços: lista de saudação do retorna de serviços em um aplicativo (via paginada).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-401">Service list: Returns hello list of services in an application (paged).</span></span>
  * <span data-ttu-id="f5ea0-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span><span class="sxs-lookup"><span data-stu-id="f5ea0-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span></span>
  * <span data-ttu-id="f5ea0-403">PowerShell: Get-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="f5ea0-403">PowerShell: Get-ServiceFabricService</span></span>
* <span data-ttu-id="f5ea0-404">Lista de partição: lista de saudação retorna de partições em um serviço (via paginada).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-404">Partition list: Returns hello list of partitions in a service (paged).</span></span>
  * <span data-ttu-id="f5ea0-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span><span class="sxs-lookup"><span data-stu-id="f5ea0-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span></span>
  * <span data-ttu-id="f5ea0-406">PowerShell: Get-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="f5ea0-406">PowerShell: Get-ServiceFabricPartition</span></span>
* <span data-ttu-id="f5ea0-407">Lista de réplica: lista de saudação retorna das réplicas de uma partição (via paginada).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-407">Replica list: Returns hello list of replicas in a partition (paged).</span></span>
  * <span data-ttu-id="f5ea0-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span><span class="sxs-lookup"><span data-stu-id="f5ea0-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span></span>
  * <span data-ttu-id="f5ea0-409">PowerShell: Get-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="f5ea0-409">PowerShell: Get-ServiceFabricReplica</span></span>
* <span data-ttu-id="f5ea0-410">Implantado a lista de aplicativos: lista de saudação retorna dos aplicativos implantados em um nó.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-410">Deployed application list: Returns hello list of deployed applications on a node.</span></span>
  * <span data-ttu-id="f5ea0-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="f5ea0-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span></span>
  * <span data-ttu-id="f5ea0-412">PowerShell: Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="f5ea0-412">PowerShell: Get-ServiceFabricDeployedApplication</span></span>
* <span data-ttu-id="f5ea0-413">Implantado a lista de pacotes de serviço: lista de saudação retorna de pacotes de serviço em um aplicativo implantado.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-413">Deployed service package list: Returns hello list of service packages in a deployed application.</span></span>
  * <span data-ttu-id="f5ea0-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span><span class="sxs-lookup"><span data-stu-id="f5ea0-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span></span>
  * <span data-ttu-id="f5ea0-415">PowerShell: Get-ServiceFabricDeployedApplication</span><span class="sxs-lookup"><span data-stu-id="f5ea0-415">PowerShell: Get-ServiceFabricDeployedApplication</span></span>

> [!NOTE]
> <span data-ttu-id="f5ea0-416">Algumas consultas Olá retornam resultados paginados.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-416">Some of hello queries return paged results.</span></span> <span data-ttu-id="f5ea0-417">retorno dessas consultas Hello é uma lista derivada [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-417">hello return of these queries is a list derived from [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span></span> <span data-ttu-id="f5ea0-418">Se os resultados de saudação não se ajustar a uma mensagem, apenas uma página será retornada e um ContinuationToken que controla qual enumeração foi interrompida.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-418">If hello results do not fit a message, only a page is returned and a ContinuationToken that tracks where enumeration stopped.</span></span> <span data-ttu-id="f5ea0-419">Continue toocall Olá mesma consulta e passar o token de continuação Olá Olá anterior tooget próximos de resultados da consulta.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-419">Continue toocall hello same query and pass in hello continuation token from hello previous query tooget next results.</span></span>
>
>

### <a name="examples"></a><span data-ttu-id="f5ea0-420">Exemplos</span><span class="sxs-lookup"><span data-stu-id="f5ea0-420">Examples</span></span>
<span data-ttu-id="f5ea0-421">Olá código a seguir obtém aplicativos problemáticos Olá no cluster hello:</span><span class="sxs-lookup"><span data-stu-id="f5ea0-421">hello following code gets hello unhealthy applications in hello cluster:</span></span>

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

<span data-ttu-id="f5ea0-422">Hello seguir obtém os detalhes do aplicativo hello para a malha de saudação: / aplicativo WordCount.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-422">hello following cmdlet gets hello application details for hello fabric:/WordCount application.</span></span> <span data-ttu-id="f5ea0-423">Observe que o estado de integridade é de aviso.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-423">Notice that health state is at warning.</span></span>

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

<span data-ttu-id="f5ea0-424">Olá, cmdlet a seguir obtém Olá serviços com um estado de integridade de erro:</span><span class="sxs-lookup"><span data-stu-id="f5ea0-424">hello following cmdlet gets hello services with a health state of error:</span></span>

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

## <a name="cluster-and-application-upgrades"></a><span data-ttu-id="f5ea0-425">Atualização de cluster e aplicativo</span><span class="sxs-lookup"><span data-stu-id="f5ea0-425">Cluster and application upgrades</span></span>
<span data-ttu-id="f5ea0-426">Durante uma atualização monitorada do cluster hello e do aplicativo, o Service Fabric verifica tooensure de integridade que tudo permaneça íntegro.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-426">During a monitored upgrade of hello cluster and application, Service Fabric checks health tooensure that everything remains healthy.</span></span> <span data-ttu-id="f5ea0-427">Se uma entidade não está íntegra, conforme avaliado usando políticas de integridade configurado, o upgrade Olá aplica próxima ação do políticas específicas de atualização toodetermine hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-427">If an entity is unhealthy as evaluated by using configured health policies, hello upgrade applies upgrade-specific policies toodetermine hello next action.</span></span> <span data-ttu-id="f5ea0-428">atualização Olá pode ser pausado tooallow interação do usuário (como corrigir as condições de erro ou alteração de políticas), ou ele pode automaticamente reverter toohello versão anterior de BOM.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-428">hello upgrade may be paused tooallow user interaction (such as fixing error conditions or changing policies), or it may automatically roll back toohello previous good version.</span></span>

<span data-ttu-id="f5ea0-429">Durante uma *cluster* atualização, você pode obter o status de atualização de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-429">During a *cluster* upgrade, you can get hello cluster upgrade status.</span></span> <span data-ttu-id="f5ea0-430">status de atualização de saudação inclui avaliações não íntegras, quais toowhat ponto não está íntegro no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-430">hello upgrade status includes unhealthy evaluations, which point toowhat is unhealthy in hello cluster.</span></span> <span data-ttu-id="f5ea0-431">Se Olá atualização é revertida devido a problemas de toohealth, status da atualização Olá lembra motivos não íntegro do último hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-431">If hello upgrade is rolled back due toohealth issues, hello upgrade status remembers hello last unhealthy reasons.</span></span> <span data-ttu-id="f5ea0-432">Essas informações podem ajudar os administradores a investigar o que deu errado atualização Olá revertida ou interrompido.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-432">This information can help administrators investigate what went wrong after hello upgrade rolled back or stopped.</span></span>

<span data-ttu-id="f5ea0-433">Da mesma forma, durante um *aplicativo* atualização, qualquer avaliações não íntegras estão contidas no status de atualização de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-433">Similarly, during an *application* upgrade, any unhealthy evaluations are contained in hello application upgrade status.</span></span>

<span data-ttu-id="f5ea0-434">Hello a seguir mostra o status de atualização de aplicativo do Olá para uma malha modificada: / aplicativo WordCount.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-434">hello following shows hello application upgrade status for a modified fabric:/WordCount application.</span></span> <span data-ttu-id="f5ea0-435">Um watchdog relatou um erro em uma de suas réplicas.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-435">A watchdog reported an error on one of its replicas.</span></span> <span data-ttu-id="f5ea0-436">atualização de Hello está sendo porque as verificações de integridade de saudação não for respeitadas.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-436">hello upgrade is rolling back because hello health checks are not respected.</span></span>

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

<span data-ttu-id="f5ea0-437">Leia mais sobre Olá [atualização do aplicativo do Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="f5ea0-437">Read more about hello [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="use-health-evaluations-tootroubleshoot"></a><span data-ttu-id="f5ea0-438">Usar tootroubleshoot de avaliações de integridade</span><span class="sxs-lookup"><span data-stu-id="f5ea0-438">Use health evaluations tootroubleshoot</span></span>
<span data-ttu-id="f5ea0-439">Sempre que houver um problema com o cluster de saudação ou um aplicativo, examine Olá toopinpoint de integridade de cluster ou o aplicativo que está errado.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-439">Whenever there is an issue with hello cluster or an application, look at hello cluster or application health toopinpoint what is wrong.</span></span> <span data-ttu-id="f5ea0-440">avaliações não íntegras Olá fornecem detalhes sobre Olá disparada atual estado não íntegro.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-440">hello unhealthy evaluations provide details about what triggered hello current unhealthy state.</span></span> <span data-ttu-id="f5ea0-441">Se você precisar, você pode fazer drill down em filho não íntegros entidades tooidentify Olá causas.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-441">If you need to, you can drill down into unhealthy child entities tooidentify hello root cause.</span></span>

<span data-ttu-id="f5ea0-442">Por exemplo, pense em um aplicativo não íntegro porque há um relatório de erros em uma de suas réplicas.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-442">For example, consider an application unhealthy because there is an error report on one of its replicas.</span></span> <span data-ttu-id="f5ea0-443">Olá seguinte cmdlet do Powershell mostra avaliações não íntegras hello:</span><span class="sxs-lookup"><span data-stu-id="f5ea0-443">hello following Powershell cmdlet shows hello unhealthy evaluations:</span></span>

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

<span data-ttu-id="f5ea0-444">Você pode examinar Olá réplica tooget obter mais informações:</span><span class="sxs-lookup"><span data-stu-id="f5ea0-444">You can look at hello replica tooget more information:</span></span>

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
> <span data-ttu-id="f5ea0-445">Olá, avaliações não íntegras Mostrar Olá primeiro motivo Olá entidade é avaliado toocurrent estado de integridade.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-445">hello unhealthy evaluations show hello first reason hello entity is evaluated toocurrent health state.</span></span> <span data-ttu-id="f5ea0-446">Pode haver vários outros eventos que disparam esse estado, mas elas não são refletidas em avaliações de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-446">There may be multiple other events that trigger this state, but they are not be reflected in hello evaluations.</span></span> <span data-ttu-id="f5ea0-447">tooget obter mais informações, busca detalhada toofigure de entidades de integridade Olá todos os relatórios de não-íntegro Olá cluster hello.</span><span class="sxs-lookup"><span data-stu-id="f5ea0-447">tooget more information, drill down into hello health entities toofigure out all hello unhealthy reports in hello cluster.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="f5ea0-448">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f5ea0-448">Next steps</span></span>
[<span data-ttu-id="f5ea0-449">Usar tootroubleshoot de relatórios de integridade do sistema</span><span class="sxs-lookup"><span data-stu-id="f5ea0-449">Use system health reports tootroubleshoot</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[<span data-ttu-id="f5ea0-450">Adicionar relatórios de integridade personalizados do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f5ea0-450">Add custom Service Fabric health reports</span></span>](service-fabric-report-health.md)

[<span data-ttu-id="f5ea0-451">Como tooreport e verificação de integridade do serviço</span><span class="sxs-lookup"><span data-stu-id="f5ea0-451">How tooreport and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="f5ea0-452">Monitorar e diagnosticar serviços localmente</span><span class="sxs-lookup"><span data-stu-id="f5ea0-452">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="f5ea0-453">Atualização de aplicativos do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f5ea0-453">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
