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
# <a name="overview-of-tables-in-sql-data-warehouse"></a><span data-ttu-id="d4d4f-103">Visão geral das tabelas no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d4d4f-103">Overview of tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="d4d4f-104">[Visão geral][Overview]</span><span class="sxs-lookup"><span data-stu-id="d4d4f-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="d4d4f-105">[Tipos de Dados][Data Types]</span><span class="sxs-lookup"><span data-stu-id="d4d4f-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="d4d4f-106">[Distribuir][Distribute]</span><span class="sxs-lookup"><span data-stu-id="d4d4f-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="d4d4f-107">[Índice][Index]</span><span class="sxs-lookup"><span data-stu-id="d4d4f-107">[Index][Index]</span></span>
> * <span data-ttu-id="d4d4f-108">[Partição][Partition]</span><span class="sxs-lookup"><span data-stu-id="d4d4f-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="d4d4f-109">[Estatísticas][Statistics]</span><span class="sxs-lookup"><span data-stu-id="d4d4f-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="d4d4f-110">[Temporário][Temporary]</span><span class="sxs-lookup"><span data-stu-id="d4d4f-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="d4d4f-111">A introdução à criação de tabelas no SQL Data Warehouse é simples.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-111">Getting started with creating tables in SQL Data Warehouse is simple.</span></span>  <span data-ttu-id="d4d4f-112">Olá básico [CREATE TABLE] [ CREATE TABLE] sintaxe segue a sintaxe comum hello, provavelmente já conhece de trabalhar com outros bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-112">hello basic [CREATE TABLE][CREATE TABLE] syntax follows hello common syntax you are most likely already familiar with from working with other databases.</span></span>  <span data-ttu-id="d4d4f-113">toocreate uma tabela, basta tooname sua tabela, nomear suas colunas e definir os tipos de dados para cada coluna.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-113">toocreate a table, you simply need tooname your table, name your columns and define data types for each column.</span></span>  <span data-ttu-id="d4d4f-114">Se você criar tabelas em outros bancos de dados, isso deve ser bastante familiar tooyou.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-114">If you've create tables in other databases, this should look very familiar tooyou.</span></span>

```sql  
CREATE TABLE Customers (FirstName VARCHAR(25), LastName VARCHAR(25))
 ``` 

<span data-ttu-id="d4d4f-115">Olá exemplo acima cria uma tabela denominada clientes com duas colunas, FirstName e LastName.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-115">hello above example creates a table named Customers with two columns, FirstName and LastName.</span></span>  <span data-ttu-id="d4d4f-116">Cada coluna é definida com um tipo de dados de varchar (25), o que limita os caracteres de too25 Olá dados.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-116">Each column is defined with a data type of VARCHAR(25), which limits hello data too25 characters.</span></span>  <span data-ttu-id="d4d4f-117">Esses atributos fundamentais de uma tabela, bem como outras, são principalmente Olá igual a outros bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-117">These fundamental attributes of a table, as well as others, are mostly hello same as other databases.</span></span>  <span data-ttu-id="d4d4f-118">Tipos de dados são definidos para cada coluna e garantem a integridade de saudação de seus dados.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-118">Data types are defined for each column and ensure hello integrity of your data.</span></span>  <span data-ttu-id="d4d4f-119">Índices podem ser adicionados tooimprove desempenho, reduzindo a e/s.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-119">Indexes can be added tooimprove performance by reducing I/O.</span></span>  <span data-ttu-id="d4d4f-120">O particionamento pode ser adicionado tooimprove desempenho quando você precisar toomodify dados.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-120">Partitioning can be added tooimprove performance when you need toomodify data.</span></span>

<span data-ttu-id="d4d4f-121">[Renomear][RENAME] uma tabela do SQL Data Warehouse fica assim:</span><span class="sxs-lookup"><span data-stu-id="d4d4f-121">[Renaming][RENAME] a SQL Data Warehouse table looks like this:</span></span>

```sql  
RENAME OBJECT Customer tooCustomerOrig; 
 ```

## <a name="distributed-tables"></a><span data-ttu-id="d4d4f-122">Tabelas distribuídas</span><span class="sxs-lookup"><span data-stu-id="d4d4f-122">Distributed tables</span></span>
<span data-ttu-id="d4d4f-123">Um novo atributo fundamental introduzido por sistemas distribuídos, como o SQL Data Warehouse é hello **coluna de distribuição**.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-123">A new fundamental attribute introduced by distributed systems like SQL Data Warehouse is hello **distribution column**.</span></span>  <span data-ttu-id="d4d4f-124">coluna de distribuição de saudação é muito o que parece.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-124">hello distribution column is very much what it sounds like.</span></span>  <span data-ttu-id="d4d4f-125">É a coluna de saudação que determina como toodistribute, ou divisão, os dados em segundo plano da saudação.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-125">It is hello column that determines how toodistribute, or divide, your data behind hello scenes.</span></span>  <span data-ttu-id="d4d4f-126">Quando você cria uma tabela sem especificar a coluna de distribuição hello, tabela Olá é automaticamente distribuída usando **rodízio**.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-126">When you create a table without specifying hello distribution column, hello table is automatically distributed using **round robin**.</span></span>  <span data-ttu-id="d4d4f-127">Embora as tabelas round robin possam ser suficientes em alguns cenários, definir colunas de distribuição pode reduzir muito a movimentação dos dados durante as consultas, otimizando o desempenho.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-127">While round robin tables can be sufficient in some scenarios, defining distribution columns can greatly reduce data movement during queries, thus optimizing performance.</span></span>  <span data-ttu-id="d4d4f-128">Em situações em que há uma pequena quantidade de dados em uma tabela, escolhendo toocreate tabela Olá Olá **replicar** tipo de distribuição copia o nó de computação tooeach de dados e salva a movimentação de dados em tempo de execução de consulta.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-128">In situations where there is a small amount of data in a table, choosing toocreate hello table with hello **replicate** distribution type copies data tooeach compute node and saves data movement at query execution time.</span></span> <span data-ttu-id="d4d4f-129">Consulte [distribuir uma tabela] [ Distribute] toolearn mais informações sobre como tooselect uma coluna de distribuição.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-129">See [Distributing a Table][Distribute] toolearn more about how tooselect a distribution column.</span></span>

## <a name="indexing-and-partitioning-tables"></a><span data-ttu-id="d4d4f-130">Indexação e particionamento de tabelas</span><span class="sxs-lookup"><span data-stu-id="d4d4f-130">Indexing and partitioning tables</span></span>
<span data-ttu-id="d4d4f-131">Como você se tornam mais avançadas usando o SQL Data Warehouse e desejar toooptimize desempenho, você desejará toolearn mais sobre o Design de tabela.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-131">As you become more advanced in using SQL Data Warehouse and want toooptimize performance, you'll want toolearn more about Table Design.</span></span>  <span data-ttu-id="d4d4f-132">toolearn mais, consulte os artigos de saudação em [tipos de dados de tabela][Data Types], [distribuir uma tabela][Distribute], [indexando uma tabela] [ Index] e [particionar uma tabela][Partition].</span><span class="sxs-lookup"><span data-stu-id="d4d4f-132">toolearn more, see hello articles on [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index] and  [Partitioning a Table][Partition].</span></span>

## <a name="table-statistics"></a><span data-ttu-id="d4d4f-133">Estatísticas da tabela</span><span class="sxs-lookup"><span data-stu-id="d4d4f-133">Table statistics</span></span>
<span data-ttu-id="d4d4f-134">As estatísticas são um toogetting extremamente importante Olá melhor desempenho do Data Warehouse do SQL.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-134">Statistics are an extremely important toogetting hello best performance out of your SQL Data Warehouse.</span></span>  <span data-ttu-id="d4d4f-135">Como o SQL Data Warehouse ainda não foram automaticamente criar e atualizar estatísticas, como você pode ter vindo tooexpect no banco de dados do SQL Azure, lendo nosso artigo em [estatísticas] [ Statistics] pode ser uma saudação artigos mais importantes ler tooensure obter um melhor desempenho de saudação de suas consultas.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-135">Since SQL Data Warehouse does not yet automatically create and update statistics for you, like you may have come tooexpect in Azure SQL Database, reading our article on [Statistics][Statistics] might be one of hello most important articles you read tooensure that you get hello best performance from your queries.</span></span>

## <a name="temporary-tables"></a><span data-ttu-id="d4d4f-136">Tabelas temporárias</span><span class="sxs-lookup"><span data-stu-id="d4d4f-136">Temporary tables</span></span>
<span data-ttu-id="d4d4f-137">Tabelas temporárias são tabelas que só existem durante saudação seu logon e não podem ser vistas por outros usuários.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-137">Temporary tables are tables which only exist for hello duration of your logon and cannot be seen by other users.</span></span>  <span data-ttu-id="d4d4f-138">Tabelas temporárias podem ser uma boa maneira tooprevent outros visualizem os resultados temporários de e também reduz a necessidade de saudação de limpeza.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-138">Temporary tables can be a good way tooprevent others from seeing temporary results and also reduce hello need for cleanup.</span></span>  <span data-ttu-id="d4d4f-139">Como as tabelas temporárias também utilizam o armazenamento local, podem oferecer um desempenho mais rápido para algumas operações.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-139">Since temporary tables also utilize local storage, they can offer faster performance for some operations.</span></span>  <span data-ttu-id="d4d4f-140">Consulte Olá [tabela temporária] [ Temporary] artigos para obter mais detalhes sobre tabelas temporárias.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-140">See hello [Temporary Table][Temporary] articles for more details about temporary tables.</span></span>

## <a name="external-tables"></a><span data-ttu-id="d4d4f-141">Tabelas externas</span><span class="sxs-lookup"><span data-stu-id="d4d4f-141">External tables</span></span>
<span data-ttu-id="d4d4f-142">Tabelas externas, também conhecido como tabelas do Polybase, são tabelas que podem ser consultadas de SQL Data Warehouse, mas toodata ponto externa do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-142">External tables, also known as Polybase tables, are tables which can be queried from SQL Data Warehouse, but point toodata external from SQL Data Warehouse.</span></span>  <span data-ttu-id="d4d4f-143">Por exemplo, você pode criar uma tabela externa que toofiles pontos no armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-143">For example, you can create an external table which points toofiles on Azure Blob Storage.</span></span>  <span data-ttu-id="d4d4f-144">Para obter mais detalhes sobre como toocreate e consulta uma tabela externa, consulte [carregar dados com o Polybase][Load data with Polybase].</span><span class="sxs-lookup"><span data-stu-id="d4d4f-144">For more details on how toocreate and query an external table, see [Load data with Polybase][Load data with Polybase].</span></span>  

## <a name="unsupported-table-features"></a><span data-ttu-id="d4d4f-145">Recursos da tabela sem suporte</span><span class="sxs-lookup"><span data-stu-id="d4d4f-145">Unsupported table features</span></span>
<span data-ttu-id="d4d4f-146">Enquanto o SQL Data Warehouse contém muitos dos mesmos recursos de tabela oferecidos por outros bancos de dados de saudação, há alguns recursos que ainda não têm suporte.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-146">While SQL Data Warehouse contains many of hello same table features offered by other databases, there are some features which are not yet supported.</span></span>  <span data-ttu-id="d4d4f-147">Abaixo está uma lista de alguns dos Olá recursos de tabela que ainda não têm suporte.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-147">Below is a list of some of hello table features which are not yet supported.</span></span>

| <span data-ttu-id="d4d4f-148">Recursos sem suporte</span><span class="sxs-lookup"><span data-stu-id="d4d4f-148">Unsupported features</span></span> |
| --- |
| <span data-ttu-id="d4d4f-149">Chave primária, Chaves estrangeiras, Exclusiva e Verificação [Restrições da Tabela][Table Constraints]</span><span class="sxs-lookup"><span data-stu-id="d4d4f-149">Primary key, Foreign keys, Unique and Check [Table Constraints][Table Constraints]</span></span> |
| <span data-ttu-id="d4d4f-150">[Índices Exclusivos][Unique Indexes]</span><span class="sxs-lookup"><span data-stu-id="d4d4f-150">[Unique Indexes][Unique Indexes]</span></span> |
| <span data-ttu-id="d4d4f-151">[Colunas Computadas][Computed Columns]</span><span class="sxs-lookup"><span data-stu-id="d4d4f-151">[Computed Columns][Computed Columns]</span></span> |
| <span data-ttu-id="d4d4f-152">[Colunas Esparsas][Sparse Columns]</span><span class="sxs-lookup"><span data-stu-id="d4d4f-152">[Sparse Columns][Sparse Columns]</span></span> |
| <span data-ttu-id="d4d4f-153">[Tipos Definidos pelo Usuário][User-Defined Types]</span><span class="sxs-lookup"><span data-stu-id="d4d4f-153">[User-Defined Types][User-Defined Types]</span></span> |
| <span data-ttu-id="d4d4f-154">[Sequência][Sequence]</span><span class="sxs-lookup"><span data-stu-id="d4d4f-154">[Sequence][Sequence]</span></span> |
| <span data-ttu-id="d4d4f-155">[Gatilhos][Triggers]</span><span class="sxs-lookup"><span data-stu-id="d4d4f-155">[Triggers][Triggers]</span></span> |
| <span data-ttu-id="d4d4f-156">[Exibições Indexadas][Indexed Views]</span><span class="sxs-lookup"><span data-stu-id="d4d4f-156">[Indexed Views][Indexed Views]</span></span> |
| <span data-ttu-id="d4d4f-157">[Sinônimos][Synonyms]</span><span class="sxs-lookup"><span data-stu-id="d4d4f-157">[Synonyms][Synonyms]</span></span> |

## <a name="table-size-queries"></a><span data-ttu-id="d4d4f-158">Consultas do tamanho da tabela</span><span class="sxs-lookup"><span data-stu-id="d4d4f-158">Table size queries</span></span>
<span data-ttu-id="d4d4f-159">Um espaço de tooidentify de maneira simples e linhas consumidas por uma tabela em cada uma das distribuições de saudação 60 é toouse [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED].</span><span class="sxs-lookup"><span data-stu-id="d4d4f-159">One simple way tooidentify space and rows consumed by a table in each of hello 60 distributions, is toouse [DBCC PDW_SHOWSPACEUSED][DBCC PDW_SHOWSPACEUSED].</span></span>

```sql
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="d4d4f-160">No entanto, usar comandos DBCC pode ser bastante limitado.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-160">However, using DBCC commands can be quite limiting.</span></span>  <span data-ttu-id="d4d4f-161">Exibições de gerenciamento dinâmico (DMVs) permitirá que você toosee muito mais detalhes, bem como oferecem muito mais controle sobre os resultados da consulta hello.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-161">Dynamic management views (DMVs) will allow you toosee much more detail as well as give you much greater control over hello query results.</span></span>  <span data-ttu-id="d4d4f-162">Comece criando nesta exibição, que será chamado tooby muitos exemplos neste e em outros artigos.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-162">Start by creating this view, which will be referred tooby many of our examples in this and other articles.</span></span>

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

### <a name="table-space-summary"></a><span data-ttu-id="d4d4f-163">Resumo do espaço da tabela</span><span class="sxs-lookup"><span data-stu-id="d4d4f-163">Table space summary</span></span>
<span data-ttu-id="d4d4f-164">Essa consulta retorna linhas de saudação e espaço por tabela.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-164">This query returns hello rows and space by table.</span></span>  <span data-ttu-id="d4d4f-165">É um toosee excelente consulta as tabelas são maiores tabelas e se elas são rodízio, replicados ou distribuídos de hash.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-165">It is a great query toosee which tables are your largest tables and whether they are round robin, replicated or hash distributed.</span></span>  <span data-ttu-id="d4d4f-166">Tabelas de hash distribuída também mostra coluna de distribuição de saudação.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-166">For hash distributed tables it also shows hello distribution column.</span></span>  <span data-ttu-id="d4d4f-167">Na maioria dos casos, suas tabelas maiores devem ser distribuídas em hash com um índice columnstore clusterizado.</span><span class="sxs-lookup"><span data-stu-id="d4d4f-167">In most cases your largest tables should be hash distributed with a clustered columnstore index.</span></span>

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

### <a name="table-space-by-distribution-type"></a><span data-ttu-id="d4d4f-168">Espaço da tabela pelo tipo de distribuição</span><span class="sxs-lookup"><span data-stu-id="d4d4f-168">Table space by distribution type</span></span>
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

### <a name="table-space-by-index-type"></a><span data-ttu-id="d4d4f-169">Espaço da tabela pelo tipo de índice</span><span class="sxs-lookup"><span data-stu-id="d4d4f-169">Table space by index type</span></span>
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

### <a name="distribution-space-summary"></a><span data-ttu-id="d4d4f-170">Resumo do espaço de distribuição</span><span class="sxs-lookup"><span data-stu-id="d4d4f-170">Distribution space summary</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="d4d4f-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d4d4f-171">Next steps</span></span>
<span data-ttu-id="d4d4f-172">toolearn mais, consulte os artigos de saudação em [tipos de dados de tabela][Data Types], [distribuir uma tabela][Distribute], [indexando uma tabela] [ Index], [Particionar uma tabela][Partition], [manter estatísticas de tabela] [ Statistics] e [ Tabelas temporárias][Temporary].</span><span class="sxs-lookup"><span data-stu-id="d4d4f-172">toolearn more, see hello articles on [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="d4d4f-173">Para saber mais sobre as práticas recomendadas, consulte [Práticas Recomendadas do SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="d4d4f-173">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
