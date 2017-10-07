---
title: "aaaHow tooimplement a navegação facetada na pesquisa do Azure | Microsoft Docs"
description: "Adicione a navegação facetada tooapplications que se integram a pesquisa do Azure, um serviço de pesquisa de nuvem hospedado no Microsoft Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: mblythe
editor: 
ms.assetid: cdf98fd4-63fd-4b50-b0b0-835cb08ad4d3
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 3/10/2017
ms.author: heidist
ms.openlocfilehash: c1e6bf9dc55d0044525db79e37d35a50ded5a736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimplement-faceted-navigation-in-azure-search"></a>Como a navegação facetada tooimplement na pesquisa do Azure
A navegação facetada é um mecanismo de filtragem que fornece navegação de busca detalhada autodirigida em aplicativos de pesquisa. termo de saudação 'Navegação facetada' pode não ser familiares, mas você provavelmente usou antes. Como Olá mostrado no exemplo a seguir, a navegação facetada é nada mais que Olá categorias usadas toofilter resultados.

 ![Demonstração de Portal de Trabalho do Azure Search][1]

A navegação facetada é um toosearch de ponto de entrada alternativa. Oferece um conveniente tootyping alternativo expressões complexas pesquisa manualmente. As facetas podem ajudar a encontrar o que você está procurando, garantindo que você não obterá zero resultados. Como desenvolvedor, facetas permitem que você exponha os critérios de pesquisa mais úteis Olá para navegar em seu corpo de pesquisa. Em aplicativos de varejo online, a navegação facetada geralmente é criada sobre marcas, departamentos (sapatos infantis), tamanho, preço, popularidade e classificações. 

A implementação da navegação facetada varia entre diferentes tecnologias de pesquisa. No Azure Search, a navegação facetada baseia-se no tempo da consulta, usando os campos atribuídos especificados anteriormente no seu esquema.

-   Em consultas de saudação que seu aplicativo cria, uma consulta deve enviar *parâmetros de consulta de faceta* conjunto de resultados de valores de filtro tooget Olá faceta disponíveis para esse documento.

-   tooactually trim Olá conjunto de resultados de documento, o aplicativo hello também deve aplicar um `$filter` expressão.

Desenvolvimento de seu aplicativo, escrevendo código que cria consultas constitui em massa de saudação do trabalho de saudação. Muitos dos comportamentos de aplicativo hello que você esperaria de navegação facetada são fornecidos pelo serviço hello, incluindo suporte interno para intervalos de definir e obter contagens de resultados da faceta. serviço Olá também inclui padrões sensíveis que ajudarão-lo a evitar estruturas de navegação complicada. 

## <a name="sample-code-and-demo"></a>Demonstração e código de exemplo
Este artigo usa um portal de pesquisa de trabalhos como um exemplo. exemplo Hello é implementado como um aplicativo ASP.NET MVC.

-   Ver e demonstração de trabalho do hello online de teste [demonstração de Portal de trabalho de pesquisa do Azure](http://azjobsdemo.azurewebsites.net/).

-   Baixar o código de saudação do hello [repositório de exemplos do Azure no GitHub](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs).

## <a name="get-started"></a>Introdução
Se você for novo desenvolvimento toosearch, Olá melhor maneira toothink de navegação facetada é que ela mostra as possibilidades de saudação de pesquisa alternativas. É um tipo de experiência de busca detalhada, com base em filtros predefinidos usados para restringir os resultados da pesquisa rapidamente por meio de ações de apontar e clicar. 

### <a name="interaction-model"></a>Modelo de interação

Olá a experiência de pesquisa para a navegação facetada é iterativa, então vamos começar com noções básicas sobre como uma sequência de consultas Desdobrar em ações de resposta de toouser.

Olá ponto de partida é uma página de aplicativo que fornece navegação facetada, normalmente colocada em periferia hello. A navegação facetada costuma ser uma estrutura de árvore, com caixas de seleção para cada valor ou texto que pode ser clicado. 

1. Uma consulta enviada tooAzure pesquisa especifica a estrutura de navegação facetada Olá por meio de um ou mais parâmetros de consulta de faceta. Por exemplo, Olá consulta inclua `facet=Rating`, talvez com um `:values` ou `:sort` toofurther opção refinar apresentação hello.
2. camada de apresentação Olá renderiza uma página de pesquisa que fornece navegação de faceta, usando as facetas Olá especificadas na solicitação de saudação.
3. Dada uma estrutura de navegação facetada que inclui a classificação, clique em "4" tooindicate que devem ser mostrados somente os produtos com uma classificação de 4 ou superior. 
4. Em resposta, o aplicativo hello envia uma consulta que inclui`$filter=Rating ge 4` 
5. página Olá apresentação camada atualizações hello, mostrando um conjunto de resultados menor, que contém apenas os itens que atendam aos critérios de novo hello (nesse caso, os produtos classificados como 4 e superior).

Uma faceta é um parâmetro de consulta, mas não a confunda com uma entrada de consulta. Ela nunca é usada como critério de seleção em uma consulta. Em vez disso, considere parâmetros de consulta de faceta como estrutura de navegação de toohello entradas que vem em resposta hello. Para cada parâmetro de consulta de faceta que você fornecer, pesquisa do Azure avalia quantos documentos estão no resultados parciais de saudação para cada valor da faceta.

Saudação de aviso `$filter` na etapa 4. filtro de saudação é um aspecto importante da navegação facetada. Embora facetas e filtros são independentes no hello API, você precisa de ambos os experiência de saudação toodeliver você pretendia. 

### <a name="app-design-pattern"></a>Padrão de design do aplicativo

No código do aplicativo, padrão Olá é toouse faceta consulta parâmetros tooreturn Olá navegação facetada estrutura junto com os resultados da faceta, além de uma expressão de $filter.  Olá Olá de identificadores de expressão de filtro de evento no valor da faceta Olá de clique. Pense Olá `$filter` expressão como código Olá corte real Olá dos resultados da pesquisa retornados toohello camada de apresentação. Dada uma faceta de cores, clicando em Olá cor vermelha é implementado através de um `$filter` expressão que seleciona somente os itens que têm uma cor vermelha. 

### <a name="query-basics"></a>Noções básicas sobre consulta

Na pesquisa do Azure, uma solicitação é especificada por meio de um ou mais parâmetros de consulta (consulte [Procurar documentos](http://msdn.microsoft.com/library/azure/dn798927.aspx) para obter uma descrição de cada um deles). Nenhum dos parâmetros de consulta Olá são necessárias, mas você deve ter pelo menos uma na ordem para um toobe de consulta válida.

Precisão, entendido como hello capacidade toofilter out acertos irrelevantes, é obtida por meio de uma ou ambas essas expressões:

-   **search=**  
    valor desse parâmetro Hello constitui a expressão de pesquisa de saudação. Pode ser uma única parte de texto ou uma expressão de pesquisa complexa que inclua vários termos e operadores. No servidor de saudação, uma expressão de pesquisa é usada para pesquisa de texto completo, consultar campos de pesquisa no índice de saudação para correspondência de termos, retornando resultados em ordem de classificação. Se você definir `search` toonull, a execução da consulta está sobre o índice inteiro da saudação (ou seja, `search=*`). In this case, outros elementos de saudação de consulta, tais como um `$filter` ou perfil de pontuação, Olá principais fatores que afetam quais documentos são retornados `($filter`) e em qual ordem (`scoringProfile` ou `$orderby`).

-   **$filter=**  
    Um filtro é um mecanismo eficiente para limitar o tamanho de saudação dos resultados da pesquisa com base nos valores de saudação de atributos de documento específico. Um `$filter` é avaliado primeiro, seguido pela lógica de facetas que gera valores disponíveis hello e contagens correspondentes para cada valor

Expressões de pesquisa complexa diminuir o desempenho de saudação de consulta de saudação. Sempre que possível, use a precisão de tooincrease de expressões de filtro bem construído e melhorar o desempenho da consulta.

toobetter entender como um filtro adiciona mais precisão, comparar uma tooone de expressão de pesquisa complexa que inclui uma expressão de filtro:

-   `GET /indexes/hotel/docs?search=lodging budget +Seattle –motel +parking`
-   `GET /indexes/hotel/docs?search=lodging&$filter=City eq ‘Seattle’ and Parking and Type ne ‘motel’`

Ambas as consultas são válidas, mas Olá segundo é superior se você está procurando não motéis com estacionamento em Seattle.
-   primeira consulta de saudação depende dessas palavras específicas está sendo mencionado ou não mencionadas nos campos de cadeia de caracteres como nome, descrição e qualquer outro campo que contém dados pesquisáveis.
-   consulta segundo Olá procura correspondências precisas em dados estruturados e é provável toobe muito mais preciso.

Em aplicativos que incluam navegação facetada, garanta que cada ação do usuário em uma estrutura de navegação facetada seja acompanhada de uma redução dos resultados da pesquisa. toonarrow resultados, use uma expressão de filtro.

<a name="howtobuildit"></a>

## <a name="build-a-faceted-navigation-app"></a>Criar um aplicativo de navegação facetada
Você implementar a navegação facetada à pesquisa do Azure no seu código de aplicativo que cria a solicitação de pesquisa de saudação. a navegação facetada Olá depende de elementos no esquema que você definiu anteriormente.

Predefinidas no seu índice de pesquisa é hello `Facetable [true|false]` atributo de índice, definido em campos selecionados tooenable ou desabilitar seu uso em uma estrutura de navegação facetada. Sem `"Facetable" = true`, um campo não pode ser usado na navegação facetada.

camada de apresentação de saudação em seu código fornece a experiência do usuário hello. Essa lista deve partes constituintes de saudação de navegação facetada Olá, como rótulo hello, valores, caixas de seleção e contagem de saudação. Olá API de REST de pesquisa do Azure é independente de plataforma, portanto, use qualquer idioma e a plataforma desejada. Olá importante é tooinclude elementos de interface do usuário que oferecem suporte a incremental refresh, com o estado da interface do usuário atualizado como cada faceta adicional está selecionada. 

No momento da consulta, o código do aplicativo cria uma solicitação que inclui `facet=[string]`, um parâmetro de solicitação que fornece Olá campo toofacet por. Uma consulta pode ter múltiplas facetas, como `&facet=color&facet=category&facet=rating`, cada uma separada por um caractere “e” comercial (&).

Código do aplicativo também deve construir uma `$filter` saudação do expressão toohandle clique em eventos na navegação facetada. Um `$filter` reduz os resultados da pesquisa hello, usando o valor da faceta hello como critérios de filtro.

A pesquisa do Azure retorna resultados hello, com base em um ou mais termos que você inserir, juntamente com a estrutura de navegação facetada toohello atualizações. Na Pesquisa do Azure, a navegação facetada é uma construção de nível único, com valores de facetas e contagens de quantos resultados são encontrados para cada uma delas.

Na Olá seções a seguir, vamos dar uma Visão aprofundada de como toobuild cada parte.

<a name="buildindex"></a>

## <a name="build-hello-index"></a>Criar índice Olá
Facetas está habilitada em uma base por um campo no índice hello, por meio desse atributo de índice: `"Facetable": true`.  
Todos os tipos de campo que poderiam ser usados na navegação facetada são `Facetable` por padrão. Esses tipos de campo incluem `Edm.String`, `Edm.DateTimeOffset`, e todos os tipos de campo numérico de hello (essencialmente, todos os tipos de campo são facetable exceto `Edm.GeographyPoint`, que não pode ser usado na navegação facetada). 

Ao criar um índice, uma prática recomendada para a navegação facetada é tooexplicitly ativar facetas desativado para os campos que nunca devem ser usados como uma faceta.  Em particular, os campos de cadeia de caracteres para valores de singleton, como um ID ou nome do produto, devem ser definidos muito`"Facetable": false` tooprevent seus acidental (e ineficazes) usar na navegação facetada. Facetas onde você não começa a ativação ajuda a manter o tamanho de saudação do índice de saudação pequeno e normalmente melhora o desempenho.

A seguir faz parte do esquema de Olá para o aplicativo de exemplo de demonstração do Portal de trabalho hello, cortado de tamanho de saudação de tooreduce alguns atributos:

```json
{
  ...
  "name": "nycjobs",
  "fields": [
    { “name”: "id",                 "type": "Edm.String",              "searchable": false, "filterable": false, ... "facetable": false, ... },
    { “name”: "job_id",             "type": "Edm.String",              "searchable": false, "filterable": false, ... "facetable": false, ... },
    { “name”: "agency",              "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "posting_type",        "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "num_of_positions",    "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "business_title",      "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "civil_service_title", "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "title_code_no",       "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "level",               "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_range_from",   "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_range_to",     "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_frequency",    "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "work_location",       "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
…
    { “name”: "geo_location",        "type": "Edm.GeographyPoint",     "searchable": false, "filterable": true, ...  "facetable": false, ... },
    { “name”: "tags",                "type": "Collection(Edm.String)", "searchable": true,  "filterable": true, ...  "facetable": true, ...  }
  ],
…
}
```

Como você pode ver no esquema de exemplo hello, `Facetable` está desativado para os campos de cadeia de caracteres que não devem ser usados como facetas, como valores de ID. Facetas onde você não começa a ativação ajuda a manter o tamanho de saudação do índice de saudação pequeno e normalmente melhora o desempenho.

> [!TIP]
> Como uma prática recomendada, incluem o conjunto completo de saudação de atributos de índice para cada campo. Embora `Facetable` é ativado por padrão para quase todos os campos, propositadamente definindo cada atributo pode ajudá-lo a considerar as implicações de saudação de cada decisão de esquema. 

<a name="checkdata"></a>

## <a name="check-hello-data"></a>Verificar dados Olá
qualidade de saudação de dados tem um efeito direto sobre se a estrutura de navegação facetada Olá materializa conforme o esperado. Isso também afeta a facilidade de saudação de construção de conjunto de resultados de saudação de tooreduce filtros.

Se você quiser toofacet por marca ou preço, cada documento deve conter valores para *nome da marca* e *ProductPrice* que são válidos, consistente e produtiva como uma opção de filtro.

Aqui estão alguns lembretes de quais tooscrub para:

* Para cada campo que você deseja toofacet por, pergunte-se se ele contém valores que são adequados como filtros na pesquisa direcionada automaticamente. valores Hello devem ser suficientemente diferente curto e descritivo toooffer uma opção entre as opções concorrentes.
* Erros de ortografia ou valores quase correspondentes. Se você faceta na cor e valores de campo incluem laranja e Ornage (erro), uma faceta com base no campo de cor Olá escolheria a ambos.
* Texto composto
de caracteres maiúsculos e minúsculos também pode causar estragos na navegação facetada, com laranja e Laranja aparecendo como dois valores diferentes. 
* Versões de único e plurais de Olá mesmo valor pode resultar em uma faceta separada para cada.

Como você pode imaginar, auditoria na preparação de dados de saudação é um aspecto essencial de navegação facetada efetivo.

<a name="presentationlayer"></a>

## <a name="build-hello-ui"></a>Criar hello da interface do usuário
Trabalhando da camada de apresentação Olá pode ajuda a descobrir os requisitos que poderá ser perdidos, caso contrário e entender quais recursos estão toohello essencial experiência de pesquisa.

Em termos de faceta de navegação, sua página da web ou aplicativo exibe a estrutura de navegação facetada hello, detecta a entrada do usuário na página hello e insere elementos Olá alterado. 

Para aplicativos web, AJAX normalmente é usado na camada de apresentação Olá porque permite alterações incrementais toorefresh. Você também pode usar o ASP.NET MVC ou qualquer outra plataforma de visualização que tooan o serviço de pesquisa do Azure pode se conectar por HTTP. aplicativo de exemplo Hello referenciado neste artigo - Olá **demonstração de Portal de trabalho de pesquisa do Azure** – acontece toobe um aplicativo ASP.NET MVC.

No exemplo hello, navegação facetada é embutida no hello página resultados da pesquisa. Olá seguinte exemplo, retirado de saudação `index.cshtml` página de resultados do arquivo do aplicativo de exemplo hello, mostra Olá HTML estrutura estática para exibir a navegação facetada na pesquisa de saudação. lista de saudação facetas é criada ou reconstruída dinamicamente quando você enviar um termo de pesquisa, ou marcar ou desmarcar uma faceta.

```html
<div class="widget sidebar-widget jobs-filter-widget">
  <h5 class="widget-title">Filter Results</h5>
    <p id="filterReset"></p>
    <div class="widget-content">

      <h6 id="businessTitleFacetTitle">Business Title</h6>
      <ul class="filter-list" id="business_title_facets">
      </ul>

      <h6>Location</h6>
      <ul class="filter-list" id="posting_type_facets">
      </ul>

      <h6>Posting Type</h6>
      <ul class="filter-list" id="posting_type_facets"></ul>

      <h6>Minimum Salary</h6>
      <ul class="filter-list" id="salary_range_facets">
      </ul>

  </div>
</div>
```

Olá seguinte trecho de código do hello `index.cshtml` página cria dinamicamente a faceta de primeiro de saudação de toodisplay do hello HTML, cargo. Funções semelhantes criar dinamicamente hello HTML para Olá outras facetas. Cada faceta tem um rótulo e uma contagem, que exibe o número de saudação de itens encontrados para o resultado dessa faceta.

```js
function UpdateBusinessTitleFacets(data) {
  var facetResultsHTML = '';
  for (var i = 0; i < data.length; i++) {
    facetResultsHTML += '<li><a href="javascript:void(0)" onclick="ChooseBusinessTitleFacet(\'' + data[i].Value + '\');">' + data[i].Value + ' (' + data[i].Count + ')</span></a></li>';
  }

  $("#business_title_facets").html(facetResultsHTML);
}
```

> [!TIP]
> Quando você criar a página de resultados da pesquisa de saudação, lembre-se tooadd um mecanismo para limpar facetas. Se você adicionar caixas de seleção, você pode ver facilmente como os filtros de tooclear hello. Para outros layouts, talvez seja necessário um padrão de navegação estrutural ou outra abordagem criativa. Por exemplo, em Olá aplicativo de exemplo do Portal de pesquisa de trabalho, você pode clicar Olá `[X]` após uma faceta de saudação tooclear faceta selecionada.

<a name="buildquery"></a>

## <a name="build-hello-query"></a>Criar consulta de saudação
código de saudação que você escreve para a criação de consultas deve especificar todas as partes de uma consulta válida, incluindo expressões de pesquisa, facetas e filtros, pontuação perfis – nada usadas tooformulate uma solicitação. Nesta seção, exploraremos onde facetas cabem em uma consulta, e como os filtros são usados com facetas toodeliver um menor conjunto de resultados.

Observe que as facetas são integrais nesse aplicativo de exemplo. Olá a experiência de pesquisa no hello demonstração do Portal de trabalho é criada em filtros e navegação facetada. posicionamento de saudação proeminentes de navegação facetada na página de saudação demonstra sua importância. 

Um exemplo geralmente é um bom lugar toobegin. Olá seguinte exemplo, retirado de saudação `JobsSearch.cs` arquivo, compilações que uma solicitação que cria a navegação de faceta com base no cargo, local, o tipo de lançamento e salário mínimo. 

```cs
SearchParameters sp = new SearchParameters()
{
  ...
  // Add facets
  Facets = new List<String>() { "business_title", "posting_type", "level", "salary_range_from,interval:50000" },
};
```

Um parâmetro de consulta de faceta é definir o campo tooa e dependendo do tipo de dados hello, podem ser parametrizado adicional por lista delimitada por vírgulas que inclui `count:<integer>`, `sort:<>`, `interval:<integer>`, e `values:<list>`. Há suporte para dados numéricos em uma lista de valores ao configurar intervalos. Consulte [Pesquisar documentos (API da Pesquisa do Azure)](http://msdn.microsoft.com/library/azure/dn798927.aspx) para obter detalhes de utilização.

Juntamente com as facetas, solicitação Olá formulada pelo seu aplicativo também deve criar filtros toonarrow para baixo do conjunto de saudação de documentos de candidato com base em uma seleção de valor da faceta. Para um repositório de bicicleta, navegação facetada fornece dicas tooquestions como *que cores, os fabricantes e os tipos de bicicletas estão disponíveis?*. A filtragem de respostas a perguntas como *Quais bicicletas exatamente são vermelhas, mountain bikes e estão neste intervalo de preços?*. Quando você clicar em "Vermelho" tooindicate que devem ser mostrados somente os produtos vermelhos, Olá próxima consulta Olá aplicativo envia os inclui `$filter=Color eq ‘Red’`.

Olá seguinte trecho de código do hello `JobsSearch.cs` página adiciona Olá selecionado cargo toohello filtro se você selecionar um valor de faceta de cargo hello.

```cs
if (businessTitleFacet != "")
  filter = "business_title eq '" + businessTitleFacet + "'";
```

<a name="tips"></a> 

## <a name="tips-and-best-practices"></a>Dicas e melhores práticas

### <a name="indexing-tips"></a>Dicas de indexação
**Melhorar a eficiência de índice se você não usar uma caixa de Pesquisa**

Se seu aplicativo usa a navegação facetada exclusivamente (ou seja, nenhuma caixa de pesquisa), você pode marcar um campo hello como `searchable=false`, `facetable=true` tooproduce um índice mais compacto. Além disso, a indexação ocorre somente em valores de inteiro de faceta, com nenhuma quebra de palavras ou indexação de partes do componente de saudação de um valor de várias palavra.

**Definir quais campos podem ser usados como facetas**

Lembre-se de que Olá esquema de índice Olá determina quais campos são toouse disponível como uma faceta. Supondo que um campo facetable, consulta Olá Especifica quais toofacet campos por. campo de saudação pelo qual você está facetas fornece valores hello aparecem abaixo do rótulo de saudação. 

valores de saudação que aparecem em cada rótulo são recuperados do índice de saudação. Por exemplo, se hello faceta campo é *cor*, Olá valores disponíveis para filtragem adicional são os valores de saudação para esse campo - vermelho, preto e assim por diante.

Para valores numéricos e de data e hora somente, você pode definir explicitamente os valores no campo de faceta hello (por exemplo, `facet=Rating,values:1|2|3|4|5`). Uma lista de valores é permitida para esses campos tipos toosimplify Olá separação dos resultados da faceta em intervalos de contíguas (qualquer um dos intervalos com base em valores numéricos ou períodos de tempo). 

**Por padrão, você só pode ter um nível de navegação facetada** 

Como observado, não há nenhum suporte direto para aninhamento de facetas em uma hierarquia. Por padrão, a navegação facetada no Azure Search dá suporte a apenas um nível de filtros. No entanto, existem soluções alternativas. Você pode codificar uma estrutura hierárquica de facetas em um `Collection(Edm.String)` com um ponto de entrada por hierarquia. Implementação dessa solução alternativa é além do escopo deste artigo hello. 

### <a name="querying-tips"></a>Dicas de consulta
**Validar campos**

Se você criar lista de saudação de facetas dinamicamente com base na entrada do usuário não confiável, valide que Olá nomes de campos de faceta Olá são válidos. Ou, retire nomes Olá ao criar URLs usando `Uri.EscapeDataString()` em .NET ou Olá equivalente em sua plataforma de escolha.

### <a name="filtering-tips"></a>Dicas de filtragem
**Aumentar a precisão da pesquisa com filtros**

Utilize filtros. Se você confiar em expressões de pesquisa apenas sozinha, lematização pode fazer com que um documento toobe retornado que não tem o valor da faceta precisão hello em qualquer um de seus campos.

**Aumentar o desempenho da pesquisa com filtros**

Os filtros restringem o conjunto de saudação de documentos de candidato para pesquisa e excluí-los da classificação. Se você tiver um grande conjunto de documentos, usar uma busca detalhada de faceta seletiva geralmente proporciona melhor desempenho.
  
**Filtrar apenas campos de faceta Olá**

No Facetado drill-down, você normalmente deseja tooonly incluem documentos que têm o valor da faceta Olá em um campo específico (Facetado), não em qualquer lugar em todos os campos pesquisáveis. Adicionar um filtro reforça o campo de destino Olá direcionando Olá serviço toosearch somente no campo de faceta Olá para um valor correspondente.

**Recortar resultados da faceta com mais filtros**

Resultados da faceta são documentos encontrados nos resultados da pesquisa Olá que correspondem a um termo da faceta. Em Olá seguinte exemplo, nos resultados da pesquisa para *de computação em nuvem*, 254 itens também possuem *especificação interna* como um tipo de conteúdo. Os itens não são necessariamente mutuamente exclusivos. Se um item atende aos critérios de saudação de ambos os filtros, ele será contado em cada uma. Essa duplicação é possível quando facetas em `Collection(Edm.String)` tooimplement documento marcação os campos, que geralmente são usados.

        Search term: "cloud computing"
        Content type
           Internal specification (254)
           Video (10) 

Em geral, se você descobrir que resultados da faceta consistentemente são muito grandes, recomendamos que você adicione mais filtros toogive usuários mais opções para restringir a pesquisa de saudação.

### <a name="tips-about-result-count"></a>Dicas sobre contagem de resultados

**Olá limitar o número de itens na navegação de faceta Olá**

Para cada campo Facetado na árvore de navegação hello, há um limite padrão de 10 valores. Esse padrão faz sentido para estruturas de navegação porque ele mantém valores hello tamanho gerenciável tooa na lista. Você pode substituir o padrão de saudação atribuindo um valor toocount.

* `&facet=city,count:5`Especifica que somente Olá cinco primeiras cidades encontradas na parte superior de saudação classificado os resultados são retornadas como um resultado da faceta. Considere um exemplo de consulta com um termo de pesquisa "aeroporto" e 32 correspondências. Se a consulta de saudação especifica `&facet=city,count:5`somente Olá primeiro cinco exclusivo cidades com hello a maioria dos documentos nos resultados da pesquisa Olá são incluídos no hello resultados da faceta.

Distinção de saudação do aviso entre os resultados da pesquisa e os resultados de faceta. Resultados da pesquisa são todos os documentos de saudação que corresponde à consulta de saudação. Resultados da faceta são Olá correspondências para cada valor da faceta. No exemplo hello, resultados da pesquisa incluem nomes de cidades que não estão na lista de classificação de faceta hello (5 em nosso exemplo). Os resultados que são filtrados por meio de navegação facetada se tornam visíveis quando você limpa facetas ou escolhe outras facetas além de Cidade. 

> [!NOTE]
> Discutir `count` quando há mais de um tipo pode ser confuso. Olá tabela a seguir oferece um resumo de como o termo Olá é usado na API de pesquisa do Azure, o código de exemplo e documentação. 

* `@colorFacet.count`<br/>
  Código de apresentação, você verá um parâmetro de contagem na faceta hello, toodisplay usado Olá número de resultados da faceta. Nos resultados da faceta, contagem indica o número Olá de documentos que correspondem em termos de faceta de saudação ou intervalo.
* `&facet=City,count:12`<br/>
  Em uma consulta de faceta, você pode definir o valor da contagem de tooa.  saudação padrão é 10, mas você pode defini-lo superior ou inferior. Configuração `count:12` obtém Olá primeiras 12 correspondências nos resultados da faceta por contagem de documentos.
* "`@odata.count`"<br/>
  Na resposta de consulta hello, esse valor indica número de saudação de itens correspondentes nos resultados da pesquisa hello. Em média, é maior do que a soma de saudação de todos os resultados da faceta combinados devido toohello presença de itens que correspondem Olá termo de pesquisa, mas sem correspondência de valor da faceta.

**Obter contagens dos resultados da faceta**

Quando você adicionar uma consulta de faceta tooa filtro, convém declaração de faceta Olá tooretain (por exemplo, `facet=Rating&$filter=Rating ge 4`). Tecnicamente, a faceta = classificação não é necessária, mas mantê-lo retorna contagens de saudação de valores de faceta para classificações 4 e superior. Por exemplo, se você clicar em "4" e Olá consulta inclui um filtro para o maior ou igual muito "4", contagens são retornadas para cada classificação é 4 e superior.  

**Certifique-se de obter contagens de facetas precisas**

Em determinadas circunstâncias, você pode achar que as contagens de faceta não coincidem Olá conjuntos de resultados (consulte [navegação facetada na pesquisa do Azure (postagem no fórum)](https://social.msdn.microsoft.com/Forums/azure/06461173-ea26-4e6a-9545-fbbd7ee61c8f/faceting-on-azure-search?forum=azuresearch)).

As contagens de faceta podem ser imprecisas devido toohello arquitetura de fragmentação. Cada índice de pesquisa tem vários fragmentos, e cada fragmento relatórios facetas de N maiores Olá por contagem de documentos, que é, em seguida, combinada em um único resultado. Se alguns fragmentos têm muitos valores correspondentes, enquanto outros têm menos, você pode achar que alguns valores de faceta estão ausentes ou em contado nos resultados da saudação.

Embora esse comportamento pode mudar a qualquer momento, se você encontrar esse comportamento hoje, você pode contornar ele artificialmente aumentando a contagem de saudação:<number> tooa grande número tooenforce total de relatórios a partir de cada fragmento. Se Olá valor de contagem: é maior que ou igual toohello número de valores exclusivos no campo hello, você terá garantia resultados precisos. No entanto, quando as contagens de documento são altas há uma penalidade de desempenho, portanto, use essa opção criteriosamente.

### <a name="user-interface-tips"></a>Dicas da interface do usuário
**Adicionar rótulos para cada campo na navegação facetada**

Rótulos são normalmente definidos no hello HTML ou no formato (`index.cshtml` no aplicativo de exemplo hello). Não há API no Azure Search para rótulos de navegação facetada ou qualquer outro metadado.

<a name="rangefacets"></a>

## <a name="filter-based-on-a-range"></a>Filtrar com base em um intervalo
A facetagem em intervalos de valores é um requisito comum de aplicativo de pesquisa. Intervalos têm suporte para dados numéricos e valores de DataHora. Você pode ler mais sobre cada abordagem em [Procurar documentos (API da Pesquisa do Azure)](http://msdn.microsoft.com/library/azure/dn798927.aspx).

A Pesquisa do Azure simplifica a construção do intervalo, fornecendo duas abordagens para a computação de um intervalo. Para ambas as abordagens, pesquisa do Azure cria Olá Olá entrados que você forneceu os intervalos adequados. Por exemplo, se você especificar valores de intervalo de 10|20|30, ele criará automaticamente intervalos de 0-10, 10-20, 20-30 -10, 10-20 e 20-30. Seu aplicativo pode, opcionalmente, remover quaisquer intervalos que estejam vazios. 

**Método 1: Usar o parâmetro de intervalo de saudação**  
facetas de preço tooset em incrementos de US $10, você deve especificar:`&facet=price,interval:10`

**Abordagem 2: usar uma lista de valores**  
Para dados numéricos, você pode usar uma lista de valores.  Considere o intervalo de faceta Olá para um `listPrice` campo, renderizado da seguinte maneira:

  ![Lista de valores de exemplo][5]

toospecify, como um intervalo de faceta Olá um Olá anterior a captura de tela, use uma lista de valores:

    facet=listPrice,values:10|25|100|500|1000|2500

Cada intervalo é criado usando 0 como ponto de partida, um valor da lista de saudação como um ponto de extremidade e, em seguida, são cortados de saudação anterior toocreate discretos intervalos. O Azure Search faz essas coisas como parte da navegação facetada. Você não tem código toowrite para estruturar a cada intervalo.

### <a name="build-a-filter-for-a-range"></a>Criar um filtro para um intervalo
documentos de toofilter com base em um intervalo que você selecionar, você pode usar o hello `"ge"` e `"lt"` operadores em uma expressão de duas partes que define os pontos de extremidade de saudação do intervalo de saudação de filtro. Por exemplo, se você escolher Olá intervalo de 10 a 25 para um `listPrice` campo, o filtro de saudação seria `$filter=listPrice ge 10 and listPrice lt 25`. No código de exemplo hello, expressão de filtro Olá usa **priceFrom** e **priceTo** parâmetros tooset Olá os pontos de extremidade. 

  ![Consultar um intervalo de valores][6]

<a name="geofacets"></a> 

## <a name="filter-based-on-distance"></a>Filtrar com base na distância
É comum toosee filtros que ajudam você a escolher uma loja, restaurante ou destino com base em seu local atual do tooyour de proximidade. Embora esse tipo de filtro possa parecer com a navegação facetada, trata-se apenas de um filtro. Mencionamos isso aqui para aqueles que estão procurando especificamente conselhos de implementação para um problema de design específico.

Há duas funções geoespaciais no Azure Search, **geo.distance** e **geo.intersects**.

* Olá **Geo** função retorna a distância de saudação em quilômetros entre dois pontos. Um ponto é um campo e a outra é uma constante passada como parte do filtro de saudação. 
* Olá **geo.intersects** função retornará true se um determinado ponto estiver dentro de um polígono determinado. Olá ponto é um campo e polígono Olá é especificado como uma lista de constante de coordenadas passada como parte do filtro de saudação.

Você pode encontrar exemplos de filtros em [Sintaxe de expressão OData (Pesquisa do Azure)](http://msdn.microsoft.com/library/azure/dn798921.aspx).

<a name="tryitout"></a>

## <a name="try-hello-demo"></a>Experimente Olá demonstração
Olá demonstração de Portal de trabalho de pesquisa do Azure contém exemplos de saudação mencionados neste artigo.

-   Ver e demonstração de trabalho do hello online de teste [demonstração de Portal de trabalho de pesquisa do Azure](http://azjobsdemo.azurewebsites.net/).

-   Baixar o código de saudação do hello [repositório de exemplos do Azure no GitHub](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs).

Como trabalhar com os resultados da pesquisa, assista a URL Olá para alterações na construção de consulta. Este aplicativo acontece tooappend facetas toohello URI que você selecionar cada um.

1. funcionalidade de mapeamento de saudação toouse do aplicativo de demonstração de Olá, obter uma chave do Bing Maps do hello [Centro de desenvolvimento do Bing Maps](https://www.bingmapsportal.com/). Cole-a chave existente Olá no hello `index.cshtml` página. Olá `BingApiKey` definindo no hello `Web.config` arquivo não é usado. 

2. Execute o aplicativo hello. Faça tour opcional hello, ou ignorar a caixa de diálogo de saudação.
   
3. Insira um termo de pesquisa, como "analista" e clique no ícone de pesquisa hello. Olá consulta é executada rapidamente.
   
   Uma estrutura de navegação facetada também é retornada com os resultados da pesquisa hello. Na página de resultados de pesquisa hello, estrutura de navegação facetada Olá inclui contagens de cada resultado da faceta. Nenhuma faceta está selecionada, todos os resultados correspondentes são retornados.
   
   ![Resultados da pesquisa antes de selecionar facetas][11]

4. Clique em um Cargo, Local ou Salário Mínimo. Facetas eram nulas na pesquisa inicial hello, mas que levem em valores, os resultados da pesquisa Olá são cortados de itens que não correspondem.
   
   ![Resultados da pesquisa após a seleção de facetas][12]

5. consulta de faceta tooclear Olá para que você possa tentar comportamentos de consulta diferentes, clique em Olá `[X]` depois Olá selecionado facetas de saudação tooclear facetas.
   
<a name="nextstep"></a>

## <a name="learn-more"></a>Saiba mais
Assista [Aprofundamento no Azure Search](http://channel9.msdn.com/Events/TechEd/Europe/2014/DBI-B410). 45:25, não há uma demonstração sobre como tooimplement facetas.

Para mais informações sobre os princípios de design para a navegação facetada, recomendamos Olá links a seguir:

* [Design para pesquisa facetada](http://www.uie.com/articles/faceted_search/)
* [Padrões de design: navegação facetada](http://alistapart.com/article/design-patterns-faceted-navigation)


<!--Anchors-->
[How toobuild it]: #howtobuildit
[Build hello presentation layer]: #presentationlayer
[Build hello index]: #buildindex
[Check for data quality]: #checkdata
[Build hello query]: #buildquery
[Tips on how toocontrol faceted navigation]: #tips
[Faceted navigation based on range values]: #rangefacets
[Faceted navigation based on GeoPoints]: #geofacets
[Try it out]: #tryitout

<!--Image references-->
[1]: ./media/search-faceted-navigation/azure-search-faceting-example.PNG
[2]: ./media/search-faceted-navigation/Facet-2-CSHTML.PNG
[3]: ./media/search-faceted-navigation/Facet-3-schema.PNG
[4]: ./media/search-faceted-navigation/Facet-4-SearchMethod.PNG
[5]: ./media/search-faceted-navigation/Facet-5-Prices.PNG
[6]: ./media/search-faceted-navigation/Facet-6-buildfilter.PNG
[7]: ./media/search-faceted-navigation/Facet-7-appstart.png
[8]: ./media/search-faceted-navigation/Facet-8-appbike.png
[9]: ./media/search-faceted-navigation/Facet-9-appbikefaceted.png
[10]: ./media/search-faceted-navigation/Facet-10-appTitle.png
[11]: ./media/search-faceted-navigation/faceted-search-before-facets.png
[12]: ./media/search-faceted-navigation/faceted-search-after-facets.png

<!--Link references-->
[Designing for Faceted Search]: http://www.uie.com/articles/faceted_search/
[Design Patterns: Faceted Navigation]: http://alistapart.com/article/design-patterns-faceted-navigation
[Create your first application]: search-create-first-solution.md
[OData expression syntax (Azure Search)]: http://msdn.microsoft.com/library/azure/dn798921.aspx
[Azure Search Adventure Works Demo]: https://azuresearchadventureworksdemo.codeplex.com/
[http://www.odata.org/documentation/odata-version-2-0/overview/]: http://www.odata.org/documentation/odata-version-2-0/overview/ 
[Faceting on Azure Search forum post]: ../faceting-on-azure-search.md?forum=azuresearch
[Search Documents (Azure Search API)]: http://msdn.microsoft.com/library/azure/dn798927.aspx

