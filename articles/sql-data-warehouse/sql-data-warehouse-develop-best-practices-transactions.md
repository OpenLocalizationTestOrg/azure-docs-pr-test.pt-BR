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
# <a name="optimizing-transactions-for-sql-data-warehouse"></a><span data-ttu-id="ccbeb-103">Otimização de transações para o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ccbeb-103">Optimizing transactions for SQL Data Warehouse</span></span>
<span data-ttu-id="ccbeb-104">Este artigo explica como toooptimize Olá desempenho do seu código transacional, minimizando o risco de reversões longo.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-104">This article explains how toooptimize hello performance of your transactional code while minimizing risk for long rollbacks.</span></span>

## <a name="transactions-and-logging"></a><span data-ttu-id="ccbeb-105">Transações e registro em log</span><span class="sxs-lookup"><span data-stu-id="ccbeb-105">Transactions and logging</span></span>
<span data-ttu-id="ccbeb-106">As transações são um componente importante de um mecanismo de banco de dados relacional.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-106">Transactions are an important component of a relational database engine.</span></span> <span data-ttu-id="ccbeb-107">O SQL Data Warehouse usa transações durante a modificação de dados.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-107">SQL Data Warehouse uses transactions during data modification.</span></span> <span data-ttu-id="ccbeb-108">Essas transações podem ser implícitas ou explícitas.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-108">These transactions can be explicit or implicit.</span></span> <span data-ttu-id="ccbeb-109">As instruções individuais `INSERT`, `UPDATE` e `DELETE` são exemplos de transações implícitas.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-109">Single `INSERT`, `UPDATE` and `DELETE` statements are all examples of implicit transactions.</span></span> <span data-ttu-id="ccbeb-110">Transações explícitas são gravadas explicitamente por um desenvolvedor usando `BEGIN TRAN`, `COMMIT TRAN` ou `ROLLBACK TRAN` e normalmente são usados quando precisam de várias instruções de modificação toobe vinculado em uma única unidade atômica.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-110">Explicit transactions are written explicitly by a developer using `BEGIN TRAN`, `COMMIT TRAN` or `ROLLBACK TRAN` and are typically used when multiple modification statements need toobe tied together in a single atomic unit.</span></span> 

<span data-ttu-id="ccbeb-111">Banco de dados de toohello de alterações usando os logs de transação é confirmada do Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-111">Azure SQL Data Warehouse commits changes toohello database using transaction logs.</span></span> <span data-ttu-id="ccbeb-112">Cada distribuição tem seu próprio log de transações.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-112">Each distribution has its own transaction log.</span></span> <span data-ttu-id="ccbeb-113">As gravações de log de transações são automáticas.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-113">Transaction log writes are automatic.</span></span> <span data-ttu-id="ccbeb-114">Não é necessária nenhuma configuração.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-114">There is no configuration required.</span></span> <span data-ttu-id="ccbeb-115">No entanto, durante esse processo garante a gravação da saudação introduz uma sobrecarga no sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-115">However, whilst this process guarantees hello write it does introduce an overhead in hello system.</span></span> <span data-ttu-id="ccbeb-116">Você pode minimizar esse impacto ao escrever um código transacionalmente eficiente.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-116">You can minimize this impact by writing transactionally efficient code.</span></span> <span data-ttu-id="ccbeb-117">De modo geral, um código transacionalmente eficiente se enquadra em duas categorias.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-117">Transactionally efficient code broadly falls into two categories.</span></span>

* <span data-ttu-id="ccbeb-118">Aproveitar constructos mínimos de registro em log quando possível</span><span class="sxs-lookup"><span data-stu-id="ccbeb-118">Leverage minimal logging constructs where possible</span></span>
* <span data-ttu-id="ccbeb-119">Processar dados usando a forma singular de tooavoid no escopo de lotes de transações de longa execução</span><span class="sxs-lookup"><span data-stu-id="ccbeb-119">Process data using scoped batches tooavoid singular long running transactions</span></span>
* <span data-ttu-id="ccbeb-120">Adotar uma padrão para modificações grande tooa determinada partição de comutação de partição</span><span class="sxs-lookup"><span data-stu-id="ccbeb-120">Adopt a partition switching pattern for large modifications tooa given partition</span></span>

## <a name="minimal-vs-full-logging"></a><span data-ttu-id="ccbeb-121">Registro mínimo em log vs. registro total em log</span><span class="sxs-lookup"><span data-stu-id="ccbeb-121">Minimal vs. full logging</span></span>
<span data-ttu-id="ccbeb-122">Ao contrário das operações registradas completas, que usam Olá transaction log tookeep controlar cada linha alterada, operações minimamente registradas controlar de alocações de extensão e somente as alterações de metadados.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-122">Unlike fully logged operations, which use hello transaction log tookeep track of every row change, minimally logged operations keep track of extent allocations and meta-data changes only.</span></span> <span data-ttu-id="ccbeb-123">Portanto, o log mínimo envolve o registro somente as informações de saudação que é necessário toorollback a transação de saudação no evento de saudação de uma falha ou uma solicitação explícita (`ROLLBACK TRAN`).</span><span class="sxs-lookup"><span data-stu-id="ccbeb-123">Therefore, minimal logging involves logging only hello information that is required toorollback hello transaction in hello event of a failure or an explicit request (`ROLLBACK TRAN`).</span></span> <span data-ttu-id="ccbeb-124">Como muito menos informações são rastreadas no log de transações hello, uma operação minimamente registrada melhor do que uma operação totalmente registrada em log de tamanho similar.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-124">As much less information is tracked in hello transaction log, a minimally logged operation performs better than a similarly sized fully logged operation.</span></span> <span data-ttu-id="ccbeb-125">Além disso, como menos gravações passam o log de transações hello, uma quantidade menor de dados de log é gerada e portanto é e/s mais eficiente.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-125">Furthermore, because fewer writes go hello transaction log, a much smaller amount of log data is generated and so is more I/O efficient.</span></span>

<span data-ttu-id="ccbeb-126">limites de segurança de transação Olá só se aplicam a operações toofully conectado.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-126">hello transaction safety limits only apply toofully logged operations.</span></span>

> [!NOTE]
> <span data-ttu-id="ccbeb-127">As operações minimamente registradas em log podem participar de transações explícitas.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-127">Minimally logged operations can participate in explicit transactions.</span></span> <span data-ttu-id="ccbeb-128">Como todas as alterações nas estruturas de alocação são rastreadas, é possível tooroll back minimamente operações registradas.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-128">As all changes in allocation structures are tracked, it is possible tooroll back minimally logged operations.</span></span> <span data-ttu-id="ccbeb-129">É importante toounderstand alteração hello "mínimo" está conectado a ele não está conectado não.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-129">It is important toounderstand that hello change is "minimally" logged it is not un-logged.</span></span>
> 
> 

## <a name="minimally-logged-operations"></a><span data-ttu-id="ccbeb-130">Operações minimamente registradas em log</span><span class="sxs-lookup"><span data-stu-id="ccbeb-130">Minimally logged operations</span></span>
<span data-ttu-id="ccbeb-131">Olá operações a seguir têm a capacidade de ser registradas minimamente:</span><span class="sxs-lookup"><span data-stu-id="ccbeb-131">hello following operations are capable of being minimally logged:</span></span>

* <span data-ttu-id="ccbeb-132">CREATE TABLE AS SELECT ([CTAS][CTAS])</span><span class="sxs-lookup"><span data-stu-id="ccbeb-132">CREATE TABLE AS SELECT ([CTAS][CTAS])</span></span>
* <span data-ttu-id="ccbeb-133">INSERT..SELECT</span><span class="sxs-lookup"><span data-stu-id="ccbeb-133">INSERT..SELECT</span></span>
* <span data-ttu-id="ccbeb-134">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="ccbeb-134">CREATE INDEX</span></span>
* <span data-ttu-id="ccbeb-135">ALTER INDEX REBUILD</span><span class="sxs-lookup"><span data-stu-id="ccbeb-135">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="ccbeb-136">DROP INDEX</span><span class="sxs-lookup"><span data-stu-id="ccbeb-136">DROP INDEX</span></span>
* <span data-ttu-id="ccbeb-137">TRUNCATE TABLE</span><span class="sxs-lookup"><span data-stu-id="ccbeb-137">TRUNCATE TABLE</span></span>
* <span data-ttu-id="ccbeb-138">DROP TABLE</span><span class="sxs-lookup"><span data-stu-id="ccbeb-138">DROP TABLE</span></span>
* <span data-ttu-id="ccbeb-139">ALTER TABLE SWITCH PARTITION</span><span class="sxs-lookup"><span data-stu-id="ccbeb-139">ALTER TABLE SWITCH PARTITION</span></span>

<!--
- MERGE
- UPDATE on LOB Types .WRITE
- SELECT..INTO
-->

> [!NOTE]
> <span data-ttu-id="ccbeb-140">As operações de movimentação de dados internos (como `BROADCAST` e `SHUFFLE`) não são afetados pelo limite de segurança de transação hello.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-140">Internal data movement operations (such as `BROADCAST` and `SHUFFLE`) are not affected by hello transaction safety limit.</span></span>
> 
> 

## <a name="minimal-logging-with-bulk-load"></a><span data-ttu-id="ccbeb-141">Registro mínimo em log com carregamento em massa</span><span class="sxs-lookup"><span data-stu-id="ccbeb-141">Minimal logging with bulk load</span></span>
<span data-ttu-id="ccbeb-142">`CTAS` e `INSERT...SELECT` são ambos operações de carregamento em massa.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-142">`CTAS` and `INSERT...SELECT` are both bulk load operations.</span></span> <span data-ttu-id="ccbeb-143">No entanto, ambos são influenciadas pela definição de tabela de destino hello e dependem do cenário de carga hello.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-143">However, both are influenced by hello target table definition and depend on hello load scenario.</span></span> <span data-ttu-id="ccbeb-144">A seguir, uma tabela que explica se a operação em massa será total ou minimamente registrada em log:</span><span class="sxs-lookup"><span data-stu-id="ccbeb-144">Below is a table that explains if your bulk operation will be fully or minimally logged:</span></span>  

| <span data-ttu-id="ccbeb-145">Índice principal</span><span class="sxs-lookup"><span data-stu-id="ccbeb-145">Primary Index</span></span> | <span data-ttu-id="ccbeb-146">Cenário de carga</span><span class="sxs-lookup"><span data-stu-id="ccbeb-146">Load Scenario</span></span> | <span data-ttu-id="ccbeb-147">Modo de registro em log</span><span class="sxs-lookup"><span data-stu-id="ccbeb-147">Logging Mode</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ccbeb-148">Heap</span><span class="sxs-lookup"><span data-stu-id="ccbeb-148">Heap</span></span> |<span data-ttu-id="ccbeb-149">Qualquer</span><span class="sxs-lookup"><span data-stu-id="ccbeb-149">Any</span></span> |<span data-ttu-id="ccbeb-150">**Mínimo**</span><span class="sxs-lookup"><span data-stu-id="ccbeb-150">**Minimal**</span></span> |
| <span data-ttu-id="ccbeb-151">Índice clusterizado</span><span class="sxs-lookup"><span data-stu-id="ccbeb-151">Clustered Index</span></span> |<span data-ttu-id="ccbeb-152">Tabela de destino vazia</span><span class="sxs-lookup"><span data-stu-id="ccbeb-152">Empty target table</span></span> |<span data-ttu-id="ccbeb-153">**Mínimo**</span><span class="sxs-lookup"><span data-stu-id="ccbeb-153">**Minimal**</span></span> |
| <span data-ttu-id="ccbeb-154">Índice clusterizado</span><span class="sxs-lookup"><span data-stu-id="ccbeb-154">Clustered Index</span></span> |<span data-ttu-id="ccbeb-155">As linhas carregadas não se sobrepõem às páginas existentes no destino</span><span class="sxs-lookup"><span data-stu-id="ccbeb-155">Loaded rows do not overlap with existing pages in target</span></span> |<span data-ttu-id="ccbeb-156">**Mínimo**</span><span class="sxs-lookup"><span data-stu-id="ccbeb-156">**Minimal**</span></span> |
| <span data-ttu-id="ccbeb-157">Índice clusterizado</span><span class="sxs-lookup"><span data-stu-id="ccbeb-157">Clustered Index</span></span> |<span data-ttu-id="ccbeb-158">Linhas carregadas se sobrepõem com páginas existentes no destino</span><span class="sxs-lookup"><span data-stu-id="ccbeb-158">Loaded rows overlap with existing pages in target</span></span> |<span data-ttu-id="ccbeb-159">Completo</span><span class="sxs-lookup"><span data-stu-id="ccbeb-159">Full</span></span> |
| <span data-ttu-id="ccbeb-160">Índice columnstore clusterizado</span><span class="sxs-lookup"><span data-stu-id="ccbeb-160">Clustered Columnstore Index</span></span> |<span data-ttu-id="ccbeb-161">Tamanho do lote >= 102.400 por distribuição alinhada por partição</span><span class="sxs-lookup"><span data-stu-id="ccbeb-161">Batch size >= 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="ccbeb-162">**Mínimo**</span><span class="sxs-lookup"><span data-stu-id="ccbeb-162">**Minimal**</span></span> |
| <span data-ttu-id="ccbeb-163">Índice columnstore clusterizado</span><span class="sxs-lookup"><span data-stu-id="ccbeb-163">Clustered Columnstore Index</span></span> |<span data-ttu-id="ccbeb-164">Tamanho do lote < 102.400 por distribuição alinhada por partição</span><span class="sxs-lookup"><span data-stu-id="ccbeb-164">Batch size < 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="ccbeb-165">Completo</span><span class="sxs-lookup"><span data-stu-id="ccbeb-165">Full</span></span> |

<span data-ttu-id="ccbeb-166">Vale a pena observar que os índices secundários ou não clusterizado tooupdate sempre será totalmente gravações operações registradas.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-166">It is worth noting that any writes tooupdate secondary or non-clustered indexes will always be fully logged operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ccbeb-167">O SQL Data Warehouse possui 60 distribuições.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-167">SQL Data Warehouse has 60 distributions.</span></span> <span data-ttu-id="ccbeb-168">Por isso, supondo que todas as linhas são distribuídas uniformemente e inicial em uma única partição, o lote será necessário toocontain 6,144,000 linhas ou toobe maior minimamente registradas durante a gravação tooa índice Columnstore clusterizado.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-168">Therefore, assuming all rows are evenly distributed and landing in a single partition, your batch will need toocontain 6,144,000 rows or larger toobe minimally logged when writing tooa Clustered Columnstore Index.</span></span> <span data-ttu-id="ccbeb-169">Se Olá tabela está particionada e linhas de saudação inseridas span limites de partição, você precisará 6,144,000 linhas por limite de partição, supondo que até mesmo a distribuição de dados.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-169">If hello table is partitioned and hello rows being inserted span partition boundaries, then you will need 6,144,000 rows per partition boundary assuming even data distribution.</span></span> <span data-ttu-id="ccbeb-170">Cada partição em cada distribuição independentemente deve exceder o limite de linha 102.400 Olá para Olá insert toobe minimamente em distribuição de saudação.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-170">Each partition in each distribution must independently exceed hello 102,400 row threshold for hello insert toobe minimally logged into hello distribution.</span></span>
> 
> 

<span data-ttu-id="ccbeb-171">Carregar dados em uma tabela não vazia com um índice clusterizado pode, muitas vezes, conter uma combinação de linhas total e minimamente registradas em log.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-171">Loading data into a non-empty table with a clustered index can often contain a mixture of fully logged and minimally logged rows.</span></span> <span data-ttu-id="ccbeb-172">Um índice clusterizado é uma árvore balanceada (árvore b) das páginas.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-172">A clustered index is a balanced tree (b-tree) of pages.</span></span> <span data-ttu-id="ccbeb-173">Se a página de hello está sendo gravada tooalready contém linhas de outra transação, em seguida, essas gravações serão totalmente registradas.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-173">If hello page being written tooalready contains rows from another transaction, then these writes will be fully logged.</span></span> <span data-ttu-id="ccbeb-174">No entanto, se a página de saudação está vazia, em seguida, página de toothat de gravação de saudação será minimamente registrada.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-174">However, if hello page is empty then hello write toothat page will be minimally logged.</span></span>

## <a name="optimizing-deletes"></a><span data-ttu-id="ccbeb-175">Otimizando exclusões</span><span class="sxs-lookup"><span data-stu-id="ccbeb-175">Optimizing deletes</span></span>
<span data-ttu-id="ccbeb-176">`DELETE` é uma operação totalmente registrada em log.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-176">`DELETE` is a fully logged operation.</span></span>  <span data-ttu-id="ccbeb-177">Se você precisar toodelete uma grande quantidade de dados em uma tabela ou uma partição, geralmente faz mais sentido muito`SELECT` dados saudação desejar tookeep, que pode ser executado como uma operação minimamente registrada.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-177">If you need toodelete a large amount of data in a table or a partition, it often makes more sense too`SELECT` hello data you wish tookeep, which can be run as a minimally logged operation.</span></span>  <span data-ttu-id="ccbeb-178">tooaccomplish isso, crie uma nova tabela com [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="ccbeb-178">tooaccomplish this, create a new table with [CTAS][CTAS].</span></span>  <span data-ttu-id="ccbeb-179">Depois de criar, usar [RENOMEAR] [ RENAME] tooswap sua tabela antiga com tabela Olá recém-criado.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-179">Once created, use [RENAME][RENAME] tooswap out your old table with hello newly created table.</span></span>

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

## <a name="optimizing-updates"></a><span data-ttu-id="ccbeb-180">Otimizando atualizações</span><span class="sxs-lookup"><span data-stu-id="ccbeb-180">Optimizing updates</span></span>
<span data-ttu-id="ccbeb-181">`UPDATE` é uma operação totalmente registrada em log.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-181">`UPDATE` is a fully logged operation.</span></span>  <span data-ttu-id="ccbeb-182">Se você precisar tooupdate um grande número de linhas em uma tabela ou uma partição geralmente pode ser muito mais eficiente toouse uma operação minimamente registrada como [CTAS] [ CTAS] toodo para.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-182">If you need tooupdate a large number of rows in a table or a partition it can often be far more efficient toouse a minimally logged operation such as [CTAS][CTAS] toodo so.</span></span>

<span data-ttu-id="ccbeb-183">No hello exemplo abaixo de uma atualização de tabela completa foi convertido tooa `CTAS` para que o log mínimo é possível.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-183">In hello example below a full table update has been converted tooa `CTAS` so that minimal logging is possible.</span></span>

<span data-ttu-id="ccbeb-184">Nesse caso retrospectively estamos adicionando um desconto quantidade toohello de vendas na tabela de saudação:</span><span class="sxs-lookup"><span data-stu-id="ccbeb-184">In this case we are retrospectively adding a discount amount toohello sales in hello table:</span></span>

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
> <span data-ttu-id="ccbeb-185">A recriação de tabelas grandes pode se beneficiar do uso de recursos de gerenciamento de carga de trabalho do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-185">Re-creating large tables can benefit from using SQL Data Warehouse workload management features.</span></span> <span data-ttu-id="ccbeb-186">Para mais detalhes, consulte a seção de gerenciamento de carga de trabalho toohello em Olá [simultaneidade] [ concurrency] artigo.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-186">For more details please refer toohello workload management section in hello [concurrency][concurrency] article.</span></span>
> 
> 

## <a name="optimizing-with-partition-switching"></a><span data-ttu-id="ccbeb-187">Otimizando com alternância de partição</span><span class="sxs-lookup"><span data-stu-id="ccbeb-187">Optimizing with partition switching</span></span>
<span data-ttu-id="ccbeb-188">Quando houver modificações em larga escala dentro de uma [partição da tabela][table partition], fará mais sentido considerar um padrão de troca de partições.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-188">When faced with large scale modifications inside a [table partition][table partition], then a partition switching pattern makes a lot of sense.</span></span> <span data-ttu-id="ccbeb-189">Se hello modificação de dados é significativa e abrange várias partições, simplesmente iteração sobre partições Olá alcança Olá mesmo resultado.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-189">If hello data modification is significant and spans multiple partitions, then simply iterating over hello partitions achieves hello same result.</span></span>

<span data-ttu-id="ccbeb-190">Olá etapas tooperform uma alternância de partição são da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="ccbeb-190">hello steps tooperform a partition switch are as follows:</span></span>

1. <span data-ttu-id="ccbeb-191">Criar uma partição de saída vazia</span><span class="sxs-lookup"><span data-stu-id="ccbeb-191">Create an empty out partition</span></span>
2. <span data-ttu-id="ccbeb-192">Executar 'update' hello como um CTAS</span><span class="sxs-lookup"><span data-stu-id="ccbeb-192">Perform hello 'update' as a CTAS</span></span>
3. <span data-ttu-id="ccbeb-193">Olá toohello existente de dados tabela de extração</span><span class="sxs-lookup"><span data-stu-id="ccbeb-193">Switch out hello existing data toohello out table</span></span>
4. <span data-ttu-id="ccbeb-194">Inserir novos dados de saudação</span><span class="sxs-lookup"><span data-stu-id="ccbeb-194">Switch in hello new data</span></span>
5. <span data-ttu-id="ccbeb-195">Limpar dados saudação</span><span class="sxs-lookup"><span data-stu-id="ccbeb-195">Clean up hello data</span></span>

<span data-ttu-id="ccbeb-196">No entanto, toohelp identificar Olá partições tooswitch primeiro precisaremos toobuild um procedimento auxiliar como Olá um abaixo.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-196">However, toohelp identify hello partitions tooswitch we will first need toobuild a helper procedure such as hello one below.</span></span> 

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

<span data-ttu-id="ccbeb-197">Esse procedimento maximiza a reutilização de código e mantém o exemplo mais compacto de comutação de partição hello.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-197">This procedure maximizes code re-use and keeps hello partition switching example more compact.</span></span>

<span data-ttu-id="ccbeb-198">Olá código a seguir demonstra as cinco etapas de saudação mencionados acima tooachieve uma rotina de comutação de partição completa.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-198">hello code below demonstrates hello five steps mentioned above tooachieve a full partition switching routine.</span></span>

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

## <a name="minimize-logging-with-small-batches"></a><span data-ttu-id="ccbeb-199">Minimizar o registro em log com pequenos lotes</span><span class="sxs-lookup"><span data-stu-id="ccbeb-199">Minimize logging with small batches</span></span>
<span data-ttu-id="ccbeb-200">Para operações de modificação de dados grandes, poderá executar operação de saudação de toodivide sentido em partes ou lotes tooscope Olá a unidade de trabalho.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-200">For large data modification operations, it may make sense toodivide hello operation into chunks or batches tooscope hello unit of work.</span></span>

<span data-ttu-id="ccbeb-201">Um exemplo funcional é fornecido abaixo.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-201">A working example is provided below.</span></span> <span data-ttu-id="ccbeb-202">tamanho do lote Olá definiu trivial técnica número Olá de toohighlight tooa.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-202">hello batch size has been set tooa trivial number toohighlight hello technique.</span></span> <span data-ttu-id="ccbeb-203">Na realidade, tamanho de lote de saudação seria significativamente maior.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-203">In reality hello batch size would be significantly larger.</span></span> 

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

## <a name="pause-and-scaling-guidance"></a><span data-ttu-id="ccbeb-204">Diretrizes de pausa e dimensionamento</span><span class="sxs-lookup"><span data-stu-id="ccbeb-204">Pause and scaling guidance</span></span>
<span data-ttu-id="ccbeb-205">O SQL Data Warehouse do Azure permite pausar, retomar e dimensionar seu data warehouse sob demanda.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-205">Azure SQL Data Warehouse lets you pause, resume and scale your data warehouse on demand.</span></span> <span data-ttu-id="ccbeb-206">Quando você pausa ou dimensionar seu SQL Data Warehouse é toounderstand importante que todas as transações em andamento serão encerradas imediatamente; fazendo com que quaisquer transações abertas toobe revertida.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-206">When you pause or scale your SQL Data Warehouse it is important toounderstand that any in-flight transactions are terminated immediately; causing any open transactions toobe rolled back.</span></span> <span data-ttu-id="ccbeb-207">Se sua carga de trabalho tinha emitido uma longa duração e a modificação de dados incompletos anterior toohello pausar ou operação de expansão, esse trabalho será necessário toobe desfeita.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-207">If your workload had issued a long running and incomplete data modification prior toohello pause or scale operation, then this work will need toobe undone.</span></span> <span data-ttu-id="ccbeb-208">Isso pode afetar Olá tempo toopause ou dimensionar seu banco de dados do Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-208">This may impact hello time it takes toopause or scale your Azure SQL Data Warehouse database.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ccbeb-209">As operações `UPDATE` e `DELETE` são totalmente registradas em log e, portanto, essas operações de desfazer/refazer podem demorar significativamente mais do que as operações equivalentes minimamente registradas em log.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-209">Both `UPDATE` and `DELETE` are fully logged operations and so these undo/redo operations can take significantly longer than equivalent minimally logged operations.</span></span> 
> 
> 

<span data-ttu-id="ccbeb-210">cenário de melhor Olá é toolet em voo dados modificação transações completa anterior toopausing ou escala SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-210">hello best scenario is toolet in flight data modification transactions complete prior toopausing or scaling SQL Data Warehouse.</span></span> <span data-ttu-id="ccbeb-211">No entanto, isso pode não sempre ser prático.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-211">However, this may not always be practical.</span></span> <span data-ttu-id="ccbeb-212">risco de saudação toomitigate de reversão longo, considere uma das Olá as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="ccbeb-212">toomitigate hello risk of a long rollback, consider one of hello following options:</span></span>

* <span data-ttu-id="ccbeb-213">Gravar novamente as operações de longa duração usando [CTAS][CTAS]</span><span class="sxs-lookup"><span data-stu-id="ccbeb-213">Re-write long running operations using [CTAS][CTAS]</span></span>
* <span data-ttu-id="ccbeb-214">Operação de saudação são divididos nas partes; operando em um subconjunto de linhas de saudação</span><span class="sxs-lookup"><span data-stu-id="ccbeb-214">Break hello operation down into chunks; operating on a subset of hello rows</span></span>

## <a name="next-steps"></a><span data-ttu-id="ccbeb-215">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ccbeb-215">Next steps</span></span>
<span data-ttu-id="ccbeb-216">Consulte [transações no SQL Data Warehouse] [ Transactions in SQL Data Warehouse] toolearn mais sobre níveis de isolamento e limites transacionais.</span><span class="sxs-lookup"><span data-stu-id="ccbeb-216">See [Transactions in SQL Data Warehouse][Transactions in SQL Data Warehouse] toolearn more about isolation levels and transactional limits.</span></span>  <span data-ttu-id="ccbeb-217">Para obter uma visão geral de outras práticas recomendadas, confira [Práticas recomendadas para o Azure SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="ccbeb-217">For an overview of other Best Practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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

