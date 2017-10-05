---
title: "Otimização de transações para o SQL Data Warehouse | Microsoft Docs"
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
ms.openlocfilehash: f9f19d75a37351b3562ce8c2f3629df14c5437c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="optimizing-transactions-for-sql-data-warehouse"></a><span data-ttu-id="12c69-103">Otimização de transações para o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="12c69-103">Optimizing transactions for SQL Data Warehouse</span></span>
<span data-ttu-id="12c69-104">Este artigo explica como otimizar o desempenho do seu código transacional ao minimizar o risco para reversões longas.</span><span class="sxs-lookup"><span data-stu-id="12c69-104">This article explains how to optimize the performance of your transactional code while minimizing risk for long rollbacks.</span></span>

## <a name="transactions-and-logging"></a><span data-ttu-id="12c69-105">Transações e registro em log</span><span class="sxs-lookup"><span data-stu-id="12c69-105">Transactions and logging</span></span>
<span data-ttu-id="12c69-106">As transações são um componente importante de um mecanismo de banco de dados relacional.</span><span class="sxs-lookup"><span data-stu-id="12c69-106">Transactions are an important component of a relational database engine.</span></span> <span data-ttu-id="12c69-107">O SQL Data Warehouse usa transações durante a modificação de dados.</span><span class="sxs-lookup"><span data-stu-id="12c69-107">SQL Data Warehouse uses transactions during data modification.</span></span> <span data-ttu-id="12c69-108">Essas transações podem ser implícitas ou explícitas.</span><span class="sxs-lookup"><span data-stu-id="12c69-108">These transactions can be explicit or implicit.</span></span> <span data-ttu-id="12c69-109">As instruções individuais `INSERT`, `UPDATE` e `DELETE` são exemplos de transações implícitas.</span><span class="sxs-lookup"><span data-stu-id="12c69-109">Single `INSERT`, `UPDATE` and `DELETE` statements are all examples of implicit transactions.</span></span> <span data-ttu-id="12c69-110">As transações explícitas são escritas explicitamente por um desenvolvedor usando `BEGIN TRAN`, `COMMIT TRAN` ou `ROLLBACK TRAN` e costumam ser usadas quando é preciso agrupar várias instruções de modificação em uma única unidade atômica.</span><span class="sxs-lookup"><span data-stu-id="12c69-110">Explicit transactions are written explicitly by a developer using `BEGIN TRAN`, `COMMIT TRAN` or `ROLLBACK TRAN` and are typically used when multiple modification statements need to be tied together in a single atomic unit.</span></span> 

<span data-ttu-id="12c69-111">O SQL Data Warehouse do Azure confirma as alterações no banco de dados usando os logs de transação.</span><span class="sxs-lookup"><span data-stu-id="12c69-111">Azure SQL Data Warehouse commits changes to the database using transaction logs.</span></span> <span data-ttu-id="12c69-112">Cada distribuição tem seu próprio log de transações.</span><span class="sxs-lookup"><span data-stu-id="12c69-112">Each distribution has its own transaction log.</span></span> <span data-ttu-id="12c69-113">As gravações de log de transações são automáticas.</span><span class="sxs-lookup"><span data-stu-id="12c69-113">Transaction log writes are automatic.</span></span> <span data-ttu-id="12c69-114">Não é necessária nenhuma configuração.</span><span class="sxs-lookup"><span data-stu-id="12c69-114">There is no configuration required.</span></span> <span data-ttu-id="12c69-115">No entanto, apesar desse processo garantir a gravação, ele introduz uma sobrecarga no sistema.</span><span class="sxs-lookup"><span data-stu-id="12c69-115">However, whilst this process guarantees the write it does introduce an overhead in the system.</span></span> <span data-ttu-id="12c69-116">Você pode minimizar esse impacto ao escrever um código transacionalmente eficiente.</span><span class="sxs-lookup"><span data-stu-id="12c69-116">You can minimize this impact by writing transactionally efficient code.</span></span> <span data-ttu-id="12c69-117">De modo geral, um código transacionalmente eficiente se enquadra em duas categorias.</span><span class="sxs-lookup"><span data-stu-id="12c69-117">Transactionally efficient code broadly falls into two categories.</span></span>

* <span data-ttu-id="12c69-118">Aproveitar constructos mínimos de registro em log quando possível</span><span class="sxs-lookup"><span data-stu-id="12c69-118">Leverage minimal logging constructs where possible</span></span>
* <span data-ttu-id="12c69-119">Processar dados usando lotes com escopo para evitar transações de longa execução singulares</span><span class="sxs-lookup"><span data-stu-id="12c69-119">Process data using scoped batches to avoid singular long running transactions</span></span>
* <span data-ttu-id="12c69-120">Adotar um padrão de alternância de partições para grandes modificações de uma determinada partição</span><span class="sxs-lookup"><span data-stu-id="12c69-120">Adopt a partition switching pattern for large modifications to a given partition</span></span>

## <a name="minimal-vs-full-logging"></a><span data-ttu-id="12c69-121">Registro mínimo em log vs. registro total em log</span><span class="sxs-lookup"><span data-stu-id="12c69-121">Minimal vs. full logging</span></span>
<span data-ttu-id="12c69-122">Ao contrário de operações totalmente registradas em log, que usam o log de transações para acompanhar cada linha alterada, as operações minimamente registradas em log controlam apenas as alocações de extensão e as alterações de metadados.</span><span class="sxs-lookup"><span data-stu-id="12c69-122">Unlike fully logged operations, which use the transaction log to keep track of every row change, minimally logged operations keep track of extent allocations and meta-data changes only.</span></span> <span data-ttu-id="12c69-123">Portanto, o registro mínimo em log só envolve o registro das informações necessárias para reverter a transação no caso de uma falha ou de uma solicitação explícita (`ROLLBACK TRAN`).</span><span class="sxs-lookup"><span data-stu-id="12c69-123">Therefore, minimal logging involves logging only the information that is required to rollback the transaction in the event of a failure or an explicit request (`ROLLBACK TRAN`).</span></span> <span data-ttu-id="12c69-124">Como muito menos informações são rastreadas no log de transações, uma operação minimamente registrada em log tem um desempenho melhor do que uma operação totalmente registrada em log de tamanho similar.</span><span class="sxs-lookup"><span data-stu-id="12c69-124">As much less information is tracked in the transaction log, a minimally logged operation performs better than a similarly sized fully logged operation.</span></span> <span data-ttu-id="12c69-125">Além disso, como ocorrem menos gravações no log de transações, uma quantidade menor de dados de log será gerada e, portanto, é mais eficiente em relação à E/S.</span><span class="sxs-lookup"><span data-stu-id="12c69-125">Furthermore, because fewer writes go the transaction log, a much smaller amount of log data is generated and so is more I/O efficient.</span></span>

<span data-ttu-id="12c69-126">Os limites de segurança de transação só se aplicam às operações totalmente registradas em log.</span><span class="sxs-lookup"><span data-stu-id="12c69-126">The transaction safety limits only apply to fully logged operations.</span></span>

> [!NOTE]
> <span data-ttu-id="12c69-127">As operações minimamente registradas em log podem participar de transações explícitas.</span><span class="sxs-lookup"><span data-stu-id="12c69-127">Minimally logged operations can participate in explicit transactions.</span></span> <span data-ttu-id="12c69-128">Como todas as alterações nas estruturas de alocação são rastreadas, é possível reverter operações minimamente registradas em log.</span><span class="sxs-lookup"><span data-stu-id="12c69-128">As all changes in allocation structures are tracked, it is possible to roll back minimally logged operations.</span></span> <span data-ttu-id="12c69-129">É importante entender que a alteração é registrada "minimamente" em log, ou seja, não tem o log cancelado.</span><span class="sxs-lookup"><span data-stu-id="12c69-129">It is important to understand that the change is "minimally" logged it is not un-logged.</span></span>
> 
> 

## <a name="minimally-logged-operations"></a><span data-ttu-id="12c69-130">Operações minimamente registradas em log</span><span class="sxs-lookup"><span data-stu-id="12c69-130">Minimally logged operations</span></span>
<span data-ttu-id="12c69-131">As seguintes operações podem ser minimamente registradas em log:</span><span class="sxs-lookup"><span data-stu-id="12c69-131">The following operations are capable of being minimally logged:</span></span>

* <span data-ttu-id="12c69-132">CREATE TABLE AS SELECT ([CTAS][CTAS])</span><span class="sxs-lookup"><span data-stu-id="12c69-132">CREATE TABLE AS SELECT ([CTAS][CTAS])</span></span>
* <span data-ttu-id="12c69-133">INSERT..SELECT</span><span class="sxs-lookup"><span data-stu-id="12c69-133">INSERT..SELECT</span></span>
* <span data-ttu-id="12c69-134">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="12c69-134">CREATE INDEX</span></span>
* <span data-ttu-id="12c69-135">ALTER INDEX REBUILD</span><span class="sxs-lookup"><span data-stu-id="12c69-135">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="12c69-136">DROP INDEX</span><span class="sxs-lookup"><span data-stu-id="12c69-136">DROP INDEX</span></span>
* <span data-ttu-id="12c69-137">TRUNCATE TABLE</span><span class="sxs-lookup"><span data-stu-id="12c69-137">TRUNCATE TABLE</span></span>
* <span data-ttu-id="12c69-138">DROP TABLE</span><span class="sxs-lookup"><span data-stu-id="12c69-138">DROP TABLE</span></span>
* <span data-ttu-id="12c69-139">ALTER TABLE SWITCH PARTITION</span><span class="sxs-lookup"><span data-stu-id="12c69-139">ALTER TABLE SWITCH PARTITION</span></span>

<!--
- MERGE
- UPDATE on LOB Types .WRITE
- SELECT..INTO
-->

> [!NOTE]
> <span data-ttu-id="12c69-140">As operações de movimentação de dados internos (como `BROADCAST` e `SHUFFLE`) não são afetadas pelo limite de segurança de transação.</span><span class="sxs-lookup"><span data-stu-id="12c69-140">Internal data movement operations (such as `BROADCAST` and `SHUFFLE`) are not affected by the transaction safety limit.</span></span>
> 
> 

## <a name="minimal-logging-with-bulk-load"></a><span data-ttu-id="12c69-141">Registro mínimo em log com carregamento em massa</span><span class="sxs-lookup"><span data-stu-id="12c69-141">Minimal logging with bulk load</span></span>
<span data-ttu-id="12c69-142">`CTAS` e `INSERT...SELECT` são ambos operações de carregamento em massa.</span><span class="sxs-lookup"><span data-stu-id="12c69-142">`CTAS` and `INSERT...SELECT` are both bulk load operations.</span></span> <span data-ttu-id="12c69-143">No entanto, ambas são influenciadas pela definição da tabela de destino e dependem do cenário de carga.</span><span class="sxs-lookup"><span data-stu-id="12c69-143">However, both are influenced by the target table definition and depend on the load scenario.</span></span> <span data-ttu-id="12c69-144">A seguir, uma tabela que explica se a operação em massa será total ou minimamente registrada em log:</span><span class="sxs-lookup"><span data-stu-id="12c69-144">Below is a table that explains if your bulk operation will be fully or minimally logged:</span></span>  

| <span data-ttu-id="12c69-145">Índice principal</span><span class="sxs-lookup"><span data-stu-id="12c69-145">Primary Index</span></span> | <span data-ttu-id="12c69-146">Cenário de carga</span><span class="sxs-lookup"><span data-stu-id="12c69-146">Load Scenario</span></span> | <span data-ttu-id="12c69-147">Modo de registro em log</span><span class="sxs-lookup"><span data-stu-id="12c69-147">Logging Mode</span></span> |
| --- | --- | --- |
| <span data-ttu-id="12c69-148">Heap</span><span class="sxs-lookup"><span data-stu-id="12c69-148">Heap</span></span> |<span data-ttu-id="12c69-149">Qualquer</span><span class="sxs-lookup"><span data-stu-id="12c69-149">Any</span></span> |<span data-ttu-id="12c69-150">**Mínimo**</span><span class="sxs-lookup"><span data-stu-id="12c69-150">**Minimal**</span></span> |
| <span data-ttu-id="12c69-151">Índice clusterizado</span><span class="sxs-lookup"><span data-stu-id="12c69-151">Clustered Index</span></span> |<span data-ttu-id="12c69-152">Tabela de destino vazia</span><span class="sxs-lookup"><span data-stu-id="12c69-152">Empty target table</span></span> |<span data-ttu-id="12c69-153">**Mínimo**</span><span class="sxs-lookup"><span data-stu-id="12c69-153">**Minimal**</span></span> |
| <span data-ttu-id="12c69-154">Índice clusterizado</span><span class="sxs-lookup"><span data-stu-id="12c69-154">Clustered Index</span></span> |<span data-ttu-id="12c69-155">As linhas carregadas não se sobrepõem às páginas existentes no destino</span><span class="sxs-lookup"><span data-stu-id="12c69-155">Loaded rows do not overlap with existing pages in target</span></span> |<span data-ttu-id="12c69-156">**Mínimo**</span><span class="sxs-lookup"><span data-stu-id="12c69-156">**Minimal**</span></span> |
| <span data-ttu-id="12c69-157">Índice clusterizado</span><span class="sxs-lookup"><span data-stu-id="12c69-157">Clustered Index</span></span> |<span data-ttu-id="12c69-158">Linhas carregadas se sobrepõem com páginas existentes no destino</span><span class="sxs-lookup"><span data-stu-id="12c69-158">Loaded rows overlap with existing pages in target</span></span> |<span data-ttu-id="12c69-159">Completo</span><span class="sxs-lookup"><span data-stu-id="12c69-159">Full</span></span> |
| <span data-ttu-id="12c69-160">Índice columnstore clusterizado</span><span class="sxs-lookup"><span data-stu-id="12c69-160">Clustered Columnstore Index</span></span> |<span data-ttu-id="12c69-161">Tamanho do lote >= 102.400 por distribuição alinhada por partição</span><span class="sxs-lookup"><span data-stu-id="12c69-161">Batch size >= 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="12c69-162">**Mínimo**</span><span class="sxs-lookup"><span data-stu-id="12c69-162">**Minimal**</span></span> |
| <span data-ttu-id="12c69-163">Índice columnstore clusterizado</span><span class="sxs-lookup"><span data-stu-id="12c69-163">Clustered Columnstore Index</span></span> |<span data-ttu-id="12c69-164">Tamanho do lote < 102.400 por distribuição alinhada por partição</span><span class="sxs-lookup"><span data-stu-id="12c69-164">Batch size < 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="12c69-165">Completo</span><span class="sxs-lookup"><span data-stu-id="12c69-165">Full</span></span> |

<span data-ttu-id="12c69-166">Vale a pena observar que todas as gravações para atualizar índices secundários ou não clusterizados sempre serão operações com log completo.</span><span class="sxs-lookup"><span data-stu-id="12c69-166">It is worth noting that any writes to update secondary or non-clustered indexes will always be fully logged operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="12c69-167">O SQL Data Warehouse possui 60 distribuições.</span><span class="sxs-lookup"><span data-stu-id="12c69-167">SQL Data Warehouse has 60 distributions.</span></span> <span data-ttu-id="12c69-168">Portanto, supondo que todas as linhas são distribuídas uniformemente e em uma única partição, o seu lote deverá conter 6.144.000 linhas ou mais para ser minimamente registrado ao gravar em um Índice Columnstore Clusterizado.</span><span class="sxs-lookup"><span data-stu-id="12c69-168">Therefore, assuming all rows are evenly distributed and landing in a single partition, your batch will need to contain 6,144,000 rows or larger to be minimally logged when writing to a Clustered Columnstore Index.</span></span> <span data-ttu-id="12c69-169">Se a tabela estiver particionada e as linhas que estiverem sendo inseridas se estenderem pelos limites de partição, você precisará de 6.144.000 linhas por limite de partição, considerando uma distribuição uniforme de dados.</span><span class="sxs-lookup"><span data-stu-id="12c69-169">If the table is partitioned and the rows being inserted span partition boundaries, then you will need 6,144,000 rows per partition boundary assuming even data distribution.</span></span> <span data-ttu-id="12c69-170">Cada partição em cada distribuição deve exceder independentemente o limite de 102.400 linhas para a inserção ser minimamente registrada em log para a distribuição.</span><span class="sxs-lookup"><span data-stu-id="12c69-170">Each partition in each distribution must independently exceed the 102,400 row threshold for the insert to be minimally logged into the distribution.</span></span>
> 
> 

<span data-ttu-id="12c69-171">Carregar dados em uma tabela não vazia com um índice clusterizado pode, muitas vezes, conter uma combinação de linhas total e minimamente registradas em log.</span><span class="sxs-lookup"><span data-stu-id="12c69-171">Loading data into a non-empty table with a clustered index can often contain a mixture of fully logged and minimally logged rows.</span></span> <span data-ttu-id="12c69-172">Um índice clusterizado é uma árvore balanceada (árvore b) das páginas.</span><span class="sxs-lookup"><span data-stu-id="12c69-172">A clustered index is a balanced tree (b-tree) of pages.</span></span> <span data-ttu-id="12c69-173">Se a página que estiver sendo gravada já contiver linhas de outra transação, então essas gravações serão totalmente registradas em log.</span><span class="sxs-lookup"><span data-stu-id="12c69-173">If the page being written to already contains rows from another transaction, then these writes will be fully logged.</span></span> <span data-ttu-id="12c69-174">No entanto, se a página estiver vazia, a gravação para essa página será minimamente registrada em log.</span><span class="sxs-lookup"><span data-stu-id="12c69-174">However, if the page is empty then the write to that page will be minimally logged.</span></span>

## <a name="optimizing-deletes"></a><span data-ttu-id="12c69-175">Otimizando exclusões</span><span class="sxs-lookup"><span data-stu-id="12c69-175">Optimizing deletes</span></span>
<span data-ttu-id="12c69-176">`DELETE` é uma operação totalmente registrada em log.</span><span class="sxs-lookup"><span data-stu-id="12c69-176">`DELETE` is a fully logged operation.</span></span>  <span data-ttu-id="12c69-177">Se você precisar excluir uma grande quantidade de dados de uma tabela ou uma partição, geralmente fará mais sentido `SELECT` (selecionar) os dados que deseja manter, que podem ser executados como uma operação minimamente registrada em log.</span><span class="sxs-lookup"><span data-stu-id="12c69-177">If you need to delete a large amount of data in a table or a partition, it often makes more sense to `SELECT` the data you wish to keep, which can be run as a minimally logged operation.</span></span>  <span data-ttu-id="12c69-178">Para isso, crie uma nova tabela com [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="12c69-178">To accomplish this, create a new table with [CTAS][CTAS].</span></span>  <span data-ttu-id="12c69-179">Depois de criada, use [RENAME][RENAME] para alternar sua tabela antiga com a recentemente criada.</span><span class="sxs-lookup"><span data-stu-id="12c69-179">Once created, use [RENAME][RENAME] to swap out your old table with the newly created table.</span></span>

```sql
-- Delete all sales transactions for Promotions except PromotionKey 2.

--Step 01. Create a new table select only the records we want to kep (PromotionKey 2)
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

--Step 02. Rename the Tables to replace the 
RENAME OBJECT [dbo].[FactInternetSales]   TO [FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_d] TO [FactInternetSales];
```

## <a name="optimizing-updates"></a><span data-ttu-id="12c69-180">Otimizando atualizações</span><span class="sxs-lookup"><span data-stu-id="12c69-180">Optimizing updates</span></span>
<span data-ttu-id="12c69-181">`UPDATE` é uma operação totalmente registrada em log.</span><span class="sxs-lookup"><span data-stu-id="12c69-181">`UPDATE` is a fully logged operation.</span></span>  <span data-ttu-id="12c69-182">Se você precisar atualizar um grande número de linhas em uma tabela ou em uma partição, no geral, poderá ser muito mais proveitoso usar uma operação minimamente registrada em log, tal como [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="12c69-182">If you need to update a large number of rows in a table or a partition it can often be far more efficient to use a minimally logged operation such as [CTAS][CTAS] to do so.</span></span>

<span data-ttu-id="12c69-183">No exemplo abaixo, uma atualização completa de tabela foi convertida em um `CTAS` para permitir o registro mínimo em log.</span><span class="sxs-lookup"><span data-stu-id="12c69-183">In the example below a full table update has been converted to a `CTAS` so that minimal logging is possible.</span></span>

<span data-ttu-id="12c69-184">Nesse caso, adiciona-se retrospectivamente um valor de desconto às vendas na tabela:</span><span class="sxs-lookup"><span data-stu-id="12c69-184">In this case we are retrospectively adding a discount amount to the sales in the table:</span></span>

```sql
--Step 01. Create a new table containing the "Update". 
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

--Step 02. Rename the tables
RENAME OBJECT [dbo].[FactInternetSales]   TO [FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_u] TO [FactInternetSales];

--Step 03. Drop the old table
DROP TABLE [dbo].[FactInternetSales_old]
```

> [!NOTE]
> <span data-ttu-id="12c69-185">A recriação de tabelas grandes pode se beneficiar do uso de recursos de gerenciamento de carga de trabalho do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="12c69-185">Re-creating large tables can benefit from using SQL Data Warehouse workload management features.</span></span> <span data-ttu-id="12c69-186">Para obter mais detalhes, confira a seção de gerenciamento de carga de trabalho no artigo sobre [simultaneidade][concurrency].</span><span class="sxs-lookup"><span data-stu-id="12c69-186">For more details please refer to the workload management section in the [concurrency][concurrency] article.</span></span>
> 
> 

## <a name="optimizing-with-partition-switching"></a><span data-ttu-id="12c69-187">Otimizando com alternância de partição</span><span class="sxs-lookup"><span data-stu-id="12c69-187">Optimizing with partition switching</span></span>
<span data-ttu-id="12c69-188">Quando houver modificações em larga escala dentro de uma [partição da tabela][table partition], fará mais sentido considerar um padrão de troca de partições.</span><span class="sxs-lookup"><span data-stu-id="12c69-188">When faced with large scale modifications inside a [table partition][table partition], then a partition switching pattern makes a lot of sense.</span></span> <span data-ttu-id="12c69-189">Se a modificação de dados for significativa e se estender por várias partições, a simples iteração nas partições terá o mesmo resultado.</span><span class="sxs-lookup"><span data-stu-id="12c69-189">If the data modification is significant and spans multiple partitions, then simply iterating over the partitions achieves the same result.</span></span>

<span data-ttu-id="12c69-190">As etapas para executar uma alternância de partições são as seguintes:</span><span class="sxs-lookup"><span data-stu-id="12c69-190">The steps to perform a partition switch are as follows:</span></span>

1. <span data-ttu-id="12c69-191">Criar uma partição de saída vazia</span><span class="sxs-lookup"><span data-stu-id="12c69-191">Create an empty out partition</span></span>
2. <span data-ttu-id="12c69-192">Executar a “atualização” como um CTAS</span><span class="sxs-lookup"><span data-stu-id="12c69-192">Perform the 'update' as a CTAS</span></span>
3. <span data-ttu-id="12c69-193">Alternar os dados existentes na tabela de saída</span><span class="sxs-lookup"><span data-stu-id="12c69-193">Switch out the existing data to the out table</span></span>
4. <span data-ttu-id="12c69-194">Inserir os novos dados</span><span class="sxs-lookup"><span data-stu-id="12c69-194">Switch in the new data</span></span>
5. <span data-ttu-id="12c69-195">Limpar os dados</span><span class="sxs-lookup"><span data-stu-id="12c69-195">Clean up the data</span></span>

<span data-ttu-id="12c69-196">No entanto, para ajudar a identificar as partições a serem alternadas, primeiro precisamos criar um procedimento auxiliar, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="12c69-196">However, to help identify the partitions to switch we will first need to build a helper procedure such as the one below.</span></span> 

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

<span data-ttu-id="12c69-197">Esse procedimento maximiza a reutilização de código e deixa o exemplo de alternância de partições mais compacto.</span><span class="sxs-lookup"><span data-stu-id="12c69-197">This procedure maximizes code re-use and keeps the partition switching example more compact.</span></span>

<span data-ttu-id="12c69-198">O código a seguir demonstra as cinco etapas mencionadas acima para obter uma rotina de alternância de partições completa.</span><span class="sxs-lookup"><span data-stu-id="12c69-198">The code below demonstrates the five steps mentioned above to achieve a full partition switching routine.</span></span>

```sql
--Create a partitioned aligned empty table to switch out the data 
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

--Create a partitioned aligned table and update the data in the select portion of the CTAS
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

--Use the helper procedure to identify the partitions
--The source table
EXEC dbo.partition_data_get 'dbo','FactInternetSales',20030101
DECLARE @ptn_nmbr_src INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_src

--The "in" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_in',20030101
DECLARE @ptn_nmbr_in INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_in

--The "out" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_out',20030101
DECLARE @ptn_nmbr_out INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_out

--Switch the partitions over
DECLARE @SQL NVARCHAR(4000) = '
ALTER TABLE [dbo].[FactInternetSales]    SWITCH PARTITION '+CAST(@ptn_nmbr_src AS VARCHAR(20))    +' TO [dbo].[FactInternetSales_out] PARTITION '    +CAST(@ptn_nmbr_out AS VARCHAR(20))+';
ALTER TABLE [dbo].[FactInternetSales_in] SWITCH PARTITION '+CAST(@ptn_nmbr_in AS VARCHAR(20))    +' TO [dbo].[FactInternetSales] PARTITION '        +CAST(@ptn_nmbr_src AS VARCHAR(20))+';'
EXEC sp_executesql @SQL

--Perform the clean-up
TRUNCATE TABLE dbo.FactInternetSales_out;
TRUNCATE TABLE dbo.FactInternetSales_in;

DROP TABLE dbo.FactInternetSales_out
DROP TABLE dbo.FactInternetSales_in
DROP TABLE #ptn_data
```

## <a name="minimize-logging-with-small-batches"></a><span data-ttu-id="12c69-199">Minimizar o registro em log com pequenos lotes</span><span class="sxs-lookup"><span data-stu-id="12c69-199">Minimize logging with small batches</span></span>
<span data-ttu-id="12c69-200">Para grandes operações de modificação de dados, talvez faça sentido dividir a operação em partes ou em lotes para abranger a unidade de trabalho.</span><span class="sxs-lookup"><span data-stu-id="12c69-200">For large data modification operations, it may make sense to divide the operation into chunks or batches to scope the unit of work.</span></span>

<span data-ttu-id="12c69-201">Um exemplo funcional é fornecido abaixo.</span><span class="sxs-lookup"><span data-stu-id="12c69-201">A working example is provided below.</span></span> <span data-ttu-id="12c69-202">O tamanho do lote foi definido como um número trivial para realçar a técnica.</span><span class="sxs-lookup"><span data-stu-id="12c69-202">The batch size has been set to a trivial number to highlight the technique.</span></span> <span data-ttu-id="12c69-203">Na realidade, o tamanho do lote seria significativamente maior.</span><span class="sxs-lookup"><span data-stu-id="12c69-203">In reality the batch size would be significantly larger.</span></span> 

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

## <a name="pause-and-scaling-guidance"></a><span data-ttu-id="12c69-204">Diretrizes de pausa e dimensionamento</span><span class="sxs-lookup"><span data-stu-id="12c69-204">Pause and scaling guidance</span></span>
<span data-ttu-id="12c69-205">O SQL Data Warehouse do Azure permite pausar, retomar e dimensionar seu data warehouse sob demanda.</span><span class="sxs-lookup"><span data-stu-id="12c69-205">Azure SQL Data Warehouse lets you pause, resume and scale your data warehouse on demand.</span></span> <span data-ttu-id="12c69-206">Quando você pausa ou dimensiona o SQL Data Warehouse, deve entender que todas as transações em trânsito serão encerradas imediatamente, fazendo com que qualquer transação aberta seja revertida.</span><span class="sxs-lookup"><span data-stu-id="12c69-206">When you pause or scale your SQL Data Warehouse it is important to understand that any in-flight transactions are terminated immediately; causing any open transactions to be rolled back.</span></span> <span data-ttu-id="12c69-207">Se sua carga de trabalho tiver emitido uma modificação de dados de longa duração e incompleta antes de a operação de dimensionamento ou pausa, o trabalho precisará ser desfeito.</span><span class="sxs-lookup"><span data-stu-id="12c69-207">If your workload had issued a long running and incomplete data modification prior to the pause or scale operation, then this work will need to be undone.</span></span> <span data-ttu-id="12c69-208">Isso pode afetar o tempo necessário para pausar ou dimensionar seu banco de dados do Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="12c69-208">This may impact the time it takes to pause or scale your Azure SQL Data Warehouse database.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="12c69-209">As operações `UPDATE` e `DELETE` são totalmente registradas em log e, portanto, essas operações de desfazer/refazer podem demorar significativamente mais do que as operações equivalentes minimamente registradas em log.</span><span class="sxs-lookup"><span data-stu-id="12c69-209">Both `UPDATE` and `DELETE` are fully logged operations and so these undo/redo operations can take significantly longer than equivalent minimally logged operations.</span></span> 
> 
> 

<span data-ttu-id="12c69-210">O melhor cenário é permitir que as transações de modificação de dados em trânsito sejam concluídas antes da pausa ou do dimensionamento do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="12c69-210">The best scenario is to let in flight data modification transactions complete prior to pausing or scaling SQL Data Warehouse.</span></span> <span data-ttu-id="12c69-211">No entanto, isso pode não sempre ser prático.</span><span class="sxs-lookup"><span data-stu-id="12c69-211">However, this may not always be practical.</span></span> <span data-ttu-id="12c69-212">Para reduzir o risco de uma longa reversão, considere uma das seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="12c69-212">To mitigate the risk of a long rollback, consider one of the following options:</span></span>

* <span data-ttu-id="12c69-213">Gravar novamente as operações de longa duração usando [CTAS][CTAS]</span><span class="sxs-lookup"><span data-stu-id="12c69-213">Re-write long running operations using [CTAS][CTAS]</span></span>
* <span data-ttu-id="12c69-214">Divida a operação em partes, trabalhando com um subconjunto de linhas</span><span class="sxs-lookup"><span data-stu-id="12c69-214">Break the operation down into chunks; operating on a subset of the rows</span></span>

## <a name="next-steps"></a><span data-ttu-id="12c69-215">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="12c69-215">Next steps</span></span>
<span data-ttu-id="12c69-216">Confira [Transações no SQL Data Warehouse][Transactions in SQL Data Warehouse] para saber mais sobre os níveis de isolamento e os limites transacionais.</span><span class="sxs-lookup"><span data-stu-id="12c69-216">See [Transactions in SQL Data Warehouse][Transactions in SQL Data Warehouse] to learn more about isolation levels and transactional limits.</span></span>  <span data-ttu-id="12c69-217">Para obter uma visão geral de outras práticas recomendadas, confira [Práticas recomendadas para o Azure SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="12c69-217">For an overview of other Best Practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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

