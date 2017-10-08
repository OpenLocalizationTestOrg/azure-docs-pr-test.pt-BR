---
title: dados de aaaExpire no banco de dados do Azure Cosmos com tempo toolive | Microsoft Docs
description: "Com TTL, o banco de dados do Microsoft Azure Cosmos fornece documentos de toohave de capacidade de saudação automaticamente excluídos do sistema Olá após um período de tempo."
services: cosmos-db
documentationcenter: 
keywords: tempo toolive
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
ms.openlocfilehash: 51d8ec46add72c9624457316a4ccd1e23fb83ad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-toolive"></a><span data-ttu-id="db7ed-104">Expirar os dados em coleções do banco de dados do Azure Cosmos automaticamente com o tempo toolive</span><span class="sxs-lookup"><span data-stu-id="db7ed-104">Expire data in Azure Cosmos DB collections automatically with time toolive</span></span>
<span data-ttu-id="db7ed-105">Os aplicativos podem gerar e armazenar grandes quantidades de dados.</span><span class="sxs-lookup"><span data-stu-id="db7ed-105">Applications can produce and store vast amounts of data.</span></span> <span data-ttu-id="db7ed-106">Alguns desses dados, como dados de evento, logs e informações da sessão do usuário gerados por computador, são úteis apenas por determinado período.</span><span class="sxs-lookup"><span data-stu-id="db7ed-106">Some of this data, like machine generated event data, logs, and user session information is only useful for a finite period of time.</span></span> <span data-ttu-id="db7ed-107">Quando dados saudação se torna toohello excedente necessidades do aplicativo hello é seguro toopurge esses dados e reduz a necessidade de armazenamento de saudação de um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="db7ed-107">Once hello data becomes surplus toohello needs of hello application it is safe toopurge this data and reduce hello storage needs of an application.</span></span>

<span data-ttu-id="db7ed-108">"Tempo toolive" ou TTL, o banco de dados do Microsoft Azure Cosmos fornece documentos de toohave de capacidade Olá limpos automaticamente do banco de dados de saudação após um período de tempo.</span><span class="sxs-lookup"><span data-stu-id="db7ed-108">With "time toolive" or TTL, Microsoft Azure Cosmos DB provides hello ability toohave documents automatically purged from hello database after a period of time.</span></span> <span data-ttu-id="db7ed-109">tempo de padrão de saudação toolive pode ser definido no nível de coleção hello e substituído em uma base por documento.</span><span class="sxs-lookup"><span data-stu-id="db7ed-109">hello default time toolive can be set at hello collection level, and overridden on a per-document basis.</span></span> <span data-ttu-id="db7ed-110">Depois de definir a TTL como um padrão de coleta ou em um nível de documento, o Cosmos DB removerá automaticamente os documentos existentes após esse período, em segundos, desde sua última modificação.</span><span class="sxs-lookup"><span data-stu-id="db7ed-110">Once TTL is set, either as a collection default or at a document level, Cosmos DB will automatically remove documents that exist after that period of time, in seconds, since they were last modified.</span></span>

<span data-ttu-id="db7ed-111">Tempo toolive no banco de dados do Cosmos usa um deslocamento em relação ao documento hello foi modificada pela última vez.</span><span class="sxs-lookup"><span data-stu-id="db7ed-111">Time toolive in Cosmos DB uses an offset against when hello document was last modified.</span></span> <span data-ttu-id="db7ed-112">toodo este TI utiliza Olá `_ts` campo que existe em todos os documentos.</span><span class="sxs-lookup"><span data-stu-id="db7ed-112">toodo this it uses hello `_ts` field which exists on every document.</span></span> <span data-ttu-id="db7ed-113">campo de TS Olá é estilo unix época timestamp representando Olá data e hora.</span><span class="sxs-lookup"><span data-stu-id="db7ed-113">hello _ts field is a unix-style epoch timestamp representing hello date and time.</span></span> <span data-ttu-id="db7ed-114">Olá `_ts` campo é atualizado sempre que um documento é modificado.</span><span class="sxs-lookup"><span data-stu-id="db7ed-114">hello `_ts` field is updated every time a document is modified.</span></span> 

## <a name="ttl-behavior"></a><span data-ttu-id="db7ed-115">Comportamento de TTL</span><span class="sxs-lookup"><span data-stu-id="db7ed-115">TTL behavior</span></span>
<span data-ttu-id="db7ed-116">recurso TTL Olá é controlado pelas propriedades TTL em dois níveis - nível de documento hello e coleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="db7ed-116">hello TTL feature is controlled by TTL properties at two levels - hello collection level and hello document level.</span></span> <span data-ttu-id="db7ed-117">os valores Hello são definidos em segundos e são tratados como um delta de saudação `_ts` documento hello foi modificada pela última vez em.</span><span class="sxs-lookup"><span data-stu-id="db7ed-117">hello values are set in seconds and are treated as a delta from hello `_ts` that hello document was last modified at.</span></span>

1. <span data-ttu-id="db7ed-118">DefaultTTL para coleção Olá</span><span class="sxs-lookup"><span data-stu-id="db7ed-118">DefaultTTL for hello collection</span></span>
   
   * <span data-ttu-id="db7ed-119">Se ausente (ou conjunto toonull), documentos não são excluídos automaticamente.</span><span class="sxs-lookup"><span data-stu-id="db7ed-119">If missing (or set toonull), documents are not deleted automatically.</span></span>
   * <span data-ttu-id="db7ed-120">Se estiver presente e o valor de saudação é "-1" = infinito – documentos não expiram por padrão</span><span class="sxs-lookup"><span data-stu-id="db7ed-120">If present and hello value is "-1" = infinite – documents don’t expire by default</span></span>
   * <span data-ttu-id="db7ed-121">Se estiver presente e o valor de saudação é um número ("n") – documentos expiram "n" segundos depois da última modificação</span><span class="sxs-lookup"><span data-stu-id="db7ed-121">If present and hello value is some number ("n") – documents expire "n” seconds after last modification</span></span>
2. <span data-ttu-id="db7ed-122">Tempo de vida para documentos de saudação:</span><span class="sxs-lookup"><span data-stu-id="db7ed-122">TTL for hello documents:</span></span> 
   
   * <span data-ttu-id="db7ed-123">Propriedade é aplicável somente se DefaultTTL está presente para da coleção pai hello.</span><span class="sxs-lookup"><span data-stu-id="db7ed-123">Property is applicable only if DefaultTTL is present for hello parent collection.</span></span>
   * <span data-ttu-id="db7ed-124">Substitui Olá DefaultTTL valor da coleção pai hello.</span><span class="sxs-lookup"><span data-stu-id="db7ed-124">Overrides hello DefaultTTL value for hello parent collection.</span></span>

<span data-ttu-id="db7ed-125">Assim que o documento de saudação expirou (`ttl`  +  `_ts` > = hora atual do servidor), Olá é marcada como "expirado".</span><span class="sxs-lookup"><span data-stu-id="db7ed-125">As soon as hello document has expired (`ttl` + `_ts` >= current server time), hello document is marked as "expired”.</span></span> <span data-ttu-id="db7ed-126">Nenhuma operação poderá ser nesses documentos depois desse período e elas serão excluídas dos resultados de saudação de todas as consultas executadas.</span><span class="sxs-lookup"><span data-stu-id="db7ed-126">No operation will be allowed on these documents after this time and they will be excluded from hello results of any queries performed.</span></span> <span data-ttu-id="db7ed-127">documentos de saudação são fisicamente no sistema de saudação e são excluídos no plano de fundo de saudação oportunamente mais tarde.</span><span class="sxs-lookup"><span data-stu-id="db7ed-127">hello documents are physically deleted in hello system, and are deleted in hello background opportunistically at a later time.</span></span> <span data-ttu-id="db7ed-128">Isso não consumir qualquer [unidades de solicitação (RUs)](request-units.md) orçamento de coleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="db7ed-128">This does not consume any [Request Units (RUs)](request-units.md) from hello collection budget.</span></span>

<span data-ttu-id="db7ed-129">Olá acima lógica pode ser mostrado no Olá matriz a seguir:</span><span class="sxs-lookup"><span data-stu-id="db7ed-129">hello above logic can be shown in hello following matrix:</span></span>

|  | <span data-ttu-id="db7ed-130">DefaultTTL ausente ou não definido na coleção de saudação</span><span class="sxs-lookup"><span data-stu-id="db7ed-130">DefaultTTL missing/not set on hello collection</span></span> | <span data-ttu-id="db7ed-131">DefaultTTL = -1 na coleção</span><span class="sxs-lookup"><span data-stu-id="db7ed-131">DefaultTTL = -1 on collection</span></span> | <span data-ttu-id="db7ed-132">DefaultTTL = “n” na coleção</span><span class="sxs-lookup"><span data-stu-id="db7ed-132">DefaultTTL = "n" on collection</span></span> |
| --- |:--- |:--- |:--- |
| <span data-ttu-id="db7ed-133">TTL Ausente no documento</span><span class="sxs-lookup"><span data-stu-id="db7ed-133">TTL Missing on document</span></span> |<span data-ttu-id="db7ed-134">Nada toooverride no nível do documento como documento hello e coleção não tem nenhum conceito de TTL.</span><span class="sxs-lookup"><span data-stu-id="db7ed-134">Nothing toooverride at document level since both hello document and collection have no concept of TTL.</span></span> |<span data-ttu-id="db7ed-135">Nenhum documento nesta coleção expirará.</span><span class="sxs-lookup"><span data-stu-id="db7ed-135">No documents in this collection will expire.</span></span> |<span data-ttu-id="db7ed-136">documentos de saudação nesta coleção expirará quando n intervalo expira.</span><span class="sxs-lookup"><span data-stu-id="db7ed-136">hello documents in this collection will expire when interval n elapses.</span></span> |
| <span data-ttu-id="db7ed-137">TTL = -1 no documento</span><span class="sxs-lookup"><span data-stu-id="db7ed-137">TTL = -1 on document</span></span> |<span data-ttu-id="db7ed-138">Nada toooverride no nível do documento hello desde que não define a coleção Olá Olá propriedade DefaultTTL que pode substituir um documento.</span><span class="sxs-lookup"><span data-stu-id="db7ed-138">Nothing toooverride at hello document level since hello collection doesn’t define hello DefaultTTL property that a document can override.</span></span> <span data-ttu-id="db7ed-139">Tempo de vida de um documento é não interpretado pelo sistema hello.</span><span class="sxs-lookup"><span data-stu-id="db7ed-139">TTL on a document is un-interpreted by hello system.</span></span> |<span data-ttu-id="db7ed-140">Nenhum documento nesta coleção expirará.</span><span class="sxs-lookup"><span data-stu-id="db7ed-140">No documents in this collection will expire.</span></span> |<span data-ttu-id="db7ed-141">documento de saudação com TTL =-1 nesta coleção nunca expirará.</span><span class="sxs-lookup"><span data-stu-id="db7ed-141">hello document with TTL=-1 in this collection will never expire.</span></span> <span data-ttu-id="db7ed-142">Todos os outros documentos expirarão após o intervalo de “n”.</span><span class="sxs-lookup"><span data-stu-id="db7ed-142">All other documents will expire after "n" interval.</span></span> |
| <span data-ttu-id="db7ed-143">TTL = n no documento</span><span class="sxs-lookup"><span data-stu-id="db7ed-143">TTL = n on document</span></span> |<span data-ttu-id="db7ed-144">Nada toooverride no nível do documento hello.</span><span class="sxs-lookup"><span data-stu-id="db7ed-144">Nothing toooverride at hello document level.</span></span> <span data-ttu-id="db7ed-145">TTL em um documento não interpretada pelo sistema hello.</span><span class="sxs-lookup"><span data-stu-id="db7ed-145">TTL on a document in un-interpreted by hello system.</span></span> |<span data-ttu-id="db7ed-146">documento de saudação com TTL = n expirará após n de intervalo, em segundos.</span><span class="sxs-lookup"><span data-stu-id="db7ed-146">hello document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="db7ed-147">Os outros documentos herdarão o intervalo de -1 e nunca expirarão.</span><span class="sxs-lookup"><span data-stu-id="db7ed-147">Other documents will inherit interval of -1 and never expire.</span></span> |<span data-ttu-id="db7ed-148">documento de saudação com TTL = n expirará após n de intervalo, em segundos.</span><span class="sxs-lookup"><span data-stu-id="db7ed-148">hello document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="db7ed-149">Outros documentos herdará o intervalo de "n" da coleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="db7ed-149">Other documents will inherit "n" interval from hello collection.</span></span> |

## <a name="configuring-ttl"></a><span data-ttu-id="db7ed-150">Configurando a TTL</span><span class="sxs-lookup"><span data-stu-id="db7ed-150">Configuring TTL</span></span>
<span data-ttu-id="db7ed-151">Por padrão, o tempo toolive é desabilitado por padrão em todas as coleções de banco de dados do Cosmos e em todos os documentos.</span><span class="sxs-lookup"><span data-stu-id="db7ed-151">By default, time toolive is disabled by default in all Cosmos DB collections and on all documents.</span></span>

## <a name="enabling-ttl"></a><span data-ttu-id="db7ed-152">Habilitando a TTL</span><span class="sxs-lookup"><span data-stu-id="db7ed-152">Enabling TTL</span></span>
<span data-ttu-id="db7ed-153">tooenable TTL em uma coleção ou documentos hello dentro de uma coleção, você precisa de propriedade de DefaultTTL Olá tooset de uma coleção de tooeither -1 ou um número positivo diferente de zero.</span><span class="sxs-lookup"><span data-stu-id="db7ed-153">tooenable TTL on a collection, or hello documents within a collection, you need tooset hello DefaultTTL property of a collection tooeither -1 or a non-zero positive number.</span></span> <span data-ttu-id="db7ed-154">A configuração Olá DefaultTTL muito-1 significa que por padrão todos os documentos na coleção de saudação operará sempre mas Olá serviço Cosmos DB deve monitorar essa coleção para documentos que tenham substituído esse padrão.</span><span class="sxs-lookup"><span data-stu-id="db7ed-154">Setting hello DefaultTTL too-1 means that by default all documents in hello collection will live forever but hello Cosmos DB service should monitor this collection for documents that have overridden this default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a><span data-ttu-id="db7ed-155">Configurando a TTL padrão em uma coleção</span><span class="sxs-lookup"><span data-stu-id="db7ed-155">Configuring default TTL on a collection</span></span>
<span data-ttu-id="db7ed-156">Você está tooconfigure capaz de um tempo padrão toolive em um nível de coleção.</span><span class="sxs-lookup"><span data-stu-id="db7ed-156">You are able tooconfigure a default time toolive at a collection level.</span></span> <span data-ttu-id="db7ed-157">Olá tooset TTL em uma coleção, você precisa tooprovide um número positivo diferente de zero que indica o período de hello, em segundos, tooexpire todos os documentos na coleção de saudação depois Olá modificado pela última vez timestamp do documento hello (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="db7ed-157">tooset hello TTL on a collection, you need tooprovide a non-zero positive number that indicates hello period, in seconds, tooexpire all documents in hello collection after hello last modified timestamp of hello document (`_ts`).</span></span> <span data-ttu-id="db7ed-158">Ou, você pode definir o saudação padrão muito-1, o que significa que todos os documentos inseridos na coleção toohello operará indefinidamente por padrão.</span><span class="sxs-lookup"><span data-stu-id="db7ed-158">Or, you can set hello default too-1, which implies that all documents inserted in toohello collection will live indefinitely by default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a><span data-ttu-id="db7ed-159">Configurando a TTL em um documento</span><span class="sxs-lookup"><span data-stu-id="db7ed-159">Setting TTL on a document</span></span>
<span data-ttu-id="db7ed-160">Além disso toosetting um TTL padrão em uma coleção você pode definir o TTL específico em um nível de documento.</span><span class="sxs-lookup"><span data-stu-id="db7ed-160">In addition toosetting a default TTL on a collection you can set specific TTL at a document level.</span></span> <span data-ttu-id="db7ed-161">Isso substituirá o padrão de saudação da coleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="db7ed-161">Doing this will override hello default of hello collection.</span></span>

* <span data-ttu-id="db7ed-162">Olá tooset TTL em um documento, você precisa tooprovide Olá a um número positivo diferente de zero, que indica o período, em segundos, o documento de saudação tooexpire depois Olá modificado pela última vez timestamp do documento hello (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="db7ed-162">tooset hello TTL on a document, you need tooprovide a non-zero positive number which indicates hello period, in seconds, tooexpire hello document after hello last modified timestamp of hello document (`_ts`).</span></span>
* <span data-ttu-id="db7ed-163">Se um documento não tem nenhum campo TTL, Olá, em seguida, o padrão de coleção de saudação será aplicada.</span><span class="sxs-lookup"><span data-stu-id="db7ed-163">If a document has no TTL field, then hello default of hello collection will apply.</span></span>
* <span data-ttu-id="db7ed-164">Se o TTL for desabilitado no nível de coleção hello, campo TTL Olá no documento hello será ignorado até que o TTL seja habilitada novamente na coleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="db7ed-164">If TTL is disabled at hello collection level, hello TTL field on hello document will be ignored until TTL is enabled again on hello collection.</span></span>

<span data-ttu-id="db7ed-165">Aqui está um trecho de código mostrando como tooset Olá expiração do TTL em um documento:</span><span class="sxs-lookup"><span data-stu-id="db7ed-165">Here's a snippet showing how tooset hello TTL expiration on a document:</span></span>

    // Include a property that serializes too"ttl" in JSON
    public class SalesOrder
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        
        [JsonProperty(PropertyName="cid")]
        public string CustomerId { get; set; }
        
        // used tooset expiration policy
        [JsonProperty(PropertyName = "ttl", NullValueHandling = NullValueHandling.Ignore)]
        public int? TimeToLive { get; set; }
        
        //...
    }
    
    // Set hello value toohello expiration in seconds
    SalesOrder salesOrder = new SalesOrder
    {
        Id = "SO05",
        CustomerId = "CO18009186470",
        TimeToLive = 60 * 60 * 24 * 30;  // Expire sales orders in 30 days 
    };


## <a name="extending-ttl-on-an-existing-document"></a><span data-ttu-id="db7ed-166">Estendendo a TTL em um documento existente</span><span class="sxs-lookup"><span data-stu-id="db7ed-166">Extending TTL on an existing document</span></span>
<span data-ttu-id="db7ed-167">Você pode redefinir Olá TTL em um documento, fazendo a qualquer operação de gravação no documento de saudação.</span><span class="sxs-lookup"><span data-stu-id="db7ed-167">You can reset hello TTL on a document by doing any write operation on hello document.</span></span> <span data-ttu-id="db7ed-168">Isso definirá Olá `_ts` toohello hora atual e Olá contagem regressiva toohello documento expiração, conforme definido pela Olá `ttl`, começará novamente.</span><span class="sxs-lookup"><span data-stu-id="db7ed-168">Doing this will set hello `_ts` toohello current time, and hello countdown toohello document expiry, as set by hello `ttl`, will begin again.</span></span> <span data-ttu-id="db7ed-169">Se você quiser Olá toochange `ttl` de um documento, você pode atualizar o campo de saudação como você pode fazer com que qualquer outro campo configurável.</span><span class="sxs-lookup"><span data-stu-id="db7ed-169">If you wish toochange hello `ttl` of a document, you can update hello field as you can do with any other settable field.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time toolive
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a><span data-ttu-id="db7ed-170">Removendo a TTL de um documento</span><span class="sxs-lookup"><span data-stu-id="db7ed-170">Removing TTL from a document</span></span>
<span data-ttu-id="db7ed-171">Se um TTL tiver sido definido em um documento e você não deseja mais que tooexpire de documento, você pode recuperar documento hello, remover o campo TTL hello e substituir Olá documento no servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="db7ed-171">If a TTL has been set on a document and you no longer want that document tooexpire, then you can retrieve hello document, remove hello TTL field and replace hello document on hello server.</span></span> <span data-ttu-id="db7ed-172">Quando o campo TTL Olá é removido do documento hello, Olá padrão da coleção de saudação será aplicado.</span><span class="sxs-lookup"><span data-stu-id="db7ed-172">When hello TTL field is removed from hello document, hello default of hello collection will be applied.</span></span> <span data-ttu-id="db7ed-173">toostop um documento de expiração e não herda da coleção hello, em seguida, você precisa tooset Olá TTL valor muito-1.</span><span class="sxs-lookup"><span data-stu-id="db7ed-173">toostop a document from expiring and not inherit from hello collection then you need tooset hello TTL value too-1.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit hello default TTL of hello collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a><span data-ttu-id="db7ed-174">Desabilitando a TTL</span><span class="sxs-lookup"><span data-stu-id="db7ed-174">Disabling TTL</span></span>
<span data-ttu-id="db7ed-175">toodisable TTL inteiramente em uma coleção e o plano de fundo de saudação parar processo de procurar documentos expirados Olá DefaultTTL na coleção de saudação deve ser excluído.</span><span class="sxs-lookup"><span data-stu-id="db7ed-175">toodisable TTL entirely on a collection and stop hello background process from looking for expired documents hello DefaultTTL property on hello collection should be deleted.</span></span> <span data-ttu-id="db7ed-176">A exclusão desta propriedade é diferente da definição de muito-1.</span><span class="sxs-lookup"><span data-stu-id="db7ed-176">Deleting this property is different from setting it too-1.</span></span> <span data-ttu-id="db7ed-177">A configuração de muito-1 significa novos documentos adicionado toohello coleção operará para sempre, mas você pode substituí-lo em documentos específicos na coleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="db7ed-177">Setting too-1 means new documents added toohello collection will live forever but you can override this on specific documents in hello collection.</span></span> <span data-ttu-id="db7ed-178">Remover essa propriedade inteiramente de coleção de saudação significa que documentos não vai expirar, mesmo se houver documentos que tenham substituído explicitamente o padrão anterior.</span><span class="sxs-lookup"><span data-stu-id="db7ed-178">Removing this property entirely from hello collection means that no documents will expire, even if there are documents that have explicitly overridden a previous default.</span></span>

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a><span data-ttu-id="db7ed-179">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="db7ed-179">FAQ</span></span>
<span data-ttu-id="db7ed-180">**Qual o preço da TTL?**</span><span class="sxs-lookup"><span data-stu-id="db7ed-180">**What will TTL cost me?**</span></span>

<span data-ttu-id="db7ed-181">Não há nenhum custo adicional de toosetting TTL em um documento.</span><span class="sxs-lookup"><span data-stu-id="db7ed-181">There is no additional cost toosetting a TTL on a document.</span></span>

<span data-ttu-id="db7ed-182">**Quanto tempo levará toodelete documento depois Olá TTL está ativo?**</span><span class="sxs-lookup"><span data-stu-id="db7ed-182">**How long will it take toodelete my document once hello TTL is up?**</span></span>

<span data-ttu-id="db7ed-183">documentos de saudação expirados imediatamente depois de saudação TTL está ativo e não poderão ser acessada por meio de CRUD ou APIs de consulta.</span><span class="sxs-lookup"><span data-stu-id="db7ed-183">hello documents are expired immediately once hello TTL is up, and will not be accessible via CRUD or query APIs.</span></span> 

<span data-ttu-id="db7ed-184">**A TTL em um documento terá algum impacto sobre os encargos de RU?**</span><span class="sxs-lookup"><span data-stu-id="db7ed-184">**Will TTL on a document have any impact on RU charges?**</span></span>

<span data-ttu-id="db7ed-185">Não haverá nenhum impacto nos encargos de RU para as exclusões de documentos expirados por meio da TTL no Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="db7ed-185">No, there will be no impact on RU charges for deletions of expired documents via TTL in Cosmos DB.</span></span>

<span data-ttu-id="db7ed-186">**Recurso TTL Olá apenas aplica tooentire documentos ou podem expirar valores de propriedade de documento individuais?**</span><span class="sxs-lookup"><span data-stu-id="db7ed-186">**Does hello TTL feature only apply tooentire documents, or can I expire individual document property values?**</span></span>

<span data-ttu-id="db7ed-187">TTL se aplica a todo o documento toohello.</span><span class="sxs-lookup"><span data-stu-id="db7ed-187">TTL applies toohello entire document.</span></span> <span data-ttu-id="db7ed-188">Se você gostaria que tooexpire apenas uma parte de um documento, ele é recomendável que você extrair parte de saudação do documento principal de saudação tooa documento separado de "vinculado" e, em seguida, use o TTL nesse documento extraída.</span><span class="sxs-lookup"><span data-stu-id="db7ed-188">If you would like tooexpire just a portion of a document, then it is recommended that you extract hello portion from hello main document in tooa separate "linked” document and then use TTL on that extracted document.</span></span>

<span data-ttu-id="db7ed-189">**Recurso TTL Olá tem os requisitos específicos de indexação?**</span><span class="sxs-lookup"><span data-stu-id="db7ed-189">**Does hello TTL feature have any specific indexing requirements?**</span></span>

<span data-ttu-id="db7ed-190">Sim.</span><span class="sxs-lookup"><span data-stu-id="db7ed-190">Yes.</span></span> <span data-ttu-id="db7ed-191">Olá coleção deve ter [conjunto de política de indexação](indexing-policies.md) tooeither consistente ou Lazy.</span><span class="sxs-lookup"><span data-stu-id="db7ed-191">hello collection must have [indexing policy set](indexing-policies.md) tooeither Consistent or Lazy.</span></span> <span data-ttu-id="db7ed-192">Tentar tooset DefaultTTL em uma coleção com indexação conjunto tooNone resultará em um erro, assim como tooturn tentar desativar a indexação em uma coleção que tem um DefaultTTL já definido.</span><span class="sxs-lookup"><span data-stu-id="db7ed-192">Trying tooset DefaultTTL on a collection with indexing set tooNone will result in an error, as will trying tooturn off indexing on a collection that has a DefaultTTL already set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db7ed-193">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="db7ed-193">Next steps</span></span>
<span data-ttu-id="db7ed-194">toolearn mais sobre Azure Cosmos DB, consulte serviço toohello [ *documentação* ](https://azure.microsoft.com/documentation/services/cosmos-db/) página.</span><span class="sxs-lookup"><span data-stu-id="db7ed-194">toolearn more about Azure Cosmos DB, refer toohello service [*documentation*](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span>

