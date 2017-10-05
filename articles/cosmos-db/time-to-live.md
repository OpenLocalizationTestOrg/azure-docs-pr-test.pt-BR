---
title: "Expirar os dados no Azure Cosmos DB com a vida útil | Microsoft Docs"
description: "Com a TTL, o Microsoft Azure Cosmos DB fornece a capacidade de limpar documentos automaticamente do sistema após determinado período."
services: cosmos-db
documentationcenter: 
keywords: "vida útil"
author: arramac
manager: jhubbard
editor: 
ms.assetid: 25fcbbda-71f7-414a-bf57-d8671358ca3f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: 6f1c43ca0113dc7579b0fc3743d3314c16ce78a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-to-live"></a><span data-ttu-id="d1868-104">Expirar os dados em coleções do Azure Cosmos DB automaticamente com a vida útil</span><span class="sxs-lookup"><span data-stu-id="d1868-104">Expire data in Azure Cosmos DB collections automatically with time to live</span></span>
<span data-ttu-id="d1868-105">Os aplicativos podem gerar e armazenar grandes quantidades de dados.</span><span class="sxs-lookup"><span data-stu-id="d1868-105">Applications can produce and store vast amounts of data.</span></span> <span data-ttu-id="d1868-106">Alguns desses dados, como dados de evento, logs e informações da sessão do usuário gerados por computador, são úteis apenas por determinado período.</span><span class="sxs-lookup"><span data-stu-id="d1868-106">Some of this data, like machine generated event data, logs, and user session information is only useful for a finite period of time.</span></span> <span data-ttu-id="d1868-107">Depois que os dados se tornam excedentes para as necessidades do aplicativo, é seguro limpar esses dados e reduzir as necessidades de armazenamento de um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d1868-107">Once the data becomes surplus to the needs of the application it is safe to purge this data and reduce the storage needs of an application.</span></span>

<span data-ttu-id="d1868-108">Com a “vida útil” ou TTL, o Microsoft Azure Cosmos DB fornece a capacidade de limpar documentos automaticamente do banco de dados após determinado período.</span><span class="sxs-lookup"><span data-stu-id="d1868-108">With "time to live" or TTL, Microsoft Azure Cosmos DB provides the ability to have documents automatically purged from the database after a period of time.</span></span> <span data-ttu-id="d1868-109">A vida útil padrão pode ser definida no nível de coleção e substituída conforme o documento.</span><span class="sxs-lookup"><span data-stu-id="d1868-109">The default time to live can be set at the collection level, and overridden on a per-document basis.</span></span> <span data-ttu-id="d1868-110">Depois de definir a TTL como um padrão de coleta ou em um nível de documento, o Cosmos DB removerá automaticamente os documentos existentes após esse período, em segundos, desde sua última modificação.</span><span class="sxs-lookup"><span data-stu-id="d1868-110">Once TTL is set, either as a collection default or at a document level, Cosmos DB will automatically remove documents that exist after that period of time, in seconds, since they were last modified.</span></span>

<span data-ttu-id="d1868-111">A vida útil no Cosmos DB usa um deslocamento em relação à data da última modificação do documento.</span><span class="sxs-lookup"><span data-stu-id="d1868-111">Time to live in Cosmos DB uses an offset against when the document was last modified.</span></span> <span data-ttu-id="d1868-112">Para fazer isso, ela usa o campo `_ts`, encontrado em todos os documentos.</span><span class="sxs-lookup"><span data-stu-id="d1868-112">To do this it uses the `_ts` field which exists on every document.</span></span> <span data-ttu-id="d1868-113">O campo _ts é um carimbo de data/hora de época estilo Unix que representa a data e a hora.</span><span class="sxs-lookup"><span data-stu-id="d1868-113">The _ts field is a unix-style epoch timestamp representing the date and time.</span></span> <span data-ttu-id="d1868-114">O campo `_ts` é atualizado sempre que um documento é modificado.</span><span class="sxs-lookup"><span data-stu-id="d1868-114">The `_ts` field is updated every time a document is modified.</span></span> 

## <a name="ttl-behavior"></a><span data-ttu-id="d1868-115">Comportamento de TTL</span><span class="sxs-lookup"><span data-stu-id="d1868-115">TTL behavior</span></span>
<span data-ttu-id="d1868-116">O recurso TTL é controlado pelas propriedades TTL em dois níveis: o nível de coleção e o nível de documento.</span><span class="sxs-lookup"><span data-stu-id="d1868-116">The TTL feature is controlled by TTL properties at two levels - the collection level and the document level.</span></span> <span data-ttu-id="d1868-117">Os valores são definidos em segundos e tratados como um delta no `_ts` em que o documento foi modificado pela última vez.</span><span class="sxs-lookup"><span data-stu-id="d1868-117">The values are set in seconds and are treated as a delta from the `_ts` that the document was last modified at.</span></span>

1. <span data-ttu-id="d1868-118">DefaultTTL da coleção</span><span class="sxs-lookup"><span data-stu-id="d1868-118">DefaultTTL for the collection</span></span>
   
   * <span data-ttu-id="d1868-119">Se estiverem ausentes (ou definidos como nulos), os documentos não serão excluídos automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d1868-119">If missing (or set to null), documents are not deleted automatically.</span></span>
   * <span data-ttu-id="d1868-120">Se estiverem presentes e o valor for "-1" = infinito, os documentos não expirarão por padrão</span><span class="sxs-lookup"><span data-stu-id="d1868-120">If present and the value is "-1" = infinite – documents don’t expire by default</span></span>
   * <span data-ttu-id="d1868-121">Se estiverem presentes e o valor for qualquer número ("n"), os documentos expirarão em "n" segundos após a última modificação</span><span class="sxs-lookup"><span data-stu-id="d1868-121">If present and the value is some number ("n") – documents expire "n” seconds after last modification</span></span>
2. <span data-ttu-id="d1868-122">TTL dos documentos:</span><span class="sxs-lookup"><span data-stu-id="d1868-122">TTL for the documents:</span></span> 
   
   * <span data-ttu-id="d1868-123">A propriedade será aplicável somente se houver uma DefaultTTL para a coleção pai.</span><span class="sxs-lookup"><span data-stu-id="d1868-123">Property is applicable only if DefaultTTL is present for the parent collection.</span></span>
   * <span data-ttu-id="d1868-124">Substitui o valor de DefaultTTL da coleção pai.</span><span class="sxs-lookup"><span data-stu-id="d1868-124">Overrides the DefaultTTL value for the parent collection.</span></span>

<span data-ttu-id="d1868-125">Assim que o documento tiver expirado (`ttl` + `_ts` >= hora atual do servidor), o documento será marcado como "expirado".</span><span class="sxs-lookup"><span data-stu-id="d1868-125">As soon as the document has expired (`ttl` + `_ts` >= current server time), the document is marked as "expired”.</span></span> <span data-ttu-id="d1868-126">Nenhuma operação será permitida nesses documentos após esse período e elas serão excluídas dos resultados de todas as consultas executadas.</span><span class="sxs-lookup"><span data-stu-id="d1868-126">No operation will be allowed on these documents after this time and they will be excluded from the results of any queries performed.</span></span> <span data-ttu-id="d1868-127">Os documentos são excluídos fisicamente no sistema e são excluídos em segundo plano oportunamente em um momento posterior.</span><span class="sxs-lookup"><span data-stu-id="d1868-127">The documents are physically deleted in the system, and are deleted in the background opportunistically at a later time.</span></span> <span data-ttu-id="d1868-128">Isso não consome nenhuma [RU (Unidade de Solicitação)](request-units.md) do orçamento da coleção.</span><span class="sxs-lookup"><span data-stu-id="d1868-128">This does not consume any [Request Units (RUs)](request-units.md) from the collection budget.</span></span>

<span data-ttu-id="d1868-129">A lógica acima pode ser mostrada na matriz a seguir:</span><span class="sxs-lookup"><span data-stu-id="d1868-129">The above logic can be shown in the following matrix:</span></span>

|  | <span data-ttu-id="d1868-130">DefaultTTL ausente/não definida na coleção</span><span class="sxs-lookup"><span data-stu-id="d1868-130">DefaultTTL missing/not set on the collection</span></span> | <span data-ttu-id="d1868-131">DefaultTTL = -1 na coleção</span><span class="sxs-lookup"><span data-stu-id="d1868-131">DefaultTTL = -1 on collection</span></span> | <span data-ttu-id="d1868-132">DefaultTTL = “n” na coleção</span><span class="sxs-lookup"><span data-stu-id="d1868-132">DefaultTTL = "n" on collection</span></span> |
| --- |:--- |:--- |:--- |
| <span data-ttu-id="d1868-133">TTL Ausente no documento</span><span class="sxs-lookup"><span data-stu-id="d1868-133">TTL Missing on document</span></span> |<span data-ttu-id="d1868-134">Nada para substituir no nível de documento, pois o documento e a coleção não têm nenhum conceito de TTL.</span><span class="sxs-lookup"><span data-stu-id="d1868-134">Nothing to override at document level since both the document and collection have no concept of TTL.</span></span> |<span data-ttu-id="d1868-135">Nenhum documento nesta coleção expirará.</span><span class="sxs-lookup"><span data-stu-id="d1868-135">No documents in this collection will expire.</span></span> |<span data-ttu-id="d1868-136">Os documentos nessa coleção expirarão quando o intervalo de n expirar.</span><span class="sxs-lookup"><span data-stu-id="d1868-136">The documents in this collection will expire when interval n elapses.</span></span> |
| <span data-ttu-id="d1868-137">TTL = -1 no documento</span><span class="sxs-lookup"><span data-stu-id="d1868-137">TTL = -1 on document</span></span> |<span data-ttu-id="d1868-138">Nada para substituir no nível de documento, pois a coleção não define a propriedade DefaultTTL que pode ser substituída por um documento.</span><span class="sxs-lookup"><span data-stu-id="d1868-138">Nothing to override at the document level since the collection doesn’t define the DefaultTTL property that a document can override.</span></span> <span data-ttu-id="d1868-139">A TTL de um documento não é interpretada pelo sistema.</span><span class="sxs-lookup"><span data-stu-id="d1868-139">TTL on a document is un-interpreted by the system.</span></span> |<span data-ttu-id="d1868-140">Nenhum documento nesta coleção expirará.</span><span class="sxs-lookup"><span data-stu-id="d1868-140">No documents in this collection will expire.</span></span> |<span data-ttu-id="d1868-141">O documento com TTL = -1 nesta coleção nunca expirará.</span><span class="sxs-lookup"><span data-stu-id="d1868-141">The document with TTL=-1 in this collection will never expire.</span></span> <span data-ttu-id="d1868-142">Todos os outros documentos expirarão após o intervalo de “n”.</span><span class="sxs-lookup"><span data-stu-id="d1868-142">All other documents will expire after "n" interval.</span></span> |
| <span data-ttu-id="d1868-143">TTL = n no documento</span><span class="sxs-lookup"><span data-stu-id="d1868-143">TTL = n on document</span></span> |<span data-ttu-id="d1868-144">Nada para substituir no nível de documento.</span><span class="sxs-lookup"><span data-stu-id="d1868-144">Nothing to override at the document level.</span></span> <span data-ttu-id="d1868-145">A TTL de um documento não é interpretada pelo sistema.</span><span class="sxs-lookup"><span data-stu-id="d1868-145">TTL on a document in un-interpreted by the system.</span></span> |<span data-ttu-id="d1868-146">O documento com TTL = n expirará após o intervalo de n, em segundos.</span><span class="sxs-lookup"><span data-stu-id="d1868-146">The document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="d1868-147">Os outros documentos herdarão o intervalo de -1 e nunca expirarão.</span><span class="sxs-lookup"><span data-stu-id="d1868-147">Other documents will inherit interval of -1 and never expire.</span></span> |<span data-ttu-id="d1868-148">O documento com TTL = n expirará após o intervalo de n, em segundos.</span><span class="sxs-lookup"><span data-stu-id="d1868-148">The document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="d1868-149">Os outros documentos herdarão o intervalo de “n” da coleção.</span><span class="sxs-lookup"><span data-stu-id="d1868-149">Other documents will inherit "n" interval from the collection.</span></span> |

## <a name="configuring-ttl"></a><span data-ttu-id="d1868-150">Configurando a TTL</span><span class="sxs-lookup"><span data-stu-id="d1868-150">Configuring TTL</span></span>
<span data-ttu-id="d1868-151">Por padrão, a vida útil é desabilitada por padrão em todas as coleções e todos os documentos do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d1868-151">By default, time to live is disabled by default in all Cosmos DB collections and on all documents.</span></span>

## <a name="enabling-ttl"></a><span data-ttu-id="d1868-152">Habilitando a TTL</span><span class="sxs-lookup"><span data-stu-id="d1868-152">Enabling TTL</span></span>
<span data-ttu-id="d1868-153">Para habilitar a TTL em uma coleção, ou no documento em uma coleção, é necessário definir a propriedade DefaultTTL de uma coleção como -1 ou um número positivo diferente de zero.</span><span class="sxs-lookup"><span data-stu-id="d1868-153">To enable TTL on a collection, or the documents within a collection, you need to set the DefaultTTL property of a collection to either -1 or a non-zero positive number.</span></span> <span data-ttu-id="d1868-154">Definir a DefaultTTL como -1 significa que, por padrão, todos os documentos na coleção residirão para sempre, mas o serviço Cosmos DB deverá monitorar, nessa coleção, os documentos que substituíram esse padrão.</span><span class="sxs-lookup"><span data-stu-id="d1868-154">Setting the DefaultTTL to -1 means that by default all documents in the collection will live forever but the Cosmos DB service should monitor this collection for documents that have overridden this default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a><span data-ttu-id="d1868-155">Configurando a TTL padrão em uma coleção</span><span class="sxs-lookup"><span data-stu-id="d1868-155">Configuring default TTL on a collection</span></span>
<span data-ttu-id="d1868-156">É possível configurar uma vida útil padrão em um nível de coleção.</span><span class="sxs-lookup"><span data-stu-id="d1868-156">You are able to configure a default time to live at a collection level.</span></span> <span data-ttu-id="d1868-157">Para definir a TTL em uma coleção, é necessário fornecer um número positivo diferente de zero que indique o período, em segundos, para expirar todos os documentos na coleção após o último carimbo de data/hora modificado do documento (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="d1868-157">To set the TTL on a collection, you need to provide a non-zero positive number that indicates the period, in seconds, to expire all documents in the collection after the last modified timestamp of the document (`_ts`).</span></span> <span data-ttu-id="d1868-158">Outra opção é definir o padrão como -1, o que significa que, por padrão, todos os documentos inseridos na coleção residirão por tempo indeterminado.</span><span class="sxs-lookup"><span data-stu-id="d1868-158">Or, you can set the default to -1, which implies that all documents inserted in to the collection will live indefinitely by default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a><span data-ttu-id="d1868-159">Configurando a TTL em um documento</span><span class="sxs-lookup"><span data-stu-id="d1868-159">Setting TTL on a document</span></span>
<span data-ttu-id="d1868-160">Além de definir uma TTL padrão em uma coleção, é possível definir uma TTL específica em um nível de documento.</span><span class="sxs-lookup"><span data-stu-id="d1868-160">In addition to setting a default TTL on a collection you can set specific TTL at a document level.</span></span> <span data-ttu-id="d1868-161">Isso substituirá o padrão da coleção.</span><span class="sxs-lookup"><span data-stu-id="d1868-161">Doing this will override the default of the collection.</span></span>

* <span data-ttu-id="d1868-162">Para definir a TTL em um documento, é necessário fornecer um número positivo diferente de zero que indique o período, em segundos, para expirar todos os documentos após o último carimbo de data/hora modificado do documento (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="d1868-162">To set the TTL on a document, you need to provide a non-zero positive number which indicates the period, in seconds, to expire the document after the last modified timestamp of the document (`_ts`).</span></span>
* <span data-ttu-id="d1868-163">Se um documento não tiver um campo TTL, será aplicado o padrão da coleção.</span><span class="sxs-lookup"><span data-stu-id="d1868-163">If a document has no TTL field, then the default of the collection will apply.</span></span>
* <span data-ttu-id="d1868-164">Se a TTL estiver desabilitada no nível de coleção, o campo TTL no documento será ignorado até que a TTL seja habilitada novamente na coleção.</span><span class="sxs-lookup"><span data-stu-id="d1868-164">If TTL is disabled at the collection level, the TTL field on the document will be ignored until TTL is enabled again on the collection.</span></span>

<span data-ttu-id="d1868-165">Veja a seguir um trecho que mostra como definir a expiração de TTL em um documento:</span><span class="sxs-lookup"><span data-stu-id="d1868-165">Here's a snippet showing how to set the TTL expiration on a document:</span></span>

    // Include a property that serializes to "ttl" in JSON
    public class SalesOrder
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        
        [JsonProperty(PropertyName="cid")]
        public string CustomerId { get; set; }
        
        // used to set expiration policy
        [JsonProperty(PropertyName = "ttl", NullValueHandling = NullValueHandling.Ignore)]
        public int? TimeToLive { get; set; }
        
        //...
    }
    
    // Set the value to the expiration in seconds
    SalesOrder salesOrder = new SalesOrder
    {
        Id = "SO05",
        CustomerId = "CO18009186470",
        TimeToLive = 60 * 60 * 24 * 30;  // Expire sales orders in 30 days 
    };


## <a name="extending-ttl-on-an-existing-document"></a><span data-ttu-id="d1868-166">Estendendo a TTL em um documento existente</span><span class="sxs-lookup"><span data-stu-id="d1868-166">Extending TTL on an existing document</span></span>
<span data-ttu-id="d1868-167">É possível redefinir a TTL em um documento executando qualquer operação de gravação no documento.</span><span class="sxs-lookup"><span data-stu-id="d1868-167">You can reset the TTL on a document by doing any write operation on the document.</span></span> <span data-ttu-id="d1868-168">Isso definirá o `_ts` como a hora atual, e a contagem regressiva para a expiração do documento, conforme definido pela `ttl`, será iniciada novamente.</span><span class="sxs-lookup"><span data-stu-id="d1868-168">Doing this will set the `_ts` to the current time, and the countdown to the document expiry, as set by the `ttl`, will begin again.</span></span> <span data-ttu-id="d1868-169">Se deseja alterar a `ttl` de um documento, é possível atualizar o campo da mesma forma que qualquer outro campo configurável.</span><span class="sxs-lookup"><span data-stu-id="d1868-169">If you wish to change the `ttl` of a document, you can update the field as you can do with any other settable field.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time to live
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a><span data-ttu-id="d1868-170">Removendo a TTL de um documento</span><span class="sxs-lookup"><span data-stu-id="d1868-170">Removing TTL from a document</span></span>
<span data-ttu-id="d1868-171">Se uma TTL tiver sido definida em um documento e você não deseja mais que o documento expire, é possível recuperar o documento, remover campo TTL e substituir o documento no servidor.</span><span class="sxs-lookup"><span data-stu-id="d1868-171">If a TTL has been set on a document and you no longer want that document to expire, then you can retrieve the document, remove the TTL field and replace the document on the server.</span></span> <span data-ttu-id="d1868-172">Quando o campo TTL for removido do documento, será aplicado o padrão da coleção.</span><span class="sxs-lookup"><span data-stu-id="d1868-172">When the TTL field is removed from the document, the default of the collection will be applied.</span></span> <span data-ttu-id="d1868-173">Para interromper a expiração de um documento e fazer com ele não herde da coleção, é necessário definir o valor de TTL como -1.</span><span class="sxs-lookup"><span data-stu-id="d1868-173">To stop a document from expiring and not inherit from the collection then you need to set the TTL value to -1.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit the default TTL of the collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a><span data-ttu-id="d1868-174">Desabilitando a TTL</span><span class="sxs-lookup"><span data-stu-id="d1868-174">Disabling TTL</span></span>
<span data-ttu-id="d1868-175">Para desabilitar a TTL por completo em uma coleção e fazer com que o processo em segundo plano pare de procurar documentos expirados, a propriedade de DefaultTTL na coleção deve ser excluída.</span><span class="sxs-lookup"><span data-stu-id="d1868-175">To disable TTL entirely on a collection and stop the background process from looking for expired documents the DefaultTTL property on the collection should be deleted.</span></span> <span data-ttu-id="d1868-176">A exclusão dessa propriedade é diferente de defini-la como -1.</span><span class="sxs-lookup"><span data-stu-id="d1868-176">Deleting this property is different from setting it to -1.</span></span> <span data-ttu-id="d1868-177">A configuração como -1 significa que os novos documentos adicionados à coleção residirão para sempre, mas é possível substituí-la em documentos específicos da coleção.</span><span class="sxs-lookup"><span data-stu-id="d1868-177">Setting to -1 means new documents added to the collection will live forever but you can override this on specific documents in the collection.</span></span> <span data-ttu-id="d1868-178">Remover esta propriedade por completo da coleção significa que os documentos não expirarão, mesmo que haja documentos que tenham explicitamente substituído um padrão anterior.</span><span class="sxs-lookup"><span data-stu-id="d1868-178">Removing this property entirely from the collection means that no documents will expire, even if there are documents that have explicitly overridden a previous default.</span></span>

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a><span data-ttu-id="d1868-179">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="d1868-179">FAQ</span></span>
<span data-ttu-id="d1868-180">**Qual o preço da TTL?**</span><span class="sxs-lookup"><span data-stu-id="d1868-180">**What will TTL cost me?**</span></span>

<span data-ttu-id="d1868-181">Não há nenhum custo adicional para definição de uma TTL em um documento.</span><span class="sxs-lookup"><span data-stu-id="d1868-181">There is no additional cost to setting a TTL on a document.</span></span>

<span data-ttu-id="d1868-182">**Quanto tempo levará para que meu documento seja excluído após a habilitação da TTL?**</span><span class="sxs-lookup"><span data-stu-id="d1868-182">**How long will it take to delete my document once the TTL is up?**</span></span>

<span data-ttu-id="d1868-183">Os documentos expiram imediatamente depois da TTL ser ativada e não poderão ser acessados por meio do CRUD ou das APIs de consulta.</span><span class="sxs-lookup"><span data-stu-id="d1868-183">The documents are expired immediately once the TTL is up, and will not be accessible via CRUD or query APIs.</span></span> 

<span data-ttu-id="d1868-184">**A TTL em um documento terá algum impacto sobre os encargos de RU?**</span><span class="sxs-lookup"><span data-stu-id="d1868-184">**Will TTL on a document have any impact on RU charges?**</span></span>

<span data-ttu-id="d1868-185">Não haverá nenhum impacto nos encargos de RU para as exclusões de documentos expirados por meio da TTL no Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d1868-185">No, there will be no impact on RU charges for deletions of expired documents via TTL in Cosmos DB.</span></span>

<span data-ttu-id="d1868-186">**O recurso TTL se aplica somente a documentos inteiros ou valores de propriedade de documentos individuais podem ser expirados?**</span><span class="sxs-lookup"><span data-stu-id="d1868-186">**Does the TTL feature only apply to entire documents, or can I expire individual document property values?**</span></span>

<span data-ttu-id="d1868-187">A TTL se aplica a todo o documento.</span><span class="sxs-lookup"><span data-stu-id="d1868-187">TTL applies to the entire document.</span></span> <span data-ttu-id="d1868-188">Caso você queira que apenas uma parte de um documento expire, é recomendável extrair a parte do documento principal em um documento "vinculado" à parte e, em seguida, usar a TTL nesse documento extraído.</span><span class="sxs-lookup"><span data-stu-id="d1868-188">If you would like to expire just a portion of a document, then it is recommended that you extract the portion from the main document in to a separate "linked” document and then use TTL on that extracted document.</span></span>

<span data-ttu-id="d1868-189">**O recurso TTL tem requisitos específicos de indexação?**</span><span class="sxs-lookup"><span data-stu-id="d1868-189">**Does the TTL feature have any specific indexing requirements?**</span></span>

<span data-ttu-id="d1868-190">Sim.</span><span class="sxs-lookup"><span data-stu-id="d1868-190">Yes.</span></span> <span data-ttu-id="d1868-191">A coleção deve ter uma [política de indexação definida](indexing-policies.md) como Consistente ou Lenta.</span><span class="sxs-lookup"><span data-stu-id="d1868-191">The collection must have [indexing policy set](indexing-policies.md) to either Consistent or Lazy.</span></span> <span data-ttu-id="d1868-192">A tentativa de definir a DefaultTTL em uma coleção com a indexação definida como Nenhum resultará em um erro, assim como a tentativa de desativar a indexação em uma coleção que tenha uma DefaultTTL já definida.</span><span class="sxs-lookup"><span data-stu-id="d1868-192">Trying to set DefaultTTL on a collection with indexing set to None will result in an error, as will trying to turn off indexing on a collection that has a DefaultTTL already set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1868-193">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d1868-193">Next steps</span></span>
<span data-ttu-id="d1868-194">Para saber mais sobre o Azure Cosmos DB, consulte a página de [*documentação*](https://azure.microsoft.com/documentation/services/cosmos-db/) do serviço.</span><span class="sxs-lookup"><span data-stu-id="d1868-194">To learn more about Azure Cosmos DB, refer to the service [*documentation*](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span>

