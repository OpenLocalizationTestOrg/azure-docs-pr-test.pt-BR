---
title: aaaIndexing uma fonte de dados do banco de dados do Cosmos para pesquisa do Azure | Microsoft Docs
description: Este artigo mostra como toocreate um indexador da pesquisa do Azure com o banco de dados do Cosmos como uma fonte de dados.
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: search
ms.date: 08/10/2017
ms.author: eugenesh
ms.openlocfilehash: 195c9bc026ee1591679dc425ef083a32a3c86be6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-cosmos-db-with-azure-search-using-indexers"></a>Conectando o Cosmos DB ao Azure Search usando indexadores

Se você quiser tooimplement pesquisa uma ótima experiência aos seus dados do banco de dados do Cosmos, você pode usar uma data de toopull do indexador de pesquisa do Azure em um índice de pesquisa do Azure. Neste artigo, mostramos como toointegrate banco de dados do Azure Cosmos à pesquisa do Azure sem ter que toowrite qualquer infraestrutura de indexação de toomaintain de código.

tooset backup de um indexador Cosmos DB, você deve ter uma [serviço Azure Search](search-create-service-portal.md)e criar um índice, a fonte de dados e finalmente indexador hello. Você pode criar esses objetos usando Olá [portal](search-import-data-portal.md), [.NET SDK](/dotnet/api/microsoft.azure.search), ou [API REST](/rest/api/searchservice/) para todas as linguagens não .NET. 

Se você optar por portal hello, Olá [Assistente de importação de dados](search-import-data-portal.md) orienta você na criação de saudação de todos esses recursos.

> [!NOTE]
> Cosmos DB é hello próxima geração de documentos. Embora o nome do produto Olá for alterado, sintaxe é Olá mesmo de antes. Continue toospecify `documentdb` conforme indicado neste artigo do indexador. 

> [!TIP]
> Você pode iniciar Olá **importar dados** Assistente de saudação Cosmos DB painel toosimplify indexação da fonte de dados. Esquerda de navegação, vá muito**coleções** > **Adicionar pesquisa do Azure** tooget iniciado.

<a name="Concepts"></a>
## <a name="azure-search-indexer-concepts"></a>Conceitos do indexador do Azure Search
Azure pesquisa oferece suporte a saudação criação e gerenciamento de fontes de dados (incluindo o banco de dados do Cosmos) e indexadores que operam em relação a essas fontes de dados.

Um **fonte de dados** Especifica Olá tooindex de dados, credenciais e políticas para identificar alterações nos dados da saudação (como documentos modificados ou excluídos dentro de sua coleção). fonte de dados de saudação é definido como um recurso independente para que ele pode ser usado por vários indexadores.

Um **indexador** descreve como Olá fluxo de dados de sua fonte de dados em um índice de pesquisa de destino. Um indexador pode ser usado para:

* Execute uma cópia única de dados de saudação toopopulate um índice.
* Um índice com as alterações na fonte de dados de saudação em uma agenda de sincronização. agendamento de saudação faz parte da definição do indexador hello.
* Invoque o índice tooan atualizações sob demanda, conforme necessário.

<a name="CreateDataSource"></a>
## <a name="step-1-create-a-data-source"></a>Etapa 1: Criar uma fonte de dados
toocreate uma fonte de dados, faça uma POSTAGEM:

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
        "name": "mydocdbdatasource",
        "type": "documentdb",
        "credentials": {
            "connectionString": "AccountEndpoint=https://myDocDbEndpoint.documents.azure.com;AccountKey=myDocDbAuthKey;Database=myDocDbDatabaseId"
        },
        "container": { "name": "myDocDbCollectionId", "query": null },
        "dataChangeDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName": "_ts"
        }
    }

corpo de saudação da solicitação Olá contém definição de fonte de dados hello, que deve incluir Olá campos a seguir:

* **nome**: escolher qualquer nome toorepresent seu banco de dados do banco de dados do Cosmos.
* **type**: deve ser `documentdb`.
* **credentials**:
  
  * **connectionString**: obrigatório. Especifique o banco de dados do hello conexão informações tooyour Azure Cosmos DB no hello formato a seguir:`AccountEndpoint=<Cosmos DB endpoint url>;AccountKey=<Cosmos DB auth key>;Database=<Cosmos DB database id>`
* **container**:
  
  * **name**: obrigatório. Especifique a id de saudação do hello Cosmos DB coleção toobe indexado.
  * **query**: opcional. Você pode especificar uma consulta tooflatten um documento JSON arbitrário em um esquema simples que pesquisa do Azure pode indexar.
* **dataChangeDetectionPolicy**: recomendado. Consulte a seção [Indexando documentos alterados](#DataChangeDetectionPolicy).
* **dataDeletionDetectionPolicy**: opcional. Consulte a seção [Indexando documentos excluídos](#DataDeletionDetectionPolicy).

### <a name="using-queries-tooshape-indexed-data"></a>Usar consultas tooshape indexado dados
Você pode especificar um tooflatten de consulta de banco de dados do Cosmos aninhados propriedades ou matrizes, JSON propriedades do projeto e filtrar Olá dados toobe indexado. 

Documento de exemplo:

    {
        "userId": 10001,
        "contact": {
            "firstName": "andy",
            "lastName": "hoh"
        },
        "company": "microsoft",
        "tags": ["azure", "documentdb", "search"]
    }

Filtrar consulta:

    SELECT * FROM c WHERE c.company = "microsoft" and c._ts >= @HighWaterMark ORDER BY c._ts

Consulta de mesclagem:

    SELECT c.id, c.userId, c.contact.firstName, c.contact.lastName, c.company, c._ts FROM c WHERE c._ts >= @HighWaterMark ORDER BY c._ts
    
    
Consulta de projeção:

    SELECT VALUE { "id":c.id, "Name":c.contact.firstName, "Company":c.company, "_ts":c._ts } FROM c WHERE c._ts >= @HighWaterMark ORDER BY c._ts


Consulta de mesclagem de matriz:

    SELECT c.id, c.userId, tag, c._ts FROM c JOIN tag IN c.tags WHERE c._ts >= @HighWaterMark ORDER BY c._ts

<a name="CreateIndex"></a>
## <a name="step-2-create-an-index"></a>Etapa 2: Criar um índice
Se ainda não tiver um, crie um índice de destino da Pesquisa do Azure. Você pode criar um índice usando Olá [interface de usuário do portal do Azure](search-create-index-portal.md), Olá [criar o índice REST API](/rest/api/searchservice/create-index) ou [classe Index](/dotnet/api/microsoft.azure.search.models.index).

saudação de exemplo a seguir cria um índice com um campo de id e a descrição:

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
       "name": "mysearchindex",
       "fields": [{
         "name": "id",
         "type": "Edm.String",
         "key": true,
         "searchable": false
       }, {
         "name": "description",
         "type": "Edm.String",
         "filterable": false,
         "sortable": false,
         "facetable": false,
         "suggestions": true
       }]
     }

Certifique-se de que Olá esquema de seu índice de destino é compatível com o esquema Olá Olá JSON de documentos de origem ou a saída de saudação de sua projeção de consulta personalizada.

> [!NOTE]
> Para as coleções particionadas, chave de documento padrão Olá é do banco de dados Cosmos `_rid` propriedade, que obtém renomeada muito`rid` na pesquisa do Azure. Além disso, os valores `_rid` do Cosmos DB contêm caracteres que são inválidos nas chaves do Azure Search. Por esse motivo, Olá `_rid` valores são codificados na Base64.
> 
> 

### <a name="mapping-between-json-data-types-and-azure-search-data-types"></a>Mapeamento entre tipos de dados JSON e tipos de dados da Pesquisa do Azure
| TIPO DE DADOS JSON | TIPOS DE CAMPOS DE ÍNDICE DE DESTINO COMPATÍVEIS |
| --- | --- |
| Bool |Edm.Boolean, Edm.String |
| Números que se parecem com inteiros |Edm.Int32, Edm.Int64, Edm.String |
| Números que se parecem com pontos flutuantes |Edm.Double, Edm.String |
| Cadeia de caracteres |Edm.String |
| Matrizes de tipos primitivos, por exemplo, [“a”, “b”, “c”] |Collection(Edm.String) |
| Cadeias de caracteres que se parecem com datas |Edm.DateTimeOffset, Edm.String |
| Objetos GeoJSON, por exemplo, { "type": "Point", "coordinates": [long, lat] } |Edm.GeographyPoint |
| Outros objetos JSON |N/D |

<a name="CreateIndexer"></a>
## <a name="step-3-create-an-indexer"></a>Etapa 3: Criar um indexador

Após Olá índice e fonte de dados foram criados, você estará pronto toocreate indexador de saudação:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "mydocdbindexer",
      "dataSourceName" : "mydocdbdatasource",
      "targetIndexName" : "mysearchindex",
      "schedule" : { "interval" : "PT2H" }
    }

Esse indexador for executado a cada duas horas (intervalo de agendamento está definido muito "PT2H"). toorun um indexador a cada 30 minutos, defina o intervalo de saudação muito "PT30M". Olá menor intervalo de com suporte é 5 minutos. Olá agenda é opcional - se ele for omitido, um indexador é executado apenas uma vez quando ela é criada. No entanto, você pode executar um indexador sob demanda a qualquer momento.   

Para obter mais detalhes sobre Olá criar indexador API, check-out [criar indexador](https://docs.microsoft.com/rest/api/searchservice/create-indexer).

<a id="RunIndexer"></a>
### <a name="running-indexer-on-demand"></a>Executando o indexador sob demanda
Adição toorunning periodicamente em um agendamento, também pode ser chamado um indexador sob demanda:

    POST https://[service name].search.windows.net/indexers/[indexer name]/run?api-version=2016-09-01
    api-key: [Search service admin key]

> [!NOTE]
> Quando executar API retorna com êxito, invocação de indexador Olá foi agendada, mas o processamento real Olá ocorre de maneira assíncrona. 

Você pode monitorar o status do indexador Olá no portal de saudação ou usando Olá obter indexador Status API, que descrevemos lado. 

<a name="GetIndexerStatus"></a>
### <a name="getting-indexer-status"></a>Obtendo o status do indexador
Você pode recuperar o histórico de execução e status de saudação de um indexador:

    GET https://[service name].search.windows.net/indexers/[indexer name]/status?api-version=2016-09-01
    api-key: [Search service admin key]

resposta Olá contém o status geral do indexador, invocação de indexador último (ou em andamento) hello e histórico Olá recente invocações do indexador.

    {
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
         },
        "executionHistory":[ {
            "status":"success",
             "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        }]
    }

Histórico de execução contém até toohello 50 últimas execuções concluídas, que são classificadas em ordem cronológica inversa (para que execução mais recente Olá vem primeira na resposta de saudação).

<a name="DataChangeDetectionPolicy"></a>
## <a name="indexing-changed-documents"></a>Indexando documentos alterados
finalidade de saudação de dados de alterar a política de detecção é tooefficiently identificar itens de dados alterados. Atualmente, a política Olá só tem suportada é Olá `High Water Mark` política usando Olá `_ts` propriedade (carimbo de hora) fornecida pelo banco de dados do Cosmos, que é especificada da seguinte maneira:

    {
        "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
        "highWaterMarkColumnName" : "_ts"
    }

Usando essa política é altamente recomendável o desempenho do indexador bom tooensure. 

Se você estiver usando uma consulta personalizada, certifique-se de que Olá `_ts` propriedade projetada pela consulta hello.

<a name="IncrementalProgress"></a>
### <a name="incremental-progress-and-custom-queries"></a>Progresso incremental e consultas personalizadas
Progresso incremental durante a indexação garante que, se a execução do indexador é interrompida por falhas transitórias ou limite de tempo de execução, indexador Olá pode escolher onde parou próxima vez que ele é executado, em vez de ter a coleção inteira do índice toore saudação do zero. Isso é especialmente importante durante a indexação de coleções grandes. 

tooenable o progresso incremental ao usar uma consulta personalizada, certifique-se de que sua consulta ordena os resultados de saudação por Olá `_ts` coluna. Isso permite periódico seleção apontando para a pesquisa do Azure usa o progresso incremental tooprovide na presença de saudação de falhas.   

Em alguns casos, mesmo se a consulta contiver uma `ORDER BY [collection alias]._ts` cláusula, pesquisa do Azure pode não inferir que consultam Olá é ordenado pela Olá `_ts`. Você pode informar a pesquisa do Azure que os resultados são ordenados usando Olá `assumeOrderByHighWaterMarkColumn` propriedade de configuração. toospecify essa dica, criar ou atualizar o indexador da seguinte maneira: 

    {
     ... other indexer definition properties
     "parameters" : {
            "configuration" : { "assumeOrderByHighWaterMarkColumn" : true } }
    } 

<a name="DataDeletionDetectionPolicy"></a>
## <a name="indexing-deleted-documents"></a>Indexando documentos excluídos
Quando linhas são excluídas da coleção hello, normalmente deseja toodelete as linhas do índice de pesquisa de saudação. finalidade de saudação de uma política de detecção de exclusão de dados é tooefficiently identificar itens de dados excluídos. Atualmente, a política Olá só tem suportada é Olá `Soft Delete` política (exclusão está marcada com um sinalizador de algum tipo), que é especificado da seguinte maneira:

    {
        "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
        "softDeleteColumnName" : "hello property that specifies whether a document was deleted",
        "softDeleteMarkerValue" : "hello value that identifies a document as deleted"
    }

Se você estiver usando uma consulta personalizada, verifique se essa propriedade Olá referenciado pelo `softDeleteColumnName` projetado pela consulta hello.

saudação de exemplo a seguir cria uma fonte de dados com uma política de exclusão reversível:

    POST https://[Search service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
        "name": "mydocdbdatasource",
        "type": "documentdb",
        "credentials": {
            "connectionString": "AccountEndpoint=https://myDocDbEndpoint.documents.azure.com;AccountKey=myDocDbAuthKey;Database=myDocDbDatabaseId"
        },
        "container": { "name": "myDocDbCollectionId" },
        "dataChangeDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName": "_ts"
        },
        "dataDeletionDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
            "softDeleteColumnName": "isDeleted",
            "softDeleteMarkerValue": "true"
        }
    }

## <a name="NextSteps"></a>Próximas etapas
Parabéns! Você aprendeu como toointegrate Azure Cosmos DB com o uso de pesquisa do Azure Olá indexador para banco de dados do Cosmos.

* toolearn como mais sobre Azure Cosmos DB, consulte Olá [página de serviço do banco de dados do Cosmos](https://azure.microsoft.com/services/documentdb/).
* toolearn como mais sobre a pesquisa do Azure, consulte Olá [página de serviço de pesquisa](https://azure.microsoft.com/services/search/).
