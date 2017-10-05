---
title: Como paginar os resultados da pesquisa na Pesquisa do Azure | Microsoft Docs
description: "Paginação na Pesquisa do Azure, um serviço de pesquisa de nuvem hospedado do Microsoft Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
ms.assetid: a0a1d315-8624-4cdf-b38e-ba12569c6fcc
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/29/2016
ms.author: heidist
ms.openlocfilehash: 1054e15a2751c53aad5dbc8054c4cec41102dee9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-page-search-results-in-azure-search"></a><span data-ttu-id="f6f69-103">Como paginar os resultados da pesquisa na Pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="f6f69-103">How to page search results in Azure Search</span></span>
<span data-ttu-id="f6f69-104">Este artigo fornece orientação sobre como usar a API REST do Serviço de Pesquisa do Azure para implementar elementos padrão da página de resultados da pesquisa, por exemplo, contagem total, recuperação de documentos, ordens de classificação e navegação.</span><span class="sxs-lookup"><span data-stu-id="f6f69-104">This article provides guidance on how to use the Azure Search Service REST API to implement standard elements of a search results page, such as total counts, document retrieval, sort orders, and navigation.</span></span>

<span data-ttu-id="f6f69-105">Em cada caso mencionado abaixo, as opções relacionadas à página que colaboram com dados ou informações para sua página de resultados da pesquisa são especificadas por meio de solicitações de [Documento de Pesquisa](http://msdn.microsoft.com/library/azure/dn798927.aspx) enviadas ao Serviço de Pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6f69-105">In every case mentioned below, page-related options that contribute data or information to your search results page are specified through the [Search Document](http://msdn.microsoft.com/library/azure/dn798927.aspx) requests sent to your Azure Search Service.</span></span> <span data-ttu-id="f6f69-106">As solicitações incluem um comando GET, um caminho e os parâmetros de consulta que informam ao serviço que está sendo solicitado, e como formular a resposta.</span><span class="sxs-lookup"><span data-stu-id="f6f69-106">Requests include a GET command, path, and query parameters that inform the service what is being requested, and how to formulate the response.</span></span>

> [!NOTE]
> <span data-ttu-id="f6f69-107">Uma solicitação válida inclui diversos elementos, como uma URL de serviço e o caminho, o verbo HTTP, `api-version` etc.</span><span class="sxs-lookup"><span data-stu-id="f6f69-107">A valid request includes a number of elements, such as a service URL and path, HTTP verb, `api-version`, and so on.</span></span> <span data-ttu-id="f6f69-108">Para resumir, recortamos os exemplos para destacar apenas a sintaxe relevante para a paginação.</span><span class="sxs-lookup"><span data-stu-id="f6f69-108">For brevity, we trimmed the examples to highlight just the syntax that is relevant to pagination.</span></span> <span data-ttu-id="f6f69-109">Confira a documentação da [API REST do Serviço de Pesquisa do Azure](http://msdn.microsoft.com/library/azure/dn798935.aspx) para obter detalhes sobre a sintaxe da solicitação.</span><span class="sxs-lookup"><span data-stu-id="f6f69-109">Please see the [Azure Search Service REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) documentation for details about request syntax.</span></span>
> 
> 

## <a name="total-hits-and-page-counts"></a><span data-ttu-id="f6f69-110">Total de ocorrências e contagens de página</span><span class="sxs-lookup"><span data-stu-id="f6f69-110">Total hits and Page Counts</span></span>
<span data-ttu-id="f6f69-111">Mostrar o número total de resultados retornados por uma consulta e, em seguida, retornar esses resultados em pedaços menores, é fundamental para praticamente todas as páginas de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="f6f69-111">Showing the total number of results returned from a query, and then returning those results in smaller chunks, is fundamental to virtually all search pages.</span></span>

![][1]

<span data-ttu-id="f6f69-112">Na Pesquisa do Azure, você deve usar os parâmetros `$count`, `$top` e `$skip` para retornar esses valores.</span><span class="sxs-lookup"><span data-stu-id="f6f69-112">In Azure Search, you use the `$count`, `$top`, and `$skip` parameters to return these values.</span></span> <span data-ttu-id="f6f69-113">O exemplo a seguir mostra um exemplo de solicitação pelo total de ocorrências, a retorna como `@OData.count`:</span><span class="sxs-lookup"><span data-stu-id="f6f69-113">The following example shows a sample request for total hits, returned as `@OData.count`:</span></span>

        GET /indexes/onlineCatalog/docs?$count=true

<span data-ttu-id="f6f69-114">Recupera documentos em grupos de 15 e também mostra o total de ocorrências, começando na primeira página:</span><span class="sxs-lookup"><span data-stu-id="f6f69-114">Retrieve documents in groups of 15, and also show the total hits, starting at the first page:</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

<span data-ttu-id="f6f69-115">A paginação de resultados exige `$top` e `$skip`, sendo que `$top` especifica quantos itens devem retornar em um lote, e `$skip` especifica quantos itens ignorar.</span><span class="sxs-lookup"><span data-stu-id="f6f69-115">Paginating results requires both `$top` and `$skip`, where `$top` specifies how many items to return in a batch, and `$skip` specifies how many items to skip.</span></span> <span data-ttu-id="f6f69-116">No exemplo a seguir, cada página mostra os próximos 15 itens, indicados por saltos incrementais no parâmetro `$skip` .</span><span class="sxs-lookup"><span data-stu-id="f6f69-116">In the following example, each page shows the next 15 items, indicated by the incremental jumps in the `$skip` parameter.</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=15&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=30&$count=true

## <a name="layout"></a><span data-ttu-id="f6f69-117">Layout</span><span class="sxs-lookup"><span data-stu-id="f6f69-117">Layout</span></span>
<span data-ttu-id="f6f69-118">Talvez você queira mostrar em uma página de resultados da pesquisa uma imagem em miniatura, um subconjunto dos campos e um link para uma página completa sobre um produto.</span><span class="sxs-lookup"><span data-stu-id="f6f69-118">On a search results page, you might want to show a thumbnail image, a subset of fields, and a link to a full product page.</span></span>

 ![][2]

<span data-ttu-id="f6f69-119">Na Pesquisa do Azure, você usaria `$select` e um comando de pesquisa para implementar essa experiência.</span><span class="sxs-lookup"><span data-stu-id="f6f69-119">In Azure Search, you would use `$select` and a lookup command to implement this experience.</span></span>

<span data-ttu-id="f6f69-120">Para retornar um subconjunto dos campos para um layout lado a lado:</span><span class="sxs-lookup"><span data-stu-id="f6f69-120">To return a subset of fields for a tiled layout:</span></span>

        GET /indexes/ onlineCatalog/docs?search=*&$select=productName,imageFile,description,price,rating 

<span data-ttu-id="f6f69-121">Arquivos de imagem e de mídia não são diretamente pesquisáveis e devem ser armazenados em outra plataforma de armazenamento, por exemplo, o armazenamento do Blob do Azure, para reduzir os custos.</span><span class="sxs-lookup"><span data-stu-id="f6f69-121">Images and media files are not directly searchable and should be stored in another storage platform, such as Azure Blob storage, to reduce costs.</span></span> <span data-ttu-id="f6f69-122">No índice e nos documentos, defina um campo que armazena o endereço da URL do conteúdo externo.</span><span class="sxs-lookup"><span data-stu-id="f6f69-122">In the index and documents, define a field that stores the URL address of the external content.</span></span> <span data-ttu-id="f6f69-123">Em seguida, use o campo como uma referência de imagem.</span><span class="sxs-lookup"><span data-stu-id="f6f69-123">You can then use the field as an image reference.</span></span> <span data-ttu-id="f6f69-124">A URL da imagem deve estar no documento.</span><span class="sxs-lookup"><span data-stu-id="f6f69-124">The URL to the image should be in the document.</span></span>

<span data-ttu-id="f6f69-125">Para recuperar uma página de descrição de produto em um evento **onClick** , use [Pesquisar Documento](http://msdn.microsoft.com/library/azure/dn798929.aspx) para passar a chave do documento que será recuperada.</span><span class="sxs-lookup"><span data-stu-id="f6f69-125">To retrieve a product description page for an **onClick** event, use [Lookup Document](http://msdn.microsoft.com/library/azure/dn798929.aspx) to pass in the key of the document to retrieve.</span></span> <span data-ttu-id="f6f69-126">O tipo de dados da chave é `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="f6f69-126">The data type of the key is `Edm.String`.</span></span> <span data-ttu-id="f6f69-127">Neste exemplo, é *246810*.</span><span class="sxs-lookup"><span data-stu-id="f6f69-127">In this example, it is *246810*.</span></span> 

        GET /indexes/onlineCatalog/docs/246810

## <a name="sort-by-relevance-rating-or-price"></a><span data-ttu-id="f6f69-128">Classificar por relevância, por classificação ou por preço</span><span class="sxs-lookup"><span data-stu-id="f6f69-128">Sort by relevance, rating, or price</span></span>
<span data-ttu-id="f6f69-129">Por padrão, as ordens de classificação normalmente usam a opção de relevância, mas é comum disponibilizar ordens de classificação alternativas para que os clientes possam reorganizar rapidamente esses resultados em uma ordem de classificação diferente.</span><span class="sxs-lookup"><span data-stu-id="f6f69-129">Sort orders often default to relevance, but it's common to make alternative sort orders readily available so that customers can quickly reshuffle existing results into a different rank order.</span></span>

 ![][3]

<span data-ttu-id="f6f69-130">Na Pesquisa do Azure, a classificação baseia-se na expressão `$orderby`, para todos os campos indexados como `"Sortable": true.`</span><span class="sxs-lookup"><span data-stu-id="f6f69-130">In Azure Search, sorting is based on the `$orderby` expression, for all fields that are indexed as `"Sortable": true.`</span></span>

<span data-ttu-id="f6f69-131">A relevância está fortemente associada a perfis de pontuação.</span><span class="sxs-lookup"><span data-stu-id="f6f69-131">Relevance is strongly associated with scoring profiles.</span></span> <span data-ttu-id="f6f69-132">Você pode usar a pontuação padrão, que depende de análise de texto e estatísticas para classificar todos os resultados, com pontuações mais altas sendo atribuídas a documentos com mais correspondências, ou correspondências mais sólidas, de um termo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="f6f69-132">You can use the default scoring, which relies on text analysis and statistics to rank order all results, with higher scores going to documents with more or stronger matches on a search term.</span></span>

<span data-ttu-id="f6f69-133">As ordens de classificação alternativas normalmente são associadas a eventos **onClick** que remetem a um método que cria a ordem de classificação.</span><span class="sxs-lookup"><span data-stu-id="f6f69-133">Alternative sort orders are typically associated with **onClick** events that call back to a method that builds the sort order.</span></span> <span data-ttu-id="f6f69-134">Por exemplo, este elemento de página:</span><span class="sxs-lookup"><span data-stu-id="f6f69-134">For example, given this page element:</span></span>

 ![][4]

<span data-ttu-id="f6f69-135">Você criaria um método que aceitasse a opção de classificação selecionada como entrada, e retornaria uma lista ordenada dos critérios associados a essa opção.</span><span class="sxs-lookup"><span data-stu-id="f6f69-135">You would create a method that accepts the selected sort option as input, and returns an ordered list for the criteria associated with that option.</span></span>

 ![][5]

> [!NOTE]
> <span data-ttu-id="f6f69-136">Embora a pontuação padrão seja suficiente para muitos cenários, recomendamos basear a relevância em um perfil personalizado de pontuação.</span><span class="sxs-lookup"><span data-stu-id="f6f69-136">While the default scoring is sufficient for many scenarios, we recommend basing relevance on a custom scoring profile instead.</span></span> <span data-ttu-id="f6f69-137">Um perfil personalizado de pontuação permite um aumento dos itens mais úteis para o seu negócio.</span><span class="sxs-lookup"><span data-stu-id="f6f69-137">A custom scoring profile gives you a way to boost items that are more beneficial to your business.</span></span> <span data-ttu-id="f6f69-138">Confira [Adicionar um perfil de pontuação](http://msdn.microsoft.com/library/azure/dn798928.aspx) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="f6f69-138">See [Add a scoring profile](http://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> 
> 
> 

## <a name="faceted-navigation"></a><span data-ttu-id="f6f69-139">Navegação facetada</span><span class="sxs-lookup"><span data-stu-id="f6f69-139">Faceted navigation</span></span>
<span data-ttu-id="f6f69-140">A navegação de pesquisa é comum em uma página de resultados, e normalmente fica na lateral ou na parte superior de uma página.</span><span class="sxs-lookup"><span data-stu-id="f6f69-140">Search navigation is common on a results page, often located at the side or top of a page.</span></span> <span data-ttu-id="f6f69-141">Na Pesquisa do Azure, a navegação facetada proporciona uma pesquisa autodirecionada com base em filtros predefinidos.</span><span class="sxs-lookup"><span data-stu-id="f6f69-141">In Azure Search, faceted navigation provides self-directed search based on predefined filters.</span></span> <span data-ttu-id="f6f69-142">Confira [Navegação facetada na Pesquisa do Azure](search-faceted-navigation.md) para mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="f6f69-142">See [Faceted navigation in Azure Search](search-faceted-navigation.md) for details.</span></span>

## <a name="filters-at-the-page-level"></a><span data-ttu-id="f6f69-143">Filtros no nível da página</span><span class="sxs-lookup"><span data-stu-id="f6f69-143">Filters at the page level</span></span>
<span data-ttu-id="f6f69-144">Se o design da solução incluir páginas de pesquisa dedicada para tipos específicos de conteúdo (por exemplo, um aplicativo de varejo online com os departamentos relacionados na parte superior da página), você poderá inserir uma expressão de filtro, junto com um evento **onClick** , para abrir uma página em um estado pré-filtrado.</span><span class="sxs-lookup"><span data-stu-id="f6f69-144">If your solution design included dedicated search pages for specific types of content (for example, an online retail application that has departments listed at the top of the page), you can insert a filter expression alongside an **onClick** event to open a page in a prefiltered state.</span></span> 

<span data-ttu-id="f6f69-145">Você pode enviar um filtro com ou sem uma expressão de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="f6f69-145">You can send a filter with or without a search expression.</span></span> <span data-ttu-id="f6f69-146">Por exemplo, a seguinte solicitação filtrará o nome da marca, retornando somente os documentos que correspondem a ele.</span><span class="sxs-lookup"><span data-stu-id="f6f69-146">For example, the following request will filter on brand name, returning only those documents that match it.</span></span>

        GET /indexes/onlineCatalog/docs?$filter=brandname eq ‘Microsoft’ and category eq ‘Games’

<span data-ttu-id="f6f69-147">Confira [Pesquisar Documentos (API de Pesquisa do Azure)](http://msdn.microsoft.com/library/azure/dn798927.aspx) para saber mais sobre expressões `$filter`.</span><span class="sxs-lookup"><span data-stu-id="f6f69-147">See [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) for more information about `$filter` expressions.</span></span>

## <a name="see-also"></a><span data-ttu-id="f6f69-148">Consulte também</span><span class="sxs-lookup"><span data-stu-id="f6f69-148">See Also</span></span>
* [<span data-ttu-id="f6f69-149">API REST do Serviço de Pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="f6f69-149">Azure Search Service REST API</span></span>](http://msdn.microsoft.com/library/azure/dn798935.aspx)
* [<span data-ttu-id="f6f69-150">Operações de índice</span><span class="sxs-lookup"><span data-stu-id="f6f69-150">Index Operations</span></span>](http://msdn.microsoft.com/library/azure/dn798918.aspx)
* [<span data-ttu-id="f6f69-151">Operações de documento.</span><span class="sxs-lookup"><span data-stu-id="f6f69-151">Document Operations</span></span>](http://msdn.microsoft.com/library/azure/dn800962.aspx)
* [<span data-ttu-id="f6f69-152">Vídeos e tutoriais sobre a Pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="f6f69-152">Video and tutorials about Azure Search</span></span>](search-video-demo-tutorial-list.md)
* [<span data-ttu-id="f6f69-153">Navegação facetada na Pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="f6f69-153">Faceted Navigation in Azure Search</span></span>](search-faceted-navigation.md)

<!--Image references-->
[1]: ./media/search-pagination-page-layout/Pages-1-Viewing1ofNResults.PNG
[2]: ./media/search-pagination-page-layout/Pages-2-Tiled.PNG
[3]: ./media/search-pagination-page-layout/Pages-3-SortBy.png
[4]: ./media/search-pagination-page-layout/Pages-4-SortbyRelevance.png
[5]: ./media/search-pagination-page-layout/Pages-5-BuildSort.png 
