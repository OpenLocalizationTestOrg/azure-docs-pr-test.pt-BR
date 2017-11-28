---
title: aaaIndexing CSV de blobs do indexador de blob de pesquisa do Azure | Microsoft Docs
description: Saiba como blobs de tooindex CSV com a pesquisa do Azure
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: ed3c9cff-1946-4af2-a05a-5e0b3d61eb25
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 12/15/2016
ms.author: eugenesh
ms.openlocfilehash: f2b1ce824e62c5b3f6155c6e88887897cf1a8eae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-csv-blobs-with-azure-search-blob-indexer"></a>Indexando blobs CSV com o indexador de blobs da Pesquisa do Azure
Por padrão, o [indexador de blobs da Pesquisa do Azure](search-howto-indexing-azure-blob-storage.md) analisa blobs de texte delimitado como um único bloco de texto. No entanto, com blobs que contêm dados CSV, geralmente é necessário tootreat cada linha no blob hello como um documento separado. Por exemplo, fornecido Olá seguinte texto delimitado: 

    id, datePublished, tags
    1, 2016-01-12, "azure-search,azure,cloud" 
    2, 2016-07-07, "cloud,mobile" 

Talvez você queira tooparse-lo em 2 documentos, cada um contendo campos de "tags", "data de publicação" e "id".

Neste artigo, você aprenderá como blobs de tooparse CSV com um indexador de blob de pesquisa do Azure. 

> [!IMPORTANT]
> Esta funcionalidade está em preview. Ele está disponível apenas no hello REST API com a versão **2015-02-28-visualização**. Lembre-se de que as APIs de visualização servem para teste e avaliação, e não devem ser usadas em ambientes de produção. 
> 
> 

## <a name="setting-up-csv-indexing"></a>Configurando a indexação de CSV
blobs CSV tooindex, criar ou atualizar uma definição do indexador com hello `delimitedText` modo de análise:  

    {
      "name" : "my-csv-indexer",
      ... other indexer properties
      "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "firstLineContainsHeaders" : true } }
    }

Para obter mais detalhes sobre Olá criar indexador API, check-out [criar indexador](search-api-indexers-2015-02-28-preview.md#create-indexer).

`firstLineContainsHeaders`indica que a primeira linha de (não está em branco) saudação de cada blob contém cabeçalhos.
Se blobs não contém uma linha de cabeçalho inicial, cabeçalhos de saudação devem ser especificados na configuração do indexador hello: 

    "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "delimitedTextHeaders" : "id,datePublished,tags" } } 

Atualmente, a codificação de UTF-8 Olá somente tem suporte. Além disso, somente Olá vírgula `','` caractere tem suporte como Olá delimitador. Se você precisa de suporte para outras codificações ou delimitadores, informe-nos em [nosso site UserVoice](https://feedback.azure.com/forums/263029-azure-search).

> [!IMPORTANT]
> Quando você usa o modo de pesquisa do Azure de análise de texto de saudação delimitada presume que todos os blobs na fonte de dados será CSV. Se você precisar toosupport uma mistura de CSV e não CSV blobs em Olá mesmo fonte de dados, informe-nos em [nosso site UserVoice](https://feedback.azure.com/forums/263029-azure-search).
> 
> 

## <a name="request-examples"></a>Exemplos de solicitação
Reunindo todos juntos, aqui estão exemplos de carga completo hello. 

Fonte de dados: 

    POST https://[service name].search.windows.net/datasources?api-version=2015-02-28-Preview
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "<optional, my-folder>" }
    }   

Indexador:

    POST https://[service name].search.windows.net/indexers?api-version=2015-02-28-Preview
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-csv-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "delimitedTextHeaders" : "id,datePublished,tags" } }
    }

## <a name="help-us-make-azure-search-better"></a>Ajude-nos a aprimorar o Azure Search
Se você tiver solicitações de recursos ou ideias para melhorias, entre em contato toous em nosso [site UserVoice](https://feedback.azure.com/forums/263029-azure-search/).

