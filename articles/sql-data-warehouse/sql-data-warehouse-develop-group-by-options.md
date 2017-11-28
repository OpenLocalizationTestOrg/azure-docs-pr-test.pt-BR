---
title: "aaaGroup pelas opções no SQL Data Warehouse | Microsoft Docs"
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
ms.openlocfilehash: cc443c2af4e3ef2babd74d78aa6fb57bb3c1c7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="group-by-options-in-sql-data-warehouse"></a><span data-ttu-id="26915-103">Agrupar por opções de SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="26915-103">Group by options in SQL Data Warehouse</span></span>
<span data-ttu-id="26915-104">Olá [GROUP BY] [ GROUP BY] cláusula é utilizada tooaggregate tooa resumo conjunto de dados linhas.</span><span class="sxs-lookup"><span data-stu-id="26915-104">hello [GROUP BY][GROUP BY] clause is used tooaggregate data tooa summary set of rows.</span></span> <span data-ttu-id="26915-105">Ele também tem algumas opções que estendem sua funcionalidade que toobe necessidade contornado como não são diretamente suportados pelo Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="26915-105">It also has a few options that extend it's functionality that need toobe worked around as they are not directly supported by Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="26915-106">Essas opções são</span><span class="sxs-lookup"><span data-stu-id="26915-106">These options are</span></span>

* <span data-ttu-id="26915-107">GROUP BY com ROLLUP</span><span class="sxs-lookup"><span data-stu-id="26915-107">GROUP BY with ROLLUP</span></span>
* <span data-ttu-id="26915-108">GROUPING SETS</span><span class="sxs-lookup"><span data-stu-id="26915-108">GROUPING SETS</span></span>
* <span data-ttu-id="26915-109">GROUP BY com CUBE</span><span class="sxs-lookup"><span data-stu-id="26915-109">GROUP BY with CUBE</span></span>

## <a name="rollup-and-grouping-sets-options"></a><span data-ttu-id="26915-110">O rollup e o agrupamento definem opções</span><span class="sxs-lookup"><span data-stu-id="26915-110">Rollup and grouping sets options</span></span>
<span data-ttu-id="26915-111">Olá, aqui a opção mais simples é toouse `UNION ALL` em vez disso, tooperform Olá rollup em vez de depender Olá sintaxe explícito.</span><span class="sxs-lookup"><span data-stu-id="26915-111">hello simplest option here is toouse `UNION ALL` instead tooperform hello rollup rather than relying on hello explicit syntax.</span></span> <span data-ttu-id="26915-112">é o resultado de saudação exatamente Olá mesmo</span><span class="sxs-lookup"><span data-stu-id="26915-112">hello result is exactly hello same</span></span>

<span data-ttu-id="26915-113">Abaixo está um exemplo de um grupo pela instrução usando Olá `ROLLUP` opção:</span><span class="sxs-lookup"><span data-stu-id="26915-113">Below is an example of a group by statement using hello `ROLLUP` option:</span></span>

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

<span data-ttu-id="26915-114">Usando o pacote cumulativo de atualizações tenhamos solicitado Olá agregações a seguir:</span><span class="sxs-lookup"><span data-stu-id="26915-114">By using ROLLUP we have requested hello following aggregations:</span></span>

* <span data-ttu-id="26915-115">país e região</span><span class="sxs-lookup"><span data-stu-id="26915-115">Country and Region</span></span>
* <span data-ttu-id="26915-116">País</span><span class="sxs-lookup"><span data-stu-id="26915-116">Country</span></span>
* <span data-ttu-id="26915-117">Grande Total</span><span class="sxs-lookup"><span data-stu-id="26915-117">Grand Total</span></span>

<span data-ttu-id="26915-118">tooreplace isso será necessário toouse `UNION ALL`; especificando agregações Olá necessárias explicitamente tooreturn Olá os mesmos resultados:</span><span class="sxs-lookup"><span data-stu-id="26915-118">tooreplace this you will need toouse `UNION ALL`; specifying hello aggregations required explicitly tooreturn hello same results:</span></span>

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

<span data-ttu-id="26915-119">Para conjuntos de AGRUPAMENTOS tudo o que precisamos toodo é adotar Olá mesmo principal, mas apenas criar seções UNION ALL para Olá níveis de agregação que desejamos toosee</span><span class="sxs-lookup"><span data-stu-id="26915-119">For GROUPING SETS all we need toodo is adopt hello same principal but only create UNION ALL sections for hello aggregation levels we want toosee</span></span>

## <a name="cube-options"></a><span data-ttu-id="26915-120">Opções Cube</span><span class="sxs-lookup"><span data-stu-id="26915-120">Cube options</span></span>
<span data-ttu-id="26915-121">É possível toocreate um GROUP BY WITH CUBE usando a abordagem de saudação UNION ALL.</span><span class="sxs-lookup"><span data-stu-id="26915-121">It is possible toocreate a GROUP BY WITH CUBE using hello UNION ALL approach.</span></span> <span data-ttu-id="26915-122">problema de saudação é código Olá rapidamente pode se tornar complicada e complicada.</span><span class="sxs-lookup"><span data-stu-id="26915-122">hello problem is that hello code can quickly become cumbersome and unwieldy.</span></span> <span data-ttu-id="26915-123">toomitigate isso você pode usar isso mais avançados abordagem.</span><span class="sxs-lookup"><span data-stu-id="26915-123">toomitigate this you can use this more advanced approach.</span></span>

<span data-ttu-id="26915-124">Vamos usar o exemplo hello acima.</span><span class="sxs-lookup"><span data-stu-id="26915-124">Let's use hello example above.</span></span>

<span data-ttu-id="26915-125">Olá primeira etapa é toodefine Olá 'cube' que define todos os níveis de saudação de agregação que desejamos toocreate.</span><span class="sxs-lookup"><span data-stu-id="26915-125">hello first step is toodefine hello 'cube' that defines all hello levels of aggregation that we want toocreate.</span></span> <span data-ttu-id="26915-126">É importante tootake anote Olá CROSS JOIN das duas tabelas derivadas de saudação.</span><span class="sxs-lookup"><span data-stu-id="26915-126">It is important tootake note of hello CROSS JOIN of hello two derived tables.</span></span> <span data-ttu-id="26915-127">Isso gera todos os níveis de saudação para nós.</span><span class="sxs-lookup"><span data-stu-id="26915-127">This generates all hello levels for us.</span></span> <span data-ttu-id="26915-128">restante de saudação do código de saudação é realmente existe para a formatação.</span><span class="sxs-lookup"><span data-stu-id="26915-128">hello rest of hello code is really there for formatting.</span></span>

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

<span data-ttu-id="26915-129">resultados de saudação do hello CTAS podem ser vistos abaixo:</span><span class="sxs-lookup"><span data-stu-id="26915-129">hello results of hello CTAS can be seen below:</span></span>

![][1]

<span data-ttu-id="26915-130">Olá segunda etapa é toospecify que resulta de uma provisória de toostore de tabela de destino:</span><span class="sxs-lookup"><span data-stu-id="26915-130">hello second step is toospecify a target table toostore interim results:</span></span>

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

<span data-ttu-id="26915-131">Olá terceira etapa é tooloop em nosso cubo de colunas executar Olá agregação.</span><span class="sxs-lookup"><span data-stu-id="26915-131">hello third step is tooloop over our cube of columns performing hello aggregation.</span></span> <span data-ttu-id="26915-132">consulta Olá será executado uma vez para cada linha na tabela temporária Olá #Cube e armazenar os resultados de saudação na tabela temporária Olá #Results</span><span class="sxs-lookup"><span data-stu-id="26915-132">hello query will run once for every row in hello #Cube temporary table and store hello results in hello #Results temp table</span></span>

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

<span data-ttu-id="26915-133">Por fim, pode retornar resultados de hello, simplesmente lendo da tabela temporária Olá #Results</span><span class="sxs-lookup"><span data-stu-id="26915-133">Lastly we can return hello results by simply reading from hello #Results temporary table</span></span>

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

<span data-ttu-id="26915-134">Dividindo o código de saudação em seções e gerando uma saudação de construção de loop código se torna mais gerenciáveis e sustentável.</span><span class="sxs-lookup"><span data-stu-id="26915-134">By breaking hello code up into sections and generating a looping construct hello code becomes more manageable and maintainable.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26915-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="26915-135">Next steps</span></span>
<span data-ttu-id="26915-136">Para obter mais dicas de desenvolvimento, confira [visão geral de desenvolvimento][development overview].</span><span class="sxs-lookup"><span data-stu-id="26915-136">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->
