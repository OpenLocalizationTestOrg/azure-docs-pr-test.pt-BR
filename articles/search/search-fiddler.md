---
title: aaaHow toouse Fiddler tooevaluate e testar as APIs de REST de pesquisa do Azure | Microsoft Docs
description: "Use o Fiddler para uma disponibilidade de pesquisa do Azure tooverifying abordagem sem código e experimentar Olá APIs REST."
services: search
documentationcenter: 
author: HeidiSteen
manager: mblythe
editor: 
ms.assetid: 790e5779-c6a3-4a07-9d1e-d6739e6b87d2
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: heidist
ms.openlocfilehash: 2912e1180717d7b40a1e4f7f7f00daf2cc254f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-fiddler-tooevaluate-and-test-azure-search-rest-apis"></a>Usar o Fiddler tooevaluate e testar as APIs de REST de pesquisa do Azure
> [!div class="op_single_selector"]
>
> * [Visão geral](search-query-overview.md)
> * [Gerenciador de Pesquisa](search-explorer.md)
> * [Fiddler](search-fiddler.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
>
>

Este artigo explica como toouse Fiddler, disponível como um [download gratuito da Telerik](http://www.telerik.com/fiddler), tooissue HTTP solicitações tooand exibir respostas usando Olá API de REST de pesquisa do Azure, sem ter que toowrite qualquer código. A Pesquisa do Azure é um serviço de pesquisa hospedado na nuvem totalmente gerenciado no Microsoft Azure, facilmente programável por meio APIs REST e .NET. saudação de serviço de pesquisa do Azure, APIs REST estão documentadas em [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).

Olá etapas a seguir, você criar um índice, carregar documentos, índice de saudação de consulta e, em seguida, sistema de saudação de consulta para obter informações de serviço.

toocomplete essas etapas, você precisará de um serviço de pesquisa do Azure e `api-key`. Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter instruções sobre como tooget iniciada.

## <a name="create-an-index"></a>Crie um índice
1. Inicie o Fiddler. Em Olá **arquivo** menu desativar **capturar tráfego** toohide estranhas HTTP atividade de tarefa atual toohello não relacionados.
2. Em Olá **criador** guia, você vai Formula uma solicitação que se parece com hello captura de tela a seguir.

      ![][1]
3. Selecione **PUT**.
4. Insira uma URL que especifica a URL do serviço hello, atributos de solicitação e Olá api-version. Alguns tookeep de ponteiros em mente:

   * Use o HTTPS como prefixo de saudação.
   * O atributo de solicitação é "/indexes/hotels". Isso informa toocreate pesquisa um índice chamado 'hotéis'.
   * A versão da API fica em letras minúsculas, especificada como "?api-version=2016-09-01". As versões da API são importantes porque a Pesquisa do Azure implanta atualizações regularmente. Em raras ocasiões, uma atualização de serviço pode apresentar uma alteração de quebra toohello API. Por esse motivo, a Pesquisa do Azure requer uma versão de api em cada solicitação para que você tenha controle total sobre qual delas será usada.

     a URL completa Olá deve ter aparência semelhante toohello exemplo a seguir.

             https://my-app.search.windows.net/indexes/hotels?api-version=2016-09-01
5. Especifica o cabeçalho de solicitação hello, substituindo host hello e chave de api com valores que são válidos para o serviço.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
6. No corpo da solicitação, cole em campos de saudação que compõem a definição de índice de saudação.

          {
         "name": "hotels",  
         "fields": [
           {"name": "hotelId", "type": "Edm.String", "key":true, "searchable": false},
           {"name": "baseRate", "type": "Edm.Double"},
           {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
           {"name": "hotelName", "type": "Edm.String"},
           {"name": "category", "type": "Edm.String"},
           {"name": "tags", "type": "Collection(Edm.String)"},
           {"name": "parkingIncluded", "type": "Edm.Boolean"},
           {"name": "smokingAllowed", "type": "Edm.Boolean"},
           {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
           {"name": "rating", "type": "Edm.Int32"},
           {"name": "location", "type": "Edm.GeographyPoint"}
          ]
         }
7. Clique em **Executar**.

Em alguns segundos, você deve ver uma resposta HTTP 201 na lista de sessão hello, indicando que o índice de saudação foi criado com êxito.

Se você receber HTTP 504, verifique se o que URL Olá Especifica o HTTPS. Se você vir HTTP 400 ou 404, verifique a solicitação de saudação corpo tooverify existe foram sem erros de copiar e colar. Um HTTP 403 normalmente indica um problema com hello-chave de api (uma chave inválida ou um problema de sintaxe com como chave de api Olá for especificado).

## <a name="load-documents"></a>Carregue os documentos
Em Olá **criador** guia documentos toopost solicitação serão semelhante a saudação a seguir. corpo de saudação da solicitação de saudação contém dados de pesquisa de Olá para 4 hotéis.

   ![][2]

1. Selecione **POST**.
2. Insira uma URL iniciada por HTTPS, seguida da URL do serviço, seguida de "/indexes/<'nomedoíndice'>/docs/index?api-version=2016-09-01". a URL completa Olá deve ter aparência semelhante toohello exemplo a seguir.

         https://my-app.search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
3. Cabeçalho de solicitação deve ser Olá mesmo de antes. Lembre-se de substituído host hello e chave de api com valores que são válidos para o serviço.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. Olá corpo da solicitação contém quatro índice hotéis toobe toohello adicionado de documentos.

         {
         "value": [
         {
             "@search.action": "upload",
             "hotelId": "1",
             "baseRate": 199.0,
             "description": "Best hotel in town",
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
             "@search.action": "upload",
             "hotelId": "3",
             "baseRate": 279.99,
             "description": "Surprisingly expensive",
             "hotelName": "Dew Drop Inn",
             "category": "Bed and Breakfast",
             "tags": ["charming", "quaint"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.33207, 47.60621] }
           },
           {
             "@search.action": "upload",
             "hotelId": "4",
             "baseRate": 220.00,
             "description": "This could be hello one",
             "hotelName": "A Hotel for Everyone",
             "category": "Basic hotel",
             "tags": ["pool", "wifi"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.12151, 47.67399] }
           }
          ]
         }
5. Clique em **Executar**.

Em alguns segundos, você deve ver uma resposta HTTP 200 na lista de sessão hello. Isso indica Olá documentos foram criados com êxito. Se você receber um 207, pelo menos um documento falha tooupload. Se você receber um 404, você tem um erro de sintaxe no cabeçalho de saudação ou corpo de solicitação de saudação.

## <a name="query-hello-index"></a>Índice de saudação de consulta
Agora que o índice e os documentos foram carregados, você pode consultá-los.  Em Olá **criador** guia, uma **obter** comando que consulta o serviço terá aparência semelhante toohello captura de tela a seguir.

   ![][3]

1. Selecione **GET**.
2. Insira uma URL iniciada por HTTPS, seguida da URL do serviço, seguida por "/indexes/<'indexname'>/docs?", seguido de parâmetros de consulta. Por exemplo, use Olá URL a seguir, substituindo o nome de host de exemplo hello por um que seja válido para o serviço.

         https://my-app.search.windows.net/indexes/hotels/docs?search=motel&facet=category&facet=rating,values:1|2|3|4|5&api-version=2016-09-01

   Essa consulta pesquisa termo hello "motel" e recupera as categorias de faceta para classificações.
3. Cabeçalho de solicitação deve ser Olá mesmo de antes. Lembre-se de substituído host hello e chave de api com valores que são válidos para o serviço.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444

código de resposta de saudação deve ser 200, e a saída de resposta hello deve parecer semelhante toohello captura de tela a seguir.

   ![][4]

Olá exemplo consulta a seguir é de saudação [a operação de índice de pesquisa (API de pesquisa do Azure)](http://msdn.microsoft.com/library/dn798927.aspx) no MSDN. Muitas consultas de exemplo hello neste tópico incluem espaços, que não são permitidos em Fiddler. Substitua cada espaço com um caractere + antes de colá-lo em Olá cadeia de caracteres de consulta antes de tentar a consulta Olá Fiddler.

**Antes da substituição dos espaços:**

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2016-09-01

**Após a substituição dos espaços por +:**

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate+desc&api-version=2016-09-01

## <a name="query-hello-system"></a>Sistema de saudação de consulta
Você também pode consultar Olá tooget documento contagens e armazenamento consumo do sistema. Em Olá **criador** guia, sua solicitação será a aparência a seguir toohello semelhante e resposta Olá retornará uma contagem do número de saudação de documentos e o espaço usado.

 ![][5]

1. Selecione **GET**.
2. Insira uma URL que inclua a URL do seu serviço, seguida por "/indexes/hotels/stats?api-version=2016-09-01":

         https://my-app.search.windows.net/indexes/hotels/stats?api-version=2016-09-01
3. Especifica o cabeçalho de solicitação hello, substituindo host hello e chave de api com valores que são válidos para o serviço.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. Corpo da solicitação Olá deixe em branco.
5. Clique em **Executar**. Você deve ver um código de status HTTP 200 na lista de sessão hello. Selecione entrada hello lançada para o comando.
6. Clique em Olá **inspetores** , clique em Olá **cabeçalhos** guia e, em seguida, selecione Olá JSON formato. Você deve ver Olá contagem e o armazenamento de tamanho do documento (em KB).

## <a name="next-steps"></a>Próximas etapas
Consulte [gerenciar o serviço de pesquisa no Azure](search-manage.md) para uma abordagem sem código toomanaging e usando a pesquisa do Azure.

<!--Image References-->
[1]: ./media/search-fiddler/AzureSearch_Fiddler1_PutIndex.png
[2]: ./media/search-fiddler/AzureSearch_Fiddler2_PostDocs.png
[3]: ./media/search-fiddler/AzureSearch_Fiddler3_Query.png
[4]: ./media/search-fiddler/AzureSearch_Fiddler4_QueryResults.png
[5]: ./media/search-fiddler/AzureSearch_Fiddler5_QueryStats.png
