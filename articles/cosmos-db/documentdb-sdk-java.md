---
title: 'Azure Cosmos DB: API, SDK e recursos em Java do DocumentDB, | Microsoft Docs'
description: "Saiba tudo sobre Olá API Java e o SDK, incluindo datas de lançamento, datas de desativação e as alterações feitas entre cada versão do hello Azure Cosmos DB documentos Java SDK."
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
ms.openlocfilehash: 8ef43ebeb7ae1bfc55512c4a7489c1b7930122d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-java-sdk-release-notes-and-resources"></a><span data-ttu-id="4cfd5-103">Azure Cosmos DB: notas de versão e recursos do SDK Java do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="4cfd5-103">Azure Cosmos DB: DocumentDB Java SDK release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4cfd5-104">.NET</span><span class="sxs-lookup"><span data-stu-id="4cfd5-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="4cfd5-105">Feed de alterações do .NET</span><span class="sxs-lookup"><span data-stu-id="4cfd5-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="4cfd5-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="4cfd5-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="4cfd5-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="4cfd5-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="4cfd5-108">Java</span><span class="sxs-lookup"><span data-stu-id="4cfd5-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="4cfd5-109">Python</span><span class="sxs-lookup"><span data-stu-id="4cfd5-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="4cfd5-110">REST</span><span class="sxs-lookup"><span data-stu-id="4cfd5-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="4cfd5-111">Provedor de recursos REST</span><span class="sxs-lookup"><span data-stu-id="4cfd5-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="4cfd5-112">SQL</span><span class="sxs-lookup"><span data-stu-id="4cfd5-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="4cfd5-113">**Baixe o SDK**</span><span class="sxs-lookup"><span data-stu-id="4cfd5-113">**SDK Download**</span></span></td><td>[<span data-ttu-id="4cfd5-114">Maven</span><span class="sxs-lookup"><span data-stu-id="4cfd5-114">Maven</span></span>](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-documentdb%22)</td></tr>

<tr><td><span data-ttu-id="4cfd5-115">**Documentação da API**</span><span class="sxs-lookup"><span data-stu-id="4cfd5-115">**API documentation**</span></span></td><td>[<span data-ttu-id="4cfd5-116">Documentação de referência de API Java</span><span class="sxs-lookup"><span data-stu-id="4cfd5-116">Java API reference documentation</span></span>](/java/api/com.microsoft.azure.documentdb)</td></tr>

<tr><td><span data-ttu-id="4cfd5-117">**Contribuir tooSDK**</span><span class="sxs-lookup"><span data-stu-id="4cfd5-117">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="4cfd5-118">GitHub</span><span class="sxs-lookup"><span data-stu-id="4cfd5-118">GitHub</span></span>](https://github.com/Azure/azure-documentdb-java/)</td></tr>

<tr><td><span data-ttu-id="4cfd5-119">**Introdução**</span><span class="sxs-lookup"><span data-stu-id="4cfd5-119">**Get started**</span></span></td><td>[<span data-ttu-id="4cfd5-120">Introdução ao SDK do Java de saudação</span><span class="sxs-lookup"><span data-stu-id="4cfd5-120">Get started with hello Java SDK</span></span>](documentdb-java-get-started.md)</td></tr>

<tr><td><span data-ttu-id="4cfd5-121">**Tutorial do aplicativo Web**</span><span class="sxs-lookup"><span data-stu-id="4cfd5-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="4cfd5-122">Desenvolvimento de aplicativos Web com o Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="4cfd5-122">Web application development with Azure Cosmos DB</span></span>](documentdb-java-application.md)</td></tr>

<tr><td><span data-ttu-id="4cfd5-123">**Tempo de execução atual com suporte**</span><span class="sxs-lookup"><span data-stu-id="4cfd5-123">**Current supported runtime**</span></span></td><td>[<span data-ttu-id="4cfd5-124">JDK 7</span><span class="sxs-lookup"><span data-stu-id="4cfd5-124">JDK 7</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="4cfd5-125">Notas de versão</span><span class="sxs-lookup"><span data-stu-id="4cfd5-125">Release Notes</span></span>

### <a name="a-name11201120"></a><span data-ttu-id="4cfd5-126"><a name="1.12.0"/>1.12.0</span><span class="sxs-lookup"><span data-stu-id="4cfd5-126"><a name="1.12.0"/>1.12.0</span></span>
* <span data-ttu-id="4cfd5-127">Divide toorequest correções de bugs críticos de processamento durante a partição.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-127">Critical bug fixes toorequest processing during partition splits.</span></span>
* <span data-ttu-id="4cfd5-128">Corrigido um problema com hello forte e BoundedStaleness níveis de consistência.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-128">Fixed an issue with hello Strong and BoundedStaleness consistency levels.</span></span>

### <a name="a-name11101110"></a><span data-ttu-id="4cfd5-129"><a name="1.11.0"/>1.11.0</span><span class="sxs-lookup"><span data-stu-id="4cfd5-129"><a name="1.11.0"/>1.11.0</span></span>
* <span data-ttu-id="4cfd5-130">Adição de suporte a um novo nível de consistência chamado ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-130">Added support for a new consistency level called ConsistentPrefix.</span></span>
* <span data-ttu-id="4cfd5-131">Corrigido um bug na leitura da coleção no modo de sessão.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-131">Fixed a bug in reading collection in session mode.</span></span>

### <a name="a-name11001100"></a><span data-ttu-id="4cfd5-132"><a name="1.10.0"/>1.10.0</span><span class="sxs-lookup"><span data-stu-id="4cfd5-132"><a name="1.10.0"/>1.10.0</span></span>
* <span data-ttu-id="4cfd5-133">Suporte habilitado para coleção particionada com 2.500 RU/s e escala em incrementos de 100 RU/s.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-133">Enabled support for partitioned collection with as low as 2,500 RU/sec and scale in increments of 100 RU/sec.</span></span>
* <span data-ttu-id="4cfd5-134">Correção de bug no assembly nativo hello, que pode causar exceção NullRef em algumas consultas.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-134">Fixed a bug in hello native assembly which can cause NullRef exception in some queries.</span></span>

### <a name="a-name196196"></a><span data-ttu-id="4cfd5-135"><a name="1.9.6"/>1.9.6</span><span class="sxs-lookup"><span data-stu-id="4cfd5-135"><a name="1.9.6"/>1.9.6</span></span>
* <span data-ttu-id="4cfd5-136">Correção de bug na configuração do mecanismo de consulta Olá que pode causar exceções para consultas no modo de Gateway.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-136">Fixed a bug in hello query engine configuration that may cause exceptions for queries in Gateway mode.</span></span>
* <span data-ttu-id="4cfd5-137">Corrigidos alguns bugs no contêiner de sessão Olá que podem causar uma exceção "Recurso proprietário não encontrado" de solicitações imediatamente após a criação de coleção.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-137">Fixed a few bugs in hello session container that may cause an "Owner resource not found" exception for requests immediately after collection creation.</span></span>

### <a name="a-name195195"></a><span data-ttu-id="4cfd5-138"><a name="1.9.5"/>1.9.5</span><span class="sxs-lookup"><span data-stu-id="4cfd5-138"><a name="1.9.5"/>1.9.5</span></span>
* <span data-ttu-id="4cfd5-139">Suporte adicionado para consultas de agregação (COUNT, MIN, MAX, SUM e AVG).</span><span class="sxs-lookup"><span data-stu-id="4cfd5-139">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="4cfd5-140">Veja [Suporte de agregação](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="4cfd5-140">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="4cfd5-141">Adicionado suporte para alteração de feed.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-141">Added support for change feed.</span></span>
* <span data-ttu-id="4cfd5-142">Adicionado suporte para informações de cota de coleção por meio de RequestOptions.setPopulateQuotaInfo.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-142">Added support for collection quota information through RequestOptions.setPopulateQuotaInfo.</span></span>
* <span data-ttu-id="4cfd5-143">Foi adicionado suporte para o log de script de procedimento armazenado por meio de RequestOptions.setScriptLoggingEnabled.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-143">Added support for stored procedure script logging through RequestOptions.setScriptLoggingEnabled.</span></span>
* <span data-ttu-id="4cfd5-144">Corrigido um bug em que a consulta no modo de DirectHttps pode travar ao encontrar falhas de limitação.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-144">Fixed a bug where query in DirectHttps mode may hang when encountering throttle failures.</span></span>
* <span data-ttu-id="4cfd5-145">Corrigido um bug no modo de sessão de consistência.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-145">Fixed a bug in session consistency mode.</span></span>
* <span data-ttu-id="4cfd5-146">Corrigido um erro que pode causar a NullReferenceException no HttpContext quando a taxa de solicitação é alta.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-146">Fixed a bug which may cause NullReferenceException in HttpContext when request rate is high.</span></span>
* <span data-ttu-id="4cfd5-147">Desempenho aprimorado de modo DirectHttps.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-147">Improved performance of DirectHttps mode.</span></span>

### <a name="a-name194194"></a><span data-ttu-id="4cfd5-148"><a name="1.9.4"/>1.9.4</span><span class="sxs-lookup"><span data-stu-id="4cfd5-148"><a name="1.9.4"/>1.9.4</span></span>
* <span data-ttu-id="4cfd5-149">Acréscimo de suporte a proxy com base em instância simples do cliente com API ConnectionPolicy.setProxy().</span><span class="sxs-lookup"><span data-stu-id="4cfd5-149">Added simple client instance-based proxy support with ConnectionPolicy.setProxy() API.</span></span>
* <span data-ttu-id="4cfd5-150">Adicionado DocumentClient.close() tooproperly desligamento DocumentClient instância da API.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-150">Added DocumentClient.close() API tooproperly shutdown DocumentClient instance.</span></span>
* <span data-ttu-id="4cfd5-151">Desempenho aprimorado de consultas no modo de conectividade direta derivando plano de consulta de saudação do assembly nativo de saudação em vez da saudação Gateway.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-151">Improved query performance in direct connectivity mode by deriving hello query plan from hello native assembly instead of hello Gateway.</span></span>
* <span data-ttu-id="4cfd5-152">Definir FAIL_ON_UNKNOWN_PROPERTIES = false para que os usuários não precisam toodefine JsonIgnoreProperties em seu POJO.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-152">Set FAIL_ON_UNKNOWN_PROPERTIES = false so users don't need toodefine JsonIgnoreProperties in their POJO.</span></span>
* <span data-ttu-id="4cfd5-153">Registro em log refatorado toouse SLF4J.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-153">Refactored logging toouse SLF4J.</span></span>
* <span data-ttu-id="4cfd5-154">Alguns outros bugs corrigidos no leitor de consistência.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-154">Fixed a few other bugs in consistency reader.</span></span>

### <a name="a-name193193"></a><span data-ttu-id="4cfd5-155"><a name="1.9.3"/>1.9.3</span><span class="sxs-lookup"><span data-stu-id="4cfd5-155"><a name="1.9.3"/>1.9.3</span></span>
* <span data-ttu-id="4cfd5-156">Correção de bug na conexão Olá gerenciamento perdas de conexão tooprevent no modo de conectividade direta.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-156">Fixed a bug in hello connection management tooprevent connection leaks in direct connectivity mode.</span></span>
* <span data-ttu-id="4cfd5-157">Correção de bug na consulta TOP Olá onde ele pode gerar exceção NullReferenece.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-157">Fixed a bug in hello TOP query where it may throw NullReferenece exception.</span></span>
* <span data-ttu-id="4cfd5-158">Melhor desempenho, reduzindo o número de saudação da chamada de rede de caches internos Olá.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-158">Improved performance by reducing hello number of network call for hello internal caches.</span></span>
* <span data-ttu-id="4cfd5-159">Acréscimo do código de status, ActivityID e URI de Solicitação em DocumentClientException para melhor solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-159">Added status code, ActivityID and Request URI in DocumentClientException for better troubleshooting.</span></span>

### <a name="a-name192192"></a><span data-ttu-id="4cfd5-160"><a name="1.9.2"/>1.9.2</span><span class="sxs-lookup"><span data-stu-id="4cfd5-160"><a name="1.9.2"/>1.9.2</span></span>
* <span data-ttu-id="4cfd5-161">Corrigido um problema no gerenciamento de conexão de saudação de estabilidade.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-161">Fixed an issue in hello connection management for stability.</span></span>

### <a name="a-name191191"></a><span data-ttu-id="4cfd5-162"><a name="1.9.1"/>1.9.1</span><span class="sxs-lookup"><span data-stu-id="4cfd5-162"><a name="1.9.1"/>1.9.1</span></span>
* <span data-ttu-id="4cfd5-163">Adicionado suporte para o nível de consistência BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-163">Added support for BoundedStaleness consistency level.</span></span>
* <span data-ttu-id="4cfd5-164">Adicionado suporte para conectividade direta para operações CRUD para coleções particionadas.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-164">Added support for direct connectivity for CRUD operations for partitioned collections.</span></span>
* <span data-ttu-id="4cfd5-165">Corrigido um erro na consulta de um banco de dados com SQL.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-165">Fixed a bug in querying a database with SQL.</span></span>
* <span data-ttu-id="4cfd5-166">Correção de bug no cache de sessão Olá onde o token de sessão pode ser definido incorretamente.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-166">Fixed a bug in hello session cache where session token may be set incorrectly.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="4cfd5-167"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="4cfd5-167"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="4cfd5-168">Adicionado suporte para várias consultas paralelas de partição.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-168">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="4cfd5-169">Adição de suporte a consultas TOP/ORDER BY de coleções particionadas.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-169">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>
* <span data-ttu-id="4cfd5-170">Adicionado suporte para consistência forte.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-170">Added support for strong consistency.</span></span>
* <span data-ttu-id="4cfd5-171">Adicionado suporte para solicitações com base em nome ao usar a conectividade direta.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-171">Added support for name based requests when using direct connectivity.</span></span>
* <span data-ttu-id="4cfd5-172">Toomake fixa ActivityId permanecer consistente em todas as tentativas de solicitação.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-172">Fixed toomake ActivityId stay consistent across all request retries.</span></span>
* <span data-ttu-id="4cfd5-173">Correção de bug relacionado toohello cache de sessão ao recriar uma coleção com hello mesmo nome.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-173">Fixed a bug related toohello session cache when recreating a collection with hello same name.</span></span>
* <span data-ttu-id="4cfd5-174">Adicionado Polygon e LineString DataTypes ao especificar a política de indexação de coleção para consultas espaciais de isolamento geográfico.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-174">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span></span>
* <span data-ttu-id="4cfd5-175">Problemas corrigidos com Java Doc para Java 1.8.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-175">Fixed issues with Java Doc for Java 1.8.</span></span>

### <a name="a-name181181"></a><span data-ttu-id="4cfd5-176"><a name="1.8.1"/>1.8.1</span><span class="sxs-lookup"><span data-stu-id="4cfd5-176"><a name="1.8.1"/>1.8.1</span></span>
* <span data-ttu-id="4cfd5-177">Correção de bug no PartitionKeyDefinitionMap toocache coleções de partição única e não fazer extra buscar partição solicitações de chave.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-177">Fixed a bug in PartitionKeyDefinitionMap toocache single partition collections and not make extra fetch partition key requests.</span></span>
* <span data-ttu-id="4cfd5-178">Corrigido uma repetição do bug toonot quando é fornecido um valor de chave de partição incorreto.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-178">Fixed a bug toonot retry when an incorrect partition key value is provided.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="4cfd5-179"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="4cfd5-179"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="4cfd5-180">Suporte adicionado Olá para contas do banco de dados de várias regiões.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-180">Added hello support for multi-region database accounts.</span></span>
* <span data-ttu-id="4cfd5-181">Adicionado suporte para repetição automática em solicitações limitadas com hello de toocustomize opções max tentativas e repita máx de tempo de espera.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-181">Added support for automatic retry on throttled requests with options toocustomize hello max retry attempts and max retry wait time.</span></span>  <span data-ttu-id="4cfd5-182">Consulte RetryOptions e ConnectionPolicy.getRetryOptions().</span><span class="sxs-lookup"><span data-stu-id="4cfd5-182">See RetryOptions and ConnectionPolicy.getRetryOptions().</span></span>
* <span data-ttu-id="4cfd5-183">IPartitionResolver preterido com base no código de particionamento personalizado.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-183">Deprecated IPartitionResolver based custom partitioning code.</span></span> <span data-ttu-id="4cfd5-184">Use coleções particionadas para uma taxa de transferência e armazenamento superiores.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-184">Please use partitioned collections for higher storage and throughput.</span></span>

### <a name="a-name171171"></a><span data-ttu-id="4cfd5-185"><a name="1.7.1"/>1.7.1</span><span class="sxs-lookup"><span data-stu-id="4cfd5-185"><a name="1.7.1"/>1.7.1</span></span>
* <span data-ttu-id="4cfd5-186">Adicionado suporte à política de repetição para limitação.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-186">Added retry policy support for throttling.</span></span>  

### <a name="a-name170170"></a><span data-ttu-id="4cfd5-187"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="4cfd5-187"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="4cfd5-188">Adicionado suporte para documentos em tempo de toolive (TTL).</span><span class="sxs-lookup"><span data-stu-id="4cfd5-188">Added time toolive (TTL) support for documents.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="4cfd5-189"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="4cfd5-189"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="4cfd5-190">Implementação de [coleções particionadas](partition-data.md) e [níveis de desempenho definidos pelo usuário](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="4cfd5-190">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <a name="a-name151151"></a><span data-ttu-id="4cfd5-191"><a name="1.5.1"/>1.5.1</span><span class="sxs-lookup"><span data-stu-id="4cfd5-191"><a name="1.5.1"/>1.5.1</span></span>
* <span data-ttu-id="4cfd5-192">Correção de bug em valores de hash toogenerate HashPartitionResolver em little endian toobe consistente com outros SDKs.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-192">Fixed a bug in HashPartitionResolver toogenerate hash values in little-endian toobe consistent with other SDKs.</span></span>

### <a name="a-name150150"></a><span data-ttu-id="4cfd5-193"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="4cfd5-193"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="4cfd5-194">Adicionar & intervalo de Hash tooassist de resolvedores de partição com aplicativos de fragmentação por várias partições.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-194">Add Hash & Range partition resolvers tooassist with sharding applications across multiple partitions.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="4cfd5-195"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="4cfd5-195"><a name="1.4.0"/>1.4.0</span></span>
* <span data-ttu-id="4cfd5-196">Implementar o Upsert.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-196">Implement Upsert.</span></span> <span data-ttu-id="4cfd5-197">Novos métodos upsertXXX adicionaram toosupport Upsert recurso.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-197">New upsertXXX methods added toosupport Upsert feature.</span></span>
* <span data-ttu-id="4cfd5-198">Implementar o roteamento com base em ID.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-198">Implement ID Based Routing.</span></span> <span data-ttu-id="4cfd5-199">Nenhuma alteração pública de API, todas as alterações são internas.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-199">No public API changes, all changes internal.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="4cfd5-200"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="4cfd5-200"><a name="1.3.0"/>1.3.0</span></span>
* <span data-ttu-id="4cfd5-201">Versão ignorada toobring o número de versão no alinhamento com outros SDKs</span><span class="sxs-lookup"><span data-stu-id="4cfd5-201">Release skipped toobring version number in alignment with other SDKs</span></span>

### <a name="a-name120120"></a><span data-ttu-id="4cfd5-202"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="4cfd5-202"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="4cfd5-203">Oferece suporte ao Índice Geoespacial.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-203">Supports GeoSpatial Index</span></span>
* <span data-ttu-id="4cfd5-204">Valida a propriedade de ID de todos os recursos.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-204">Validates id property for all resources.</span></span> <span data-ttu-id="4cfd5-205">As IDs de recursos não podem conter caracteres ?, /, #, \, ou terminar com um espaço.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-205">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="4cfd5-206">Adiciona novo tooResourceResponse "andamento de transformação de índice" de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-206">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="4cfd5-207"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="4cfd5-207"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="4cfd5-208">Implementa a política de indexação V2</span><span class="sxs-lookup"><span data-stu-id="4cfd5-208">Implements V2 indexing policy</span></span>

### <a name="a-name100100"></a><span data-ttu-id="4cfd5-209"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="4cfd5-209"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="4cfd5-210">SDK DO GA</span><span class="sxs-lookup"><span data-stu-id="4cfd5-210">GA SDK</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="4cfd5-211">Datas de lançamento e desativação</span><span class="sxs-lookup"><span data-stu-id="4cfd5-211">Release & Retirement Dates</span></span>
<span data-ttu-id="4cfd5-212">A Microsoft fornecerá notificação pelo menos **12 meses** antes de desativar um SDK na versão mais recente/suporte ordem toosmooth Olá transição tooa.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-212">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="4cfd5-213">Novos recursos e funcionalidade e as otimizações são adicionadas apenas toohello atual SDK, como tal, é recomendável que você sempre atualize toohello mais recente versão do SDK mais cedo possível.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-213">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommend that you always upgrade toohello latest SDK version as early as possible.</span></span>

<span data-ttu-id="4cfd5-214">TooCosmos qualquer solicitação usando um SDK obsoleto do banco de dados serão rejeitados pelo serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-214">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

> [!WARNING]
> <span data-ttu-id="4cfd5-215">Todas as versões do hello SDK do DocumentDB para tooversion anterior Java **1.0.0** será desativado em **29 de fevereiro de 2016**.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-215">All versions of hello DocumentDB SDK for Java prior tooversion **1.0.0** will be retired on **February 29, 2016**.</span></span>
> 
> 

<br/>

| <span data-ttu-id="4cfd5-216">Versão</span><span class="sxs-lookup"><span data-stu-id="4cfd5-216">Version</span></span> | <span data-ttu-id="4cfd5-217">Data do lançamento</span><span class="sxs-lookup"><span data-stu-id="4cfd5-217">Release Date</span></span> | <span data-ttu-id="4cfd5-218">Data de desativação</span><span class="sxs-lookup"><span data-stu-id="4cfd5-218">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="4cfd5-219">1.12.0</span><span class="sxs-lookup"><span data-stu-id="4cfd5-219">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="4cfd5-220">11 de julho de 2017</span><span class="sxs-lookup"><span data-stu-id="4cfd5-220">July 11, 2017</span></span> |--- |
| [<span data-ttu-id="4cfd5-221">1.11.0</span><span class="sxs-lookup"><span data-stu-id="4cfd5-221">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="4cfd5-222">10 de maio de 2017</span><span class="sxs-lookup"><span data-stu-id="4cfd5-222">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="4cfd5-223">1.10.0</span><span class="sxs-lookup"><span data-stu-id="4cfd5-223">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="4cfd5-224">11 de março de 2017</span><span class="sxs-lookup"><span data-stu-id="4cfd5-224">March 11, 2017</span></span> |--- |
| [<span data-ttu-id="4cfd5-225">1.9.6</span><span class="sxs-lookup"><span data-stu-id="4cfd5-225">1.9.6</span></span>](#1.9.6) |<span data-ttu-id="4cfd5-226">21 de fevereiro de 2017</span><span class="sxs-lookup"><span data-stu-id="4cfd5-226">February 21, 2017</span></span> |--- |
| [<span data-ttu-id="4cfd5-227">1.9.5</span><span class="sxs-lookup"><span data-stu-id="4cfd5-227">1.9.5</span></span>](#1.9.5) |<span data-ttu-id="4cfd5-228">31 de janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="4cfd5-228">January 31, 2017</span></span> |--- |
| [<span data-ttu-id="4cfd5-229">1.9.4</span><span class="sxs-lookup"><span data-stu-id="4cfd5-229">1.9.4</span></span>](#1.9.4) |<span data-ttu-id="4cfd5-230">24 de novembro de 2016</span><span class="sxs-lookup"><span data-stu-id="4cfd5-230">November 24, 2016</span></span> |--- |
| [<span data-ttu-id="4cfd5-231">1.9.3</span><span class="sxs-lookup"><span data-stu-id="4cfd5-231">1.9.3</span></span>](#1.9.3) |<span data-ttu-id="4cfd5-232">30 de outubro de 2016</span><span class="sxs-lookup"><span data-stu-id="4cfd5-232">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="4cfd5-233">1.9.2</span><span class="sxs-lookup"><span data-stu-id="4cfd5-233">1.9.2</span></span>](#1.9.2) |<span data-ttu-id="4cfd5-234">28 de outubro de 2016</span><span class="sxs-lookup"><span data-stu-id="4cfd5-234">October 28, 2016</span></span> |--- |
| [<span data-ttu-id="4cfd5-235">1.9.1</span><span class="sxs-lookup"><span data-stu-id="4cfd5-235">1.9.1</span></span>](#1.9.1) |<span data-ttu-id="4cfd5-236">26 de outubro de 2016</span><span class="sxs-lookup"><span data-stu-id="4cfd5-236">October 26, 2016</span></span> |--- |
| [<span data-ttu-id="4cfd5-237">1.9.0</span><span class="sxs-lookup"><span data-stu-id="4cfd5-237">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="4cfd5-238">3 de outubro de 2016</span><span class="sxs-lookup"><span data-stu-id="4cfd5-238">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="4cfd5-239">1.8.1</span><span class="sxs-lookup"><span data-stu-id="4cfd5-239">1.8.1</span></span>](#1.8.1) |<span data-ttu-id="4cfd5-240">30 de junho de 2016</span><span class="sxs-lookup"><span data-stu-id="4cfd5-240">June 30, 2016</span></span> |--- |
| [<span data-ttu-id="4cfd5-241">1.8.0</span><span class="sxs-lookup"><span data-stu-id="4cfd5-241">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="4cfd5-242">14 de junho de 2016</span><span class="sxs-lookup"><span data-stu-id="4cfd5-242">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="4cfd5-243">1.7.1</span><span class="sxs-lookup"><span data-stu-id="4cfd5-243">1.7.1</span></span>](#1.7.1) |<span data-ttu-id="4cfd5-244">30 de abril de 2016</span><span class="sxs-lookup"><span data-stu-id="4cfd5-244">April 30, 2016</span></span> |--- |
| [<span data-ttu-id="4cfd5-245">1.7.0</span><span class="sxs-lookup"><span data-stu-id="4cfd5-245">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="4cfd5-246">27 de abril de 2016</span><span class="sxs-lookup"><span data-stu-id="4cfd5-246">April 27, 2016</span></span> |--- |
| [<span data-ttu-id="4cfd5-247">1.6.0</span><span class="sxs-lookup"><span data-stu-id="4cfd5-247">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="4cfd5-248">29 de março de 2016</span><span class="sxs-lookup"><span data-stu-id="4cfd5-248">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="4cfd5-249">1.5.1</span><span class="sxs-lookup"><span data-stu-id="4cfd5-249">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="4cfd5-250">31 de dezembro de 2015</span><span class="sxs-lookup"><span data-stu-id="4cfd5-250">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="4cfd5-251">1.5.0</span><span class="sxs-lookup"><span data-stu-id="4cfd5-251">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="4cfd5-252">4 de dezembro de 2015</span><span class="sxs-lookup"><span data-stu-id="4cfd5-252">December 04, 2015</span></span> |--- |
| [<span data-ttu-id="4cfd5-253">1.4.0</span><span class="sxs-lookup"><span data-stu-id="4cfd5-253">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="4cfd5-254">5 de outubro de 2015</span><span class="sxs-lookup"><span data-stu-id="4cfd5-254">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="4cfd5-255">1.3.0</span><span class="sxs-lookup"><span data-stu-id="4cfd5-255">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="4cfd5-256">5 de outubro de 2015</span><span class="sxs-lookup"><span data-stu-id="4cfd5-256">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="4cfd5-257">1.2.0</span><span class="sxs-lookup"><span data-stu-id="4cfd5-257">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="4cfd5-258">5 de agosto de 2015</span><span class="sxs-lookup"><span data-stu-id="4cfd5-258">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="4cfd5-259">1.1.0</span><span class="sxs-lookup"><span data-stu-id="4cfd5-259">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="4cfd5-260">9 de julho de 2015</span><span class="sxs-lookup"><span data-stu-id="4cfd5-260">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="4cfd5-261">1.0.1</span><span class="sxs-lookup"><span data-stu-id="4cfd5-261">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="4cfd5-262">12 de maio de 2015</span><span class="sxs-lookup"><span data-stu-id="4cfd5-262">May 12, 2015</span></span> |--- |
| [<span data-ttu-id="4cfd5-263">1.0.0</span><span class="sxs-lookup"><span data-stu-id="4cfd5-263">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="4cfd5-264">7 de abril de 2015</span><span class="sxs-lookup"><span data-stu-id="4cfd5-264">April 07, 2015</span></span> |--- |
| <span data-ttu-id="4cfd5-265">0.9.5-prelease</span><span class="sxs-lookup"><span data-stu-id="4cfd5-265">0.9.5-prelease</span></span> |<span data-ttu-id="4cfd5-266">9 de março de 2015</span><span class="sxs-lookup"><span data-stu-id="4cfd5-266">Mar 09, 2015</span></span> |<span data-ttu-id="4cfd5-267">29 de fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="4cfd5-267">February 29, 2016</span></span> |
| <span data-ttu-id="4cfd5-268">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="4cfd5-268">0.9.4-prelease</span></span> |<span data-ttu-id="4cfd5-269">17 de fevereiro de 2015</span><span class="sxs-lookup"><span data-stu-id="4cfd5-269">February 17, 2015</span></span> |<span data-ttu-id="4cfd5-270">29 de fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="4cfd5-270">February 29, 2016</span></span> |
| <span data-ttu-id="4cfd5-271">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="4cfd5-271">0.9.3-prelease</span></span> |<span data-ttu-id="4cfd5-272">13 de janeiro de 2015</span><span class="sxs-lookup"><span data-stu-id="4cfd5-272">January 13, 2015</span></span> |<span data-ttu-id="4cfd5-273">29 de fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="4cfd5-273">February 29, 2016</span></span> |
| <span data-ttu-id="4cfd5-274">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="4cfd5-274">0.9.2-prelease</span></span> |<span data-ttu-id="4cfd5-275">19 de dezembro de 2014</span><span class="sxs-lookup"><span data-stu-id="4cfd5-275">December 19, 2014</span></span> |<span data-ttu-id="4cfd5-276">29 de fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="4cfd5-276">February 29, 2016</span></span> |
| <span data-ttu-id="4cfd5-277">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="4cfd5-277">0.9.1-prelease</span></span> |<span data-ttu-id="4cfd5-278">19 de dezembro de 2014</span><span class="sxs-lookup"><span data-stu-id="4cfd5-278">December 19, 2014</span></span> |<span data-ttu-id="4cfd5-279">29 de fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="4cfd5-279">February 29, 2016</span></span> |
| <span data-ttu-id="4cfd5-280">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="4cfd5-280">0.9.0-prelease</span></span> |<span data-ttu-id="4cfd5-281">10 de dezembro de 2014</span><span class="sxs-lookup"><span data-stu-id="4cfd5-281">December 10, 2014</span></span> |<span data-ttu-id="4cfd5-282">29 de fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="4cfd5-282">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="4cfd5-283">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="4cfd5-283">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="4cfd5-284">Consulte também</span><span class="sxs-lookup"><span data-stu-id="4cfd5-284">See Also</span></span>
<span data-ttu-id="4cfd5-285">toolearn mais sobre o banco de dados do Cosmos, consulte [banco de dados do Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) página de serviço.</span><span class="sxs-lookup"><span data-stu-id="4cfd5-285">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

