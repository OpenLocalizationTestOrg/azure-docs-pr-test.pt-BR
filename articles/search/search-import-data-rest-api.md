---
title: AAA "carregar dados (API REST - pesquisa do Azure) | Microsoft Docs"
description: "Saiba como o índice de tooan tooupload dados na pesquisa do Azure usando Olá API REST."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: 
ms.assetid: 8d0749fb-6e08-4a17-8cd3-1a215138abc6
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: 6ba1336012d1f0f6d6d6c933e16aa879afb9b824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search-using-hello-rest-api"></a>Carregar dados tooAzure pesquisa usando Olá API REST
> [!div class="op_single_selector"]
>
> * [Visão geral](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
>
>

Este artigo mostra como Olá toouse [API de REST de pesquisa do Azure](https://docs.microsoft.com/rest/api/searchservice/) tooimport dados em um índice de pesquisa do Azure.

Antes de começar este passo a passo, você já deve ter [criado um índice de Pesquisa do Azure](search-what-is-an-index.md).

Em documentos de toopush ordem pra o índice usando a API REST do hello, emitirá o ponto de extremidade de URL de um HTTP POST solicitação tooyour índice. corpo de saudação do hello solicitação HTTP corpo é um objeto JSON que contém documentos Olá toobe adicionada, modificada ou excluída.

## <a name="identify-your-azure-search-services-admin-api-key"></a>Identificar a api-key do administrador de seu serviço do Azure Search
Ao emitir solicitações HTTP em seu serviço usando Olá API REST, *cada* solicitação de API deve incluir Olá api-chave que foi gerada para Olá Você provisionou do serviço de pesquisa. Ter uma chave válida estabelece confiança, em uma base por solicitação, entre solicitação de envio Olá Olá aplicativo e serviço de saudação que lida com ele.

1. toofind chaves de api do serviço, você pode entrar no toohello [portal do Azure](https://portal.azure.com/)
2. Vá folha do serviço de pesquisa do Azure tooyour
3. Clique em Olá ícone "Chaves"

O serviço terá *chaves de administração* e *chaves de consulta*.

* O primário e secundário *chaves de administração* conceder direitos totais tooall operações, incluindo Olá capacidade toomanage Olá serviço, criar e excluir índices, indexadores e fontes de dados. Há duas chaves para que você possa continuar chave secundária do toouse Olá se você decidir chave primária do tooregenerate hello e vice-versa.
* O *chaves de consulta* conceder acesso somente leitura tooindexes e documentos, e são normalmente distribuídos tooclient aplicativos que emitem solicitações de pesquisa.

Para fins de saudação da importação de dados para um índice, você pode usar a chave primária ou secundária de administração.

## <a name="decide-which-indexing-action-toouse"></a>Decidir quais indexação toouse de ação
Ao usar o hello API REST, você emitir solicitações HTTP POST com URL de ponto de extremidade do índice de pesquisa do Azure tooyour corpos JSON solicitação. objeto do Hello JSON no corpo da solicitação HTTP conterá uma matriz JSON denominado "valor", que contém objetos JSON que representa os documentos que você gostaria que tooadd tooyour índice, atualizar ou excluir.

Cada objeto JSON na matriz de "valor" hello representa um toobe documento indexado. Cada um desses objetos contém a chave do documento hello e especifica a ação de indexação Olá desejado (carregar, mesclar, excluir, etc.). Dependendo de qual dos Olá ações que você escolher abaixo, somente determinados campos devem ser incluídos para cada documento:

| @search.action | Descrição | Campos necessários para cada documento | Observações |
| --- | --- | --- | --- |
| `upload` |Um `upload` ação é similar tooan "upsert" onde documento hello será inserido se for novo e atualizado/substituído se ele existir. |chave, além de quaisquer outros campos que você deseja toodefine |Ao atualizar/substituir um documento existente, qualquer campo que não está especificado na solicitação de saudação terá seu campo definido muito`null`. Isso ocorre mesmo quando o campo Olá tiver sido definido anteriormente tooa valor de não-nulo. |
| `merge` |Atualizações de uma existente de documento com hello especificado campos. Se o documento de saudação não existe no índice hello, mesclagem Olá falhará. |chave, além de quaisquer outros campos que você deseja toodefine |Qualquer campo que você especificar em uma mesclagem substituirá o campo de saudação existente no documento de saudação. Isso inclui campos do tipo `Collection(Edm.String)`. Por exemplo, se hello documento contém um campo `tags` com valor `["budget"]` e executar uma mesclagem com valor `["economy", "pool"]` para `tags`, Olá valor final do hello `tags` campo será `["economy", "pool"]`. Ele não será `["budget", "economy", "pool"]`. |
| `mergeOrUpload` |Esta ação se comporta como `merge` se um documento com hello atribuída a chave já existe no índice hello. Se o documento de saudação não existir, ele se comporta como `upload` com um novo documento. |chave, além de quaisquer outros campos que você deseja toodefine |- |
| `delete` |Remove o documento especificado Olá do índice de saudação. |somente chave |Todos os campos que você especificar que o campo de chave hello será ignorado. Se você quiser tooremove um campo individual de um documento, use `merge` em vez disso e basta definir campo Olá explicitamente toonull. |

## <a name="construct-your-http-request-and-request-body"></a>Construir sua solicitação HTTP e o corpo da solicitação
Agora que você coletou valores de campo necessário Olá para suas ações de índice, são solicitação HTTP tooconstruct pronto Olá real e solicitação de JSON corpo tooimport seus dados.

#### <a name="request-and-request-headers"></a>Solicitação e cabeçalhos de solicitação
Saudação de URL, você precisará tooprovide seu nome de serviço, nome do índice ("hotéis" neste caso), bem como versão de API apropriada hello (Olá atual versão da API é `2016-09-01` em tempo de saudação da publicação neste documento). Você precisará Olá toodefine `Content-Type` e `api-key` cabeçalhos de solicitação. Para Olá último, use uma das chaves de administração do serviço.

    POST https://[search service].search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

#### <a name="request-body"></a>Corpo da solicitação
```JSON
{
    "value": [
        {
            "@search.action": "upload",
            "hotelId": "1",
            "baseRate": 199.0,
            "description": "Best hotel in town",
            "description_fr": "Meilleur hôtel en ville",
            "hotelName": "Fancy Stay",
            "category": "Luxury",
            "tags": ["pool", "view", "wifi", "concierge"],
            "parkingIncluded": false,
            "smokingAllowed": false,
            "lastRenovationDate": "2010-06-27T00:00:00Z",
            "rating": 5,
            "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
        },
        {
            "@search.action": "upload",
            "hotelId": "2",
            "baseRate": 79.99,
            "description": "Cheapest hotel in town",
            "description_fr": "Hôtel le moins cher en ville",
            "hotelName": "Roach Motel",
            "category": "Budget",
            "tags": ["motel", "budget"],
            "parkingIncluded": true,
            "smokingAllowed": true,
            "lastRenovationDate": "1982-04-28T00:00:00Z",
            "rating": 1,
            "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
        },
        {
            "@search.action": "mergeOrUpload",
            "hotelId": "3",
            "baseRate": 129.99,
            "description": "Close tootown hall and hello river"
        },
        {
            "@search.action": "delete",
            "hotelId": "6"
        }
    ]
}
```

Nesse caso, estamos usando `upload`, `mergeOrUpload` e `delete` como nossas ações de pesquisa.

Suponha que o índice de exemplo "hotels" já esteja preenchido com vários documentos. Observe como não tínhamos toospecify todos os campos de documento possíveis Olá ao usar `mergeOrUpload` e como podemos só especificado de chave de documento hello (`hotelId`) ao usar `delete`.

Além disso, observe que você só pode incluir documentos too1000 (ou 16 MB) em uma única solicitação de indexação.

## <a name="understand-your-http-response-code"></a>Compreender o código de resposta HTTP
#### <a name="200"></a>200
Após enviar uma solicitação de indexação bem-sucedida, você receberá uma resposta HTTP com o código de status `200 OK`. Olá corpo JSON do hello resposta HTTP será da seguinte maneira:

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": true,
            "errorMessage": null
        },
        ...
    ]
}
```

#### <a name="207"></a>207
Um código de status `207` será retornado quando pelo menos um item não tiver sido indexado com êxito. Olá corpo JSON de resposta HTTP de saudação conterá informações sobre documentos malsucedida hello.

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": false,
            "errorMessage": "hello search service is too busy tooprocess this document. Please try again later."
        },
        ...
    ]
}
```

> [!NOTE]
> Isso geralmente significa que a carga Olá na sua pesquisa de serviço é atingir um ponto em que solicitações de indexação começarão tooreturn `503` respostas. Nesse caso, é altamente recomendável que o código do cliente faça uma pausa e aguarde antes de tentar novamente. Isso dará sistema Olá toorecover algum tempo, aumentar as chances de saudação que as solicitações futuras serão bem-sucedidas. Repetir rapidamente suas solicitações só prolongará a situação de saudação.
>
>

#### <a name="429"></a>429
Um código de status `429` serão retornados quando você excedeu sua cota no número de saudação de documentos por índice.

#### <a name="503"></a>503
Um código de status `503` será retornado se nenhum dos itens de saudação na solicitação Olá foram indexados com êxito. Esse erro significa que o sistema hello está sob carga pesada e sua solicitação não pode ser processada neste momento.

> [!NOTE]
> Nesse caso, é altamente recomendável que o código do cliente faça uma pausa e aguarde antes de tentar novamente. Isso dará sistema Olá toorecover algum tempo, aumentar as chances de saudação que as solicitações futuras serão bem-sucedidas. Repetir rapidamente suas solicitações só prolongará a situação de saudação.
>
>

Para obter mais informações sobre as ações do documento e as respostas de êxito/erro, consulte [Adicionar, Atualizar ou Excluir Documentos](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents). Para obter mais informações sobre outros códigos de status HTTP que podem ser retornados em caso de falha, confira [Códigos de status HTTP (Pesquisa do Azure)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).

## <a name="next-steps"></a>Próximas etapas
Depois de preencher o índice de pesquisa do Azure, você será toostart pronto emitir consultas toosearch para documentos. Veja [Consultar seu Índice de Pesquisa do Azure](search-query-overview.md) para obter detalhes.
