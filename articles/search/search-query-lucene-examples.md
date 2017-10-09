---
title: exemplos de consulta aaaLucene pesquisa do Azure | Microsoft Docs
description: "Sintaxe de consulta Lucene para pesquisa difusa, pesquisa por proximidade, aumento de termos, pesquisa com expressão regular e pesquisa com curinga."
services: search
documentationcenter: 
author: LiamCa
manager: pablocas
editor: 
tags: Lucene query analyzer syntax
ms.assetid: 147f360d-a5ce-4d7b-a909-c8b65bfb748c
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/21/2017
ms.author: liamca
ms.openlocfilehash: d859cf697ef9485a49e9e0591b68e812ffa55f1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="lucene-query-syntax-examples-for-building-queries-in-azure-search"></a>Exemplos de sintaxe de consulta Lucene para criar consultas no Azure Search
Ao construir consultas de pesquisa do Azure, você pode usar o padrão de saudação [sintaxe de consulta simples](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) ou saudação alternativa [Lucene analisador de consulta na pesquisa do Azure](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search). Olá Lucene analisador de consulta dá suporte a construções de consulta mais complexas, como consultas com escopo de campo, pesquisa difusa, pesquisa por proximidade, aumentando o termo e pesquisa de expressão regular.

Neste artigo, você pode percorrer exemplos que demonstram operações de consulta disponíveis ao usar a sintaxe completa da saudação.

## <a name="viewing-hello-examples-in-jsfiddle"></a>Exibindo exemplos Olá JSFiddle

Todos os exemplos de saudação neste artigo são executáveis consultas executadas em um índice de pesquisa pré-carregado em [JSFiddle](https://jsfiddle.net), um editor de código on-line para testar o script e HTML. 

toorun-los, clique em Olá consulta exemplo URLs tooopen JSFiddle em uma janela separada do navegador.

> [!NOTE]
> exemplos a seguir Hello aproveitam um índice de pesquisa que consiste em trabalhos disponíveis com base em um conjunto de dados fornecido pelo Olá [cidade de Nova York OpenData](https://nycopendata.socrata.com/) iniciativa. Esses dados não devem ser considerados atuais ou completos. índice de saudação esteja em um serviço de proteção fornecido pela Microsoft. Você não precisa de uma assinatura do Azure ou a pesquisa do Azure tootry essas consultas.
>


## <a name="how-tooinvoke-full-lucene-parsing"></a>Como tooinvoke completo Lucene análise

Todos os exemplos neste artigo Olá especificar Olá **queryType = full** parâmetro, indicando que sintaxe completa da saudação, tratada pelo Olá Lucene analisador de consulta de pesquisa. 

**Exemplo 1** - Olá atalho tooopen de trecho de código de consulta em um navegador nova página a seguir carrega JSFiddle e executa Olá consulta:

* [&queryType=full&search=*](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26searchFields=business_title%26$select=business_title%26queryType=full%26search=*)

Na nova janela do navegador Olá origem de JavaScript hello e saída HTML são apresentados lado a lado. Olá script fizer referência a uma consulta completa (não apenas Olá trecho de código, conforme mostrado no link de saudação). consulta completa Olá é mostrada no hello URLs para cada exemplo. 

Essa consulta retorna documentos de nosso índice New York City Jobs (nycjobs, carregado em um serviço de área restrita). Para resumir, a consulta de saudação especifica apenas os títulos de negócios são retornados. consulta de base completa Olá é o seguinte:

    http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26searchFields=business_title%26$select=business_title%26queryType=full%26search=*

Olá **searchFields** parâmetro restringe Olá pesquisa toojust Olá business o campo do título. Olá **queryType** está definido muito**completo**, que instrui o hello toouse de pesquisa do Azure, Lucene analisador de consulta para esta consulta.

> [!NOTE]
> Para saber o contexto do processamento da consulta, consulte [Como funciona a pesquisa de texto completo no Azure Search](search-lucene-query-architecture.md). Para obter mais informações sobre parâmetros de pesquisa, consulte [Pesquisar documentos (API REST do serviço Azure Search)](https://docs.microsoft.com/rest/api/searchservice/Search-Documents).
>

### <a name="fielded-query-operation"></a>Operação de consulta por campo
Você pode modificar os exemplos neste artigo Olá especificando um **fieldname:searchterm** toodefine de construção uma operação de consulta por campo, onde campo Olá é uma palavra única, e o termo de pesquisa Olá também é uma única palavra ou frase, Opcionalmente, com operadores boolianos. Alguns exemplos incluem o seguinte hello:

* business_title:(sênior NOT júnior)
* state:(“Nova York” AND “Nova Jersey”)

Ser tooput se várias cadeias de caracteres entre aspas se você quiser que os dois toobe de cadeias de caracteres avaliada como uma única entidade, como neste caso procurando duas cidades diferentes no campo de local de saudação. Além disso, certifique-se de operador hello está em letras maiusculas como você pode ver com NOT e and.

campo de saudação especificado na **fieldname:searchterm** deve ser um campo pesquisável. Confira [Create Index (Azure Search Service REST API)](https://docs.microsoft.com/rest/api/searchservice/create-index) (Criar índice [API REST do Serviço Azure Search]) para obter detalhes sobre como os atributos de índice são usados em definições de campo.

**Exemplo 2** – consulta a seguir do botão direito do mouse Olá trecho esta consulta procura por títulos de negócios com hello termo sênior nelas, mas não júnior:

* [&queryType=full&search= business_title:senior NOT junior](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:senior+NOT+junior)

## <a name="fuzzy-search-example"></a>Exemplo de pesquisa difusa
Uma pesquisa difusa encontra correspondências em termos com uma construção semelhante. De acordo com a [documentação do Lucene](https://lucene.apache.org/core/4_10_2/queryparser/org/apache/lucene/queryparser/classic/package-summary.html), as pesquisas imprecisas se baseiam na [distância de Damerau-Levenshtein](https://en.wikipedia.org/wiki/Damerau%e2%80%93Levenshtein_distance).

toodo uma pesquisa difusa, acrescente til hello "~" símbolo final de saudação de uma única palavra com um parâmetro opcional, um valor entre 0 e 2, que especifica a distância de edição de saudação. Por exemplo, "mar~" ou "mar~1" retornaria mar, amar e maré.

**Exemplo 3** – trecho de consulta a seguir de saudação com o botão direito. Essa consulta pesquisa trabalhos com associação de termo hello (onde ele está escrito incorretamente):

* [&queryType=full&search= business_title:asosiate~](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:asosiate~)

> [!Note]
> Consultas difusas não são [analisadas](https://docs.microsoft.com/azure/search/search-lucene-query-architecture#stage-2-lexical-analysis), o que poderá ser uma surpresa se você esperar a lematização. A análise lexical é realizada somente em termos completos (uma consulta de termo ou de frase). Tipos de consulta com os termos incompletos (consulta de prefixo, consulta curinga, regex consulta, consulta difusa) são adicionados diretamente toohello árvore de consulta, ignorando o estágio de análise de saudação. Olá somente transformação executada em termos de consulta incompleta é minúsculas.
>

## <a name="proximity-search-example"></a>Exemplo de pesquisa por proximidade
Pesquisas de proximidade são termos usados toofind que estão próximos um do outro em um documento. Inserir um til "~" símbolo final de saudação de uma frase seguido pelo número de saudação de palavras que criar hello proximidade limite. Por exemplo, "aeroporto de hotel" ~ 5 encontrará hotel de termos hello e aeroporto dentro de 5 palavras uns dos outros em um documento.

**Exemplo 4** -consulta de saudação do botão direito do mouse. Pesquise trabalhos com o termo hello "analista sênior" onde ele é separado por não mais de uma palavra:

* [&queryType=full&search=business_title:"senior analyst"~1](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:%22senior%20analyst%22~1)

**Exemplo 5** -tente novamente remover palavras Olá entre termo hello "analista sênior".

* [&queryType=full&search=business_title:"senior analyst"~0](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:%22senior%20analyst%22~0)

## <a name="term-boosting-examples"></a>Exemplos de aumento de termo
Aumentando o termo se refere a tooranking um documento maior se ele contém Olá ampliada termo, toodocuments relativo que não contêm o termo de saudação. Isso é diferente dos perfis de pontuação, já que os perfis de pontuação aumentam determinados campos, em vez de termos específicos. Olá ajudam a ilustrar as diferenças de saudação do exemplo a seguir.

Considere a possibilidade de um perfil de pontuação aumenta faz a correspondência em um determinado campo, como **gênero** no exemplo de musicstoreindex hello. Aumentando o termo pode ser usado toofurther aumento determinados termos da pesquisa maior do que outras pessoas. Por exemplo, "rock ^ 2 eletrônicos" melhora a documentos que contêm termos de pesquisa de saudação na Olá **gênero** maior do que outros campos de pesquisa no índice de saudação do campo. Além disso, os documentos que contêm o termo de pesquisa hello "rock" serão classificados maior do que Olá outro termo de pesquisa "eletrônico" como resultado do valor de aumento de termo hello (2).

tooboost um termo, use Olá cursor, "^", símbolo com um fator de aumento (um número) no final de saudação do termo Olá você está pesquisando. Olá fator de aumento de saudação superior, hello termo de hello mais relevante será relativo tooother termos de pesquisa. Por padrão, o fator de aumento de saudação é 1. Embora o fator de aumento de saudação deve ser positivo, ele pode ser menor que 1 (por exemplo, 0.2).

**Exemplo 6** – consulta de saudação do botão direito do mouse. Pesquisar trabalhos com o termo hello "analista do computador" onde podemos ver nenhum resultado com o computador de palavras e analista ainda trabalhos de analista estão na parte superior da saudação de resultados de saudação.

* [&queryType=full&search=business_title:computer analyst](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:computer%5e2%20analyst)

**Exemplo 7** -tente novamente, esse aumento do tempo resultados com o computador de termo Olá sobre analista de termo Olá se ambas as palavras não existe.

* [&queryType=full&search=business_title:computer^2 analyst](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:computer%5e2%20analyst)

## <a name="regular-expression-example"></a>Exemplo de expressão regular
Uma pesquisa de expressão regular localiza uma correspondência com base no conteúdo de saudação entre barras "/", como saudação está documentada [classe RegExp](http://lucene.apache.org/core/4_10_2/core/org/apache/lucene/util/automaton/RegExp.html).

**Exemplo 8** – consulta de saudação do botão direito do mouse. Pesquisa de trabalhos com o termo Olá sênior ou júnior.

* `&queryType=full&$select=business_title&search=business_title:/(Sen|Jun)ior/`

Olá URL para este exemplo não será renderizado corretamente na página de saudação. Como alternativa, copie Olá URL abaixo e cole-o no endereço da URL do navegador hello:`http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26queryType=full%26$select=business_title%26search=business_title:/(Sen|Jun)ior/)`

## <a name="wildcard-search-example"></a>Exemplo de pesquisa de curinga
Você pode usar a sintaxe geralmente reconhecida para pesquisas com vários caracteres curinga (\*) ou um caractere curinga (?). Observe a consulta do Lucene Olá analisador dá suporte ao uso Olá desses símbolos com um único termo e não uma frase.

**Exemplo 9** – consulta de saudação do botão direito do mouse. Pesquisar trabalhos que contêm Olá prefixo 'programa' que inclui títulos de negócios com os termos de saudação de programação e programador nele.

* [&queryType=full&$select=business_title&search=business_title:prog*](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26queryType=full%26$select=business_title%26search=business_title:prog*)

Não é possível usar um símbolo * ou ? símbolo como primeiro caractere saudação de uma pesquisa.

## <a name="next-steps"></a>Próximas etapas
Tente especificar Olá Lucene analisador de consulta em seu código. Olá links a seguir explica como tooset a pesquisa de consulta para .NET e Olá API REST. links de Olá usam a sintaxe simples de padrão de saudação assim será necessário tooapply de saudação de toospecify neste artigo, você aprendeu **queryType**.

* [Consultar seu índice de pesquisa do Azure usando o SDK .NET de saudação](search-query-dotnet.md)
* [Consultar seu índice de pesquisa do Azure usando a API REST de saudação](search-query-rest-api.md)

## <a name="see-also"></a>Consulte também

 [Como funciona a pesquisa de texto completo no Azure Search](search-lucene-query-architecture.md)