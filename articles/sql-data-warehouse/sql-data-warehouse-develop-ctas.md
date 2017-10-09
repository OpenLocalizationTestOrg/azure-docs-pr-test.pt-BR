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
# <a name="create-table-as-select-ctas-in-sql-data-warehouse"></a>Instrução Create Table As Select (CTAS) no SQL Data Warehouse
Criar tabela como select ou `CTAS` é uma saudação mais importantes recursos de T-SQL disponíveis. É uma operação totalmente em paralelo que cria uma nova tabela com base na saída de saudação de uma instrução SELECT. `CTAS`é uma cópia de uma tabela de toocreate de maneira mais rápida e simples de saudação. Este documento fornece exemplos e melhores práticas para o `CTAS`.

## <a name="selectinto-vs-ctas"></a>SELECT..INTO versus CTAS
Você pode considerar `CTAS` como uma versão turbinada de `SELECT..INTO`.

Veja a seguir um exemplo de uma instrução `SELECT..INTO` simples:

```sql
SELECT *
INTO    [dbo].[FactInternetSales_new]
FROM    [dbo].[FactInternetSales]
```

No exemplo hello acima `[dbo].[FactInternetSales_new]` seria criado como tabela de ROUND_ROBIN distribuída com um índice de COLUMNSTORE CLUSTERIZADO nela conforme estes são os padrões de tabela Olá no Azure SQL Data Warehouse.

`SELECT..INTO`No entanto não permitem que você toochange qualquer índice Olá distribuição hello ou método de tipo como parte da operação de saudação. É aí que `CTAS` entra em cena.

Olá tooconvert acima muito`CTAS` é bastante direta:

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

Com `CTAS` são toochange capaz de ambos Olá a distribuição de dados da tabela hello, bem como o tipo de tabela hello. 

> [!NOTE]
> Se você estiver apenas tentando índice Olá toochange seu `CTAS` operação e hello tabela de origem é hash distribuída seu `CTAS` irá realizar a operação melhor se você mantiver Olá mesmo tipo de coluna e os dados de distribuição. Isso evitará cruzada movimentação de dados de distribuição durante a operação de saudação que é mais eficiente.
> 
> 

## <a name="using-ctas-toocopy-a-table"></a>Usando CTAS toocopy uma tabela
Talvez um dos mais comuns de saudação usos de `CTAS` está criando uma cópia de uma tabela para que você possa alterar Olá DDL. Se por exemplo você criou a tabela como `ROUND_ROBIN` e agora deseja alterá-la tooa tabela distribuído em uma coluna, `CTAS` é como coluna de distribuição Olá deve ser alterada. `CTAS`também é possível toochange usado tipos de particionamento, indexação ou coluna.

Digamos que você criou esta tabela usando o tipo de distribuição de padrão de saudação do `ROUND_ROBIN` distribuída porque nenhuma coluna de distribuição foi especificada no hello `CREATE TABLE`.

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

Agora você deseja toocreate uma nova cópia da tabela com um índice Columnstore clusterizado, para que você pode tirar proveito do desempenho de saudação do tabelas Columnstore clusterizado. Você também deseja toodistribute essa tabela na ProductKey desde que você está prevendo junções nessa coluna e deseja tooavoid a movimentação de dados durante a junções em ProductKey. Por fim deseja tooadd particionamento em OrderDateKey para que você pode excluir dados antigos, soltando partições antigas. Aqui está a instrução CTAS Olá copie a tabela antiga para uma nova tabela.

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

Finalmente você pode renomear seu tooswap tabelas em sua nova tabela e, em seguida, remova a tabela antiga.

```sql
RENAME OBJECT FactInternetSales tooFactInternetSales_old;
RENAME OBJECT FactInternetSales_new tooFactInternetSales;

DROP TABLE FactInternetSales_old;
```

> [!NOTE]
> O SQL Data Warehouse do Azure ainda não dá suporte a estatísticas de criação ou atualização automática.  Em ordem tooget Olá melhor desempenho de suas consultas, é importante que ser criadas estatísticas em todas as colunas de todas as tabelas após a primeira carga de saudação ou alterações substanciais ocorrerem nos dados de saudação.  Para obter uma explicação detalhada de estatísticas, consulte Olá [estatísticas] [ Statistics] tópico no grupo de desenvolver Olá de tópicos.
> 
> 

## <a name="using-ctas-toowork-around-unsupported-features"></a>Usando toowork CTAS em torno de recursos sem suporte
`CTAS`também pode ser usado toowork em torno de uma série de recursos de saudação sem suporte listados abaixo. Isso pode geralmente se Mostrar toobe win/ganham não só será compatível com seu código, mas serão geralmente executadas mais rapidamente no SQL Data Warehouse. Isso é devido ao seu design totalmente em paralelo. Os cenários que podem ser solucionados com CTAS incluem:

* ANSI JOINS em instruções UPDATE
* ANSI JOINs em instruções DELETE
* Instrução MERGE

> [!NOTE]
> Tente toothink "CTAS primeiro". Se você achar que é possível resolver um problema usando `CTAS` que geralmente é Olá melhor maneira tooapproach-- mesmo se você está gravando os dados mais como resultado.
> 
> 

## <a name="ansi-join-replacement-for-update-statements"></a>Substituição da junção ANSI para atualizar instruções
Você pode achar que uma atualização complexa que une mais de duas tabelas usando ANSI unindo Olá de tooperform sintaxe UPDATE ou DELETE.

Imagine que você tinha tooupdate nesta tabela:

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

consulta original Olá pode se parecer com isso:

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

Desde que não oferece suporte a SQL Data Warehouse ANSI junções na Olá `FROM` cláusula de um `UPDATE` instrução, você não pode copiar este código sobre sem alterá-lo um pouco.

Você pode usar uma combinação de um `CTAS` e implícita ingressar tooreplace este código:

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

## <a name="ansi-join-replacement-for-delete-statements"></a>Substituição de junção ANSI para instruções delete
Às vezes, a melhor abordagem Olá para exclusão de dados é toouse `CTAS`. Em vez de excluir dados Olá simplesmente selecione Olá dados tookeep. Este especialmente verdadeiro para `DELETE` instruções que usam ansi unindo sintaxe desde que o SQL Data Warehouse não oferece suporte a junções de ANSI em Olá `FROM` cláusula de um `DELETE` instrução.

Um exemplo de uma instrução DELETE convertida está disponível abaixo:

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

## <a name="replace-merge-statements"></a>Substituir instruções merge
Instruções de mesclagem podem ser substituídas, pelo menos em parte, usando `CTAS`. Você pode consolidar Olá `INSERT` e hello `UPDATE` em uma única instrução. Quaisquer registros excluídos precisaria toobe fechada em uma segunda instrução.

Um exemplo de uma instrução `UPSERT` está disponível abaixo:

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

## <a name="ctas-recommendation-explicitly-state-data-type-and-nullability-of-output"></a>Recomendação de CTAS: declarar explicitamente o tipo de dados e a nulidade da saída
Ao migrar o código, você pode achar executar por esse tipo de padrão de codificação:

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

Instintivamente, você pode pensar tooa esse código CTAS devem ser migrados e você está correto. No entanto, há um problema oculto aqui.

Olá código a seguir não geram Olá mesmo resultado:

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

Observe o resultado"hello coluna" carrega com os valores hello tipo e a nulidade de dados da expressão de saudação. Isso pode levar toosubtle variações nos valores se você não tiver cuidado.

Tente o seguinte hello como um exemplo:

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

Olá valor armazenado para o resultado é diferente. Como hello persistente valor na coluna de resultado de saudação é usado em outras expressões Olá erro torna-se ainda mais significativo.

![][1]

Isso é particularmente importante para migrações de dados. Mesmo que a segunda consulta de saudação é indiscutivelmente mais precisa, há um problema. dados de saudação seriam diferentes toohello em comparação com o sistema de origem e que leva tooquestions de integridade na migração de saudação. Esta é uma das raros casos em que a resposta "incorreto" hello é realmente saudação à direita um!

Olá motivo, podemos ver essa discrepância entre resultados Olá dois está inoperante tooimplicit conversão de tipo. No Olá a primeira tabela do exemplo hello define definição de coluna Olá. Quando a linha hello é inserida ocorre uma conversão implícita de tipo. No segundo exemplo de saudação não há nenhuma conversão implícita de tipo como expressão Olá define o tipo de dados da coluna de saudação. Observe que também que a coluna Olá no segundo exemplo de saudação foi definida como uma coluna anulável enquanto o primeiro exemplo de saudação não tem. Quando Olá tabela foi criada no primeiro nulidade da coluna exemplo hello foi definida explicitamente. No segundo exemplo de hello apenas estava toohello expressão e, por padrão, isso pode resultar em uma definição de NULL.  

tooresolve esses problemas que você deve definir explicitamente a conversão de tipo hello e nulidade em Olá `SELECT` parte da saudação `CTAS` instrução. Não é possível definir essas propriedades no hello criam parte da tabela.

exemplo Hello abaixo demonstra como toofix Olá código:

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

Observe o seguinte hello:

* CAST ou CONVERT poderia ter sido usado
* ISNULL é usada tooforce nulidade ADESÃO não
* ISNULL é função mais externa Olá
* Olá segunda parte da saudação ISNULL é uma constante ou seja, 0

> [!NOTE]
> Olá nulidade toobe definida corretamente é vital toouse `ISNULL` e não `COALESCE`. `COALESCE`não é uma função determinística e então Olá resultado da saudação expressão será sempre NULLable. `ISNULL` é diferente. É determinístico. Quando Olá, portanto, a segunda parte da saudação `ISNULL` função é uma constante ou um literal, o valor resultante hello serão não nulo.
> 
> 

Esta dica não é útil apenas para assegurar a integridade de saudação de seus cálculos. Também é importante para a alternância de partição de tabela. Imagine que você tenha essa tabela definida como o caso:

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

No entanto, o campo de valor de saudação é uma expressão calculada não faz parte dos dados de origem de saudação.

toocreate seu conjunto de dados particionado, talvez você queira toodo isso:

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

consulta de saudação será executado perfeitamente normal. problema de saudação é fornecido quando você tenta a alternância de partição tooperform Olá. definições de tabela Olá não coincidem. definições de tabela Olá toomake encontrar hello que CTAS precisa toobe modificado.

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

Você pode ver, portanto, que a consistência de tipo e manutenção das propriedades de nulidade em um CTAS é uma boa prática recomendada de desenvolvimento. Ele ajuda a integridade de toomaintain em seus cálculos e também garante que a alternância de partição é possível.

Consulte para obter mais informações sobre como usar tooMSDN [CTAS][CTAS]. É uma das instruções de hello mais importantes no Azure SQL Data Warehouse. Certifique-se compreendê-la totalmente.

## <a name="next-steps"></a>Próximas etapas
Para obter mais dicas de desenvolvimento, confira [visão geral de desenvolvimento][development overview].

<!--Image references-->
[1]: media/sql-data-warehouse-develop-ctas/ctas-results.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[CTAS]: https://msdn.microsoft.com/library/mt204041.aspx

<!--Other Web references-->
