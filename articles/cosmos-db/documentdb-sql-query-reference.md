---
title: 'API DocumentDB do BD Cosmos do Azure: sintaxe SQL | Microsoft Docs'
description: "Documentação de referência para a linguagem de consulta SQL da API DocumentDB do BD Cosmos do Azure."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: reference
ms.date: 06/13/2017
ms.author: mimig
ms.openlocfilehash: 63b2d20c74df4fd6173994ee1a727594ba8afba3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-documentdb-api-sql-syntax-reference"></a><span data-ttu-id="60630-103">API DocumentDB do BD Cosmos do Azure: referência de sintaxe SQL</span><span class="sxs-lookup"><span data-stu-id="60630-103">Azure Cosmos DB DocumentDB API: SQL syntax reference</span></span>

<span data-ttu-id="60630-104">A API DocumentDB do BD Cosmos do Azure dá suporte a documentos de consulta usando um SQL (Structured Query Language) familiar, como a gramática, em documentos JSON hierárquicos, sem a necessidade de esquema explícito ou criação de índices secundários.</span><span class="sxs-lookup"><span data-stu-id="60630-104">The Azure Cosmos DB DocumentDB API supports querying documents using a familiar SQL (Structured Query Language) like grammar over hierarchical JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> <span data-ttu-id="60630-105">Este tópico fornece a documentação de referência para a linguagem de consulta SQL da API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="60630-105">This topic provides reference documentation for the DocumentDB API SQL query language.</span></span>

<span data-ttu-id="60630-106">Para obter uma explicação da linguagem de consulta SQL da API DocumentDB, confira [Consultas SQL para a API DocumentDB do BD Cosmos do Azure](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="60630-106">For a walkthrough of the DocumentDB API SQL query language, see [SQL queries for Azure Cosmos DB DocumentDB API](documentdb-sql-query.md).</span></span>  
  
<span data-ttu-id="60630-107">Você também está convidado a visitar o [Query Playground](http://www.documentdb.com/sql/demo), onde pode experimentar o BD Cosmos do Azure e executar consultas SQL em relação a nosso conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="60630-107">We also invite you to visit the [Query Playground](http://www.documentdb.com/sql/demo) where you can try Azure Cosmos DB and run SQL queries against our dataset.</span></span>  
  
## <a name="select-query"></a><span data-ttu-id="60630-108">Consulta SELECT</span><span class="sxs-lookup"><span data-stu-id="60630-108">SELECT query</span></span>  
<span data-ttu-id="60630-109">Recupera documentos JSON do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="60630-109">Retrieves JSON documents from the database.</span></span> <span data-ttu-id="60630-110">Dá suporte a avaliação de expressão, projeções, filtragem e junções.</span><span class="sxs-lookup"><span data-stu-id="60630-110">Supports expression evaluation, projections, filtering and joins.</span></span>  <span data-ttu-id="60630-111">As convenções usadas para descrever as instruções SELECT são tabuladas na seção Convenções de sintaxe.</span><span class="sxs-lookup"><span data-stu-id="60630-111">The conventions used for describing the SELECT statements are tabulated in the Syntax conventions section.</span></span>  
  
<span data-ttu-id="60630-112">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-112">**Syntax**</span></span>  
  
```
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 <span data-ttu-id="60630-113">**Comentários**</span><span class="sxs-lookup"><span data-stu-id="60630-113">**Remarks**</span></span>  
  
 <span data-ttu-id="60630-114">Consulte as seguintes seções para obter detalhes sobre cada cláusula:</span><span class="sxs-lookup"><span data-stu-id="60630-114">See following sections for details on each clause:</span></span>  
  
-   [<span data-ttu-id="60630-115">Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="60630-115">SELECT clause</span></span>](#bk_select_query)  
  
-   [<span data-ttu-id="60630-116">Cláusula FROM</span><span class="sxs-lookup"><span data-stu-id="60630-116">FROM clause</span></span>](#bk_from_clause)  
  
-   [<span data-ttu-id="60630-117">Cláusula WHERE</span><span class="sxs-lookup"><span data-stu-id="60630-117">WHERE clause</span></span>](#bk_where_clause)  
  
-   [<span data-ttu-id="60630-118">Cláusula ORDER BY</span><span class="sxs-lookup"><span data-stu-id="60630-118">ORDER BY clause</span></span>](#bk_orderby_clause)  
  
<span data-ttu-id="60630-119">As cláusulas na instrução SELECT devem ser ordenadas conforme mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="60630-119">The clauses in the SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="60630-120">Qualquer uma das cláusulas opcionais pode ser omitida.</span><span class="sxs-lookup"><span data-stu-id="60630-120">Any one of the optional clauses can be omitted.</span></span> <span data-ttu-id="60630-121">Mas quando são usadas, elas devem aparecer na ordem correta.</span><span class="sxs-lookup"><span data-stu-id="60630-121">But when optional clauses are used, they must appear in the right order.</span></span>  
  
<span data-ttu-id="60630-122">**Ordem de processamento lógico da instrução SELECT**</span><span class="sxs-lookup"><span data-stu-id="60630-122">**Logical Processing Order of the SELECT statement**</span></span>  
  
<span data-ttu-id="60630-123">A ordem na qual as cláusulas são processadas é:</span><span class="sxs-lookup"><span data-stu-id="60630-123">The order in which clauses are processed is:</span></span>  

1.  [<span data-ttu-id="60630-124">Cláusula FROM</span><span class="sxs-lookup"><span data-stu-id="60630-124">FROM clause</span></span>](#bk_from_clause)  
2.  [<span data-ttu-id="60630-125">Cláusula WHERE</span><span class="sxs-lookup"><span data-stu-id="60630-125">WHERE clause</span></span>](#bk_where_clause)  
3.  [<span data-ttu-id="60630-126">Cláusula ORDER BY</span><span class="sxs-lookup"><span data-stu-id="60630-126">ORDER BY clause</span></span>](#bk_orderby_clause)  
4.  [<span data-ttu-id="60630-127">Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="60630-127">SELECT clause</span></span>](#bk_select_query)  

<span data-ttu-id="60630-128">Observe que isso é diferente da ordem em que aparecem na sintaxe.</span><span class="sxs-lookup"><span data-stu-id="60630-128">Note that this is different from the order in which they appear in the syntax.</span></span> <span data-ttu-id="60630-129">A ordenação é tal que todos os símbolos novos introduzidos por uma cláusula processada são visíveis e podem ser usados em cláusulas processadas posteriormente.</span><span class="sxs-lookup"><span data-stu-id="60630-129">The ordering is such that all new symbols introduced by a processed clause are visible and can be used in clauses processed later.</span></span> <span data-ttu-id="60630-130">Por exemplo, os aliases declarados em uma cláusula FROM podem ser acessados nas cláusulas SELECT e WHERE.</span><span class="sxs-lookup"><span data-stu-id="60630-130">For instance, aliases declared in a FROM clause are accessible in WHERE and SELECT clauses.</span></span>  

<span data-ttu-id="60630-131">**Comentários e caracteres de espaço em branco**</span><span class="sxs-lookup"><span data-stu-id="60630-131">**Whitespace characters and comments**</span></span>  

<span data-ttu-id="60630-132">Todos os caracteres de espaço em branco que não fazem parte de uma cadeia de caracteres entre aspas ou identificador entre aspas não fazem parte da gramática da linguagem e são ignorados durante a análise.</span><span class="sxs-lookup"><span data-stu-id="60630-132">All white space characters which are not part of a quoted string or quoted identifier are not part of the language grammar and are ignored during parsing.</span></span>  

<span data-ttu-id="60630-133">A linguagem de consulta dá suporte a comentários de estilo T-SQL, como</span><span class="sxs-lookup"><span data-stu-id="60630-133">The query language supports T-SQL style comments like</span></span>  

-   <span data-ttu-id="60630-134">Instrução SQL`-- comment text [newline]`</span><span class="sxs-lookup"><span data-stu-id="60630-134">SQL Statement `-- comment text [newline]`</span></span>  

<span data-ttu-id="60630-135">Embora os comentários e caracteres de espaço em branco não tenham nenhum significado na gramática, eles devem ser usados para separar os tokens.</span><span class="sxs-lookup"><span data-stu-id="60630-135">While whitespace characters and comments do not have any significance in the grammar, they must be used to separate tokens.</span></span> <span data-ttu-id="60630-136">Por exemplo: `-1e5` é um token de número único, ao passo que `: – 1 e5` é um token de sinal de subtração seguido pelo número 1 e identificador e5.</span><span class="sxs-lookup"><span data-stu-id="60630-136">For instance: `-1e5` is a single number token, while`: – 1 e5` is a minus token followed by number 1 and identifier e5.</span></span>  

##  <span data-ttu-id="60630-137"><a name="bk_select_query"></a> Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="60630-137"><a name="bk_select_query"></a> SELECT clause</span></span>  
<span data-ttu-id="60630-138">As cláusulas na instrução SELECT devem ser ordenadas conforme mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="60630-138">The clauses in the SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="60630-139">Qualquer uma das cláusulas opcionais pode ser omitida.</span><span class="sxs-lookup"><span data-stu-id="60630-139">Any one of the optional clauses can be omitted.</span></span> <span data-ttu-id="60630-140">Mas quando são usadas, elas devem aparecer na ordem correta.</span><span class="sxs-lookup"><span data-stu-id="60630-140">But when optional clauses are used, they must appear in the right order.</span></span>  

<span data-ttu-id="60630-141">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-141">**Syntax**</span></span>  
```  
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 <span data-ttu-id="60630-142">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-142">**Arguments**</span></span>  
  
 `<select_specification>`  
  
 <span data-ttu-id="60630-143">Propriedades ou valor a ser selecionado para o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-143">Properties or value to be selected for the result set.</span></span>  
  
 `'*'`  
  
<span data-ttu-id="60630-144">Especifica que o valor deve ser recuperado sem fazer alterações.</span><span class="sxs-lookup"><span data-stu-id="60630-144">Specifies that the value should be retrieved without making any changes.</span></span> <span data-ttu-id="60630-145">Especificamente, se o valor processado for um objeto, todas as propriedades serão recuperadas.</span><span class="sxs-lookup"><span data-stu-id="60630-145">Specifically if the processed value is an object, all properties will be retrieved.</span></span>  
  
 `<object_property_list>`  
  
<span data-ttu-id="60630-146">Especifica a lista de propriedades a serem recuperadas.</span><span class="sxs-lookup"><span data-stu-id="60630-146">Specifies the list of properties to be retrieved.</span></span> <span data-ttu-id="60630-147">Cada valor retornado será um objeto com as propriedades especificadas.</span><span class="sxs-lookup"><span data-stu-id="60630-147">Each returned value will be an object with the properties specified.</span></span>  
  
`VALUE`  
  
<span data-ttu-id="60630-148">Especifica que o valor JSON deve ser recuperado em vez do objeto JSON completo.</span><span class="sxs-lookup"><span data-stu-id="60630-148">Specifies that the JSON value should be retrieved instead of the complete JSON object.</span></span> <span data-ttu-id="60630-149">Isso, ao contrário de `<property_list>`, não encapsula o valor projetado em um objeto.</span><span class="sxs-lookup"><span data-stu-id="60630-149">This, unlike `<property_list>` does not wrap the projected value in an object.</span></span>  
  
`<scalar_expression>`  
  
<span data-ttu-id="60630-150">Expressão que representa o valor a ser calculado.</span><span class="sxs-lookup"><span data-stu-id="60630-150">Expression representing the value to be computed.</span></span> <span data-ttu-id="60630-151">Consulte a seção [Expressões escalares](#bk_scalar_expressions) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="60630-151">See [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
<span data-ttu-id="60630-152">**Comentários**</span><span class="sxs-lookup"><span data-stu-id="60630-152">**Remarks**</span></span>  
  
<span data-ttu-id="60630-153">A sintaxe `SELECT *` só será válida se a cláusula FROM tiver declarado exatamente um alias.</span><span class="sxs-lookup"><span data-stu-id="60630-153">The `SELECT *` syntax is only valid if FROM clause has declared exactly one alias.</span></span> <span data-ttu-id="60630-154">`SELECT *` fornece uma projeção de identidade, que pode ser útil se nenhuma projeção é necessária.</span><span class="sxs-lookup"><span data-stu-id="60630-154">`SELECT *` provides an identity projection, which can be useful if no projection is needed.</span></span> <span data-ttu-id="60630-155">SELECT * só é válida se a cláusula FROM é especificada e introduzida uma única fonte de entrada.</span><span class="sxs-lookup"><span data-stu-id="60630-155">SELECT * is only valid if FROM clause is specified and introduced only a single input source.</span></span>  
  
<span data-ttu-id="60630-156">Observe que `SELECT <select_list>` e `SELECT *` são "açúcar sintático" e podem ser expressos, como alternativa, usando instruções SELECT simples, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="60630-156">Note that `SELECT <select_list>` and `SELECT *` are "syntactic sugar" and can be alternatively expressed by using simple SELECT statements as shown below.</span></span>  
  
1.  `SELECT * FROM ... AS from_alias ...`  
  
     <span data-ttu-id="60630-157">é equivalente a:</span><span class="sxs-lookup"><span data-stu-id="60630-157">is equivalent to:</span></span>  
  
     `SELECT from_alias FROM ... AS from_alias ...`  
  
2.  `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
     <span data-ttu-id="60630-158">é equivalente a:</span><span class="sxs-lookup"><span data-stu-id="60630-158">is equivalent to:</span></span>  
  
     `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
<span data-ttu-id="60630-159">**Consulte também**</span><span class="sxs-lookup"><span data-stu-id="60630-159">**See Also**</span></span>  
  
[<span data-ttu-id="60630-160">Expressões escalares</span><span class="sxs-lookup"><span data-stu-id="60630-160">Scalar expressions</span></span>](#bk_scalar_expressions)  
[<span data-ttu-id="60630-161">Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="60630-161">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="60630-162"><a name="bk_from_clause"></a> Cláusula FROM</span><span class="sxs-lookup"><span data-stu-id="60630-162"><a name="bk_from_clause"></a> FROM clause</span></span>  
<span data-ttu-id="60630-163">Especifica a fonte ou as fontes unidas.</span><span class="sxs-lookup"><span data-stu-id="60630-163">Specifies the source or joined sources.</span></span> <span data-ttu-id="60630-164">A cláusula FROM é opcional.</span><span class="sxs-lookup"><span data-stu-id="60630-164">The FROM clause is optional.</span></span> <span data-ttu-id="60630-165">Se não for especificado, outras cláusulas ainda serão executadas como se a cláusula FROM fornecesse um único documento.</span><span class="sxs-lookup"><span data-stu-id="60630-165">If not specified, other clauses will still be executed as if FROM clause provided a single document.</span></span>  
  
<span data-ttu-id="60630-166">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-166">**Syntax**</span></span>  
  
```  
FROM <from_specification>  
  
<from_specification> ::=   
        <from_source> {[ JOIN <from_source>][,...n]}  
  
<from_source> ::=   
          <collection_expression> [[AS] input_alias]  
        | input_alias IN <collection_expression>  
  
<collection_expression> ::=   
        ROOT   
     | collection_name  
     | input_alias  
     | <collection_expression> '.' property_name  
     | <collection_expression> '[' "property_name" | array_index ']'  
```  
  
<span data-ttu-id="60630-167">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-167">**Arguments**</span></span>  
  
`<from_source>`  
  
<span data-ttu-id="60630-168">Especifica uma fonte de dados, com ou sem um alias.</span><span class="sxs-lookup"><span data-stu-id="60630-168">Specifies a data source, with or without an alias.</span></span> <span data-ttu-id="60630-169">Se o alias não for especificado, ele será inferido de `<collection_expression>` usando as seguinte regras:</span><span class="sxs-lookup"><span data-stu-id="60630-169">If alias is not specified, it will be inferred from the `<collection_expression>` using following rules:</span></span>  
  
-   <span data-ttu-id="60630-170">Se a expressão for um collection_name, collection_name será usado como um alias.</span><span class="sxs-lookup"><span data-stu-id="60630-170">If the expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
-   <span data-ttu-id="60630-171">Se a expressão for `<collection_expression>`, property_name e, em seguida, property_name serão usados como alias.</span><span class="sxs-lookup"><span data-stu-id="60630-171">If the expression is `<collection_expression>`, then property_name, then property_name will be used as an alias.</span></span> <span data-ttu-id="60630-172">Se a expressão for um collection_name, collection_name será usado como um alias.</span><span class="sxs-lookup"><span data-stu-id="60630-172">If the expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
<span data-ttu-id="60630-173">AS `input_alias`</span><span class="sxs-lookup"><span data-stu-id="60630-173">AS `input_alias`</span></span>  
  
<span data-ttu-id="60630-174">Especifica que `input_alias` é um conjunto de valores retornados pela expressão de coleção subjacente.</span><span class="sxs-lookup"><span data-stu-id="60630-174">Specifies that the `input_alias` is a set of values returned by the underlying collection expression.</span></span>  
 
<span data-ttu-id="60630-175">`input_alias` IN</span><span class="sxs-lookup"><span data-stu-id="60630-175">`input_alias` IN</span></span>  
  
<span data-ttu-id="60630-176">Especifica que o `input_alias` deve representar o conjunto de valores obtidos pela iteração em todos os elementos da matriz de cada matriz retornada pela expressão de coleção subjacente.</span><span class="sxs-lookup"><span data-stu-id="60630-176">Specifies that the `input_alias` should represent the set of values obtained by iterating over all array elements of each array returned by the underlying collection expression.</span></span> <span data-ttu-id="60630-177">Qualquer valor retornado pela expressão de coleção subjacente que não seja uma matriz é ignorado.</span><span class="sxs-lookup"><span data-stu-id="60630-177">Any value returned by underlying collection expression that is not an array is ignored.</span></span>  
  
`<collection_expression>`  
  
<span data-ttu-id="60630-178">Especifica a expressão de coleção a ser usada para recuperar os documentos.</span><span class="sxs-lookup"><span data-stu-id="60630-178">Specifies the collection expression to be used to retrieve the documents.</span></span>  
  
`ROOT`  
  
<span data-ttu-id="60630-179">Especifica que documento deve ser recuperado da coleção padrão conectada no momento.</span><span class="sxs-lookup"><span data-stu-id="60630-179">Specifies that document should be retrieved from the default, currently connected collection.</span></span>  
  
`collection_name`  
  
<span data-ttu-id="60630-180">Especifica que documento deve ser recuperado da coleção fornecida.</span><span class="sxs-lookup"><span data-stu-id="60630-180">Specifies that document should be retrieved from the provided collection.</span></span> <span data-ttu-id="60630-181">O nome da coleção deve corresponder ao nome da coleção conectada no momento.</span><span class="sxs-lookup"><span data-stu-id="60630-181">The name of the collection must match the name of the collection currently connected to.</span></span>  
  
`input_alias`  
  
<span data-ttu-id="60630-182">Especifica que documento deve ser recuperado de outra fonte definida pelo alias fornecido.</span><span class="sxs-lookup"><span data-stu-id="60630-182">Specifies that document should be retrieved from the other source defined by the provided alias.</span></span>  
  
`<collection_expression> '.' property_`  
  
<span data-ttu-id="60630-183">Especifica que documento deve ser recuperado acessando a propriedade `property_name` ou o elemento de matriz array_index para todos os documentos recuperados pela expressão de coleção especificada.</span><span class="sxs-lookup"><span data-stu-id="60630-183">Specifies that document should be retrieved by accessing the `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
`<collection_expression> '[' "property_name" | array_index ']'`  
  
<span data-ttu-id="60630-184">Especifica que documento deve ser recuperado acessando a propriedade `property_name` ou o elemento de matriz array_index para todos os documentos recuperados pela expressão de coleção especificada.</span><span class="sxs-lookup"><span data-stu-id="60630-184">Specifies that document should be retrieved by accessing the `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
<span data-ttu-id="60630-185">**Comentários**</span><span class="sxs-lookup"><span data-stu-id="60630-185">**Remarks**</span></span>  
  
<span data-ttu-id="60630-186">Todos os aliases fornecidos ou inferidos nos `<from_source>(`s) devem ser exclusivos.</span><span class="sxs-lookup"><span data-stu-id="60630-186">All aliases provided or inferred in the `<from_source>(`s) must be unique.</span></span> <span data-ttu-id="60630-187">A sintaxe de `<collection_expression>.`property_name é a mesma de `<collection_expression>' ['"property_name"']'`.</span><span class="sxs-lookup"><span data-stu-id="60630-187">The Syntax `<collection_expression>.`property_name is the same as `<collection_expression>' ['"property_name"']'`.</span></span> <span data-ttu-id="60630-188">No entanto, a sintaxe desta última pode ser usada se um nome de propriedade contém um caractere não identificador.</span><span class="sxs-lookup"><span data-stu-id="60630-188">However, the latter syntax can be used if a property name contains a non-identifier characters.</span></span>  
  
<span data-ttu-id="60630-189">**Propriedades ausentes, elementos de matriz ausentes, tratamento de valores indefinidos**</span><span class="sxs-lookup"><span data-stu-id="60630-189">**Missing properties, missing array elements, undefined values handling**</span></span>  
  
<span data-ttu-id="60630-190">Se uma expressão de coleção acessar propriedades ou elementos da matriz e o valor não existir, esse valor será ignorado e não processado.</span><span class="sxs-lookup"><span data-stu-id="60630-190">If a collection expression accesses properties or array elements and that value does not exist, that value will be ignored and not processed further.</span></span>  
  
<span data-ttu-id="60630-191">**Escopo de contexto de expressão de coleção**</span><span class="sxs-lookup"><span data-stu-id="60630-191">**Collection expression context scoping**</span></span>  
  
<span data-ttu-id="60630-192">Uma expressão de coleção pode ser coleção com escopo ou documento com escopo:</span><span class="sxs-lookup"><span data-stu-id="60630-192">A collection expression may be collection-scoped or document-scoped:</span></span>  
  
-   <span data-ttu-id="60630-193">Uma expressão é coleção com escopo se a fonte subjacente da expressão de coleção é ROOT ou `collection_name`.</span><span class="sxs-lookup"><span data-stu-id="60630-193">An expression is collection-scoped, if the underlying source of the collection expression is either ROOT or `collection_name`.</span></span> <span data-ttu-id="60630-194">Essa expressão representa um conjunto de documentos recuperados diretamente da coleção e não depende de processamento de outras expressões de coleção.</span><span class="sxs-lookup"><span data-stu-id="60630-194">Such an expression represents a set of documents retrieved from the collection directly, and is not dependent on the processing of other collection expressions.</span></span>  
  
-   <span data-ttu-id="60630-195">Uma expressão tem escopo de documento se a fonte subjacente da expressão de coleção é um `input_alias` introduzido anteriormente na consulta.</span><span class="sxs-lookup"><span data-stu-id="60630-195">An expression is document-scoped, if the underlying source of the collection expression is `input_alias` introduced earlier in the query.</span></span> <span data-ttu-id="60630-196">Essa expressão representa um conjunto de documentos obtidos avaliando a expressão de coleção no escopo de cada documento pertencente ao conjunto associado à coleção de alias.</span><span class="sxs-lookup"><span data-stu-id="60630-196">Such an expression represents a set of documents obtained by evaluating the collection expression in the scope of each document belonging to the set associated with the aliased collection.</span></span>  <span data-ttu-id="60630-197">O conjunto resultante será uma união de conjuntos obtidos pela avaliação da expressão de coleção para cada um dos documentos no conjunto subjacente.</span><span class="sxs-lookup"><span data-stu-id="60630-197">The resulting set will be a union of sets obtained by evaluating the collection expression for each of the documents in the underlying set.</span></span>  
  
<span data-ttu-id="60630-198">**Junções**</span><span class="sxs-lookup"><span data-stu-id="60630-198">**Joins**</span></span>  
  
<span data-ttu-id="60630-199">Na versão atual, o BD Cosmos do Azure dá suporte a junções internas.</span><span class="sxs-lookup"><span data-stu-id="60630-199">In the current release, Azure Cosmos DB supports inner joins.</span></span> <span data-ttu-id="60630-200">Recursos adicionais de junção serão disponibilizados em breve.</span><span class="sxs-lookup"><span data-stu-id="60630-200">Additional join capabilities are forthcoming.</span></span>

<span data-ttu-id="60630-201">Junções internas resultam em um produto completo cruzando os conjuntos associados à junção.</span><span class="sxs-lookup"><span data-stu-id="60630-201">Inner joins result in a complete cross product of the sets participating in the join.</span></span> <span data-ttu-id="60630-202">O resultado de uma junção de N maneiras é um conjunto de tuplas com N elementos, em que cada valor na tupla é associado ao alias do conjunto membro da junção e pode ser acessado pela referência desse alias em outras cláusulas.</span><span class="sxs-lookup"><span data-stu-id="60630-202">The result of an N-way join is a set of N-element tuples, where each value in the tuple is associated with the aliased set participating in the join and can be accessed by referencing that alias in other clauses.</span></span>  
  
<span data-ttu-id="60630-203">A avaliação da junção depende do escopo de contexto dos conjuntos participantes:</span><span class="sxs-lookup"><span data-stu-id="60630-203">The evaluation of the join depends on the context scope of the participating sets:</span></span>  
  
-  <span data-ttu-id="60630-204">Uma junção entre um conjunto de coleção A e o conjunto de coleção com escopo definido B resulta em um produto cruzado de todos os elementos nos conjuntos A e B.</span><span class="sxs-lookup"><span data-stu-id="60630-204">A join between collection-set A and collection-scoped set B, results in a cross product of all elements in sets A and B.</span></span>
  
-   <span data-ttu-id="60630-205">Uma associação entre o conjunto A e o conjunto com escopo de documento B resulta em uma união de todos os conjuntos obtidos pela avaliação do conjunto com escopo de documento B para cada documento do conjunto A.</span><span class="sxs-lookup"><span data-stu-id="60630-205">A join between set A and document-scoped set B, results in a union of all sets obtained by evaluating document-scoped set B for each document from set A.</span></span>  
  
 <span data-ttu-id="60630-206">Na versão atual, há suporte para, no máximo, uma expressão com escopo de coleção pelo processador de consulta.</span><span class="sxs-lookup"><span data-stu-id="60630-206">In the current release, a maximum of one collection-scoped expression is supported by the query processor.</span></span>  
  
<span data-ttu-id="60630-207">**Exemplos de junções:**</span><span class="sxs-lookup"><span data-stu-id="60630-207">**Examples of joins:**</span></span>  
  
<span data-ttu-id="60630-208">Vamos começar com a seguinte cláusula FROM: `<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span><span class="sxs-lookup"><span data-stu-id="60630-208">Let's look at the following FROM clause: `<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span></span>  
  
 <span data-ttu-id="60630-209">Permite que cada fonte defina `input_alias1, input_alias2, …, input_aliasN`.</span><span class="sxs-lookup"><span data-stu-id="60630-209">Let each source define `input_alias1, input_alias2, …, input_aliasN`.</span></span> <span data-ttu-id="60630-210">Essa cláusula FROM retorna um conjunto de tuplas N (tupla com valores N).</span><span class="sxs-lookup"><span data-stu-id="60630-210">This FROM clause returns a set of N-tuples (tuple with N values).</span></span> <span data-ttu-id="60630-211">Cada tupla terá os valores produzidos pela iteração de todos os alias da coleção em seus respectivos conjuntos.</span><span class="sxs-lookup"><span data-stu-id="60630-211">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span>  
  
<span data-ttu-id="60630-212">*JUNÇÃO exemplo 1, com 2 fontes:*</span><span class="sxs-lookup"><span data-stu-id="60630-212">*JOIN example 1, with 2 sources:*</span></span>  
  
- <span data-ttu-id="60630-213">Permite que `<from_source1>` tenha escopo de coleção e represente o conjunto {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="60630-213">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="60630-214">Permite que `<from_source2>` tenha escopo de documento, referenciando input_alias1 e represente os conjuntos:</span><span class="sxs-lookup"><span data-stu-id="60630-214">Let `<from_source2>` be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="60630-215">{1,2} para `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="60630-215">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="60630-216">{3} para`input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="60630-216">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="60630-217">{4,5} para`input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="60630-217">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="60630-218">A cláusula FROM `<from_source1> JOIN <from_source2>` resultará nas tuplas abaixo:</span><span class="sxs-lookup"><span data-stu-id="60630-218">The FROM clause `<from_source1> JOIN <from_source2>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="60630-219">(`input_alias1, input_alias2`):</span><span class="sxs-lookup"><span data-stu-id="60630-219">(`input_alias1, input_alias2`):</span></span>  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
<span data-ttu-id="60630-220">*JUNÇÃO exemplo 2, com 3 fontes:*</span><span class="sxs-lookup"><span data-stu-id="60630-220">*JOIN example 2, with 3 sources:*</span></span>  
  
- <span data-ttu-id="60630-221">Permite que `<from_source1>` tenha escopo de coleção e represente o conjunto {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="60630-221">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="60630-222">Permite que `<from_source2>` tenha escopo de documento, referenciando `input_alias1` e represente os conjuntos:</span><span class="sxs-lookup"><span data-stu-id="60630-222">Let `<from_source2>` be document-scoped referencing `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="60630-223">{1,2} para `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="60630-223">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="60630-224">{3} para`input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="60630-224">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="60630-225">{4,5} para`input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="60630-225">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="60630-226">Permite que `<from_source3>` tenha escopo de documento, referenciando `input_alias2` e represente os conjuntos:</span><span class="sxs-lookup"><span data-stu-id="60630-226">Let `<from_source3>` be document-scoped referencing `input_alias2` and represent sets:</span></span>  
  
    <span data-ttu-id="60630-227">{100, 200} para`input_alias2 = 1,`</span><span class="sxs-lookup"><span data-stu-id="60630-227">{100, 200} for `input_alias2 = 1,`</span></span>  
  
    <span data-ttu-id="60630-228">{300} para`input_alias2 = 3,`</span><span class="sxs-lookup"><span data-stu-id="60630-228">{300} for `input_alias2 = 3,`</span></span>  
  
- <span data-ttu-id="60630-229">A cláusula FROM `<from_source1> JOIN <from_source2> JOIN <from_source3>` resultará nas tuplas abaixo:</span><span class="sxs-lookup"><span data-stu-id="60630-229">The FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="60630-230">(input_alias1, input_alias2, input_alias3):</span><span class="sxs-lookup"><span data-stu-id="60630-230">(input_alias1, input_alias2, input_alias3):</span></span>  
  
    <span data-ttu-id="60630-231">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span><span class="sxs-lookup"><span data-stu-id="60630-231">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="60630-232">Falta de tuplas para outros valores de `input_alias1`, `input_alias2`, para os quais `<from_source3>` não retornou nenhum valor.</span><span class="sxs-lookup"><span data-stu-id="60630-232">Lack of tuples for other values of `input_alias1`, `input_alias2`, for which the `<from_source3>` did not return any values.</span></span>  
  
<span data-ttu-id="60630-233">*JUNÇÃO exemplo 3, com 3 fontes:*</span><span class="sxs-lookup"><span data-stu-id="60630-233">*JOIN example 3, with 3 sources:*</span></span>  
  
- <span data-ttu-id="60630-234">Permite que <from_source1> tenha escopo de coleção e represente o conjunto {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="60630-234">Let <from_source1> be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="60630-235">Permite que `<from_source1>` tenha escopo de coleção e represente o conjunto {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="60630-235">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="60630-236">Permite que <from_source2> tenha escopo de documento, referenciando input_alias1 e represente os conjuntos:</span><span class="sxs-lookup"><span data-stu-id="60630-236">Let <from_source2> be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="60630-237">{1,2} para `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="60630-237">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="60630-238">{3} para`input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="60630-238">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="60630-239">{4,5} para`input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="60630-239">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="60630-240">Permite que `<from_source3>` tenha escopo `input_alias1` e represente os conjuntos:</span><span class="sxs-lookup"><span data-stu-id="60630-240">Let `<from_source3>` be scoped to `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="60630-241">{100, 200} para`input_alias2 = A,`</span><span class="sxs-lookup"><span data-stu-id="60630-241">{100, 200} for `input_alias2 = A,`</span></span>  
  
    <span data-ttu-id="60630-242">{300} para`input_alias2 = C,`</span><span class="sxs-lookup"><span data-stu-id="60630-242">{300} for `input_alias2 = C,`</span></span>  
  
- <span data-ttu-id="60630-243">A cláusula FROM `<from_source1> JOIN <from_source2> JOIN <from_source3>` resultará nas tuplas abaixo:</span><span class="sxs-lookup"><span data-stu-id="60630-243">The FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in the following tuples:</span></span>  
  
    <span data-ttu-id="60630-244">(`input_alias1, input_alias2, input_alias3`):</span><span class="sxs-lookup"><span data-stu-id="60630-244">(`input_alias1, input_alias2, input_alias3`):</span></span>  
  
    <span data-ttu-id="60630-245">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) , (C, 5, 300)</span><span class="sxs-lookup"><span data-stu-id="60630-245">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="60630-246">Isso resultou em produto cruzado entre `<from_source2>` e `<from_source3>` porque ambos têm o escopo para a mesma `<from_source1>`.</span><span class="sxs-lookup"><span data-stu-id="60630-246">This resulted in cross product between `<from_source2>` and `<from_source3>` because both are scoped to the same `<from_source1>`.</span></span>  <span data-ttu-id="60630-247">Isso resultou em 4 (2 x 2) tuplas com valor A, 0 tuplas com valor B (1 x 0) e 2 (2 x 1) tuplas com valor C.</span><span class="sxs-lookup"><span data-stu-id="60630-247">This resulted in 4 (2x2) tuples having value A, 0 tuples having value B (1x0) and 2 (2x1) tuples having value C.</span></span>  
  
<span data-ttu-id="60630-248">**Consulte também**</span><span class="sxs-lookup"><span data-stu-id="60630-248">**See also**</span></span>  
  
 [<span data-ttu-id="60630-249">Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="60630-249">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="60630-250"><a name="bk_where_clause"></a> Cláusula WHERE</span><span class="sxs-lookup"><span data-stu-id="60630-250"><a name="bk_where_clause"></a> WHERE clause</span></span>  
 <span data-ttu-id="60630-251">Especifica o critério de pesquisa para os documentos retornados pela consulta.</span><span class="sxs-lookup"><span data-stu-id="60630-251">Specifies the search condition for the documents returned by the query.</span></span>  
  
 <span data-ttu-id="60630-252">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-252">**Syntax**</span></span>  
  
```  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 <span data-ttu-id="60630-253">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-253">**Arguments**</span></span>  
  
-   `<filter_condition>`  
  
     <span data-ttu-id="60630-254">Especifica a condição a ser atendida para que os documentos sejam retornados.</span><span class="sxs-lookup"><span data-stu-id="60630-254">Specifies the condition to be met for the documents to be returned.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="60630-255">Expressão que representa o valor a ser calculado.</span><span class="sxs-lookup"><span data-stu-id="60630-255">Expression representing the value to be computed.</span></span> <span data-ttu-id="60630-256">Consulte a seção [Expressões escalares](#bk_scalar_expressions) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="60630-256">See the [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
 <span data-ttu-id="60630-257">**Comentários**</span><span class="sxs-lookup"><span data-stu-id="60630-257">**Remarks**</span></span>  
  
 <span data-ttu-id="60630-258">Para que o documento seja retornado, uma expressão especificada como condição de filtro deve ser avaliada como verdadeira.</span><span class="sxs-lookup"><span data-stu-id="60630-258">In order for the document to be returned an expression specified as filter condition must evaluate to true.</span></span> <span data-ttu-id="60630-259">Somente o valor booliano verdadeiro atenderá à condição. Nenhum outro valor, seja indefinido, nulo, falso, número, matriz ou objeto, atenderá à condição.</span><span class="sxs-lookup"><span data-stu-id="60630-259">Only Boolean value true will satisfy the condition, any other value: undefined, null, false, Number, Array or Object will not satisfy the condition.</span></span>  
  
##  <span data-ttu-id="60630-260"><a name="bk_orderby_clause"></a> Cláusula ORDER BY</span><span class="sxs-lookup"><span data-stu-id="60630-260"><a name="bk_orderby_clause"></a> ORDER BY clause</span></span>  
 <span data-ttu-id="60630-261">Especifica a ordem de classificação para resultados retornados pela consulta.</span><span class="sxs-lookup"><span data-stu-id="60630-261">Specifies the sorting order for results returned by the query.</span></span>  
  
 <span data-ttu-id="60630-262">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-262">**Syntax**</span></span>  
  
```  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 <span data-ttu-id="60630-263">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-263">**Arguments**</span></span>  
  
-   `<sort_specification>`  
  
     <span data-ttu-id="60630-264">Especifica uma propriedade ou expressão pela qual classificar o conjunto de resultados da consulta.</span><span class="sxs-lookup"><span data-stu-id="60630-264">Specifies a property or expression on which to sort the query result set.</span></span> <span data-ttu-id="60630-265">Uma coluna de classificação pode ser especificada como um alias de nome ou coluna.</span><span class="sxs-lookup"><span data-stu-id="60630-265">A sort column can be specified as a name or column alias.</span></span>  
  
     <span data-ttu-id="60630-266">Várias colunas de classificação podem ser especificadas.</span><span class="sxs-lookup"><span data-stu-id="60630-266">Multiple sort columns can be specified.</span></span> <span data-ttu-id="60630-267">Os nomes de coluna devem ser exclusivos.</span><span class="sxs-lookup"><span data-stu-id="60630-267">Column names must be unique.</span></span> <span data-ttu-id="60630-268">A sequência das colunas de classificação na cláusula ORDER BY define a organização do conjunto de resultados classificado.</span><span class="sxs-lookup"><span data-stu-id="60630-268">The sequence of the sort columns in the ORDER BY clause defines the organization of the sorted result set.</span></span> <span data-ttu-id="60630-269">Ou seja, o conjunto de resultados é classificado pela primeira propriedade e, em seguida, essa lista ordenada é classificada pela segunda propriedade e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="60630-269">That is, the result set is sorted by the first property and then that ordered list is sorted by the second property, and so on.</span></span>  
  
     <span data-ttu-id="60630-270">Os nomes de coluna referenciados na cláusula ORDER BY devem corresponder a uma coluna na lista de seleção ou a uma coluna definida em uma tabela especificada na cláusula FROM sem nenhuma ambiguidade.</span><span class="sxs-lookup"><span data-stu-id="60630-270">The column names referenced in the ORDER BY clause must correspond to either a column in the select list or to a column defined in a table specified in the FROM clause without any ambiguities.</span></span>  
  
-   `<sort_expression>`  
  
     <span data-ttu-id="60630-271">Especifica uma única propriedade ou expressão na qual classificar o conjunto de resultados da consulta.</span><span class="sxs-lookup"><span data-stu-id="60630-271">Specifies a single property or expression on which to sort the query result set.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="60630-272">Consulte a seção [Expressões escalares](#bk_scalar_expressions) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="60630-272">See the [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
-   `ASC | DESC`  
  
     <span data-ttu-id="60630-273">Especifica que os valores na coluna especificada devem ser classificados em ordem crescente ou decrescente.</span><span class="sxs-lookup"><span data-stu-id="60630-273">Specifies that the values in the specified column should be sorted in ascending or descending order.</span></span> <span data-ttu-id="60630-274">ASC classifica do valor mais baixo para o valor mais alto.</span><span class="sxs-lookup"><span data-stu-id="60630-274">ASC sorts from the lowest value to highest value.</span></span> <span data-ttu-id="60630-275">DESC classifica do valor mais alto para o valor mais baixo.</span><span class="sxs-lookup"><span data-stu-id="60630-275">DESC sorts from highest value to lowest value.</span></span> <span data-ttu-id="60630-276">ASC é a ordem de classificação padrão.</span><span class="sxs-lookup"><span data-stu-id="60630-276">ASC is the default sort order.</span></span> <span data-ttu-id="60630-277">Os valores nulos são tratados como os menores valores possíveis.</span><span class="sxs-lookup"><span data-stu-id="60630-277">Null values are treated as the lowest possible values.</span></span>  
  
 <span data-ttu-id="60630-278">**Comentários**</span><span class="sxs-lookup"><span data-stu-id="60630-278">**Remarks**</span></span>  
  
 <span data-ttu-id="60630-279">Enquanto a gramática de consulta dá suporte a vários pedidos por propriedades, o tempo de execução de consulta do BD Cosmos do Azure dá suporte à classificação apenas em relação a uma única propriedade e somente em relação a nomes de propriedade, ou seja, não em relação a propriedades calculadas.</span><span class="sxs-lookup"><span data-stu-id="60630-279">While the query grammar supports multiple order by properties, the Azure Cosmos DB query runtime supports sorting only against a single property, and only against property names, i.e., not against computed properties.</span></span> <span data-ttu-id="60630-280">A classificação também requer que a política de indexação inclua um índice de intervalo para a propriedade e o tipo especificado, com precisão máxima.</span><span class="sxs-lookup"><span data-stu-id="60630-280">Sorting also requires that the indexing policy includes a range index for the property and the specified type, with the maximum precision.</span></span> <span data-ttu-id="60630-281">Consulte a documentação de política de indexação para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="60630-281">Refer to the indexing policy documentation for more details.</span></span>  
  
##  <span data-ttu-id="60630-282"><a name="bk_scalar_expressions"></a> Expressões escalares</span><span class="sxs-lookup"><span data-stu-id="60630-282"><a name="bk_scalar_expressions"></a> Scalar expressions</span></span>  
 <span data-ttu-id="60630-283">Uma expressão escalar é uma combinação de símbolos e operadores que podem ser avaliados para se obter um único valor.</span><span class="sxs-lookup"><span data-stu-id="60630-283">A scalar expression is a combination of symbols and operators that can be evaluated to obtain a single value.</span></span> <span data-ttu-id="60630-284">Expressões simples podem ser constantes, referências de propriedade, referências de elemento de matriz, referências de alias ou chamadas de função.</span><span class="sxs-lookup"><span data-stu-id="60630-284">Simple expressions can be constants, property references, array element references, alias references, or function calls.</span></span> <span data-ttu-id="60630-285">As expressões simples podem ser combinadas em expressões complexas usando operadores.</span><span class="sxs-lookup"><span data-stu-id="60630-285">Simple expressions can be combined into complex expressions using operators.</span></span>  
  
 <span data-ttu-id="60630-286">Para obter detalhes sobre os valores que a expressão escalar pode ter, consulte a seção [Constantes](#bk_constants).</span><span class="sxs-lookup"><span data-stu-id="60630-286">For details on values which scalar expression may have, see [Constants](#bk_constants) section.</span></span>  
  
 <span data-ttu-id="60630-287">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-287">**Syntax**</span></span>  
  
```  
<scalar_expression> ::=  
       <constant>   
     | input_alias   
     | parameter_name  
     | <scalar_expression>.property_name  
     | <scalar_expression>'['"property_name"|array_index']'  
     | unary_operator <scalar_expression>  
     | <scalar_expression> binary_operator <scalar_expression>    
     | <scalar_expression> ? <scalar_expression> : <scalar_expression>  
     | <scalar_function_expression>  
     | <create_object_expression>   
     | <create_array_expression>  
     | (<scalar_expression>)   
  
<scalar_function_expression> ::=  
        'udf.' Udf_scalar_function([<scalar_expression>][,…n])  
        | builtin_scalar_function([<scalar_expression>][,…n])  
  
<create_object_expression> ::=  
   '{' [{property_name | "property_name"} : <scalar_expression>][,…n] '}'  
  
<create_array_expression> ::=  
   '[' [<scalar_expression>][,…n] ']'  
  
```  
  
 <span data-ttu-id="60630-288">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-288">**Arguments**</span></span>  
  
-   `<constant>`  
  
     <span data-ttu-id="60630-289">Representa um valor constante.</span><span class="sxs-lookup"><span data-stu-id="60630-289">Represents a constant value.</span></span> <span data-ttu-id="60630-290">Consulte a seção [Constantes](#bk_constants) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="60630-290">See [Constants](#bk_constants) section for details.</span></span>  
  
-   `input_alias`  
  
     <span data-ttu-id="60630-291">Representa um valor definido pelo `input_alias` introduzido na cláusula `FROM`.</span><span class="sxs-lookup"><span data-stu-id="60630-291">Represents a value defined by the `input_alias` introduced in the `FROM` clause.</span></span>  
    <span data-ttu-id="60630-292">Esse valor é garantidamente diferente de **indefinido**; os valores **indefinidos** na entrada são ignorados.</span><span class="sxs-lookup"><span data-stu-id="60630-292">This value is guaranteed to not be **undefined** –**undefined** values in the input are skipped.</span></span>  
  
-   `<scalar_expression>.property_name`  
  
     <span data-ttu-id="60630-293">Representa um valor da propriedade de um objeto.</span><span class="sxs-lookup"><span data-stu-id="60630-293">Represents a value of the property of an object.</span></span> <span data-ttu-id="60630-294">Se a propriedade não existe ou é referenciada em um valor que não é um objeto, a expressão é avaliada como valor **indefinido**.</span><span class="sxs-lookup"><span data-stu-id="60630-294">If the property does not exist or property is referenced on a value which is not an object, then the expression evaluates to **undefined** value.</span></span>  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     <span data-ttu-id="60630-295">Representa um valor da propriedade com nome `property_name` ou elemento de matriz com índice `array_index` de um objeto ou uma matriz.</span><span class="sxs-lookup"><span data-stu-id="60630-295">Represents a value of the property with name `property_name` or array element with index `array_index` of an object/array.</span></span> <span data-ttu-id="60630-296">Se o índice de matriz/propriedade não existe ou é referenciado em um valor que não é um objeto ou uma matriz, a expressão é avaliada como valor indefinido.</span><span class="sxs-lookup"><span data-stu-id="60630-296">If the property/array index does not exist or the property/array index is referenced on a value which is not an object/array, then the expression evaluates to undefined value.</span></span>  
  
-   `unary_operator <scalar_expression>`  
  
     <span data-ttu-id="60630-297">Representa um operador que é aplicado a um único valor.</span><span class="sxs-lookup"><span data-stu-id="60630-297">Represents an operator that is applied to a single value.</span></span> <span data-ttu-id="60630-298">Consulte a seção [Operadores](#bk_operators) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="60630-298">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     <span data-ttu-id="60630-299">Representa um operador que é aplicado a dois valores.</span><span class="sxs-lookup"><span data-stu-id="60630-299">Represents an operator that is applied to two values.</span></span> <span data-ttu-id="60630-300">Consulte a seção [Operadores](#bk_operators) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="60630-300">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_function_expression>`  
  
     <span data-ttu-id="60630-301">Representa um valor definido por um resultado de uma chamada de função.</span><span class="sxs-lookup"><span data-stu-id="60630-301">Represents a value defined by a result of a function call.</span></span>  
  
-   `udf_scalar_function`  
  
     <span data-ttu-id="60630-302">Nome da função escalar definida pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="60630-302">Name of the user defined scalar function.</span></span>  
  
-   `builtin_scalar_function`  
  
     <span data-ttu-id="60630-303">Nome da função escalar interna.</span><span class="sxs-lookup"><span data-stu-id="60630-303">Name of the built-in scalar function.</span></span>  
  
-   `<create_object_expression>`  
  
     <span data-ttu-id="60630-304">Representa um valor obtido pela criação de um novo objeto com propriedades especificadas e seus valores.</span><span class="sxs-lookup"><span data-stu-id="60630-304">Represents a value obtained by creating a new object with specified properties and their values.</span></span>  
  
-   `<create_array_expression>`  
  
     <span data-ttu-id="60630-305">Representa um valor obtido pela criação de uma nova matriz com valores especificados como elementos</span><span class="sxs-lookup"><span data-stu-id="60630-305">Represents a value obtained by creating a new array with specified values as elements</span></span>  
  
-   `parameter_name`  
  
     <span data-ttu-id="60630-306">Representa um valor do nome de parâmetro especificado.</span><span class="sxs-lookup"><span data-stu-id="60630-306">Represents a value of the specified parameter name.</span></span> <span data-ttu-id="60630-307">Os nomes de parâmetro devem ter uma única @ como primeiro caractere.</span><span class="sxs-lookup"><span data-stu-id="60630-307">Parameter names must have a single @ as the first character.</span></span>  
  
 <span data-ttu-id="60630-308">**Comentários**</span><span class="sxs-lookup"><span data-stu-id="60630-308">**Remarks**</span></span>  
  
 <span data-ttu-id="60630-309">Ao chamar uma função escalar interna ou definida pelo usuário, todos os argumentos deverão ser definidos.</span><span class="sxs-lookup"><span data-stu-id="60630-309">When calling a built-in or user defined scalar function all arguments must be defined.</span></span> <span data-ttu-id="60630-310">Se um dos argumentos for indefinido, a função não será chamada e o resultado será indefinido.</span><span class="sxs-lookup"><span data-stu-id="60630-310">If any of the arguments is undefined, the function will not be called and the result will be undefined.</span></span>  
  
 <span data-ttu-id="60630-311">Ao criar um objeto, as propriedades a que forem atribuídas um valor indefinido serão ignoradas e não serão incluídas no objeto criado.</span><span class="sxs-lookup"><span data-stu-id="60630-311">When creating an object, any property that is assigned undefined value will be skipped and not included in the created object.</span></span>  
  
 <span data-ttu-id="60630-312">Ao criar uma matriz, os valores de elemento a que forem atribuídos um valor **indefinido** serão ignorados e não serão incluídos no objeto criado.</span><span class="sxs-lookup"><span data-stu-id="60630-312">When creating an array, any element value that is assigned **undefined** value will be skipped and not included in the created object.</span></span> <span data-ttu-id="60630-313">Isso fará com que o próximo elemento definido assuma o seu lugar, de forma que a matriz criada não tenha índices ignorados.</span><span class="sxs-lookup"><span data-stu-id="60630-313">This will cause the next defined element to take its place in such a way that the created array will not have skipped indexes.</span></span>  
  
##  <span data-ttu-id="60630-314"><a name="bk_operators"></a> Operadores</span><span class="sxs-lookup"><span data-stu-id="60630-314"><a name="bk_operators"></a> Operators</span></span>  
 <span data-ttu-id="60630-315">Esta seção descreve os operadores com suporte.</span><span class="sxs-lookup"><span data-stu-id="60630-315">This section describes the supported operators.</span></span> <span data-ttu-id="60630-316">Cada operador pode ser atribuído a exatamente uma categoria.</span><span class="sxs-lookup"><span data-stu-id="60630-316">Each operator can be assigned to exactly one category.</span></span>  
  
 <span data-ttu-id="60630-317">Consulte a tabela **Categorias de operador** abaixo para obter detalhes sobre o tratamento de valores **indefinidos**, requisitos de tipo para valores de entrada e tratamento de valores com tipos não correspondentes.</span><span class="sxs-lookup"><span data-stu-id="60630-317">See **Operator categories** table below, for details regarding handling of **undefined** values, type requirements for input values and handling of values with not matching types.</span></span>  
  
 <span data-ttu-id="60630-318">**Categorias de operador:**</span><span class="sxs-lookup"><span data-stu-id="60630-318">**Operator categories:**</span></span>  
  
|<span data-ttu-id="60630-319">**Categoria**</span><span class="sxs-lookup"><span data-stu-id="60630-319">**Category**</span></span>|<span data-ttu-id="60630-320">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="60630-320">**Details**</span></span>|  
|-|-|  
|<span data-ttu-id="60630-321">**aritmético**</span><span class="sxs-lookup"><span data-stu-id="60630-321">**arithmetic**</span></span>|<span data-ttu-id="60630-322">O operador espera que as entradas sejam números.</span><span class="sxs-lookup"><span data-stu-id="60630-322">Operator expects input(s) to be Number(s).</span></span> <span data-ttu-id="60630-323">A saída também é um número.</span><span class="sxs-lookup"><span data-stu-id="60630-323">Output is also a Number.</span></span> <span data-ttu-id="60630-324">Se qualquer uma das entradas for **indefinido** ou um tipo que não seja número, o resultado será **indefinido**.</span><span class="sxs-lookup"><span data-stu-id="60630-324">If any of the inputs is **undefined** or type other than Number then the result is **undefined**.</span></span>|  
|<span data-ttu-id="60630-325">**bit a bit**</span><span class="sxs-lookup"><span data-stu-id="60630-325">**bitwise**</span></span>|<span data-ttu-id="60630-326">O operador espera que as entradas sejam números inteiros com sinal de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="60630-326">Operator expects input(s) to be 32-bit signed integer Number(s).</span></span> <span data-ttu-id="60630-327">A saída também é um número inteiro com sinal de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="60630-327">Output is also 32-bit signed integer Number.</span></span><br /><br /> <span data-ttu-id="60630-328">Os valores não inteiros serão arredondados.</span><span class="sxs-lookup"><span data-stu-id="60630-328">Any non-integer value will be rounded.</span></span> <span data-ttu-id="60630-329">Os valores positivos serão arredondados para baixo; os valores negativos, arredondados para cima.</span><span class="sxs-lookup"><span data-stu-id="60630-329">Positive value will be rounded down, negative values rounded up.</span></span><br /><br /> <span data-ttu-id="60630-330">Qualquer valor fora do intervalo inteiro de 32 bits será convertido usando-se os últimos 32 bits de notação de complemento do dois.</span><span class="sxs-lookup"><span data-stu-id="60630-330">Any value that is outside of the 32-bit integer range will be converted, by taking last 32-bits of its two's complement notation.</span></span><br /><br /> <span data-ttu-id="60630-331">Se qualquer uma das entradas for **indefinido** ou um tipo que não seja número, o resultado será **indefinido**.</span><span class="sxs-lookup"><span data-stu-id="60630-331">If any of the inputs is **undefined** or type other than Number, then the result is **undefined**.</span></span><br /><br /> <span data-ttu-id="60630-332">**Observação:** o comportamento acima é compatível com o comportamento do operador bit a bit de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="60630-332">**Note:** The above behavior is compatible with JavaScript bitwise operator behavior.</span></span>|  
|<span data-ttu-id="60630-333">**lógico**</span><span class="sxs-lookup"><span data-stu-id="60630-333">**logical**</span></span>|<span data-ttu-id="60630-334">O operador espera que as entradas sejam boolianos.</span><span class="sxs-lookup"><span data-stu-id="60630-334">Operator expects input(s) to be Boolean(s).</span></span> <span data-ttu-id="60630-335">A saída também é um valor booliano.</span><span class="sxs-lookup"><span data-stu-id="60630-335">Output is also a Boolean.</span></span><br /><span data-ttu-id="60630-336">Se qualquer uma das entradas for **indefinido** ou um tipo que não seja booliano, o resultado será **indefinido**.</span><span class="sxs-lookup"><span data-stu-id="60630-336">If any of the inputs is **undefined** or type other than Boolean, then the result will be **undefined**.</span></span>|  
|<span data-ttu-id="60630-337">**comparação**</span><span class="sxs-lookup"><span data-stu-id="60630-337">**comparison**</span></span>|<span data-ttu-id="60630-338">O operador espera que as entradas tenham o mesmo tipo e não sejam indefinidas.</span><span class="sxs-lookup"><span data-stu-id="60630-338">Operator expects input(s) to have the same type and not be undefined.</span></span> <span data-ttu-id="60630-339">A saída é um valor booliano.</span><span class="sxs-lookup"><span data-stu-id="60630-339">Output is a Boolean.</span></span><br /><br /> <span data-ttu-id="60630-340">Se qualquer uma das entradas for **indefinido** ou tiver tipos diferentes, o resultado será **indefinido**.</span><span class="sxs-lookup"><span data-stu-id="60630-340">If any of the inputs is **undefined** or the inputs have different types, then the result is **undefined**.</span></span><br /><br /> <span data-ttu-id="60630-341">Consulte a tabela **Ordenação dos valores para comparação** para ver detalhes da ordem dos valores.</span><span class="sxs-lookup"><span data-stu-id="60630-341">See **Ordering of values for comparison** table for value ordering details.</span></span>|  
|<span data-ttu-id="60630-342">**string**</span><span class="sxs-lookup"><span data-stu-id="60630-342">**string**</span></span>|<span data-ttu-id="60630-343">O operador espera que as entradas sejam cadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="60630-343">Operator expects input(s) to be String(s).</span></span> <span data-ttu-id="60630-344">A saída também é uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="60630-344">Output is also a String.</span></span><br /><span data-ttu-id="60630-345">Se qualquer uma das entradas for **indefinido** ou um tipo que não seja cadeia de caracteres, o resultado será **indefinido**.</span><span class="sxs-lookup"><span data-stu-id="60630-345">If any of the inputs is **undefined** or type other than String then the result is **undefined**.</span></span>|  
  
 <span data-ttu-id="60630-346">**Operadores unários:**</span><span class="sxs-lookup"><span data-stu-id="60630-346">**Unary operators:**</span></span>  
  
|<span data-ttu-id="60630-347">**Nome**</span><span class="sxs-lookup"><span data-stu-id="60630-347">**Name**</span></span>|<span data-ttu-id="60630-348">**Operador**</span><span class="sxs-lookup"><span data-stu-id="60630-348">**Operator**</span></span>|<span data-ttu-id="60630-349">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="60630-349">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="60630-350">**aritmético**</span><span class="sxs-lookup"><span data-stu-id="60630-350">**arithmetic**</span></span>|+<br /><br /> -|<span data-ttu-id="60630-351">Retorna o valor do número.</span><span class="sxs-lookup"><span data-stu-id="60630-351">Returns the number value.</span></span><br /><br /> <span data-ttu-id="60630-352">Negação bit a bit.</span><span class="sxs-lookup"><span data-stu-id="60630-352">Bitwise negation.</span></span> <span data-ttu-id="60630-353">Retorna o valor do número negado.</span><span class="sxs-lookup"><span data-stu-id="60630-353">Returns negated number value.</span></span>|  
|<span data-ttu-id="60630-354">**bit a bit**</span><span class="sxs-lookup"><span data-stu-id="60630-354">**bitwise**</span></span>|~|<span data-ttu-id="60630-355">Complemento de um.</span><span class="sxs-lookup"><span data-stu-id="60630-355">Ones' complement.</span></span> <span data-ttu-id="60630-356">Retorna um complemento de um valor numérico.</span><span class="sxs-lookup"><span data-stu-id="60630-356">Returns a complement of a number value.</span></span>|  
|<span data-ttu-id="60630-357">**Lógico**</span><span class="sxs-lookup"><span data-stu-id="60630-357">**Logical**</span></span>|<span data-ttu-id="60630-358">**NOT**</span><span class="sxs-lookup"><span data-stu-id="60630-358">**NOT**</span></span>|<span data-ttu-id="60630-359">Negação.</span><span class="sxs-lookup"><span data-stu-id="60630-359">Negation.</span></span> <span data-ttu-id="60630-360">Retorna o valor booliano negado.</span><span class="sxs-lookup"><span data-stu-id="60630-360">Returns negated Boolean value.</span></span>|  
  
 <span data-ttu-id="60630-361">**Operadores binários:**</span><span class="sxs-lookup"><span data-stu-id="60630-361">**Binary operators:**</span></span>  
  
|<span data-ttu-id="60630-362">**Nome**</span><span class="sxs-lookup"><span data-stu-id="60630-362">**Name**</span></span>|<span data-ttu-id="60630-363">**Operador**</span><span class="sxs-lookup"><span data-stu-id="60630-363">**Operator**</span></span>|<span data-ttu-id="60630-364">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="60630-364">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="60630-365">**aritmético**</span><span class="sxs-lookup"><span data-stu-id="60630-365">**arithmetic**</span></span>|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|<span data-ttu-id="60630-366">Adição.</span><span class="sxs-lookup"><span data-stu-id="60630-366">Addition.</span></span><br /><br /> <span data-ttu-id="60630-367">Subtração.</span><span class="sxs-lookup"><span data-stu-id="60630-367">Subtraction.</span></span><br /><br /> <span data-ttu-id="60630-368">Multiplicação.</span><span class="sxs-lookup"><span data-stu-id="60630-368">Multiplication.</span></span><br /><br /> <span data-ttu-id="60630-369">Divisão.</span><span class="sxs-lookup"><span data-stu-id="60630-369">Division.</span></span><br /><br /> <span data-ttu-id="60630-370">Modulação.</span><span class="sxs-lookup"><span data-stu-id="60630-370">Modulation.</span></span>|  
|<span data-ttu-id="60630-371">**bit a bit**</span><span class="sxs-lookup"><span data-stu-id="60630-371">**bitwise**</span></span>|<span data-ttu-id="60630-372">&#124;</span><span class="sxs-lookup"><span data-stu-id="60630-372">&#124;</span></span><br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|<span data-ttu-id="60630-373">OR bit a bit.</span><span class="sxs-lookup"><span data-stu-id="60630-373">Bitwise OR.</span></span><br /><br /> <span data-ttu-id="60630-374">AND bit a bit.</span><span class="sxs-lookup"><span data-stu-id="60630-374">Bitwise AND.</span></span><br /><br /> <span data-ttu-id="60630-375">XOR bit a bit.</span><span class="sxs-lookup"><span data-stu-id="60630-375">Bitwise XOR.</span></span><br /><br /> <span data-ttu-id="60630-376">Deslocamento para a esquerda.</span><span class="sxs-lookup"><span data-stu-id="60630-376">Left Shift.</span></span><br /><br /> <span data-ttu-id="60630-377">Deslocamento para a direita.</span><span class="sxs-lookup"><span data-stu-id="60630-377">Right Shift.</span></span><br /><br /> <span data-ttu-id="60630-378">Deslocamento à direita com preenchimento com zero.</span><span class="sxs-lookup"><span data-stu-id="60630-378">Zero-fill Right Shift.</span></span>|  
|<span data-ttu-id="60630-379">**lógico**</span><span class="sxs-lookup"><span data-stu-id="60630-379">**logical**</span></span>|<span data-ttu-id="60630-380">**AND**</span><span class="sxs-lookup"><span data-stu-id="60630-380">**AND**</span></span><br /><br /> <span data-ttu-id="60630-381">**OR**</span><span class="sxs-lookup"><span data-stu-id="60630-381">**OR**</span></span>|<span data-ttu-id="60630-382">Conjunção lógica.</span><span class="sxs-lookup"><span data-stu-id="60630-382">Logical conjunction.</span></span> <span data-ttu-id="60630-383">Retorna **true** se os dois argumentos forem **true**; do contrário, retorna **false**.</span><span class="sxs-lookup"><span data-stu-id="60630-383">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="60630-384">Conjunção lógica.</span><span class="sxs-lookup"><span data-stu-id="60630-384">Logical conjunction.</span></span> <span data-ttu-id="60630-385">Retorna **true** se os dois argumentos forem **true**; do contrário, retorna **false**.</span><span class="sxs-lookup"><span data-stu-id="60630-385">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span>|  
|<span data-ttu-id="60630-386">**comparação**</span><span class="sxs-lookup"><span data-stu-id="60630-386">**comparison**</span></span>|**=**<br /><br /> <span data-ttu-id="60630-387">**!=, <>**</span><span class="sxs-lookup"><span data-stu-id="60630-387">**!=, <>**</span></span><br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> <span data-ttu-id="60630-388">**??**</span><span class="sxs-lookup"><span data-stu-id="60630-388">**??**</span></span>|<span data-ttu-id="60630-389">Igual a.</span><span class="sxs-lookup"><span data-stu-id="60630-389">Equals.</span></span> <span data-ttu-id="60630-390">Retorna **true** se os argumentos forem iguais; do contrário, retorna **false**.</span><span class="sxs-lookup"><span data-stu-id="60630-390">Returns **true** if arguments are equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="60630-391">Não igual a.</span><span class="sxs-lookup"><span data-stu-id="60630-391">Not equal to.</span></span> <span data-ttu-id="60630-392">Retorna **true** se os argumentos não forem iguais; do contrário, retorna **false**.</span><span class="sxs-lookup"><span data-stu-id="60630-392">Returns **true** if arguments are not equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="60630-393">Maior que.</span><span class="sxs-lookup"><span data-stu-id="60630-393">Greater Than.</span></span> <span data-ttu-id="60630-394">Retorna **true** se o primeiro argumento for maior do que o segundo; do contrário, retorna **false**.</span><span class="sxs-lookup"><span data-stu-id="60630-394">Returns **true** if first argument is greater than the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="60630-395">Maior ou igual a.</span><span class="sxs-lookup"><span data-stu-id="60630-395">Greater Than or Equal To.</span></span> <span data-ttu-id="60630-396">Retorna **true** se o primeiro argumento for maior ou igual ao segundo; do contrário, retorna **false**.</span><span class="sxs-lookup"><span data-stu-id="60630-396">Returns **true** if first argument is greater than or equal to the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="60630-397">Menor que.</span><span class="sxs-lookup"><span data-stu-id="60630-397">Less Than.</span></span> <span data-ttu-id="60630-398">Retorna **true** se o primeiro argumento for menor do que o segundo; do contrário, retorna **false**.</span><span class="sxs-lookup"><span data-stu-id="60630-398">Returns **true** if first argument is less than the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="60630-399">Menor ou igual a.</span><span class="sxs-lookup"><span data-stu-id="60630-399">Less Than or Equal To.</span></span> <span data-ttu-id="60630-400">Retorna **true** se o primeiro argumento for menor ou igual ao segundo; do contrário, retorna **false**.</span><span class="sxs-lookup"><span data-stu-id="60630-400">Returns **true** if first argument is less than or equal to the second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="60630-401">Coalesce.</span><span class="sxs-lookup"><span data-stu-id="60630-401">Coalesce.</span></span> <span data-ttu-id="60630-402">Retorna o segundo argumento se o primeiro argumento tem valor **indefinido**.</span><span class="sxs-lookup"><span data-stu-id="60630-402">Returns the second argument if the first argument is an **undefined** value.</span></span>|  
|<span data-ttu-id="60630-403">**Cadeia de caracteres**</span><span class="sxs-lookup"><span data-stu-id="60630-403">**String**</span></span>|<span data-ttu-id="60630-404">**&#124;&#124;**</span><span class="sxs-lookup"><span data-stu-id="60630-404">**&#124;&#124;**</span></span>|<span data-ttu-id="60630-405">Concatenação.</span><span class="sxs-lookup"><span data-stu-id="60630-405">Concatenation.</span></span> <span data-ttu-id="60630-406">Retorna uma concatenação dos dois argumentos.</span><span class="sxs-lookup"><span data-stu-id="60630-406">Returns a concatenation of both arguments.</span></span>|  
  
 <span data-ttu-id="60630-407">**Operadores ternários:**</span><span class="sxs-lookup"><span data-stu-id="60630-407">**Ternary operators:**</span></span>  
  
|<span data-ttu-id="60630-408">Operador ternário</span><span class="sxs-lookup"><span data-stu-id="60630-408">Ternary operator</span></span>|<span data-ttu-id="60630-409">?</span><span class="sxs-lookup"><span data-stu-id="60630-409">?</span></span>|<span data-ttu-id="60630-410">Retorna o segundo argumento se o primeiro argumento é avaliado como **true**; do contrário, retorna o terceiro argumento.</span><span class="sxs-lookup"><span data-stu-id="60630-410">Returns the second argument if the first argument evaluates to **true**; return the third argument otherwise.</span></span>|  
|-|-|-|  
  
 <span data-ttu-id="60630-411">**Ordenação dos valores para comparação**</span><span class="sxs-lookup"><span data-stu-id="60630-411">**Ordering of values for comparison**</span></span>  
  
|<span data-ttu-id="60630-412">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="60630-412">**Type**</span></span>|<span data-ttu-id="60630-413">**Ordem de valores**</span><span class="sxs-lookup"><span data-stu-id="60630-413">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="60630-414">**Indefinido**</span><span class="sxs-lookup"><span data-stu-id="60630-414">**Undefined**</span></span>|<span data-ttu-id="60630-415">Não é comparável.</span><span class="sxs-lookup"><span data-stu-id="60630-415">Not comparable.</span></span>|  
|<span data-ttu-id="60630-416">**Nulo**</span><span class="sxs-lookup"><span data-stu-id="60630-416">**Null**</span></span>|<span data-ttu-id="60630-417">Valor único: **nulo**</span><span class="sxs-lookup"><span data-stu-id="60630-417">Single value: **null**</span></span>|  
|<span data-ttu-id="60630-418">**Número**</span><span class="sxs-lookup"><span data-stu-id="60630-418">**Number**</span></span>|<span data-ttu-id="60630-419">Número real natural.</span><span class="sxs-lookup"><span data-stu-id="60630-419">Natural real number.</span></span><br /><br /> <span data-ttu-id="60630-420">O valor infinito negativo é menor do que qualquer outro valor numérico.</span><span class="sxs-lookup"><span data-stu-id="60630-420">Negative Infinity value is smaller than any other Number value.</span></span><br /><br /> <span data-ttu-id="60630-421">Um valor infinito positivo é maior do que qualquer outro valor numérico. O valor **NaN** não é comparável.</span><span class="sxs-lookup"><span data-stu-id="60630-421">Positive Infinity value is larger than any other Number value.**NaN** value is not comparable.</span></span> <span data-ttu-id="60630-422">A comparação com **NaN** resultará em um valor **indefinido**.</span><span class="sxs-lookup"><span data-stu-id="60630-422">Comparing with **NaN** will result in **undefined** value.</span></span>|  
|<span data-ttu-id="60630-423">**Cadeia de caracteres**</span><span class="sxs-lookup"><span data-stu-id="60630-423">**String**</span></span>|<span data-ttu-id="60630-424">Ordem lexicográfica.</span><span class="sxs-lookup"><span data-stu-id="60630-424">Lexicographical order.</span></span>|  
|<span data-ttu-id="60630-425">**Matriz**</span><span class="sxs-lookup"><span data-stu-id="60630-425">**Array**</span></span>|<span data-ttu-id="60630-426">Nenhuma ordem, mas justa.</span><span class="sxs-lookup"><span data-stu-id="60630-426">No ordering, but equitable.</span></span>|  
|<span data-ttu-id="60630-427">**Objeto**</span><span class="sxs-lookup"><span data-stu-id="60630-427">**Object**</span></span>|<span data-ttu-id="60630-428">Nenhuma ordem, mas justa.</span><span class="sxs-lookup"><span data-stu-id="60630-428">No ordering, but equitable.</span></span>|  
  
 <span data-ttu-id="60630-429">**Comentários**</span><span class="sxs-lookup"><span data-stu-id="60630-429">**Remarks**</span></span>  
  
 <span data-ttu-id="60630-430">No BD Cosmos do Azure, os tipos de valores geralmente não são conhecidos até que sejam realmente recuperados do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="60630-430">In Azure Cosmos DB, the types of values are often not known until they are actually retrieved from the database.</span></span> <span data-ttu-id="60630-431">Para dar suporte à execução de consultas com eficiência, a maioria dos operadores tem requisitos restritos de tipo.</span><span class="sxs-lookup"><span data-stu-id="60630-431">In order to support efficient execution of queries, most of the operators have strict type requirements.</span></span> <span data-ttu-id="60630-432">Além disso, os operadores por si só não executam conversões implícitas.</span><span class="sxs-lookup"><span data-stu-id="60630-432">Also operators by themselves do not perform implicit conversions.</span></span>  
  
 <span data-ttu-id="60630-433">Isso significa que uma consulta como: SELECT * FROM ROOT r WHERE r.Age = 21 retornará apenas documentos com propriedade Age igual ao número 21.</span><span class="sxs-lookup"><span data-stu-id="60630-433">This means that a query like: SELECT * FROM ROOT r WHERE r.Age = 21 will only return documents with property Age equal to the number 21.</span></span> <span data-ttu-id="60630-434">Documentos com propriedade Age igual à cadeia de caracteres "21" ou à cadeia de caracteres "0021" não corresponderão, já que a expressão "21" = 21 é avaliada como indefinida.</span><span class="sxs-lookup"><span data-stu-id="60630-434">Documents with property Age equal to the string "21" or the string "0021" will not match, as the expression "21" = 21 evaluates to undefined.</span></span> <span data-ttu-id="60630-435">Isso permite um melhor uso dos índices, pois a pesquisa de um valor específico (por exemplo, número 21) é mais rápida que a pesquisa de um número indefinido de possíveis correspondências (ou seja, número 21 ou cadeias de caracteres "21", "021", "21,0"...).</span><span class="sxs-lookup"><span data-stu-id="60630-435">This allows for a better use of indexes, because the lookup of a specific value (i.e. number 21) is faster than search for indefinite number of potential matches (i.e. number 21 or strings "21", "021", "21.0" …).</span></span> <span data-ttu-id="60630-436">Isso é diferente de como o JavaScript avalia os operadores em relação a valores de tipos diferentes.</span><span class="sxs-lookup"><span data-stu-id="60630-436">This is different from how JavaScript evaluates operators on values of different types.</span></span>  
  
 <span data-ttu-id="60630-437">**Comparação e igualdade de objetos e matrizes**</span><span class="sxs-lookup"><span data-stu-id="60630-437">**Arrays and objects equality and comparison**</span></span>  
  
 <span data-ttu-id="60630-438">A comparação de valores de objeto ou matriz usando os operadores de intervalo (>, >=, <, <=) resulta em indefinido, pois não tem ordem definida nos valores de objeto ou matriz.</span><span class="sxs-lookup"><span data-stu-id="60630-438">Comparing of Array or Object values using range operators (>, >=, <, <=) will result in undefined as there is not order defined on Object or Array values.</span></span> <span data-ttu-id="60630-439">No entanto, o uso de operadores de igualdade/desigualdade (=,! =, <>) tem suporte e os valores são comparados estruturalmente.</span><span class="sxs-lookup"><span data-stu-id="60630-439">However using equality/inequality operators (=, !=, <>) is supported and values will be compared structurally.</span></span>  
  
 <span data-ttu-id="60630-440">As matrizes são iguais se as duas matrizes têm o mesmo número de elementos e os elementos em posições de correspondência também são iguais.</span><span class="sxs-lookup"><span data-stu-id="60630-440">Arrays are equal if both arrays have same number of elements and elements at matching positions are also equal.</span></span> <span data-ttu-id="60630-441">Se a comparação de qualquer par de elementos resulta em indefinido, o resultado da comparação de matriz é indefinido.</span><span class="sxs-lookup"><span data-stu-id="60630-441">If comparing any pair of elements results in undefined, the result of array comparison is undefined.</span></span>  
  
 <span data-ttu-id="60630-442">Os objetos são iguais se os dois objetos têm as mesmas propriedades definidas e se os valores das propriedades correspondentes também são iguais.</span><span class="sxs-lookup"><span data-stu-id="60630-442">Objects are equal if both objects have same properties defined, and if values of matching properties are also equal.</span></span> <span data-ttu-id="60630-443">Se a comparação de qualquer par de valores de propriedade resulta em indefinido, o resultado da comparação de objetos é indefinido.</span><span class="sxs-lookup"><span data-stu-id="60630-443">If comparing any pair of property values results in undefined, the result of object comparison is undefined.</span></span>  
  
##  <span data-ttu-id="60630-444"><a name="bk_constants"></a> Constantes</span><span class="sxs-lookup"><span data-stu-id="60630-444"><a name="bk_constants"></a> Constants</span></span>  
 <span data-ttu-id="60630-445">Uma constante, também conhecida como valor literal ou escalar, é um símbolo que representa um valor de dados específico.</span><span class="sxs-lookup"><span data-stu-id="60630-445">A constant, also known as a literal or a scalar value, is a symbol that represents a specific data value.</span></span> <span data-ttu-id="60630-446">O formato de uma constante depende do valor que representa o tipo de dados.</span><span class="sxs-lookup"><span data-stu-id="60630-446">The format of a constant depends on the data type of the value it represents.</span></span>  
  
 <span data-ttu-id="60630-447">**Suporte para tipos de dados escalares:**</span><span class="sxs-lookup"><span data-stu-id="60630-447">**Supported scalar data types:**</span></span>  
  
|<span data-ttu-id="60630-448">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="60630-448">**Type**</span></span>|<span data-ttu-id="60630-449">**Ordem de valores**</span><span class="sxs-lookup"><span data-stu-id="60630-449">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="60630-450">**Indefinido**</span><span class="sxs-lookup"><span data-stu-id="60630-450">**Undefined**</span></span>|<span data-ttu-id="60630-451">Valor único: **indefinido**</span><span class="sxs-lookup"><span data-stu-id="60630-451">Single value: **undefined**</span></span>|  
|<span data-ttu-id="60630-452">**Nulo**</span><span class="sxs-lookup"><span data-stu-id="60630-452">**Null**</span></span>|<span data-ttu-id="60630-453">Valor único: **nulo**</span><span class="sxs-lookup"><span data-stu-id="60630-453">Single value: **null**</span></span>|  
|<span data-ttu-id="60630-454">**Booliano**</span><span class="sxs-lookup"><span data-stu-id="60630-454">**Boolean**</span></span>|<span data-ttu-id="60630-455">Valores: **falso**, **verdadeiro**.</span><span class="sxs-lookup"><span data-stu-id="60630-455">Values: **false**, **true**.</span></span>|  
|<span data-ttu-id="60630-456">**Número**</span><span class="sxs-lookup"><span data-stu-id="60630-456">**Number**</span></span>|<span data-ttu-id="60630-457">Um número de ponto flutuante de precisão dupla, padrão IEEE 754.</span><span class="sxs-lookup"><span data-stu-id="60630-457">A double-precision floating-point number, IEEE 754 standard.</span></span>|  
|<span data-ttu-id="60630-458">**Cadeia de caracteres**</span><span class="sxs-lookup"><span data-stu-id="60630-458">**String**</span></span>|<span data-ttu-id="60630-459">Uma sequência de zero ou mais caracteres Unicode.</span><span class="sxs-lookup"><span data-stu-id="60630-459">A sequence of zero or more Unicode characters.</span></span> <span data-ttu-id="60630-460">As cadeias de caracteres devem ser colocadas entre aspas simples ou duplas.</span><span class="sxs-lookup"><span data-stu-id="60630-460">Strings must be enclosed in single or double quotes.</span></span>|  
|<span data-ttu-id="60630-461">**Matriz**</span><span class="sxs-lookup"><span data-stu-id="60630-461">**Array**</span></span>|<span data-ttu-id="60630-462">Uma sequência de zero ou mais elementos.</span><span class="sxs-lookup"><span data-stu-id="60630-462">A sequence of zero or more elements.</span></span> <span data-ttu-id="60630-463">Cada elemento pode ser um valor de qualquer tipo de dados escalares, exceto Indefinido.</span><span class="sxs-lookup"><span data-stu-id="60630-463">Each element can be a value of any scalar data type, except Undefined.</span></span>|  
|<span data-ttu-id="60630-464">**Objeto**</span><span class="sxs-lookup"><span data-stu-id="60630-464">**Object**</span></span>|<span data-ttu-id="60630-465">Um conjunto ordenado de zero ou mais pares de nome/valor.</span><span class="sxs-lookup"><span data-stu-id="60630-465">An unordered set of zero or more name/value pairs.</span></span> <span data-ttu-id="60630-466">Nome é uma cadeia de caracteres Unicode; o valor pode ser de qualquer tipo de dados escalares, exceto **Indefinido**.</span><span class="sxs-lookup"><span data-stu-id="60630-466">Name is a Unicode string, value can be of any scalar data type, except **Undefined**.</span></span>|  
  
 <span data-ttu-id="60630-467">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-467">**Syntax**</span></span>  
  
```  
<constant> ::=  
   <undefined_constant>  
     | <null_constant>   
     | <boolean_constant>   
     | <number_constant>   
     | <string_constant>   
     | <array_constant>   
     | <object_constant>   
  
<undefined_constant> ::= undefined  
  
<null_constant> ::= null  
  
<boolean_constant> ::= false | true  
  
<number_constant> ::= decimal_literal | hexadecimal_literal  
  
<string_constant> ::= string_literal  
  
<array_constant> ::=  
    '[' [<constant>][,...n] ']'  
  
<object_constant> ::=   
   '{' [{property_name | "property_name"} : <constant>][,...n] '}'  
  
```  
  
 <span data-ttu-id="60630-468">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-468">**Arguments**</span></span>  
  
1.  `<undefined_constant>; undefined`  
  
     <span data-ttu-id="60630-469">Representa o valor indefinido do tipo Indefinido.</span><span class="sxs-lookup"><span data-stu-id="60630-469">Represents undefined value of type Undefined.</span></span>  
  
2.  `<null_constant>; null`  
  
     <span data-ttu-id="60630-470">Representa o valor **null** do tipo **Nulo**.</span><span class="sxs-lookup"><span data-stu-id="60630-470">Represents **null** value of type **Null**.</span></span>  
  
3.  `<boolean_constant>`  
  
     <span data-ttu-id="60630-471">Representa a constante do tipo booliano.</span><span class="sxs-lookup"><span data-stu-id="60630-471">Represents constant of type Boolean.</span></span>  
  
4.  `false`  
  
     <span data-ttu-id="60630-472">Representa o valor **false** do tipo booliano.</span><span class="sxs-lookup"><span data-stu-id="60630-472">Represents **false** value of type Boolean.</span></span>  
  
5.  `true`  
  
     <span data-ttu-id="60630-473">Representa o valor **true** do tipo booliano.</span><span class="sxs-lookup"><span data-stu-id="60630-473">Represents **true** value of type Boolean.</span></span>  
  
6.  `<number_constant>`  
  
     <span data-ttu-id="60630-474">Representa uma constante.</span><span class="sxs-lookup"><span data-stu-id="60630-474">Represents a constant.</span></span>  
  
7.  `decimal_literal`  
  
     <span data-ttu-id="60630-475">Os literais decimais são números representados usando notação decimal ou notação científica.</span><span class="sxs-lookup"><span data-stu-id="60630-475">Decimal literals are numbers represented using either decimal notation, or scientific notation.</span></span>  
  
8.  `hexadecimal_literal`  
  
     <span data-ttu-id="60630-476">Os literais hexadecimais são números representados usando o prefixo '0x' seguido por um ou mais dígitos hexadecimais.</span><span class="sxs-lookup"><span data-stu-id="60630-476">Hexadecimal literals are numbers represented using prefix '0x' followed by one or more hexadecimal digits.</span></span>  
  
9. `<string_constant>`  
  
     <span data-ttu-id="60630-477">Representa uma constante do tipo Cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="60630-477">Represents a constant of type String.</span></span>  
  
10. `string _literal`  
  
     <span data-ttu-id="60630-478">Literais de cadeia de caracteres são cadeias de caracteres Unicode representadas por uma sequência de zero ou mais caracteres Unicode ou sequências de escape.</span><span class="sxs-lookup"><span data-stu-id="60630-478">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="60630-479">As literais de cadeia de caracteres são colocadas entre aspas simples (apóstrofe: ') ou aspas duplas (aspas: ").</span><span class="sxs-lookup"><span data-stu-id="60630-479">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span>  
  
 <span data-ttu-id="60630-480">As seguintes sequências de escape são permitidas:</span><span class="sxs-lookup"><span data-stu-id="60630-480">Following escape sequences are allowed:</span></span>  
  
|<span data-ttu-id="60630-481">**Sequência de escape**</span><span class="sxs-lookup"><span data-stu-id="60630-481">**Escape sequence**</span></span>|<span data-ttu-id="60630-482">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="60630-482">**Description**</span></span>|<span data-ttu-id="60630-483">**Caractere Unicode**</span><span class="sxs-lookup"><span data-stu-id="60630-483">**Unicode character**</span></span>|  
|-|-|-|  
|<span data-ttu-id="60630-484">\\'</span><span class="sxs-lookup"><span data-stu-id="60630-484">\\'</span></span>|<span data-ttu-id="60630-485">apóstrofo (')</span><span class="sxs-lookup"><span data-stu-id="60630-485">apostrophe (')</span></span>|<span data-ttu-id="60630-486">U+0027</span><span class="sxs-lookup"><span data-stu-id="60630-486">U+0027</span></span>|  
|<span data-ttu-id="60630-487">\\"</span><span class="sxs-lookup"><span data-stu-id="60630-487">\\"</span></span>|<span data-ttu-id="60630-488">aspas (")</span><span class="sxs-lookup"><span data-stu-id="60630-488">quotation mark (")</span></span>|<span data-ttu-id="60630-489">U+0022</span><span class="sxs-lookup"><span data-stu-id="60630-489">U+0022</span></span>|  
|\\\|<span data-ttu-id="60630-490">barra invertida (\\)</span><span class="sxs-lookup"><span data-stu-id="60630-490">reverse solidus (\\)</span></span>|<span data-ttu-id="60630-491">U+005C</span><span class="sxs-lookup"><span data-stu-id="60630-491">U+005C</span></span>|  
|\\/|<span data-ttu-id="60630-492">barra (/)</span><span class="sxs-lookup"><span data-stu-id="60630-492">solidus (/)</span></span>|<span data-ttu-id="60630-493">U+002F</span><span class="sxs-lookup"><span data-stu-id="60630-493">U+002F</span></span>|  
|<span data-ttu-id="60630-494">\b</span><span class="sxs-lookup"><span data-stu-id="60630-494">\b</span></span>|<span data-ttu-id="60630-495">backspace</span><span class="sxs-lookup"><span data-stu-id="60630-495">backspace</span></span>|<span data-ttu-id="60630-496">U+0008</span><span class="sxs-lookup"><span data-stu-id="60630-496">U+0008</span></span>|  
|<span data-ttu-id="60630-497">\f</span><span class="sxs-lookup"><span data-stu-id="60630-497">\f</span></span>|<span data-ttu-id="60630-498">avanço de página</span><span class="sxs-lookup"><span data-stu-id="60630-498">form feed</span></span>|<span data-ttu-id="60630-499">U+000C</span><span class="sxs-lookup"><span data-stu-id="60630-499">U+000C</span></span>|  
|\n|<span data-ttu-id="60630-500">alimentação de linha</span><span class="sxs-lookup"><span data-stu-id="60630-500">line feed</span></span>|<span data-ttu-id="60630-501">U+000A</span><span class="sxs-lookup"><span data-stu-id="60630-501">U+000A</span></span>|  
|<span data-ttu-id="60630-502">\r</span><span class="sxs-lookup"><span data-stu-id="60630-502">\r</span></span>|<span data-ttu-id="60630-503">retorno de carro</span><span class="sxs-lookup"><span data-stu-id="60630-503">carriage return</span></span>|<span data-ttu-id="60630-504">U+000D</span><span class="sxs-lookup"><span data-stu-id="60630-504">U+000D</span></span>|  
|<span data-ttu-id="60630-505">\t</span><span class="sxs-lookup"><span data-stu-id="60630-505">\t</span></span>|<span data-ttu-id="60630-506">tab</span><span class="sxs-lookup"><span data-stu-id="60630-506">tab</span></span>|<span data-ttu-id="60630-507">U+0009</span><span class="sxs-lookup"><span data-stu-id="60630-507">U+0009</span></span>|  
|<span data-ttu-id="60630-508">\uXXXX</span><span class="sxs-lookup"><span data-stu-id="60630-508">\uXXXX</span></span>|<span data-ttu-id="60630-509">Um caractere Unicode definido por 4 dígitos hexadecimais.</span><span class="sxs-lookup"><span data-stu-id="60630-509">A Unicode character defined by 4 hexadecimal digits.</span></span>|<span data-ttu-id="60630-510">U+XXXX</span><span class="sxs-lookup"><span data-stu-id="60630-510">U+XXXX</span></span>|  
  
##  <span data-ttu-id="60630-511"><a name="bk_query_perf_guidelines"></a>Diretrizes de desempenho de consulta</span><span class="sxs-lookup"><span data-stu-id="60630-511"><a name="bk_query_perf_guidelines"></a> Query performance guidelines</span></span>  
 <span data-ttu-id="60630-512">Para que uma consulta seja executada com eficiência em uma grande coleção, ela deve usar filtros que podem ser oferecidos por um ou mais índices.</span><span class="sxs-lookup"><span data-stu-id="60630-512">In order for a query to be executed efficiently for a large collection, it should use filters which can be served through one or more indexes.</span></span>  
  
 <span data-ttu-id="60630-513">Os seguintes filtros serão considerados para a pesquisa de índice:</span><span class="sxs-lookup"><span data-stu-id="60630-513">The following filters will be considered for index lookup:</span></span>  
  
-   <span data-ttu-id="60630-514">Use o operador de igualdade (=) com uma expressão de caminho de documento e uma constante.</span><span class="sxs-lookup"><span data-stu-id="60630-514">Use equality operator ( = ) with a document path expression and a constant.</span></span>  
  
-   <span data-ttu-id="60630-515">Use o operador de intervalo (<, \<=, >, >=) com uma expressão de caminho de documento e constantes numéricas.</span><span class="sxs-lookup"><span data-stu-id="60630-515">Use range operators (<, \<=, >, >=) with a document path expression and number constants.</span></span>  
  
-   <span data-ttu-id="60630-516">Expressão de caminho de documento significa qualquer expressão que identifica um caminho constante nos documentos da coleção de banco de dados referenciada.</span><span class="sxs-lookup"><span data-stu-id="60630-516">Document path expression stands for any expression which identifies a constant path in the documents from the referenced database collection.</span></span>  
  
 <span data-ttu-id="60630-517">**Expressão de caminho de documento**</span><span class="sxs-lookup"><span data-stu-id="60630-517">**Document path expression**</span></span>  
  
 <span data-ttu-id="60630-518">Expressões de caminho de documento são expressões que um caminho de propriedade ou um indexador de matriz avalia em um documento proveniente dos documentos da coleção do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="60630-518">Document path expressions are expressions that a path of property or array indexer assessors over a document coming from database collection documents.</span></span> <span data-ttu-id="60630-519">Esse caminho pode ser usado para identificar o local dos valores referenciados em um filtro diretamente nos documentos da coleção do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="60630-519">This path can be used to identify the location of values referenced in a filter directly within the documents in the database collection.</span></span>  
  
 <span data-ttu-id="60630-520">Para uma expressão ser considerada uma expressão de caminho de documento, ela deve:</span><span class="sxs-lookup"><span data-stu-id="60630-520">For an expression to be considered a document path expression, it should:</span></span>  
  
1.  <span data-ttu-id="60630-521">Fazer referência diretamente à raiz da coleção.</span><span class="sxs-lookup"><span data-stu-id="60630-521">Reference the collection root directly.</span></span>  
  
2.  <span data-ttu-id="60630-522">Fazer referência ao indexador de matriz da constante ou à propriedade de alguma expressão de caminho de documento</span><span class="sxs-lookup"><span data-stu-id="60630-522">Reference property or constant array indexer of some document path expression</span></span>  
  
3.  <span data-ttu-id="60630-523">Fazer referência a um alias que represente alguma expressão de caminho de documento.</span><span class="sxs-lookup"><span data-stu-id="60630-523">Reference an alias, which represents some document path expression.</span></span>  
  
     <span data-ttu-id="60630-524">**Convenções de sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-524">**Syntax conventions**</span></span>  
  
     <span data-ttu-id="60630-525">A tabela a seguir descreve as convenções usadas para descrever a sintaxe na referência da linguagem de consulta da API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="60630-525">The following table describes the conventions used to describe syntax in the DocumentDB API Query Language reference.</span></span>  
  
    |<span data-ttu-id="60630-526">**Convenção**</span><span class="sxs-lookup"><span data-stu-id="60630-526">**Convention**</span></span>|<span data-ttu-id="60630-527">**Usadas para**</span><span class="sxs-lookup"><span data-stu-id="60630-527">**Used for**</span></span>|  
    |-|-|    
    |<span data-ttu-id="60630-528">LETRAS MAIÚSCULAS</span><span class="sxs-lookup"><span data-stu-id="60630-528">UPPERCASE</span></span>|<span data-ttu-id="60630-529">Palavras-chave não diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="60630-529">Case-insensitive keywords.</span></span>|  
    |<span data-ttu-id="60630-530">letras minúsculas</span><span class="sxs-lookup"><span data-stu-id="60630-530">lowercase</span></span>|<span data-ttu-id="60630-531">Palavras-chave diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="60630-531">Case-sensitive keywords.</span></span>|  
    |<span data-ttu-id="60630-532">\<não terminal></span><span class="sxs-lookup"><span data-stu-id="60630-532">\<nonterminal></span></span>|<span data-ttu-id="60630-533">Não terminal, definido separadamente.</span><span class="sxs-lookup"><span data-stu-id="60630-533">Nonterminal, defined separately.</span></span>|  
    |<span data-ttu-id="60630-534">\<não terminal> ::=</span><span class="sxs-lookup"><span data-stu-id="60630-534">\<nonterminal> ::=</span></span>|<span data-ttu-id="60630-535">Definição de sintaxe do não terminal.</span><span class="sxs-lookup"><span data-stu-id="60630-535">Syntax definition of the nonterminal.</span></span>|  
    |<span data-ttu-id="60630-536">other_terminal</span><span class="sxs-lookup"><span data-stu-id="60630-536">other_terminal</span></span>|<span data-ttu-id="60630-537">Terminal (token), descritos em detalhes em palavras.</span><span class="sxs-lookup"><span data-stu-id="60630-537">Terminal (token), described in detail in words.</span></span>|  
    |<span data-ttu-id="60630-538">identificador</span><span class="sxs-lookup"><span data-stu-id="60630-538">identifier</span></span>|<span data-ttu-id="60630-539">Identificador.</span><span class="sxs-lookup"><span data-stu-id="60630-539">Identifier.</span></span> <span data-ttu-id="60630-540">Permite apenas os seguintes caracteres: a-z A-Z 0-9 _O primeiro caractere não pode ser um dígito.</span><span class="sxs-lookup"><span data-stu-id="60630-540">Allows following characters only: a-z A-Z 0-9 _First character cannot be a digit.</span></span>|  
    |<span data-ttu-id="60630-541">“cadeia de caracteres”</span><span class="sxs-lookup"><span data-stu-id="60630-541">"string"</span></span>|<span data-ttu-id="60630-542">Cadeia de caracteres entre aspas.</span><span class="sxs-lookup"><span data-stu-id="60630-542">Quoted string.</span></span> <span data-ttu-id="60630-543">Permite qualquer cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="60630-543">Allows any valid string.</span></span> <span data-ttu-id="60630-544">Consulte a descrição de um string_literal.</span><span class="sxs-lookup"><span data-stu-id="60630-544">See description of a string_literal.</span></span>|  
    |<span data-ttu-id="60630-545">'símbolo'</span><span class="sxs-lookup"><span data-stu-id="60630-545">'symbol'</span></span>|<span data-ttu-id="60630-546">Símbolo de literal que faz parte da sintaxe.</span><span class="sxs-lookup"><span data-stu-id="60630-546">Literal symbol which is part of the syntax.</span></span>|  
    |<span data-ttu-id="60630-547">&#124; (barra vertical)</span><span class="sxs-lookup"><span data-stu-id="60630-547">&#124; (vertical bar)</span></span>|<span data-ttu-id="60630-548">Alternativas para itens de sintaxe.</span><span class="sxs-lookup"><span data-stu-id="60630-548">Alternatives for syntax items.</span></span> <span data-ttu-id="60630-549">Você pode usar apenas um dos itens especificados.</span><span class="sxs-lookup"><span data-stu-id="60630-549">You can use only one of the items specified.</span></span>|  
    |<span data-ttu-id="60630-550">[ ] /(colchetes)</span><span class="sxs-lookup"><span data-stu-id="60630-550">[ ] /(brackets)</span></span>|<span data-ttu-id="60630-551">Os colchetes colocam um ou mais itens opcionais.</span><span class="sxs-lookup"><span data-stu-id="60630-551">Brackets enclose one or more optional items.</span></span>|  
    |<span data-ttu-id="60630-552">[ ,...n ]</span><span class="sxs-lookup"><span data-stu-id="60630-552">[ ,...n ]</span></span>|<span data-ttu-id="60630-553">Indica que o item precedente pode ser repetido n vezes.</span><span class="sxs-lookup"><span data-stu-id="60630-553">Indicates the preceding item can be repeated n number of times.</span></span> <span data-ttu-id="60630-554">As ocorrências são separadas por vírgulas.</span><span class="sxs-lookup"><span data-stu-id="60630-554">The occurrences are separated by commas.</span></span>|  
    |<span data-ttu-id="60630-555">[ ...n ]</span><span class="sxs-lookup"><span data-stu-id="60630-555">[ ...n ]</span></span>|<span data-ttu-id="60630-556">Indica que o item precedente pode ser repetido n vezes.</span><span class="sxs-lookup"><span data-stu-id="60630-556">Indicates the preceding item can be repeated n number of times.</span></span> <span data-ttu-id="60630-557">As ocorrências são separadas por espaços em branco.</span><span class="sxs-lookup"><span data-stu-id="60630-557">The occurrences are separated by blanks.</span></span>|  
  
##  <span data-ttu-id="60630-558"><a name="bk_built_in_functions"></a> Funções internas</span><span class="sxs-lookup"><span data-stu-id="60630-558"><a name="bk_built_in_functions"></a> Built-in functions</span></span>  
 <span data-ttu-id="60630-559">O BD Cosmos do Azure fornece muitas funções SQL internas.</span><span class="sxs-lookup"><span data-stu-id="60630-559">Azure Cosmos DB provides many built-in SQL functions.</span></span> <span data-ttu-id="60630-560">As categorias de funções internas estão listadas abaixo.</span><span class="sxs-lookup"><span data-stu-id="60630-560">The categories of built-in functions are listed below.</span></span>  
  
|<span data-ttu-id="60630-561">Função</span><span class="sxs-lookup"><span data-stu-id="60630-561">Function</span></span>|<span data-ttu-id="60630-562">Descrição</span><span class="sxs-lookup"><span data-stu-id="60630-562">Description</span></span>|  
|--------------|-----------------|  
|[<span data-ttu-id="60630-563">Funções matemáticas</span><span class="sxs-lookup"><span data-stu-id="60630-563">Mathematical functions</span></span>](#bk_mathematical_functions)|<span data-ttu-id="60630-564">As funções matemáticas executam um cálculo, normalmente com base em valores de entrada que são fornecidos como argumentos, e retornam um valor numérico.</span><span class="sxs-lookup"><span data-stu-id="60630-564">The mathematical functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>|  
|[<span data-ttu-id="60630-565">Funções de verificação de tipo</span><span class="sxs-lookup"><span data-stu-id="60630-565">Type checking functions</span></span>](#bk_type_checking_functions)|<span data-ttu-id="60630-566">As funções de verificação de tipo permitem que você verifique o tipo de uma expressão em consultas SQL.</span><span class="sxs-lookup"><span data-stu-id="60630-566">The type checking functions allow you to check the type of an expression within SQL queries.</span></span>|  
|[<span data-ttu-id="60630-567">Funções de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="60630-567">String functions</span></span>](#bk_string_functions)|<span data-ttu-id="60630-568">As funções de cadeia de caracteres executam uma operação em um valor de cadeia de caracteres de entrada e retornam uma cadeia de caracteres, um valor numérico ou um valor booliano.</span><span class="sxs-lookup"><span data-stu-id="60630-568">The string functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>|  
|[<span data-ttu-id="60630-569">Funções de matriz</span><span class="sxs-lookup"><span data-stu-id="60630-569">Array functions</span></span>](#bk_array_functions)|<span data-ttu-id="60630-570">As funções de matriz executam uma operação em um valor de matriz de entrada e retornam um valor numérico, booliano ou um valor de matriz.</span><span class="sxs-lookup"><span data-stu-id="60630-570">The array functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span>|  
|[<span data-ttu-id="60630-571">Funções espaciais</span><span class="sxs-lookup"><span data-stu-id="60630-571">Spatial functions</span></span>](#bk_spatial_functions)|<span data-ttu-id="60630-572">As funções espaciais a seguir executam uma operação em um valor de entrada de objeto espacial e retornam um valor numérico ou um valor booliano.</span><span class="sxs-lookup"><span data-stu-id="60630-572">The spatial functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>|  
  
###  <span data-ttu-id="60630-573"><a name="bk_mathematical_functions"></a>Funções matemáticas</span><span class="sxs-lookup"><span data-stu-id="60630-573"><a name="bk_mathematical_functions"></a> Mathematical functions</span></span>  
 <span data-ttu-id="60630-574">As funções a seguir executam um cálculo, normalmente com base em valores de entrada que são fornecidos como argumentos, e retornam um valor numérico.</span><span class="sxs-lookup"><span data-stu-id="60630-574">The following functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="60630-575">ABS</span><span class="sxs-lookup"><span data-stu-id="60630-575">ABS</span></span>](#bk_abs)|[<span data-ttu-id="60630-576">ACOS</span><span class="sxs-lookup"><span data-stu-id="60630-576">ACOS</span></span>](#bk_acos)|[<span data-ttu-id="60630-577">ASIN</span><span class="sxs-lookup"><span data-stu-id="60630-577">ASIN</span></span>](#bk_asin)|  
|[<span data-ttu-id="60630-578">ATAN</span><span class="sxs-lookup"><span data-stu-id="60630-578">ATAN</span></span>](#bk_atan)|[<span data-ttu-id="60630-579">ATN2</span><span class="sxs-lookup"><span data-stu-id="60630-579">ATN2</span></span>](#bk_atn2)|[<span data-ttu-id="60630-580">CEILING</span><span class="sxs-lookup"><span data-stu-id="60630-580">CEILING</span></span>](#bk_ceiling)|  
|[<span data-ttu-id="60630-581">COS</span><span class="sxs-lookup"><span data-stu-id="60630-581">COS</span></span>](#bk_cos)|[<span data-ttu-id="60630-582">COT</span><span class="sxs-lookup"><span data-stu-id="60630-582">COT</span></span>](#bk_cot)|[<span data-ttu-id="60630-583">DEGREES</span><span class="sxs-lookup"><span data-stu-id="60630-583">DEGREES</span></span>](#bk_degrees)|  
|[<span data-ttu-id="60630-584">EXP</span><span class="sxs-lookup"><span data-stu-id="60630-584">EXP</span></span>](#bk_exp)|[<span data-ttu-id="60630-585">FLOOR</span><span class="sxs-lookup"><span data-stu-id="60630-585">FLOOR</span></span>](#bk_floor)|[<span data-ttu-id="60630-586">LOG</span><span class="sxs-lookup"><span data-stu-id="60630-586">LOG</span></span>](#bk_log)|  
|[<span data-ttu-id="60630-587">LOG10</span><span class="sxs-lookup"><span data-stu-id="60630-587">LOG10</span></span>](#bk_log10)|[<span data-ttu-id="60630-588">PI</span><span class="sxs-lookup"><span data-stu-id="60630-588">PI</span></span>](#bk_pi)|[<span data-ttu-id="60630-589">POWER</span><span class="sxs-lookup"><span data-stu-id="60630-589">POWER</span></span>](#bk_power)|  
|[<span data-ttu-id="60630-590">RADIANS</span><span class="sxs-lookup"><span data-stu-id="60630-590">RADIANS</span></span>](#bk_radians)|[<span data-ttu-id="60630-591">ROUND</span><span class="sxs-lookup"><span data-stu-id="60630-591">ROUND</span></span>](#bk_round)|[<span data-ttu-id="60630-592">SIN</span><span class="sxs-lookup"><span data-stu-id="60630-592">SIN</span></span>](#bk_sin)|  
|[<span data-ttu-id="60630-593">SQRT</span><span class="sxs-lookup"><span data-stu-id="60630-593">SQRT</span></span>](#bk_sqrt)|[<span data-ttu-id="60630-594">SQUARE</span><span class="sxs-lookup"><span data-stu-id="60630-594">SQUARE</span></span>](#bk_square)|[<span data-ttu-id="60630-595">SIGN</span><span class="sxs-lookup"><span data-stu-id="60630-595">SIGN</span></span>](#bk_sign)|  
|[<span data-ttu-id="60630-596">TAN</span><span class="sxs-lookup"><span data-stu-id="60630-596">TAN</span></span>](#bk_tan)|[<span data-ttu-id="60630-597">TRUNC</span><span class="sxs-lookup"><span data-stu-id="60630-597">TRUNC</span></span>](#bk_trunc)||  
  
####  <span data-ttu-id="60630-598"><a name="bk_abs"></a> ABS</span><span class="sxs-lookup"><span data-stu-id="60630-598"><a name="bk_abs"></a> ABS</span></span>  
 <span data-ttu-id="60630-599">Retorna o valor absoluto (positivo) da expressão numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="60630-599">Returns the absolute (positive) value of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="60630-600">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-600">**Syntax**</span></span>  
  
```  
ABS (<numeric_expression>)  
```  
  
 <span data-ttu-id="60630-601">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-601">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="60630-602">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-602">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-603">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-603">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-604">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-604">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-605">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-605">**Examples**</span></span>  
  
 <span data-ttu-id="60630-606">O exemplo a seguir mostra os resultados do uso da função ABS em três números diferentes.</span><span class="sxs-lookup"><span data-stu-id="60630-606">The following example shows the results of using the ABS function on three different numbers.</span></span>  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 <span data-ttu-id="60630-607">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-607">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <span data-ttu-id="60630-608"><a name="bk_acos"></a> ACOS</span><span class="sxs-lookup"><span data-stu-id="60630-608"><a name="bk_acos"></a> ACOS</span></span>  
 <span data-ttu-id="60630-609">Retorna o ângulo, em radianos, cujo cosseno é a expressão numérica especificada (também chamado de arco cosseno).</span><span class="sxs-lookup"><span data-stu-id="60630-609">Returns the angle, in radians, whose cosine is the specified numeric expression; also called arccosine.</span></span>  
  
 <span data-ttu-id="60630-610">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-610">**Syntax**</span></span>  
  
```  
ACOS(<numeric_expression>)  
```  
  
 <span data-ttu-id="60630-611">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-611">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="60630-612">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-612">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-613">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-613">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-614">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-614">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-615">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-615">**Examples**</span></span>  
  
 <span data-ttu-id="60630-616">O exemplo a seguir retorna ACOS de -1.</span><span class="sxs-lookup"><span data-stu-id="60630-616">The following example returns the ACOS of -1.</span></span>  
  
```  
SELECT ACOS(-1)  
```  
  
 <span data-ttu-id="60630-617">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-617">Here is the result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="60630-618"><a name="bk_asin"></a> ASIN</span><span class="sxs-lookup"><span data-stu-id="60630-618"><a name="bk_asin"></a> ASIN</span></span>  
 <span data-ttu-id="60630-619">Retorna o ângulo, em radianos, cujo seno é a expressão numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="60630-619">Returns the angle, in radians, whose sine is the specified numeric expression.</span></span> <span data-ttu-id="60630-620">Isso também é chamado de arco seno.</span><span class="sxs-lookup"><span data-stu-id="60630-620">This is also called arcsine.</span></span>  
  
 <span data-ttu-id="60630-621">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-621">**Syntax**</span></span>  
  
```  
ASIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="60630-622">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-622">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="60630-623">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-623">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-624">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-624">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-625">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-625">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-626">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-626">**Examples**</span></span>  
  
 <span data-ttu-id="60630-627">O exemplo a seguir retorna ASIN de -1.</span><span class="sxs-lookup"><span data-stu-id="60630-627">The following example returns the ASIN of -1.</span></span>  
  
```  
SELECT ASIN(-1)  
```  
  
 <span data-ttu-id="60630-628">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-628">Here is the result set.</span></span>  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <span data-ttu-id="60630-629"><a name="bk_atan"></a> ATAN</span><span class="sxs-lookup"><span data-stu-id="60630-629"><a name="bk_atan"></a> ATAN</span></span>  
 <span data-ttu-id="60630-630">Retorna o ângulo, em radianos, cuja tangente é a expressão numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="60630-630">Returns the angle, in radians, whose tangent is the specified numeric expression.</span></span> <span data-ttu-id="60630-631">Isso também é chamado de arco tangente.</span><span class="sxs-lookup"><span data-stu-id="60630-631">This is also called arctangent.</span></span>  
  
 <span data-ttu-id="60630-632">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-632">**Syntax**</span></span>  
  
```  
ATAN(<numeric_expression>)  
```  
  
 <span data-ttu-id="60630-633">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-633">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="60630-634">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-634">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-635">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-635">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-636">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-636">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-637">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-637">**Examples**</span></span>  
  
 <span data-ttu-id="60630-638">O exemplo a seguir retorna o ATAN do valor especificado.</span><span class="sxs-lookup"><span data-stu-id="60630-638">The following example returns the ATAN of the specified value.</span></span>  
  
```  
SELECT ATAN(-45.01)  
```  
  
 <span data-ttu-id="60630-639">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-639">Here is the result set.</span></span>  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <span data-ttu-id="60630-640"><a name="bk_atn2"></a> ATN2</span><span class="sxs-lookup"><span data-stu-id="60630-640"><a name="bk_atn2"></a> ATN2</span></span>  
 <span data-ttu-id="60630-641">Retorna o valor principal do arco tangente de y/x, expresso em radianos.</span><span class="sxs-lookup"><span data-stu-id="60630-641">Returns the principal value of the arc tangent of y/x, expressed in radians.</span></span>  
  
 <span data-ttu-id="60630-642">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-642">**Syntax**</span></span>  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 <span data-ttu-id="60630-643">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-643">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="60630-644">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-644">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-645">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-645">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-646">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-646">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-647">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-647">**Examples**</span></span>  
  
 <span data-ttu-id="60630-648">O exemplo a seguir calcula o ATN2 dos componentes x e y especificados.</span><span class="sxs-lookup"><span data-stu-id="60630-648">The following example calculates the ATN2 for the specified x and y components.</span></span>  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 <span data-ttu-id="60630-649">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-649">Here is the result set.</span></span>  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <span data-ttu-id="60630-650"><a name="bk_ceiling"></a> CEILING</span><span class="sxs-lookup"><span data-stu-id="60630-650"><a name="bk_ceiling"></a> CEILING</span></span>  
 <span data-ttu-id="60630-651">Retorna o menor valor de número inteiro maior ou igual à expressão numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="60630-651">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span>  
  
 <span data-ttu-id="60630-652">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-652">**Syntax**</span></span>  
  
```  
CEILING (<numeric_expression>)  
```  
  
 <span data-ttu-id="60630-653">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-653">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="60630-654">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-654">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-655">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-655">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-656">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-656">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-657">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-657">**Examples**</span></span>  
  
 <span data-ttu-id="60630-658">O exemplo a seguir mostra valores numéricos positivos, negativos e zero com a função CEILING.</span><span class="sxs-lookup"><span data-stu-id="60630-658">The following example shows positive numeric, negative, and zero values with the CEILING function.</span></span>  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 <span data-ttu-id="60630-659">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-659">Here is the result set.</span></span>  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <span data-ttu-id="60630-660"><a name="bk_cos"></a> COS</span><span class="sxs-lookup"><span data-stu-id="60630-660"><a name="bk_cos"></a> COS</span></span>  
 <span data-ttu-id="60630-661">Retorna o cosseno trigonométrico do ângulo especificado, em radianos, na expressão especificada.</span><span class="sxs-lookup"><span data-stu-id="60630-661">Returns the trigonometric cosine of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="60630-662">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-662">**Syntax**</span></span>  
  
```  
COS(<numeric_expression>)  
```  
  
 <span data-ttu-id="60630-663">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-663">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="60630-664">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-664">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-665">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-665">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-666">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-666">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-667">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-667">**Examples**</span></span>  
  
 <span data-ttu-id="60630-668">O exemplo a seguir calcula o COS do ângulo especificado.</span><span class="sxs-lookup"><span data-stu-id="60630-668">The following example calculates the COS of the specified angle.</span></span>  
  
```  
SELECT COS(14.78)  
```  
  
 <span data-ttu-id="60630-669">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-669">Here is the result set.</span></span>  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <span data-ttu-id="60630-670"><a name="bk_cot"></a> COT</span><span class="sxs-lookup"><span data-stu-id="60630-670"><a name="bk_cot"></a> COT</span></span>  
 <span data-ttu-id="60630-671">Retorna a cotangente trigonométrica do ângulo especificado, em radianos, na expressão numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="60630-671">Returns the trigonometric cotangent of the specified angle, in radians, in the specified numeric expression.</span></span>  
  
 <span data-ttu-id="60630-672">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-672">**Syntax**</span></span>  
  
```  
COT(<numeric_expression>)  
```  
  
 <span data-ttu-id="60630-673">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-673">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="60630-674">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-674">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-675">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-675">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-676">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-676">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-677">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-677">**Examples**</span></span>  
  
 <span data-ttu-id="60630-678">O exemplo a seguir calcula o COT do ângulo especificado.</span><span class="sxs-lookup"><span data-stu-id="60630-678">The following example calculates the COT of the specified angle.</span></span>  
  
```  
SELECT COT(124.1332)  
```  
  
 <span data-ttu-id="60630-679">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-679">Here is the result set.</span></span>  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <span data-ttu-id="60630-680"><a name="bk_degrees"></a> DEGREES</span><span class="sxs-lookup"><span data-stu-id="60630-680"><a name="bk_degrees"></a> DEGREES</span></span>  
 <span data-ttu-id="60630-681">Retorna o ângulo correspondente, em graus, para um ângulo especificado em radianos.</span><span class="sxs-lookup"><span data-stu-id="60630-681">Returns the corresponding angle in degrees for an angle specified in radians.</span></span>  
  
 <span data-ttu-id="60630-682">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-682">**Syntax**</span></span>  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 <span data-ttu-id="60630-683">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-683">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="60630-684">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-684">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-685">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-685">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-686">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-686">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-687">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-687">**Examples**</span></span>  
  
 <span data-ttu-id="60630-688">O exemplo a seguir retorna o número de graus em um ângulo de radiano PI/2.</span><span class="sxs-lookup"><span data-stu-id="60630-688">The following example returns the number of degrees in an angle of PI/2 radians.</span></span>  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 <span data-ttu-id="60630-689">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-689">Here is the result set.</span></span>  
  
```  
[{"$1": 90}]  
```  
  
####  <span data-ttu-id="60630-690"><a name="bk_floor"></a> FLOOR</span><span class="sxs-lookup"><span data-stu-id="60630-690"><a name="bk_floor"></a> FLOOR</span></span>  
 <span data-ttu-id="60630-691">Retorna o maior inteiro menor ou igual à expressão numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="60630-691">Returns the largest integer less than or equal to the specified numeric expression.</span></span>  
  
 <span data-ttu-id="60630-692">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-692">**Syntax**</span></span>  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 <span data-ttu-id="60630-693">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-693">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="60630-694">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-694">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-695">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-695">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-696">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-696">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-697">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-697">**Examples**</span></span>  
  
 <span data-ttu-id="60630-698">O exemplo a seguir mostra valores numéricos positivos, negativos e zero com a função FLOOR.</span><span class="sxs-lookup"><span data-stu-id="60630-698">The following example shows positive numeric, negative, and zero values with the FLOOR function.</span></span>  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 <span data-ttu-id="60630-699">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-699">Here is the result set.</span></span>  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <span data-ttu-id="60630-700"><a name="bk_exp"></a> EXP</span><span class="sxs-lookup"><span data-stu-id="60630-700"><a name="bk_exp"></a> EXP</span></span>  
 <span data-ttu-id="60630-701">Retorna o valor exponencial da expressão numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="60630-701">Returns the exponential value of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="60630-702">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-702">**Syntax**</span></span>  
  
```  
EXP (<numeric_expression>)  
```  
  
 <span data-ttu-id="60630-703">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-703">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="60630-704">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-704">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-705">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-705">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-706">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-706">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-707">**Comentários**</span><span class="sxs-lookup"><span data-stu-id="60630-707">**Remarks**</span></span>  
  
 <span data-ttu-id="60630-708">A constante **e** (2,718281...) é a base dos logaritmos naturais.</span><span class="sxs-lookup"><span data-stu-id="60630-708">The constant **e** (2.718281…), is the base of natural logarithms.</span></span>  
  
 <span data-ttu-id="60630-709">O expoente de um número é a constante **e** elevado à potência do número.</span><span class="sxs-lookup"><span data-stu-id="60630-709">The exponent of a number is the constant **e** raised to the power of the number.</span></span> <span data-ttu-id="60630-710">Por exemplo, EXP(1.0) = e^1.0 = 2.71828182845905 e EXP(10) = e^10 = 22026.4657948067.</span><span class="sxs-lookup"><span data-stu-id="60630-710">For example EXP(1.0) = e^1.0 = 2.71828182845905 and EXP(10) = e^10 = 22026.4657948067.</span></span>  
  
 <span data-ttu-id="60630-711">O exponencial do logaritmo natural de um número é o número em si: EXP (LOG (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="60630-711">The exponential of the natural logarithm of a number is the number itself: EXP (LOG (n)) = n.</span></span> <span data-ttu-id="60630-712">E o logaritmo natural do exponencial de um número é o número em si: LOG (EXP (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="60630-712">And the natural logarithm of the exponential of a number is the number itself: LOG (EXP (n)) = n.</span></span>  
  
 <span data-ttu-id="60630-713">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-713">**Examples**</span></span>  
  
 <span data-ttu-id="60630-714">O exemplo a seguir declara uma variável e retorna o valor exponencial da variável especificada (10).</span><span class="sxs-lookup"><span data-stu-id="60630-714">The following example declares a variable and returns the exponential value of the specified variable (10).</span></span>  
  
```  
SELECT EXP(10)  
```  
  
 <span data-ttu-id="60630-715">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-715">Here is the result set.</span></span>  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 <span data-ttu-id="60630-716">O exemplo a seguir retorna o valor exponencial do logaritmo natural de 20 e o logaritmo natural do exponencial de 20.</span><span class="sxs-lookup"><span data-stu-id="60630-716">The following example returns the exponential value of the natural logarithm of 20 and the natural logarithm of the exponential of 20.</span></span> <span data-ttu-id="60630-717">Como essas funções são funções inversas uma da outra, o valor retornado com o arredondamento para a matemática do ponto flutuante em ambos os casos é 20.</span><span class="sxs-lookup"><span data-stu-id="60630-717">Because these functions are inverse functions of one another, the return value with rounding for floating point math in both cases is 20.</span></span>  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 <span data-ttu-id="60630-718">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-718">Here is the result set.</span></span>  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <span data-ttu-id="60630-719"><a name="bk_log"></a> LOG</span><span class="sxs-lookup"><span data-stu-id="60630-719"><a name="bk_log"></a> LOG</span></span>  
 <span data-ttu-id="60630-720">Retorna o logaritmo natural de expressão numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="60630-720">Returns the natural logarithm of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="60630-721">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-721">**Syntax**</span></span>  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 <span data-ttu-id="60630-722">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-722">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="60630-723">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-723">Is a numeric expression.</span></span>  
  
-   `base`  
  
     <span data-ttu-id="60630-724">Argumento numérico opcional que define a base para o logaritmo.</span><span class="sxs-lookup"><span data-stu-id="60630-724">Optional numeric argument that sets the base for the logarithm.</span></span>  
  
 <span data-ttu-id="60630-725">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-725">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-726">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-726">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-727">**Comentários**</span><span class="sxs-lookup"><span data-stu-id="60630-727">**Remarks**</span></span>  
  
 <span data-ttu-id="60630-728">Por padrão, LOG() retorna o logaritmo natural.</span><span class="sxs-lookup"><span data-stu-id="60630-728">By default, LOG() returns the natural logarithm.</span></span> <span data-ttu-id="60630-729">Você pode alterar a base do logaritmo para outro valor usando o parâmetro opcional de base.</span><span class="sxs-lookup"><span data-stu-id="60630-729">You can change the base of the logarithm to another value by using the optional base parameter.</span></span>  
  
 <span data-ttu-id="60630-730">O logaritmo natural é o logaritmo de base **e**, em que **e** é uma constante irracional aproximadamente igual a 2,718281828.</span><span class="sxs-lookup"><span data-stu-id="60630-730">The natural logarithm is the logarithm to the base **e**, where **e** is an irrational constant approximately equal to 2.718281828.</span></span>  
  
 <span data-ttu-id="60630-731">O logaritmo natural do exponencial de um número é o número em si: LOG(EXP(n)) = n.</span><span class="sxs-lookup"><span data-stu-id="60630-731">The natural logarithm of the exponential of a number is the number itself: LOG( EXP( n ) ) = n.</span></span> <span data-ttu-id="60630-732">E o exponencial do logaritmo natural de um número é o número em si: EXP(LOG(n)) = n.</span><span class="sxs-lookup"><span data-stu-id="60630-732">And the exponential of the natural logarithm of a number is the number itself: EXP( LOG( n ) ) = n.</span></span>  
  
 <span data-ttu-id="60630-733">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-733">**Examples**</span></span>  
  
 <span data-ttu-id="60630-734">O exemplo a seguir declara uma variável e retorna o valor logarítmico da variável especificada (10).</span><span class="sxs-lookup"><span data-stu-id="60630-734">The following example declares a variable and returns the logarithm value of the specified variable (10).</span></span>  
  
```  
SELECT LOG(10)  
```  
  
 <span data-ttu-id="60630-735">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-735">Here is the result set.</span></span>  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 <span data-ttu-id="60630-736">O exemplo a seguir calcula o LOG para o expoente de um número.</span><span class="sxs-lookup"><span data-stu-id="60630-736">The following example calculates the LOG for the exponent of a number.</span></span>  
  
```  
SELECT EXP(LOG(10))  
```  
  
 <span data-ttu-id="60630-737">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-737">Here is the result set.</span></span>  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <span data-ttu-id="60630-738"><a name="bk_log10"></a> LOG10</span><span class="sxs-lookup"><span data-stu-id="60630-738"><a name="bk_log10"></a> LOG10</span></span>  
 <span data-ttu-id="60630-739">Retorna o logaritmo de base 10 da expressão numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="60630-739">Returns the base-10 logarithm of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="60630-740">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-740">**Syntax**</span></span>  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 <span data-ttu-id="60630-741">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-741">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="60630-742">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-742">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-743">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-743">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-744">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-744">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-745">**Comentários**</span><span class="sxs-lookup"><span data-stu-id="60630-745">**Remarks**</span></span>  
  
 <span data-ttu-id="60630-746">As funções LOG10 e POWER estão inversamente relacionadas entre si.</span><span class="sxs-lookup"><span data-stu-id="60630-746">The LOG10 and POWER functions are inversely related to one another.</span></span> <span data-ttu-id="60630-747">Por exemplo, 10 ^ LOG10(n) = n.</span><span class="sxs-lookup"><span data-stu-id="60630-747">For example, 10 ^ LOG10(n) = n.</span></span>  
  
 <span data-ttu-id="60630-748">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-748">**Examples**</span></span>  
  
 <span data-ttu-id="60630-749">O exemplo a seguir declara uma variável e retorna o valor LOG10 da variável especificada (100).</span><span class="sxs-lookup"><span data-stu-id="60630-749">The following example declares a variable and returns the LOG10 value of the specified variable (100).</span></span>  
  
```  
SELECT LOG10(100)  
```  
  
 <span data-ttu-id="60630-750">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-750">Here is the result set.</span></span>  
  
```  
[{$1: 2}]  
```  
  
####  <span data-ttu-id="60630-751"><a name="bk_pi"></a> PI</span><span class="sxs-lookup"><span data-stu-id="60630-751"><a name="bk_pi"></a> PI</span></span>  
 <span data-ttu-id="60630-752">Retorna o valor constante de PI.</span><span class="sxs-lookup"><span data-stu-id="60630-752">Returns the constant value of PI.</span></span>  
  
 <span data-ttu-id="60630-753">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-753">**Syntax**</span></span>  
  
```  
PI ()  
```  
  
 <span data-ttu-id="60630-754">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-754">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="60630-755">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-755">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-756">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-756">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-757">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-757">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-758">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-758">**Examples**</span></span>  
  
 <span data-ttu-id="60630-759">O exemplo a seguir retorna o valor de PI.</span><span class="sxs-lookup"><span data-stu-id="60630-759">The following example returns the value of PI.</span></span>  
  
```  
SELECT PI()  
```  
  
 <span data-ttu-id="60630-760">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-760">Here is the result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="60630-761"><a name="bk_power"></a> POWER</span><span class="sxs-lookup"><span data-stu-id="60630-761"><a name="bk_power"></a> POWER</span></span>  
 <span data-ttu-id="60630-762">Retorna o valor da expressão especificada para a potência indicada.</span><span class="sxs-lookup"><span data-stu-id="60630-762">Returns the value of the specified expression to the specified power.</span></span>  
  
 <span data-ttu-id="60630-763">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-763">**Syntax**</span></span>  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 <span data-ttu-id="60630-764">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-764">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="60630-765">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-765">Is a numeric expression.</span></span>  
  
-   `y`  
  
     <span data-ttu-id="60630-766">É a potência à qual elevar `numeric_expression`.</span><span class="sxs-lookup"><span data-stu-id="60630-766">Is the power to which to raise `numeric_expression`.</span></span>  
  
 <span data-ttu-id="60630-767">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-767">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-768">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-768">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-769">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-769">**Examples**</span></span>  
  
 <span data-ttu-id="60630-770">O exemplo a seguir demonstra como elevar um número ao cubo.</span><span class="sxs-lookup"><span data-stu-id="60630-770">The following example demonstrates raising a number to the power of 3 (the cube of the number).</span></span>  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 <span data-ttu-id="60630-771">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-771">Here is the result set.</span></span>  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <span data-ttu-id="60630-772"><a name="bk_radians"></a> RADIANS</span><span class="sxs-lookup"><span data-stu-id="60630-772"><a name="bk_radians"></a> RADIANS</span></span>  
 <span data-ttu-id="60630-773">Retorna radianos quando uma expressão numérica é inserida em graus.</span><span class="sxs-lookup"><span data-stu-id="60630-773">Returns radians when a numeric expression, in degrees, is entered.</span></span>  
  
 <span data-ttu-id="60630-774">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-774">**Syntax**</span></span>  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 <span data-ttu-id="60630-775">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-775">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="60630-776">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-776">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-777">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-777">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-778">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-778">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-779">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-779">**Examples**</span></span>  
  
 <span data-ttu-id="60630-780">O exemplo a seguir usa alguns ângulos como entrada e retorna seus valores radianos correspondentes.</span><span class="sxs-lookup"><span data-stu-id="60630-780">The following example takes a few angles as input and returns their corresponding radian values.</span></span>  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 <span data-ttu-id="60630-781">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-781">Here is the result set.</span></span>  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <span data-ttu-id="60630-782"><a name="bk_round"></a> ROUND</span><span class="sxs-lookup"><span data-stu-id="60630-782"><a name="bk_round"></a> ROUND</span></span>  
 <span data-ttu-id="60630-783">Retorna um valor numérico, arredondado para o valor inteiro mais próximo.</span><span class="sxs-lookup"><span data-stu-id="60630-783">Returns a numeric value, rounded to the closest integer value.</span></span>  
  
 <span data-ttu-id="60630-784">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-784">**Syntax**</span></span>  
  
```  
ROUND(<numeric_expression>)  
```  
  
 <span data-ttu-id="60630-785">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-785">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="60630-786">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-786">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-787">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-787">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-788">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-788">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-789">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-789">**Examples**</span></span>  
  
 <span data-ttu-id="60630-790">O exemplo a seguir arredonda os números positivos e negativos para o inteiro mais próximo.</span><span class="sxs-lookup"><span data-stu-id="60630-790">The following example rounds the following positive and negative numbers to the nearest integer.</span></span>  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 <span data-ttu-id="60630-791">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-791">Here is the result set.</span></span>  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <span data-ttu-id="60630-792"><a name="bk_sign"></a> SIGN</span><span class="sxs-lookup"><span data-stu-id="60630-792"><a name="bk_sign"></a> SIGN</span></span>  
 <span data-ttu-id="60630-793">Retorna o sinal positivo (+1), zero (0) ou negativo (-1) da expressão numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="60630-793">Returns the positive (+1), zero (0), or negative (-1) sign of the specified numeric expression.</span></span>  
  
 <span data-ttu-id="60630-794">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-794">**Syntax**</span></span>  
  
```  
SIGN(<numeric_expression>)  
```  
  
 <span data-ttu-id="60630-795">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-795">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="60630-796">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-796">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-797">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-797">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-798">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-798">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-799">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-799">**Examples**</span></span>  
  
 <span data-ttu-id="60630-800">O exemplo a seguir retorna os valores SIGN de números de -2 a 2.</span><span class="sxs-lookup"><span data-stu-id="60630-800">The following example returns the SIGN values of numbers from -2 to 2.</span></span>  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 <span data-ttu-id="60630-801">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-801">Here is the result set.</span></span>  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <span data-ttu-id="60630-802"><a name="bk_sin"></a> SIN</span><span class="sxs-lookup"><span data-stu-id="60630-802"><a name="bk_sin"></a> SIN</span></span>  
 <span data-ttu-id="60630-803">Retorna o seno trigonométrico do ângulo especificado, em radianos, na expressão especificada.</span><span class="sxs-lookup"><span data-stu-id="60630-803">Returns the trigonometric sine of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="60630-804">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-804">**Syntax**</span></span>  
  
```  
SIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="60630-805">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-805">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="60630-806">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-806">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-807">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-807">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-808">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-808">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-809">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-809">**Examples**</span></span>  
  
 <span data-ttu-id="60630-810">O exemplo a seguir calcula o SIN do ângulo especificado.</span><span class="sxs-lookup"><span data-stu-id="60630-810">The following example calculates the SIN of the specified angle.</span></span>  
  
```  
SELECT SIN(45.175643)  
```  
  
 <span data-ttu-id="60630-811">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-811">Here is the result set.</span></span>  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <span data-ttu-id="60630-812"><a name="bk_sqrt"></a> SQRT</span><span class="sxs-lookup"><span data-stu-id="60630-812"><a name="bk_sqrt"></a> SQRT</span></span>  
 <span data-ttu-id="60630-813">Retorna a raiz quadrada do valor numérico especificado.</span><span class="sxs-lookup"><span data-stu-id="60630-813">Returns the square root of the specified numeric value.</span></span>  
  
 <span data-ttu-id="60630-814">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-814">**Syntax**</span></span>  
  
```  
SQRT(<numeric_expression>)  
```  
  
 <span data-ttu-id="60630-815">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-815">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="60630-816">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-816">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-817">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-817">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-818">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-818">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-819">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-819">**Examples**</span></span>  
  
 <span data-ttu-id="60630-820">O exemplo a seguir retorna as raízes quadradas dos números de 1 a 3.</span><span class="sxs-lookup"><span data-stu-id="60630-820">The following example returns the square roots of numbers 1-3.</span></span>  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 <span data-ttu-id="60630-821">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-821">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <span data-ttu-id="60630-822"><a name="bk_square"></a> SQUARE</span><span class="sxs-lookup"><span data-stu-id="60630-822"><a name="bk_square"></a> SQUARE</span></span>  
 <span data-ttu-id="60630-823">Retorna o quadrado do valor numérico especificado.</span><span class="sxs-lookup"><span data-stu-id="60630-823">Returns the square of the specified numeric value.</span></span>  
  
 <span data-ttu-id="60630-824">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-824">**Syntax**</span></span>  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 <span data-ttu-id="60630-825">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-825">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="60630-826">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-826">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-827">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-827">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-828">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-828">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-829">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-829">**Examples**</span></span>  
  
 <span data-ttu-id="60630-830">O exemplo a seguir retorna os quadrados dos números de 1 a 3.</span><span class="sxs-lookup"><span data-stu-id="60630-830">The following example returns the squares of numbers 1-3.</span></span>  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 <span data-ttu-id="60630-831">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-831">Here is the result set.</span></span>  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <span data-ttu-id="60630-832"><a name="bk_tan"></a> TAN</span><span class="sxs-lookup"><span data-stu-id="60630-832"><a name="bk_tan"></a> TAN</span></span>  
 <span data-ttu-id="60630-833">Retorna a tangente do ângulo especificado, em radianos, na expressão especificada.</span><span class="sxs-lookup"><span data-stu-id="60630-833">Returns the tangent of the specified angle, in radians, in the specified expression.</span></span>  
  
 <span data-ttu-id="60630-834">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-834">**Syntax**</span></span>  
  
```  
TAN (<numeric_expression>)  
```  
  
 <span data-ttu-id="60630-835">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-835">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="60630-836">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-836">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-837">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-837">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-838">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-838">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-839">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-839">**Examples**</span></span>  
  
 <span data-ttu-id="60630-840">O exemplo a seguir calcula a tangente de PI()/2.</span><span class="sxs-lookup"><span data-stu-id="60630-840">The following example calculates the tangent of PI()/2.</span></span>  
  
```  
SELECT TAN(PI()/2);  
```  
  
 <span data-ttu-id="60630-841">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-841">Here is the result set.</span></span>  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <span data-ttu-id="60630-842"><a name="bk_trunc"></a>TRUNC</span><span class="sxs-lookup"><span data-stu-id="60630-842"><a name="bk_trunc"></a> TRUNC</span></span>  
 <span data-ttu-id="60630-843">Retorna um valor numérico, truncado para o valor inteiro mais próximo.</span><span class="sxs-lookup"><span data-stu-id="60630-843">Returns a numeric value, truncated to the closest integer value.</span></span>  
  
 <span data-ttu-id="60630-844">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-844">**Syntax**</span></span>  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 <span data-ttu-id="60630-845">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-845">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="60630-846">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-846">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-847">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-847">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-848">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-848">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-849">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-849">**Examples**</span></span>  
  
 <span data-ttu-id="60630-850">O exemplo a seguir trunca os números positivos e negativos para o valor inteiro mais próximo.</span><span class="sxs-lookup"><span data-stu-id="60630-850">The following example truncates the following positive and negative numbers to the nearest integer value.</span></span>  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 <span data-ttu-id="60630-851">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-851">Here is the result set.</span></span>  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <span data-ttu-id="60630-852"><a name="bk_type_checking_functions"></a> Funções de verificação de tipo</span><span class="sxs-lookup"><span data-stu-id="60630-852"><a name="bk_type_checking_functions"></a> Type checking functions</span></span>  
 <span data-ttu-id="60630-853">As funções a seguir dão suporte a verificação de tipo em relação aos valores de entrada e retornam, cada um, um valor booliano.</span><span class="sxs-lookup"><span data-stu-id="60630-853">The following functions support type checking against input values, and each return a Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="60630-854">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="60630-854">IS_ARRAY</span></span>](#bk_is_array)|[<span data-ttu-id="60630-855">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="60630-855">IS_BOOL</span></span>](#bk_is_bool)|[<span data-ttu-id="60630-856">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="60630-856">IS_DEFINED</span></span>](#bk_is_defined)|  
|[<span data-ttu-id="60630-857">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="60630-857">IS_NULL</span></span>](#bk_is_null)|[<span data-ttu-id="60630-858">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="60630-858">IS_NUMBER</span></span>](#bk_is_number)|[<span data-ttu-id="60630-859">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="60630-859">IS_OBJECT</span></span>](#bk_is_object)|  
|[<span data-ttu-id="60630-860">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="60630-860">IS_PRIMITIVE</span></span>](#bk_is_primitive)|[<span data-ttu-id="60630-861">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="60630-861">IS_STRING</span></span>](#bk_is_string)||  
  
####  <span data-ttu-id="60630-862"><a name="bk_is_array"></a>IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="60630-862"><a name="bk_is_array"></a> IS_ARRAY</span></span>  
 <span data-ttu-id="60630-863">Retorna um valor booliano que indica se o tipo da expressão especificada é uma matriz.</span><span class="sxs-lookup"><span data-stu-id="60630-863">Returns a Boolean value indicating if the type of the specified expression is an array.</span></span>  
  
 <span data-ttu-id="60630-864">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-864">**Syntax**</span></span>  
  
```  
IS_ARRAY(<expression>)  
```  
  
 <span data-ttu-id="60630-865">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-865">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="60630-866">É qualquer expressão válida.</span><span class="sxs-lookup"><span data-stu-id="60630-866">Is any valid expression.</span></span>  
  
 <span data-ttu-id="60630-867">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-867">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-868">Retorna uma expressão booliana.</span><span class="sxs-lookup"><span data-stu-id="60630-868">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="60630-869">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-869">**Examples**</span></span>  
  
 <span data-ttu-id="60630-870">O exemplo a seguir verifica objetos JSON booliano, número, cadeia de caracteres, nulo, objeto, matriz e tipos indefinidos usando a função IS_ARRAY.</span><span class="sxs-lookup"><span data-stu-id="60630-870">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_ARRAY function.</span></span>  
  
```  
SELECT   
 IS_ARRAY(true),   
 IS_ARRAY(1),  
 IS_ARRAY("value"),  
 IS_ARRAY(null),  
 IS_ARRAY({prop: "value"}),   
 IS_ARRAY([1, 2, 3]),  
 IS_ARRAY({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="60630-871">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-871">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <span data-ttu-id="60630-872"><a name="bk_is_bool"></a>IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="60630-872"><a name="bk_is_bool"></a> IS_BOOL</span></span>  
 <span data-ttu-id="60630-873">Retorna um valor booliano que indica se o tipo da expressão especificada é um booliano.</span><span class="sxs-lookup"><span data-stu-id="60630-873">Returns a Boolean value indicating if the type of the specified expression is a Boolean.</span></span>  
  
 <span data-ttu-id="60630-874">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-874">**Syntax**</span></span>  
  
```  
IS_BOOL(<expression>)  
```  
  
 <span data-ttu-id="60630-875">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-875">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="60630-876">É qualquer expressão válida.</span><span class="sxs-lookup"><span data-stu-id="60630-876">Is any valid expression.</span></span>  
  
 <span data-ttu-id="60630-877">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-877">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-878">Retorna uma expressão booliana.</span><span class="sxs-lookup"><span data-stu-id="60630-878">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="60630-879">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-879">**Examples**</span></span>  
  
 <span data-ttu-id="60630-880">O exemplo a seguir verifica objetos JSON booliano, número, cadeia de caracteres, nulo, objeto, matriz e tipos indefinidos usando a função IS_BOOL.</span><span class="sxs-lookup"><span data-stu-id="60630-880">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_BOOL function.</span></span>  
  
```  
SELECT   
    IS_BOOL(true),   
    IS_BOOL(1),  
    IS_BOOL("value"),   
    IS_BOOL(null),  
    IS_BOOL({prop: "value"}),   
    IS_BOOL([1, 2, 3]),  
    IS_BOOL({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="60630-881">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-881">Here is the result set.</span></span>  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="60630-882"><a name="bk_is_defined"></a>IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="60630-882"><a name="bk_is_defined"></a> IS_DEFINED</span></span>  
 <span data-ttu-id="60630-883">Retorna um valor booliano que indica se um valor foi atribuído à propriedade.</span><span class="sxs-lookup"><span data-stu-id="60630-883">Returns a Boolean indicating if the property has been assigned a value.</span></span>  
  
 <span data-ttu-id="60630-884">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-884">**Syntax**</span></span>  
  
```  
IS_DEFINED(<expression>)  
```  
  
 <span data-ttu-id="60630-885">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-885">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="60630-886">É qualquer expressão válida.</span><span class="sxs-lookup"><span data-stu-id="60630-886">Is any valid expression.</span></span>  
  
 <span data-ttu-id="60630-887">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-887">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-888">Retorna uma expressão booliana.</span><span class="sxs-lookup"><span data-stu-id="60630-888">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="60630-889">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-889">**Examples**</span></span>  
  
 <span data-ttu-id="60630-890">O exemplo a seguir verifica a presença de uma propriedade no documento JSON especificado.</span><span class="sxs-lookup"><span data-stu-id="60630-890">The following example checks for the presence of a property within the specified JSON document.</span></span> <span data-ttu-id="60630-891">O primeiro retorna true, já que "a" está presente, mas o segundo retorna false porque "b" está ausente.</span><span class="sxs-lookup"><span data-stu-id="60630-891">The first returns true since "a" is present, but the second returns false since "b" is absent.</span></span>  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 <span data-ttu-id="60630-892">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-892">Here is the result set.</span></span>  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <span data-ttu-id="60630-893"><a name="bk_is_null"></a>IS_NULL</span><span class="sxs-lookup"><span data-stu-id="60630-893"><a name="bk_is_null"></a> IS_NULL</span></span>  
 <span data-ttu-id="60630-894">Retorna um valor booliano que indica se o tipo da expressão especificada é nulo.</span><span class="sxs-lookup"><span data-stu-id="60630-894">Returns a Boolean value indicating if the type of the specified expression is null.</span></span>  
  
 <span data-ttu-id="60630-895">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-895">**Syntax**</span></span>  
  
```  
IS_NULL(<expression>)  
```  
  
 <span data-ttu-id="60630-896">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-896">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="60630-897">É qualquer expressão válida.</span><span class="sxs-lookup"><span data-stu-id="60630-897">Is any valid expression.</span></span>  
  
 <span data-ttu-id="60630-898">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-898">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-899">Retorna uma expressão booliana.</span><span class="sxs-lookup"><span data-stu-id="60630-899">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="60630-900">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-900">**Examples**</span></span>  
  
 <span data-ttu-id="60630-901">O exemplo a seguir verifica objetos JSON booliano, número, cadeia de caracteres, nulo, objeto, matriz e tipos indefinidos usando a função IS_NULL.</span><span class="sxs-lookup"><span data-stu-id="60630-901">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_NULL function.</span></span>  
  
```  
SELECT   
    IS_NULL(true),   
    IS_NULL(1),  
    IS_NULL("value"),   
    IS_NULL(null),  
    IS_NULL({prop: "value"}),   
    IS_NULL([1, 2, 3]),  
    IS_NULL({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="60630-902">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-902">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="60630-903"><a name="bk_is_number"></a>IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="60630-903"><a name="bk_is_number"></a> IS_NUMBER</span></span>  
 <span data-ttu-id="60630-904">Retorna um valor booliano que indica se o tipo da expressão especificada é um número.</span><span class="sxs-lookup"><span data-stu-id="60630-904">Returns a Boolean value indicating if the type of the specified expression is a number.</span></span>  
  
 <span data-ttu-id="60630-905">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-905">**Syntax**</span></span>  
  
```  
IS_NUMBER(<expression>)  
```  
  
 <span data-ttu-id="60630-906">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-906">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="60630-907">É qualquer expressão válida.</span><span class="sxs-lookup"><span data-stu-id="60630-907">Is any valid expression.</span></span>  
  
 <span data-ttu-id="60630-908">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-908">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-909">Retorna uma expressão booliana.</span><span class="sxs-lookup"><span data-stu-id="60630-909">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="60630-910">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-910">**Examples**</span></span>  
  
 <span data-ttu-id="60630-911">O exemplo a seguir verifica objetos JSON booliano, número, cadeia de caracteres, nulo, objeto, matriz e tipos indefinidos usando a função IS_NULL.</span><span class="sxs-lookup"><span data-stu-id="60630-911">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_NULL function.</span></span>  
  
```  
SELECT   
    IS_NUMBER(true),   
    IS_NUMBER(1),  
    IS_NUMBER("value"),   
    IS_NUMBER(null),  
    IS_NUMBER({prop: "value"}),   
    IS_NUMBER([1, 2, 3]),  
    IS_NUMBER({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="60630-912">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-912">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="60630-913"><a name="bk_is_object"></a>IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="60630-913"><a name="bk_is_object"></a> IS_OBJECT</span></span>  
 <span data-ttu-id="60630-914">Retorna um valor booliano que indica se o tipo da expressão especificada é um objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="60630-914">Returns a Boolean value indicating if the type of the specified expression is a JSON object.</span></span>  
  
 <span data-ttu-id="60630-915">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-915">**Syntax**</span></span>  
  
```  
IS_OBJECT(<expression>)  
```  
  
 <span data-ttu-id="60630-916">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-916">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="60630-917">É qualquer expressão válida.</span><span class="sxs-lookup"><span data-stu-id="60630-917">Is any valid expression.</span></span>  
  
 <span data-ttu-id="60630-918">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-918">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-919">Retorna uma expressão booliana.</span><span class="sxs-lookup"><span data-stu-id="60630-919">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="60630-920">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-920">**Examples**</span></span>  
  
 <span data-ttu-id="60630-921">O exemplo a seguir verifica objetos JSON booliano, número, cadeia de caracteres, nulo, objeto, matriz e tipos indefinidos usando a função IS_OBJECT.</span><span class="sxs-lookup"><span data-stu-id="60630-921">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_OBJECT function.</span></span>  
  
```  
SELECT   
    IS_OBJECT(true),   
    IS_OBJECT(1),  
    IS_OBJECT("value"),   
    IS_OBJECT(null),  
    IS_OBJECT({prop: "value"}),   
    IS_OBJECT([1, 2, 3]),  
    IS_OBJECT({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="60630-922">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-922">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <span data-ttu-id="60630-923"><a name="bk_is_primitive"></a>IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="60630-923"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span></span>  
 <span data-ttu-id="60630-924">Retorna um valor booliano que indica se o tipo da expressão especificada é um primitivo (cadeia de caracteres, booliano, numérico ou nulo).</span><span class="sxs-lookup"><span data-stu-id="60630-924">Returns a Boolean value indicating if the type of the specified expression is a primitive (string, Boolean, numeric or null).</span></span>  
  
 <span data-ttu-id="60630-925">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-925">**Syntax**</span></span>  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 <span data-ttu-id="60630-926">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-926">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="60630-927">É qualquer expressão válida.</span><span class="sxs-lookup"><span data-stu-id="60630-927">Is any valid expression.</span></span>  
  
 <span data-ttu-id="60630-928">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-928">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-929">Retorna uma expressão booliana.</span><span class="sxs-lookup"><span data-stu-id="60630-929">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="60630-930">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-930">**Examples**</span></span>  
  
 <span data-ttu-id="60630-931">O exemplo a seguir verifica objetos JSON booliano, número, cadeia de caracteres, nulo, objeto, matriz e tipos indefinidos usando a função IS_PRIMITIVE.</span><span class="sxs-lookup"><span data-stu-id="60630-931">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_PRIMITIVE function.</span></span>  
  
```  
SELECT   
           IS_PRIMITIVE(true),   
           IS_PRIMITIVE(1),  
           IS_PRIMITIVE("value"),   
           IS_PRIMITIVE(null),  
           IS_PRIMITIVE({prop: "value"}),   
           IS_PRIMITIVE([1, 2, 3]),  
           IS_PRIMITIVE({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="60630-932">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-932">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <span data-ttu-id="60630-933"><a name="bk_is_string"></a> IS_STRING</span><span class="sxs-lookup"><span data-stu-id="60630-933"><a name="bk_is_string"></a> IS_STRING</span></span>  
 <span data-ttu-id="60630-934">Retorna um valor booliano que indica se o tipo da expressão especificada é uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="60630-934">Returns a Boolean value indicating if the type of the specified expression is a string.</span></span>  
  
 <span data-ttu-id="60630-935">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-935">**Syntax**</span></span>  
  
```  
IS_STRING(<expression>)  
```  
  
 <span data-ttu-id="60630-936">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-936">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="60630-937">É qualquer expressão válida.</span><span class="sxs-lookup"><span data-stu-id="60630-937">Is any valid expression.</span></span>  
  
 <span data-ttu-id="60630-938">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-938">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-939">Retorna uma expressão booliana.</span><span class="sxs-lookup"><span data-stu-id="60630-939">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="60630-940">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-940">**Examples**</span></span>  
  
 <span data-ttu-id="60630-941">O exemplo a seguir verifica objetos JSON booliano, número, cadeia de caracteres, nulo, objeto, matriz e tipos indefinidos usando a função IS_STRING.</span><span class="sxs-lookup"><span data-stu-id="60630-941">The following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using the IS_STRING function.</span></span>  
  
```  
SELECT   
       IS_STRING(true),   
       IS_STRING(1),  
       IS_STRING("value"),   
       IS_STRING(null),  
       IS_STRING({prop: "value"}),   
       IS_STRING([1, 2, 3]),  
       IS_STRING({prop: "value"}.prop2)  
```  
  
 <span data-ttu-id="60630-942">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-942">Here is the result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <span data-ttu-id="60630-943"><a name="bk_string_functions"></a> Funções de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="60630-943"><a name="bk_string_functions"></a> String functions</span></span>  
 <span data-ttu-id="60630-944">As funções escalares a seguir executam uma operação em um valor de cadeia de caracteres de entrada e retornam uma cadeia de caracteres, um valor numérico ou um valor booliano.</span><span class="sxs-lookup"><span data-stu-id="60630-944">The following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="60630-945">CONCAT</span><span class="sxs-lookup"><span data-stu-id="60630-945">CONCAT</span></span>](#bk_concat)|[<span data-ttu-id="60630-946">CONTAINS</span><span class="sxs-lookup"><span data-stu-id="60630-946">CONTAINS</span></span>](#bk_contains)|[<span data-ttu-id="60630-947">ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="60630-947">ENDSWITH</span></span>](#bk_endswith)|  
|[<span data-ttu-id="60630-948">INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="60630-948">INDEX_OF</span></span>](#bk_index_of)|[<span data-ttu-id="60630-949">LEFT</span><span class="sxs-lookup"><span data-stu-id="60630-949">LEFT</span></span>](#bk_left)|[<span data-ttu-id="60630-950">COMPRIMENTO</span><span class="sxs-lookup"><span data-stu-id="60630-950">LENGTH</span></span>](#bk_length)|  
|[<span data-ttu-id="60630-951">LOWER</span><span class="sxs-lookup"><span data-stu-id="60630-951">LOWER</span></span>](#bk_lower)|[<span data-ttu-id="60630-952">LTRIM</span><span class="sxs-lookup"><span data-stu-id="60630-952">LTRIM</span></span>](#bk_ltrim)|[<span data-ttu-id="60630-953">REPLACE</span><span class="sxs-lookup"><span data-stu-id="60630-953">REPLACE</span></span>](#bk_replace)|  
|[<span data-ttu-id="60630-954">REPLICATE</span><span class="sxs-lookup"><span data-stu-id="60630-954">REPLICATE</span></span>](#bk_replicate)|[<span data-ttu-id="60630-955">REVERSE</span><span class="sxs-lookup"><span data-stu-id="60630-955">REVERSE</span></span>](#bk_reverse)|[<span data-ttu-id="60630-956">RIGHT</span><span class="sxs-lookup"><span data-stu-id="60630-956">RIGHT</span></span>](#bk_right)|  
|[<span data-ttu-id="60630-957">RTRIM</span><span class="sxs-lookup"><span data-stu-id="60630-957">RTRIM</span></span>](#bk_rtrim)|[<span data-ttu-id="60630-958">STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="60630-958">STARTSWITH</span></span>](#bk_startswith)|[<span data-ttu-id="60630-959">SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="60630-959">SUBSTRING</span></span>](#bk_substring)|  
|[<span data-ttu-id="60630-960">UPPER</span><span class="sxs-lookup"><span data-stu-id="60630-960">UPPER</span></span>](#bk_upper)|||  
  
####  <span data-ttu-id="60630-961"><a name="bk_concat"></a> CONCAT</span><span class="sxs-lookup"><span data-stu-id="60630-961"><a name="bk_concat"></a> CONCAT</span></span>  
 <span data-ttu-id="60630-962">Retorna uma cadeia de caracteres que é o resultado da concatenação de dois ou mais valores de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="60630-962">Returns a string that is the result of concatenating two or more string values.</span></span>  
  
 <span data-ttu-id="60630-963">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-963">**Syntax**</span></span>  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 <span data-ttu-id="60630-964">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-964">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="60630-965">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="60630-965">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="60630-966">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-966">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-967">Retorna uma expressão de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="60630-967">Returns a string expression.</span></span>  
  
 <span data-ttu-id="60630-968">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-968">**Examples**</span></span>  
  
 <span data-ttu-id="60630-969">O exemplo a seguir retorna a cadeia de caracteres concatenada do valor especificado.</span><span class="sxs-lookup"><span data-stu-id="60630-969">The following example returns the concatenated string of the specified values.</span></span>  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 <span data-ttu-id="60630-970">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-970">Here is the result set.</span></span>  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <span data-ttu-id="60630-971"><a name="bk_contains"></a> CONTAINS</span><span class="sxs-lookup"><span data-stu-id="60630-971"><a name="bk_contains"></a> CONTAINS</span></span>  
 <span data-ttu-id="60630-972">Retorna um valor booliano que indica se a primeira expressão de cadeia de caracteres contém a segunda.</span><span class="sxs-lookup"><span data-stu-id="60630-972">Returns a Boolean indicating whether the first string expression contains the second.</span></span>  
  
 <span data-ttu-id="60630-973">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-973">**Syntax**</span></span>  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="60630-974">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-974">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="60630-975">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="60630-975">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="60630-976">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-976">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-977">Retorna uma expressão booliana.</span><span class="sxs-lookup"><span data-stu-id="60630-977">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="60630-978">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-978">**Examples**</span></span>  
  
 <span data-ttu-id="60630-979">O exemplo a seguir verifica se "abc" contém "ab" e contém "d".</span><span class="sxs-lookup"><span data-stu-id="60630-979">The following example checks if "abc" contains "ab" and contains "d".</span></span>  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 <span data-ttu-id="60630-980">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-980">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="60630-981"><a name="bk_endswith"></a> ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="60630-981"><a name="bk_endswith"></a> ENDSWITH</span></span>  
 <span data-ttu-id="60630-982">Retorna um valor booliano que indica se a primeira expressão de cadeia de caracteres termina com a segunda.</span><span class="sxs-lookup"><span data-stu-id="60630-982">Returns a Boolean indicating whether the first string expression ends with the second.</span></span>  
  
 <span data-ttu-id="60630-983">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-983">**Syntax**</span></span>  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="60630-984">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-984">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="60630-985">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="60630-985">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="60630-986">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-986">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-987">Retorna uma expressão booliana.</span><span class="sxs-lookup"><span data-stu-id="60630-987">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="60630-988">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-988">**Examples**</span></span>  
  
 <span data-ttu-id="60630-989">O exemplo a seguir retorna "abc" terminando com "b" e "bc".</span><span class="sxs-lookup"><span data-stu-id="60630-989">The following example returns the "abc" ends with "b" and "bc".</span></span>  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 <span data-ttu-id="60630-990">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-990">Here is the result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="60630-991"><a name="bk_index_of"></a>INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="60630-991"><a name="bk_index_of"></a> INDEX_OF</span></span>  
 <span data-ttu-id="60630-992">Retorna a posição inicial da primeira ocorrência da segunda expressão de cadeia de caracteres dentro da primeira expressão de cadeia de caracteres especificada, ou -1 se a cadeia de caracteres não for encontrada.</span><span class="sxs-lookup"><span data-stu-id="60630-992">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span>  
  
 <span data-ttu-id="60630-993">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-993">**Syntax**</span></span>  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="60630-994">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-994">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="60630-995">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="60630-995">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="60630-996">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-996">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-997">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-997">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-998">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-998">**Examples**</span></span>  
  
 <span data-ttu-id="60630-999">O exemplo a seguir retorna o índice de diversas subcadeias de caracteres dentro de "abc".</span><span class="sxs-lookup"><span data-stu-id="60630-999">The following example returns the index of various substrings inside "abc".</span></span>  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 <span data-ttu-id="60630-1000">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-1000">Here is the result set.</span></span>  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <span data-ttu-id="60630-1001"><a name="bk_left"></a> ESQUERDA</span><span class="sxs-lookup"><span data-stu-id="60630-1001"><a name="bk_left"></a> LEFT</span></span>  
 <span data-ttu-id="60630-1002">Retorna a parte esquerda de uma cadeia de caracteres com o número especificado de caracteres.</span><span class="sxs-lookup"><span data-stu-id="60630-1002">Returns the left part of a string with the specified number of characters.</span></span>  
  
 <span data-ttu-id="60630-1003">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-1003">**Syntax**</span></span>  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="60630-1004">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-1004">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="60630-1005">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="60630-1005">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="60630-1006">É qualquer expressão numérica válida.</span><span class="sxs-lookup"><span data-stu-id="60630-1006">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="60630-1007">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-1007">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-1008">Retorna uma expressão de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="60630-1008">Returns a string expression.</span></span>  
  
 <span data-ttu-id="60630-1009">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-1009">**Examples**</span></span>  
  
 <span data-ttu-id="60630-1010">O exemplo a seguir retorna a parte esquerda de "abc" para vários valores de comprimento.</span><span class="sxs-lookup"><span data-stu-id="60630-1010">The following example returns the left part of "abc" for various length values.</span></span>  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 <span data-ttu-id="60630-1011">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-1011">Here is the result set.</span></span>  
  
```  
[{"$1": "ab", "$2": "ab"}]  
```  
  
####  <span data-ttu-id="60630-1012"><a name="bk_length"></a> COMPRIMENTO</span><span class="sxs-lookup"><span data-stu-id="60630-1012"><a name="bk_length"></a> LENGTH</span></span>  
 <span data-ttu-id="60630-1013">Retorna o número de caracteres da expressão de cadeia de caracteres especificada.</span><span class="sxs-lookup"><span data-stu-id="60630-1013">Returns the number of characters of the specified string expression.</span></span>  
  
 <span data-ttu-id="60630-1014">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-1014">**Syntax**</span></span>  
  
```  
LENGTH(<str_expr>)  
```  
  
 <span data-ttu-id="60630-1015">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-1015">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="60630-1016">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="60630-1016">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="60630-1017">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-1017">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-1018">Retorna uma expressão de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="60630-1018">Returns a string expression.</span></span>  
  
 <span data-ttu-id="60630-1019">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-1019">**Examples**</span></span>  
  
 <span data-ttu-id="60630-1020">O exemplo a seguir retorna o comprimento de uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="60630-1020">The following example returns the length of a string.</span></span>  
  
```  
SELECT LENGTH("abc")  
```  
  
 <span data-ttu-id="60630-1021">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-1021">Here is the result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="60630-1022"><a name="bk_lower"></a> LOWER</span><span class="sxs-lookup"><span data-stu-id="60630-1022"><a name="bk_lower"></a> LOWER</span></span>  
 <span data-ttu-id="60630-1023">Retorna uma expressão de cadeia de caracteres depois de converter dados de caracteres maiúsculos em minúsculos.</span><span class="sxs-lookup"><span data-stu-id="60630-1023">Returns a string expression after converting uppercase character data to lowercase.</span></span>  
  
 <span data-ttu-id="60630-1024">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-1024">**Syntax**</span></span>  
  
```  
LOWER(<str_expr>)  
```  
  
 <span data-ttu-id="60630-1025">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-1025">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="60630-1026">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="60630-1026">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="60630-1027">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-1027">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-1028">Retorna uma expressão de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="60630-1028">Returns a string expression.</span></span>  
  
 <span data-ttu-id="60630-1029">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-1029">**Examples**</span></span>  
  
 <span data-ttu-id="60630-1030">O exemplo a seguir mostra como usar LOWER em uma consulta.</span><span class="sxs-lookup"><span data-stu-id="60630-1030">The following example shows how to use LOWER in a query.</span></span>  
  
```  
SELECT LOWER("Abc")  
```  
  
 <span data-ttu-id="60630-1031">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-1031">Here is the result set.</span></span>  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <span data-ttu-id="60630-1032"><a name="bk_ltrim"></a> LTRIM</span><span class="sxs-lookup"><span data-stu-id="60630-1032"><a name="bk_ltrim"></a> LTRIM</span></span>  
 <span data-ttu-id="60630-1033">Retorna uma expressão de cadeia de caracteres após remover os espaços em branco iniciais.</span><span class="sxs-lookup"><span data-stu-id="60630-1033">Returns a string expression after it removes leading blanks.</span></span>  
  
 <span data-ttu-id="60630-1034">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-1034">**Syntax**</span></span>  
  
```  
LTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="60630-1035">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-1035">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="60630-1036">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="60630-1036">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="60630-1037">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-1037">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-1038">Retorna uma expressão de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="60630-1038">Returns a string expression.</span></span>  
  
 <span data-ttu-id="60630-1039">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-1039">**Examples**</span></span>  
  
 <span data-ttu-id="60630-1040">O exemplo a seguir mostra como usar LTRIM em uma consulta.</span><span class="sxs-lookup"><span data-stu-id="60630-1040">The following example shows how to use LTRIM inside a query.</span></span>  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 <span data-ttu-id="60630-1041">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-1041">Here is the result set.</span></span>  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <span data-ttu-id="60630-1042"><a name="bk_replace"></a> SUBSTITUIR</span><span class="sxs-lookup"><span data-stu-id="60630-1042"><a name="bk_replace"></a> REPLACE</span></span>  
 <span data-ttu-id="60630-1043">Substitui todas as ocorrências de um valor de cadeia de caracteres especificado por outro valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="60630-1043">Replaces all occurrences of a specified string value with another string value.</span></span>  
  
 <span data-ttu-id="60630-1044">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-1044">**Syntax**</span></span>  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="60630-1045">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-1045">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="60630-1046">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="60630-1046">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="60630-1047">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-1047">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-1048">Retorna uma expressão de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="60630-1048">Returns a string expression.</span></span>  
  
 <span data-ttu-id="60630-1049">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-1049">**Examples**</span></span>  
  
 <span data-ttu-id="60630-1050">O exemplo a seguir mostra como usar REPLACE em uma consulta.</span><span class="sxs-lookup"><span data-stu-id="60630-1050">The following example shows how to use REPLACE in a query.</span></span>  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 <span data-ttu-id="60630-1051">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-1051">Here is the result set.</span></span>  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <span data-ttu-id="60630-1052"><a name="bk_replicate"></a> REPLICATE</span><span class="sxs-lookup"><span data-stu-id="60630-1052"><a name="bk_replicate"></a> REPLICATE</span></span>  
 <span data-ttu-id="60630-1053">Repete um valor de cadeia de caracteres por um número de vezes especificado.</span><span class="sxs-lookup"><span data-stu-id="60630-1053">Repeats a string value a specified number of times.</span></span>  
  
 <span data-ttu-id="60630-1054">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-1054">**Syntax**</span></span>  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="60630-1055">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-1055">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="60630-1056">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="60630-1056">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="60630-1057">É qualquer expressão numérica válida.</span><span class="sxs-lookup"><span data-stu-id="60630-1057">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="60630-1058">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-1058">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-1059">Retorna uma expressão de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="60630-1059">Returns a string expression.</span></span>  
  
 <span data-ttu-id="60630-1060">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-1060">**Examples**</span></span>  
  
 <span data-ttu-id="60630-1061">O exemplo a seguir mostra como usar REPLICATE em uma consulta.</span><span class="sxs-lookup"><span data-stu-id="60630-1061">The following example shows how to use REPLICATE in a query.</span></span>  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 <span data-ttu-id="60630-1062">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-1062">Here is the result set.</span></span>  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <span data-ttu-id="60630-1063"><a name="bk_reverse"></a> REVERSE</span><span class="sxs-lookup"><span data-stu-id="60630-1063"><a name="bk_reverse"></a> REVERSE</span></span>  
 <span data-ttu-id="60630-1064">Retorna a ordem inversa de um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="60630-1064">Returns the reverse order of a string value.</span></span>  
  
 <span data-ttu-id="60630-1065">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-1065">**Syntax**</span></span>  
  
```  
REVERSE(<str_expr>)  
```  
  
 <span data-ttu-id="60630-1066">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-1066">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="60630-1067">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="60630-1067">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="60630-1068">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-1068">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-1069">Retorna uma expressão de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="60630-1069">Returns a string expression.</span></span>  
  
 <span data-ttu-id="60630-1070">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-1070">**Examples**</span></span>  
  
 <span data-ttu-id="60630-1071">O exemplo a seguir mostra como usar REVERSE em uma consulta.</span><span class="sxs-lookup"><span data-stu-id="60630-1071">The following example shows how to use REVERSE in a query.</span></span>  
  
```  
SELECT REVERSE("Abc")  
```  
  
 <span data-ttu-id="60630-1072">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-1072">Here is the result set.</span></span>  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <span data-ttu-id="60630-1073"><a name="bk_right"></a> RIGHT</span><span class="sxs-lookup"><span data-stu-id="60630-1073"><a name="bk_right"></a> RIGHT</span></span>  
 <span data-ttu-id="60630-1074">Retorna a parte direita de uma cadeia de caracteres com o número especificado de caracteres.</span><span class="sxs-lookup"><span data-stu-id="60630-1074">Returns the right part of a string with the specified number of characters.</span></span>  
  
 <span data-ttu-id="60630-1075">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-1075">**Syntax**</span></span>  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="60630-1076">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-1076">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="60630-1077">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="60630-1077">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="60630-1078">É qualquer expressão numérica válida.</span><span class="sxs-lookup"><span data-stu-id="60630-1078">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="60630-1079">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-1079">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-1080">Retorna uma expressão de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="60630-1080">Returns a string expression.</span></span>  
  
 <span data-ttu-id="60630-1081">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-1081">**Examples**</span></span>  
  
 <span data-ttu-id="60630-1082">O exemplo a seguir retorna a parte direita de "abc" para vários valores de comprimento.</span><span class="sxs-lookup"><span data-stu-id="60630-1082">The following example returns the right part of "abc" for various length values.</span></span>  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 <span data-ttu-id="60630-1083">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-1083">Here is the result set.</span></span>  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <span data-ttu-id="60630-1084"><a name="bk_rtrim"></a> RTRIM</span><span class="sxs-lookup"><span data-stu-id="60630-1084"><a name="bk_rtrim"></a> RTRIM</span></span>  
 <span data-ttu-id="60630-1085">Retorna uma expressão de cadeia de caracteres após remover os espaços em branco finais.</span><span class="sxs-lookup"><span data-stu-id="60630-1085">Returns a string expression after it removes trailing blanks.</span></span>  
  
 <span data-ttu-id="60630-1086">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-1086">**Syntax**</span></span>  
  
```  
RTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="60630-1087">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-1087">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="60630-1088">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="60630-1088">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="60630-1089">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-1089">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-1090">Retorna uma expressão de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="60630-1090">Returns a string expression.</span></span>  
  
 <span data-ttu-id="60630-1091">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-1091">**Examples**</span></span>  
  
 <span data-ttu-id="60630-1092">O exemplo a seguir mostra como usar RTRIM em uma consulta.</span><span class="sxs-lookup"><span data-stu-id="60630-1092">The following example shows how to use RTRIM inside a query.</span></span>  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 <span data-ttu-id="60630-1093">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-1093">Here is the result set.</span></span>  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <span data-ttu-id="60630-1094"><a name="bk_startswith"></a> STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="60630-1094"><a name="bk_startswith"></a> STARTSWITH</span></span>  
 <span data-ttu-id="60630-1095">Retorna um valor booliano que indica se a primeira expressão de cadeia de caracteres começa com a segunda.</span><span class="sxs-lookup"><span data-stu-id="60630-1095">Returns a Boolean indicating whether the first string expression starts with the second.</span></span>  
  
 <span data-ttu-id="60630-1096">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-1096">**Syntax**</span></span>  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="60630-1097">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-1097">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="60630-1098">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="60630-1098">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="60630-1099">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-1099">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-1100">Retorna uma expressão booliana.</span><span class="sxs-lookup"><span data-stu-id="60630-1100">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="60630-1101">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-1101">**Examples**</span></span>  
  
 <span data-ttu-id="60630-1102">O exemplo a seguir verifica se a cadeia de caracteres "abc" começa com "b" e "a".</span><span class="sxs-lookup"><span data-stu-id="60630-1102">The following example checks if the string "abc" begins with "b" and "a".</span></span>  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 <span data-ttu-id="60630-1103">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-1103">Here is the result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="60630-1104"><a name="bk_substring"></a> SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="60630-1104"><a name="bk_substring"></a> SUBSTRING</span></span>  
 <span data-ttu-id="60630-1105">Retorna parte de uma expressão de cadeia de caracteres começando na posição baseada em zero do caractere especificado e continua até o comprimento especificado ou até o final da cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="60630-1105">Returns part of a string expression starting at the specified character zero-based position and continues to the specified length, or to the end of the string.</span></span>  
  
 <span data-ttu-id="60630-1106">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-1106">**Syntax**</span></span>  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="60630-1107">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-1107">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="60630-1108">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="60630-1108">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="60630-1109">É qualquer expressão numérica válida.</span><span class="sxs-lookup"><span data-stu-id="60630-1109">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="60630-1110">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-1110">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-1111">Retorna uma expressão de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="60630-1111">Returns a string expression.</span></span>  
  
 <span data-ttu-id="60630-1112">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-1112">**Examples**</span></span>  
  
 <span data-ttu-id="60630-1113">O exemplo a seguir retorna a subcadeia de caracteres de "abc" começando em 1 e com o comprimento de 1 caractere.</span><span class="sxs-lookup"><span data-stu-id="60630-1113">The following example returns the substring of "abc" starting at 1 and for a length of 1 character.</span></span>  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 <span data-ttu-id="60630-1114">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-1114">Here is the result set.</span></span>  
  
```  
[{"$1": "b"}]  
```  
  
####  <span data-ttu-id="60630-1115"><a name="bk_upper"></a> UPPER</span><span class="sxs-lookup"><span data-stu-id="60630-1115"><a name="bk_upper"></a> UPPER</span></span>  
 <span data-ttu-id="60630-1116">Retorna uma expressão de cadeia de caracteres depois de converter dados de caracteres minúsculos em maiúsculos.</span><span class="sxs-lookup"><span data-stu-id="60630-1116">Returns a string expression after converting lowercase character data to uppercase.</span></span>  
  
 <span data-ttu-id="60630-1117">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-1117">**Syntax**</span></span>  
  
```  
UPPER(<str_expr>)  
```  
  
 <span data-ttu-id="60630-1118">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-1118">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="60630-1119">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="60630-1119">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="60630-1120">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-1120">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-1121">Retorna uma expressão de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="60630-1121">Returns a string expression.</span></span>  
  
 <span data-ttu-id="60630-1122">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-1122">**Examples**</span></span>  
  
 <span data-ttu-id="60630-1123">O exemplo abaixo mostra como usar UPPER em uma consulta</span><span class="sxs-lookup"><span data-stu-id="60630-1123">The following example shows how to use UPPER in a query</span></span>  
  
```  
SELECT UPPER("Abc")  
```  
  
 <span data-ttu-id="60630-1124">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-1124">Here is the result set.</span></span>  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <span data-ttu-id="60630-1125"><a name="bk_array_functions"></a> Funções de matriz</span><span class="sxs-lookup"><span data-stu-id="60630-1125"><a name="bk_array_functions"></a> Array functions</span></span>  
 <span data-ttu-id="60630-1126">As funções escalares a seguir executam uma operação em um valor de matriz de entrada e retornam um valor numérico, booliano ou um valor de matriz</span><span class="sxs-lookup"><span data-stu-id="60630-1126">The following scalar functions perform an operation on an array input value and return numeric, Boolean or array value</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="60630-1127">ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="60630-1127">ARRAY_CONCAT</span></span>](#bk_array_concat)|[<span data-ttu-id="60630-1128">ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="60630-1128">ARRAY_CONTAINS</span></span>](#bk_array_contains)|[<span data-ttu-id="60630-1129">ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="60630-1129">ARRAY_LENGTH</span></span>](#bk_array_length)|  
|[<span data-ttu-id="60630-1130">ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="60630-1130">ARRAY_SLICE</span></span>](#bk_array_slice)|||  
  
####  <span data-ttu-id="60630-1131"><a name="bk_array_concat"></a>ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="60630-1131"><a name="bk_array_concat"></a> ARRAY_CONCAT</span></span>  
 <span data-ttu-id="60630-1132">Retorna uma matriz que é o resultado da concatenação de dois ou mais valores de matriz.</span><span class="sxs-lookup"><span data-stu-id="60630-1132">Returns an array that is the result of concatenating two or more array values.</span></span>  
  
 <span data-ttu-id="60630-1133">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-1133">**Syntax**</span></span>  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 <span data-ttu-id="60630-1134">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-1134">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="60630-1135">É qualquer expressão válida de matriz.</span><span class="sxs-lookup"><span data-stu-id="60630-1135">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="60630-1136">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-1136">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-1137">Retorna uma expressão de matriz.</span><span class="sxs-lookup"><span data-stu-id="60630-1137">Returns an array expression.</span></span>  
  
 <span data-ttu-id="60630-1138">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-1138">**Examples**</span></span>  
  
 <span data-ttu-id="60630-1139">O exemplo a seguir mostra como concatenar duas matrizes.</span><span class="sxs-lookup"><span data-stu-id="60630-1139">The following example how to concatenate two arrays.</span></span>  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 <span data-ttu-id="60630-1140">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-1140">Here is the result set.</span></span>  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <span data-ttu-id="60630-1141"><a name="bk_array_contains"></a>ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="60630-1141"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span></span>  
 <span data-ttu-id="60630-1142">Retorna um valor booliano que indica se a matriz contém o valor especificado.</span><span class="sxs-lookup"><span data-stu-id="60630-1142">Returns a Boolean indicating whether the array contains the specified value.</span></span>  
  
 <span data-ttu-id="60630-1143">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-1143">**Syntax**</span></span>  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr>)  
```  
  
 <span data-ttu-id="60630-1144">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-1144">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="60630-1145">É qualquer expressão válida de matriz.</span><span class="sxs-lookup"><span data-stu-id="60630-1145">Is any valid array expression.</span></span>  
  
-   `expr`  
  
     <span data-ttu-id="60630-1146">É qualquer expressão válida.</span><span class="sxs-lookup"><span data-stu-id="60630-1146">Is any valid expression.</span></span>  
  
 <span data-ttu-id="60630-1147">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-1147">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-1148">Retorna um valor booliano.</span><span class="sxs-lookup"><span data-stu-id="60630-1148">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="60630-1149">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-1149">**Examples**</span></span>  
  
 <span data-ttu-id="60630-1150">O exemplo a seguir mostra como verificar a associação em uma matriz usando ARRAY_CONTAINS.</span><span class="sxs-lookup"><span data-stu-id="60630-1150">The following example how to check for membership in an array using ARRAY_CONTAINS.</span></span>  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 <span data-ttu-id="60630-1151">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-1151">Here is the result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="60630-1152"><a name="bk_array_length"></a>ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="60630-1152"><a name="bk_array_length"></a> ARRAY_LENGTH</span></span>  
 <span data-ttu-id="60630-1153">Retorna o número de elementos da expressão de matriz especificada.</span><span class="sxs-lookup"><span data-stu-id="60630-1153">Returns the number of elements of the specified array expression.</span></span>  
  
 <span data-ttu-id="60630-1154">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-1154">**Syntax**</span></span>  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 <span data-ttu-id="60630-1155">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-1155">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="60630-1156">É qualquer expressão válida de matriz.</span><span class="sxs-lookup"><span data-stu-id="60630-1156">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="60630-1157">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-1157">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-1158">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="60630-1158">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="60630-1159">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-1159">**Examples**</span></span>  
  
 <span data-ttu-id="60630-1160">O exemplo a seguir mostra como obter o comprimento de uma matriz usando ARRAY_LENGTH.</span><span class="sxs-lookup"><span data-stu-id="60630-1160">The following example how to get the length of an array using ARRAY_LENGTH.</span></span>  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 <span data-ttu-id="60630-1161">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-1161">Here is the result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="60630-1162"><a name="bk_array_slice"></a>ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="60630-1162"><a name="bk_array_slice"></a> ARRAY_SLICE</span></span>  
 <span data-ttu-id="60630-1163">Retorna parte de uma expressão de matriz.</span><span class="sxs-lookup"><span data-stu-id="60630-1163">Returns part of an array expression.</span></span>
  
 <span data-ttu-id="60630-1164">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-1164">**Syntax**</span></span>  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="60630-1165">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-1165">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="60630-1166">É qualquer expressão válida de matriz.</span><span class="sxs-lookup"><span data-stu-id="60630-1166">Is any valid array expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="60630-1167">É qualquer expressão numérica válida.</span><span class="sxs-lookup"><span data-stu-id="60630-1167">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="60630-1168">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-1168">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-1169">Retorna um valor booliano.</span><span class="sxs-lookup"><span data-stu-id="60630-1169">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="60630-1170">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-1170">**Examples**</span></span>  
  
 <span data-ttu-id="60630-1171">O exemplo a seguir mostra como obter uma parte de uma matriz usando ARRAY_SLICE.</span><span class="sxs-lookup"><span data-stu-id="60630-1171">The following example how to get a part of an array using ARRAY_SLICE.</span></span>  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 <span data-ttu-id="60630-1172">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-1172">Here is the result set.</span></span>  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <span data-ttu-id="60630-1173"><a name="bk_spatial_functions"></a> Funções espaciais</span><span class="sxs-lookup"><span data-stu-id="60630-1173"><a name="bk_spatial_functions"></a> Spatial functions</span></span>  
 <span data-ttu-id="60630-1174">As funções escalares a seguir executam uma operação em um valor de entrada de objeto espacial e retornam um valor numérico ou um valor booliano.</span><span class="sxs-lookup"><span data-stu-id="60630-1174">The following scalar functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="60630-1175">ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="60630-1175">ST_DISTANCE</span></span>](#bk_st_distance)|[<span data-ttu-id="60630-1176">ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="60630-1176">ST_WITHIN</span></span>](#bk_st_within)|[<span data-ttu-id="60630-1177">ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="60630-1177">ST_INTERSECTS</span></span>](#bk_st_intersects)|[<span data-ttu-id="60630-1178">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="60630-1178">ST_ISVALID</span></span>](#bk_st_isvalid)|  
|[<span data-ttu-id="60630-1179">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="60630-1179">ST_ISVALIDDETAILED</span></span>](#bk_st_isvaliddetailed)|||  
  
####  <span data-ttu-id="60630-1180"><a name="bk_st_distance"></a> ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="60630-1180"><a name="bk_st_distance"></a> ST_DISTANCE</span></span>  
 <span data-ttu-id="60630-1181">Retorna a distância entre as duas expressões de ponto GeoJSON, Polígono ou LineString.</span><span class="sxs-lookup"><span data-stu-id="60630-1181">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span>  
  
 <span data-ttu-id="60630-1182">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-1182">**Syntax**</span></span>  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="60630-1183">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-1183">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="60630-1184">É qualquer expressão de objeto Ponto GeoJSON, Polígono ou LineString válida.</span><span class="sxs-lookup"><span data-stu-id="60630-1184">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="60630-1185">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-1185">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-1186">Retorna uma expressão numérica que contém a distância.</span><span class="sxs-lookup"><span data-stu-id="60630-1186">Returns a numeric expression containing the distance.</span></span> <span data-ttu-id="60630-1187">Isso é expresso em metros no sistema de referência padrão.</span><span class="sxs-lookup"><span data-stu-id="60630-1187">This is expressed in meters for the default reference system.</span></span>  
  
 <span data-ttu-id="60630-1188">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-1188">**Examples**</span></span>  
  
 <span data-ttu-id="60630-1189">O exemplo a seguir mostra como retornar todos os documentos de família que estejam em um raio de 30 km do local especificado usando a função interna ST_DISTANCE.</span><span class="sxs-lookup"><span data-stu-id="60630-1189">The following example shows how to return all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> <span data-ttu-id="60630-1190">.</span><span class="sxs-lookup"><span data-stu-id="60630-1190">.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 <span data-ttu-id="60630-1191">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-1191">Here is the result set.</span></span>  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <span data-ttu-id="60630-1192"><a name="bk_st_within"></a> ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="60630-1192"><a name="bk_st_within"></a> ST_WITHIN</span></span>  
 <span data-ttu-id="60630-1193">Retorna uma expressão booliana que indica se o objeto GeoJSON (Ponto, Polígono ou LineString) especificado no primeiro argumento está dentro do GeoJSON (Ponto, Polígono ou LineString) no segundo argumento.</span><span class="sxs-lookup"><span data-stu-id="60630-1193">Returns a Boolean expression indicating whether the GeoJSON object (Point, Polygon, or LineString) specified in the first argument is within the GeoJSON (Point, Polygon, or LineString) in the second argument.</span></span>  
  
 <span data-ttu-id="60630-1194">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-1194">**Syntax**</span></span>  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="60630-1195">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-1195">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="60630-1196">É qualquer expressão de objeto Ponto GeoJSON, Polígono ou LineString válida.</span><span class="sxs-lookup"><span data-stu-id="60630-1196">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="60630-1197">É qualquer expressão de objeto Ponto GeoJSON, Polígono ou LineString válida.</span><span class="sxs-lookup"><span data-stu-id="60630-1197">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="60630-1198">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-1198">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-1199">Retorna um valor booliano.</span><span class="sxs-lookup"><span data-stu-id="60630-1199">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="60630-1200">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-1200">**Examples**</span></span>  
  
 <span data-ttu-id="60630-1201">O exemplo a seguir mostra como localizar todos os documentos da família em um polígono usando ST_WITHIN.</span><span class="sxs-lookup"><span data-stu-id="60630-1201">The following example shows how to find all family documents within a polygon using ST_WITHIN.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="60630-1202">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-1202">Here is the result set.</span></span>  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <span data-ttu-id="60630-1203"><a name="bk_st_intersects"></a>ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="60630-1203"><a name="bk_st_intersects"></a> ST_INTERSECTS</span></span>  
 <span data-ttu-id="60630-1204">Retorna uma expressão booliana que indica se o objeto GeoJSON (ponto, polígono ou LineString) especificado no primeiro argumento intercepta o GeoJSON (ponto, polígono ou LineString) no segundo argumento.</span><span class="sxs-lookup"><span data-stu-id="60630-1204">Returns a Boolean expression indicating whether the GeoJSON object (Point, Polygon, or LineString) specified in the first argument intersects the GeoJSON (Point, Polygon, or LineString) in the second argument.</span></span>  
  
 <span data-ttu-id="60630-1205">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-1205">**Syntax**</span></span>  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="60630-1206">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-1206">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="60630-1207">É qualquer expressão de objeto Ponto GeoJSON, Polígono ou LineString válida.</span><span class="sxs-lookup"><span data-stu-id="60630-1207">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="60630-1208">É qualquer expressão de objeto Ponto GeoJSON, Polígono ou LineString válida.</span><span class="sxs-lookup"><span data-stu-id="60630-1208">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="60630-1209">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-1209">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-1210">Retorna um valor booliano.</span><span class="sxs-lookup"><span data-stu-id="60630-1210">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="60630-1211">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-1211">**Examples**</span></span>  
  
 <span data-ttu-id="60630-1212">O exemplo a seguir mostra como localizar todas as áreas que fazem interseção com o polígono determinado.</span><span class="sxs-lookup"><span data-stu-id="60630-1212">The following example shows how to find all areas that intersects with the given polygon.</span></span>  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="60630-1213">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-1213">Here is the result set.</span></span>  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <span data-ttu-id="60630-1214"><a name="bk_st_isvalid"></a> ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="60630-1214"><a name="bk_st_isvalid"></a> ST_ISVALID</span></span>  
 <span data-ttu-id="60630-1215">Retorna um valor Booliano que indica se a expressão especificada de Ponto, Polígono ou LineString GeoJSON é válida.</span><span class="sxs-lookup"><span data-stu-id="60630-1215">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span>  
  
 <span data-ttu-id="60630-1216">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-1216">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="60630-1217">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-1217">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="60630-1218">É qualquer expressão válida de LineString, polígono ou ponto GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="60630-1218">Is any valid GeoJSON Point, Polygon, or LineString expression.</span></span>  
  
 <span data-ttu-id="60630-1219">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-1219">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-1220">Retorna uma expressão booliana.</span><span class="sxs-lookup"><span data-stu-id="60630-1220">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="60630-1221">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-1221">**Examples**</span></span>  
  
 <span data-ttu-id="60630-1222">O exemplo a seguir mostra como verificar se um ponto é válido usando ST_VALID.</span><span class="sxs-lookup"><span data-stu-id="60630-1222">The following example shows how to check if a point is valid using ST_VALID.</span></span>  
  
 <span data-ttu-id="60630-1223">Por exemplo, esse ponto tem um valor de latitude que não está no intervalo de valores válido [-90, 90] e, portanto, a consulta retornará false.</span><span class="sxs-lookup"><span data-stu-id="60630-1223">For example, this point has a latitude value that's not in the valid range of values [-90, 90], so the query returns false.</span></span>  
  
 <span data-ttu-id="60630-1224">No caso dos polígonos, a especificação GeoJSON exige que o último par de coordenadas fornecido seja igual ao primeiro para criar uma forma fechada.</span><span class="sxs-lookup"><span data-stu-id="60630-1224">For polygons, the GeoJSON specification requires that the last coordinate pair provided should be the same as the first, to create a closed shape.</span></span> <span data-ttu-id="60630-1225">Os pontos em um polígono devem ser especificados no sentido anti-horário.</span><span class="sxs-lookup"><span data-stu-id="60630-1225">Points within a polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="60630-1226">Um polígono especificado no sentido horário representa o inverso da região dentro dele.</span><span class="sxs-lookup"><span data-stu-id="60630-1226">A polygon specified in clockwise order represents the inverse of the region within it.</span></span>  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 <span data-ttu-id="60630-1227">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-1227">Here is the result set.</span></span>  
  
```  
[{ "$1": false }]  
```  
  
####  <span data-ttu-id="60630-1228"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="60630-1228"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span></span>  
 <span data-ttu-id="60630-1229">Retorna um valor JSON que contém um valor Booliano caso a expressão especificada de Ponto, Polígono ou LineString GeoJSON é válida e, se for inválida, adicionalmente o motivo como um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="60630-1229">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span>  
  
 <span data-ttu-id="60630-1230">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="60630-1230">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="60630-1231">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="60630-1231">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="60630-1232">É qualquer expressão válida de ponto ou polígono GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="60630-1232">Is any valid GeoJSON point or polygon expression.</span></span>  
  
 <span data-ttu-id="60630-1233">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="60630-1233">**Return Types**</span></span>  
  
 <span data-ttu-id="60630-1234">Retorna um valor JSON que contém um valor Booliano caso a expressão de ponto ou polígono GeoJSON especificada é válida e, se for inválida, adicionalmente o motivo como um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="60630-1234">Returns a JSON value containing a Boolean value if the specified GeoJSON point or polygon expression is valid, and if invalid, additionally the reason as a string value.</span></span>  
  
 <span data-ttu-id="60630-1235">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="60630-1235">**Examples**</span></span>  
  
 <span data-ttu-id="60630-1236">O exemplo a seguir mostra como verificar a validade (com detalhes) usando ST_ISVALIDDETAILED.</span><span class="sxs-lookup"><span data-stu-id="60630-1236">The following example how to check validity (with details) using ST_ISVALIDDETAILED.</span></span>  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 <span data-ttu-id="60630-1237">Este é o conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="60630-1237">Here is the result set.</span></span>  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "The Polygon input is not valid because the start and end points of the ring number 1 are not the same. Each ring of a polygon must have the same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a><span data-ttu-id="60630-1238">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="60630-1238">Next steps</span></span>  
 <span data-ttu-id="60630-1239">[Sintaxe SQL e consulta SQL para BD Cosmos do Azure](documentdb-sql-query.md) </span><span class="sxs-lookup"><span data-stu-id="60630-1239">[SQL syntax and SQL query for Azure Cosmos DB](documentdb-sql-query.md) </span></span>  
 [<span data-ttu-id="60630-1240">Documentação do BD Cosmos do Azure</span><span class="sxs-lookup"><span data-stu-id="60630-1240">Azure Cosmos DB documentation</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/)  
  
  
