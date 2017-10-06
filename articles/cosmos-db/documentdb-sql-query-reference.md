---
título: aaa "API DocumentDB do Azure Cosmos DB: sintaxe SQL | Descrição de Microsoft Docs": documentação para Olá linguagem de consulta SQL de API do DocumentDB do Azure Cosmos banco de dados de referência.
serviços: cosmos db autor: manager mimig1: jhubbard editor: mimig documentationcenter: '

MS. AssetID: MS. Service: cosmos db Workload: serviços de dados tgt_pltfrm: na MS. devlang: na MS. Topic: referência MS. Date: 13/06/2017 Author: mimig

---

# <a name="azure-cosmos-db-documentdb-api-sql-syntax-reference"></a>API DocumentDB do BD Cosmos do Azure: referência de sintaxe SQL

Olá API DocumentDB do Azure Cosmos DB dá suporte a documentos de consultando usando um familiar SQL (Structured Query Language) como a gramática em documentos JSON hierárquicos sem a necessidade de esquema explícito ou a criação de índices secundários. Este tópico fornece documentação de referência para Olá linguagem de consulta SQL de API do DocumentDB.

Para obter uma explicação da saudação linguagem de consulta SQL de API de documentos, consulte [consultas SQL para a API DocumentDB do Azure Cosmos DB](documentdb-sql-query.md).  
  
Também você está convidado Olá toovisit [parque de consulta](http://www.documentdb.com/sql/demo) onde você pode tentar o banco de dados do Azure Cosmos e executar consultas SQL em nosso conjunto de dados.  
  
## <a name="select-query"></a>Consulta SELECT  
Recupera documentos JSON do banco de dados de saudação. Dá suporte a avaliação de expressão, projeções, filtragem e junções.  convenções de saudação usadas para descrever instruções SELECT Olá são tabuladas na Olá seção de convenções de sintaxe.  
  
**Sintaxe**  
  
```
<select_query> ::=  
SELECT <select_specification>   
    [ FROM <from_specification>]   
    [ WHERE <filter_condition> ]  
    [ ORDER BY <sort_specification> ]  
```  
  
 **Comentários**  
  
 Consulte as seguintes seções para obter detalhes sobre cada cláusula:  
  
-   [Cláusula SELECT](#bk_select_query)  
  
-   [Cláusula FROM](#bk_from_clause)  
  
-   [Cláusula WHERE](#bk_where_clause)  
  
-   [Cláusula ORDER BY](#bk_orderby_clause)  
  
cláusulas de saudação na instrução SELECT Olá devem ser ordenadas, conforme mostrado acima. Qualquer uma das cláusulas opcionais Olá pode ser omitida. Mas quando são usadas, eles devem aparecer na ordem correta hello.  
  
**Ordem de processamento lógico da instrução SELECT Olá**  
  
Olá ordem na qual as cláusulas são processadas é:  

1.  [Cláusula FROM](#bk_from_clause)  
2.  [Cláusula WHERE](#bk_where_clause)  
3.  [Cláusula ORDER BY](#bk_orderby_clause)  
4.  [Cláusula SELECT](#bk_select_query)  

Observe que isso é diferente da saudação ordem em que aparecem na sintaxe de saudação. Olá ordenação é tal que todos os símbolos novos introduzidos por uma cláusula processada são visíveis e podem ser usados em cláusulas processadas posteriormente. Por exemplo, os aliases declarados em uma cláusula FROM podem ser acessados nas cláusulas SELECT e WHERE.  

**Comentários e caracteres de espaço em branco**  

Todos os caracteres de espaço em branco que não fazem parte de uma cadeia de caracteres entre aspas ou identificador entre aspas não fazem parte da gramática da linguagem hello e são ignorados durante a análise.  

oferece suporte a linguagem de consulta Hello como comentários de estilo do T-SQL  

-   Instrução SQL`-- comment text [newline]`  

Enquanto comentários e caracteres de espaço em branco não tenham nenhum significado na gramática hello, eles devem ser usados tooseparate tokens. Por exemplo: `-1e5` é um token de número único, ao passo que `: – 1 e5` é um token de sinal de subtração seguido pelo número 1 e identificador e5.  

##  <a name="bk_select_query"></a> Cláusula SELECT  
cláusulas de saudação na instrução SELECT Olá devem ser ordenadas, conforme mostrado acima. Qualquer uma das cláusulas opcionais Olá pode ser omitida. Mas quando são usadas, eles devem aparecer na ordem correta hello.  

**Sintaxe**  
```  
SELECT <select_specification>  

<select_specification> ::=   
      '*'   
      | <object_property_list>   
      | VALUE <scalar_expression> [[ AS ] value_alias]  
  
<object_property_list> ::=   
{ <scalar_expression> [ [ AS ] property_alias ] } [ ,...n ]  
  
```  
  
 **Argumentos**  
  
 `<select_specification>`  
  
 Toobe propriedades ou o valor selecionado para o resultado de saudação definido.  
  
 `'*'`  
  
Especifica que o valor de saudação deve ser recuperado sem fazer alterações. Especificamente se o valor de saudação processada é um objeto, todas as propriedades serão recuperadas.  
  
 `<object_property_list>`  
  
Especifica a lista de saudação do toobe de propriedades recuperada. Cada valor retornado será um objeto com propriedades de saudação especificado.  
  
`VALUE`  
  
Especifica que o valor JSON Olá deve ser recuperada em vez do objeto JSON completo de saudação. Isso, ao contrário `<property_list>` não colocar o valor de saudação projetada em um objeto.  
  
`<scalar_expression>`  
  
Expressão que representa a saudação toobe de valor computado. Consulte a seção [Expressões escalares](#bk_scalar_expressions) para obter detalhes.  
  
**Comentários**  
  
Olá `SELECT *` sintaxe só será válida se a cláusula FROM tiver declarado exatamente um alias. `SELECT *` fornece uma projeção de identidade, que pode ser útil se nenhuma projeção é necessária. SELECT * só é válida se a cláusula FROM é especificada e introduzida uma única fonte de entrada.  
  
Observe que `SELECT <select_list>` e `SELECT *` são "açúcar sintático" e podem ser expressos, como alternativa, usando instruções SELECT simples, conforme mostrado abaixo.  
  
1.  `SELECT * FROM ... AS from_alias ...`  
  
     é equivalente a:  
  
     `SELECT from_alias FROM ... AS from_alias ...`  
  
2.  `SELECT <expr1> AS p1, <expr2> AS p2,..., <exprN> AS pN [other clauses...]`  
  
     é equivalente a:  
  
     `SELECT VALUE { p1: <expr1>, p2: <expr2>, ..., pN: <exprN> }[other clauses...]`  
  
**Consulte também**  
  
[Expressões escalares](#bk_scalar_expressions)  
[Cláusula SELECT](#bk_select_query)  
  
##  <a name="bk_from_clause"></a> Cláusula FROM  
Especifica a fonte de saudação ou fontes unidas. cláusula FROM de saudação é opcional. Se não for especificado, outras cláusulas ainda serão executadas como se a cláusula FROM fornecesse um único documento.  
  
**Sintaxe**  
  
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
  
**Argumentos**  
  
`<from_source>`  
  
Especifica uma fonte de dados, com ou sem um alias. Se o alias não for especificado, ele será inferido de saudação `<collection_expression>` usando as seguinte regras:  
  
-   Se a expressão de saudação for um collection_name, collection_name será ser usado como um alias.  
  
-   Se a expressão de saudação é `<collection_expression>`, property_name e, em seguida, property_name será usado como um alias. Se a expressão de saudação for um collection_name, collection_name será ser usado como um alias.  
  
AS `input_alias`  
  
Especifica que Olá `input_alias` é um conjunto de valores retornados por Olá subjacente da expressão de coleção.  
 
`input_alias` IN  
  
Especifica que Olá `input_alias` deve representar o conjunto de saudação de valores obtidos pela iteração em todos os elementos da matriz de cada matriz retornada por Olá subjacente da expressão de coleção. Qualquer valor retornado pela expressão de coleção subjacente que não seja uma matriz é ignorado.  
  
`<collection_expression>`  
  
Especifica Olá coleção expressão toobe tooretrieve documentos de saudação.  
  
`ROOT`  
  
Especifica que documento deve ser recuperado do padrão de saudação, coleção conectada no momento.  
  
`collection_name`  
  
Especifica que documento deve ser recuperado da coleção Olá fornecido. nome de Olá da coleção de saudação deve corresponder o nome de saudação da coleção Olá conectada no momento.  
  
`input_alias`  
  
Especifica que documento deve ser recuperado da saudação outra fonte definida pelo alias Olá fornecido.  
  
`<collection_expression> '.' property_`  
  
Especifica que documento deve ser recuperado acessando Olá `property_name` especificado de elemento de matriz de propriedade ou array_index para todos os documentos recuperados pela expressão de coleção.  
  
`<collection_expression> '[' "property_name" | array_index ']'`  
  
Especifica que documento deve ser recuperado acessando Olá `property_name` especificado de elemento de matriz de propriedade ou array_index para todos os documentos recuperados pela expressão de coleção.  
  
**Comentários**  
  
Todos os aliases fornecidos ou inferidos em Olá `<from_source>(`s) deve ser exclusivo. Olá sintaxe `<collection_expression>.`property_name é Olá igual `<collection_expression>' ['"property_name"']'`. No entanto, última sintaxe de saudação pode ser usado se um nome de propriedade contém um caractere não identificador.  
  
**Propriedades ausentes, elementos de matriz ausentes, tratamento de valores indefinidos**  
  
Se uma expressão de coleção acessar propriedades ou elementos da matriz e o valor não existir, esse valor será ignorado e não processado.  
  
**Escopo de contexto de expressão de coleção**  
  
Uma expressão de coleção pode ser coleção com escopo ou documento com escopo:  
  
-   Uma expressão é coleção com escopo, se hello fonte subjacente da expressão de coleção de saudação for ROOT ou `collection_name`. Essa expressão representa um conjunto de documentos recuperados diretamente da coleção Olá e não é dependente de processamento de saudação de outras expressões de coleção.  
  
-   Uma expressão é documento com escopo, se hello fonte subjacente da expressão de coleção de saudação é `input_alias` introduzida anteriormente na consulta de saudação. Essa expressão representa um conjunto de documentos obtido avaliando a expressão de coleção Olá no escopo de saudação de cada documento pertencente toohello conjunto associado a coleção de um alias de saudação.  conjunto resultante da saudação será uma união de conjuntos obtidos avaliando a expressão de coleção Olá para cada um dos documentos Olá Olá subjacente conjunto.  
  
**Junções**  
  
Na versão atual do hello, o banco de dados do Azure Cosmos oferece suporte a junções internas. Recursos adicionais de junção serão disponibilizados em breve.

Conjuntos de resultados de junções internas em um produto cruzado completo de saudação participam da junção hello. resultado de saudação de uma junção N-way é um conjunto de tuplas de elemento N, onde cada valor na tupla Olá é associado com um alias de saudação conjunto de participação na junção hello e pode ser acessada referenciando esse alias em outras cláusulas.  
  
avaliação de saudação de junção Olá depende escopo contexto Olá Olá conjuntos de participação:  
  
-  Uma junção entre um conjunto de coleção A e o conjunto de coleção com escopo definido B resulta em um produto cruzado de todos os elementos nos conjuntos A e B.
  
-   Uma associação entre o conjunto A e o conjunto com escopo de documento B resulta em uma união de todos os conjuntos obtidos pela avaliação do conjunto com escopo de documento B para cada documento do conjunto A.  
  
 Na versão atual do hello, um máximo de uma expressão de coleção com escopo suportado pelo processador de consulta de saudação.  
  
**Exemplos de junções:**  
  
Vejamos Olá seguinte cláusula FROM:`<from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>`  
  
 Permite que cada fonte defina `input_alias1, input_alias2, …, input_aliasN`. Essa cláusula FROM retorna um conjunto de tuplas N (tupla com valores N). Cada tupla terá os valores produzidos pela iteração de todos os alias da coleção em seus respectivos conjuntos.  
  
*JUNÇÃO exemplo 1, com 2 fontes:*  
  
- Permite que `<from_source1>` tenha escopo de coleção e represente o conjunto {A, B, C}.  
  
- Permite que `<from_source2>` tenha escopo de documento, referenciando input_alias1 e represente os conjuntos:  
  
    {1,2} para `input_alias1 = A,`  
  
    {3} para`input_alias1 = B,`  
  
    {4,5} para`input_alias1 = C,`  
  
- Olá cláusula FROM `<from_source1> JOIN <from_source2>` resultará em Olá tuplas a seguir:  
  
    (`input_alias1, input_alias2`):  
  
    `(A, 1), (A, 2), (B, 3), (C, 4), (C, 5)`  
  
*JUNÇÃO exemplo 2, com 3 fontes:*  
  
- Permite que `<from_source1>` tenha escopo de coleção e represente o conjunto {A, B, C}.  
  
- Permite que `<from_source2>` tenha escopo de documento, referenciando `input_alias1` e represente os conjuntos:  
  
    {1,2} para `input_alias1 = A,`  
  
    {3} para`input_alias1 = B,`  
  
    {4,5} para`input_alias1 = C,`  
  
- Permite que `<from_source3>` tenha escopo de documento, referenciando `input_alias2` e represente os conjuntos:  
  
    {100, 200} para`input_alias2 = 1,`  
  
    {300} para`input_alias2 = 3,`  
  
- Olá cláusula FROM `<from_source1> JOIN <from_source2> JOIN <from_source3>` resultará em Olá tuplas a seguir:  
  
    (input_alias1, input_alias2, input_alias3):  
  
    (A, 1, 100), (A, 1, 200), (B, 3, 300)  
  
> [!NOTE]
> Falta de tuplas para outros valores de `input_alias1`, `input_alias2`, para qual Olá `<from_source3>` não retornou nenhum valor.  
  
*JUNÇÃO exemplo 3, com 3 fontes:*  
  
- Permite que <from_source1> tenha escopo de coleção e represente o conjunto {A, B, C}.  
  
- Permite que `<from_source1>` tenha escopo de coleção e represente o conjunto {A, B, C}.  
  
- Permite que <from_source2> tenha escopo de documento, referenciando input_alias1 e represente os conjuntos:  
  
    {1,2} para `input_alias1 = A,`  
  
    {3} para`input_alias1 = B,`  
  
    {4,5} para`input_alias1 = C,`  
  
- Permitir que `<from_source3>` escopo muito`input_alias1` e represente conjuntos:  
  
    {100, 200} para`input_alias2 = A,`  
  
    {300} para`input_alias2 = C,`  
  
- Olá cláusula FROM `<from_source1> JOIN <from_source2> JOIN <from_source3>` resultará em Olá tuplas a seguir:  
  
    (`input_alias1, input_alias2, input_alias3`):  
  
    (A, 1, 100), (A, 1, 200), (A, 2, 100), (A, 2, 200),  (C, 4, 300) , (C, 5, 300)  
  
> [!NOTE]
> Isso resultou em produto cruzado entre `<from_source2>` e `<from_source3>` porque ambos estão no escopo toohello mesmo `<from_source1>`.  Isso resultou em 4 (2 x 2) tuplas com valor A, 0 tuplas com valor B (1 x 0) e 2 (2 x 1) tuplas com valor C.  
  
**Consulte também**  
  
 [Cláusula SELECT](#bk_select_query)  
  
##  <a name="bk_where_clause"></a> Cláusula WHERE  
 Especifica o critério de pesquisa Olá Olá documentos retornados pela consulta hello.  
  
 **Sintaxe**  
  
```  
WHERE <filter_condition>  
<filter_condition> ::= <scalar_expression>  
  
```  
  
 **Argumentos**  
  
-   `<filter_condition>`  
  
     Especifica a saudação condição toobe atendido para Olá documentos toobe retornado.  
  
-   `<scalar_expression>`  
  
     Expressão que representa a saudação toobe de valor computado. Consulte Olá [expressões escalares](#bk_scalar_expressions) seção para obter detalhes.  
  
 **Comentários**  
  
 Para que Olá toobe documento retornado uma expressão especificada como condição de filtro deve ser avaliada tootrue. Somente o valor booliano true atenderá a condição de hello, qualquer outro valor: indefinido, nulo, FALSO, número, matriz ou objeto não atenderá Olá condição.  
  
##  <a name="bk_orderby_clause"></a> Cláusula ORDER BY  
 Especifica a saudação ordem de classificação para resultados retornados pela consulta hello.  
  
 **Sintaxe**  
  
```  
ORDER BY <sort_specification>  
<sort_specification> ::= <sort_expression> [, <sort_expression>]  
<sort_expression> ::= <scalar_expression> [ASC | DESC]  
  
```  
  
 **Argumentos**  
  
-   `<sort_specification>`  
  
     Especifica uma propriedade ou expressão na qual conjunto de resultados de consulta de saudação toosort. Uma coluna de classificação pode ser especificada como um alias de nome ou coluna.  
  
     Várias colunas de classificação podem ser especificadas. Os nomes de coluna devem ser exclusivos. sequência de saudação de colunas de classificação de saudação na cláusula ORDER BY da saudação define a organização Olá Olá classificado do conjunto de resultados. Ou seja, Olá conjunto de resultados é classificado pela propriedade primeiro hello e, em seguida, essa lista ordenada é classificada pela propriedade segundo Olá e assim por diante.  
  
     nomes de coluna Olá referenciados na cláusula ORDER BY da saudação devem corresponder tooeither uma coluna em Olá Selecionar coluna de lista ou tooa definida em uma tabela especificada na cláusula FROM de saudação sem qualquer ambiguidade.  
  
-   `<sort_expression>`  
  
     Especifica uma única propriedade ou expressão na qual conjunto de resultados de consulta de saudação toosort.  
  
-   `<scalar_expression>`  
  
     Consulte Olá [expressões escalares](#bk_scalar_expressions) seção para obter detalhes.  
  
-   `ASC | DESC`  
  
     Especifica que os valores hello na coluna especificada Olá devem ser classificados em ordem crescente ou decrescente. ASC classifica do valor de toohighest valor mais baixo de saudação. DESC classifica do valor de toolowest de valor mais alto. ASC é a ordem de classificação padrão hello. Valores nulos são tratados como valores possíveis mais baixos de saudação.  
  
 **Comentários**  
  
 Enquanto a gramática de consulta Olá dá suporte a vários pedidos por propriedades, tempo de execução de consulta de banco de dados do Azure Cosmos Olá dá suporte à classificação apenas contra uma única propriedade e somente nomes de propriedade, ou seja, não contra propriedades calculadas. A classificação também requer que Olá política de indexação inclui um índice de intervalo para a propriedade hello e hello especificado tipo, com precisão máxima da saudação. Consulte toohello documentação para obter mais detalhes da política de indexação.  
  
##  <a name="bk_scalar_expressions"></a> Expressões escalares  
 Uma expressão escalar é uma combinação de símbolos e operadores que podem ser avaliados tooobtain um único valor. Expressões simples podem ser constantes, referências de propriedade, referências de elemento de matriz, referências de alias ou chamadas de função. As expressões simples podem ser combinadas em expressões complexas usando operadores.  
  
 Para obter detalhes sobre os valores que a expressão escalar pode ter, consulte a seção [Constantes](#bk_constants).  
  
 **Sintaxe**  
  
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
  
 **Argumentos**  
  
-   `<constant>`  
  
     Representa um valor constante. Consulte a seção [Constantes](#bk_constants) para obter detalhes.  
  
-   `input_alias`  
  
     Representa um valor definido por Olá `input_alias` introduzido no hello `FROM` cláusula.  
    Esse valor tem garantia toonot ser **indefinido** –**indefinido** os valores na entrada hello serão ignorados.  
  
-   `<scalar_expression>.property_name`  
  
     Representa um valor de propriedade de saudação de um objeto. Se Olá a propriedade não existe ou propriedade é referenciada em um valor que não é um objeto, Olá avalia muito**indefinido** valor.  
  
-   `<scalar_expression>'['"property_name"|array_index']'`  
  
     Representa um valor da propriedade Olá com nome `property_name` ou elemento de matriz com índice `array_index` de uma matriz de objetos /. Se o índice de matriz/propriedade Olá não existe ou o índice de matriz/propriedade Olá é referenciado em um valor que não é uma matriz de objetos /, Olá expressão é avaliada a tooundefined valor.  
  
-   `unary_operator <scalar_expression>`  
  
     Representa um operador que é aplicada tooa valor único. Consulte a seção [Operadores](#bk_operators) para obter detalhes.  
  
-   `<scalar_expression> binary_operator <scalar_expression>`  
  
     Representa um operador que é aplicada tootwo valores. Consulte a seção [Operadores](#bk_operators) para obter detalhes.  
  
-   `<scalar_function_expression>`  
  
     Representa um valor definido por um resultado de uma chamada de função.  
  
-   `udf_scalar_function`  
  
     Função escalar definida pelo nome de usuário de saudação.  
  
-   `builtin_scalar_function`  
  
     Nome de função escalar interna de saudação.  
  
-   `<create_object_expression>`  
  
     Representa um valor obtido pela criação de um novo objeto com propriedades especificadas e seus valores.  
  
-   `<create_array_expression>`  
  
     Representa um valor obtido pela criação de uma nova matriz com valores especificados como elementos  
  
-   `parameter_name`  
  
     Representa um valor de nome de parâmetro especificado hello. Nomes de parâmetro devem ter uma única @ como primeiro caractere do hello.  
  
 **Comentários**  
  
 Ao chamar uma função escalar interna ou definida pelo usuário, todos os argumentos deverão ser definidos. Se qualquer um dos argumentos de saudação é indefinido, não será chamada de função hello e Olá resultado será indefinido.  
  
 Ao criar um objeto, qualquer propriedade que é atribuída um valor indefinido será ignorada e não incluída no hello criado o objeto.  
  
 Quando a criação de uma matriz, qualquer valor do elemento que é atribuído **indefinido** valor será ignorado e não está incluído no objeto de saudação criado. Isso fará com que Olá lado definido pelo elemento tootake seu local de forma que matriz Olá criado será não terá os índices ignorados.  
  
##  <a name="bk_operators"></a> Operadores  
 Esta seção descreve os operadores de saudação com suporte. Cada operador pode ser atribuído tooexactly uma categoria.  
  
 Consulte a tabela **Categorias de operador** abaixo para obter detalhes sobre o tratamento de valores **indefinidos**, requisitos de tipo para valores de entrada e tratamento de valores com tipos não correspondentes.  
  
 **Categorias de operador:**  
  
|**Categoria**|**Detalhes**|  
|-|-|  
|**aritmético**|Operador espera entradas toobe número (s). A saída também é um número. Se qualquer uma das entradas de saudação for **indefinido** ou tipo diferente de resultado de número, Olá **indefinido**.|  
|**bit a bit**|Operador espera entradas inteiro assinado de 32 bits de toobe número (s). A saída também é um número inteiro com sinal de 32 bits.<br /><br /> Os valores não inteiros serão arredondados. Os valores positivos serão arredondados para baixo; os valores negativos, arredondados para cima.<br /><br /> Qualquer valor que está fora do intervalo de inteiros de 32 bits do hello será convertido, colocando os últimos 32 bits de notação de complemento de dois.<br /><br /> Se qualquer uma das entradas de saudação for **indefinido** ou tipo diferente de número, a saudação resultado será **indefinido**.<br /><br /> **Observação:** Olá acima comportamento é compatível com o comportamento do operador bit a bit de JavaScript.|  
|**lógico**|Operador espera entradas toobe Boolianas. A saída também é um valor booliano.<br />Se qualquer uma das entradas de saudação for **indefinido** ou tipo diferente de booliano, a saudação resultado será **indefinido**.|  
|**comparação**|Operador espera entradas toohave Olá mesmo tipo e não ser indefinido. A saída é um valor booliano.<br /><br /> Se qualquer uma das entradas de saudação for **indefinido** ou Olá entradas tiverem tipos diferentes, é o resultado de saudação **indefinido**.<br /><br /> Consulte a tabela **Ordenação dos valores para comparação** para ver detalhes da ordem dos valores.|  
|**string**|Operador espera entradas toobe cadeias de caracteres. A saída também é uma cadeia de caracteres.<br />Se qualquer uma das entradas de saudação for **indefinido** ou tipo diferente de resultado de cadeia de caracteres, em seguida, Olá **indefinido**.|  
  
 **Operadores unários:**  
  
|**Nome**|**Operador**|**Detalhes**|  
|-|-|-|  
|**aritmético**|+<br /><br /> -|Retorna um valor numérico hello.<br /><br /> Negação bit a bit. Retorna o valor do número negado.|  
|**bit a bit**|~|Complemento de um. Retorna um complemento de um valor numérico.|  
|**Lógico**|**NOT**|Negação. Retorna o valor booliano negado.|  
  
 **Operadores binários:**  
  
|**Nome**|**Operador**|**Detalhes**|  
|-|-|-|  
|**aritmético**|+<br /><br /> -<br /><br /> *<br /><br /> /<br /><br /> %|Adição.<br /><br /> Subtração.<br /><br /> Multiplicação.<br /><br /> Divisão.<br /><br /> Modulação.|  
|**bit a bit**|&#124;<br /><br /> &<br /><br /> ^<br /><br /> <<<br /><br /> >><br /><br /> >>>|OR bit a bit.<br /><br /> AND bit a bit.<br /><br /> XOR bit a bit.<br /><br /> Deslocamento para a esquerda.<br /><br /> Deslocamento para a direita.<br /><br /> Deslocamento à direita com preenchimento com zero.|  
|**lógico**|**AND**<br /><br /> **OR**|Conjunção lógica. Retorna **true** se os dois argumentos forem **true**; do contrário, retorna **false**.<br /><br /> Conjunção lógica. Retorna **true** se os dois argumentos forem **true**; do contrário, retorna **false**.|  
|**comparação**|**=**<br /><br /> **!=, <>**<br /><br /> **>**<br /><br /> **>=**<br /><br /> **<**<br /><br /> **<=**<br /><br /> **??**|Igual a. Retorna **true** se os argumentos forem iguais; do contrário, retorna **false**.<br /><br /> Não igual a. Retorna **true** se os argumentos não forem iguais; do contrário, retorna **false**.<br /><br /> Maior que. Retorna **true** se o primeiro argumento for maior do que Olá segundo, retornar **false** caso contrário.<br /><br /> Maior ou igual a. Retorna **true** retornar se o primeiro argumento for maior que ou igual a segunda toohello, **false** caso contrário.<br /><br /> Menor que. Retorna **true** se o primeiro argumento é menor que o hello segundo, retornar **false** caso contrário.<br /><br /> Menor ou igual a. Retorna **true** se o primeiro argumento é menor ou igual toohello segundo um retorno **false** caso contrário.<br /><br /> Coalesce. Retorna Olá segundo argumento se Olá primeiro argumento for um **indefinido** valor.|  
|**Cadeia de caracteres**|**&#124;&#124;**|Concatenação. Retorna uma concatenação dos dois argumentos.|  
  
 **Operadores ternários:**  
  
|Operador ternário|?|Retorna Olá segundo argumento se Olá primeiro argumento for avaliado muito**true**; retorna o terceiro argumento de saudação caso contrário.|  
|-|-|-|  
  
 **Ordenação dos valores para comparação**  
  
|**Tipo**|**Ordem de valores**|  
|-|-|  
|**Indefinido**|Não é comparável.|  
|**Nulo**|Valor único: **nulo**|  
|**Número**|Número real natural.<br /><br /> O valor infinito negativo é menor do que qualquer outro valor numérico.<br /><br /> Um valor infinito positivo é maior do que qualquer outro valor numérico. O valor **NaN** não é comparável. A comparação com **NaN** resultará em um valor **indefinido**.|  
|**Cadeia de caracteres**|Ordem lexicográfica.|  
|**Matriz**|Nenhuma ordem, mas justa.|  
|**Objeto**|Nenhuma ordem, mas justa.|  
  
 **Comentários**  
  
 No banco de dados do Azure Cosmos, tipos de saudação de valores geralmente não são conhecidos até que eles sejam realmente recuperados do banco de dados de saudação. Em ordem toosupport uma execução eficiente de consultas, a maioria dos operadores de saudação tiver requisitos de tipo estrito. Além disso, os operadores por si só não executam conversões implícitas.  
  
 Isso significa que uma consulta como: selecione * FROM ROOT r WHERE age = 21 retornará apenas documentos com a propriedade número de toohello igual idade 21. Documentos com a cadeia de caracteres de propriedade Age igual toohello "21" ou cadeia de caracteres hello "0021" não corresponderão, como expressão hello "21" = 21 é avaliada tooundefined. Isso permite um melhor uso de índices, pois a pesquisa Olá de um valor específico (por exemplo, número 21) é mais rápido que a pesquisa por um número indefinido de possíveis correspondências (ou seja, número 21 ou cadeias de caracteres "21", "021", "21.0"...). Isso é diferente de como o JavaScript avalia os operadores em relação a valores de tipos diferentes.  
  
 **Comparação e igualdade de objetos e matrizes**  
  
 A comparação de valores de objeto ou matriz usando os operadores de intervalo (>, >=, <, <=) resulta em indefinido, pois não tem ordem definida nos valores de objeto ou matriz. No entanto, o uso de operadores de igualdade/desigualdade (=,! =, <>) tem suporte e os valores são comparados estruturalmente.  
  
 As matrizes são iguais se as duas matrizes têm o mesmo número de elementos e os elementos em posições de correspondência também são iguais. Se comparar qualquer par de elementos resulta em indefinido, o resultado de saudação de comparação de matriz é indefinido.  
  
 Os objetos são iguais se os dois objetos têm as mesmas propriedades definidas e se os valores das propriedades correspondentes também são iguais. Se comparar qualquer par de valores de propriedade resulta em indefinido, o resultado de saudação de comparação de objeto será indefinido.  
  
##  <a name="bk_constants"></a> Constantes  
 Uma constante, também conhecida como valor literal ou escalar, é um símbolo que representa um valor de dados específico. formato de saudação de uma constante depende de tipo de dados de saudação do valor de saudação representa.  
  
 **Suporte para tipos de dados escalares:**  
  
|**Tipo**|**Ordem de valores**|  
|-|-|  
|**Indefinido**|Valor único: **indefinido**|  
|**Nulo**|Valor único: **nulo**|  
|**Booliano**|Valores: **falso**, **verdadeiro**.|  
|**Número**|Um número de ponto flutuante de precisão dupla, padrão IEEE 754.|  
|**Cadeia de caracteres**|Uma sequência de zero ou mais caracteres Unicode. As cadeias de caracteres devem ser colocadas entre aspas simples ou duplas.|  
|**Matriz**|Uma sequência de zero ou mais elementos. Cada elemento pode ser um valor de qualquer tipo de dados escalares, exceto Indefinido.|  
|**Objeto**|Um conjunto ordenado de zero ou mais pares de nome/valor. Nome é uma cadeia de caracteres Unicode; o valor pode ser de qualquer tipo de dados escalares, exceto **Indefinido**.|  
  
 **Sintaxe**  
  
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
  
 **Argumentos**  
  
1.  `<undefined_constant>; undefined`  
  
     Representa o valor indefinido do tipo Indefinido.  
  
2.  `<null_constant>; null`  
  
     Representa o valor **null** do tipo **Nulo**.  
  
3.  `<boolean_constant>`  
  
     Representa a constante do tipo booliano.  
  
4.  `false`  
  
     Representa o valor **false** do tipo booliano.  
  
5.  `true`  
  
     Representa o valor **true** do tipo booliano.  
  
6.  `<number_constant>`  
  
     Representa uma constante.  
  
7.  `decimal_literal`  
  
     Os literais decimais são números representados usando notação decimal ou notação científica.  
  
8.  `hexadecimal_literal`  
  
     Os literais hexadecimais são números representados usando o prefixo '0x' seguido por um ou mais dígitos hexadecimais.  
  
9. `<string_constant>`  
  
     Representa uma constante do tipo Cadeia de caracteres.  
  
10. `string _literal`  
  
     Literais de cadeia de caracteres são cadeias de caracteres Unicode representadas por uma sequência de zero ou mais caracteres Unicode ou sequências de escape. As literais de cadeia de caracteres são colocadas entre aspas simples (apóstrofe: ') ou aspas duplas (aspas: ").  
  
 As seguintes sequências de escape são permitidas:  
  
|**Sequência de escape**|**Descrição**|**Caractere Unicode**|  
|-|-|-|  
|\\'|apóstrofo (')|U+0027|  
|\\"|aspas (")|U+0022|  
|\\\|barra invertida (\\)|U+005C|  
|\\/|barra (/)|U+002F|  
|\b|backspace|U+0008|  
|\f|avanço de página|U+000C|  
|\n|alimentação de linha|U+000A|  
|\r|retorno de carro|U+000D|  
|\t|tab|U+0009|  
|\uXXXX|Um caractere Unicode definido por 4 dígitos hexadecimais.|U+XXXX|  
  
##  <a name="bk_query_perf_guidelines"></a>Diretrizes de desempenho de consulta  
 Para um toobe consulta executada com eficiência para uma grande coleção, ele deve usar filtros que podem ser atendidos por meio de um ou mais índices.  
  
 Olá filtros a seguir será considerado para o índice de pesquisa:  
  
-   Use o operador de igualdade (=) com uma expressão de caminho de documento e uma constante.  
  
-   Use o operador de intervalo (<, \<=, >, >=) com uma expressão de caminho de documento e constantes numéricas.  
  
-   Expressão de caminho de documento significa qualquer expressão que identifica um caminho constante nos documentos de saudação da coleção de banco de dados de saudação referenciada.  
  
 **Expressão de caminho de documento**  
  
 Expressões de caminho de documento são expressões que um caminho de propriedade ou um indexador de matriz avalia em um documento proveniente dos documentos da coleção do banco de dados. Esse caminho pode ser usado tooidentify Olá local de valores referenciados em um filtro diretamente dentro de documentos de saudação na coleção de banco de dados de saudação.  
  
 Para um toobe expressão considerada uma expressão de caminho de documento, ele deve:  
  
1.  Diretamente raiz da referência Olá coleção.  
  
2.  Fazer referência ao indexador de matriz da constante ou à propriedade de alguma expressão de caminho de documento  
  
3.  Fazer referência a um alias que represente alguma expressão de caminho de documento.  
  
     **Convenções de sintaxe**  
  
     Olá, a tabela a seguir descreve Olá convenções usadas toodescribe sintaxe na referência de linguagem de consulta do DocumentDB API hello.  
  
    |**Convenção**|**Usadas para**|  
    |-|-|    
    |LETRAS MAIÚSCULAS|Palavras-chave não diferenciam maiúsculas de minúsculas.|  
    |letras minúsculas|Palavras-chave diferenciam maiúsculas de minúsculas.|  
    |\<não terminal>|Não terminal, definido separadamente.|  
    |\<não terminal> ::=|Definição de sintaxe do não terminal de saudação.|  
    |other_terminal|Terminal (token), descritos em detalhes em palavras.|  
    |identificador|Identificador. Permite apenas os seguintes caracteres: a-z A-Z 0-9 _O primeiro caractere não pode ser um dígito.|  
    |“cadeia de caracteres”|Cadeia de caracteres entre aspas. Permite qualquer cadeia de caracteres válida. Consulte a descrição de um string_literal.|  
    |'símbolo'|Símbolo literal que faz parte da sintaxe de saudação.|  
    |&#124; (barra vertical)|Alternativas para itens de sintaxe. Você pode usar apenas um dos itens de saudação especificados.|  
    |[ ] /(colchetes)|Os colchetes colocam um ou mais itens opcionais.|  
    |[ ,...n ]|Indica a saudação precede item pode ser repetido n número de vezes. Olá ocorrências são separadas por vírgulas.|  
    |[ ...n ]|Indica a saudação precede item pode ser repetido n número de vezes. Olá ocorrências são separadas por espaços em branco.|  
  
##  <a name="bk_built_in_functions"></a> Funções internas  
 O BD Cosmos do Azure fornece muitas funções SQL internas. categorias de saudação de funções internas estão listadas abaixo.  
  
|Função|Descrição|  
|--------------|-----------------|  
|[Funções matemáticas](#bk_mathematical_functions)|Olá funções matemáticas executam um cálculo, normalmente com base em valores de entrada que são fornecidos como argumentos e retornam um valor numérico.|  
|[Funções de verificação de tipo](#bk_type_checking_functions)|funções de verificação de tipo Hello permitem tipo de saudação toocheck de uma expressão em consultas SQL.|  
|[Funções de cadeia de caracteres](#bk_string_functions)|funções de cadeia de caracteres de saudação executam uma operação em um valor de cadeia de caracteres de entrada e retornam uma cadeia de caracteres, o valor numérico ou booleano.|  
|[Funções de matriz](#bk_array_functions)|funções de matriz Olá executam uma operação em um valor de entrada de matriz e numérico de retorno, um valor booleano ou de matriz.|  
|[Funções espaciais](#bk_spatial_functions)|funções espaciais Olá executam uma operação em um valor de entrada do objeto espacial e retornam um valor numérico ou booleano.|  
  
###  <a name="bk_mathematical_functions"></a>Funções matemáticas  
 Olá funções a seguir executam um cálculo, normalmente com base em valores de entrada que são fornecidos como argumentos e retornam um valor numérico.  
  
||||  
|-|-|-|  
|[ABS](#bk_abs)|[ACOS](#bk_acos)|[ASIN](#bk_asin)|  
|[ATAN](#bk_atan)|[ATN2](#bk_atn2)|[CEILING](#bk_ceiling)|  
|[COS](#bk_cos)|[COT](#bk_cot)|[DEGREES](#bk_degrees)|  
|[EXP](#bk_exp)|[FLOOR](#bk_floor)|[LOG](#bk_log)|  
|[LOG10](#bk_log10)|[PI](#bk_pi)|[POWER](#bk_power)|  
|[RADIANS](#bk_radians)|[ROUND](#bk_round)|[SIN](#bk_sin)|  
|[SQRT](#bk_sqrt)|[SQUARE](#bk_square)|[SIGN](#bk_sign)|  
|[TAN](#bk_tan)|[TRUNC](#bk_trunc)||  
  
####  <a name="bk_abs"></a> ABS  
 Retorna Olá valor absoluto (positivo) da saudação especificado expressão numérica.  
  
 **Sintaxe**  
  
```  
ABS (<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     É uma expressão numérica.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão numérica.  
  
 **Exemplos**  
  
 Hello exemplo a seguir mostra os resultados de saudação do usando a função hello ABS em três números diferentes.  
  
```  
SELECT ABS(-1), ABS(0), ABS(1)  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{$1: 1, $2: 0, $3: 1}]  
```  
  
####  <a name="bk_acos"></a> ACOS  
 Ângulo de saudação retorna, em radianos, cujo cosseno é Olá expressão numérica especificada; também chamado de arco cosseno.  
  
 **Sintaxe**  
  
```  
ACOS(<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     É uma expressão numérica.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão numérica.  
  
 **Exemplos**  
  
 Olá, exemplo a seguir retorna Olá ACOS de -1.  
  
```  
SELECT ACOS(-1)  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <a name="bk_asin"></a> ASIN  
 Ângulo de saudação retorna, em radianos, cujo seno é hello especificado expressão numérica. Isso também é chamado de arco seno.  
  
 **Sintaxe**  
  
```  
ASIN(<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     É uma expressão numérica.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão numérica.  
  
 **Exemplos**  
  
 Olá, exemplo a seguir retorna Olá ASEN de -1.  
  
```  
SELECT ASIN(-1)  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": -1.5707963267948966}]  
```  
  
####  <a name="bk_atan"></a> ATAN  
 Ângulo de saudação retorna, em radianos, cuja tangente é hello especificado expressão numérica. Isso também é chamado de arco tangente.  
  
 **Sintaxe**  
  
```  
ATAN(<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     É uma expressão numérica.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão numérica.  
  
 **Exemplos**  
  
 Olá retorna Olá ATAN de saudação do exemplo a seguir o valor especificado.  
  
```  
SELECT ATAN(-45.01)  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": -1.5485826962062663}]  
```  
  
####  <a name="bk_atn2"></a> ATN2  
 Retorna o valor principal Olá Olá arco tangente de y / x, expressado em radianos.  
  
 **Sintaxe**  
  
```  
ATN2(<numeric_expression>, <numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     É uma expressão numérica.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão numérica.  
  
 **Exemplos**  
  
 Olá, exemplo a seguir calcula hello ATN2 para Olá especificado x e y componentes.  
  
```  
SELECT ATN2(35.175643, 129.44)  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": 1.3054517947300646}]  
```  
  
####  <a name="bk_ceiling"></a> CEILING  
 Retorna Olá menor valor de número inteiro maior ou igual ao Olá expressão numérica especificada.  
  
 **Sintaxe**  
  
```  
CEILING (<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     É uma expressão numérica.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão numérica.  
  
 **Exemplos**  
  
 saudação de exemplo a seguir mostra numéricos positivos, negativos e valores zero com hello função CEILING.  
  
```  
SELECT CEILING(123.45), CEILING(-123.45), CEILING(0.0)  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{$1: 124, $2: -123, $3: 0}]  
```  
  
####  <a name="bk_cos"></a> COS  
 Retorna Olá cosseno trigonométrico Olá especificado o ângulo em radianos, na Olá expressão especificada.  
  
 **Sintaxe**  
  
```  
COS(<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     É uma expressão numérica.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão numérica.  
  
 **Exemplos**  
  
 saudação de exemplo a seguir calcula Olá COS de saudação especificado ângulo.  
  
```  
SELECT COS(14.78)  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": -0.59946542619465426}]  
```  
  
####  <a name="bk_cot"></a> COT  
 Retorna Olá cotangente trigonométrica Olá especificado o ângulo em radianos, Olá especificada expressão numérica.  
  
 **Sintaxe**  
  
```  
COT(<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     É uma expressão numérica.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão numérica.  
  
 **Exemplos**  
  
 saudação de exemplo a seguir calcula Olá COT do ângulo especificado hello.  
  
```  
SELECT COT(124.1332)  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": -0.040311998371148884}]  
```  
  
####  <a name="bk_degrees"></a> DEGREES  
 Retorna Olá ângulo correspondente em graus para um ângulo especificado em radianos.  
  
 **Sintaxe**  
  
```  
DEGREES (<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     É uma expressão numérica.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão numérica.  
  
 **Exemplos**  
  
 Olá exemplo a seguir retorna Olá número de graus em um ângulo de PI/2 radianos.  
  
```  
SELECT DEGREES(PI()/2)  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": 90}]  
```  
  
####  <a name="bk_floor"></a> FLOOR  
 Retorna Olá maior inteiro menor ou igual a toohello especificado expressão numérica.  
  
 **Sintaxe**  
  
```  
FLOOR (<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     É uma expressão numérica.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão numérica.  
  
 **Exemplos**  
  
 saudação de exemplo a seguir mostra numéricos positivos, negativos e valores zero com hello função FLOOR.  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR(0.0)  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{$1: 123, $2: -124, $3: 0}]  
```  
  
####  <a name="bk_exp"></a> EXP  
 Retorna um valor Olá exponencial de saudação especificado expressão numérica.  
  
 **Sintaxe**  
  
```  
EXP (<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     É uma expressão numérica.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão numérica.  
  
 **Comentários**  
  
 constante Olá **e** (2,718281...), é Olá base dos logaritmos naturais.  
  
 Olá, expoente de um número é constante Olá **e** gerado toohello potência do número de saudação. Por exemplo, EXP(1.0) = e^1.0 = 2.71828182845905 e EXP(10) = e^10 = 22026.4657948067.  
  
 Olá exponencial do logaritmo natural de saudação de um número é o número de saudação em si: EXP (LOG (n)) = n. E o logaritmo natural de saudação do hello exponencial de um número é o número de saudação em si: LOG (EXP (n)) = n.  
  
 **Exemplos**  
  
 Olá exemplo a seguir declara uma variável e retorna o valor exponencial de saudação da variável especificada da saudação (10).  
  
```  
SELECT EXP(10)  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{$1: 22026.465794806718}]  
```  
  
 Olá exemplo a seguir retorna valor exponencial Olá Olá o logaritmo natural de 20 e o logaritmo natural de saudação do hello exponencial de 20. Como essas funções são funções inversas uma da outra, o valor de retorno Olá com o arredondamento para matemática em ambos os casos é 20 de ponto flutuante.  
  
```  
SELECT EXP(LOG(20)), LOG(EXP(20))  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{$1: 19.999999999999996, $2: 20}]  
```  
  
####  <a name="bk_log"></a> LOG  
 Retorna Olá o logaritmo natural de saudação especificada uma expressão numérica.  
  
 **Sintaxe**  
  
```  
LOG (<numeric_expression> [, <base>])  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     É uma expressão numérica.  
  
-   `base`  
  
     Argumento numérico opcional que define Olá base do logaritmo hello.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão numérica.  
  
 **Comentários**  
  
 Por padrão, o log () retorna o logaritmo natural hello. Você pode alterar a base de saudação do valor de tooanother logaritmo Olá usando o parâmetro opcional de base hello.  
  
 logaritmo natural de saudação é Olá logaritmo toohello base **e**, onde **e** é uma constante too2.718281828 aproximadamente igual a irracional.  
  
 logaritmo natural de saudação do hello exponencial de um número é o número de saudação em si: LOG (EXP (n)) = n. E Olá exponencial do logaritmo natural de saudação de um número é o número de saudação em si: EXP (LOG (n)) = n.  
  
 **Exemplos**  
  
 Olá exemplo a seguir declara uma variável e retorna o valor de logaritmo de saudação da variável especificada da saudação (10).  
  
```  
SELECT LOG(10)  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{$1: 2.3025850929940459}]  
```  
  
 Olá, exemplo a seguir calcula hello LOG para o expoente de saudação de um número.  
  
```  
SELECT EXP(LOG(10))  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{$1: 10.000000000000002}]  
```  
  
####  <a name="bk_log10"></a> LOG10  
 Logaritmo de base 10 de saudação retorna da saudação especificado expressão numérica.  
  
 **Sintaxe**  
  
```  
LOG10 (<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     É uma expressão numérica.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão numérica.  
  
 **Comentários**  
  
 Olá LOG10 e funções de POWER estão inversamente relacionada tooone outro. Por exemplo, 10 ^ LOG10(n) = n.  
  
 **Exemplos**  
  
 Olá exemplo a seguir declara uma variável e retorna Olá LOG10 valor da variável especificada da saudação (100).  
  
```  
SELECT LOG10(100)  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{$1: 2}]  
```  
  
####  <a name="bk_pi"></a> PI  
 Retorna Olá valor constante de PI.  
  
 **Sintaxe**  
  
```  
PI ()  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     É uma expressão numérica.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão numérica.  
  
 **Exemplos**  
  
 Olá, exemplo a seguir retorna Olá valor de PI.  
  
```  
SELECT PI()  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": 3.1415926535897931}]  
```  
  
####  <a name="bk_power"></a> POWER  
 Retorna Olá Olá especificado valor toohello da expressão especificada de energia.  
  
 **Sintaxe**  
  
```  
POWER (<numeric_expression>, <y>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     É uma expressão numérica.  
  
-   `y`  
  
     É Olá power toowhich tooraise `numeric_expression`.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão numérica.  
  
 **Exemplos**  
  
 saudação de exemplo a seguir demonstra como elevar uma potência de toohello número de 3 (Olá cubo do número de saudação).  
  
```  
SELECT POWER(2, 3), POWER(2.5, 3)  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{$1: 8, $2: 15.625}]  
```  
  
####  <a name="bk_radians"></a> RADIANS  
 Retorna radianos quando uma expressão numérica é inserida em graus.  
  
 **Sintaxe**  
  
```  
RADIANS (<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     É uma expressão numérica.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão numérica.  
  
 **Exemplos**  
  
 Olá exemplo a seguir usa alguns ângulos como entrada e retorna seus valores radianos correspondentes.  
  
```  
SELECT RADIANS(-45.01), RADIANS(-181.01), RADIANS(0), RADIANS(0.1472738), RADIANS(197.1099392)  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{  
       "$1": -0.7855726963226477,  
       "$2": -3.1592204790349356,  
       "$3": 0,  
       "$4": 0.0025704127119236249,  
       "$5": 3.4402174274458375  
   }]  
```  
  
####  <a name="bk_round"></a> ROUND  
 Retorna um valor numérico, arredondado toohello valor de inteiro mais próximo.  
  
 **Sintaxe**  
  
```  
ROUND(<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     É uma expressão numérica.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão numérica.  
  
 **Exemplos**  
  
 Olá, exemplo a seguir Arredonda Olá seguintes números positivos e negativos toohello inteiro mais próximo.  
  
```  
SELECT ROUND(2.4), ROUND(2.6), ROUND(2.5), ROUND(-2.4), ROUND(-2.6)  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{$1: 2, $2: 3, $3: 3, $4: -2, $5: -3}]  
```  
  
####  <a name="bk_sign"></a> SIGN  
 Retorna Olá positivo (+ 1), zero (0), ou sinal de negativo (-1) de saudação especificado expressão numérica.  
  
 **Sintaxe**  
  
```  
SIGN(<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     É uma expressão numérica.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão numérica.  
  
 **Exemplos**  
  
 Olá exemplo a seguir retorna valores de entrada hello de números de too2-2.  
  
```  
SELECT SIGN(-2), SIGN(-1), SIGN(0), SIGN(1), SIGN(2)  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{$1: -1, $2: -1, $3: 0, $4: 1, $5: 1}]  
```  
  
####  <a name="bk_sin"></a> SIN  
 Retorna Olá seno trigonométrico Olá especificado o ângulo em radianos, na Olá expressão especificada.  
  
 **Sintaxe**  
  
```  
SIN(<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     É uma expressão numérica.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão numérica.  
  
 **Exemplos**  
  
 saudação de exemplo a seguir calcula Olá sen do ângulo especificado hello.  
  
```  
SELECT SIN(45.175643)  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": 0.929607286611012}]  
```  
  
####  <a name="bk_sqrt"></a> SQRT  
 Retorna Olá quadrado raiz de saudação especificado valor numérico.  
  
 **Sintaxe**  
  
```  
SQRT(<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     É uma expressão numérica.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão numérica.  
  
 **Exemplos**  
  
 Olá, exemplo a seguir retorna raízes quadradas de saudação de números de 1 a 3.  
  
```  
SELECT SQRT(1), SQRT(2.0), SQRT(3)  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{$1: 1, $2: 1.4142135623730952, $3: 1.7320508075688772}]  
```  
  
####  <a name="bk_square"></a> SQUARE  
 Saudação de retorna quadrada de saudação especificado valor numérico.  
  
 **Sintaxe**  
  
```  
SQUARE(<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     É uma expressão numérica.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão numérica.  
  
 **Exemplos**  
  
 Olá, exemplo a seguir retorna quadrados Olá dos números de 1 a 3.  
  
```  
SELECT SQUARE(1), SQUARE(2.0), SQUARE(3)  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{$1: 1, $2: 4, $3: 9}]  
```  
  
####  <a name="bk_tan"></a> TAN  
 Tangente de saudação retorna da saudação especificado o ângulo em radianos, na Olá expressão especificada.  
  
 **Sintaxe**  
  
```  
TAN (<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     É uma expressão numérica.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão numérica.  
  
 **Exemplos**  
  
 Olá, exemplo a seguir calcula a tangente Olá de PI () / 2.  
  
```  
SELECT TAN(PI()/2);  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": 16331239353195370 }]  
```  
  
####  <a name="bk_trunc"></a>TRUNC  
 Retorna um valor numérico, o valor inteiro mais próximo de toohello truncados.  
  
 **Sintaxe**  
  
```  
TRUNC(<numeric_expression>)  
```  
  
 **Argumentos**  
  
-   `numeric_expression`  
  
     É uma expressão numérica.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão numérica.  
  
 **Exemplos**  
  
 saudação de exemplo a seguir trunca Olá seguintes números positivos e negativos toohello valor inteiro mais próximo.  
  
```  
SELECT TRUNC(2.4), TRUNC(2.6), TRUNC(2.5), TRUNC(-2.4), TRUNC(-2.6)  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{$1: 2, $2: 2, $3: 2, $4: -2, $5: -2}]  
```  
  
###  <a name="bk_type_checking_functions"></a> Funções de verificação de tipo  
 Olá funções a seguir oferece suporte ao tipo verificando em relação aos valores de entrada e retornam um valor booleano.  
  
||||  
|-|-|-|  
|[IS_ARRAY](#bk_is_array)|[IS_BOOL](#bk_is_bool)|[IS_DEFINED](#bk_is_defined)|  
|[IS_NULL](#bk_is_null)|[IS_NUMBER](#bk_is_number)|[IS_OBJECT](#bk_is_object)|  
|[IS_PRIMITIVE](#bk_is_primitive)|[IS_STRING](#bk_is_string)||  
  
####  <a name="bk_is_array"></a>IS_ARRAY  
 Retorna um valor booliano que indica se o tipo de saudação de saudação especificado expressão é uma matriz.  
  
 **Sintaxe**  
  
```  
IS_ARRAY(<expression>)  
```  
  
 **Argumentos**  
  
-   `expression`  
  
     É qualquer expressão válida.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão booliana.  
  
 **Exemplos**  
  
 Olá exemplo a seguir verifica objetos JSON booliano, número, cadeia de caracteres, nula, objeto, matriz e tipos indefinidos usando Olá função IS_ARRAY.  
  
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
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: false, $6: true}]  
```  
  
####  <a name="bk_is_bool"></a>IS_BOOL  
 Retorna um valor booliano que indica se o tipo de saudação de saudação especificado expressão é um valor booleano.  
  
 **Sintaxe**  
  
```  
IS_BOOL(<expression>)  
```  
  
 **Argumentos**  
  
-   `expression`  
  
     É qualquer expressão válida.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão booliana.  
  
 **Exemplos**  
  
 Olá exemplo a seguir verifica objetos JSON booliano, número, cadeia de caracteres, nula, objeto, matriz e tipos indefinidos usando Olá função IS_BOOL.  
  
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
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{$1: true, $2: false, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_defined"></a>IS_DEFINED  
 Retorna um valor booleano que indica se a propriedade de saudação foi atribuída um valor.  
  
 **Sintaxe**  
  
```  
IS_DEFINED(<expression>)  
```  
  
 **Argumentos**  
  
-   `expression`  
  
     É qualquer expressão válida.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão booliana.  
  
 **Exemplos**  
  
 Olá seguindo o exemplo verifica a presença de saudação de uma propriedade dentro de saudação especificado documento JSON. Olá primeiro retorna true, porque "a" está presente, mas Olá segundo retorna false, porque "b" está ausente.  
  
```  
SELECT IS_DEFINED({ "a" : 5 }.a), IS_DEFINED({ "a" : 5 }.b)  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{  
       "$1": true,    
       "$2": false   
   }]  
```  
  
####  <a name="bk_is_null"></a>IS_NULL  
 Retorna um valor booliano que indica se o tipo de saudação de saudação especificado expressão é nulo.  
  
 **Sintaxe**  
  
```  
IS_NULL(<expression>)  
```  
  
 **Argumentos**  
  
-   `expression`  
  
     É qualquer expressão válida.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão booliana.  
  
 **Exemplos**  
  
 Olá exemplo a seguir verifica objetos JSON booliano, número, cadeia de caracteres, nula, objeto, matriz e tipos indefinidos usando Olá função IS_NULL.  
  
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
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{$1: false, $2: false, $3: false, $4: true, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_number"></a>IS_NUMBER  
 Retorna um valor booliano que indica se o tipo de saudação de saudação especificado expressão é um número.  
  
 **Sintaxe**  
  
```  
IS_NUMBER(<expression>)  
```  
  
 **Argumentos**  
  
-   `expression`  
  
     É qualquer expressão válida.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão booliana.  
  
 **Exemplos**  
  
 Olá exemplo a seguir verifica objetos JSON booliano, número, cadeia de caracteres, nula, objeto, matriz e tipos indefinidos usando Olá função IS_NULL.  
  
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
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{$1: false, $2: true, $3: false, $4: false, $5: false, $6: false}]  
```  
  
####  <a name="bk_is_object"></a>IS_OBJECT  
 Retorna um valor booliano que indica se o tipo de saudação de saudação especificado expressão é um objeto JSON.  
  
 **Sintaxe**  
  
```  
IS_OBJECT(<expression>)  
```  
  
 **Argumentos**  
  
-   `expression`  
  
     É qualquer expressão válida.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão booliana.  
  
 **Exemplos**  
  
 Olá exemplo a seguir verifica objetos JSON booliano, número, cadeia de caracteres, nula, objeto, matriz e tipos indefinidos usando Olá função IS_OBJECT.  
  
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
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{$1: false, $2: false, $3: false, $4: false, $5: true, $6: false}]  
```  
  
####  <a name="bk_is_primitive"></a>IS_PRIMITIVE  
 Retorna um valor booliano que indica se o tipo de saudação do hello especificado de expressão é um primitivo (cadeia de caracteres, booleano, numérico ou nulo).  
  
 **Sintaxe**  
  
```  
IS_PRIMITIVE(<expression>)  
```  
  
 **Argumentos**  
  
-   `expression`  
  
     É qualquer expressão válida.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão booliana.  
  
 **Exemplos**  
  
 Olá exemplo a seguir verifica objetos JSON booliano, número, cadeia de caracteres, nula, objeto, matriz e tipos indefinidos usando Olá função IS_PRIMITIVE.  
  
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
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": true, "$2": true, "$3": true, "$4": true, "$5": false, "$6": false, "$7": false}]  
```  
  
####  <a name="bk_is_string"></a> IS_STRING  
 Retorna um valor booliano que indica se o tipo de saudação de saudação especificado expressão é uma cadeia de caracteres.  
  
 **Sintaxe**  
  
```  
IS_STRING(<expression>)  
```  
  
 **Argumentos**  
  
-   `expression`  
  
     É qualquer expressão válida.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão booliana.  
  
 **Exemplos**  
  
 Olá exemplo a seguir verifica objetos JSON booliano, número, cadeia de caracteres, nula, objeto, matriz e tipos indefinidos usando Olá função IS_STRING.  
  
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
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{$1: false, $2: false, $3: true, $4: false, $5: false, $6: false}]  
```  
  
###  <a name="bk_string_functions"></a> Funções de cadeia de caracteres  
 Olá funções escalares a seguir executam uma operação em um valor de cadeia de caracteres de entrada e retornam uma cadeia de caracteres, o valor numérico ou booleano.  
  
||||  
|-|-|-|  
|[CONCAT](#bk_concat)|[CONTAINS](#bk_contains)|[ENDSWITH](#bk_endswith)|  
|[INDEX_OF](#bk_index_of)|[LEFT](#bk_left)|[COMPRIMENTO](#bk_length)|  
|[LOWER](#bk_lower)|[LTRIM](#bk_ltrim)|[REPLACE](#bk_replace)|  
|[REPLICATE](#bk_replicate)|[REVERSE](#bk_reverse)|[RIGHT](#bk_right)|  
|[RTRIM](#bk_rtrim)|[STARTSWITH](#bk_startswith)|[SUBSTRING](#bk_substring)|  
|[UPPER](#bk_upper)|||  
  
####  <a name="bk_concat"></a> CONCAT  
 Retorna uma cadeia de caracteres que é o resultado de saudação da concatenação de dois ou mais valores de cadeia de caracteres.  
  
 **Sintaxe**  
  
```  
CONCAT(<str_expr>, <str_expr> [, <str_expr>])  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     É qualquer expressão de cadeia de caracteres válida.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão de cadeia de caracteres.  
  
 **Exemplos**  
  
 Olá Olá concatenado exemplo retorna cadeia de caracteres de saudação a seguir valores especificados.  
  
```  
SELECT CONCAT("abc", "def")  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": "abcdef"}  
```  
  
####  <a name="bk_contains"></a> CONTAINS  
 Retorna um valor booleano que indica se a primeira expressão de cadeia de caracteres hello contém Olá segundo.  
  
 **Sintaxe**  
  
```  
CONTAINS(<str_expr>, <str_expr>)  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     É qualquer expressão de cadeia de caracteres válida.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão booliana.  
  
 **Exemplos**  
  
 Olá exemplo a seguir verifica se "abc" contém "ab" e contém "d".  
  
```  
SELECT CONTAINS("abc", "ab"), CONTAINS("abc", "d")  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <a name="bk_endswith"></a> ENDSWITH  
 Retorna um valor booleano que indica se primeira expressão de cadeia de caracteres hello termina com hello segundo.  
  
 **Sintaxe**  
  
```  
ENDSWITH(<str_expr>, <str_expr>)  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     É qualquer expressão de cadeia de caracteres válida.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão booliana.  
  
 **Exemplos**  
  
 Olá, exemplo a seguir retorna hello "abc" termina com "b" e "bc".  
  
```  
SELECT ENDSWITH("abc", "b"), ENDSWITH("abc", "bc")  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <a name="bk_index_of"></a>INDEX_OF  
 Retorna a saudação iniciando a posição da primeira ocorrência de saudação da segunda expressão de cadeia de caracteres hello na primeira expressão de cadeia de caracteres especificada hello, ou -1 se a cadeia de caracteres de saudação não foi encontrada.  
  
 **Sintaxe**  
  
```  
INDEX_OF(<str_expr>, <str_expr>)  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     É qualquer expressão de cadeia de caracteres válida.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão numérica.  
  
 **Exemplos**  
  
 Olá exemplo a seguir retorna o índice de saudação de diversas subcadeias de caracteres dentro de "abc".  
  
```  
SELECT INDEX_OF("abc", "ab"), INDEX_OF("abc", "b"), INDEX_OF("abc", "c")  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": 0, "$2": 1, "$3": -1}]  
```  
  
####  <a name="bk_left"></a> ESQUERDA  
 Retorna Olá parte esquerda de uma cadeia de caracteres com hello especificado número de caracteres.  
  
 **Sintaxe**  
  
```  
LEFT(<str_expr>, <num_expr>)  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     É qualquer expressão de cadeia de caracteres válida.  
  
-   `num_expr`  
  
     É qualquer expressão numérica válida.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão de cadeia de caracteres.  
  
 **Exemplos**  
  
 Olá, exemplo a seguir retorna Olá esquerda a parte de "abc" para vários valores de comprimento.  
  
```  
SELECT LEFT("abc", 1), LEFT("abc", 2)  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": "ab", "$2": "ab"}]  
```  
  
####  <a name="bk_length"></a> COMPRIMENTO  
 Retorna o número de saudação de caracteres da saudação especificado expressão de cadeia de caracteres.  
  
 **Sintaxe**  
  
```  
LENGTH(<str_expr>)  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     É qualquer expressão de cadeia de caracteres válida.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão de cadeia de caracteres.  
  
 **Exemplos**  
  
 Olá, exemplo a seguir retorna Olá comprimento de uma cadeia de caracteres.  
  
```  
SELECT LENGTH("abc")  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": 3}]  
```  
  
####  <a name="bk_lower"></a> LOWER  
 Retorna uma expressão de cadeia de caracteres após converter caracteres maiusculos toolowercase de dados.  
  
 **Sintaxe**  
  
```  
LOWER(<str_expr>)  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     É qualquer expressão de cadeia de caracteres válida.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão de cadeia de caracteres.  
  
 **Exemplos**  
  
 Olá mostrado no exemplo a seguir como toouse inferior em uma consulta.  
  
```  
SELECT LOWER("Abc")  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": "abc"}]  
  
```  
  
####  <a name="bk_ltrim"></a> LTRIM  
 Retorna uma expressão de cadeia de caracteres após remover os espaços em branco iniciais.  
  
 **Sintaxe**  
  
```  
LTRIM(<str_expr>)  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     É qualquer expressão de cadeia de caracteres válida.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão de cadeia de caracteres.  
  
 **Exemplos**  
  
 Olá mostrado no exemplo a seguir como toouse LTRIM dentro de uma consulta.  
  
```  
SELECT LTRIM("  abc"), LTRIM("abc"), LTRIM("abc   ")  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": "abc", "$2": "abc", "$3": "abc   "}]  
```  
  
####  <a name="bk_replace"></a> SUBSTITUIR  
 Substitui todas as ocorrências de um valor de cadeia de caracteres especificado por outro valor de cadeia de caracteres.  
  
 **Sintaxe**  
  
```  
REPLACE(<str_expr>, <str_expr>, <str_expr>)  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     É qualquer expressão de cadeia de caracteres válida.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão de cadeia de caracteres.  
  
 **Exemplos**  
  
 saudação de exemplo a seguir mostra como toouse substituir em uma consulta.  
  
```  
SELECT REPLACE("This is a Test", "Test", "desk")  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": "This is a desk"}]  
```  
  
####  <a name="bk_replicate"></a> REPLICATE  
 Repete um valor de cadeia de caracteres por um número de vezes especificado.  
  
 **Sintaxe**  
  
```  
REPLICATE(<str_expr>, <num_expr>)  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     É qualquer expressão de cadeia de caracteres válida.  
  
-   `num_expr`  
  
     É qualquer expressão numérica válida.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão de cadeia de caracteres.  
  
 **Exemplos**  
  
 saudação de exemplo a seguir mostra como toouse REPLICAR em uma consulta.  
  
```  
SELECT REPLICATE("a", 3)  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": "aaa"}]  
```  
  
####  <a name="bk_reverse"></a> REVERSE  
 Retorna a ordem inversa Olá de um valor de cadeia de caracteres.  
  
 **Sintaxe**  
  
```  
REVERSE(<str_expr>)  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     É qualquer expressão de cadeia de caracteres válida.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão de cadeia de caracteres.  
  
 **Exemplos**  
  
 saudação de exemplo a seguir mostra como toouse INVERTER em uma consulta.  
  
```  
SELECT REVERSE("Abc")  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": "cbA"}]  
```  
  
####  <a name="bk_right"></a> RIGHT  
 Olá retorna parte direita de uma cadeia de caracteres com hello número especificado de caracteres.  
  
 **Sintaxe**  
  
```  
RIGHT(<str_expr>, <num_expr>)  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     É qualquer expressão de cadeia de caracteres válida.  
  
-   `num_expr`  
  
     É qualquer expressão numérica válida.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão de cadeia de caracteres.  
  
 **Exemplos**  
  
 Olá, exemplo a seguir retorna Olá parte direita de "abc" para vários valores de comprimento.  
  
```  
SELECT RIGHT("abc", 1), RIGHT("abc", 2)  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": "c", "$2": "bc"}]  
```  
  
####  <a name="bk_rtrim"></a> RTRIM  
 Retorna uma expressão de cadeia de caracteres após remover os espaços em branco finais.  
  
 **Sintaxe**  
  
```  
RTRIM(<str_expr>)  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     É qualquer expressão de cadeia de caracteres válida.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão de cadeia de caracteres.  
  
 **Exemplos**  
  
 Olá mostrado no exemplo a seguir como toouse RTRIM dentro de uma consulta.  
  
```  
SELECT RTRIM("  abc"), RTRIM("abc"), RTRIM("abc   ")  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": "   abc", "$2": "abc", "$3": "abc"}]  
```  
  
####  <a name="bk_startswith"></a> STARTSWITH  
 Retorna um valor booleano que indica se primeira expressão de cadeia de caracteres hello começa com hello segundo.  
  
 **Sintaxe**  
  
```  
STARTSWITH(<str_expr>, <str_expr>)  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     É qualquer expressão de cadeia de caracteres válida.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão booliana.  
  
 **Exemplos**  
  
 Olá exemplo a seguir verifica se hello cadeia de caracteres "abc" começa com "b" e "a".  
  
```  
SELECT STARTSWITH("abc", "b"), STARTSWITH("abc", "a")  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": false, "$2": true}]  
```  
  
####  <a name="bk_substring"></a> SUBSTRING  
 Retorna parte de uma expressão de cadeia de caracteres começando em Olá especificado a posição do caractere com base em zero e continua toohello especificado comprimento ou toohello final da cadeia de caracteres de saudação.  
  
 **Sintaxe**  
  
```  
SUBSTRING(<str_expr>, <num_expr> [, <num_expr>])  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     É qualquer expressão de cadeia de caracteres válida.  
  
-   `num_expr`  
  
     É qualquer expressão numérica válida.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão de cadeia de caracteres.  
  
 **Exemplos**  
  
 Olá exemplo a seguir retorna Olá subcadeia de caracteres de "abc" começando em 1 e por um período de 1 caractere.  
  
```  
SELECT SUBSTRING("abc", 1, 1)  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": "b"}]  
```  
  
####  <a name="bk_upper"></a> UPPER  
 Retorna uma expressão de cadeia de caracteres após converter caracteres minúsculos toouppercase de dados.  
  
 **Sintaxe**  
  
```  
UPPER(<str_expr>)  
```  
  
 **Argumentos**  
  
-   `str_expr`  
  
     É qualquer expressão de cadeia de caracteres válida.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão de cadeia de caracteres.  
  
 **Exemplos**  
  
 Olá mostrado no exemplo a seguir como toouse superior em uma consulta  
  
```  
SELECT UPPER("Abc")  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": "ABC"}]  
```  
  
###  <a name="bk_array_functions"></a> Funções de matriz  
 Olá funções escalares a seguir executam uma operação em um valor de entrada de matriz e retorno numérico, valor booleano ou de matriz  
  
||||  
|-|-|-|  
|[ARRAY_CONCAT](#bk_array_concat)|[ARRAY_CONTAINS](#bk_array_contains)|[ARRAY_LENGTH](#bk_array_length)|  
|[ARRAY_SLICE](#bk_array_slice)|||  
  
####  <a name="bk_array_concat"></a>ARRAY_CONCAT  
 Retorna uma matriz que é o resultado de saudação da concatenação de dois ou mais valores de matriz.  
  
 **Sintaxe**  
  
```  
ARRAY_CONCAT (<arr_expr>, <arr_expr> [, <arr_expr>])  
```  
  
 **Argumentos**  
  
-   `arr_expr`  
  
     É qualquer expressão válida de matriz.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão de matriz.  
  
 **Exemplos**  
  
 Olá como tooconcatenate duas matrizes de exemplo a seguir.  
  
```  
SELECT ARRAY_CONCAT(["apples", "strawberries"], ["bananas"])  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": ["apples", "strawberries", "bananas"]}]  
```  
  
####  <a name="bk_array_contains"></a>ARRAY_CONTAINS  
 Retorna um valor booleano que indica se a matriz de saudação contém Olá valor especificado.  
  
 **Sintaxe**  
  
```  
ARRAY_CONTAINS (<arr_expr>, <expr>)  
```  
  
 **Argumentos**  
  
-   `arr_expr`  
  
     É qualquer expressão válida de matriz.  
  
-   `expr`  
  
     É qualquer expressão válida.  
  
 **Tipos de retorno**  
  
 Retorna um valor booliano.  
  
 **Exemplos**  
  
 saudação de exemplo a seguir como toocheck associação em uma matriz usando ARRAY_CONTAINS.  
  
```  
SELECT   
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "apples"),  
           ARRAY_CONTAINS(["apples", "strawberries", "bananas"], "mangoes")  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": true, "$2": false}]  
```  
  
####  <a name="bk_array_length"></a>ARRAY_LENGTH  
 Retorna o número de saudação de elementos da saudação especificado expressão de matriz.  
  
 **Sintaxe**  
  
```  
ARRAY_LENGTH(<arr_expr>)  
```  
  
 **Argumentos**  
  
-   `arr_expr`  
  
     É qualquer expressão válida de matriz.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão numérica.  
  
 **Exemplos**  
  
 Olá exemplo a seguir como tooget Olá comprimento de uma matriz usando ARRAY_LENGTH.  
  
```  
SELECT ARRAY_LENGTH(["apples", "strawberries", "bananas"])  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{"$1": 3}]  
```  
  
####  <a name="bk_array_slice"></a>ARRAY_SLICE  
 Retorna parte de uma expressão de matriz.
  
 **Sintaxe**  
  
```  
ARRAY_SLICE (<arr_expr>, <num_expr> [, <num_expr>])  
```  
  
 **Argumentos**  
  
-   `arr_expr`  
  
     É qualquer expressão válida de matriz.  
  
-   `num_expr`  
  
     É qualquer expressão numérica válida.  
  
 **Tipos de retorno**  
  
 Retorna um valor booliano.  
  
 **Exemplos**  
  
 saudação de exemplo a seguir como tooget uma parte de uma matriz usando ARRAY_SLICE.  
  
```  
SELECT   
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1),  
           ARRAY_SLICE(["apples", "strawberries", "bananas"], 1, 1)  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{  
           "$1": ["strawberries", "bananas"],   
           "$2": ["strawberries"]  
       }]  
```  
  
###  <a name="bk_spatial_functions"></a> Funções espaciais  
 Olá funções escalares a seguir executam uma operação em um valor de entrada do objeto espacial e retornam um valor numérico ou booleano.  
  
||||  
|-|-|-|  
|[ST_DISTANCE](#bk_st_distance)|[ST_WITHIN](#bk_st_within)|[ST_INTERSECTS](#bk_st_intersects)|[ST_ISVALID](#bk_st_isvalid)|  
|[ST_ISVALIDDETAILED](#bk_st_isvaliddetailed)|||  
  
####  <a name="bk_st_distance"></a> ST_DISTANCE  
 Retorna a distância de saudação entre expressões de LineString, Polygon ou ponto GeoJSON Olá dois.  
  
 **Sintaxe**  
  
```  
ST_DISTANCE (<spatial_expr>, <spatial_expr>)  
```  
  
 **Argumentos**  
  
-   `spatial_expr`  
  
     É qualquer expressão de objeto Ponto GeoJSON, Polígono ou LineString válida.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão numérica que contém a distância de saudação. Isso é expresso em metros para o sistema de referência padrão hello.  
  
 **Exemplos**  
  
 Olá mostrado no exemplo a seguir como tooreturn todos os documentos de família de produtos que estão dentro de 30 km de saudação especificado usando a função interna de ST_DISTANCE de saudação do local. .  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{  
  "id": "WakefieldFamily"  
}]  
```  
  
####  <a name="bk_st_within"></a> ST_WITHIN  
 Retorna uma expressão booleana que indica se Olá GeoJSON o objeto (ponto, polígono ou LineString) especificado no primeiro argumento de saudação está dentro Olá GeoJSON (ponto, polígono ou LineString) no segundo argumento de saudação.  
  
 **Sintaxe**  
  
```  
ST_WITHIN (<spatial_expr>, <spatial_expr>)  
```  
  
 **Argumentos**  
  
-   `spatial_expr`  
  
     É qualquer expressão de objeto Ponto GeoJSON, Polígono ou LineString válida.  
 
-   `spatial_expr`  
  
     É qualquer expressão de objeto Ponto GeoJSON, Polígono ou LineString válida.  
  
 **Tipos de retorno**  
  
 Retorna um valor booliano.  
  
 **Exemplos**  
  
 saudação de exemplo a seguir mostra como toofind família de todos os documentos dentro de um polígono usando ST_WITHIN.  
  
```  
SELECT f.id   
FROM Families f   
WHERE ST_WITHIN(f.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{ "id": "WakefieldFamily" }]  
```  

####  <a name="bk_st_intersects"></a>ST_INTERSECTS  
 Retorna uma expressão booleana que indica se Olá GeoJSON o objeto (ponto, polígono ou LineString) especificado no primeiro argumento de saudação intercepta Olá GeoJSON (ponto, polígono ou LineString) no segundo argumento de saudação.  
  
 **Sintaxe**  
  
```  
ST_INTERSECTS (<spatial_expr>, <spatial_expr>)  
```  
  
 **Argumentos**  
  
-   `spatial_expr`  
  
     É qualquer expressão de objeto Ponto GeoJSON, Polígono ou LineString válida.  
 
-   `spatial_expr`  
  
     É qualquer expressão de objeto Ponto GeoJSON, Polígono ou LineString válida.  
  
 **Tipos de retorno**  
  
 Retorna um valor booliano.  
  
 **Exemplos**  
  
 Olá mostrado no exemplo a seguir como toofind todas as áreas que faz interseção com hello fornecido polígono.  
  
```  
SELECT a.id   
FROM Areas a   
WHERE ST_INTERSECTS(a.location, {  
    'type':'Polygon',   
    'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]  
})  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{ "id": "IntersectingPolygon" }]  
```  
  
####  <a name="bk_st_isvalid"></a> ST_ISVALID  
 Retorna um valor booliano que indica se a saudação especificado LineString, Polygon ou ponto GeoJSON expressão é válida.  
  
 **Sintaxe**  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 **Argumentos**  
  
-   `spatial_expr`  
  
     É qualquer expressão válida de LineString, polígono ou ponto GeoJSON.  
  
 **Tipos de retorno**  
  
 Retorna uma expressão booliana.  
  
 **Exemplos**  
  
 Olá mostrado no exemplo a seguir como toocheck se um ponto é válido usar ST_VALID.  
  
 Por exemplo, esse ponto tem um valor de latitude que não está em um intervalo válido de valores [-90, 90] hello, Olá então consulta retornará false.  
  
 Para polígonos, Olá GeoJSON especificação requer que Olá último par de coordenadas fornecido deve ser Olá mesmo como toocreate primeiro, Olá uma forma fechada. Os pontos em um polígono devem ser especificados no sentido anti-horário. Um polígono especificado na ordem no sentido horário representa inverso de saudação da região hello dentro dele.  
  
```  
SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{ "$1": false }]  
```  
  
####  <a name="bk_st_isvaliddetailed"></a> ST_ISVALIDDETAILED  
 Retorna um valor JSON que contém um valor booliano se Olá especificado expressão LineString, Polygon ou ponto GeoJSON é válido e se for inválido, além disso Olá motivo como um valor de cadeia de caracteres.  
  
 **Sintaxe**  
  
```  
ST_ISVALID(<spatial_expr>)  
```  
  
 **Argumentos**  
  
-   `spatial_expr`  
  
     É qualquer expressão válida de ponto ou polígono GeoJSON.  
  
 **Tipos de retorno**  
  
 Retorna um valor JSON que contém um valor booliano se Olá especificado ponto GeoJSON ou expressão de polígono é válido e se for inválido, além disso Olá motivo como um valor de cadeia de caracteres.  
  
 **Exemplos**  
  
 saudação de exemplo a seguir como toocheck validade (com detalhes) usando ST_ISVALIDDETAILED.  
  
```  
SELECT ST_ISVALIDDETAILED({   
  "type": "Polygon",   
  "coordinates": [[ [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] ]]  
})  
```  
  
 Aqui está o conjunto de resultados de saudação.  
  
```  
[{  
  "$1": {   
    "valid": false,   
    "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a polygon must have hello same start and end points."   
  }  
}]  
```  
  
## <a name="next-steps"></a>Próximas etapas  
 [Sintaxe SQL e consulta SQL para BD Cosmos do Azure](documentdb-sql-query.md)   
 [Documentação do BD Cosmos do Azure](https://docs.microsoft.com/en-us/azure/cosmos-db/)  
  
  
