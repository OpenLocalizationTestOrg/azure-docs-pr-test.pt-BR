---
title: aaaAzure Cosmos DB Node. js API, SDK e recursos | Microsoft Docs
description: "Saiba tudo sobre Olá Node. js API e o SDK, incluindo datas de lançamento, datas de desativação e as alterações feitas entre cada versão do hello Azure Cosmos DB Node. js SDK."
services: cosmos-db
documentationcenter: nodejs
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 9d5621fa-0e11-4619-a28b-a19d872bcf37
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d450b9a9ea7b0f4717ddae8940121fc458ea3744
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a><span data-ttu-id="763d7-103">SDK de Node.js do Azure Cosmos DB: Notas de versão e recursos</span><span class="sxs-lookup"><span data-stu-id="763d7-103">Azure Cosmos DB Node.js SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="763d7-104">.NET</span><span class="sxs-lookup"><span data-stu-id="763d7-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="763d7-105">Feed de alterações do .NET</span><span class="sxs-lookup"><span data-stu-id="763d7-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="763d7-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="763d7-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="763d7-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="763d7-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="763d7-108">Java</span><span class="sxs-lookup"><span data-stu-id="763d7-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="763d7-109">Python</span><span class="sxs-lookup"><span data-stu-id="763d7-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="763d7-110">REST</span><span class="sxs-lookup"><span data-stu-id="763d7-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="763d7-111">Provedor de recursos REST</span><span class="sxs-lookup"><span data-stu-id="763d7-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="763d7-112">SQL</span><span class="sxs-lookup"><span data-stu-id="763d7-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="763d7-113">**Baixar o SDK**</span><span class="sxs-lookup"><span data-stu-id="763d7-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="763d7-114">NPM</span><span class="sxs-lookup"><span data-stu-id="763d7-114">NPM</span></span>](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td><span data-ttu-id="763d7-115">**Documentação da API**</span><span class="sxs-lookup"><span data-stu-id="763d7-115">**API documentation**</span></span></td><td>[<span data-ttu-id="763d7-116">Documentação de referência da API do Node.js</span><span class="sxs-lookup"><span data-stu-id="763d7-116">Node.js API reference documentation</span></span>](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td><span data-ttu-id="763d7-117">**Instruções de instalação do SDK**</span><span class="sxs-lookup"><span data-stu-id="763d7-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="763d7-118">Instruções de instalação</span><span class="sxs-lookup"><span data-stu-id="763d7-118">Installation instructions</span></span>](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td><span data-ttu-id="763d7-119">**Contribuir tooSDK**</span><span class="sxs-lookup"><span data-stu-id="763d7-119">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="763d7-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="763d7-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td><span data-ttu-id="763d7-121">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="763d7-121">**Samples**</span></span></td><td>[<span data-ttu-id="763d7-122">Exemplos de código do Node.js</span><span class="sxs-lookup"><span data-stu-id="763d7-122">Node.js code samples</span></span>](documentdb-nodejs-samples.md)</td></tr>

<tr><td><span data-ttu-id="763d7-123">**Tutorial de introdução**</span><span class="sxs-lookup"><span data-stu-id="763d7-123">**Get started tutorial**</span></span></td><td>[<span data-ttu-id="763d7-124">Introdução ao Olá Node. js SDK</span><span class="sxs-lookup"><span data-stu-id="763d7-124">Get started with hello Node.js SDK</span></span>](documentdb-nodejs-get-started.md)</td></tr>

<tr><td><span data-ttu-id="763d7-125">**Tutorial do aplicativo Web**</span><span class="sxs-lookup"><span data-stu-id="763d7-125">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="763d7-126">Criar um aplicativo web Node.js usando o Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="763d7-126">Build a Node.js web application using Azure Cosmos DB</span></span>](documentdb-nodejs-application.md)</td></tr>

<tr><td><span data-ttu-id="763d7-127">**Plataforma atual com suporte**</span><span class="sxs-lookup"><span data-stu-id="763d7-127">**Current supported platform**</span></span></td><td> 
[<span data-ttu-id="763d7-128">Node.js v6.x</span><span class="sxs-lookup"><span data-stu-id="763d7-128">Node.js v6.x</span></span>](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[<span data-ttu-id="763d7-129">Node.js v4.2.0</span><span class="sxs-lookup"><span data-stu-id="763d7-129">Node.js v4.2.0</span></span>](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[<span data-ttu-id="763d7-130">Node.js v0.12</span><span class="sxs-lookup"><span data-stu-id="763d7-130">Node.js v0.12</span></span>](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
<span data-ttu-id="763d7-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span><span class="sxs-lookup"><span data-stu-id="763d7-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="763d7-132">Notas de versão</span><span class="sxs-lookup"><span data-stu-id="763d7-132">Release notes</span></span>

### <span data-ttu-id="763d7-133"><a name="1.12.2"/>1.12.2</a></span><span class="sxs-lookup"><span data-stu-id="763d7-133"><a name="1.12.2"/>1.12.2</a></span></span>
*   <span data-ttu-id="763d7-134">documentação do npm corrigida.</span><span class="sxs-lookup"><span data-stu-id="763d7-134">npm documentation fixed.</span></span>

### <span data-ttu-id="763d7-135"><a name="1.12.1"/>1.12.1</a></span><span class="sxs-lookup"><span data-stu-id="763d7-135"><a name="1.12.1"/>1.12.1</a></span></span>
* <span data-ttu-id="763d7-136">Correção de um bug no executeStoredProcedure, em que documentos envolvidos tinham caracteres especiais Unicode (LS, PS).</span><span class="sxs-lookup"><span data-stu-id="763d7-136">Fixed a bug in executeStoredProcedure where documents involved had special Unicode characters (LS, PS).</span></span>
* <span data-ttu-id="763d7-137">Correção de bug na manipulação de documentos com caracteres de Unicode na chave de partição hello.</span><span class="sxs-lookup"><span data-stu-id="763d7-137">Fixed a bug in handling documents with Unicode characters in hello partition key.</span></span>
* <span data-ttu-id="763d7-138">Suporte fixado para criar coleções com mídia de nome hello.</span><span class="sxs-lookup"><span data-stu-id="763d7-138">Fixed support for creating collections with hello name media.</span></span> <span data-ttu-id="763d7-139">Problema nº 114 do Github.</span><span class="sxs-lookup"><span data-stu-id="763d7-139">Github issue #114.</span></span>
* <span data-ttu-id="763d7-140">Suporte fixo para o token de autorização de permissão.</span><span class="sxs-lookup"><span data-stu-id="763d7-140">Fixed support for permission authorization token.</span></span> <span data-ttu-id="763d7-141">Problema nº 178 do Github.</span><span class="sxs-lookup"><span data-stu-id="763d7-141">Github issue #178.</span></span>

### <span data-ttu-id="763d7-142"><a name="1.12.0"/>1.12.0</a></span><span class="sxs-lookup"><span data-stu-id="763d7-142"><a name="1.12.0"/>1.12.0</a></span></span>
* <span data-ttu-id="763d7-143">Foi adicionado suporte a um novo [nível de consistência](consistency-levels.md) chamado ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="763d7-143">Added support for a new [consistency level](consistency-levels.md) called ConsistentPrefix.</span></span>
* <span data-ttu-id="763d7-144">Foi adicionado suporte para UriFactory.</span><span class="sxs-lookup"><span data-stu-id="763d7-144">Added support for UriFactory.</span></span>
* <span data-ttu-id="763d7-145">Correção de um bug de suporte ao Unicode.</span><span class="sxs-lookup"><span data-stu-id="763d7-145">Fixed a Unicode support bug.</span></span> <span data-ttu-id="763d7-146">Problema nº 171 do Github.</span><span class="sxs-lookup"><span data-stu-id="763d7-146">GitHub issue #171.</span></span>

### <span data-ttu-id="763d7-147"><a name="1.11.0"/>1.11.0</a></span><span class="sxs-lookup"><span data-stu-id="763d7-147"><a name="1.11.0"/>1.11.0</a></span></span>
* <span data-ttu-id="763d7-148">Suporte adicionado Olá para consultas de agregação (COUNT, MIN, MAX, SUM e AVG).</span><span class="sxs-lookup"><span data-stu-id="763d7-148">Added hello support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="763d7-149">Opção de saudação adicionado para controlar o grau de paralelismo de várias consultas de partição.</span><span class="sxs-lookup"><span data-stu-id="763d7-149">Added hello option for controlling degree of parallelism for cross partition queries.</span></span>
* <span data-ttu-id="763d7-150">Opção de saudação adicionado para desabilitar a verificação de SSL durante a execução no emulador do Azure Cosmos banco de dados.</span><span class="sxs-lookup"><span data-stu-id="763d7-150">Added hello option for disabling SSL verification when running against Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="763d7-151">Reduzida a taxa de transferência mínima em coleções particionadas de 10,100 RU/s too2500 RU/s.</span><span class="sxs-lookup"><span data-stu-id="763d7-151">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>
* <span data-ttu-id="763d7-152">Bug token de continuação de Olá fixa para coleção única partição.</span><span class="sxs-lookup"><span data-stu-id="763d7-152">Fixed hello continuation token bug for single partition collection.</span></span> <span data-ttu-id="763d7-153">Problema nº 107 do Github.</span><span class="sxs-lookup"><span data-stu-id="763d7-153">Github issue #107.</span></span>
* <span data-ttu-id="763d7-154">Bug de executeStoredProcedure Olá fixa no tratamento 0 como parâmetro único.</span><span class="sxs-lookup"><span data-stu-id="763d7-154">Fixed hello executeStoredProcedure bug in handling 0 as single param.</span></span> <span data-ttu-id="763d7-155">Problema nº 155 do Github.</span><span class="sxs-lookup"><span data-stu-id="763d7-155">Github issue #155.</span></span>

### <span data-ttu-id="763d7-156"><a name="1.10.2"/>1.10.2</a></span><span class="sxs-lookup"><span data-stu-id="763d7-156"><a name="1.10.2"/>1.10.2</a></span></span>
* <span data-ttu-id="763d7-157">Versão do agente de usuário fixo cabeçalho tooinclude Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="763d7-157">Fixed user-agent header tooinclude hello SDK version.</span></span>
* <span data-ttu-id="763d7-158">Limpeza de código secundária.</span><span class="sxs-lookup"><span data-stu-id="763d7-158">Minor code cleanup.</span></span>

### <span data-ttu-id="763d7-159"><a name="1.10.1"/>1.10.1</a></span><span class="sxs-lookup"><span data-stu-id="763d7-159"><a name="1.10.1"/>1.10.1</a></span></span>
* <span data-ttu-id="763d7-160">Desabilitar a verificação de SSL ao usar Olá SDK tootarget Olá emulator(hostname=localhost).</span><span class="sxs-lookup"><span data-stu-id="763d7-160">Disabling SSL verification when using hello SDK tootarget hello emulator(hostname=localhost).</span></span>
* <span data-ttu-id="763d7-161">Adicionado suporte para habilitar o registro em log de script durante a execução do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="763d7-161">Added support for enabling script logging during stored procedure execution.</span></span>

### <span data-ttu-id="763d7-162"><a name="1.10.0"/>1.10.0</a></span><span class="sxs-lookup"><span data-stu-id="763d7-162"><a name="1.10.0"/>1.10.0</a></span></span>
* <span data-ttu-id="763d7-163">Adicionado suporte para várias consultas paralelas de partição.</span><span class="sxs-lookup"><span data-stu-id="763d7-163">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="763d7-164">Adição de suporte a consultas TOP/ORDER BY de coleções particionadas.</span><span class="sxs-lookup"><span data-stu-id="763d7-164">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>

### <span data-ttu-id="763d7-165"><a name="1.9.0"/>1.9.0</a></span><span class="sxs-lookup"><span data-stu-id="763d7-165"><a name="1.9.0"/>1.9.0</a></span></span>
* <span data-ttu-id="763d7-166">Suporte à política de repetições para solicitações limitadas adicionado.</span><span class="sxs-lookup"><span data-stu-id="763d7-166">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="763d7-167">(As solicitações limitadas recebem uma exceção muito grande de taxa de solicitação, código de erro 429.) Por padrão, banco de dados do Azure Cosmos repete nove vezes para cada solicitação quando o código de erro 429 é encontrado, para respeitar o tempo de retryAfter saudação no cabeçalho de resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="763d7-167">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring hello retryAfter time in hello response header.</span></span> <span data-ttu-id="763d7-168">Um intervalo de tempo fixo de repetição agora pode ser definido como parte da saudação RetryOptions propriedade no objeto de ConnectionPolicy Olá se você desejar tooignore Olá retryAfter tempo retornado pelo servidor entre as tentativas de saudação.</span><span class="sxs-lookup"><span data-stu-id="763d7-168">A fixed retry interval time can now be set as part of hello RetryOptions property on hello ConnectionPolicy object if you want tooignore hello retryAfter time returned by server between hello retries.</span></span> <span data-ttu-id="763d7-169">Banco de dados do Azure Cosmos agora aguarda um máximo de 30 segundos para cada solicitação que está sendo limitado (independentemente da contagem de repetição) e retorna a resposta de saudação com código de erro 429.</span><span class="sxs-lookup"><span data-stu-id="763d7-169">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns hello response with error code 429.</span></span> <span data-ttu-id="763d7-170">Também pode ser substituído neste momento no hello RetryOptions propriedade no objeto ConnectionPolicy.</span><span class="sxs-lookup"><span data-stu-id="763d7-170">This time can also be overridden in hello RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="763d7-171">Cosmos DB agora retorna x-ms-acelerador--contagem de repetição e x-ms-throttle-retry-wait-time-ms como cabeçalhos de resposta de saudação na limitação de saudação de toodenote cada solicitação repetir contagem e hello tempo cumulativo Olá solicitação espera entre as tentativas de saudação.</span><span class="sxs-lookup"><span data-stu-id="763d7-171">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as hello response headers in every request toodenote hello throttle retry count and hello cumulative time hello request waited between hello retries.</span></span>
* <span data-ttu-id="763d7-172">Olá classe RetryOptions foi adicionado, expondo a propriedade de RetryOptions Olá na classe de ConnectionPolicy Olá que pode ser usado toooverride alguns padrão Olá opções de repetição.</span><span class="sxs-lookup"><span data-stu-id="763d7-172">hello RetryOptions class was added, exposing hello RetryOptions property on hello ConnectionPolicy class that can be used toooverride some of hello default retry options.</span></span>

### <span data-ttu-id="763d7-173"><a name="1.8.0"/>1.8.0</a></span><span class="sxs-lookup"><span data-stu-id="763d7-173"><a name="1.8.0"/>1.8.0</a></span></span>
* <span data-ttu-id="763d7-174">Suporte adicionado Olá para contas do banco de dados de várias regiões.</span><span class="sxs-lookup"><span data-stu-id="763d7-174">Added hello support for multi-region database accounts.</span></span>

### <span data-ttu-id="763d7-175"><a name="1.7.0"/>1.7.0</a></span><span class="sxs-lookup"><span data-stu-id="763d7-175"><a name="1.7.0"/>1.7.0</a></span></span>
* <span data-ttu-id="763d7-176">Olá adicionado suporte para o recurso de tooLive(TTL) de tempo para documentos.</span><span class="sxs-lookup"><span data-stu-id="763d7-176">Added hello support for Time tooLive(TTL) feature for documents.</span></span>

### <span data-ttu-id="763d7-177"><a name="1.6.0"/>1.6.0</a></span><span class="sxs-lookup"><span data-stu-id="763d7-177"><a name="1.6.0"/>1.6.0</a></span></span>
* <span data-ttu-id="763d7-178">Implementação de [coleções particionadas](partition-data.md) e [níveis de desempenho definidos pelo usuário](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="763d7-178">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <span data-ttu-id="763d7-179"><a name="1.5.6"/>1.5.6</a></span><span class="sxs-lookup"><span data-stu-id="763d7-179"><a name="1.5.6"/>1.5.6</a></span></span>
* <span data-ttu-id="763d7-180">Correção do bug RangePartitionResolver.resolveForRead onde ele não estava retornando links devido concat incorreta de tooa de resultados.</span><span class="sxs-lookup"><span data-stu-id="763d7-180">Fixed RangePartitionResolver.resolveForRead bug where it was not returning links due tooa bad concat of results.</span></span>

### <span data-ttu-id="763d7-181"><a name="1.5.5"/>1.5.5</a></span><span class="sxs-lookup"><span data-stu-id="763d7-181"><a name="1.5.5"/>1.5.5</a></span></span>
* <span data-ttu-id="763d7-182">hashPartitionResolver resolveForRead() corrigido: quando nenhuma chave de partição fornecida estava emitindo exceção, em vez de retornar uma lista de todos os links registrados.</span><span class="sxs-lookup"><span data-stu-id="763d7-182">Fixed hashParitionResolver resolveForRead(): When no partition key supplied was throwing exception, instead of returning a list of all registered links.</span></span>

### <span data-ttu-id="763d7-183"><a name="1.5.4"/>1.5.4</a></span><span class="sxs-lookup"><span data-stu-id="763d7-183"><a name="1.5.4"/>1.5.4</a></span></span>
* <span data-ttu-id="763d7-184">Corrige o problema [#100](https://github.com/Azure/azure-documentdb-node/issues/100) -agente dedicado de HTTPS: evitar modificar globais do agente para fins de banco de dados do Azure Cosmos hello.</span><span class="sxs-lookup"><span data-stu-id="763d7-184">Fixes issue [#100](https://github.com/Azure/azure-documentdb-node/issues/100) - Dedicated HTTPS Agent: Avoid modifying hello global agent for Azure Cosmos DB purposes.</span></span> <span data-ttu-id="763d7-185">Use um agente dedicado para todas as solicitações do lib hello.</span><span class="sxs-lookup"><span data-stu-id="763d7-185">Use a dedicated agent for all of hello lib’s requests.</span></span>

### <span data-ttu-id="763d7-186"><a name="1.5.3"/>1.5.3</a></span><span class="sxs-lookup"><span data-stu-id="763d7-186"><a name="1.5.3"/>1.5.3</a></span></span>
* <span data-ttu-id="763d7-187">Corrige o problema [nº 81](https://github.com/Azure/azure-documentdb-node/issues/81) — trate corretamente os traços em IDs de mídia.</span><span class="sxs-lookup"><span data-stu-id="763d7-187">Fixes issue [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - Properly handle dashes in media ids.</span></span>

### <span data-ttu-id="763d7-188"><a name="1.5.2"/>1.5.2</a></span><span class="sxs-lookup"><span data-stu-id="763d7-188"><a name="1.5.2"/>1.5.2</a></span></span>
* <span data-ttu-id="763d7-189">Corrige o problema [nº 95](https://github.com/Azure/azure-documentdb-node/issues/95) — aviso de perda do ouvinte EventEmitter.</span><span class="sxs-lookup"><span data-stu-id="763d7-189">Fixes issue [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter listener leak warning.</span></span>

### <span data-ttu-id="763d7-190"><a name="1.5.1"/>1.5.1</a></span><span class="sxs-lookup"><span data-stu-id="763d7-190"><a name="1.5.1"/>1.5.1</a></span></span>
* <span data-ttu-id="763d7-191">Corrige o problema [&#92;](https://github.com/Azure/azure-documentdb-node/issues/90) -renomear a pasta Hash toohash para sistemas diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="763d7-191">Fixes issue [#92](https://github.com/Azure/azure-documentdb-node/issues/90) - rename folder Hash toohash for case-sensitive systems.</span></span>

### <span data-ttu-id="763d7-192"><a name="1.5.0"/>1.5.0</a></span><span class="sxs-lookup"><span data-stu-id="763d7-192"><a name="1.5.0"/>1.5.0</a></span></span>
* <span data-ttu-id="763d7-193">Implemente o suporte a fragmentação ao adicionar os resolvedores de partição de hash e de intervalo.</span><span class="sxs-lookup"><span data-stu-id="763d7-193">Implement sharding support by adding hash & range partition resolvers.</span></span>

### <span data-ttu-id="763d7-194"><a name="1.4.0"/>1.4.0</a></span><span class="sxs-lookup"><span data-stu-id="763d7-194"><a name="1.4.0"/>1.4.0</a></span></span>
* <span data-ttu-id="763d7-195">Implementar o Upsert.</span><span class="sxs-lookup"><span data-stu-id="763d7-195">Implement Upsert.</span></span> <span data-ttu-id="763d7-196">Novos métodos upsertXXX em documentClient.</span><span class="sxs-lookup"><span data-stu-id="763d7-196">New upsertXXX methods on documentClient.</span></span>

### <span data-ttu-id="763d7-197"><a name="1.3.0"/>1.3.0</a></span><span class="sxs-lookup"><span data-stu-id="763d7-197"><a name="1.3.0"/>1.3.0</a></span></span>
* <span data-ttu-id="763d7-198">Números de versão toobring ignorada no alinhamento com outros SDKs.</span><span class="sxs-lookup"><span data-stu-id="763d7-198">Skipped toobring version numbers in alignment with other SDKs.</span></span>

### <span data-ttu-id="763d7-199"><a name="1.2.2"/>1.2.2</a></span><span class="sxs-lookup"><span data-stu-id="763d7-199"><a name="1.2.2"/>1.2.2</a></span></span>
* <span data-ttu-id="763d7-200">Divisão p promete repositório toonew do wrapper.</span><span class="sxs-lookup"><span data-stu-id="763d7-200">Split Q promises wrapper toonew repository.</span></span>
* <span data-ttu-id="763d7-201">Atualize o arquivo toopackage do registro npm.</span><span class="sxs-lookup"><span data-stu-id="763d7-201">Update toopackage file for npm registry.</span></span>

### <span data-ttu-id="763d7-202"><a name="1.2.1"/>1.2.1</a></span><span class="sxs-lookup"><span data-stu-id="763d7-202"><a name="1.2.1"/>1.2.1</a></span></span>
* <span data-ttu-id="763d7-203">Implementa o roteamento com base em ID.</span><span class="sxs-lookup"><span data-stu-id="763d7-203">Implements ID Based Routing.</span></span>
* <span data-ttu-id="763d7-204">Corrige o problema [nº 49](https://github.com/Azure/azure-documentdb-node/issues/49) - a propriedade atual está em conflito com o método atual().</span><span class="sxs-lookup"><span data-stu-id="763d7-204">Fixes Issue [#49](https://github.com/Azure/azure-documentdb-node/issues/49) - current property conflicts with method current().</span></span>

### <span data-ttu-id="763d7-205"><a name="1.2.0"/>1.2.0</a></span><span class="sxs-lookup"><span data-stu-id="763d7-205"><a name="1.2.0"/>1.2.0</a></span></span>
* <span data-ttu-id="763d7-206">Suporte adicionado para índice geoespaciais.</span><span class="sxs-lookup"><span data-stu-id="763d7-206">Added support for GeoSpatial index.</span></span>
* <span data-ttu-id="763d7-207">Valida a propriedade de ID de todos os recursos.</span><span class="sxs-lookup"><span data-stu-id="763d7-207">Validates id property for all resources.</span></span> <span data-ttu-id="763d7-208">As IDs de recursos não podem conter caracteres ?, /, #, &#47;&#47; ou terminar com um espaço.</span><span class="sxs-lookup"><span data-stu-id="763d7-208">Ids for resources cannot contain ?, /, #, &#47;&#47;, characters or end with a space.</span></span>
* <span data-ttu-id="763d7-209">Adiciona novo tooResourceResponse "andamento de transformação de índice" de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="763d7-209">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <span data-ttu-id="763d7-210"><a name="1.1.0"/>1.1.0</a></span><span class="sxs-lookup"><span data-stu-id="763d7-210"><a name="1.1.0"/>1.1.0</a></span></span>
* <span data-ttu-id="763d7-211">Implementa a política de indexação V2.</span><span class="sxs-lookup"><span data-stu-id="763d7-211">Implements V2 indexing policy.</span></span>

### <span data-ttu-id="763d7-212"><a name="1.0.3"/>1.0.3</a></span><span class="sxs-lookup"><span data-stu-id="763d7-212"><a name="1.0.3"/>1.0.3</a></span></span>
* <span data-ttu-id="763d7-213">Problema [&#40;](https://github.com/Azure/azure-documentdb-node/issues/40) - implementado eslint e Assistente de configurações no núcleo do hello e promise SDK.</span><span class="sxs-lookup"><span data-stu-id="763d7-213">Issue [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - Implemented eslint and grunt configurations in hello core and promise SDK.</span></span>

### <span data-ttu-id="763d7-214"><a name="1.0.2"/>1.0.2</a></span><span class="sxs-lookup"><span data-stu-id="763d7-214"><a name="1.0.2"/>1.0.2</a></span></span>
* <span data-ttu-id="763d7-215">Problema [nº 45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promessa de wrapper não inclui o cabeçalho com erro.</span><span class="sxs-lookup"><span data-stu-id="763d7-215">Issue [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promises wrapper does not include header with error.</span></span>

### <span data-ttu-id="763d7-216"><a name="1.0.1"/>1.0.1</a></span><span class="sxs-lookup"><span data-stu-id="763d7-216"><a name="1.0.1"/>1.0.1</a></span></span>
* <span data-ttu-id="763d7-217">Implementado tooquery capacidade conflitos adicionando readConflicts, readConflictAsync e queryConflicts.</span><span class="sxs-lookup"><span data-stu-id="763d7-217">Implemented ability tooquery for conflicts by adding readConflicts, readConflictAsync, and queryConflicts.</span></span>
* <span data-ttu-id="763d7-218">Documentação da API atualizada.</span><span class="sxs-lookup"><span data-stu-id="763d7-218">Updated API documentation.</span></span>
* <span data-ttu-id="763d7-219">Problema [nº 41](https://github.com/Azure/azure-documentdb-node/issues/41) - Erro client.createDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="763d7-219">Issue [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync error.</span></span>

### <span data-ttu-id="763d7-220"><a name="1.0.0"/>1.0.0</a></span><span class="sxs-lookup"><span data-stu-id="763d7-220"><a name="1.0.0"/>1.0.0</a></span></span>
* <span data-ttu-id="763d7-221">SDK DO GA.</span><span class="sxs-lookup"><span data-stu-id="763d7-221">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="763d7-222">Datas de lançamento e desativação</span><span class="sxs-lookup"><span data-stu-id="763d7-222">Release & Retirement Dates</span></span>
<span data-ttu-id="763d7-223">A Microsoft fornece notificação pelo menos **12 meses** antes de desativar um SDK na versão mais recente/suporte ordem toosmooth Olá transição tooa.</span><span class="sxs-lookup"><span data-stu-id="763d7-223">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="763d7-224">Novos recursos e funcionalidade e as otimizações são adicionadas apenas toohello atual SDK, como tal, é recomendável que você sempre atualize toohello mais recente versão do SDK mais cedo possível.</span><span class="sxs-lookup"><span data-stu-id="763d7-224">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommended that you always upgrade toohello latest SDK version as early as possible.</span></span>

<span data-ttu-id="763d7-225">Qualquer solicitação tooCosmos banco de dados usando um SDK obsoleto é rejeitados pelo serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="763d7-225">Any request tooCosmos DB using a retired SDK is be rejected by hello service.</span></span>

<br/>

| <span data-ttu-id="763d7-226">Versão</span><span class="sxs-lookup"><span data-stu-id="763d7-226">Version</span></span> | <span data-ttu-id="763d7-227">Data do lançamento</span><span class="sxs-lookup"><span data-stu-id="763d7-227">Release Date</span></span> | <span data-ttu-id="763d7-228">Data de desativação</span><span class="sxs-lookup"><span data-stu-id="763d7-228">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="763d7-229">1.12.2</span><span class="sxs-lookup"><span data-stu-id="763d7-229">1.12.2</span></span>](#1.12.2) |<span data-ttu-id="763d7-230">10 de agosto de 2017</span><span class="sxs-lookup"><span data-stu-id="763d7-230">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="763d7-231">1.12.1</span><span class="sxs-lookup"><span data-stu-id="763d7-231">1.12.1</span></span>](#1.12.1) |<span data-ttu-id="763d7-232">10 de agosto de 2017</span><span class="sxs-lookup"><span data-stu-id="763d7-232">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="763d7-233">1.12.0</span><span class="sxs-lookup"><span data-stu-id="763d7-233">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="763d7-234">10 de maio de 2017</span><span class="sxs-lookup"><span data-stu-id="763d7-234">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="763d7-235">1.11.0</span><span class="sxs-lookup"><span data-stu-id="763d7-235">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="763d7-236">16 de março de 2017</span><span class="sxs-lookup"><span data-stu-id="763d7-236">March 16, 2017</span></span> |--- |
| [<span data-ttu-id="763d7-237">1.10.2</span><span class="sxs-lookup"><span data-stu-id="763d7-237">1.10.2</span></span>](#1.10.2) |<span data-ttu-id="763d7-238">27 de janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="763d7-238">January 27, 2017</span></span> |--- |
| [<span data-ttu-id="763d7-239">1.10.1</span><span class="sxs-lookup"><span data-stu-id="763d7-239">1.10.1</span></span>](#1.10.1) |<span data-ttu-id="763d7-240">22 de dezembro de 2016</span><span class="sxs-lookup"><span data-stu-id="763d7-240">December 22, 2016</span></span> |--- |
| [<span data-ttu-id="763d7-241">1.10.0</span><span class="sxs-lookup"><span data-stu-id="763d7-241">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="763d7-242">3 de outubro de 2016</span><span class="sxs-lookup"><span data-stu-id="763d7-242">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="763d7-243">1.9.0</span><span class="sxs-lookup"><span data-stu-id="763d7-243">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="763d7-244">07 de julho de 2016</span><span class="sxs-lookup"><span data-stu-id="763d7-244">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="763d7-245">1.8.0</span><span class="sxs-lookup"><span data-stu-id="763d7-245">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="763d7-246">14 de junho de 2016</span><span class="sxs-lookup"><span data-stu-id="763d7-246">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="763d7-247">1.7.0</span><span class="sxs-lookup"><span data-stu-id="763d7-247">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="763d7-248">26 de abril de 2016</span><span class="sxs-lookup"><span data-stu-id="763d7-248">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="763d7-249">1.6.0</span><span class="sxs-lookup"><span data-stu-id="763d7-249">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="763d7-250">29 de março de 2016</span><span class="sxs-lookup"><span data-stu-id="763d7-250">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="763d7-251">1.5.6</span><span class="sxs-lookup"><span data-stu-id="763d7-251">1.5.6</span></span>](#1.5.6) |<span data-ttu-id="763d7-252">08 de março de 2016</span><span class="sxs-lookup"><span data-stu-id="763d7-252">March 08, 2016</span></span> |--- |
| [<span data-ttu-id="763d7-253">1.5.5</span><span class="sxs-lookup"><span data-stu-id="763d7-253">1.5.5</span></span>](#1.5.5) |<span data-ttu-id="763d7-254">02 de fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="763d7-254">February 02, 2016</span></span> |--- |
| [<span data-ttu-id="763d7-255">1.5.4</span><span class="sxs-lookup"><span data-stu-id="763d7-255">1.5.4</span></span>](#1.5.4) |<span data-ttu-id="763d7-256">1 de fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="763d7-256">February 01, 2016</span></span> |--- |
| [<span data-ttu-id="763d7-257">1.5.2</span><span class="sxs-lookup"><span data-stu-id="763d7-257">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="763d7-258">26 de janeiro de 2016</span><span class="sxs-lookup"><span data-stu-id="763d7-258">January 26, 2016</span></span> |--- |
| [<span data-ttu-id="763d7-259">1.5.2</span><span class="sxs-lookup"><span data-stu-id="763d7-259">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="763d7-260">22 de janeiro de 2016</span><span class="sxs-lookup"><span data-stu-id="763d7-260">January 22, 2016</span></span> |--- |
| [<span data-ttu-id="763d7-261">1.5.1</span><span class="sxs-lookup"><span data-stu-id="763d7-261">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="763d7-262">4 de janeiro de 2016</span><span class="sxs-lookup"><span data-stu-id="763d7-262">January 4, 2016</span></span> |--- |
| [<span data-ttu-id="763d7-263">1.5.0</span><span class="sxs-lookup"><span data-stu-id="763d7-263">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="763d7-264">31 de dezembro de 2015</span><span class="sxs-lookup"><span data-stu-id="763d7-264">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="763d7-265">1.4.0</span><span class="sxs-lookup"><span data-stu-id="763d7-265">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="763d7-266">06 de outubro de 2015</span><span class="sxs-lookup"><span data-stu-id="763d7-266">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="763d7-267">1.3.0</span><span class="sxs-lookup"><span data-stu-id="763d7-267">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="763d7-268">06 de outubro de 2015</span><span class="sxs-lookup"><span data-stu-id="763d7-268">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="763d7-269">1.2.2</span><span class="sxs-lookup"><span data-stu-id="763d7-269">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="763d7-270">10 de setembro de 2015</span><span class="sxs-lookup"><span data-stu-id="763d7-270">September 10, 2015</span></span> |--- |
| [<span data-ttu-id="763d7-271">1.2.1</span><span class="sxs-lookup"><span data-stu-id="763d7-271">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="763d7-272">15 de agosto de 2015</span><span class="sxs-lookup"><span data-stu-id="763d7-272">August 15, 2015</span></span> |--- |
| [<span data-ttu-id="763d7-273">1.2.0</span><span class="sxs-lookup"><span data-stu-id="763d7-273">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="763d7-274">5 de agosto de 2015</span><span class="sxs-lookup"><span data-stu-id="763d7-274">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="763d7-275">1.1.0</span><span class="sxs-lookup"><span data-stu-id="763d7-275">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="763d7-276">9 de julho de 2015</span><span class="sxs-lookup"><span data-stu-id="763d7-276">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="763d7-277">1.0.3</span><span class="sxs-lookup"><span data-stu-id="763d7-277">1.0.3</span></span>](#1.0.3) |<span data-ttu-id="763d7-278">04 de junho de 2015</span><span class="sxs-lookup"><span data-stu-id="763d7-278">June 04, 2015</span></span> |--- |
| [<span data-ttu-id="763d7-279">1.0.2</span><span class="sxs-lookup"><span data-stu-id="763d7-279">1.0.2</span></span>](#1.0.2) |<span data-ttu-id="763d7-280">23 de maio de 2015</span><span class="sxs-lookup"><span data-stu-id="763d7-280">May 23, 2015</span></span> |--- |
| [<span data-ttu-id="763d7-281">1.0.1</span><span class="sxs-lookup"><span data-stu-id="763d7-281">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="763d7-282">15 de maio de 2015</span><span class="sxs-lookup"><span data-stu-id="763d7-282">May 15, 2015</span></span> |--- |
| [<span data-ttu-id="763d7-283">1.0.0</span><span class="sxs-lookup"><span data-stu-id="763d7-283">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="763d7-284">8 de abril de 2015</span><span class="sxs-lookup"><span data-stu-id="763d7-284">April 08, 2015</span></span> |--- |

## <a name="faq"></a><span data-ttu-id="763d7-285">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="763d7-285">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="763d7-286">Consulte também</span><span class="sxs-lookup"><span data-stu-id="763d7-286">See also</span></span>
<span data-ttu-id="763d7-287">toolearn mais sobre o banco de dados do Cosmos, consulte [banco de dados do Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) página de serviço.</span><span class="sxs-lookup"><span data-stu-id="763d7-287">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

