---
title: blobs JSON aaaIndexing com indexador de blob de pesquisa do Azure
description: Indexando blobs JSON com o indexador de blobs da Pesquisa do Azure
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 57e32e51-9286-46da-9d59-31884650ba99
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/10/2017
ms.author: eugenesh
ms.openlocfilehash: 269968714358cd40ea66863b4dbb97766e1d77e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-json-blobs-with-azure-search-blob-indexer"></a>Indexando blobs JSON com o indexador de blobs da Pesquisa do Azure
Este artigo mostra como tooconfigure pesquisa do Azure blob indexador tooextract estruturado conteúdo de blobs que contêm JSON.

## <a name="scenarios"></a>Cenários
Por padrão, o [indexador de blobs da Pesquisa do Azure](search-howto-indexing-azure-blob-storage.md) analisa blobs JSON como um único bloco de texto. Geralmente, você deseja toopreserve estrutura de saudação de seus documentos JSON. Por exemplo, considerando o documento JSON Olá

    {
        "article" : {
             "text" : "A hopefully useful article explaining how tooparse JSON blobs",
            "datePublished" : "2016-04-13"
            "tags" : [ "search", "storage", "howto" ]    
        }
    }

Talvez você queira tooparse-lo em uma pesquisa do Azure um documento com campos "tags", "data de publicação" e "texto".

Como alternativa, quando seus blobs contêm um **matriz de objetos JSON**, convém cada elemento de saudação matriz toobecome um documento de pesquisa do Azure separado. Por exemplo, um blob com este JSON:  

    [
        { "id" : "1", "text" : "example 1" },
        { "id" : "2", "text" : "example 2" },
        { "id" : "3", "text" : "example 3" }
    ]

você pode popular o índice do Azure Search com três documentos separados, cada um com os campos "id" e "text".

> [!IMPORTANT]
> matriz JSON Olá análise funcionalidade está atualmente em visualização. Ele está disponível apenas no hello REST API com a versão **2015-02-28-visualização**. Lembre-se de que as APIs em visualização ia servem para teste e avaliação e não devem ser usadas em ambientes de produção.
>
>

## <a name="setting-up-json-indexing"></a>Configuração da indexação de JSON
Indexação de blobs do JSON é extração de documento regular toohello semelhante. Primeiro, crie a fonte de dados Olá exatamente como faria normalmente: 

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "optional, my-folder" }
    }   

Em seguida, crie índice de pesquisa de destino Olá se você ainda não tiver um. 

Por fim, crie um indexador e defina Olá `parsingMode` parâmetro muito`json` (tooindex cada blob como um único documento) ou `jsonArray` (se seus blobs contenham matrizes JSON, e é necessário que cada elemento de uma toobe matriz tratado como um documento separado):

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-json-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "parameters" : { "configuration" : { "parsingMode" : "json" } }
    }

Se necessário, use **mapeamentos de campo** toopick Olá propriedades de saudação fonte JSON documento usado toopopulate o índice de pesquisa de destino, conforme mostrado na próxima seção, Olá.

> [!IMPORTANT]
> Ao usar o modo de análise `json` ou `jsonArray`, o Azure Search pressupõe que todos os blobs em sua fonte de dados contêm JSON. Se você precisar toosupport uma mistura de JSON e JSON não blobs em Olá mesmo fonte de dados, nos informar em [nosso site UserVoice](https://feedback.azure.com/forums/263029-azure-search).
>
>

## <a name="using-field-mappings-toobuild-search-documents"></a>Usando documentos de pesquisa de toobuild de mapeamentos de campo
Atualmente, a Pesquisa do Azure não pode indexar documentos JSON arbitrários diretamente porque dá suporte somente a tipos de dados primitivos, matrizes de cadeia de caracteres e pontos GeoJSON. No entanto, você pode usar **mapeamentos de campo** toopick partes o JSON de documento e "comparação de precisão"-las nos campos de nível superior do documento da pesquisa de saudação. toolearn sobre noções básicas sobre mapeamentos de campo, consulte [mapeamentos de campo do indexador de pesquisa do Azure ligar as diferenças de saudação entre fontes de dados e índices de pesquisa](search-indexer-field-mappings.md).

Voltando tooour documento JSON de exemplo:

    {
        "article" : {
             "text" : "A hopefully useful article explaining how tooparse JSON blobs",
            "datePublished" : "2016-04-13"
            "tags" : [ "search", "storage", "howto" ]    
        }
    }

Digamos que você tenha um índice de pesquisa com hello campos a seguir: `text` do tipo `Edm.String`, `date` do tipo `Edm.DateTimeOffset`, e `tags` do tipo `Collection(Edm.String)`. toomap forma desejada do seu JSON em hello, use Olá mapeamentos de campo a seguir:

    "fieldMappings" : [
        { "sourceFieldName" : "/article/text", "targetFieldName" : "text" },
        { "sourceFieldName" : "/article/datePublished", "targetFieldName" : "date" },
        { "sourceFieldName" : "/article/tags", "targetFieldName" : "tags" }
      ]

Olá nomes de campo de fonte de mapeamentos de saudação são especificados usando Olá [JSON ponteiro](http://tools.ietf.org/html/rfc6901) notação. Você começar com uma raiz de toohello toorefer barra do documento JSON, depois selecione a propriedade Olá desejado (nível arbitrário de aninhamento) usando encaminhamento caminho separados por barra.

Você também pode consultar tooindividual elementos da matriz, usando um índice com base em zero. Por exemplo, toopick Olá primeiro elemento da matriz de "tags" hello da saudação acima como exemplo, use um mapeamento de campo como este:

    { "sourceFieldName" : "/article/tags/0", "targetFieldName" : "firstTag" }

> [!NOTE]
> Se um nome de campo de origem em um caminho de mapeamento de campo refere-se a propriedade tooa que não existe em JSON, esse mapeamento é ignorado sem erro. Isso é feito para que possamos dar suporte a documentos com um esquema diferente (o que é um caso de uso comum). Porque não há nenhuma validação, você precisa de erros de digitação tootake cuidado tooavoid na especificação do mapeamento de campo.
>
>

Se seus documentos JSON contiverem somente propriedades simples de nível superior, talvez você não precise de mapeamentos de campo. Por exemplo, se o JSON se parece com este, propriedades de nível superior hello "text", "data de publicação" e "q" diretamente mapeia toohello de campos correspondentes no índice de pesquisa de saudação:

    {
       "text" : "A hopefully useful article explaining how tooparse JSON blobs",
       "datePublished" : "2016-04-13"
       "tags" : [ "search", "storage", "howto" ]    
     }

Aqui está um conteúdo completo do indexador com mapeamentos de campo:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-json-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "parameters" : { "configuration" : { "parsingMode" : "json" } },
      "fieldMappings" : [
        { "sourceFieldName" : "/article/text", "targetFieldName" : "text" },
        { "sourceFieldName" : "/article/datePublished", "targetFieldName" : "date" },
        { "sourceFieldName" : "/article/tags", "targetFieldName" : "tags" }
        ]
    }

## <a name="indexing-nested-json-arrays"></a>Indexação de matrizes aninhadas de JSON
Se desejar que tooindex uma matriz de objetos JSON, mas essa matriz está aninhado em algum lugar no documento Olá? Você pode escolher qual propriedade contém a matriz de saudação usando Olá `documentRoot` propriedade de configuração. Por exemplo, se o seu blob tiver esta aparência:

    {
        "level1" : {
            "level2" : [
                { "id" : "1", "text" : "Use hello documentRoot property" },
                { "id" : "2", "text" : "toopluck hello array you want tooindex" },
                { "id" : "3", "text" : "even if it's nested inside hello document" }  
            ]
        }
    }

Use essa matriz de saudação de tooindex configuração contida na Olá `level2` propriedade:

    {
        "name" : "my-json-array-indexer",
        ... other indexer properties
        "parameters" : { "configuration" : { "parsingMode" : "jsonArray", "documentRoot" : "/level1/level2" } }
    }

## <a name="help-us-make-azure-search-better"></a>Ajude-nos a aprimorar o Azure Search
Se você tiver solicitações de recursos ou ideias para melhorias, alcançar toous em nosso [site UserVoice](https://feedback.azure.com/forums/263029-azure-search/).
