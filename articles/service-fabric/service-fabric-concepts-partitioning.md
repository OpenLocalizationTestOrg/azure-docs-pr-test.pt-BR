---
title: "os serviços do Service Fabric aaaPartitioning | Microsoft Docs"
description: "Descreve como os serviços com monitoração de estado toopartition Service Fabric. Partições permite o armazenamento de dados em máquinas locais Olá para que dados e computação podem ser dimensionados em conjunto."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 3b7248c8-ea92-4964-85e7-6f1291b5cc7b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: msfussell
ms.openlocfilehash: 6ead48716c08f4212535202ee69d169067d5c6d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="partition-service-fabric-reliable-services"></a><span data-ttu-id="4d1cd-104">Particionar Reliable Services do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4d1cd-104">Partition Service Fabric reliable services</span></span>
<span data-ttu-id="4d1cd-105">Este artigo fornece uma introdução toohello conceitos básicos de particionamento serviços confiáveis do Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-105">This article provides an introduction toohello basic concepts of partitioning Azure Service Fabric reliable services.</span></span> <span data-ttu-id="4d1cd-106">Olá código-fonte usado no artigo Olá também está disponível em [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span><span class="sxs-lookup"><span data-stu-id="4d1cd-106">hello source code used in hello article is also available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="partitioning"></a><span data-ttu-id="4d1cd-107">Particionamento</span><span class="sxs-lookup"><span data-stu-id="4d1cd-107">Partitioning</span></span>
<span data-ttu-id="4d1cd-108">O particionamento não é exclusivo tooService malha.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-108">Partitioning is not unique tooService Fabric.</span></span> <span data-ttu-id="4d1cd-109">Na verdade, é um padrão núcleo da criação de serviços escalonáveis.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-109">In fact, it is a core pattern of building scalable services.</span></span> <span data-ttu-id="4d1cd-110">Em um sentido mais amplo, podemos pensar em particionamento como um conceito de divisão do estado (dados) e de computação de desempenho e escalabilidade de tooimprove acessível unidades menor.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-110">In a broader sense, we can think about partitioning as a concept of dividing state (data) and compute into smaller accessible units tooimprove scalability and performance.</span></span> <span data-ttu-id="4d1cd-111">Uma forma bem conhecida de particionamento é o [particionamento de dados][wikipartition], também conhecido como fragmentação.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-111">A well-known form of partitioning is [data partitioning][wikipartition], also known as sharding.</span></span>

### <a name="partition-service-fabric-stateless-services"></a><span data-ttu-id="4d1cd-112">Particionar serviços sem estado do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4d1cd-112">Partition Service Fabric stateless services</span></span>
<span data-ttu-id="4d1cd-113">Para serviços sem estado, você pode pensar em uma partição como uma unidade lógica que contém uma ou mais instâncias de um serviço.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-113">For stateless services, you can think about a partition being a logical unit that contains one or more instances of a service.</span></span> <span data-ttu-id="4d1cd-114">A Figura 1 mostra um serviço sem estado com cinco instâncias distribuídas em um cluster usando uma partição.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-114">Figure 1 shows a stateless service with five instances distributed across a cluster using one partition.</span></span>

![Serviço sem estado](./media/service-fabric-concepts-partitioning/statelessinstances.png)

<span data-ttu-id="4d1cd-116">Há realmente dois tipos de soluções de serviço sem estado.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-116">There are really two types of stateless service solutions.</span></span> <span data-ttu-id="4d1cd-117">Hello primeiro um é um serviço que mantém seu estado externamente, por exemplo em um banco de dados do SQL Azure (como um site que armazena dados e informações de sessão Olá).</span><span class="sxs-lookup"><span data-stu-id="4d1cd-117">hello first one is a service that persists its state externally, for example in an Azure SQL database (like a website that stores hello session information and data).</span></span> <span data-ttu-id="4d1cd-118">Olá, um segundo é somente para computação serviços (como miniaturas uma calculadora ou imagem) que não gerencia qualquer estado persistente.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-118">hello second one is computation-only services (like a calculator or image thumbnailing) that do not manage any persistent state.</span></span>

<span data-ttu-id="4d1cd-119">Em ambos os casos o particionamento de um serviço sem estado é um cenário muito raro – a escalabilidade e disponibilidade normalmente são obtidas pela adição de mais instâncias.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-119">In either case, partitioning a stateless service is a very rare scenario--scalability and availability are normally achieved by adding more instances.</span></span> <span data-ttu-id="4d1cd-120">Olá somente tempo tooconsider várias partições para instâncias de serviço sem monitoração de estado é quando você precisa do roteamento especial do toomeet solicitações.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-120">hello only time you want tooconsider multiple partitions for stateless service instances is when you need toomeet special routing requests.</span></span>

<span data-ttu-id="4d1cd-121">Por exemplo, considere um caso em que os usuários com IDs de um determinado intervalo só devem ser atendidos por uma instância de determinado serviço.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-121">As an example, consider a case where users with IDs in a certain range should only be served by a particular service instance.</span></span> <span data-ttu-id="4d1cd-122">Outro exemplo de quando é possível particionar um serviço sem monitoração de estado é quando você tiver um back-end realmente particionado (por exemplo, um SQL banco de dados fragmentado) e você deseja toocontrol qual instância de serviço deve gravar toohello fragmentos do banco de dados – ou realizar outro trabalho de preparação em Olá serviço sem monitoração de estado que exige Olá mesmo informações de particionamento como é usado em Olá back-end.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-122">Another example of when you could partition a stateless service is when you have a truly partitioned backend (e.g. a sharded SQL database) and you want toocontrol which service instance should write toohello database shard--or perform other preparation work within hello stateless service that requires hello same partitioning information as is used in hello backend.</span></span> <span data-ttu-id="4d1cd-123">Esses tipos de cenários também podem ser resolvidos de diferentes maneiras e não exigem, necessariamente, particionamento de serviço.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-123">Those types of scenarios can also be solved in different ways and do not necessarily require service partitioning.</span></span>

<span data-ttu-id="4d1cd-124">Olá restante deste passo a passo se concentra nos serviços de monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-124">hello remainder of this walkthrough focuses on stateful services.</span></span>

### <a name="partition-service-fabric-stateful-services"></a><span data-ttu-id="4d1cd-125">Particionar serviços com estado do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4d1cd-125">Partition Service Fabric stateful services</span></span>
<span data-ttu-id="4d1cd-126">Service Fabric torna fácil toodevelop serviços escalonáveis de monitoração de estado, oferecendo uma maneira de primeira classe toopartition estado (dados).</span><span class="sxs-lookup"><span data-stu-id="4d1cd-126">Service Fabric makes it easy toodevelop scalable stateful services by offering a first-class way toopartition state (data).</span></span> <span data-ttu-id="4d1cd-127">Conceitualmente, você pode pensar em uma partição de um serviço com monitoração de estado como uma unidade de escala que é altamente confiável por meio de [réplicas](service-fabric-availability-services.md) que são distribuídos e equilibrada em Olá nós em um cluster.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-127">Conceptually, you can think about a partition of a stateful service as a scale unit that is highly reliable through [replicas](service-fabric-availability-services.md) that are distributed and balanced across hello nodes in a cluster.</span></span>

<span data-ttu-id="4d1cd-128">No contexto de saudação do serviços de malha do serviço com monitoração de estado refere-se toohello o processo de determinar que uma partição de serviço é responsável por uma parte do estado de conclusão Olá do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-128">Partitioning in hello context of Service Fabric stateful services refers toohello process of determining that a particular service partition is responsible for a portion of hello complete state of hello service.</span></span> <span data-ttu-id="4d1cd-129">(Conforme mencionado anteriormente, uma partição é um conjunto de [réplicas](service-fabric-availability-services.md)).</span><span class="sxs-lookup"><span data-stu-id="4d1cd-129">(As mentioned before, a partition is a set of [replicas](service-fabric-availability-services.md)).</span></span> <span data-ttu-id="4d1cd-130">Uma grande vantagem do Service Fabric é que ele coloca partições Olá em nós diferentes.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-130">A great thing about Service Fabric is that it places hello partitions on different nodes.</span></span> <span data-ttu-id="4d1cd-131">Isso permite que o limite de recurso do nó de tooa toogrow.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-131">This allows them toogrow tooa node's resource limit.</span></span> <span data-ttu-id="4d1cd-132">Como dados saudação crescer, aumento de partições e do Service Fabric redistribui partições em nós.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-132">As hello data needs grow, partitions grow, and Service Fabric rebalances partitions across nodes.</span></span> <span data-ttu-id="4d1cd-133">Isso garante a saudação continuação uso eficiente dos recursos de hardware.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-133">This ensures hello continued efficient use of hardware resources.</span></span>

<span data-ttu-id="4d1cd-134">toogive você, por exemplo, digamos que você comece com um cluster de nó 5 e um serviço que é configurado toohave 10 partições e um destino de três réplicas.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-134">toogive you an example, say you start with a 5-node cluster and a service that is configured toohave 10 partitions and a target of three replicas.</span></span> <span data-ttu-id="4d1cd-135">Nesse caso, Service Fabric deve equilibrar e distribuir réplicas Olá em cluster hello – e acabar com dois [réplicas](service-fabric-availability-services.md) por nó.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-135">In this case, Service Fabric would balance and distribute hello replicas across hello cluster--and you would end up with two primary [replicas](service-fabric-availability-services.md) per node.</span></span>
<span data-ttu-id="4d1cd-136">Se você precisar agora tooscale nós de too10 cluster hello, Service Fabric seria reequilibrar Olá primário [réplicas](service-fabric-availability-services.md) em todos os nós de 10.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-136">If you now need tooscale out hello cluster too10 nodes, Service Fabric would rebalance hello primary [replicas](service-fabric-availability-services.md) across all 10 nodes.</span></span> <span data-ttu-id="4d1cd-137">Da mesma forma, se você voltar too5 nós em escala, Service Fabric seria reequilibrar todas as réplicas de saudação em nós Olá 5.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-137">Likewise, if you scaled back too5 nodes, Service Fabric would rebalance all hello replicas across hello 5 nodes.</span></span>  

<span data-ttu-id="4d1cd-138">Figura 2 mostra a distribuição de saudação de 10 partições antes e depois de dimensionamento do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-138">Figure 2 shows hello distribution of 10 partitions before and after scaling hello cluster.</span></span>

![Serviço com estado](./media/service-fabric-concepts-partitioning/partitions.png)

<span data-ttu-id="4d1cd-140">Como resultado, Olá expansão é obtido desde que as solicitações de clientes são distribuídas entre computadores, é melhor desempenho geral do aplicativo hello e contenção no toochunks de acesso de dados é reduzida.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-140">As a result, hello scale-out is achieved since requests from clients are distributed across computers, overall performance of hello application is improved, and contention on access toochunks of data is reduced.</span></span>

## <a name="plan-for-partitioning"></a><span data-ttu-id="4d1cd-141">Plano de particionamento</span><span class="sxs-lookup"><span data-stu-id="4d1cd-141">Plan for partitioning</span></span>
<span data-ttu-id="4d1cd-142">Antes de implementar um serviço, você deve sempre considerar Olá estratégia é necessário tooscale-out de particionamento. Há maneiras diferentes, mas todos eles se concentrar no que aplicativo hello precisa tooachieve.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-142">Before implementing a service, you should always consider hello partitioning strategy that is required tooscale out. There are different ways, but all of them focus on what hello application needs tooachieve.</span></span> <span data-ttu-id="4d1cd-143">Contexto Olá neste artigo, vamos considerar alguns Olá aspectos mais importantes.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-143">For hello context of this article, let's consider some of hello more important aspects.</span></span>

<span data-ttu-id="4d1cd-144">Uma boa abordagem é toothink sobre estrutura de saudação do estado de saudação que precisa toobe particionada, como primeira etapa de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-144">A good approach is toothink about hello structure of hello state that needs toobe partitioned, as hello first step.</span></span>

<span data-ttu-id="4d1cd-145">Veja abaixo um exemplo simples</span><span class="sxs-lookup"><span data-stu-id="4d1cd-145">Let's take a simple example.</span></span> <span data-ttu-id="4d1cd-146">Se você fosse toobuild um serviço para uma pesquisa countywide, você pode criar uma partição de cada cidade no município de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-146">If you were toobuild a service for a countywide poll, you could create a partition for each city in hello county.</span></span> <span data-ttu-id="4d1cd-147">Em seguida, você pode armazenar Olá votos para cada pessoa cidade Olá na partição de saudação corresponde toothat cidade.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-147">Then, you could store hello votes for every person in hello city in hello partition that corresponds toothat city.</span></span> <span data-ttu-id="4d1cd-148">A Figura 3 ilustra um conjunto de pessoas e hello cidade em que eles residem.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-148">Figure 3 illustrates a set of people and hello city in which they reside.</span></span>

![Partição simples](./media/service-fabric-concepts-partitioning/cities.png)

<span data-ttu-id="4d1cd-150">Como a população de saudação de cidades varia muito, você pode acabar com algumas partições que contêm muitos dados (por exemplo, Seattle) e outras partições com muito pouco estado (por exemplo, Kirkland).</span><span class="sxs-lookup"><span data-stu-id="4d1cd-150">As hello population of cities varies widely, you may end up with some partitions that contain a lot of data (e.g. Seattle) and other partitions with very little state (e.g. Kirkland).</span></span> <span data-ttu-id="4d1cd-151">Então, qual é o impacto de saudação de partições com quantidades irregulares de estado?</span><span class="sxs-lookup"><span data-stu-id="4d1cd-151">So what is hello impact of having partitions with uneven amounts of state?</span></span>

<span data-ttu-id="4d1cd-152">Se você pensar sobre o exemplo hello novamente, você pode ver facilmente que partição Olá que contém a saudação votos para Seattle obterão mais tráfego que Kirkland Olá um.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-152">If you think about hello example again, you can easily see that hello partition that holds hello votes for Seattle will get more traffic than hello Kirkland one.</span></span> <span data-ttu-id="4d1cd-153">Por padrão, o Service Fabric torna-se de que há sobre Olá mesmo número de réplicas primárias e secundárias em cada nó.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-153">By default, Service Fabric makes sure that there is about hello same number of primary and secondary replicas on each node.</span></span> <span data-ttu-id="4d1cd-154">Assim, você pode acabar com nós que hospedam réplicas que atendem a mais tráfego e outras que atendem a menos tráfego.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-154">So you may end up with nodes that hold replicas that serve more traffic and others that serve less traffic.</span></span> <span data-ttu-id="4d1cd-155">Preferencialmente deseje tooavoid ativa e frios pontos como isso em um cluster.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-155">You would preferably want tooavoid hot and cold spots like this in a cluster.</span></span>

<span data-ttu-id="4d1cd-156">Em ordem tooavoid isso, você deve fazer duas coisas, de um ponto de vista particionamento:</span><span class="sxs-lookup"><span data-stu-id="4d1cd-156">In order tooavoid this, you should do two things, from a partitioning point of view:</span></span>

* <span data-ttu-id="4d1cd-157">Tente o estado de saudação toopartition para que ele é distribuído uniformemente entre todas as partições.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-157">Try toopartition hello state so that it is evenly distributed across all partitions.</span></span>
* <span data-ttu-id="4d1cd-158">Relatório de carga de cada uma das réplicas Olá para o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-158">Report load from each of hello replicas for hello service.</span></span> <span data-ttu-id="4d1cd-159">(Para obter informações sobre como fazer isso, leia este artigo sobre [métricas e carga](service-fabric-cluster-resource-manager-metrics.md)).</span><span class="sxs-lookup"><span data-stu-id="4d1cd-159">(For information on how, check out this article on [Metrics and Load](service-fabric-cluster-resource-manager-metrics.md)).</span></span> <span data-ttu-id="4d1cd-160">Malha do serviço fornecem a carga de tooreport de recurso Olá consumida por serviços, como a quantidade de memória ou o número de registros.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-160">Service Fabric provides hello capability tooreport load consumed by services, such as amount of memory or number of records.</span></span> <span data-ttu-id="4d1cd-161">Com base nas métricas de saudação relatadas, o Service Fabric detecta que algumas partições estão servindo cargas mais altas que outros e redistribui cluster Olá pela movimentação réplicas toomore adequado nós, para que geral nenhum nó está sobrecarregado.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-161">Based on hello metrics reported, Service Fabric detects that some partitions are serving higher loads than others and rebalances hello cluster by moving replicas toomore suitable nodes, so that overall no node is overloaded.</span></span>

<span data-ttu-id="4d1cd-162">Às vezes, você não tem como saber quantos dados haverá em uma determinada partição.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-162">Sometimes, you cannot know how much data will be in a given partition.</span></span> <span data-ttu-id="4d1cd-163">Uma recomendação geral é toodo ambos – primeiro, adotando uma estratégia de particionamento que se espalha dados saudação uniformemente entre partições hello e, segundo, pelo relatório de carga.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-163">So a general recommendation is toodo both--first, by adopting a partitioning strategy that spreads hello data evenly across hello partitions and second, by reporting load.</span></span>  <span data-ttu-id="4d1cd-164">método primeiro Hello impede situações descritas no hello votação de exemplo, enquanto Olá segundo ajuda a suavizar temporárias diferenças no access ou carga ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-164">hello first method prevents situations described in hello voting example, while hello second helps smooth out temporary differences in access or load over time.</span></span>

<span data-ttu-id="4d1cd-165">Outro aspecto do planejamento de partição é número correto de saudação de toochoose de toobegin de partições com.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-165">Another aspect of partition planning is toochoose hello correct number of partitions toobegin with.</span></span>
<span data-ttu-id="4d1cd-166">Do ponto de vista do Service Fabric, não há nada que impeça começar com um número de partições maior do o previsto para o cenário.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-166">From a Service Fabric perspective, there is nothing that prevents you from starting out with a higher number of partitions than anticipated for your scenario.</span></span>
<span data-ttu-id="4d1cd-167">Na verdade, supondo que o número máximo de saudação de partições é uma abordagem válida.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-167">In fact, assuming hello maximum number of partitions is a valid approach.</span></span>

<span data-ttu-id="4d1cd-168">Em casos raros, você acabará precisando de mais partições do que escolheu inicialmente.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-168">In rare cases, you may end up needing more partitions than you have initially chosen.</span></span> <span data-ttu-id="4d1cd-169">Como você não pode alterar a contagem de partição Olá após o fato de hello, você precisaria tooapply algumas abordagens de partição avançadas, como criar uma nova instância de serviço da saudação mesmo tipo de serviço.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-169">As you cannot change hello partition count after hello fact, you would need tooapply some advanced partition approaches, such as creating a new service instance of hello same service type.</span></span> <span data-ttu-id="4d1cd-170">Também é necessário tooimplement alguma lógica do lado do cliente que roteia Olá solicitações toohello instância de serviço correto, com base no conhecimento do lado do cliente que deve manter o código do cliente.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-170">You would also need tooimplement some client-side logic that routes hello requests toohello correct service instance, based on client-side knowledge that your client code must maintain.</span></span>

<span data-ttu-id="4d1cd-171">Outra consideração de planejamento de particionamento é recursos de computação disponíveis hello.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-171">Another consideration for partitioning planning is hello available computer resources.</span></span> <span data-ttu-id="4d1cd-172">Como estado de saudação precisa toobe acessados e armazenados, você está toofollow associada:</span><span class="sxs-lookup"><span data-stu-id="4d1cd-172">As hello state needs toobe accessed and stored, you are bound toofollow:</span></span>

* <span data-ttu-id="4d1cd-173">Limites de largura de banda de rede</span><span class="sxs-lookup"><span data-stu-id="4d1cd-173">Network bandwidth limits</span></span>
* <span data-ttu-id="4d1cd-174">Limites de memória do sistema</span><span class="sxs-lookup"><span data-stu-id="4d1cd-174">System memory limits</span></span>
* <span data-ttu-id="4d1cd-175">Limites de armazenamento de disco</span><span class="sxs-lookup"><span data-stu-id="4d1cd-175">Disk storage limits</span></span>

<span data-ttu-id="4d1cd-176">O que acontece se você tiver restrições de recursos em um cluster em execução? resposta de saudação é que você pode expandir simplesmente Olá cluster tooaccommodate Olá novos requisitos.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-176">So what happens if you run into resource constraints in a running cluster? hello answer is that you can simply scale out hello cluster tooaccommodate hello new requirements.</span></span>

<span data-ttu-id="4d1cd-177">[Guia de planejamento de capacidade de saudação](service-fabric-capacity-planning.md) oferece orientação sobre como toodetermine quantos nós de cluster precisa.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-177">[hello capacity planning guide](service-fabric-capacity-planning.md) offers guidance for how toodetermine how many nodes your cluster needs.</span></span>

## <a name="get-started-with-partitioning"></a><span data-ttu-id="4d1cd-178">Introdução ao particionamento</span><span class="sxs-lookup"><span data-stu-id="4d1cd-178">Get started with partitioning</span></span>
<span data-ttu-id="4d1cd-179">Esta seção descreve como tooget iniciada com o particionamento de seu serviço.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-179">This section describes how tooget started with partitioning your service.</span></span>

<span data-ttu-id="4d1cd-180">O Service Fabric oferece uma variedade de três esquemas de partição:</span><span class="sxs-lookup"><span data-stu-id="4d1cd-180">Service Fabric offers a choice of three partition schemes:</span></span>

* <span data-ttu-id="4d1cd-181">Intervalo de particionamento (também conhecido como UniformInt64Partition).</span><span class="sxs-lookup"><span data-stu-id="4d1cd-181">Ranged partitioning (otherwise known as UniformInt64Partition).</span></span>
* <span data-ttu-id="4d1cd-182">Particionamento nomeado.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-182">Named partitioning.</span></span> <span data-ttu-id="4d1cd-183">Aplicativos que usam esse modelo geralmente têm dados em bucket, dentro de um conjunto limitado.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-183">Applications using this model usually have data that can be bucketed, within a bounded set.</span></span> <span data-ttu-id="4d1cd-184">Alguns exemplos comuns de campos de dados usados como chaves de partição nomeada seriam regiões, códigos postais, grupos de clientes ou outros limites de negócios.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-184">Some common examples of data fields used as named partition keys would be regions, postal codes, customer groups, or other business boundaries.</span></span>
* <span data-ttu-id="4d1cd-185">Particionamento de singleton.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-185">Singleton partitioning.</span></span> <span data-ttu-id="4d1cd-186">Partições de singleton normalmente são usadas quando o serviço Olá não requer qualquer roteamento adicional.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-186">Singleton partitions are typically used when hello service does not require any additional routing.</span></span> <span data-ttu-id="4d1cd-187">Por exemplo, serviços sem estado usam esse esquema de particionamento por padrão.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-187">For example, stateless services use this partitioning scheme by default.</span></span>

<span data-ttu-id="4d1cd-188">Os esquemas de particionamento Singleton e Nomeado são formulários especiais de partições de intervalos.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-188">Named and Singleton partitioning schemes are special forms of ranged partitions.</span></span> <span data-ttu-id="4d1cd-189">Por padrão, modelos do Visual Studio Olá para uso do Service Fabric alcance particionamento, conforme é Olá um mais comuns e úteis.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-189">By default, hello Visual Studio templates for Service Fabric use ranged partitioning, as it is hello most common and useful one.</span></span> <span data-ttu-id="4d1cd-190">Olá restante deste artigo se concentra no esquema de particionamento intervalos hello.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-190">hello remainder of this article focuses on hello ranged partitioning scheme.</span></span>

### <a name="ranged-partitioning-scheme"></a><span data-ttu-id="4d1cd-191">Esquema de particionamento por intervalos</span><span class="sxs-lookup"><span data-stu-id="4d1cd-191">Ranged partitioning scheme</span></span>
<span data-ttu-id="4d1cd-192">Isso é usado toospecify um número inteiro (identificadas por uma chave baixa e alta chave) de intervalo e um número de partições (n).</span><span class="sxs-lookup"><span data-stu-id="4d1cd-192">This is used toospecify an integer range (identified by a low key and high key) and a number of partitions (n).</span></span> <span data-ttu-id="4d1cd-193">Ele cria partições n, cada responsáveis por um subintervalo sem sobreposição de saudação geral de intervalo de chave de partição.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-193">It creates n partitions, each responsible for a non-overlapping subrange of hello overall partition key range.</span></span> <span data-ttu-id="4d1cd-194">Por exemplo, um esquema de particionamento por intervalos com uma chave baixa de 0, uma chave de alta de 99 e uma contagem de 4 criaria quatro partições, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-194">For example, a ranged partitioning scheme with a low key of 0, a high key of 99, and a count of 4 would create four partitions, as shown below.</span></span>

![Particionamento por intervalos](./media/service-fabric-concepts-partitioning/range-partitioning.png)

<span data-ttu-id="4d1cd-196">Uma abordagem comum é toocreate um hash com base em uma chave exclusiva no conjunto de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-196">A common approach is toocreate a hash based on a unique key within hello data set.</span></span> <span data-ttu-id="4d1cd-197">Alguns exemplos comuns de chaves seriam um número de identificação de veículo (VIN), uma ID de funcionário ou uma cadeia de caracteres exclusiva.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-197">Some common examples of keys would be a vehicle identification number (VIN), an employee ID, or a unique string.</span></span> <span data-ttu-id="4d1cd-198">Usando essa chave exclusiva, você poderia, em seguida, gerar um código hash, o intervalo de chave de saudação do módulo, toouse como sua chave.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-198">By using this unique key, you would then generate a hash code, modulus hello key range, toouse as your key.</span></span> <span data-ttu-id="4d1cd-199">Você pode especificar hello superior e limites inferiores da saudação chave intervalo permitido.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-199">You can specify hello upper and lower bounds of hello allowed key range.</span></span>

### <a name="select-a-hash-algorithm"></a><span data-ttu-id="4d1cd-200">Selecionar um algoritmo de hash</span><span class="sxs-lookup"><span data-stu-id="4d1cd-200">Select a hash algorithm</span></span>
<span data-ttu-id="4d1cd-201">Uma parte importante de hash é selecionar o algoritmo de hash.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-201">An important part of hashing is selecting your hash algorithm.</span></span> <span data-ttu-id="4d1cd-202">Uma consideração é se o objetivo de saudação é chaves semelhante de toogroup próximos um do outro (hash confidenciais localidade) – ou se a atividade deve ser distribuída em larga escala em todas as partições (hash de distribuição), que é mais comum.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-202">A consideration is whether hello goal is toogroup similar keys near each other (locality sensitive hashing)--or if activity should be distributed broadly across all partitions (distribution hashing), which is more common.</span></span>

<span data-ttu-id="4d1cd-203">características de saudação de um algoritmo de hash de distribuição BOM são que é fácil toocompute, ele tem poucos conflitos e distribui chaves Olá uniformemente.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-203">hello characteristics of a good distribution hashing algorithm are that it is easy toocompute, it has few collisions, and it distributes hello keys evenly.</span></span> <span data-ttu-id="4d1cd-204">Um bom exemplo de um algoritmo de hash eficiente é hello [FNV 1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) algoritmo de hash.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-204">A good example of an efficient hash algorithm is hello [FNV-1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) hash algorithm.</span></span>

<span data-ttu-id="4d1cd-205">Um bom recurso para obter opções de algoritmo hash geral código é hello [página da Wikipédia sobre funções de hash](http://en.wikipedia.org/wiki/Hash_function).</span><span class="sxs-lookup"><span data-stu-id="4d1cd-205">A good resource for general hash code algorithm choices is hello [Wikipedia page on hash functions](http://en.wikipedia.org/wiki/Hash_function).</span></span>

## <a name="build-a-stateful-service-with-multiple-partitions"></a><span data-ttu-id="4d1cd-206">Criar um serviço com estado com várias partições</span><span class="sxs-lookup"><span data-stu-id="4d1cd-206">Build a stateful service with multiple partitions</span></span>
<span data-ttu-id="4d1cd-207">Vamos criar seu primeiro serviço com estado confiável com várias partições.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-207">Let's create your first reliable stateful service with multiple partitions.</span></span> <span data-ttu-id="4d1cd-208">Neste exemplo, você criará um aplicativo muito simples, onde você deseja toostore todos os sobrenomes que começam com hello mesmo letra no hello mesma partição.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-208">In this example, you will build a very simple application where you want toostore all last names that start with hello same letter in hello same partition.</span></span>

<span data-ttu-id="4d1cd-209">Antes de gravar qualquer código, você precisa toothink sobre partições hello e chaves de partição.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-209">Before you write any code, you need toothink about hello partitions and partition keys.</span></span> <span data-ttu-id="4d1cd-210">Você precisa 26 partições (uma para cada letra no alfabeto Olá), mas e sobre Olá chaves baixa e alta?</span><span class="sxs-lookup"><span data-stu-id="4d1cd-210">You need 26 partitions (one for each letter in hello alphabet), but what about hello low and high keys?</span></span>
<span data-ttu-id="4d1cd-211">Como desejamos literalmente toohave uma partição por letra, podemos usar 0 como chave baixa hello e 25 como chave de alta hello, como cada letra é sua própria chave.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-211">As we literally want toohave one partition per letter, we can use 0 as hello low key and 25 as hello high key, as each letter is its own key.</span></span>

> [!NOTE]
> <span data-ttu-id="4d1cd-212">Este é um cenário simplificado, como na realidade distribuição Olá seria irregular.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-212">This is a simplified scenario, as in reality hello distribution would be uneven.</span></span> <span data-ttu-id="4d1cd-213">Último nomes que começam com letras hello "S" ou "M" são mais comuns que Olá aqueles começando com "X" ou "Y".</span><span class="sxs-lookup"><span data-stu-id="4d1cd-213">Last names starting with hello letters "S" or "M" are more common than hello ones starting with "X" or "Y".</span></span>
> 
> 

1. <span data-ttu-id="4d1cd-214">Abra **Visual Studio** > **Arquivo** > **Novo** > **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-214">Open **Visual Studio** > **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="4d1cd-215">Em Olá **novo projeto** caixa de diálogo caixa, escolha o aplicativo de serviço de malha hello.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-215">In hello **New Project** dialog box, choose hello Service Fabric application.</span></span>
3. <span data-ttu-id="4d1cd-216">Chame projeto hello "AlphabetPartitions".</span><span class="sxs-lookup"><span data-stu-id="4d1cd-216">Call hello project "AlphabetPartitions".</span></span>
4. <span data-ttu-id="4d1cd-217">Em Olá **criar um serviço** caixa de diálogo caixa, escolha **com monitoração de estado** de serviço e chamá-lo "Alphabet.Processing" conforme mostrado na imagem de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-217">In hello **Create a Service** dialog box, choose **Stateful** service and call it "Alphabet.Processing" as shown in hello image below.</span></span>
       <span data-ttu-id="4d1cd-218">![Caixa de diálogo Novo serviço no Visual Studio][1]</span><span class="sxs-lookup"><span data-stu-id="4d1cd-218">![New service dialog in Visual Studio][1]</span></span>

  <!--  ![Stateful service screenshot](./media/service-fabric-concepts-partitioning/createstateful.png)-->

5. <span data-ttu-id="4d1cd-219">Defina o número de saudação de partições.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-219">Set hello number of partitions.</span></span> <span data-ttu-id="4d1cd-220">Arquivo de Applicationmanifest.xml de saudação abrir localizado no Olá ApplicationPackageRoot pasta Olá AlphabetPartitions projeto e atualize Olá parâmetro Processing_PartitionCount too26 conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-220">Open hello Applicationmanifest.xml file located in hello ApplicationPackageRoot folder of hello AlphabetPartitions project and update hello parameter Processing_PartitionCount too26 as shown below.</span></span>
   
    ```xml
    <Parameter Name="Processing_PartitionCount" DefaultValue="26" />
    ```
   
    <span data-ttu-id="4d1cd-221">Você também precisa Olá tooupdate LowKey e HighKey propriedades de elemento StatefulService Olá Olá ApplicationManifest.xml, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-221">You also need tooupdate hello LowKey and HighKey properties of hello StatefulService element in hello ApplicationManifest.xml as shown below.</span></span>
   
    ```xml
    <Service Name="Processing">
      <StatefulService ServiceTypeName="ProcessingType" TargetReplicaSetSize="[Processing_TargetReplicaSetSize]" MinReplicaSetSize="[Processing_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[Processing_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    ```
6. <span data-ttu-id="4d1cd-222">Para Olá toobe de serviço acessível, abra um ponto de extremidade em uma porta, adicionando o elemento de ponto de extremidade de saudação do ServiceManifest.xml (localizado na pasta de PackageRoot Olá) para Olá Alphabet.Processing serviço conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="4d1cd-222">For hello service toobe accessible, open up an endpoint on a port by adding hello endpoint element of ServiceManifest.xml (located in hello PackageRoot folder) for hello Alphabet.Processing service as shown below:</span></span>
   
    ```xml
    <Endpoint Name="ProcessingServiceEndpoint" Port="8089" Protocol="http" Type="Internal" />
    ```
   
    <span data-ttu-id="4d1cd-223">Agora o serviço de saudação é configurado toolisten tooan ponto de extremidade interno com 26 partições.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-223">Now hello service is configured toolisten tooan internal endpoint with 26 partitions.</span></span>
7. <span data-ttu-id="4d1cd-224">Em seguida, você precisa toooverride Olá `CreateServiceReplicaListeners()` método da classe de processamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-224">Next, you need toooverride hello `CreateServiceReplicaListeners()` method of hello Processing class.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4d1cd-225">Para este exemplo, supomos que você esteja usando um HttpCommunicationListener simples.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-225">For this sample, we assume that you are using a simple HttpCommunicationListener.</span></span> <span data-ttu-id="4d1cd-226">Para obter mais informações sobre a comunicação de serviço confiável, consulte [modelo de comunicação de serviço confiável Olá](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="4d1cd-226">For more information on reliable service communication, see [hello Reliable Service communication model](service-fabric-reliable-services-communication.md).</span></span>
   > 
   > 
8. <span data-ttu-id="4d1cd-227">Um padrão recomendado para a URL de saudação que uma réplica escuta em é Olá formato a seguir: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-227">A recommended pattern for hello URL that a replica listens on is hello following format: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.</span></span>
    <span data-ttu-id="4d1cd-228">Portanto, você tooconfigure sua toolisten de ouvinte de comunicação em pontos de extremidade correto hello e com esse padrão.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-228">So you want tooconfigure your communication listener toolisten on hello correct endpoints and with this pattern.</span></span>
   
    <span data-ttu-id="4d1cd-229">Várias réplicas do serviço podem ser hospedadas em Olá mesmo computador, para que esse endereço precisa toobe toohello exclusivo réplica.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-229">Multiple replicas of this service may be hosted on hello same computer, so this address needs toobe unique toohello replica.</span></span> <span data-ttu-id="4d1cd-230">Isso é porque a ID de partição + ID de réplica na URL de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-230">This is why   partition ID + replica ID are in hello URL.</span></span> <span data-ttu-id="4d1cd-231">HttpListener pode escutar em vários endereços Olá que mesma porta como prefixo da URL Olá é exclusivo.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-231">HttpListener can listen on multiple addresses on hello same port as long as hello URL prefix    is unique.</span></span>
   
    <span data-ttu-id="4d1cd-232">Olá que GUID extra há um caso avançada em réplicas secundárias também escutam solicitações somente leitura.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-232">hello extra GUID is there for an advanced case where secondary replicas also listen for read-only requests.</span></span> <span data-ttu-id="4d1cd-233">Quando esse for o caso de Olá, você deseja toomake-se de que um novo endereço exclusivo é usado durante a transição de endereço de saudação toosecondary primário tooforce clientes toore resolver.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-233">When that's hello case, you want toomake sure that a new unique address is used when transitioning from primary toosecondary tooforce clients toore-resolve hello address.</span></span> <span data-ttu-id="4d1cd-234">'+' é usado como o endereço de saudação aqui para que hello réplica escuta em todos os códigos de saudação hosts disponíveis (IP, FQDM, localhost, etc.) abaixo mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-234">'+' is used as hello address here so that hello replica listens on all available hosts (IP, FQDM, localhost, etc.) hello code below shows an example.</span></span>
   
    ```CSharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
         return new[] { new ServiceReplicaListener(context => this.CreateInternalListener(context))};
    }
    private ICommunicationListener CreateInternalListener(ServiceContext context)
    {
   
         EndpointResourceDescription internalEndpoint = context.CodePackageActivationContext.GetEndpoint("ProcessingServiceEndpoint");
         string uriPrefix = String.Format(
                "{0}://+:{1}/{2}/{3}-{4}/",
                internalEndpoint.Protocol,
                internalEndpoint.Port,
                context.PartitionId,
                context.ReplicaOrInstanceId,
                Guid.NewGuid());
   
         string nodeIP = FabricRuntime.GetNodeContext().IPAddressOrFQDN;
   
         string uriPublished = uriPrefix.Replace("+", nodeIP);
         return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInternalRequest);
    }
    ```
   
    <span data-ttu-id="4d1cd-235">Também vale a pena observar que Olá publicado URL é ligeiramente diferente do prefixo de URL escutando hello.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-235">It's also worth noting that hello published URL is slightly different from hello listening URL prefix.</span></span>
    <span data-ttu-id="4d1cd-236">URL de escuta Olá recebe tooHttpListener.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-236">hello listening URL is given tooHttpListener.</span></span> <span data-ttu-id="4d1cd-237">Olá que publicado URL é Olá que é publicado toohello serviço de nomenclatura do Service Fabric, que é usado para descoberta de serviço.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-237">hello published URL is hello URL that is published toohello Service Fabric Naming Service, which is used for service discovery.</span></span> <span data-ttu-id="4d1cd-238">Os clientes pedirão esse endereço por meio desse serviço de descoberta.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-238">Clients will ask for this address through that discovery service.</span></span> <span data-ttu-id="4d1cd-239">endereço de saudação que os clientes obtêm necessidades toohave Olá real IP ou FQDN do nó de saudação em ordem tooconnect.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-239">hello address that clients get needs toohave hello actual IP or FQDN of hello node in order tooconnect.</span></span> <span data-ttu-id="4d1cd-240">Portanto, você precisa tooreplace '+' com hello do nó IP ou FQDN conforme mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-240">So you need tooreplace '+' with hello node's IP or FQDN as shown above.</span></span>
9. <span data-ttu-id="4d1cd-241">Olá última etapa é Olá tooadd lógica toohello serviço conforme mostrado abaixo de processamento.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-241">hello last step is tooadd hello processing logic toohello service as shown below.</span></span>
   
    ```CSharp
    private async Task ProcessInternalRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        string output = null;
        string user = context.Request.QueryString["lastname"].ToString();
   
        try
        {
            output = await this.AddUserAsync(user);
        }
        catch (Exception ex)
        {
            output = ex.Message;
        }
   
        using (HttpListenerResponse response = context.Response)
        {
            if (output != null)
            {
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    private async Task<string> AddUserAsync(string user)
    {
        IReliableDictionary<String, String> dictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<String, String>>("dictionary");
   
        using (ITransaction tx = this.StateManager.CreateTransaction())
        {
            bool addResult = await dictionary.TryAddAsync(tx, user.ToUpperInvariant(), user);
   
            await tx.CommitAsync();
   
            return String.Format(
                "User {0} {1}",
                user,
                addResult ? "sucessfully added" : "already exists");
        }
    }
    ```
   
    <span data-ttu-id="4d1cd-242">`ProcessInternalRequest`Leituras Olá valores de parâmetro usado de cadeia de caracteres do Olá consulta toocall Olá partição e chamadas `AddUserAsync` dicionário confiável do tooadd Olá lastname toohello `dictionary`.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-242">`ProcessInternalRequest` reads hello values of hello query string parameter used toocall hello partition and calls `AddUserAsync` tooadd hello lastname toohello reliable dictionary `dictionary`.</span></span>
10. <span data-ttu-id="4d1cd-243">Vamos adicionar um toosee de projeto do serviço sem monitoração de estado toohello como você pode chamar uma partição específica.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-243">Let's add a stateless service toohello project toosee how you can call a particular partition.</span></span>
    
    <span data-ttu-id="4d1cd-244">Esse serviço serve como uma interface simples da web que aceita Olá lastname como um parâmetro de cadeia de caracteres de consulta, determina a chave de partição hello e envia toohello Alphabet.Processing serviço para processamento.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-244">This service serves as a simple web interface that accepts hello lastname as a query string parameter, determines hello partition key, and sends it toohello Alphabet.Processing service for processing.</span></span>
11. <span data-ttu-id="4d1cd-245">Em Olá **criar um serviço** caixa de diálogo caixa, escolha **sem monitoração de estado** de serviço e chamá-lo "Alphabet.Web" conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-245">In hello **Create a Service** dialog box, choose **Stateless** service and call it "Alphabet.Web" as shown below.</span></span>
    
    ![Captura de tela de serviço sem estado](./media/service-fabric-concepts-partitioning/createnewstateless.png)<span data-ttu-id="4d1cd-247">.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-247">.</span></span>
12. <span data-ttu-id="4d1cd-248">Atualize informações de ponto de extremidade Olá no hello ServiceManifest.xml de saudação Alphabet.WebApi serviço tooopen uma porta, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-248">Update hello endpoint information in hello ServiceManifest.xml of hello Alphabet.WebApi service tooopen up a port as shown below.</span></span>
    
    ```xml
    <Endpoint Name="WebApiServiceEndpoint" Protocol="http" Port="8081"/>
    ```
13. <span data-ttu-id="4d1cd-249">É necessário tooreturn uma coleção de ServiceInstanceListeners na classe Olá Web.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-249">You need tooreturn a collection of ServiceInstanceListeners in hello class Web.</span></span> <span data-ttu-id="4d1cd-250">Novamente, você pode escolher tooimplement um HttpCommunicationListener simple.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-250">Again, you can choose tooimplement a simple HttpCommunicationListener.</span></span>
    
    ```CSharp
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] {new ServiceInstanceListener(context => this.CreateInputListener(context))};
    }
    private ICommunicationListener CreateInputListener(ServiceContext context)
    {
        // Service instance's URL is hello node's IP & desired port
        EndpointResourceDescription inputEndpoint = context.CodePackageActivationContext.GetEndpoint("WebApiServiceEndpoint")
        string uriPrefix = String.Format("{0}://+:{1}/alphabetpartitions/", inputEndpoint.Protocol, inputEndpoint.Port);
        var uriPublished = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
        return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInputRequest);
    }
    ```
14. <span data-ttu-id="4d1cd-251">Agora, é necessário tooimplement lógica de processamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-251">Now you need tooimplement hello processing logic.</span></span> <span data-ttu-id="4d1cd-252">Olá chamadas HttpCommunicationListener `ProcessInputRequest` quando chegar a uma solicitação.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-252">hello HttpCommunicationListener calls `ProcessInputRequest` when a request comes in.</span></span> <span data-ttu-id="4d1cd-253">Vamos em frente e adicione Olá código abaixo.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-253">So let's go ahead and add hello code below.</span></span>
    
    ```CSharp
    private async Task ProcessInputRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        String output = null;
        try
        {
            string lastname = context.Request.QueryString["lastname"];
            char firstLetterOfLastName = lastname.First();
            ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    
            ResolvedServicePartition partition = await this.servicePartitionResolver.ResolveAsync(alphabetServiceUri, partitionKey, cancelRequest);
            ResolvedServiceEndpoint ep = partition.GetEndpoint();
    
            JObject addresses = JObject.Parse(ep.Address);
            string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
            UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
            primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
            string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    
            output = String.Format(
                    "Result: {0}. <p>Partition key: '{1}' generated from hello first letter '{2}' of input value '{3}'. <br>Processing service partition ID: {4}. <br>Processing service replica address: {5}",
                    result,
                    partitionKey,
                    firstLetterOfLastName,
                    lastname,
                    partition.Info.Id,
                    primaryReplicaAddress);
        }
        catch (Exception ex) { output = ex.Message; }
    
        using (var response = context.Response)
        {
            if (output != null)
            {
                output = output + "added tooPartition: " + primaryReplicaAddress;
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    ```
    
    <span data-ttu-id="4d1cd-254">Vamos ver o passo a passo.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-254">Let's walk through it step by step.</span></span> <span data-ttu-id="4d1cd-255">código de Olá lê a primeira letra de saudação do parâmetro de cadeia de caracteres de consulta Olá `lastname` em char.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-255">hello code reads hello first letter of hello query string parameter `lastname` into a char.</span></span> <span data-ttu-id="4d1cd-256">Em seguida, ele determina a chave de partição Olá para essa letra de subtraindo o valor hexadecimal de saudação do `A` do valor hexadecimal de saudação da primeira letra dos hello sobrenomes.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-256">Then, it determines hello partition key for this letter by subtracting hello hexadecimal value of `A` from hello hexadecimal value of hello last names' first letter.</span></span>
    
    ```CSharp
    string lastname = context.Request.QueryString["lastname"];
    char firstLetterOfLastName = lastname.First();
    ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    ```
    
    <span data-ttu-id="4d1cd-257">Lembre-se de que, neste exemplo, estamos usando 26 partições com uma chave de partição por partição.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-257">Remember, for this example, we are using 26 partitions with one partition key per partition.</span></span>
    <span data-ttu-id="4d1cd-258">Em seguida, podemos obter partição de serviço Olá `partition` para essa chave usando Olá `ResolveAsync` método hello `servicePartitionResolver` objeto.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-258">Next, we obtain hello service partition `partition` for this key by using hello `ResolveAsync` method on hello `servicePartitionResolver` object.</span></span> <span data-ttu-id="4d1cd-259">`servicePartitionResolver` é definido como</span><span class="sxs-lookup"><span data-stu-id="4d1cd-259">`servicePartitionResolver` is defined as</span></span>
    
    ```CSharp
    private readonly ServicePartitionResolver servicePartitionResolver = ServicePartitionResolver.GetDefault();
    ```
    
    <span data-ttu-id="4d1cd-260">Olá `ResolveAsync` URI de serviço do método leva hello, chave de partição hello e um token de cancelamento como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-260">hello `ResolveAsync` method takes hello service URI, hello partition key, and a cancellation token as parameters.</span></span> <span data-ttu-id="4d1cd-261">Olá URI do serviço para o serviço de processamento de saudação é `fabric:/AlphabetPartitions/Processing`.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-261">hello service URI for hello processing service is `fabric:/AlphabetPartitions/Processing`.</span></span> <span data-ttu-id="4d1cd-262">Em seguida, podemos obter ponto de extremidade de saudação da partição hello.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-262">Next, we get hello endpoint of hello partition.</span></span>
    
    ```CSharp
    ResolvedServiceEndpoint ep = partition.GetEndpoint()
    ```
    
    <span data-ttu-id="4d1cd-263">Finalmente, criar URL de ponto de extremidade hello mais querystring hello e chamar o serviço de processamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-263">Finally, we build hello endpoint URL plus hello querystring and call hello processing service.</span></span>
    
    ```CSharp
    JObject addresses = JObject.Parse(ep.Address);
    string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
    UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
    primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
    string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    ```
    
    <span data-ttu-id="4d1cd-264">Depois de processamento Olá, podemos gravar saída Olá novamente.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-264">Once hello processing is done, we write hello output back.</span></span>
15. <span data-ttu-id="4d1cd-265">Olá última etapa é o serviço de saudação tootest.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-265">hello last step is tootest hello service.</span></span> <span data-ttu-id="4d1cd-266">O Visual Studio usa parâmetros do aplicativo para implantação local e na nuvem.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-266">Visual Studio uses application parameters for local and cloud deployment.</span></span> <span data-ttu-id="4d1cd-267">serviço de saudação tootest com 26 partições localmente, você precisa Olá tooupdate `Local.xml` arquivo na pasta de ApplicationParameters saudação do projeto de AlphabetPartitions hello, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="4d1cd-267">tootest hello service with 26 partitions locally, you need tooupdate hello `Local.xml` file in hello ApplicationParameters folder of hello AlphabetPartitions project as shown below:</span></span>
    
    ```xml
    <Parameters>
      <Parameter Name="Processing_PartitionCount" Value="26" />
      <Parameter Name="WebApi_InstanceCount" Value="1" />
    </Parameters>
    ```
16. <span data-ttu-id="4d1cd-268">Depois de concluir a implantação, você pode verificar o serviço hello e todas as suas partições em Olá Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-268">Once you finish deployment, you can check hello service and all of its partitions in hello Service Fabric Explorer.</span></span>
    
    ![Captura de tela do Gerenciador do Service Fabric](./media/service-fabric-concepts-partitioning/sfxpartitions.png)
17. <span data-ttu-id="4d1cd-270">Em um navegador, você pode testar Olá lógica de particionamento, inserindo `http://localhost:8081/?lastname=somename`.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-270">In a browser, you can test hello partitioning logic by entering `http://localhost:8081/?lastname=somename`.</span></span> <span data-ttu-id="4d1cd-271">Você verá que cada sobrenome que inicia com hello a mesma letra está sendo armazenada no hello mesma partição.</span><span class="sxs-lookup"><span data-stu-id="4d1cd-271">You will see that each last name that starts with hello same letter is being stored in hello same partition.</span></span>
    
    ![Captura de tela do navegador](./media/service-fabric-concepts-partitioning/samplerunning.png)

<span data-ttu-id="4d1cd-273">código-fonte inteira saudação do exemplo hello está disponível em [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span><span class="sxs-lookup"><span data-stu-id="4d1cd-273">hello entire source code of hello sample is available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d1cd-274">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4d1cd-274">Next steps</span></span>
<span data-ttu-id="4d1cd-275">Para obter informações sobre os conceitos de malha do serviço, consulte o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="4d1cd-275">For information on Service Fabric concepts, see hello following:</span></span>

* [<span data-ttu-id="4d1cd-276">Disponibilidade dos serviços de malha do serviço</span><span class="sxs-lookup"><span data-stu-id="4d1cd-276">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="4d1cd-277">Escalabilidade de serviços da Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="4d1cd-277">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="4d1cd-278">Planejamento de capacidade para Aplicativos do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4d1cd-278">Capacity planning for Service Fabric applications</span></span>](service-fabric-capacity-planning.md)

[wikipartition]: https://en.wikipedia.org/wiki/Partition_(database)

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png