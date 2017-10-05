---
title: Particionando tabelas no SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: 3edfd34d368228be32afef48688739639a3b03ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="partitioning-tables-in-sql-data-warehouse"></a><span data-ttu-id="7a78e-103">Particionando tabelas no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="7a78e-103">Partitioning tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="7a78e-104">[Visão geral][Overview]</span><span class="sxs-lookup"><span data-stu-id="7a78e-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="7a78e-105">[Tipos de Dados][Data Types]</span><span class="sxs-lookup"><span data-stu-id="7a78e-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="7a78e-106">[Distribuir][Distribute]</span><span class="sxs-lookup"><span data-stu-id="7a78e-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="7a78e-107">[Índice][Index]</span><span class="sxs-lookup"><span data-stu-id="7a78e-107">[Index][Index]</span></span>
> * <span data-ttu-id="7a78e-108">[Partição][Partition]</span><span class="sxs-lookup"><span data-stu-id="7a78e-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="7a78e-109">[Estatísticas][Statistics]</span><span class="sxs-lookup"><span data-stu-id="7a78e-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="7a78e-110">[Temporário][Temporary]</span><span class="sxs-lookup"><span data-stu-id="7a78e-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="7a78e-111">O particionamento tem suporte em todos os tipos de tabela do SQL Data Warehouse, incluindo columnstore clusterizado, índice clusterizado e heap.</span><span class="sxs-lookup"><span data-stu-id="7a78e-111">Partitioning is supported on all SQL Data Warehouse table types; including clustered columnstore, clustered index, and heap.</span></span>  <span data-ttu-id="7a78e-112">O particionamento também tem suporte em todos os tipos de distribuição, incluindo hash ou round robin.</span><span class="sxs-lookup"><span data-stu-id="7a78e-112">Partitioning is also supported on all distribution types, including both hash or round robin distributed.</span></span>  <span data-ttu-id="7a78e-113">O particionamento permite dividir seus dados em grupos menores de dados e, na maioria dos casos, o particionamento é feito em uma coluna de data.</span><span class="sxs-lookup"><span data-stu-id="7a78e-113">Partitioning enables you to divide your data into smaller groups of data and in most cases, partitioning is done on a date column.</span></span>

## <a name="benefits-of-partitioning"></a><span data-ttu-id="7a78e-114">Benefícios do particionamento</span><span class="sxs-lookup"><span data-stu-id="7a78e-114">Benefits of partitioning</span></span>
<span data-ttu-id="7a78e-115">O particionamento pode melhorar o desempenho da consulta e a manutenção de dados.</span><span class="sxs-lookup"><span data-stu-id="7a78e-115">Partitioning can benefit data maintenance and query performance.</span></span>  <span data-ttu-id="7a78e-116">Se ele beneficia ambos ou apenas um depende de como os dados são carregados e se a mesma coluna pode ser usada para ambas as finalidades, já que o particionamento só pode ser feito em uma coluna.</span><span class="sxs-lookup"><span data-stu-id="7a78e-116">Whether it benefits both or just one is dependent on how data is loaded and whether the same column can be used for both purposes, since partitioning can only be done on one column.</span></span>

### <a name="benefits-to-loads"></a><span data-ttu-id="7a78e-117">Benefícios para cargas</span><span class="sxs-lookup"><span data-stu-id="7a78e-117">Benefits to loads</span></span>
<span data-ttu-id="7a78e-118">A principal vantagem do particionamento no SQL Data Warehouse é melhorar a eficiência e o desempenho de carregamento de dados pelo uso de exclusão, troca e mesclagem de partição.</span><span class="sxs-lookup"><span data-stu-id="7a78e-118">The primary benefit of partitioning in SQL Data Warehouse is improve the efficiency and performance of loading data by use of partition deletion, switching and merging.</span></span>  <span data-ttu-id="7a78e-119">Na maioria dos casos, os dados são particionados em uma coluna de data que está intimamente ligada à sequência em que os dados são carregados no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="7a78e-119">In most cases data is partitioned on a date column that is closely tied to the sequence which the data is loaded to the database.</span></span>  <span data-ttu-id="7a78e-120">Uma das maiores vantagens de usar partições para manter dados é evitar o registro de transações em log.</span><span class="sxs-lookup"><span data-stu-id="7a78e-120">One of the greatest benefits of using partitions to maintain data it the avoidance of transaction logging.</span></span>  <span data-ttu-id="7a78e-121">Embora a simples inserção, atualização ou exclusão de dados possa ser a abordagem mais simples, com um pouco de empenho, o uso de particionamento durante o processo de carregamento pode melhorar consideravelmente o desempenho.</span><span class="sxs-lookup"><span data-stu-id="7a78e-121">While simply inserting, updating or deleting data can be the most straightforward approach, with a little thought and effort, using partitioning during your load process can substantially improve performance.</span></span>

<span data-ttu-id="7a78e-122">A alternância de partição pode ser usada para remover ou substituir uma seção de uma tabela rapidamente.</span><span class="sxs-lookup"><span data-stu-id="7a78e-122">Partition switching can be used to quickly remove or replace a section of a table.</span></span>  <span data-ttu-id="7a78e-123">Por exemplo, uma tabela de fatos de vendas pode conter apenas dados dos últimos 36 meses.</span><span class="sxs-lookup"><span data-stu-id="7a78e-123">For example, a sales fact table might contain just data for the past 36 months.</span></span>  <span data-ttu-id="7a78e-124">No final de cada mês, o mês de dados de vendas mais antigo é excluído da tabela.</span><span class="sxs-lookup"><span data-stu-id="7a78e-124">At the end of every month, the oldest month of sales data is deleted from the table.</span></span>  <span data-ttu-id="7a78e-125">Esses dados poderiam ser excluídos usando uma instrução delete para excluir os dados do mês mais antigo.</span><span class="sxs-lookup"><span data-stu-id="7a78e-125">This data could be deleted by using a delete statement to delete the data for the oldest month.</span></span>  <span data-ttu-id="7a78e-126">No entanto, a exclusão de uma grande quantidade de dados linha a linha com uma instrução delete pode levar muito tempo e criar o risco de transações grandes, o que poderia levar muito tempo para reverter se algo desse errado.</span><span class="sxs-lookup"><span data-stu-id="7a78e-126">However, deleting a large amount of data row-by-row with a delete statement can take a very long time, as well as create the risk of large transactions which could take a long time to rollback if something goes wrong.</span></span>  <span data-ttu-id="7a78e-127">Uma abordagem melhor é simplesmente remover a partição mais antiga dos dados.</span><span class="sxs-lookup"><span data-stu-id="7a78e-127">A more optimal approach is to simply drop the oldest partition of data.</span></span>  <span data-ttu-id="7a78e-128">A exclusão de linhas individuais pode levar horas. A exclusão de uma partição inteira pode demorar segundos.</span><span class="sxs-lookup"><span data-stu-id="7a78e-128">Where deleting the individual rows could take hours, deleting an entire partition could take seconds.</span></span>

### <a name="benefits-to-queries"></a><span data-ttu-id="7a78e-129">Vantagens para consultas</span><span class="sxs-lookup"><span data-stu-id="7a78e-129">Benefits to queries</span></span>
<span data-ttu-id="7a78e-130">O particionamento também pode ser usado para melhorar o desempenho da consulta.</span><span class="sxs-lookup"><span data-stu-id="7a78e-130">Partitioning can also be used to improve query performance.</span></span>  <span data-ttu-id="7a78e-131">Se uma consulta aplica um filtro em uma coluna particionada, isso pode limitar a varredura apenas às partições qualificadas que podem ser um subconjunto muito menor de dados, impedindo uma verificação completa.</span><span class="sxs-lookup"><span data-stu-id="7a78e-131">If a query applies a filter on a partitioned column, this can limit the scan to only the qualifying partitions which may be a much smaller subset of the data, avoiding a full table scan.</span></span>  <span data-ttu-id="7a78e-132">Com a introdução de índices columnstore clusterizados, os benefícios de desempenho de eliminação de predicado são menores, mas em alguns casos pode haver vantagem para as consultas.</span><span class="sxs-lookup"><span data-stu-id="7a78e-132">With the introduction of clustered columnstore indexes, the predicate elimination performance benefits are less beneficial, but in some cases there can be a benefit to queries.</span></span>  <span data-ttu-id="7a78e-133">Por exemplo, se a tabela de fatos de vendas for particionada em 36 meses usando o campo de data das vendas, as consultas que forem filtradas pela data da venda podem pular a pesquisa de partições que não correspondam ao filtro.</span><span class="sxs-lookup"><span data-stu-id="7a78e-133">For example, if the sales fact table is partitioned into 36 months using the sales date field, then queries that filter on the sale date can skip searching in partitions that don’t match the filter.</span></span>

## <a name="partition-sizing-guidance"></a><span data-ttu-id="7a78e-134">Diretrizes de dimensionamento da partição</span><span class="sxs-lookup"><span data-stu-id="7a78e-134">Partition sizing guidance</span></span>
<span data-ttu-id="7a78e-135">Embora o particionamento possa ser usado para melhorar o desempenho de alguns cenários, a criação de uma tabela com **muitas** partições pode prejudicar o desempenho em algumas circunstâncias.</span><span class="sxs-lookup"><span data-stu-id="7a78e-135">While partitioning can be used to improve performance some scenarios, creating a table with **too many** partitions can hurt performance under some circumstances.</span></span>  <span data-ttu-id="7a78e-136">Esses problemas são especialmente verdadeiros para tabelas columnstore clusterizadas.</span><span class="sxs-lookup"><span data-stu-id="7a78e-136">These concerns are especially true for clustered columnstore tables.</span></span>  <span data-ttu-id="7a78e-137">Para que o particionamento seja útil, é importante entender quando usar o particionamento e o número de partições a serem criadas.</span><span class="sxs-lookup"><span data-stu-id="7a78e-137">For partitioning to be helpful, it is important to understand when to use partitioning and the number of partitions to create.</span></span>  <span data-ttu-id="7a78e-138">Não há nenhuma regra rígida sobre o que é o excesso de partições. Isso depende de seus dados e de quantas partições você está carregando simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="7a78e-138">There is no hard fast rule as to how many partitions are too many, it depends on your data and how many partitions you are loading to simultaneously.</span></span>  <span data-ttu-id="7a78e-139">Mas, como regra geral, considere adicionar dezenas a centenas de partições, não milhares.</span><span class="sxs-lookup"><span data-stu-id="7a78e-139">But as a general rule of thumb, think of adding 10s to 100s of partitions, not 1000s.</span></span>

<span data-ttu-id="7a78e-140">Ao criar o particionamento em tabelas **columnstore clusterizadas** , é importante considerar o número de linhas que vão para cada partição.</span><span class="sxs-lookup"><span data-stu-id="7a78e-140">When creating partitioning on **clustered columnstore** tables, it is important to consider how many rows will land in each partition.</span></span>  <span data-ttu-id="7a78e-141">Para compactação e desempenho ideais de tabelas columnstore clusterizadas, é necessário um mínimo de um milhão de linhas por distribuição, e também é necessário haver partição.</span><span class="sxs-lookup"><span data-stu-id="7a78e-141">For optimal compression and performance of clustered columnstore tables, a minimum of 1 million rows per distribution and partition is needed.</span></span>  <span data-ttu-id="7a78e-142">Antes das partições serem criadas, o SQL Data Warehouse já divide cada tabela em 60 bancos de dados distribuídos.</span><span class="sxs-lookup"><span data-stu-id="7a78e-142">Before partitions are created, SQL Data Warehouse already divides each table into 60 distributed databases.</span></span>  <span data-ttu-id="7a78e-143">O particionamento adicionado a uma tabela é além das distribuições criadas nos bastidores.</span><span class="sxs-lookup"><span data-stu-id="7a78e-143">Any partitioning added to a table is in addition to the distributions created behind the scenes.</span></span>  <span data-ttu-id="7a78e-144">Usando esse exemplo, se a tabela de fatos de vendas contiver 36 partições mensais, e uma vez que o SQL Data Warehouse tem 60 distribuições, a tabela de fatos de vendas deverá conter 60 milhões de linhas por mês, ou 2.1 bilhões de linhas quando todos os meses forem populados.</span><span class="sxs-lookup"><span data-stu-id="7a78e-144">Using this example, if the sales fact table contained 36 monthly partitions, and given that SQL Data Warehouse has 60 distributions, then the sales fact table should contain 60 million rows per month, or 2.1 billion rows when all months are populated.</span></span>  <span data-ttu-id="7a78e-145">Se uma tabela possuir significativamente menos linhas do que o mínimo recomendado, considere usar menos partições para aumentar o número de linhas por partição.</span><span class="sxs-lookup"><span data-stu-id="7a78e-145">If a table contains significantly less rows than the recommended minimum number of rows per partition, consider using fewer partitions in order to make increase the number of rows per partition.</span></span>  <span data-ttu-id="7a78e-146">Confira também o artigo [Indexação][Index], que inclui consultas que podem ser executadas no SQL Data Warehouse para avaliar a qualidade dos índices columnstore do cluster.</span><span class="sxs-lookup"><span data-stu-id="7a78e-146">Also see the [Indexing][Index] article which includes queries that can be run on SQL Data Warehouse to assess the quality of cluster columnstore indexes.</span></span>

## <a name="syntax-difference-from-sql-server"></a><span data-ttu-id="7a78e-147">Diferença de sintaxe do SQL Server</span><span class="sxs-lookup"><span data-stu-id="7a78e-147">Syntax difference from SQL Server</span></span>
<span data-ttu-id="7a78e-148">O SQL Data Warehouse apresenta uma definição simplificada de partições que é ligeiramente diferente do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7a78e-148">SQL Data Warehouse introduces a simplified definition of partitions which is slightly different from SQL Server.</span></span>  <span data-ttu-id="7a78e-149">As funções e esquemas de particionamento não são usados no SQL Data Warehouse como são no SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7a78e-149">Partitioning functions and schemes are not used in SQL Data Warehouse as they are in SQL Server.</span></span>  <span data-ttu-id="7a78e-150">Em vez disso,tudo o que você precisa fazer é identificar a coluna particionada e os pontos delimitadores.</span><span class="sxs-lookup"><span data-stu-id="7a78e-150">Instead, all you need to do is identify partitioned column and the boundary points.</span></span>  <span data-ttu-id="7a78e-151">Embora a sintaxe de particionamento possa ser ligeiramente diferente do SQL Server, os conceitos básicos são os mesmos.</span><span class="sxs-lookup"><span data-stu-id="7a78e-151">While the syntax of partitioning may be slightly different from SQL Server, the basic concepts are the same.</span></span>  <span data-ttu-id="7a78e-152">O SQL Server e o SQL Data Warehouse dão suporte a uma coluna de partição por tabela, que pode ser partição intervalada.</span><span class="sxs-lookup"><span data-stu-id="7a78e-152">SQL Server and SQL Data Warehouse support one partition column per table, which can be ranged partition.</span></span>  <span data-ttu-id="7a78e-153">Para saber mais sobre particionamento, confira [Tabelas e índices particionados][Partitioned Tables and Indexes].</span><span class="sxs-lookup"><span data-stu-id="7a78e-153">To learn more about partitioning, see [Partitioned Tables and Indexes][Partitioned Tables and Indexes].</span></span>

<span data-ttu-id="7a78e-154">O exemplo de uma instrução particionada [CREATE TABLE][CREATE TABLE] do SQL Data Warehouse particiona a tabela FactInternetSales na coluna OrderDateKey:</span><span class="sxs-lookup"><span data-stu-id="7a78e-154">The below example of a SQL Data Warehouse partitioned [CREATE TABLE][CREATE TABLE] statement, partitions the FactInternetSales table on the OrderDateKey column:</span></span>

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

## <a name="migrating-partitioning-from-sql-server"></a><span data-ttu-id="7a78e-155">Migrando o particionamento do SQL Server</span><span class="sxs-lookup"><span data-stu-id="7a78e-155">Migrating partitioning from SQL Server</span></span>
<span data-ttu-id="7a78e-156">Para migrar definições de partição do SQL Server para o SQL Data Warehouse, basta:</span><span class="sxs-lookup"><span data-stu-id="7a78e-156">To migrate SQL Server partition definitions to SQL Data Warehouse simply:</span></span>

* <span data-ttu-id="7a78e-157">Elimine o [esquema de partição][partition scheme] do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7a78e-157">Eliminate the SQL Server [partition scheme][partition scheme].</span></span>
* <span data-ttu-id="7a78e-158">Adicione a definição [função de partição][partition function] para CREATE TABLE.</span><span class="sxs-lookup"><span data-stu-id="7a78e-158">Add the [partition function][partition function] definition to your CREATE TABLE.</span></span>

<span data-ttu-id="7a78e-159">Se você estiver migrando uma tabela particionada em uma instância do SQL Server, o SQL abaixo poderá ajudá-lo a investigar o número de linhas em cada partição.</span><span class="sxs-lookup"><span data-stu-id="7a78e-159">If you are migrating a partitioned table from a SQL Server instance the below SQL can help you to interrogate the number of rows that are in each partition.</span></span>  <span data-ttu-id="7a78e-160">Tenha em mente que, se a mesma granularidade de particionamento é usada no SQL Data Warehouse, o número de linhas por partição é reduzido por 60.</span><span class="sxs-lookup"><span data-stu-id="7a78e-160">Keep in mind that if the same partitioning granularity is used on SQL Data Warehouse, the number of rows per partition will decrease by a factor of 60.</span></span>  

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

## <a name="workload-management"></a><span data-ttu-id="7a78e-161">Gerenciamento de carga de trabalho</span><span class="sxs-lookup"><span data-stu-id="7a78e-161">Workload management</span></span>
<span data-ttu-id="7a78e-162">Uma questão final a considerar ao tomar a decisão sobre a partição de tabela é o [gerenciamento de carga de trabalho][workload management].</span><span class="sxs-lookup"><span data-stu-id="7a78e-162">One final piece consideration to factor in to the table partition decision is [workload management][workload management].</span></span>  <span data-ttu-id="7a78e-163">O gerenciamento de carga de trabalho no SQL Data Warehouse é basicamente o gerenciamento de memória e simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="7a78e-163">Workload management in SQL Data Warehouse is primarily the management of memory and concurrency.</span></span>  <span data-ttu-id="7a78e-164">No SQL Data Warehouse, a memória máxima alocada para cada distribuição durante a execução da consulta é regida pelas classes de recurso.</span><span class="sxs-lookup"><span data-stu-id="7a78e-164">In SQL Data Warehouse the maximum memory allocated to each distribution during query execution is governed resource classes.</span></span>  <span data-ttu-id="7a78e-165">O ideal é que suas partições sejam dimensionadas em relação a outros fatores, como as necessidades de memória da criação de índices columnstore clusterizados.</span><span class="sxs-lookup"><span data-stu-id="7a78e-165">Ideally your partitions will be sized in consideration of other factors like the memory needs of building clustered columnstore indexes.</span></span>  <span data-ttu-id="7a78e-166">Os índices columnstore clusterizados são melhores quando têm mais memória alocada.</span><span class="sxs-lookup"><span data-stu-id="7a78e-166">Clustered columnstore indexes benefit greatly when they are allocated more memory.</span></span>  <span data-ttu-id="7a78e-167">Portanto, você desejará garantir que uma recompilação do índice da partição não fique sem memória.</span><span class="sxs-lookup"><span data-stu-id="7a78e-167">Therefore, you will want to ensure that a partition index rebuild is not starved of memory.</span></span> <span data-ttu-id="7a78e-168">O aumento da quantidade de memória disponível para a sua consulta pode ser obtido ao alternar da função padrão, smallrc, para uma das outras funções, como largerc.</span><span class="sxs-lookup"><span data-stu-id="7a78e-168">Increasing the amount of memory available to your query can be achieved by switching from the default role, smallrc, to one of the other roles such as largerc.</span></span>

<span data-ttu-id="7a78e-169">Informações sobre a alocação de memória por distribuição estão disponíveis consultando as exibições de gerenciamento dinâmico do administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="7a78e-169">Information on the allocation of memory per distribution is available by querying the resource governor dynamic management views.</span></span> <span data-ttu-id="7a78e-170">Na realidade, a concessão de memória será menor do que apresentada abaixo.</span><span class="sxs-lookup"><span data-stu-id="7a78e-170">In reality your memory grant will be less than the figures below.</span></span> <span data-ttu-id="7a78e-171">No entanto, isso fornece um nível de diretrizes que podem ser usados ao dimensionar suas partições para operações de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="7a78e-171">However, this provides a level of guidance that you can use when sizing your partitions for data management operations.</span></span>  <span data-ttu-id="7a78e-172">Tente evitar o dimensionamento das partições além da concessão de memória fornecida pela classe de recurso muito grande.</span><span class="sxs-lookup"><span data-stu-id="7a78e-172">Try to avoid sizing your partitions beyond the memory grant provided by the extra large resource class.</span></span> <span data-ttu-id="7a78e-173">Se as partições ultrapassarem este valor, você corre o risco de pressão de memória, que por sua vez, leva à menor compactação ideal.</span><span class="sxs-lookup"><span data-stu-id="7a78e-173">If your partitions grow beyond this figure you run the risk of memory pressure which in turn leads to less optimal compression.</span></span>

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

## <a name="partition-switching"></a><span data-ttu-id="7a78e-174">Alternância de partição</span><span class="sxs-lookup"><span data-stu-id="7a78e-174">Partition switching</span></span>
<span data-ttu-id="7a78e-175">O SQL Data Warehouse dá suporte à divisão, mesclagem e comutação de partição.</span><span class="sxs-lookup"><span data-stu-id="7a78e-175">SQL Data Warehouse supports partition splitting, merging, and switching.</span></span> <span data-ttu-id="7a78e-176">Todas essas funções são executadas usando a instrução [ALTER TABLE][ALTER TABLE].</span><span class="sxs-lookup"><span data-stu-id="7a78e-176">Each of these functions is excuted using the [ALTER TABLE][ALTER TABLE] statement.</span></span>

<span data-ttu-id="7a78e-177">Para alternar as partições entre duas tabelas, você deve garantir que as partições alinhem em seus respectivos limites e que correspondam as definições de tabela.</span><span class="sxs-lookup"><span data-stu-id="7a78e-177">To switch partitions between two tables you must ensure that the partitions align on their respective boundaries and that the table definitions match.</span></span> <span data-ttu-id="7a78e-178">Como restrições de verificação não estão disponíveis para impor o intervalo de valores em uma tabela, a tabela de origem deve conter os mesmos limites de partição da tabela de destino.</span><span class="sxs-lookup"><span data-stu-id="7a78e-178">As check constraints are not available to enforce the range of values in a table the source table must contain the same partition boundaries as the target table.</span></span> <span data-ttu-id="7a78e-179">Se este não for o caso, a alternância de partição falhará, já que os metadados da partição não serão sincronizados.</span><span class="sxs-lookup"><span data-stu-id="7a78e-179">If this is not the case, then the partition switch will fail as the partition metadata will not be synchronized.</span></span>

### <a name="how-to-split-a-partition-that-contains-data"></a><span data-ttu-id="7a78e-180">Como dividir uma partição que contém dados</span><span class="sxs-lookup"><span data-stu-id="7a78e-180">How to split a partition that contains data</span></span>
<span data-ttu-id="7a78e-181">O método mais eficiente para dividir uma partição que já contém dados é usar um `CTAS` instrução.</span><span class="sxs-lookup"><span data-stu-id="7a78e-181">The most efficient method to split a partition that already contains data is to use a `CTAS` statement.</span></span> <span data-ttu-id="7a78e-182">Se a tabela particionada é uma columnstore clusterizada, então a partição de tabela deve estar vazia antes que ela possa ser dividida.</span><span class="sxs-lookup"><span data-stu-id="7a78e-182">If the partitioned table is a clustered columnstore then the table partition must be empty before it can be split.</span></span>

<span data-ttu-id="7a78e-183">Veja abaixo um exemplo de tabela columnstore particionada que contém uma linha em cada partição:</span><span class="sxs-lookup"><span data-stu-id="7a78e-183">Below is a sample partitioned columnstore table containing one row in each partition:</span></span>

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
> <span data-ttu-id="7a78e-184">Criando o objeto de estatística garantimos que os metadados de tabela sejam mais precisos.</span><span class="sxs-lookup"><span data-stu-id="7a78e-184">By Creating the statistic object, we ensure that table metadata is more accurate.</span></span> <span data-ttu-id="7a78e-185">Se omitirmos a criação de estatísticas, o SQL Data Warehouse usará os valores padrão.</span><span class="sxs-lookup"><span data-stu-id="7a78e-185">If we omit creating statistics, then SQL Data Warehouse will use default values.</span></span> <span data-ttu-id="7a78e-186">Para obter detalhes sobre as estatísticas examine [estatísticas][statistics].</span><span class="sxs-lookup"><span data-stu-id="7a78e-186">For details on statistics please review [statistics][statistics].</span></span>
> 
> 

<span data-ttu-id="7a78e-187">Em seguida, podemos consultar a contagem de linhas usando a exibição do catálogo `sys.partitions` :</span><span class="sxs-lookup"><span data-stu-id="7a78e-187">We can then query for the row count using the `sys.partitions` catalog view:</span></span>

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

<span data-ttu-id="7a78e-188">Se tentarmos dividir essa tabela, obteremos um erro:</span><span class="sxs-lookup"><span data-stu-id="7a78e-188">If we try to split this table, we will get an error:</span></span>

```sql
ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="7a78e-189">Msg 35346, Nível 15, Estado 1, linha 44 da cláusula SPLIT da instrução ALTER PARTITION falhou porque a partição não está vazia.</span><span class="sxs-lookup"><span data-stu-id="7a78e-189">Msg 35346, Level 15, State 1, Line 44 SPLIT clause of ALTER PARTITION statement failed because the partition is not empty.</span></span>  <span data-ttu-id="7a78e-190">Somente partições vazias podem ser divididas quando existe um índice columnstore na tabela.</span><span class="sxs-lookup"><span data-stu-id="7a78e-190">Only empty partitions can be split in when a columnstore index exists on the table.</span></span> <span data-ttu-id="7a78e-191">Considere desabilitar o índice columnstore antes de emitir a instrução ALTER PARTITION, e então recriar o índice columnstore após a instrução ALTER PARTITION estar concluída.</span><span class="sxs-lookup"><span data-stu-id="7a78e-191">Consider disabling the columnstore index before issuing the ALTER PARTITION statement, then rebuilding the columnstore index after ALTER PARTITION is complete.</span></span>

<span data-ttu-id="7a78e-192">No entanto, podemos usar `CTAS` para criar uma nova tabela para manter nossos dados.</span><span class="sxs-lookup"><span data-stu-id="7a78e-192">However, we can use `CTAS` to create a new table to hold our data.</span></span>

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

<span data-ttu-id="7a78e-193">Como os limites de partição estão alinhados, uma alternância é permitida.</span><span class="sxs-lookup"><span data-stu-id="7a78e-193">As the partition boundaries are aligned a switch is permitted.</span></span> <span data-ttu-id="7a78e-194">Isso deixará a tabela de origem com uma partição vazia que podemos dividir posteriormente.</span><span class="sxs-lookup"><span data-stu-id="7a78e-194">This will leave the source table with an empty partition that we can subsequently split.</span></span>

```sql
ALTER TABLE FactInternetSales SWITCH PARTITION 2 TO  FactInternetSales_20000101 PARTITION 2;

ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="7a78e-195">Tudo o que resta a fazer é alinhar os dados para os novos limites de partição usando `CTAS` e alternar nossos dados de volta para a tabela principal</span><span class="sxs-lookup"><span data-stu-id="7a78e-195">All that is left to do is to align our data to the new partition boundaries using `CTAS` and switch our data back in to the main table</span></span>

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

ALTER TABLE dbo.FactInternetSales_20000101_20010101 SWITCH PARTITION 2 TO dbo.FactInternetSales PARTITION 2;
```

<span data-ttu-id="7a78e-196">Depois de ter concluído a movimentação dos dados, é uma boa ideia atualizar as estatísticas na tabela de destino para garantir que reflitam com precisão a nova distribuição dos dados em suas respectivas partições:</span><span class="sxs-lookup"><span data-stu-id="7a78e-196">Once you have completed the movement of the data it is a good idea to refresh the statistics on the target table to ensure they accurately reflect the new distribution of the data in their respective partitions:</span></span>

```sql
UPDATE STATISTICS [dbo].[FactInternetSales];
```

### <a name="table-partitioning-source-control"></a><span data-ttu-id="7a78e-197">Controle da origem do particionamento da tabela</span><span class="sxs-lookup"><span data-stu-id="7a78e-197">Table partitioning source control</span></span>
<span data-ttu-id="7a78e-198">Para evitar a definição da tabela de **rusting** em seu sistema de controle de origem, você talvez queira considerar a abordagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="7a78e-198">To avoid your table definition from **rusting** in your source control system you may want to consider the following approach:</span></span>

1. <span data-ttu-id="7a78e-199">Criar a tabela como uma tabela particionada, mas sem valores de partição</span><span class="sxs-lookup"><span data-stu-id="7a78e-199">Create the table as a partitioned table but with no partition values</span></span>

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

1. <span data-ttu-id="7a78e-200">`SPLIT` a tabela como parte do processo de implantação:</span><span class="sxs-lookup"><span data-stu-id="7a78e-200">`SPLIT` the table as part of the deployment process:</span></span>

```sql
-- Create a table containing the partition boundaries

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

-- Iterate over the partition boundaries and split the table

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

<span data-ttu-id="7a78e-201">Com essa abordagem, o código no controle de origem permanece estático e são permitidos valores de limite de particionamento dinâmicos, evoluindo com o depósito ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="7a78e-201">With this approach the code in source control remains static and the partitioning boundary values are allowed to be dynamic; evolving with the warehouse over time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a78e-202">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7a78e-202">Next steps</span></span>
<span data-ttu-id="7a78e-203">Para saber mais, confira os artigos em [Visão geral da tabela][Overview], [Tipos de dados de tabela][Data Types], [Distribuindo uma tabela][Distribute], [Indexando uma tabela][Index], [Mantendo estatísticas de tabela][Statistics] e [Tabelas temporárias][Temporary].</span><span class="sxs-lookup"><span data-stu-id="7a78e-203">To learn more, see the articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="7a78e-204">Para saber mais sobre as práticas recomendadas, consulte [Práticas Recomendadas do SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="7a78e-204">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
