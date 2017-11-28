---
title: "nível de compatibilidade 130 - banco de dados SQL do aaaDatabase | Microsoft Docs"
description: "Neste artigo, vamos explore Olá benefícios da execução do seu banco de dados do SQL Azure no nível de compatibilidade 130 e aproveitar os benefícios de Olá Olá novo Otimizador de consulta e recursos do processador de consulta. Podemos também abordam Olá possíveis efeitos colaterais no desempenho da consulta Olá para aplicativos de SQL existentes hello."
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
ms.openlocfilehash: 25693c5f7b01405b7073fa7d4cc2833fbe125e2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a><span data-ttu-id="66bb1-104">Desempenho aprimorado de consultas com nível de compatibilidade 130 no Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="66bb1-104">Improved query performance with compatibility Level 130 in Azure SQL Database</span></span>
<span data-ttu-id="66bb1-105">Banco de dados SQL do Azure está executando transparentemente centenas de milhares de bancos de dados em vários níveis de compatibilidade diferentes, preservando e garantindo a versão correspondente do hello compatibilidade com versões anteriores toohello do Microsoft SQL Server para todos os seus clientes!</span><span class="sxs-lookup"><span data-stu-id="66bb1-105">Azure SQL Database is running transparently hundreds of thousands of databases at many different compatibility levels, preserving and guaranteeing hello backward compatibility toohello corresponding version of Microsoft SQL Server for all its customers!</span></span>

<span data-ttu-id="66bb1-106">Neste artigo, vamos explore Olá benefícios da execução do seu banco de dados do SQL Azure no nível de compatibilidade 130 e aproveitar os benefícios de Olá Olá novo Otimizador de consulta e recursos do processador de consulta.</span><span class="sxs-lookup"><span data-stu-id="66bb1-106">In this article, we explore hello benefits of running your Azure SQL Databse at compatibility level 130, and leveraging hello benefits of hello new query optimizer and query processor features.</span></span> <span data-ttu-id="66bb1-107">Podemos também abordam Olá possíveis efeitos colaterais no desempenho da consulta Olá para aplicativos de SQL existentes hello.</span><span class="sxs-lookup"><span data-stu-id="66bb1-107">We also address hello possible side-effects on hello query performance for hello existing SQL applications.</span></span>

<span data-ttu-id="66bb1-108">Como um lembrete de histórico, alinhamento de saudação de níveis de compatibilidade com versões SQL toodefault são:</span><span class="sxs-lookup"><span data-stu-id="66bb1-108">As a reminder of history, hello alignment of SQL versions toodefault compatibility levels are as follows:</span></span>

* <span data-ttu-id="66bb1-109">100: no SQL Server 2008 e no Banco de Dados SQL do Azure V11.</span><span class="sxs-lookup"><span data-stu-id="66bb1-109">100: in SQL Server 2008 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="66bb1-110">110: no SQL Server 2012 e no Banco de Dados SQL do Azure V11.</span><span class="sxs-lookup"><span data-stu-id="66bb1-110">110: in SQL Server 2012 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="66bb1-111">120: no SQL Server 2014 e no Banco de Dados SQL do Azure V12.</span><span class="sxs-lookup"><span data-stu-id="66bb1-111">120: in SQL Server 2014 and Azure SQL Database V12.</span></span>
* <span data-ttu-id="66bb1-112">130: no SQL Server 2016 e no Banco de Dados SQL do Azure V12.</span><span class="sxs-lookup"><span data-stu-id="66bb1-112">130: in SQL Server 2016 and Azure SQL Database V12.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="66bb1-113">A partir do **meados de junho de 2016**, no banco de dados SQL Azure, o nível de compatibilidade padrão Olá será 130 em vez de 120 para **recém-criado** bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="66bb1-113">Starting in **mid-June 2016**, in Azure SQL Database, hello default compatibility level will be 130 instead of 120 for **newly created** databases.</span></span>
> 
> <span data-ttu-id="66bb1-114">Bancos de dados criados antes de meados de junho de 2016 *não* serão afetados e manterão seu nível de compatibilidade atual (100, 110 ou 120).</span><span class="sxs-lookup"><span data-stu-id="66bb1-114">Databases created before mid-June 2016 will *not* be affected, and will maintain their current compatibility level (100, 110, or 120).</span></span> <span data-ttu-id="66bb1-115">Bancos de dados migrados de banco de dados SQL versão V11 tooV12 terá um nível de compatibilidade de 100 ou 110.</span><span class="sxs-lookup"><span data-stu-id="66bb1-115">Databases that migrated from Azure SQL Database version V11 tooV12 will have a compatibility level of either 100 or 110.</span></span> 
> 

## <a name="about-compatibility-level-130"></a><span data-ttu-id="66bb1-116">Sobre o nível de compatibilidade 130</span><span class="sxs-lookup"><span data-stu-id="66bb1-116">About compatibility level 130</span></span>
<span data-ttu-id="66bb1-117">Primeiro, se você quiser tooknow Olá atual nível de compatibilidade do banco de dados, execute Olá instrução Transact-SQL a seguir.</span><span class="sxs-lookup"><span data-stu-id="66bb1-117">First, if you want tooknow hello current compatibility level of your database, execute hello following Transact-SQL statement.</span></span>

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


<span data-ttu-id="66bb1-118">Antes desta alteração toolevel 130 ocorre para **recentemente** criar bancos de dados, vamos examinar o que essa alteração está relacionado a alguns exemplos de consulta muito básica e ver como qualquer pessoa pode se beneficiar dela.</span><span class="sxs-lookup"><span data-stu-id="66bb1-118">Before this change toolevel 130 happens for **newly** created databases, let’s review what this change is all about through some very basic query examples, and see how anyone can benefit from it.</span></span>

<span data-ttu-id="66bb1-119">Processamento de consultas em bancos de dados relacionais pode ser muito complexo e pode levar toolots computador ciência e matemática toounderstand Olá inerente escolhas de design e comportamentos.</span><span class="sxs-lookup"><span data-stu-id="66bb1-119">Query processing in relational databases can be very complex and can lead toolots of computer science and mathematics toounderstand hello inherent design choices and behaviors.</span></span> <span data-ttu-id="66bb1-120">Neste documento, conteúdo de saudação foi tooensure intencionalmente simplificado que qualquer pessoa com algumas técnicas básicas mínimo pode entender o impacto de saudação de alteração do nível de compatibilidade hello e determinar como ele pode se beneficiar de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="66bb1-120">In this document, hello content has been intentionally simplified tooensure that anyone with some minimum technical background can understand hello impact of hello compatibility level change and determine how it can benefit applications.</span></span>

<span data-ttu-id="66bb1-121">Vamos dar uma olhada rápida o nível de compatibilidade 130 Olá coloca na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="66bb1-121">Let’s have a quick look at what hello compatibility level 130 brings at hello table.</span></span>  <span data-ttu-id="66bb1-122">Você pode encontrar mais detalhes em [ALTERAR o nível de compatibilidade do BANCO DE DADOS (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), mas aqui está um breve resumo:</span><span class="sxs-lookup"><span data-stu-id="66bb1-122">You can find more details at [ALTER DATABASE Compatibility Level (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), but here is a short summary:</span></span>

* <span data-ttu-id="66bb1-123">Hello operação de inserção de uma instrução Insert select pode ser multithread ou pode ter um plano paralelo, embora antes dessa operação era single-threaded.</span><span class="sxs-lookup"><span data-stu-id="66bb1-123">hello Insert operation of an Insert-select statement can be multi-threaded or can have a parallel plan, while before this operation was single-threaded.</span></span>
* <span data-ttu-id="66bb1-124">Tabela com Otimização de Memória e consultas de variáveis de tabela agora podem ter planos paralelos, enquanto antes essa operação também era de single-thread.</span><span class="sxs-lookup"><span data-stu-id="66bb1-124">Memory Optimized table and table variables queries can now have parallel plans, while before this operation was also single-threaded .</span></span>
* <span data-ttu-id="66bb1-125">As estatísticas de tabela com Otimização de Memória agora podem ser utilizadas e são atualizadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="66bb1-125">Statistics for Memory Optimized table can now be sampled and are auto-updated.</span></span> <span data-ttu-id="66bb1-126">Consulte [O que há de novo no mecanismo de banco de dados: OLTP na memória](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="66bb1-126">See [What's New in Database Engine: In-Memory OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) for more details.</span></span>
* <span data-ttu-id="66bb1-127">Modo de lote vs. Modo de Linha muda com índices de Repositório de Coluna</span><span class="sxs-lookup"><span data-stu-id="66bb1-127">Batch mode v/s Row Mode changes with Column Store indexes</span></span>
  * <span data-ttu-id="66bb1-128">As classificações em uma tabela com um índice de Repositório de Coluna agora estão em modo de lote.</span><span class="sxs-lookup"><span data-stu-id="66bb1-128">Sorts on a table with a Column Store index are now in batch mode.</span></span>
  * <span data-ttu-id="66bb1-129">As agregações em janela agora operam em modo de lote como instruções TSQL LAG/LEAD.</span><span class="sxs-lookup"><span data-stu-id="66bb1-129">Windowing aggregates now operate in batch mode such as TSQL LAG/LEAD statements.</span></span>
  * <span data-ttu-id="66bb1-130">Consultas em tabelas de Repositório de Coluna com Múltiplas cláusulas distintas operam em modo de Lote.</span><span class="sxs-lookup"><span data-stu-id="66bb1-130">Queries on Column Store tables with Multiple distinct clauses operate in Batch mode.</span></span>
  * <span data-ttu-id="66bb1-131">Consultas em execução com DOP = 1 ou um plano serial também são executadas em Modo de Lote.</span><span class="sxs-lookup"><span data-stu-id="66bb1-131">Queries running under DOP=1 or with a serial plan also execute in Batch Mode.</span></span>
* <span data-ttu-id="66bb1-132">Por último, melhorias de estimativa de cardinalidade realmente são provenientes com nível de compatibilidade 120, mas para aqueles em execução em uma compatibilidade mais baixo nível (ou seja, 100 ou 110), hello mover toocompatibility nível 130 também fará com que esses melhorias e eles também podem tirar proveito do desempenho de consulta de saudação de seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="66bb1-132">Last, Cardinality Estimation improvements are actually coming with compatibility level 120, but for those of you running at a lower Compatibility level (i.e. 100, or 110), hello move toocompatibility level 130 will also bring these improvements, and these can also benefit hello query performance of your applications.</span></span>

## <a name="practicing-compatibility-level-130"></a><span data-ttu-id="66bb1-133">Praticando o nível de compatibilidade 130</span><span class="sxs-lookup"><span data-stu-id="66bb1-133">Practicing compatibility level 130</span></span>
<span data-ttu-id="66bb1-134">Primeiro, vamos algumas tabelas, índices e dados aleatórios criados toopractice alguns desses recursos.</span><span class="sxs-lookup"><span data-stu-id="66bb1-134">First let’s get some tables, indexes and random data created toopractice some of these new capabilities.</span></span> <span data-ttu-id="66bb1-135">exemplos de script TSQL Olá podem ser executados no SQL Server 2016 ou no banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="66bb1-135">hello TSQL script examples can be executed under SQL Server 2016, or under Azure SQL Database.</span></span> <span data-ttu-id="66bb1-136">No entanto, ao criar um banco de dados do SQL Azure, certifique-se de escolher por Olá mínimo um P2 de banco de dados porque você precisa de pelo menos dois núcleos tooallow multithreading e, portanto, aproveitar esses recursos.</span><span class="sxs-lookup"><span data-stu-id="66bb1-136">However, when creating an Azure SQL database, make sure you choose at hello minimum a P2 database because you need at least a couple of cores tooallow multi-threading and therefore benefit from these features.</span></span>

```
-- Create a Premium P2 Database in Azure SQL Database

CREATE DATABASE MyTestDB
    (EDITION=’Premium’, SERVICE_OBJECTIVE=’P2′);
GO

-- Create 2 tables with a column store index on
-- hello second one (only available on Premium databases)

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


<span data-ttu-id="66bb1-137">Agora, vamos dar uma toosome aparência dos recursos de processamento de consulta Olá vêm com o nível de compatibilidade 130.</span><span class="sxs-lookup"><span data-stu-id="66bb1-137">Now, let’s have a look toosome of hello Query Processing features coming with compatibility level 130.</span></span>

## <a name="parallel-insert"></a><span data-ttu-id="66bb1-138">INSERT paralela</span><span class="sxs-lookup"><span data-stu-id="66bb1-138">Parallel INSERT</span></span>
<span data-ttu-id="66bb1-139">Executar instruções de TSQL Olá abaixo executa Olá operação de inserção no nível de compatibilidade 120 e 130, que executa respectivamente Olá operação de inserção em um único modelo de thread (120) e em um modelo multi-threaded (130).</span><span class="sxs-lookup"><span data-stu-id="66bb1-139">Executing hello TSQL statements below executes hello INSERT operation under compatibility level 120 and 130, which respectively executes hello INSERT operation in a single threaded model (120), and in a multi-threaded model (130).</span></span>

```
-- Parallel INSERT … SELECT … in heap or CCI
-- is available under 130 only

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO 

-- hello INSERT part is in serial

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130
GO

-- hello INSERT part is in parallel

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

SET STATISTICS XML OFF;
```


<span data-ttu-id="66bb1-140">Solicitando o plano de consulta real Olá Olá, examinando sua representação gráfica ou seu conteúdo XML, você pode determinar quais estimativa de cardinalidade função está em execução.</span><span class="sxs-lookup"><span data-stu-id="66bb1-140">By requesting hello actual hello query plan, looking at its graphical representation or its XML content, you can determine which Cardinality Estimation function is at play.</span></span> <span data-ttu-id="66bb1-141">Analisar planos de saudação lado a lado na Figura 1, podem ver claramente que Olá execução de inserção de repositório de coluna for de serial em 120 tooparallel em 130.</span><span class="sxs-lookup"><span data-stu-id="66bb1-141">Looking at hello plans side-by-side on figure 1, we can clearly see that hello Column Store INSERT execution goes from serial in 120 tooparallel in 130.</span></span> <span data-ttu-id="66bb1-142">Observe também, essa alteração de saudação do ícone de iterador Olá no plano de 130 Olá mostrando duas setas paralelas, ilustrar o fato de Olá Olá agora a execução do iterador é realmente paralela.</span><span class="sxs-lookup"><span data-stu-id="66bb1-142">Also, note that hello change of hello iterator icon in hello 130 plan showing two parallel arrows, illustrating hello fact that now hello iterator execution is indeed parallel.</span></span> <span data-ttu-id="66bb1-143">Se você tiver grande toocomplete de operações de inserção, execução paralela hello, número toohello vinculado do núcleo que à sua disposição para banco de dados Olá, terão um desempenho melhor; Dependendo da sua situação backup tooa 100 vezes mais rápido!</span><span class="sxs-lookup"><span data-stu-id="66bb1-143">If you have large INSERT operations toocomplete, hello parallel execution, linked toohello number of core you have at your disposal for hello database, will perform better; up tooa 100 times faster depending your situation!</span></span>

<span data-ttu-id="66bb1-144">*Figura 1: Inserir alterações de operação de tooparallel serial com nível de compatibilidade 130.*</span><span class="sxs-lookup"><span data-stu-id="66bb1-144">*Figure 1: INSERT operation changes from serial tooparallel with compatibility level 130.*</span></span>

![A figura 1](./media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a><span data-ttu-id="66bb1-146">Modo de lote SERIAL</span><span class="sxs-lookup"><span data-stu-id="66bb1-146">SERIAL Batch Mode</span></span>
<span data-ttu-id="66bb1-147">Da mesma forma, mover toocompatibility nível 130 durante o processamento de linhas de dados permite o processamento de modo de lote.</span><span class="sxs-lookup"><span data-stu-id="66bb1-147">Similarly, moving toocompatibility level 130 when processing rows of data enables batch mode processing.</span></span> <span data-ttu-id="66bb1-148">Primeiro, operações no modo de lote só estão disponíveis quando você tem um índice de repositório de coluna em vigor.</span><span class="sxs-lookup"><span data-stu-id="66bb1-148">First, batch mode operations  are only available when you have a column store index in place.</span></span> <span data-ttu-id="66bb1-149">Em segundo lugar, um lote normalmente representa aproximadamente 900 linhas e usa uma lógica de código otimizada para CPU com vários núcleos, a maior taxa de transferência de memória e diretamente aproveita Olá dados compactados de saudação repositório de coluna sempre que possível.</span><span class="sxs-lookup"><span data-stu-id="66bb1-149">Second, a batch typically represents ~900 rows, and uses a code logic optimized for multicore CPU, higher memory throughput and directly leverages hello compressed data of hello Column Store whenever possible.</span></span> <span data-ttu-id="66bb1-150">Sob essas condições, SQL Server 2016 pode processar aproximadamente 900 linhas ao mesmo tempo, em vez de 1 linha no tempo de saudação, e como consequência, hello custo geral da operação de saudação agora compartilhado por lote inteiro de hello, reduzindo o custo por linha hello geral.</span><span class="sxs-lookup"><span data-stu-id="66bb1-150">Under these conditions, SQL Server 2016 can process ~900 rows at once, instead of 1 row at hello time, and as a consequence, hello overall overhead cost of hello operation is now shared by hello entire batch, reducing hello overall cost by row.</span></span> <span data-ttu-id="66bb1-151">Essa quantidade compartilhada de operações combinada com a compactação do repositório de coluna Olá basicamente reduz a latência de saudação envolvida em uma operação de modo de seleção de lote.</span><span class="sxs-lookup"><span data-stu-id="66bb1-151">This shared amount of operations combined with hello column store compression basically reduces hello latency involved in a SELECT batch mode operation.</span></span> <span data-ttu-id="66bb1-152">Você pode encontrar mais detalhes sobre o repositório de coluna hello e lotes de modo a [guia de índices Columnstore](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="66bb1-152">You can find more details about hello column store and batch mode at [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

```
-- Serial batch mode execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT (C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO 

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="66bb1-153">Como visível abaixo, observando Olá consulta planos-lado a lado na Figura 2, podemos ver que o modo de processamento Olá foi alterado com o nível de compatibilidade de saudação e como consequência, ao executar consultas de saudação em ambos os nível de compatibilidade completamente, podemos ver que a maioria do tempo de processamento de saudação é gasto em linha em comparação com o modo (86%) toohello modo de lote (% 14), onde 2 lotes foram processadas.</span><span class="sxs-lookup"><span data-stu-id="66bb1-153">As visible below, by observing hello query plans side-by-side on figure 2, we can see that hello processing mode has changed with hello compatibility level, and as a consequence, when executing hello queries in both compatibility level altogether, we can see that most of hello processing time is spent in row mode (86%) compared toohello batch mode (14%), where 2 batches have been processed.</span></span> <span data-ttu-id="66bb1-154">Aumentar conjunto de dados hello, hello benefício aumentam.</span><span class="sxs-lookup"><span data-stu-id="66bb1-154">Increase hello dataset, hello benefit will increase.</span></span>

<span data-ttu-id="66bb1-155">*Figura 2: Selecione as alterações de operação de modo serial toobatch com nível de compatibilidade 130.*</span><span class="sxs-lookup"><span data-stu-id="66bb1-155">*Figure 2: SELECT operation changes from serial toobatch mode with compatibility level 130.*</span></span>

![Figura 2](./media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a><span data-ttu-id="66bb1-157">Modo em lotes em Execução de Classificação</span><span class="sxs-lookup"><span data-stu-id="66bb1-157">Batch mode on Sort Execution</span></span>
<span data-ttu-id="66bb1-158">Semelhante toohello acima, mas a operação de classificação tooa aplicada, a transição de saudação do (nível de compatibilidade 120) toobatch modo linha (nível de compatibilidade 130) aprimora o desempenho Olá Olá a operação de classificação para Olá mesmos motivos.</span><span class="sxs-lookup"><span data-stu-id="66bb1-158">Similar toohello above, but applied tooa sort operation, hello transition from row mode (compatibility level 120) toobatch mode (compatibility level 130) improves hello performance of hello SORT operation for hello same reasons.</span></span>

```
-- Batch mode on sort execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="66bb1-159">Visível-lado a lado na Figura 3, podemos ver que a operação de classificação Olá no modo de linha representa 81% de saudação de custo, enquanto o modo de lote Olá representa apenas 19% do custo da saudação (respectivamente 81% e % de 56 na classificação de saudação em si).</span><span class="sxs-lookup"><span data-stu-id="66bb1-159">Visible side-by-side on figure 3, we can see that hello sort operation in row mode represents 81% of hello cost, while hello batch mode only represents 19% of hello cost (respectively 81% and 56% on hello sort itself).</span></span>

<span data-ttu-id="66bb1-160">*Figura 3: Operação de classificação é alterado de modo de toobatch de linha com o nível de compatibilidade 130.*</span><span class="sxs-lookup"><span data-stu-id="66bb1-160">*Figure 3: SORT operation changes from row toobatch mode with compatibility level 130.*</span></span>

![A figura 3](./media/sql-database-compatibility-level-query-performance-130/figure-3.png)

<span data-ttu-id="66bb1-162">Obviamente, esses exemplos só contêm dezenas de milhares de linhas, que é nada ao analisar dados de saudação disponíveis na maioria dos SQL Servers hoje em dia.</span><span class="sxs-lookup"><span data-stu-id="66bb1-162">Obviously, these samples only contain tens of thousands of rows, which is nothing when looking at hello data available in most SQL Servers these days.</span></span> <span data-ttu-id="66bb1-163">Apenas projeto esses executada em milhões de linhas em vez disso, e isso pode se transformar em alguns minutos de execução dispensados diariamente pendentes natureza Olá da carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="66bb1-163">Just project these against millions of rows instead, and this can translate in several minutes of execution spared every day pending hello nature of your workload.</span></span>

## <a name="cardinality-estimation-ce-improvements"></a><span data-ttu-id="66bb1-164">Aprimoramentos de CE (Estimativa de Cardinalidade)</span><span class="sxs-lookup"><span data-stu-id="66bb1-164">Cardinality Estimation (CE) improvements</span></span>
<span data-ttu-id="66bb1-165">Introduzido com o SQL Server 2014, qualquer banco de dados em execução em um nível de compatibilidade 120 ou acima fará com que usa Olá nova funcionalidade de estimativa de cardinalidade.</span><span class="sxs-lookup"><span data-stu-id="66bb1-165">Introduced with SQL Server 2014, any database running at a compatibility level 120 or above will make use of hello new Cardinality Estimation functionality.</span></span> <span data-ttu-id="66bb1-166">Essencialmente, a estimativa de cardinalidade é lógica Olá usado toodetermine como o SQL server executará uma consulta com base em seu custo estimado.</span><span class="sxs-lookup"><span data-stu-id="66bb1-166">Essentially, cardinality estimation is hello logic used toodetermine how SQL server will execute a query based on its estimated cost.</span></span> <span data-ttu-id="66bb1-167">estimativa de saudação é calculada com a entrada de estatísticas associadas a objetos envolvidos na consulta.</span><span class="sxs-lookup"><span data-stu-id="66bb1-167">hello estimation is calculated using input from statistics associated with objects involved in that query.</span></span> <span data-ttu-id="66bb1-168">Praticamente, em um nível alto, as funções de estimativa de cardinalidade são estimativas de contagem de linha juntamente com informações sobre distribuição de saudação de valores hello, contagens de valores distintos e contagens duplicadas contido no hello tabelas e objetos referenciados na consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="66bb1-168">Practically, at a high-level, Cardinality Estimation functions are row count estimates along with information about hello distribution of hello values, distinct value counts, and duplicate counts contained in hello tables and objects referenced in hello query.</span></span> <span data-ttu-id="66bb1-169">Obtendo essas estimativas errado, pode levar a e/s de disco toounnecessary devido tooinsufficient concessões de memória (ou seja, o TempDB derramamentos) ou tooa seleção de um plano serial em paralelo plano de execução, tooname alguns.</span><span class="sxs-lookup"><span data-stu-id="66bb1-169">Getting these estimates wrong, can lead toounnecessary disk I/O due tooinsufficient memory grants (i.e. TempDB spills), or tooa selection of a serial plan execution over a parallel plan execution, tooname a few.</span></span> <span data-ttu-id="66bb1-170">Conclusão, estimativas incorretas podem levar tooan degradação do desempenho geral Olá da execução da consulta.</span><span class="sxs-lookup"><span data-stu-id="66bb1-170">Conclusion, incorrect estimates can lead tooan overall performance degradation of hello query execution.</span></span> <span data-ttu-id="66bb1-171">Em Olá outro lado, melhores estimativas, mais estimativas precisas, clientes potenciais toobetter as execuções de consulta!</span><span class="sxs-lookup"><span data-stu-id="66bb1-171">On hello other side, better estimates, more accurate estimates, leads toobetter query executions!</span></span>

<span data-ttu-id="66bb1-172">Como mencionado anteriormente, otimizações de consulta e as previsões são um assunto complexo, mas toolearn mais informações sobre planos de consulta e o avaliador de cardinalidade, você pode consultar documentos toohello em [otimizar seus planos de consulta com hello SQL Server 2014 Avaliador de cardinalidade](https://msdn.microsoft.com/library/dn673537.aspx) para aprofundar.</span><span class="sxs-lookup"><span data-stu-id="66bb1-172">As mentioned before, query optimizations and estimates are a complex matter, but if you want toolearn more about query plans and cardinality estimator, you can refer toohello document at [Optimizing Your Query Plans with hello SQL Server 2014 Cardinality Estimator](https://msdn.microsoft.com/library/dn673537.aspx) for a deeper dive.</span></span>

## <a name="which-cardinality-estimation-do-you-currently-use"></a><span data-ttu-id="66bb1-173">Que Estimativa de Cardinalidade você usa atualmente?</span><span class="sxs-lookup"><span data-stu-id="66bb1-173">Which Cardinality Estimation do you currently use?</span></span>
<span data-ttu-id="66bb1-174">toodetermine sob qual estimativa de cardinalidade executam suas consultas, vamos usar apenas a consulta de saudação exemplos abaixo.</span><span class="sxs-lookup"><span data-stu-id="66bb1-174">toodetermine under which Cardinality Estimation your queries are running, let’s just use hello query samples below.</span></span> <span data-ttu-id="66bb1-175">Observe que este primeiro exemplo será executado com nível de compatibilidade 110, indicando o uso de saudação de funções de estimativa de cardinalidade antigos hello.</span><span class="sxs-lookup"><span data-stu-id="66bb1-175">Note that this first example will run under compatibility level 110, implying hello use of hello old Cardinality Estimation functions.</span></span>

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


<span data-ttu-id="66bb1-176">Após a conclusão da execução, clique no link XML hello e examinar propriedades de saudação do iterador primeiro hello, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="66bb1-176">Once execution is complete, click on hello XML link, and look at hello properties of hello first iterator as shown below.</span></span> <span data-ttu-id="66bb1-177">Observe o nome da propriedade Olá chamado CardinalityEstimationModelVersion definido no momento em 70.</span><span class="sxs-lookup"><span data-stu-id="66bb1-177">Note hello property name called CardinalityEstimationModelVersion currently set on 70.</span></span> <span data-ttu-id="66bb1-178">Isso não significa que nível de compatibilidade do banco de dados de saudação é definido a versão do SQL Server 7.0 toohello (definido em 110 como visível em instruções de TSQL Olá acima), mas valor Olá 70 simplesmente representa Olá herdada estimativa de cardinalidade funcionalidade disponível desde o SQL Servidor 7.0, que não tinha nenhum revisões principais até que o SQL Server 2014 (que vem com um nível de compatibilidade 120).</span><span class="sxs-lookup"><span data-stu-id="66bb1-178">It does not mean that hello database compatibility level is set toohello SQL Server 7.0 version (it is set on 110 as visible in hello TSQL statements above), but hello value 70 simply represents hello legacy Cardinality Estimation functionality available since SQL Server 7.0, which had no major revisions until SQL Server 2014 (which comes with a compatibility level of 120).</span></span>

<span data-ttu-id="66bb1-179">*Figura 4: Olá CardinalityEstimationModelVersion é definido too70 ao usar um nível de compatibilidade de 110 ou abaixo.*</span><span class="sxs-lookup"><span data-stu-id="66bb1-179">*Figure 4: hello CardinalityEstimationModelVersion is set too70 when using a compatibility level of 110 or below.*</span></span>

![Figura 4](./media/sql-database-compatibility-level-query-performance-130/figure-4.png)

<span data-ttu-id="66bb1-181">Como alternativa, você pode alterar too130 de nível de compatibilidade de saudação e desabilitar o uso de saudação da nova função de estimativa de cardinalidade hello usando Olá LEGACY_CARDINALITY_ESTIMATION definir tooON com [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span><span class="sxs-lookup"><span data-stu-id="66bb1-181">Alternatively, you can change hello compatibility level too130, and disable hello use of hello new Cardinality Estimation function by using hello LEGACY_CARDINALITY_ESTIMATION set tooON with [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span></span> <span data-ttu-id="66bb1-182">Isso será ser exatamente Olá mesmo que usar 110 de estimativa de cardinalidade função de uma perspectiva, ao usar o nível de compatibilidade de processamento de consulta mais recente hello.</span><span class="sxs-lookup"><span data-stu-id="66bb1-182">This will be exactly hello same as using 110 from a Cardinality Estimation function point of view, while using hello latest query processing compatibility level.</span></span> <span data-ttu-id="66bb1-183">Dessa forma, que você pode se beneficiar de nova consulta de saudação vêm com o nível de compatibilidade mais recente hello (ou seja, o modo de lote) de recursos de processamento, mas ainda dependem de funcionalidade de estimativa de cardinalidade antiga Olá se necessário.</span><span class="sxs-lookup"><span data-stu-id="66bb1-183">Doing so, you can benefit from hello new query processing features coming with hello latest compatibility level (i.e. batch mode), but still rely on hello old Cardinality Estimation functionality if necessary.</span></span>

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


<span data-ttu-id="66bb1-184">Simplesmente mover toohello nível de compatibilidade 120 ou 130 habilita a funcionalidade de estimativa de cardinalidade novo hello.</span><span class="sxs-lookup"><span data-stu-id="66bb1-184">Simply moving toohello compatibility level 120 or 130 enables hello new Cardinality Estimation functionality.</span></span> <span data-ttu-id="66bb1-185">Nesse caso, Olá padrão CardinalityEstimationModelVersion será definido adequadamente too120 ou 130 como visível abaixo.</span><span class="sxs-lookup"><span data-stu-id="66bb1-185">In such a case, hello default CardinalityEstimationModelVersion will be set accordingly too120 or 130 as visible below.</span></span>

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


<span data-ttu-id="66bb1-186">*Figura 5: Olá CardinalityEstimationModelVersion é definido too130 ao usar um nível de compatibilidade 130.*</span><span class="sxs-lookup"><span data-stu-id="66bb1-186">*Figure 5: hello CardinalityEstimationModelVersion is set too130 when using a compatibility level of 130.*</span></span>

![Figura 5](./media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-hello-cardinality-estimation-differences"></a><span data-ttu-id="66bb1-188">Diferenças de estimativa de cardinalidade Olá testemunhando</span><span class="sxs-lookup"><span data-stu-id="66bb1-188">Witnessing hello Cardinality Estimation differences</span></span>
<span data-ttu-id="66bb1-189">Agora, vamos executar um pouco mais complexo que envolvem uma INNER JOIN com uma cláusula WHERE com alguns predicados de consulta e vamos dar uma olhada na estimativa de contagem de linha de saudação da função de estimativa de cardinalidade antiga hello primeiro.</span><span class="sxs-lookup"><span data-stu-id="66bb1-189">Now, let’s run a slightly more complex query involving an INNER JOIN with a WHERE clause with some predicates, and let’s look at hello row count estimate from hello old Cardinality Estimation function first.</span></span>

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


<span data-ttu-id="66bb1-190">A execução desta consulta efetivamente retorna 200,704 linhas, enquanto Olá estimativa de linha com a funcionalidade de estimativa de cardinalidade antiga Olá declarações 194,284 linhas.</span><span class="sxs-lookup"><span data-stu-id="66bb1-190">Executing this query effectively returns 200,704 rows, while hello row estimate with hello old Cardinality Estimation functionality claims 194,284 rows.</span></span> <span data-ttu-id="66bb1-191">Obviamente, como já dissemos, esses resultados de contagem de linha também dependerá quantas vezes você executou Olá exemplos anteriores, que preenche as tabelas de exemplo hello repetidamente em cada execução.</span><span class="sxs-lookup"><span data-stu-id="66bb1-191">Obviously, as said before, these row count results will also depend how often you ran hello previous samples, which populates hello sample tables over and over again at each run.</span></span> <span data-ttu-id="66bb1-192">Obviamente, predicados de saudação em sua consulta também terá uma influência na estimativa de real Olá além de forma de tabela hello, conteúdo de dados e como esses dados realmente correlacionam entre si.</span><span class="sxs-lookup"><span data-stu-id="66bb1-192">Obviously, hello predicates in your query will also have an influence on hello actual estimation aside from hello table shape, data content, and how this data actually correlate with each other.</span></span>

<span data-ttu-id="66bb1-193">*Figura 6: estimativa de contagem de linha de saudação é 194,284 ou 6.000 linhas fora de linhas de 200,704 Olá esperadas.*</span><span class="sxs-lookup"><span data-stu-id="66bb1-193">*Figure 6: hello row count estimate is 194,284 or 6,000 rows off from hello 200,704 rows expected.*</span></span>

![Figura 6](./media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

<span data-ttu-id="66bb1-195">Em Olá mesma forma, vamos executar agora Olá mesma consulta com a nova funcionalidade de estimativa de cardinalidade hello.</span><span class="sxs-lookup"><span data-stu-id="66bb1-195">In hello same way, let’s now execute hello same query with hello new Cardinality Estimation functionality.</span></span>

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


<span data-ttu-id="66bb1-196">Observando Olá abaixo, agora vemos que estimativa de linha de saudação é 202,877, ou muito mais próximo e maior do que o hello estimativa de cardinalidade antigo.</span><span class="sxs-lookup"><span data-stu-id="66bb1-196">Looking at hello below, we now see that hello row estimate is 202,877, or much closer and higher than hello old Cardinality Estimation.</span></span>

<span data-ttu-id="66bb1-197">*Figura 7: estimativa de contagem de linha hello agora é 202,877, em vez de 194,284.*</span><span class="sxs-lookup"><span data-stu-id="66bb1-197">*Figure 7: hello row count estimate is now 202,877, instead of 194,284.*</span></span>

![Figura 7](./media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

<span data-ttu-id="66bb1-199">Na realidade, o conjunto de resultados de saudação é 200,704 linhas (mas tudo depende de quantas vezes você tiver executado consultas Olá Olá exemplos anteriores, mas é mais importante, como Olá TSQL usa a instrução de rand () do hello, Olá real valores retornados podem variar com toohello de execução de um lado).</span><span class="sxs-lookup"><span data-stu-id="66bb1-199">In reality, hello result set is 200,704 rows (but all of it depends how often you did run hello queries of hello previous samples, but more importantly, because hello TSQL uses hello RAND() statement, hello actual values returned can vary from one run toohello next).</span></span> <span data-ttu-id="66bb1-200">Portanto, nesse exemplo específico, hello nova estimativa de cardinalidade faz um trabalho melhor ao estimar o número de saudação de linhas porque 202,877 é muito mais perto too200, 704, que 194,284!</span><span class="sxs-lookup"><span data-stu-id="66bb1-200">Therefore, in this particular example, hello new Cardinality Estimation does a better job at estimating hello number of rows because 202,877 is much closer too200,704, than 194,284!</span></span> <span data-ttu-id="66bb1-201">Último, se você alterar Olá cláusula WHERE predicados tooequality (em vez de ">" para a instância), isso poderia fazer estimativas de saudação entre hello antiga e nova função de cardinalidade ainda mais diferentes, dependendo de quantas correspondências, você pode obter.</span><span class="sxs-lookup"><span data-stu-id="66bb1-201">Last, if you change hello WHERE clause predicates tooequality (rather than “>” for instance), this could make hello estimates between hello old and new Cardinality function even more different, depending on how many matches you can get.</span></span>

<span data-ttu-id="66bb1-202">Obviamente, nesse caso, estar ~6000 aquém da contagem real não representa muitos dados em algumas situações.</span><span class="sxs-lookup"><span data-stu-id="66bb1-202">Obviously, in this case, being ~6000 rows off from actual count does not represent a lot of data in some situations.</span></span> <span data-ttu-id="66bb1-203">Agora, transpor essa toomillions de linhas em várias tabelas e consultas mais complexas e estimativa de saudação às vezes pode ficar inativo por milhões de linhas e hello, portanto, o risco de separação-up Olá incorreto de plano de execução, ou solicitar memória insuficiente concede à esquerda derramamentos tooTempDB e assim por mais de e/s, são muito maior.</span><span class="sxs-lookup"><span data-stu-id="66bb1-203">Now, transpose this toomillions of rows across several tables and more complex queries, and at times hello estimate can be off by millions of rows , and therefore, hello risk of picking-up hello wrong execution plan, or requesting insufficient memory grants leading tooTempDB spills, and so more I/O, are much higher.</span></span>

<span data-ttu-id="66bb1-204">Se você tem a oportunidade de hello, práticas essa comparação com suas consultas mais comuns e os conjuntos de dados e ver por conta própria em quanto algumas das estimativas de saudação antiga e nova são afetadas, enquanto alguns podem acabou de se tornar mais fora da realidade hello, ou alguns outros simplesmente as contagens de linhas de real toohello mais próxima, na verdade, retornadas em conjuntos de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="66bb1-204">If you have hello opportunity, practice this comparison with your most typical queries and datasets, and see for yourself by how much some of hello old and new estimates are affected, while some could just become more off from hello reality, or some others just simply closer toohello actual row counts actually returned in hello result sets.</span></span> <span data-ttu-id="66bb1-205">Tudo depende da forma de saudação de consultas, características de banco de dados do SQL Azure hello, natureza hello e tamanho de saudação de conjuntos de dados e estatísticas de saudação disponíveis sobre eles.</span><span class="sxs-lookup"><span data-stu-id="66bb1-205">All of it will depend of hello shape of your queries, hello Azure SQL database characteristics, hello nature and hello size of your datasets, and hello statistics available about them.</span></span> <span data-ttu-id="66bb1-206">Se você acabou de criar sua instância de banco de dados SQL, a consulta de saudação otimizador terá toobuild seu conhecimento do zero, em vez de estatísticas reutilizando feitas da consulta anterior Olá será executado.</span><span class="sxs-lookup"><span data-stu-id="66bb1-206">If you just created your Azure SQL Database instance, hello query optimizer will have toobuild its knowledge from scratch instead of reusing statistics made of hello previous query runs.</span></span> <span data-ttu-id="66bb1-207">Portanto, Olá estimativas são situação tooevery muito contextuais e quase específico de servidores e aplicativos.</span><span class="sxs-lookup"><span data-stu-id="66bb1-207">So, hello estimates are very contextual and almost specific tooevery server and application situation.</span></span> <span data-ttu-id="66bb1-208">Ele é tookeep um aspecto importante em mente!</span><span class="sxs-lookup"><span data-stu-id="66bb1-208">It is an important aspect tookeep in mind!</span></span>

## <a name="some-considerations-tootake-into-account"></a><span data-ttu-id="66bb1-209">Tootake algumas considerações para a conta</span><span class="sxs-lookup"><span data-stu-id="66bb1-209">Some considerations tootake into account</span></span>
<span data-ttu-id="66bb1-210">Embora a maioria das cargas de trabalho pode se beneficiar do nível de compatibilidade 130, Olá antes de adoção de nível de compatibilidade de saudação para seu ambiente de produção, você basicamente tem 3 opções:</span><span class="sxs-lookup"><span data-stu-id="66bb1-210">Although most workloads would benefit from hello compatibility level 130, before you adopting hello compatibility level for your production environment, you basically have 3 options:</span></span>

1. <span data-ttu-id="66bb1-211">Mover toocompatibility nível 130 e veja como fazer as coisas.</span><span class="sxs-lookup"><span data-stu-id="66bb1-211">You move toocompatibility level 130, and see how things perform.</span></span> <span data-ttu-id="66bb1-212">No caso de você observar algumas regressões, simplesmente definir tooits back nível de compatibilidade Olá nível original, ou manter 130 e reverter somente modo herdado do hello estimativa de cardinalidade toohello back (conforme explicado acima, isso sozinho pode solucionar problema de saudação).</span><span class="sxs-lookup"><span data-stu-id="66bb1-212">In case you notice some regressions, you just simply set hello compatibility level back tooits original level, or keep 130, and only reverse hello Cardinality Estimation back toohello legacy mode (As explained above, this alone could address hello issue).</span></span>
2. <span data-ttu-id="66bb1-213">Testar seus aplicativos existentes em semelhante à carga de produção, ajustar e validar o desempenho de saudação antes tooproduction contínuo.</span><span class="sxs-lookup"><span data-stu-id="66bb1-213">You thoroughly test your existing applications under similar production load, fine tune, and validate hello performance before going tooproduction.</span></span> <span data-ttu-id="66bb1-214">No caso de problemas, mesmo que acima, você pode sempre voltar toohello nível de compatibilidade original ou simplesmente reverter modo herdado do toohello back Olá estimativa de cardinalidade.</span><span class="sxs-lookup"><span data-stu-id="66bb1-214">In case of issues, same as above, you can always go back toohello original compatibility level, or simply reverse hello Cardinality Estimation back toohello legacy mode.</span></span>
3. <span data-ttu-id="66bb1-215">Como uma opção final e hello tooaddress de maneira mais recente essas perguntas, é o repositório de consultas Olá tooleverage.</span><span class="sxs-lookup"><span data-stu-id="66bb1-215">As a final option, and hello most recent way tooaddress these questions, is tooleverage hello Query Store.</span></span> <span data-ttu-id="66bb1-216">Essa é a opção recomendada de hoje!</span><span class="sxs-lookup"><span data-stu-id="66bb1-216">That’s today’s recommended option!</span></span> <span data-ttu-id="66bb1-217">análise de saudação tooassist de suas consultas sob compatibilidade nível 120 ou abaixo versus 130, não recomendamos que você suficiente toouse repositório de consultas.</span><span class="sxs-lookup"><span data-stu-id="66bb1-217">tooassist hello analysis of your queries under compatibility level 120 or below versus 130, we cannot encourage you enough toouse Query Store.</span></span> <span data-ttu-id="66bb1-218">Repositório de consultas está disponível com a versão mais recente de saudação do Azure SQL Database V12 e foi projetada toohelp é uma solução de problemas de desempenho de consulta.</span><span class="sxs-lookup"><span data-stu-id="66bb1-218">Query Store is available with hello latest version of Azure SQL Database V12, and it’s designed toohelp you with query performance troubleshooting.</span></span> <span data-ttu-id="66bb1-219">Pense Olá repositório de consultas como um gravador de dados de voo para seu banco de dados coletar e apresentar informações históricas sobre todas as consultas.</span><span class="sxs-lookup"><span data-stu-id="66bb1-219">Think of hello Query Store as a flight data recorder for your database collecting and presenting detailed historic information about all queries.</span></span> <span data-ttu-id="66bb1-220">Isso bastante simplifica a análise forense de desempenho, reduzindo Olá tempo toodiagnose e resolver problemas.</span><span class="sxs-lookup"><span data-stu-id="66bb1-220">This greatly simplifies performance forensics by reducing hello time toodiagnose and resolve issues.</span></span> <span data-ttu-id="66bb1-221">Você pode encontrar mais informações no artigo sobre [Repositório de Consultas: o gravador de dados de voo para o banco de dados](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span><span class="sxs-lookup"><span data-stu-id="66bb1-221">You can find more information at [Query Store: A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span></span>

<span data-ttu-id="66bb1-222">Em alto nível, se você já tiver um conjunto de bancos de dados em execução no nível de compatibilidade 120 ou abaixo e planejar toomove de saudação algumas delas too130, ou porque sua carga de trabalho provisionar novos bancos de dados que serão automaticamente assim ser definido por padrão too130, considere seguinte Hello:</span><span class="sxs-lookup"><span data-stu-id="66bb1-222">At hello high-level, if you already have a set of databases running at compatibility level 120 or below, and plan toomove some of them too130, or because your workload automatically provision new databases that will be soon be set by default too130, please consider hello followings:</span></span>

* <span data-ttu-id="66bb1-223">Antes de alterar o novo nível de compatibilidade toohello em produção, habilite o repositório de consultas.</span><span class="sxs-lookup"><span data-stu-id="66bb1-223">Before changing toohello new compatibility level in production, enable Query Store.</span></span> <span data-ttu-id="66bb1-224">Você pode consultar muito[alterar o repositório de consultas de saudação de modo de compatibilidade do banco de dados e o uso de saudação](https://msdn.microsoft.com/library/bb895281.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="66bb1-224">You can refer too[Change hello Database Compatibility Mode and Use hello Query Store](https://msdn.microsoft.com/library/bb895281.aspx) for more information.</span></span>
* <span data-ttu-id="66bb1-225">Em seguida, teste críticas todas as cargas de trabalho usando dados representativos e as consultas de um ambiente de produção e compare o desempenho Olá apresentou e como relatado pelo repositório de consultas.</span><span class="sxs-lookup"><span data-stu-id="66bb1-225">Next, test all critical workloads using representative data and queries of a production-like environment, and compare hello performance experienced and as reported by Query Store.</span></span> <span data-ttu-id="66bb1-226">Se você tiver algum regressões, você pode identificar Olá consultas retornadas por hello repositório de consultas e usar a opção de armazenamento de consulta para forçar o plano hello (também conhecido como plano de fixação).</span><span class="sxs-lookup"><span data-stu-id="66bb1-226">If you experience some regressions, you can identify hello regressed queries with hello Query Store and use hello plan forcing option from Query Store (aka plan pinning).</span></span> <span data-ttu-id="66bb1-227">Nesse caso, você definitivamente permanecer com o nível de compatibilidade de saudação 130 e usar plano de consulta anterior hello como sugerido pelo Olá repositório de consultas.</span><span class="sxs-lookup"><span data-stu-id="66bb1-227">In such a case, you definitively stay with hello compatibility level 130, and use hello former query plan as suggested by hello Query Store.</span></span>
* <span data-ttu-id="66bb1-228">Se você quiser tooleverage novos recursos e funcionalidades do banco de dados do SQL Azure (que está executando o SQL Server 2016), mas é confidenciais toochanges trazido pelo nível de compatibilidade 130, Olá como um último recurso, é possível considerar o forçar novamente o nível de compatibilidade Olá nível de toohello que atenda às suas cargas de trabalho usando a instrução ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="66bb1-228">If you want tooleverage new features and capabilities of Azure SQL Database (which is running SQL Server 2016), but are sensitive toochanges brought by hello compatibility level 130, as a last resort, you could consider forcing hello compatibility level back toohello level that suits your workload by using an ALTER DATABASE statement.</span></span> <span data-ttu-id="66bb1-229">Mas primeiro, lembre-se desse plano do repositório de consultas Olá fixação de opção é a melhor opção porque não usando 130 basicamente permanecer no nível de funcionalidade de saudação de uma versão mais antiga do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="66bb1-229">But first, be aware that hello Query Store plan pinning option is your best option because not using 130 is basically staying at hello functionality level of an older SQL Server version.</span></span>
* <span data-ttu-id="66bb1-230">Se você tiver aplicativos multilocatários, abrangendo vários bancos de dados, pode ser necessário tooupdate Olá provisionamento de lógica de seu bancos de dados de tooensure um nível de compatibilidade consistente em todos os bancos de dados; os antigos e provisionados recentemente.</span><span class="sxs-lookup"><span data-stu-id="66bb1-230">If you have multitenant applications spanning multiple databases, it may be necessary tooupdate hello provisioning logic of your databases tooensure a consistent compatibility level across all databases; old and newly provisioned ones.</span></span> <span data-ttu-id="66bb1-231">O desempenho da carga de trabalho de aplicativo poderia ser fatos toohello confidenciais que alguns bancos de dados estão em execução em níveis de compatibilidade diferentes, e portanto, a consistência de nível de compatibilidade em qualquer banco de dados poderão ser necessária na ordem tooprovide Olá mesmo experiência de clientes tooyour todo quadro hello.</span><span class="sxs-lookup"><span data-stu-id="66bb1-231">Your application workload performance could be sensitive toohello fact that some databases are running at different compatibility levels, and therefore, compatibility level consistency across any database could be required in order tooprovide hello same experience tooyour customers all across hello board.</span></span> <span data-ttu-id="66bb1-232">Observe que não é uma exigência, ela realmente depende de como seu aplicativo é afetado pelo nível de compatibilidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="66bb1-232">Note that it is not a mandate, it really depends on how your application is affected by hello compatibility level.</span></span>
* <span data-ttu-id="66bb1-233">Por fim, sobre Olá estimativa de cardinalidade e como alterar o nível de compatibilidade hello, antes de continuar na produção, é recomendável tootest sua carga de trabalho de produção em Olá novas condições toodetermine se beneficia do seu aplicativo melhorias de estimativa de cardinalidade Hello.</span><span class="sxs-lookup"><span data-stu-id="66bb1-233">Last, regarding hello Cardinality Estimation, and just like changing hello compatibility level, before proceeding in production, it is recommended tootest your production workload under hello new conditions toodetermine if your application benefits from hello Cardinality Estimation improvements.</span></span>

## <a name="conclusion"></a><span data-ttu-id="66bb1-234">Conclusão</span><span class="sxs-lookup"><span data-stu-id="66bb1-234">Conclusion</span></span>
<span data-ttu-id="66bb1-235">Usando o banco de dados do SQL Azure toobenefit de todos os aprimoramentos do SQL Server 2016 claramente pode melhorar as execuções de sua consulta.</span><span class="sxs-lookup"><span data-stu-id="66bb1-235">Using Azure SQL Database toobenefit from all SQL Server 2016 enhancements can clearly improve your query executions.</span></span> <span data-ttu-id="66bb1-236">Exatamente como é!</span><span class="sxs-lookup"><span data-stu-id="66bb1-236">Just as-is!</span></span> <span data-ttu-id="66bb1-237">É claro que, como qualquer novo recurso, uma avaliação adequada deve ser feita condições exata do hello toodetermine sob a qual sua carga de trabalho do banco de dados opera Olá melhor.</span><span class="sxs-lookup"><span data-stu-id="66bb1-237">Of course, like any new feature, a proper evaluation must be done toodetermine hello exact conditions under which your database workload operates hello best.</span></span> <span data-ttu-id="66bb1-238">Experiência mostra que a maioria das cargas de trabalho esperada tooat menos executado de maneira transparente em nível de compatibilidade 130, aproveitando as novas funções e a nova estimativa de cardinalidade de processamento de consulta.</span><span class="sxs-lookup"><span data-stu-id="66bb1-238">Experience shows that most workload are expected tooat least run transparently under compatibility level 130, while leveraging new query processing functions, and new Cardinality Estimation.</span></span> <span data-ttu-id="66bb1-239">Que diz, na verdade, sempre há algumas exceções e fazendo adequado devido auditoria é um toodetermine importante avaliação quanto você pode aproveitar esses aprimoramentos.</span><span class="sxs-lookup"><span data-stu-id="66bb1-239">That said, realistically, there are always some exceptions and doing proper due diligence is an important assessment toodetermine how much you can benefit from these enhancements.</span></span> <span data-ttu-id="66bb1-240">E, novamente, o repositório de consultas de saudação podem ser de muito útil para fazer esse trabalho!</span><span class="sxs-lookup"><span data-stu-id="66bb1-240">And again, hello Query Store can be of a great help in doing this work!</span></span>

<span data-ttu-id="66bb1-241">Como a evolução do SQL Azure, você pode esperar um nível de compatibilidade 140 em Olá futuras.</span><span class="sxs-lookup"><span data-stu-id="66bb1-241">As SQL Azure evolves, you can expect a compatibility level 140 in hello future.</span></span> <span data-ttu-id="66bb1-242">No momento adequado, começaremos a falar sobre o que esse futuro nível de compatibilidade 140 trará, assim como brevemente discutimos aqui o que o nível de compatibilidade 130 está trazendo hoje.</span><span class="sxs-lookup"><span data-stu-id="66bb1-242">When time is appropriate, we will start talking about what this future compatibility level 140 will bring, just as we briefly discussed here what compatibility level 130 is bringing today.</span></span>

<span data-ttu-id="66bb1-243">Por enquanto, vamos não se esqueça de, a partir de junho de 2016, banco de dados do SQL Azure será alterado nível de compatibilidade padrão de saudação de 120 too130 para bancos de dados recém-criado.</span><span class="sxs-lookup"><span data-stu-id="66bb1-243">For now, let’s not forget, starting June 2016, Azure SQL Database will change hello default compatibility level from 120 too130 for newly created databases.</span></span> <span data-ttu-id="66bb1-244">Lembre-se!</span><span class="sxs-lookup"><span data-stu-id="66bb1-244">Be aware!</span></span>

## <a name="references"></a><span data-ttu-id="66bb1-245">Referências</span><span class="sxs-lookup"><span data-stu-id="66bb1-245">References</span></span>
* [<span data-ttu-id="66bb1-246">O que há de novo no mecanismo de banco de dados</span><span class="sxs-lookup"><span data-stu-id="66bb1-246">What’s New in Database Engine</span></span>](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [<span data-ttu-id="66bb1-247">Blog: Repositório de Consultas: um gravador de dados de voo para o banco de dados, por Borko Novakovic, de 8 de junho de 2016</span><span class="sxs-lookup"><span data-stu-id="66bb1-247">Blog: Query Store: A flight data recorder for your database, by Borko Novakovic, June 8 2016</span></span>](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [<span data-ttu-id="66bb1-248">Nível de compatibilidade ALTER DATABASE (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="66bb1-248">ALTER DATABASE Compatibility Level (Transact-SQL)</span></span>](https://msdn.microsoft.com/library/bb510680.aspx)
* [<span data-ttu-id="66bb1-249">ALTER DATABASE SCOPED CONFIGURATION</span><span class="sxs-lookup"><span data-stu-id="66bb1-249">ALTER DATABASE SCOPED CONFIGURATION</span></span>](https://msdn.microsoft.com/library/mt629158.aspx)
* [<span data-ttu-id="66bb1-250">Nível de compatibilidade 130 para Banco de Dados SQL do Azure V12</span><span class="sxs-lookup"><span data-stu-id="66bb1-250">Compatibility Level 130 for Azure SQL Database V12</span></span>](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [<span data-ttu-id="66bb1-251">Otimizando a seus planos de consulta com hello avaliador de cardinalidade do SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="66bb1-251">Optimizing Your Query Plans with hello SQL Server 2014 Cardinality Estimator</span></span>](https://msdn.microsoft.com/library/dn673537.aspx)
* [<span data-ttu-id="66bb1-252">Guia de índices ColumnStore</span><span class="sxs-lookup"><span data-stu-id="66bb1-252">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
* [<span data-ttu-id="66bb1-253">Blog: Desempenho aprimorado de consultas com nível de compatibilidade 130 no Banco de Dados SQL do Azure, por Alain Lissoir, 6 de maio de 2016</span><span class="sxs-lookup"><span data-stu-id="66bb1-253">Blog: Improved Query Performance with Compatibility Level 130 in Azure SQL Database, by Alain Lissoir, May 6 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)

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
