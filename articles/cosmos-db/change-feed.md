---
title: "Trabalhando com o suporte ao feed de alterações no Azure Cosmos DB | Microsoft Docs"
description: "Use o suporte ao feed de alterações do Azure Cosmos DB para controlar as alterações nos documentos e executar o processamento baseado em eventos como gatilhos e manter os caches e sistemas de análise atualizados."
keywords: "feed de alteração"
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 2d7798db-857f-431a-b10f-3ccbc7d93b50
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: rest-api
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 160fbc98e0f3dcc7d17cbe0c7f7425811596a896
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="working-with-the-change-feed-support-in-azure-cosmos-db"></a><span data-ttu-id="848de-104">Trabalhando com o suporte ao feed de alterações no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="848de-104">Working with the change feed support in Azure Cosmos DB</span></span>
<span data-ttu-id="848de-105">O [Azure Cosmos DB](../cosmos-db/introduction.md) é um serviço de banco de dados rápido, flexível e replicado globalmente, usado para armazenar grandes volumes de dados transacionais e operacionais com latência previsível de milissegundos de dígito único para leituras e gravações.</span><span class="sxs-lookup"><span data-stu-id="848de-105">[Azure Cosmos DB](../cosmos-db/introduction.md) is a fast and flexible globally replicated database service that is used for storing high-volume transactional and operational data with predictable single-digit millisecond latency for reads and writes.</span></span> <span data-ttu-id="848de-106">Isso o torna adequado para IoT, jogos, varejo e aplicativos de log operacional.</span><span class="sxs-lookup"><span data-stu-id="848de-106">This makes it well-suited for IoT, gaming, retail, and operational logging applications.</span></span> <span data-ttu-id="848de-107">Um padrão de design comum nesses aplicativos é controlar as alterações feitas nos dados do Azure Cosmos DB e atualizar exibições materializadas, executar análise em tempo real, arquivar dados em armazenamento frio e disparar notificações em determinados eventos de acordo com essas alterações.</span><span class="sxs-lookup"><span data-stu-id="848de-107">A common design pattern in these applications is to track changes made to Azure Cosmos DB data, and update materialized views, perform real-time analytics, archive data to cold storage, and trigger notifications on certain events based on these changes.</span></span> <span data-ttu-id="848de-108">O **suporte ao feed de alterações** do Azure Cosmos DB permite que você crie soluções eficientes e escalonáveis para cada um desses padrões.</span><span class="sxs-lookup"><span data-stu-id="848de-108">The **change feed support** in Azure Cosmos DB enables you to build efficient and scalable solutions for each of these patterns.</span></span>

<span data-ttu-id="848de-109">Com suporte ao feed de alterações, o Azure Cosmos DB fornece uma lista classificada de documentos em uma coleção do Azure Cosmos DB na ordem em que eles foram modificados.</span><span class="sxs-lookup"><span data-stu-id="848de-109">With change feed support, Azure Cosmos DB provides a sorted list of documents within an Azure Cosmos DB collection in the order in which they were modified.</span></span> <span data-ttu-id="848de-110">Este feed pode ser usado para ouvir as modificações de dados dentro da coleção e executar ações como:</span><span class="sxs-lookup"><span data-stu-id="848de-110">This feed can be used to listen for modifications to data within the collection and perform actions such as:</span></span>

* <span data-ttu-id="848de-111">Disparar uma chamada a uma API quando um documento é inserido ou modificado</span><span class="sxs-lookup"><span data-stu-id="848de-111">Trigger a call to an API when a document is inserted or modified</span></span>
* <span data-ttu-id="848de-112">Executar o processamento em tempo real (fluxo) em atualizações</span><span class="sxs-lookup"><span data-stu-id="848de-112">Perform real-time (stream) processing on updates</span></span>
* <span data-ttu-id="848de-113">Sincronizar dados com um cache, o mecanismo de pesquisa ou o data warehouse</span><span class="sxs-lookup"><span data-stu-id="848de-113">Synchronize data with a cache, search engine, or data warehouse</span></span>

<span data-ttu-id="848de-114">As alterações no Azure Cosmos DB são persistentes e podem ser processadas de forma assíncrona e distribuídas entre um ou mais consumidores para processamento paralelo.</span><span class="sxs-lookup"><span data-stu-id="848de-114">Changes in Azure Cosmos DB are persisted and can be processed asynchronously, and distributed across one or more consumers for parallel processing.</span></span> <span data-ttu-id="848de-115">Vamos examinar as APIs do feed de alterações e como usá-las para criar aplicativos escalonáveis em tempo real.</span><span class="sxs-lookup"><span data-stu-id="848de-115">Let's look at the APIs for change feed and how you can use them to build scalable real-time applications.</span></span> <span data-ttu-id="848de-116">Este artigo mostra como trabalhar com o feed de alterações do Azure Cosmos DB e a API do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="848de-116">This article shows how to work with Azure Cosmos DB change feed and the DocumentDB API.</span></span> 

![Usando o feed de alterações do Azure Cosmos DB para capacitar a análise em tempo real e cenários de computação orientada a eventos](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> <span data-ttu-id="848de-118">O suporte ao feed de alterações é fornecido apenas para a API do DocumentDB neste momento. A API do Graph e a API de Tabela não têm suporte no momento.</span><span class="sxs-lookup"><span data-stu-id="848de-118">Change feed support is only provided for the DocumentDB API at this time; the Graph API and Table API are not currently supported.</span></span>

## <a name="use-cases-and-scenarios"></a><span data-ttu-id="848de-119">Cenários e casos de uso</span><span class="sxs-lookup"><span data-stu-id="848de-119">Use cases and scenarios</span></span>
<span data-ttu-id="848de-120">O feed de alterações permite o processamento eficiente de grandes conjuntos de dados com um alto volume de gravações e oferece uma alternativa à consulta de conjuntos de dados inteiros para identificar o que foi alterado.</span><span class="sxs-lookup"><span data-stu-id="848de-120">Change feed allows for efficient processing of large datasets with a high volume of writes, and offers an alternative to querying entire datasets to identify what has changed.</span></span> <span data-ttu-id="848de-121">Por exemplo, você pode executar as seguintes etapas de forma eficiente:</span><span class="sxs-lookup"><span data-stu-id="848de-121">For example, you can perform the following tasks efficiently:</span></span>

* <span data-ttu-id="848de-122">Atualize um cache, índice de pesquisa ou data warehouse com os dados armazenados no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="848de-122">Update a cache, search index, or a data warehouse with data stored in Azure Cosmos DB.</span></span>
* <span data-ttu-id="848de-123">Implementar camadas e arquivamento de dados em nível do aplicativo, ou seja, armazenar “dados quentes” no Azure Cosmos DB e arquivar “dados frios” no [Armazenamento de Blobs do Azure](../storage/common/storage-introduction.md) ou no [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="848de-123">Implement application-level data tiering and archival, that is, store "hot data" in Azure Cosmos DB, and age out "cold data" to [Azure Blob Storage](../storage/common/storage-introduction.md) or [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span></span>
* <span data-ttu-id="848de-124">Implementar a análise em lote nos dados usando o [Apache Hadoop](run-hadoop-with-hdinsight.md).</span><span class="sxs-lookup"><span data-stu-id="848de-124">Implement batch analytics on data using [Apache Hadoop](run-hadoop-with-hdinsight.md).</span></span>
* <span data-ttu-id="848de-125">Implementar [pipelines lambda no Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) com o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="848de-125">Implement [lambda pipelines on Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) with Azure Cosmos DB.</span></span> <span data-ttu-id="848de-126">O Azure Cosmos DB fornece uma solução de banco de dados escalonável que pode manipular a ingestão e a consulta, além de implementar arquiteturas lambda com baixo TCO.</span><span class="sxs-lookup"><span data-stu-id="848de-126">Azure Cosmos DB provides a scalable database solution that can handle both ingestion and query, and implement lambda architectures with low TCO.</span></span> 
* <span data-ttu-id="848de-127">Realize migrações com zero tempo de inatividade para outra conta do Azure Cosmos DB com um esquema de particionamento diferente.</span><span class="sxs-lookup"><span data-stu-id="848de-127">Perform zero down-time migrations to another Azure Cosmos DB account with a different partitioning scheme.</span></span>

<span data-ttu-id="848de-128">**Pipelines lambda com o Azure Cosmos DB para ingestão e consulta:**</span><span class="sxs-lookup"><span data-stu-id="848de-128">**Lambda Pipelines with Azure Cosmos DB for ingestion and query:**</span></span>

![Pipeline lambda baseado no Azure Cosmos DB para ingestão e consulta](./media/change-feed/lambda.png)

<span data-ttu-id="848de-130">Use o Azure Cosmos DB para receber e armazenar dados de evento de dispositivos, sensores, infraestrutura e aplicativos, além de processar esses eventos em tempo real com o [Stream Analytics do Azure](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md) ou [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="848de-130">You can use Azure Cosmos DB to receive and store event data from devices, sensors, infrastructure, and applications, and process these events in real-time with [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), or [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span></span> 

<span data-ttu-id="848de-131">Em aplicativos Web e móveis [sem servidor](http://azure.com/serverless), você pode acompanhar eventos como alterações no perfil, nas preferências ou no local do cliente para disparar determinadas ações, como enviar notificações por push para seus dispositivos usando o [Azure Functions](../azure-functions/functions-bindings-documentdb.md) ou os [Serviços de Aplicativos](https://azure.microsoft.com/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="848de-131">Within your [serverless](http://azure.com/serverless) web and mobile apps, you can track events such as changes to your customer's profile, preferences, or location to trigger certain actions like sending push notifications to their devices using [Azure Functions](../azure-functions/functions-bindings-documentdb.md) or [App Services](https://azure.microsoft.com/services/app-service/).</span></span> <span data-ttu-id="848de-132">Se você estiver usando o Azure Cosmos DB para criar um jogo, poderá, por exemplo, usar o feed de alterações para implementar placares em tempo real de acordo com as pontuações dos jogos concluídos.</span><span class="sxs-lookup"><span data-stu-id="848de-132">If you're using Azure Cosmos DB to build a game, you can, for example, use change feed to implement real-time leaderboards based on scores from completed games.</span></span>

## <a name="how-change-feed-works-in-azure-cosmos-db"></a><span data-ttu-id="848de-133">Como funciona o feed de alterações no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="848de-133">How change feed works in Azure Cosmos DB</span></span>
<span data-ttu-id="848de-134">O Azure Cosmos DB fornece a capacidade de ler de forma incremental as atualizações feitas em uma coleção do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="848de-134">Azure Cosmos DB provides the ability to incrementally read updates made to an Azure Cosmos DB collection.</span></span> <span data-ttu-id="848de-135">Este feed de alteração tem as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="848de-135">This change feed has the following properties:</span></span>

* <span data-ttu-id="848de-136">As alterações são persistentes no Azure Cosmos DB e podem ser processadas de forma assíncrona.</span><span class="sxs-lookup"><span data-stu-id="848de-136">Changes are persistent in Azure Cosmos DB and can be processed asynchronously.</span></span>
* <span data-ttu-id="848de-137">As alterações em documentos em uma coleção ficam imediatamente disponíveis no feed de alteração.</span><span class="sxs-lookup"><span data-stu-id="848de-137">Changes to documents within a collection are available immediately in the change feed.</span></span>
* <span data-ttu-id="848de-138">Cada alteração em um documento aparece exatamente uma vez no feed de alterações, e os clientes gerenciam a respectiva lógica do ponto de verificação.</span><span class="sxs-lookup"><span data-stu-id="848de-138">Each change to a document appears exactly once in the change feed, and clients manage their checkpointing logic.</span></span> <span data-ttu-id="848de-139">A biblioteca do processador do feed de alterações fornece ponto de verificação automático e semântica "pelo menos uma vez".</span><span class="sxs-lookup"><span data-stu-id="848de-139">The change feed processor library provides automatic checkpointing and "at least once" semantics.</span></span>
* <span data-ttu-id="848de-140">Somente a alteração mais recente de um determinado documento é incluída no log de alterações.</span><span class="sxs-lookup"><span data-stu-id="848de-140">Only the most recent change for a given document is included in the change log.</span></span> <span data-ttu-id="848de-141">As alterações intermediárias podem não estar disponíveis.</span><span class="sxs-lookup"><span data-stu-id="848de-141">Intermediate changes may not be available.</span></span>
* <span data-ttu-id="848de-142">O feed de alteração é classificado por ordem de modificação em cada valor de chave de partição.</span><span class="sxs-lookup"><span data-stu-id="848de-142">The change feed is sorted by order of modification within each partition key value.</span></span> <span data-ttu-id="848de-143">Não há nenhuma garantia de ordem entre os valores de chave de partição.</span><span class="sxs-lookup"><span data-stu-id="848de-143">There is no guaranteed order across partition-key values.</span></span>
* <span data-ttu-id="848de-144">As alterações podem ser sincronizadas de qualquer ponto no tempo, ou seja, não há nenhum período de retenção de dados fixo para o qual haja alterações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="848de-144">Changes can be synchronized from any point-in-time, that is, there is no fixed data retention period for which changes are available.</span></span>
* <span data-ttu-id="848de-145">As alterações estão disponíveis em blocos de intervalos de chaves de partição.</span><span class="sxs-lookup"><span data-stu-id="848de-145">Changes are available in chunks of partition key ranges.</span></span> <span data-ttu-id="848de-146">Esse recurso permite que as alterações de coleções grandes sejam processadas em paralelo por vários consumidores/servidores.</span><span class="sxs-lookup"><span data-stu-id="848de-146">This capability allows changes from large collections to be processed in parallel by multiple consumers/servers.</span></span>
* <span data-ttu-id="848de-147">Os aplicativos podem solicitar vários feeds de alteração simultaneamente na mesma coleção.</span><span class="sxs-lookup"><span data-stu-id="848de-147">Applications can request for multiple change feeds simultaneously on the same collection.</span></span>

<span data-ttu-id="848de-148">O feed de alterações do Azure Cosmos DB é habilitado por padrão para todas as contas.</span><span class="sxs-lookup"><span data-stu-id="848de-148">Azure Cosmos DB's change feed is enabled by default for all accounts.</span></span> <span data-ttu-id="848de-149">Use a [produtividade provisionada](request-units.md) em sua região de gravação ou em qualquer [região de leitura](distribute-data-globally.md) para ler o feed de alterações, assim como qualquer outra operação do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="848de-149">You can use your [provisioned throughput](request-units.md) in your write region or any [read region](distribute-data-globally.md) to read from the change feed, just like any other operation from Azure Cosmos DB.</span></span> <span data-ttu-id="848de-150">O feed de alteração inclui inserções e as operações de atualização feitas em documentos na coleção.</span><span class="sxs-lookup"><span data-stu-id="848de-150">The change feed includes inserts and update operations made to documents within the collection.</span></span> <span data-ttu-id="848de-151">Você pode capturar exclusões ao definir um sinalizador de "exclusão reversível" em seus documentos em vez de exclusões.</span><span class="sxs-lookup"><span data-stu-id="848de-151">You can capture deletes by setting a "soft-delete" flag within your documents in place of deletes.</span></span> <span data-ttu-id="848de-152">Como alternativa, você pode definir um período de validade finito para seus documentos por meio do [recurso TTL](time-to-live.md), por exemplo, de 24 horas, e usar o valor dessa propriedade para capturar as exclusões.</span><span class="sxs-lookup"><span data-stu-id="848de-152">Alternatively, you can set a finite expiration period for your documents via the [TTL capability](time-to-live.md), for example, 24 hours and use the value of that property to capture deletes.</span></span> <span data-ttu-id="848de-153">Com essa solução, você precisa processar alterações em um intervalo de tempo menor do que o período de expiração do TTL.</span><span class="sxs-lookup"><span data-stu-id="848de-153">With this solution, you have to process changes within a shorter time interval than the TTL expiration period.</span></span> <span data-ttu-id="848de-154">O feed de alteração está disponível para cada intervalo de chaves de partição dentro da coleção de documentos e, portanto, pode ser distribuído entre um ou mais consumidores para processamento paralelo.</span><span class="sxs-lookup"><span data-stu-id="848de-154">The change feed is available for each partition key range within the document collection, and thus can be distributed across one or more consumers for parallel processing.</span></span> 

![Processamento distribuído do feed de alterações do Azure Cosmos DB](./media/change-feed/changefeedvisual.png)

<span data-ttu-id="848de-156">Você tem algumas opções para implementar um feed de alterações em seu código de cliente.</span><span class="sxs-lookup"><span data-stu-id="848de-156">You have a few options in how you implement a change feed in your client code.</span></span> <span data-ttu-id="848de-157">As seções a seguir descrevem como implementar o feed de alterações usando a API REST do Azure Cosmos DB e os SDKs do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="848de-157">The sections that immediately follow describe how to implement the change feed using the Azure Cosmos DB REST API and the DocumentDB SDKs.</span></span> <span data-ttu-id="848de-158">No entanto, para aplicativos .NET, é recomendável usar a nova [Biblioteca do processador de feed de alterações](#change-feed-processor) para processar eventos do feed de alterações, pois ela simplifica a leitura de alterações em partições e habilita vários threads trabalhando em paralelo.</span><span class="sxs-lookup"><span data-stu-id="848de-158">However, for .NET applications, we recommend using the new [Change feed processor library](#change-feed-processor) for processing events from the change feed as it simplifies reading changes across partitions and enables multiple threads working in parallel.</span></span> 

## <span data-ttu-id="848de-159"><a id="rest-apis"></a>Trabalhando com a API REST e os SDKs do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="848de-159"><a id="rest-apis"></a>Working with the REST API and DocumentDB SDKs</span></span>
<span data-ttu-id="848de-160">O Azure Cosmos DB fornece contêineres elásticos de armazenamento e produtividade chamados **coleções**.</span><span class="sxs-lookup"><span data-stu-id="848de-160">Azure Cosmos DB provides elastic containers of storage and throughput called **collections**.</span></span> <span data-ttu-id="848de-161">Os dados em coleções são logicamente agrupados usando [chaves de partição](partition-data.md) para obtenção de escalabilidade e desempenho.</span><span class="sxs-lookup"><span data-stu-id="848de-161">Data within collections is logically grouped using [partition keys](partition-data.md) for scalability and performance.</span></span> <span data-ttu-id="848de-162">O Azure Cosmos DB fornece várias APIs para acessar esses dados, incluindo pesquisa por ID (Read/Get), consulta e feeds de leitura (verificações).</span><span class="sxs-lookup"><span data-stu-id="848de-162">Azure Cosmos DB provides various APIs for accessing this data, including lookup by ID (Read/Get), query, and read-feeds (scans).</span></span> <span data-ttu-id="848de-163">O feed de alterações pode ser obtido populando dois novos cabeçalhos de solicitação na API `ReadDocumentFeed` do DocumentDB e pode ser processado em paralelo em intervalos de chaves de partição.</span><span class="sxs-lookup"><span data-stu-id="848de-163">The change feed can be obtained by populating two new request headers to the DocumentDB `ReadDocumentFeed` API, and can be processed in parallel across ranges of partition keys.</span></span>

### <a name="readdocumentfeed-api"></a><span data-ttu-id="848de-164">API do ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="848de-164">ReadDocumentFeed API</span></span>
<span data-ttu-id="848de-165">Vamos examinar o funcionamento do ReadDocumentFeed.</span><span class="sxs-lookup"><span data-stu-id="848de-165">Let's take a brief look at how ReadDocumentFeed works.</span></span> <span data-ttu-id="848de-166">O Azure Cosmos DB dá suporte à leitura de um feed de documentos em uma coleção por meio da API `ReadDocumentFeed`.</span><span class="sxs-lookup"><span data-stu-id="848de-166">Azure Cosmos DB supports reading a feed of documents within a collection via the `ReadDocumentFeed` API.</span></span> <span data-ttu-id="848de-167">Por exemplo, a solicitação a seguir retorna uma página de documentos na coleção `serverlogs`.</span><span class="sxs-lookup"><span data-stu-id="848de-167">For example, the following request returns a page of documents inside the `serverlogs` collection.</span></span> 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="848de-168">Os resultados podem ser limitados por meio do cabeçalho `x-ms-max-item-count` e as leituras podem ser retomadas reenviando a solicitação com um cabeçalho `x-ms-continuation` retornado na resposta anterior.</span><span class="sxs-lookup"><span data-stu-id="848de-168">Results can be limited by using the `x-ms-max-item-count` header, and reads can be resumed by resubmitting the request with a `x-ms-continuation` header returned in the previous response.</span></span> <span data-ttu-id="848de-169">Quando executado de um único cliente, `ReadDocumentFeed` itera resultados entre partições em série.</span><span class="sxs-lookup"><span data-stu-id="848de-169">When performed from a single client, `ReadDocumentFeed` iterates through results across partitions serially.</span></span> 

<span data-ttu-id="848de-170">**Leitura serial de feed de documento**</span><span class="sxs-lookup"><span data-stu-id="848de-170">**Serial read document feed**</span></span>

<span data-ttu-id="848de-171">Você também pode recuperar o feed de documentos usando um dos [SDKs do Azure Cosmos DB](documentdb-sdk-dotnet.md) compatíveis.</span><span class="sxs-lookup"><span data-stu-id="848de-171">You can also retrieve the feed of documents using one of the supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="848de-172">Por exemplo, o trecho a seguir mostra como usar o [método ReadDocumentFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) no .NET.</span><span class="sxs-lookup"><span data-stu-id="848de-172">For example, the following snippet shows how to use the [ReadDocumentFeedAsync method](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) in .NET.</span></span>

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a><span data-ttu-id="848de-173">Execução distribuída do ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="848de-173">Distributed execution of ReadDocumentFeed</span></span>
<span data-ttu-id="848de-174">Para coleções que contêm terabytes de dados ou mais, ou um grande volume de atualizações de ingestão, a execução serial de feed de leitura de um único computador cliente pode não ser prática.</span><span class="sxs-lookup"><span data-stu-id="848de-174">For collections that contain terabytes of data or more, or ingest a large volume of updates, serial execution of read feed from a single client machine might not be practical.</span></span> <span data-ttu-id="848de-175">Para dar suporte a esses cenários de Big Data, o Azure Cosmos DB fornece APIs para distribuir chamadas `ReadDocumentFeed` de forma transparente entre vários leitores/consumidores cliente.</span><span class="sxs-lookup"><span data-stu-id="848de-175">In order to support these big data scenarios, Azure Cosmos DB provides APIs to distribute `ReadDocumentFeed` calls transparently across multiple client readers/consumers.</span></span> 

<span data-ttu-id="848de-176">**Feed de Documento de Leitura Distribuída**</span><span class="sxs-lookup"><span data-stu-id="848de-176">**Distributed Read Document Feed**</span></span>

<span data-ttu-id="848de-177">Para fornecer o processamento escalonável das alterações incrementais, o Azure Cosmos DB dá suporte a um modelo de expansão para a API do feed de alterações de acordo com intervalos de chaves de partição.</span><span class="sxs-lookup"><span data-stu-id="848de-177">To provide scalable processing of incremental changes, Azure Cosmos DB supports a scale-out model for the change feed API based on ranges of partition keys.</span></span>

* <span data-ttu-id="848de-178">Você pode obter uma lista de intervalos de chaves de partição para uma coleção que esteja executando uma chamada `ReadPartitionKeyRanges`.</span><span class="sxs-lookup"><span data-stu-id="848de-178">You can obtain a list of partition key ranges for a collection performing a `ReadPartitionKeyRanges` call.</span></span> 
* <span data-ttu-id="848de-179">Para cada intervalo de chaves de partição, você pode realizar uma `ReadDocumentFeed` para ler documentos com chaves de partição dentro do intervalo.</span><span class="sxs-lookup"><span data-stu-id="848de-179">For each partition key range, you can perform a `ReadDocumentFeed` to read documents with partition keys within that range.</span></span>

### <a name="retrieving-partition-key-ranges-for-a-collection"></a><span data-ttu-id="848de-180">Recuperação de intervalos de chaves de partição para uma coleção</span><span class="sxs-lookup"><span data-stu-id="848de-180">Retrieving partition key ranges for a collection</span></span>
<span data-ttu-id="848de-181">Você pode recuperar os intervalos de chaves de partição solicitando o recurso `pkranges` em uma coleção.</span><span class="sxs-lookup"><span data-stu-id="848de-181">You can retrieve the partition key ranges by requesting the `pkranges` resource within a collection.</span></span> <span data-ttu-id="848de-182">Por exemplo, a solicitação a seguir recupera a lista de intervalos de chaves de partição para a coleção `serverlogs`:</span><span class="sxs-lookup"><span data-stu-id="848de-182">For example the following request retrieves the list of partition key ranges for the `serverlogs` collection:</span></span>

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

<span data-ttu-id="848de-183">Essa solicitação retorna a seguinte resposta com metadados sobre os intervalos de chaves de partição:</span><span class="sxs-lookup"><span data-stu-id="848de-183">This request returns the following response containing metadata about the partition key ranges:</span></span>

    HTTP/1.1 200 Ok
    Content-Type: application/json
    x-ms-item-count: 25
    x-ms-schemaversion: 1.1
    Date: Tue, 15 Nov 2016 07:26:51 GMT

    {
       "_rid":"qYcAAPEvJBQ=",
       "PartitionKeyRanges":[
          {
             "_rid":"qYcAAPEvJBQCAAAAAAAAUA==",
             "id":"0",
             "_etag":"\"00002800-0000-0000-0000-580ac4ea0000\"",
             "minInclusive":"",
             "maxExclusive":"05C1CFFFFFFFF8",
             "_self":"dbs\/qYcAAA==\/colls\/qYcAAPEvJBQ=\/pkranges\/qYcAAPEvJBQCAAAAAAAAUA==\/",
             "_ts":1477100776
          },
          ...
       ],
       "_count": 25
    }


<span data-ttu-id="848de-184">**Propriedades do intervalo de chaves de partição**: cada intervalo de chaves de partição inclui as propriedades de metadados da seguinte tabela:</span><span class="sxs-lookup"><span data-stu-id="848de-184">**Partition key range properties**: Each partition key range includes the metadata properties in the following table:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="848de-185">Nome do cabeçalho</span><span class="sxs-lookup"><span data-stu-id="848de-185">Header name</span></span></th>
        <th><span data-ttu-id="848de-186">Descrição</span><span class="sxs-lookup"><span data-stu-id="848de-186">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="848de-187">ID</span><span class="sxs-lookup"><span data-stu-id="848de-187">id</span></span></td>
        <td>
            <p><span data-ttu-id="848de-188">A ID para o intervalo de chaves de partição.</span><span class="sxs-lookup"><span data-stu-id="848de-188">The ID for the partition key range.</span></span> <span data-ttu-id="848de-189">É uma ID estável e exclusiva dentro de cada coleção.</span><span class="sxs-lookup"><span data-stu-id="848de-189">This is a stable and unique ID within each collection.</span></span></p>
            <p><span data-ttu-id="848de-190">Deve ser usada na seguinte chamada para ler as alterações por intervalo de chaves de partição.</span><span class="sxs-lookup"><span data-stu-id="848de-190">Must be used in the following call to read changes by partition key range.</span></span></p>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="848de-191">maxExclusive</span><span class="sxs-lookup"><span data-stu-id="848de-191">maxExclusive</span></span></td>
        <td><span data-ttu-id="848de-192">O valor de hash de chave de partição máxima para o intervalo de chaves de partição.</span><span class="sxs-lookup"><span data-stu-id="848de-192">The maximum partition key hash value for the partition key range.</span></span> <span data-ttu-id="848de-193">Para uso interno.</span><span class="sxs-lookup"><span data-stu-id="848de-193">For internal use.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="848de-194">minInclusive</span><span class="sxs-lookup"><span data-stu-id="848de-194">minInclusive</span></span></td>
        <td><span data-ttu-id="848de-195">O valor de hash da chave de partição mínimo para o intervalo de chaves de partição.</span><span class="sxs-lookup"><span data-stu-id="848de-195">The minimum partition key hash value for the partition key range.</span></span> <span data-ttu-id="848de-196">Para uso interno.</span><span class="sxs-lookup"><span data-stu-id="848de-196">For internal use.</span></span></td>
    </tr>       
</table>

<span data-ttu-id="848de-197">Faça isso usando um dos [SDKs do Azure Cosmos DB](documentdb-sdk-dotnet.md) com suporte.</span><span class="sxs-lookup"><span data-stu-id="848de-197">You can do this using one of the supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="848de-198">Por exemplo, o trecho a seguir mostra como recuperar intervalos de chaves de partição no .NET, usando o método [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="848de-198">For example, the following snippet shows how to retrieve partition key ranges in .NET using the [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) method.</span></span>

```csharp
string pkRangesResponseContinuation = null;
List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

do
{
    FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
        collectionUri, 
        new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

    partitionKeyRanges.AddRange(pkRangesResponse);
    pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
}
while (pkRangesResponseContinuation != null);
```

<span data-ttu-id="848de-199">O Azure Cosmos DB dá suporte à recuperação de documentos por intervalo de chaves de partição definindo o cabeçalho `x-ms-documentdb-partitionkeyrangeid` opcional.</span><span class="sxs-lookup"><span data-stu-id="848de-199">Azure Cosmos DB supports retrieval of documents per partition key range by setting the optional `x-ms-documentdb-partitionkeyrangeid` header.</span></span> 

### <a name="performing-an-incremental-readdocumentfeed"></a><span data-ttu-id="848de-200">Execução de um ReadDocumentFeed incremental</span><span class="sxs-lookup"><span data-stu-id="848de-200">Performing an incremental ReadDocumentFeed</span></span>
<span data-ttu-id="848de-201">O ReadDocumentFeed dá suporte aos seguintes cenários/tarefas de processamento incremental de alterações em coleções do Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="848de-201">ReadDocumentFeed supports the following scenarios/tasks for incremental processing of changes in Azure Cosmos DB collections:</span></span>

* <span data-ttu-id="848de-202">Leia todas as alterações para documentos desde o início, ou seja, desde a criação da coleção.</span><span class="sxs-lookup"><span data-stu-id="848de-202">Read all changes to documents from the beginning, that is, from collection creation.</span></span>
* <span data-ttu-id="848de-203">Leia todas as alterações para atualizações futuras nos documentos a partir da hora atual ou todas as alterações desde a hora especificada por um usuário.</span><span class="sxs-lookup"><span data-stu-id="848de-203">Read all changes to future updates to documents from current time, or any changes since a user-specified time.</span></span>
* <span data-ttu-id="848de-204">Leia todas as alterações feitas em documentos de uma versão lógica da coleção (ETag).</span><span class="sxs-lookup"><span data-stu-id="848de-204">Read all changes to documents from a logical version of the collection (ETag).</span></span> <span data-ttu-id="848de-205">É possível criar pontos de verificação de seus clientes com base em ETag retornado de solicitações de feed de leitura incrementais.</span><span class="sxs-lookup"><span data-stu-id="848de-205">You can checkpoint your consumers based on the returned ETag from incremental read-feed requests.</span></span>

<span data-ttu-id="848de-206">As alterações incluem inserções e atualizações em documentos.</span><span class="sxs-lookup"><span data-stu-id="848de-206">The changes include inserts and updates to documents.</span></span> <span data-ttu-id="848de-207">Para capturar as exclusões, você deve usar uma propriedade de "exclusão reversível" em documentos ou usar a [propriedade TTL interna](time-to-live.md) para sinalizar uma exclusão pendente no feed de alteração.</span><span class="sxs-lookup"><span data-stu-id="848de-207">To capture deletes, you must use a "soft delete" property within your documents, or use the [built-in TTL property](time-to-live.md) to signal a pending deletion in the change feed.</span></span>

<span data-ttu-id="848de-208">A tabela a seguir lista os [cabeçalhos de solicitação](/rest/api/documentdb/common-documentdb-rest-request-headers.md) e de [resposta](/rest/api/documentdb/common-documentdb-rest-response-headers.md) para operações do ReadDocumentFeed.</span><span class="sxs-lookup"><span data-stu-id="848de-208">The following table lists the [request](/rest/api/documentdb/common-documentdb-rest-request-headers.md) and [response headers](/rest/api/documentdb/common-documentdb-rest-response-headers.md) for ReadDocumentFeed operations.</span></span>

<span data-ttu-id="848de-209">**Cabeçalhos de solicitação para ReadDocumentFeed incremental**:</span><span class="sxs-lookup"><span data-stu-id="848de-209">**Request headers for incremental ReadDocumentFeed**:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="848de-210">Nome do cabeçalho</span><span class="sxs-lookup"><span data-stu-id="848de-210">Header name</span></span></th>
        <th><span data-ttu-id="848de-211">Descrição</span><span class="sxs-lookup"><span data-stu-id="848de-211">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="848de-212">A-IM</span><span class="sxs-lookup"><span data-stu-id="848de-212">A-IM</span></span></td>
        <td><span data-ttu-id="848de-213">Deve ser definido como "feed Incremental" ou omitido</span><span class="sxs-lookup"><span data-stu-id="848de-213">Must be set to "Incremental feed", or omitted otherwise</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="848de-214">If-None-Match</span><span class="sxs-lookup"><span data-stu-id="848de-214">If-None-Match</span></span></td>
        <td>
            <p><span data-ttu-id="848de-215">Nenhum cabeçalho: retorna todas as alterações desde o início (criação de coleção)</span><span class="sxs-lookup"><span data-stu-id="848de-215">No header: returns all changes from the beginning (collection creation)</span></span></p>
            <p><span data-ttu-id="848de-216">"*": retorna todas as novas alterações para dados na coleção</span><span class="sxs-lookup"><span data-stu-id="848de-216">"*": returns all new changes to data within the collection</span></span></p>           
            <p><span data-ttu-id="848de-217">&lt;etag&gt;: se definida como uma ETag de coleção, retorna todas as alterações feitas desde o carimbo de data/hora lógico</span><span class="sxs-lookup"><span data-stu-id="848de-217">&lt;etag&gt;: If set to a collection ETag, returns all changes made since that logical timestamp</span></span></p>
        </td>
    </tr>
    <tr>    
        <td><span data-ttu-id="848de-218">If-Modified-Since</span><span class="sxs-lookup"><span data-stu-id="848de-218">If-Modified-Since</span></span></td> 
        <td><span data-ttu-id="848de-219">Formato de hora RFC 1123; ignorado se If-None-Match for especificado</span><span class="sxs-lookup"><span data-stu-id="848de-219">RFC 1123 time format; ignored if If-None-Match is specified</span></span></td> 
    </tr> 
    <tr>
        <td><span data-ttu-id="848de-220">x-ms-documentdb-partitionkeyrangeid</span><span class="sxs-lookup"><span data-stu-id="848de-220">x-ms-documentdb-partitionkeyrangeid</span></span></td>
        <td><span data-ttu-id="848de-221">A ID de intervalo de chaves de partição de leitura de dados.</span><span class="sxs-lookup"><span data-stu-id="848de-221">The partition key range ID for reading data.</span></span></td>
    </tr>
</table>

<span data-ttu-id="848de-222">**Cabeçalhos de resposta para ReadDocumentFeed incremental**:</span><span class="sxs-lookup"><span data-stu-id="848de-222">**Response headers for incremental ReadDocumentFeed**:</span></span>

<table> <tr>
        <th><span data-ttu-id="848de-223">Nome do cabeçalho</span><span class="sxs-lookup"><span data-stu-id="848de-223">Header name</span></span></th>
        <th><span data-ttu-id="848de-224">Descrição</span><span class="sxs-lookup"><span data-stu-id="848de-224">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="848de-225">etag</span><span class="sxs-lookup"><span data-stu-id="848de-225">etag</span></span></td>
        <td>
            <p><span data-ttu-id="848de-226">O número de sequência lógica (LSN) do último documento retornado na resposta.</span><span class="sxs-lookup"><span data-stu-id="848de-226">The logical sequence number (LSN) of last document returned in the response.</span></span></p>
            <p><span data-ttu-id="848de-227">O ReadDocumentFeed incremental pode ser retomado por meio do reenvio desse valor em If-None-Match.</span><span class="sxs-lookup"><span data-stu-id="848de-227">Incremental ReadDocumentFeed can be resumed by resubmitting this value in If-None-Match.</span></span></p>
        </td>
    </tr>
</table>

<span data-ttu-id="848de-228">Aqui está um exemplo de solicitação para retornar todas as alterações incrementais na coleção da versão/ETag lógica `28535` e intervalo de chaves de partição = `16`:</span><span class="sxs-lookup"><span data-stu-id="848de-228">Here's a sample request to return all incremental changes in collection from the logical version/ETag `28535` and partition key range = `16`:</span></span>

    GET https://mydocumentdb.documents.azure.com/dbs/bigdb/colls/bigcoll/docs HTTP/1.1
    x-ms-max-item-count: 1
    If-None-Match: "28535"
    A-IM: Incremental feed
    x-ms-documentdb-partitionkeyrangeid: 16
    x-ms-date: Tue, 22 Nov 2016 20:43:01 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dzdpL2QQ8TCfiNbW%2fEcT88JHNvWeCgDA8gWeRZ%2btfN5o%3d
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="848de-229">As alterações são ordenadas por tempo em cada valor de chave de partição dentro do intervalo de chaves de partição.</span><span class="sxs-lookup"><span data-stu-id="848de-229">Changes are ordered by time within each partition key value within the partition key range.</span></span> <span data-ttu-id="848de-230">Não há nenhuma garantia de ordem entre os valores de chave de partição.</span><span class="sxs-lookup"><span data-stu-id="848de-230">There is no guaranteed order across partition-key values.</span></span> <span data-ttu-id="848de-231">Se houver mais resultados do que pode caber em uma única página, você poderá ler a próxima página de resultados reenviando a solicitação com o cabeçalho `If-None-Match` com valor igual a `etag` da resposta anterior.</span><span class="sxs-lookup"><span data-stu-id="848de-231">If there are more results than can fit in a single page, you can read the next page of results by resubmitting the request with the `If-None-Match` header with value equal to the `etag` from the previous response.</span></span> <span data-ttu-id="848de-232">Se vários documentos tiverem sido inseridos ou atualizados transacionalmente dentro de um procedimento armazenado ou gatilho, serão todos retornados na mesma página de resposta.</span><span class="sxs-lookup"><span data-stu-id="848de-232">If multiple documents were inserted or updated transactionally within a stored procedure or trigger, they will all be returned within the same response page.</span></span>

> [!NOTE]
> <span data-ttu-id="848de-233">Com o feed de alterações, você poderá obter mais itens retornados em uma página que o especificado em `x-ms-max-item-count`, no caso de vários documentos inseridos ou atualizados dentro de procedimentos armazenados ou gatilhos.</span><span class="sxs-lookup"><span data-stu-id="848de-233">With change feed, you might get more items returned in a page than specified in `x-ms-max-item-count` in the case of multiple documents inserted or updated inside a stored procedures or triggers.</span></span> 

<span data-ttu-id="848de-234">Ao usar o SDK do .NET (1.17.0), defina o campo `StartTime` em `ChangeFeedOptions` para retornar diretamente documentos alterados desde `StartTime` ao chamar `CreateDocumentChangeFeedQuery`.</span><span class="sxs-lookup"><span data-stu-id="848de-234">When using the .NET SDK (1.17.0), set the field `StartTime` in `ChangeFeedOptions` to directly return changed documents since `StartTime` when calling  `CreateDocumentChangeFeedQuery`.</span></span> <span data-ttu-id="848de-235">Ao especificar `If-Modified-Since` usando a API REST, sua solicitação não retornará os documentos em si, mas o token de continuação ou `etag` no cabeçalho da resposta.</span><span class="sxs-lookup"><span data-stu-id="848de-235">By specifying `If-Modified-Since` using the REST API, your request will return not the documents themselves, but rather the continuation token or `etag` in the response header.</span></span> <span data-ttu-id="848de-236">Para retornar os documentos modificados na hora especificada, o token de continuação `etag` deve ser usado na próxima solicitação com `If-None-Match` para retornar os documentos reais.</span><span class="sxs-lookup"><span data-stu-id="848de-236">To return the documents modified the specified time, the continuation token `etag` must then be used in the next request with `If-None-Match` to return the actual documents.</span></span> 

<span data-ttu-id="848de-237">O SDK do .NET fornece as classes auxiliares [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) e [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) para acessar as alterações feitas em uma coleção.</span><span class="sxs-lookup"><span data-stu-id="848de-237">The .NET SDK provides the [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) and [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) helper classes to access changes made to a collection.</span></span> <span data-ttu-id="848de-238">O trecho a seguir mostra como recuperar todas as alterações desde o início usando o SDK do .NET de um único cliente.</span><span class="sxs-lookup"><span data-stu-id="848de-238">The following snippet shows how to retrieve all changes from the beginning using the .NET SDK from a single client.</span></span>

```csharp
private async Task<Dictionary<string, string>> GetChanges(
    DocumentClient client,
    string collection,
    Dictionary<string, string> checkpoints)
{
    string pkRangesResponseContinuation = null;
    List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

    do
    {
        FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
            collectionUri, 
            new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

        partitionKeyRanges.AddRange(pkRangesResponse);
        pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
    }
    while (pkRangesResponseContinuation != null);

    foreach (PartitionKeyRange pkRange in partitionKeyRanges)
    {
        string continuation = null;
        checkpoints.TryGetValue(pkRange.Id, out continuation);

        IDocumentQuery<Document> query = client.CreateDocumentChangeFeedQuery(
            collection,
            new ChangeFeedOptions
            {
                PartitionKeyRangeId = pkRange.Id,
                StartFromBeginning = true,
                RequestContinuation = continuation,
                MaxItemCount = 1
            });

        while (query.HasMoreResults)
        {
            FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

            foreach (DeviceReading changedDocument in readChangesResponse)
            {
                Console.WriteLine(changedDocument.Id);
            }

            checkpoints[pkRange.Id] = readChangesResponse.ResponseContinuation;
        }
    }

    return checkpoints;
}
```
<span data-ttu-id="848de-239">E o trecho a seguir mostra como processar alterações em tempo real com o Azure Cosmos DB usando o suporte ao feed de alterações e a função anterior.</span><span class="sxs-lookup"><span data-stu-id="848de-239">And the following snippet shows how to process changes in real-time with Azure Cosmos DB by using the change feed support and the preceding function.</span></span> <span data-ttu-id="848de-240">A primeira chamada retorna todos os documentos na coleção, e o segundo retorna apenas os dois documentos criados desde o último ponto de verificação.</span><span class="sxs-lookup"><span data-stu-id="848de-240">The first call returns all the documents in the collection, and the second only returns the two documents created that were created since the last checkpoint.</span></span>

```csharp
// Returns all documents in the collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only the two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

<span data-ttu-id="848de-241">Você também pode filtrar o feed de alteração usando lógica de cliente para processar eventos seletivamente.</span><span class="sxs-lookup"><span data-stu-id="848de-241">You can also filter the change feed using client side logic to selectively process events.</span></span> <span data-ttu-id="848de-242">Por exemplo, aqui está um trecho que usa o LINQ no lado do cliente para processar somente os eventos de alteração de temperatura de sensores de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="848de-242">For example, here's a snippet that uses client side LINQ to process only temperature change events from device sensors.</span></span>

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <span data-ttu-id="848de-243"><a id="change-feed-processor"></a>Biblioteca do processador do feed de alterações</span><span class="sxs-lookup"><span data-stu-id="848de-243"><a id="change-feed-processor"></a>Change Feed Processor library</span></span>
<span data-ttu-id="848de-244">Outra opção é usar a [Biblioteca do processador do feed de alterações do Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), que pode ajudá-lo a distribuir facilmente o processamento de eventos de um feed de alterações entre vários consumidores.</span><span class="sxs-lookup"><span data-stu-id="848de-244">Another option is to use the [Azure Cosmos DB Change Feed Processor library](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), which can help you easily distribute event processing from a change feed across multiple consumers.</span></span> <span data-ttu-id="848de-245">A biblioteca é excelente para a criação de leitores de feed de alterações na plataforma .NET.</span><span class="sxs-lookup"><span data-stu-id="848de-245">The library is great for building change feed readers on the .NET platform.</span></span> <span data-ttu-id="848de-246">Alguns fluxos de trabalho que seriam simplificados usando a Biblioteca do processador do feed de alterações comparados com métodos incluídos em outros SDKs do Cosmos DB incluem:</span><span class="sxs-lookup"><span data-stu-id="848de-246">Some workflows that would be simplified by using the Change Feed Processor library over the methods included in the other Cosmos DB SDKs include:</span></span> 

* <span data-ttu-id="848de-247">Efetuar pull de atualizações de feed de alterações quando os dados são armazenados em várias partições</span><span class="sxs-lookup"><span data-stu-id="848de-247">Pulling updates from change feed when data is stored across multiple partitions</span></span>
* <span data-ttu-id="848de-248">Mover ou replicar dados de uma coleção para outra</span><span class="sxs-lookup"><span data-stu-id="848de-248">Moving or replicating data from one collection to another</span></span>
* <span data-ttu-id="848de-249">Execução paralela de ações disparadas por atualizações aos dados e ao feed de alterações</span><span class="sxs-lookup"><span data-stu-id="848de-249">Parallel execution of actions triggered by updates to data and change feed</span></span> 

<span data-ttu-id="848de-250">Embora o uso das APIs nos SDKs do Cosmos forneça acesso preciso às atualizações do feed de alterações em cada partição, o uso da Biblioteca do processador do feed de alterações simplifica a leitura de alterações em partições e em vários threads trabalhando em paralelo.</span><span class="sxs-lookup"><span data-stu-id="848de-250">While using the APIs in the Cosmos SDKs provides precise access to change feed updates in each partition, using the Change Feed Processor library simplifies reading changes across partitions and multiple threads working in parallel.</span></span> <span data-ttu-id="848de-251">Em vez de ler manualmente as alterações de cada contêiner e salvar um token de continuação para cada partição, o Processador do feed de alterações gerencia automaticamente a leitura de alterações em partições usando um mecanismo de concessão.</span><span class="sxs-lookup"><span data-stu-id="848de-251">Instead of manually reading changes from each container and saving a continuation token for each partition, the Change Feed Processor automatically manages reading changes across partitions using a lease mechanism.</span></span>

<span data-ttu-id="848de-252">A biblioteca está disponível como um Pacote NuGet: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) e do código-fonte como um [exemplo](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor) do Github.</span><span class="sxs-lookup"><span data-stu-id="848de-252">The library is available as a NuGet Package: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) and from source code as a Github [sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span></span> 

### <a name="understanding-change-feed-processor-library"></a><span data-ttu-id="848de-253">Noções básicas sobre a biblioteca do processador do feed de alterações</span><span class="sxs-lookup"><span data-stu-id="848de-253">Understanding Change Feed Processor library</span></span> 

<span data-ttu-id="848de-254">Há quatro componentes principais da implementação do Processador do feed de alterações: a coleção monitorada, a coleção de concessão, o host de processador e os consumidores.</span><span class="sxs-lookup"><span data-stu-id="848de-254">There are four main components of implementing the Change Feed Processor: the monitored collection, the lease collection, the processor host, and the consumers.</span></span> 

<span data-ttu-id="848de-255">**Coleção monitorada:** a coleção monitorada são os dados dos quais o feed de alterações é gerado.</span><span class="sxs-lookup"><span data-stu-id="848de-255">**Monitored Collection:** The monitored collection is the data from which the change feed is generated.</span></span> <span data-ttu-id="848de-256">Todas as inserções e alterações à coleção monitorada são refletidas no feed de alterações da coleção.</span><span class="sxs-lookup"><span data-stu-id="848de-256">Any inserts and changes to the monitored collection are reflected in the change feed of the collection.</span></span> 

<span data-ttu-id="848de-257">**Coleção de concessão:** a coleção de concessão coordena o processamento do feed de alterações em vários trabalhos.</span><span class="sxs-lookup"><span data-stu-id="848de-257">**Lease Collection:** The lease collection coordinates processing the change feed across multiple workers.</span></span> <span data-ttu-id="848de-258">Uma coleção separada é usada para armazenar as concessões com uma concessão por partição.</span><span class="sxs-lookup"><span data-stu-id="848de-258">A separate collection is used to store the leases with one lease per partition.</span></span> <span data-ttu-id="848de-259">É vantajoso armazenar essa coleção de concessão em uma conta diferente, com a região de gravação mais próxima do local em que o Processador do feed de alterações está em execução.</span><span class="sxs-lookup"><span data-stu-id="848de-259">It is advantageous to store this lease collection on a different account with the write region closer to where the Change Feed Processor is running.</span></span> <span data-ttu-id="848de-260">Um objeto de concessão contém os seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="848de-260">A lease object contains the following attributes:</span></span> 
* <span data-ttu-id="848de-261">Proprietário: especifica o host que é proprietário da concessão</span><span class="sxs-lookup"><span data-stu-id="848de-261">Owner: Specifies the host that owns the lease</span></span>
* <span data-ttu-id="848de-262">Continuação: especifica a posição (token de continuação) de uma determinada partição no feed de alterações</span><span class="sxs-lookup"><span data-stu-id="848de-262">Continuation: Specifies the position (continuation token) in the change feed for a particular partition</span></span>
* <span data-ttu-id="848de-263">Carimbo de data/hora: última vez em que a concessão foi atualizada; o carimbo de data/hora pode ser usado para verificar se a concessão está expirada</span><span class="sxs-lookup"><span data-stu-id="848de-263">Timestamp: Last time lease was updated; the timestamp can be used to check whether the lease is considered expired</span></span> 

<span data-ttu-id="848de-264">**Host de processador:** cada host determina quantas partições devem ser processadas com base no número de instâncias de hosts com concessões ativas.</span><span class="sxs-lookup"><span data-stu-id="848de-264">**Processor Host:** Each host determines how many partitions to process based on how many other instances of hosts have active leases.</span></span> 
1.  <span data-ttu-id="848de-265">Quando um host é iniciado, ele adquire concessões para balancear a carga de trabalho entre todos os hosts.</span><span class="sxs-lookup"><span data-stu-id="848de-265">When a host starts up, it acquires leases to balance the workload across all hosts.</span></span> <span data-ttu-id="848de-266">Um host renova concessões periodicamente para que as concessões permaneçam ativas.</span><span class="sxs-lookup"><span data-stu-id="848de-266">A host periodically renews leases, so leases remain active.</span></span> 
2.  <span data-ttu-id="848de-267">Um host realiza pontos de verificação do último token de continuação em relação à respectiva concessão para cada leitura.</span><span class="sxs-lookup"><span data-stu-id="848de-267">A host checkpoints the last continuation token to its lease for each read.</span></span> <span data-ttu-id="848de-268">Para garantir a segurança de simultaneidade, um host verifica o Etag de cada atualização de concessão.</span><span class="sxs-lookup"><span data-stu-id="848de-268">To ensure concurrency safety, a host checks the ETag for each lease update.</span></span> <span data-ttu-id="848de-269">Também há suporte para outras estratégias de ponto de verificação.</span><span class="sxs-lookup"><span data-stu-id="848de-269">Other checkpoint strategies are also supported.</span></span>  
3.  <span data-ttu-id="848de-270">Durante o desligamento, um host libera todas as concessões, mas mantém as informações de continuação, para que possa retomar a leitura do ponto de verificação armazenado mais tarde.</span><span class="sxs-lookup"><span data-stu-id="848de-270">Upon shutdown, a host releases all leases but keeps the continuation information, so it can resume reading from the stored checkpoint later.</span></span> 

<span data-ttu-id="848de-271">Neste momento, o número de hosts não pode ser maior que o número de partições (concessões).</span><span class="sxs-lookup"><span data-stu-id="848de-271">At this time the number of hosts cannot be greater than the number of partitions (leases).</span></span>

<span data-ttu-id="848de-272">**Consumidores:** consumidores ou trabalhos, são os threads que realizam o processamento do feed de alterações iniciado por cada host.</span><span class="sxs-lookup"><span data-stu-id="848de-272">**Consumers:** Consumers, or workers, are threads that perform the change feed processing initiated by each host.</span></span> <span data-ttu-id="848de-273">Cada host de processador pode ter vários consumidores.</span><span class="sxs-lookup"><span data-stu-id="848de-273">Each processor host can have multiple consumers.</span></span> <span data-ttu-id="848de-274">Cada consumidor lê o feed de alterações da partição à qual ele é atribuído e notifica o respectivo host sobre as alterações e as concessões expiradas.</span><span class="sxs-lookup"><span data-stu-id="848de-274">Each consumer reads the change feed from the partition it is assigned to and notifies its host of changes and expired leases.</span></span>

<span data-ttu-id="848de-275">Para compreender melhor como esses quatro elementos do Processador do feed de alterações funcionam em conjunto, vamos examinar um exemplo no diagrama a seguir.</span><span class="sxs-lookup"><span data-stu-id="848de-275">To further understand how these four elements of Change Feed Processor work together, let's look at an example in the following diagram.</span></span> <span data-ttu-id="848de-276">A coleção monitorada armazena documentos e usa a "cidade" como a chave de partição.</span><span class="sxs-lookup"><span data-stu-id="848de-276">The monitored collection stores documents and uses the "city" as the partition key.</span></span> <span data-ttu-id="848de-277">Podemos ver que a partição azul contém documentos com o campo "cidade" de "A a E" e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="848de-277">We see that the blue partition contains documents with the "city" field from "A-E" and so on.</span></span> <span data-ttu-id="848de-278">Há dois hosts, cada um com dois consumidores lendo das quatro partições em paralelo.</span><span class="sxs-lookup"><span data-stu-id="848de-278">There are two hosts, each with two consumers reading from the four partitions in parallel.</span></span> <span data-ttu-id="848de-279">As setas mostram os consumidores lendo de um ponto específico no feed de alterações.</span><span class="sxs-lookup"><span data-stu-id="848de-279">The arrows show the consumers reading from a specific spot in the change feed.</span></span> <span data-ttu-id="848de-280">Na primeira partição, o azul mais escuro representa as alterações não lidas enquanto que o azul claro representa as alterações já lidas no feed de alterações.</span><span class="sxs-lookup"><span data-stu-id="848de-280">In the first partition, the darker blue represents unread changes while the light blue represents the already read changes on the change feed.</span></span> <span data-ttu-id="848de-281">Os hosts de usam a coleção de concessão para armazenar um valor de "continuação" a fim de manter um registro da posição atual de leitura para cada consumidor.</span><span class="sxs-lookup"><span data-stu-id="848de-281">The hosts use the lease collection to store a "continuation" value to keep track of the current reading position for each consumer.</span></span> 

![Usando o host do processador do feed de alterações do Azure Cosmos DB](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a><span data-ttu-id="848de-283">Usando a Biblioteca do processador do feed de alterações</span><span class="sxs-lookup"><span data-stu-id="848de-283">Using Change Feed Processor Library</span></span> 
<span data-ttu-id="848de-284">A seção a seguir explica como usar a Biblioteca do processador do feed de alterações no contexto de replicar alterações de uma coleção de origem para uma coleção de destino.</span><span class="sxs-lookup"><span data-stu-id="848de-284">The following section explains how to use the Change Feed Processor library in the context of replicating changes from a source collection to a destination collection.</span></span> <span data-ttu-id="848de-285">Aqui, a coleção de origem é a coleção monitorada no Processador do feed de alterações.</span><span class="sxs-lookup"><span data-stu-id="848de-285">Here, the source collection is the monitored collection in Change Feed Processor.</span></span> 

<span data-ttu-id="848de-286">**Instalar e incluir o Pacote NuGet do Processador do feed de alterações**</span><span class="sxs-lookup"><span data-stu-id="848de-286">**Install and include the Change Feed Processor NuGet package**</span></span> 

<span data-ttu-id="848de-287">Antes de instalar o Pacote NuGet do Processador do feed de alterações, instale:</span><span class="sxs-lookup"><span data-stu-id="848de-287">Before installing Change Feed Processor NuGet Package, first install:</span></span> 
* <span data-ttu-id="848de-288">Microsoft.Azure.DocumentDB, versão 1.13.1 ou superior</span><span class="sxs-lookup"><span data-stu-id="848de-288">Microsoft.Azure.DocumentDB, version 1.13.1 or above</span></span> 
* <span data-ttu-id="848de-289">Newtonsoft.Json, versão 9.0.1 ou superior. Instale `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` e o inclua como uma referência.</span><span class="sxs-lookup"><span data-stu-id="848de-289">Newtonsoft.Json, version 9.0.1 or above Install `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` and include it as a reference.</span></span>

<span data-ttu-id="848de-290">**Criar uma coleção monitorada, uma coleção de destino e uma coleção de concessão**</span><span class="sxs-lookup"><span data-stu-id="848de-290">**Create a monitored, lease and destination collection**</span></span> 

<span data-ttu-id="848de-291">Para usar a Biblioteca do processador do feed de alterações, a coleção de concessão precisa ser criada antes de executar o(s) host(s) do processador.</span><span class="sxs-lookup"><span data-stu-id="848de-291">In order to use the Change Feed Processor Library, the lease collection needs to be created before running the processor host(s).</span></span> <span data-ttu-id="848de-292">Novamente, é recomendável armazenar uma coleção de concessão em uma conta diferente, com a região de gravação mais próxima do local em que o Processador do feed de alterações está em execução.</span><span class="sxs-lookup"><span data-stu-id="848de-292">Again, we recommend storing a lease collection on a different account with a write region closer to where the Change Feed Processor is running.</span></span> <span data-ttu-id="848de-293">Neste exemplo de movimentação de dados, precisamos criar a coleção de destino antes de executar o host do Processador do feed de alterações.</span><span class="sxs-lookup"><span data-stu-id="848de-293">In this data movement example, we need to create the destination collection before running the Change Feed Processor host.</span></span> <span data-ttu-id="848de-294">No código de exemplo, chamamos um método auxiliar para criar a coleção monitorada, a coleção de concessão e a de destino, caso ainda não existam.</span><span class="sxs-lookup"><span data-stu-id="848de-294">In the sample code we call a helper method to create the monitored, leased, and destination collections if they do not already exist.</span></span> 

> [!WARNING]
> <span data-ttu-id="848de-295">Criar uma coleção tem implicações de preços, pois você está reservando a taxa de transferência para o aplicativo se comunicar com o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="848de-295">Creating a collection has pricing implications, as you are reserving throughput for the application to communicate with Azure Cosmos DB.</span></span> <span data-ttu-id="848de-296">Para obter mais detalhes, visite a [página de preços](https://azure.microsoft.com/pricing/details/cosmos-db/)</span><span class="sxs-lookup"><span data-stu-id="848de-296">For more details, please visit the [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

<span data-ttu-id="848de-297">*Criando um host de processador*</span><span class="sxs-lookup"><span data-stu-id="848de-297">*Creating a processor host*</span></span>

<span data-ttu-id="848de-298">A classe `ChangeFeedProcessorHost` fornece um ambiente de tempo de execução seguro, thread-safe e de vários processos para implementações do processador de eventos, que também fornece gerenciamento de concessão de ponto de verificação e partição.</span><span class="sxs-lookup"><span data-stu-id="848de-298">The `ChangeFeedProcessorHost` class provides a thread-safe, multi-process, safe runtime environment for event processor implementations that also provides checkpointing and partition lease management.</span></span> <span data-ttu-id="848de-299">Para usar a classe `ChangeFeedProcessorHost`, você pode implementar `IChangeFeedObserver`.</span><span class="sxs-lookup"><span data-stu-id="848de-299">To use the `ChangeFeedProcessorHost` class, you can implement `IChangeFeedObserver`.</span></span> <span data-ttu-id="848de-300">Essa interface contém três métodos:</span><span class="sxs-lookup"><span data-stu-id="848de-300">This interface contains three methods:</span></span>

* <span data-ttu-id="848de-301">`OpenAsync`: essa função é chamada quando o observador do feed de alterações é aberto.</span><span class="sxs-lookup"><span data-stu-id="848de-301">`OpenAsync`: This function is called when change feed observer is opened.</span></span> <span data-ttu-id="848de-302">Ela pode ser modificada para realizar uma ação específica quando o consumidor/observador for aberto.</span><span class="sxs-lookup"><span data-stu-id="848de-302">It can be modified to perform a specific action when consumer/observer is opened.</span></span>  
* <span data-ttu-id="848de-303">`CloseAsync`: essa função é chamada quando o observador do feed de alterações é terminado.</span><span class="sxs-lookup"><span data-stu-id="848de-303">`CloseAsync`: This function is called when change feed observer is terminated.</span></span> <span data-ttu-id="848de-304">Ela pode ser modificada para realizar uma ação específica quando o consumidor/observador for fechado.</span><span class="sxs-lookup"><span data-stu-id="848de-304">It can be modified to perform a specific action when consumer/observer is closed.</span></span>  
* <span data-ttu-id="848de-305">`ProcessChangesAsync`: essa função é chamada quando novas alterações de documento estão disponíveis no feed de alterações.</span><span class="sxs-lookup"><span data-stu-id="848de-305">`ProcessChangesAsync`: This function is called when document new changes are available on change feed.</span></span> <span data-ttu-id="848de-306">Ela pode ser modificada para realizar uma ação específica após cada atualização do feed de alterações.</span><span class="sxs-lookup"><span data-stu-id="848de-306">It can be modified to perform a specific action upon every change feed update.</span></span>  

<span data-ttu-id="848de-307">Em nosso exemplo, implementamos a interface `IChangeFeedObserver` por meio da classe `DocumentFeedObserver`.</span><span class="sxs-lookup"><span data-stu-id="848de-307">In our example, we implement the interface `IChangeFeedObserver` through the `DocumentFeedObserver` class.</span></span> <span data-ttu-id="848de-308">Aqui, a função `ProcessChangesAsync` faz upsert (atualiza) de um documento do feed de alterações na coleção de destino.</span><span class="sxs-lookup"><span data-stu-id="848de-308">Here, the `ProcessChangesAsync` function upserts (updates) a document from change feed into the destination collection.</span></span> <span data-ttu-id="848de-309">Este exemplo é útil para mover dados de uma coleção para outra, a fim de alterar a chave de partição de um conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="848de-309">This example is useful for moving data from one collection to another in order to change the partition key of a data set.</span></span> 

<span data-ttu-id="848de-310">*Executando o Host de processador*</span><span class="sxs-lookup"><span data-stu-id="848de-310">*Running the Processor Host*</span></span>

<span data-ttu-id="848de-311">Antes de começar o processamento de eventos, as opções do feed de alterações e as opções de host do feed de alterações podem ser personalizadas.</span><span class="sxs-lookup"><span data-stu-id="848de-311">Before beginning event processing, both change feed options and change feed host options can be customized.</span></span> 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval to 15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
<span data-ttu-id="848de-312">Os campos específicos que podem ser personalizados estão resumidos nas tabelas a seguir.</span><span class="sxs-lookup"><span data-stu-id="848de-312">The specific fields that can be customized are summarized in the following tables.</span></span> 

<span data-ttu-id="848de-313">**Opções do feed de alterações**:</span><span class="sxs-lookup"><span data-stu-id="848de-313">**Change Feed Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="848de-314">Nome da Propriedade</span><span class="sxs-lookup"><span data-stu-id="848de-314">Property Name</span></span></th>
        <th><span data-ttu-id="848de-315">Descrição</span><span class="sxs-lookup"><span data-stu-id="848de-315">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="848de-316">MaxItemCount</span><span class="sxs-lookup"><span data-stu-id="848de-316">MaxItemCount</span></span></td>
        <td><span data-ttu-id="848de-317">Obtém ou define o número máximo de itens a serem retornados na operação de enumeração no serviço de banco de dados do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="848de-317">Gets or sets the maximum number of items to be returned in the enumeration operation in the Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="848de-318">PartitionKeyRangeId</span><span class="sxs-lookup"><span data-stu-id="848de-318">PartitionKeyRangeId</span></span></td>
        <td><span data-ttu-id="848de-319">Obtém ou define a ID do intervalo de chave de partição da solicitação atual no serviço de banco de dados do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="848de-319">Gets or sets the partition key range id for the current request in the Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="848de-320">RequestContinuation</span><span class="sxs-lookup"><span data-stu-id="848de-320">RequestContinuation</span></span></td>
        <td><span data-ttu-id="848de-321">Obtém ou define o token de continuação de solicitação no serviço de banco de dados do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="848de-321">Gets or sets the request continuation token in the Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="848de-322">SessionToken</span><span class="sxs-lookup"><span data-stu-id="848de-322">SessionToken</span></span></td>
        <td><span data-ttu-id="848de-323">Obtém ou define o token de sessão para ser usado com a consistência de sessão no serviço de banco de dados do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="848de-323">Gets or sets the session token for use with session consistency in the Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="848de-324">StartFromBeginning</span><span class="sxs-lookup"><span data-stu-id="848de-324">StartFromBeginning</span></span></td>
        <td><span data-ttu-id="848de-325">Obtém ou define se o feed de alterações no serviço de banco de dados do Azure Cosmos DB deve começar do início (true) ou do local atual (false).</span><span class="sxs-lookup"><span data-stu-id="848de-325">Gets or sets whether change feed in the Azure Cosmos DB database service should start from the beginning (true) or from current (false).</span></span> <span data-ttu-id="848de-326">Por padrão, ele inicia do local atual (false).</span><span class="sxs-lookup"><span data-stu-id="848de-326">By default, it starts from current (false).</span></span></td>
    </tr>
</table>

<span data-ttu-id="848de-327">**Opções do host do feed de alterações**:</span><span class="sxs-lookup"><span data-stu-id="848de-327">**Change Feed Host Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="848de-328">Nome da Propriedade</span><span class="sxs-lookup"><span data-stu-id="848de-328">Property Name</span></span></th>
        <th><span data-ttu-id="848de-329">Tipo</span><span class="sxs-lookup"><span data-stu-id="848de-329">Type</span></span></th>
        <th><span data-ttu-id="848de-330">Descrição</span><span class="sxs-lookup"><span data-stu-id="848de-330">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="848de-331">LeaseRenewInterval</span><span class="sxs-lookup"><span data-stu-id="848de-331">LeaseRenewInterval</span></span></td>
        <td><span data-ttu-id="848de-332">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="848de-332">TimeSpan</span></span></td>
        <td><span data-ttu-id="848de-333">O intervalo de todas as concessões para partições mantidas atualmente pela instância ChangeFeedEventHost.</span><span class="sxs-lookup"><span data-stu-id="848de-333">The interval for all leases for partitions currently held by the ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="848de-334">LeaseAcquireInterval</span><span class="sxs-lookup"><span data-stu-id="848de-334">LeaseAcquireInterval</span></span></td>
        <td><span data-ttu-id="848de-335">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="848de-335">TimeSpan</span></span></td>
        <td><span data-ttu-id="848de-336">O intervalo para disparar uma tarefa para computar se as partições são distribuídas uniformemente entre as instâncias de host conhecidas.</span><span class="sxs-lookup"><span data-stu-id="848de-336">The interval to kick off a task to compute whether partitions are distributed evenly among known host instances.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="848de-337">LeaseExpirationInterval</span><span class="sxs-lookup"><span data-stu-id="848de-337">LeaseExpirationInterval</span></span></td>
        <td><span data-ttu-id="848de-338">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="848de-338">TimeSpan</span></span></td>
        <td><span data-ttu-id="848de-339">O intervalo para o qual a concessão é tomada em uma concessão que representa uma partição.</span><span class="sxs-lookup"><span data-stu-id="848de-339">The interval for which the lease is taken on a lease representing a partition.</span></span> <span data-ttu-id="848de-340">Se a concessão não for renovada dentro deste intervalo, ela será expirada e a propriedade da partição será movida para outra instância de ChangeFeedEventHost.</span><span class="sxs-lookup"><span data-stu-id="848de-340">If the lease is not renewed within this interval, it is expired and ownership of the partition moves to another ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="848de-341">FeedPollDelay</span><span class="sxs-lookup"><span data-stu-id="848de-341">FeedPollDelay</span></span></td>
        <td><span data-ttu-id="848de-342">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="848de-342">TimeSpan</span></span></td>
        <td><span data-ttu-id="848de-343">O atraso entre a sondagem de uma partição quanto a novas alterações no feed, depois que todas as alterações atuais forem descarregadas.</span><span class="sxs-lookup"><span data-stu-id="848de-343">The delay between polling a partition for new changes on the feed, after all current changes are drained.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="848de-344">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="848de-344">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="848de-345">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="848de-345">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="848de-346">A frequência das concessões de ponto de verificação.</span><span class="sxs-lookup"><span data-stu-id="848de-346">The frequency to checkpoint leases.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="848de-347">MinPartitionCount</span><span class="sxs-lookup"><span data-stu-id="848de-347">MinPartitionCount</span></span></td>
        <td><span data-ttu-id="848de-348">int</span><span class="sxs-lookup"><span data-stu-id="848de-348">Int</span></span></td>
        <td><span data-ttu-id="848de-349">A contagem de partição mínima para o host.</span><span class="sxs-lookup"><span data-stu-id="848de-349">The minimum partition count for the host.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="848de-350">MaxPartitionCount</span><span class="sxs-lookup"><span data-stu-id="848de-350">MaxPartitionCount</span></span></td>
        <td><span data-ttu-id="848de-351">int</span><span class="sxs-lookup"><span data-stu-id="848de-351">Int</span></span></td>
        <td><span data-ttu-id="848de-352">O número máximo de partições a que o host pode servir.</span><span class="sxs-lookup"><span data-stu-id="848de-352">The maximum number of partitions the host can serve.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="848de-353">DiscardExistingLeases</span><span class="sxs-lookup"><span data-stu-id="848de-353">DiscardExistingLeases</span></span></td>
        <td><span data-ttu-id="848de-354">Bool</span><span class="sxs-lookup"><span data-stu-id="848de-354">Bool</span></span></td>
        <td><span data-ttu-id="848de-355">Se todas as concessões existentes no início do host devem ser excluídas e se o host deve começar do zero.</span><span class="sxs-lookup"><span data-stu-id="848de-355">Whether on the start of the host all existing leases should be deleted and the host should start from scratch.</span></span></td>
    </tr>
</table>


<span data-ttu-id="848de-356">Para iniciar o processamento de eventos, crie uma instância do `ChangeFeedProcessorHost`, fornecendo os parâmetros apropriados para a sua coleção do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="848de-356">To start event processing, instantiate `ChangeFeedProcessorHost`, providing the appropriate parameters for your Azure Cosmos DB collection.</span></span> <span data-ttu-id="848de-357">Em seguida, chame `RegisterObserverAsync` para registrar sua implementação `IChangeFeedObserver` (DocumentFeedObserver neste exemplo) com o tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="848de-357">Then, call `RegisterObserverAsync` to register your `IChangeFeedObserver` (DocumentFeedObserver in this example) implementation with the runtime.</span></span> <span data-ttu-id="848de-358">Neste ponto, o host tenta adquirir uma concessão em todos os intervalos de chaves de partição na coleção do Azure Cosmos DB usando um algoritmo "greedy".</span><span class="sxs-lookup"><span data-stu-id="848de-358">At this point, the host attempts to acquire a lease on every partition key range in the Azure Cosmos DB collection using a "greedy" algorithm.</span></span> <span data-ttu-id="848de-359">Essas concessões duram por determinado período e, em seguida, devem ser renovadas.</span><span class="sxs-lookup"><span data-stu-id="848de-359">These leases last for a given timeframe and must then be renewed.</span></span> <span data-ttu-id="848de-360">Como novos nós, as instâncias de trabalho, nesse caso, ficam online, colocam reservas de concessão e, com o tempo, a carga é trocada entre os nós, à medida que cada host tenta adquirir mais concessões.</span><span class="sxs-lookup"><span data-stu-id="848de-360">As new nodes, worker instances, in this case, come online, they place lease reservations and over time the load shifts between nodes as each host attempts to acquire more leases.</span></span> 

<span data-ttu-id="848de-361">No código de exemplo, usamos uma classe factory (DocumentFeedObserverFactory.cs) para criar um observador e a `RegistObserverFactoryAsync` para registrar o observador.</span><span class="sxs-lookup"><span data-stu-id="848de-361">In the sample code, we use a factory class (DocumentFeedObserverFactory.cs) to create an observer and the `RegistObserverFactoryAsync` to register the observer.</span></span> 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter to stop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
<span data-ttu-id="848de-362">Ao longo do tempo, é estabelecido um equilíbrio.</span><span class="sxs-lookup"><span data-stu-id="848de-362">Over time, an equilibrium is established.</span></span> <span data-ttu-id="848de-363">Essa funcionalidade dinâmica permite que o dimensionamento automático baseado em CPU seja aplicado aos consumidores tanto para escalar quanto para reduzir verticalmente.</span><span class="sxs-lookup"><span data-stu-id="848de-363">This dynamic capability enables CPU-based auto-scaling to be applied to consumers for both scale-up and scale-down.</span></span> <span data-ttu-id="848de-364">Se as alterações estiverem disponíveis no Azure Cosmos DB a uma taxa mais rápida do que os consumidores podem processar, o aumento de CPU nos consumidores poderá ser usado para causar uma escala automática na contagem de instâncias de trabalho.</span><span class="sxs-lookup"><span data-stu-id="848de-364">If changes are available in Azure Cosmos DB at a faster rate than consumers can process, the CPU increase on consumers can be used to cause an auto-scale on worker instance count.</span></span>

## <a name="next-steps"></a><span data-ttu-id="848de-365">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="848de-365">Next steps</span></span>
* <span data-ttu-id="848de-366">Experimente as [amostras de código do Feed de alterações do Azure Cosmos DB no GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span><span class="sxs-lookup"><span data-stu-id="848de-366">Try the [Azure Cosmos DB Change feed code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span></span>
* <span data-ttu-id="848de-367">Introdução à codificação com os [SDKs do Azure Cosmos DB](documentdb-sdk-dotnet.md) ou a [API REST](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="848de-367">Get started coding with the [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md) or the [REST API](/rest/api/documentdb/).</span></span>
