---
title: aaaAzure Cosmos DB .NET Core API, SDK e recursos | Microsoft Docs
description: "Saiba tudo sobre Olá .NET Core API e do SDK, incluindo datas de lançamento, datas de desativação e as alterações feitas entre cada versão do hello Azure Cosmos DB .NET Core SDK."
services: cosmos-db
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: f899b314-26ac-4ddb-86b2-bfdf05c2abf2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/11/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1269cafe0ea1caaa871404d507b12632dbb3ed82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-net-core-sdk-release-notes-and-resources"></a><span data-ttu-id="8513c-103">SDK do .NET Core do Azure Cosmos DB: notas de versão e recursos</span><span class="sxs-lookup"><span data-stu-id="8513c-103">Azure Cosmos DB .NET Core SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8513c-104">.NET</span><span class="sxs-lookup"><span data-stu-id="8513c-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="8513c-105">Feed de alterações do .NET</span><span class="sxs-lookup"><span data-stu-id="8513c-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="8513c-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="8513c-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="8513c-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="8513c-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="8513c-108">Java</span><span class="sxs-lookup"><span data-stu-id="8513c-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="8513c-109">Python</span><span class="sxs-lookup"><span data-stu-id="8513c-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="8513c-110">REST</span><span class="sxs-lookup"><span data-stu-id="8513c-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="8513c-111">Provedor de recursos REST</span><span class="sxs-lookup"><span data-stu-id="8513c-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="8513c-112">SQL</span><span class="sxs-lookup"><span data-stu-id="8513c-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="8513c-113">**Baixe o SDK**</span><span class="sxs-lookup"><span data-stu-id="8513c-113">**SDK download**</span></span></td><td>[<span data-ttu-id="8513c-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="8513c-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/)</td></tr>

<tr><td><span data-ttu-id="8513c-115">**Documentação da API**</span><span class="sxs-lookup"><span data-stu-id="8513c-115">**API documentation**</span></span></td><td>[<span data-ttu-id="8513c-116">Documentação de referência de API .NET</span><span class="sxs-lookup"><span data-stu-id="8513c-116">.NET API reference documentation</span></span>](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="8513c-117">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="8513c-117">**Samples**</span></span></td><td>[<span data-ttu-id="8513c-118">Exemplos de código .NET</span><span class="sxs-lookup"><span data-stu-id="8513c-118">.NET code samples</span></span>](documentdb-dotnet-samples.md)</td></tr>

<tr><td><span data-ttu-id="8513c-119">**Introdução**</span><span class="sxs-lookup"><span data-stu-id="8513c-119">**Get started**</span></span></td><td>[<span data-ttu-id="8513c-120">Introdução ao hello Azure Cosmos DB .NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="8513c-120">Get started with hello Azure Cosmos DB .NET Core SDK</span></span>](documentdb-dotnetcore-get-started.md)</td></tr>

<tr><td><span data-ttu-id="8513c-121">**Tutorial do aplicativo Web**</span><span class="sxs-lookup"><span data-stu-id="8513c-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="8513c-122">Desenvolvimento de aplicativos Web com o Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8513c-122">Web application development with Azure Cosmos DB</span></span>](documentdb-dotnet-application.md)</td></tr>

<tr><td><span data-ttu-id="8513c-123">**Framework atualmente com suporte**</span><span class="sxs-lookup"><span data-stu-id="8513c-123">**Current supported framework**</span></span></td><td>[<span data-ttu-id="8513c-124">.NET Standard 1.6 e .NET Standard 1.5</span><span class="sxs-lookup"><span data-stu-id="8513c-124">.NET Standard 1.6 and .NET Standard 1.5</span></span>](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="8513c-125">Notas de versão</span><span class="sxs-lookup"><span data-stu-id="8513c-125">Release Notes</span></span>

<span data-ttu-id="8513c-126">Hello Azure Cosmos DB .NET Core SDK tem paridade de recursos com versão mais recente de saudação do hello [SDK .NET do Azure Cosmos DB](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="8513c-126">hello Azure Cosmos DB .NET Core SDK has feature parity with hello latest version of hello [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="8513c-127">Hello Azure Cosmos DB .NET Core SDK ainda não é compatível com aplicativos do Windows UWP (plataforma Universal).</span><span class="sxs-lookup"><span data-stu-id="8513c-127">hello Azure Cosmos DB .NET Core SDK is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="8513c-128">Se você estiver interessado em Olá .NET Core SDK que dá suporte a aplicativos UWP, envie um email muito[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="8513c-128">If you are interested in hello .NET Core SDK that does support UWP apps, send email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

### <a name="a-name150150"></a><span data-ttu-id="8513c-129"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="8513c-129"><a name="1.5.0"/>1.5.0</span></span> 

* <span data-ttu-id="8513c-130">Adicionado suporte para PartitionKeyRangeId como um FeedOption para definir o valor de intervalo de chave consulta resultados tooa partição específica.</span><span class="sxs-lookup"><span data-stu-id="8513c-130">Added support for PartitionKeyRangeId as a FeedOption for scoping query results tooa specific partition key range value.</span></span> 
* <span data-ttu-id="8513c-131">Adicionado suporte para StartTime como um toostart ChangeFeedOption em busca de alterações de saudação depois desse tempo.</span><span class="sxs-lookup"><span data-stu-id="8513c-131">Added support for StartTime as a ChangeFeedOption toostart looking for hello changes after that time.</span></span> 

### <a name="a-name141141"></a><span data-ttu-id="8513c-132"><a name="1.4.1"/>1.4.1</span><span class="sxs-lookup"><span data-stu-id="8513c-132"><a name="1.4.1"/>1.4.1</span></span>

*   <span data-ttu-id="8513c-133">Corrigido um problema no hello JsonSerializable classe que pode gerar uma exceção de estouro de pilha.</span><span class="sxs-lookup"><span data-stu-id="8513c-133">Fixed an issue in hello JsonSerializable class that may cause a stack overflow exception.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="8513c-134"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="8513c-134"><a name="1.4.0"/>1.4.0</span></span>

*   <span data-ttu-id="8513c-135">Adicionado suporte para a especificação de JsonSerializerSettings personalizadas ao instanciar uma instância [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="8513c-135">Added support for specifying custom JsonSerializerSettings while instantiating a [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) instance.</span></span>

### <a name="a-name132132"></a><span data-ttu-id="8513c-136"><a name="1.3.2"/>1.3.2</span><span class="sxs-lookup"><span data-stu-id="8513c-136"><a name="1.3.2"/>1.3.2</span></span>

*   <span data-ttu-id="8513c-137">Suporte 1.5 padrão do .NET como uma saudação estruturas de destino.</span><span class="sxs-lookup"><span data-stu-id="8513c-137">Supporting .NET Standard 1.5 as one of hello target frameworks.</span></span>

### <a name="a-name131131"></a><span data-ttu-id="8513c-138"><a name="1.3.1"/>1.3.1</span><span class="sxs-lookup"><span data-stu-id="8513c-138"><a name="1.3.1"/>1.3.1</span></span>

*   <span data-ttu-id="8513c-139">Corrigido um problema que afetava computadores x64 que não davam suporte à instrução SSE4 e que geravam SEHException ao executarem consultas do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8513c-139">Fixed an issue that affected x64 machines that don’t support SSE4 instruction and throw SEHException when running Azure Cosmos DB queries.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="8513c-140"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="8513c-140"><a name="1.3.0"/>1.3.0</span></span>

*   <span data-ttu-id="8513c-141">Adição de suporte a um novo nível de consistência chamado ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="8513c-141">Added support for a new consistency level called ConsistentPrefix.</span></span>
*   <span data-ttu-id="8513c-142">Adição de suporte a métricas de consulta em partições individuais.</span><span class="sxs-lookup"><span data-stu-id="8513c-142">Added support for query metrics for individual partitions.</span></span>
*   <span data-ttu-id="8513c-143">Adicionado suporte para limitar o tamanho de saudação do token de continuação Olá para consultas.</span><span class="sxs-lookup"><span data-stu-id="8513c-143">Added support for limiting hello size of hello continuation token for queries.</span></span>
*   <span data-ttu-id="8513c-144">Adição de suporte para um rastreamento mais detalhado das solicitações com falha.</span><span class="sxs-lookup"><span data-stu-id="8513c-144">Added support for more detailed tracing for failed requests.</span></span>
*   <span data-ttu-id="8513c-145">Feitas algumas melhorias de desempenho no hello SDK.</span><span class="sxs-lookup"><span data-stu-id="8513c-145">Made some performance improvements in hello SDK.</span></span>

### <a name="a-name122122"></a><span data-ttu-id="8513c-146"><a name="1.2.2"/>1.2.2</span><span class="sxs-lookup"><span data-stu-id="8513c-146"><a name="1.2.2"/>1.2.2</span></span>

* <span data-ttu-id="8513c-147">Corrigido um problema que ignorou o valor de PartitionKey Olá fornecido no FeedOptions para consultas de agregação.</span><span class="sxs-lookup"><span data-stu-id="8513c-147">Fixed an issue that ignored hello PartitionKey value provided in FeedOptions for aggregate queries.</span></span>
* <span data-ttu-id="8513c-148">Correção de um problema na manipulação transparente do gerenciamento de partição durante a metade da execução da consulta Order By entre partições.</span><span class="sxs-lookup"><span data-stu-id="8513c-148">Fixed an issue in transparent handling of partition management during mid-flight cross-partition Order By query execution.</span></span>

### <a name="a-name121121"></a><span data-ttu-id="8513c-149"><a name="1.2.1"/>1.2.1</span><span class="sxs-lookup"><span data-stu-id="8513c-149"><a name="1.2.1"/>1.2.1</span></span>

* <span data-ttu-id="8513c-150">Corrigido um problema que causou deadlocks em alguns Olá async APIs quando usada dentro do contexto do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="8513c-150">Fixed an issue which caused deadlocks in some of hello async APIs when used inside ASP.NET context.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="8513c-151"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="8513c-151"><a name="1.2.0"/>1.2.0</span></span>

* <span data-ttu-id="8513c-152">Correções toomake SDK mais resiliente tooautomatic failover sob determinadas condições.</span><span class="sxs-lookup"><span data-stu-id="8513c-152">Fixes toomake SDK more resilient tooautomatic failover under certain conditions.</span></span>

### <a name="a-name112112"></a><span data-ttu-id="8513c-153"><a name="1.1.2"/>1.1.2</span><span class="sxs-lookup"><span data-stu-id="8513c-153"><a name="1.1.2"/>1.1.2</span></span>

* <span data-ttu-id="8513c-154">Correção para um problema que causa ocasionalmente um WebException: nome remoto Olá não pôde ser resolvido.</span><span class="sxs-lookup"><span data-stu-id="8513c-154">Fix for an issue that occasionally causes a WebException: hello remote name could not be resolved.</span></span>
* <span data-ttu-id="8513c-155">Olá adicionado suporte para ler um documento digitado diretamente, adicionando nova API de tooReadDocumentAsync sobrecargas.</span><span class="sxs-lookup"><span data-stu-id="8513c-155">Added hello support for directly reading a typed document by adding new overloads tooReadDocumentAsync API.</span></span>

### <a name="a-name111111"></a><span data-ttu-id="8513c-156"><a name="1.1.1"/>1.1.1</span><span class="sxs-lookup"><span data-stu-id="8513c-156"><a name="1.1.1"/>1.1.1</span></span>

* <span data-ttu-id="8513c-157">Adicionado suporte ao LINQ para consultas de agregação (CONT.NÚM, MÍNIMO, MÁXIMO, SOMA e MÉDIA).</span><span class="sxs-lookup"><span data-stu-id="8513c-157">Added LINQ support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="8513c-158">Correção para um problema de vazamento de memória para o objeto de ConnectionPolicy Olá causado pelo uso de saudação do manipulador de eventos.</span><span class="sxs-lookup"><span data-stu-id="8513c-158">Fix for a memory leak issue for hello ConnectionPolicy object caused by hello use of event handler.</span></span>
* <span data-ttu-id="8513c-159">Correção de um problema no qual UpsertAttachmentAsync não estava funcionando quando ETag era usada.</span><span class="sxs-lookup"><span data-stu-id="8513c-159">Fix for an issue wherein UpsertAttachmentAsync was not working when ETag was used.</span></span>
* <span data-ttu-id="8513c-160">Correção de um problema no qual a continuação da consulta order-by entre partições não estava funcionando ao classificar no campo de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="8513c-160">Fix for an issue wherein cross partition order-by query continuation was not working when sorting on string field.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="8513c-161"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="8513c-161"><a name="1.1.0"/>1.1.0</span></span>

* <span data-ttu-id="8513c-162">Suporte adicionado para consultas de agregação (COUNT, MIN, MAX, SUM e AVG).</span><span class="sxs-lookup"><span data-stu-id="8513c-162">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="8513c-163">Veja [Suporte de agregação](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="8513c-163">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="8513c-164">Reduzida a taxa de transferência mínima em coleções particionadas de 10,100 RU/s too2500 RU/s.</span><span class="sxs-lookup"><span data-stu-id="8513c-164">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="8513c-165"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="8513c-165"><a name="1.0.0"/>1.0.0</span></span>

<span data-ttu-id="8513c-166">Hello Azure Cosmos DB .NET Core SDK permite que você toobuild rápidos entre plataformas [ASP.NET Core](https://www.asp.net/core) e [.NET Core](https://www.microsoft.com/net/core#windows) toorun de aplicativos no Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="8513c-166">hello Azure Cosmos DB .NET Core SDK enables you toobuild fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps toorun on Windows, Mac, and Linux.</span></span> <span data-ttu-id="8513c-167">Olá versão mais recente do hello Azure Cosmos DB .NET Core SDK é totalmente [Xamarin](https://www.xamarin.com) compatível e ser usado toobuild aplicativos voltados para iOS, Android e Mono (Linux).</span><span class="sxs-lookup"><span data-stu-id="8513c-167">hello latest release of hello Azure Cosmos DB .NET Core SDK is fully [Xamarin](https://www.xamarin.com) compatible and be used toobuild applications that target iOS, Android, and Mono (Linux).</span></span>  

### <a name="a-name010-preview010-preview"></a><span data-ttu-id="8513c-168"><a name="0.1.0-preview"/>0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="8513c-168"><a name="0.1.0-preview"/>0.1.0-preview</span></span>

<span data-ttu-id="8513c-169">Hello Azure Cosmos DB .NET Core Preview SDK permite que você toobuild rápidos entre plataformas [ASP.NET Core](https://www.asp.net/core) e [.NET Core](https://www.microsoft.com/net/core#windows) toorun de aplicativos no Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="8513c-169">hello Azure Cosmos DB .NET Core Preview SDK enables you toobuild fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps toorun on Windows, Mac, and Linux.</span></span>

<span data-ttu-id="8513c-170">Hello Azure Cosmos DB .NET Core Preview SDK tem paridade de recursos com versão mais recente de saudação do hello [SDK .NET do Azure Cosmos DB](documentdb-sdk-dotnet.md) e suporta Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="8513c-170">hello Azure Cosmos DB .NET Core Preview SDK has feature parity with hello latest version of hello [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md) and supports hello following:</span></span>
* <span data-ttu-id="8513c-171">Todos os [modos de conexão](performance-tips.md#networking): Modo de gateway, TCP Direto e HTTPs Direto.</span><span class="sxs-lookup"><span data-stu-id="8513c-171">All [connection modes](performance-tips.md#networking): Gateway mode, Direct TCP, and Direct HTTPs.</span></span> 
* <span data-ttu-id="8513c-172">Todos os [níveis de consistência](consistency-levels.md): Forte, Sessão, Desatualização Limitada e Eventual.</span><span class="sxs-lookup"><span data-stu-id="8513c-172">All [consistency levels](consistency-levels.md): Strong, Session, Bounded Staleness, and Eventual.</span></span>
* <span data-ttu-id="8513c-173">[Coleções particionadas](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="8513c-173">[Partitioned collections](partition-data.md).</span></span> 
* <span data-ttu-id="8513c-174">[Contas e replicação geográfica de banco de dados de várias regiões](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="8513c-174">[Multi-region database accounts and geo-replication](distribute-data-globally.md).</span></span>

<span data-ttu-id="8513c-175">Se você tiver dúvidas relacionadas toothis SDK, postar muito[StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), ou um problema de arquivo hello [repositório github](https://github.com/Azure/azure-documentdb-dotnet/issues).</span><span class="sxs-lookup"><span data-stu-id="8513c-175">If you have questions related toothis SDK, post too[StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), or file an issue in hello [github repository](https://github.com/Azure/azure-documentdb-dotnet/issues).</span></span> 

## <a name="release--retirement-dates"></a><span data-ttu-id="8513c-176">Datas de lançamento e desativação</span><span class="sxs-lookup"><span data-stu-id="8513c-176">Release & Retirement Dates</span></span>

| <span data-ttu-id="8513c-177">Versão</span><span class="sxs-lookup"><span data-stu-id="8513c-177">Version</span></span> | <span data-ttu-id="8513c-178">Data do lançamento</span><span class="sxs-lookup"><span data-stu-id="8513c-178">Release Date</span></span> | <span data-ttu-id="8513c-179">Data de desativação</span><span class="sxs-lookup"><span data-stu-id="8513c-179">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="8513c-180">1.5.0</span><span class="sxs-lookup"><span data-stu-id="8513c-180">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="8513c-181">10 de agosto de 2017</span><span class="sxs-lookup"><span data-stu-id="8513c-181">August 10, 2017</span></span> |--- | 
| [<span data-ttu-id="8513c-182">1.4.1</span><span class="sxs-lookup"><span data-stu-id="8513c-182">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="8513c-183">7 de agosto de 2017</span><span class="sxs-lookup"><span data-stu-id="8513c-183">August 07, 2017</span></span> |--- |
| [<span data-ttu-id="8513c-184">1.4.0</span><span class="sxs-lookup"><span data-stu-id="8513c-184">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="8513c-185">2 de agosto de 2017</span><span class="sxs-lookup"><span data-stu-id="8513c-185">August 02, 2017</span></span> |--- |
| [<span data-ttu-id="8513c-186">1.3.2</span><span class="sxs-lookup"><span data-stu-id="8513c-186">1.3.2</span></span>](#1.3.2) |<span data-ttu-id="8513c-187">12 de junho de 2017</span><span class="sxs-lookup"><span data-stu-id="8513c-187">June 12, 2017</span></span> |--- |
| [<span data-ttu-id="8513c-188">1.3.1</span><span class="sxs-lookup"><span data-stu-id="8513c-188">1.3.1</span></span>](#1.3.1) |<span data-ttu-id="8513c-189">23 de maio de 2017</span><span class="sxs-lookup"><span data-stu-id="8513c-189">May 23, 2017</span></span> |--- |
| [<span data-ttu-id="8513c-190">1.3.0</span><span class="sxs-lookup"><span data-stu-id="8513c-190">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="8513c-191">10 de maio de 2017</span><span class="sxs-lookup"><span data-stu-id="8513c-191">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="8513c-192">1.2.2</span><span class="sxs-lookup"><span data-stu-id="8513c-192">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="8513c-193">19 de abril de 2017</span><span class="sxs-lookup"><span data-stu-id="8513c-193">April 19, 2017</span></span> |--- |
| [<span data-ttu-id="8513c-194">1.2.1</span><span class="sxs-lookup"><span data-stu-id="8513c-194">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="8513c-195">29 de março de 2017</span><span class="sxs-lookup"><span data-stu-id="8513c-195">March 29, 2017</span></span> |--- |
| [<span data-ttu-id="8513c-196">1.2.0</span><span class="sxs-lookup"><span data-stu-id="8513c-196">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="8513c-197">25 de março de 2017</span><span class="sxs-lookup"><span data-stu-id="8513c-197">March 25, 2017</span></span> |--- |
| [<span data-ttu-id="8513c-198">1.1.2</span><span class="sxs-lookup"><span data-stu-id="8513c-198">1.1.2</span></span>](#1.1.2) |<span data-ttu-id="8513c-199">20 de março de 2017</span><span class="sxs-lookup"><span data-stu-id="8513c-199">March 20, 2017</span></span> |--- |
| [<span data-ttu-id="8513c-200">1.1.1</span><span class="sxs-lookup"><span data-stu-id="8513c-200">1.1.1</span></span>](#1.1.1) |<span data-ttu-id="8513c-201">14 de março de 2017</span><span class="sxs-lookup"><span data-stu-id="8513c-201">March 14, 2017</span></span> |--- |
| [<span data-ttu-id="8513c-202">1.1.0</span><span class="sxs-lookup"><span data-stu-id="8513c-202">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="8513c-203">16 de fevereiro de 2017</span><span class="sxs-lookup"><span data-stu-id="8513c-203">February 16, 2017</span></span> |--- |
| [<span data-ttu-id="8513c-204">1.0.0</span><span class="sxs-lookup"><span data-stu-id="8513c-204">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="8513c-205">21 de dezembro de 2016</span><span class="sxs-lookup"><span data-stu-id="8513c-205">December 21, 2016</span></span> |--- |
| [<span data-ttu-id="8513c-206">0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="8513c-206">0.1.0-preview</span></span>](#0.1.0-preview) |<span data-ttu-id="8513c-207">15 de novembro de 2016</span><span class="sxs-lookup"><span data-stu-id="8513c-207">November 15, 2016</span></span> |<span data-ttu-id="8513c-208">31 de dezembro de 2016</span><span class="sxs-lookup"><span data-stu-id="8513c-208">December 31, 2016</span></span> |

## <a name="see-also"></a><span data-ttu-id="8513c-209">Consulte também</span><span class="sxs-lookup"><span data-stu-id="8513c-209">See Also</span></span>
<span data-ttu-id="8513c-210">toolearn mais sobre o banco de dados do Cosmos, consulte [banco de dados do Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) página de serviço.</span><span class="sxs-lookup"><span data-stu-id="8513c-210">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

