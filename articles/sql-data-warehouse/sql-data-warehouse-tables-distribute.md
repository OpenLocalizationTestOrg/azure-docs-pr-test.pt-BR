---
title: Como distribuir tabelas no SQL Data Warehouse | Microsoft Docs
description: "Introdução à distribuição de tabelas no Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: 5ed4337f-7262-4ef6-8fd6-1809ce9634fc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: d0e12bf821a81826a20b8db84e76c48fa60ad9b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="distributing-tables-in-sql-data-warehouse"></a><span data-ttu-id="60f3c-103">Distribuindo tabelas no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="60f3c-103">Distributing tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="60f3c-104">[Visão geral][Overview]</span><span class="sxs-lookup"><span data-stu-id="60f3c-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="60f3c-105">[Tipos de Dados][Data Types]</span><span class="sxs-lookup"><span data-stu-id="60f3c-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="60f3c-106">[Distribuir][Distribute]</span><span class="sxs-lookup"><span data-stu-id="60f3c-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="60f3c-107">[Índice][Index]</span><span class="sxs-lookup"><span data-stu-id="60f3c-107">[Index][Index]</span></span>
> * <span data-ttu-id="60f3c-108">[Partição][Partition]</span><span class="sxs-lookup"><span data-stu-id="60f3c-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="60f3c-109">[Estatísticas][Statistics]</span><span class="sxs-lookup"><span data-stu-id="60f3c-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="60f3c-110">[Temporário][Temporary]</span><span class="sxs-lookup"><span data-stu-id="60f3c-110">[Temporary][Temporary]</span></span>
>
>

<span data-ttu-id="60f3c-111">SQL Data Warehouse é um sistema de banco de dados distribuído de processamento extremamente paralelo (MPP).</span><span class="sxs-lookup"><span data-stu-id="60f3c-111">SQL Data Warehouse is a massively parallel processing (MPP) distributed database system.</span></span>  <span data-ttu-id="60f3c-112">Ao dividir os dados e a funcionalidade de processamento em vários nós, o SQL Data Warehouse pode oferecer uma enorme escalabilidade, muito além de qualquer sistema individual.</span><span class="sxs-lookup"><span data-stu-id="60f3c-112">By dividing data and processing capability across multiple nodes, SQL Data Warehouse can offer huge scalability - far beyond any single system.</span></span>  <span data-ttu-id="60f3c-113">Decidir como distribuir seus dados dentro de seu SQL Data Warehouse é um dos fatores mais importantes para alcançar um desempenho ideal.</span><span class="sxs-lookup"><span data-stu-id="60f3c-113">Deciding how to distribute your data within your SQL Data Warehouse is one of the most important factors to achieving optimal performance.</span></span>   <span data-ttu-id="60f3c-114">A chave para o desempenho ideal é minimizar a movimentação dos dados, e a chave para minimizar a movimentação de dados é selecionar a estratégia de distribuição correta.</span><span class="sxs-lookup"><span data-stu-id="60f3c-114">The key to optimal performance is minimizing data movement and in turn the key to minimizing data movement is selecting the right distribution strategy.</span></span>

## <a name="understanding-data-movement"></a><span data-ttu-id="60f3c-115">Noções básicas sobre a movimentação de dados</span><span class="sxs-lookup"><span data-stu-id="60f3c-115">Understanding data movement</span></span>
<span data-ttu-id="60f3c-116">Em um sistema MPP, os dados de cada tabela são divididos em vários bancos de dados subjacentes.</span><span class="sxs-lookup"><span data-stu-id="60f3c-116">In an MPP system, the data from each table is divided across several underlying databases.</span></span>  <span data-ttu-id="60f3c-117">As consultas mais otimizadas em um sistema MPP podem simplesmente ser passadas para executar em bancos de dados distribuídos individuais sem interação entre os outros bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="60f3c-117">The most optimized queries on an MPP system can simply be passed through to execute on the individual distributed databases with no interaction between the other databases.</span></span>  <span data-ttu-id="60f3c-118">Por exemplo, digamos que você tenha um banco de dados com dados de vendas que contém duas tabelas, vendas e clientes.</span><span class="sxs-lookup"><span data-stu-id="60f3c-118">For example, let's say you have a database with sales data which contains two tables, sales and customers.</span></span>  <span data-ttu-id="60f3c-119">Se você tiver uma consulta que precise unir a tabela de vendas à tabela de clientes, e dividir as tabelas de vendas e clientes pelo número de clientes, colocando cada cliente em um banco de dados separado, todas as consultas que unem vendas e clientes poderão ser resolvidas em cada banco de dados sem conhecimento dos outros bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="60f3c-119">If you have a query that needs to join your sales table to your customer table and you divide both your sales and customer tables up by customer number, putting each customer in a separate database, any queries which join sales and customer can be solved within each database with no knowledge of the other databases.</span></span>  <span data-ttu-id="60f3c-120">Por outro lado, se você dividir seus dados de vendas pelo número de pedido e seus dados de clientes pelo número de cliente, qualquer banco de dados específico não terá os dados correspondentes para cada cliente e, assim, se você quiser unir os dados de vendas aos dados de clientes, precisará obter os dados de cada cliente dos outros bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="60f3c-120">In contrast, if you divided your sales data by order number and your customer data by customer number, then any given database will not have the corresponding data for each customer and thus if you wanted to join your sales data to your customer data, you would need to get the data for each customer from the other databases.</span></span>  <span data-ttu-id="60f3c-121">No segundo exemplo, a movimentação de dados precisa ocorrer para mover os dados de clientes para os dados de vendas, de modo que as duas tabelas possam ser unidas.</span><span class="sxs-lookup"><span data-stu-id="60f3c-121">In this second example, data movement would need to occur to move the customer data to the sales data, so that the two tables can be joined.</span></span>  

<span data-ttu-id="60f3c-122">A movimentação de dados nem sempre é ruim; às vezes, ela é necessária para resolver uma consulta.</span><span class="sxs-lookup"><span data-stu-id="60f3c-122">Data movement isn't always a bad thing, sometimes it's necessary to solve a query.</span></span>  <span data-ttu-id="60f3c-123">Porém, quando essa etapa extra pode ser evitada, naturalmente a consulta é executada mais depressa.</span><span class="sxs-lookup"><span data-stu-id="60f3c-123">But when this extra step can be avoided, naturally your query will run faster.</span></span>  <span data-ttu-id="60f3c-124">A movimentação de dados geralmente surge quando tabelas são unidas ou são executadas agregações.</span><span class="sxs-lookup"><span data-stu-id="60f3c-124">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="60f3c-125">Muitas vezes, você precisa fazer ambos. Portanto, embora possa fazer a otimização de um cenário, como uma associação, você ainda precisará da movimentação de dados para ajudar a resolver o outro cenário, como uma agregação.</span><span class="sxs-lookup"><span data-stu-id="60f3c-125">Often you need to do both, so while you may be able to optimize for one scenario, like a join, you still need data movement to help you solve for the other scenario, like an aggregation.</span></span>  <span data-ttu-id="60f3c-126">O truque é descobrir o que dá menos trabalho.</span><span class="sxs-lookup"><span data-stu-id="60f3c-126">The trick is figuring out which is less work.</span></span>  <span data-ttu-id="60f3c-127">Na maioria dos casos, a distribuição de grandes tabelas de fatos em uma coluna unida normalmente é o método mais eficaz para reduzir a maior parte da movimentação de dados.</span><span class="sxs-lookup"><span data-stu-id="60f3c-127">In most cases, distributing large fact tables on a commonly joined column is the most effective method for reducing the most data movement.</span></span>  <span data-ttu-id="60f3c-128">A distribuição de dados em colunas de junção é um método muito mais comum para reduzir a movimentação de dados, em vez da distribuição de dados em colunas envolvidas em uma agregação.</span><span class="sxs-lookup"><span data-stu-id="60f3c-128">Distributing data on join columns is a much more common method to reduce data movement than distributing data on columns involved in an aggregation.</span></span>

## <a name="select-distribution-method"></a><span data-ttu-id="60f3c-129">Selecionar método de distribuição</span><span class="sxs-lookup"><span data-stu-id="60f3c-129">Select distribution method</span></span>
<span data-ttu-id="60f3c-130">Nos bastidores, o SQL Data Warehouse divide seus dados em 60 bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="60f3c-130">Behind the scenes, SQL Data Warehouse divides your data into 60 databases.</span></span>  <span data-ttu-id="60f3c-131">Cada banco de dados individual é conhecido como uma **distribuição**.</span><span class="sxs-lookup"><span data-stu-id="60f3c-131">Each individual database is referred to as a **distribution**.</span></span>  <span data-ttu-id="60f3c-132">Quando os dados são carregados em cada tabela, o SQL Data Warehouse precisa saber como dividir dados entre essas 60 distribuições.</span><span class="sxs-lookup"><span data-stu-id="60f3c-132">When data is loaded into each table, SQL Data Warehouse has to know how to divide your data across these 60 distributions.</span></span>  

<span data-ttu-id="60f3c-133">O método de distribuição é definido no nível da tabela e, atualmente, há duas opções:</span><span class="sxs-lookup"><span data-stu-id="60f3c-133">The distribution method is defined at the table level and currently there are two choices:</span></span>

1. <span data-ttu-id="60f3c-134">**Round robin** , que distribui dados uniformemente, mas aleatoriamente.</span><span class="sxs-lookup"><span data-stu-id="60f3c-134">**Round robin** which distribute data evenly but randomly.</span></span>
2. <span data-ttu-id="60f3c-135">**Distribuídos por hash** , que distribui dados baseados em valores de hash de uma única coluna</span><span class="sxs-lookup"><span data-stu-id="60f3c-135">**Hash Distributed** which distributes data based on hashing values from a single column</span></span>

<span data-ttu-id="60f3c-136">Por padrão, quando você não define um método de distribuição de dados, a tabela será distribuída usando o método de distribuição **round robin** .</span><span class="sxs-lookup"><span data-stu-id="60f3c-136">By default, when you do not define a data distribution method, your table will be distributed using the **round robin** distribution method.</span></span>  <span data-ttu-id="60f3c-137">No entanto, conforme a sua implementação vai se tornando mais sofisticada, convém considerar o uso de tabelas **distribuídas por hash** para minimizar a movimentação de dados, que por sua vez otimizará o desempenho da consulta.</span><span class="sxs-lookup"><span data-stu-id="60f3c-137">However, as you become more sophisticated in your implementation, you will want to consider using **hash distributed** tables to minimize data movement which will in turn optimize query performance.</span></span>

### <a name="round-robin-tables"></a><span data-ttu-id="60f3c-138">Tabelas Round Robin</span><span class="sxs-lookup"><span data-stu-id="60f3c-138">Round Robin Tables</span></span>
<span data-ttu-id="60f3c-139">O uso do método Round Robin de distribuição de dados é basicamente como parece.</span><span class="sxs-lookup"><span data-stu-id="60f3c-139">Using the Round Robin method of distributing data is very much how it sounds.</span></span>  <span data-ttu-id="60f3c-140">Conforme seus dados vão sendo carregados, cada linha é simplesmente enviada para a próxima distribuição.</span><span class="sxs-lookup"><span data-stu-id="60f3c-140">As your data is loaded, each row is simply sent to the next distribution.</span></span>  <span data-ttu-id="60f3c-141">Esse método de distribuição de dados sempre distribui os dados muito uniforme e aleatoriamente em todas as distribuições.</span><span class="sxs-lookup"><span data-stu-id="60f3c-141">This method of distributing the data will always randomly distribute the data very evenly across all of the distributions.</span></span>  <span data-ttu-id="60f3c-142">Ou seja, não há uma classificação durante o processo de round robin que coloca seus dados.</span><span class="sxs-lookup"><span data-stu-id="60f3c-142">That is, there is no sorting done during the round robin process which places your data.</span></span>  <span data-ttu-id="60f3c-143">Uma distribuição round robin é chamada às vezes de hash aleatório por esse motivo.</span><span class="sxs-lookup"><span data-stu-id="60f3c-143">A round robin distribution is sometimes called a random hash for this reason.</span></span>  <span data-ttu-id="60f3c-144">Com uma tabela distribuída por round robin, não é necessário compreender os dados.</span><span class="sxs-lookup"><span data-stu-id="60f3c-144">With a round-robin distributed table there is no need to understand the data.</span></span>  <span data-ttu-id="60f3c-145">Por esse motivo, as tabelas Round Robin normalmente são bons destinos de carregamento.</span><span class="sxs-lookup"><span data-stu-id="60f3c-145">For this reason, Round-Robin tables often make good loading targets.</span></span>

<span data-ttu-id="60f3c-146">Por padrão, se nenhum método de distribuição for escolhido, o método de distribuição round robin será usado.</span><span class="sxs-lookup"><span data-stu-id="60f3c-146">By default, if no distribution method is chosen, the round robin distribution method will be used.</span></span>  <span data-ttu-id="60f3c-147">No entanto, embora as tabelas round robin sejam fáceis de usar, como os dados são distribuídos aleatoriamente em todo o sistema, isso significa que o sistema não pode garantir em que distribuição está cada linha.</span><span class="sxs-lookup"><span data-stu-id="60f3c-147">However, while round robin tables are easy to use, because data is randomly distributed across the system it means that the system can't guarantee which distribution each row is on.</span></span>  <span data-ttu-id="60f3c-148">Como resultado, o sistema às vezes precisa chamar uma operação de movimentação de dados para organizar melhor seus dados antes de poder resolver uma consulta.</span><span class="sxs-lookup"><span data-stu-id="60f3c-148">As a result, the system sometimes needs to invoke a data movement operation to better organize your data before it can resolve a query.</span></span>  <span data-ttu-id="60f3c-149">Essa etapa extra pode causar lentidão em suas consultas.</span><span class="sxs-lookup"><span data-stu-id="60f3c-149">This extra step can slow down your queries.</span></span>

<span data-ttu-id="60f3c-150">Considere usar a distribuição round robin para a sua tabela nos seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="60f3c-150">Consider using Round Robin distribution for your table in the following scenarios:</span></span>

* <span data-ttu-id="60f3c-151">Ao começar, como um simples ponto de partida</span><span class="sxs-lookup"><span data-stu-id="60f3c-151">When getting started as a simple starting point</span></span>
* <span data-ttu-id="60f3c-152">Se não houver uma chave de junção óbvia</span><span class="sxs-lookup"><span data-stu-id="60f3c-152">If there is no obvious joining key</span></span>
* <span data-ttu-id="60f3c-153">Se não houver colunas candidatas boas para distribuir a tabela de hash</span><span class="sxs-lookup"><span data-stu-id="60f3c-153">If there is not good candidate column for hash distributing the table</span></span>
* <span data-ttu-id="60f3c-154">Se a tabela não compartilhar uma chave de junção comum com outras tabelas</span><span class="sxs-lookup"><span data-stu-id="60f3c-154">If the table does not share a common join key with other tables</span></span>
* <span data-ttu-id="60f3c-155">Se a junção for menos significativa do que outras junções na consulta</span><span class="sxs-lookup"><span data-stu-id="60f3c-155">If the join is less significant than other joins in the query</span></span>
* <span data-ttu-id="60f3c-156">Quando a tabela é uma tabela temporária de preparo</span><span class="sxs-lookup"><span data-stu-id="60f3c-156">When the table is a temporary staging table</span></span>

<span data-ttu-id="60f3c-157">Ambos os exemplos criarão uma tabela Round Robin:</span><span class="sxs-lookup"><span data-stu-id="60f3c-157">Both of these examples will create a Round Robin Table:</span></span>

```SQL
-- Round Robin created by default
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
;

-- Explicitly Created Round Robin Table
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
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
,   DISTRIBUTION = ROUND_ROBIN
)
;
```

> [!NOTE]
> <span data-ttu-id="60f3c-158">Embora o round robin seja o tipo de tabela padrão, ser claro em seu DDL é considerado uma prática recomendada para que as intenções do seu layout de tabela fiquem claras para outras pessoas.</span><span class="sxs-lookup"><span data-stu-id="60f3c-158">While round robin is the default table type being explicit in your DDL is considered a best practice so that the intentions of your table layout are clear to others.</span></span>
>
>

### <a name="hash-distributed-tables"></a><span data-ttu-id="60f3c-159">Tabelas distribuídas por hash</span><span class="sxs-lookup"><span data-stu-id="60f3c-159">Hash Distributed Tables</span></span>
<span data-ttu-id="60f3c-160">Usar um algoritmo **Distribuído por hash** para distribuir suas tabelas pode melhorar o desempenho em muitos cenários, reduzindo a movimentação de dados no momento da consulta.</span><span class="sxs-lookup"><span data-stu-id="60f3c-160">Using a **Hash distributed** algorithm to distribute your tables can improve performance for many scenarios by reducing data movement at query time.</span></span>  <span data-ttu-id="60f3c-161">As tabelas distribuídas por hash são tabelas divididas entre os bancos de dados distribuídos usando um algoritmo de hash em uma única coluna que você seleciona.</span><span class="sxs-lookup"><span data-stu-id="60f3c-161">Hash distributed tables are tables which are divided between the distributed databases using a hashing algorithm on a single column which you select.</span></span>  <span data-ttu-id="60f3c-162">A coluna de distribuição é o que determina como os dados são divididos em seus bancos de dados distribuídos.</span><span class="sxs-lookup"><span data-stu-id="60f3c-162">The distribution column is what determines how the data is divided across your distributed databases.</span></span>  <span data-ttu-id="60f3c-163">A função de hash usa a coluna de distribuição para atribuir linhas a distribuições.</span><span class="sxs-lookup"><span data-stu-id="60f3c-163">The hash function uses the distribution column to assign rows to distributions.</span></span>  <span data-ttu-id="60f3c-164">O algoritmo de hash e a distribuição resultante são determinísticos.</span><span class="sxs-lookup"><span data-stu-id="60f3c-164">The hashing algorithm and resulting distribution is deterministic.</span></span>  <span data-ttu-id="60f3c-165">Isso é, o mesmo valor com o mesmo tipo de dados sempre terá a mesma distribuição.</span><span class="sxs-lookup"><span data-stu-id="60f3c-165">That is the same value with the same data type will always has to the same distribution.</span></span>    

<span data-ttu-id="60f3c-166">Este exemplo criará uma tabela distribuída na ID:</span><span class="sxs-lookup"><span data-stu-id="60f3c-166">This example will create a table distributed on id:</span></span>

```SQL
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
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
,  DISTRIBUTION = HASH([ProductKey])
)
;
```

## <a name="select-distribution-column"></a><span data-ttu-id="60f3c-167">Selecionar coluna de distribuição</span><span class="sxs-lookup"><span data-stu-id="60f3c-167">Select distribution column</span></span>
<span data-ttu-id="60f3c-168">Quando você opta por **distribuir uma tabela por hash** , precisa selecionar uma coluna de distribuição individual.</span><span class="sxs-lookup"><span data-stu-id="60f3c-168">When you choose to **hash distribute** a table, you will need to select a single distribution column.</span></span>  <span data-ttu-id="60f3c-169">Ao selecionar uma coluna de distribuição, três principais fatores deverão ser considerados.</span><span class="sxs-lookup"><span data-stu-id="60f3c-169">When selecting a distribution column, there are three major factors to consider.</span></span>  

<span data-ttu-id="60f3c-170">Selecione uma única coluna que:</span><span class="sxs-lookup"><span data-stu-id="60f3c-170">Select a single column which will:</span></span>

1. <span data-ttu-id="60f3c-171">Não será atualizada</span><span class="sxs-lookup"><span data-stu-id="60f3c-171">Not be updated</span></span>
2. <span data-ttu-id="60f3c-172">Distribuirá os dados uniformemente, evitando a distorção de dados</span><span class="sxs-lookup"><span data-stu-id="60f3c-172">Distribute data evenly, avoiding data skew</span></span>
3. <span data-ttu-id="60f3c-173">Minimizar a movimentação de dados</span><span class="sxs-lookup"><span data-stu-id="60f3c-173">Minimize data movement</span></span>

### <a name="select-distribution-column-which-will-not-be-updated"></a><span data-ttu-id="60f3c-174">Selecionar a coluna de distribuição que não será atualizada</span><span class="sxs-lookup"><span data-stu-id="60f3c-174">Select distribution column which will not be updated</span></span>
<span data-ttu-id="60f3c-175">As colunas de distribuição não são atualizáveis. Portanto, selecione uma coluna com valores estáticos.</span><span class="sxs-lookup"><span data-stu-id="60f3c-175">Distribution columns are not updatable, therefore, select a column with static values.</span></span>  <span data-ttu-id="60f3c-176">Se uma coluna precisar ser atualizada, ela geralmente não será uma candidata a distribuição válida.</span><span class="sxs-lookup"><span data-stu-id="60f3c-176">If a column will need to be updated, it is generally not a good distribution candidate.</span></span>  <span data-ttu-id="60f3c-177">Se você precisar atualizar uma coluna de distribuição, isso pode ser feito excluindo a linha e inserindo uma nova linha.</span><span class="sxs-lookup"><span data-stu-id="60f3c-177">If there is a case where you must update a distribution column, this can be done by first deleting the row and then inserting a new row.</span></span>

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a><span data-ttu-id="60f3c-178">Selecionar a coluna de distribuição que distribuirá os dados uniformemente</span><span class="sxs-lookup"><span data-stu-id="60f3c-178">Select distribution column which will distribute data evenly</span></span>
<span data-ttu-id="60f3c-179">Como a velocidade máxima de um sistema distribuído é a sua distribuição mais lenta, é importante dividir o trabalho igualmente entre as distribuições para conseguir uma execução equilibrada em todo o sistema.</span><span class="sxs-lookup"><span data-stu-id="60f3c-179">Since a distributed system performs only as fast as its slowest distribution, it is important to divide the work evenly across the distributions in order to achieve balanced execution across the system.</span></span>  <span data-ttu-id="60f3c-180">A forma como o trabalho é dividido em um sistema distribuído baseia-se em onde residem os dados de cada distribuição.</span><span class="sxs-lookup"><span data-stu-id="60f3c-180">The way the work is divided on a distributed system is based on where the data for each distribution lives.</span></span>  <span data-ttu-id="60f3c-181">Isso faz com que a seleção da coluna de distribuição correta para distribuir os dados seja muito importante, para que cada distribuição possua a mesma quantidade de trabalho e leve o mesmo tempo para concluir sua parte do trabalho.</span><span class="sxs-lookup"><span data-stu-id="60f3c-181">This makes it very important to select the right distribution column for distributing the data so that each distribution has equal work and will take the same time to complete its portion of the work.</span></span>  <span data-ttu-id="60f3c-182">Quando o trabalho é bem dividido em todo o sistema, os dados são equilibrados entre as distribuições.</span><span class="sxs-lookup"><span data-stu-id="60f3c-182">When work is well divided across the system, the data is balanced across the distributions.</span></span>  <span data-ttu-id="60f3c-183">Quando os dados não são equilibrados igualmente, chamamos esse evento de **distorção de dados**.</span><span class="sxs-lookup"><span data-stu-id="60f3c-183">When data is not evenly balanced, we call this **data skew**.</span></span>  

<span data-ttu-id="60f3c-184">Para dividir os dados uniformemente e evitar a distorção de dados, considere o seguinte ao selecionar a coluna de distribuição:</span><span class="sxs-lookup"><span data-stu-id="60f3c-184">To divide data evenly and avoid data skew, consider the following when selecting your distribution column:</span></span>

1. <span data-ttu-id="60f3c-185">Selecione uma coluna quem contenha um número significativo de valores distintos.</span><span class="sxs-lookup"><span data-stu-id="60f3c-185">Select a column which contains a significant number of distinct values.</span></span>
2. <span data-ttu-id="60f3c-186">Evite a distribuição de dados em colunas com poucos valores distintos.</span><span class="sxs-lookup"><span data-stu-id="60f3c-186">Avoid distributing data on columns with a few distinct values.</span></span>
3. <span data-ttu-id="60f3c-187">Evite a distribuição de dados em colunas com uma alta frequência de valores nulos.</span><span class="sxs-lookup"><span data-stu-id="60f3c-187">Avoid distributing data on columns with a high frequency of nulls.</span></span>
4. <span data-ttu-id="60f3c-188">Evite a distribuição de dados em colunas de data.</span><span class="sxs-lookup"><span data-stu-id="60f3c-188">Avoid distributing data on date columns.</span></span>

<span data-ttu-id="60f3c-189">Já que cada valor é distribuído por hash para uma das 60 distribuições, para conseguir uma distribuição uniforme, você deverá selecionar uma coluna que seja altamente exclusiva e que forneça mais de 60 valores exclusivos.</span><span class="sxs-lookup"><span data-stu-id="60f3c-189">Since each value is hashed to 1 of 60 distributions, to achieve even distribution you will want to select a column that is highly unique and contains more than 60 unique values.</span></span>  <span data-ttu-id="60f3c-190">Para ilustrar, considere o caso em que a coluna tenha apenas 40 valores exclusivos.</span><span class="sxs-lookup"><span data-stu-id="60f3c-190">To illustrate, consider a case where a column only has 40 unique values.</span></span>  <span data-ttu-id="60f3c-191">Se esta coluna tivesse sido selecionada como a chave de distribuição, os dados da tabela acabariam em 40 distribuições no máximo, deixando 20 distribuições sem nenhum processamento ou dados.</span><span class="sxs-lookup"><span data-stu-id="60f3c-191">If this column was selected as the distribution key, the data for that table would land on 40 distributions at most, leaving 20 distributions with no data and no processing to do.</span></span>  <span data-ttu-id="60f3c-192">Por outro lado, as outras 40 distribuições teriam mais trabalho a fazer do que se os dados fossem espalhados uniformemente entre as 60 distribuições.</span><span class="sxs-lookup"><span data-stu-id="60f3c-192">Conversely, the other 40 distributions would have more work to do that if the data was evenly spread over 60 distributions.</span></span>  <span data-ttu-id="60f3c-193">Esse cenário é um exemplo de distorção de dados.</span><span class="sxs-lookup"><span data-stu-id="60f3c-193">This scenario is an example of data skew.</span></span>

<span data-ttu-id="60f3c-194">No sistema MPP, cada etapa de consulta aguarda todas as distribuições concluírem sua parte do trabalho.</span><span class="sxs-lookup"><span data-stu-id="60f3c-194">In MPP system, each query step waits for all distributions to complete their share of the work.</span></span>  <span data-ttu-id="60f3c-195">Se uma distribuição estiver fazendo mais trabalho do que as outras, o recurso das outras distribuições serão essencialmente desperdiçados enquanto aguardam a distribuição ocupada.</span><span class="sxs-lookup"><span data-stu-id="60f3c-195">If one distribution is doing more work than the others, then the resource of the other distributions are essentially wasted just waiting on the busy distribution.</span></span>  <span data-ttu-id="60f3c-196">Quando o trabalho não é distribuído de maneira uniforme entre todas as distribuições, nós chamamos este evento de **distorção de processamento**.</span><span class="sxs-lookup"><span data-stu-id="60f3c-196">When work is not evenly spread across all distributions, we call this **processing skew**.</span></span>  <span data-ttu-id="60f3c-197">A distorção de processamento fará com que as consultas sejam executadas de forma mais lenta do que se a carga de trabalho pudesse ser distribuída de modo uniforme entre as distribuições.</span><span class="sxs-lookup"><span data-stu-id="60f3c-197">Processing skew will cause queries to run slower than if the workload can be evenly spread across the distributions.</span></span>  <span data-ttu-id="60f3c-198">A distorção de dados levará à distorção de processamento.</span><span class="sxs-lookup"><span data-stu-id="60f3c-198">Data skew will lead to processing skew.</span></span>

<span data-ttu-id="60f3c-199">Evite distribuir na coluna altamente anulável, uma vez que os valores nulos serão levados na mesma distribuição.</span><span class="sxs-lookup"><span data-stu-id="60f3c-199">Avoid distributing on highly nullable column as the null values will all land on the same distribution.</span></span> <span data-ttu-id="60f3c-200">A distribuição em uma coluna de data também pode causar a distorção de processamento porque todos os dados de uma determinada data serão levados para a mesma distribuição.</span><span class="sxs-lookup"><span data-stu-id="60f3c-200">Distributing on a date column can also cause processing skew because all data for a given date will land on the same distribution.</span></span> <span data-ttu-id="60f3c-201">Se vários usuários estiverem executando consultas e todos estiverem filtrando na mesma data, apenas uma das 60 distribuições estará fazendo todo o trabalho, visto que uma determinada data estará somente em uma distribuição.</span><span class="sxs-lookup"><span data-stu-id="60f3c-201">If several users are executing queries all filtering on the same date, then only 1 of the 60 distributions will be doing all of the work since a given date will only be on one distribution.</span></span> <span data-ttu-id="60f3c-202">Neste cenário, as consultas provavelmente serão executadas de forma 60 vezes mais lenta do que se os dados fossem divididos igualmente por todas as distribuições.</span><span class="sxs-lookup"><span data-stu-id="60f3c-202">In this scenario, the queries will likely run 60 times slower than if the data were equally spread over all of the distributions.</span></span>

<span data-ttu-id="60f3c-203">Quando não há colunas adequadas, considere o uso de round robin como método de distribuição.</span><span class="sxs-lookup"><span data-stu-id="60f3c-203">When no good candidate columns exist, then consider using round robin as the distribution method.</span></span>

### <a name="select-distribution-column-which-will-minimize-data-movement"></a><span data-ttu-id="60f3c-204">Selecione a coluna de distribuição que irá minimizar a movimentação de dados</span><span class="sxs-lookup"><span data-stu-id="60f3c-204">Select distribution column which will minimize data movement</span></span>
<span data-ttu-id="60f3c-205">Minimizar a movimentação de dados selecionando a coluna de distribuição correta é uma das estratégias mais importantes para otimizar o desempenho do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="60f3c-205">Minimizing data movement by selecting the right distribution column is one of the most important strategies for optimizing performance of your SQL Data Warehouse.</span></span>  <span data-ttu-id="60f3c-206">A movimentação de dados geralmente surge quando tabelas são unidas ou são executadas agregações.</span><span class="sxs-lookup"><span data-stu-id="60f3c-206">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="60f3c-207">Todas as colunas usadas nas cláusulas `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` e `HAVING` são candidatas à **boa** distribuição de hash.</span><span class="sxs-lookup"><span data-stu-id="60f3c-207">Columns used in `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` and `HAVING` clauses all make for **good** hash distribution candidates.</span></span>

<span data-ttu-id="60f3c-208">Por outro lado, as colunas na cláusula `WHERE`**não** são boas para a coluna de hash porque elas limitam quais distribuições participam da consulta, causando a distorção do processamento.</span><span class="sxs-lookup"><span data-stu-id="60f3c-208">On the other hand, columns in the `WHERE` clause do **not** make for good hash column candidates because they limit which distributions participate in the query, causing processing skew.</span></span>  <span data-ttu-id="60f3c-209">Um bom exemplo de uma coluna que pode ser convidativa para distribuir, mas geralmente pode causar essa distorção de processamento, é uma coluna de data.</span><span class="sxs-lookup"><span data-stu-id="60f3c-209">A good example of a column which might be tempting to distribute on, but often can cause this processing skew is a date column.</span></span>

<span data-ttu-id="60f3c-210">Em termos gerais, se tiver duas tabelas de fatos grande frequentemente envolvidas em uma associação, você obterá mais desempenho distribuindo ambas as tabelas em uma das colunas de junção.</span><span class="sxs-lookup"><span data-stu-id="60f3c-210">Generally speaking, if you have two large fact tables frequently involved in a join, you will gain the most performance by distributing both tables on one of the join columns.</span></span>  <span data-ttu-id="60f3c-211">Se você tiver uma tabela que nunca foi unida a outra tabela de fatos grande, procure as colunas que estão frequentemente na cláusula `GROUP BY` .</span><span class="sxs-lookup"><span data-stu-id="60f3c-211">If you have a table that is never joined to another large fact table, then look to columns that are frequently in the `GROUP BY` clause.</span></span>

<span data-ttu-id="60f3c-212">Há alguns critérios principais que devem ser atendidos para evitar a movimentação de dados durante uma junção:</span><span class="sxs-lookup"><span data-stu-id="60f3c-212">There are a few key criteria which must be met to avoid data movement during a join:</span></span>

1. <span data-ttu-id="60f3c-213">As tabelas envolvidas na junção devem ser distribuídas por hash em **uma** das colunas que participam da junção.</span><span class="sxs-lookup"><span data-stu-id="60f3c-213">The tables involved in the join must be hash distributed on **one** of the columns participating in the join.</span></span>
2. <span data-ttu-id="60f3c-214">Os tipos de dados das colunas de junção devem ser correspondentes entre as duas tabelas.</span><span class="sxs-lookup"><span data-stu-id="60f3c-214">The data types of the join columns must match between both tables.</span></span>
3. <span data-ttu-id="60f3c-215">As colunas devem ser associadas com um operador equals.</span><span class="sxs-lookup"><span data-stu-id="60f3c-215">The columns must be joined with an equals operator.</span></span>
4. <span data-ttu-id="60f3c-216">O tipo de associação pode não ser uma `CROSS JOIN`.</span><span class="sxs-lookup"><span data-stu-id="60f3c-216">The join type may not be a `CROSS JOIN`.</span></span>

## <a name="troubleshooting-data-skew"></a><span data-ttu-id="60f3c-217">Solucionando problemas de distorção de dados</span><span class="sxs-lookup"><span data-stu-id="60f3c-217">Troubleshooting data skew</span></span>
<span data-ttu-id="60f3c-218">Quando os dados da tabela são distribuídos usando o método de distribuição de hash, é possível que algumas distribuições sejam distorcidas para ter desproporcionalmente mais dados que outras.</span><span class="sxs-lookup"><span data-stu-id="60f3c-218">When table data is distributed using the hash distribution method there is a chance that some distributions will be skewed to have disproportionately more data than others.</span></span> <span data-ttu-id="60f3c-219">A distorção de dados em excesso pode afetar o desempenho de consulta porque o resultado final de uma consulta distribuída precisa aguardar até que a distribuição de execução mais longa termine.</span><span class="sxs-lookup"><span data-stu-id="60f3c-219">Excessive data skew can impact query performance because the final result of a distributed query must wait for the longest running distribution to finish.</span></span> <span data-ttu-id="60f3c-220">Dependendo do grau da distorção de dados, pode ser necessário tratá-lo.</span><span class="sxs-lookup"><span data-stu-id="60f3c-220">Depending on the degree of the data skew you might need to address it.</span></span>

### <a name="identifying-skew"></a><span data-ttu-id="60f3c-221">Identificando distorções</span><span class="sxs-lookup"><span data-stu-id="60f3c-221">Identifying skew</span></span>
<span data-ttu-id="60f3c-222">Uma maneira simples de identificar uma tabela como distorcida é usar `DBCC PDW_SHOWSPACEUSED`.</span><span class="sxs-lookup"><span data-stu-id="60f3c-222">A simple way to identify a table as skewed is to use `DBCC PDW_SHOWSPACEUSED`.</span></span>  <span data-ttu-id="60f3c-223">Esta é uma maneira simples e rápida de ver o número de linhas da tabela que estão armazenadas em cada uma das 60 distribuições do seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="60f3c-223">This is a very quick and simple way to see the number of table rows that are stored in each of the 60 distributions of your database.</span></span>  <span data-ttu-id="60f3c-224">Lembre-se que, para um desempenho mais equilibrado, as linhas na tabela distribuída devem ser divididas uniformemente entre todas as distribuições.</span><span class="sxs-lookup"><span data-stu-id="60f3c-224">Remember that for the most balanced performance, the rows in your distributed table should be spread evenly across all the distributions.</span></span>

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="60f3c-225">No entanto, se você consultar as exibições de gerenciamento dinâmico do Azure SQL Data Warehouse (DMV), poderá executar uma análise mais detalhada.</span><span class="sxs-lookup"><span data-stu-id="60f3c-225">However, if you query the Azure SQL Data Warehouse dynamic management views (DMV) you can perform a more detailed analysis.</span></span>  <span data-ttu-id="60f3c-226">Para começar, crie o modo de exibição [dbo.vTableSizes][dbo.vTableSizes] usando o SQL do artigo [Visão geral da tabela][Overview].</span><span class="sxs-lookup"><span data-stu-id="60f3c-226">To start, create the view [dbo.vTableSizes][dbo.vTableSizes] view using the SQL from [Table Overview][Overview] article.</span></span>  <span data-ttu-id="60f3c-227">Depois que a exibição é criada, execute esta consulta para identificar quais tabelas têm mais de 10% de distorção de dados.</span><span class="sxs-lookup"><span data-stu-id="60f3c-227">Once the view is created, run this query to identify which tables have more than 10% data skew.</span></span>

```sql
select *
from dbo.vTableSizes
where two_part_name in
    (
    select two_part_name
    from dbo.vTableSizes
    where row_count > 0
    group by two_part_name
    having min(row_count * 1.000)/max(row_count * 1.000) > .10
    )
order by two_part_name, row_count
;
```

### <a name="resolving-data-skew"></a><span data-ttu-id="60f3c-228">Resolvendo distorções de dados</span><span class="sxs-lookup"><span data-stu-id="60f3c-228">Resolving data skew</span></span>
<span data-ttu-id="60f3c-229">Nem toda distorção é suficiente para exigir uma correção.</span><span class="sxs-lookup"><span data-stu-id="60f3c-229">Not all skew is enough to warrant a fix.</span></span>  <span data-ttu-id="60f3c-230">Em alguns casos, o desempenho de uma tabela em algumas consultas pode superar os danos de distorção de dados.</span><span class="sxs-lookup"><span data-stu-id="60f3c-230">In some cases, the performance of a table in some queries can outweigh the harm of data skew.</span></span>  <span data-ttu-id="60f3c-231">Para decidir se deve resolver a distorção de dados em uma tabela, você deve compreender o máximo possível sobre os volumes de dados e consultas na carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="60f3c-231">To decide if you should resolve data skew in a table, you should understand as much as possible about the data volumes and queries in your workload.</span></span>   <span data-ttu-id="60f3c-232">Uma maneira de observar o impacto da distorção é usar as etapas do artigo [Consultar monitoramento][Query Monitoring] para monitorar o impacto da distorção no desempenho da consulta e, especificamente, o impacto sobre o tempo usado para conclusão das consultas nas distribuições individuais.</span><span class="sxs-lookup"><span data-stu-id="60f3c-232">One way to look at the impact of skew is to use the steps in the [Query Monitoring][Query Monitoring] article to monitor the impact of skew on query performance and specifically the impact to how long queries take to complete on the individual distributions.</span></span>

<span data-ttu-id="60f3c-233">A distribuição de dados é uma questão de encontrar o equilíbrio certo entre minimizar a distorção de dados e minimizar a movimentação de dados.</span><span class="sxs-lookup"><span data-stu-id="60f3c-233">Distributing data is a matter of finding the right balance between minimizing data skew and minimizing data movement.</span></span> <span data-ttu-id="60f3c-234">Esses podem ser objetivos opostos e, às vezes, você desejará manter a distorção de dados para reduzir a movimentação de dados.</span><span class="sxs-lookup"><span data-stu-id="60f3c-234">These can be opposing goals, and sometimes you will want to keep data skew in order to reduce data movement.</span></span> <span data-ttu-id="60f3c-235">Por exemplo, quando a coluna de distribuição com frequência é a coluna compartilhada em junções e agregações, você vai minimizar a movimentação de dados.</span><span class="sxs-lookup"><span data-stu-id="60f3c-235">For example, when the distribution column is frequently the shared column in joins and aggregations, you will be minimizing data movement.</span></span> <span data-ttu-id="60f3c-236">O benefício de ter o mínimo de movimentação de dados pode superar o impacto de ter a distorção de dados.</span><span class="sxs-lookup"><span data-stu-id="60f3c-236">The benefit of having the minimal data movement might outweigh the impact of having data skew.</span></span>

<span data-ttu-id="60f3c-237">A maneira comum de resolver a distorção de dados é recriar a tabela com uma coluna de distribuição diferente.</span><span class="sxs-lookup"><span data-stu-id="60f3c-237">The typical way to resolve data skew is to re-create the table with a different distribution column.</span></span> <span data-ttu-id="60f3c-238">Como não há nenhuma maneira de alterar a coluna de distribuição em uma tabela existente, a maneira de alterar a distribuição de uma tabela é recriá-la com [CTAS][].</span><span class="sxs-lookup"><span data-stu-id="60f3c-238">Since there is no way to change the distribution column on an existing table, the way to change the distribution of a table it to recreate it with a [CTAS][].</span></span>  <span data-ttu-id="60f3c-239">Aqui estão dois exemplos de como resolver a distorção de dados:</span><span class="sxs-lookup"><span data-stu-id="60f3c-239">Here are two examples of how resolve data skew:</span></span>

### <a name="example-1-re-create-the-table-with-a-new-distribution-column"></a><span data-ttu-id="60f3c-240">Exemplo 1: criar novamente a tabela com uma nova coluna de distribuição</span><span class="sxs-lookup"><span data-stu-id="60f3c-240">Example 1: Re-create the table with a new distribution column</span></span>
<span data-ttu-id="60f3c-241">Este exemplo usa [CTAS][] para recriar uma tabela com uma coluna de distribuição de hash diferente.</span><span class="sxs-lookup"><span data-stu-id="60f3c-241">This example uses [CTAS][] to re-create a table with a different hash distribution column.</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_CustomerKey]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  HASH([CustomerKey])
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_CustomerKey')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_CustomerKey] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_CustomerKey] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_CustomerKey] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_CustomerKey] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_CustomerKey] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_CustomerKey] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_CustomerKey] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_CustomerKey] ([SalesAmount]);

--Rename the tables
RENAME OBJECT [dbo].[FactInternetSales] TO [FactInternetSales_ProductKey];
RENAME OBJECT [dbo].[FactInternetSales_CustomerKey] TO [FactInternetSales];
```

### <a name="example-2-re-create-the-table-using-round-robin-distribution"></a><span data-ttu-id="60f3c-242">Exemplo 2: recriar a tabela usando a distribuição round robin</span><span class="sxs-lookup"><span data-stu-id="60f3c-242">Example 2: Re-create the table using round robin distribution</span></span>
<span data-ttu-id="60f3c-243">Este exemplo usa [CTAS][] para recriar uma tabela com round robin em vez de uma distribuição por hash.</span><span class="sxs-lookup"><span data-stu-id="60f3c-243">This example uses [CTAS][] to re-create a table with round robin instead of a hash distribution.</span></span> <span data-ttu-id="60f3c-244">Essa alteração produzirá a distribuição uniforme de dados às custas de uma maior movimentação de dados.</span><span class="sxs-lookup"><span data-stu-id="60f3c-244">This change will produce even data distribution at the cost of increased data movement.</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_ROUND_ROBIN]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  ROUND_ROBIN
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_ROUND_ROBIN')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_ROUND_ROBIN] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_ROUND_ROBIN] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_ROUND_ROBIN] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_ROUND_ROBIN] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_ROUND_ROBIN] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_ROUND_ROBIN] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_ROUND_ROBIN] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_ROUND_ROBIN] ([SalesAmount]);

--Rename the tables
RENAME OBJECT [dbo].[FactInternetSales] TO [FactInternetSales_HASH];
RENAME OBJECT [dbo].[FactInternetSales_ROUND_ROBIN] TO [FactInternetSales];
```

## <a name="next-steps"></a><span data-ttu-id="60f3c-245">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="60f3c-245">Next steps</span></span>
<span data-ttu-id="60f3c-246">Para saber mais sobre o design da tabela, confira os artigos [Distribuir][Distribute], [Índice][Index], [Partição][Partition], [Tipos de dados][Data Types], [Estatísticas][Statistics] e [Tabelas temporárias][Temporary].</span><span class="sxs-lookup"><span data-stu-id="60f3c-246">To learn more about table design, see the [Distribute][Distribute], [Index][Index], [Partition][Partition], [Data Types][Data Types], [Statistics][Statistics] and [Temporary Tables][Temporary] articles.</span></span>

<span data-ttu-id="60f3c-247">Para obter uma visão geral das práticas recomendadas, confira [Práticas recomendadas para o SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="60f3c-247">For an overview of best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
[Query Monitoring]: ./sql-data-warehouse-manage-monitor.md
[dbo.vTableSizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries

<!--MSDN references-->
[DBCC PDW_SHOWSPACEUSED()]: https://msdn.microsoft.com/library/mt204028.aspx

<!--Other Web references-->
