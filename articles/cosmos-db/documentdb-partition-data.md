---
title: Particionamento e escala no Azure Cosmos DB | Microsoft Docs
description: "Saiba mais sobre como o particionamento funciona no DB Cosmos do Azure, como configurar o particionamento e as chaves de partição e como escolher a chave de partição correta para seu aplicativo."
services: cosmos-db
author: arramac
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 702c39b4-1798-48dd-9993-4493a2f6df9e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 81010d91ac7fe8fa7149c52ed56af304cf4e83d9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="partitioning-in-azure-cosmos-db-using-the-documentdb-api"></a><span data-ttu-id="dd531-103">Particionamento no Azure Cosmos DB usando a API do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="dd531-103">Partitioning in Azure Cosmos DB using the DocumentDB API</span></span>

<span data-ttu-id="dd531-104">O [DB Cosmos do Microsoft Azure](../cosmos-db/introduction.md) é um serviço com vários modelos de banco de dados, distribuído globalmente, que foi criado para ajudá-lo a obter um desempenho rápido e previsível e a dimensionar continuamente conforme o crescimento de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dd531-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) is a global distributed, multi-model database service designed to help you achieve fast, predictable performance and scale seamlessly along with your application as it grows.</span></span> 

<span data-ttu-id="dd531-105">Este artigo fornece uma visão geral de como trabalhar com o particionamento de contêineres do Cosmos DB com a API do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="dd531-105">This article provides an overview of how to work with partitioning of Cosmos DB containers with the DocumentDB API.</span></span> <span data-ttu-id="dd531-106">Consulte [particionamento e escala horizontal](../cosmos-db/partition-data.md) para obter uma visão geral dos conceitos e das melhores práticas de particionamento com uma API do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="dd531-106">See [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

<span data-ttu-id="dd531-107">Para começar a codificar, baixe o projeto no [GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="dd531-107">To get started with code, download the project from [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<span data-ttu-id="dd531-108">Depois de ler este artigo, você poderá responder as seguintes perguntas:</span><span class="sxs-lookup"><span data-stu-id="dd531-108">After reading this article, you will be able to answer the following questions:</span></span>   

* <span data-ttu-id="dd531-109">Como funciona o particionamento no Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="dd531-109">How does partitioning work in Azure Cosmos DB?</span></span>
* <span data-ttu-id="dd531-110">Como fazer para configurar o particionamento no Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="dd531-110">How do I configure partitioning in Azure Cosmos DB</span></span>
* <span data-ttu-id="dd531-111">O que são chaves de partição e como escolher a chave de partição correta para meu aplicativo?</span><span class="sxs-lookup"><span data-stu-id="dd531-111">What are partition keys, and how do I pick the right partition key for my application?</span></span>

<span data-ttu-id="dd531-112">Para começar a codificar, baixe o projeto na [Amostra de Test Drive de Desempenho do Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="dd531-112">To get started with code, download the project from [Azure Cosmos DB Performance Testing Driver Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<!-- placeholder until we have a permanent solution-->
<a name="partition-keys"></a>
<a name="single-partition-and-partitioned-collections"></a>
<a name="migrating-from-single-partition"></a>

## <a name="partition-keys"></a><span data-ttu-id="dd531-113">Chaves de partição</span><span class="sxs-lookup"><span data-stu-id="dd531-113">Partition keys</span></span>

<span data-ttu-id="dd531-114">Na API do DocumentDB, você especifica a definição da chave de partição na forma de um caminho JSON.</span><span class="sxs-lookup"><span data-stu-id="dd531-114">In the DocumentDB API, you specify the partition key definition in the form of a JSON path.</span></span> <span data-ttu-id="dd531-115">A tabela a seguir mostra exemplos de definições de chave de partição e os valores correspondentes a cada uma.</span><span class="sxs-lookup"><span data-stu-id="dd531-115">The following table shows examples of partition key definitions and the values corresponding to each.</span></span> <span data-ttu-id="dd531-116">A chave de partição é especificada como um caminho, por exemplo, `/department` representa o departamento de propriedade.</span><span class="sxs-lookup"><span data-stu-id="dd531-116">The partition key is specified as a path, e.g. `/department` represents the property department.</span></span> 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="dd531-117"><strong>Chave de partição</strong></span><span class="sxs-lookup"><span data-stu-id="dd531-117"><strong>Partition Key</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="dd531-118"><strong>Descrição</strong></span><span class="sxs-lookup"><span data-stu-id="dd531-118"><strong>Description</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="dd531-119">/department</span><span class="sxs-lookup"><span data-stu-id="dd531-119">/department</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="dd531-120">Corresponde ao valor de doc.department, em que doc é o item.</span><span class="sxs-lookup"><span data-stu-id="dd531-120">Corresponds to the value of doc.department where doc is the item.</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="dd531-121">/properties/name</span><span class="sxs-lookup"><span data-stu-id="dd531-121">/properties/name</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="dd531-122">Corresponde ao valor de doc.properties.name, em que doc é o item (propriedade aninhada).</span><span class="sxs-lookup"><span data-stu-id="dd531-122">Corresponds to the value of doc.properties.name where doc is the item (nested property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="dd531-123">/id</span><span class="sxs-lookup"><span data-stu-id="dd531-123">/id</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="dd531-124">Corresponde ao valor de doc.id (a ID e a chave de partição são a mesma propriedade).</span><span class="sxs-lookup"><span data-stu-id="dd531-124">Corresponds to the value of doc.id (id and partition key are the same property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="dd531-125">/"nome do departamento"</span><span class="sxs-lookup"><span data-stu-id="dd531-125">/"department name"</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="dd531-126">Corresponde ao valor de doc[“nome do departamento”], em que doc é o item.</span><span class="sxs-lookup"><span data-stu-id="dd531-126">Corresponds to the value of doc["department name"] where doc is the item.</span></span></p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> <span data-ttu-id="dd531-127">A sintaxe da chave de partição é semelhante à especificação de caminho para caminhos de política de indexação, com a diferença básica de que o caminho corresponde à propriedade em vez do valor, ou seja, não há nenhum caractere curinga no final.</span><span class="sxs-lookup"><span data-stu-id="dd531-127">The syntax for partition key is similar to the path specification for indexing policy paths with the key difference that the path corresponds to the property instead of the value, i.e. there is no wild card at the end.</span></span> <span data-ttu-id="dd531-128">Por exemplo, você especificaria /department/?</span><span class="sxs-lookup"><span data-stu-id="dd531-128">For example, you would specify /department/?</span></span> <span data-ttu-id="dd531-129">para indexar os valores de departamento, mas especificaria /department como a definição de chave de partição.</span><span class="sxs-lookup"><span data-stu-id="dd531-129">to index the values under department, but specify /department as the partition key definition.</span></span> <span data-ttu-id="dd531-130">A chave de partição é indexada implicitamente e não pode ser excluída da indexação com substituições de política de indexação.</span><span class="sxs-lookup"><span data-stu-id="dd531-130">The partition key is implicitly indexed and cannot be excluded from indexing using indexing policy overrides.</span></span>
> 
> 

<span data-ttu-id="dd531-131">Vamos analisar como a opção da chave de partição afeta o desempenho do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dd531-131">Let's look at how the choice of partition key impacts the performance of your application.</span></span>

## <a name="working-with-the-azure-cosmos-db-sdks"></a><span data-ttu-id="dd531-132">Trabalhando com SDKs do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="dd531-132">Working with the Azure Cosmos DB SDKs</span></span>
<span data-ttu-id="dd531-133">O Azure Cosmos DB adicionou suporte ao particionamento automático na [API REST versão 2015-12-16](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="dd531-133">Azure Cosmos DB added support for automatic partitioning with [REST API version 2015-12-16](/rest/api/documentdb/).</span></span> <span data-ttu-id="dd531-134">Para criar contêineres particionados, você deve baixar versões do SDK 1.6.0 ou mais novas em uma das plataformas do SDK com suporte (.NET, Node.js, Java, Python, MongoDB).</span><span class="sxs-lookup"><span data-stu-id="dd531-134">In order to create partitioned containers, you must download SDK versions 1.6.0 or newer in one of the supported SDK platforms (.NET, Node.js, Java, Python, MongoDB).</span></span> 

### <a name="creating-containers"></a><span data-ttu-id="dd531-135">Criando contêineres</span><span class="sxs-lookup"><span data-stu-id="dd531-135">Creating containers</span></span>
<span data-ttu-id="dd531-136">O exemplo a seguir mostra um trecho do .NET para criação de um contêiner para armazenar dados telemétricos do dispositivo de 20.000 unidades de solicitação por segundo de produtividade.</span><span class="sxs-lookup"><span data-stu-id="dd531-136">The following sample shows a .NET snippet to create a container to store device telemetry data of 20,000 request units per second of throughput.</span></span> <span data-ttu-id="dd531-137">O SDK define o valor de OfferThroughput (que por sua vez define o cabeçalho de solicitação `x-ms-offer-throughput` na API REST).</span><span class="sxs-lookup"><span data-stu-id="dd531-137">The SDK sets the OfferThroughput value (which in turn sets the `x-ms-offer-throughput` request header in the REST API).</span></span> <span data-ttu-id="dd531-138">Aqui, definimos `/deviceId` como a chave de partição.</span><span class="sxs-lookup"><span data-stu-id="dd531-138">Here we set the `/deviceId` as the partition key.</span></span> <span data-ttu-id="dd531-139">A opção de chave de partição é salva com o restante dos metadados do contêiner, como nome e política de indexação.</span><span class="sxs-lookup"><span data-stu-id="dd531-139">The choice of partition key is saved along with the rest of the container metadata like name and indexing policy.</span></span>

<span data-ttu-id="dd531-140">Para este exemplo, escolhemos `deviceId` , pois sabemos que (a) uma vez que há um grande número de dispositivos, as gravações podem ser distribuídas uniformemente nas partições e nos permite dimensionar o banco de dados para incluir grandes volumes de dados e (b) muitas solicitações como buscar a última leitura para um dispositivo limitam-se a um único deviceId e podem ser recuperadas de uma única partição.</span><span class="sxs-lookup"><span data-stu-id="dd531-140">For this sample, we picked `deviceId` since we know that (a) since there are a large number of devices, writes can be distributed across partitions evenly and allowing us to scale the database to ingest massive volumes of data and (b) many of the requests like fetching the latest reading for a device are scoped to a single deviceId and can be retrieved from a single partition.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

// Container for device telemetry. Here the property deviceId will be used as the partition key to 
// spread across partitions. Configured for 10K RU/s throughput and an indexing policy that supports 
// sorting against any number or string property.
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 20000 });
```

<span data-ttu-id="dd531-141">Esse método faz uma chamada à API REST ao Cosmos DB e o serviço provisionará várias partições com base na produtividade solicitada.</span><span class="sxs-lookup"><span data-stu-id="dd531-141">This method makes a REST API call to Cosmos DB, and the service will provision a number of partitions based on the requested throughput.</span></span> <span data-ttu-id="dd531-142">Você pode alterar a produtividade de um contêiner conforme suas necessidades de desempenho mudarem.</span><span class="sxs-lookup"><span data-stu-id="dd531-142">You can change the throughput of a container as your performance needs evolve.</span></span> 

### <a name="reading-and-writing-items"></a><span data-ttu-id="dd531-143">Lendo e gravando itens</span><span class="sxs-lookup"><span data-stu-id="dd531-143">Reading and writing items</span></span>
<span data-ttu-id="dd531-144">Agora, vamos inserir dados no Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="dd531-144">Now, let's insert data into Cosmos DB.</span></span> <span data-ttu-id="dd531-145">Esta é uma classe de exemplo que contém uma leitura de dispositivo e uma chamada a CreateDocumentAsync para inserir uma nova leitura de dispositivo em um contêiner.</span><span class="sxs-lookup"><span data-stu-id="dd531-145">Here's a sample class containing a device reading, and a call to CreateDocumentAsync to insert a new device reading into a container.</span></span> <span data-ttu-id="dd531-146">Este é um exemplo que utiliza a API do DocumentDB:</span><span class="sxs-lookup"><span data-stu-id="dd531-146">This is an example leveraging the DocumentDB API:</span></span>

```csharp
public class DeviceReading
{
    [JsonProperty("id")]
    public string Id;

    [JsonProperty("deviceId")]
    public string DeviceId;

    [JsonConverter(typeof(IsoDateTimeConverter))]
    [JsonProperty("readingTime")]
    public DateTime ReadingTime;

    [JsonProperty("metricType")]
    public string MetricType;

    [JsonProperty("unit")]
    public string Unit;

    [JsonProperty("metricValue")]
    public double MetricValue;
  }

// Create a document. Here the partition key is extracted as "XMS-0001" based on the collection definition
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "coll"),
    new DeviceReading
    {
        Id = "XMS-001-FE24C",
        DeviceId = "XMS-0001",
        MetricType = "Temperature",
        MetricValue = 105.00,
        Unit = "Fahrenheit",
        ReadingTime = DateTime.UtcNow
    });
```

<span data-ttu-id="dd531-147">Vamos ler o item pela chave da partição e ID, atualizá-lo e, então, como uma etapa final, excluí-lo pela chave de partição e ID. Observe que as leituras incluem um valor de PartitionKey (correspondente ao cabeçalho de solicitação `x-ms-documentdb-partitionkey` na API REST).</span><span class="sxs-lookup"><span data-stu-id="dd531-147">Let's read the item by its partition key and id, update it, and then as a final step, delete it by partition key and id. Note that the reads include a PartitionKey value (corresponding to the `x-ms-documentdb-partitionkey` request header in the REST API).</span></span>

```csharp
// Read document. Needs the partition key and the ID to be specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;

// Update the document. Partition key is not required, again extracted from the document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);

// Delete document. Needs partition key
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="querying-partitioned-containers"></a><span data-ttu-id="dd531-148">Consultando contêineres particionados</span><span class="sxs-lookup"><span data-stu-id="dd531-148">Querying partitioned containers</span></span>
<span data-ttu-id="dd531-149">Quando você consulta dados em contêineres particionados, o Azure Cosmos DB encaminha automaticamente a consulta para as partições que correspondem aos valores de chave de partição especificados no filtro (se houver).</span><span class="sxs-lookup"><span data-stu-id="dd531-149">When you query data in partitioned containers, Cosmos DB automatically routes the query to the partitions corresponding to the partition key values specified in the filter (if there are any).</span></span> <span data-ttu-id="dd531-150">Por exemplo, esta consulta é roteada para apenas a partição que contém a chave de partição "XMS-0001".</span><span class="sxs-lookup"><span data-stu-id="dd531-150">For example, this query is routed to just the partition containing the partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="dd531-151">A consulta a seguir não tem um filtro na chave de partição (DeviceId) e é distribuída para todas as partições em que ela é executada no índice da partição.</span><span class="sxs-lookup"><span data-stu-id="dd531-151">The following query does not have a filter on the partition key (DeviceId) and is fanned out to all partitions where it is executed against the partition's index.</span></span> <span data-ttu-id="dd531-152">Observe que você precisa especificar o EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` na API REST) para fazer com que o SDK execute uma consulta em partições.</span><span class="sxs-lookup"><span data-stu-id="dd531-152">Note that you have to specify the EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in the REST API) to have the SDK to execute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

<span data-ttu-id="dd531-153">O Cosmos DB dá suporte a [funções de agregação](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` e `AVG` em contêineres particionados usando SQL, a partir dos SDKs 1.12.0 e posterior.</span><span class="sxs-lookup"><span data-stu-id="dd531-153">Cosmos DB supports [aggregate functions](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` and `AVG` over partitioned containers using SQL starting with SDKs 1.12.0 and above.</span></span> <span data-ttu-id="dd531-154">As consultas devem incluir um único operador de agregação e um único valor na projeção.</span><span class="sxs-lookup"><span data-stu-id="dd531-154">Queries must include a single aggregate operator, and must include a single value in the projection.</span></span>

### <a name="parallel-query-execution"></a><span data-ttu-id="dd531-155">Execução de consulta paralela</span><span class="sxs-lookup"><span data-stu-id="dd531-155">Parallel query execution</span></span>
<span data-ttu-id="dd531-156">Os SDKs 1.9.0 e posterior do Cosmos DB dão suporte a opções de execução de consulta paralela, que permitem realizar consultas de baixa latência em coleções particionadas, mesmo quando elas precisam acessar um grande número de partições.</span><span class="sxs-lookup"><span data-stu-id="dd531-156">The Cosmos DB SDKs 1.9.0 and above support parallel query execution options, which allow you to perform low latency queries against partitioned collections, even when they need to touch a large number of partitions.</span></span> <span data-ttu-id="dd531-157">Por exemplo, a consulta a seguir é configurada para ser executada paralelamente entre partições.</span><span class="sxs-lookup"><span data-stu-id="dd531-157">For example, the following query is configured to run in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="dd531-158">Você pode gerenciar a execução de consulta paralela ajustando os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="dd531-158">You can manage parallel query execution by tuning the following parameters:</span></span>

* <span data-ttu-id="dd531-159">Ao definir `MaxDegreeOfParallelism`, é possível controlar o grau de paralelismo, ou seja, o número máximo de conexões de rede simultâneas às partições do contêiner.</span><span class="sxs-lookup"><span data-stu-id="dd531-159">By setting `MaxDegreeOfParallelism`, you can control the degree of parallelism i.e., the maximum number of simultaneous network connections to the container's partitions.</span></span> <span data-ttu-id="dd531-160">Se você definir esse valor como -1, o grau de paralelismo será gerenciado pelo SDK.</span><span class="sxs-lookup"><span data-stu-id="dd531-160">If you set this to -1, the degree of parallelism is managed by the SDK.</span></span> <span data-ttu-id="dd531-161">Se o `MaxDegreeOfParallelism` não for especificado nem definido como 0, que é o valor padrão, haverá uma única conexão de rede às partições do contêiner.</span><span class="sxs-lookup"><span data-stu-id="dd531-161">If the `MaxDegreeOfParallelism` is not specified or set to 0, which is the default value, there will be a single network connection to the container's partitions.</span></span>
* <span data-ttu-id="dd531-162">Definindo `MaxBufferedItemCount`, você pode compensar a latência da consulta e a utilização da memória no lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="dd531-162">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="dd531-163">Se você omitir esse parâmetro ou defini-lo como -1, o número de itens armazenados em buffer durante a execução da consulta paralela será gerenciado pelo SDK.</span><span class="sxs-lookup"><span data-stu-id="dd531-163">If you omit this parameter or set this to -1, the number of items buffered during parallel query execution is managed by the SDK.</span></span>

<span data-ttu-id="dd531-164">Dado o mesmo estado da coleção, uma consulta paralela retornará resultados na mesma ordem da execução serial.</span><span class="sxs-lookup"><span data-stu-id="dd531-164">Given the same state of the collection, a parallel query will return results in the same order as in serial execution.</span></span> <span data-ttu-id="dd531-165">Ao executar uma consulta entre partições que inclui classificação (ORDER BY e/ou TOP), o SDK do Azure Cosmos DB emite a consulta paralelamente entre partições e mescla os resultados parcialmente classificados no lado do cliente para produzir resultados ordenados globalmente.</span><span class="sxs-lookup"><span data-stu-id="dd531-165">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), the Azure Cosmos DB SDK issues the query in parallel across partitions and merges partially sorted results in the client side to produce globally ordered results.</span></span>

### <a name="executing-stored-procedures"></a><span data-ttu-id="dd531-166">Executando procedimentos armazenados</span><span class="sxs-lookup"><span data-stu-id="dd531-166">Executing stored procedures</span></span>
<span data-ttu-id="dd531-167">Você também poderá executar transações atômicas em documentos com a mesma ID de dispositivo, por exemplo, se estiver mantendo agregações ou o último estado de um dispositivo em um único item.</span><span class="sxs-lookup"><span data-stu-id="dd531-167">You can also execute atomic transactions against documents with the same device ID, e.g. if you're maintaining aggregates or the latest state of a device in a single item.</span></span> 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
   
<span data-ttu-id="dd531-168">Na próxima seção, examinaremos como é possível passar de contêineres de partição única para contêineres particionados.</span><span class="sxs-lookup"><span data-stu-id="dd531-168">In the next section, we look at how you can move to partitioned containers from single-partition containers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd531-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dd531-169">Next steps</span></span>
<span data-ttu-id="dd531-170">Neste artigo, apresentamos uma visão geral de como trabalhar com o particionamento de contêineres do Azure Cosmos DB com a API do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="dd531-170">In this article, we provided an overview of how to work with partitioning of Azure Cosmos DB containers with the DocumentDB API.</span></span> <span data-ttu-id="dd531-171">Consulte também [particionamento e escala horizontal](../cosmos-db/partition-data.md) para obter uma visão geral dos conceitos e das melhores práticas de particionamento com uma API do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="dd531-171">Also see [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

* <span data-ttu-id="dd531-172">Executar testes de desempenho e escala com o BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd531-172">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="dd531-173">Consulte [Teste de desempenho e escala com o BD Cosmos do Azure](performance-testing.md) para obter um exemplo.</span><span class="sxs-lookup"><span data-stu-id="dd531-173">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="dd531-174">Introdução à codificação com os [SDKs](documentdb-sdk-dotnet.md) ou a [API REST](/rest/api/documentdb/)</span><span class="sxs-lookup"><span data-stu-id="dd531-174">Get started coding with the [SDKs](documentdb-sdk-dotnet.md) or the [REST API](/rest/api/documentdb/)</span></span>
* <span data-ttu-id="dd531-175">Saiba mais sobre a [produtividade provisionada no DB Cosmos do Azure](request-units.md)</span><span class="sxs-lookup"><span data-stu-id="dd531-175">Learn about [provisioned throughput in Azure Cosmos DB](request-units.md)</span></span>

