---
title: aaaAzure suporte Cosmos DB Gremlin | Microsoft Docs
description: "Saiba mais sobre Olá idioma Gremlin TinkerPop Apache, quais recursos e as etapas e disponíveis no banco de dados do Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
tags: 
ms.assetid: 6016ccba-0fb9-4218-892e-8f32a1bcc590
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/10/2017
ms.author: denlee
ms.openlocfilehash: f8c2ce50c6946e971f56fe1f3838b0899cb2ad8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-gremlin-graph-support"></a>Suporte do BD Cosmos do Azure para gráfico do Gremlin
O Azure Cosmos DB dá suporte à linguagem de cruzamento de gráficos [Gremlin](http://tinkerpop.apache.org) da [Apache Tinkerpop](http://tinkerpop.apache.org/docs/current/reference/#graph-traversal-steps), que é uma API do Graph para criar entidades de gráficos e executar operações de consulta de gráficos. Usar Olá Gremlin idioma toocreate gráfico entidades (vértices e bordas), modificar propriedades dentro dessas entidades, executar consultas e traversais e excluir entidades. 

Banco de dados do Azure Cosmos traz recursos prontos para empresas toograph bancos de dados. Isso inclui distribuição global, dimensionamento independente do armazenamento e da taxa de transferência, latências de milissegundos de dígito único previsíveis, indexação automática e SLAs de 99,99%. Como o banco de dados do Azure Cosmos oferece suporte a TinkerPop/Gremlin, você pode facilmente migrar aplicativos escritos usando outro banco de dados do gráfico sem a necessidade de alterações de código toomake. Além disso, devido ao suporte para Gremlin, o BD Cosmos do Azure integra-se perfeitamente com estruturas de análise habilitadas para TinkerPop, como o [Apache Spark GraphX](http://spark.apache.org/graphx/). 

Neste artigo, fornecem uma rápida explicação passo a passo de Gremlin e enumerar os recursos de Gremlin hello e etapas que são suportadas na visualização de saudação do suporte da API do Graph.

## <a name="gremlin-by-example"></a>Gremlin pelo exemplo
Vamos usar uma toounderstand de gráfico de exemplo como consultas podem ser expressos em Gremlin. Olá figura a seguir mostra um aplicativo de negócios que gerencia dados sobre usuários, interesses e dispositivos na forma de saudação de um gráfico.  

![Banco de dados de exemplo mostrando interesses, dispositivos e pessoas](./media/gremlin-support/sample-graph.png) 

Esse gráfico tem Olá seguintes tipos de vértice (chamados de "rótulo" em Gremlin):

- Pessoas: gráfico de Olá tem três pessoas Robin Thomas e Ben
- Interesses: seus interesses, neste exemplo, Olá jogo de futebol
- : Olá dispositivos de que as pessoas que usam
- Sistemas operacionais: sistemas operacionais Olá Olá dispositivos executar em

Nós representam relações Olá entre essas entidades por meio de saudação tipos/rótulos de borda a seguir:

- Knows (conhece): por exemplo, "Thomas conhece Robin"
- Interessado: interesses de saudação toorepresent de pessoas Olá em nosso gráfico, por exemplo, "Ben está interessado em futebol"
- RunsOS: Saudação de execuções de Laptop sistema operacional Windows
- Usa: toorepresent usa o dispositivo uma pessoa. Por exemplo, Robin usa um telefone Motorola com o número de série 77

Vamos executar algumas operações em relação a esse gráfico usando Olá [Gremlin Console](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console). Você também pode executar essas operações usando drivers de Gremlin na plataforma de saudação de sua escolha (Java, Node.js, Python ou .NET).  Antes de examinarmos o que tem suporte no banco de dados do Azure Cosmos, vamos examinar alguns exemplos tooget familiarizado com a sintaxe de saudação.

Primeiro, vamos ver o CRUD. Olá Gremlin instrução a seguir insere Olá vértice "Thomas" no gráfico de saudação:

```
:> g.addV('person').property('id', 'thomas.1').property('firstName', 'Thomas').property('lastName', 'Andersen').property('age', 44)
```

Em seguida, Olá instrução Gremlin a seguir insere uma borda "sabe" entre Thomas e Robin.

```
:> g.V('thomas.1').addE('knows').to(g.V('robin.1'))
```

Olá consulta a seguir retorna vértices de "pessoa" hello em ordem decrescente de seus nomes:
```
:> g.V().hasLabel('person').order().by('firstName', decr)
```

Onde gráficos brilho é quando você precisar tooanswer perguntas como "quais sistemas operacionais dos amigos dos Thomas usa?". Você pode executar essa tooget de passagem simple Gremlin essas informações do gráfico de saudação:

```
:> g.V('thomas.1').out('knows').out('uses').out('runsos').group().by('name').by(count())
```
Agora, vejamos o que o BD Cosmos do Azure oferece para desenvolvedores de Gremlin.

## <a name="gremlin-features"></a>Recursos do Gremlin
O TinkerPop é um padrão que abrange uma ampla variedade de tecnologias de gráfico. Portanto, ele tem terminologia padrão toodescribe quais recursos são fornecidos por um provedor de gráfico. O BD Cosmos do Azure fornece um banco de dados de gráfico gravável, persistente e de alta simultaneidade que pode ser particionado em vários servidores ou clusters. 

Olá tabela a seguir lista os recursos de TinkerPop Olá implementados pelo banco de dados do Azure Cosmos: 

| Categoria | Implementação do BD Cosmos do Azure |  Observações | 
| --- | --- | --- |
| Recursos de gráfico | Fornece Persistence e ConcurrentAccess na versão prévia. Toosupport projetado transações | Métodos de computador podem ser implementados por meio do conector do Spark hello. |
| Recursos variáveis | Dá suporte a Boolean, Integer, Byte, Double, Float, Integer, Long, String | Dá suporte a tipos primitivos, é compatível com tipos complexos por meio do modelo de dados |
| Recursos do vértice | Dá suporte a RemoveVertices, MetaProperties, AddVertices, MultiProperties, StringIds, UserSuppliedIds, AddProperty, RemoveProperty  | Dá suporte à criação, modificação e exclusão de vértices |
| Recursos de propriedade do vértice | StringIds, UserSuppliedIds, AddProperty, RemoveProperty, BooleanValues, ByteValues, DoubleValues, FloatValues, IntegerValues, LongValues, StringValues | Dá suporte à criação, modificação e exclusão de propriedades do vértice |
| Recursos da borda | AddEges, RemoveEdges, StringIds, UserSuppliedIds, AddProperty, RemoveProperty | Dá suporte à criação, modificação e exclusão de bordas |
| Recursos de propriedade da borda | Properties, BooleanValues, ByteValues, DoubleValues, FloatValues, IntegerValues, LongValues, StringValues | Dá suporte à criação, modificação e exclusão de propriedades da borda |

## <a name="gremlin-wire-format-graphson"></a>Formato de transmissão do Gremlin: GraphSON

Banco de dados do Azure Cosmos usa Olá [GraphSON formato](https://github.com/thinkaurelius/faunus/wiki/GraphSON-Format) ao retornar resultados de operações de Gremlin. GraphSON é formato padrão de Gremlin de saudação para representar vértices, bordas e propriedades (propriedades simples e múltiplos) usando JSON. 

Por exemplo, hello trecho a seguir mostra uma representação de um vértice de GraphSON *retornou toohello cliente* do banco de dados do Azure Cosmos. 

```json
  {
    "id": "a7111ba7-0ea1-43c9-b6b2-efc5e3aea4c0",
    "label": "person",
    "type": "vertex",
    "outE": {
      "knows": [
        {
          "id": "3ee53a60-c561-4c5e-9a9f-9c7924bc9aef",
          "inV": "04779300-1c8e-489d-9493-50fd1325a658"
        },
        {
          "id": "21984248-ee9e-43a8-a7f6-30642bc14609",
          "inV": "a8e3e741-2ef7-4c01-b7c8-199f8e43e3bc"
        }
      ]
    },
    "properties": {
      "firstName": [
        {
          "value": "Thomas"
        }
      ],
      "lastName": [
        {
          "value": "Andersen"
        }
      ],
      "age": [
        {
          "value": 45
        }
      ]
    }
  }
```

Propriedades de saudação usadas pelo GraphSON para vértices são seguinte hello:

| Propriedade | Descrição |
| --- | --- |
| ID | ID de saudação vértice hello. Deve ser exclusivo (em combinação com o valor de saudação do _partition se aplicável) |
| label | rótulo de saudação do vértice hello. Este é o tipo de entidade de saudação do toodescribe opcionais e usadas. |
| type | Toodistinguish usado vértices de documentos não gráficos |
| propriedades | Recipiente de propriedades definidas pelo usuário associadas a vértice hello. Cada propriedade pode ter vários valores. |
| _partition (configurável) | chave de partição de saudação do vértice hello. Pode ser usado tooscale out gráficos toomultiple servidores |
| outE | Contém uma lista de bordas externas de um vértice. Armazenando informações de proximidade Olá com vértice permite execução rápida das traversais. As bordas são agrupadas com base em seus rótulos. |

E borda Olá contém Olá toohelp informações com partes de tooother de navegação do gráfico Olá a seguir.

| Propriedade | Descrição |
| --- | --- |
| ID | Olá ID borda hello. Deve ser exclusivo (em combinação com o valor de saudação do _partition se aplicável) |
| label | rótulo de saudação da borda hello. Essa propriedade é o tipo de relação de saudação do toodescribe opcional e é usada. |
| inV | Ela contém uma lista nos vértices de uma borda. Armazenando informações de proximidade de saudação com borda Olá permite execução rápida das traversais. Os vértices são agrupados com base em seus rótulos. |
| propriedades | Recipiente de propriedades definidas pelo usuário associadas a borda de saudação. Cada propriedade pode ter vários valores. |

Cada propriedade pode armazenar diversos valores em uma matriz. 

| Propriedade | Descrição |
| --- | --- |
| valor | valor de saudação da propriedade Olá

## <a name="gremlin-partitioning"></a>Particionamento do Gremlin

No BD Cosmos do Azure, os gráficos são armazenados dentro de contêineres que podem ser dimensionados de forma independente em termos de armazenamento e taxa de transferência (expressa em solicitações normalizadas por segundo). Cada contêiner deve definir uma propriedade de chave de partição opcional, mas recomendada, que determina um limite de partição lógico para dados relacionados. Cada vértice/borda deve ter uma propriedade `id` exclusiva para entidades dentro desse valor de chave de partição. Olá detalhes são abordados em [particionamento no banco de dados do Azure Cosmos](partition-data.md).

As operações de Gremlin funcionam perfeitamente em dados de gráfico que abrangem várias partições no BD Cosmos do Azure. No entanto, é recomendável toochoose uma chave de partição para seu gráficos que normalmente é usado como um filtro em consultas, tem muitos valores distintos e frequência semelhante de acessar esses valores. 

## <a name="gremlin-steps"></a>Etapas do Gremlin
Agora vamos dar uma olhada em Olá etapas Gremlin suportadas pelo Azure Cosmos DB. Para obter uma referência completa sobre o Gremlin, consulte [Referência do TinkerPop](http://tinkerpop.apache.org/docs/current/reference).

| Etapa | Descrição | Documentação do TinkerPop 3.2 | Observações |
| --- | --- | --- | --- |
| `addE` | Adiciona uma borda entre dois vértices | [Etapa addE](http://tinkerpop.apache.org/docs/current/reference/#addedge-step) | |
| `addV` | Adiciona um gráfico de toohello de vértice | [Etapa addV](http://tinkerpop.apache.org/docs/current/reference/#addvertex-step) | |
| `and` | Ensurest traversais de saudação todos retornam um valor | [e uma etapa](http://tinkerpop.apache.org/docs/current/reference/#and-step) | |
| `as` | Um modulador de etapa tooassign uma saída de variável toohello de uma etapa | [Etapa as](http://tinkerpop.apache.org/docs/current/reference/#as-step) | |
| `by` | Um modulador de etapa usado com `group` e `order` | [Etapa by](http://tinkerpop.apache.org/docs/current/reference/#by-step) | |
| `coalesce` | Retorna Olá primeira passagem que retorna um resultado | [Etapa coalesce](http://tinkerpop.apache.org/docs/current/reference/#coalesce-step) | |
| `constant` | Retorna um valor constante. Usada com `coalesce`| [Etapa constant](http://tinkerpop.apache.org/docs/current/reference/#constant-step) | |
| `count` | Retorna a contagem de saudação de passagem Olá | [Etapa count](http://tinkerpop.apache.org/docs/current/reference/#count-step) | |
| `dedup` | Retorna Olá valores com hello duplicatas removidas | [Etapa dedup](http://tinkerpop.apache.org/docs/current/reference/#dedup-step) | |
| `drop` | Descarta Olá valores (vértice/borda) | [Etapa drop](http://tinkerpop.apache.org/docs/current/reference/#drop-step) | |
| `fold` | Age como uma barreira que calcula a agregação de saudação de resultados| [Etapa fold](http://tinkerpop.apache.org/docs/current/reference/#fold-step) | |
| `group` | Grupos Olá valores com base nos rótulos de saudação especificados| [Etapa group](http://tinkerpop.apache.org/docs/current/reference/#group-step) | |
| `has` | Propriedades de toofilter usadas, vértices e bordas. Dá suporte às variantes `hasLabel`, `hasId`, `hasNot` e `has`. | [Etapa has](http://tinkerpop.apache.org/docs/current/reference/#has-step) | |
| `inject` | Insere valores em um fluxo| [Etapa inject](http://tinkerpop.apache.org/docs/current/reference/#inject-step) | |
| `is` | Usado tooperform um filtro usando uma expressão booliana | [Etapa is](http://tinkerpop.apache.org/docs/current/reference/#is-step) | |
| `limit` | Usado toolimit o número de itens no percurso Olá| [Etapa limit](http://tinkerpop.apache.org/docs/current/reference/#limit-step) | |
| `local` | Local encapsula uma seção de uma subconsulta de passagem, de forma semelhante tooa | [Etapa local](http://tinkerpop.apache.org/docs/current/reference/#local-step) | |
| `not` | Usado tooproduce negação de saudação de um filtro | [Etapa not](http://tinkerpop.apache.org/docs/current/reference/#not-step) | |
| `optional` | Retorna Olá resultado da saudação especificado passagem se ele produz um resultado mais retorna Olá elemento de chamada | [Etapa optional](http://tinkerpop.apache.org/docs/current/reference/#optional-step) | |
| `or` | Garante que pelo menos uma das traversais Olá retorna um valor | [Etapa or](http://tinkerpop.apache.org/docs/current/reference/#or-step) | |
| `order` | Retorna resultados em Olá especificado a ordem de classificação | [Etapa order](http://tinkerpop.apache.org/docs/current/reference/#order-step) | |
| `path` | Caminho completo do hello retorna transversal Olá | [Etapa path](http://tinkerpop.apache.org/docs/current/reference/#path-step) | |
| `project` | Propriedades de saudação projetos como um mapa | [Etapa project](http://tinkerpop.apache.org/docs/current/reference/#project-step) | |
| `properties` | Retorna as propriedades para Olá Olá especificado rótulos | [Etapa properties](http://tinkerpop.apache.org/docs/current/reference/#properties-step) | |
| `range` | Filtros toohello o intervalo de valores especificado| [Etapa range](http://tinkerpop.apache.org/docs/current/reference/#range-step) | |
| `repeat` | Repetições Olá etapa para hello número especificado de vezes. Usada para efetuar loop | [Etapa repeat](http://tinkerpop.apache.org/docs/current/reference/#repeat-step) | |
| `sample` | Os resultados de toosample de passagem Olá usados | [Etapa sample](http://tinkerpop.apache.org/docs/current/reference/#sample-step) | |
| `select` | Os resultados de tooproject de passagem Olá usados |  [Etapa select](http://tinkerpop.apache.org/docs/current/reference/#select-step) | |
| `store` | Usada para agregações sem bloqueio de passagem Olá | [Etapa store](http://tinkerpop.apache.org/docs/current/reference/#store-step) | |
| `tree` | Agrega os caminhos de um vértice em uma árvore | [Etapa tree](http://tinkerpop.apache.org/docs/current/reference/#tree-step) | |
| `unfold` | Desenrola um iterador como uma etapa| [Etapa unfold](http://tinkerpop.apache.org/docs/current/reference/#unfold-step) | |
| `union` | Mescla resultados de várias passagens| [Etapa union](http://tinkerpop.apache.org/docs/current/reference/#union-step) | |
| `V` | Inclui Olá etapas necessárias para traversais entre vértices e bordas `V`, `E`, `out`, `in`, `both`, `outE`, `inE`, `bothE`, `outV`, `inV`, `bothV`, e `otherV` para | [Etapa vertex](http://tinkerpop.apache.org/docs/current/reference/#vertex-steps) | |
| `where` | Usado toofilter resultados de passagem de saudação. Dá suporte aos operadores `eq`, `neq`, `lt`, `lte`, `gt`, `gte` e `between`  | [Etapa where](http://tinkerpop.apache.org/docs/current/reference/#where-step) | |

O mecanismo otimizado para gravação do BD Cosmos do Azure dá suporte à indexação automática de todas as propriedades dentro dos vértices e bordas por padrão. Portanto, consultas com filtros, consultas, classificação, o intervalo ou agregações em qualquer propriedade que são processadas do índice hello e atendidas com eficiência. Para obter mais informações sobre como a indexação funciona no BD Cosmos do Azure, consulte nosso artigo sobre [Indexação independente do esquema](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf).

## <a name="next-steps"></a>Próximas etapas
* Comece a compilar um aplicativo de gráfico [usando nossos SDKs](create-graph-dotnet.md) 
* Saiba mais sobre o [Suporte para gráfico do BD Cosmos do Azure](graph-introduction.md)
