---
title: resultados da pesquisa de toopage de aaaHow na pesquisa do Azure | Microsoft Docs
description: "Paginação na Pesquisa do Azure, um serviço de pesquisa de nuvem hospedado do Microsoft Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
ms.assetid: a0a1d315-8624-4cdf-b38e-ba12569c6fcc
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/29/2016
ms.author: heidist
ms.openlocfilehash: e3abc1ca4d5994b0a77955379081a4fcfa5a7fa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopage-search-results-in-azure-search"></a>Como os resultados de pesquisa toopage na pesquisa do Azure
Este artigo fornece orientação sobre como toouse Olá API de REST do serviço de pesquisa do Azure tooimplement elementos padrão de uma pesquisa de página de resultados, como contagens do total, recuperação de documentos, ordens de classificação e navegação.

Em cada caso mencionado a seguir, relacionados à página de opções que contribuem com dados ou informações tooyour página resultados da pesquisa são especificadas por meio de saudação [pesquisar documento](http://msdn.microsoft.com/library/azure/dn798927.aspx) solicitações enviadas tooyour serviço de pesquisa do Azure. Solicitações incluem um comando GET, caminho e os parâmetros de consulta que informam o serviço de saudação que está sendo solicitado e como tooformulate Olá resposta.

> [!NOTE]
> Uma solicitação válida inclui diversos elementos, como uma URL de serviço e o caminho, o verbo HTTP, `api-version` etc. Para resumir, podemos cortados Olá exemplos toohighlight Olá apenas sintaxe toopagination relevante. Consulte Olá [API de REST do serviço de pesquisa do Azure](http://msdn.microsoft.com/library/azure/dn798935.aspx) documentação para obter detalhes sobre a sintaxe de solicitação.
> 
> 

## <a name="total-hits-and-page-counts"></a>Total de ocorrências e contagens de página
Mostrar Olá total do número de resultados retornados por uma consulta e, em seguida, retornar os resultados em partes menores, é fundamental toovirtually todas as páginas de pesquisa.

![][1]

Na pesquisa do Azure, você usar Olá `$count`, `$top`, e `$skip` parâmetros tooreturn esses valores. Olá, exemplo a seguir mostra uma solicitação de exemplo para o total de acertos, retornados como `@OData.count`:

        GET /indexes/onlineCatalog/docs?$count=true

Recupere documentos em grupos de 15 e também mostra o total de acertos hello, começando na primeira página do hello:

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

Resultados de paginação requer `$top` e `$skip`, onde `$top` Especifica quantos tooreturn de itens em um lote e `$skip` Especifica quantos tooskip de itens. Olá seguinte exemplo, cada página mostra Olá itens lado 15, indicadas pela saltos incremental de saudação em Olá `$skip` parâmetro.

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=15&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=30&$count=true

## <a name="layout"></a>Layout
Em uma página de resultados de pesquisa, talvez você queira tooshow uma imagem em miniatura, um subconjunto de campos e uma página do link tooa completa do produto.

 ![][2]

Pesquisa do Azure, você usaria `$select` e uma pesquisa de comando tooimplement essa experiência.

tooreturn um subconjunto de campos para um layout lado a lado:

        GET /indexes/ onlineCatalog/docs?search=*&$select=productName,imageFile,description,price,rating 

Arquivos de mídia e imagens não são diretamente pesquisáveis e devem ser armazenados em outra plataforma de armazenamento, como o armazenamento de BLOBs do Azure, os custos de tooreduce. No índice hello e documentos, defina um campo que armazena o endereço de URL de saudação do conteúdo externo hello. Em seguida, você pode usar o campo hello como uma referência de imagem. imagem de toohello URL Olá deve estar no documento hello.

tooretrieve uma descrição do produto da página para um **onClick** evento, use [pesquisar documento](http://msdn.microsoft.com/library/azure/dn798929.aspx) toopass na chave de saudação do hello tooretrieve de documento. saudação de tipo de dados da chave de saudação é `Edm.String`. Neste exemplo, é *246810*. 

        GET /indexes/onlineCatalog/docs/246810

## <a name="sort-by-relevance-rating-or-price"></a>Classificar por relevância, por classificação ou por preço
Ordens de classificação geralmente padrão toorelevance, mas é comum ordens de classificação alternativa de toomake prontamente disponíveis para que os clientes podem rapidamente rearranjas essas resultados existentes em uma ordem de classificação diferente.

 ![][3]

Na pesquisa do Azure, a classificação é baseada em Olá `$orderby` expressão para todos os campos são indexados como`"Sortable": true.`

A relevância está fortemente associada a perfis de pontuação. Você pode usar saudação padrão de pontuação, que se baseia em ordem de toorank de análise e estatísticas de texto todos os resultados com pontuações mais altas toodocuments com mais ou mais correspondências um termo de pesquisa em andamento.

Ordens de classificação alternativa normalmente estão associadas **onClick** eventos que o retorno de chamada tooa método que cria a ordem de classificação de saudação. Por exemplo, este elemento de página:

 ![][4]

Você deve criar um método que aceita a opção de classificação de saudação selecionada como entrada e retorna uma lista ordenada para critérios de saudação associados a essa opção.

 ![][5]

> [!NOTE]
> Enquanto a pontuação do saudação padrão é suficiente para muitos cenários, é recomendável baseando relevantes em um perfil de pontuação personalizado em vez disso. Um perfil de pontuação personalizado oferece uma forma como os itens tooboost que são mais benéfico tooyour para os negócios. Confira [Adicionar um perfil de pontuação](http://msdn.microsoft.com/library/azure/dn798928.aspx) para saber mais. 
> 
> 

## <a name="faceted-navigation"></a>Navegação facetada
Navegação de pesquisa é comum em uma página de resultados, geralmente localizada no lado de saudação ou superior de uma página. Na Pesquisa do Azure, a navegação facetada proporciona uma pesquisa autodirecionada com base em filtros predefinidos. Confira [Navegação facetada na Pesquisa do Azure](search-faceted-navigation.md) para mais detalhes.

## <a name="filters-at-hello-page-level"></a>Filtros no nível de página Olá
Se seu design de solução incluído páginas de pesquisa dedicado para tipos específicos de conteúdo (por exemplo, um aplicativo de varejo online que tem departamentos listados na parte superior de saudação da página Olá), você pode inserir uma expressão de filtro junto com um **onClick** evento tooopen uma página em um estado pré-filtrada. 

Você pode enviar um filtro com ou sem uma expressão de pesquisa. Por exemplo, hello solicitação a seguir filtra em nome de marca, retornando somente os documentos que correspondem a ele.

        GET /indexes/onlineCatalog/docs?$filter=brandname eq ‘Microsoft’ and category eq ‘Games’

Confira [Pesquisar Documentos (API de Pesquisa do Azure)](http://msdn.microsoft.com/library/azure/dn798927.aspx) para saber mais sobre expressões `$filter`.

## <a name="see-also"></a>Consulte também
* [API REST do Serviço de Pesquisa do Azure](http://msdn.microsoft.com/library/azure/dn798935.aspx)
* [Operações de índice](http://msdn.microsoft.com/library/azure/dn798918.aspx)
* [Operações de documento.](http://msdn.microsoft.com/library/azure/dn800962.aspx)
* [Vídeos e tutoriais sobre a Pesquisa do Azure](search-video-demo-tutorial-list.md)
* [Navegação facetada na Pesquisa do Azure](search-faceted-navigation.md)

<!--Image references-->
[1]: ./media/search-pagination-page-layout/Pages-1-Viewing1ofNResults.PNG
[2]: ./media/search-pagination-page-layout/Pages-2-Tiled.PNG
[3]: ./media/search-pagination-page-layout/Pages-3-SortBy.png
[4]: ./media/search-pagination-page-layout/Pages-4-SortbyRelevance.png
[5]: ./media/search-pagination-page-layout/Pages-5-BuildSort.png 
