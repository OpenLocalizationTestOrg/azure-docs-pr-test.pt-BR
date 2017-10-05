---
title: "Compatibilidade de banco de dados nível 130 - Banco de Dados SQL do Azure | Microsoft Docs"
description: "Neste artigo, exploramos os benefícios de executar o Banco de Dados SQL do Azure no nível de compatibilidade 130 e de aproveitar os benefícios dos novos recursos do processador de consultas e do otimizador de consulta. Também vamos abordar os possíveis efeitos colaterais sobre o desempenho para os aplicativos SQL existentes."
services: sql-database
documentationcenter: 
author: alainlissoir
manager: jhubbard
editor: 
ms.assetid: 8619f90b-7516-46dc-9885-98429add0053
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.devlang: NA
ms.tgt_pltfrm: NA
ms.topic: article
ms.date: 08/08/2016
ms.author: alainl
ms.openlocfilehash: c08c0690df4f389416e4ed2e2df2dbb72d6fd567
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a><span data-ttu-id="07757-104">Desempenho aprimorado de consultas com nível de compatibilidade 130 no Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="07757-104">Improved query performance with compatibility Level 130 in Azure SQL Database</span></span>
<span data-ttu-id="07757-105">O Banco de Dados SQL do Azure está executando de modo transparente centenas de milhares de bancos de dados em vários níveis de compatibilidade diferentes, preservando e garantindo a compatibilidade com versões anteriores à versão correspondente do Microsoft SQL Server para todos os seus clientes!</span><span class="sxs-lookup"><span data-stu-id="07757-105">Azure SQL Database is running transparently hundreds of thousands of databases at many different compatibility levels, preserving and guaranteeing the backward compatibility to the corresponding version of Microsoft SQL Server for all its customers!</span></span>

<span data-ttu-id="07757-106">Neste artigo, exploraremos os benefícios da execução de seu Banco de Dados SQL do Azure no nível de compatibilidade 130, e aproveitaremos os benefícios dos novos recursos de processador de consulta e otimizador de consultas.</span><span class="sxs-lookup"><span data-stu-id="07757-106">In this article, we explore the benefits of running your Azure SQL Databse at compatibility level 130, and leveraging the benefits of the new query optimizer and query processor features.</span></span> <span data-ttu-id="07757-107">Também vamos abordar os possíveis efeitos colaterais sobre o desempenho para os aplicativos SQL existentes.</span><span class="sxs-lookup"><span data-stu-id="07757-107">We also address the possible side-effects on the query performance for the existing SQL applications.</span></span>

<span data-ttu-id="07757-108">Como um lembrete do histórico, os alinhamentos das versões do SQL com os níveis de compatibilidade padrão são:</span><span class="sxs-lookup"><span data-stu-id="07757-108">As a reminder of history, the alignment of SQL versions to default compatibility levels are as follows:</span></span>

* <span data-ttu-id="07757-109">100: no SQL Server 2008 e no Banco de Dados SQL do Azure V11.</span><span class="sxs-lookup"><span data-stu-id="07757-109">100: in SQL Server 2008 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="07757-110">110: no SQL Server 2012 e no Banco de Dados SQL do Azure V11.</span><span class="sxs-lookup"><span data-stu-id="07757-110">110: in SQL Server 2012 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="07757-111">120: no SQL Server 2014 e no Banco de Dados SQL do Azure V12.</span><span class="sxs-lookup"><span data-stu-id="07757-111">120: in SQL Server 2014 and Azure SQL Database V12.</span></span>
* <span data-ttu-id="07757-112">130: no SQL Server 2016 e no Banco de Dados SQL do Azure V12.</span><span class="sxs-lookup"><span data-stu-id="07757-112">130: in SQL Server 2016 and Azure SQL Database V12.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07757-113">A partir de **meados de junho de 2016**, no Banco de Dados SQL do Azure, o nível de compatibilidade padrão será de 130 em vez de 120 para bancos de dados **recém-criados**.</span><span class="sxs-lookup"><span data-stu-id="07757-113">Starting in **mid-June 2016**, in Azure SQL Database, the default compatibility level will be 130 instead of 120 for **newly created** databases.</span></span>
> 
> <span data-ttu-id="07757-114">Bancos de dados criados antes de meados de junho de 2016 *não* serão afetados e manterão seu nível de compatibilidade atual (100, 110 ou 120).</span><span class="sxs-lookup"><span data-stu-id="07757-114">Databases created before mid-June 2016 will *not* be affected, and will maintain their current compatibility level (100, 110, or 120).</span></span> <span data-ttu-id="07757-115">Bancos de dados que migraram do Banco de Dados SQL do Azure versão V11 para V12 terão um nível de compatibilidade de 100 ou 110.</span><span class="sxs-lookup"><span data-stu-id="07757-115">Databases that migrated from Azure SQL Database version V11 to V12 will have a compatibility level of either 100 or 110.</span></span> 
> 

## <a name="about-compatibility-level-130"></a><span data-ttu-id="07757-116">Sobre o nível de compatibilidade 130</span><span class="sxs-lookup"><span data-stu-id="07757-116">About compatibility level 130</span></span>
<span data-ttu-id="07757-117">Primeiro, se você quiser saber o nível de compatibilidade atual do seu banco de dados, execute a instrução Transact-SQL a seguir.</span><span class="sxs-lookup"><span data-stu-id="07757-117">First, if you want to know the current compatibility level of your database, execute the following Transact-SQL statement.</span></span>

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


<span data-ttu-id="07757-118">Antes que essa alteração para o nível 130 ocorra para bancos de dados **recém** -criados, vamos examinar do que se trata essa alteração com alguns exemplos de consulta muito básicos e ver como qualquer pessoa pode se beneficiar com ela.</span><span class="sxs-lookup"><span data-stu-id="07757-118">Before this change to level 130 happens for **newly** created databases, let’s review what this change is all about through some very basic query examples, and see how anyone can benefit from it.</span></span>

<span data-ttu-id="07757-119">Processamento de consultas em bancos de dados relacionais pode ser muito complexo e pode exigir muita ciência da computação e matemática para entender as opções de design e os comportamentos inerentes.</span><span class="sxs-lookup"><span data-stu-id="07757-119">Query processing in relational databases can be very complex and can lead to lots of computer science and mathematics to understand the inherent design choices and behaviors.</span></span> <span data-ttu-id="07757-120">Neste documento, o conteúdo foi intencionalmente simplificado para garantir que qualquer pessoa com algum conhecimento técnico mínimo possa entender o impacto da alteração do nível de compatibilidade e determinar como ele pode beneficiar os aplicativos.</span><span class="sxs-lookup"><span data-stu-id="07757-120">In this document, the content has been intentionally simplified to ensure that anyone with some minimum technical background can understand the impact of the compatibility level change and determine how it can benefit applications.</span></span>

<span data-ttu-id="07757-121">Vamos dar uma olhada rápida em o que o nível de compatibilidade 130 traz para o cenário.</span><span class="sxs-lookup"><span data-stu-id="07757-121">Let’s have a quick look at what the compatibility level 130 brings at the table.</span></span>  <span data-ttu-id="07757-122">Você pode encontrar mais detalhes em [ALTERAR o nível de compatibilidade do BANCO DE DADOS (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), mas aqui está um breve resumo:</span><span class="sxs-lookup"><span data-stu-id="07757-122">You can find more details at [ALTER DATABASE Compatibility Level (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), but here is a short summary:</span></span>

* <span data-ttu-id="07757-123">A operação Insert de uma instrução Insert-select pode ser multi-threaded ou pode ter um plano paralelo, enquanto essa operação antes era de single-thread.</span><span class="sxs-lookup"><span data-stu-id="07757-123">The Insert operation of an Insert-select statement can be multi-threaded or can have a parallel plan, while before this operation was single-threaded.</span></span>
* <span data-ttu-id="07757-124">Tabela com Otimização de Memória e consultas de variáveis de tabela agora podem ter planos paralelos, enquanto antes essa operação também era de single-thread.</span><span class="sxs-lookup"><span data-stu-id="07757-124">Memory Optimized table and table variables queries can now have parallel plans, while before this operation was also single-threaded .</span></span>
* <span data-ttu-id="07757-125">As estatísticas de tabela com Otimização de Memória agora podem ser utilizadas e são atualizadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="07757-125">Statistics for Memory Optimized table can now be sampled and are auto-updated.</span></span> <span data-ttu-id="07757-126">Consulte [O que há de novo no mecanismo de banco de dados: OLTP na memória](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="07757-126">See [What's New in Database Engine: In-Memory OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) for more details.</span></span>
* <span data-ttu-id="07757-127">Modo de lote vs. Modo de Linha muda com índices de Repositório de Coluna</span><span class="sxs-lookup"><span data-stu-id="07757-127">Batch mode v/s Row Mode changes with Column Store indexes</span></span>
  * <span data-ttu-id="07757-128">As classificações em uma tabela com um índice de Repositório de Coluna agora estão em modo de lote.</span><span class="sxs-lookup"><span data-stu-id="07757-128">Sorts on a table with a Column Store index are now in batch mode.</span></span>
  * <span data-ttu-id="07757-129">As agregações em janela agora operam em modo de lote como instruções TSQL LAG/LEAD.</span><span class="sxs-lookup"><span data-stu-id="07757-129">Windowing aggregates now operate in batch mode such as TSQL LAG/LEAD statements.</span></span>
  * <span data-ttu-id="07757-130">Consultas em tabelas de Repositório de Coluna com Múltiplas cláusulas distintas operam em modo de Lote.</span><span class="sxs-lookup"><span data-stu-id="07757-130">Queries on Column Store tables with Multiple distinct clauses operate in Batch mode.</span></span>
  * <span data-ttu-id="07757-131">Consultas em execução com DOP = 1 ou um plano serial também são executadas em Modo de Lote.</span><span class="sxs-lookup"><span data-stu-id="07757-131">Queries running under DOP=1 or with a serial plan also execute in Batch Mode.</span></span>
* <span data-ttu-id="07757-132">Por fim, melhorias de Estimativa de Cardinalidade estão, na verdade, vindo com o nível de compatibilidade 120, mas para quem está executando em um nível de Compatibilidade inferior (ou seja, 100 ou 110), a mudança para o nível de compatibilidade 130 também trará esses aprimoramentos, e eles também podem beneficiar o desempenho da consulta de seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="07757-132">Last, Cardinality Estimation improvements are actually coming with compatibility level 120, but for those of you running at a lower Compatibility level (i.e. 100, or 110), the move to compatibility level 130 will also bring these improvements, and these can also benefit the query performance of your applications.</span></span>

## <a name="practicing-compatibility-level-130"></a><span data-ttu-id="07757-133">Praticando o nível de compatibilidade 130</span><span class="sxs-lookup"><span data-stu-id="07757-133">Practicing compatibility level 130</span></span>
<span data-ttu-id="07757-134">Primeiro, vejamos algumas tabelas, índices e dados aleatórios criados para praticar alguns desses novos recursos.</span><span class="sxs-lookup"><span data-stu-id="07757-134">First let’s get some tables, indexes and random data created to practice some of these new capabilities.</span></span> <span data-ttu-id="07757-135">Os exemplos de script TSQL podem ser executados no SQL Server 2016 ou no Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="07757-135">The TSQL script examples can be executed under SQL Server 2016, or under Azure SQL Database.</span></span> <span data-ttu-id="07757-136">No entanto, ao criar um Banco de Dados SQL do Azure, escolha pelo menos o banco de dados P2, pois precisará de pelo menos dois núcleos para permitir que multi-threads e, portanto, para aproveitar esses recursos.</span><span class="sxs-lookup"><span data-stu-id="07757-136">However, when creating an Azure SQL database, make sure you choose at the minimum a P2 database because you need at least a couple of cores to allow multi-threading and therefore benefit from these features.</span></span>

```
-- Create a Premium P2 Database in Azure SQL Database

CREATE DATABASE MyTestDB
    (EDITION=’Premium’, SERVICE_OBJECTIVE=’P2′);
GO

-- Create 2 tables with a column store index on
-- the second one (only available on Premium databases)

CREATE TABLE T_source
    (Color varchar(10), c1 bigint, c2 bigint);

CREATE TABLE T_target
    (c1 bigint, c2 bigint);

CREATE CLUSTERED COLUMNSTORE INDEX CCI ON T_target;
GO

-- Insert few rows.

INSERT T_source VALUES
    (‘Blue’, RAND() * 100000, RAND() * 100000),
    (‘Yellow’, RAND() * 100000, RAND() * 100000),
    (‘Red’, RAND() * 100000, RAND() * 100000),
    (‘Green’, RAND() * 100000, RAND() * 100000),
    (‘Black’, RAND() * 100000, RAND() * 100000);

GO 200

INSERT T_source SELECT * FROM T_source;

GO 10
```


<span data-ttu-id="07757-137">Agora, vamos dar uma olhada em alguns dos recursos de Processamento de Consulta que estão vindo com o nível de compatibilidade 130.</span><span class="sxs-lookup"><span data-stu-id="07757-137">Now, let’s have a look to some of the Query Processing features coming with compatibility level 130.</span></span>

## <a name="parallel-insert"></a><span data-ttu-id="07757-138">INSERT paralela</span><span class="sxs-lookup"><span data-stu-id="07757-138">Parallel INSERT</span></span>
<span data-ttu-id="07757-139">Executar as instruções TSQL abaixo executa a operação de INSERT no nível de compatibilidade 120 e 130, que executa, respectivamente, a operação INSERT em um modelo com single-thread (120) e em um modelo com multi-thread (130).</span><span class="sxs-lookup"><span data-stu-id="07757-139">Executing the TSQL statements below executes the INSERT operation under compatibility level 120 and 130, which respectively executes the INSERT operation in a single threaded model (120), and in a multi-threaded model (130).</span></span>

```
-- Parallel INSERT … SELECT … in heap or CCI
-- is available under 130 only

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO 

-- The INSERT part is in serial

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130
GO

-- The INSERT part is in parallel

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

SET STATISTICS XML OFF;
```


<span data-ttu-id="07757-140">Solicitando o plano de consulta real, examinando sua representação gráfica ou seu conteúdo XML, você pode determinar qual função está de Estimativa de Cardinalidade está em jogo.</span><span class="sxs-lookup"><span data-stu-id="07757-140">By requesting the actual the query plan, looking at its graphical representation or its XML content, you can determine which Cardinality Estimation function is at play.</span></span> <span data-ttu-id="07757-141">Observando a planos lado a lado na Figura 1, podemos ver claramente que a execução de INSERT do Repositório de Coluna vai de serial em 120 a paralela em 130.</span><span class="sxs-lookup"><span data-stu-id="07757-141">Looking at the plans side-by-side on figure 1, we can clearly see that the Column Store INSERT execution goes from serial in 120 to parallel in 130.</span></span> <span data-ttu-id="07757-142">Além disso, observe a alteração do ícone do iterador no plano 130 mostrando duas setas paralelas, ilustrando o fato de que agora a execução do iterador é, realmente, paralela.</span><span class="sxs-lookup"><span data-stu-id="07757-142">Also, note that the change of the iterator icon in the 130 plan showing two parallel arrows, illustrating the fact that now the iterator execution is indeed parallel.</span></span> <span data-ttu-id="07757-143">Se você tiver grandes operações de INSERT para concluir, a execução paralela, vinculada ao número de núcleos que você tem à sua disposição para o banco de dados, terá um melhor desempenho; dependendo da sua situação, até 100 vezes mais rápido!</span><span class="sxs-lookup"><span data-stu-id="07757-143">If you have large INSERT operations to complete, the parallel execution, linked to the number of core you have at your disposal for the database, will perform better; up to a 100 times faster depending your situation!</span></span>

<span data-ttu-id="07757-144">*Figura 1: a operação de INSERT muda de serial para paralela com compatibilidade de nível 130.*</span><span class="sxs-lookup"><span data-stu-id="07757-144">*Figure 1: INSERT operation changes from serial to parallel with compatibility level 130.*</span></span>

![A figura 1](./media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a><span data-ttu-id="07757-146">Modo de lote SERIAL</span><span class="sxs-lookup"><span data-stu-id="07757-146">SERIAL Batch Mode</span></span>
<span data-ttu-id="07757-147">Da mesma forma, passar para o nível de compatibilidade 130 ao processar linhas de dados habilita o processamento no modo de lote.</span><span class="sxs-lookup"><span data-stu-id="07757-147">Similarly, moving to compatibility level 130 when processing rows of data enables batch mode processing.</span></span> <span data-ttu-id="07757-148">Primeiro, operações no modo de lote só estão disponíveis quando você tem um índice de repositório de coluna em vigor.</span><span class="sxs-lookup"><span data-stu-id="07757-148">First, batch mode operations  are only available when you have a column store index in place.</span></span> <span data-ttu-id="07757-149">Em segundo lugar, um lote normalmente representa ~900 linhas e usa uma lógica de código otimizada para vários núcleos de CPU, maior taxa de transferência de memória e aproveita diretamente os dados compactados do Repositório de Coluna, sempre que possível.</span><span class="sxs-lookup"><span data-stu-id="07757-149">Second, a batch typically represents ~900 rows, and uses a code logic optimized for multicore CPU, higher memory throughput and directly leverages the compressed data of the Column Store whenever possible.</span></span> <span data-ttu-id="07757-150">Nessas condições, o SQL Server 2016 pode processar ~900 linhas ao mesmo tempo, em vez de uma linha por vez, assim, o custo geral de sobrecarga da operação agora é compartilhado por todo o lote, reduzindo o custo geral por linha.</span><span class="sxs-lookup"><span data-stu-id="07757-150">Under these conditions, SQL Server 2016 can process ~900 rows at once, instead of 1 row at the time, and as a consequence, the overall overhead cost of the operation is now shared by the entire batch, reducing the overall cost by row.</span></span> <span data-ttu-id="07757-151">Essa quantidade compartilhada de operações combinada com a compactação do repositório de coluna basicamente reduz a latência envolvida em uma operação de modo de lote SELECT.</span><span class="sxs-lookup"><span data-stu-id="07757-151">This shared amount of operations combined with the column store compression basically reduces the latency involved in a SELECT batch mode operation.</span></span> <span data-ttu-id="07757-152">Você pode encontrar mais detalhes sobre o repositório de coluna e o modo de lote no [Guia de índices Columnstore](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="07757-152">You can find more details about the column store and batch mode at [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

```
-- Serial batch mode execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- The scan and aggregate are in row mode

SELECT C1, COUNT (C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO 

-- The scan and aggregate are in batch mode,
-- and force MAXDOP to 1 to show that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="07757-153">Como visível abaixo, observando os planos de consulta lado a lado na figura 2, podemos ver que o modo de processamento mudou com o nível de compatibilidade e, assim, ao executar as consultas em ambos os nível de compatibilidade de uma única vez, podemos ver que a maior parte do tempo de processamento é gasto no modo de linha (86%) em comparação ao modo em lote (% 14), em que os 2 lotes foram processados.</span><span class="sxs-lookup"><span data-stu-id="07757-153">As visible below, by observing the query plans side-by-side on figure 2, we can see that the processing mode has changed with the compatibility level, and as a consequence, when executing the queries in both compatibility level altogether, we can see that most of the processing time is spent in row mode (86%) compared to the batch mode (14%), where 2 batches have been processed.</span></span> <span data-ttu-id="07757-154">Aumentar o conjunto de dados aumentará o benefício.</span><span class="sxs-lookup"><span data-stu-id="07757-154">Increase the dataset, the benefit will increase.</span></span>

<span data-ttu-id="07757-155">*Figura 2: a operação SELECT muda do modo serial para o modo de lote com o nível de compatibilidade 130.*</span><span class="sxs-lookup"><span data-stu-id="07757-155">*Figure 2: SELECT operation changes from serial to batch mode with compatibility level 130.*</span></span>

![Figura 2](./media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a><span data-ttu-id="07757-157">Modo em lotes em Execução de Classificação</span><span class="sxs-lookup"><span data-stu-id="07757-157">Batch mode on Sort Execution</span></span>
<span data-ttu-id="07757-158">Semelhante ao acima, mas aplicado a uma operação de classificação, a transição do modo de linha (nível de compatibilidade 120) para o modo de lote (nível de compatibilidade 130) melhora o desempenho da operação SORT pelas mesmas razões.</span><span class="sxs-lookup"><span data-stu-id="07757-158">Similar to the above, but applied to a sort operation, the transition from row mode (compatibility level 120) to batch mode (compatibility level 130) improves the performance of the SORT operation for the same reasons.</span></span>

```
-- Batch mode on sort execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- The scan and aggregate are in row mode

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

-- The scan and aggregate are in batch mode,
-- and force MAXDOP to 1 to show that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="07757-159">Visível lado a lado na figura 3, podemos ver que a operação de classificação no modo linha representa 81% do custo, enquanto o modo em lote representa apenas 19% do custo (respectivamente, 81% e 56% na classificação em si).</span><span class="sxs-lookup"><span data-stu-id="07757-159">Visible side-by-side on figure 3, we can see that the sort operation in row mode represents 81% of the cost, while the batch mode only represents 19% of the cost (respectively 81% and 56% on the sort itself).</span></span>

<span data-ttu-id="07757-160">*Figura 3: a operação SORT muda do modo de linha para o em lotes com o nível de compatibilidade 130.*</span><span class="sxs-lookup"><span data-stu-id="07757-160">*Figure 3: SORT operation changes from row to batch mode with compatibility level 130.*</span></span>

![A figura 3](./media/sql-database-compatibility-level-query-performance-130/figure-3.png)

<span data-ttu-id="07757-162">Obviamente, esses exemplos contêm apenas dezenas de milhares de linhas, o que não é nada ao examinar os dados disponíveis na maioria dos SQL Servers hoje em dia.</span><span class="sxs-lookup"><span data-stu-id="07757-162">Obviously, these samples only contain tens of thousands of rows, which is nothing when looking at the data available in most SQL Servers these days.</span></span> <span data-ttu-id="07757-163">Apenas projete isso com relação a milhões de linhas, e isso poderá se converter em vários minutos de execução poupados diariamente dependendo da natureza da sua carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="07757-163">Just project these against millions of rows instead, and this can translate in several minutes of execution spared every day pending the nature of your workload.</span></span>

## <a name="cardinality-estimation-ce-improvements"></a><span data-ttu-id="07757-164">Aprimoramentos de CE (Estimativa de Cardinalidade)</span><span class="sxs-lookup"><span data-stu-id="07757-164">Cardinality Estimation (CE) improvements</span></span>
<span data-ttu-id="07757-165">Introduzida com o SQL Server 2014, qualquer banco de dados em execução em um nível de compatibilidade 120 ou acima usará a nova funcionalidade de Estimativa de Cardinalidade.</span><span class="sxs-lookup"><span data-stu-id="07757-165">Introduced with SQL Server 2014, any database running at a compatibility level 120 or above will make use of the new Cardinality Estimation functionality.</span></span> <span data-ttu-id="07757-166">Essencialmente, a estimativa de cardinalidade é a lógica usada para determinar como o SQL Server executará uma consulta com base em seu custo estimado.</span><span class="sxs-lookup"><span data-stu-id="07757-166">Essentially, cardinality estimation is the logic used to determine how SQL server will execute a query based on its estimated cost.</span></span> <span data-ttu-id="07757-167">A estimativa é calculada usando dados de estatísticas associadas aos objetos envolvidos na consulta.</span><span class="sxs-lookup"><span data-stu-id="07757-167">The estimation is calculated using input from statistics associated with objects involved in that query.</span></span> <span data-ttu-id="07757-168">Na prática, em um alto nível, funções de Estimativa de Cardinalidade são estimativas de contagem de linha juntamente com informações sobre a distribuição de valores, contagens de valores distintos e contagens duplicadas contidas nas tabelas e nos objetos referenciados na consulta.</span><span class="sxs-lookup"><span data-stu-id="07757-168">Practically, at a high-level, Cardinality Estimation functions are row count estimates along with information about the distribution of the values, distinct value counts, and duplicate counts contained in the tables and objects referenced in the query.</span></span> <span data-ttu-id="07757-169">Errar essas estimativas pode levar a E/S de disco desnecessárias devido a concessões de memória insuficientes (ou seja, derramamentos de TempDB) ou a uma seleção de uma execução de plano serial sobre a execução de um plano paralelo, para citar alguns exemplos.</span><span class="sxs-lookup"><span data-stu-id="07757-169">Getting these estimates wrong, can lead to unnecessary disk I/O due to insufficient memory grants (i.e. TempDB spills), or to a selection of a serial plan execution over a parallel plan execution, to name a few.</span></span> <span data-ttu-id="07757-170">Em conclusão, estimativas incorretas podem levar a uma degradação do desempenho geral da execução da consulta.</span><span class="sxs-lookup"><span data-stu-id="07757-170">Conclusion, incorrect estimates can lead to an overall performance degradation of the query execution.</span></span> <span data-ttu-id="07757-171">Por outro lado, melhores estimativas, estimativas mais precisas, levam a execuções de consulta melhores!</span><span class="sxs-lookup"><span data-stu-id="07757-171">On the other side, better estimates, more accurate estimates, leads to better query executions!</span></span>

<span data-ttu-id="07757-172">Como mencionado anteriormente, estimativas e otimizações de consulta são uma questão complexa, mas, se você quiser saber mais sobre planos de consulta e o avaliador de cardinalidade, consulte o documento em [Otimizar seus planos de consulta com o avaliador de cardinalidade do SQL Server 2014](https://msdn.microsoft.com/library/dn673537.aspx) para se aprofundar.</span><span class="sxs-lookup"><span data-stu-id="07757-172">As mentioned before, query optimizations and estimates are a complex matter, but if you want to learn more about query plans and cardinality estimator, you can refer to the document at [Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator](https://msdn.microsoft.com/library/dn673537.aspx) for a deeper dive.</span></span>

## <a name="which-cardinality-estimation-do-you-currently-use"></a><span data-ttu-id="07757-173">Que Estimativa de Cardinalidade você usa atualmente?</span><span class="sxs-lookup"><span data-stu-id="07757-173">Which Cardinality Estimation do you currently use?</span></span>
<span data-ttu-id="07757-174">Para determinar em qual Estimativa de Cardinalidade suas consultas estão sendo executadas, vamos simplesmente usar os exemplos de consulta abaixo.</span><span class="sxs-lookup"><span data-stu-id="07757-174">To determine under which Cardinality Estimation your queries are running, let’s just use the query samples below.</span></span> <span data-ttu-id="07757-175">Observe que este primeiro exemplo será executado no nível de compatibilidade 110, indicando o uso das funções de estimativa de cardinalidade antigas.</span><span class="sxs-lookup"><span data-stu-id="07757-175">Note that this first example will run under compatibility level 110, implying the use of the old Cardinality Estimation functions.</span></span>

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 110;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="07757-176">Quando a execução estiver concluída, clique no link de XML e examine as propriedades do primeiro iterador conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="07757-176">Once execution is complete, click on the XML link, and look at the properties of the first iterator as shown below.</span></span> <span data-ttu-id="07757-177">Observe o nome da propriedade chamada CardinalityEstimationModelVersion definido no momento em 70.</span><span class="sxs-lookup"><span data-stu-id="07757-177">Note the property name called CardinalityEstimationModelVersion currently set on 70.</span></span> <span data-ttu-id="07757-178">Isso significa que o nível de compatibilidade do banco de dados está definido para a versão do SQL Server 7.0 (definido em 110 como visíveis nas instruções TSQL acima), mas o valor 70 simplesmente representa a funcionalidade de estimativa de cardinalidade herdada disponível desde o SQL Server 7.0, que não teve revisões importantes até o SQL Server 2014 (que vem com um nível de compatibilidade de 120).</span><span class="sxs-lookup"><span data-stu-id="07757-178">It does not mean that the database compatibility level is set to the SQL Server 7.0 version (it is set on 110 as visible in the TSQL statements above), but the value 70 simply represents the legacy Cardinality Estimation functionality available since SQL Server 7.0, which had no major revisions until SQL Server 2014 (which comes with a compatibility level of 120).</span></span>

<span data-ttu-id="07757-179">*Figura 4: a CardinalityEstimationModelVersion é definida para 70 ao usar um nível de compatibilidade 110 ou abaixo.*</span><span class="sxs-lookup"><span data-stu-id="07757-179">*Figure 4: The CardinalityEstimationModelVersion is set to 70 when using a compatibility level of 110 or below.*</span></span>

![Figura 4](./media/sql-database-compatibility-level-query-performance-130/figure-4.png)

<span data-ttu-id="07757-181">Como alternativa, você pode alterar o nível de compatibilidade para 130 e desabilitar o uso da nova função de Estimativa de Cardinalidade usando o LEGACY_CARDINALITY_ESTIMATION definido como ON com [ALTERAR CONFIGURAÇÃO DE ESCOPO DO BANCO DE DADOS](https://msdn.microsoft.com/library/mt629158.aspx).</span><span class="sxs-lookup"><span data-stu-id="07757-181">Alternatively, you can change the compatibility level to 130, and disable the use of the new Cardinality Estimation function by using the LEGACY_CARDINALITY_ESTIMATION set to ON with [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span></span> <span data-ttu-id="07757-182">Isso será exatamente o mesmo que usar 110 de um ponto de vista de função de Estimativa de Cardinalidade enquanto se usa o nível de compatibilidade de processamento de consulta mais recente.</span><span class="sxs-lookup"><span data-stu-id="07757-182">This will be exactly the same as using 110 from a Cardinality Estimation function point of view, while using the latest query processing compatibility level.</span></span> <span data-ttu-id="07757-183">Ao fazer isso, você pode se beneficiar dos novos recursos de processamento de consulta disponíveis com o nível de compatibilidade mais recente (ou seja, o modo de lote), mas ainda contar com a funcionalidade de Estimativa de Cardinalidade antiga, se necessário.</span><span class="sxs-lookup"><span data-stu-id="07757-183">Doing so, you can benefit from the new query processing features coming with the latest compatibility level (i.e. batch mode), but still rely on the old Cardinality Estimation functionality if necessary.</span></span>

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="07757-184">Simplesmente passar para o nível de compatibilidade 120 ou 130 habilita a nova funcionalidade de Estimativa de Cardinalidade.</span><span class="sxs-lookup"><span data-stu-id="07757-184">Simply moving to the compatibility level 120 or 130 enables the new Cardinality Estimation functionality.</span></span> <span data-ttu-id="07757-185">Nesse caso, o padrão CardinalityEstimationModelVersion será definido de acordo para 120 ou 130, como visível a seguir.</span><span class="sxs-lookup"><span data-stu-id="07757-185">In such a case, the default CardinalityEstimationModelVersion will be set accordingly to 120 or 130 as visible below.</span></span>

```
-- New CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="07757-186">*Figura 5: o CardinalityEstimationModelVersion é definido para 130 ao usar um nível de compatibilidade de 130.*</span><span class="sxs-lookup"><span data-stu-id="07757-186">*Figure 5: The CardinalityEstimationModelVersion is set to 130 when using a compatibility level of 130.*</span></span>

![Figura 5](./media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-the-cardinality-estimation-differences"></a><span data-ttu-id="07757-188">Testemunhando as diferenças de Estimativa de Cardinalidade</span><span class="sxs-lookup"><span data-stu-id="07757-188">Witnessing the Cardinality Estimation differences</span></span>
<span data-ttu-id="07757-189">Agora vamos executar uma consulta um pouco mais complexa que envolve uma INNER JOIN com uma cláusula WHERE com alguns predicados e vamos examinar a estimativa de contagem de linha da função de Estimativa de Cardinalidade antiga primeiro.</span><span class="sxs-lookup"><span data-stu-id="07757-189">Now, let’s run a slightly more complex query involving an INNER JOIN with a WHERE clause with some predicates, and let’s look at the row count estimate from the old Cardinality Estimation function first.</span></span>

```
-- Old CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="07757-190">A execução desta consulta efetivamente retorna 200.704 linhas, enquanto a estimativa de linha com a funcionalidade de Estimativa de Cardinalidade antiga reivindica 194.284 linhas.</span><span class="sxs-lookup"><span data-stu-id="07757-190">Executing this query effectively returns 200,704 rows, while the row estimate with the old Cardinality Estimation functionality claims 194,284 rows.</span></span> <span data-ttu-id="07757-191">Obviamente, como dito antes, esses resultados de contagem de linha também dependerão da frequência com que você executou os exemplos anteriores, que preenchem as tabelas de exemplo repetidamente a cada execução.</span><span class="sxs-lookup"><span data-stu-id="07757-191">Obviously, as said before, these row count results will also depend how often you ran the previous samples, which populates the sample tables over and over again at each run.</span></span> <span data-ttu-id="07757-192">Obviamente, os predicados na consulta também terão uma influência sobre a estimativa real além da forma de tabela, do conteúdo de dados e de como esses dados realmente se correlacionam entre si.</span><span class="sxs-lookup"><span data-stu-id="07757-192">Obviously, the predicates in your query will also have an influence on the actual estimation aside from the table shape, data content, and how this data actually correlate with each other.</span></span>

<span data-ttu-id="07757-193">*Figura 6: a estimativa de contagem de linhas é de 194.284 ou 6.000 linhas aquém das 200.704 linhas esperadas.*</span><span class="sxs-lookup"><span data-stu-id="07757-193">*Figure 6: The row count estimate is 194,284 or 6,000 rows off from the 200,704 rows expected.*</span></span>

![Figura 6](./media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

<span data-ttu-id="07757-195">Da mesma forma, agora vamos executar a mesma consulta com a nova funcionalidade de Estimativa de Cardinalidade.</span><span class="sxs-lookup"><span data-stu-id="07757-195">In the same way, let’s now execute the same query with the new Cardinality Estimation functionality.</span></span>

```
-- New CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="07757-196">Observando o abaixo, agora vemos que a estimativa de linha é de 202.877, ou muito perto e maior do que a Estimativa de Cardinalidade antiga.</span><span class="sxs-lookup"><span data-stu-id="07757-196">Looking at the below, we now see that the row estimate is 202,877, or much closer and higher than the old Cardinality Estimation.</span></span>

<span data-ttu-id="07757-197">*Figura 7: a estimativa de contagem de linha agora é de 202.877, em vez de 194.284.*</span><span class="sxs-lookup"><span data-stu-id="07757-197">*Figure 7: The row count estimate is now 202,877, instead of 194,284.*</span></span>

![Figura 7](./media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

<span data-ttu-id="07757-199">Na realidade, o conjunto de resultados é de 200.704 linhas (mas tudo depende de quantas vezes você executou as consultas dos exemplos anteriores; mas, mais importante, porque o TSQL usa a instrução RAND(), os valores reais retornados podem variar de uma execução para a próxima).</span><span class="sxs-lookup"><span data-stu-id="07757-199">In reality, the result set is 200,704 rows (but all of it depends how often you did run the queries of the previous samples, but more importantly, because the TSQL uses the RAND() statement, the actual values returned can vary from one run to the next).</span></span> <span data-ttu-id="07757-200">Portanto, neste exemplo específico, a nova Estimativa de Cardinalidade faz um trabalho melhor de estimar o número de linhas, pois 202.877 está muito mais próximo de 200.704, que 194.284!</span><span class="sxs-lookup"><span data-stu-id="07757-200">Therefore, in this particular example, the new Cardinality Estimation does a better job at estimating the number of rows because 202,877 is much closer to 200,704, than 194,284!</span></span> <span data-ttu-id="07757-201">Por fim, se você alterar os predicados da cláusula WHERE para igualdade (em vez de ">", por exemplo), isso poderá tornar as estimativas entre as funções de Cardinalidade antiga e nova ainda mais diferentes, dependendo de quantas correspondências você pode obter.</span><span class="sxs-lookup"><span data-stu-id="07757-201">Last, if you change the WHERE clause predicates to equality (rather than “>” for instance), this could make the estimates between the old and new Cardinality function even more different, depending on how many matches you can get.</span></span>

<span data-ttu-id="07757-202">Obviamente, nesse caso, estar ~6000 aquém da contagem real não representa muitos dados em algumas situações.</span><span class="sxs-lookup"><span data-stu-id="07757-202">Obviously, in this case, being ~6000 rows off from actual count does not represent a lot of data in some situations.</span></span> <span data-ttu-id="07757-203">Agora, transponha isso para milhões de linhas em várias tabelas e consultas mais complexas e, às vezes, a estimativa poderá ter uma diferença de milhões de linhas, portanto, correndo o risco de selecionar o plano de execução incorreto ou solicitar concessões de memória insuficientes, levando a derramamentos de TempDB e, portanto, as E/S são muito maiores.</span><span class="sxs-lookup"><span data-stu-id="07757-203">Now, transpose this to millions of rows across several tables and more complex queries, and at times the estimate can be off by millions of rows , and therefore, the risk of picking-up the wrong execution plan, or requesting insufficient memory grants leading to TempDB spills, and so more I/O, are much higher.</span></span>

<span data-ttu-id="07757-204">Se você tiver a oportunidade, pratique essa comparação com suas consultas e conjuntos de dados mais comuns e veja você mesmo em quanto algumas das estimativas novas e antigas são afetadas, enquanto algumas podem estar mais distantes da realidade, ou outras simplesmente mais perto das contagens de linhas reais de fato retornadas nos conjuntos de resultados.</span><span class="sxs-lookup"><span data-stu-id="07757-204">If you have the opportunity, practice this comparison with your most typical queries and datasets, and see for yourself by how much some of the old and new estimates are affected, while some could just become more off from the reality, or some others just simply closer to the actual row counts actually returned in the result sets.</span></span> <span data-ttu-id="07757-205">Tudo isso depende da forma de suas consultas, das características do Banco de Dados SQL do Azure, da natureza e do tamanho de seus conjuntos de dados e das estatísticas disponíveis sobre eles.</span><span class="sxs-lookup"><span data-stu-id="07757-205">All of it will depend of the shape of your queries, the Azure SQL database characteristics, the nature and the size of your datasets, and the statistics available about them.</span></span> <span data-ttu-id="07757-206">Se você tiver acabado de criar sua instância do Banco de Dados SQL do Azure, o otimizador de consulta precisará criar seu conhecimento do zero, em vez de reutilizar estatísticas criadas com base em execuções de consulta anterior.</span><span class="sxs-lookup"><span data-stu-id="07757-206">If you just created your Azure SQL Database instance, the query optimizer will have to build its knowledge from scratch instead of reusing statistics made of the previous query runs.</span></span> <span data-ttu-id="07757-207">Portanto, as estimativas são muito contextuais e quase específicas a cada situação de servidor e aplicativo.</span><span class="sxs-lookup"><span data-stu-id="07757-207">So, the estimates are very contextual and almost specific to every server and application situation.</span></span> <span data-ttu-id="07757-208">Ele é um aspecto importante para ter em mente!</span><span class="sxs-lookup"><span data-stu-id="07757-208">It is an important aspect to keep in mind!</span></span>

## <a name="some-considerations-to-take-into-account"></a><span data-ttu-id="07757-209">Algumas considerações para levar em conta</span><span class="sxs-lookup"><span data-stu-id="07757-209">Some considerations to take into account</span></span>
<span data-ttu-id="07757-210">Embora a maioria das cargas de trabalho possa se beneficiar do nível de compatibilidade 130, antes de adotar o nível de compatibilidade para o seu ambiente de produção, você tem basicamente 3 opções:</span><span class="sxs-lookup"><span data-stu-id="07757-210">Although most workloads would benefit from the compatibility level 130, before you adopting the compatibility level for your production environment, you basically have 3 options:</span></span>

1. <span data-ttu-id="07757-211">Você passa para o nível de compatibilidade 130 e examina como fica o desempenho.</span><span class="sxs-lookup"><span data-stu-id="07757-211">You move to compatibility level 130, and see how things perform.</span></span> <span data-ttu-id="07757-212">Caso você perceba algum regressão, simplesmente define o nível de compatibilidade de volta ao nível original ou mantém 130 e apenas reverte a Estimativa de Cardinalidade de volta para o modo herdado (conforme explicado anteriormente, isso sozinho pode resolver o problema).</span><span class="sxs-lookup"><span data-stu-id="07757-212">In case you notice some regressions, you just simply set the compatibility level back to its original level, or keep 130, and only reverse the Cardinality Estimation back to the legacy mode (As explained above, this alone could address the issue).</span></span>
2. <span data-ttu-id="07757-213">Você testa seus aplicativos existentes sob uma carga de produção semelhante, ajusta e valida o desempenho antes de entrar em produção.</span><span class="sxs-lookup"><span data-stu-id="07757-213">You thoroughly test your existing applications under similar production load, fine tune, and validate the performance before going to production.</span></span> <span data-ttu-id="07757-214">No caso de problemas, da mesma foram que acima, você pode voltar para o nível de compatibilidade original ou simplesmente reverter a Estimativa de Cardinalidade de volta para o modo herdado.</span><span class="sxs-lookup"><span data-stu-id="07757-214">In case of issues, same as above, you can always go back to the original compatibility level, or simply reverse the Cardinality Estimation back to the legacy mode.</span></span>
3. <span data-ttu-id="07757-215">Como uma opção final e a maneira mais recente de tratar essas questões, aproveite o Repositório de Consultas.</span><span class="sxs-lookup"><span data-stu-id="07757-215">As a final option, and the most recent way to address these questions, is to leverage the Query Store.</span></span> <span data-ttu-id="07757-216">Essa é a opção recomendada de hoje!</span><span class="sxs-lookup"><span data-stu-id="07757-216">That’s today’s recommended option!</span></span> <span data-ttu-id="07757-217">Para ajudar na análise de suas consultas em compatibilidade de nível 120 ou abaixo versus 130, nunca é suficiente incentivar o uso do Repositório de Consultas.</span><span class="sxs-lookup"><span data-stu-id="07757-217">To assist the analysis of your queries under compatibility level 120 or below versus 130, we cannot encourage you enough to use Query Store.</span></span> <span data-ttu-id="07757-218">O Repositório de Consultas está disponível com a versão mais recente do Banco de Dados SQL do Azure V12 e foi projetada para ajudá-lo a solucionar problemas de desempenho de consulta.</span><span class="sxs-lookup"><span data-stu-id="07757-218">Query Store is available with the latest version of Azure SQL Database V12, and it’s designed to help you with query performance troubleshooting.</span></span> <span data-ttu-id="07757-219">Considere o Repositório de Consultas um gravador de dados de voo para seu banco de dados, coletando e apresentando informações históricas detalhadas sobre todas as consultas.</span><span class="sxs-lookup"><span data-stu-id="07757-219">Think of the Query Store as a flight data recorder for your database collecting and presenting detailed historic information about all queries.</span></span> <span data-ttu-id="07757-220">Isso simplifica bastante a forense de desempenho, reduzindo o tempo para diagnosticar e resolver problemas.</span><span class="sxs-lookup"><span data-stu-id="07757-220">This greatly simplifies performance forensics by reducing the time to diagnose and resolve issues.</span></span> <span data-ttu-id="07757-221">Você pode encontrar mais informações no artigo sobre [Repositório de Consultas: o gravador de dados de voo para o banco de dados](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span><span class="sxs-lookup"><span data-stu-id="07757-221">You can find more information at [Query Store: A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span></span>

<span data-ttu-id="07757-222">No geral, se você já tiver um conjunto de bancos de dados em execução no nível de compatibilidade 120 ou abaixo e planejar mover alguns deles para 130, ou porque sua carga de trabalho provisionará novos bancos de dados que logo serão automaticamente definidos por padrão como 130, considere o seguinte:</span><span class="sxs-lookup"><span data-stu-id="07757-222">At the high-level, if you already have a set of databases running at compatibility level 120 or below, and plan to move some of them to 130, or because your workload automatically provision new databases that will be soon be set by default to 130, please consider the followings:</span></span>

* <span data-ttu-id="07757-223">Antes de alterar para o novo nível de compatibilidade em produção, habilite o Repositório de Consultas.</span><span class="sxs-lookup"><span data-stu-id="07757-223">Before changing to the new compatibility level in production, enable Query Store.</span></span> <span data-ttu-id="07757-224">Você pode consultar o artigo sobre como [alterar o modo de compatibilidade do banco de dados e usar o armazenamento de consulta](https://msdn.microsoft.com/library/bb895281.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="07757-224">You can refer to [Change the Database Compatibility Mode and Use the Query Store](https://msdn.microsoft.com/library/bb895281.aspx) for more information.</span></span>
* <span data-ttu-id="07757-225">Em seguida, teste todas as cargas de trabalho críticas usando dados representativos e consultas de um ambiente de produção e compare o desempenho observado e o relatado pelo Repositório de Consulta.</span><span class="sxs-lookup"><span data-stu-id="07757-225">Next, test all critical workloads using representative data and queries of a production-like environment, and compare the performance experienced and as reported by Query Store.</span></span> <span data-ttu-id="07757-226">Se você sofrer algumas regressões, poderá identificar as consultas retornadas com o Repositório de Consulta e usar a opção de imposição de plano do Repositório de Consultas (também conhecido como fixação de plano).</span><span class="sxs-lookup"><span data-stu-id="07757-226">If you experience some regressions, you can identify the regressed queries with the Query Store and use the plan forcing option from Query Store (aka plan pinning).</span></span> <span data-ttu-id="07757-227">Nesse caso, você definitivamente fica com o nível de compatibilidade 130 e usa o plano de consulta anterior conforme sugerido pelo Repositório de Consultas.</span><span class="sxs-lookup"><span data-stu-id="07757-227">In such a case, you definitively stay with the compatibility level 130, and use the former query plan as suggested by the Query Store.</span></span>
* <span data-ttu-id="07757-228">Se você desejar aproveitar os novos recursos e funcionalidades do Banco de Dados SQL do Azure (que está executando o SQL Server 2016), mas for sensível às mudanças trazidas pelo nível de compatibilidade 130, como último recurso, você poderá considerar forçar o nível de compatibilidade de volta para o nível adequado de sua carga de trabalho usando uma instrução ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="07757-228">If you want to leverage new features and capabilities of Azure SQL Database (which is running SQL Server 2016), but are sensitive to changes brought by the compatibility level 130, as a last resort, you could consider forcing the compatibility level back to the level that suits your workload by using an ALTER DATABASE statement.</span></span> <span data-ttu-id="07757-229">Mas primeiro, lembre-se de que a opção de fixação de plano do Repositório de Consultas é sua melhor opção, porque não usar 130 basicamente é permanecer no nível de funcionalidade de uma versão mais antiga do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="07757-229">But first, be aware that the Query Store plan pinning option is your best option because not using 130 is basically staying at the functionality level of an older SQL Server version.</span></span>
* <span data-ttu-id="07757-230">Se você tiver aplicativos multilocatários abrangendo vários bancos de dados, poderá ser necessário atualizar a lógica de provisionamento dos bancos de dados para garantir um nível de compatibilidade consistente em todos os bancos de dados; tantos nos antigos quanto nos recentemente configurados.</span><span class="sxs-lookup"><span data-stu-id="07757-230">If you have multitenant applications spanning multiple databases, it may be necessary to update the provisioning logic of your databases to ensure a consistent compatibility level across all databases; old and newly provisioned ones.</span></span> <span data-ttu-id="07757-231">O desempenho de carga de trabalho do aplicativo pode ser sensível ao fato de que alguns bancos de dados estão em execução em diferentes níveis de compatibilidade, portanto, pode ser necessária consistência de nível de compatibilidade entre quaisquer bancos de dados de para oferecer a mesma experiência aos clientes de um modo geral.</span><span class="sxs-lookup"><span data-stu-id="07757-231">Your application workload performance could be sensitive to the fact that some databases are running at different compatibility levels, and therefore, compatibility level consistency across any database could be required in order to provide the same experience to your customers all across the board.</span></span> <span data-ttu-id="07757-232">Observe que isso não é uma exigência, realmente depende de como seu aplicativo é afetado pelo nível de compatibilidade.</span><span class="sxs-lookup"><span data-stu-id="07757-232">Note that it is not a mandate, it really depends on how your application is affected by the compatibility level.</span></span>
* <span data-ttu-id="07757-233">Por fim, em relação à Estimativa de Cardinalidade e como alterar o nível de compatibilidade, antes de continuar na produção, é recomendável testar sua carga de trabalho de produção em novas condições para determinar se seu aplicativo se beneficia das melhorias de Estimativa de Cardinalidade.</span><span class="sxs-lookup"><span data-stu-id="07757-233">Last, regarding the Cardinality Estimation, and just like changing the compatibility level, before proceeding in production, it is recommended to test your production workload under the new conditions to determine if your application benefits from the Cardinality Estimation improvements.</span></span>

## <a name="conclusion"></a><span data-ttu-id="07757-234">Conclusão</span><span class="sxs-lookup"><span data-stu-id="07757-234">Conclusion</span></span>
<span data-ttu-id="07757-235">Usar o Banco de Dados SQL do Azure para se beneficiar de todos os aprimoramentos do SQL Server 2016 claramente pode melhorar suas execuções de consulta.</span><span class="sxs-lookup"><span data-stu-id="07757-235">Using Azure SQL Database to benefit from all SQL Server 2016 enhancements can clearly improve your query executions.</span></span> <span data-ttu-id="07757-236">Exatamente como é!</span><span class="sxs-lookup"><span data-stu-id="07757-236">Just as-is!</span></span> <span data-ttu-id="07757-237">É claro que, como qualquer novo recurso, deve ser feita uma avaliação adequada para determinar as condições exatas em que sua carga de trabalho de banco de dados opera melhor.</span><span class="sxs-lookup"><span data-stu-id="07757-237">Of course, like any new feature, a proper evaluation must be done to determine the exact conditions under which your database workload operates the best.</span></span> <span data-ttu-id="07757-238">A experiência mostra que a maioria das cargas de trabalho deve executar pelo menos de maneira transparente no nível de compatibilidade 130, ao mesmo tempo aproveitando as novas funções de processamento de consulta e a nova Estimativa de Cardinalidade.</span><span class="sxs-lookup"><span data-stu-id="07757-238">Experience shows that most workload are expected to at least run transparently under compatibility level 130, while leveraging new query processing functions, and new Cardinality Estimation.</span></span> <span data-ttu-id="07757-239">Dito isso, na verdade, sempre há algumas exceções e ter fazer uma avaliação cuidadosa adequada é uma avaliação importante para determinar quanto você pode aproveitar esses aperfeiçoamentos.</span><span class="sxs-lookup"><span data-stu-id="07757-239">That said, realistically, there are always some exceptions and doing proper due diligence is an important assessment to determine how much you can benefit from these enhancements.</span></span> <span data-ttu-id="07757-240">E, novamente, o Repositório de Consultas pode ser de grande ajuda para fazer esse trabalho!</span><span class="sxs-lookup"><span data-stu-id="07757-240">And again, the Query Store can be of a great help in doing this work!</span></span>

<span data-ttu-id="07757-241">Conforme o SQL Azure evolui, você pode esperar um nível de compatibilidade 140 no futuro.</span><span class="sxs-lookup"><span data-stu-id="07757-241">As SQL Azure evolves, you can expect a compatibility level 140 in the future.</span></span> <span data-ttu-id="07757-242">No momento adequado, começaremos a falar sobre o que esse futuro nível de compatibilidade 140 trará, assim como brevemente discutimos aqui o que o nível de compatibilidade 130 está trazendo hoje.</span><span class="sxs-lookup"><span data-stu-id="07757-242">When time is appropriate, we will start talking about what this future compatibility level 140 will bring, just as we briefly discussed here what compatibility level 130 is bringing today.</span></span>

<span data-ttu-id="07757-243">Por enquanto, não vamos nos esquecer, a partir de junho de 2016, o Banco de Dados SQL do Azure mudará do nível de compatibilidade padrão 120 para o 130 para bancos de dados recém-criados.</span><span class="sxs-lookup"><span data-stu-id="07757-243">For now, let’s not forget, starting June 2016, Azure SQL Database will change the default compatibility level from 120 to 130 for newly created databases.</span></span> <span data-ttu-id="07757-244">Lembre-se!</span><span class="sxs-lookup"><span data-stu-id="07757-244">Be aware!</span></span>

## <a name="references"></a><span data-ttu-id="07757-245">Referências</span><span class="sxs-lookup"><span data-stu-id="07757-245">References</span></span>
* [<span data-ttu-id="07757-246">O que há de novo no mecanismo de banco de dados</span><span class="sxs-lookup"><span data-stu-id="07757-246">What’s New in Database Engine</span></span>](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [<span data-ttu-id="07757-247">Blog: Repositório de Consultas: um gravador de dados de voo para o banco de dados, por Borko Novakovic, de 8 de junho de 2016</span><span class="sxs-lookup"><span data-stu-id="07757-247">Blog: Query Store: A flight data recorder for your database, by Borko Novakovic, June 8 2016</span></span>](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [<span data-ttu-id="07757-248">Nível de compatibilidade ALTER DATABASE (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="07757-248">ALTER DATABASE Compatibility Level (Transact-SQL)</span></span>](https://msdn.microsoft.com/library/bb510680.aspx)
* [<span data-ttu-id="07757-249">ALTER DATABASE SCOPED CONFIGURATION</span><span class="sxs-lookup"><span data-stu-id="07757-249">ALTER DATABASE SCOPED CONFIGURATION</span></span>](https://msdn.microsoft.com/library/mt629158.aspx)
* [<span data-ttu-id="07757-250">Nível de compatibilidade 130 para Banco de Dados SQL do Azure V12</span><span class="sxs-lookup"><span data-stu-id="07757-250">Compatibility Level 130 for Azure SQL Database V12</span></span>](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [<span data-ttu-id="07757-251">Otimizando seus planos de consulta com o Avaliador de Cardinalidade SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="07757-251">Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator</span></span>](https://msdn.microsoft.com/library/dn673537.aspx)
* [<span data-ttu-id="07757-252">Guia de índices ColumnStore</span><span class="sxs-lookup"><span data-stu-id="07757-252">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
* [<span data-ttu-id="07757-253">Blog: Desempenho aprimorado de consultas com nível de compatibilidade 130 no Banco de Dados SQL do Azure, por Alain Lissoir, 6 de maio de 2016</span><span class="sxs-lookup"><span data-stu-id="07757-253">Blog: Improved Query Performance with Compatibility Level 130 in Azure SQL Database, by Alain Lissoir, May 6 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)

<!--
Improved Query Performance with Compatibility Level 130 in Azure SQL Database

May 6, 2016 by Alain Lissoir (AlainL), on GitHub 'alainlissoir'.

https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/

..... Now, above.
....................
..... Soon, below?

CAPS / MSDN ideally, but instead on ACom:
.. # Assess effects of latest compatibility level on query performance, how to

sql-database-compatibility-level-query-performance-130.md

genemi = MightyPen , 2016-05-20  Friday  17:00pm
-->
