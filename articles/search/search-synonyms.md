---
pageTitle: Synonyms in Azure Search (preview) | Microsoft Docs
description: "Documentação preliminar para o recurso de sinônimos (visualização) hello, exposto em Olá API de REST de pesquisa do Azure."
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
ms.openlocfilehash: 2695139d2b298fa2e7c1814715fdf96729f594ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="synonyms-in-azure-search-preview"></a><span data-ttu-id="74936-102">Sinônimos no Azure Search (versão prévia)</span><span class="sxs-lookup"><span data-stu-id="74936-102">Synonyms in Azure Search (preview)</span></span>

<span data-ttu-id="74936-103">Sinônimos nos mecanismos de pesquisa associar termos equivalentes que implicitamente expandem o escopo da saudação de uma consulta, sem ter tooactually fornecem os termos de saudação do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="74936-103">Synonyms in search engines associate equivalent terms that implicitly expand hello scope of a query, without hello user having tooactually provide hello term.</span></span> <span data-ttu-id="74936-104">Por exemplo, termo de determinado hello "dog" e associações de sinônimo de "canino" e "filhote de cachorro", todos os documentos que contenham "dog", "canino" ou "filhote de cachorro" corresponderá no escopo de saudação de consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="74936-104">For example, given hello term "dog" and synonym associations of "canine" and "puppy", any documents containing "dog", "canine" or "puppy" will fall within hello scope of hello query.</span></span>

<span data-ttu-id="74936-105">No Azure Search, a expansão do sinônimo é feita no momento da consulta.</span><span class="sxs-lookup"><span data-stu-id="74936-105">In Azure Search, synonym expansion is done at query time.</span></span> <span data-ttu-id="74936-106">Você pode adicionar sinônimo mapas tooa serviço sem operações de tooexisting de interrupção.</span><span class="sxs-lookup"><span data-stu-id="74936-106">You can add synonym maps tooa service with no disruption tooexisting operations.</span></span> <span data-ttu-id="74936-107">Você pode adicionar uma **synonymMaps** definição de campo propriedade tooa sem toorebuild Olá índice.</span><span class="sxs-lookup"><span data-stu-id="74936-107">You can add a  **synonymMaps** property tooa field definition without having toorebuild hello index.</span></span> <span data-ttu-id="74936-108">Consulte [Atualizar Índice](https://docs.microsoft.com/rest/api/searchservice/update-index) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="74936-108">For more information, see [Update Index](https://docs.microsoft.com/rest/api/searchservice/update-index).</span></span>

## <a name="feature-availability"></a><span data-ttu-id="74936-109">Disponibilidade de recursos</span><span class="sxs-lookup"><span data-stu-id="74936-109">Feature availability</span></span>

<span data-ttu-id="74936-110">sinônimos Olá recurso está atualmente em visualização e somente tem suporte no hello versão de api de visualização mais recente (api-version = 2016-09-01-Preview).</span><span class="sxs-lookup"><span data-stu-id="74936-110">hello synonyms feature is currently in preview and only supported in hello latest preview api-version (api-version=2016-09-01-Preview).</span></span> <span data-ttu-id="74936-111">Não há suporte do portal do Azure no momento.</span><span class="sxs-lookup"><span data-stu-id="74936-111">There is no Azure portal support at this time.</span></span> <span data-ttu-id="74936-112">Como Olá API versão for especificada na solicitação Olá, é possível toocombine disponibilidade geral (GA) e APIs de visualização no hello mesmo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="74936-112">Because hello API version is specified on hello request, it's possible toocombine generally available (GA) and preview APIs in hello same app.</span></span> <span data-ttu-id="74936-113">No entanto, as APIs de versão prévia não estão no SLA e os recursos podem mudar, portanto, não recomendamos usá-las em aplicativos de produção.</span><span class="sxs-lookup"><span data-stu-id="74936-113">However, preview APIs are not under SLA and features may change, so we do not recommend using them in production applications.</span></span>

## <a name="how-toouse-synonyms-in-azure-search"></a><span data-ttu-id="74936-114">Como a pesquisa de sinônimos toouse no Azure</span><span class="sxs-lookup"><span data-stu-id="74936-114">How toouse synonyms in Azure search</span></span>

<span data-ttu-id="74936-115">Na pesquisa do Azure, suporte de sinônimo baseia-se em mapas que você define e carregar o serviço tooyour de sinônimo.</span><span class="sxs-lookup"><span data-stu-id="74936-115">In Azure Search, synonym support is based on synonym maps that you define and upload tooyour service.</span></span> <span data-ttu-id="74936-116">Esses mapas constituem um recurso independente (como índices ou fontes de dados) e podem ser usados por qualquer campo pesquisável em um índice do serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="74936-116">These maps constitute an independent resource (like indexes or data sources), and can be used by any searchable field in any index in your search service.</span></span>

<span data-ttu-id="74936-117">Mapas de sinônimo e índices são mantidos de maneira independente.</span><span class="sxs-lookup"><span data-stu-id="74936-117">Synonym maps and indexes are maintained independently.</span></span> <span data-ttu-id="74936-118">Depois de definir um mapa de sinônimo e carregue-o serviço de tooyour, você pode habilitar o recurso de sinônimo de saudação em um campo, adicionando uma nova propriedade chamada **synonymMaps** na definição de campo hello.</span><span class="sxs-lookup"><span data-stu-id="74936-118">Once you define a synonym map and upload it tooyour service, you can enable hello synonym feature on a field by adding a new property called **synonymMaps** in hello field definition.</span></span> <span data-ttu-id="74936-119">Criar, atualizar e excluir que um mapa de sinônimo é sempre uma operação do documento inteiro, que significa que você não pode criar, atualizar ou excluir partes de mapa de sinônimo Olá incrementalmente.</span><span class="sxs-lookup"><span data-stu-id="74936-119">Creating, updating, and deleting a synonym map is always a whole-document operation, meaning that you cannot create, update or delete parts of hello synonym map incrementally.</span></span> <span data-ttu-id="74936-120">Até mesmo uma única entrada a atualização requer um recarregamento.</span><span class="sxs-lookup"><span data-stu-id="74936-120">Updating even a single entry requires a reload.</span></span>

<span data-ttu-id="74936-121">A incorporação de sinônimos ao seu aplicativo de pesquisa é um processo de duas etapas:</span><span class="sxs-lookup"><span data-stu-id="74936-121">Incorporating synonyms into your search application is a two-step process:</span></span>

1.  <span data-ttu-id="74936-122">Adicione um serviço de pesquisa do sinônimo mapa tooyour por meio de saudação APIs abaixo.</span><span class="sxs-lookup"><span data-stu-id="74936-122">Add a synonym map tooyour search service through hello APIs below.</span></span>  

2.  <span data-ttu-id="74936-123">Configure um campo pesquisável toouse Olá sinônimo mapa na definição de índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="74936-123">Configure a searchable field toouse hello synonym map in hello index definition.</span></span>

### <a name="synonymmaps-resource-apis"></a><span data-ttu-id="74936-124">APIs do recurso SynonymMaps</span><span class="sxs-lookup"><span data-stu-id="74936-124">SynonymMaps Resource APIs</span></span>

#### <a name="add-or-update-a-synonym-map-under-your-service-using-post-or-put"></a><span data-ttu-id="74936-125">Adicione ou atualize um mapa de sinônimos em seu serviço, usando POST ou PUT.</span><span class="sxs-lookup"><span data-stu-id="74936-125">Add or update a synonym map under your service, using POST or PUT.</span></span>

<span data-ttu-id="74936-126">Mapas de sinônimo são carregados toohello serviço via POST ou PUT.</span><span class="sxs-lookup"><span data-stu-id="74936-126">Synonym maps are uploaded toohello service via POST or PUT.</span></span> <span data-ttu-id="74936-127">Cada regra deve ser delimitada por Olá caractere de nova linha ('\n').</span><span class="sxs-lookup"><span data-stu-id="74936-127">Each rule must be delimited by hello new line character ('\n').</span></span> <span data-ttu-id="74936-128">Você pode definir too5, 000 regras por mapa de sinônimo em um serviço gratuito e 10.000 regras em todos os outros SKUs.</span><span class="sxs-lookup"><span data-stu-id="74936-128">You can define up too5,000 rules per synonym map in a free service and 10,000 rules in all other SKUs.</span></span> <span data-ttu-id="74936-129">Cada regra pode ter até too20 expansões.</span><span class="sxs-lookup"><span data-stu-id="74936-129">Each rule can have up too20 expansions.</span></span>

<span data-ttu-id="74936-130">Nesta visualização, mapas de sinônimo devem estar no formato de Apache Solr de saudação que é explicado abaixo.</span><span class="sxs-lookup"><span data-stu-id="74936-130">In this preview, synonym maps must be in hello Apache Solr format which is explained below.</span></span> <span data-ttu-id="74936-131">Se você tiver um dicionário de sinônimo existente em um formato diferente e quiser toouse-lo diretamente, informe-em [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="74936-131">If you have an existing synonym dictionary in a different format and want toouse it directly, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

<span data-ttu-id="74936-132">Você pode criar um novo mapa de sinônimo usando HTTP POST, como no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="74936-132">You can create a new synonym map using HTTP POST, as in hello following example:</span></span>

    POST https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "name":"mysynonymmap",
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

<span data-ttu-id="74936-133">Como alternativa, você pode usar PUT e especificar o nome do mapa de sinônimo Olá em Olá URI.</span><span class="sxs-lookup"><span data-stu-id="74936-133">Alternatively, you can use PUT and specify hello synonym map name on hello URI.</span></span> <span data-ttu-id="74936-134">Se o mapa de sinônimo Olá não existir, ele será criado.</span><span class="sxs-lookup"><span data-stu-id="74936-134">If hello synonym map does not exist, it will be created.</span></span>

    PUT https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

##### <a name="apache-solr-synonym-format"></a><span data-ttu-id="74936-135">Formato de sinônimo Apache Solr</span><span class="sxs-lookup"><span data-stu-id="74936-135">Apache Solr synonym format</span></span>

<span data-ttu-id="74936-136">formato de Solr Olá dá suporte aos mapeamentos de sinônimo equivalente e explícitas.</span><span class="sxs-lookup"><span data-stu-id="74936-136">hello Solr format supports equivalent and explicit synonym mappings.</span></span> <span data-ttu-id="74936-137">As regras de mapeamento aderem a especificação de filtro de sinônimo toohello código-fonte aberto do Apache Solr, descritas neste documento: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span><span class="sxs-lookup"><span data-stu-id="74936-137">Mapping rules adhere toohello open source synonym filter specification of Apache Solr, described in this document: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span></span> <span data-ttu-id="74936-138">Abaixo está um exemplo de regra de sinônimos equivalentes.</span><span class="sxs-lookup"><span data-stu-id="74936-138">Below is a sample rule for equivalent synonyms.</span></span>
```
              USA, United States, United States of America
```

<span data-ttu-id="74936-139">Com a regra de saudação acima, um consulta de pesquisa "EUA" expandirá muito "EUA" ou "EUA" ou "Estados Unidos da América".</span><span class="sxs-lookup"><span data-stu-id="74936-139">With hello rule above, a search query "USA" will expand too"USA" OR "United States" OR "United States of America".</span></span>

<span data-ttu-id="74936-140">Mapeamento explícito é indicado por uma seta "=>".</span><span class="sxs-lookup"><span data-stu-id="74936-140">Explicit mapping is denoted by an arrow "=>".</span></span> <span data-ttu-id="74936-141">Quando especificado, uma sequência de prazo de uma consulta de pesquisa que corresponda a saudação esquerda de "= >" será substituído pelo alternativas Olá no lado direito hello.</span><span class="sxs-lookup"><span data-stu-id="74936-141">When specified, a term sequence of a search query that matches hello left hand side of "=>" will be replaced with hello alternatives on hello right hand side.</span></span> <span data-ttu-id="74936-142">Dada a regra de saudação abaixo, consultas de pesquisa "Washington", "Washington."</span><span class="sxs-lookup"><span data-stu-id="74936-142">Given hello rule below, search queries "Washington", "Wash."</span></span> <span data-ttu-id="74936-143">ou "WA" será todos regravado muito "WA".</span><span class="sxs-lookup"><span data-stu-id="74936-143">or "WA" will all be rewritten too"WA".</span></span> <span data-ttu-id="74936-144">Mapeamento explícito aplica-se em direção de saudação especificada e não regravar consulta hello "WA" muito "Washington" neste caso.</span><span class="sxs-lookup"><span data-stu-id="74936-144">Explicit mapping only applies in hello direction specified and does not rewrite hello query "WA" too"Washington" in this case.</span></span>
```
              Washington, Wash., WA => WA
```

#### <a name="list-synonym-maps-under-your-service"></a><span data-ttu-id="74936-145">Liste os mapas de sinônimos em seu serviço.</span><span class="sxs-lookup"><span data-stu-id="74936-145">List synonym maps under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="get-a-synonym-map-under-your-service"></a><span data-ttu-id="74936-146">Obtenha um mapa de sinônimos em seu serviço.</span><span class="sxs-lookup"><span data-stu-id="74936-146">Get a synonym map under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="delete-a-synonyms-map-under-your-service"></a><span data-ttu-id="74936-147">Exclua um mapa de sinônimos em seu serviço.</span><span class="sxs-lookup"><span data-stu-id="74936-147">Delete a synonyms map under your service.</span></span>

    DELETE https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

### <a name="configure-a-searchable-field-toouse-hello-synonym-map-in-hello-index-definition"></a><span data-ttu-id="74936-148">Configure um campo pesquisável toouse Olá sinônimo mapa na definição de índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="74936-148">Configure a searchable field toouse hello synonym map in hello index definition.</span></span>

<span data-ttu-id="74936-149">Uma nova propriedade de campo **synonymMaps** pode ser usado toospecify toouse de mapa um sinônimo para um campo pesquisável.</span><span class="sxs-lookup"><span data-stu-id="74936-149">A new field property **synonymMaps** can be used toospecify a synonym map toouse for a searchable field.</span></span> <span data-ttu-id="74936-150">Mapas de sinônimo são recursos de nível de serviço e podem ser referenciados por qualquer campo de um índice no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="74936-150">Synonym maps are service level resources and can be referenced by any field of an index under hello service.</span></span>

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

<span data-ttu-id="74936-151">**synonymMaps** podem ser especificados para campos de pesquisa de tipo de saudação 'EDM. String' ou 'Collection'.</span><span class="sxs-lookup"><span data-stu-id="74936-151">**synonymMaps** can be specified for searchable fields of hello type 'Edm.String' or 'Collection(Edm.String)'.</span></span>

> [!NOTE]
> <span data-ttu-id="74936-152">Nesta versão prévia, só pode haver um mapa de sinônimos por campo.</span><span class="sxs-lookup"><span data-stu-id="74936-152">In this preview, you can only have one synonym map per field.</span></span> <span data-ttu-id="74936-153">Se você quiser toouse vários mapas de sinônimo, informe-em [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span><span class="sxs-lookup"><span data-stu-id="74936-153">If you want toouse multiple synonym maps, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

## <a name="impact-of-synonyms-on-other-search-features"></a><span data-ttu-id="74936-154">Impacto de sinônimos em outros recursos de pesquisa</span><span class="sxs-lookup"><span data-stu-id="74936-154">Impact of synonyms on other search features</span></span>

<span data-ttu-id="74936-155">recurso de sinônimos Olá reconfigura a consulta original Olá com sinônimos com hello operador OR.</span><span class="sxs-lookup"><span data-stu-id="74936-155">hello synonyms feature rewrites hello original query with synonyms with hello OR operator.</span></span> <span data-ttu-id="74936-156">Por esse motivo, realce de ocorrências e perfis de pontuação tratam termo original hello e sinônimos como equivalentes.</span><span class="sxs-lookup"><span data-stu-id="74936-156">For this reason, hit highlighting and scoring profiles treat hello original term and synonyms as equivalent.</span></span>

<span data-ttu-id="74936-157">Recurso de sinônimo se aplica a consultas de toosearch e não se aplica a toofilters ou facetas.</span><span class="sxs-lookup"><span data-stu-id="74936-157">Synonym feature applies toosearch queries and does not apply toofilters or facets.</span></span> <span data-ttu-id="74936-158">Da mesma forma, as sugestões são baseadas apenas no termo original da saudação; correspondências de sinônimo não apareceu na resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="74936-158">Similarly, suggestions are based only on hello original term; synonym matches do not appear in hello response.</span></span>

<span data-ttu-id="74936-159">Expansões de sinônimo não se aplicam a termos de pesquisa toowildcard; prefixo, difuso e os termos de regex não são expandidas.</span><span class="sxs-lookup"><span data-stu-id="74936-159">Synonym expansions do not apply toowildcard search terms; prefix, fuzzy, and regex terms aren't expanded.</span></span>

## <a name="tips-for-building-a-synonym-map"></a><span data-ttu-id="74936-160">Dicas para criação de um mapa de sinônimos</span><span class="sxs-lookup"><span data-stu-id="74936-160">Tips for building a synonym map</span></span>

- <span data-ttu-id="74936-161">Um mapa de sinônimos conciso e bem projetado é mais eficiente do que uma lista de possíveis correspondências.</span><span class="sxs-lookup"><span data-stu-id="74936-161">A concise, well-designed synonym map is more efficient than an exhaustive list of possible matches.</span></span> <span data-ttu-id="74936-162">Dicionários excessivamente grandes ou complexos levar mais tempo tooparse e afetam a latência da consulta Olá se consulta Olá expande toomany sinônimos.</span><span class="sxs-lookup"><span data-stu-id="74936-162">Excessively large or complex dictionaries take longer tooparse and affect hello query latency if hello query expands toomany synonyms.</span></span> <span data-ttu-id="74936-163">Em vez de estimativa na qual os termos podem ser usados, você pode obter os termos de saudação real por meio de um [relatório de análise de tráfego de pesquisa](search-traffic-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="74936-163">Rather than guess at which terms might be used, you can get hello actual terms via a [search traffic analysis report](search-traffic-analytics.md).</span></span>

- <span data-ttu-id="74936-164">Como um preliminar e a validação exercício, habilitar e, em seguida, use esse relatório tooprecisely determinar quais termos se beneficiar de uma correspondência de sinônimo e continue toouse como validação que o mapa de sinônimo está produzindo um resultado melhor.</span><span class="sxs-lookup"><span data-stu-id="74936-164">As both a preliminary and validation exercise, enable and then use this report tooprecisely determine which terms will benefit from a synonym match, and then continue toouse it as validation that your synonym map is producing a better outcome.</span></span> <span data-ttu-id="74936-165">No relatório de saudação predefinido, Olá blocos "consultas de pesquisa mais comuns" e "consultas de pesquisa de resultado de Zero" fornecerá Olá informações necessárias.</span><span class="sxs-lookup"><span data-stu-id="74936-165">In hello predefined report, hello tiles "Most common search queries" and "Zero-result search queries" will give you hello necessary information.</span></span>

- <span data-ttu-id="74936-166">Você pode criar vários mapas de sinônimos para o aplicativo de pesquisa (por exemplo, por idioma, se seu aplicativo dá suporte a uma base de clientes com vários idiomas).</span><span class="sxs-lookup"><span data-stu-id="74936-166">You can create multiple synonym maps for your search application (for example, by language if your application supports a multi-lingual customer base).</span></span> <span data-ttu-id="74936-167">Atualmente, um campo só pode usar um deles.</span><span class="sxs-lookup"><span data-stu-id="74936-167">Currently, a field can only use one of them.</span></span> <span data-ttu-id="74936-168">Atualize a propriedade synonymMaps de um campo a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="74936-168">You can update a field's synonymMaps property at any time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74936-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="74936-169">Next Steps</span></span>

- <span data-ttu-id="74936-170">Se você tiver um índice existente em um ambiente de desenvolvimento (não seja de produção), fazer experiências com um pequeno dicionário toosee como adição de saudação de sinônimos altera Olá experiência de pesquisa, incluindo o impacto em perfis de pontuação, ocorrências realce e sugestões.</span><span class="sxs-lookup"><span data-stu-id="74936-170">If you have an existing index in a development (non-production) environment, experiment with a small dictionary toosee how hello addition of synonyms changes hello search experience, including impact on scoring profiles, hit highlighting, and suggestions.</span></span>

- <span data-ttu-id="74936-171">[Habilitar análise de tráfego de pesquisa](search-traffic-analytics.md) e use Olá predefinidos toolearn quais termos são usados mais e quais os retorno Olá zero documentos de relatório do Power BI.</span><span class="sxs-lookup"><span data-stu-id="74936-171">[Enable search traffic analytics](search-traffic-analytics.md) and use hello predefined Power BI report toolearn which terms are used hello most, and which ones return zero documents.</span></span> <span data-ttu-id="74936-172">Armado com essas informações, revise tooinclude sinônimos dicionário Olá improdutivos consultas que devem ser Resolvendo toodocuments no índice.</span><span class="sxs-lookup"><span data-stu-id="74936-172">Armed with these insights, revise hello dictionary tooinclude synonyms for unproductive queries that should be resolving toodocuments in your index.</span></span>
