---
title: "Melhorar o desempenho do índice columnstore no Azure SQL | Microsoft Docs"
description: "Reduza os requisitos de memória ou aumente a memória disponível para maximizar o número de linhas que um índice columnstore compacta em cada rowgroup."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 6/2/2017
ms.author: shigu;barbkess
ms.openlocfilehash: f0e0b839b4a0c216eee2eb5134d43b91d8f83289
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="maximizing-rowgroup-quality-for-columnstore"></a><span data-ttu-id="dfdaf-103">Maximizando a qualidade do grupo de linhas para o columnstore</span><span class="sxs-lookup"><span data-stu-id="dfdaf-103">Maximizing rowgroup quality for columnstore</span></span>

<span data-ttu-id="dfdaf-104">A qualidade do grupo de linhas é determinada pelo número de linhas em um grupo de linhas.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-104">Rowgroup quality is determined by the number of rows in a rowgroup.</span></span> <span data-ttu-id="dfdaf-105">Reduza os requisitos de memória ou aumente a memória disponível para maximizar o número de linhas que um índice columnstore compacta em cada rowgroup.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-105">Reduce memory requirements or increase the available memory to maximize the number of rows a columnstore index compresses into each rowgroup.</span></span>  <span data-ttu-id="dfdaf-106">Use estes métodos para melhorar as taxas de compactação e o desempenho da consulta em índices columnstore.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-106">Use these methods to improve compression rates and query performance for columnstore indexes.</span></span>

## <a name="why-the-rowgroup-size-matters"></a><span data-ttu-id="dfdaf-107">Por que o tamanho do rowgroup é importante</span><span class="sxs-lookup"><span data-stu-id="dfdaf-107">Why the rowgroup size matters</span></span>
<span data-ttu-id="dfdaf-108">Como um índice columnstore examina uma tabela com o exame de segmentos de coluna de rowgroups individuais, maximizar o número de linhas em cada rowgroup melhora o desempenho da consulta.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-108">Since a columnstore index scans a table by scanning column segments of individual rowgroups, maximizing the number of rows in each rowgroup enhances query performance.</span></span> <span data-ttu-id="dfdaf-109">Quando os rowgroups têm um número elevado de linhas, a compactação de dados melhora, o que significa que há menos dados para serem lidos do disco.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-109">When rowgroups have a high number of rows, data compression improves which means there is less data to read from disk.</span></span>

<span data-ttu-id="dfdaf-110">Para obter mais informações sobre rowgroups, consulte [Guia de índices Columnstore](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="dfdaf-110">For more information about rowgroups, see [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

## <a name="target-size-for-rowgroups"></a><span data-ttu-id="dfdaf-111">Tamanho de destino para rowgroups</span><span class="sxs-lookup"><span data-stu-id="dfdaf-111">Target size for rowgroups</span></span>
<span data-ttu-id="dfdaf-112">Para o melhor desempenho de consulta, o objetivo é maximizar o número de linhas por rowgroup em um índice columnstore.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-112">For best query performance, the goal is to maximize the number of rows per rowgroup in a columnstore index.</span></span> <span data-ttu-id="dfdaf-113">Um rowgroup pode ter, no máximo, 1.048.576 linhas.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-113">A rowgroup can have a maximum of 1,048,576 rows.</span></span> <span data-ttu-id="dfdaf-114">Não é um problema ter o número máximo de linhas por rowgroup.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-114">It's okay to not have the maximum number of rows per rowgroup.</span></span> <span data-ttu-id="dfdaf-115">Os índices Columnstore obtêm um bom desempenho quando os rowgroups têm, pelo menos, 100.000 linhas.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-115">Columnstore indexes achieve good performance when rowgroups have at least 100,000 rows.</span></span>

## <a name="rowgroups-can-get-trimmed-during-compression"></a><span data-ttu-id="dfdaf-116">Os rowgroups podem ser cortados durante a compactação</span><span class="sxs-lookup"><span data-stu-id="dfdaf-116">Rowgroups can get trimmed during compression</span></span>

<span data-ttu-id="dfdaf-117">Durante um carregamento em massa ou uma recompilação de índices columnstore, às vezes, não há memória suficiente disponível para compactar todas as linhas designadas para cada rowgroup.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-117">During a bulk load or columnstore index rebuild, sometimes there isn't enough memory available to compress all the rows designated for each rowgroup.</span></span> <span data-ttu-id="dfdaf-118">Quando há pressão de memória, os índices columnstore cortam o tamanho do rowgroup para que a compactação no columnstore possa ser bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-118">When there is memory pressure, columnstore indexes trim the rowgroup sizes so compression into the columnstore can succeed.</span></span> 

<span data-ttu-id="dfdaf-119">Quando não há memória suficiente para compactar, pelo menos, 10.000 linhas em cada rowgroup, o SQL Data Warehouse gera um erro.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-119">When there is insufficient memory to compress at least 10,000 rows into each rowgroup, SQL Data Warehouse generates an error.</span></span>

<span data-ttu-id="dfdaf-120">Para obter mais informações sobre o carregamento em massa, consulte [Carregamento em massa em um índice columnstore clusterizado](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span><span class="sxs-lookup"><span data-stu-id="dfdaf-120">For more information on bulk loading, see [Bulk load into a clustered columnstore index](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span></span>

## <a name="how-to-monitor-rowgroup-quality"></a><span data-ttu-id="dfdaf-121">Como monitorar a qualidade do grupo de linhas</span><span class="sxs-lookup"><span data-stu-id="dfdaf-121">How to monitor rowgroup quality</span></span>

<span data-ttu-id="dfdaf-122">Há uma DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) que expõe informações úteis, como o número de linhas em grupos de linhas e o motivo para a fragmentação se houver fragmentação.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-122">There is a DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) that exposes useful information such as number of rows in rowgroups and the reason for trimming if there was trimming.</span></span> <span data-ttu-id="dfdaf-123">Você pode criar a exibição a seguir como uma maneira útil consultar essa DMV para obter informações sobre a fragmentação do grupo de linhas.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-123">You can create the following view as a handy way to query this DMV to get information on rowgroup trimming.</span></span>

```sql
create view dbo.vCS_rg_physical_stats
as 
with cte
as
(
select   tb.[name]                    AS [logical_table_name]
,        rg.[row_group_id]            AS [row_group_id]
,        rg.[state]                   AS [state]
,        rg.[state_desc]              AS [state_desc]
,        rg.[total_rows]              AS [total_rows]
,        rg.[trim_reason_desc]        AS trim_reason_desc
,        mp.[physical_name]           AS physical_name
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb               ON  sm.[schema_id]          = tb.[schema_id]                             
JOIN    sys.[pdw_table_mappings] mp   ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt     ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[dm_pdw_nodes_db_column_store_row_group_physical_stats] rg      ON  rg.[object_id]     = nt.[object_id]
                                                                            AND rg.[pdw_node_id]   = nt.[pdw_node_id]
                                        AND rg.[distribution_id]    = nt.[distribution_id]                                          
)
select *
from cte;
```

<span data-ttu-id="dfdaf-124">O trim_reason_desc informa se o grupo de linhas foi cortado (trim_reason_desc = NO_TRIM implica que não houve corte e grupo de linhas é de melhor qualidade).</span><span class="sxs-lookup"><span data-stu-id="dfdaf-124">The trim_reason_desc tells whether the rowgroup was trimmed(trim_reason_desc = NO_TRIM implies there was no trimming and row group is of optimal quality).</span></span> <span data-ttu-id="dfdaf-125">Os motivos de corte a seguir indicam prematuro corte do grupo de linhas:</span><span class="sxs-lookup"><span data-stu-id="dfdaf-125">The following trim reasons indicate premature trimming of the rowgroup:</span></span>
- <span data-ttu-id="dfdaf-126">CARREGAMENTO EM MASSA: Esse motivo de corte é usado quando o lote de entrada de linhas para a carga tinha menos de 1 milhão de linhas.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-126">BULKLOAD: This trim reason is used when the incoming batch of rows for the load had less than 1 million rows.</span></span> <span data-ttu-id="dfdaf-127">O mecanismo criará grupos de linhas compactado se houver mais que 100.000 linhas sendo inseridas (em vez de inserir no repositório delta), mas define o motivo do corte para CARREGAMENTO EM MASSA.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-127">The engine will create compressed row groups if there are greater than 100,000 rows being inserted (as opposed to inserting into the delta store) but sets the trim reason to BULKLOAD.</span></span> <span data-ttu-id="dfdaf-128">Nesse cenário, considere aumentar a janela de carga de lote para acumular mais linhas.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-128">In this scenario, consider increasing your batch load window to accumulate more rows.</span></span> <span data-ttu-id="dfdaf-129">Além disso, reavalie o esquema de particionamento para garantir que não está muito granular, já que os grupos de linhas não podem abranger os limites de partição.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-129">Also, reevaluate your partitioning scheme to ensure it is not too granular as row groups cannot span partition boundaries.</span></span>
- <span data-ttu-id="dfdaf-130">MEMORY_LIMITATION: Para criar grupos de linhas com 1 milhão de linhas, uma determinada quantidade de memória de trabalho é necessária para o mecanismo.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-130">MEMORY_LIMITATION: To create row groups with 1 million rows, a certain amount of working memory is required by the engine.</span></span> <span data-ttu-id="dfdaf-131">Quando a memória disponível da sessão de carregamento é menor do que a memória necessária do trabalho, grupos de linhas são cortados prematuramente.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-131">When available memory of the loading session is less than the required working memory, row groups get prematurely trimmed.</span></span> <span data-ttu-id="dfdaf-132">As seções a seguir explicam como estimar a memória necessária e alocar mais memória.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-132">The following sections explain how to estimate memory required and allocate more memory.</span></span>
- <span data-ttu-id="dfdaf-133">DICTIONARY_SIZE: Este motivo do corte indica que a fragmentação do grupo de linhas ocorreu devido a pelo menos uma coluna de cadeia de caracteres com cadeias de caracteres ampla e/ou de alta cardinalidade.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-133">DICTIONARY_SIZE: This trim reason indicates that rowgroup trimming occurred because there was at least one string column with wide and/or high cardinality strings.</span></span> <span data-ttu-id="dfdaf-134">O tamanho do dicionário está limitado a 16 MB de memória e quando esse limite é atingido o grupo de linhas é compactado.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-134">The dictionary size is limited to 16 MB in memory and once this limit is reached the row group is compressed.</span></span> <span data-ttu-id="dfdaf-135">Se você se deparar com essa situação, considere isolar a coluna problemática em uma tabela separada.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-135">If you do run into this situation, consider isolating the problematic column into a separate table.</span></span>

## <a name="how-to-estimate-memory-requirements"></a><span data-ttu-id="dfdaf-136">Como estimar os requisitos de memória</span><span class="sxs-lookup"><span data-stu-id="dfdaf-136">How to estimate memory requirements</span></span>

<!--
To view an estimate of the memory requirements to compress a rowgroup of maximum size into a columnstore index, download and run the view [dbo.vCS_mon_mem_grant](). This view shows the size of the memory grant that a rowgroup requires for compression in to the columnstore.
-->

<span data-ttu-id="dfdaf-137">O máximo de memória necessário para compactar um rowgroup é aproximadamente</span><span class="sxs-lookup"><span data-stu-id="dfdaf-137">The maximum required memory to compress one rowgroup is approximately</span></span>

- <span data-ttu-id="dfdaf-138">72 MB +</span><span class="sxs-lookup"><span data-stu-id="dfdaf-138">72 MB +</span></span>
- <span data-ttu-id="dfdaf-139">\#linhas \* \#colunas \* 8 bytes +</span><span class="sxs-lookup"><span data-stu-id="dfdaf-139">\#rows \* \#columns \* 8 bytes +</span></span>
- <span data-ttu-id="dfdaf-140">\#linhas \* \#colunas de cadeia de caracteres curta \* 32 bytes +</span><span class="sxs-lookup"><span data-stu-id="dfdaf-140">\#rows \* \#short-string-columns \* 32 bytes +</span></span>
- <span data-ttu-id="dfdaf-141">\#colunas de cadeia de caracteres longa \* 16 MB para o dicionário de compactação</span><span class="sxs-lookup"><span data-stu-id="dfdaf-141">\#long-string-columns \* 16 MB for compression dictionary</span></span>

<span data-ttu-id="dfdaf-142">em que as colunas de cadeia de caracteres curta usam tipos de dados de cadeia de caracteres de <= 32 bytes e as colunas de cadeia de caracteres longa usam tipos de dados de cadeia de caracteres de > 32 bytes.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-142">where short-string-columns use string data types of <= 32 bytes and long-string-columns use string data types of > 32 bytes.</span></span>

<span data-ttu-id="dfdaf-143">As cadeias de caracteres longas são compactadas com um método de compactação projetado para a compactação de texto.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-143">Long strings are compressed with a compression method designed for compressing text.</span></span> <span data-ttu-id="dfdaf-144">Esse método de compactação usa um *dicionário* para armazenar os padrões de texto.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-144">This compression method uses a *dictionary* to store text patterns.</span></span> <span data-ttu-id="dfdaf-145">O tamanho máximo de um dicionário é de 16 MB.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-145">The maximum size of a dictionary is 16 MB.</span></span> <span data-ttu-id="dfdaf-146">Há apenas um dicionário para cada coluna de cadeia de caracteres longa no rowgroup.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-146">There is only one dictionary for each long string column in the rowgroup.</span></span>

<span data-ttu-id="dfdaf-147">Para obter uma discussão detalhada sobre os requisitos de memória de columnstore, assista ao vídeo [Escala do SQL Data Warehouse do Azure: configuração e diretrizes](https://myignite.microsoft.com/videos/14822).</span><span class="sxs-lookup"><span data-stu-id="dfdaf-147">For an in-depth discussion of columnstore memory requirements, see the video [Azure SQL Data Warehouse scaling: configuration and guidance](https://myignite.microsoft.com/videos/14822).</span></span>

## <a name="ways-to-reduce-memory-requirements"></a><span data-ttu-id="dfdaf-148">Maneiras de reduzir os requisitos de memória</span><span class="sxs-lookup"><span data-stu-id="dfdaf-148">Ways to reduce memory requirements</span></span>

<span data-ttu-id="dfdaf-149">Use as técnicas a seguir para reduzir os requisitos de memória para compactar rowgroups em índices columnstore.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-149">Use the following techniques to reduce the memory requirements for compressing rowgroups into columnstore indexes.</span></span>

### <a name="use-fewer-columns"></a><span data-ttu-id="dfdaf-150">Usar menos colunas</span><span class="sxs-lookup"><span data-stu-id="dfdaf-150">Use fewer columns</span></span>
<span data-ttu-id="dfdaf-151">Se possível, crie a tabela com menos colunas.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-151">If possible, design the table with fewer columns.</span></span> <span data-ttu-id="dfdaf-152">Quando um rowgroup é compactado no columnstore, o índice columnstore compacta cada segmento de coluna separadamente.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-152">When a rowgroup is compressed into the columnstore, the columnstore index compresses each column segment separately.</span></span> <span data-ttu-id="dfdaf-153">Portanto, os requisitos de memória para compactação de um rowgroup aumentam de acordo com o número de colunas.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-153">Therefore the memory requirements to compress a rowgroup increase as the number of columns increases.</span></span>


### <a name="use-fewer-string-columns"></a><span data-ttu-id="dfdaf-154">Usar menos colunas de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="dfdaf-154">Use fewer string columns</span></span>
<span data-ttu-id="dfdaf-155">As colunas de tipos de dados de cadeia de caracteres exigem mais memória do que os tipos de dados numéricos e de data.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-155">Columns of string data types require more memory than numeric and date data types.</span></span> <span data-ttu-id="dfdaf-156">Para reduzir os requisitos de memória, considere remover as colunas de cadeia de caracteres de tabelas de fatos e colocá-las em tabelas de dimensão menores.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-156">To reduce memory requirements, consider removing string columns from fact tables and putting them in smaller dimension tables.</span></span>

<span data-ttu-id="dfdaf-157">Requisitos de memória adicionais para a compactação de cadeia de caracteres:</span><span class="sxs-lookup"><span data-stu-id="dfdaf-157">Additional memory requirements for string compression:</span></span>

- <span data-ttu-id="dfdaf-158">Tipos de dados de cadeia de caracteres de até 32 caracteres podem exigir 32 bytes adicionais por valor.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-158">String data types up to 32 characters can require 32 additional bytes per value.</span></span>
- <span data-ttu-id="dfdaf-159">Tipos de dados de cadeia de caracteres com mais de 32 caracteres são compactados usando métodos de dicionário.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-159">String data types with more than 32 characters are compressed using dictionary methods.</span></span>  <span data-ttu-id="dfdaf-160">Cada coluna no rowgroup pode exigir até 16 MB adicionais para a criação do dicionário.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-160">Each column in the rowgroup can require up to an additional 16 MB to build the dictionary.</span></span>

### <a name="avoid-over-partitioning"></a><span data-ttu-id="dfdaf-161">Evitar o excesso de particionamento</span><span class="sxs-lookup"><span data-stu-id="dfdaf-161">Avoid over-partitioning</span></span>

<span data-ttu-id="dfdaf-162">Os índices Columnstore criam um ou mais rowgroups por partição.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-162">Columnstore indexes create one or more rowgroups per partition.</span></span> <span data-ttu-id="dfdaf-163">No SQL Data Warehouse, o número de partições aumenta rapidamente porque os dados são distribuídos e cada distribuição é particionada.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-163">In SQL Data Warehouse, the number of partitions grows quickly because the data is distributed and each distribution is partitioned.</span></span> <span data-ttu-id="dfdaf-164">Se a tabela tiver um número excessivo de partições, talvez não haja linhas suficientes para preencher os rowgroups.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-164">If the table has too many partitions, there might not be enough rows to fill the rowgroups.</span></span> <span data-ttu-id="dfdaf-165">A falta de linhas não cria a pressão de memória durante a compactação, mas leva a rowgroups que não obtêm o melhor desempenho de consulta de columnstore.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-165">The lack of rows does not create memory pressure during compression, but it leads to rowgroups that do not achieve the best columnstore query performance.</span></span>

<span data-ttu-id="dfdaf-166">Outro motivo para evitar o excesso de particionamento é que há uma sobrecarga de memória no carregamento de linhas em um índice columnstore em uma tabela particionada.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-166">Another reason to avoid over-partitioning is there is a memory overhead for loading rows into a columnstore index on a partitioned table.</span></span> <span data-ttu-id="dfdaf-167">Durante o carregamento, várias partições poderão receber as linhas de entrada, que são mantidas na memória até que cada partição tenha linhas suficientes para ser compactada.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-167">During a load, many partitions could receive the incoming rows, which are held in memory until each partition has enough rows to be compressed.</span></span> <span data-ttu-id="dfdaf-168">Ter um número excessivo de partições cria pressão de memória adicional.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-168">Having too many partitions creates additional memory pressure.</span></span>

### <a name="simplify-the-load-query"></a><span data-ttu-id="dfdaf-169">Simplificar a consulta de carga</span><span class="sxs-lookup"><span data-stu-id="dfdaf-169">Simplify the load query</span></span>

<span data-ttu-id="dfdaf-170">O banco de dados compartilha a concessão de memória para uma consulta entre todos os operadores na consulta.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-170">The database shares the memory grant for a query among all the operators in the query.</span></span> <span data-ttu-id="dfdaf-171">Quando uma consulta de carga tem classificações e junções complexas, a memória disponível para compactação é reduzida.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-171">When a load query has complex sorts and joins, the memory available for compression is reduced.</span></span>

<span data-ttu-id="dfdaf-172">Crie a consulta de carga para que ela se concentre apenas no carregamento da consulta.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-172">Design the load query to focus only on loading the query.</span></span> <span data-ttu-id="dfdaf-173">Se você precisar executar transformações nos dados, execute-as separadamente da consulta de carga.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-173">If you need to run transformations on the data, run them separate from the load query.</span></span> <span data-ttu-id="dfdaf-174">Por exemplo, prepare os dados em uma tabela de heap, execute as transformações e carregue a tabela de preparo no índice columnstore.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-174">For example, stage the data in a heap table, run the transformations, and then load the staging table into the columnstore index.</span></span> <span data-ttu-id="dfdaf-175">Você também pode carregar os dados primeiro e usar o sistema MPP para transformar os dados.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-175">You can also load the data first and then use the MPP system to transform the data.</span></span>

### <a name="adjust-maxdop"></a><span data-ttu-id="dfdaf-176">Ajustar o MAXDOP</span><span class="sxs-lookup"><span data-stu-id="dfdaf-176">Adjust MAXDOP</span></span>

<span data-ttu-id="dfdaf-177">Cada distribuição compacta rowgroups no columnstore em paralelo quando há mais de um núcleo de CPU disponível por distribuição.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-177">Each distribution compresses rowgroups into the columnstore in parallel when there is more than one CPU core available per distribution.</span></span> <span data-ttu-id="dfdaf-178">O paralelismo exige recursos de memória adicionais, o que pode levar à pressão de memória e ao corte de rowgroup.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-178">The parallelism requires additional memory resources, which can lead to memory pressure and rowgroup trimming.</span></span>

<span data-ttu-id="dfdaf-179">Para reduzir a pressão de memória, use a dica de consulta MAXDOP para forçar a operação de carregamento a ser executada em modo serial em cada distribuição.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-179">To reduce memory pressure, you can use the MAXDOP query hint to force the load operation to run in serial mode within each distribution.</span></span>

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-to-allocate-more-memory"></a><span data-ttu-id="dfdaf-180">Maneiras de alocar mais memória</span><span class="sxs-lookup"><span data-stu-id="dfdaf-180">Ways to allocate more memory</span></span>

<span data-ttu-id="dfdaf-181">O tamanho da DWU e a classe de recurso de usuário em conjunto determinam a quantidade de memória disponível para uma consulta de usuário.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-181">DWU size and the user resource class together determine how much memory is available for a user query.</span></span> <span data-ttu-id="dfdaf-182">Para aumentar a concessão de memória para uma consulta de carga, você pode aumentar o número de DWUs ou aumentar a classe de recurso.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-182">To increase the memory grant for a load query, you can either increase the number of DWUs or increase the resource class.</span></span>

- <span data-ttu-id="dfdaf-183">Para aumentar as DWUs, consulte [Como faço para escalar o desempenho?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span><span class="sxs-lookup"><span data-stu-id="dfdaf-183">To increase the DWUs, see [How do I scale performance?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span></span>
- <span data-ttu-id="dfdaf-184">Para alterar a classe de recurso de uma consulta, consulte [Alterar um exemplo de classe de recurso de usuário](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="dfdaf-184">To change the resource class for a query, see [Change a user resource class example](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

<span data-ttu-id="dfdaf-185">Por exemplo, em 100 DWUs, um usuário na classe de recurso smallrc pode usar 100 MB de memória para cada distribuição.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-185">For example, on DWU 100 a user in the smallrc resource class can use 100 MB of memory for each distribution.</span></span> <span data-ttu-id="dfdaf-186">Para obter detalhes, consulte [Simultaneidade no SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span><span class="sxs-lookup"><span data-stu-id="dfdaf-186">For the details, see [Concurrency in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span></span>

<span data-ttu-id="dfdaf-187">Suponha que você determina que precisa de 700 MB de memória para obter tamanhos de rowgroup de alta qualidade.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-187">Suppose you determine that you need 700 MB of memory to get high-quality rowgroup sizes.</span></span> <span data-ttu-id="dfdaf-188">Esses exemplos mostram como você pode executar a consulta de carga com memória suficiente.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-188">These examples show how you can run the load query with enough memory.</span></span>

- <span data-ttu-id="dfdaf-189">Usando 1000 DWUs e mediumrc, a concessão de memória é de 800 MB</span><span class="sxs-lookup"><span data-stu-id="dfdaf-189">Using DWU 1000 and mediumrc, your memory grant is 800 MB</span></span>
- <span data-ttu-id="dfdaf-190">Usando 600 DWUs e largerc, a concessão de memória é de 800 MB.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-190">Using DWU 600 and largerc, your memory grant is 800 MB.</span></span>


## <a name="next-steps"></a><span data-ttu-id="dfdaf-191">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dfdaf-191">Next steps</span></span>

<span data-ttu-id="dfdaf-192">Para encontrar mais maneiras de melhorar o desempenho no SQL Data Warehouse, consulte a [Visão geral do desempenho](sql-data-warehouse-overview-manage-user-queries.md).</span><span class="sxs-lookup"><span data-stu-id="dfdaf-192">To find more ways to improve performance in SQL Data Warehouse, see the [Performance overview](sql-data-warehouse-overview-manage-user-queries.md).</span></span>

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
