---
title: "aaaWorking com alteração Olá feed suporte no banco de dados do Azure Cosmos | Microsoft Docs"
description: "Banco de dados do uso do Azure Cosmos alterar suporte feed tootrack alterações nos documentos e executar o processamento baseado em evento, como gatilhos e mantendo os sistemas de caches e análise atualizada."
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
ms.openlocfilehash: a4dcf4ceb476e3e08266dbcdcbee1d75e1d1eed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-hello-change-feed-support-in-azure-cosmos-db"></a><span data-ttu-id="0b7c5-104">Trabalhando com suporte de feed Olá alteração no banco de dados do Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="0b7c5-104">Working with hello change feed support in Azure Cosmos DB</span></span>
<span data-ttu-id="0b7c5-105">O [Azure Cosmos DB](../cosmos-db/introduction.md) é um serviço de banco de dados rápido, flexível e replicado globalmente, usado para armazenar grandes volumes de dados transacionais e operacionais com latência previsível de milissegundos de dígito único para leituras e gravações.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-105">[Azure Cosmos DB](../cosmos-db/introduction.md) is a fast and flexible globally replicated database service that is used for storing high-volume transactional and operational data with predictable single-digit millisecond latency for reads and writes.</span></span> <span data-ttu-id="0b7c5-106">Isso o torna adequado para IoT, jogos, varejo e aplicativos de log operacional.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-106">This makes it well-suited for IoT, gaming, retail, and operational logging applications.</span></span> <span data-ttu-id="0b7c5-107">Um padrão de design comum nesses aplicativos é tootrack alterações feitas a dados do banco de dados do Cosmos tooAzure e atualizar a exibições materializadas, executam a análise em tempo real, toocold de dados de arquivamento e acionar notificações em determinados eventos de acordo com essas alterações.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-107">A common design pattern in these applications is tootrack changes made tooAzure Cosmos DB data, and update materialized views, perform real-time analytics, archive data toocold storage, and trigger notifications on certain events based on these changes.</span></span> <span data-ttu-id="0b7c5-108">Olá **alteração feed suporte** no banco de dados do Azure Cosmos permite soluções de toobuild eficiente e escalonável para cada um desses padrões.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-108">hello **change feed support** in Azure Cosmos DB enables you toobuild efficient and scalable solutions for each of these patterns.</span></span>

<span data-ttu-id="0b7c5-109">Com suporte de feed de alteração, o banco de dados do Azure Cosmos fornece uma lista ordenada de documentos em uma coleção de banco de dados do Azure Cosmos na ordem de saudação na qual elas foram modificadas.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-109">With change feed support, Azure Cosmos DB provides a sorted list of documents within an Azure Cosmos DB collection in hello order in which they were modified.</span></span> <span data-ttu-id="0b7c5-110">Este feed pode ser usado toolisten para toodata modificações na coleção de saudação e executar ações como:</span><span class="sxs-lookup"><span data-stu-id="0b7c5-110">This feed can be used toolisten for modifications toodata within hello collection and perform actions such as:</span></span>

* <span data-ttu-id="0b7c5-111">Disparar tooan uma chamada de API, quando um documento é inserido ou modificado</span><span class="sxs-lookup"><span data-stu-id="0b7c5-111">Trigger a call tooan API when a document is inserted or modified</span></span>
* <span data-ttu-id="0b7c5-112">Executar o processamento em tempo real (fluxo) em atualizações</span><span class="sxs-lookup"><span data-stu-id="0b7c5-112">Perform real-time (stream) processing on updates</span></span>
* <span data-ttu-id="0b7c5-113">Sincronizar dados com um cache, o mecanismo de pesquisa ou o data warehouse</span><span class="sxs-lookup"><span data-stu-id="0b7c5-113">Synchronize data with a cache, search engine, or data warehouse</span></span>

<span data-ttu-id="0b7c5-114">As alterações no Azure Cosmos DB são persistentes e podem ser processadas de forma assíncrona e distribuídas entre um ou mais consumidores para processamento paralelo.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-114">Changes in Azure Cosmos DB are persisted and can be processed asynchronously, and distributed across one or more consumers for parallel processing.</span></span> <span data-ttu-id="0b7c5-115">Vamos examinar Olá APIs de feed de alteração e como você pode usá-los toobuild aplicativos escalonáveis de em tempo real.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-115">Let's look at hello APIs for change feed and how you can use them toobuild scalable real-time applications.</span></span> <span data-ttu-id="0b7c5-116">Este artigo mostra como toowork com o banco de dados do Azure Cosmos alterar feed e hello API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-116">This article shows how toowork with Azure Cosmos DB change feed and hello DocumentDB API.</span></span> 

![Usar o banco de dados do Azure Cosmos alteração feed análise em tempo real toopower e cenários de computação controlada por evento](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> <span data-ttu-id="0b7c5-118">Alteração de feed de suporte é fornecida somente para Olá API DocumentDB neste momento. Olá Graph API e a API de tabela não têm suporte no momento.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-118">Change feed support is only provided for hello DocumentDB API at this time; hello Graph API and Table API are not currently supported.</span></span>

## <a name="use-cases-and-scenarios"></a><span data-ttu-id="0b7c5-119">Cenários e casos de uso</span><span class="sxs-lookup"><span data-stu-id="0b7c5-119">Use cases and scenarios</span></span>
<span data-ttu-id="0b7c5-120">Feed de alteração permite processamento eficiente de grandes conjuntos de dados com um alto volume de gravações e oferece uma tooidentify de conjuntos de dados inteiro tooquerying alternativo que foi alterado.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-120">Change feed allows for efficient processing of large datasets with a high volume of writes, and offers an alternative tooquerying entire datasets tooidentify what has changed.</span></span> <span data-ttu-id="0b7c5-121">Por exemplo, você pode executar Olá seguintes tarefas com eficiência:</span><span class="sxs-lookup"><span data-stu-id="0b7c5-121">For example, you can perform hello following tasks efficiently:</span></span>

* <span data-ttu-id="0b7c5-122">Atualize um cache, índice de pesquisa ou data warehouse com os dados armazenados no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-122">Update a cache, search index, or a data warehouse with data stored in Azure Cosmos DB.</span></span>
* <span data-ttu-id="0b7c5-123">Implementar dados de nível de aplicativo em camadas e de arquivamento, ou seja, armazenar "dados ativos" no banco de dados do Azure Cosmos e perder a validade "dados frios" muito[armazenamento de BLOBs do Azure](../storage/common/storage-introduction.md) ou [repositório Azure Data Lake](../data-lake-store/data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0b7c5-123">Implement application-level data tiering and archival, that is, store "hot data" in Azure Cosmos DB, and age out "cold data" too[Azure Blob Storage](../storage/common/storage-introduction.md) or [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span></span>
* <span data-ttu-id="0b7c5-124">Implementar a análise em lote nos dados usando o [Apache Hadoop](run-hadoop-with-hdinsight.md).</span><span class="sxs-lookup"><span data-stu-id="0b7c5-124">Implement batch analytics on data using [Apache Hadoop](run-hadoop-with-hdinsight.md).</span></span>
* <span data-ttu-id="0b7c5-125">Implementar [pipelines lambda no Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) com o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-125">Implement [lambda pipelines on Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) with Azure Cosmos DB.</span></span> <span data-ttu-id="0b7c5-126">O Azure Cosmos DB fornece uma solução de banco de dados escalonável que pode manipular a ingestão e a consulta, além de implementar arquiteturas lambda com baixo TCO.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-126">Azure Cosmos DB provides a scalable database solution that can handle both ingestion and query, and implement lambda architectures with low TCO.</span></span> 
* <span data-ttu-id="0b7c5-127">Execute tooanother zero tempo de inatividade migrações conta de banco de dados do Azure Cosmos com um esquema de particionamento diferente.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-127">Perform zero down-time migrations tooanother Azure Cosmos DB account with a different partitioning scheme.</span></span>

<span data-ttu-id="0b7c5-128">**Pipelines lambda com o Azure Cosmos DB para ingestão e consulta:**</span><span class="sxs-lookup"><span data-stu-id="0b7c5-128">**Lambda Pipelines with Azure Cosmos DB for ingestion and query:**</span></span>

![Pipeline lambda baseado no Azure Cosmos DB para ingestão e consulta](./media/change-feed/lambda.png)

<span data-ttu-id="0b7c5-130">Você pode usar o banco de dados do Azure Cosmos tooreceive e armazenar dados de evento de dispositivos, sensores, infraestrutura e aplicativos e processar esses eventos em tempo real com [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), ou [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0b7c5-130">You can use Azure Cosmos DB tooreceive and store event data from devices, sensors, infrastructure, and applications, and process these events in real-time with [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), or [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span></span> 

<span data-ttu-id="0b7c5-131">Dentro de seu [sem servidor](http://azure.com/serverless) aplicativos web e móveis, você pode monitorar eventos como tootrigger de perfil, preferências ou local do cliente de tooyour alterações determinadas ações como dispositivo de envio por push notificações tootheir usando [As funções do azure](../azure-functions/functions-bindings-documentdb.md) ou [serviços de aplicativos](https://azure.microsoft.com/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="0b7c5-131">Within your [serverless](http://azure.com/serverless) web and mobile apps, you can track events such as changes tooyour customer's profile, preferences, or location tootrigger certain actions like sending push notifications tootheir devices using [Azure Functions](../azure-functions/functions-bindings-documentdb.md) or [App Services](https://azure.microsoft.com/services/app-service/).</span></span> <span data-ttu-id="0b7c5-132">Se você estiver usando o banco de dados do Azure Cosmos toobuild um jogo, você pode, por exemplo, usar tabelas em tempo real do feed tooimplement alterações com base em classificações de jogos concluídas.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-132">If you're using Azure Cosmos DB toobuild a game, you can, for example, use change feed tooimplement real-time leaderboards based on scores from completed games.</span></span>

## <a name="how-change-feed-works-in-azure-cosmos-db"></a><span data-ttu-id="0b7c5-133">Como funciona o feed de alterações no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0b7c5-133">How change feed works in Azure Cosmos DB</span></span>
<span data-ttu-id="0b7c5-134">Banco de dados do Azure Cosmos fornece Olá capacidade tooincrementally ler as atualizações feitas tooan coleção do banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-134">Azure Cosmos DB provides hello ability tooincrementally read updates made tooan Azure Cosmos DB collection.</span></span> <span data-ttu-id="0b7c5-135">Este feed alteração tem Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="0b7c5-135">This change feed has hello following properties:</span></span>

* <span data-ttu-id="0b7c5-136">As alterações são persistentes no Azure Cosmos DB e podem ser processadas de forma assíncrona.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-136">Changes are persistent in Azure Cosmos DB and can be processed asynchronously.</span></span>
* <span data-ttu-id="0b7c5-137">Alterações toodocuments dentro de uma coleção estão disponíveis imediatamente no feed de alteração de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-137">Changes toodocuments within a collection are available immediately in hello change feed.</span></span>
* <span data-ttu-id="0b7c5-138">Cada documento de tooa alteração aparece exatamente uma vez no feed de alteração de saudação e clientes gerenciem sua lógica de ponto de verificação.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-138">Each change tooa document appears exactly once in hello change feed, and clients manage their checkpointing logic.</span></span> <span data-ttu-id="0b7c5-139">biblioteca de feed do processador de alteração Olá fornece verificação automática e "pelo menos uma vez" semântica.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-139">hello change feed processor library provides automatic checkpointing and "at least once" semantics.</span></span>
* <span data-ttu-id="0b7c5-140">A mudança mais recente Olá somente para um determinado documento está incluída no log de alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-140">Only hello most recent change for a given document is included in hello change log.</span></span> <span data-ttu-id="0b7c5-141">As alterações intermediárias podem não estar disponíveis.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-141">Intermediate changes may not be available.</span></span>
* <span data-ttu-id="0b7c5-142">Olá alteração feed é classificado por ordem de modificação em cada valor de chave de partição.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-142">hello change feed is sorted by order of modification within each partition key value.</span></span> <span data-ttu-id="0b7c5-143">Não há nenhuma garantia de ordem entre os valores de chave de partição.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-143">There is no guaranteed order across partition-key values.</span></span>
* <span data-ttu-id="0b7c5-144">As alterações podem ser sincronizadas de qualquer ponto no tempo, ou seja, não há nenhum período de retenção de dados fixo para o qual haja alterações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-144">Changes can be synchronized from any point-in-time, that is, there is no fixed data retention period for which changes are available.</span></span>
* <span data-ttu-id="0b7c5-145">As alterações estão disponíveis em blocos de intervalos de chaves de partição.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-145">Changes are available in chunks of partition key ranges.</span></span> <span data-ttu-id="0b7c5-146">Esse recurso permite que as alterações de coleções grandes toobe processados em paralelo por vários consumidores/servidores.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-146">This capability allows changes from large collections toobe processed in parallel by multiple consumers/servers.</span></span>
* <span data-ttu-id="0b7c5-147">Os aplicativos podem solicitar para alterar vários feeds simultaneamente em Olá mesmo coleção.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-147">Applications can request for multiple change feeds simultaneously on hello same collection.</span></span>

<span data-ttu-id="0b7c5-148">O feed de alterações do Azure Cosmos DB é habilitado por padrão para todas as contas.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-148">Azure Cosmos DB's change feed is enabled by default for all accounts.</span></span> <span data-ttu-id="0b7c5-149">Você pode usar o [taxa de transferência fornecida](request-units.md) em sua região de gravação ou em qualquer [ler região](distribute-data-globally.md) tooread de saudação alterar feed, assim como qualquer outra operação do banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-149">You can use your [provisioned throughput](request-units.md) in your write region or any [read region](distribute-data-globally.md) tooread from hello change feed, just like any other operation from Azure Cosmos DB.</span></span> <span data-ttu-id="0b7c5-150">feed de alteração de saudação inclui inserções e operações de atualização feitas toodocuments na coleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-150">hello change feed includes inserts and update operations made toodocuments within hello collection.</span></span> <span data-ttu-id="0b7c5-151">Você pode capturar exclusões ao definir um sinalizador de "exclusão reversível" em seus documentos em vez de exclusões.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-151">You can capture deletes by setting a "soft-delete" flag within your documents in place of deletes.</span></span> <span data-ttu-id="0b7c5-152">Como alternativa, você pode definir um período de validade finito para seus documentos por meio de saudação [recurso TTL](time-to-live.md), por exemplo, 24 horas e use Olá valor dessa propriedade toocapture exclui.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-152">Alternatively, you can set a finite expiration period for your documents via hello [TTL capability](time-to-live.md), for example, 24 hours and use hello value of that property toocapture deletes.</span></span> <span data-ttu-id="0b7c5-153">Com essa solução, você tem alterações tooprocess dentro de um intervalo de tempo menor que o período de validade de TTL hello.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-153">With this solution, you have tooprocess changes within a shorter time interval than hello TTL expiration period.</span></span> <span data-ttu-id="0b7c5-154">Olá alteração feed está disponível para cada intervalo de chave de partição na coleção de saudação do documento e, portanto, pode ser distribuído em um ou mais consumidores para processamento paralelo.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-154">hello change feed is available for each partition key range within hello document collection, and thus can be distributed across one or more consumers for parallel processing.</span></span> 

![Processamento distribuído do feed de alterações do Azure Cosmos DB](./media/change-feed/changefeedvisual.png)

<span data-ttu-id="0b7c5-156">Você tem algumas opções para implementar um feed de alterações em seu código de cliente.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-156">You have a few options in how you implement a change feed in your client code.</span></span> <span data-ttu-id="0b7c5-157">Olá seções que imediatamente a seguir descrevem como tooimplement Olá feed de alteração usando hello Azure Cosmos DB REST API e Olá SDKs do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-157">hello sections that immediately follow describe how tooimplement hello change feed using hello Azure Cosmos DB REST API and hello DocumentDB SDKs.</span></span> <span data-ttu-id="0b7c5-158">No entanto, para aplicativos .NET, recomendamos usar Olá novo [processador biblioteca de feed de alteração](#change-feed-processor) para eventos de processamento de saudação alterar feed como ele simplifica a alterações de leitura em partições e permite que vários threads trabalhando em paralelo.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-158">However, for .NET applications, we recommend using hello new [Change feed processor library](#change-feed-processor) for processing events from hello change feed as it simplifies reading changes across partitions and enables multiple threads working in parallel.</span></span> 

## <span data-ttu-id="0b7c5-159"><a id="rest-apis"></a>Trabalhando com hello API REST e SDKs do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="0b7c5-159"><a id="rest-apis"></a>Working with hello REST API and DocumentDB SDKs</span></span>
<span data-ttu-id="0b7c5-160">O Azure Cosmos DB fornece contêineres elásticos de armazenamento e produtividade chamados **coleções**.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-160">Azure Cosmos DB provides elastic containers of storage and throughput called **collections**.</span></span> <span data-ttu-id="0b7c5-161">Os dados em coleções são logicamente agrupados usando [chaves de partição](partition-data.md) para obtenção de escalabilidade e desempenho.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-161">Data within collections is logically grouped using [partition keys](partition-data.md) for scalability and performance.</span></span> <span data-ttu-id="0b7c5-162">O Azure Cosmos DB fornece várias APIs para acessar esses dados, incluindo pesquisa por ID (Read/Get), consulta e feeds de leitura (verificações).</span><span class="sxs-lookup"><span data-stu-id="0b7c5-162">Azure Cosmos DB provides various APIs for accessing this data, including lookup by ID (Read/Get), query, and read-feeds (scans).</span></span> <span data-ttu-id="0b7c5-163">Olá feed de alteração pode ser obtida preenchendo dois nova solicitação cabeçalhos toohello documentos `ReadDocumentFeed` API e podem ser processadas em paralelo em intervalos de chaves de partição.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-163">hello change feed can be obtained by populating two new request headers toohello DocumentDB `ReadDocumentFeed` API, and can be processed in parallel across ranges of partition keys.</span></span>

### <a name="readdocumentfeed-api"></a><span data-ttu-id="0b7c5-164">API do ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="0b7c5-164">ReadDocumentFeed API</span></span>
<span data-ttu-id="0b7c5-165">Vamos examinar o funcionamento do ReadDocumentFeed.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-165">Let's take a brief look at how ReadDocumentFeed works.</span></span> <span data-ttu-id="0b7c5-166">Ler um feed de documentos em uma coleção por meio de saudação dá suporte a banco de dados do Azure Cosmos `ReadDocumentFeed` API.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-166">Azure Cosmos DB supports reading a feed of documents within a collection via hello `ReadDocumentFeed` API.</span></span> <span data-ttu-id="0b7c5-167">Por exemplo, hello solicitação a seguir retorna uma página de documentos dentro Olá `serverlogs` coleção.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-167">For example, hello following request returns a page of documents inside hello `serverlogs` collection.</span></span> 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="0b7c5-168">Resultados podem ser limitados usando Olá `x-ms-max-item-count` cabeçalho e leituras podem ser retomado reenviando a solicitação de saudação com um `x-ms-continuation` cabeçalho é retornado na resposta anterior hello.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-168">Results can be limited by using hello `x-ms-max-item-count` header, and reads can be resumed by resubmitting hello request with a `x-ms-continuation` header returned in hello previous response.</span></span> <span data-ttu-id="0b7c5-169">Quando executado de um único cliente, `ReadDocumentFeed` itera resultados entre partições em série.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-169">When performed from a single client, `ReadDocumentFeed` iterates through results across partitions serially.</span></span> 

<span data-ttu-id="0b7c5-170">**Leitura serial de feed de documento**</span><span class="sxs-lookup"><span data-stu-id="0b7c5-170">**Serial read document feed**</span></span>

<span data-ttu-id="0b7c5-171">Você também pode recuperar o feed de saudação de documentos usando uma saudação suportada [SDKs do banco de dados do Azure Cosmos](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="0b7c5-171">You can also retrieve hello feed of documents using one of hello supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="0b7c5-172">Por exemplo, Olá trecho a seguir mostra como Olá toouse [ReadDocumentFeedAsync método](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) no .NET.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-172">For example, hello following snippet shows how toouse hello [ReadDocumentFeedAsync method](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) in .NET.</span></span>

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a><span data-ttu-id="0b7c5-173">Execução distribuída do ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="0b7c5-173">Distributed execution of ReadDocumentFeed</span></span>
<span data-ttu-id="0b7c5-174">Para coleções que contêm terabytes de dados ou mais, ou um grande volume de atualizações de ingestão, a execução serial de feed de leitura de um único computador cliente pode não ser prática.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-174">For collections that contain terabytes of data or more, or ingest a large volume of updates, serial execution of read feed from a single client machine might not be practical.</span></span> <span data-ttu-id="0b7c5-175">Em ordem toosupport esses cenários de dados grande, Cosmos do Azure DB fornece APIs toodistribute `ReadDocumentFeed` chamadas de modo transparente entre vários leitores/consumidores de cliente.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-175">In order toosupport these big data scenarios, Azure Cosmos DB provides APIs toodistribute `ReadDocumentFeed` calls transparently across multiple client readers/consumers.</span></span> 

<span data-ttu-id="0b7c5-176">**Feed de Documento de Leitura Distribuída**</span><span class="sxs-lookup"><span data-stu-id="0b7c5-176">**Distributed Read Document Feed**</span></span>

<span data-ttu-id="0b7c5-177">processamento escalonável de tooprovide de alterações incrementais, o banco de dados do Cosmos do Azure oferece suporte a um modelo de expansão para alteração de saudação feed API com base em intervalos de chaves de partição.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-177">tooprovide scalable processing of incremental changes, Azure Cosmos DB supports a scale-out model for hello change feed API based on ranges of partition keys.</span></span>

* <span data-ttu-id="0b7c5-178">Você pode obter uma lista de intervalos de chaves de partição para uma coleção que esteja executando uma chamada `ReadPartitionKeyRanges`.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-178">You can obtain a list of partition key ranges for a collection performing a `ReadPartitionKeyRanges` call.</span></span> 
* <span data-ttu-id="0b7c5-179">Para cada intervalo de chave de partição, você pode realizar uma `ReadDocumentFeed` tooread documentos com chaves de partição dentro desse intervalo.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-179">For each partition key range, you can perform a `ReadDocumentFeed` tooread documents with partition keys within that range.</span></span>

### <a name="retrieving-partition-key-ranges-for-a-collection"></a><span data-ttu-id="0b7c5-180">Recuperação de intervalos de chaves de partição para uma coleção</span><span class="sxs-lookup"><span data-stu-id="0b7c5-180">Retrieving partition key ranges for a collection</span></span>
<span data-ttu-id="0b7c5-181">Você pode recuperar intervalos de chave de partição Olá Olá solicitante `pkranges` recursos dentro de uma coleção.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-181">You can retrieve hello partition key ranges by requesting hello `pkranges` resource within a collection.</span></span> <span data-ttu-id="0b7c5-182">Por exemplo hello solicitação a seguir recupera Olá lista de intervalos de chaves de partição para Olá `serverlogs` coleção:</span><span class="sxs-lookup"><span data-stu-id="0b7c5-182">For example hello following request retrieves hello list of partition key ranges for hello `serverlogs` collection:</span></span>

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

<span data-ttu-id="0b7c5-183">Essa solicitação retorna Olá resposta que contém metadados sobre intervalos de chave de partição Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="0b7c5-183">This request returns hello following response containing metadata about hello partition key ranges:</span></span>

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


<span data-ttu-id="0b7c5-184">**Propriedades do intervalo de chave de partição**: cada intervalo de chave de partição inclui propriedades de metadados de saudação de saudação a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="0b7c5-184">**Partition key range properties**: Each partition key range includes hello metadata properties in hello following table:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="0b7c5-185">Nome do cabeçalho</span><span class="sxs-lookup"><span data-stu-id="0b7c5-185">Header name</span></span></th>
        <th><span data-ttu-id="0b7c5-186">Descrição</span><span class="sxs-lookup"><span data-stu-id="0b7c5-186">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="0b7c5-187">ID</span><span class="sxs-lookup"><span data-stu-id="0b7c5-187">id</span></span></td>
        <td>
            <p><span data-ttu-id="0b7c5-188">Olá ID para o intervalo de chave de partição hello.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-188">hello ID for hello partition key range.</span></span> <span data-ttu-id="0b7c5-189">É uma ID estável e exclusiva dentro de cada coleção.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-189">This is a stable and unique ID within each collection.</span></span></p>
            <p><span data-ttu-id="0b7c5-190">Deve ser usado em Olá as seguintes alterações de tooread chamada pelo intervalo de chave de partição.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-190">Must be used in hello following call tooread changes by partition key range.</span></span></p>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="0b7c5-191">maxExclusive</span><span class="sxs-lookup"><span data-stu-id="0b7c5-191">maxExclusive</span></span></td>
        <td><span data-ttu-id="0b7c5-192">valor de hash da chave da partição máximo de Olá para o intervalo de chave de partição hello.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-192">hello maximum partition key hash value for hello partition key range.</span></span> <span data-ttu-id="0b7c5-193">Para uso interno.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-193">For internal use.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0b7c5-194">minInclusive</span><span class="sxs-lookup"><span data-stu-id="0b7c5-194">minInclusive</span></span></td>
        <td><span data-ttu-id="0b7c5-195">valor de hash da chave de partição mínima Olá para intervalo de chave de partição de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-195">hello minimum partition key hash value for hello partition key range.</span></span> <span data-ttu-id="0b7c5-196">Para uso interno.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-196">For internal use.</span></span></td>
    </tr>       
</table>

<span data-ttu-id="0b7c5-197">Você pode fazer isso usando uma saudação suportada [SDKs do banco de dados do Azure Cosmos](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="0b7c5-197">You can do this using one of hello supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="0b7c5-198">Por exemplo, hello trecho a seguir mostra como os intervalos de chave de partição tooretrieve no .NET usando Olá [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) método.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-198">For example, hello following snippet shows how tooretrieve partition key ranges in .NET using hello [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) method.</span></span>

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

<span data-ttu-id="0b7c5-199">Banco de dados do Azure Cosmos oferece suporte à recuperação de documentos por intervalo de chave de partição por configuração Olá opcional `x-ms-documentdb-partitionkeyrangeid` cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-199">Azure Cosmos DB supports retrieval of documents per partition key range by setting hello optional `x-ms-documentdb-partitionkeyrangeid` header.</span></span> 

### <a name="performing-an-incremental-readdocumentfeed"></a><span data-ttu-id="0b7c5-200">Execução de um ReadDocumentFeed incremental</span><span class="sxs-lookup"><span data-stu-id="0b7c5-200">Performing an incremental ReadDocumentFeed</span></span>
<span data-ttu-id="0b7c5-201">ReadDocumentFeed dá suporte a saudação cenários/tarefas para processamento incremental de alterações no banco de dados do Azure Cosmos coleções a seguir:</span><span class="sxs-lookup"><span data-stu-id="0b7c5-201">ReadDocumentFeed supports hello following scenarios/tasks for incremental processing of changes in Azure Cosmos DB collections:</span></span>

* <span data-ttu-id="0b7c5-202">Ler todas as alterações toodocuments desde o início de Olá, ou seja, desde a criação de coleção.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-202">Read all changes toodocuments from hello beginning, that is, from collection creation.</span></span>
* <span data-ttu-id="0b7c5-203">Ler todas as alterações toofuture atualizações toodocuments da hora atual, ou as alterações desde um tempo especificado pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-203">Read all changes toofuture updates toodocuments from current time, or any changes since a user-specified time.</span></span>
* <span data-ttu-id="0b7c5-204">Ler toodocuments de todas as alterações de uma versão lógica da coleção de saudação (ETag).</span><span class="sxs-lookup"><span data-stu-id="0b7c5-204">Read all changes toodocuments from a logical version of hello collection (ETag).</span></span> <span data-ttu-id="0b7c5-205">Você pode seus consumidores com base em Olá retornado ETag de solicitações de leitura de feed incrementais de ponto de verificação.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-205">You can checkpoint your consumers based on hello returned ETag from incremental read-feed requests.</span></span>

<span data-ttu-id="0b7c5-206">alterações de saudação incluem toodocuments inserções e atualizações.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-206">hello changes include inserts and updates toodocuments.</span></span> <span data-ttu-id="0b7c5-207">Exclui toocapture, você deve usar uma propriedade "exclusão reversível" em seus documentos, ou Olá [propriedade TTL interna](time-to-live.md) toosignal uma exclusão pendente no hello alterar feed.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-207">toocapture deletes, you must use a "soft delete" property within your documents, or use hello [built-in TTL property](time-to-live.md) toosignal a pending deletion in hello change feed.</span></span>

<span data-ttu-id="0b7c5-208">Olá a seguinte tabela lista Olá [solicitação](/rest/api/documentdb/common-documentdb-rest-request-headers.md) e [cabeçalhos de resposta](/rest/api/documentdb/common-documentdb-rest-response-headers.md) para operações de ReadDocumentFeed.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-208">hello following table lists hello [request](/rest/api/documentdb/common-documentdb-rest-request-headers.md) and [response headers](/rest/api/documentdb/common-documentdb-rest-response-headers.md) for ReadDocumentFeed operations.</span></span>

<span data-ttu-id="0b7c5-209">**Cabeçalhos de solicitação para ReadDocumentFeed incremental**:</span><span class="sxs-lookup"><span data-stu-id="0b7c5-209">**Request headers for incremental ReadDocumentFeed**:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="0b7c5-210">Nome do cabeçalho</span><span class="sxs-lookup"><span data-stu-id="0b7c5-210">Header name</span></span></th>
        <th><span data-ttu-id="0b7c5-211">Descrição</span><span class="sxs-lookup"><span data-stu-id="0b7c5-211">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="0b7c5-212">A-IM</span><span class="sxs-lookup"><span data-stu-id="0b7c5-212">A-IM</span></span></td>
        <td><span data-ttu-id="0b7c5-213">Deve ser definido de muito "feed Incremental", ou não especificado de outra forma</span><span class="sxs-lookup"><span data-stu-id="0b7c5-213">Must be set too"Incremental feed", or omitted otherwise</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0b7c5-214">If-None-Match</span><span class="sxs-lookup"><span data-stu-id="0b7c5-214">If-None-Match</span></span></td>
        <td>
            <p><span data-ttu-id="0b7c5-215">Nenhum cabeçalho: retorna todas as alterações de saudação começando (criação de coleção)</span><span class="sxs-lookup"><span data-stu-id="0b7c5-215">No header: returns all changes from hello beginning (collection creation)</span></span></p>
            <p><span data-ttu-id="0b7c5-216">"*": retorna todos os novos toodata alterações na coleção de saudação</span><span class="sxs-lookup"><span data-stu-id="0b7c5-216">"*": returns all new changes toodata within hello collection</span></span></p>         
            <p><span data-ttu-id="0b7c5-217">&lt;ETag&gt;: se definir tooa coleção ETag, retorna todas as alterações feitas desde que timestamp lógico</span><span class="sxs-lookup"><span data-stu-id="0b7c5-217">&lt;etag&gt;: If set tooa collection ETag, returns all changes made since that logical timestamp</span></span></p>
        </td>
    </tr>
    <tr>    
        <td><span data-ttu-id="0b7c5-218">If-Modified-Since</span><span class="sxs-lookup"><span data-stu-id="0b7c5-218">If-Modified-Since</span></span></td> 
        <td><span data-ttu-id="0b7c5-219">Formato de hora RFC 1123; ignorado se If-None-Match for especificado</span><span class="sxs-lookup"><span data-stu-id="0b7c5-219">RFC 1123 time format; ignored if If-None-Match is specified</span></span></td> 
    </tr> 
    <tr>
        <td><span data-ttu-id="0b7c5-220">x-ms-documentdb-partitionkeyrangeid</span><span class="sxs-lookup"><span data-stu-id="0b7c5-220">x-ms-documentdb-partitionkeyrangeid</span></span></td>
        <td><span data-ttu-id="0b7c5-221">ID de intervalo de chave da partição de saudação de leitura de dados.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-221">hello partition key range ID for reading data.</span></span></td>
    </tr>
</table>

<span data-ttu-id="0b7c5-222">**Cabeçalhos de resposta para ReadDocumentFeed incremental**:</span><span class="sxs-lookup"><span data-stu-id="0b7c5-222">**Response headers for incremental ReadDocumentFeed**:</span></span>

<table> <tr>
        <th><span data-ttu-id="0b7c5-223">Nome do cabeçalho</span><span class="sxs-lookup"><span data-stu-id="0b7c5-223">Header name</span></span></th>
        <th><span data-ttu-id="0b7c5-224">Descrição</span><span class="sxs-lookup"><span data-stu-id="0b7c5-224">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="0b7c5-225">etag</span><span class="sxs-lookup"><span data-stu-id="0b7c5-225">etag</span></span></td>
        <td>
            <p><span data-ttu-id="0b7c5-226">número de sequência lógica de Hello (LSN) do último documento retornado na resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-226">hello logical sequence number (LSN) of last document returned in hello response.</span></span></p>
            <p><span data-ttu-id="0b7c5-227">O ReadDocumentFeed incremental pode ser retomado por meio do reenvio desse valor em If-None-Match.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-227">Incremental ReadDocumentFeed can be resumed by resubmitting this value in If-None-Match.</span></span></p>
        </td>
    </tr>
</table>

<span data-ttu-id="0b7c5-228">Aqui está um tooreturn de solicitação de exemplo todas as alterações incrementais na coleção de versão/ETag Olá lógica `28535` e intervalo de chave de partição = `16`:</span><span class="sxs-lookup"><span data-stu-id="0b7c5-228">Here's a sample request tooreturn all incremental changes in collection from hello logical version/ETag `28535` and partition key range = `16`:</span></span>

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

<span data-ttu-id="0b7c5-229">As alterações são ordenadas por vez em cada valor de chave de partição dentro do intervalo de chave de partição hello.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-229">Changes are ordered by time within each partition key value within hello partition key range.</span></span> <span data-ttu-id="0b7c5-230">Não há nenhuma garantia de ordem entre os valores de chave de partição.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-230">There is no guaranteed order across partition-key values.</span></span> <span data-ttu-id="0b7c5-231">Se houver mais resultados que pode caber em uma única página, você pode ler a próxima página Olá de resultados reenviando a solicitação Olá com hello `If-None-Match` cabeçalho com toohello igual valor `etag` da resposta anterior hello.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-231">If there are more results than can fit in a single page, you can read hello next page of results by resubmitting hello request with hello `If-None-Match` header with value equal toohello `etag` from hello previous response.</span></span> <span data-ttu-id="0b7c5-232">Se vários documentos foram inseridos ou atualizados transacionalmente dentro de um procedimento armazenado ou gatilho, eles serão todos os retornados em Olá mesmo página de resposta.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-232">If multiple documents were inserted or updated transactionally within a stored procedure or trigger, they will all be returned within hello same response page.</span></span>

> [!NOTE]
> <span data-ttu-id="0b7c5-233">Com o feed de alteração, você pode obter mais itens retornados em uma página que o especificado na `x-ms-max-item-count` no caso de saudação de vários documentos inseridos ou atualizados dentro de procedimentos armazenados ou disparadores.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-233">With change feed, you might get more items returned in a page than specified in `x-ms-max-item-count` in hello case of multiple documents inserted or updated inside a stored procedures or triggers.</span></span> 

<span data-ttu-id="0b7c5-234">Ao usar o hello .NET SDK (1.17.0), defina o campo Olá `StartTime` na `ChangeFeedOptions` documentos toodirectly retorno alterado desde `StartTime` ao chamar `CreateDocumentChangeFeedQuery`.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-234">When using hello .NET SDK (1.17.0), set hello field `StartTime` in `ChangeFeedOptions` toodirectly return changed documents since `StartTime` when calling  `CreateDocumentChangeFeedQuery`.</span></span> <span data-ttu-id="0b7c5-235">Especificando `If-Modified-Since` usando Olá API REST, sua solicitação retorna não Olá documentos si, mas em vez disso, o token de continuação hello ou `etag` no cabeçalho de resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-235">By specifying `If-Modified-Since` using hello REST API, your request will return not hello documents themselves, but rather hello continuation token or `etag` in hello response header.</span></span> <span data-ttu-id="0b7c5-236">documentos de Olá tooreturn Olá modificado especificado tempo, o token de continuação Olá `etag` deve ser usado na próxima solicitação Olá com `If-None-Match` tooreturn Olá documentos reais.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-236">tooreturn hello documents modified hello specified time, hello continuation token `etag` must then be used in hello next request with `If-None-Match` tooreturn hello actual documents.</span></span> 

<span data-ttu-id="0b7c5-237">Olá .NET SDK fornece Olá [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) e [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) tooaccess alterações tooa coleção de classes auxiliares.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-237">hello .NET SDK provides hello [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) and [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) helper classes tooaccess changes made tooa collection.</span></span> <span data-ttu-id="0b7c5-238">Olá trecho a seguir mostra como tooretrieve todas as alterações desde o início do hello usando Olá SDK .NET de um único cliente.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-238">hello following snippet shows how tooretrieve all changes from hello beginning using hello .NET SDK from a single client.</span></span>

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
<span data-ttu-id="0b7c5-239">E hello trecho a seguir mostra como tooprocess é alterado em tempo real com o banco de dados do Azure Cosmos usando Olá alterações de feed de suporte e Olá anterior de função.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-239">And hello following snippet shows how tooprocess changes in real-time with Azure Cosmos DB by using hello change feed support and hello preceding function.</span></span> <span data-ttu-id="0b7c5-240">Olá primeira chamada retorna todos os documentos de saudação na coleção de saudação e Olá segundo só retorna Olá dois documentos criados que foram criados desde o último ponto de verificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-240">hello first call returns all hello documents in hello collection, and hello second only returns hello two documents created that were created since hello last checkpoint.</span></span>

```csharp
// Returns all documents in hello collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only hello two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

<span data-ttu-id="0b7c5-241">Você também pode filtrar Olá alteração feed usando eventos do processo do cliente no lado do lógica tooselectively.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-241">You can also filter hello change feed using client side logic tooselectively process events.</span></span> <span data-ttu-id="0b7c5-242">Por exemplo, aqui está um trecho de código que usa o cliente lado LINQ tooprocess apenas eventos de alteração de temperatura de sensores de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-242">For example, here's a snippet that uses client side LINQ tooprocess only temperature change events from device sensors.</span></span>

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <span data-ttu-id="0b7c5-243"><a id="change-feed-processor"></a>Biblioteca do processador do feed de alterações</span><span class="sxs-lookup"><span data-stu-id="0b7c5-243"><a id="change-feed-processor"></a>Change Feed Processor library</span></span>
<span data-ttu-id="0b7c5-244">Outra opção é Olá toouse [biblioteca Azure Cosmos DB alterar Feed processador](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), que podem ajudá-lo a facilmente distribuir o processamento de uma alteração de feed em vários consumidores de eventos.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-244">Another option is toouse hello [Azure Cosmos DB Change Feed Processor library](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), which can help you easily distribute event processing from a change feed across multiple consumers.</span></span> <span data-ttu-id="0b7c5-245">biblioteca de saudação é excelente para a criação de leitores de feed na plataforma .NET de saudação de alteração.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-245">hello library is great for building change feed readers on hello .NET platform.</span></span> <span data-ttu-id="0b7c5-246">Alguns fluxos de trabalho que seriam simplificados usando biblioteca de processador de Feed de alteração Olá sobre métodos de saudação incluídos no hello outros SDKs do banco de dados Cosmos incluem:</span><span class="sxs-lookup"><span data-stu-id="0b7c5-246">Some workflows that would be simplified by using hello Change Feed Processor library over hello methods included in hello other Cosmos DB SDKs include:</span></span> 

* <span data-ttu-id="0b7c5-247">Efetuar pull de atualizações de feed de alterações quando os dados são armazenados em várias partições</span><span class="sxs-lookup"><span data-stu-id="0b7c5-247">Pulling updates from change feed when data is stored across multiple partitions</span></span>
* <span data-ttu-id="0b7c5-248">Movendo ou replicando dados de uma coleção tooanother</span><span class="sxs-lookup"><span data-stu-id="0b7c5-248">Moving or replicating data from one collection tooanother</span></span>
* <span data-ttu-id="0b7c5-249">Execução paralela de ações disparadas por toodata atualizações e alterações de feed</span><span class="sxs-lookup"><span data-stu-id="0b7c5-249">Parallel execution of actions triggered by updates toodata and change feed</span></span> 

<span data-ttu-id="0b7c5-250">Enquanto usar Olá APIs em Olá Cosmos SDKs fornece acesso preciso toochange feed atualizações em cada partição, usando biblioteca de processador de Feed de alteração de saudação simplifica as alterações de leitura em partições e vários threads de trabalho em paralelo.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-250">While using hello APIs in hello Cosmos SDKs provides precise access toochange feed updates in each partition, using hello Change Feed Processor library simplifies reading changes across partitions and multiple threads working in parallel.</span></span> <span data-ttu-id="0b7c5-251">Em vez de ler manualmente as alterações de cada contêiner e salvar um token de continuação para cada partição, Olá alterar Feed do processador gerencia automaticamente as alterações de leitura em partições usando um mecanismo de concessão.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-251">Instead of manually reading changes from each container and saving a continuation token for each partition, hello Change Feed Processor automatically manages reading changes across partitions using a lease mechanism.</span></span>

<span data-ttu-id="0b7c5-252">biblioteca de saudação está disponível como um pacote do NuGet: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) e de código-fonte como Github [exemplo](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span><span class="sxs-lookup"><span data-stu-id="0b7c5-252">hello library is available as a NuGet Package: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) and from source code as a Github [sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span></span> 

### <a name="understanding-change-feed-processor-library"></a><span data-ttu-id="0b7c5-253">Noções básicas sobre a biblioteca do processador do feed de alterações</span><span class="sxs-lookup"><span data-stu-id="0b7c5-253">Understanding Change Feed Processor library</span></span> 

<span data-ttu-id="0b7c5-254">Existem quatro componentes principais da implementação Olá alterar Feed do processador: Olá monitorado coleção, coleção de concessão hello, host de processador hello e consumidores de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-254">There are four main components of implementing hello Change Feed Processor: hello monitored collection, hello lease collection, hello processor host, and hello consumers.</span></span> 

<span data-ttu-id="0b7c5-255">**Coleta monitorada:** coleção Olá monitorado é dados de saudação do qual Olá alteração feed é gerado.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-255">**Monitored Collection:** hello monitored collection is hello data from which hello change feed is generated.</span></span> <span data-ttu-id="0b7c5-256">Qualquer coleção toohello monitorado inserções e as alterações são refletidas no feed de alteração de saudação da coleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-256">Any inserts and changes toohello monitored collection are reflected in hello change feed of hello collection.</span></span> 

<span data-ttu-id="0b7c5-257">**Coleção de concessão:** Olá coordenadas de coleção de concessão alteração Olá feed entre vários trabalhadores de processamento.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-257">**Lease Collection:** hello lease collection coordinates processing hello change feed across multiple workers.</span></span> <span data-ttu-id="0b7c5-258">Uma coleção separada é toostore usado concessões de saudação com uma concessão por partição.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-258">A separate collection is used toostore hello leases with one lease per partition.</span></span> <span data-ttu-id="0b7c5-259">É vantajoso toostore esta coleção de concessão em uma conta diferente com hello gravar Olá toowhere próximo região processador de Feed de alteração está em execução.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-259">It is advantageous toostore this lease collection on a different account with hello write region closer toowhere hello Change Feed Processor is running.</span></span> <span data-ttu-id="0b7c5-260">Um objeto de concessão contém Olá seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="0b7c5-260">A lease object contains hello following attributes:</span></span> 
* <span data-ttu-id="0b7c5-261">Proprietário: Especifica o host de saudação que possui a concessão de saudação</span><span class="sxs-lookup"><span data-stu-id="0b7c5-261">Owner: Specifies hello host that owns hello lease</span></span>
* <span data-ttu-id="0b7c5-262">Continuação: Especifica a posição de saudação (token de continuação) na alteração Olá feed para uma determinada partição</span><span class="sxs-lookup"><span data-stu-id="0b7c5-262">Continuation: Specifies hello position (continuation token) in hello change feed for a particular partition</span></span>
* <span data-ttu-id="0b7c5-263">Timestamp: Hora da última concessão foi atualizada; Olá timestamp pode ser usado toocheck se a concessão de saudação é considerado expirado</span><span class="sxs-lookup"><span data-stu-id="0b7c5-263">Timestamp: Last time lease was updated; hello timestamp can be used toocheck whether hello lease is considered expired</span></span> 

<span data-ttu-id="0b7c5-264">**Host de processador:** cada host determina quantos tooprocess de partições com base em quantos outras instâncias de hosts têm concessões ativas.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-264">**Processor Host:** Each host determines how many partitions tooprocess based on how many other instances of hosts have active leases.</span></span> 
1.  <span data-ttu-id="0b7c5-265">Quando um host é iniciado, ele adquire cargas de trabalho concessões toobalance Olá em todos os hosts.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-265">When a host starts up, it acquires leases toobalance hello workload across all hosts.</span></span> <span data-ttu-id="0b7c5-266">Um host renova concessões periodicamente para que as concessões permaneçam ativas.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-266">A host periodically renews leases, so leases remain active.</span></span> 
2.  <span data-ttu-id="0b7c5-267">Uma host pontos de verificação Olá última continuação tooits token concessão para cada leitura.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-267">A host checkpoints hello last continuation token tooits lease for each read.</span></span> <span data-ttu-id="0b7c5-268">tooensure simultaneidade, um host de verificações de segurança hello ETag para cada atualização de concessão.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-268">tooensure concurrency safety, a host checks hello ETag for each lease update.</span></span> <span data-ttu-id="0b7c5-269">Também há suporte para outras estratégias de ponto de verificação.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-269">Other checkpoint strategies are also supported.</span></span>  
3.  <span data-ttu-id="0b7c5-270">Durante o desligamento, um host libera todas as concessões mas mantém Olá informações de continuação, para que ele possa retomar a leitura do ponto de verificação armazenado hello mais tarde.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-270">Upon shutdown, a host releases all leases but keeps hello continuation information, so it can resume reading from hello stored checkpoint later.</span></span> 

<span data-ttu-id="0b7c5-271">No momento o número de saudação de hosts não pode ser maior que o número de saudação de partições (concessões).</span><span class="sxs-lookup"><span data-stu-id="0b7c5-271">At this time hello number of hosts cannot be greater than hello number of partitions (leases).</span></span>

<span data-ttu-id="0b7c5-272">**Os consumidores:** workers, ou os consumidores são os threads que executam alteração Olá feed processamento iniciado por cada host.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-272">**Consumers:** Consumers, or workers, are threads that perform hello change feed processing initiated by each host.</span></span> <span data-ttu-id="0b7c5-273">Cada host de processador pode ter vários consumidores.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-273">Each processor host can have multiple consumers.</span></span> <span data-ttu-id="0b7c5-274">Cada consumidor lê o feed de alteração de saudação do hello partição é atribuída tooand notifica o host de alterações e expirado concessões.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-274">Each consumer reads hello change feed from hello partition it is assigned tooand notifies its host of changes and expired leases.</span></span>

<span data-ttu-id="0b7c5-275">toofurther compreender como esses quatro elementos do processador de Feed de alteração de trabalham juntos, vamos examinar um exemplo hello diagrama a seguir.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-275">toofurther understand how these four elements of Change Feed Processor work together, let's look at an example in hello following diagram.</span></span> <span data-ttu-id="0b7c5-276">Olá monitorado coleção armazena documentos e usa city"hello" como chave de partição hello.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-276">hello monitored collection stores documents and uses hello "city" as hello partition key.</span></span> <span data-ttu-id="0b7c5-277">Podemos ver que partição Olá azul contém documentos com campo de "city" hello de "E um" e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-277">We see that hello blue partition contains documents with hello "city" field from "A-E" and so on.</span></span> <span data-ttu-id="0b7c5-278">Há dois hosts, cada um com dois consumidores lendo de partições Olá quatro em paralelo.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-278">There are two hosts, each with two consumers reading from hello four partitions in parallel.</span></span> <span data-ttu-id="0b7c5-279">Olá setas mostram a consumidores Olá lendo de um ponto específico no hello alterar feed.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-279">hello arrows show hello consumers reading from a specific spot in hello change feed.</span></span> <span data-ttu-id="0b7c5-280">Na primeira partição do hello, azul mais escuro Olá representa alterações não lidas enquanto azul-claro Olá representa Olá já ler alterações no feed de alteração de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-280">In hello first partition, hello darker blue represents unread changes while hello light blue represents hello already read changes on hello change feed.</span></span> <span data-ttu-id="0b7c5-281">hosts de saudação usam Olá concessão coleção toostore uma faixa de tookeep "continuação" valor de saudação atual de leitura de posição de cada consumidor.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-281">hello hosts use hello lease collection toostore a "continuation" value tookeep track of hello current reading position for each consumer.</span></span> 

![Usando a alteração do banco de dados do Azure Cosmos Olá alimentação de host de processador](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a><span data-ttu-id="0b7c5-283">Usando a Biblioteca do processador do feed de alterações</span><span class="sxs-lookup"><span data-stu-id="0b7c5-283">Using Change Feed Processor Library</span></span> 
<span data-ttu-id="0b7c5-284">Olá seção a seguir explica como toouse Olá biblioteca de processador de Feed de alteração no contexto de saudação de replicar as alterações de uma coleção de destino de tooa de coleção de origem.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-284">hello following section explains how toouse hello Change Feed Processor library in hello context of replicating changes from a source collection tooa destination collection.</span></span> <span data-ttu-id="0b7c5-285">Aqui, a coleção de origem Olá é coleção Olá monitorado no processador de Feed de alteração.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-285">Here, hello source collection is hello monitored collection in Change Feed Processor.</span></span> 

<span data-ttu-id="0b7c5-286">**Instalar e incluir o pacote de NuGet de processador de Feed de alteração de saudação**</span><span class="sxs-lookup"><span data-stu-id="0b7c5-286">**Install and include hello Change Feed Processor NuGet package**</span></span> 

<span data-ttu-id="0b7c5-287">Antes de instalar o Pacote NuGet do Processador do feed de alterações, instale:</span><span class="sxs-lookup"><span data-stu-id="0b7c5-287">Before installing Change Feed Processor NuGet Package, first install:</span></span> 
* <span data-ttu-id="0b7c5-288">Microsoft.Azure.DocumentDB, versão 1.13.1 ou superior</span><span class="sxs-lookup"><span data-stu-id="0b7c5-288">Microsoft.Azure.DocumentDB, version 1.13.1 or above</span></span> 
* <span data-ttu-id="0b7c5-289">Newtonsoft.Json, versão 9.0.1 ou superior. Instale `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` e o inclua como uma referência.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-289">Newtonsoft.Json, version 9.0.1 or above Install `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` and include it as a reference.</span></span>

<span data-ttu-id="0b7c5-290">**Criar uma coleção monitorada, uma coleção de destino e uma coleção de concessão**</span><span class="sxs-lookup"><span data-stu-id="0b7c5-290">**Create a monitored, lease and destination collection**</span></span> 

<span data-ttu-id="0b7c5-291">Saudação de toouse ordem biblioteca de processador de Feed de alteração, coleção de concessão Olá precisa toobe criado antes de executar o (s) processador de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-291">In order toouse hello Change Feed Processor Library, hello lease collection needs toobe created before running hello processor host(s).</span></span> <span data-ttu-id="0b7c5-292">Novamente, é recomendável armazenar uma coleção de concessão em uma conta diferente com uma saudação de toowhere gravação região mais próxima que alteração de Feed de processador está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-292">Again, we recommend storing a lease collection on a different account with a write region closer toowhere hello Change Feed Processor is running.</span></span> <span data-ttu-id="0b7c5-293">Neste exemplo de movimentação de dados, precisamos de coleção de destino Olá toocreate antes de executar o host de processador de Feed de alteração de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-293">In this data movement example, we need toocreate hello destination collection before running hello Change Feed Processor host.</span></span> <span data-ttu-id="0b7c5-294">No código de exemplo hello, podemos chamar uma saudação de toocreate método auxiliar monitorada, concedida e as coleções de destino se eles ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-294">In hello sample code we call a helper method toocreate hello monitored, leased, and destination collections if they do not already exist.</span></span> 

> [!WARNING]
> <span data-ttu-id="0b7c5-295">Criando uma coleção tem preços implicações, como reservar a taxa de transferência para Olá toocommunicate de aplicativo com o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-295">Creating a collection has pricing implications, as you are reserving throughput for hello application toocommunicate with Azure Cosmos DB.</span></span> <span data-ttu-id="0b7c5-296">Para obter mais detalhes, visite Olá [página de preços](https://azure.microsoft.com/pricing/details/cosmos-db/)</span><span class="sxs-lookup"><span data-stu-id="0b7c5-296">For more details, please visit hello [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

<span data-ttu-id="0b7c5-297">*Criando um host de processador*</span><span class="sxs-lookup"><span data-stu-id="0b7c5-297">*Creating a processor host*</span></span>

<span data-ttu-id="0b7c5-298">Olá `ChangeFeedProcessorHost` classe fornece um ambiente de tempo de execução do thread-safe, vários processos, seguro para implementações de processador de evento que também fornece gerenciamento de concessão de ponto de verificação e partição.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-298">hello `ChangeFeedProcessorHost` class provides a thread-safe, multi-process, safe runtime environment for event processor implementations that also provides checkpointing and partition lease management.</span></span> <span data-ttu-id="0b7c5-299">Olá toouse `ChangeFeedProcessorHost` classe, você pode implementar `IChangeFeedObserver`.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-299">toouse hello `ChangeFeedProcessorHost` class, you can implement `IChangeFeedObserver`.</span></span> <span data-ttu-id="0b7c5-300">Essa interface contém três métodos:</span><span class="sxs-lookup"><span data-stu-id="0b7c5-300">This interface contains three methods:</span></span>

* <span data-ttu-id="0b7c5-301">`OpenAsync`: essa função é chamada quando o observador do feed de alterações é aberto.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-301">`OpenAsync`: This function is called when change feed observer is opened.</span></span> <span data-ttu-id="0b7c5-302">Pode ser modificado tooperform uma ação específica ao consumidor/observador é aberto.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-302">It can be modified tooperform a specific action when consumer/observer is opened.</span></span>  
* <span data-ttu-id="0b7c5-303">`CloseAsync`: essa função é chamada quando o observador do feed de alterações é terminado.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-303">`CloseAsync`: This function is called when change feed observer is terminated.</span></span> <span data-ttu-id="0b7c5-304">Pode ser modificado tooperform uma ação específica ao consumidor/observador está fechado.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-304">It can be modified tooperform a specific action when consumer/observer is closed.</span></span>  
* <span data-ttu-id="0b7c5-305">`ProcessChangesAsync`: essa função é chamada quando novas alterações de documento estão disponíveis no feed de alterações.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-305">`ProcessChangesAsync`: This function is called when document new changes are available on change feed.</span></span> <span data-ttu-id="0b7c5-306">Ele pode ser modificado tooperform uma ação específica após cada atualização de alteração de feed.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-306">It can be modified tooperform a specific action upon every change feed update.</span></span>  

<span data-ttu-id="0b7c5-307">Em nosso exemplo, implementamos interface Olá `IChangeFeedObserver` por meio de saudação `DocumentFeedObserver` classe.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-307">In our example, we implement hello interface `IChangeFeedObserver` through hello `DocumentFeedObserver` class.</span></span> <span data-ttu-id="0b7c5-308">Aqui, Olá `ProcessChangesAsync` upserts (atualizações) um documento de alteração de feed na coleção de destino de saudação de função.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-308">Here, hello `ProcessChangesAsync` function upserts (updates) a document from change feed into hello destination collection.</span></span> <span data-ttu-id="0b7c5-309">Este exemplo é útil para mover dados de uma coleção tooanother na chave de partição de saudação de toochange de ordem de um conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-309">This example is useful for moving data from one collection tooanother in order toochange hello partition key of a data set.</span></span> 

<span data-ttu-id="0b7c5-310">*Executando Olá Host de processador*</span><span class="sxs-lookup"><span data-stu-id="0b7c5-310">*Running hello Processor Host*</span></span>

<span data-ttu-id="0b7c5-311">Antes de começar o processamento de eventos, as opções do feed de alterações e as opções de host do feed de alterações podem ser personalizadas.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-311">Before beginning event processing, both change feed options and change feed host options can be customized.</span></span> 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval too15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
<span data-ttu-id="0b7c5-312">campos específicos de saudação que podem ser personalizados são resumidos na Olá tabelas a seguir.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-312">hello specific fields that can be customized are summarized in hello following tables.</span></span> 

<span data-ttu-id="0b7c5-313">**Opções do feed de alterações**:</span><span class="sxs-lookup"><span data-stu-id="0b7c5-313">**Change Feed Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="0b7c5-314">Nome da Propriedade</span><span class="sxs-lookup"><span data-stu-id="0b7c5-314">Property Name</span></span></th>
        <th><span data-ttu-id="0b7c5-315">Descrição</span><span class="sxs-lookup"><span data-stu-id="0b7c5-315">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="0b7c5-316">MaxItemCount</span><span class="sxs-lookup"><span data-stu-id="0b7c5-316">MaxItemCount</span></span></td>
        <td><span data-ttu-id="0b7c5-317">Obtém ou define o número máximo de saudação do toobe de itens retornado na operação de enumeração Olá no serviço de banco de dados do banco de dados do Azure Cosmos de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-317">Gets or sets hello maximum number of items toobe returned in hello enumeration operation in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0b7c5-318">PartitionKeyRangeId</span><span class="sxs-lookup"><span data-stu-id="0b7c5-318">PartitionKeyRangeId</span></span></td>
        <td><span data-ttu-id="0b7c5-319">Obtém ou define a id de intervalo de chave da partição para a solicitação atual Olá Olá no serviço de banco de dados do banco de dados do Azure Cosmos hello.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-319">Gets or sets hello partition key range id for hello current request in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0b7c5-320">RequestContinuation</span><span class="sxs-lookup"><span data-stu-id="0b7c5-320">RequestContinuation</span></span></td>
        <td><span data-ttu-id="0b7c5-321">Obtém ou define o token de continuação Olá solicitação no serviço de banco de dados do banco de dados do Azure Cosmos hello.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-321">Gets or sets hello request continuation token in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="0b7c5-322">SessionToken</span><span class="sxs-lookup"><span data-stu-id="0b7c5-322">SessionToken</span></span></td>
        <td><span data-ttu-id="0b7c5-323">Obtém ou define o token de sessão Olá para uso com a coerência de sessão no serviço de banco de dados do banco de dados do Azure Cosmos de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-323">Gets or sets hello session token for use with session consistency in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="0b7c5-324">StartFromBeginning</span><span class="sxs-lookup"><span data-stu-id="0b7c5-324">StartFromBeginning</span></span></td>
        <td><span data-ttu-id="0b7c5-325">Obtém ou define se a alteração de feed no serviço de banco de dados do banco de dados do Azure Cosmos Olá deve começar de Olá começando (true) ou do atual (false).</span><span class="sxs-lookup"><span data-stu-id="0b7c5-325">Gets or sets whether change feed in hello Azure Cosmos DB database service should start from hello beginning (true) or from current (false).</span></span> <span data-ttu-id="0b7c5-326">Por padrão, ele inicia do local atual (false).</span><span class="sxs-lookup"><span data-stu-id="0b7c5-326">By default, it starts from current (false).</span></span></td>
    </tr>
</table>

<span data-ttu-id="0b7c5-327">**Opções do host do feed de alterações**:</span><span class="sxs-lookup"><span data-stu-id="0b7c5-327">**Change Feed Host Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="0b7c5-328">Nome da Propriedade</span><span class="sxs-lookup"><span data-stu-id="0b7c5-328">Property Name</span></span></th>
        <th><span data-ttu-id="0b7c5-329">Tipo</span><span class="sxs-lookup"><span data-stu-id="0b7c5-329">Type</span></span></th>
        <th><span data-ttu-id="0b7c5-330">Descrição</span><span class="sxs-lookup"><span data-stu-id="0b7c5-330">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="0b7c5-331">LeaseRenewInterval</span><span class="sxs-lookup"><span data-stu-id="0b7c5-331">LeaseRenewInterval</span></span></td>
        <td><span data-ttu-id="0b7c5-332">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0b7c5-332">TimeSpan</span></span></td>
        <td><span data-ttu-id="0b7c5-333">intervalo de saudação para todas as concessões para partições mantidos atualmente pela instância de ChangeFeedEventHost hello.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-333">hello interval for all leases for partitions currently held by hello ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0b7c5-334">LeaseAcquireInterval</span><span class="sxs-lookup"><span data-stu-id="0b7c5-334">LeaseAcquireInterval</span></span></td>
        <td><span data-ttu-id="0b7c5-335">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0b7c5-335">TimeSpan</span></span></td>
        <td><span data-ttu-id="0b7c5-336">Olá intervalo tookick off toocompute uma tarefa se partições são distribuídas uniformemente entre as instâncias do host conhecido.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-336">hello interval tookick off a task toocompute whether partitions are distributed evenly among known host instances.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0b7c5-337">LeaseExpirationInterval</span><span class="sxs-lookup"><span data-stu-id="0b7c5-337">LeaseExpirationInterval</span></span></td>
        <td><span data-ttu-id="0b7c5-338">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0b7c5-338">TimeSpan</span></span></td>
        <td><span data-ttu-id="0b7c5-339">intervalo de saudação para qual Olá concessão é obtida em uma concessão que representa uma partição.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-339">hello interval for which hello lease is taken on a lease representing a partition.</span></span> <span data-ttu-id="0b7c5-340">Se a concessão de saudação não for renovada dentro deste intervalo, expirou e propriedade de partição Olá move tooanother ChangeFeedEventHost instância.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-340">If hello lease is not renewed within this interval, it is expired and ownership of hello partition moves tooanother ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0b7c5-341">FeedPollDelay</span><span class="sxs-lookup"><span data-stu-id="0b7c5-341">FeedPollDelay</span></span></td>
        <td><span data-ttu-id="0b7c5-342">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0b7c5-342">TimeSpan</span></span></td>
        <td><span data-ttu-id="0b7c5-343">atraso de saudação entre a sondagem de uma partição para as novas alterações no hello feed depois que todas as alterações atuais serão descarregadas.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-343">hello delay between polling a partition for new changes on hello feed, after all current changes are drained.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0b7c5-344">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="0b7c5-344">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="0b7c5-345">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="0b7c5-345">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="0b7c5-346">Olá concessões de toocheckpoint de frequência.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-346">hello frequency toocheckpoint leases.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0b7c5-347">MinPartitionCount</span><span class="sxs-lookup"><span data-stu-id="0b7c5-347">MinPartitionCount</span></span></td>
        <td><span data-ttu-id="0b7c5-348">int</span><span class="sxs-lookup"><span data-stu-id="0b7c5-348">Int</span></span></td>
        <td><span data-ttu-id="0b7c5-349">Contagem de partição mínima Olá para o host de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-349">hello minimum partition count for hello host.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0b7c5-350">MaxPartitionCount</span><span class="sxs-lookup"><span data-stu-id="0b7c5-350">MaxPartitionCount</span></span></td>
        <td><span data-ttu-id="0b7c5-351">int</span><span class="sxs-lookup"><span data-stu-id="0b7c5-351">Int</span></span></td>
        <td><span data-ttu-id="0b7c5-352">número máximo de saudação do host de saudação de partições pode atender.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-352">hello maximum number of partitions hello host can serve.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="0b7c5-353">DiscardExistingLeases</span><span class="sxs-lookup"><span data-stu-id="0b7c5-353">DiscardExistingLeases</span></span></td>
        <td><span data-ttu-id="0b7c5-354">Bool</span><span class="sxs-lookup"><span data-stu-id="0b7c5-354">Bool</span></span></td>
        <td><span data-ttu-id="0b7c5-355">Se na saudação de início do host de saudação todas as concessões existentes deve ser excluído e host Olá deve começar do zero.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-355">Whether on hello start of hello host all existing leases should be deleted and hello host should start from scratch.</span></span></td>
    </tr>
</table>


<span data-ttu-id="0b7c5-356">toostart processamento de eventos, instanciar `ChangeFeedProcessorHost`, fornecendo os parâmetros adequados Olá para sua coleção de banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-356">toostart event processing, instantiate `ChangeFeedProcessorHost`, providing hello appropriate parameters for your Azure Cosmos DB collection.</span></span> <span data-ttu-id="0b7c5-357">Em seguida, chame `RegisterObserverAsync` tooregister sua `IChangeFeedObserver` implementação (DocumentFeedObserver neste exemplo) com o tempo de execução de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-357">Then, call `RegisterObserverAsync` tooregister your `IChangeFeedObserver` (DocumentFeedObserver in this example) implementation with hello runtime.</span></span> <span data-ttu-id="0b7c5-358">Neste ponto, o host Olá tentativas tooacquire uma concessão em cada intervalo de chave de partição na coleção de banco de dados do Azure Cosmos hello usando um algoritmo de "greedy".</span><span class="sxs-lookup"><span data-stu-id="0b7c5-358">At this point, hello host attempts tooacquire a lease on every partition key range in hello Azure Cosmos DB collection using a "greedy" algorithm.</span></span> <span data-ttu-id="0b7c5-359">Essas concessões duram por determinado período e, em seguida, devem ser renovadas.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-359">These leases last for a given timeframe and must then be renewed.</span></span> <span data-ttu-id="0b7c5-360">Como novos nós, instâncias de trabalho, nesse caso, ficam online, eles usam reservas de concessão e ao longo do tempo carga Olá alterna entre os nós como cada host tenta tooacquire mais concessões.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-360">As new nodes, worker instances, in this case, come online, they place lease reservations and over time hello load shifts between nodes as each host attempts tooacquire more leases.</span></span> 

<span data-ttu-id="0b7c5-361">No código de exemplo hello, usamos um toocreate (DocumentFeedObserverFactory.cs) de classe de fábrica um observador e hello `RegistObserverFactoryAsync` tooregister observador de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-361">In hello sample code, we use a factory class (DocumentFeedObserverFactory.cs) toocreate an observer and hello `RegistObserverFactoryAsync` tooregister hello observer.</span></span> 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter toostop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
<span data-ttu-id="0b7c5-362">Ao longo do tempo, é estabelecido um equilíbrio.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-362">Over time, an equilibrium is established.</span></span> <span data-ttu-id="0b7c5-363">Esse recurso dinâmico permite que a CPU com base em tooconsumers toobe aplicado o dimensionamento automático, para ampliar e reduzir.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-363">This dynamic capability enables CPU-based auto-scaling toobe applied tooconsumers for both scale-up and scale-down.</span></span> <span data-ttu-id="0b7c5-364">Se as alterações estão disponíveis no banco de dados do Azure Cosmos a uma taxa mais rápida que os consumidores possam processar, Olá aumento de CPU nos consumidores pode ser usado toocause um dimensionamento automático na contagem de instâncias de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0b7c5-364">If changes are available in Azure Cosmos DB at a faster rate than consumers can process, hello CPU increase on consumers can be used toocause an auto-scale on worker instance count.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b7c5-365">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0b7c5-365">Next steps</span></span>
* <span data-ttu-id="0b7c5-366">Tente Olá [alteração de banco de dados do Azure Cosmos feed exemplos de código no GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span><span class="sxs-lookup"><span data-stu-id="0b7c5-366">Try hello [Azure Cosmos DB Change feed code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span></span>
* <span data-ttu-id="0b7c5-367">Introdução a codificação com hello [SDKs do banco de dados do Azure Cosmos](documentdb-sdk-dotnet.md) ou hello [API REST](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="0b7c5-367">Get started coding with hello [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/).</span></span>
