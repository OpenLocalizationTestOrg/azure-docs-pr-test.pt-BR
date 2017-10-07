---
title: "transações de aaaOptimizing para o SQL Data Warehouse | Microsoft Docs"
description: "Diretrizes de práticas recomendadas sobre como gravar atualizações de transação eficientes no SQL Data Warehouse do Azure"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 6f326f26-8a54-49df-a482-9c96a58db371
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 1a821161711db9460b7e10d3cf7ba498d711448b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-transactions-for-sql-data-warehouse"></a>Otimização de transações para o SQL Data Warehouse
Este artigo explica como toooptimize Olá desempenho do seu código transacional, minimizando o risco de reversões longo.

## <a name="transactions-and-logging"></a>Transações e registro em log
As transações são um componente importante de um mecanismo de banco de dados relacional. O SQL Data Warehouse usa transações durante a modificação de dados. Essas transações podem ser implícitas ou explícitas. As instruções individuais `INSERT`, `UPDATE` e `DELETE` são exemplos de transações implícitas. Transações explícitas são gravadas explicitamente por um desenvolvedor usando `BEGIN TRAN`, `COMMIT TRAN` ou `ROLLBACK TRAN` e normalmente são usados quando precisam de várias instruções de modificação toobe vinculado em uma única unidade atômica. 

Banco de dados de toohello de alterações usando os logs de transação é confirmada do Azure SQL Data Warehouse. Cada distribuição tem seu próprio log de transações. As gravações de log de transações são automáticas. Não é necessária nenhuma configuração. No entanto, durante esse processo garante a gravação da saudação introduz uma sobrecarga no sistema de saudação. Você pode minimizar esse impacto ao escrever um código transacionalmente eficiente. De modo geral, um código transacionalmente eficiente se enquadra em duas categorias.

* Aproveitar constructos mínimos de registro em log quando possível
* Processar dados usando a forma singular de tooavoid no escopo de lotes de transações de longa execução
* Adotar uma padrão para modificações grande tooa determinada partição de comutação de partição

## <a name="minimal-vs-full-logging"></a>Registro mínimo em log vs. registro total em log
Ao contrário das operações registradas completas, que usam Olá transaction log tookeep controlar cada linha alterada, operações minimamente registradas controlar de alocações de extensão e somente as alterações de metadados. Portanto, o log mínimo envolve o registro somente as informações de saudação que é necessário toorollback a transação de saudação no evento de saudação de uma falha ou uma solicitação explícita (`ROLLBACK TRAN`). Como muito menos informações são rastreadas no log de transações hello, uma operação minimamente registrada melhor do que uma operação totalmente registrada em log de tamanho similar. Além disso, como menos gravações passam o log de transações hello, uma quantidade menor de dados de log é gerada e portanto é e/s mais eficiente.

limites de segurança de transação Olá só se aplicam a operações toofully conectado.

> [!NOTE]
> As operações minimamente registradas em log podem participar de transações explícitas. Como todas as alterações nas estruturas de alocação são rastreadas, é possível tooroll back minimamente operações registradas. É importante toounderstand alteração hello "mínimo" está conectado a ele não está conectado não.
> 
> 

## <a name="minimally-logged-operations"></a>Operações minimamente registradas em log
Olá operações a seguir têm a capacidade de ser registradas minimamente:

* CREATE TABLE AS SELECT ([CTAS][CTAS])
* INSERT..SELECT
* CREATE INDEX
* ALTER INDEX REBUILD
* DROP INDEX
* TRUNCATE TABLE
* DROP TABLE
* ALTER TABLE SWITCH PARTITION

<!--
- MERGE
- UPDATE on LOB Types .WRITE
- SELECT..INTO
-->

> [!NOTE]
> As operações de movimentação de dados internos (como `BROADCAST` e `SHUFFLE`) não são afetados pelo limite de segurança de transação hello.
> 
> 

## <a name="minimal-logging-with-bulk-load"></a>Registro mínimo em log com carregamento em massa
`CTAS` e `INSERT...SELECT` são ambos operações de carregamento em massa. No entanto, ambos são influenciadas pela definição de tabela de destino hello e dependem do cenário de carga hello. A seguir, uma tabela que explica se a operação em massa será total ou minimamente registrada em log:  

| Índice principal | Cenário de carga | Modo de registro em log |
| --- | --- | --- |
| Heap |Qualquer |**Mínimo** |
| Índice clusterizado |Tabela de destino vazia |**Mínimo** |
| Índice clusterizado |As linhas carregadas não se sobrepõem às páginas existentes no destino |**Mínimo** |
| Índice clusterizado |Linhas carregadas se sobrepõem com páginas existentes no destino |Completo |
| Índice columnstore clusterizado |Tamanho do lote >= 102.400 por distribuição alinhada por partição |**Mínimo** |
| Índice columnstore clusterizado |Tamanho do lote < 102.400 por distribuição alinhada por partição |Completo |

Vale a pena observar que os índices secundários ou não clusterizado tooupdate sempre será totalmente gravações operações registradas.

> [!IMPORTANT]
> O SQL Data Warehouse possui 60 distribuições. Por isso, supondo que todas as linhas são distribuídas uniformemente e inicial em uma única partição, o lote será necessário toocontain 6,144,000 linhas ou toobe maior minimamente registradas durante a gravação tooa índice Columnstore clusterizado. Se Olá tabela está particionada e linhas de saudação inseridas span limites de partição, você precisará 6,144,000 linhas por limite de partição, supondo que até mesmo a distribuição de dados. Cada partição em cada distribuição independentemente deve exceder o limite de linha 102.400 Olá para Olá insert toobe minimamente em distribuição de saudação.
> 
> 

Carregar dados em uma tabela não vazia com um índice clusterizado pode, muitas vezes, conter uma combinação de linhas total e minimamente registradas em log. Um índice clusterizado é uma árvore balanceada (árvore b) das páginas. Se a página de hello está sendo gravada tooalready contém linhas de outra transação, em seguida, essas gravações serão totalmente registradas. No entanto, se a página de saudação está vazia, em seguida, página de toothat de gravação de saudação será minimamente registrada.

## <a name="optimizing-deletes"></a>Otimizando exclusões
`DELETE` é uma operação totalmente registrada em log.  Se você precisar toodelete uma grande quantidade de dados em uma tabela ou uma partição, geralmente faz mais sentido muito`SELECT` dados saudação desejar tookeep, que pode ser executado como uma operação minimamente registrada.  tooaccomplish isso, crie uma nova tabela com [CTAS][CTAS].  Depois de criar, usar [RENOMEAR] [ RENAME] tooswap sua tabela antiga com tabela Olá recém-criado.

```sql
-- Delete all sales transactions for Promotions except PromotionKey 2.

--Step 01. Create a new table select only hello records we want tookep (PromotionKey 2)
CREATE TABLE [dbo].[FactInternetSales_d]
WITH
(    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([ProductKey])
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20000101, 20010101, 20020101, 20030101, 20040101, 20050101
                                                ,    20060101, 20070101, 20080101, 20090101, 20100101, 20110101
                                                ,    20120101, 20130101, 20140101, 20150101, 20160101, 20170101
                                                ,    20180101, 20190101, 20200101, 20210101, 20220101, 20230101
                                                ,    20240101, 20250101, 20260101, 20270101, 20280101, 20290101
                                                )
)
AS
SELECT     *
FROM     [dbo].[FactInternetSales]
WHERE    [PromotionKey] = 2
OPTION (LABEL = 'CTAS : Delete')
;

--Step 02. Rename hello Tables tooreplace hello 
RENAME OBJECT [dbo].[FactInternetSales]   too[FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_d] too[FactInternetSales];
```

## <a name="optimizing-updates"></a>Otimizando atualizações
`UPDATE` é uma operação totalmente registrada em log.  Se você precisar tooupdate um grande número de linhas em uma tabela ou uma partição geralmente pode ser muito mais eficiente toouse uma operação minimamente registrada como [CTAS] [ CTAS] toodo para.

No hello exemplo abaixo de uma atualização de tabela completa foi convertido tooa `CTAS` para que o log mínimo é possível.

Nesse caso retrospectively estamos adicionando um desconto quantidade toohello de vendas na tabela de saudação:

```sql
--Step 01. Create a new table containing hello "Update". 
CREATE TABLE [dbo].[FactInternetSales_u]
WITH
(    CLUSTERED INDEX
,    DISTRIBUTION = HASH([ProductKey])
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20000101, 20010101, 20020101, 20030101, 20040101, 20050101
                                                ,    20060101, 20070101, 20080101, 20090101, 20100101, 20110101
                                                ,    20120101, 20130101, 20140101, 20150101, 20160101, 20170101
                                                ,    20180101, 20190101, 20200101, 20210101, 20220101, 20230101
                                                ,    20240101, 20250101, 20260101, 20270101, 20280101, 20290101
                                                )
                )
)
AS 
SELECT
    [ProductKey]  
,    [OrderDateKey] 
,    [DueDateKey]  
,    [ShipDateKey] 
,    [CustomerKey] 
,    [PromotionKey] 
,    [CurrencyKey] 
,    [SalesTerritoryKey]
,    [SalesOrderNumber]
,    [SalesOrderLineNumber]
,    [RevisionNumber]
,    [OrderQuantity]
,    [UnitPrice]
,    [ExtendedAmount]
,    [UnitPriceDiscountPct]
,    ISNULL(CAST(5 as float),0) AS [DiscountAmount]
,    [ProductStandardCost]
,    [TotalProductCost]
,    ISNULL(CAST(CASE WHEN [SalesAmount] <=5 THEN 0
         ELSE [SalesAmount] - 5
         END AS MONEY),0) AS [SalesAmount]
,    [TaxAmt]
,    [Freight]
,    [CarrierTrackingNumber] 
,    [CustomerPONumber]
FROM    [dbo].[FactInternetSales]
OPTION (LABEL = 'CTAS : Update')
;

--Step 02. Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales]   too[FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_u] too[FactInternetSales];

--Step 03. Drop hello old table
DROP TABLE [dbo].[FactInternetSales_old]
```

> [!NOTE]
> A recriação de tabelas grandes pode se beneficiar do uso de recursos de gerenciamento de carga de trabalho do SQL Data Warehouse. Para mais detalhes, consulte a seção de gerenciamento de carga de trabalho toohello em Olá [simultaneidade] [ concurrency] artigo.
> 
> 

## <a name="optimizing-with-partition-switching"></a>Otimizando com alternância de partição
Quando houver modificações em larga escala dentro de uma [partição da tabela][table partition], fará mais sentido considerar um padrão de troca de partições. Se hello modificação de dados é significativa e abrange várias partições, simplesmente iteração sobre partições Olá alcança Olá mesmo resultado.

Olá etapas tooperform uma alternância de partição são da seguinte maneira:

1. Criar uma partição de saída vazia
2. Executar 'update' hello como um CTAS
3. Olá toohello existente de dados tabela de extração
4. Inserir novos dados de saudação
5. Limpar dados saudação

No entanto, toohelp identificar Olá partições tooswitch primeiro precisaremos toobuild um procedimento auxiliar como Olá um abaixo. 

```sql
CREATE PROCEDURE dbo.partition_data_get
    @schema_name           NVARCHAR(128)
,    @table_name               NVARCHAR(128)
,    @boundary_value           INT
AS
IF OBJECT_ID('tempdb..#ptn_data') IS NOT NULL
BEGIN
    DROP TABLE #ptn_data
END
CREATE TABLE #ptn_data
WITH    (    DISTRIBUTION = ROUND_ROBIN
        ,    HEAP
        )
AS
WITH CTE
AS
(
SELECT     s.name                            AS [schema_name]
,        t.name                            AS [table_name]
,         p.partition_number                AS [ptn_nmbr]
,        p.[rows]                        AS [ptn_rows]
,        CAST(r.[value] AS INT)            AS [boundary_value]
FROM        sys.schemas                    AS s
JOIN        sys.tables                    AS t    ON  s.[schema_id]        = t.[schema_id]
JOIN        sys.indexes                    AS i    ON     t.[object_id]        = i.[object_id]
JOIN        sys.partitions                AS p    ON     i.[object_id]        = p.[object_id] 
                                                AND i.[index_id]        = p.[index_id] 
JOIN        sys.partition_schemes        AS h    ON     i.[data_space_id]    = h.[data_space_id]
JOIN        sys.partition_functions        AS f    ON     h.[function_id]        = f.[function_id]
LEFT JOIN    sys.partition_range_values    AS r     ON     f.[function_id]        = r.[function_id] 
                                                AND r.[boundary_id]        = p.[partition_number]
WHERE i.[index_id] <= 1
)
SELECT    *
FROM    CTE
WHERE    [schema_name]        = @schema_name
AND        [table_name]        = @table_name
AND        [boundary_value]    = @boundary_value
OPTION (LABEL = 'dbo.partition_data_get : CTAS : #ptn_data')
;
GO
```

Esse procedimento maximiza a reutilização de código e mantém o exemplo mais compacto de comutação de partição hello.

Olá código a seguir demonstra as cinco etapas de saudação mencionados acima tooachieve uma rotina de comutação de partição completa.

```sql
--Create a partitioned aligned empty table tooswitch out hello data 
IF OBJECT_ID('[dbo].[FactInternetSales_out]') IS NOT NULL
BEGIN
    DROP TABLE [dbo].[FactInternetSales_out]
END

CREATE TABLE [dbo].[FactInternetSales_out]
WITH
(    DISTRIBUTION = HASH([ProductKey])
,    CLUSTERED COLUMNSTORE INDEX
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20020101, 20030101
                                                )
                )
)
AS
SELECT *
FROM    [dbo].[FactInternetSales]
WHERE 1=2
OPTION (LABEL = 'CTAS : Partition Switch IN : UPDATE')
;

--Create a partitioned aligned table and update hello data in hello select portion of hello CTAS
IF OBJECT_ID('[dbo].[FactInternetSales_in]') IS NOT NULL
BEGIN
    DROP TABLE [dbo].[FactInternetSales_in]
END

CREATE TABLE [dbo].[FactInternetSales_in]
WITH
(    DISTRIBUTION = HASH([ProductKey])
,    CLUSTERED COLUMNSTORE INDEX
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20020101, 20030101
                                                )
                )
)
AS 
SELECT
    [ProductKey]  
,    [OrderDateKey] 
,    [DueDateKey]  
,    [ShipDateKey] 
,    [CustomerKey] 
,    [PromotionKey] 
,    [CurrencyKey] 
,    [SalesTerritoryKey]
,    [SalesOrderNumber]
,    [SalesOrderLineNumber]
,    [RevisionNumber]
,    [OrderQuantity]
,    [UnitPrice]
,    [ExtendedAmount]
,    [UnitPriceDiscountPct]
,    ISNULL(CAST(5 as float),0) AS [DiscountAmount]
,    [ProductStandardCost]
,    [TotalProductCost]
,    ISNULL(CAST(CASE WHEN [SalesAmount] <=5 THEN 0
         ELSE [SalesAmount] - 5
         END AS MONEY),0) AS [SalesAmount]
,    [TaxAmt]
,    [Freight]
,    [CarrierTrackingNumber] 
,    [CustomerPONumber]
FROM    [dbo].[FactInternetSales]
WHERE    OrderDateKey BETWEEN 20020101 AND 20021231
OPTION (LABEL = 'CTAS : Partition Switch IN : UPDATE')
;

--Use hello helper procedure tooidentify hello partitions
--hello source table
EXEC dbo.partition_data_get 'dbo','FactInternetSales',20030101
DECLARE @ptn_nmbr_src INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_src

--hello "in" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_in',20030101
DECLARE @ptn_nmbr_in INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_in

--hello "out" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_out',20030101
DECLARE @ptn_nmbr_out INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_out

--Switch hello partitions over
DECLARE @SQL NVARCHAR(4000) = '
ALTER TABLE [dbo].[FactInternetSales]    SWITCH PARTITION '+CAST(@ptn_nmbr_src AS VARCHAR(20))    +' too[dbo].[FactInternetSales_out] PARTITION '    +CAST(@ptn_nmbr_out AS VARCHAR(20))+';
ALTER TABLE [dbo].[FactInternetSales_in] SWITCH PARTITION '+CAST(@ptn_nmbr_in AS VARCHAR(20))    +' too[dbo].[FactInternetSales] PARTITION '        +CAST(@ptn_nmbr_src AS VARCHAR(20))+';'
EXEC sp_executesql @SQL

--Perform hello clean-up
TRUNCATE TABLE dbo.FactInternetSales_out;
TRUNCATE TABLE dbo.FactInternetSales_in;

DROP TABLE dbo.FactInternetSales_out
DROP TABLE dbo.FactInternetSales_in
DROP TABLE #ptn_data
```

## <a name="minimize-logging-with-small-batches"></a>Minimizar o registro em log com pequenos lotes
Para operações de modificação de dados grandes, poderá executar operação de saudação de toodivide sentido em partes ou lotes tooscope Olá a unidade de trabalho.

Um exemplo funcional é fornecido abaixo. tamanho do lote Olá definiu trivial técnica número Olá de toohighlight tooa. Na realidade, tamanho de lote de saudação seria significativamente maior. 

```sql
SET NO_COUNT ON;
IF OBJECT_ID('tempdb..#t') IS NOT NULL
BEGIN
    DROP TABLE #t;
    PRINT '#t dropped';
END

CREATE TABLE #t
WITH    (    DISTRIBUTION = ROUND_ROBIN
        ,    HEAP
        )
AS
SELECT    ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS seq_nmbr
,        SalesOrderNumber
,        SalesOrderLineNumber
FROM    dbo.FactInternetSales
WHERE    [OrderDateKey] BETWEEN 20010101 and 20011231
;

DECLARE    @seq_start        INT = 1
,        @batch_iterator    INT = 1
,        @batch_size        INT = 50
,        @max_seq_nmbr    INT = (SELECT MAX(seq_nmbr) FROM dbo.#t)
;

DECLARE    @batch_count    INT = (SELECT CEILING((@max_seq_nmbr*1.0)/@batch_size))
,        @seq_end        INT = @batch_size
;

SELECT COUNT(*)
FROM    dbo.FactInternetSales f

PRINT 'MAX_seq_nmbr '+CAST(@max_seq_nmbr AS VARCHAR(20))
PRINT 'MAX_Batch_count '+CAST(@batch_count AS VARCHAR(20))

WHILE    @batch_iterator <= @batch_count
BEGIN
    DELETE
    FROM    dbo.FactInternetSales
    WHERE EXISTS
    (
            SELECT    1
            FROM    #t t
            WHERE    seq_nmbr BETWEEN  @seq_start AND @seq_end
            AND        FactInternetSales.SalesOrderNumber        = t.SalesOrderNumber
            AND        FactInternetSales.SalesOrderLineNumber    = t.SalesOrderLineNumber
    )
    ;

    SET @seq_start = @seq_end
    SET @seq_end = (@seq_start+@batch_size);
    SET @batch_iterator +=1;
END
```

## <a name="pause-and-scaling-guidance"></a>Diretrizes de pausa e dimensionamento
O SQL Data Warehouse do Azure permite pausar, retomar e dimensionar seu data warehouse sob demanda. Quando você pausa ou dimensionar seu SQL Data Warehouse é toounderstand importante que todas as transações em andamento serão encerradas imediatamente; fazendo com que quaisquer transações abertas toobe revertida. Se sua carga de trabalho tinha emitido uma longa duração e a modificação de dados incompletos anterior toohello pausar ou operação de expansão, esse trabalho será necessário toobe desfeita. Isso pode afetar Olá tempo toopause ou dimensionar seu banco de dados do Azure SQL Data Warehouse. 

> [!IMPORTANT]
> As operações `UPDATE` e `DELETE` são totalmente registradas em log e, portanto, essas operações de desfazer/refazer podem demorar significativamente mais do que as operações equivalentes minimamente registradas em log. 
> 
> 

cenário de melhor Olá é toolet em voo dados modificação transações completa anterior toopausing ou escala SQL Data Warehouse. No entanto, isso pode não sempre ser prático. risco de saudação toomitigate de reversão longo, considere uma das Olá as opções a seguir:

* Gravar novamente as operações de longa duração usando [CTAS][CTAS]
* Operação de saudação são divididos nas partes; operando em um subconjunto de linhas de saudação

## <a name="next-steps"></a>Próximas etapas
Consulte [transações no SQL Data Warehouse] [ Transactions in SQL Data Warehouse] toolearn mais sobre níveis de isolamento e limites transacionais.  Para obter uma visão geral de outras práticas recomendadas, confira [Práticas recomendadas para o Azure SQL Data Warehouse][SQL Data Warehouse Best Practices].

<!--Image references-->

<!--Article references-->
[Transactions in SQL Data Warehouse]: ./sql-data-warehouse-develop-transactions.md
[table partition]: ./sql-data-warehouse-tables-partition.md
[Concurrency]: ./sql-data-warehouse-develop-concurrency.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->
[alter index]:https://msdn.microsoft.com/library/ms188388.aspx
[RENAME]: https://msdn.microsoft.com/library/mt631611.aspx

<!-- Other web references -->

