---
title: Criar chaves substitutas usando IDENTITY | Microsoft Docs
description: Saiba como usar o IDENTITY para criar chaves substitutas em suas tabelas.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/13/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 3ab5d159e6eaeb830135fe134e108b0e4de4b7d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-surrogate-keys-by-using-identity"></a><span data-ttu-id="cb329-103">Criar chaves substitutas usando IDENTITY</span><span class="sxs-lookup"><span data-stu-id="cb329-103">Create surrogate keys by using IDENTITY</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="cb329-104">[Visão geral][Overview]</span><span class="sxs-lookup"><span data-stu-id="cb329-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="cb329-105">[Tipos de dados][Data Types]</span><span class="sxs-lookup"><span data-stu-id="cb329-105">[Data types][Data Types]</span></span>
> * <span data-ttu-id="cb329-106">[Distribuir][Distribute]</span><span class="sxs-lookup"><span data-stu-id="cb329-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="cb329-107">[Índice][Index]</span><span class="sxs-lookup"><span data-stu-id="cb329-107">[Index][Index]</span></span>
> * <span data-ttu-id="cb329-108">[Partição][Partition]</span><span class="sxs-lookup"><span data-stu-id="cb329-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="cb329-109">[Estatísticas][Statistics]</span><span class="sxs-lookup"><span data-stu-id="cb329-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="cb329-110">[Temporário][Temporary]</span><span class="sxs-lookup"><span data-stu-id="cb329-110">[Temporary][Temporary]</span></span>
> * <span data-ttu-id="cb329-111">[Identidade][Identity]</span><span class="sxs-lookup"><span data-stu-id="cb329-111">[Identity][Identity]</span></span>
> 
> 

<span data-ttu-id="cb329-112">Muitos modeladores de dados gostam de criar chaves substitutas em suas tabelas quando criam modelos de data warehouse.</span><span class="sxs-lookup"><span data-stu-id="cb329-112">Many data modelers like to create surrogate keys on their tables when they design data warehouse models.</span></span> <span data-ttu-id="cb329-113">Você pode usar a propriedade IDENTITY para atingir esse objetivo de forma simples e eficiente, sem afetar o desempenho de carga.</span><span class="sxs-lookup"><span data-stu-id="cb329-113">You can use the IDENTITY property to achieve this goal simply and effectively without affecting load performance.</span></span> 

## <a name="get-started-with-identity"></a><span data-ttu-id="cb329-114">Introdução ao IDENTITY</span><span class="sxs-lookup"><span data-stu-id="cb329-114">Get started with IDENTITY</span></span>
<span data-ttu-id="cb329-115">Você pode definir uma tabela como tendo a propriedade IDENTITY quando você cria a tabela pela primeira vez usando uma sintaxe semelhante à instrução a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb329-115">You can define a table as having the IDENTITY property when you first create the table by using syntax that is similar to the following statement:</span></span>

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1) NOT NULL
,   C2 INT NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;
```

<span data-ttu-id="cb329-116">Você pode usar `INSERT..SELECT` para popular a tabela.</span><span class="sxs-lookup"><span data-stu-id="cb329-116">You can then use `INSERT..SELECT` to populate the table.</span></span>

## <a name="behavior"></a><span data-ttu-id="cb329-117">Comportamento</span><span class="sxs-lookup"><span data-stu-id="cb329-117">Behavior</span></span>
<span data-ttu-id="cb329-118">A propriedade IDENTITY foi projetada para expansão em todas as distribuições no data warehouse sem afetar o desempenho de carga.</span><span class="sxs-lookup"><span data-stu-id="cb329-118">The IDENTITY property is designed to scale out across all the distributions in the data warehouse without affecting load performance.</span></span> <span data-ttu-id="cb329-119">Portanto, a implementação de IDENTITY é orientada para atingir esses objetivos.</span><span class="sxs-lookup"><span data-stu-id="cb329-119">Therefore, the implementation of IDENTITY is oriented toward achieving these goals.</span></span> <span data-ttu-id="cb329-120">Esta seção destaca as nuances da implementação para ajudá-lo a entendê-los mais detalhadamente.</span><span class="sxs-lookup"><span data-stu-id="cb329-120">This section highlights the nuances of the implementation to help you understand them more fully.</span></span>  

### <a name="allocation-of-values"></a><span data-ttu-id="cb329-121">Alocação de valores</span><span class="sxs-lookup"><span data-stu-id="cb329-121">Allocation of values</span></span>
<span data-ttu-id="cb329-122">A propriedade IDENTITY não garante a ordem na qual os valores substitutos são alocados, o que reflete o comportamento do SQL Server e do Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb329-122">The IDENTITY property doesn't guarantee the order in which the surrogate values are allocated, which reflects the behavior of SQL Server and Azure SQL Database.</span></span> <span data-ttu-id="cb329-123">No entanto, no SQL Data Warehouse do Azure, a ausência de uma garantia é mais pronunciada.</span><span class="sxs-lookup"><span data-stu-id="cb329-123">However, in Azure SQL Data Warehouse, the absence of a guarantee is more pronounced.</span></span> 

<span data-ttu-id="cb329-124">O exemplo a seguir é uma ilustração:</span><span class="sxs-lookup"><span data-stu-id="cb329-124">The following example is an illustration:</span></span>

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)    NOT NULL
,   C2 VARCHAR(30)              NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

INSERT INTO dbo.T1
VALUES (NULL);

INSERT INTO dbo.T1
VALUES (NULL);

SELECT *
FROM dbo.T1;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

<span data-ttu-id="cb329-125">No exemplo anterior, duas linhas foram descarregadas na distribuição 1.</span><span class="sxs-lookup"><span data-stu-id="cb329-125">In the preceding example, two rows landed in distribution 1.</span></span> <span data-ttu-id="cb329-126">A primeira linha tem o valor substituto de 1 na coluna `C1`, e a segunda linha tem o valor substituto 61.</span><span class="sxs-lookup"><span data-stu-id="cb329-126">The first row has the surrogate value of 1 in column `C1`, and the second row has the surrogate value of 61.</span></span> <span data-ttu-id="cb329-127">Ambos os valores foram gerados pela propriedade IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="cb329-127">Both of these values were generated by the IDENTITY property.</span></span> <span data-ttu-id="cb329-128">No entanto, a alocação dos valores não é contígua.</span><span class="sxs-lookup"><span data-stu-id="cb329-128">However, the allocation of the values is not contiguous.</span></span> <span data-ttu-id="cb329-129">Este comportamento ocorre por design.</span><span class="sxs-lookup"><span data-stu-id="cb329-129">This behavior is by design.</span></span>

### <a name="skewed-data"></a><span data-ttu-id="cb329-130">Dados distorcidos</span><span class="sxs-lookup"><span data-stu-id="cb329-130">Skewed data</span></span> 
<span data-ttu-id="cb329-131">Os intervalos de valores para o tipo de dados são distribuídos igualmente pelas distribuições.</span><span class="sxs-lookup"><span data-stu-id="cb329-131">The range of values for the data type are spread evenly across the distributions.</span></span> <span data-ttu-id="cb329-132">Se uma tabela distribuída tiver dados distorcidos, então o intervalo de valores disponível para o tipo de dados pode ser esgotado prematuramente.</span><span class="sxs-lookup"><span data-stu-id="cb329-132">If a distributed table suffers from skewed data, then the range of values available to the datatype can be exhausted prematurely.</span></span> <span data-ttu-id="cb329-133">Por exemplo, se todos os dados resultam em uma única distribuição, então efetivamente a tabela tem acesso a apenas um sexagésimo dos valores do tipo de dados.</span><span class="sxs-lookup"><span data-stu-id="cb329-133">For example, if all the data ends up in a single distribution, then effectively the table has access to only one-sixtieth of the values of the data type.</span></span> <span data-ttu-id="cb329-134">Por esse motivo, a propriedade de identidade é limitada somente aos tipos de dados `INT` e `BIGINT`.</span><span class="sxs-lookup"><span data-stu-id="cb329-134">For this reason, the IDENTITY property is limited to `INT` and `BIGINT` data types only.</span></span>

### <a name="selectinto"></a><span data-ttu-id="cb329-135">SELECT..INTO</span><span class="sxs-lookup"><span data-stu-id="cb329-135">SELECT..INTO</span></span>
<span data-ttu-id="cb329-136">Quando uma coluna de IDENTITY existente é selecionada em uma nova tabela, a nova coluna herda a propriedade IDENTITY, a menos que uma das seguintes condições seja verdadeira:</span><span class="sxs-lookup"><span data-stu-id="cb329-136">When an existing IDENTITY column is selected into a new table, the new column inherits the IDENTITY property, unless one of the following conditions is true:</span></span>
- <span data-ttu-id="cb329-137">A instrução SELECT contém uma junção.</span><span class="sxs-lookup"><span data-stu-id="cb329-137">The SELECT statement contains a join.</span></span>
- <span data-ttu-id="cb329-138">Várias instruções SELECT são unidas usando UNION.</span><span class="sxs-lookup"><span data-stu-id="cb329-138">Multiple SELECT statements are joined by using UNION.</span></span>
- <span data-ttu-id="cb329-139">A coluna IDENTITY é listada mais de uma vez na lista SELECT.</span><span class="sxs-lookup"><span data-stu-id="cb329-139">The IDENTITY column is listed more than one time in the SELECT list.</span></span>
- <span data-ttu-id="cb329-140">A coluna IDENTITY é parte de uma expressão.</span><span class="sxs-lookup"><span data-stu-id="cb329-140">The IDENTITY column is part of an expression.</span></span>
    
<span data-ttu-id="cb329-141">Se qualquer uma das seguintes condições for verdadeira, a coluna é criada como NOT NULL em vez de herdar a propriedade IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="cb329-141">If any one of these conditions is true, the column is created NOT NULL instead of inheriting the IDENTITY property.</span></span>

### <a name="create-table-as-select"></a><span data-ttu-id="cb329-142">CREATE TABLE AS SELECT</span><span class="sxs-lookup"><span data-stu-id="cb329-142">CREATE TABLE AS SELECT</span></span>
<span data-ttu-id="cb329-143">CREATE TABLE AS SELECT (CTAS) segue o mesmo comportamento do SQL Server que está documentado para SELECT..INTO.</span><span class="sxs-lookup"><span data-stu-id="cb329-143">CREATE TABLE AS SELECT (CTAS) follows the same SQL Server behavior that's documented for SELECT..INTO.</span></span> <span data-ttu-id="cb329-144">No entanto, você não pode especificar uma propriedade IDENTITY na definição de coluna da parte `CREATE TABLE` da instrução.</span><span class="sxs-lookup"><span data-stu-id="cb329-144">However, you can't specify an IDENTITY property in the column definition of the `CREATE TABLE` part of the statement.</span></span> <span data-ttu-id="cb329-145">Você também não pode usar a função IDENTITY na parte `SELECT` do CTAS.</span><span class="sxs-lookup"><span data-stu-id="cb329-145">You also can't use the IDENTITY function in the `SELECT` part of the CTAS.</span></span> <span data-ttu-id="cb329-146">Para popular uma tabela, você precisa usar `CREATE TABLE` para definir a tabela, seguido de `INSERT..SELECT` para preenchê-la.</span><span class="sxs-lookup"><span data-stu-id="cb329-146">To populate a table, you need to use `CREATE TABLE` to define the table followed by `INSERT..SELECT` to populate it.</span></span>

## <a name="explicitly-insert-values-into-an-identity-column"></a><span data-ttu-id="cb329-147">Insera explicitamente os valores em uma coluna IDENTITY</span><span class="sxs-lookup"><span data-stu-id="cb329-147">Explicitly insert values into an IDENTITY column</span></span> 
<span data-ttu-id="cb329-148">O SQL Data Warehouse oferece suporte à sintaxe `SET IDENTITY_INSERT <your table> ON|OFF`.</span><span class="sxs-lookup"><span data-stu-id="cb329-148">SQL Data Warehouse supports `SET IDENTITY_INSERT <your table> ON|OFF` syntax.</span></span> <span data-ttu-id="cb329-149">Você pode usar essa sintaxe para inserir explicitamente os valores na coluna IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="cb329-149">You can use this syntax to explicitly insert values into the IDENTITY column.</span></span>

<span data-ttu-id="cb329-150">Muitos modeladores de dados gostam de usar valores negativos predefinidos para determinadas linhas em suas dimensões.</span><span class="sxs-lookup"><span data-stu-id="cb329-150">Many data modelers like to use predefined negative values for certain rows in their dimensions.</span></span> <span data-ttu-id="cb329-151">Um exemplo é de -1 ou a linha "membro desconhecido".</span><span class="sxs-lookup"><span data-stu-id="cb329-151">An example is the -1 or "unknown member" row.</span></span> 

<span data-ttu-id="cb329-152">O próximo script mostra como adicionar essa linha explicitamente usando SET IDENTITY_INSERT:</span><span class="sxs-lookup"><span data-stu-id="cb329-152">The next script shows how to explicitly add this row by using SET IDENTITY_INSERT:</span></span>

```sql
SET IDENTITY_INSERT dbo.T1 ON;

INSERT INTO dbo.T1
(   C1
,   C2
)
VALUES (-1,'UNKNOWN')
;

SET IDENTITY_INSERT dbo.T1 OFF;

SELECT  *
FROM    dbo.T1
;
```    

## <a name="load-data-into-a-table-with-identity"></a><span data-ttu-id="cb329-153">Carregar dados em uma tabela com IDENTITY</span><span class="sxs-lookup"><span data-stu-id="cb329-153">Load data into a table with IDENTITY</span></span>

<span data-ttu-id="cb329-154">A presença da propriedade IDENTITY tem algumas implicações no seu código de carregamento de dados.</span><span class="sxs-lookup"><span data-stu-id="cb329-154">The presence of the IDENTITY property has some implications to your data-loading code.</span></span> <span data-ttu-id="cb329-155">Esta seção destaca alguns padrões básicos para carregar dados em tabelas usando IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="cb329-155">This section highlights some basic patterns for loading data into tables by using IDENTITY.</span></span> 

### <a name="load-data-with-polybase"></a><span data-ttu-id="cb329-156">Carregar dados com o PolyBase</span><span class="sxs-lookup"><span data-stu-id="cb329-156">Load data with PolyBase</span></span>
<span data-ttu-id="cb329-157">Para carregar dados em uma tabela e gerar uma chave substituta, usando IDENTITY, crie a tabela e, em seguida, use INSERT..SELECT ou INSERT..VALUES para executar o carregamento.</span><span class="sxs-lookup"><span data-stu-id="cb329-157">To load data into a table and generate a surrogate key by using IDENTITY, create the table and then use INSERT..SELECT or INSERT..VALUES to perform the load.</span></span>

<span data-ttu-id="cb329-158">O exemplo a seguir destaca o padrão básico:</span><span class="sxs-lookup"><span data-stu-id="cb329-158">The following example highlights the basic pattern:</span></span>
 
```sql
--CREATE TABLE with IDENTITY
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)
,   C2 VARCHAR(30)
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

--Use INSERT..SELECT to populate the table from an external table
INSERT INTO dbo.T1
(C2)
SELECT  C2
FROM    ext.T1
;

SELECT  *
FROM    dbo.T1
;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

> [!NOTE] 
> <span data-ttu-id="cb329-159">Não é possível usar `CREATE TABLE AS SELECT` atualmente ao carregar dados em uma tabela com uma coluna IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="cb329-159">It's not possible to use `CREATE TABLE AS SELECT` currently when loading data into a table with an IDENTITY column.</span></span>
> 

<span data-ttu-id="cb329-160">Para obter mais informações sobre como carregar dados usando a ferramenta de programa de cópia em massa (BCP), consulte os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="cb329-160">For more information on loading data by using the bulk copy program (BCP) tool, see the following articles:</span></span>

- <span data-ttu-id="cb329-161">[Carregar com PolyBase][]</span><span class="sxs-lookup"><span data-stu-id="cb329-161">[Load with PolyBase][]</span></span>
- <span data-ttu-id="cb329-162">[Práticas recomendadas do PolyBase][]</span><span class="sxs-lookup"><span data-stu-id="cb329-162">[PolyBase best practices][]</span></span>

### <a name="load-data-with-bcp"></a><span data-ttu-id="cb329-163">Carregar dados com o BCP</span><span class="sxs-lookup"><span data-stu-id="cb329-163">Load data with BCP</span></span>
<span data-ttu-id="cb329-164">O BCP é uma ferramenta de linha de comando que você pode usar para carregar dados no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="cb329-164">BCP is a command-line tool that you can use to load data into SQL Data Warehouse.</span></span> <span data-ttu-id="cb329-165">Um dos seus parâmetros (-E) controla o comportamento do BCP ao carregar dados em uma tabela com uma coluna IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="cb329-165">One of its parameters (-E) controls the behavior of BCP when loading data into a table with an IDENTITY column.</span></span> 

<span data-ttu-id="cb329-166">Quando -E for especificado, os valores mantidos no arquivo de entrada para a coluna com IDENTITY serão retidos.</span><span class="sxs-lookup"><span data-stu-id="cb329-166">When -E is specified, the values held in the input file for the column with IDENTITY are retained.</span></span> <span data-ttu-id="cb329-167">Se -E *não* for especificado, os valores nesta coluna são ignorados.</span><span class="sxs-lookup"><span data-stu-id="cb329-167">If -E is *not* specified, then the values in this column are ignored.</span></span> <span data-ttu-id="cb329-168">Se a coluna de identidade não for incluída, os dados são carregados normalmente.</span><span class="sxs-lookup"><span data-stu-id="cb329-168">If the identity column is not included, then the data is loaded as normal.</span></span> <span data-ttu-id="cb329-169">Os valores são gerados de acordo com a política de incremento e semente da propriedade.</span><span class="sxs-lookup"><span data-stu-id="cb329-169">The values are generated according to the increment and seed policy of the property.</span></span>

<span data-ttu-id="cb329-170">Para obter mais informações sobre como carregar dados usando o BCP, consulte os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="cb329-170">For more information on loading data by using BCP, see the following articles:</span></span>

- <span data-ttu-id="cb329-171">[Carregar com BCP][]</span><span class="sxs-lookup"><span data-stu-id="cb329-171">[Load with BCP][]</span></span>
- <span data-ttu-id="cb329-172">[BCP no MSDN][]</span><span class="sxs-lookup"><span data-stu-id="cb329-172">[BCP in MSDN][]</span></span>

## <a name="catalog-views"></a><span data-ttu-id="cb329-173">Exibições do catálogo</span><span class="sxs-lookup"><span data-stu-id="cb329-173">Catalog views</span></span>
<span data-ttu-id="cb329-174">O SQL Data Warehouse oferece suporte à exibição do catálogo `sys.identity_columns`.</span><span class="sxs-lookup"><span data-stu-id="cb329-174">SQL Data Warehouse supports the `sys.identity_columns` catalog view.</span></span> <span data-ttu-id="cb329-175">Este modo de exibição pode ser usado para identificar uma coluna que tem a propriedade IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="cb329-175">This view can be used to identify a column that has the IDENTITY property.</span></span>

<span data-ttu-id="cb329-176">Para ajudá-lo a entender melhor o esquema de banco de dados, este exemplo mostra como integrar `sys.identity_columns` com outra exibições de catálogo do sistema:</span><span class="sxs-lookup"><span data-stu-id="cb329-176">To help you better understand the database schema, this example shows how to integrate `sys.identity_columns` with other system catalog views:</span></span>

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       CASE WHEN ic.column_id IS NOT NULL
             THEN 1
        ELSE 0
        END AS is_identity 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
LEFT JOIN   sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="limitations"></a><span data-ttu-id="cb329-177">Limitações</span><span class="sxs-lookup"><span data-stu-id="cb329-177">Limitations</span></span>
<span data-ttu-id="cb329-178">A propriedade IDENTITY não pode ser usada nos seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="cb329-178">The IDENTITY property can't be used in the following scenarios:</span></span>
- <span data-ttu-id="cb329-179">O tipo de dados da coluna não é INT ou BIGINT</span><span class="sxs-lookup"><span data-stu-id="cb329-179">Where the column data type is not INT or BIGINT</span></span>
- <span data-ttu-id="cb329-180">A coluna é também a chave de distribuição</span><span class="sxs-lookup"><span data-stu-id="cb329-180">Where the column is also the distribution key</span></span>
- <span data-ttu-id="cb329-181">A tabela é uma tabela externa</span><span class="sxs-lookup"><span data-stu-id="cb329-181">Where the table is an external table</span></span> 

<span data-ttu-id="cb329-182">As funções relacionadas a seguir não têm suporte no SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="cb329-182">The following related functions are not supported in SQL Data Warehouse:</span></span>

- <span data-ttu-id="cb329-183">[IDENTITY()][]</span><span class="sxs-lookup"><span data-stu-id="cb329-183">[IDENTITY()][]</span></span>
- <span data-ttu-id="cb329-184">[@@IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="cb329-184">[@@IDENTITY][]</span></span>
- <span data-ttu-id="cb329-185">[SCOPE_IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="cb329-185">[SCOPE_IDENTITY][]</span></span>
- <span data-ttu-id="cb329-186">[IDENT_CURRENT][]</span><span class="sxs-lookup"><span data-stu-id="cb329-186">[IDENT_CURRENT][]</span></span>
- <span data-ttu-id="cb329-187">[IDENT_INCR][]</span><span class="sxs-lookup"><span data-stu-id="cb329-187">[IDENT_INCR][]</span></span>
- <span data-ttu-id="cb329-188">[IDENT_SEED][]</span><span class="sxs-lookup"><span data-stu-id="cb329-188">[IDENT_SEED][]</span></span>
- <span data-ttu-id="cb329-189">[DBCC CHECK_IDENT()][]</span><span class="sxs-lookup"><span data-stu-id="cb329-189">[DBCC CHECK_IDENT()][]</span></span>

## <a name="tasks"></a><span data-ttu-id="cb329-190">Tarefas</span><span class="sxs-lookup"><span data-stu-id="cb329-190">Tasks</span></span>

<span data-ttu-id="cb329-191">Esta seção fornece um código de exemplo que você pode usar para executar tarefas comuns ao trabalhar com colunas IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="cb329-191">This section provides some sample code you can use to perform common tasks when you work with IDENTITY columns.</span></span>

> [!NOTE] 
> <span data-ttu-id="cb329-192">A coluna C1 é a IDENTITY em todas as tarefas a seguir.</span><span class="sxs-lookup"><span data-stu-id="cb329-192">Column C1 is the IDENTITY in all the following tasks.</span></span>
> 
 
### <a name="find-the-highest-allocated-value-for-a-table"></a><span data-ttu-id="cb329-193">Localizar o maior valor alocado para uma tabela</span><span class="sxs-lookup"><span data-stu-id="cb329-193">Find the highest allocated value for a table</span></span>
<span data-ttu-id="cb329-194">Use a função `MAX()` para determinar o valor mais alto alocado para uma tabela distribuída:</span><span class="sxs-lookup"><span data-stu-id="cb329-194">Use the `MAX()` function to determine the highest value allocated for a distributed table:</span></span>

```sql
SELECT  MAX(C1)
FROM    dbo.T1
``` 

### <a name="find-the-seed-and-increment-for-the-identity-property"></a><span data-ttu-id="cb329-195">Localizar a semente e o incremento para a propriedade IDENTITY</span><span class="sxs-lookup"><span data-stu-id="cb329-195">Find the seed and increment for the IDENTITY property</span></span>
<span data-ttu-id="cb329-196">Você pode usar as exibições de catálogo para descobrir os valores de configuração da semente e do incremento da identidade para uma tabela usando a consulta a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb329-196">You can use the catalog views to discover the identity increment and seed configuration values for a table by using the following query:</span></span> 

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       ic.seed_value
,       ic.increment_value 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
JOIN        sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="next-steps"></a><span data-ttu-id="cb329-197">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cb329-197">Next steps</span></span>

* <span data-ttu-id="cb329-198">Para saber mais sobre o desenvolvimento de tabelas, consulte [Visão geral da tabela][Overview], [Tipos de dados da tabela][Data Types], [Distribuição de uma tabela][Distribute], [Indexação de uma tabela][Index], [Partição de uma tabela][Partition] e [Tabelas temporárias][Temporary].</span><span class="sxs-lookup"><span data-stu-id="cb329-198">To learn more about developing tables, see [Table overview][Overview], [Table data types][Data Types], [Distribute a table][Distribute], [Index a table][Index], [Partition a table][Partition], and [Temporary tables][Temporary].</span></span> 
* <span data-ttu-id="cb329-199">Para saber mais sobre as práticas recomendadas, consulte [Práticas recomendadas do SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="cb329-199">For more information about best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse Best Practices].</span></span>  

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Identity]: ./sql-data-warehouse-tables-identity.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<span data-ttu-id="cb329-200">[Carregar com BCP]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/</span><span class="sxs-lookup"><span data-stu-id="cb329-200">[Load with bcp]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/</span></span>
<span data-ttu-id="cb329-201">[Carregar com PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/</span><span class="sxs-lookup"><span data-stu-id="cb329-201">[Load with PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/</span></span>
<span data-ttu-id="cb329-202">[Práticas recomendadas do PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/</span><span class="sxs-lookup"><span data-stu-id="cb329-202">[PolyBase best practices]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/</span></span>


<!--MSDN references-->
[Identity property]: https://msdn.microsoft.com/library/ms186775.aspx
[sys.identity_columns]: https://msdn.microsoft.com/library/ms187334.aspx
<span data-ttu-id="cb329-203">[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx</span><span class="sxs-lookup"><span data-stu-id="cb329-203">[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx</span></span>
<span data-ttu-id="cb329-204">[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx</span><span class="sxs-lookup"><span data-stu-id="cb329-204">[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx</span></span>
<span data-ttu-id="cb329-205">[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx</span><span class="sxs-lookup"><span data-stu-id="cb329-205">[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx</span></span>
<span data-ttu-id="cb329-206">[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx</span><span class="sxs-lookup"><span data-stu-id="cb329-206">[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx</span></span>
<span data-ttu-id="cb329-207">[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx</span><span class="sxs-lookup"><span data-stu-id="cb329-207">[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx</span></span>
<span data-ttu-id="cb329-208">[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx</span><span class="sxs-lookup"><span data-stu-id="cb329-208">[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx</span></span>
<span data-ttu-id="cb329-209">[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx</span><span class="sxs-lookup"><span data-stu-id="cb329-209">[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx</span></span>

<span data-ttu-id="cb329-210">[BCP no MSDN]: https://msdn.microsoft.com/library/ms162802.aspx</span><span class="sxs-lookup"><span data-stu-id="cb329-210">[bcp in MSDN]: https://msdn.microsoft.com/library/ms162802.aspx</span></span>
  

<!--Other Web references-->  
