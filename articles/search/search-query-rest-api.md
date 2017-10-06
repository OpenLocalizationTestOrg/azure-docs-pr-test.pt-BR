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
# <a name="query-your-azure-search-index-using-hello-rest-api"></a>Consultar seu índice de pesquisa do Azure usando a API REST de saudação
> [!div class="op_single_selector"]
>
> * [Visão geral](search-query-overview.md)
> * [Portal](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
>
>

Este artigo mostra como tooquery um índice usando Olá [API de REST de pesquisa do Azure](https://docs.microsoft.com/rest/api/searchservice/).

Antes de começar este passo a passo, você já deve ter [criado um índice do Azure Search](search-what-is-an-index.md), e este já deve estar [preenchido com os dados](search-what-is-data-import.md). Para obter informações de contexto, veja [Como funciona a pesquisa de texto completo no Azure Search](search-lucene-query-architecture.md).

## <a name="identify-your-azure-search-services-query-api-key"></a>Identificar sua api-key de consulta do serviço de Pesquisa do Azure
Um componente fundamental de cada operação de pesquisa em relação a saudação API de REST de pesquisa do Azure é hello *chave de api* que foi gerado para o serviço de saudação Você provisionou. Ter uma chave válida estabelece confiança, em uma base por solicitação, entre solicitação de envio Olá Olá aplicativo e serviço de saudação que lida com ele.

1. toofind chaves de api do serviço, você pode entrar no toohello [portal do Azure](https://portal.azure.com/)
2. Vá folha do serviço de pesquisa do Azure tooyour
3. Clique no ícone de "Chaves" hello

O serviço tem *chaves de administração* e *chaves de consulta*.

* O primário e secundário *chaves de administração* conceder direitos totais tooall operações, incluindo Olá capacidade toomanage Olá serviço, criar e excluir índices, indexadores e fontes de dados. Há duas chaves para que você possa continuar chave secundária do toouse Olá se você decidir chave primária do tooregenerate hello e vice-versa.
* O *chaves de consulta* conceder acesso somente leitura tooindexes e documentos, e são normalmente distribuídos tooclient aplicativos que emitem solicitações de pesquisa.

Para fins de saudação de consultar um índice, você pode usar uma de suas chaves de consulta. As chaves de administração também podem ser usadas para consultas, mas você deve usar uma chave de consulta no código do aplicativo, isso melhor da seguinte maneira Olá [princípio de menos privilégios](https://en.wikipedia.org/wiki/Principle_of_least_privilege).

## <a name="formulate-your-query"></a>Formular sua consulta
Há duas maneiras muito[pesquise o índice usando a API REST de saudação](https://docs.microsoft.com/rest/api/searchservice/Search-Documents). Uma maneira é tooissue uma solicitação HTTP POST em que os parâmetros de consulta são definidos em um objeto JSON no corpo da solicitação de saudação. saudação de outra forma é tooissue uma solicitação HTTP GET em que os parâmetros de consulta são definidos na URL de solicitação de saudação. POSTAGEM tem mais [relaxada limites](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) no tamanho de saudação de parâmetros de consulta que GET. Por esse motivo, é recomendável usar POST, a menos que haja circunstâncias especiais em que o uso de GET seja mais conveniente.

Para POST e GET, você precisa tooprovide seu *nome do serviço*, *nome do índice*e hello adequada *versão da API* (Olá atual versão da API é `2016-09-01` no tempo de saudação Publicar este documento) em Olá URL da solicitação. Para obter, Olá *cadeia de caracteres de consulta* em Olá final da URL da saudação é onde você pode fornecer parâmetros de consulta hello. Consulte abaixo para o formato de URL hello:

    https://[service name].search.windows.net/indexes/[index name]/docs?[query string]&api-version=2016-09-01

saudação de formato para POST é Olá mesmo, mas com apenas uma versão de api em parâmetros de cadeia de caracteres de consulta de saudação.

#### <a name="example-queries"></a>Consultas de Exemplo
Veja algumas consultas de exemplo em um índice chamado "hotels". Essas consultas são mostradas nos formatos GET e POST.

Pesquisar índice inteiro Olá Olá termo 'orçamento' e retornar somente Olá `hotelName` campo:

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=budget&$select=hotelName&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "budget",
    "select": "hotelName"
}
```

Aplicar um mais barato do que r $150 por noite de hotéis filtro toofind do índice de toohello e retornar Olá `hotelId` e `description`:

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$filter=baseRate lt 150&$select=hotelId,description&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "filter": "baseRate lt 150",
    "select": "hotelId,description"
}
```

Pesquisar Olá todo o índice, a ordem por um campo específico (`lastRenovationDate`) em ordem decrescente, levar a resultados de duas primeiras hello e mostrar apenas `hotelName` e `lastRenovationDate`:

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

## <a name="submit-your-http-request"></a>Enviar sua solicitação HTTP
Agora que formulou a consulta como parte da URL de solicitação HTTP (para GET) ou o corpo (POST), você pode definir os cabeçalhos de solicitação e enviar a consulta.

#### <a name="request-and-request-headers"></a>Solicitação e cabeçalhos de solicitação
Você deve definir dois cabeçalhos de solicitação de GET ou três de POST:

1. Olá `api-key` cabeçalho deve ser definido como chave de consulta toohello encontrado na etapa acima. Você também pode usar uma chave de administração como Olá `api-key` cabeçalho, mas é recomendável que você use uma chave de consulta como exclusivamente concede acesso somente leitura tooindexes e documentos.
2. Olá `Accept` cabeçalho deve ser definido muito`application/json`.
3. POST, Olá `Content-Type` cabeçalho também deve ser definido muito`application/json`.

Veja abaixo um HTTP GET solicitação toosearch hello "hotéis" índice usando Olá API de REST de pesquisa do Azure, usando uma consulta simple que procura o termo hello "motel":

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=motel&api-version=2016-09-01
Accept: application/json
api-key: [query key]
```

Aqui está o hello mesmo exemplo de consulta, desta vez usando HTTP POST:

```
POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
Content-Type: application/json
Accept: application/json
api-key: [query key]

{
    "search": "motel"
}
```

Uma solicitação de consulta bem-sucedida resultará em um código de Status `200 OK` e resultados da pesquisa Olá são retornados como JSON no corpo de resposta de saudação. É aqui que Olá resultados para Olá acima consulta aparência, supondo que hotéis"hello" índice é populado com dados de exemplo hello em [Olá importação de dados de pesquisa do Azure usando a API REST](search-import-data-rest-api.md) (Observe que Olá JSON foi formatado para maior clareza).

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

toolearn mais, visite seção "Resposta" hello [procurar documentos](https://docs.microsoft.com/rest/api/searchservice/Search-Documents). Para obter mais informações sobre outros códigos de status HTTP que podem ser retornados em caso de falha, confira [Códigos de status HTTP (Pesquisa do Azure)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).
