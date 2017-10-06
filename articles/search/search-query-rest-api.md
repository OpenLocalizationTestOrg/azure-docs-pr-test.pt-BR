---
title: "AAA \"consultar um índice (API REST - pesquisa do Azure) | Microsoft Docs\""
description: "Criar uma consulta de pesquisa na pesquisa do Azure e usar os resultados da pesquisa pesquisa parâmetros toofilter e classificação."
services: search
documentationcenter: 
manager: jhubbard
author: ashmaka
ms.assetid: 8b3ca890-2f5f-44b6-a140-6cb676fc2c9c
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/12/2017
ms.author: ashmaka
ms.openlocfilehash: 2f12238b8f4b045f536489cfc8766fb68307bbe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index-using-hello-rest-api"></a><span data-ttu-id="92810-103">Consultar seu índice de pesquisa do Azure usando a API REST de saudação</span><span class="sxs-lookup"><span data-stu-id="92810-103">Query your Azure Search index using hello REST API</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="92810-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="92810-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="92810-105">Portal</span><span class="sxs-lookup"><span data-stu-id="92810-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="92810-106">.NET</span><span class="sxs-lookup"><span data-stu-id="92810-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="92810-107">REST</span><span class="sxs-lookup"><span data-stu-id="92810-107">REST</span></span>](search-query-rest-api.md)
>
>

<span data-ttu-id="92810-108">Este artigo mostra como tooquery um índice usando Olá [API de REST de pesquisa do Azure](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="92810-108">This article shows you how tooquery an index using hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

<span data-ttu-id="92810-109">Antes de começar este passo a passo, você já deve ter [criado um índice do Azure Search](search-what-is-an-index.md), e este já deve estar [preenchido com os dados](search-what-is-data-import.md).</span><span class="sxs-lookup"><span data-stu-id="92810-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span> <span data-ttu-id="92810-110">Para obter informações de contexto, veja [Como funciona a pesquisa de texto completo no Azure Search](search-lucene-query-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="92810-110">For background information, see [How full text search works in Azure Search](search-lucene-query-architecture.md).</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="92810-111">Identificar sua api-key de consulta do serviço de Pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="92810-111">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="92810-112">Um componente fundamental de cada operação de pesquisa em relação a saudação API de REST de pesquisa do Azure é hello *chave de api* que foi gerado para o serviço de saudação Você provisionou.</span><span class="sxs-lookup"><span data-stu-id="92810-112">A key component of every search operation against hello Azure Search REST API is hello *api-key* that was generated for hello service you provisioned.</span></span> <span data-ttu-id="92810-113">Ter uma chave válida estabelece confiança, em uma base por solicitação, entre solicitação de envio Olá Olá aplicativo e serviço de saudação que lida com ele.</span><span class="sxs-lookup"><span data-stu-id="92810-113">Having a valid key establishes trust, on a per request basis, between hello application sending hello request and hello service that handles it.</span></span>

1. <span data-ttu-id="92810-114">toofind chaves de api do serviço, você pode entrar no toohello [portal do Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="92810-114">toofind your service's api-keys, you can sign in toohello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="92810-115">Vá folha do serviço de pesquisa do Azure tooyour</span><span class="sxs-lookup"><span data-stu-id="92810-115">Go tooyour Azure Search service's blade</span></span>
3. <span data-ttu-id="92810-116">Clique no ícone de "Chaves" hello</span><span class="sxs-lookup"><span data-stu-id="92810-116">Click hello "Keys" icon</span></span>

<span data-ttu-id="92810-117">O serviço tem *chaves de administração* e *chaves de consulta*.</span><span class="sxs-lookup"><span data-stu-id="92810-117">Your service has *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="92810-118">O primário e secundário *chaves de administração* conceder direitos totais tooall operações, incluindo Olá capacidade toomanage Olá serviço, criar e excluir índices, indexadores e fontes de dados.</span><span class="sxs-lookup"><span data-stu-id="92810-118">Your primary and secondary *admin keys* grant full rights tooall operations, including hello ability toomanage hello service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="92810-119">Há duas chaves para que você possa continuar chave secundária do toouse Olá se você decidir chave primária do tooregenerate hello e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="92810-119">There are two keys so that you can continue toouse hello secondary key if you decide tooregenerate hello primary key, and vice-versa.</span></span>
* <span data-ttu-id="92810-120">O *chaves de consulta* conceder acesso somente leitura tooindexes e documentos, e são normalmente distribuídos tooclient aplicativos que emitem solicitações de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="92810-120">Your *query keys* grant read-only access tooindexes and documents, and are typically distributed tooclient applications that issue search requests.</span></span>

<span data-ttu-id="92810-121">Para fins de saudação de consultar um índice, você pode usar uma de suas chaves de consulta.</span><span class="sxs-lookup"><span data-stu-id="92810-121">For hello purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="92810-122">As chaves de administração também podem ser usadas para consultas, mas você deve usar uma chave de consulta no código do aplicativo, isso melhor da seguinte maneira Olá [princípio de menos privilégios](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span><span class="sxs-lookup"><span data-stu-id="92810-122">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows hello [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="formulate-your-query"></a><span data-ttu-id="92810-123">Formular sua consulta</span><span class="sxs-lookup"><span data-stu-id="92810-123">Formulate your query</span></span>
<span data-ttu-id="92810-124">Há duas maneiras muito[pesquise o índice usando a API REST de saudação](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span><span class="sxs-lookup"><span data-stu-id="92810-124">There are two ways too[search your index using hello REST API](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="92810-125">Uma maneira é tooissue uma solicitação HTTP POST em que os parâmetros de consulta são definidos em um objeto JSON no corpo da solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="92810-125">One way is tooissue an HTTP POST request where your query parameters are defined in a JSON object in hello request body.</span></span> <span data-ttu-id="92810-126">saudação de outra forma é tooissue uma solicitação HTTP GET em que os parâmetros de consulta são definidos na URL de solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="92810-126">hello other way is tooissue an HTTP GET request where your query parameters are defined within hello request URL.</span></span> <span data-ttu-id="92810-127">POSTAGEM tem mais [relaxada limites](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) no tamanho de saudação de parâmetros de consulta que GET.</span><span class="sxs-lookup"><span data-stu-id="92810-127">POST has more [relaxed limits](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) on hello size of query parameters than GET.</span></span> <span data-ttu-id="92810-128">Por esse motivo, é recomendável usar POST, a menos que haja circunstâncias especiais em que o uso de GET seja mais conveniente.</span><span class="sxs-lookup"><span data-stu-id="92810-128">For this reason, we recommend using POST unless you have special circumstances where using GET would be more convenient.</span></span>

<span data-ttu-id="92810-129">Para POST e GET, você precisa tooprovide seu *nome do serviço*, *nome do índice*e hello adequada *versão da API* (Olá atual versão da API é `2016-09-01` no tempo de saudação Publicar este documento) em Olá URL da solicitação.</span><span class="sxs-lookup"><span data-stu-id="92810-129">For both POST and GET, you need tooprovide your *service name*, *index name*, and hello proper *API version* (hello current API version is `2016-09-01` at hello time of publishing this document) in hello request URL.</span></span> <span data-ttu-id="92810-130">Para obter, Olá *cadeia de caracteres de consulta* em Olá final da URL da saudação é onde você pode fornecer parâmetros de consulta hello.</span><span class="sxs-lookup"><span data-stu-id="92810-130">For GET, hello *query string* at hello end of hello URL is where you provide hello query parameters.</span></span> <span data-ttu-id="92810-131">Consulte abaixo para o formato de URL hello:</span><span class="sxs-lookup"><span data-stu-id="92810-131">See below for hello URL format:</span></span>

    https://[service name].search.windows.net/indexes/[index name]/docs?[query string]&api-version=2016-09-01

<span data-ttu-id="92810-132">saudação de formato para POST é Olá mesmo, mas com apenas uma versão de api em parâmetros de cadeia de caracteres de consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="92810-132">hello format for POST is hello same, but with only api-version in hello query string parameters.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="92810-133">Consultas de Exemplo</span><span class="sxs-lookup"><span data-stu-id="92810-133">Example Queries</span></span>
<span data-ttu-id="92810-134">Veja algumas consultas de exemplo em um índice chamado "hotels".</span><span class="sxs-lookup"><span data-stu-id="92810-134">Here are a few example queries on an index named "hotels".</span></span> <span data-ttu-id="92810-135">Essas consultas são mostradas nos formatos GET e POST.</span><span class="sxs-lookup"><span data-stu-id="92810-135">These queries are shown in both GET and POST format.</span></span>

<span data-ttu-id="92810-136">Pesquisar índice inteiro Olá Olá termo 'orçamento' e retornar somente Olá `hotelName` campo:</span><span class="sxs-lookup"><span data-stu-id="92810-136">Search hello entire index for hello term 'budget' and return only hello `hotelName` field:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=budget&$select=hotelName&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "budget",
    "select": "hotelName"
}
```

<span data-ttu-id="92810-137">Aplicar um mais barato do que r $150 por noite de hotéis filtro toofind do índice de toohello e retornar Olá `hotelId` e `description`:</span><span class="sxs-lookup"><span data-stu-id="92810-137">Apply a filter toohello index toofind hotels cheaper than $150 per night, and return hello `hotelId` and `description`:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$filter=baseRate lt 150&$select=hotelId,description&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "filter": "baseRate lt 150",
    "select": "hotelId,description"
}
```

<span data-ttu-id="92810-138">Pesquisar Olá todo o índice, a ordem por um campo específico (`lastRenovationDate`) em ordem decrescente, levar a resultados de duas primeiras hello e mostrar apenas `hotelName` e `lastRenovationDate`:</span><span class="sxs-lookup"><span data-stu-id="92810-138">Search hello entire index, order by a specific field (`lastRenovationDate`) in descending order, take hello top two results, and show only `hotelName` and `lastRenovationDate`:</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$top=2&$orderby=lastRenovationDate desc&$select=hotelName,lastRenovationDate&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "orderby": "lastRenovationDate desc",
    "select": "hotelName,lastRenovationDate",
    "top": 2
}
```

## <a name="submit-your-http-request"></a><span data-ttu-id="92810-139">Enviar sua solicitação HTTP</span><span class="sxs-lookup"><span data-stu-id="92810-139">Submit your HTTP request</span></span>
<span data-ttu-id="92810-140">Agora que formulou a consulta como parte da URL de solicitação HTTP (para GET) ou o corpo (POST), você pode definir os cabeçalhos de solicitação e enviar a consulta.</span><span class="sxs-lookup"><span data-stu-id="92810-140">Now that you have formulated your query as part of your HTTP request URL (for GET) or body (for POST), you can define your request headers and submit your query.</span></span>

#### <a name="request-and-request-headers"></a><span data-ttu-id="92810-141">Solicitação e cabeçalhos de solicitação</span><span class="sxs-lookup"><span data-stu-id="92810-141">Request and Request Headers</span></span>
<span data-ttu-id="92810-142">Você deve definir dois cabeçalhos de solicitação de GET ou três de POST:</span><span class="sxs-lookup"><span data-stu-id="92810-142">You must define two request headers for GET, or three for POST:</span></span>

1. <span data-ttu-id="92810-143">Olá `api-key` cabeçalho deve ser definido como chave de consulta toohello encontrado na etapa acima.</span><span class="sxs-lookup"><span data-stu-id="92810-143">hello `api-key` header must be set toohello query key you found in step I above.</span></span> <span data-ttu-id="92810-144">Você também pode usar uma chave de administração como Olá `api-key` cabeçalho, mas é recomendável que você use uma chave de consulta como exclusivamente concede acesso somente leitura tooindexes e documentos.</span><span class="sxs-lookup"><span data-stu-id="92810-144">You can also use an admin key as hello `api-key` header, but it is recommended that you use a query key as it exclusively grants read-only access tooindexes and documents.</span></span>
2. <span data-ttu-id="92810-145">Olá `Accept` cabeçalho deve ser definido muito`application/json`.</span><span class="sxs-lookup"><span data-stu-id="92810-145">hello `Accept` header must be set too`application/json`.</span></span>
3. <span data-ttu-id="92810-146">POST, Olá `Content-Type` cabeçalho também deve ser definido muito`application/json`.</span><span class="sxs-lookup"><span data-stu-id="92810-146">For POST only, hello `Content-Type` header should also be set too`application/json`.</span></span>

<span data-ttu-id="92810-147">Veja abaixo um HTTP GET solicitação toosearch hello "hotéis" índice usando Olá API de REST de pesquisa do Azure, usando uma consulta simple que procura o termo hello "motel":</span><span class="sxs-lookup"><span data-stu-id="92810-147">See below for an HTTP GET request toosearch hello "hotels" index using hello Azure Search REST API, using a simple query that searches for hello term "motel":</span></span>

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=motel&api-version=2016-09-01
Accept: application/json
api-key: [query key]
```

<span data-ttu-id="92810-148">Aqui está o hello mesmo exemplo de consulta, desta vez usando HTTP POST:</span><span class="sxs-lookup"><span data-stu-id="92810-148">Here is hello same example query, this time using HTTP POST:</span></span>

```
POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
Content-Type: application/json
Accept: application/json
api-key: [query key]

{
    "search": "motel"
}
```

<span data-ttu-id="92810-149">Uma solicitação de consulta bem-sucedida resultará em um código de Status `200 OK` e resultados da pesquisa Olá são retornados como JSON no corpo de resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="92810-149">A successful query request will result in a Status Code of `200 OK` and hello search results are returned as JSON in hello response body.</span></span> <span data-ttu-id="92810-150">É aqui que Olá resultados para Olá acima consulta aparência, supondo que hotéis"hello" índice é populado com dados de exemplo hello em [Olá importação de dados de pesquisa do Azure usando a API REST](search-import-data-rest-api.md) (Observe que Olá JSON foi formatado para maior clareza).</span><span class="sxs-lookup"><span data-stu-id="92810-150">Here is what hello results for hello above query look like, assuming hello "hotels" index is populated with hello sample data in [Data Import in Azure Search using hello REST API](search-import-data-rest-api.md) (note that hello JSON has been formatted for clarity).</span></span>

```JSON
{
    "value": [
        {
            "@search.score": 0.59600675,
            "hotelId": "2",
            "baseRate": 79.99,
            "description": "Cheapest hotel in town",
            "description_fr": "Hôtel le moins cher en ville",
            "hotelName": "Roach Motel",
            "category": "Budget",
            "tags":["motel", "budget"],
            "parkingIncluded": true,
            "smokingAllowed": true,
            "lastRenovationDate": "1982-04-28T00:00:00Z",
            "rating": 1,
            "location": {
                "type": "Point",
                "coordinates": [-122.131577, 49.678581],
                "crs": {
                    "type":"name",
                    "properties": {
                        "name": "EPSG:4326"
                    }
                }
            }
        }
    ]
}
```

<span data-ttu-id="92810-151">toolearn mais, visite seção "Resposta" hello [procurar documentos](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span><span class="sxs-lookup"><span data-stu-id="92810-151">toolearn more, please visit hello "Response" section of [Search Documents](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).</span></span> <span data-ttu-id="92810-152">Para obter mais informações sobre outros códigos de status HTTP que podem ser retornados em caso de falha, confira [Códigos de status HTTP (Pesquisa do Azure)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span><span class="sxs-lookup"><span data-stu-id="92810-152">For more information on other HTTP status codes that could be returned in case of failure, see [HTTP status codes (Azure Search)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).</span></span>
