---
title: tabelas de aaaDistributing no SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: 65093eeaeb00fef85aaa6070da2c976fed3f4bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="distributing-tables-in-sql-data-warehouse"></a><span data-ttu-id="88c26-103">Distribuindo tabelas no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="88c26-103">Distributing tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="88c26-104">[Visão geral][Overview]</span><span class="sxs-lookup"><span data-stu-id="88c26-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="88c26-105">[Tipos de Dados][Data Types]</span><span class="sxs-lookup"><span data-stu-id="88c26-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="88c26-106">[Distribuir][Distribute]</span><span class="sxs-lookup"><span data-stu-id="88c26-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="88c26-107">[Índice][Index]</span><span class="sxs-lookup"><span data-stu-id="88c26-107">[Index][Index]</span></span>
> * <span data-ttu-id="88c26-108">[Partição][Partition]</span><span class="sxs-lookup"><span data-stu-id="88c26-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="88c26-109">[Estatísticas][Statistics]</span><span class="sxs-lookup"><span data-stu-id="88c26-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="88c26-110">[Temporário][Temporary]</span><span class="sxs-lookup"><span data-stu-id="88c26-110">[Temporary][Temporary]</span></span>
>
>

<span data-ttu-id="88c26-111">SQL Data Warehouse é um sistema de banco de dados distribuído de processamento extremamente paralelo (MPP).</span><span class="sxs-lookup"><span data-stu-id="88c26-111">SQL Data Warehouse is a massively parallel processing (MPP) distributed database system.</span></span>  <span data-ttu-id="88c26-112">Ao dividir os dados e a funcionalidade de processamento em vários nós, o SQL Data Warehouse pode oferecer uma enorme escalabilidade, muito além de qualquer sistema individual.</span><span class="sxs-lookup"><span data-stu-id="88c26-112">By dividing data and processing capability across multiple nodes, SQL Data Warehouse can offer huge scalability - far beyond any single system.</span></span>  <span data-ttu-id="88c26-113">Decidir como toodistribute seus dados no Data Warehouse do SQL são uma saudação mais importante fatores tooachieving o desempenho ideal.</span><span class="sxs-lookup"><span data-stu-id="88c26-113">Deciding how toodistribute your data within your SQL Data Warehouse is one of hello most important factors tooachieving optimal performance.</span></span>   <span data-ttu-id="88c26-114">desempenho de chave toooptimal Olá é minimizar a movimentação de dados e por sua vez movimentação de dados de chave toominimizing Olá é selecionando estratégia de distribuição direita hello.</span><span class="sxs-lookup"><span data-stu-id="88c26-114">hello key toooptimal performance is minimizing data movement and in turn hello key toominimizing data movement is selecting hello right distribution strategy.</span></span>

## <a name="understanding-data-movement"></a><span data-ttu-id="88c26-115">Noções básicas sobre a movimentação de dados</span><span class="sxs-lookup"><span data-stu-id="88c26-115">Understanding data movement</span></span>
<span data-ttu-id="88c26-116">Em um sistema MPP, dados de saudação de cada tabela são divididos em vários bancos de dados subjacentes.</span><span class="sxs-lookup"><span data-stu-id="88c26-116">In an MPP system, hello data from each table is divided across several underlying databases.</span></span>  <span data-ttu-id="88c26-117">consultas Hello mais otimizado em um sistema MPP podem simplesmente ser passadas tooexecute em Olá individuais bancos de dados distribuídos sem a interação entre Olá outros bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="88c26-117">hello most optimized queries on an MPP system can simply be passed through tooexecute on hello individual distributed databases with no interaction between hello other databases.</span></span>  <span data-ttu-id="88c26-118">Por exemplo, digamos que você tenha um banco de dados com dados de vendas que contém duas tabelas, vendas e clientes.</span><span class="sxs-lookup"><span data-stu-id="88c26-118">For example, let's say you have a database with sales data which contains two tables, sales and customers.</span></span>  <span data-ttu-id="88c26-119">Se você tiver uma consulta que precisa toojoin sua tabela de cliente tooyour tabela de vendas e você dividir vendas e tabelas de cliente para cima pelo número de clientes, colocando cada cliente em um banco de dados, todas as consultas que unem vendas e clientes podem ser resolvidas dentro de cada banco de dados sem conhecimento de Olá outros bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="88c26-119">If you have a query that needs toojoin your sales table tooyour customer table and you divide both your sales and customer tables up by customer number, putting each customer in a separate database, any queries which join sales and customer can be solved within each database with no knowledge of hello other databases.</span></span>  <span data-ttu-id="88c26-120">Por outro lado, se seus dados de vendas é dividido pelo número de ordem e dados do cliente por número de cliente, em seguida, determinado banco de dados não terá dados correspondentes Olá para cada cliente e, portanto, se você quisesse toojoin seus dados de cliente de tooyour de dados de vendas, você precisaria tooget hello dados para cada cliente da saudação outros bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="88c26-120">In contrast, if you divided your sales data by order number and your customer data by customer number, then any given database will not have hello corresponding data for each customer and thus if you wanted toojoin your sales data tooyour customer data, you would need tooget hello data for each customer from hello other databases.</span></span>  <span data-ttu-id="88c26-121">No segundo exemplo, a movimentação de dados necessário toooccur toomove Olá dados toohello vendas dados do cliente, para que Olá duas tabelas podem ser unidas.</span><span class="sxs-lookup"><span data-stu-id="88c26-121">In this second example, data movement would need toooccur toomove hello customer data toohello sales data, so that hello two tables can be joined.</span></span>  

<span data-ttu-id="88c26-122">Movimentação de dados nem sempre é ruim, às vezes é necessário toosolve uma consulta.</span><span class="sxs-lookup"><span data-stu-id="88c26-122">Data movement isn't always a bad thing, sometimes it's necessary toosolve a query.</span></span>  <span data-ttu-id="88c26-123">Porém, quando essa etapa extra pode ser evitada, naturalmente a consulta é executada mais depressa.</span><span class="sxs-lookup"><span data-stu-id="88c26-123">But when this extra step can be avoided, naturally your query will run faster.</span></span>  <span data-ttu-id="88c26-124">A movimentação de dados geralmente surge quando tabelas são unidas ou são executadas agregações.</span><span class="sxs-lookup"><span data-stu-id="88c26-124">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="88c26-125">Geralmente, é necessário toodo ambos, portanto enquanto você poderá toooptimize para um cenário, como uma junção, você ainda precisa toohelp de movimentação de dados para resolver Olá outro cenário, como uma agregação.</span><span class="sxs-lookup"><span data-stu-id="88c26-125">Often you need toodo both, so while you may be able toooptimize for one scenario, like a join, you still need data movement toohelp you solve for hello other scenario, like an aggregation.</span></span>  <span data-ttu-id="88c26-126">truque Olá é descobrir qual é o menos trabalho.</span><span class="sxs-lookup"><span data-stu-id="88c26-126">hello trick is figuring out which is less work.</span></span>  <span data-ttu-id="88c26-127">Na maioria dos casos, a distribuição de grandes tabelas de fatos em uma coluna normalmente associada é Olá método mais eficaz para reduzir a saudação mais a movimentação de dados.</span><span class="sxs-lookup"><span data-stu-id="88c26-127">In most cases, distributing large fact tables on a commonly joined column is hello most effective method for reducing hello most data movement.</span></span>  <span data-ttu-id="88c26-128">Distribuição de dados em colunas de junção é uma movimentação de dados de tooreduce método muito mais comum de distribuir dados em colunas envolvidas em uma agregação.</span><span class="sxs-lookup"><span data-stu-id="88c26-128">Distributing data on join columns is a much more common method tooreduce data movement than distributing data on columns involved in an aggregation.</span></span>

## <a name="select-distribution-method"></a><span data-ttu-id="88c26-129">Selecionar método de distribuição</span><span class="sxs-lookup"><span data-stu-id="88c26-129">Select distribution method</span></span>
<span data-ttu-id="88c26-130">Em segundo plano hello, o SQL Data Warehouse divide os dados em 60 bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="88c26-130">Behind hello scenes, SQL Data Warehouse divides your data into 60 databases.</span></span>  <span data-ttu-id="88c26-131">Cada banco de dados individual é chamado tooas um **distribuição**.</span><span class="sxs-lookup"><span data-stu-id="88c26-131">Each individual database is referred tooas a **distribution**.</span></span>  <span data-ttu-id="88c26-132">Quando dados são carregados em cada tabela, o SQL Data Warehouse tem tooknow como toodivide seus dados em 60 distribuições.</span><span class="sxs-lookup"><span data-stu-id="88c26-132">When data is loaded into each table, SQL Data Warehouse has tooknow how toodivide your data across these 60 distributions.</span></span>  

<span data-ttu-id="88c26-133">método de distribuição de saudação é definido no nível de tabela hello e atualmente, há duas opções:</span><span class="sxs-lookup"><span data-stu-id="88c26-133">hello distribution method is defined at hello table level and currently there are two choices:</span></span>

1. <span data-ttu-id="88c26-134">**Round robin** , que distribui dados uniformemente, mas aleatoriamente.</span><span class="sxs-lookup"><span data-stu-id="88c26-134">**Round robin** which distribute data evenly but randomly.</span></span>
2. <span data-ttu-id="88c26-135">**Distribuídos por hash** , que distribui dados baseados em valores de hash de uma única coluna</span><span class="sxs-lookup"><span data-stu-id="88c26-135">**Hash Distributed** which distributes data based on hashing values from a single column</span></span>

<span data-ttu-id="88c26-136">Por padrão, quando você não definir um método de distribuição de dados, sua tabela será distribuída usando Olá **rodízio** método de distribuição.</span><span class="sxs-lookup"><span data-stu-id="88c26-136">By default, when you do not define a data distribution method, your table will be distributed using hello **round robin** distribution method.</span></span>  <span data-ttu-id="88c26-137">No entanto, como se tornam mais sofisticadas em sua implementação, será conveniente usando tooconsider **hash distribuída** tabelas toominimize a movimentação de dados que por sua vez otimizar desempenho de consulta.</span><span class="sxs-lookup"><span data-stu-id="88c26-137">However, as you become more sophisticated in your implementation, you will want tooconsider using **hash distributed** tables toominimize data movement which will in turn optimize query performance.</span></span>

### <a name="round-robin-tables"></a><span data-ttu-id="88c26-138">Tabelas Round Robin</span><span class="sxs-lookup"><span data-stu-id="88c26-138">Round Robin Tables</span></span>
<span data-ttu-id="88c26-139">Usar Olá método Round Robin de distribuição de dados é muito como parece.</span><span class="sxs-lookup"><span data-stu-id="88c26-139">Using hello Round Robin method of distributing data is very much how it sounds.</span></span>  <span data-ttu-id="88c26-140">Como seus dados são carregados, cada linha é simplesmente enviada toohello próxima distribuição.</span><span class="sxs-lookup"><span data-stu-id="88c26-140">As your data is loaded, each row is simply sent toohello next distribution.</span></span>  <span data-ttu-id="88c26-141">Esse método de distribuição de dados saudação será sempre distribui aleatoriamente dados saudação muito uniformemente em todas as distribuições de saudação.</span><span class="sxs-lookup"><span data-stu-id="88c26-141">This method of distributing hello data will always randomly distribute hello data very evenly across all of hello distributions.</span></span>  <span data-ttu-id="88c26-142">Ou seja, não há nenhuma classificação feito durante a saudação round robin processo coloca seus dados.</span><span class="sxs-lookup"><span data-stu-id="88c26-142">That is, there is no sorting done during hello round robin process which places your data.</span></span>  <span data-ttu-id="88c26-143">Uma distribuição round robin é chamada às vezes de hash aleatório por esse motivo.</span><span class="sxs-lookup"><span data-stu-id="88c26-143">A round robin distribution is sometimes called a random hash for this reason.</span></span>  <span data-ttu-id="88c26-144">Com uma tabela distribuída round robin, não há nenhum dado de saudação do toounderstand de necessidade.</span><span class="sxs-lookup"><span data-stu-id="88c26-144">With a round-robin distributed table there is no need toounderstand hello data.</span></span>  <span data-ttu-id="88c26-145">Por esse motivo, as tabelas Round Robin normalmente são bons destinos de carregamento.</span><span class="sxs-lookup"><span data-stu-id="88c26-145">For this reason, Round-Robin tables often make good loading targets.</span></span>

<span data-ttu-id="88c26-146">Por padrão, se nenhum método de distribuição for escolhido, hello método de distribuição de round robin será usado.</span><span class="sxs-lookup"><span data-stu-id="88c26-146">By default, if no distribution method is chosen, hello round robin distribution method will be used.</span></span>  <span data-ttu-id="88c26-147">No entanto, enquanto as tabelas de rodízio são toouse fácil, porque os dados são distribuídos aleatoriamente sistema Olá significa que o sistema Olá não pode garantir qual distribuição cada linha são no.</span><span class="sxs-lookup"><span data-stu-id="88c26-147">However, while round robin tables are easy toouse, because data is randomly distributed across hello system it means that hello system can't guarantee which distribution each row is on.</span></span>  <span data-ttu-id="88c26-148">Como resultado, o sistema de hello, às vezes, precisa tooinvoke um toobetter de operação de movimentação de dados organize seus dados antes que ele possa resolver uma consulta.</span><span class="sxs-lookup"><span data-stu-id="88c26-148">As a result, hello system sometimes needs tooinvoke a data movement operation toobetter organize your data before it can resolve a query.</span></span>  <span data-ttu-id="88c26-149">Essa etapa extra pode causar lentidão em suas consultas.</span><span class="sxs-lookup"><span data-stu-id="88c26-149">This extra step can slow down your queries.</span></span>

<span data-ttu-id="88c26-150">Considere o uso de distribuição de Round Robin para a tabela na Olá os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="88c26-150">Consider using Round Robin distribution for your table in hello following scenarios:</span></span>

* <span data-ttu-id="88c26-151">Ao começar, como um simples ponto de partida</span><span class="sxs-lookup"><span data-stu-id="88c26-151">When getting started as a simple starting point</span></span>
* <span data-ttu-id="88c26-152">Se não houver uma chave de junção óbvia</span><span class="sxs-lookup"><span data-stu-id="88c26-152">If there is no obvious joining key</span></span>
* <span data-ttu-id="88c26-153">Se não houver coluna boa candidata para hash distribuindo tabela Olá</span><span class="sxs-lookup"><span data-stu-id="88c26-153">If there is not good candidate column for hash distributing hello table</span></span>
* <span data-ttu-id="88c26-154">Se hello tabela não deve compartilhar uma chave de junção comum com outras tabelas</span><span class="sxs-lookup"><span data-stu-id="88c26-154">If hello table does not share a common join key with other tables</span></span>
* <span data-ttu-id="88c26-155">Se a junção Olá será menos significativa do que outras junções na consulta Olá</span><span class="sxs-lookup"><span data-stu-id="88c26-155">If hello join is less significant than other joins in hello query</span></span>
* <span data-ttu-id="88c26-156">Quando Olá é uma tabela de preparo temporária</span><span class="sxs-lookup"><span data-stu-id="88c26-156">When hello table is a temporary staging table</span></span>

<span data-ttu-id="88c26-157">Ambos os exemplos criarão uma tabela Round Robin:</span><span class="sxs-lookup"><span data-stu-id="88c26-157">Both of these examples will create a Round Robin Table:</span></span>

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
> <span data-ttu-id="88c26-158">Enquanto o round robin é o tipo de tabela padrão Olá sendo explícita no seu DDL é considerado uma prática recomendada para que intenções saudação de seu layout de tabela são tooothers clara.</span><span class="sxs-lookup"><span data-stu-id="88c26-158">While round robin is hello default table type being explicit in your DDL is considered a best practice so that hello intentions of your table layout are clear tooothers.</span></span>
>
>

### <a name="hash-distributed-tables"></a><span data-ttu-id="88c26-159">Tabelas distribuídas por hash</span><span class="sxs-lookup"><span data-stu-id="88c26-159">Hash Distributed Tables</span></span>
<span data-ttu-id="88c26-160">Usando um **Hash distribuída** algoritmo toodistribute suas tabelas podem melhorar o desempenho em muitos cenários, reduzindo a movimentação de dados no momento da consulta.</span><span class="sxs-lookup"><span data-stu-id="88c26-160">Using a **Hash distributed** algorithm toodistribute your tables can improve performance for many scenarios by reducing data movement at query time.</span></span>  <span data-ttu-id="88c26-161">Hash de tabelas distribuídas são aquelas que são divididas entre hello distribuído bancos de dados usando um algoritmo de hash em uma única coluna que você selecionar.</span><span class="sxs-lookup"><span data-stu-id="88c26-161">Hash distributed tables are tables which are divided between hello distributed databases using a hashing algorithm on a single column which you select.</span></span>  <span data-ttu-id="88c26-162">coluna de distribuição de saudação é o que determina como os dados saudação são divididos em seus bancos de dados distribuídos.</span><span class="sxs-lookup"><span data-stu-id="88c26-162">hello distribution column is what determines how hello data is divided across your distributed databases.</span></span>  <span data-ttu-id="88c26-163">função de hash Olá usa Olá distribuição coluna tooassign linhas toodistributions.</span><span class="sxs-lookup"><span data-stu-id="88c26-163">hello hash function uses hello distribution column tooassign rows toodistributions.</span></span>  <span data-ttu-id="88c26-164">Olá algoritmo de hash e distribuição resultante é determinística.</span><span class="sxs-lookup"><span data-stu-id="88c26-164">hello hashing algorithm and resulting distribution is deterministic.</span></span>  <span data-ttu-id="88c26-165">Ou seja, Olá mesmo valor com o mesmo tipo de dados será sempre de saudação tem toohello mesma distribuição.</span><span class="sxs-lookup"><span data-stu-id="88c26-165">That is hello same value with hello same data type will always has toohello same distribution.</span></span>    

<span data-ttu-id="88c26-166">Este exemplo criará uma tabela distribuída na ID:</span><span class="sxs-lookup"><span data-stu-id="88c26-166">This example will create a table distributed on id:</span></span>

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

## <a name="select-distribution-column"></a><span data-ttu-id="88c26-167">Selecionar coluna de distribuição</span><span class="sxs-lookup"><span data-stu-id="88c26-167">Select distribution column</span></span>
<span data-ttu-id="88c26-168">Quando você escolhe muito**hash distribuir** uma tabela, você precisará tooselect uma coluna de distribuição individuais.</span><span class="sxs-lookup"><span data-stu-id="88c26-168">When you choose too**hash distribute** a table, you will need tooselect a single distribution column.</span></span>  <span data-ttu-id="88c26-169">Ao selecionar uma coluna de distribuição, há tooconsider de três fatores principais.</span><span class="sxs-lookup"><span data-stu-id="88c26-169">When selecting a distribution column, there are three major factors tooconsider.</span></span>  

<span data-ttu-id="88c26-170">Selecione uma única coluna que:</span><span class="sxs-lookup"><span data-stu-id="88c26-170">Select a single column which will:</span></span>

1. <span data-ttu-id="88c26-171">Não será atualizada</span><span class="sxs-lookup"><span data-stu-id="88c26-171">Not be updated</span></span>
2. <span data-ttu-id="88c26-172">Distribuirá os dados uniformemente, evitando a distorção de dados</span><span class="sxs-lookup"><span data-stu-id="88c26-172">Distribute data evenly, avoiding data skew</span></span>
3. <span data-ttu-id="88c26-173">Minimizar a movimentação de dados</span><span class="sxs-lookup"><span data-stu-id="88c26-173">Minimize data movement</span></span>

### <a name="select-distribution-column-which-will-not-be-updated"></a><span data-ttu-id="88c26-174">Selecionar a coluna de distribuição que não será atualizada</span><span class="sxs-lookup"><span data-stu-id="88c26-174">Select distribution column which will not be updated</span></span>
<span data-ttu-id="88c26-175">As colunas de distribuição não são atualizáveis. Portanto, selecione uma coluna com valores estáticos.</span><span class="sxs-lookup"><span data-stu-id="88c26-175">Distribution columns are not updatable, therefore, select a column with static values.</span></span>  <span data-ttu-id="88c26-176">Se uma coluna precisará toobe atualizado, geralmente não é um candidato de distribuição válido.</span><span class="sxs-lookup"><span data-stu-id="88c26-176">If a column will need toobe updated, it is generally not a good distribution candidate.</span></span>  <span data-ttu-id="88c26-177">Se houver um caso em que você deve atualizar uma coluna de distribuição, isso pode ser feito primeiro excluindo linha hello e, em seguida, inserir uma nova linha.</span><span class="sxs-lookup"><span data-stu-id="88c26-177">If there is a case where you must update a distribution column, this can be done by first deleting hello row and then inserting a new row.</span></span>

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a><span data-ttu-id="88c26-178">Selecionar a coluna de distribuição que distribuirá os dados uniformemente</span><span class="sxs-lookup"><span data-stu-id="88c26-178">Select distribution column which will distribute data evenly</span></span>
<span data-ttu-id="88c26-179">Como um sistema distribuído executa somente tão rápida quanto sua distribuição mais lenta, é importante toodivide Olá trabalho uniformemente em distribuições de saudação em ordem tooachieve balanceada execução em todo sistema Olá.</span><span class="sxs-lookup"><span data-stu-id="88c26-179">Since a distributed system performs only as fast as its slowest distribution, it is important toodivide hello work evenly across hello distributions in order tooachieve balanced execution across hello system.</span></span>  <span data-ttu-id="88c26-180">forma de Olá Olá trabalho é dividido em um sistema distribuído baseia-se em onde residem os dados de saudação para cada distribuição.</span><span class="sxs-lookup"><span data-stu-id="88c26-180">hello way hello work is divided on a distributed system is based on where hello data for each distribution lives.</span></span>  <span data-ttu-id="88c26-181">Isso torna coluna de distribuição direita Olá tooselect muito importante para distribuir dados saudação para que cada distribuição tem trabalho igual e será take Olá mesmo toocomplete de tempo sua parte do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="88c26-181">This makes it very important tooselect hello right distribution column for distributing hello data so that each distribution has equal work and will take hello same time toocomplete its portion of hello work.</span></span>  <span data-ttu-id="88c26-182">Quando o trabalho também é dividido em todo sistema hello, dados de saudação são balanceados em distribuições de saudação.</span><span class="sxs-lookup"><span data-stu-id="88c26-182">When work is well divided across hello system, hello data is balanced across hello distributions.</span></span>  <span data-ttu-id="88c26-183">Quando os dados não são equilibrados igualmente, chamamos esse evento de **distorção de dados**.</span><span class="sxs-lookup"><span data-stu-id="88c26-183">When data is not evenly balanced, we call this **data skew**.</span></span>  

<span data-ttu-id="88c26-184">toodivide dados uniformemente e evitar a distorção de dados, considere a seguinte Olá ao selecionar a coluna de distribuição:</span><span class="sxs-lookup"><span data-stu-id="88c26-184">toodivide data evenly and avoid data skew, consider hello following when selecting your distribution column:</span></span>

1. <span data-ttu-id="88c26-185">Selecione uma coluna quem contenha um número significativo de valores distintos.</span><span class="sxs-lookup"><span data-stu-id="88c26-185">Select a column which contains a significant number of distinct values.</span></span>
2. <span data-ttu-id="88c26-186">Evite a distribuição de dados em colunas com poucos valores distintos.</span><span class="sxs-lookup"><span data-stu-id="88c26-186">Avoid distributing data on columns with a few distinct values.</span></span>
3. <span data-ttu-id="88c26-187">Evite a distribuição de dados em colunas com uma alta frequência de valores nulos.</span><span class="sxs-lookup"><span data-stu-id="88c26-187">Avoid distributing data on columns with a high frequency of nulls.</span></span>
4. <span data-ttu-id="88c26-188">Evite a distribuição de dados em colunas de data.</span><span class="sxs-lookup"><span data-stu-id="88c26-188">Avoid distributing data on date columns.</span></span>

<span data-ttu-id="88c26-189">Como cada valor de hash too1 de 60 distribuições, distribuição uniforme tooachieve você desejará tooselect uma coluna que é altamente exclusivo e contém mais de 60 valores exclusivos.</span><span class="sxs-lookup"><span data-stu-id="88c26-189">Since each value is hashed too1 of 60 distributions, tooachieve even distribution you will want tooselect a column that is highly unique and contains more than 60 unique values.</span></span>  <span data-ttu-id="88c26-190">tooillustrate, considere um caso em que a coluna tem apenas 40 valores exclusivos.</span><span class="sxs-lookup"><span data-stu-id="88c26-190">tooillustrate, consider a case where a column only has 40 unique values.</span></span>  <span data-ttu-id="88c26-191">Se esta coluna foi marcada como chave de distribuição Olá, dados Olá para aquela tabela acabaria em 40 distribuições no máximo, deixando 20 distribuições com nenhum dado e nenhum toodo de processamento.</span><span class="sxs-lookup"><span data-stu-id="88c26-191">If this column was selected as hello distribution key, hello data for that table would land on 40 distributions at most, leaving 20 distributions with no data and no processing toodo.</span></span>  <span data-ttu-id="88c26-192">Por outro lado, hello outras 40 distribuições teria mais toodo de trabalho que se hello dados foi distribuídos uniformemente distribuições mais de 60.</span><span class="sxs-lookup"><span data-stu-id="88c26-192">Conversely, hello other 40 distributions would have more work toodo that if hello data was evenly spread over 60 distributions.</span></span>  <span data-ttu-id="88c26-193">Esse cenário é um exemplo de distorção de dados.</span><span class="sxs-lookup"><span data-stu-id="88c26-193">This scenario is an example of data skew.</span></span>

<span data-ttu-id="88c26-194">No sistema MPP, cada etapa de consulta aguarda toocomplete de todas as distribuições seu compartilhamento de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="88c26-194">In MPP system, each query step waits for all distributions toocomplete their share of hello work.</span></span>  <span data-ttu-id="88c26-195">Se uma distribuição fazendo mais trabalho do hello outras pessoas, Olá recursos de saudação outras distribuições são essencialmente desperdiçadas espera na distribuição de saudação ocupado.</span><span class="sxs-lookup"><span data-stu-id="88c26-195">If one distribution is doing more work than hello others, then hello resource of hello other distributions are essentially wasted just waiting on hello busy distribution.</span></span>  <span data-ttu-id="88c26-196">Quando o trabalho não é distribuído de maneira uniforme entre todas as distribuições, nós chamamos este evento de **distorção de processamento**.</span><span class="sxs-lookup"><span data-stu-id="88c26-196">When work is not evenly spread across all distributions, we call this **processing skew**.</span></span>  <span data-ttu-id="88c26-197">Distorção de processamento fará com que consultas toorun mais lento do que se cargas de trabalho Olá possam ser distribuídas uniformemente em distribuições de saudação.</span><span class="sxs-lookup"><span data-stu-id="88c26-197">Processing skew will cause queries toorun slower than if hello workload can be evenly spread across hello distributions.</span></span>  <span data-ttu-id="88c26-198">Distorção de dados levará tooprocessing distorção.</span><span class="sxs-lookup"><span data-stu-id="88c26-198">Data skew will lead tooprocessing skew.</span></span>

<span data-ttu-id="88c26-199">Evitar a distribuição na coluna anulável altamente como valores nulos Olá todos verá Olá mesmo distribuição.</span><span class="sxs-lookup"><span data-stu-id="88c26-199">Avoid distributing on highly nullable column as hello null values will all land on hello same distribution.</span></span> <span data-ttu-id="88c26-200">Distribuindo em uma coluna de data também pode causar distorção de processamento porque todos os dados para uma determinada data serão levadas em Olá mesmo distribuição.</span><span class="sxs-lookup"><span data-stu-id="88c26-200">Distributing on a date column can also cause processing skew because all data for a given date will land on hello same distribution.</span></span> <span data-ttu-id="88c26-201">Se vários usuários estiverem executando consultas todos filtragem em Olá mesmo data, em seguida, apenas 1 de distribuições de 60 Olá fará todo o trabalho de saudação desde a data será apenas em uma distribuição.</span><span class="sxs-lookup"><span data-stu-id="88c26-201">If several users are executing queries all filtering on hello same date, then only 1 of hello 60 distributions will be doing all of hello work since a given date will only be on one distribution.</span></span> <span data-ttu-id="88c26-202">Nesse cenário, as consultas de saudação provavelmente serão executado 60 vezes mais lentos do que se os dados saudação foram igualmente distribuídos por todas as distribuições de saudação do.</span><span class="sxs-lookup"><span data-stu-id="88c26-202">In this scenario, hello queries will likely run 60 times slower than if hello data were equally spread over all of hello distributions.</span></span>

<span data-ttu-id="88c26-203">Quando nenhuma coluna de boa candidata existe, considere o uso de rodízio como método de distribuição hello.</span><span class="sxs-lookup"><span data-stu-id="88c26-203">When no good candidate columns exist, then consider using round robin as hello distribution method.</span></span>

### <a name="select-distribution-column-which-will-minimize-data-movement"></a><span data-ttu-id="88c26-204">Selecione a coluna de distribuição que irá minimizar a movimentação de dados</span><span class="sxs-lookup"><span data-stu-id="88c26-204">Select distribution column which will minimize data movement</span></span>
<span data-ttu-id="88c26-205">Minimizando a movimentação de dados, selecionando Olá distribuição certa coluna é uma das estratégias mais importantes de saudação para otimizar o desempenho do Data Warehouse do SQL.</span><span class="sxs-lookup"><span data-stu-id="88c26-205">Minimizing data movement by selecting hello right distribution column is one of hello most important strategies for optimizing performance of your SQL Data Warehouse.</span></span>  <span data-ttu-id="88c26-206">A movimentação de dados geralmente surge quando tabelas são unidas ou são executadas agregações.</span><span class="sxs-lookup"><span data-stu-id="88c26-206">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="88c26-207">Todas as colunas usadas nas cláusulas `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` e `HAVING` são candidatas à **boa** distribuição de hash.</span><span class="sxs-lookup"><span data-stu-id="88c26-207">Columns used in `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` and `HAVING` clauses all make for **good** hash distribution candidates.</span></span>

<span data-ttu-id="88c26-208">Olá por outro lado, as colunas em Olá `WHERE` cláusula execute **não** fazer candidatos a coluna hash bom porque eles limitam quais distribuições participarem consulta hello, fazendo com que o processamento de distorção.</span><span class="sxs-lookup"><span data-stu-id="88c26-208">On hello other hand, columns in hello `WHERE` clause do **not** make for good hash column candidates because they limit which distributions participate in hello query, causing processing skew.</span></span>  <span data-ttu-id="88c26-209">Um bom exemplo de uma coluna que pode ser tentador toodistribute, mas geralmente pode causar esse processamento distorção é uma coluna de data.</span><span class="sxs-lookup"><span data-stu-id="88c26-209">A good example of a column which might be tempting toodistribute on, but often can cause this processing skew is a date column.</span></span>

<span data-ttu-id="88c26-210">Em geral, se você tiver duas tabelas de fatos grande envolvidas frequentemente em uma junção, você obterá Olá maioria do desempenho através da distribuição de ambas as tabelas em uma das colunas de junção de saudação.</span><span class="sxs-lookup"><span data-stu-id="88c26-210">Generally speaking, if you have two large fact tables frequently involved in a join, you will gain hello most performance by distributing both tables on one of hello join columns.</span></span>  <span data-ttu-id="88c26-211">Se você tiver uma tabela que nunca é unida tooanother grande tabela de fatos, então, ser toocolumns que estejam frequentemente em Olá `GROUP BY` cláusula.</span><span class="sxs-lookup"><span data-stu-id="88c26-211">If you have a table that is never joined tooanother large fact table, then look toocolumns that are frequently in hello `GROUP BY` clause.</span></span>

<span data-ttu-id="88c26-212">Há alguns critérios principais que devem ser atendidos tooavoid a movimentação de dados durante uma junção:</span><span class="sxs-lookup"><span data-stu-id="88c26-212">There are a few key criteria which must be met tooavoid data movement during a join:</span></span>

1. <span data-ttu-id="88c26-213">Hello tabelas envolvidas na junção Olá devem ser distribuído em hash **um** de colunas Olá participam da junção hello.</span><span class="sxs-lookup"><span data-stu-id="88c26-213">hello tables involved in hello join must be hash distributed on **one** of hello columns participating in hello join.</span></span>
2. <span data-ttu-id="88c26-214">tipos de dados Olá Olá de colunas de junção devem corresponder entre as duas tabelas.</span><span class="sxs-lookup"><span data-stu-id="88c26-214">hello data types of hello join columns must match between both tables.</span></span>
3. <span data-ttu-id="88c26-215">colunas de saudação devem estar associadas com um operador equals.</span><span class="sxs-lookup"><span data-stu-id="88c26-215">hello columns must be joined with an equals operator.</span></span>
4. <span data-ttu-id="88c26-216">Olá tipo de associação não pode ser um `CROSS JOIN`.</span><span class="sxs-lookup"><span data-stu-id="88c26-216">hello join type may not be a `CROSS JOIN`.</span></span>

## <a name="troubleshooting-data-skew"></a><span data-ttu-id="88c26-217">Solucionando problemas de distorção de dados</span><span class="sxs-lookup"><span data-stu-id="88c26-217">Troubleshooting data skew</span></span>
<span data-ttu-id="88c26-218">Quando os dados da tabela são distribuídos usando o método de distribuição de hash hello há uma chance de que algumas distribuições será desviada toohave desproporcionalmente mais dados do que outras pessoas.</span><span class="sxs-lookup"><span data-stu-id="88c26-218">When table data is distributed using hello hash distribution method there is a chance that some distributions will be skewed toohave disproportionately more data than others.</span></span> <span data-ttu-id="88c26-219">Dados de distorção podem afetar o desempenho de consulta porque o resultado final de saudação de uma consulta distribuída deve esperar hello mais longa em execução toofinish de distribuição.</span><span class="sxs-lookup"><span data-stu-id="88c26-219">Excessive data skew can impact query performance because hello final result of a distributed query must wait for hello longest running distribution toofinish.</span></span> <span data-ttu-id="88c26-220">Dependendo do grau de saudação de dados de saudação distorção, que talvez seja necessário tooaddress-lo.</span><span class="sxs-lookup"><span data-stu-id="88c26-220">Depending on hello degree of hello data skew you might need tooaddress it.</span></span>

### <a name="identifying-skew"></a><span data-ttu-id="88c26-221">Identificando distorções</span><span class="sxs-lookup"><span data-stu-id="88c26-221">Identifying skew</span></span>
<span data-ttu-id="88c26-222">Tooidentify uma maneira simples uma tabela como inclinada é toouse `DBCC PDW_SHOWSPACEUSED`.</span><span class="sxs-lookup"><span data-stu-id="88c26-222">A simple way tooidentify a table as skewed is toouse `DBCC PDW_SHOWSPACEUSED`.</span></span>  <span data-ttu-id="88c26-223">Isso é uma maneira rápida e simples toosee Olá o número de linhas da tabela que são armazenados em cada uma das distribuições de saudação 60 do seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="88c26-223">This is a very quick and simple way toosee hello number of table rows that are stored in each of hello 60 distributions of your database.</span></span>  <span data-ttu-id="88c26-224">Lembre-se de que para desempenho hello mais balanceada, linhas de saudação em sua tabela distribuída devem ser divididas uniformemente em todas as distribuições de saudação.</span><span class="sxs-lookup"><span data-stu-id="88c26-224">Remember that for hello most balanced performance, hello rows in your distributed table should be spread evenly across all hello distributions.</span></span>

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="88c26-225">No entanto, se você consultar exibições de gerenciamento dinâmico Olá Azure SQL Data Warehouse (DMV), você pode executar uma análise mais detalhada.</span><span class="sxs-lookup"><span data-stu-id="88c26-225">However, if you query hello Azure SQL Data Warehouse dynamic management views (DMV) you can perform a more detailed analysis.</span></span>  <span data-ttu-id="88c26-226">toostart, criar exibição Olá [dbo.vTableSizes] [ dbo.vTableSizes] exibir usando Olá SQL de [visão geral da tabela] [ Overview] artigo.</span><span class="sxs-lookup"><span data-stu-id="88c26-226">toostart, create hello view [dbo.vTableSizes][dbo.vTableSizes] view using hello SQL from [Table Overview][Overview] article.</span></span>  <span data-ttu-id="88c26-227">Depois de saudação exibição é criada, execute este tooidentify consulta quais tabelas têm mais de distorção de dados de 10%.</span><span class="sxs-lookup"><span data-stu-id="88c26-227">Once hello view is created, run this query tooidentify which tables have more than 10% data skew.</span></span>

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

### <a name="resolving-data-skew"></a><span data-ttu-id="88c26-228">Resolvendo distorções de dados</span><span class="sxs-lookup"><span data-stu-id="88c26-228">Resolving data skew</span></span>
<span data-ttu-id="88c26-229">Não, todos os distorção é suficiente toowarrant uma correção.</span><span class="sxs-lookup"><span data-stu-id="88c26-229">Not all skew is enough toowarrant a fix.</span></span>  <span data-ttu-id="88c26-230">Em alguns casos, desempenho de saudação de uma tabela em algumas consultas pode exceder danos de saudação de distorção de dados.</span><span class="sxs-lookup"><span data-stu-id="88c26-230">In some cases, hello performance of a table in some queries can outweigh hello harm of data skew.</span></span>  <span data-ttu-id="88c26-231">toodecide se você deve resolver esses dados distorcer em uma tabela, você deve compreender tanto quanto possível sobre os volumes de dados hello e consultas na carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="88c26-231">toodecide if you should resolve data skew in a table, you should understand as much as possible about hello data volumes and queries in your workload.</span></span>   <span data-ttu-id="88c26-232">Toolook unidirecional no impacto de saudação de distorção é toouse etapas Olá Olá [consulta monitoramento] [ Query Monitoring] artigo toomonitor Olá impacto distorção no desempenho da consulta e especificamente Olá consultas demoradas de toohow de impacto assumir toocomplete distribuições de saudação individuais.</span><span class="sxs-lookup"><span data-stu-id="88c26-232">One way toolook at hello impact of skew is toouse hello steps in hello [Query Monitoring][Query Monitoring] article toomonitor hello impact of skew on query performance and specifically hello impact toohow long queries take toocomplete on hello individual distributions.</span></span>

<span data-ttu-id="88c26-233">Distribuição de dados é uma questão de encontrar o equilíbrio correto de saudação entre minimizar a distorção de dados e minimizar a movimentação de dados.</span><span class="sxs-lookup"><span data-stu-id="88c26-233">Distributing data is a matter of finding hello right balance between minimizing data skew and minimizing data movement.</span></span> <span data-ttu-id="88c26-234">Eles podem ser opostas metas e, às vezes, você desejará tookeep dados distorção na movimentação de dados de tooreduce de ordem.</span><span class="sxs-lookup"><span data-stu-id="88c26-234">These can be opposing goals, and sometimes you will want tookeep data skew in order tooreduce data movement.</span></span> <span data-ttu-id="88c26-235">Por exemplo, quando Olá distribuição coluna é frequentemente Olá compartilhado na junções e agregações, você será minimizando a movimentação de dados.</span><span class="sxs-lookup"><span data-stu-id="88c26-235">For example, when hello distribution column is frequently hello shared column in joins and aggregations, you will be minimizing data movement.</span></span> <span data-ttu-id="88c26-236">Olá benefício de ter a movimentação de dados mínimos Olá pode compensar impacto de saudação de distorção dados.</span><span class="sxs-lookup"><span data-stu-id="88c26-236">hello benefit of having hello minimal data movement might outweigh hello impact of having data skew.</span></span>

<span data-ttu-id="88c26-237">forma comum de saudação tooresolve distorção de dados é toore-criar tabela Olá com uma coluna de distribuição diferente.</span><span class="sxs-lookup"><span data-stu-id="88c26-237">hello typical way tooresolve data skew is toore-create hello table with a different distribution column.</span></span> <span data-ttu-id="88c26-238">Como não há nenhuma coluna de distribuição de saudação toochange em uma distribuição da tabela, Olá maneira toochange saudação de uma tabela de maneira-toorecreate-lo com um [] de [CTAS].</span><span class="sxs-lookup"><span data-stu-id="88c26-238">Since there is no way toochange hello distribution column on an existing table, hello way toochange hello distribution of a table it toorecreate it with a [CTAS][].</span></span>  <span data-ttu-id="88c26-239">Aqui estão dois exemplos de como resolver a distorção de dados:</span><span class="sxs-lookup"><span data-stu-id="88c26-239">Here are two examples of how resolve data skew:</span></span>

### <a name="example-1-re-create-hello-table-with-a-new-distribution-column"></a><span data-ttu-id="88c26-240">Exemplo 1: Criar novamente a tabela de saudação com uma nova coluna de distribuição</span><span class="sxs-lookup"><span data-stu-id="88c26-240">Example 1: Re-create hello table with a new distribution column</span></span>
<span data-ttu-id="88c26-241">Este exemplo usa [CTAS] [] toore-criar uma tabela com uma coluna de distribuição hash diferente.</span><span class="sxs-lookup"><span data-stu-id="88c26-241">This example uses [CTAS][] toore-create a table with a different hash distribution column.</span></span>

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

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_ProductKey];
RENAME OBJECT [dbo].[FactInternetSales_CustomerKey] too[FactInternetSales];
```

### <a name="example-2-re-create-hello-table-using-round-robin-distribution"></a><span data-ttu-id="88c26-242">Exemplo 2: Crie novamente a tabela hello usando a distribuição de rodízio</span><span class="sxs-lookup"><span data-stu-id="88c26-242">Example 2: Re-create hello table using round robin distribution</span></span>
<span data-ttu-id="88c26-243">Este exemplo usa [CTAS] [] toore-criar uma tabela com rodízio, em vez de uma distribuição de hash.</span><span class="sxs-lookup"><span data-stu-id="88c26-243">This example uses [CTAS][] toore-create a table with round robin instead of a hash distribution.</span></span> <span data-ttu-id="88c26-244">Essa alteração produzirá a distribuição de dados de mesmo custo de saudação de movimentação de dados maior.</span><span class="sxs-lookup"><span data-stu-id="88c26-244">This change will produce even data distribution at hello cost of increased data movement.</span></span>

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

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_HASH];
RENAME OBJECT [dbo].[FactInternetSales_ROUND_ROBIN] too[FactInternetSales];
```

## <a name="next-steps"></a><span data-ttu-id="88c26-245">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="88c26-245">Next steps</span></span>
<span data-ttu-id="88c26-246">toolearn mais sobre o design da tabela, consulte Olá [distribuir][Distribute], [índice][Index], [partição] [ Partition], [Tipos de dados][Data Types], [estatísticas] [ Statistics] e [tabelas temporárias] [ Temporary] artigos.</span><span class="sxs-lookup"><span data-stu-id="88c26-246">toolearn more about table design, see hello [Distribute][Distribute], [Index][Index], [Partition][Partition], [Data Types][Data Types], [Statistics][Statistics] and [Temporary Tables][Temporary] articles.</span></span>

<span data-ttu-id="88c26-247">Para obter uma visão geral das práticas recomendadas, confira [Práticas recomendadas para o SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="88c26-247">For an overview of best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
