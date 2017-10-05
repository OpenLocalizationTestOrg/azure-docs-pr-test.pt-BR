---
title: API de Node.js do Azure Cosmos DB, SDK & recursos | Microsoft Docs
description: "Saiba tudo sobre o SDK e a API do Node.js, incluindo as datas de lançamento, as datas de desativação e as alterações feitas entre cada versão do SDK do Node.js para o Azure Cosmos DB."
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
ms.openlocfilehash: 4376a5c07b5f00311ce0fe3c0056efdf79c273f9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a><span data-ttu-id="88923-103">SDK de Node.js do Azure Cosmos DB: Notas de versão e recursos</span><span class="sxs-lookup"><span data-stu-id="88923-103">Azure Cosmos DB Node.js SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="88923-104">.NET</span><span class="sxs-lookup"><span data-stu-id="88923-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="88923-105">Feed de alterações do .NET</span><span class="sxs-lookup"><span data-stu-id="88923-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="88923-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="88923-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="88923-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="88923-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="88923-108">Java</span><span class="sxs-lookup"><span data-stu-id="88923-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="88923-109">Python</span><span class="sxs-lookup"><span data-stu-id="88923-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="88923-110">REST</span><span class="sxs-lookup"><span data-stu-id="88923-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="88923-111">Provedor de recursos REST</span><span class="sxs-lookup"><span data-stu-id="88923-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="88923-112">SQL</span><span class="sxs-lookup"><span data-stu-id="88923-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="88923-113">**Baixar o SDK**</span><span class="sxs-lookup"><span data-stu-id="88923-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="88923-114">NPM</span><span class="sxs-lookup"><span data-stu-id="88923-114">NPM</span></span>](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td><span data-ttu-id="88923-115">**Documentação da API**</span><span class="sxs-lookup"><span data-stu-id="88923-115">**API documentation**</span></span></td><td>[<span data-ttu-id="88923-116">Documentação de referência da API do Node.js</span><span class="sxs-lookup"><span data-stu-id="88923-116">Node.js API reference documentation</span></span>](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td><span data-ttu-id="88923-117">**Instruções de instalação do SDK**</span><span class="sxs-lookup"><span data-stu-id="88923-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="88923-118">Instruções de instalação</span><span class="sxs-lookup"><span data-stu-id="88923-118">Installation instructions</span></span>](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td><span data-ttu-id="88923-119">**Contribuir para o SDK**</span><span class="sxs-lookup"><span data-stu-id="88923-119">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="88923-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="88923-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td><span data-ttu-id="88923-121">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="88923-121">**Samples**</span></span></td><td>[<span data-ttu-id="88923-122">Exemplos de código do Node.js</span><span class="sxs-lookup"><span data-stu-id="88923-122">Node.js code samples</span></span>](documentdb-nodejs-samples.md)</td></tr>

<tr><td><span data-ttu-id="88923-123">**Tutorial de introdução**</span><span class="sxs-lookup"><span data-stu-id="88923-123">**Get started tutorial**</span></span></td><td>[<span data-ttu-id="88923-124">Introdução ao SDK do Node.js</span><span class="sxs-lookup"><span data-stu-id="88923-124">Get started with the Node.js SDK</span></span>](documentdb-nodejs-get-started.md)</td></tr>

<tr><td><span data-ttu-id="88923-125">**Tutorial do aplicativo Web**</span><span class="sxs-lookup"><span data-stu-id="88923-125">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="88923-126">Criar um aplicativo web Node.js usando o Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="88923-126">Build a Node.js web application using Azure Cosmos DB</span></span>](documentdb-nodejs-application.md)</td></tr>

<tr><td><span data-ttu-id="88923-127">**Plataforma atual com suporte**</span><span class="sxs-lookup"><span data-stu-id="88923-127">**Current supported platform**</span></span></td><td> 
[<span data-ttu-id="88923-128">Node.js v6.x</span><span class="sxs-lookup"><span data-stu-id="88923-128">Node.js v6.x</span></span>](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[<span data-ttu-id="88923-129">Node.js v4.2.0</span><span class="sxs-lookup"><span data-stu-id="88923-129">Node.js v4.2.0</span></span>](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[<span data-ttu-id="88923-130">Node.js v0.12</span><span class="sxs-lookup"><span data-stu-id="88923-130">Node.js v0.12</span></span>](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
<span data-ttu-id="88923-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span><span class="sxs-lookup"><span data-stu-id="88923-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="88923-132">Notas de versão</span><span class="sxs-lookup"><span data-stu-id="88923-132">Release notes</span></span>

### <span data-ttu-id="88923-133"><a name="1.12.2"/>1.12.2</a></span><span class="sxs-lookup"><span data-stu-id="88923-133"><a name="1.12.2"/>1.12.2</a></span></span>
*   <span data-ttu-id="88923-134">documentação do npm corrigida.</span><span class="sxs-lookup"><span data-stu-id="88923-134">npm documentation fixed.</span></span>

### <span data-ttu-id="88923-135"><a name="1.12.1"/>1.12.1</a></span><span class="sxs-lookup"><span data-stu-id="88923-135"><a name="1.12.1"/>1.12.1</a></span></span>
* <span data-ttu-id="88923-136">Correção de um bug no executeStoredProcedure, em que documentos envolvidos tinham caracteres especiais Unicode (LS, PS).</span><span class="sxs-lookup"><span data-stu-id="88923-136">Fixed a bug in executeStoredProcedure where documents involved had special Unicode characters (LS, PS).</span></span>
* <span data-ttu-id="88923-137">Correção de um bug no tratamento de documentos com caracteres Unicode na chave de partição.</span><span class="sxs-lookup"><span data-stu-id="88923-137">Fixed a bug in handling documents with Unicode characters in the partition key.</span></span>
* <span data-ttu-id="88923-138">Suporte corrigido para criar coleções com a mídia de nome.</span><span class="sxs-lookup"><span data-stu-id="88923-138">Fixed support for creating collections with the name media.</span></span> <span data-ttu-id="88923-139">Problema nº 114 do Github.</span><span class="sxs-lookup"><span data-stu-id="88923-139">Github issue #114.</span></span>
* <span data-ttu-id="88923-140">Suporte fixo para o token de autorização de permissão.</span><span class="sxs-lookup"><span data-stu-id="88923-140">Fixed support for permission authorization token.</span></span> <span data-ttu-id="88923-141">Problema nº 178 do Github.</span><span class="sxs-lookup"><span data-stu-id="88923-141">Github issue #178.</span></span>

### <span data-ttu-id="88923-142"><a name="1.12.0"/>1.12.0</a></span><span class="sxs-lookup"><span data-stu-id="88923-142"><a name="1.12.0"/>1.12.0</a></span></span>
* <span data-ttu-id="88923-143">Foi adicionado suporte a um novo [nível de consistência](consistency-levels.md) chamado ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="88923-143">Added support for a new [consistency level](consistency-levels.md) called ConsistentPrefix.</span></span>
* <span data-ttu-id="88923-144">Foi adicionado suporte para UriFactory.</span><span class="sxs-lookup"><span data-stu-id="88923-144">Added support for UriFactory.</span></span>
* <span data-ttu-id="88923-145">Correção de um bug de suporte ao Unicode.</span><span class="sxs-lookup"><span data-stu-id="88923-145">Fixed a Unicode support bug.</span></span> <span data-ttu-id="88923-146">Problema nº 171 do Github.</span><span class="sxs-lookup"><span data-stu-id="88923-146">GitHub issue #171.</span></span>

### <span data-ttu-id="88923-147"><a name="1.11.0"/>1.11.0</a></span><span class="sxs-lookup"><span data-stu-id="88923-147"><a name="1.11.0"/>1.11.0</a></span></span>
* <span data-ttu-id="88923-148">Adição do suporte para consultas de agregação (COUNT, MIN, MAX, SUM e AVG).</span><span class="sxs-lookup"><span data-stu-id="88923-148">Added the support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="88923-149">Adição da opção para controlar o grau de paralelismo em consultas de partição cruzada.</span><span class="sxs-lookup"><span data-stu-id="88923-149">Added the option for controlling degree of parallelism for cross partition queries.</span></span>
* <span data-ttu-id="88923-150">Adição da opção para desabilitar a verificação do SSL quando executada no Emulador do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="88923-150">Added the option for disabling SSL verification when running against Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="88923-151">Taxa de transferência mínima reduzida em coleções particionadas de 10.100 RU/s a 2500 RU/s.</span><span class="sxs-lookup"><span data-stu-id="88923-151">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>
* <span data-ttu-id="88923-152">Correção do bug de token de continuação para a coleta de partição única.</span><span class="sxs-lookup"><span data-stu-id="88923-152">Fixed the continuation token bug for single partition collection.</span></span> <span data-ttu-id="88923-153">Problema nº 107 do Github.</span><span class="sxs-lookup"><span data-stu-id="88923-153">Github issue #107.</span></span>
* <span data-ttu-id="88923-154">Correção do bug executeStoredProcedure no tratamento de 0 como parâmetro único.</span><span class="sxs-lookup"><span data-stu-id="88923-154">Fixed the executeStoredProcedure bug in handling 0 as single param.</span></span> <span data-ttu-id="88923-155">Problema nº 155 do Github.</span><span class="sxs-lookup"><span data-stu-id="88923-155">Github issue #155.</span></span>

### <span data-ttu-id="88923-156"><a name="1.10.2"/>1.10.2</a></span><span class="sxs-lookup"><span data-stu-id="88923-156"><a name="1.10.2"/>1.10.2</a></span></span>
* <span data-ttu-id="88923-157">Cabeçalho de agente do usuário fixo para incluir a versão do SDK.</span><span class="sxs-lookup"><span data-stu-id="88923-157">Fixed user-agent header to include the SDK version.</span></span>
* <span data-ttu-id="88923-158">Limpeza de código secundária.</span><span class="sxs-lookup"><span data-stu-id="88923-158">Minor code cleanup.</span></span>

### <span data-ttu-id="88923-159"><a name="1.10.1"/>1.10.1</a></span><span class="sxs-lookup"><span data-stu-id="88923-159"><a name="1.10.1"/>1.10.1</a></span></span>
* <span data-ttu-id="88923-160">Desabilitar verificação de SSL ao usar o SDK visando o emulator(hostname=localhost).</span><span class="sxs-lookup"><span data-stu-id="88923-160">Disabling SSL verification when using the SDK to target the emulator(hostname=localhost).</span></span>
* <span data-ttu-id="88923-161">Adicionado suporte para habilitar o registro em log de script durante a execução do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="88923-161">Added support for enabling script logging during stored procedure execution.</span></span>

### <span data-ttu-id="88923-162"><a name="1.10.0"/>1.10.0</a></span><span class="sxs-lookup"><span data-stu-id="88923-162"><a name="1.10.0"/>1.10.0</a></span></span>
* <span data-ttu-id="88923-163">Adicionado suporte para várias consultas paralelas de partição.</span><span class="sxs-lookup"><span data-stu-id="88923-163">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="88923-164">Adição de suporte a consultas TOP/ORDER BY de coleções particionadas.</span><span class="sxs-lookup"><span data-stu-id="88923-164">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>

### <span data-ttu-id="88923-165"><a name="1.9.0"/>1.9.0</a></span><span class="sxs-lookup"><span data-stu-id="88923-165"><a name="1.9.0"/>1.9.0</a></span></span>
* <span data-ttu-id="88923-166">Suporte à política de repetições para solicitações limitadas adicionado.</span><span class="sxs-lookup"><span data-stu-id="88923-166">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="88923-167">(As solicitações limitadas recebem uma exceção muito grande de taxa de solicitação, código de erro 429.) Por padrão, o Azure Cosmos DB tenta cada solicitação novamente nove vezes quando o código de erro 429 é encontrado, respeitando o tempo retryAfter no cabeçalho de resposta.</span><span class="sxs-lookup"><span data-stu-id="88923-167">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring the retryAfter time in the response header.</span></span> <span data-ttu-id="88923-168">Um intervalo de repetição fixo agora poderá ser definido como parte da propriedade RetryOptions no objeto ConnectionPolicy, se você quiser ignorar o tempo retryAfter retornado pelo servidor entre as repetições.</span><span class="sxs-lookup"><span data-stu-id="88923-168">A fixed retry interval time can now be set as part of the RetryOptions property on the ConnectionPolicy object if you want to ignore the retryAfter time returned by server between the retries.</span></span> <span data-ttu-id="88923-169">O Azure Cosmos DB agora aguarda um período máximo de 30 segundos para cada solicitação que está sendo limitada (independentemente da contagem de repetições) e retorna a resposta com o código de erro 429.</span><span class="sxs-lookup"><span data-stu-id="88923-169">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns the response with error code 429.</span></span> <span data-ttu-id="88923-170">Esse tempo também pode ser substituído na propriedade RetryOptions, no objeto ConnectionPolicy.</span><span class="sxs-lookup"><span data-stu-id="88923-170">This time can also be overridden in the RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="88923-171">O Cosmos DB agora retorna x-ms-throttle-retry-count e x-ms-throttle-retry-wait-time-ms como os cabeçalhos de resposta em cada solicitação para indicar a contagem de repetições restritas e o tempo cumulativo que a solicitação aguardou entre as tentativas.</span><span class="sxs-lookup"><span data-stu-id="88923-171">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as the response headers in every request to denote the throttle retry count and the cumulative time the request waited between the retries.</span></span>
* <span data-ttu-id="88923-172">A classe RetryOptions foi adicionada, expondo a propriedade RetryOptions na classe ConnectionPolicy, que pode ser usada para substituir algumas das opções de repetição padrão.</span><span class="sxs-lookup"><span data-stu-id="88923-172">The RetryOptions class was added, exposing the RetryOptions property on the ConnectionPolicy class that can be used to override some of the default retry options.</span></span>

### <span data-ttu-id="88923-173"><a name="1.8.0"/>1.8.0</a></span><span class="sxs-lookup"><span data-stu-id="88923-173"><a name="1.8.0"/>1.8.0</a></span></span>
* <span data-ttu-id="88923-174">Suporte adicionado para contas de banco de dados de várias regiões.</span><span class="sxs-lookup"><span data-stu-id="88923-174">Added the support for multi-region database accounts.</span></span>

### <span data-ttu-id="88923-175"><a name="1.7.0"/>1.7.0</a></span><span class="sxs-lookup"><span data-stu-id="88923-175"><a name="1.7.0"/>1.7.0</a></span></span>
* <span data-ttu-id="88923-176">Adicionado o suporte para o recurso TTL (tempo de vida) para documentos.</span><span class="sxs-lookup"><span data-stu-id="88923-176">Added the support for Time To Live(TTL) feature for documents.</span></span>

### <span data-ttu-id="88923-177"><a name="1.6.0"/>1.6.0</a></span><span class="sxs-lookup"><span data-stu-id="88923-177"><a name="1.6.0"/>1.6.0</a></span></span>
* <span data-ttu-id="88923-178">Implementação de [coleções particionadas](partition-data.md) e [níveis de desempenho definidos pelo usuário](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="88923-178">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <span data-ttu-id="88923-179"><a name="1.5.6"/>1.5.6</a></span><span class="sxs-lookup"><span data-stu-id="88923-179"><a name="1.5.6"/>1.5.6</a></span></span>
* <span data-ttu-id="88923-180">O bug RangePartitionResolver.resolveForRead foi corrigido, pois ele não estava retornando links devido a uma concatenação incorreta dos resultados.</span><span class="sxs-lookup"><span data-stu-id="88923-180">Fixed RangePartitionResolver.resolveForRead bug where it was not returning links due to a bad concat of results.</span></span>

### <span data-ttu-id="88923-181"><a name="1.5.5"/>1.5.5</a></span><span class="sxs-lookup"><span data-stu-id="88923-181"><a name="1.5.5"/>1.5.5</a></span></span>
* <span data-ttu-id="88923-182">hashPartitionResolver resolveForRead() corrigido: quando nenhuma chave de partição fornecida estava emitindo exceção, em vez de retornar uma lista de todos os links registrados.</span><span class="sxs-lookup"><span data-stu-id="88923-182">Fixed hashParitionResolver resolveForRead(): When no partition key supplied was throwing exception, instead of returning a list of all registered links.</span></span>

### <span data-ttu-id="88923-183"><a name="1.5.4"/>1.5.4</a></span><span class="sxs-lookup"><span data-stu-id="88923-183"><a name="1.5.4"/>1.5.4</a></span></span>
* <span data-ttu-id="88923-184">Corrige o problema [nº 100](https://github.com/Azure/azure-documentdb-node/issues/100) — Agente HTTPS Dedicado: evite modificar o agente global para os fins do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="88923-184">Fixes issue [#100](https://github.com/Azure/azure-documentdb-node/issues/100) - Dedicated HTTPS Agent: Avoid modifying the global agent for Azure Cosmos DB purposes.</span></span> <span data-ttu-id="88923-185">Use um agente dedicado para todas as solicitações da biblioteca.</span><span class="sxs-lookup"><span data-stu-id="88923-185">Use a dedicated agent for all of the lib’s requests.</span></span>

### <span data-ttu-id="88923-186"><a name="1.5.3"/>1.5.3</a></span><span class="sxs-lookup"><span data-stu-id="88923-186"><a name="1.5.3"/>1.5.3</a></span></span>
* <span data-ttu-id="88923-187">Corrige o problema [nº 81](https://github.com/Azure/azure-documentdb-node/issues/81) — trate corretamente os traços em IDs de mídia.</span><span class="sxs-lookup"><span data-stu-id="88923-187">Fixes issue [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - Properly handle dashes in media ids.</span></span>

### <span data-ttu-id="88923-188"><a name="1.5.2"/>1.5.2</a></span><span class="sxs-lookup"><span data-stu-id="88923-188"><a name="1.5.2"/>1.5.2</a></span></span>
* <span data-ttu-id="88923-189">Corrige o problema [nº 95](https://github.com/Azure/azure-documentdb-node/issues/95) — aviso de perda do ouvinte EventEmitter.</span><span class="sxs-lookup"><span data-stu-id="88923-189">Fixes issue [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter listener leak warning.</span></span>

### <span data-ttu-id="88923-190"><a name="1.5.1"/>1.5.1</a></span><span class="sxs-lookup"><span data-stu-id="88923-190"><a name="1.5.1"/>1.5.1</a></span></span>
* <span data-ttu-id="88923-191">Corrige o problema [nº 92](https://github.com/Azure/azure-documentdb-node/issues/90) — renomeie a pasta Hash para hash nos sistemas que diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="88923-191">Fixes issue [#92](https://github.com/Azure/azure-documentdb-node/issues/90) - rename folder Hash to hash for case-sensitive systems.</span></span>

### <span data-ttu-id="88923-192"><a name="1.5.0"/>1.5.0</a></span><span class="sxs-lookup"><span data-stu-id="88923-192"><a name="1.5.0"/>1.5.0</a></span></span>
* <span data-ttu-id="88923-193">Implemente o suporte a fragmentação ao adicionar os resolvedores de partição de hash e de intervalo.</span><span class="sxs-lookup"><span data-stu-id="88923-193">Implement sharding support by adding hash & range partition resolvers.</span></span>

### <span data-ttu-id="88923-194"><a name="1.4.0"/>1.4.0</a></span><span class="sxs-lookup"><span data-stu-id="88923-194"><a name="1.4.0"/>1.4.0</a></span></span>
* <span data-ttu-id="88923-195">Implementar o Upsert.</span><span class="sxs-lookup"><span data-stu-id="88923-195">Implement Upsert.</span></span> <span data-ttu-id="88923-196">Novos métodos upsertXXX em documentClient.</span><span class="sxs-lookup"><span data-stu-id="88923-196">New upsertXXX methods on documentClient.</span></span>

### <span data-ttu-id="88923-197"><a name="1.3.0"/>1.3.0</a></span><span class="sxs-lookup"><span data-stu-id="88923-197"><a name="1.3.0"/>1.3.0</a></span></span>
* <span data-ttu-id="88923-198">Ignorado para alinhar os números de versão com outros SDKs.</span><span class="sxs-lookup"><span data-stu-id="88923-198">Skipped to bring version numbers in alignment with other SDKs.</span></span>

### <span data-ttu-id="88923-199"><a name="1.2.2"/>1.2.2</a></span><span class="sxs-lookup"><span data-stu-id="88923-199"><a name="1.2.2"/>1.2.2</a></span></span>
* <span data-ttu-id="88923-200">Slipt Q promete wrapper para o novo repositório.</span><span class="sxs-lookup"><span data-stu-id="88923-200">Split Q promises wrapper to new repository.</span></span>
* <span data-ttu-id="88923-201">Atualização para o arquivo de pacote do registro npm.</span><span class="sxs-lookup"><span data-stu-id="88923-201">Update to package file for npm registry.</span></span>

### <span data-ttu-id="88923-202"><a name="1.2.1"/>1.2.1</a></span><span class="sxs-lookup"><span data-stu-id="88923-202"><a name="1.2.1"/>1.2.1</a></span></span>
* <span data-ttu-id="88923-203">Implementa o roteamento com base em ID.</span><span class="sxs-lookup"><span data-stu-id="88923-203">Implements ID Based Routing.</span></span>
* <span data-ttu-id="88923-204">Corrige o problema [nº 49](https://github.com/Azure/azure-documentdb-node/issues/49) - a propriedade atual está em conflito com o método atual().</span><span class="sxs-lookup"><span data-stu-id="88923-204">Fixes Issue [#49](https://github.com/Azure/azure-documentdb-node/issues/49) - current property conflicts with method current().</span></span>

### <span data-ttu-id="88923-205"><a name="1.2.0"/>1.2.0</a></span><span class="sxs-lookup"><span data-stu-id="88923-205"><a name="1.2.0"/>1.2.0</a></span></span>
* <span data-ttu-id="88923-206">Suporte adicionado para índice geoespaciais.</span><span class="sxs-lookup"><span data-stu-id="88923-206">Added support for GeoSpatial index.</span></span>
* <span data-ttu-id="88923-207">Valida a propriedade de ID de todos os recursos.</span><span class="sxs-lookup"><span data-stu-id="88923-207">Validates id property for all resources.</span></span> <span data-ttu-id="88923-208">As IDs de recursos não podem conter caracteres ?, /, #, &#47;&#47; ou terminar com um espaço.</span><span class="sxs-lookup"><span data-stu-id="88923-208">Ids for resources cannot contain ?, /, #, &#47;&#47;, characters or end with a space.</span></span>
* <span data-ttu-id="88923-209">Adiciona o novo cabeçalho "andamento de transformação do índice" ao ResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="88923-209">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <span data-ttu-id="88923-210"><a name="1.1.0"/>1.1.0</a></span><span class="sxs-lookup"><span data-stu-id="88923-210"><a name="1.1.0"/>1.1.0</a></span></span>
* <span data-ttu-id="88923-211">Implementa a política de indexação V2.</span><span class="sxs-lookup"><span data-stu-id="88923-211">Implements V2 indexing policy.</span></span>

### <span data-ttu-id="88923-212"><a name="1.0.3"/>1.0.3</a></span><span class="sxs-lookup"><span data-stu-id="88923-212"><a name="1.0.3"/>1.0.3</a></span></span>
* <span data-ttu-id="88923-213">Problema [nº 40](https://github.com/Azure/azure-documentdb-node/issues/40) - Configurações eslint e grunt implementadas no núcleo e SDK de promessa.</span><span class="sxs-lookup"><span data-stu-id="88923-213">Issue [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - Implemented eslint and grunt configurations in the core and promise SDK.</span></span>

### <span data-ttu-id="88923-214"><a name="1.0.2"/>1.0.2</a></span><span class="sxs-lookup"><span data-stu-id="88923-214"><a name="1.0.2"/>1.0.2</a></span></span>
* <span data-ttu-id="88923-215">Problema [nº 45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promessa de wrapper não inclui o cabeçalho com erro.</span><span class="sxs-lookup"><span data-stu-id="88923-215">Issue [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promises wrapper does not include header with error.</span></span>

### <span data-ttu-id="88923-216"><a name="1.0.1"/>1.0.1</a></span><span class="sxs-lookup"><span data-stu-id="88923-216"><a name="1.0.1"/>1.0.1</a></span></span>
* <span data-ttu-id="88923-217">Habilidade implementada de consultar conflitos por meio da adição de readConflicts, readConflictAsync e queryConflicts.</span><span class="sxs-lookup"><span data-stu-id="88923-217">Implemented ability to query for conflicts by adding readConflicts, readConflictAsync, and queryConflicts.</span></span>
* <span data-ttu-id="88923-218">Documentação da API atualizada.</span><span class="sxs-lookup"><span data-stu-id="88923-218">Updated API documentation.</span></span>
* <span data-ttu-id="88923-219">Problema [nº 41](https://github.com/Azure/azure-documentdb-node/issues/41) - Erro client.createDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="88923-219">Issue [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync error.</span></span>

### <span data-ttu-id="88923-220"><a name="1.0.0"/>1.0.0</a></span><span class="sxs-lookup"><span data-stu-id="88923-220"><a name="1.0.0"/>1.0.0</a></span></span>
* <span data-ttu-id="88923-221">SDK DO GA.</span><span class="sxs-lookup"><span data-stu-id="88923-221">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="88923-222">Datas de lançamento e desativação</span><span class="sxs-lookup"><span data-stu-id="88923-222">Release & Retirement Dates</span></span>
<span data-ttu-id="88923-223">A Microsoft notifica pelo menos **12 meses** antes de desativar um SDK, a fim de realizar uma transição tranquila para uma versão mais recente/com suporte.</span><span class="sxs-lookup"><span data-stu-id="88923-223">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="88923-224">Os novos recursos, funcionalidades e otimizações são adicionados apenas ao SDK atual. Portanto, é recomendável atualizar sempre que possível para a versão do SDK mais recente.</span><span class="sxs-lookup"><span data-stu-id="88923-224">New features and functionality and optimizations are only added to the current SDK, as such it is  recommended that you always upgrade to the latest SDK version as early as possible.</span></span>

<span data-ttu-id="88923-225">Qualquer solicitação feita ao Cosmos DB com o uso de um SDK desativado é rejeitada pelo serviço.</span><span class="sxs-lookup"><span data-stu-id="88923-225">Any request to Cosmos DB using a retired SDK is be rejected by the service.</span></span>

<br/>

| <span data-ttu-id="88923-226">Versão</span><span class="sxs-lookup"><span data-stu-id="88923-226">Version</span></span> | <span data-ttu-id="88923-227">Data do lançamento</span><span class="sxs-lookup"><span data-stu-id="88923-227">Release Date</span></span> | <span data-ttu-id="88923-228">Data de desativação</span><span class="sxs-lookup"><span data-stu-id="88923-228">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="88923-229">1.12.2</span><span class="sxs-lookup"><span data-stu-id="88923-229">1.12.2</span></span>](#1.12.2) |<span data-ttu-id="88923-230">10 de agosto de 2017</span><span class="sxs-lookup"><span data-stu-id="88923-230">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="88923-231">1.12.1</span><span class="sxs-lookup"><span data-stu-id="88923-231">1.12.1</span></span>](#1.12.1) |<span data-ttu-id="88923-232">10 de agosto de 2017</span><span class="sxs-lookup"><span data-stu-id="88923-232">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="88923-233">1.12.0</span><span class="sxs-lookup"><span data-stu-id="88923-233">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="88923-234">10 de maio de 2017</span><span class="sxs-lookup"><span data-stu-id="88923-234">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="88923-235">1.11.0</span><span class="sxs-lookup"><span data-stu-id="88923-235">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="88923-236">16 de março de 2017</span><span class="sxs-lookup"><span data-stu-id="88923-236">March 16, 2017</span></span> |--- |
| [<span data-ttu-id="88923-237">1.10.2</span><span class="sxs-lookup"><span data-stu-id="88923-237">1.10.2</span></span>](#1.10.2) |<span data-ttu-id="88923-238">27 de janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="88923-238">January 27, 2017</span></span> |--- |
| [<span data-ttu-id="88923-239">1.10.1</span><span class="sxs-lookup"><span data-stu-id="88923-239">1.10.1</span></span>](#1.10.1) |<span data-ttu-id="88923-240">22 de dezembro de 2016</span><span class="sxs-lookup"><span data-stu-id="88923-240">December 22, 2016</span></span> |--- |
| [<span data-ttu-id="88923-241">1.10.0</span><span class="sxs-lookup"><span data-stu-id="88923-241">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="88923-242">3 de outubro de 2016</span><span class="sxs-lookup"><span data-stu-id="88923-242">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="88923-243">1.9.0</span><span class="sxs-lookup"><span data-stu-id="88923-243">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="88923-244">07 de julho de 2016</span><span class="sxs-lookup"><span data-stu-id="88923-244">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="88923-245">1.8.0</span><span class="sxs-lookup"><span data-stu-id="88923-245">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="88923-246">14 de junho de 2016</span><span class="sxs-lookup"><span data-stu-id="88923-246">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="88923-247">1.7.0</span><span class="sxs-lookup"><span data-stu-id="88923-247">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="88923-248">26 de abril de 2016</span><span class="sxs-lookup"><span data-stu-id="88923-248">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="88923-249">1.6.0</span><span class="sxs-lookup"><span data-stu-id="88923-249">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="88923-250">29 de março de 2016</span><span class="sxs-lookup"><span data-stu-id="88923-250">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="88923-251">1.5.6</span><span class="sxs-lookup"><span data-stu-id="88923-251">1.5.6</span></span>](#1.5.6) |<span data-ttu-id="88923-252">08 de março de 2016</span><span class="sxs-lookup"><span data-stu-id="88923-252">March 08, 2016</span></span> |--- |
| [<span data-ttu-id="88923-253">1.5.5</span><span class="sxs-lookup"><span data-stu-id="88923-253">1.5.5</span></span>](#1.5.5) |<span data-ttu-id="88923-254">02 de fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="88923-254">February 02, 2016</span></span> |--- |
| [<span data-ttu-id="88923-255">1.5.4</span><span class="sxs-lookup"><span data-stu-id="88923-255">1.5.4</span></span>](#1.5.4) |<span data-ttu-id="88923-256">1 de fevereiro de 2016</span><span class="sxs-lookup"><span data-stu-id="88923-256">February 01, 2016</span></span> |--- |
| [<span data-ttu-id="88923-257">1.5.2</span><span class="sxs-lookup"><span data-stu-id="88923-257">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="88923-258">26 de janeiro de 2016</span><span class="sxs-lookup"><span data-stu-id="88923-258">January 26, 2016</span></span> |--- |
| [<span data-ttu-id="88923-259">1.5.2</span><span class="sxs-lookup"><span data-stu-id="88923-259">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="88923-260">22 de janeiro de 2016</span><span class="sxs-lookup"><span data-stu-id="88923-260">January 22, 2016</span></span> |--- |
| [<span data-ttu-id="88923-261">1.5.1</span><span class="sxs-lookup"><span data-stu-id="88923-261">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="88923-262">4 de janeiro de 2016</span><span class="sxs-lookup"><span data-stu-id="88923-262">January 4, 2016</span></span> |--- |
| [<span data-ttu-id="88923-263">1.5.0</span><span class="sxs-lookup"><span data-stu-id="88923-263">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="88923-264">31 de dezembro de 2015</span><span class="sxs-lookup"><span data-stu-id="88923-264">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="88923-265">1.4.0</span><span class="sxs-lookup"><span data-stu-id="88923-265">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="88923-266">06 de outubro de 2015</span><span class="sxs-lookup"><span data-stu-id="88923-266">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="88923-267">1.3.0</span><span class="sxs-lookup"><span data-stu-id="88923-267">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="88923-268">06 de outubro de 2015</span><span class="sxs-lookup"><span data-stu-id="88923-268">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="88923-269">1.2.2</span><span class="sxs-lookup"><span data-stu-id="88923-269">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="88923-270">10 de setembro de 2015</span><span class="sxs-lookup"><span data-stu-id="88923-270">September 10, 2015</span></span> |--- |
| [<span data-ttu-id="88923-271">1.2.1</span><span class="sxs-lookup"><span data-stu-id="88923-271">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="88923-272">15 de agosto de 2015</span><span class="sxs-lookup"><span data-stu-id="88923-272">August 15, 2015</span></span> |--- |
| [<span data-ttu-id="88923-273">1.2.0</span><span class="sxs-lookup"><span data-stu-id="88923-273">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="88923-274">5 de agosto de 2015</span><span class="sxs-lookup"><span data-stu-id="88923-274">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="88923-275">1.1.0</span><span class="sxs-lookup"><span data-stu-id="88923-275">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="88923-276">9 de julho de 2015</span><span class="sxs-lookup"><span data-stu-id="88923-276">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="88923-277">1.0.3</span><span class="sxs-lookup"><span data-stu-id="88923-277">1.0.3</span></span>](#1.0.3) |<span data-ttu-id="88923-278">04 de junho de 2015</span><span class="sxs-lookup"><span data-stu-id="88923-278">June 04, 2015</span></span> |--- |
| [<span data-ttu-id="88923-279">1.0.2</span><span class="sxs-lookup"><span data-stu-id="88923-279">1.0.2</span></span>](#1.0.2) |<span data-ttu-id="88923-280">23 de maio de 2015</span><span class="sxs-lookup"><span data-stu-id="88923-280">May 23, 2015</span></span> |--- |
| [<span data-ttu-id="88923-281">1.0.1</span><span class="sxs-lookup"><span data-stu-id="88923-281">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="88923-282">15 de maio de 2015</span><span class="sxs-lookup"><span data-stu-id="88923-282">May 15, 2015</span></span> |--- |
| [<span data-ttu-id="88923-283">1.0.0</span><span class="sxs-lookup"><span data-stu-id="88923-283">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="88923-284">8 de abril de 2015</span><span class="sxs-lookup"><span data-stu-id="88923-284">April 08, 2015</span></span> |--- |

## <a name="faq"></a><span data-ttu-id="88923-285">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="88923-285">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="88923-286">Consulte também</span><span class="sxs-lookup"><span data-stu-id="88923-286">See also</span></span>
<span data-ttu-id="88923-287">Para saber mais sobre o Cosmos DB, consulte a página de serviço do [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="88923-287">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

