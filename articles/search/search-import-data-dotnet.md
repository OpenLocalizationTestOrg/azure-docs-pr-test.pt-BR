---
title: Carregar dados (.NET - Azure Search) | Microsoft Docs
description: "Aprenda a carregar dados em um índice na Pesquisa do Azure usando o SDK do .NET."
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
ms.openlocfilehash: bdd952869143c6ca6374bb9264db5bcba1f32b50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="upload-data-to-azure-search-using-the-net-sdk"></a><span data-ttu-id="b8e52-103">Carregar dados para a Pesquisa do Azure usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="b8e52-103">Upload data to Azure Search using the .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b8e52-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="b8e52-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="b8e52-105">.NET</span><span class="sxs-lookup"><span data-stu-id="b8e52-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="b8e52-106">REST</span><span class="sxs-lookup"><span data-stu-id="b8e52-106">REST</span></span>](search-import-data-rest-api.md)
> 
> 

<span data-ttu-id="b8e52-107">Este artigo mostrará como usar o [SDK do .NET de Pesquisa do Azure](https://aka.ms/search-sdk) para importar os dados para um índice de Pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8e52-107">This article will show you how to use the [Azure Search .NET SDK](https://aka.ms/search-sdk) to import data into an Azure Search index.</span></span>

<span data-ttu-id="b8e52-108">Antes de começar este passo a passo, você já deve ter [criado um índice de Pesquisa do Azure](search-what-is-an-index.md).</span><span class="sxs-lookup"><span data-stu-id="b8e52-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span> <span data-ttu-id="b8e52-109">Este artigo também presume que você já criou um objeto `SearchServiceClient` , conforme mostrado em [Criar um índice de Pesquisa do Azure usando o SDK do .NET](search-create-index-dotnet.md#CreateSearchServiceClient).</span><span class="sxs-lookup"><span data-stu-id="b8e52-109">This article also assumes that you have already created a `SearchServiceClient` object, as shown in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#CreateSearchServiceClient).</span></span>

> [!NOTE]
> <span data-ttu-id="b8e52-110">Todos os códigos de exemplo neste artigo foram escritos em C#.</span><span class="sxs-lookup"><span data-stu-id="b8e52-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="b8e52-111">Você pode encontrar o código-fonte completo [no GitHub](http://aka.ms/search-dotnet-howto).</span><span class="sxs-lookup"><span data-stu-id="b8e52-111">You can find the full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="b8e52-112">Você também pode ler sobre o [SDK .NET do Azure Search](search-howto-dotnet-sdk.md) para passo a passo mais detalhado do código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="b8e52-112">You can also read about the [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of the sample code.</span></span>

<span data-ttu-id="b8e52-113">Para enviar por push documentos no índice usando o SDK do .NET, você precisa:</span><span class="sxs-lookup"><span data-stu-id="b8e52-113">In order to push documents into your index using the .NET SDK, you will need to:</span></span>

1. <span data-ttu-id="b8e52-114">Crie um objeto `SearchIndexClient` para conectar o índice de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="b8e52-114">Create a `SearchIndexClient` object to connect to your search index.</span></span>
2. <span data-ttu-id="b8e52-115">Criar um `IndexBatch` contendo os documentos a serem adicionados, modificados ou excluídos.</span><span class="sxs-lookup"><span data-stu-id="b8e52-115">Create an `IndexBatch` containing the documents to be added, modified, or deleted.</span></span>
3. <span data-ttu-id="b8e52-116">Chame o método `Documents.Index` do `SearchIndexClient` para enviar o `IndexBatch` para o índice de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="b8e52-116">Call the `Documents.Index` method of your `SearchIndexClient` to send the `IndexBatch` to your search index.</span></span>

## <a name="create-an-instance-of-the-searchindexclient-class"></a><span data-ttu-id="b8e52-117">Criar uma instância da classe SearchIndexClient</span><span class="sxs-lookup"><span data-stu-id="b8e52-117">Create an instance of the SearchIndexClient class</span></span>
<span data-ttu-id="b8e52-118">Para importar os dados para o índice usando o SDK do .NET de Pesquisa do Azure, você precisará criar uma instância da classe `SearchIndexClient` .</span><span class="sxs-lookup"><span data-stu-id="b8e52-118">To import data into your index using the Azure Search .NET SDK, you will need to create an instance of the `SearchIndexClient` class.</span></span> <span data-ttu-id="b8e52-119">Você pode construir essa instância por conta própria, mas será mais fácil se já tiver uma instância `SearchServiceClient` para chamar o método `Indexes.GetClient`.</span><span class="sxs-lookup"><span data-stu-id="b8e52-119">You can construct this instance yourself, but it's easier if you already have a `SearchServiceClient` instance to call its `Indexes.GetClient` method.</span></span> <span data-ttu-id="b8e52-120">Por exemplo, aqui está como você obteria um `SearchIndexClient` para o índice chamado "hotéis" a partir de um `SearchServiceClient` denominado `serviceClient`:</span><span class="sxs-lookup"><span data-stu-id="b8e52-120">For example, here is how you would obtain a `SearchIndexClient` for the index named "hotels" from a `SearchServiceClient` named `serviceClient`:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="b8e52-121">Em um aplicativo típico de pesquisa, o gerenciamento e o preenchimento do índice é tratado por um componente separado das consultas de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="b8e52-121">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="b8e52-122">`Indexes.GetClient` é conveniente para preencher um índice porque poupa o trabalho de fornecer outras `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="b8e52-122">`Indexes.GetClient` is convenient for populating an index because it saves you the trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="b8e52-123">Ele faz isso passando a chave de administrador que você usou para criar o `SearchServiceClient` ao novo `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="b8e52-123">It does this by passing the admin key that you used to create the `SearchServiceClient` to the new `SearchIndexClient`.</span></span> <span data-ttu-id="b8e52-124">No entanto, na parte do aplicativo que executa consultas, é melhor criar o `SearchIndexClient` diretamente para que você possa passar uma chave de consulta em vez de uma chave de administrador.</span><span class="sxs-lookup"><span data-stu-id="b8e52-124">However, in the part of your application that executes queries, it is better to create the `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="b8e52-125">Isso é consistente com o [princípio do privilégio mínimo](https://en.wikipedia.org/wiki/Principle_of_least_privilege) e ajudará a tornar seu aplicativo mais seguro.</span><span class="sxs-lookup"><span data-stu-id="b8e52-125">This is consistent with the [principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege) and will help to make your application more secure.</span></span> <span data-ttu-id="b8e52-126">Você pode encontrar mais informações sobre as chaves de administração e as chaves de consulta na [Referência da API REST do Azure Search](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="b8e52-126">You can find out more about admin keys and query keys in the [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
> 
> 

<span data-ttu-id="b8e52-127">`SearchIndexClient` tem uma propriedade `Documents`.</span><span class="sxs-lookup"><span data-stu-id="b8e52-127">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="b8e52-128">Esta propriedade fornece todos os métodos que você precisa para adicionar, modificar, excluir ou consultar documentos no índice.</span><span class="sxs-lookup"><span data-stu-id="b8e52-128">This property provides all the methods you need to add, modify, delete, or query documents in your index.</span></span>

## <a name="decide-which-indexing-action-to-use"></a><span data-ttu-id="b8e52-129">Decidir qual ação de indexação será usada</span><span class="sxs-lookup"><span data-stu-id="b8e52-129">Decide which indexing action to use</span></span>
<span data-ttu-id="b8e52-130">Para importar os dados usando o SDK do .NET, você precisará empacotar seus dados em um objeto `IndexBatch` .</span><span class="sxs-lookup"><span data-stu-id="b8e52-130">To import data using the .NET SDK, you will need to package up your data into an `IndexBatch` object.</span></span> <span data-ttu-id="b8e52-131">Um `IndexBatch` encapsula uma coleção de objetos `IndexAction`, que contém, cada um deles, um documento e uma propriedade que informam à Pesquisa do Azure qual ação executar nesse documento (carregar, mesclar, excluir etc.).</span><span class="sxs-lookup"><span data-stu-id="b8e52-131">An `IndexBatch` encapsulates a collection of `IndexAction` objects, each of which contains a document and a property that tells Azure Search what action to perform on that document (upload, merge, delete, etc).</span></span> <span data-ttu-id="b8e52-132">Dependendo de qual das ações abaixo você escolher, apenas determinados campos deverão ser incluídos em cada documento:</span><span class="sxs-lookup"><span data-stu-id="b8e52-132">Depending on which of the below actions you choose, only certain fields must be included for each document:</span></span>

| <span data-ttu-id="b8e52-133">Ação</span><span class="sxs-lookup"><span data-stu-id="b8e52-133">Action</span></span> | <span data-ttu-id="b8e52-134">Descrição</span><span class="sxs-lookup"><span data-stu-id="b8e52-134">Description</span></span> | <span data-ttu-id="b8e52-135">Campos necessários para cada documento</span><span class="sxs-lookup"><span data-stu-id="b8e52-135">Necessary fields for each document</span></span> | <span data-ttu-id="b8e52-136">Observações</span><span class="sxs-lookup"><span data-stu-id="b8e52-136">Notes</span></span> |
| --- | --- | --- | --- |
| `Upload` |<span data-ttu-id="b8e52-137">Uma ação `Upload` é semelhante a um "upsert", em que o documento será inserido se for novo e atualizado/substituído se existir.</span><span class="sxs-lookup"><span data-stu-id="b8e52-137">An `Upload` action is similar to an "upsert" where the document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="b8e52-138">chave, além de quaisquer outros campos que você quiser definir</span><span class="sxs-lookup"><span data-stu-id="b8e52-138">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="b8e52-139">Ao atualizar/substituir um documento existente, qualquer campo não especificado na solicitação terá seu campo definido para `null`.</span><span class="sxs-lookup"><span data-stu-id="b8e52-139">When updating/replacing an existing document, any field that is not specified in the request will have its field set to `null`.</span></span> <span data-ttu-id="b8e52-140">Isso ocorre mesmo quando o campo tiver sido definido anteriormente como um valor não nulo.</span><span class="sxs-lookup"><span data-stu-id="b8e52-140">This occurs even when the field was previously set to a non-null value.</span></span> |
| `Merge` |<span data-ttu-id="b8e52-141">Atualiza um documento existente com os campos especificados.</span><span class="sxs-lookup"><span data-stu-id="b8e52-141">Updates an existing document with the specified fields.</span></span> <span data-ttu-id="b8e52-142">Se o documento não existir no índice, a mesclagem falhará.</span><span class="sxs-lookup"><span data-stu-id="b8e52-142">If the document does not exist in the index, the merge will fail.</span></span> |<span data-ttu-id="b8e52-143">chave, além de quaisquer outros campos que você quiser definir</span><span class="sxs-lookup"><span data-stu-id="b8e52-143">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="b8e52-144">Qualquer campo que você especificar em uma mesclagem substituirá o campo existente no documento.</span><span class="sxs-lookup"><span data-stu-id="b8e52-144">Any field you specify in a merge will replace the existing field in the document.</span></span> <span data-ttu-id="b8e52-145">Isso inclui campos do tipo `DataType.Collection(DataType.String)`.</span><span class="sxs-lookup"><span data-stu-id="b8e52-145">This includes fields of type `DataType.Collection(DataType.String)`.</span></span> <span data-ttu-id="b8e52-146">Por exemplo, se o documento contiver um campo `tags` com o valor `["budget"]` e você executar uma mesclagem com o valor `["economy", "pool"]` para `tags`, o valor final do campo `tags` será `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="b8e52-146">For example, if the document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, the final value of the `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="b8e52-147">Ele não será `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="b8e52-147">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `MergeOrUpload` |<span data-ttu-id="b8e52-148">Essa ação se comportará como `Merge` se já existir um documento com a chave especificada no índice.</span><span class="sxs-lookup"><span data-stu-id="b8e52-148">This action behaves like `Merge` if a document with the given key already exists in the index.</span></span> <span data-ttu-id="b8e52-149">Se o documento não existir, ele se comportará como `Upload` com um novo documento.</span><span class="sxs-lookup"><span data-stu-id="b8e52-149">If the document does not exist, it behaves like `Upload` with a new document.</span></span> |<span data-ttu-id="b8e52-150">chave, além de quaisquer outros campos que você quiser definir</span><span class="sxs-lookup"><span data-stu-id="b8e52-150">key, plus any other fields you wish to define</span></span> |- |
| `Delete` |<span data-ttu-id="b8e52-151">Remove o documento especificado do índice.</span><span class="sxs-lookup"><span data-stu-id="b8e52-151">Removes the specified document from the index.</span></span> |<span data-ttu-id="b8e52-152">somente chave</span><span class="sxs-lookup"><span data-stu-id="b8e52-152">key only</span></span> |<span data-ttu-id="b8e52-153">Todos os campos que você especificar, exceto o campo de chave, serão ignorados.</span><span class="sxs-lookup"><span data-stu-id="b8e52-153">Any fields you specify other than the key field will be ignored.</span></span> <span data-ttu-id="b8e52-154">Se você quiser remover um campo individual de um documento, use `Merge` e apenas defina o campo explicitamente para null.</span><span class="sxs-lookup"><span data-stu-id="b8e52-154">If you want to remove an individual field from a document, use `Merge` instead and simply set the field explicitly to null.</span></span> |

<span data-ttu-id="b8e52-155">Você pode especificar a ação que deseja usar com os diversos métodos estáticos das classes `IndexBatch` e `IndexAction`, conforme mostrado na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="b8e52-155">You can specify what action you want to use with the various static methods of the `IndexBatch` and `IndexAction` classes, as shown in the next section.</span></span>

## <a name="construct-your-indexbatch"></a><span data-ttu-id="b8e52-156">Construa seu IndexBatch</span><span class="sxs-lookup"><span data-stu-id="b8e52-156">Construct your IndexBatch</span></span>
<span data-ttu-id="b8e52-157">Agora que você sabe quais ações executar em seus documentos, está pronto para construir o `IndexBatch`.</span><span class="sxs-lookup"><span data-stu-id="b8e52-157">Now that you know which actions to perform on your documents, you are ready to construct the `IndexBatch`.</span></span> <span data-ttu-id="b8e52-158">O exemplo a seguir mostra como criar um lote com algumas ações diferentes.</span><span class="sxs-lookup"><span data-stu-id="b8e52-158">The example below shows how to create a batch with a few different actions.</span></span> <span data-ttu-id="b8e52-159">Observe que nosso exemplo usa uma classe personalizada denominada `Hotel` que mapeia para um documento no índice "hotéis".</span><span class="sxs-lookup"><span data-stu-id="b8e52-159">Note that our example uses a custom class called `Hotel` that maps to a document in the "hotels" index.</span></span>

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
                Description = "Close to town hall and the river"
            }),
        IndexAction.Delete(new Hotel() { HotelId = "6" })
    };

var batch = IndexBatch.New(actions);
```

<span data-ttu-id="b8e52-160">Nesse caso, estamos usando `Upload`, `MergeOrUpload` e `Delete` como nossas ações de pesquisa, conforme especificado pelos métodos chamados na classe `IndexAction`.</span><span class="sxs-lookup"><span data-stu-id="b8e52-160">In this case, we are using `Upload`, `MergeOrUpload`, and `Delete` as our search actions, as specified by the methods called on the `IndexAction` class.</span></span>

<span data-ttu-id="b8e52-161">Suponha que o índice de exemplo "hotels" já esteja preenchido com vários documentos.</span><span class="sxs-lookup"><span data-stu-id="b8e52-161">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="b8e52-162">Observe como não precisamos especificar todos os campos de documento possíveis ao usar `MergeOrUpload` e como especificamos apenas a chave do documento (`HotelId`) ao usar `Delete`.</span><span class="sxs-lookup"><span data-stu-id="b8e52-162">Note how we did not have to specify all the possible document fields when using `MergeOrUpload` and how we only specified the document key (`HotelId`) when using `Delete`.</span></span>

<span data-ttu-id="b8e52-163">Além disso, observe que você só pode incluir até 1000 documentos em uma única solicitação de indexação.</span><span class="sxs-lookup"><span data-stu-id="b8e52-163">Also, note that you can only include up to 1000 documents in a single indexing request.</span></span>

> [!NOTE]
> <span data-ttu-id="b8e52-164">Neste exemplo, estamos aplicando ações diferentes para documentos diferentes.</span><span class="sxs-lookup"><span data-stu-id="b8e52-164">In this example, we are applying different actions to different documents.</span></span> <span data-ttu-id="b8e52-165">Se você quisesse executar as mesmas ações em todos os documentos do lote, em vez de chamar `IndexBatch.New`, poderia usar os outros métodos estáticos de `IndexBatch`.</span><span class="sxs-lookup"><span data-stu-id="b8e52-165">If you wanted to perform the same actions across all documents in the batch, instead of calling `IndexBatch.New`, you could use the other static methods of `IndexBatch`.</span></span> <span data-ttu-id="b8e52-166">Por exemplo, você poderia criar lotes chamando `IndexBatch.Merge`, `IndexBatch.MergeOrUpload` ou `IndexBatch.Delete`.</span><span class="sxs-lookup"><span data-stu-id="b8e52-166">For example, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete`.</span></span> <span data-ttu-id="b8e52-167">Esses métodos usam um conjunto de documentos (objetos do tipo `Hotel` neste exemplo) em vez de objetos `IndexAction`.</span><span class="sxs-lookup"><span data-stu-id="b8e52-167">These methods take a collection of documents (objects of type `Hotel` in this example) instead of `IndexAction` objects.</span></span>
> 
> 

## <a name="import-data-to-the-index"></a><span data-ttu-id="b8e52-168">Importar dados para o índice</span><span class="sxs-lookup"><span data-stu-id="b8e52-168">Import data to the index</span></span>
<span data-ttu-id="b8e52-169">Agora que você tem um objeto `IndexBatch` inicializado, pode enviá-lo para o índice chamando `Documents.Index` em seu objeto `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="b8e52-169">Now that you have an initialized `IndexBatch` object, you can send it to the index by calling `Documents.Index` on your `SearchIndexClient` object.</span></span> <span data-ttu-id="b8e52-170">O exemplo a seguir mostra como chamar `Index`, assim como algumas etapas adicionais que você precisa executar:</span><span class="sxs-lookup"><span data-stu-id="b8e52-170">The following example shows how to call `Index`, as well as some extra steps you will need to perform:</span></span>

```csharp
try
{
    indexClient.Documents.Index(batch);
}
catch (IndexBatchException e)
{
    // Sometimes when your Search service is under load, indexing will fail for some of the documents in
    // the batch. Depending on your application, you can take compensating actions like delaying and
    // retrying. For this simple demo, we just log the failed document keys and continue.
    Console.WriteLine(
        "Failed to index some of the documents: {0}",
        String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
}

Console.WriteLine("Waiting for documents to be indexed...\n");
Thread.Sleep(2000);
```

<span data-ttu-id="b8e52-171">Observe `try`/`catch` em torno da chamada para o método `Index`.</span><span class="sxs-lookup"><span data-stu-id="b8e52-171">Note the `try`/`catch` surrounding the call to the `Index` method.</span></span> <span data-ttu-id="b8e52-172">O bloco catch lida com um caso de erro importante para a indexação.</span><span class="sxs-lookup"><span data-stu-id="b8e52-172">The catch block handles an important error case for indexing.</span></span> <span data-ttu-id="b8e52-173">Se o serviço de Pesquisa do Azure não indexar alguns documentos no lote, uma `IndexBatchException` será lançada por `Documents.Index`.</span><span class="sxs-lookup"><span data-stu-id="b8e52-173">If your Azure Search service fails to index some of the documents in the batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="b8e52-174">Isso pode acontecer se você estiver indexando documentos enquanto o serviço estiver sob carga pesada.</span><span class="sxs-lookup"><span data-stu-id="b8e52-174">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="b8e52-175">**É altamente recomendável a manipulação explícita desse caso em seu código.**</span><span class="sxs-lookup"><span data-stu-id="b8e52-175">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="b8e52-176">Você pode atrasar e repetir a indexação de documentos que falharam, ou você pode registrar em log e continuar, como faz o exemplo, ou pode alguma outra coisa, dependendo dos requisitos de consistência de dados do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b8e52-176">You can delay and then retry indexing the documents that failed, or you can log and continue like the sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

<span data-ttu-id="b8e52-177">Por fim, o código no exemplo acima, atrasa por dois segundos.</span><span class="sxs-lookup"><span data-stu-id="b8e52-177">Finally, the code in the example above delays for two seconds.</span></span> <span data-ttu-id="b8e52-178">A indexação ocorre de maneira assíncrona em seu serviço de Pesquisa do Azure, portanto, o exemplo de aplicativo precisa aguardar alguns instantes para garantir que os documentos estejam disponíveis para pesquisa.</span><span class="sxs-lookup"><span data-stu-id="b8e52-178">Indexing happens asynchronously in your Azure Search service, so the sample application needs to wait a short time to ensure that the documents are available for searching.</span></span> <span data-ttu-id="b8e52-179">Normalmente, atrasos como esses só são necessários em demonstrações, testes e exemplos de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b8e52-179">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

<a name="HotelClass"></a>

### <a name="how-the-net-sdk-handles-documents"></a><span data-ttu-id="b8e52-180">Como o SDK do .NET lida com documentos</span><span class="sxs-lookup"><span data-stu-id="b8e52-180">How the .NET SDK handles documents</span></span>
<span data-ttu-id="b8e52-181">Você pode estar se perguntando como o SDK do .NET da Pesquisa do Azure é capaz de carregar instâncias de uma classe definida pelo usuário, como `Hotel` , no índice.</span><span class="sxs-lookup"><span data-stu-id="b8e52-181">You may be wondering how the Azure Search .NET SDK is able to upload instances of a user-defined class like `Hotel` to the index.</span></span> <span data-ttu-id="b8e52-182">Para ajudar a responder a essa pergunta, examinaremos a classe `Hotel` , que mapeia para o esquema de índice definido em [Criar um Índice de pesquisa do Azure usando o SDK do .NET](search-create-index-dotnet.md#DefineIndex):</span><span class="sxs-lookup"><span data-stu-id="b8e52-182">To help answer that question, let's look at the `Hotel` class, which maps to the index schema defined in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#DefineIndex):</span></span>

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

<span data-ttu-id="b8e52-183">A primeira coisa a observar é que cada propriedade pública de `Hotel` corresponde a um campo na definição do índice, mas com uma diferença fundamental: o nome de cada campo começa com uma letra minúscula ("minúsculas concatenadas"), enquanto o nome de cada propriedade pública de `Hotel` começa com uma letra maiúscula ("maiúsculas concatenadas").</span><span class="sxs-lookup"><span data-stu-id="b8e52-183">The first thing to notice is that each public property of `Hotel` corresponds to a field in the index definition, but with one crucial difference: The name of each field starts with a lower-case letter ("camel case"), while the name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="b8e52-184">Esse é um cenário comum em aplicativos .NET que executam associação de dados quando o esquema de destino está fora do controle do desenvolvedor do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b8e52-184">This is a common scenario in .NET applications that perform data-binding where the target schema is outside the control of the application developer.</span></span> <span data-ttu-id="b8e52-185">Em vez de violar as diretrizes de nomenclatura do .NET, usando minúscula para os nomes de propriedade, você pode informar ao SDK para mapear automaticamente os nomes de propriedade como minúscula com o atributo `[SerializePropertyNamesAsCamelCase]` .</span><span class="sxs-lookup"><span data-stu-id="b8e52-185">Rather than having to violate the .NET naming guidelines by making property names camel-case, you can tell the SDK to map the property names to camel-case automatically with the `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="b8e52-186">O SDK do .NET de Pesquisa do Azure usa a biblioteca [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) para serializar e desserializar os objetos de modelo personalizados para e a partir do JSON.</span><span class="sxs-lookup"><span data-stu-id="b8e52-186">The Azure Search .NET SDK uses the [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library to serialize and deserialize your custom model objects to and from JSON.</span></span> <span data-ttu-id="b8e52-187">Se necessário, você pode personalizar essa serialização.</span><span class="sxs-lookup"><span data-stu-id="b8e52-187">You can customize this serialization if needed.</span></span> <span data-ttu-id="b8e52-188">Encontre mais detalhes em [Serialização personalizada com JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet).</span><span class="sxs-lookup"><span data-stu-id="b8e52-188">You can find more details in [Custom Serialization with JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet).</span></span> <span data-ttu-id="b8e52-189">Um exemplo disso é o uso do atributo `[JsonProperty]` na propriedade `DescriptionFr` no código de exemplo acima.</span><span class="sxs-lookup"><span data-stu-id="b8e52-189">One example of this is the use of the `[JsonProperty]` attribute on the `DescriptionFr` property in the sample code above.</span></span>
> 
> 

<span data-ttu-id="b8e52-190">Um segundo fator importante sobre a classe `Hotel` são os tipos de dados das propriedades públicas.</span><span class="sxs-lookup"><span data-stu-id="b8e52-190">The second important thing about the `Hotel` class are the data types of the public properties.</span></span> <span data-ttu-id="b8e52-191">Os tipos .NET dessas propriedades são mapeados para seus tipos de campo equivalentes na definição do índice.</span><span class="sxs-lookup"><span data-stu-id="b8e52-191">The .NET types of these properties map to their equivalent field types in the index definition.</span></span> <span data-ttu-id="b8e52-192">Por exemplo, a propriedade de cadeia de caracteres `Category` mapeia para o campo `category`, que é do tipo `DataType.String`.</span><span class="sxs-lookup"><span data-stu-id="b8e52-192">For example, the `Category` string property maps to the `category` field, which is of type `DataType.String`.</span></span> <span data-ttu-id="b8e52-193">Há mapeamentos de tipo semelhantes entre `bool?` e `DataType.Boolean`, `DateTimeOffset?` e `DataType.DateTimeOffset` etc.</span><span class="sxs-lookup"><span data-stu-id="b8e52-193">There are similar type mappings between `bool?` and `DataType.Boolean`, `DateTimeOffset?` and `DataType.DateTimeOffset`, and so forth.</span></span> <span data-ttu-id="b8e52-194">As regras específicas para o mapeamento de tipos estão documentadas com o método `Documents.Get` na [referência do SDK do .NET do Search](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span><span class="sxs-lookup"><span data-stu-id="b8e52-194">The specific rules for the type mapping are documented with the `Documents.Get` method in the [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span>

<span data-ttu-id="b8e52-195">Essa capacidade de usar suas próprias classes como documentos funciona em ambas as direções. Você também pode recuperar os resultados da pesquisa e fazer com que o SDK desserialize-os automaticamente para um tipo de sua escolha, como mostrado no [próximo artigo](search-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="b8e52-195">This ability to use your own classes as documents works in both directions; You can also retrieve search results and have the SDK automatically deserialize them to a type of your choice, as shown in the [next article](search-query-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b8e52-196">O SDK do .NET da Pesquisa do Azure também oferece suporte a documentos do tipo dinâmico usando a classe `Document`, que é um mapeamento de chave/valor de nomes de campo para valores de campo.</span><span class="sxs-lookup"><span data-stu-id="b8e52-196">The Azure Search .NET SDK also supports dynamically-typed documents using the `Document` class, which is a key/value mapping of field names to field values.</span></span> <span data-ttu-id="b8e52-197">Isso é útil em cenários nos quais você não conhece o esquema de índice no momento do design, ou nos quais seria inconveniente associar a classes de modelo específico.</span><span class="sxs-lookup"><span data-stu-id="b8e52-197">This is useful in scenarios where you don't know the index schema at design-time, or where it would be inconvenient to bind to specific model classes.</span></span> <span data-ttu-id="b8e52-198">Todos os métodos no SDK que lidam com documentos têm sobrecargas que funcionam com a classe `Document` , bem como sobrecargas fortemente tipadas que utilizam um parâmetro de tipo genérico.</span><span class="sxs-lookup"><span data-stu-id="b8e52-198">All the methods in the SDK that deal with documents have overloads that work with the `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="b8e52-199">Somente as últimas são usadas no código de exemplo neste artigo.</span><span class="sxs-lookup"><span data-stu-id="b8e52-199">Only the latter are used in the sample code in this article.</span></span>
> 
> 

<span data-ttu-id="b8e52-200">**Por que você deve usar tipos de dados anuláveis**</span><span class="sxs-lookup"><span data-stu-id="b8e52-200">**Why you should use nullable data types**</span></span>

<span data-ttu-id="b8e52-201">Ao criar suas próprias classes de modelo para mapear para um índice de Pesquisa do Azure, sugerimos declarar as propriedades dos tipos de valor como `bool` e `int` para serem anuláveis (por exemplo, `bool?` em vez de `bool`).</span><span class="sxs-lookup"><span data-stu-id="b8e52-201">When designing your own model classes to map to an Azure Search index, we recommend declaring properties of value types such as `bool` and `int` to be nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="b8e52-202">Se você usar uma propriedade não anulável, será preciso **assegurar** que nenhum documento no índice contenha um valor nulo para o campo correspondente.</span><span class="sxs-lookup"><span data-stu-id="b8e52-202">If you use a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span></span> <span data-ttu-id="b8e52-203">Nem o SDK, nem o serviço Pesquisa do Azure ajudarão você a impor isso.</span><span class="sxs-lookup"><span data-stu-id="b8e52-203">Neither the SDK nor the Azure Search service will help you to enforce this.</span></span>

<span data-ttu-id="b8e52-204">Isso não é apenas uma preocupação hipotética: imagine um cenário em que você adiciona um novo campo a um índice existente do tipo `DataType.Int32`.</span><span class="sxs-lookup"><span data-stu-id="b8e52-204">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `DataType.Int32`.</span></span> <span data-ttu-id="b8e52-205">Depois de atualizar a definição de índice, todos os documentos terão um valor nulo para esse novo campo (já que todos os tipos são anuláveis na Pesquisa do Azure).</span><span class="sxs-lookup"><span data-stu-id="b8e52-205">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="b8e52-206">Ao usar uma classe de modelo com uma propriedade não anulável `int` para esse campo, você obterá uma `JsonSerializationException` como esta ao tentar recuperar os documentos:</span><span class="sxs-lookup"><span data-stu-id="b8e52-206">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span></span>

    Error converting value {null} to type 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="b8e52-207">Por esse motivo, sugerimos que você use tipos anuláveis nas suas classes de modelo como uma prática recomendada.</span><span class="sxs-lookup"><span data-stu-id="b8e52-207">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8e52-208">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b8e52-208">Next steps</span></span>
<span data-ttu-id="b8e52-209">Depois de popular o índice de Pesquisa do Azure, você estará pronto para começar a emitir consultas para pesquisar documentos.</span><span class="sxs-lookup"><span data-stu-id="b8e52-209">After populating your Azure Search index, you will be ready to start issuing queries to search for documents.</span></span> <span data-ttu-id="b8e52-210">Veja [Consultar seu Índice de Pesquisa do Azure](search-query-overview.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="b8e52-210">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>

