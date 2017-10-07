---
title: AAA "carregar dados (.NET - pesquisa do Azure) | Microsoft Docs"
description: "Saiba como o índice de tooan tooupload dados na pesquisa do Azure usando Olá .NET SDK."
services: search
documentationcenter: 
author: brjohnstmsft
manager: jhubbard
editor: 
tags: 
ms.assetid: 0e0e7e7b-7178-4c26-95c6-2fd1e8015aca
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/13/2017
ms.author: brjohnst
ms.openlocfilehash: 78ddbefb522884d1f61cb275c25c091487aee639
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search-using-hello-net-sdk"></a><span data-ttu-id="c2686-103">Carregar dados tooAzure pesquisa usando Olá SDK .NET</span><span class="sxs-lookup"><span data-stu-id="c2686-103">Upload data tooAzure Search using hello .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c2686-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="c2686-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="c2686-105">.NET</span><span class="sxs-lookup"><span data-stu-id="c2686-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="c2686-106">REST</span><span class="sxs-lookup"><span data-stu-id="c2686-106">REST</span></span>](search-import-data-rest-api.md)
> 
> 

<span data-ttu-id="c2686-107">Este artigo mostra como Olá toouse [SDK .NET da pesquisa do Azure](https://aka.ms/search-sdk) tooimport dados em um índice de pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="c2686-107">This article will show you how toouse hello [Azure Search .NET SDK](https://aka.ms/search-sdk) tooimport data into an Azure Search index.</span></span>

<span data-ttu-id="c2686-108">Antes de começar este passo a passo, você já deve ter [criado um índice de Pesquisa do Azure](search-what-is-an-index.md).</span><span class="sxs-lookup"><span data-stu-id="c2686-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span> <span data-ttu-id="c2686-109">Este artigo também pressupõe que você já tenha criado um `SearchServiceClient` do objeto, como mostrado na [criar um índice de pesquisa do Azure usando o SDK .NET de saudação](search-create-index-dotnet.md#CreateSearchServiceClient).</span><span class="sxs-lookup"><span data-stu-id="c2686-109">This article also assumes that you have already created a `SearchServiceClient` object, as shown in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md#CreateSearchServiceClient).</span></span>

> [!NOTE]
> <span data-ttu-id="c2686-110">Todos os códigos de exemplo neste artigo foram escritos em C#.</span><span class="sxs-lookup"><span data-stu-id="c2686-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="c2686-111">Você pode encontrar o código-fonte completo Olá [no GitHub](http://aka.ms/search-dotnet-howto).</span><span class="sxs-lookup"><span data-stu-id="c2686-111">You can find hello full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="c2686-112">Você também pode ler sobre Olá [SDK .NET da pesquisa do Azure](search-howto-dotnet-sdk.md) para um mais detalhado passo a passo do código de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="c2686-112">You can also read about hello [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of hello sample code.</span></span>

<span data-ttu-id="c2686-113">Em documentos de toopush ordem pra o índice usando Olá .NET SDK, você precisará:</span><span class="sxs-lookup"><span data-stu-id="c2686-113">In order toopush documents into your index using hello .NET SDK, you will need to:</span></span>

1. <span data-ttu-id="c2686-114">Criar um `SearchIndexClient` objeto tooconnect tooyour índice de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="c2686-114">Create a `SearchIndexClient` object tooconnect tooyour search index.</span></span>
2. <span data-ttu-id="c2686-115">Criar um `IndexBatch` contendo Olá documentos toobe adicionada, modificada ou excluída.</span><span class="sxs-lookup"><span data-stu-id="c2686-115">Create an `IndexBatch` containing hello documents toobe added, modified, or deleted.</span></span>
3. <span data-ttu-id="c2686-116">Chamar hello `Documents.Index` método de sua `SearchIndexClient` toosend Olá `IndexBatch` tooyour índice de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="c2686-116">Call hello `Documents.Index` method of your `SearchIndexClient` toosend hello `IndexBatch` tooyour search index.</span></span>

## <a name="create-an-instance-of-hello-searchindexclient-class"></a><span data-ttu-id="c2686-117">Crie uma instância da classe SearchIndexClient de saudação</span><span class="sxs-lookup"><span data-stu-id="c2686-117">Create an instance of hello SearchIndexClient class</span></span>
<span data-ttu-id="c2686-118">tooimport dados usando seu índice Olá SDK .NET da pesquisa do Azure, você precisará toocreate uma instância do hello `SearchIndexClient` classe.</span><span class="sxs-lookup"><span data-stu-id="c2686-118">tooimport data into your index using hello Azure Search .NET SDK, you will need toocreate an instance of hello `SearchIndexClient` class.</span></span> <span data-ttu-id="c2686-119">Você pode construir essa instância por conta própria, mas é mais fácil se você já tiver um `SearchServiceClient` toocall instância seu `Indexes.GetClient` método.</span><span class="sxs-lookup"><span data-stu-id="c2686-119">You can construct this instance yourself, but it's easier if you already have a `SearchServiceClient` instance toocall its `Indexes.GetClient` method.</span></span> <span data-ttu-id="c2686-120">Por exemplo, aqui está como você poderia obter um `SearchIndexClient` índice Olá denominado "hotéis" de um `SearchServiceClient` chamado `serviceClient`:</span><span class="sxs-lookup"><span data-stu-id="c2686-120">For example, here is how you would obtain a `SearchIndexClient` for hello index named "hotels" from a `SearchServiceClient` named `serviceClient`:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="c2686-121">Em um aplicativo típico de pesquisa, o gerenciamento e o preenchimento do índice é tratado por um componente separado das consultas de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="c2686-121">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="c2686-122">`Indexes.GetClient`é conveniente para preencher um índice porque poupa Olá problemas de fornecer outra `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="c2686-122">`Indexes.GetClient` is convenient for populating an index because it saves you hello trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="c2686-123">Ele faz isso passando a chave de administração Olá Olá de toocreate usadas que você `SearchServiceClient` toohello novo `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="c2686-123">It does this by passing hello admin key that you used toocreate hello `SearchServiceClient` toohello new `SearchIndexClient`.</span></span> <span data-ttu-id="c2686-124">No entanto, em parte de saudação do aplicativo que executa consultas, é melhor Olá de toocreate `SearchIndexClient` diretamente para que você pode passar de uma chave de consulta em vez de uma chave de administração.</span><span class="sxs-lookup"><span data-stu-id="c2686-124">However, in hello part of your application that executes queries, it is better toocreate hello `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="c2686-125">Isso é consistente com hello [princípio de menos privilégios](https://en.wikipedia.org/wiki/Principle_of_least_privilege) e ajudará toomake seu aplicativo mais seguro.</span><span class="sxs-lookup"><span data-stu-id="c2686-125">This is consistent with hello [principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege) and will help toomake your application more secure.</span></span> <span data-ttu-id="c2686-126">Você pode encontrar mais informações sobre chaves de administração e as chaves de consulta Olá [referência da API de REST de pesquisa do Azure](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="c2686-126">You can find out more about admin keys and query keys in hello [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
> 
> 

<span data-ttu-id="c2686-127">`SearchIndexClient` tem uma propriedade `Documents`.</span><span class="sxs-lookup"><span data-stu-id="c2686-127">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="c2686-128">Esta propriedade fornece todos os métodos de saudação tooadd, você precisa modificar, excluir ou consultar documentos no índice.</span><span class="sxs-lookup"><span data-stu-id="c2686-128">This property provides all hello methods you need tooadd, modify, delete, or query documents in your index.</span></span>

## <a name="decide-which-indexing-action-toouse"></a><span data-ttu-id="c2686-129">Decidir quais indexação toouse de ação</span><span class="sxs-lookup"><span data-stu-id="c2686-129">Decide which indexing action toouse</span></span>
<span data-ttu-id="c2686-130">dados tooimport usando Olá .NET SDK, você precisará toopackage backup de seus dados em um `IndexBatch` objeto.</span><span class="sxs-lookup"><span data-stu-id="c2686-130">tooimport data using hello .NET SDK, you will need toopackage up your data into an `IndexBatch` object.</span></span> <span data-ttu-id="c2686-131">Um `IndexBatch` encapsula uma coleção de `IndexAction` objetos, cada qual contendo um documento e uma propriedade que indica a pesquisa do Azure que tooperform ação nesse documento (carregar, mesclar, excluir, etc.).</span><span class="sxs-lookup"><span data-stu-id="c2686-131">An `IndexBatch` encapsulates a collection of `IndexAction` objects, each of which contains a document and a property that tells Azure Search what action tooperform on that document (upload, merge, delete, etc).</span></span> <span data-ttu-id="c2686-132">Dependendo de qual dos Olá ações que você escolher abaixo, somente determinados campos devem ser incluídos para cada documento:</span><span class="sxs-lookup"><span data-stu-id="c2686-132">Depending on which of hello below actions you choose, only certain fields must be included for each document:</span></span>

| <span data-ttu-id="c2686-133">Ação</span><span class="sxs-lookup"><span data-stu-id="c2686-133">Action</span></span> | <span data-ttu-id="c2686-134">Descrição</span><span class="sxs-lookup"><span data-stu-id="c2686-134">Description</span></span> | <span data-ttu-id="c2686-135">Campos necessários para cada documento</span><span class="sxs-lookup"><span data-stu-id="c2686-135">Necessary fields for each document</span></span> | <span data-ttu-id="c2686-136">Observações</span><span class="sxs-lookup"><span data-stu-id="c2686-136">Notes</span></span> |
| --- | --- | --- | --- |
| `Upload` |<span data-ttu-id="c2686-137">Um `Upload` ação é similar tooan "upsert" onde documento hello será inserido se for novo e atualizado/substituído se ele existir.</span><span class="sxs-lookup"><span data-stu-id="c2686-137">An `Upload` action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="c2686-138">chave, além de quaisquer outros campos que você deseja toodefine</span><span class="sxs-lookup"><span data-stu-id="c2686-138">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="c2686-139">Ao atualizar/substituir um documento existente, qualquer campo que não está especificado na solicitação de saudação terá seu campo definido muito`null`.</span><span class="sxs-lookup"><span data-stu-id="c2686-139">When updating/replacing an existing document, any field that is not specified in hello request will have its field set too`null`.</span></span> <span data-ttu-id="c2686-140">Isso ocorre mesmo quando o campo Olá tiver sido definido anteriormente tooa valor de não-nulo.</span><span class="sxs-lookup"><span data-stu-id="c2686-140">This occurs even when hello field was previously set tooa non-null value.</span></span> |
| `Merge` |<span data-ttu-id="c2686-141">Atualizações de uma existente de documento com hello especificado campos.</span><span class="sxs-lookup"><span data-stu-id="c2686-141">Updates an existing document with hello specified fields.</span></span> <span data-ttu-id="c2686-142">Se o documento de saudação não existe no índice hello, mesclagem Olá falhará.</span><span class="sxs-lookup"><span data-stu-id="c2686-142">If hello document does not exist in hello index, hello merge will fail.</span></span> |<span data-ttu-id="c2686-143">chave, além de quaisquer outros campos que você deseja toodefine</span><span class="sxs-lookup"><span data-stu-id="c2686-143">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="c2686-144">Qualquer campo que você especificar em uma mesclagem substituirá o campo de saudação existente no documento de saudação.</span><span class="sxs-lookup"><span data-stu-id="c2686-144">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="c2686-145">Isso inclui campos do tipo `DataType.Collection(DataType.String)`.</span><span class="sxs-lookup"><span data-stu-id="c2686-145">This includes fields of type `DataType.Collection(DataType.String)`.</span></span> <span data-ttu-id="c2686-146">Por exemplo, se hello documento contém um campo `tags` com valor `["budget"]` e executar uma mesclagem com valor `["economy", "pool"]` para `tags`, Olá valor final do hello `tags` campo será `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="c2686-146">For example, if hello document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, hello final value of hello `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="c2686-147">Ele não será `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="c2686-147">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `MergeOrUpload` |<span data-ttu-id="c2686-148">Esta ação se comporta como `Merge` se um documento com hello atribuída a chave já existe no índice hello.</span><span class="sxs-lookup"><span data-stu-id="c2686-148">This action behaves like `Merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="c2686-149">Se o documento de saudação não existir, ele se comporta como `Upload` com um novo documento.</span><span class="sxs-lookup"><span data-stu-id="c2686-149">If hello document does not exist, it behaves like `Upload` with a new document.</span></span> |<span data-ttu-id="c2686-150">chave, além de quaisquer outros campos que você deseja toodefine</span><span class="sxs-lookup"><span data-stu-id="c2686-150">key, plus any other fields you wish toodefine</span></span> |- |
| `Delete` |<span data-ttu-id="c2686-151">Remove o documento especificado Olá do índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="c2686-151">Removes hello specified document from hello index.</span></span> |<span data-ttu-id="c2686-152">somente chave</span><span class="sxs-lookup"><span data-stu-id="c2686-152">key only</span></span> |<span data-ttu-id="c2686-153">Todos os campos que você especificar que o campo de chave hello será ignorado.</span><span class="sxs-lookup"><span data-stu-id="c2686-153">Any fields you specify other than hello key field will be ignored.</span></span> <span data-ttu-id="c2686-154">Se você quiser tooremove um campo individual de um documento, use `Merge` em vez disso e basta definir campo Olá explicitamente toonull.</span><span class="sxs-lookup"><span data-stu-id="c2686-154">If you want tooremove an individual field from a document, use `Merge` instead and simply set hello field explicitly toonull.</span></span> |

<span data-ttu-id="c2686-155">Você pode especificar a ação que você deseja toouse com hello vários métodos estáticos da saudação `IndexBatch` e `IndexAction` classes, conforme mostrado na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="c2686-155">You can specify what action you want toouse with hello various static methods of hello `IndexBatch` and `IndexAction` classes, as shown in hello next section.</span></span>

## <a name="construct-your-indexbatch"></a><span data-ttu-id="c2686-156">Construa seu IndexBatch</span><span class="sxs-lookup"><span data-stu-id="c2686-156">Construct your IndexBatch</span></span>
<span data-ttu-id="c2686-157">Agora que você sabe quais ações tooperform em seus documentos, você está pronto tooconstruct Olá `IndexBatch`.</span><span class="sxs-lookup"><span data-stu-id="c2686-157">Now that you know which actions tooperform on your documents, you are ready tooconstruct hello `IndexBatch`.</span></span> <span data-ttu-id="c2686-158">Olá o exemplo a seguir mostra como toocreate um lote com algumas ações diferentes.</span><span class="sxs-lookup"><span data-stu-id="c2686-158">hello example below shows how toocreate a batch with a few different actions.</span></span> <span data-ttu-id="c2686-159">Observe que o nosso exemplo usa uma classe personalizada chamada `Hotel` que mapeia tooa documento no índice de "hotéis" hello.</span><span class="sxs-lookup"><span data-stu-id="c2686-159">Note that our example uses a custom class called `Hotel` that maps tooa document in hello "hotels" index.</span></span>

```csharp
var actions =
    new IndexAction<Hotel>[]
    {
        IndexAction.Upload(
            new Hotel()
            {
                HotelId = "1",
                BaseRate = 199.0,
                Description = "Best hotel in town",
                DescriptionFr = "Meilleur hôtel en ville",
                HotelName = "Fancy Stay",
                Category = "Luxury",
                Tags = new[] { "pool", "view", "wifi", "concierge" },
                ParkingIncluded = false,
                SmokingAllowed = false,
                LastRenovationDate = new DateTimeOffset(2010, 6, 27, 0, 0, 0, TimeSpan.Zero),
                Rating = 5,
                Location = GeographyPoint.Create(47.678581, -122.131577)
            }),
        IndexAction.Upload(
            new Hotel()
            {
                HotelId = "2",
                BaseRate = 79.99,
                Description = "Cheapest hotel in town",
                DescriptionFr = "Hôtel le moins cher en ville",
                HotelName = "Roach Motel",
                Category = "Budget",
                Tags = new[] { "motel", "budget" },
                ParkingIncluded = true,
                SmokingAllowed = true,
                LastRenovationDate = new DateTimeOffset(1982, 4, 28, 0, 0, 0, TimeSpan.Zero),
                Rating = 1,
                Location = GeographyPoint.Create(49.678581, -122.131577)
            }),
        IndexAction.MergeOrUpload(
            new Hotel()
            {
                HotelId = "3",
                BaseRate = 129.99,
                Description = "Close tootown hall and hello river"
            }),
        IndexAction.Delete(new Hotel() { HotelId = "6" })
    };

var batch = IndexBatch.New(actions);
```

<span data-ttu-id="c2686-160">Nesse caso, estamos usando `Upload`, `MergeOrUpload`, e `Delete` como nossas ações de pesquisa, conforme especificado por métodos Olá chamados hello `IndexAction` classe.</span><span class="sxs-lookup"><span data-stu-id="c2686-160">In this case, we are using `Upload`, `MergeOrUpload`, and `Delete` as our search actions, as specified by hello methods called on hello `IndexAction` class.</span></span>

<span data-ttu-id="c2686-161">Suponha que o índice de exemplo "hotels" já esteja preenchido com vários documentos.</span><span class="sxs-lookup"><span data-stu-id="c2686-161">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="c2686-162">Observe como não tínhamos toospecify todos os campos de documento possíveis Olá ao usar `MergeOrUpload` e como podemos só especificado de chave de documento hello (`HotelId`) ao usar `Delete`.</span><span class="sxs-lookup"><span data-stu-id="c2686-162">Note how we did not have toospecify all hello possible document fields when using `MergeOrUpload` and how we only specified hello document key (`HotelId`) when using `Delete`.</span></span>

<span data-ttu-id="c2686-163">Além disso, observe que você só pode incluir documentos too1000 em uma única solicitação de indexação.</span><span class="sxs-lookup"><span data-stu-id="c2686-163">Also, note that you can only include up too1000 documents in a single indexing request.</span></span>

> [!NOTE]
> <span data-ttu-id="c2686-164">Neste exemplo, estamos aplicando documentos de toodifferent ações diferentes.</span><span class="sxs-lookup"><span data-stu-id="c2686-164">In this example, we are applying different actions toodifferent documents.</span></span> <span data-ttu-id="c2686-165">Se você quisesse tooperform Olá ações mesmo em todos os documentos em lote hello, em vez de chamar `IndexBatch.New`, você pode usar Olá outros métodos estáticos de `IndexBatch`.</span><span class="sxs-lookup"><span data-stu-id="c2686-165">If you wanted tooperform hello same actions across all documents in hello batch, instead of calling `IndexBatch.New`, you could use hello other static methods of `IndexBatch`.</span></span> <span data-ttu-id="c2686-166">Por exemplo, você poderia criar lotes chamando `IndexBatch.Merge`, `IndexBatch.MergeOrUpload` ou `IndexBatch.Delete`.</span><span class="sxs-lookup"><span data-stu-id="c2686-166">For example, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete`.</span></span> <span data-ttu-id="c2686-167">Esses métodos usam um conjunto de documentos (objetos do tipo `Hotel` neste exemplo) em vez de objetos `IndexAction`.</span><span class="sxs-lookup"><span data-stu-id="c2686-167">These methods take a collection of documents (objects of type `Hotel` in this example) instead of `IndexAction` objects.</span></span>
> 
> 

## <a name="import-data-toohello-index"></a><span data-ttu-id="c2686-168">Índice de toohello de dados de importação</span><span class="sxs-lookup"><span data-stu-id="c2686-168">Import data toohello index</span></span>
<span data-ttu-id="c2686-169">Agora que você tem uma inicializado `IndexBatch` do objeto, você pode enviá-lo toohello índice chamando `Documents.Index` em seu `SearchIndexClient` objeto.</span><span class="sxs-lookup"><span data-stu-id="c2686-169">Now that you have an initialized `IndexBatch` object, you can send it toohello index by calling `Documents.Index` on your `SearchIndexClient` object.</span></span> <span data-ttu-id="c2686-170">Olá mostrado no exemplo a seguir como toocall `Index`, bem como algumas etapas adicionais que você precisará tooperform:</span><span class="sxs-lookup"><span data-stu-id="c2686-170">hello following example shows how toocall `Index`, as well as some extra steps you will need tooperform:</span></span>

```csharp
try
{
    indexClient.Documents.Index(batch);
}
catch (IndexBatchException e)
{
    // Sometimes when your Search service is under load, indexing will fail for some of hello documents in
    // hello batch. Depending on your application, you can take compensating actions like delaying and
    // retrying. For this simple demo, we just log hello failed document keys and continue.
    Console.WriteLine(
        "Failed tooindex some of hello documents: {0}",
        String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
}

Console.WriteLine("Waiting for documents toobe indexed...\n");
Thread.Sleep(2000);
```

<span data-ttu-id="c2686-171">Saudação de Observação `try` / `catch` ao redor Olá chamada toohello `Index` método.</span><span class="sxs-lookup"><span data-stu-id="c2686-171">Note hello `try`/`catch` surrounding hello call toohello `Index` method.</span></span> <span data-ttu-id="c2686-172">bloco catch de saudação trata um caso de erro importante para indexação.</span><span class="sxs-lookup"><span data-stu-id="c2686-172">hello catch block handles an important error case for indexing.</span></span> <span data-ttu-id="c2686-173">Se o serviço de pesquisa do Azure falhar tooindex alguns Olá documentos em lote hello, um `IndexBatchException` é gerada pelo `Documents.Index`.</span><span class="sxs-lookup"><span data-stu-id="c2686-173">If your Azure Search service fails tooindex some of hello documents in hello batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="c2686-174">Isso pode acontecer se você estiver indexando documentos enquanto o serviço estiver sob carga pesada.</span><span class="sxs-lookup"><span data-stu-id="c2686-174">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="c2686-175">**É altamente recomendável a manipulação explícita desse caso em seu código.**</span><span class="sxs-lookup"><span data-stu-id="c2686-175">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="c2686-176">Você pode atrasar e repita indexação documentos Olá que falhou, ou faça e continuar como não do exemplo hello, ou você pode fazer algo diferente, dependendo dos requisitos de consistência de dados do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c2686-176">You can delay and then retry indexing hello documents that failed, or you can log and continue like hello sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

<span data-ttu-id="c2686-177">Por fim, Olá código exemplo hello acima atrasos por dois segundos.</span><span class="sxs-lookup"><span data-stu-id="c2686-177">Finally, hello code in hello example above delays for two seconds.</span></span> <span data-ttu-id="c2686-178">A indexação ocorre assincronamente no serviço de pesquisa do Azure, para que o aplicativo de exemplo hello precisa toowait um tooensure curto período de tempo que os documentos de saudação estão disponíveis para pesquisa.</span><span class="sxs-lookup"><span data-stu-id="c2686-178">Indexing happens asynchronously in your Azure Search service, so hello sample application needs toowait a short time tooensure that hello documents are available for searching.</span></span> <span data-ttu-id="c2686-179">Normalmente, atrasos como esses só são necessários em demonstrações, testes e exemplos de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="c2686-179">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

<a name="HotelClass"></a>

### <a name="how-hello-net-sdk-handles-documents"></a><span data-ttu-id="c2686-180">Olá como documentos de identificadores do SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="c2686-180">How hello .NET SDK handles documents</span></span>
<span data-ttu-id="c2686-181">Você deve estar se perguntando como Olá SDK .NET da pesquisa do Azure é instâncias tooupload capaz de uma classe definida pelo usuário como `Hotel` toohello índice.</span><span class="sxs-lookup"><span data-stu-id="c2686-181">You may be wondering how hello Azure Search .NET SDK is able tooupload instances of a user-defined class like `Hotel` toohello index.</span></span> <span data-ttu-id="c2686-182">toohelp responder essa pergunta, vamos examinar a saudação `Hotel` classe, que mapeia o esquema de índice toohello definido em [criar um índice de pesquisa do Azure usando o SDK .NET de saudação](search-create-index-dotnet.md#DefineIndex):</span><span class="sxs-lookup"><span data-stu-id="c2686-182">toohelp answer that question, let's look at hello `Hotel` class, which maps toohello index schema defined in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md#DefineIndex):</span></span>

```csharp
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [Key]
    [IsFilterable]
    public string HotelId { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public double? BaseRate { get; set; }

    [IsSearchable]
    public string Description { get; set; }

    [IsSearchable]
    [Analyzer(AnalyzerName.AsString.FrLucene)]
    [JsonProperty("description_fr")]
    public string DescriptionFr { get; set; }

    [IsSearchable, IsFilterable, IsSortable]
    public string HotelName { get; set; }

    [IsSearchable, IsFilterable, IsSortable, IsFacetable]
    public string Category { get; set; }

    [IsSearchable, IsFilterable, IsFacetable]
    public string[] Tags { get; set; }

    [IsFilterable, IsFacetable]
    public bool? ParkingIncluded { get; set; }

    [IsFilterable, IsFacetable]
    public bool? SmokingAllowed { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public DateTimeOffset? LastRenovationDate { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public int? Rating { get; set; }

    [IsFilterable, IsSortable]
    public GeographyPoint Location { get; set; }

    // ToString() method omitted for brevity...
}
```

<span data-ttu-id="c2686-183">Olá primeiro toonotice é que cada propriedade pública de `Hotel` corresponde tooa campo na definição de índice hello, mas com uma diferença fundamental: nome de saudação de cada campo começa com uma letra minúscula ("concatenação com maiusculas"), ao nome de saudação de cada público propriedade de `Hotel` começa com uma letra maiuscula ("Pascal case").</span><span class="sxs-lookup"><span data-stu-id="c2686-183">hello first thing toonotice is that each public property of `Hotel` corresponds tooa field in hello index definition, but with one crucial difference: hello name of each field starts with a lower-case letter ("camel case"), while hello name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="c2686-184">Este é um cenário comum em aplicativos .NET que executem a associação de dados em que o esquema de destino Olá é controle Olá fora do desenvolvedor do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="c2686-184">This is a common scenario in .NET applications that perform data-binding where hello target schema is outside hello control of hello application developer.</span></span> <span data-ttu-id="c2686-185">Em vez de tooviolate Olá .NET diretrizes de nomenclatura, tornando o caso de ter de nomes de propriedade, você pode informar Olá SDK toomap Olá propriedade nomes toocamel caso automaticamente com hello `[SerializePropertyNamesAsCamelCase]` atributo.</span><span class="sxs-lookup"><span data-stu-id="c2686-185">Rather than having tooviolate hello .NET naming guidelines by making property names camel-case, you can tell hello SDK toomap hello property names toocamel-case automatically with hello `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="c2686-186">Olá SDK .NET da pesquisa do Azure usa Olá [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) tooserialize de biblioteca e desserializar o tooand de objetos de modelo personalizado do JSON.</span><span class="sxs-lookup"><span data-stu-id="c2686-186">hello Azure Search .NET SDK uses hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library tooserialize and deserialize your custom model objects tooand from JSON.</span></span> <span data-ttu-id="c2686-187">Se necessário, você pode personalizar essa serialização.</span><span class="sxs-lookup"><span data-stu-id="c2686-187">You can customize this serialization if needed.</span></span> <span data-ttu-id="c2686-188">Encontre mais detalhes em [Serialização personalizada com JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet).</span><span class="sxs-lookup"><span data-stu-id="c2686-188">You can find more details in [Custom Serialization with JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet).</span></span> <span data-ttu-id="c2686-189">Um exemplo disso é o uso de saudação do hello `[JsonProperty]` atributo Olá `DescriptionFr` propriedade no código de exemplo hello acima.</span><span class="sxs-lookup"><span data-stu-id="c2686-189">One example of this is hello use of hello `[JsonProperty]` attribute on hello `DescriptionFr` property in hello sample code above.</span></span>
> 
> 

<span data-ttu-id="c2686-190">Olá segundo importante sobre Olá `Hotel` classe são tipos de dados de saudação de propriedades públicas de saudação.</span><span class="sxs-lookup"><span data-stu-id="c2686-190">hello second important thing about hello `Hotel` class are hello data types of hello public properties.</span></span> <span data-ttu-id="c2686-191">tipos de .NET Olá dessas propriedades mapeiam tipos de campo equivalente de tootheir na definição de índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="c2686-191">hello .NET types of these properties map tootheir equivalent field types in hello index definition.</span></span> <span data-ttu-id="c2686-192">Por exemplo, Olá `Category` mapas de propriedade de cadeia de caracteres toohello `category` campo, que é do tipo `DataType.String`.</span><span class="sxs-lookup"><span data-stu-id="c2686-192">For example, hello `Category` string property maps toohello `category` field, which is of type `DataType.String`.</span></span> <span data-ttu-id="c2686-193">Há mapeamentos de tipo semelhantes entre `bool?` e `DataType.Boolean`, `DateTimeOffset?` e `DataType.DateTimeOffset` etc.</span><span class="sxs-lookup"><span data-stu-id="c2686-193">There are similar type mappings between `bool?` and `DataType.Boolean`, `DateTimeOffset?` and `DataType.DateTimeOffset`, and so forth.</span></span> <span data-ttu-id="c2686-194">regras específicas de saudação para mapeamento de tipo hello documentadas com hello `Documents.Get` método hello [referência de SDK .NET da pesquisa do Azure](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span><span class="sxs-lookup"><span data-stu-id="c2686-194">hello specific rules for hello type mapping are documented with hello `Documents.Get` method in hello [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span>

<span data-ttu-id="c2686-195">Essa capacidade toouse suas próprias classes como documentos funciona em ambas as direções; Você também pode recuperar os resultados da pesquisa e ter Olá SDK automaticamente desserializá-los tooa tipo de sua escolha, conforme mostrado no hello [próximo artigo](search-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="c2686-195">This ability toouse your own classes as documents works in both directions; You can also retrieve search results and have hello SDK automatically deserialize them tooa type of your choice, as shown in hello [next article](search-query-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c2686-196">Olá SDK .NET da pesquisa do Azure também oferece suporte a documentos digitadas dinamicamente usando Olá `Document` classe, que é um mapeamento de chave/valor nomes toofield de valores de campo.</span><span class="sxs-lookup"><span data-stu-id="c2686-196">hello Azure Search .NET SDK also supports dynamically-typed documents using hello `Document` class, which is a key/value mapping of field names toofield values.</span></span> <span data-ttu-id="c2686-197">Isso é útil em cenários onde você não souber o esquema de índice Olá em tempo de design, ou onde seria classes de modelo de toospecific toobind inconveniente.</span><span class="sxs-lookup"><span data-stu-id="c2686-197">This is useful in scenarios where you don't know hello index schema at design-time, or where it would be inconvenient toobind toospecific model classes.</span></span> <span data-ttu-id="c2686-198">Todos os métodos Olá Olá SDK que lidam com documentos têm sobrecargas que funcionam com hello `Document` classe, bem como sobrecargas fortemente tipados que usam um parâmetro de tipo genérico.</span><span class="sxs-lookup"><span data-stu-id="c2686-198">All hello methods in hello SDK that deal with documents have overloads that work with hello `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="c2686-199">Olá somente última são usados no código de exemplo hello neste artigo.</span><span class="sxs-lookup"><span data-stu-id="c2686-199">Only hello latter are used in hello sample code in this article.</span></span>
> 
> 

<span data-ttu-id="c2686-200">**Por que você deve usar tipos de dados anuláveis**</span><span class="sxs-lookup"><span data-stu-id="c2686-200">**Why you should use nullable data types**</span></span>

<span data-ttu-id="c2686-201">Durante a criação de índice de pesquisa do Azure seu próprio modelo classes toomap tooan, é recomendável declarando propriedades de tipos de valor como `bool` e `int` toobe anulável (por exemplo, `bool?` em vez de `bool`).</span><span class="sxs-lookup"><span data-stu-id="c2686-201">When designing your own model classes toomap tooan Azure Search index, we recommend declaring properties of value types such as `bool` and `int` toobe nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="c2686-202">Se você usar uma propriedade não anulável, você tem muito**garante** sem documentos no índice contêm um valor nulo para o campo correspondente do hello.</span><span class="sxs-lookup"><span data-stu-id="c2686-202">If you use a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="c2686-203">Olá SDK, nem Olá serviço Azure Search ajudará você tooenforce isso.</span><span class="sxs-lookup"><span data-stu-id="c2686-203">Neither hello SDK nor hello Azure Search service will help you tooenforce this.</span></span>

<span data-ttu-id="c2686-204">Isso não é apenas uma preocupação hipotética: Imagine um cenário em que você adicionar um novo campo tooan índice existente que é do tipo `DataType.Int32`.</span><span class="sxs-lookup"><span data-stu-id="c2686-204">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `DataType.Int32`.</span></span> <span data-ttu-id="c2686-205">Depois de atualizar a definição de índice hello, todos os documentos terá um valor nulo para esse novo campo (desde que todos os tipos são anuláveis na pesquisa do Azure).</span><span class="sxs-lookup"><span data-stu-id="c2686-205">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="c2686-206">Se você usar uma classe de modelo com um não anulável `int` propriedade para esse campo, você receberá um `JsonSerializationException` assim ao tentar tooretrieve documentos:</span><span class="sxs-lookup"><span data-stu-id="c2686-206">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="c2686-207">Por esse motivo, sugerimos que você use tipos anuláveis nas suas classes de modelo como uma prática recomendada.</span><span class="sxs-lookup"><span data-stu-id="c2686-207">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2686-208">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c2686-208">Next steps</span></span>
<span data-ttu-id="c2686-209">Depois de preencher o índice de pesquisa do Azure, você será toostart pronto emitir consultas toosearch para documentos.</span><span class="sxs-lookup"><span data-stu-id="c2686-209">After populating your Azure Search index, you will be ready toostart issuing queries toosearch for documents.</span></span> <span data-ttu-id="c2686-210">Veja [Consultar seu Índice de Pesquisa do Azure](search-query-overview.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="c2686-210">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>

