---
title: tabela aaaCreate como selecionar (CTAS) no SQL Data Warehouse | Microsoft Docs
description: "Dicas para codificação com hello criar tabela como selecionar instrução (CTAS) no Azure SQL Data Warehouse para o desenvolvimento de soluções."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 68ac9a94-09f9-424b-b536-06a125a653bd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 01/30/2017
ms.author: shigu;barbkess
ms.openlocfilehash: e381601a0a4d94e189d8f9115bf2e7593025410b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-table-as-select-ctas-in-sql-data-warehouse"></a><span data-ttu-id="c6a49-103">Instrução Create Table As Select (CTAS) no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c6a49-103">Create Table As Select (CTAS) in SQL Data Warehouse</span></span>
<span data-ttu-id="c6a49-104">Criar tabela como select ou `CTAS` é uma saudação mais importantes recursos de T-SQL disponíveis.</span><span class="sxs-lookup"><span data-stu-id="c6a49-104">Create table as select or `CTAS` is one of hello most important T-SQL features available.</span></span> <span data-ttu-id="c6a49-105">É uma operação totalmente em paralelo que cria uma nova tabela com base na saída de saudação de uma instrução SELECT.</span><span class="sxs-lookup"><span data-stu-id="c6a49-105">It is a fully parallelized operation that creates a new table based on hello output of a SELECT statement.</span></span> <span data-ttu-id="c6a49-106">`CTAS`é uma cópia de uma tabela de toocreate de maneira mais rápida e simples de saudação.</span><span class="sxs-lookup"><span data-stu-id="c6a49-106">`CTAS` is hello simplest and fastest way toocreate a copy of a table.</span></span> <span data-ttu-id="c6a49-107">Este documento fornece exemplos e melhores práticas para o `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="c6a49-107">This document provides both examples and best practices for `CTAS`.</span></span>

## <a name="selectinto-vs-ctas"></a><span data-ttu-id="c6a49-108">SELECT..INTO versus CTAS</span><span class="sxs-lookup"><span data-stu-id="c6a49-108">SELECT..INTO vs. CTAS</span></span>
<span data-ttu-id="c6a49-109">Você pode considerar `CTAS` como uma versão turbinada de `SELECT..INTO`.</span><span class="sxs-lookup"><span data-stu-id="c6a49-109">You can consider `CTAS` as a super-charged version of `SELECT..INTO`.</span></span>

<span data-ttu-id="c6a49-110">Veja a seguir um exemplo de uma instrução `SELECT..INTO` simples:</span><span class="sxs-lookup"><span data-stu-id="c6a49-110">Below is an example of a simple `SELECT..INTO` statement:</span></span>

```sql
SELECT *
INTO    [dbo].[FactInternetSales_new]
FROM    [dbo].[FactInternetSales]
```

<span data-ttu-id="c6a49-111">No exemplo hello acima `[dbo].[FactInternetSales_new]` seria criado como tabela de ROUND_ROBIN distribuída com um índice de COLUMNSTORE CLUSTERIZADO nela conforme estes são os padrões de tabela Olá no Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c6a49-111">In hello example above `[dbo].[FactInternetSales_new]` would be created as ROUND_ROBIN distributed table with a CLUSTERED COLUMNSTORE INDEX on it as these are hello table defaults in Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="c6a49-112">`SELECT..INTO`No entanto não permitem que você toochange qualquer índice Olá distribuição hello ou método de tipo como parte da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="c6a49-112">`SELECT..INTO` however does not allow you toochange either hello distribution method or hello index type as part of hello operation.</span></span> <span data-ttu-id="c6a49-113">É aí que `CTAS` entra em cena.</span><span class="sxs-lookup"><span data-stu-id="c6a49-113">This is where `CTAS` comes in.</span></span>

<span data-ttu-id="c6a49-114">Olá tooconvert acima muito`CTAS` é bastante direta:</span><span class="sxs-lookup"><span data-stu-id="c6a49-114">tooconvert hello above too`CTAS` is quite straight-forward:</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_new]
WITH
(
    DISTRIBUTION = ROUND_ROBIN
,   CLUSTERED COLUMNSTORE INDEX
)
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
;
```

<span data-ttu-id="c6a49-115">Com `CTAS` são toochange capaz de ambos Olá a distribuição de dados da tabela hello, bem como o tipo de tabela hello.</span><span class="sxs-lookup"><span data-stu-id="c6a49-115">With `CTAS` you are able toochange both hello distribution of hello table data as well as hello table type.</span></span> 

> [!NOTE]
> <span data-ttu-id="c6a49-116">Se você estiver apenas tentando índice Olá toochange seu `CTAS` operação e hello tabela de origem é hash distribuída seu `CTAS` irá realizar a operação melhor se você mantiver Olá mesmo tipo de coluna e os dados de distribuição.</span><span class="sxs-lookup"><span data-stu-id="c6a49-116">If you are only trying toochange hello index in your `CTAS` operation and hello source table is hash distributed then your `CTAS` operation will perform best if you maintain hello same distribution column and data type.</span></span> <span data-ttu-id="c6a49-117">Isso evitará cruzada movimentação de dados de distribuição durante a operação de saudação que é mais eficiente.</span><span class="sxs-lookup"><span data-stu-id="c6a49-117">This will avoid cross distribution data movement during hello operation which is more efficient.</span></span>
> 
> 

## <a name="using-ctas-toocopy-a-table"></a><span data-ttu-id="c6a49-118">Usando CTAS toocopy uma tabela</span><span class="sxs-lookup"><span data-stu-id="c6a49-118">Using CTAS toocopy a table</span></span>
<span data-ttu-id="c6a49-119">Talvez um dos mais comuns de saudação usos de `CTAS` está criando uma cópia de uma tabela para que você possa alterar Olá DDL.</span><span class="sxs-lookup"><span data-stu-id="c6a49-119">Perhaps one of hello most common uses of `CTAS` is creating a copy of a table so that you can change hello DDL.</span></span> <span data-ttu-id="c6a49-120">Se por exemplo você criou a tabela como `ROUND_ROBIN` e agora deseja alterá-la tooa tabela distribuído em uma coluna, `CTAS` é como coluna de distribuição Olá deve ser alterada.</span><span class="sxs-lookup"><span data-stu-id="c6a49-120">If for example you originally created your table as `ROUND_ROBIN` and now want change it tooa table distributed on a column, `CTAS` is how you would change hello distribution column.</span></span> <span data-ttu-id="c6a49-121">`CTAS`também é possível toochange usado tipos de particionamento, indexação ou coluna.</span><span class="sxs-lookup"><span data-stu-id="c6a49-121">`CTAS` can also be used toochange partitioning, indexing, or column types.</span></span>

<span data-ttu-id="c6a49-122">Digamos que você criou esta tabela usando o tipo de distribuição de padrão de saudação do `ROUND_ROBIN` distribuída porque nenhuma coluna de distribuição foi especificada no hello `CREATE TABLE`.</span><span class="sxs-lookup"><span data-stu-id="c6a49-122">Let's say you created this table using hello default distribution type of `ROUND_ROBIN` distributed since no distribution column was specified in hello `CREATE TABLE`.</span></span>

```sql
CREATE TABLE FactInternetSales
(
    ProductKey int NOT NULL,
    OrderDateKey int NOT NULL,
    DueDateKey int NOT NULL,
    ShipDateKey int NOT NULL,
    CustomerKey int NOT NULL,
    PromotionKey int NOT NULL,
    CurrencyKey int NOT NULL,
    SalesTerritoryKey int NOT NULL,
    SalesOrderNumber nvarchar(20) NOT NULL,
    SalesOrderLineNumber tinyint NOT NULL,
    RevisionNumber tinyint NOT NULL,
    OrderQuantity smallint NOT NULL,
    UnitPrice money NOT NULL,
    ExtendedAmount money NOT NULL,
    UnitPriceDiscountPct float NOT NULL,
    DiscountAmount float NOT NULL,
    ProductStandardCost money NOT NULL,
    TotalProductCost money NOT NULL,
    SalesAmount money NOT NULL,
    TaxAmt money NOT NULL,
    Freight money NOT NULL,
    CarrierTrackingNumber nvarchar(25),
    CustomerPONumber nvarchar(25)
);
```

<span data-ttu-id="c6a49-123">Agora você deseja toocreate uma nova cópia da tabela com um índice Columnstore clusterizado, para que você pode tirar proveito do desempenho de saudação do tabelas Columnstore clusterizado.</span><span class="sxs-lookup"><span data-stu-id="c6a49-123">Now you want toocreate a new copy of this table with a Clustered Columnstore Index so that you can take advantage of hello performance of Clustered Columnstore tables.</span></span> <span data-ttu-id="c6a49-124">Você também deseja toodistribute essa tabela na ProductKey desde que você está prevendo junções nessa coluna e deseja tooavoid a movimentação de dados durante a junções em ProductKey.</span><span class="sxs-lookup"><span data-stu-id="c6a49-124">You also want toodistribute this table on ProductKey since you are anticipating joins on this column and want tooavoid data movement during joins on ProductKey.</span></span> <span data-ttu-id="c6a49-125">Por fim deseja tooadd particionamento em OrderDateKey para que você pode excluir dados antigos, soltando partições antigas.</span><span class="sxs-lookup"><span data-stu-id="c6a49-125">Lastly you also want tooadd partitioning on OrderDateKey so that you can quickly delete old data by dropping old partitions.</span></span> <span data-ttu-id="c6a49-126">Aqui está a instrução CTAS Olá copie a tabela antiga para uma nova tabela.</span><span class="sxs-lookup"><span data-stu-id="c6a49-126">Here is hello CTAS statement which would copy your old table into a new table.</span></span>

```sql
CREATE TABLE FactInternetSales_new
WITH
(
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = HASH(ProductKey),
    PARTITION
    (
        OrderDateKey RANGE RIGHT FOR VALUES
        (
        20000101,20010101,20020101,20030101,20040101,20050101,20060101,20070101,20080101,20090101,
        20100101,20110101,20120101,20130101,20140101,20150101,20160101,20170101,20180101,20190101,
        20200101,20210101,20220101,20230101,20240101,20250101,20260101,20270101,20280101,20290101
        )
    )
)
AS SELECT * FROM FactInternetSales;
```

<span data-ttu-id="c6a49-127">Finalmente você pode renomear seu tooswap tabelas em sua nova tabela e, em seguida, remova a tabela antiga.</span><span class="sxs-lookup"><span data-stu-id="c6a49-127">Finally you can rename your tables tooswap in your new table and then drop your old table.</span></span>

```sql
RENAME OBJECT FactInternetSales tooFactInternetSales_old;
RENAME OBJECT FactInternetSales_new tooFactInternetSales;

DROP TABLE FactInternetSales_old;
```

> [!NOTE]
> <span data-ttu-id="c6a49-128">O SQL Data Warehouse do Azure ainda não dá suporte a estatísticas de criação ou atualização automática.</span><span class="sxs-lookup"><span data-stu-id="c6a49-128">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="c6a49-129">Em ordem tooget Olá melhor desempenho de suas consultas, é importante que ser criadas estatísticas em todas as colunas de todas as tabelas após a primeira carga de saudação ou alterações substanciais ocorrerem nos dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="c6a49-129">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span>  <span data-ttu-id="c6a49-130">Para obter uma explicação detalhada de estatísticas, consulte Olá [estatísticas] [ Statistics] tópico no grupo de desenvolver Olá de tópicos.</span><span class="sxs-lookup"><span data-stu-id="c6a49-130">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span>
> 
> 

## <a name="using-ctas-toowork-around-unsupported-features"></a><span data-ttu-id="c6a49-131">Usando toowork CTAS em torno de recursos sem suporte</span><span class="sxs-lookup"><span data-stu-id="c6a49-131">Using CTAS toowork around unsupported features</span></span>
<span data-ttu-id="c6a49-132">`CTAS`também pode ser usado toowork em torno de uma série de recursos de saudação sem suporte listados abaixo.</span><span class="sxs-lookup"><span data-stu-id="c6a49-132">`CTAS` can also be used toowork around a number of hello unsupported features listed below.</span></span> <span data-ttu-id="c6a49-133">Isso pode geralmente se Mostrar toobe win/ganham não só será compatível com seu código, mas serão geralmente executadas mais rapidamente no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c6a49-133">This can often prove toobe a win/win situation as not only will your code be compliant but it will often execute faster on SQL Data Warehouse.</span></span> <span data-ttu-id="c6a49-134">Isso é devido ao seu design totalmente em paralelo.</span><span class="sxs-lookup"><span data-stu-id="c6a49-134">This is as a result of its fully parallelized design.</span></span> <span data-ttu-id="c6a49-135">Os cenários que podem ser solucionados com CTAS incluem:</span><span class="sxs-lookup"><span data-stu-id="c6a49-135">Scenarios that can be worked around with CTAS include:</span></span>

* <span data-ttu-id="c6a49-136">ANSI JOINS em instruções UPDATE</span><span class="sxs-lookup"><span data-stu-id="c6a49-136">ANSI JOINS on UPDATEs</span></span>
* <span data-ttu-id="c6a49-137">ANSI JOINs em instruções DELETE</span><span class="sxs-lookup"><span data-stu-id="c6a49-137">ANSI JOINs on DELETEs</span></span>
* <span data-ttu-id="c6a49-138">Instrução MERGE</span><span class="sxs-lookup"><span data-stu-id="c6a49-138">MERGE statement</span></span>

> [!NOTE]
> <span data-ttu-id="c6a49-139">Tente toothink "CTAS primeiro".</span><span class="sxs-lookup"><span data-stu-id="c6a49-139">Try toothink "CTAS first".</span></span> <span data-ttu-id="c6a49-140">Se você achar que é possível resolver um problema usando `CTAS` que geralmente é Olá melhor maneira tooapproach-- mesmo se você está gravando os dados mais como resultado.</span><span class="sxs-lookup"><span data-stu-id="c6a49-140">If you think you can solve a problem using `CTAS` then that is generally hello best way tooapproach it - even if you are writing more data as a result.</span></span>
> 
> 

## <a name="ansi-join-replacement-for-update-statements"></a><span data-ttu-id="c6a49-141">Substituição da junção ANSI para atualizar instruções</span><span class="sxs-lookup"><span data-stu-id="c6a49-141">ANSI join replacement for update statements</span></span>
<span data-ttu-id="c6a49-142">Você pode achar que uma atualização complexa que une mais de duas tabelas usando ANSI unindo Olá de tooperform sintaxe UPDATE ou DELETE.</span><span class="sxs-lookup"><span data-stu-id="c6a49-142">You may find you have a complex update that joins more than two tables together using ANSI joining syntax tooperform hello UPDATE or DELETE.</span></span>

<span data-ttu-id="c6a49-143">Imagine que você tinha tooupdate nesta tabela:</span><span class="sxs-lookup"><span data-stu-id="c6a49-143">Imagine you had tooupdate this table:</span></span>

```sql
CREATE TABLE [dbo].[AnnualCategorySales]
(    [EnglishProductCategoryName]    NVARCHAR(50)    NOT NULL
,    [CalendarYear]                    SMALLINT        NOT NULL
,    [TotalSalesAmount]                MONEY            NOT NULL
)
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
;
```

<span data-ttu-id="c6a49-144">consulta original Olá pode se parecer com isso:</span><span class="sxs-lookup"><span data-stu-id="c6a49-144">hello original query might have looked something like this:</span></span>

```sql
UPDATE    acs
SET        [TotalSalesAmount] = [fis].[TotalSalesAmount]
FROM    [dbo].[AnnualCategorySales]     AS acs
JOIN    (
        SELECT    [EnglishProductCategoryName]
        ,        [CalendarYear]
        ,        SUM([SalesAmount])                AS [TotalSalesAmount]
        FROM    [dbo].[FactInternetSales]        AS s
        JOIN    [dbo].[DimDate]                    AS d    ON s.[OrderDateKey]                = d.[DateKey]
        JOIN    [dbo].[DimProduct]                AS p    ON s.[ProductKey]                = p.[ProductKey]
        JOIN    [dbo].[DimProductSubCategory]    AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
        JOIN    [dbo].[DimProductCategory]        AS c    ON u.[ProductCategoryKey]        = c.[ProductCategoryKey]
        WHERE     [CalendarYear] = 2004
        GROUP BY
                [EnglishProductCategoryName]
        ,        [CalendarYear]
        ) AS fis
ON    [acs].[EnglishProductCategoryName]    = [fis].[EnglishProductCategoryName]
AND    [acs].[CalendarYear]                = [fis].[CalendarYear]
;
```

<span data-ttu-id="c6a49-145">Desde que não oferece suporte a SQL Data Warehouse ANSI junções na Olá `FROM` cláusula de um `UPDATE` instrução, você não pode copiar este código sobre sem alterá-lo um pouco.</span><span class="sxs-lookup"><span data-stu-id="c6a49-145">Since SQL Data Warehouse does not support ANSI joins in hello `FROM` clause of an `UPDATE` statement, you cannot copy this code over without changing it slightly.</span></span>

<span data-ttu-id="c6a49-146">Você pode usar uma combinação de um `CTAS` e implícita ingressar tooreplace este código:</span><span class="sxs-lookup"><span data-stu-id="c6a49-146">You can use a combination of a `CTAS` and an implicit join tooreplace this code:</span></span>

```sql
-- Create an interim table
CREATE TABLE CTAS_acs
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT    ISNULL(CAST([EnglishProductCategoryName] AS NVARCHAR(50)),0)    AS [EnglishProductCategoryName]
,        ISNULL(CAST([CalendarYear] AS SMALLINT),0)                         AS [CalendarYear]
,        ISNULL(CAST(SUM([SalesAmount]) AS MONEY),0)                        AS [TotalSalesAmount]
FROM    [dbo].[FactInternetSales]        AS s
JOIN    [dbo].[DimDate]                    AS d    ON s.[OrderDateKey]                = d.[DateKey]
JOIN    [dbo].[DimProduct]                AS p    ON s.[ProductKey]                = p.[ProductKey]
JOIN    [dbo].[DimProductSubCategory]    AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
JOIN    [dbo].[DimProductCategory]        AS c    ON u.[ProductCategoryKey]        = c.[ProductCategoryKey]
WHERE     [CalendarYear] = 2004
GROUP BY
        [EnglishProductCategoryName]
,        [CalendarYear]
;

-- Use an implicit join tooperform hello update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop hello interim table
DROP TABLE CTAS_acs
;
```

## <a name="ansi-join-replacement-for-delete-statements"></a><span data-ttu-id="c6a49-147">Substituição de junção ANSI para instruções delete</span><span class="sxs-lookup"><span data-stu-id="c6a49-147">ANSI join replacement for delete statements</span></span>
<span data-ttu-id="c6a49-148">Às vezes, a melhor abordagem Olá para exclusão de dados é toouse `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="c6a49-148">Sometimes hello best approach for deleting data is toouse `CTAS`.</span></span> <span data-ttu-id="c6a49-149">Em vez de excluir dados Olá simplesmente selecione Olá dados tookeep.</span><span class="sxs-lookup"><span data-stu-id="c6a49-149">Rather than deleting hello data simply select hello data you want tookeep.</span></span> <span data-ttu-id="c6a49-150">Este especialmente verdadeiro para `DELETE` instruções que usam ansi unindo sintaxe desde que o SQL Data Warehouse não oferece suporte a junções de ANSI em Olá `FROM` cláusula de um `DELETE` instrução.</span><span class="sxs-lookup"><span data-stu-id="c6a49-150">This especially true for `DELETE` statements that use ansi joining syntax since SQL Data Warehouse does not support ANSI joins in hello `FROM` clause of a `DELETE` statement.</span></span>

<span data-ttu-id="c6a49-151">Um exemplo de uma instrução DELETE convertida está disponível abaixo:</span><span class="sxs-lookup"><span data-stu-id="c6a49-151">An example of a converted DELETE statement is available below:</span></span>

```sql
CREATE TABLE dbo.DimProduct_upsert
WITH
(   Distribution=HASH(ProductKey)
,   CLUSTERED INDEX (ProductKey)
)
AS -- Select Data you wish tookeep
SELECT     p.ProductKey
,          p.EnglishProductName
,          p.Color
FROM       dbo.DimProduct p
RIGHT JOIN dbo.stg_DimProduct s
ON         p.ProductKey = s.ProductKey
;

RENAME OBJECT dbo.DimProduct        tooDimProduct_old;
RENAME OBJECT dbo.DimProduct_upsert tooDimProduct;
```

## <a name="replace-merge-statements"></a><span data-ttu-id="c6a49-152">Substituir instruções merge</span><span class="sxs-lookup"><span data-stu-id="c6a49-152">Replace merge statements</span></span>
<span data-ttu-id="c6a49-153">Instruções de mesclagem podem ser substituídas, pelo menos em parte, usando `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="c6a49-153">Merge statements can be replaced, at least in part, by using `CTAS`.</span></span> <span data-ttu-id="c6a49-154">Você pode consolidar Olá `INSERT` e hello `UPDATE` em uma única instrução.</span><span class="sxs-lookup"><span data-stu-id="c6a49-154">You can consolidate hello `INSERT` and hello `UPDATE` into a single statement.</span></span> <span data-ttu-id="c6a49-155">Quaisquer registros excluídos precisaria toobe fechada em uma segunda instrução.</span><span class="sxs-lookup"><span data-stu-id="c6a49-155">Any deleted records would need toobe closed off in a second statement.</span></span>

<span data-ttu-id="c6a49-156">Um exemplo de uma instrução `UPSERT` está disponível abaixo:</span><span class="sxs-lookup"><span data-stu-id="c6a49-156">An example of an `UPSERT` is available below:</span></span>

```sql
CREATE TABLE dbo.[DimProduct_upsert]
WITH
(   DISTRIBUTION = HASH([ProductKey])
,   CLUSTERED INDEX ([ProductKey])
)
AS
-- New rows and new versions of rows
SELECT      s.[ProductKey]
,           s.[EnglishProductName]
,           s.[Color]
FROM      dbo.[stg_DimProduct] AS s
UNION ALL  
-- Keep rows that are not being touched
SELECT      p.[ProductKey]
,           p.[EnglishProductName]
,           p.[Color]
FROM      dbo.[DimProduct] AS p
WHERE NOT EXISTS
(   SELECT  *
    FROM    [dbo].[stg_DimProduct] s
    WHERE   s.[ProductKey] = p.[ProductKey]
)
;

RENAME OBJECT dbo.[DimProduct]          too[DimProduct_old];
RENAME OBJECT dbo.[DimpProduct_upsert]  too[DimProduct];

```

## <a name="ctas-recommendation-explicitly-state-data-type-and-nullability-of-output"></a><span data-ttu-id="c6a49-157">Recomendação de CTAS: declarar explicitamente o tipo de dados e a nulidade da saída</span><span class="sxs-lookup"><span data-stu-id="c6a49-157">CTAS recommendation: Explicitly state data type and nullability of output</span></span>
<span data-ttu-id="c6a49-158">Ao migrar o código, você pode achar executar por esse tipo de padrão de codificação:</span><span class="sxs-lookup"><span data-stu-id="c6a49-158">When migrating code you might find you run across this type of coding pattern:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE result
(result DECIMAL(7,2) NOT NULL
)
WITH (DISTRIBUTION = ROUND_ROBIN)

INSERT INTO result
SELECT @d*@f
;
```

<span data-ttu-id="c6a49-159">Instintivamente, você pode pensar tooa esse código CTAS devem ser migrados e você está correto.</span><span class="sxs-lookup"><span data-stu-id="c6a49-159">Instinctively you might think you should migrate this code tooa CTAS and you would be correct.</span></span> <span data-ttu-id="c6a49-160">No entanto, há um problema oculto aqui.</span><span class="sxs-lookup"><span data-stu-id="c6a49-160">However, there is a hidden issue here.</span></span>

<span data-ttu-id="c6a49-161">Olá código a seguir não geram Olá mesmo resultado:</span><span class="sxs-lookup"><span data-stu-id="c6a49-161">hello following code does NOT yield hello same result:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455
;

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT @d*@f as result
;
```

<span data-ttu-id="c6a49-162">Observe o resultado"hello coluna" carrega com os valores hello tipo e a nulidade de dados da expressão de saudação.</span><span class="sxs-lookup"><span data-stu-id="c6a49-162">Notice that hello column "result" carries forward hello data type and nullability values of hello expression.</span></span> <span data-ttu-id="c6a49-163">Isso pode levar toosubtle variações nos valores se você não tiver cuidado.</span><span class="sxs-lookup"><span data-stu-id="c6a49-163">This can lead toosubtle variances in values if you aren't careful.</span></span>

<span data-ttu-id="c6a49-164">Tente o seguinte hello como um exemplo:</span><span class="sxs-lookup"><span data-stu-id="c6a49-164">Try hello following as an example:</span></span>

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

<span data-ttu-id="c6a49-165">Olá valor armazenado para o resultado é diferente.</span><span class="sxs-lookup"><span data-stu-id="c6a49-165">hello value stored for result is different.</span></span> <span data-ttu-id="c6a49-166">Como hello persistente valor na coluna de resultado de saudação é usado em outras expressões Olá erro torna-se ainda mais significativo.</span><span class="sxs-lookup"><span data-stu-id="c6a49-166">As hello persisted value in hello result column is used in other expressions hello error becomes even more significant.</span></span>

![][1]

<span data-ttu-id="c6a49-167">Isso é particularmente importante para migrações de dados.</span><span class="sxs-lookup"><span data-stu-id="c6a49-167">This is particularly important for data migrations.</span></span> <span data-ttu-id="c6a49-168">Mesmo que a segunda consulta de saudação é indiscutivelmente mais precisa, há um problema.</span><span class="sxs-lookup"><span data-stu-id="c6a49-168">Even though hello second query is arguably more accurate there is a problem.</span></span> <span data-ttu-id="c6a49-169">dados de saudação seriam diferentes toohello em comparação com o sistema de origem e que leva tooquestions de integridade na migração de saudação.</span><span class="sxs-lookup"><span data-stu-id="c6a49-169">hello data would be different compared toohello source system and that leads tooquestions of integrity in hello migration.</span></span> <span data-ttu-id="c6a49-170">Esta é uma das raros casos em que a resposta "incorreto" hello é realmente saudação à direita um!</span><span class="sxs-lookup"><span data-stu-id="c6a49-170">This is one of those rare cases where hello "wrong" answer is actually hello right one!</span></span>

<span data-ttu-id="c6a49-171">Olá motivo, podemos ver essa discrepância entre resultados Olá dois está inoperante tooimplicit conversão de tipo.</span><span class="sxs-lookup"><span data-stu-id="c6a49-171">hello reason we see this disparity between hello two results is down tooimplicit type casting.</span></span> <span data-ttu-id="c6a49-172">No Olá a primeira tabela do exemplo hello define definição de coluna Olá.</span><span class="sxs-lookup"><span data-stu-id="c6a49-172">In hello first example hello table defines hello column definition.</span></span> <span data-ttu-id="c6a49-173">Quando a linha hello é inserida ocorre uma conversão implícita de tipo.</span><span class="sxs-lookup"><span data-stu-id="c6a49-173">When hello row is inserted an implicit type conversion occurs.</span></span> <span data-ttu-id="c6a49-174">No segundo exemplo de saudação não há nenhuma conversão implícita de tipo como expressão Olá define o tipo de dados da coluna de saudação.</span><span class="sxs-lookup"><span data-stu-id="c6a49-174">In hello second example there is no implicit type conversion as hello expression defines data type of hello column.</span></span> <span data-ttu-id="c6a49-175">Observe que também que a coluna Olá no segundo exemplo de saudação foi definida como uma coluna anulável enquanto o primeiro exemplo de saudação não tem.</span><span class="sxs-lookup"><span data-stu-id="c6a49-175">Notice also that hello column in hello second example has been defined as a NULLable column whereas in hello first example it has not.</span></span> <span data-ttu-id="c6a49-176">Quando Olá tabela foi criada no primeiro nulidade da coluna exemplo hello foi definida explicitamente.</span><span class="sxs-lookup"><span data-stu-id="c6a49-176">When hello table was created in hello first example column nullability was explicitly defined.</span></span> <span data-ttu-id="c6a49-177">No segundo exemplo de hello apenas estava toohello expressão e, por padrão, isso pode resultar em uma definição de NULL.</span><span class="sxs-lookup"><span data-stu-id="c6a49-177">In hello second example it was just left toohello expression and by default this would result in a NULL definition.</span></span>  

<span data-ttu-id="c6a49-178">tooresolve esses problemas que você deve definir explicitamente a conversão de tipo hello e nulidade em Olá `SELECT` parte da saudação `CTAS` instrução.</span><span class="sxs-lookup"><span data-stu-id="c6a49-178">tooresolve these issues you must explicitly set hello type conversion and nullability in hello `SELECT` portion of hello `CTAS` statement.</span></span> <span data-ttu-id="c6a49-179">Não é possível definir essas propriedades no hello criam parte da tabela.</span><span class="sxs-lookup"><span data-stu-id="c6a49-179">You cannot set these properties in hello create table part.</span></span>

<span data-ttu-id="c6a49-180">exemplo Hello abaixo demonstra como toofix Olá código:</span><span class="sxs-lookup"><span data-stu-id="c6a49-180">hello example below demonstrates how toofix hello code:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

<span data-ttu-id="c6a49-181">Observe o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="c6a49-181">Note hello following:</span></span>

* <span data-ttu-id="c6a49-182">CAST ou CONVERT poderia ter sido usado</span><span class="sxs-lookup"><span data-stu-id="c6a49-182">CAST or CONVERT could have been used</span></span>
* <span data-ttu-id="c6a49-183">ISNULL é usada tooforce nulidade ADESÃO não</span><span class="sxs-lookup"><span data-stu-id="c6a49-183">ISNULL is used tooforce NULLability not COALESCE</span></span>
* <span data-ttu-id="c6a49-184">ISNULL é função mais externa Olá</span><span class="sxs-lookup"><span data-stu-id="c6a49-184">ISNULL is hello outermost function</span></span>
* <span data-ttu-id="c6a49-185">Olá segunda parte da saudação ISNULL é uma constante ou seja, 0</span><span class="sxs-lookup"><span data-stu-id="c6a49-185">hello second part of hello ISNULL is a constant i.e. 0</span></span>

> [!NOTE]
> <span data-ttu-id="c6a49-186">Olá nulidade toobe definida corretamente é vital toouse `ISNULL` e não `COALESCE`.</span><span class="sxs-lookup"><span data-stu-id="c6a49-186">For hello nullability toobe correctly set it is vital toouse `ISNULL` and not `COALESCE`.</span></span> <span data-ttu-id="c6a49-187">`COALESCE`não é uma função determinística e então Olá resultado da saudação expressão será sempre NULLable.</span><span class="sxs-lookup"><span data-stu-id="c6a49-187">`COALESCE` is not a deterministic function and so hello result of hello expression will always be NULLable.</span></span> <span data-ttu-id="c6a49-188">`ISNULL` é diferente.</span><span class="sxs-lookup"><span data-stu-id="c6a49-188">`ISNULL` is different.</span></span> <span data-ttu-id="c6a49-189">É determinístico.</span><span class="sxs-lookup"><span data-stu-id="c6a49-189">It is deterministic.</span></span> <span data-ttu-id="c6a49-190">Quando Olá, portanto, a segunda parte da saudação `ISNULL` função é uma constante ou um literal, o valor resultante hello serão não nulo.</span><span class="sxs-lookup"><span data-stu-id="c6a49-190">Therefore when hello second part of hello `ISNULL` function is a constant or a literal then hello resulting value will be NOT NULL.</span></span>
> 
> 

<span data-ttu-id="c6a49-191">Esta dica não é útil apenas para assegurar a integridade de saudação de seus cálculos.</span><span class="sxs-lookup"><span data-stu-id="c6a49-191">This tip is not just useful for ensuring hello integrity of your calculations.</span></span> <span data-ttu-id="c6a49-192">Também é importante para a alternância de partição de tabela.</span><span class="sxs-lookup"><span data-stu-id="c6a49-192">It is also important for table partition switching.</span></span> <span data-ttu-id="c6a49-193">Imagine que você tenha essa tabela definida como o caso:</span><span class="sxs-lookup"><span data-stu-id="c6a49-193">Imagine you have this table defined as your fact:</span></span>

```sql
CREATE TABLE [dbo].[Sales]
(
    [date]      INT     NOT NULL
,   [product]   INT     NOT NULL
,   [store]     INT     NOT NULL
,   [quantity]  INT     NOT NULL
,   [price]     MONEY   NOT NULL
,   [amount]    MONEY   NOT NULL
)
WITH
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

<span data-ttu-id="c6a49-194">No entanto, o campo de valor de saudação é uma expressão calculada não faz parte dos dados de origem de saudação.</span><span class="sxs-lookup"><span data-stu-id="c6a49-194">However, hello value field is a calculated expression it is not part of hello source data.</span></span>

<span data-ttu-id="c6a49-195">toocreate seu conjunto de dados particionado, talvez você queira toodo isso:</span><span class="sxs-lookup"><span data-stu-id="c6a49-195">toocreate your partitioned dataset you might want toodo this:</span></span>

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   [quantity]*[price]  AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create')
;
```

<span data-ttu-id="c6a49-196">consulta de saudação será executado perfeitamente normal.</span><span class="sxs-lookup"><span data-stu-id="c6a49-196">hello query would run perfectly fine.</span></span> <span data-ttu-id="c6a49-197">problema de saudação é fornecido quando você tenta a alternância de partição tooperform Olá.</span><span class="sxs-lookup"><span data-stu-id="c6a49-197">hello problem comes when you try tooperform hello partition switch.</span></span> <span data-ttu-id="c6a49-198">definições de tabela Olá não coincidem.</span><span class="sxs-lookup"><span data-stu-id="c6a49-198">hello table definitions do not match.</span></span> <span data-ttu-id="c6a49-199">definições de tabela Olá toomake encontrar hello que CTAS precisa toobe modificado.</span><span class="sxs-lookup"><span data-stu-id="c6a49-199">toomake hello table definitions match hello CTAS needs toobe modified.</span></span>

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   ISNULL(CAST([quantity]*[price] AS MONEY),0) AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create');
```

<span data-ttu-id="c6a49-200">Você pode ver, portanto, que a consistência de tipo e manutenção das propriedades de nulidade em um CTAS é uma boa prática recomendada de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="c6a49-200">You can see therefore that type consistency and maintaining nullability properties on a CTAS is a good engineering best practice.</span></span> <span data-ttu-id="c6a49-201">Ele ajuda a integridade de toomaintain em seus cálculos e também garante que a alternância de partição é possível.</span><span class="sxs-lookup"><span data-stu-id="c6a49-201">It helps toomaintain integrity in your calculations and also ensures that partition switching is possible.</span></span>

<span data-ttu-id="c6a49-202">Consulte para obter mais informações sobre como usar tooMSDN [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="c6a49-202">Please refer tooMSDN for more information on using [CTAS][CTAS].</span></span> <span data-ttu-id="c6a49-203">É uma das instruções de hello mais importantes no Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c6a49-203">It is one of hello most important statements in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="c6a49-204">Certifique-se compreendê-la totalmente.</span><span class="sxs-lookup"><span data-stu-id="c6a49-204">Make sure you thoroughly understand it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6a49-205">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c6a49-205">Next steps</span></span>
<span data-ttu-id="c6a49-206">Para obter mais dicas de desenvolvimento, confira [visão geral de desenvolvimento][development overview].</span><span class="sxs-lookup"><span data-stu-id="c6a49-206">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-ctas/ctas-results.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[CTAS]: https://msdn.microsoft.com/library/mt204041.aspx

<!--Other Web references-->
