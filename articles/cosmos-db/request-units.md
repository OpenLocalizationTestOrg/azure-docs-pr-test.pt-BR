---
title: "Unidades de solicitação e estimativa de produtividade – Azure Cosmos DB | Microsoft Docs"
description: "Saiba mais sobre como entender, especificar e estimar os requisitos de unidades de solicitação no Azure Cosmos DB."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: d0a3c310-eb63-4e45-8122-b7724095c32f
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 7a4efc0fb9b3855b9dbbe445768ceb2a9940d0b2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="request-units-in-azure-cosmos-db"></a><span data-ttu-id="22f77-103">Unidades de Solicitação no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="22f77-103">Request Units in Azure Cosmos DB</span></span>
<span data-ttu-id="22f77-104">Agora disponível: [calculadora de unidades de solicitação](https://www.documentdb.com/capacityplanner) do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="22f77-104">Now available: Azure Cosmos DB [request unit calculator](https://www.documentdb.com/capacityplanner).</span></span> <span data-ttu-id="22f77-105">Saiba mais em [Estimativa das necessidades de produção](request-units.md#estimating-throughput-needs).</span><span class="sxs-lookup"><span data-stu-id="22f77-105">Learn more in [Estimating your throughput needs](request-units.md#estimating-throughput-needs).</span></span>

![Calculadora de produtividade][5]

## <a name="introduction"></a><span data-ttu-id="22f77-107">Introdução</span><span class="sxs-lookup"><span data-stu-id="22f77-107">Introduction</span></span>
<span data-ttu-id="22f77-108">O [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) é o multimodelo de banco de dados distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="22f77-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is Microsoft's globally distributed multi-model database.</span></span> <span data-ttu-id="22f77-109">Com o Azure Cosmos DB, você não precisa alugar máquinas virtuais, implantar softwares ou monitorar bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="22f77-109">With Azure Cosmos DB, you don't have to rent virtual machines, deploy software, or monitor databases.</span></span> <span data-ttu-id="22f77-110">O Azure Cosmos DB é operado e continuamente monitorado pelos melhores engenheiros da Microsoft para fornecer disponibilidade, desempenho e proteção de dados da mais alta qualidade.</span><span class="sxs-lookup"><span data-stu-id="22f77-110">Azure Cosmos DB is operated and continuously monitored by Microsoft top engineers to deliver world class availability, performance, and data protection.</span></span> <span data-ttu-id="22f77-111">Você pode acessar seus dados usando as APIs de sua preferência, como [SQL do DocumentDB](documentdb-sql-query.md) (documento), MongoDB (documento), [Armazenamento de Tabelas do Azure](https://azure.microsoft.com/services/storage/tables/) (chave-valor) e [Gremlin](https://tinkerpop.apache.org/gremlin.html) (gráfico), todas com suporte nativo.</span><span class="sxs-lookup"><span data-stu-id="22f77-111">You can access your data using APIs of your choice, as [DocumentDB SQL](documentdb-sql-query.md) (document), MongoDB (document), [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/) (key-value), and [Gremlin](https://tinkerpop.apache.org/gremlin.html) (graph) are all natively supported.</span></span> <span data-ttu-id="22f77-112">A moeda do Azure Cosmos DB é a RU (Unidade de Solicitação).</span><span class="sxs-lookup"><span data-stu-id="22f77-112">The currency of Azure Cosmos DB is the Request Unit (RU).</span></span> <span data-ttu-id="22f77-113">Com RUs, você não precisa reservar capacidades de leitura/gravação nem provisionar CPU, Memória e IOPS.</span><span class="sxs-lookup"><span data-stu-id="22f77-113">With RUs, you do not need to reserve read/write capacities or provision CPU, Memory and IOPS.</span></span>

<span data-ttu-id="22f77-114">O Azure Cosmos DB dá suporte a uma série de APIs com operações diferentes que variam de leituras e gravações simples a consultas de gráfico complexas.</span><span class="sxs-lookup"><span data-stu-id="22f77-114">Azure Cosmos DB supports a number of APIs with different operations ranging from simple reads and writes to complex graph queries.</span></span> <span data-ttu-id="22f77-115">Como nem todas as solicitações são iguais, elas são atribuídas a uma quantidade normalizada de **unidades de solicitação** com base na quantidade de computação necessária para atender à solicitação.</span><span class="sxs-lookup"><span data-stu-id="22f77-115">Since not all requests are equal, they are assigned a normalized quantity of **request units** based on the amount of computation required to serve the request.</span></span> <span data-ttu-id="22f77-116">O número de unidades de solicitação de uma operação é determinístico e você pode acompanhar o número de unidades de solicitação consumidas por uma operação no Azure Cosmos DB por meio de um cabeçalho de resposta.</span><span class="sxs-lookup"><span data-stu-id="22f77-116">The number of request units for an operation is deterministic, and you can track the number of request units consumed by any operation in Azure Cosmos DB via a response header.</span></span> 

<span data-ttu-id="22f77-117">Para fornecer um desempenho previsível, você precisa reservar a produtividade em unidades de 100 RUs/segundo.</span><span class="sxs-lookup"><span data-stu-id="22f77-117">To provide predictable performance, you need to reserve throughput in units of 100 RU/second.</span></span> 

<span data-ttu-id="22f77-118">Após ler este artigo, você poderá responder as perguntas a seguir:</span><span class="sxs-lookup"><span data-stu-id="22f77-118">After reading this article, you'll be able to answer the following questions:</span></span>  

* <span data-ttu-id="22f77-119">O que são unidades de solicitação e solicitações de encargos?</span><span class="sxs-lookup"><span data-stu-id="22f77-119">What are request units and request charges?</span></span>
* <span data-ttu-id="22f77-120">Como especificar a capacidade da unidade de solicitação para uma coleção?</span><span class="sxs-lookup"><span data-stu-id="22f77-120">How do I specify request unit capacity for a collection?</span></span>
* <span data-ttu-id="22f77-121">Como estimar as necessidades de unidades de solicitação de meu aplicativo?</span><span class="sxs-lookup"><span data-stu-id="22f77-121">How do I estimate my application's request unit needs?</span></span>
* <span data-ttu-id="22f77-122">O que acontecerá se eu exceder a capacidade da unidade de solicitação de uma coleção?</span><span class="sxs-lookup"><span data-stu-id="22f77-122">What happens if I exceed request unit capacity for a collection?</span></span>

<span data-ttu-id="22f77-123">Como o Azure Cosmos DB é um multimodelo de banco de dados, é importante observar que nos referiremos a uma coleção ou um documento como uma API de documento, um gráfico/nó como uma API de gráfico e uma tabela/entidade como uma API de tabela.</span><span class="sxs-lookup"><span data-stu-id="22f77-123">As Azure Cosmos DB is a multi-model database, it is important to note that we will refer to a collection/document for a document API, a graph/node for a graph API and a table/entity for table API.</span></span> <span data-ttu-id="22f77-124">Neste documento, para produtividade, generalizaremos como os conceitos de contêiner/item.</span><span class="sxs-lookup"><span data-stu-id="22f77-124">Throughput this document we will generalize to the concepts of container/item.</span></span>

## <a name="request-units-and-request-charges"></a><span data-ttu-id="22f77-125">Unidades de solicitação e solicitações de encargos</span><span class="sxs-lookup"><span data-stu-id="22f77-125">Request units and request charges</span></span>
<span data-ttu-id="22f77-126">O Azure Cosmos DB fornece desempenho rápido e previsível *reservando* recursos para atender às necessidades de produtividade do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="22f77-126">Azure Cosmos DB delivers fast, predictable performance by *reserving* resources to satisfy your application's throughput needs.</span></span>  <span data-ttu-id="22f77-127">Como os padrões de carga e acesso do aplicativo mudam com o tempo, o Azure Cosmos DB permite que você aumente ou diminua facilmente a quantidade de produtividade reservada disponível para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="22f77-127">Because application load and access patterns change over time, Azure Cosmos DB allows you to easily increase or decrease the amount of reserved throughput available to your application.</span></span>

<span data-ttu-id="22f77-128">Com o Azure Cosmos DB, a produtividade reservada é especificada em termos de processamento de unidades de solicitação por segundo.</span><span class="sxs-lookup"><span data-stu-id="22f77-128">With Azure Cosmos DB, reserved throughput is specified in terms of request units processing per second.</span></span> <span data-ttu-id="22f77-129">Você pode considerar as unidades de solicitação como a moeda de produtividade, com as quais você *reserva* uma quantidade de unidades de solicitação garantidas disponíveis para o aplicativo por segundo.</span><span class="sxs-lookup"><span data-stu-id="22f77-129">You can think of request units as throughput currency, whereby you *reserve* an amount of guaranteed request units available to your application on per second basis.</span></span>  <span data-ttu-id="22f77-130">Cada operação do Azure Cosmos DB – gravar um documento, realizar uma consulta, atualizar um documento – consome CPU, memória e IOPS.</span><span class="sxs-lookup"><span data-stu-id="22f77-130">Each operation in Azure Cosmos DB - writing a document, performing a query, updating a document - consumes CPU, memory, and IOPS.</span></span>  <span data-ttu-id="22f77-131">Ou seja, cada operação resulta em um *encargo de solicitação*, que é expressa em *unidades de solicitação*.</span><span class="sxs-lookup"><span data-stu-id="22f77-131">That is, each operation incurs a *request charge*, which is expressed in *request units*.</span></span>  <span data-ttu-id="22f77-132">Ao entender os fatores que afetam os encargos de unidade de solicitação e os requisitos de taxa de transferência do aplicativo, você pode executar o aplicativo da maneira mais econômica possível.</span><span class="sxs-lookup"><span data-stu-id="22f77-132">Understanding the factors which impact request unit charges, along with your application's throughput requirements, enables you to run your application as cost effectively as possible.</span></span> <span data-ttu-id="22f77-133">O gerenciador de consultas também é uma ferramenta excelente para testar o núcleo de uma consulta.</span><span class="sxs-lookup"><span data-stu-id="22f77-133">The query explorer is also a wonderful tool to test the core of a query.</span></span>

<span data-ttu-id="22f77-134">Recomendamos que você comece assistindo ao vídeo a seguir, no qual Aravind Ramachandran explica as unidades de solicitação e o desempenho previsível com o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="22f77-134">We recommend getting started by watching the following video, where Aravind Ramachandran explains request units and predictable performance with Azure Cosmos DB.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Predictable-Performance-with-DocumentDB/player]
> 
> 

## <a name="specifying-request-unit-capacity-in-azure-cosmos-db"></a><span data-ttu-id="22f77-135">Especificando a capacidade de unidades de solicitação no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="22f77-135">Specifying request unit capacity in Azure Cosmos DB</span></span>
<span data-ttu-id="22f77-136">Ao iniciar uma nova coleção, tabela ou um novo gráfico, especifique o número de unidades de solicitação por segundo (RU por segundo) que você deseja ter reservado.</span><span class="sxs-lookup"><span data-stu-id="22f77-136">When starting a new collection, table or graph, you specify the number of request units per second (RU per second) you want reserved.</span></span> <span data-ttu-id="22f77-137">Com base na produtividade provisionada, o Azure Cosmos DB aloca partições físicas para hospedar sua coleção e divide/redistribui os dados entre partições conforme eles aumentam.</span><span class="sxs-lookup"><span data-stu-id="22f77-137">Based on the provisioned throughput, Azure Cosmos DB allocates physical partitions to host your collection and splits/rebalances data across partitions as it grows.</span></span>

<span data-ttu-id="22f77-138">O Azure Cosmos DB exige que uma chave de partição seja especificada quando uma coleção é provisionada com 2.500 unidades de solicitação ou mais.</span><span class="sxs-lookup"><span data-stu-id="22f77-138">Azure Cosmos DB requires a partition key to be specified when a collection is provisioned with 2,500 request units or higher.</span></span> <span data-ttu-id="22f77-139">Uma chave de partição também é necessária para dimensionar a produtividade da coleção além das 2.500 unidades de solicitação no futuro.</span><span class="sxs-lookup"><span data-stu-id="22f77-139">A partition key is also required to scale your collection's throughput beyond 2,500 request units in the future.</span></span> <span data-ttu-id="22f77-140">Portanto, é altamente recomendável configurar uma [chave de partição](partition-data.md) durante a criação de um contêiner, independentemente da produtividade inicial.</span><span class="sxs-lookup"><span data-stu-id="22f77-140">Therefore, it is highly recommended to configure a [partition key](partition-data.md) when creating a container regardless of your initial throughput.</span></span> <span data-ttu-id="22f77-141">Como os dados podem estar divididos em várias partições, é necessário escolher uma chave de partição que tem uma cardinalidade alta (centenas a milhões de valores distintos), de forma que a coleção, a tabela ou o gráfico e as solicitações possam ser dimensionados de maneira uniforme pelo Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="22f77-141">Since your data might have to be split across multiple partitions, it is necessary to pick a partition key that has a high cardinality (100 to millions of distinct values) so that your collection/table/graph and requests can be scaled uniformly by Azure Cosmos DB.</span></span> 

> [!NOTE]
> <span data-ttu-id="22f77-142">Uma chave de partição é um limite lógico e não físico.</span><span class="sxs-lookup"><span data-stu-id="22f77-142">A partition key is a logical boundary, and not a physical one.</span></span> <span data-ttu-id="22f77-143">Portanto, não é necessário limitar o número de valores de chave de partição distinta.</span><span class="sxs-lookup"><span data-stu-id="22f77-143">Therefore, you do not need to limit the number of distinct partition key values.</span></span> <span data-ttu-id="22f77-144">Na verdade, já que o Azure Cosmos DB tem mais opções de balanceamento de carga, é melhor ter mais valores de chave de partição distintos do que menos.</span><span class="sxs-lookup"><span data-stu-id="22f77-144">It is in fact better to have more distinct partition key values than less, as Azure Cosmos DB has more load balancing options.</span></span>

<span data-ttu-id="22f77-145">Segue um trecho de código para criar uma coleção com 3.000 unidades de solicitação por segundo usando o SDK do .NET:</span><span class="sxs-lookup"><span data-stu-id="22f77-145">Here is a code snippet for creating a collection with 3,000 request units per second using the .NET SDK:</span></span>

```csharp
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000 });
```

<span data-ttu-id="22f77-146">O Azure Cosmos DB opera em um modelo de reserva na produtividade.</span><span class="sxs-lookup"><span data-stu-id="22f77-146">Azure Cosmos DB operates on a reservation model on throughput.</span></span> <span data-ttu-id="22f77-147">Ou seja, você será cobrado pela quantidade de produtividade *reservada*, independentemente do quanto da produtividade estiver em *uso*.</span><span class="sxs-lookup"><span data-stu-id="22f77-147">That is, you are billed for the amount of throughput *reserved*, regardless of how much of that throughput is actively *used*.</span></span> <span data-ttu-id="22f77-148">À medida que a carga, os dados e os padrões de uso do aplicativo mudarem, você poderá aumentar ou reduzir verticalmente a quantidade de RUs reservadas por meio de SDKs ou usando o [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="22f77-148">As your application's load, data, and usage patterns change you can easily scale up and down the amount of reserved RUs through SDKs or using the [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="22f77-149">Cada coleção/tabela/gráfico é mapeado para um recurso `Offer` no Azure Cosmos DB, que tem metadados sobre a produtividade provisionada.</span><span class="sxs-lookup"><span data-stu-id="22f77-149">Each collection/table/graph are mapped to an `Offer` resource in Azure Cosmos DB, which has metadata about the provisioned throughput.</span></span> <span data-ttu-id="22f77-150">Altere a produtividade alocada procurando o recurso de oferta correspondente de um contêiner e, em seguida, atualizando-o com o novo valor de produtividade.</span><span class="sxs-lookup"><span data-stu-id="22f77-150">You can change the allocated throughput by looking up the corresponding offer resource for a container, then updating it with the new throughput value.</span></span> <span data-ttu-id="22f77-151">Aqui está um trecho de código para alterar a taxa de transferência de uma coleção para 5.000 unidades de solicitação por segundo usando o SDK do .NET:</span><span class="sxs-lookup"><span data-stu-id="22f77-151">Here is a code snippet for changing the throughput of a collection to 5,000 request units per second using the .NET SDK:</span></span>

```csharp
// Fetch the resource to be updated
Offer offer = client.CreateOfferQuery()
                .Where(r => r.ResourceLink == collection.SelfLink)    
                .AsEnumerable()
                .SingleOrDefault();

// Set the throughput to 5000 request units per second
offer = new OfferV2(offer, 5000);

// Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offer);
```

<span data-ttu-id="22f77-152">Não há nenhum impacto sobre a disponibilidade do contêiner quando a produtividade é alterada.</span><span class="sxs-lookup"><span data-stu-id="22f77-152">There is no impact to the availability of your container when you change the throughput.</span></span> <span data-ttu-id="22f77-153">Normalmente, a nova taxa de transferência reservada se torna eficaz em segundos no aplicativo da nova taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="22f77-153">Typically the new reserved throughput is effective within seconds on application of the new throughput.</span></span>

## <a name="request-unit-considerations"></a><span data-ttu-id="22f77-154">Considerações sobre unidades de solicitação</span><span class="sxs-lookup"><span data-stu-id="22f77-154">Request unit considerations</span></span>
<span data-ttu-id="22f77-155">Ao estimar o número de unidades de solicitação a ser reservado para o contêiner do Azure Cosmos DB, é importante considerar as seguintes variáveis:</span><span class="sxs-lookup"><span data-stu-id="22f77-155">When estimating the number of request units to reserve for your Azure Cosmos DB container, it is important to take the following variables into consideration:</span></span>

* <span data-ttu-id="22f77-156">**Tamanho do item**.</span><span class="sxs-lookup"><span data-stu-id="22f77-156">**Item size**.</span></span> <span data-ttu-id="22f77-157">À medida que o tamanho aumentar, as unidades consumidas para ler ou gravar os dados também aumentarão.</span><span class="sxs-lookup"><span data-stu-id="22f77-157">As size increases the units consumed to read or write the data will also increase.</span></span>
* <span data-ttu-id="22f77-158">**Contagem de propriedades do item**.</span><span class="sxs-lookup"><span data-stu-id="22f77-158">**Item property count**.</span></span> <span data-ttu-id="22f77-159">Pressupondo a indexação padrão de todas as propriedades, as unidades consumidas para gravar um documento, um nó ou uma entidade aumentarão conforme a contagem de propriedades aumentar.</span><span class="sxs-lookup"><span data-stu-id="22f77-159">Assuming default indexing of all properties, the units consumed to write a document/node/ntity will increase as the property count increases.</span></span>
* <span data-ttu-id="22f77-160">**Consistência de dados**.</span><span class="sxs-lookup"><span data-stu-id="22f77-160">**Data consistency**.</span></span> <span data-ttu-id="22f77-161">Ao usar os níveis de consistência de dados Forte ou Desatualização Limitada, unidades adicionais serão consumidas para ler os itens.</span><span class="sxs-lookup"><span data-stu-id="22f77-161">When using data consistency levels of Strong or Bounded Staleness, additional units will be consumed to read items.</span></span>
* <span data-ttu-id="22f77-162">**Propriedades indexadas**.</span><span class="sxs-lookup"><span data-stu-id="22f77-162">**Indexed properties**.</span></span> <span data-ttu-id="22f77-163">Uma política de índice em cada contêiner determina quais propriedades são indexadas por padrão.</span><span class="sxs-lookup"><span data-stu-id="22f77-163">An index policy on each container determines which properties are indexed by default.</span></span> <span data-ttu-id="22f77-164">Você pode reduzir o consumo de unidades de solicitação limitando o número de propriedades indexadas ou habilitando a indexação lenta.</span><span class="sxs-lookup"><span data-stu-id="22f77-164">You can reduce your request unit consumption by limiting the number of indexed properties or by enabling lazy indexing.</span></span>
* <span data-ttu-id="22f77-165">**Indexação de documentos**.</span><span class="sxs-lookup"><span data-stu-id="22f77-165">**Document indexing**.</span></span> <span data-ttu-id="22f77-166">Por padrão, cada item é indexado automaticamente. Você consumirá menos unidades de solicitação se optar por não indexar alguns dos itens.</span><span class="sxs-lookup"><span data-stu-id="22f77-166">By default each item is automatically indexed, you will consume fewer request units if you choose not to index some of your items.</span></span>
* <span data-ttu-id="22f77-167">**Padrões de consulta**.</span><span class="sxs-lookup"><span data-stu-id="22f77-167">**Query patterns**.</span></span> <span data-ttu-id="22f77-168">A complexidade de uma consulta afeta a quantidade de Unidades de Solicitação que são consumidas para uma operação.</span><span class="sxs-lookup"><span data-stu-id="22f77-168">The complexity of a query impacts how many Request Units are consumed for an operation.</span></span> <span data-ttu-id="22f77-169">O número de predicados, a natureza dos predicados, as projeções, o número de UDFs e o tamanho do conjunto de dados de origem influenciam o custo das operações de consulta.</span><span class="sxs-lookup"><span data-stu-id="22f77-169">The number of predicates, nature of the predicates, projections, number of UDFs, and the size of the source data set all influence the cost of query operations.</span></span>
* <span data-ttu-id="22f77-170">**Uso de scripts**.</span><span class="sxs-lookup"><span data-stu-id="22f77-170">**Script usage**.</span></span>  <span data-ttu-id="22f77-171">Assim como ocorre com as consultas, os procedimentos armazenados e os gatilhos consomem unidades de solicitação com base na complexidade das operações que estão sendo executadas.</span><span class="sxs-lookup"><span data-stu-id="22f77-171">As with queries, stored procedures and triggers consume request units based on the complexity of the operations being performed.</span></span> <span data-ttu-id="22f77-172">À medida que desenvolver seu aplicativo, inspecione o cabeçalho de solicitação de carga para entender melhor como cada operação está consumindo a capacidade de unidades de solicitação.</span><span class="sxs-lookup"><span data-stu-id="22f77-172">As you develop your application, inspect the request charge header to better understand how each operation is consuming request unit capacity.</span></span>

## <a name="estimating-throughput-needs"></a><span data-ttu-id="22f77-173">Estimativa das necessidades de produção</span><span class="sxs-lookup"><span data-stu-id="22f77-173">Estimating throughput needs</span></span>
<span data-ttu-id="22f77-174">Uma unidade de solicitação é uma medida normalizada de custo de processamento de solicitação.</span><span class="sxs-lookup"><span data-stu-id="22f77-174">A request unit is a normalized measure of request processing cost.</span></span> <span data-ttu-id="22f77-175">Uma única unidade de solicitação representa a capacidade de processamento necessária para ler (por meio de self link ou ID) um único item de 1 KB que consiste em 10 valores de propriedade exclusivos (excluindo as propriedades do sistema).</span><span class="sxs-lookup"><span data-stu-id="22f77-175">A single request unit represents the processing capacity required to read (via self link or id) a single 1KB item consisting of 10 unique property values (excluding system properties).</span></span> <span data-ttu-id="22f77-176">Uma solicitação para criar (inserir), substituir ou excluir o mesmo item consumirá mais processamento do serviço e, assim, mais unidades de solicitação.</span><span class="sxs-lookup"><span data-stu-id="22f77-176">A request to create (insert), replace or delete the same item will consume more processing from the service and thereby more request units.</span></span>   

> [!NOTE]
> <span data-ttu-id="22f77-177">A linha de base de 1 unidade de solicitação para um item de 1 KB corresponde a um GET simples por self link ou ID do item.</span><span class="sxs-lookup"><span data-stu-id="22f77-177">The baseline of 1 request unit for a 1KB item corresponds to a simple GET by self link or id of the item.</span></span>
> 
> 

<span data-ttu-id="22f77-178">Por exemplo, esta é uma tabela que mostra quantas unidades de solicitação devem ser provisionadas em três tamanhos de item diferentes (1 KB, 4 KB e 64 KB) e em dois níveis de desempenho diferentes (500 leituras/segundo + 100 gravações/segundo e 500 leituras/segundo + 500 gravações/segundo).</span><span class="sxs-lookup"><span data-stu-id="22f77-178">For example, here's a table that shows how many request units to provision at three different item sizes (1KB, 4KB, and 64KB) and at two different performance levels (500 reads/second + 100 writes/second and 500 reads/second + 500 writes/second).</span></span> <span data-ttu-id="22f77-179">A consistência dos dados foi configurada em Sessão e a política de indexação foi definida como Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="22f77-179">The data consistency was configured at Session, and the indexing policy was set to None.</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="22f77-180"><strong>Tamanho do item</strong></span><span class="sxs-lookup"><span data-stu-id="22f77-180"><strong>Item size</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="22f77-181"><strong>Leituras/segundo</strong></span><span class="sxs-lookup"><span data-stu-id="22f77-181"><strong>Reads/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="22f77-182"><strong>Gravações/segundo</strong></span><span class="sxs-lookup"><span data-stu-id="22f77-182"><strong>Writes/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="22f77-183"><strong>Unidades de solicitação</strong></span><span class="sxs-lookup"><span data-stu-id="22f77-183"><strong>Request units</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="22f77-184">1 KB</span><span class="sxs-lookup"><span data-stu-id="22f77-184">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="22f77-185">500</span><span class="sxs-lookup"><span data-stu-id="22f77-185">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="22f77-186">100</span><span class="sxs-lookup"><span data-stu-id="22f77-186">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="22f77-187">(500 * 1) + (100 * 5) = 1.000 RU/s</span><span class="sxs-lookup"><span data-stu-id="22f77-187">(500 * 1) + (100 * 5) = 1,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="22f77-188">1 KB</span><span class="sxs-lookup"><span data-stu-id="22f77-188">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="22f77-189">500</span><span class="sxs-lookup"><span data-stu-id="22f77-189">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="22f77-190">500</span><span class="sxs-lookup"><span data-stu-id="22f77-190">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="22f77-191">(500 * 1) + (500 * 5) = 3.000 RU/s</span><span class="sxs-lookup"><span data-stu-id="22f77-191">(500 * 1) + (500 * 5) = 3,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="22f77-192">4 KB</span><span class="sxs-lookup"><span data-stu-id="22f77-192">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="22f77-193">500</span><span class="sxs-lookup"><span data-stu-id="22f77-193">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="22f77-194">100</span><span class="sxs-lookup"><span data-stu-id="22f77-194">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="22f77-195">(500 * 1,3) + (100 * 7) = 1.350 RU/s</span><span class="sxs-lookup"><span data-stu-id="22f77-195">(500 * 1.3) + (100 * 7) = 1,350 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="22f77-196">4 KB</span><span class="sxs-lookup"><span data-stu-id="22f77-196">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="22f77-197">500</span><span class="sxs-lookup"><span data-stu-id="22f77-197">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="22f77-198">500</span><span class="sxs-lookup"><span data-stu-id="22f77-198">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="22f77-199">(500 * 1,3) + (500 * 7) = 4.150 RU/s</span><span class="sxs-lookup"><span data-stu-id="22f77-199">(500 * 1.3) + (500 * 7) = 4,150 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="22f77-200">64 KB</span><span class="sxs-lookup"><span data-stu-id="22f77-200">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="22f77-201">500</span><span class="sxs-lookup"><span data-stu-id="22f77-201">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="22f77-202">100</span><span class="sxs-lookup"><span data-stu-id="22f77-202">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="22f77-203">(500 * 10) + (100 * 48) = 9.800 RU/s</span><span class="sxs-lookup"><span data-stu-id="22f77-203">(500 * 10) + (100 * 48) = 9,800 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="22f77-204">64 KB</span><span class="sxs-lookup"><span data-stu-id="22f77-204">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="22f77-205">500</span><span class="sxs-lookup"><span data-stu-id="22f77-205">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="22f77-206">500</span><span class="sxs-lookup"><span data-stu-id="22f77-206">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="22f77-207">(500 * 10) + (500 * 48) = 29.000 RU/s</span><span class="sxs-lookup"><span data-stu-id="22f77-207">(500 * 10) + (500 * 48) = 29,000 RU/s</span></span></p></td>
        </tr>
    </tbody>
</table>

### <a name="use-the-request-unit-calculator"></a><span data-ttu-id="22f77-208">Usar a calculadora de unidade de solicitação</span><span class="sxs-lookup"><span data-stu-id="22f77-208">Use the request unit calculator</span></span>
<span data-ttu-id="22f77-209">Para ajudar os clientes a ajustar as estimativas de produtividade, há uma [calculadora de unidade de solicitação](https://www.documentdb.com/capacityplanner) baseada na Web que ajuda a fazer uma estimativa dos requisitos de unidade de solicitação para operações comuns, incluindo:</span><span class="sxs-lookup"><span data-stu-id="22f77-209">To help customers fine tune their throughput estimations, there is a web based [request unit calculator](https://www.documentdb.com/capacityplanner) to help estimate the request unit requirements for typical operations, including:</span></span>

* <span data-ttu-id="22f77-210">Criações de itens (gravações)</span><span class="sxs-lookup"><span data-stu-id="22f77-210">Item creates (writes)</span></span>
* <span data-ttu-id="22f77-211">Leituras de itens</span><span class="sxs-lookup"><span data-stu-id="22f77-211">Item reads</span></span>
* <span data-ttu-id="22f77-212">Exclusões de itens</span><span class="sxs-lookup"><span data-stu-id="22f77-212">Item deletes</span></span>
* <span data-ttu-id="22f77-213">Atualizações de itens</span><span class="sxs-lookup"><span data-stu-id="22f77-213">Item updates</span></span>

<span data-ttu-id="22f77-214">A ferramenta também inclui suporte para estimar as necessidades de armazenamento de dados com base nos itens de exemplo fornecidos.</span><span class="sxs-lookup"><span data-stu-id="22f77-214">The tool also includes support for estimating data storage needs based on the sample items you provide.</span></span>

<span data-ttu-id="22f77-215">Usar a ferramenta é simples:</span><span class="sxs-lookup"><span data-stu-id="22f77-215">Using the tool is simple:</span></span>

1. <span data-ttu-id="22f77-216">Carregue um ou mais itens representativos.</span><span class="sxs-lookup"><span data-stu-id="22f77-216">Upload one or more representative items.</span></span>
   
    ![Carregar itens na calculadora de unidades de solicitação][2]
2. <span data-ttu-id="22f77-218">Para estimar os requisitos de armazenamento de dados, insira o número total de itens que você espera armazenar.</span><span class="sxs-lookup"><span data-stu-id="22f77-218">To estimate data storage requirements, enter the total number of items you expect to store.</span></span>
3. <span data-ttu-id="22f77-219">Insira o número de operações de criação, leitura e atualização e exclusão de itens necessário (por segundo).</span><span class="sxs-lookup"><span data-stu-id="22f77-219">Enter the number of items create, read, update, and delete operations you require (on a per-second basis).</span></span> <span data-ttu-id="22f77-220">Para estimar as cobranças da unidade de solicitação das operações de atualização de itens, carregue uma cópia do item de exemplo da etapa 1 acima que inclui atualizações típicas de campo.</span><span class="sxs-lookup"><span data-stu-id="22f77-220">To estimate the request unit charges of item update operations, upload a copy of the sample item from step 1 above that includes typical field updates.</span></span>  <span data-ttu-id="22f77-221">Por exemplo, se as atualizações de itens normalmente modificarem duas propriedades chamadas lastLogin e userVisits, basta copiar o item de exemplo, atualizar os valores dessas duas propriedades e carregar o item copiado.</span><span class="sxs-lookup"><span data-stu-id="22f77-221">For example, if item updates typically modify two properties named lastLogin and userVisits, then simply copy the sample item, update the values for those two properties, and upload the copied item.</span></span>
   
    ![Inserir requisitos de produtividade na calculadora de unidade de solicitação][3]
4. <span data-ttu-id="22f77-223">Clique em Calcular e examinar os resultados.</span><span class="sxs-lookup"><span data-stu-id="22f77-223">Click calculate and examine the results.</span></span>
   
    ![Resultados da calculadora de unidade de solicitação][4]

> [!NOTE]
> <span data-ttu-id="22f77-225">Se você tiver tipos de itens que são muito diferentes em termos de tamanho e número de propriedades indexadas, carregue uma amostra da cada *tipo* do item típico na ferramenta e, depois, calcule os resultados.</span><span class="sxs-lookup"><span data-stu-id="22f77-225">If you have item types which will differ dramatically in terms of size and the number of indexed properties, then upload a sample of each *type* of typical item to the tool and then calculate the results.</span></span>
> 
> 

### <a name="use-the-azure-cosmos-db-request-charge-response-header"></a><span data-ttu-id="22f77-226">Usar o cabeçalho de resposta de encargos da solicitação do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="22f77-226">Use the Azure Cosmos DB request charge response header</span></span>
<span data-ttu-id="22f77-227">Todas as respostas do serviço Azure Cosmos DB incluem um cabeçalho personalizado (`x-ms-request-charge`) que contém as unidades de solicitação consumidas para a solicitação.</span><span class="sxs-lookup"><span data-stu-id="22f77-227">Every response from the Azure Cosmos DB service includes a custom header (`x-ms-request-charge`) that contains the request units consumed for the request.</span></span> <span data-ttu-id="22f77-228">Esse cabeçalho também está acessível por meio dos SDKs do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="22f77-228">This header is also accessible through the Azure Cosmos DB SDKs.</span></span> <span data-ttu-id="22f77-229">No SDK .NET, RequestCharge é uma propriedade do objeto ResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="22f77-229">In the .NET SDK, RequestCharge is a property of the ResourceResponse object.</span></span>  <span data-ttu-id="22f77-230">Para consultas, o Gerenciador de Consultas do Azure Cosmos DB no portal do Azure fornece informações de encargos de solicitação para as consultas executadas.</span><span class="sxs-lookup"><span data-stu-id="22f77-230">For queries, the Azure Cosmos DB Query Explorer in the Azure portal provides request charge information for executed queries.</span></span>

![Análise de encargos de RU no Gerenciador de Consultas][1]

<span data-ttu-id="22f77-232">Tendo isso em mente, um método para estimar a quantidade de produtividade reservada exigida pelo aplicativo é registrar o encargo de unidade de solicitação associado à execução de operações típicas em relação a um item representativo usado pelo aplicativo e, em seguida, estimar o número de operações que você prevê que executará a cada segundo.</span><span class="sxs-lookup"><span data-stu-id="22f77-232">With this in mind, one method for estimating the amount of reserved throughput required by your application is to record the request unit charge associated with running typical operations against a representative item used by your application and then estimating the number of operations you anticipate performing each second.</span></span>  <span data-ttu-id="22f77-233">Também meça e inclua consultas típicas e o uso de scripts do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="22f77-233">Be sure to measure and include typical queries and Azure Cosmos DB script usage as well.</span></span>

> [!NOTE]
> <span data-ttu-id="22f77-234">Se você tiver tipos de itens que são muito diferentes em termos de tamanho e número de propriedades indexadas, registre o encargo de unidades de solicitação da operação aplicável associado a cada *tipo* de item típico.</span><span class="sxs-lookup"><span data-stu-id="22f77-234">If you have item types which will differ dramatically in terms of size and the number of indexed properties, then record the applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

<span data-ttu-id="22f77-235">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="22f77-235">For example:</span></span>

1. <span data-ttu-id="22f77-236">Registre o encargo de unidades de solicitação para a criação (inserção) de um item típico.</span><span class="sxs-lookup"><span data-stu-id="22f77-236">Record the request unit charge of creating (inserting) a typical item.</span></span> 
2. <span data-ttu-id="22f77-237">Registre o encargo de unidades de solicitação para a leitura de um item típico.</span><span class="sxs-lookup"><span data-stu-id="22f77-237">Record the request unit charge of reading a typical item.</span></span>
3. <span data-ttu-id="22f77-238">Registre o encargo de unidades de solicitação para a atualização de um item típico.</span><span class="sxs-lookup"><span data-stu-id="22f77-238">Record the request unit charge of updating a typical item.</span></span>
4. <span data-ttu-id="22f77-239">Registre o encargo de unidades de solicitação para consultas de itens comuns e típicos.</span><span class="sxs-lookup"><span data-stu-id="22f77-239">Record the request unit charge of typical, common item queries.</span></span>
5. <span data-ttu-id="22f77-240">Registre o encargo de unidade de solicitação de quaisquer scripts personalizados (procedimentos armazenados, gatilhos, funções definidas pelo usuário) utilizados pelo aplicativo</span><span class="sxs-lookup"><span data-stu-id="22f77-240">Record the request unit charge of any custom scripts (stored procedures, triggers, user-defined functions) leveraged by the application</span></span>
6. <span data-ttu-id="22f77-241">Calcule as unidades de solicitação necessárias, dado o número estimado de operações que você prevê que executará por segundo.</span><span class="sxs-lookup"><span data-stu-id="22f77-241">Calculate the required request units given the estimated number of operations you anticipate to run each second.</span></span>

### <span data-ttu-id="22f77-242"><a id="GetLastRequestStatistics"></a>Usar o comando GetLastRequestStatistics da API para MongoDB</span><span class="sxs-lookup"><span data-stu-id="22f77-242"><a id="GetLastRequestStatistics"></a>Use API for MongoDB's GetLastRequestStatistics command</span></span>
<span data-ttu-id="22f77-243">A API para MongoDB dá suporte a um comando personalizado, *getLastRequestStatistics*, para recuperar a carga de solicitação de operações especificadas.</span><span class="sxs-lookup"><span data-stu-id="22f77-243">API for MongoDB supports a custom command, *getLastRequestStatistics*, for retrieving the request charge for specified operations.</span></span>

<span data-ttu-id="22f77-244">Por exemplo, no Shell do Mongo, execute a operação para a qual você deseja verificar a carga de solicitação.</span><span class="sxs-lookup"><span data-stu-id="22f77-244">For example, in the Mongo Shell, execute the operation you want to verify the request charge for.</span></span>
```
> db.sample.find()
```

<span data-ttu-id="22f77-245">Em seguida, execute o comando *getLastRequestStatistics*.</span><span class="sxs-lookup"><span data-stu-id="22f77-245">Next, execute the command *getLastRequestStatistics*.</span></span>
```
> db.runCommand({getLastRequestStatistics: 1})
{
    "_t": "GetRequestStatisticsResponse",
    "ok": 1,
    "CommandName": "OP_QUERY",
    "RequestCharge": 2.48,
    "RequestDurationInMilliSeconds" : 4.0048
}
```

<span data-ttu-id="22f77-246">Tendo isso em mente, um método para estimar a quantidade de produtividade reservada exigida pelo aplicativo é registrar o encargo de unidade de solicitação associado à execução de operações típicas em relação a um item representativo usado pelo aplicativo e, em seguida, estimar o número de operações que você prevê que executará a cada segundo.</span><span class="sxs-lookup"><span data-stu-id="22f77-246">With this in mind, one method for estimating the amount of reserved throughput required by your application is to record the request unit charge associated with running typical operations against a representative item used by your application and then estimating the number of operations you anticipate performing each second.</span></span>

> [!NOTE]
> <span data-ttu-id="22f77-247">Se você tiver tipos de itens que são muito diferentes em termos de tamanho e número de propriedades indexadas, registre o encargo de unidades de solicitação da operação aplicável associado a cada *tipo* de item típico.</span><span class="sxs-lookup"><span data-stu-id="22f77-247">If you have item types which will differ dramatically in terms of size and the number of indexed properties, then record the applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

## <a name="use-api-for-mongodbs-portal-metrics"></a><span data-ttu-id="22f77-248">Usar as métricas de portal da API para MongoDB</span><span class="sxs-lookup"><span data-stu-id="22f77-248">Use API for MongoDB's portal metrics</span></span>
<span data-ttu-id="22f77-249">A maneira mais simples de obter uma boa estimativa dos encargos da unidade de solicitação para seu banco de dados da API para MongoDB é usar as métricas do [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="22f77-249">The simplest way to get a good estimation of request unit charges for your API for MongoDB database is to use the [Azure portal](https://portal.azure.com) metrics.</span></span> <span data-ttu-id="22f77-250">Com os gráficos *Número de solicitações* e *Custo da Solicitação*, você pode obter uma estimativa de quantas unidades de solicitação cada operação está consumindo, e quantas unidades de solicitação elas consomem com relação às outras operações.</span><span class="sxs-lookup"><span data-stu-id="22f77-250">With the *Number of requests* and *Request Charge* charts, you can get an estimation of how many request units each operation is consuming and how many request units they consume relative to one another.</span></span>

![Métricas do portal da API para MongoDB][6]

## <a name="a-request-unit-estimation-example"></a><span data-ttu-id="22f77-252">Um exemplo de estimativa de unidade de solicitação</span><span class="sxs-lookup"><span data-stu-id="22f77-252">A request unit estimation example</span></span>
<span data-ttu-id="22f77-253">Considere o seguinte documento de aproximadamente 1 KB:</span><span class="sxs-lookup"><span data-stu-id="22f77-253">Consider the following ~1KB document:</span></span>

```json
{
 "id": "08259",
  "description": "Cereals ready-to-eat, KELLOGG, KELLOGG'S CRISPIX",
  "tags": [
    {
      "name": "cereals ready-to-eat"
    },
    {
      "name": "kellogg"
    },
    {
      "name": "kellogg's crispix"
    }
  ],
  "version": 1,
  "commonName": "Includes USDA Commodity B855",
  "manufacturerName": "Kellogg, Co.",
  "isFromSurvey": false,
  "foodGroup": "Breakfast Cereals",
  "nutrients": [
    {
      "id": "262",
      "description": "Caffeine",
      "nutritionValue": 0,
      "units": "mg"
    },
    {
      "id": "307",
      "description": "Sodium, Na",
      "nutritionValue": 611,
      "units": "mg"
    },
    {
      "id": "309",
      "description": "Zinc, Zn",
      "nutritionValue": 5.2,
      "units": "mg"
    }
  ],
  "servings": [
    {
      "amount": 1,
      "description": "cup (1 NLEA serving)",
      "weightInGrams": 29
    }
  ]
}
```

> [!NOTE]
> <span data-ttu-id="22f77-254">Os documentos são reduzidos no Azure Cosmos DB e, portanto, o tamanho do documento acima calculado pelo sistema é um pouco menor que 1 KB.</span><span class="sxs-lookup"><span data-stu-id="22f77-254">Documents are minified in Azure Cosmos DB, so the system calculated size of the document above is slightly less than 1KB.</span></span>
> 
> 

<span data-ttu-id="22f77-255">A seguinte tabela mostra os encargos de unidades de solicitação aproximados para operações típicas nesse item (o encargo de unidades de solicitação aproximado pressupõe que o nível de consistência de conta seja definido como “Sessão” e que todos os itens sejam indexados automaticamente):</span><span class="sxs-lookup"><span data-stu-id="22f77-255">The following table shows approximate request unit charges for typical operations on this item (the approximate request unit charge assumes that the account consistency level is set to “Session” and that all items are automatically indexed):</span></span>

| <span data-ttu-id="22f77-256">Operação</span><span class="sxs-lookup"><span data-stu-id="22f77-256">Operation</span></span> | <span data-ttu-id="22f77-257">Encargo de Unidade de Solicitação</span><span class="sxs-lookup"><span data-stu-id="22f77-257">Request Unit Charge</span></span> |
| --- | --- |
| <span data-ttu-id="22f77-258">Criar item</span><span class="sxs-lookup"><span data-stu-id="22f77-258">Create item</span></span> |<span data-ttu-id="22f77-259">Cerca de 15 RUs</span><span class="sxs-lookup"><span data-stu-id="22f77-259">~15 RU</span></span> |
| <span data-ttu-id="22f77-260">Ler item</span><span class="sxs-lookup"><span data-stu-id="22f77-260">Read item</span></span> |<span data-ttu-id="22f77-261">Cerca de 1 RU</span><span class="sxs-lookup"><span data-stu-id="22f77-261">~1 RU</span></span> |
| <span data-ttu-id="22f77-262">Consultar item por ID</span><span class="sxs-lookup"><span data-stu-id="22f77-262">Query item by id</span></span> |<span data-ttu-id="22f77-263">Cerca de 2,5 RUs</span><span class="sxs-lookup"><span data-stu-id="22f77-263">~2.5 RU</span></span> |

<span data-ttu-id="22f77-264">Adicionalmente, a tabela mostra os encargos de unidade de solicitação aproximados para consultas típicas usadas no aplicativo:</span><span class="sxs-lookup"><span data-stu-id="22f77-264">Additionally, this table shows approximate request unit charges for typical queries used in the application:</span></span>

| <span data-ttu-id="22f77-265">Consultar</span><span class="sxs-lookup"><span data-stu-id="22f77-265">Query</span></span> | <span data-ttu-id="22f77-266">Encargo de Unidade de Solicitação</span><span class="sxs-lookup"><span data-stu-id="22f77-266">Request Unit Charge</span></span> | <span data-ttu-id="22f77-267">Nº de itens retornados</span><span class="sxs-lookup"><span data-stu-id="22f77-267"># of Returned Items</span></span> |
| --- | --- | --- |
| <span data-ttu-id="22f77-268">Selecionar alimentos por id</span><span class="sxs-lookup"><span data-stu-id="22f77-268">Select food by id</span></span> |<span data-ttu-id="22f77-269">Cerca de 2,5 RUs</span><span class="sxs-lookup"><span data-stu-id="22f77-269">~2.5 RU</span></span> |<span data-ttu-id="22f77-270">1</span><span class="sxs-lookup"><span data-stu-id="22f77-270">1</span></span> |
| <span data-ttu-id="22f77-271">Selecionar alimentos por fabricante</span><span class="sxs-lookup"><span data-stu-id="22f77-271">Select foods by manufacturer</span></span> |<span data-ttu-id="22f77-272">Cerca de 7 RUs</span><span class="sxs-lookup"><span data-stu-id="22f77-272">~7 RU</span></span> |<span data-ttu-id="22f77-273">7</span><span class="sxs-lookup"><span data-stu-id="22f77-273">7</span></span> |
| <span data-ttu-id="22f77-274">Selecionar por grupo de alimentos e solicitar por peso</span><span class="sxs-lookup"><span data-stu-id="22f77-274">Select by food group and order by weight</span></span> |<span data-ttu-id="22f77-275">Cerca de 70 RUs</span><span class="sxs-lookup"><span data-stu-id="22f77-275">~70 RU</span></span> |<span data-ttu-id="22f77-276">100</span><span class="sxs-lookup"><span data-stu-id="22f77-276">100</span></span> |
| <span data-ttu-id="22f77-277">Selecionar os 10 alimentos principais em um grupo de alimentos</span><span class="sxs-lookup"><span data-stu-id="22f77-277">Select top 10 foods in a food group</span></span> |<span data-ttu-id="22f77-278">Cerca de 10 RUs</span><span class="sxs-lookup"><span data-stu-id="22f77-278">~10 RU</span></span> |<span data-ttu-id="22f77-279">10</span><span class="sxs-lookup"><span data-stu-id="22f77-279">10</span></span> |

> [!NOTE]
> <span data-ttu-id="22f77-280">Os encargos de RU variam com base no número de itens retornados.</span><span class="sxs-lookup"><span data-stu-id="22f77-280">RU charges vary based on the number of items returned.</span></span>
> 
> 

<span data-ttu-id="22f77-281">Com essas informações, podemos estimar os requisitos de RU para o aplicativo, dado o número de operações e consultas que esperamos por segundo:</span><span class="sxs-lookup"><span data-stu-id="22f77-281">With this information, we can estimate the RU requirements for this application given the number of operations and queries we expect per second:</span></span>

| <span data-ttu-id="22f77-282">Operação/consulta</span><span class="sxs-lookup"><span data-stu-id="22f77-282">Operation/Query</span></span> | <span data-ttu-id="22f77-283">Número estimado por segundo</span><span class="sxs-lookup"><span data-stu-id="22f77-283">Estimated number per second</span></span> | <span data-ttu-id="22f77-284">RUs necessárias</span><span class="sxs-lookup"><span data-stu-id="22f77-284">Required RUs</span></span> |
| --- | --- | --- |
| <span data-ttu-id="22f77-285">Criar item</span><span class="sxs-lookup"><span data-stu-id="22f77-285">Create item</span></span> |<span data-ttu-id="22f77-286">10</span><span class="sxs-lookup"><span data-stu-id="22f77-286">10</span></span> |<span data-ttu-id="22f77-287">150</span><span class="sxs-lookup"><span data-stu-id="22f77-287">150</span></span> |
| <span data-ttu-id="22f77-288">Ler item</span><span class="sxs-lookup"><span data-stu-id="22f77-288">Read item</span></span> |<span data-ttu-id="22f77-289">100</span><span class="sxs-lookup"><span data-stu-id="22f77-289">100</span></span> |<span data-ttu-id="22f77-290">100</span><span class="sxs-lookup"><span data-stu-id="22f77-290">100</span></span> |
| <span data-ttu-id="22f77-291">Selecionar alimentos por fabricante</span><span class="sxs-lookup"><span data-stu-id="22f77-291">Select foods by manufacturer</span></span> |<span data-ttu-id="22f77-292">25</span><span class="sxs-lookup"><span data-stu-id="22f77-292">25</span></span> |<span data-ttu-id="22f77-293">175</span><span class="sxs-lookup"><span data-stu-id="22f77-293">175</span></span> |
| <span data-ttu-id="22f77-294">Selecionar por grupo de alimentos</span><span class="sxs-lookup"><span data-stu-id="22f77-294">Select by food group</span></span> |<span data-ttu-id="22f77-295">10</span><span class="sxs-lookup"><span data-stu-id="22f77-295">10</span></span> |<span data-ttu-id="22f77-296">700</span><span class="sxs-lookup"><span data-stu-id="22f77-296">700</span></span> |
| <span data-ttu-id="22f77-297">Selecionar os 10 principais</span><span class="sxs-lookup"><span data-stu-id="22f77-297">Select top 10</span></span> |<span data-ttu-id="22f77-298">15</span><span class="sxs-lookup"><span data-stu-id="22f77-298">15</span></span> |<span data-ttu-id="22f77-299">Total de 150</span><span class="sxs-lookup"><span data-stu-id="22f77-299">150 Total</span></span> |

<span data-ttu-id="22f77-300">Nesse caso, esperamos um requisito de taxa de transferência médio de 1.275 RUs/s.</span><span class="sxs-lookup"><span data-stu-id="22f77-300">In this case, we expect an average throughput requirement of 1,275 RU/s.</span></span>  <span data-ttu-id="22f77-301">Arredondando para a centena mais próxima, vamos provisionar 1.300 RUs/s para a coleção desse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="22f77-301">Rounding up to the nearest 100, we would provision 1,300 RU/s for this application's collection.</span></span>

## <span data-ttu-id="22f77-302"><a id="RequestRateTooLarge"></a> Excedendo os limites de produtividade reservada no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="22f77-302"><a id="RequestRateTooLarge"></a> Exceeding reserved throughput limits in Azure Cosmos DB</span></span>
<span data-ttu-id="22f77-303">Lembre-se de que o consumo de unidades de solicitação será avaliado como uma taxa por segundo se o orçamento estiver vazio.</span><span class="sxs-lookup"><span data-stu-id="22f77-303">Recall that request unit consumption is evaluated as a rate per second if the budget is empty.</span></span> <span data-ttu-id="22f77-304">Para aplicativos que excedem a taxa de unidades de solicitação provisionada de um contêiner, as solicitações a essa coleção serão limitadas até que a taxa fique abaixo do nível reservado.</span><span class="sxs-lookup"><span data-stu-id="22f77-304">For applications that exceed the provisioned request unit rate for a container, requests to that collection will be throttled until the rate drops below the reserved level.</span></span> <span data-ttu-id="22f77-305">Quando ocorre uma restrição, o servidor encerra preventivamente a solicitação com RequestRateTooLargeException (código de status HTTP 429) e retorna o cabeçalho x-ms-retry-after-ms, indicando a quantidade de tempo, em milissegundos, que o usuário deve aguardar antes de tentar novamente a solicitação.</span><span class="sxs-lookup"><span data-stu-id="22f77-305">When a throttle occurs, the server will preemptively end the request with RequestRateTooLargeException (HTTP status code 429) and return the x-ms-retry-after-ms header indicating the amount of time, in milliseconds, that the user must wait before reattempting the request.</span></span>

    HTTP Status 429
    Status Line: RequestRateTooLarge
    x-ms-retry-after-ms :100

<span data-ttu-id="22f77-306">Se estiver usando as consultas do SDK do cliente .NET e LINQ, em seguida, na maioria das vezes, você nunca precisará lidar com essa exceção, pois a versão atual do SDK do Cliente .NET captura implicitamente essa resposta, respeita o cabeçalho retry-after especificado pelo servidor e tenta novamente a solicitação.</span><span class="sxs-lookup"><span data-stu-id="22f77-306">If you are using the .NET Client SDK and LINQ queries, then most of the time you never have to deal with this exception, as the current version of the .NET Client SDK implicitly catches this response, respects the server-specified retry-after header, and retries the request.</span></span> <span data-ttu-id="22f77-307">A menos que sua conta esteja sendo acessada simultaneamente por vários clientes, a próxima tentativa será bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="22f77-307">Unless your account is being accessed concurrently by multiple clients, the next retry will succeed.</span></span>

<span data-ttu-id="22f77-308">Se você tiver mais de um cliente operando cumulativamente acima da taxa de solicitação, o comportamento de repetição padrão poderá não ser suficiente e o cliente lançará uma DocumentClientException com o código de status 429 para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="22f77-308">If you have more than one client cumulatively operating above the request rate, the default retry behavior may not suffice, and the client will throw a DocumentClientException with status code 429 to the application.</span></span> <span data-ttu-id="22f77-309">Em casos como esse, considere a manipulação do comportamento de repetição e da lógica nas rotinas de tratamento de erro do aplicativo ou o aumento da produtividade reservada para o contêiner.</span><span class="sxs-lookup"><span data-stu-id="22f77-309">In cases such as this, you may consider handling retry behavior and logic in your application's error handling routines or increasing the reserved throughput for the container.</span></span>

## <span data-ttu-id="22f77-310"><a id="RequestRateTooLargeAPIforMongoDB"></a> Exceder os limites de taxa de transferência reservada na API para MongoDB</span><span class="sxs-lookup"><span data-stu-id="22f77-310"><a id="RequestRateTooLargeAPIforMongoDB"></a> Exceeding reserved throughput limits in API for MongoDB</span></span>
<span data-ttu-id="22f77-311">Os aplicativos que ultrapassarem as unidades de solicitação provisionadas para uma coleção serão limitados até que a taxa caia para baixo do nível reservado.</span><span class="sxs-lookup"><span data-stu-id="22f77-311">Applications that exceed the provisioned request units for a collection will be throttled until the rate drops below the reserved level.</span></span> <span data-ttu-id="22f77-312">Quando ocorrer uma limitação, o back-end terminará preventivamente a solicitação com um código de erro *16500* - *Muitas Solicitações*.</span><span class="sxs-lookup"><span data-stu-id="22f77-312">When a throttle occurs, the backend will preemptively end the request with a *16500* error code - *Too Many Requests*.</span></span> <span data-ttu-id="22f77-313">Por padrão, a API para MongoDB repetirá automaticamente até 10 vezes antes de retornar um código de erro *Muitas Solicitações*.</span><span class="sxs-lookup"><span data-stu-id="22f77-313">By default, API for MongoDB will automatically retry up to 10 times before returning a *Too Many Requests* error code.</span></span> <span data-ttu-id="22f77-314">Se você estiver recebendo códigos de erro *Muitas Solicitações*, considere a repetição nas rotinas de manipulação de erro de seu aplicativo ou [aumentar a taxa de transferência reservada para a coleção](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="22f77-314">If you are receiving many *Too Many Requests* error codes, you may consider either adding retry behavior in your application's error handling routines or [increasing the reserved throughput for the collection](set-throughput.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="22f77-315">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="22f77-315">Next steps</span></span>
<span data-ttu-id="22f77-316">Para saber mais sobre a produtividade reservada com bancos de dados do Azure Cosmos DB, conheça estes recursos:</span><span class="sxs-lookup"><span data-stu-id="22f77-316">To learn more about reserved throughput with Azure Cosmos DB databases, explore these resources:</span></span>

* [<span data-ttu-id="22f77-317">Preços do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="22f77-317">Azure Cosmos DB pricing</span></span>](https://azure.microsoft.com/pricing/details/cosmos-db/)
* [<span data-ttu-id="22f77-318">Particionando dados no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="22f77-318">Partitioning data in Azure Cosmos DB</span></span>](partition-data.md)

<span data-ttu-id="22f77-319">Para saber mais sobre o Azure Cosmos DB, consulte a [documentação](https://azure.microsoft.com/documentation/services/cosmos-db/) do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="22f77-319">To learn more about Azure Cosmos DB, see the Azure Cosmos DB [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/).</span></span> 

<span data-ttu-id="22f77-320">Para obter uma introdução aos testes de escala e desempenho com o Azure Cosmos DB, consulte [Testes de desempenho e escala com o Azure Cosmos DB](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="22f77-320">To get started with scale and performance testing with Azure Cosmos DB, see [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md).</span></span>

[1]: ./media/request-units/queryexplorer.png 
[2]: ./media/request-units/RUEstimatorUpload.png
[3]: ./media/request-units/RUEstimatorDocuments.png
[4]: ./media/request-units/RUEstimatorResults.png
[5]: ./media/request-units/RUCalculator2.png
[6]: ./media/request-units/api-for-mongodb-metrics.png
