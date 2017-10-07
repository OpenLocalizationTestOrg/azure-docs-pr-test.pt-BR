---
title: "desempenho do índice columnstore aaaImprove no SQL Azure | Microsoft Docs"
description: "Reduza os requisitos de memória ou aumentar Olá memória disponível toomaximize Olá número de linhas de que um índice columnstore compacta em cada grupo de linhas."
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
ms.openlocfilehash: 2c5a68435aa200236a2dc8538aa4638b52a59093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="maximizing-rowgroup-quality-for-columnstore"></a><span data-ttu-id="82d74-103">Maximizando a qualidade do grupo de linhas para o columnstore</span><span class="sxs-lookup"><span data-stu-id="82d74-103">Maximizing rowgroup quality for columnstore</span></span>

<span data-ttu-id="82d74-104">Qualidade do grupo de linhas é determinada pelo número de saudação de linhas em um grupo de linhas.</span><span class="sxs-lookup"><span data-stu-id="82d74-104">Rowgroup quality is determined by hello number of rows in a rowgroup.</span></span> <span data-ttu-id="82d74-105">Reduza os requisitos de memória ou aumentar Olá memória disponível toomaximize Olá número de linhas de que um índice columnstore compacta em cada grupo de linhas.</span><span class="sxs-lookup"><span data-stu-id="82d74-105">Reduce memory requirements or increase hello available memory toomaximize hello number of rows a columnstore index compresses into each rowgroup.</span></span>  <span data-ttu-id="82d74-106">Use essas taxas de compactação métodos tooimprove e o desempenho da consulta para índices columnstore.</span><span class="sxs-lookup"><span data-stu-id="82d74-106">Use these methods tooimprove compression rates and query performance for columnstore indexes.</span></span>

## <a name="why-hello-rowgroup-size-matters"></a><span data-ttu-id="82d74-107">Por que o tamanho do rowgroup Olá é importante</span><span class="sxs-lookup"><span data-stu-id="82d74-107">Why hello rowgroup size matters</span></span>
<span data-ttu-id="82d74-108">Desde que um índice columnstore examina uma tabela por meio do exame segmentos de colunas de rowgroups individuais, maximizar o número de saudação de linhas em cada grupo de linhas melhora o desempenho de consulta.</span><span class="sxs-lookup"><span data-stu-id="82d74-108">Since a columnstore index scans a table by scanning column segments of individual rowgroups, maximizing hello number of rows in each rowgroup enhances query performance.</span></span> <span data-ttu-id="82d74-109">Quando rowgroups tiver um grande número de linhas, a compactação de dados melhora o que significa que há menos tooread de dados do disco.</span><span class="sxs-lookup"><span data-stu-id="82d74-109">When rowgroups have a high number of rows, data compression improves which means there is less data tooread from disk.</span></span>

<span data-ttu-id="82d74-110">Para obter mais informações sobre rowgroups, consulte [Guia de índices Columnstore](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="82d74-110">For more information about rowgroups, see [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

## <a name="target-size-for-rowgroups"></a><span data-ttu-id="82d74-111">Tamanho de destino para rowgroups</span><span class="sxs-lookup"><span data-stu-id="82d74-111">Target size for rowgroups</span></span>
<span data-ttu-id="82d74-112">Para melhor desempenho de consulta, o objetivo de Olá é toomaximize número de saudação de linhas por grupo de linhas em um índice columnstore.</span><span class="sxs-lookup"><span data-stu-id="82d74-112">For best query performance, hello goal is toomaximize hello number of rows per rowgroup in a columnstore index.</span></span> <span data-ttu-id="82d74-113">Um rowgroup pode ter, no máximo, 1.048.576 linhas.</span><span class="sxs-lookup"><span data-stu-id="82d74-113">A rowgroup can have a maximum of 1,048,576 rows.</span></span> <span data-ttu-id="82d74-114">Seu toonot okey tem o número de máximo de saudação de linhas por rowgroup.</span><span class="sxs-lookup"><span data-stu-id="82d74-114">It's okay toonot have hello maximum number of rows per rowgroup.</span></span> <span data-ttu-id="82d74-115">Os índices Columnstore obtêm um bom desempenho quando os rowgroups têm, pelo menos, 100.000 linhas.</span><span class="sxs-lookup"><span data-stu-id="82d74-115">Columnstore indexes achieve good performance when rowgroups have at least 100,000 rows.</span></span>

## <a name="rowgroups-can-get-trimmed-during-compression"></a><span data-ttu-id="82d74-116">Os rowgroups podem ser cortados durante a compactação</span><span class="sxs-lookup"><span data-stu-id="82d74-116">Rowgroups can get trimmed during compression</span></span>

<span data-ttu-id="82d74-117">Durante uma bulk load ou columnstore recompilação de índice, às vezes, há não suficiente toocompress disponíveis de memória que todos Olá linhas designadas para cada grupo de linhas.</span><span class="sxs-lookup"><span data-stu-id="82d74-117">During a bulk load or columnstore index rebuild, sometimes there isn't enough memory available toocompress all hello rows designated for each rowgroup.</span></span> <span data-ttu-id="82d74-118">Quando há pressão de memória, índices columnstore trim tamanhos do rowgroup Olá para que compactação ColumnStore Olá pode ter êxito.</span><span class="sxs-lookup"><span data-stu-id="82d74-118">When there is memory pressure, columnstore indexes trim hello rowgroup sizes so compression into hello columnstore can succeed.</span></span> 

<span data-ttu-id="82d74-119">Quando há linhas de toocompress 10.000 pelo menos memória insuficiente em cada grupo de linhas, o SQL Data Warehouse gera um erro.</span><span class="sxs-lookup"><span data-stu-id="82d74-119">When there is insufficient memory toocompress at least 10,000 rows into each rowgroup, SQL Data Warehouse generates an error.</span></span>

<span data-ttu-id="82d74-120">Para obter mais informações sobre o carregamento em massa, consulte [Carregamento em massa em um índice columnstore clusterizado](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span><span class="sxs-lookup"><span data-stu-id="82d74-120">For more information on bulk loading, see [Bulk load into a clustered columnstore index](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span></span>

## <a name="how-toomonitor-rowgroup-quality"></a><span data-ttu-id="82d74-121">Como toomonitor rowgroup qualidade</span><span class="sxs-lookup"><span data-stu-id="82d74-121">How toomonitor rowgroup quality</span></span>

<span data-ttu-id="82d74-122">Há uma DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) que expõe informações úteis, como o número de linhas em rowgroups e hello motivo para a fragmentação se há foi cortar.</span><span class="sxs-lookup"><span data-stu-id="82d74-122">There is a DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) that exposes useful information such as number of rows in rowgroups and hello reason for trimming if there was trimming.</span></span> <span data-ttu-id="82d74-123">Você pode criar hello após a exibição como uma maneira útil tooquery informações tooget DMV na remoção do grupo de linhas.</span><span class="sxs-lookup"><span data-stu-id="82d74-123">You can create hello following view as a handy way tooquery this DMV tooget information on rowgroup trimming.</span></span>

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

<span data-ttu-id="82d74-124">Olá trim_reason_desc informa se Olá rowgroup foi cortado (trim_reason_desc = NO_TRIM implica sem corte e grupo de linhas é de melhor qualidade).</span><span class="sxs-lookup"><span data-stu-id="82d74-124">hello trim_reason_desc tells whether hello rowgroup was trimmed(trim_reason_desc = NO_TRIM implies there was no trimming and row group is of optimal quality).</span></span> <span data-ttu-id="82d74-125">Olá motivos trim indicam prematuro corte do grupo de linhas de saudação:</span><span class="sxs-lookup"><span data-stu-id="82d74-125">hello following trim reasons indicate premature trimming of hello rowgroup:</span></span>
- <span data-ttu-id="82d74-126">Carregamento em MASSA: Esse motivo do corte é usado quando o lote de entrada hello de linhas para carregamento Olá tinha menos de 1 milhão de linhas.</span><span class="sxs-lookup"><span data-stu-id="82d74-126">BULKLOAD: This trim reason is used when hello incoming batch of rows for hello load had less than 1 million rows.</span></span> <span data-ttu-id="82d74-127">mecanismo de saudação criará grupos de linhas compactado se há maior que 100.000 linhas sendo inseridas (como tooinserting contrário no repositório de delta Olá), mas conjuntos Olá tooBULKLOAD motivo trim.</span><span class="sxs-lookup"><span data-stu-id="82d74-127">hello engine will create compressed row groups if there are greater than 100,000 rows being inserted (as opposed tooinserting into hello delta store) but sets hello trim reason tooBULKLOAD.</span></span> <span data-ttu-id="82d74-128">Nesse cenário, considere aumentar o tooaccumulate de janela de carga de lote mais linhas.</span><span class="sxs-lookup"><span data-stu-id="82d74-128">In this scenario, consider increasing your batch load window tooaccumulate more rows.</span></span> <span data-ttu-id="82d74-129">Além disso, reavalie sua tooensure de esquema de particionamento não está muito granular, como grupos de linhas não podem abranger os limites de partição.</span><span class="sxs-lookup"><span data-stu-id="82d74-129">Also, reevaluate your partitioning scheme tooensure it is not too granular as row groups cannot span partition boundaries.</span></span>
- <span data-ttu-id="82d74-130">MEMORY_LIMITATION: toocreate grupos de linhas com 1 milhão de linhas, uma determinada quantidade de memória de trabalho é exigido pelo mecanismo de saudação.</span><span class="sxs-lookup"><span data-stu-id="82d74-130">MEMORY_LIMITATION: toocreate row groups with 1 million rows, a certain amount of working memory is required by hello engine.</span></span> <span data-ttu-id="82d74-131">Quando a memória disponível de saudação ao carregar a sessão é menor que o hello necessário trabalhar memória, grupos de linhas prematuramente obtenham cortados.</span><span class="sxs-lookup"><span data-stu-id="82d74-131">When available memory of hello loading session is less than hello required working memory, row groups get prematurely trimmed.</span></span> <span data-ttu-id="82d74-132">Olá seções a seguir explica como tooestimate memória necessária e alocar mais memória.</span><span class="sxs-lookup"><span data-stu-id="82d74-132">hello following sections explain how tooestimate memory required and allocate more memory.</span></span>
- <span data-ttu-id="82d74-133">DICTIONARY_SIZE: Este motivo do corte indica que a fragmentação do grupo de linhas ocorreu devido a pelo menos uma coluna de cadeia de caracteres com cadeias de caracteres ampla e/ou de alta cardinalidade.</span><span class="sxs-lookup"><span data-stu-id="82d74-133">DICTIONARY_SIZE: This trim reason indicates that rowgroup trimming occurred because there was at least one string column with wide and/or high cardinality strings.</span></span> <span data-ttu-id="82d74-134">tamanho do dicionário Olá é limitado too16 MB na memória e quando esse limite é atingido o grupo de linhas de saudação é compactado.</span><span class="sxs-lookup"><span data-stu-id="82d74-134">hello dictionary size is limited too16 MB in memory and once this limit is reached hello row group is compressed.</span></span> <span data-ttu-id="82d74-135">Se você se deparar com essa situação, considere isolar coluna problemático Olá em uma tabela separada.</span><span class="sxs-lookup"><span data-stu-id="82d74-135">If you do run into this situation, consider isolating hello problematic column into a separate table.</span></span>

## <a name="how-tooestimate-memory-requirements"></a><span data-ttu-id="82d74-136">Como os requisitos de memória tooestimate</span><span class="sxs-lookup"><span data-stu-id="82d74-136">How tooestimate memory requirements</span></span>

<!--
tooview an estimate of hello memory requirements toocompress a rowgroup of maximum size into a columnstore index, download and run hello view [dbo.vCS_mon_mem_grant](). This view shows hello size of hello memory grant that a rowgroup requires for compression in toohello columnstore.
-->

<span data-ttu-id="82d74-137">Olá máximo de memória necessária toocompress um rowgroup é aproximadamente</span><span class="sxs-lookup"><span data-stu-id="82d74-137">hello maximum required memory toocompress one rowgroup is approximately</span></span>

- <span data-ttu-id="82d74-138">72 MB +</span><span class="sxs-lookup"><span data-stu-id="82d74-138">72 MB +</span></span>
- <span data-ttu-id="82d74-139">\#linhas \* \#colunas \* 8 bytes +</span><span class="sxs-lookup"><span data-stu-id="82d74-139">\#rows \* \#columns \* 8 bytes +</span></span>
- <span data-ttu-id="82d74-140">\#linhas \* \#colunas de cadeia de caracteres curta \* 32 bytes +</span><span class="sxs-lookup"><span data-stu-id="82d74-140">\#rows \* \#short-string-columns \* 32 bytes +</span></span>
- <span data-ttu-id="82d74-141">\#colunas de cadeia de caracteres longa \* 16 MB para o dicionário de compactação</span><span class="sxs-lookup"><span data-stu-id="82d74-141">\#long-string-columns \* 16 MB for compression dictionary</span></span>

<span data-ttu-id="82d74-142">em que as colunas de cadeia de caracteres curta usam tipos de dados de cadeia de caracteres de <= 32 bytes e as colunas de cadeia de caracteres longa usam tipos de dados de cadeia de caracteres de > 32 bytes.</span><span class="sxs-lookup"><span data-stu-id="82d74-142">where short-string-columns use string data types of <= 32 bytes and long-string-columns use string data types of > 32 bytes.</span></span>

<span data-ttu-id="82d74-143">As cadeias de caracteres longas são compactadas com um método de compactação projetado para a compactação de texto.</span><span class="sxs-lookup"><span data-stu-id="82d74-143">Long strings are compressed with a compression method designed for compressing text.</span></span> <span data-ttu-id="82d74-144">Esse método de compactação usa um *dicionário* toostore padrões de texto.</span><span class="sxs-lookup"><span data-stu-id="82d74-144">This compression method uses a *dictionary* toostore text patterns.</span></span> <span data-ttu-id="82d74-145">tamanho máximo de saudação de um dicionário é 16 MB.</span><span class="sxs-lookup"><span data-stu-id="82d74-145">hello maximum size of a dictionary is 16 MB.</span></span> <span data-ttu-id="82d74-146">Há apenas um dicionário para cada coluna de cadeia de caracteres longa no grupo de linhas de saudação.</span><span class="sxs-lookup"><span data-stu-id="82d74-146">There is only one dictionary for each long string column in hello rowgroup.</span></span>

<span data-ttu-id="82d74-147">Para obter uma discussão detalhada sobre os requisitos de memória de columnstore, assista ao vídeo [Escala do SQL Data Warehouse do Azure: configuração e diretrizes](https://myignite.microsoft.com/videos/14822).</span><span class="sxs-lookup"><span data-stu-id="82d74-147">For an in-depth discussion of columnstore memory requirements, see the video [Azure SQL Data Warehouse scaling: configuration and guidance](https://myignite.microsoft.com/videos/14822).</span></span>

## <a name="ways-tooreduce-memory-requirements"></a><span data-ttu-id="82d74-148">Requisitos de memória tooreduce maneiras</span><span class="sxs-lookup"><span data-stu-id="82d74-148">Ways tooreduce memory requirements</span></span>

<span data-ttu-id="82d74-149">Use Olá seguindo os requisitos de memória de saudação técnicas tooreduce para compactar os rowgroups em índices columnstore.</span><span class="sxs-lookup"><span data-stu-id="82d74-149">Use hello following techniques tooreduce hello memory requirements for compressing rowgroups into columnstore indexes.</span></span>

### <a name="use-fewer-columns"></a><span data-ttu-id="82d74-150">Usar menos colunas</span><span class="sxs-lookup"><span data-stu-id="82d74-150">Use fewer columns</span></span>
<span data-ttu-id="82d74-151">Se possível, crie tabela Olá com menos colunas.</span><span class="sxs-lookup"><span data-stu-id="82d74-151">If possible, design hello table with fewer columns.</span></span> <span data-ttu-id="82d74-152">Quando um rowgroup é compactado no columnstore hello, o índice de columnstore Olá compacta cada segmento de coluna separadamente.</span><span class="sxs-lookup"><span data-stu-id="82d74-152">When a rowgroup is compressed into hello columnstore, hello columnstore index compresses each column segment separately.</span></span> <span data-ttu-id="82d74-153">Olá, portanto, os requisitos de memória toocompress um grupo de linhas aumente como Olá aumento do número de colunas.</span><span class="sxs-lookup"><span data-stu-id="82d74-153">Therefore hello memory requirements toocompress a rowgroup increase as hello number of columns increases.</span></span>


### <a name="use-fewer-string-columns"></a><span data-ttu-id="82d74-154">Usar menos colunas de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="82d74-154">Use fewer string columns</span></span>
<span data-ttu-id="82d74-155">As colunas de tipos de dados de cadeia de caracteres exigem mais memória do que os tipos de dados numéricos e de data.</span><span class="sxs-lookup"><span data-stu-id="82d74-155">Columns of string data types require more memory than numeric and date data types.</span></span> <span data-ttu-id="82d74-156">requisitos de memória tooreduce, considere remover colunas de cadeia de caracteres de tabelas de fatos e colocá-los em tabelas de dimensão menores.</span><span class="sxs-lookup"><span data-stu-id="82d74-156">tooreduce memory requirements, consider removing string columns from fact tables and putting them in smaller dimension tables.</span></span>

<span data-ttu-id="82d74-157">Requisitos de memória adicionais para a compactação de cadeia de caracteres:</span><span class="sxs-lookup"><span data-stu-id="82d74-157">Additional memory requirements for string compression:</span></span>

- <span data-ttu-id="82d74-158">Tipos de dados de cadeia de caracteres too32 caracteres podem exigir 32 bytes adicionais por valor.</span><span class="sxs-lookup"><span data-stu-id="82d74-158">String data types up too32 characters can require 32 additional bytes per value.</span></span>
- <span data-ttu-id="82d74-159">Tipos de dados de cadeia de caracteres com mais de 32 caracteres são compactados usando métodos de dicionário.</span><span class="sxs-lookup"><span data-stu-id="82d74-159">String data types with more than 32 characters are compressed using dictionary methods.</span></span>  <span data-ttu-id="82d74-160">Cada coluna no rowgroup Olá pode exigir o dicionário do tooan adicional 16 MB toobuild hello.</span><span class="sxs-lookup"><span data-stu-id="82d74-160">Each column in hello rowgroup can require up tooan additional 16 MB toobuild hello dictionary.</span></span>

### <a name="avoid-over-partitioning"></a><span data-ttu-id="82d74-161">Evitar o excesso de particionamento</span><span class="sxs-lookup"><span data-stu-id="82d74-161">Avoid over-partitioning</span></span>

<span data-ttu-id="82d74-162">Os índices Columnstore criam um ou mais rowgroups por partição.</span><span class="sxs-lookup"><span data-stu-id="82d74-162">Columnstore indexes create one or more rowgroups per partition.</span></span> <span data-ttu-id="82d74-163">No SQL Data Warehouse, o número de saudação de partições rapidamente aumenta porque dados saudação são distribuídos e cada distribuição é particionada.</span><span class="sxs-lookup"><span data-stu-id="82d74-163">In SQL Data Warehouse, hello number of partitions grows quickly because hello data is distributed and each distribution is partitioned.</span></span> <span data-ttu-id="82d74-164">Se a tabela Olá tem muitas partições, pode não ser suficiente rowgroups de saudação toofill linhas.</span><span class="sxs-lookup"><span data-stu-id="82d74-164">If hello table has too many partitions, there might not be enough rows toofill hello rowgroups.</span></span> <span data-ttu-id="82d74-165">falta de saudação de linhas não cria a pressão de memória durante a compactação, mas leva toorowgroups que não obtenha o melhor desempenho de consulta de columnstore hello.</span><span class="sxs-lookup"><span data-stu-id="82d74-165">hello lack of rows does not create memory pressure during compression, but it leads toorowgroups that do not achieve hello best columnstore query performance.</span></span>

<span data-ttu-id="82d74-166">Outro motivo tooavoid excesso de particionamento é uma sobrecarga de memória para carregamento de linhas em um índice columnstore em uma tabela particionada.</span><span class="sxs-lookup"><span data-stu-id="82d74-166">Another reason tooavoid over-partitioning is there is a memory overhead for loading rows into a columnstore index on a partitioned table.</span></span> <span data-ttu-id="82d74-167">Durante o carregamento, várias partições podem receber linhas de entrada hello, que são mantidas na memória até que cada partição tem suficiente toobe linhas compactada.</span><span class="sxs-lookup"><span data-stu-id="82d74-167">During a load, many partitions could receive hello incoming rows, which are held in memory until each partition has enough rows toobe compressed.</span></span> <span data-ttu-id="82d74-168">Ter um número excessivo de partições cria pressão de memória adicional.</span><span class="sxs-lookup"><span data-stu-id="82d74-168">Having too many partitions creates additional memory pressure.</span></span>

### <a name="simplify-hello-load-query"></a><span data-ttu-id="82d74-169">Simplificar a consulta de carga Olá</span><span class="sxs-lookup"><span data-stu-id="82d74-169">Simplify hello load query</span></span>

<span data-ttu-id="82d74-170">banco de dados de saudação compartilha Olá concessão de memória para uma consulta entre todos os operadores de saudação na consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="82d74-170">hello database shares hello memory grant for a query among all hello operators in hello query.</span></span> <span data-ttu-id="82d74-171">Quando uma consulta de carga tem relações e tipos complexos, Olá memória disponível para a compactação é reduzida.</span><span class="sxs-lookup"><span data-stu-id="82d74-171">When a load query has complex sorts and joins, hello memory available for compression is reduced.</span></span>

<span data-ttu-id="82d74-172">Olá carga consulta toofocus somente na consulta Olá de carregamento de design.</span><span class="sxs-lookup"><span data-stu-id="82d74-172">Design hello load query toofocus only on loading hello query.</span></span> <span data-ttu-id="82d74-173">Se você precisar toorun transformações nos dados hello, executá-los separado da consulta de carga hello.</span><span class="sxs-lookup"><span data-stu-id="82d74-173">If you need toorun transformations on hello data, run them separate from hello load query.</span></span> <span data-ttu-id="82d74-174">Por exemplo, dados de saudação do estágio em uma tabela de heap, executar transformações de saudação e, em seguida, carregar Olá tabela de preparo no índice de columnstore hello.</span><span class="sxs-lookup"><span data-stu-id="82d74-174">For example, stage hello data in a heap table, run hello transformations, and then load hello staging table into hello columnstore index.</span></span> <span data-ttu-id="82d74-175">Você pode também carregar dados saudação primeiro e usar Olá MPP sistema tootransform Olá dados.</span><span class="sxs-lookup"><span data-stu-id="82d74-175">You can also load hello data first and then use hello MPP system tootransform hello data.</span></span>

### <a name="adjust-maxdop"></a><span data-ttu-id="82d74-176">Ajustar o MAXDOP</span><span class="sxs-lookup"><span data-stu-id="82d74-176">Adjust MAXDOP</span></span>

<span data-ttu-id="82d74-177">Cada distribuição compacta rowgroups Olá ColumnStore em paralelo quando há mais de um núcleo de CPU disponível por distribuição.</span><span class="sxs-lookup"><span data-stu-id="82d74-177">Each distribution compresses rowgroups into hello columnstore in parallel when there is more than one CPU core available per distribution.</span></span> <span data-ttu-id="82d74-178">paralelismo de saudação requer mais recursos de memória, que podem levar a pressão toomemory e remoção de linhas.</span><span class="sxs-lookup"><span data-stu-id="82d74-178">hello parallelism requires additional memory resources, which can lead toomemory pressure and rowgroup trimming.</span></span>

<span data-ttu-id="82d74-179">tooreduce pressão de memória, você pode usar o hello MAXDOP consulta dica tooforce Olá carga operação toorun em modo serial dentro de cada distribuição.</span><span class="sxs-lookup"><span data-stu-id="82d74-179">tooreduce memory pressure, you can use hello MAXDOP query hint tooforce hello load operation toorun in serial mode within each distribution.</span></span>

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-tooallocate-more-memory"></a><span data-ttu-id="82d74-180">Maneiras tooallocate mais memória</span><span class="sxs-lookup"><span data-stu-id="82d74-180">Ways tooallocate more memory</span></span>

<span data-ttu-id="82d74-181">Classe de recurso de usuário de tamanho e hello DWU juntos determinar quanta memória está disponível para uma consulta de usuário.</span><span class="sxs-lookup"><span data-stu-id="82d74-181">DWU size and hello user resource class together determine how much memory is available for a user query.</span></span> <span data-ttu-id="82d74-182">tooincrease Olá para concessão de memória para uma consulta de carga, você pode aumentar o número de saudação do DWUs ou aumentar a classe de recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="82d74-182">tooincrease hello memory grant for a load query, you can either increase hello number of DWUs or increase hello resource class.</span></span>

- <span data-ttu-id="82d74-183">Olá tooincrease DWUs, consulte [como dimensionar o desempenho?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span><span class="sxs-lookup"><span data-stu-id="82d74-183">tooincrease hello DWUs, see [How do I scale performance?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span></span>
- <span data-ttu-id="82d74-184">classe de recurso de saudação toochange para uma consulta, consulte [alterar um exemplo de classe de recurso de usuário](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="82d74-184">toochange hello resource class for a query, see [Change a user resource class example](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

<span data-ttu-id="82d74-185">Por exemplo, em 100 DWU um usuário na classe de recurso Olá smallrc pode usar 100 MB de memória para cada distribuição.</span><span class="sxs-lookup"><span data-stu-id="82d74-185">For example, on DWU 100 a user in hello smallrc resource class can use 100 MB of memory for each distribution.</span></span> <span data-ttu-id="82d74-186">Para obter detalhes hello, consulte [simultaneidade no Data Warehouse SQL](sql-data-warehouse-develop-concurrency.md).</span><span class="sxs-lookup"><span data-stu-id="82d74-186">For hello details, see [Concurrency in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span></span>

<span data-ttu-id="82d74-187">Suponha que você determinar que precisa de 700 MB de tamanhos do rowgroup de alta qualidade de tooget de memória.</span><span class="sxs-lookup"><span data-stu-id="82d74-187">Suppose you determine that you need 700 MB of memory tooget high-quality rowgroup sizes.</span></span> <span data-ttu-id="82d74-188">Estes exemplos mostram como você pode executar a consulta de carga Olá com memória suficiente.</span><span class="sxs-lookup"><span data-stu-id="82d74-188">These examples show how you can run hello load query with enough memory.</span></span>

- <span data-ttu-id="82d74-189">Usando 1000 DWUs e mediumrc, a concessão de memória é de 800 MB</span><span class="sxs-lookup"><span data-stu-id="82d74-189">Using DWU 1000 and mediumrc, your memory grant is 800 MB</span></span>
- <span data-ttu-id="82d74-190">Usando 600 DWUs e largerc, a concessão de memória é de 800 MB.</span><span class="sxs-lookup"><span data-stu-id="82d74-190">Using DWU 600 and largerc, your memory grant is 800 MB.</span></span>


## <a name="next-steps"></a><span data-ttu-id="82d74-191">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="82d74-191">Next steps</span></span>

<span data-ttu-id="82d74-192">toofind mais maneiras tooimprove desempenho SQL Data Warehouse, consulte Olá [visão geral do desempenho](sql-data-warehouse-overview-manage-user-queries.md).</span><span class="sxs-lookup"><span data-stu-id="82d74-192">toofind more ways tooimprove performance in SQL Data Warehouse, see hello [Performance overview](sql-data-warehouse-overview-manage-user-queries.md).</span></span>

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
