---
title: 'Azure Cosmos DB: API, SDK e recursos em Java do DocumentDB, | Microsoft Docs'
description: "Saiba tudo sobre o SDK e a API Java, incluindo datas de lançamento, datas de desativação e alterações feitas entre cada versão do SDK Java do DocumentDB do Azure Cosmos DB."
services: cosmos-db
documentationcenter: java
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 7861cadf-2a05-471a-9925-0fec0599351b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 07/11/2017
ms.author: khdang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 15e3f7ef3bfd6b1f61fe6081a378bdb29e0a1aa2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-documentdb-java-sdk-release-notes-and-resources"></a><span data-ttu-id="f5294-103">Azure Cosmos DB: notas de versão e recursos do SDK Java do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="f5294-103">Azure Cosmos DB: DocumentDB Java SDK release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f5294-104">.NET</span><span class="sxs-lookup"><span data-stu-id="f5294-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="f5294-105">Feed de alterações do .NET</span><span class="sxs-lookup"><span data-stu-id="f5294-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="f5294-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="f5294-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="f5294-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="f5294-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="f5294-108">Java</span><span class="sxs-lookup"><span data-stu-id="f5294-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="f5294-109">Python</span><span class="sxs-lookup"><span data-stu-id="f5294-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="f5294-110">REST</span><span class="sxs-lookup"><span data-stu-id="f5294-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="f5294-111">Provedor de recursos REST</span><span class="sxs-lookup"><span data-stu-id="f5294-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="f5294-112">SQL</span><span class="sxs-lookup"><span data-stu-id="f5294-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="f5294-113">**Baixe o SDK**</span><span class="sxs-lookup"><span data-stu-id="f5294-113">**SDK Download**</span></span></td><td>[<span data-ttu-id="f5294-114">Maven</span><span class="sxs-lookup"><span data-stu-id="f5294-114">Maven</span></span>](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-documentdb%22)</td></tr>

<tr><td><span data-ttu-id="f5294-115">**Documentação da API**</span><span class="sxs-lookup"><span data-stu-id="f5294-115">**API documentation**</span></span></td><td>[<span data-ttu-id="f5294-116">Documentação de referência de API Java</span><span class="sxs-lookup"><span data-stu-id="f5294-116">Java API reference documentation</span></span>](/java/api/com.microsoft.azure.documentdb)</td></tr>

<tr><td><span data-ttu-id="f5294-117">**Contribuir para o SDK**</span><span class="sxs-lookup"><span data-stu-id="f5294-117">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="f5294-118">GitHub</span><span class="sxs-lookup"><span data-stu-id="f5294-118">GitHub</span></span>](https://github.com/Azure/azure-documentdb-java/)</td></tr>

<tr><td><span data-ttu-id="f5294-119">**Introdução**</span><span class="sxs-lookup"><span data-stu-id="f5294-119">**Get started**</span></span></td><td>[<span data-ttu-id="f5294-120">Introdução ao SDK do Java</span><span class="sxs-lookup"><span data-stu-id="f5294-120">Get started with the Java SDK</span></span>](documentdb-java-get-started.md)</td></tr>

<tr><td><span data-ttu-id="f5294-121">**Tutorial do aplicativo Web**</span><span class="sxs-lookup"><span data-stu-id="f5294-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="f5294-122">Desenvolvimento de aplicativos Web com o Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f5294-122">Web application development with Azure Cosmos DB</span></span>](documentdb-java-application.md)</td></tr>

<tr><td><span data-ttu-id="f5294-123">**Tempo de execução atual com suporte**</span><span class="sxs-lookup"><span data-stu-id="f5294-123">**Current supported runtime**</span></span></td><td>[<span data-ttu-id="f5294-124">JDK 7</span><span class="sxs-lookup"><span data-stu-id="f5294-124">JDK 7</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="f5294-125">Notas de versão</span><span class="sxs-lookup"><span data-stu-id="f5294-125">Release Notes</span></span>

### <a name="a-name11201120"></a><span data-ttu-id="f5294-126"><a name="1.12.0"/>1.12.0</span><span class="sxs-lookup"><span data-stu-id="f5294-126"><a name="1.12.0"/>1.12.0</span></span>
* <span data-ttu-id="f5294-127">Correções de bugs críticos para solicitar processamento durante divisões de partição.</span><span class="sxs-lookup"><span data-stu-id="f5294-127">Critical bug fixes to request processing during partition splits.</span></span>
* <span data-ttu-id="f5294-128">Corrigido um problema com os níveis de consistência Strong e BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="f5294-128">Fixed an issue with the Strong and BoundedStaleness consistency levels.</span></span>

### <a name="a-name11101110"></a><span data-ttu-id="f5294-129"><a name="1.11.0"/>1.11.0</span><span class="sxs-lookup"><span data-stu-id="f5294-129"><a name="1.11.0"/>1.11.0</span></span>
* <span data-ttu-id="f5294-130">Adição de suporte a um novo nível de consistência chamado ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="f5294-130">Added support for a new consistency level called ConsistentPrefix.</span></span>
* <span data-ttu-id="f5294-131">Corrigido um bug na leitura da coleção no modo de sessão.</span><span class="sxs-lookup"><span data-stu-id="f5294-131">Fixed a bug in reading collection in session mode.</span></span>

### <a name="a-name11001100"></a><span data-ttu-id="f5294-132"><a name="1.10.0"/>1.10.0</span><span class="sxs-lookup"><span data-stu-id="f5294-132"><a name="1.10.0"/>1.10.0</span></span>
* <span data-ttu-id="f5294-133">Suporte habilitado para coleção particionada com 2.500 RU/s e escala em incrementos de 100 RU/s.</span><span class="sxs-lookup"><span data-stu-id="f5294-133">Enabled support for partitioned collection with as low as 2,500 RU/sec and scale in increments of 100 RU/sec.</span></span>
* <span data-ttu-id="f5294-134">Correção de um bug no assembly nativo que pode causar exceção NullRef em algumas consultas.</span><span class="sxs-lookup"><span data-stu-id="f5294-134">Fixed a bug in the native assembly which can cause NullRef exception in some queries.</span></span>

### <a name="a-name196196"></a><span data-ttu-id="f5294-135"><a name="1.9.6"/>1.9.6</span><span class="sxs-lookup"><span data-stu-id="f5294-135"><a name="1.9.6"/>1.9.6</span></span>
* <span data-ttu-id="f5294-136">Corrigido um erro na configuração do mecanismo de consulta que pode causar exceções para consultas no modo de gateway.</span><span class="sxs-lookup"><span data-stu-id="f5294-136">Fixed a bug in the query engine configuration that may cause exceptions for queries in Gateway mode.</span></span>
* <span data-ttu-id="f5294-137">Corrigidos alguns bugs no contêiner de sessão que podem causar uma exceção "Recurso proprietário não encontrado" para solicitações imediatamente após a criação da coleção.</span><span class="sxs-lookup"><span data-stu-id="f5294-137">Fixed a few bugs in the session container that may cause an "Owner resource not found" exception for requests immediately after collection creation.</span></span>

### <a name="a-name195195"></a><span data-ttu-id="f5294-138"><a name="1.9.5"/>1.9.5</span><span class="sxs-lookup"><span data-stu-id="f5294-138"><a name="1.9.5"/>1.9.5</span></span>
* <span data-ttu-id="f5294-139">Suporte adicionado para consultas de agregação (COUNT, MIN, MAX, SUM e AVG).</span><span class="sxs-lookup"><span data-stu-id="f5294-139">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="f5294-140">Veja [Suporte de agregação](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="f5294-140">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="f5294-141">Adicionado suporte para alteração de feed.</span><span class="sxs-lookup"><span data-stu-id="f5294-141">Added support for change feed.</span></span>
* <span data-ttu-id="f5294-142">Adicionado suporte para informações de cota de coleção por meio de RequestOptions.setPopulateQuotaInfo.</span><span class="sxs-lookup"><span data-stu-id="f5294-142">Added support for collection quota information through RequestOptions.setPopulateQuotaInfo.</span></span>
* <span data-ttu-id="f5294-143">Foi adicionado suporte para o log de script de procedimento armazenado por meio de RequestOptions.setScriptLoggingEnabled.</span><span class="sxs-lookup"><span data-stu-id="f5294-143">Added support for stored procedure script logging through RequestOptions.setScriptLoggingEnabled.</span></span>
* <span data-ttu-id="f5294-144">Corrigido um bug em que a consulta no modo de DirectHttps pode travar ao encontrar falhas de limitação.</span><span class="sxs-lookup"><span data-stu-id="f5294-144">Fixed a bug where query in DirectHttps mode may hang when encountering throttle failures.</span></span>
* <span data-ttu-id="f5294-145">Corrigido um bug no modo de sessão de consistência.</span><span class="sxs-lookup"><span data-stu-id="f5294-145">Fixed a bug in session consistency mode.</span></span>
* <span data-ttu-id="f5294-146">Corrigido um erro que pode causar a NullReferenceException no HttpContext quando a taxa de solicitação é alta.</span><span class="sxs-lookup"><span data-stu-id="f5294-146">Fixed a bug which may cause NullReferenceException in HttpContext when request rate is high.</span></span>
* <span data-ttu-id="f5294-147">Desempenho aprimorado de modo DirectHttps.</span><span class="sxs-lookup"><span data-stu-id="f5294-147">Improved performance of DirectHttps mode.</span></span>

### <a name="a-name194194"></a><span data-ttu-id="f5294-148"><a name="1.9.4"/>1.9.4</span><span class="sxs-lookup"><span data-stu-id="f5294-148"><a name="1.9.4"/>1.9.4</span></span>
* <span data-ttu-id="f5294-149">Acréscimo de suporte a proxy com base em instância simples do cliente com API ConnectionPolicy.setProxy().</span><span class="sxs-lookup"><span data-stu-id="f5294-149">Added simple client instance-based proxy support with ConnectionPolicy.setProxy() API.</span></span>
* <span data-ttu-id="f5294-150">Acréscimo da API DocumentClient.close() para desligar apropriadamente a instância DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="f5294-150">Added DocumentClient.close() API to properly shutdown DocumentClient instance.</span></span>
* <span data-ttu-id="f5294-151">Melhor desempenho de consulta no modo de conectividade direta, derivando o plano de consulta do assembly nativo em vez do Gateway.</span><span class="sxs-lookup"><span data-stu-id="f5294-151">Improved query performance in direct connectivity mode by deriving the query plan from the native assembly instead of the Gateway.</span></span>
* <span data-ttu-id="f5294-152">Defina FAIL_ON_UNKNOWN_PROPERTIES = false para que os usuários não precisem definir JsonIgnoreProperties em seu POJO.</span><span class="sxs-lookup"><span data-stu-id="f5294-152">Set FAIL_ON_UNKNOWN_PROPERTIES = false so users don't need to define JsonIgnoreProperties in their POJO.</span></span>
* <span data-ttu-id="f5294-153">Registro em log refatorado para usar SLF4J.</span><span class="sxs-lookup"><span data-stu-id="f5294-153">Refactored logging to use SLF4J.</span></span>
* <span data-ttu-id="f5294-154">Alguns outros bugs corrigidos no leitor de consistência.</span><span class="sxs-lookup"><span data-stu-id="f5294-154">Fixed a few other bugs in consistency reader.</span></span>

### <a name="a-name193193"></a><span data-ttu-id="f5294-155"><a name="1.9.3"/>1.9.3</span><span class="sxs-lookup"><span data-stu-id="f5294-155"><a name="1.9.3"/>1.9.3</span></span>
* <span data-ttu-id="f5294-156">Correção de um erro no gerenciamento de conexão para evitar perdas de conexão no modo de conectividade direta.</span><span class="sxs-lookup"><span data-stu-id="f5294-156">Fixed a bug in the connection management to prevent connection leaks in direct connectivity mode.</span></span>
* <span data-ttu-id="f5294-157">Correção de um erro na consulta TOP, na qual pode lançar exceções NullReferenece.</span><span class="sxs-lookup"><span data-stu-id="f5294-157">Fixed a bug in the TOP query where it may throw NullReferenece exception.</span></span>
* <span data-ttu-id="f5294-158">Desempenho aprimorado por meio da redução do número de chamadas de rede para os caches internos.</span><span class="sxs-lookup"><span data-stu-id="f5294-158">Improved performance by reducing the number of network call for the internal caches.</span></span>
* <span data-ttu-id="f5294-159">Acréscimo do código de status, ActivityID e URI de Solicitação em DocumentClientException para melhor solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="f5294-159">Added status code, ActivityID and Request URI in DocumentClientException for better troubleshooting.</span></span>

### <a name="a-name192192"></a><span data-ttu-id="f5294-160"><a name="1.9.2"/>1.9.2</span><span class="sxs-lookup"><span data-stu-id="f5294-160"><a name="1.9.2"/>1.9.2</span></span>
* <span data-ttu-id="f5294-161">Correção de um problema no gerenciamento de conexão para estabilidade.</span><span class="sxs-lookup"><span data-stu-id="f5294-161">Fixed an issue in the connection management for stability.</span></span>

### <a name="a-name191191"></a><span data-ttu-id="f5294-162"><a name="1.9.1"/>1.9.1</span><span class="sxs-lookup"><span data-stu-id="f5294-162"><a name="1.9.1"/>1.9.1</span></span>
* <span data-ttu-id="f5294-163">Adicionado suporte para o nível de consistência BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="f5294-163">Added support for BoundedStaleness consistency level.</span></span>
* <span data-ttu-id="f5294-164">Adicionado suporte para conectividade direta para operações CRUD para coleções particionadas.</span><span class="sxs-lookup"><span data-stu-id="f5294-164">Added support for direct connectivity for CRUD operations for partitioned collections.</span></span>
* <span data-ttu-id="f5294-165">Corrigido um erro na consulta de um banco de dados com SQL.</span><span class="sxs-lookup"><span data-stu-id="f5294-165">Fixed a bug in querying a database with SQL.</span></span>
* <span data-ttu-id="f5294-166">Corrigido um erro no cache da sessão em que o token de sessão pode ser definido incorretamente.</span><span class="sxs-lookup"><span data-stu-id="f5294-166">Fixed a bug in the session cache where session token may be set incorrectly.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="f5294-167"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="f5294-167"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="f5294-168">Adicionado suporte para várias consultas paralelas de partição.</span><span class="sxs-lookup"><span data-stu-id="f5294-168">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="f5294-169">Adição de suporte a consultas TOP/ORDER BY de coleções particionadas.</span><span class="sxs-lookup"><span data-stu-id="f5294-169">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>
* <span data-ttu-id="f5294-170">Adicionado suporte para consistência forte.</span><span class="sxs-lookup"><span data-stu-id="f5294-170">Added support for strong consistency.</span></span>
* <span data-ttu-id="f5294-171">Adicionado suporte para solicitações com base em nome ao usar a conectividade direta.</span><span class="sxs-lookup"><span data-stu-id="f5294-171">Added support for name based requests when using direct connectivity.</span></span>
* <span data-ttu-id="f5294-172">Corrigido para deixar o ActivityId consistente em todas as tentativas de solicitação.</span><span class="sxs-lookup"><span data-stu-id="f5294-172">Fixed to make ActivityId stay consistent across all request retries.</span></span>
* <span data-ttu-id="f5294-173">Corrigido um erro relacionado ao cache de sessão ao recriar uma coleção com o mesmo nome.</span><span class="sxs-lookup"><span data-stu-id="f5294-173">Fixed a bug related to the session cache when recreating a collection with the same name.</span></span>
* <span data-ttu-id="f5294-174">Adicionado Polygon e LineString DataTypes ao especificar a política de indexação de coleção para consultas espaciais de isolamento geográfico.</span><span class="sxs-lookup"><span data-stu-id="f5294-174">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span></span>
* <span data-ttu-id="f5294-175">Problemas corrigidos com Java Doc para Java 1.8.</span><span class="sxs-lookup"><span data-stu-id="f5294-175">Fixed issues with Java Doc for Java 1.8.</span></span>

### <a name="a-name181181"></a><span data-ttu-id="f5294-176"><a name="1.8.1"/>1.8.1</span><span class="sxs-lookup"><span data-stu-id="f5294-176"><a name="1.8.1"/>1.8.1</span></span>
* <span data-ttu-id="f5294-177">Um bug foi corrigido em PartitionKeyDefinitionMap para armazenar as coleções de partição única em cache e para não fazer solicitações extras de chave de partição de busca.</span><span class="sxs-lookup"><span data-stu-id="f5294-177">Fixed a bug in PartitionKeyDefinitionMap to cache single partition collections and not make extra fetch partition key requests.</span></span>
* <span data-ttu-id="f5294-178">Um bug foi corrigido para não tentar novamente quando um valor de chave de partição incorreto for fornecido.</span><span class="sxs-lookup"><span data-stu-id="f5294-178">Fixed a bug to not retry when an incorrect partition key value is provided.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="f5294-179"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="f5294-179"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="f5294-180">Suporte adicionado para contas de banco de dados de várias regiões.</span><span class="sxs-lookup"><span data-stu-id="f5294-180">Added the support for multi-region database accounts.</span></span>
* <span data-ttu-id="f5294-181">Suporte adicionado para repetição automática em solicitações limitadas, com opções para personalizar o número máximo de repetições e o tempo de espera máximo de repetição.</span><span class="sxs-lookup"><span data-stu-id="f5294-181">Added support for automatic retry on throttled requests with options to customize the max retry attempts and max retry wait time.</span></span>  <span data-ttu-id="f5294-182">Consulte RetryOptions e ConnectionPolicy.getRetryOptions().</span><span class="sxs-lookup"><span data-stu-id="f5294-182">See RetryOptions and ConnectionPolicy.getRetryOptions().</span></span>
* <span data-ttu-id="f5294-183">IPartitionResolver preterido com base no código de particionamento personalizado.</span><span class="sxs-lookup"><span data-stu-id="f5294-183">Deprecated IPartitionResolver based custom partitioning code.</span></span> <span data-ttu-id="f5294-184">Use coleções particionadas para uma taxa de transferência e armazenamento superiores.</span><span class="sxs-lookup"><span data-stu-id="f5294-184">Please use partitioned collections for higher storage and throughput.</span></span>

### <a name="a-name171171"></a><span data-ttu-id="f5294-185"><a name="1.7.1"/>1.7.1</span><span class="sxs-lookup"><span data-stu-id="f5294-185"><a name="1.7.1"/>1.7.1</span></span>
* <span data-ttu-id="f5294-186">Adicionado suporte à política de repetição para limitação.</span><span class="sxs-lookup"><span data-stu-id="f5294-186">Added retry policy support for throttling.</span></span>  

### <a name="a-name170170"></a><span data-ttu-id="f5294-187"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="f5294-187"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="f5294-188">Adicionado suporte a TTL (vida útil) para documentos.</span><span class="sxs-lookup"><span data-stu-id="f5294-188">Added time to live (TTL) support for documents.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="f5294-189"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="f5294-189"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="f5294-190">Implementação de [coleções particionadas](partition-data.md) e [níveis de desempenho definidos pelo usuário](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="f5294-190">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <a name="a-name151151"></a><span data-ttu-id="f5294-191"><a name="1.5.1"/>1.5.1</span><span class="sxs-lookup"><span data-stu-id="f5294-191"><a name="1.5.1"/>1.5.1</span></span>
* <span data-ttu-id="f5294-192">Foi corrigido um bug no HashPartitionResolver para gerar valores de hash em little-endian para ser consistente com outros SDKs.</span><span class="sxs-lookup"><span data-stu-id="f5294-192">Fixed a bug in HashPartitionResolver to generate hash values in little-endian to be consistent with other SDKs.</span></span>

### <a name="a-name150150"></a><span data-ttu-id="f5294-193"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="f5294-193"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="f5294-194">Adicionar resolvedores de hash e intervalo para ajudar com a fragmentação de arquivos em várias partições.</span><span class="sxs-lookup"><span data-stu-id="f5294-194">Add Hash & Range partition resolvers to assist with sharding applications across multiple partitions.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="f5294-195"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="f5294-195"><a name="1.4.0"/>1.4.0</span></span>
* <span data-ttu-id="f5294-196">Implementar o Upsert.</span><span class="sxs-lookup"><span data-stu-id="f5294-196">Implement Upsert.</span></span> <span data-ttu-id="f5294-197">Novos métodos upsertXXX adicionados para dar suporte ao recurso Upsert.</span><span class="sxs-lookup"><span data-stu-id="f5294-197">New upsertXXX methods added to support Upsert feature.</span></span>
* <span data-ttu-id="f5294-198">Implementar o roteamento com base em ID.</span><span class="sxs-lookup"><span data-stu-id="f5294-198">Implement ID Based Routing.</span></span> <span data-ttu-id="f5294-199">Nenhuma alteração pública de API, todas as alterações são internas.</span><span class="sxs-lookup"><span data-stu-id="f5294-199">No public API changes, all changes internal.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="f5294-200"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="f5294-200"><a name="1.3.0"/>1.3.0</span></span>
* <span data-ttu-id="f5294-201">Versão ignorada para alinhar os números de versão com outros SDKs</span><span class="sxs-lookup"><span data-stu-id="f5294-201">Release skipped to bring version number in alignment with other SDKs</span></span>

### <a name="a-name120120"></a><span data-ttu-id="f5294-202"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="f5294-202"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="f5294-203">Oferece suporte ao Índice Geoespacial.</span><span class="sxs-lookup"><span data-stu-id="f5294-203">Supports GeoSpatial Index</span></span>
* <span data-ttu-id="f5294-204">Valida a propriedade de ID de todos os recursos.</span><span class="sxs-lookup"><span data-stu-id="f5294-204">Validates id property for all resources.</span></span> <span data-ttu-id="f5294-205">As IDs de recursos não podem conter caracteres ?, /, #, \, ou terminar com um espaço.</span><span class="sxs-lookup"><span data-stu-id="f5294-205">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="f5294-206">Adiciona o novo cabeçalho "andamento de transformação do índice" ao ResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="f5294-206">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="f5294-207"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="f5294-207"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="f5294-208">Implementa a política de indexação V2</span><span class="sxs-lookup"><span data-stu-id="f5294-208">Implements V2 indexing policy</span></span>

### <a name="a-name100100"></a><span data-ttu-id="f5294-209"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="f5294-209"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="f5294-210">SDK DO GA</span><span class="sxs-lookup"><span data-stu-id="f5294-210">GA SDK</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="f5294-211">Datas de lançamento e desativação</span><span class="sxs-lookup"><span data-stu-id="f5294-211">Release & Retirement Dates</span></span>
<span data-ttu-id="f5294-212">A Microsoft fornecerá uma notificação pelo menos **12 meses** antes de desativar um SDK, a fim de realizar uma transição tranquila para uma versão mais recente/com suporte.</span><span class="sxs-lookup"><span data-stu-id="f5294-212">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="f5294-213">Os novos recursos, funcionalidades e otimizações são adicionados apenas ao SDK atual. Portanto, recomendamos que você atualize sempre que possível para a versão do SDK mais recente.</span><span class="sxs-lookup"><span data-stu-id="f5294-213">New features and functionality and optimizations are only added to the current SDK, as such it is  recommend that you always upgrade to the latest SDK version as early as possible.</span></span>

<span data-ttu-id="f5294-214">Qualquer solicitação feita ao Cosmos DB com o uso de um SDK desativado será rejeitada pelo serviço.</span><span class="sxs-lookup"><span data-stu-id="f5294-214">Any request to Cosmos DB using a retired SDK will be rejected by the service.</span></span>

> [!WARNING]
> <span data-ttu-id="f5294-215">Todas as versões do SDK do DocumentDB para Java anteriores à versão **1.0.0** foram desativadas em **29 de fevereiro de 2016**.</span><span class="sxs-lookup"><span data-stu-id="f5294-215">All versions of the DocumentDB SDK for Java prior to version **1.0.0** will be retired on **February 29, 2016**.</span></span>
> 
> 

<br/>

| <span data-ttu-id="f5294-216">Versão</span><span class="sxs-lookup"><span data-stu-id="f5294-216">Version</span></span> | <span data-ttu-id="f5294-217">Data do lançamento</span><span class="sxs-lookup"><span data-stu-id="f5294-217">Release Date</span></span> | <span data-ttu-id="f5294-218">Data de desativação</span><span class="sxs-lookup"><span data-stu-id="f5294-218">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="f5294-219">1.12.0</span><span class="sxs-lookup"><span data-stu-id="f5294-219">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="f5294-220">11 de julho de 2017</span><span class="sxs-lookup"><span data-stu-id="f5294-220">July 11, 2017</span></span> |--- |
| [<span data-ttu-id="f5294-221">1.11.0</span><span class="sxs-lookup"><span data-stu-id="f5294-221">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="f5294-222">10 de maio de 2017</span><span class="sxs-lookup"><span data-stu-id="f5294-222">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="f5294-223">1.10.0</span><span class="sxs-lookup"><span data-stu-id="f5294-223">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="f5294-224">11 de março de 2017</span><span class="sxs-lookup"><span data-stu-id="f5294-224">March 11, 2017</span></span> |--- |
| [<span data-ttu-id="f5294-225">1.9.6</span><span class="sxs-lookup"><span data-stu-id="f5294-225">1.9.6</span></span>](#1.9.6) |<span data-ttu-id="f5294-226">21 de fevereiro de 2017</span><span class="sxs-lookup"><span data-stu-id="f5294-226">February 21, 2017</span></span> |--- |
| [<span data-ttu-id="f5294-227">1.9.5</span><span class="sxs-lookup"><span data-stu-id="f5294-227">1.9.5</span></span>](#1.9.5) |<span data-ttu-id="f5294-228">31 de janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="f5294-228">January 31, 2017</span></span> |--- |
| [<span data-ttu-id="f5294-229">1.9.4</span><span class="sxs-lookup"><span data-stu-id="f5294-229">1.9.4</span></span>](#1.9.4) |<span data-ttu-id="f5294-230">24 de novembro de 2016</span><span class="sxs-lookup"><span data-stu-id="f5294-230">November 24, 2016</span></span> |--- |
| [<span data-ttu-id="f5294-231">1.9.3</span><span class="sxs-lookup"><span data-stu-id="f5294-231">1.9.3</span></span>](#1.9.3) |<span data-ttu-id="f5294-232">30 de outubro de 2016</span><span class="sxs-lookup"><span data-stu-id="f5294-232">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="f5294-233">1.9.2</span><span class="sxs-lookup"><span data-stu-id="f5294-233">1.9.2</span></span>](#1.9.2) |<span data-ttu-id="f5294-234">28 de outubro de 2016</span><span class="sxs-lookup"><span data-stu-id="f5294-234">October 28, 2016</span></span> |--- |
| [<span data-ttu-id="f5294-235">1.9.1</span><span class="sxs-lookup"><span data-stu-id="f5294-235">1.9.1</span></span>](#1.9.1) |<span data-ttu-id="f5294-236">26 de outubro de 2016</span><span class="sxs-lookup"><span data-stu-id="f5294-236">October 26, 2016</span></span> |--- |
| [<span data-ttu-id="f5294-237">1.9.0</span><span class="sxs-lookup"><span data-stu-id="f5294-237">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="f5294-238">3 de outubro de 2016</span><span class="sxs-lookup"><span data-stu-id="f5294-238">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="f5294-239">1.8.1</span><span class="sxs-lookup"><span data-stu-id="f5294-239">1.8.1</span></span>](#1.8.1) |<span data-ttu-id="f5294-240">30 de junho de 2016</span><span class="sxs-lookup"><span data-stu-id="f5294-240">June 30, 2016</span></span> |--- |
| [<span data-ttu-id="f5294-241">1.8.0</span><span class="sxs-lookup"><span data-stu-id="f5294-241">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="f5294-242">14 de junho de 2016</span><span class="sxs-lookup"><span data-stu-id="f5294-242">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="f5294-243">1.7.1</span><span class="sxs-lookup"><span data-stu-id="f5294-243">1.7.1</span></span>](#1.7.1) |<span data-ttu-id="f5294-244">30 de abril de 2016</span><span class="sxs-lookup"><span data-stu-id="f5294-244">April 30, 2016</span></span> |--- |
| [<span data-ttu-id="f5294-245">1.7.0</span><span class="sxs-lookup"><span data-stu-id="f5294-245">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="f5294-246">27 de abril de 2016</span><span class="sxs-lookup"><span data-stu-id="f5294-246">April 27, 2016</span></span> |--- |
| [<span data-ttu-id="f5294-247">1.6.0</span><span class="sxs-lookup"><span data-stu-id="f5294-247">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="f5294-248">29 de março de 2016</span><span class="sxs-lookup"><span data-stu-id="f5294-248">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="f5294-249">1.5.1</span><span class="sxs-lookup"><span data-stu-id="f5294-249">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="f5294-250">31 de dezembro de 2015</span><span class="sxs-lookup"><span data-stu-id="f5294-250">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="f5294-251">1.5.0</span><span class="sxs-lookup"><span data-stu-id="f5294-251">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="f5294-252">4 de dezembro de 2015</span><span class="sxs-lookup"><span data-stu-id="f5294-252">December 04, 2015</span></span> |--- |
| [<span data-ttu-id="f5294-253">1.4.0</span><span class="sxs-lookup"><span data-stu-id="f5294-253">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="f5294-254">5 de outubro de 2015</span><span class="sxs-lookup"><span data-stu-id="f5294-254">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="f5294-255">1.3.0</span><span class="sxs-lookup"><span data-stu-id="f5294-255">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="f5294-256">5 de outubro de 2015</span><span class="sxs-lookup"><span data-stu-id="f5294-256">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="f5294-257">1.2.0</span><span class="sxs-lookup"><span data-stu-id="f5294-257">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="f5294-258">5 de agosto de 2015</span><span class="sxs-lookup"><span data-stu-id="f5294-258">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="f5294-259">1.1.0</span><span class="sxs-lookup"><span data-stu-id="f5294-259">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="f5294-260">9 de julho de 2015</span><span class="sxs-lookup"><span data-stu-id="f5294-260">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="f5294-261">1.0.1</span><span class="sxs-lookup"><span data-stu-id="f5294-261">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="f5294-262">12 de maio de 2015</span><span class="sxs-lookup"><span data-stu-id="f5294-262">May 12, 2015</span></span> |--- |
| [<span data-ttu-id="f5294-263">1.0.0</span><span class="sxs-lookup"><span data-stu-id="f5294-263">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="f5294-264">7 de abril de 2015</span><span class="sxs-lookup"><span data-stu-id="f5294-264">April 07, 2015</span></span> |--- |
| <span data-ttu-id="f5294-265">0.9.5-prelease</span><span class="sxs-lookup"><span data-stu-id="f5294-265">0.9.5-prelease</span></span> |<span data-ttu-id="f5294-266">9 de março de 2015</span><span class="sxs-lookup"><span data-stu-id="f5294-266">Mar 09, 2015</span></span> |<span data-ttu-id="f5294-267">29 de fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="f5294-267">February 29, 2016</span></span> |
| <span data-ttu-id="f5294-268">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="f5294-268">0.9.4-prelease</span></span> |<span data-ttu-id="f5294-269">17 de fevereiro de 2015</span><span class="sxs-lookup"><span data-stu-id="f5294-269">February 17, 2015</span></span> |<span data-ttu-id="f5294-270">29 de fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="f5294-270">February 29, 2016</span></span> |
| <span data-ttu-id="f5294-271">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="f5294-271">0.9.3-prelease</span></span> |<span data-ttu-id="f5294-272">13 de janeiro de 2015</span><span class="sxs-lookup"><span data-stu-id="f5294-272">January 13, 2015</span></span> |<span data-ttu-id="f5294-273">29 de fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="f5294-273">February 29, 2016</span></span> |
| <span data-ttu-id="f5294-274">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="f5294-274">0.9.2-prelease</span></span> |<span data-ttu-id="f5294-275">19 de dezembro de 2014</span><span class="sxs-lookup"><span data-stu-id="f5294-275">December 19, 2014</span></span> |<span data-ttu-id="f5294-276">29 de fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="f5294-276">February 29, 2016</span></span> |
| <span data-ttu-id="f5294-277">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="f5294-277">0.9.1-prelease</span></span> |<span data-ttu-id="f5294-278">19 de dezembro de 2014</span><span class="sxs-lookup"><span data-stu-id="f5294-278">December 19, 2014</span></span> |<span data-ttu-id="f5294-279">29 de fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="f5294-279">February 29, 2016</span></span> |
| <span data-ttu-id="f5294-280">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="f5294-280">0.9.0-prelease</span></span> |<span data-ttu-id="f5294-281">10 de dezembro de 2014</span><span class="sxs-lookup"><span data-stu-id="f5294-281">December 10, 2014</span></span> |<span data-ttu-id="f5294-282">29 de fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="f5294-282">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="f5294-283">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="f5294-283">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="f5294-284">Consulte também</span><span class="sxs-lookup"><span data-stu-id="f5294-284">See Also</span></span>
<span data-ttu-id="f5294-285">Para saber mais sobre o Cosmos DB, consulte a página de serviço do [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="f5294-285">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

