---
title: "AAA \"consultar um índice (API .NET - pesquisa do Azure) | Microsoft Docs\""
description: "Criar uma consulta de pesquisa na pesquisa do Azure e usar os resultados da pesquisa pesquisa parâmetros toofilter e classificação."
services: search
manager: jhubbard
documentationcenter: 
author: brjohnstmsft
ms.assetid: 12c3efba-ea99-4187-9d2d-f63b5ec7040d
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/19/2017
ms.author: brjohnst
ms.openlocfilehash: 8b3ba1cd1270aad038fb48d9053fcff35d243e13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index-using-hello-net-sdk"></a><span data-ttu-id="db13c-103">Consultar seu índice de pesquisa do Azure usando o SDK .NET de saudação</span><span class="sxs-lookup"><span data-stu-id="db13c-103">Query your Azure Search index using hello .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="db13c-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="db13c-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="db13c-105">Portal</span><span class="sxs-lookup"><span data-stu-id="db13c-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="db13c-106">.NET</span><span class="sxs-lookup"><span data-stu-id="db13c-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="db13c-107">REST</span><span class="sxs-lookup"><span data-stu-id="db13c-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="db13c-108">Este artigo mostra como tooquery um índice usando Olá [SDK .NET da pesquisa do Azure](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="db13c-108">This article will show you how tooquery an index using hello [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span>

<span data-ttu-id="db13c-109">Antes de começar este passo a passo, você já deve ter [criado um índice do Azure Search](search-what-is-an-index.md), e este já deve estar [preenchido com os dados](search-what-is-data-import.md).</span><span class="sxs-lookup"><span data-stu-id="db13c-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span>

> [!NOTE]
> <span data-ttu-id="db13c-110">Todos os códigos de exemplo neste artigo foram escritos em C#.</span><span class="sxs-lookup"><span data-stu-id="db13c-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="db13c-111">Você pode encontrar o código-fonte completo Olá [no GitHub](http://aka.ms/search-dotnet-howto).</span><span class="sxs-lookup"><span data-stu-id="db13c-111">You can find hello full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="db13c-112">Você também pode ler sobre Olá [SDK .NET da pesquisa do Azure](search-howto-dotnet-sdk.md) para um mais detalhado passo a passo do código de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="db13c-112">You can also read about hello [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of hello sample code.</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="db13c-113">Identificar sua api-key de consulta do serviço de Pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="db13c-113">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="db13c-114">Agora que você criou um índice de pesquisa do Azure, você está quase pronto tooissue consultas usando Olá SDK do .NET.</span><span class="sxs-lookup"><span data-stu-id="db13c-114">Now that you have created an Azure Search index, you are almost ready tooissue queries using hello .NET SDK.</span></span> <span data-ttu-id="db13c-115">Primeiro, você precisará tooobtain uma saudação consulta chaves de api que foi gerado para o serviço de pesquisa Olá que você provisionou.</span><span class="sxs-lookup"><span data-stu-id="db13c-115">First, you will need tooobtain one of hello query api-keys that was generated for hello search service you provisioned.</span></span> <span data-ttu-id="db13c-116">Olá .NET SDK enviará esta chave de api em cada solicitação de serviço tooyour.</span><span class="sxs-lookup"><span data-stu-id="db13c-116">hello .NET SDK will send this api-key on every request tooyour service.</span></span> <span data-ttu-id="db13c-117">Ter uma chave válida estabelece confiança, em uma base por solicitação, entre solicitação de envio Olá Olá aplicativo e serviço de saudação que lida com ele.</span><span class="sxs-lookup"><span data-stu-id="db13c-117">Having a valid key establishes trust, on a per request basis, between hello application sending hello request and hello service that handles it.</span></span>

1. <span data-ttu-id="db13c-118">toofind chaves do serviço de api pode entrar toohello [portal do Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="db13c-118">toofind your service's api-keys you can sign in toohello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="db13c-119">Vá folha do serviço de pesquisa do Azure tooyour</span><span class="sxs-lookup"><span data-stu-id="db13c-119">Go tooyour Azure Search service's blade</span></span>
3. <span data-ttu-id="db13c-120">Clique em Olá ícone "Chaves"</span><span class="sxs-lookup"><span data-stu-id="db13c-120">Click on hello "Keys" icon</span></span>

<span data-ttu-id="db13c-121">O serviço terá *chaves de administração* e *chaves de consulta*.</span><span class="sxs-lookup"><span data-stu-id="db13c-121">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="db13c-122">O primário e secundário *chaves de administração* conceder direitos totais tooall operações, incluindo Olá capacidade toomanage Olá serviço, criar e excluir índices, indexadores e fontes de dados.</span><span class="sxs-lookup"><span data-stu-id="db13c-122">Your primary and secondary *admin keys* grant full rights tooall operations, including hello ability toomanage hello service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="db13c-123">Há duas chaves para que você possa continuar chave secundária do toouse Olá se você decidir chave primária do tooregenerate hello e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="db13c-123">There are two keys so that you can continue toouse hello secondary key if you decide tooregenerate hello primary key, and vice-versa.</span></span>
* <span data-ttu-id="db13c-124">O *chaves de consulta* conceder acesso somente leitura tooindexes e documentos, e são normalmente distribuídos tooclient aplicativos que emitem solicitações de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="db13c-124">Your *query keys* grant read-only access tooindexes and documents, and are typically distributed tooclient applications that issue search requests.</span></span>

<span data-ttu-id="db13c-125">Para fins de saudação de consultar um índice, você pode usar uma de suas chaves de consulta.</span><span class="sxs-lookup"><span data-stu-id="db13c-125">For hello purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="db13c-126">As chaves de administração também podem ser usadas para consultas, mas você deve usar uma chave de consulta no código do aplicativo, isso melhor da seguinte maneira Olá [princípio de menos privilégios](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span><span class="sxs-lookup"><span data-stu-id="db13c-126">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows hello [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="create-an-instance-of-hello-searchindexclient-class"></a><span data-ttu-id="db13c-127">Crie uma instância da classe SearchIndexClient de saudação</span><span class="sxs-lookup"><span data-stu-id="db13c-127">Create an instance of hello SearchIndexClient class</span></span>
<span data-ttu-id="db13c-128">consultas de tooissue com hello SDK .NET da pesquisa do Azure, você precisará toocreate uma instância de saudação `SearchIndexClient` classe.</span><span class="sxs-lookup"><span data-stu-id="db13c-128">tooissue queries with hello Azure Search .NET SDK, you will need toocreate an instance of hello `SearchIndexClient` class.</span></span> <span data-ttu-id="db13c-129">Essa classe tem vários construtores.</span><span class="sxs-lookup"><span data-stu-id="db13c-129">This class has several constructors.</span></span> <span data-ttu-id="db13c-130">Olá você deseja usa o nome do serviço de pesquisa, o nome do índice e uma `SearchCredentials` objeto como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="db13c-130">hello one you want takes your search service name, index name, and a `SearchCredentials` object as parameters.</span></span> <span data-ttu-id="db13c-131">`SearchCredentials` encapsula sua api-key.</span><span class="sxs-lookup"><span data-stu-id="db13c-131">`SearchCredentials` wraps your api-key.</span></span>

<span data-ttu-id="db13c-132">Olá código a seguir cria um novo `SearchIndexClient` para índice de "hotéis" hello (criado em [criar um índice de pesquisa do Azure usando o SDK .NET de saudação](search-create-index-dotnet.md)) usando valores para o nome do serviço de pesquisa hello e chave de api que são armazenados na configuração do aplicativo hello arquivo (`appsettings.json` no caso de saudação de saudação [aplicativo de exemplo](http://aka.ms/search-dotnet-howto)):</span><span class="sxs-lookup"><span data-stu-id="db13c-132">hello code below creates a new `SearchIndexClient` for hello "hotels" index (created in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md)) using values for hello search service name and api-key that are stored in hello application's config file (`appsettings.json` in hello case of hello [sample application](http://aka.ms/search-dotnet-howto)):</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="db13c-133">`SearchIndexClient` tem uma propriedade `Documents`.</span><span class="sxs-lookup"><span data-stu-id="db13c-133">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="db13c-134">Esta propriedade fornece que todos os Olá métodos que você precisa tooquery índices de pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="db13c-134">This property provides all hello methods you need tooquery Azure Search indexes.</span></span>

## <a name="query-your-index"></a><span data-ttu-id="db13c-135">Consultar o índice</span><span class="sxs-lookup"><span data-stu-id="db13c-135">Query your index</span></span>
<span data-ttu-id="db13c-136">Pesquisando com hello .NET SDK é tão simple quanto Olá chamada `Documents.Search` método no seu `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="db13c-136">Searching with hello .NET SDK is as simple as calling hello `Documents.Search` method on your `SearchIndexClient`.</span></span> <span data-ttu-id="db13c-137">Este método usa alguns parâmetros, incluindo o texto de pesquisa hello, juntamente com um `SearchParameters` objeto que pode ser usado toofurther refinar Olá consulta.</span><span class="sxs-lookup"><span data-stu-id="db13c-137">This method takes a few parameters, including hello search text, along with a `SearchParameters` object that can be used toofurther refine hello query.</span></span>

#### <a name="types-of-queries"></a><span data-ttu-id="db13c-138">Tipos de Consultas</span><span class="sxs-lookup"><span data-stu-id="db13c-138">Types of Queries</span></span>
<span data-ttu-id="db13c-139">principal Olá dois [tipos de consulta](search-query-overview.md#types-of-queries) você usará são `search` e `filter`.</span><span class="sxs-lookup"><span data-stu-id="db13c-139">hello two main [query types](search-query-overview.md#types-of-queries) you will use are `search` and `filter`.</span></span> <span data-ttu-id="db13c-140">Uma consulta `search` procura um ou mais termos em todos os campos *pesquisáveis* no índice.</span><span class="sxs-lookup"><span data-stu-id="db13c-140">A `search` query searches for one or more terms in all *searchable* fields in your index.</span></span> <span data-ttu-id="db13c-141">Uma consulta `filter` avalia uma expressão booliana em todos os campos *filtráveis* em um índice.</span><span class="sxs-lookup"><span data-stu-id="db13c-141">A `filter` query evaluates a boolean expression over all *filterable* fields in an index.</span></span>

<span data-ttu-id="db13c-142">Pesquisa e filtros são executados usando Olá `Documents.Search` método.</span><span class="sxs-lookup"><span data-stu-id="db13c-142">Both searches and filters are performed using hello `Documents.Search` method.</span></span> <span data-ttu-id="db13c-143">Uma consulta de pesquisa pode ser passada no hello `searchText` parâmetro, enquanto uma expressão de filtro pode ser passada em Olá `Filter` propriedade Olá `SearchParameters` classe.</span><span class="sxs-lookup"><span data-stu-id="db13c-143">A search query can be passed in hello `searchText` parameter, while a filter expression can be passed in hello `Filter` property of hello `SearchParameters` class.</span></span> <span data-ttu-id="db13c-144">toofilter sem procurando, basta passar `"*"` para Olá `searchText` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="db13c-144">toofilter without searching, just pass `"*"` for hello `searchText` parameter.</span></span> <span data-ttu-id="db13c-145">toosearch sem filtragem, deixe Olá `Filter` propriedade unset, ou não passar um `SearchParameters` instância em todos os.</span><span class="sxs-lookup"><span data-stu-id="db13c-145">toosearch without filtering, just leave hello `Filter` property unset, or do not pass in a `SearchParameters` instance at all.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="db13c-146">Consultas de Exemplo</span><span class="sxs-lookup"><span data-stu-id="db13c-146">Example Queries</span></span>
<span data-ttu-id="db13c-147">Olá, código de exemplo a seguir mostra algumas maneiras diferentes tooquery hello "hotéis" índice definido na [criar um índice de pesquisa do Azure usando o SDK .NET de saudação](search-create-index-dotnet.md#DefineIndex).</span><span class="sxs-lookup"><span data-stu-id="db13c-147">hello following sample code shows a few different ways tooquery hello "hotels" index defined in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md#DefineIndex).</span></span> <span data-ttu-id="db13c-148">Observe que os documentos Olá retornados com os resultados da pesquisa Olá são instâncias de saudação `Hotel` classe, que foi definida no [importação de dados de pesquisa do Azure usando Olá .NET SDK](search-import-data-dotnet.md#HotelClass).</span><span class="sxs-lookup"><span data-stu-id="db13c-148">Note that hello documents returned with hello search results are instances of hello `Hotel` class, which was defined in [Data Import in Azure Search using hello .NET SDK](search-import-data-dotnet.md#HotelClass).</span></span> <span data-ttu-id="db13c-149">Olá código de exemplo usa um `WriteDocuments` console toohello resultados de pesquisa do método toooutput hello.</span><span class="sxs-lookup"><span data-stu-id="db13c-149">hello sample code makes use of a `WriteDocuments` method toooutput hello search results toohello console.</span></span> <span data-ttu-id="db13c-150">Esse método é descrito na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="db13c-150">This method is described in hello next section.</span></span>

```csharp
SearchParameters parameters;
DocumentSearchResult<Hotel> results;

Console.WriteLine("Search hello entire index for hello term 'budget' and return only hello hotelName field:\n");

parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);

Console.Write("Apply a filter toohello index toofind hotels cheaper than $150 per night, ");
Console.WriteLine("and return hello hotelId and description:\n");

parameters =
    new SearchParameters()
    {
        Filter = "baseRate lt 150",
        Select = new[] { "hotelId", "description" }
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);

Console.Write("Search hello entire index, order by a specific field (lastRenovationDate) ");
Console.Write("in descending order, take hello top two results, and show only hotelName and ");
Console.WriteLine("lastRenovationDate:\n");

parameters =
    new SearchParameters()
    {
        OrderBy = new[] { "lastRenovationDate desc" },
        Select = new[] { "hotelName", "lastRenovationDate" },
        Top = 2
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);

Console.WriteLine("Search hello entire index for hello term 'motel':\n");

parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

## <a name="handle-search-results"></a><span data-ttu-id="db13c-151">Controlar os resultados da pesquisa</span><span class="sxs-lookup"><span data-stu-id="db13c-151">Handle search results</span></span>
<span data-ttu-id="db13c-152">Olá `Documents.Search` método retorna um `DocumentSearchResult` objeto que contém Olá resultados de consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="db13c-152">hello `Documents.Search` method returns a `DocumentSearchResult` object that contains hello results of hello query.</span></span> <span data-ttu-id="db13c-153">exemplo Hello na seção anterior Olá usado um método chamado `WriteDocuments` console toohello de resultados de pesquisa do toooutput hello:</span><span class="sxs-lookup"><span data-stu-id="db13c-153">hello example in hello previous section used a method called `WriteDocuments` toooutput hello search results toohello console:</span></span>

```csharp
private static void WriteDocuments(DocumentSearchResult<Hotel> searchResults)
{
    foreach (SearchResult<Hotel> result in searchResults.Results)
    {
        Console.WriteLine(result.Document);
    }

    Console.WriteLine();
}
```

<span data-ttu-id="db13c-154">Aqui está o que os resultados de saudação aparência para consultas de saudação na seção anterior hello, assumindo índice de hotéis"hello" é populado com dados de exemplo hello no [importação de dados de pesquisa do Azure usando Olá .NET SDK](search-import-data-dotnet.md):</span><span class="sxs-lookup"><span data-stu-id="db13c-154">Here is what hello results look like for hello queries in hello previous section, assuming hello "hotels" index is populated with hello sample data in [Data Import in Azure Search using hello .NET SDK](search-import-data-dotnet.md):</span></span>

```
Search hello entire index for hello term 'budget' and return only hello hotelName field:

Name: Roach Motel

Apply a filter toohello index toofind hotels cheaper than $150 per night, and return hello hotelId and description:

ID: 2   Description: Cheapest hotel in town
ID: 3   Description: Close tootown hall and hello river

Search hello entire index, order by a specific field (lastRenovationDate) in descending order, take hello top two results, and show only hotelName and lastRenovationDate:

Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

Search hello entire index for hello term 'motel':

ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
```

<span data-ttu-id="db13c-155">Olá exemplo de código acima usa os resultados da pesquisa Olá console toooutput.</span><span class="sxs-lookup"><span data-stu-id="db13c-155">hello sample code above uses hello console toooutput search results.</span></span> <span data-ttu-id="db13c-156">Da mesma forma, você precisará toodisplay resultados da pesquisa em seu próprio aplicativo.</span><span class="sxs-lookup"><span data-stu-id="db13c-156">You will likewise need toodisplay search results in your own application.</span></span> <span data-ttu-id="db13c-157">Consulte [Este exemplo no GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) para obter um exemplo de como os resultados de pesquisa toorender em um aplicativo web do ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="db13c-157">See [this sample on GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) for an example of how toorender search results in an ASP.NET MVC-based web application.</span></span>

