---
title: "AAA \"criar um índice (API REST - pesquisa do Azure) | Microsoft Docs\""
description: "Crie um índice no código usando Olá API de REST de HTTP de pesquisa do Azure."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: ac6c5fba-ad59-492d-b715-d25a7a7ae051
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: 117ab64a9874a443351a8a02a9b959b8f7beb7c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-rest-api"></a>Criar um índice de pesquisa do Azure usando a API REST de saudação
> [!div class="op_single_selector"]
>
> * [Visão geral](search-what-is-an-index.md)
> * [Portal](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
>
>

Este artigo o guiará pelo processo de saudação de criação de uma pesquisa do Azure [índice](https://docs.microsoft.com/rest/api/searchservice/Create-Index) Olá usando a API de REST de pesquisa do Azure.

Antes de seguir este guia e criar um índice, você já deverá ter [criado um serviço do Azure Search](search-create-service-portal.md).

toocreate um índice de pesquisa do Azure usando Olá API REST, você emitir ponto de extremidade de URL de um único HTTP POST solicitação tooyour pesquisa do Azure do serviço. Definição do índice estarão contida no corpo da solicitação de hello como o conteúdo JSON bem formado.

## <a name="identify-your-azure-search-services-admin-api-key"></a>Identificar a api-key do administrador de seu serviço do Azure Search
Agora que você possua um serviço de pesquisa do Azure, você pode emitir solicitações HTTP no ponto de extremidade de URL do serviço usando a API REST de saudação. *Todos os* solicitações de API devem incluir Olá api-chave que foi gerada para Olá Você provisionou do serviço de pesquisa. Ter uma chave válida estabelece confiança, em uma base por solicitação, entre solicitação de envio Olá Olá aplicativo e serviço de saudação que lida com ele.

1. toofind api-chaves do serviço, você deve efetuar login Olá [portal do Azure](https://portal.azure.com/)
2. Vá folha do serviço de pesquisa do Azure tooyour
3. Clique em Olá ícone "Chaves"

O serviço terá *chaves de administração* e *chaves de consulta*.

* O primário e secundário *chaves de administração* conceder direitos totais tooall operações, incluindo Olá capacidade toomanage Olá serviço, criar e excluir índices, indexadores e fontes de dados. Há duas chaves para que você possa continuar chave secundária do toouse Olá se você decidir chave primária do tooregenerate hello e vice-versa.
* O *chaves de consulta* conceder acesso somente leitura tooindexes e documentos, e são normalmente distribuídos tooclient aplicativos que emitem solicitações de pesquisa.

Para fins de saudação de criação de um índice, você pode usar a chave primária ou secundária de administração.

## <a name="define-your-azure-search-index-using-well-formed-json"></a>Definir o índice de Pesquisa do Azure usando JSON bem formado
Um único serviço tooyour de solicitação HTTP POST criará seu índice. corpo de saudação da solicitação HTTP POST conterá um único objeto JSON que define o índice de pesquisa do Azure.

1. a primeira propriedade saudação do objeto JSON é o nome de saudação do índice.
2. Olá segunda propriedade do objeto JSON é uma matriz JSON chamada `fields` que contém um objeto JSON separado para cada campo no índice. Cada um desses objetos JSON contém vários pares de nome/valor para cada Olá campo atributos, incluindo "name", "tipo", etc.

É importante que você mantenha suas necessidades de negócios e experiência de usuário pesquisa em mente ao criar o índice de cada campo deve ser atribuída a saudação [atributos adequados](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Esses atributos controlam a qual pesquisar recursos (filtragem, facetas, classificação de pesquisa de texto completo, etc.) se aplicam a campos de toowhich. Para qualquer atributo que não for especificado, o padrão de Olá será recurso de pesquisa tooenable Olá correspondente, a menos que especificamente desativá-lo.

Para nosso exemplo, chamamos o índice de "hotels" e definimos os campos da seguinte maneira:

```JSON
{
    "name": "hotels",  
    "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false, "sortable": false, "facetable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String", "facetable": false},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean", "sortable": false},
        {"name": "smokingAllowed", "type": "Edm.Boolean", "sortable": false},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
    ]
}
```

Escolhemos cuidadosamente Olá indexar atributos de cada campo com base em como achamos que serão usados em um aplicativo. Por exemplo, `hotelId` é uma chave exclusiva que as pessoas procurando hotéis provavelmente não saberão, assim, podemos desabilitar pesquisa de texto completo para esse campo definindo `searchable` muito`false`, que economiza espaço no índice de saudação.

Observe que exatamente um campo no índice de tipo `Edm.String` deve ser Olá designado como um campo de 'key' hello.

definição de índice de saudação acima usa um analisador de linguagem para Olá `description_fr` campo porque ele é um texto em francês toostore pretendido. Consulte [tópico de suporte de idioma Olá](https://docs.microsoft.com/rest/api/searchservice/Language-support) , bem como Olá correspondente [postagem de blog](https://azure.microsoft.com/blog/language-support-in-azure-search/) para obter mais informações sobre os analisadores de idioma.

## <a name="issue-hello-http-request"></a>Solicitação HTTP de saudação do problema
1. Usando a definição de índice como o corpo da solicitação hello, emita uma URL de ponto de extremidade de serviço HTTP POST solicitação tooyour pesquisa do Azure. Na URL hello, ser toouse-se de que o nome do serviço como o nome de host hello e coloque Olá adequada `api-version` como um parâmetro de cadeia de caracteres de consulta (Olá atual versão da API é `2016-09-01` em tempo de saudação da publicação neste documento).
2. Nos cabeçalhos de solicitação hello, especifique Olá `Content-Type` como `application/json`. Você também precisará tooprovide chave de administração do serviço que você identificou na etapa I no hello `api-key` cabeçalho.

Você terá tooprovide seu próprio nome e a api chave tooissue Olá solicitação de serviço abaixo:

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [api-key]


Para uma solicitação bem-sucedida, você deverá ver o código de status 201 (Criado). Para obter mais informações sobre como criar um índice por meio de saudação API REST, visite Olá [referência da API aqui](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Para obter mais informações sobre outros códigos de status HTTP que podem ser retornados em caso de falha, confira [Códigos de status HTTP (Pesquisa do Azure)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).

Quando tiver terminado com um índice e quiser toodelete-lo, basta emita uma solicitação HTTP DELETE. Por exemplo, isso é como podemos seria Excluir índice de "hotéis" hello:

    DELETE https://[service name].search.windows.net/indexes/hotels?api-version=2016-09-01
    api-key: [api-key]


## <a name="next-steps"></a>Próximas etapas
Depois de criar um índice de pesquisa do Azure, você estará pronto muito[carregar o conteúdo no índice Olá](search-what-is-data-import.md) para que você pode começar a procurar seus dados.
