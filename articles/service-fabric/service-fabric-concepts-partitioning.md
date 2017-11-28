---
title: "Particionar serviços do Service Fabric | Microsoft Docs"
description: "Descreve como particionar os serviços com estado do Service Fabric. As partições permitem o armazenamento de dados em computadores locais para que dados e computação sejam dimensionados juntos."
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
ms.openlocfilehash: 3c1e80305cb65f41a6981b99f69e8b87f89599ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="partition-service-fabric-reliable-services"></a><span data-ttu-id="e741f-104">Particionar Reliable Services do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e741f-104">Partition Service Fabric reliable services</span></span>
<span data-ttu-id="e741f-105">Este artigo fornece uma introdução aos conceitos básicos de particionamento de Reliable Services do Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e741f-105">This article provides an introduction to the basic concepts of partitioning Azure Service Fabric reliable services.</span></span> <span data-ttu-id="e741f-106">O código-fonte usado no artigo também está disponível no [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span><span class="sxs-lookup"><span data-stu-id="e741f-106">The source code used in the article is also available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="partitioning"></a><span data-ttu-id="e741f-107">Particionamento</span><span class="sxs-lookup"><span data-stu-id="e741f-107">Partitioning</span></span>
<span data-ttu-id="e741f-108">O particionamento não é exclusivo para o Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e741f-108">Partitioning is not unique to Service Fabric.</span></span> <span data-ttu-id="e741f-109">Na verdade, é um padrão núcleo da criação de serviços escalonáveis.</span><span class="sxs-lookup"><span data-stu-id="e741f-109">In fact, it is a core pattern of building scalable services.</span></span> <span data-ttu-id="e741f-110">Em um sentido mais amplo, podemos pensar em particionamento como um conceito de divisão de estado (dados) e computar unidades menores acessíveis para melhorar o desempenho e a escalabilidade.</span><span class="sxs-lookup"><span data-stu-id="e741f-110">In a broader sense, we can think about partitioning as a concept of dividing state (data) and compute into smaller accessible units to improve scalability and performance.</span></span> <span data-ttu-id="e741f-111">Uma forma bem conhecida de particionamento é o [particionamento de dados][wikipartition], também conhecido como fragmentação.</span><span class="sxs-lookup"><span data-stu-id="e741f-111">A well-known form of partitioning is [data partitioning][wikipartition], also known as sharding.</span></span>

### <a name="partition-service-fabric-stateless-services"></a><span data-ttu-id="e741f-112">Particionar serviços sem estado do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e741f-112">Partition Service Fabric stateless services</span></span>
<span data-ttu-id="e741f-113">Para serviços sem estado, você pode pensar em uma partição como uma unidade lógica que contém uma ou mais instâncias de um serviço.</span><span class="sxs-lookup"><span data-stu-id="e741f-113">For stateless services, you can think about a partition being a logical unit that contains one or more instances of a service.</span></span> <span data-ttu-id="e741f-114">A Figura 1 mostra um serviço sem estado com cinco instâncias distribuídas em um cluster usando uma partição.</span><span class="sxs-lookup"><span data-stu-id="e741f-114">Figure 1 shows a stateless service with five instances distributed across a cluster using one partition.</span></span>

![Serviço sem estado](./media/service-fabric-concepts-partitioning/statelessinstances.png)

<span data-ttu-id="e741f-116">Há realmente dois tipos de soluções de serviço sem estado.</span><span class="sxs-lookup"><span data-stu-id="e741f-116">There are really two types of stateless service solutions.</span></span> <span data-ttu-id="e741f-117">O primeiro é um serviço que mantém o estado externamente, por exemplo, em um banco de dados SQL do Azure (como um site que armazena dados e informações de sessão).</span><span class="sxs-lookup"><span data-stu-id="e741f-117">The first one is a service that persists its state externally, for example in an Azure SQL database (like a website that stores the session information and data).</span></span> <span data-ttu-id="e741f-118">A segunda são serviços apenas de computação (como uma calculadora ou a criação de miniaturas imagem) que não gerenciam nenhum estado persistente.</span><span class="sxs-lookup"><span data-stu-id="e741f-118">The second one is computation-only services (like a calculator or image thumbnailing) that do not manage any persistent state.</span></span>

<span data-ttu-id="e741f-119">Em ambos os casos o particionamento de um serviço sem estado é um cenário muito raro – a escalabilidade e disponibilidade normalmente são obtidas pela adição de mais instâncias.</span><span class="sxs-lookup"><span data-stu-id="e741f-119">In either case, partitioning a stateless service is a very rare scenario--scalability and availability are normally achieved by adding more instances.</span></span> <span data-ttu-id="e741f-120">As únicas vezes em que você deve considerar várias partições para instâncias de serviço sem estado é quando precisar atender a solicitações especiais de roteamento.</span><span class="sxs-lookup"><span data-stu-id="e741f-120">The only time you want to consider multiple partitions for stateless service instances is when you need to meet special routing requests.</span></span>

<span data-ttu-id="e741f-121">Por exemplo, considere um caso em que os usuários com IDs de um determinado intervalo só devem ser atendidos por uma instância de determinado serviço.</span><span class="sxs-lookup"><span data-stu-id="e741f-121">As an example, consider a case where users with IDs in a certain range should only be served by a particular service instance.</span></span> <span data-ttu-id="e741f-122">Outro exemplo de quando é possível particionar um serviço sem estado é quando você tem um back-end realmente particionado (por exemplo, um banco de dados SQL fragmentado) e você deseja controlar qual instância de serviço deve gravar o fragmento do banco de dados ou executar outras tarefas de preparação dentro do serviço sem estado que requer as mesmas informações de particionamento como usadas no back-end.</span><span class="sxs-lookup"><span data-stu-id="e741f-122">Another example of when you could partition a stateless service is when you have a truly partitioned backend (e.g. a sharded SQL database) and you want to control which service instance should write to the database shard--or perform other preparation work within the stateless service that requires the same partitioning information as is used in the backend.</span></span> <span data-ttu-id="e741f-123">Esses tipos de cenários também podem ser resolvidos de diferentes maneiras e não exigem, necessariamente, particionamento de serviço.</span><span class="sxs-lookup"><span data-stu-id="e741f-123">Those types of scenarios can also be solved in different ways and do not necessarily require service partitioning.</span></span>

<span data-ttu-id="e741f-124">O restante deste passo a passo se concentra nos serviços sem estado.</span><span class="sxs-lookup"><span data-stu-id="e741f-124">The remainder of this walkthrough focuses on stateful services.</span></span>

### <a name="partition-service-fabric-stateful-services"></a><span data-ttu-id="e741f-125">Particionar serviços com estado do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e741f-125">Partition Service Fabric stateful services</span></span>
<span data-ttu-id="e741f-126">A Malha de Serviço facilita o desenvolvimento serviços com estado escalonáveis, oferecendo uma ótima forma para o estado de partição (dados).</span><span class="sxs-lookup"><span data-stu-id="e741f-126">Service Fabric makes it easy to develop scalable stateful services by offering a first-class way to partition state (data).</span></span> <span data-ttu-id="e741f-127">Conceitualmente, uma partição de um serviço com estado é uma unidade de escala altamente confiável por meio de [réplicas](service-fabric-availability-services.md) distribuídas e balanceadas entre os nós de um cluster.</span><span class="sxs-lookup"><span data-stu-id="e741f-127">Conceptually, you can think about a partition of a stateful service as a scale unit that is highly reliable through [replicas](service-fabric-availability-services.md) that are distributed and balanced across the nodes in a cluster.</span></span>

<span data-ttu-id="e741f-128">No contexto dos serviços com estado do Service Fabric, o particionamento se refere ao processo de determinar que uma partição de serviço específica é responsável por uma parte do estado completo do serviço.</span><span class="sxs-lookup"><span data-stu-id="e741f-128">Partitioning in the context of Service Fabric stateful services refers to the process of determining that a particular service partition is responsible for a portion of the complete state of the service.</span></span> <span data-ttu-id="e741f-129">(Conforme mencionado anteriormente, uma partição é um conjunto de [réplicas](service-fabric-availability-services.md)).</span><span class="sxs-lookup"><span data-stu-id="e741f-129">(As mentioned before, a partition is a set of [replicas](service-fabric-availability-services.md)).</span></span> <span data-ttu-id="e741f-130">Uma grande vantagem do Service Fabric é que ele coloca as partições em nós diferentes.</span><span class="sxs-lookup"><span data-stu-id="e741f-130">A great thing about Service Fabric is that it places the partitions on different nodes.</span></span> <span data-ttu-id="e741f-131">Isso permite aumentar o limite de recursos do nó.</span><span class="sxs-lookup"><span data-stu-id="e741f-131">This allows them to grow to a node's resource limit.</span></span> <span data-ttu-id="e741f-132">Conforme os dados precisam crescer, as partições crescem e o Service Fabric redistribui as partições entre os nós.</span><span class="sxs-lookup"><span data-stu-id="e741f-132">As the data needs grow, partitions grow, and Service Fabric rebalances partitions across nodes.</span></span> <span data-ttu-id="e741f-133">Isso garante o uso contínuo eficiente dos recursos de hardware.</span><span class="sxs-lookup"><span data-stu-id="e741f-133">This ensures the continued efficient use of hardware resources.</span></span>

<span data-ttu-id="e741f-134">Para dar um exemplo, digamos que você comece com um cluster de cinco nós e um serviço configurado para ter 10 partições e um destino de três réplicas.</span><span class="sxs-lookup"><span data-stu-id="e741f-134">To give you an example, say you start with a 5-node cluster and a service that is configured to have 10 partitions and a target of three replicas.</span></span> <span data-ttu-id="e741f-135">Nesse caso, o Service Fabric deveria balancear e distribuir as réplicas no cluster e – você acabaria com duas [réplicas](service-fabric-availability-services.md) principais por nó.</span><span class="sxs-lookup"><span data-stu-id="e741f-135">In this case, Service Fabric would balance and distribute the replicas across the cluster--and you would end up with two primary [replicas](service-fabric-availability-services.md) per node.</span></span>
<span data-ttu-id="e741f-136">Caso você precise escalar horizontalmente nosso cluster para 10 nós, o Service Fabric rebalanceará as [réplicas](service-fabric-availability-services.md) principais entre todos os 10 nós.</span><span class="sxs-lookup"><span data-stu-id="e741f-136">If you now need to scale out the cluster to 10 nodes, Service Fabric would rebalance the primary [replicas](service-fabric-availability-services.md) across all 10 nodes.</span></span> <span data-ttu-id="e741f-137">Da mesma forma, se você dimensionar para cinco nós, o Service Fabric rebalanceará todas as réplicas entre todos os cinco nós.</span><span class="sxs-lookup"><span data-stu-id="e741f-137">Likewise, if you scaled back to 5 nodes, Service Fabric would rebalance all the replicas across the 5 nodes.</span></span>  

<span data-ttu-id="e741f-138">A Figura 2 mostra a distribuição de 10 partições antes e depois do dimensionamento do cluster.</span><span class="sxs-lookup"><span data-stu-id="e741f-138">Figure 2 shows the distribution of 10 partitions before and after scaling the cluster.</span></span>

![Serviço com estado](./media/service-fabric-concepts-partitioning/partitions.png)

<span data-ttu-id="e741f-140">Como resultado a expansão é atingida pois as solicitações de clientes são distribuídas entre computadores, o desempenho geral do aplicativo é aprimorado e a contenção no acesso a partes de dados é reduzida.</span><span class="sxs-lookup"><span data-stu-id="e741f-140">As a result, the scale-out is achieved since requests from clients are distributed across computers, overall performance of the application is improved, and contention on access to chunks of data is reduced.</span></span>

## <a name="plan-for-partitioning"></a><span data-ttu-id="e741f-141">Plano de particionamento</span><span class="sxs-lookup"><span data-stu-id="e741f-141">Plan for partitioning</span></span>
<span data-ttu-id="e741f-142">Antes de implementar um serviço, sempre considere a estratégia de particionamento necessária para escalar horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="e741f-142">Before implementing a service, you should always consider the partitioning strategy that is required to scale out.</span></span> <span data-ttu-id="e741f-143">Há maneiras diferentes, mas todas elas voltadas para o que o aplicativo precisa atingir.</span><span class="sxs-lookup"><span data-stu-id="e741f-143">There are different ways, but all of them focus on what the application needs to achieve.</span></span> <span data-ttu-id="e741f-144">Para o contexto deste artigo, vamos considerar alguns dos aspectos mais importantes.</span><span class="sxs-lookup"><span data-stu-id="e741f-144">For the context of this article, let's consider some of the more important aspects.</span></span>

<span data-ttu-id="e741f-145">Uma boa abordagem é pensar sobre a estrutura do estado que precisará ser particionado como a primeira etapa.</span><span class="sxs-lookup"><span data-stu-id="e741f-145">A good approach is to think about the structure of the state that needs to be partitioned, as the first step.</span></span>

<span data-ttu-id="e741f-146">Veja abaixo um exemplo simples</span><span class="sxs-lookup"><span data-stu-id="e741f-146">Let's take a simple example.</span></span> <span data-ttu-id="e741f-147">Se você fosse criar um serviço em uma pesquisa regional, poderia criar uma partição de cada cidade na região.</span><span class="sxs-lookup"><span data-stu-id="e741f-147">If you were to build a service for a countywide poll, you could create a partition for each city in the county.</span></span> <span data-ttu-id="e741f-148">Em seguida, poderia armazenar os votos para cada pessoa na cidade na partição que corresponde à cidade.</span><span class="sxs-lookup"><span data-stu-id="e741f-148">Then, you could store the votes for every person in the city in the partition that corresponds to that city.</span></span> <span data-ttu-id="e741f-149">A Figura 3 ilustra um conjunto de pessoas e a cidade em que residem.</span><span class="sxs-lookup"><span data-stu-id="e741f-149">Figure 3 illustrates a set of people and the city in which they reside.</span></span>

![Partição simples](./media/service-fabric-concepts-partitioning/cities.png)

<span data-ttu-id="e741f-151">Como a população das cidades varia muito, você poderia acabar com algumas partições que contêm muitos dados (por exemplo, Seattle) e outras partições com muito pouco estado (por exemplo, Kirkland).</span><span class="sxs-lookup"><span data-stu-id="e741f-151">As the population of cities varies widely, you may end up with some partitions that contain a lot of data (e.g. Seattle) and other partitions with very little state (e.g. Kirkland).</span></span> <span data-ttu-id="e741f-152">Então, qual é o impacto de ter partições com quantidades irregulares de estado?</span><span class="sxs-lookup"><span data-stu-id="e741f-152">So what is the impact of having partitions with uneven amounts of state?</span></span>

<span data-ttu-id="e741f-153">Se você pensar sobre o exemplo novamente, poderá facilmente ver que a partição que contém os votos de Seattle obterá mais tráfego do que a de Kirkland.</span><span class="sxs-lookup"><span data-stu-id="e741f-153">If you think about the example again, you can easily see that the partition that holds the votes for Seattle will get more traffic than the Kirkland one.</span></span> <span data-ttu-id="e741f-154">Por padrão, o Service Fabric garante que haja aproximadamente o mesmo número de réplicas primárias e secundárias em cada nó.</span><span class="sxs-lookup"><span data-stu-id="e741f-154">By default, Service Fabric makes sure that there is about the same number of primary and secondary replicas on each node.</span></span> <span data-ttu-id="e741f-155">Assim, você pode acabar com nós que hospedam réplicas que atendem a mais tráfego e outras que atendem a menos tráfego.</span><span class="sxs-lookup"><span data-stu-id="e741f-155">So you may end up with nodes that hold replicas that serve more traffic and others that serve less traffic.</span></span> <span data-ttu-id="e741f-156">Você deve, de preferência, evitar pontos altos e baixos assim em um cluster.</span><span class="sxs-lookup"><span data-stu-id="e741f-156">You would preferably want to avoid hot and cold spots like this in a cluster.</span></span>

<span data-ttu-id="e741f-157">Para evitar isso, você deve realizar duas ações do ponto de vista de particionamento:</span><span class="sxs-lookup"><span data-stu-id="e741f-157">In order to avoid this, you should do two things, from a partitioning point of view:</span></span>

* <span data-ttu-id="e741f-158">Tente particionar o estado que ele seja distribuído igualmente entre todas as partições.</span><span class="sxs-lookup"><span data-stu-id="e741f-158">Try to partition the state so that it is evenly distributed across all partitions.</span></span>
* <span data-ttu-id="e741f-159">Relatar carga de cada uma das réplicas para o serviço.</span><span class="sxs-lookup"><span data-stu-id="e741f-159">Report load from each of the replicas for the service.</span></span> <span data-ttu-id="e741f-160">(Para obter informações sobre como fazer isso, leia este artigo sobre [métricas e carga](service-fabric-cluster-resource-manager-metrics.md)).</span><span class="sxs-lookup"><span data-stu-id="e741f-160">(For information on how, check out this article on [Metrics and Load](service-fabric-cluster-resource-manager-metrics.md)).</span></span> <span data-ttu-id="e741f-161">A Service Fabric oferece a capacidade de relatar a carga consumida por serviços, como a quantidade de memória ou o número de registros.</span><span class="sxs-lookup"><span data-stu-id="e741f-161">Service Fabric provides the capability to report load consumed by services, such as amount of memory or number of records.</span></span> <span data-ttu-id="e741f-162">Com base nas métricas relatadas, o Service Fabric detecta que algumas partições estão atendendo a cargas mais altas que outras e faz um novo balanceamento do cluster, movendo réplicas para nós mais adequados de modo que, no geral, nenhum nó seja sobrecarregado.</span><span class="sxs-lookup"><span data-stu-id="e741f-162">Based on the metrics reported, Service Fabric detects that some partitions are serving higher loads than others and rebalances the cluster by moving replicas to more suitable nodes, so that overall no node is overloaded.</span></span>

<span data-ttu-id="e741f-163">Às vezes, você não tem como saber quantos dados haverá em uma determinada partição.</span><span class="sxs-lookup"><span data-stu-id="e741f-163">Sometimes, you cannot know how much data will be in a given partition.</span></span> <span data-ttu-id="e741f-164">Uma recomendação geral é realizar ambas as ações – primeiro, adotar uma estratégia de particionamento que distribua os dados uniformemente entre as partições; segundo, relatar a carga.</span><span class="sxs-lookup"><span data-stu-id="e741f-164">So a general recommendation is to do both--first, by adopting a partitioning strategy that spreads the data evenly across the partitions and second, by reporting load.</span></span>  <span data-ttu-id="e741f-165">O primeiro método impede as situações descritas no exemplo de votação, enquanto o segundo ajuda a amenizar diferenças temporárias no acesso ou carga ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="e741f-165">The first method prevents situations described in the voting example, while the second helps smooth out temporary differences in access or load over time.</span></span>

<span data-ttu-id="e741f-166">Outro aspecto do planejamento de partição é escolher o número correto de partições para começar.</span><span class="sxs-lookup"><span data-stu-id="e741f-166">Another aspect of partition planning is to choose the correct number of partitions to begin with.</span></span>
<span data-ttu-id="e741f-167">Do ponto de vista do Service Fabric, não há nada que impeça começar com um número de partições maior do o previsto para o cenário.</span><span class="sxs-lookup"><span data-stu-id="e741f-167">From a Service Fabric perspective, there is nothing that prevents you from starting out with a higher number of partitions than anticipated for your scenario.</span></span>
<span data-ttu-id="e741f-168">Na verdade, suponha que o número máximo de partições seja uma abordagem válida.</span><span class="sxs-lookup"><span data-stu-id="e741f-168">In fact, assuming the maximum number of partitions is a valid approach.</span></span>

<span data-ttu-id="e741f-169">Em casos raros, você acabará precisando de mais partições do que escolheu inicialmente.</span><span class="sxs-lookup"><span data-stu-id="e741f-169">In rare cases, you may end up needing more partitions than you have initially chosen.</span></span> <span data-ttu-id="e741f-170">Como você não pode alterar a contagem de partições após o fato, precisará aplicar algumas abordagens de partição avançadas, como criar uma nova instância de serviço do mesmo tipo de serviço.</span><span class="sxs-lookup"><span data-stu-id="e741f-170">As you cannot change the partition count after the fact, you would need to apply some advanced partition approaches, such as creating a new service instance of the same service type.</span></span> <span data-ttu-id="e741f-171">Você também precisaria implementar alguma lógica no lado do cliente que encaminhe as solicitações para a instância de serviço correta, com base no conhecimento do lado do cliente que o seu código de cliente deve manter.</span><span class="sxs-lookup"><span data-stu-id="e741f-171">You would also need to implement some client-side logic that routes the requests to the correct service instance, based on client-side knowledge that your client code must maintain.</span></span>

<span data-ttu-id="e741f-172">Outra consideração de planejamento de particionamento são os recursos disponíveis do computador.</span><span class="sxs-lookup"><span data-stu-id="e741f-172">Another consideration for partitioning planning is the available computer resources.</span></span> <span data-ttu-id="e741f-173">Como o estado precisa ser acessado e armazenados, você deve fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e741f-173">As the state needs to be accessed and stored, you are bound to follow:</span></span>

* <span data-ttu-id="e741f-174">Limites de largura de banda de rede</span><span class="sxs-lookup"><span data-stu-id="e741f-174">Network bandwidth limits</span></span>
* <span data-ttu-id="e741f-175">Limites de memória do sistema</span><span class="sxs-lookup"><span data-stu-id="e741f-175">System memory limits</span></span>
* <span data-ttu-id="e741f-176">Limites de armazenamento de disco</span><span class="sxs-lookup"><span data-stu-id="e741f-176">Disk storage limits</span></span>

<span data-ttu-id="e741f-177">O que acontece se você tiver restrições de recursos em um cluster em execução?</span><span class="sxs-lookup"><span data-stu-id="e741f-177">So what happens if you run into resource constraints in a running cluster?</span></span> <span data-ttu-id="e741f-178">A resposta é que você pode simplesmente escalar horizontalmente o cluster para acomodar os novos requisitos.</span><span class="sxs-lookup"><span data-stu-id="e741f-178">The answer is that you can simply scale out the cluster to accommodate the new requirements.</span></span>

<span data-ttu-id="e741f-179">[O guia de planejamento de capacidade](service-fabric-capacity-planning.md) oferece orientação sobre como determinar a quantidade necessária de nós no cluster.</span><span class="sxs-lookup"><span data-stu-id="e741f-179">[The capacity planning guide](service-fabric-capacity-planning.md) offers guidance for how to determine how many nodes your cluster needs.</span></span>

## <a name="get-started-with-partitioning"></a><span data-ttu-id="e741f-180">Introdução ao particionamento</span><span class="sxs-lookup"><span data-stu-id="e741f-180">Get started with partitioning</span></span>
<span data-ttu-id="e741f-181">Esta seção descreve como começar com o particionamento do seu serviço.</span><span class="sxs-lookup"><span data-stu-id="e741f-181">This section describes how to get started with partitioning your service.</span></span>

<span data-ttu-id="e741f-182">O Service Fabric oferece uma variedade de três esquemas de partição:</span><span class="sxs-lookup"><span data-stu-id="e741f-182">Service Fabric offers a choice of three partition schemes:</span></span>

* <span data-ttu-id="e741f-183">Intervalo de particionamento (também conhecido como UniformInt64Partition).</span><span class="sxs-lookup"><span data-stu-id="e741f-183">Ranged partitioning (otherwise known as UniformInt64Partition).</span></span>
* <span data-ttu-id="e741f-184">Particionamento nomeado.</span><span class="sxs-lookup"><span data-stu-id="e741f-184">Named partitioning.</span></span> <span data-ttu-id="e741f-185">Aplicativos que usam esse modelo geralmente têm dados em bucket, dentro de um conjunto limitado.</span><span class="sxs-lookup"><span data-stu-id="e741f-185">Applications using this model usually have data that can be bucketed, within a bounded set.</span></span> <span data-ttu-id="e741f-186">Alguns exemplos comuns de campos de dados usados como chaves de partição nomeada seriam regiões, códigos postais, grupos de clientes ou outros limites de negócios.</span><span class="sxs-lookup"><span data-stu-id="e741f-186">Some common examples of data fields used as named partition keys would be regions, postal codes, customer groups, or other business boundaries.</span></span>
* <span data-ttu-id="e741f-187">Particionamento de singleton.</span><span class="sxs-lookup"><span data-stu-id="e741f-187">Singleton partitioning.</span></span> <span data-ttu-id="e741f-188">Partições de singleton normalmente são usadas quando o serviço não requer qualquer roteamento adicional.</span><span class="sxs-lookup"><span data-stu-id="e741f-188">Singleton partitions are typically used when the service does not require any additional routing.</span></span> <span data-ttu-id="e741f-189">Por exemplo, serviços sem estado usam esse esquema de particionamento por padrão.</span><span class="sxs-lookup"><span data-stu-id="e741f-189">For example, stateless services use this partitioning scheme by default.</span></span>

<span data-ttu-id="e741f-190">Os esquemas de particionamento Singleton e Nomeado são formulários especiais de partições de intervalos.</span><span class="sxs-lookup"><span data-stu-id="e741f-190">Named and Singleton partitioning schemes are special forms of ranged partitions.</span></span> <span data-ttu-id="e741f-191">Por padrão os modelos do Visual Studio para o Service Fabric usam o particionamento nomeado, já que é o mais comum e o mais útil.</span><span class="sxs-lookup"><span data-stu-id="e741f-191">By default, the Visual Studio templates for Service Fabric use ranged partitioning, as it is the most common and useful one.</span></span> <span data-ttu-id="e741f-192">O restante deste artigo se concentra no esquema de particionamento por intervalo.</span><span class="sxs-lookup"><span data-stu-id="e741f-192">The remainder of this article focuses on the ranged partitioning scheme.</span></span>

### <a name="ranged-partitioning-scheme"></a><span data-ttu-id="e741f-193">Esquema de particionamento por intervalos</span><span class="sxs-lookup"><span data-stu-id="e741f-193">Ranged partitioning scheme</span></span>
<span data-ttu-id="e741f-194">Usado para especificar um intervalo inteiro (identificado por uma chave alta e uma chave baixa) e um várias partições (n).</span><span class="sxs-lookup"><span data-stu-id="e741f-194">This is used to specify an integer range (identified by a low key and high key) and a number of partitions (n).</span></span> <span data-ttu-id="e741f-195">Cria n partições, cada uma responsável por um subintervalo sem sobreposição do intervalo de chave de partição geral.</span><span class="sxs-lookup"><span data-stu-id="e741f-195">It creates n partitions, each responsible for a non-overlapping subrange of the overall partition key range.</span></span> <span data-ttu-id="e741f-196">Por exemplo, um esquema de particionamento por intervalos com uma chave baixa de 0, uma chave de alta de 99 e uma contagem de 4 criaria quatro partições, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="e741f-196">For example, a ranged partitioning scheme with a low key of 0, a high key of 99, and a count of 4 would create four partitions, as shown below.</span></span>

![Particionamento por intervalos](./media/service-fabric-concepts-partitioning/range-partitioning.png)

<span data-ttu-id="e741f-198">Uma abordagem comum é criar um hash com base em uma chave exclusiva dentro do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="e741f-198">A common approach is to create a hash based on a unique key within the data set.</span></span> <span data-ttu-id="e741f-199">Alguns exemplos comuns de chaves seriam um número de identificação de veículo (VIN), uma ID de funcionário ou uma cadeia de caracteres exclusiva.</span><span class="sxs-lookup"><span data-stu-id="e741f-199">Some common examples of keys would be a vehicle identification number (VIN), an employee ID, or a unique string.</span></span> <span data-ttu-id="e741f-200">Usando essa chave exclusiva, você criaria um código de hash longo, o módulo do intervalo de chaves, para usar como sua chave.</span><span class="sxs-lookup"><span data-stu-id="e741f-200">By using this unique key, you would then generate a hash code, modulus the key range, to use as your key.</span></span> <span data-ttu-id="e741f-201">Você pode especificar os limites superior e inferior do intervalo de chave permitido.</span><span class="sxs-lookup"><span data-stu-id="e741f-201">You can specify the upper and lower bounds of the allowed key range.</span></span>

### <a name="select-a-hash-algorithm"></a><span data-ttu-id="e741f-202">Selecionar um algoritmo de hash</span><span class="sxs-lookup"><span data-stu-id="e741f-202">Select a hash algorithm</span></span>
<span data-ttu-id="e741f-203">Uma parte importante de hash é selecionar o algoritmo de hash.</span><span class="sxs-lookup"><span data-stu-id="e741f-203">An important part of hashing is selecting your hash algorithm.</span></span> <span data-ttu-id="e741f-204">Uma consideração é se o objetivo é agrupar chaves semelhantes próximas umas das outras (hash sensível à localidade) ou se a atividade precisa ser distribuída amplamente em todas as partições (hash de distribuição), que é o mais comum.</span><span class="sxs-lookup"><span data-stu-id="e741f-204">A consideration is whether the goal is to group similar keys near each other (locality sensitive hashing)--or if activity should be distributed broadly across all partitions (distribution hashing), which is more common.</span></span>

<span data-ttu-id="e741f-205">As características de um bom algoritmo de hash de distribuição são facilidade de computar, poucas colisões e distribuição uniforme de chaves.</span><span class="sxs-lookup"><span data-stu-id="e741f-205">The characteristics of a good distribution hashing algorithm are that it is easy to compute, it has few collisions, and it distributes the keys evenly.</span></span> <span data-ttu-id="e741f-206">Um bom exemplo de algoritmo de hash eficiente é o algoritmo de hash [FNV-1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) .</span><span class="sxs-lookup"><span data-stu-id="e741f-206">A good example of an efficient hash algorithm is the [FNV-1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) hash algorithm.</span></span>

<span data-ttu-id="e741f-207">Um bom recurso para opções gerais de algoritmo de código de hash é [a página do Wikipedia sobre funções de hash](http://en.wikipedia.org/wiki/Hash_function).</span><span class="sxs-lookup"><span data-stu-id="e741f-207">A good resource for general hash code algorithm choices is the [Wikipedia page on hash functions](http://en.wikipedia.org/wiki/Hash_function).</span></span>

## <a name="build-a-stateful-service-with-multiple-partitions"></a><span data-ttu-id="e741f-208">Criar um serviço com estado com várias partições</span><span class="sxs-lookup"><span data-stu-id="e741f-208">Build a stateful service with multiple partitions</span></span>
<span data-ttu-id="e741f-209">Vamos criar seu primeiro serviço com estado confiável com várias partições.</span><span class="sxs-lookup"><span data-stu-id="e741f-209">Let's create your first reliable stateful service with multiple partitions.</span></span> <span data-ttu-id="e741f-210">Neste exemplo, você criará um aplicativo muito simples no qual deseja armazenar todos os sobrenomes que começam com a mesma letra na mesma partição.</span><span class="sxs-lookup"><span data-stu-id="e741f-210">In this example, you will build a very simple application where you want to store all last names that start with the same letter in the same partition.</span></span>

<span data-ttu-id="e741f-211">Antes de escrever qualquer código, você precisa pensar sobre as chaves de partição e partições.</span><span class="sxs-lookup"><span data-stu-id="e741f-211">Before you write any code, you need to think about the partitions and partition keys.</span></span> <span data-ttu-id="e741f-212">Você precisa de 26 partições (uma para cada letra no alfabeto), mas e quanto às chaves baixas e altas?</span><span class="sxs-lookup"><span data-stu-id="e741f-212">You need 26 partitions (one for each letter in the alphabet), but what about the low and high keys?</span></span>
<span data-ttu-id="e741f-213">Uma vez que queremos literalmente ter uma partição por letra, podemos usar 0 como a chave baixa e 25 como a chave alta, já que cada letra é sua própria chave.</span><span class="sxs-lookup"><span data-stu-id="e741f-213">As we literally want to have one partition per letter, we can use 0 as the low key and 25 as the high key, as each letter is its own key.</span></span>

> [!NOTE]
> <span data-ttu-id="e741f-214">Esse é um cenário simplificado, pois, na realidade, a distribuição seria irregular.</span><span class="sxs-lookup"><span data-stu-id="e741f-214">This is a simplified scenario, as in reality the distribution would be uneven.</span></span> <span data-ttu-id="e741f-215">Sobrenomes começando com a letra “S” ou “M” são mais comuns do que os que começam com “X” ou “Y”.</span><span class="sxs-lookup"><span data-stu-id="e741f-215">Last names starting with the letters "S" or "M" are more common than the ones starting with "X" or "Y".</span></span>
> 
> 

1. <span data-ttu-id="e741f-216">Abra **Visual Studio** > **Arquivo** > **Novo** > **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="e741f-216">Open **Visual Studio** > **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="e741f-217">Na caixa de diálogo **Novo Projeto** escolha um aplicativo do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e741f-217">In the **New Project** dialog box, choose the Service Fabric application.</span></span>
3. <span data-ttu-id="e741f-218">Dê ao projeto o nome de “AlphabetPartitions”.</span><span class="sxs-lookup"><span data-stu-id="e741f-218">Call the project "AlphabetPartitions".</span></span>
4. <span data-ttu-id="e741f-219">Na caixa de diálogo **Criar um Serviço**, escolha o serviço **Com Estado** e dê a ele o nome “Alphabet.Processing”, como mostra a imagem abaixo.</span><span class="sxs-lookup"><span data-stu-id="e741f-219">In the **Create a Service** dialog box, choose **Stateful** service and call it "Alphabet.Processing" as shown in the image below.</span></span>
       <span data-ttu-id="e741f-220">![Caixa de diálogo Novo serviço no Visual Studio][1]</span><span class="sxs-lookup"><span data-stu-id="e741f-220">![New service dialog in Visual Studio][1]</span></span>

  <!--  ![Stateful service screenshot](./media/service-fabric-concepts-partitioning/createstateful.png)-->

5. <span data-ttu-id="e741f-221">Defina o número de partições.</span><span class="sxs-lookup"><span data-stu-id="e741f-221">Set the number of partitions.</span></span> <span data-ttu-id="e741f-222">Abra o arquivo Applicationmanifest.xml localizado na pasta ApplicationPackageRoot do projeto AlphabetPartitions e atualize o parâmetro Processing_PartitionCount para 26, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="e741f-222">Open the Applicationmanifest.xml file located in the ApplicationPackageRoot folder of the AlphabetPartitions project and update the parameter Processing_PartitionCount to 26 as shown below.</span></span>
   
    ```xml
    <Parameter Name="Processing_PartitionCount" DefaultValue="26" />
    ```
   
    <span data-ttu-id="e741f-223">Você também deve atualizar as propriedades LowKey e HighKey do elemento StatefulService no ApplicationManifest.xml, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="e741f-223">You also need to update the LowKey and HighKey properties of the StatefulService element in the ApplicationManifest.xml as shown below.</span></span>
   
    ```xml
    <Service Name="Processing">
      <StatefulService ServiceTypeName="ProcessingType" TargetReplicaSetSize="[Processing_TargetReplicaSetSize]" MinReplicaSetSize="[Processing_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[Processing_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    ```
6. <span data-ttu-id="e741f-224">Para que o serviço fique acessível, abra um ponto de extremidade em uma porta adicionando o elemento de ponto de extremidade do ServiceManifest.xml (localizado na pasta PackageRoot) para o serviço Alphabet.Processing, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="e741f-224">For the service to be accessible, open up an endpoint on a port by adding the endpoint element of ServiceManifest.xml (located in the PackageRoot folder) for the Alphabet.Processing service as shown below:</span></span>
   
    ```xml
    <Endpoint Name="ProcessingServiceEndpoint" Port="8089" Protocol="http" Type="Internal" />
    ```
   
    <span data-ttu-id="e741f-225">Agora o serviço está configurado para escutar um ponto de extremidade interno com 26 partições.</span><span class="sxs-lookup"><span data-stu-id="e741f-225">Now the service is configured to listen to an internal endpoint with 26 partitions.</span></span>
7. <span data-ttu-id="e741f-226">Em seguida, substitua o método `CreateServiceReplicaListeners()` da classe Processing.</span><span class="sxs-lookup"><span data-stu-id="e741f-226">Next, you need to override the `CreateServiceReplicaListeners()` method of the Processing class.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e741f-227">Para este exemplo, supomos que você esteja usando um HttpCommunicationListener simples.</span><span class="sxs-lookup"><span data-stu-id="e741f-227">For this sample, we assume that you are using a simple HttpCommunicationListener.</span></span> <span data-ttu-id="e741f-228">Para obter mais informações sobre comunicação de Reliable Service, consulte [O modelo de comunicação de Reliable Service](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="e741f-228">For more information on reliable service communication, see [The Reliable Service communication model](service-fabric-reliable-services-communication.md).</span></span>
   > 
   > 
8. <span data-ttu-id="e741f-229">Um padrão recomendado para a URL que escuta uma réplica é o seguinte formato: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.</span><span class="sxs-lookup"><span data-stu-id="e741f-229">A recommended pattern for the URL that a replica listens on is the following format: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.</span></span>
    <span data-ttu-id="e741f-230">Assim, você deseja configurar o ouvinte de comunicação para escutar nos pontos de extremidade corretos e com esse padrão.</span><span class="sxs-lookup"><span data-stu-id="e741f-230">So you want to configure your communication listener to listen on the correct endpoints and with this pattern.</span></span>
   
    <span data-ttu-id="e741f-231">Várias réplicas do serviço podem ser hospedadas no mesmo computador, portanto, esse endereço deve ser exclusivo para a réplica.</span><span class="sxs-lookup"><span data-stu-id="e741f-231">Multiple replicas of this service may be hosted on the same computer, so this address needs to be unique to the replica.</span></span> <span data-ttu-id="e741f-232">É por isso que a ID de partição + ID da réplica estão na URL.</span><span class="sxs-lookup"><span data-stu-id="e741f-232">This is why   partition ID + replica ID are in the URL.</span></span> <span data-ttu-id="e741f-233">HttpListener pode escutar em vários endereços na mesma porta, se o prefixo de URL for exclusivo.</span><span class="sxs-lookup"><span data-stu-id="e741f-233">HttpListener can listen on multiple addresses on the same port as long as the URL prefix    is unique.</span></span>
   
    <span data-ttu-id="e741f-234">O GUID extra existe para um caso avançado em que as réplicas secundárias também escutam solicitações de somente leitura.</span><span class="sxs-lookup"><span data-stu-id="e741f-234">The extra GUID is there for an advanced case where secondary replicas also listen for read-only requests.</span></span> <span data-ttu-id="e741f-235">Quando esse for o caso, você deve certificar-se de que um novo endereço exclusivo é usado durante a transição do principal para o secundário para forçar os clientes a resolver o endereço novamente.</span><span class="sxs-lookup"><span data-stu-id="e741f-235">When that's the case, you want to make sure that a new unique address is used when transitioning from primary to secondary to force clients to re-resolve the address.</span></span> <span data-ttu-id="e741f-236">'+' é usado como o endereço aqui para que a réplica escute em todos os hosts disponíveis (IP, FQDM, localhost etc.) O código abaixo mostra um exemplo.</span><span class="sxs-lookup"><span data-stu-id="e741f-236">'+' is used as the address here so that the replica listens on all available hosts (IP, FQDM, localhost, etc.) The code below shows an example.</span></span>
   
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
   
    <span data-ttu-id="e741f-237">Também vale a pena observar que a URL publicada é ligeiramente diferente do prefixo da URL de escuta.</span><span class="sxs-lookup"><span data-stu-id="e741f-237">It's also worth noting that the published URL is slightly different from the listening URL prefix.</span></span>
    <span data-ttu-id="e741f-238">A URL de escuta é dada ao HttpListener.</span><span class="sxs-lookup"><span data-stu-id="e741f-238">The listening URL is given to HttpListener.</span></span> <span data-ttu-id="e741f-239">A URL publicada é a URL que será publicada para o Serviço de Nomenclatura da Malha de Serviço, que é usado para descoberta de serviço.</span><span class="sxs-lookup"><span data-stu-id="e741f-239">The published URL is the URL that is published to the Service Fabric Naming Service, which is used for service discovery.</span></span> <span data-ttu-id="e741f-240">Os clientes pedirão esse endereço por meio desse serviço de descoberta.</span><span class="sxs-lookup"><span data-stu-id="e741f-240">Clients will ask for this address through that discovery service.</span></span> <span data-ttu-id="e741f-241">O endereço que os clientes obtêm precisa ter o IP ou o FQDN do nó real para se conectar.</span><span class="sxs-lookup"><span data-stu-id="e741f-241">The address that clients get needs to have the actual IP or FQDN of the node in order to connect.</span></span> <span data-ttu-id="e741f-242">Por isso, você precisa substituir '+' pelo IP ou FQDN do nó conforme mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="e741f-242">So you need to replace '+' with the node's IP or FQDN as shown above.</span></span>
9. <span data-ttu-id="e741f-243">A última etapa é adicionar a lógica de processamento ao serviço, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="e741f-243">The last step is to add the processing logic to the service as shown below.</span></span>
   
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
   
    <span data-ttu-id="e741f-244">`ProcessInternalRequest` lê os valores do parâmetro de cadeia de caracteres da consulta usada para chamar a partição e chama `AddUserAsync` para adicionar o sobrenome ao dicionário confiável `dictionary`.</span><span class="sxs-lookup"><span data-stu-id="e741f-244">`ProcessInternalRequest` reads the values of the query string parameter used to call the partition and calls `AddUserAsync` to add the lastname to the reliable dictionary `dictionary`.</span></span>
10. <span data-ttu-id="e741f-245">Vamos adicionar um serviço sem estado ao projeto para ver como você pode chamar uma partição específica.</span><span class="sxs-lookup"><span data-stu-id="e741f-245">Let's add a stateless service to the project to see how you can call a particular partition.</span></span>
    
    <span data-ttu-id="e741f-246">Esse serviço serve como uma interface web simples que aceita lastname como um parâmetro de cadeia de caracteres de consulta, determina a chave de partição e envia-o para o serviço Alphabet.Processing para processamento.</span><span class="sxs-lookup"><span data-stu-id="e741f-246">This service serves as a simple web interface that accepts the lastname as a query string parameter, determines the partition key, and sends it to the Alphabet.Processing service for processing.</span></span>
11. <span data-ttu-id="e741f-247">Na caixa de diálogo **Criar um Serviço**, escolha o serviço **Sem Estado** e dê a ele o nome de "Alphabet.Web", como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="e741f-247">In the **Create a Service** dialog box, choose **Stateless** service and call it "Alphabet.Web" as shown below.</span></span>
    
    ![Captura de tela de serviço sem estado](./media/service-fabric-concepts-partitioning/createnewstateless.png)<span data-ttu-id="e741f-249">.</span><span class="sxs-lookup"><span data-stu-id="e741f-249">.</span></span>
12. <span data-ttu-id="e741f-250">Atualize as informações de ponto de extremidade no ServiceManifest.xml do serviço Alphabet.WebApi para abrir uma porta, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="e741f-250">Update the endpoint information in the ServiceManifest.xml of the Alphabet.WebApi service to open up a port as shown below.</span></span>
    
    ```xml
    <Endpoint Name="WebApiServiceEndpoint" Protocol="http" Port="8081"/>
    ```
13. <span data-ttu-id="e741f-251">Você precisa retornar uma coleção de ServiceInstanceListeners na classe Web.</span><span class="sxs-lookup"><span data-stu-id="e741f-251">You need to return a collection of ServiceInstanceListeners in the class Web.</span></span> <span data-ttu-id="e741f-252">Novamente, você pode optar por implementar um HttpCommunicationListener simples.</span><span class="sxs-lookup"><span data-stu-id="e741f-252">Again, you can choose to implement a simple HttpCommunicationListener.</span></span>
    
    ```CSharp
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] {new ServiceInstanceListener(context => this.CreateInputListener(context))};
    }
    private ICommunicationListener CreateInputListener(ServiceContext context)
    {
        // Service instance's URL is the node's IP & desired port
        EndpointResourceDescription inputEndpoint = context.CodePackageActivationContext.GetEndpoint("WebApiServiceEndpoint")
        string uriPrefix = String.Format("{0}://+:{1}/alphabetpartitions/", inputEndpoint.Protocol, inputEndpoint.Port);
        var uriPublished = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
        return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInputRequest);
    }
    ```
14. <span data-ttu-id="e741f-253">Agora você precisa implementar a lógica de processamento.</span><span class="sxs-lookup"><span data-stu-id="e741f-253">Now you need to implement the processing logic.</span></span> <span data-ttu-id="e741f-254">O HttpCommunicationListener chama `ProcessInputRequest` quando chega uma solicitação.</span><span class="sxs-lookup"><span data-stu-id="e741f-254">The HttpCommunicationListener calls `ProcessInputRequest` when a request comes in.</span></span> <span data-ttu-id="e741f-255">Vamos prosseguir e adicionar o código a abaixo.</span><span class="sxs-lookup"><span data-stu-id="e741f-255">So let's go ahead and add the code below.</span></span>
    
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
                    "Result: {0}. <p>Partition key: '{1}' generated from the first letter '{2}' of input value '{3}'. <br>Processing service partition ID: {4}. <br>Processing service replica address: {5}",
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
                output = output + "added to Partition: " + primaryReplicaAddress;
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    ```
    
    <span data-ttu-id="e741f-256">Vamos ver o passo a passo.</span><span class="sxs-lookup"><span data-stu-id="e741f-256">Let's walk through it step by step.</span></span> <span data-ttu-id="e741f-257">O código lê a primeira letra do parâmetro da cadeia de caracteres de consulta `lastname` dentro de um char.</span><span class="sxs-lookup"><span data-stu-id="e741f-257">The code reads the first letter of the query string parameter `lastname` into a char.</span></span> <span data-ttu-id="e741f-258">Isso determina a chave de partição para essa letra, subtraindo o valor hexadecimal de `A` do valor hexadecimal da primeira letra do último nome.</span><span class="sxs-lookup"><span data-stu-id="e741f-258">Then, it determines the partition key for this letter by subtracting the hexadecimal value of `A` from the hexadecimal value of the last names' first letter.</span></span>
    
    ```CSharp
    string lastname = context.Request.QueryString["lastname"];
    char firstLetterOfLastName = lastname.First();
    ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    ```
    
    <span data-ttu-id="e741f-259">Lembre-se de que, neste exemplo, estamos usando 26 partições com uma chave de partição por partição.</span><span class="sxs-lookup"><span data-stu-id="e741f-259">Remember, for this example, we are using 26 partitions with one partition key per partition.</span></span>
    <span data-ttu-id="e741f-260">Em seguida, obtemos a partição de serviço `partition` para essa chave usando o método `ResolveAsync` no objeto `servicePartitionResolver`.</span><span class="sxs-lookup"><span data-stu-id="e741f-260">Next, we obtain the service partition `partition` for this key by using the `ResolveAsync` method on the `servicePartitionResolver` object.</span></span> <span data-ttu-id="e741f-261">`servicePartitionResolver` é definido como</span><span class="sxs-lookup"><span data-stu-id="e741f-261">`servicePartitionResolver` is defined as</span></span>
    
    ```CSharp
    private readonly ServicePartitionResolver servicePartitionResolver = ServicePartitionResolver.GetDefault();
    ```
    
    <span data-ttu-id="e741f-262">O método `ResolveAsync` usa o URI do serviço, a chave da partição e um token de cancelamento como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="e741f-262">The `ResolveAsync` method takes the service URI, the partition key, and a cancellation token as parameters.</span></span> <span data-ttu-id="e741f-263">O URI do serviço para o serviço de processamento é `fabric:/AlphabetPartitions/Processing`.</span><span class="sxs-lookup"><span data-stu-id="e741f-263">The service URI for the processing service is `fabric:/AlphabetPartitions/Processing`.</span></span> <span data-ttu-id="e741f-264">Em seguida, obtemos o ponto de extremidade da partição.</span><span class="sxs-lookup"><span data-stu-id="e741f-264">Next, we get the endpoint of the partition.</span></span>
    
    ```CSharp
    ResolvedServiceEndpoint ep = partition.GetEndpoint()
    ```
    
    <span data-ttu-id="e741f-265">Por fim, criamos a URL do ponto de extremidade mais a querystring e chamamos o serviço de processamento.</span><span class="sxs-lookup"><span data-stu-id="e741f-265">Finally, we build the endpoint URL plus the querystring and call the processing service.</span></span>
    
    ```CSharp
    JObject addresses = JObject.Parse(ep.Address);
    string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
    UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
    primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
    string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    ```
    
    <span data-ttu-id="e741f-266">Após a conclusão do processamento, podemos gravar a saída de volta.</span><span class="sxs-lookup"><span data-stu-id="e741f-266">Once the processing is done, we write the output back.</span></span>
15. <span data-ttu-id="e741f-267">A última etapa é testar o serviço.</span><span class="sxs-lookup"><span data-stu-id="e741f-267">The last step is to test the service.</span></span> <span data-ttu-id="e741f-268">O Visual Studio usa parâmetros do aplicativo para implantação local e na nuvem.</span><span class="sxs-lookup"><span data-stu-id="e741f-268">Visual Studio uses application parameters for local and cloud deployment.</span></span> <span data-ttu-id="e741f-269">Para testar o serviço com 26 partições localmente, atualize o arquivo `Local.xml` na pasta ApplicationParameters do projeto AlphabetPartitions, como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="e741f-269">To test the service with 26 partitions locally, you need to update the `Local.xml` file in the ApplicationParameters folder of the AlphabetPartitions project as shown below:</span></span>
    
    ```xml
    <Parameters>
      <Parameter Name="Processing_PartitionCount" Value="26" />
      <Parameter Name="WebApi_InstanceCount" Value="1" />
    </Parameters>
    ```
16. <span data-ttu-id="e741f-270">Depois de concluir a implantação, você pode verificar o serviço e todas as respectivas partições no Gerenciador do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e741f-270">Once you finish deployment, you can check the service and all of its partitions in the Service Fabric Explorer.</span></span>
    
    ![Captura de tela do Gerenciador do Service Fabric](./media/service-fabric-concepts-partitioning/sfxpartitions.png)
17. <span data-ttu-id="e741f-272">Insira `http://localhost:8081/?lastname=somename`em um navegador para testar a lógica de particionamento.</span><span class="sxs-lookup"><span data-stu-id="e741f-272">In a browser, you can test the partitioning logic by entering `http://localhost:8081/?lastname=somename`.</span></span> <span data-ttu-id="e741f-273">Você verá que cada sobrenome iniciado com a mesma letra está sendo armazenado na mesma partição.</span><span class="sxs-lookup"><span data-stu-id="e741f-273">You will see that each last name that starts with the same letter is being stored in the same partition.</span></span>
    
    ![Captura de tela do navegador](./media/service-fabric-concepts-partitioning/samplerunning.png)

<span data-ttu-id="e741f-275">O código-fonte completo do exemplo está disponível no [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span><span class="sxs-lookup"><span data-stu-id="e741f-275">The entire source code of the sample is available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e741f-276">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e741f-276">Next steps</span></span>
<span data-ttu-id="e741f-277">Para obter informações sobre os conceitos de malha do serviço, consulte:</span><span class="sxs-lookup"><span data-stu-id="e741f-277">For information on Service Fabric concepts, see the following:</span></span>

* [<span data-ttu-id="e741f-278">Disponibilidade dos serviços de malha do serviço</span><span class="sxs-lookup"><span data-stu-id="e741f-278">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="e741f-279">Escalabilidade de serviços da Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="e741f-279">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="e741f-280">Planejamento de capacidade para Aplicativos do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e741f-280">Capacity planning for Service Fabric applications</span></span>](service-fabric-capacity-planning.md)

[wikipartition]: https://en.wikipedia.org/wiki/Partition_(database)

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png