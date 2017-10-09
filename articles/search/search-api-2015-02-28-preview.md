---
title: "aaaAzure pesquisa serviço REST API Versão 2015-02-28-visualização | Microsoft Docs"
description: "A API do serviço Azure Search Versão 2015-02-28-Preview inclui recursos experimentais como analisadores de linguagem natural e pesquisas do tipo moreLikeThis."
services: search
documentationcenter: na
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 3dba3bf8-9c83-42f6-82bc-04727bd11037
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: search
ms.date: 05/01/2017
ms.author: brjohnst
ms.openlocfilehash: 63cb30b7f43a42552c6744ea087afea947857224
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-service-rest-api-version-2015-02-28-preview"></a>API REST do serviço Azure Search: Versão 2015-02-28-Preview
Este artigo é uma documentação de referência Olá para `api-version=2015-02-28-Preview`. Essa visualização estende a versão disponível atual de hello, [api-version = 2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), fornecendo Olá recursos experimentais a seguir:

* `moreLikeThis`consulta parâmetro hello [procurar documentos](#SearchDocs) API. Encontrar outros documentos que são documentos específicos tooanother relevantes.

Algumas partes adicionais de saudação `2015-02-28-Preview` API REST estão documentados separadamente. Estão incluídos:

* [Perfis de pontuação](search-api-scoring-profiles-2015-02-28-preview.md)
* [Indexadores](search-api-indexers-2015-02-28-preview.md)

O serviço Azure Search está disponível em várias versões. Consulte também[controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes.

## <a name="apis-in-this-document"></a>APIs neste documento
A API do serviço Pesquisa do Azure dá suporte a duas sintaxes de URL para operações de API: simples e OData (consulte [Suporte a OData (API da Pesquisa do Azure)](http://msdn.microsoft.com/library/azure/dn798932.aspx) para obter detalhes). Olá lista a seguir mostra a saudação simples sintaxe.

[Criar o índice](#CreateIndex)

    POST /indexes?api-version=2015-02-28-Preview

[Atualizar o índice](#UpdateIndex)

    PUT /indexes/[index name]?api-version=2015-02-28-Preview

[Obter o índice](#GetIndex)

    GET /indexes/[index name]?api-version=2015-02-28-Preview

[Listando índices](#ListIndexes)

    GET /indexes?api-version=2015-02-28-Preview

[Obter estatísticas de índice](#GetIndexStats)

    GET /indexes/[index name]/stats?api-version=2015-02-28-Preview

[Analisador de teste](#TestAnalyzer)

    POST /indexes/[index name]/analyze?api-version=2015-02-28-Preview

[Excluir um índice](#DeleteIndex)

    DELETE /indexes/[index name]?api-version=2015-02-28-Preview

[Adicionar, excluir e atualizar dados em um índice](#AddOrUpdateDocuments)

    POST /indexes/[index name]/docs/index?api-version=2015-02-28-Preview

[Pesquisar documentos](#SearchDocs)

    GET /indexes/[index name]/docs?[query parameters]
    POST /indexes/[index name]/docs/search?api-version=2015-02-28-Preview

[Procurar documento](#LookupAPI)

     GET /indexes/[index name]/docs/[key]?[query parameters]

[Contar documentos](#CountDocs)

    GET /indexes/[index name]/docs/$count?api-version=2015-02-28-Preview

[Sugestões](#Suggestions)

    GET /indexes/[index name]/docs/suggest?[query parameters]
    POST /indexes/[index name]/docs/suggest?api-version=2015-02-28-Preview

- - -
<a name="IndexOps"></a>

## <a name="index-operations"></a>Operações de índice
Você pode criar e gerenciar índices no serviço Azure Search por meio de solicitações HTTP simples (POST, GET, PUT, DELETE) em relação a um recurso de índice específico. toocreate um índice, você primeiro lançar um documento JSON que descreve o esquema de índice hello. esquema de saudação define campos de saudação do índice hello, seus tipos de dados e como eles podem ser usados (por exemplo, em pesquisas de texto completo, filtros, classificação ou facetas). Ele também define os perfis de pontuação, sugestões e outros comportamentos de saudação do tooconfigure de atributos de índice de saudação.

Olá, exemplo a seguir fornece uma ilustração de um esquema usado para pesquisar informações de hotel com campo de descrição de saudação definido em dois idiomas. Observe como atributos controlam como o campo de saudação é usado. Por exemplo hello `hotelId` é usada como chave de documento hello (`"key": true`) e é excluído do pesquisas de texto completo (`"searchable": false`).

    {
    "name": "hotels",  
    "fields": [
      {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
      {"name": "baseRate", "type": "Edm.Double"},
      {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
      {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
      {"name": "hotelName", "type": "Edm.String"},
      {"name": "category", "type": "Edm.String"},
      {"name": "tags", "type": "Collection(Edm.String)"},
      {"name": "parkingIncluded", "type": "Edm.Boolean"},
      {"name": "smokingAllowed", "type": "Edm.Boolean"},
      {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
      {"name": "rating", "type": "Edm.Int32"},
      {"name": "location", "type": "Edm.GeographyPoint"}
     ],
     "suggesters": [
      {
       "name": "sg",
       "searchMode": "analyzingInfixMatching",
       "sourceFields": ["hotelName"]
      }
     ]
    }

Após a criação de índice hello, você vai carregar documentos que preenchem o índice de saudação. Consulte [Adicionar ou Atualizar Documentos](#AddOrUpdateDocuments) para a próxima etapa.

Para um tooindexing de vídeo de Introdução na pesquisa do Azure, consulte Olá [episódio de cobertura de nuvem do Channel 9 na pesquisa do Azure](http://go.microsoft.com/fwlink/p/?LinkId=511509).

<a name="CreateIndex"></a>

## <a name="create-index"></a>Criar o índice
Um índice é o meio principal de saudação de organizar e pesquisar documentos na pesquisa do Azure, semelhante toohow uma tabela organiza registros em um banco de dados. Cada índice tem uma coleção de documentos que todos estejam de acordo com o esquema de índice toohello (nomes de campo, tipos de dados e propriedades), mas índices também especificam outras construções (sugestões, perfis de pontuação e opções de CORS) que definem outros comportamentos de pesquisa.

Você pode criar um novo índice em um serviço Azure Search usando uma solicitação HTTP POST ou PUT. corpo de saudação da solicitação de saudação é um esquema JSON que especifica as informações de configuração e de índice hello.

    POST https://[service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Como alternativa, você pode usar PUT e especificar o nome do índice Olá em Olá URI. Se o índice de saudação não existir, ele será criado.

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]

Criando um índice determina a estrutura Olá Olá documentos armazenados e usados em operações de pesquisa. Índice de saudação popular é uma operação separada. Nessa etapa, você pode usar um [indexador](https://msdn.microsoft.com/library/azure/mt183328.aspx) (disponível para fontes de dados com suporte) ou uma operação [Adicionar, Atualizar ou Excluir Documentos](https://msdn.microsoft.com/library/azure/dn798930.aspx). índice de saudação invertida é gerado quando Olá documentos são publicados.

**Observação**: número máximo de saudação de índices permitidos varia por tipo de preço. serviço gratuito Olá permite que até too3 índices. O serviço padrão permite 50 índices por serviço de pesquisa. Consulte [Limites e restrições](http://msdn.microsoft.com/library/azure/dn798934.aspx) para obter detalhes.

**Solicitação**

HTTPS é necessário para todas as solicitações de serviço. Olá **Create Index** solicitação pode ser criada usando um método POST ou PUT. Ao usar POST, você deve fornecer um nome de índice no corpo da solicitação de saudação junto com a definição de esquema de índice hello. Com PUT, o nome do índice Olá é parte da URL de saudação. Se o índice Olá não existir, ele será criado. Se já existir, é atualizado toohello nova definição.

nome do índice Olá deve estar em letras minúsculas, começar com uma letra ou número, não ter barras ou pontos e ter menos de 128 caracteres. Depois de iniciar o nome do índice Olá com uma letra ou número, restante de saudação do nome hello pode incluir qualquer letra, número e traços, como Olá traços não sejam consecutivos.

Olá `api-version` é necessária. Consulte [Controle de Versão de Serviço de Pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter uma lista das versões disponíveis.

**Cabeçalhos da solicitação**

Olá lista a seguir descreve hello necessárias e cabeçalhos opcionais da solicitação.

* `Content-Type`: obrigatório. Defina esta opção muito`application/json`
* `api-key`: obrigatório. Olá `api-key` é usado para
* autenticar o serviço de pesquisa do hello solicitação tooyour. É um valor de cadeia de caracteres, o serviço de tooyour exclusivo. Olá **Create Index** solicitação deve incluir um `api-key` cabeçalho definido tooyour a chave de administração (como a chave de consulta tooa contrário).

Você também precisará Olá serviço nome tooconstruct Olá solicitação URL. Você pode obter o nome do serviço hello e `api-key` do seu painel de serviço no hello Portal do Azure. Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter ajuda de navegação de página.

<a name="RequestData"></a>
**Sintaxe do Corpo da Solicitação**

corpo de saudação da solicitação Olá contém uma definição de esquema, que inclui Olá lista de campos de dados em documentos que serão inseridos nesse índice, atributos, tipos de dados, bem como uma lista opcional de perfis de pontuação é usado tooscore correspondência documentos em tempo de consulta.

Observe que, para uma solicitação POST, você deve especificar o nome do índice Olá no corpo da solicitação de saudação.

Pode haver apenas um campo de chave no índice de saudação. Ele tem toobe um campo de cadeia de caracteres. Este campo representa o identificador exclusivo de saudação para cada documento armazenado no índice de saudação.

partes principais de saudação de um índice incluem o seguinte hello:

* `name`
* `fields` que serão inseridos nesse índice, incluindo nome, tipo de dados e propriedades que definem as ações permitidas nesse campo.
* `suggesters` usados para consultas de preenchimento automático ou digitação antecipada.
* `scoringProfiles` usados para classificação de pontuação de pesquisa personalizada. Consulte [Adicionar perfis de pontuação](https://msdn.microsoft.com/library/azure/dn798928.aspx) para obter detalhes.
* `analyzers`, `charFilters`, `tokenizers`, `tokenFilters` usado toodefine como documentos/consultas são divididas em tokens indexáveis pesquisável. Confira [Análise na Pesquisa do Azure](https://aka.ms//azsanalysis) para obter detalhes.
* `defaultScoringProfile`usado o padrão de saudação toooverwrite comportamentos de pontuação.
* `corsOptions`consultas entre origens de tooallow em seu índice.

sintaxe de saudação para estruturar a carga de solicitação de saudação é da seguinte maneira. Uma solicitação de exemplo é fornecida mais adiante neste tópico.

    {
      "name": (optional on PUT; required on POST) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false,              
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
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
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }

**Atributos de índice**

Olá seguintes atributos podem ser definidos ao criar um índice. Para obter detalhes sobre pontuação e perfis de pontuação, consulte [Adicionar perfis de pontuação](https://msdn.microsoft.com/library/azure/dn798928.aspx).

`name`-Conjuntos de Olá nome do campo de saudação.

`type`-Conjuntos de Olá tipo de dados para o campo de saudação.

`searchable`-Marca Olá campo como texto completo pode ser pesquisado. Isso significa que ele será submetido a análise, como separação de palavras, durante a indexação. Se você definir um `searchable` campo tooa valor como "dia ensolarado", internamente ele será dividido em tokens individuais hello "Ensolarado" e "dia". Isso habilita pesquisas de texto completo para esses termos. Os campos dos tipos `Edm.String` ou `Collection(Edm.String)` são `searchable` por padrão. Campos de outros tipos não podem ser `searchable`.

* **Observação**: `searchable` campos consomem espaço extra no índice, desde que a pesquisa do Azure armazenará uma versão com token adicional do valor do campo Olá para pesquisas de texto completo. Se você quiser toosave espaço no seu índice e não é necessário um toobe campo incluído nas pesquisas, defina `searchable` muito`false`.

`filterable`-Permite Olá campo toobe referenciado em `$filter` consultas. `filterable` difere de `searchable` da maneira como cadeias de caracteres são tratadas. Campos dos tipos `Edm.String` ou `Collection(Edm.String)` que são `filterable` não são submetidos à quebra de palavras. Portanto, as comparações são apenas para correspondências exatas. Por exemplo, se você definir um campo `f` muito "dia ensolarado", `$filter=f eq 'sunny'` encontrará nenhuma correspondência, mas `$filter=f eq 'sunny day'` será. Todos os campos são `filterable` por padrão.

`sortable`-Por padrão Olá sistema classifica os resultados pela pontuação, mas em muitas experiências os usuários desejarão toosort por campos nos documentos de saudação. Campos do tipo `Collection(Edm.String)` não podem ser `sortable`. Todos os outros campos são `sortable` por padrão.

`facetable`‒ geralmente usado em uma apresentação dos resultados de pesquisa que inclui a contagem de ocorrências por categoria (por exemplo, pesquisar câmeras digitais e ver as ocorrências por marca, por megapixels, por preço etc.). Essa opção não pode ser usada com campos do tipo `Edm.GeographyPoint`. Todos os outros campos são `facetable` por padrão.

* **Observação**: campos do tipo `Edm.String` que são `filterable`, `sortable` ou `facetable` podem ter no máximo 32 KB de comprimento. Isso ocorre porque esses campos são tratados como um termo de pesquisa único e o comprimento máximo de saudação de um termo na pesquisa do Azure é de 32KB. Se você precisar toostore mais texto que isso em um campo de cadeia de caracteres único, você precisará tooexplicitly definir `filterable`, `sortable`, e `facetable` muito`false` na definição do índice.
* **Observação**: se um campo não tiver nenhum Olá acima atributos definidos muito`true` (`searchable`, `filterable`, `sortable`, ou`facetable`) campo Olá será excluído efetivamente do índice Olá invertido. Essa opção é útil para campos que não são usados em consultas, mas são necessários em resultados de pesquisa. Excluir esses campos do índice Olá melhora o desempenho.

`key`-As marcas Olá campo como contendo identificadores exclusivos para documentos no índice de saudação. Exatamente um campo deve ser escolhido como Olá `key` campo e ele devem ser do tipo `Edm.String`. Campos de chave podem ser usado toolook documentos diretamente por meio de saudação [API de pesquisa](#LookupAPI).

`retrievable`-Define se o campo Olá pode ser retornado em um resultado de pesquisa.  Isso é útil quando você deseja toouse um campo (por exemplo, margem) como um filtro, classificação ou mecanismo de pontuação, mas não deseja usuário final do hello campo toobe toohello visível. Esse atributo deve ser `true` for `key` .

`analyzer`-Define Olá nome da saudação analisador toouse Olá campo em tempo de pesquisa e indexação de hora. Para Olá conjunto de valores permitido consulte [analisadores](https://msdn.microsoft.com/library/mt605304.aspx). Essa opção pode ser usada apenas com campos `searchable`, e não pode ser definida com `searchAnalyzer` ou `indexAnalyzer`.  Depois que o analisador de saudação for escolhido, não pode ser alterado para o campo de saudação.

`searchAnalyzer`-Conjuntos de Olá nome do analisador Olá usado em tempo de pesquisa para o campo de saudação. Para Olá conjunto de valores permitido consulte [analisadores](https://msdn.microsoft.com/library/mt605304.aspx). Essa opção só pode ser usada com campos `searchable` . Ele deve ser definido em conjunto com `indexAnalyzer` e não pode ser definida com hello `analyzer` opção. Esse analisador pode ser atualizado em um campo existente.

`indexAnalyzer`-Conjuntos de Olá nome do analisador de saudação usada no momento da indexação para o campo de saudação. Para Olá conjunto de valores permitido consulte [analisadores](https://msdn.microsoft.com/library/mt605304.aspx). Essa opção só pode ser usada com campos `searchable` . Ele deve ser definido em conjunto com `searchAnalyzer` e não pode ser definida com hello `analyzer` opção. Depois que o analisador de saudação for escolhido, não pode ser alterado para o campo de saudação.

`suggesters`-Conjuntos de Olá modo de pesquisa e campos de origem de saudação do conteúdo de saudação para obter sugestões. Consulte [Sugestores](#Suggesters) para obter detalhes.

`scoringProfiles` ‒ define comportamentos de pontuação personalizados que permitem influenciam quais itens aparecem em posição mais elevada nos resultados de pesquisa. Perfis de pontuação são compostos de funções e pesos de campos. Consulte [adicionar perfis de pontuação](https://msdn.microsoft.com/library/azure/dn798928.aspx) para obter mais informações sobre atributos de saudação usados em um perfil de pontuação.

<!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Suporte ao idioma**

Os campos pesquisáveis são submetidos a análise que, frequentemente, envolve quebra de palavras, normalização do texto e filtragem de termos. Por padrão, os campos de pesquisa na pesquisa do Azure são analisados com hello [analisador padrão do Apache Lucene](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) que quebra o texto em elementos seguindo o["Segmentação de texto Unicode"](http://unicode.org/reports/tr29/) regras. Além disso, analisador padrão Olá converte a forma de letras minúsculas do todos os caracteres tootheir. Os documentos indexados e termos de pesquisa percorrer analysis Olá durante a indexação e processamento de consulta.

A Pesquisa do Azure oferece suporte a vários idiomas. Cada um desses idiomas requer um analisador de texto não padrão que leva em consideração as características de determinado idioma. O Azure Search oferece dois tipos de analisadores:

* 35 analisadores ativados pela Lucene.
* 50 analisadores apoiados pela tecnologia de processamento de idioma natural proprietária da Microsoft usada no Office e no Bing.

Alguns desenvolvedores talvez prefira Olá solução mais familiar, simple de código-fonte aberto do Lucene. Analisadores Lucene são mais rápidas, mas analisadores de Microsoft hello têm recursos avançados, como lematização, decompounding (nos idiomas alemão, dinamarquês, holandês, sueco, norueguês, estoniano, concluir, húngaro, Eslovaco) e reconhecimento de entidade (URLs de palavras emails, datas, números). Se possível, você deve executar comparações de ambos os Olá Lucene e Microsoft analisadores toodecide qual é a melhor opção.

***Veja a comparação***

Analisador do Lucene Olá para inglês estende o analisador padrão hello. Ele remove possessivos (apóstrofos à direita) de palavras, aplica a lematização conforme o [algoritmo de lematização de Porter](http://tartarus.org/~martin/PorterStemmer/) e remove as [palavras irrelevantes](http://en.wikipedia.org/wiki/Stop_words) do inglês.

Em comparação, o analisador do Microsoft hello executa lematização em vez de lematização. Isso significa que ele pode tratar muito melhor as formas irregulares e inflexivas de palavras, o que gera resultados da pesquisa mais relevantes (observe o módulo 7 da [Apresentação MVA da Pesquisa do Azure](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) para obter mais detalhes).

A indexação com analisadores da Microsoft em média é duas vezes toothree mais lentos que seus equivalentes do Lucene, dependendo da linguagem de saudação. O desempenho da pesquisa não dever significativamente afetado para consultas de tamanho médio.

***Configuração***

Para cada campo na definição de índice hello, você pode definir Olá `analyzer` nome da propriedade tooan analisador que especifica o idioma e o fornecedor. Olá analisador mesmo será aplicada quando a indexação e pesquisa para esse campo.
Por exemplo, você pode ter campos separados para descrições de hotel em inglês, francês e espanhol que existem lado a lado no hello mesmo índice. Saudação de uso [parâmetro de consulta 'searchFields'](#SearchQueryParameters) toospecify que toosearch campo específico do idioma contra em suas consultas. Você pode examinar os exemplos de consultas que incluem hello `analyzer` propriedade [procurar documentos](#SearchDocs). 

***Lista de analisadores***

Abaixo está a lista de saudação de idiomas com suporte, juntamente com os nomes de analisador Lucene e Microsoft.

<table style="font-size:12">
    <tr>
        <th>idioma</th>
        <th>Nome do analisador da Microsoft</th>
        <th>Nome do analisador da Lucene</th>
    </tr>
    <tr>
        <td>Árabe</td>
        <td>ar.microsoft</td>
        <td>ar.lucene</td>        
    </tr>
    <tr>
        <td>Armênia</td>
        <td></td>
        <td>hy.Lucene</td>
      </tr>
    <tr>
        <td>Bangla</td>
        <td>bn.microsoft</td>
        <td></td>
    </tr>
      <tr>
        <td>Basco</td>
        <td></td>
        <td>Eu.Lucene</td>
    </tr>
      <tr>
         <td>Búlgaro</td>
        <td>bg.microsoft</td>
        <td>BG.Lucene</td>
      </tr>
      <tr>
        <td>Catalão</td>
        <td>ca.microsoft</td>
        <td>CA.Lucene</td>          
      </tr>
    <tr>
        <td>Chinês (simplificado)</td>
        <td>zh-Hans.microsoft</td>
        <td>zh-Hans.lucene</td>        
    </tr>
    <tr>
        <td>Chinês (tradicional)</td>
        <td>zh-Hant.microsoft</td>
        <td>zh-Hant.lucene</td>        
    <tr>
    <tr>
        <td>Croata</td>
        <td>hr.microsoft</td>
        <td/></td>
    </tr>
    <tr>
        <td>Tcheco</td>
        <td>cs.microsoft</td>
        <td>cs.lucene</td>        
    </tr>    
    <tr>
        <td>Dinamarquês</td>
        <td>da.Microsoft</td>
        <td>da.lucene</td>        
    </tr>    
    <tr>
        <td>Holandês</td>
        <td>nl.microsoft</td>
        <td>nl.lucene</td>    
    </tr>    
    <tr>
        <td>Inglês</td>        
        <td>en.Microsoft</td>
        <td>en.lucene</td>        
    </tr>
    <tr>
        <td>Estoniano</td>
        <td>et.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Finlandês</td>
        <td>fi.microsoft</td>
        <td>fi.lucene</td>        
    </tr>    
    <tr>
        <td>Francês</td>
        <td>fr.microsoft</td>
        <td>fr.lucene</td>        
    </tr>
    <tr>
        <td>Galego</td>
        <td></td>
        <td>GL.Lucene</td>        
      </tr>
    <tr>
        <td>Alemão</td>
        <td>de.microsoft</td>
        <td>de.lucene</td>        
    </tr>
    <tr>
        <td>Grego</td>
        <td>el.microsoft</td>
        <td>el.lucene</td>        
    </tr>
    <tr>
        <td>Guzerate</td>
        <td>gu.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Hebraico</td>
        <td>he.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Híndi</td>
        <td>hi.microsoft</td>
        <td>hi.lucene</td>        
    </tr>
    <tr>
        <td>Húngaro</td>        
        <td>hu.Microsoft</td>
        <td>hu.lucene</td>
    </tr>
    <tr>
        <td>Islandês</td>
        <td>is.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Indonésio (Bahasa)</td>
        <td>id.microsoft</td>
        <td>id.lucene</td>        
    </tr>
    <tr>
        <td>Irlandês</td>
        <td></td>
          <td>GA.Lucene</td>
    </tr>
    <tr>
        <td>Italiano</td>
        <td>it.microsoft</td>
        <td>it.lucene</td>        
    </tr>
    <tr>
        <td>Japonês</td>
        <td>ja.microsoft</td>
        <td>ja.lucene</td>

    </tr>
    <tr>
        <td>Kannada</td>
        <td>ka.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Coreano</td>
        <td>ko.Microsoft</td>
        <td>ko.lucene</td>
    </tr>
    <tr>
        <td>Letão</td>        
        <td>lv.microsoft</td>
        <td>lv.lucene</td>    
    </tr>
    <tr>
        <td>Lituano</td>
        <td>lt.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Malaiala</td>
        <td>ml.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Malaio (latino)</td>
        <td>ms.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Marati</td>
        <td>mr.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Norueguês</td>
        <td>nb.microsoft</td>
        <td>no.lucene</td>        
    </tr>
      <tr>
        <td>Persa</td>
        <td></td>
        <td>FA.Lucene</td>        
      </tr>
    <tr>
        <td>Polonês</td>
        <td>pl.Microsoft</td>
        <td>pl.lucene</td>        
    </tr>
    <tr>
        <td>Português (Brasil)</td>
        <td>pt-Br.microsoft</td>
        <td>pt-Br.lucene</td>        
    </tr>
    <tr>
        <td>Português (Portugal)</td>
        <td>pt-Pt.microsoft</td>        
        <td>pt-Pt.lucene</td>
    </tr>
    <tr>
        <td>Punjabi</td>
        <td>pa.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Romeno</td>
        <td>ro.microsoft</td>
        <td>ro.lucene</td>
    </tr>
    <tr>
        <td>Russo</td>
        <td>ru.microsoft</td>
        <td>ru.lucene</td>    
    </tr>
    <tr>
        <td>Sérvio (cirílico)</td>
        <td>sr-cyrillic.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Sérvio (latino)</td>
        <td>sr-latin.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Eslovaco</td>
        <td>sk.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Esloveno</td>
        <td>sl.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Espanhol</td>
        <td>es.microsoft</td>
        <td>es.lucene</td>
    </tr>
    <tr>
        <td>Sueco</td>
        <td>sv.microsoft</td>
        <td>sv.lucene</td>
    </tr>

    <tr>
        <td>Tâmil</td>
        <td>ta.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Télugo</td>
        <td>te.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Tailandês</td>
        <td>th.microsoft</td>
        <td>th.lucene</td>
    </tr>
    <tr>
        <td>Turco</td>
        <td>tr.microsoft</td>
        <td>tr.lucene</td>        
    </tr>
    <tr>
        <td>Ucraniano</td>
        <td>uk.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Urdu</td>
        <td>ur.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Vietnamita</td>
        <td>vi.microsoft</td>
        <td></td>
    </tr>
    <td colspan="3">Além disso, o Azure Search fornece configurações do analisador que não são específicas de idiomas</td>
    <tr>
        <td>Dobra ASCII padrão</td>
        <td>standardasciifolding.Lucene</td>
        <td>
        <ul>
            <li>Segmentação de texto Unicode (Criador de Token Padrão)</li>
            <li>Filtro de dobra em ASCII - converte caracteres Unicode que não pertencem a toohello conjunto dos primeiros 127 caracteres ASCII em seus equivalentes em ASCII. Isso é útil para remover os sinais diacríticos.</li>
        </ul>
        </td>
    </tr>
</table>

Todos os analisadores com nomes anotados com <i>lucene</i> são da plataforma de [analisadores de idiomas do Apache Lucene](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html). Para obter mais informações sobre o filtro de dobra em ASCII Olá podem ser encontradas [aqui](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).

**Sugestores**

Um `suggester` define quais campos em um índice são usada toosupport preenchimento automático em pesquisas. Normalmente, cadeias de caracteres de pesquisa parciais são enviadas toohello [API de sugestões](#Suggestions) enquanto o usuário hello está digitando uma consulta de pesquisa e Olá API retorna um conjunto de frases sugeridas. Uma sugestão que você definir no índice Olá determina quais campos são os termos de pesquisa de preenchimento automático de saudação do toobuild usado. Consulte [Sugestores](#Suggesters) para obter detalhes de configuração.

**Perfis de pontuação**

Um `scoringProfile` define os comportamentos de pontuação personalizados que lhe permitem influenciar quais itens aparecerão nos resultados da pesquisa hello. Perfis de pontuação são compostos de funções e pesos de campos. toouse-los, especifique um perfil por nome na cadeia de caracteres de consulta de saudação.

Um perfil de pontuação padrão funciona por trás Olá cenas toocompute uma pontuação de pesquisa para cada item em um conjunto de resultados. Você pode usar o perfil de pontuação interno e sem nome hello. Como alternativa, defina `defaultScoringProfile` toouse um perfil personalizado como padrão hello, invocado sempre que um perfil personalizado não for especificado na cadeia de caracteres de consulta de saudação.

Consulte [tooa índice de pesquisa (API de REST do serviço de pesquisa do Azure) de perfis de pontuação adicionar](search-api-scoring-profiles-2015-02-28-preview.md) para obter detalhes.

**Opções de CORS**

Javascript do lado do cliente não é possível chamar quaisquer APIs por padrão, desde que o navegador Olá impedirá que todas as solicitações entre origens. Habilitar o CORS (Cross-Origin Resource Sharing) por configuração Olá `corsOptions` índice de tooyour do atributo tooallow consultas entre origens. Observe que apenas APIs de consulta dão suporte a CORS por motivos de segurança. Olá, as opções a seguir pode ser definida para CORS:

* `allowedOrigins`(obrigatório): esta é uma lista de origens que terão o índice de tooyour de acesso. Isso significa que qualquer código Javascript servido dessas origens terá permissão tooquery seu índice (assumindo que fornece Olá chave de API correta). Cada origem é geralmente do formulário Olá `protocol://fully-qualified-domain-name:port` embora Olá porta seja frequentemente omitida. Consulte [este artigo](http://go.microsoft.com/fwlink/?LinkId=330822) para obter mais detalhes.
  * Origens de tooall acesso tooallow, inclua `*` como um único item no hello `allowedOrigins` matriz. Observe que **essa não é uma prática recomendável para serviços de pesquisa de produção.** No entanto, pode ser útil para fins de depuração ou de desenvolvimento.
* `maxAgeInSeconds`(opcional): os navegadores usam esse valor toodetermine Olá duração (em segundos) toocache CORS respostas de simulação. Esse deve ser um inteiro não negativo. Olá maior que esse valor é Olá desempenho será melhor, mas hello mais tempo levará para efeito de tootake de alterações de política CORS. Se ele não for definido, uma duração padrão de cinco minutos será usada.

<a name="CreateUpdateIndexExample"></a>
**Exemplo de Corpo de Solicitação**

    {
      "name": "hotels",  
      "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String"},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean"},
        {"name": "smokingAllowed", "type": "Edm.Boolean"},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["hotelName"]
        }
      ]
    }

**Resposta**

Para uma solicitação bem-sucedida: "201 Criado".

Por padrão a corpo da resposta Olá conterá hello JSON para definição de índice de saudação que foi criada. Se hello `Prefer` cabeçalho de solicitação está definido muito`return=minimal`, Olá corpo de resposta estará vazio e código de status de êxito Olá será "204 sem conteúdo" em vez de "201 criado". Isso é verdadeiro independentemente se PUT ou POST foi índice de saudação toocreate usado.

**Comentários**

Atualmente, há suporte limitado para atualizações de esquema de índice. Atualmente, não há suporte às atualizações de esquema que exigem reindexação, como a alteração de tipos de campo. Embora os campos existentes não podem ser alterados ou excluídos, novos campos podem ser adicionados índice existente tooan a qualquer momento. Quando um novo campo for adicionado, todos os documentos existentes no índice Olá terão automaticamente um valor nulo para esse campo. Não há espaço de armazenamento adicional será consumido até novos documentos são adicionados toohello índice.

<a name="Suggesters"></a>

## <a name="suggesters"></a>Sugestores
recurso de sugestões de saudação na pesquisa do Azure é um recurso de consulta de preenchimento automático ou AutoCompletar, fornecendo uma lista de possíveis condições de pesquisa na entrada de cadeia de caracteres toopartial resposta inserida em uma caixa de pesquisa. Você já deve ter notado sugestões de consulta ao usar mecanismos de pesquisa da web comercial: digitando ".NET" no Bing produz uma lista de termos de ".NET 4.5", ".NET Framework 3.5", e assim por diante. Ao usar a API REST do serviço de pesquisa hello, implementar sugestões em um aplicativo de pesquisa do Azure personalizado requer o seguinte hello:

* Habilitar sugestões adicionando uma **sugestão** construção em seu índice, fornecendo nome hello, no modo de pesquisa e uma lista de campos para a qual adiantado é invocada. Por exemplo, se você especificar "cityName" como um campo de origem, digitar uma cadeia de caracteres de pesquisa parciais de "Sea" resultará em "Seattle", "Seaside" e "Seatac" (todos os três são nomes de cidades reais) oferecidos como usuário de toohello de sugestões de consulta.
* Invocar sugestões chamando Olá [API de sugestões](#Suggestions) no código do aplicativo. Normalmente, cadeias de caracteres de pesquisa parciais são enviadas toohello serviço enquanto o usuário hello está digitando uma consulta de pesquisa, e essa API retorna um conjunto de frases sugeridas.

Este artigo explica como tooconfigure uma **sugestão**. Você também deve revisar Olá [API de sugestões](#Suggestions) para obter detalhes sobre como uma sugestão é usada.

**Uso**

`Suggesters`são criados no índice hello e funcionam melhor quando usadas documentos toosuggest específico em vez de perder termos ou frases. campos de candidato Olá recomendados são títulos, nomes e outras frases relativamente curtas que podem identificar um item. Os campos repetitivos, como categorias e marcas, ou campos muito longos, como campos de comentários ou descrições, são menos eficazes.

Como parte da definição de índice Olá, você pode adicionar um único sugestão toohello `suggesters` coleção. As propriedades que definem uma sugestão incluem seguinte hello:

* `name`: nome de saudação do encarregado da sugestão hello. Você usa o nome de saudação do encarregado da sugestão Olá ao chamar hello `suggest` API.
* `searchMode`: Olá toosearch estratégia usada para frases do candidato. Olá único modo atualmente suportado é `analyzingInfixMatching`, que executa uma correspondência flexível de frases no início de saudação ou no meio de saudação das frases.
* `sourceFields`: Uma lista de um ou mais campos que são Olá origem de conteúdo Olá para obter sugestões. Somente os campos dos tipos `Edm.String` e `Collection(Edm.String)` podem ser fontes de sugestões. Somente os campos que não têm um analisador de idioma personalizado definido podem ser usados.

**Exemplo de sugestor**

Uma sugestão é parte do índice de saudação. Apenas uma sugestão pode existir em Olá `suggesters` coleção de campos da coleção na versão atual do hello, juntamente com hello e `scoringProfiles`.

        {
          "name": "hotels",
          "fields": [
             . . .
           ],
          "suggesters": [
            {
            "name": "sg",
            "searchMode": "analyzingInfixMatching",
            "sourceFields: ["hotelName", "category"]
            }
          ],
          "scoringProfiles": [
             . . .
          ]
        }

> [!NOTE]
> Se você usou a versão de visualização pública de saudação da pesquisa do Azure, `suggesters` substitui uma propriedade booliana mais antiga (`"suggestions": false`) que suporte apenas sugestões de prefixo para cadeias de caracteres curtas (de 3 a 25 caracteres). Sua substituição, `suggesters`, dá suporte a correspondência infixo que localiza os termos correspondentes no início de saudação ou no meio de saudação do conteúdo do campo, com melhor tolerância para erros em cadeias de caracteres de pesquisa. A partir da versão disponível hello, isso é agora Olá única implementação de API de sugestões de saudação. Olá antigo `suggestions` propriedade foi introduzida no `api-version=2014-07-31-Preview` continua toowork nessa versão, mas não está operacional no hello `2015-02-28` ou versões posteriores da pesquisa do Azure.
> 
> 

<a name="UpdateIndex"></a>

## <a name="update-index"></a>Atualizar o índice
Você pode atualizar um índice existente no Azure Search usando uma solicitação HTTP PUT. As atualizações podem incluir a adição de novos campos toohello esquema existente, modificando as opções de CORS e modificar perfis de pontuação. Confira [Adicionar perfis de pontuação](https://msdn.microsoft.com/library/azure/dn798928.aspx) para saber mais. Especifique o nome de Olá de saudação índice tooupdate no URI de solicitação de saudação:

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**Importante:** suporte para atualizações de esquema de índice é limitado toooperations que não requerem a recriação do índice de pesquisa de saudação. Atualmente, não há suporte às atualizações de esquema que exigem reindexação, como a alteração de tipos de campo. Novos campos podem ser adicionados a qualquer momento, embora os campos existentes não possam ser alterados nem excluídos. Olá mesmo se aplica muito`suggesters`. Novos campos podem ser adicionados sugestão tooa em campos de Olá Olá hora são adicionados, mas não não possível remover campos `suggesters` e os campos existentes não podem ser adicionados muito`suggesters`.

Ao adicionar um novo índice tooan campo, todos os documentos existentes no índice Olá terão automaticamente um valor nulo para esse campo. Não há espaço de armazenamento adicional será consumido até novos documentos são adicionados toohello índice.

**Solicitação**

HTTPS é necessário para todas as solicitações de serviço. Olá **índice de atualização** solicitação é construída usando HTTP PUT. Com PUT, o nome do índice Olá é parte da URL de saudação. Se o índice Olá não existir, ele será criado. Se já existir um índice de Olá, é atualizado toohello nova definição.

nome do índice Olá deve estar em letras minúsculas, começar com uma letra ou número, não ter barras ou pontos e ter menos de 128 caracteres. Depois de iniciar o nome do índice Olá com uma letra ou número, restante de saudação do nome hello pode incluir qualquer letra, número e traços, como Olá traços não sejam consecutivos.

`api-version=[string]` (obrigatório). versão de visualização de saudação é `api-version=2015-02-28-Preview`. Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.

**Cabeçalhos da solicitação**

Olá lista a seguir descreve hello necessárias e cabeçalhos opcionais da solicitação.

* `Content-Type`: obrigatório. Defina esta opção muito`application/json`
* `api-key`: obrigatório. Olá `api-key` é usado tooauthenticate Olá solicitação tooyour serviço de pesquisa. É um valor de cadeia de caracteres, o serviço de tooyour exclusivo. Olá **índice de atualização** solicitação deve incluir um `api-key` cabeçalho definido tooyour a chave de administração (como a chave de consulta tooa contrário).

Você também precisará Olá serviço nome tooconstruct Olá solicitação URL. Você pode obter o nome do serviço hello e `api-key` do seu painel de serviço no hello Portal do Azure. Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter ajuda de navegação de página.

**Sintaxe de corpo da solicitação**

Ao atualizar um índice existente, corpo Olá deve incluir a definição de esquema original hello, além de adicionar novos campos de hello, bem como Olá modificado perfis de pontuação, sugestões e opções de CORS, se houver. Se você não estiver modificando os perfis de pontuação hello e opções de CORS, você deve incluir originais de saudação do quando o índice de saudação foi criado. Em geral Olá melhor padrão toouse atualizações é definição de índice de saudação tooretrieve com um GET, modificá-lo e atualizá-la com PUT.

sintaxe de esquema Olá usado toocreate que um índice é reproduzido aqui por conveniência. Consulte [Criar Índice](#CreateIndex) para obter mais detalhes.

    {
      "name": (optional) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false, 
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
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
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }


**Resposta**

Para uma solicitação bem-sucedida: "204 sem Conteúdo".

Por padrão, o corpo de resposta Olá estará vazio. No entanto, se hello `Prefer` cabeçalho de solicitação está definido muito`return=representation`, corpo da resposta Olá conterá Olá JSON para definição de índice de saudação que foi atualizada. Nesse caso, o código de status de êxito Olá será "200 Okey".

**Atualizando a definição de índice com analisadores personalizados**

Quando um analisador, um criador de token, um filtro de token ou um filtro de char é definido, ele não pode ser modificado. Novos podem ser adicionados índice existente tooan somente se hello `allowIndexDowntime` sinalizador é definido tootrue na solicitação de atualização do índice hello: 

`PUT https://[search service name].search.windows.net/indexes/[index name]?api-version=[api-version]&allowIndexDowntime=true`

Observe que essa operação colocará seu índice offline pelo menos alguns segundos, fazendo com que a indexação e consulta solicita toofail. Disponibilidade de desempenho e a gravação de índice Olá pode ser afetado por vários minutos após a atualização do índice de hello, ou mais índices muito grandes.

<a name="ListIndexes"></a>

## <a name="list-indexes"></a>Listar Índices
Olá **lista índices** operação retorna uma lista de índices de saudação atualmente em seu serviço de pesquisa do Azure.

    GET https://[service name].search.windows.net/indexes?api-version=[api-version]
    api-key: [admin key]

**Solicitação**

HTTPS é necessário para todas as solicitações de serviço. Olá **lista índices** solicitação pode ser criada usando o método GET hello.

`api-version=[string]` (obrigatório). versão de visualização de saudação é `api-version=2015-02-28-Preview`. Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.

**Cabeçalhos da solicitação**

Olá lista a seguir descreve hello necessárias e cabeçalhos opcionais da solicitação.

* `api-key`: obrigatório. Olá `api-key` é usado tooauthenticate Olá solicitação tooyour serviço de pesquisa. É um valor de cadeia de caracteres, o serviço de tooyour exclusivo. Olá **lista índices** solicitação deve incluir um `api-key` chave de administração do conjunto tooan (como a chave de consulta tooa contrário).

Você também precisará Olá serviço nome tooconstruct Olá solicitação URL. Você pode obter o nome do serviço hello e `api-key` do seu painel de serviço no hello Portal do Azure. Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter ajuda de navegação de página.

**Corpo da solicitação**

Nenhuma.

**Resposta**

Código de status: 200 OK é retornado para uma resposta bem-sucedida.

Aqui está um exemplo de corpo de resposta:

    {
      "value": [
        {
          "name": "Books",
          "fields": [
            {"name": "ISBN", ...},
            ...
          ]
        },
        {
          "name": "Games",
          ...
        },
        ...
      ]
    }

Observe que você pode filtrar a resposta Olá para propriedades de saudação toojust em que você estiver interessado. Por exemplo, se você quiser apenas uma lista de nomes de índice, use Olá OData `$select` opção de consulta:

    GET /indexes?api-version=2015-02-28-Preview&$select=name

Nesse caso, resposta Olá Olá acima exemplo seria exibida da seguinte maneira:

    {
      "value": [
        {"name": "Books"},
        {"name": "Games"},
        ...
      ]
    }

Isso é uma largura de banda de toosave técnica útil se você tiver muitos índices em seu serviço de pesquisa.

<a name="GetIndex"></a>

## <a name="get-index"></a>Obter o índice
Olá **obter índice** operação obtém a definição de índice de saudação da pesquisa do Azure.

    GET https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

**Solicitação**

HTTPS é necessário para as solicitações de serviço. Olá **obter índice** solicitação pode ser criada usando o método GET hello.

Olá [nome do índice] no URI de solicitação de saudação especifica quais tooreturn de índice da coleção de índices de saudação.

`api-version=[string]` (obrigatório). versão de visualização de saudação é `api-version=2015-02-28-Preview`. Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.

**Cabeçalhos da solicitação**

Olá lista a seguir descreve hello necessárias e cabeçalhos opcionais da solicitação.

* `api-key`: Olá `api-key` é usado tooauthenticate Olá solicitação tooyour serviço de pesquisa. É um valor de cadeia de caracteres, o serviço de tooyour exclusivo. Olá **obter índice** solicitação deve incluir um `api-key` chave de administração do conjunto tooan (como a chave de consulta tooa contrário).

Você também precisará Olá serviço nome tooconstruct Olá solicitação URL. Você pode obter o nome do serviço hello e `api-key` do seu painel de serviço no hello Portal do Azure. Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter ajuda de navegação de página.

**Corpo da solicitação**

Nenhuma.

**Resposta**

Código de status: 200 OK é retornado para uma resposta bem-sucedida.

Consulte o exemplo hello JSON em [criação e atualização de um índice](#CreateUpdateIndexExample) para obter um exemplo da carga de resposta de saudação.

<a name="DeleteIndex"></a>

## <a name="delete-index"></a>Excluir o índice
Olá **Excluir índice** operação remove um índice e os documentos associados do seu serviço de pesquisa do Azure. Você pode obter o nome do índice Olá Olá no painel de serviço no portal do Azure de saudação ou Olá API. Consulte [Listar índices](#ListIndexes) para obter detalhes.

    DELETE https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

**Solicitação**

HTTPS é necessário para as solicitações de serviço. Olá **Excluir índice** solicitação pode ser criada usando o método de exclusão hello.

Olá [nome do índice] no URI de solicitação de saudação especifica quais toodelete de índice da coleção de índices de saudação.

`api-version=[string]` (obrigatório). versão de visualização de saudação é `api-version=2015-02-28-Preview`. Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.

**Cabeçalhos da solicitação**

Olá lista a seguir descreve hello necessárias e cabeçalhos opcionais da solicitação.

* `api-key`: obrigatório. Olá `api-key` é usado tooauthenticate Olá solicitação tooyour serviço de pesquisa. É um valor de cadeia de caracteres, a URL do serviço tooyour exclusivo. Olá **Excluir índice** solicitação deve incluir um `api-key` cabeçalho definido tooyour a chave de administração (como a chave de consulta tooa contrário).

Você também precisará Olá serviço nome tooconstruct Olá solicitação URL. Você pode obter o nome do serviço hello e `api-key` do seu painel de serviço no hello Portal do Azure. Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter ajuda de navegação de página.

**Corpo da solicitação**

Nenhuma.

**Resposta**

Código de status: 204 Sem Conteúdo é retornado para uma resposta bem-sucedida.

<a name="GetIndexStats"></a>

## <a name="get-index-statistics"></a>Obter estatísticas de índice
Olá **obter estatísticas de índice** operação retorna uma contagem de documento de índice atual hello, além de utilização de armazenamento da pesquisa do Azure.

    GET https://[service name].search.windows.net/indexes/[index name]/stats?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> As estatísticas de tamanho de armazenamento e contagem de documentos são coletadas a cada poucos minutos, não em tempo real. Portanto, estatísticas de hello retornadas pela API podem não refletir as alterações causadas por operações de indexação recentes.
> 
> 

**Solicitação**

HTTPS é necessário para todas as solicitações de serviço. Olá **obter estatísticas de índice** solicitação pode ser criada usando o método GET hello.

Olá [nome do índice] no URI de solicitação Olá informa Olá serviço tooreturn as estatísticas de índice para o índice especificado da saudação.

`api-version=[string]` (obrigatório). versão de visualização de saudação é `api-version=2015-02-28-Preview`. Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.

**Cabeçalhos da solicitação**

Olá lista a seguir descreve hello necessárias e cabeçalhos opcionais da solicitação.

* `api-key`: Olá `api-key` é usado tooauthenticate Olá solicitação tooyour serviço de pesquisa. É um valor de cadeia de caracteres, o serviço de tooyour exclusivo. Olá **obter estatísticas de índice** solicitação deve incluir um `api-key` chave de administração do conjunto tooan (como a chave de consulta tooa contrário).

Você também precisará Olá serviço nome tooconstruct Olá solicitação URL. Você pode obter o nome do serviço hello e `api-key` do seu painel de serviço no hello Portal do Azure. Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter ajuda de navegação de página.

**Corpo da solicitação**

Nenhuma.

**Resposta**

Código de status: 200 OK é retornado para uma resposta bem-sucedida.

corpo da resposta Hello está em Olá formato a seguir:

    {
      "documentCount": number,
      "storageSize": number (size of hello index in bytes)
    }

<a name="TestAnalyzer"></a>

## <a name="test-analyzer"></a>Analisador de teste
Olá **API analisar** mostra como um analisador quebra o texto em tokens.

    POST https://[service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**Solicitação**

HTTPS é necessário para todas as solicitações de serviço. Olá **API analisar** solicitação pode ser criada usando o método de POSTAGEM hello.

`api-version=[string]` (obrigatório). versão de visualização de saudação é `api-version=2015-02-28-Preview`. Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.

**Cabeçalhos da solicitação**

Olá lista a seguir descreve hello necessárias e cabeçalhos opcionais da solicitação.

* `api-key`: Olá `api-key` é usado tooauthenticate Olá solicitação tooyour serviço de pesquisa. É um valor de cadeia de caracteres, o serviço de tooyour exclusivo. Olá **API analisar** solicitação deve incluir um `api-key` chave de administração do conjunto tooan (como a chave de consulta tooa contrário).

Nome do índice hello e URL de solicitação de Olá Olá serviço nome tooconstruct também será necessário. Você pode obter o nome do serviço hello e `api-key` do seu painel de serviço no hello Portal do Azure. Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter ajuda de navegação de página.

**Corpo da solicitação**

    {
      "text": "Text tooanalyze",
      "analyzer": "analyzer_name"
    }

ou o

    {
      "text": "Text tooanalyze",
      "tokenizer": "tokenizer_name",
      "tokenFilters": (optional) [ "token_filter_name" ],
      "charFilters": (optional) [ "char_filter_name" ]
    }

Olá `analyzer_name`, `tokenizer_name`, `token_filter_name` e `char_filter_name` necessários toobe os nomes válidos de analisadores predefinidas ou personalizadas, tokenizers, filtros de token e filtros de char para índice de saudação. toolearn mais informações sobre o processo de saudação de análise lexical consulte [análise na pesquisa do Azure](https://aka.ms/azsanalysis).

**Resposta**

Código de status: 200 OK é retornado para uma resposta bem-sucedida.

corpo da resposta Hello está em Olá formato a seguir:

    {
      "tokens": [
        {
          "token": string (token),
          "startOffset": number (index of hello first character of hello token),
          "endOffset": number (index of hello last character of hello token),
          "position": number (position of hello token in hello input text)
        },
        ...
      ]
    }

**Analisar exemplo de API**

**Solicitação**

    {
      "text": "Text tooanalyze",
      "analyzer": "standard"
    }

**Resposta**

    {
      "tokens": [
        {
          "token": "text",
          "startOffset": 0,
          "endOffset": 4,
          "position": 0
        },
        {
          "token": "to",
          "startOffset": 5,
          "endOffset": 7,
          "position": 1
        },
        {
          "token": "analyze",
          "startOffset": 8,
          "endOffset": 15,
          "position": 2
        }
      ]
    }

- - -
<a name="DocOps"></a>

## <a name="document-operations"></a>Operações de documento
Na pesquisa do Azure, um índice é armazenado na nuvem hello e preenchido usando documentos JSON que você carregue toohello serviço. Todos os documentos de saudação que você carregar incluem corpo de saudação de seus dados de pesquisa. Documentos contêm campos, alguns dos quais são indexados em termos de pesquisa ao serem carregados. Olá `/docs` segmento de URL no hello API de pesquisa do Azure representa a coleção de saudação de documentos em um índice. Todas as operações executadas na coleção de saudação, como carregar, mesclar, excluir ou consultar documentos ocorrem no contexto de saudação de um único índice, portanto URLs de saudação para essas operações sempre começam com `/indexes/[index name]/docs` para um nome de índice fornecido.

O código do aplicativo deve gerar JSON documentos tooupload tooAzure pesquisa ou você pode usar um [indexador](https://msdn.microsoft.com/library/dn946891.aspx) tooload documentos se a fonte de dados de saudação é o banco de dados SQL ou banco de dados do Azure Cosmos. Normalmente, os índices são preenchidos por meio de um único conjunto de dados que você fornece.

Você deve planejar ter um documento para cada item que você deseja toosearch. Um aplicativo de aluguel de filmes pode ter um documento por filme, um aplicativo de vitrine pode ter um documento por SKU, um aplicativo de cursos online pode ter um documento por curso, uma empresa de pesquisa pode ter um documento para cada artigo acadêmico em seu repositório e assim por diante.

Os documentos consistem em um ou mais campos. Os campos podem conter texto indexado pelo Azure Search em termos de pesquisa, bem como valores não indexados ou que não são de texto, que podem ser usadas em filtros ou perfis de pontuação. Olá nomes, tipos de dados e recursos de pesquisa com suporte para cada campo são determinados pelo esquema de índice hello. Um dos campos de saudação em cada esquema de índice deve ser designado como uma ID e cada documento deve ter um valor para o campo de ID de saudação que identifica exclusivamente o documento no índice de saudação. Todos os outros campos de documento são opcionais e assumirá o valor nulo tooa se não especificado. Observe que valores nulos não ocupam espaço no índice de pesquisa de saudação.

Antes de poder carregar documentos, você já deve ter criado o índice de saudação no serviço de saudação. Consulte [Criar o índice](#CreateIndex) para obter detalhes sobre essa primeira etapa.

<a name="AddOrUpdateDocuments"></a>

## <a name="add-update-or-delete-documents"></a>Adicionar, Atualizar ou Excluir Documentos
Você pode carregar, mesclar, mesclar ou carregar ou excluir documentos de um índice especificado usando HTTP POST. Para um grande número de atualizações, recomenda-se o processamento em lotes de documentos (too1000 documentos por lote) ou aproximadamente 16 MB por lote.

    POST https://[service name].search.windows.net/indexes/[index name]/docs/index?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**Solicitação**

HTTPS é necessário para todas as solicitações de serviço. Você pode carregar, mesclar, mesclar ou carregar ou excluir documentos de um índice especificado usando HTTP POST.

Olá URI da solicitação inclui [nome do índice], especificando quais documentos toopost de índice. Só é possível publicar o índice de tooone documentos por vez.

`api-version=[string]` (obrigatório). versão de visualização de saudação é `api-version=2015-02-28-Preview`. Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.

**Cabeçalhos da solicitação**

Olá lista a seguir descreve hello necessárias e cabeçalhos opcionais da solicitação.

* `Content-Type`: obrigatório. Defina esta opção muito`application/json`
* `api-key`: obrigatório. Olá `api-key` é usado tooauthenticate Olá solicitação tooyour serviço de pesquisa. É um valor de cadeia de caracteres, o serviço de tooyour exclusivo. Olá **adicionar documentos** solicitação deve incluir um `api-key` cabeçalho definido tooyour a chave de administração (como a chave de consulta tooa contrário).

Você também precisará Olá serviço nome tooconstruct Olá solicitação URL. Você pode obter o nome do serviço hello e `api-key` do seu painel de serviço no hello Portal do Azure. Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter ajuda de navegação de página.

**Corpo da solicitação**

corpo de saudação da solicitação de saudação contém um ou mais toobe de documentos indexados. Os documentos são identificados por uma chave exclusiva. Cada documento está associado uma ação: carregar, mesclar, mesclar ou carregar ou excluir. Solicitações de carregamento devem incluir dados de documento hello como um conjunto de pares chave/valor.

    {
      "value": [
        {
          "@search.action": "upload (default) | merge | mergeOrUpload | delete",
          "key_field_name": "unique_key_of_document", (key/value pair for key field from index schema)
          "field_name": field_value (key/value pairs matching index schema)
            ...
        },
        ...
      ]
    }

> [!NOTE]
> As chaves de documento só podem conter letras, números, traços ("-"), sublinhados ("_") e sinais de igual ("="). Para obter mais detalhes, veja [Regras de nomenclatura](https://msdn.microsoft.com/library/azure/dn857353.aspx).
> 
> 

**Ações do documento**

* `upload`: Uma ação de carregamento é semelhante tooan "upsert" onde documento hello será inserido se for novo e atualizado/substituído se ele existir. Observe que todos os campos são substituídos no caso de atualização de saudação.
* `merge`: Merge atualiza uma existente de documento com hello especificado campos. Se o documento de saudação não existir, a mesclagem de Olá falhará. Qualquer campo que você especificar em uma mesclagem substituirá o campo de saudação existente no documento de saudação. Isso inclui campos do tipo `Collection(Edm.String)`. Por exemplo, se hello documento contém um campo "tags" com valor `["budget"]` e executar uma mesclagem com valor `["economy", "pool"]` para "tags", o valor final de saudação do campo "tags" hello será `["economy", "pool"]`. Ele **não** será `["budget", "economy", "pool"]`.
* `mergeOrUpload`: se comporta como `merge` se um documento com hello atribuída a chave já existe no índice hello. Se o documento de saudação não existir, ela se comporta como `upload` com um novo documento.
* `delete`: Excluir remove o documento especificado de saudação do índice de saudação. Observe que todos os campos que você especificar em uma `delete` operação diferente de campo de chave hello será ignorada. Se você quiser tooremove um campo individual de um documento, use `merge` em vez disso e basta definir campo Olá explicitamente muito`null`.

**Resposta**

O código de status 200 (OK) é retornado para uma resposta bem-sucedida, indicando que todos os itens foram indexados com êxito. Isso é indicado por Olá `status` propriedade sendo definida tootrue para todos os itens, bem como Olá `statusCode` propriedade sendo definida tooeither 201 (para documentos recentemente carregados) ou 200 (para documentos mesclados ou excluídos):

    {
      "value": [
        {
          "key": "unique_key_of_new_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 201
        },
        {
          "key": "unique_key_of_merged_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        },
        {
          "key": "unique_key_of_deleted_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        }
      ]
    }  

O código de status 207 (Multi-Status) será retornado quando pelo menos um item não tiver sido indexado com êxito. Itens que não tenham sido indexados possuem Olá `status` toofalse do conjunto de campos. Olá `errorMessage` e `statusCode` propriedades indicará o motivo Olá Olá erro de indexação:

    {
      "value": [
        {
          "key": "unique_key_of_document_1",
          "status": false,
          "errorMessage": "hello search service is too busy tooprocess this document. Please try again later.",
          "statusCode": 503
        },
        {
          "key": "unique_key_of_document_2",
          "status": false,
          "errorMessage": "Document not found.",
          "statusCode": 404
        },
        {
          "key": "unique_key_of_document_3",
          "status": false,
          "errorMessage": "Index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'. Please try again later.",
          "statusCode": 422
        }
      ]
    }  

Olá, a tabela a seguir explica Olá vários por documento códigos de status que podem ser retornados em resposta hello. Observe que alguns indicam problemas com solicitação hello, enquanto outros indicam as condições de erro temporário. Olá último que deve tentar novamente após um atraso.

<table style="font-size:12">
    <tr>
        <th>Código de status</th>
        <th>Significado</th>
        <th>Com nova tentativa</th>
        <th>Observações</th>
    </tr>
    <tr>
        <td>200</td>
        <td>O documento foi modificado ou excluído com êxito.</td>
        <td>n/d</td>
        <td>As operações de exclusão são <a href="https://en.wikipedia.org/wiki/Idempotence">idempotentes</a>. Ou seja, mesmo se não existir uma chave de documento no índice hello, a tentativa de uma operação de exclusão com essa chave resultará em um código de 200 status.</td>
    </tr>
    <tr>
        <td>201</td>
        <td>O documento foi criado com êxito.</td>
        <td>n/d</td>
        <td></td>
    </tr>
    <tr>
        <td>400</td>
        <td>Ocorreu um erro no documento de saudação que impediu a serem indexados.</td>
        <td>Não</td>
        <td>mensagem de erro de saudação em resposta Olá indicará o que há de errado com o documento de saudação.</td>
    </tr>
    <tr>
        <td>404</td>
        <td>documento de saudação não pode ser mesclado porque Olá recebe a chave não existe no índice de saudação.</td>
        <td>Não</td>
        <td>Esse erro não ocorre em carregamentos, uma vez que eles criam novos documentos e não ocorre em exclusões porque elas são <a href="https://en.wikipedia.org/wiki/Idempotence">idempotentes</a>.</td>
    </tr>
    <tr>
        <td>409</td>
        <td>Foi detectado um conflito de versão durante a tentativa de tooindex um documento.</td>
        <td>Sim</td>
        <td>Isso pode acontecer quando você estiver tentando Olá tooindex mesmo documento mais de uma vez simultaneamente.</td>
    </tr>
    <tr>
        <td>422</td>
        <td>índice de saudação está temporariamente indisponível porque ele foi atualizado com too'true de conjunto de sinalizador Olá 'allowIndexDowntime' '.</td>
        <td>Sim</td>
        <td></td>
    </tr>
    <tr>
        <td>503</td>
        <td>O serviço de pesquisa está temporariamente indisponível, possivelmente devido a carga de tooheavy.</td>
        <td>Sim</td>
        <td>Seu código deve aguardar antes de tentar novamente neste caso ou prolongando indisponibilidade de serviço Olá o risco.</td>
    </tr>
</table> 

**Observação**: se o seu código de cliente com frequência encontrar uma resposta 207, um motivo possível é que o sistema hello está sob carga. Você pode confirmar isso verificando Olá `statusCode` propriedade 503. Se esse for o caso de Olá, é recomendável ***limitação de solicitações de indexação***. Caso contrário, se o tráfego de indexação não diminuir, o sistema Olá pode iniciar a rejeição de todas as solicitações com 503 erros.

O código de status 429 indica que você excedeu sua cota no número de saudação de documentos por índice. Você deve criar um novo índice ou atualizar para limites de capacidade mais altos.

**Exemplo:**

    {
      "value": [
        {
          "@search.action": "upload",
          "hotelId": "1",
          "baseRate": 199.0,
          "description": "Best hotel in town",
          "description_fr": "Meilleur hôtel en ville",
          "hotelName": "Fancy Stay",
          "category": "Luxury",
          "tags": ["pool", "view", "wifi", "concierge"],
          "parkingIncluded": false,
          "smokingAllowed": false,
          "lastRenovationDate": "2010-06-27T00:00:00Z",
          "rating": 5,
          "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
        },
        {
          "@search.action": "upload",
          "hotelId": "2",
          "baseRate": 79.99,
          "description": "Cheapest hotel in town",
          "description_fr": "Hôtel le moins cher en ville",
          "hotelName": "Roach Motel",
          "category": "Budget",
          "tags": ["motel", "budget"],
          "parkingIncluded": true,
          "smokingAllowed": true,
          "lastRenovationDate": "1982-04-28T00:00:00Z",
          "rating": 1,
          "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
        },
        {
          "@search.action": "merge",
          "hotelId": "3",
          "baseRate": 279.99,
          "description": "Surprisingly expensive",
          "lastRenovationDate": null
        },
        {
          "@search.action": "delete",
          "hotelId": "4"
        }
      ]
    }
- - -
<a name="SearchDocs"></a>

## <a name="search-documents"></a>Pesquisar Documentos
Um **pesquisa** operação é emitida como uma solicitação GET ou POST e especifica os parâmetros que fornecem os critérios de saudação para seleção de documentos correspondentes.

    GET https://[service name].search.windows.net/indexes/[index name]/docs?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/search?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

**Quando toouse POST em vez de obter**

Quando você usa o HTTP GET toocall Olá **pesquisa** API, você precisa toobe ciente de que o comprimento Olá Olá URL da solicitação não pode exceder 8 KB. Isso costuma ser suficiente para a maioria dos aplicativos. No entanto, alguns aplicativos geram consultas muito grandes ou expressões de filtro OData. Para esses aplicativos, usar HTTP POST é uma opção melhor, pois permite filtros e consultas maiores que o GET. Com o POST, o número de saudação de cláusulas em uma consulta ou termos Olá limitar fator, não o tamanho de saudação de consulta brutos de saudação desde que o limite de tamanho de solicitação de saudação do POST é aproximadamente 16 MB.

> [!NOTE]
> Mesmo que o limite de tamanho de solicitação POST Olá for muito grande, as consultas de pesquisa e as expressões de filtro não podem ser arbitrariamente complexas. Confira a [Sintaxe de consulta Lucene](https://msdn.microsoft.com/library/mt589323.aspx) e a [Sintaxe de expressão OData](https://msdn.microsoft.com/library/dn798921.aspx) para obter mais informações sobre as limitações de complexidade de consulta e filtro de pesquisa.
> 
> 

**Solicitação**

HTTPS é necessário para as solicitações de serviço. Olá **pesquisa** solicitação pode ser criada usando Olá GET ou métodos POST.

URI de solicitação de saudação especifica quais tooquery de índice, para todos os documentos que correspondam a parâmetros de saudação. Parâmetros são especificados na cadeia de caracteres de consulta de saudação no caso de saudação de solicitações GET e na solicitação Olá solicitações de corpo no caso de saudação de POSTAGEM.

Como uma prática recomendada, ao criar solicitações GET, lembre-se muito[a codificação de URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) consulta específica parâmetros ao chamar hello API REST diretamente. Para operações de **Pesquisa** , isso inclui:

* `$filter`
* `facet`
* `highlightPreTag`
* `highlightPostTag`
* `search`
* `moreLikeThis`

Codificação de URL é recomendada apenas nos Olá acima parâmetros de consulta. Se você inadvertidamente a codificação de URL hello cadeia de caracteres de consulta inteira (tudo após Olá?), as solicitações são interrompidas.

Além disso, a codificação de URL só é necessária ao chamar hello API REST diretamente usando obter. Nenhuma codificação de URL é necessária ao chamar **pesquisa** usando POST, ou ao usar o hello [biblioteca cliente .NET](https://msdn.microsoft.com/library/dn951165.aspx), que trata de codificação de URL para você.

<a name="SearchQueryParameters"></a>
**Parâmetros de consulta**

**Search** aceita vários parâmetros que fornecem critérios de consulta e especificam o comportamento da pesquisa. Você fornecer esses parâmetros na URL Olá cadeia de caracteres de consulta ao chamar **pesquisa** por meio de GET e como propriedades JSON no corpo da solicitação Olá ao chamar **pesquisa** por meio de POST. sintaxe de saudação para alguns parâmetros é ligeiramente diferente entre GET e POST. Essas diferenças são indicadas, como aplicável, abaixo:

`search=[string]`(opcional) - Olá toosearch de texto para. Todos os campos `searchable` são pesquisados por padrão, a menos que `searchFields` sejam especificados. Ao pesquisar `searchable` campos, Olá texto de pesquisa é indexado para vários termos podem ser separados por espaços em branco (por exemplo: `search=hello world`). toomatch qualquer termo, use `*` (Isso pode ser útil para consultas de filtro booliano). Omitir esse parâmetro tem o mesmo efeito que defini-lo muito de saudação`*`. Consulte [sintaxe de consulta simples](https://msdn.microsoft.com/library/dn798920.aspx) para obter informações específicas sobre a sintaxe de pesquisa de saudação.

* **Observação**: resultados Olá às vezes podem ser surpreendentes ao consultar sobre `searchable` campos. tokenizer Olá inclui lógica toohandle casos comuns tooEnglish texto como apóstrofes, vírgulas nos números, etc. Por exemplo, `search=123,456` corresponderá a um único termo 123,456, em vez de termos individuais de saudação 123 e 456, já que as vírgulas são usadas como separadores de milhar para números grandes em inglês. Por esse motivo, recomendamos o uso de espaço em branco em vez de termos de tooseparate de pontuação em Olá `search` parâmetro.

`searchMode=any|all`(opcional, padrão é muito`any`): se qualquer ou todos os termos de pesquisa Olá devem ser iguais em ordem toocount Olá documento uma correspondência.

`searchFields=[string]`(opcional) - lista de saudação do toosearch de nomes de campos separados por vírgulas para Olá o texto especificado. Os campos de destino devem ser marcados como `searchable`.

`queryType=simple|full`(opcional, padrão é muito`simple`) - ao definir o texto de pesquisa muito "simples" é interpretado usando uma linguagem de consulta simples que permite símbolos, como +, * e "". As consultas são avaliadas em todos os campos pesquisáveis (ou nos campos indicados em `searchFields`) em cada documento por padrão. Quando o tipo de consulta de saudação está definido muito`full` texto de pesquisa é interpretado usando linguagem de consulta do Lucene Olá que permite que as pesquisas de campo específicos e ponderadas. Consulte [sintaxe de consulta simples](https://msdn.microsoft.com/library/dn798920.aspx) e [sintaxe de consulta do Lucene](https://msdn.microsoft.com/library/mt589323.aspx) para obter informações específicas sobre sintaxes de pesquisa de saudação. 

> [!NOTE]
> Intervalo de pesquisa no hello Lucene, não há suporte para a linguagem de consulta em favor $filter que oferece funcionalidade semelhante.
> 
> 

`moreLikeThis=[key]` (opcional) **Importante:** esse recurso só está disponível na `2015-02-28-Preview`. Essa opção não pode ser usada em uma consulta que contém o parâmetro de pesquisa de texto de saudação, `search=[string]`. Olá `moreLikeThis` parâmetro localiza os documentos que são semelhantes documento toohello especificado pela chave do documento hello. Quando uma solicitação de pesquisa é feita com `moreLikeThis`, uma lista de termos de pesquisa é gerada com base em frequência hello e raridade termos no documento de origem de saudação. Esses termos são usado toomake Olá solicitação. Por padrão, Olá conteúdo de todos os `searchable` campos serão considerados, a menos que `searchFields` é usado toorestrict quais campos são pesquisados.  

`$skip=#`(opcional) - número de saudação de pesquisa resulta tooskip; Não pode ser superior a 100.000. Se você precisar tooscan documentos em sequência, mas não é possível usar `$skip` devido a limitação de toothis, considere o uso de `$orderby` em uma chave totalmente ordenada e `$filter` com um intervalo de consulta em vez disso.

> [!NOTE]
> Ao chamar **Pesquisa** usando POST, esse parâmetro será chamado de `skip`, em vez de `$skip`.
> 
> 

`$top=#`(opcional) - número de saudação de pesquisa resulta tooretrieve. Isso pode ser usado em conjunto com `$skip` tooimplement cliente paginação de resultados da pesquisa.

> [!NOTE]
> Ao chamar **Pesquisa** usando POST, esse parâmetro será chamado de `top`, em vez de `$top`.
> 
> 

`$count=true|false`(opcional, padrão é muito`false`)-Especifica se toofetch Olá contagem total de resultados. É Olá contagem de todos os documentos que correspondam a saudação `search` e `$filter` parâmetros, ignorando `$top` e `$skip`. Definir esse valor muito`true` pode ter um impacto de desempenho. Observe que a contagem de saudação retornada é uma aproximação.

> [!NOTE]
> Ao chamar **Pesquisa** usando POST, esse parâmetro será chamado de `count`, em vez de `$count`.
> 
> 

`$orderby=[string]`(opcional) - uma lista de expressões separadas por vírgulas toosort Olá resultados por. Cada expressão pode ser um nome de campo ou uma chamada toohello `geo.distance()` função. Cada expressão pode ser seguido por `asc` tooindicated em ordem crescente e `desc` tooindicate em ordem decrescente. saudação padrão é a ordem crescente. As ligações são rompidas pelas pontuações de correspondência de saudação de documentos. Se nenhum `$orderby` for especificado, ordem de classificação saudação padrão é decrescente pela pontuação de correspondência do documento. Há um limite de 32 cláusulas para `$orderby`.

> [!NOTE]
> Ao chamar **Pesquisa** usando POST, esse parâmetro será chamado de `orderby`, em vez de `$orderby`.
> 
> 

`$select=[string]`(opcional) - uma lista de campos separados por vírgula tooretrieve. Se não for especificado, todos os campos marcados como recuperáveis no esquema de saudação são incluídos. Você pode solicitar explicitamente todos os campos ao definir esse parâmetro muito`*`.

> [!NOTE]
> Ao chamar **Pesquisa** usando POST, esse parâmetro será chamado de `select`, em vez de `$select`.
> 
> 

`facet=[string]`(zero ou mais) - toofacet um campo por. Opcionalmente, cadeia de caracteres de saudação pode conter facetas de saudação toocustomize parâmetros expressada como separados por vírgula `name:value` pares. Os parâmetros válidos são:

* `count` (número máximo de termos de faceta; o padrão é 10). Não há nenhum máximo, mas os valores mais altos incorrem em uma penalidade de desempenho correspondente, especialmente se o campo Facetado Olá contiver um grande número de termos exclusivos.
  * Por exemplo: `facet=category,count:5` obtém Olá principais cinco categorias nos resultados da faceta.  
  * **Observação**: se hello `count` parâmetro for menor que o número de saudação de termos exclusivos, Olá resultados podem não ser precisos. Isso é devido a maneira toohello consultas de faceta são distribuídas em fragmentos. Aumentar `count` geralmente aumenta Olá precisão Olá das contagens de termos, mas a um custo de desempenho.
* `sort`(um dos `count` toosort *decrescente* por contagem, `-count` toosort *crescente* por contagem, `value` toosort *crescente* por valor, ou `-value` toosort *decrescente* por valor)
  * Por exemplo: `facet=category,count:3,sort:count` obtém Olá três categorias principais nos resultados da faceta em ordem decrescente pelo número de saudação de documentos com o nome de cada cidade. Por exemplo, se três categorias de saudação principais forem orçamento, Motel e luxo e orçamento tiver 5 ocorrências, Motel tiver 6 e luxo tiver 4, em seguida, hello buckets será em ordem Olá Motel, orçamento, luxo.
  * Por exemplo: `facet=rating,sort:-value` produz todas as classificações possíveis, em ordem decrescente por valor. Por exemplo, se as classificações de saudação são de 1 too5, Olá buckets são ordenados 5, 4, 3, 2, 1, independentemente de quantos documentos correspondem cada classificação.
* `values` (valores numéricos delimitados por barras verticais ou valores `Edm.DateTimeOffset` que especificam um conjunto dinâmico de valores de entrada de faceta)
  * Por exemplo: `facet=baseRate,values:10|20` produz três buckets: um para a taxa de base 0 backup toobut não incluindo, 10, um para 10 backup toobut não incluindo, 20 e um para 20 ou superior.
  * Por exemplo: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` produz duas classificações: uma para hotéis reformados antes de fevereiro de 2010 e outra para hotéis reformados em ou depois de 1º de fevereiro de 2010.
* `interval` (intervalo inteiro maior que 0 para números ou `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` para valores de tempo de data)
  * Por exemplo: `facet=baseRate,interval:100` produz classificações com base em intervalos de taxa de base de tamanho 100. Por exemplo, se as taxas de base estiverem todas entre US$ 60 e US$ 600, haverá classificações para 0-100, 100-200, 200-300, 300-400, 400-500 e 500-600.
  * Por exemplo: `facet=lastRenovationDate,interval:year` produz uma classificação para cada ano em que os hotéis foram reformados.
* `timeoffset` ([+-]hh:mm, [+-]hhmm ou [+-]hh) `timeoffset` é opcional. Só podem ser combinada com hello `interval` opção e somente quando aplicada tooa campo do tipo `Edm.DateTimeOffset`. valor de saudação especifica tooaccount de deslocamento de hora Olá UTC na configuração de limites de tempo.
  * Por exemplo: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` usa Olá limites de dia que inicia em UTC 01:00:00 (meia-noite no fuso horário Olá destino)
* **Observação**: `count` e `sort` podem ser combinados em Olá mesma especificação de faceta, mas eles não podem ser combinados com `interval` ou `values`, e `interval` e `values` não podem ser combinados.
* **Observação**: as facetas de intervalo de data e hora serão calculadas com base na hora UTC, caso `timeoffset` não seja especificado. Por exemplo: para `facet=lastRenovationDate,interval:day`, limites de dia de saudação inicia às 00:00:00 UTC. 

> [!NOTE]
> Ao chamar **Pesquisa** usando POST, esse parâmetro será chamado de `facets`, em vez de `facet`. Além disso, especifique-o como uma matriz JSON de cadeias de caracteres em que cada cadeia é uma expressão de faceta separada.
> 
> 

`$filter=[string]` (opcional) ‒ uma expressão de pesquisa estruturada na sintaxe de OData padrão.

> [!NOTE]
> Ao chamar **Pesquisa** usando POST, esse parâmetro será chamado de `filter`, em vez de `$filter`.
> 
> 

`highlight=[string]` (opcional) ‒ realça um conjunto de nomes de campo separados por vírgulas usado para realçar ocorrências. Somente campos `searchable` podem ser usados para realçar ocorrências.

`highlightPreTag=[string]`(opcional, padrão é muito`<em>`) - uma cadeia de caracteres que precede toohit destaques. Deve ser definida com `highlightPostTag`.

> [!NOTE]
> Ao chamar **pesquisa** usando GET, os caracteres reservados na URL de saudação devem ser codificados por cento (por exemplo, % 23, em vez de #).
> 
> 

`highlightPostTag=[string]`(opcional, padrão é muito`</em>`)-uma marca de cadeia de caracteres que anexa toohit destaques. Deve ser definida com `highlightPreTag`.

> [!NOTE]
> Ao chamar **pesquisa** usando GET, os caracteres reservados na URL de saudação devem ser codificados por cento (por exemplo, % 23, em vez de #).
> 
> 

`scoringProfile=[string]`(opcional) - nome hello uma pontuação tooevaluate de perfil corresponde pontuações para documentos correspondentes nos resultados da ordem toosort hello.

`scoringParameter=[string]`(zero ou mais) - indica valores hello para cada parâmetro definido em uma função de pontuação (por exemplo, `referencePointParameter`) usando o formato de saudação `name-value1,value2,...`.

* Por exemplo, se o perfil de pontuação de saudação define uma função com um parâmetro chamado "mylocation" opção de cadeia de caracteres de consulta de saudação seria `&scoringParameter=mylocation--122.2,44.8`. traço primeiro Olá separa o nome de saudação da lista de valores hello, enquanto o traço segundo Olá faz parte do primeiro valor de saudação (longitude neste exemplo).
* Para parâmetros de pontuação, como marca de aumento que pode conter vírgulas, escape qualquer esses valores na lista de saudação usando aspas simples. Se os próprios valores hello contiverem aspas, você pode reservá-los ao duplicar.
  * Por exemplo, se você tiver uma marca de aumento parâmetro chamado "mytag" e você desejar tooboost na marca de saudação valores "Olá, o ' Brien" e "Smith" consulta Olá opção de cadeia de caracteres seria `&scoringParameter=mytag-'Hello, O''Brien',Smith`. Observe que as aspas são necessárias apenas para os valores que contêm vírgulas.

> [!NOTE]
> Ao chamar **Pesquisa** usando POST, esse parâmetro será chamado de `scoringParameters`, em vez de `scoringParameter`. Além disso, especifique-o como uma matriz de cadeias de caracteres JSON, na qual cada cadeia é um par de nome `name-values` .
> 
> 

`minimumCoverage`(opcional, padrão é too100) - um número entre 0 e 100 que indica a porcentagem saudação do índice de saudação que deve ser abordada por uma consulta de pesquisa na ordem para Olá consulta toobe relatados como sucesso. Por padrão, o índice inteiro Olá deve estar disponível ou `Search` retornará o código de status HTTP 503. Se você definir `minimumCoverage` e `Search` for bem-sucedida, ela retornará HTTP 200 e incluir um `@search.coverage` valor na resposta de saudação indicando a porcentagem de saudação do índice de saudação que foi incluído na consulta de saudação.

> [!NOTE]
> Definir esse valor do parâmetro tooa menor que 100 pode ser útil para garantir a disponibilidade de pesquisa mesmo para os serviços com apenas uma réplica. No entanto, nem todos os documentos correspondentes são garantia toobe presente nos resultados da pesquisa hello. Se lembre-se de pesquisa é mais importante do aplicativo tooyour de disponibilidade, é melhor tooleave `minimumCoverage` com seu valor padrão de 100.
> 
> 

`api-version=[string]` (obrigatório). versão de visualização de saudação é `api-version=2015-02-28-Preview`. Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.

Observação: Para essa operação, Olá `api-version` é especificado como um parâmetro de consulta na URL de saudação independentemente se você chamar **pesquisa** com GET ou POST.

**Cabeçalhos da solicitação**

Olá lista a seguir descreve hello necessárias e cabeçalhos opcionais da solicitação.

* `api-key`: Olá `api-key` é usado tooauthenticate Olá solicitação tooyour serviço de pesquisa. É um valor de cadeia de caracteres, a URL do serviço tooyour exclusivo. Olá **pesquisa** solicitação pode especificar uma chave de administração ou a chave de consulta para `api-key`.

Você também precisará Olá serviço nome tooconstruct Olá solicitação URL. Você pode obter o nome do serviço hello e `api-key` do seu painel de serviço no hello Portal do Azure. Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter ajuda de navegação de página.

**Corpo da solicitação**

Para GET: Nenhum.

Para POST:

    {
      "count": true | false (default),
      "facets": [ "facet_expression_1", "facet_expression_2", ... ],
      "filter": "odata_filter_expression",
      "highlight": "highlight_field_1, highlight_field_2, ...",
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 100),
      "moreLikeThis": "document_key" (mutually exclusive with "search" parameter),
      "orderby": "orderby_expression",
      "scoringParameters": [ "scoring_parameter_1", "scoring_parameter_2", ... ],
      "scoringProfile": "scoring_profile_name",
      "search": "simple_query_expression",
      "searchFields": "field_name_1, field_name_2, ...",
      "searchMode": "any" (default) | "all",
      "select": "field_name_1, field_name_2, ...",
      "skip": # (default 0),
      "top": #
    }

**Continuação de respostas de pesquisa parciais**

Às vezes, pesquisa do Azure não pode retornar que todos os Olá solicitada resulta em uma única resposta de pesquisa. Isso pode ocorrer por diferentes motivos, por exemplo, quando a consulta Olá solicita muitos documentos não especificando `$top` ou especificando um valor para `$top` que é muito grande. Nesses casos, a pesquisa do Azure incluirá Olá `@odata.nextLink` anotação no corpo de resposta Olá e também `@search.nextPageParameters` se fosse uma solicitação POST. Você pode usar valores de saudação do tooformulate anotações outra pesquisa solicitação tooget Olá próxima parte da resposta da pesquisa hello. Isso é chamado de um ***continuação*** de solicitação de pesquisa original hello e hello anotações são geralmente chamadas ***tokens de acompanhamento***. Consulte [exemplo hello abaixo](#SearchResponse) para obter detalhes sobre a sintaxe de saudação dessas anotações e onde eles aparecem no corpo de resposta de saudação. 

os motivos Olá porque a pesquisa do Azure pode retornar tokens de acompanhamento são toochange específicos de implementação e o assunto. Clientes robustos devem sempre ser toohandle pronto casos em que são retornados documentos menos que o esperado e um token de continuação é incluído toocontinue recuperar documentos. Também Observe que você deve usar Olá mesmo método HTTP a solicitação original Olá em ordem toocontinue. Por exemplo, se você tiver enviado uma solicitação GET, quaisquer solicitações de continuação que você enviar também deverão usar GET (e da mesma forma para POST).

<a name="SearchResponse"></a>
**Resposta**

Código de status: 200 OK é retornado para uma resposta bem-sucedida.

    {
      "@odata.count": # (if $count=true was provided in hello query),
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "@search.facets": { (if faceting was specified in hello query)
        "facet_field": [
          {
            "value": facet_entry_value (for non-range facets),
            "from": facet_entry_value (for range facets),
            "to": facet_entry_value (for range facets),
            "count": number_of_documents
          }
        ],
        ...
      },
      "@search.nextPageParameters": { (request body toofetch hello next page of results if not all results could be returned in this response and Search was called with POST)
        "count": ... (value from request body if present),
        "facets": ... (value from request body if present),
        "filter": ... (value from request body if present),
        "highlight": ... (value from request body if present),
        "highlightPreTag": ... (value from request body if present),
        "highlightPostTag": ... (value from request body if present),
        "minimumCoverage": ... (value from request body if present),
        "moreLikeThis": ... (value from request body if present),
        "orderby": ... (value from request body if present),
        "scoringParameters": ... (value from request body if present),
        "scoringProfile": ... (value from request body if present),
        "search": ... (value from request body if present),
        "searchFields": ... (value from request body if present),
        "searchMode": ... (value from request body if present),
        "select": ... (value from request body if present),
        "skip": ... (page size plus value from request body if present),
        "top": ... (value from request body if present minus page size),
      },
      "value": [
        {
          "@search.score": document_score (if a text query was provided),
          "@search.highlights": {
            field_name: [ subset of text, ... ],
            ...
          },
          key_field_name: document_key,
          field_name: field_value (retrievable fields or specified projection),
          ...
        },
        ...
      ],
      "@odata.nextLink": (URL toofetch hello next page of results if not all results could be returned in this response; Applies tooboth GET and POST)
    }

**Exemplos:**

Você pode encontrar exemplos adicionais no hello [sintaxe de expressão do OData para pesquisa do Azure](https://msdn.microsoft.com/library/azure/dn798921.aspx) página.

1)    Saudação de pesquisa índice classificado em ordem decrescente por data.

    GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }

2)    Em uma pesquisa de faceta, pesquise o índice de saudação e recupere facetas para categorias, classificação, marcas, bem como os itens com baseRate em intervalos específicos:

    GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }

3)    Usando um filtro, limitar resultados de consulta de faceta anterior Olá depois Olá usuário clica em classificação 3 e a categoria "Motel":

    GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }

4) Em uma pesquisa facetada, definir um limite superior para termos exclusivos retornados em uma consulta. saudação padrão é 10, mas você pode aumentar ou diminuir esse valor usando Olá `count` parâmetro hello `facet` atributo:

    GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }

5)    Saudação de pesquisa índice de campos específicos; Por exemplo, um campo específico do idioma:

    GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }

6) Saudação de índice em vários campos de pesquisa. Por exemplo, você pode armazenar e Olá de campos de pesquisa de consulta em vários idiomas, tudo isso no mesmo índice.  Se as descrições de inglês e francês coexistam em Olá mesmo documento, você pode retornar hello em qualquer ou todos os resultados da consulta:

    GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }

Observe que você pode consultar apenas um índice por vez. Não crie vários índices para cada idioma, a menos que você planejar tooquery um por vez.

7)    Paginação – obter Olá 1ª página de itens (o tamanho da página é 10):

    GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }

8)    Paginação – página de 2º Get hello de itens (o tamanho da página é 10):

    GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }

9)    Recuperar um conjunto específico de campos:

    GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }

10)  Recupere documentos que correspondem a uma expressão de filtro específica:

    GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }

11) Pesquise o índice de saudação e retorne fragmentos com realces de ocorrências

    GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }

12) Pesquise o índice de saudação e retorne documentos classificados do toofarther mais próximo para fora do local de referência

    GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }

13) Pesquisa Olá índice supondo que não há é um perfil de pontuação chamado "geo" com duas funções de pontuação de distância, uma definição de um parâmetro chamada "currentLocation" e uma definição de um parâmetro chamado "lastLocation"

    GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }

14) Localizar documentos no índice de saudação usando [sintaxe de consulta simples](https://msdn.microsoft.com/library/dn798920.aspx). Esta consulta retorna hotéis onde os campos de pesquisa contêm Olá termos "conforto" e "local", mas não "motel":

    GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }

Observe o uso de saudação do `searchMode=all` acima. Incluindo esse parâmetro substitui o padrão de saudação do `searchMode=any`, garantindo que `-motel` significa "AND NOT" em vez de "OR NOT". Sem `searchMode=all`, você obtém "OR NOT" que expande em vez de restringir os resultados da pesquisa, e isso pode ser contrário à intuição toosome usuários.

15) Localizar documentos no índice de saudação usando [sintaxe de consulta do lucene](https://msdn.microsoft.com/library/mt589323.aspx). Essa consulta retorna hotéis onde o campo de categoria de saudação contém termo hello "budget" e campos de pesquisa todos os que contêm a frase hello "recentemente renovado". Documentos que contêm a frase hello "recentemente renovado" são com classificação mais alta como resultado do valor de aumento de termo hello (3)

    GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }

<a name="LookupAPI"></a>

## <a name="lookup-document"></a>Procurar documento
Olá **pesquisar documento** operação recupera um documento da pesquisa do Azure. Isso é útil quando um usuário clica em um resultado de pesquisa específico e desejar toolook detalhes específicos sobre esse documento.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/[key]?[query parameters]
    api-key: [admin or query key]

**Solicitação**

HTTPS é necessário para as solicitações de serviço. Olá **pesquisar documento** solicitação pode ser construída da seguinte maneira.

    GET /indexes/[index name]/docs/key?[query parameters]

Como alternativa, você pode usar a sintaxe tradicional do OData Olá para pesquisa de chave:

    GET /indexes('[index name]')/docs('[key]')?[query parameters]

Olá URI da solicitação inclui um [nome do índice] e [chave], especificando quais tooretrieve documento de índice que. Você pode obter apenas um documento por vez. Use **pesquisa** tooget vários documentos em uma única solicitação.

**Parâmetros de consulta**

`$select=[string]`(opcional) - uma lista de campos separados por vírgula tooretrieve. Se não for especificado ou definido muito`*`, todos os campos marcados como recuperáveis no esquema de saudação são incluídos na projeção de saudação.

`api-version=[string]` (obrigatório). versão de visualização de saudação é `api-version=2015-02-28-Preview`. Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.

Observação: Para essa operação, Olá `api-version` é especificado como um parâmetro de consulta.

**Cabeçalhos da solicitação**

Olá lista a seguir descreve hello necessárias e cabeçalhos opcionais da solicitação.

* `api-key`: Olá `api-key` é usado tooauthenticate Olá solicitação tooyour serviço de pesquisa. É um valor de cadeia de caracteres, a URL do serviço tooyour exclusivo. Olá **pesquisar documento** solicitação pode especificar uma chave de administração ou a chave de consulta para `api-key`.

Você também precisará Olá serviço nome tooconstruct Olá solicitação URL. Você pode obter o nome do serviço hello e `api-key` do seu painel de serviço no hello Portal do Azure. Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter ajuda de navegação de página.

**Corpo da solicitação**

Nenhuma.

**Resposta**

Código de status: 200 OK é retornado para uma resposta bem-sucedida.

    {
      field_name: field_value (fields matching hello default or specified projection)
    }

**Exemplo**

Pesquisar documento hello que tem a chave '2'

    GET /indexes/hotels/docs/2?api-version=2015-02-28-Preview

Pesquisar documento hello que tem a chave '3' usando a sintaxe do OData:

    GET /indexes('hotels')/docs('3')?api-version=2015-02-28-Preview

<a name="CountDocs"></a>

## <a name="count-documents"></a>Contar documentos
Olá **contar documentos** operação recupera uma contagem do número de saudação de documentos em um índice de pesquisa. Olá `$count` sintaxe é parte da saudação protocolo OData.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/$count?api-version=[api-version]
    Accept: text/plain
    api-key: [admin or query key]

**Solicitação**

HTTPS é necessário para as solicitações de serviço. Olá **contar documentos** solicitação pode ser criada usando o método GET hello.

Olá [nome do índice] no URI de solicitação Olá informa Olá serviço tooreturn uma contagem de todos os itens na coleção de documentos de saudação do índice especificado da saudação.

`api-version=[string]` (obrigatório). versão de visualização de saudação é `api-version=2015-02-28-Preview`. Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.

**Cabeçalhos da solicitação**

Olá lista a seguir descreve hello necessárias e cabeçalhos opcionais da solicitação.

* `Accept`: Esse valor deve ser definido muito`text/plain`.
* `api-key`: Olá `api-key` é usado tooauthenticate Olá solicitação tooyour serviço de pesquisa. É um valor de cadeia de caracteres, a URL do serviço tooyour exclusivo. Olá **contar documentos** solicitação pode especificar uma chave de administração ou a chave de consulta para `api-key`.

Você também precisará Olá serviço nome tooconstruct Olá solicitação URL. Você pode obter o nome do serviço hello e `api-key` do seu painel de serviço no hello Portal do Azure. Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter ajuda de navegação de página.

**Corpo da solicitação**

Nenhuma.

**Resposta**

Código de status: 200 OK é retornado para uma resposta bem-sucedida.

corpo da resposta Olá contém o valor de contagem de saudação como um inteiro em texto sem formatação.

<a name="Suggestions"></a>

## <a name="suggestions"></a>Sugestões
Olá **sugestões** operação recupera as sugestões com base na entrada de pesquisa parcial. Ela é normalmente usada em sugestões de preenchimento automático pesquisa caixas tooprovide como os usuários inserem termos de pesquisa.

Solicitações de sugestões focalizam a sugestão de documentos de destino, para que Olá sugerido de texto pode ser repetido se vários documentos de candidato correspondem Olá mesmo entrada de pesquisa. Você pode usar `$select` tooretrieve outros documentos campos (incluindo a chave de documento hello) para que você possa determinar qual documento é a fonte Olá para cada sugestão.

Uma operação **Suggestions** é emitida como uma solicitação GET ou POST.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/suggest?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/suggest?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

**Quando toouse POST em vez de obter**

Quando você usa o HTTP GET toocall Olá **sugestões** API, você precisa toobe ciente de que o comprimento Olá Olá URL da solicitação não pode exceder 8 KB. Isso costuma ser suficiente para a maioria dos aplicativos. No entanto, alguns aplicativos geram consultas muito grandes, especificamente expressões de filtro OData. Para esses aplicativos, usar HTTP POST é uma opção melhor, pois permite filtros maiores que o GET. Com o POST, Olá número cláusulas em um filtro é fator limitante hello, Olá não tamanho da cadeia de caracteres de filtro bruto Olá desde que o limite de tamanho de solicitação de saudação do POST é aproximadamente 16 MB.

> [!NOTE]
> Mesmo que o limite de tamanho de solicitação POST Olá for muito grande, as expressões de filtro não podem ser arbitrariamente complexas. Confira [Sintaxe de expressão OData](https://msdn.microsoft.com/library/dn798921.aspx) para obter mais informações sobre as limitações de complexidade de filtro.
> 
> 

**Solicitação**

HTTPS é necessário para as solicitações de serviço. Olá **sugestões** solicitação pode ser criada usando Olá GET ou métodos POST.

URI de solicitação de saudação especifica o nome de saudação do hello índice tooquery. Parâmetros, como o termo de pesquisa de entrada parcial hello, são especificados na cadeia de caracteres de consulta de saudação no caso de saudação de solicitações GET e na solicitação Olá solicitações de corpo no caso de saudação de POSTAGEM.

Como uma prática recomendada, ao criar solicitações GET, lembre-se muito[a codificação de URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) consulta específica parâmetros ao chamar hello API REST diretamente. Para as operações **Sugestões** , isso inclui:

* `$filter`
* `highlightPreTag`
* `highlightPostTag`
* `search`

Codificação de URL é recomendada apenas nos Olá acima parâmetros de consulta. Se você inadvertidamente a codificação de URL hello cadeia de caracteres de consulta inteira (tudo após Olá?), as solicitações são interrompidas.

Além disso, a codificação de URL só é necessária ao chamar hello API REST diretamente usando obter. Nenhuma codificação de URL é necessária ao chamar **sugestões** usando POST, ou ao usar o hello [biblioteca cliente .NET](https://msdn.microsoft.com/library/dn951165.aspx), que trata de codificação de URL para você.

**Parâmetros de consulta**

**Suggestions** aceita vários parâmetros que fornecem critérios de consulta e também especificam o comportamento da pesquisa. Você fornecer esses parâmetros na URL Olá cadeia de caracteres de consulta ao chamar **sugestões** por meio de GET e como propriedades JSON no corpo da solicitação Olá ao chamar **sugestões** por meio de POST. sintaxe de saudação para alguns parâmetros é ligeiramente diferente entre GET e POST. Essas diferenças são indicadas, como aplicável, abaixo:

`search=[string]`-Olá consultas de pesquisa de texto toouse toosuggest. Deve ter pelo menos 1 e não mais que 100 caracteres.

`highlightPreTag=[string]`(opcional) - uma marca de cadeia de caracteres que precede toosearch ocorrências. Deve ser definida com `highlightPostTag`.

> [!NOTE]
> Ao chamar **sugestões** usando GET, os caracteres reservados na URL de saudação devem ser codificados por cento (por exemplo, % 23, em vez de #).
> 
> 

`highlightPostTag=[string]`(opcional) - uma marca de cadeia de caracteres que anexa toosearch ocorrências. Deve ser definida com `highlightPreTag`.

> [!NOTE]
> Ao chamar **sugestões** usando GET, os caracteres reservados na URL de saudação devem ser codificados por cento (por exemplo, % 23, em vez de #).
> 
> 

`suggesterName=[string]`-nome de saudação da sugestão, Olá conforme especificado no hello `suggesters` coleção que faz parte da definição de índice de saudação. Um `suggester` determina quais campos são examinados em busca de termos de consulta sugeridos. Consulte [Sugestores](#Suggesters) para obter detalhes.

`fuzzy=[boolean]`(opcional, padrão = false)-quando definido tootrue essa API encontrará sugestões mesmo se houver um caractere ausente ou substituído no texto de pesquisa de saudação. Embora isso proporcione uma experiência melhor em alguns cenários, prejudica o desempenho, pois pesquisas com sugestões difusas são mais lentas e consumem mais recursos.

`searchFields=[string]`(opcional) - lista de saudação do toosearch de nomes de campos separados por vírgulas para hello especificada texto de pesquisa. Os campos de destino devem ser habilitados para sugestões.

`$top=#`(opcional, padrão = 5)-Olá número de sugestões tooretrieve. Deve ser um número entre 1 e 100.

> [!NOTE]
> Ao chamar **Suggestions** usando POST, esse parâmetro será chamado de `top` em vez de `$top`.
> 
> 

`$filter=[string]`(opcional) - uma expressão que filtra os documentos Olá considerados para obter sugestões.

> [!NOTE]
> Ao chamar **Suggestions** usando POST, esse parâmetro será chamado de `filter` em vez de `$filter`.
> 
> 

`$orderby=[string]`(opcional) - uma lista de expressões separadas por vírgulas toosort Olá resultados por. Cada expressão pode ser um nome de campo ou uma chamada toohello `geo.distance()` função. Cada expressão pode ser seguido por `asc` tooindicated em ordem crescente e `desc` tooindicate em ordem decrescente. saudação padrão é a ordem crescente. Há um limite de 32 cláusulas para `$orderby`.

> [!NOTE]
> Ao chamar **Suggestions** usando POST, esse parâmetro será chamado de `orderby` em vez de `$orderby`.
> 
> 

`$select=[string]`(opcional) - uma lista de campos separados por vírgula tooretrieve. Se não for especificado, Olá apenas a chave de documento e texto de sugestão é retornado. Você pode solicitar explicitamente todos os campos ao definir esse parâmetro muito`*`.

> [!NOTE]
> Ao chamar **Suggestions** usando POST, esse parâmetro será chamado de `select` em vez de `$select`.
> 
> 

`minimumCoverage`(opcional, padrão é too80) - um número entre 0 e 100 que indica a porcentagem saudação do índice de saudação que deve ser abordada por uma consulta de sugestões na ordem para Olá consulta toobe relatados como sucesso. Por padrão, pelo menos 80% do índice Olá deve estar disponível ou `Suggest` retornará o código de status HTTP 503. Se você definir `minimumCoverage` e `Suggest` for bem-sucedida, ela retornará HTTP 200 e incluir um `@search.coverage` valor na resposta de saudação indicando a porcentagem de saudação do índice de saudação que foi incluído na consulta de saudação.

> [!NOTE]
> Definir esse valor do parâmetro tooa menor que 100 pode ser útil para garantir a disponibilidade de pesquisa mesmo para os serviços com apenas uma réplica. No entanto, nem todas as sugestões de correspondência são garantidas toobe presente nos resultados de saudação. Se a recuperação é mais importante do aplicativo tooyour de disponibilidade, é melhor não toolower `minimumCoverage` abaixo de seu valor padrão 80.
> 
> 

`api-version=[string]` (obrigatório). versão de visualização de saudação é `api-version=2015-02-28-Preview`. Consulte [Controle de versão de serviço de pesquisa](http://msdn.microsoft.com/library/azure/dn864560.aspx) para obter detalhes e versões alternativas.

Observação: Para essa operação, Olá `api-version` é especificado como um parâmetro de consulta na URL de saudação independentemente se você chamar **sugestões** com GET ou POST.

**Cabeçalhos da solicitação**

Olá lista a seguir descreve hello necessárias e cabeçalhos de solicitação opcional

* `api-key`: Olá `api-key` é usado tooauthenticate Olá solicitação tooyour serviço de pesquisa. É um valor de cadeia de caracteres, a URL do serviço tooyour exclusivo. Olá **sugestões** solicitação pode especificar uma chave de administração ou a chave de consulta como Olá `api-key`.

Você também precisará Olá serviço nome tooconstruct Olá solicitação URL. Você pode obter o nome do serviço hello e `api-key` do seu painel de serviço no hello Portal do Azure. Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter ajuda de navegação de página.

**Corpo da solicitação**

Para GET: Nenhum.

Para POST:

    {
      "filter": "odata_filter_expression",
      "fuzzy": true | false (default),
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 80),
      "orderby": "orderby_expression",
      "search": "partial_search_input",
      "searchFields": "field_name_1, field_name_2, ...",
      "select": "field_name_1, field_name_2, ...",
      "suggesterName": "suggester_name",
      "top": # (default 5)
    }

**Resposta**

Código de status: 200 OK é retornado para uma resposta bem-sucedida.

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
        },
        ...
      ]
    }

Se a opção de projeção Olá for tooretrieve usados campos que estão incluídos em cada elemento da matriz de saudação:

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
          <other projected data fields>
        },
        ...
      ]
    }

**Exemplo**

Recupere 5 sugestões, onde a entrada de pesquisa parcial Olá é "lux"

    GET /indexes/hotels/docs/suggest?search=lux&$top=5&suggesterName=sg&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/suggest?api-version=2015-02-28-Preview
    {
      "search": "lux",
      "top": 5,
      "suggesterName": "sg"
    }
