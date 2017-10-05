---
title: API do Python, SDK e recursos do Azure Cosmos DB | Microsoft Docs
description: "Saiba tudo sobre o SDK e a API do Python, incluindo datas de lançamento, datas de desativação e alterações feitas entre cada versão do SDK do Python para o Azure Cosmos DB."
services: cosmos-db
documentationcenter: python
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 3ac344a9-b2fa-4a3f-a4cc-02d287e05469
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/24/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70d2550f713ff0e9daed235eb8053589b8682633
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a><span data-ttu-id="3a951-103">SDK do Python do Azure Cosmos DB: notas de versão e recursos</span><span class="sxs-lookup"><span data-stu-id="3a951-103">Azure Cosmos DB Python SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3a951-104">.NET</span><span class="sxs-lookup"><span data-stu-id="3a951-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="3a951-105">Feed de alterações do .NET</span><span class="sxs-lookup"><span data-stu-id="3a951-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="3a951-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="3a951-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="3a951-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="3a951-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="3a951-108">Java</span><span class="sxs-lookup"><span data-stu-id="3a951-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="3a951-109">Python</span><span class="sxs-lookup"><span data-stu-id="3a951-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="3a951-110">REST</span><span class="sxs-lookup"><span data-stu-id="3a951-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="3a951-111">Provedor de recursos REST</span><span class="sxs-lookup"><span data-stu-id="3a951-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="3a951-112">SQL</span><span class="sxs-lookup"><span data-stu-id="3a951-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="3a951-113">**Baixar o SDK**</span><span class="sxs-lookup"><span data-stu-id="3a951-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="3a951-114">PyPI</span><span class="sxs-lookup"><span data-stu-id="3a951-114">PyPI</span></span>](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td><span data-ttu-id="3a951-115">**Documentação da API**</span><span class="sxs-lookup"><span data-stu-id="3a951-115">**API documentation**</span></span></td><td>[<span data-ttu-id="3a951-116">Documentação de referência da API do Python</span><span class="sxs-lookup"><span data-stu-id="3a951-116">Python API reference documentation</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td><span data-ttu-id="3a951-117">**Instruções de instalação do SDK**</span><span class="sxs-lookup"><span data-stu-id="3a951-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="3a951-118">Instruções de instalação do SDK do Python</span><span class="sxs-lookup"><span data-stu-id="3a951-118">Python SDK installation instructions</span></span>](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td><span data-ttu-id="3a951-119">**Contribuir para o SDK**</span><span class="sxs-lookup"><span data-stu-id="3a951-119">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="3a951-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="3a951-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td><span data-ttu-id="3a951-121">**Introdução**</span><span class="sxs-lookup"><span data-stu-id="3a951-121">**Get started**</span></span></td><td>[<span data-ttu-id="3a951-122">Introdução ao SDK do Python</span><span class="sxs-lookup"><span data-stu-id="3a951-122">Get started with the Python SDK</span></span>](documentdb-python-application.md)</td></tr>

<tr><td><span data-ttu-id="3a951-123">**Plataforma atual com suporte**</span><span class="sxs-lookup"><span data-stu-id="3a951-123">**Current supported platform**</span></span></td><td><span data-ttu-id="3a951-124">[Python 2.7](https://www.python.org/downloads/) e [Python 3.5](https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="3a951-124">[Python 2.7](https://www.python.org/downloads/) and [Python 3.5](https://www.python.org/downloads/)</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="3a951-125">Notas de versão</span><span class="sxs-lookup"><span data-stu-id="3a951-125">Release notes</span></span>
### <a name="a-name220220"></a><span data-ttu-id="3a951-126"><a name="2.2.0"/>2.2.0</span><span class="sxs-lookup"><span data-stu-id="3a951-126"><a name="2.2.0"/>2.2.0</span></span>
* <span data-ttu-id="3a951-127">Adição de suporte a um novo nível de consistência chamado ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="3a951-127">Added support for a new consistency level called ConsistentPrefix.</span></span>


### <a name="a-name210210"></a><span data-ttu-id="3a951-128"><a name="2.1.0"/>2.1.0</span><span class="sxs-lookup"><span data-stu-id="3a951-128"><a name="2.1.0"/>2.1.0</span></span>
* <span data-ttu-id="3a951-129">Suporte adicionado para consultas de agregação (COUNT, MIN, MAX, SUM e AVG).</span><span class="sxs-lookup"><span data-stu-id="3a951-129">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="3a951-130">Adição de uma opção para desabilitar a verificação do SSL quando executada no Emulador do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3a951-130">Added an option for disabling SSL verification when running against Cosmos DB Emulator.</span></span>
* <span data-ttu-id="3a951-131">Removida a restrição do módulo de solicitações dependentes para serem exatamente 2.10.0.</span><span class="sxs-lookup"><span data-stu-id="3a951-131">Removed the restriction of dependent requests module to be exactly 2.10.0.</span></span>
* <span data-ttu-id="3a951-132">Taxa de transferência mínima reduzida em coleções particionadas de 10.100 RU/s a 2500 RU/s.</span><span class="sxs-lookup"><span data-stu-id="3a951-132">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>
* <span data-ttu-id="3a951-133">Adicionado suporte para habilitar o registro em log de script durante a execução do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="3a951-133">Added support for enabling script logging during stored procedure execution.</span></span>
* <span data-ttu-id="3a951-134">Versão da API REST aumentado para '2017-01-19' nesta versão.</span><span class="sxs-lookup"><span data-stu-id="3a951-134">REST API version bumped to '2017-01-19' with this release.</span></span>

### <a name="a-name201201"></a><span data-ttu-id="3a951-135"><a name="2.0.1"/>2.0.1</span><span class="sxs-lookup"><span data-stu-id="3a951-135"><a name="2.0.1"/>2.0.1</span></span>
* <span data-ttu-id="3a951-136">Alterações editoriais feitas a comentários de documentação.</span><span class="sxs-lookup"><span data-stu-id="3a951-136">Made editorial changes to documentation comments.</span></span>

### <a name="a-name200200"></a><span data-ttu-id="3a951-137"><a name="2.0.0"/>2.0.0</span><span class="sxs-lookup"><span data-stu-id="3a951-137"><a name="2.0.0"/>2.0.0</span></span>
* <span data-ttu-id="3a951-138">Suporte ao Python 3.5 adicionado.</span><span class="sxs-lookup"><span data-stu-id="3a951-138">Added support for Python 3.5.</span></span>
* <span data-ttu-id="3a951-139">Suporte ao pool de conexões usando um módulo de solicitações adicionado.</span><span class="sxs-lookup"><span data-stu-id="3a951-139">Added support for connection pooling using a requests module.</span></span>
* <span data-ttu-id="3a951-140">Suporte à consistência da sessão adicionado.</span><span class="sxs-lookup"><span data-stu-id="3a951-140">Added support for session consistency.</span></span>
* <span data-ttu-id="3a951-141">Suporte às consultas TOP/ORDERBY de coleções particionadas adicionado.</span><span class="sxs-lookup"><span data-stu-id="3a951-141">Added support for TOP/ORDERBY queries for partitioned collections.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="3a951-142"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="3a951-142"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="3a951-143">Suporte à política de repetições para solicitações limitadas adicionado.</span><span class="sxs-lookup"><span data-stu-id="3a951-143">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="3a951-144">(As solicitações limitadas recebem uma exceção muito grande de taxa de solicitação, código de erro 429.) Por padrão, o Azure Cosmos DB tenta cada solicitação novamente nove vezes quando o código de erro 429 é encontrado, respeitando o tempo retryAfter no cabeçalho de resposta.</span><span class="sxs-lookup"><span data-stu-id="3a951-144">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring the retryAfter time in the response header.</span></span> <span data-ttu-id="3a951-145">Um intervalo de repetição fixo agora poderá ser definido como parte da propriedade RetryOptions no objeto ConnectionPolicy, se você quiser ignorar o tempo retryAfter retornado pelo servidor entre as repetições.</span><span class="sxs-lookup"><span data-stu-id="3a951-145">A fixed retry interval time can now be set as part of the RetryOptions property on the ConnectionPolicy object if you want to ignore the retryAfter time returned by server between the retries.</span></span> <span data-ttu-id="3a951-146">O Azure Cosmos DB agora aguarda um período máximo de 30 segundos para cada solicitação que está sendo limitada (independentemente da contagem de repetições) e retorna a resposta com o código de erro 429.</span><span class="sxs-lookup"><span data-stu-id="3a951-146">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns the response with error code 429.</span></span> <span data-ttu-id="3a951-147">Este tempo também pode ser substituído na propriedade RetryOptions, no objeto ConnectionPolicy.</span><span class="sxs-lookup"><span data-stu-id="3a951-147">This time can also be overriden in the RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="3a951-148">O Cosmos DB agora retorna x-ms-throttle-retry-count e x-ms-throttle-retry-wait-time-ms como os cabeçalhos de resposta em cada solicitação para indicar a contagem de repetições restritas e o tempo cumulativo que a solicitação aguardou entre as tentativas.</span><span class="sxs-lookup"><span data-stu-id="3a951-148">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as the response headers in every request to denote the throttle retry count and the cummulative time the request waited between the retries.</span></span>
* <span data-ttu-id="3a951-149">A classe RetryPolicy foi removida e a propriedade correspondente (retry_policy) foi exposta na classe document_client. Como alternativa, foi introduzida uma classe RetryOptions, expondo a propriedade RetryOptions na classe ConnectionPolicy, que pode ser usada para substituir algumas das opções de repetição padrão.</span><span class="sxs-lookup"><span data-stu-id="3a951-149">Removed the RetryPolicy class and the corresponding property (retry_policy) exposed on the document_client class and instead introduced a RetryOptions class exposing the RetryOptions property on ConnectionPolicy class that can be used to override some of the default retry options.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="3a951-150"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="3a951-150"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="3a951-151">Suporte adicionado para contas de banco de dados de várias regiões.</span><span class="sxs-lookup"><span data-stu-id="3a951-151">Added the support for multi-region database accounts.</span></span>

### <a name="a-name170170"></a><span data-ttu-id="3a951-152"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="3a951-152"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="3a951-153">Adicionado o suporte para o recurso TTL (tempo de vida) para documentos.</span><span class="sxs-lookup"><span data-stu-id="3a951-153">Added the support for Time To Live(TTL) feature for documents.</span></span>

### <a name="a-name161161"></a><span data-ttu-id="3a951-154"><a name="1.6.1"/>1.6.1</span><span class="sxs-lookup"><span data-stu-id="3a951-154"><a name="1.6.1"/>1.6.1</span></span>
* <span data-ttu-id="3a951-155">Correções de bugs relacionadas ao particionamento no lado do servidor a fim de permitir caracteres especiais no caminho de partitionkey.</span><span class="sxs-lookup"><span data-stu-id="3a951-155">Bug fixes related to server side partitioning to allow special characters in partitionkey path.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="3a951-156"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="3a951-156"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="3a951-157">Implementação de [coleções particionadas](partition-data.md) e [níveis de desempenho definidos pelo usuário](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="3a951-157">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span> 

### <a name="a-name150150"></a><span data-ttu-id="3a951-158"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="3a951-158"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="3a951-159">Adicionar resolvedores de hash e intervalo para ajudar com a fragmentação de arquivos em várias partições.</span><span class="sxs-lookup"><span data-stu-id="3a951-159">Add Hash & Range partition resolvers to assist with sharding applications across multiple partitions.</span></span>

### <a name="a-name142142"></a><span data-ttu-id="3a951-160"><a name="1.4.2"/>1.4.2</span><span class="sxs-lookup"><span data-stu-id="3a951-160"><a name="1.4.2"/>1.4.2</span></span>
* <span data-ttu-id="3a951-161">Implementar o Upsert.</span><span class="sxs-lookup"><span data-stu-id="3a951-161">Implement Upsert.</span></span> <span data-ttu-id="3a951-162">Novos métodos UpsertXXX adicionados para dar suporte ao recurso Upsert.</span><span class="sxs-lookup"><span data-stu-id="3a951-162">New UpsertXXX methods added to support Upsert feature.</span></span>
* <span data-ttu-id="3a951-163">Implementar o roteamento com base em ID.</span><span class="sxs-lookup"><span data-stu-id="3a951-163">Implement ID Based Routing.</span></span> <span data-ttu-id="3a951-164">Nenhuma alteração pública de API, todas as alterações são internas.</span><span class="sxs-lookup"><span data-stu-id="3a951-164">No public API changes, all changes internal.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="3a951-165"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="3a951-165"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="3a951-166">Oferece suporte ao índice Geoespacial.</span><span class="sxs-lookup"><span data-stu-id="3a951-166">Supports GeoSpatial index.</span></span>
* <span data-ttu-id="3a951-167">Valida a propriedade de ID de todos os recursos.</span><span class="sxs-lookup"><span data-stu-id="3a951-167">Validates id property for all resources.</span></span> <span data-ttu-id="3a951-168">As IDs de recursos não podem conter caracteres ?, /, #, \, ou terminar com um espaço.</span><span class="sxs-lookup"><span data-stu-id="3a951-168">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="3a951-169">Adiciona o novo cabeçalho "andamento de transformação do índice" ao ResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="3a951-169">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="3a951-170"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="3a951-170"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="3a951-171">Implementa a política de indexação V2.</span><span class="sxs-lookup"><span data-stu-id="3a951-171">Implements V2 indexing policy.</span></span>

### <a name="a-name101101"></a><span data-ttu-id="3a951-172"><a name="1.0.1"/>1.0.1</span><span class="sxs-lookup"><span data-stu-id="3a951-172"><a name="1.0.1"/>1.0.1</span></span>
* <span data-ttu-id="3a951-173">Oferece suporte à conexão de proxy.</span><span class="sxs-lookup"><span data-stu-id="3a951-173">Supports proxy connection.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="3a951-174"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="3a951-174"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="3a951-175">SDK DO GA.</span><span class="sxs-lookup"><span data-stu-id="3a951-175">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="3a951-176">Datas de lançamento e de baixa</span><span class="sxs-lookup"><span data-stu-id="3a951-176">Release & retirement dates</span></span>
<span data-ttu-id="3a951-177">A Microsoft fornecerá uma notificação pelo menos **12 meses** antes de desativar um SDK, a fim de realizar uma transição tranquila para uma versão mais recente/com suporte.</span><span class="sxs-lookup"><span data-stu-id="3a951-177">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="3a951-178">Os novos recursos, funcionalidades e otimizações são adicionados apenas ao SDK atual. Portanto, recomendamos que você atualize sempre que possível para a versão do SDK mais recente.</span><span class="sxs-lookup"><span data-stu-id="3a951-178">New features and functionality and optimizations are only added to the current SDK, as such it is  recommend that you always upgrade to the latest SDK version as early as possible.</span></span> 

<span data-ttu-id="3a951-179">Qualquer solicitação feita ao Cosmos DB com o uso de um SDK desativado será rejeitada pelo serviço.</span><span class="sxs-lookup"><span data-stu-id="3a951-179">Any request to Cosmos DB using a retired SDK will be rejected by the service.</span></span>

> [!WARNING]
> <span data-ttu-id="3a951-180">Todas as versões do SDK do DocumentDB do Azure para Python anteriores à versão **1.0.0** serão desativadas em **29 de fevereiro de 2016**.</span><span class="sxs-lookup"><span data-stu-id="3a951-180">All versions of the Azure DocumentDB SDK for Python prior to version **1.0.0** will be retired on **February 29, 2016**.</span></span> 
> 
> 

<br/>

| <span data-ttu-id="3a951-181">Versão</span><span class="sxs-lookup"><span data-stu-id="3a951-181">Version</span></span> | <span data-ttu-id="3a951-182">Data do lançamento</span><span class="sxs-lookup"><span data-stu-id="3a951-182">Release Date</span></span> | <span data-ttu-id="3a951-183">Data de desativação</span><span class="sxs-lookup"><span data-stu-id="3a951-183">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="3a951-184">2.2.0</span><span class="sxs-lookup"><span data-stu-id="3a951-184">2.2.0</span></span>](#2.2.0) |<span data-ttu-id="3a951-185">10 de maio de 2017</span><span class="sxs-lookup"><span data-stu-id="3a951-185">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="3a951-186">2.1.0</span><span class="sxs-lookup"><span data-stu-id="3a951-186">2.1.0</span></span>](#2.1.0) |<span data-ttu-id="3a951-187">1º de maio de 2017</span><span class="sxs-lookup"><span data-stu-id="3a951-187">May 01, 2017</span></span> |--- |
| [<span data-ttu-id="3a951-188">2.0.1</span><span class="sxs-lookup"><span data-stu-id="3a951-188">2.0.1</span></span>](#2.0.1) |<span data-ttu-id="3a951-189">30 de outubro de 2016</span><span class="sxs-lookup"><span data-stu-id="3a951-189">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="3a951-190">2.0.0</span><span class="sxs-lookup"><span data-stu-id="3a951-190">2.0.0</span></span>](#2.0.0) |<span data-ttu-id="3a951-191">29 de setembro de 2016</span><span class="sxs-lookup"><span data-stu-id="3a951-191">September 29, 2016</span></span> |--- |
| [<span data-ttu-id="3a951-192">1.9.0</span><span class="sxs-lookup"><span data-stu-id="3a951-192">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="3a951-193">07 de julho de 2016</span><span class="sxs-lookup"><span data-stu-id="3a951-193">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="3a951-194">1.8.0</span><span class="sxs-lookup"><span data-stu-id="3a951-194">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="3a951-195">14 de junho de 2016</span><span class="sxs-lookup"><span data-stu-id="3a951-195">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="3a951-196">1.7.0</span><span class="sxs-lookup"><span data-stu-id="3a951-196">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="3a951-197">26 de abril de 2016</span><span class="sxs-lookup"><span data-stu-id="3a951-197">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="3a951-198">1.6.1</span><span class="sxs-lookup"><span data-stu-id="3a951-198">1.6.1</span></span>](#1.6.1) |<span data-ttu-id="3a951-199">08 de abril de 2016</span><span class="sxs-lookup"><span data-stu-id="3a951-199">April 08, 2016</span></span> |--- |
| [<span data-ttu-id="3a951-200">1.6.0</span><span class="sxs-lookup"><span data-stu-id="3a951-200">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="3a951-201">29 de março de 2016</span><span class="sxs-lookup"><span data-stu-id="3a951-201">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="3a951-202">1.5.0</span><span class="sxs-lookup"><span data-stu-id="3a951-202">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="3a951-203">03 de janeiro de 2016</span><span class="sxs-lookup"><span data-stu-id="3a951-203">January 03, 2016</span></span> |--- |
| [<span data-ttu-id="3a951-204">1.4.2</span><span class="sxs-lookup"><span data-stu-id="3a951-204">1.4.2</span></span>](#1.4.2) |<span data-ttu-id="3a951-205">06 de outubro de 2015</span><span class="sxs-lookup"><span data-stu-id="3a951-205">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="3a951-206">1.4.1</span><span class="sxs-lookup"><span data-stu-id="3a951-206">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="3a951-207">06 de outubro de 2015</span><span class="sxs-lookup"><span data-stu-id="3a951-207">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="3a951-208">1.2.0</span><span class="sxs-lookup"><span data-stu-id="3a951-208">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="3a951-209">06 de agosto de 2015</span><span class="sxs-lookup"><span data-stu-id="3a951-209">August 06, 2015</span></span> |--- |
| [<span data-ttu-id="3a951-210">1.1.0</span><span class="sxs-lookup"><span data-stu-id="3a951-210">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="3a951-211">9 de julho de 2015</span><span class="sxs-lookup"><span data-stu-id="3a951-211">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="3a951-212">1.0.1</span><span class="sxs-lookup"><span data-stu-id="3a951-212">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="3a951-213">25 de maio de 2015</span><span class="sxs-lookup"><span data-stu-id="3a951-213">May 25, 2015</span></span> |--- |
| [<span data-ttu-id="3a951-214">1.0.0</span><span class="sxs-lookup"><span data-stu-id="3a951-214">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="3a951-215">7 de abril de 2015</span><span class="sxs-lookup"><span data-stu-id="3a951-215">April 07, 2015</span></span> |--- |
| <span data-ttu-id="3a951-216">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="3a951-216">0.9.4-prelease</span></span> |<span data-ttu-id="3a951-217">14 de janeiro de 2015</span><span class="sxs-lookup"><span data-stu-id="3a951-217">January 14, 2015</span></span> |<span data-ttu-id="3a951-218">29 de fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="3a951-218">February 29, 2016</span></span> |
| <span data-ttu-id="3a951-219">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="3a951-219">0.9.3-prelease</span></span> |<span data-ttu-id="3a951-220">09 de dezembro de 2014</span><span class="sxs-lookup"><span data-stu-id="3a951-220">December 09, 2014</span></span> |<span data-ttu-id="3a951-221">29 de fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="3a951-221">February 29, 2016</span></span> |
| <span data-ttu-id="3a951-222">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="3a951-222">0.9.2-prelease</span></span> |<span data-ttu-id="3a951-223">25 de novembro de 2014</span><span class="sxs-lookup"><span data-stu-id="3a951-223">November 25, 2014</span></span> |<span data-ttu-id="3a951-224">29 de fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="3a951-224">February 29, 2016</span></span> |
| <span data-ttu-id="3a951-225">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="3a951-225">0.9.1-prelease</span></span> |<span data-ttu-id="3a951-226">23 de setembro de 2014</span><span class="sxs-lookup"><span data-stu-id="3a951-226">September 23, 2014</span></span> |<span data-ttu-id="3a951-227">29 de fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="3a951-227">February 29, 2016</span></span> |
| <span data-ttu-id="3a951-228">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="3a951-228">0.9.0-prelease</span></span> |<span data-ttu-id="3a951-229">21 de agosto de 2014</span><span class="sxs-lookup"><span data-stu-id="3a951-229">August 21, 2014</span></span> |<span data-ttu-id="3a951-230">29 de fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="3a951-230">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="3a951-231">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="3a951-231">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="3a951-232">Consulte também</span><span class="sxs-lookup"><span data-stu-id="3a951-232">See also</span></span>
<span data-ttu-id="3a951-233">Para saber mais sobre o Cosmos DB, consulte a página de serviço do [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="3a951-233">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

