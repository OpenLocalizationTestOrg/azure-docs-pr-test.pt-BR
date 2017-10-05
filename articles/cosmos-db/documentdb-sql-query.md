---
title: Consultas SQL para a API do DocumentDB do Azure Cosmos DB | Microsoft Docs
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
ms.openlocfilehash: 9b2b5668ef0552485a86f63a120b57c4623bfe35
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="sql-queries-for-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="545b9-105">Consultas SQL para a API do DocumentDB do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="545b9-105">SQL queries for Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="545b9-106">O Microsoft Azure Cosmos DB dá suporte à consulta de documentos usando a linguagem SQL como uma linguagem de consulta JSON.</span><span class="sxs-lookup"><span data-stu-id="545b9-106">Microsoft Azure Cosmos DB supports querying documents using SQL (Structured Query Language) as a JSON query language.</span></span> <span data-ttu-id="545b9-107">O Cosmos DB é verdadeiramente sem esquemas.</span><span class="sxs-lookup"><span data-stu-id="545b9-107">Cosmos DB is truly schema-free.</span></span> <span data-ttu-id="545b9-108">Em virtude de seu comprometimento com o modelo de dados JSON diretamente dentro do mecanismo do banco de dados, ele fornece a indexação automática de documentos JSON sem a necessidade de esquemas explícitos ou da criação de índices secundários.</span><span class="sxs-lookup"><span data-stu-id="545b9-108">By virtue of its commitment to the JSON data model directly within the database engine, it provides automatic indexing of JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> 

<span data-ttu-id="545b9-109">Ao criar a linguagem de consulta para o Cosmos DB, temos dois objetivos em mente:</span><span class="sxs-lookup"><span data-stu-id="545b9-109">While designing the query language for Cosmos DB, we had two goals in mind:</span></span>

* <span data-ttu-id="545b9-110">Em vez de inventar uma nova linguagem de consulta JSON, queremos oferecer suporte ao SQL.</span><span class="sxs-lookup"><span data-stu-id="545b9-110">Instead of inventing a new JSON query language, we wanted to support SQL.</span></span> <span data-ttu-id="545b9-111">A SQL é uma das linguagens de consulta mais conhecidas e populares.</span><span class="sxs-lookup"><span data-stu-id="545b9-111">SQL is one of the most familiar and popular query languages.</span></span> <span data-ttu-id="545b9-112">O SQL do Cosmos DB fornece um modelo de programação formal para consultas avançadas em documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="545b9-112">Cosmos DB SQL provides a formal programming model for rich queries over JSON documents.</span></span>
* <span data-ttu-id="545b9-113">Como um banco de dados de documentos JSON capaz de executar o JavaScript diretamente no mecanismo do banco de dados, queríamos usar o modelo de programação do JavaScript como os alicerces da nossa linguagem de consulta.</span><span class="sxs-lookup"><span data-stu-id="545b9-113">As a JSON document database capable of executing JavaScript directly in the database engine, we wanted to use JavaScript's programming model as the foundation for our query language.</span></span> <span data-ttu-id="545b9-114">O SQL da API do DocumentDB é baseado no sistema de tipos, na avaliação de expressão e na invocação de função do JavaScript.</span><span class="sxs-lookup"><span data-stu-id="545b9-114">The DocumentDB API SQL is rooted in JavaScript's type system, expression evaluation, and function invocation.</span></span> <span data-ttu-id="545b9-115">Isso, por sua vez, oferece um modelo de programação natural para projeções relacionais, navegação hierárquica em documentos JSON, autojunções, consultas espaciais e invocação de UDFs (funções definidas pelo usuário) gravadas inteiramente em JavaScript, entre outros recursos.</span><span class="sxs-lookup"><span data-stu-id="545b9-115">This in-turn provides a natural programming model for relational projections, hierarchical navigation across JSON documents, self joins, spatial queries, and invocation of user-defined functions (UDFs) written entirely in JavaScript, among other features.</span></span> 

<span data-ttu-id="545b9-116">Nós acreditamos que esses recursos sejam fundamentais para reduzir o atrito entre o aplicativo e o banco de dados e cruciais para a produtividade do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="545b9-116">We believe that these capabilities are key to reducing the friction between the application and the database and are crucial for developer productivity.</span></span>

<span data-ttu-id="545b9-117">Recomendamos que você comece assistindo ao vídeo a seguir, em que Aravind Ramachandran mostra as funcionalidades de consulta do Cosmos DB e visitando nosso [Espaço de Consulta](http://www.documentdb.com/sql/demo), em que você pode experimentar o Cosmos DB e executar consultas SQL em nosso conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="545b9-117">We recommend getting started by watching the following video, where Aravind Ramachandran shows Cosmos DB's querying capabilities, and by visiting our [Query Playground](http://www.documentdb.com/sql/demo), where you can try out Cosmos DB and run SQL queries against our dataset.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

<span data-ttu-id="545b9-118">Em seguida, retorne a este artigo, em que começamos com um tutorial de consulta SQL que apresenta alguns documentos JSON e comandos SQL simples.</span><span class="sxs-lookup"><span data-stu-id="545b9-118">Then, return to this article, where we start with a SQL query tutorial that walks you through some simple JSON documents and SQL commands.</span></span>

## <span data-ttu-id="545b9-119"><a id="GettingStarted"></a>Introdução aos comandos SQL no Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="545b9-119"><a id="GettingStarted"></a>Getting started with SQL commands in Cosmos DB</span></span>
<span data-ttu-id="545b9-120">Para ver o SQL do Cosmos DB em ação, vamos começar com alguns documentos JSON simples e analisar algumas consultas simples neles.</span><span class="sxs-lookup"><span data-stu-id="545b9-120">To see Cosmos DB SQL at work, let's begin with a few simple JSON documents and walk through some simple queries against it.</span></span> <span data-ttu-id="545b9-121">Considere esses dois documentos JSON sobre duas famílias.</span><span class="sxs-lookup"><span data-stu-id="545b9-121">Consider these two JSON documents about two families.</span></span> <span data-ttu-id="545b9-122">Com o Cosmos DB, não precisamos criar nenhum esquema nem índice secundário explicitamente.</span><span class="sxs-lookup"><span data-stu-id="545b9-122">With Cosmos DB, we do not need to create any schemas or secondary indices explicitly.</span></span> <span data-ttu-id="545b9-123">Basta inserir os documentos JSON em uma coleção do Cosmos DB e, em seguida, realizar a consulta.</span><span class="sxs-lookup"><span data-stu-id="545b9-123">We simply need to insert the JSON documents to a Cosmos DB collection and subsequently query.</span></span> <span data-ttu-id="545b9-124">Aqui, temos um documento JSON simples relacionado à família Andersen, os pais, os filhos (e seus animais de estimação), endereço e informações de registro.</span><span class="sxs-lookup"><span data-stu-id="545b9-124">Here we have a simple JSON document for the Andersen family, the parents, children (and their pets), address, and registration information.</span></span> <span data-ttu-id="545b9-125">O documento tem cadeias de caracteres, números, boolianos, matrizes e propriedades aninhadas.</span><span class="sxs-lookup"><span data-stu-id="545b9-125">The document has strings, numbers, Booleans, arrays, and nested properties.</span></span> 

<span data-ttu-id="545b9-126">**Documento**</span><span class="sxs-lookup"><span data-stu-id="545b9-126">**Document**</span></span>  

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

<span data-ttu-id="545b9-127">Aqui está um segundo documento, com uma pequena diferença: `givenName` e `familyName` são usados em vez de `firstName` e `lastName`.</span><span class="sxs-lookup"><span data-stu-id="545b9-127">Here's a second document with one subtle difference – `givenName` and `familyName` are used instead of `firstName` and `lastName`.</span></span>

<span data-ttu-id="545b9-128">**Documento**</span><span class="sxs-lookup"><span data-stu-id="545b9-128">**Document**</span></span>  

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

<span data-ttu-id="545b9-129">Agora, vamos tentar realizar algumas consultas nesses dados para entender alguns dos principais aspectos do SQL da API do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="545b9-129">Now let's try a few queries against this data to understand some of the key aspects of DocumentDB API SQL.</span></span> <span data-ttu-id="545b9-130">Por exemplo, a consulta a seguir retorna documentos cujo campo de ID corresponde a `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="545b9-130">For example, the following query returns the documents where the id field matches `AndersenFamily`.</span></span> <span data-ttu-id="545b9-131">Por se tratar de um `SELECT *`, a saída da consulta será todo o documento JSON:</span><span class="sxs-lookup"><span data-stu-id="545b9-131">Since it's a `SELECT *`, the output of the query is the complete JSON document:</span></span>

<span data-ttu-id="545b9-132">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-132">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="545b9-133">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-133">**Results**</span></span>

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


<span data-ttu-id="545b9-134">Agora, considere um caso em que precisamos reformatar a saída JSON para um formato diferente.</span><span class="sxs-lookup"><span data-stu-id="545b9-134">Now consider the case where we need to reformat the JSON output in a different shape.</span></span> <span data-ttu-id="545b9-135">Esta consulta projeta um novo documento JSON com dois campos selecionados, Nome e Cidade, com a cidade e o estado tendo o mesmo nome.</span><span class="sxs-lookup"><span data-stu-id="545b9-135">This query projects a new JSON object with two selected fields, Name and City, when the address' city has the same name as the state.</span></span> <span data-ttu-id="545b9-136">Neste caso, "NY, NY" é correspondente.</span><span class="sxs-lookup"><span data-stu-id="545b9-136">In this case, "NY, NY" matches.</span></span>

<span data-ttu-id="545b9-137">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-137">**Query**</span></span>    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

<span data-ttu-id="545b9-138">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-138">**Results**</span></span>

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


<span data-ttu-id="545b9-139">A próxima consulta retorna todos os nomes dos filhos na família cuja identificação corresponde ao `WakefieldFamily` solicitado pela cidade de residência.</span><span class="sxs-lookup"><span data-stu-id="545b9-139">The next query returns all the given names of children in the family whose id matches `WakefieldFamily` ordered by the city of residence.</span></span>

<span data-ttu-id="545b9-140">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-140">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

<span data-ttu-id="545b9-141">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-141">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


<span data-ttu-id="545b9-142">Gostaríamos de chamar atenção para alguns aspectos de destaque da linguagem de consulta do Cosmos DB nos exemplos que vimos até agora:</span><span class="sxs-lookup"><span data-stu-id="545b9-142">We would like to draw attention to a few noteworthy aspects of the Cosmos DB query language through the examples we've seen so far:</span></span>  

* <span data-ttu-id="545b9-143">Como o SQL da API do DocumentDB trabalha com valores JSON, ele lida com entidades com formato de árvore em vez de linhas e colunas.</span><span class="sxs-lookup"><span data-stu-id="545b9-143">Since DocumentDB API SQL works on JSON values, it deals with tree shaped entities instead of rows and columns.</span></span> <span data-ttu-id="545b9-144">A linguagem, portanto, possibilita a referência a nós da árvore em qualquer profundidade arbitrária, como `Node1.Node2.Node3…..Nodem`, de forma semelhante à SQL relacional relativa à referência bipartida de `<table>.<column>`.</span><span class="sxs-lookup"><span data-stu-id="545b9-144">Therefore, the language lets you refer to nodes of the tree at any arbitrary depth, like `Node1.Node2.Node3…..Nodem`, similar to relational SQL referring to the two part reference of `<table>.<column>`.</span></span>   
* <span data-ttu-id="545b9-145">A linguagem de consulta estruturada trabalha com dados com menos esquema.</span><span class="sxs-lookup"><span data-stu-id="545b9-145">The structured query language works with schema-less data.</span></span> <span data-ttu-id="545b9-146">Portanto, o sistema de tipos precisa estar vinculado dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="545b9-146">Therefore, the type system needs to be bound dynamically.</span></span> <span data-ttu-id="545b9-147">A mesma expressão pode obter diferentes tipos em diferentes documentos.</span><span class="sxs-lookup"><span data-stu-id="545b9-147">The same expression could yield different types on different documents.</span></span> <span data-ttu-id="545b9-148">O resultado de uma consulta é um valor JSON válido, mas não há garantia de que seja de um esquema fixo.</span><span class="sxs-lookup"><span data-stu-id="545b9-148">The result of a query is a valid JSON value, but is not guaranteed to be of a fixed schema.</span></span>  
* <span data-ttu-id="545b9-149">O Cosmos DB dá suporte apenas a documentos JSON estritos.</span><span class="sxs-lookup"><span data-stu-id="545b9-149">Cosmos DB only supports strict JSON documents.</span></span> <span data-ttu-id="545b9-150">Isto significa que as expressões e sistema de tipos são restritos para lidar somente com tipos JSON.</span><span class="sxs-lookup"><span data-stu-id="545b9-150">This means the type system and expressions are restricted to deal only with JSON types.</span></span> <span data-ttu-id="545b9-151">Consulte a [especificação JSON](http://www.json.org/) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="545b9-151">Refer to the [JSON specification](http://www.json.org/) for more details.</span></span>  
* <span data-ttu-id="545b9-152">Uma coleção do Cosmos DB é um contêiner de documentos JSON sem esquemas.</span><span class="sxs-lookup"><span data-stu-id="545b9-152">A Cosmos DB collection is a schema-free container of JSON documents.</span></span> <span data-ttu-id="545b9-153">As relações nas entidades de dados dentro e entre documentos em uma coleção são capturadas implicitamente pela contenção e não pelas relações chave primária e chave estrangeira.</span><span class="sxs-lookup"><span data-stu-id="545b9-153">The relations in data entities within and across documents in a collection are implicitly captured by containment and not by primary key and foreign key relations.</span></span> <span data-ttu-id="545b9-154">Este é um importante aspecto que vale a pena destacar em virtude das junções intradocumentos abordadas mais adiante neste artigo.</span><span class="sxs-lookup"><span data-stu-id="545b9-154">This is an important aspect worth pointing out in light of the intra-document joins discussed later in this article.</span></span>

## <span data-ttu-id="545b9-155"><a id="Indexing"></a> Indexação do Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="545b9-155"><a id="Indexing"></a> Cosmos DB indexing</span></span>
<span data-ttu-id="545b9-156">Antes de passarmos à sintaxe do SQL da API do DocumentDB, vale a pena explorar o design de indexação no Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="545b9-156">Before we get into the DocumentDB API SQL syntax, it is worth exploring the indexing design in Cosmos DB.</span></span> 

<span data-ttu-id="545b9-157">O objetivo de índices de bancos de dados é atender a consultas em suas diversas formas com um consumo mínimo de recursos (como CPU, entrada/saída), oferecendo alta produtividade e baixa latência.</span><span class="sxs-lookup"><span data-stu-id="545b9-157">The purpose of database indexes is to serve queries in their various forms and shapes with minimum resource consumption (like CPU and input/output) while providing good throughput and low latency.</span></span> <span data-ttu-id="545b9-158">Frequentemente, a escolha do índice correto para consultar um banco de dados requer muito planejamento e experimentação.</span><span class="sxs-lookup"><span data-stu-id="545b9-158">Often, the choice of the right index for querying a database requires much planning and experimentation.</span></span> <span data-ttu-id="545b9-159">Esta abordagem representa um desafio para bancos de dados sem esquemas, nos quais os dados não seguem um esquema rígido e evoluem rapidamente.</span><span class="sxs-lookup"><span data-stu-id="545b9-159">This approach poses a challenge for schema-less databases where the data doesn’t conform to a strict schema and evolves rapidly.</span></span> 

<span data-ttu-id="545b9-160">Portanto, quando criamos o subsistema de indexação do Cosmos DB, definimos os seguintes objetivos:</span><span class="sxs-lookup"><span data-stu-id="545b9-160">Therefore, when we designed the Cosmos DB indexing subsystem, we set the following goals:</span></span>

* <span data-ttu-id="545b9-161">Indexar documentos sem precisar de um esquema: o subsistema de indexação não requer nenhuma informação de esquema e não faz suposições sobre o esquema dos documentos.</span><span class="sxs-lookup"><span data-stu-id="545b9-161">Index documents without requiring schema: The indexing subsystem does not require any schema information or make any assumptions about schema of the documents.</span></span> 
* <span data-ttu-id="545b9-162">Suporte para pesquisas hierárquicas e relacionais avançadas e eficientes: o índice dá suporte à linguagem de pesquisa do Cosmos DB de maneira eficiente, incluindo suporte para projeções hierárquicas e relacionais.</span><span class="sxs-lookup"><span data-stu-id="545b9-162">Support for efficient, rich hierarchical, and relational queries: The index supports the Cosmos DB query language efficiently, including support for hierarchical and relational projections.</span></span>
* <span data-ttu-id="545b9-163">Suporte para consultas consistentes diante do grande volume de gravações: para possibilitar cargas de trabalho com alta produtividade de gravação com consultas consistentes, o índice é atualizado gradativamente, eficientemente e online, em face de um volume contínuo de gravações.</span><span class="sxs-lookup"><span data-stu-id="545b9-163">Support for consistent queries in face of a sustained volume of writes: For high write throughput workloads with consistent queries, the index is updated incrementally, efficiently, and online in the face of a sustained volume of writes.</span></span> <span data-ttu-id="545b9-164">A atualização consistente do índice é crucial para atender às consultas no nível de consistência em que o usuário configurou o sistema.</span><span class="sxs-lookup"><span data-stu-id="545b9-164">The consistent index update is crucial to serve the queries at the consistency level in which the user configured the document service.</span></span>
* <span data-ttu-id="545b9-165">Suporte a multilocatário: dado o modelo baseado em reserva para a governança de recurso entre os locatários, as atualizações do índice são realizadas dentro do orçamento dos recursos do sistema (CPU, memória e operações de entrada/saída por segundo) alocados por réplica.</span><span class="sxs-lookup"><span data-stu-id="545b9-165">Support for multi-tenancy: Given the reservation-based model for resource governance across tenants, index updates are performed within the budget of system resources (CPU, memory, and input/output operations per second) allocated per replica.</span></span> 
* <span data-ttu-id="545b9-166">Eficiência no armazenamento: para manter um bom custo-benefício, a sobrecarga do armazenamento em disco do índice é vinculada e previsível.</span><span class="sxs-lookup"><span data-stu-id="545b9-166">Storage efficiency: For cost effectiveness, the on-disk storage overhead of the index is bounded and predictable.</span></span> <span data-ttu-id="545b9-167">Isto é fundamental porque o Cosmos DB permite que o desenvolvedor faça compensações baseadas em custo entre a sobrecarga do índice em relação ao desempenho da consulta.</span><span class="sxs-lookup"><span data-stu-id="545b9-167">This is crucial because Cosmos DB allows the developer to make cost-based tradeoffs between index overhead in relation to the query performance.</span></span>  

<span data-ttu-id="545b9-168">Consulte as [amostras do Azure Cosmos DB](https://github.com/Azure/azure-documentdb-net) no MSDN para obter amostras que exibem como configurar a política de indexação de uma coleção.</span><span class="sxs-lookup"><span data-stu-id="545b9-168">Refer to the [Azure Cosmos DB samples](https://github.com/Azure/azure-documentdb-net) on MSDN for samples showing how to configure the indexing policy for a collection.</span></span> <span data-ttu-id="545b9-169">Agora, vejamos os detalhes da sintaxe SQL do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="545b9-169">Let’s now get into the details of the Azure Cosmos DB SQL syntax.</span></span>

## <span data-ttu-id="545b9-170"><a id="Basics"></a>Noções básicas de uma consulta SQL do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="545b9-170"><a id="Basics"></a>Basics of an Azure Cosmos DB SQL query</span></span>
<span data-ttu-id="545b9-171">Toda consulta consiste em uma cláusula SELECT e cláusulas FROM e WHERE opcionais de acordo com os padrões ANSI-SQL.</span><span class="sxs-lookup"><span data-stu-id="545b9-171">Every query consists of a SELECT clause and optional FROM and WHERE clauses per ANSI-SQL standards.</span></span> <span data-ttu-id="545b9-172">Normalmente, para cada consulta, a fonte da cláusula FROM é enumerada.</span><span class="sxs-lookup"><span data-stu-id="545b9-172">Typically, for each query, the source in the FROM clause is enumerated.</span></span> <span data-ttu-id="545b9-173">Então, o filtro da cláusula WHERE é aplicado para recuperar um subconjunto de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="545b9-173">Then the filter in the WHERE clause is applied on the source to retrieve a subset of JSON documents.</span></span> <span data-ttu-id="545b9-174">Por fim, a cláusula SELECT é usada para projetar os valores JSON solicitados na lista selecionada.</span><span class="sxs-lookup"><span data-stu-id="545b9-174">Finally, the SELECT clause is used to project the requested JSON values in the select list.</span></span>

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <span data-ttu-id="545b9-175"><a id="FromClause"></a>Cláusula FROM</span><span class="sxs-lookup"><span data-stu-id="545b9-175"><a id="FromClause"></a>FROM clause</span></span>
<span data-ttu-id="545b9-176">A cláusula `FROM <from_specification>` é opcional, a menos que a fonte seja filtrada ou projetada mais adiante na consulta.</span><span class="sxs-lookup"><span data-stu-id="545b9-176">The `FROM <from_specification>` clause is optional unless the source is filtered or projected later in the query.</span></span> <span data-ttu-id="545b9-177">O objetivo desta cláusula é especificar a fonte de dados na qual a consulta deve operar.</span><span class="sxs-lookup"><span data-stu-id="545b9-177">The purpose of this clause is to specify the data source upon which the query must operate.</span></span> <span data-ttu-id="545b9-178">Normalmente, a coleção inteira é a fonte, mas é possível também especificar um subconjunto da coleção.</span><span class="sxs-lookup"><span data-stu-id="545b9-178">Commonly the whole collection is the source, but one can specify a subset of the collection instead.</span></span> 

<span data-ttu-id="545b9-179">Uma consulta como `SELECT * FROM Families` indica que a coleção Families inteira é a fonte a ser enumerada.</span><span class="sxs-lookup"><span data-stu-id="545b9-179">A query like `SELECT * FROM Families` indicates that the entire Families collection is the source over which to enumerate.</span></span> <span data-ttu-id="545b9-180">Um identificador especial ROOT pode ser usado para representar a coleção em vez de usar o nome da coleção.</span><span class="sxs-lookup"><span data-stu-id="545b9-180">A special identifier ROOT can be used to represent the collection instead of using the collection name.</span></span> <span data-ttu-id="545b9-181">A lista a seguir contém as regras que são impostas por uma consulta:</span><span class="sxs-lookup"><span data-stu-id="545b9-181">The following list contains the rules that are enforced per query:</span></span>

* <span data-ttu-id="545b9-182">A coleção pode ter um alias como `SELECT f.id FROM Families AS f`, ou simplesmente `SELECT f.id FROM Families f`.</span><span class="sxs-lookup"><span data-stu-id="545b9-182">The collection can be aliased, such as `SELECT f.id FROM Families AS f` or simply `SELECT f.id FROM Families f`.</span></span> <span data-ttu-id="545b9-183">Aqui, `f` é o equivalente de `Families`.</span><span class="sxs-lookup"><span data-stu-id="545b9-183">Here `f` is the equivalent of `Families`.</span></span> <span data-ttu-id="545b9-184">`AS` é uma palavra-chave opcional que serve como alias para o identificador.</span><span class="sxs-lookup"><span data-stu-id="545b9-184">`AS` is an optional keyword to alias the identifier.</span></span>
* <span data-ttu-id="545b9-185">Após receber um alias, a fonte original não pode ser associada.</span><span class="sxs-lookup"><span data-stu-id="545b9-185">Once aliased, the original source cannot be bound.</span></span> <span data-ttu-id="545b9-186">Por exemplo: `SELECT Families.id FROM Families f` é sintaticamente inválido, pois o identificador "Families" não pode mais ser resolvido.</span><span class="sxs-lookup"><span data-stu-id="545b9-186">For example, `SELECT Families.id FROM Families f` is syntactically invalid since the identifier "Families" cannot be resolved anymore.</span></span>
* <span data-ttu-id="545b9-187">Todas as propriedades que precisam ser referidas devem ser completamente qualificadas.</span><span class="sxs-lookup"><span data-stu-id="545b9-187">All properties that need to be referenced must be fully qualified.</span></span> <span data-ttu-id="545b9-188">Na falta de aderência a um esquema rígido, esta regra é aplicada para evitar associações ambíguas.</span><span class="sxs-lookup"><span data-stu-id="545b9-188">In the absence of strict schema adherence, this is enforced to avoid any ambiguous bindings.</span></span> <span data-ttu-id="545b9-189">Portanto, `SELECT id FROM Families f` é sintaticamente inválido, pois a propriedade `id` não está vinculada.</span><span class="sxs-lookup"><span data-stu-id="545b9-189">Therefore, `SELECT id FROM Families f` is syntactically invalid since the property `id` is not bound.</span></span>

### <a name="subdocuments"></a><span data-ttu-id="545b9-190">Subdocumentos</span><span class="sxs-lookup"><span data-stu-id="545b9-190">Subdocuments</span></span>
<span data-ttu-id="545b9-191">A fonte também pode ser reduzida a um subconjunto menor.</span><span class="sxs-lookup"><span data-stu-id="545b9-191">The source can also be reduced to a smaller subset.</span></span> <span data-ttu-id="545b9-192">Por exemplo, para enumerar somente uma subárvore de cada documento, a sub-raiz pode então se tornar a fonte, como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="545b9-192">For instance, to enumerating only a subtree in each document, the subroot could then become the source, as shown in the following example:</span></span>

<span data-ttu-id="545b9-193">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-193">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="545b9-194">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-194">**Results**</span></span>  

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

<span data-ttu-id="545b9-195">Embora o exemplo acima tenha usado uma matriz como origem, um objeto também pode ser usado como origem, o que é mostrado no exemplo a seguir: qualquer valor JSON válido (não indefinido) que pode ser encontrado na origem é considerado para inclusão no resultado da consulta.</span><span class="sxs-lookup"><span data-stu-id="545b9-195">While the above example used an array as the source, an object could also be used as the source, which is what's shown in the following example: Any valid JSON value (not undefined) that can be found in the source is considered for inclusion in the result of the query.</span></span> <span data-ttu-id="545b9-196">Se algumas famílias não tiverem um valor de `address.state`, elas serão excluídas do resultado da consulta.</span><span class="sxs-lookup"><span data-stu-id="545b9-196">If some families don’t have an `address.state` value, they are excluded in the query result.</span></span>

<span data-ttu-id="545b9-197">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-197">**Query**</span></span>

    SELECT * 
    FROM Families.address.state

<span data-ttu-id="545b9-198">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-198">**Results**</span></span>

    [
      "WA", 
      "NY"
    ]


## <span data-ttu-id="545b9-199"><a id="WhereClause"></a>Cláusula WHERE</span><span class="sxs-lookup"><span data-stu-id="545b9-199"><a id="WhereClause"></a>WHERE clause</span></span>
<span data-ttu-id="545b9-200">A cláusula WHERE (**`WHERE <filter_condition>`**) é opcional.</span><span class="sxs-lookup"><span data-stu-id="545b9-200">The WHERE clause (**`WHERE <filter_condition>`**) is optional.</span></span> <span data-ttu-id="545b9-201">Ela especifica as condições que os documentos JSON fornecidos pela fonte devem satisfazer para serem incluídas como parte dos resultados.</span><span class="sxs-lookup"><span data-stu-id="545b9-201">It specifies the condition(s) that the JSON documents provided by the source must satisfy in order to be included as part of the result.</span></span> <span data-ttu-id="545b9-202">Qualquer documento JSON deve avaliar as condições especificadas como “verdadeiras” para serem consideradas para os resultados.</span><span class="sxs-lookup"><span data-stu-id="545b9-202">Any JSON document must evaluate the specified conditions to "true" to be considered for the result.</span></span> <span data-ttu-id="545b9-203">A cláusula WHERE é usada pela camada do índice para determinar o subconjunto absolutamente menor de documentos fonte que pode fazer parte do resultado.</span><span class="sxs-lookup"><span data-stu-id="545b9-203">The WHERE clause is used by the index layer in order to determine the absolute smallest subset of source documents that can be part of the result.</span></span> 

<span data-ttu-id="545b9-204">A consulta a seguir solicita documentos que contêm uma propriedade de nome cujo valor é `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="545b9-204">The following query requests documents that contain a name property whose value is `AndersenFamily`.</span></span> <span data-ttu-id="545b9-205">Qualquer outro documento que não tiver uma propriedade de nome ou cujo valor não corresponder a `AndersenFamily` será excluído.</span><span class="sxs-lookup"><span data-stu-id="545b9-205">Any other document that does not have a name property, or where the value does not match `AndersenFamily` is excluded.</span></span> 

<span data-ttu-id="545b9-206">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-206">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="545b9-207">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-207">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


<span data-ttu-id="545b9-208">O exemplo anterior mostrou uma consulta de igualdade simples.</span><span class="sxs-lookup"><span data-stu-id="545b9-208">The previous example showed a simple equality query.</span></span> <span data-ttu-id="545b9-209">O SQL da API do DocumentDB também dá suporte a diversas expressões escalares.</span><span class="sxs-lookup"><span data-stu-id="545b9-209">DocumentDB API SQL also supports a variety of scalar expressions.</span></span> <span data-ttu-id="545b9-210">As expressões mais usadas são as binárias e unárias.</span><span class="sxs-lookup"><span data-stu-id="545b9-210">The most commonly used are binary and unary expressions.</span></span> <span data-ttu-id="545b9-211">Referências de propriedade do objeto JSON fonte também são expressões válidas.</span><span class="sxs-lookup"><span data-stu-id="545b9-211">Property references from the source JSON object are also valid expressions.</span></span> 

<span data-ttu-id="545b9-212">Os operadores binários a seguir têm suporte atualmente em consultas como as exemplificadas:</span><span class="sxs-lookup"><span data-stu-id="545b9-212">The following binary operators are currently supported and can be used in queries as shown in the following examples:</span></span>  

<table>
<tr>
<td><span data-ttu-id="545b9-213">Aritmético</span><span class="sxs-lookup"><span data-stu-id="545b9-213">Arithmetic</span></span></td>    
<td><span data-ttu-id="545b9-214">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="545b9-214">+,-,*,/,%</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="545b9-215">Bit a bit</span><span class="sxs-lookup"><span data-stu-id="545b9-215">Bitwise</span></span></td>    
<td><span data-ttu-id="545b9-216">|, &, ^, <<, >>, >>> (deslocamento à direita com preenchimento com zero)</span><span class="sxs-lookup"><span data-stu-id="545b9-216">|, &, ^, <<, >>, >>> (zero-fill right shift)</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="545b9-217">Lógico</span><span class="sxs-lookup"><span data-stu-id="545b9-217">Logical</span></span></td>
<td><span data-ttu-id="545b9-218">AND, OR, NOT</span><span class="sxs-lookup"><span data-stu-id="545b9-218">AND, OR, NOT</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="545b9-219">Comparação</span><span class="sxs-lookup"><span data-stu-id="545b9-219">Comparison</span></span></td>    
<td><span data-ttu-id="545b9-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span><span class="sxs-lookup"><span data-stu-id="545b9-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="545b9-221">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="545b9-221">String</span></span></td>    
<td><span data-ttu-id="545b9-222">|| (concatenado)</span><span class="sxs-lookup"><span data-stu-id="545b9-222">|| (concatenate)</span></span></td>
</tr>
</table>  


<span data-ttu-id="545b9-223">Vejamos algumas consultas que usam valores binários.</span><span class="sxs-lookup"><span data-stu-id="545b9-223">Let’s take a look at some queries using binary operators.</span></span>

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


<span data-ttu-id="545b9-224">Os operadores unários +,-, ~ e NOT também têm suporte e podem ser usados dentro de consultas, como mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="545b9-224">The unary operators +,-, ~ and NOT are also supported, and can be used inside queries as shown in the following example:</span></span>

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



<span data-ttu-id="545b9-225">Além de operadores binários e unários, as referências de propriedade também são permitidas.</span><span class="sxs-lookup"><span data-stu-id="545b9-225">In addition to binary and unary operators, property references are also allowed.</span></span> <span data-ttu-id="545b9-226">Por exemplo, `SELECT * FROM Families f WHERE f.isRegistered` retorna o documento JSON que contém a propriedade `isRegistered`, em que o valor da propriedade é igual ao valor JSON `true`.</span><span class="sxs-lookup"><span data-stu-id="545b9-226">For example, `SELECT * FROM Families f WHERE f.isRegistered` returns the JSON document containing the property `isRegistered` where the property's value is equal to the JSON `true` value.</span></span> <span data-ttu-id="545b9-227">Todos os outros valores (false, null, Indefinido, `<number>`, `<string>`, `<object>`, `<array>` etc.) levam ao documento de origem que está sendo excluído do resultado.</span><span class="sxs-lookup"><span data-stu-id="545b9-227">Any other values (false, null, Undefined, `<number>`, `<string>`, `<object>`, `<array>`, etc.) leads to the source document being excluded from the result.</span></span> 

### <a name="equality-and-comparison-operators"></a><span data-ttu-id="545b9-228">Operadores de igualdade e de comparação</span><span class="sxs-lookup"><span data-stu-id="545b9-228">Equality and comparison operators</span></span>
<span data-ttu-id="545b9-229">A tabela a seguir mostra o resultado de comparações de igualdade no SQL da API do DocumentDB entre dois tipos JSON quaisquer.</span><span class="sxs-lookup"><span data-stu-id="545b9-229">The following table shows the result of equality comparisons in DocumentDB API SQL between any two JSON types.</span></span>

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top"><span data-ttu-id="545b9-230">
            <strong>Op</strong>
         </span><span class="sxs-lookup"><span data-stu-id="545b9-230">
            <strong>Op</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="545b9-231">
            <strong>Indefinido</strong>
         </span><span class="sxs-lookup"><span data-stu-id="545b9-231">
            <strong>Undefined</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="545b9-232">
            <strong>Nulo</strong>
         </span><span class="sxs-lookup"><span data-stu-id="545b9-232">
            <strong>Null</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="545b9-233">
            <strong>Booliano</strong>
         </span><span class="sxs-lookup"><span data-stu-id="545b9-233">
            <strong>Boolean</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="545b9-234">
            <strong>Número</strong>
         </span><span class="sxs-lookup"><span data-stu-id="545b9-234">
            <strong>Number</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="545b9-235">
            <strong>Cadeia de caracteres</strong>
         </span><span class="sxs-lookup"><span data-stu-id="545b9-235">
            <strong>String</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="545b9-236">
            <strong>Objeto</strong>
         </span><span class="sxs-lookup"><span data-stu-id="545b9-236">
            <strong>Object</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="545b9-237">
            <strong>Matriz</strong>
         </span><span class="sxs-lookup"><span data-stu-id="545b9-237">
            <strong>Array</strong>
         </span></span></td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="545b9-238">
            <strong>Indefinido<strong>
         </span><span class="sxs-lookup"><span data-stu-id="545b9-238">
            <strong>Undefined<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="545b9-239">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-239">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-240">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-240">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-241">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-241">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-242">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-242">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-243">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-243">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-244">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-244">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-245">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-245">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="545b9-246">
            <strong>Nulo<strong>
         </span><span class="sxs-lookup"><span data-stu-id="545b9-246">
            <strong>Null<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="545b9-247">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-247">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="545b9-248">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="545b9-248">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="545b9-249">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-249">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-250">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-250">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-251">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-251">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-252">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-252">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-253">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-253">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="545b9-254">
            <strong>Booliano<strong>
         </span><span class="sxs-lookup"><span data-stu-id="545b9-254">
            <strong>Boolean<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="545b9-255">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-255">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-256">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-256">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="545b9-257">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="545b9-257">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="545b9-258">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-258">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-259">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-259">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-260">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-260">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-261">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-261">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="545b9-262">
            <strong>Número<strong>
         </span><span class="sxs-lookup"><span data-stu-id="545b9-262">
            <strong>Number<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="545b9-263">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-263">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-264">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-264">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-265">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-265">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="545b9-266">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="545b9-266">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="545b9-267">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-267">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-268">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-268">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-269">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-269">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="545b9-270">
            <strong>Cadeia de caracteres<strong>
         </span><span class="sxs-lookup"><span data-stu-id="545b9-270">
            <strong>String<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="545b9-271">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-271">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-272">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-272">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-273">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-273">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-274">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-274">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="545b9-275">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="545b9-275">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="545b9-276">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-276">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-277">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-277">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="545b9-278">
            <strong>Objeto<strong>
         </span><span class="sxs-lookup"><span data-stu-id="545b9-278">
            <strong>Object<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="545b9-279">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-279">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-280">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-280">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-281">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-281">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-282">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-282">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-283">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-283">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="545b9-284">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="545b9-284">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="545b9-285">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-285">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="545b9-286">
            <strong>Matriz<strong>
         </span><span class="sxs-lookup"><span data-stu-id="545b9-286">
            <strong>Array<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="545b9-287">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-287">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-288">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-288">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-289">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-289">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-290">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-290">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-291">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-291">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="545b9-292">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-292">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="545b9-293">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="545b9-293">
            <strong>OK</strong>
         </span></span></td>
      </tr>
   </tbody>
</table>

<span data-ttu-id="545b9-294">Para outros operadores de comparação, como >, >=, !=, < e <=, aplicam-se as seguintes regras:</span><span class="sxs-lookup"><span data-stu-id="545b9-294">For other comparison operators such as >, >=, !=, < and <=, the following rules apply:</span></span>   

* <span data-ttu-id="545b9-295">Comparação entre resultados de tipos em Indefinido.</span><span class="sxs-lookup"><span data-stu-id="545b9-295">Comparison across types results in Undefined.</span></span>
* <span data-ttu-id="545b9-296">Comparação entre resultados de dois objetos ou duas matrizes em Indefinido.</span><span class="sxs-lookup"><span data-stu-id="545b9-296">Comparison between two objects or two arrays results in Undefined.</span></span>   

<span data-ttu-id="545b9-297">Se o resultado da expressão escalar do filtro for Indefinido, o documento correspondente não seria incluído no resultado, uma ver que Indefinido não corresponde logicamente a “verdadeiro”.</span><span class="sxs-lookup"><span data-stu-id="545b9-297">If the result of the scalar expression in the filter is Undefined, the corresponding document would not be included in the result, since Undefined doesn't logically equate to "true".</span></span>

### <a name="between-keyword"></a><span data-ttu-id="545b9-298">Palavra-chave BETWEEN</span><span class="sxs-lookup"><span data-stu-id="545b9-298">BETWEEN keyword</span></span>
<span data-ttu-id="545b9-299">Você também pode usar a palavra-chave BETWEEN para expressar consultas a intervalos de valores, como na ANSI SQL.</span><span class="sxs-lookup"><span data-stu-id="545b9-299">You can also use the BETWEEN keyword to express queries against ranges of values like in ANSI SQL.</span></span> <span data-ttu-id="545b9-300">BETWEEN pode ser usado em cadeias de caracteres ou números.</span><span class="sxs-lookup"><span data-stu-id="545b9-300">BETWEEN can be used against strings or numbers.</span></span>

<span data-ttu-id="545b9-301">Por exemplo, esta consulta retorna todos os documentos de família nos quais a série do primeiro filho vai de 1 a 5 (incluindo ambos).</span><span class="sxs-lookup"><span data-stu-id="545b9-301">For example, this query returns all family documents in which the first child's grade is between 1-5 (both inclusive).</span></span> 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

<span data-ttu-id="545b9-302">Diferente da ANSI-SQL, você também pode usar a cláusula BETWEEN na cláusula FROM, como no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="545b9-302">Unlike in ANSI-SQL, you can also use the BETWEEN clause in the FROM clause like in the following example.</span></span>

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

<span data-ttu-id="545b9-303">Para que os tempos de execução das consultas sejam menores, lembre-se de criar uma política de indexação que use um índice do tipo intervalo para quaisquer caminhos/propriedades numéricas que sejam filtradas na cláusula BETWEEN.</span><span class="sxs-lookup"><span data-stu-id="545b9-303">For faster query execution times, remember to create an indexing policy that uses a range index type against any numeric properties/paths that are filtered in the BETWEEN clause.</span></span> 

<span data-ttu-id="545b9-304">A principal diferença entre usar BETWEEN na API do DocumentDB e no ANSI SQL é que você pode expressar consultas de intervalo em propriedades de tipos mistos. Por exemplo, você pode designar “série” como um número (5) em alguns documentos e como cadeias de caracteres em outros (“grade4”).</span><span class="sxs-lookup"><span data-stu-id="545b9-304">The main difference between using BETWEEN in DocumentDB API and ANSI SQL is that you can express range queries against properties of mixed types – for example, you might have "grade" be a number (5) in some documents and strings in others ("grade4").</span></span> <span data-ttu-id="545b9-305">Nesses casos, como no JavaScript, uma comparação entre dois tipos diferentes traz um resultado "indefinido" e o documento é ignorado.</span><span class="sxs-lookup"><span data-stu-id="545b9-305">In these cases, like in JavaScript, a comparison between two different types results in "undefined", and the document will be skipped.</span></span>

### <a name="logical-and-or-and-not-operators"></a><span data-ttu-id="545b9-306">Operadores lógicos (AND, OR e NOT)</span><span class="sxs-lookup"><span data-stu-id="545b9-306">Logical (AND, OR and NOT) operators</span></span>
<span data-ttu-id="545b9-307">Operadores lógicos funcionam em valores boolianos.</span><span class="sxs-lookup"><span data-stu-id="545b9-307">Logical operators operate on Boolean values.</span></span> <span data-ttu-id="545b9-308">As tabelas de verdade lógica desses operadores são mostradas nas tabelas a seguir.</span><span class="sxs-lookup"><span data-stu-id="545b9-308">The logical truth tables for these operators are shown in the following tables.</span></span>

| <span data-ttu-id="545b9-309">OU</span><span class="sxs-lookup"><span data-stu-id="545b9-309">OR</span></span> | <span data-ttu-id="545b9-310">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="545b9-310">True</span></span> | <span data-ttu-id="545b9-311">Falso</span><span class="sxs-lookup"><span data-stu-id="545b9-311">False</span></span> | <span data-ttu-id="545b9-312">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-312">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="545b9-313">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="545b9-313">True</span></span> |<span data-ttu-id="545b9-314">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="545b9-314">True</span></span> |<span data-ttu-id="545b9-315">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="545b9-315">True</span></span> |<span data-ttu-id="545b9-316">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="545b9-316">True</span></span> |
| <span data-ttu-id="545b9-317">Falso</span><span class="sxs-lookup"><span data-stu-id="545b9-317">False</span></span> |<span data-ttu-id="545b9-318">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="545b9-318">True</span></span> |<span data-ttu-id="545b9-319">Falso</span><span class="sxs-lookup"><span data-stu-id="545b9-319">False</span></span> |<span data-ttu-id="545b9-320">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-320">Undefined</span></span> |
| <span data-ttu-id="545b9-321">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-321">Undefined</span></span> |<span data-ttu-id="545b9-322">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="545b9-322">True</span></span> |<span data-ttu-id="545b9-323">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-323">Undefined</span></span> |<span data-ttu-id="545b9-324">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-324">Undefined</span></span> |

| <span data-ttu-id="545b9-325">E</span><span class="sxs-lookup"><span data-stu-id="545b9-325">AND</span></span> | <span data-ttu-id="545b9-326">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="545b9-326">True</span></span> | <span data-ttu-id="545b9-327">Falso</span><span class="sxs-lookup"><span data-stu-id="545b9-327">False</span></span> | <span data-ttu-id="545b9-328">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-328">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="545b9-329">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="545b9-329">True</span></span> |<span data-ttu-id="545b9-330">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="545b9-330">True</span></span> |<span data-ttu-id="545b9-331">Falso</span><span class="sxs-lookup"><span data-stu-id="545b9-331">False</span></span> |<span data-ttu-id="545b9-332">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-332">Undefined</span></span> |
| <span data-ttu-id="545b9-333">Falso</span><span class="sxs-lookup"><span data-stu-id="545b9-333">False</span></span> |<span data-ttu-id="545b9-334">Falso</span><span class="sxs-lookup"><span data-stu-id="545b9-334">False</span></span> |<span data-ttu-id="545b9-335">Falso</span><span class="sxs-lookup"><span data-stu-id="545b9-335">False</span></span> |<span data-ttu-id="545b9-336">Falso</span><span class="sxs-lookup"><span data-stu-id="545b9-336">False</span></span> |
| <span data-ttu-id="545b9-337">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-337">Undefined</span></span> |<span data-ttu-id="545b9-338">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-338">Undefined</span></span> |<span data-ttu-id="545b9-339">Falso</span><span class="sxs-lookup"><span data-stu-id="545b9-339">False</span></span> |<span data-ttu-id="545b9-340">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-340">Undefined</span></span> |

| <span data-ttu-id="545b9-341">NÃO</span><span class="sxs-lookup"><span data-stu-id="545b9-341">NOT</span></span> |  |
| --- | --- |
| <span data-ttu-id="545b9-342">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="545b9-342">True</span></span> |<span data-ttu-id="545b9-343">Falso</span><span class="sxs-lookup"><span data-stu-id="545b9-343">False</span></span> |
| <span data-ttu-id="545b9-344">Falso</span><span class="sxs-lookup"><span data-stu-id="545b9-344">False</span></span> |<span data-ttu-id="545b9-345">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="545b9-345">True</span></span> |
| <span data-ttu-id="545b9-346">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-346">Undefined</span></span> |<span data-ttu-id="545b9-347">Indefinido</span><span class="sxs-lookup"><span data-stu-id="545b9-347">Undefined</span></span> |

### <a name="in-keyword"></a><span data-ttu-id="545b9-348">Palavra-chave IN</span><span class="sxs-lookup"><span data-stu-id="545b9-348">IN keyword</span></span>
<span data-ttu-id="545b9-349">A palavra-chave IN pode ser usada para verificar se um valor especificado corresponde a qualquer dos valores em uma lista.</span><span class="sxs-lookup"><span data-stu-id="545b9-349">The IN keyword can be used to check whether a specified value matches any value in a list.</span></span> <span data-ttu-id="545b9-350">Por exemplo, esta consulta retorna todos os documentos de família cuja ID é "WakefieldFamily" ou então "AndersenFamily".</span><span class="sxs-lookup"><span data-stu-id="545b9-350">For example, this query returns all family documents where the id is one of "WakefieldFamily" or "AndersenFamily".</span></span> 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

<span data-ttu-id="545b9-351">Este exemplo retorna todos os documentos cujo estado é qualquer um dos valores especificados.</span><span class="sxs-lookup"><span data-stu-id="545b9-351">This example returns all documents where the state is any of the specified values.</span></span>

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a><span data-ttu-id="545b9-352">Operadores Ternário (?) e de União (??)</span><span class="sxs-lookup"><span data-stu-id="545b9-352">Ternary (?) and Coalesce (??) operators</span></span>
<span data-ttu-id="545b9-353">Os operadores Ternário e de União podem ser usados para compilar expressões condicionais, de modo semelhante a linguagens de programação populares como C# e JavaScript.</span><span class="sxs-lookup"><span data-stu-id="545b9-353">The Ternary and Coalesce operators can be used to build conditional expressions, similar to popular programming languages like C# and JavaScript.</span></span> 

<span data-ttu-id="545b9-354">O operador Ternário (?) pode ser muito útil para construir novas propriedades JSON com muita rapidez.</span><span class="sxs-lookup"><span data-stu-id="545b9-354">The Ternary (?) operator can be very handy when constructing new JSON properties on the fly.</span></span> <span data-ttu-id="545b9-355">Por exemplo, agora você pode criar consultas para classificar os níveis de classe em um formato legível, como Iniciante/Intermediário/Avançado, como é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="545b9-355">For example, now you can write queries to classify the class levels into a human readable form like Beginner/Intermediate/Advanced as shown below.</span></span>

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

<span data-ttu-id="545b9-356">Você também pode aninhar as chamadas no operador, como na consulta a seguir.</span><span class="sxs-lookup"><span data-stu-id="545b9-356">You can also nest the calls to the operator like in the query below.</span></span>

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

<span data-ttu-id="545b9-357">Assim como outros operadores de consulta, se as propriedades mencionadas na expressão condicional estiverem faltando em algum documento ou se os tipos comparados forem diferentes, esses documentos serão excluídos dos resultados da consulta.</span><span class="sxs-lookup"><span data-stu-id="545b9-357">As with other query operators, if the referenced properties in the conditional expression are missing in any document, or if the types being compared are different, then those documents are excluded in the query results.</span></span>

<span data-ttu-id="545b9-358">O operador de União (??) pode ser usado para verificar de modo eficaz a presença de uma propriedade (ou seja,</span><span class="sxs-lookup"><span data-stu-id="545b9-358">The Coalesce (??) operator can be used to efficiently check for the presence of a property (a.k.a.</span></span> <span data-ttu-id="545b9-359">é definido) em um documento.</span><span class="sxs-lookup"><span data-stu-id="545b9-359">is defined) in a document.</span></span> <span data-ttu-id="545b9-360">Isso é útil ao consultar dados semiestruturados ou dados de tipos mistos.</span><span class="sxs-lookup"><span data-stu-id="545b9-360">This is useful when querying against semi-structured or data of mixed types.</span></span> <span data-ttu-id="545b9-361">Por exemplo, a consulta retorna o "lastName" se estiver presente ou o "surname" se não estiver.</span><span class="sxs-lookup"><span data-stu-id="545b9-361">For example, this query returns the "lastName" if present, or the "surname" if it isn't present.</span></span>

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <span data-ttu-id="545b9-362"><a id="EscapingReservedKeywords"></a>Acessador de propriedade entre aspas</span><span class="sxs-lookup"><span data-stu-id="545b9-362"><a id="EscapingReservedKeywords"></a>Quoted property accessor</span></span>
<span data-ttu-id="545b9-363">Você também pode acessar propriedades usando o operador de propriedade entre aspas `[]`.</span><span class="sxs-lookup"><span data-stu-id="545b9-363">You can also access properties using the quoted property operator `[]`.</span></span> <span data-ttu-id="545b9-364">Por exemplo: `SELECT c.grade` and `SELECT c["grade"]` são equivalentes.</span><span class="sxs-lookup"><span data-stu-id="545b9-364">For example, `SELECT c.grade` and `SELECT c["grade"]` are equivalent.</span></span> <span data-ttu-id="545b9-365">Essa sintaxe é útil quando você precisa substituir uma propriedade que contém espaços, caracteres especiais ou compartilha o mesmo nome que uma palavra-chave ou palavra reservada SQL.</span><span class="sxs-lookup"><span data-stu-id="545b9-365">This syntax is useful when you need to escape a property that contains spaces, special characters, or happens to share the same name as a SQL keyword or reserved word.</span></span>

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <span data-ttu-id="545b9-366"><a id="SelectClause"></a>Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="545b9-366"><a id="SelectClause"></a>SELECT clause</span></span>
<span data-ttu-id="545b9-367">A cláusula SELECT (**`SELECT <select_list>`**) é obrigatória e especifica quais valores são recuperados da consulta, exatamente como ocorre em ANSI-SQL.</span><span class="sxs-lookup"><span data-stu-id="545b9-367">The SELECT clause (**`SELECT <select_list>`**) is mandatory and specifies what values are retrieved from the query, just like in ANSI-SQL.</span></span> <span data-ttu-id="545b9-368">O subconjunto que foi filtrado sobre os documentos fonte é passado à fase de projeção, em que os valores JSON especificados são recuperados e um novo objeto JSON é construído, para cada entrada passada a ele.</span><span class="sxs-lookup"><span data-stu-id="545b9-368">The subset that's been filtered on top of the source documents are passed onto the projection phase, where the specified JSON values are retrieved and a new JSON object is constructed, for each input passed onto it.</span></span> 

<span data-ttu-id="545b9-369">O exemplo a seguir mostra uma consulta SELECT típica.</span><span class="sxs-lookup"><span data-stu-id="545b9-369">The following example shows a typical SELECT query.</span></span> 

<span data-ttu-id="545b9-370">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-370">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="545b9-371">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-371">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a><span data-ttu-id="545b9-372">Propriedades aninhadas</span><span class="sxs-lookup"><span data-stu-id="545b9-372">Nested properties</span></span>
<span data-ttu-id="545b9-373">No exemplo a seguir, estamos projetando duas propriedades aninhadas, `f.address.state` and `f.address.city`.</span><span class="sxs-lookup"><span data-stu-id="545b9-373">In the following example, we are projecting two nested properties `f.address.state` and `f.address.city`.</span></span>

<span data-ttu-id="545b9-374">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-374">**Query**</span></span>

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="545b9-375">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-375">**Results**</span></span>

    [{
      "state": "WA", 
      "city": "seattle"
    }]


<span data-ttu-id="545b9-376">A projeção tem suporte também para expressões JSON, conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="545b9-376">Projection also supports JSON expressions as shown in the following example:</span></span>

<span data-ttu-id="545b9-377">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-377">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="545b9-378">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-378">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


<span data-ttu-id="545b9-379">Vejamos a função de `$1` aqui.</span><span class="sxs-lookup"><span data-stu-id="545b9-379">Let's look at the role of `$1` here.</span></span> <span data-ttu-id="545b9-380">A cláusula `SELECT` precisa criar um objeto JSON e, como nenhuma chave é fornecida, usamos nomes de variáveis de argumento implícito iniciadas por `$1`.</span><span class="sxs-lookup"><span data-stu-id="545b9-380">The `SELECT` clause needs to create a JSON object and since no key is provided, we use implicit argument variable names starting with `$1`.</span></span> <span data-ttu-id="545b9-381">Por exemplo, esta consulta retorna duas variáveis de argumento implícito, rotuladas como `$1` and `$2`.</span><span class="sxs-lookup"><span data-stu-id="545b9-381">For example, this query returns two implicit argument variables, labeled `$1` and `$2`.</span></span>

<span data-ttu-id="545b9-382">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-382">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="545b9-383">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-383">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a><span data-ttu-id="545b9-384">Atribuição de alias</span><span class="sxs-lookup"><span data-stu-id="545b9-384">Aliasing</span></span>
<span data-ttu-id="545b9-385">Agora, vamos estender o exemplo acima com a atribuição explícita de alias aos valores.</span><span class="sxs-lookup"><span data-stu-id="545b9-385">Now let's extend the example above with explicit aliasing of values.</span></span> <span data-ttu-id="545b9-386">AS é a palavra-chave usada para a atribuição de alias.</span><span class="sxs-lookup"><span data-stu-id="545b9-386">AS is the keyword used for aliasing.</span></span> <span data-ttu-id="545b9-387">É opcional, conforme mostrado ao projetar o segundo valor como `NameInfo`.</span><span class="sxs-lookup"><span data-stu-id="545b9-387">It's optional as shown while projecting the second value as `NameInfo`.</span></span> 

<span data-ttu-id="545b9-388">Caso uma consulta tenha duas propriedades com o mesmo nome, a atribuição de alias deve ser usada para renomear uma ou as duas propriedades para que elas não sejam ambíguas no resultado projetado.</span><span class="sxs-lookup"><span data-stu-id="545b9-388">In case a query has two properties with the same name, aliasing must be used to rename one or both of the properties so that they are disambiguated in the projected result.</span></span>

<span data-ttu-id="545b9-389">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-389">**Query**</span></span>

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="545b9-390">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-390">**Results**</span></span>

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a><span data-ttu-id="545b9-391">Expressões escalares</span><span class="sxs-lookup"><span data-stu-id="545b9-391">Scalar expressions</span></span>
<span data-ttu-id="545b9-392">Além de referências de propriedade, a cláusula SELECT dá suporte também a expressões escalares como constantes, expressões aritméticas, expressões lógicas etc. Por exemplo, vejamos uma consulta simples do tipo "Olá mundo".</span><span class="sxs-lookup"><span data-stu-id="545b9-392">In addition to property references, the SELECT clause also supports scalar expressions like constants, arithmetic expressions, logical expressions, etc. For example, here's a simple "Hello World" query.</span></span>

<span data-ttu-id="545b9-393">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-393">**Query**</span></span>

    SELECT "Hello World"

<span data-ttu-id="545b9-394">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-394">**Results**</span></span>

    [{
      "$1": "Hello World"
    }]


<span data-ttu-id="545b9-395">Este é um exemplo mais complexo que usa uma expressão escalar.</span><span class="sxs-lookup"><span data-stu-id="545b9-395">Here's a more complex example that uses a scalar expression.</span></span>

<span data-ttu-id="545b9-396">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-396">**Query**</span></span>

    SELECT ((2 + 11 % 7)-2)/3    

<span data-ttu-id="545b9-397">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-397">**Results**</span></span>

    [{
      "$1": 1.33333
    }]


<span data-ttu-id="545b9-398">No exemplo a seguir, o resultado da expressão escalar é um booliano.</span><span class="sxs-lookup"><span data-stu-id="545b9-398">In the following example, the result of the scalar expression is a Boolean.</span></span>

<span data-ttu-id="545b9-399">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-399">**Query**</span></span>

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

<span data-ttu-id="545b9-400">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-400">**Results**</span></span>

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a><span data-ttu-id="545b9-401">Criação de objeto e de matriz</span><span class="sxs-lookup"><span data-stu-id="545b9-401">Object and array creation</span></span>
<span data-ttu-id="545b9-402">Outro recurso fundamental do SQL da API do DocumentDB é a criação de matriz/objeto.</span><span class="sxs-lookup"><span data-stu-id="545b9-402">Another key feature of DocumentDB API SQL is array/object creation.</span></span> <span data-ttu-id="545b9-403">Observe que, no exemplo anterior, criamos um novo objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="545b9-403">In the previous example, note that we created a new JSON object.</span></span> <span data-ttu-id="545b9-404">De modo semelhante, é possível construir matrizes, como mostram os exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="545b9-404">Similarly, one can also construct arrays as shown in the following examples:</span></span>

<span data-ttu-id="545b9-405">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-405">**Query**</span></span>

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

<span data-ttu-id="545b9-406">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-406">**Results**</span></span>  

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

### <span data-ttu-id="545b9-407"><a id="ValueKeyword"></a>Palavra-chave VALUE</span><span class="sxs-lookup"><span data-stu-id="545b9-407"><a id="ValueKeyword"></a>VALUE keyword</span></span>
<span data-ttu-id="545b9-408">A palavra-chave **VALUE** é uma forma de retornar valores JSON.</span><span class="sxs-lookup"><span data-stu-id="545b9-408">The **VALUE** keyword provides a way to return JSON value.</span></span> <span data-ttu-id="545b9-409">Por exemplo: a consulta mostrada abaixo retorna o `"Hello World"` escalar, em vez de `{$1: "Hello World"}`.</span><span class="sxs-lookup"><span data-stu-id="545b9-409">For example, the query shown below returns the scalar `"Hello World"` instead of `{$1: "Hello World"}`.</span></span>

<span data-ttu-id="545b9-410">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-410">**Query**</span></span>

    SELECT VALUE "Hello World"

<span data-ttu-id="545b9-411">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-411">**Results**</span></span>

    [
      "Hello World"
    ]


<span data-ttu-id="545b9-412">A consulta a seguir retorna o valor JSON sem o rótulo `"address"` nos resultados.</span><span class="sxs-lookup"><span data-stu-id="545b9-412">The following query returns the JSON value without the `"address"` label in the results.</span></span>

<span data-ttu-id="545b9-413">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-413">**Query**</span></span>

    SELECT VALUE f.address
    FROM Families f    

<span data-ttu-id="545b9-414">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-414">**Results**</span></span>  

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

<span data-ttu-id="545b9-415">O exemplo a seguir expande esse procedimento para mostrar como retornar valores JSON primitivos (no nível da folha da árvore JSON).</span><span class="sxs-lookup"><span data-stu-id="545b9-415">The following example extends this to show how to return JSON primitive values (the leaf level of the JSON tree).</span></span> 

<span data-ttu-id="545b9-416">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-416">**Query**</span></span>

    SELECT VALUE f.address.state
    FROM Families f    

<span data-ttu-id="545b9-417">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-417">**Results**</span></span>

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a><span data-ttu-id="545b9-418">* Operador</span><span class="sxs-lookup"><span data-stu-id="545b9-418">* Operator</span></span>
<span data-ttu-id="545b9-419">O operador especial (*) é suportado para projetar o documento da forma que ele é.</span><span class="sxs-lookup"><span data-stu-id="545b9-419">The special operator (*) is supported to project the document as-is.</span></span> <span data-ttu-id="545b9-420">Quando usado, ele deve ser o único campo projetado.</span><span class="sxs-lookup"><span data-stu-id="545b9-420">When used, it must be the only projected field.</span></span> <span data-ttu-id="545b9-421">Embora uma consulta como `SELECT * FROM Families f` seja válida, `SELECT VALUE * FROM Families f ` e `SELECT *, f.id FROM Families f ` não são.</span><span class="sxs-lookup"><span data-stu-id="545b9-421">While a query like `SELECT * FROM Families f` is valid, `SELECT VALUE * FROM Families f ` and  `SELECT *, f.id FROM Families f ` are not valid.</span></span>

<span data-ttu-id="545b9-422">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-422">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="545b9-423">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-423">**Results**</span></span>

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

### <span data-ttu-id="545b9-424"><a id="TopKeyword"></a>Operador TOP</span><span class="sxs-lookup"><span data-stu-id="545b9-424"><a id="TopKeyword"></a>TOP Operator</span></span>
<span data-ttu-id="545b9-425">A palavra-chave TOP pode ser usada para limitar o número de valores de uma consulta.</span><span class="sxs-lookup"><span data-stu-id="545b9-425">The TOP keyword can be used to limit the number of values from a query.</span></span> <span data-ttu-id="545b9-426">Quando TOP é usado em conjunto com a cláusula ORDER BY, o conjunto de resultados é limitado ao primeiro número N de valores ordenados; caso contrário, ele retorna o primeiro número N de resultados em uma ordem indefinida.</span><span class="sxs-lookup"><span data-stu-id="545b9-426">When TOP is used in conjunction with the ORDER BY clause, the result set is limited to the first N number of ordered values; otherwise, it returns the first N number of results in an undefined order.</span></span> <span data-ttu-id="545b9-427">Como melhor prática, em uma instrução SELECT, sempre use uma cláusula ORDER BY com a cláusula TOP.</span><span class="sxs-lookup"><span data-stu-id="545b9-427">As a best practice, in a SELECT statement, always use an ORDER BY clause with the TOP clause.</span></span> <span data-ttu-id="545b9-428">Essa é a única maneira de indicar de modo previsível quais linhas são afetadas pelo TOP.</span><span class="sxs-lookup"><span data-stu-id="545b9-428">This is the only way to predictably indicate which rows are affected by TOP.</span></span> 

<span data-ttu-id="545b9-429">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-429">**Query**</span></span>

    SELECT TOP 1 * 
    FROM Families f 

<span data-ttu-id="545b9-430">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-430">**Results**</span></span>

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

<span data-ttu-id="545b9-431">O TOP pode ser usado com um valor constante (conforme mostrado acima) ou com um valor de variável usando consultas parametrizadas.</span><span class="sxs-lookup"><span data-stu-id="545b9-431">TOP can be used with a constant value (as shown above) or with a variable value using parameterized queries.</span></span> <span data-ttu-id="545b9-432">Para obter mais detalhes, veja as consultas parametrizadas abaixo.</span><span class="sxs-lookup"><span data-stu-id="545b9-432">For more details, please see parameterized queries below.</span></span>

### <span data-ttu-id="545b9-433"><a id="Aggregates"></a>Funções de agregação</span><span class="sxs-lookup"><span data-stu-id="545b9-433"><a id="Aggregates"></a>Aggregate Functions</span></span>
<span data-ttu-id="545b9-434">Você também pode executar agregações na cláusula `SELECT`.</span><span class="sxs-lookup"><span data-stu-id="545b9-434">You can also perform aggregations in the `SELECT` clause.</span></span> <span data-ttu-id="545b9-435">Funções agregadas executam um cálculo em um conjunto de valores e retornam um único valor.</span><span class="sxs-lookup"><span data-stu-id="545b9-435">Aggregate functions perform a calculation on a set of values and return a single value.</span></span> <span data-ttu-id="545b9-436">Por exemplo, a consulta a seguir retorna a contagem de documentos de família dentro da coleção.</span><span class="sxs-lookup"><span data-stu-id="545b9-436">For example, the following query returns the count of family documents within the collection.</span></span>

<span data-ttu-id="545b9-437">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-437">**Query**</span></span>

    SELECT COUNT(1) 
    FROM Families f 

<span data-ttu-id="545b9-438">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-438">**Results**</span></span>

    [{
        "$1": 2
    }]

<span data-ttu-id="545b9-439">Você também pode retornar o valor escalar da agregação usando a palavra-chave `VALUE`.</span><span class="sxs-lookup"><span data-stu-id="545b9-439">You can also return the scalar value of the aggregate by using the `VALUE` keyword.</span></span> <span data-ttu-id="545b9-440">Por exemplo, a consulta a seguir retorna a contagem de valores como um único número:</span><span class="sxs-lookup"><span data-stu-id="545b9-440">For example, the following query returns the count of values as a single number:</span></span>

<span data-ttu-id="545b9-441">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-441">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f 

<span data-ttu-id="545b9-442">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-442">**Results**</span></span>

    [ 2 ]

<span data-ttu-id="545b9-443">Você também pode executar agregações em combinação com filtros.</span><span class="sxs-lookup"><span data-stu-id="545b9-443">You can also perform aggregates in combination with filters.</span></span> <span data-ttu-id="545b9-444">Por exemplo, a consulta a seguir retorna a contagem de documentos com endereço no estado de Washington.</span><span class="sxs-lookup"><span data-stu-id="545b9-444">For example, the following query returns the count of documents with the address in the state of Washington.</span></span>

<span data-ttu-id="545b9-445">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-445">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

<span data-ttu-id="545b9-446">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-446">**Results**</span></span>

    [ 1 ]

<span data-ttu-id="545b9-447">A tabela a seguir mostra a lista de funções de agregação com suporte na API do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="545b9-447">The following table shows the list of supported aggregate functions in DocumentDB API.</span></span> <span data-ttu-id="545b9-448">`SUM` e `AVG` são executados por meio de valores numéricos, enquanto `COUNT`, `MIN` e `MAX` podem ser executados em relação a números, cadeias de caracteres, Boolianos e nulos.</span><span class="sxs-lookup"><span data-stu-id="545b9-448">`SUM` and `AVG` are performed over numeric values, whereas `COUNT`, `MIN`, and `MAX` can be performed over numbers, strings, Booleans, and nulls.</span></span> 

| <span data-ttu-id="545b9-449">Uso</span><span class="sxs-lookup"><span data-stu-id="545b9-449">Usage</span></span> | <span data-ttu-id="545b9-450">Descrição</span><span class="sxs-lookup"><span data-stu-id="545b9-450">Description</span></span> |
|-------|-------------|
| <span data-ttu-id="545b9-451">COUNT</span><span class="sxs-lookup"><span data-stu-id="545b9-451">COUNT</span></span> | <span data-ttu-id="545b9-452">Retorna o número de itens na expressão.</span><span class="sxs-lookup"><span data-stu-id="545b9-452">Returns the number of items in the expression.</span></span> |
| <span data-ttu-id="545b9-453">SUM</span><span class="sxs-lookup"><span data-stu-id="545b9-453">SUM</span></span>   | <span data-ttu-id="545b9-454">Retorna a soma de todos os valores na expressão.</span><span class="sxs-lookup"><span data-stu-id="545b9-454">Returns the sum of all the values in the expression.</span></span> |
| <span data-ttu-id="545b9-455">MÍN.</span><span class="sxs-lookup"><span data-stu-id="545b9-455">MIN</span></span>   | <span data-ttu-id="545b9-456">Retorna o valor mínimo na expressão.</span><span class="sxs-lookup"><span data-stu-id="545b9-456">Returns the minimum value in the expression.</span></span> |
| <span data-ttu-id="545b9-457">MÁX.</span><span class="sxs-lookup"><span data-stu-id="545b9-457">MAX</span></span>   | <span data-ttu-id="545b9-458">Retorna o valor máximo na expressão.</span><span class="sxs-lookup"><span data-stu-id="545b9-458">Returns the maximum value in the expression.</span></span> |
| <span data-ttu-id="545b9-459">AVG</span><span class="sxs-lookup"><span data-stu-id="545b9-459">AVG</span></span>   | <span data-ttu-id="545b9-460">Retorna a média dos valores na expressão.</span><span class="sxs-lookup"><span data-stu-id="545b9-460">Returns the average of the values in the expression.</span></span> |

<span data-ttu-id="545b9-461">Agregações também podem ser executadas em relação aos resultados de uma iteração de matriz.</span><span class="sxs-lookup"><span data-stu-id="545b9-461">Aggregates can also be performed over the results of an array iteration.</span></span> <span data-ttu-id="545b9-462">Para obter mais informações, consulte [Iteração de matriz em consultas](#Iteration).</span><span class="sxs-lookup"><span data-stu-id="545b9-462">For more information, see [Array Iteration in Queries](#Iteration).</span></span>

> [!NOTE]
> <span data-ttu-id="545b9-463">Ao usar o Gerenciador de Consultas do portal do Azure, observe que as consultas de agregação podem retornar resultados parcialmente agregados em uma página de consulta.</span><span class="sxs-lookup"><span data-stu-id="545b9-463">When using the Azure portal's Query Explorer, note that aggregation queries may return the partially aggregated results over a query page.</span></span> <span data-ttu-id="545b9-464">Os SDKs produzem um único valor cumulativo em todas as páginas.</span><span class="sxs-lookup"><span data-stu-id="545b9-464">The SDKs produces a single cumulative value across all pages.</span></span> 
> 
> <span data-ttu-id="545b9-465">Para executar consultas de agregação usando o código, você precisa do .NET SDK 1.12.0, .NET Core SDK 1.1.0 ou Java SDK 1.9.5 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="545b9-465">In order to perform aggregation queries using code, you need .NET SDK 1.12.0, .NET Core SDK 1.1.0, or Java SDK 1.9.5 or above.</span></span>    
>

## <span data-ttu-id="545b9-466"><a id="OrderByClause"></a>Cláusula ORDER BY</span><span class="sxs-lookup"><span data-stu-id="545b9-466"><a id="OrderByClause"></a>ORDER BY clause</span></span>
<span data-ttu-id="545b9-467">Como no ANSI-SQL, agora você pode incluir uma cláusula Order By opcional ao realizar consultas.</span><span class="sxs-lookup"><span data-stu-id="545b9-467">Like in ANSI-SQL, you can include an optional Order By clause while querying.</span></span> <span data-ttu-id="545b9-468">A cláusula pode incluir um argumento ASC/DESC opcional para especificar a ordem na qual os resultados devem ser recuperados.</span><span class="sxs-lookup"><span data-stu-id="545b9-468">The clause can include an optional ASC/DESC argument to specify the order in which results must be retrieved.</span></span>

<span data-ttu-id="545b9-469">Por exemplo, aqui está uma consulta que recupera famílias pela ordem do nome da cidade do residente.</span><span class="sxs-lookup"><span data-stu-id="545b9-469">For example, here's a query that retrieves families in order of the resident city's name.</span></span>

<span data-ttu-id="545b9-470">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-470">**Query**</span></span>

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

<span data-ttu-id="545b9-471">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-471">**Results**</span></span>

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

<span data-ttu-id="545b9-472">E aqui está uma consulta que recupera famílias em ordem de data de criação, que é armazenada como um número que representa a época, ou seja, o tempo decorrido desde 1 de janeiro de 1970, em segundos.</span><span class="sxs-lookup"><span data-stu-id="545b9-472">And here's a query that retrieves families in order of creation date, which is stored as a number representing the epoch time, i.e, elapsed time since Jan 1, 1970 in seconds.</span></span>

<span data-ttu-id="545b9-473">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-473">**Query**</span></span>

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

<span data-ttu-id="545b9-474">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-474">**Results**</span></span>

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

## <span data-ttu-id="545b9-475"><a id="Advanced"></a>Conceitos avançados de banco de dados e consultas SQL</span><span class="sxs-lookup"><span data-stu-id="545b9-475"><a id="Advanced"></a>Advanced database concepts and SQL queries</span></span>

### <span data-ttu-id="545b9-476"><a id="Iteration"></a>Iteração</span><span class="sxs-lookup"><span data-stu-id="545b9-476"><a id="Iteration"></a>Iteration</span></span>
<span data-ttu-id="545b9-477">Um novo constructo foi adicionado por meio da palavra-chave **IN** ao SQL da API do DocumentDB para fornecer suporte à iteração em matrizes JSON.</span><span class="sxs-lookup"><span data-stu-id="545b9-477">A new construct was added via the **IN** keyword in DocumentDB API SQL to provide support for iterating over JSON arrays.</span></span> <span data-ttu-id="545b9-478">A fonte FROM dá suporte à iteração.</span><span class="sxs-lookup"><span data-stu-id="545b9-478">The FROM source provides support for iteration.</span></span> <span data-ttu-id="545b9-479">Comecemos com o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="545b9-479">Let's start with the following example:</span></span>

<span data-ttu-id="545b9-480">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-480">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="545b9-481">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-481">**Results**</span></span>  

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

<span data-ttu-id="545b9-482">Agora, vejamos outra consulta que realiza a iteração em filhos na coleção.</span><span class="sxs-lookup"><span data-stu-id="545b9-482">Now let's look at another query that performs iteration over children in the collection.</span></span> <span data-ttu-id="545b9-483">Observe a diferença na matriz de saída.</span><span class="sxs-lookup"><span data-stu-id="545b9-483">Note the difference in the output array.</span></span> <span data-ttu-id="545b9-484">Este exemplo divide `children` e planifica os resultados em uma única matriz.</span><span class="sxs-lookup"><span data-stu-id="545b9-484">This example splits `children` and flattens the results into a single array.</span></span>  

<span data-ttu-id="545b9-485">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-485">**Query**</span></span>

    SELECT * 
    FROM c IN Families.children

<span data-ttu-id="545b9-486">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-486">**Results**</span></span>  

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

<span data-ttu-id="545b9-487">Isso pode ser usado ainda para filtrar cada entrada individual da matriz, como mostra o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="545b9-487">This can be further used to filter on each individual entry of the array as shown in the following example:</span></span>

<span data-ttu-id="545b9-488">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-488">**Query**</span></span>

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

<span data-ttu-id="545b9-489">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-489">**Results**</span></span>  

    [{
      "givenName": "Lisa"
    }]

<span data-ttu-id="545b9-490">Você também pode executar a agregação sobre o resultado da iteração de matriz.</span><span class="sxs-lookup"><span data-stu-id="545b9-490">You can also perform aggregation over the result of array iteration.</span></span> <span data-ttu-id="545b9-491">Por exemplo, a consulta a seguir conta o número de filhos entre todas as famílias.</span><span class="sxs-lookup"><span data-stu-id="545b9-491">For example, the following query counts the number of children among all families.</span></span>

<span data-ttu-id="545b9-492">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-492">**Query**</span></span>

    SELECT COUNT(child) 
    FROM child IN Families.children

<span data-ttu-id="545b9-493">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-493">**Results**</span></span>  

    [
      { 
        "$1": 3
      }
    ]

### <span data-ttu-id="545b9-494"><a id="Joins"></a>Junções</span><span class="sxs-lookup"><span data-stu-id="545b9-494"><a id="Joins"></a>Joins</span></span>
<span data-ttu-id="545b9-495">Em um banco de dados relacional, a necessidade de realizar junções entre tabelas é importante.</span><span class="sxs-lookup"><span data-stu-id="545b9-495">In a relational database, the need to join across tables is important.</span></span> <span data-ttu-id="545b9-496">É o padrão lógico para criar esquemas normalizados.</span><span class="sxs-lookup"><span data-stu-id="545b9-496">It's the logical corollary to designing normalized schemas.</span></span> <span data-ttu-id="545b9-497">De forma contrária, a API do DocumentDB lida com o modelo de dados desnormalizado dos documentos sem esquemas.</span><span class="sxs-lookup"><span data-stu-id="545b9-497">Contrary to this, DocumentDB API deals with the denormalized data model of schema-free documents.</span></span> <span data-ttu-id="545b9-498">Trata-se do equivalente lógico de uma “autojunção”.</span><span class="sxs-lookup"><span data-stu-id="545b9-498">This is the logical equivalent of a "self-join".</span></span>

<span data-ttu-id="545b9-499">A sintaxe à qual a linguagem oferece suporte é <from_source1> JOIN <from_source2> JOIN ... JUNÇÃO < from_sourceN >.</span><span class="sxs-lookup"><span data-stu-id="545b9-499">The syntax that the language supports is <from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>.</span></span> <span data-ttu-id="545b9-500">De modo geral, isto retorna um conjunto de tuplas **N** (tupla com valores **N**).</span><span class="sxs-lookup"><span data-stu-id="545b9-500">Overall, this returns a set of **N**-tuples (tuple with **N** values).</span></span> <span data-ttu-id="545b9-501">Cada tupla terá os valores produzidos pela iteração de todos os alias da coleção em seus respectivos conjuntos.</span><span class="sxs-lookup"><span data-stu-id="545b9-501">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span> <span data-ttu-id="545b9-502">Em outras palavras, trata-se do produto do cruzamento completo dos conjuntos que participam da junção.</span><span class="sxs-lookup"><span data-stu-id="545b9-502">In other words, this is a full cross product of the sets participating in the join.</span></span>

<span data-ttu-id="545b9-503">Os exemplos a seguir mostram como a cláusula junção funciona.</span><span class="sxs-lookup"><span data-stu-id="545b9-503">The following examples show how the JOIN clause works.</span></span> <span data-ttu-id="545b9-504">No exemplo a seguir, o resultado é vazio porque o produto cruzado de cada documento da fonte e de um conjunto vazio é vazio.</span><span class="sxs-lookup"><span data-stu-id="545b9-504">In the following example, the result is empty since the cross product of each document from source and an empty set is empty.</span></span>

<span data-ttu-id="545b9-505">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-505">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

<span data-ttu-id="545b9-506">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-506">**Results**</span></span>  

    [{
    }]


<span data-ttu-id="545b9-507">No exemplo a seguir, a junção ocorre entre a raiz do documento e a sub-raiz de `children`.</span><span class="sxs-lookup"><span data-stu-id="545b9-507">In the following example, the join is between the document root and the `children` subroot.</span></span> <span data-ttu-id="545b9-508">Trata-se de um produto cruzado entre dois objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="545b9-508">It's a cross product between two JSON objects.</span></span> <span data-ttu-id="545b9-509">O fato de os filhos serem uma matriz não tem efeito sobre a junção, pois estamos lidando com uma única raiz que é a matriz de filhos.</span><span class="sxs-lookup"><span data-stu-id="545b9-509">The fact that children is an array is not effective in the JOIN since we are dealing with a single root that is the children array.</span></span> <span data-ttu-id="545b9-510">Sendo assim, os resultados contêm apenas dois resultados, uma vez que o produto cruzado de cada documento com a matriz resulta em exatamente um documento.</span><span class="sxs-lookup"><span data-stu-id="545b9-510">Hence the result contains only two results, since the cross product of each document with the array yields exactly only one document.</span></span>

<span data-ttu-id="545b9-511">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-511">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.children

<span data-ttu-id="545b9-512">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-512">**Results**</span></span>

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


<span data-ttu-id="545b9-513">O exemplo a seguir mostra uma junção mais convencional:</span><span class="sxs-lookup"><span data-stu-id="545b9-513">The following example shows a more conventional join:</span></span>

<span data-ttu-id="545b9-514">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-514">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

<span data-ttu-id="545b9-515">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-515">**Results**</span></span>

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



<span data-ttu-id="545b9-516">A primeira coisa a observar é que o `from_source` da cláusula **JOIN** é um iterador.</span><span class="sxs-lookup"><span data-stu-id="545b9-516">The first thing to note is that the `from_source` of the **JOIN** clause is an iterator.</span></span> <span data-ttu-id="545b9-517">Sendo assim, neste caso o fluxo é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="545b9-517">So, the flow in this case is as follows:</span></span>  

* <span data-ttu-id="545b9-518">Expanda cada elemento filho **c** na matriz.</span><span class="sxs-lookup"><span data-stu-id="545b9-518">Expand each child element **c** in the array.</span></span>
* <span data-ttu-id="545b9-519">Aplique um produto cruzado com a raiz do documento **f** com cada elemento filho **c** que foi tornado bidimensional na primeira etapa.</span><span class="sxs-lookup"><span data-stu-id="545b9-519">Apply a cross product with the root of the document **f** with each child element **c** that was flattened in the first step.</span></span>
* <span data-ttu-id="545b9-520">Por fim, projete a propriedade do nome do objeto raiz **f** sozinha.</span><span class="sxs-lookup"><span data-stu-id="545b9-520">Finally, project the root object **f** name property alone.</span></span> 

<span data-ttu-id="545b9-521">O primeiro documento (`AndersenFamily`) contém somente um elemento filho, de modo que o conjunto de resultados contém apenas um único objeto correspondente a esse documento.</span><span class="sxs-lookup"><span data-stu-id="545b9-521">The first document (`AndersenFamily`) contains only one child element, so the result set contains only a single object corresponding to this document.</span></span> <span data-ttu-id="545b9-522">O segundo documento (`WakefieldFamily`) contém dois filhos.</span><span class="sxs-lookup"><span data-stu-id="545b9-522">The second document (`WakefieldFamily`) contains two children.</span></span> <span data-ttu-id="545b9-523">Sendo assim, o produto cruzado produz um objeto separado para cada filho, resultando em dois objetos, um para cada filho correspondente a este documento.</span><span class="sxs-lookup"><span data-stu-id="545b9-523">So, the cross product produces a separate object for each child, thereby resulting in two objects, one for each child corresponding to this document.</span></span> <span data-ttu-id="545b9-524">Os campos raiz em ambos os documentos são os mesmos, exatamente como você esperaria em um produto cruzado.</span><span class="sxs-lookup"><span data-stu-id="545b9-524">The root fields in both these documents are the same, just as you would expect in a cross product.</span></span>

<span data-ttu-id="545b9-525">A utilidade real da junção é formar tuplas do produto cruzado em um formato que, de outra forma, seria difícil projetar.</span><span class="sxs-lookup"><span data-stu-id="545b9-525">The real utility of the JOIN is to form tuples from the cross-product in a shape that's otherwise difficult to project.</span></span> <span data-ttu-id="545b9-526">Além disso, como vemos no exemplo abaixo, é possível filtrar a combinação de uma tupla que permite ao usuário escolher uma condição que é atendida pelas tuplas de modo geral.</span><span class="sxs-lookup"><span data-stu-id="545b9-526">Furthermore, as we see in the example below, you could filter on the combination of a tuple that lets' the user chose a condition satisfied by the tuples overall.</span></span>

<span data-ttu-id="545b9-527">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-527">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

<span data-ttu-id="545b9-528">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-528">**Results**</span></span>

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



<span data-ttu-id="545b9-529">Este exemplo é uma extensão natural do exemplo anterior, e realiza uma junção dupla.</span><span class="sxs-lookup"><span data-stu-id="545b9-529">This example is a natural extension of the preceding example, and performs a double join.</span></span> <span data-ttu-id="545b9-530">Assim, o produto cruzado pode ser visto como o pseudocódigo a seguir:</span><span class="sxs-lookup"><span data-stu-id="545b9-530">So, the cross product can be viewed as the following pseudo-code:</span></span>

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

<span data-ttu-id="545b9-531">`AndersenFamily` tem um filho que, por sua vez, tem um animal de estimação.</span><span class="sxs-lookup"><span data-stu-id="545b9-531">`AndersenFamily` has one child who has one pet.</span></span> <span data-ttu-id="545b9-532">Assim, o produto cruzado traz uma linha (1\*1\*1) desta família.</span><span class="sxs-lookup"><span data-stu-id="545b9-532">So, the cross product yields one row (1\*1\*1) from this family.</span></span> <span data-ttu-id="545b9-533">WakefieldFamily, no entanto, tem dois filhos, mas apenas a filha "Jesse" tem animais de estimação.</span><span class="sxs-lookup"><span data-stu-id="545b9-533">WakefieldFamily however has two children, but only one child "Jesse" has pets.</span></span> <span data-ttu-id="545b9-534">Porém, Jesse tem dois animais de estimação.</span><span class="sxs-lookup"><span data-stu-id="545b9-534">Jesse has two pets though.</span></span> <span data-ttu-id="545b9-535">Assim, o produto cruzado traz 1\*1\*2 = 2 linhas desta família.</span><span class="sxs-lookup"><span data-stu-id="545b9-535">Hence the cross product yields 1\*1\*2 = 2 rows from this family.</span></span>

<span data-ttu-id="545b9-536">No próximo exemplo, há um filtro adicional em `pet`.</span><span class="sxs-lookup"><span data-stu-id="545b9-536">In the next example, there is an additional filter on `pet`.</span></span> <span data-ttu-id="545b9-537">Isto exclui todas as tuplas em que o nome do animal não é "Shadow".</span><span class="sxs-lookup"><span data-stu-id="545b9-537">This excludes all the tuples where the pet name is not "Shadow".</span></span> <span data-ttu-id="545b9-538">Observe que podemos criar tuplas por meio de matrizes, filtrar qualquer um dos elementos da tupla e projetas qualquer combinação dos elementos.</span><span class="sxs-lookup"><span data-stu-id="545b9-538">Notice that we are able to build tuples from arrays, filter on any of the elements of the tuple, and project any combination of the elements.</span></span> 

<span data-ttu-id="545b9-539">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-539">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

<span data-ttu-id="545b9-540">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-540">**Results**</span></span>

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <span data-ttu-id="545b9-541"><a id="JavaScriptIntegration"></a>Integração do JavaScript</span><span class="sxs-lookup"><span data-stu-id="545b9-541"><a id="JavaScriptIntegration"></a>JavaScript integration</span></span>
<span data-ttu-id="545b9-542">O Azure Cosmos DB oferece um modelo de programação para executar a lógica de aplicativos baseados em JavaScript diretamente nas coleções, com relação a procedimentos armazenados e gatilhos.</span><span class="sxs-lookup"><span data-stu-id="545b9-542">Azure Cosmos DB provides a programming model for executing JavaScript based application logic directly on the collections in terms of stored procedures and triggers.</span></span> <span data-ttu-id="545b9-543">Isso possibilita:</span><span class="sxs-lookup"><span data-stu-id="545b9-543">This allows for both:</span></span>

* <span data-ttu-id="545b9-544">Capacidade de realizar operações CRUD transacionais de alto desempenho e consultas documentos em uma coleção devido à profunda integração do tempo de execução do JavaScript diretamente ao mecanismo de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="545b9-544">Ability to do high-performance transactional CRUD operations and queries against documents in a collection by virtue of the deep integration of JavaScript runtime directly within the database engine.</span></span> 
* <span data-ttu-id="545b9-545">Um modelamento natural de fluxo de controle, escopo de variáveis, atribuição e integração de primitivos que lidam com exceções com transações de bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="545b9-545">A natural modeling of control flow, variable scoping, and assignment and integration of exception handling primitives with database transactions.</span></span> <span data-ttu-id="545b9-546">Para obter detalhes sobre o suporte do Azure Cosmos DB à integração com JavaScript, consulte a documentação sobre programação JavaScript do lado do servidor.</span><span class="sxs-lookup"><span data-stu-id="545b9-546">For more details about Azure Cosmos DB support for JavaScript integration, please refer to the JavaScript server-side programmability documentation.</span></span>

### <span data-ttu-id="545b9-547"><a id="UserDefinedFunctions"></a>UDFs (Funções Definidas pelo Usuário)</span><span class="sxs-lookup"><span data-stu-id="545b9-547"><a id="UserDefinedFunctions"></a>User-Defined Functions (UDFs)</span></span>
<span data-ttu-id="545b9-548">Além dos tipos já definidos neste artigo, o SQL da API do DocumentDB fornece suporte a UDFs (Funções Definidas pelo Usuário).</span><span class="sxs-lookup"><span data-stu-id="545b9-548">Along with the types already defined in this article, DocumentDB API SQL provides support for User Defined Functions (UDF).</span></span> <span data-ttu-id="545b9-549">Em particular, há suporte a UDFs escalares nas quais os desenvolvedores podem passar zero ou muitos argumentos e retornar um resultado com um único argumento.</span><span class="sxs-lookup"><span data-stu-id="545b9-549">In particular, scalar UDFs are supported where the developers can pass in zero or many arguments and return a single argument result back.</span></span> <span data-ttu-id="545b9-550">Cada um desses argumentos é verificado para definir se são valores JSON legais.</span><span class="sxs-lookup"><span data-stu-id="545b9-550">Each of these arguments is checked for being legal JSON values.</span></span>  

<span data-ttu-id="545b9-551">A sintaxe SQL da API do DocumentDB é estendida para dar suporte à lógica de aplicativos personalizados usando essas Funções Definidas pelo Usuário.</span><span class="sxs-lookup"><span data-stu-id="545b9-551">The DocumentDB API SQL syntax is extended to support custom application logic using these User-Defined Functions.</span></span> <span data-ttu-id="545b9-552">As UDFs podem ser registradas na API do DocumentDB e então referenciadas como parte de uma consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="545b9-552">UDFs can be registered with DocumentDB API and then be referenced as part of a SQL query.</span></span> <span data-ttu-id="545b9-553">De fato, as UDFs são projetadas de maneira especial para serem invocadas por consultas.</span><span class="sxs-lookup"><span data-stu-id="545b9-553">In fact, the UDFs are exquisitely designed to be invoked by queries.</span></span> <span data-ttu-id="545b9-554">Como consequência dessa escolha, as UDFs não têm acesso ao objeto de contexto que outros tipos de JavaScript (procedimentos armazenados e gatilhos) têm.</span><span class="sxs-lookup"><span data-stu-id="545b9-554">As a corollary to this choice, UDFs do not have access to the context object which the other JavaScript types (stored procedures and triggers) have.</span></span> <span data-ttu-id="545b9-555">Como as consultas são executadas como somente leitura, elas podem ser executadas em réplicas primárias ou secundárias.</span><span class="sxs-lookup"><span data-stu-id="545b9-555">Since queries execute as read-only, they can run either on primary or on secondary replicas.</span></span> <span data-ttu-id="545b9-556">Portanto, as UDFs foram criadas para serem executadas em réplicas secundárias, diferente de outros tipos de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="545b9-556">Therefore, UDFs are designed to run on secondary replicas unlike other JavaScript types.</span></span>

<span data-ttu-id="545b9-557">Veja abaixo um exemplo de como uma UDF pode ser registrada no banco de dados do Cosmos DB, especificamente em uma coleção de documentos.</span><span class="sxs-lookup"><span data-stu-id="545b9-557">Below is an example of how a UDF can be registered at the Cosmos DB database, specifically under a document collection.</span></span>

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

<span data-ttu-id="545b9-558">O exemplo anterior cria um UDF cujo nome é `REGEX_MATCH`.</span><span class="sxs-lookup"><span data-stu-id="545b9-558">The preceding example creates a UDF whose name is `REGEX_MATCH`.</span></span> <span data-ttu-id="545b9-559">Ele aceita dois valores de cadeia de caracteres JSON `input` and `pattern` , além de verificar, pelo uso da função string.match() do JavaScript, se o primeiro desses valores corresponde ao padrão especificado no segundo.</span><span class="sxs-lookup"><span data-stu-id="545b9-559">It accepts two JSON string values `input` and `pattern` and checks if the first matches the pattern specified in the second using JavaScript's string.match() function.</span></span>

<span data-ttu-id="545b9-560">Agora, podemos usar esta UDF em uma consulta em uma projeção.</span><span class="sxs-lookup"><span data-stu-id="545b9-560">We can now use this UDF in a query in a projection.</span></span> <span data-ttu-id="545b9-561">UDFs devem ser qualificadas com o prefixo que diferencia maiúsculas de minúsculas "udf."</span><span class="sxs-lookup"><span data-stu-id="545b9-561">UDFs must be qualified with the case-sensitive prefix "udf."</span></span> <span data-ttu-id="545b9-562">quando chamadas por meio de consultas.</span><span class="sxs-lookup"><span data-stu-id="545b9-562">when called from within queries.</span></span> 

> [!NOTE]
> <span data-ttu-id="545b9-563">Antes de 17/03/2015, o Cosmos DB dava suporte a chamadas a UDF sem o prefixo “udf”.</span><span class="sxs-lookup"><span data-stu-id="545b9-563">Prior to 3/17/2015, Cosmos DB supported UDF calls without the "udf."</span></span> <span data-ttu-id="545b9-564">como SELECT REGEX_MATCH().</span><span class="sxs-lookup"><span data-stu-id="545b9-564">prefix like SELECT REGEX_MATCH().</span></span> <span data-ttu-id="545b9-565">Esse padrão de chamada foi preterido.</span><span class="sxs-lookup"><span data-stu-id="545b9-565">This calling pattern has been deprecated.</span></span>  
> 
> 

<span data-ttu-id="545b9-566">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-566">**Query**</span></span>

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

<span data-ttu-id="545b9-567">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-567">**Results**</span></span>

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

<span data-ttu-id="545b9-568">A UDF também pode ser usada dentro de um filtro, conforme mostrado no exemplo abaixo, também qualificado com o prefixo "udf."</span><span class="sxs-lookup"><span data-stu-id="545b9-568">The UDF can also be used inside a filter as shown in the example below, also qualified with the "udf."</span></span> <span data-ttu-id="545b9-569">prefixo:</span><span class="sxs-lookup"><span data-stu-id="545b9-569">prefix:</span></span>

<span data-ttu-id="545b9-570">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-570">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

<span data-ttu-id="545b9-571">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-571">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


<span data-ttu-id="545b9-572">Basicamente, as UDFs são expressões escalares válidas e podem ser usadas em projeções e filtros.</span><span class="sxs-lookup"><span data-stu-id="545b9-572">In essence, UDFs are valid scalar expressions and can be used in both projections and filters.</span></span> 

<span data-ttu-id="545b9-573">Para expandir o poder das UDFs, vejamos outro exemplo com lógica condicional:</span><span class="sxs-lookup"><span data-stu-id="545b9-573">To expand on the power of UDFs, let's look at another example with conditional logic:</span></span>

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


<span data-ttu-id="545b9-574">Abaixo há um exemplo que aplica a UDF.</span><span class="sxs-lookup"><span data-stu-id="545b9-574">Below is an example that exercises the UDF.</span></span>

<span data-ttu-id="545b9-575">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-575">**Query**</span></span>

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

<span data-ttu-id="545b9-576">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-576">**Results**</span></span>

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


<span data-ttu-id="545b9-577">Como os exemplos anteriores demonstram, as UDFs integram o poder da linguagem JavaScript ao SQL da API do DocumentDB para fornecer uma avançada interface programável, a fim de realizar uma lógica complexa, condicional e de procedimentos com a ajuda das funcionalidades em tempo de execução internas do JavaScript.</span><span class="sxs-lookup"><span data-stu-id="545b9-577">As the preceding examples showcase, UDFs integrate the power of JavaScript language with the DocumentDB API SQL to provide a rich programmable interface to do complex procedural, conditional logic with the help of inbuilt JavaScript runtime capabilities.</span></span>

<span data-ttu-id="545b9-578">O SQL da API do DocumentDB fornece os argumentos às UDFs para cada documento na fonte no estágio atual (cláusula WHERE ou cláusula SELECT) de processamento da UDF.</span><span class="sxs-lookup"><span data-stu-id="545b9-578">DocumentDB API SQL provides the arguments to the UDFs for each document in the source at the current stage (WHERE clause or SELECT clause) of processing the UDF.</span></span> <span data-ttu-id="545b9-579">O resultado é incorporado perfeitamente ao pipeline de execução geral.</span><span class="sxs-lookup"><span data-stu-id="545b9-579">The result is incorporated in the overall execution pipeline seamlessly.</span></span> <span data-ttu-id="545b9-580">Se as propriedades referidas aos parâmetros das UDFs não estiverem disponíveis no valor JSON, o parâmetro é considerado indefinido e a invocação das UDFs é totalmente ignorada.</span><span class="sxs-lookup"><span data-stu-id="545b9-580">If the properties referred to by the UDF parameters are not available in the JSON value, the parameter is considered as undefined and hence the UDF invocation is entirely skipped.</span></span> <span data-ttu-id="545b9-581">De maneira semelhante, se o resultado das UDFs for indefinido, ele não será incluído nos resultados.</span><span class="sxs-lookup"><span data-stu-id="545b9-581">Similarly if the result of the UDF is undefined, it's not included in the result.</span></span> 

<span data-ttu-id="545b9-582">Em resumo, as UDFs são ótimas ferramentas para realizar lógicas de negócios complexas como parte da consulta.</span><span class="sxs-lookup"><span data-stu-id="545b9-582">In summary, UDFs are great tools to do complex business logic as part of the query.</span></span>

### <a name="operator-evaluation"></a><span data-ttu-id="545b9-583">Avaliação de operador</span><span class="sxs-lookup"><span data-stu-id="545b9-583">Operator evaluation</span></span>
<span data-ttu-id="545b9-584">O Cosmos DB, em virtude se ser um banco de dados JSON, estabelece um paralelo com operadores JavaScript e sua semântica de avaliação.</span><span class="sxs-lookup"><span data-stu-id="545b9-584">Cosmos DB, by the virtue of being a JSON database, draws parallels with JavaScript operators and its evaluation semantics.</span></span> <span data-ttu-id="545b9-585">Embora o Cosmos DB tente preservar a semântica do JavaScript em termos de suporte ao JSON, a avaliação da operação se desvia em alguns casos.</span><span class="sxs-lookup"><span data-stu-id="545b9-585">While Cosmos DB tries to preserve JavaScript semantics in terms of JSON support, the operation evaluation deviates in some instances.</span></span>

<span data-ttu-id="545b9-586">No SQL da API do DocumentDB, ao contrário do que ocorre no SQL tradicional, é frequente que os tipos de valores não sejam conhecidos até que os valores sejam recuperados do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="545b9-586">In DocumentDB API SQL, unlike in traditional SQL, the types of values are often not known until the values are retrieved from database.</span></span> <span data-ttu-id="545b9-587">Para executar consultas com eficiência, a maioria dos operadores tem requisitos restritos de tipo.</span><span class="sxs-lookup"><span data-stu-id="545b9-587">In order to efficiently execute queries, most of the operators have strict type requirements.</span></span> 

<span data-ttu-id="545b9-588">O SQL da API do DocumentDB não realiza conversões implícitas, diferente do JavaScript.</span><span class="sxs-lookup"><span data-stu-id="545b9-588">DocumentDB API SQL doesn't perform implicit conversions, unlike JavaScript.</span></span> <span data-ttu-id="545b9-589">Por exemplo, uma consulta como `SELECT * FROM Person p WHERE p.Age = 21` corresponde a documentos que contêm a propriedade Age com o valor 21.</span><span class="sxs-lookup"><span data-stu-id="545b9-589">For instance, a query like `SELECT * FROM Person p WHERE p.Age = 21` matches documents that contain an Age property whose value is 21.</span></span> <span data-ttu-id="545b9-590">Qualquer outro documento cuja propriedade Age corresponder a “21” — ou a outras variações potencialmente infinitas como “021”, “21,0”, “0021”, “00021” etc. — não será correspondido.</span><span class="sxs-lookup"><span data-stu-id="545b9-590">Any other document whose Age property matches string "21", or other possibly infinite variations like "021", "21.0", "0021", "00021", etc. will not be matched.</span></span> <span data-ttu-id="545b9-591">Isso ocorre em oposição ao JavaScript, que os valores das cadeias de caracteres são convertidos implicitamente em números (baseado em operador como, por exemplo: ==).</span><span class="sxs-lookup"><span data-stu-id="545b9-591">This is in contrast to the JavaScript where the string values are implicitly casted to numbers (based on operator, ex: ==).</span></span> <span data-ttu-id="545b9-592">Esta escolha é fundamental para uma correspondência eficiente de índices no SQL da API do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="545b9-592">This choice is crucial for efficient index matching in DocumentDB API SQL.</span></span> 

## <a name="parameterized-sql-queries"></a><span data-ttu-id="545b9-593">Consultas SQL parametrizadas</span><span class="sxs-lookup"><span data-stu-id="545b9-593">Parameterized SQL queries</span></span>
<span data-ttu-id="545b9-594">O Cosmos DB dá suporte a consultas com parâmetros expressos com a conhecida notação @.</span><span class="sxs-lookup"><span data-stu-id="545b9-594">Cosmos DB supports queries with parameters expressed with the familiar @ notation.</span></span> <span data-ttu-id="545b9-595">A SQL parametrizada oferece recursos robustos de manuseio e saída das entradas de usuário, evitando a exposição acidental de dados por meio de uma injeção SQL.</span><span class="sxs-lookup"><span data-stu-id="545b9-595">Parameterized SQL provides robust handling and escaping of user input, preventing accidental exposure of data through SQL injection.</span></span> 

<span data-ttu-id="545b9-596">Por exemplo, você pode escrever uma consulta que define o sobrenome e o estado do endereço como parâmetros e executá-la para vários valores de sobrenome e estado de endereço, com base na entrada do usuário.</span><span class="sxs-lookup"><span data-stu-id="545b9-596">For example, you can write a query that takes last name and address state as parameters, and then execute it for various values of last name and address state based on user input.</span></span>

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

<span data-ttu-id="545b9-597">Essa solicitação pode então ser enviada ao Cosmos DB como uma consulta JSON parametrizada, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="545b9-597">This request can then be sent to Cosmos DB as a parameterized JSON query like shown below.</span></span>

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

<span data-ttu-id="545b9-598">O argumento para TOP pode ser definido usando consultas parametrizadas, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="545b9-598">The argument to TOP can be set using parameterized queries like shown below.</span></span>

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

<span data-ttu-id="545b9-599">Os valores dos parâmetros podem ser qualquer JSON válido (cadeias de caracteres, números, boolianos, nulos, ou mesmo matrizes e JSON aninhado).</span><span class="sxs-lookup"><span data-stu-id="545b9-599">Parameter values can be any valid JSON (strings, numbers, Booleans, null, even arrays or nested JSON).</span></span> <span data-ttu-id="545b9-600">Além disso, como o Cosmos DB não tem esquemas, os parâmetros não são validados em relação a nenhum tipo.</span><span class="sxs-lookup"><span data-stu-id="545b9-600">Also since Cosmos DB is schema-less, parameters are not validated against any type.</span></span>

## <span data-ttu-id="545b9-601"><a id="BuiltinFunctions"></a>Funções internas</span><span class="sxs-lookup"><span data-stu-id="545b9-601"><a id="BuiltinFunctions"></a>Built-in functions</span></span>
<span data-ttu-id="545b9-602">O Cosmos DB também dá suporte a várias funções internas para operações comuns, que podem ser usadas em consultas como UDFs (funções definidas pelo usuário).</span><span class="sxs-lookup"><span data-stu-id="545b9-602">Cosmos DB also supports a number of built-in functions for common operations, that can be used inside queries like user-defined functions (UDFs).</span></span>

| <span data-ttu-id="545b9-603">Grupo de funções</span><span class="sxs-lookup"><span data-stu-id="545b9-603">Function group</span></span>          | <span data-ttu-id="545b9-604">Operações</span><span class="sxs-lookup"><span data-stu-id="545b9-604">Operations</span></span>                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="545b9-605">Funções matemáticas</span><span class="sxs-lookup"><span data-stu-id="545b9-605">Mathematical functions</span></span>  | <span data-ttu-id="545b9-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN e TAN</span><span class="sxs-lookup"><span data-stu-id="545b9-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN, and TAN</span></span> |
| <span data-ttu-id="545b9-607">Funções de verificação de tipo</span><span class="sxs-lookup"><span data-stu-id="545b9-607">Type checking functions</span></span> | <span data-ttu-id="545b9-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED e IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="545b9-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED, and IS_PRIMITIVE</span></span>                                                           |
| <span data-ttu-id="545b9-609">Funções de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="545b9-609">String functions</span></span>        | <span data-ttu-id="545b9-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING e UPPER</span><span class="sxs-lookup"><span data-stu-id="545b9-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING, and UPPER</span></span>       |
| <span data-ttu-id="545b9-611">Funções de matriz</span><span class="sxs-lookup"><span data-stu-id="545b9-611">Array functions</span></span>         | <span data-ttu-id="545b9-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH e ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="545b9-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH, and ARRAY_SLICE</span></span>                                                                                         |
| <span data-ttu-id="545b9-613">Funções espaciais</span><span class="sxs-lookup"><span data-stu-id="545b9-613">Spatial functions</span></span>       | <span data-ttu-id="545b9-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID e ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="545b9-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID, and ST_ISVALIDDETAILED</span></span>                                                                           | 

<span data-ttu-id="545b9-615">Se, no momento, você estiver usando uma UDF (função definida pelo usuário) para a qual uma função interna agora está disponível, deverá usar a função interna correspondente, pois sua execução será mais rápida e mais eficiente.</span><span class="sxs-lookup"><span data-stu-id="545b9-615">If you’re currently using a user-defined function (UDF) for which a built-in function is now available, you should use the corresponding built-in function as it is going to be quicker to run and more efficiently.</span></span> 

### <a name="mathematical-functions"></a><span data-ttu-id="545b9-616">Funções matemáticas</span><span class="sxs-lookup"><span data-stu-id="545b9-616">Mathematical functions</span></span>
<span data-ttu-id="545b9-617">As funções matemáticas executam um cálculo, com base em valores de entrada fornecidos como argumentos e retornam um valor numérico.</span><span class="sxs-lookup"><span data-stu-id="545b9-617">The mathematical functions each perform a calculation, based on input values that are provided as arguments, and return a numeric value.</span></span> <span data-ttu-id="545b9-618">Aqui está uma tabela de funções matemáticas internas com suporte.</span><span class="sxs-lookup"><span data-stu-id="545b9-618">Here’s a table of supported built-in mathematical functions.</span></span>


| <span data-ttu-id="545b9-619">Uso</span><span class="sxs-lookup"><span data-stu-id="545b9-619">Usage</span></span> | <span data-ttu-id="545b9-620">Descrição</span><span class="sxs-lookup"><span data-stu-id="545b9-620">Description</span></span> |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="545b9-621">[[ABS (num_expr)](#bk_abs)</span><span class="sxs-lookup"><span data-stu-id="545b9-621">[[ABS (num_expr)](#bk_abs)</span></span> | <span data-ttu-id="545b9-622">Retorna o valor absoluto (positivo) da expressão numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="545b9-622">Returns the absolute (positive) value of the specified numeric expression.</span></span> |
| [<span data-ttu-id="545b9-623">CEILING (num_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-623">CEILING (num_expr)</span></span>](#bk_ceiling) | <span data-ttu-id="545b9-624">Retorna o menor valor de número inteiro maior ou igual à expressão numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="545b9-624">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span> |
| [<span data-ttu-id="545b9-625">FLOOR (num_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-625">FLOOR (num_expr)</span></span>](#bk_floor) | <span data-ttu-id="545b9-626">Retorna o maior inteiro menor ou igual à expressão numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="545b9-626">Returns the largest integer less than or equal to the specified numeric expression.</span></span> |
| [<span data-ttu-id="545b9-627">EXP (num_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-627">EXP (num_expr)</span></span>](#bk_exp) | <span data-ttu-id="545b9-628">Retorna o expoente da expressão numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="545b9-628">Returns the exponent of the specified numeric expression.</span></span> |
| <span data-ttu-id="545b9-629">[LOG (num_expr [,base])](#bk_log)</span><span class="sxs-lookup"><span data-stu-id="545b9-629">[LOG (num_expr [,base])](#bk_log)</span></span> | <span data-ttu-id="545b9-630">Retorna o logaritmo natural da expressão numérica especificada ou o logaritmo usando a base especificada</span><span class="sxs-lookup"><span data-stu-id="545b9-630">Returns the natural logarithm of the specified numeric expression, or the logarithm using the specified base</span></span> |
| [<span data-ttu-id="545b9-631">LOG10 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-631">LOG10 (num_expr)</span></span>](#bk_log10) | <span data-ttu-id="545b9-632">Retorna o valor logarítmico de base 10 da expressão numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="545b9-632">Returns the base-10 logarithmic value of the specified numeric expression.</span></span> |
| [<span data-ttu-id="545b9-633">ROUND (num_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-633">ROUND (num_expr)</span></span>](#bk_round) | <span data-ttu-id="545b9-634">Retorna um valor numérico, arredondado para o valor inteiro mais próximo.</span><span class="sxs-lookup"><span data-stu-id="545b9-634">Returns a numeric value, rounded to the closest integer value.</span></span> |
| [<span data-ttu-id="545b9-635">TRUNC (num_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-635">TRUNC (num_expr)</span></span>](#bk_trunc) | <span data-ttu-id="545b9-636">Retorna um valor numérico, truncado para o valor inteiro mais próximo.</span><span class="sxs-lookup"><span data-stu-id="545b9-636">Returns a numeric value, truncated to the closest integer value.</span></span> |
| [<span data-ttu-id="545b9-637">SQRT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-637">SQRT (num_expr)</span></span>](#bk_sqrt) | <span data-ttu-id="545b9-638">Retorna a raiz quadrada de expressão numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="545b9-638">Returns the square root of the specified numeric expression.</span></span> |
| [<span data-ttu-id="545b9-639">SQUARE (num_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-639">SQUARE (num_expr)</span></span>](#bk_square) | <span data-ttu-id="545b9-640">Retorna o quadrado de expressão numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="545b9-640">Returns the square of the specified numeric expression.</span></span> |
| [<span data-ttu-id="545b9-641">POWER (num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-641">POWER (num_expr, num_expr)</span></span>](#bk_power) | <span data-ttu-id="545b9-642">Retorna a potência da expressão numérica especificada para o valor especificado.</span><span class="sxs-lookup"><span data-stu-id="545b9-642">Returns the power of the specified numeric expression to the value specified.</span></span> |
| [<span data-ttu-id="545b9-643">SIGN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-643">SIGN (num_expr)</span></span>](#bk_sign) | <span data-ttu-id="545b9-644">Retorna o valor de entrada (-1, 0, 1) da expressão numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="545b9-644">Returns the sign value (-1, 0, 1) of the specified numeric expression.</span></span> |
| [<span data-ttu-id="545b9-645">ACOS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-645">ACOS (num_expr)</span></span>](#bk_acos) | <span data-ttu-id="545b9-646">Retorna o ângulo, em radianos, cujo cosseno é a expressão numérica especificada (também chamado de arco cosseno).</span><span class="sxs-lookup"><span data-stu-id="545b9-646">Returns the angle, in radians, whose cosine is the specified numeric expression; also called arccosine.</span></span> |
| [<span data-ttu-id="545b9-647">ASIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-647">ASIN (num_expr)</span></span>](#bk_asin) | <span data-ttu-id="545b9-648">Retorna o ângulo, em radianos, cujo seno é a expressão numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="545b9-648">Returns the angle, in radians, whose sine is the specified numeric expression.</span></span> <span data-ttu-id="545b9-649">Isso também é chamado de arco seno.</span><span class="sxs-lookup"><span data-stu-id="545b9-649">This is also called arcsine.</span></span> |
| [<span data-ttu-id="545b9-650">ATAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-650">ATAN (num_expr)</span></span>](#bk_atan) | <span data-ttu-id="545b9-651">Retorna o ângulo, em radianos, cuja tangente é a expressão numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="545b9-651">Returns the angle, in radians, whose tangent is the specified numeric expression.</span></span> <span data-ttu-id="545b9-652">Isso também é chamado de arco tangente.</span><span class="sxs-lookup"><span data-stu-id="545b9-652">This is also called arctangent.</span></span> |
| [<span data-ttu-id="545b9-653">ATN2 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-653">ATN2 (num_expr)</span></span>](#bk_atn2) | <span data-ttu-id="545b9-654">Retorna o ângulo, em radianos, entre o eixo x positivo e o raio da origem até o ponto (x, y), em que x e y são os valores de duas expressões flutuantes especificadas.</span><span class="sxs-lookup"><span data-stu-id="545b9-654">Returns the angle, in radians, between the positive x-axis and the ray from the origin to the point (y, x), where x and y are the values of the two specified float expressions.</span></span> |
| [<span data-ttu-id="545b9-655">COS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-655">COS (num_expr)</span></span>](#bk_cos) | <span data-ttu-id="545b9-656">Retorna o cosseno trigonométrico do ângulo especificado, em radianos, na expressão especificada.</span><span class="sxs-lookup"><span data-stu-id="545b9-656">Returns the trigonometric cosine of the specified angle, in radians, in the specified expression.</span></span> |
| [<span data-ttu-id="545b9-657">COT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-657">COT (num_expr)</span></span>](#bk_cot) | <span data-ttu-id="545b9-658">Retorna a cotangente trigonométrica do ângulo especificado, em radianos, na expressão numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="545b9-658">Returns the trigonometric cotangent of the specified angle, in radians, in the specified numeric expression.</span></span> |
| [<span data-ttu-id="545b9-659">DEGREES (num_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-659">DEGREES (num_expr)</span></span>](#bk_degrees) | <span data-ttu-id="545b9-660">Retorna o ângulo correspondente, em graus, para um ângulo especificado em radianos.</span><span class="sxs-lookup"><span data-stu-id="545b9-660">Returns the corresponding angle in degrees for an angle specified in radians.</span></span> |
| [<span data-ttu-id="545b9-661">PI ()</span><span class="sxs-lookup"><span data-stu-id="545b9-661">PI ()</span></span>](#bk_pi) | <span data-ttu-id="545b9-662">Retorna o valor constante de PI.</span><span class="sxs-lookup"><span data-stu-id="545b9-662">Returns the constant value of PI.</span></span> |
| [<span data-ttu-id="545b9-663">RADIANS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-663">RADIANS (num_expr)</span></span>](#bk_radians) | <span data-ttu-id="545b9-664">Retorna radianos quando uma expressão numérica é inserida em graus.</span><span class="sxs-lookup"><span data-stu-id="545b9-664">Returns radians when a numeric expression, in degrees, is entered.</span></span> |
| [<span data-ttu-id="545b9-665">SIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-665">SIN (num_expr)</span></span>](#bk_sin) | <span data-ttu-id="545b9-666">Retorna o seno trigonométrico do ângulo especificado, em radianos, na expressão especificada.</span><span class="sxs-lookup"><span data-stu-id="545b9-666">Returns the trigonometric sine of the specified angle, in radians, in the specified expression.</span></span> |
| [<span data-ttu-id="545b9-667">TAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-667">TAN (num_expr)</span></span>](#bk_tan) | <span data-ttu-id="545b9-668">Retorna a tangente da expressão de entrada, na expressão especificada.</span><span class="sxs-lookup"><span data-stu-id="545b9-668">Returns the tangent of the input expression, in the specified expression.</span></span> |

<span data-ttu-id="545b9-669">Por exemplo, agora você pode executar consultas como as seguintes:</span><span class="sxs-lookup"><span data-stu-id="545b9-669">For example, you can now run queries like the following:</span></span>

<span data-ttu-id="545b9-670">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-670">**Query**</span></span>

    SELECT VALUE ABS(-4)

<span data-ttu-id="545b9-671">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-671">**Results**</span></span>

    [4]

<span data-ttu-id="545b9-672">A principal diferença entre as funções do Cosmos DB em comparação com o ANSI SQL é que elas são criadas para funcionar bem com os dados de esquemas mistos e sem esquemas.</span><span class="sxs-lookup"><span data-stu-id="545b9-672">The main difference between Cosmos DB’s functions compared to ANSI SQL is that they are designed to work well with schema-less and mixed schema data.</span></span> <span data-ttu-id="545b9-673">Por exemplo, se você tem um documento em que a propriedade Tamanho está ausente ou tem um valor não numérico, como "desconhecido", o documento é ignorado, em vez de retornar um erro.</span><span class="sxs-lookup"><span data-stu-id="545b9-673">For example, if you have a document where the Size property is missing, or has a non-numeric value like “unknown”, then the document is skipped over, instead of returning an error.</span></span>

### <a name="type-checking-functions"></a><span data-ttu-id="545b9-674">Funções de verificação de tipo</span><span class="sxs-lookup"><span data-stu-id="545b9-674">Type checking functions</span></span>
<span data-ttu-id="545b9-675">As funções de verificação de tipo permitem que você verifique o tipo de uma expressão em consultas SQL.</span><span class="sxs-lookup"><span data-stu-id="545b9-675">The type checking functions allow you to check the type of an expression within SQL queries.</span></span> <span data-ttu-id="545b9-676">As funções de verificação de tipo podem ser usadas para determinar o tipo de propriedades em documentos imediatamente quando ele é desconhecido ou variável.</span><span class="sxs-lookup"><span data-stu-id="545b9-676">Type checking functions can be used to determine the type of properties within documents on the fly when it is variable or unknown.</span></span> <span data-ttu-id="545b9-677">Aqui está uma tabela de funções de verificação de tipo internas com suporte.</span><span class="sxs-lookup"><span data-stu-id="545b9-677">Here’s a table of supported built-in type checking functions.</span></span>

<table>
<tr>
  <td><span data-ttu-id="545b9-678"><strong>Uso</strong></span><span class="sxs-lookup"><span data-stu-id="545b9-678"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="545b9-679"><strong>Descrição</strong></span><span class="sxs-lookup"><span data-stu-id="545b9-679"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="545b9-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span><span class="sxs-lookup"><span data-stu-id="545b9-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span></span></td>
  <td><span data-ttu-id="545b9-681">Retorna um booliano indicando se o tipo do valor é uma matriz.</span><span class="sxs-lookup"><span data-stu-id="545b9-681">Returns a Boolean indicating if the type of the value is an array.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="545b9-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="545b9-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span></span></td>
  <td><span data-ttu-id="545b9-683">Retorna um booliano indicando se o tipo do valor é um booliano.</span><span class="sxs-lookup"><span data-stu-id="545b9-683">Returns a Boolean indicating if the type of the value is a Boolean.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="545b9-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="545b9-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span></span></td>
  <td><span data-ttu-id="545b9-685">Retorna um booliano indicando se o tipo do valor é nulo.</span><span class="sxs-lookup"><span data-stu-id="545b9-685">Returns a Boolean indicating if the type of the value is null.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="545b9-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span><span class="sxs-lookup"><span data-stu-id="545b9-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span></span></td>
  <td><span data-ttu-id="545b9-687">Retorna um booliano indicando se o tipo do valor é um número.</span><span class="sxs-lookup"><span data-stu-id="545b9-687">Returns a Boolean indicating if the type of the value is a number.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="545b9-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span><span class="sxs-lookup"><span data-stu-id="545b9-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span></span></td>
  <td><span data-ttu-id="545b9-689">Retorna um booliano indicando se o tipo do valor é um objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="545b9-689">Returns a Boolean indicating if the type of the value is a JSON object.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="545b9-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span><span class="sxs-lookup"><span data-stu-id="545b9-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span></span></td>
  <td><span data-ttu-id="545b9-691">Retorna um booliano indicando se o tipo do valor é uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="545b9-691">Returns a Boolean indicating if the type of the value is a string.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="545b9-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span><span class="sxs-lookup"><span data-stu-id="545b9-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span></span></td>
  <td><span data-ttu-id="545b9-693">Retorna um valor booliano que indica se um valor foi atribuído à propriedade.</span><span class="sxs-lookup"><span data-stu-id="545b9-693">Returns a Boolean indicating if the property has been assigned a value.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="545b9-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span><span class="sxs-lookup"><span data-stu-id="545b9-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span></span></td>
  <td><span data-ttu-id="545b9-695">Retorna um valor booliano indicando se o tipo do valor é uma cadeia de caracteres, número, booliano ou nulo.</span><span class="sxs-lookup"><span data-stu-id="545b9-695">Returns a Boolean indicating if the type of the value is a string, number, Boolean or null.</span></span></td>
</tr>

</table>

<span data-ttu-id="545b9-696">Usando essas funções, agora você pode executar consultas como as seguintes:</span><span class="sxs-lookup"><span data-stu-id="545b9-696">Using these functions, you can now run queries like the following:</span></span>

<span data-ttu-id="545b9-697">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-697">**Query**</span></span>

    SELECT VALUE IS_NUMBER(-4)

<span data-ttu-id="545b9-698">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-698">**Results**</span></span>

    [true]

### <a name="string-functions"></a><span data-ttu-id="545b9-699">Funções de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="545b9-699">String functions</span></span>
<span data-ttu-id="545b9-700">As funções escalares a seguir executam uma operação em um valor de cadeia de caracteres de entrada e retornam uma cadeia de caracteres, um valor numérico ou um valor booliano.</span><span class="sxs-lookup"><span data-stu-id="545b9-700">The following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span> <span data-ttu-id="545b9-701">Aqui temos uma tabela de funções de cadeia de caracteres internas:</span><span class="sxs-lookup"><span data-stu-id="545b9-701">Here's a table of built-in string functions:</span></span>

| <span data-ttu-id="545b9-702">Uso</span><span class="sxs-lookup"><span data-stu-id="545b9-702">Usage</span></span> | <span data-ttu-id="545b9-703">Descrição</span><span class="sxs-lookup"><span data-stu-id="545b9-703">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="545b9-704">LENGTH (str_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-704">LENGTH (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |<span data-ttu-id="545b9-705">Retorna o número de caracteres da expressão de cadeia de caracteres especificada</span><span class="sxs-lookup"><span data-stu-id="545b9-705">Returns the number of characters of the specified string expression</span></span> |
| <span data-ttu-id="545b9-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span><span class="sxs-lookup"><span data-stu-id="545b9-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span></span> |<span data-ttu-id="545b9-707">Retorna uma cadeia de caracteres que é o resultado da concatenação de dois ou mais valores de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="545b9-707">Returns a string that is the result of concatenating two or more string values.</span></span> |
| [<span data-ttu-id="545b9-708">SUBSTRING (str_expr, num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-708">SUBSTRING (str_expr, num_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |<span data-ttu-id="545b9-709">Retorna parte de uma expressão de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="545b9-709">Returns part of a string expression.</span></span> |
| [<span data-ttu-id="545b9-710">STARTSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-710">STARTSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |<span data-ttu-id="545b9-711">Retorna um valor booliano que indica se a primeira expressão de cadeia de caracteres termina com a segunda</span><span class="sxs-lookup"><span data-stu-id="545b9-711">Returns a Boolean indicating whether the first string expression ends with the second</span></span> |
| [<span data-ttu-id="545b9-712">ENDSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-712">ENDSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |<span data-ttu-id="545b9-713">Retorna um valor booliano que indica se a primeira expressão de cadeia de caracteres termina com a segunda</span><span class="sxs-lookup"><span data-stu-id="545b9-713">Returns a Boolean indicating whether the first string expression ends with the second</span></span> |
| [<span data-ttu-id="545b9-714">CONTAINS (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-714">CONTAINS (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |<span data-ttu-id="545b9-715">Retorna um valor booliano que indica se a primeira expressão de cadeia de caracteres contém a segunda.</span><span class="sxs-lookup"><span data-stu-id="545b9-715">Returns a Boolean indicating whether the first string expression contains the second.</span></span> |
| [<span data-ttu-id="545b9-716">INDEX_OF (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-716">INDEX_OF (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |<span data-ttu-id="545b9-717">Retorna a posição inicial da primeira ocorrência da segunda expressão de cadeia de caracteres dentro da primeira expressão de cadeia de caracteres especificada, ou -1 se a cadeia de caracteres não for encontrada.</span><span class="sxs-lookup"><span data-stu-id="545b9-717">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span> |
| [<span data-ttu-id="545b9-718">LEFT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-718">LEFT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |<span data-ttu-id="545b9-719">Retorna a parte esquerda de uma cadeia de caracteres com o número especificado de caracteres.</span><span class="sxs-lookup"><span data-stu-id="545b9-719">Returns the left part of a string with the specified number of characters.</span></span> |
| [<span data-ttu-id="545b9-720">RIGHT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-720">RIGHT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |<span data-ttu-id="545b9-721">Retorna a parte direita de uma cadeia de caracteres com o número especificado de caracteres.</span><span class="sxs-lookup"><span data-stu-id="545b9-721">Returns the right part of a string with the specified number of characters.</span></span> |
| [<span data-ttu-id="545b9-722">LTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-722">LTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |<span data-ttu-id="545b9-723">Retorna uma expressão de cadeia de caracteres após remover os espaços em branco iniciais.</span><span class="sxs-lookup"><span data-stu-id="545b9-723">Returns a string expression after it removes leading blanks.</span></span> |
| [<span data-ttu-id="545b9-724">RTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-724">RTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |<span data-ttu-id="545b9-725">Retorna uma expressão de cadeia de caracteres após truncar todos os espaços em branco finais.</span><span class="sxs-lookup"><span data-stu-id="545b9-725">Returns a string expression after truncating all trailing blanks.</span></span> |
| [<span data-ttu-id="545b9-726">LOWER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-726">LOWER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |<span data-ttu-id="545b9-727">Retorna uma expressão de cadeia de caracteres depois de converter dados de caracteres maiúsculos em minúsculos.</span><span class="sxs-lookup"><span data-stu-id="545b9-727">Returns a string expression after converting uppercase character data to lowercase.</span></span> |
| [<span data-ttu-id="545b9-728">UPPER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-728">UPPER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |<span data-ttu-id="545b9-729">Retorna uma expressão de cadeia de caracteres depois de converter dados de caracteres minúsculos em maiúsculos.</span><span class="sxs-lookup"><span data-stu-id="545b9-729">Returns a string expression after converting lowercase character data to uppercase.</span></span> |
| [<span data-ttu-id="545b9-730">REPLACE (str_expr, str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-730">REPLACE (str_expr, str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |<span data-ttu-id="545b9-731">Substitui todas as ocorrências de um valor de cadeia de caracteres especificado por outro valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="545b9-731">Replaces all occurrences of a specified string value with another string value.</span></span> |
| [<span data-ttu-id="545b9-732">REPLICATE (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-732">REPLICATE (str_expr, num_expr)</span></span>](https://docs.microsoft.com/azure/cosmos-db/documentdb-sql-query-reference#bk_replicate) |<span data-ttu-id="545b9-733">Repete um valor de cadeia de caracteres por um número de vezes especificado.</span><span class="sxs-lookup"><span data-stu-id="545b9-733">Repeats a string value a specified number of times.</span></span> |
| [<span data-ttu-id="545b9-734">REVERSE (str_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-734">REVERSE (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |<span data-ttu-id="545b9-735">Retorna a ordem inversa de um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="545b9-735">Returns the reverse order of a string value.</span></span> |

<span data-ttu-id="545b9-736">Usando essas funções, agora você pode executar consultas como as descritas a seguir.</span><span class="sxs-lookup"><span data-stu-id="545b9-736">Using these functions, you can now run queries like the following.</span></span> <span data-ttu-id="545b9-737">Por exemplo, você pode retornar o sobrenome em caracteres maiúsculos, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="545b9-737">For example, you can return the family name in uppercase as follows:</span></span>

<span data-ttu-id="545b9-738">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-738">**Query**</span></span>

    SELECT VALUE UPPER(Families.id)
    FROM Families

<span data-ttu-id="545b9-739">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-739">**Results**</span></span>

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

<span data-ttu-id="545b9-740">Ou concatenar cadeias de caracteres, como neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="545b9-740">Or concatenate strings like in this example:</span></span>

<span data-ttu-id="545b9-741">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-741">**Query**</span></span>

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

<span data-ttu-id="545b9-742">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-742">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


<span data-ttu-id="545b9-743">Funções de cadeia de caracteres também podem ser usadas na cláusula WHERE para filtrar os resultados, como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="545b9-743">String functions can also be used in the WHERE clause to filter results, like in the following example:</span></span>

<span data-ttu-id="545b9-744">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-744">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

<span data-ttu-id="545b9-745">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-745">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a><span data-ttu-id="545b9-746">Funções de matriz</span><span class="sxs-lookup"><span data-stu-id="545b9-746">Array functions</span></span>
<span data-ttu-id="545b9-747">As funções escalares a seguir executam uma operação em um valor de matriz de entrada e retornam um valor numérico, booliano ou um valor de matriz.</span><span class="sxs-lookup"><span data-stu-id="545b9-747">The following scalar functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span> <span data-ttu-id="545b9-748">Aqui temos uma tabela de funções de matriz internas:</span><span class="sxs-lookup"><span data-stu-id="545b9-748">Here's a table of built-in array functions:</span></span>

| <span data-ttu-id="545b9-749">Uso</span><span class="sxs-lookup"><span data-stu-id="545b9-749">Usage</span></span> | <span data-ttu-id="545b9-750">Descrição</span><span class="sxs-lookup"><span data-stu-id="545b9-750">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="545b9-751">ARRAY_LENGTH (arr_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-751">ARRAY_LENGTH (arr_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |<span data-ttu-id="545b9-752">Retorna o número de elementos da expressão de matriz especificada.</span><span class="sxs-lookup"><span data-stu-id="545b9-752">Returns the number of elements of the specified array expression.</span></span> |
| <span data-ttu-id="545b9-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span><span class="sxs-lookup"><span data-stu-id="545b9-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span></span> |<span data-ttu-id="545b9-754">Retorna uma matriz que é o resultado da concatenação de dois ou mais valores de matriz.</span><span class="sxs-lookup"><span data-stu-id="545b9-754">Returns an array that is the result of concatenating two or more array values.</span></span> |
| <span data-ttu-id="545b9-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span><span class="sxs-lookup"><span data-stu-id="545b9-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span></span> |<span data-ttu-id="545b9-756">Retorna um valor booliano que indica se a matriz contém o valor especificado.</span><span class="sxs-lookup"><span data-stu-id="545b9-756">Returns a Boolean indicating whether the array contains the specified value.</span></span> <span data-ttu-id="545b9-757">Pode especificar se a correspondência é completa ou parcial.</span><span class="sxs-lookup"><span data-stu-id="545b9-757">Can specify if the match is full or partial.</span></span> |
| <span data-ttu-id="545b9-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span><span class="sxs-lookup"><span data-stu-id="545b9-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span></span> |<span data-ttu-id="545b9-759">Retorna parte de uma expressão de matriz.</span><span class="sxs-lookup"><span data-stu-id="545b9-759">Returns part of an array expression.</span></span> |

<span data-ttu-id="545b9-760">Funções de matriz podem ser usadas para manipular matrizes contidas no JSON.</span><span class="sxs-lookup"><span data-stu-id="545b9-760">Array functions can be used to manipulate arrays within JSON.</span></span> <span data-ttu-id="545b9-761">Por exemplo, aqui está uma consulta que retorna todos os documentos nos quais um dos pais é "Robin Wakefield".</span><span class="sxs-lookup"><span data-stu-id="545b9-761">For example, here's a query that returns all documents where one of the parents is "Robin Wakefield".</span></span> 

<span data-ttu-id="545b9-762">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-762">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

<span data-ttu-id="545b9-763">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-763">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="545b9-764">Você pode especificar um fragmento parcial para elementos correspondentes dentro da matriz.</span><span class="sxs-lookup"><span data-stu-id="545b9-764">You can specify a partial fragment for matching elements within the array.</span></span> <span data-ttu-id="545b9-765">A consulta a seguir localiza todos os pais com o `givenName` de `Robin`.</span><span class="sxs-lookup"><span data-stu-id="545b9-765">The following query finds all parents with the `givenName` of `Robin`.</span></span>

<span data-ttu-id="545b9-766">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-766">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)

<span data-ttu-id="545b9-767">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-767">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]


<span data-ttu-id="545b9-768">Aqui está outro exemplo que usa ARRAY_LENGTH para obter o número de filhos por família.</span><span class="sxs-lookup"><span data-stu-id="545b9-768">Here's another example that uses ARRAY_LENGTH to get the number of children per family.</span></span>

<span data-ttu-id="545b9-769">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-769">**Query**</span></span>

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

<span data-ttu-id="545b9-770">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-770">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a><span data-ttu-id="545b9-771">Funções espaciais</span><span class="sxs-lookup"><span data-stu-id="545b9-771">Spatial functions</span></span>
<span data-ttu-id="545b9-772">O Cosmos DB dá suporte às funções internas do OGC (Open Geospatial Consortium) a seguir em consultas geoespaciais.</span><span class="sxs-lookup"><span data-stu-id="545b9-772">Cosmos DB supports the following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> 

<table>
<tr>
  <td><span data-ttu-id="545b9-773"><strong>Uso</strong></span><span class="sxs-lookup"><span data-stu-id="545b9-773"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="545b9-774"><strong>Descrição</strong></span><span class="sxs-lookup"><span data-stu-id="545b9-774"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="545b9-775">ST_DISTANCE (point_expr, point_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-775">ST_DISTANCE (point_expr, point_expr)</span></span></td>
  <td><span data-ttu-id="545b9-776">Retorna a distância entre as duas expressões de ponto GeoJSON, Polígono ou LineString.</span><span class="sxs-lookup"><span data-stu-id="545b9-776">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="545b9-777">ST_WITHIN (point_expr, polygon_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-777">ST_WITHIN (point_expr, polygon_expr)</span></span></td>
  <td><span data-ttu-id="545b9-778">Retorna uma expressão booliana que indica se o primeiro objeto GeoJSON (Ponto, Polígono ou LineString) está em um segundo objeto GeoJSON (Ponto, Polígono ou LineString).</span><span class="sxs-lookup"><span data-stu-id="545b9-778">Returns a Boolean expression indicating whether the first GeoJSON object (Point, Polygon, or LineString) is within the second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="545b9-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="545b9-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="545b9-780">Retorna uma expressão booliana que indica se os dois objetos GeoJSON especificados (Ponto, Polígono ou LineString) se cruzam.</span><span class="sxs-lookup"><span data-stu-id="545b9-780">Returns a Boolean expression indicating whether the two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="545b9-781">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="545b9-781">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="545b9-782">Retorna um valor Booliano que indica se a expressão especificada de Ponto, Polígono ou LineString GeoJSON é válida.</span><span class="sxs-lookup"><span data-stu-id="545b9-782">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="545b9-783">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="545b9-783">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="545b9-784">Retorna um valor JSON que contém um valor Booliano caso a expressão especificada de Ponto, Polígono ou LineString GeoJSON é válida e, se for inválida, adicionalmente o motivo como um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="545b9-784">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="545b9-785">As funções espaciais podem ser usadas para executar consultas de proximidade em consultas espaciais.</span><span class="sxs-lookup"><span data-stu-id="545b9-785">Spatial functions can be used to perform proximity queries against spatial data.</span></span> <span data-ttu-id="545b9-786">Por exemplo, veja uma consulta que retorna todos os documentos de família que estejam em um raio de 30 km do local especificado usando a função interna ST_DISTANCE.</span><span class="sxs-lookup"><span data-stu-id="545b9-786">For example, here's a query that returns all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="545b9-787">**Consulta**</span><span class="sxs-lookup"><span data-stu-id="545b9-787">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="545b9-788">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-788">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="545b9-789">Para obter detalhes sobre o suporte geoespacial no Cosmos DB, consulte [Trabalhando com os dados geoespaciais no Azure Cosmos DB](geospatial.md).</span><span class="sxs-lookup"><span data-stu-id="545b9-789">For more details on geospatial support in Cosmos DB, please see [Working with geospatial data in Azure Cosmos DB](geospatial.md).</span></span> <span data-ttu-id="545b9-790">Com isso, encerramos as funções espaciais e a sintaxe SQL do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="545b9-790">That wraps up spatial functions, and the SQL syntax for Cosmos DB.</span></span> <span data-ttu-id="545b9-791">Agora vamos dar uma olhada em como o sistema de consultas LINQ funciona e como ele interage com a sintaxe que vimos até agora.</span><span class="sxs-lookup"><span data-stu-id="545b9-791">Now let's take a look at how LINQ querying works and how it interacts with the syntax we've seen so far.</span></span>

## <span data-ttu-id="545b9-792"><a id="Linq"></a>LINQ para SQL da API do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="545b9-792"><a id="Linq"></a>LINQ to DocumentDB API SQL</span></span>
<span data-ttu-id="545b9-793">O LINQ é um modelo de programação .NET que expressa a computação como consultas em fluxos de objetos.</span><span class="sxs-lookup"><span data-stu-id="545b9-793">LINQ is a .NET programming model that expresses computation as queries on streams of objects.</span></span> <span data-ttu-id="545b9-794">O Cosmos DB oferece uma biblioteca do lado do cliente para fazer interface com o LINQ ao facilitar a conversão entre objetos JSON e .NET e um mapeamento por meio de um subconjunto de consultas LINQ para consultas do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="545b9-794">Cosmos DB provides a client-side library to interface with LINQ by facilitating a conversion between JSON and .NET objects and a mapping from a subset of LINQ queries to Cosmos DB queries.</span></span> 

<span data-ttu-id="545b9-795">A imagem abaixo mostra a arquitetura do suporte a consultas LINQ usando o Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="545b9-795">The picture below shows the architecture of supporting LINQ queries using Cosmos DB.</span></span>  <span data-ttu-id="545b9-796">Usando o cliente do Cosmos DB, os desenvolvedores podem criar um objeto **IQueryable** que consulta diretamente o provedor de consultas do Cosmos DB que, por sua vez, converte a consulta LINQ em uma consulta do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="545b9-796">Using the Cosmos DB client, developers can create an **IQueryable** object that directly queries the Cosmos DB query provider, which then translates the LINQ query into a Cosmos DB query.</span></span> <span data-ttu-id="545b9-797">A consulta é, então, passada ao servidor do Cosmos DB para recuperar um conjunto de resultados no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="545b9-797">The query is then passed to the Cosmos DB server to retrieve a set of results in JSON format.</span></span> <span data-ttu-id="545b9-798">Os resultados retornados são desserializados em um fluxo de objetos .NET no lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="545b9-798">The returned results are deserialized into a stream of .NET objects on the client side.</span></span>

![Arquitetura de suporte a consultas LINQ usando a API do DocumentDB – sintaxe SQL, linguagem de consulta JSON, conceitos de banco de dados e consultas SQL][1]

### <a name="net-and-json-mapping"></a><span data-ttu-id="545b9-800">Mapeamento de .NET e JSON</span><span class="sxs-lookup"><span data-stu-id="545b9-800">.NET and JSON mapping</span></span>
<span data-ttu-id="545b9-801">O mapeamento entre objetos .NET e documentos JSON é natural - cada campo de membro de dados é mapeado para um objeto JSON, em que o nome do campo é mapeado para a parte “chave” do objeto e a parte do “valor” é mapeada recursivamente para a parte de valor do objeto.</span><span class="sxs-lookup"><span data-stu-id="545b9-801">The mapping between .NET objects and JSON documents is natural - each data member field is mapped to a JSON object, where the field name is mapped to the "key" part of the object and the "value" part is recursively mapped to the value part of the object.</span></span> <span data-ttu-id="545b9-802">Considere o seguinte exemplo: o objeto Família criado é mapeado para o documento JSON conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="545b9-802">Consider the following example: The Family object created is mapped to the JSON document as shown below.</span></span> <span data-ttu-id="545b9-803">E vice-versa, o documento JSON é mapeado para um objeto .NET.</span><span class="sxs-lookup"><span data-stu-id="545b9-803">And vice versa, the JSON document is mapped back to a .NET object.</span></span>

<span data-ttu-id="545b9-804">**Classe C#**</span><span class="sxs-lookup"><span data-stu-id="545b9-804">**C# Class**</span></span>

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


<span data-ttu-id="545b9-805">**JSON**</span><span class="sxs-lookup"><span data-stu-id="545b9-805">**JSON**</span></span>  

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



### <a name="linq-to-sql-translation"></a><span data-ttu-id="545b9-806">Tradução de LINQ em SQL</span><span class="sxs-lookup"><span data-stu-id="545b9-806">LINQ to SQL translation</span></span>
<span data-ttu-id="545b9-807">O provedor de consultas do Cosmos DB realiza um mapeamento de melhor esforço de uma consulta LINQ para uma consulta SQL do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="545b9-807">The Cosmos DB query provider performs a best effort mapping from a LINQ query into a Cosmos DB SQL query.</span></span> <span data-ttu-id="545b9-808">Na descrição a seguir, presumimos uma familiaridade básica do leitor com o LINQ.</span><span class="sxs-lookup"><span data-stu-id="545b9-808">In the following description, we assume the reader has a basic familiarity of LINQ.</span></span>

<span data-ttu-id="545b9-809">Primeiro, para o sistema de tipos, oferecemos suporte para todos os tipos de JSON primitivos - tipos numéricos, boolianos, cadeia de caracteres e nulo.</span><span class="sxs-lookup"><span data-stu-id="545b9-809">First, for the type system, we support all JSON primitive types – numeric types, boolean, string, and null.</span></span> <span data-ttu-id="545b9-810">Somente esses tipos de JSON têm suporte.</span><span class="sxs-lookup"><span data-stu-id="545b9-810">Only these JSON types are supported.</span></span> <span data-ttu-id="545b9-811">As expressões escalares são suportadas.</span><span class="sxs-lookup"><span data-stu-id="545b9-811">The following scalar expressions are supported.</span></span>

* <span data-ttu-id="545b9-812">Valores constantes – incluem valores constantes dos tipos de dados primitivos no momento em que a consulta é avaliada.</span><span class="sxs-lookup"><span data-stu-id="545b9-812">Constant values – these include constant values of the primitive data types at the time the query is evaluated.</span></span>
* <span data-ttu-id="545b9-813">Expressões de índice de propriedade/matriz – essas expressões se referem à propriedade de um objeto ou um elemento de matriz.</span><span class="sxs-lookup"><span data-stu-id="545b9-813">Property/array index expressions – these expressions refer to the property of an object or an array element.</span></span>
  
     <span data-ttu-id="545b9-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n é uma variável int</span><span class="sxs-lookup"><span data-stu-id="545b9-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n is an int variable</span></span>
* <span data-ttu-id="545b9-815">Expressões aritméticas - Incluem expressões aritméticas comuns em valores numéricos e boolianos.</span><span class="sxs-lookup"><span data-stu-id="545b9-815">Arithmetic expressions - These include common arithmetic expressions on numerical and boolean values.</span></span> <span data-ttu-id="545b9-816">Para obter uma lista completa, consulte a especificação da SQL.</span><span class="sxs-lookup"><span data-stu-id="545b9-816">For the complete list, refer to the SQL specification.</span></span>
  
     <span data-ttu-id="545b9-817">2 * family.children[0].grade;    x + y;</span><span class="sxs-lookup"><span data-stu-id="545b9-817">2 * family.children[0].grade;    x + y;</span></span>
* <span data-ttu-id="545b9-818">Expressão de comparação de cadeias de caracteres - incluem a comparação de um valor de cadeia de caracteres a um valor constante de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="545b9-818">String comparison expression - these include comparing a string value to some constant string value.</span></span>  
  
     <span data-ttu-id="545b9-819">mother.familyName == "Smith";    child.givenName == s; //s é uma variável de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="545b9-819">mother.familyName == "Smith";    child.givenName == s; //s is a string variable</span></span>
* <span data-ttu-id="545b9-820">Expressão de criação de objeto/matriz - estas expressões retornam um objeto do tipo de valor composto ou tipo anônimo ou uma matriz desses objetos.</span><span class="sxs-lookup"><span data-stu-id="545b9-820">Object/array creation expression - these expressions return an object of compound value type or anonymous type or an array of such objects.</span></span> <span data-ttu-id="545b9-821">Esses valores podem ser aninhados.</span><span class="sxs-lookup"><span data-stu-id="545b9-821">These values can be nested.</span></span>
  
     <span data-ttu-id="545b9-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //um tipo anônimo com dois campos</span><span class="sxs-lookup"><span data-stu-id="545b9-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //an anonymous type with two fields</span></span>              
     <span data-ttu-id="545b9-823">novo int[] { 3, child.grade, 5 };</span><span class="sxs-lookup"><span data-stu-id="545b9-823">new int[] { 3, child.grade, 5 };</span></span>

### <span data-ttu-id="545b9-824"><a id="SupportedLinqOperators"></a>Lista de operadores LINQ com suporte</span><span class="sxs-lookup"><span data-stu-id="545b9-824"><a id="SupportedLinqOperators"></a>List of supported LINQ operators</span></span>
<span data-ttu-id="545b9-825">Aqui está uma lista de operadores LINQ com suporte no provedor LINQ incluídos no SDK do .NET do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="545b9-825">Here is a list of supported LINQ operators in the LINQ provider included with the DocumentDB .NET SDK.</span></span>

* <span data-ttu-id="545b9-826">**Select**: as projeções são convertidas para SQL SELECT, incluindo a construção de objetos</span><span class="sxs-lookup"><span data-stu-id="545b9-826">**Select**: Projections translate to the SQL SELECT including object construction</span></span>
* <span data-ttu-id="545b9-827">**Em que**: os filtros são convertidos para SQL WHERE e dão suporte à conversão entre && , || e !</span><span class="sxs-lookup"><span data-stu-id="545b9-827">**Where**: Filters translate to the SQL WHERE, and support translation between && , || and !</span></span> <span data-ttu-id="545b9-828">para os operadores SQL</span><span class="sxs-lookup"><span data-stu-id="545b9-828">to the SQL operators</span></span>
* <span data-ttu-id="545b9-829">**SelectMany**: permite o desenrolamento de matrizes à cláusula SQL JOIN.</span><span class="sxs-lookup"><span data-stu-id="545b9-829">**SelectMany**: Allows unwinding of arrays to the SQL JOIN clause.</span></span> <span data-ttu-id="545b9-830">Pode ser usado para encadear/aninhar expressões para filtrar elementos de matriz</span><span class="sxs-lookup"><span data-stu-id="545b9-830">Can be used to chain/nest expressions to filter on array elements</span></span>
* <span data-ttu-id="545b9-831">**OrderBy e OrderByDescending**: são convertidas em ORDER BY de forma crescente/decrescente</span><span class="sxs-lookup"><span data-stu-id="545b9-831">**OrderBy and OrderByDescending**: Translates to ORDER BY ascending/descending</span></span>
* <span data-ttu-id="545b9-832">Operadores **Count**, **Sum**, **Min**, **Max** e **Average** para agregação e os seus equivalentes assíncronos, **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync** e **AverageAsync**.</span><span class="sxs-lookup"><span data-stu-id="545b9-832">**Count**, **Sum**, **Min**, **Max**, and **Average** operators for aggregation, and their async equivalents **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, and **AverageAsync**.</span></span>
* <span data-ttu-id="545b9-833">**CompareTo**: é convertido em comparações de intervalo.</span><span class="sxs-lookup"><span data-stu-id="545b9-833">**CompareTo**: Translates to range comparisons.</span></span> <span data-ttu-id="545b9-834">Normalmente usados para cadeias de caracteres, já que não são comparáveis no .NET</span><span class="sxs-lookup"><span data-stu-id="545b9-834">Commonly used for strings since they’re not comparable in .NET</span></span>
* <span data-ttu-id="545b9-835">**Take**: é convertido em SQL TOP para limitar os resultados de uma consulta</span><span class="sxs-lookup"><span data-stu-id="545b9-835">**Take**: Translates to the SQL TOP for limiting results from a query</span></span>
* <span data-ttu-id="545b9-836">**Funções matemáticas**: dão suporte à conversão de Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan e Truncate do .NET nas funções internas do SQL equivalentes.</span><span class="sxs-lookup"><span data-stu-id="545b9-836">**Math Functions**: Supports translation from .NET’s Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="545b9-837">**Funções de cadeia de caracteres**: dão suporte à conversão de Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString e ToUpper do .NET nas funções internas do SQL equivalentes.</span><span class="sxs-lookup"><span data-stu-id="545b9-837">**String Functions**: Supports translation from .NET’s Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="545b9-838">**Funções de matriz**: dão suporte à conversão de Concat, Contains e Count do .NET nas funções internas do SQL equivalentes.</span><span class="sxs-lookup"><span data-stu-id="545b9-838">**Array Functions**: Supports translation from .NET’s Concat, Contains, and Count to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="545b9-839">**Funções de extensão geoespacial**: dão suporte à conversão dos métodos stub Distance, Within, IsValid e IsValidDetailed nas funções internas do SQL equivalentes.</span><span class="sxs-lookup"><span data-stu-id="545b9-839">**Geospatial Extension Functions**: Supports translation from stub methods Distance, Within, IsValid, and IsValidDetailed to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="545b9-840">**Função de Extensão da Função Definida pelo Usuário**: dá suporte à translação do método stub UserDefinedFunctionProvider.Invoke na função definida pelo usuário correspondente.</span><span class="sxs-lookup"><span data-stu-id="545b9-840">**User-Defined Function Extension Function**: Supports translation from the stub method UserDefinedFunctionProvider.Invoke to the corresponding user-defined function.</span></span>
* <span data-ttu-id="545b9-841">**Diversos**: dá suporte à conversão dos operadores de união e condicional.</span><span class="sxs-lookup"><span data-stu-id="545b9-841">**Miscellaneous**: Supports translation of the coalesce and conditional operators.</span></span> <span data-ttu-id="545b9-842">Pode converter Contains para a Cadeia de caracteres CONTAINS, ARRAY_CONTAINS ou para o SQL IN, dependendo do contexto.</span><span class="sxs-lookup"><span data-stu-id="545b9-842">Can translate Contains to String CONTAINS, ARRAY_CONTAINS, or the SQL IN depending on context.</span></span>

### <a name="sql-query-operators"></a><span data-ttu-id="545b9-843">Operadores de consulta SQL</span><span class="sxs-lookup"><span data-stu-id="545b9-843">SQL query operators</span></span>
<span data-ttu-id="545b9-844">Aqui, temos alguns exemplos que ilustram como alguns dos operadores de consulta LINQ padrão são convertidos em consultas do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="545b9-844">Here are some examples that illustrate how some of the standard LINQ query operators are translated down to Cosmos DB queries.</span></span>

#### <a name="select-operator"></a><span data-ttu-id="545b9-845">Operador Select</span><span class="sxs-lookup"><span data-stu-id="545b9-845">Select Operator</span></span>
<span data-ttu-id="545b9-846">A sintaxe é `input.Select(x => f(x))`, em que `f` é uma expressão escalar.</span><span class="sxs-lookup"><span data-stu-id="545b9-846">The syntax is `input.Select(x => f(x))`, where `f` is a scalar expression.</span></span>

<span data-ttu-id="545b9-847">**Expressão lambda do LINQ**</span><span class="sxs-lookup"><span data-stu-id="545b9-847">**LINQ lambda expression**</span></span>

    input.Select(family => family.parents[0].familyName);

<span data-ttu-id="545b9-848">**SQL**</span><span class="sxs-lookup"><span data-stu-id="545b9-848">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



<span data-ttu-id="545b9-849">**Expressão lambda do LINQ**</span><span class="sxs-lookup"><span data-stu-id="545b9-849">**LINQ lambda expression**</span></span>

    input.Select(family => family.children[0].grade + c); // c is an int variable


<span data-ttu-id="545b9-850">**SQL**</span><span class="sxs-lookup"><span data-stu-id="545b9-850">**SQL**</span></span> 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



<span data-ttu-id="545b9-851">**Expressão lambda do LINQ**</span><span class="sxs-lookup"><span data-stu-id="545b9-851">**LINQ lambda expression**</span></span>

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


<span data-ttu-id="545b9-852">**SQL**</span><span class="sxs-lookup"><span data-stu-id="545b9-852">**SQL**</span></span> 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a><span data-ttu-id="545b9-853">Operador SelectMany</span><span class="sxs-lookup"><span data-stu-id="545b9-853">SelectMany operator</span></span>
<span data-ttu-id="545b9-854">A sintaxe é `input.SelectMany(x => f(x))`, em que `f` é uma expressão escalar que retorna um tipo de coleção.</span><span class="sxs-lookup"><span data-stu-id="545b9-854">The syntax is `input.SelectMany(x => f(x))`, where `f` is a scalar expression that returns a collection type.</span></span>

<span data-ttu-id="545b9-855">**Expressão lambda do LINQ**</span><span class="sxs-lookup"><span data-stu-id="545b9-855">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children);

<span data-ttu-id="545b9-856">**SQL**</span><span class="sxs-lookup"><span data-stu-id="545b9-856">**SQL**</span></span> 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a><span data-ttu-id="545b9-857">Operador Where</span><span class="sxs-lookup"><span data-stu-id="545b9-857">Where operator</span></span>
<span data-ttu-id="545b9-858">A sintaxe é `input.Where(x => f(x))`, em que `f` é uma expressão escalar que retorna um valor booliano.</span><span class="sxs-lookup"><span data-stu-id="545b9-858">The syntax is `input.Where(x => f(x))`, where `f` is a scalar expression, which returns a Boolean value.</span></span>

<span data-ttu-id="545b9-859">**Expressão lambda do LINQ**</span><span class="sxs-lookup"><span data-stu-id="545b9-859">**LINQ lambda expression**</span></span>

    input.Where(family=> family.parents[0].familyName == "Smith");

<span data-ttu-id="545b9-860">**SQL**</span><span class="sxs-lookup"><span data-stu-id="545b9-860">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



<span data-ttu-id="545b9-861">**Expressão lambda do LINQ**</span><span class="sxs-lookup"><span data-stu-id="545b9-861">**LINQ lambda expression**</span></span>

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

<span data-ttu-id="545b9-862">**SQL**</span><span class="sxs-lookup"><span data-stu-id="545b9-862">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a><span data-ttu-id="545b9-863">Consultas SQL composta</span><span class="sxs-lookup"><span data-stu-id="545b9-863">Composite SQL queries</span></span>
<span data-ttu-id="545b9-864">Os operadores acima podem ser compostos para formar consultas mais poderosas.</span><span class="sxs-lookup"><span data-stu-id="545b9-864">The above operators can be composed to form more powerful queries.</span></span> <span data-ttu-id="545b9-865">Como o Cosmos DB dá suporte a coleções aninhadas, a composição pode ser concatenada ou aninhada.</span><span class="sxs-lookup"><span data-stu-id="545b9-865">Since Cosmos DB supports nested collections, the composition can either be concatenated or nested.</span></span>

#### <a name="concatenation"></a><span data-ttu-id="545b9-866">Concatenação</span><span class="sxs-lookup"><span data-stu-id="545b9-866">Concatenation</span></span>
<span data-ttu-id="545b9-867">A sintaxe é `input(.|.SelectMany())(.Select()|.Where())*`.</span><span class="sxs-lookup"><span data-stu-id="545b9-867">The syntax is `input(.|.SelectMany())(.Select()|.Where())*`.</span></span> <span data-ttu-id="545b9-868">Uma consulta concatenada pode ser iniciada por uma consulta `SelectMany` opcional, seguida por múltiplos operadores `Select` ou `Where`.</span><span class="sxs-lookup"><span data-stu-id="545b9-868">A concatenated query can start with an optional `SelectMany` query followed by multiple `Select` or `Where` operators.</span></span>

<span data-ttu-id="545b9-869">**Expressão lambda do LINQ**</span><span class="sxs-lookup"><span data-stu-id="545b9-869">**LINQ lambda expression**</span></span>

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

<span data-ttu-id="545b9-870">**SQL**</span><span class="sxs-lookup"><span data-stu-id="545b9-870">**SQL**</span></span>

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



<span data-ttu-id="545b9-871">**Expressão lambda do LINQ**</span><span class="sxs-lookup"><span data-stu-id="545b9-871">**LINQ lambda expression**</span></span>

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

<span data-ttu-id="545b9-872">**SQL**</span><span class="sxs-lookup"><span data-stu-id="545b9-872">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



<span data-ttu-id="545b9-873">**Expressão lambda do LINQ**</span><span class="sxs-lookup"><span data-stu-id="545b9-873">**LINQ lambda expression**</span></span>

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

<span data-ttu-id="545b9-874">**SQL**</span><span class="sxs-lookup"><span data-stu-id="545b9-874">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



<span data-ttu-id="545b9-875">**Expressão lambda do LINQ**</span><span class="sxs-lookup"><span data-stu-id="545b9-875">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

<span data-ttu-id="545b9-876">**SQL**</span><span class="sxs-lookup"><span data-stu-id="545b9-876">**SQL**</span></span> 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a><span data-ttu-id="545b9-877">Aninhamento</span><span class="sxs-lookup"><span data-stu-id="545b9-877">Nesting</span></span>
<span data-ttu-id="545b9-878">A sintaxe é `input.SelectMany(x=>x.Q())`, em que Q é um operador `Select`, `SelectMany` ou `Where`.</span><span class="sxs-lookup"><span data-stu-id="545b9-878">The syntax is `input.SelectMany(x=>x.Q())` where Q is a `Select`, `SelectMany`, or `Where` operator.</span></span>

<span data-ttu-id="545b9-879">Em uma consulta aninhada, a consulta interior é aplicada a cada elemento da coleção externa.</span><span class="sxs-lookup"><span data-stu-id="545b9-879">In a nested query, the inner query is applied to each element of the outer collection.</span></span> <span data-ttu-id="545b9-880">Um recurso importante é que a consulta interna pode se referir aos campos dos elementos na coleção exterior, como autojunções.</span><span class="sxs-lookup"><span data-stu-id="545b9-880">One important feature is that the inner query can refer to the fields of the elements in the outer collection like self-joins.</span></span>

<span data-ttu-id="545b9-881">**Expressão lambda do LINQ**</span><span class="sxs-lookup"><span data-stu-id="545b9-881">**LINQ lambda expression**</span></span>

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

<span data-ttu-id="545b9-882">**SQL**</span><span class="sxs-lookup"><span data-stu-id="545b9-882">**SQL**</span></span> 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


<span data-ttu-id="545b9-883">**Expressão lambda do LINQ**</span><span class="sxs-lookup"><span data-stu-id="545b9-883">**LINQ lambda expression**</span></span>

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

<span data-ttu-id="545b9-884">**SQL**</span><span class="sxs-lookup"><span data-stu-id="545b9-884">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



<span data-ttu-id="545b9-885">**Expressão lambda do LINQ**</span><span class="sxs-lookup"><span data-stu-id="545b9-885">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

<span data-ttu-id="545b9-886">**SQL**</span><span class="sxs-lookup"><span data-stu-id="545b9-886">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <span data-ttu-id="545b9-887"><a id="ExecutingSqlQueries"></a>Execução de consultas SQL</span><span class="sxs-lookup"><span data-stu-id="545b9-887"><a id="ExecutingSqlQueries"></a>Executing SQL queries</span></span>
<span data-ttu-id="545b9-888">O Cosmos DB expõe recursos por meio de uma API REST que pode ser chamada por qualquer linguagem que possa fazer solicitações HTTP/HTTPS.</span><span class="sxs-lookup"><span data-stu-id="545b9-888">Cosmos DB exposes resources through a REST API that can be called by any language capable of making HTTP/HTTPS requests.</span></span> <span data-ttu-id="545b9-889">Além disso, o Cosmos DB oferece bibliotecas de programação para várias linguagens populares, como .NET, Node.js, JavaScript e Python.</span><span class="sxs-lookup"><span data-stu-id="545b9-889">Additionally, Cosmos DB offers programming libraries for several popular languages like .NET, Node.js, JavaScript, and Python.</span></span> <span data-ttu-id="545b9-890">A API REST e as diversas bibliotecas suportam a consulta por meio de SQL.</span><span class="sxs-lookup"><span data-stu-id="545b9-890">The REST API and the various libraries all support querying through SQL.</span></span> <span data-ttu-id="545b9-891">O SDK .NET oferece suporte para consultas no LINQ além da SQL.</span><span class="sxs-lookup"><span data-stu-id="545b9-891">The .NET SDK supports LINQ querying in addition to SQL.</span></span>

<span data-ttu-id="545b9-892">Os exemplos a seguir mostram como criar uma consulta e enviá-la a uma conta de banco de dados do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="545b9-892">The following examples show how to create a query and submit it against a Cosmos DB database account.</span></span>

### <span data-ttu-id="545b9-893"><a id="RestAPI"></a>API REST</span><span class="sxs-lookup"><span data-stu-id="545b9-893"><a id="RestAPI"></a>REST API</span></span>
<span data-ttu-id="545b9-894">O Cosmos DB oferece um modelo de programação RESTful por HTTP.</span><span class="sxs-lookup"><span data-stu-id="545b9-894">Cosmos DB offers an open RESTful programming model over HTTP.</span></span> <span data-ttu-id="545b9-895">As contas do banco de dados podem ser provisionadas usando uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="545b9-895">Database accounts can be provisioned using an Azure subscription.</span></span> <span data-ttu-id="545b9-896">O modelo de recurso do Cosmos DB consiste em um conjunto de recursos em uma conta de banco de dados, cada um endereçável usando um URI lógico e estável.</span><span class="sxs-lookup"><span data-stu-id="545b9-896">The Cosmos DB resource model consists of a set of resources under a database account, each  of which is addressable using a logical and stable URI.</span></span> <span data-ttu-id="545b9-897">Um conjunto de recursos é referido como um feed neste documento.</span><span class="sxs-lookup"><span data-stu-id="545b9-897">A set of resources is referred to as a feed in this document.</span></span> <span data-ttu-id="545b9-898">Uma conta do banco de dados é formada por um conjunto de bancos de dados, cada um contendo diversas coleções, cada uma delas, por sua vez, contendo documentos, UDFs e outros tipos de recursos.</span><span class="sxs-lookup"><span data-stu-id="545b9-898">A database account consists of a set of databases, each containing multiple collections, each of which in-turn contain documents, UDFs, and other resource types.</span></span>

<span data-ttu-id="545b9-899">O modelo de interação básico com esses recursos é por meio dos verbos HTTP GET, PUT, POST e DELETE, com sua interpretação padrão.</span><span class="sxs-lookup"><span data-stu-id="545b9-899">The basic interaction model with these resources is through the HTTP verbs GET, PUT, POST, and DELETE with their standard interpretation.</span></span> <span data-ttu-id="545b9-900">O verbo POST é usado para criação de um novo recurso, para executar um procedimento armazenado ou para emitir uma consulta do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="545b9-900">The POST verb is used for creation of a new resource, for executing a stored procedure or for issuing a Cosmos DB query.</span></span> <span data-ttu-id="545b9-901">As consultas sempre são operações somente leitura, sem efeitos colaterais.</span><span class="sxs-lookup"><span data-stu-id="545b9-901">Queries are always read-only operations with no side-effects.</span></span>

<span data-ttu-id="545b9-902">Os exemplos a seguir mostram um POST para uma consulta da API do DocumentDB feita em uma coleção que contém os dois documentos de exemplo que vimos até agora.</span><span class="sxs-lookup"><span data-stu-id="545b9-902">The following examples show a POST for a DocumentDB API query made against a collection containing the two sample documents we've reviewed so far.</span></span> <span data-ttu-id="545b9-903">A consulta tem um filtro simples na propriedade do nome JSON.</span><span class="sxs-lookup"><span data-stu-id="545b9-903">The query has a simple filter on the JSON name property.</span></span> <span data-ttu-id="545b9-904">Observe o uso dos cabeçalhos `x-ms-documentdb-isquery` e Content-Type: `application/query+json` para indicar que a operação é uma consulta.</span><span class="sxs-lookup"><span data-stu-id="545b9-904">Note the use of the `x-ms-documentdb-isquery` and Content-Type: `application/query+json` headers to denote that the operation is a query.</span></span>

<span data-ttu-id="545b9-905">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="545b9-905">**Request**</span></span>

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


<span data-ttu-id="545b9-906">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-906">**Results**</span></span>

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


<span data-ttu-id="545b9-907">O segundo exemplo mostra uma consulta mais complexa que retorna múltiplos resultados da junção.</span><span class="sxs-lookup"><span data-stu-id="545b9-907">The second example shows a more complex query that returns multiple results from the join.</span></span>

<span data-ttu-id="545b9-908">**Solicitação**</span><span class="sxs-lookup"><span data-stu-id="545b9-908">**Request**</span></span>

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


<span data-ttu-id="545b9-909">**Resultados**</span><span class="sxs-lookup"><span data-stu-id="545b9-909">**Results**</span></span>

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


<span data-ttu-id="545b9-910">Se os resultados de uma consulta não couberem em uma página de resultados, a API REST retornará um token de continuação por meio do cabeçalho de resposta `x-ms-continuation-token` .</span><span class="sxs-lookup"><span data-stu-id="545b9-910">If a query's results cannot fit within a single page of results, then the REST API returns a continuation token through the `x-ms-continuation-token` response header.</span></span> <span data-ttu-id="545b9-911">Os clientes podem paginar os resultados incluindo o cabeçalho nos resultados subsequentes.</span><span class="sxs-lookup"><span data-stu-id="545b9-911">Clients can paginate results by including the header in subsequent results.</span></span> <span data-ttu-id="545b9-912">O número de resultados por página também pode ser controlado por meio do cabeçalho de número `x-ms-max-item-count` .</span><span class="sxs-lookup"><span data-stu-id="545b9-912">The number of results per page can also be controlled through the `x-ms-max-item-count` number header.</span></span> <span data-ttu-id="545b9-913">Se a consulta especificada tiver uma função de agregação como `COUNT`, a página de consulta poderá retornar um valor parcialmente agregado na página de resultados.</span><span class="sxs-lookup"><span data-stu-id="545b9-913">If the specified query has an aggregation function like `COUNT`, then the query page may return a partially aggregated value over the page of results.</span></span> <span data-ttu-id="545b9-914">Os clientes devem executar uma segunda agregação nesses resultados para produzir os resultados finais. Por exemplo, a soma das contagens retornadas nas páginas individuais para retornar a contagem total.</span><span class="sxs-lookup"><span data-stu-id="545b9-914">The clients must perform a second-level aggregation over these results to produce the final results, for example, sum over the counts returned in the individual pages to return the total count.</span></span>

<span data-ttu-id="545b9-915">Para gerenciar a política de consistência de dados para consultas, use o cabeçalho `x-ms-consistency-level` como todas as solicitações da API REST.</span><span class="sxs-lookup"><span data-stu-id="545b9-915">To manage the data consistency policy for queries, use the `x-ms-consistency-level` header like all REST API requests.</span></span> <span data-ttu-id="545b9-916">Para que haja consistência da sessão, é necessário também ecoar o cabeçalho de cookie `x-ms-session-token` mais recente na solicitação de consulta.</span><span class="sxs-lookup"><span data-stu-id="545b9-916">For session consistency, it is required to also echo the latest `x-ms-session-token` Cookie header in the query request.</span></span> <span data-ttu-id="545b9-917">A política de indexação da coleção consultada também pode influenciar a consistência dos resultados da consulta.</span><span class="sxs-lookup"><span data-stu-id="545b9-917">The queried collection's indexing policy can also influence the consistency of query results.</span></span> <span data-ttu-id="545b9-918">Com as configurações da política de indexação padrão, para as coleções, o índice sempre está atualizado com o conteúdo dos documentos e os resultados das consultas correspondem à consistência escolhida para os dados.</span><span class="sxs-lookup"><span data-stu-id="545b9-918">With the default indexing policy settings, for collections the index is always current with the document contents and query results match the consistency chosen for data.</span></span> <span data-ttu-id="545b9-919">Se a política de indexação for relaxada para Lenta, as consultas poderão retornar resultados obsoletos.</span><span class="sxs-lookup"><span data-stu-id="545b9-919">If the indexing policy is relaxed to Lazy, then queries can return stale results.</span></span> <span data-ttu-id="545b9-920">Para obter mais informações, consulte [Níveis de consistência no Azure Cosmos DB][consistency-levels].</span><span class="sxs-lookup"><span data-stu-id="545b9-920">For more information, see [Azure Cosmos DB Consistency Levels][consistency-levels].</span></span>

<span data-ttu-id="545b9-921">Se a política de indexação configurada na coleção não puder dar suporte à consulta especificada, o servidor do Azure Cosmos DB retornará um erro 400, “Solicitação Inválida”.</span><span class="sxs-lookup"><span data-stu-id="545b9-921">If the configured indexing policy on the collection cannot support the specified query, the Azure Cosmos DB server returns 400 "Bad Request".</span></span> <span data-ttu-id="545b9-922">Este código é retornado para consultas de intervalo em caminhos configurados para pesquisas hash (igualdade), e para caminhos excluídos explicitamente da indexação.</span><span class="sxs-lookup"><span data-stu-id="545b9-922">This is returned for range queries against paths configured for hash (equality) lookups, and for paths explicitly excluded from indexing.</span></span> <span data-ttu-id="545b9-923">O cabeçalho `x-ms-documentdb-query-enable-scan` pode ser especificado para permitir que a consulta faça uma verificação quando um índice estiver indisponível.</span><span class="sxs-lookup"><span data-stu-id="545b9-923">The `x-ms-documentdb-query-enable-scan` header can be specified to allow the query to perform a scan when an index is not available.</span></span>

<span data-ttu-id="545b9-924">Você pode obter métricas detalhadas na execução da consulta configurando o cabeçalho `x-ms-documentdb-populatequerymetrics` como `True`.</span><span class="sxs-lookup"><span data-stu-id="545b9-924">You can get detailed metrics on query execution by setting `x-ms-documentdb-populatequerymetrics` header to `True`.</span></span> <span data-ttu-id="545b9-925">Para obter mais informações, consulte [Métricas de consulta SQL para a API do DocumentDB do Azure Cosmos DB](documentdb-sql-query-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="545b9-925">For more information, see [SQL query metrics for Azure Cosmos DB DocumentDB API](documentdb-sql-query-metrics.md).</span></span>

### <span data-ttu-id="545b9-926"><a id="DotNetSdk"></a>SDK do C# (.NET)</span><span class="sxs-lookup"><span data-stu-id="545b9-926"><a id="DotNetSdk"></a>C# (.NET) SDK</span></span>
<span data-ttu-id="545b9-927">O SDK .NET suporta consultas LINQ e SQL.</span><span class="sxs-lookup"><span data-stu-id="545b9-927">The .NET SDK supports both LINQ and SQL querying.</span></span> <span data-ttu-id="545b9-928">O exemplo a seguir mostra como realizar a consulta de filtro simples mencionada no início deste documento.</span><span class="sxs-lookup"><span data-stu-id="545b9-928">The following example shows how to perform the simple filter query introduced earlier in this document.</span></span>

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


<span data-ttu-id="545b9-929">Esta amostra compara duas propriedades quanto à igualdade dentro de cada documento e usa projeções anônimas.</span><span class="sxs-lookup"><span data-stu-id="545b9-929">This sample compares two properties for equality within each document and uses anonymous projections.</span></span> 

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


<span data-ttu-id="545b9-930">A amostra seguinte mostra junções, expressas por meio do LINQ SelectMany.</span><span class="sxs-lookup"><span data-stu-id="545b9-930">The next sample shows joins, expressed through LINQ SelectMany.</span></span>

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



<span data-ttu-id="545b9-931">O cliente .NET itera automaticamente em todas as páginas dos resultados de pesquisa nos blocos foreach, conforme mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="545b9-931">The .NET client automatically iterates through all the pages of query results in the foreach blocks as shown above.</span></span> <span data-ttu-id="545b9-932">As opções de consulta introduzidas na seção da API REST também estão disponíveis no SDK .NET usando as classes `FeedOptions` and `FeedResponse` no método CreateDocumentQuery.</span><span class="sxs-lookup"><span data-stu-id="545b9-932">The query options introduced in the REST API section are also available in the .NET SDK using the `FeedOptions` and `FeedResponse` classes in the CreateDocumentQuery method.</span></span> <span data-ttu-id="545b9-933">O número de páginas pode ser controlado usando a configuração `MaxItemCount` .</span><span class="sxs-lookup"><span data-stu-id="545b9-933">The number of pages can be controlled using the `MaxItemCount` setting.</span></span> 

<span data-ttu-id="545b9-934">Você também pode controlar explicitamente paginação criando `IDocumentQueryable` usando o objeto `IQueryable`, lendo os valores` ResponseContinuationToken` e passando-os de volta como `RequestContinuationToken` em `FeedOptions`.</span><span class="sxs-lookup"><span data-stu-id="545b9-934">You can also explicitly control paging by creating `IDocumentQueryable` using the `IQueryable` object, then by reading the` ResponseContinuationToken` values and passing them back as `RequestContinuationToken` in `FeedOptions`.</span></span> <span data-ttu-id="545b9-935">`EnableScanInQuery` pode ser configurado para permitir verificações quando não for possível que a política de indexação configurada dê suporte à consulta.</span><span class="sxs-lookup"><span data-stu-id="545b9-935">`EnableScanInQuery` can be set to enable scans when the query cannot be supported by the configured indexing policy.</span></span> <span data-ttu-id="545b9-936">Para coleções particionadas, use `PartitionKey` para executar a consulta em uma única partição (embora o Cosmos DB possa extraí-la do texto da consulta) e `EnableCrossPartitionQuery` para executar consultas que talvez precisem ser executadas em várias partições.</span><span class="sxs-lookup"><span data-stu-id="545b9-936">For partitioned collections, you can use `PartitionKey` to run the query against a single partition (though Cosmos DB can automatically extract this from the query text), and `EnableCrossPartitionQuery` to run queries that may need to be run against multiple partitions.</span></span> 

<span data-ttu-id="545b9-937">Consulte [Amostras do .NET no Azure Cosmos DB](https://github.com/Azure/azure-documentdb-net) para obter mais amostras que contêm consultas.</span><span class="sxs-lookup"><span data-stu-id="545b9-937">Refer to [Azure Cosmos DB .NET samples](https://github.com/Azure/azure-documentdb-net) for more samples containing queries.</span></span> 

### <span data-ttu-id="545b9-938"><a id="JavaScriptServerSideApi"></a>API do lado servidor do JavaScript</span><span class="sxs-lookup"><span data-stu-id="545b9-938"><a id="JavaScriptServerSideApi"></a>JavaScript server-side API</span></span>
<span data-ttu-id="545b9-939">O Cosmos DB oferece um modelo de programação para executar a lógica de aplicativos baseados em JavaScript diretamente nas coleções usando procedimentos armazenados e gatilhos.</span><span class="sxs-lookup"><span data-stu-id="545b9-939">Cosmos DB provides a programming model for executing JavaScript based application logic directly on the collections using stored procedures and triggers.</span></span> <span data-ttu-id="545b9-940">A lógica de JavaScript registrada no nível da coleção pode então emitir operações do banco de dados nas operações dos documentos da coleção determinada.</span><span class="sxs-lookup"><span data-stu-id="545b9-940">The JavaScript logic registered at a collection level can then issue database operations on the operations on the documents of the given collection.</span></span> <span data-ttu-id="545b9-941">Essas operações são encapsuladas em transações ACID ambiente.</span><span class="sxs-lookup"><span data-stu-id="545b9-941">These operations are wrapped in ambient ACID transactions.</span></span>

<span data-ttu-id="545b9-942">O exemplo a seguir mostra como usar o queryDocuments na API do servidor do JavaScript para realizar consultas de dentro de procedimentos e gatilhos armazenados.</span><span class="sxs-lookup"><span data-stu-id="545b9-942">The following example shows how to use the queryDocuments in the JavaScript server API to make queries from inside stored procedures and triggers.</span></span>

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

                        // Replace the author name for all documents that satisfied the query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don't need to execute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);
                        }
                    })
            });
    }

## <span data-ttu-id="545b9-943"><a id="References"></a>Referências</span><span class="sxs-lookup"><span data-stu-id="545b9-943"><a id="References"></a>References</span></span>
1. <span data-ttu-id="545b9-944">[Introdução ao Azure Cosmos DB][introduction]</span><span class="sxs-lookup"><span data-stu-id="545b9-944">[Introduction to Azure Cosmos DB][introduction]</span></span>
2. [<span data-ttu-id="545b9-945">Especificação do SQL no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="545b9-945">Azure Cosmos DB SQL specification</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=510612)
3. [<span data-ttu-id="545b9-946">Amostras do .NET no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="545b9-946">Azure Cosmos DB .NET samples</span></span>](https://github.com/Azure/azure-documentdb-net)
4. <span data-ttu-id="545b9-947">[Níveis de consistência do Azure Cosmos DB][consistency-levels]</span><span class="sxs-lookup"><span data-stu-id="545b9-947">[Azure Cosmos DB Consistency Levels][consistency-levels]</span></span>
5. <span data-ttu-id="545b9-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span><span class="sxs-lookup"><span data-stu-id="545b9-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span></span>
6. <span data-ttu-id="545b9-949">JSON [http://json.org/](http://json.org/)</span><span class="sxs-lookup"><span data-stu-id="545b9-949">JSON [http://json.org/](http://json.org/)</span></span>
7. <span data-ttu-id="545b9-950">Especificação Javascript [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span><span class="sxs-lookup"><span data-stu-id="545b9-950">Javascript Specification [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span></span> 
8. <span data-ttu-id="545b9-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span><span class="sxs-lookup"><span data-stu-id="545b9-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span></span> 
9. <span data-ttu-id="545b9-952">Técnicas de avaliação de consulta para bancos de dados de grande porte [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span><span class="sxs-lookup"><span data-stu-id="545b9-952">Query evaluation techniques for large databases [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span></span>
10. <span data-ttu-id="545b9-953">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span><span class="sxs-lookup"><span data-stu-id="545b9-953">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span></span>
11. <span data-ttu-id="545b9-954">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span><span class="sxs-lookup"><span data-stu-id="545b9-954">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span></span>
12. <span data-ttu-id="545b9-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span><span class="sxs-lookup"><span data-stu-id="545b9-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span></span>
13. <span data-ttu-id="545b9-956">G.</span><span class="sxs-lookup"><span data-stu-id="545b9-956">G.</span></span> <span data-ttu-id="545b9-957">Graefe.</span><span class="sxs-lookup"><span data-stu-id="545b9-957">Graefe.</span></span> <span data-ttu-id="545b9-958">Estrutura em cascata para otimização da consulta.</span><span class="sxs-lookup"><span data-stu-id="545b9-958">The Cascades framework for query optimization.</span></span> <span data-ttu-id="545b9-959">IEEE Data Eng.</span><span class="sxs-lookup"><span data-stu-id="545b9-959">IEEE Data Eng.</span></span> <span data-ttu-id="545b9-960">Bull., 18(3): 1995.</span><span class="sxs-lookup"><span data-stu-id="545b9-960">Bull., 18(3): 1995.</span></span>

[1]: ./media/documentdb-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md