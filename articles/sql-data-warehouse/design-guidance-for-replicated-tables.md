---
title: diretrizes de aaaDesign para Azure SQL Data Warehouse de tabelas - replicadas | Microsoft Docs
description: "Recomendações para criar tabelas replicadas em seu esquema do SQL Data Warehouse do Azure."
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/14/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 5d405b8c404c65177b387ba959126839c1cf8799
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="design-guidance-for-using-replicated-tables-in-azure-sql-data-warehouse"></a><span data-ttu-id="6a4af-103">Diretrizes de design para usar tabelas replicadas no SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="6a4af-103">Design guidance for using replicated tables in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="6a4af-104">Este artigo fornece recomendações para criar tabelas replicadas no esquema do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6a4af-104">This article gives recommendations for designing replicated tables in your SQL Data Warehouse schema.</span></span> <span data-ttu-id="6a4af-105">Use o desempenho da consulta essas recomendações tooimprove, reduzindo a complexidade de consulta e de movimentação de dados.</span><span class="sxs-lookup"><span data-stu-id="6a4af-105">Use these recommendations tooimprove query performance by reducing data movement and query complexity.</span></span>

> [!NOTE]
> <span data-ttu-id="6a4af-106">recurso de tabela replicada Hello está atualmente em visualização pública.</span><span class="sxs-lookup"><span data-stu-id="6a4af-106">hello replicated table feature is currently in public preview.</span></span> <span data-ttu-id="6a4af-107">Alguns comportamentos são toochange de assunto.</span><span class="sxs-lookup"><span data-stu-id="6a4af-107">Some behaviors are subject toochange.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="6a4af-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6a4af-108">Prerequisites</span></span>
<span data-ttu-id="6a4af-109">Este artigo pressupõe que você esteja familiarizado com os conceitos de movimentação e distribuição de dados no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="6a4af-109">This article assumes you are familiar with data distribution and data movement concepts in SQL Data Warehouse.</span></span>  <span data-ttu-id="6a4af-110">Para obter mais informações, consulte [Dados distribuídos](sql-data-warehouse-distributed-data.md).</span><span class="sxs-lookup"><span data-stu-id="6a4af-110">For more information, see [Distributed data](sql-data-warehouse-distributed-data.md).</span></span> 

<span data-ttu-id="6a4af-111">Como parte do design de tabela, entenda tanto quanto possível sobre seus dados e como os dados de saudação são consultados.</span><span class="sxs-lookup"><span data-stu-id="6a4af-111">As part of table design, understand as much as possible about your data and how hello data is queried.</span></span>  <span data-ttu-id="6a4af-112">Por exemplo, considere estas perguntas:</span><span class="sxs-lookup"><span data-stu-id="6a4af-112">For example, consider these questions:</span></span>

- <span data-ttu-id="6a4af-113">O tamanho é Olá?</span><span class="sxs-lookup"><span data-stu-id="6a4af-113">How large is hello table?</span></span>   
- <span data-ttu-id="6a4af-114">A frequência de tabela Olá atualização?</span><span class="sxs-lookup"><span data-stu-id="6a4af-114">How often is hello table refreshed?</span></span>   
- <span data-ttu-id="6a4af-115">Há tabelas de dimensões e fatos no data warehouse?</span><span class="sxs-lookup"><span data-stu-id="6a4af-115">Do I have fact and dimension tables in a data warehouse?</span></span>   

## <a name="what-is-a-replicated-table"></a><span data-ttu-id="6a4af-116">O que é uma tabela replicada?</span><span class="sxs-lookup"><span data-stu-id="6a4af-116">What is a replicated table?</span></span>
<span data-ttu-id="6a4af-117">Uma tabela replicada tem uma cópia completa da tabela de saudação acessível em cada nó de computação.</span><span class="sxs-lookup"><span data-stu-id="6a4af-117">A replicated table has a full copy of hello table accessible on each Compute node.</span></span> <span data-ttu-id="6a4af-118">Duplicar uma tabela remove os dados de tootransfer de necessidade Olá entre nós de computação antes de uma junção ou agregação.</span><span class="sxs-lookup"><span data-stu-id="6a4af-118">Replicating a table removes hello need tootransfer data among Compute nodes before a join or aggregation.</span></span> <span data-ttu-id="6a4af-119">Como tabela de saudação tem várias cópias, tabelas replicadas funcionam melhor quando o tamanho da tabela Olá é menor que 2 GB compactado.</span><span class="sxs-lookup"><span data-stu-id="6a4af-119">Since hello table has multiple copies, replicated tables work best when hello table size is less than 2 GB compressed.</span></span>

<span data-ttu-id="6a4af-120">Olá diagrama a seguir mostra uma tabela replicada que é acessível em cada nó de computação.</span><span class="sxs-lookup"><span data-stu-id="6a4af-120">hello following diagram shows a replicated table that is accessible on each Compute node.</span></span> <span data-ttu-id="6a4af-121">No SQL Data Warehouse, tabela replicada Olá é tooa totalmente copiados o banco de dados de distribuição em cada nó de computação.</span><span class="sxs-lookup"><span data-stu-id="6a4af-121">In SQL Data Warehouse, hello replicated table is fully copied tooa distribution database on each Compute node.</span></span> 

<span data-ttu-id="6a4af-122">![Tabela replicada](media/guidance-for-using-replicated-tables/replicated-table.png "Tabela replicada")</span><span class="sxs-lookup"><span data-stu-id="6a4af-122">![Replicated table](media/guidance-for-using-replicated-tables/replicated-table.png "Replicated table")</span></span>  

<span data-ttu-id="6a4af-123">As tabelas replicadas funcionam bem nas tabelas de dimensões pequenas em um esquema em estrela.</span><span class="sxs-lookup"><span data-stu-id="6a4af-123">Replicated tables work well for small dimension tables in a star schema.</span></span> <span data-ttu-id="6a4af-124">Tabelas de dimensões são geralmente de um tamanho que torna mais viável toostore e mantêm várias cópias.</span><span class="sxs-lookup"><span data-stu-id="6a4af-124">Dimension tables are usually of a size that makes it feasible toostore and maintain multiple copies.</span></span> <span data-ttu-id="6a4af-125">As dimensões armazenam dados descritivos que são alterados lentamente, como nome e endereço do cliente e detalhes do produto.</span><span class="sxs-lookup"><span data-stu-id="6a4af-125">Dimensions store descriptive data that changes slowly, such as customer name and address, and product details.</span></span> <span data-ttu-id="6a4af-126">saudação de alteração lenta natureza dos dados Olá leva toofewer recriações de tabela replicada hello.</span><span class="sxs-lookup"><span data-stu-id="6a4af-126">hello slowly changing nature of hello data leads toofewer rebuilds of hello replicated table.</span></span> 

<span data-ttu-id="6a4af-127">Considere usar uma tabela replicada quando:</span><span class="sxs-lookup"><span data-stu-id="6a4af-127">Consider using a replicated table when:</span></span>

- <span data-ttu-id="6a4af-128">tamanho da tabela Olá em disco é menor que 2 GB, independentemente do número de saudação de linhas.</span><span class="sxs-lookup"><span data-stu-id="6a4af-128">hello table size on disk is less than 2 GB, regardless of hello number of rows.</span></span> <span data-ttu-id="6a4af-129">tamanho de saudação toofind de uma tabela, você pode usar o hello [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) comando: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span><span class="sxs-lookup"><span data-stu-id="6a4af-129">toofind hello size of a table, you can use hello [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) command: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span></span> 
- <span data-ttu-id="6a4af-130">Olá tabela é usada em junções que normalmente exigiriam a movimentação de dados.</span><span class="sxs-lookup"><span data-stu-id="6a4af-130">hello table is used in joins that would otherwise require data movement.</span></span> <span data-ttu-id="6a4af-131">Por exemplo, uma junção em tabelas de hash distribuída requer a movimentação de dados quando as colunas de junção Olá não são Olá a mesma coluna de distribuição.</span><span class="sxs-lookup"><span data-stu-id="6a4af-131">For example, a join on hash-distributed tables requires data movement when hello joining columns are not hello same distribution column.</span></span> <span data-ttu-id="6a4af-132">Se uma das tabelas de hash distribuída Olá for pequena, considere uma tabela replicada.</span><span class="sxs-lookup"><span data-stu-id="6a4af-132">If one of hello hash-distributed tables is small, consider a replicated table.</span></span> <span data-ttu-id="6a4af-133">Uma união em uma tabela round robin requer a movimentação de dados.</span><span class="sxs-lookup"><span data-stu-id="6a4af-133">A join on a round-robin table requires data movement.</span></span> <span data-ttu-id="6a4af-134">É recomendável usar tabelas replicadas em vez de tabelas round robin na maioria dos casos.</span><span class="sxs-lookup"><span data-stu-id="6a4af-134">We recommend using replicated tables instead of round-robin tables in most cases.</span></span> 


<span data-ttu-id="6a4af-135">Considere a possibilidade de converter um existente distribuídas tooa tabela replicada tabela quando:</span><span class="sxs-lookup"><span data-stu-id="6a4af-135">Consider converting an existing distributed table tooa replicated table when:</span></span>

- <span data-ttu-id="6a4af-136">Operações de movimentação de dados de uso que transmitem a nós de computação Olá dados tooall Olá os planos de consulta.</span><span class="sxs-lookup"><span data-stu-id="6a4af-136">Query plans use data movement operations that broadcast hello data tooall hello Compute nodes.</span></span> <span data-ttu-id="6a4af-137">Olá BroadcastMoveOperation é caro e reduz o desempenho da consulta.</span><span class="sxs-lookup"><span data-stu-id="6a4af-137">hello BroadcastMoveOperation is expensive and slows query performance.</span></span> <span data-ttu-id="6a4af-138">operações de movimentação de dados tooview em planos de consulta, use [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="6a4af-138">tooview data movement operations in query plans, use [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span></span>
 
<span data-ttu-id="6a4af-139">Tabelas replicadas não podem resultar em melhor desempenho de consulta hello quando:</span><span class="sxs-lookup"><span data-stu-id="6a4af-139">Replicated tables may not yield hello best query performance when:</span></span>

- <span data-ttu-id="6a4af-140">tabela de saudação tem inserção frequentes, atualizar e excluir operações.</span><span class="sxs-lookup"><span data-stu-id="6a4af-140">hello table has frequent insert, update, and delete operations.</span></span> <span data-ttu-id="6a4af-141">Essas operações de DML (linguagem) de manipulação de dados requerem uma recriação de tabela Olá replicada.</span><span class="sxs-lookup"><span data-stu-id="6a4af-141">These data manipulation language (DML) operations require a rebuild of hello replicated table.</span></span> <span data-ttu-id="6a4af-142">Recompilar com frequência pode causar um desempenho mais lento.</span><span class="sxs-lookup"><span data-stu-id="6a4af-142">Rebuilding frequently can cause slower performance.</span></span>
- <span data-ttu-id="6a4af-143">data warehouse de saudação é dimensionado com frequência.</span><span class="sxs-lookup"><span data-stu-id="6a4af-143">hello data warehouse is scaled frequently.</span></span> <span data-ttu-id="6a4af-144">Dimensionamento de um data warehouse altera o número de saudação de nós de computação, que gera uma recompilação.</span><span class="sxs-lookup"><span data-stu-id="6a4af-144">Scaling a data warehouse changes hello number of Compute nodes, which incurs a rebuild.</span></span>
- <span data-ttu-id="6a4af-145">tabela de saudação tem um grande número de colunas, mas as operações de dados normalmente acessam somente um pequeno número de colunas.</span><span class="sxs-lookup"><span data-stu-id="6a4af-145">hello table has a large number of columns, but data operations typically access only a small number of columns.</span></span> <span data-ttu-id="6a4af-146">Nesse cenário, em vez de replicar toda a tabela hello, pode ser mais eficiente toohash distribuir tabela hello e, em seguida, criar um índice em colunas de saudação acessada com frequência.</span><span class="sxs-lookup"><span data-stu-id="6a4af-146">In this scenario, instead of replicating hello entire table, it might be more effective toohash distribute hello table, and then create an index on hello frequently accessed columns.</span></span> <span data-ttu-id="6a4af-147">Quando uma consulta requer a movimentação de dados, SQL Data Warehouse apenas move dados em Olá solicitadas colunas.</span><span class="sxs-lookup"><span data-stu-id="6a4af-147">When a query requires data movement, SQL Data Warehouse only moves data in hello requested columns.</span></span> 



## <a name="use-replicated-tables-with-simple-query-predicates"></a><span data-ttu-id="6a4af-148">Usar tabelas replicadas com predicados de consulta simples</span><span class="sxs-lookup"><span data-stu-id="6a4af-148">Use replicated tables with simple query predicates</span></span>
<span data-ttu-id="6a4af-149">Antes de escolher toodistribute ou replicar uma tabela, pense em tipos de saudação de consultas que você planejar toorun em relação à tabela hello.</span><span class="sxs-lookup"><span data-stu-id="6a4af-149">Before you choose toodistribute or replicate a table, think about hello types of queries you plan toorun against hello table.</span></span> <span data-ttu-id="6a4af-150">Sempre que possível,</span><span class="sxs-lookup"><span data-stu-id="6a4af-150">Whenever possible,</span></span>

- <span data-ttu-id="6a4af-151">Use tabelas replicadas para consultas com predicados de consulta simples, como igualdade ou desigualdade.</span><span class="sxs-lookup"><span data-stu-id="6a4af-151">Use replicated tables for queries with simple query predicates, such as equality or inequality.</span></span>
- <span data-ttu-id="6a4af-152">Use tabelas distribuídas para consultas com predicados de consulta complexos, como CURTIR ou NÃO CURTIR.</span><span class="sxs-lookup"><span data-stu-id="6a4af-152">Use distributed tables for queries with complex query predicates, such as LIKE or NOT LIKE.</span></span>

<span data-ttu-id="6a4af-153">Consultas de uso intensivo de CPU ter melhor desempenho quando o trabalho de saudação é distribuído em todos os nós de computação hello.</span><span class="sxs-lookup"><span data-stu-id="6a4af-153">CPU-intensive queries perform best when hello work is distributed across all of hello Compute nodes.</span></span> <span data-ttu-id="6a4af-154">Por exemplo, as consultas que executam cálculos em cada linha de uma tabela apresentam um desempenho melhor nas tabelas distribuídas do que nas tabelas replicadas.</span><span class="sxs-lookup"><span data-stu-id="6a4af-154">For example, queries that run computations on each row of a table perform better on distributed tables than replicated tables.</span></span> <span data-ttu-id="6a4af-155">Como uma tabela replicada é armazenada por completo em cada nó de computação, uma consulta de uso intensivo de CPU em uma tabela replicada é executado em relação à tabela inteira Olá em cada nó de computação.</span><span class="sxs-lookup"><span data-stu-id="6a4af-155">Since a replicated table is stored in full on each Compute node, a CPU-intensive query against a replicated table runs against hello entire table on every Compute node.</span></span> <span data-ttu-id="6a4af-156">Olá computação extra pode diminuir o desempenho de consulta.</span><span class="sxs-lookup"><span data-stu-id="6a4af-156">hello extra computation can slow query performance.</span></span>

<span data-ttu-id="6a4af-157">Por exemplo, esta consulta tem um predicado complexo.</span><span class="sxs-lookup"><span data-stu-id="6a4af-157">For example, this query has a complex predicate.</span></span>  <span data-ttu-id="6a4af-158">Ele é executado mais rapidamente quando o fornecedor é uma tabela distribuída em vez de uma tabela replicada.</span><span class="sxs-lookup"><span data-stu-id="6a4af-158">It runs faster when supplier is a distributed table instead of a replicated table.</span></span> <span data-ttu-id="6a4af-159">Neste exemplo, o fornecedor pode ser distribuído em hash ou em round robin.</span><span class="sxs-lookup"><span data-stu-id="6a4af-159">In this example, supplier can be hash-distributed or round-robin distributed.</span></span>

```sql

SELECT EnglishProductName 
FROM DimProduct 
WHERE EnglishDescription LIKE '%frame%comfortable%'

```

## <a name="convert-existing-round-robin-tables-tooreplicated-tables"></a><span data-ttu-id="6a4af-160">Converter as tabelas tooreplicated round-robin tabelas existentes</span><span class="sxs-lookup"><span data-stu-id="6a4af-160">Convert existing round-robin tables tooreplicated tables</span></span>
<span data-ttu-id="6a4af-161">Se você já tiver tabelas round robin, recomendamos convertê-las tooreplicated tabelas se eles atender aos critérios descritos neste artigo.</span><span class="sxs-lookup"><span data-stu-id="6a4af-161">If you already have round-robin tables, we recommend converting them tooreplicated tables if they meet with criteria outlined in this article.</span></span> <span data-ttu-id="6a4af-162">Tabelas replicadas melhoram o desempenho em tabelas de round-robin porque eles eliminam a necessidade de saudação de movimentação de dados.</span><span class="sxs-lookup"><span data-stu-id="6a4af-162">Replicated tables improve performance over round-robin tables because they eliminate hello need for data movement.</span></span>  <span data-ttu-id="6a4af-163">Uma tabela round robin sempre requer a movimentação de dados para as junções.</span><span class="sxs-lookup"><span data-stu-id="6a4af-163">A round-robin table always requires data movement for joins.</span></span> 

<span data-ttu-id="6a4af-164">Este exemplo usa [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) toochange Olá DimSalesTerritory tabela tooa replicadas de tabela.</span><span class="sxs-lookup"><span data-stu-id="6a4af-164">This example uses [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) toochange hello DimSalesTerritory table tooa replicated table.</span></span> <span data-ttu-id="6a4af-165">Este exemplo funciona independentemente de DimSalesTerritory ser distribuído por hash ou por round robin.</span><span class="sxs-lookup"><span data-stu-id="6a4af-165">This example works regardless of whether DimSalesTerritory is hash-distributed or round-robin.</span></span>

```sql
CREATE TABLE [dbo].[DimSalesTerritory_REPLICATE]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = REPLICATE  
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]
OPTION  (LABEL  = 'CTAS : DimSalesTerritory_REPLICATE') 

--Create statistics on new table
CREATE STATISTICS [SalesTerritoryKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryKey]);
CREATE STATISTICS [SalesTerritoryAlternateKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryAlternateKey]);
CREATE STATISTICS [SalesTerritoryRegion] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryRegion]);
CREATE STATISTICS [SalesTerritoryCountry] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryCountry]);
CREATE STATISTICS [SalesTerritoryGroup] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryGroup]);

-- Switch table names
RENAME OBJECT [dbo].[DimSalesTerritory] too[DimSalesTerritory_old];
RENAME OBJECT [dbo].[DimSalesTerritory_REPLICATE] too[DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```  

### <a name="query-performance-example-for-round-robin-versus-replicated"></a><span data-ttu-id="6a4af-166">Exemplo de desempenho de consulta de round-robin versus replicado</span><span class="sxs-lookup"><span data-stu-id="6a4af-166">Query performance example for round-robin versus replicated</span></span> 

<span data-ttu-id="6a4af-167">Uma tabela replicada não requer nenhuma movimentação de dados para junções porque a tabela inteira Olá já está presente em cada nó de computação.</span><span class="sxs-lookup"><span data-stu-id="6a4af-167">A replicated table does not require any data movement for joins because hello entire table is already present on each Compute node.</span></span> <span data-ttu-id="6a4af-168">Se as tabelas de dimensões Olá round-robin distribuído, uma junção copia tabela de dimensões Olá tooeach completo do nó de computação.</span><span class="sxs-lookup"><span data-stu-id="6a4af-168">If hello dimension tables are round-robin distributed, a join copies hello dimension table in full tooeach Compute node.</span></span> <span data-ttu-id="6a4af-169">dados de saudação toomove, o plano de consulta de saudação contém uma operação chamada BroadcastMoveOperation.</span><span class="sxs-lookup"><span data-stu-id="6a4af-169">toomove hello data, hello query plan contains an operation called BroadcastMoveOperation.</span></span> <span data-ttu-id="6a4af-170">Esse tipo de operação de movimentação de dados reduz o desempenho da consulta e é eliminada usando tabelas replicadas.</span><span class="sxs-lookup"><span data-stu-id="6a4af-170">This type of data movement operation slows query performance and is eliminated by using replicated tables.</span></span> <span data-ttu-id="6a4af-171">etapas de plano de consulta tooview, use Olá [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) exibição de catálogo do sistema.</span><span class="sxs-lookup"><span data-stu-id="6a4af-171">tooview query plan steps, use hello [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) system catalog view.</span></span> 

<span data-ttu-id="6a4af-172">Por exemplo, na seguinte consulta no esquema de AdventureWorks hello, Olá ` FactInternetSales` tabela é distribuída de hash.</span><span class="sxs-lookup"><span data-stu-id="6a4af-172">For example, in following query against hello AdventureWorks schema, hello ` FactInternetSales` table is hash-distributed.</span></span> <span data-ttu-id="6a4af-173">Olá `DimDate` e `DimSalesTerritory` as tabelas são tabelas de dimensão menores.</span><span class="sxs-lookup"><span data-stu-id="6a4af-173">hello `DimDate` and `DimSalesTerritory` tables are smaller dimension tables.</span></span> <span data-ttu-id="6a4af-174">Esta consulta retorna o total de vendas Olá na América do Norte do ano fiscal de 2004:</span><span class="sxs-lookup"><span data-stu-id="6a4af-174">This query returns hello total sales in North America for fiscal year 2004:</span></span>
 
```sql
SELECT [TotalSalesAmount] = SUM(SalesAmount)
FROM dbo.FactInternetSales s
INNER JOIN dbo.DimDate d
  ON d.DateKey = s.OrderDateKey
INNER JOIN dbo.DimSalesTerritory t
  ON t.SalesTerritoryKey = s.SalesTerritoryKey
WHERE d.FiscalYear = 2004
  AND t.SalesTerritoryGroup = 'North America'
```
<span data-ttu-id="6a4af-175">Recriamos `DimDate` e `DimSalesTerritory` como tabelas round robin.</span><span class="sxs-lookup"><span data-stu-id="6a4af-175">We re-created `DimDate` and `DimSalesTerritory` as round-robin tables.</span></span> <span data-ttu-id="6a4af-176">Como resultado, a consulta Olá mostrou Olá plano de consulta, que tem vários difusão mover as operações a seguir:</span><span class="sxs-lookup"><span data-stu-id="6a4af-176">As a result, hello query showed hello following query plan, which has multiple broadcast move operations:</span></span> 
 
![Plano de consulta round robin](media/design-guidance-for-replicated-tables/round-robin-tables-query-plan.jpg) 

<span data-ttu-id="6a4af-178">Criamos novamente `DimDate` e `DimSalesTerritory` como tabelas replicadas e executar a consulta de saudação novamente.</span><span class="sxs-lookup"><span data-stu-id="6a4af-178">We re-created `DimDate` and `DimSalesTerritory` as replicated tables, and ran hello query again.</span></span> <span data-ttu-id="6a4af-179">plano de consulta resultante Olá é muito menor e não tem qualquer difundir move.</span><span class="sxs-lookup"><span data-stu-id="6a4af-179">hello resulting query plan is much shorter and does not have any broadcast moves.</span></span>

![Plano de consulta replicado](media/design-guidance-for-replicated-tables/replicated-tables-query-plan.jpg) 


## <a name="performance-considerations-for-modifying-replicated-tables"></a><span data-ttu-id="6a4af-181">Considerações sobre o desempenho para modificar as tabelas replicadas</span><span class="sxs-lookup"><span data-stu-id="6a4af-181">Performance considerations for modifying replicated tables</span></span>
<span data-ttu-id="6a4af-182">SQL Data Warehouse implementa uma tabela replicada, mantendo uma versão principal da tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="6a4af-182">SQL Data Warehouse implements a replicated table by maintaining a master version of hello table.</span></span> <span data-ttu-id="6a4af-183">Copia Olá versão mestre tooone distribuição banco de dados em cada nó de computação.</span><span class="sxs-lookup"><span data-stu-id="6a4af-183">It copies hello master version tooone distribution database on each Compute node.</span></span> <span data-ttu-id="6a4af-184">Quando há uma alteração, o SQL Data Warehouse atualiza primeiro tabela mestre hello.</span><span class="sxs-lookup"><span data-stu-id="6a4af-184">When there is a change, SQL Data Warehouse first updates hello master table.</span></span> <span data-ttu-id="6a4af-185">Em seguida, ele exige uma recriação de tabelas de saudação em cada nó de computação.</span><span class="sxs-lookup"><span data-stu-id="6a4af-185">Then it requires a rebuild of hello tables on each Compute node.</span></span> <span data-ttu-id="6a4af-186">Uma recriação de uma tabela replicada inclui copiar do nó de computação tooeach Olá tabela e, em seguida, a recriação de índices de saudação.</span><span class="sxs-lookup"><span data-stu-id="6a4af-186">A rebuild of a replicated table includes copying hello table tooeach Compute node and then rebuilding hello indexes.</span></span>

<span data-ttu-id="6a4af-187">As recompilações são necessárias depois que:</span><span class="sxs-lookup"><span data-stu-id="6a4af-187">Rebuilds are required after:</span></span>
- <span data-ttu-id="6a4af-188">Os dados são carregados ou modificados</span><span class="sxs-lookup"><span data-stu-id="6a4af-188">Data is loaded or modified</span></span>
- <span data-ttu-id="6a4af-189">Olá data warehouse é dimensionado tooa configuração de DWU diferente</span><span class="sxs-lookup"><span data-stu-id="6a4af-189">hello data warehouse is scaled tooa different DWU setting</span></span>
- <span data-ttu-id="6a4af-190">A definição da tabela é atualizada</span><span class="sxs-lookup"><span data-stu-id="6a4af-190">Table definition is updated</span></span>

<span data-ttu-id="6a4af-191">As recompilações não são necessárias após:</span><span class="sxs-lookup"><span data-stu-id="6a4af-191">Rebuilds are not required after:</span></span>
- <span data-ttu-id="6a4af-192">Pausar a operação</span><span class="sxs-lookup"><span data-stu-id="6a4af-192">Pause operation</span></span>
- <span data-ttu-id="6a4af-193">Retomar a operação</span><span class="sxs-lookup"><span data-stu-id="6a4af-193">Resume operation</span></span>

<span data-ttu-id="6a4af-194">Olá de reconstrução não acontece imediatamente depois que os dados são modificados.</span><span class="sxs-lookup"><span data-stu-id="6a4af-194">hello rebuild does not happen immediately after data is modified.</span></span> <span data-ttu-id="6a4af-195">Em vez disso, a recriação de saudação é disparada Olá a primeira vez que uma consulta seleciona da tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="6a4af-195">Instead, hello rebuild is triggered hello first time a query selects from hello table.</span></span>  <span data-ttu-id="6a4af-196">Instrução select inicial, Olá da tabela de saudação são toorebuild de etapas Olá tabela replicada.</span><span class="sxs-lookup"><span data-stu-id="6a4af-196">Within hello initial select statement from hello table are steps toorebuild hello replicated table.</span></span>  <span data-ttu-id="6a4af-197">Como Olá de reconstrução é feita em consulta hello, Olá impacto toohello inicial instrução select pode ser significativa dependendo do tamanho da saudação da tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="6a4af-197">Because hello rebuild is done within hello query, hello impact toohello initial select statement could be significant depending on hello size of hello table.</span></span>  <span data-ttu-id="6a4af-198">Se várias tabelas replicadas estão envolvidas que precisam de uma recompilação, cada cópia será reconstruída em série como etapas dentro de instrução de saudação.</span><span class="sxs-lookup"><span data-stu-id="6a4af-198">If multiple replicated tables are involved that need a rebuild, each copy is rebuilt serially as steps within hello statement.</span></span>  <span data-ttu-id="6a4af-199">toomaintain consistência de dados durante a recriação de saudação do hello replicadas um bloqueio exclusivo é obtido na tabela de saudação de tabela.</span><span class="sxs-lookup"><span data-stu-id="6a4af-199">toomaintain data consistency during hello rebuild of hello replicated table an exclusive lock is taken on hello table.</span></span>  <span data-ttu-id="6a4af-200">bloqueio de saudação impede que todas as tabelas de toohello de acesso para duração Olá de reconstrução de saudação.</span><span class="sxs-lookup"><span data-stu-id="6a4af-200">hello lock prevents all access toohello table for hello duration of hello rebuild.</span></span> 

### <a name="use-indexes-conservatively"></a><span data-ttu-id="6a4af-201">Use os índices de forma prudente</span><span class="sxs-lookup"><span data-stu-id="6a4af-201">Use indexes conservatively</span></span>
<span data-ttu-id="6a4af-202">Práticas recomendadas de indexação padrão se aplica a tabelas tooreplicated.</span><span class="sxs-lookup"><span data-stu-id="6a4af-202">Standard indexing practices apply tooreplicated tables.</span></span> <span data-ttu-id="6a4af-203">SQL Data Warehouse recria o índice cada tabela replicada como parte da recompilação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6a4af-203">SQL Data Warehouse rebuilds each replicated table index as part of hello rebuild.</span></span> <span data-ttu-id="6a4af-204">Só use índices ganho de desempenho Olá supera o custo de Olá de reconstrução de índices de saudação.</span><span class="sxs-lookup"><span data-stu-id="6a4af-204">Only use indexes when hello performance gain outweighs hello cost of rebuilding hello indexes.</span></span>  
 
### <a name="batch-data-loads"></a><span data-ttu-id="6a4af-205">Cargas de dados em lotes</span><span class="sxs-lookup"><span data-stu-id="6a4af-205">Batch data loads</span></span>
<span data-ttu-id="6a4af-206">Ao carregar dados em tabelas replicadas, tente toominimize recria por envio em lote cargas juntas.</span><span class="sxs-lookup"><span data-stu-id="6a4af-206">When loading data into replicated tables, try toominimize rebuilds by batching loads together.</span></span> <span data-ttu-id="6a4af-207">Execute todas as cargas de saudação em lote antes de executar instruções select.</span><span class="sxs-lookup"><span data-stu-id="6a4af-207">Perform all hello batched loads before running select statements.</span></span>

<span data-ttu-id="6a4af-208">Por exemplo, esse padrão de carga carrega dados de quatro fontes e invoca quatro recompilações.</span><span class="sxs-lookup"><span data-stu-id="6a4af-208">For example, this load pattern loads data from four sources and invokes four rebuilds.</span></span> 

- <span data-ttu-id="6a4af-209">Carregar da fonte de dados 1.</span><span class="sxs-lookup"><span data-stu-id="6a4af-209">Load from source 1.</span></span>
- <span data-ttu-id="6a4af-210">A instrução SELECT aciona a recompilação 1.</span><span class="sxs-lookup"><span data-stu-id="6a4af-210">Select statement triggers rebuild 1.</span></span>
- <span data-ttu-id="6a4af-211">Carregar da fonte de dados 2.</span><span class="sxs-lookup"><span data-stu-id="6a4af-211">Load from source 2.</span></span>
- <span data-ttu-id="6a4af-212">A instrução SELECT aciona a recompilação 2.</span><span class="sxs-lookup"><span data-stu-id="6a4af-212">Select statement triggers rebuild 2.</span></span>
- <span data-ttu-id="6a4af-213">Carregar da fonte de dados 3.</span><span class="sxs-lookup"><span data-stu-id="6a4af-213">Load from source 3.</span></span>
- <span data-ttu-id="6a4af-214">A instrução SELECT aciona a recompilação 3.</span><span class="sxs-lookup"><span data-stu-id="6a4af-214">Select statement triggers rebuild 3.</span></span>
- <span data-ttu-id="6a4af-215">Carregar da fonte de dados 4.</span><span class="sxs-lookup"><span data-stu-id="6a4af-215">Load from source 4.</span></span>
- <span data-ttu-id="6a4af-216">A instrução SELECT aciona a recompilação 4.</span><span class="sxs-lookup"><span data-stu-id="6a4af-216">Select statement triggers rebuild 4.</span></span>

<span data-ttu-id="6a4af-217">Por exemplo, esse padrão de carga carrega dados de quatro fontes, mas invoca apenas uma recompilação.</span><span class="sxs-lookup"><span data-stu-id="6a4af-217">For example, this load pattern loads data from four sources, but only invokes one rebuild.</span></span>

- <span data-ttu-id="6a4af-218">Carregar da fonte de dados 1.</span><span class="sxs-lookup"><span data-stu-id="6a4af-218">Load from source 1.</span></span>
- <span data-ttu-id="6a4af-219">Carregar da fonte de dados 2.</span><span class="sxs-lookup"><span data-stu-id="6a4af-219">Load from source 2.</span></span>
- <span data-ttu-id="6a4af-220">Carregar da fonte de dados 3.</span><span class="sxs-lookup"><span data-stu-id="6a4af-220">Load from source 3.</span></span>
- <span data-ttu-id="6a4af-221">Carregar da fonte de dados 4.</span><span class="sxs-lookup"><span data-stu-id="6a4af-221">Load from source 4.</span></span>
- <span data-ttu-id="6a4af-222">A instrução SELECT aciona a recompilação.</span><span class="sxs-lookup"><span data-stu-id="6a4af-222">Select statement triggers rebuild.</span></span>


### <a name="rebuild-a-replicated-table-after-a-batch-load"></a><span data-ttu-id="6a4af-223">Recompilar uma tabela replicada após um carregamento em lote</span><span class="sxs-lookup"><span data-stu-id="6a4af-223">Rebuild a replicated table after a batch load</span></span>
<span data-ttu-id="6a4af-224">tempos de execução de consulta consistentes tooensure, é recomendável forçar uma atualização de tabelas de saudação replicada depois de uma carga de lote.</span><span class="sxs-lookup"><span data-stu-id="6a4af-224">tooensure consistent query execution times, we recommend forcing a refresh of hello replicated tables after a batch load.</span></span> <span data-ttu-id="6a4af-225">Caso contrário, consulta primeiro Olá deve aguardar Olá tabelas toorefresh, que inclui a recriação de índices de saudação.</span><span class="sxs-lookup"><span data-stu-id="6a4af-225">Otherwise, hello first query must wait for hello tables toorefresh, which includes rebuilding hello indexes.</span></span> <span data-ttu-id="6a4af-226">Dependendo do tamanho de saudação e o número de tabelas replicadas afetados, o impacto no desempenho Olá pode ser significativo.</span><span class="sxs-lookup"><span data-stu-id="6a4af-226">Depending on hello size and number of replicated tables affected, hello performance impact can be significant.</span></span>  

<span data-ttu-id="6a4af-227">Essa consulta usa Olá [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) saudação do DMV toolist replicadas tabelas que foram modificadas, mas não foi recompiladas.</span><span class="sxs-lookup"><span data-stu-id="6a4af-227">This query uses hello [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV toolist hello replicated tables that have been modified, but not rebuilt.</span></span>

```sql 
SELECT [ReplicatedTable] = t.[name]
  FROM sys.tables t  
  JOIN sys.pdw_replicated_table_cache_state c  
    ON c.object_id = t.object_id 
  JOIN sys.pdw_table_distribution_properties p 
    ON p.object_id = t.object_id 
  WHERE c.[state] = 'NotReady'
    AND p.[distribution_policy_desc] = 'REPLICATE'
```
 
<span data-ttu-id="6a4af-228">tooforce executar Olá instrução a seguir em cada tabela no hello precede a saída de uma recompilação.</span><span class="sxs-lookup"><span data-stu-id="6a4af-228">tooforce a rebuild, run hello following statement on each table in hello preceding output.</span></span> 

```sql
SELECT TOP 1 * FROM [ReplicatedTable]
``` 
 
## <a name="next-steps"></a><span data-ttu-id="6a4af-229">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6a4af-229">Next steps</span></span> 
<span data-ttu-id="6a4af-230">toocreate uma tabela replicada, use uma das instruções a seguir:</span><span class="sxs-lookup"><span data-stu-id="6a4af-230">toocreate a replicated table, use one of these statements:</span></span>

- [<span data-ttu-id="6a4af-231">CRIAR TABELA (SQL Data Warehouse do Azure)</span><span class="sxs-lookup"><span data-stu-id="6a4af-231">CREATE TABLE (Azure SQL Data Warehouse)</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-azure-sql-data-warehouse)
- [<span data-ttu-id="6a4af-232">CREATE TABLE AS SELECT (SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="6a4af-232">CREATE TABLE AS SELECT (Azure SQL Data Warehouse</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)

<span data-ttu-id="6a4af-233">Para obter uma visão geral das tabelas distribuídas, consulte [Tabelas distribuídas](sql-data-warehouse-tables-distribute.md).</span><span class="sxs-lookup"><span data-stu-id="6a4af-233">For an overview of distributed tables, see [distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>



