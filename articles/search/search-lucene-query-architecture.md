---
title: Arquitetura do mecanismo de pesquisa de texto completo (Lucene) no Azure Search | Microsoft Docs
description: "Explicação dos conceitos de recuperação de documento e processamento de consulta do Lucene para pesquisa de texto completo, relacionada ao Azure Search."
services: search
manager: jhubbard
author: yahnoosh
documentationcenter: 
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/06/2017
ms.author: jlembicz
ms.openlocfilehash: 9b7adf78271407963ed1d4b34a7760d707b5fc3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-full-text-search-works-in-azure-search"></a><span data-ttu-id="72f54-103">Como funciona a pesquisa de texto completo no Azure Search</span><span class="sxs-lookup"><span data-stu-id="72f54-103">How full text search works in Azure Search</span></span>

<span data-ttu-id="72f54-104">Este artigo é para desenvolvedores que precisam de uma compreensão mais profunda de como a pesquisa de texto completo do Lucene funciona no Azure Search.</span><span class="sxs-lookup"><span data-stu-id="72f54-104">This article is for developers who need a deeper understanding of how Lucene full text search works in Azure Search.</span></span> <span data-ttu-id="72f54-105">Para consultas de texto, o Azure Search fornecerá perfeitamente os resultados esperados na maioria dos cenários, mas, ocasionalmente, você pode obter um resultado que pode parecer "estranho".</span><span class="sxs-lookup"><span data-stu-id="72f54-105">For text queries, Azure Search will seamlessly deliver expected results in most scenarios, but occasionally you might get a result that seems "off" somehow.</span></span> <span data-ttu-id="72f54-106">Nessas situações, ter um plano de fundo nos quatro estágios da execução da consulta do Lucene (análise léxica e análise da consulta, correspondência de documentos e pontuação) pode ajudá-lo a identificar alterações específicas para parâmetros de consulta ou a configuração de índice que proporcionará o resultado desejado.</span><span class="sxs-lookup"><span data-stu-id="72f54-106">In these situations, having a background in the four stages of Lucene query execution (query parsing, lexical analysis, document matching, scoring) can help you identify specific changes to query parameters or index configuration that will deliver the desired outcome.</span></span> 

> [!Note] 
> <span data-ttu-id="72f54-107">O Azure Search usa o Lucene para pesquisa de texto completo, mas a integração do Lucene não é completa.</span><span class="sxs-lookup"><span data-stu-id="72f54-107">Azure Search uses Lucene for full text search, but Lucene integration is not exhaustive.</span></span> <span data-ttu-id="72f54-108">Vamos seletivamente expor e estender a funcionalidade do Lucene para habilitar os cenários importantes para o Azure Search.</span><span class="sxs-lookup"><span data-stu-id="72f54-108">We selectively expose and extend Lucene functionality to enable the scenarios important to Azure Search.</span></span> 

## <a name="architecture-overview-and-diagram"></a><span data-ttu-id="72f54-109">Diagrama e visão geral da arquitetura</span><span class="sxs-lookup"><span data-stu-id="72f54-109">Architecture overview and diagram</span></span>

<span data-ttu-id="72f54-110">O processamento de uma consulta de pesquisa de texto completo começa com a análise do texto da consulta para extrair os termos de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="72f54-110">Processing a full text search query starts with parsing the query text to extract search terms.</span></span> <span data-ttu-id="72f54-111">O mecanismo de pesquisa usa um índice para recuperar documentos com os termos correspondentes.</span><span class="sxs-lookup"><span data-stu-id="72f54-111">The search engine uses an index to retrieve documents with matching terms.</span></span> <span data-ttu-id="72f54-112">Os termos de consulta individual, às vezes, são divididos e reconstituídos em novos formulários para obter uma rede mais ampla sobre o que poderia ser considerado como uma possível correspondência.</span><span class="sxs-lookup"><span data-stu-id="72f54-112">Individual query terms are sometimes broken down and reconstituted into new forms to cast a broader net over what could be considered as a potential match.</span></span> <span data-ttu-id="72f54-113">Um conjunto de resultados é classificado por uma pontuação de relevância atribuída a cada documento correspondente individual.</span><span class="sxs-lookup"><span data-stu-id="72f54-113">A result set is then sorted by a relevance score assigned to each individual matching document.</span></span> <span data-ttu-id="72f54-114">Aqueles no topo da lista com a classificação são retornados para o aplicativo de chamada.</span><span class="sxs-lookup"><span data-stu-id="72f54-114">Those at the top of the ranked list are returned to the calling application.</span></span>

<span data-ttu-id="72f54-115">A execução de consulta redefinida, tem quatro fases:</span><span class="sxs-lookup"><span data-stu-id="72f54-115">Restated, query execution has four stages:</span></span> 

1. <span data-ttu-id="72f54-116">Análise da consulta</span><span class="sxs-lookup"><span data-stu-id="72f54-116">Query parsing</span></span> 
2. <span data-ttu-id="72f54-117">Análise léxica</span><span class="sxs-lookup"><span data-stu-id="72f54-117">Lexical analysis</span></span> 
3. <span data-ttu-id="72f54-118">Recuperação de documentos</span><span class="sxs-lookup"><span data-stu-id="72f54-118">Document retrieval</span></span> 
4. <span data-ttu-id="72f54-119">Pontuação</span><span class="sxs-lookup"><span data-stu-id="72f54-119">Scoring</span></span> 

<span data-ttu-id="72f54-120">O diagrama a seguir ilustra os componentes usados para processar uma solicitação de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="72f54-120">The diagram below illustrates the components used to process a search request.</span></span> 

 ![Diagrama da arquitetura de consulta do Lucene no Azure Search][1]


| <span data-ttu-id="72f54-122">Principais componentes</span><span class="sxs-lookup"><span data-stu-id="72f54-122">Key components</span></span> | <span data-ttu-id="72f54-123">Descrição funcional</span><span class="sxs-lookup"><span data-stu-id="72f54-123">Functional description</span></span> | 
|----------------|------------------------|
|<span data-ttu-id="72f54-124">**Analisadores de consulta**</span><span class="sxs-lookup"><span data-stu-id="72f54-124">**Query parsers**</span></span> | <span data-ttu-id="72f54-125">Separam os termos de consulta de operadores de consulta e criam a estrutura da consulta (uma árvore de consulta) a ser enviada para o mecanismo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="72f54-125">Separate query terms from query operators and create the query structure (a query tree) to be sent to the search engine.</span></span> |
|<span data-ttu-id="72f54-126">**Analisadores**</span><span class="sxs-lookup"><span data-stu-id="72f54-126">**Analyzers**</span></span> | <span data-ttu-id="72f54-127">Executam a análise léxica dos termos de consulta.</span><span class="sxs-lookup"><span data-stu-id="72f54-127">Perform lexical analysis on query terms.</span></span> <span data-ttu-id="72f54-128">Esse processo pode envolver a transformação, remoção ou expansão dos termos de consulta.</span><span class="sxs-lookup"><span data-stu-id="72f54-128">This process can involve transforming, removing, or expanding of query terms.</span></span> |
|<span data-ttu-id="72f54-129">**Índice**</span><span class="sxs-lookup"><span data-stu-id="72f54-129">**Index**</span></span> | <span data-ttu-id="72f54-130">Uma estrutura de dados eficiente usada para armazenar e organizar termos pesquisáveis extraídos de documentos indexados.</span><span class="sxs-lookup"><span data-stu-id="72f54-130">An efficient data structure used to store and organize searchable terms extracted from indexed documents.</span></span> |
|<span data-ttu-id="72f54-131">**Mecanismo de pesquisa**</span><span class="sxs-lookup"><span data-stu-id="72f54-131">**Search engine**</span></span> | <span data-ttu-id="72f54-132">Recupera e atribui uma pontuação aos documentos correspondentes com base no conteúdo do índice invertido.</span><span class="sxs-lookup"><span data-stu-id="72f54-132">Retrieves and scores matching documents based on the contents of the inverted index.</span></span> |

## <a name="anatomy-of-a-search-request"></a><span data-ttu-id="72f54-133">Anatomia de uma solicitação de pesquisa</span><span class="sxs-lookup"><span data-stu-id="72f54-133">Anatomy of a search request</span></span>

<span data-ttu-id="72f54-134">Uma solicitação de pesquisa é uma especificação completa do que deve ser retornado em um conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="72f54-134">A search request is a complete specification of what should be returned in a result set.</span></span> <span data-ttu-id="72f54-135">Na forma mais simples, é uma consulta vazia sem critérios de nenhum tipo.</span><span class="sxs-lookup"><span data-stu-id="72f54-135">In simplest form, it is an empty query with no criteria of any kind.</span></span> <span data-ttu-id="72f54-136">Um exemplo mais realista inclui parâmetros, vários termos de consulta, talvez com escopo para determinados campos, com possivelmente uma expressão de filtro e as regras de ordenação.</span><span class="sxs-lookup"><span data-stu-id="72f54-136">A more realistic example includes parameters, several query terms, perhaps scoped to certain fields, with possibly a filter expression and ordering rules.</span></span>  

<span data-ttu-id="72f54-137">O exemplo a seguir é uma solicitação de pesquisa que você pode enviar ao Azure Search usando a [API REST](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span><span class="sxs-lookup"><span data-stu-id="72f54-137">The following example is a search request you might send to Azure Search using the [REST API](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span></span>  

~~~~
POST /indexes/hotels/docs/search?api-version=2016-09-01 
{  
    "search": "Spacious, air-condition* +\"Ocean view\"",  
    "searchFields": "description, title",  
    "searchMode": "any",
    "filter": "price ge 60 and price lt 300",  
    "orderby": "geo.distance(location, geography'POINT(-159.476235 22.227659)')", 
    "queryType": "full" 
 } 
~~~~

<span data-ttu-id="72f54-138">Para essa solicitação, o mecanismo de pesquisa faz o seguinte:</span><span class="sxs-lookup"><span data-stu-id="72f54-138">For this request, the search engine does the following:</span></span>

1. <span data-ttu-id="72f54-139">Filtra os documentos em que o preço é pelo menos US $60 e menor que US $300.</span><span class="sxs-lookup"><span data-stu-id="72f54-139">Filters out documents where the price is at least $60 and less than $300.</span></span>
2. <span data-ttu-id="72f54-140">Executa a consulta.</span><span class="sxs-lookup"><span data-stu-id="72f54-140">Executes the query.</span></span> <span data-ttu-id="72f54-141">Neste exemplo, a consulta de pesquisa consiste de frases e termos: `"Spacious, air-condition* +\"Ocean view\""` (os usuários normalmente não inserem pontuação, mas incluí-la no exemplo permite explicar como os analisadores tratam a pontuação).</span><span class="sxs-lookup"><span data-stu-id="72f54-141">In this example, the search query consists of phrases and terms: `"Spacious, air-condition* +\"Ocean view\""` (users typically don't enter punctuation, but including it in the example allows us to explain how analyzers handle it).</span></span> <span data-ttu-id="72f54-142">Para essa consulta, o mecanismo de pesquisa examina a descrição e os campos de título especificados em `searchFields` para documentos que contenham "Vista para o mar", além do termo "espaçoso" ou em termos que começam com o prefixo "ar-condicio".</span><span class="sxs-lookup"><span data-stu-id="72f54-142">For this query, the search engine scans the description and title fields specified in `searchFields` for documents that contain "Ocean view", and additionally on the term "spacious", or on terms that start with the prefix "air-condition".</span></span> <span data-ttu-id="72f54-143">O parâmetro `searchMode` é usado para corresponder a qualquer termo (padrão) ou todos eles, para casos em que um termo não for explicitamente solicitado (`+`).</span><span class="sxs-lookup"><span data-stu-id="72f54-143">The `searchMode` parameter is used to match on any term (default) or all of them, for cases where a term is not explicitly required (`+`).</span></span>
3. <span data-ttu-id="72f54-144">Ordena o conjunto resultante de hotéis por proximidade de uma localização geográfica indicada e retorna para o aplicativo de chamada.</span><span class="sxs-lookup"><span data-stu-id="72f54-144">Orders the resulting set of hotels by proximity to a given geography location, and then returned to the calling application.</span></span> 

<span data-ttu-id="72f54-145">A maior parte deste artigo é sobre o processamento da *consulta da pesquisa*: `"Spacious, air-condition* +\"Ocean view\""`.</span><span class="sxs-lookup"><span data-stu-id="72f54-145">The majority of this article is about processing of the *search query*: `"Spacious, air-condition* +\"Ocean view\""`.</span></span> <span data-ttu-id="72f54-146">Filtragem e ordenação estão fora do escopo.</span><span class="sxs-lookup"><span data-stu-id="72f54-146">Filtering and ordering are out of scope.</span></span> <span data-ttu-id="72f54-147">Para obter mais informações, consulte as [documentação de referência da API de pesquisa](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span><span class="sxs-lookup"><span data-stu-id="72f54-147">For more information, see the [Search API reference documentation](https://docs.microsoft.com/rest/api/searchservice/search-documents).</span></span>

<a name="stage1"></a>
## <a name="stage-1-query-parsing"></a><span data-ttu-id="72f54-148">Estágio 1: Análise da consulta</span><span class="sxs-lookup"><span data-stu-id="72f54-148">Stage 1: Query parsing</span></span> 

<span data-ttu-id="72f54-149">Conforme observado, a cadeia de caracteres de consulta é a primeira linha da solicitação:</span><span class="sxs-lookup"><span data-stu-id="72f54-149">As noted, the query string is the first line of the request:</span></span> 

~~~~
 "search": "Spacious, air-condition* +\"Ocean view\"", 
~~~~

<span data-ttu-id="72f54-150">O analisador de consulta separa os operadores (como `*` e `+` no exemplo) dos termos de pesquisa e desconstrói a consulta de pesquisa em *subconsultas* de um tipo com suporte:</span><span class="sxs-lookup"><span data-stu-id="72f54-150">The query parser separates operators (such as `*` and `+` in the example) from search terms, and deconstructs the search query into *subqueries* of a supported type:</span></span> 

+ <span data-ttu-id="72f54-151">*consulta de termo* para termos independentes (espaçoso, por exemplo)</span><span class="sxs-lookup"><span data-stu-id="72f54-151">*term query* for standalone terms (like spacious)</span></span>
+ <span data-ttu-id="72f54-152">*consulta de frase* para termos entre aspas (vista para o mar, por exemplo)</span><span class="sxs-lookup"><span data-stu-id="72f54-152">*phrase query* for quoted terms (like ocean view)</span></span>
+ <span data-ttu-id="72f54-153">*consulta de prefixo* por termos seguidos por um operador de prefixo `*` (ar-condicio, por exemplo)</span><span class="sxs-lookup"><span data-stu-id="72f54-153">*prefix query* for terms followed by a prefix operator `*` (like air-condition)</span></span>

<span data-ttu-id="72f54-154">Para obter uma lista completa dos tipos de consulta com suporte, consulte [sintaxe da consulta do Lucene](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)</span><span class="sxs-lookup"><span data-stu-id="72f54-154">For a full list of supported query types see [Lucene query sytnax](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)</span></span>

<span data-ttu-id="72f54-155">Os operadores associados com uma subconsulta determinam se a consulta deve ser obrigatoriamente satisfeita ou não para um documento ser considerado uma correspondência.</span><span class="sxs-lookup"><span data-stu-id="72f54-155">Operators associated with a subquery determine whether the query "must be" or "should be" satisfied in order for a document to be considered a match.</span></span> <span data-ttu-id="72f54-156">Por exemplo, `+"Ocean view"` é "obrigatória" devido ao operador `+`.</span><span class="sxs-lookup"><span data-stu-id="72f54-156">For example, `+"Ocean view"` is "must" due to the `+` operator.</span></span> 

<span data-ttu-id="72f54-157">O analisador de consulta reestrutura as subconsultas em uma *árvore de consulta* (uma estrutura interna que representa a consulta) passada para o mecanismo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="72f54-157">The query parser restructures the subqueries into a *query tree* (an internal structure representing the query) it passes on to the search engine.</span></span> <span data-ttu-id="72f54-158">No primeiro estágio da análise de consulta, a árvore de consulta se parece com isto.</span><span class="sxs-lookup"><span data-stu-id="72f54-158">In the first stage of query parsing, the query tree looks like this.</span></span>  

 ![Booliano consulta modo de pesquisa qualquer][2]

### <a name="supported-parsers-simple-and-full-lucene"></a><span data-ttu-id="72f54-160">Analisadores com suporte: simples e Lucena completa</span><span class="sxs-lookup"><span data-stu-id="72f54-160">Supported parsers: Simple and Full Lucene</span></span> 

 <span data-ttu-id="72f54-161">O Azure Search apresenta duas linguagens de consulta diferentes, `simple` (padrão) e `full`.</span><span class="sxs-lookup"><span data-stu-id="72f54-161">Azure Search exposes two different query languages, `simple` (default) and `full`.</span></span> <span data-ttu-id="72f54-162">Ao definir o parâmetro `queryType` com sua solicitação de pesquisa, você informa ao analisador de consulta a linguagem de consulta que você escolheu para que ele saiba como interpretar os operadores e a sintaxe.</span><span class="sxs-lookup"><span data-stu-id="72f54-162">By setting the `queryType` parameter with your search request, you tell the query parser which query language you choose so that it knows how to interpret the operators and syntax.</span></span> <span data-ttu-id="72f54-163">A [linguagem de consulta simples](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) é intuitiva e robusta, geralmente adequada para interpretar a entrada do usuário conforme inserida, sem processamento no lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="72f54-163">The [Simple query langauge](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) is intuitive and robust, often suitable to interpret user input as-is without client-side processing.</span></span> <span data-ttu-id="72f54-164">Ela oferece suporte a operadores de consulta familiares de mecanismos de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="72f54-164">It supports query operators familiar from web search engines.</span></span> <span data-ttu-id="72f54-165">A [linguagem de consulta Lucene completa](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), que você obtém definindo `queryType=full`, estende a linguagem de consulta simples padrão, adicionando suporte para mais operadores e tipos de consulta como caractere curinga, difusa, regex e consultas com escopo de campo.</span><span class="sxs-lookup"><span data-stu-id="72f54-165">The [Full Lucene query language](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), which you get by setting `queryType=full`, extends the default Simple query language by adding support for more operators and query types like wildcard, fuzzy, regex, and field-scoped queries.</span></span> <span data-ttu-id="72f54-166">Por exemplo, uma expressão regular enviada na sintaxe de consulta simples será interpretada como uma cadeia de caracteres de consulta e não é uma expressão.</span><span class="sxs-lookup"><span data-stu-id="72f54-166">For example, a regular expression sent in Simple query syntax would be interpreted as a query string and not an expression.</span></span> <span data-ttu-id="72f54-167">A solicitação de exemplo neste artigo usa a linguagem de consulta Lucene completa.</span><span class="sxs-lookup"><span data-stu-id="72f54-167">The example request in this article uses the Full Lucene query language.</span></span>

### <a name="impact-of-searchmode-on-the-parser"></a><span data-ttu-id="72f54-168">Impacto do modo de pesquisa no analisador</span><span class="sxs-lookup"><span data-stu-id="72f54-168">Impact of searchMode on the parser</span></span> 

<span data-ttu-id="72f54-169">Outro parâmetro de solicitação de pesquisa que afeta a análise é o parâmetro `searchMode`.</span><span class="sxs-lookup"><span data-stu-id="72f54-169">Another search request parameter that affects parsing is the `searchMode` parameter.</span></span> <span data-ttu-id="72f54-170">Ele controla o operador padrão para consultas boolianas: qualquer (padrão) ou todos.</span><span class="sxs-lookup"><span data-stu-id="72f54-170">It controls the default operator for Boolean queries: any (default) or all.</span></span>  

<span data-ttu-id="72f54-171">Quando `searchMode=any`, que é o padrão, o delimitador de espaço entre espaçoso e ar-condicio é OR (`||`), tornando o texto da consulta de exemplo equivalente a:</span><span class="sxs-lookup"><span data-stu-id="72f54-171">When `searchMode=any`, which is the default, the space delimiter between spacious and air-condition is OR (`||`), making the sample query text equivalent to:</span></span> 

~~~~
Spacious,||air-condition*+"Ocean view" 
~~~~

<span data-ttu-id="72f54-172">Operadores explícitos, como `+` em `+"Ocean view"`, não são ambíguos na construção de consulta booliana (o termo *deve* corresponder).</span><span class="sxs-lookup"><span data-stu-id="72f54-172">Explicit operators, such as `+` in `+"Ocean view"`, are unambiguous in boolean query construction (the term *must* match).</span></span> <span data-ttu-id="72f54-173">Menos óbvio é como interpretar os demais termos: espaçoso e ar-condicio.</span><span class="sxs-lookup"><span data-stu-id="72f54-173">Less obvious is how to interpret the remaining terms: spacious and air-condition.</span></span> <span data-ttu-id="72f54-174">O mecanismo de pesquisa deve localizar correspondências para vista para o mar *e* espaçoso *e* ar-condicio?</span><span class="sxs-lookup"><span data-stu-id="72f54-174">Should the search engine find matches on ocean view *and* spacious *and* air-condition?</span></span> <span data-ttu-id="72f54-175">Ou deve encontrar vista para o mar mais *qualquer um* dos demais termos?</span><span class="sxs-lookup"><span data-stu-id="72f54-175">Or should it find ocean view plus *either one* of the remaining terms?</span></span> 

<span data-ttu-id="72f54-176">Por padrão (`searchMode=any`), o mecanismo de pesquisa assume a interpretação mais ampla.</span><span class="sxs-lookup"><span data-stu-id="72f54-176">By default (`searchMode=any`), the search engine assumes the broader interpretation.</span></span> <span data-ttu-id="72f54-177">Cada campo *deve* ter uma correspondência, refletindo a semântica de "ou".</span><span class="sxs-lookup"><span data-stu-id="72f54-177">Either field *should* be matched, reflecting "or" semantics.</span></span> <span data-ttu-id="72f54-178">A árvore de consulta inicial ilustrada anteriormente, com as duas operações de “não obrigatório”, mostra o padrão.</span><span class="sxs-lookup"><span data-stu-id="72f54-178">The initial query tree illustrated previously, with the two "should" operations, shows the default.</span></span>  

<span data-ttu-id="72f54-179">Suponha que agora definimos `searchMode=all`.</span><span class="sxs-lookup"><span data-stu-id="72f54-179">Suppose that we now set `searchMode=all`.</span></span> <span data-ttu-id="72f54-180">Nesse caso, o espaço é interpretado como uma operação "e".</span><span class="sxs-lookup"><span data-stu-id="72f54-180">In this case, the space is interpreted as an "and" operation.</span></span> <span data-ttu-id="72f54-181">Cada um dos demais termos deve estar presente no documento para ser qualificado como uma correspondência.</span><span class="sxs-lookup"><span data-stu-id="72f54-181">Each of the remaining terms must both be present in the document to qualify as a match.</span></span> <span data-ttu-id="72f54-182">O exemplo de consulta resultante será interpretado da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="72f54-182">The resulting sample query would be interpreted as follows:</span></span> 

~~~~
+Spacious,+air-condition*+"Ocean view"  
~~~~

<span data-ttu-id="72f54-183">Uma árvore de consulta modificada para esta consulta seria a seguinte, onde um documento correspondente é a interseção de todas as três subconsultas:</span><span class="sxs-lookup"><span data-stu-id="72f54-183">A modified query tree for this query would be as follows, where a matching document is the intersection of all three subqueries:</span></span> 

 ![Booliano consulta modo de pesquisa todos][3]

> [!Note] 
> <span data-ttu-id="72f54-185">Escolher `searchMode=any` em vez de `searchMode=all` é uma decisão melhor ao executar consultas representativas.</span><span class="sxs-lookup"><span data-stu-id="72f54-185">Choosing `searchMode=any` over `searchMode=all` is a decision best arrived at by running representative queries.</span></span> <span data-ttu-id="72f54-186">Os usuários mais propensos a incluir operadores (comum ao pesquisar repositórios de documentos) pode encontrar resultados mais intuitivos se `searchMode=all` informa construções de consulta boolianas.</span><span class="sxs-lookup"><span data-stu-id="72f54-186">Users who are likely to include operators (common when searching document stores) might find results more intuitive if `searchMode=all` informs boolean query constructs.</span></span> <span data-ttu-id="72f54-187">Para obter mais informações sobre a interação entre `searchMode` e os operadores, consulte [sintaxe de consulta simples](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search).</span><span class="sxs-lookup"><span data-stu-id="72f54-187">For more about the interplay between `searchMode` and operators, see [Simple query syntax](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search).</span></span>

<a name="stage2"></a>
## <a name="stage-2-lexical-analysis"></a><span data-ttu-id="72f54-188">Estágio 2: Análise léxica</span><span class="sxs-lookup"><span data-stu-id="72f54-188">Stage 2: Lexical analysis</span></span> 

<span data-ttu-id="72f54-189">Os analisadores léxicos processam *consultas de termo* e *consultas de frase* depois que a árvore de consulta é estruturada.</span><span class="sxs-lookup"><span data-stu-id="72f54-189">Lexical analyzers process *term queries* and *phrase queries* after the query tree is structured.</span></span> <span data-ttu-id="72f54-190">Um analisador aceita as entradas de texto fornecidas pelo analisador, processa o texto e, em seguida, envia de volta os termos com token a serem incorporados na árvore de consulta.</span><span class="sxs-lookup"><span data-stu-id="72f54-190">An analyzer accepts the text inputs given to it by the parser, processes the text, and then sends back tokenized terms to be incorporated into the query tree.</span></span> 

<span data-ttu-id="72f54-191">A forma mais comum de análise léxica é a *análise linguística* que transforma consultas baseadas em termos em regras específicas para um idioma específico:</span><span class="sxs-lookup"><span data-stu-id="72f54-191">The most common form of lexical analysis is *linguistic analysis* which transforms query terms based on rules specific to a given language:</span></span> 

* <span data-ttu-id="72f54-192">Reduzindo um termo de consulta para a raiz de uma palavra</span><span class="sxs-lookup"><span data-stu-id="72f54-192">Reducing a query term to the root form of a word</span></span> 
* <span data-ttu-id="72f54-193">Removendo palavras não-essenciais (palavras irrelevantes, como "o/a" ou "e" em português)</span><span class="sxs-lookup"><span data-stu-id="72f54-193">Removing non-essential words (stopwords, such as "the" or "and" in English)</span></span> 
* <span data-ttu-id="72f54-194">Dividir uma palavra composta em componentes</span><span class="sxs-lookup"><span data-stu-id="72f54-194">Breaking a composite word into component parts</span></span> 
* <span data-ttu-id="72f54-195">Colocando letras minúsculas em uma palavra de letras maiúsculas</span><span class="sxs-lookup"><span data-stu-id="72f54-195">Lower casing an upper case word</span></span> 

<span data-ttu-id="72f54-196">Todas essas operações tendem a apagar as diferenças entre a entrada de texto fornecida pelo usuário e os termos armazenados no índice.</span><span class="sxs-lookup"><span data-stu-id="72f54-196">All of these operations tend to erase differences between the text input provided by the user and the terms stored in the index.</span></span> <span data-ttu-id="72f54-197">Essas operações vão além do processamento de texto e exigem um conhecimento profundo do próprio idioma.</span><span class="sxs-lookup"><span data-stu-id="72f54-197">Such operations go beyond text processing and require in-depth knowledge of the language itself.</span></span> <span data-ttu-id="72f54-198">Para adicionar essa camada de reconhecimento linguístico, o Azure Search dá suporte a uma longa lista de [analisadores de idioma](https://docs.microsoft.com/rest/api/searchservice/language-support) da Lucene e da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="72f54-198">To add this layer of linguistic awareness, Azure Search supports a long list of [language analyzers](https://docs.microsoft.com/rest/api/searchservice/language-support) from both Lucene and Microsoft.</span></span>

> [!Note]
> <span data-ttu-id="72f54-199">Os requisitos de análise podem variar de básicos a elaborados dependendo do seu cenário.</span><span class="sxs-lookup"><span data-stu-id="72f54-199">Analysis requirements can range from minimal to elaborate depending on your scenario.</span></span> <span data-ttu-id="72f54-200">Você pode controlar a complexidade da análise léxica selecionando um dos analisadores predefinidos ou criando seu próprio [analisador personalizado](https://docs.microsoft.com/rest/api/searchservice/Custom-analyzers-in-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="72f54-200">You can control complexity of lexical analysis by the selecting one of the predefined analyzers or by creating your own [custom analyzer](https://docs.microsoft.com/rest/api/searchservice/Custom-analyzers-in-Azure-Search).</span></span> <span data-ttu-id="72f54-201">O escopo dos analisadores inclui campos pesquisáveis e são especificados como parte de uma definição do campo.</span><span class="sxs-lookup"><span data-stu-id="72f54-201">Analyzers are scoped to searchable fields and are specified as part of a field definition.</span></span> <span data-ttu-id="72f54-202">Isso permite que você varie a análise léxica baseada no campo.</span><span class="sxs-lookup"><span data-stu-id="72f54-202">This allows you to vary lexical analysis on a per-field basis.</span></span> <span data-ttu-id="72f54-203">Se não for especificado, o analisador *padrão* para Lucene é usado.</span><span class="sxs-lookup"><span data-stu-id="72f54-203">Unspecified, the *standard* Lucene analyzer is used.</span></span>

<span data-ttu-id="72f54-204">Em nosso exemplo, antes da análise, a árvore de consulta inicial tem o termo "Espaçoso," com um "E" maiúsculo e uma vírgula que o analisador de consulta interpreta como parte do termo de consulta (uma vírgula não é considerada um operador de linguagem de consulta).</span><span class="sxs-lookup"><span data-stu-id="72f54-204">In our example, prior to analysis, the initial query tree has the term "Spacious," with an uppercase "S" and a comma that the query parser interprets as a part of the query term (a comma is not considered a query language operator).</span></span>  

<span data-ttu-id="72f54-205">Quando o analisador padrão processa o termo, ele colocará "vista para o mar" e "espaçoso" em letras minúsculas e removerá o caractere de vírgula.</span><span class="sxs-lookup"><span data-stu-id="72f54-205">When the default analyzer processes the term, it will lowercase "ocean view" and "spacious", and remove the comma character.</span></span> <span data-ttu-id="72f54-206">A árvore de consulta modificada ficará da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="72f54-206">The modified query tree will look as follows:</span></span> 

 ![Consulta booliana com termos analisados][4]

### <a name="testing-analyzer-behaviors"></a><span data-ttu-id="72f54-208">Testando os comportamentos do analisador</span><span class="sxs-lookup"><span data-stu-id="72f54-208">Testing analyzer behaviors</span></span> 

<span data-ttu-id="72f54-209">O comportamento de um analisador pode ser testado usando a [API de análise](https://docs.microsoft.com/rest/api/searchservice/test-analyzer).</span><span class="sxs-lookup"><span data-stu-id="72f54-209">The behavior of an analyzer can be tested using the [Analyze API](https://docs.microsoft.com/rest/api/searchservice/test-analyzer).</span></span> <span data-ttu-id="72f54-210">Forneça o texto que você deseja analisar para ver quais termos o analisador irá gerar.</span><span class="sxs-lookup"><span data-stu-id="72f54-210">Provide the text you want to analyze to see what terms given analyzer will generate.</span></span> <span data-ttu-id="72f54-211">Por exemplo, para ver como o analisador padrão processaria o texto "ar-condicio", você pode emitir a solicitação a seguir:</span><span class="sxs-lookup"><span data-stu-id="72f54-211">For example, to see how the standard analyzer would process the text "air-condition", you can issue the following request:</span></span>

~~~~
{ 
    "text": "air-condition",
    "analyzer": "standard"
}
~~~~

<span data-ttu-id="72f54-212">O analisador padrão quebra o texto de entrada nos dois tokens a seguir, associando atributos como deslocamentos inicial e final (usados para realçar ocorrências), bem como sua posição (usada para correspondência de frase):</span><span class="sxs-lookup"><span data-stu-id="72f54-212">The standard analyzer breaks the input text into the following two tokens, annotating them with attributes like start and end offsets (used for hit highlighting) as well as their position (used for phrase matching):</span></span>

~~~~
{  
  "tokens": [
    {
      "token": "air",
      "startOffset": 0,
      "endOffset": 3,
      "position": 0
    },
    {
      "token": "condition",
      "startOffset": 4,
      "endOffset": 13,
      "position": 1
    }
  ]
}
~~~~

### <a name="exceptions-to-lexical-analysis"></a><span data-ttu-id="72f54-213">Exceções para análise léxica</span><span class="sxs-lookup"><span data-stu-id="72f54-213">Exceptions to lexical analysis</span></span> 

<span data-ttu-id="72f54-214">A análise léxica só se aplica a tipos de consultas que exigem termos completos – uma consulta de termo ou uma consulta de frase.</span><span class="sxs-lookup"><span data-stu-id="72f54-214">Lexical analysis applies only to query types that require complete terms – either a term query or a phrase query.</span></span> <span data-ttu-id="72f54-215">Ela não se aplica aos tipos de consulta com termos incompletos – consulta de prefixo, consulta de caractere curinga, consulta regex – ou a uma consulta difusa.</span><span class="sxs-lookup"><span data-stu-id="72f54-215">It doesn’t apply to query types with incomplete terms – prefix query, wildcard query, regex query – or to a fuzzy query.</span></span> <span data-ttu-id="72f54-216">Esses tipos de consulta, incluindo a consulta de prefixo com o termo *ar-condicio\** em nosso exemplo, são adicionados diretamente à árvore de consulta, ignorando o estágio de análise.</span><span class="sxs-lookup"><span data-stu-id="72f54-216">Those query types, including the prefix query with term *air-condition\** in our example, are added directly to the query tree, bypassing the analysis stage.</span></span> <span data-ttu-id="72f54-217">A única transformação realizada em termos de consulta desses tipos é colocá-los em letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="72f54-217">The only transformation performed on query terms of those types is lowercasing.</span></span>

<a name="stage3"></a>
## <a name="stage-3-document-retrieval"></a><span data-ttu-id="72f54-218">Estágio 3: Recuperação de documentos</span><span class="sxs-lookup"><span data-stu-id="72f54-218">Stage 3: Document retrieval</span></span> 

<span data-ttu-id="72f54-219">A recuperação de documentos se refere à procura de documentos com correspondência de termos no índice.</span><span class="sxs-lookup"><span data-stu-id="72f54-219">Document retrieval refers to finding documents with matching terms in the index.</span></span> <span data-ttu-id="72f54-220">Este estágio é melhor compreendido por meio de um exemplo.</span><span class="sxs-lookup"><span data-stu-id="72f54-220">This stage is understood best through an example.</span></span> <span data-ttu-id="72f54-221">Vamos começar com um índice de hotéis com o esquema simples a seguir:</span><span class="sxs-lookup"><span data-stu-id="72f54-221">Let's start with a hotels index having the following simple schema:</span></span> 

~~~~
{   
    "name": "hotels",     
    "fields": [     
        { "name": "id", "type": "Edm.String", "key": true, "searchable": false },     
        { "name": "title", "type": "Edm.String", "searchable": true },     
        { "name": "description", "type": "Edm.String", "searchable": true }
    ] 
} 
~~~~

<span data-ttu-id="72f54-222">Suponhamos ainda que esse índice contém os quatro documentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="72f54-222">Further assume that this index contains the following four documents:</span></span> 

~~~~
{ 
    "value": [
        {         
            "id": "1",         
            "title": "Hotel Atman",         
            "description": "Spacious rooms, ocean view, walking distance to the beach."   
        },       
        {         
            "id": "2",         
            "title": "Beach Resort",        
            "description": "Located on the north shore of the island of Kauaʻi. Ocean view."     
        },       
        {         
            "id": "3",         
            "title": "Playa Hotel",         
            "description": "Comfortable, air-conditioned rooms with ocean view."
        },       
        {         
            "id": "4",         
            "title": "Ocean Retreat",         
            "description": "Quiet and secluded"
        }    
    ]
}
~~~~

<span data-ttu-id="72f54-223">**Como os termos são indexados**</span><span class="sxs-lookup"><span data-stu-id="72f54-223">**How terms are indexed**</span></span>

<span data-ttu-id="72f54-224">Para entender a recuperação, é útil conhecer algumas noções básicas sobre indexação.</span><span class="sxs-lookup"><span data-stu-id="72f54-224">To understand retrieval, it helps to know a few basics about indexing.</span></span> <span data-ttu-id="72f54-225">A unidade de armazenamento é um índice invertido, um para cada campo pesquisável.</span><span class="sxs-lookup"><span data-stu-id="72f54-225">The unit of storage is an inverted index, one for each searchable field.</span></span> <span data-ttu-id="72f54-226">Dentro de um índice invertido está uma lista classificada de todos os termos de todos os documentos.</span><span class="sxs-lookup"><span data-stu-id="72f54-226">Within an inverted index is a sorted list of all terms from all documents.</span></span> <span data-ttu-id="72f54-227">Cada termo é mapeado para a lista de documentos nos quais ele ocorre, tão evidente no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="72f54-227">Each term maps to the list of documents in which it occurs, as evident in the example below.</span></span>

<span data-ttu-id="72f54-228">Para produzir os termos de um índice invertido, o mecanismo de pesquisa executa a análise léxica do o conteúdo dos documentos, de forma semelhante ao que acontece durante o processamento da consulta.</span><span class="sxs-lookup"><span data-stu-id="72f54-228">To produce the terms in an inverted index, the search engine performs lexical analysis over the content of documents, similar to what happens during query processing.</span></span> <span data-ttu-id="72f54-229">As entradas de texto são passadas para um analisador, em letras minúsculas, sem pontuação e assim por diante, dependendo da configuração do analisador.</span><span class="sxs-lookup"><span data-stu-id="72f54-229">Text inputs are passed to an analyzer, lower-cased, stripped of punctuation, and so forth, depending on the analyzer configuration.</span></span> <span data-ttu-id="72f54-230">É comum, mas não obrigatório, usar os mesmo analisadores para operações de indexação para que os termos da consulta pareçam mais com os termos dentro do índice.</span><span class="sxs-lookup"><span data-stu-id="72f54-230">It's common, but not required, to use the same analyzers for search and indexing operations so that query terms look more like terms inside the index.</span></span>

> [!Note]
> <span data-ttu-id="72f54-231">O Azure Search permite especificar diferentes analisadores para indexação e pesquisa através dos parâmetros de campo adicionais `indexAnalyzer` e `searchAnalyzer`.</span><span class="sxs-lookup"><span data-stu-id="72f54-231">Azure Search lets you specify different analyzers for indexing and search via additional `indexAnalyzer` and `searchAnalyzer` field parameters.</span></span> <span data-ttu-id="72f54-232">Se não forem especificados, o analisador definido com a propriedade `analyzer` é usado para indexação e pesquisa.</span><span class="sxs-lookup"><span data-stu-id="72f54-232">If unspecified, the analyzer set with the `analyzer` property is used for both indexing and searching.</span></span>  

<span data-ttu-id="72f54-233">**Índice invertido para documentos de exemplo**</span><span class="sxs-lookup"><span data-stu-id="72f54-233">**Inverted index for example documents**</span></span>

<span data-ttu-id="72f54-234">Retornando ao nosso exemplo, para o campo **título**, o índice invertido tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="72f54-234">Returning to our example, for the **title** field, the inverted index looks like this:</span></span>

| <span data-ttu-id="72f54-235">Termo</span><span class="sxs-lookup"><span data-stu-id="72f54-235">Term</span></span> | <span data-ttu-id="72f54-236">Lista de documentos</span><span class="sxs-lookup"><span data-stu-id="72f54-236">Document list</span></span> |
|------|---------------|
| <span data-ttu-id="72f54-237">atman</span><span class="sxs-lookup"><span data-stu-id="72f54-237">atman</span></span> | <span data-ttu-id="72f54-238">1</span><span class="sxs-lookup"><span data-stu-id="72f54-238">1</span></span> |
| <span data-ttu-id="72f54-239">praia</span><span class="sxs-lookup"><span data-stu-id="72f54-239">beach</span></span> | <span data-ttu-id="72f54-240">2</span><span class="sxs-lookup"><span data-stu-id="72f54-240">2</span></span> |
| <span data-ttu-id="72f54-241">hotel</span><span class="sxs-lookup"><span data-stu-id="72f54-241">hotel</span></span> | <span data-ttu-id="72f54-242">1, 3</span><span class="sxs-lookup"><span data-stu-id="72f54-242">1, 3</span></span> |
| <span data-ttu-id="72f54-243">mar</span><span class="sxs-lookup"><span data-stu-id="72f54-243">ocean</span></span> | <span data-ttu-id="72f54-244">4</span><span class="sxs-lookup"><span data-stu-id="72f54-244">4</span></span>  |
| <span data-ttu-id="72f54-245">playa</span><span class="sxs-lookup"><span data-stu-id="72f54-245">playa</span></span> | <span data-ttu-id="72f54-246">3</span><span class="sxs-lookup"><span data-stu-id="72f54-246">3</span></span> |
| <span data-ttu-id="72f54-247">resort</span><span class="sxs-lookup"><span data-stu-id="72f54-247">resort</span></span> | <span data-ttu-id="72f54-248">3</span><span class="sxs-lookup"><span data-stu-id="72f54-248">3</span></span> |
| <span data-ttu-id="72f54-249">retiro</span><span class="sxs-lookup"><span data-stu-id="72f54-249">retreat</span></span> | <span data-ttu-id="72f54-250">4</span><span class="sxs-lookup"><span data-stu-id="72f54-250">4</span></span> |

<span data-ttu-id="72f54-251">No campo título, apenas *hotel* aparece em dois documentos: 1, 3.</span><span class="sxs-lookup"><span data-stu-id="72f54-251">In the title field, only *hotel* shows up in two documents: 1, 3.</span></span>

<span data-ttu-id="72f54-252">Para o campo **descrição**, o índice é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="72f54-252">For the **description** field, the index is as follows:</span></span>

| <span data-ttu-id="72f54-253">Termo</span><span class="sxs-lookup"><span data-stu-id="72f54-253">Term</span></span> | <span data-ttu-id="72f54-254">Lista de documentos</span><span class="sxs-lookup"><span data-stu-id="72f54-254">Document list</span></span> |
|------|---------------|
| <span data-ttu-id="72f54-255">ar</span><span class="sxs-lookup"><span data-stu-id="72f54-255">air</span></span> | <span data-ttu-id="72f54-256">3</span><span class="sxs-lookup"><span data-stu-id="72f54-256">3</span></span>
| <span data-ttu-id="72f54-257">e</span><span class="sxs-lookup"><span data-stu-id="72f54-257">and</span></span> | <span data-ttu-id="72f54-258">4</span><span class="sxs-lookup"><span data-stu-id="72f54-258">4</span></span>
| <span data-ttu-id="72f54-259">praia</span><span class="sxs-lookup"><span data-stu-id="72f54-259">beach</span></span> | <span data-ttu-id="72f54-260">1</span><span class="sxs-lookup"><span data-stu-id="72f54-260">1</span></span>
| <span data-ttu-id="72f54-261">condicionado</span><span class="sxs-lookup"><span data-stu-id="72f54-261">conditioned</span></span> | <span data-ttu-id="72f54-262">3</span><span class="sxs-lookup"><span data-stu-id="72f54-262">3</span></span>
| <span data-ttu-id="72f54-263">confortável</span><span class="sxs-lookup"><span data-stu-id="72f54-263">comfortable</span></span> | <span data-ttu-id="72f54-264">3</span><span class="sxs-lookup"><span data-stu-id="72f54-264">3</span></span>
| <span data-ttu-id="72f54-265">distância</span><span class="sxs-lookup"><span data-stu-id="72f54-265">distance</span></span> | <span data-ttu-id="72f54-266">1</span><span class="sxs-lookup"><span data-stu-id="72f54-266">1</span></span>
| <span data-ttu-id="72f54-267">ilha</span><span class="sxs-lookup"><span data-stu-id="72f54-267">island</span></span> | <span data-ttu-id="72f54-268">2</span><span class="sxs-lookup"><span data-stu-id="72f54-268">2</span></span>
| <span data-ttu-id="72f54-269">kauaʻi</span><span class="sxs-lookup"><span data-stu-id="72f54-269">kauaʻi</span></span> | <span data-ttu-id="72f54-270">2</span><span class="sxs-lookup"><span data-stu-id="72f54-270">2</span></span>
| <span data-ttu-id="72f54-271">local</span><span class="sxs-lookup"><span data-stu-id="72f54-271">located</span></span> | <span data-ttu-id="72f54-272">2</span><span class="sxs-lookup"><span data-stu-id="72f54-272">2</span></span>
| <span data-ttu-id="72f54-273">norte</span><span class="sxs-lookup"><span data-stu-id="72f54-273">north</span></span> | <span data-ttu-id="72f54-274">2</span><span class="sxs-lookup"><span data-stu-id="72f54-274">2</span></span>
| <span data-ttu-id="72f54-275">mar</span><span class="sxs-lookup"><span data-stu-id="72f54-275">ocean</span></span> | <span data-ttu-id="72f54-276">1, 2, 3</span><span class="sxs-lookup"><span data-stu-id="72f54-276">1, 2, 3</span></span>
| <span data-ttu-id="72f54-277">de</span><span class="sxs-lookup"><span data-stu-id="72f54-277">of</span></span> | <span data-ttu-id="72f54-278">2</span><span class="sxs-lookup"><span data-stu-id="72f54-278">2</span></span>
| <span data-ttu-id="72f54-279">em</span><span class="sxs-lookup"><span data-stu-id="72f54-279">on</span></span> |<span data-ttu-id="72f54-280">2</span><span class="sxs-lookup"><span data-stu-id="72f54-280">2</span></span>
| <span data-ttu-id="72f54-281">silencioso</span><span class="sxs-lookup"><span data-stu-id="72f54-281">quiet</span></span> | <span data-ttu-id="72f54-282">4</span><span class="sxs-lookup"><span data-stu-id="72f54-282">4</span></span>
| <span data-ttu-id="72f54-283">quartos</span><span class="sxs-lookup"><span data-stu-id="72f54-283">rooms</span></span>  | <span data-ttu-id="72f54-284">1, 3</span><span class="sxs-lookup"><span data-stu-id="72f54-284">1, 3</span></span>
| <span data-ttu-id="72f54-285">reservado</span><span class="sxs-lookup"><span data-stu-id="72f54-285">secluded</span></span> | <span data-ttu-id="72f54-286">4</span><span class="sxs-lookup"><span data-stu-id="72f54-286">4</span></span>
| <span data-ttu-id="72f54-287">beira-mar</span><span class="sxs-lookup"><span data-stu-id="72f54-287">shore</span></span> | <span data-ttu-id="72f54-288">2</span><span class="sxs-lookup"><span data-stu-id="72f54-288">2</span></span>
| <span data-ttu-id="72f54-289">espaçoso</span><span class="sxs-lookup"><span data-stu-id="72f54-289">spacious</span></span> | <span data-ttu-id="72f54-290">1</span><span class="sxs-lookup"><span data-stu-id="72f54-290">1</span></span>
| <span data-ttu-id="72f54-291">o</span><span class="sxs-lookup"><span data-stu-id="72f54-291">the</span></span> | <span data-ttu-id="72f54-292">1, 2</span><span class="sxs-lookup"><span data-stu-id="72f54-292">1, 2</span></span>
| <span data-ttu-id="72f54-293">para</span><span class="sxs-lookup"><span data-stu-id="72f54-293">to</span></span> | <span data-ttu-id="72f54-294">1</span><span class="sxs-lookup"><span data-stu-id="72f54-294">1</span></span>
| <span data-ttu-id="72f54-295">view</span><span class="sxs-lookup"><span data-stu-id="72f54-295">view</span></span> | <span data-ttu-id="72f54-296">1, 2, 3</span><span class="sxs-lookup"><span data-stu-id="72f54-296">1, 2, 3</span></span>
| <span data-ttu-id="72f54-297">a pé</span><span class="sxs-lookup"><span data-stu-id="72f54-297">walking</span></span> | <span data-ttu-id="72f54-298">1</span><span class="sxs-lookup"><span data-stu-id="72f54-298">1</span></span>
| <span data-ttu-id="72f54-299">por:</span><span class="sxs-lookup"><span data-stu-id="72f54-299">with</span></span> | <span data-ttu-id="72f54-300">3</span><span class="sxs-lookup"><span data-stu-id="72f54-300">3</span></span>


<span data-ttu-id="72f54-301">**Correspondência de termos de consulta com os termos indexados**</span><span class="sxs-lookup"><span data-stu-id="72f54-301">**Matching query terms against indexed terms**</span></span>

<span data-ttu-id="72f54-302">Considerando os índices invertidos acima, vamos voltar para a consulta de exemplo e ver como documentos com correspondência são encontrados para a nossa consulta de exemplo.</span><span class="sxs-lookup"><span data-stu-id="72f54-302">Given the inverted indices above, let’s return to the sample query and see how matching documents are found for our example query.</span></span> <span data-ttu-id="72f54-303">Lembre-se de que a árvore de consulta final tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="72f54-303">Recall that the final query tree looks like this:</span></span> 

 ![Consulta booliana com termos analisados][4]

<span data-ttu-id="72f54-305">Durante a execução de consulta, consultas individuais são executadas nos campos pesquisáveis de independente.</span><span class="sxs-lookup"><span data-stu-id="72f54-305">During query execution, individual queries are executed against the searchable fields independently.</span></span> 

+ <span data-ttu-id="72f54-306">A pesquisa do termo, "espaçoso", corresponde ao documento 1 (Hotel Atman).</span><span class="sxs-lookup"><span data-stu-id="72f54-306">The TermQuery, "spacious", matches document 1 (Hotel Atman).</span></span> 

+ <span data-ttu-id="72f54-307">A consulta de prefixo, "ar-condicio *", não corresponde a nenhum documento.</span><span class="sxs-lookup"><span data-stu-id="72f54-307">The PrefixQuery, "air-condition*", doesn't match any documents.</span></span> 

  <span data-ttu-id="72f54-308">Esse é um comportamento que às vezes confunde os desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="72f54-308">This is a behavior that sometimes confuses developers.</span></span> <span data-ttu-id="72f54-309">Embora o termo com ar condicionado exista no documento, ele é dividido em dois termos pelo analisador padrão.</span><span class="sxs-lookup"><span data-stu-id="72f54-309">Although the term air-conditioned exists in the document, it is split into two terms by the default analyzer.</span></span> <span data-ttu-id="72f54-310">Lembre-se de que as consultas de prefixo, que contêm termos parciais, não são analisadas.</span><span class="sxs-lookup"><span data-stu-id="72f54-310">Recall that prefix queries, which contain partial terms, are not analyzed.</span></span> <span data-ttu-id="72f54-311">Portanto, os termos com o prefixo "ar-condicio" são pesquisados no índice invertido e não são encontrados.</span><span class="sxs-lookup"><span data-stu-id="72f54-311">Therefore terms with prefix "air-condition" are looked up in the inverted index and not found.</span></span>

+ <span data-ttu-id="72f54-312">A consulta de frase, "vista para o mar", procura os termos "mar" e "vista para o" e verifica a proximidade dos termos no documento original.</span><span class="sxs-lookup"><span data-stu-id="72f54-312">The PhraseQuery, "ocean view", looks up the terms "ocean" and "view" and checks the proximity of terms in the original document.</span></span> <span data-ttu-id="72f54-313">Os documentos 1, 2 e 3 correspondem a essa consulta no campo descrição.</span><span class="sxs-lookup"><span data-stu-id="72f54-313">Documents 1, 2 and 3 match this query in the description field.</span></span> <span data-ttu-id="72f54-314">Observe que o documento 4 possui o termo mar termo no título, mas não é considerado uma correspondência, pois estamos procurando a frase "vista para o mar" em vez de palavras individuais.</span><span class="sxs-lookup"><span data-stu-id="72f54-314">Notice document 4 has the term ocean in the title but isn’t considered a match, as we're looking for the "ocean view" phrase rather than individual words.</span></span> 

> [!Note]
> <span data-ttu-id="72f54-315">Uma consulta de pesquisa é executada de forma independente em relação a todos os campos pesquisáveis no índice do Azure Search, a menos que você limite os campos definidos com o parâmetro `searchFields`, conforme ilustrado na solicitação de pesquisa de exemplo.</span><span class="sxs-lookup"><span data-stu-id="72f54-315">A search query is executed independently against all searchable fields in the Azure Search index unless you limit the fields set with the `searchFields` parameter, as illustrated in the example search request.</span></span> <span data-ttu-id="72f54-316">Os documentos correspondentes em qualquer um dos campos selecionados são retornados.</span><span class="sxs-lookup"><span data-stu-id="72f54-316">Documents that match in any of the selected fields are returned.</span></span> 

<span data-ttu-id="72f54-317">De modo geral, para a consulta em questão, os documentos que correspondem são 1, 2, 3.</span><span class="sxs-lookup"><span data-stu-id="72f54-317">On the whole, for the query in question, the documents that match are 1, 2, 3.</span></span> 

## <a name="stage-4-scoring"></a><span data-ttu-id="72f54-318">Estágio 4: Pontuação</span><span class="sxs-lookup"><span data-stu-id="72f54-318">Stage 4: Scoring</span></span>  

<span data-ttu-id="72f54-319">Todos os documentos em um conjunto de resultados de pesquisa recebe uma pontuação de relevância.</span><span class="sxs-lookup"><span data-stu-id="72f54-319">Every document in a search result set is assigned a relevance score.</span></span> <span data-ttu-id="72f54-320">A função da pontuação de relevância é classificar com uma pontuação mais alta os documentos que melhor respondem a uma pergunta do usuário melhor conforme expressa pela consulta de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="72f54-320">The function of the relevance score is to rank higher those documents that best answer a user question as expressed by the search query.</span></span> <span data-ttu-id="72f54-321">A pontuação é calculada com base nas propriedades estatísticas dos termos com correspondência.</span><span class="sxs-lookup"><span data-stu-id="72f54-321">The score is computed based on statistical properties of terms that matched.</span></span> <span data-ttu-id="72f54-322">A fórmula da pontuação é basicamente [TF/IDF (frequência do termo sobre frequência inversa do documento)](https://en.wikipedia.org/wiki/Tf%E2%80%93idf).</span><span class="sxs-lookup"><span data-stu-id="72f54-322">At the core of the scoring formula is [TF/IDF (term frequency-inverse document frequency)](https://en.wikipedia.org/wiki/Tf%E2%80%93idf).</span></span> <span data-ttu-id="72f54-323">Em consultas que contêm termos comuns e raros, TF/IDF fornece resultados que contêm o termo raro.</span><span class="sxs-lookup"><span data-stu-id="72f54-323">In queries containing rare and common terms, TF/IDF promotes results containing the rare term.</span></span> <span data-ttu-id="72f54-324">Por exemplo, em um índice hipotético com todos os artigos da Wikipédia, de documentos que correspondem à consulta *o presidente*, os documentos com correspondência para *presidente* são considerados mais relevantes do que os documentos com correspondência para *o*.</span><span class="sxs-lookup"><span data-stu-id="72f54-324">For example, in a hypothetical index with all Wikipedia articles, from documents that matched the query *the president*, documents matching on *president* are considered more relevant than documents matching on *the*.</span></span>


### <a name="scoring-example"></a><span data-ttu-id="72f54-325">Exemplo de pontuação</span><span class="sxs-lookup"><span data-stu-id="72f54-325">Scoring example</span></span>

<span data-ttu-id="72f54-326">Lembre-se dos três documentos que correspondem à nossa consulta de exemplo:</span><span class="sxs-lookup"><span data-stu-id="72f54-326">Recall the three documents that matched our example query:</span></span>
~~~~
search=Spacious, air-condition* +"Ocean view"  
~~~~
~~~~
{  
  "value": [
    {
      "@search.score": 0.25610128,
      "id": "1",
      "title": "Hotel Atman",
      "description": "Spacious rooms, ocean view, walking distance to the beach."
    },
    {
      "@search.score": 0.08951007,
      "id": "3",
      "title": "Playa Hotel",
      "description": "Comfortable, air-conditioned rooms with ocean view."
    },
    {
      "@search.score": 0.05967338,
      "id": "2",
      "title": "Ocean Resort",
      "description": "Located on a cliff on the north shore of the island of Kauai. Ocean view."
    }
  ]
}
~~~~

<span data-ttu-id="72f54-327">O documento 1 foi o que melhor correspondeu à consulta, pois tanto o termo *espaçoso* como a frase solicitada *vista para o mar* ocorrem no campo descrição.</span><span class="sxs-lookup"><span data-stu-id="72f54-327">Document 1 matched the query best because both the term *spacious* and the required phrase *ocean view* occur in the description field.</span></span> <span data-ttu-id="72f54-328">Os próximos dois documentos correspondem apenas à frase *vista para o mar*.</span><span class="sxs-lookup"><span data-stu-id="72f54-328">The next two documents match only the phrase *ocean view*.</span></span> <span data-ttu-id="72f54-329">Pode ser surpreendente que as pontuações de relevância para os documentos 2 e 3 sejam diferentes, mesmo que ambos tenham correspondido à consulta da mesma maneira.</span><span class="sxs-lookup"><span data-stu-id="72f54-329">It might be surprising that the relevance score for document 2 and 3 is different even though they matched the query in the same way.</span></span> <span data-ttu-id="72f54-330">Isso ocorre porque a fórmula de pontuação tem mais componentes do que simplesmente TF/IDF.</span><span class="sxs-lookup"><span data-stu-id="72f54-330">It's because the scoring formula has more components than just TF/IDF.</span></span> <span data-ttu-id="72f54-331">Nesse caso, o documento 3 recebeu uma pontuação ligeiramente mais alta porque sua descrição é mais curta.</span><span class="sxs-lookup"><span data-stu-id="72f54-331">In this case, document 3 was assigned a slightly higher score because its description is shorter.</span></span> <span data-ttu-id="72f54-332">Saiba mais sobre a [Fórmula de pontuação prática do Lucene](https://lucene.apache.org/core/4_0_0/core/org/apache/lucene/search/similarities/TFIDFSimilarity.html) para entender como o tamanho do campo e outros fatores podem influenciar a pontuação de relevância.</span><span class="sxs-lookup"><span data-stu-id="72f54-332">Learn about [Lucene's Practical Scoring Formula](https://lucene.apache.org/core/4_0_0/core/org/apache/lucene/search/similarities/TFIDFSimilarity.html) to understand how field length and other factors can influence the relevance score.</span></span>

<span data-ttu-id="72f54-333">Alguns tipos de consulta (caractere curinga, prefixo, regex) sempre contribuem com uma pontuação constante para a pontuação total do documento.</span><span class="sxs-lookup"><span data-stu-id="72f54-333">Some query types (wildcard, prefix, regex) always contribute a constant score to the overall document score.</span></span> <span data-ttu-id="72f54-334">Isso permite que as correspondências encontradas por meio da expansão de consulta sejam incluídas nos resultados, mas sem afetar a classificação.</span><span class="sxs-lookup"><span data-stu-id="72f54-334">This allows matches found through query expansion to be included in the results, but without affecting the ranking.</span></span> 

<span data-ttu-id="72f54-335">Um exemplo ilustra por que isso é importante.</span><span class="sxs-lookup"><span data-stu-id="72f54-335">An example illustrates why this matters.</span></span> <span data-ttu-id="72f54-336">Pesquisas com caractere curinga, inclusive pesquisas de prefixo são ambíguas por definição, porque a entrada é uma cadeia de caracteres parcial com correspondências possíveis em um grande número de termos diferentes (considere uma entrada de "pass *", com correspondências encontradas em "passeios", "passagem" e "passarela").</span><span class="sxs-lookup"><span data-stu-id="72f54-336">Wildcard searches, including prefix searches, are ambiguous by definition because the input is a partial string with potential matches on a very large number of disparate terms (consider an input of "tour*", with matches found on “tours”, “tourettes”, and “tourmaline”).</span></span> <span data-ttu-id="72f54-337">Dada a natureza desses resultados, não é possível inferir de forma razoável quais termos são mais valiosos do que outros.</span><span class="sxs-lookup"><span data-stu-id="72f54-337">Given the nature of these results, there is no way to reasonably infer which terms are more valuable than others.</span></span> <span data-ttu-id="72f54-338">Por esse motivo, podemos ignorar as frequências dos termos ao pontuar resultados em consultas dos tipos caractere curinga, prefixo e regex.</span><span class="sxs-lookup"><span data-stu-id="72f54-338">For this reason, we ignore term frequencies when scoring results in queries of types wildcard, prefix and regex.</span></span> <span data-ttu-id="72f54-339">Em uma solicitação de pesquisa de várias partes que inclui termos parciais e completos, os resultados da entrada parcial são incorporados com uma pontuação de constante para evitar desvios em relação às correspondências potencialmente inesperadas.</span><span class="sxs-lookup"><span data-stu-id="72f54-339">In a multi-part search request that includes partial and complete terms, results from the partial input are incorporated with a constant score to avoid bias towards potentially unexpected matches.</span></span>

### <a name="score-tuning"></a><span data-ttu-id="72f54-340">Ajuste da pontuação</span><span class="sxs-lookup"><span data-stu-id="72f54-340">Score tuning</span></span>

<span data-ttu-id="72f54-341">Existem duas maneiras de ajustar as pontuações de relevância no Azure Search:</span><span class="sxs-lookup"><span data-stu-id="72f54-341">There are two ways to tune relevance scores in Azure Search:</span></span>

1. <span data-ttu-id="72f54-342">**Perfis de pontuação** melhoram a classificação dos documentos na lista classificada de resultados com base em um conjunto de regras.</span><span class="sxs-lookup"><span data-stu-id="72f54-342">**Scoring profiles** promote documents in the ranked list of results based on a set of rules.</span></span> <span data-ttu-id="72f54-343">Em nosso exemplo, podemos considerar a possibilidade de que os documentos correspondentes no campo de título são mais relevante do que os documentos correspondentes no campo descrição.</span><span class="sxs-lookup"><span data-stu-id="72f54-343">In our example, we could consider documents that matched in the title field more relevant than documents that matched in the description field.</span></span> <span data-ttu-id="72f54-344">Além disso, se o índice tiver um campo preço para cada hotel, poderíamos promover documentos com preços mais baixos.</span><span class="sxs-lookup"><span data-stu-id="72f54-344">Additionally, if our index had a price field for each hotel, we could promote documents with lower price.</span></span> <span data-ttu-id="72f54-345">Saiba mais sobre como [adicionar perfis de pontuação a um índice de pesquisa.](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)</span><span class="sxs-lookup"><span data-stu-id="72f54-345">Learn more how to [add Scoring Profiles to a search index.](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)</span></span>
2. <span data-ttu-id="72f54-346">**Incremento de termo** (disponível apenas na sintaxe da consulta Lucene completo) fornece um operador de incremento `^` que pode ser aplicado a qualquer parte da árvore de consulta.</span><span class="sxs-lookup"><span data-stu-id="72f54-346">**Term boosting** (available only in the Full Lucene query syntax) provides a boosting operator `^` that can be applied to any part of the query tree.</span></span> <span data-ttu-id="72f54-347">Em nosso exemplo, em vez de procurar no prefixo *ar-condicio*\*, um usuário poderia pesquisar o termo exato *ar-condicio* ou o prefixo, mas os documentos que correspondem ao termo exato apresentam uma classificação superior quando é aplicado o incremento à consulta do termo: *ar-condicio^2||ar-condicio**.</span><span class="sxs-lookup"><span data-stu-id="72f54-347">In our example, instead of searching on the prefix *air-condition*\*, one could search for either the exact term *air-condition* or the prefix, but documents that match on the exact term are ranked higher by applying boost to the term query: *air-condition^2||air-condition**.</span></span> <span data-ttu-id="72f54-348">Saiba mais sobre [incremento do termo](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search#bkmk_termboost).</span><span class="sxs-lookup"><span data-stu-id="72f54-348">Learn more about [term boosting](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search#bkmk_termboost).</span></span>


### <a name="scoring-in-a-distributed-index"></a><span data-ttu-id="72f54-349">Pontuação em um índice distribuído</span><span class="sxs-lookup"><span data-stu-id="72f54-349">Scoring in a distributed index</span></span>

<span data-ttu-id="72f54-350">Todos os índices do Azure Search são automaticamente divididos em vários fragmentos, permitindo distribuir rapidamente o índice entre vários nós rapidamente ao escalar ou reduzir verticalmente o serviço.</span><span class="sxs-lookup"><span data-stu-id="72f54-350">All indexes in Azure Search are automatically split into multiple shards, allowing us to quickly distribute the index among multiple nodes during service scale up or scale down.</span></span> <span data-ttu-id="72f54-351">Quando uma solicitação de pesquisa é emitida, ela é emitida em relação a cada fragmento de forma independente.</span><span class="sxs-lookup"><span data-stu-id="72f54-351">When a search request is issued, it’s issued against each shard independently.</span></span> <span data-ttu-id="72f54-352">Os resultados de cada fragmento são então mesclados e ordenados conforme a pontuação (se nenhuma outra ordem for definida).</span><span class="sxs-lookup"><span data-stu-id="72f54-352">The results from each shard are then merged and ordered by score (if no other ordering is defined).</span></span> <span data-ttu-id="72f54-353">É importante saber que a função de pontuação faz a ponderação da frequência do termo de consulta em relação a sua frequência de documento inversa em todos os documentos dentro do fragmento, não em todos os fragmentos!</span><span class="sxs-lookup"><span data-stu-id="72f54-353">It is important to know that the scoring function weights query term frequency against its inverse document frequency in all documents within the shard, not across all shards!</span></span>

<span data-ttu-id="72f54-354">Isso significa que uma pontuação de relevância *pode* ser diferentes para documentos idênticos se estes estiverem em fragmentos diferentes.</span><span class="sxs-lookup"><span data-stu-id="72f54-354">This means a relevance score *could* be different for identical documents if they reside on different shards.</span></span> <span data-ttu-id="72f54-355">Felizmente, essas diferenças tendem a desaparecer conforme aumenta o número de documentos no índice devido a uma distribuição de termo mais uniforme.</span><span class="sxs-lookup"><span data-stu-id="72f54-355">Fortunately, such differences tend to disappear as the number of documents in the index grows due to more even term distribution.</span></span> <span data-ttu-id="72f54-356">Não é possível supor em qual fragmento qualquer documento especificado será colocado.</span><span class="sxs-lookup"><span data-stu-id="72f54-356">It’s not possible to assume on which shard any given document will be placed.</span></span> <span data-ttu-id="72f54-357">No entanto, supondo que uma chave de documento não é alterado, ela sempre será atribuída ao mesmo fragmento.</span><span class="sxs-lookup"><span data-stu-id="72f54-357">However, assuming a document key doesn't change, it will always be assigned to the same shard.</span></span>

<span data-ttu-id="72f54-358">Em geral, a pontuação de documentos não é o melhor atributo para classificar documentos se a estabilidade da classificação for importante.</span><span class="sxs-lookup"><span data-stu-id="72f54-358">In general, document score is not the best attribute for ordering documents if order stability is important.</span></span> <span data-ttu-id="72f54-359">Por exemplo, considerando dois documentos com uma pontuação idêntica, não há nenhuma garantia de qual aparece primeiro nas execuções posteriores da mesma consulta.</span><span class="sxs-lookup"><span data-stu-id="72f54-359">For example, given two document with an identical score, there is no guarantee which one appears first in subsequent runs of the same query.</span></span> <span data-ttu-id="72f54-360">A pontuação de documento deve dar somente uma noção geral de relevância do documento em relação a outros documentos no conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="72f54-360">Document score should only give a general sense of document relevance relative to other documents in the results set.</span></span>

## <a name="conclusion"></a><span data-ttu-id="72f54-361">Conclusão</span><span class="sxs-lookup"><span data-stu-id="72f54-361">Conclusion</span></span>

<span data-ttu-id="72f54-362">O sucesso dos mecanismos de pesquisa da Internet gerou expectativas para a pesquisa de texto completo em dados particulares.</span><span class="sxs-lookup"><span data-stu-id="72f54-362">The success of internet search engines has raised expectations for full text search over private data.</span></span> <span data-ttu-id="72f54-363">Para quase qualquer tipo de experiência de pesquisa, esperamos que o mecanismo entenda a nossa intenção, mesmo quando os termos estão incorretos ou incompletos.</span><span class="sxs-lookup"><span data-stu-id="72f54-363">For almost any kind of search experience, we now expect the engine to understand our intent, even when terms are misspelled or incomplete.</span></span> <span data-ttu-id="72f54-364">Esperamos até correspondências com base em termos equivalentes ou sinônimos que nem especificamos.</span><span class="sxs-lookup"><span data-stu-id="72f54-364">We might even expect matches based on near equivalent terms or synonyms that we never actually specified.</span></span>

<span data-ttu-id="72f54-365">Do ponto de vista técnico, a pesquisa de texto completo é altamente complexa, exigindo uma análise linguística sofisticada e uma abordagem sistemática para processamento de forma a extrair, expandir e transformar os termos da consulta para fornecer um resultado relevante.</span><span class="sxs-lookup"><span data-stu-id="72f54-365">From a technical standpoint, full text search is highly complex, requiring sophisticated linguistic analysis and a systematic approach to processing in ways that distill, expand, and transform query terms to deliver a relevant result.</span></span> <span data-ttu-id="72f54-366">Devido às complexidades inerentes, há muitos fatores que podem afetar o resultado de uma consulta.</span><span class="sxs-lookup"><span data-stu-id="72f54-366">Given the inherent complexities, there are a lot of factors that can affect the outcome of a query.</span></span> <span data-ttu-id="72f54-367">Por esse motivo, investir tempo para entender os mecanismos de pesquisa de texto completo oferece benefícios tangíveis quando se tenta trabalhar com resultados inesperados.</span><span class="sxs-lookup"><span data-stu-id="72f54-367">For this reason, investing the time to understand the mechanics of full text search offers tangible benefits when trying to work through unexpected results.</span></span>  

<span data-ttu-id="72f54-368">Este artigo explorou a pesquisa de texto completo no contexto do Azure Search.</span><span class="sxs-lookup"><span data-stu-id="72f54-368">This article explored full text search in the context of Azure Search.</span></span> <span data-ttu-id="72f54-369">Esperamos que todas essas informações sejam o suficiente para você reconhecer possíveis causas e resoluções para resolver problemas comuns de consulta.</span><span class="sxs-lookup"><span data-stu-id="72f54-369">We hope it gives you sufficient background to recognize potential causes and resolutions for addressing common query problems.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="72f54-370">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="72f54-370">Next steps</span></span>

+ <span data-ttu-id="72f54-371">Criar o índice de exemplo, experimentar consultas diferentes e examinar os resultados.</span><span class="sxs-lookup"><span data-stu-id="72f54-371">Build the sample index, try out different queries and review results.</span></span> <span data-ttu-id="72f54-372">Para obter instruções, consulte [Criar e consultar um índice no portal](search-get-started-portal.md#query-index).</span><span class="sxs-lookup"><span data-stu-id="72f54-372">For instructions, see [Build and query an index in the portal](search-get-started-portal.md#query-index).</span></span>

+ <span data-ttu-id="72f54-373">Tente outras sintaxes de consulta a partir da seção de exemplo [Pesquisar documentos](https://docs.microsoft.com/rest/api/searchservice/search-documents#examples) da [sintaxe de consulta simples](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) no gerenciador de pesquisa no portal.</span><span class="sxs-lookup"><span data-stu-id="72f54-373">Try additional query syntax from the [Search Documents](https://docs.microsoft.com/rest/api/searchservice/search-documents#examples) example section or from [Simple query syntax](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) in Search explorer in the portal.</span></span>

+ <span data-ttu-id="72f54-374">Analise os [perfis de pontuação](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) para ajustar a classificação no seu aplicativo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="72f54-374">Review [scoring profiles](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) if you want to tune ranking in your search application.</span></span>

+ <span data-ttu-id="72f54-375">Saiba como aplicar [analisadores léxicos específico do idioma](https://docs.microsoft.com/rest/api/searchservice/language-support).</span><span class="sxs-lookup"><span data-stu-id="72f54-375">Learn how to apply [language-specific lexical analyzers](https://docs.microsoft.com/rest/api/searchservice/language-support).</span></span>

+ <span data-ttu-id="72f54-376">[Configurar analisadores personalizados](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) para o mínimo de processamento ou processamento especializado em campos específicos.</span><span class="sxs-lookup"><span data-stu-id="72f54-376">[Configure custom analyzers](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) for either minimal processing or specialized processing on specific fields.</span></span>

+ <span data-ttu-id="72f54-377">[Compare os analisadores padrão e inglês](http://alice.unearth.ai/) lado a lado neste site da Web de demonstração.</span><span class="sxs-lookup"><span data-stu-id="72f54-377">[Compare standard and English analyzers](http://alice.unearth.ai/)) side-by-side on this demo web site.</span></span> 

## <a name="see-also"></a><span data-ttu-id="72f54-378">Consulte também</span><span class="sxs-lookup"><span data-stu-id="72f54-378">See also</span></span>

[<span data-ttu-id="72f54-379">API REST para pesquisar documentos</span><span class="sxs-lookup"><span data-stu-id="72f54-379">Search Documents REST API</span></span>](https://docs.microsoft.com/rest/api/searchservice/search-documents)

[<span data-ttu-id="72f54-380">Sintaxe de consulta simples</span><span class="sxs-lookup"><span data-stu-id="72f54-380">Simple query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)

[<span data-ttu-id="72f54-381">Sintaxe de consulta Lucene completa</span><span class="sxs-lookup"><span data-stu-id="72f54-381">Full Lucene query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)

[<span data-ttu-id="72f54-382">Controlar os resultados da pesquisa</span><span class="sxs-lookup"><span data-stu-id="72f54-382">Handle search results</span></span>](https://docs.microsoft.com/azure/search/search-pagination-page-layout)

<!--Image references-->
[1]: ./media/search-lucene-query-architecture/architecture-diagram2.png
[2]: ./media/search-lucene-query-architecture/azSearch-queryparsing-should2.png
[3]: ./media/search-lucene-query-architecture/azSearch-queryparsing-must2.png
[4]: ./media/search-lucene-query-architecture/azSearch-queryparsing-spacious2.png
