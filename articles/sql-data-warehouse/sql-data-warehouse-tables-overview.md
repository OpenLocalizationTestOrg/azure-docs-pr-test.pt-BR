---
title: aaaOverview de tabelas no Data Warehouse SQL | Microsoft Docs
description: "Introdução às Tabelas do SQL Data Warehouse do Azure."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 2114d9ad-c113-43da-859f-419d72604bdf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 06/29/2016
ms.author: shigu;jrj
ms.openlocfilehash: 4edabcb4b0754bf6c99c2b6b3f0c077749051d9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-tables-in-sql-data-warehouse"></a>Visão geral das tabelas no SQL Data Warehouse
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

A introdução à criação de tabelas no SQL Data Warehouse é simples.  Olá básico [CREATE TABLE] [ CREATE TABLE] sintaxe segue a sintaxe comum hello, provavelmente já conhece de trabalhar com outros bancos de dados.  toocreate uma tabela, basta tooname sua tabela, nomear suas colunas e definir os tipos de dados para cada coluna.  Se você criar tabelas em outros bancos de dados, isso deve ser bastante familiar tooyou.

```sql  
CREATE TABLE Customers (FirstName VARCHAR(25), LastName VARCHAR(25))
 ``` 

Olá exemplo acima cria uma tabela denominada clientes com duas colunas, FirstName e LastName.  Cada coluna é definida com um tipo de dados de varchar (25), o que limita os caracteres de too25 Olá dados.  Esses atributos fundamentais de uma tabela, bem como outras, são principalmente Olá igual a outros bancos de dados.  Tipos de dados são definidos para cada coluna e garantem a integridade de saudação de seus dados.  Índices podem ser adicionados tooimprove desempenho, reduzindo a e/s.  O particionamento pode ser adicionado tooimprove desempenho quando você precisar toomodify dados.

[Renomear][RENAME] uma tabela do SQL Data Warehouse fica assim:

```sql  
RENAME OBJECT Customer tooCustomerOrig; 
 ```

## <a name="distributed-tables"></a>Tabelas distribuídas
Um novo atributo fundamental introduzido por sistemas distribuídos, como o SQL Data Warehouse é hello **coluna de distribuição**.  coluna de distribuição de saudação é muito o que parece.  É a coluna de saudação que determina como toodistribute, ou divisão, os dados em segundo plano da saudação.  Quando você cria uma tabela sem especificar a coluna de distribuição hello, tabela Olá é automaticamente distribuída usando **rodízio**.  Embora as tabelas round robin possam ser suficientes em alguns cenários, definir colunas de distribuição pode reduzir muito a movimentação dos dados durante as consultas, otimizando o desempenho.  Em situações em que há uma pequena quantidade de dados em uma tabela, escolhendo toocreate tabela Olá Olá **replicar** tipo de distribuição copia o nó de computação tooeach de dados e salva a movimentação de dados em tempo de execução de consulta. Consulte [distribuir uma tabela] [ Distribute] toolearn mais informações sobre como tooselect uma coluna de distribuição.

## <a name="indexing-and-partitioning-tables"></a>Indexação e particionamento de tabelas
Como você se tornam mais avançadas usando o SQL Data Warehouse e desejar toooptimize desempenho, você desejará toolearn mais sobre o Design de tabela.  toolearn mais, consulte os artigos de saudação em [tipos de dados de tabela][Data Types], [distribuir uma tabela][Distribute], [indexando uma tabela] [ Index] e [particionar uma tabela][Partition].

## <a name="table-statistics"></a>Estatísticas da tabela
As estatísticas são um toogetting extremamente importante Olá melhor desempenho do Data Warehouse do SQL.  Como o SQL Data Warehouse ainda não foram automaticamente criar e atualizar estatísticas, como você pode ter vindo tooexpect no banco de dados do SQL Azure, lendo nosso artigo em [estatísticas] [ Statistics] pode ser uma saudação artigos mais importantes ler tooensure obter um melhor desempenho de saudação de suas consultas.

## <a name="temporary-tables"></a>Tabelas temporárias
Tabelas temporárias são tabelas que só existem durante saudação seu logon e não podem ser vistas por outros usuários.  Tabelas temporárias podem ser uma boa maneira tooprevent outros visualizem os resultados temporários de e também reduz a necessidade de saudação de limpeza.  Como as tabelas temporárias também utilizam o armazenamento local, podem oferecer um desempenho mais rápido para algumas operações.  Consulte Olá [tabela temporária] [ Temporary] artigos para obter mais detalhes sobre tabelas temporárias.

## <a name="external-tables"></a>Tabelas externas
Tabelas externas, também conhecido como tabelas do Polybase, são tabelas que podem ser consultadas de SQL Data Warehouse, mas toodata ponto externa do SQL Data Warehouse.  Por exemplo, você pode criar uma tabela externa que toofiles pontos no armazenamento de BLOBs do Azure.  Para obter mais detalhes sobre como toocreate e consulta uma tabela externa, consulte [carregar dados com o Polybase][Load data with Polybase].  

## <a name="unsupported-table-features"></a>Recursos da tabela sem suporte
Enquanto o SQL Data Warehouse contém muitos dos mesmos recursos de tabela oferecidos por outros bancos de dados de saudação, há alguns recursos que ainda não têm suporte.  Abaixo está uma lista de alguns dos Olá recursos de tabela que ainda não têm suporte.

| Recursos sem suporte |
| --- |
| Chave primária, Chaves estrangeiras, Exclusiva e Verificação [Restrições da Tabela][Table Constraints] |
| [Índices Exclusivos][Unique Indexes] |
| [Colunas Computadas][Computed Columns] |
| [Colunas Esparsas][Sparse Columns] |
| [Tipos Definidos pelo Usuário][User-Defined Types] |
| [Sequência][Sequence] |
| [Gatilhos][Triggers] |
| [Exibições Indexadas][Indexed Views] |
| [Sinônimos][Synonyms] |

## <a name="table-size-queries"></a>Consultas do tamanho da tabela
Um espaço de tooidentify de maneira simples e linhas consumidas por uma tabela em cada uma das distribuições de saudação 60 é toouse [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED].

```sql
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

No entanto, usar comandos DBCC pode ser bastante limitado.  Exibições de gerenciamento dinâmico (DMVs) permitirá que você toosee muito mais detalhes, bem como oferecem muito mais controle sobre os resultados da consulta hello.  Comece criando nesta exibição, que será chamado tooby muitos exemplos neste e em outros artigos.

```sql
CREATE VIEW dbo.vTableSizes
AS
WITH base
AS
(
SELECT 
 GETDATE()                                                             AS  [execution_time]
, DB_NAME()                                                            AS  [database_name]
, s.name                                                               AS  [schema_name]
, t.name                                                               AS  [table_name]
, QUOTENAME(s.name)+'.'+QUOTENAME(t.name)                              AS  [two_part_name]
, nt.[name]                                                            AS  [node_table_name]
, ROW_NUMBER() OVER(PARTITION BY nt.[name] ORDER BY (SELECT NULL))     AS  [node_table_name_seq]
, tp.[distribution_policy_desc]                                        AS  [distribution_policy_name]
, c.[name]                                                             AS  [distribution_column]
, nt.[distribution_id]                                                 AS  [distribution_id]
, i.[type]                                                             AS  [index_type]
, i.[type_desc]                                                        AS  [index_type_desc]
, nt.[pdw_node_id]                                                     AS  [pdw_node_id]
, pn.[type]                                                            AS  [pdw_node_type]
, pn.[name]                                                            AS  [pdw_node_name]
, di.name                                                              AS  [dist_name]
, di.position                                                          AS  [dist_position]
, nps.[partition_number]                                               AS  [partition_nmbr]
, nps.[reserved_page_count]                                            AS  [reserved_space_page_count]
, nps.[reserved_page_count] - nps.[used_page_count]                    AS  [unused_space_page_count]
, nps.[in_row_data_page_count] 
    + nps.[row_overflow_used_page_count] 
    + nps.[lob_used_page_count]                                        AS  [data_space_page_count]
, nps.[reserved_page_count] 
 - (nps.[reserved_page_count] - nps.[used_page_count]) 
 - ([in_row_data_page_count] 
         + [row_overflow_used_page_count]+[lob_used_page_count])       AS  [index_space_page_count]
, nps.[row_count]                                                      AS  [row_count]
from 
    sys.schemas s
INNER JOIN sys.tables t
    ON s.[schema_id] = t.[schema_id]
INNER JOIN sys.indexes i
    ON  t.[object_id] = i.[object_id]
    AND i.[index_id] <= 1
INNER JOIN sys.pdw_table_distribution_properties tp
    ON t.[object_id] = tp.[object_id]
INNER JOIN sys.pdw_table_mappings tm
    ON t.[object_id] = tm.[object_id]
INNER JOIN sys.pdw_nodes_tables nt
    ON tm.[physical_name] = nt.[name]
INNER JOIN sys.dm_pdw_nodes pn
    ON  nt.[pdw_node_id] = pn.[pdw_node_id]
INNER JOIN sys.pdw_distributions di
    ON  nt.[distribution_id] = di.[distribution_id]
INNER JOIN sys.dm_pdw_nodes_db_partition_stats nps
    ON nt.[object_id] = nps.[object_id]
    AND nt.[pdw_node_id] = nps.[pdw_node_id]
    AND nt.[distribution_id] = nps.[distribution_id]
LEFT OUTER JOIN (select * from sys.pdw_column_distribution_properties where distribution_ordinal = 1) cdp
    ON t.[object_id] = cdp.[object_id]
LEFT OUTER JOIN sys.columns c
    ON cdp.[object_id] = c.[object_id]
    AND cdp.[column_id] = c.[column_id]
)
, size
AS
(
SELECT
   [execution_time]
,  [database_name]
,  [schema_name]
,  [table_name]
,  [two_part_name]
,  [node_table_name]
,  [node_table_name_seq]
,  [distribution_policy_name]
,  [distribution_column]
,  [distribution_id]
,  [index_type]
,  [index_type_desc]
,  [pdw_node_id]
,  [pdw_node_type]
,  [pdw_node_name]
,  [dist_name]
,  [dist_position]
,  [partition_nmbr]
,  [reserved_space_page_count]
,  [unused_space_page_count]
,  [data_space_page_count]
,  [index_space_page_count]
,  [row_count]
,  ([reserved_space_page_count] * 8.0)                                 AS [reserved_space_KB]
,  ([reserved_space_page_count] * 8.0)/1000                            AS [reserved_space_MB]
,  ([reserved_space_page_count] * 8.0)/1000000                         AS [reserved_space_GB]
,  ([reserved_space_page_count] * 8.0)/1000000000                      AS [reserved_space_TB]
,  ([unused_space_page_count]   * 8.0)                                 AS [unused_space_KB]
,  ([unused_space_page_count]   * 8.0)/1000                            AS [unused_space_MB]
,  ([unused_space_page_count]   * 8.0)/1000000                         AS [unused_space_GB]
,  ([unused_space_page_count]   * 8.0)/1000000000                      AS [unused_space_TB]
,  ([data_space_page_count]     * 8.0)                                 AS [data_space_KB]
,  ([data_space_page_count]     * 8.0)/1000                            AS [data_space_MB]
,  ([data_space_page_count]     * 8.0)/1000000                         AS [data_space_GB]
,  ([data_space_page_count]     * 8.0)/1000000000                      AS [data_space_TB]
,  ([index_space_page_count]  * 8.0)                                   AS [index_space_KB]
,  ([index_space_page_count]  * 8.0)/1000                              AS [index_space_MB]
,  ([index_space_page_count]  * 8.0)/1000000                           AS [index_space_GB]
,  ([index_space_page_count]  * 8.0)/1000000000                        AS [index_space_TB]
FROM base
)
SELECT * 
FROM size
;
```

### <a name="table-space-summary"></a>Resumo do espaço da tabela
Essa consulta retorna linhas de saudação e espaço por tabela.  É um toosee excelente consulta as tabelas são maiores tabelas e se elas são rodízio, replicados ou distribuídos de hash.  Tabelas de hash distribuída também mostra coluna de distribuição de saudação.  Na maioria dos casos, suas tabelas maiores devem ser distribuídas em hash com um índice columnstore clusterizado.

```sql
SELECT 
     database_name
,    schema_name
,    table_name
,    distribution_policy_name
,      distribution_column
,    index_type_desc
,    COUNT(distinct partition_nmbr) as nbr_partitions
,    SUM(row_count)                 as table_row_count
,    SUM(reserved_space_GB)         as table_reserved_space_GB
,    SUM(data_space_GB)             as table_data_space_GB
,    SUM(index_space_GB)            as table_index_space_GB
,    SUM(unused_space_GB)           as table_unused_space_GB
FROM 
    dbo.vTableSizes
GROUP BY 
     database_name
,    schema_name
,    table_name
,    distribution_policy_name
,      distribution_column
,    index_type_desc
ORDER BY
    table_reserved_space_GB desc
;
```

### <a name="table-space-by-distribution-type"></a>Espaço da tabela pelo tipo de distribuição
```sql
SELECT 
     distribution_policy_name
,    SUM(row_count)                as table_type_row_count
,    SUM(reserved_space_GB)        as table_type_reserved_space_GB
,    SUM(data_space_GB)            as table_type_data_space_GB
,    SUM(index_space_GB)           as table_type_index_space_GB
,    SUM(unused_space_GB)          as table_type_unused_space_GB
FROM dbo.vTableSizes
GROUP BY distribution_policy_name
;
```

### <a name="table-space-by-index-type"></a>Espaço da tabela pelo tipo de índice
```sql
SELECT 
     index_type_desc
,    SUM(row_count)                as table_type_row_count
,    SUM(reserved_space_GB)        as table_type_reserved_space_GB
,    SUM(data_space_GB)            as table_type_data_space_GB
,    SUM(index_space_GB)           as table_type_index_space_GB
,    SUM(unused_space_GB)          as table_type_unused_space_GB
FROM dbo.vTableSizes
GROUP BY index_type_desc
;
```

### <a name="distribution-space-summary"></a>Resumo do espaço de distribuição
```sql
SELECT 
    distribution_id
,    SUM(row_count)                as total_node_distribution_row_count
,    SUM(reserved_space_MB)        as total_node_distribution_reserved_space_MB
,    SUM(data_space_MB)            as total_node_distribution_data_space_MB
,    SUM(index_space_MB)           as total_node_distribution_index_space_MB
,    SUM(unused_space_MB)          as total_node_distribution_unused_space_MB
FROM dbo.vTableSizes
GROUP BY     distribution_id
ORDER BY    distribution_id
;
```

## <a name="next-steps"></a>Próximas etapas
toolearn mais, consulte os artigos de saudação em [tipos de dados de tabela][Data Types], [distribuir uma tabela][Distribute], [indexando uma tabela] [ Index], [Particionar uma tabela][Partition], [manter estatísticas de tabela] [ Statistics] e [ Tabelas temporárias][Temporary].  Para saber mais sobre as práticas recomendadas, consulte [Práticas Recomendadas do SQL Data Warehouse][SQL Data Warehouse Best Practices].

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md
[Load data with Polybase]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md

<!--MSDN references-->
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[RENAME]: https://msdn.microsoft.com/library/mt631611.aspx
[DBCC PDW_SHOWSPACEUSED]: https://msdn.microsoft.com/library/mt204028.aspx
[Table Constraints]: https://msdn.microsoft.com/library/ms188066.aspx
[Computed Columns]: https://msdn.microsoft.com/library/ms186241.aspx
[Sparse Columns]: https://msdn.microsoft.com/library/cc280604.aspx
[User-Defined Types]: https://msdn.microsoft.com/library/ms131694.aspx
[Sequence]: https://msdn.microsoft.com/library/ff878091.aspx
[Triggers]: https://msdn.microsoft.com/library/ms189799.aspx
[Indexed Views]: https://msdn.microsoft.com/library/ms191432.aspx
[Synonyms]: https://msdn.microsoft.com/library/ms177544.aspx
[Unique Indexes]: https://msdn.microsoft.com/library/ms188783.aspx

<!--Other Web references-->
