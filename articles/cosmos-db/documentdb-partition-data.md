---
title: aaaPartitioning e escala no banco de dados do Azure Cosmos | Microsoft Docs
description: "Saiba mais sobre como particionamento funciona no banco de dados do Azure Cosmos, como particionamento tooconfigure e chaves de partição e como toopick Olá direito chave da partição para seu aplicativo."
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
ms.openlocfilehash: 30621d2ba0b89efb72005680d5f3a73998347514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="partitioning-in-azure-cosmos-db-using-hello-documentdb-api"></a><span data-ttu-id="4f085-103">Particionamento no banco de dados do Cosmos do Azure usando Olá API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="4f085-103">Partitioning in Azure Cosmos DB using hello DocumentDB API</span></span>

<span data-ttu-id="4f085-104">[Banco de dados do Microsoft Azure Cosmos](../cosmos-db/introduction.md) é toohelp de serviço criado um banco de dados distribuído, vários modelos global você alcançar desempenho rápido e previsível e escalabilidade perfeitamente junto com seu aplicativo à medida que cresce.</span><span class="sxs-lookup"><span data-stu-id="4f085-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) is a global distributed, multi-model database service designed toohelp you achieve fast, predictable performance and scale seamlessly along with your application as it grows.</span></span> 

<span data-ttu-id="4f085-105">Este artigo fornece uma visão geral de como toowork com o particionamento de banco de dados do Cosmos contêineres com hello API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="4f085-105">This article provides an overview of how toowork with partitioning of Cosmos DB containers with hello DocumentDB API.</span></span> <span data-ttu-id="4f085-106">Consulte [particionamento e escala horizontal](../cosmos-db/partition-data.md) para obter uma visão geral dos conceitos e das melhores práticas de particionamento com uma API do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4f085-106">See [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

<span data-ttu-id="4f085-107">tooget iniciada com o código, baixe o projeto de saudação do [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="4f085-107">tooget started with code, download hello project from [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<span data-ttu-id="4f085-108">Depois de ler este artigo, você será capaz de tooanswer Olá perguntas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4f085-108">After reading this article, you will be able tooanswer hello following questions:</span></span>   

* <span data-ttu-id="4f085-109">Como funciona o particionamento no Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="4f085-109">How does partitioning work in Azure Cosmos DB?</span></span>
* <span data-ttu-id="4f085-110">Como fazer para configurar o particionamento no Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="4f085-110">How do I configure partitioning in Azure Cosmos DB</span></span>
* <span data-ttu-id="4f085-111">Quais são as chaves de partição, e como escolher a chave de partição correta de saudação para meu aplicativo?</span><span class="sxs-lookup"><span data-stu-id="4f085-111">What are partition keys, and how do I pick hello right partition key for my application?</span></span>

<span data-ttu-id="4f085-112">tooget iniciada com o código, baixe o projeto de saudação do [exemplo de Driver de teste do Azure Cosmos DB desempenho](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="4f085-112">tooget started with code, download hello project from [Azure Cosmos DB Performance Testing Driver Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<!-- placeholder until we have a permanent solution-->
<a name="partition-keys"></a>
<a name="single-partition-and-partitioned-collections"></a>
<a name="migrating-from-single-partition"></a>

## <a name="partition-keys"></a><span data-ttu-id="4f085-113">Chaves de partição</span><span class="sxs-lookup"><span data-stu-id="4f085-113">Partition keys</span></span>

<span data-ttu-id="4f085-114">Olá API DocumentDB, você especifica a definição de chave de partição Olá na forma de saudação de um caminho JSON.</span><span class="sxs-lookup"><span data-stu-id="4f085-114">In hello DocumentDB API, you specify hello partition key definition in hello form of a JSON path.</span></span> <span data-ttu-id="4f085-115">Olá tabela a seguir mostra exemplos de definições de chave de partição e valores hello correspondente tooeach.</span><span class="sxs-lookup"><span data-stu-id="4f085-115">hello following table shows examples of partition key definitions and hello values corresponding tooeach.</span></span> <span data-ttu-id="4f085-116">chave de partição Olá é especificado como um caminho, por exemplo, `/department` representa Olá departamento de propriedade.</span><span class="sxs-lookup"><span data-stu-id="4f085-116">hello partition key is specified as a path, e.g. `/department` represents hello property department.</span></span> 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="4f085-117"><strong>Chave de partição</strong></span><span class="sxs-lookup"><span data-stu-id="4f085-117"><strong>Partition Key</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4f085-118"><strong>Descrição</strong></span><span class="sxs-lookup"><span data-stu-id="4f085-118"><strong>Description</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="4f085-119">/department</span><span class="sxs-lookup"><span data-stu-id="4f085-119">/department</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4f085-120">Corresponde o valor toohello doc.department onde o documento é o item de saudação.</span><span class="sxs-lookup"><span data-stu-id="4f085-120">Corresponds toohello value of doc.department where doc is hello item.</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="4f085-121">/properties/name</span><span class="sxs-lookup"><span data-stu-id="4f085-121">/properties/name</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4f085-122">Corresponde o valor de toohello de doc.properties.name onde o documento é o item de saudação (propriedade aninhada).</span><span class="sxs-lookup"><span data-stu-id="4f085-122">Corresponds toohello value of doc.properties.name where doc is hello item (nested property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="4f085-123">/id</span><span class="sxs-lookup"><span data-stu-id="4f085-123">/id</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4f085-124">Corresponde o valor de toohello de doc.id (chave de id e a partição são Olá mesmo propriedade).</span><span class="sxs-lookup"><span data-stu-id="4f085-124">Corresponds toohello value of doc.id (id and partition key are hello same property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="4f085-125">/"nome do departamento"</span><span class="sxs-lookup"><span data-stu-id="4f085-125">/"department name"</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="4f085-126">Corresponde o valor toohello doc ["nome do departamento"] onde o documento é o item de saudação.</span><span class="sxs-lookup"><span data-stu-id="4f085-126">Corresponds toohello value of doc["department name"] where doc is hello item.</span></span></p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> <span data-ttu-id="4f085-127">sintaxe Olá para chave de partição é especificação de caminho toohello semelhante para caminhos de política de indexação com diferença chave Olá Olá caminho corresponde a propriedade toohello em vez do valor de hello, ou seja, não há nenhum caractere curinga no final da saudação.</span><span class="sxs-lookup"><span data-stu-id="4f085-127">hello syntax for partition key is similar toohello path specification for indexing policy paths with hello key difference that hello path corresponds toohello property instead of hello value, i.e. there is no wild card at hello end.</span></span> <span data-ttu-id="4f085-128">Por exemplo, você especificaria /department/?</span><span class="sxs-lookup"><span data-stu-id="4f085-128">For example, you would specify /department/?</span></span> <span data-ttu-id="4f085-129">Olá tooindex valores em departamento, mas Especifica /department como definição de chave de partição de saudação.</span><span class="sxs-lookup"><span data-stu-id="4f085-129">tooindex hello values under department, but specify /department as hello partition key definition.</span></span> <span data-ttu-id="4f085-130">chave de partição Olá implicitamente é indexada e não pode ser excluído da indexação usando substituições de política de indexação.</span><span class="sxs-lookup"><span data-stu-id="4f085-130">hello partition key is implicitly indexed and cannot be excluded from indexing using indexing policy overrides.</span></span>
> 
> 

<span data-ttu-id="4f085-131">Vamos examinar como opção de saudação de chave de partição afeta o desempenho de saudação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4f085-131">Let's look at how hello choice of partition key impacts hello performance of your application.</span></span>

## <a name="working-with-hello-azure-cosmos-db-sdks"></a><span data-ttu-id="4f085-132">Trabalhando com hello SDKs do banco de dados do Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="4f085-132">Working with hello Azure Cosmos DB SDKs</span></span>
<span data-ttu-id="4f085-133">O Azure Cosmos DB adicionou suporte ao particionamento automático na [API REST versão 2015-12-16](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="4f085-133">Azure Cosmos DB added support for automatic partitioning with [REST API version 2015-12-16](/rest/api/documentdb/).</span></span> <span data-ttu-id="4f085-134">Em contêineres de toocreate particionado de ordem, você deve baixar versões do SDK 1.6.0 ou suporte mais recente, em uma saudação plataformas SDK (.NET, Node.js, Java, Python, MongoDB).</span><span class="sxs-lookup"><span data-stu-id="4f085-134">In order toocreate partitioned containers, you must download SDK versions 1.6.0 or newer in one of hello supported SDK platforms (.NET, Node.js, Java, Python, MongoDB).</span></span> 

### <a name="creating-containers"></a><span data-ttu-id="4f085-135">Criando contêineres</span><span class="sxs-lookup"><span data-stu-id="4f085-135">Creating containers</span></span>
<span data-ttu-id="4f085-136">Olá exemplo a seguir mostra um toocreate de trecho de código .NET dados de telemetria de dispositivo um contêiner toostore 20.000 de unidades de solicitação por segundo de taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="4f085-136">hello following sample shows a .NET snippet toocreate a container toostore device telemetry data of 20,000 request units per second of throughput.</span></span> <span data-ttu-id="4f085-137">Olá SDK define o valor de OfferThroughput de saudação (que por sua vez define Olá `x-ms-offer-throughput` cabeçalho de solicitação na Olá REST API).</span><span class="sxs-lookup"><span data-stu-id="4f085-137">hello SDK sets hello OfferThroughput value (which in turn sets hello `x-ms-offer-throughput` request header in hello REST API).</span></span> <span data-ttu-id="4f085-138">Aqui vamos definir Olá `/deviceId` como chave de partição hello.</span><span class="sxs-lookup"><span data-stu-id="4f085-138">Here we set hello `/deviceId` as hello partition key.</span></span> <span data-ttu-id="4f085-139">opção de saudação de chave de partição é salvo junto com o restante Olá Olá metadados do contêiner como o nome e a política de indexação.</span><span class="sxs-lookup"><span data-stu-id="4f085-139">hello choice of partition key is saved along with hello rest of hello container metadata like name and indexing policy.</span></span>

<span data-ttu-id="4f085-140">Para este exemplo, escolhemos `deviceId` como sabemos que (a) uma vez que há um grande número de dispositivos, gravações podem ser distribuídas uniformemente em partições e possibilitando tooscale Olá banco de dados tooingest grandes volumes de dados e (b) muitas solicitações hello como busca de leitura mais recente Olá para um dispositivo são deviceId único tooa no escopo e podem ser recuperados de uma única partição.</span><span class="sxs-lookup"><span data-stu-id="4f085-140">For this sample, we picked `deviceId` since we know that (a) since there are a large number of devices, writes can be distributed across partitions evenly and allowing us tooscale hello database tooingest massive volumes of data and (b) many of hello requests like fetching hello latest reading for a device are scoped tooa single deviceId and can be retrieved from a single partition.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

// Container for device telemetry. Here hello property deviceId will be used as hello partition key too
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

<span data-ttu-id="4f085-141">Este método faz uma API REST chamar tooCosmos banco de dados e serviço Olá provisionará um número de partições com base na taxa de transferência solicitada hello.</span><span class="sxs-lookup"><span data-stu-id="4f085-141">This method makes a REST API call tooCosmos DB, and hello service will provision a number of partitions based on hello requested throughput.</span></span> <span data-ttu-id="4f085-142">Você pode alterar a taxa de transferência de saudação de um contêiner como o desempenho precisa evoluir.</span><span class="sxs-lookup"><span data-stu-id="4f085-142">You can change hello throughput of a container as your performance needs evolve.</span></span> 

### <a name="reading-and-writing-items"></a><span data-ttu-id="4f085-143">Lendo e gravando itens</span><span class="sxs-lookup"><span data-stu-id="4f085-143">Reading and writing items</span></span>
<span data-ttu-id="4f085-144">Agora, vamos inserir dados no Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4f085-144">Now, let's insert data into Cosmos DB.</span></span> <span data-ttu-id="4f085-145">Aqui está um exemplo de classe que contém uma leitura do dispositivo e tooinsert de tooCreateDocumentAsync uma chamada de um novo dispositivo de leitura de um contêiner.</span><span class="sxs-lookup"><span data-stu-id="4f085-145">Here's a sample class containing a device reading, and a call tooCreateDocumentAsync tooinsert a new device reading into a container.</span></span> <span data-ttu-id="4f085-146">Este é um exemplo utilizando Olá API DocumentDB:</span><span class="sxs-lookup"><span data-stu-id="4f085-146">This is an example leveraging hello DocumentDB API:</span></span>

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

// Create a document. Here hello partition key is extracted as "XMS-0001" based on hello collection definition
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

<span data-ttu-id="4f085-147">Vamos ler Olá item por sua chave de partição e a id, atualizá-lo e como uma etapa final, exclua-o por id e a chave de partição. Observe que as leituras de saudação incluem um valor de PartitionKey (correspondente toohello `x-ms-documentdb-partitionkey` cabeçalho de solicitação na Olá API REST).</span><span class="sxs-lookup"><span data-stu-id="4f085-147">Let's read hello item by its partition key and id, update it, and then as a final step, delete it by partition key and id. Note that hello reads include a PartitionKey value (corresponding toohello `x-ms-documentdb-partitionkey` request header in hello REST API).</span></span>

```csharp
// Read document. Needs hello partition key and hello ID toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;

// Update hello document. Partition key is not required, again extracted from hello document
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

### <a name="querying-partitioned-containers"></a><span data-ttu-id="4f085-148">Consultando contêineres particionados</span><span class="sxs-lookup"><span data-stu-id="4f085-148">Querying partitioned containers</span></span>
<span data-ttu-id="4f085-149">Quando você consulta dados em contêineres particionados, o banco de dados do Cosmos automaticamente rotas Olá partições toohello de consulta correspondente valores de chave de partição do toohello especificados no filtro de saudação (se houver).</span><span class="sxs-lookup"><span data-stu-id="4f085-149">When you query data in partitioned containers, Cosmos DB automatically routes hello query toohello partitions corresponding toohello partition key values specified in hello filter (if there are any).</span></span> <span data-ttu-id="4f085-150">Por exemplo, esta consulta é roteado toojust Olá partição contendo Olá chave de partição "XMS-0001".</span><span class="sxs-lookup"><span data-stu-id="4f085-150">For example, this query is routed toojust hello partition containing hello partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="4f085-151">Olá consulta a seguir não tem um filtro na chave de partição da saudação (DeviceId) e é leque exibindo tooall partições onde ela é executada no índice da partição Olá.</span><span class="sxs-lookup"><span data-stu-id="4f085-151">hello following query does not have a filter on hello partition key (DeviceId) and is fanned out tooall partitions where it is executed against hello partition's index.</span></span> <span data-ttu-id="4f085-152">Observe que você tem Olá toospecify EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` em Olá API REST) toohave Olá SDK tooexecute uma consulta em partições.</span><span class="sxs-lookup"><span data-stu-id="4f085-152">Note that you have toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in hello REST API) toohave hello SDK tooexecute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

<span data-ttu-id="4f085-153">O Cosmos DB dá suporte a [funções de agregação](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` e `AVG` em contêineres particionados usando SQL, a partir dos SDKs 1.12.0 e posterior.</span><span class="sxs-lookup"><span data-stu-id="4f085-153">Cosmos DB supports [aggregate functions](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` and `AVG` over partitioned containers using SQL starting with SDKs 1.12.0 and above.</span></span> <span data-ttu-id="4f085-154">Consultas devem incluir um único operador de agregação e devem incluir um valor único na projeção de saudação.</span><span class="sxs-lookup"><span data-stu-id="4f085-154">Queries must include a single aggregate operator, and must include a single value in hello projection.</span></span>

### <a name="parallel-query-execution"></a><span data-ttu-id="4f085-155">Execução de consulta paralela</span><span class="sxs-lookup"><span data-stu-id="4f085-155">Parallel query execution</span></span>
<span data-ttu-id="4f085-156">Olá Cosmos DB SDKs 1.9.0 e acima do opções de execução de consulta paralela, que permitem que você tooperform baixa latência as consultas em coleções particionadas, mesmo quando eles precisarem de tootouch um grande número de partições.</span><span class="sxs-lookup"><span data-stu-id="4f085-156">hello Cosmos DB SDKs 1.9.0 and above support parallel query execution options, which allow you tooperform low latency queries against partitioned collections, even when they need tootouch a large number of partitions.</span></span> <span data-ttu-id="4f085-157">Por exemplo, Olá consulta a seguir é toorun configurado em paralelo entre partições.</span><span class="sxs-lookup"><span data-stu-id="4f085-157">For example, hello following query is configured toorun in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="4f085-158">Você pode gerenciar a execução de consulta paralela ajustando Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="4f085-158">You can manage parallel query execution by tuning hello following parameters:</span></span>

* <span data-ttu-id="4f085-159">Definindo `MaxDegreeOfParallelism`, você pode controlar o grau de paralelismo, ou seja, Olá de número máximo de partições do contêiner de rede simultâneas conexões toohello hello.</span><span class="sxs-lookup"><span data-stu-id="4f085-159">By setting `MaxDegreeOfParallelism`, you can control hello degree of parallelism i.e., hello maximum number of simultaneous network connections toohello container's partitions.</span></span> <span data-ttu-id="4f085-160">Se você definir muito-1, o grau de paralelismo Olá é gerenciado pelo Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="4f085-160">If you set this too-1, hello degree of parallelism is managed by hello SDK.</span></span> <span data-ttu-id="4f085-161">Se hello `MaxDegreeOfParallelism` não for especificado ou definido too0, que é o valor padrão de saudação, haverá partições de uma única rede conexão toohello contêiner.</span><span class="sxs-lookup"><span data-stu-id="4f085-161">If hello `MaxDegreeOfParallelism` is not specified or set too0, which is hello default value, there will be a single network connection toohello container's partitions.</span></span>
* <span data-ttu-id="4f085-162">Definindo `MaxBufferedItemCount`, você pode compensar a latência da consulta e a utilização da memória no lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="4f085-162">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="4f085-163">Se você omite esse parâmetro ou defina muito-1, número de saudação de itens em buffer durante a execução de consulta paralela é gerenciado pelo Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="4f085-163">If you omit this parameter or set this too-1, hello number of items buffered during parallel query execution is managed by hello SDK.</span></span>

<span data-ttu-id="4f085-164">Considerando Olá mesmo estado da coleção hello, uma consulta paralela retornará resultados Olá mesma ordem como em execução em série.</span><span class="sxs-lookup"><span data-stu-id="4f085-164">Given hello same state of hello collection, a parallel query will return results in hello same order as in serial execution.</span></span> <span data-ttu-id="4f085-165">Ao executar uma consulta entre partições que inclui a classificação (ORDER BY e/ou superior), problemas de banco de dados do SDK do Azure Cosmos Olá Olá consulta em paralelo em partições e mesclagens resultados parcialmente classificados no hello cliente lado tooproduce resultados ordenados globalmente.</span><span class="sxs-lookup"><span data-stu-id="4f085-165">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), hello Azure Cosmos DB SDK issues hello query in parallel across partitions and merges partially sorted results in hello client side tooproduce globally ordered results.</span></span>

### <a name="executing-stored-procedures"></a><span data-ttu-id="4f085-166">Executando procedimentos armazenados</span><span class="sxs-lookup"><span data-stu-id="4f085-166">Executing stored procedures</span></span>
<span data-ttu-id="4f085-167">Você também pode executar transações atômicas em relação a documentos com hello a mesma ID de dispositivo, por exemplo, se você estiver mantendo agregações ou Olá estado mais recente de um dispositivo em um único item.</span><span class="sxs-lookup"><span data-stu-id="4f085-167">You can also execute atomic transactions against documents with hello same device ID, e.g. if you're maintaining aggregates or hello latest state of a device in a single item.</span></span> 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
   
<span data-ttu-id="4f085-168">Na próxima seção, Olá, vamos examinar como você pode mover toopartitioned contêineres de contêineres de partição única.</span><span class="sxs-lookup"><span data-stu-id="4f085-168">In hello next section, we look at how you can move toopartitioned containers from single-partition containers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f085-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4f085-169">Next steps</span></span>
<span data-ttu-id="4f085-170">Neste artigo, fornecemos uma visão geral de como toowork com o particionamento do banco de dados do Azure Cosmos contêineres com hello API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="4f085-170">In this article, we provided an overview of how toowork with partitioning of Azure Cosmos DB containers with hello DocumentDB API.</span></span> <span data-ttu-id="4f085-171">Consulte também [particionamento e escala horizontal](../cosmos-db/partition-data.md) para obter uma visão geral dos conceitos e das melhores práticas de particionamento com uma API do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4f085-171">Also see [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

* <span data-ttu-id="4f085-172">Executar testes de desempenho e escala com o BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="4f085-172">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="4f085-173">Consulte [Teste de desempenho e escala com o BD Cosmos do Azure](performance-testing.md) para obter um exemplo.</span><span class="sxs-lookup"><span data-stu-id="4f085-173">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="4f085-174">Introdução a codificação com hello [SDKs](documentdb-sdk-dotnet.md) ou hello [API REST](/rest/api/documentdb/)</span><span class="sxs-lookup"><span data-stu-id="4f085-174">Get started coding with hello [SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/)</span></span>
* <span data-ttu-id="4f085-175">Saiba mais sobre a [produtividade provisionada no DB Cosmos do Azure](request-units.md)</span><span class="sxs-lookup"><span data-stu-id="4f085-175">Learn about [provisioned throughput in Azure Cosmos DB](request-units.md)</span></span>

