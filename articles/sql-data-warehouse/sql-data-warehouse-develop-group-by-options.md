---
title: "Agrupar por opções no SQL Data Warehouse | Microsoft Docs"
description: "Dicas para implementar o agrupamento por opções no SQL Data Warehouse do Azure para desenvolver soluções."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: f95a1e43-768f-4b7b-8a10-8a0509d0c871
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: da71cb834c13da5d0f5690f471efc6c696163f30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="group-by-options-in-sql-data-warehouse"></a><span data-ttu-id="ee9e7-103">Agrupar por opções de SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ee9e7-103">Group by options in SQL Data Warehouse</span></span>
<span data-ttu-id="ee9e7-104">A cláusula [GROUP BY][GROUP BY] é usada para agregar dados a um conjunto de linhas de resumo.</span><span class="sxs-lookup"><span data-stu-id="ee9e7-104">The [GROUP BY][GROUP BY] clause is used to aggregate data to a summary set of rows.</span></span> <span data-ttu-id="ee9e7-105">Ela também tem algumas opções que ampliam sua funcionalidade que precisam ser solucionadas pois não tem suporte diretamente pelo SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee9e7-105">It also has a few options that extend it's functionality that need to be worked around as they are not directly supported by Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="ee9e7-106">Essas opções são</span><span class="sxs-lookup"><span data-stu-id="ee9e7-106">These options are</span></span>

* <span data-ttu-id="ee9e7-107">GROUP BY com ROLLUP</span><span class="sxs-lookup"><span data-stu-id="ee9e7-107">GROUP BY with ROLLUP</span></span>
* <span data-ttu-id="ee9e7-108">GROUPING SETS</span><span class="sxs-lookup"><span data-stu-id="ee9e7-108">GROUPING SETS</span></span>
* <span data-ttu-id="ee9e7-109">GROUP BY com CUBE</span><span class="sxs-lookup"><span data-stu-id="ee9e7-109">GROUP BY with CUBE</span></span>

## <a name="rollup-and-grouping-sets-options"></a><span data-ttu-id="ee9e7-110">O rollup e o agrupamento definem opções</span><span class="sxs-lookup"><span data-stu-id="ee9e7-110">Rollup and grouping sets options</span></span>
<span data-ttu-id="ee9e7-111">A opção mais simples é usar `UNION ALL` ao invés de executar o rollup do que contar com a sintaxe explícita.</span><span class="sxs-lookup"><span data-stu-id="ee9e7-111">The simplest option here is to use `UNION ALL` instead to perform the rollup rather than relying on the explicit syntax.</span></span> <span data-ttu-id="ee9e7-112">O resultado é exatamente o mesmo</span><span class="sxs-lookup"><span data-stu-id="ee9e7-112">The result is exactly the same</span></span>

<span data-ttu-id="ee9e7-113">Abaixo está um exemplo de um agrupamento pela instrução usando a opção `ROLLUP` :</span><span class="sxs-lookup"><span data-stu-id="ee9e7-113">Below is an example of a group by statement using the `ROLLUP` option:</span></span>

```sql
SELECT [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
,      SUM(SalesAmount)             AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t       ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY ROLLUP (
                        [SalesTerritoryCountry]
                ,       [SalesTerritoryRegion]
                )
;
```

<span data-ttu-id="ee9e7-114">Ao usar ROLLUP, solicitamos as seguintes agregações:</span><span class="sxs-lookup"><span data-stu-id="ee9e7-114">By using ROLLUP we have requested the following aggregations:</span></span>

* <span data-ttu-id="ee9e7-115">país e região</span><span class="sxs-lookup"><span data-stu-id="ee9e7-115">Country and Region</span></span>
* <span data-ttu-id="ee9e7-116">País</span><span class="sxs-lookup"><span data-stu-id="ee9e7-116">Country</span></span>
* <span data-ttu-id="ee9e7-117">Grande Total</span><span class="sxs-lookup"><span data-stu-id="ee9e7-117">Grand Total</span></span>

<span data-ttu-id="ee9e7-118">Para substituir isso, você precisará usar `UNION ALL`; especificar as agregações explicitamente necessárias para retornar os mesmos resultados:</span><span class="sxs-lookup"><span data-stu-id="ee9e7-118">To replace this you will need to use `UNION ALL`; specifying the aggregations required explicitly to return the same results:</span></span>

```sql
SELECT [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY
       [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
UNION ALL
SELECT [SalesTerritoryCountry]
,      NULL
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY
       [SalesTerritoryCountry]
UNION ALL
SELECT NULL
,      NULL
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey;
```

<span data-ttu-id="ee9e7-119">Para GROUPING SETS, tudo o que precisamos fazer é adotar a mesma entidade principal, mas apenas criar seções UNION ALL para os níveis de agregação que queremos ver</span><span class="sxs-lookup"><span data-stu-id="ee9e7-119">For GROUPING SETS all we need to do is adopt the same principal but only create UNION ALL sections for the aggregation levels we want to see</span></span>

## <a name="cube-options"></a><span data-ttu-id="ee9e7-120">Opções Cube</span><span class="sxs-lookup"><span data-stu-id="ee9e7-120">Cube options</span></span>
<span data-ttu-id="ee9e7-121">É possível criar uma instrução GROUP BY WITH CUBE usando a abordagem UNION ALL.</span><span class="sxs-lookup"><span data-stu-id="ee9e7-121">It is possible to create a GROUP BY WITH CUBE using the UNION ALL approach.</span></span> <span data-ttu-id="ee9e7-122">O problema é que o código pode rapidamente se tornar complicado e difícil.</span><span class="sxs-lookup"><span data-stu-id="ee9e7-122">The problem is that the code can quickly become cumbersome and unwieldy.</span></span> <span data-ttu-id="ee9e7-123">Para atenuar isso, você pode usar essa abordagem mais avançada.</span><span class="sxs-lookup"><span data-stu-id="ee9e7-123">To mitigate this you can use this more advanced approach.</span></span>

<span data-ttu-id="ee9e7-124">Vamos usar o exemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="ee9e7-124">Let's use the example above.</span></span>

<span data-ttu-id="ee9e7-125">A primeira etapa é definir o ‘cube’ que define todos os níveis de agregação que desejamos criar.</span><span class="sxs-lookup"><span data-stu-id="ee9e7-125">The first step is to define the 'cube' that defines all the levels of aggregation that we want to create.</span></span> <span data-ttu-id="ee9e7-126">É importante que você observe o CROSS JOIN das duas tabelas derivadas.</span><span class="sxs-lookup"><span data-stu-id="ee9e7-126">It is important to take note of the CROSS JOIN of the two derived tables.</span></span> <span data-ttu-id="ee9e7-127">Isso gera todos os níveis.</span><span class="sxs-lookup"><span data-stu-id="ee9e7-127">This generates all the levels for us.</span></span> <span data-ttu-id="ee9e7-128">O restante do código está lá para formatação.</span><span class="sxs-lookup"><span data-stu-id="ee9e7-128">The rest of the code is really there for formatting.</span></span>

```sql
CREATE TABLE #Cube
WITH
(   DISTRIBUTION = ROUND_ROBIN
,   LOCATION = USER_DB
)
AS
WITH GrpCube AS
(SELECT    CAST(ISNULL(Country,'NULL')+','+ISNULL(Region,'NULL') AS NVARCHAR(50)) as 'Cols'
,          CAST(ISNULL(Country+',','')+ISNULL(Region,'') AS NVARCHAR(50))  as 'GroupBy'
,          ROW_NUMBER() OVER (ORDER BY Country) as 'Seq'
FROM       ( SELECT 'SalesTerritoryCountry' as Country
             UNION ALL
             SELECT NULL
           ) c
CROSS JOIN ( SELECT 'SalesTerritoryRegion' as Region
             UNION ALL
             SELECT NULL
           ) r
)
SELECT Cols
,      CASE WHEN SUBSTRING(GroupBy,LEN(GroupBy),1) = ','
            THEN SUBSTRING(GroupBy,1,LEN(GroupBy)-1)
            ELSE GroupBy
       END AS GroupBy  --Remove Trailing Comma
,Seq
FROM GrpCube;
```

<span data-ttu-id="ee9e7-129">Os resultados de CTAS podem ser vistos abaixo:</span><span class="sxs-lookup"><span data-stu-id="ee9e7-129">The results of the CTAS can be seen below:</span></span>

![][1]

<span data-ttu-id="ee9e7-130">A segunda etapa é especificar uma tabela de destino para armazenar os resultados intermediários:</span><span class="sxs-lookup"><span data-stu-id="ee9e7-130">The second step is to specify a target table to store interim results:</span></span>

```sql
DECLARE
 @SQL NVARCHAR(4000)
,@Columns NVARCHAR(4000)
,@GroupBy NVARCHAR(4000)
,@i INT = 1
,@nbr INT = 0
;
CREATE TABLE #Results
(
 [SalesTerritoryCountry] NVARCHAR(50)
,[SalesTerritoryRegion]  NVARCHAR(50)
,[TotalSalesAmount]      MONEY
)
WITH
(   DISTRIBUTION = ROUND_ROBIN
,   LOCATION = USER_DB
)
;
```

<span data-ttu-id="ee9e7-131">A terceira etapa é executar um loop sobre o cubo de colunas realizando a agregação.</span><span class="sxs-lookup"><span data-stu-id="ee9e7-131">The third step is to loop over our cube of columns performing the aggregation.</span></span> <span data-ttu-id="ee9e7-132">A consulta será executada uma vez para cada linha na tabela temporária #Cube e armazenará os resultados na tabela temporária #Results</span><span class="sxs-lookup"><span data-stu-id="ee9e7-132">The query will run once for every row in the #Cube temporary table and store the results in the #Results temp table</span></span>

```sql
SET @nbr =(SELECT MAX(Seq) FROM #Cube);

WHILE @i<=@nbr
BEGIN
    SET @Columns = (SELECT Cols    FROM #Cube where seq = @i);
    SET @GroupBy = (SELECT GroupBy FROM #Cube where seq = @i);

    SET @SQL ='INSERT INTO #Results
              SELECT '+@Columns+'
              ,      SUM(SalesAmount) AS TotalSalesAmount
              FROM  dbo.factInternetSales s
              JOIN  dbo.DimSalesTerritory t  
              ON s.SalesTerritoryKey = t.SalesTerritoryKey
              '+CASE WHEN @GroupBy <>''
                     THEN 'GROUP BY '+@GroupBy ELSE '' END

    EXEC sp_executesql @SQL;
    SET @i +=1;
END
```

<span data-ttu-id="ee9e7-133">Por fim, retornamos os resultados apenas lendo da tabela temporária #Results</span><span class="sxs-lookup"><span data-stu-id="ee9e7-133">Lastly we can return the results by simply reading from the #Results temporary table</span></span>

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

<span data-ttu-id="ee9e7-134">Dividir o código em seções e gerar uma construção de loop, torna o código mais gerenciável e sustentável.</span><span class="sxs-lookup"><span data-stu-id="ee9e7-134">By breaking the code up into sections and generating a looping construct the code becomes more manageable and maintainable.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee9e7-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ee9e7-135">Next steps</span></span>
<span data-ttu-id="ee9e7-136">Para obter mais dicas de desenvolvimento, confira [visão geral de desenvolvimento][development overview].</span><span class="sxs-lookup"><span data-stu-id="ee9e7-136">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->
