---
pageTitle: Synonyms in Azure Search (preview) | Microsoft Docs
description: "Documentação preliminar para o recurso de sinônimos (versão prévia), exposto na API REST do Azure Search."
services: search
documentationCenter: 
authors: mhko
manager: pablocas
editor: 
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/07/2016
ms.author: nateko
ms.openlocfilehash: 739a0ad77c68ea74ec25bc80c7539ac8b3f18201
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="synonyms-in-azure-search-preview"></a><span data-ttu-id="88342-102">Sinônimos no Azure Search (versão prévia)</span><span class="sxs-lookup"><span data-stu-id="88342-102">Synonyms in Azure Search (preview)</span></span>

<span data-ttu-id="88342-103">Sinônimos nos termos equivalentes associados do mecanismo de pesquisa que expandem implicitamente o escopo de uma consulta, sem que o usuário tenha de fornecer realmente o termo.</span><span class="sxs-lookup"><span data-stu-id="88342-103">Synonyms in search engines associate equivalent terms that implicitly expand the scope of a query, without the user having to actually provide the term.</span></span> <span data-ttu-id="88342-104">Por exemplo, considerando o termo "cão" e as associações de sinônimo de "canino" e "filhote de cão", qualquer documento contendo "cão", "canino" ou "filhote de cão" cairá dentro do escopo da consulta.</span><span class="sxs-lookup"><span data-stu-id="88342-104">For example, given the term "dog" and synonym associations of "canine" and "puppy", any documents containing "dog", "canine" or "puppy" will fall within the scope of the query.</span></span>

<span data-ttu-id="88342-105">No Azure Search, a expansão do sinônimo é feita no momento da consulta.</span><span class="sxs-lookup"><span data-stu-id="88342-105">In Azure Search, synonym expansion is done at query time.</span></span> <span data-ttu-id="88342-106">Você pode adicionar mapas de sinônimo a um serviço sem interromper as operações existentes.</span><span class="sxs-lookup"><span data-stu-id="88342-106">You can add synonym maps to a service with no disruption to existing operations.</span></span> <span data-ttu-id="88342-107">Você pode adicionar uma propriedade **synonymMaps** a uma definição de campo sem necessidade de recriar o índice.</span><span class="sxs-lookup"><span data-stu-id="88342-107">You can add a  **synonymMaps** property to a field definition without having to rebuild the index.</span></span> <span data-ttu-id="88342-108">Consulte [Atualizar Índice](https://docs.microsoft.com/rest/api/searchservice/update-index) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="88342-108">For more information, see [Update Index](https://docs.microsoft.com/rest/api/searchservice/update-index).</span></span>

## <a name="feature-availability"></a><span data-ttu-id="88342-109">Disponibilidade de recursos</span><span class="sxs-lookup"><span data-stu-id="88342-109">Feature availability</span></span>

<span data-ttu-id="88342-110">O recurso de sinônimos está atualmente em versão prévia e só tem suporte na última api-version da versão prévia (api-version=2016-09-01-Preview).</span><span class="sxs-lookup"><span data-stu-id="88342-110">The synonyms feature is currently in preview and only supported in the latest preview api-version (api-version=2016-09-01-Preview).</span></span> <span data-ttu-id="88342-111">Não há suporte do portal do Azure no momento.</span><span class="sxs-lookup"><span data-stu-id="88342-111">There is no Azure portal support at this time.</span></span> <span data-ttu-id="88342-112">Como a versão da API é especificada na solicitação, é possível combinar APIs de versão prévia e disponibilidade geral (GA) no mesmo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="88342-112">Because the API version is specified on the request, it's possible to combine generally available (GA) and preview APIs in the same app.</span></span> <span data-ttu-id="88342-113">No entanto, as APIs de versão prévia não estão no SLA e os recursos podem mudar, portanto, não recomendamos usá-las em aplicativos de produção.</span><span class="sxs-lookup"><span data-stu-id="88342-113">However, preview APIs are not under SLA and features may change, so we do not recommend using them in production applications.</span></span>

## <a name="how-to-use-synonyms-in-azure-search"></a><span data-ttu-id="88342-114">Como usar sinônimos no Azure Search</span><span class="sxs-lookup"><span data-stu-id="88342-114">How to use synonyms in Azure search</span></span>

<span data-ttu-id="88342-115">No Azure Search, suporte a sinônimos baseia-se em mapas de sinônimo que você define e carrega em seu serviço.</span><span class="sxs-lookup"><span data-stu-id="88342-115">In Azure Search, synonym support is based on synonym maps that you define and upload to your service.</span></span> <span data-ttu-id="88342-116">Esses mapas constituem um recurso independente (como índices ou fontes de dados) e podem ser usados por qualquer campo pesquisável em um índice do serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="88342-116">These maps constitute an independent resource (like indexes or data sources), and can be used by any searchable field in any index in your search service.</span></span>

<span data-ttu-id="88342-117">Mapas de sinônimo e índices são mantidos de maneira independente.</span><span class="sxs-lookup"><span data-stu-id="88342-117">Synonym maps and indexes are maintained independently.</span></span> <span data-ttu-id="88342-118">Depois de definir um mapa de sinônimo e carregá-lo em seu serviço, habilite o recurso de sinônimo em um campo, adicionando uma nova propriedade chamada **synonymMaps** à definição de campo.</span><span class="sxs-lookup"><span data-stu-id="88342-118">Once you define a synonym map and upload it to your service, you can enable the synonym feature on a field by adding a new property called **synonymMaps** in the field definition.</span></span> <span data-ttu-id="88342-119">Criar, atualizar e excluir um mapa de sinônimo é sempre uma operação de documento inteiro, o que significa que você não pode criar, atualizar nem excluir partes do mapa sinônimo incrementalmente.</span><span class="sxs-lookup"><span data-stu-id="88342-119">Creating, updating, and deleting a synonym map is always a whole-document operation, meaning that you cannot create, update or delete parts of the synonym map incrementally.</span></span> <span data-ttu-id="88342-120">Até mesmo uma única entrada a atualização requer um recarregamento.</span><span class="sxs-lookup"><span data-stu-id="88342-120">Updating even a single entry requires a reload.</span></span>

<span data-ttu-id="88342-121">A incorporação de sinônimos ao seu aplicativo de pesquisa é um processo de duas etapas:</span><span class="sxs-lookup"><span data-stu-id="88342-121">Incorporating synonyms into your search application is a two-step process:</span></span>

1.  <span data-ttu-id="88342-122">Adicione um mapa de sinônimos ao serviço de pesquisa por meio das APIs a seguir.</span><span class="sxs-lookup"><span data-stu-id="88342-122">Add a synonym map to your search service through the APIs below.</span></span>  

2.  <span data-ttu-id="88342-123">Configure um campo de pesquisa para usar o mapa de sinônimos na definição do índice.</span><span class="sxs-lookup"><span data-stu-id="88342-123">Configure a searchable field to use the synonym map in the index definition.</span></span>

### <a name="synonymmaps-resource-apis"></a><span data-ttu-id="88342-124">APIs do recurso SynonymMaps</span><span class="sxs-lookup"><span data-stu-id="88342-124">SynonymMaps Resource APIs</span></span>

#### <a name="add-or-update-a-synonym-map-under-your-service-using-post-or-put"></a><span data-ttu-id="88342-125">Adicione ou atualize um mapa de sinônimos em seu serviço, usando POST ou PUT.</span><span class="sxs-lookup"><span data-stu-id="88342-125">Add or update a synonym map under your service, using POST or PUT.</span></span>

<span data-ttu-id="88342-126">Mapas de sinônimos são carregados no serviço via POST ou PUT.</span><span class="sxs-lookup"><span data-stu-id="88342-126">Synonym maps are uploaded to the service via POST or PUT.</span></span> <span data-ttu-id="88342-127">Cada regra deve ser delimitada por um caractere de nova linha ('\n').</span><span class="sxs-lookup"><span data-stu-id="88342-127">Each rule must be delimited by the new line character ('\n').</span></span> <span data-ttu-id="88342-128">É possível definir até 5.000 regras por mapa de sinônimos em um serviço gratuito e 10.000 regras em todas as outras SKUs.</span><span class="sxs-lookup"><span data-stu-id="88342-128">You can define up to 5,000 rules per synonym map in a free service and 10,000 rules in all other SKUs.</span></span> <span data-ttu-id="88342-129">Cada regra pode ter até 20 expansões.</span><span class="sxs-lookup"><span data-stu-id="88342-129">Each rule can have up to 20 expansions.</span></span>

<span data-ttu-id="88342-130">Nesta versão prévia, os mapas de sinônimos devem estar no formato Apache Solr explicado abaixo.</span><span class="sxs-lookup"><span data-stu-id="88342-130">In this preview, synonym maps must be in the Apache Solr format which is explained below.</span></span> <span data-ttu-id="88342-131">Se você tiver um dicionário de sinônimos em um formato diferente e quiser usá-lo diretamente, informe-nos no [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="88342-131">If you have an existing synonym dictionary in a different format and want to use it directly, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

<span data-ttu-id="88342-132">Crie um novo mapa de sinônimos usando HTTP POST, como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="88342-132">You can create a new synonym map using HTTP POST, as in the following example:</span></span>

    POST https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "name":"mysynonymmap",
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

<span data-ttu-id="88342-133">Como alternativa, use PUT e especifique o nome do mapa de sinônimos no URI.</span><span class="sxs-lookup"><span data-stu-id="88342-133">Alternatively, you can use PUT and specify the synonym map name on the URI.</span></span> <span data-ttu-id="88342-134">Se o mapa de sinônimos não existir, ele será criado.</span><span class="sxs-lookup"><span data-stu-id="88342-134">If the synonym map does not exist, it will be created.</span></span>

    PUT https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

##### <a name="apache-solr-synonym-format"></a><span data-ttu-id="88342-135">Formato de sinônimo Apache Solr</span><span class="sxs-lookup"><span data-stu-id="88342-135">Apache Solr synonym format</span></span>

<span data-ttu-id="88342-136">O formato Solr dá suporte a mapeamentos de sinônimo equivalentes e explícitos.</span><span class="sxs-lookup"><span data-stu-id="88342-136">The Solr format supports equivalent and explicit synonym mappings.</span></span> <span data-ttu-id="88342-137">Regras de mapeamento são compatíveis com a especificação de filtro de sinônimo de software livre do Apache Solr, descritos neste documento: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span><span class="sxs-lookup"><span data-stu-id="88342-137">Mapping rules adhere to the open source synonym filter specification of Apache Solr, described in this document: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span></span> <span data-ttu-id="88342-138">Abaixo está um exemplo de regra de sinônimos equivalentes.</span><span class="sxs-lookup"><span data-stu-id="88342-138">Below is a sample rule for equivalent synonyms.</span></span>
```
              USA, United States, United States of America
```

<span data-ttu-id="88342-139">Com a regra acima, uma consulta de pesquisa "EUA" será expandida para "EUA" OR "Estados Unidos" OR "Estados Unidos da América".</span><span class="sxs-lookup"><span data-stu-id="88342-139">With the rule above, a search query "USA" will expand to "USA" OR "United States" OR "United States of America".</span></span>

<span data-ttu-id="88342-140">Mapeamento explícito é indicado por uma seta "=>".</span><span class="sxs-lookup"><span data-stu-id="88342-140">Explicit mapping is denoted by an arrow "=>".</span></span> <span data-ttu-id="88342-141">Quando especificado, uma sequência de termos de uma consulta de pesquisa que corresponda à esquerda de "=>" será substituída com as alternativas do lado direito.</span><span class="sxs-lookup"><span data-stu-id="88342-141">When specified, a term sequence of a search query that matches the left hand side of "=>" will be replaced with the alternatives on the right hand side.</span></span> <span data-ttu-id="88342-142">Dada a regra abaixo, consultas de pesquisa "Washington", "Wash."</span><span class="sxs-lookup"><span data-stu-id="88342-142">Given the rule below, search queries "Washington", "Wash."</span></span> <span data-ttu-id="88342-143">ou "WA" serão regravadas como "WA".</span><span class="sxs-lookup"><span data-stu-id="88342-143">or "WA" will all be rewritten to "WA".</span></span> <span data-ttu-id="88342-144">Mapeamento explícito só é aplicável na direção especificada e não regrava a consulta "WA" para "Washington" nesse caso.</span><span class="sxs-lookup"><span data-stu-id="88342-144">Explicit mapping only applies in the direction specified and does not rewrite the query "WA" to "Washington" in this case.</span></span>
```
              Washington, Wash., WA => WA
```

#### <a name="list-synonym-maps-under-your-service"></a><span data-ttu-id="88342-145">Liste os mapas de sinônimos em seu serviço.</span><span class="sxs-lookup"><span data-stu-id="88342-145">List synonym maps under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="get-a-synonym-map-under-your-service"></a><span data-ttu-id="88342-146">Obtenha um mapa de sinônimos em seu serviço.</span><span class="sxs-lookup"><span data-stu-id="88342-146">Get a synonym map under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="delete-a-synonyms-map-under-your-service"></a><span data-ttu-id="88342-147">Exclua um mapa de sinônimos em seu serviço.</span><span class="sxs-lookup"><span data-stu-id="88342-147">Delete a synonyms map under your service.</span></span>

    DELETE https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

### <a name="configure-a-searchable-field-to-use-the-synonym-map-in-the-index-definition"></a><span data-ttu-id="88342-148">Configure um campo de pesquisa para usar o mapa de sinônimos na definição do índice.</span><span class="sxs-lookup"><span data-stu-id="88342-148">Configure a searchable field to use the synonym map in the index definition.</span></span>

<span data-ttu-id="88342-149">Uma nova propriedade de campo **synonymMaps** pode ser usada a fim de especificar um mapa de sinônimos para usar em um campo pesquisável.</span><span class="sxs-lookup"><span data-stu-id="88342-149">A new field property **synonymMaps** can be used to specify a synonym map to use for a searchable field.</span></span> <span data-ttu-id="88342-150">Mapas de sinônimos são recursos de nível de serviço e podem ser consultados por qualquer campo de um índice no serviço.</span><span class="sxs-lookup"><span data-stu-id="88342-150">Synonym maps are service level resources and can be referenced by any field of an index under the service.</span></span>

    POST https://[servicename].search.windows.net/indexes?api-version=2016-09-01-Preview
    api-key: [admin key]

    {
       "name":"myindex",
       "fields":[
          {
             "name":"id",
             "type":"Edm.String",
             "key":true
          },
          {
             "name":"name",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"en.lucene",
             "synonymMaps":[
                "mysynonymmap"
             ]
          },
          {
             "name":"name_jp",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"ja.microsoft",
             "synonymMaps":[
                "japanesesynonymmap"
             ]
          }
       ]
    }

<span data-ttu-id="88342-151">**synonymMaps** pode ser especificado para campos de pesquisa do tipo “Edm.String” ou “Collection(Edm.String)”.</span><span class="sxs-lookup"><span data-stu-id="88342-151">**synonymMaps** can be specified for searchable fields of the type 'Edm.String' or 'Collection(Edm.String)'.</span></span>

> [!NOTE]
> <span data-ttu-id="88342-152">Nesta versão prévia, só pode haver um mapa de sinônimos por campo.</span><span class="sxs-lookup"><span data-stu-id="88342-152">In this preview, you can only have one synonym map per field.</span></span> <span data-ttu-id="88342-153">Se você quiser usar vários mapas de sinônimo, informe-nos no [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="88342-153">If you want to use multiple synonym maps, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

## <a name="impact-of-synonyms-on-other-search-features"></a><span data-ttu-id="88342-154">Impacto de sinônimos em outros recursos de pesquisa</span><span class="sxs-lookup"><span data-stu-id="88342-154">Impact of synonyms on other search features</span></span>

<span data-ttu-id="88342-155">O recurso de sinônimos regrava a consulta original com sinônimos com o operador OR.</span><span class="sxs-lookup"><span data-stu-id="88342-155">The synonyms feature rewrites the original query with synonyms with the OR operator.</span></span> <span data-ttu-id="88342-156">Por esse motivo, os perfis de destaque e pontuação acessados tratam o termo original e os sinônimos como equivalentes.</span><span class="sxs-lookup"><span data-stu-id="88342-156">For this reason, hit highlighting and scoring profiles treat the original term and synonyms as equivalent.</span></span>

<span data-ttu-id="88342-157">O recurso de sinônimo aplica-se a consultas de pesquisa e não se aplicam a filtros ou facetas.</span><span class="sxs-lookup"><span data-stu-id="88342-157">Synonym feature applies to search queries and does not apply to filters or facets.</span></span> <span data-ttu-id="88342-158">Da mesma forma, sugestões baseiam-se apenas no termo original; correspondências de sinônimo não aparecem na resposta.</span><span class="sxs-lookup"><span data-stu-id="88342-158">Similarly, suggestions are based only on the original term; synonym matches do not appear in the response.</span></span>

<span data-ttu-id="88342-159">Expansões de sinônimo não se aplicam a termos de pesquisa de curinga; prefixo, lógica difusa e termos de regex não são expandidos.</span><span class="sxs-lookup"><span data-stu-id="88342-159">Synonym expansions do not apply to wildcard search terms; prefix, fuzzy, and regex terms aren't expanded.</span></span>

## <a name="tips-for-building-a-synonym-map"></a><span data-ttu-id="88342-160">Dicas para criação de um mapa de sinônimos</span><span class="sxs-lookup"><span data-stu-id="88342-160">Tips for building a synonym map</span></span>

- <span data-ttu-id="88342-161">Um mapa de sinônimos conciso e bem projetado é mais eficiente do que uma lista de possíveis correspondências.</span><span class="sxs-lookup"><span data-stu-id="88342-161">A concise, well-designed synonym map is more efficient than an exhaustive list of possible matches.</span></span> <span data-ttu-id="88342-162">Dicionários excessivamente grandes ou complexos demorarão mais para serem analisados e afetarão a latência se a consulta expandir muitos sinônimos.</span><span class="sxs-lookup"><span data-stu-id="88342-162">Excessively large or complex dictionaries take longer to parse and affect the query latency if the query expands to many synonyms.</span></span> <span data-ttu-id="88342-163">Em vez de adivinhar o termo a ser usado, você pode obter os termos reais por meio de um [relatório de análise de tráfego de pesquisa](search-traffic-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="88342-163">Rather than guess at which terms might be used, you can get the actual terms via a [search traffic analysis report](search-traffic-analytics.md).</span></span>

- <span data-ttu-id="88342-164">Como um exercício preliminar e de validação, habilite e use esse relatório para determinar exatamente quais termos se beneficiarão de uma correspondência de sinônimo e continue a usá-lo como validação de que o mapa de sinônimos está produzindo resultado melhor.</span><span class="sxs-lookup"><span data-stu-id="88342-164">As both a preliminary and validation exercise, enable and then use this report to precisely determine which terms will benefit from a synonym match, and then continue to use it as validation that your synonym map is producing a better outcome.</span></span> <span data-ttu-id="88342-165">No relatório predefinido, os blocos "Consultas de pesquisa mais comuns" e "Consultas de pesquisa de resultado zero" fornecerão a você as informações necessárias.</span><span class="sxs-lookup"><span data-stu-id="88342-165">In the predefined report, the tiles "Most common search queries" and "Zero-result search queries" will give you the necessary information.</span></span>

- <span data-ttu-id="88342-166">Você pode criar vários mapas de sinônimos para o aplicativo de pesquisa (por exemplo, por idioma, se seu aplicativo dá suporte a uma base de clientes com vários idiomas).</span><span class="sxs-lookup"><span data-stu-id="88342-166">You can create multiple synonym maps for your search application (for example, by language if your application supports a multi-lingual customer base).</span></span> <span data-ttu-id="88342-167">Atualmente, um campo só pode usar um deles.</span><span class="sxs-lookup"><span data-stu-id="88342-167">Currently, a field can only use one of them.</span></span> <span data-ttu-id="88342-168">Atualize a propriedade synonymMaps de um campo a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="88342-168">You can update a field's synonymMaps property at any time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88342-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="88342-169">Next Steps</span></span>

- <span data-ttu-id="88342-170">Se houver um índice em um ambiente de desenvolvimento (não produção), experimente um dicionário pequeno para ver como a adição de sinônimos altera a experiência de pesquisa, incluindo o impacto nos perfis de pontuação, o realce de acesso e as sugestões.</span><span class="sxs-lookup"><span data-stu-id="88342-170">If you have an existing index in a development (non-production) environment, experiment with a small dictionary to see how the addition of synonyms changes the search experience, including impact on scoring profiles, hit highlighting, and suggestions.</span></span>

- <span data-ttu-id="88342-171">[Habilite a análise de tráfego de pesquisa](search-traffic-analytics.md) e use o relatório do Power BI predefinido para saber quais termos são os mais usados e quais retornam zero documentos.</span><span class="sxs-lookup"><span data-stu-id="88342-171">[Enable search traffic analytics](search-traffic-analytics.md) and use the predefined Power BI report to learn which terms are used the most, and which ones return zero documents.</span></span> <span data-ttu-id="88342-172">Armado com essa visão, revise o dicionário para incluir sinônimos de consultas improdutivas que devem ser resolvidas para documentos no índice.</span><span class="sxs-lookup"><span data-stu-id="88342-172">Armed with these insights, revise the dictionary to include synonyms for unproductive queries that should be resolving to documents in your index.</span></span>
