---
title: CTAS (create table as select) no SQL Data Warehouse | Microsoft Docs
description: "Dicas para codificação com a instrução create table as select (CTAS) no SQL Data Warehouse do Azure para desenvolvimento de soluções."
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
ms.openlocfilehash: cb08313726e8135feaa9b413937c2197ea397f4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-table-as-select-ctas-in-sql-data-warehouse"></a><span data-ttu-id="2f3b6-103">Instrução Create Table As Select (CTAS) no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="2f3b6-103">Create Table As Select (CTAS) in SQL Data Warehouse</span></span>
<span data-ttu-id="2f3b6-104">Create table as select ou `CTAS` é um dos recursos do T-SQL mais importantes disponíveis.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-104">Create table as select or `CTAS` is one of the most important T-SQL features available.</span></span> <span data-ttu-id="2f3b6-105">É uma operação totalmente em paralelo que cria uma nova tabela com base na saída de uma instrução SELECT.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-105">It is a fully parallelized operation that creates a new table based on the output of a SELECT statement.</span></span> <span data-ttu-id="2f3b6-106">`CTAS` é a maneira mais rápida e simples de criar uma cópia de uma tabela.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-106">`CTAS` is the simplest and fastest way to create a copy of a table.</span></span> <span data-ttu-id="2f3b6-107">Este documento fornece exemplos e melhores práticas para o `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-107">This document provides both examples and best practices for `CTAS`.</span></span>

## <a name="selectinto-vs-ctas"></a><span data-ttu-id="2f3b6-108">SELECT..INTO versus CTAS</span><span class="sxs-lookup"><span data-stu-id="2f3b6-108">SELECT..INTO vs. CTAS</span></span>
<span data-ttu-id="2f3b6-109">Você pode considerar `CTAS` como uma versão turbinada de `SELECT..INTO`.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-109">You can consider `CTAS` as a super-charged version of `SELECT..INTO`.</span></span>

<span data-ttu-id="2f3b6-110">Veja a seguir um exemplo de uma instrução `SELECT..INTO` simples:</span><span class="sxs-lookup"><span data-stu-id="2f3b6-110">Below is an example of a simple `SELECT..INTO` statement:</span></span>

```sql
SELECT *
INTO    [dbo].[FactInternetSales_new]
FROM    [dbo].[FactInternetSales]
```

<span data-ttu-id="2f3b6-111">No exemplo acima, `[dbo].[FactInternetSales_new]` seria criado como uma tabela distribuída por ROUND_ROBIN com um ÍNDICE DE COLUMNSTORE CLUSTERIZADO nela, pois esses são os padrões de tabela no Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-111">In the example above `[dbo].[FactInternetSales_new]` would be created as ROUND_ROBIN distributed table with a CLUSTERED COLUMNSTORE INDEX on it as these are the table defaults in Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="2f3b6-112">No entanto, `SELECT..INTO` não permite alterar o método de distribuição ou o tipo de índice como parte da operação.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-112">`SELECT..INTO` however does not allow you to change either the distribution method or the index type as part of the operation.</span></span> <span data-ttu-id="2f3b6-113">É aí que `CTAS` entra em cena.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-113">This is where `CTAS` comes in.</span></span>

<span data-ttu-id="2f3b6-114">Converter o acima para `CTAS` é bem simples:</span><span class="sxs-lookup"><span data-stu-id="2f3b6-114">To convert the above to `CTAS` is quite straight-forward:</span></span>

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

<span data-ttu-id="2f3b6-115">Com `CTAS`, você pode alterar a distribuição dos dados da tabela, bem como o tipo de tabela.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-115">With `CTAS` you are able to change both the distribution of the table data as well as the table type.</span></span> 

> [!NOTE]
> <span data-ttu-id="2f3b6-116">Se você estiver apenas tentando alterar o índice em sua operação `CTAS`, e a tabela de origem for distribuída por hash, sua operação `CTAS` executará melhor se você mantiver o mesmo tipo de coluna e dados de distribuição.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-116">If you are only trying to change the index in your `CTAS` operation and the source table is hash distributed then your `CTAS` operation will perform best if you maintain the same distribution column and data type.</span></span> <span data-ttu-id="2f3b6-117">Isso evitará a movimentação de dados de distribuição cruzada durante a operação, o que é mais eficiente.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-117">This will avoid cross distribution data movement during the operation which is more efficient.</span></span>
> 
> 

## <a name="using-ctas-to-copy-a-table"></a><span data-ttu-id="2f3b6-118">Usando o CTAS para copiar uma tabela</span><span class="sxs-lookup"><span data-stu-id="2f3b6-118">Using CTAS to copy a table</span></span>
<span data-ttu-id="2f3b6-119">Talvez um dos usos mais comuns do `CTAS` seja criar uma cópia de uma tabela para que você possa alterar a DDL.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-119">Perhaps one of the most common uses of `CTAS` is creating a copy of a table so that you can change the DDL.</span></span> <span data-ttu-id="2f3b6-120">Se, por exemplo, você originalmente tiver criado a tabela como `ROUND_ROBIN` e agora quiser alterá-la para uma tabela distribuída em uma coluna, `CTAS` é como você alteraria a coluna de distribuição.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-120">If for example you originally created your table as `ROUND_ROBIN` and now want change it to a table distributed on a column, `CTAS` is how you would change the distribution column.</span></span> <span data-ttu-id="2f3b6-121">`CTAS` também pode ser usado para alterar os tipos de particionamento, indexação ou coluna.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-121">`CTAS` can also be used to change partitioning, indexing, or column types.</span></span>

<span data-ttu-id="2f3b6-122">Digamos que você tenha criado essa tabela usando o tipo de distribuição padrão do `ROUND_ROBIN` distribuído, já que nenhuma coluna de distribuição foi especificada em `CREATE TABLE`.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-122">Let's say you created this table using the default distribution type of `ROUND_ROBIN` distributed since no distribution column was specified in the `CREATE TABLE`.</span></span>

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

<span data-ttu-id="2f3b6-123">Agora, você deseja criar uma nova cópia da tabela com um Índice Columnstore Clusterizado para que possa aproveitar o desempenho das tabelas Columnstore Clusterizado.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-123">Now you want to create a new copy of this table with a Clustered Columnstore Index so that you can take advantage of the performance of Clustered Columnstore tables.</span></span> <span data-ttu-id="2f3b6-124">Você também deseja distribuir essa tabela na ProductKey, uma vez que está antecipando as associações nessa coluna e quer evitar a movimentação dos dados durante as junções em ProductKey.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-124">You also want to distribute this table on ProductKey since you are anticipating joins on this column and want to avoid data movement during joins on ProductKey.</span></span> <span data-ttu-id="2f3b6-125">Por fim, também deseja adicionar o particionamento em OrderDateKey para que possa excluir rapidamente os dados antigos descartando as partições antigas.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-125">Lastly you also want to add partitioning on OrderDateKey so that you can quickly delete old data by dropping old partitions.</span></span> <span data-ttu-id="2f3b6-126">Aqui está a declaração CTAS que copiaria sua tabela antiga para uma nova tabela.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-126">Here is the CTAS statement which would copy your old table into a new table.</span></span>

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

<span data-ttu-id="2f3b6-127">Finalmente, você pode renomear suas tabelas para trocar na nova tabela, em seguida, descartar a tabela antiga.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-127">Finally you can rename your tables to swap in your new table and then drop your old table.</span></span>

```sql
RENAME OBJECT FactInternetSales TO FactInternetSales_old;
RENAME OBJECT FactInternetSales_new TO FactInternetSales;

DROP TABLE FactInternetSales_old;
```

> [!NOTE]
> <span data-ttu-id="2f3b6-128">O SQL Data Warehouse do Azure ainda não dá suporte às estatísticas de criação ou atualização automática.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-128">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="2f3b6-129">Para obter o melhor desempenho de suas consultas, é importante que as estatísticas sejam criadas em todas as colunas de todas as tabelas após o primeiro carregamento ou após uma alteração significativa nos dados.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-129">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span>  <span data-ttu-id="2f3b6-130">Para obter uma explicação detalhada das estatísticas, confira o tópico [Estatísticas][Statistics] no grupo de tópicos Desenvolver.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-130">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span>
> 
> 

## <a name="using-ctas-to-work-around-unsupported-features"></a><span data-ttu-id="2f3b6-131">Usando o CTAS para resolver os recursos sem suporte</span><span class="sxs-lookup"><span data-stu-id="2f3b6-131">Using CTAS to work around unsupported features</span></span>
<span data-ttu-id="2f3b6-132">`CTAS` também pode ser usado para solucionar os diversos recursos sem suporte listados abaixo.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-132">`CTAS` can also be used to work around a number of the unsupported features listed below.</span></span> <span data-ttu-id="2f3b6-133">Isso pode ser geralmente uma situação de ganho mútuo pois não apenas o seu código estará compatível, mas ele será executado muitas vezes mais rapidamente no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-133">This can often prove to be a win/win situation as not only will your code be compliant but it will often execute faster on SQL Data Warehouse.</span></span> <span data-ttu-id="2f3b6-134">Isso é devido ao seu design totalmente em paralelo.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-134">This is as a result of its fully parallelized design.</span></span> <span data-ttu-id="2f3b6-135">Os cenários que podem ser solucionados com CTAS incluem:</span><span class="sxs-lookup"><span data-stu-id="2f3b6-135">Scenarios that can be worked around with CTAS include:</span></span>

* <span data-ttu-id="2f3b6-136">ANSI JOINS em instruções UPDATE</span><span class="sxs-lookup"><span data-stu-id="2f3b6-136">ANSI JOINS on UPDATEs</span></span>
* <span data-ttu-id="2f3b6-137">ANSI JOINs em instruções DELETE</span><span class="sxs-lookup"><span data-stu-id="2f3b6-137">ANSI JOINs on DELETEs</span></span>
* <span data-ttu-id="2f3b6-138">Instrução MERGE</span><span class="sxs-lookup"><span data-stu-id="2f3b6-138">MERGE statement</span></span>

> [!NOTE]
> <span data-ttu-id="2f3b6-139">Tente imaginar “CTAS primeiro”.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-139">Try to think "CTAS first".</span></span> <span data-ttu-id="2f3b6-140">Caso você ache que pode resolver um problema usando `CTAS` , que geralmente é a melhor maneira de abordá-lo, mesmo se você está escrevendo mais dados como um resultado.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-140">If you think you can solve a problem using `CTAS` then that is generally the best way to approach it - even if you are writing more data as a result.</span></span>
> 
> 

## <a name="ansi-join-replacement-for-update-statements"></a><span data-ttu-id="2f3b6-141">Substituição da junção ANSI para atualizar instruções</span><span class="sxs-lookup"><span data-stu-id="2f3b6-141">ANSI join replacement for update statements</span></span>
<span data-ttu-id="2f3b6-142">Você pode descobrir uma atualização complexa que une mais de duas tabelas usando a sintaxe da junção ANSI para executar a UPDATE ou DELETE.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-142">You may find you have a complex update that joins more than two tables together using ANSI joining syntax to perform the UPDATE or DELETE.</span></span>

<span data-ttu-id="2f3b6-143">Imagine que você precisava atualizar esta tabela:</span><span class="sxs-lookup"><span data-stu-id="2f3b6-143">Imagine you had to update this table:</span></span>

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

<span data-ttu-id="2f3b6-144">A consulta original pode se parecer com isso:</span><span class="sxs-lookup"><span data-stu-id="2f3b6-144">The original query might have looked something like this:</span></span>

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

<span data-ttu-id="2f3b6-145">Já que o SQL Data Warehouse não dá suporte a junções ANSI na cláusula `FROM` da instrução `UPDATE`, você não pode copiar esse código sem alterá-lo um pouco.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-145">Since SQL Data Warehouse does not support ANSI joins in the `FROM` clause of an `UPDATE` statement, you cannot copy this code over without changing it slightly.</span></span>

<span data-ttu-id="2f3b6-146">Você pode usar uma combinação de um `CTAS` e uma junção implícita para substituir este código:</span><span class="sxs-lookup"><span data-stu-id="2f3b6-146">You can use a combination of a `CTAS` and an implicit join to replace this code:</span></span>

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

-- Use an implicit join to perform the update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop the interim table
DROP TABLE CTAS_acs
;
```

## <a name="ansi-join-replacement-for-delete-statements"></a><span data-ttu-id="2f3b6-147">Substituição de junção ANSI para instruções delete</span><span class="sxs-lookup"><span data-stu-id="2f3b6-147">ANSI join replacement for delete statements</span></span>
<span data-ttu-id="2f3b6-148">Às vezes, a melhor abordagem para a exclusão de dados é usar `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-148">Sometimes the best approach for deleting data is to use `CTAS`.</span></span> <span data-ttu-id="2f3b6-149">Em vez de excluir os dados, simplesmente selecione os dados que você deseja manter.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-149">Rather than deleting the data simply select the data you want to keep.</span></span> <span data-ttu-id="2f3b6-150">Isso é especialmente verdadeiro para instruções `DELETE` que usam sintaxe de junção ansi, já que o SQL Data Warehouse não dá suporte a junções ANSI na cláusula `FROM` de uma instrução `DELETE`.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-150">This especially true for `DELETE` statements that use ansi joining syntax since SQL Data Warehouse does not support ANSI joins in the `FROM` clause of a `DELETE` statement.</span></span>

<span data-ttu-id="2f3b6-151">Um exemplo de uma instrução DELETE convertida está disponível abaixo:</span><span class="sxs-lookup"><span data-stu-id="2f3b6-151">An example of a converted DELETE statement is available below:</span></span>

```sql
CREATE TABLE dbo.DimProduct_upsert
WITH
(   Distribution=HASH(ProductKey)
,   CLUSTERED INDEX (ProductKey)
)
AS -- Select Data you wish to keep
SELECT     p.ProductKey
,          p.EnglishProductName
,          p.Color
FROM       dbo.DimProduct p
RIGHT JOIN dbo.stg_DimProduct s
ON         p.ProductKey = s.ProductKey
;

RENAME OBJECT dbo.DimProduct        TO DimProduct_old;
RENAME OBJECT dbo.DimProduct_upsert TO DimProduct;
```

## <a name="replace-merge-statements"></a><span data-ttu-id="2f3b6-152">Substituir instruções merge</span><span class="sxs-lookup"><span data-stu-id="2f3b6-152">Replace merge statements</span></span>
<span data-ttu-id="2f3b6-153">Instruções de mesclagem podem ser substituídas, pelo menos em parte, usando `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-153">Merge statements can be replaced, at least in part, by using `CTAS`.</span></span> <span data-ttu-id="2f3b6-154">Você pode consolidar o `INSERT` e a `UPDATE` em uma única instrução.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-154">You can consolidate the `INSERT` and the `UPDATE` into a single statement.</span></span> <span data-ttu-id="2f3b6-155">Quaisquer registros excluídos precisariam ser fechados em uma segunda instrução.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-155">Any deleted records would need to be closed off in a second statement.</span></span>

<span data-ttu-id="2f3b6-156">Um exemplo de uma instrução `UPSERT` está disponível abaixo:</span><span class="sxs-lookup"><span data-stu-id="2f3b6-156">An example of an `UPSERT` is available below:</span></span>

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

RENAME OBJECT dbo.[DimProduct]          TO [DimProduct_old];
RENAME OBJECT dbo.[DimpProduct_upsert]  TO [DimProduct];

```

## <a name="ctas-recommendation-explicitly-state-data-type-and-nullability-of-output"></a><span data-ttu-id="2f3b6-157">Recomendação de CTAS: declarar explicitamente o tipo de dados e a nulidade da saída</span><span class="sxs-lookup"><span data-stu-id="2f3b6-157">CTAS recommendation: Explicitly state data type and nullability of output</span></span>
<span data-ttu-id="2f3b6-158">Ao migrar o código, você pode achar executar por esse tipo de padrão de codificação:</span><span class="sxs-lookup"><span data-stu-id="2f3b6-158">When migrating code you might find you run across this type of coding pattern:</span></span>

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

<span data-ttu-id="2f3b6-159">Instintivamente, é possível pensar que é necessário migrar esse código para um CTAS e você estaria certo.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-159">Instinctively you might think you should migrate this code to a CTAS and you would be correct.</span></span> <span data-ttu-id="2f3b6-160">No entanto, há um problema oculto aqui.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-160">However, there is a hidden issue here.</span></span>

<span data-ttu-id="2f3b6-161">O código a seguir NÃO produz o mesmo resultado:</span><span class="sxs-lookup"><span data-stu-id="2f3b6-161">The following code does NOT yield the same result:</span></span>

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

<span data-ttu-id="2f3b6-162">Observe que a coluna “resultado” transporta os valores de tipo e a nulidade de dados da expressão.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-162">Notice that the column "result" carries forward the data type and nullability values of the expression.</span></span> <span data-ttu-id="2f3b6-163">Se você não tiver cuidado, isso pode levar a variações sutis em valores.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-163">This can lead to subtle variances in values if you aren't careful.</span></span>

<span data-ttu-id="2f3b6-164">Tente o seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="2f3b6-164">Try the following as an example:</span></span>

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

<span data-ttu-id="2f3b6-165">O valor armazenado para o resultado é diferente.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-165">The value stored for result is different.</span></span> <span data-ttu-id="2f3b6-166">Como o valor persistente na coluna de resultado é usado em outras expressões, o erro se torna ainda mais significativo.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-166">As the persisted value in the result column is used in other expressions the error becomes even more significant.</span></span>

![][1]

<span data-ttu-id="2f3b6-167">Isso é particularmente importante para migrações de dados.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-167">This is particularly important for data migrations.</span></span> <span data-ttu-id="2f3b6-168">Mesmo que a segunda consulta seja indiscutivelmente mais precisa, há um problema.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-168">Even though the second query is arguably more accurate there is a problem.</span></span> <span data-ttu-id="2f3b6-169">Os dados seriam diferentes em comparação com o sistema de origem e que leva a questões de integridade da migração.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-169">The data would be different compared to the source system and that leads to questions of integrity in the migration.</span></span> <span data-ttu-id="2f3b6-170">Esse é um dos casos raros em que a resposta “incorreta” é realmente a melhor!</span><span class="sxs-lookup"><span data-stu-id="2f3b6-170">This is one of those rare cases where the "wrong" answer is actually the right one!</span></span>

<span data-ttu-id="2f3b6-171">O motivo que vemos esta disparidade entre os dois resultados é a conversão de tipo implícito.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-171">The reason we see this disparity between the two results is down to implicit type casting.</span></span> <span data-ttu-id="2f3b6-172">No primeiro exemplo, a tabela define a definição de coluna.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-172">In the first example the table defines the column definition.</span></span> <span data-ttu-id="2f3b6-173">Quando a linha é inserida uma conversão implícita de tipo ocorre.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-173">When the row is inserted an implicit type conversion occurs.</span></span> <span data-ttu-id="2f3b6-174">No segundo exemplo não há nenhuma conversão implícita de tipo como a expressão define o tipo de dados da coluna.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-174">In the second example there is no implicit type conversion as the expression defines data type of the column.</span></span> <span data-ttu-id="2f3b6-175">Observe também que a coluna no segundo exemplo tenha sido definida como uma coluna anulável, enquanto no primeiro exemplo não tem.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-175">Notice also that the column in the second example has been defined as a NULLable column whereas in the first example it has not.</span></span> <span data-ttu-id="2f3b6-176">Quando a tabela foi criada no primeiro exemplo, a nulidade da coluna foi explicitamente definida.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-176">When the table was created in the first example column nullability was explicitly defined.</span></span> <span data-ttu-id="2f3b6-177">No segundo exemplo, ela estava à esquerda da expressão e, por padrão isso resultaria em uma definição NULL.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-177">In the second example it was just left to the expression and by default this would result in a NULL definition.</span></span>  

<span data-ttu-id="2f3b6-178">Para resolver esses problemas, defina explicitamente a nulidade e conversão de tipo na parte `SELECT` da instrução `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-178">To resolve these issues you must explicitly set the type conversion and nullability in the `SELECT` portion of the `CTAS` statement.</span></span> <span data-ttu-id="2f3b6-179">Você não pode definir essas propriedades na parte criar tabela.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-179">You cannot set these properties in the create table part.</span></span>

<span data-ttu-id="2f3b6-180">O exemplo a seguir demonstra como corrigir o código:</span><span class="sxs-lookup"><span data-stu-id="2f3b6-180">The example below demonstrates how to fix the code:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

<span data-ttu-id="2f3b6-181">Observe o seguinte:</span><span class="sxs-lookup"><span data-stu-id="2f3b6-181">Note the following:</span></span>

* <span data-ttu-id="2f3b6-182">CAST ou CONVERT poderia ter sido usado</span><span class="sxs-lookup"><span data-stu-id="2f3b6-182">CAST or CONVERT could have been used</span></span>
* <span data-ttu-id="2f3b6-183">ISNULL é usado para forçar NULLability não COALESCE</span><span class="sxs-lookup"><span data-stu-id="2f3b6-183">ISNULL is used to force NULLability not COALESCE</span></span>
* <span data-ttu-id="2f3b6-184">ISNULL é a função mais externa</span><span class="sxs-lookup"><span data-stu-id="2f3b6-184">ISNULL is the outermost function</span></span>
* <span data-ttu-id="2f3b6-185">A segunda parte do ISNULL é uma constante, ou seja, 0</span><span class="sxs-lookup"><span data-stu-id="2f3b6-185">The second part of the ISNULL is a constant i.e. 0</span></span>

> [!NOTE]
> <span data-ttu-id="2f3b6-186">Para a nulidade ser definida corretamente, é vital usar `ISNULL`, e não `COALESCE`.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-186">For the nullability to be correctly set it is vital to use `ISNULL` and not `COALESCE`.</span></span> <span data-ttu-id="2f3b6-187">`COALESCE` não é uma função determinística, assim, o resultado da expressão sempre será anulável.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-187">`COALESCE` is not a deterministic function and so the result of the expression will always be NULLable.</span></span> <span data-ttu-id="2f3b6-188">`ISNULL` é diferente.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-188">`ISNULL` is different.</span></span> <span data-ttu-id="2f3b6-189">É determinístico.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-189">It is deterministic.</span></span> <span data-ttu-id="2f3b6-190">Portanto, quando a segunda parte da função `ISNULL` é uma constante ou um literal, o valor resultante será NOT NULL.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-190">Therefore when the second part of the `ISNULL` function is a constant or a literal then the resulting value will be NOT NULL.</span></span>
> 
> 

<span data-ttu-id="2f3b6-191">Esta dica não é apenas útil para assegurar a integridade de seus cálculos.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-191">This tip is not just useful for ensuring the integrity of your calculations.</span></span> <span data-ttu-id="2f3b6-192">Também é importante para a alternância de partição de tabela.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-192">It is also important for table partition switching.</span></span> <span data-ttu-id="2f3b6-193">Imagine que você tenha essa tabela definida como o caso:</span><span class="sxs-lookup"><span data-stu-id="2f3b6-193">Imagine you have this table defined as your fact:</span></span>

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

<span data-ttu-id="2f3b6-194">No entanto, o campo de valor é uma expressão calculada que não é parte dos dados de origem.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-194">However, the value field is a calculated expression it is not part of the source data.</span></span>

<span data-ttu-id="2f3b6-195">Para criar o conjunto de dados particionado, você poderia fazer isso:</span><span class="sxs-lookup"><span data-stu-id="2f3b6-195">To create your partitioned dataset you might want to do this:</span></span>

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

<span data-ttu-id="2f3b6-196">A consulta seria executada perfeitamente bem.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-196">The query would run perfectly fine.</span></span> <span data-ttu-id="2f3b6-197">O problema surge quando você tenta executar a opção de partição.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-197">The problem comes when you try to perform the partition switch.</span></span> <span data-ttu-id="2f3b6-198">As definições de tabela não correspondem.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-198">The table definitions do not match.</span></span> <span data-ttu-id="2f3b6-199">Para fazer com que as definições de tabela correspondam, a CTAS precisa ser modificada.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-199">To make the table definitions match the CTAS needs to be modified.</span></span>

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

<span data-ttu-id="2f3b6-200">Você pode ver, portanto, que a consistência de tipo e manutenção das propriedades de nulidade em um CTAS é uma boa prática recomendada de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-200">You can see therefore that type consistency and maintaining nullability properties on a CTAS is a good engineering best practice.</span></span> <span data-ttu-id="2f3b6-201">Ela ajuda a manter a integridade de seus cálculos e também garante que a alternância de partição é possível.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-201">It helps to maintain integrity in your calculations and also ensures that partition switching is possible.</span></span>

<span data-ttu-id="2f3b6-202">Consulte o MSDN para obter mais informações sobre como usar o [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="2f3b6-202">Please refer to MSDN for more information on using [CTAS][CTAS].</span></span> <span data-ttu-id="2f3b6-203">Ela é uma das instruções mais importantes no SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-203">It is one of the most important statements in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="2f3b6-204">Certifique-se compreendê-la totalmente.</span><span class="sxs-lookup"><span data-stu-id="2f3b6-204">Make sure you thoroughly understand it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f3b6-205">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2f3b6-205">Next steps</span></span>
<span data-ttu-id="2f3b6-206">Para obter mais dicas de desenvolvimento, confira [visão geral de desenvolvimento][development overview].</span><span class="sxs-lookup"><span data-stu-id="2f3b6-206">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-ctas/ctas-results.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[CTAS]: https://msdn.microsoft.com/library/mt204041.aspx

<!--Other Web references-->
