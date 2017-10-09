---
title: "Índice de pesquisa do Azure aaaQuery | Microsoft Docs"
description: "Criar uma consulta de pesquisa na pesquisa do Azure e usar os resultados da pesquisa pesquisa parâmetros toofilter e classificação."
services: search
manager: jhubbard
documentationcenter: 
author: ashmaka
ms.assetid: 69205d7a-363f-4b92-a53f-6ca818a3d2c7
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: ashmaka
ms.openlocfilehash: 4a5ffffe179695fc09446760e21a738dd36c29b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index"></a>Consultar seu índice de Pesquisa do Azure
> [!div class="op_single_selector"]
> * [Visão geral](search-query-overview.md)
> * [Portal](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

Ao enviar solicitações de pesquisa tooAzure pesquisa, há um número de parâmetros que pode ser especificado junto com hello real de palavras que é digitados na caixa de pesquisa de saudação do seu aplicativo. Esses parâmetros de consulta permitem que você tooachieve algum controle mais profunda da saudação [experiência de pesquisa de texto completo](search-lucene-query-architecture.md).

Abaixo está uma lista que explica os usos comuns dos parâmetros de consulta Olá na pesquisa do Azure. Cobertura completa de parâmetros de consulta e seu comportamento, consulte Olá detalhadas páginas para Olá [API REST](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) e [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters#microsoft_azure_search_models_searchparameters#properties_summary).

## <a name="types-of-queries"></a>Tipos de consultas
A pesquisa do Azure oferece muitas consultas extremamente eficiente toocreate de opções. Olá dois principais tipos de consulta que você usará são `search` e `filter`. Um `search` consulta procura por um ou mais termos em todos os *pesquisável* campos no índice e funcionamento Olá você esperaria de um mecanismo de pesquisa como o Google ou Bing toowork. Uma consulta `filter` avalia uma expressão booliana em todos os campos *filtráveis* em um índice. Ao contrário de `search` consultas, `filter` consultas correspondem o conteúdo exato de saudação de um campo, o que significa que eles diferenciam maiusculas de minúsculas para campos de cadeia de caracteres.

Você pode usar pesquisas e filtros juntos ou separados. Se você usá-los juntos, o filtro de saudação é aplicada primeiro índice de inteiro toohello e, em seguida, pesquisa de saudação é executada em resultados de saudação do filtro de saudação. Filtros, portanto, podem ser um desempenho de consulta tooimprove técnica útil, pois elas reduzem o conjunto de saudação de documentos que Olá tooprocess de necessidades de consulta de pesquisa.

sintaxe de saudação para expressões de filtro é um subconjunto de saudação [idioma de filtro OData](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search). Para consultas de pesquisa, você pode usar o hello [simplificado sintaxe](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search) ou hello [sintaxe de consulta do Lucene](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search) que é discutido abaixo.

### <a name="simple-query-syntax"></a>Sintaxe de consulta simples
Olá [sintaxe de consulta simples](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search) é a linguagem de consulta padrão Olá usada na pesquisa do Azure. sintaxe de consulta simples Olá dá suporte a um número de operadores de pesquisa comuns, incluindo Olá AND, OR, não, a frase, sufixo e operadores de precedência.

### <a name="lucene-query-syntax"></a>sintaxe de consulta Lucene
Olá [sintaxe de consulta do Lucene](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search) permite que você toouse Olá amplamente adotado e linguagem de consulta expressivas desenvolvidos como parte da [Apache Lucene](https://lucene.apache.org/core/4_10_2/queryparser/org/apache/lucene/queryparser/classic/package-summary.html).

Usando a sintaxe de consulta permite que você tooeasily atingir Olá recursos a seguir: [consultas com escopo de campo](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_fields), [pesquisa difusa](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_fuzzy), [pesquisa por proximidade](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_proximity), [ aumento de termos](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_termboost), [pesquisa de expressão regular](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_regex), [pesquisa curinga](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_wildcard), [conceitos básicos de sintaxe](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_syntax), e [as consultas que usam operadores boolianos](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_boolean).

## <a name="ordering-results"></a>Ordenando resultados
Ao receber os resultados de uma consulta de pesquisa, você pode solicitar que a pesquisa do Azure serve resultados Olá ordenados por valores em um campo específico. Por padrão, pesquisa do Azure ordena os resultados da pesquisa Olá com base na classificação de saudação da pontuação de pesquisa de cada documento, que é derivada de [TF-IDF](https://en.wikipedia.org/wiki/Tf%E2%80%93idf).

Se você quiser tooreturn de pesquisa do Azure, seus resultados ordenados por um valor diferente de pontuação de pesquisa hello, você pode usar o hello `orderby` parâmetro de pesquisa. Você pode especificar o valor Olá Olá `orderby` nomes de campo do parâmetro tooinclude e chama toohello [ `geo.distance()` função](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search) para valores geospaciais. Cada expressão pode ser seguido por `asc` tooindicate que os resultados são solicitados em ordem crescente, e `desc` tooindicate que os resultados são solicitados em ordem decrescente. classificação de padrão de saudação ordem crescente.

## <a name="paging"></a>Paginamento
A pesquisa do Azure torna fácil tooimplement paginação de resultados da pesquisa. Usando Olá `top` e `skip` parâmetros, você pode emitir perfeitamente solicitações de pesquisa que permitir que você tooreceive Olá total conjunto de resultados da pesquisa em subconjuntos gerenciáveis, ordenados que habilitar facilmente as práticas recomendadas da interface do usuário de pesquisa válida. Ao receber esses subconjuntos menores de resultados, você também pode receber a contagem de saudação de documentos no conjunto de saudação total dos resultados da pesquisa.

Você pode aprender mais sobre paginação de resultados da pesquisa no artigo Olá [como os resultados de pesquisa toopage na pesquisa do Azure](search-pagination-page-layout.md).

## <a name="hit-highlighting"></a>Realce de ocorrência
Na pesquisa do Azure, enfatizando a parte exata Olá dos resultados da pesquisa que correspondam à consulta de pesquisa Olá fica mais fácil usando Olá `highlight`, `highlightPreTag`, e `highlightPostTag` parâmetros. Você pode especificar qual *pesquisável* campos devem ter o texto correspondente enfatizado, bem como especificar Olá exata cadeia de caracteres de marcas tooappend toohello inicial e final da saudação corresponde ao texto que a pesquisa do Azure retorna.

## <a name="try-out-query-syntax"></a>Experimente a sintaxe de consulta

diferenças de sintaxe de toounderstand de maneira melhor de saudação é pelo envio de consultas e revisar os resultados.

+ Use [Search Explorer](search-explorer.md) em Olá portal do Azure. Implantando [índice de exemplo hello](search-get-started-portal.md), você pode consultar o índice de saudação em minutos, usando as ferramentas no portal de saudação.

+ Use [Fiddler](search-fiddler.md) ou Chrome carteiro toosubmit consultas tooan índice que você carregou tooyour serviço de pesquisa. Ambas as ferramentas de suporte para o ponto de extremidade do REST chamadas tooan HTTP. 
