---
title: "perfis de aaaScoring (Azure pesquisa REST API Versão 2015-02-28-visualização) | Microsoft Docs"
description: "A Pesquisa do Azure é um serviço de pesquisa de nuvem hospedado que dá suporte ao ajuste de resultados classificados com base em perfis de pontuação definidos pelo usuário."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
ms.assetid: bfd62649-13d7-40b3-a8fa-85521a15084d
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.author: heidist
ms.date: 10/27/2016
ms.openlocfilehash: 17f83fdf6818dc6ffcc3e04f5d0185c6f646b63d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scoring-profiles-azure-search-rest-api-version-2015-02-28-preview"></a>Perfis de pontuação (API REST do Azure Search Versão 2015-02-28-Preview)
> [!NOTE]
> Este artigo descreve os perfis de pontuação Olá [2015-02-28-visualização](search-api-2015-02-28-preview.md). Atualmente não há nenhuma diferença entre hello `2016-09-01` versão documentado em [MSDN](http://msdn.microsoft.com/library/azure/mt183328.aspx) e hello `2015-02-28-Preview` versão descritas aqui, mas oferecemos neste documento assim mesmo na cobertura de documento tooprovide ordem entre Olá toda a API.
>
>

## <a name="overview"></a>Visão geral
Pontuação refere-se a computação toohello de uma pontuação de pesquisa para cada item retornado nos resultados da pesquisa. pontuação de saudação é um indicador de relevância de um item no contexto de saudação da operação de pesquisa atual hello. Olá pontuação mais alta de hello, Olá mais relevantes do item de saudação. Nos resultados da pesquisa, os itens são ordenados de alta toolow, com base em Olá pontuação de pesquisa calculadas para cada item.

Pesquisa do Azure usa a pontuação toocompute uma pontuação inicial padrão, mas você pode personalizar o cálculo de saudação por meio de um perfil de pontuação. Perfis de pontuação oferecem maior controle sobre a classificação de saudação de itens nos resultados da pesquisa. Por exemplo, você pode deseja tooboost itens com base em seu potencial de receita, promover itens mais recentes ou talvez aumentar os itens no inventário muito longo.

Um perfil de pontuação é parte da definição de índice hello, composta de campos, funções e parâmetros.

toogive você uma ideia do que um perfil de pontuação parece, hello, exemplo a seguir mostra um perfil simples chamado "geo". Ele aumenta os itens que têm o termo de pesquisa de saudação em Olá `hotelName` campo. Ele também usa Olá `distance` toofavor itens que estão dentro de dez quilômetros do local atual da saudação de função. Se alguém procura no termo hello "inn" e "inn" fizer parte de toobe do nome do hotel Olá, documentos que incluem hotéis com "inn" aparecerá mais nos resultados da pesquisa hello.

    "scoringProfiles": [
      {
        "name": "geo",
        "text": {
          "weights": { "hotelName": 5 }
        },
        "functions": [
          {
            "type": "distance",
            "boost": 5,
            "fieldName": "location",
            "interpolation": "logarithmic",
            "distance": {
              "referencePointParameter": "currentLocation",
              "boostingDistance": 10
            }
          }
        ]
      }
    ]

toouse que este perfil de pontuação, a consulta é formulada toospecify perfil de saudação na cadeia de caracteres de consulta de saudação. Na consulta Olá abaixo, observe o parâmetro de consulta hello, `scoringProfile=geo` na solicitação de saudação.

    GET /indexes/hotels/docs?search=inn&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&api-version=2015-02-28-Preview

Essa consulta pesquisa termo hello "inn" e passa no local atual da saudação. Observe que essa consulta inclui outros parâmetros, como `scoringParameter`. Os parâmetros de consulta são descritos em [Pesquisar documentos (API do Azure Search)](search-api-2015-02-28-preview.md#SearchDocs).

Clique em [exemplo](#example) tooreview um exemplo mais detalhado de um perfil de pontuação.

## <a name="what-is-default-scoring"></a>O que é a pontuação padrão?
A pontuação calcula um resultado de pesquisa para cada item em um conjunto de resultados ordenados por classificação. Cada item em um conjunto de resultados de pesquisa é atribuído a uma pontuação de pesquisa e classificação mais alta toolowest. Itens com pontuações mais altas de saudação são retornados toohello aplicativo. Por padrão, hello 50 principais são retornados, mas você pode usar o hello `$top` parâmetro tooreturn um número maior ou menor de itens (até too1000 em uma única resposta).

Por padrão, uma pontuação de pesquisa é calculada com base nas propriedades estatísticas dos dados saudação e consulta de saudação. A pesquisa do Azure localiza os documentos que incluem os termos de pesquisa de saudação na cadeia de caracteres de consulta de saudação (algumas ou todas, dependendo de `searchMode`), favorecendo os documentos que contêm muitas instâncias do termo de pesquisa de saudação. Olá pontuação de pesquisa aumenta ainda mais se o termo de saudação for raro no corpo de dados hello, mas comum no documento de saudação. Base de saudação de relevância de toocomputing essa abordagem é conhecida como TF-IDF ou (frequência de documento inversa da frequência do termo).

Supondo que não há nenhuma classificação personalizada, os resultados são então classificados pela pontuação de pesquisa antes de serem retornadas toohello aplicativo de chamada. Se `$top` não for especificado, 50 itens com a pesquisa mais alta de saudação pontuação é retornada.

Os valores de pontuação de pesquisa podem ser repetidos em todo um conjunto de resultados. Por exemplo, você pode ter 10 itens com uma pontuação de 1,2, 20 itens com uma pontuação de 1,0 e 20 itens com uma pontuação de 0,5. Quando várias ocorrências ter hello mesma pontuação de pesquisa, Olá ordenação dos mesmos itens de pontuação não está definido e não é estável. Execute a consulta Olá novamente e você poderá ver itens de deslocamento para a posição. Se houver dois itens com uma pontuação idêntica, não há garantia de qual deles aparecerá primeiro.

## <a name="when-toouse-custom-scoring"></a>Quando a pontuação personalizada do toouse
Você deve criar um ou mais perfis de pontuação ao comportamento de classificação padrão de saudação não vá suficiente em atender seus objetivos de negócios. Por exemplo, você pode decidir que a relevância de pesquisa deve favorecer itens adicionados recentemente. Da mesma forma, você pode ter um campo que contenha a margem de lucro ou algum outro campo indicando o potencial de receita. Aumentar as ocorrências que trazem benefícios comerciais tooyour pode ser um fator importante na decisão toouse perfis de pontuação.

A ordenação com base em relevância também é implementada por meio de perfis de pontuação. Considere os resultados da pesquisa de páginas que você usou no hello passado que lhe permitem classificar por relevância, data, classificação ou preço. Na pesquisa do Azure, perfis de pontuação direcionam a opção de "relevância" hello. definição de saudação de relevância é controlada por você, vinculada objetivos de negócios e o tipo de saudação de experiência de pesquisa, que você deseja toodeliver.

<a name="example"></a>

## <a name="example"></a>Exemplo
Como observado, a pontuação personalizada é implementada por meio de perfis de pontuação definidos em um esquema de índice.

Este exemplo mostra Olá esquema de um índice com dois perfis de pontuação (`boostGenre`, `newAndHighlyRated`). Qualquer consulta em relação a esse índice que inclui o perfil como um parâmetro de consulta usará o conjunto de resultados de saudação do hello perfil tooscore.

    {
      "name": "musicstoreindex",
      "fields": [
        { "name": "key", "type": "Edm.String", "key": true },
        { "name": "albumTitle", "type": "Edm.String" },
        { "name": "albumUrl", "type": "Edm.String", "filterable": false },
        { "name": "genre", "type": "Edm.String" },
        { "name": "genreDescription", "type": "Edm.String", "filterable": false },
        { "name": "artistName", "type": "Edm.String" },
        { "name": "orderableOnline", "type": "Edm.Boolean" },
        { "name": "rating", "type": "Edm.Int32" },
        { "name": "tags", "type": "Collection(Edm.String)" },
        { "name": "price", "type": "Edm.Double", "filterable": false },
        { "name": "margin", "type": "Edm.Int32", "retrievable": false },
        { "name": "inventory", "type": "Edm.Int32" },
        { "name": "lastUpdated", "type": "Edm.DateTimeOffset" }
      ],
      "scoringProfiles": [
        {
          "name": "boostGenre",
          "text": {
            "weights": {
              "albumTitle": 1.5,
              "genre": 5,
              "artistName": 2
            }
          }
        },
        {
          "name": "newAndHighlyRated",
          "functions": [
            {
              "type": "freshness",
              "fieldName": "lastUpdated",
              "boost": 10,
              "interpolation": "quadratic",
              "freshness": {
                "boostingDuration": "P365D"
              }
            },
            {
              "type": "magnitude",
              "fieldName": "rating",
              "boost": 10,
              "interpolation": "linear",
              "magnitude": {
                "boostingRangeStart": 1,
                "boostingRangeEnd": 5,
                "constantBoostBeyondRange": false
              }
            }
          ]
        }
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["albumTitle", "artistName"]
        }
      ]
    }


## <a name="workflow"></a>Fluxo de trabalho
tooimplement personalizado pontuação comportamento, adicione um esquema de toohello pontuação do perfil que define o índice de saudação. Você pode ter até too16 perfis de pontuação dentro de um índice (consulte [limites de serviço](search-limits-quotas-capacity.md)), mas você só pode especificar um perfil de tempo em qualquer consulta.

Iniciar com hello [modelo](#bkmk_template) fornecidas neste tópico.

Forneça um nome. Perfis de pontuação são opcionais, mas se você adicionar um, o nome de saudação é necessária. Ser toofollow-se de que as convenções de nomenclatura de saudação de campos (começar com uma letra, evita palavras reservadas e caracteres especiais). Consulte [Regras de nomenclatura](http://msdn.microsoft.com/library/azure/dn857353.aspx) para obter mais informações.

corpo de saudação do hello perfil de pontuação é construído com funções e campos ponderados.

### <a name="weights"></a>Pesos
Olá `weights` propriedade de um perfil de pontuação especifica pares de nome-valor que atribui um campo de tooa de peso relativo. Em Olá [exemplo](#example), campos de campos albumTitle, gênero e artistName Olá são ampliadas 1.5, 5 e 2, respectivamente. Por que é gênero mais aumentado de Olá outras pessoas? Se a pesquisa é realizada em dados que são um pouco homogêneos (como Olá caso gênero em Olá `musicstoreindex`), talvez seja necessário uma variação maior nos pesos relativos hello. Por exemplo, em Olá `musicstoreindex`, "rock" é exibido como um gênero e nas descrições de gênero escritas de forma idêntica. Se desejar que a descrição de gênero toooutweigh gênero, o campo de gênero Olá precisará um peso relativo mais alto.

### <a name="functions"></a>Funções
As funções são usadas quando cálculos adicionais são necessários para contextos específicos. Os tipos de função válidos são `freshness`, `magnitude`, `distance` e `tag`. Cada função tem parâmetros que são tooit exclusivo.

* `freshness`deve ser usado quando você quiser é tooboost por como novo ou antigo um item. Essa função só pode ser usada com campos datetime (`Edm.DataTimeOffset`). Saudação de Observação `boostingDuration` atributo é usado apenas com a função de atualização de saudação.
* `magnitude`deve ser usado quando você deseja tooboost com base em como alto ou baixo um valor numérico é. Cenários que exigem essa função incluem aumentar de acordo com a margem de lucro, maior preço, menor preço ou uma contagem de downloads. Você pode reverter o intervalo hello, toolow alta, se você quiser que o padrão inverso da saudação (por exemplo, tooboost menor preço itens mais itens com preço mais alto). Fornecido um intervalo de preços de USD 100 muito$ 1, você definiria `boostingRangeStart` em 100 e `boostingRangeEnd` em itens de menor preço de saudação 1 tooboost. Essa função só pode ser usada com campos duplo e inteiro.
* `distance`deve ser usado quando você quiser tooboost proximidade ou a localização geográfica. Essa função só pode ser usada com campos `Edm.GeographyPoint` .
* `tag`deve ser usado quando você quiser tooboost por marcas em comum entre documentos e consultas de pesquisa. Essa função só pode ser usada com campos `Edm.String` e `Collection(Edm.String)`.

#### <a name="rules-for-using-functions"></a>Regras para o uso de funções
* O tipo de função (freshness, magnitude, distance, tag) deve estar em minúsculas.
* As funções não podem incluir valores nulos ou vazios. Especificamente, se você incluir fieldname, você tem tooset-toosomething.
* Funções só podem ser aplicadas toofilterable campos. Consulte [Criar índice](search-api-2015-02-28-preview.md#CreateIndex) para obter mais informações sobre campos filtráveis.
* Funções só podem ser aplicadas toofields que estão definidos na coleção de campos de saudação de um índice.

Após a definição de índice hello, crie o índice de saudação carregando o esquema de índice hello, seguida pelos documentos. Consulte [Criar índice](search-api-2015-02-28-preview.md#CreateIndex) e [Adicionar ou atualizar documentos](search-api-2015-02-28-preview.md#AddOrUpdateDocuments) para obter instruções sobre essas operações. Depois de saudação índice é criado, você deve ter um perfil de pontuação funcional que funciona com seus dados de pesquisa.

<a name="bkmk_template"></a>

## <a name="template"></a>Modelo
Esta seção mostra a sintaxe de saudação e o modelo para perfis de pontuação. Consulte também[referência de atributo de índice](#bkmk_indexref) na próxima seção, para obter descrições dos atributos Olá Olá.

    ...
    "scoringProfiles": [
      {
        "name": "name of scoring profile",
        "text": (optional, only applies toosearchable fields) {
          "weights": {
            "searchable_field_name": relative_weight_value (positive #'s),
            ...
          }
        },
        "functions": (optional) [
          {
            "type": "magnitude | freshness | distance | tag",
            "boost": # (positive number used as multiplier for raw score != 1),
            "fieldName": "...",
            "interpolation": "constant | linear (default) | quadratic | logarithmic",

            "magnitude": {
              "boostingRangeStart": #,
              "boostingRangeEnd": #,
              "constantBoostBeyondRange": true | false (default)
            }

            // (- or -)

            "freshness": {
              "boostingDuration": "..." (value representing timespan over which boosting occurs)
            }

            // (- or -)

            "distance": {
              "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location)
              "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
            }

            // (- or -)

            "tag": {
              "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field)
            }
          }
        ],
        "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
      }
    ],
    "defaultScoringProfile": (optional) "...",
    ...

<a name="bkmk_indexref"></a>

## <a name="scoring-profile-property-reference"></a>Referência de propriedades de perfil de pontuação
> [!NOTE]
> Uma função de pontuação só pode ser aplicado toofields que podem ser filtrados.
>
>

| Propriedade | Descrição |
| --- | --- |
| `name` |Obrigatório. Este é o nome de saudação do hello perfil de pontuação. Ele segue Olá mesmas convenções de nomenclatura de um campo. Ele deve começar com uma letra, não podem conter pontos, dois-pontos ou símbolos @ e não pode começar com a frase hello "azureSearch" (diferencia maiusculas de minúsculas). |
| `text` |Contém a propriedade de pesos de saudação. |
| `weights` |Opcional. Um par de nome-valor que especifica um nome de campo e o peso relativo. O peso relativo deve ser um inteiro positivo ou o número de ponto flutuante. Você pode especificar o nome do campo Olá sem um peso correspondente. Os pesos são usados tooindicate Olá importância tooanother relativo de um campo. |
| `functions` |Opcional. Observe que uma função de pontuação só pode ser aplicado toofields que podem ser filtrados. |
| `type` |Necessário para funções de pontuação. Indica o tipo de saudação da função toouse. Os valores válidos incluem `magnitude`, `freshness`, `distance` e `tag`. Você pode incluir mais de uma função em cada perfil de pontuação. nome da função Hello deve estar em letras minúsculas. |
| `boost` |Necessário para funções de pontuação. Um número positivo usado como multiplicador para pontuação bruta. Ele não pode ser too1 igual. |
| `fieldName` |Necessário para funções de pontuação. Uma função de pontuação só pode ser aplicado toofields que fazem parte da coleção de campos de saudação do índice hello e que são podem ser filtrados. Além disso, cada tipo de função introduz restrições adicionais (a atualização é usada com campos datetime, a magnitude com campos de inteiro ou duplo, a distância com campos de local e a marca com campos de cadeia de caracteres ou coleção de cadeias de caracteres). Você só pode especificar um único campo por definição de função. Para o exemplo, toouse magnitude duas vezes em Olá mesmo perfil, você precisaria tooinclude duas magnitudes de definições, uma para cada campo. |
| `interpolation` |Necessário para funções de pontuação. Define a inclinação Olá para qual Olá impulso da pontuação aumente a partir do início de saudação do fim do intervalo de saudação toohello do intervalo de saudação. Os valores válidos incluem `linear` (padrão), `constant`, `quadratic` e `logarithmic`. Confira [Set interpolations](#bkmk_interpolation) (Definir interpolações) para obter detalhes. |
| `magnitude` |função de pontuação de magnitude de saudação é usado tooalter classificações com base no intervalo de saudação de valores para um campo numérico. Alguns exemplos de uso mais comuns Olá isso são:<ul><li>Classificações por estrelas: Alter Olá pontuação baseada no valor de saudação do campo de "Classificação por estrelas" hello. Quando dois itens forem relevantes, Olá item com classificação mais alta Olá será exibido primeiro.</li><li>Margem: Quando dois documentos forem relevantes, um revendedor poderá tooboost documentos que tenham margens superiores primeiro.</li><li>Contagens de cliques: para aplicativos que acompanham cliques por meio de ações tooproducts ou páginas, você pode usar itens de tooboost de magnitude que tendem a saudação tooget maior parte do tráfego.</li><li>Contagens de downloads: para aplicativos que controlam downloads, Olá a função de magnitude permite que você Impulsione os itens que têm a maioria dos downloads de saudação.</li></ul> |
| `magnitude:boostingRangeStart` |Olá conjuntos iniciar o valor do intervalo de saudação no qual a magnitude foi classificada. valor de saudação deve ser um inteiro ou um número de ponto flutuante. Para classificações por estrelas de 1 a 4, isso seria 1. Para mais acima de 50% de margens, isso seria 50. |
| `magnitude:boostingRangeEnd` |Define o valor de final de saudação do intervalo de saudação no qual a magnitude foi classificada. valor de saudação deve ser um inteiro ou um número de ponto flutuante. Para classificações por estrelas de 1 a 4, isso seria 4. |
| `magnitude:constantBoostBeyondRange` |Os valores válidos são true ou false (padrão). Quando definido como tootrue, aumento completo Olá continuará toodocuments tooapply que tem um valor de campo de destino de saudação que é maior do que Olá o final superior do intervalo de saudação. Se for false, aumento Olá dessa função não será aplicado toodocuments com um valor para o campo de destino Olá que está fora do intervalo de saudação. |
| `freshness` |função de pontuação de atualização de saudação é usado tooalter classificação pontuações de itens com base nos valores dos campos DateTimeOffset. Por exemplo, um item com uma data mais recente pode ter classificação mais alta do que itens mais antigos. (Observe que também é possível toorank itens como eventos de calendário com datas futuras, de modo que toohello mais próximo de itens presente pode ser classificado melhor do que itens em Olá futuras.) Na versão atual do serviço hello, uma das extremidades do intervalo de saudação será corrigida toohello hora atual. Olá, outra extremidade é uma hora com base em Olá Olá últimos `boostingDuration`. tooboost um intervalo de horas em Olá futuras usar um negativo `boostingDuration`. taxa de saudação no qual Olá aumentando as alterações de um intervalo mínimo e máximo é determinado pelo Olá interpolação aplicada toohello perfil de pontuação (consulte a Figura Olá abaixo). tooreverse Olá fator de aumento aplicado, escolha um fator de aumento de menor que 1. |
| `freshness:boostingDuration` |Define um período de expiração após o qual o aumento será interrompido para um documento específico. Consulte [definir boostingDuration](#bkmk_boostdur) em Olá seção de sintaxe e exemplos a seguir. |
| `distance` |função de pontuação de distância de saudação é usado tooaffect Olá pontuação dos documentos com base em como fecha ou longe eles estão tooa relativo localização geográfica de referência. local de referência de saudação é fornecido como parte da consulta de saudação em um parâmetro (usando Olá `scoringParameter` parâmetro de consulta) como um argumento lon, lat. |
| `distance:referencePointParameter` |Toobe um parâmetro passado em consultas toouse como local de referência. scoringParameter é um parâmetro de consulta. Consulte [Pesquisar documentos](search-api-2015-02-28-preview.md#SearchDocs) para obter descrições dos parâmetros de consulta. |
| `distance:boostingDistance` |Um número que indica a distância de saudação em quilômetros do local de referência de saudação onde Olá aumentando o intervalo termina. |
| `tag` |Olá marca de pontuação de função é usada tooaffect pontuação de saudação de documentos com base em marcas em documentos e consultas de pesquisa. Documentos que tenham marcas em comum com a consulta de pesquisa hello serão ser ampliados. Olá marcas para consulta de pesquisa de saudação é fornecida como um parâmetro de pontuação em cada solicitação de pesquisa (usando Olá `scoringParameter` parâmetro de consulta). |
| `tag:tagsParameter` |Um parâmetro toobe transmitido em consultas toospecify marcas para uma determinada solicitação. `scoringParameter` é um parâmetro de consulta. Consulte [Pesquisar documentos](search-api-2015-02-28-preview.md#SearchDocs) para obter descrições dos parâmetros de consulta. |
| `functionAggregation` |Opcional. Aplicável apenas quando funções são especificadas. Os valores válidos incluem: `sum` (padrão), `average`, `minimum`, `maximum` e `firstMatching`. Uma pontuação de pesquisa é um valor único calculado por meio de diversas variáveis, incluindo várias funções. Esses atributos indica como os aumentos de saudação de todas as funções hello são combinados em um único aumento de agregação que é então aplicado toohello base pontuação de documento. pontuação básica Olá baseia-se em Olá tf-idf valor computado do documento hello e consulta de pesquisa de saudação. |
| `defaultScoringProfile` |Ao se executar uma solicitação de pesquisa, se nenhum perfil de pontuação for especificado, a pontuação padrão será usada (somente tf-idf). Um nome de perfil de pontuação padrão pode ser definido aqui, fazendo com que toouse de pesquisa do Azure que esse perfil quando nenhum perfil específico for fornecido na solicitação de pesquisa de saudação. |

<a name="bkmk_interpolation"></a>

## <a name="set-interpolations"></a>Set interpolations
As interpolações permitem que você toodefine inclinação de saudação para qual Olá impulso da pontuação aumente a partir do início de saudação do fim do intervalo de saudação toohello do intervalo de saudação. Olá interpolações a seguir pode ser usado:

* `Linear`: Para itens que estão dentro de saudação max e min intervalo, Olá aumento aplicado toohello item será feito em um período decrescente de forma constante. Linear é a interpolação saudação padrão para um perfil de pontuação.
* `Constant`: Para itens que estão no intervalo saudação inicial e final, um aumento constante será aplicado toohello resultados de classificação.
* `Quadratic`: Na comparação tooa interpolação Linear que tenha um aumento decrescente de forma constante, quadrática inicialmente diminuirá em um nível menor e, em seguida, à medida que se aproxima o intervalo de término hello, ela diminui em um intervalo muito maior. Essa opção de interpolação não é permitida em funções de pontuação de marca.
* `Logarithmic`: Na comparação tooa interpolação Linear que tenha um aumento decrescente de forma constante, logarítmica inicialmente diminuirá em um nível maior e, em seguida, à medida que se aproxima o intervalo de término hello, ela diminui em um intervalo muito menor. Essa opção de interpolação não é permitida em funções de pontuação de marca.

<a name="Figure1"></a> ![][1]

<a name="bkmk_boostdur"></a>

## <a name="set-boostingduration"></a>Definir boostingDuration
`boostingDuration`é um atributo da função de atualização de saudação. Use-tooset um período de expiração após o qual o aumento parará para um determinado documento. Por exemplo, tooboost uma linha de produto ou marca por um período promocional de 10 dias, você especificaria período de 10 dias hello como "P10D" para esses documentos. Ou especificam tooboost próximos eventos Olá próxima semana "-P7D".

`boostingDuration` deve ser formatado como um valor XSD de "dayTimeDuration" (um subconjunto restrito de um valor de duração ISO 8601). saudação padrão para isso é: `[-]P[nD][T[nH][nM][nS]]`.

Olá, a tabela a seguir fornece vários exemplos.

| Duration | boostingDuration |
| --- | --- |
| 1 dia |"P1D" |
| 2 dias e 12 horas |"P2DT12H" |
| 15 minutos |"PT15M" |
| 30 dias, 5 horas, 10 minutos e 6,334 segundos |"P30DT5H10M6.334S" |

Para obter mais exemplos, consulte [Esquema XML: tipos de dados (site W3.org)](http://www.w3.org/TR/xmlschema11-2/).

**Veja também**
[API REST do Serviço do Azure Search](http://msdn.microsoft.com/library/azure/dn798935.aspx) no MSDN <br/>
[Criar índice (API do Azure Search)](http://msdn.microsoft.com/library/azure/dn798941.aspx) no MSDN<br/>
[Adicionar um índice de pesquisa de tooa perfil pontuação](http://msdn.microsoft.com/library/azure/dn798928.aspx) no MSDN<br/>

<!--Image references-->
[1]: ./media/search-api-scoring-profiles-2015-02-28-Preview/scoring_interpolations.png
