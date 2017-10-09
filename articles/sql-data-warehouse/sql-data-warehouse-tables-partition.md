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
# <a name="partitioning-tables-in-sql-data-warehouse"></a><span data-ttu-id="0c48b-103">Particionando tabelas no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="0c48b-103">Partitioning tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="0c48b-104">[Visão geral][Overview]</span><span class="sxs-lookup"><span data-stu-id="0c48b-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="0c48b-105">[Tipos de Dados][Data Types]</span><span class="sxs-lookup"><span data-stu-id="0c48b-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="0c48b-106">[Distribuir][Distribute]</span><span class="sxs-lookup"><span data-stu-id="0c48b-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="0c48b-107">[Índice][Index]</span><span class="sxs-lookup"><span data-stu-id="0c48b-107">[Index][Index]</span></span>
> * <span data-ttu-id="0c48b-108">[Partição][Partition]</span><span class="sxs-lookup"><span data-stu-id="0c48b-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="0c48b-109">[Estatísticas][Statistics]</span><span class="sxs-lookup"><span data-stu-id="0c48b-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="0c48b-110">[Temporário][Temporary]</span><span class="sxs-lookup"><span data-stu-id="0c48b-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="0c48b-111">O particionamento tem suporte em todos os tipos de tabela do SQL Data Warehouse, incluindo columnstore clusterizado, índice clusterizado e heap.</span><span class="sxs-lookup"><span data-stu-id="0c48b-111">Partitioning is supported on all SQL Data Warehouse table types; including clustered columnstore, clustered index, and heap.</span></span>  <span data-ttu-id="0c48b-112">O particionamento também tem suporte em todos os tipos de distribuição, incluindo hash ou round robin.</span><span class="sxs-lookup"><span data-stu-id="0c48b-112">Partitioning is also supported on all distribution types, including both hash or round robin distributed.</span></span>  <span data-ttu-id="0c48b-113">Particionamento permite toodivide seus dados em grupos menores de dados e na maioria dos casos, o particionamento são feitos em uma coluna de data.</span><span class="sxs-lookup"><span data-stu-id="0c48b-113">Partitioning enables you toodivide your data into smaller groups of data and in most cases, partitioning is done on a date column.</span></span>

## <a name="benefits-of-partitioning"></a><span data-ttu-id="0c48b-114">Benefícios do particionamento</span><span class="sxs-lookup"><span data-stu-id="0c48b-114">Benefits of partitioning</span></span>
<span data-ttu-id="0c48b-115">O particionamento pode melhorar o desempenho da consulta e a manutenção de dados.</span><span class="sxs-lookup"><span data-stu-id="0c48b-115">Partitioning can benefit data maintenance and query performance.</span></span>  <span data-ttu-id="0c48b-116">Se ele se beneficia ambos ou apenas uma é dependente de como os dados são carregados e se hello mesma coluna pode ser usada para ambas as finalidades, como particionamento só pode ser feito em uma coluna.</span><span class="sxs-lookup"><span data-stu-id="0c48b-116">Whether it benefits both or just one is dependent on how data is loaded and whether hello same column can be used for both purposes, since partitioning can only be done on one column.</span></span>

### <a name="benefits-tooloads"></a><span data-ttu-id="0c48b-117">Benefícios tooloads</span><span class="sxs-lookup"><span data-stu-id="0c48b-117">Benefits tooloads</span></span>
<span data-ttu-id="0c48b-118">o principal benefício de saudação do particionamento no SQL Data Warehouse é melhorar a eficiência de saudação e desempenho de carregamento de dados através do uso de exclusão de partição, troca e mesclagem.</span><span class="sxs-lookup"><span data-stu-id="0c48b-118">hello primary benefit of partitioning in SQL Data Warehouse is improve hello efficiency and performance of loading data by use of partition deletion, switching and merging.</span></span>  <span data-ttu-id="0c48b-119">Na maioria dos casos, os dados são particionados em uma data a coluna que é ligado sequência toohello quais dados Olá são carregado toohello banco de dados.</span><span class="sxs-lookup"><span data-stu-id="0c48b-119">In most cases data is partitioned on a date column that is closely tied toohello sequence which hello data is loaded toohello database.</span></span>  <span data-ttu-id="0c48b-120">Um dos maiores benefícios de saudação do uso de partições toomaintain dados Olá a redução do log de transações.</span><span class="sxs-lookup"><span data-stu-id="0c48b-120">One of hello greatest benefits of using partitions toomaintain data it hello avoidance of transaction logging.</span></span>  <span data-ttu-id="0c48b-121">Ao simplesmente inserção, atualização ou exclusão de dados pode ser a abordagem mais simples de hello, com um pouco de esforço e pensamento usar particionamento durante o processo de carregamento pode melhorar substancialmente o desempenho.</span><span class="sxs-lookup"><span data-stu-id="0c48b-121">While simply inserting, updating or deleting data can be hello most straightforward approach, with a little thought and effort, using partitioning during your load process can substantially improve performance.</span></span>

<span data-ttu-id="0c48b-122">Alternância de partição pode ser usado tooquickly remover ou substituir uma seção de uma tabela.</span><span class="sxs-lookup"><span data-stu-id="0c48b-122">Partition switching can be used tooquickly remove or replace a section of a table.</span></span>  <span data-ttu-id="0c48b-123">Por exemplo, uma tabela de fatos de vendas pode conter apenas os dados para Olá últimos 36 meses.</span><span class="sxs-lookup"><span data-stu-id="0c48b-123">For example, a sales fact table might contain just data for hello past 36 months.</span></span>  <span data-ttu-id="0c48b-124">No final da saudação de cada mês, hello dados de vendas do mês mais antigo é excluído da tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="0c48b-124">At hello end of every month, hello oldest month of sales data is deleted from hello table.</span></span>  <span data-ttu-id="0c48b-125">Esses dados podem ser excluídos usando um delete instrução toodelete Olá de dados para Olá mês mais antigo.</span><span class="sxs-lookup"><span data-stu-id="0c48b-125">This data could be deleted by using a delete statement toodelete hello data for hello oldest month.</span></span>  <span data-ttu-id="0c48b-126">No entanto, a exclusão de uma grande quantidade de dados linha a linha com uma instrução delete pode levar muito tempo, bem como criar um risco de saudação de grandes transações que poderiam levar um longo tempo toorollback se algo der errado.</span><span class="sxs-lookup"><span data-stu-id="0c48b-126">However, deleting a large amount of data row-by-row with a delete statement can take a very long time, as well as create hello risk of large transactions which could take a long time toorollback if something goes wrong.</span></span>  <span data-ttu-id="0c48b-127">Uma abordagem melhor é drop toosimply partição mais antiga de saudação de dados.</span><span class="sxs-lookup"><span data-stu-id="0c48b-127">A more optimal approach is toosimply drop hello oldest partition of data.</span></span>  <span data-ttu-id="0c48b-128">Onde excluir linhas individuais Olá pode levar horas, a exclusão de uma partição inteira poderá levar segundos.</span><span class="sxs-lookup"><span data-stu-id="0c48b-128">Where deleting hello individual rows could take hours, deleting an entire partition could take seconds.</span></span>

### <a name="benefits-tooqueries"></a><span data-ttu-id="0c48b-129">Benefícios tooqueries</span><span class="sxs-lookup"><span data-stu-id="0c48b-129">Benefits tooqueries</span></span>
<span data-ttu-id="0c48b-130">O particionamento também pode ser usado tooimprove desempenho da consulta.</span><span class="sxs-lookup"><span data-stu-id="0c48b-130">Partitioning can also be used tooimprove query performance.</span></span>  <span data-ttu-id="0c48b-131">Se uma consulta aplica um filtro em uma coluna particionada, isso pode limitar Olá verificação tooonly Olá qualificação partições que podem ser um subconjunto de dados hello, evitando uma verificação completa muito menor.</span><span class="sxs-lookup"><span data-stu-id="0c48b-131">If a query applies a filter on a partitioned column, this can limit hello scan tooonly hello qualifying partitions which may be a much smaller subset of hello data, avoiding a full table scan.</span></span>  <span data-ttu-id="0c48b-132">Com a introdução de saudação de índices columnstore clusterizados, os benefícios de desempenho de eliminação de predicado Olá são benéficos menor, mas em alguns casos pode haver um benefício tooqueries.</span><span class="sxs-lookup"><span data-stu-id="0c48b-132">With hello introduction of clustered columnstore indexes, hello predicate elimination performance benefits are less beneficial, but in some cases there can be a benefit tooqueries.</span></span>  <span data-ttu-id="0c48b-133">Por exemplo, se a tabela de fatos de vendas de saudação é dividida em 36 meses usando o campo de data de venda hello, consultas de filtro na data de venda Olá poderá ignorar pesquisa nas partições que não correspondem ao filtro de saudação.</span><span class="sxs-lookup"><span data-stu-id="0c48b-133">For example, if hello sales fact table is partitioned into 36 months using hello sales date field, then queries that filter on hello sale date can skip searching in partitions that don’t match hello filter.</span></span>

## <a name="partition-sizing-guidance"></a><span data-ttu-id="0c48b-134">Diretrizes de dimensionamento da partição</span><span class="sxs-lookup"><span data-stu-id="0c48b-134">Partition sizing guidance</span></span>
<span data-ttu-id="0c48b-135">Durante o particionamento pode ser usado tooimprove desempenho em alguns cenários, como criar uma tabela com **muitos** partições podem prejudicar o desempenho em algumas circunstâncias.</span><span class="sxs-lookup"><span data-stu-id="0c48b-135">While partitioning can be used tooimprove performance some scenarios, creating a table with **too many** partitions can hurt performance under some circumstances.</span></span>  <span data-ttu-id="0c48b-136">Esses problemas são especialmente verdadeiros para tabelas columnstore clusterizadas.</span><span class="sxs-lookup"><span data-stu-id="0c48b-136">These concerns are especially true for clustered columnstore tables.</span></span>  <span data-ttu-id="0c48b-137">Para particionamento toobe úteis, é importante toounderstand quando toouse particionamento e Olá o número de partições toocreate.</span><span class="sxs-lookup"><span data-stu-id="0c48b-137">For partitioning toobe helpful, it is important toounderstand when toouse partitioning and hello number of partitions toocreate.</span></span>  <span data-ttu-id="0c48b-138">Há é nenhuma regra rígida rápida como toohow várias partições são muitos, depende de seus dados e quantas partições você está carregando toosimultaneously.</span><span class="sxs-lookup"><span data-stu-id="0c48b-138">There is no hard fast rule as toohow many partitions are too many, it depends on your data and how many partitions you are loading toosimultaneously.</span></span>  <span data-ttu-id="0c48b-139">Mas como um regra geral, considere adicionar por 10 too100s de partições, não 1000s.</span><span class="sxs-lookup"><span data-stu-id="0c48b-139">But as a general rule of thumb, think of adding 10s too100s of partitions, not 1000s.</span></span>

<span data-ttu-id="0c48b-140">Ao criar o particionamento em **columnstore clusterizado** tabelas, é importante tooconsider quantas linhas serão levadas em cada partição.</span><span class="sxs-lookup"><span data-stu-id="0c48b-140">When creating partitioning on **clustered columnstore** tables, it is important tooconsider how many rows will land in each partition.</span></span>  <span data-ttu-id="0c48b-141">Para compactação e desempenho ideais de tabelas columnstore clusterizadas, é necessário um mínimo de um milhão de linhas por distribuição, e também é necessário haver partição.</span><span class="sxs-lookup"><span data-stu-id="0c48b-141">For optimal compression and performance of clustered columnstore tables, a minimum of 1 million rows per distribution and partition is needed.</span></span>  <span data-ttu-id="0c48b-142">Antes das partições serem criadas, o SQL Data Warehouse já divide cada tabela em 60 bancos de dados distribuídos.</span><span class="sxs-lookup"><span data-stu-id="0c48b-142">Before partitions are created, SQL Data Warehouse already divides each table into 60 distributed databases.</span></span>  <span data-ttu-id="0c48b-143">Qualquer tabela tooa adicionado particionamento Além disso é toohello distribuições criadas em segundo plano da saudação.</span><span class="sxs-lookup"><span data-stu-id="0c48b-143">Any partitioning added tooa table is in addition toohello distributions created behind hello scenes.</span></span>  <span data-ttu-id="0c48b-144">Usando este exemplo, se tabela de fatos de vendas Olá contidos 36 partições mensais e considerando que o SQL Data Warehouse tem 60 distribuições, então Olá fatos de vendas tabela deve conter 60 milhões de linhas por mês ou 2.1 bilhões de linhas quando todos os meses são populados.</span><span class="sxs-lookup"><span data-stu-id="0c48b-144">Using this example, if hello sales fact table contained 36 monthly partitions, and given that SQL Data Warehouse has 60 distributions, then hello sales fact table should contain 60 million rows per month, or 2.1 billion rows when all months are populated.</span></span>  <span data-ttu-id="0c48b-145">Se uma tabela contém significativamente menos linhas que a saudação recomendada número mínimo de linhas por partição, considere usar menos partições no número do pedido toomake aumento Olá de linhas por partição.</span><span class="sxs-lookup"><span data-stu-id="0c48b-145">If a table contains significantly less rows than hello recommended minimum number of rows per partition, consider using fewer partitions in order toomake increase hello number of rows per partition.</span></span>  <span data-ttu-id="0c48b-146">Consulte também Olá [indexação] [ Index] artigo que inclui as consultas que podem ser executadas na qualidade do SQL Data Warehouse tooassess Olá de índices de columnstore do cluster.</span><span class="sxs-lookup"><span data-stu-id="0c48b-146">Also see hello [Indexing][Index] article which includes queries that can be run on SQL Data Warehouse tooassess hello quality of cluster columnstore indexes.</span></span>

## <a name="syntax-difference-from-sql-server"></a><span data-ttu-id="0c48b-147">Diferença de sintaxe do SQL Server</span><span class="sxs-lookup"><span data-stu-id="0c48b-147">Syntax difference from SQL Server</span></span>
<span data-ttu-id="0c48b-148">O SQL Data Warehouse apresenta uma definição simplificada de partições que é ligeiramente diferente do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0c48b-148">SQL Data Warehouse introduces a simplified definition of partitions which is slightly different from SQL Server.</span></span>  <span data-ttu-id="0c48b-149">As funções e esquemas de particionamento não são usados no SQL Data Warehouse como são no SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0c48b-149">Partitioning functions and schemes are not used in SQL Data Warehouse as they are in SQL Server.</span></span>  <span data-ttu-id="0c48b-150">Em vez disso, você só precisa toodo é identificar pontos de limite de coluna e hello particionados.</span><span class="sxs-lookup"><span data-stu-id="0c48b-150">Instead, all you need toodo is identify partitioned column and hello boundary points.</span></span>  <span data-ttu-id="0c48b-151">Sintaxe de saudação do particionamento pode ser ligeiramente diferente do SQL Server, os conceitos básicos do hello são Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="0c48b-151">While hello syntax of partitioning may be slightly different from SQL Server, hello basic concepts are hello same.</span></span>  <span data-ttu-id="0c48b-152">O SQL Server e o SQL Data Warehouse dão suporte a uma coluna de partição por tabela, que pode ser partição intervalada.</span><span class="sxs-lookup"><span data-stu-id="0c48b-152">SQL Server and SQL Data Warehouse support one partition column per table, which can be ranged partition.</span></span>  <span data-ttu-id="0c48b-153">toolearn mais informações sobre particionamento, consulte [tabelas e índices particionados][Partitioned Tables and Indexes].</span><span class="sxs-lookup"><span data-stu-id="0c48b-153">toolearn more about partitioning, see [Partitioned Tables and Indexes][Partitioned Tables and Indexes].</span></span>

<span data-ttu-id="0c48b-154">Olá abaixo o exemplo de um SQL Data Warehouse particionada [CREATE TABLE] [ CREATE TABLE] instrução, partições de tabela FactInternetSales Olá coluna OrderDateKey de saudação:</span><span class="sxs-lookup"><span data-stu-id="0c48b-154">hello below example of a SQL Data Warehouse partitioned [CREATE TABLE][CREATE TABLE] statement, partitions hello FactInternetSales table on hello OrderDateKey column:</span></span>

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

## <a name="migrating-partitioning-from-sql-server"></a><span data-ttu-id="0c48b-155">Migrando o particionamento do SQL Server</span><span class="sxs-lookup"><span data-stu-id="0c48b-155">Migrating partitioning from SQL Server</span></span>
<span data-ttu-id="0c48b-156">toomigrate do SQL Server de partição simplesmente tooSQL definições do Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="0c48b-156">toomigrate SQL Server partition definitions tooSQL Data Warehouse simply:</span></span>

* <span data-ttu-id="0c48b-157">Eliminar saudação do SQL Server [esquema de partição][partition scheme].</span><span class="sxs-lookup"><span data-stu-id="0c48b-157">Eliminate hello SQL Server [partition scheme][partition scheme].</span></span>
* <span data-ttu-id="0c48b-158">Adicionar Olá [função de partição] [ partition function] tooyour definição criar tabela.</span><span class="sxs-lookup"><span data-stu-id="0c48b-158">Add hello [partition function][partition function] definition tooyour CREATE TABLE.</span></span>

<span data-ttu-id="0c48b-159">Se você estiver migrando uma tabela particionada de uma saudação de instância do SQL Server abaixo SQL pode ajudá-lo a toointerrogate número de saudação de linhas em cada partição.</span><span class="sxs-lookup"><span data-stu-id="0c48b-159">If you are migrating a partitioned table from a SQL Server instance hello below SQL can help you toointerrogate hello number of rows that are in each partition.</span></span>  <span data-ttu-id="0c48b-160">Tenha em mente que, se hello mesma granularidade de particionamento é usada no SQL Data Warehouse, Olá número de linhas por partição diminuirá por um fator de 60.</span><span class="sxs-lookup"><span data-stu-id="0c48b-160">Keep in mind that if hello same partitioning granularity is used on SQL Data Warehouse, hello number of rows per partition will decrease by a factor of 60.</span></span>  

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

## <a name="workload-management"></a><span data-ttu-id="0c48b-161">Gerenciamento de carga de trabalho</span><span class="sxs-lookup"><span data-stu-id="0c48b-161">Workload management</span></span>
<span data-ttu-id="0c48b-162">É um toofactor de consideração parte final na decisão de partição de tabela toohello [gerenciamento de carga de trabalho][workload management].</span><span class="sxs-lookup"><span data-stu-id="0c48b-162">One final piece consideration toofactor in toohello table partition decision is [workload management][workload management].</span></span>  <span data-ttu-id="0c48b-163">Gerenciamento de carga de trabalho no SQL Data Warehouse é principalmente de saudação gerenciamento de memória e simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="0c48b-163">Workload management in SQL Data Warehouse is primarily hello management of memory and concurrency.</span></span>  <span data-ttu-id="0c48b-164">Olá SQL Data Warehouse memória máxima alocada a distribuição tooeach durante a execução da consulta é classes de recursos controlados.</span><span class="sxs-lookup"><span data-stu-id="0c48b-164">In SQL Data Warehouse hello maximum memory allocated tooeach distribution during query execution is governed resource classes.</span></span>  <span data-ttu-id="0c48b-165">Idealmente, suas partições serão dimensionadas em relação aos outros fatores, como Olá necessidades de memória de compilação de índices columnstore clusterizados.</span><span class="sxs-lookup"><span data-stu-id="0c48b-165">Ideally your partitions will be sized in consideration of other factors like hello memory needs of building clustered columnstore indexes.</span></span>  <span data-ttu-id="0c48b-166">Os índices columnstore clusterizados são melhores quando têm mais memória alocada.</span><span class="sxs-lookup"><span data-stu-id="0c48b-166">Clustered columnstore indexes benefit greatly when they are allocated more memory.</span></span>  <span data-ttu-id="0c48b-167">Portanto, você desejará tooensure recriar um índice de partição não fiquem sem de memória.</span><span class="sxs-lookup"><span data-stu-id="0c48b-167">Therefore, you will want tooensure that a partition index rebuild is not starved of memory.</span></span> <span data-ttu-id="0c48b-168">Saudação de aumento da memória disponível tooyour consulta pode ser obtida com a troca de função padrão de saudação, smallrc, tooone de Olá outras funções, como largerc.</span><span class="sxs-lookup"><span data-stu-id="0c48b-168">Increasing hello amount of memory available tooyour query can be achieved by switching from hello default role, smallrc, tooone of hello other roles such as largerc.</span></span>

<span data-ttu-id="0c48b-169">Obter informações sobre alocação de saudação de memória por distribuição estão disponíveis consultando as exibições de gerenciamento dinâmico Olá resource governor.</span><span class="sxs-lookup"><span data-stu-id="0c48b-169">Information on hello allocation of memory per distribution is available by querying hello resource governor dynamic management views.</span></span> <span data-ttu-id="0c48b-170">Na realidade a concessão de memória será menor do que figuras de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="0c48b-170">In reality your memory grant will be less than hello figures below.</span></span> <span data-ttu-id="0c48b-171">No entanto, isso fornece um nível de diretrizes que podem ser usados ao dimensionar suas partições para operações de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="0c48b-171">However, this provides a level of guidance that you can use when sizing your partitions for data management operations.</span></span>  <span data-ttu-id="0c48b-172">Tente tooavoid suas partições além da concessão de memória Olá fornecida pela classe de recurso muito grande de saudação de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="0c48b-172">Try tooavoid sizing your partitions beyond hello memory grant provided by hello extra large resource class.</span></span> <span data-ttu-id="0c48b-173">Se as partições ultrapassem nesta figura você corre o risco de saudação de pressão de memória, que por sua vez, leva compactação ideal tooless.</span><span class="sxs-lookup"><span data-stu-id="0c48b-173">If your partitions grow beyond this figure you run hello risk of memory pressure which in turn leads tooless optimal compression.</span></span>

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

## <a name="partition-switching"></a><span data-ttu-id="0c48b-174">Alternância de partição</span><span class="sxs-lookup"><span data-stu-id="0c48b-174">Partition switching</span></span>
<span data-ttu-id="0c48b-175">O SQL Data Warehouse dá suporte à divisão, mesclagem e comutação de partição.</span><span class="sxs-lookup"><span data-stu-id="0c48b-175">SQL Data Warehouse supports partition splitting, merging, and switching.</span></span> <span data-ttu-id="0c48b-176">Cada uma dessas funções é excuted usando Olá [ALTER TABLE] [ ALTER TABLE] instrução.</span><span class="sxs-lookup"><span data-stu-id="0c48b-176">Each of these functions is excuted using hello [ALTER TABLE][ALTER TABLE] statement.</span></span>

<span data-ttu-id="0c48b-177">partições de tooswitch entre duas tabelas, que você deve garantir que partições Olá alinham em seus respectivos limites e se as definições de tabela Olá correspondem.</span><span class="sxs-lookup"><span data-stu-id="0c48b-177">tooswitch partitions between two tables you must ensure that hello partitions align on their respective boundaries and that hello table definitions match.</span></span> <span data-ttu-id="0c48b-178">Como restrições de verificação não estão disponíveis tooenforce intervalo de saudação de valores em uma tabela de origem de saudação da tabela deve conter Olá mesmo limites de partição como tabela de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="0c48b-178">As check constraints are not available tooenforce hello range of values in a table hello source table must contain hello same partition boundaries as hello target table.</span></span> <span data-ttu-id="0c48b-179">Se não for o caso de Olá, alternância de partição Olá falhará como Olá metadados da partição não serão sincronizados.</span><span class="sxs-lookup"><span data-stu-id="0c48b-179">If this is not hello case, then hello partition switch will fail as hello partition metadata will not be synchronized.</span></span>

### <a name="how-toosplit-a-partition-that-contains-data"></a><span data-ttu-id="0c48b-180">Como toosplit uma partição que contém dados</span><span class="sxs-lookup"><span data-stu-id="0c48b-180">How toosplit a partition that contains data</span></span>
<span data-ttu-id="0c48b-181">Olá, mais eficiente método toosplit uma partição que já contém dados é toouse um `CTAS` instrução.</span><span class="sxs-lookup"><span data-stu-id="0c48b-181">hello most efficient method toosplit a partition that already contains data is toouse a `CTAS` statement.</span></span> <span data-ttu-id="0c48b-182">Se a tabela particionada Olá é uma columnstore clusterizada, em seguida, partição de tabela Olá deve estar vazia antes ela pode ser dividida.</span><span class="sxs-lookup"><span data-stu-id="0c48b-182">If hello partitioned table is a clustered columnstore then hello table partition must be empty before it can be split.</span></span>

<span data-ttu-id="0c48b-183">Veja abaixo um exemplo de tabela columnstore particionada que contém uma linha em cada partição:</span><span class="sxs-lookup"><span data-stu-id="0c48b-183">Below is a sample partitioned columnstore table containing one row in each partition:</span></span>

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
> <span data-ttu-id="0c48b-184">Criando objeto de estatística hello, garantimos que metadados de tabela são mais preciso.</span><span class="sxs-lookup"><span data-stu-id="0c48b-184">By Creating hello statistic object, we ensure that table metadata is more accurate.</span></span> <span data-ttu-id="0c48b-185">Se omitirmos a criação de estatísticas, o SQL Data Warehouse usará os valores padrão.</span><span class="sxs-lookup"><span data-stu-id="0c48b-185">If we omit creating statistics, then SQL Data Warehouse will use default values.</span></span> <span data-ttu-id="0c48b-186">Para obter detalhes sobre as estatísticas examine [estatísticas][statistics].</span><span class="sxs-lookup"><span data-stu-id="0c48b-186">For details on statistics please review [statistics][statistics].</span></span>
> 
> 

<span data-ttu-id="0c48b-187">Podemos pode fazer consultas para contagem de linhas de saudação usando Olá `sys.partitions` exibição do catálogo:</span><span class="sxs-lookup"><span data-stu-id="0c48b-187">We can then query for hello row count using hello `sys.partitions` catalog view:</span></span>

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

<span data-ttu-id="0c48b-188">Se tentarmos toosplit nesta tabela, obtemos um erro:</span><span class="sxs-lookup"><span data-stu-id="0c48b-188">If we try toosplit this table, we will get an error:</span></span>

```sql
ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="0c48b-189">Msg 35346, nível 15, estado 1, linha 44 DIVIDIDA cláusula da instrução ALTER PARTITION falhou porque Olá partição não está vazia.</span><span class="sxs-lookup"><span data-stu-id="0c48b-189">Msg 35346, Level 15, State 1, Line 44 SPLIT clause of ALTER PARTITION statement failed because hello partition is not empty.</span></span>  <span data-ttu-id="0c48b-190">Somente partições vazias podem ser divididas quando existe um índice na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="0c48b-190">Only empty partitions can be split in when a columnstore index exists on hello table.</span></span> <span data-ttu-id="0c48b-191">Considere desabilitar o índice de columnstore Olá antes de emitir a instrução ALTER PARTITION de saudação e a recompilação de índice de columnstore Olá depois de ALTER PARTITION estar concluído.</span><span class="sxs-lookup"><span data-stu-id="0c48b-191">Consider disabling hello columnstore index before issuing hello ALTER PARTITION statement, then rebuilding hello columnstore index after ALTER PARTITION is complete.</span></span>

<span data-ttu-id="0c48b-192">No entanto, podemos usar `CTAS` toocreate um novo toohold de tabela nossos dados.</span><span class="sxs-lookup"><span data-stu-id="0c48b-192">However, we can use `CTAS` toocreate a new table toohold our data.</span></span>

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

<span data-ttu-id="0c48b-193">Como os limites de partição Olá são alinhados um comutador é permitido.</span><span class="sxs-lookup"><span data-stu-id="0c48b-193">As hello partition boundaries are aligned a switch is permitted.</span></span> <span data-ttu-id="0c48b-194">Isso deixará a tabela de origem Olá com uma partição vazia que podemos subsequentemente dividir.</span><span class="sxs-lookup"><span data-stu-id="0c48b-194">This will leave hello source table with an empty partition that we can subsequently split.</span></span>

```sql
ALTER TABLE FactInternetSales SWITCH PARTITION 2 too FactInternetSales_20000101 PARTITION 2;

ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="0c48b-195">Tudo o que resta toodo é tooalign toohello nossos dados de partição novos limites usando `CTAS` e alternar nossos dados de volta na tabela principal toohello</span><span class="sxs-lookup"><span data-stu-id="0c48b-195">All that is left toodo is tooalign our data toohello new partition boundaries using `CTAS` and switch our data back in toohello main table</span></span>

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

<span data-ttu-id="0c48b-196">Depois de concluir a movimentação de saudação de dados de saudação é estatísticas de saudação de toorefresh uma boa ideia eles refletem com precisão em tooensure de tabela de destino Olá distribuição de nova Olá dos dados de saudação em suas respectivas partições:</span><span class="sxs-lookup"><span data-stu-id="0c48b-196">Once you have completed hello movement of hello data it is a good idea toorefresh hello statistics on hello target table tooensure they accurately reflect hello new distribution of hello data in their respective partitions:</span></span>

```sql
UPDATE STATISTICS [dbo].[FactInternetSales];
```

### <a name="table-partitioning-source-control"></a><span data-ttu-id="0c48b-197">Controle da origem do particionamento da tabela</span><span class="sxs-lookup"><span data-stu-id="0c48b-197">Table partitioning source control</span></span>
<span data-ttu-id="0c48b-198">tooavoid sua definição da tabela de **enferrujado** em seu sistema de controle de origem, você pode desejar Olá tooconsider abordagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="0c48b-198">tooavoid your table definition from **rusting** in your source control system you may want tooconsider hello following approach:</span></span>

1. <span data-ttu-id="0c48b-199">Criar tabela hello como uma tabela particionada, mas sem valores de partição</span><span class="sxs-lookup"><span data-stu-id="0c48b-199">Create hello table as a partitioned table but with no partition values</span></span>

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

1. <span data-ttu-id="0c48b-200">`SPLIT`tabela Hello como parte do processo de implantação de saudação:</span><span class="sxs-lookup"><span data-stu-id="0c48b-200">`SPLIT` hello table as part of hello deployment process:</span></span>

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

<span data-ttu-id="0c48b-201">Com hello essa abordagem código no controle de origem permanece estático e valores de limite de particionamento de saudação são permitidos toobe dinâmico; Desenvolvendo com warehouse Olá ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="0c48b-201">With this approach hello code in source control remains static and hello partitioning boundary values are allowed toobe dynamic; evolving with hello warehouse over time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c48b-202">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0c48b-202">Next steps</span></span>
<span data-ttu-id="0c48b-203">toolearn mais, consulte os artigos de saudação em [visão geral da tabela][Overview], [tipos de dados de tabela][Data Types], [distribuir uma tabela] [ Distribute], [Indexando uma tabela][Index], [manter estatísticas de tabela] [ Statistics] e [ Tabelas temporárias][Temporary].</span><span class="sxs-lookup"><span data-stu-id="0c48b-203">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="0c48b-204">Para saber mais sobre as práticas recomendadas, consulte [Práticas Recomendadas do SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="0c48b-204">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
