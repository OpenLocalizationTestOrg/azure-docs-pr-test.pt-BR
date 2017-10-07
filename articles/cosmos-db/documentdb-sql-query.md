---
title: consultas de aaaSQL para a API DocumentDB do Azure Cosmos DB | Microsoft Docs
description: Saiba mais sobre a sintaxe SQL, os conceitos sobre banco de dados e as consultas SQL do Azure Cosmos DB. O SQL pode ser usado como uma linguagem de consulta JSON no Azure Cosmos DB.
keywords: "sintaxe sql, consulta sql, consultas sql, linguagem de consulta json, conceitos de banco de dados e consultas sql, funções agregadas"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: a73b4ab3-0786-42fd-b59b-555fce09db6e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: arramac
ms.openlocfilehash: f4db95b87f5796c4e4299aaf016435cb6301bbfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-queries-for-azure-cosmos-db-documentdb-api"></a>Consultas SQL para a API do DocumentDB do Azure Cosmos DB
O Microsoft Azure Cosmos DB dá suporte à consulta de documentos usando a linguagem SQL como uma linguagem de consulta JSON. O Cosmos DB é verdadeiramente sem esquemas. Em virtude do seu compromisso toohello JSON modelo de dados diretamente no mecanismo de banco de dados hello, ele fornece a indexação automática dos documentos JSON sem a necessidade de esquema explícito ou a criação de índices secundários. 

Ao projetar a linguagem de consulta Olá Cosmos DB, tivemos que dois objetivos em mente:

* Em vez de criação de uma nova linguagem de consulta JSON, queremos toosupport SQL. SQL é uma das linguagens de consulta mais populares e familiar hello. O SQL do Cosmos DB fornece um modelo de programação formal para consultas avançadas em documentos JSON.
* Como JSON documento banco de dados capaz de executar o JavaScript diretamente no mecanismo de banco de dados de hello, queremos o modelo de programação do JavaScript toouse como base Olá para a linguagem de consulta. Olá SQL do DocumentDB API baseada no sistema de tipos do JavaScript, a avaliação de expressão e invocação de função. Isso, por sua vez, oferece um modelo de programação natural para projeções relacionais, navegação hierárquica em documentos JSON, autojunções, consultas espaciais e invocação de UDFs (funções definidas pelo usuário) gravadas inteiramente em JavaScript, entre outros recursos. 

Acreditamos que esses recursos são tooreducing chave fricção de saudação entre o aplicativo hello e o banco de dados de saudação e são essenciais para a produtividade do desenvolvedor.

É recomendável que guia de Introdução observando Olá seguindo o vídeo, onde Aravind Ramachandran mostra os recursos de consulta do banco de dados Cosmos e visitando nosso [parque de consulta](http://www.documentdb.com/sql/demo), onde você pode experimentar o banco de dados do Cosmos e executar consultas SQL nosso conjunto de dados.

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

Em seguida, retorne toothis artigo, onde começamos com um tutorial de consulta SQL que percorre alguns documentos JSON simples e comandos SQL.

## <a id="GettingStarted"></a>Introdução aos comandos SQL no Cosmos DB
toosee Cosmos banco de dados SQL em funciona, vamos começar com alguns documentos JSON simples e percorrer algumas consultas simples em relação a ela. Considere esses dois documentos JSON sobre duas famílias. Com o banco de dados do Cosmos, não precisamos toocreate qualquer esquemas ou índices secundários explicitamente. Precisamos simplesmente tooinsert Olá JSON documentos tooa Cosmos DB coleta e subsequentemente de consulta. Aqui temos JSON simple de documentos para Olá família Andersen, Olá pais, filhos (e seus animais de estimação), endereço e informações de registro. documento de saudação tem cadeias de caracteres, números, valores booleanos, matrizes e propriedades aninhadas. 

**Documento**  

```JSON
{
  "id": "AndersenFamily",
  "lastName": "Andersen",
  "parents": [
     { "firstName": "Thomas" },
     { "firstName": "Mary Kay"}
  ],
  "children": [
     {
         "firstName": "Henriette Thaulow", 
         "gender": "female", 
         "grade": 5,
         "pets": [{ "givenName": "Fluffy" }]
     }
  ],
  "address": { "state": "WA", "county": "King", "city": "seattle" },
  "creationDate": 1431620472,
  "isRegistered": true
}
```

Aqui está um segundo documento, com uma pequena diferença: `givenName` e `familyName` são usados em vez de `firstName` e `lastName`.

**Documento**  

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

Agora vamos tentar algumas consultas em relação a esse toounderstand dados alguns Olá chave aspectos de SQL de API do DocumentDB. Por exemplo, o seguinte Olá consulta retorna documentos de saudação em que o campo de id de saudação corresponde `AndersenFamily`. Uma vez que ele é um `SELECT *`, Olá saída consulta Olá é documento JSON completo hello:

**Consulta**

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Resultados**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]


Agora considere o caso de Olá onde precisamos tooreformat Olá a saída JSON em uma forma diferente. Essa consulta projetos novos JSON do objeto com dois campos selecionados, nome e a cidade quando, cidade dos Olá endereço tem Olá mesmo nome como o estado de saudação. Neste caso, "NY, NY" é correspondente.

**Consulta**    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

**Resultados**

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


consulta seguinte Olá retorna todos os nomes de fornecido de saudação de filhos na família Olá cuja id corresponde `WakefieldFamily` ordenados por cidade Olá de residência.

**Consulta**

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

**Resultados**

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


Gostaríamos toodraw atenção tooa alguns aspectos notáveis Olá Cosmos DB consulta por meio de exemplos de saudação que vimos até agora:  

* Como o SQL da API do DocumentDB trabalha com valores JSON, ele lida com entidades com formato de árvore em vez de linhas e colunas. Portanto, linguagem Olá permite que você consulte toonodes da árvore de saudação em qualquer profundidade arbitrária, como `Node1.Node2.Node3…..Nodem`, semelhante toorelational Referência toohello dois parte referência SQL do `<table>.<column>`.   
* Olá estruturado funciona de linguagem de consulta com os dados sem esquema. Portanto, Olá vinculado do tipo sistema necessidades toobe dinamicamente. Olá mesma expressão pode produzir diferentes tipos em documentos diferentes. resultado de saudação de uma consulta é um valor JSON válido, mas não há garantia de toobe de um esquema fixo.  
* O Cosmos DB dá suporte apenas a documentos JSON estritos. Isso significa expressões e sistema de tipo hello são restrito toodeal somente com tipos JSON. Consulte toohello [especificação JSON](http://www.json.org/) para obter mais detalhes.  
* Uma coleção do Cosmos DB é um contêiner de documentos JSON sem esquemas. relações de saudação em entidades de dados dentro e entre documentos em uma coleção implicitamente são capturadas por confinamento e não pela chave primária e as relações de chave estrangeiras. Este é um aspecto importante vale a pena destacar levando em consideração as junções de dentro do documento hello discutidas posteriormente neste artigo.

## <a id="Indexing"></a> Indexação do Cosmos DB
Antes de entrar em Olá sintaxe SQL de API de documentos, vale a pena explorar Olá indexação de design no banco de dados do Cosmos. 

finalidade de saudação de índices do banco de dados é tooserve consultas em suas várias formas e formas com consumo de recursos mínimo (como CPU e entrada/saída), proporcionando uma taxa de transferência e baixa latência. Muitas vezes, a escolha de saudação do índice Olá para consultar um banco de dados requer muito planejamento e experimentação. Essa abordagem representa um desafio para bancos de dados sem esquema onde dados saudação não está de acordo com esquema estrita tooa e evolui rapidamente. 

Portanto, quando criamos o subsistema de indexação de banco de dados do Cosmos hello, definimos Olá seguintes metas:

* Indexar documentos sem a necessidade de esquema: Olá indexação subsistema não exige nenhuma informação de esquema ou fazer suposições sobre o esquema de documentos de saudação. 
* Suporte para consultas de hierárquicas, relacionais e eficientes, avançadas: índice Olá dá suporte a linguagem de consulta de banco de dados do Cosmos Olá com eficiência, incluindo suporte para projeções hierárquicas e relacionais.
* Suporte para consultas consistentes em face de um volume prolongada de gravações: para cargas de trabalho gravação alta taxa de transferência com consultas consistentes, Olá índice é atualizado incrementalmente com eficiência e online na face de saudação de um volume prolongado de gravações. atualização do índice consistente de saudação é consultas de saudação tooserve crucial no nível de consistência de saudação em qual serviço de documento Olá Olá configurado pelo usuário.
* Suporte para multilocação: dado o modelo com base em reserva de saudação de governança de recursos entre locatários, as atualizações de índice são executadas dentro do orçamento Olá de recursos do sistema (CPU, memória e operações de entrada/saída por segundo) alocados por réplica. 
* Eficiência de armazenamento: para economia, Olá armazenamento em disco de sobrecarga de índice Olá é limitada e previsível. Isso é essencial porque Cosmos DB permite Olá desenvolvedor toomake baseado no custo vantagens e desvantagens entre sobrecarga de índice no desempenho da consulta toohello relação.  

Consulte toohello [exemplos de banco de dados do Azure Cosmos](https://github.com/Azure/azure-documentdb-net) no MSDN para obter exemplos que mostram como tooconfigure Olá política de indexação para uma coleção. Agora, vamos nos detalhes de saudação de saudação sintaxe SQL de banco de dados do Azure Cosmos.

## <a id="Basics"></a>Noções básicas de uma consulta SQL do Azure Cosmos DB
Toda consulta consiste em uma cláusula SELECT e cláusulas FROM e WHERE opcionais de acordo com os padrões ANSI-SQL. Normalmente, para cada consulta, código-fonte na cláusula FROM de Olá Olá é enumerado. Em seguida, Olá filtrar em Olá cláusula WHERE é aplicada em Olá fonte tooretrieve um subconjunto de documentos JSON. Finalmente, a cláusula SELECT Olá é usada tooproject Olá solicitado valores JSON em Olá selecione lista.

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <a id="FromClause"></a>Cláusula FROM
Olá `FROM <from_specification>` cláusula é opcional, a menos que fonte Olá é filtrada ou projetado posteriormente na consulta de saudação. Olá finalidade essa cláusula é toospecify fonte de dados de saudação após a qual Olá consulta deve operar. Normalmente coleção inteira de saudação é origem hello, mas você pode especificar um subconjunto da coleção de saudação em vez disso. 

Uma consulta como `SELECT * FROM Families` indica que a coleção inteira de famílias Olá é origem Olá sobre quais tooenumerate. Um identificador especial raiz pode ser usado toorepresent Olá coleção em vez de usar o nome da coleção hello. Olá lista a seguir contém regras de saudação que são impostas por consulta:

* coleção de saudação pode ser um alias, como `SELECT f.id FROM Families AS f` ou simplesmente `SELECT f.id FROM Families f`. Aqui `f` é equivalente a saudação `Families`. `AS`é um identificador de saudação tooalias palavra-chave opcional.
* Uma vez um alias, origem Olá não pode ser associada. Por exemplo, `SELECT Families.id FROM Families f` é sintaticamente inválida, pois o identificador de hello "Famílias" não pode ser resolvido mais.
* Todas as propriedades que precisar toobe referenciado devem ser totalmente qualificadas. Na ausência de saudação do cumprimento de esquema estrita, isso é imposto tooavoid associações ambíguas. Portanto, `SELECT id FROM Families f` é sintaticamente inválida como propriedade Olá `id` não está associado.

### <a name="subdocuments"></a>Subdocumentos
origem Olá também pode ser o subconjunto menor reduzidos tooa. Por exemplo, tooenumerating apenas uma subárvore de cada documento, subroot Olá poderá se tornar fonte hello, conforme mostrado no exemplo a seguir de saudação:

**Consulta**

    SELECT * 
    FROM Families.children

**Resultados**  

    [
      [
        {
            "firstName": "Henriette Thaulow",
            "gender": "female",
            "grade": 5,
            "pets": [
              {
                  "givenName": "Fluffy"
              }
            ]
        }
      ],
      [
        {
            "familyName": "Merriam",
            "givenName": "Jesse",
            "gender": "female",
            "grade": 1
        },
        {
            "familyName": "Miller",
            "givenName": "Lisa",
            "gender": "female",
            "grade": 8
        }
      ]
    ]

Enquanto Olá acima de exemplo usado uma matriz como origem de Olá, um objeto também pode ser usado como origem de saudação, que é o que é mostrado no exemplo a seguir de saudação: qualquer valor JSON válido que pode ser encontrado na origem da saudação (não indefinido) é considerado para inclusão no resultado de saudação do consulta de saudação. Se não tem algumas famílias um `address.state` valor, eles são excluídos no resultado de consulta hello.

**Consulta**

    SELECT * 
    FROM Families.address.state

**Resultados**

    [
      "WA", 
      "NY"
    ]


## <a id="WhereClause"></a>Cláusula WHERE
Olá cláusula WHERE (**`WHERE <filter_condition>`**) é opcional. Ele especifica Olá condições que os documentos JSON Olá fornecidos pela fonte de saudação devem atender em ordem toobe incluído como parte do resultado de saudação. Qualquer documento JSON deve ser avaliada Olá especificado condições muito "true" toobe considerado para resultados de saudação. Olá onde cláusula é usada pela camada de índice Olá em ordem toodetermine Olá absoluto subconjunto menor de documentos de origem que podem fazer parte do resultado de saudação. 

Olá, consulta a seguir solicita documentos que contêm uma propriedade de nome cujo valor é `AndersenFamily`. Qualquer outro documento que não tem uma propriedade de nome, ou onde o valor de saudação não corresponde `AndersenFamily` é excluído. 

**Consulta**

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Resultados**

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


exemplo de Hello anterior mostrou uma consulta de igualdade simples. O SQL da API do DocumentDB também dá suporte a diversas expressões escalares. Olá mais comumente usada são expressões binário e unário. Referências de propriedade do objeto JSON de origem Olá também são expressões válidas. 

Olá operadores binários a seguir têm suporte atualmente e pode ser usado em consultas, conforme mostrado nos exemplos a seguir de saudação:  

<table>
<tr>
<td>Aritmético</td>    
<td>+,-,*,/,%</td>
</tr>
<tr>
<td>Bit a bit</td>    
<td>|, &, ^, <<, >>, >>> (deslocamento à direita com preenchimento com zero)</td>
</tr>
<tr>
<td>Lógico</td>
<td>AND, OR, NOT</td>
</tr>
<tr>
<td>Comparação</td>    
<td>=, !=, &lt;, &gt;, &lt;=, &gt;=, <></td>
</tr>
<tr>
<td>Cadeia de caracteres</td>    
<td>|| (concatenado)</td>
</tr>
</table>  


Vejamos algumas consultas que usam valores binários.

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


Olá operadores unários +,-, ~ não também têm suporte e podem ser usados em consultas, conforme mostrado no exemplo a seguir de saudação:

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



Além disso operadores unários e de toobinary, referências de propriedade também são permitidas. Por exemplo, `SELECT * FROM Families f WHERE f.isRegistered` retorna Olá documento JSON que contém a propriedade Olá `isRegistered` onde o valor da propriedade Olá é igual toohello JSON `true` valor. Quaisquer outros valores (false, null, indefinido, `<number>`, `<string>`, `<object>`, `<array>`, etc.) leva toohello documento de origem que está sendo excluído do resultado de saudação. 

### <a name="equality-and-comparison-operators"></a>Operadores de igualdade e de comparação
Olá tabela a seguir mostra Olá resultado de comparações de igualdade em documentos API SQL entre quaisquer dois tipos JSON.

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top">
            <strong>Op</strong>
         </td>
         <td valign="top">
            <strong>Indefinido</strong>
         </td>
         <td valign="top">
            <strong>Nulo</strong>
         </td>
         <td valign="top">
            <strong>Booliano</strong>
         </td>
         <td valign="top">
            <strong>Número</strong>
         </td>
         <td valign="top">
            <strong>Cadeia de caracteres</strong>
         </td>
         <td valign="top">
            <strong>Objeto</strong>
         </td>
         <td valign="top">
            <strong>Matriz</strong>
         </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Indefinido<strong>
         </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Nulo<strong>
         </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Booliano<strong>
         </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Número<strong>
         </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Cadeia de caracteres<strong>
         </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Objeto<strong>
         </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
         <td valign="top">
Indefinido </td>
      </tr>
      <tr>
         <td valign="top">
            <strong>Matriz<strong>
         </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
Indefinido </td>
         <td valign="top">
            <strong>OK</strong>
         </td>
      </tr>
   </tbody>
</table>

Para outros operadores de comparação, como >, > =,! =, < e < =, hello seguintes regras se aplicam:   

* Comparação entre resultados de tipos em Indefinido.
* Comparação entre resultados de dois objetos ou duas matrizes em Indefinido.   

Se o resultado de saudação de expressão escalar do hello no filtro de saudação é indefinido, documento correspondente Olá poderia não ser incluído no resultado de hello, pois indefinido muito "true" logicamente não serão iguais.

### <a name="between-keyword"></a>Palavra-chave BETWEEN
Você também pode usar consultas de tooexpress de palavra-chave do hello BETWEEN em intervalos de valores, como no ANSI SQL. BETWEEN pode ser usado em cadeias de caracteres ou números.

Por exemplo, esta consulta retorna todos os documentos de família em qual Olá classificação de seu primeiro filho é entre 1-5 (ambos incluídos). 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

Ao contrário no ANSI SQL, você também pode usar Olá BETWEEN cláusula na cláusula FROM de saudação como no exemplo a seguir de saudação.

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

Para tempos de execução de consulta mais rápidos, lembre-se toocreate uma política de indexação que usa um tipo de índice de intervalo em relação a qualquer propriedades ou caminhos numéricos que são filtradas na cláusula BETWEEN hello. 

Olá principal diferença entre usando BETWEEN na API de documentos e ANSI SQL é que você pode expressar consultas de intervalo em Propriedades de tipos mistos – por exemplo, você pode ter "nota" ser um número (5) em alguns documentos e cadeias de caracteres em outros ("grade4"). Nesses casos, como em JavaScript, uma comparação entre dois resultados de tipos diferentes de "indefinidos" e documento hello será ignorada.

### <a name="logical-and-or-and-not-operators"></a>Operadores lógicos (AND, OR e NOT)
Operadores lógicos funcionam em valores boolianos. Olá tabelas lógicas de verdade para esses operadores são mostradas no hello tabelas a seguir.

| OU | Verdadeiro | Falso | Indefinido |
| --- | --- | --- | --- |
| Verdadeiro |Verdadeiro |Verdadeiro |Verdadeiro |
| Falso |Verdadeiro |Falso |Indefinido |
| Indefinido |Verdadeiro |Indefinido |Indefinido |

| E | Verdadeiro | Falso | Indefinido |
| --- | --- | --- | --- |
| Verdadeiro |Verdadeiro |Falso |Indefinido |
| Falso |Falso |Falso |Falso |
| Indefinido |Indefinido |Falso |Indefinido |

| NÃO |  |
| --- | --- |
| Verdadeiro |Falso |
| Falso |Verdadeiro |
| Indefinido |Indefinido |

### <a name="in-keyword"></a>Palavra-chave IN
palavra-chave IN de saudação pode ser usado toocheck se um valor especificado corresponde a qualquer valor em uma lista. Por exemplo, esta consulta retorna todos os documentos família onde a id de saudação é "WakefieldFamily" ou "AndersenFamily". 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

Este exemplo retorna todos os documentos em que o estado de saudação é qualquer Olá especificado valores.

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a>Operadores Ternário (?) e de União (??)
operadores ternários e adesão de saudação podem ser expressões condicionais toobuild usado, semelhante toopopular linguagens como c# e JavaScript de programação. 

operador ternário (?) de saudação pode ser muito útil quando a criação de novas propriedades JSON no hello surgir. Por exemplo, agora você pode criar níveis de classe consultas tooclassify Olá em um formato legível humano como iniciante/intermediário/Avançado conforme mostrado abaixo.

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

Você também pode aninhar um operador de toohello de chamadas hello como na consulta de saudação abaixo.

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

Como com outros operadores de consulta, se hello propriedades de referência em expressão condicional Olá estão ausentes em qualquer documento, ou se Olá tipos que estão sendo comparados forem diferentes, em seguida, esses documentos são excluídos nos resultados da consulta hello.

Olá adesão (?) pode ser usada para tooefficiently Verificar presença de saudação de uma propriedade (também conhecido como é definido) em um documento. Isso é útil ao consultar dados semiestruturados ou dados de tipos mistos. Por exemplo, esta consulta retorna lastName"hello" se estiver presente, ou hello "surname" se não estiver presente.

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <a id="EscapingReservedKeywords"></a>Acessador de propriedade entre aspas
Você também pode acessar as propriedades usando o operador de propriedade entre aspas Olá `[]`. Por exemplo: `SELECT c.grade` and `SELECT c["grade"]` são equivalentes. Essa sintaxe é útil quando você precisar tooescape uma propriedade que contém espaços, caracteres especiais, ou acontece Olá tooshare mesmo nome como uma palavra reservada ou uma palavra-chave SQL.

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <a id="SelectClause"></a>Cláusula SELECT
cláusula SELECT Hello (**`SELECT <select_list>`**) é obrigatório e especifica quais valores são recuperados da consulta hello, exatamente como no ANSI SQL. subconjunto Olá filtrado sobre documentos de origem Olá são passadas em fase de projeção hello, onde Olá especificados valores JSON são recuperados e um novo objeto JSON é construído, para cada entrada passada para ele. 

saudação de exemplo a seguir mostra uma consulta SELECT típica. 

**Consulta**

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Resultados**

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a>Propriedades aninhadas
Em Olá exemplo a seguir, está projetando duas propriedades aninhadas `f.address.state` e `f.address.city`.

**Consulta**

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Resultados**

    [{
      "state": "WA", 
      "city": "seattle"
    }]


Projeção também oferece suporte a expressões de JSON conforme mostrado no exemplo a seguir de saudação:

**Consulta**

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Resultados**

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


Vamos dar uma olhada na função de saudação do `$1` aqui. Olá `SELECT` cláusula precisa toocreate um objeto JSON e já que nenhuma chave é fornecida, podemos usar nomes de variável implícita argumento começando com `$1`. Por exemplo, esta consulta retorna duas variáveis de argumento implícito, rotuladas como `$1` and `$2`.

**Consulta**

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Resultados**

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a>Atribuição de alias
Agora vamos estender o exemplo de hello acima com o alias explícita de valores. COMO é Olá palavra-chave usada para o alias. É opcional, conforme mostrado durante a projeção Olá segundo valor como `NameInfo`. 

No caso de uma consulta tem duas propriedades com hello mesmo nome, o alias devem ser usado toorename Olá propriedades uma ou ambas, para que suas ambiguidades são desfeitas no hello projetado resultado.

**Consulta**

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Resultados**

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a>Expressões escalares
Além do tooproperty faz referência, a cláusula SELECT Olá também oferece suporte a expressões escalares como constantes, expressões aritméticas, expressões lógicas, etc. Por exemplo, vejamos uma consulta simples do tipo "Olá mundo".

**Consulta**

    SELECT "Hello World"

**Resultados**

    [{
      "$1": "Hello World"
    }]


Este é um exemplo mais complexo que usa uma expressão escalar.

**Consulta**

    SELECT ((2 + 11 % 7)-2)/3    

**Resultados**

    [{
      "$1": 1.33333
    }]


Olá exemplo a seguir, o resultado de Olá da expressão escalar Olá é um valor booleano.

**Consulta**

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

**Resultados**

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a>Criação de objeto e de matriz
Outro recurso fundamental do SQL da API do DocumentDB é a criação de matriz/objeto. No exemplo anterior de saudação, observe que criamos um novo objeto JSON. Da mesma forma, um também pode construir matrizes, conforme mostrado no hello exemplos a seguir:

**Consulta**

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

**Resultados**  

    [
      {
        "CityState": [
          "seattle", 
          "WA"
        ]
      }, 
      {
        "CityState": [
          "NY", 
          "NY"
        ]
      }
    ]

### <a id="ValueKeyword"></a>Palavra-chave VALUE
Olá **valor** palavra-chave fornece um valor do modo tooreturn JSON. Por exemplo, consulta Olá mostrada a seguir retorna Olá escalar `"Hello World"` em vez de `{$1: "Hello World"}`.

**Consulta**

    SELECT VALUE "Hello World"

**Resultados**

    [
      "Hello World"
    ]


Olá, consulta a seguir retorna valor JSON de saudação sem Olá `"address"` rótulo nos resultados da saudação.

**Consulta**

    SELECT VALUE f.address
    FROM Families f    

**Resultados**  

    [
      {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }, 
      {
        "state": "NY", 
        "county": "Manhattan", 
        "city": "NY"
      }
    ]

Olá exemplo a seguir estende essa tooshow como valores primitivos de JSON de tooreturn (nível de folha de saudação da árvore JSON Olá). 

**Consulta**

    SELECT VALUE f.address.state
    FROM Families f    

**Resultados**

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a>* Operador
Olá, operador especial (*) é documento de saudação tooproject com suporte como-é. Quando usado, ele deve ser Olá projetado apenas o campo. Embora uma consulta como `SELECT * FROM Families f` seja válida, `SELECT VALUE * FROM Families f ` e `SELECT *, f.id FROM Families f ` não são.

**Consulta**

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

**Resultados**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

### <a id="TopKeyword"></a>Operador TOP
palavra-chave TOP de saudação pode ser usado toolimit Olá número de valores de uma consulta. Quando TOP é usado em conjunto com a cláusula ORDER BY da saudação, o conjunto de resultados de Olá é o primeiro número de N toohello limitado de valores ordenados; Caso contrário, retornará Olá primeiro N número de resultados em uma ordem indefinida. Como prática recomendada, em uma instrução SELECT, sempre use uma cláusula ORDER BY com a cláusula TOP hello. Isso é única forma de saudação toopredictably indicar quais linhas são afetadas por TOP. 

**Consulta**

    SELECT TOP 1 * 
    FROM Families f 

**Resultados**

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

O TOP pode ser usado com um valor constante (conforme mostrado acima) ou com um valor de variável usando consultas parametrizadas. Para obter mais detalhes, veja as consultas parametrizadas abaixo.

### <a id="Aggregates"></a>Funções de agregação
Você também pode executar agregações em Olá `SELECT` cláusula. Funções agregadas executam um cálculo em um conjunto de valores e retornam um único valor. Por exemplo, hello consulta a seguir retorna Olá contagem de família documentos na coleção de saudação.

**Consulta**

    SELECT COUNT(1) 
    FROM Families f 

**Resultados**

    [{
        "$1": 2
    }]

Você também pode retornar valor escalar Olá Olá agregação usando Olá `VALUE` palavra-chave. Por exemplo, hello consulta a seguir retorna Olá contagem de valores como um único número:

**Consulta**

    SELECT VALUE COUNT(1) 
    FROM Families f 

**Resultados**

    [ 2 ]

Você também pode executar agregações em combinação com filtros. Por exemplo, hello consulta a seguir retorna Olá contagem de documentos com o endereço de saudação em Olá estado de Washington.

**Consulta**

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

**Resultados**

    [ 1 ]

Olá tabela a seguir mostra Olá lista de funções de agregação com suporte na API do DocumentDB. `SUM` e `AVG` são executados por meio de valores numéricos, enquanto `COUNT`, `MIN` e `MAX` podem ser executados em relação a números, cadeias de caracteres, Boolianos e nulos. 

| Uso | Descrição |
|-------|-------------|
| COUNT | Retorna Olá número de itens na expressão de saudação. |
| SUM   | Retorna Olá soma de todos os valores hello expressão hello. |
| MÍN.   | Retorna Olá valor mínimo na expressão de saudação. |
| MÁX.   | Retorna Olá valor máximo na expressão de saudação. |
| AVG   | Retorna Olá média dos valores de saudação na expressão de saudação. |

Agregações também podem ser executadas nos resultados de saudação de uma iteração de matriz. Para obter mais informações, consulte [Iteração de matriz em consultas](#Iteration).

> [!NOTE]
> Quando usar hello Pesquisador de objetos de consulta do portal do Azure, observe que consultas de agregação podem retornar Olá resultados parcialmente agregados em uma página de consulta. Olá SDKs produz um único valor cumulativo em todas as páginas. 
> 
> Ordem em consultas de agregação tooperform usando o código, você precisa de SDK .NET 1.12.0, .NET Core SDK 1.1.0 ou Java SDK 1.9.5 ou superior.    
>

## <a id="OrderByClause"></a>Cláusula ORDER BY
Como no ANSI-SQL, agora você pode incluir uma cláusula Order By opcional ao realizar consultas. cláusula Olá pode incluir uma opcional Crescente/Decrescente argumento toospecify Olá ordem na qual os resultados devem ser recuperados.

Por exemplo, aqui está uma consulta que recupera famílias em ordem de nome de cidade residente hello.

**Consulta**

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

**Resultados**

    [
      {
        "id": "WakefieldFamily",
        "city": "NY"
      },
      {
        "id": "AndersenFamily",
        "city": "Seattle"    
      }
    ]

E aqui está uma consulta que recupera famílias na ordem da data de criação, que é armazenada como um número que representa Olá tempo, ou seja, tempo decorrido desde 1º de janeiro de 1970 em segundos.

**Consulta**

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

**Resultados**

    [
      {
        "id": "WakefieldFamily",
        "creationDate": 1431620462
      },
      {
        "id": "AndersenFamily",
        "creationDate": 1431620472    
      }
    ]

## <a id="Advanced"></a>Conceitos avançados de banco de dados e consultas SQL

### <a id="Iteration"></a>Iteração
Uma nova construção de foi adicionada via Olá **IN** palavra-chave no suporte do SQL do DocumentDB API tooprovide para iterar em matrizes JSON. origem do Hello FROM dá suporte à iteração. Vamos começar com hello exemplo a seguir:

**Consulta**

    SELECT * 
    FROM Families.children

**Resultados**  

    [
      [
        {
          "firstName": "Henriette Thaulow", 
          "gender": "female", 
          "grade": 5, 
          "pets": [{ "givenName": "Fluffy"}]
        }
      ], 
      [
        {
            "familyName": "Merriam", 
            "givenName": "Jesse", 
            "gender": "female", 
            "grade": 1
        }, 
        {
            "familyName": "Miller", 
            "givenName": "Lisa", 
            "gender": "female", 
            "grade": 8
        }
      ]
    ]

Agora vamos dar uma olhada em outra consulta que executa a iteração por filhos na coleção de saudação. Observe a diferença Olá Olá matriz de saída. Este exemplo divide `children` e mescla os resultados de saudação em uma única matriz.  

**Consulta**

    SELECT * 
    FROM c IN Families.children

**Resultados**  

    [
      {
          "firstName": "Henriette Thaulow",
          "gender": "female",
          "grade": 5,
          "pets": [{ "givenName": "Fluffy" }]
      },
      {
          "familyName": "Merriam",
          "givenName": "Jesse",
          "gender": "female",
          "grade": 1
      },
      {
          "familyName": "Miller",
          "givenName": "Lisa",
          "gender": "female",
          "grade": 8
      }
    ]

Isso pode ser mais usado toofilter em cada entrada individual da matriz de saudação conforme mostrado no exemplo a seguir de saudação:

**Consulta**

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

**Resultados**  

    [{
      "givenName": "Lisa"
    }]

Você também pode executar a agregação sobre o resultado de saudação de iteração de matriz. Por exemplo, hello consulta a seguir conta Olá número de filhos entre todas as famílias.

**Consulta**

    SELECT COUNT(child) 
    FROM child IN Families.children

**Resultados**  

    [
      { 
        "$1": 3
      }
    ]

### <a id="Joins"></a>Junções
Em um banco de dados relacional, é importante Olá necessidade toojoin entre tabelas. Sua saudação lógica toodesigning corolário normalizado esquemas. Contrary toothis, API DocumentDB lida com o modelo de dados desnormalizados Olá de documentos sem esquema. Este é o equivalente lógico de saudação de um "autojunção".

sintaxe de saudação que dá suporte a idioma Olá é junção de junção < from_source2 > de < from_source1 >... JUNÇÃO < from_sourceN >. De modo geral, isto retorna um conjunto de tuplas **N** (tupla com valores **N**). Cada tupla terá os valores produzidos pela iteração de todos os alias da coleção em seus respectivos conjuntos. Em outras palavras, este é um produto cruzado completo dos conjuntos de saudação participam da junção de saudação.

Olá exemplos a seguir mostram como funciona a cláusula de junção hello. Olá exemplo a seguir, o resultado de saudação é vazio pois hello produto cruzado de cada documento de origem e um conjunto vazio está vazio.

**Consulta**

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

**Resultados**  

    [{
    }]


Em Olá exemplo a seguir, junção de saudação é entre a raiz do documento hello e hello `children` subroot. Trata-se de um produto cruzado entre dois objetos JSON. fato Olá filhos é uma matriz não é eficaz em Olá junção já que estamos lidando com uma única raiz é Olá filhos matriz. Portanto, o resultado de Olá contém dois resultados, desde que o produto cruzado de cada documento com matriz Olá Olá produz exatamente apenas um documento.

**Consulta**

    SELECT f.id
    FROM Families f
    JOIN f.children

**Resultados**

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


saudação de exemplo a seguir mostra uma junção mais convencional:

**Consulta**

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

**Resultados**

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]



Olá primeiro toonote é que hello `from_source` de saudação **INGRESSAR** cláusula é um iterador. Portanto, Olá fluxo nesse caso é o seguinte:  

* Expanda cada elemento filho **c** na matriz de saudação.
* Aplicar um produto cruzado com raiz de saudação do documento hello **f** com cada elemento filho **c** que foi simplificada na primeira etapa de saudação.
* Por fim, objeto de raiz de saudação do projeto **f** apenas da propriedade name. 

documento primeiro Hello (`AndersenFamily`) contém apenas um elemento filho, portanto o conjunto de resultados Olá contém apenas um único objeto documento correspondente do toothis. segundo documento de saudação (`WakefieldFamily`) contém dois filhos. Portanto, hello produto cruzado produz um objeto separado para cada filho, resultando assim em dois objetos, um para cada documento de toothis filho correspondente. raiz de saudação campos em ambos esses documentos são iguais, Olá conforme o esperado em um produto cruzado.

Olá utilitário real de saudação junção é tooform tuplas de produto cruzado de saudação em uma forma que seja difícil tooproject. Além disso, como podemos ver no exemplo hello abaixo, você pode filtrar na combinação de saudação de uma tupla Olá que permite o usuário optou por uma condição atendida por tuplas Olá geral.

**Consulta**

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

**Resultados**

    [
      {
        "familyName": "AndersenFamily", 
        "childFirstName": "Henriette Thaulow", 
        "petName": "Fluffy"
      }, 
      {
        "familyName": "WakefieldFamily", 
        "childGivenName": "Jesse", 
        "petName": "Goofy"
      }, 
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]



Este exemplo é uma extensão natural da saudação anterior de exemplo e executa uma junção dupla. Portanto, hello produto cruzado podem ser exibido como Olá pseudocódigo a seguir:

    for-each(Family f in Families)
    {    
        for-each(Child c in f.children)
        {
            for-each(Pet p in c.pets)
            {
                return (Tuple(f.id AS familyName, 
                  c.givenName AS childGivenName, 
                  c.firstName AS childFirstName,
                  p.givenName AS petName));
            }
        }
    }

`AndersenFamily` tem um filho que, por sua vez, tem um animal de estimação. Portanto, hello produto cruzado produz uma linha (1\*1\*1) desta família. WakefieldFamily, no entanto, tem dois filhos, mas apenas a filha "Jesse" tem animais de estimação. Porém, Jesse tem dois animais de estimação. Portanto, hello produto cruzado produz 1\*1\*2 = 2 linhas a partir desta família.

No exemplo a seguir hello, há um filtro adicional no `pet`. Exclui todas as tuplas Olá onde Olá animal de estimação nome não é "Sombra". Observe que estamos tuplas toobuild capaz de matrizes de filtro em qualquer um dos elementos de saudação de tupla Olá e qualquer combinação de elementos de saudação do projeto. 

**Consulta**

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

**Resultados**

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <a id="JavaScriptIntegration"></a>Integração do JavaScript
Banco de dados do Azure Cosmos fornece um modelo de programação para a execução lógica do aplicativo JavaScript baseado diretamente em coleções de saudação em termos de procedimentos armazenados e gatilhos. Isso possibilita:

* Capacidade toodo alto desempenho transacional as operações CRUD e consultas em documentos em uma coleção por meio da integração profunda de saudação do tempo de execução de JavaScript diretamente no mecanismo de banco de dados de saudação. 
* Um modelamento natural de fluxo de controle, escopo de variáveis, atribuição e integração de primitivos que lidam com exceções com transações de bancos de dados. Para obter mais detalhes sobre o suporte de banco de dados do Azure Cosmos para integração do JavaScript, consulte toohello documentação de programação do lado do servidor de JavaScript.

### <a id="UserDefinedFunctions"></a>UDFs (Funções Definidas pelo Usuário)
Juntamente com os tipos de saudação já foi definidos neste artigo, o DocumentDB API SQL oferece suporte para funções de definida pelo usuário (UDF). Em particular, UDFs escalares têm suporte em que os desenvolvedores de saudação podem passar argumentos zero ou muitos e retornar um resultado de único argumento novamente. Cada um desses argumentos é verificado para definir se são valores JSON legais.  

Olá sintaxe SQL de API de documentos é estendido toosupport lógica de aplicativo personalizado usando estas funções definidas pelo usuário. As UDFs podem ser registradas na API do DocumentDB e então referenciadas como parte de uma consulta SQL. Na verdade, Olá UDFs exquisitely são projetados toobe chamado através de consultas. Como uma opção de resultado toothis, UDFs não tem objeto de contexto de toohello de acesso que Olá outros JavaScript têm tipos (procedimentos armazenados e gatilhos). Como as consultas são executadas como somente leitura, elas podem ser executadas em réplicas primárias ou secundárias. Portanto, UDFs são toorun projetado em réplicas secundárias ao contrário de outros tipos de JavaScript.

Abaixo está um exemplo de como uma UDF pode ser registrada em Olá Cosmos banco de dados, especificamente em uma coleção de documentos.

       UserDefinedFunction regexMatchUdf = new UserDefinedFunction
       {
           Id = "REGEX_MATCH",
           Body = @"function (input, pattern) { 
                       return input.match(pattern) !== null;
                   };",
       };

       UserDefinedFunction createdUdf = client.CreateUserDefinedFunctionAsync(
           UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
           regexMatchUdf).Result;  

Olá, exemplo anterior cria um UDF cujo nome é `REGEX_MATCH`. Ele aceita dois valores de cadeia de caracteres JSON `input` e `pattern` e verifica se a correspondência do primeiro Olá Olá padrão especificado no segundo Olá usando a função de string de JavaScript.

Agora, podemos usar esta UDF em uma consulta em uma projeção. UDFs devem ser qualificadas com o prefixo de maiusculas e minúsculas hello "udf." quando chamadas por meio de consultas. 

> [!NOTE]
> Anterior too3/17/2015, Cosmos DB suporte para chamadas UDF sem hello "udf." como SELECT REGEX_MATCH(). Esse padrão de chamada foi preterido.  
> 
> 

**Consulta**

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

**Resultados**

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

Olá UDF também pode ser usado dentro de um filtro como mostrado no exemplo hello abaixo, também qualificado com hello "udf." prefixo:

**Consulta**

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

**Resultados**

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


Basicamente, as UDFs são expressões escalares válidas e podem ser usadas em projeções e filtros. 

tooexpand energia Olá de UDFs, vejamos outro exemplo com lógica condicional:

       UserDefinedFunction seaLevelUdf = new UserDefinedFunction()
       {
           Id = "SEALEVEL",
           Body = @"function(city) {
                   switch (city) {
                       case 'seattle':
                           return 520;
                       case 'NY':
                           return 410;
                       case 'Chicago':
                           return 673;
                       default:
                           return -1;
                    }"
            };

            UserDefinedFunction createdUdf = await client.CreateUserDefinedFunctionAsync(
                UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
                seaLevelUdf);


Abaixo está um exemplo exercícios Olá UDF.

**Consulta**

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

**Resultados**

     [
      {
        "city": "seattle", 
        "seaLevel": 520
      }, 
      {
        "city": "NY", 
        "seaLevel": 410
      }
    ]


Como hello showcase de exemplos anteriores, UDFs integram power Olá da linguagem JavaScript Olá documentos API SQL tooprovide uma sofisticada interface programável toodo procedimento, condicional lógica complexa com a Ajuda de saudação do tempo de execução de JavaScript embutida recursos.

Documentos API SQL fornece argumentos Olá toohello UDFs para cada documento na fonte Olá Olá atual estágio (cláusula WHERE ou cláusula SELECT) de processamento hello UDF. Olá resultado é incorporado na Olá diretamente o pipeline de execução geral. Se propriedades de Olá tooby chamado hello UDF parâmetros não estão disponíveis em Olá valor JSON, hello parâmetro é considerado como indefinido e, portanto, Olá invocação UDF inteiramente será ignorada. Da mesma forma se resultado Olá Olá UDF é indefinido, ele não está incluído no resultado de saudação. 

Em resumo, UDFs são lógica de negócios complexa toodo excelentes ferramentas como parte da consulta de saudação.

### <a name="operator-evaluation"></a>Avaliação de operador
Cosmos banco de dados, porque Olá de ser um banco de dados JSON, desenha paralelos com operadores (JavaScript) e sua semântica de avaliação. Enquanto o banco de dados do Cosmos tenta toopreserve semântica de JavaScript em termos de suporte JSON, avaliação de operação de saudação do desvio em alguns casos.

No SQL da API de documentos, diferentemente no SQL tradicional, tipos de saudação de valores geralmente não são conhecidos até que os valores hello são recuperados do banco de dados. Em ordem tooefficiently executar consultas, a maioria dos operadores de saudação tem requisitos de tipo estrito. 

O SQL da API do DocumentDB não realiza conversões implícitas, diferente do JavaScript. Por exemplo, uma consulta como `SELECT * FROM Person p WHERE p.Age = 21` corresponde a documentos que contêm a propriedade Age com o valor 21. Qualquer outro documento cuja propriedade Age corresponder a “21” — ou a outras variações potencialmente infinitas como “021”, “21,0”, “0021”, “00021” etc. — não será correspondido. Isso é, em contraste, toohello JavaScript onde os valores de cadeia de caracteres de hello são implicitamente convertidos toonumbers (com base no operador, por exemplo: = =). Esta escolha é fundamental para uma correspondência eficiente de índices no SQL da API do DocumentDB. 

## <a name="parameterized-sql-queries"></a>Consultas SQL parametrizadas
Cosmos banco de dados oferece suporte a consultas com parâmetros expressados com hello familiar notação @. A SQL parametrizada oferece recursos robustos de manuseio e saída das entradas de usuário, evitando a exposição acidental de dados por meio de uma injeção SQL. 

Por exemplo, você pode escrever uma consulta que define o sobrenome e o estado do endereço como parâmetros e executá-la para vários valores de sobrenome e estado de endereço, com base na entrada do usuário.

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

Essa solicitação pode então ser enviada tooCosmos banco de dados como uma consulta parametrizada de JSON como mostrado abaixo.

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

Olá argumento tooTOP pode ser definido usando consultas parametrizadas como mostrado abaixo.

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

Os valores dos parâmetros podem ser qualquer JSON válido (cadeias de caracteres, números, boolianos, nulos, ou mesmo matrizes e JSON aninhado). Além disso, como o Cosmos DB não tem esquemas, os parâmetros não são validados em relação a nenhum tipo.

## <a id="BuiltinFunctions"></a>Funções internas
O Cosmos DB também dá suporte a várias funções internas para operações comuns, que podem ser usadas em consultas como UDFs (funções definidas pelo usuário).

| Grupo de funções          | Operações                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| Funções matemáticas  | ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN e TAN |
| Funções de verificação de tipo | IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED e IS_PRIMITIVE                                                           |
| Funções de cadeia de caracteres        | CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING e UPPER       |
| Funções de matriz         | ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH e ARRAY_SLICE                                                                                         |
| Funções espaciais       | ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID e ST_ISVALIDDETAILED                                                                           | 

Se você estiver usando uma função definida pelo usuário (UDF) para o qual uma função interna agora está disponível, você deve usar a função interna correspondente do hello como vai toobe toorun de mais rápido e mais eficiente. 

### <a name="mathematical-functions"></a>Funções matemáticas
Olá funções matemáticas executam um cálculo, com base em valores de entrada que são fornecidos como argumentos e retornam um valor numérico. Aqui está uma tabela de funções matemáticas internas com suporte.


| Uso | Descrição |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [[ABS (num_expr)](#bk_abs) | Retorna Olá valor absoluto (positivo) da saudação especificado expressão numérica. |
| [CEILING (num_expr)](#bk_ceiling) | Retorna Olá menor valor de número inteiro maior ou igual ao Olá expressão numérica especificada. |
| [FLOOR (num_expr)](#bk_floor) | Retorna Olá maior inteiro menor ou igual a toohello especificado expressão numérica. |
| [EXP (num_expr)](#bk_exp) | Expoente de saudação retorna da saudação especificado expressão numérica. |
| [LOG (num_expr [,base])](#bk_log) | Retorna Olá o logaritmo natural de saudação expressão numérica, ou logaritmo hello usando Olá especificada base |
| [LOG10 (num_expr)](#bk_log10) | Olá retorna valor logarítmica de base 10 de saudação especificado expressão numérica. |
| [ROUND (num_expr)](#bk_round) | Retorna um valor numérico, arredondado toohello valor de inteiro mais próximo. |
| [TRUNC (num_expr)](#bk_trunc) | Retorna um valor numérico, o valor inteiro mais próximo de toohello truncados. |
| [SQRT (num_expr)](#bk_sqrt) | Retorna Olá quadrado raiz de saudação especificado expressão numérica. |
| [SQUARE (num_expr)](#bk_square) | Saudação de retorna quadrada de saudação especificado expressão numérica. |
| [POWER (num_expr, num_expr)](#bk_power) | Retorna Olá power de saudação especificado expressão numérica toohello valor especificado. |
| [SIGN (num_expr)](#bk_sign) | Retorna Olá sinal valor (-1, 0, 1) de saudação especificado expressão numérica. |
| [ACOS (num_expr)](#bk_acos) | Ângulo de saudação retorna, em radianos, cujo cosseno é Olá expressão numérica especificada; também chamado de arco cosseno. |
| [ASIN (num_expr)](#bk_asin) | Ângulo de saudação retorna, em radianos, cujo seno é hello especificado expressão numérica. Isso também é chamado de arco seno. |
| [ATAN (num_expr)](#bk_atan) | Ângulo de saudação retorna, em radianos, cuja tangente é hello especificado expressão numérica. Isso também é chamado de arco tangente. |
| [ATN2 (num_expr)](#bk_atn2) | Retorna Olá ângulo em radianos, entre o eixo x positivo de saudação e raio de saudação do hello toohello de ponto de origem (x, y), onde x e y são valores de saudação do hello duas expressões flutuantes especificadas. |
| [COS (num_expr)](#bk_cos) | Retorna Olá cosseno trigonométrico Olá especificado o ângulo em radianos, na Olá expressão especificada. |
| [COT (num_expr)](#bk_cot) | Retorna Olá cotangente trigonométrica Olá especificado o ângulo em radianos, Olá especificada expressão numérica. |
| [DEGREES (num_expr)](#bk_degrees) | Retorna Olá ângulo correspondente em graus para um ângulo especificado em radianos. |
| [PI ()](#bk_pi) | Retorna Olá valor constante de PI. |
| [RADIANS (num_expr)](#bk_radians) | Retorna radianos quando uma expressão numérica é inserida em graus. |
| [SIN (num_expr)](#bk_sin) | Retorna Olá seno trigonométrico Olá especificado o ângulo em radianos, na Olá expressão especificada. |
| [TAN (num_expr)](#bk_tan) | Tangente de saudação retorna da expressão de entrada hello, em Olá expressão especificada. |

Por exemplo, agora você pode executar consultas com hello seguinte:

**Consulta**

    SELECT VALUE ABS(-4)

**Resultados**

    [4]

Olá principal diferença entre tooANSI de funções em comparação do banco de dados Cosmos SQL é que eles são projetado toowork bem com dados de esquema sem esquema e misto. Por exemplo, se você tiver um documento em que a propriedade de tamanho hello está ausente ou tem um valor não numérico, como "desconhecido", em seguida, documento hello é ignorado, em vez de retornar um erro.

### <a name="type-checking-functions"></a>Funções de verificação de tipo
funções de verificação de tipo Hello permitem tipo de saudação toocheck de uma expressão em consultas SQL. Tipo de funções de verificação podem ser usado toodetermine tipo de saudação de propriedades nos documentos imediatamente hello quando é desconhecido ou variável. Aqui está uma tabela de funções de verificação de tipo internas com suporte.

<table>
<tr>
  <td><strong>Uso</strong></td>
  <td><strong>Descrição</strong></td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></td>
  <td>Retorna um valor booleano que indica se o tipo de saudação do valor de saudação é uma matriz.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></td>
  <td>Retorna um valor booleano que indica se o tipo de saudação do valor de saudação é um valor booleano.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></td>
  <td>Retorna um valor booleano que indica se o tipo de saudação do valor de saudação é nulo.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></td>
  <td>Retorna um valor booleano que indica se o tipo de saudação do valor de saudação é um número.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></td>
  <td>Retorna um valor booleano que indica se o tipo de saudação do valor de saudação é um objeto JSON.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></td>
  <td>Retorna um valor booleano que indica se o tipo de saudação do valor de saudação é uma cadeia de caracteres.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></td>
  <td>Retorna um valor booleano que indica se a propriedade de saudação foi atribuída um valor.</td>
</tr>
<tr>
  <td><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></td>
  <td>Retorna um valor booleano que indica se tipo de saudação do valor de saudação é cadeia de caracteres, número, booliano ou null.</td>
</tr>

</table>

Usando essas funções, agora você pode executar consultas com hello seguinte:

**Consulta**

    SELECT VALUE IS_NUMBER(-4)

**Resultados**

    [true]

### <a name="string-functions"></a>Funções de cadeia de caracteres
Olá funções escalares a seguir executam uma operação em um valor de cadeia de caracteres de entrada e retornam uma cadeia de caracteres, o valor numérico ou booleano. Aqui temos uma tabela de funções de cadeia de caracteres internas:

| Uso | Descrição |
| --- | --- |
| [LENGTH (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |Retorna o número de saudação de caracteres da saudação especificado expressão de cadeia de caracteres |
| [CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat) |Retorna uma cadeia de caracteres que é o resultado de saudação da concatenação de dois ou mais valores de cadeia de caracteres. |
| [SUBSTRING (str_expr, num_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |Retorna parte de uma expressão de cadeia de caracteres. |
| [STARTSWITH (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |Retorna um valor booleano que indica se primeira expressão de cadeia de caracteres hello termina com hello segundo |
| [ENDSWITH (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |Retorna um valor booleano que indica se primeira expressão de cadeia de caracteres hello termina com hello segundo |
| [CONTAINS (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |Retorna um valor booleano que indica se a primeira expressão de cadeia de caracteres hello contém Olá segundo. |
| [INDEX_OF (str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |Retorna a saudação iniciando a posição da primeira ocorrência de saudação da segunda expressão de cadeia de caracteres hello na primeira expressão de cadeia de caracteres especificada hello, ou -1 se a cadeia de caracteres de saudação não foi encontrada. |
| [LEFT (str_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |Retorna Olá parte esquerda de uma cadeia de caracteres com hello especificado número de caracteres. |
| [RIGHT (str_expr, num_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |Olá retorna parte direita de uma cadeia de caracteres com hello número especificado de caracteres. |
| [LTRIM (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |Retorna uma expressão de cadeia de caracteres após remover os espaços em branco iniciais. |
| [RTRIM (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |Retorna uma expressão de cadeia de caracteres após truncar todos os espaços em branco finais. |
| [LOWER (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |Retorna uma expressão de cadeia de caracteres após converter caracteres maiusculos toolowercase de dados. |
| [UPPER (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |Retorna uma expressão de cadeia de caracteres após converter caracteres minúsculos toouppercase de dados. |
| [REPLACE (str_expr, str_expr, str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |Substitui todas as ocorrências de um valor de cadeia de caracteres especificado por outro valor de cadeia de caracteres. |
| [REPLICATE (str_expr, num_expr)](https://docs.microsoft.com/azure/cosmos-db/documentdb-sql-query-reference#bk_replicate) |Repete um valor de cadeia de caracteres por um número de vezes especificado. |
| [REVERSE (str_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |Retorna a ordem inversa Olá de um valor de cadeia de caracteres. |

Usando essas funções, agora você pode executar consultas com hello seguinte. Por exemplo, você pode retornar sobrenome Olá em maiusculas da seguinte maneira:

**Consulta**

    SELECT VALUE UPPER(Families.id)
    FROM Families

**Resultados**

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

Ou concatenar cadeias de caracteres, como neste exemplo:

**Consulta**

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

**Resultados**

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


Funções de cadeia de caracteres também podem ser usadas em Olá onde os resultados de toofilter cláusula, como no exemplo a seguir de saudação:

**Consulta**

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

**Resultados**

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a>Funções de matriz
Olá funções escalares a seguir executam uma operação em um valor de entrada de matriz e retorno numérico, valor booleano ou de matriz. Aqui temos uma tabela de funções de matriz internas:

| Uso | Descrição |
| --- | --- |
| [ARRAY_LENGTH (arr_expr)](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |Retorna o número de saudação de elementos da saudação especificado expressão de matriz. |
| [ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat) |Retorna uma matriz que é o resultado de saudação da concatenação de dois ou mais valores de matriz. |
| [ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains) |Retorna um valor booleano que indica se a matriz de saudação contém Olá valor especificado. Pode especificar se a correspondência de saudação é completo ou parcial. |
| [ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice) |Retorna parte de uma expressão de matriz. |

Funções de matriz podem ser matrizes de toomanipulate usado em JSON. Por exemplo, aqui está uma consulta que retorna todos os documentos em que um dos pais hello "Robin Wakefield". 

**Consulta**

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

**Resultados**

    [{
      "id": "WakefieldFamily"
    }]

Você pode especificar um fragmento parcial de elementos na matriz de saudação. Olá, consulta a seguir localiza todos os pais com hello `givenName` de `Robin`.

**Consulta**

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)

**Resultados**

    [{
      "id": "WakefieldFamily"
    }]


Aqui está outro exemplo que usa ARRAY_LENGTH tooget Olá número de filhos por família.

**Consulta**

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

**Resultados**

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a>Funções espaciais
Cosmos banco de dados oferece suporte a saudação funções internas do Open Geospatial Consortium (OGC) para consultar geoespaciais a seguir. 

<table>
<tr>
  <td><strong>Uso</strong></td>
  <td><strong>Descrição</strong></td>
</tr>
<tr>
  <td>ST_DISTANCE (point_expr, point_expr)</td>
  <td>Retorna a distância de saudação entre expressões de LineString, Polygon ou ponto GeoJSON Olá dois.</td>
</tr>
<tr>
  <td>ST_WITHIN (point_expr, polygon_expr)</td>
  <td>Retorna uma expressão booleana que indica se o objeto de GeoJSON primeiro Olá (ponto, polígono ou LineString) é no objeto de GeoJSON segundo hello (ponto, polígono ou LineString).</td>
</tr>
<tr>
  <td>ST_INTERSECTS (spatial_expr, spatial_expr)</td>
  <td>Retorna uma expressão booleana que indica se cruzam Olá dois GeoJSON objetos especificados (ponto, polígono ou LineString).</td>
</tr>
<tr>
  <td>ST_ISVALID</td>
  <td>Retorna um valor booliano que indica se a saudação especificado LineString, Polygon ou ponto GeoJSON expressão é válida.</td>
</tr>
<tr>
  <td>ST_ISVALIDDETAILED</td>
  <td>Retorna um valor JSON que contém um valor booliano se Olá especificado expressão LineString, Polygon ou ponto GeoJSON é válido e se for inválido, além disso Olá motivo como um valor de cadeia de caracteres.</td>
</tr>
</table>

Funções espaciais podem ser usado tooperform proximidade consultas em relação aos dados espaciais. Por exemplo, aqui está uma consulta que retorna a que família de todos os documentos que está dentro de 30 km de saudação local especificado usando Olá ST_DISTANCE função interna. 

**Consulta**

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

**Resultados**

    [{
      "id": "WakefieldFamily"
    }]

Para obter detalhes sobre o suporte geoespacial no Cosmos DB, consulte [Trabalhando com os dados geoespaciais no Azure Cosmos DB](geospatial.md). Isso conclui funções espaciais e Olá sintaxe SQL para banco de dados do Cosmos. Agora vamos dar uma olhada em como LINQ consultando funciona e como ele interage com a sintaxe de saudação que vimos até agora.

## <a id="Linq"></a>LINQ tooDocumentDB API SQL
O LINQ é um modelo de programação .NET que expressa a computação como consultas em fluxos de objetos. Cosmos DB fornece toointerface uma biblioteca de cliente com o LINQ, facilitando a uma conversão entre objetos JSON e .NET e um mapeamento de um subconjunto de LINQ consulta tooCosmos DB de consultas. 

imagem de saudação abaixo mostra a arquitetura de saudação de dar suporte a consultas LINQ usando o banco de dados do Cosmos.  Usando o cliente de banco de dados do Cosmos hello, os desenvolvedores podem criar um **IQueryable** que diretamente consultas hello provedor de consulta de banco de dados do Cosmos, que converte a consulta LINQ Olá em uma consulta de banco de dados do Cosmos do objeto. consulta de saudação é então passada toohello tooretrieve do servidor de banco de dados do Cosmos um conjunto de resultados no formato JSON. Olá retornou resultados são desserializados em um fluxo de objetos .NET no lado do cliente de saudação.

![Arquitetura de suporte a consultas LINQ usando a API do DocumentDB – sintaxe SQL, linguagem de consulta JSON, conceitos de banco de dados e consultas SQL][1]

### <a name="net-and-json-mapping"></a>Mapeamento de .NET e JSON
Olá o mapeamento entre objetos .NET e documentos JSON é natural - cada campo de membro de dados é mapeado tooa objeto JSON, onde é o nome do campo Olá mapeados toohello "chave", parte do objeto de saudação e parte de "valor" hello recursivamente mapeado toohello parte de valor de objeto de saudação. Considere Olá exemplo a seguir: objeto de família Olá criado é documento JSON de toohello mapeado conforme mostrado abaixo. E vice-versa, documento JSON de saudação é objeto do .NET tooa back mapeada.

**Classe C#**

    public class Family
    {
        [JsonProperty(PropertyName="id")]
        public string Id;
        public Parent[] parents;
        public Child[] children;
        public bool isRegistered;
    };

    public struct Parent
    {
        public string familyName;
        public string givenName;
    };

    public class Child
    {
        public string familyName;
        public string givenName;
        public string gender;
        public int grade;
        public List<Pet> pets;
    };

    public class Pet
    {
        public string givenName;
    };

    public class Address
    {
        public string state;
        public string county;
        public string city;
    };

    // Create a Family object.
    Parent mother = new Parent { familyName= "Wakefield", givenName="Robin" };
    Parent father = new Parent { familyName = "Miller", givenName = "Ben" };
    Child child = new Child { familyName="Merriam", givenName="Jesse", gender="female", grade=1 };
    Pet pet = new Pet { givenName = "Fluffy" };
    Address address = new Address { state = "NY", county = "Manhattan", city = "NY" };
    Family family = new Family { Id = "WakefieldFamily", parents = new Parent [] { mother, father}, children = new Child[] { child }, isRegistered = false };


**JSON**  

    {
        "id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam", 
                "givenName": "Jesse", 
                "gender": "female", 
                "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            { 
              "familyName": "Miller", 
              "givenName": "Lisa", 
              "gender": "female", 
              "grade": 8 
            }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
    };



### <a name="linq-toosql-translation"></a>Conversão de tooSQL LINQ
provedor de consulta de banco de dados do Cosmos Olá executa um mapeamento de melhor esforço de uma consulta LINQ em uma consulta SQL de banco de dados do Cosmos. Olá descrição a seguir, vamos supor leitor Olá tem uma familiaridade básica do LINQ.

Primeiro, para o sistema de tipo hello, há suporte para todos os tipos de primitivos JSON – tipos numéricos, booliano, cadeia de caracteres e null. Somente esses tipos de JSON têm suporte. Olá expressões escalares a seguir têm suporte.

* Valores de constantes – isso inclui valores constantes Olá primitivos de tipos de dados em tempo de Olá Olá consulta é avaliada.
* Expressões de índice de matriz/propriedade – essas expressões consulte toohello de propriedade de um objeto ou um elemento de matriz.
  
     family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n é uma variável int
* Expressões aritméticas - Incluem expressões aritméticas comuns em valores numéricos e boolianos. Para a lista completa de hello, consulte toohello SQL specification.
  
     2 * family.children[0].grade;    x + y;
* Expressão de comparação de cadeia de caracteres - isso inclui a comparar um valor constante de cadeia de caracteres de toosome de valor de cadeia de caracteres.  
  
     mother.familyName == "Smith";    child.givenName == s; //s é uma variável de cadeia de caracteres
* Expressão de criação de objeto/matriz - estas expressões retornam um objeto do tipo de valor composto ou tipo anônimo ou uma matriz desses objetos. Esses valores podem ser aninhados.
  
     new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //um tipo anônimo com dois campos              
     novo int[] { 3, child.grade, 5 };

### <a id="SupportedLinqOperators"></a>Lista de operadores LINQ com suporte
Aqui está uma lista de operadores LINQ com suporte no provedor LINQ Olá incluídos com hello SDK .NET do DocumentDB.

* **Selecione**: projeções traduzem toohello SQL SELECT incluindo construção de objeto
* **Onde**: filtros traduzir toohello SQL WHERE e suporte a conversão entre & &, | | e! operadores SQL toohello
* **SelectMany**: permite que o desenrolamento da cláusula de junção SQL toohello de matrizes. Pode ser usado toochain/aninhar expressões toofilter em elementos de matriz
* **OrderBy e OrderByDescending**: converte tooORDER BY crescente/decrescente
* Operadores **Count**, **Sum**, **Min**, **Max** e **Average** para agregação e os seus equivalentes assíncronos, **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync** e **AverageAsync**.
* **CompareTo**: converte toorange comparações. Normalmente usados para cadeias de caracteres, já que não são comparáveis no .NET
* **Levar**: converte toohello SQL TOP para limitar os resultados de uma consulta
* **Funções matemáticas**: dá suporte à conversão do. Abs, Acos, Asin do NET, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, logon, Sin, Sqrt, Tan, Truncate funções internas do toohello equivalentes SQL.
* **Funções de cadeia de caracteres**: dá suporte à conversão do. Concat, Contains, EndsWith do NET, IndexOf, contagem, ToLower, TrimStart, Replace, inverso, TrimEnd, StartsWith, SubString, ToUpper toohello equivalente SQL funções internas.
* **Funções de matriz**: dá suporte à conversão do. Concat, Contains e contagem toohello equivalente SQL funções internas do NET.
* **Funções de extensão geoespaciais**: dá suporte à conversão de métodos de stub distância dentro IsValid e IsValidDetailed toohello equivalente SQL funções internas.
* **Função de extensão de função definida pelo usuário**: conversão suporta de saudação stub de método UserDefinedFunctionProvider.Invoke toohello correspondente definido pelo usuário função.
* **Diversos**: dá suporte à conversão de saudação de união e operadores condicionais. É possível converter a tooString contém CONTAINS, ARRAY_CONTAINS ou Olá IN SQL dependendo do contexto.

### <a name="sql-query-operators"></a>Operadores de consulta SQL
Aqui estão alguns exemplos que ilustram como alguns dos operadores de consulta LINQ padrão Olá são convertidos tooCosmos consultas de banco de dados.

#### <a name="select-operator"></a>Operador Select
sintaxe de saudação é `input.Select(x => f(x))`, onde `f` é uma expressão escalar.

**Expressão lambda do LINQ**

    input.Select(family => family.parents[0].familyName);

**SQL** 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



**Expressão lambda do LINQ**

    input.Select(family => family.children[0].grade + c); // c is an int variable


**SQL** 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



**Expressão lambda do LINQ**

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


**SQL** 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a>Operador SelectMany
sintaxe de saudação é `input.SelectMany(x => f(x))`, onde `f` é uma expressão escalar que retorna um tipo de coleção.

**Expressão lambda do LINQ**

    input.SelectMany(family => family.children);

**SQL** 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a>Operador Where
sintaxe de saudação é `input.Where(x => f(x))`, onde `f` é uma expressão escalar, que retorna um valor booliano.

**Expressão lambda do LINQ**

    input.Where(family=> family.parents[0].familyName == "Smith");

**SQL** 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



**Expressão lambda do LINQ**

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

**SQL** 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a>Consultas SQL composta
Olá acima operadores pode ser composto tooform consultas mais avançadas. Como Cosmos DB dá suporte a coleções aninhadas, composição Olá pode ser concatenada ou aninhada.

#### <a name="concatenation"></a>Concatenação
sintaxe de saudação é `input(.|.SelectMany())(.Select()|.Where())*`. Uma consulta concatenada pode ser iniciada por uma consulta `SelectMany` opcional, seguida por múltiplos operadores `Select` ou `Where`.

**Expressão lambda do LINQ**

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

**SQL**

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



**Expressão lambda do LINQ**

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

**SQL** 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



**Expressão lambda do LINQ**

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

**SQL** 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



**Expressão lambda do LINQ**

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

**SQL** 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a>Aninhamento
sintaxe de saudação é `input.SelectMany(x=>x.Q())` onde p é um `Select`, `SelectMany`, ou `Where` operador.

Em uma consulta aninhada, consulta interna Olá é tooeach aplicada elemento da coleção externa hello. Um recurso importante é a que consulta interna Olá pode fazer referência a campos toohello de elementos Olá coleção externa de saudação como autojunções.

**Expressão lambda do LINQ**

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

**SQL** 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


**Expressão lambda do LINQ**

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

**SQL** 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



**Expressão lambda do LINQ**

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

**SQL** 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <a id="ExecutingSqlQueries"></a>Execução de consultas SQL
O Cosmos DB expõe recursos por meio de uma API REST que pode ser chamada por qualquer linguagem que possa fazer solicitações HTTP/HTTPS. Além disso, o Cosmos DB oferece bibliotecas de programação para várias linguagens populares, como .NET, Node.js, JavaScript e Python. Olá API REST e hello todas as várias bibliotecas, oferecem suporte à consulta por meio do SQL. Olá SDK .NET oferece suporte a LINQ, além de consultar tooSQL.

Olá seguintes exemplos mostram como toocreate uma consulta e enviá-lo em uma conta de banco de dados do banco de dados do Cosmos.

### <a id="RestAPI"></a>API REST
O Cosmos DB oferece um modelo de programação RESTful por HTTP. As contas do banco de dados podem ser provisionadas usando uma assinatura do Azure. modelo de recurso de banco de dados do Cosmos Olá consiste em um conjunto de recursos em uma conta de banco de dados, cada um deles é endereçáveis por meio de um URI de lógico e estável. Um conjunto de recursos é chamado tooas um feed neste documento. Uma conta do banco de dados é formada por um conjunto de bancos de dados, cada um contendo diversas coleções, cada uma delas, por sua vez, contendo documentos, UDFs e outros tipos de recursos.

modelo de interação básica Olá com esses recursos é por meio de verbos Olá HTTP GET, PUT, POST e DELETE com a interpretação padrão. verbo POST Olá é usado para a criação de um novo recurso, para executar um procedimento armazenado ou para emitir uma consulta de banco de dados do Cosmos. As consultas sempre são operações somente leitura, sem efeitos colaterais.

Olá exemplos a seguir mostram um POST para uma consulta de API DocumentDB feita em relação a uma coleção que contém dois documentos de exemplo hello que examinamos até o momento. consulta de saudação tem um filtro simples na propriedade de nome hello JSON. Observe o uso de saudação do hello `x-ms-documentdb-isquery` e tipo de conteúdo: `application/query+json` toodenote cabeçalhos que Olá operação é uma consulta.

**Solicitação**

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT * FROM Families f WHERE f.id = @familyId",     
        "parameters": [          
            {"name": "@familyId", "value": "AndersenFamily"}         
        ] 
    }


**Resultados**

    HTTP/1.1 200 Ok
    x-ms-activity-id: 8b4678fa-a947-47d3-8dd3-549a40da6eed
    x-ms-item-count: 1
    x-ms-request-charge: 0.32

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "id":"AndersenFamily",
             "lastName":"Andersen",
             "parents":[  
                {  
                   "firstName":"Thomas"
                },
                {  
                   "firstName":"Mary Kay"
                }
             ],
             "children":[  
                {  
                   "firstName":"Henriette Thaulow",
                   "gender":"female",
                   "grade":5,
                   "pets":[  
                      {  
                         "givenName":"Fluffy"
                      }
                   ]
                }
             ],
             "address":{  
                "state":"WA",
                "county":"King",
                "city":"seattle"
             },
             "_rid":"u1NXANcKogEcAAAAAAAAAA==",
             "_ts":1407691744,
             "_self":"dbs\/u1NXAA==\/colls\/u1NXANcKogE=\/docs\/u1NXANcKogEcAAAAAAAAAA==\/",
             "_etag":"00002b00-0000-0000-0000-53e7abe00000",
             "_attachments":"_attachments\/"
          }
       ],
       "count":1
    }


Olá segundo exemplo mostra uma consulta mais complexa que retorna vários resultados de junção hello.

**Solicitação**

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT 
                     f.id AS familyName, 
                     c.givenName AS childGivenName, 
                     c.firstName AS childFirstName, 
                     p.givenName AS petName 
                  FROM Families f 
                  JOIN c IN f.children 
                  JOIN p in c.pets",     
        "parameters": [] 
    }


**Resultados**

    HTTP/1.1 200 Ok
    x-ms-activity-id: 568f34e3-5695-44d3-9b7d-62f8b83e509d
    x-ms-item-count: 1
    x-ms-request-charge: 7.84

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "familyName":"AndersenFamily",
             "childFirstName":"Henriette Thaulow",
             "petName":"Fluffy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Goofy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Shadow"
          }
       ],
       "count":3
    }


Se os resultados da consulta não podem se ajustar dentro de uma única página de resultados, Olá REST API retorna um token de continuação por meio de saudação `x-ms-continuation-token` cabeçalho de resposta. Os clientes podem pagina resultados, incluindo o cabeçalho de saudação nos resultados subsequentes. número de saudação de resultados por página também pode ser controlado pela Olá `x-ms-max-item-count` cabeçalho do número. Se a consulta especificada Olá tem uma função de agregação como `COUNT`, página Olá da consulta pode retornar um valor agregado parcialmente pela página de saudação de resultados. clientes de saudação deve executar uma agregação de segundo nível sobre esses resultados tooproduce Olá resultados finais, por exemplo, soma contagens de hello retornadas na contagem total de Olá Olá de tooreturn páginas individuais.

política de consistência de dados toomanage Olá para consultas, use Olá `x-ms-consistency-level` cabeçalho como todas as solicitações da API REST. Para consistência de sessão, ele é necessário tooalso echo hello mais recente `x-ms-session-token` cabeçalho de Cookie na solicitação de consulta de saudação. Olá política de indexação da coleção consultado também pode influenciar consistência Olá dos resultados da consulta. Com as configurações de política de indexação padrão de saudação, para coleções Olá índice sempre é atual com o conteúdo do documento hello e resultados corresponderem consistência Olá escolhida para dados de consulta. Se Olá política de indexação é reduzida tooLazy, consultas podem retornar resultados atualizados. Para obter mais informações, consulte [Níveis de consistência no Azure Cosmos DB][consistency-levels].

Se a política de indexação Olá configurado na coleção de saudação não oferecer suporte a consulta especificada hello, servidor de banco de dados do Azure Cosmos Olá retorna 400 "solicitação incorreta". Este código é retornado para consultas de intervalo em caminhos configurados para pesquisas hash (igualdade), e para caminhos excluídos explicitamente da indexação. Olá `x-ms-documentdb-query-enable-scan` cabeçalho pode ser especificado tooallow Olá consulta tooperform uma verificação quando um índice não está disponível.

Você pode obter métricas detalhadas na execução da consulta definindo `x-ms-documentdb-populatequerymetrics` cabeçalho muito`True`. Para obter mais informações, consulte [Métricas de consulta SQL para a API do DocumentDB do Azure Cosmos DB](documentdb-sql-query-metrics.md).

### <a id="DotNetSdk"></a>SDK do C# (.NET)
Olá SDK .NET oferece suporte a LINQ e SQL consultando. Olá exemplo a seguir mostra como a consulta de filtro simples Olá tooperform introduzido no início deste documento.

    foreach (var family in client.CreateDocumentQuery(collectionLink, 
        "SELECT * FROM Families f WHERE f.id = \"AndersenFamily\""))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    SqlQuerySpec query = new SqlQuerySpec("SELECT * FROM Families f WHERE f.id = @familyId");
    query.Parameters = new SqlParameterCollection();
    query.Parameters.Add(new SqlParameter("@familyId", "AndersenFamily"));

    foreach (var family in client.CreateDocumentQuery(collectionLink, query))
    {
        Console.WriteLine("\tRead {0} from parameterized SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery(collectionLink)
        where f.Id == "AndersenFamily"
        select f))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in client.CreateDocumentQuery(collectionLink)
        .Where(f => f.Id == "AndersenFamily")
        .Select(f => f))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


Esta amostra compara duas propriedades quanto à igualdade dentro de cada documento e usa projeções anônimas. 

    foreach (var family in client.CreateDocumentQuery(collectionLink,
        @"SELECT {""Name"": f.id, ""City"":f.address.city} AS Family 
        FROM Families f 
        WHERE f.address.city = f.address.state"))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery<Family>(collectionLink)
        where f.address.city == f.address.state
        select new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in
        client.CreateDocumentQuery<Family>(collectionLink)
        .Where(f => f.address.city == f.address.state)
        .Select(f => new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


Olá próximo exemplo mostra junções, expressadas por meio de LINQ SelectMany.

    foreach (var pet in client.CreateDocumentQuery(collectionLink,
          @"SELECT p
            FROM Families f 
                 JOIN c IN f.children 
                 JOIN p in c.pets 
            WHERE p.givenName = ""Shadow"""))
    {
        Console.WriteLine("\tRead {0} from SQL", pet);
    }

    // Equivalent in Lambda expressions
    foreach (var pet in
        client.CreateDocumentQuery<Family>(collectionLink)
        .SelectMany(f => f.children)
        .SelectMany(c => c.pets)
        .Where(p => p.givenName == "Shadow"))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", pet);
    }



cliente do .NET Olá automaticamente itera em todas as páginas de saudação dos resultados de consulta em blocos de foreach hello como mostrado acima. consulta Olá introduzidas no hello seção da API REST de opções também estão disponíveis no hello SDK do .NET usando Olá `FeedOptions` e `FeedResponse` classes Olá CreateDocumentQuery método. número de saudação de páginas pode ser controlado usando Olá `MaxItemCount` configuração. 

Explicitamente você pode controlar a paginação criando `IDocumentQueryable` usando Olá `IQueryable` objeto, em seguida, lendo a` ResponseContinuationToken` valores e transmiti-los de volta como `RequestContinuationToken` em `FeedOptions`. `EnableScanInQuery`pode ser o conjunto tooenable verificações quando consulta Olá não pode ser suportada pela política de indexação de saudação configurada. Para as coleções particionadas, você pode usar `PartitionKey` toorun consulta Olá uma única partição (embora Cosmos DB pode extrair esse automaticamente de texto da consulta Olá), e `EnableCrossPartitionQuery` toorun as consultas que talvez seja necessário toobe executadas várias partições. 

Consulte também[amostras do .NET de banco de dados do Azure Cosmos](https://github.com/Azure/azure-documentdb-net) para obter mais exemplos contêm consultas. 

### <a id="JavaScriptServerSideApi"></a>API do lado servidor do JavaScript
Cosmos banco de dados fornece um modelo de programação para a execução lógica do aplicativo JavaScript baseado diretamente em coleções de saudação usando procedimentos armazenados e gatilhos. lógica de JavaScript Olá registrada em um nível de coleção pode emitir, em seguida, operações de banco de dados em operações de saudação em documentos Olá de Olá considerando a coleção. Essas operações são encapsuladas em transações ACID ambiente.

Olá exemplo a seguir mostra como as consultas de toouse Olá queryDocuments em toomake Olá API JavaScript do servidor interno procedimentos armazenados e gatilhos.

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            { name: name, author: author },
            function (err, documentCreated) {
                if (err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function (err, matchingDocuments) {
                        if (err) throw new Error(err.message);
    context.getResponse().setBody(matchingDocuments.length);

                        // Replace hello author name for all documents that satisfied hello query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don't need tooexecute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);
                        }
                    })
            });
    }

## <a id="References"></a>Referências
1. [Introdução tooAzure Cosmos DB][introduction]
2. [Especificação do SQL no Azure Cosmos DB](http://go.microsoft.com/fwlink/p/?LinkID=510612)
3. [Amostras do .NET no Azure Cosmos DB](https://github.com/Azure/azure-documentdb-net)
4. [Níveis de consistência do Azure Cosmos DB][consistency-levels]
5. ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)
6. JSON [http://json.org/](http://json.org/)
7. Especificação Javascript [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm) 
8. LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx) 
9. Técnicas de avaliação de consulta para bancos de dados de grande porte [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)
10. Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994
11. Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.
12. Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.
13. G. Graefe. estrutura de cascatas de saudação para otimização da consulta. IEEE Data Eng. Bull., 18(3): 1995.

[1]: ./media/documentdb-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md