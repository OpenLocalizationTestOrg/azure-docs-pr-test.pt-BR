---
title: "AAA \"consultar um índice (portal - pesquisa do Azure) | Microsoft Docs\""
description: Execute uma consulta de pesquisa no Gerenciador de pesquisa do Portal do Azure hello.
services: search
manager: jhubbard
documentationcenter: 
author: ashmaka
ms.assetid: 8e524188-73a7-44db-9e64-ae8bf66b05d3
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 07/10/2017
ms.author: ashmaka
ms.openlocfilehash: 56bab3ef8a66eeb053fbbeb6d322acb6824fb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="query-an-azure-search-index-using-search-explorer-in-hello-azure-portal"></a>Consultar um índice de pesquisa do Azure usando o Gerenciador de pesquisa no hello Portal do Azure
> [!div class="op_single_selector"]
> * [Visão geral](search-query-overview.md)
> * [Portal](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

Este artigo mostra como tooquery uma pesquisa do Azure índice usando **Search Explorer** em Olá portal do Azure. Você pode usar pesquisa Explorer toosubmit simple ou completo Lucene consulta cadeias de caracteres tooany existente índice em seu serviço.

## <a name="open-hello-service-dashboard"></a>Painel de serviço abrir Olá
1. Clique em **todos os recursos** na barra de salto Olá Olá lado esquerdo da saudação [portal do Azure](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).
2. Selecione o serviço Azure Search.

## <a name="select-an-index"></a>Selecionar um índice

Índice Olá selecione você gostaria que toosearch de saudação **índices** lado a lado.

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a>Abrir o Search Explorer

Clique em Olá barra de pesquisa do Gerenciador de pesquisa bloco tooslide Olá aberto e o painel de resultados.

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a>Iniciar a pesquisa

Ao usar o hello Explorer de pesquisa, você pode especificar [parâmetros de consulta](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) tooformulate consulta de saudação.

1. Em **Cadeia de caracteres de consulta**, digite uma consulta e então pressione **Pesquisar**. 

   cadeia de caracteres de consulta de saudação é automaticamente analisada em solicitação adequada Olá URL toosubmit uma solicitação HTTP em relação a saudação API de REST de pesquisa do Azure.   
   
   Você pode usar qualquer válido simple ou completa Lucene sintaxe toocreate Olá solicitação de consulta. Olá `*` caractere é equivalente tooan pesquisa vazia ou não especificado que retorna todos os documentos em nenhuma ordem específica.

2. Em **resultados**, resultados da consulta são apresentados em JSON bruto, carga toohello idênticos retornados em um corpo de resposta HTTP ao emitir solicitações de forma programática.

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a>Próximas etapas

Olá recursos a seguir fornece exemplos e informações de sintaxe de consulta adicionais.

 + [Sintaxe de consulta simples](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [Sintaxe de consulta Lucene](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [Exemplos de sintaxe de consulta Lucene](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + [Sintaxe de expressão do filtro OData](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) 