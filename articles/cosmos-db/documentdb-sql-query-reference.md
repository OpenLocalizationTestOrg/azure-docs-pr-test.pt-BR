---
<span data-ttu-id="27f42-101">título: aaa "API DocumentDB do Azure Cosmos DB: sintaxe SQL | Descrição de Microsoft Docs": documentação para Olá linguagem de consulta SQL de API do DocumentDB do Azure Cosmos banco de dados de referência.</span><span class="sxs-lookup"><span data-stu-id="27f42-101">title: aaa"Azure Cosmos DB DocumentDB API: SQL syntax | Microsoft Docs" description: Reference documentation for hello Azure Cosmos DB DocumentDB API SQL query language.</span></span>
<span data-ttu-id="27f42-102">serviços: cosmos db autor: manager mimig1: jhubbard editor: mimig documentationcenter: '</span><span class="sxs-lookup"><span data-stu-id="27f42-102">services: cosmos-db author: mimig1 manager: jhubbard editor: mimig documentationcenter: ''</span></span>

<span data-ttu-id="27f42-103">MS. AssetID: MS. Service: cosmos db Workload: serviços de dados tgt_pltfrm: na MS. devlang: na MS. Topic: referência MS. Date: 13/06/2017 Author: mimig</span><span class="sxs-lookup"><span data-stu-id="27f42-103">ms.assetid: ms.service: cosmos-db ms.workload: data-services ms.tgt_pltfrm: na ms.devlang: na ms.topic: reference ms.date: 06/13/2017 ms.author: mimig</span></span>

---

# <a name="azure-cosmos-db-documentdb-api-sql-syntax-reference"></a><span data-ttu-id="27f42-104">API DocumentDB do BD Cosmos do Azure: referência de sintaxe SQL</span><span class="sxs-lookup"><span data-stu-id="27f42-104">Azure Cosmos DB DocumentDB API: SQL syntax reference</span></span>

<span data-ttu-id="27f42-105">Olá API DocumentDB do Azure Cosmos DB dá suporte a documentos de consultando usando um familiar SQL (Structured Query Language) como a gramática em documentos JSON hierárquicos sem a necessidade de esquema explícito ou a criação de índices secundários.</span><span class="sxs-lookup"><span data-stu-id="27f42-105">hello Azure Cosmos DB DocumentDB API supports querying documents using a familiar SQL (Structured Query Language) like grammar over hierarchical JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> <span data-ttu-id="27f42-106">Este tópico fornece documentação de referência para Olá linguagem de consulta SQL de API do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="27f42-106">This topic provides reference documentation for hello DocumentDB API SQL query language.</span></span>

<span data-ttu-id="27f42-107">Para obter uma explicação da saudação linguagem de consulta SQL de API de documentos, consulte [consultas SQL para a API DocumentDB do Azure Cosmos DB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="27f42-107">For a walkthrough of hello DocumentDB API SQL query language, see [SQL queries for Azure Cosmos DB DocumentDB API](documentdb-sql-query.md).</span></span>  
  
<span data-ttu-id="27f42-108">Também você está convidado Olá toovisit [parque de consulta](http://www.documentdb.com/sql/demo) onde você pode tentar o banco de dados do Azure Cosmos e executar consultas SQL em nosso conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="27f42-108">We also invite you toovisit hello [Query Playground](http://www.documentdb.com/sql/demo) where you can try Azure Cosmos DB and run SQL queries against our dataset.</span></span>  
  
## <a name="select-query"></a><span data-ttu-id="27f42-109">Consulta SELECT</span><span class="sxs-lookup"><span data-stu-id="27f42-109">SELECT query</span></span>  
<span data-ttu-id="27f42-110">Recupera documentos JSON do banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-110">Retrieves JSON documents from hello database.</span></span> <span data-ttu-id="27f42-111">Dá suporte a avaliação de expressão, projeções, filtragem e junções.</span><span class="sxs-lookup"><span data-stu-id="27f42-111">Supports expression evaluation, projections, filtering and joins.</span></span>  <span data-ttu-id="27f42-112">convenções de saudação usadas para descrever instruções SELECT Olá são tabuladas na Olá seção de convenções de sintaxe.</span><span class="sxs-lookup"><span data-stu-id="27f42-112">hello conventions used for describing hello SELECT statements are tabulated in hello Syntax conventions section.</span></span>  
  
<span data-ttu-id="27f42-113">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-113">**Syntax**</span></span>  
  
```
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 <span data-ttu-id="27f42-114">**Comentários**</span><span class="sxs-lookup"><span data-stu-id="27f42-114">**Remarks**</span></span>  
  
 <span data-ttu-id="27f42-115">Consulte as seguintes seções para obter detalhes sobre cada cláusula:</span><span class="sxs-lookup"><span data-stu-id="27f42-115">See following sections for details on each clause:</span></span>  
  
-   [<span data-ttu-id="27f42-116">Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="27f42-116">SELECT clause</span></span>](#bk_select_query)  
  
-   [<span data-ttu-id="27f42-117">Cláusula FROM</span><span class="sxs-lookup"><span data-stu-id="27f42-117">FROM clause</span></span>](#bk_from_clause)  
  
-   [<span data-ttu-id="27f42-118">Cláusula WHERE</span><span class="sxs-lookup"><span data-stu-id="27f42-118">WHERE clause</span></span>](#bk_where_clause)  
  
-   [<span data-ttu-id="27f42-119">Cláusula ORDER BY</span><span class="sxs-lookup"><span data-stu-id="27f42-119">ORDER BY clause</span></span>](#bk_orderby_clause)  
  
<span data-ttu-id="27f42-120">cláusulas de saudação na instrução SELECT Olá devem ser ordenadas, conforme mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="27f42-120">hello clauses in hello SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="27f42-121">Qualquer uma das cláusulas opcionais Olá pode ser omitida.</span><span class="sxs-lookup"><span data-stu-id="27f42-121">Any one of hello optional clauses can be omitted.</span></span> <span data-ttu-id="27f42-122">Mas quando são usadas, eles devem aparecer na ordem correta hello.</span><span class="sxs-lookup"><span data-stu-id="27f42-122">But when optional clauses are used, they must appear in hello right order.</span></span>  
  
<span data-ttu-id="27f42-123">**Ordem de processamento lógico da instrução SELECT Olá**</span><span class="sxs-lookup"><span data-stu-id="27f42-123">**Logical Processing Order of hello SELECT statement**</span></span>  
  
<span data-ttu-id="27f42-124">Olá ordem na qual as cláusulas são processadas é:</span><span class="sxs-lookup"><span data-stu-id="27f42-124">hello order in which clauses are processed is:</span></span>  

1.  [<span data-ttu-id="27f42-125">Cláusula FROM</span><span class="sxs-lookup"><span data-stu-id="27f42-125">FROM clause</span></span>](#bk_from_clause)  
2.  [<span data-ttu-id="27f42-126">Cláusula WHERE</span><span class="sxs-lookup"><span data-stu-id="27f42-126">WHERE clause</span></span>](#bk_where_clause)  
3.  [<span data-ttu-id="27f42-127">Cláusula ORDER BY</span><span class="sxs-lookup"><span data-stu-id="27f42-127">ORDER BY clause</span></span>](#bk_orderby_clause)  
4.  [<span data-ttu-id="27f42-128">Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="27f42-128">SELECT clause</span></span>](#bk_select_query)  

<span data-ttu-id="27f42-129">Observe que isso é diferente da saudação ordem em que aparecem na sintaxe de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-129">Note that this is different from hello order in which they appear in hello syntax.</span></span> <span data-ttu-id="27f42-130">Olá ordenação é tal que todos os símbolos novos introduzidos por uma cláusula processada são visíveis e podem ser usados em cláusulas processadas posteriormente.</span><span class="sxs-lookup"><span data-stu-id="27f42-130">hello ordering is such that all new symbols introduced by a processed clause are visible and can be used in clauses processed later.</span></span> <span data-ttu-id="27f42-131">Por exemplo, os aliases declarados em uma cláusula FROM podem ser acessados nas cláusulas SELECT e WHERE.</span><span class="sxs-lookup"><span data-stu-id="27f42-131">For instance, aliases declared in a FROM clause are accessible in WHERE and SELECT clauses.</span></span>  

<span data-ttu-id="27f42-132">**Comentários e caracteres de espaço em branco**</span><span class="sxs-lookup"><span data-stu-id="27f42-132">**Whitespace characters and comments**</span></span>  

<span data-ttu-id="27f42-133">Todos os caracteres de espaço em branco que não fazem parte de uma cadeia de caracteres entre aspas ou identificador entre aspas não fazem parte da gramática da linguagem hello e são ignorados durante a análise.</span><span class="sxs-lookup"><span data-stu-id="27f42-133">All white space characters which are not part of a quoted string or quoted identifier are not part of hello language grammar and are ignored during parsing.</span></span>  

<span data-ttu-id="27f42-134">oferece suporte a linguagem de consulta Hello como comentários de estilo do T-SQL</span><span class="sxs-lookup"><span data-stu-id="27f42-134">hello query language supports T-SQL style comments like</span></span>  

-   <span data-ttu-id="27f42-135">Instrução SQL`-- comment text [newline]`</span><span class="sxs-lookup"><span data-stu-id="27f42-135">SQL Statement `-- comment text [newline]`</span></span>  

<span data-ttu-id="27f42-136">Enquanto comentários e caracteres de espaço em branco não tenham nenhum significado na gramática hello, eles devem ser usados tooseparate tokens.</span><span class="sxs-lookup"><span data-stu-id="27f42-136">While whitespace characters and comments do not have any significance in hello grammar, they must be used tooseparate tokens.</span></span> <span data-ttu-id="27f42-137">Por exemplo: `-1e5` é um token de número único, ao passo que `: – 1 e5` é um token de sinal de subtração seguido pelo número 1 e identificador e5.</span><span class="sxs-lookup"><span data-stu-id="27f42-137">For instance: `-1e5` is a single number token, while`: – 1 e5` is a minus token followed by number 1 and identifier e5.</span></span>  

##  <span data-ttu-id="27f42-138"><a name="bk_select_query"></a> Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="27f42-138"><a name="bk_select_query"></a> SELECT clause</span></span>  
<span data-ttu-id="27f42-139">cláusulas de saudação na instrução SELECT Olá devem ser ordenadas, conforme mostrado acima.</span><span class="sxs-lookup"><span data-stu-id="27f42-139">hello clauses in hello SELECT statement must be ordered as shown above.</span></span> <span data-ttu-id="27f42-140">Qualquer uma das cláusulas opcionais Olá pode ser omitida.</span><span class="sxs-lookup"><span data-stu-id="27f42-140">Any one of hello optional clauses can be omitted.</span></span> <span data-ttu-id="27f42-141">Mas quando são usadas, eles devem aparecer na ordem correta hello.</span><span class="sxs-lookup"><span data-stu-id="27f42-141">But when optional clauses are used, they must appear in hello right order.</span></span>  

<span data-ttu-id="27f42-142">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-142">**Syntax**</span></span>  
```  
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 <span data-ttu-id="27f42-143">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-143">**Arguments**</span></span>  
  
 `<select_specification>`  
  
 <span data-ttu-id="27f42-144">Toobe propriedades ou o valor selecionado para o resultado de saudação definido.</span><span class="sxs-lookup"><span data-stu-id="27f42-144">Properties or value toobe selected for hello result set.</span></span>  
  
 `'*'`  
  
<span data-ttu-id="27f42-145">Especifica que o valor de saudação deve ser recuperado sem fazer alterações.</span><span class="sxs-lookup"><span data-stu-id="27f42-145">Specifies that hello value should be retrieved without making any changes.</span></span> <span data-ttu-id="27f42-146">Especificamente se o valor de saudação processada é um objeto, todas as propriedades serão recuperadas.</span><span class="sxs-lookup"><span data-stu-id="27f42-146">Specifically if hello processed value is an object, all properties will be retrieved.</span></span>  
  
 `<object_property_list>`  
  
<span data-ttu-id="27f42-147">Especifica a lista de saudação do toobe de propriedades recuperada.</span><span class="sxs-lookup"><span data-stu-id="27f42-147">Specifies hello list of properties toobe retrieved.</span></span> <span data-ttu-id="27f42-148">Cada valor retornado será um objeto com propriedades de saudação especificado.</span><span class="sxs-lookup"><span data-stu-id="27f42-148">Each returned value will be an object with hello properties specified.</span></span>  
  
`VALUE`  
  
<span data-ttu-id="27f42-149">Especifica que o valor JSON Olá deve ser recuperada em vez do objeto JSON completo de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-149">Specifies that hello JSON value should be retrieved instead of hello complete JSON object.</span></span> <span data-ttu-id="27f42-150">Isso, ao contrário `<property_list>` não colocar o valor de saudação projetada em um objeto.</span><span class="sxs-lookup"><span data-stu-id="27f42-150">This, unlike `<property_list>` does not wrap hello projected value in an object.</span></span>  
  
`<scalar_expression>`  
  
<span data-ttu-id="27f42-151">Expressão que representa a saudação toobe de valor computado.</span><span class="sxs-lookup"><span data-stu-id="27f42-151">Expression representing hello value toobe computed.</span></span> <span data-ttu-id="27f42-152">Consulte a seção [Expressões escalares](#bk_scalar_expressions) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="27f42-152">See [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
<span data-ttu-id="27f42-153">**Comentários**</span><span class="sxs-lookup"><span data-stu-id="27f42-153">**Remarks**</span></span>  
  
<span data-ttu-id="27f42-154">Olá `SELECT *` sintaxe só será válida se a cláusula FROM tiver declarado exatamente um alias.</span><span class="sxs-lookup"><span data-stu-id="27f42-154">hello `SELECT *` syntax is only valid if FROM clause has declared exactly one alias.</span></span> <span data-ttu-id="27f42-155">`SELECT *` fornece uma projeção de identidade, que pode ser útil se nenhuma projeção é necessária.</span><span class="sxs-lookup"><span data-stu-id="27f42-155">`SELECT *` provides an identity projection, which can be useful if no projection is needed.</span></span> <span data-ttu-id="27f42-156">SELECT * só é válida se a cláusula FROM é especificada e introduzida uma única fonte de entrada.</span><span class="sxs-lookup"><span data-stu-id="27f42-156">SELECT * is only valid if FROM clause is specified and introduced only a single input source.</span></span>  
  
<span data-ttu-id="27f42-157">Observe que `SELECT <select_list>` e `SELECT *` são "açúcar sintático" e podem ser expressos, como alternativa, usando instruções SELECT simples, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="27f42-157">Note that `SELECT <select_list>` and `SELECT *` are "syntactic sugar" and can be alternatively expressed by using simple SELECT statements as shown below.</span></span>  
  
1.  `SELECT * FROM ... AS from_alias ...`  
  
     <span data-ttu-id="27f42-158">é equivalente a:</span><span class="sxs-lookup"><span data-stu-id="27f42-158">is equivalent to:</span></span>  
  
     `SELECT from_alias FROM ... AS from_alias ...`  
  
2.  `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
     <span data-ttu-id="27f42-159">é equivalente a:</span><span class="sxs-lookup"><span data-stu-id="27f42-159">is equivalent to:</span></span>  
  
     `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
<span data-ttu-id="27f42-160">**Consulte também**</span><span class="sxs-lookup"><span data-stu-id="27f42-160">**See Also**</span></span>  
  
[<span data-ttu-id="27f42-161">Expressões escalares</span><span class="sxs-lookup"><span data-stu-id="27f42-161">Scalar expressions</span></span>](#bk_scalar_expressions)  
[<span data-ttu-id="27f42-162">Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="27f42-162">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="27f42-163"><a name="bk_from_clause"></a> Cláusula FROM</span><span class="sxs-lookup"><span data-stu-id="27f42-163"><a name="bk_from_clause"></a> FROM clause</span></span>  
<span data-ttu-id="27f42-164">Especifica a fonte de saudação ou fontes unidas.</span><span class="sxs-lookup"><span data-stu-id="27f42-164">Specifies hello source or joined sources.</span></span> <span data-ttu-id="27f42-165">cláusula FROM de saudação é opcional.</span><span class="sxs-lookup"><span data-stu-id="27f42-165">hello FROM clause is optional.</span></span> <span data-ttu-id="27f42-166">Se não for especificado, outras cláusulas ainda serão executadas como se a cláusula FROM fornecesse um único documento.</span><span class="sxs-lookup"><span data-stu-id="27f42-166">If not specified, other clauses will still be executed as if FROM clause provided a single document.</span></span>  
  
<span data-ttu-id="27f42-167">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-167">**Syntax**</span></span>  
  
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
  
<span data-ttu-id="27f42-168">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-168">**Arguments**</span></span>  
  
`<from_source>`  
  
<span data-ttu-id="27f42-169">Especifica uma fonte de dados, com ou sem um alias.</span><span class="sxs-lookup"><span data-stu-id="27f42-169">Specifies a data source, with or without an alias.</span></span> <span data-ttu-id="27f42-170">Se o alias não for especificado, ele será inferido de saudação `<collection_expression>` usando as seguinte regras:</span><span class="sxs-lookup"><span data-stu-id="27f42-170">If alias is not specified, it will be inferred from hello `<collection_expression>` using following rules:</span></span>  
  
-   <span data-ttu-id="27f42-171">Se a expressão de saudação for um collection_name, collection_name será ser usado como um alias.</span><span class="sxs-lookup"><span data-stu-id="27f42-171">If hello expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
-   <span data-ttu-id="27f42-172">Se a expressão de saudação é `<collection_expression>`, property_name e, em seguida, property_name será usado como um alias.</span><span class="sxs-lookup"><span data-stu-id="27f42-172">If hello expression is `<collection_expression>`, then property_name, then property_name will be used as an alias.</span></span> <span data-ttu-id="27f42-173">Se a expressão de saudação for um collection_name, collection_name será ser usado como um alias.</span><span class="sxs-lookup"><span data-stu-id="27f42-173">If hello expression is a collection_name, then collection_name will be used as an alias.</span></span>  
  
<span data-ttu-id="27f42-174">AS `input_alias`</span><span class="sxs-lookup"><span data-stu-id="27f42-174">AS `input_alias`</span></span>  
  
<span data-ttu-id="27f42-175">Especifica que Olá `input_alias` é um conjunto de valores retornados por Olá subjacente da expressão de coleção.</span><span class="sxs-lookup"><span data-stu-id="27f42-175">Specifies that hello `input_alias` is a set of values returned by hello underlying collection expression.</span></span>  
 
<span data-ttu-id="27f42-176">`input_alias` IN</span><span class="sxs-lookup"><span data-stu-id="27f42-176">`input_alias` IN</span></span>  
  
<span data-ttu-id="27f42-177">Especifica que Olá `input_alias` deve representar o conjunto de saudação de valores obtidos pela iteração em todos os elementos da matriz de cada matriz retornada por Olá subjacente da expressão de coleção.</span><span class="sxs-lookup"><span data-stu-id="27f42-177">Specifies that hello `input_alias` should represent hello set of values obtained by iterating over all array elements of each array returned by hello underlying collection expression.</span></span> <span data-ttu-id="27f42-178">Qualquer valor retornado pela expressão de coleção subjacente que não seja uma matriz é ignorado.</span><span class="sxs-lookup"><span data-stu-id="27f42-178">Any value returned by underlying collection expression that is not an array is ignored.</span></span>  
  
`<collection_expression>`  
  
<span data-ttu-id="27f42-179">Especifica Olá coleção expressão toobe tooretrieve documentos de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-179">Specifies hello collection expression toobe used tooretrieve hello documents.</span></span>  
  
`ROOT`  
  
<span data-ttu-id="27f42-180">Especifica que documento deve ser recuperado do padrão de saudação, coleção conectada no momento.</span><span class="sxs-lookup"><span data-stu-id="27f42-180">Specifies that document should be retrieved from hello default, currently connected collection.</span></span>  
  
`collection_name`  
  
<span data-ttu-id="27f42-181">Especifica que documento deve ser recuperado da coleção Olá fornecido.</span><span class="sxs-lookup"><span data-stu-id="27f42-181">Specifies that document should be retrieved from hello provided collection.</span></span> <span data-ttu-id="27f42-182">nome de Olá da coleção de saudação deve corresponder o nome de saudação da coleção Olá conectada no momento.</span><span class="sxs-lookup"><span data-stu-id="27f42-182">hello name of hello collection must match hello name of hello collection currently connected to.</span></span>  
  
`input_alias`  
  
<span data-ttu-id="27f42-183">Especifica que documento deve ser recuperado da saudação outra fonte definida pelo alias Olá fornecido.</span><span class="sxs-lookup"><span data-stu-id="27f42-183">Specifies that document should be retrieved from hello other source defined by hello provided alias.</span></span>  
  
`<collection_expression> '.' property_`  
  
<span data-ttu-id="27f42-184">Especifica que documento deve ser recuperado acessando Olá `property_name` especificado de elemento de matriz de propriedade ou array_index para todos os documentos recuperados pela expressão de coleção.</span><span class="sxs-lookup"><span data-stu-id="27f42-184">Specifies that document should be retrieved by accessing hello `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
`<collection_expression> '[' "property_name" | array_index ']'`  
  
<span data-ttu-id="27f42-185">Especifica que documento deve ser recuperado acessando Olá `property_name` especificado de elemento de matriz de propriedade ou array_index para todos os documentos recuperados pela expressão de coleção.</span><span class="sxs-lookup"><span data-stu-id="27f42-185">Specifies that document should be retrieved by accessing hello `property_name` property or array_index array element for all documents retrieved by specified collection expression.</span></span>  
  
<span data-ttu-id="27f42-186">**Comentários**</span><span class="sxs-lookup"><span data-stu-id="27f42-186">**Remarks**</span></span>  
  
<span data-ttu-id="27f42-187">Todos os aliases fornecidos ou inferidos em Olá `<from_source>(`s) deve ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="27f42-187">All aliases provided or inferred in hello `<from_source>(`s) must be unique.</span></span> <span data-ttu-id="27f42-188">Olá sintaxe `<collection_expression>.`property_name é Olá igual `<collection_expression>' ['"property_name"']'`.</span><span class="sxs-lookup"><span data-stu-id="27f42-188">hello Syntax `<collection_expression>.`property_name is hello same as `<collection_expression>' ['"property_name"']'`.</span></span> <span data-ttu-id="27f42-189">No entanto, última sintaxe de saudação pode ser usado se um nome de propriedade contém um caractere não identificador.</span><span class="sxs-lookup"><span data-stu-id="27f42-189">However, hello latter syntax can be used if a property name contains a non-identifier characters.</span></span>  
  
<span data-ttu-id="27f42-190">**Propriedades ausentes, elementos de matriz ausentes, tratamento de valores indefinidos**</span><span class="sxs-lookup"><span data-stu-id="27f42-190">**Missing properties, missing array elements, undefined values handling**</span></span>  
  
<span data-ttu-id="27f42-191">Se uma expressão de coleção acessar propriedades ou elementos da matriz e o valor não existir, esse valor será ignorado e não processado.</span><span class="sxs-lookup"><span data-stu-id="27f42-191">If a collection expression accesses properties or array elements and that value does not exist, that value will be ignored and not processed further.</span></span>  
  
<span data-ttu-id="27f42-192">**Escopo de contexto de expressão de coleção**</span><span class="sxs-lookup"><span data-stu-id="27f42-192">**Collection expression context scoping**</span></span>  
  
<span data-ttu-id="27f42-193">Uma expressão de coleção pode ser coleção com escopo ou documento com escopo:</span><span class="sxs-lookup"><span data-stu-id="27f42-193">A collection expression may be collection-scoped or document-scoped:</span></span>  
  
-   <span data-ttu-id="27f42-194">Uma expressão é coleção com escopo, se hello fonte subjacente da expressão de coleção de saudação for ROOT ou `collection_name`.</span><span class="sxs-lookup"><span data-stu-id="27f42-194">An expression is collection-scoped, if hello underlying source of hello collection expression is either ROOT or `collection_name`.</span></span> <span data-ttu-id="27f42-195">Essa expressão representa um conjunto de documentos recuperados diretamente da coleção Olá e não é dependente de processamento de saudação de outras expressões de coleção.</span><span class="sxs-lookup"><span data-stu-id="27f42-195">Such an expression represents a set of documents retrieved from hello collection directly, and is not dependent on hello processing of other collection expressions.</span></span>  
  
-   <span data-ttu-id="27f42-196">Uma expressão é documento com escopo, se hello fonte subjacente da expressão de coleção de saudação é `input_alias` introduzida anteriormente na consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-196">An expression is document-scoped, if hello underlying source of hello collection expression is `input_alias` introduced earlier in hello query.</span></span> <span data-ttu-id="27f42-197">Essa expressão representa um conjunto de documentos obtido avaliando a expressão de coleção Olá no escopo de saudação de cada documento pertencente toohello conjunto associado a coleção de um alias de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-197">Such an expression represents a set of documents obtained by evaluating hello collection expression in hello scope of each document belonging toohello set associated with hello aliased collection.</span></span>  <span data-ttu-id="27f42-198">conjunto resultante da saudação será uma união de conjuntos obtidos avaliando a expressão de coleção Olá para cada um dos documentos Olá Olá subjacente conjunto.</span><span class="sxs-lookup"><span data-stu-id="27f42-198">hello resulting set will be a union of sets obtained by evaluating hello collection expression for each of hello documents in hello underlying set.</span></span>  
  
<span data-ttu-id="27f42-199">**Junções**</span><span class="sxs-lookup"><span data-stu-id="27f42-199">**Joins**</span></span>  
  
<span data-ttu-id="27f42-200">Na versão atual do hello, o banco de dados do Azure Cosmos oferece suporte a junções internas.</span><span class="sxs-lookup"><span data-stu-id="27f42-200">In hello current release, Azure Cosmos DB supports inner joins.</span></span> <span data-ttu-id="27f42-201">Recursos adicionais de junção serão disponibilizados em breve.</span><span class="sxs-lookup"><span data-stu-id="27f42-201">Additional join capabilities are forthcoming.</span></span>

<span data-ttu-id="27f42-202">Conjuntos de resultados de junções internas em um produto cruzado completo de saudação participam da junção hello.</span><span class="sxs-lookup"><span data-stu-id="27f42-202">Inner joins result in a complete cross product of hello sets participating in hello join.</span></span> <span data-ttu-id="27f42-203">resultado de saudação de uma junção N-way é um conjunto de tuplas de elemento N, onde cada valor na tupla Olá é associado com um alias de saudação conjunto de participação na junção hello e pode ser acessada referenciando esse alias em outras cláusulas.</span><span class="sxs-lookup"><span data-stu-id="27f42-203">hello result of an N-way join is a set of N-element tuples, where each value in hello tuple is associated with hello aliased set participating in hello join and can be accessed by referencing that alias in other clauses.</span></span>  
  
<span data-ttu-id="27f42-204">avaliação de saudação de junção Olá depende escopo contexto Olá Olá conjuntos de participação:</span><span class="sxs-lookup"><span data-stu-id="27f42-204">hello evaluation of hello join depends on hello context scope of hello participating sets:</span></span>  
  
-  <span data-ttu-id="27f42-205">Uma junção entre um conjunto de coleção A e o conjunto de coleção com escopo definido B resulta em um produto cruzado de todos os elementos nos conjuntos A e B.</span><span class="sxs-lookup"><span data-stu-id="27f42-205">A join between collection-set A and collection-scoped set B, results in a cross product of all elements in sets A and B.</span></span>
  
-   <span data-ttu-id="27f42-206">Uma associação entre o conjunto A e o conjunto com escopo de documento B resulta em uma união de todos os conjuntos obtidos pela avaliação do conjunto com escopo de documento B para cada documento do conjunto A.</span><span class="sxs-lookup"><span data-stu-id="27f42-206">A join between set A and document-scoped set B, results in a union of all sets obtained by evaluating document-scoped set B for each document from set A.</span></span>  
  
 <span data-ttu-id="27f42-207">Na versão atual do hello, um máximo de uma expressão de coleção com escopo suportado pelo processador de consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-207">In hello current release, a maximum of one collection-scoped expression is supported by hello query processor.</span></span>  
  
<span data-ttu-id="27f42-208">**Exemplos de junções:**</span><span class="sxs-lookup"><span data-stu-id="27f42-208">**Examples of joins:**</span></span>  
  
<span data-ttu-id="27f42-209">Vejamos Olá seguinte cláusula FROM:`<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span><span class="sxs-lookup"><span data-stu-id="27f42-209">Let's look at hello following FROM clause: `<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`</span></span>  
  
 <span data-ttu-id="27f42-210">Permite que cada fonte defina `input_alias1, input_alias2, …, input_aliasN`.</span><span class="sxs-lookup"><span data-stu-id="27f42-210">Let each source define `input_alias1, input_alias2, …, input_aliasN`.</span></span> <span data-ttu-id="27f42-211">Essa cláusula FROM retorna um conjunto de tuplas N (tupla com valores N).</span><span class="sxs-lookup"><span data-stu-id="27f42-211">This FROM clause returns a set of N-tuples (tuple with N values).</span></span> <span data-ttu-id="27f42-212">Cada tupla terá os valores produzidos pela iteração de todos os alias da coleção em seus respectivos conjuntos.</span><span class="sxs-lookup"><span data-stu-id="27f42-212">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span>  
  
<span data-ttu-id="27f42-213">*JUNÇÃO exemplo 1, com 2 fontes:*</span><span class="sxs-lookup"><span data-stu-id="27f42-213">*JOIN example 1, with 2 sources:*</span></span>  
  
- <span data-ttu-id="27f42-214">Permite que `<from_source1>` tenha escopo de coleção e represente o conjunto {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="27f42-214">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="27f42-215">Permite que `<from_source2>` tenha escopo de documento, referenciando input_alias1 e represente os conjuntos:</span><span class="sxs-lookup"><span data-stu-id="27f42-215">Let `<from_source2>` be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="27f42-216">{1,2} para `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="27f42-216">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="27f42-217">{3} para`input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="27f42-217">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="27f42-218">{4,5} para`input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="27f42-218">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="27f42-219">Olá cláusula FROM `<from_source1> JOIN <from_source2>` resultará em Olá tuplas a seguir:</span><span class="sxs-lookup"><span data-stu-id="27f42-219">hello FROM clause `<from_source1> JOIN <from_source2>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="27f42-220">(`input_alias1, input_alias2`):</span><span class="sxs-lookup"><span data-stu-id="27f42-220">(`input_alias1, input_alias2`):</span></span>  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
<span data-ttu-id="27f42-221">*JUNÇÃO exemplo 2, com 3 fontes:*</span><span class="sxs-lookup"><span data-stu-id="27f42-221">*JOIN example 2, with 3 sources:*</span></span>  
  
- <span data-ttu-id="27f42-222">Permite que `<from_source1>` tenha escopo de coleção e represente o conjunto {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="27f42-222">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="27f42-223">Permite que `<from_source2>` tenha escopo de documento, referenciando `input_alias1` e represente os conjuntos:</span><span class="sxs-lookup"><span data-stu-id="27f42-223">Let `<from_source2>` be document-scoped referencing `input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="27f42-224">{1,2} para `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="27f42-224">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="27f42-225">{3} para`input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="27f42-225">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="27f42-226">{4,5} para`input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="27f42-226">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="27f42-227">Permite que `<from_source3>` tenha escopo de documento, referenciando `input_alias2` e represente os conjuntos:</span><span class="sxs-lookup"><span data-stu-id="27f42-227">Let `<from_source3>` be document-scoped referencing `input_alias2` and represent sets:</span></span>  
  
    <span data-ttu-id="27f42-228">{100, 200} para`input_alias2 = 1,`</span><span class="sxs-lookup"><span data-stu-id="27f42-228">{100, 200} for `input_alias2 = 1,`</span></span>  
  
    <span data-ttu-id="27f42-229">{300} para`input_alias2 = 3,`</span><span class="sxs-lookup"><span data-stu-id="27f42-229">{300} for `input_alias2 = 3,`</span></span>  
  
- <span data-ttu-id="27f42-230">Olá cláusula FROM `<from_source1> JOIN <from_source2> JOIN <from_source3>` resultará em Olá tuplas a seguir:</span><span class="sxs-lookup"><span data-stu-id="27f42-230">hello FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="27f42-231">(input_alias1, input_alias2, input_alias3):</span><span class="sxs-lookup"><span data-stu-id="27f42-231">(input_alias1, input_alias2, input_alias3):</span></span>  
  
    <span data-ttu-id="27f42-232">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span><span class="sxs-lookup"><span data-stu-id="27f42-232">(A, 1, 100), (A, 1, 200), (B, 3, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="27f42-233">Falta de tuplas para outros valores de `input_alias1`, `input_alias2`, para qual Olá `<from_source3>` não retornou nenhum valor.</span><span class="sxs-lookup"><span data-stu-id="27f42-233">Lack of tuples for other values of `input_alias1`, `input_alias2`, for which hello `<from_source3>` did not return any values.</span></span>  
  
<span data-ttu-id="27f42-234">*JUNÇÃO exemplo 3, com 3 fontes:*</span><span class="sxs-lookup"><span data-stu-id="27f42-234">*JOIN example 3, with 3 sources:*</span></span>  
  
- <span data-ttu-id="27f42-235">Permite que <from_source1> tenha escopo de coleção e represente o conjunto {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="27f42-235">Let <from_source1> be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="27f42-236">Permite que `<from_source1>` tenha escopo de coleção e represente o conjunto {A, B, C}.</span><span class="sxs-lookup"><span data-stu-id="27f42-236">Let `<from_source1>` be collection-scoped and represent set {A, B, C}.</span></span>  
  
- <span data-ttu-id="27f42-237">Permite que <from_source2> tenha escopo de documento, referenciando input_alias1 e represente os conjuntos:</span><span class="sxs-lookup"><span data-stu-id="27f42-237">Let <from_source2> be document-scoped referencing input_alias1 and represent sets:</span></span>  
  
    <span data-ttu-id="27f42-238">{1,2} para `input_alias1 = A,`</span><span class="sxs-lookup"><span data-stu-id="27f42-238">{1, 2} for `input_alias1 = A,`</span></span>  
  
    <span data-ttu-id="27f42-239">{3} para`input_alias1 = B,`</span><span class="sxs-lookup"><span data-stu-id="27f42-239">{3} for `input_alias1 = B,`</span></span>  
  
    <span data-ttu-id="27f42-240">{4,5} para`input_alias1 = C,`</span><span class="sxs-lookup"><span data-stu-id="27f42-240">{4, 5} for `input_alias1 = C,`</span></span>  
  
- <span data-ttu-id="27f42-241">Permitir que `<from_source3>` escopo muito`input_alias1` e represente conjuntos:</span><span class="sxs-lookup"><span data-stu-id="27f42-241">Let `<from_source3>` be scoped too`input_alias1` and represent sets:</span></span>  
  
    <span data-ttu-id="27f42-242">{100, 200} para`input_alias2 = A,`</span><span class="sxs-lookup"><span data-stu-id="27f42-242">{100, 200} for `input_alias2 = A,`</span></span>  
  
    <span data-ttu-id="27f42-243">{300} para`input_alias2 = C,`</span><span class="sxs-lookup"><span data-stu-id="27f42-243">{300} for `input_alias2 = C,`</span></span>  
  
- <span data-ttu-id="27f42-244">Olá cláusula FROM `<from_source1> JOIN <from_source2> JOIN <from_source3>` resultará em Olá tuplas a seguir:</span><span class="sxs-lookup"><span data-stu-id="27f42-244">hello FROM clause `<from_source1> JOIN <from_source2> JOIN <from_source3>` will result in hello following tuples:</span></span>  
  
    <span data-ttu-id="27f42-245">(`input_alias1, input_alias2, input_alias3`):</span><span class="sxs-lookup"><span data-stu-id="27f42-245">(`input_alias1, input_alias2, input_alias3`):</span></span>  
  
    <span data-ttu-id="27f42-246">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) , (C, 5, 300)</span><span class="sxs-lookup"><span data-stu-id="27f42-246">(A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) ,  (C, 5, 300)</span></span>  
  
> [!NOTE]
> <span data-ttu-id="27f42-247">Isso resultou em produto cruzado entre `<from_source2>` e `<from_source3>` porque ambos estão no escopo toohello mesmo `<from_source1>`.</span><span class="sxs-lookup"><span data-stu-id="27f42-247">This resulted in cross product between `<from_source2>` and `<from_source3>` because both are scoped toohello same `<from_source1>`.</span></span>  <span data-ttu-id="27f42-248">Isso resultou em 4 (2 x 2) tuplas com valor A, 0 tuplas com valor B (1 x 0) e 2 (2 x 1) tuplas com valor C.</span><span class="sxs-lookup"><span data-stu-id="27f42-248">This resulted in 4 (2x2) tuples having value A, 0 tuples having value B (1x0) and 2 (2x1) tuples having value C.</span></span>  
  
<span data-ttu-id="27f42-249">**Consulte também**</span><span class="sxs-lookup"><span data-stu-id="27f42-249">**See also**</span></span>  
  
 [<span data-ttu-id="27f42-250">Cláusula SELECT</span><span class="sxs-lookup"><span data-stu-id="27f42-250">SELECT clause</span></span>](#bk_select_query)  
  
##  <span data-ttu-id="27f42-251"><a name="bk_where_clause"></a> Cláusula WHERE</span><span class="sxs-lookup"><span data-stu-id="27f42-251"><a name="bk_where_clause"></a> WHERE clause</span></span>  
 <span data-ttu-id="27f42-252">Especifica o critério de pesquisa Olá Olá documentos retornados pela consulta hello.</span><span class="sxs-lookup"><span data-stu-id="27f42-252">Specifies hello search condition for hello documents returned by hello query.</span></span>  
  
 <span data-ttu-id="27f42-253">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-253">**Syntax**</span></span>  
  
```  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 <span data-ttu-id="27f42-254">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-254">**Arguments**</span></span>  
  
-   `<filter_condition>`  
  
     <span data-ttu-id="27f42-255">Especifica a saudação condição toobe atendido para Olá documentos toobe retornado.</span><span class="sxs-lookup"><span data-stu-id="27f42-255">Specifies hello condition toobe met for hello documents toobe returned.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="27f42-256">Expressão que representa a saudação toobe de valor computado.</span><span class="sxs-lookup"><span data-stu-id="27f42-256">Expression representing hello value toobe computed.</span></span> <span data-ttu-id="27f42-257">Consulte Olá [expressões escalares](#bk_scalar_expressions) seção para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="27f42-257">See hello [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
 <span data-ttu-id="27f42-258">**Comentários**</span><span class="sxs-lookup"><span data-stu-id="27f42-258">**Remarks**</span></span>  
  
 <span data-ttu-id="27f42-259">Para que Olá toobe documento retornado uma expressão especificada como condição de filtro deve ser avaliada tootrue.</span><span class="sxs-lookup"><span data-stu-id="27f42-259">In order for hello document toobe returned an expression specified as filter condition must evaluate tootrue.</span></span> <span data-ttu-id="27f42-260">Somente o valor booliano true atenderá a condição de hello, qualquer outro valor: indefinido, nulo, FALSO, número, matriz ou objeto não atenderá Olá condição.</span><span class="sxs-lookup"><span data-stu-id="27f42-260">Only Boolean value true will satisfy hello condition, any other value: undefined, null, false, Number, Array or Object will not satisfy hello condition.</span></span>  
  
##  <span data-ttu-id="27f42-261"><a name="bk_orderby_clause"></a> Cláusula ORDER BY</span><span class="sxs-lookup"><span data-stu-id="27f42-261"><a name="bk_orderby_clause"></a> ORDER BY clause</span></span>  
 <span data-ttu-id="27f42-262">Especifica a saudação ordem de classificação para resultados retornados pela consulta hello.</span><span class="sxs-lookup"><span data-stu-id="27f42-262">Specifies hello sorting order for results returned by hello query.</span></span>  
  
 <span data-ttu-id="27f42-263">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-263">**Syntax**</span></span>  
  
```  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 <span data-ttu-id="27f42-264">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-264">**Arguments**</span></span>  
  
-   `<sort_specification>`  
  
     <span data-ttu-id="27f42-265">Especifica uma propriedade ou expressão na qual conjunto de resultados de consulta de saudação toosort.</span><span class="sxs-lookup"><span data-stu-id="27f42-265">Specifies a property or expression on which toosort hello query result set.</span></span> <span data-ttu-id="27f42-266">Uma coluna de classificação pode ser especificada como um alias de nome ou coluna.</span><span class="sxs-lookup"><span data-stu-id="27f42-266">A sort column can be specified as a name or column alias.</span></span>  
  
     <span data-ttu-id="27f42-267">Várias colunas de classificação podem ser especificadas.</span><span class="sxs-lookup"><span data-stu-id="27f42-267">Multiple sort columns can be specified.</span></span> <span data-ttu-id="27f42-268">Os nomes de coluna devem ser exclusivos.</span><span class="sxs-lookup"><span data-stu-id="27f42-268">Column names must be unique.</span></span> <span data-ttu-id="27f42-269">sequência de saudação de colunas de classificação de saudação na cláusula ORDER BY da saudação define a organização Olá Olá classificado do conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="27f42-269">hello sequence of hello sort columns in hello ORDER BY clause defines hello organization of hello sorted result set.</span></span> <span data-ttu-id="27f42-270">Ou seja, Olá conjunto de resultados é classificado pela propriedade primeiro hello e, em seguida, essa lista ordenada é classificada pela propriedade segundo Olá e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="27f42-270">That is, hello result set is sorted by hello first property and then that ordered list is sorted by hello second property, and so on.</span></span>  
  
     <span data-ttu-id="27f42-271">nomes de coluna Olá referenciados na cláusula ORDER BY da saudação devem corresponder tooeither uma coluna em Olá Selecionar coluna de lista ou tooa definida em uma tabela especificada na cláusula FROM de saudação sem qualquer ambiguidade.</span><span class="sxs-lookup"><span data-stu-id="27f42-271">hello column names referenced in hello ORDER BY clause must correspond tooeither a column in hello select list or tooa column defined in a table specified in hello FROM clause without any ambiguities.</span></span>  
  
-   `<sort_expression>`  
  
     <span data-ttu-id="27f42-272">Especifica uma única propriedade ou expressão na qual conjunto de resultados de consulta de saudação toosort.</span><span class="sxs-lookup"><span data-stu-id="27f42-272">Specifies a single property or expression on which toosort hello query result set.</span></span>  
  
-   `<scalar_expression>`  
  
     <span data-ttu-id="27f42-273">Consulte Olá [expressões escalares](#bk_scalar_expressions) seção para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="27f42-273">See hello [Scalar expressions](#bk_scalar_expressions) section for details.</span></span>  
  
-   `ASC | DESC`  
  
     <span data-ttu-id="27f42-274">Especifica que os valores hello na coluna especificada Olá devem ser classificados em ordem crescente ou decrescente.</span><span class="sxs-lookup"><span data-stu-id="27f42-274">Specifies that hello values in hello specified column should be sorted in ascending or descending order.</span></span> <span data-ttu-id="27f42-275">ASC classifica do valor de toohighest valor mais baixo de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-275">ASC sorts from hello lowest value toohighest value.</span></span> <span data-ttu-id="27f42-276">DESC classifica do valor de toolowest de valor mais alto.</span><span class="sxs-lookup"><span data-stu-id="27f42-276">DESC sorts from highest value toolowest value.</span></span> <span data-ttu-id="27f42-277">ASC é a ordem de classificação padrão hello.</span><span class="sxs-lookup"><span data-stu-id="27f42-277">ASC is hello default sort order.</span></span> <span data-ttu-id="27f42-278">Valores nulos são tratados como valores possíveis mais baixos de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-278">Null values are treated as hello lowest possible values.</span></span>  
  
 <span data-ttu-id="27f42-279">**Comentários**</span><span class="sxs-lookup"><span data-stu-id="27f42-279">**Remarks**</span></span>  
  
 <span data-ttu-id="27f42-280">Enquanto a gramática de consulta Olá dá suporte a vários pedidos por propriedades, tempo de execução de consulta de banco de dados do Azure Cosmos Olá dá suporte à classificação apenas contra uma única propriedade e somente nomes de propriedade, ou seja, não contra propriedades calculadas.</span><span class="sxs-lookup"><span data-stu-id="27f42-280">While hello query grammar supports multiple order by properties, hello Azure Cosmos DB query runtime supports sorting only against a single property, and only against property names, i.e., not against computed properties.</span></span> <span data-ttu-id="27f42-281">A classificação também requer que Olá política de indexação inclui um índice de intervalo para a propriedade hello e hello especificado tipo, com precisão máxima da saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-281">Sorting also requires that hello indexing policy includes a range index for hello property and hello specified type, with hello maximum precision.</span></span> <span data-ttu-id="27f42-282">Consulte toohello documentação para obter mais detalhes da política de indexação.</span><span class="sxs-lookup"><span data-stu-id="27f42-282">Refer toohello indexing policy documentation for more details.</span></span>  
  
##  <span data-ttu-id="27f42-283"><a name="bk_scalar_expressions"></a> Expressões escalares</span><span class="sxs-lookup"><span data-stu-id="27f42-283"><a name="bk_scalar_expressions"></a> Scalar expressions</span></span>  
 <span data-ttu-id="27f42-284">Uma expressão escalar é uma combinação de símbolos e operadores que podem ser avaliados tooobtain um único valor.</span><span class="sxs-lookup"><span data-stu-id="27f42-284">A scalar expression is a combination of symbols and operators that can be evaluated tooobtain a single value.</span></span> <span data-ttu-id="27f42-285">Expressões simples podem ser constantes, referências de propriedade, referências de elemento de matriz, referências de alias ou chamadas de função.</span><span class="sxs-lookup"><span data-stu-id="27f42-285">Simple expressions can be constants, property references, array element references, alias references, or function calls.</span></span> <span data-ttu-id="27f42-286">As expressões simples podem ser combinadas em expressões complexas usando operadores.</span><span class="sxs-lookup"><span data-stu-id="27f42-286">Simple expressions can be combined into complex expressions using operators.</span></span>  
  
 <span data-ttu-id="27f42-287">Para obter detalhes sobre os valores que a expressão escalar pode ter, consulte a seção [Constantes](#bk_constants).</span><span class="sxs-lookup"><span data-stu-id="27f42-287">For details on values which scalar expression may have, see [Constants](#bk_constants) section.</span></span>  
  
 <span data-ttu-id="27f42-288">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-288">**Syntax**</span></span>  
  
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
  
 <span data-ttu-id="27f42-289">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-289">**Arguments**</span></span>  
  
-   `<constant>`  
  
     <span data-ttu-id="27f42-290">Representa um valor constante.</span><span class="sxs-lookup"><span data-stu-id="27f42-290">Represents a constant value.</span></span> <span data-ttu-id="27f42-291">Consulte a seção [Constantes](#bk_constants) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="27f42-291">See [Constants](#bk_constants) section for details.</span></span>  
  
-   `input_alias`  
  
     <span data-ttu-id="27f42-292">Representa um valor definido por Olá `input_alias` introduzido no hello `FROM` cláusula.</span><span class="sxs-lookup"><span data-stu-id="27f42-292">Represents a value defined by hello `input_alias` introduced in hello `FROM` clause.</span></span>  
    <span data-ttu-id="27f42-293">Esse valor tem garantia toonot ser **indefinido** –**indefinido** os valores na entrada hello serão ignorados.</span><span class="sxs-lookup"><span data-stu-id="27f42-293">This value is guaranteed toonot be **undefined** –**undefined** values in hello input are skipped.</span></span>  
  
-   `<scalar_expression>.property_name`  
  
     <span data-ttu-id="27f42-294">Representa um valor de propriedade de saudação de um objeto.</span><span class="sxs-lookup"><span data-stu-id="27f42-294">Represents a value of hello property of an object.</span></span> <span data-ttu-id="27f42-295">Se Olá a propriedade não existe ou propriedade é referenciada em um valor que não é um objeto, Olá avalia muito**indefinido** valor.</span><span class="sxs-lookup"><span data-stu-id="27f42-295">If hello property does not exist or property is referenced on a value which is not an object, then hello expression evaluates too**undefined** value.</span></span>  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     <span data-ttu-id="27f42-296">Representa um valor da propriedade Olá com nome `property_name` ou elemento de matriz com índice `array_index` de uma matriz de objetos /.</span><span class="sxs-lookup"><span data-stu-id="27f42-296">Represents a value of hello property with name `property_name` or array element with index `array_index` of an object/array.</span></span> <span data-ttu-id="27f42-297">Se o índice de matriz/propriedade Olá não existe ou o índice de matriz/propriedade Olá é referenciado em um valor que não é uma matriz de objetos /, Olá expressão é avaliada a tooundefined valor.</span><span class="sxs-lookup"><span data-stu-id="27f42-297">If hello property/array index does not exist or hello property/array index is referenced on a value which is not an object/array, then hello expression evaluates tooundefined value.</span></span>  
  
-   `unary_operator <scalar_expression>`  
  
     <span data-ttu-id="27f42-298">Representa um operador que é aplicada tooa valor único.</span><span class="sxs-lookup"><span data-stu-id="27f42-298">Represents an operator that is applied tooa single value.</span></span> <span data-ttu-id="27f42-299">Consulte a seção [Operadores](#bk_operators) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="27f42-299">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     <span data-ttu-id="27f42-300">Representa um operador que é aplicada tootwo valores.</span><span class="sxs-lookup"><span data-stu-id="27f42-300">Represents an operator that is applied tootwo values.</span></span> <span data-ttu-id="27f42-301">Consulte a seção [Operadores](#bk_operators) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="27f42-301">See [Operators](#bk_operators) section for details.</span></span>  
  
-   `<scalar_function_expression>`  
  
     <span data-ttu-id="27f42-302">Representa um valor definido por um resultado de uma chamada de função.</span><span class="sxs-lookup"><span data-stu-id="27f42-302">Represents a value defined by a result of a function call.</span></span>  
  
-   `udf_scalar_function`  
  
     <span data-ttu-id="27f42-303">Função escalar definida pelo nome de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-303">Name of hello user defined scalar function.</span></span>  
  
-   `builtin_scalar_function`  
  
     <span data-ttu-id="27f42-304">Nome de função escalar interna de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-304">Name of hello built-in scalar function.</span></span>  
  
-   `<create_object_expression>`  
  
     <span data-ttu-id="27f42-305">Representa um valor obtido pela criação de um novo objeto com propriedades especificadas e seus valores.</span><span class="sxs-lookup"><span data-stu-id="27f42-305">Represents a value obtained by creating a new object with specified properties and their values.</span></span>  
  
-   `<create_array_expression>`  
  
     <span data-ttu-id="27f42-306">Representa um valor obtido pela criação de uma nova matriz com valores especificados como elementos</span><span class="sxs-lookup"><span data-stu-id="27f42-306">Represents a value obtained by creating a new array with specified values as elements</span></span>  
  
-   `parameter_name`  
  
     <span data-ttu-id="27f42-307">Representa um valor de nome de parâmetro especificado hello.</span><span class="sxs-lookup"><span data-stu-id="27f42-307">Represents a value of hello specified parameter name.</span></span> <span data-ttu-id="27f42-308">Nomes de parâmetro devem ter uma única @ como primeiro caractere do hello.</span><span class="sxs-lookup"><span data-stu-id="27f42-308">Parameter names must have a single @ as hello first character.</span></span>  
  
 <span data-ttu-id="27f42-309">**Comentários**</span><span class="sxs-lookup"><span data-stu-id="27f42-309">**Remarks**</span></span>  
  
 <span data-ttu-id="27f42-310">Ao chamar uma função escalar interna ou definida pelo usuário, todos os argumentos deverão ser definidos.</span><span class="sxs-lookup"><span data-stu-id="27f42-310">When calling a built-in or user defined scalar function all arguments must be defined.</span></span> <span data-ttu-id="27f42-311">Se qualquer um dos argumentos de saudação é indefinido, não será chamada de função hello e Olá resultado será indefinido.</span><span class="sxs-lookup"><span data-stu-id="27f42-311">If any of hello arguments is undefined, hello function will not be called and hello result will be undefined.</span></span>  
  
 <span data-ttu-id="27f42-312">Ao criar um objeto, qualquer propriedade que é atribuída um valor indefinido será ignorada e não incluída no hello criado o objeto.</span><span class="sxs-lookup"><span data-stu-id="27f42-312">When creating an object, any property that is assigned undefined value will be skipped and not included in hello created object.</span></span>  
  
 <span data-ttu-id="27f42-313">Quando a criação de uma matriz, qualquer valor do elemento que é atribuído **indefinido** valor será ignorado e não está incluído no objeto de saudação criado.</span><span class="sxs-lookup"><span data-stu-id="27f42-313">When creating an array, any element value that is assigned **undefined** value will be skipped and not included in hello created object.</span></span> <span data-ttu-id="27f42-314">Isso fará com que Olá lado definido pelo elemento tootake seu local de forma que matriz Olá criado será não terá os índices ignorados.</span><span class="sxs-lookup"><span data-stu-id="27f42-314">This will cause hello next defined element tootake its place in such a way that hello created array will not have skipped indexes.</span></span>  
  
##  <span data-ttu-id="27f42-315"><a name="bk_operators"></a> Operadores</span><span class="sxs-lookup"><span data-stu-id="27f42-315"><a name="bk_operators"></a> Operators</span></span>  
 <span data-ttu-id="27f42-316">Esta seção descreve os operadores de saudação com suporte.</span><span class="sxs-lookup"><span data-stu-id="27f42-316">This section describes hello supported operators.</span></span> <span data-ttu-id="27f42-317">Cada operador pode ser atribuído tooexactly uma categoria.</span><span class="sxs-lookup"><span data-stu-id="27f42-317">Each operator can be assigned tooexactly one category.</span></span>  
  
 <span data-ttu-id="27f42-318">Consulte a tabela **Categorias de operador** abaixo para obter detalhes sobre o tratamento de valores **indefinidos**, requisitos de tipo para valores de entrada e tratamento de valores com tipos não correspondentes.</span><span class="sxs-lookup"><span data-stu-id="27f42-318">See **Operator categories** table below, for details regarding handling of **undefined** values, type requirements for input values and handling of values with not matching types.</span></span>  
  
 <span data-ttu-id="27f42-319">**Categorias de operador:**</span><span class="sxs-lookup"><span data-stu-id="27f42-319">**Operator categories:**</span></span>  
  
|<span data-ttu-id="27f42-320">**Categoria**</span><span class="sxs-lookup"><span data-stu-id="27f42-320">**Category**</span></span>|<span data-ttu-id="27f42-321">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="27f42-321">**Details**</span></span>|  
|-|-|  
|<span data-ttu-id="27f42-322">**aritmético**</span><span class="sxs-lookup"><span data-stu-id="27f42-322">**arithmetic**</span></span>|<span data-ttu-id="27f42-323">Operador espera entradas toobe número (s).</span><span class="sxs-lookup"><span data-stu-id="27f42-323">Operator expects input(s) toobe Number(s).</span></span> <span data-ttu-id="27f42-324">A saída também é um número.</span><span class="sxs-lookup"><span data-stu-id="27f42-324">Output is also a Number.</span></span> <span data-ttu-id="27f42-325">Se qualquer uma das entradas de saudação for **indefinido** ou tipo diferente de resultado de número, Olá **indefinido**.</span><span class="sxs-lookup"><span data-stu-id="27f42-325">If any of hello inputs is **undefined** or type other than Number then hello result is **undefined**.</span></span>|  
|<span data-ttu-id="27f42-326">**bit a bit**</span><span class="sxs-lookup"><span data-stu-id="27f42-326">**bitwise**</span></span>|<span data-ttu-id="27f42-327">Operador espera entradas inteiro assinado de 32 bits de toobe número (s).</span><span class="sxs-lookup"><span data-stu-id="27f42-327">Operator expects input(s) toobe 32-bit signed integer Number(s).</span></span> <span data-ttu-id="27f42-328">A saída também é um número inteiro com sinal de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="27f42-328">Output is also 32-bit signed integer Number.</span></span><br /><br /> <span data-ttu-id="27f42-329">Os valores não inteiros serão arredondados.</span><span class="sxs-lookup"><span data-stu-id="27f42-329">Any non-integer value will be rounded.</span></span> <span data-ttu-id="27f42-330">Os valores positivos serão arredondados para baixo; os valores negativos, arredondados para cima.</span><span class="sxs-lookup"><span data-stu-id="27f42-330">Positive value will be rounded down, negative values rounded up.</span></span><br /><br /> <span data-ttu-id="27f42-331">Qualquer valor que está fora do intervalo de inteiros de 32 bits do hello será convertido, colocando os últimos 32 bits de notação de complemento de dois.</span><span class="sxs-lookup"><span data-stu-id="27f42-331">Any value that is outside of hello 32-bit integer range will be converted, by taking last 32-bits of its two's complement notation.</span></span><br /><br /> <span data-ttu-id="27f42-332">Se qualquer uma das entradas de saudação for **indefinido** ou tipo diferente de número, a saudação resultado será **indefinido**.</span><span class="sxs-lookup"><span data-stu-id="27f42-332">If any of hello inputs is **undefined** or type other than Number, then hello result is **undefined**.</span></span><br /><br /> <span data-ttu-id="27f42-333">**Observação:** Olá acima comportamento é compatível com o comportamento do operador bit a bit de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="27f42-333">**Note:** hello above behavior is compatible with JavaScript bitwise operator behavior.</span></span>|  
|<span data-ttu-id="27f42-334">**lógico**</span><span class="sxs-lookup"><span data-stu-id="27f42-334">**logical**</span></span>|<span data-ttu-id="27f42-335">Operador espera entradas toobe Boolianas.</span><span class="sxs-lookup"><span data-stu-id="27f42-335">Operator expects input(s) toobe Boolean(s).</span></span> <span data-ttu-id="27f42-336">A saída também é um valor booliano.</span><span class="sxs-lookup"><span data-stu-id="27f42-336">Output is also a Boolean.</span></span><br /><span data-ttu-id="27f42-337">Se qualquer uma das entradas de saudação for **indefinido** ou tipo diferente de booliano, a saudação resultado será **indefinido**.</span><span class="sxs-lookup"><span data-stu-id="27f42-337">If any of hello inputs is **undefined** or type other than Boolean, then hello result will be **undefined**.</span></span>|  
|<span data-ttu-id="27f42-338">**comparação**</span><span class="sxs-lookup"><span data-stu-id="27f42-338">**comparison**</span></span>|<span data-ttu-id="27f42-339">Operador espera entradas toohave Olá mesmo tipo e não ser indefinido.</span><span class="sxs-lookup"><span data-stu-id="27f42-339">Operator expects input(s) toohave hello same type and not be undefined.</span></span> <span data-ttu-id="27f42-340">A saída é um valor booliano.</span><span class="sxs-lookup"><span data-stu-id="27f42-340">Output is a Boolean.</span></span><br /><br /> <span data-ttu-id="27f42-341">Se qualquer uma das entradas de saudação for **indefinido** ou Olá entradas tiverem tipos diferentes, é o resultado de saudação **indefinido**.</span><span class="sxs-lookup"><span data-stu-id="27f42-341">If any of hello inputs is **undefined** or hello inputs have different types, then hello result is **undefined**.</span></span><br /><br /> <span data-ttu-id="27f42-342">Consulte a tabela **Ordenação dos valores para comparação** para ver detalhes da ordem dos valores.</span><span class="sxs-lookup"><span data-stu-id="27f42-342">See **Ordering of values for comparison** table for value ordering details.</span></span>|  
|<span data-ttu-id="27f42-343">**string**</span><span class="sxs-lookup"><span data-stu-id="27f42-343">**string**</span></span>|<span data-ttu-id="27f42-344">Operador espera entradas toobe cadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="27f42-344">Operator expects input(s) toobe String(s).</span></span> <span data-ttu-id="27f42-345">A saída também é uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="27f42-345">Output is also a String.</span></span><br /><span data-ttu-id="27f42-346">Se qualquer uma das entradas de saudação for **indefinido** ou tipo diferente de resultado de cadeia de caracteres, em seguida, Olá **indefinido**.</span><span class="sxs-lookup"><span data-stu-id="27f42-346">If any of hello inputs is **undefined** or type other than String then hello result is **undefined**.</span></span>|  
  
 <span data-ttu-id="27f42-347">**Operadores unários:**</span><span class="sxs-lookup"><span data-stu-id="27f42-347">**Unary operators:**</span></span>  
  
|<span data-ttu-id="27f42-348">**Nome**</span><span class="sxs-lookup"><span data-stu-id="27f42-348">**Name**</span></span>|<span data-ttu-id="27f42-349">**Operador**</span><span class="sxs-lookup"><span data-stu-id="27f42-349">**Operator**</span></span>|<span data-ttu-id="27f42-350">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="27f42-350">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="27f42-351">**aritmético**</span><span class="sxs-lookup"><span data-stu-id="27f42-351">**arithmetic**</span></span>|+<br /><br /> -|<span data-ttu-id="27f42-352">Retorna um valor numérico hello.</span><span class="sxs-lookup"><span data-stu-id="27f42-352">Returns hello number value.</span></span><br /><br /> <span data-ttu-id="27f42-353">Negação bit a bit.</span><span class="sxs-lookup"><span data-stu-id="27f42-353">Bitwise negation.</span></span> <span data-ttu-id="27f42-354">Retorna o valor do número negado.</span><span class="sxs-lookup"><span data-stu-id="27f42-354">Returns negated number value.</span></span>|  
|<span data-ttu-id="27f42-355">**bit a bit**</span><span class="sxs-lookup"><span data-stu-id="27f42-355">**bitwise**</span></span>|~|<span data-ttu-id="27f42-356">Complemento de um.</span><span class="sxs-lookup"><span data-stu-id="27f42-356">Ones' complement.</span></span> <span data-ttu-id="27f42-357">Retorna um complemento de um valor numérico.</span><span class="sxs-lookup"><span data-stu-id="27f42-357">Returns a complement of a number value.</span></span>|  
|<span data-ttu-id="27f42-358">**Lógico**</span><span class="sxs-lookup"><span data-stu-id="27f42-358">**Logical**</span></span>|<span data-ttu-id="27f42-359">**NOT**</span><span class="sxs-lookup"><span data-stu-id="27f42-359">**NOT**</span></span>|<span data-ttu-id="27f42-360">Negação.</span><span class="sxs-lookup"><span data-stu-id="27f42-360">Negation.</span></span> <span data-ttu-id="27f42-361">Retorna o valor booliano negado.</span><span class="sxs-lookup"><span data-stu-id="27f42-361">Returns negated Boolean value.</span></span>|  
  
 <span data-ttu-id="27f42-362">**Operadores binários:**</span><span class="sxs-lookup"><span data-stu-id="27f42-362">**Binary operators:**</span></span>  
  
|<span data-ttu-id="27f42-363">**Nome**</span><span class="sxs-lookup"><span data-stu-id="27f42-363">**Name**</span></span>|<span data-ttu-id="27f42-364">**Operador**</span><span class="sxs-lookup"><span data-stu-id="27f42-364">**Operator**</span></span>|<span data-ttu-id="27f42-365">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="27f42-365">**Details**</span></span>|  
|-|-|-|  
|<span data-ttu-id="27f42-366">**aritmético**</span><span class="sxs-lookup"><span data-stu-id="27f42-366">**arithmetic**</span></span>|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|<span data-ttu-id="27f42-367">Adição.</span><span class="sxs-lookup"><span data-stu-id="27f42-367">Addition.</span></span><br /><br /> <span data-ttu-id="27f42-368">Subtração.</span><span class="sxs-lookup"><span data-stu-id="27f42-368">Subtraction.</span></span><br /><br /> <span data-ttu-id="27f42-369">Multiplicação.</span><span class="sxs-lookup"><span data-stu-id="27f42-369">Multiplication.</span></span><br /><br /> <span data-ttu-id="27f42-370">Divisão.</span><span class="sxs-lookup"><span data-stu-id="27f42-370">Division.</span></span><br /><br /> <span data-ttu-id="27f42-371">Modulação.</span><span class="sxs-lookup"><span data-stu-id="27f42-371">Modulation.</span></span>|  
|<span data-ttu-id="27f42-372">**bit a bit**</span><span class="sxs-lookup"><span data-stu-id="27f42-372">**bitwise**</span></span>|<span data-ttu-id="27f42-373">&#124;</span><span class="sxs-lookup"><span data-stu-id="27f42-373">&#124;</span></span><br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|<span data-ttu-id="27f42-374">OR bit a bit.</span><span class="sxs-lookup"><span data-stu-id="27f42-374">Bitwise OR.</span></span><br /><br /> <span data-ttu-id="27f42-375">AND bit a bit.</span><span class="sxs-lookup"><span data-stu-id="27f42-375">Bitwise AND.</span></span><br /><br /> <span data-ttu-id="27f42-376">XOR bit a bit.</span><span class="sxs-lookup"><span data-stu-id="27f42-376">Bitwise XOR.</span></span><br /><br /> <span data-ttu-id="27f42-377">Deslocamento para a esquerda.</span><span class="sxs-lookup"><span data-stu-id="27f42-377">Left Shift.</span></span><br /><br /> <span data-ttu-id="27f42-378">Deslocamento para a direita.</span><span class="sxs-lookup"><span data-stu-id="27f42-378">Right Shift.</span></span><br /><br /> <span data-ttu-id="27f42-379">Deslocamento à direita com preenchimento com zero.</span><span class="sxs-lookup"><span data-stu-id="27f42-379">Zero-fill Right Shift.</span></span>|  
|<span data-ttu-id="27f42-380">**lógico**</span><span class="sxs-lookup"><span data-stu-id="27f42-380">**logical**</span></span>|<span data-ttu-id="27f42-381">**AND**</span><span class="sxs-lookup"><span data-stu-id="27f42-381">**AND**</span></span><br /><br /> <span data-ttu-id="27f42-382">**OR**</span><span class="sxs-lookup"><span data-stu-id="27f42-382">**OR**</span></span>|<span data-ttu-id="27f42-383">Conjunção lógica.</span><span class="sxs-lookup"><span data-stu-id="27f42-383">Logical conjunction.</span></span> <span data-ttu-id="27f42-384">Retorna **true** se os dois argumentos forem **true**; do contrário, retorna **false**.</span><span class="sxs-lookup"><span data-stu-id="27f42-384">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="27f42-385">Conjunção lógica.</span><span class="sxs-lookup"><span data-stu-id="27f42-385">Logical conjunction.</span></span> <span data-ttu-id="27f42-386">Retorna **true** se os dois argumentos forem **true**; do contrário, retorna **false**.</span><span class="sxs-lookup"><span data-stu-id="27f42-386">Returns **true** if both arguments are **true**, returns **false** otherwise.</span></span>|  
|<span data-ttu-id="27f42-387">**comparação**</span><span class="sxs-lookup"><span data-stu-id="27f42-387">**comparison**</span></span>|**=**<br /><br /> <span data-ttu-id="27f42-388">**!=, <>**</span><span class="sxs-lookup"><span data-stu-id="27f42-388">**!=, <>**</span></span><br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> <span data-ttu-id="27f42-389">**??**</span><span class="sxs-lookup"><span data-stu-id="27f42-389">**??**</span></span>|<span data-ttu-id="27f42-390">Igual a.</span><span class="sxs-lookup"><span data-stu-id="27f42-390">Equals.</span></span> <span data-ttu-id="27f42-391">Retorna **true** se os argumentos forem iguais; do contrário, retorna **false**.</span><span class="sxs-lookup"><span data-stu-id="27f42-391">Returns **true** if arguments are equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="27f42-392">Não igual a.</span><span class="sxs-lookup"><span data-stu-id="27f42-392">Not equal to.</span></span> <span data-ttu-id="27f42-393">Retorna **true** se os argumentos não forem iguais; do contrário, retorna **false**.</span><span class="sxs-lookup"><span data-stu-id="27f42-393">Returns **true** if arguments are not equal, returns **false** otherwise.</span></span><br /><br /> <span data-ttu-id="27f42-394">Maior que.</span><span class="sxs-lookup"><span data-stu-id="27f42-394">Greater Than.</span></span> <span data-ttu-id="27f42-395">Retorna **true** se o primeiro argumento for maior do que Olá segundo, retornar **false** caso contrário.</span><span class="sxs-lookup"><span data-stu-id="27f42-395">Returns **true** if first argument is greater than hello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="27f42-396">Maior ou igual a.</span><span class="sxs-lookup"><span data-stu-id="27f42-396">Greater Than or Equal To.</span></span> <span data-ttu-id="27f42-397">Retorna **true** retornar se o primeiro argumento for maior que ou igual a segunda toohello, **false** caso contrário.</span><span class="sxs-lookup"><span data-stu-id="27f42-397">Returns **true** if first argument is greater than or equal toohello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="27f42-398">Menor que.</span><span class="sxs-lookup"><span data-stu-id="27f42-398">Less Than.</span></span> <span data-ttu-id="27f42-399">Retorna **true** se o primeiro argumento é menor que o hello segundo, retornar **false** caso contrário.</span><span class="sxs-lookup"><span data-stu-id="27f42-399">Returns **true** if first argument is less than hello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="27f42-400">Menor ou igual a.</span><span class="sxs-lookup"><span data-stu-id="27f42-400">Less Than or Equal To.</span></span> <span data-ttu-id="27f42-401">Retorna **true** se o primeiro argumento é menor ou igual toohello segundo um retorno **false** caso contrário.</span><span class="sxs-lookup"><span data-stu-id="27f42-401">Returns **true** if first argument is less than or equal toohello second one, return **false** otherwise.</span></span><br /><br /> <span data-ttu-id="27f42-402">Coalesce.</span><span class="sxs-lookup"><span data-stu-id="27f42-402">Coalesce.</span></span> <span data-ttu-id="27f42-403">Retorna Olá segundo argumento se Olá primeiro argumento for um **indefinido** valor.</span><span class="sxs-lookup"><span data-stu-id="27f42-403">Returns hello second argument if hello first argument is an **undefined** value.</span></span>|  
|<span data-ttu-id="27f42-404">**Cadeia de caracteres**</span><span class="sxs-lookup"><span data-stu-id="27f42-404">**String**</span></span>|<span data-ttu-id="27f42-405">**&#124;&#124;**</span><span class="sxs-lookup"><span data-stu-id="27f42-405">**&#124;&#124;**</span></span>|<span data-ttu-id="27f42-406">Concatenação.</span><span class="sxs-lookup"><span data-stu-id="27f42-406">Concatenation.</span></span> <span data-ttu-id="27f42-407">Retorna uma concatenação dos dois argumentos.</span><span class="sxs-lookup"><span data-stu-id="27f42-407">Returns a concatenation of both arguments.</span></span>|  
  
 <span data-ttu-id="27f42-408">**Operadores ternários:**</span><span class="sxs-lookup"><span data-stu-id="27f42-408">**Ternary operators:**</span></span>  
  
|<span data-ttu-id="27f42-409">Operador ternário</span><span class="sxs-lookup"><span data-stu-id="27f42-409">Ternary operator</span></span>|<span data-ttu-id="27f42-410">?</span><span class="sxs-lookup"><span data-stu-id="27f42-410">?</span></span>|<span data-ttu-id="27f42-411">Retorna Olá segundo argumento se Olá primeiro argumento for avaliado muito**true**; retorna o terceiro argumento de saudação caso contrário.</span><span class="sxs-lookup"><span data-stu-id="27f42-411">Returns hello second argument if hello first argument evaluates too**true**; return hello third argument otherwise.</span></span>|  
|-|-|-|  
  
 <span data-ttu-id="27f42-412">**Ordenação dos valores para comparação**</span><span class="sxs-lookup"><span data-stu-id="27f42-412">**Ordering of values for comparison**</span></span>  
  
|<span data-ttu-id="27f42-413">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="27f42-413">**Type**</span></span>|<span data-ttu-id="27f42-414">**Ordem de valores**</span><span class="sxs-lookup"><span data-stu-id="27f42-414">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="27f42-415">**Indefinido**</span><span class="sxs-lookup"><span data-stu-id="27f42-415">**Undefined**</span></span>|<span data-ttu-id="27f42-416">Não é comparável.</span><span class="sxs-lookup"><span data-stu-id="27f42-416">Not comparable.</span></span>|  
|<span data-ttu-id="27f42-417">**Nulo**</span><span class="sxs-lookup"><span data-stu-id="27f42-417">**Null**</span></span>|<span data-ttu-id="27f42-418">Valor único: **nulo**</span><span class="sxs-lookup"><span data-stu-id="27f42-418">Single value: **null**</span></span>|  
|<span data-ttu-id="27f42-419">**Número**</span><span class="sxs-lookup"><span data-stu-id="27f42-419">**Number**</span></span>|<span data-ttu-id="27f42-420">Número real natural.</span><span class="sxs-lookup"><span data-stu-id="27f42-420">Natural real number.</span></span><br /><br /> <span data-ttu-id="27f42-421">O valor infinito negativo é menor do que qualquer outro valor numérico.</span><span class="sxs-lookup"><span data-stu-id="27f42-421">Negative Infinity value is smaller than any other Number value.</span></span><br /><br /> <span data-ttu-id="27f42-422">Um valor infinito positivo é maior do que qualquer outro valor numérico. O valor **NaN** não é comparável.</span><span class="sxs-lookup"><span data-stu-id="27f42-422">Positive Infinity value is larger than any other Number value.**NaN** value is not comparable.</span></span> <span data-ttu-id="27f42-423">A comparação com **NaN** resultará em um valor **indefinido**.</span><span class="sxs-lookup"><span data-stu-id="27f42-423">Comparing with **NaN** will result in **undefined** value.</span></span>|  
|<span data-ttu-id="27f42-424">**Cadeia de caracteres**</span><span class="sxs-lookup"><span data-stu-id="27f42-424">**String**</span></span>|<span data-ttu-id="27f42-425">Ordem lexicográfica.</span><span class="sxs-lookup"><span data-stu-id="27f42-425">Lexicographical order.</span></span>|  
|<span data-ttu-id="27f42-426">**Matriz**</span><span class="sxs-lookup"><span data-stu-id="27f42-426">**Array**</span></span>|<span data-ttu-id="27f42-427">Nenhuma ordem, mas justa.</span><span class="sxs-lookup"><span data-stu-id="27f42-427">No ordering, but equitable.</span></span>|  
|<span data-ttu-id="27f42-428">**Objeto**</span><span class="sxs-lookup"><span data-stu-id="27f42-428">**Object**</span></span>|<span data-ttu-id="27f42-429">Nenhuma ordem, mas justa.</span><span class="sxs-lookup"><span data-stu-id="27f42-429">No ordering, but equitable.</span></span>|  
  
 <span data-ttu-id="27f42-430">**Comentários**</span><span class="sxs-lookup"><span data-stu-id="27f42-430">**Remarks**</span></span>  
  
 <span data-ttu-id="27f42-431">No banco de dados do Azure Cosmos, tipos de saudação de valores geralmente não são conhecidos até que eles sejam realmente recuperados do banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-431">In Azure Cosmos DB, hello types of values are often not known until they are actually retrieved from hello database.</span></span> <span data-ttu-id="27f42-432">Em ordem toosupport uma execução eficiente de consultas, a maioria dos operadores de saudação tiver requisitos de tipo estrito.</span><span class="sxs-lookup"><span data-stu-id="27f42-432">In order toosupport efficient execution of queries, most of hello operators have strict type requirements.</span></span> <span data-ttu-id="27f42-433">Além disso, os operadores por si só não executam conversões implícitas.</span><span class="sxs-lookup"><span data-stu-id="27f42-433">Also operators by themselves do not perform implicit conversions.</span></span>  
  
 <span data-ttu-id="27f42-434">Isso significa que uma consulta como: selecione * FROM ROOT r WHERE age = 21 retornará apenas documentos com a propriedade número de toohello igual idade 21.</span><span class="sxs-lookup"><span data-stu-id="27f42-434">This means that a query like: SELECT * FROM ROOT r WHERE r.Age = 21 will only return documents with property Age equal toohello number 21.</span></span> <span data-ttu-id="27f42-435">Documentos com a cadeia de caracteres de propriedade Age igual toohello "21" ou cadeia de caracteres hello "0021" não corresponderão, como expressão hello "21" = 21 é avaliada tooundefined.</span><span class="sxs-lookup"><span data-stu-id="27f42-435">Documents with property Age equal toohello string "21" or hello string "0021" will not match, as hello expression "21" = 21 evaluates tooundefined.</span></span> <span data-ttu-id="27f42-436">Isso permite um melhor uso de índices, pois a pesquisa Olá de um valor específico (por exemplo, número 21) é mais rápido que a pesquisa por um número indefinido de possíveis correspondências (ou seja, número 21 ou cadeias de caracteres "21", "021", "21.0"...).</span><span class="sxs-lookup"><span data-stu-id="27f42-436">This allows for a better use of indexes, because hello lookup of a specific value (i.e. number 21) is faster than search for indefinite number of potential matches (i.e. number 21 or strings "21", "021", "21.0" …).</span></span> <span data-ttu-id="27f42-437">Isso é diferente de como o JavaScript avalia os operadores em relação a valores de tipos diferentes.</span><span class="sxs-lookup"><span data-stu-id="27f42-437">This is different from how JavaScript evaluates operators on values of different types.</span></span>  
  
 <span data-ttu-id="27f42-438">**Comparação e igualdade de objetos e matrizes**</span><span class="sxs-lookup"><span data-stu-id="27f42-438">**Arrays and objects equality and comparison**</span></span>  
  
 <span data-ttu-id="27f42-439">A comparação de valores de objeto ou matriz usando os operadores de intervalo (>, >=, <, <=) resulta em indefinido, pois não tem ordem definida nos valores de objeto ou matriz.</span><span class="sxs-lookup"><span data-stu-id="27f42-439">Comparing of Array or Object values using range operators (>, >=, <, <=) will result in undefined as there is not order defined on Object or Array values.</span></span> <span data-ttu-id="27f42-440">No entanto, o uso de operadores de igualdade/desigualdade (=,! =, <>) tem suporte e os valores são comparados estruturalmente.</span><span class="sxs-lookup"><span data-stu-id="27f42-440">However using equality/inequality operators (=, !=, <>) is supported and values will be compared structurally.</span></span>  
  
 <span data-ttu-id="27f42-441">As matrizes são iguais se as duas matrizes têm o mesmo número de elementos e os elementos em posições de correspondência também são iguais.</span><span class="sxs-lookup"><span data-stu-id="27f42-441">Arrays are equal if both arrays have same number of elements and elements at matching positions are also equal.</span></span> <span data-ttu-id="27f42-442">Se comparar qualquer par de elementos resulta em indefinido, o resultado de saudação de comparação de matriz é indefinido.</span><span class="sxs-lookup"><span data-stu-id="27f42-442">If comparing any pair of elements results in undefined, hello result of array comparison is undefined.</span></span>  
  
 <span data-ttu-id="27f42-443">Os objetos são iguais se os dois objetos têm as mesmas propriedades definidas e se os valores das propriedades correspondentes também são iguais.</span><span class="sxs-lookup"><span data-stu-id="27f42-443">Objects are equal if both objects have same properties defined, and if values of matching properties are also equal.</span></span> <span data-ttu-id="27f42-444">Se comparar qualquer par de valores de propriedade resulta em indefinido, o resultado de saudação de comparação de objeto será indefinido.</span><span class="sxs-lookup"><span data-stu-id="27f42-444">If comparing any pair of property values results in undefined, hello result of object comparison is undefined.</span></span>  
  
##  <span data-ttu-id="27f42-445"><a name="bk_constants"></a> Constantes</span><span class="sxs-lookup"><span data-stu-id="27f42-445"><a name="bk_constants"></a> Constants</span></span>  
 <span data-ttu-id="27f42-446">Uma constante, também conhecida como valor literal ou escalar, é um símbolo que representa um valor de dados específico.</span><span class="sxs-lookup"><span data-stu-id="27f42-446">A constant, also known as a literal or a scalar value, is a symbol that represents a specific data value.</span></span> <span data-ttu-id="27f42-447">formato de saudação de uma constante depende de tipo de dados de saudação do valor de saudação representa.</span><span class="sxs-lookup"><span data-stu-id="27f42-447">hello format of a constant depends on hello data type of hello value it represents.</span></span>  
  
 <span data-ttu-id="27f42-448">**Suporte para tipos de dados escalares:**</span><span class="sxs-lookup"><span data-stu-id="27f42-448">**Supported scalar data types:**</span></span>  
  
|<span data-ttu-id="27f42-449">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="27f42-449">**Type**</span></span>|<span data-ttu-id="27f42-450">**Ordem de valores**</span><span class="sxs-lookup"><span data-stu-id="27f42-450">**Values order**</span></span>|  
|-|-|  
|<span data-ttu-id="27f42-451">**Indefinido**</span><span class="sxs-lookup"><span data-stu-id="27f42-451">**Undefined**</span></span>|<span data-ttu-id="27f42-452">Valor único: **indefinido**</span><span class="sxs-lookup"><span data-stu-id="27f42-452">Single value: **undefined**</span></span>|  
|<span data-ttu-id="27f42-453">**Nulo**</span><span class="sxs-lookup"><span data-stu-id="27f42-453">**Null**</span></span>|<span data-ttu-id="27f42-454">Valor único: **nulo**</span><span class="sxs-lookup"><span data-stu-id="27f42-454">Single value: **null**</span></span>|  
|<span data-ttu-id="27f42-455">**Booliano**</span><span class="sxs-lookup"><span data-stu-id="27f42-455">**Boolean**</span></span>|<span data-ttu-id="27f42-456">Valores: **falso**, **verdadeiro**.</span><span class="sxs-lookup"><span data-stu-id="27f42-456">Values: **false**, **true**.</span></span>|  
|<span data-ttu-id="27f42-457">**Número**</span><span class="sxs-lookup"><span data-stu-id="27f42-457">**Number**</span></span>|<span data-ttu-id="27f42-458">Um número de ponto flutuante de precisão dupla, padrão IEEE 754.</span><span class="sxs-lookup"><span data-stu-id="27f42-458">A double-precision floating-point number, IEEE 754 standard.</span></span>|  
|<span data-ttu-id="27f42-459">**Cadeia de caracteres**</span><span class="sxs-lookup"><span data-stu-id="27f42-459">**String**</span></span>|<span data-ttu-id="27f42-460">Uma sequência de zero ou mais caracteres Unicode.</span><span class="sxs-lookup"><span data-stu-id="27f42-460">A sequence of zero or more Unicode characters.</span></span> <span data-ttu-id="27f42-461">As cadeias de caracteres devem ser colocadas entre aspas simples ou duplas.</span><span class="sxs-lookup"><span data-stu-id="27f42-461">Strings must be enclosed in single or double quotes.</span></span>|  
|<span data-ttu-id="27f42-462">**Matriz**</span><span class="sxs-lookup"><span data-stu-id="27f42-462">**Array**</span></span>|<span data-ttu-id="27f42-463">Uma sequência de zero ou mais elementos.</span><span class="sxs-lookup"><span data-stu-id="27f42-463">A sequence of zero or more elements.</span></span> <span data-ttu-id="27f42-464">Cada elemento pode ser um valor de qualquer tipo de dados escalares, exceto Indefinido.</span><span class="sxs-lookup"><span data-stu-id="27f42-464">Each element can be a value of any scalar data type, except Undefined.</span></span>|  
|<span data-ttu-id="27f42-465">**Objeto**</span><span class="sxs-lookup"><span data-stu-id="27f42-465">**Object**</span></span>|<span data-ttu-id="27f42-466">Um conjunto ordenado de zero ou mais pares de nome/valor.</span><span class="sxs-lookup"><span data-stu-id="27f42-466">An unordered set of zero or more name/value pairs.</span></span> <span data-ttu-id="27f42-467">Nome é uma cadeia de caracteres Unicode; o valor pode ser de qualquer tipo de dados escalares, exceto **Indefinido**.</span><span class="sxs-lookup"><span data-stu-id="27f42-467">Name is a Unicode string, value can be of any scalar data type, except **Undefined**.</span></span>|  
  
 <span data-ttu-id="27f42-468">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-468">**Syntax**</span></span>  
  
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
  
 <span data-ttu-id="27f42-469">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-469">**Arguments**</span></span>  
  
1.  `<undefined_constant>; undefined`  
  
     <span data-ttu-id="27f42-470">Representa o valor indefinido do tipo Indefinido.</span><span class="sxs-lookup"><span data-stu-id="27f42-470">Represents undefined value of type Undefined.</span></span>  
  
2.  `<null_constant>; null`  
  
     <span data-ttu-id="27f42-471">Representa o valor **null** do tipo **Nulo**.</span><span class="sxs-lookup"><span data-stu-id="27f42-471">Represents **null** value of type **Null**.</span></span>  
  
3.  `<boolean_constant>`  
  
     <span data-ttu-id="27f42-472">Representa a constante do tipo booliano.</span><span class="sxs-lookup"><span data-stu-id="27f42-472">Represents constant of type Boolean.</span></span>  
  
4.  `false`  
  
     <span data-ttu-id="27f42-473">Representa o valor **false** do tipo booliano.</span><span class="sxs-lookup"><span data-stu-id="27f42-473">Represents **false** value of type Boolean.</span></span>  
  
5.  `true`  
  
     <span data-ttu-id="27f42-474">Representa o valor **true** do tipo booliano.</span><span class="sxs-lookup"><span data-stu-id="27f42-474">Represents **true** value of type Boolean.</span></span>  
  
6.  `<number_constant>`  
  
     <span data-ttu-id="27f42-475">Representa uma constante.</span><span class="sxs-lookup"><span data-stu-id="27f42-475">Represents a constant.</span></span>  
  
7.  `decimal_literal`  
  
     <span data-ttu-id="27f42-476">Os literais decimais são números representados usando notação decimal ou notação científica.</span><span class="sxs-lookup"><span data-stu-id="27f42-476">Decimal literals are numbers represented using either decimal notation, or scientific notation.</span></span>  
  
8.  `hexadecimal_literal`  
  
     <span data-ttu-id="27f42-477">Os literais hexadecimais são números representados usando o prefixo '0x' seguido por um ou mais dígitos hexadecimais.</span><span class="sxs-lookup"><span data-stu-id="27f42-477">Hexadecimal literals are numbers represented using prefix '0x' followed by one or more hexadecimal digits.</span></span>  
  
9. `<string_constant>`  
  
     <span data-ttu-id="27f42-478">Representa uma constante do tipo Cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="27f42-478">Represents a constant of type String.</span></span>  
  
10. `string _literal`  
  
     <span data-ttu-id="27f42-479">Literais de cadeia de caracteres são cadeias de caracteres Unicode representadas por uma sequência de zero ou mais caracteres Unicode ou sequências de escape.</span><span class="sxs-lookup"><span data-stu-id="27f42-479">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="27f42-480">As literais de cadeia de caracteres são colocadas entre aspas simples (apóstrofe: ') ou aspas duplas (aspas: ").</span><span class="sxs-lookup"><span data-stu-id="27f42-480">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span>  
  
 <span data-ttu-id="27f42-481">As seguintes sequências de escape são permitidas:</span><span class="sxs-lookup"><span data-stu-id="27f42-481">Following escape sequences are allowed:</span></span>  
  
|<span data-ttu-id="27f42-482">**Sequência de escape**</span><span class="sxs-lookup"><span data-stu-id="27f42-482">**Escape sequence**</span></span>|<span data-ttu-id="27f42-483">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="27f42-483">**Description**</span></span>|<span data-ttu-id="27f42-484">**Caractere Unicode**</span><span class="sxs-lookup"><span data-stu-id="27f42-484">**Unicode character**</span></span>|  
|-|-|-|  
|<span data-ttu-id="27f42-485">\\'</span><span class="sxs-lookup"><span data-stu-id="27f42-485">\\'</span></span>|<span data-ttu-id="27f42-486">apóstrofo (')</span><span class="sxs-lookup"><span data-stu-id="27f42-486">apostrophe (')</span></span>|<span data-ttu-id="27f42-487">U+0027</span><span class="sxs-lookup"><span data-stu-id="27f42-487">U+0027</span></span>|  
|<span data-ttu-id="27f42-488">\\"</span><span class="sxs-lookup"><span data-stu-id="27f42-488">\\"</span></span>|<span data-ttu-id="27f42-489">aspas (")</span><span class="sxs-lookup"><span data-stu-id="27f42-489">quotation mark (")</span></span>|<span data-ttu-id="27f42-490">U+0022</span><span class="sxs-lookup"><span data-stu-id="27f42-490">U+0022</span></span>|  
|\\\|<span data-ttu-id="27f42-491">barra invertida (\\)</span><span class="sxs-lookup"><span data-stu-id="27f42-491">reverse solidus (\\)</span></span>|<span data-ttu-id="27f42-492">U+005C</span><span class="sxs-lookup"><span data-stu-id="27f42-492">U+005C</span></span>|  
|\\/|<span data-ttu-id="27f42-493">barra (/)</span><span class="sxs-lookup"><span data-stu-id="27f42-493">solidus (/)</span></span>|<span data-ttu-id="27f42-494">U+002F</span><span class="sxs-lookup"><span data-stu-id="27f42-494">U+002F</span></span>|  
|<span data-ttu-id="27f42-495">\b</span><span class="sxs-lookup"><span data-stu-id="27f42-495">\b</span></span>|<span data-ttu-id="27f42-496">backspace</span><span class="sxs-lookup"><span data-stu-id="27f42-496">backspace</span></span>|<span data-ttu-id="27f42-497">U+0008</span><span class="sxs-lookup"><span data-stu-id="27f42-497">U+0008</span></span>|  
|<span data-ttu-id="27f42-498">\f</span><span class="sxs-lookup"><span data-stu-id="27f42-498">\f</span></span>|<span data-ttu-id="27f42-499">avanço de página</span><span class="sxs-lookup"><span data-stu-id="27f42-499">form feed</span></span>|<span data-ttu-id="27f42-500">U+000C</span><span class="sxs-lookup"><span data-stu-id="27f42-500">U+000C</span></span>|  
|\n|<span data-ttu-id="27f42-501">alimentação de linha</span><span class="sxs-lookup"><span data-stu-id="27f42-501">line feed</span></span>|<span data-ttu-id="27f42-502">U+000A</span><span class="sxs-lookup"><span data-stu-id="27f42-502">U+000A</span></span>|  
|<span data-ttu-id="27f42-503">\r</span><span class="sxs-lookup"><span data-stu-id="27f42-503">\r</span></span>|<span data-ttu-id="27f42-504">retorno de carro</span><span class="sxs-lookup"><span data-stu-id="27f42-504">carriage return</span></span>|<span data-ttu-id="27f42-505">U+000D</span><span class="sxs-lookup"><span data-stu-id="27f42-505">U+000D</span></span>|  
|<span data-ttu-id="27f42-506">\t</span><span class="sxs-lookup"><span data-stu-id="27f42-506">\t</span></span>|<span data-ttu-id="27f42-507">tab</span><span class="sxs-lookup"><span data-stu-id="27f42-507">tab</span></span>|<span data-ttu-id="27f42-508">U+0009</span><span class="sxs-lookup"><span data-stu-id="27f42-508">U+0009</span></span>|  
|<span data-ttu-id="27f42-509">\uXXXX</span><span class="sxs-lookup"><span data-stu-id="27f42-509">\uXXXX</span></span>|<span data-ttu-id="27f42-510">Um caractere Unicode definido por 4 dígitos hexadecimais.</span><span class="sxs-lookup"><span data-stu-id="27f42-510">A Unicode character defined by 4 hexadecimal digits.</span></span>|<span data-ttu-id="27f42-511">U+XXXX</span><span class="sxs-lookup"><span data-stu-id="27f42-511">U+XXXX</span></span>|  
  
##  <span data-ttu-id="27f42-512"><a name="bk_query_perf_guidelines"></a>Diretrizes de desempenho de consulta</span><span class="sxs-lookup"><span data-stu-id="27f42-512"><a name="bk_query_perf_guidelines"></a> Query performance guidelines</span></span>  
 <span data-ttu-id="27f42-513">Para um toobe consulta executada com eficiência para uma grande coleção, ele deve usar filtros que podem ser atendidos por meio de um ou mais índices.</span><span class="sxs-lookup"><span data-stu-id="27f42-513">In order for a query toobe executed efficiently for a large collection, it should use filters which can be served through one or more indexes.</span></span>  
  
 <span data-ttu-id="27f42-514">Olá filtros a seguir será considerado para o índice de pesquisa:</span><span class="sxs-lookup"><span data-stu-id="27f42-514">hello following filters will be considered for index lookup:</span></span>  
  
-   <span data-ttu-id="27f42-515">Use o operador de igualdade (=) com uma expressão de caminho de documento e uma constante.</span><span class="sxs-lookup"><span data-stu-id="27f42-515">Use equality operator ( = ) with a document path expression and a constant.</span></span>  
  
-   <span data-ttu-id="27f42-516">Use o operador de intervalo (<, \<=, >, >=) com uma expressão de caminho de documento e constantes numéricas.</span><span class="sxs-lookup"><span data-stu-id="27f42-516">Use range operators (<, \<=, >, >=) with a document path expression and number constants.</span></span>  
  
-   <span data-ttu-id="27f42-517">Expressão de caminho de documento significa qualquer expressão que identifica um caminho constante nos documentos de saudação da coleção de banco de dados de saudação referenciada.</span><span class="sxs-lookup"><span data-stu-id="27f42-517">Document path expression stands for any expression which identifies a constant path in hello documents from hello referenced database collection.</span></span>  
  
 <span data-ttu-id="27f42-518">**Expressão de caminho de documento**</span><span class="sxs-lookup"><span data-stu-id="27f42-518">**Document path expression**</span></span>  
  
 <span data-ttu-id="27f42-519">Expressões de caminho de documento são expressões que um caminho de propriedade ou um indexador de matriz avalia em um documento proveniente dos documentos da coleção do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="27f42-519">Document path expressions are expressions that a path of property or array indexer assessors over a document coming from database collection documents.</span></span> <span data-ttu-id="27f42-520">Esse caminho pode ser usado tooidentify Olá local de valores referenciados em um filtro diretamente dentro de documentos de saudação na coleção de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-520">This path can be used tooidentify hello location of values referenced in a filter directly within hello documents in hello database collection.</span></span>  
  
 <span data-ttu-id="27f42-521">Para um toobe expressão considerada uma expressão de caminho de documento, ele deve:</span><span class="sxs-lookup"><span data-stu-id="27f42-521">For an expression toobe considered a document path expression, it should:</span></span>  
  
1.  <span data-ttu-id="27f42-522">Diretamente raiz da referência Olá coleção.</span><span class="sxs-lookup"><span data-stu-id="27f42-522">Reference hello collection root directly.</span></span>  
  
2.  <span data-ttu-id="27f42-523">Fazer referência ao indexador de matriz da constante ou à propriedade de alguma expressão de caminho de documento</span><span class="sxs-lookup"><span data-stu-id="27f42-523">Reference property or constant array indexer of some document path expression</span></span>  
  
3.  <span data-ttu-id="27f42-524">Fazer referência a um alias que represente alguma expressão de caminho de documento.</span><span class="sxs-lookup"><span data-stu-id="27f42-524">Reference an alias, which represents some document path expression.</span></span>  
  
     <span data-ttu-id="27f42-525">**Convenções de sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-525">**Syntax conventions**</span></span>  
  
     <span data-ttu-id="27f42-526">Olá, a tabela a seguir descreve Olá convenções usadas toodescribe sintaxe na referência de linguagem de consulta do DocumentDB API hello.</span><span class="sxs-lookup"><span data-stu-id="27f42-526">hello following table describes hello conventions used toodescribe syntax in hello DocumentDB API Query Language reference.</span></span>  
  
    |<span data-ttu-id="27f42-527">**Convenção**</span><span class="sxs-lookup"><span data-stu-id="27f42-527">**Convention**</span></span>|<span data-ttu-id="27f42-528">**Usadas para**</span><span class="sxs-lookup"><span data-stu-id="27f42-528">**Used for**</span></span>|  
    |-|-|    
    |<span data-ttu-id="27f42-529">LETRAS MAIÚSCULAS</span><span class="sxs-lookup"><span data-stu-id="27f42-529">UPPERCASE</span></span>|<span data-ttu-id="27f42-530">Palavras-chave não diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="27f42-530">Case-insensitive keywords.</span></span>|  
    |<span data-ttu-id="27f42-531">letras minúsculas</span><span class="sxs-lookup"><span data-stu-id="27f42-531">lowercase</span></span>|<span data-ttu-id="27f42-532">Palavras-chave diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="27f42-532">Case-sensitive keywords.</span></span>|  
    |<span data-ttu-id="27f42-533">\<não terminal></span><span class="sxs-lookup"><span data-stu-id="27f42-533">\<nonterminal></span></span>|<span data-ttu-id="27f42-534">Não terminal, definido separadamente.</span><span class="sxs-lookup"><span data-stu-id="27f42-534">Nonterminal, defined separately.</span></span>|  
    |<span data-ttu-id="27f42-535">\<não terminal> ::=</span><span class="sxs-lookup"><span data-stu-id="27f42-535">\<nonterminal> ::=</span></span>|<span data-ttu-id="27f42-536">Definição de sintaxe do não terminal de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-536">Syntax definition of hello nonterminal.</span></span>|  
    |<span data-ttu-id="27f42-537">other_terminal</span><span class="sxs-lookup"><span data-stu-id="27f42-537">other_terminal</span></span>|<span data-ttu-id="27f42-538">Terminal (token), descritos em detalhes em palavras.</span><span class="sxs-lookup"><span data-stu-id="27f42-538">Terminal (token), described in detail in words.</span></span>|  
    |<span data-ttu-id="27f42-539">identificador</span><span class="sxs-lookup"><span data-stu-id="27f42-539">identifier</span></span>|<span data-ttu-id="27f42-540">Identificador.</span><span class="sxs-lookup"><span data-stu-id="27f42-540">Identifier.</span></span> <span data-ttu-id="27f42-541">Permite apenas os seguintes caracteres: a-z A-Z 0-9 _O primeiro caractere não pode ser um dígito.</span><span class="sxs-lookup"><span data-stu-id="27f42-541">Allows following characters only: a-z A-Z 0-9 _First character cannot be a digit.</span></span>|  
    |<span data-ttu-id="27f42-542">“cadeia de caracteres”</span><span class="sxs-lookup"><span data-stu-id="27f42-542">"string"</span></span>|<span data-ttu-id="27f42-543">Cadeia de caracteres entre aspas.</span><span class="sxs-lookup"><span data-stu-id="27f42-543">Quoted string.</span></span> <span data-ttu-id="27f42-544">Permite qualquer cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-544">Allows any valid string.</span></span> <span data-ttu-id="27f42-545">Consulte a descrição de um string_literal.</span><span class="sxs-lookup"><span data-stu-id="27f42-545">See description of a string_literal.</span></span>|  
    |<span data-ttu-id="27f42-546">'símbolo'</span><span class="sxs-lookup"><span data-stu-id="27f42-546">'symbol'</span></span>|<span data-ttu-id="27f42-547">Símbolo literal que faz parte da sintaxe de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-547">Literal symbol which is part of hello syntax.</span></span>|  
    |<span data-ttu-id="27f42-548">&#124; (barra vertical)</span><span class="sxs-lookup"><span data-stu-id="27f42-548">&#124; (vertical bar)</span></span>|<span data-ttu-id="27f42-549">Alternativas para itens de sintaxe.</span><span class="sxs-lookup"><span data-stu-id="27f42-549">Alternatives for syntax items.</span></span> <span data-ttu-id="27f42-550">Você pode usar apenas um dos itens de saudação especificados.</span><span class="sxs-lookup"><span data-stu-id="27f42-550">You can use only one of hello items specified.</span></span>|  
    |<span data-ttu-id="27f42-551">[ ] /(colchetes)</span><span class="sxs-lookup"><span data-stu-id="27f42-551">[ ] /(brackets)</span></span>|<span data-ttu-id="27f42-552">Os colchetes colocam um ou mais itens opcionais.</span><span class="sxs-lookup"><span data-stu-id="27f42-552">Brackets enclose one or more optional items.</span></span>|  
    |<span data-ttu-id="27f42-553">[ ,...n ]</span><span class="sxs-lookup"><span data-stu-id="27f42-553">[ ,...n ]</span></span>|<span data-ttu-id="27f42-554">Indica a saudação precede item pode ser repetido n número de vezes.</span><span class="sxs-lookup"><span data-stu-id="27f42-554">Indicates hello preceding item can be repeated n number of times.</span></span> <span data-ttu-id="27f42-555">Olá ocorrências são separadas por vírgulas.</span><span class="sxs-lookup"><span data-stu-id="27f42-555">hello occurrences are separated by commas.</span></span>|  
    |<span data-ttu-id="27f42-556">[ ...n ]</span><span class="sxs-lookup"><span data-stu-id="27f42-556">[ ...n ]</span></span>|<span data-ttu-id="27f42-557">Indica a saudação precede item pode ser repetido n número de vezes.</span><span class="sxs-lookup"><span data-stu-id="27f42-557">Indicates hello preceding item can be repeated n number of times.</span></span> <span data-ttu-id="27f42-558">Olá ocorrências são separadas por espaços em branco.</span><span class="sxs-lookup"><span data-stu-id="27f42-558">hello occurrences are separated by blanks.</span></span>|  
  
##  <span data-ttu-id="27f42-559"><a name="bk_built_in_functions"></a> Funções internas</span><span class="sxs-lookup"><span data-stu-id="27f42-559"><a name="bk_built_in_functions"></a> Built-in functions</span></span>  
 <span data-ttu-id="27f42-560">O BD Cosmos do Azure fornece muitas funções SQL internas.</span><span class="sxs-lookup"><span data-stu-id="27f42-560">Azure Cosmos DB provides many built-in SQL functions.</span></span> <span data-ttu-id="27f42-561">categorias de saudação de funções internas estão listadas abaixo.</span><span class="sxs-lookup"><span data-stu-id="27f42-561">hello categories of built-in functions are listed below.</span></span>  
  
|<span data-ttu-id="27f42-562">Função</span><span class="sxs-lookup"><span data-stu-id="27f42-562">Function</span></span>|<span data-ttu-id="27f42-563">Descrição</span><span class="sxs-lookup"><span data-stu-id="27f42-563">Description</span></span>|  
|--------------|-----------------|  
|[<span data-ttu-id="27f42-564">Funções matemáticas</span><span class="sxs-lookup"><span data-stu-id="27f42-564">Mathematical functions</span></span>](#bk_mathematical_functions)|<span data-ttu-id="27f42-565">Olá funções matemáticas executam um cálculo, normalmente com base em valores de entrada que são fornecidos como argumentos e retornam um valor numérico.</span><span class="sxs-lookup"><span data-stu-id="27f42-565">hello mathematical functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>|  
|[<span data-ttu-id="27f42-566">Funções de verificação de tipo</span><span class="sxs-lookup"><span data-stu-id="27f42-566">Type checking functions</span></span>](#bk_type_checking_functions)|<span data-ttu-id="27f42-567">funções de verificação de tipo Hello permitem tipo de saudação toocheck de uma expressão em consultas SQL.</span><span class="sxs-lookup"><span data-stu-id="27f42-567">hello type checking functions allow you toocheck hello type of an expression within SQL queries.</span></span>|  
|[<span data-ttu-id="27f42-568">Funções de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="27f42-568">String functions</span></span>](#bk_string_functions)|<span data-ttu-id="27f42-569">funções de cadeia de caracteres de saudação executam uma operação em um valor de cadeia de caracteres de entrada e retornam uma cadeia de caracteres, o valor numérico ou booleano.</span><span class="sxs-lookup"><span data-stu-id="27f42-569">hello string functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>|  
|[<span data-ttu-id="27f42-570">Funções de matriz</span><span class="sxs-lookup"><span data-stu-id="27f42-570">Array functions</span></span>](#bk_array_functions)|<span data-ttu-id="27f42-571">funções de matriz Olá executam uma operação em um valor de entrada de matriz e numérico de retorno, um valor booleano ou de matriz.</span><span class="sxs-lookup"><span data-stu-id="27f42-571">hello array functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span>|  
|[<span data-ttu-id="27f42-572">Funções espaciais</span><span class="sxs-lookup"><span data-stu-id="27f42-572">Spatial functions</span></span>](#bk_spatial_functions)|<span data-ttu-id="27f42-573">funções espaciais Olá executam uma operação em um valor de entrada do objeto espacial e retornam um valor numérico ou booleano.</span><span class="sxs-lookup"><span data-stu-id="27f42-573">hello spatial functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>|  
  
###  <span data-ttu-id="27f42-574"><a name="bk_mathematical_functions"></a>Funções matemáticas</span><span class="sxs-lookup"><span data-stu-id="27f42-574"><a name="bk_mathematical_functions"></a> Mathematical functions</span></span>  
 <span data-ttu-id="27f42-575">Olá funções a seguir executam um cálculo, normalmente com base em valores de entrada que são fornecidos como argumentos e retornam um valor numérico.</span><span class="sxs-lookup"><span data-stu-id="27f42-575">hello following functions each perform a calculation, usually based on input values that are provided as arguments, and return a numeric value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="27f42-576">ABS</span><span class="sxs-lookup"><span data-stu-id="27f42-576">ABS</span></span>](#bk_abs)|[<span data-ttu-id="27f42-577">ACOS</span><span class="sxs-lookup"><span data-stu-id="27f42-577">ACOS</span></span>](#bk_acos)|[<span data-ttu-id="27f42-578">ASIN</span><span class="sxs-lookup"><span data-stu-id="27f42-578">ASIN</span></span>](#bk_asin)|  
|[<span data-ttu-id="27f42-579">ATAN</span><span class="sxs-lookup"><span data-stu-id="27f42-579">ATAN</span></span>](#bk_atan)|[<span data-ttu-id="27f42-580">ATN2</span><span class="sxs-lookup"><span data-stu-id="27f42-580">ATN2</span></span>](#bk_atn2)|[<span data-ttu-id="27f42-581">CEILING</span><span class="sxs-lookup"><span data-stu-id="27f42-581">CEILING</span></span>](#bk_ceiling)|  
|[<span data-ttu-id="27f42-582">COS</span><span class="sxs-lookup"><span data-stu-id="27f42-582">COS</span></span>](#bk_cos)|[<span data-ttu-id="27f42-583">COT</span><span class="sxs-lookup"><span data-stu-id="27f42-583">COT</span></span>](#bk_cot)|[<span data-ttu-id="27f42-584">DEGREES</span><span class="sxs-lookup"><span data-stu-id="27f42-584">DEGREES</span></span>](#bk_degrees)|  
|[<span data-ttu-id="27f42-585">EXP</span><span class="sxs-lookup"><span data-stu-id="27f42-585">EXP</span></span>](#bk_exp)|[<span data-ttu-id="27f42-586">FLOOR</span><span class="sxs-lookup"><span data-stu-id="27f42-586">FLOOR</span></span>](#bk_floor)|[<span data-ttu-id="27f42-587">LOG</span><span class="sxs-lookup"><span data-stu-id="27f42-587">LOG</span></span>](#bk_log)|  
|[<span data-ttu-id="27f42-588">LOG10</span><span class="sxs-lookup"><span data-stu-id="27f42-588">LOG10</span></span>](#bk_log10)|[<span data-ttu-id="27f42-589">PI</span><span class="sxs-lookup"><span data-stu-id="27f42-589">PI</span></span>](#bk_pi)|[<span data-ttu-id="27f42-590">POWER</span><span class="sxs-lookup"><span data-stu-id="27f42-590">POWER</span></span>](#bk_power)|  
|[<span data-ttu-id="27f42-591">RADIANS</span><span class="sxs-lookup"><span data-stu-id="27f42-591">RADIANS</span></span>](#bk_radians)|[<span data-ttu-id="27f42-592">ROUND</span><span class="sxs-lookup"><span data-stu-id="27f42-592">ROUND</span></span>](#bk_round)|[<span data-ttu-id="27f42-593">SIN</span><span class="sxs-lookup"><span data-stu-id="27f42-593">SIN</span></span>](#bk_sin)|  
|[<span data-ttu-id="27f42-594">SQRT</span><span class="sxs-lookup"><span data-stu-id="27f42-594">SQRT</span></span>](#bk_sqrt)|[<span data-ttu-id="27f42-595">SQUARE</span><span class="sxs-lookup"><span data-stu-id="27f42-595">SQUARE</span></span>](#bk_square)|[<span data-ttu-id="27f42-596">SIGN</span><span class="sxs-lookup"><span data-stu-id="27f42-596">SIGN</span></span>](#bk_sign)|  
|[<span data-ttu-id="27f42-597">TAN</span><span class="sxs-lookup"><span data-stu-id="27f42-597">TAN</span></span>](#bk_tan)|[<span data-ttu-id="27f42-598">TRUNC</span><span class="sxs-lookup"><span data-stu-id="27f42-598">TRUNC</span></span>](#bk_trunc)||  
  
####  <span data-ttu-id="27f42-599"><a name="bk_abs"></a> ABS</span><span class="sxs-lookup"><span data-stu-id="27f42-599"><a name="bk_abs"></a> ABS</span></span>  
 <span data-ttu-id="27f42-600">Retorna Olá valor absoluto (positivo) da saudação especificado expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-600">Returns hello absolute (positive) value of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-601">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-601">**Syntax**</span></span>  
  
```  
ABS (<numeric_expression>)  
```  
  
 <span data-ttu-id="27f42-602">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-602">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="27f42-603">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-603">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-604">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-604">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-605">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-605">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-606">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-606">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-607">Hello exemplo a seguir mostra os resultados de saudação do usando a função hello ABS em três números diferentes.</span><span class="sxs-lookup"><span data-stu-id="27f42-607">hello following example shows hello results of using hello ABS function on three different numbers.</span></span>  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 <span data-ttu-id="27f42-608">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-608">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <span data-ttu-id="27f42-609"><a name="bk_acos"></a> ACOS</span><span class="sxs-lookup"><span data-stu-id="27f42-609"><a name="bk_acos"></a> ACOS</span></span>  
 <span data-ttu-id="27f42-610">Ângulo de saudação retorna, em radianos, cujo cosseno é Olá expressão numérica especificada; também chamado de arco cosseno.</span><span class="sxs-lookup"><span data-stu-id="27f42-610">Returns hello angle, in radians, whose cosine is hello specified numeric expression; also called arccosine.</span></span>  
  
 <span data-ttu-id="27f42-611">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-611">**Syntax**</span></span>  
  
```  
ACOS(<numeric_expression>)  
```  
  
 <span data-ttu-id="27f42-612">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-612">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="27f42-613">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-613">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-614">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-614">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-615">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-615">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-616">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-616">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-617">Olá, exemplo a seguir retorna Olá ACOS de -1.</span><span class="sxs-lookup"><span data-stu-id="27f42-617">hello following example returns hello ACOS of -1.</span></span>  
  
```  
SELECT ACOS(-1)  
```  
  
 <span data-ttu-id="27f42-618">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-618">Here is hello result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="27f42-619"><a name="bk_asin"></a> ASIN</span><span class="sxs-lookup"><span data-stu-id="27f42-619"><a name="bk_asin"></a> ASIN</span></span>  
 <span data-ttu-id="27f42-620">Ângulo de saudação retorna, em radianos, cujo seno é hello especificado expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-620">Returns hello angle, in radians, whose sine is hello specified numeric expression.</span></span> <span data-ttu-id="27f42-621">Isso também é chamado de arco seno.</span><span class="sxs-lookup"><span data-stu-id="27f42-621">This is also called arcsine.</span></span>  
  
 <span data-ttu-id="27f42-622">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-622">**Syntax**</span></span>  
  
```  
ASIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="27f42-623">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-623">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="27f42-624">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-624">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-625">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-625">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-626">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-626">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-627">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-627">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-628">Olá, exemplo a seguir retorna Olá ASEN de -1.</span><span class="sxs-lookup"><span data-stu-id="27f42-628">hello following example returns hello ASIN of -1.</span></span>  
  
```  
SELECT ASIN(-1)  
```  
  
 <span data-ttu-id="27f42-629">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-629">Here is hello result set.</span></span>  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <span data-ttu-id="27f42-630"><a name="bk_atan"></a> ATAN</span><span class="sxs-lookup"><span data-stu-id="27f42-630"><a name="bk_atan"></a> ATAN</span></span>  
 <span data-ttu-id="27f42-631">Ângulo de saudação retorna, em radianos, cuja tangente é hello especificado expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-631">Returns hello angle, in radians, whose tangent is hello specified numeric expression.</span></span> <span data-ttu-id="27f42-632">Isso também é chamado de arco tangente.</span><span class="sxs-lookup"><span data-stu-id="27f42-632">This is also called arctangent.</span></span>  
  
 <span data-ttu-id="27f42-633">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-633">**Syntax**</span></span>  
  
```  
ATAN(<numeric_expression>)  
```  
  
 <span data-ttu-id="27f42-634">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-634">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="27f42-635">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-635">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-636">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-636">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-637">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-637">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-638">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-638">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-639">Olá retorna Olá ATAN de saudação do exemplo a seguir o valor especificado.</span><span class="sxs-lookup"><span data-stu-id="27f42-639">hello following example returns hello ATAN of hello specified value.</span></span>  
  
```  
SELECT ATAN(-45.01)  
```  
  
 <span data-ttu-id="27f42-640">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-640">Here is hello result set.</span></span>  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <span data-ttu-id="27f42-641"><a name="bk_atn2"></a> ATN2</span><span class="sxs-lookup"><span data-stu-id="27f42-641"><a name="bk_atn2"></a> ATN2</span></span>  
 <span data-ttu-id="27f42-642">Retorna o valor principal Olá Olá arco tangente de y / x, expressado em radianos.</span><span class="sxs-lookup"><span data-stu-id="27f42-642">Returns hello principal value of hello arc tangent of y/x, expressed in radians.</span></span>  
  
 <span data-ttu-id="27f42-643">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-643">**Syntax**</span></span>  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 <span data-ttu-id="27f42-644">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-644">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="27f42-645">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-645">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-646">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-646">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-647">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-647">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-648">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-648">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-649">Olá, exemplo a seguir calcula hello ATN2 para Olá especificado x e y componentes.</span><span class="sxs-lookup"><span data-stu-id="27f42-649">hello following example calculates hello ATN2 for hello specified x and y components.</span></span>  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 <span data-ttu-id="27f42-650">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-650">Here is hello result set.</span></span>  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <span data-ttu-id="27f42-651"><a name="bk_ceiling"></a> CEILING</span><span class="sxs-lookup"><span data-stu-id="27f42-651"><a name="bk_ceiling"></a> CEILING</span></span>  
 <span data-ttu-id="27f42-652">Retorna Olá menor valor de número inteiro maior ou igual ao Olá expressão numérica especificada.</span><span class="sxs-lookup"><span data-stu-id="27f42-652">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-653">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-653">**Syntax**</span></span>  
  
```  
CEILING (<numeric_expression>)  
```  
  
 <span data-ttu-id="27f42-654">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-654">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="27f42-655">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-655">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-656">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-656">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-657">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-657">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-658">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-658">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-659">saudação de exemplo a seguir mostra numéricos positivos, negativos e valores zero com hello função CEILING.</span><span class="sxs-lookup"><span data-stu-id="27f42-659">hello following example shows positive numeric, negative, and zero values with hello CEILING function.</span></span>  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 <span data-ttu-id="27f42-660">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-660">Here is hello result set.</span></span>  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <span data-ttu-id="27f42-661"><a name="bk_cos"></a> COS</span><span class="sxs-lookup"><span data-stu-id="27f42-661"><a name="bk_cos"></a> COS</span></span>  
 <span data-ttu-id="27f42-662">Retorna Olá cosseno trigonométrico Olá especificado o ângulo em radianos, na Olá expressão especificada.</span><span class="sxs-lookup"><span data-stu-id="27f42-662">Returns hello trigonometric cosine of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="27f42-663">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-663">**Syntax**</span></span>  
  
```  
COS(<numeric_expression>)  
```  
  
 <span data-ttu-id="27f42-664">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-664">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="27f42-665">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-665">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-666">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-666">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-667">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-667">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-668">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-668">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-669">saudação de exemplo a seguir calcula Olá COS de saudação especificado ângulo.</span><span class="sxs-lookup"><span data-stu-id="27f42-669">hello following example calculates hello COS of hello specified angle.</span></span>  
  
```  
SELECT COS(14.78)  
```  
  
 <span data-ttu-id="27f42-670">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-670">Here is hello result set.</span></span>  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <span data-ttu-id="27f42-671"><a name="bk_cot"></a> COT</span><span class="sxs-lookup"><span data-stu-id="27f42-671"><a name="bk_cot"></a> COT</span></span>  
 <span data-ttu-id="27f42-672">Retorna Olá cotangente trigonométrica Olá especificado o ângulo em radianos, Olá especificada expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-672">Returns hello trigonometric cotangent of hello specified angle, in radians, in hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-673">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-673">**Syntax**</span></span>  
  
```  
COT(<numeric_expression>)  
```  
  
 <span data-ttu-id="27f42-674">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-674">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="27f42-675">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-675">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-676">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-676">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-677">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-677">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-678">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-678">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-679">saudação de exemplo a seguir calcula Olá COT do ângulo especificado hello.</span><span class="sxs-lookup"><span data-stu-id="27f42-679">hello following example calculates hello COT of hello specified angle.</span></span>  
  
```  
SELECT COT(124.1332)  
```  
  
 <span data-ttu-id="27f42-680">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-680">Here is hello result set.</span></span>  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <span data-ttu-id="27f42-681"><a name="bk_degrees"></a> DEGREES</span><span class="sxs-lookup"><span data-stu-id="27f42-681"><a name="bk_degrees"></a> DEGREES</span></span>  
 <span data-ttu-id="27f42-682">Retorna Olá ângulo correspondente em graus para um ângulo especificado em radianos.</span><span class="sxs-lookup"><span data-stu-id="27f42-682">Returns hello corresponding angle in degrees for an angle specified in radians.</span></span>  
  
 <span data-ttu-id="27f42-683">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-683">**Syntax**</span></span>  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 <span data-ttu-id="27f42-684">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-684">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="27f42-685">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-685">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-686">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-686">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-687">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-687">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-688">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-688">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-689">Olá exemplo a seguir retorna Olá número de graus em um ângulo de PI/2 radianos.</span><span class="sxs-lookup"><span data-stu-id="27f42-689">hello following example returns hello number of degrees in an angle of PI/2 radians.</span></span>  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 <span data-ttu-id="27f42-690">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-690">Here is hello result set.</span></span>  
  
```  
[{"$1": 90}]  
```  
  
####  <span data-ttu-id="27f42-691"><a name="bk_floor"></a> FLOOR</span><span class="sxs-lookup"><span data-stu-id="27f42-691"><a name="bk_floor"></a> FLOOR</span></span>  
 <span data-ttu-id="27f42-692">Retorna Olá maior inteiro menor ou igual a toohello especificado expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-692">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-693">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-693">**Syntax**</span></span>  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 <span data-ttu-id="27f42-694">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-694">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="27f42-695">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-695">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-696">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-696">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-697">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-697">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-698">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-698">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-699">saudação de exemplo a seguir mostra numéricos positivos, negativos e valores zero com hello função FLOOR.</span><span class="sxs-lookup"><span data-stu-id="27f42-699">hello following example shows positive numeric, negative, and zero values with hello FLOOR function.</span></span>  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 <span data-ttu-id="27f42-700">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-700">Here is hello result set.</span></span>  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <span data-ttu-id="27f42-701"><a name="bk_exp"></a> EXP</span><span class="sxs-lookup"><span data-stu-id="27f42-701"><a name="bk_exp"></a> EXP</span></span>  
 <span data-ttu-id="27f42-702">Retorna um valor Olá exponencial de saudação especificado expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-702">Returns hello exponential value of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-703">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-703">**Syntax**</span></span>  
  
```  
EXP (<numeric_expression>)  
```  
  
 <span data-ttu-id="27f42-704">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-704">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="27f42-705">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-705">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-706">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-706">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-707">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-707">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-708">**Comentários**</span><span class="sxs-lookup"><span data-stu-id="27f42-708">**Remarks**</span></span>  
  
 <span data-ttu-id="27f42-709">constante Olá **e** (2,718281...), é Olá base dos logaritmos naturais.</span><span class="sxs-lookup"><span data-stu-id="27f42-709">hello constant **e** (2.718281…), is hello base of natural logarithms.</span></span>  
  
 <span data-ttu-id="27f42-710">Olá, expoente de um número é constante Olá **e** gerado toohello potência do número de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-710">hello exponent of a number is hello constant **e** raised toohello power of hello number.</span></span> <span data-ttu-id="27f42-711">Por exemplo, EXP(1.0) = e^1.0 = 2.71828182845905 e EXP(10) = e^10 = 22026.4657948067.</span><span class="sxs-lookup"><span data-stu-id="27f42-711">For example EXP(1.0) = e^1.0 = 2.71828182845905 and EXP(10) = e^10 = 22026.4657948067.</span></span>  
  
 <span data-ttu-id="27f42-712">Olá exponencial do logaritmo natural de saudação de um número é o número de saudação em si: EXP (LOG (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="27f42-712">hello exponential of hello natural logarithm of a number is hello number itself: EXP (LOG (n)) = n.</span></span> <span data-ttu-id="27f42-713">E o logaritmo natural de saudação do hello exponencial de um número é o número de saudação em si: LOG (EXP (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="27f42-713">And hello natural logarithm of hello exponential of a number is hello number itself: LOG (EXP (n)) = n.</span></span>  
  
 <span data-ttu-id="27f42-714">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-714">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-715">Olá exemplo a seguir declara uma variável e retorna o valor exponencial de saudação da variável especificada da saudação (10).</span><span class="sxs-lookup"><span data-stu-id="27f42-715">hello following example declares a variable and returns hello exponential value of hello specified variable (10).</span></span>  
  
```  
SELECT EXP(10)  
```  
  
 <span data-ttu-id="27f42-716">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-716">Here is hello result set.</span></span>  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 <span data-ttu-id="27f42-717">Olá exemplo a seguir retorna valor exponencial Olá Olá o logaritmo natural de 20 e o logaritmo natural de saudação do hello exponencial de 20.</span><span class="sxs-lookup"><span data-stu-id="27f42-717">hello following example returns hello exponential value of hello natural logarithm of 20 and hello natural logarithm of hello exponential of 20.</span></span> <span data-ttu-id="27f42-718">Como essas funções são funções inversas uma da outra, o valor de retorno Olá com o arredondamento para matemática em ambos os casos é 20 de ponto flutuante.</span><span class="sxs-lookup"><span data-stu-id="27f42-718">Because these functions are inverse functions of one another, hello return value with rounding for floating point math in both cases is 20.</span></span>  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 <span data-ttu-id="27f42-719">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-719">Here is hello result set.</span></span>  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <span data-ttu-id="27f42-720"><a name="bk_log"></a> LOG</span><span class="sxs-lookup"><span data-stu-id="27f42-720"><a name="bk_log"></a> LOG</span></span>  
 <span data-ttu-id="27f42-721">Retorna Olá o logaritmo natural de saudação especificada uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-721">Returns hello natural logarithm of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-722">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-722">**Syntax**</span></span>  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 <span data-ttu-id="27f42-723">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-723">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="27f42-724">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-724">Is a numeric expression.</span></span>  
  
-   `base`  
  
     <span data-ttu-id="27f42-725">Argumento numérico opcional que define Olá base do logaritmo hello.</span><span class="sxs-lookup"><span data-stu-id="27f42-725">Optional numeric argument that sets hello base for hello logarithm.</span></span>  
  
 <span data-ttu-id="27f42-726">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-726">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-727">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-727">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-728">**Comentários**</span><span class="sxs-lookup"><span data-stu-id="27f42-728">**Remarks**</span></span>  
  
 <span data-ttu-id="27f42-729">Por padrão, o log () retorna o logaritmo natural hello.</span><span class="sxs-lookup"><span data-stu-id="27f42-729">By default, LOG() returns hello natural logarithm.</span></span> <span data-ttu-id="27f42-730">Você pode alterar a base de saudação do valor de tooanother logaritmo Olá usando o parâmetro opcional de base hello.</span><span class="sxs-lookup"><span data-stu-id="27f42-730">You can change hello base of hello logarithm tooanother value by using hello optional base parameter.</span></span>  
  
 <span data-ttu-id="27f42-731">logaritmo natural de saudação é Olá logaritmo toohello base **e**, onde **e** é uma constante too2.718281828 aproximadamente igual a irracional.</span><span class="sxs-lookup"><span data-stu-id="27f42-731">hello natural logarithm is hello logarithm toohello base **e**, where **e** is an irrational constant approximately equal too2.718281828.</span></span>  
  
 <span data-ttu-id="27f42-732">logaritmo natural de saudação do hello exponencial de um número é o número de saudação em si: LOG (EXP (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="27f42-732">hello natural logarithm of hello exponential of a number is hello number itself: LOG( EXP( n ) ) = n.</span></span> <span data-ttu-id="27f42-733">E Olá exponencial do logaritmo natural de saudação de um número é o número de saudação em si: EXP (LOG (n)) = n.</span><span class="sxs-lookup"><span data-stu-id="27f42-733">And hello exponential of hello natural logarithm of a number is hello number itself: EXP( LOG( n ) ) = n.</span></span>  
  
 <span data-ttu-id="27f42-734">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-734">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-735">Olá exemplo a seguir declara uma variável e retorna o valor de logaritmo de saudação da variável especificada da saudação (10).</span><span class="sxs-lookup"><span data-stu-id="27f42-735">hello following example declares a variable and returns hello logarithm value of hello specified variable (10).</span></span>  
  
```  
SELECT LOG(10)  
```  
  
 <span data-ttu-id="27f42-736">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-736">Here is hello result set.</span></span>  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 <span data-ttu-id="27f42-737">Olá, exemplo a seguir calcula hello LOG para o expoente de saudação de um número.</span><span class="sxs-lookup"><span data-stu-id="27f42-737">hello following example calculates hello LOG for hello exponent of a number.</span></span>  
  
```  
SELECT EXP(LOG(10))  
```  
  
 <span data-ttu-id="27f42-738">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-738">Here is hello result set.</span></span>  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <span data-ttu-id="27f42-739"><a name="bk_log10"></a> LOG10</span><span class="sxs-lookup"><span data-stu-id="27f42-739"><a name="bk_log10"></a> LOG10</span></span>  
 <span data-ttu-id="27f42-740">Logaritmo de base 10 de saudação retorna da saudação especificado expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-740">Returns hello base-10 logarithm of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-741">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-741">**Syntax**</span></span>  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 <span data-ttu-id="27f42-742">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-742">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="27f42-743">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-743">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-744">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-744">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-745">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-745">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-746">**Comentários**</span><span class="sxs-lookup"><span data-stu-id="27f42-746">**Remarks**</span></span>  
  
 <span data-ttu-id="27f42-747">Olá LOG10 e funções de POWER estão inversamente relacionada tooone outro.</span><span class="sxs-lookup"><span data-stu-id="27f42-747">hello LOG10 and POWER functions are inversely related tooone another.</span></span> <span data-ttu-id="27f42-748">Por exemplo, 10 ^ LOG10(n) = n.</span><span class="sxs-lookup"><span data-stu-id="27f42-748">For example, 10 ^ LOG10(n) = n.</span></span>  
  
 <span data-ttu-id="27f42-749">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-749">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-750">Olá exemplo a seguir declara uma variável e retorna Olá LOG10 valor da variável especificada da saudação (100).</span><span class="sxs-lookup"><span data-stu-id="27f42-750">hello following example declares a variable and returns hello LOG10 value of hello specified variable (100).</span></span>  
  
```  
SELECT LOG10(100)  
```  
  
 <span data-ttu-id="27f42-751">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-751">Here is hello result set.</span></span>  
  
```  
[{$1: 2}]  
```  
  
####  <span data-ttu-id="27f42-752"><a name="bk_pi"></a> PI</span><span class="sxs-lookup"><span data-stu-id="27f42-752"><a name="bk_pi"></a> PI</span></span>  
 <span data-ttu-id="27f42-753">Retorna Olá valor constante de PI.</span><span class="sxs-lookup"><span data-stu-id="27f42-753">Returns hello constant value of PI.</span></span>  
  
 <span data-ttu-id="27f42-754">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-754">**Syntax**</span></span>  
  
```  
PI ()  
```  
  
 <span data-ttu-id="27f42-755">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-755">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="27f42-756">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-756">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-757">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-757">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-758">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-758">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-759">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-759">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-760">Olá, exemplo a seguir retorna Olá valor de PI.</span><span class="sxs-lookup"><span data-stu-id="27f42-760">hello following example returns hello value of PI.</span></span>  
  
```  
SELECT PI()  
```  
  
 <span data-ttu-id="27f42-761">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-761">Here is hello result set.</span></span>  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <span data-ttu-id="27f42-762"><a name="bk_power"></a> POWER</span><span class="sxs-lookup"><span data-stu-id="27f42-762"><a name="bk_power"></a> POWER</span></span>  
 <span data-ttu-id="27f42-763">Retorna Olá Olá especificado valor toohello da expressão especificada de energia.</span><span class="sxs-lookup"><span data-stu-id="27f42-763">Returns hello value of hello specified expression toohello specified power.</span></span>  
  
 <span data-ttu-id="27f42-764">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-764">**Syntax**</span></span>  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 <span data-ttu-id="27f42-765">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-765">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="27f42-766">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-766">Is a numeric expression.</span></span>  
  
-   `y`  
  
     <span data-ttu-id="27f42-767">É Olá power toowhich tooraise `numeric_expression`.</span><span class="sxs-lookup"><span data-stu-id="27f42-767">Is hello power toowhich tooraise `numeric_expression`.</span></span>  
  
 <span data-ttu-id="27f42-768">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-768">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-769">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-769">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-770">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-770">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-771">saudação de exemplo a seguir demonstra como elevar uma potência de toohello número de 3 (Olá cubo do número de saudação).</span><span class="sxs-lookup"><span data-stu-id="27f42-771">hello following example demonstrates raising a number toohello power of 3 (hello cube of hello number).</span></span>  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 <span data-ttu-id="27f42-772">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-772">Here is hello result set.</span></span>  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <span data-ttu-id="27f42-773"><a name="bk_radians"></a> RADIANS</span><span class="sxs-lookup"><span data-stu-id="27f42-773"><a name="bk_radians"></a> RADIANS</span></span>  
 <span data-ttu-id="27f42-774">Retorna radianos quando uma expressão numérica é inserida em graus.</span><span class="sxs-lookup"><span data-stu-id="27f42-774">Returns radians when a numeric expression, in degrees, is entered.</span></span>  
  
 <span data-ttu-id="27f42-775">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-775">**Syntax**</span></span>  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 <span data-ttu-id="27f42-776">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-776">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="27f42-777">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-777">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-778">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-778">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-779">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-779">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-780">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-780">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-781">Olá exemplo a seguir usa alguns ângulos como entrada e retorna seus valores radianos correspondentes.</span><span class="sxs-lookup"><span data-stu-id="27f42-781">hello following example takes a few angles as input and returns their corresponding radian values.</span></span>  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 <span data-ttu-id="27f42-782">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-782">Here is hello result set.</span></span>  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <span data-ttu-id="27f42-783"><a name="bk_round"></a> ROUND</span><span class="sxs-lookup"><span data-stu-id="27f42-783"><a name="bk_round"></a> ROUND</span></span>  
 <span data-ttu-id="27f42-784">Retorna um valor numérico, arredondado toohello valor de inteiro mais próximo.</span><span class="sxs-lookup"><span data-stu-id="27f42-784">Returns a numeric value, rounded toohello closest integer value.</span></span>  
  
 <span data-ttu-id="27f42-785">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-785">**Syntax**</span></span>  
  
```  
ROUND(<numeric_expression>)  
```  
  
 <span data-ttu-id="27f42-786">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-786">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="27f42-787">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-787">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-788">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-788">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-789">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-789">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-790">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-790">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-791">Olá, exemplo a seguir Arredonda Olá seguintes números positivos e negativos toohello inteiro mais próximo.</span><span class="sxs-lookup"><span data-stu-id="27f42-791">hello following example rounds hello following positive and negative numbers toohello nearest integer.</span></span>  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 <span data-ttu-id="27f42-792">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-792">Here is hello result set.</span></span>  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <span data-ttu-id="27f42-793"><a name="bk_sign"></a> SIGN</span><span class="sxs-lookup"><span data-stu-id="27f42-793"><a name="bk_sign"></a> SIGN</span></span>  
 <span data-ttu-id="27f42-794">Retorna Olá positivo (+ 1), zero (0), ou sinal de negativo (-1) de saudação especificado expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-794">Returns hello positive (+1), zero (0), or negative (-1) sign of hello specified numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-795">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-795">**Syntax**</span></span>  
  
```  
SIGN(<numeric_expression>)  
```  
  
 <span data-ttu-id="27f42-796">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-796">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="27f42-797">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-797">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-798">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-798">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-799">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-799">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-800">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-800">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-801">Olá exemplo a seguir retorna valores de entrada hello de números de too2-2.</span><span class="sxs-lookup"><span data-stu-id="27f42-801">hello following example returns hello SIGN values of numbers from -2 too2.</span></span>  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 <span data-ttu-id="27f42-802">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-802">Here is hello result set.</span></span>  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <span data-ttu-id="27f42-803"><a name="bk_sin"></a> SIN</span><span class="sxs-lookup"><span data-stu-id="27f42-803"><a name="bk_sin"></a> SIN</span></span>  
 <span data-ttu-id="27f42-804">Retorna Olá seno trigonométrico Olá especificado o ângulo em radianos, na Olá expressão especificada.</span><span class="sxs-lookup"><span data-stu-id="27f42-804">Returns hello trigonometric sine of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="27f42-805">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-805">**Syntax**</span></span>  
  
```  
SIN(<numeric_expression>)  
```  
  
 <span data-ttu-id="27f42-806">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-806">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="27f42-807">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-807">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-808">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-808">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-809">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-809">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-810">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-810">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-811">saudação de exemplo a seguir calcula Olá sen do ângulo especificado hello.</span><span class="sxs-lookup"><span data-stu-id="27f42-811">hello following example calculates hello SIN of hello specified angle.</span></span>  
  
```  
SELECT SIN(45.175643)  
```  
  
 <span data-ttu-id="27f42-812">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-812">Here is hello result set.</span></span>  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <span data-ttu-id="27f42-813"><a name="bk_sqrt"></a> SQRT</span><span class="sxs-lookup"><span data-stu-id="27f42-813"><a name="bk_sqrt"></a> SQRT</span></span>  
 <span data-ttu-id="27f42-814">Retorna Olá quadrado raiz de saudação especificado valor numérico.</span><span class="sxs-lookup"><span data-stu-id="27f42-814">Returns hello square root of hello specified numeric value.</span></span>  
  
 <span data-ttu-id="27f42-815">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-815">**Syntax**</span></span>  
  
```  
SQRT(<numeric_expression>)  
```  
  
 <span data-ttu-id="27f42-816">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-816">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="27f42-817">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-817">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-818">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-818">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-819">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-819">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-820">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-820">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-821">Olá, exemplo a seguir retorna raízes quadradas de saudação de números de 1 a 3.</span><span class="sxs-lookup"><span data-stu-id="27f42-821">hello following example returns hello square roots of numbers 1-3.</span></span>  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 <span data-ttu-id="27f42-822">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-822">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <span data-ttu-id="27f42-823"><a name="bk_square"></a> SQUARE</span><span class="sxs-lookup"><span data-stu-id="27f42-823"><a name="bk_square"></a> SQUARE</span></span>  
 <span data-ttu-id="27f42-824">Saudação de retorna quadrada de saudação especificado valor numérico.</span><span class="sxs-lookup"><span data-stu-id="27f42-824">Returns hello square of hello specified numeric value.</span></span>  
  
 <span data-ttu-id="27f42-825">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-825">**Syntax**</span></span>  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 <span data-ttu-id="27f42-826">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-826">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="27f42-827">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-827">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-828">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-828">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-829">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-829">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-830">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-830">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-831">Olá, exemplo a seguir retorna quadrados Olá dos números de 1 a 3.</span><span class="sxs-lookup"><span data-stu-id="27f42-831">hello following example returns hello squares of numbers 1-3.</span></span>  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 <span data-ttu-id="27f42-832">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-832">Here is hello result set.</span></span>  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <span data-ttu-id="27f42-833"><a name="bk_tan"></a> TAN</span><span class="sxs-lookup"><span data-stu-id="27f42-833"><a name="bk_tan"></a> TAN</span></span>  
 <span data-ttu-id="27f42-834">Tangente de saudação retorna da saudação especificado o ângulo em radianos, na Olá expressão especificada.</span><span class="sxs-lookup"><span data-stu-id="27f42-834">Returns hello tangent of hello specified angle, in radians, in hello specified expression.</span></span>  
  
 <span data-ttu-id="27f42-835">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-835">**Syntax**</span></span>  
  
```  
TAN (<numeric_expression>)  
```  
  
 <span data-ttu-id="27f42-836">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-836">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="27f42-837">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-837">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-838">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-838">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-839">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-839">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-840">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-840">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-841">Olá, exemplo a seguir calcula a tangente Olá de PI () / 2.</span><span class="sxs-lookup"><span data-stu-id="27f42-841">hello following example calculates hello tangent of PI()/2.</span></span>  
  
```  
SELECT TAN(PI()/2);  
```  
  
 <span data-ttu-id="27f42-842">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-842">Here is hello result set.</span></span>  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <span data-ttu-id="27f42-843"><a name="bk_trunc"></a>TRUNC</span><span class="sxs-lookup"><span data-stu-id="27f42-843"><a name="bk_trunc"></a> TRUNC</span></span>  
 <span data-ttu-id="27f42-844">Retorna um valor numérico, o valor inteiro mais próximo de toohello truncados.</span><span class="sxs-lookup"><span data-stu-id="27f42-844">Returns a numeric value, truncated toohello closest integer value.</span></span>  
  
 <span data-ttu-id="27f42-845">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-845">**Syntax**</span></span>  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 <span data-ttu-id="27f42-846">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-846">**Arguments**</span></span>  
  
-   `numeric_expression`  
  
     <span data-ttu-id="27f42-847">É uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-847">Is a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-848">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-848">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-849">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-849">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-850">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-850">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-851">saudação de exemplo a seguir trunca Olá seguintes números positivos e negativos toohello valor inteiro mais próximo.</span><span class="sxs-lookup"><span data-stu-id="27f42-851">hello following example truncates hello following positive and negative numbers toohello nearest integer value.</span></span>  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 <span data-ttu-id="27f42-852">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-852">Here is hello result set.</span></span>  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <span data-ttu-id="27f42-853"><a name="bk_type_checking_functions"></a> Funções de verificação de tipo</span><span class="sxs-lookup"><span data-stu-id="27f42-853"><a name="bk_type_checking_functions"></a> Type checking functions</span></span>  
 <span data-ttu-id="27f42-854">Olá funções a seguir oferece suporte ao tipo verificando em relação aos valores de entrada e retornam um valor booleano.</span><span class="sxs-lookup"><span data-stu-id="27f42-854">hello following functions support type checking against input values, and each return a Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="27f42-855">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="27f42-855">IS_ARRAY</span></span>](#bk_is_array)|[<span data-ttu-id="27f42-856">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="27f42-856">IS_BOOL</span></span>](#bk_is_bool)|[<span data-ttu-id="27f42-857">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="27f42-857">IS_DEFINED</span></span>](#bk_is_defined)|  
|[<span data-ttu-id="27f42-858">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="27f42-858">IS_NULL</span></span>](#bk_is_null)|[<span data-ttu-id="27f42-859">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="27f42-859">IS_NUMBER</span></span>](#bk_is_number)|[<span data-ttu-id="27f42-860">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="27f42-860">IS_OBJECT</span></span>](#bk_is_object)|  
|[<span data-ttu-id="27f42-861">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="27f42-861">IS_PRIMITIVE</span></span>](#bk_is_primitive)|[<span data-ttu-id="27f42-862">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="27f42-862">IS_STRING</span></span>](#bk_is_string)||  
  
####  <span data-ttu-id="27f42-863"><a name="bk_is_array"></a>IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="27f42-863"><a name="bk_is_array"></a> IS_ARRAY</span></span>  
 <span data-ttu-id="27f42-864">Retorna um valor booliano que indica se o tipo de saudação de saudação especificado expressão é uma matriz.</span><span class="sxs-lookup"><span data-stu-id="27f42-864">Returns a Boolean value indicating if hello type of hello specified expression is an array.</span></span>  
  
 <span data-ttu-id="27f42-865">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-865">**Syntax**</span></span>  
  
```  
IS_ARRAY(<expression>)  
```  
  
 <span data-ttu-id="27f42-866">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-866">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="27f42-867">É qualquer expressão válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-867">Is any valid expression.</span></span>  
  
 <span data-ttu-id="27f42-868">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-868">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-869">Retorna uma expressão booliana.</span><span class="sxs-lookup"><span data-stu-id="27f42-869">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="27f42-870">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-870">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-871">Olá exemplo a seguir verifica objetos JSON booliano, número, cadeia de caracteres, nula, objeto, matriz e tipos indefinidos usando Olá função IS_ARRAY.</span><span class="sxs-lookup"><span data-stu-id="27f42-871">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_ARRAY function.</span></span>  
  
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
  
 <span data-ttu-id="27f42-872">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-872">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <span data-ttu-id="27f42-873"><a name="bk_is_bool"></a>IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="27f42-873"><a name="bk_is_bool"></a> IS_BOOL</span></span>  
 <span data-ttu-id="27f42-874">Retorna um valor booliano que indica se o tipo de saudação de saudação especificado expressão é um valor booleano.</span><span class="sxs-lookup"><span data-stu-id="27f42-874">Returns a Boolean value indicating if hello type of hello specified expression is a Boolean.</span></span>  
  
 <span data-ttu-id="27f42-875">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-875">**Syntax**</span></span>  
  
```  
IS_BOOL(<expression>)  
```  
  
 <span data-ttu-id="27f42-876">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-876">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="27f42-877">É qualquer expressão válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-877">Is any valid expression.</span></span>  
  
 <span data-ttu-id="27f42-878">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-878">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-879">Retorna uma expressão booliana.</span><span class="sxs-lookup"><span data-stu-id="27f42-879">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="27f42-880">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-880">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-881">Olá exemplo a seguir verifica objetos JSON booliano, número, cadeia de caracteres, nula, objeto, matriz e tipos indefinidos usando Olá função IS_BOOL.</span><span class="sxs-lookup"><span data-stu-id="27f42-881">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_BOOL function.</span></span>  
  
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
  
 <span data-ttu-id="27f42-882">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-882">Here is hello result set.</span></span>  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="27f42-883"><a name="bk_is_defined"></a>IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="27f42-883"><a name="bk_is_defined"></a> IS_DEFINED</span></span>  
 <span data-ttu-id="27f42-884">Retorna um valor booleano que indica se a propriedade de saudação foi atribuída um valor.</span><span class="sxs-lookup"><span data-stu-id="27f42-884">Returns a Boolean indicating if hello property has been assigned a value.</span></span>  
  
 <span data-ttu-id="27f42-885">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-885">**Syntax**</span></span>  
  
```  
IS_DEFINED(<expression>)  
```  
  
 <span data-ttu-id="27f42-886">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-886">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="27f42-887">É qualquer expressão válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-887">Is any valid expression.</span></span>  
  
 <span data-ttu-id="27f42-888">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-888">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-889">Retorna uma expressão booliana.</span><span class="sxs-lookup"><span data-stu-id="27f42-889">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="27f42-890">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-890">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-891">Olá seguindo o exemplo verifica a presença de saudação de uma propriedade dentro de saudação especificado documento JSON.</span><span class="sxs-lookup"><span data-stu-id="27f42-891">hello following example checks for hello presence of a property within hello specified JSON document.</span></span> <span data-ttu-id="27f42-892">Olá primeiro retorna true, porque "a" está presente, mas Olá segundo retorna false, porque "b" está ausente.</span><span class="sxs-lookup"><span data-stu-id="27f42-892">hello first returns true since "a" is present, but hello second returns false since "b" is absent.</span></span>  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 <span data-ttu-id="27f42-893">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-893">Here is hello result set.</span></span>  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <span data-ttu-id="27f42-894"><a name="bk_is_null"></a>IS_NULL</span><span class="sxs-lookup"><span data-stu-id="27f42-894"><a name="bk_is_null"></a> IS_NULL</span></span>  
 <span data-ttu-id="27f42-895">Retorna um valor booliano que indica se o tipo de saudação de saudação especificado expressão é nulo.</span><span class="sxs-lookup"><span data-stu-id="27f42-895">Returns a Boolean value indicating if hello type of hello specified expression is null.</span></span>  
  
 <span data-ttu-id="27f42-896">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-896">**Syntax**</span></span>  
  
```  
IS_NULL(<expression>)  
```  
  
 <span data-ttu-id="27f42-897">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-897">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="27f42-898">É qualquer expressão válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-898">Is any valid expression.</span></span>  
  
 <span data-ttu-id="27f42-899">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-899">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-900">Retorna uma expressão booliana.</span><span class="sxs-lookup"><span data-stu-id="27f42-900">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="27f42-901">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-901">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-902">Olá exemplo a seguir verifica objetos JSON booliano, número, cadeia de caracteres, nula, objeto, matriz e tipos indefinidos usando Olá função IS_NULL.</span><span class="sxs-lookup"><span data-stu-id="27f42-902">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_NULL function.</span></span>  
  
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
  
 <span data-ttu-id="27f42-903">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-903">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="27f42-904"><a name="bk_is_number"></a>IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="27f42-904"><a name="bk_is_number"></a> IS_NUMBER</span></span>  
 <span data-ttu-id="27f42-905">Retorna um valor booliano que indica se o tipo de saudação de saudação especificado expressão é um número.</span><span class="sxs-lookup"><span data-stu-id="27f42-905">Returns a Boolean value indicating if hello type of hello specified expression is a number.</span></span>  
  
 <span data-ttu-id="27f42-906">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-906">**Syntax**</span></span>  
  
```  
IS_NUMBER(<expression>)  
```  
  
 <span data-ttu-id="27f42-907">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-907">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="27f42-908">É qualquer expressão válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-908">Is any valid expression.</span></span>  
  
 <span data-ttu-id="27f42-909">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-909">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-910">Retorna uma expressão booliana.</span><span class="sxs-lookup"><span data-stu-id="27f42-910">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="27f42-911">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-911">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-912">Olá exemplo a seguir verifica objetos JSON booliano, número, cadeia de caracteres, nula, objeto, matriz e tipos indefinidos usando Olá função IS_NULL.</span><span class="sxs-lookup"><span data-stu-id="27f42-912">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_NULL function.</span></span>  
  
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
  
 <span data-ttu-id="27f42-913">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-913">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <span data-ttu-id="27f42-914"><a name="bk_is_object"></a>IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="27f42-914"><a name="bk_is_object"></a> IS_OBJECT</span></span>  
 <span data-ttu-id="27f42-915">Retorna um valor booliano que indica se o tipo de saudação de saudação especificado expressão é um objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="27f42-915">Returns a Boolean value indicating if hello type of hello specified expression is a JSON object.</span></span>  
  
 <span data-ttu-id="27f42-916">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-916">**Syntax**</span></span>  
  
```  
IS_OBJECT(<expression>)  
```  
  
 <span data-ttu-id="27f42-917">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-917">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="27f42-918">É qualquer expressão válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-918">Is any valid expression.</span></span>  
  
 <span data-ttu-id="27f42-919">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-919">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-920">Retorna uma expressão booliana.</span><span class="sxs-lookup"><span data-stu-id="27f42-920">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="27f42-921">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-921">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-922">Olá exemplo a seguir verifica objetos JSON booliano, número, cadeia de caracteres, nula, objeto, matriz e tipos indefinidos usando Olá função IS_OBJECT.</span><span class="sxs-lookup"><span data-stu-id="27f42-922">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_OBJECT function.</span></span>  
  
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
  
 <span data-ttu-id="27f42-923">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-923">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <span data-ttu-id="27f42-924"><a name="bk_is_primitive"></a>IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="27f42-924"><a name="bk_is_primitive"></a> IS_PRIMITIVE</span></span>  
 <span data-ttu-id="27f42-925">Retorna um valor booliano que indica se o tipo de saudação do hello especificado de expressão é um primitivo (cadeia de caracteres, booleano, numérico ou nulo).</span><span class="sxs-lookup"><span data-stu-id="27f42-925">Returns a Boolean value indicating if hello type of hello specified expression is a primitive (string, Boolean, numeric or null).</span></span>  
  
 <span data-ttu-id="27f42-926">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-926">**Syntax**</span></span>  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 <span data-ttu-id="27f42-927">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-927">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="27f42-928">É qualquer expressão válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-928">Is any valid expression.</span></span>  
  
 <span data-ttu-id="27f42-929">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-929">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-930">Retorna uma expressão booliana.</span><span class="sxs-lookup"><span data-stu-id="27f42-930">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="27f42-931">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-931">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-932">Olá exemplo a seguir verifica objetos JSON booliano, número, cadeia de caracteres, nula, objeto, matriz e tipos indefinidos usando Olá função IS_PRIMITIVE.</span><span class="sxs-lookup"><span data-stu-id="27f42-932">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_PRIMITIVE function.</span></span>  
  
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
  
 <span data-ttu-id="27f42-933">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-933">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <span data-ttu-id="27f42-934"><a name="bk_is_string"></a> IS_STRING</span><span class="sxs-lookup"><span data-stu-id="27f42-934"><a name="bk_is_string"></a> IS_STRING</span></span>  
 <span data-ttu-id="27f42-935">Retorna um valor booliano que indica se o tipo de saudação de saudação especificado expressão é uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="27f42-935">Returns a Boolean value indicating if hello type of hello specified expression is a string.</span></span>  
  
 <span data-ttu-id="27f42-936">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-936">**Syntax**</span></span>  
  
```  
IS_STRING(<expression>)  
```  
  
 <span data-ttu-id="27f42-937">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-937">**Arguments**</span></span>  
  
-   `expression`  
  
     <span data-ttu-id="27f42-938">É qualquer expressão válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-938">Is any valid expression.</span></span>  
  
 <span data-ttu-id="27f42-939">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-939">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-940">Retorna uma expressão booliana.</span><span class="sxs-lookup"><span data-stu-id="27f42-940">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="27f42-941">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-941">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-942">Olá exemplo a seguir verifica objetos JSON booliano, número, cadeia de caracteres, nula, objeto, matriz e tipos indefinidos usando Olá função IS_STRING.</span><span class="sxs-lookup"><span data-stu-id="27f42-942">hello following example checks objects of JSON Boolean, number, string, null, object, array and undefined types using hello IS_STRING function.</span></span>  
  
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
  
 <span data-ttu-id="27f42-943">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-943">Here is hello result set.</span></span>  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <span data-ttu-id="27f42-944"><a name="bk_string_functions"></a> Funções de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="27f42-944"><a name="bk_string_functions"></a> String functions</span></span>  
 <span data-ttu-id="27f42-945">Olá funções escalares a seguir executam uma operação em um valor de cadeia de caracteres de entrada e retornam uma cadeia de caracteres, o valor numérico ou booleano.</span><span class="sxs-lookup"><span data-stu-id="27f42-945">hello following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="27f42-946">CONCAT</span><span class="sxs-lookup"><span data-stu-id="27f42-946">CONCAT</span></span>](#bk_concat)|[<span data-ttu-id="27f42-947">CONTAINS</span><span class="sxs-lookup"><span data-stu-id="27f42-947">CONTAINS</span></span>](#bk_contains)|[<span data-ttu-id="27f42-948">ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="27f42-948">ENDSWITH</span></span>](#bk_endswith)|  
|[<span data-ttu-id="27f42-949">INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="27f42-949">INDEX_OF</span></span>](#bk_index_of)|[<span data-ttu-id="27f42-950">LEFT</span><span class="sxs-lookup"><span data-stu-id="27f42-950">LEFT</span></span>](#bk_left)|[<span data-ttu-id="27f42-951">COMPRIMENTO</span><span class="sxs-lookup"><span data-stu-id="27f42-951">LENGTH</span></span>](#bk_length)|  
|[<span data-ttu-id="27f42-952">LOWER</span><span class="sxs-lookup"><span data-stu-id="27f42-952">LOWER</span></span>](#bk_lower)|[<span data-ttu-id="27f42-953">LTRIM</span><span class="sxs-lookup"><span data-stu-id="27f42-953">LTRIM</span></span>](#bk_ltrim)|[<span data-ttu-id="27f42-954">REPLACE</span><span class="sxs-lookup"><span data-stu-id="27f42-954">REPLACE</span></span>](#bk_replace)|  
|[<span data-ttu-id="27f42-955">REPLICATE</span><span class="sxs-lookup"><span data-stu-id="27f42-955">REPLICATE</span></span>](#bk_replicate)|[<span data-ttu-id="27f42-956">REVERSE</span><span class="sxs-lookup"><span data-stu-id="27f42-956">REVERSE</span></span>](#bk_reverse)|[<span data-ttu-id="27f42-957">RIGHT</span><span class="sxs-lookup"><span data-stu-id="27f42-957">RIGHT</span></span>](#bk_right)|  
|[<span data-ttu-id="27f42-958">RTRIM</span><span class="sxs-lookup"><span data-stu-id="27f42-958">RTRIM</span></span>](#bk_rtrim)|[<span data-ttu-id="27f42-959">STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="27f42-959">STARTSWITH</span></span>](#bk_startswith)|[<span data-ttu-id="27f42-960">SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="27f42-960">SUBSTRING</span></span>](#bk_substring)|  
|[<span data-ttu-id="27f42-961">UPPER</span><span class="sxs-lookup"><span data-stu-id="27f42-961">UPPER</span></span>](#bk_upper)|||  
  
####  <span data-ttu-id="27f42-962"><a name="bk_concat"></a> CONCAT</span><span class="sxs-lookup"><span data-stu-id="27f42-962"><a name="bk_concat"></a> CONCAT</span></span>  
 <span data-ttu-id="27f42-963">Retorna uma cadeia de caracteres que é o resultado de saudação da concatenação de dois ou mais valores de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="27f42-963">Returns a string that is hello result of concatenating two or more string values.</span></span>  
  
 <span data-ttu-id="27f42-964">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-964">**Syntax**</span></span>  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 <span data-ttu-id="27f42-965">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-965">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="27f42-966">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-966">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="27f42-967">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-967">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-968">Retorna uma expressão de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="27f42-968">Returns a string expression.</span></span>  
  
 <span data-ttu-id="27f42-969">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-969">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-970">Olá Olá concatenado exemplo retorna cadeia de caracteres de saudação a seguir valores especificados.</span><span class="sxs-lookup"><span data-stu-id="27f42-970">hello following example returns hello concatenated string of hello specified values.</span></span>  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 <span data-ttu-id="27f42-971">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-971">Here is hello result set.</span></span>  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <span data-ttu-id="27f42-972"><a name="bk_contains"></a> CONTAINS</span><span class="sxs-lookup"><span data-stu-id="27f42-972"><a name="bk_contains"></a> CONTAINS</span></span>  
 <span data-ttu-id="27f42-973">Retorna um valor booleano que indica se a primeira expressão de cadeia de caracteres hello contém Olá segundo.</span><span class="sxs-lookup"><span data-stu-id="27f42-973">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span>  
  
 <span data-ttu-id="27f42-974">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-974">**Syntax**</span></span>  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="27f42-975">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-975">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="27f42-976">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-976">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="27f42-977">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-977">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-978">Retorna uma expressão booliana.</span><span class="sxs-lookup"><span data-stu-id="27f42-978">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="27f42-979">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-979">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-980">Olá exemplo a seguir verifica se "abc" contém "ab" e contém "d".</span><span class="sxs-lookup"><span data-stu-id="27f42-980">hello following example checks if "abc" contains "ab" and contains "d".</span></span>  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 <span data-ttu-id="27f42-981">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-981">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="27f42-982"><a name="bk_endswith"></a> ENDSWITH</span><span class="sxs-lookup"><span data-stu-id="27f42-982"><a name="bk_endswith"></a> ENDSWITH</span></span>  
 <span data-ttu-id="27f42-983">Retorna um valor booleano que indica se primeira expressão de cadeia de caracteres hello termina com hello segundo.</span><span class="sxs-lookup"><span data-stu-id="27f42-983">Returns a Boolean indicating whether hello first string expression ends with hello second.</span></span>  
  
 <span data-ttu-id="27f42-984">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-984">**Syntax**</span></span>  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="27f42-985">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-985">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="27f42-986">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-986">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="27f42-987">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-987">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-988">Retorna uma expressão booliana.</span><span class="sxs-lookup"><span data-stu-id="27f42-988">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="27f42-989">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-989">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-990">Olá, exemplo a seguir retorna hello "abc" termina com "b" e "bc".</span><span class="sxs-lookup"><span data-stu-id="27f42-990">hello following example returns hello "abc" ends with "b" and "bc".</span></span>  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 <span data-ttu-id="27f42-991">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-991">Here is hello result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="27f42-992"><a name="bk_index_of"></a>INDEX_OF</span><span class="sxs-lookup"><span data-stu-id="27f42-992"><a name="bk_index_of"></a> INDEX_OF</span></span>  
 <span data-ttu-id="27f42-993">Retorna a saudação iniciando a posição da primeira ocorrência de saudação da segunda expressão de cadeia de caracteres hello na primeira expressão de cadeia de caracteres especificada hello, ou -1 se a cadeia de caracteres de saudação não foi encontrada.</span><span class="sxs-lookup"><span data-stu-id="27f42-993">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span>  
  
 <span data-ttu-id="27f42-994">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-994">**Syntax**</span></span>  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="27f42-995">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-995">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="27f42-996">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-996">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="27f42-997">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-997">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-998">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-998">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-999">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-999">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-1000">Olá exemplo a seguir retorna o índice de saudação de diversas subcadeias de caracteres dentro de "abc".</span><span class="sxs-lookup"><span data-stu-id="27f42-1000">hello following example returns hello index of various substrings inside "abc".</span></span>  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 <span data-ttu-id="27f42-1001">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-1001">Here is hello result set.</span></span>  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <span data-ttu-id="27f42-1002"><a name="bk_left"></a> ESQUERDA</span><span class="sxs-lookup"><span data-stu-id="27f42-1002"><a name="bk_left"></a> LEFT</span></span>  
 <span data-ttu-id="27f42-1003">Retorna Olá parte esquerda de uma cadeia de caracteres com hello especificado número de caracteres.</span><span class="sxs-lookup"><span data-stu-id="27f42-1003">Returns hello left part of a string with hello specified number of characters.</span></span>  
  
 <span data-ttu-id="27f42-1004">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-1004">**Syntax**</span></span>  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="27f42-1005">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1005">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="27f42-1006">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-1006">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="27f42-1007">É qualquer expressão numérica válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-1007">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-1008">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-1008">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-1009">Retorna uma expressão de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="27f42-1009">Returns a string expression.</span></span>  
  
 <span data-ttu-id="27f42-1010">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1010">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-1011">Olá, exemplo a seguir retorna Olá esquerda a parte de "abc" para vários valores de comprimento.</span><span class="sxs-lookup"><span data-stu-id="27f42-1011">hello following example returns hello left part of "abc" for various length values.</span></span>  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 <span data-ttu-id="27f42-1012">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-1012">Here is hello result set.</span></span>  
  
```  
[{"$1": "ab", "$2": "ab"}]  
```  
  
####  <span data-ttu-id="27f42-1013"><a name="bk_length"></a> COMPRIMENTO</span><span class="sxs-lookup"><span data-stu-id="27f42-1013"><a name="bk_length"></a> LENGTH</span></span>  
 <span data-ttu-id="27f42-1014">Retorna o número de saudação de caracteres da saudação especificado expressão de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="27f42-1014">Returns hello number of characters of hello specified string expression.</span></span>  
  
 <span data-ttu-id="27f42-1015">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-1015">**Syntax**</span></span>  
  
```  
LENGTH(<str_expr>)  
```  
  
 <span data-ttu-id="27f42-1016">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1016">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="27f42-1017">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-1017">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="27f42-1018">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-1018">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-1019">Retorna uma expressão de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="27f42-1019">Returns a string expression.</span></span>  
  
 <span data-ttu-id="27f42-1020">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1020">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-1021">Olá, exemplo a seguir retorna Olá comprimento de uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="27f42-1021">hello following example returns hello length of a string.</span></span>  
  
```  
SELECT LENGTH("abc")  
```  
  
 <span data-ttu-id="27f42-1022">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-1022">Here is hello result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="27f42-1023"><a name="bk_lower"></a> LOWER</span><span class="sxs-lookup"><span data-stu-id="27f42-1023"><a name="bk_lower"></a> LOWER</span></span>  
 <span data-ttu-id="27f42-1024">Retorna uma expressão de cadeia de caracteres após converter caracteres maiusculos toolowercase de dados.</span><span class="sxs-lookup"><span data-stu-id="27f42-1024">Returns a string expression after converting uppercase character data toolowercase.</span></span>  
  
 <span data-ttu-id="27f42-1025">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-1025">**Syntax**</span></span>  
  
```  
LOWER(<str_expr>)  
```  
  
 <span data-ttu-id="27f42-1026">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1026">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="27f42-1027">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-1027">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="27f42-1028">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-1028">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-1029">Retorna uma expressão de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="27f42-1029">Returns a string expression.</span></span>  
  
 <span data-ttu-id="27f42-1030">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1030">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-1031">Olá mostrado no exemplo a seguir como toouse inferior em uma consulta.</span><span class="sxs-lookup"><span data-stu-id="27f42-1031">hello following example shows how toouse LOWER in a query.</span></span>  
  
```  
SELECT LOWER("Abc")  
```  
  
 <span data-ttu-id="27f42-1032">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-1032">Here is hello result set.</span></span>  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <span data-ttu-id="27f42-1033"><a name="bk_ltrim"></a> LTRIM</span><span class="sxs-lookup"><span data-stu-id="27f42-1033"><a name="bk_ltrim"></a> LTRIM</span></span>  
 <span data-ttu-id="27f42-1034">Retorna uma expressão de cadeia de caracteres após remover os espaços em branco iniciais.</span><span class="sxs-lookup"><span data-stu-id="27f42-1034">Returns a string expression after it removes leading blanks.</span></span>  
  
 <span data-ttu-id="27f42-1035">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-1035">**Syntax**</span></span>  
  
```  
LTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="27f42-1036">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1036">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="27f42-1037">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-1037">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="27f42-1038">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-1038">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-1039">Retorna uma expressão de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="27f42-1039">Returns a string expression.</span></span>  
  
 <span data-ttu-id="27f42-1040">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1040">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-1041">Olá mostrado no exemplo a seguir como toouse LTRIM dentro de uma consulta.</span><span class="sxs-lookup"><span data-stu-id="27f42-1041">hello following example shows how toouse LTRIM inside a query.</span></span>  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 <span data-ttu-id="27f42-1042">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-1042">Here is hello result set.</span></span>  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <span data-ttu-id="27f42-1043"><a name="bk_replace"></a> SUBSTITUIR</span><span class="sxs-lookup"><span data-stu-id="27f42-1043"><a name="bk_replace"></a> REPLACE</span></span>  
 <span data-ttu-id="27f42-1044">Substitui todas as ocorrências de um valor de cadeia de caracteres especificado por outro valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="27f42-1044">Replaces all occurrences of a specified string value with another string value.</span></span>  
  
 <span data-ttu-id="27f42-1045">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-1045">**Syntax**</span></span>  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="27f42-1046">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1046">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="27f42-1047">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-1047">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="27f42-1048">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-1048">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-1049">Retorna uma expressão de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="27f42-1049">Returns a string expression.</span></span>  
  
 <span data-ttu-id="27f42-1050">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1050">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-1051">saudação de exemplo a seguir mostra como toouse substituir em uma consulta.</span><span class="sxs-lookup"><span data-stu-id="27f42-1051">hello following example shows how toouse REPLACE in a query.</span></span>  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 <span data-ttu-id="27f42-1052">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-1052">Here is hello result set.</span></span>  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <span data-ttu-id="27f42-1053"><a name="bk_replicate"></a> REPLICATE</span><span class="sxs-lookup"><span data-stu-id="27f42-1053"><a name="bk_replicate"></a> REPLICATE</span></span>  
 <span data-ttu-id="27f42-1054">Repete um valor de cadeia de caracteres por um número de vezes especificado.</span><span class="sxs-lookup"><span data-stu-id="27f42-1054">Repeats a string value a specified number of times.</span></span>  
  
 <span data-ttu-id="27f42-1055">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-1055">**Syntax**</span></span>  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="27f42-1056">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1056">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="27f42-1057">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-1057">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="27f42-1058">É qualquer expressão numérica válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-1058">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-1059">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-1059">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-1060">Retorna uma expressão de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="27f42-1060">Returns a string expression.</span></span>  
  
 <span data-ttu-id="27f42-1061">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1061">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-1062">saudação de exemplo a seguir mostra como toouse REPLICAR em uma consulta.</span><span class="sxs-lookup"><span data-stu-id="27f42-1062">hello following example shows how toouse REPLICATE in a query.</span></span>  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 <span data-ttu-id="27f42-1063">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-1063">Here is hello result set.</span></span>  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <span data-ttu-id="27f42-1064"><a name="bk_reverse"></a> REVERSE</span><span class="sxs-lookup"><span data-stu-id="27f42-1064"><a name="bk_reverse"></a> REVERSE</span></span>  
 <span data-ttu-id="27f42-1065">Retorna a ordem inversa Olá de um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="27f42-1065">Returns hello reverse order of a string value.</span></span>  
  
 <span data-ttu-id="27f42-1066">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-1066">**Syntax**</span></span>  
  
```  
REVERSE(<str_expr>)  
```  
  
 <span data-ttu-id="27f42-1067">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1067">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="27f42-1068">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-1068">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="27f42-1069">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-1069">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-1070">Retorna uma expressão de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="27f42-1070">Returns a string expression.</span></span>  
  
 <span data-ttu-id="27f42-1071">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1071">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-1072">saudação de exemplo a seguir mostra como toouse INVERTER em uma consulta.</span><span class="sxs-lookup"><span data-stu-id="27f42-1072">hello following example shows how toouse REVERSE in a query.</span></span>  
  
```  
SELECT REVERSE("Abc")  
```  
  
 <span data-ttu-id="27f42-1073">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-1073">Here is hello result set.</span></span>  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <span data-ttu-id="27f42-1074"><a name="bk_right"></a> RIGHT</span><span class="sxs-lookup"><span data-stu-id="27f42-1074"><a name="bk_right"></a> RIGHT</span></span>  
 <span data-ttu-id="27f42-1075">Olá retorna parte direita de uma cadeia de caracteres com hello número especificado de caracteres.</span><span class="sxs-lookup"><span data-stu-id="27f42-1075">Returns hello right part of a string with hello specified number of characters.</span></span>  
  
 <span data-ttu-id="27f42-1076">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-1076">**Syntax**</span></span>  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 <span data-ttu-id="27f42-1077">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1077">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="27f42-1078">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-1078">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="27f42-1079">É qualquer expressão numérica válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-1079">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-1080">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-1080">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-1081">Retorna uma expressão de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="27f42-1081">Returns a string expression.</span></span>  
  
 <span data-ttu-id="27f42-1082">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1082">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-1083">Olá, exemplo a seguir retorna Olá parte direita de "abc" para vários valores de comprimento.</span><span class="sxs-lookup"><span data-stu-id="27f42-1083">hello following example returns hello right part of "abc" for various length values.</span></span>  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 <span data-ttu-id="27f42-1084">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-1084">Here is hello result set.</span></span>  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <span data-ttu-id="27f42-1085"><a name="bk_rtrim"></a> RTRIM</span><span class="sxs-lookup"><span data-stu-id="27f42-1085"><a name="bk_rtrim"></a> RTRIM</span></span>  
 <span data-ttu-id="27f42-1086">Retorna uma expressão de cadeia de caracteres após remover os espaços em branco finais.</span><span class="sxs-lookup"><span data-stu-id="27f42-1086">Returns a string expression after it removes trailing blanks.</span></span>  
  
 <span data-ttu-id="27f42-1087">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-1087">**Syntax**</span></span>  
  
```  
RTRIM(<str_expr>)  
```  
  
 <span data-ttu-id="27f42-1088">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1088">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="27f42-1089">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-1089">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="27f42-1090">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-1090">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-1091">Retorna uma expressão de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="27f42-1091">Returns a string expression.</span></span>  
  
 <span data-ttu-id="27f42-1092">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1092">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-1093">Olá mostrado no exemplo a seguir como toouse RTRIM dentro de uma consulta.</span><span class="sxs-lookup"><span data-stu-id="27f42-1093">hello following example shows how toouse RTRIM inside a query.</span></span>  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 <span data-ttu-id="27f42-1094">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-1094">Here is hello result set.</span></span>  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <span data-ttu-id="27f42-1095"><a name="bk_startswith"></a> STARTSWITH</span><span class="sxs-lookup"><span data-stu-id="27f42-1095"><a name="bk_startswith"></a> STARTSWITH</span></span>  
 <span data-ttu-id="27f42-1096">Retorna um valor booleano que indica se primeira expressão de cadeia de caracteres hello começa com hello segundo.</span><span class="sxs-lookup"><span data-stu-id="27f42-1096">Returns a Boolean indicating whether hello first string expression starts with hello second.</span></span>  
  
 <span data-ttu-id="27f42-1097">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-1097">**Syntax**</span></span>  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 <span data-ttu-id="27f42-1098">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1098">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="27f42-1099">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-1099">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="27f42-1100">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-1100">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-1101">Retorna uma expressão booliana.</span><span class="sxs-lookup"><span data-stu-id="27f42-1101">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="27f42-1102">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1102">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-1103">Olá exemplo a seguir verifica se hello cadeia de caracteres "abc" começa com "b" e "a".</span><span class="sxs-lookup"><span data-stu-id="27f42-1103">hello following example checks if hello string "abc" begins with "b" and "a".</span></span>  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 <span data-ttu-id="27f42-1104">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-1104">Here is hello result set.</span></span>  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <span data-ttu-id="27f42-1105"><a name="bk_substring"></a> SUBSTRING</span><span class="sxs-lookup"><span data-stu-id="27f42-1105"><a name="bk_substring"></a> SUBSTRING</span></span>  
 <span data-ttu-id="27f42-1106">Retorna parte de uma expressão de cadeia de caracteres começando em Olá especificado a posição do caractere com base em zero e continua toohello especificado comprimento ou toohello final da cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-1106">Returns part of a string expression starting at hello specified character zero-based position and continues toohello specified length, or toohello end of hello string.</span></span>  
  
 <span data-ttu-id="27f42-1107">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-1107">**Syntax**</span></span>  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="27f42-1108">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1108">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="27f42-1109">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-1109">Is any valid string expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="27f42-1110">É qualquer expressão numérica válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-1110">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-1111">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-1111">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-1112">Retorna uma expressão de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="27f42-1112">Returns a string expression.</span></span>  
  
 <span data-ttu-id="27f42-1113">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1113">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-1114">Olá exemplo a seguir retorna Olá subcadeia de caracteres de "abc" começando em 1 e por um período de 1 caractere.</span><span class="sxs-lookup"><span data-stu-id="27f42-1114">hello following example returns hello substring of "abc" starting at 1 and for a length of 1 character.</span></span>  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 <span data-ttu-id="27f42-1115">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-1115">Here is hello result set.</span></span>  
  
```  
[{"$1": "b"}]  
```  
  
####  <span data-ttu-id="27f42-1116"><a name="bk_upper"></a> UPPER</span><span class="sxs-lookup"><span data-stu-id="27f42-1116"><a name="bk_upper"></a> UPPER</span></span>  
 <span data-ttu-id="27f42-1117">Retorna uma expressão de cadeia de caracteres após converter caracteres minúsculos toouppercase de dados.</span><span class="sxs-lookup"><span data-stu-id="27f42-1117">Returns a string expression after converting lowercase character data toouppercase.</span></span>  
  
 <span data-ttu-id="27f42-1118">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-1118">**Syntax**</span></span>  
  
```  
UPPER(<str_expr>)  
```  
  
 <span data-ttu-id="27f42-1119">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1119">**Arguments**</span></span>  
  
-   `str_expr`  
  
     <span data-ttu-id="27f42-1120">É qualquer expressão de cadeia de caracteres válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-1120">Is any valid string expression.</span></span>  
  
 <span data-ttu-id="27f42-1121">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-1121">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-1122">Retorna uma expressão de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="27f42-1122">Returns a string expression.</span></span>  
  
 <span data-ttu-id="27f42-1123">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1123">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-1124">Olá mostrado no exemplo a seguir como toouse superior em uma consulta</span><span class="sxs-lookup"><span data-stu-id="27f42-1124">hello following example shows how toouse UPPER in a query</span></span>  
  
```  
SELECT UPPER("Abc")  
```  
  
 <span data-ttu-id="27f42-1125">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-1125">Here is hello result set.</span></span>  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <span data-ttu-id="27f42-1126"><a name="bk_array_functions"></a> Funções de matriz</span><span class="sxs-lookup"><span data-stu-id="27f42-1126"><a name="bk_array_functions"></a> Array functions</span></span>  
 <span data-ttu-id="27f42-1127">Olá funções escalares a seguir executam uma operação em um valor de entrada de matriz e retorno numérico, valor booleano ou de matriz</span><span class="sxs-lookup"><span data-stu-id="27f42-1127">hello following scalar functions perform an operation on an array input value and return numeric, Boolean or array value</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="27f42-1128">ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="27f42-1128">ARRAY_CONCAT</span></span>](#bk_array_concat)|[<span data-ttu-id="27f42-1129">ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="27f42-1129">ARRAY_CONTAINS</span></span>](#bk_array_contains)|[<span data-ttu-id="27f42-1130">ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="27f42-1130">ARRAY_LENGTH</span></span>](#bk_array_length)|  
|[<span data-ttu-id="27f42-1131">ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="27f42-1131">ARRAY_SLICE</span></span>](#bk_array_slice)|||  
  
####  <span data-ttu-id="27f42-1132"><a name="bk_array_concat"></a>ARRAY_CONCAT</span><span class="sxs-lookup"><span data-stu-id="27f42-1132"><a name="bk_array_concat"></a> ARRAY_CONCAT</span></span>  
 <span data-ttu-id="27f42-1133">Retorna uma matriz que é o resultado de saudação da concatenação de dois ou mais valores de matriz.</span><span class="sxs-lookup"><span data-stu-id="27f42-1133">Returns an array that is hello result of concatenating two or more array values.</span></span>  
  
 <span data-ttu-id="27f42-1134">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-1134">**Syntax**</span></span>  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 <span data-ttu-id="27f42-1135">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1135">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="27f42-1136">É qualquer expressão válida de matriz.</span><span class="sxs-lookup"><span data-stu-id="27f42-1136">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="27f42-1137">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-1137">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-1138">Retorna uma expressão de matriz.</span><span class="sxs-lookup"><span data-stu-id="27f42-1138">Returns an array expression.</span></span>  
  
 <span data-ttu-id="27f42-1139">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1139">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-1140">Olá como tooconcatenate duas matrizes de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="27f42-1140">hello following example how tooconcatenate two arrays.</span></span>  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 <span data-ttu-id="27f42-1141">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-1141">Here is hello result set.</span></span>  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <span data-ttu-id="27f42-1142"><a name="bk_array_contains"></a>ARRAY_CONTAINS</span><span class="sxs-lookup"><span data-stu-id="27f42-1142"><a name="bk_array_contains"></a> ARRAY_CONTAINS</span></span>  
 <span data-ttu-id="27f42-1143">Retorna um valor booleano que indica se a matriz de saudação contém Olá valor especificado.</span><span class="sxs-lookup"><span data-stu-id="27f42-1143">Returns a Boolean indicating whether hello array contains hello specified value.</span></span>  
  
 <span data-ttu-id="27f42-1144">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-1144">**Syntax**</span></span>  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr>)  
```  
  
 <span data-ttu-id="27f42-1145">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1145">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="27f42-1146">É qualquer expressão válida de matriz.</span><span class="sxs-lookup"><span data-stu-id="27f42-1146">Is any valid array expression.</span></span>  
  
-   `expr`  
  
     <span data-ttu-id="27f42-1147">É qualquer expressão válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-1147">Is any valid expression.</span></span>  
  
 <span data-ttu-id="27f42-1148">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-1148">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-1149">Retorna um valor booliano.</span><span class="sxs-lookup"><span data-stu-id="27f42-1149">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="27f42-1150">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1150">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-1151">saudação de exemplo a seguir como toocheck associação em uma matriz usando ARRAY_CONTAINS.</span><span class="sxs-lookup"><span data-stu-id="27f42-1151">hello following example how toocheck for membership in an array using ARRAY_CONTAINS.</span></span>  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 <span data-ttu-id="27f42-1152">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-1152">Here is hello result set.</span></span>  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <span data-ttu-id="27f42-1153"><a name="bk_array_length"></a>ARRAY_LENGTH</span><span class="sxs-lookup"><span data-stu-id="27f42-1153"><a name="bk_array_length"></a> ARRAY_LENGTH</span></span>  
 <span data-ttu-id="27f42-1154">Retorna o número de saudação de elementos da saudação especificado expressão de matriz.</span><span class="sxs-lookup"><span data-stu-id="27f42-1154">Returns hello number of elements of hello specified array expression.</span></span>  
  
 <span data-ttu-id="27f42-1155">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-1155">**Syntax**</span></span>  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 <span data-ttu-id="27f42-1156">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1156">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="27f42-1157">É qualquer expressão válida de matriz.</span><span class="sxs-lookup"><span data-stu-id="27f42-1157">Is any valid array expression.</span></span>  
  
 <span data-ttu-id="27f42-1158">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-1158">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-1159">Retorna uma expressão numérica.</span><span class="sxs-lookup"><span data-stu-id="27f42-1159">Returns a numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-1160">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1160">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-1161">Olá exemplo a seguir como tooget Olá comprimento de uma matriz usando ARRAY_LENGTH.</span><span class="sxs-lookup"><span data-stu-id="27f42-1161">hello following example how tooget hello length of an array using ARRAY_LENGTH.</span></span>  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 <span data-ttu-id="27f42-1162">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-1162">Here is hello result set.</span></span>  
  
```  
[{"$1": 3}]  
```  
  
####  <span data-ttu-id="27f42-1163"><a name="bk_array_slice"></a>ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="27f42-1163"><a name="bk_array_slice"></a> ARRAY_SLICE</span></span>  
 <span data-ttu-id="27f42-1164">Retorna parte de uma expressão de matriz.</span><span class="sxs-lookup"><span data-stu-id="27f42-1164">Returns part of an array expression.</span></span>
  
 <span data-ttu-id="27f42-1165">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-1165">**Syntax**</span></span>  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 <span data-ttu-id="27f42-1166">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1166">**Arguments**</span></span>  
  
-   `arr_expr`  
  
     <span data-ttu-id="27f42-1167">É qualquer expressão válida de matriz.</span><span class="sxs-lookup"><span data-stu-id="27f42-1167">Is any valid array expression.</span></span>  
  
-   `num_expr`  
  
     <span data-ttu-id="27f42-1168">É qualquer expressão numérica válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-1168">Is any valid numeric expression.</span></span>  
  
 <span data-ttu-id="27f42-1169">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-1169">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-1170">Retorna um valor booliano.</span><span class="sxs-lookup"><span data-stu-id="27f42-1170">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="27f42-1171">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1171">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-1172">saudação de exemplo a seguir como tooget uma parte de uma matriz usando ARRAY_SLICE.</span><span class="sxs-lookup"><span data-stu-id="27f42-1172">hello following example how tooget a part of an array using ARRAY_SLICE.</span></span>  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 <span data-ttu-id="27f42-1173">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-1173">Here is hello result set.</span></span>  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <span data-ttu-id="27f42-1174"><a name="bk_spatial_functions"></a> Funções espaciais</span><span class="sxs-lookup"><span data-stu-id="27f42-1174"><a name="bk_spatial_functions"></a> Spatial functions</span></span>  
 <span data-ttu-id="27f42-1175">Olá funções escalares a seguir executam uma operação em um valor de entrada do objeto espacial e retornam um valor numérico ou booleano.</span><span class="sxs-lookup"><span data-stu-id="27f42-1175">hello following scalar functions perform an operation on an spatial object input value and return a numeric or Boolean value.</span></span>  
  
||||  
|-|-|-|  
|[<span data-ttu-id="27f42-1176">ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="27f42-1176">ST_DISTANCE</span></span>](#bk_st_distance)|[<span data-ttu-id="27f42-1177">ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="27f42-1177">ST_WITHIN</span></span>](#bk_st_within)|[<span data-ttu-id="27f42-1178">ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="27f42-1178">ST_INTERSECTS</span></span>](#bk_st_intersects)|[<span data-ttu-id="27f42-1179">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="27f42-1179">ST_ISVALID</span></span>](#bk_st_isvalid)|  
|[<span data-ttu-id="27f42-1180">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="27f42-1180">ST_ISVALIDDETAILED</span></span>](#bk_st_isvaliddetailed)|||  
  
####  <span data-ttu-id="27f42-1181"><a name="bk_st_distance"></a> ST_DISTANCE</span><span class="sxs-lookup"><span data-stu-id="27f42-1181"><a name="bk_st_distance"></a> ST_DISTANCE</span></span>  
 <span data-ttu-id="27f42-1182">Retorna a distância de saudação entre expressões de LineString, Polygon ou ponto GeoJSON Olá dois.</span><span class="sxs-lookup"><span data-stu-id="27f42-1182">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span>  
  
 <span data-ttu-id="27f42-1183">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-1183">**Syntax**</span></span>  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="27f42-1184">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1184">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="27f42-1185">É qualquer expressão de objeto Ponto GeoJSON, Polígono ou LineString válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-1185">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="27f42-1186">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-1186">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-1187">Retorna uma expressão numérica que contém a distância de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-1187">Returns a numeric expression containing hello distance.</span></span> <span data-ttu-id="27f42-1188">Isso é expresso em metros para o sistema de referência padrão hello.</span><span class="sxs-lookup"><span data-stu-id="27f42-1188">This is expressed in meters for hello default reference system.</span></span>  
  
 <span data-ttu-id="27f42-1189">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1189">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-1190">Olá mostrado no exemplo a seguir como tooreturn todos os documentos de família de produtos que estão dentro de 30 km de saudação especificado usando a função interna de ST_DISTANCE de saudação do local.</span><span class="sxs-lookup"><span data-stu-id="27f42-1190">hello following example shows how tooreturn all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> <span data-ttu-id="27f42-1191">.</span><span class="sxs-lookup"><span data-stu-id="27f42-1191">.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 <span data-ttu-id="27f42-1192">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-1192">Here is hello result set.</span></span>  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <span data-ttu-id="27f42-1193"><a name="bk_st_within"></a> ST_WITHIN</span><span class="sxs-lookup"><span data-stu-id="27f42-1193"><a name="bk_st_within"></a> ST_WITHIN</span></span>  
 <span data-ttu-id="27f42-1194">Retorna uma expressão booleana que indica se Olá GeoJSON o objeto (ponto, polígono ou LineString) especificado no primeiro argumento de saudação está dentro Olá GeoJSON (ponto, polígono ou LineString) no segundo argumento de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-1194">Returns a Boolean expression indicating whether hello GeoJSON object (Point, Polygon, or LineString) specified in hello first argument is within hello GeoJSON (Point, Polygon, or LineString) in hello second argument.</span></span>  
  
 <span data-ttu-id="27f42-1195">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-1195">**Syntax**</span></span>  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="27f42-1196">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1196">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="27f42-1197">É qualquer expressão de objeto Ponto GeoJSON, Polígono ou LineString válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-1197">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="27f42-1198">É qualquer expressão de objeto Ponto GeoJSON, Polígono ou LineString válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-1198">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="27f42-1199">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-1199">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-1200">Retorna um valor booliano.</span><span class="sxs-lookup"><span data-stu-id="27f42-1200">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="27f42-1201">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1201">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-1202">saudação de exemplo a seguir mostra como toofind família de todos os documentos dentro de um polígono usando ST_WITHIN.</span><span class="sxs-lookup"><span data-stu-id="27f42-1202">hello following example shows how toofind all family documents within a polygon using ST_WITHIN.</span></span>  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="27f42-1203">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-1203">Here is hello result set.</span></span>  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <span data-ttu-id="27f42-1204"><a name="bk_st_intersects"></a>ST_INTERSECTS</span><span class="sxs-lookup"><span data-stu-id="27f42-1204"><a name="bk_st_intersects"></a> ST_INTERSECTS</span></span>  
 <span data-ttu-id="27f42-1205">Retorna uma expressão booleana que indica se Olá GeoJSON o objeto (ponto, polígono ou LineString) especificado no primeiro argumento de saudação intercepta Olá GeoJSON (ponto, polígono ou LineString) no segundo argumento de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-1205">Returns a Boolean expression indicating whether hello GeoJSON object (Point, Polygon, or LineString) specified in hello first argument intersects hello GeoJSON (Point, Polygon, or LineString) in hello second argument.</span></span>  
  
 <span data-ttu-id="27f42-1206">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-1206">**Syntax**</span></span>  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 <span data-ttu-id="27f42-1207">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1207">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="27f42-1208">É qualquer expressão de objeto Ponto GeoJSON, Polígono ou LineString válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-1208">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
 
-   `spatial_expr`  
  
     <span data-ttu-id="27f42-1209">É qualquer expressão de objeto Ponto GeoJSON, Polígono ou LineString válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-1209">Is any valid GeoJSON Point, Polygon, or LineString object expression.</span></span>  
  
 <span data-ttu-id="27f42-1210">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-1210">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-1211">Retorna um valor booliano.</span><span class="sxs-lookup"><span data-stu-id="27f42-1211">Returns a Boolean value.</span></span>  
  
 <span data-ttu-id="27f42-1212">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1212">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-1213">Olá mostrado no exemplo a seguir como toofind todas as áreas que faz interseção com hello fornecido polígono.</span><span class="sxs-lookup"><span data-stu-id="27f42-1213">hello following example shows how toofind all areas that intersects with hello given polygon.</span></span>  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 <span data-ttu-id="27f42-1214">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-1214">Here is hello result set.</span></span>  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <span data-ttu-id="27f42-1215"><a name="bk_st_isvalid"></a> ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="27f42-1215"><a name="bk_st_isvalid"></a> ST_ISVALID</span></span>  
 <span data-ttu-id="27f42-1216">Retorna um valor booliano que indica se a saudação especificado LineString, Polygon ou ponto GeoJSON expressão é válida.</span><span class="sxs-lookup"><span data-stu-id="27f42-1216">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span>  
  
 <span data-ttu-id="27f42-1217">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-1217">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="27f42-1218">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1218">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="27f42-1219">É qualquer expressão válida de LineString, polígono ou ponto GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="27f42-1219">Is any valid GeoJSON Point, Polygon, or LineString expression.</span></span>  
  
 <span data-ttu-id="27f42-1220">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-1220">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-1221">Retorna uma expressão booliana.</span><span class="sxs-lookup"><span data-stu-id="27f42-1221">Returns a Boolean expression.</span></span>  
  
 <span data-ttu-id="27f42-1222">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1222">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-1223">Olá mostrado no exemplo a seguir como toocheck se um ponto é válido usar ST_VALID.</span><span class="sxs-lookup"><span data-stu-id="27f42-1223">hello following example shows how toocheck if a point is valid using ST_VALID.</span></span>  
  
 <span data-ttu-id="27f42-1224">Por exemplo, esse ponto tem um valor de latitude que não está em um intervalo válido de valores [-90, 90] hello, Olá então consulta retornará false.</span><span class="sxs-lookup"><span data-stu-id="27f42-1224">For example, this point has a latitude value that's not in hello valid range of values [-90, 90], so hello query returns false.</span></span>  
  
 <span data-ttu-id="27f42-1225">Para polígonos, Olá GeoJSON especificação requer que Olá último par de coordenadas fornecido deve ser Olá mesmo como toocreate primeiro, Olá uma forma fechada.</span><span class="sxs-lookup"><span data-stu-id="27f42-1225">For polygons, hello GeoJSON specification requires that hello last coordinate pair provided should be hello same as hello first, toocreate a closed shape.</span></span> <span data-ttu-id="27f42-1226">Os pontos em um polígono devem ser especificados no sentido anti-horário.</span><span class="sxs-lookup"><span data-stu-id="27f42-1226">Points within a polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="27f42-1227">Um polígono especificado na ordem no sentido horário representa inverso de saudação da região hello dentro dele.</span><span class="sxs-lookup"><span data-stu-id="27f42-1227">A polygon specified in clockwise order represents hello inverse of hello region within it.</span></span>  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 <span data-ttu-id="27f42-1228">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-1228">Here is hello result set.</span></span>  
  
```  
[{ "$1": false }]  
```  
  
####  <span data-ttu-id="27f42-1229"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="27f42-1229"><a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED</span></span>  
 <span data-ttu-id="27f42-1230">Retorna um valor JSON que contém um valor booliano se Olá especificado expressão LineString, Polygon ou ponto GeoJSON é válido e se for inválido, além disso Olá motivo como um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="27f42-1230">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span>  
  
 <span data-ttu-id="27f42-1231">**Sintaxe**</span><span class="sxs-lookup"><span data-stu-id="27f42-1231">**Syntax**</span></span>  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 <span data-ttu-id="27f42-1232">**Argumentos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1232">**Arguments**</span></span>  
  
-   `spatial_expr`  
  
     <span data-ttu-id="27f42-1233">É qualquer expressão válida de ponto ou polígono GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="27f42-1233">Is any valid GeoJSON point or polygon expression.</span></span>  
  
 <span data-ttu-id="27f42-1234">**Tipos de retorno**</span><span class="sxs-lookup"><span data-stu-id="27f42-1234">**Return Types**</span></span>  
  
 <span data-ttu-id="27f42-1235">Retorna um valor JSON que contém um valor booliano se Olá especificado ponto GeoJSON ou expressão de polígono é válido e se for inválido, além disso Olá motivo como um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="27f42-1235">Returns a JSON value containing a Boolean value if hello specified GeoJSON point or polygon expression is valid, and if invalid, additionally hello reason as a string value.</span></span>  
  
 <span data-ttu-id="27f42-1236">**Exemplos**</span><span class="sxs-lookup"><span data-stu-id="27f42-1236">**Examples**</span></span>  
  
 <span data-ttu-id="27f42-1237">saudação de exemplo a seguir como toocheck validade (com detalhes) usando ST_ISVALIDDETAILED.</span><span class="sxs-lookup"><span data-stu-id="27f42-1237">hello following example how toocheck validity (with details) using ST_ISVALIDDETAILED.</span></span>  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 <span data-ttu-id="27f42-1238">Aqui está o conjunto de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="27f42-1238">Here is hello result set.</span></span>  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a polygon must have hello same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a><span data-ttu-id="27f42-1239">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="27f42-1239">Next steps</span></span>  
 <span data-ttu-id="27f42-1240">[Sintaxe SQL e consulta SQL para BD Cosmos do Azure](documentdb-sql-query.md) </span><span class="sxs-lookup"><span data-stu-id="27f42-1240">[SQL syntax and SQL query for Azure Cosmos DB](documentdb-sql-query.md) </span></span>  
 [<span data-ttu-id="27f42-1241">Documentação do BD Cosmos do Azure</span><span class="sxs-lookup"><span data-stu-id="27f42-1241">Azure Cosmos DB documentation</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/)  
  
  
