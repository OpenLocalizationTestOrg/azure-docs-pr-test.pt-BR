---
title: aaaAzure Cosmos DB Python API, SDK e recursos | Microsoft Docs
description: "Saiba tudo sobre Olá Python API e o SDK, incluindo datas de lançamento, datas de desativação e as alterações feitas entre cada versão da saudação do SDK do Azure Cosmos DB Python."
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
ms.openlocfilehash: 1a164b72d2bd819de87df0229357b82e2177af2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a><span data-ttu-id="8891f-103">SDK do Python do Azure Cosmos DB: notas de versão e recursos</span><span class="sxs-lookup"><span data-stu-id="8891f-103">Azure Cosmos DB Python SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8891f-104">.NET</span><span class="sxs-lookup"><span data-stu-id="8891f-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="8891f-105">Feed de alterações do .NET</span><span class="sxs-lookup"><span data-stu-id="8891f-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="8891f-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="8891f-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="8891f-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="8891f-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="8891f-108">Java</span><span class="sxs-lookup"><span data-stu-id="8891f-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="8891f-109">Python</span><span class="sxs-lookup"><span data-stu-id="8891f-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="8891f-110">REST</span><span class="sxs-lookup"><span data-stu-id="8891f-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="8891f-111">Provedor de recursos REST</span><span class="sxs-lookup"><span data-stu-id="8891f-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="8891f-112">SQL</span><span class="sxs-lookup"><span data-stu-id="8891f-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="8891f-113">**Baixar o SDK**</span><span class="sxs-lookup"><span data-stu-id="8891f-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="8891f-114">PyPI</span><span class="sxs-lookup"><span data-stu-id="8891f-114">PyPI</span></span>](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td><span data-ttu-id="8891f-115">**Documentação da API**</span><span class="sxs-lookup"><span data-stu-id="8891f-115">**API documentation**</span></span></td><td>[<span data-ttu-id="8891f-116">Documentação de referência da API do Python</span><span class="sxs-lookup"><span data-stu-id="8891f-116">Python API reference documentation</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td><span data-ttu-id="8891f-117">**Instruções de instalação do SDK**</span><span class="sxs-lookup"><span data-stu-id="8891f-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="8891f-118">Instruções de instalação do SDK do Python</span><span class="sxs-lookup"><span data-stu-id="8891f-118">Python SDK installation instructions</span></span>](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td><span data-ttu-id="8891f-119">**Contribuir tooSDK**</span><span class="sxs-lookup"><span data-stu-id="8891f-119">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="8891f-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="8891f-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td><span data-ttu-id="8891f-121">**Introdução**</span><span class="sxs-lookup"><span data-stu-id="8891f-121">**Get started**</span></span></td><td>[<span data-ttu-id="8891f-122">Introdução ao SDK de Python de saudação</span><span class="sxs-lookup"><span data-stu-id="8891f-122">Get started with hello Python SDK</span></span>](documentdb-python-application.md)</td></tr>

<tr><td><span data-ttu-id="8891f-123">**Plataforma atual com suporte**</span><span class="sxs-lookup"><span data-stu-id="8891f-123">**Current supported platform**</span></span></td><td><span data-ttu-id="8891f-124">[Python 2.7](https://www.python.org/downloads/) e [Python 3.5](https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="8891f-124">[Python 2.7](https://www.python.org/downloads/) and [Python 3.5](https://www.python.org/downloads/)</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="8891f-125">Notas de versão</span><span class="sxs-lookup"><span data-stu-id="8891f-125">Release notes</span></span>
### <a name="a-name220220"></a><span data-ttu-id="8891f-126"><a name="2.2.0"/>2.2.0</span><span class="sxs-lookup"><span data-stu-id="8891f-126"><a name="2.2.0"/>2.2.0</span></span>
* <span data-ttu-id="8891f-127">Adição de suporte a um novo nível de consistência chamado ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="8891f-127">Added support for a new consistency level called ConsistentPrefix.</span></span>


### <a name="a-name210210"></a><span data-ttu-id="8891f-128"><a name="2.1.0"/>2.1.0</span><span class="sxs-lookup"><span data-stu-id="8891f-128"><a name="2.1.0"/>2.1.0</span></span>
* <span data-ttu-id="8891f-129">Suporte adicionado para consultas de agregação (COUNT, MIN, MAX, SUM e AVG).</span><span class="sxs-lookup"><span data-stu-id="8891f-129">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="8891f-130">Adição de uma opção para desabilitar a verificação do SSL quando executada no Emulador do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8891f-130">Added an option for disabling SSL verification when running against Cosmos DB Emulator.</span></span>
* <span data-ttu-id="8891f-131">Remover restrição de saudação do módulo de solicitações dependentes toobe 2.10.0 exatamente.</span><span class="sxs-lookup"><span data-stu-id="8891f-131">Removed hello restriction of dependent requests module toobe exactly 2.10.0.</span></span>
* <span data-ttu-id="8891f-132">Reduzida a taxa de transferência mínima em coleções particionadas de 10,100 RU/s too2500 RU/s.</span><span class="sxs-lookup"><span data-stu-id="8891f-132">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>
* <span data-ttu-id="8891f-133">Adicionado suporte para habilitar o registro em log de script durante a execução do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="8891f-133">Added support for enabling script logging during stored procedure execution.</span></span>
* <span data-ttu-id="8891f-134">Versão da API REST muito aumentado ' 2017-01-19' com esta versão.</span><span class="sxs-lookup"><span data-stu-id="8891f-134">REST API version bumped too'2017-01-19' with this release.</span></span>

### <a name="a-name201201"></a><span data-ttu-id="8891f-135"><a name="2.0.1"/>2.0.1</span><span class="sxs-lookup"><span data-stu-id="8891f-135"><a name="2.0.1"/>2.0.1</span></span>
* <span data-ttu-id="8891f-136">Fez alterações editoriais toodocumentation comentários.</span><span class="sxs-lookup"><span data-stu-id="8891f-136">Made editorial changes toodocumentation comments.</span></span>

### <a name="a-name200200"></a><span data-ttu-id="8891f-137"><a name="2.0.0"/>2.0.0</span><span class="sxs-lookup"><span data-stu-id="8891f-137"><a name="2.0.0"/>2.0.0</span></span>
* <span data-ttu-id="8891f-138">Suporte ao Python 3.5 adicionado.</span><span class="sxs-lookup"><span data-stu-id="8891f-138">Added support for Python 3.5.</span></span>
* <span data-ttu-id="8891f-139">Suporte ao pool de conexões usando um módulo de solicitações adicionado.</span><span class="sxs-lookup"><span data-stu-id="8891f-139">Added support for connection pooling using a requests module.</span></span>
* <span data-ttu-id="8891f-140">Suporte à consistência da sessão adicionado.</span><span class="sxs-lookup"><span data-stu-id="8891f-140">Added support for session consistency.</span></span>
* <span data-ttu-id="8891f-141">Suporte às consultas TOP/ORDERBY de coleções particionadas adicionado.</span><span class="sxs-lookup"><span data-stu-id="8891f-141">Added support for TOP/ORDERBY queries for partitioned collections.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="8891f-142"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="8891f-142"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="8891f-143">Suporte à política de repetições para solicitações limitadas adicionado.</span><span class="sxs-lookup"><span data-stu-id="8891f-143">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="8891f-144">(As solicitações limitadas recebem uma exceção muito grande de taxa de solicitação, código de erro 429.) Por padrão, banco de dados do Azure Cosmos repete nove vezes para cada solicitação quando o código de erro 429 é encontrado, para respeitar o tempo de retryAfter saudação no cabeçalho de resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="8891f-144">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring hello retryAfter time in hello response header.</span></span> <span data-ttu-id="8891f-145">Um intervalo de tempo fixo de repetição agora pode ser definido como parte da saudação RetryOptions propriedade no objeto de ConnectionPolicy Olá se você desejar tooignore Olá retryAfter tempo retornado pelo servidor entre as tentativas de saudação.</span><span class="sxs-lookup"><span data-stu-id="8891f-145">A fixed retry interval time can now be set as part of hello RetryOptions property on hello ConnectionPolicy object if you want tooignore hello retryAfter time returned by server between hello retries.</span></span> <span data-ttu-id="8891f-146">Banco de dados do Azure Cosmos agora aguarda um máximo de 30 segundos para cada solicitação que está sendo limitado (independentemente da contagem de repetição) e retorna a resposta de saudação com código de erro 429.</span><span class="sxs-lookup"><span data-stu-id="8891f-146">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns hello response with error code 429.</span></span> <span data-ttu-id="8891f-147">Neste momento também pode ser substituída em Olá RetryOptions propriedade no objeto ConnectionPolicy.</span><span class="sxs-lookup"><span data-stu-id="8891f-147">This time can also be overriden in hello RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="8891f-148">Cosmos DB agora retorna x-ms-acelerador--contagem de repetição e x-ms-throttle-retry-wait-time-ms como cabeçalhos de resposta de saudação em cada Acelerador de saudação solicitação toodenote tempo de nova tentativa contagem e hello cummulative Olá solicitação espera entre as tentativas de saudação.</span><span class="sxs-lookup"><span data-stu-id="8891f-148">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as hello response headers in every request toodenote hello throttle retry count and hello cummulative time hello request waited between hello retries.</span></span>
* <span data-ttu-id="8891f-149">Classe de RetryPolicy Olá removido e propriedade correspondente da saudação (retry_policy) exposto na classe de document_client hello e introduzida em vez disso, uma classe RetryOptions expondo a propriedade de RetryOptions Olá na classe ConnectionPolicy que pode ser usado toooverride alguns dos padrão Olá opções de repetição.</span><span class="sxs-lookup"><span data-stu-id="8891f-149">Removed hello RetryPolicy class and hello corresponding property (retry_policy) exposed on hello document_client class and instead introduced a RetryOptions class exposing hello RetryOptions property on ConnectionPolicy class that can be used toooverride some of hello default retry options.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="8891f-150"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="8891f-150"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="8891f-151">Suporte adicionado Olá para contas do banco de dados de várias regiões.</span><span class="sxs-lookup"><span data-stu-id="8891f-151">Added hello support for multi-region database accounts.</span></span>

### <a name="a-name170170"></a><span data-ttu-id="8891f-152"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="8891f-152"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="8891f-153">Olá adicionado suporte para o recurso de tooLive(TTL) de tempo para documentos.</span><span class="sxs-lookup"><span data-stu-id="8891f-153">Added hello support for Time tooLive(TTL) feature for documents.</span></span>

### <a name="a-name161161"></a><span data-ttu-id="8891f-154"><a name="1.6.1"/>1.6.1</span><span class="sxs-lookup"><span data-stu-id="8891f-154"><a name="1.6.1"/>1.6.1</span></span>
* <span data-ttu-id="8891f-155">Correções de bug relacionado lado tooserver particionamento tooallow de caracteres especiais no caminho de partitionkey.</span><span class="sxs-lookup"><span data-stu-id="8891f-155">Bug fixes related tooserver side partitioning tooallow special characters in partitionkey path.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="8891f-156"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="8891f-156"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="8891f-157">Implementação de [coleções particionadas](partition-data.md) e [níveis de desempenho definidos pelo usuário](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="8891f-157">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span> 

### <a name="a-name150150"></a><span data-ttu-id="8891f-158"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="8891f-158"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="8891f-159">Adicionar & intervalo de Hash tooassist de resolvedores de partição com aplicativos de fragmentação por várias partições.</span><span class="sxs-lookup"><span data-stu-id="8891f-159">Add Hash & Range partition resolvers tooassist with sharding applications across multiple partitions.</span></span>

### <a name="a-name142142"></a><span data-ttu-id="8891f-160"><a name="1.4.2"/>1.4.2</span><span class="sxs-lookup"><span data-stu-id="8891f-160"><a name="1.4.2"/>1.4.2</span></span>
* <span data-ttu-id="8891f-161">Implementar o Upsert.</span><span class="sxs-lookup"><span data-stu-id="8891f-161">Implement Upsert.</span></span> <span data-ttu-id="8891f-162">Novos métodos UpsertXXX adicionaram toosupport Upsert recurso.</span><span class="sxs-lookup"><span data-stu-id="8891f-162">New UpsertXXX methods added toosupport Upsert feature.</span></span>
* <span data-ttu-id="8891f-163">Implementar o roteamento com base em ID.</span><span class="sxs-lookup"><span data-stu-id="8891f-163">Implement ID Based Routing.</span></span> <span data-ttu-id="8891f-164">Nenhuma alteração pública de API, todas as alterações são internas.</span><span class="sxs-lookup"><span data-stu-id="8891f-164">No public API changes, all changes internal.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="8891f-165"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="8891f-165"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="8891f-166">Oferece suporte ao índice Geoespacial.</span><span class="sxs-lookup"><span data-stu-id="8891f-166">Supports GeoSpatial index.</span></span>
* <span data-ttu-id="8891f-167">Valida a propriedade de ID de todos os recursos.</span><span class="sxs-lookup"><span data-stu-id="8891f-167">Validates id property for all resources.</span></span> <span data-ttu-id="8891f-168">As IDs de recursos não podem conter caracteres ?, /, #, \, ou terminar com um espaço.</span><span class="sxs-lookup"><span data-stu-id="8891f-168">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="8891f-169">Adiciona novo tooResourceResponse "andamento de transformação de índice" de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="8891f-169">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="8891f-170"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="8891f-170"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="8891f-171">Implementa a política de indexação V2.</span><span class="sxs-lookup"><span data-stu-id="8891f-171">Implements V2 indexing policy.</span></span>

### <a name="a-name101101"></a><span data-ttu-id="8891f-172"><a name="1.0.1"/>1.0.1</span><span class="sxs-lookup"><span data-stu-id="8891f-172"><a name="1.0.1"/>1.0.1</span></span>
* <span data-ttu-id="8891f-173">Oferece suporte à conexão de proxy.</span><span class="sxs-lookup"><span data-stu-id="8891f-173">Supports proxy connection.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="8891f-174"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="8891f-174"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="8891f-175">SDK DO GA.</span><span class="sxs-lookup"><span data-stu-id="8891f-175">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="8891f-176">Datas de lançamento e de baixa</span><span class="sxs-lookup"><span data-stu-id="8891f-176">Release & retirement dates</span></span>
<span data-ttu-id="8891f-177">A Microsoft fornecerá notificação pelo menos **12 meses** antes de desativar um SDK na versão mais recente/suporte ordem toosmooth Olá transição tooa.</span><span class="sxs-lookup"><span data-stu-id="8891f-177">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="8891f-178">Novos recursos e funcionalidade e as otimizações são adicionadas apenas toohello atual SDK, como tal, é recomendável que você sempre atualize toohello mais recente versão do SDK mais cedo possível.</span><span class="sxs-lookup"><span data-stu-id="8891f-178">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommend that you always upgrade toohello latest SDK version as early as possible.</span></span> 

<span data-ttu-id="8891f-179">TooCosmos qualquer solicitação usando um SDK obsoleto do banco de dados serão rejeitados pelo serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="8891f-179">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

> [!WARNING]
> <span data-ttu-id="8891f-180">Todas as versões do hello SDK do DocumentDB do Azure para tooversion anterior Python **1.0.0** será desativado em **29 de fevereiro de 2016**.</span><span class="sxs-lookup"><span data-stu-id="8891f-180">All versions of hello Azure DocumentDB SDK for Python prior tooversion **1.0.0** will be retired on **February 29, 2016**.</span></span> 
> 
> 

<br/>

| <span data-ttu-id="8891f-181">Versão</span><span class="sxs-lookup"><span data-stu-id="8891f-181">Version</span></span> | <span data-ttu-id="8891f-182">Data do lançamento</span><span class="sxs-lookup"><span data-stu-id="8891f-182">Release Date</span></span> | <span data-ttu-id="8891f-183">Data de desativação</span><span class="sxs-lookup"><span data-stu-id="8891f-183">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="8891f-184">2.2.0</span><span class="sxs-lookup"><span data-stu-id="8891f-184">2.2.0</span></span>](#2.2.0) |<span data-ttu-id="8891f-185">10 de maio de 2017</span><span class="sxs-lookup"><span data-stu-id="8891f-185">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="8891f-186">2.1.0</span><span class="sxs-lookup"><span data-stu-id="8891f-186">2.1.0</span></span>](#2.1.0) |<span data-ttu-id="8891f-187">1º de maio de 2017</span><span class="sxs-lookup"><span data-stu-id="8891f-187">May 01, 2017</span></span> |--- |
| [<span data-ttu-id="8891f-188">2.0.1</span><span class="sxs-lookup"><span data-stu-id="8891f-188">2.0.1</span></span>](#2.0.1) |<span data-ttu-id="8891f-189">30 de outubro de 2016</span><span class="sxs-lookup"><span data-stu-id="8891f-189">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="8891f-190">2.0.0</span><span class="sxs-lookup"><span data-stu-id="8891f-190">2.0.0</span></span>](#2.0.0) |<span data-ttu-id="8891f-191">29 de setembro de 2016</span><span class="sxs-lookup"><span data-stu-id="8891f-191">September 29, 2016</span></span> |--- |
| [<span data-ttu-id="8891f-192">1.9.0</span><span class="sxs-lookup"><span data-stu-id="8891f-192">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="8891f-193">07 de julho de 2016</span><span class="sxs-lookup"><span data-stu-id="8891f-193">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="8891f-194">1.8.0</span><span class="sxs-lookup"><span data-stu-id="8891f-194">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="8891f-195">14 de junho de 2016</span><span class="sxs-lookup"><span data-stu-id="8891f-195">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="8891f-196">1.7.0</span><span class="sxs-lookup"><span data-stu-id="8891f-196">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="8891f-197">26 de abril de 2016</span><span class="sxs-lookup"><span data-stu-id="8891f-197">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="8891f-198">1.6.1</span><span class="sxs-lookup"><span data-stu-id="8891f-198">1.6.1</span></span>](#1.6.1) |<span data-ttu-id="8891f-199">08 de abril de 2016</span><span class="sxs-lookup"><span data-stu-id="8891f-199">April 08, 2016</span></span> |--- |
| [<span data-ttu-id="8891f-200">1.6.0</span><span class="sxs-lookup"><span data-stu-id="8891f-200">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="8891f-201">29 de março de 2016</span><span class="sxs-lookup"><span data-stu-id="8891f-201">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="8891f-202">1.5.0</span><span class="sxs-lookup"><span data-stu-id="8891f-202">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="8891f-203">03 de janeiro de 2016</span><span class="sxs-lookup"><span data-stu-id="8891f-203">January 03, 2016</span></span> |--- |
| [<span data-ttu-id="8891f-204">1.4.2</span><span class="sxs-lookup"><span data-stu-id="8891f-204">1.4.2</span></span>](#1.4.2) |<span data-ttu-id="8891f-205">06 de outubro de 2015</span><span class="sxs-lookup"><span data-stu-id="8891f-205">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="8891f-206">1.4.1</span><span class="sxs-lookup"><span data-stu-id="8891f-206">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="8891f-207">06 de outubro de 2015</span><span class="sxs-lookup"><span data-stu-id="8891f-207">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="8891f-208">1.2.0</span><span class="sxs-lookup"><span data-stu-id="8891f-208">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="8891f-209">06 de agosto de 2015</span><span class="sxs-lookup"><span data-stu-id="8891f-209">August 06, 2015</span></span> |--- |
| [<span data-ttu-id="8891f-210">1.1.0</span><span class="sxs-lookup"><span data-stu-id="8891f-210">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="8891f-211">9 de julho de 2015</span><span class="sxs-lookup"><span data-stu-id="8891f-211">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="8891f-212">1.0.1</span><span class="sxs-lookup"><span data-stu-id="8891f-212">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="8891f-213">25 de maio de 2015</span><span class="sxs-lookup"><span data-stu-id="8891f-213">May 25, 2015</span></span> |--- |
| [<span data-ttu-id="8891f-214">1.0.0</span><span class="sxs-lookup"><span data-stu-id="8891f-214">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="8891f-215">7 de abril de 2015</span><span class="sxs-lookup"><span data-stu-id="8891f-215">April 07, 2015</span></span> |--- |
| <span data-ttu-id="8891f-216">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="8891f-216">0.9.4-prelease</span></span> |<span data-ttu-id="8891f-217">14 de janeiro de 2015</span><span class="sxs-lookup"><span data-stu-id="8891f-217">January 14, 2015</span></span> |<span data-ttu-id="8891f-218">29 de fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="8891f-218">February 29, 2016</span></span> |
| <span data-ttu-id="8891f-219">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="8891f-219">0.9.3-prelease</span></span> |<span data-ttu-id="8891f-220">09 de dezembro de 2014</span><span class="sxs-lookup"><span data-stu-id="8891f-220">December 09, 2014</span></span> |<span data-ttu-id="8891f-221">29 de fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="8891f-221">February 29, 2016</span></span> |
| <span data-ttu-id="8891f-222">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="8891f-222">0.9.2-prelease</span></span> |<span data-ttu-id="8891f-223">25 de novembro de 2014</span><span class="sxs-lookup"><span data-stu-id="8891f-223">November 25, 2014</span></span> |<span data-ttu-id="8891f-224">29 de fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="8891f-224">February 29, 2016</span></span> |
| <span data-ttu-id="8891f-225">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="8891f-225">0.9.1-prelease</span></span> |<span data-ttu-id="8891f-226">23 de setembro de 2014</span><span class="sxs-lookup"><span data-stu-id="8891f-226">September 23, 2014</span></span> |<span data-ttu-id="8891f-227">29 de fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="8891f-227">February 29, 2016</span></span> |
| <span data-ttu-id="8891f-228">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="8891f-228">0.9.0-prelease</span></span> |<span data-ttu-id="8891f-229">21 de agosto de 2014</span><span class="sxs-lookup"><span data-stu-id="8891f-229">August 21, 2014</span></span> |<span data-ttu-id="8891f-230">29 de fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="8891f-230">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="8891f-231">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="8891f-231">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="8891f-232">Consulte também</span><span class="sxs-lookup"><span data-stu-id="8891f-232">See also</span></span>
<span data-ttu-id="8891f-233">toolearn mais sobre o banco de dados do Cosmos, consulte [banco de dados do Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) página de serviço.</span><span class="sxs-lookup"><span data-stu-id="8891f-233">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

