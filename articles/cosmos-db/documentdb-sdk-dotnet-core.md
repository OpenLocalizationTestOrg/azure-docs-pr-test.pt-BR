---
title: API do .NET Core, SDK e recursos do Azure Cosmos DB | Microsoft Docs
description: "Saiba tudo sobre o SDK e a API do .NET Core, incluindo as datas de lançamento, as datas de desativação e as alterações feitas entre cada versão do SDK do .NET Core para Azure Cosmos DB."
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
ms.openlocfilehash: a7ce4d771e9c655687f72f4b46c7405cf64aeb74
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-net-core-sdk-release-notes-and-resources"></a><span data-ttu-id="2e5aa-103">SDK do .NET Core do Azure Cosmos DB: notas de versão e recursos</span><span class="sxs-lookup"><span data-stu-id="2e5aa-103">Azure Cosmos DB .NET Core SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2e5aa-104">.NET</span><span class="sxs-lookup"><span data-stu-id="2e5aa-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="2e5aa-105">Feed de alterações do .NET</span><span class="sxs-lookup"><span data-stu-id="2e5aa-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="2e5aa-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="2e5aa-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="2e5aa-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="2e5aa-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="2e5aa-108">Java</span><span class="sxs-lookup"><span data-stu-id="2e5aa-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="2e5aa-109">Python</span><span class="sxs-lookup"><span data-stu-id="2e5aa-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="2e5aa-110">REST</span><span class="sxs-lookup"><span data-stu-id="2e5aa-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="2e5aa-111">Provedor de recursos REST</span><span class="sxs-lookup"><span data-stu-id="2e5aa-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="2e5aa-112">SQL</span><span class="sxs-lookup"><span data-stu-id="2e5aa-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="2e5aa-113">**Baixe o SDK**</span><span class="sxs-lookup"><span data-stu-id="2e5aa-113">**SDK download**</span></span></td><td>[<span data-ttu-id="2e5aa-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="2e5aa-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/)</td></tr>

<tr><td><span data-ttu-id="2e5aa-115">**Documentação da API**</span><span class="sxs-lookup"><span data-stu-id="2e5aa-115">**API documentation**</span></span></td><td>[<span data-ttu-id="2e5aa-116">Documentação de referência de API .NET</span><span class="sxs-lookup"><span data-stu-id="2e5aa-116">.NET API reference documentation</span></span>](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="2e5aa-117">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="2e5aa-117">**Samples**</span></span></td><td>[<span data-ttu-id="2e5aa-118">Exemplos de código .NET</span><span class="sxs-lookup"><span data-stu-id="2e5aa-118">.NET code samples</span></span>](documentdb-dotnet-samples.md)</td></tr>

<tr><td><span data-ttu-id="2e5aa-119">**Introdução**</span><span class="sxs-lookup"><span data-stu-id="2e5aa-119">**Get started**</span></span></td><td>[<span data-ttu-id="2e5aa-120">Introdução ao SDK do .NET Core do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2e5aa-120">Get started with the Azure Cosmos DB .NET Core SDK</span></span>](documentdb-dotnetcore-get-started.md)</td></tr>

<tr><td><span data-ttu-id="2e5aa-121">**Tutorial do aplicativo Web**</span><span class="sxs-lookup"><span data-stu-id="2e5aa-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="2e5aa-122">Desenvolvimento de aplicativos Web com o Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2e5aa-122">Web application development with Azure Cosmos DB</span></span>](documentdb-dotnet-application.md)</td></tr>

<tr><td><span data-ttu-id="2e5aa-123">**Framework atualmente com suporte**</span><span class="sxs-lookup"><span data-stu-id="2e5aa-123">**Current supported framework**</span></span></td><td>[<span data-ttu-id="2e5aa-124">.NET Standard 1.6 e .NET Standard 1.5</span><span class="sxs-lookup"><span data-stu-id="2e5aa-124">.NET Standard 1.6 and .NET Standard 1.5</span></span>](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="2e5aa-125">Notas de versão</span><span class="sxs-lookup"><span data-stu-id="2e5aa-125">Release Notes</span></span>

<span data-ttu-id="2e5aa-126">O SDK do .NET Core do Azure Cosmos DB tem paridade de recurso com a versão mais recente do [SDK do .NET do Azure Cosmos DB](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="2e5aa-126">The Azure Cosmos DB .NET Core SDK has feature parity with the latest version of the [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="2e5aa-127">O SDK do .NET Core do Azure Cosmos DB não é compatível com aplicativos UWP (Plataforma Universal do Windows).</span><span class="sxs-lookup"><span data-stu-id="2e5aa-127">The Azure Cosmos DB .NET Core SDK is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="2e5aa-128">Se você estiver interessado no SDK do .NET Core que dê suporte a aplicativos UWP, envie um email para [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="2e5aa-128">If you are interested in the .NET Core SDK that does support UWP apps, send email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

### <a name="a-name150150"></a><span data-ttu-id="2e5aa-129"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="2e5aa-129"><a name="1.5.0"/>1.5.0</span></span> 

* <span data-ttu-id="2e5aa-130">Adição de suporte a PartitionKeyRangeId como FeedOption de modo a definir o escopo dos resultados da consulta para um valor específico do intervalo de chaves de partição.</span><span class="sxs-lookup"><span data-stu-id="2e5aa-130">Added support for PartitionKeyRangeId as a FeedOption for scoping query results to a specific partition key range value.</span></span> 
* <span data-ttu-id="2e5aa-131">Adição de suporte a StartTime como ChangeFeedOption para começar a procurar as alterações após esse horário.</span><span class="sxs-lookup"><span data-stu-id="2e5aa-131">Added support for StartTime as a ChangeFeedOption to start looking for the changes after that time.</span></span> 

### <a name="a-name141141"></a><span data-ttu-id="2e5aa-132"><a name="1.4.1"/>1.4.1</span><span class="sxs-lookup"><span data-stu-id="2e5aa-132"><a name="1.4.1"/>1.4.1</span></span>

*   <span data-ttu-id="2e5aa-133">Foi corrigido um problema na classe JsonSerializable que podia gerar uma exceção de excedente de pilha.</span><span class="sxs-lookup"><span data-stu-id="2e5aa-133">Fixed an issue in the JsonSerializable class that may cause a stack overflow exception.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="2e5aa-134"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="2e5aa-134"><a name="1.4.0"/>1.4.0</span></span>

*   <span data-ttu-id="2e5aa-135">Adicionado suporte para a especificação de JsonSerializerSettings personalizadas ao instanciar uma instância [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="2e5aa-135">Added support for specifying custom JsonSerializerSettings while instantiating a [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) instance.</span></span>

### <a name="a-name132132"></a><span data-ttu-id="2e5aa-136"><a name="1.3.2"/>1.3.2</span><span class="sxs-lookup"><span data-stu-id="2e5aa-136"><a name="1.3.2"/>1.3.2</span></span>

*   <span data-ttu-id="2e5aa-137">Suporte ao .NET Standard 1.5 como uma das estruturas de destino.</span><span class="sxs-lookup"><span data-stu-id="2e5aa-137">Supporting .NET Standard 1.5 as one of the target frameworks.</span></span>

### <a name="a-name131131"></a><span data-ttu-id="2e5aa-138"><a name="1.3.1"/>1.3.1</span><span class="sxs-lookup"><span data-stu-id="2e5aa-138"><a name="1.3.1"/>1.3.1</span></span>

*   <span data-ttu-id="2e5aa-139">Corrigido um problema que afetava computadores x64 que não davam suporte à instrução SSE4 e que geravam SEHException ao executarem consultas do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2e5aa-139">Fixed an issue that affected x64 machines that don’t support SSE4 instruction and throw SEHException when running Azure Cosmos DB queries.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="2e5aa-140"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="2e5aa-140"><a name="1.3.0"/>1.3.0</span></span>

*   <span data-ttu-id="2e5aa-141">Adição de suporte a um novo nível de consistência chamado ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="2e5aa-141">Added support for a new consistency level called ConsistentPrefix.</span></span>
*   <span data-ttu-id="2e5aa-142">Adição de suporte a métricas de consulta em partições individuais.</span><span class="sxs-lookup"><span data-stu-id="2e5aa-142">Added support for query metrics for individual partitions.</span></span>
*   <span data-ttu-id="2e5aa-143">Adição de suporte para limitar o tamanho do token de continuação em consultas.</span><span class="sxs-lookup"><span data-stu-id="2e5aa-143">Added support for limiting the size of the continuation token for queries.</span></span>
*   <span data-ttu-id="2e5aa-144">Adição de suporte para um rastreamento mais detalhado das solicitações com falha.</span><span class="sxs-lookup"><span data-stu-id="2e5aa-144">Added support for more detailed tracing for failed requests.</span></span>
*   <span data-ttu-id="2e5aa-145">Melhorias de desempenho no SDK.</span><span class="sxs-lookup"><span data-stu-id="2e5aa-145">Made some performance improvements in the SDK.</span></span>

### <a name="a-name122122"></a><span data-ttu-id="2e5aa-146"><a name="1.2.2"/>1.2.2</span><span class="sxs-lookup"><span data-stu-id="2e5aa-146"><a name="1.2.2"/>1.2.2</span></span>

* <span data-ttu-id="2e5aa-147">Correção de um problema no qual o valor de PartitionKey fornecido em FeedOptions para consultas de agregação é ignorado.</span><span class="sxs-lookup"><span data-stu-id="2e5aa-147">Fixed an issue that ignored the PartitionKey value provided in FeedOptions for aggregate queries.</span></span>
* <span data-ttu-id="2e5aa-148">Correção de um problema na manipulação transparente do gerenciamento de partição durante a metade da execução da consulta Order By entre partições.</span><span class="sxs-lookup"><span data-stu-id="2e5aa-148">Fixed an issue in transparent handling of partition management during mid-flight cross-partition Order By query execution.</span></span>

### <a name="a-name121121"></a><span data-ttu-id="2e5aa-149"><a name="1.2.1"/>1.2.1</span><span class="sxs-lookup"><span data-stu-id="2e5aa-149"><a name="1.2.1"/>1.2.1</span></span>

* <span data-ttu-id="2e5aa-150">Correção de um problema que causou deadlocks em algumas APIs assíncronas quando usado dentro do contexto do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2e5aa-150">Fixed an issue which caused deadlocks in some of the async APIs when used inside ASP.NET context.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="2e5aa-151"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="2e5aa-151"><a name="1.2.0"/>1.2.0</span></span>

* <span data-ttu-id="2e5aa-152">Correções para tornar o SDK mais resilientes ao failover automático em determinadas condições.</span><span class="sxs-lookup"><span data-stu-id="2e5aa-152">Fixes to make SDK more resilient to automatic failover under certain conditions.</span></span>

### <a name="a-name112112"></a><span data-ttu-id="2e5aa-153"><a name="1.1.2"/>1.1.2</span><span class="sxs-lookup"><span data-stu-id="2e5aa-153"><a name="1.1.2"/>1.1.2</span></span>

* <span data-ttu-id="2e5aa-154">Correção de um problema que eventualmente causa uma WebException: O nome remoto não pôde ser resolvido.</span><span class="sxs-lookup"><span data-stu-id="2e5aa-154">Fix for an issue that occasionally causes a WebException: The remote name could not be resolved.</span></span>
* <span data-ttu-id="2e5aa-155">Adição do suporte para ler um documento digitado diretamente com a adição de novas sobrecargas à API ReadDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="2e5aa-155">Added the support for directly reading a typed document by adding new overloads to ReadDocumentAsync API.</span></span>

### <a name="a-name111111"></a><span data-ttu-id="2e5aa-156"><a name="1.1.1"/>1.1.1</span><span class="sxs-lookup"><span data-stu-id="2e5aa-156"><a name="1.1.1"/>1.1.1</span></span>

* <span data-ttu-id="2e5aa-157">Adicionado suporte ao LINQ para consultas de agregação (CONT.NÚM, MÍNIMO, MÁXIMO, SOMA e MÉDIA).</span><span class="sxs-lookup"><span data-stu-id="2e5aa-157">Added LINQ support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="2e5aa-158">Correção de um problema de vazamento de memória do objeto ConnectionPolicy causado pelo uso do manipulador de eventos.</span><span class="sxs-lookup"><span data-stu-id="2e5aa-158">Fix for a memory leak issue for the ConnectionPolicy object caused by the use of event handler.</span></span>
* <span data-ttu-id="2e5aa-159">Correção de um problema no qual UpsertAttachmentAsync não estava funcionando quando ETag era usada.</span><span class="sxs-lookup"><span data-stu-id="2e5aa-159">Fix for an issue wherein UpsertAttachmentAsync was not working when ETag was used.</span></span>
* <span data-ttu-id="2e5aa-160">Correção de um problema no qual a continuação da consulta order-by entre partições não estava funcionando ao classificar no campo de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="2e5aa-160">Fix for an issue wherein cross partition order-by query continuation was not working when sorting on string field.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="2e5aa-161"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="2e5aa-161"><a name="1.1.0"/>1.1.0</span></span>

* <span data-ttu-id="2e5aa-162">Suporte adicionado para consultas de agregação (COUNT, MIN, MAX, SUM e AVG).</span><span class="sxs-lookup"><span data-stu-id="2e5aa-162">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="2e5aa-163">Veja [Suporte de agregação](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="2e5aa-163">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="2e5aa-164">Taxa de transferência mínima reduzida em coleções particionadas de 10.100 RU/s a 2500 RU/s.</span><span class="sxs-lookup"><span data-stu-id="2e5aa-164">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="2e5aa-165"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="2e5aa-165"><a name="1.0.0"/>1.0.0</span></span>

<span data-ttu-id="2e5aa-166">O SDK do .NET Core para Azure Cosmos DB permite criar aplicativos [ASP.NET Core](https://www.asp.net/core) e [.NET Core](https://www.microsoft.com/net/core#windows) rápidos de plataforma cruzada para execução em Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="2e5aa-166">The Azure Cosmos DB .NET Core SDK enables you to build fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps to run on Windows, Mac, and Linux.</span></span> <span data-ttu-id="2e5aa-167">A versão mais recente do SDK do .NET Core do Azure Cosmos DB é totalmente compatível com o [Xamarin](https://www.xamarin.com) e pode ser usada para criar aplicativos destinados a iOS, Android e Mono (Linux).</span><span class="sxs-lookup"><span data-stu-id="2e5aa-167">The latest release of the Azure Cosmos DB .NET Core SDK is fully [Xamarin](https://www.xamarin.com) compatible and be used to build applications that target iOS, Android, and Mono (Linux).</span></span>  

### <a name="a-name010-preview010-preview"></a><span data-ttu-id="2e5aa-168"><a name="0.1.0-preview"/>0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="2e5aa-168"><a name="0.1.0-preview"/>0.1.0-preview</span></span>

<span data-ttu-id="2e5aa-169">O SDK de Versão Prévia do .NET Core para Azure Cosmos DB permite criar aplicativos [ASP.NET Core](https://www.asp.net/core) e [.NET Core](https://www.microsoft.com/net/core#windows) rápidos de plataforma cruzada para execução em Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="2e5aa-169">The Azure Cosmos DB .NET Core Preview SDK enables you to build fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps to run on Windows, Mac, and Linux.</span></span>

<span data-ttu-id="2e5aa-170">O SDK de Versão Prévia do .NET Core do Azure Cosmos DB tem paridade de recurso com a versão mais recente do [SDK do .NET do Azure Cosmos DB](documentdb-sdk-dotnet.md) e dá suporte para o seguinte:</span><span class="sxs-lookup"><span data-stu-id="2e5aa-170">The Azure Cosmos DB .NET Core Preview SDK has feature parity with the latest version of the [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md) and supports the following:</span></span>
* <span data-ttu-id="2e5aa-171">Todos os [modos de conexão](performance-tips.md#networking): Modo de gateway, TCP Direto e HTTPs Direto.</span><span class="sxs-lookup"><span data-stu-id="2e5aa-171">All [connection modes](performance-tips.md#networking): Gateway mode, Direct TCP, and Direct HTTPs.</span></span> 
* <span data-ttu-id="2e5aa-172">Todos os [níveis de consistência](consistency-levels.md): Forte, Sessão, Desatualização Limitada e Eventual.</span><span class="sxs-lookup"><span data-stu-id="2e5aa-172">All [consistency levels](consistency-levels.md): Strong, Session, Bounded Staleness, and Eventual.</span></span>
* <span data-ttu-id="2e5aa-173">[Coleções particionadas](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="2e5aa-173">[Partitioned collections](partition-data.md).</span></span> 
* <span data-ttu-id="2e5aa-174">[Contas e replicação geográfica de banco de dados de várias regiões](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="2e5aa-174">[Multi-region database accounts and geo-replication](distribute-data-globally.md).</span></span>

<span data-ttu-id="2e5aa-175">Se você tiver dúvidas relacionadas a esse SDK, poste no [StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb) ou registre um problema no [repositório do github](https://github.com/Azure/azure-documentdb-dotnet/issues).</span><span class="sxs-lookup"><span data-stu-id="2e5aa-175">If you have questions related to this SDK, post to [StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), or file an issue in the [github repository](https://github.com/Azure/azure-documentdb-dotnet/issues).</span></span> 

## <a name="release--retirement-dates"></a><span data-ttu-id="2e5aa-176">Datas de lançamento e desativação</span><span class="sxs-lookup"><span data-stu-id="2e5aa-176">Release & Retirement Dates</span></span>

| <span data-ttu-id="2e5aa-177">Versão</span><span class="sxs-lookup"><span data-stu-id="2e5aa-177">Version</span></span> | <span data-ttu-id="2e5aa-178">Data do lançamento</span><span class="sxs-lookup"><span data-stu-id="2e5aa-178">Release Date</span></span> | <span data-ttu-id="2e5aa-179">Data de desativação</span><span class="sxs-lookup"><span data-stu-id="2e5aa-179">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="2e5aa-180">1.5.0</span><span class="sxs-lookup"><span data-stu-id="2e5aa-180">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="2e5aa-181">10 de agosto de 2017</span><span class="sxs-lookup"><span data-stu-id="2e5aa-181">August 10, 2017</span></span> |--- | 
| [<span data-ttu-id="2e5aa-182">1.4.1</span><span class="sxs-lookup"><span data-stu-id="2e5aa-182">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="2e5aa-183">7 de agosto de 2017</span><span class="sxs-lookup"><span data-stu-id="2e5aa-183">August 07, 2017</span></span> |--- |
| [<span data-ttu-id="2e5aa-184">1.4.0</span><span class="sxs-lookup"><span data-stu-id="2e5aa-184">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="2e5aa-185">2 de agosto de 2017</span><span class="sxs-lookup"><span data-stu-id="2e5aa-185">August 02, 2017</span></span> |--- |
| [<span data-ttu-id="2e5aa-186">1.3.2</span><span class="sxs-lookup"><span data-stu-id="2e5aa-186">1.3.2</span></span>](#1.3.2) |<span data-ttu-id="2e5aa-187">12 de junho de 2017</span><span class="sxs-lookup"><span data-stu-id="2e5aa-187">June 12, 2017</span></span> |--- |
| [<span data-ttu-id="2e5aa-188">1.3.1</span><span class="sxs-lookup"><span data-stu-id="2e5aa-188">1.3.1</span></span>](#1.3.1) |<span data-ttu-id="2e5aa-189">23 de maio de 2017</span><span class="sxs-lookup"><span data-stu-id="2e5aa-189">May 23, 2017</span></span> |--- |
| [<span data-ttu-id="2e5aa-190">1.3.0</span><span class="sxs-lookup"><span data-stu-id="2e5aa-190">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="2e5aa-191">10 de maio de 2017</span><span class="sxs-lookup"><span data-stu-id="2e5aa-191">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="2e5aa-192">1.2.2</span><span class="sxs-lookup"><span data-stu-id="2e5aa-192">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="2e5aa-193">19 de abril de 2017</span><span class="sxs-lookup"><span data-stu-id="2e5aa-193">April 19, 2017</span></span> |--- |
| [<span data-ttu-id="2e5aa-194">1.2.1</span><span class="sxs-lookup"><span data-stu-id="2e5aa-194">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="2e5aa-195">29 de março de 2017</span><span class="sxs-lookup"><span data-stu-id="2e5aa-195">March 29, 2017</span></span> |--- |
| [<span data-ttu-id="2e5aa-196">1.2.0</span><span class="sxs-lookup"><span data-stu-id="2e5aa-196">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="2e5aa-197">25 de março de 2017</span><span class="sxs-lookup"><span data-stu-id="2e5aa-197">March 25, 2017</span></span> |--- |
| [<span data-ttu-id="2e5aa-198">1.1.2</span><span class="sxs-lookup"><span data-stu-id="2e5aa-198">1.1.2</span></span>](#1.1.2) |<span data-ttu-id="2e5aa-199">20 de março de 2017</span><span class="sxs-lookup"><span data-stu-id="2e5aa-199">March 20, 2017</span></span> |--- |
| [<span data-ttu-id="2e5aa-200">1.1.1</span><span class="sxs-lookup"><span data-stu-id="2e5aa-200">1.1.1</span></span>](#1.1.1) |<span data-ttu-id="2e5aa-201">14 de março de 2017</span><span class="sxs-lookup"><span data-stu-id="2e5aa-201">March 14, 2017</span></span> |--- |
| [<span data-ttu-id="2e5aa-202">1.1.0</span><span class="sxs-lookup"><span data-stu-id="2e5aa-202">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="2e5aa-203">16 de fevereiro de 2017</span><span class="sxs-lookup"><span data-stu-id="2e5aa-203">February 16, 2017</span></span> |--- |
| [<span data-ttu-id="2e5aa-204">1.0.0</span><span class="sxs-lookup"><span data-stu-id="2e5aa-204">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="2e5aa-205">21 de dezembro de 2016</span><span class="sxs-lookup"><span data-stu-id="2e5aa-205">December 21, 2016</span></span> |--- |
| [<span data-ttu-id="2e5aa-206">0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="2e5aa-206">0.1.0-preview</span></span>](#0.1.0-preview) |<span data-ttu-id="2e5aa-207">15 de novembro de 2016</span><span class="sxs-lookup"><span data-stu-id="2e5aa-207">November 15, 2016</span></span> |<span data-ttu-id="2e5aa-208">31 de dezembro de 2016</span><span class="sxs-lookup"><span data-stu-id="2e5aa-208">December 31, 2016</span></span> |

## <a name="see-also"></a><span data-ttu-id="2e5aa-209">Consulte também</span><span class="sxs-lookup"><span data-stu-id="2e5aa-209">See Also</span></span>
<span data-ttu-id="2e5aa-210">Para saber mais sobre o Cosmos DB, consulte a página de serviço do [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="2e5aa-210">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

