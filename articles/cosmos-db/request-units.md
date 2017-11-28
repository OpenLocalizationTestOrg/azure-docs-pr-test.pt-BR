---
title: "aaaRequest unidades e taxa de transferência estimando - banco de dados do Azure Cosmos | Microsoft Docs"
description: "Saiba mais sobre como toounderstand, especifique e estimar os requisitos de unidade de solicitação no banco de dados do Azure Cosmos."
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
ms.openlocfilehash: 13c4e7aeb6222fa14ef982e238716e15a0159fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-in-azure-cosmos-db"></a><span data-ttu-id="f29bc-103">Unidades de Solicitação no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f29bc-103">Request Units in Azure Cosmos DB</span></span>
<span data-ttu-id="f29bc-104">Agora disponível: [calculadora de unidades de solicitação](https://www.documentdb.com/capacityplanner) do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f29bc-104">Now available: Azure Cosmos DB [request unit calculator](https://www.documentdb.com/capacityplanner).</span></span> <span data-ttu-id="f29bc-105">Saiba mais em [Estimativa das necessidades de produção](request-units.md#estimating-throughput-needs).</span><span class="sxs-lookup"><span data-stu-id="f29bc-105">Learn more in [Estimating your throughput needs](request-units.md#estimating-throughput-needs).</span></span>

![Calculadora de produtividade][5]

## <a name="introduction"></a><span data-ttu-id="f29bc-107">Introdução</span><span class="sxs-lookup"><span data-stu-id="f29bc-107">Introduction</span></span>
<span data-ttu-id="f29bc-108">O [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) é o multimodelo de banco de dados distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f29bc-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is Microsoft's globally distributed multi-model database.</span></span> <span data-ttu-id="f29bc-109">Com o banco de dados do Azure Cosmos, você não tem máquinas virtuais de toorent, implantar o software ou monitorar bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="f29bc-109">With Azure Cosmos DB, you don't have toorent virtual machines, deploy software, or monitor databases.</span></span> <span data-ttu-id="f29bc-110">Banco de dados do Azure Cosmos é operado e continuamente monitorado pelo Microsoft engenheiros superior toodeliver world classe disponibilidade, desempenho e proteção de dados.</span><span class="sxs-lookup"><span data-stu-id="f29bc-110">Azure Cosmos DB is operated and continuously monitored by Microsoft top engineers toodeliver world class availability, performance, and data protection.</span></span> <span data-ttu-id="f29bc-111">Você pode acessar seus dados usando as APIs de sua preferência, como [SQL do DocumentDB](documentdb-sql-query.md) (documento), MongoDB (documento), [Armazenamento de Tabelas do Azure](https://azure.microsoft.com/services/storage/tables/) (chave-valor) e [Gremlin](https://tinkerpop.apache.org/gremlin.html) (gráfico), todas com suporte nativo.</span><span class="sxs-lookup"><span data-stu-id="f29bc-111">You can access your data using APIs of your choice, as [DocumentDB SQL](documentdb-sql-query.md) (document), MongoDB (document), [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/) (key-value), and [Gremlin](https://tinkerpop.apache.org/gremlin.html) (graph) are all natively supported.</span></span> <span data-ttu-id="f29bc-112">moeda de saudação do banco de dados do Azure Cosmos é hello unidade de solicitação (RU).</span><span class="sxs-lookup"><span data-stu-id="f29bc-112">hello currency of Azure Cosmos DB is hello Request Unit (RU).</span></span> <span data-ttu-id="f29bc-113">Com RUs, não é necessário tooreserve capacidades de leitura/gravação ou provisionar CPU, memória e IOPS.</span><span class="sxs-lookup"><span data-stu-id="f29bc-113">With RUs, you do not need tooreserve read/write capacities or provision CPU, Memory and IOPS.</span></span>

<span data-ttu-id="f29bc-114">Banco de dados do Azure Cosmos dá suporte a várias APIs com operações diferentes, variando de leituras simples e grava toocomplex consultas de gráfico.</span><span class="sxs-lookup"><span data-stu-id="f29bc-114">Azure Cosmos DB supports a number of APIs with different operations ranging from simple reads and writes toocomplex graph queries.</span></span> <span data-ttu-id="f29bc-115">Como nem todas as solicitações são iguais, eles recebem uma quantidade normalizada de **unidades de solicitação** com base na quantidade de saudação da solicitação de saudação do computação tooserve necessária.</span><span class="sxs-lookup"><span data-stu-id="f29bc-115">Since not all requests are equal, they are assigned a normalized quantity of **request units** based on hello amount of computation required tooserve hello request.</span></span> <span data-ttu-id="f29bc-116">número de saudação de unidades de solicitação para uma operação é determinístico, e você pode acompanhar o número de saudação de unidades de solicitação consumidos por qualquer operação no banco de dados do Azure Cosmos por meio de um cabeçalho de resposta.</span><span class="sxs-lookup"><span data-stu-id="f29bc-116">hello number of request units for an operation is deterministic, and you can track hello number of request units consumed by any operation in Azure Cosmos DB via a response header.</span></span> 

<span data-ttu-id="f29bc-117">tooprovide um desempenho previsível, você precisa de taxa de transferência tooreserve em unidades de 100 RU/segundo.</span><span class="sxs-lookup"><span data-stu-id="f29bc-117">tooprovide predictable performance, you need tooreserve throughput in units of 100 RU/second.</span></span> 

<span data-ttu-id="f29bc-118">Depois de ler este artigo, você será capaz de tooanswer Olá perguntas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f29bc-118">After reading this article, you'll be able tooanswer hello following questions:</span></span>  

* <span data-ttu-id="f29bc-119">O que são unidades de solicitação e solicitações de encargos?</span><span class="sxs-lookup"><span data-stu-id="f29bc-119">What are request units and request charges?</span></span>
* <span data-ttu-id="f29bc-120">Como especificar a capacidade da unidade de solicitação para uma coleção?</span><span class="sxs-lookup"><span data-stu-id="f29bc-120">How do I specify request unit capacity for a collection?</span></span>
* <span data-ttu-id="f29bc-121">Como estimar as necessidades de unidades de solicitação de meu aplicativo?</span><span class="sxs-lookup"><span data-stu-id="f29bc-121">How do I estimate my application's request unit needs?</span></span>
* <span data-ttu-id="f29bc-122">O que acontecerá se eu exceder a capacidade da unidade de solicitação de uma coleção?</span><span class="sxs-lookup"><span data-stu-id="f29bc-122">What happens if I exceed request unit capacity for a collection?</span></span>

<span data-ttu-id="f29bc-123">Como o banco de dados do Azure Cosmos é um banco de dados de vários modelo, é importante toonote que chamaremos tooa coleta/documento para um documento de API, um nó do gráfico/com a API do graph e uma tabela/entidade para a API de tabela.</span><span class="sxs-lookup"><span data-stu-id="f29bc-123">As Azure Cosmos DB is a multi-model database, it is important toonote that we will refer tooa collection/document for a document API, a graph/node for a graph API and a table/entity for table API.</span></span> <span data-ttu-id="f29bc-124">Taxa de transferência neste documento generalizaremos toohello conceitos de contêiner/item.</span><span class="sxs-lookup"><span data-stu-id="f29bc-124">Throughput this document we will generalize toohello concepts of container/item.</span></span>

## <a name="request-units-and-request-charges"></a><span data-ttu-id="f29bc-125">Unidades de solicitação e solicitações de encargos</span><span class="sxs-lookup"><span data-stu-id="f29bc-125">Request units and request charges</span></span>
<span data-ttu-id="f29bc-126">Banco de dados do Azure Cosmos oferece desempenho rápido e previsível por *reservar* toosatisfy recursos taxa de transferência do seu aplicativo precisa.</span><span class="sxs-lookup"><span data-stu-id="f29bc-126">Azure Cosmos DB delivers fast, predictable performance by *reserving* resources toosatisfy your application's throughput needs.</span></span>  <span data-ttu-id="f29bc-127">Porque o aplicativo de carga e acessar a mudança nos padrões ao longo do tempo, o banco de dados do Azure Cosmos permite tooeasily aumentar ou diminuir a quantidade de saudação do aplicativo de tooyour disponíveis de produtividade reservados.</span><span class="sxs-lookup"><span data-stu-id="f29bc-127">Because application load and access patterns change over time, Azure Cosmos DB allows you tooeasily increase or decrease hello amount of reserved throughput available tooyour application.</span></span>

<span data-ttu-id="f29bc-128">Com o Azure Cosmos DB, a produtividade reservada é especificada em termos de processamento de unidades de solicitação por segundo.</span><span class="sxs-lookup"><span data-stu-id="f29bc-128">With Azure Cosmos DB, reserved throughput is specified in terms of request units processing per second.</span></span> <span data-ttu-id="f29bc-129">Você pode pensar unidades de solicitação como moeda da taxa de transferência, no qual você *reservar* garantia de uma quantidade de unidades de solicitação disponíveis tooyour aplicativo por segundo.</span><span class="sxs-lookup"><span data-stu-id="f29bc-129">You can think of request units as throughput currency, whereby you *reserve* an amount of guaranteed request units available tooyour application on per second basis.</span></span>  <span data-ttu-id="f29bc-130">Cada operação do Azure Cosmos DB – gravar um documento, realizar uma consulta, atualizar um documento – consome CPU, memória e IOPS.</span><span class="sxs-lookup"><span data-stu-id="f29bc-130">Each operation in Azure Cosmos DB - writing a document, performing a query, updating a document - consumes CPU, memory, and IOPS.</span></span>  <span data-ttu-id="f29bc-131">Ou seja, cada operação resulta em um *encargo de solicitação*, que é expressa em *unidades de solicitação*.</span><span class="sxs-lookup"><span data-stu-id="f29bc-131">That is, each operation incurs a *request charge*, which is expressed in *request units*.</span></span>  <span data-ttu-id="f29bc-132">Noções básicas sobre fatores de saudação que afetam as cobranças de unidade de solicitação, juntamente com requisitos de taxa de transferência do seu aplicativo, permite que você toorun seu aplicativo como custo com eficiência possível.</span><span class="sxs-lookup"><span data-stu-id="f29bc-132">Understanding hello factors which impact request unit charges, along with your application's throughput requirements, enables you toorun your application as cost effectively as possible.</span></span> <span data-ttu-id="f29bc-133">Pesquisador de objetos de consulta Olá também é um núcleo de saudação tootest ferramenta excelente de uma consulta.</span><span class="sxs-lookup"><span data-stu-id="f29bc-133">hello query explorer is also a wonderful tool tootest hello core of a query.</span></span>

<span data-ttu-id="f29bc-134">É recomendável que guia de Introdução observando Olá seguindo o vídeo, onde Aravind Ramachandran explica unidades de solicitação e um desempenho previsível com o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f29bc-134">We recommend getting started by watching hello following video, where Aravind Ramachandran explains request units and predictable performance with Azure Cosmos DB.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Predictable-Performance-with-DocumentDB/player]
> 
> 

## <a name="specifying-request-unit-capacity-in-azure-cosmos-db"></a><span data-ttu-id="f29bc-135">Especificando a capacidade de unidades de solicitação no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f29bc-135">Specifying request unit capacity in Azure Cosmos DB</span></span>
<span data-ttu-id="f29bc-136">Ao iniciar uma nova coleção, tabela ou gráfico, você especificar o número de saudação de unidades de solicitação por segundo (RU por segundo) que você deseja reservado.</span><span class="sxs-lookup"><span data-stu-id="f29bc-136">When starting a new collection, table or graph, you specify hello number of request units per second (RU per second) you want reserved.</span></span> <span data-ttu-id="f29bc-137">Com base na taxa de transferência fornecida hello, o banco de dados do Azure Cosmos aloca partições físicas toohost sua coleção e divisões/rebalances dados em partições à medida que cresce.</span><span class="sxs-lookup"><span data-stu-id="f29bc-137">Based on hello provisioned throughput, Azure Cosmos DB allocates physical partitions toohost your collection and splits/rebalances data across partitions as it grows.</span></span>

<span data-ttu-id="f29bc-138">Banco de dados do Azure Cosmos requer que um toobe de chave de partição especificado quando uma coleção é provisionado com 2.500 unidades de solicitação ou superior.</span><span class="sxs-lookup"><span data-stu-id="f29bc-138">Azure Cosmos DB requires a partition key toobe specified when a collection is provisioned with 2,500 request units or higher.</span></span> <span data-ttu-id="f29bc-139">Uma chave de partição é tooscale necessário também taxa de transferência da coleção além 2.500 unidades de solicitação no hello futuras.</span><span class="sxs-lookup"><span data-stu-id="f29bc-139">A partition key is also required tooscale your collection's throughput beyond 2,500 request units in hello future.</span></span> <span data-ttu-id="f29bc-140">Portanto, é altamente recomendável tooconfigure um [chave de partição](partition-data.md) ao criar um contêiner, independentemente da taxa de transferência inicial.</span><span class="sxs-lookup"><span data-stu-id="f29bc-140">Therefore, it is highly recommended tooconfigure a [partition key](partition-data.md) when creating a container regardless of your initial throughput.</span></span> <span data-ttu-id="f29bc-141">Como os dados podem ter toobe divididos em várias partições, é necessário toopick uma chave de partição que tenha uma alta cardinalidade (100 toomillions de valores distintos), para que seu gráfico/de tabela de coleta e solicitações podem ser dimensionadas uniformemente por banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f29bc-141">Since your data might have toobe split across multiple partitions, it is necessary toopick a partition key that has a high cardinality (100 toomillions of distinct values) so that your collection/table/graph and requests can be scaled uniformly by Azure Cosmos DB.</span></span> 

> [!NOTE]
> <span data-ttu-id="f29bc-142">Uma chave de partição é um limite lógico e não físico.</span><span class="sxs-lookup"><span data-stu-id="f29bc-142">A partition key is a logical boundary, and not a physical one.</span></span> <span data-ttu-id="f29bc-143">Portanto, não é necessário toolimit número de saudação dos valores de chave de partição distintos.</span><span class="sxs-lookup"><span data-stu-id="f29bc-143">Therefore, you do not need toolimit hello number of distinct partition key values.</span></span> <span data-ttu-id="f29bc-144">Na verdade é melhor toohave distinto particionar os valores de chave que menor, como o banco de dados do Azure Cosmos tem mais opções de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="f29bc-144">It is in fact better toohave more distinct partition key values than less, as Azure Cosmos DB has more load balancing options.</span></span>

<span data-ttu-id="f29bc-145">Aqui está um trecho de código para criar uma coleção com 3.000 unidades por segundo usando Olá SDK .NET de solicitação:</span><span class="sxs-lookup"><span data-stu-id="f29bc-145">Here is a code snippet for creating a collection with 3,000 request units per second using hello .NET SDK:</span></span>

```csharp
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000 });
```

<span data-ttu-id="f29bc-146">O Azure Cosmos DB opera em um modelo de reserva na produtividade.</span><span class="sxs-lookup"><span data-stu-id="f29bc-146">Azure Cosmos DB operates on a reservation model on throughput.</span></span> <span data-ttu-id="f29bc-147">Ou seja, você será cobrado pela quantidade de saudação de taxa de transferência *reservado*, independentemente de quantos essa taxa de transferência é ativamente *usado*.</span><span class="sxs-lookup"><span data-stu-id="f29bc-147">That is, you are billed for hello amount of throughput *reserved*, regardless of how much of that throughput is actively *used*.</span></span> <span data-ttu-id="f29bc-148">Como uso, dados e carga padrões alteração seu aplicativo você pode facilmente aumentar e diminuir Olá quantidade de RUs reservados por meio de SDKs ou usando Olá [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f29bc-148">As your application's load, data, and usage patterns change you can easily scale up and down hello amount of reserved RUs through SDKs or using hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="f29bc-149">Cada coleção/tabela/gráfico são mapeados tooan `Offer` recursos no Azure Cosmos DB, que tem metadados sobre a taxa de transferência fornecida hello.</span><span class="sxs-lookup"><span data-stu-id="f29bc-149">Each collection/table/graph are mapped tooan `Offer` resource in Azure Cosmos DB, which has metadata about hello provisioned throughput.</span></span> <span data-ttu-id="f29bc-150">Você pode alterar o throughput Olá alocada pesquisando o recurso de oferta correspondente Olá para um contêiner, em seguida, atualizá-lo com o novo valor de taxa de transferência hello.</span><span class="sxs-lookup"><span data-stu-id="f29bc-150">You can change hello allocated throughput by looking up hello corresponding offer resource for a container, then updating it with hello new throughput value.</span></span> <span data-ttu-id="f29bc-151">Aqui está um trecho de código para alterar a taxa de transferência de saudação de uma coleção too5, 000 unidades de solicitação por segundo usando Olá .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="f29bc-151">Here is a code snippet for changing hello throughput of a collection too5,000 request units per second using hello .NET SDK:</span></span>

```csharp
// Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
                .Where(r => r.ResourceLink == collection.SelfLink)    
                .AsEnumerable()
                .SingleOrDefault();

// Set hello throughput too5000 request units per second
offer = new OfferV2(offer, 5000);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

<span data-ttu-id="f29bc-152">Não há toohello sem causar impacto na disponibilidade do seu contêiner quando você alterar a taxa de transferência de saudação.</span><span class="sxs-lookup"><span data-stu-id="f29bc-152">There is no impact toohello availability of your container when you change hello throughput.</span></span> <span data-ttu-id="f29bc-153">Normalmente reservado novos Olá de taxa de transferência é efetivo em segundos no aplicativo de taxa de transferência nova hello.</span><span class="sxs-lookup"><span data-stu-id="f29bc-153">Typically hello new reserved throughput is effective within seconds on application of hello new throughput.</span></span>

## <a name="request-unit-considerations"></a><span data-ttu-id="f29bc-154">Considerações sobre unidades de solicitação</span><span class="sxs-lookup"><span data-stu-id="f29bc-154">Request unit considerations</span></span>
<span data-ttu-id="f29bc-155">Ao estimar o número de saudação do tooreserve de unidades de solicitação para o contêiner de banco de dados do Azure Cosmos, é importante tootake Olá variáveis a seguir em consideração:</span><span class="sxs-lookup"><span data-stu-id="f29bc-155">When estimating hello number of request units tooreserve for your Azure Cosmos DB container, it is important tootake hello following variables into consideration:</span></span>

* <span data-ttu-id="f29bc-156">**Tamanho do item**.</span><span class="sxs-lookup"><span data-stu-id="f29bc-156">**Item size**.</span></span> <span data-ttu-id="f29bc-157">Olá unidades consumidas tooread aumenta o tamanho ou gravar dados de saudação também aumentará.</span><span class="sxs-lookup"><span data-stu-id="f29bc-157">As size increases hello units consumed tooread or write hello data will also increase.</span></span>
* <span data-ttu-id="f29bc-158">**Contagem de propriedades do item**.</span><span class="sxs-lookup"><span data-stu-id="f29bc-158">**Item property count**.</span></span> <span data-ttu-id="f29bc-159">Supondo que a indexação de padrão de todas as propriedades, Olá unidades consumidas toowrite um documento/nó/ntity aumentará o aumento do número de propriedade hello.</span><span class="sxs-lookup"><span data-stu-id="f29bc-159">Assuming default indexing of all properties, hello units consumed toowrite a document/node/ntity will increase as hello property count increases.</span></span>
* <span data-ttu-id="f29bc-160">**Consistência de dados**.</span><span class="sxs-lookup"><span data-stu-id="f29bc-160">**Data consistency**.</span></span> <span data-ttu-id="f29bc-161">Ao usar níveis de consistência de dados de alta segurança ou envelhecimento limitado, unidades adicionais será consumido tooread itens.</span><span class="sxs-lookup"><span data-stu-id="f29bc-161">When using data consistency levels of Strong or Bounded Staleness, additional units will be consumed tooread items.</span></span>
* <span data-ttu-id="f29bc-162">**Propriedades indexadas**.</span><span class="sxs-lookup"><span data-stu-id="f29bc-162">**Indexed properties**.</span></span> <span data-ttu-id="f29bc-163">Uma política de índice em cada contêiner determina quais propriedades são indexadas por padrão.</span><span class="sxs-lookup"><span data-stu-id="f29bc-163">An index policy on each container determines which properties are indexed by default.</span></span> <span data-ttu-id="f29bc-164">Você pode reduzir o consumo de unidade de solicitação, limitando o número de saudação de propriedades indexadas ou habilitando o recurso de indexação lento.</span><span class="sxs-lookup"><span data-stu-id="f29bc-164">You can reduce your request unit consumption by limiting hello number of indexed properties or by enabling lazy indexing.</span></span>
* <span data-ttu-id="f29bc-165">**Indexação de documentos**.</span><span class="sxs-lookup"><span data-stu-id="f29bc-165">**Document indexing**.</span></span> <span data-ttu-id="f29bc-166">Por padrão a que cada item é indexado automaticamente, consumirá menos unidades de solicitação se você escolher não tooindex alguns de seus itens.</span><span class="sxs-lookup"><span data-stu-id="f29bc-166">By default each item is automatically indexed, you will consume fewer request units if you choose not tooindex some of your items.</span></span>
* <span data-ttu-id="f29bc-167">**Padrões de consulta**.</span><span class="sxs-lookup"><span data-stu-id="f29bc-167">**Query patterns**.</span></span> <span data-ttu-id="f29bc-168">complexidade de saudação de uma consulta afeta quantas unidades de solicitação são consumidas para uma operação.</span><span class="sxs-lookup"><span data-stu-id="f29bc-168">hello complexity of a query impacts how many Request Units are consumed for an operation.</span></span> <span data-ttu-id="f29bc-169">número de saudação de predicados, natureza dos predicados hello, projeções, número de UDFs e tamanho de saudação do conjunto de dados de origem Olá todos influenciam o custo de saudação de operações de consulta.</span><span class="sxs-lookup"><span data-stu-id="f29bc-169">hello number of predicates, nature of hello predicates, projections, number of UDFs, and hello size of hello source data set all influence hello cost of query operations.</span></span>
* <span data-ttu-id="f29bc-170">**Uso de scripts**.</span><span class="sxs-lookup"><span data-stu-id="f29bc-170">**Script usage**.</span></span>  <span data-ttu-id="f29bc-171">Assim como acontece com consultas, procedimentos armazenados e gatilhos consumam unidades de solicitação com base em complexidade Olá das operações de saudação que está sendo executada.</span><span class="sxs-lookup"><span data-stu-id="f29bc-171">As with queries, stored procedures and triggers consume request units based on hello complexity of hello operations being performed.</span></span> <span data-ttu-id="f29bc-172">À medida que desenvolve seu aplicativo, inspecionar a carga de solicitação Olá cabeçalho toobetter entender como cada operação está consumindo a capacidade da unidade de solicitação.</span><span class="sxs-lookup"><span data-stu-id="f29bc-172">As you develop your application, inspect hello request charge header toobetter understand how each operation is consuming request unit capacity.</span></span>

## <a name="estimating-throughput-needs"></a><span data-ttu-id="f29bc-173">Estimativa das necessidades de produção</span><span class="sxs-lookup"><span data-stu-id="f29bc-173">Estimating throughput needs</span></span>
<span data-ttu-id="f29bc-174">Uma unidade de solicitação é uma medida normalizada de custo de processamento de solicitação.</span><span class="sxs-lookup"><span data-stu-id="f29bc-174">A request unit is a normalized measure of request processing cost.</span></span> <span data-ttu-id="f29bc-175">Uma unidade única solicitação representa Olá processamento capacidade necessária tooread (via autolink ou id) um único 1KB item consiste em 10 valores de propriedade unique (excluindo as propriedades do sistema).</span><span class="sxs-lookup"><span data-stu-id="f29bc-175">A single request unit represents hello processing capacity required tooread (via self link or id) a single 1KB item consisting of 10 unique property values (excluding system properties).</span></span> <span data-ttu-id="f29bc-176">Uma solicitação toocreate (inserir), substituir ou excluir Olá mesmo item consumirá mais processamento do serviço de saudação e, portanto, mais unidades de solicitação.</span><span class="sxs-lookup"><span data-stu-id="f29bc-176">A request toocreate (insert), replace or delete hello same item will consume more processing from hello service and thereby more request units.</span></span>   

> [!NOTE]
> <span data-ttu-id="f29bc-177">linha de base de saudação da unidade de solicitação de 1 para 1KB item corresponde tooa simple obter self link ou a id do item de saudação.</span><span class="sxs-lookup"><span data-stu-id="f29bc-177">hello baseline of 1 request unit for a 1KB item corresponds tooa simple GET by self link or id of hello item.</span></span>
> 
> 

<span data-ttu-id="f29bc-178">Por exemplo, aqui está uma tabela que mostra a solicitação de quantas unidades tooprovision em três tamanhos de item diferentes (1KB, 4KB e 64KB) e em dois níveis diferentes de desempenho (leituras de 500/segundo 100 gravações por segundo e 500 leituras/segundo + 500 gravações por segundo).</span><span class="sxs-lookup"><span data-stu-id="f29bc-178">For example, here's a table that shows how many request units tooprovision at three different item sizes (1KB, 4KB, and 64KB) and at two different performance levels (500 reads/second + 100 writes/second and 500 reads/second + 500 writes/second).</span></span> <span data-ttu-id="f29bc-179">consistência de dados Olá foi configurada na sessão e Olá política de indexação foi definido tooNone.</span><span class="sxs-lookup"><span data-stu-id="f29bc-179">hello data consistency was configured at Session, and hello indexing policy was set tooNone.</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="f29bc-180"><strong>Tamanho do item</strong></span><span class="sxs-lookup"><span data-stu-id="f29bc-180"><strong>Item size</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f29bc-181"><strong>Leituras/segundo</strong></span><span class="sxs-lookup"><span data-stu-id="f29bc-181"><strong>Reads/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f29bc-182"><strong>Gravações/segundo</strong></span><span class="sxs-lookup"><span data-stu-id="f29bc-182"><strong>Writes/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f29bc-183"><strong>Unidades de solicitação</strong></span><span class="sxs-lookup"><span data-stu-id="f29bc-183"><strong>Request units</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="f29bc-184">1 KB</span><span class="sxs-lookup"><span data-stu-id="f29bc-184">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f29bc-185">500</span><span class="sxs-lookup"><span data-stu-id="f29bc-185">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f29bc-186">100</span><span class="sxs-lookup"><span data-stu-id="f29bc-186">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f29bc-187">(500 * 1) + (100 * 5) = 1.000 RU/s</span><span class="sxs-lookup"><span data-stu-id="f29bc-187">(500 * 1) + (100 * 5) = 1,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="f29bc-188">1 KB</span><span class="sxs-lookup"><span data-stu-id="f29bc-188">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f29bc-189">500</span><span class="sxs-lookup"><span data-stu-id="f29bc-189">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f29bc-190">500</span><span class="sxs-lookup"><span data-stu-id="f29bc-190">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f29bc-191">(500 * 1) + (500 * 5) = 3.000 RU/s</span><span class="sxs-lookup"><span data-stu-id="f29bc-191">(500 * 1) + (500 * 5) = 3,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="f29bc-192">4 KB</span><span class="sxs-lookup"><span data-stu-id="f29bc-192">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f29bc-193">500</span><span class="sxs-lookup"><span data-stu-id="f29bc-193">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f29bc-194">100</span><span class="sxs-lookup"><span data-stu-id="f29bc-194">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f29bc-195">(500 * 1,3) + (100 * 7) = 1.350 RU/s</span><span class="sxs-lookup"><span data-stu-id="f29bc-195">(500 * 1.3) + (100 * 7) = 1,350 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="f29bc-196">4 KB</span><span class="sxs-lookup"><span data-stu-id="f29bc-196">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f29bc-197">500</span><span class="sxs-lookup"><span data-stu-id="f29bc-197">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f29bc-198">500</span><span class="sxs-lookup"><span data-stu-id="f29bc-198">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f29bc-199">(500 * 1,3) + (500 * 7) = 4.150 RU/s</span><span class="sxs-lookup"><span data-stu-id="f29bc-199">(500 * 1.3) + (500 * 7) = 4,150 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="f29bc-200">64 KB</span><span class="sxs-lookup"><span data-stu-id="f29bc-200">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f29bc-201">500</span><span class="sxs-lookup"><span data-stu-id="f29bc-201">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f29bc-202">100</span><span class="sxs-lookup"><span data-stu-id="f29bc-202">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f29bc-203">(500 * 10) + (100 * 48) = 9.800 RU/s</span><span class="sxs-lookup"><span data-stu-id="f29bc-203">(500 * 10) + (100 * 48) = 9,800 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="f29bc-204">64 KB</span><span class="sxs-lookup"><span data-stu-id="f29bc-204">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f29bc-205">500</span><span class="sxs-lookup"><span data-stu-id="f29bc-205">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f29bc-206">500</span><span class="sxs-lookup"><span data-stu-id="f29bc-206">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="f29bc-207">(500 * 10) + (500 * 48) = 29.000 RU/s</span><span class="sxs-lookup"><span data-stu-id="f29bc-207">(500 * 10) + (500 * 48) = 29,000 RU/s</span></span></p></td>
        </tr>
    </tbody>
</table>

### <a name="use-hello-request-unit-calculator"></a><span data-ttu-id="f29bc-208">Use a Calculadora de unidade de solicitação Olá</span><span class="sxs-lookup"><span data-stu-id="f29bc-208">Use hello request unit calculator</span></span>
<span data-ttu-id="f29bc-209">problemas de clientes toohelp ajustar suas estimativas de taxa de transferência, não há um baseado na web [Calculadora de unidade de solicitação](https://www.documentdb.com/capacityplanner) toohelp estimar Olá solicitação unidade requisitos para operações comuns, incluindo:</span><span class="sxs-lookup"><span data-stu-id="f29bc-209">toohelp customers fine tune their throughput estimations, there is a web based [request unit calculator](https://www.documentdb.com/capacityplanner) toohelp estimate hello request unit requirements for typical operations, including:</span></span>

* <span data-ttu-id="f29bc-210">Criações de itens (gravações)</span><span class="sxs-lookup"><span data-stu-id="f29bc-210">Item creates (writes)</span></span>
* <span data-ttu-id="f29bc-211">Leituras de itens</span><span class="sxs-lookup"><span data-stu-id="f29bc-211">Item reads</span></span>
* <span data-ttu-id="f29bc-212">Exclusões de itens</span><span class="sxs-lookup"><span data-stu-id="f29bc-212">Item deletes</span></span>
* <span data-ttu-id="f29bc-213">Atualizações de itens</span><span class="sxs-lookup"><span data-stu-id="f29bc-213">Item updates</span></span>

<span data-ttu-id="f29bc-214">ferramenta de saudação também inclui suporte para estimar as necessidades de armazenamento de dados com base nos itens do exemplo hello que você fornecer.</span><span class="sxs-lookup"><span data-stu-id="f29bc-214">hello tool also includes support for estimating data storage needs based on hello sample items you provide.</span></span>

<span data-ttu-id="f29bc-215">Usando a ferramenta de saudação é simple:</span><span class="sxs-lookup"><span data-stu-id="f29bc-215">Using hello tool is simple:</span></span>

1. <span data-ttu-id="f29bc-216">Carregue um ou mais itens representativos.</span><span class="sxs-lookup"><span data-stu-id="f29bc-216">Upload one or more representative items.</span></span>
   
    ![Carregar o cálculo de unidade de solicitação de toohello itens][2]
2. <span data-ttu-id="f29bc-218">requisitos de armazenamento de dados tooestimate, insira o número total de saudação de itens esperada toostore.</span><span class="sxs-lookup"><span data-stu-id="f29bc-218">tooestimate data storage requirements, enter hello total number of items you expect toostore.</span></span>
3. <span data-ttu-id="f29bc-219">Inserir número Olá de itens a criar, ler, atualizar e excluir operações requer (em uma base por segundo).</span><span class="sxs-lookup"><span data-stu-id="f29bc-219">Enter hello number of items create, read, update, and delete operations you require (on a per-second basis).</span></span> <span data-ttu-id="f29bc-220">encargos de unidade de solicitação tooestimate Olá de operações de atualização de item, carregue uma cópia do item do exemplo hello da etapa 1 acima, o que inclui atualizações de campo típico.</span><span class="sxs-lookup"><span data-stu-id="f29bc-220">tooestimate hello request unit charges of item update operations, upload a copy of hello sample item from step 1 above that includes typical field updates.</span></span>  <span data-ttu-id="f29bc-221">Por exemplo, se as atualizações de item normalmente modificam duas propriedades chamadas lastLogin e userVisits, simplesmente copiar item do exemplo hello, atualizar Olá valores para essas duas propriedades e carregar item Olá copiado.</span><span class="sxs-lookup"><span data-stu-id="f29bc-221">For example, if item updates typically modify two properties named lastLogin and userVisits, then simply copy hello sample item, update hello values for those two properties, and upload hello copied item.</span></span>
   
    ![Insira os requisitos de taxa de transferência no cálculo de unidade de solicitação Olá][3]
4. <span data-ttu-id="f29bc-223">Clique em calcular e examine os resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="f29bc-223">Click calculate and examine hello results.</span></span>
   
    ![Resultados da calculadora de unidade de solicitação][4]

> [!NOTE]
> <span data-ttu-id="f29bc-225">Se você tiver tipos de item que serão muito diferente em termos de tamanho e hello número de propriedades indexadas, em seguida, carregue um exemplo de cada *tipo* de item típico toohello ferramenta e, em seguida, calcular os resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="f29bc-225">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then upload a sample of each *type* of typical item toohello tool and then calculate hello results.</span></span>
> 
> 

### <a name="use-hello-azure-cosmos-db-request-charge-response-header"></a><span data-ttu-id="f29bc-226">Use o cabeçalho de resposta de custos do hello Azure Cosmos DB solicitação</span><span class="sxs-lookup"><span data-stu-id="f29bc-226">Use hello Azure Cosmos DB request charge response header</span></span>
<span data-ttu-id="f29bc-227">Cada resposta do hello Azure Cosmos DB serviço inclui um cabeçalho personalizado (`x-ms-request-charge`) que contém unidades de solicitação Olá consumidas para solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="f29bc-227">Every response from hello Azure Cosmos DB service includes a custom header (`x-ms-request-charge`) that contains hello request units consumed for hello request.</span></span> <span data-ttu-id="f29bc-228">Esse cabeçalho também é acessível por meio de saudação do Azure Cosmos SDKs do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f29bc-228">This header is also accessible through hello Azure Cosmos DB SDKs.</span></span> <span data-ttu-id="f29bc-229">Em Olá .NET SDK, RequestCharge é uma propriedade do objeto de ResourceResponse hello.</span><span class="sxs-lookup"><span data-stu-id="f29bc-229">In hello .NET SDK, RequestCharge is a property of hello ResourceResponse object.</span></span>  <span data-ttu-id="f29bc-230">Para consultas, Olá Gerenciador de consulta de banco de dados do Azure Cosmos em Olá portal do Azure fornece informações de taxa de solicitação para consultas executadas.</span><span class="sxs-lookup"><span data-stu-id="f29bc-230">For queries, hello Azure Cosmos DB Query Explorer in hello Azure portal provides request charge information for executed queries.</span></span>

![Examinando os encargos de RU no hello Pesquisador de objetos de consulta][1]

<span data-ttu-id="f29bc-232">Com isso em mente, um método para calcular a quantidade de saudação de produtividade reservados exigida por seu aplicativo é associado à execução de operações típicas em relação a um representante item usado pelo seu aplicativo dos custos de unidade de solicitação toorecord hello e, em seguida, estimar Olá número de operações você antecipar executando a cada segundo.</span><span class="sxs-lookup"><span data-stu-id="f29bc-232">With this in mind, one method for estimating hello amount of reserved throughput required by your application is toorecord hello request unit charge associated with running typical operations against a representative item used by your application and then estimating hello number of operations you anticipate performing each second.</span></span>  <span data-ttu-id="f29bc-233">Ser toomeasure se e incluem consultas típicas e uso de script de banco de dados do Azure Cosmos também.</span><span class="sxs-lookup"><span data-stu-id="f29bc-233">Be sure toomeasure and include typical queries and Azure Cosmos DB script usage as well.</span></span>

> [!NOTE]
> <span data-ttu-id="f29bc-234">Se você tiver tipos de item que serão muito diferente em termos de tamanho e hello número de propriedades indexadas, registre associada a cada carga de unidade Olá operação aplicável solicitação *tipo* de item típico.</span><span class="sxs-lookup"><span data-stu-id="f29bc-234">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then record hello applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

<span data-ttu-id="f29bc-235">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f29bc-235">For example:</span></span>

1. <span data-ttu-id="f29bc-236">Registre os custos de unidade de solicitação de saudação de criação (inserir) um item típico.</span><span class="sxs-lookup"><span data-stu-id="f29bc-236">Record hello request unit charge of creating (inserting) a typical item.</span></span> 
2. <span data-ttu-id="f29bc-237">Encargo de unidade de solicitação de registro Olá de leitura de um item típico.</span><span class="sxs-lookup"><span data-stu-id="f29bc-237">Record hello request unit charge of reading a typical item.</span></span>
3. <span data-ttu-id="f29bc-238">Custos de unidade de solicitação de registro Olá de atualização de um item típico.</span><span class="sxs-lookup"><span data-stu-id="f29bc-238">Record hello request unit charge of updating a typical item.</span></span>
4. <span data-ttu-id="f29bc-239">Encargo de unidade de solicitação Olá registro de consultas de item típico, comuns.</span><span class="sxs-lookup"><span data-stu-id="f29bc-239">Record hello request unit charge of typical, common item queries.</span></span>
5. <span data-ttu-id="f29bc-240">Olá registro solicitação unidade encargo de quaisquer scripts personalizados (procedimentos armazenados, disparadores, funções definidas pelo usuário) utilizado pelo aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="f29bc-240">Record hello request unit charge of any custom scripts (stored procedures, triggers, user-defined functions) leveraged by hello application</span></span>
6. <span data-ttu-id="f29bc-241">Calcule a solicitação de necessária Olá que unidades especificadas Olá estimada o número de operações você antecipar toorun por segundo.</span><span class="sxs-lookup"><span data-stu-id="f29bc-241">Calculate hello required request units given hello estimated number of operations you anticipate toorun each second.</span></span>

### <span data-ttu-id="f29bc-242"><a id="GetLastRequestStatistics"></a>Usar o comando GetLastRequestStatistics da API para MongoDB</span><span class="sxs-lookup"><span data-stu-id="f29bc-242"><a id="GetLastRequestStatistics"></a>Use API for MongoDB's GetLastRequestStatistics command</span></span>
<span data-ttu-id="f29bc-243">API para o MongoDB dá suporte a um comando personalizado, *getLastRequestStatistics*, para recuperar a taxa de solicitação de saudação para operações especificadas.</span><span class="sxs-lookup"><span data-stu-id="f29bc-243">API for MongoDB supports a custom command, *getLastRequestStatistics*, for retrieving hello request charge for specified operations.</span></span>

<span data-ttu-id="f29bc-244">Por exemplo, em Olá Shell Mongo, execute operação de Olá que deseja tooverify Olá solicitação gratuitamente.</span><span class="sxs-lookup"><span data-stu-id="f29bc-244">For example, in hello Mongo Shell, execute hello operation you want tooverify hello request charge for.</span></span>
```
> db.sample.find()
```

<span data-ttu-id="f29bc-245">Em seguida, execute o comando Olá *getLastRequestStatistics*.</span><span class="sxs-lookup"><span data-stu-id="f29bc-245">Next, execute hello command *getLastRequestStatistics*.</span></span>
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

<span data-ttu-id="f29bc-246">Com isso em mente, um método para calcular a quantidade de saudação de produtividade reservados exigida por seu aplicativo é associado à execução de operações típicas em relação a um representante item usado pelo seu aplicativo dos custos de unidade de solicitação toorecord hello e, em seguida, estimar Olá número de operações você antecipar executando a cada segundo.</span><span class="sxs-lookup"><span data-stu-id="f29bc-246">With this in mind, one method for estimating hello amount of reserved throughput required by your application is toorecord hello request unit charge associated with running typical operations against a representative item used by your application and then estimating hello number of operations you anticipate performing each second.</span></span>

> [!NOTE]
> <span data-ttu-id="f29bc-247">Se você tiver tipos de item que serão muito diferente em termos de tamanho e hello número de propriedades indexadas, registre associada a cada carga de unidade Olá operação aplicável solicitação *tipo* de item típico.</span><span class="sxs-lookup"><span data-stu-id="f29bc-247">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then record hello applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

## <a name="use-api-for-mongodbs-portal-metrics"></a><span data-ttu-id="f29bc-248">Usar as métricas de portal da API para MongoDB</span><span class="sxs-lookup"><span data-stu-id="f29bc-248">Use API for MongoDB's portal metrics</span></span>
<span data-ttu-id="f29bc-249">Olá tooget de maneira mais simples uma boa estimativa da unidade de solicitação de encargos para a sua API para o banco de dados do MongoDB é toouse Olá [portal do Azure](https://portal.azure.com) métricas.</span><span class="sxs-lookup"><span data-stu-id="f29bc-249">hello simplest way tooget a good estimation of request unit charges for your API for MongoDB database is toouse hello [Azure portal](https://portal.azure.com) metrics.</span></span> <span data-ttu-id="f29bc-250">Com hello *o número de solicitações* e *custos de solicitação* gráficos, você pode obter uma estimativa de quantas unidades de solicitação cada operação de consumo e quantas unidades de solicitação consomem relativo tooone outro.</span><span class="sxs-lookup"><span data-stu-id="f29bc-250">With hello *Number of requests* and *Request Charge* charts, you can get an estimation of how many request units each operation is consuming and how many request units they consume relative tooone another.</span></span>

![Métricas do portal da API para MongoDB][6]

## <a name="a-request-unit-estimation-example"></a><span data-ttu-id="f29bc-252">Um exemplo de estimativa de unidade de solicitação</span><span class="sxs-lookup"><span data-stu-id="f29bc-252">A request unit estimation example</span></span>
<span data-ttu-id="f29bc-253">Considere Olá aproximadamente 1KB documento a seguir:</span><span class="sxs-lookup"><span data-stu-id="f29bc-253">Consider hello following ~1KB document:</span></span>

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
> <span data-ttu-id="f29bc-254">Documentos são minimizados no banco de dados do Azure Cosmos, portanto calculado pelo sistema Olá tamanho do documento de saudação acima é um pouco menos de 1KB.</span><span class="sxs-lookup"><span data-stu-id="f29bc-254">Documents are minified in Azure Cosmos DB, so hello system calculated size of hello document above is slightly less than 1KB.</span></span>
> 
> 

<span data-ttu-id="f29bc-255">Hello tabela a seguir mostra a solicitação aproximada encargos de unidade para operações típicas neste item (encargos de unidade de solicitação aproximado Olá presume que o nível de consistência de conta Olá é definido muito "Sessão" e todos os itens são indexados automaticamente):</span><span class="sxs-lookup"><span data-stu-id="f29bc-255">hello following table shows approximate request unit charges for typical operations on this item (hello approximate request unit charge assumes that hello account consistency level is set too“Session” and that all items are automatically indexed):</span></span>

| <span data-ttu-id="f29bc-256">Operação</span><span class="sxs-lookup"><span data-stu-id="f29bc-256">Operation</span></span> | <span data-ttu-id="f29bc-257">Encargo de Unidade de Solicitação</span><span class="sxs-lookup"><span data-stu-id="f29bc-257">Request Unit Charge</span></span> |
| --- | --- |
| <span data-ttu-id="f29bc-258">Criar item</span><span class="sxs-lookup"><span data-stu-id="f29bc-258">Create item</span></span> |<span data-ttu-id="f29bc-259">Cerca de 15 RUs</span><span class="sxs-lookup"><span data-stu-id="f29bc-259">~15 RU</span></span> |
| <span data-ttu-id="f29bc-260">Ler item</span><span class="sxs-lookup"><span data-stu-id="f29bc-260">Read item</span></span> |<span data-ttu-id="f29bc-261">Cerca de 1 RU</span><span class="sxs-lookup"><span data-stu-id="f29bc-261">~1 RU</span></span> |
| <span data-ttu-id="f29bc-262">Consultar item por ID</span><span class="sxs-lookup"><span data-stu-id="f29bc-262">Query item by id</span></span> |<span data-ttu-id="f29bc-263">Cerca de 2,5 RUs</span><span class="sxs-lookup"><span data-stu-id="f29bc-263">~2.5 RU</span></span> |

<span data-ttu-id="f29bc-264">Além disso, esta tabela mostra solicitação aproximada encargos de unidade para consultas típicas usadas no aplicativo hello:</span><span class="sxs-lookup"><span data-stu-id="f29bc-264">Additionally, this table shows approximate request unit charges for typical queries used in hello application:</span></span>

| <span data-ttu-id="f29bc-265">Consultar</span><span class="sxs-lookup"><span data-stu-id="f29bc-265">Query</span></span> | <span data-ttu-id="f29bc-266">Encargo de Unidade de Solicitação</span><span class="sxs-lookup"><span data-stu-id="f29bc-266">Request Unit Charge</span></span> | <span data-ttu-id="f29bc-267">Nº de itens retornados</span><span class="sxs-lookup"><span data-stu-id="f29bc-267"># of Returned Items</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f29bc-268">Selecionar alimentos por id</span><span class="sxs-lookup"><span data-stu-id="f29bc-268">Select food by id</span></span> |<span data-ttu-id="f29bc-269">Cerca de 2,5 RUs</span><span class="sxs-lookup"><span data-stu-id="f29bc-269">~2.5 RU</span></span> |<span data-ttu-id="f29bc-270">1</span><span class="sxs-lookup"><span data-stu-id="f29bc-270">1</span></span> |
| <span data-ttu-id="f29bc-271">Selecionar alimentos por fabricante</span><span class="sxs-lookup"><span data-stu-id="f29bc-271">Select foods by manufacturer</span></span> |<span data-ttu-id="f29bc-272">Cerca de 7 RUs</span><span class="sxs-lookup"><span data-stu-id="f29bc-272">~7 RU</span></span> |<span data-ttu-id="f29bc-273">7</span><span class="sxs-lookup"><span data-stu-id="f29bc-273">7</span></span> |
| <span data-ttu-id="f29bc-274">Selecionar por grupo de alimentos e solicitar por peso</span><span class="sxs-lookup"><span data-stu-id="f29bc-274">Select by food group and order by weight</span></span> |<span data-ttu-id="f29bc-275">Cerca de 70 RUs</span><span class="sxs-lookup"><span data-stu-id="f29bc-275">~70 RU</span></span> |<span data-ttu-id="f29bc-276">100</span><span class="sxs-lookup"><span data-stu-id="f29bc-276">100</span></span> |
| <span data-ttu-id="f29bc-277">Selecionar os 10 alimentos principais em um grupo de alimentos</span><span class="sxs-lookup"><span data-stu-id="f29bc-277">Select top 10 foods in a food group</span></span> |<span data-ttu-id="f29bc-278">Cerca de 10 RUs</span><span class="sxs-lookup"><span data-stu-id="f29bc-278">~10 RU</span></span> |<span data-ttu-id="f29bc-279">10</span><span class="sxs-lookup"><span data-stu-id="f29bc-279">10</span></span> |

> [!NOTE]
> <span data-ttu-id="f29bc-280">Encargos de RU variam com base no número de saudação de itens retornados.</span><span class="sxs-lookup"><span data-stu-id="f29bc-280">RU charges vary based on hello number of items returned.</span></span>
> 
> 

<span data-ttu-id="f29bc-281">Com essas informações, podemos estimar requisitos de RU saudação do número de saudação desse aplicativo considerando de operações e consultas que esperamos por segundo:</span><span class="sxs-lookup"><span data-stu-id="f29bc-281">With this information, we can estimate hello RU requirements for this application given hello number of operations and queries we expect per second:</span></span>

| <span data-ttu-id="f29bc-282">Operação/consulta</span><span class="sxs-lookup"><span data-stu-id="f29bc-282">Operation/Query</span></span> | <span data-ttu-id="f29bc-283">Número estimado por segundo</span><span class="sxs-lookup"><span data-stu-id="f29bc-283">Estimated number per second</span></span> | <span data-ttu-id="f29bc-284">RUs necessárias</span><span class="sxs-lookup"><span data-stu-id="f29bc-284">Required RUs</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f29bc-285">Criar item</span><span class="sxs-lookup"><span data-stu-id="f29bc-285">Create item</span></span> |<span data-ttu-id="f29bc-286">10</span><span class="sxs-lookup"><span data-stu-id="f29bc-286">10</span></span> |<span data-ttu-id="f29bc-287">150</span><span class="sxs-lookup"><span data-stu-id="f29bc-287">150</span></span> |
| <span data-ttu-id="f29bc-288">Ler item</span><span class="sxs-lookup"><span data-stu-id="f29bc-288">Read item</span></span> |<span data-ttu-id="f29bc-289">100</span><span class="sxs-lookup"><span data-stu-id="f29bc-289">100</span></span> |<span data-ttu-id="f29bc-290">100</span><span class="sxs-lookup"><span data-stu-id="f29bc-290">100</span></span> |
| <span data-ttu-id="f29bc-291">Selecionar alimentos por fabricante</span><span class="sxs-lookup"><span data-stu-id="f29bc-291">Select foods by manufacturer</span></span> |<span data-ttu-id="f29bc-292">25</span><span class="sxs-lookup"><span data-stu-id="f29bc-292">25</span></span> |<span data-ttu-id="f29bc-293">175</span><span class="sxs-lookup"><span data-stu-id="f29bc-293">175</span></span> |
| <span data-ttu-id="f29bc-294">Selecionar por grupo de alimentos</span><span class="sxs-lookup"><span data-stu-id="f29bc-294">Select by food group</span></span> |<span data-ttu-id="f29bc-295">10</span><span class="sxs-lookup"><span data-stu-id="f29bc-295">10</span></span> |<span data-ttu-id="f29bc-296">700</span><span class="sxs-lookup"><span data-stu-id="f29bc-296">700</span></span> |
| <span data-ttu-id="f29bc-297">Selecionar os 10 principais</span><span class="sxs-lookup"><span data-stu-id="f29bc-297">Select top 10</span></span> |<span data-ttu-id="f29bc-298">15</span><span class="sxs-lookup"><span data-stu-id="f29bc-298">15</span></span> |<span data-ttu-id="f29bc-299">Total de 150</span><span class="sxs-lookup"><span data-stu-id="f29bc-299">150 Total</span></span> |

<span data-ttu-id="f29bc-300">Nesse caso, esperamos um requisito de taxa de transferência médio de 1.275 RUs/s.</span><span class="sxs-lookup"><span data-stu-id="f29bc-300">In this case, we expect an average throughput requirement of 1,275 RU/s.</span></span>  <span data-ttu-id="f29bc-301">Arredondamento toohello mais próximo de 100, seriam provisionar 1.300 RU/s para a coleção deste aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f29bc-301">Rounding up toohello nearest 100, we would provision 1,300 RU/s for this application's collection.</span></span>

## <span data-ttu-id="f29bc-302"><a id="RequestRateTooLarge"></a> Excedendo os limites de produtividade reservada no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f29bc-302"><a id="RequestRateTooLarge"></a> Exceeding reserved throughput limits in Azure Cosmos DB</span></span>
<span data-ttu-id="f29bc-303">Lembre-se de que o consumo de unidade de solicitação é avaliado como uma taxa por segundo se orçamento hello está vazio.</span><span class="sxs-lookup"><span data-stu-id="f29bc-303">Recall that request unit consumption is evaluated as a rate per second if hello budget is empty.</span></span> <span data-ttu-id="f29bc-304">Para aplicativos que excedem Olá taxa de solicitação de provisionamento de unidade para um contêiner, solicitações toothat coleção será limitada até que a taxa de saudação cai abaixo de nível de saudação reservada.</span><span class="sxs-lookup"><span data-stu-id="f29bc-304">For applications that exceed hello provisioned request unit rate for a container, requests toothat collection will be throttled until hello rate drops below hello reserved level.</span></span> <span data-ttu-id="f29bc-305">Quando ocorre uma limitação, o servidor de saudação preventivamente terminará solicitação Olá com RequestRateTooLargeException (código de status HTTP 429) e retorno Olá o cabeçalho x-ms-repetição-após-ms indicando de saudação período de tempo, em milissegundos, que Olá usuário deve aguardar antes de tentar novamente a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="f29bc-305">When a throttle occurs, hello server will preemptively end hello request with RequestRateTooLargeException (HTTP status code 429) and return hello x-ms-retry-after-ms header indicating hello amount of time, in milliseconds, that hello user must wait before reattempting hello request.</span></span>

    HTTP Status 429
    Status Line: RequestRateTooLarge
    x-ms-retry-after-ms :100

<span data-ttu-id="f29bc-306">Se você estiver usando consultas de SDK de cliente .NET e LINQ hello e maior parte do tempo de saudação nunca tiver toodeal com esta exceção, como a versão atual de saudação do hello SDK de cliente .NET implicitamente captura essa resposta, aspectos Olá servidor especificado cabeçalho retry-after, e solicitação de saudação de repetições.</span><span class="sxs-lookup"><span data-stu-id="f29bc-306">If you are using hello .NET Client SDK and LINQ queries, then most of hello time you never have toodeal with this exception, as hello current version of hello .NET Client SDK implicitly catches this response, respects hello server-specified retry-after header, and retries hello request.</span></span> <span data-ttu-id="f29bc-307">A menos que sua conta está sendo acessada simultaneamente por vários clientes, a próxima repetição de saudação terá êxito.</span><span class="sxs-lookup"><span data-stu-id="f29bc-307">Unless your account is being accessed concurrently by multiple clients, hello next retry will succeed.</span></span>

<span data-ttu-id="f29bc-308">Se você tiver mais de um cliente cumulativamente operando acima a taxa de solicitação hello, hello comportamento de repetição padrão pode não ser suficiente e cliente Olá lançará um DocumentClientException com o aplicativo de 429 toohello status código.</span><span class="sxs-lookup"><span data-stu-id="f29bc-308">If you have more than one client cumulatively operating above hello request rate, hello default retry behavior may not suffice, and hello client will throw a DocumentClientException with status code 429 toohello application.</span></span> <span data-ttu-id="f29bc-309">Em casos como esse, você pode considerar o tratamento de comportamento de repetição e lógica de erro do aplicativo as rotinas de tratamento ou aumentando a taxa de transferência reservada para o contêiner de Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="f29bc-309">In cases such as this, you may consider handling retry behavior and logic in your application's error handling routines or increasing hello reserved throughput for hello container.</span></span>

## <span data-ttu-id="f29bc-310"><a id="RequestRateTooLargeAPIforMongoDB"></a> Exceder os limites de taxa de transferência reservada na API para MongoDB</span><span class="sxs-lookup"><span data-stu-id="f29bc-310"><a id="RequestRateTooLargeAPIforMongoDB"></a> Exceeding reserved throughput limits in API for MongoDB</span></span>
<span data-ttu-id="f29bc-311">Aplicativos que excedem a unidades de solicitação Olá provisionado para uma coleção serão limitados até que a taxa de saudação cai abaixo de nível de saudação reservada.</span><span class="sxs-lookup"><span data-stu-id="f29bc-311">Applications that exceed hello provisioned request units for a collection will be throttled until hello rate drops below hello reserved level.</span></span> <span data-ttu-id="f29bc-312">Quando ocorre um acelerador, Olá back-end preventivamente terminará solicitação Olá com um *16500* código de erro - *muito muitas solicitações*.</span><span class="sxs-lookup"><span data-stu-id="f29bc-312">When a throttle occurs, hello backend will preemptively end hello request with a *16500* error code - *Too Many Requests*.</span></span> <span data-ttu-id="f29bc-313">Por padrão, a API para o MongoDB automaticamente tentará too10 horas antes de retornar um *muito muitas solicitações* código de erro.</span><span class="sxs-lookup"><span data-stu-id="f29bc-313">By default, API for MongoDB will automatically retry up too10 times before returning a *Too Many Requests* error code.</span></span> <span data-ttu-id="f29bc-314">Se você estiver recebendo muitas *muito muitas solicitações* códigos de erro, você pode considerar o comportamento de repetição de adição em rotinas de tratamento de erros do aplicativo ou [aumenta o processamento reservado para a coleção de saudaçãoOlá](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="f29bc-314">If you are receiving many *Too Many Requests* error codes, you may consider either adding retry behavior in your application's error handling routines or [increasing hello reserved throughput for hello collection](set-throughput.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f29bc-315">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f29bc-315">Next steps</span></span>
<span data-ttu-id="f29bc-316">toolearn mais informações sobre a taxa de transferência reservada com bancos de dados do banco de dados do Azure Cosmos explorar estes recursos:</span><span class="sxs-lookup"><span data-stu-id="f29bc-316">toolearn more about reserved throughput with Azure Cosmos DB databases, explore these resources:</span></span>

* [<span data-ttu-id="f29bc-317">Preços do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f29bc-317">Azure Cosmos DB pricing</span></span>](https://azure.microsoft.com/pricing/details/cosmos-db/)
* [<span data-ttu-id="f29bc-318">Particionando dados no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f29bc-318">Partitioning data in Azure Cosmos DB</span></span>](partition-data.md)

<span data-ttu-id="f29bc-319">toolearn mais sobre Azure Cosmos DB, consulte hello Azure Cosmos DB [documentação](https://azure.microsoft.com/documentation/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="f29bc-319">toolearn more about Azure Cosmos DB, see hello Azure Cosmos DB [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/).</span></span> 

<span data-ttu-id="f29bc-320">tooget iniciado com a escala e testes de desempenho com o Azure Cosmos DB, consulte [teste de desempenho e escala com o banco de dados do Azure Cosmos](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="f29bc-320">tooget started with scale and performance testing with Azure Cosmos DB, see [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md).</span></span>

[1]: ./media/request-units/queryexplorer.png 
[2]: ./media/request-units/RUEstimatorUpload.png
[3]: ./media/request-units/RUEstimatorDocuments.png
[4]: ./media/request-units/RUEstimatorResults.png
[5]: ./media/request-units/RUCalculator2.png
[6]: ./media/request-units/api-for-mongodb-metrics.png
