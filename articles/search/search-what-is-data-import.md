---
title: carregamento de aaaData na pesquisa do Azure | Microsoft Docs
description: "Saiba como tooupload tooan de dados de índice na pesquisa do Azure."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: 
ms.assetid: aa8d47c1-4ae6-4209-a8ce-48d5a9474707
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: ashmaka
ms.openlocfilehash: a95eae94f72c1d0926804ff7e1152f21773fcabf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search"></a>Carregar dados tooAzure pesquisa
> [!div class="op_single_selector"]
> * [Visão geral](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
> 
> 

Há toopopulate de duas maneiras de um índice com seus dados. opção primeira Olá manualmente é enviar seus dados no índice de saudação usando Olá pesquisa do Azure [API REST](search-import-data-rest-api.md) ou [.NET SDK](search-import-data-dotnet.md). Olá segunda opção é muito[do ponto de uma fonte de dados com suporte](search-indexer-overview.md) tooyour índice e permitir que a pesquisa do Azure extraem dados saudação automaticamente.

## <a name="push-data-tooan-index"></a>Índice de tooan de dados por push
Essa abordagem se refere a tooprogrammatically enviar seu toomake de pesquisa de tooAzure de dados disponível para pesquisa. Para aplicativos com requisitos de latência muito baixa (por exemplo, se você precisar pesquisar operações toobe em sincronia com bancos de dados de inventário dinâmico), o modelo de push Olá é a única opção.

Você pode usar o hello [API REST](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents) ou [.NET SDK](search-import-data-dotnet.md) toopush dados tooan índice. Atualmente, não há nenhum suporte de ferramenta para envio de dados por meio do portal de saudação.

Essa abordagem é mais flexível que o modelo de pull Olá porque você pode carregar documentos individualmente ou em lotes (backup too1000 por lote ou 16 MB, o limite que ocorrer primeiro). modelo de push Olá também permite que você tooupload documentos tooAzure pesquisa, independentemente de onde os dados estão.

formato de dados Olá entendido por pesquisa do Azure é JSON, e todos os documentos no conjunto de dados Olá devem ter campos mapeados toofields definido em seu esquema de índice. 

## <a name="pull-data-into-an-index"></a>Extrair dados para um índice
modelo de pull Olá rastreia uma fonte de dados com suporte e carrega automaticamente os dados de saudação em seu índice. No Azure Search, esse recurso é implementado por meio de *indexadores*, disponíveis no momento para o [Armazenamento de blobs](search-howto-indexing-azure-blob-storage.md), [Armazenamento de tabelas](search-howto-indexing-azure-tables.md), [Azure Cosmos DB](http://aka.ms/documentdb-search-indexer), [banco de dados SQL do Azure e SQL Server nas VMs do Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md). 

Indexadores se conectar a uma fonte de dados tooa do índice (geralmente uma tabela, exibição ou estrutura equivalente) e tooequivalent campos de origem no índice de saudação do mapa. Durante a execução, o conjunto de linhas de saudação é tooJSON automaticamente transformado e carregados no índice especificado da saudação. Todos os indexadores oferece suporte à programação para que você pode especificar a frequência com dados saudação toobe atualizado. A maioria dos indexadores fornecem controle de alterações se a fonte de dados Olá dá suporte a ele. Controle de alterações e exclusões tooexisting documentos além do toorecognizing novos documentos, indexadores eliminar a necessidade de saudação tooactively gerenciar dados Olá no índice. 

Indexador funcionalidade é exposta no hello [portal do Azure](search-import-data-portal.md), Olá [API REST](/rest/api/searchservice/Indexer-operations)e hello [.NET SDK](/dotnet/api/microsoft.azure.search.indexersoperations). 

Um portal de saudação toousing vantagem é que a pesquisa do Azure pode geralmente gerar um esquema de índice padrão para você ao ler metadados de saudação do conjunto de dados de origem de saudação. Você pode modificar o índice gerado Olá até que o índice de saudação é processado, após o qual Olá edições de esquema somente permitido são aqueles que não exigem reindexação. Se alterações Olá desejadas toomake impacto hello esquema diretamente, você precisaria toorebuild índice de saudação. 

Depois que o índice Olá for preenchida, você pode usar **Search Explorer** na barra de comando portal hello como uma etapa de verificação.

## <a name="query-an-index-using-search-explorer"></a>Consultar um índice usando o Search Explorer

Uma maneira rápida de tooperform uma verificação preliminar no carregamento do documento hello é toouse **Search Explorer** no portal de saudação. explorer Olá lhe permite consultar um índice sem ter que toowrite qualquer código. Olá experiência de pesquisa é com base nas configurações padrão, como Olá [sintaxe simples](/rest/api/searchservice/simple-query-syntax-in-azure-search) e padrão [searchMode parâmetro de consulta](/rest/api/searchservice/search-documents). Resultados são retornados em JSON, para que você pode inspecionar o documento inteiro hello.

> [!TIP]
> Vários [exemplos de código de pesquisa do Azure](https://github.com/Azure-Samples/?utf8=%E2%9C%93&query=search) incluem prontamente disponíveis ou inseridos conjuntos de dados, oferecendo uma maneira fácil tooget iniciado. portal de saudação também fornece um indexador de exemplo e uma fonte de dados consiste em um conjunto de dados de imóveis pequeno ("realestate-us-exemplo nomeado"). Quando você executar o indexador pré-configurado Olá na fonte de dados de exemplo hello, um índice é criado e carregado com documentos que podem ser consultados, em seguida, no Gerenciador de pesquisa ou pelo código que você escreve.
