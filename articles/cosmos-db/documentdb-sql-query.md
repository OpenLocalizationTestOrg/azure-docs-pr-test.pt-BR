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
# <a name="sql-queries-for-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="bf3c8-105">Consultas SQL para a API do DocumentDB do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bf3c8-105">SQL queries for Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="bf3c8-106">O Microsoft Azure Cosmos DB dá suporte à consulta de documentos usando a linguagem SQL como uma linguagem de consulta JSON.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-106">Microsoft Azure Cosmos DB supports querying documents using SQL (Structured Query Language) as a JSON query language.</span></span> <span data-ttu-id="bf3c8-107">O Cosmos DB é verdadeiramente sem esquemas.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-107">Cosmos DB is truly schema-free.</span></span> <span data-ttu-id="bf3c8-108">Em virtude do seu compromisso toohello JSON modelo de dados diretamente no mecanismo de banco de dados hello, ele fornece a indexação automática dos documentos JSON sem a necessidade de esquema explícito ou a criação de índices secundários.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-108">By virtue of its commitment toohello JSON data model directly within hello database engine, it provides automatic indexing of JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> 

<span data-ttu-id="bf3c8-109">Ao projetar a linguagem de consulta Olá Cosmos DB, tivemos que dois objetivos em mente:</span><span class="sxs-lookup"><span data-stu-id="bf3c8-109">While designing hello query language for Cosmos DB, we had two goals in mind:</span></span>

* <span data-ttu-id="bf3c8-110">Em vez de criação de uma nova linguagem de consulta JSON, queremos toosupport SQL.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-110">Instead of inventing a new JSON query language, we wanted toosupport SQL.</span></span> <span data-ttu-id="bf3c8-111">SQL é uma das linguagens de consulta mais populares e familiar hello.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-111">SQL is one of hello most familiar and popular query languages.</span></span> <span data-ttu-id="bf3c8-112">O SQL do Cosmos DB fornece um modelo de programação formal para consultas avançadas em documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-112">Cosmos DB SQL provides a formal programming model for rich queries over JSON documents.</span></span>
* <span data-ttu-id="bf3c8-113">Como JSON documento banco de dados capaz de executar o JavaScript diretamente no mecanismo de banco de dados de hello, queremos o modelo de programação do JavaScript toouse como base Olá para a linguagem de consulta.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-113">As a JSON document database capable of executing JavaScript directly in hello database engine, we wanted toouse JavaScript's programming model as hello foundation for our query language.</span></span> <span data-ttu-id="bf3c8-114">Olá SQL do DocumentDB API baseada no sistema de tipos do JavaScript, a avaliação de expressão e invocação de função.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-114">hello DocumentDB API SQL is rooted in JavaScript's type system, expression evaluation, and function invocation.</span></span> <span data-ttu-id="bf3c8-115">Isso, por sua vez, oferece um modelo de programação natural para projeções relacionais, navegação hierárquica em documentos JSON, autojunções, consultas espaciais e invocação de UDFs (funções definidas pelo usuário) gravadas inteiramente em JavaScript, entre outros recursos.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-115">This in-turn provides a natural programming model for relational projections, hierarchical navigation across JSON documents, self joins, spatial queries, and invocation of user-defined functions (UDFs) written entirely in JavaScript, among other features.</span></span> 

<span data-ttu-id="bf3c8-116">Acreditamos que esses recursos são tooreducing chave fricção de saudação entre o aplicativo hello e o banco de dados de saudação e são essenciais para a produtividade do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-116">We believe that these capabilities are key tooreducing hello friction between hello application and hello database and are crucial for developer productivity.</span></span>

<span data-ttu-id="bf3c8-117">É recomendável que guia de Introdução observando Olá seguindo o vídeo, onde Aravind Ramachandran mostra os recursos de consulta do banco de dados Cosmos e visitando nosso [parque de consulta](http://www.documentdb.com/sql/demo), onde você pode experimentar o banco de dados do Cosmos e executar consultas SQL nosso conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-117">We recommend getting started by watching hello following video, where Aravind Ramachandran shows Cosmos DB's querying capabilities, and by visiting our [Query Playground](http://www.documentdb.com/sql/demo), where you can try out Cosmos DB and run SQL queries against our dataset.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

<span data-ttu-id="bf3c8-118">Em seguida, retorne toothis artigo, onde começamos com um tutorial de consulta SQL que percorre alguns documentos JSON simples e comandos SQL.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-118">Then, return toothis article, where we start with a SQL query tutorial that walks you through some simple JSON documents and SQL commands.</span></span>

## <span data-ttu-id="bf3c8-119"><a id="GettingStarted"></a>Introdução aos comandos SQL no Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bf3c8-119"><a id="GettingStarted"></a>Getting started with SQL commands in Cosmos DB</span></span>
<span data-ttu-id="bf3c8-120">toosee Cosmos banco de dados SQL em funciona, vamos começar com alguns documentos JSON simples e percorrer algumas consultas simples em relação a ela.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-120">toosee Cosmos DB SQL at work, let's begin with a few simple JSON documents and walk through some simple queries against it.</span></span> <span data-ttu-id="bf3c8-121">Considere esses dois documentos JSON sobre duas famílias.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-121">Consider these two JSON documents about two families.</span></span> <span data-ttu-id="bf3c8-122">Com o banco de dados do Cosmos, não precisamos toocreate qualquer esquemas ou índices secundários explicitamente.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-122">With Cosmos DB, we do not need toocreate any schemas or secondary indices explicitly.</span></span> <span data-ttu-id="bf3c8-123">Precisamos simplesmente tooinsert Olá JSON documentos tooa Cosmos DB coleta e subsequentemente de consulta.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-123">We simply need tooinsert hello JSON documents tooa Cosmos DB collection and subsequently query.</span></span> <span data-ttu-id="bf3c8-124">Aqui temos JSON simple de documentos para Olá família Andersen, Olá pais, filhos (e seus animais de estimação), endereço e informações de registro.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-124">Here we have a simple JSON document for hello Andersen family, hello parents, children (and their pets), address, and registration information.</span></span> <span data-ttu-id="bf3c8-125">documento de saudação tem cadeias de caracteres, números, valores booleanos, matrizes e propriedades aninhadas.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-125">hello document has strings, numbers, Booleans, arrays, and nested properties.</span></span> 

<span data-ttu-id="bf3c8-126">**Documento**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-126">**Document**</span></span>  

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

<span data-ttu-id="bf3c8-127">Aqui está um segundo documento, com uma pequena diferença: `givenName` e `familyName` são usados em vez de `firstName` e `lastName`.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-127">Here's a second document with one subtle difference – `givenName` and `familyName` are used instead of `firstName` and `lastName`.</span></span>

<span data-ttu-id="bf3c8-128">**Documento**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-128">**Document**</span></span>  

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

<span data-ttu-id="bf3c8-129">Agora vamos tentar algumas consultas em relação a esse toounderstand dados alguns Olá chave aspectos de SQL de API do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-129">Now let's try a few queries against this data toounderstand some of hello key aspects of DocumentDB API SQL.</span></span> <span data-ttu-id="bf3c8-130">Por exemplo, o seguinte Olá consulta retorna documentos de saudação em que o campo de id de saudação corresponde `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-130">For example, hello following query returns hello documents where hello id field matches `AndersenFamily`.</span></span> <span data-ttu-id="bf3c8-131">Uma vez que ele é um `SELECT *`, Olá saída consulta Olá é documento JSON completo hello:</span><span class="sxs-lookup"><span data-stu-id="bf3c8-131">Since it's a `SELECT *`, hello output of hello query is hello complete JSON document:</span></span>

<span data-ttu-id="bf3c8-132">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-132">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="bf3c8-133">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-133">**Results**</span></span>

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


<span data-ttu-id="bf3c8-134">Agora considere o caso de Olá onde precisamos tooreformat Olá a saída JSON em uma forma diferente.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-134">Now consider hello case where we need tooreformat hello JSON output in a different shape.</span></span> <span data-ttu-id="bf3c8-135">Essa consulta projetos novos JSON do objeto com dois campos selecionados, nome e a cidade quando, cidade dos Olá endereço tem Olá mesmo nome como o estado de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-135">This query projects a new JSON object with two selected fields, Name and City, when hello address' city has hello same name as hello state.</span></span> <span data-ttu-id="bf3c8-136">Neste caso, "NY, NY" é correspondente.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-136">In this case, "NY, NY" matches.</span></span>

<span data-ttu-id="bf3c8-137">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-137">**Query**</span></span>    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

<span data-ttu-id="bf3c8-138">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-138">**Results**</span></span>

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


<span data-ttu-id="bf3c8-139">consulta seguinte Olá retorna todos os nomes de fornecido de saudação de filhos na família Olá cuja id corresponde `WakefieldFamily` ordenados por cidade Olá de residência.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-139">hello next query returns all hello given names of children in hello family whose id matches `WakefieldFamily` ordered by hello city of residence.</span></span>

<span data-ttu-id="bf3c8-140">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-140">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

<span data-ttu-id="bf3c8-141">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-141">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


<span data-ttu-id="bf3c8-142">Gostaríamos toodraw atenção tooa alguns aspectos notáveis Olá Cosmos DB consulta por meio de exemplos de saudação que vimos até agora:</span><span class="sxs-lookup"><span data-stu-id="bf3c8-142">We would like toodraw attention tooa few noteworthy aspects of hello Cosmos DB query language through hello examples we've seen so far:</span></span>  

* <span data-ttu-id="bf3c8-143">Como o SQL da API do DocumentDB trabalha com valores JSON, ele lida com entidades com formato de árvore em vez de linhas e colunas.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-143">Since DocumentDB API SQL works on JSON values, it deals with tree shaped entities instead of rows and columns.</span></span> <span data-ttu-id="bf3c8-144">Portanto, linguagem Olá permite que você consulte toonodes da árvore de saudação em qualquer profundidade arbitrária, como `Node1.Node2.Node3…..Nodem`, semelhante toorelational Referência toohello dois parte referência SQL do `<table>.<column>`.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-144">Therefore, hello language lets you refer toonodes of hello tree at any arbitrary depth, like `Node1.Node2.Node3…..Nodem`, similar toorelational SQL referring toohello two part reference of `<table>.<column>`.</span></span>   
* <span data-ttu-id="bf3c8-145">Olá estruturado funciona de linguagem de consulta com os dados sem esquema.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-145">hello structured query language works with schema-less data.</span></span> <span data-ttu-id="bf3c8-146">Portanto, Olá vinculado do tipo sistema necessidades toobe dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-146">Therefore, hello type system needs toobe bound dynamically.</span></span> <span data-ttu-id="bf3c8-147">Olá mesma expressão pode produzir diferentes tipos em documentos diferentes.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-147">hello same expression could yield different types on different documents.</span></span> <span data-ttu-id="bf3c8-148">resultado de saudação de uma consulta é um valor JSON válido, mas não há garantia de toobe de um esquema fixo.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-148">hello result of a query is a valid JSON value, but is not guaranteed toobe of a fixed schema.</span></span>  
* <span data-ttu-id="bf3c8-149">O Cosmos DB dá suporte apenas a documentos JSON estritos.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-149">Cosmos DB only supports strict JSON documents.</span></span> <span data-ttu-id="bf3c8-150">Isso significa expressões e sistema de tipo hello são restrito toodeal somente com tipos JSON.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-150">This means hello type system and expressions are restricted toodeal only with JSON types.</span></span> <span data-ttu-id="bf3c8-151">Consulte toohello [especificação JSON](http://www.json.org/) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-151">Refer toohello [JSON specification](http://www.json.org/) for more details.</span></span>  
* <span data-ttu-id="bf3c8-152">Uma coleção do Cosmos DB é um contêiner de documentos JSON sem esquemas.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-152">A Cosmos DB collection is a schema-free container of JSON documents.</span></span> <span data-ttu-id="bf3c8-153">relações de saudação em entidades de dados dentro e entre documentos em uma coleção implicitamente são capturadas por confinamento e não pela chave primária e as relações de chave estrangeiras.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-153">hello relations in data entities within and across documents in a collection are implicitly captured by containment and not by primary key and foreign key relations.</span></span> <span data-ttu-id="bf3c8-154">Este é um aspecto importante vale a pena destacar levando em consideração as junções de dentro do documento hello discutidas posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-154">This is an important aspect worth pointing out in light of hello intra-document joins discussed later in this article.</span></span>

## <span data-ttu-id="bf3c8-155"><a id="Indexing"></a> Indexação do Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bf3c8-155"><a id="Indexing"></a> Cosmos DB indexing</span></span>
<span data-ttu-id="bf3c8-156">Antes de entrar em Olá sintaxe SQL de API de documentos, vale a pena explorar Olá indexação de design no banco de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-156">Before we get into hello DocumentDB API SQL syntax, it is worth exploring hello indexing design in Cosmos DB.</span></span> 

<span data-ttu-id="bf3c8-157">finalidade de saudação de índices do banco de dados é tooserve consultas em suas várias formas e formas com consumo de recursos mínimo (como CPU e entrada/saída), proporcionando uma taxa de transferência e baixa latência.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-157">hello purpose of database indexes is tooserve queries in their various forms and shapes with minimum resource consumption (like CPU and input/output) while providing good throughput and low latency.</span></span> <span data-ttu-id="bf3c8-158">Muitas vezes, a escolha de saudação do índice Olá para consultar um banco de dados requer muito planejamento e experimentação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-158">Often, hello choice of hello right index for querying a database requires much planning and experimentation.</span></span> <span data-ttu-id="bf3c8-159">Essa abordagem representa um desafio para bancos de dados sem esquema onde dados saudação não está de acordo com esquema estrita tooa e evolui rapidamente.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-159">This approach poses a challenge for schema-less databases where hello data doesn’t conform tooa strict schema and evolves rapidly.</span></span> 

<span data-ttu-id="bf3c8-160">Portanto, quando criamos o subsistema de indexação de banco de dados do Cosmos hello, definimos Olá seguintes metas:</span><span class="sxs-lookup"><span data-stu-id="bf3c8-160">Therefore, when we designed hello Cosmos DB indexing subsystem, we set hello following goals:</span></span>

* <span data-ttu-id="bf3c8-161">Indexar documentos sem a necessidade de esquema: Olá indexação subsistema não exige nenhuma informação de esquema ou fazer suposições sobre o esquema de documentos de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-161">Index documents without requiring schema: hello indexing subsystem does not require any schema information or make any assumptions about schema of hello documents.</span></span> 
* <span data-ttu-id="bf3c8-162">Suporte para consultas de hierárquicas, relacionais e eficientes, avançadas: índice Olá dá suporte a linguagem de consulta de banco de dados do Cosmos Olá com eficiência, incluindo suporte para projeções hierárquicas e relacionais.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-162">Support for efficient, rich hierarchical, and relational queries: hello index supports hello Cosmos DB query language efficiently, including support for hierarchical and relational projections.</span></span>
* <span data-ttu-id="bf3c8-163">Suporte para consultas consistentes em face de um volume prolongada de gravações: para cargas de trabalho gravação alta taxa de transferência com consultas consistentes, Olá índice é atualizado incrementalmente com eficiência e online na face de saudação de um volume prolongado de gravações.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-163">Support for consistent queries in face of a sustained volume of writes: For high write throughput workloads with consistent queries, hello index is updated incrementally, efficiently, and online in hello face of a sustained volume of writes.</span></span> <span data-ttu-id="bf3c8-164">atualização do índice consistente de saudação é consultas de saudação tooserve crucial no nível de consistência de saudação em qual serviço de documento Olá Olá configurado pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-164">hello consistent index update is crucial tooserve hello queries at hello consistency level in which hello user configured hello document service.</span></span>
* <span data-ttu-id="bf3c8-165">Suporte para multilocação: dado o modelo com base em reserva de saudação de governança de recursos entre locatários, as atualizações de índice são executadas dentro do orçamento Olá de recursos do sistema (CPU, memória e operações de entrada/saída por segundo) alocados por réplica.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-165">Support for multi-tenancy: Given hello reservation-based model for resource governance across tenants, index updates are performed within hello budget of system resources (CPU, memory, and input/output operations per second) allocated per replica.</span></span> 
* <span data-ttu-id="bf3c8-166">Eficiência de armazenamento: para economia, Olá armazenamento em disco de sobrecarga de índice Olá é limitada e previsível.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-166">Storage efficiency: For cost effectiveness, hello on-disk storage overhead of hello index is bounded and predictable.</span></span> <span data-ttu-id="bf3c8-167">Isso é essencial porque Cosmos DB permite Olá desenvolvedor toomake baseado no custo vantagens e desvantagens entre sobrecarga de índice no desempenho da consulta toohello relação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-167">This is crucial because Cosmos DB allows hello developer toomake cost-based tradeoffs between index overhead in relation toohello query performance.</span></span>  

<span data-ttu-id="bf3c8-168">Consulte toohello [exemplos de banco de dados do Azure Cosmos](https://github.com/Azure/azure-documentdb-net) no MSDN para obter exemplos que mostram como tooconfigure Olá política de indexação para uma coleção.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-168">Refer toohello [Azure Cosmos DB samples](https://github.com/Azure/azure-documentdb-net) on MSDN for samples showing how tooconfigure hello indexing policy for a collection.</span></span> <span data-ttu-id="bf3c8-169">Agora, vamos nos detalhes de saudação de saudação sintaxe SQL de banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-169">Let’s now get into hello details of hello Azure Cosmos DB SQL syntax.</span></span>

## <span data-ttu-id="bf3c8-170"><a id="Basics"></a>Noções básicas de uma consulta SQL do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bf3c8-170"><a id="Basics"></a>Basics of an Azure Cosmos DB SQL query</span></span>
<span data-ttu-id="bf3c8-171">Toda consulta consiste em uma cláusula SELECT e cláusulas FROM e WHERE opcionais de acordo com os padrões ANSI-SQL.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-171">Every query consists of a SELECT clause and optional FROM and WHERE clauses per ANSI-SQL standards.</span></span> <span data-ttu-id="bf3c8-172">Normalmente, para cada consulta, código-fonte na cláusula FROM de Olá Olá é enumerado.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-172">Typically, for each query, hello source in hello FROM clause is enumerated.</span></span> <span data-ttu-id="bf3c8-173">Em seguida, Olá filtrar em Olá cláusula WHERE é aplicada em Olá fonte tooretrieve um subconjunto de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-173">Then hello filter in hello WHERE clause is applied on hello source tooretrieve a subset of JSON documents.</span></span> <span data-ttu-id="bf3c8-174">Finalmente, a cláusula SELECT Olá é usada tooproject Olá solicitado valores JSON em Olá selecione lista.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-174">Finally, hello SELECT clause is used tooproject hello requested JSON values in hello select list.</span></span>

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <span data-ttu-id="bf3c8-175"><a id="FromClause"></a>Cláusula FROM</span><span class="sxs-lookup"><span data-stu-id="bf3c8-175"><a id="FromClause"></a>FROM clause</span></span>
<span data-ttu-id="bf3c8-176">Olá `FROM <from_specification>` cláusula é opcional, a menos que fonte Olá é filtrada ou projetado posteriormente na consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-176">hello `FROM <from_specification>` clause is optional unless hello source is filtered or projected later in hello query.</span></span> <span data-ttu-id="bf3c8-177">Olá finalidade essa cláusula é toospecify fonte de dados de saudação após a qual Olá consulta deve operar.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-177">hello purpose of this clause is toospecify hello data source upon which hello query must operate.</span></span> <span data-ttu-id="bf3c8-178">Normalmente coleção inteira de saudação é origem hello, mas você pode especificar um subconjunto da coleção de saudação em vez disso.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-178">Commonly hello whole collection is hello source, but one can specify a subset of hello collection instead.</span></span> 

<span data-ttu-id="bf3c8-179">Uma consulta como `SELECT * FROM Families` indica que a coleção inteira de famílias Olá é origem Olá sobre quais tooenumerate.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-179">A query like `SELECT * FROM Families` indicates that hello entire Families collection is hello source over which tooenumerate.</span></span> <span data-ttu-id="bf3c8-180">Um identificador especial raiz pode ser usado toorepresent Olá coleção em vez de usar o nome da coleção hello.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-180">A special identifier ROOT can be used toorepresent hello collection instead of using hello collection name.</span></span> <span data-ttu-id="bf3c8-181">Olá lista a seguir contém regras de saudação que são impostas por consulta:</span><span class="sxs-lookup"><span data-stu-id="bf3c8-181">hello following list contains hello rules that are enforced per query:</span></span>

* <span data-ttu-id="bf3c8-182">coleção de saudação pode ser um alias, como `SELECT f.id FROM Families AS f` ou simplesmente `SELECT f.id FROM Families f`.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-182">hello collection can be aliased, such as `SELECT f.id FROM Families AS f` or simply `SELECT f.id FROM Families f`.</span></span> <span data-ttu-id="bf3c8-183">Aqui `f` é equivalente a saudação `Families`.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-183">Here `f` is hello equivalent of `Families`.</span></span> <span data-ttu-id="bf3c8-184">`AS`é um identificador de saudação tooalias palavra-chave opcional.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-184">`AS` is an optional keyword tooalias hello identifier.</span></span>
* <span data-ttu-id="bf3c8-185">Uma vez um alias, origem Olá não pode ser associada.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-185">Once aliased, hello original source cannot be bound.</span></span> <span data-ttu-id="bf3c8-186">Por exemplo, `SELECT Families.id FROM Families f` é sintaticamente inválida, pois o identificador de hello "Famílias" não pode ser resolvido mais.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-186">For example, `SELECT Families.id FROM Families f` is syntactically invalid since hello identifier "Families" cannot be resolved anymore.</span></span>
* <span data-ttu-id="bf3c8-187">Todas as propriedades que precisar toobe referenciado devem ser totalmente qualificadas.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-187">All properties that need toobe referenced must be fully qualified.</span></span> <span data-ttu-id="bf3c8-188">Na ausência de saudação do cumprimento de esquema estrita, isso é imposto tooavoid associações ambíguas.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-188">In hello absence of strict schema adherence, this is enforced tooavoid any ambiguous bindings.</span></span> <span data-ttu-id="bf3c8-189">Portanto, `SELECT id FROM Families f` é sintaticamente inválida como propriedade Olá `id` não está associado.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-189">Therefore, `SELECT id FROM Families f` is syntactically invalid since hello property `id` is not bound.</span></span>

### <a name="subdocuments"></a><span data-ttu-id="bf3c8-190">Subdocumentos</span><span class="sxs-lookup"><span data-stu-id="bf3c8-190">Subdocuments</span></span>
<span data-ttu-id="bf3c8-191">origem Olá também pode ser o subconjunto menor reduzidos tooa.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-191">hello source can also be reduced tooa smaller subset.</span></span> <span data-ttu-id="bf3c8-192">Por exemplo, tooenumerating apenas uma subárvore de cada documento, subroot Olá poderá se tornar fonte hello, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="bf3c8-192">For instance, tooenumerating only a subtree in each document, hello subroot could then become hello source, as shown in hello following example:</span></span>

<span data-ttu-id="bf3c8-193">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-193">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="bf3c8-194">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-194">**Results**</span></span>  

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

<span data-ttu-id="bf3c8-195">Enquanto Olá acima de exemplo usado uma matriz como origem de Olá, um objeto também pode ser usado como origem de saudação, que é o que é mostrado no exemplo a seguir de saudação: qualquer valor JSON válido que pode ser encontrado na origem da saudação (não indefinido) é considerado para inclusão no resultado de saudação do consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-195">While hello above example used an array as hello source, an object could also be used as hello source, which is what's shown in hello following example: Any valid JSON value (not undefined) that can be found in hello source is considered for inclusion in hello result of hello query.</span></span> <span data-ttu-id="bf3c8-196">Se não tem algumas famílias um `address.state` valor, eles são excluídos no resultado de consulta hello.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-196">If some families don’t have an `address.state` value, they are excluded in hello query result.</span></span>

<span data-ttu-id="bf3c8-197">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-197">**Query**</span></span>

    SELECT * 
    FROM Families.address.state

<span data-ttu-id="bf3c8-198">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-198">**Results**</span></span>

    [
      "WA", 
      "NY"
    ]


## <span data-ttu-id="bf3c8-199"><a id="WhereClause"></a>Cláusula WHERE</span><span class="sxs-lookup"><span data-stu-id="bf3c8-199"><a id="WhereClause"></a>WHERE clause</span></span>
<span data-ttu-id="bf3c8-200">Olá cláusula WHERE (**`WHERE <filter_condition>`**) é opcional.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-200">hello WHERE clause (**`WHERE <filter_condition>`**) is optional.</span></span> <span data-ttu-id="bf3c8-201">Ele especifica Olá condições que os documentos JSON Olá fornecidos pela fonte de saudação devem atender em ordem toobe incluído como parte do resultado de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-201">It specifies hello condition(s) that hello JSON documents provided by hello source must satisfy in order toobe included as part of hello result.</span></span> <span data-ttu-id="bf3c8-202">Qualquer documento JSON deve ser avaliada Olá especificado condições muito "true" toobe considerado para resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-202">Any JSON document must evaluate hello specified conditions too"true" toobe considered for hello result.</span></span> <span data-ttu-id="bf3c8-203">Olá onde cláusula é usada pela camada de índice Olá em ordem toodetermine Olá absoluto subconjunto menor de documentos de origem que podem fazer parte do resultado de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-203">hello WHERE clause is used by hello index layer in order toodetermine hello absolute smallest subset of source documents that can be part of hello result.</span></span> 

<span data-ttu-id="bf3c8-204">Olá, consulta a seguir solicita documentos que contêm uma propriedade de nome cujo valor é `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-204">hello following query requests documents that contain a name property whose value is `AndersenFamily`.</span></span> <span data-ttu-id="bf3c8-205">Qualquer outro documento que não tem uma propriedade de nome, ou onde o valor de saudação não corresponde `AndersenFamily` é excluído.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-205">Any other document that does not have a name property, or where hello value does not match `AndersenFamily` is excluded.</span></span> 

<span data-ttu-id="bf3c8-206">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-206">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="bf3c8-207">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-207">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


<span data-ttu-id="bf3c8-208">exemplo de Hello anterior mostrou uma consulta de igualdade simples.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-208">hello previous example showed a simple equality query.</span></span> <span data-ttu-id="bf3c8-209">O SQL da API do DocumentDB também dá suporte a diversas expressões escalares.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-209">DocumentDB API SQL also supports a variety of scalar expressions.</span></span> <span data-ttu-id="bf3c8-210">Olá mais comumente usada são expressões binário e unário.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-210">hello most commonly used are binary and unary expressions.</span></span> <span data-ttu-id="bf3c8-211">Referências de propriedade do objeto JSON de origem Olá também são expressões válidas.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-211">Property references from hello source JSON object are also valid expressions.</span></span> 

<span data-ttu-id="bf3c8-212">Olá operadores binários a seguir têm suporte atualmente e pode ser usado em consultas, conforme mostrado nos exemplos a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="bf3c8-212">hello following binary operators are currently supported and can be used in queries as shown in hello following examples:</span></span>  

<table>
<tr>
<td><span data-ttu-id="bf3c8-213">Aritmético</span><span class="sxs-lookup"><span data-stu-id="bf3c8-213">Arithmetic</span></span></td>    
<td><span data-ttu-id="bf3c8-214">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="bf3c8-214">+,-,*,/,%</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="bf3c8-215">Bit a bit</span><span class="sxs-lookup"><span data-stu-id="bf3c8-215">Bitwise</span></span></td>    
<td><span data-ttu-id="bf3c8-216">|, &, ^, <<, >>, >>> (deslocamento à direita com preenchimento com zero)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-216">|, &, ^, <<, >>, >>> (zero-fill right shift)</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="bf3c8-217">Lógico</span><span class="sxs-lookup"><span data-stu-id="bf3c8-217">Logical</span></span></td>
<td><span data-ttu-id="bf3c8-218">AND, OR, NOT</span><span class="sxs-lookup"><span data-stu-id="bf3c8-218">AND, OR, NOT</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="bf3c8-219">Comparação</span><span class="sxs-lookup"><span data-stu-id="bf3c8-219">Comparison</span></span></td>    
<td><span data-ttu-id="bf3c8-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span><span class="sxs-lookup"><span data-stu-id="bf3c8-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="bf3c8-221">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="bf3c8-221">String</span></span></td>    
<td><span data-ttu-id="bf3c8-222">|| (concatenado)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-222">|| (concatenate)</span></span></td>
</tr>
</table>  


<span data-ttu-id="bf3c8-223">Vejamos algumas consultas que usam valores binários.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-223">Let’s take a look at some queries using binary operators.</span></span>

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


<span data-ttu-id="bf3c8-224">Olá operadores unários +,-, ~ não também têm suporte e podem ser usados em consultas, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="bf3c8-224">hello unary operators +,-, ~ and NOT are also supported, and can be used inside queries as shown in hello following example:</span></span>

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



<span data-ttu-id="bf3c8-225">Além disso operadores unários e de toobinary, referências de propriedade também são permitidas.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-225">In addition toobinary and unary operators, property references are also allowed.</span></span> <span data-ttu-id="bf3c8-226">Por exemplo, `SELECT * FROM Families f WHERE f.isRegistered` retorna Olá documento JSON que contém a propriedade Olá `isRegistered` onde o valor da propriedade Olá é igual toohello JSON `true` valor.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-226">For example, `SELECT * FROM Families f WHERE f.isRegistered` returns hello JSON document containing hello property `isRegistered` where hello property's value is equal toohello JSON `true` value.</span></span> <span data-ttu-id="bf3c8-227">Quaisquer outros valores (false, null, indefinido, `<number>`, `<string>`, `<object>`, `<array>`, etc.) leva toohello documento de origem que está sendo excluído do resultado de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-227">Any other values (false, null, Undefined, `<number>`, `<string>`, `<object>`, `<array>`, etc.) leads toohello source document being excluded from hello result.</span></span> 

### <a name="equality-and-comparison-operators"></a><span data-ttu-id="bf3c8-228">Operadores de igualdade e de comparação</span><span class="sxs-lookup"><span data-stu-id="bf3c8-228">Equality and comparison operators</span></span>
<span data-ttu-id="bf3c8-229">Olá tabela a seguir mostra Olá resultado de comparações de igualdade em documentos API SQL entre quaisquer dois tipos JSON.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-229">hello following table shows hello result of equality comparisons in DocumentDB API SQL between any two JSON types.</span></span>

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top"><span data-ttu-id="bf3c8-230">
            <strong>Op</strong>
         </span><span class="sxs-lookup"><span data-stu-id="bf3c8-230">
            <strong>Op</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="bf3c8-231">
            <strong>Indefinido</strong>
         </span><span class="sxs-lookup"><span data-stu-id="bf3c8-231">
            <strong>Undefined</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="bf3c8-232">
            <strong>Nulo</strong>
         </span><span class="sxs-lookup"><span data-stu-id="bf3c8-232">
            <strong>Null</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="bf3c8-233">
            <strong>Booliano</strong>
         </span><span class="sxs-lookup"><span data-stu-id="bf3c8-233">
            <strong>Boolean</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="bf3c8-234">
            <strong>Número</strong>
         </span><span class="sxs-lookup"><span data-stu-id="bf3c8-234">
            <strong>Number</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="bf3c8-235">
            <strong>Cadeia de caracteres</strong>
         </span><span class="sxs-lookup"><span data-stu-id="bf3c8-235">
            <strong>String</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="bf3c8-236">
            <strong>Objeto</strong>
         </span><span class="sxs-lookup"><span data-stu-id="bf3c8-236">
            <strong>Object</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="bf3c8-237">
            <strong>Matriz</strong>
         </span><span class="sxs-lookup"><span data-stu-id="bf3c8-237">
            <strong>Array</strong>
         </span></span></td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="bf3c8-238">
            <strong>Indefinido<strong>
         </span><span class="sxs-lookup"><span data-stu-id="bf3c8-238">
            <strong>Undefined<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="bf3c8-239">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-239">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-240">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-240">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-241">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-241">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-242">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-242">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-243">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-243">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-244">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-244">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-245">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-245">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="bf3c8-246">
            <strong>Nulo<strong>
         </span><span class="sxs-lookup"><span data-stu-id="bf3c8-246">
            <strong>Null<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="bf3c8-247">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-247">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="bf3c8-248">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="bf3c8-248">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="bf3c8-249">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-249">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-250">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-250">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-251">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-251">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-252">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-252">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-253">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-253">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="bf3c8-254">
            <strong>Booliano<strong>
         </span><span class="sxs-lookup"><span data-stu-id="bf3c8-254">
            <strong>Boolean<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="bf3c8-255">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-255">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-256">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-256">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="bf3c8-257">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="bf3c8-257">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="bf3c8-258">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-258">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-259">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-259">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-260">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-260">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-261">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-261">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="bf3c8-262">
            <strong>Número<strong>
         </span><span class="sxs-lookup"><span data-stu-id="bf3c8-262">
            <strong>Number<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="bf3c8-263">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-263">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-264">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-264">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-265">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-265">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="bf3c8-266">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="bf3c8-266">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="bf3c8-267">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-267">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-268">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-268">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-269">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-269">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="bf3c8-270">
            <strong>Cadeia de caracteres<strong>
         </span><span class="sxs-lookup"><span data-stu-id="bf3c8-270">
            <strong>String<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="bf3c8-271">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-271">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-272">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-272">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-273">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-273">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-274">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-274">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="bf3c8-275">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="bf3c8-275">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="bf3c8-276">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-276">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-277">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-277">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="bf3c8-278">
            <strong>Objeto<strong>
         </span><span class="sxs-lookup"><span data-stu-id="bf3c8-278">
            <strong>Object<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="bf3c8-279">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-279">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-280">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-280">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-281">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-281">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-282">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-282">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-283">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-283">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="bf3c8-284">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="bf3c8-284">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="bf3c8-285">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-285">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="bf3c8-286">
            <strong>Matriz<strong>
         </span><span class="sxs-lookup"><span data-stu-id="bf3c8-286">
            <strong>Array<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="bf3c8-287">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-287">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-288">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-288">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-289">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-289">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-290">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-290">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-291">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-291">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="bf3c8-292">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-292">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="bf3c8-293">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="bf3c8-293">
            <strong>OK</strong>
         </span></span></td>
      </tr>
   </tbody>
</table>

<span data-ttu-id="bf3c8-294">Para outros operadores de comparação, como >, > =,! =, < e < =, hello seguintes regras se aplicam:</span><span class="sxs-lookup"><span data-stu-id="bf3c8-294">For other comparison operators such as >, >=, !=, < and <=, hello following rules apply:</span></span>   

* <span data-ttu-id="bf3c8-295">Comparação entre resultados de tipos em Indefinido.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-295">Comparison across types results in Undefined.</span></span>
* <span data-ttu-id="bf3c8-296">Comparação entre resultados de dois objetos ou duas matrizes em Indefinido.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-296">Comparison between two objects or two arrays results in Undefined.</span></span>   

<span data-ttu-id="bf3c8-297">Se o resultado de saudação de expressão escalar do hello no filtro de saudação é indefinido, documento correspondente Olá poderia não ser incluído no resultado de hello, pois indefinido muito "true" logicamente não serão iguais.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-297">If hello result of hello scalar expression in hello filter is Undefined, hello corresponding document would not be included in hello result, since Undefined doesn't logically equate too"true".</span></span>

### <a name="between-keyword"></a><span data-ttu-id="bf3c8-298">Palavra-chave BETWEEN</span><span class="sxs-lookup"><span data-stu-id="bf3c8-298">BETWEEN keyword</span></span>
<span data-ttu-id="bf3c8-299">Você também pode usar consultas de tooexpress de palavra-chave do hello BETWEEN em intervalos de valores, como no ANSI SQL.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-299">You can also use hello BETWEEN keyword tooexpress queries against ranges of values like in ANSI SQL.</span></span> <span data-ttu-id="bf3c8-300">BETWEEN pode ser usado em cadeias de caracteres ou números.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-300">BETWEEN can be used against strings or numbers.</span></span>

<span data-ttu-id="bf3c8-301">Por exemplo, esta consulta retorna todos os documentos de família em qual Olá classificação de seu primeiro filho é entre 1-5 (ambos incluídos).</span><span class="sxs-lookup"><span data-stu-id="bf3c8-301">For example, this query returns all family documents in which hello first child's grade is between 1-5 (both inclusive).</span></span> 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

<span data-ttu-id="bf3c8-302">Ao contrário no ANSI SQL, você também pode usar Olá BETWEEN cláusula na cláusula FROM de saudação como no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-302">Unlike in ANSI-SQL, you can also use hello BETWEEN clause in hello FROM clause like in hello following example.</span></span>

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

<span data-ttu-id="bf3c8-303">Para tempos de execução de consulta mais rápidos, lembre-se toocreate uma política de indexação que usa um tipo de índice de intervalo em relação a qualquer propriedades ou caminhos numéricos que são filtradas na cláusula BETWEEN hello.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-303">For faster query execution times, remember toocreate an indexing policy that uses a range index type against any numeric properties/paths that are filtered in hello BETWEEN clause.</span></span> 

<span data-ttu-id="bf3c8-304">Olá principal diferença entre usando BETWEEN na API de documentos e ANSI SQL é que você pode expressar consultas de intervalo em Propriedades de tipos mistos – por exemplo, você pode ter "nota" ser um número (5) em alguns documentos e cadeias de caracteres em outros ("grade4").</span><span class="sxs-lookup"><span data-stu-id="bf3c8-304">hello main difference between using BETWEEN in DocumentDB API and ANSI SQL is that you can express range queries against properties of mixed types – for example, you might have "grade" be a number (5) in some documents and strings in others ("grade4").</span></span> <span data-ttu-id="bf3c8-305">Nesses casos, como em JavaScript, uma comparação entre dois resultados de tipos diferentes de "indefinidos" e documento hello será ignorada.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-305">In these cases, like in JavaScript, a comparison between two different types results in "undefined", and hello document will be skipped.</span></span>

### <a name="logical-and-or-and-not-operators"></a><span data-ttu-id="bf3c8-306">Operadores lógicos (AND, OR e NOT)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-306">Logical (AND, OR and NOT) operators</span></span>
<span data-ttu-id="bf3c8-307">Operadores lógicos funcionam em valores boolianos.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-307">Logical operators operate on Boolean values.</span></span> <span data-ttu-id="bf3c8-308">Olá tabelas lógicas de verdade para esses operadores são mostradas no hello tabelas a seguir.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-308">hello logical truth tables for these operators are shown in hello following tables.</span></span>

| <span data-ttu-id="bf3c8-309">OU</span><span class="sxs-lookup"><span data-stu-id="bf3c8-309">OR</span></span> | <span data-ttu-id="bf3c8-310">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="bf3c8-310">True</span></span> | <span data-ttu-id="bf3c8-311">Falso</span><span class="sxs-lookup"><span data-stu-id="bf3c8-311">False</span></span> | <span data-ttu-id="bf3c8-312">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-312">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="bf3c8-313">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="bf3c8-313">True</span></span> |<span data-ttu-id="bf3c8-314">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="bf3c8-314">True</span></span> |<span data-ttu-id="bf3c8-315">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="bf3c8-315">True</span></span> |<span data-ttu-id="bf3c8-316">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="bf3c8-316">True</span></span> |
| <span data-ttu-id="bf3c8-317">Falso</span><span class="sxs-lookup"><span data-stu-id="bf3c8-317">False</span></span> |<span data-ttu-id="bf3c8-318">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="bf3c8-318">True</span></span> |<span data-ttu-id="bf3c8-319">Falso</span><span class="sxs-lookup"><span data-stu-id="bf3c8-319">False</span></span> |<span data-ttu-id="bf3c8-320">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-320">Undefined</span></span> |
| <span data-ttu-id="bf3c8-321">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-321">Undefined</span></span> |<span data-ttu-id="bf3c8-322">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="bf3c8-322">True</span></span> |<span data-ttu-id="bf3c8-323">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-323">Undefined</span></span> |<span data-ttu-id="bf3c8-324">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-324">Undefined</span></span> |

| <span data-ttu-id="bf3c8-325">E</span><span class="sxs-lookup"><span data-stu-id="bf3c8-325">AND</span></span> | <span data-ttu-id="bf3c8-326">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="bf3c8-326">True</span></span> | <span data-ttu-id="bf3c8-327">Falso</span><span class="sxs-lookup"><span data-stu-id="bf3c8-327">False</span></span> | <span data-ttu-id="bf3c8-328">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-328">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="bf3c8-329">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="bf3c8-329">True</span></span> |<span data-ttu-id="bf3c8-330">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="bf3c8-330">True</span></span> |<span data-ttu-id="bf3c8-331">Falso</span><span class="sxs-lookup"><span data-stu-id="bf3c8-331">False</span></span> |<span data-ttu-id="bf3c8-332">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-332">Undefined</span></span> |
| <span data-ttu-id="bf3c8-333">Falso</span><span class="sxs-lookup"><span data-stu-id="bf3c8-333">False</span></span> |<span data-ttu-id="bf3c8-334">Falso</span><span class="sxs-lookup"><span data-stu-id="bf3c8-334">False</span></span> |<span data-ttu-id="bf3c8-335">Falso</span><span class="sxs-lookup"><span data-stu-id="bf3c8-335">False</span></span> |<span data-ttu-id="bf3c8-336">Falso</span><span class="sxs-lookup"><span data-stu-id="bf3c8-336">False</span></span> |
| <span data-ttu-id="bf3c8-337">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-337">Undefined</span></span> |<span data-ttu-id="bf3c8-338">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-338">Undefined</span></span> |<span data-ttu-id="bf3c8-339">Falso</span><span class="sxs-lookup"><span data-stu-id="bf3c8-339">False</span></span> |<span data-ttu-id="bf3c8-340">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-340">Undefined</span></span> |

| <span data-ttu-id="bf3c8-341">NÃO</span><span class="sxs-lookup"><span data-stu-id="bf3c8-341">NOT</span></span> |  |
| --- | --- |
| <span data-ttu-id="bf3c8-342">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="bf3c8-342">True</span></span> |<span data-ttu-id="bf3c8-343">Falso</span><span class="sxs-lookup"><span data-stu-id="bf3c8-343">False</span></span> |
| <span data-ttu-id="bf3c8-344">Falso</span><span class="sxs-lookup"><span data-stu-id="bf3c8-344">False</span></span> |<span data-ttu-id="bf3c8-345">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="bf3c8-345">True</span></span> |
| <span data-ttu-id="bf3c8-346">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-346">Undefined</span></span> |<span data-ttu-id="bf3c8-347">Indefinido</span><span class="sxs-lookup"><span data-stu-id="bf3c8-347">Undefined</span></span> |

### <a name="in-keyword"></a><span data-ttu-id="bf3c8-348">Palavra-chave IN</span><span class="sxs-lookup"><span data-stu-id="bf3c8-348">IN keyword</span></span>
<span data-ttu-id="bf3c8-349">palavra-chave IN de saudação pode ser usado toocheck se um valor especificado corresponde a qualquer valor em uma lista.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-349">hello IN keyword can be used toocheck whether a specified value matches any value in a list.</span></span> <span data-ttu-id="bf3c8-350">Por exemplo, esta consulta retorna todos os documentos família onde a id de saudação é "WakefieldFamily" ou "AndersenFamily".</span><span class="sxs-lookup"><span data-stu-id="bf3c8-350">For example, this query returns all family documents where hello id is one of "WakefieldFamily" or "AndersenFamily".</span></span> 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

<span data-ttu-id="bf3c8-351">Este exemplo retorna todos os documentos em que o estado de saudação é qualquer Olá especificado valores.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-351">This example returns all documents where hello state is any of hello specified values.</span></span>

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a><span data-ttu-id="bf3c8-352">Operadores Ternário (?) e de União (??)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-352">Ternary (?) and Coalesce (??) operators</span></span>
<span data-ttu-id="bf3c8-353">operadores ternários e adesão de saudação podem ser expressões condicionais toobuild usado, semelhante toopopular linguagens como c# e JavaScript de programação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-353">hello Ternary and Coalesce operators can be used toobuild conditional expressions, similar toopopular programming languages like C# and JavaScript.</span></span> 

<span data-ttu-id="bf3c8-354">operador ternário (?) de saudação pode ser muito útil quando a criação de novas propriedades JSON no hello surgir.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-354">hello Ternary (?) operator can be very handy when constructing new JSON properties on hello fly.</span></span> <span data-ttu-id="bf3c8-355">Por exemplo, agora você pode criar níveis de classe consultas tooclassify Olá em um formato legível humano como iniciante/intermediário/Avançado conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-355">For example, now you can write queries tooclassify hello class levels into a human readable form like Beginner/Intermediate/Advanced as shown below.</span></span>

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

<span data-ttu-id="bf3c8-356">Você também pode aninhar um operador de toohello de chamadas hello como na consulta de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-356">You can also nest hello calls toohello operator like in hello query below.</span></span>

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

<span data-ttu-id="bf3c8-357">Como com outros operadores de consulta, se hello propriedades de referência em expressão condicional Olá estão ausentes em qualquer documento, ou se Olá tipos que estão sendo comparados forem diferentes, em seguida, esses documentos são excluídos nos resultados da consulta hello.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-357">As with other query operators, if hello referenced properties in hello conditional expression are missing in any document, or if hello types being compared are different, then those documents are excluded in hello query results.</span></span>

<span data-ttu-id="bf3c8-358">Olá adesão (?) pode ser usada para tooefficiently Verificar presença de saudação de uma propriedade (também conhecido como</span><span class="sxs-lookup"><span data-stu-id="bf3c8-358">hello Coalesce (??) operator can be used tooefficiently check for hello presence of a property (a.k.a.</span></span> <span data-ttu-id="bf3c8-359">é definido) em um documento.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-359">is defined) in a document.</span></span> <span data-ttu-id="bf3c8-360">Isso é útil ao consultar dados semiestruturados ou dados de tipos mistos.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-360">This is useful when querying against semi-structured or data of mixed types.</span></span> <span data-ttu-id="bf3c8-361">Por exemplo, esta consulta retorna lastName"hello" se estiver presente, ou hello "surname" se não estiver presente.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-361">For example, this query returns hello "lastName" if present, or hello "surname" if it isn't present.</span></span>

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <span data-ttu-id="bf3c8-362"><a id="EscapingReservedKeywords"></a>Acessador de propriedade entre aspas</span><span class="sxs-lookup"><span data-stu-id="bf3c8-362"><a id="EscapingReservedKeywords"></a>Quoted property accessor</span></span>
<span data-ttu-id="bf3c8-363">Você também pode acessar as propriedades usando o operador de propriedade entre aspas Olá `[]`.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-363">You can also access properties using hello quoted property operator `[]`.</span></span> <span data-ttu-id="bf3c8-364">Por exemplo: `SELECT c.grade` and `SELECT c["grade"]` são equivalentes.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-364">For example, `SELECT c.grade` and `SELECT c["grade"]` are equivalent.</span></span> <span data-ttu-id="bf3c8-365">Essa sintaxe é útil quando você precisar tooescape uma propriedade que contém espaços, caracteres especiais, ou acontece Olá tooshare mesmo nome como uma palavra reservada ou uma palavra-chave SQL.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-365">This syntax is useful when you need tooescape a property that contains spaces, special characters, or happens tooshare hello same name as a SQL keyword or reserved word.</span></span>

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <span data-ttu-id="bf3c8-366"><a id="SelectClause"></a>Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="bf3c8-366"><a id="SelectClause"></a>SELECT clause</span></span>
<span data-ttu-id="bf3c8-367">cláusula SELECT Hello (**`SELECT <select_list>`**) é obrigatório e especifica quais valores são recuperados da consulta hello, exatamente como no ANSI SQL.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-367">hello SELECT clause (**`SELECT <select_list>`**) is mandatory and specifies what values are retrieved from hello query, just like in ANSI-SQL.</span></span> <span data-ttu-id="bf3c8-368">subconjunto Olá filtrado sobre documentos de origem Olá são passadas em fase de projeção hello, onde Olá especificados valores JSON são recuperados e um novo objeto JSON é construído, para cada entrada passada para ele.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-368">hello subset that's been filtered on top of hello source documents are passed onto hello projection phase, where hello specified JSON values are retrieved and a new JSON object is constructed, for each input passed onto it.</span></span> 

<span data-ttu-id="bf3c8-369">saudação de exemplo a seguir mostra uma consulta SELECT típica.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-369">hello following example shows a typical SELECT query.</span></span> 

<span data-ttu-id="bf3c8-370">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-370">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="bf3c8-371">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-371">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a><span data-ttu-id="bf3c8-372">Propriedades aninhadas</span><span class="sxs-lookup"><span data-stu-id="bf3c8-372">Nested properties</span></span>
<span data-ttu-id="bf3c8-373">Em Olá exemplo a seguir, está projetando duas propriedades aninhadas `f.address.state` e `f.address.city`.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-373">In hello following example, we are projecting two nested properties `f.address.state` and `f.address.city`.</span></span>

<span data-ttu-id="bf3c8-374">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-374">**Query**</span></span>

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="bf3c8-375">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-375">**Results**</span></span>

    [{
      "state": "WA", 
      "city": "seattle"
    }]


<span data-ttu-id="bf3c8-376">Projeção também oferece suporte a expressões de JSON conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="bf3c8-376">Projection also supports JSON expressions as shown in hello following example:</span></span>

<span data-ttu-id="bf3c8-377">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-377">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="bf3c8-378">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-378">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


<span data-ttu-id="bf3c8-379">Vamos dar uma olhada na função de saudação do `$1` aqui.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-379">Let's look at hello role of `$1` here.</span></span> <span data-ttu-id="bf3c8-380">Olá `SELECT` cláusula precisa toocreate um objeto JSON e já que nenhuma chave é fornecida, podemos usar nomes de variável implícita argumento começando com `$1`.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-380">hello `SELECT` clause needs toocreate a JSON object and since no key is provided, we use implicit argument variable names starting with `$1`.</span></span> <span data-ttu-id="bf3c8-381">Por exemplo, esta consulta retorna duas variáveis de argumento implícito, rotuladas como `$1` and `$2`.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-381">For example, this query returns two implicit argument variables, labeled `$1` and `$2`.</span></span>

<span data-ttu-id="bf3c8-382">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-382">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="bf3c8-383">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-383">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a><span data-ttu-id="bf3c8-384">Atribuição de alias</span><span class="sxs-lookup"><span data-stu-id="bf3c8-384">Aliasing</span></span>
<span data-ttu-id="bf3c8-385">Agora vamos estender o exemplo de hello acima com o alias explícita de valores.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-385">Now let's extend hello example above with explicit aliasing of values.</span></span> <span data-ttu-id="bf3c8-386">COMO é Olá palavra-chave usada para o alias.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-386">AS is hello keyword used for aliasing.</span></span> <span data-ttu-id="bf3c8-387">É opcional, conforme mostrado durante a projeção Olá segundo valor como `NameInfo`.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-387">It's optional as shown while projecting hello second value as `NameInfo`.</span></span> 

<span data-ttu-id="bf3c8-388">No caso de uma consulta tem duas propriedades com hello mesmo nome, o alias devem ser usado toorename Olá propriedades uma ou ambas, para que suas ambiguidades são desfeitas no hello projetado resultado.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-388">In case a query has two properties with hello same name, aliasing must be used toorename one or both of hello properties so that they are disambiguated in hello projected result.</span></span>

<span data-ttu-id="bf3c8-389">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-389">**Query**</span></span>

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="bf3c8-390">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-390">**Results**</span></span>

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a><span data-ttu-id="bf3c8-391">Expressões escalares</span><span class="sxs-lookup"><span data-stu-id="bf3c8-391">Scalar expressions</span></span>
<span data-ttu-id="bf3c8-392">Além do tooproperty faz referência, a cláusula SELECT Olá também oferece suporte a expressões escalares como constantes, expressões aritméticas, expressões lógicas, etc. Por exemplo, vejamos uma consulta simples do tipo "Olá mundo".</span><span class="sxs-lookup"><span data-stu-id="bf3c8-392">In addition tooproperty references, hello SELECT clause also supports scalar expressions like constants, arithmetic expressions, logical expressions, etc. For example, here's a simple "Hello World" query.</span></span>

<span data-ttu-id="bf3c8-393">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-393">**Query**</span></span>

    SELECT "Hello World"

<span data-ttu-id="bf3c8-394">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-394">**Results**</span></span>

    [{
      "$1": "Hello World"
    }]


<span data-ttu-id="bf3c8-395">Este é um exemplo mais complexo que usa uma expressão escalar.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-395">Here's a more complex example that uses a scalar expression.</span></span>

<span data-ttu-id="bf3c8-396">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-396">**Query**</span></span>

    SELECT ((2 + 11 % 7)-2)/3    

<span data-ttu-id="bf3c8-397">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-397">**Results**</span></span>

    [{
      "$1": 1.33333
    }]


<span data-ttu-id="bf3c8-398">Olá exemplo a seguir, o resultado de Olá da expressão escalar Olá é um valor booleano.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-398">In hello following example, hello result of hello scalar expression is a Boolean.</span></span>

<span data-ttu-id="bf3c8-399">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-399">**Query**</span></span>

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

<span data-ttu-id="bf3c8-400">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-400">**Results**</span></span>

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a><span data-ttu-id="bf3c8-401">Criação de objeto e de matriz</span><span class="sxs-lookup"><span data-stu-id="bf3c8-401">Object and array creation</span></span>
<span data-ttu-id="bf3c8-402">Outro recurso fundamental do SQL da API do DocumentDB é a criação de matriz/objeto.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-402">Another key feature of DocumentDB API SQL is array/object creation.</span></span> <span data-ttu-id="bf3c8-403">No exemplo anterior de saudação, observe que criamos um novo objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-403">In hello previous example, note that we created a new JSON object.</span></span> <span data-ttu-id="bf3c8-404">Da mesma forma, um também pode construir matrizes, conforme mostrado no hello exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf3c8-404">Similarly, one can also construct arrays as shown in hello following examples:</span></span>

<span data-ttu-id="bf3c8-405">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-405">**Query**</span></span>

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

<span data-ttu-id="bf3c8-406">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-406">**Results**</span></span>  

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

### <span data-ttu-id="bf3c8-407"><a id="ValueKeyword"></a>Palavra-chave VALUE</span><span class="sxs-lookup"><span data-stu-id="bf3c8-407"><a id="ValueKeyword"></a>VALUE keyword</span></span>
<span data-ttu-id="bf3c8-408">Olá **valor** palavra-chave fornece um valor do modo tooreturn JSON.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-408">hello **VALUE** keyword provides a way tooreturn JSON value.</span></span> <span data-ttu-id="bf3c8-409">Por exemplo, consulta Olá mostrada a seguir retorna Olá escalar `"Hello World"` em vez de `{$1: "Hello World"}`.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-409">For example, hello query shown below returns hello scalar `"Hello World"` instead of `{$1: "Hello World"}`.</span></span>

<span data-ttu-id="bf3c8-410">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-410">**Query**</span></span>

    SELECT VALUE "Hello World"

<span data-ttu-id="bf3c8-411">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-411">**Results**</span></span>

    [
      "Hello World"
    ]


<span data-ttu-id="bf3c8-412">Olá, consulta a seguir retorna valor JSON de saudação sem Olá `"address"` rótulo nos resultados da saudação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-412">hello following query returns hello JSON value without hello `"address"` label in hello results.</span></span>

<span data-ttu-id="bf3c8-413">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-413">**Query**</span></span>

    SELECT VALUE f.address
    FROM Families f    

<span data-ttu-id="bf3c8-414">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-414">**Results**</span></span>  

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

<span data-ttu-id="bf3c8-415">Olá exemplo a seguir estende essa tooshow como valores primitivos de JSON de tooreturn (nível de folha de saudação da árvore JSON Olá).</span><span class="sxs-lookup"><span data-stu-id="bf3c8-415">hello following example extends this tooshow how tooreturn JSON primitive values (hello leaf level of hello JSON tree).</span></span> 

<span data-ttu-id="bf3c8-416">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-416">**Query**</span></span>

    SELECT VALUE f.address.state
    FROM Families f    

<span data-ttu-id="bf3c8-417">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-417">**Results**</span></span>

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a><span data-ttu-id="bf3c8-418">* Operador</span><span class="sxs-lookup"><span data-stu-id="bf3c8-418">* Operator</span></span>
<span data-ttu-id="bf3c8-419">Olá, operador especial (*) é documento de saudação tooproject com suporte como-é.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-419">hello special operator (*) is supported tooproject hello document as-is.</span></span> <span data-ttu-id="bf3c8-420">Quando usado, ele deve ser Olá projetado apenas o campo.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-420">When used, it must be hello only projected field.</span></span> <span data-ttu-id="bf3c8-421">Embora uma consulta como `SELECT * FROM Families f` seja válida, `SELECT VALUE * FROM Families f ` e `SELECT *, f.id FROM Families f ` não são.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-421">While a query like `SELECT * FROM Families f` is valid, `SELECT VALUE * FROM Families f ` and  `SELECT *, f.id FROM Families f ` are not valid.</span></span>

<span data-ttu-id="bf3c8-422">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-422">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="bf3c8-423">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-423">**Results**</span></span>

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

### <span data-ttu-id="bf3c8-424"><a id="TopKeyword"></a>Operador TOP</span><span class="sxs-lookup"><span data-stu-id="bf3c8-424"><a id="TopKeyword"></a>TOP Operator</span></span>
<span data-ttu-id="bf3c8-425">palavra-chave TOP de saudação pode ser usado toolimit Olá número de valores de uma consulta.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-425">hello TOP keyword can be used toolimit hello number of values from a query.</span></span> <span data-ttu-id="bf3c8-426">Quando TOP é usado em conjunto com a cláusula ORDER BY da saudação, o conjunto de resultados de Olá é o primeiro número de N toohello limitado de valores ordenados; Caso contrário, retornará Olá primeiro N número de resultados em uma ordem indefinida.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-426">When TOP is used in conjunction with hello ORDER BY clause, hello result set is limited toohello first N number of ordered values; otherwise, it returns hello first N number of results in an undefined order.</span></span> <span data-ttu-id="bf3c8-427">Como prática recomendada, em uma instrução SELECT, sempre use uma cláusula ORDER BY com a cláusula TOP hello.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-427">As a best practice, in a SELECT statement, always use an ORDER BY clause with hello TOP clause.</span></span> <span data-ttu-id="bf3c8-428">Isso é única forma de saudação toopredictably indicar quais linhas são afetadas por TOP.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-428">This is hello only way toopredictably indicate which rows are affected by TOP.</span></span> 

<span data-ttu-id="bf3c8-429">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-429">**Query**</span></span>

    SELECT TOP 1 * 
    FROM Families f 

<span data-ttu-id="bf3c8-430">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-430">**Results**</span></span>

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

<span data-ttu-id="bf3c8-431">O TOP pode ser usado com um valor constante (conforme mostrado acima) ou com um valor de variável usando consultas parametrizadas.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-431">TOP can be used with a constant value (as shown above) or with a variable value using parameterized queries.</span></span> <span data-ttu-id="bf3c8-432">Para obter mais detalhes, veja as consultas parametrizadas abaixo.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-432">For more details, please see parameterized queries below.</span></span>

### <span data-ttu-id="bf3c8-433"><a id="Aggregates"></a>Funções de agregação</span><span class="sxs-lookup"><span data-stu-id="bf3c8-433"><a id="Aggregates"></a>Aggregate Functions</span></span>
<span data-ttu-id="bf3c8-434">Você também pode executar agregações em Olá `SELECT` cláusula.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-434">You can also perform aggregations in hello `SELECT` clause.</span></span> <span data-ttu-id="bf3c8-435">Funções agregadas executam um cálculo em um conjunto de valores e retornam um único valor.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-435">Aggregate functions perform a calculation on a set of values and return a single value.</span></span> <span data-ttu-id="bf3c8-436">Por exemplo, hello consulta a seguir retorna Olá contagem de família documentos na coleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-436">For example, hello following query returns hello count of family documents within hello collection.</span></span>

<span data-ttu-id="bf3c8-437">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-437">**Query**</span></span>

    SELECT COUNT(1) 
    FROM Families f 

<span data-ttu-id="bf3c8-438">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-438">**Results**</span></span>

    [{
        "$1": 2
    }]

<span data-ttu-id="bf3c8-439">Você também pode retornar valor escalar Olá Olá agregação usando Olá `VALUE` palavra-chave.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-439">You can also return hello scalar value of hello aggregate by using hello `VALUE` keyword.</span></span> <span data-ttu-id="bf3c8-440">Por exemplo, hello consulta a seguir retorna Olá contagem de valores como um único número:</span><span class="sxs-lookup"><span data-stu-id="bf3c8-440">For example, hello following query returns hello count of values as a single number:</span></span>

<span data-ttu-id="bf3c8-441">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-441">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f 

<span data-ttu-id="bf3c8-442">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-442">**Results**</span></span>

    [ 2 ]

<span data-ttu-id="bf3c8-443">Você também pode executar agregações em combinação com filtros.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-443">You can also perform aggregates in combination with filters.</span></span> <span data-ttu-id="bf3c8-444">Por exemplo, hello consulta a seguir retorna Olá contagem de documentos com o endereço de saudação em Olá estado de Washington.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-444">For example, hello following query returns hello count of documents with hello address in hello state of Washington.</span></span>

<span data-ttu-id="bf3c8-445">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-445">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

<span data-ttu-id="bf3c8-446">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-446">**Results**</span></span>

    [ 1 ]

<span data-ttu-id="bf3c8-447">Olá tabela a seguir mostra Olá lista de funções de agregação com suporte na API do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-447">hello following table shows hello list of supported aggregate functions in DocumentDB API.</span></span> <span data-ttu-id="bf3c8-448">`SUM` e `AVG` são executados por meio de valores numéricos, enquanto `COUNT`, `MIN` e `MAX` podem ser executados em relação a números, cadeias de caracteres, Boolianos e nulos.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-448">`SUM` and `AVG` are performed over numeric values, whereas `COUNT`, `MIN`, and `MAX` can be performed over numbers, strings, Booleans, and nulls.</span></span> 

| <span data-ttu-id="bf3c8-449">Uso</span><span class="sxs-lookup"><span data-stu-id="bf3c8-449">Usage</span></span> | <span data-ttu-id="bf3c8-450">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf3c8-450">Description</span></span> |
|-------|-------------|
| <span data-ttu-id="bf3c8-451">COUNT</span><span class="sxs-lookup"><span data-stu-id="bf3c8-451">COUNT</span></span> | <span data-ttu-id="bf3c8-452">Retorna Olá número de itens na expressão de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-452">Returns hello number of items in hello expression.</span></span> |
| <span data-ttu-id="bf3c8-453">SUM</span><span class="sxs-lookup"><span data-stu-id="bf3c8-453">SUM</span></span>   | <span data-ttu-id="bf3c8-454">Retorna Olá soma de todos os valores hello expressão hello.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-454">Returns hello sum of all hello values in hello expression.</span></span> |
| <span data-ttu-id="bf3c8-455">MÍN.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-455">MIN</span></span>   | <span data-ttu-id="bf3c8-456">Retorna Olá valor mínimo na expressão de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-456">Returns hello minimum value in hello expression.</span></span> |
| <span data-ttu-id="bf3c8-457">MÁX.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-457">MAX</span></span>   | <span data-ttu-id="bf3c8-458">Retorna Olá valor máximo na expressão de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-458">Returns hello maximum value in hello expression.</span></span> |
| <span data-ttu-id="bf3c8-459">AVG</span><span class="sxs-lookup"><span data-stu-id="bf3c8-459">AVG</span></span>   | <span data-ttu-id="bf3c8-460">Retorna Olá média dos valores de saudação na expressão de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-460">Returns hello average of hello values in hello expression.</span></span> |

<span data-ttu-id="bf3c8-461">Agregações também podem ser executadas nos resultados de saudação de uma iteração de matriz.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-461">Aggregates can also be performed over hello results of an array iteration.</span></span> <span data-ttu-id="bf3c8-462">Para obter mais informações, consulte [Iteração de matriz em consultas](#Iteration).</span><span class="sxs-lookup"><span data-stu-id="bf3c8-462">For more information, see [Array Iteration in Queries](#Iteration).</span></span>

> [!NOTE]
> <span data-ttu-id="bf3c8-463">Quando usar hello Pesquisador de objetos de consulta do portal do Azure, observe que consultas de agregação podem retornar Olá resultados parcialmente agregados em uma página de consulta.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-463">When using hello Azure portal's Query Explorer, note that aggregation queries may return hello partially aggregated results over a query page.</span></span> <span data-ttu-id="bf3c8-464">Olá SDKs produz um único valor cumulativo em todas as páginas.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-464">hello SDKs produces a single cumulative value across all pages.</span></span> 
> 
> <span data-ttu-id="bf3c8-465">Ordem em consultas de agregação tooperform usando o código, você precisa de SDK .NET 1.12.0, .NET Core SDK 1.1.0 ou Java SDK 1.9.5 ou superior.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-465">In order tooperform aggregation queries using code, you need .NET SDK 1.12.0, .NET Core SDK 1.1.0, or Java SDK 1.9.5 or above.</span></span>    
>

## <span data-ttu-id="bf3c8-466"><a id="OrderByClause"></a>Cláusula ORDER BY</span><span class="sxs-lookup"><span data-stu-id="bf3c8-466"><a id="OrderByClause"></a>ORDER BY clause</span></span>
<span data-ttu-id="bf3c8-467">Como no ANSI-SQL, agora você pode incluir uma cláusula Order By opcional ao realizar consultas.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-467">Like in ANSI-SQL, you can include an optional Order By clause while querying.</span></span> <span data-ttu-id="bf3c8-468">cláusula Olá pode incluir uma opcional Crescente/Decrescente argumento toospecify Olá ordem na qual os resultados devem ser recuperados.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-468">hello clause can include an optional ASC/DESC argument toospecify hello order in which results must be retrieved.</span></span>

<span data-ttu-id="bf3c8-469">Por exemplo, aqui está uma consulta que recupera famílias em ordem de nome de cidade residente hello.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-469">For example, here's a query that retrieves families in order of hello resident city's name.</span></span>

<span data-ttu-id="bf3c8-470">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-470">**Query**</span></span>

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

<span data-ttu-id="bf3c8-471">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-471">**Results**</span></span>

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

<span data-ttu-id="bf3c8-472">E aqui está uma consulta que recupera famílias na ordem da data de criação, que é armazenada como um número que representa Olá tempo, ou seja, tempo decorrido desde 1º de janeiro de 1970 em segundos.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-472">And here's a query that retrieves families in order of creation date, which is stored as a number representing hello epoch time, i.e, elapsed time since Jan 1, 1970 in seconds.</span></span>

<span data-ttu-id="bf3c8-473">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-473">**Query**</span></span>

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

<span data-ttu-id="bf3c8-474">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-474">**Results**</span></span>

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

## <span data-ttu-id="bf3c8-475"><a id="Advanced"></a>Conceitos avançados de banco de dados e consultas SQL</span><span class="sxs-lookup"><span data-stu-id="bf3c8-475"><a id="Advanced"></a>Advanced database concepts and SQL queries</span></span>

### <span data-ttu-id="bf3c8-476"><a id="Iteration"></a>Iteração</span><span class="sxs-lookup"><span data-stu-id="bf3c8-476"><a id="Iteration"></a>Iteration</span></span>
<span data-ttu-id="bf3c8-477">Uma nova construção de foi adicionada via Olá **IN** palavra-chave no suporte do SQL do DocumentDB API tooprovide para iterar em matrizes JSON.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-477">A new construct was added via hello **IN** keyword in DocumentDB API SQL tooprovide support for iterating over JSON arrays.</span></span> <span data-ttu-id="bf3c8-478">origem do Hello FROM dá suporte à iteração.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-478">hello FROM source provides support for iteration.</span></span> <span data-ttu-id="bf3c8-479">Vamos começar com hello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf3c8-479">Let's start with hello following example:</span></span>

<span data-ttu-id="bf3c8-480">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-480">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="bf3c8-481">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-481">**Results**</span></span>  

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

<span data-ttu-id="bf3c8-482">Agora vamos dar uma olhada em outra consulta que executa a iteração por filhos na coleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-482">Now let's look at another query that performs iteration over children in hello collection.</span></span> <span data-ttu-id="bf3c8-483">Observe a diferença Olá Olá matriz de saída.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-483">Note hello difference in hello output array.</span></span> <span data-ttu-id="bf3c8-484">Este exemplo divide `children` e mescla os resultados de saudação em uma única matriz.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-484">This example splits `children` and flattens hello results into a single array.</span></span>  

<span data-ttu-id="bf3c8-485">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-485">**Query**</span></span>

    SELECT * 
    FROM c IN Families.children

<span data-ttu-id="bf3c8-486">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-486">**Results**</span></span>  

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

<span data-ttu-id="bf3c8-487">Isso pode ser mais usado toofilter em cada entrada individual da matriz de saudação conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="bf3c8-487">This can be further used toofilter on each individual entry of hello array as shown in hello following example:</span></span>

<span data-ttu-id="bf3c8-488">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-488">**Query**</span></span>

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

<span data-ttu-id="bf3c8-489">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-489">**Results**</span></span>  

    [{
      "givenName": "Lisa"
    }]

<span data-ttu-id="bf3c8-490">Você também pode executar a agregação sobre o resultado de saudação de iteração de matriz.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-490">You can also perform aggregation over hello result of array iteration.</span></span> <span data-ttu-id="bf3c8-491">Por exemplo, hello consulta a seguir conta Olá número de filhos entre todas as famílias.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-491">For example, hello following query counts hello number of children among all families.</span></span>

<span data-ttu-id="bf3c8-492">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-492">**Query**</span></span>

    SELECT COUNT(child) 
    FROM child IN Families.children

<span data-ttu-id="bf3c8-493">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-493">**Results**</span></span>  

    [
      { 
        "$1": 3
      }
    ]

### <span data-ttu-id="bf3c8-494"><a id="Joins"></a>Junções</span><span class="sxs-lookup"><span data-stu-id="bf3c8-494"><a id="Joins"></a>Joins</span></span>
<span data-ttu-id="bf3c8-495">Em um banco de dados relacional, é importante Olá necessidade toojoin entre tabelas.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-495">In a relational database, hello need toojoin across tables is important.</span></span> <span data-ttu-id="bf3c8-496">Sua saudação lógica toodesigning corolário normalizado esquemas.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-496">It's hello logical corollary toodesigning normalized schemas.</span></span> <span data-ttu-id="bf3c8-497">Contrary toothis, API DocumentDB lida com o modelo de dados desnormalizados Olá de documentos sem esquema.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-497">Contrary toothis, DocumentDB API deals with hello denormalized data model of schema-free documents.</span></span> <span data-ttu-id="bf3c8-498">Este é o equivalente lógico de saudação de um "autojunção".</span><span class="sxs-lookup"><span data-stu-id="bf3c8-498">This is hello logical equivalent of a "self-join".</span></span>

<span data-ttu-id="bf3c8-499">sintaxe de saudação que dá suporte a idioma Olá é junção de junção < from_source2 > de < from_source1 >... JUNÇÃO < from_sourceN >.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-499">hello syntax that hello language supports is <from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>.</span></span> <span data-ttu-id="bf3c8-500">De modo geral, isto retorna um conjunto de tuplas **N** (tupla com valores **N**).</span><span class="sxs-lookup"><span data-stu-id="bf3c8-500">Overall, this returns a set of **N**-tuples (tuple with **N** values).</span></span> <span data-ttu-id="bf3c8-501">Cada tupla terá os valores produzidos pela iteração de todos os alias da coleção em seus respectivos conjuntos.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-501">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span> <span data-ttu-id="bf3c8-502">Em outras palavras, este é um produto cruzado completo dos conjuntos de saudação participam da junção de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-502">In other words, this is a full cross product of hello sets participating in hello join.</span></span>

<span data-ttu-id="bf3c8-503">Olá exemplos a seguir mostram como funciona a cláusula de junção hello.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-503">hello following examples show how hello JOIN clause works.</span></span> <span data-ttu-id="bf3c8-504">Olá exemplo a seguir, o resultado de saudação é vazio pois hello produto cruzado de cada documento de origem e um conjunto vazio está vazio.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-504">In hello following example, hello result is empty since hello cross product of each document from source and an empty set is empty.</span></span>

<span data-ttu-id="bf3c8-505">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-505">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

<span data-ttu-id="bf3c8-506">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-506">**Results**</span></span>  

    [{
    }]


<span data-ttu-id="bf3c8-507">Em Olá exemplo a seguir, junção de saudação é entre a raiz do documento hello e hello `children` subroot.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-507">In hello following example, hello join is between hello document root and hello `children` subroot.</span></span> <span data-ttu-id="bf3c8-508">Trata-se de um produto cruzado entre dois objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-508">It's a cross product between two JSON objects.</span></span> <span data-ttu-id="bf3c8-509">fato Olá filhos é uma matriz não é eficaz em Olá junção já que estamos lidando com uma única raiz é Olá filhos matriz.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-509">hello fact that children is an array is not effective in hello JOIN since we are dealing with a single root that is hello children array.</span></span> <span data-ttu-id="bf3c8-510">Portanto, o resultado de Olá contém dois resultados, desde que o produto cruzado de cada documento com matriz Olá Olá produz exatamente apenas um documento.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-510">Hence hello result contains only two results, since hello cross product of each document with hello array yields exactly only one document.</span></span>

<span data-ttu-id="bf3c8-511">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-511">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.children

<span data-ttu-id="bf3c8-512">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-512">**Results**</span></span>

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


<span data-ttu-id="bf3c8-513">saudação de exemplo a seguir mostra uma junção mais convencional:</span><span class="sxs-lookup"><span data-stu-id="bf3c8-513">hello following example shows a more conventional join:</span></span>

<span data-ttu-id="bf3c8-514">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-514">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

<span data-ttu-id="bf3c8-515">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-515">**Results**</span></span>

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



<span data-ttu-id="bf3c8-516">Olá primeiro toonote é que hello `from_source` de saudação **INGRESSAR** cláusula é um iterador.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-516">hello first thing toonote is that hello `from_source` of hello **JOIN** clause is an iterator.</span></span> <span data-ttu-id="bf3c8-517">Portanto, Olá fluxo nesse caso é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="bf3c8-517">So, hello flow in this case is as follows:</span></span>  

* <span data-ttu-id="bf3c8-518">Expanda cada elemento filho **c** na matriz de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-518">Expand each child element **c** in hello array.</span></span>
* <span data-ttu-id="bf3c8-519">Aplicar um produto cruzado com raiz de saudação do documento hello **f** com cada elemento filho **c** que foi simplificada na primeira etapa de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-519">Apply a cross product with hello root of hello document **f** with each child element **c** that was flattened in hello first step.</span></span>
* <span data-ttu-id="bf3c8-520">Por fim, objeto de raiz de saudação do projeto **f** apenas da propriedade name.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-520">Finally, project hello root object **f** name property alone.</span></span> 

<span data-ttu-id="bf3c8-521">documento primeiro Hello (`AndersenFamily`) contém apenas um elemento filho, portanto o conjunto de resultados Olá contém apenas um único objeto documento correspondente do toothis.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-521">hello first document (`AndersenFamily`) contains only one child element, so hello result set contains only a single object corresponding toothis document.</span></span> <span data-ttu-id="bf3c8-522">segundo documento de saudação (`WakefieldFamily`) contém dois filhos.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-522">hello second document (`WakefieldFamily`) contains two children.</span></span> <span data-ttu-id="bf3c8-523">Portanto, hello produto cruzado produz um objeto separado para cada filho, resultando assim em dois objetos, um para cada documento de toothis filho correspondente.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-523">So, hello cross product produces a separate object for each child, thereby resulting in two objects, one for each child corresponding toothis document.</span></span> <span data-ttu-id="bf3c8-524">raiz de saudação campos em ambos esses documentos são iguais, Olá conforme o esperado em um produto cruzado.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-524">hello root fields in both these documents are hello same, just as you would expect in a cross product.</span></span>

<span data-ttu-id="bf3c8-525">Olá utilitário real de saudação junção é tooform tuplas de produto cruzado de saudação em uma forma que seja difícil tooproject.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-525">hello real utility of hello JOIN is tooform tuples from hello cross-product in a shape that's otherwise difficult tooproject.</span></span> <span data-ttu-id="bf3c8-526">Além disso, como podemos ver no exemplo hello abaixo, você pode filtrar na combinação de saudação de uma tupla Olá que permite o usuário optou por uma condição atendida por tuplas Olá geral.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-526">Furthermore, as we see in hello example below, you could filter on hello combination of a tuple that lets' hello user chose a condition satisfied by hello tuples overall.</span></span>

<span data-ttu-id="bf3c8-527">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-527">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

<span data-ttu-id="bf3c8-528">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-528">**Results**</span></span>

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



<span data-ttu-id="bf3c8-529">Este exemplo é uma extensão natural da saudação anterior de exemplo e executa uma junção dupla.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-529">This example is a natural extension of hello preceding example, and performs a double join.</span></span> <span data-ttu-id="bf3c8-530">Portanto, hello produto cruzado podem ser exibido como Olá pseudocódigo a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf3c8-530">So, hello cross product can be viewed as hello following pseudo-code:</span></span>

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

<span data-ttu-id="bf3c8-531">`AndersenFamily` tem um filho que, por sua vez, tem um animal de estimação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-531">`AndersenFamily` has one child who has one pet.</span></span> <span data-ttu-id="bf3c8-532">Portanto, hello produto cruzado produz uma linha (1\*1\*1) desta família.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-532">So, hello cross product yields one row (1\*1\*1) from this family.</span></span> <span data-ttu-id="bf3c8-533">WakefieldFamily, no entanto, tem dois filhos, mas apenas a filha "Jesse" tem animais de estimação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-533">WakefieldFamily however has two children, but only one child "Jesse" has pets.</span></span> <span data-ttu-id="bf3c8-534">Porém, Jesse tem dois animais de estimação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-534">Jesse has two pets though.</span></span> <span data-ttu-id="bf3c8-535">Portanto, hello produto cruzado produz 1\*1\*2 = 2 linhas a partir desta família.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-535">Hence hello cross product yields 1\*1\*2 = 2 rows from this family.</span></span>

<span data-ttu-id="bf3c8-536">No exemplo a seguir hello, há um filtro adicional no `pet`.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-536">In hello next example, there is an additional filter on `pet`.</span></span> <span data-ttu-id="bf3c8-537">Exclui todas as tuplas Olá onde Olá animal de estimação nome não é "Sombra".</span><span class="sxs-lookup"><span data-stu-id="bf3c8-537">This excludes all hello tuples where hello pet name is not "Shadow".</span></span> <span data-ttu-id="bf3c8-538">Observe que estamos tuplas toobuild capaz de matrizes de filtro em qualquer um dos elementos de saudação de tupla Olá e qualquer combinação de elementos de saudação do projeto.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-538">Notice that we are able toobuild tuples from arrays, filter on any of hello elements of hello tuple, and project any combination of hello elements.</span></span> 

<span data-ttu-id="bf3c8-539">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-539">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

<span data-ttu-id="bf3c8-540">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-540">**Results**</span></span>

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <span data-ttu-id="bf3c8-541"><a id="JavaScriptIntegration"></a>Integração do JavaScript</span><span class="sxs-lookup"><span data-stu-id="bf3c8-541"><a id="JavaScriptIntegration"></a>JavaScript integration</span></span>
<span data-ttu-id="bf3c8-542">Banco de dados do Azure Cosmos fornece um modelo de programação para a execução lógica do aplicativo JavaScript baseado diretamente em coleções de saudação em termos de procedimentos armazenados e gatilhos.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-542">Azure Cosmos DB provides a programming model for executing JavaScript based application logic directly on hello collections in terms of stored procedures and triggers.</span></span> <span data-ttu-id="bf3c8-543">Isso possibilita:</span><span class="sxs-lookup"><span data-stu-id="bf3c8-543">This allows for both:</span></span>

* <span data-ttu-id="bf3c8-544">Capacidade toodo alto desempenho transacional as operações CRUD e consultas em documentos em uma coleção por meio da integração profunda de saudação do tempo de execução de JavaScript diretamente no mecanismo de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-544">Ability toodo high-performance transactional CRUD operations and queries against documents in a collection by virtue of hello deep integration of JavaScript runtime directly within hello database engine.</span></span> 
* <span data-ttu-id="bf3c8-545">Um modelamento natural de fluxo de controle, escopo de variáveis, atribuição e integração de primitivos que lidam com exceções com transações de bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-545">A natural modeling of control flow, variable scoping, and assignment and integration of exception handling primitives with database transactions.</span></span> <span data-ttu-id="bf3c8-546">Para obter mais detalhes sobre o suporte de banco de dados do Azure Cosmos para integração do JavaScript, consulte toohello documentação de programação do lado do servidor de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-546">For more details about Azure Cosmos DB support for JavaScript integration, please refer toohello JavaScript server-side programmability documentation.</span></span>

### <span data-ttu-id="bf3c8-547"><a id="UserDefinedFunctions"></a>UDFs (Funções Definidas pelo Usuário)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-547"><a id="UserDefinedFunctions"></a>User-Defined Functions (UDFs)</span></span>
<span data-ttu-id="bf3c8-548">Juntamente com os tipos de saudação já foi definidos neste artigo, o DocumentDB API SQL oferece suporte para funções de definida pelo usuário (UDF).</span><span class="sxs-lookup"><span data-stu-id="bf3c8-548">Along with hello types already defined in this article, DocumentDB API SQL provides support for User Defined Functions (UDF).</span></span> <span data-ttu-id="bf3c8-549">Em particular, UDFs escalares têm suporte em que os desenvolvedores de saudação podem passar argumentos zero ou muitos e retornar um resultado de único argumento novamente.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-549">In particular, scalar UDFs are supported where hello developers can pass in zero or many arguments and return a single argument result back.</span></span> <span data-ttu-id="bf3c8-550">Cada um desses argumentos é verificado para definir se são valores JSON legais.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-550">Each of these arguments is checked for being legal JSON values.</span></span>  

<span data-ttu-id="bf3c8-551">Olá sintaxe SQL de API de documentos é estendido toosupport lógica de aplicativo personalizado usando estas funções definidas pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-551">hello DocumentDB API SQL syntax is extended toosupport custom application logic using these User-Defined Functions.</span></span> <span data-ttu-id="bf3c8-552">As UDFs podem ser registradas na API do DocumentDB e então referenciadas como parte de uma consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-552">UDFs can be registered with DocumentDB API and then be referenced as part of a SQL query.</span></span> <span data-ttu-id="bf3c8-553">Na verdade, Olá UDFs exquisitely são projetados toobe chamado através de consultas.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-553">In fact, hello UDFs are exquisitely designed toobe invoked by queries.</span></span> <span data-ttu-id="bf3c8-554">Como uma opção de resultado toothis, UDFs não tem objeto de contexto de toohello de acesso que Olá outros JavaScript têm tipos (procedimentos armazenados e gatilhos).</span><span class="sxs-lookup"><span data-stu-id="bf3c8-554">As a corollary toothis choice, UDFs do not have access toohello context object which hello other JavaScript types (stored procedures and triggers) have.</span></span> <span data-ttu-id="bf3c8-555">Como as consultas são executadas como somente leitura, elas podem ser executadas em réplicas primárias ou secundárias.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-555">Since queries execute as read-only, they can run either on primary or on secondary replicas.</span></span> <span data-ttu-id="bf3c8-556">Portanto, UDFs são toorun projetado em réplicas secundárias ao contrário de outros tipos de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-556">Therefore, UDFs are designed toorun on secondary replicas unlike other JavaScript types.</span></span>

<span data-ttu-id="bf3c8-557">Abaixo está um exemplo de como uma UDF pode ser registrada em Olá Cosmos banco de dados, especificamente em uma coleção de documentos.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-557">Below is an example of how a UDF can be registered at hello Cosmos DB database, specifically under a document collection.</span></span>

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

<span data-ttu-id="bf3c8-558">Olá, exemplo anterior cria um UDF cujo nome é `REGEX_MATCH`.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-558">hello preceding example creates a UDF whose name is `REGEX_MATCH`.</span></span> <span data-ttu-id="bf3c8-559">Ele aceita dois valores de cadeia de caracteres JSON `input` e `pattern` e verifica se a correspondência do primeiro Olá Olá padrão especificado no segundo Olá usando a função de string de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-559">It accepts two JSON string values `input` and `pattern` and checks if hello first matches hello pattern specified in hello second using JavaScript's string.match() function.</span></span>

<span data-ttu-id="bf3c8-560">Agora, podemos usar esta UDF em uma consulta em uma projeção.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-560">We can now use this UDF in a query in a projection.</span></span> <span data-ttu-id="bf3c8-561">UDFs devem ser qualificadas com o prefixo de maiusculas e minúsculas hello "udf."</span><span class="sxs-lookup"><span data-stu-id="bf3c8-561">UDFs must be qualified with hello case-sensitive prefix "udf."</span></span> <span data-ttu-id="bf3c8-562">quando chamadas por meio de consultas.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-562">when called from within queries.</span></span> 

> [!NOTE]
> <span data-ttu-id="bf3c8-563">Anterior too3/17/2015, Cosmos DB suporte para chamadas UDF sem hello "udf."</span><span class="sxs-lookup"><span data-stu-id="bf3c8-563">Prior too3/17/2015, Cosmos DB supported UDF calls without hello "udf."</span></span> <span data-ttu-id="bf3c8-564">como SELECT REGEX_MATCH().</span><span class="sxs-lookup"><span data-stu-id="bf3c8-564">prefix like SELECT REGEX_MATCH().</span></span> <span data-ttu-id="bf3c8-565">Esse padrão de chamada foi preterido.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-565">This calling pattern has been deprecated.</span></span>  
> 
> 

<span data-ttu-id="bf3c8-566">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-566">**Query**</span></span>

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

<span data-ttu-id="bf3c8-567">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-567">**Results**</span></span>

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

<span data-ttu-id="bf3c8-568">Olá UDF também pode ser usado dentro de um filtro como mostrado no exemplo hello abaixo, também qualificado com hello "udf."</span><span class="sxs-lookup"><span data-stu-id="bf3c8-568">hello UDF can also be used inside a filter as shown in hello example below, also qualified with hello "udf."</span></span> <span data-ttu-id="bf3c8-569">prefixo:</span><span class="sxs-lookup"><span data-stu-id="bf3c8-569">prefix:</span></span>

<span data-ttu-id="bf3c8-570">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-570">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

<span data-ttu-id="bf3c8-571">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-571">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


<span data-ttu-id="bf3c8-572">Basicamente, as UDFs são expressões escalares válidas e podem ser usadas em projeções e filtros.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-572">In essence, UDFs are valid scalar expressions and can be used in both projections and filters.</span></span> 

<span data-ttu-id="bf3c8-573">tooexpand energia Olá de UDFs, vejamos outro exemplo com lógica condicional:</span><span class="sxs-lookup"><span data-stu-id="bf3c8-573">tooexpand on hello power of UDFs, let's look at another example with conditional logic:</span></span>

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


<span data-ttu-id="bf3c8-574">Abaixo está um exemplo exercícios Olá UDF.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-574">Below is an example that exercises hello UDF.</span></span>

<span data-ttu-id="bf3c8-575">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-575">**Query**</span></span>

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

<span data-ttu-id="bf3c8-576">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-576">**Results**</span></span>

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


<span data-ttu-id="bf3c8-577">Como hello showcase de exemplos anteriores, UDFs integram power Olá da linguagem JavaScript Olá documentos API SQL tooprovide uma sofisticada interface programável toodo procedimento, condicional lógica complexa com a Ajuda de saudação do tempo de execução de JavaScript embutida recursos.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-577">As hello preceding examples showcase, UDFs integrate hello power of JavaScript language with hello DocumentDB API SQL tooprovide a rich programmable interface toodo complex procedural, conditional logic with hello help of inbuilt JavaScript runtime capabilities.</span></span>

<span data-ttu-id="bf3c8-578">Documentos API SQL fornece argumentos Olá toohello UDFs para cada documento na fonte Olá Olá atual estágio (cláusula WHERE ou cláusula SELECT) de processamento hello UDF.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-578">DocumentDB API SQL provides hello arguments toohello UDFs for each document in hello source at hello current stage (WHERE clause or SELECT clause) of processing hello UDF.</span></span> <span data-ttu-id="bf3c8-579">Olá resultado é incorporado na Olá diretamente o pipeline de execução geral.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-579">hello result is incorporated in hello overall execution pipeline seamlessly.</span></span> <span data-ttu-id="bf3c8-580">Se propriedades de Olá tooby chamado hello UDF parâmetros não estão disponíveis em Olá valor JSON, hello parâmetro é considerado como indefinido e, portanto, Olá invocação UDF inteiramente será ignorada.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-580">If hello properties referred tooby hello UDF parameters are not available in hello JSON value, hello parameter is considered as undefined and hence hello UDF invocation is entirely skipped.</span></span> <span data-ttu-id="bf3c8-581">Da mesma forma se resultado Olá Olá UDF é indefinido, ele não está incluído no resultado de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-581">Similarly if hello result of hello UDF is undefined, it's not included in hello result.</span></span> 

<span data-ttu-id="bf3c8-582">Em resumo, UDFs são lógica de negócios complexa toodo excelentes ferramentas como parte da consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-582">In summary, UDFs are great tools toodo complex business logic as part of hello query.</span></span>

### <a name="operator-evaluation"></a><span data-ttu-id="bf3c8-583">Avaliação de operador</span><span class="sxs-lookup"><span data-stu-id="bf3c8-583">Operator evaluation</span></span>
<span data-ttu-id="bf3c8-584">Cosmos banco de dados, porque Olá de ser um banco de dados JSON, desenha paralelos com operadores (JavaScript) e sua semântica de avaliação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-584">Cosmos DB, by hello virtue of being a JSON database, draws parallels with JavaScript operators and its evaluation semantics.</span></span> <span data-ttu-id="bf3c8-585">Enquanto o banco de dados do Cosmos tenta toopreserve semântica de JavaScript em termos de suporte JSON, avaliação de operação de saudação do desvio em alguns casos.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-585">While Cosmos DB tries toopreserve JavaScript semantics in terms of JSON support, hello operation evaluation deviates in some instances.</span></span>

<span data-ttu-id="bf3c8-586">No SQL da API de documentos, diferentemente no SQL tradicional, tipos de saudação de valores geralmente não são conhecidos até que os valores hello são recuperados do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-586">In DocumentDB API SQL, unlike in traditional SQL, hello types of values are often not known until hello values are retrieved from database.</span></span> <span data-ttu-id="bf3c8-587">Em ordem tooefficiently executar consultas, a maioria dos operadores de saudação tem requisitos de tipo estrito.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-587">In order tooefficiently execute queries, most of hello operators have strict type requirements.</span></span> 

<span data-ttu-id="bf3c8-588">O SQL da API do DocumentDB não realiza conversões implícitas, diferente do JavaScript.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-588">DocumentDB API SQL doesn't perform implicit conversions, unlike JavaScript.</span></span> <span data-ttu-id="bf3c8-589">Por exemplo, uma consulta como `SELECT * FROM Person p WHERE p.Age = 21` corresponde a documentos que contêm a propriedade Age com o valor 21.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-589">For instance, a query like `SELECT * FROM Person p WHERE p.Age = 21` matches documents that contain an Age property whose value is 21.</span></span> <span data-ttu-id="bf3c8-590">Qualquer outro documento cuja propriedade Age corresponder a “21” — ou a outras variações potencialmente infinitas como “021”, “21,0”, “0021”, “00021” etc. — não será correspondido.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-590">Any other document whose Age property matches string "21", or other possibly infinite variations like "021", "21.0", "0021", "00021", etc. will not be matched.</span></span> <span data-ttu-id="bf3c8-591">Isso é, em contraste, toohello JavaScript onde os valores de cadeia de caracteres de hello são implicitamente convertidos toonumbers (com base no operador, por exemplo: = =).</span><span class="sxs-lookup"><span data-stu-id="bf3c8-591">This is in contrast toohello JavaScript where hello string values are implicitly casted toonumbers (based on operator, ex: ==).</span></span> <span data-ttu-id="bf3c8-592">Esta escolha é fundamental para uma correspondência eficiente de índices no SQL da API do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-592">This choice is crucial for efficient index matching in DocumentDB API SQL.</span></span> 

## <a name="parameterized-sql-queries"></a><span data-ttu-id="bf3c8-593">Consultas SQL parametrizadas</span><span class="sxs-lookup"><span data-stu-id="bf3c8-593">Parameterized SQL queries</span></span>
<span data-ttu-id="bf3c8-594">Cosmos banco de dados oferece suporte a consultas com parâmetros expressados com hello familiar notação @.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-594">Cosmos DB supports queries with parameters expressed with hello familiar @ notation.</span></span> <span data-ttu-id="bf3c8-595">A SQL parametrizada oferece recursos robustos de manuseio e saída das entradas de usuário, evitando a exposição acidental de dados por meio de uma injeção SQL.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-595">Parameterized SQL provides robust handling and escaping of user input, preventing accidental exposure of data through SQL injection.</span></span> 

<span data-ttu-id="bf3c8-596">Por exemplo, você pode escrever uma consulta que define o sobrenome e o estado do endereço como parâmetros e executá-la para vários valores de sobrenome e estado de endereço, com base na entrada do usuário.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-596">For example, you can write a query that takes last name and address state as parameters, and then execute it for various values of last name and address state based on user input.</span></span>

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

<span data-ttu-id="bf3c8-597">Essa solicitação pode então ser enviada tooCosmos banco de dados como uma consulta parametrizada de JSON como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-597">This request can then be sent tooCosmos DB as a parameterized JSON query like shown below.</span></span>

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

<span data-ttu-id="bf3c8-598">Olá argumento tooTOP pode ser definido usando consultas parametrizadas como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-598">hello argument tooTOP can be set using parameterized queries like shown below.</span></span>

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

<span data-ttu-id="bf3c8-599">Os valores dos parâmetros podem ser qualquer JSON válido (cadeias de caracteres, números, boolianos, nulos, ou mesmo matrizes e JSON aninhado).</span><span class="sxs-lookup"><span data-stu-id="bf3c8-599">Parameter values can be any valid JSON (strings, numbers, Booleans, null, even arrays or nested JSON).</span></span> <span data-ttu-id="bf3c8-600">Além disso, como o Cosmos DB não tem esquemas, os parâmetros não são validados em relação a nenhum tipo.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-600">Also since Cosmos DB is schema-less, parameters are not validated against any type.</span></span>

## <span data-ttu-id="bf3c8-601"><a id="BuiltinFunctions"></a>Funções internas</span><span class="sxs-lookup"><span data-stu-id="bf3c8-601"><a id="BuiltinFunctions"></a>Built-in functions</span></span>
<span data-ttu-id="bf3c8-602">O Cosmos DB também dá suporte a várias funções internas para operações comuns, que podem ser usadas em consultas como UDFs (funções definidas pelo usuário).</span><span class="sxs-lookup"><span data-stu-id="bf3c8-602">Cosmos DB also supports a number of built-in functions for common operations, that can be used inside queries like user-defined functions (UDFs).</span></span>

| <span data-ttu-id="bf3c8-603">Grupo de funções</span><span class="sxs-lookup"><span data-stu-id="bf3c8-603">Function group</span></span>          | <span data-ttu-id="bf3c8-604">Operações</span><span class="sxs-lookup"><span data-stu-id="bf3c8-604">Operations</span></span>                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="bf3c8-605">Funções matemáticas</span><span class="sxs-lookup"><span data-stu-id="bf3c8-605">Mathematical functions</span></span>  | <span data-ttu-id="bf3c8-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN e TAN</span><span class="sxs-lookup"><span data-stu-id="bf3c8-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN, and TAN</span></span> |
| <span data-ttu-id="bf3c8-607">Funções de verificação de tipo</span><span class="sxs-lookup"><span data-stu-id="bf3c8-607">Type checking functions</span></span> | <span data-ttu-id="bf3c8-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED e IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="bf3c8-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED, and IS_PRIMITIVE</span></span>                                                           |
| <span data-ttu-id="bf3c8-609">Funções de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="bf3c8-609">String functions</span></span>        | <span data-ttu-id="bf3c8-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING e UPPER</span><span class="sxs-lookup"><span data-stu-id="bf3c8-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING, and UPPER</span></span>       |
| <span data-ttu-id="bf3c8-611">Funções de matriz</span><span class="sxs-lookup"><span data-stu-id="bf3c8-611">Array functions</span></span>         | <span data-ttu-id="bf3c8-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH e ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="bf3c8-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH, and ARRAY_SLICE</span></span>                                                                                         |
| <span data-ttu-id="bf3c8-613">Funções espaciais</span><span class="sxs-lookup"><span data-stu-id="bf3c8-613">Spatial functions</span></span>       | <span data-ttu-id="bf3c8-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID e ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="bf3c8-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID, and ST_ISVALIDDETAILED</span></span>                                                                           | 

<span data-ttu-id="bf3c8-615">Se você estiver usando uma função definida pelo usuário (UDF) para o qual uma função interna agora está disponível, você deve usar a função interna correspondente do hello como vai toobe toorun de mais rápido e mais eficiente.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-615">If you’re currently using a user-defined function (UDF) for which a built-in function is now available, you should use hello corresponding built-in function as it is going toobe quicker toorun and more efficiently.</span></span> 

### <a name="mathematical-functions"></a><span data-ttu-id="bf3c8-616">Funções matemáticas</span><span class="sxs-lookup"><span data-stu-id="bf3c8-616">Mathematical functions</span></span>
<span data-ttu-id="bf3c8-617">Olá funções matemáticas executam um cálculo, com base em valores de entrada que são fornecidos como argumentos e retornam um valor numérico.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-617">hello mathematical functions each perform a calculation, based on input values that are provided as arguments, and return a numeric value.</span></span> <span data-ttu-id="bf3c8-618">Aqui está uma tabela de funções matemáticas internas com suporte.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-618">Here’s a table of supported built-in mathematical functions.</span></span>


| <span data-ttu-id="bf3c8-619">Uso</span><span class="sxs-lookup"><span data-stu-id="bf3c8-619">Usage</span></span> | <span data-ttu-id="bf3c8-620">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf3c8-620">Description</span></span> |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="bf3c8-621">[[ABS (num_expr)](#bk_abs)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-621">[[ABS (num_expr)](#bk_abs)</span></span> | <span data-ttu-id="bf3c8-622">Retorna Olá valor absoluto (positivo) da saudação especificado expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-622">Returns hello absolute (positive) value of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="bf3c8-623">CEILING (num_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-623">CEILING (num_expr)</span></span>](#bk_ceiling) | <span data-ttu-id="bf3c8-624">Retorna Olá menor valor de número inteiro maior ou igual ao Olá expressão numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-624">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span> |
| [<span data-ttu-id="bf3c8-625">FLOOR (num_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-625">FLOOR (num_expr)</span></span>](#bk_floor) | <span data-ttu-id="bf3c8-626">Retorna Olá maior inteiro menor ou igual a toohello especificado expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-626">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span> |
| [<span data-ttu-id="bf3c8-627">EXP (num_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-627">EXP (num_expr)</span></span>](#bk_exp) | <span data-ttu-id="bf3c8-628">Expoente de saudação retorna da saudação especificado expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-628">Returns hello exponent of hello specified numeric expression.</span></span> |
| <span data-ttu-id="bf3c8-629">[LOG (num_expr [,base])](#bk_log)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-629">[LOG (num_expr [,base])](#bk_log)</span></span> | <span data-ttu-id="bf3c8-630">Retorna Olá o logaritmo natural de saudação expressão numérica, ou logaritmo hello usando Olá especificada base</span><span class="sxs-lookup"><span data-stu-id="bf3c8-630">Returns hello natural logarithm of hello specified numeric expression, or hello logarithm using hello specified base</span></span> |
| [<span data-ttu-id="bf3c8-631">LOG10 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-631">LOG10 (num_expr)</span></span>](#bk_log10) | <span data-ttu-id="bf3c8-632">Olá retorna valor logarítmica de base 10 de saudação especificado expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-632">Returns hello base-10 logarithmic value of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="bf3c8-633">ROUND (num_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-633">ROUND (num_expr)</span></span>](#bk_round) | <span data-ttu-id="bf3c8-634">Retorna um valor numérico, arredondado toohello valor de inteiro mais próximo.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-634">Returns a numeric value, rounded toohello closest integer value.</span></span> |
| [<span data-ttu-id="bf3c8-635">TRUNC (num_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-635">TRUNC (num_expr)</span></span>](#bk_trunc) | <span data-ttu-id="bf3c8-636">Retorna um valor numérico, o valor inteiro mais próximo de toohello truncados.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-636">Returns a numeric value, truncated toohello closest integer value.</span></span> |
| [<span data-ttu-id="bf3c8-637">SQRT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-637">SQRT (num_expr)</span></span>](#bk_sqrt) | <span data-ttu-id="bf3c8-638">Retorna Olá quadrado raiz de saudação especificado expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-638">Returns hello square root of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="bf3c8-639">SQUARE (num_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-639">SQUARE (num_expr)</span></span>](#bk_square) | <span data-ttu-id="bf3c8-640">Saudação de retorna quadrada de saudação especificado expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-640">Returns hello square of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="bf3c8-641">POWER (num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-641">POWER (num_expr, num_expr)</span></span>](#bk_power) | <span data-ttu-id="bf3c8-642">Retorna Olá power de saudação especificado expressão numérica toohello valor especificado.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-642">Returns hello power of hello specified numeric expression toohello value specified.</span></span> |
| [<span data-ttu-id="bf3c8-643">SIGN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-643">SIGN (num_expr)</span></span>](#bk_sign) | <span data-ttu-id="bf3c8-644">Retorna Olá sinal valor (-1, 0, 1) de saudação especificado expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-644">Returns hello sign value (-1, 0, 1) of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="bf3c8-645">ACOS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-645">ACOS (num_expr)</span></span>](#bk_acos) | <span data-ttu-id="bf3c8-646">Ângulo de saudação retorna, em radianos, cujo cosseno é Olá expressão numérica especificada; também chamado de arco cosseno.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-646">Returns hello angle, in radians, whose cosine is hello specified numeric expression; also called arccosine.</span></span> |
| [<span data-ttu-id="bf3c8-647">ASIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-647">ASIN (num_expr)</span></span>](#bk_asin) | <span data-ttu-id="bf3c8-648">Ângulo de saudação retorna, em radianos, cujo seno é hello especificado expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-648">Returns hello angle, in radians, whose sine is hello specified numeric expression.</span></span> <span data-ttu-id="bf3c8-649">Isso também é chamado de arco seno.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-649">This is also called arcsine.</span></span> |
| [<span data-ttu-id="bf3c8-650">ATAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-650">ATAN (num_expr)</span></span>](#bk_atan) | <span data-ttu-id="bf3c8-651">Ângulo de saudação retorna, em radianos, cuja tangente é hello especificado expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-651">Returns hello angle, in radians, whose tangent is hello specified numeric expression.</span></span> <span data-ttu-id="bf3c8-652">Isso também é chamado de arco tangente.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-652">This is also called arctangent.</span></span> |
| [<span data-ttu-id="bf3c8-653">ATN2 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-653">ATN2 (num_expr)</span></span>](#bk_atn2) | <span data-ttu-id="bf3c8-654">Retorna Olá ângulo em radianos, entre o eixo x positivo de saudação e raio de saudação do hello toohello de ponto de origem (x, y), onde x e y são valores de saudação do hello duas expressões flutuantes especificadas.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-654">Returns hello angle, in radians, between hello positive x-axis and hello ray from hello origin toohello point (y, x), where x and y are hello values of hello two specified float expressions.</span></span> |
| [<span data-ttu-id="bf3c8-655">COS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-655">COS (num_expr)</span></span>](#bk_cos) | <span data-ttu-id="bf3c8-656">Retorna Olá cosseno trigonométrico Olá especificado o ângulo em radianos, na Olá expressão especificada.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-656">Returns hello trigonometric cosine of hello specified angle, in radians, in hello specified expression.</span></span> |
| [<span data-ttu-id="bf3c8-657">COT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-657">COT (num_expr)</span></span>](#bk_cot) | <span data-ttu-id="bf3c8-658">Retorna Olá cotangente trigonométrica Olá especificado o ângulo em radianos, Olá especificada expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-658">Returns hello trigonometric cotangent of hello specified angle, in radians, in hello specified numeric expression.</span></span> |
| [<span data-ttu-id="bf3c8-659">DEGREES (num_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-659">DEGREES (num_expr)</span></span>](#bk_degrees) | <span data-ttu-id="bf3c8-660">Retorna Olá ângulo correspondente em graus para um ângulo especificado em radianos.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-660">Returns hello corresponding angle in degrees for an angle specified in radians.</span></span> |
| [<span data-ttu-id="bf3c8-661">PI ()</span><span class="sxs-lookup"><span data-stu-id="bf3c8-661">PI ()</span></span>](#bk_pi) | <span data-ttu-id="bf3c8-662">Retorna Olá valor constante de PI.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-662">Returns hello constant value of PI.</span></span> |
| [<span data-ttu-id="bf3c8-663">RADIANS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-663">RADIANS (num_expr)</span></span>](#bk_radians) | <span data-ttu-id="bf3c8-664">Retorna radianos quando uma expressão numérica é inserida em graus.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-664">Returns radians when a numeric expression, in degrees, is entered.</span></span> |
| [<span data-ttu-id="bf3c8-665">SIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-665">SIN (num_expr)</span></span>](#bk_sin) | <span data-ttu-id="bf3c8-666">Retorna Olá seno trigonométrico Olá especificado o ângulo em radianos, na Olá expressão especificada.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-666">Returns hello trigonometric sine of hello specified angle, in radians, in hello specified expression.</span></span> |
| [<span data-ttu-id="bf3c8-667">TAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-667">TAN (num_expr)</span></span>](#bk_tan) | <span data-ttu-id="bf3c8-668">Tangente de saudação retorna da expressão de entrada hello, em Olá expressão especificada.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-668">Returns hello tangent of hello input expression, in hello specified expression.</span></span> |

<span data-ttu-id="bf3c8-669">Por exemplo, agora você pode executar consultas com hello seguinte:</span><span class="sxs-lookup"><span data-stu-id="bf3c8-669">For example, you can now run queries like hello following:</span></span>

<span data-ttu-id="bf3c8-670">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-670">**Query**</span></span>

    SELECT VALUE ABS(-4)

<span data-ttu-id="bf3c8-671">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-671">**Results**</span></span>

    [4]

<span data-ttu-id="bf3c8-672">Olá principal diferença entre tooANSI de funções em comparação do banco de dados Cosmos SQL é que eles são projetado toowork bem com dados de esquema sem esquema e misto.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-672">hello main difference between Cosmos DB’s functions compared tooANSI SQL is that they are designed toowork well with schema-less and mixed schema data.</span></span> <span data-ttu-id="bf3c8-673">Por exemplo, se você tiver um documento em que a propriedade de tamanho hello está ausente ou tem um valor não numérico, como "desconhecido", em seguida, documento hello é ignorado, em vez de retornar um erro.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-673">For example, if you have a document where hello Size property is missing, or has a non-numeric value like “unknown”, then hello document is skipped over, instead of returning an error.</span></span>

### <a name="type-checking-functions"></a><span data-ttu-id="bf3c8-674">Funções de verificação de tipo</span><span class="sxs-lookup"><span data-stu-id="bf3c8-674">Type checking functions</span></span>
<span data-ttu-id="bf3c8-675">funções de verificação de tipo Hello permitem tipo de saudação toocheck de uma expressão em consultas SQL.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-675">hello type checking functions allow you toocheck hello type of an expression within SQL queries.</span></span> <span data-ttu-id="bf3c8-676">Tipo de funções de verificação podem ser usado toodetermine tipo de saudação de propriedades nos documentos imediatamente hello quando é desconhecido ou variável.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-676">Type checking functions can be used toodetermine hello type of properties within documents on hello fly when it is variable or unknown.</span></span> <span data-ttu-id="bf3c8-677">Aqui está uma tabela de funções de verificação de tipo internas com suporte.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-677">Here’s a table of supported built-in type checking functions.</span></span>

<table>
<tr>
  <td><span data-ttu-id="bf3c8-678"><strong>Uso</strong></span><span class="sxs-lookup"><span data-stu-id="bf3c8-678"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="bf3c8-679"><strong>Descrição</strong></span><span class="sxs-lookup"><span data-stu-id="bf3c8-679"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="bf3c8-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span><span class="sxs-lookup"><span data-stu-id="bf3c8-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span></span></td>
  <td><span data-ttu-id="bf3c8-681">Retorna um valor booleano que indica se o tipo de saudação do valor de saudação é uma matriz.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-681">Returns a Boolean indicating if hello type of hello value is an array.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="bf3c8-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="bf3c8-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span></span></td>
  <td><span data-ttu-id="bf3c8-683">Retorna um valor booleano que indica se o tipo de saudação do valor de saudação é um valor booleano.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-683">Returns a Boolean indicating if hello type of hello value is a Boolean.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="bf3c8-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="bf3c8-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span></span></td>
  <td><span data-ttu-id="bf3c8-685">Retorna um valor booleano que indica se o tipo de saudação do valor de saudação é nulo.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-685">Returns a Boolean indicating if hello type of hello value is null.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="bf3c8-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span><span class="sxs-lookup"><span data-stu-id="bf3c8-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span></span></td>
  <td><span data-ttu-id="bf3c8-687">Retorna um valor booleano que indica se o tipo de saudação do valor de saudação é um número.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-687">Returns a Boolean indicating if hello type of hello value is a number.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="bf3c8-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span><span class="sxs-lookup"><span data-stu-id="bf3c8-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span></span></td>
  <td><span data-ttu-id="bf3c8-689">Retorna um valor booleano que indica se o tipo de saudação do valor de saudação é um objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-689">Returns a Boolean indicating if hello type of hello value is a JSON object.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="bf3c8-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span><span class="sxs-lookup"><span data-stu-id="bf3c8-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span></span></td>
  <td><span data-ttu-id="bf3c8-691">Retorna um valor booleano que indica se o tipo de saudação do valor de saudação é uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-691">Returns a Boolean indicating if hello type of hello value is a string.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="bf3c8-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span><span class="sxs-lookup"><span data-stu-id="bf3c8-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span></span></td>
  <td><span data-ttu-id="bf3c8-693">Retorna um valor booleano que indica se a propriedade de saudação foi atribuída um valor.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-693">Returns a Boolean indicating if hello property has been assigned a value.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="bf3c8-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span><span class="sxs-lookup"><span data-stu-id="bf3c8-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span></span></td>
  <td><span data-ttu-id="bf3c8-695">Retorna um valor booleano que indica se tipo de saudação do valor de saudação é cadeia de caracteres, número, booliano ou null.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-695">Returns a Boolean indicating if hello type of hello value is a string, number, Boolean or null.</span></span></td>
</tr>

</table>

<span data-ttu-id="bf3c8-696">Usando essas funções, agora você pode executar consultas com hello seguinte:</span><span class="sxs-lookup"><span data-stu-id="bf3c8-696">Using these functions, you can now run queries like hello following:</span></span>

<span data-ttu-id="bf3c8-697">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-697">**Query**</span></span>

    SELECT VALUE IS_NUMBER(-4)

<span data-ttu-id="bf3c8-698">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-698">**Results**</span></span>

    [true]

### <a name="string-functions"></a><span data-ttu-id="bf3c8-699">Funções de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="bf3c8-699">String functions</span></span>
<span data-ttu-id="bf3c8-700">Olá funções escalares a seguir executam uma operação em um valor de cadeia de caracteres de entrada e retornam uma cadeia de caracteres, o valor numérico ou booleano.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-700">hello following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span> <span data-ttu-id="bf3c8-701">Aqui temos uma tabela de funções de cadeia de caracteres internas:</span><span class="sxs-lookup"><span data-stu-id="bf3c8-701">Here's a table of built-in string functions:</span></span>

| <span data-ttu-id="bf3c8-702">Uso</span><span class="sxs-lookup"><span data-stu-id="bf3c8-702">Usage</span></span> | <span data-ttu-id="bf3c8-703">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf3c8-703">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="bf3c8-704">LENGTH (str_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-704">LENGTH (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |<span data-ttu-id="bf3c8-705">Retorna o número de saudação de caracteres da saudação especificado expressão de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="bf3c8-705">Returns hello number of characters of hello specified string expression</span></span> |
| <span data-ttu-id="bf3c8-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span></span> |<span data-ttu-id="bf3c8-707">Retorna uma cadeia de caracteres que é o resultado de saudação da concatenação de dois ou mais valores de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-707">Returns a string that is hello result of concatenating two or more string values.</span></span> |
| [<span data-ttu-id="bf3c8-708">SUBSTRING (str_expr, num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-708">SUBSTRING (str_expr, num_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |<span data-ttu-id="bf3c8-709">Retorna parte de uma expressão de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-709">Returns part of a string expression.</span></span> |
| [<span data-ttu-id="bf3c8-710">STARTSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-710">STARTSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |<span data-ttu-id="bf3c8-711">Retorna um valor booleano que indica se primeira expressão de cadeia de caracteres hello termina com hello segundo</span><span class="sxs-lookup"><span data-stu-id="bf3c8-711">Returns a Boolean indicating whether hello first string expression ends with hello second</span></span> |
| [<span data-ttu-id="bf3c8-712">ENDSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-712">ENDSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |<span data-ttu-id="bf3c8-713">Retorna um valor booleano que indica se primeira expressão de cadeia de caracteres hello termina com hello segundo</span><span class="sxs-lookup"><span data-stu-id="bf3c8-713">Returns a Boolean indicating whether hello first string expression ends with hello second</span></span> |
| [<span data-ttu-id="bf3c8-714">CONTAINS (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-714">CONTAINS (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |<span data-ttu-id="bf3c8-715">Retorna um valor booleano que indica se a primeira expressão de cadeia de caracteres hello contém Olá segundo.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-715">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span> |
| [<span data-ttu-id="bf3c8-716">INDEX_OF (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-716">INDEX_OF (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |<span data-ttu-id="bf3c8-717">Retorna a saudação iniciando a posição da primeira ocorrência de saudação da segunda expressão de cadeia de caracteres hello na primeira expressão de cadeia de caracteres especificada hello, ou -1 se a cadeia de caracteres de saudação não foi encontrada.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-717">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span> |
| [<span data-ttu-id="bf3c8-718">LEFT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-718">LEFT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |<span data-ttu-id="bf3c8-719">Retorna Olá parte esquerda de uma cadeia de caracteres com hello especificado número de caracteres.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-719">Returns hello left part of a string with hello specified number of characters.</span></span> |
| [<span data-ttu-id="bf3c8-720">RIGHT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-720">RIGHT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |<span data-ttu-id="bf3c8-721">Olá retorna parte direita de uma cadeia de caracteres com hello número especificado de caracteres.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-721">Returns hello right part of a string with hello specified number of characters.</span></span> |
| [<span data-ttu-id="bf3c8-722">LTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-722">LTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |<span data-ttu-id="bf3c8-723">Retorna uma expressão de cadeia de caracteres após remover os espaços em branco iniciais.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-723">Returns a string expression after it removes leading blanks.</span></span> |
| [<span data-ttu-id="bf3c8-724">RTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-724">RTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |<span data-ttu-id="bf3c8-725">Retorna uma expressão de cadeia de caracteres após truncar todos os espaços em branco finais.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-725">Returns a string expression after truncating all trailing blanks.</span></span> |
| [<span data-ttu-id="bf3c8-726">LOWER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-726">LOWER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |<span data-ttu-id="bf3c8-727">Retorna uma expressão de cadeia de caracteres após converter caracteres maiusculos toolowercase de dados.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-727">Returns a string expression after converting uppercase character data toolowercase.</span></span> |
| [<span data-ttu-id="bf3c8-728">UPPER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-728">UPPER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |<span data-ttu-id="bf3c8-729">Retorna uma expressão de cadeia de caracteres após converter caracteres minúsculos toouppercase de dados.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-729">Returns a string expression after converting lowercase character data toouppercase.</span></span> |
| [<span data-ttu-id="bf3c8-730">REPLACE (str_expr, str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-730">REPLACE (str_expr, str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |<span data-ttu-id="bf3c8-731">Substitui todas as ocorrências de um valor de cadeia de caracteres especificado por outro valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-731">Replaces all occurrences of a specified string value with another string value.</span></span> |
| [<span data-ttu-id="bf3c8-732">REPLICATE (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-732">REPLICATE (str_expr, num_expr)</span></span>](https://docs.microsoft.com/azure/cosmos-db/documentdb-sql-query-reference#bk_replicate) |<span data-ttu-id="bf3c8-733">Repete um valor de cadeia de caracteres por um número de vezes especificado.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-733">Repeats a string value a specified number of times.</span></span> |
| [<span data-ttu-id="bf3c8-734">REVERSE (str_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-734">REVERSE (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |<span data-ttu-id="bf3c8-735">Retorna a ordem inversa Olá de um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-735">Returns hello reverse order of a string value.</span></span> |

<span data-ttu-id="bf3c8-736">Usando essas funções, agora você pode executar consultas com hello seguinte.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-736">Using these functions, you can now run queries like hello following.</span></span> <span data-ttu-id="bf3c8-737">Por exemplo, você pode retornar sobrenome Olá em maiusculas da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="bf3c8-737">For example, you can return hello family name in uppercase as follows:</span></span>

<span data-ttu-id="bf3c8-738">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-738">**Query**</span></span>

    SELECT VALUE UPPER(Families.id)
    FROM Families

<span data-ttu-id="bf3c8-739">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-739">**Results**</span></span>

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

<span data-ttu-id="bf3c8-740">Ou concatenar cadeias de caracteres, como neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="bf3c8-740">Or concatenate strings like in this example:</span></span>

<span data-ttu-id="bf3c8-741">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-741">**Query**</span></span>

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

<span data-ttu-id="bf3c8-742">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-742">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


<span data-ttu-id="bf3c8-743">Funções de cadeia de caracteres também podem ser usadas em Olá onde os resultados de toofilter cláusula, como no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="bf3c8-743">String functions can also be used in hello WHERE clause toofilter results, like in hello following example:</span></span>

<span data-ttu-id="bf3c8-744">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-744">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

<span data-ttu-id="bf3c8-745">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-745">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a><span data-ttu-id="bf3c8-746">Funções de matriz</span><span class="sxs-lookup"><span data-stu-id="bf3c8-746">Array functions</span></span>
<span data-ttu-id="bf3c8-747">Olá funções escalares a seguir executam uma operação em um valor de entrada de matriz e retorno numérico, valor booleano ou de matriz.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-747">hello following scalar functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span> <span data-ttu-id="bf3c8-748">Aqui temos uma tabela de funções de matriz internas:</span><span class="sxs-lookup"><span data-stu-id="bf3c8-748">Here's a table of built-in array functions:</span></span>

| <span data-ttu-id="bf3c8-749">Uso</span><span class="sxs-lookup"><span data-stu-id="bf3c8-749">Usage</span></span> | <span data-ttu-id="bf3c8-750">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf3c8-750">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="bf3c8-751">ARRAY_LENGTH (arr_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-751">ARRAY_LENGTH (arr_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |<span data-ttu-id="bf3c8-752">Retorna o número de saudação de elementos da saudação especificado expressão de matriz.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-752">Returns hello number of elements of hello specified array expression.</span></span> |
| <span data-ttu-id="bf3c8-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span></span> |<span data-ttu-id="bf3c8-754">Retorna uma matriz que é o resultado de saudação da concatenação de dois ou mais valores de matriz.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-754">Returns an array that is hello result of concatenating two or more array values.</span></span> |
| <span data-ttu-id="bf3c8-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span></span> |<span data-ttu-id="bf3c8-756">Retorna um valor booleano que indica se a matriz de saudação contém Olá valor especificado.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-756">Returns a Boolean indicating whether hello array contains hello specified value.</span></span> <span data-ttu-id="bf3c8-757">Pode especificar se a correspondência de saudação é completo ou parcial.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-757">Can specify if hello match is full or partial.</span></span> |
| <span data-ttu-id="bf3c8-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span></span> |<span data-ttu-id="bf3c8-759">Retorna parte de uma expressão de matriz.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-759">Returns part of an array expression.</span></span> |

<span data-ttu-id="bf3c8-760">Funções de matriz podem ser matrizes de toomanipulate usado em JSON.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-760">Array functions can be used toomanipulate arrays within JSON.</span></span> <span data-ttu-id="bf3c8-761">Por exemplo, aqui está uma consulta que retorna todos os documentos em que um dos pais hello "Robin Wakefield".</span><span class="sxs-lookup"><span data-stu-id="bf3c8-761">For example, here's a query that returns all documents where one of hello parents is "Robin Wakefield".</span></span> 

<span data-ttu-id="bf3c8-762">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-762">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

<span data-ttu-id="bf3c8-763">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-763">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="bf3c8-764">Você pode especificar um fragmento parcial de elementos na matriz de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-764">You can specify a partial fragment for matching elements within hello array.</span></span> <span data-ttu-id="bf3c8-765">Olá, consulta a seguir localiza todos os pais com hello `givenName` de `Robin`.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-765">hello following query finds all parents with hello `givenName` of `Robin`.</span></span>

<span data-ttu-id="bf3c8-766">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-766">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)

<span data-ttu-id="bf3c8-767">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-767">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]


<span data-ttu-id="bf3c8-768">Aqui está outro exemplo que usa ARRAY_LENGTH tooget Olá número de filhos por família.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-768">Here's another example that uses ARRAY_LENGTH tooget hello number of children per family.</span></span>

<span data-ttu-id="bf3c8-769">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-769">**Query**</span></span>

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

<span data-ttu-id="bf3c8-770">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-770">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a><span data-ttu-id="bf3c8-771">Funções espaciais</span><span class="sxs-lookup"><span data-stu-id="bf3c8-771">Spatial functions</span></span>
<span data-ttu-id="bf3c8-772">Cosmos banco de dados oferece suporte a saudação funções internas do Open Geospatial Consortium (OGC) para consultar geoespaciais a seguir.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-772">Cosmos DB supports hello following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> 

<table>
<tr>
  <td><span data-ttu-id="bf3c8-773"><strong>Uso</strong></span><span class="sxs-lookup"><span data-stu-id="bf3c8-773"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="bf3c8-774"><strong>Descrição</strong></span><span class="sxs-lookup"><span data-stu-id="bf3c8-774"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="bf3c8-775">ST_DISTANCE (point_expr, point_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-775">ST_DISTANCE (point_expr, point_expr)</span></span></td>
  <td><span data-ttu-id="bf3c8-776">Retorna a distância de saudação entre expressões de LineString, Polygon ou ponto GeoJSON Olá dois.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-776">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="bf3c8-777">ST_WITHIN (point_expr, polygon_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-777">ST_WITHIN (point_expr, polygon_expr)</span></span></td>
  <td><span data-ttu-id="bf3c8-778">Retorna uma expressão booleana que indica se o objeto de GeoJSON primeiro Olá (ponto, polígono ou LineString) é no objeto de GeoJSON segundo hello (ponto, polígono ou LineString).</span><span class="sxs-lookup"><span data-stu-id="bf3c8-778">Returns a Boolean expression indicating whether hello first GeoJSON object (Point, Polygon, or LineString) is within hello second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="bf3c8-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="bf3c8-780">Retorna uma expressão booleana que indica se cruzam Olá dois GeoJSON objetos especificados (ponto, polígono ou LineString).</span><span class="sxs-lookup"><span data-stu-id="bf3c8-780">Returns a Boolean expression indicating whether hello two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="bf3c8-781">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="bf3c8-781">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="bf3c8-782">Retorna um valor booliano que indica se a saudação especificado LineString, Polygon ou ponto GeoJSON expressão é válida.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-782">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="bf3c8-783">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="bf3c8-783">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="bf3c8-784">Retorna um valor JSON que contém um valor booliano se Olá especificado expressão LineString, Polygon ou ponto GeoJSON é válido e se for inválido, além disso Olá motivo como um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-784">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="bf3c8-785">Funções espaciais podem ser usado tooperform proximidade consultas em relação aos dados espaciais.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-785">Spatial functions can be used tooperform proximity queries against spatial data.</span></span> <span data-ttu-id="bf3c8-786">Por exemplo, aqui está uma consulta que retorna a que família de todos os documentos que está dentro de 30 km de saudação local especificado usando Olá ST_DISTANCE função interna.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-786">For example, here's a query that returns all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="bf3c8-787">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-787">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="bf3c8-788">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-788">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="bf3c8-789">Para obter detalhes sobre o suporte geoespacial no Cosmos DB, consulte [Trabalhando com os dados geoespaciais no Azure Cosmos DB](geospatial.md).</span><span class="sxs-lookup"><span data-stu-id="bf3c8-789">For more details on geospatial support in Cosmos DB, please see [Working with geospatial data in Azure Cosmos DB](geospatial.md).</span></span> <span data-ttu-id="bf3c8-790">Isso conclui funções espaciais e Olá sintaxe SQL para banco de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-790">That wraps up spatial functions, and hello SQL syntax for Cosmos DB.</span></span> <span data-ttu-id="bf3c8-791">Agora vamos dar uma olhada em como LINQ consultando funciona e como ele interage com a sintaxe de saudação que vimos até agora.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-791">Now let's take a look at how LINQ querying works and how it interacts with hello syntax we've seen so far.</span></span>

## <span data-ttu-id="bf3c8-792"><a id="Linq"></a>LINQ tooDocumentDB API SQL</span><span class="sxs-lookup"><span data-stu-id="bf3c8-792"><a id="Linq"></a>LINQ tooDocumentDB API SQL</span></span>
<span data-ttu-id="bf3c8-793">O LINQ é um modelo de programação .NET que expressa a computação como consultas em fluxos de objetos.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-793">LINQ is a .NET programming model that expresses computation as queries on streams of objects.</span></span> <span data-ttu-id="bf3c8-794">Cosmos DB fornece toointerface uma biblioteca de cliente com o LINQ, facilitando a uma conversão entre objetos JSON e .NET e um mapeamento de um subconjunto de LINQ consulta tooCosmos DB de consultas.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-794">Cosmos DB provides a client-side library toointerface with LINQ by facilitating a conversion between JSON and .NET objects and a mapping from a subset of LINQ queries tooCosmos DB queries.</span></span> 

<span data-ttu-id="bf3c8-795">imagem de saudação abaixo mostra a arquitetura de saudação de dar suporte a consultas LINQ usando o banco de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-795">hello picture below shows hello architecture of supporting LINQ queries using Cosmos DB.</span></span>  <span data-ttu-id="bf3c8-796">Usando o cliente de banco de dados do Cosmos hello, os desenvolvedores podem criar um **IQueryable** que diretamente consultas hello provedor de consulta de banco de dados do Cosmos, que converte a consulta LINQ Olá em uma consulta de banco de dados do Cosmos do objeto.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-796">Using hello Cosmos DB client, developers can create an **IQueryable** object that directly queries hello Cosmos DB query provider, which then translates hello LINQ query into a Cosmos DB query.</span></span> <span data-ttu-id="bf3c8-797">consulta de saudação é então passada toohello tooretrieve do servidor de banco de dados do Cosmos um conjunto de resultados no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-797">hello query is then passed toohello Cosmos DB server tooretrieve a set of results in JSON format.</span></span> <span data-ttu-id="bf3c8-798">Olá retornou resultados são desserializados em um fluxo de objetos .NET no lado do cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-798">hello returned results are deserialized into a stream of .NET objects on hello client side.</span></span>

![Arquitetura de suporte a consultas LINQ usando a API do DocumentDB – sintaxe SQL, linguagem de consulta JSON, conceitos de banco de dados e consultas SQL][1]

### <a name="net-and-json-mapping"></a><span data-ttu-id="bf3c8-800">Mapeamento de .NET e JSON</span><span class="sxs-lookup"><span data-stu-id="bf3c8-800">.NET and JSON mapping</span></span>
<span data-ttu-id="bf3c8-801">Olá o mapeamento entre objetos .NET e documentos JSON é natural - cada campo de membro de dados é mapeado tooa objeto JSON, onde é o nome do campo Olá mapeados toohello "chave", parte do objeto de saudação e parte de "valor" hello recursivamente mapeado toohello parte de valor de objeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-801">hello mapping between .NET objects and JSON documents is natural - each data member field is mapped tooa JSON object, where hello field name is mapped toohello "key" part of hello object and hello "value" part is recursively mapped toohello value part of hello object.</span></span> <span data-ttu-id="bf3c8-802">Considere Olá exemplo a seguir: objeto de família Olá criado é documento JSON de toohello mapeado conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-802">Consider hello following example: hello Family object created is mapped toohello JSON document as shown below.</span></span> <span data-ttu-id="bf3c8-803">E vice-versa, documento JSON de saudação é objeto do .NET tooa back mapeada.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-803">And vice versa, hello JSON document is mapped back tooa .NET object.</span></span>

<span data-ttu-id="bf3c8-804">**Classe C#**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-804">**C# Class**</span></span>

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


<span data-ttu-id="bf3c8-805">**JSON**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-805">**JSON**</span></span>  

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



### <a name="linq-toosql-translation"></a><span data-ttu-id="bf3c8-806">Conversão de tooSQL LINQ</span><span class="sxs-lookup"><span data-stu-id="bf3c8-806">LINQ tooSQL translation</span></span>
<span data-ttu-id="bf3c8-807">provedor de consulta de banco de dados do Cosmos Olá executa um mapeamento de melhor esforço de uma consulta LINQ em uma consulta SQL de banco de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-807">hello Cosmos DB query provider performs a best effort mapping from a LINQ query into a Cosmos DB SQL query.</span></span> <span data-ttu-id="bf3c8-808">Olá descrição a seguir, vamos supor leitor Olá tem uma familiaridade básica do LINQ.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-808">In hello following description, we assume hello reader has a basic familiarity of LINQ.</span></span>

<span data-ttu-id="bf3c8-809">Primeiro, para o sistema de tipo hello, há suporte para todos os tipos de primitivos JSON – tipos numéricos, booliano, cadeia de caracteres e null.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-809">First, for hello type system, we support all JSON primitive types – numeric types, boolean, string, and null.</span></span> <span data-ttu-id="bf3c8-810">Somente esses tipos de JSON têm suporte.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-810">Only these JSON types are supported.</span></span> <span data-ttu-id="bf3c8-811">Olá expressões escalares a seguir têm suporte.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-811">hello following scalar expressions are supported.</span></span>

* <span data-ttu-id="bf3c8-812">Valores de constantes – isso inclui valores constantes Olá primitivos de tipos de dados em tempo de Olá Olá consulta é avaliada.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-812">Constant values – these include constant values of hello primitive data types at hello time hello query is evaluated.</span></span>
* <span data-ttu-id="bf3c8-813">Expressões de índice de matriz/propriedade – essas expressões consulte toohello de propriedade de um objeto ou um elemento de matriz.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-813">Property/array index expressions – these expressions refer toohello property of an object or an array element.</span></span>
  
     <span data-ttu-id="bf3c8-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n é uma variável int</span><span class="sxs-lookup"><span data-stu-id="bf3c8-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n is an int variable</span></span>
* <span data-ttu-id="bf3c8-815">Expressões aritméticas - Incluem expressões aritméticas comuns em valores numéricos e boolianos.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-815">Arithmetic expressions - These include common arithmetic expressions on numerical and boolean values.</span></span> <span data-ttu-id="bf3c8-816">Para a lista completa de hello, consulte toohello SQL specification.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-816">For hello complete list, refer toohello SQL specification.</span></span>
  
     <span data-ttu-id="bf3c8-817">2 * family.children[0].grade;    x + y;</span><span class="sxs-lookup"><span data-stu-id="bf3c8-817">2 * family.children[0].grade;    x + y;</span></span>
* <span data-ttu-id="bf3c8-818">Expressão de comparação de cadeia de caracteres - isso inclui a comparar um valor constante de cadeia de caracteres de toosome de valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-818">String comparison expression - these include comparing a string value toosome constant string value.</span></span>  
  
     <span data-ttu-id="bf3c8-819">mother.familyName == "Smith";    child.givenName == s; //s é uma variável de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="bf3c8-819">mother.familyName == "Smith";    child.givenName == s; //s is a string variable</span></span>
* <span data-ttu-id="bf3c8-820">Expressão de criação de objeto/matriz - estas expressões retornam um objeto do tipo de valor composto ou tipo anônimo ou uma matriz desses objetos.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-820">Object/array creation expression - these expressions return an object of compound value type or anonymous type or an array of such objects.</span></span> <span data-ttu-id="bf3c8-821">Esses valores podem ser aninhados.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-821">These values can be nested.</span></span>
  
     <span data-ttu-id="bf3c8-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //um tipo anônimo com dois campos</span><span class="sxs-lookup"><span data-stu-id="bf3c8-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //an anonymous type with two fields</span></span>              
     <span data-ttu-id="bf3c8-823">novo int[] { 3, child.grade, 5 };</span><span class="sxs-lookup"><span data-stu-id="bf3c8-823">new int[] { 3, child.grade, 5 };</span></span>

### <span data-ttu-id="bf3c8-824"><a id="SupportedLinqOperators"></a>Lista de operadores LINQ com suporte</span><span class="sxs-lookup"><span data-stu-id="bf3c8-824"><a id="SupportedLinqOperators"></a>List of supported LINQ operators</span></span>
<span data-ttu-id="bf3c8-825">Aqui está uma lista de operadores LINQ com suporte no provedor LINQ Olá incluídos com hello SDK .NET do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-825">Here is a list of supported LINQ operators in hello LINQ provider included with hello DocumentDB .NET SDK.</span></span>

* <span data-ttu-id="bf3c8-826">**Selecione**: projeções traduzem toohello SQL SELECT incluindo construção de objeto</span><span class="sxs-lookup"><span data-stu-id="bf3c8-826">**Select**: Projections translate toohello SQL SELECT including object construction</span></span>
* <span data-ttu-id="bf3c8-827">**Onde**: filtros traduzir toohello SQL WHERE e suporte a conversão entre & &, | | e!</span><span class="sxs-lookup"><span data-stu-id="bf3c8-827">**Where**: Filters translate toohello SQL WHERE, and support translation between && , || and !</span></span> <span data-ttu-id="bf3c8-828">operadores SQL toohello</span><span class="sxs-lookup"><span data-stu-id="bf3c8-828">toohello SQL operators</span></span>
* <span data-ttu-id="bf3c8-829">**SelectMany**: permite que o desenrolamento da cláusula de junção SQL toohello de matrizes.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-829">**SelectMany**: Allows unwinding of arrays toohello SQL JOIN clause.</span></span> <span data-ttu-id="bf3c8-830">Pode ser usado toochain/aninhar expressões toofilter em elementos de matriz</span><span class="sxs-lookup"><span data-stu-id="bf3c8-830">Can be used toochain/nest expressions toofilter on array elements</span></span>
* <span data-ttu-id="bf3c8-831">**OrderBy e OrderByDescending**: converte tooORDER BY crescente/decrescente</span><span class="sxs-lookup"><span data-stu-id="bf3c8-831">**OrderBy and OrderByDescending**: Translates tooORDER BY ascending/descending</span></span>
* <span data-ttu-id="bf3c8-832">Operadores **Count**, **Sum**, **Min**, **Max** e **Average** para agregação e os seus equivalentes assíncronos, **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync** e **AverageAsync**.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-832">**Count**, **Sum**, **Min**, **Max**, and **Average** operators for aggregation, and their async equivalents **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, and **AverageAsync**.</span></span>
* <span data-ttu-id="bf3c8-833">**CompareTo**: converte toorange comparações.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-833">**CompareTo**: Translates toorange comparisons.</span></span> <span data-ttu-id="bf3c8-834">Normalmente usados para cadeias de caracteres, já que não são comparáveis no .NET</span><span class="sxs-lookup"><span data-stu-id="bf3c8-834">Commonly used for strings since they’re not comparable in .NET</span></span>
* <span data-ttu-id="bf3c8-835">**Levar**: converte toohello SQL TOP para limitar os resultados de uma consulta</span><span class="sxs-lookup"><span data-stu-id="bf3c8-835">**Take**: Translates toohello SQL TOP for limiting results from a query</span></span>
* <span data-ttu-id="bf3c8-836">**Funções matemáticas**: dá suporte à conversão do. Abs, Acos, Asin do NET, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, logon, Sin, Sqrt, Tan, Truncate funções internas do toohello equivalentes SQL.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-836">**Math Functions**: Supports translation from .NET’s Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="bf3c8-837">**Funções de cadeia de caracteres**: dá suporte à conversão do. Concat, Contains, EndsWith do NET, IndexOf, contagem, ToLower, TrimStart, Replace, inverso, TrimEnd, StartsWith, SubString, ToUpper toohello equivalente SQL funções internas.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-837">**String Functions**: Supports translation from .NET’s Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="bf3c8-838">**Funções de matriz**: dá suporte à conversão do. Concat, Contains e contagem toohello equivalente SQL funções internas do NET.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-838">**Array Functions**: Supports translation from .NET’s Concat, Contains, and Count toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="bf3c8-839">**Funções de extensão geoespaciais**: dá suporte à conversão de métodos de stub distância dentro IsValid e IsValidDetailed toohello equivalente SQL funções internas.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-839">**Geospatial Extension Functions**: Supports translation from stub methods Distance, Within, IsValid, and IsValidDetailed toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="bf3c8-840">**Função de extensão de função definida pelo usuário**: conversão suporta de saudação stub de método UserDefinedFunctionProvider.Invoke toohello correspondente definido pelo usuário função.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-840">**User-Defined Function Extension Function**: Supports translation from hello stub method UserDefinedFunctionProvider.Invoke toohello corresponding user-defined function.</span></span>
* <span data-ttu-id="bf3c8-841">**Diversos**: dá suporte à conversão de saudação de união e operadores condicionais.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-841">**Miscellaneous**: Supports translation of hello coalesce and conditional operators.</span></span> <span data-ttu-id="bf3c8-842">É possível converter a tooString contém CONTAINS, ARRAY_CONTAINS ou Olá IN SQL dependendo do contexto.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-842">Can translate Contains tooString CONTAINS, ARRAY_CONTAINS, or hello SQL IN depending on context.</span></span>

### <a name="sql-query-operators"></a><span data-ttu-id="bf3c8-843">Operadores de consulta SQL</span><span class="sxs-lookup"><span data-stu-id="bf3c8-843">SQL query operators</span></span>
<span data-ttu-id="bf3c8-844">Aqui estão alguns exemplos que ilustram como alguns dos operadores de consulta LINQ padrão Olá são convertidos tooCosmos consultas de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-844">Here are some examples that illustrate how some of hello standard LINQ query operators are translated down tooCosmos DB queries.</span></span>

#### <a name="select-operator"></a><span data-ttu-id="bf3c8-845">Operador Select</span><span class="sxs-lookup"><span data-stu-id="bf3c8-845">Select Operator</span></span>
<span data-ttu-id="bf3c8-846">sintaxe de saudação é `input.Select(x => f(x))`, onde `f` é uma expressão escalar.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-846">hello syntax is `input.Select(x => f(x))`, where `f` is a scalar expression.</span></span>

<span data-ttu-id="bf3c8-847">**Expressão lambda do LINQ**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-847">**LINQ lambda expression**</span></span>

    input.Select(family => family.parents[0].familyName);

<span data-ttu-id="bf3c8-848">**SQL**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-848">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



<span data-ttu-id="bf3c8-849">**Expressão lambda do LINQ**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-849">**LINQ lambda expression**</span></span>

    input.Select(family => family.children[0].grade + c); // c is an int variable


<span data-ttu-id="bf3c8-850">**SQL**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-850">**SQL**</span></span> 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



<span data-ttu-id="bf3c8-851">**Expressão lambda do LINQ**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-851">**LINQ lambda expression**</span></span>

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


<span data-ttu-id="bf3c8-852">**SQL**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-852">**SQL**</span></span> 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a><span data-ttu-id="bf3c8-853">Operador SelectMany</span><span class="sxs-lookup"><span data-stu-id="bf3c8-853">SelectMany operator</span></span>
<span data-ttu-id="bf3c8-854">sintaxe de saudação é `input.SelectMany(x => f(x))`, onde `f` é uma expressão escalar que retorna um tipo de coleção.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-854">hello syntax is `input.SelectMany(x => f(x))`, where `f` is a scalar expression that returns a collection type.</span></span>

<span data-ttu-id="bf3c8-855">**Expressão lambda do LINQ**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-855">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children);

<span data-ttu-id="bf3c8-856">**SQL**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-856">**SQL**</span></span> 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a><span data-ttu-id="bf3c8-857">Operador Where</span><span class="sxs-lookup"><span data-stu-id="bf3c8-857">Where operator</span></span>
<span data-ttu-id="bf3c8-858">sintaxe de saudação é `input.Where(x => f(x))`, onde `f` é uma expressão escalar, que retorna um valor booliano.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-858">hello syntax is `input.Where(x => f(x))`, where `f` is a scalar expression, which returns a Boolean value.</span></span>

<span data-ttu-id="bf3c8-859">**Expressão lambda do LINQ**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-859">**LINQ lambda expression**</span></span>

    input.Where(family=> family.parents[0].familyName == "Smith");

<span data-ttu-id="bf3c8-860">**SQL**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-860">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



<span data-ttu-id="bf3c8-861">**Expressão lambda do LINQ**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-861">**LINQ lambda expression**</span></span>

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

<span data-ttu-id="bf3c8-862">**SQL**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-862">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a><span data-ttu-id="bf3c8-863">Consultas SQL composta</span><span class="sxs-lookup"><span data-stu-id="bf3c8-863">Composite SQL queries</span></span>
<span data-ttu-id="bf3c8-864">Olá acima operadores pode ser composto tooform consultas mais avançadas.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-864">hello above operators can be composed tooform more powerful queries.</span></span> <span data-ttu-id="bf3c8-865">Como Cosmos DB dá suporte a coleções aninhadas, composição Olá pode ser concatenada ou aninhada.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-865">Since Cosmos DB supports nested collections, hello composition can either be concatenated or nested.</span></span>

#### <a name="concatenation"></a><span data-ttu-id="bf3c8-866">Concatenação</span><span class="sxs-lookup"><span data-stu-id="bf3c8-866">Concatenation</span></span>
<span data-ttu-id="bf3c8-867">sintaxe de saudação é `input(.|.SelectMany())(.Select()|.Where())*`.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-867">hello syntax is `input(.|.SelectMany())(.Select()|.Where())*`.</span></span> <span data-ttu-id="bf3c8-868">Uma consulta concatenada pode ser iniciada por uma consulta `SelectMany` opcional, seguida por múltiplos operadores `Select` ou `Where`.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-868">A concatenated query can start with an optional `SelectMany` query followed by multiple `Select` or `Where` operators.</span></span>

<span data-ttu-id="bf3c8-869">**Expressão lambda do LINQ**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-869">**LINQ lambda expression**</span></span>

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

<span data-ttu-id="bf3c8-870">**SQL**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-870">**SQL**</span></span>

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



<span data-ttu-id="bf3c8-871">**Expressão lambda do LINQ**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-871">**LINQ lambda expression**</span></span>

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

<span data-ttu-id="bf3c8-872">**SQL**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-872">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



<span data-ttu-id="bf3c8-873">**Expressão lambda do LINQ**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-873">**LINQ lambda expression**</span></span>

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

<span data-ttu-id="bf3c8-874">**SQL**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-874">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



<span data-ttu-id="bf3c8-875">**Expressão lambda do LINQ**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-875">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

<span data-ttu-id="bf3c8-876">**SQL**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-876">**SQL**</span></span> 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a><span data-ttu-id="bf3c8-877">Aninhamento</span><span class="sxs-lookup"><span data-stu-id="bf3c8-877">Nesting</span></span>
<span data-ttu-id="bf3c8-878">sintaxe de saudação é `input.SelectMany(x=>x.Q())` onde p é um `Select`, `SelectMany`, ou `Where` operador.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-878">hello syntax is `input.SelectMany(x=>x.Q())` where Q is a `Select`, `SelectMany`, or `Where` operator.</span></span>

<span data-ttu-id="bf3c8-879">Em uma consulta aninhada, consulta interna Olá é tooeach aplicada elemento da coleção externa hello.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-879">In a nested query, hello inner query is applied tooeach element of hello outer collection.</span></span> <span data-ttu-id="bf3c8-880">Um recurso importante é a que consulta interna Olá pode fazer referência a campos toohello de elementos Olá coleção externa de saudação como autojunções.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-880">One important feature is that hello inner query can refer toohello fields of hello elements in hello outer collection like self-joins.</span></span>

<span data-ttu-id="bf3c8-881">**Expressão lambda do LINQ**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-881">**LINQ lambda expression**</span></span>

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

<span data-ttu-id="bf3c8-882">**SQL**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-882">**SQL**</span></span> 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


<span data-ttu-id="bf3c8-883">**Expressão lambda do LINQ**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-883">**LINQ lambda expression**</span></span>

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

<span data-ttu-id="bf3c8-884">**SQL**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-884">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



<span data-ttu-id="bf3c8-885">**Expressão lambda do LINQ**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-885">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

<span data-ttu-id="bf3c8-886">**SQL**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-886">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <span data-ttu-id="bf3c8-887"><a id="ExecutingSqlQueries"></a>Execução de consultas SQL</span><span class="sxs-lookup"><span data-stu-id="bf3c8-887"><a id="ExecutingSqlQueries"></a>Executing SQL queries</span></span>
<span data-ttu-id="bf3c8-888">O Cosmos DB expõe recursos por meio de uma API REST que pode ser chamada por qualquer linguagem que possa fazer solicitações HTTP/HTTPS.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-888">Cosmos DB exposes resources through a REST API that can be called by any language capable of making HTTP/HTTPS requests.</span></span> <span data-ttu-id="bf3c8-889">Além disso, o Cosmos DB oferece bibliotecas de programação para várias linguagens populares, como .NET, Node.js, JavaScript e Python.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-889">Additionally, Cosmos DB offers programming libraries for several popular languages like .NET, Node.js, JavaScript, and Python.</span></span> <span data-ttu-id="bf3c8-890">Olá API REST e hello todas as várias bibliotecas, oferecem suporte à consulta por meio do SQL.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-890">hello REST API and hello various libraries all support querying through SQL.</span></span> <span data-ttu-id="bf3c8-891">Olá SDK .NET oferece suporte a LINQ, além de consultar tooSQL.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-891">hello .NET SDK supports LINQ querying in addition tooSQL.</span></span>

<span data-ttu-id="bf3c8-892">Olá seguintes exemplos mostram como toocreate uma consulta e enviá-lo em uma conta de banco de dados do banco de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-892">hello following examples show how toocreate a query and submit it against a Cosmos DB database account.</span></span>

### <span data-ttu-id="bf3c8-893"><a id="RestAPI"></a>API REST</span><span class="sxs-lookup"><span data-stu-id="bf3c8-893"><a id="RestAPI"></a>REST API</span></span>
<span data-ttu-id="bf3c8-894">O Cosmos DB oferece um modelo de programação RESTful por HTTP.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-894">Cosmos DB offers an open RESTful programming model over HTTP.</span></span> <span data-ttu-id="bf3c8-895">As contas do banco de dados podem ser provisionadas usando uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-895">Database accounts can be provisioned using an Azure subscription.</span></span> <span data-ttu-id="bf3c8-896">modelo de recurso de banco de dados do Cosmos Olá consiste em um conjunto de recursos em uma conta de banco de dados, cada um deles é endereçáveis por meio de um URI de lógico e estável.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-896">hello Cosmos DB resource model consists of a set of resources under a database account, each  of which is addressable using a logical and stable URI.</span></span> <span data-ttu-id="bf3c8-897">Um conjunto de recursos é chamado tooas um feed neste documento.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-897">A set of resources is referred tooas a feed in this document.</span></span> <span data-ttu-id="bf3c8-898">Uma conta do banco de dados é formada por um conjunto de bancos de dados, cada um contendo diversas coleções, cada uma delas, por sua vez, contendo documentos, UDFs e outros tipos de recursos.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-898">A database account consists of a set of databases, each containing multiple collections, each of which in-turn contain documents, UDFs, and other resource types.</span></span>

<span data-ttu-id="bf3c8-899">modelo de interação básica Olá com esses recursos é por meio de verbos Olá HTTP GET, PUT, POST e DELETE com a interpretação padrão.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-899">hello basic interaction model with these resources is through hello HTTP verbs GET, PUT, POST, and DELETE with their standard interpretation.</span></span> <span data-ttu-id="bf3c8-900">verbo POST Olá é usado para a criação de um novo recurso, para executar um procedimento armazenado ou para emitir uma consulta de banco de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-900">hello POST verb is used for creation of a new resource, for executing a stored procedure or for issuing a Cosmos DB query.</span></span> <span data-ttu-id="bf3c8-901">As consultas sempre são operações somente leitura, sem efeitos colaterais.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-901">Queries are always read-only operations with no side-effects.</span></span>

<span data-ttu-id="bf3c8-902">Olá exemplos a seguir mostram um POST para uma consulta de API DocumentDB feita em relação a uma coleção que contém dois documentos de exemplo hello que examinamos até o momento.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-902">hello following examples show a POST for a DocumentDB API query made against a collection containing hello two sample documents we've reviewed so far.</span></span> <span data-ttu-id="bf3c8-903">consulta de saudação tem um filtro simples na propriedade de nome hello JSON.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-903">hello query has a simple filter on hello JSON name property.</span></span> <span data-ttu-id="bf3c8-904">Observe o uso de saudação do hello `x-ms-documentdb-isquery` e tipo de conteúdo: `application/query+json` toodenote cabeçalhos que Olá operação é uma consulta.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-904">Note hello use of hello `x-ms-documentdb-isquery` and Content-Type: `application/query+json` headers toodenote that hello operation is a query.</span></span>

<span data-ttu-id="bf3c8-905">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-905">**Request**</span></span>

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


<span data-ttu-id="bf3c8-906">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-906">**Results**</span></span>

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


<span data-ttu-id="bf3c8-907">Olá segundo exemplo mostra uma consulta mais complexa que retorna vários resultados de junção hello.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-907">hello second example shows a more complex query that returns multiple results from hello join.</span></span>

<span data-ttu-id="bf3c8-908">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-908">**Request**</span></span>

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


<span data-ttu-id="bf3c8-909">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="bf3c8-909">**Results**</span></span>

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


<span data-ttu-id="bf3c8-910">Se os resultados da consulta não podem se ajustar dentro de uma única página de resultados, Olá REST API retorna um token de continuação por meio de saudação `x-ms-continuation-token` cabeçalho de resposta.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-910">If a query's results cannot fit within a single page of results, then hello REST API returns a continuation token through hello `x-ms-continuation-token` response header.</span></span> <span data-ttu-id="bf3c8-911">Os clientes podem pagina resultados, incluindo o cabeçalho de saudação nos resultados subsequentes.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-911">Clients can paginate results by including hello header in subsequent results.</span></span> <span data-ttu-id="bf3c8-912">número de saudação de resultados por página também pode ser controlado pela Olá `x-ms-max-item-count` cabeçalho do número.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-912">hello number of results per page can also be controlled through hello `x-ms-max-item-count` number header.</span></span> <span data-ttu-id="bf3c8-913">Se a consulta especificada Olá tem uma função de agregação como `COUNT`, página Olá da consulta pode retornar um valor agregado parcialmente pela página de saudação de resultados.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-913">If hello specified query has an aggregation function like `COUNT`, then hello query page may return a partially aggregated value over hello page of results.</span></span> <span data-ttu-id="bf3c8-914">clientes de saudação deve executar uma agregação de segundo nível sobre esses resultados tooproduce Olá resultados finais, por exemplo, soma contagens de hello retornadas na contagem total de Olá Olá de tooreturn páginas individuais.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-914">hello clients must perform a second-level aggregation over these results tooproduce hello final results, for example, sum over hello counts returned in hello individual pages tooreturn hello total count.</span></span>

<span data-ttu-id="bf3c8-915">política de consistência de dados toomanage Olá para consultas, use Olá `x-ms-consistency-level` cabeçalho como todas as solicitações da API REST.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-915">toomanage hello data consistency policy for queries, use hello `x-ms-consistency-level` header like all REST API requests.</span></span> <span data-ttu-id="bf3c8-916">Para consistência de sessão, ele é necessário tooalso echo hello mais recente `x-ms-session-token` cabeçalho de Cookie na solicitação de consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-916">For session consistency, it is required tooalso echo hello latest `x-ms-session-token` Cookie header in hello query request.</span></span> <span data-ttu-id="bf3c8-917">Olá política de indexação da coleção consultado também pode influenciar consistência Olá dos resultados da consulta.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-917">hello queried collection's indexing policy can also influence hello consistency of query results.</span></span> <span data-ttu-id="bf3c8-918">Com as configurações de política de indexação padrão de saudação, para coleções Olá índice sempre é atual com o conteúdo do documento hello e resultados corresponderem consistência Olá escolhida para dados de consulta.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-918">With hello default indexing policy settings, for collections hello index is always current with hello document contents and query results match hello consistency chosen for data.</span></span> <span data-ttu-id="bf3c8-919">Se Olá política de indexação é reduzida tooLazy, consultas podem retornar resultados atualizados.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-919">If hello indexing policy is relaxed tooLazy, then queries can return stale results.</span></span> <span data-ttu-id="bf3c8-920">Para obter mais informações, consulte [Níveis de consistência no Azure Cosmos DB][consistency-levels].</span><span class="sxs-lookup"><span data-stu-id="bf3c8-920">For more information, see [Azure Cosmos DB Consistency Levels][consistency-levels].</span></span>

<span data-ttu-id="bf3c8-921">Se a política de indexação Olá configurado na coleção de saudação não oferecer suporte a consulta especificada hello, servidor de banco de dados do Azure Cosmos Olá retorna 400 "solicitação incorreta".</span><span class="sxs-lookup"><span data-stu-id="bf3c8-921">If hello configured indexing policy on hello collection cannot support hello specified query, hello Azure Cosmos DB server returns 400 "Bad Request".</span></span> <span data-ttu-id="bf3c8-922">Este código é retornado para consultas de intervalo em caminhos configurados para pesquisas hash (igualdade), e para caminhos excluídos explicitamente da indexação.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-922">This is returned for range queries against paths configured for hash (equality) lookups, and for paths explicitly excluded from indexing.</span></span> <span data-ttu-id="bf3c8-923">Olá `x-ms-documentdb-query-enable-scan` cabeçalho pode ser especificado tooallow Olá consulta tooperform uma verificação quando um índice não está disponível.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-923">hello `x-ms-documentdb-query-enable-scan` header can be specified tooallow hello query tooperform a scan when an index is not available.</span></span>

<span data-ttu-id="bf3c8-924">Você pode obter métricas detalhadas na execução da consulta definindo `x-ms-documentdb-populatequerymetrics` cabeçalho muito`True`.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-924">You can get detailed metrics on query execution by setting `x-ms-documentdb-populatequerymetrics` header too`True`.</span></span> <span data-ttu-id="bf3c8-925">Para obter mais informações, consulte [Métricas de consulta SQL para a API do DocumentDB do Azure Cosmos DB](documentdb-sql-query-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="bf3c8-925">For more information, see [SQL query metrics for Azure Cosmos DB DocumentDB API](documentdb-sql-query-metrics.md).</span></span>

### <span data-ttu-id="bf3c8-926"><a id="DotNetSdk"></a>SDK do C# (.NET)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-926"><a id="DotNetSdk"></a>C# (.NET) SDK</span></span>
<span data-ttu-id="bf3c8-927">Olá SDK .NET oferece suporte a LINQ e SQL consultando.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-927">hello .NET SDK supports both LINQ and SQL querying.</span></span> <span data-ttu-id="bf3c8-928">Olá exemplo a seguir mostra como a consulta de filtro simples Olá tooperform introduzido no início deste documento.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-928">hello following example shows how tooperform hello simple filter query introduced earlier in this document.</span></span>

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


<span data-ttu-id="bf3c8-929">Esta amostra compara duas propriedades quanto à igualdade dentro de cada documento e usa projeções anônimas.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-929">This sample compares two properties for equality within each document and uses anonymous projections.</span></span> 

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


<span data-ttu-id="bf3c8-930">Olá próximo exemplo mostra junções, expressadas por meio de LINQ SelectMany.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-930">hello next sample shows joins, expressed through LINQ SelectMany.</span></span>

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



<span data-ttu-id="bf3c8-931">cliente do .NET Olá automaticamente itera em todas as páginas de saudação dos resultados de consulta em blocos de foreach hello como mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-931">hello .NET client automatically iterates through all hello pages of query results in hello foreach blocks as shown above.</span></span> <span data-ttu-id="bf3c8-932">consulta Olá introduzidas no hello seção da API REST de opções também estão disponíveis no hello SDK do .NET usando Olá `FeedOptions` e `FeedResponse` classes Olá CreateDocumentQuery método.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-932">hello query options introduced in hello REST API section are also available in hello .NET SDK using hello `FeedOptions` and `FeedResponse` classes in hello CreateDocumentQuery method.</span></span> <span data-ttu-id="bf3c8-933">número de saudação de páginas pode ser controlado usando Olá `MaxItemCount` configuração.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-933">hello number of pages can be controlled using hello `MaxItemCount` setting.</span></span> 

<span data-ttu-id="bf3c8-934">Explicitamente você pode controlar a paginação criando `IDocumentQueryable` usando Olá `IQueryable` objeto, em seguida, lendo a` ResponseContinuationToken` valores e transmiti-los de volta como `RequestContinuationToken` em `FeedOptions`.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-934">You can also explicitly control paging by creating `IDocumentQueryable` using hello `IQueryable` object, then by reading the` ResponseContinuationToken` values and passing them back as `RequestContinuationToken` in `FeedOptions`.</span></span> <span data-ttu-id="bf3c8-935">`EnableScanInQuery`pode ser o conjunto tooenable verificações quando consulta Olá não pode ser suportada pela política de indexação de saudação configurada.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-935">`EnableScanInQuery` can be set tooenable scans when hello query cannot be supported by hello configured indexing policy.</span></span> <span data-ttu-id="bf3c8-936">Para as coleções particionadas, você pode usar `PartitionKey` toorun consulta Olá uma única partição (embora Cosmos DB pode extrair esse automaticamente de texto da consulta Olá), e `EnableCrossPartitionQuery` toorun as consultas que talvez seja necessário toobe executadas várias partições.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-936">For partitioned collections, you can use `PartitionKey` toorun hello query against a single partition (though Cosmos DB can automatically extract this from hello query text), and `EnableCrossPartitionQuery` toorun queries that may need toobe run against multiple partitions.</span></span> 

<span data-ttu-id="bf3c8-937">Consulte também[amostras do .NET de banco de dados do Azure Cosmos](https://github.com/Azure/azure-documentdb-net) para obter mais exemplos contêm consultas.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-937">Refer too[Azure Cosmos DB .NET samples](https://github.com/Azure/azure-documentdb-net) for more samples containing queries.</span></span> 

### <span data-ttu-id="bf3c8-938"><a id="JavaScriptServerSideApi"></a>API do lado servidor do JavaScript</span><span class="sxs-lookup"><span data-stu-id="bf3c8-938"><a id="JavaScriptServerSideApi"></a>JavaScript server-side API</span></span>
<span data-ttu-id="bf3c8-939">Cosmos banco de dados fornece um modelo de programação para a execução lógica do aplicativo JavaScript baseado diretamente em coleções de saudação usando procedimentos armazenados e gatilhos.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-939">Cosmos DB provides a programming model for executing JavaScript based application logic directly on hello collections using stored procedures and triggers.</span></span> <span data-ttu-id="bf3c8-940">lógica de JavaScript Olá registrada em um nível de coleção pode emitir, em seguida, operações de banco de dados em operações de saudação em documentos Olá de Olá considerando a coleção.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-940">hello JavaScript logic registered at a collection level can then issue database operations on hello operations on hello documents of hello given collection.</span></span> <span data-ttu-id="bf3c8-941">Essas operações são encapsuladas em transações ACID ambiente.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-941">These operations are wrapped in ambient ACID transactions.</span></span>

<span data-ttu-id="bf3c8-942">Olá exemplo a seguir mostra como as consultas de toouse Olá queryDocuments em toomake Olá API JavaScript do servidor interno procedimentos armazenados e gatilhos.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-942">hello following example shows how toouse hello queryDocuments in hello JavaScript server API toomake queries from inside stored procedures and triggers.</span></span>

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

## <span data-ttu-id="bf3c8-943"><a id="References"></a>Referências</span><span class="sxs-lookup"><span data-stu-id="bf3c8-943"><a id="References"></a>References</span></span>
1. <span data-ttu-id="bf3c8-944">[Introdução tooAzure Cosmos DB][introduction]</span><span class="sxs-lookup"><span data-stu-id="bf3c8-944">[Introduction tooAzure Cosmos DB][introduction]</span></span>
2. [<span data-ttu-id="bf3c8-945">Especificação do SQL no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bf3c8-945">Azure Cosmos DB SQL specification</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=510612)
3. [<span data-ttu-id="bf3c8-946">Amostras do .NET no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bf3c8-946">Azure Cosmos DB .NET samples</span></span>](https://github.com/Azure/azure-documentdb-net)
4. <span data-ttu-id="bf3c8-947">[Níveis de consistência do Azure Cosmos DB][consistency-levels]</span><span class="sxs-lookup"><span data-stu-id="bf3c8-947">[Azure Cosmos DB Consistency Levels][consistency-levels]</span></span>
5. <span data-ttu-id="bf3c8-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span></span>
6. <span data-ttu-id="bf3c8-949">JSON [http://json.org/](http://json.org/)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-949">JSON [http://json.org/](http://json.org/)</span></span>
7. <span data-ttu-id="bf3c8-950">Especificação Javascript [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-950">Javascript Specification [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span></span> 
8. <span data-ttu-id="bf3c8-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span></span> 
9. <span data-ttu-id="bf3c8-952">Técnicas de avaliação de consulta para bancos de dados de grande porte [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span><span class="sxs-lookup"><span data-stu-id="bf3c8-952">Query evaluation techniques for large databases [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span></span>
10. <span data-ttu-id="bf3c8-953">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span><span class="sxs-lookup"><span data-stu-id="bf3c8-953">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span></span>
11. <span data-ttu-id="bf3c8-954">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-954">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span></span>
12. <span data-ttu-id="bf3c8-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span></span>
13. <span data-ttu-id="bf3c8-956">G.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-956">G.</span></span> <span data-ttu-id="bf3c8-957">Graefe.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-957">Graefe.</span></span> <span data-ttu-id="bf3c8-958">estrutura de cascatas de saudação para otimização da consulta.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-958">hello Cascades framework for query optimization.</span></span> <span data-ttu-id="bf3c8-959">IEEE Data Eng.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-959">IEEE Data Eng.</span></span> <span data-ttu-id="bf3c8-960">Bull., 18(3): 1995.</span><span class="sxs-lookup"><span data-stu-id="bf3c8-960">Bull., 18(3): 1995.</span></span>

[1]: ./media/documentdb-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md