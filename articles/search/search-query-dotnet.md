---
title: "Consultar um índice (API .NET - Azure Search) | Microsoft Docs"
description: "Crie uma consulta de pesquisa na Pesquisa do Azure e use parâmetros de pesquisa para filtrar e classificar os resultados da pesquisa."
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
ms.openlocfilehash: 52bd0fd4cf70401dcf881c7f28d5cd91397bb059
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="query-your-azure-search-index-using-the-net-sdk"></a><span data-ttu-id="dd8d7-103">Consultar seu índice de Pesquisa do Azure usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="dd8d7-103">Query your Azure Search index using the .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dd8d7-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="dd8d7-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="dd8d7-105">Portal</span><span class="sxs-lookup"><span data-stu-id="dd8d7-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="dd8d7-106">.NET</span><span class="sxs-lookup"><span data-stu-id="dd8d7-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="dd8d7-107">REST</span><span class="sxs-lookup"><span data-stu-id="dd8d7-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="dd8d7-108">Este artigo mostrará como consultar um índice usando o [SDK do .NET da Pesquisa do Azure](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="dd8d7-108">This article will show you how to query an index using the [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span>

<span data-ttu-id="dd8d7-109">Antes de começar este passo a passo, você já deve ter [criado um índice do Azure Search](search-what-is-an-index.md), e este já deve estar [preenchido com os dados](search-what-is-data-import.md).</span><span class="sxs-lookup"><span data-stu-id="dd8d7-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span>

> [!NOTE]
> <span data-ttu-id="dd8d7-110">Todos os códigos de exemplo neste artigo foram escritos em C#.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="dd8d7-111">Você pode encontrar o código-fonte completo [no GitHub](http://aka.ms/search-dotnet-howto).</span><span class="sxs-lookup"><span data-stu-id="dd8d7-111">You can find the full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="dd8d7-112">Você também pode ler sobre o [SDK .NET do Azure Search](search-howto-dotnet-sdk.md) para passo a passo mais detalhado do código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-112">You can also read about the [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of the sample code.</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="dd8d7-113">Identificar sua api-key de consulta do serviço de Pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="dd8d7-113">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="dd8d7-114">Agora que criou um índice de Pesquisa do Azure, você está quase pronto para emitir consultas usando o SDK do .NET.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-114">Now that you have created an Azure Search index, you are almost ready to issue queries using the .NET SDK.</span></span> <span data-ttu-id="dd8d7-115">Primeiro, você precisará obter uma das chaves da API de consulta que foram geradas para o serviço de pesquisa que provisionou.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-115">First, you will need to obtain one of the query api-keys that was generated for the search service you provisioned.</span></span> <span data-ttu-id="dd8d7-116">O SDK do .NET enviará essa chave de API em cada solicitação para o serviço.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-116">The .NET SDK will send this api-key on every request to your service.</span></span> <span data-ttu-id="dd8d7-117">Ter uma chave válida estabelece a relação de confiança, para cada solicitação, entre o aplicativo que envia a solicitação e o serviço que lida com ela.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-117">Having a valid key establishes trust, on a per request basis, between the application sending the request and the service that handles it.</span></span>

1. <span data-ttu-id="dd8d7-118">Para localizar as api-keys de seu serviço, você deve fazer logon no [portal do Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="dd8d7-118">To find your service's api-keys you can sign in to the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="dd8d7-119">Vá para a folha do serviço de Pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="dd8d7-119">Go to your Azure Search service's blade</span></span>
3. <span data-ttu-id="dd8d7-120">Clique no ícone de "Chaves"</span><span class="sxs-lookup"><span data-stu-id="dd8d7-120">Click on the "Keys" icon</span></span>

<span data-ttu-id="dd8d7-121">O serviço terá *chaves de administração* e *chaves de consulta*.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-121">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="dd8d7-122">Suas *chaves de administração* principal e secundária concedem direitos totais para todas as operações, incluindo a capacidade de gerenciar o serviço, criar e excluir índices, indexadores e fontes de dados.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-122">Your primary and secondary *admin keys* grant full rights to all operations, including the ability to manage the service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="dd8d7-123">Há duas chaves para que você possa continuar a usar a chave secundária se decidir regenerar a chave primária e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-123">There are two keys so that you can continue to use the secondary key if you decide to regenerate the primary key, and vice-versa.</span></span>
* <span data-ttu-id="dd8d7-124">As *chaves de consulta* concedem acesso somente leitura a índices e documentos e normalmente são distribuídas para aplicativos cliente que emitem solicitações de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-124">Your *query keys* grant read-only access to indexes and documents, and are typically distributed to client applications that issue search requests.</span></span>

<span data-ttu-id="dd8d7-125">Para consultar um índice, você pode usar uma de suas chaves de consulta.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-125">For the purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="dd8d7-126">As chaves de administração também podem ser usadas para consultas, mas você deve usar uma chave de consulta no código do aplicativo, já que isso segue melhor o [Princípio do privilégio mínimo](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span><span class="sxs-lookup"><span data-stu-id="dd8d7-126">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows the [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="create-an-instance-of-the-searchindexclient-class"></a><span data-ttu-id="dd8d7-127">Criar uma instância da classe SearchIndexClient</span><span class="sxs-lookup"><span data-stu-id="dd8d7-127">Create an instance of the SearchIndexClient class</span></span>
<span data-ttu-id="dd8d7-128">Para emitir consultas com o SDK do .NET da Pesquisa do Azure, você precisará criar uma instância da classe `SearchIndexClient` .</span><span class="sxs-lookup"><span data-stu-id="dd8d7-128">To issue queries with the Azure Search .NET SDK, you will need to create an instance of the `SearchIndexClient` class.</span></span> <span data-ttu-id="dd8d7-129">Essa classe tem vários construtores.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-129">This class has several constructors.</span></span> <span data-ttu-id="dd8d7-130">A classe desejada usa o nome do serviço de pesquisa, nome do índice e um objeto `SearchCredentials` como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-130">The one you want takes your search service name, index name, and a `SearchCredentials` object as parameters.</span></span> <span data-ttu-id="dd8d7-131">`SearchCredentials` encapsula sua api-key.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-131">`SearchCredentials` wraps your api-key.</span></span>

<span data-ttu-id="dd8d7-132">O código a seguir cria um `SearchIndexClient` novo para o índice "hotéis" (criado em [Como criar um índice do Azure Search usando o SDK do .NET](search-create-index-dotnet.md)) usando valores para o nome do serviço de pesquisa e a api-key armazenados no arquivo de configuração do aplicativo (`appsettings.json` em caso do [aplicativo de exemplo](http://aka.ms/search-dotnet-howto)):</span><span class="sxs-lookup"><span data-stu-id="dd8d7-132">The code below creates a new `SearchIndexClient` for the "hotels" index (created in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md)) using values for the search service name and api-key that are stored in the application's config file (`appsettings.json` in the case of the [sample application](http://aka.ms/search-dotnet-howto)):</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="dd8d7-133">`SearchIndexClient` tem uma propriedade `Documents`.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-133">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="dd8d7-134">Essa propriedade fornece todos os métodos necessários para consultar índices de Pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-134">This property provides all the methods you need to query Azure Search indexes.</span></span>

## <a name="query-your-index"></a><span data-ttu-id="dd8d7-135">Consultar o índice</span><span class="sxs-lookup"><span data-stu-id="dd8d7-135">Query your index</span></span>
<span data-ttu-id="dd8d7-136">Pesquisar com o SDK do .NET é tão simples quanto chamar o método `Documents.Search` em seu `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-136">Searching with the .NET SDK is as simple as calling the `Documents.Search` method on your `SearchIndexClient`.</span></span> <span data-ttu-id="dd8d7-137">Este método usa alguns parâmetros, incluindo o texto de pesquisa, junto com um objeto `SearchParameters` que pode ser usado para refinar mais a consulta.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-137">This method takes a few parameters, including the search text, along with a `SearchParameters` object that can be used to further refine the query.</span></span>

#### <a name="types-of-queries"></a><span data-ttu-id="dd8d7-138">Tipos de Consultas</span><span class="sxs-lookup"><span data-stu-id="dd8d7-138">Types of Queries</span></span>
<span data-ttu-id="dd8d7-139">Os dois [tipos de consulta](search-query-overview.md#types-of-queries) principais que você usará são `search` e `filter`.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-139">The two main [query types](search-query-overview.md#types-of-queries) you will use are `search` and `filter`.</span></span> <span data-ttu-id="dd8d7-140">Uma consulta `search` procura um ou mais termos em todos os campos *pesquisáveis* no índice.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-140">A `search` query searches for one or more terms in all *searchable* fields in your index.</span></span> <span data-ttu-id="dd8d7-141">Uma consulta `filter` avalia uma expressão booliana em todos os campos *filtráveis* em um índice.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-141">A `filter` query evaluates a boolean expression over all *filterable* fields in an index.</span></span>

<span data-ttu-id="dd8d7-142">As pesquisas e os filtros são executados usando o método `Documents.Search` .</span><span class="sxs-lookup"><span data-stu-id="dd8d7-142">Both searches and filters are performed using the `Documents.Search` method.</span></span> <span data-ttu-id="dd8d7-143">Uma consulta de pesquisa pode ser passada no parâmetro `searchText`, enquanto uma expressão de filtro pode ser passada na propriedade `Filter` da classe `SearchParameters`.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-143">A search query can be passed in the `searchText` parameter, while a filter expression can be passed in the `Filter` property of the `SearchParameters` class.</span></span> <span data-ttu-id="dd8d7-144">Para filtrar sem pesquisar, basta passar `"*"` para o parâmetro `searchText`.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-144">To filter without searching, just pass `"*"` for the `searchText` parameter.</span></span> <span data-ttu-id="dd8d7-145">Para pesquisar sem filtrar, deixe a propriedade `Filter` indefinida ou simplesmente não passe uma instância `SearchParameters`.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-145">To search without filtering, just leave the `Filter` property unset, or do not pass in a `SearchParameters` instance at all.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="dd8d7-146">Consultas de Exemplo</span><span class="sxs-lookup"><span data-stu-id="dd8d7-146">Example Queries</span></span>
<span data-ttu-id="dd8d7-147">O código de exemplo a seguir mostra algumas maneiras diferentes de consultar o índice "hotéis" definido em [Criar um índice de Pesquisa do Azure usando o SDK do .NET](search-create-index-dotnet.md#DefineIndex).</span><span class="sxs-lookup"><span data-stu-id="dd8d7-147">The following sample code shows a few different ways to query the "hotels" index defined in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#DefineIndex).</span></span> <span data-ttu-id="dd8d7-148">Observe que os documentos retornados com os resultados da pesquisa são instâncias da classe `Hotel` , que foi definida em [Importação de dados na Pesquisa do Azure usando o SDK do .NET](search-import-data-dotnet.md#HotelClass).</span><span class="sxs-lookup"><span data-stu-id="dd8d7-148">Note that the documents returned with the search results are instances of the `Hotel` class, which was defined in [Data Import in Azure Search using the .NET SDK](search-import-data-dotnet.md#HotelClass).</span></span> <span data-ttu-id="dd8d7-149">O código de exemplo usa um método `WriteDocuments` para enviar os resultados da pesquisa para o console.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-149">The sample code makes use of a `WriteDocuments` method to output the search results to the console.</span></span> <span data-ttu-id="dd8d7-150">Esse método é descrito na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-150">This method is described in the next section.</span></span>

```csharp
SearchParameters parameters;
DocumentSearchResult<Hotel> results;

Console.WriteLine("Search the entire index for the term 'budget' and return only the hotelName field:\n");

parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);

Console.Write("Apply a filter to the index to find hotels cheaper than $150 per night, ");
Console.WriteLine("and return the hotelId and description:\n");

parameters =
    new SearchParameters()
    {
        Filter = "baseRate lt 150",
        Select = new[] { "hotelId", "description" }
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);

Console.Write("Search the entire index, order by a specific field (lastRenovationDate) ");
Console.Write("in descending order, take the top two results, and show only hotelName and ");
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

Console.WriteLine("Search the entire index for the term 'motel':\n");

parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

## <a name="handle-search-results"></a><span data-ttu-id="dd8d7-151">Controlar os resultados da pesquisa</span><span class="sxs-lookup"><span data-stu-id="dd8d7-151">Handle search results</span></span>
<span data-ttu-id="dd8d7-152">O método `Documents.Search` retorna um objeto `DocumentSearchResult` que contém os resultados da consulta.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-152">The `Documents.Search` method returns a `DocumentSearchResult` object that contains the results of the query.</span></span> <span data-ttu-id="dd8d7-153">O exemplo na seção anterior usou um método denominado `WriteDocuments` para enviar os resultados da pesquisa para o console:</span><span class="sxs-lookup"><span data-stu-id="dd8d7-153">The example in the previous section used a method called `WriteDocuments` to output the search results to the console:</span></span>

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

<span data-ttu-id="dd8d7-154">Os resultados das consultas da seção anterior se parecem com esses, supondo que o índice "hotéis" seja preenchido com os dados de exemplo em [Importação de dados na Pesquisa do Azure usando o SDK do .NET](search-import-data-dotnet.md):</span><span class="sxs-lookup"><span data-stu-id="dd8d7-154">Here is what the results look like for the queries in the previous section, assuming the "hotels" index is populated with the sample data in [Data Import in Azure Search using the .NET SDK](search-import-data-dotnet.md):</span></span>

```
Search the entire index for the term 'budget' and return only the hotelName field:

Name: Roach Motel

Apply a filter to the index to find hotels cheaper than $150 per night, and return the hotelId and description:

ID: 2   Description: Cheapest hotel in town
ID: 3   Description: Close to town hall and the river

Search the entire index, order by a specific field (lastRenovationDate) in descending order, take the top two results, and show only hotelName and lastRenovationDate:

Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

Search the entire index for the term 'motel':

ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
```

<span data-ttu-id="dd8d7-155">O código de exemplo acima usa o console para gerar os resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-155">The sample code above uses the console to output search results.</span></span> <span data-ttu-id="dd8d7-156">Da mesma forma, você precisará exibir os resultados da pesquisa em seu próprio aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-156">You will likewise need to display search results in your own application.</span></span> <span data-ttu-id="dd8d7-157">Consulte [este exemplo no GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) de como renderizar os resultados da pesquisa em um aplicativo Web baseado no ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="dd8d7-157">See [this sample on GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) for an example of how to render search results in an ASP.NET MVC-based web application.</span></span>

