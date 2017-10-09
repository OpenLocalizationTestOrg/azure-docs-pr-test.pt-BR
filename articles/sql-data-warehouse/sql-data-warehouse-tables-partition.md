---
title: tabelas de aaaPartitioning no SQL Data Warehouse | Microsoft Docs
description: "Introdução ao particionamento de tabela no Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 6cef870c-114f-470c-af10-02300c58885d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: aa63c51562f3e6f83063320860b195e135a721e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="partitioning-tables-in-sql-data-warehouse"></a>Particionando tabelas no SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Visão geral][Overview]
> * [Tipos de Dados][Data Types]
> * [Distribuir][Distribute]
> * [Índice][Index]
> * [Partição][Partition]
> * [Estatísticas][Statistics]
> * [Temporário][Temporary]
> 
> 

O particionamento tem suporte em todos os tipos de tabela do SQL Data Warehouse, incluindo columnstore clusterizado, índice clusterizado e heap.  O particionamento também tem suporte em todos os tipos de distribuição, incluindo hash ou round robin.  Particionamento permite toodivide seus dados em grupos menores de dados e na maioria dos casos, o particionamento são feitos em uma coluna de data.

## <a name="benefits-of-partitioning"></a>Benefícios do particionamento
O particionamento pode melhorar o desempenho da consulta e a manutenção de dados.  Se ele se beneficia ambos ou apenas uma é dependente de como os dados são carregados e se hello mesma coluna pode ser usada para ambas as finalidades, como particionamento só pode ser feito em uma coluna.

### <a name="benefits-tooloads"></a>Benefícios tooloads
o principal benefício de saudação do particionamento no SQL Data Warehouse é melhorar a eficiência de saudação e desempenho de carregamento de dados através do uso de exclusão de partição, troca e mesclagem.  Na maioria dos casos, os dados são particionados em uma data a coluna que é ligado sequência toohello quais dados Olá são carregado toohello banco de dados.  Um dos maiores benefícios de saudação do uso de partições toomaintain dados Olá a redução do log de transações.  Ao simplesmente inserção, atualização ou exclusão de dados pode ser a abordagem mais simples de hello, com um pouco de esforço e pensamento usar particionamento durante o processo de carregamento pode melhorar substancialmente o desempenho.

Alternância de partição pode ser usado tooquickly remover ou substituir uma seção de uma tabela.  Por exemplo, uma tabela de fatos de vendas pode conter apenas os dados para Olá últimos 36 meses.  No final da saudação de cada mês, hello dados de vendas do mês mais antigo é excluído da tabela de saudação.  Esses dados podem ser excluídos usando um delete instrução toodelete Olá de dados para Olá mês mais antigo.  No entanto, a exclusão de uma grande quantidade de dados linha a linha com uma instrução delete pode levar muito tempo, bem como criar um risco de saudação de grandes transações que poderiam levar um longo tempo toorollback se algo der errado.  Uma abordagem melhor é drop toosimply partição mais antiga de saudação de dados.  Onde excluir linhas individuais Olá pode levar horas, a exclusão de uma partição inteira poderá levar segundos.

### <a name="benefits-tooqueries"></a>Benefícios tooqueries
O particionamento também pode ser usado tooimprove desempenho da consulta.  Se uma consulta aplica um filtro em uma coluna particionada, isso pode limitar Olá verificação tooonly Olá qualificação partições que podem ser um subconjunto de dados hello, evitando uma verificação completa muito menor.  Com a introdução de saudação de índices columnstore clusterizados, os benefícios de desempenho de eliminação de predicado Olá são benéficos menor, mas em alguns casos pode haver um benefício tooqueries.  Por exemplo, se a tabela de fatos de vendas de saudação é dividida em 36 meses usando o campo de data de venda hello, consultas de filtro na data de venda Olá poderá ignorar pesquisa nas partições que não correspondem ao filtro de saudação.

## <a name="partition-sizing-guidance"></a>Diretrizes de dimensionamento da partição
Durante o particionamento pode ser usado tooimprove desempenho em alguns cenários, como criar uma tabela com **muitos** partições podem prejudicar o desempenho em algumas circunstâncias.  Esses problemas são especialmente verdadeiros para tabelas columnstore clusterizadas.  Para particionamento toobe úteis, é importante toounderstand quando toouse particionamento e Olá o número de partições toocreate.  Há é nenhuma regra rígida rápida como toohow várias partições são muitos, depende de seus dados e quantas partições você está carregando toosimultaneously.  Mas como um regra geral, considere adicionar por 10 too100s de partições, não 1000s.

Ao criar o particionamento em **columnstore clusterizado** tabelas, é importante tooconsider quantas linhas serão levadas em cada partição.  Para compactação e desempenho ideais de tabelas columnstore clusterizadas, é necessário um mínimo de um milhão de linhas por distribuição, e também é necessário haver partição.  Antes das partições serem criadas, o SQL Data Warehouse já divide cada tabela em 60 bancos de dados distribuídos.  Qualquer tabela tooa adicionado particionamento Além disso é toohello distribuições criadas em segundo plano da saudação.  Usando este exemplo, se tabela de fatos de vendas Olá contidos 36 partições mensais e considerando que o SQL Data Warehouse tem 60 distribuições, então Olá fatos de vendas tabela deve conter 60 milhões de linhas por mês ou 2.1 bilhões de linhas quando todos os meses são populados.  Se uma tabela contém significativamente menos linhas que a saudação recomendada número mínimo de linhas por partição, considere usar menos partições no número do pedido toomake aumento Olá de linhas por partição.  Consulte também Olá [indexação] [ Index] artigo que inclui as consultas que podem ser executadas na qualidade do SQL Data Warehouse tooassess Olá de índices de columnstore do cluster.

## <a name="syntax-difference-from-sql-server"></a>Diferença de sintaxe do SQL Server
O SQL Data Warehouse apresenta uma definição simplificada de partições que é ligeiramente diferente do SQL Server.  As funções e esquemas de particionamento não são usados no SQL Data Warehouse como são no SQL Server.  Em vez disso, você só precisa toodo é identificar pontos de limite de coluna e hello particionados.  Sintaxe de saudação do particionamento pode ser ligeiramente diferente do SQL Server, os conceitos básicos do hello são Olá mesmo.  O SQL Server e o SQL Data Warehouse dão suporte a uma coluna de partição por tabela, que pode ser partição intervalada.  toolearn mais informações sobre particionamento, consulte [tabelas e índices particionados][Partitioned Tables and Indexes].

Olá abaixo o exemplo de um SQL Data Warehouse particionada [CREATE TABLE] [ CREATE TABLE] instrução, partições de tabela FactInternetSales Olá coluna OrderDateKey de saudação:

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
    [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

## <a name="migrating-partitioning-from-sql-server"></a>Migrando o particionamento do SQL Server
toomigrate do SQL Server de partição simplesmente tooSQL definições do Data Warehouse:

* Eliminar saudação do SQL Server [esquema de partição][partition scheme].
* Adicionar Olá [função de partição] [ partition function] tooyour definição criar tabela.

Se você estiver migrando uma tabela particionada de uma saudação de instância do SQL Server abaixo SQL pode ajudá-lo a toointerrogate número de saudação de linhas em cada partição.  Tenha em mente que, se hello mesma granularidade de particionamento é usada no SQL Data Warehouse, Olá número de linhas por partição diminuirá por um fator de 60.  

```sql
-- Partition information for a SQL Server Database
SELECT      s.[name]                        AS      [schema_name]
,           t.[name]                        AS      [table_name]
,           i.[name]                        AS      [index_name]
,           p.[partition_number]            AS      [partition_number]
,           SUM(a.[used_pages]*8.0)         AS      [partition_size_kb]
,           SUM(a.[used_pages]*8.0)/1024    AS      [partition_size_mb]
,           SUM(a.[used_pages]*8.0)/1048576 AS      [partition_size_gb]
,           p.[rows]                        AS      [partition_row_count]
,           rv.[value]                      AS      [partition_boundary_value]
,           p.[data_compression_desc]       AS      [partition_compression_desc]
FROM        sys.schemas s
JOIN        sys.tables t                    ON      t.[schema_id]         = s.[schema_id]
JOIN        sys.partitions p                ON      p.[object_id]         = t.[object_id]
JOIN        sys.allocation_units a          ON      a.[container_id]      = p.[partition_id]
JOIN        sys.indexes i                   ON      i.[object_id]         = p.[object_id]
                                            AND     i.[index_id]          = p.[index_id]
JOIN        sys.data_spaces ds              ON      ds.[data_space_id]    = i.[data_space_id]
LEFT JOIN   sys.partition_schemes ps        ON      ps.[data_space_id]    = ds.[data_space_id]
LEFT JOIN   sys.partition_functions pf      ON      pf.[function_id]      = ps.[function_id]
LEFT JOIN   sys.partition_range_values rv   ON      rv.[function_id]      = pf.[function_id]
                                            AND     rv.[boundary_id]      = p.[partition_number]
WHERE       p.[index_id] <=1
GROUP BY    s.[name]
,           t.[name]
,           i.[name]
,           p.[partition_number]
,           p.[rows]
,           rv.[value]
,           p.[data_compression_desc]
;
```

## <a name="workload-management"></a>Gerenciamento de carga de trabalho
É um toofactor de consideração parte final na decisão de partição de tabela toohello [gerenciamento de carga de trabalho][workload management].  Gerenciamento de carga de trabalho no SQL Data Warehouse é principalmente de saudação gerenciamento de memória e simultaneidade.  Olá SQL Data Warehouse memória máxima alocada a distribuição tooeach durante a execução da consulta é classes de recursos controlados.  Idealmente, suas partições serão dimensionadas em relação aos outros fatores, como Olá necessidades de memória de compilação de índices columnstore clusterizados.  Os índices columnstore clusterizados são melhores quando têm mais memória alocada.  Portanto, você desejará tooensure recriar um índice de partição não fiquem sem de memória. Saudação de aumento da memória disponível tooyour consulta pode ser obtida com a troca de função padrão de saudação, smallrc, tooone de Olá outras funções, como largerc.

Obter informações sobre alocação de saudação de memória por distribuição estão disponíveis consultando as exibições de gerenciamento dinâmico Olá resource governor. Na realidade a concessão de memória será menor do que figuras de saudação abaixo. No entanto, isso fornece um nível de diretrizes que podem ser usados ao dimensionar suas partições para operações de gerenciamento de dados.  Tente tooavoid suas partições além da concessão de memória Olá fornecida pela classe de recurso muito grande de saudação de dimensionamento. Se as partições ultrapassem nesta figura você corre o risco de saudação de pressão de memória, que por sua vez, leva compactação ideal tooless.

```sql
SELECT  rp.[name]                                AS [pool_name]
,       rp.[max_memory_kb]                        AS [max_memory_kb]
,       rp.[max_memory_kb]/1024                    AS [max_memory_mb]
,       rp.[max_memory_kb]/1048576                AS [mex_memory_gb]
,       rp.[max_memory_percent]                    AS [max_memory_percent]
,       wg.[name]                                AS [group_name]
,       wg.[importance]                            AS [group_importance]
,       wg.[request_max_memory_grant_percent]    AS [request_max_memory_grant_percent]
FROM    sys.dm_pdw_nodes_resource_governor_workload_groups    wg
JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools    rp ON wg.[pool_id] = rp.[pool_id]
WHERE   wg.[name] like 'SloDWGroup%'
AND     rp.[name]    = 'SloDWPool'
;
```

## <a name="partition-switching"></a>Alternância de partição
O SQL Data Warehouse dá suporte à divisão, mesclagem e comutação de partição. Cada uma dessas funções é excuted usando Olá [ALTER TABLE] [ ALTER TABLE] instrução.

partições de tooswitch entre duas tabelas, que você deve garantir que partições Olá alinham em seus respectivos limites e se as definições de tabela Olá correspondem. Como restrições de verificação não estão disponíveis tooenforce intervalo de saudação de valores em uma tabela de origem de saudação da tabela deve conter Olá mesmo limites de partição como tabela de destino de saudação. Se não for o caso de Olá, alternância de partição Olá falhará como Olá metadados da partição não serão sincronizados.

### <a name="how-toosplit-a-partition-that-contains-data"></a>Como toosplit uma partição que contém dados
Olá, mais eficiente método toosplit uma partição que já contém dados é toouse um `CTAS` instrução. Se a tabela particionada Olá é uma columnstore clusterizada, em seguida, partição de tabela Olá deve estar vazia antes ela pode ser dividida.

Veja abaixo um exemplo de tabela columnstore particionada que contém uma linha em cada partição:

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
        [ProductKey]            int          NOT NULL
    ,   [OrderDateKey]          int          NOT NULL
    ,   [CustomerKey]           int          NOT NULL
    ,   [PromotionKey]          int          NOT NULL
    ,   [SalesOrderNumber]      nvarchar(20) NOT NULL
    ,   [OrderQuantity]         smallint     NOT NULL
    ,   [UnitPrice]             money        NOT NULL
    ,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    (20000101
                    )
                )
)
;

INSERT INTO dbo.FactInternetSales
VALUES (1,19990101,1,1,1,1,1,1);
INSERT INTO dbo.FactInternetSales
VALUES (1,20000101,1,1,1,1,1,1);


CREATE STATISTICS Stat_dbo_FactInternetSales_OrderDateKey ON dbo.FactInternetSales(OrderDateKey);
```

> [!NOTE]
> Criando objeto de estatística hello, garantimos que metadados de tabela são mais preciso. Se omitirmos a criação de estatísticas, o SQL Data Warehouse usará os valores padrão. Para obter detalhes sobre as estatísticas examine [estatísticas][statistics].
> 
> 

Podemos pode fazer consultas para contagem de linhas de saudação usando Olá `sys.partitions` exibição do catálogo:

```sql
SELECT  QUOTENAME(s.[name])+'.'+QUOTENAME(t.[name]) as Table_name
,       i.[name] as Index_name
,       p.partition_number as Partition_nmbr
,       p.[rows] as Row_count
,       p.[data_compression_desc] as Data_Compression_desc
FROM    sys.partitions p
JOIN    sys.tables     t    ON    p.[object_id]   = t.[object_id]
JOIN    sys.schemas    s    ON    t.[schema_id]   = s.[schema_id]
JOIN    sys.indexes    i    ON    p.[object_id]   = i.[object_Id]
                            AND   p.[index_Id]    = i.[index_Id]
WHERE t.[name] = 'FactInternetSales'
;
```

Se tentarmos toosplit nesta tabela, obtemos um erro:

```sql
ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

Msg 35346, nível 15, estado 1, linha 44 DIVIDIDA cláusula da instrução ALTER PARTITION falhou porque Olá partição não está vazia.  Somente partições vazias podem ser divididas quando existe um índice na tabela de saudação. Considere desabilitar o índice de columnstore Olá antes de emitir a instrução ALTER PARTITION de saudação e a recompilação de índice de columnstore Olá depois de ALTER PARTITION estar concluído.

No entanto, podemos usar `CTAS` toocreate um novo toohold de tabela nossos dados.

```sql
CREATE TABLE dbo.FactInternetSales_20000101
    WITH    (   DISTRIBUTION = HASH(ProductKey)
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101
                                )
                            )
            )
AS
SELECT *
FROM    FactInternetSales
WHERE   1=2
;
```

Como os limites de partição Olá são alinhados um comutador é permitido. Isso deixará a tabela de origem Olá com uma partição vazia que podemos subsequentemente dividir.

```sql
ALTER TABLE FactInternetSales SWITCH PARTITION 2 too FactInternetSales_20000101 PARTITION 2;

ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

Tudo o que resta toodo é tooalign toohello nossos dados de partição novos limites usando `CTAS` e alternar nossos dados de volta na tabela principal toohello

```sql
CREATE TABLE [dbo].[FactInternetSales_20000101_20010101]
    WITH    (   DISTRIBUTION = HASH([ProductKey])
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101,20010101
                                )
                            )
            )
AS
SELECT  *
FROM    [dbo].[FactInternetSales_20000101]
WHERE   [OrderDateKey] >= 20000101
AND     [OrderDateKey] <  20010101
;

ALTER TABLE dbo.FactInternetSales_20000101_20010101 SWITCH PARTITION 2 toodbo.FactInternetSales PARTITION 2;
```

Depois de concluir a movimentação de saudação de dados de saudação é estatísticas de saudação de toorefresh uma boa ideia eles refletem com precisão em tooensure de tabela de destino Olá distribuição de nova Olá dos dados de saudação em suas respectivas partições:

```sql
UPDATE STATISTICS [dbo].[FactInternetSales];
```

### <a name="table-partitioning-source-control"></a>Controle da origem do particionamento da tabela
tooavoid sua definição da tabela de **enferrujado** em seu sistema de controle de origem, você pode desejar Olá tooconsider abordagem a seguir:

1. Criar tabela hello como uma tabela particionada, mas sem valores de partição

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
    [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    ()
                )
)
;
```

1. `SPLIT`tabela Hello como parte do processo de implantação de saudação:

```sql
-- Create a table containing hello partition boundaries

CREATE TABLE #partitions
WITH
(
    LOCATION = USER_DB
,   DISTRIBUTION = HASH(ptn_no)
)
AS
SELECT  ptn_no
,       ROW_NUMBER() OVER (ORDER BY (ptn_no)) as seq_no
FROM    (
        SELECT CAST(20000101 AS INT) ptn_no
        UNION ALL
        SELECT CAST(20010101 AS INT)
        UNION ALL
        SELECT CAST(20020101 AS INT)
        UNION ALL
        SELECT CAST(20030101 AS INT)
        UNION ALL
        SELECT CAST(20040101 AS INT)
        ) a
;

-- Iterate over hello partition boundaries and split hello table

DECLARE @c INT = (SELECT COUNT(*) FROM #partitions)
,       @i INT = 1                                 --iterator for while loop
,       @q NVARCHAR(4000)                          --query
,       @p NVARCHAR(20)     = N''                  --partition_number
,       @s NVARCHAR(128)    = N'dbo'               --schema
,       @t NVARCHAR(128)    = N'FactInternetSales' --table
;

WHILE @i <= @c
BEGIN
    SET @p = (SELECT ptn_no FROM #partitions WHERE seq_no = @i);
    SET @q = (SELECT N'ALTER TABLE '+@s+N'.'+@t+N' SPLIT RANGE ('+@p+N');');

    -- PRINT @q;
    EXECUTE sp_executesql @q;

    SET @i+=1;
END

-- Code clean-up

DROP TABLE #partitions;
```

Com hello essa abordagem código no controle de origem permanece estático e valores de limite de particionamento de saudação são permitidos toobe dinâmico; Desenvolvendo com warehouse Olá ao longo do tempo.

## <a name="next-steps"></a>Próximas etapas
toolearn mais, consulte os artigos de saudação em [visão geral da tabela][Overview], [tipos de dados de tabela][Data Types], [distribuir uma tabela] [ Distribute], [Indexando uma tabela][Index], [manter estatísticas de tabela] [ Statistics] e [ Tabelas temporárias][Temporary].  Para saber mais sobre as práticas recomendadas, consulte [Práticas Recomendadas do SQL Data Warehouse][SQL Data Warehouse Best Practices].

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[workload management]: ./sql-data-warehouse-develop-concurrency.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!-- MSDN Articles -->
[Partitioned Tables and Indexes]: https://msdn.microsoft.com/library/ms190787.aspx
[ALTER TABLE]: https://msdn.microsoft.com/en-us/library/ms190273.aspx
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[partition function]: https://msdn.microsoft.com/library/ms187802.aspx
[partition scheme]: https://msdn.microsoft.com/library/ms179854.aspx


<!-- Other web references -->
