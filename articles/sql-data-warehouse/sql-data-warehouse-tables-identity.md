---
title: as chaves substitutas aaaCreate usando a identidade | Microsoft Docs
description: Saiba como substituto do toouse identidade toocreate chaves em suas tabelas.
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
ms.openlocfilehash: 502cdd2b510b229b2a19c1f78b11862a7386ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-surrogate-keys-by-using-identity"></a><span data-ttu-id="0dcb3-103">Criar chaves substitutas usando IDENTITY</span><span class="sxs-lookup"><span data-stu-id="0dcb3-103">Create surrogate keys by using IDENTITY</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="0dcb3-104">[Visão geral][Overview]</span><span class="sxs-lookup"><span data-stu-id="0dcb3-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="0dcb3-105">[Tipos de dados][Data Types]</span><span class="sxs-lookup"><span data-stu-id="0dcb3-105">[Data types][Data Types]</span></span>
> * <span data-ttu-id="0dcb3-106">[Distribuir][Distribute]</span><span class="sxs-lookup"><span data-stu-id="0dcb3-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="0dcb3-107">[Índice][Index]</span><span class="sxs-lookup"><span data-stu-id="0dcb3-107">[Index][Index]</span></span>
> * <span data-ttu-id="0dcb3-108">[Partição][Partition]</span><span class="sxs-lookup"><span data-stu-id="0dcb3-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="0dcb3-109">[Estatísticas][Statistics]</span><span class="sxs-lookup"><span data-stu-id="0dcb3-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="0dcb3-110">[Temporário][Temporary]</span><span class="sxs-lookup"><span data-stu-id="0dcb3-110">[Temporary][Temporary]</span></span>
> * <span data-ttu-id="0dcb3-111">[Identidade][Identity]</span><span class="sxs-lookup"><span data-stu-id="0dcb3-111">[Identity][Identity]</span></span>
> 
> 

<span data-ttu-id="0dcb3-112">Muitos modeladores de dados, como chaves substitutas de toocreate em suas tabelas quando criam modelos de depósito de dados.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-112">Many data modelers like toocreate surrogate keys on their tables when they design data warehouse models.</span></span> <span data-ttu-id="0dcb3-113">Você pode usar tooachieve de propriedade de identidade Olá essa meta simples e eficiente sem afetar o desempenho de carga.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-113">You can use hello IDENTITY property tooachieve this goal simply and effectively without affecting load performance.</span></span> 

## <a name="get-started-with-identity"></a><span data-ttu-id="0dcb3-114">Introdução ao IDENTITY</span><span class="sxs-lookup"><span data-stu-id="0dcb3-114">Get started with IDENTITY</span></span>
<span data-ttu-id="0dcb3-115">Você pode definir uma tabela como tendo a propriedade IDENTITY hello quando você cria tabela hello usando sintaxe semelhante toohello instrução a seguir:</span><span class="sxs-lookup"><span data-stu-id="0dcb3-115">You can define a table as having hello IDENTITY property when you first create hello table by using syntax that is similar toohello following statement:</span></span>

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

<span data-ttu-id="0dcb3-116">Você pode usar `INSERT..SELECT` toopopulate tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-116">You can then use `INSERT..SELECT` toopopulate hello table.</span></span>

## <a name="behavior"></a><span data-ttu-id="0dcb3-117">Comportamento</span><span class="sxs-lookup"><span data-stu-id="0dcb3-117">Behavior</span></span>
<span data-ttu-id="0dcb3-118">Olá propriedade IDENTITY é projetado tooscale out em todas as distribuições de saudação no data warehouse de saudação sem afetar o desempenho de carga.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-118">hello IDENTITY property is designed tooscale out across all hello distributions in hello data warehouse without affecting load performance.</span></span> <span data-ttu-id="0dcb3-119">Portanto, a implementação de saudação da identidade é orientada para atingir esses objetivos.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-119">Therefore, hello implementation of IDENTITY is oriented toward achieving these goals.</span></span> <span data-ttu-id="0dcb3-120">Esta seção destaca nuances de saudação do hello implementação toohelp é compreendê-los mais detalhadamente.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-120">This section highlights hello nuances of hello implementation toohelp you understand them more fully.</span></span>  

### <a name="allocation-of-values"></a><span data-ttu-id="0dcb3-121">Alocação de valores</span><span class="sxs-lookup"><span data-stu-id="0dcb3-121">Allocation of values</span></span>
<span data-ttu-id="0dcb3-122">Olá a propriedade IDENTITY não garante a ordem de saudação em qual Olá valores substitutos são alocados, que refletem o comportamento de saudação do SQL Server e banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-122">hello IDENTITY property doesn't guarantee hello order in which hello surrogate values are allocated, which reflects hello behavior of SQL Server and Azure SQL Database.</span></span> <span data-ttu-id="0dcb3-123">No entanto, no Azure SQL Data Warehouse, ausência de saudação de uma garantia é mais pronunciada.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-123">However, in Azure SQL Data Warehouse, hello absence of a guarantee is more pronounced.</span></span> 

<span data-ttu-id="0dcb3-124">saudação de exemplo a seguir é uma ilustração:</span><span class="sxs-lookup"><span data-stu-id="0dcb3-124">hello following example is an illustration:</span></span>

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

<span data-ttu-id="0dcb3-125">Em Olá anterior de exemplo, duas linhas descarregou na distribuição 1.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-125">In hello preceding example, two rows landed in distribution 1.</span></span> <span data-ttu-id="0dcb3-126">Olá primeira linha tem o valor substituto Olá 1 na coluna `C1`, e Olá segunda linha tem o valor substituto Olá 61.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-126">hello first row has hello surrogate value of 1 in column `C1`, and hello second row has hello surrogate value of 61.</span></span> <span data-ttu-id="0dcb3-127">Ambos os valores foram gerados por Olá propriedade de identidade.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-127">Both of these values were generated by hello IDENTITY property.</span></span> <span data-ttu-id="0dcb3-128">No entanto, a alocação de saudação de valores de saudação não é contígua.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-128">However, hello allocation of hello values is not contiguous.</span></span> <span data-ttu-id="0dcb3-129">Este comportamento ocorre por design.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-129">This behavior is by design.</span></span>

### <a name="skewed-data"></a><span data-ttu-id="0dcb3-130">Dados distorcidos</span><span class="sxs-lookup"><span data-stu-id="0dcb3-130">Skewed data</span></span> 
<span data-ttu-id="0dcb3-131">Olá intervalo de valores para o tipo de dados Olá estarão distribuídos igualmente por distribuições hello.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-131">hello range of values for hello data type are spread evenly across hello distributions.</span></span> <span data-ttu-id="0dcb3-132">Se uma tabela distribuída tiver dados distorcidos, Olá, em seguida, o intervalo de valores de tipo de dados toohello disponíveis pode ser esgotado prematuramente.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-132">If a distributed table suffers from skewed data, then hello range of values available toohello datatype can be exhausted prematurely.</span></span> <span data-ttu-id="0dcb3-133">Por exemplo, se todos os dados de saudação termina em um único de distribuição, em seguida, efetivamente Olá tabela tem acesso tooonly sixtieth um dos valores de Olá Olá do tipo de dados.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-133">For example, if all hello data ends up in a single distribution, then effectively hello table has access tooonly one-sixtieth of hello values of hello data type.</span></span> <span data-ttu-id="0dcb3-134">Por esse motivo, Olá propriedade IDENTITY é limitado muito`INT` e `BIGINT` apenas tipos de dados.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-134">For this reason, hello IDENTITY property is limited too`INT` and `BIGINT` data types only.</span></span>

### <a name="selectinto"></a><span data-ttu-id="0dcb3-135">SELECT..INTO</span><span class="sxs-lookup"><span data-stu-id="0dcb3-135">SELECT..INTO</span></span>
<span data-ttu-id="0dcb3-136">Quando uma coluna de identidade existente é selecionada em uma nova tabela, o hello nova coluna herda a propriedade de identidade Olá, a menos que uma saudação seguintes condições for verdadeira:</span><span class="sxs-lookup"><span data-stu-id="0dcb3-136">When an existing IDENTITY column is selected into a new table, hello new column inherits hello IDENTITY property, unless one of hello following conditions is true:</span></span>
- <span data-ttu-id="0dcb3-137">Olá a instrução SELECT contém uma junção.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-137">hello SELECT statement contains a join.</span></span>
- <span data-ttu-id="0dcb3-138">Várias instruções SELECT são unidas usando UNION.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-138">Multiple SELECT statements are joined by using UNION.</span></span>
- <span data-ttu-id="0dcb3-139">coluna de identidade Hello está listada mais de uma vez na lista de seleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-139">hello IDENTITY column is listed more than one time in hello SELECT list.</span></span>
- <span data-ttu-id="0dcb3-140">coluna de identidade Olá faz parte de uma expressão.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-140">hello IDENTITY column is part of an expression.</span></span>
    
<span data-ttu-id="0dcb3-141">Se qualquer uma das seguintes condições for verdadeira, a coluna de saudação é criada NOT NULL em vez de herdar a propriedade IDENTITY hello.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-141">If any one of these conditions is true, hello column is created NOT NULL instead of inheriting hello IDENTITY property.</span></span>

### <a name="create-table-as-select"></a><span data-ttu-id="0dcb3-142">CREATE TABLE AS SELECT</span><span class="sxs-lookup"><span data-stu-id="0dcb3-142">CREATE TABLE AS SELECT</span></span>
<span data-ttu-id="0dcb3-143">Criar tabela como selecionar (CTAS) segue Olá mesmo comportamento do SQL Server que está documentado para SELECT... EM.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-143">CREATE TABLE AS SELECT (CTAS) follows hello same SQL Server behavior that's documented for SELECT..INTO.</span></span> <span data-ttu-id="0dcb3-144">No entanto, você não pode especificar uma propriedade de identidade na definição de coluna de saudação do hello `CREATE TABLE` parte da instrução de saudação.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-144">However, you can't specify an IDENTITY property in hello column definition of hello `CREATE TABLE` part of hello statement.</span></span> <span data-ttu-id="0dcb3-145">Você também não é possível usar função de identidade hello em Olá `SELECT` fazem parte do hello CTAS.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-145">You also can't use hello IDENTITY function in hello `SELECT` part of hello CTAS.</span></span> <span data-ttu-id="0dcb3-146">toopopulate uma tabela, você precisa toouse `CREATE TABLE` seguido de tabela de saudação toodefine `INSERT..SELECT` toopopulate-lo.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-146">toopopulate a table, you need toouse `CREATE TABLE` toodefine hello table followed by `INSERT..SELECT` toopopulate it.</span></span>

## <a name="explicitly-insert-values-into-an-identity-column"></a><span data-ttu-id="0dcb3-147">Insera explicitamente os valores em uma coluna IDENTITY</span><span class="sxs-lookup"><span data-stu-id="0dcb3-147">Explicitly insert values into an IDENTITY column</span></span> 
<span data-ttu-id="0dcb3-148">O SQL Data Warehouse oferece suporte à sintaxe `SET IDENTITY_INSERT <your table> ON|OFF`.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-148">SQL Data Warehouse supports `SET IDENTITY_INSERT <your table> ON|OFF` syntax.</span></span> <span data-ttu-id="0dcb3-149">Você pode usar essa sintaxe tooexplicitly inserir os valores na coluna de identidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-149">You can use this syntax tooexplicitly insert values into hello IDENTITY column.</span></span>

<span data-ttu-id="0dcb3-150">Muitos modeladores de dados como negativo predefinidos toouse para determinados valores de linhas em suas dimensões.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-150">Many data modelers like toouse predefined negative values for certain rows in their dimensions.</span></span> <span data-ttu-id="0dcb3-151">Um exemplo é Olá -1 ou linha "membro desconhecido".</span><span class="sxs-lookup"><span data-stu-id="0dcb3-151">An example is hello -1 or "unknown member" row.</span></span> 

<span data-ttu-id="0dcb3-152">próximo de script Hello mostra como tooexplicitly adicionar essa linha usando SET IDENTITY_INSERT:</span><span class="sxs-lookup"><span data-stu-id="0dcb3-152">hello next script shows how tooexplicitly add this row by using SET IDENTITY_INSERT:</span></span>

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

## <a name="load-data-into-a-table-with-identity"></a><span data-ttu-id="0dcb3-153">Carregar dados em uma tabela com IDENTITY</span><span class="sxs-lookup"><span data-stu-id="0dcb3-153">Load data into a table with IDENTITY</span></span>

<span data-ttu-id="0dcb3-154">presença Olá Olá propriedade IDENTITY tem código de carregamento de dados de tooyour algumas implicações.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-154">hello presence of hello IDENTITY property has some implications tooyour data-loading code.</span></span> <span data-ttu-id="0dcb3-155">Esta seção destaca alguns padrões básicos para carregar dados em tabelas usando IDENTITY.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-155">This section highlights some basic patterns for loading data into tables by using IDENTITY.</span></span> 

### <a name="load-data-with-polybase"></a><span data-ttu-id="0dcb3-156">Carregar dados com o PolyBase</span><span class="sxs-lookup"><span data-stu-id="0dcb3-156">Load data with PolyBase</span></span>
<span data-ttu-id="0dcb3-157">dados tooload em uma tabela e gerar uma chave substituta, usando a identidade, criar tabela hello e, em seguida, usar INSERT... SELECT ou INSERT... VALORES tooperform Olá carga.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-157">tooload data into a table and generate a surrogate key by using IDENTITY, create hello table and then use INSERT..SELECT or INSERT..VALUES tooperform hello load.</span></span>

<span data-ttu-id="0dcb3-158">Olá, exemplo a seguir destaca padrão básico hello:</span><span class="sxs-lookup"><span data-stu-id="0dcb3-158">hello following example highlights hello basic pattern:</span></span>
 
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

--Use INSERT..SELECT toopopulate hello table from an external table
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
> <span data-ttu-id="0dcb3-159">Não é possível toouse `CREATE TABLE AS SELECT` atualmente ao carregar dados em uma tabela com uma coluna de identidade.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-159">It's not possible toouse `CREATE TABLE AS SELECT` currently when loading data into a table with an IDENTITY column.</span></span>
> 

<span data-ttu-id="0dcb3-160">Para obter mais informações sobre carregar dados usando a ferramenta de BCP (programa) de cópia em massa hello, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="0dcb3-160">For more information on loading data by using hello bulk copy program (BCP) tool, see hello following articles:</span></span>

- <span data-ttu-id="0dcb3-161">[Carregar com PolyBase][]</span><span class="sxs-lookup"><span data-stu-id="0dcb3-161">[Load with PolyBase][]</span></span>
- <span data-ttu-id="0dcb3-162">[Práticas recomendadas do PolyBase][]</span><span class="sxs-lookup"><span data-stu-id="0dcb3-162">[PolyBase best practices][]</span></span>

### <a name="load-data-with-bcp"></a><span data-ttu-id="0dcb3-163">Carregar dados com o BCP</span><span class="sxs-lookup"><span data-stu-id="0dcb3-163">Load data with BCP</span></span>
<span data-ttu-id="0dcb3-164">O BCP é uma ferramenta de linha de comando que você pode usar dados tooload no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-164">BCP is a command-line tool that you can use tooload data into SQL Data Warehouse.</span></span> <span data-ttu-id="0dcb3-165">Um de seus parâmetros (-E) controles Olá comportamento de BCP ao carregar dados em uma tabela com uma coluna de identidade.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-165">One of its parameters (-E) controls hello behavior of BCP when loading data into a table with an IDENTITY column.</span></span> 

<span data-ttu-id="0dcb3-166">Quando -E também for especificado, os valores de saudação mantidos no arquivo de entrada hello para coluna Olá com identidade serão retidos.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-166">When -E is specified, hello values held in hello input file for hello column with IDENTITY are retained.</span></span> <span data-ttu-id="0dcb3-167">Se -E é *não* especificado, Olá valores nessa coluna são ignorados.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-167">If -E is *not* specified, then hello values in this column are ignored.</span></span> <span data-ttu-id="0dcb3-168">Se a coluna de identidade de saudação não for incluída, dados de saudação são carregados como normal.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-168">If hello identity column is not included, then hello data is loaded as normal.</span></span> <span data-ttu-id="0dcb3-169">valores Hello são gerados de acordo com a política de incremento e semente toohello da propriedade hello.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-169">hello values are generated according toohello increment and seed policy of hello property.</span></span>

<span data-ttu-id="0dcb3-170">Para obter mais informações sobre carregar dados usando BCP, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="0dcb3-170">For more information on loading data by using BCP, see hello following articles:</span></span>

- <span data-ttu-id="0dcb3-171">[Carregar com BCP][]</span><span class="sxs-lookup"><span data-stu-id="0dcb3-171">[Load with BCP][]</span></span>
- <span data-ttu-id="0dcb3-172">[BCP no MSDN][]</span><span class="sxs-lookup"><span data-stu-id="0dcb3-172">[BCP in MSDN][]</span></span>

## <a name="catalog-views"></a><span data-ttu-id="0dcb3-173">Exibições do catálogo</span><span class="sxs-lookup"><span data-stu-id="0dcb3-173">Catalog views</span></span>
<span data-ttu-id="0dcb3-174">SQL Data Warehouse dá suporte a saudação `sys.identity_columns` exibição do catálogo.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-174">SQL Data Warehouse supports hello `sys.identity_columns` catalog view.</span></span> <span data-ttu-id="0dcb3-175">Este modo de exibição pode ser usado tooidentify uma coluna que tem a propriedade de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-175">This view can be used tooidentify a column that has hello IDENTITY property.</span></span>

<span data-ttu-id="0dcb3-176">toohelp você entender melhor o esquema de banco de dados hello, este exemplo mostra como toointegrate `sys.identity_columns` com outros modos de exibição de catálogo do sistema:</span><span class="sxs-lookup"><span data-stu-id="0dcb3-176">toohelp you better understand hello database schema, this example shows how toointegrate `sys.identity_columns` with other system catalog views:</span></span>

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

## <a name="limitations"></a><span data-ttu-id="0dcb3-177">Limitações</span><span class="sxs-lookup"><span data-stu-id="0dcb3-177">Limitations</span></span>
<span data-ttu-id="0dcb3-178">Olá a propriedade IDENTITY não pode ser usado Olá os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="0dcb3-178">hello IDENTITY property can't be used in hello following scenarios:</span></span>
- <span data-ttu-id="0dcb3-179">Qual tipo de dados de coluna Olá não é INT ou BIGINT</span><span class="sxs-lookup"><span data-stu-id="0dcb3-179">Where hello column data type is not INT or BIGINT</span></span>
- <span data-ttu-id="0dcb3-180">Onde a coluna Olá também é chave de distribuição de saudação</span><span class="sxs-lookup"><span data-stu-id="0dcb3-180">Where hello column is also hello distribution key</span></span>
- <span data-ttu-id="0dcb3-181">Onde a tabela de saudação é uma tabela externa</span><span class="sxs-lookup"><span data-stu-id="0dcb3-181">Where hello table is an external table</span></span> 

<span data-ttu-id="0dcb3-182">Olá funções relacionadas a seguir não têm suporte no SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="0dcb3-182">hello following related functions are not supported in SQL Data Warehouse:</span></span>

- <span data-ttu-id="0dcb3-183">[IDENTITY()][]</span><span class="sxs-lookup"><span data-stu-id="0dcb3-183">[IDENTITY()][]</span></span>
- <span data-ttu-id="0dcb3-184">[@@IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="0dcb3-184">[@@IDENTITY][]</span></span>
- <span data-ttu-id="0dcb3-185">[SCOPE_IDENTITY][]</span><span class="sxs-lookup"><span data-stu-id="0dcb3-185">[SCOPE_IDENTITY][]</span></span>
- <span data-ttu-id="0dcb3-186">[IDENT_CURRENT][]</span><span class="sxs-lookup"><span data-stu-id="0dcb3-186">[IDENT_CURRENT][]</span></span>
- <span data-ttu-id="0dcb3-187">[IDENT_INCR][]</span><span class="sxs-lookup"><span data-stu-id="0dcb3-187">[IDENT_INCR][]</span></span>
- <span data-ttu-id="0dcb3-188">[IDENT_SEED][]</span><span class="sxs-lookup"><span data-stu-id="0dcb3-188">[IDENT_SEED][]</span></span>
- <span data-ttu-id="0dcb3-189">[DBCC CHECK_IDENT()][]</span><span class="sxs-lookup"><span data-stu-id="0dcb3-189">[DBCC CHECK_IDENT()][]</span></span>

## <a name="tasks"></a><span data-ttu-id="0dcb3-190">Tarefas</span><span class="sxs-lookup"><span data-stu-id="0dcb3-190">Tasks</span></span>

<span data-ttu-id="0dcb3-191">Esta seção fornece um exemplo de código você pode usar tarefas comuns de tooperform quando você trabalha com colunas de identidade.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-191">This section provides some sample code you can use tooperform common tasks when you work with IDENTITY columns.</span></span>

> [!NOTE] 
> <span data-ttu-id="0dcb3-192">Coluna C1 é hello identidade no hello todas as tarefas a seguir.</span><span class="sxs-lookup"><span data-stu-id="0dcb3-192">Column C1 is hello IDENTITY in all hello following tasks.</span></span>
> 
 
### <a name="find-hello-highest-allocated-value-for-a-table"></a><span data-ttu-id="0dcb3-193">Localize o valor de hello mais alta alocada para uma tabela</span><span class="sxs-lookup"><span data-stu-id="0dcb3-193">Find hello highest allocated value for a table</span></span>
<span data-ttu-id="0dcb3-194">Saudação de uso `MAX()` função toodetermine Olá maior valor alocado para uma tabela distribuída:</span><span class="sxs-lookup"><span data-stu-id="0dcb3-194">Use hello `MAX()` function toodetermine hello highest value allocated for a distributed table:</span></span>

```sql
SELECT  MAX(C1)
FROM    dbo.T1
``` 

### <a name="find-hello-seed-and-increment-for-hello-identity-property"></a><span data-ttu-id="0dcb3-195">Localizar Olá semente e incremento para Olá propriedade de identidade</span><span class="sxs-lookup"><span data-stu-id="0dcb3-195">Find hello seed and increment for hello IDENTITY property</span></span>
<span data-ttu-id="0dcb3-196">Você pode usar o hello catálogo exibições toodiscover Olá identity incremento e semente valores de configuração para uma tabela usando Olá consulta a seguir:</span><span class="sxs-lookup"><span data-stu-id="0dcb3-196">You can use hello catalog views toodiscover hello identity increment and seed configuration values for a table by using hello following query:</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="0dcb3-197">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0dcb3-197">Next steps</span></span>

* <span data-ttu-id="0dcb3-198">toolearn mais sobre o desenvolvimento de tabelas, consulte [visão geral da tabela][Overview], [tipos de dados de tabela][Data Types], [distribuir uma tabela] [ Distribute], [Uma tabela de índice][Index], [particionar uma tabela][Partition], e [ Tabelas temporárias][Temporary].</span><span class="sxs-lookup"><span data-stu-id="0dcb3-198">toolearn more about developing tables, see [Table overview][Overview], [Table data types][Data Types], [Distribute a table][Distribute], [Index a table][Index], [Partition a table][Partition], and [Temporary tables][Temporary].</span></span> 
* <span data-ttu-id="0dcb3-199">Para saber mais sobre as práticas recomendadas, consulte [Práticas recomendadas do SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="0dcb3-199">For more information about best practices, see [SQL Data Warehouse best practices][SQL Data Warehouse Best Practices].</span></span>  

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

[Carregar com BCP]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/
[Carregar com PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/
[Práticas recomendadas do PolyBase]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/


<!--MSDN references-->
[Identity property]: https://msdn.microsoft.com/library/ms186775.aspx
[sys.identity_columns]: https://msdn.microsoft.com/library/ms187334.aspx
[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx
[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx
[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx
[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx
[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx
[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx
[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx

[BCP no MSDN]: https://msdn.microsoft.com/library/ms162802.aspx
  

<!--Other Web references-->  
