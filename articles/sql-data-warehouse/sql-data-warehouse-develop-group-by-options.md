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
# <a name="group-by-options-in-sql-data-warehouse"></a>Agrupar por opções de SQL Data Warehouse
Olá [GROUP BY] [ GROUP BY] cláusula é utilizada tooaggregate tooa resumo conjunto de dados linhas. Ele também tem algumas opções que estendem sua funcionalidade que toobe necessidade contornado como não são diretamente suportados pelo Azure SQL Data Warehouse.

Essas opções são

* GROUP BY com ROLLUP
* GROUPING SETS
* GROUP BY com CUBE

## <a name="rollup-and-grouping-sets-options"></a>O rollup e o agrupamento definem opções
Olá, aqui a opção mais simples é toouse `UNION ALL` em vez disso, tooperform Olá rollup em vez de depender Olá sintaxe explícito. é o resultado de saudação exatamente Olá mesmo

Abaixo está um exemplo de um grupo pela instrução usando Olá `ROLLUP` opção:

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

Usando o pacote cumulativo de atualizações tenhamos solicitado Olá agregações a seguir:

* país e região
* País
* Grande Total

tooreplace isso será necessário toouse `UNION ALL`; especificando agregações Olá necessárias explicitamente tooreturn Olá os mesmos resultados:

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

Para conjuntos de AGRUPAMENTOS tudo o que precisamos toodo é adotar Olá mesmo principal, mas apenas criar seções UNION ALL para Olá níveis de agregação que desejamos toosee

## <a name="cube-options"></a>Opções Cube
É possível toocreate um GROUP BY WITH CUBE usando a abordagem de saudação UNION ALL. problema de saudação é código Olá rapidamente pode se tornar complicada e complicada. toomitigate isso você pode usar isso mais avançados abordagem.

Vamos usar o exemplo hello acima.

Olá primeira etapa é toodefine Olá 'cube' que define todos os níveis de saudação de agregação que desejamos toocreate. É importante tootake anote Olá CROSS JOIN das duas tabelas derivadas de saudação. Isso gera todos os níveis de saudação para nós. restante de saudação do código de saudação é realmente existe para a formatação.

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

resultados de saudação do hello CTAS podem ser vistos abaixo:

![][1]

Olá segunda etapa é toospecify que resulta de uma provisória de toostore de tabela de destino:

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

Olá terceira etapa é tooloop em nosso cubo de colunas executar Olá agregação. consulta Olá será executado uma vez para cada linha na tabela temporária Olá #Cube e armazenar os resultados de saudação na tabela temporária Olá #Results

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

Por fim, pode retornar resultados de hello, simplesmente lendo da tabela temporária Olá #Results

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

Dividindo o código de saudação em seções e gerando uma saudação de construção de loop código se torna mais gerenciáveis e sustentável.

## <a name="next-steps"></a>Próximas etapas
Para obter mais dicas de desenvolvimento, confira [visão geral de desenvolvimento][development overview].

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->
