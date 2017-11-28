---
title: resultados da pesquisa de toopage de aaaHow na pesquisa do Azure | Microsoft Docs
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
ms.openlocfilehash: e3abc1ca4d5994b0a77955379081a4fcfa5a7fa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopage-search-results-in-azure-search"></a><span data-ttu-id="3d653-103">Como os resultados de pesquisa toopage na pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="3d653-103">How toopage search results in Azure Search</span></span>
<span data-ttu-id="3d653-104">Este artigo fornece orientação sobre como toouse Olá API de REST do serviço de pesquisa do Azure tooimplement elementos padrão de uma pesquisa de página de resultados, como contagens do total, recuperação de documentos, ordens de classificação e navegação.</span><span class="sxs-lookup"><span data-stu-id="3d653-104">This article provides guidance on how toouse hello Azure Search Service REST API tooimplement standard elements of a search results page, such as total counts, document retrieval, sort orders, and navigation.</span></span>

<span data-ttu-id="3d653-105">Em cada caso mencionado a seguir, relacionados à página de opções que contribuem com dados ou informações tooyour página resultados da pesquisa são especificadas por meio de saudação [pesquisar documento](http://msdn.microsoft.com/library/azure/dn798927.aspx) solicitações enviadas tooyour serviço de pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="3d653-105">In every case mentioned below, page-related options that contribute data or information tooyour search results page are specified through hello [Search Document](http://msdn.microsoft.com/library/azure/dn798927.aspx) requests sent tooyour Azure Search Service.</span></span> <span data-ttu-id="3d653-106">Solicitações incluem um comando GET, caminho e os parâmetros de consulta que informam o serviço de saudação que está sendo solicitado e como tooformulate Olá resposta.</span><span class="sxs-lookup"><span data-stu-id="3d653-106">Requests include a GET command, path, and query parameters that inform hello service what is being requested, and how tooformulate hello response.</span></span>

> [!NOTE]
> <span data-ttu-id="3d653-107">Uma solicitação válida inclui diversos elementos, como uma URL de serviço e o caminho, o verbo HTTP, `api-version` etc.</span><span class="sxs-lookup"><span data-stu-id="3d653-107">A valid request includes a number of elements, such as a service URL and path, HTTP verb, `api-version`, and so on.</span></span> <span data-ttu-id="3d653-108">Para resumir, podemos cortados Olá exemplos toohighlight Olá apenas sintaxe toopagination relevante.</span><span class="sxs-lookup"><span data-stu-id="3d653-108">For brevity, we trimmed hello examples toohighlight just hello syntax that is relevant toopagination.</span></span> <span data-ttu-id="3d653-109">Consulte Olá [API de REST do serviço de pesquisa do Azure](http://msdn.microsoft.com/library/azure/dn798935.aspx) documentação para obter detalhes sobre a sintaxe de solicitação.</span><span class="sxs-lookup"><span data-stu-id="3d653-109">Please see hello [Azure Search Service REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) documentation for details about request syntax.</span></span>
> 
> 

## <a name="total-hits-and-page-counts"></a><span data-ttu-id="3d653-110">Total de ocorrências e contagens de página</span><span class="sxs-lookup"><span data-stu-id="3d653-110">Total hits and Page Counts</span></span>
<span data-ttu-id="3d653-111">Mostrar Olá total do número de resultados retornados por uma consulta e, em seguida, retornar os resultados em partes menores, é fundamental toovirtually todas as páginas de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="3d653-111">Showing hello total number of results returned from a query, and then returning those results in smaller chunks, is fundamental toovirtually all search pages.</span></span>

![][1]

<span data-ttu-id="3d653-112">Na pesquisa do Azure, você usar Olá `$count`, `$top`, e `$skip` parâmetros tooreturn esses valores.</span><span class="sxs-lookup"><span data-stu-id="3d653-112">In Azure Search, you use hello `$count`, `$top`, and `$skip` parameters tooreturn these values.</span></span> <span data-ttu-id="3d653-113">Olá, exemplo a seguir mostra uma solicitação de exemplo para o total de acertos, retornados como `@OData.count`:</span><span class="sxs-lookup"><span data-stu-id="3d653-113">hello following example shows a sample request for total hits, returned as `@OData.count`:</span></span>

        GET /indexes/onlineCatalog/docs?$count=true

<span data-ttu-id="3d653-114">Recupere documentos em grupos de 15 e também mostra o total de acertos hello, começando na primeira página do hello:</span><span class="sxs-lookup"><span data-stu-id="3d653-114">Retrieve documents in groups of 15, and also show hello total hits, starting at hello first page:</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

<span data-ttu-id="3d653-115">Resultados de paginação requer `$top` e `$skip`, onde `$top` Especifica quantos tooreturn de itens em um lote e `$skip` Especifica quantos tooskip de itens.</span><span class="sxs-lookup"><span data-stu-id="3d653-115">Paginating results requires both `$top` and `$skip`, where `$top` specifies how many items tooreturn in a batch, and `$skip` specifies how many items tooskip.</span></span> <span data-ttu-id="3d653-116">Olá seguinte exemplo, cada página mostra Olá itens lado 15, indicadas pela saltos incremental de saudação em Olá `$skip` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3d653-116">In hello following example, each page shows hello next 15 items, indicated by hello incremental jumps in hello `$skip` parameter.</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=15&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=30&$count=true

## <a name="layout"></a><span data-ttu-id="3d653-117">Layout</span><span class="sxs-lookup"><span data-stu-id="3d653-117">Layout</span></span>
<span data-ttu-id="3d653-118">Em uma página de resultados de pesquisa, talvez você queira tooshow uma imagem em miniatura, um subconjunto de campos e uma página do link tooa completa do produto.</span><span class="sxs-lookup"><span data-stu-id="3d653-118">On a search results page, you might want tooshow a thumbnail image, a subset of fields, and a link tooa full product page.</span></span>

 ![][2]

<span data-ttu-id="3d653-119">Pesquisa do Azure, você usaria `$select` e uma pesquisa de comando tooimplement essa experiência.</span><span class="sxs-lookup"><span data-stu-id="3d653-119">In Azure Search, you would use `$select` and a lookup command tooimplement this experience.</span></span>

<span data-ttu-id="3d653-120">tooreturn um subconjunto de campos para um layout lado a lado:</span><span class="sxs-lookup"><span data-stu-id="3d653-120">tooreturn a subset of fields for a tiled layout:</span></span>

        GET /indexes/ onlineCatalog/docs?search=*&$select=productName,imageFile,description,price,rating 

<span data-ttu-id="3d653-121">Arquivos de mídia e imagens não são diretamente pesquisáveis e devem ser armazenados em outra plataforma de armazenamento, como o armazenamento de BLOBs do Azure, os custos de tooreduce.</span><span class="sxs-lookup"><span data-stu-id="3d653-121">Images and media files are not directly searchable and should be stored in another storage platform, such as Azure Blob storage, tooreduce costs.</span></span> <span data-ttu-id="3d653-122">No índice hello e documentos, defina um campo que armazena o endereço de URL de saudação do conteúdo externo hello.</span><span class="sxs-lookup"><span data-stu-id="3d653-122">In hello index and documents, define a field that stores hello URL address of hello external content.</span></span> <span data-ttu-id="3d653-123">Em seguida, você pode usar o campo hello como uma referência de imagem.</span><span class="sxs-lookup"><span data-stu-id="3d653-123">You can then use hello field as an image reference.</span></span> <span data-ttu-id="3d653-124">imagem de toohello URL Olá deve estar no documento hello.</span><span class="sxs-lookup"><span data-stu-id="3d653-124">hello URL toohello image should be in hello document.</span></span>

<span data-ttu-id="3d653-125">tooretrieve uma descrição do produto da página para um **onClick** evento, use [pesquisar documento](http://msdn.microsoft.com/library/azure/dn798929.aspx) toopass na chave de saudação do hello tooretrieve de documento.</span><span class="sxs-lookup"><span data-stu-id="3d653-125">tooretrieve a product description page for an **onClick** event, use [Lookup Document](http://msdn.microsoft.com/library/azure/dn798929.aspx) toopass in hello key of hello document tooretrieve.</span></span> <span data-ttu-id="3d653-126">saudação de tipo de dados da chave de saudação é `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="3d653-126">hello data type of hello key is `Edm.String`.</span></span> <span data-ttu-id="3d653-127">Neste exemplo, é *246810*.</span><span class="sxs-lookup"><span data-stu-id="3d653-127">In this example, it is *246810*.</span></span> 

        GET /indexes/onlineCatalog/docs/246810

## <a name="sort-by-relevance-rating-or-price"></a><span data-ttu-id="3d653-128">Classificar por relevância, por classificação ou por preço</span><span class="sxs-lookup"><span data-stu-id="3d653-128">Sort by relevance, rating, or price</span></span>
<span data-ttu-id="3d653-129">Ordens de classificação geralmente padrão toorelevance, mas é comum ordens de classificação alternativa de toomake prontamente disponíveis para que os clientes podem rapidamente rearranjas essas resultados existentes em uma ordem de classificação diferente.</span><span class="sxs-lookup"><span data-stu-id="3d653-129">Sort orders often default toorelevance, but it's common toomake alternative sort orders readily available so that customers can quickly reshuffle existing results into a different rank order.</span></span>

 ![][3]

<span data-ttu-id="3d653-130">Na pesquisa do Azure, a classificação é baseada em Olá `$orderby` expressão para todos os campos são indexados como`"Sortable": true.`</span><span class="sxs-lookup"><span data-stu-id="3d653-130">In Azure Search, sorting is based on hello `$orderby` expression, for all fields that are indexed as `"Sortable": true.`</span></span>

<span data-ttu-id="3d653-131">A relevância está fortemente associada a perfis de pontuação.</span><span class="sxs-lookup"><span data-stu-id="3d653-131">Relevance is strongly associated with scoring profiles.</span></span> <span data-ttu-id="3d653-132">Você pode usar saudação padrão de pontuação, que se baseia em ordem de toorank de análise e estatísticas de texto todos os resultados com pontuações mais altas toodocuments com mais ou mais correspondências um termo de pesquisa em andamento.</span><span class="sxs-lookup"><span data-stu-id="3d653-132">You can use hello default scoring, which relies on text analysis and statistics toorank order all results, with higher scores going toodocuments with more or stronger matches on a search term.</span></span>

<span data-ttu-id="3d653-133">Ordens de classificação alternativa normalmente estão associadas **onClick** eventos que o retorno de chamada tooa método que cria a ordem de classificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d653-133">Alternative sort orders are typically associated with **onClick** events that call back tooa method that builds hello sort order.</span></span> <span data-ttu-id="3d653-134">Por exemplo, este elemento de página:</span><span class="sxs-lookup"><span data-stu-id="3d653-134">For example, given this page element:</span></span>

 ![][4]

<span data-ttu-id="3d653-135">Você deve criar um método que aceita a opção de classificação de saudação selecionada como entrada e retorna uma lista ordenada para critérios de saudação associados a essa opção.</span><span class="sxs-lookup"><span data-stu-id="3d653-135">You would create a method that accepts hello selected sort option as input, and returns an ordered list for hello criteria associated with that option.</span></span>

 ![][5]

> [!NOTE]
> <span data-ttu-id="3d653-136">Enquanto a pontuação do saudação padrão é suficiente para muitos cenários, é recomendável baseando relevantes em um perfil de pontuação personalizado em vez disso.</span><span class="sxs-lookup"><span data-stu-id="3d653-136">While hello default scoring is sufficient for many scenarios, we recommend basing relevance on a custom scoring profile instead.</span></span> <span data-ttu-id="3d653-137">Um perfil de pontuação personalizado oferece uma forma como os itens tooboost que são mais benéfico tooyour para os negócios.</span><span class="sxs-lookup"><span data-stu-id="3d653-137">A custom scoring profile gives you a way tooboost items that are more beneficial tooyour business.</span></span> <span data-ttu-id="3d653-138">Confira [Adicionar um perfil de pontuação](http://msdn.microsoft.com/library/azure/dn798928.aspx) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="3d653-138">See [Add a scoring profile](http://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> 
> 
> 

## <a name="faceted-navigation"></a><span data-ttu-id="3d653-139">Navegação facetada</span><span class="sxs-lookup"><span data-stu-id="3d653-139">Faceted navigation</span></span>
<span data-ttu-id="3d653-140">Navegação de pesquisa é comum em uma página de resultados, geralmente localizada no lado de saudação ou superior de uma página.</span><span class="sxs-lookup"><span data-stu-id="3d653-140">Search navigation is common on a results page, often located at hello side or top of a page.</span></span> <span data-ttu-id="3d653-141">Na Pesquisa do Azure, a navegação facetada proporciona uma pesquisa autodirecionada com base em filtros predefinidos.</span><span class="sxs-lookup"><span data-stu-id="3d653-141">In Azure Search, faceted navigation provides self-directed search based on predefined filters.</span></span> <span data-ttu-id="3d653-142">Confira [Navegação facetada na Pesquisa do Azure](search-faceted-navigation.md) para mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="3d653-142">See [Faceted navigation in Azure Search](search-faceted-navigation.md) for details.</span></span>

## <a name="filters-at-hello-page-level"></a><span data-ttu-id="3d653-143">Filtros no nível de página Olá</span><span class="sxs-lookup"><span data-stu-id="3d653-143">Filters at hello page level</span></span>
<span data-ttu-id="3d653-144">Se seu design de solução incluído páginas de pesquisa dedicado para tipos específicos de conteúdo (por exemplo, um aplicativo de varejo online que tem departamentos listados na parte superior de saudação da página Olá), você pode inserir uma expressão de filtro junto com um **onClick** evento tooopen uma página em um estado pré-filtrada.</span><span class="sxs-lookup"><span data-stu-id="3d653-144">If your solution design included dedicated search pages for specific types of content (for example, an online retail application that has departments listed at hello top of hello page), you can insert a filter expression alongside an **onClick** event tooopen a page in a prefiltered state.</span></span> 

<span data-ttu-id="3d653-145">Você pode enviar um filtro com ou sem uma expressão de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="3d653-145">You can send a filter with or without a search expression.</span></span> <span data-ttu-id="3d653-146">Por exemplo, hello solicitação a seguir filtra em nome de marca, retornando somente os documentos que correspondem a ele.</span><span class="sxs-lookup"><span data-stu-id="3d653-146">For example, hello following request will filter on brand name, returning only those documents that match it.</span></span>

        GET /indexes/onlineCatalog/docs?$filter=brandname eq ‘Microsoft’ and category eq ‘Games’

<span data-ttu-id="3d653-147">Confira [Pesquisar Documentos (API de Pesquisa do Azure)](http://msdn.microsoft.com/library/azure/dn798927.aspx) para saber mais sobre expressões `$filter`.</span><span class="sxs-lookup"><span data-stu-id="3d653-147">See [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) for more information about `$filter` expressions.</span></span>

## <a name="see-also"></a><span data-ttu-id="3d653-148">Consulte também</span><span class="sxs-lookup"><span data-stu-id="3d653-148">See Also</span></span>
* [<span data-ttu-id="3d653-149">API REST do Serviço de Pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="3d653-149">Azure Search Service REST API</span></span>](http://msdn.microsoft.com/library/azure/dn798935.aspx)
* [<span data-ttu-id="3d653-150">Operações de índice</span><span class="sxs-lookup"><span data-stu-id="3d653-150">Index Operations</span></span>](http://msdn.microsoft.com/library/azure/dn798918.aspx)
* [<span data-ttu-id="3d653-151">Operações de documento.</span><span class="sxs-lookup"><span data-stu-id="3d653-151">Document Operations</span></span>](http://msdn.microsoft.com/library/azure/dn800962.aspx)
* [<span data-ttu-id="3d653-152">Vídeos e tutoriais sobre a Pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="3d653-152">Video and tutorials about Azure Search</span></span>](search-video-demo-tutorial-list.md)
* [<span data-ttu-id="3d653-153">Navegação facetada na Pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="3d653-153">Faceted Navigation in Azure Search</span></span>](search-faceted-navigation.md)

<!--Image references-->
[1]: ./media/search-pagination-page-layout/Pages-1-Viewing1ofNResults.PNG
[2]: ./media/search-pagination-page-layout/Pages-2-Tiled.PNG
[3]: ./media/search-pagination-page-layout/Pages-3-SortBy.png
[4]: ./media/search-pagination-page-layout/Pages-4-SortbyRelevance.png
[5]: ./media/search-pagination-page-layout/Pages-5-BuildSort.png 
