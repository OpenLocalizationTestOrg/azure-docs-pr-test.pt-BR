---
title: aaaMigrate tooSQL o esquema do Data Warehouse | Microsoft Docs
description: "Dicas para migrar seu tooAzure esquema SQL Data Warehouse para o desenvolvimento de soluções."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 538b60c9-a07f-49bf-9ea3-1082ed6699fb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 1309b743b78564575695038a4856d9d25a2b18d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-schemas-toosql-data-warehouse"></a><span data-ttu-id="b10f4-103">Migrar seu tooSQL esquemas do Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b10f4-103">Migrate your schemas tooSQL Data Warehouse</span></span>
<span data-ttu-id="b10f4-104">Diretrizes para migrar seu tooSQL de esquemas do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b10f4-104">Guidance for migrating your SQL schemas tooSQL Data Warehouse.</span></span> 

## <a name="plan-your-schema-migration"></a><span data-ttu-id="b10f4-105">Planejar a migração de esquema</span><span class="sxs-lookup"><span data-stu-id="b10f4-105">Plan your schema migration</span></span>

<span data-ttu-id="b10f4-106">Ao planejar uma migração, consulte Olá [visão geral da tabela] [ table overview] toobecome familiarizado com as considerações de design de tabela, como estatísticas, distribuição, particionamento e indexação.</span><span class="sxs-lookup"><span data-stu-id="b10f4-106">As you plan a migration, see hello [table overview][table overview] toobecome familiar with table design considerations such as statistics, distribution, partitioning, and indexing.</span></span>  <span data-ttu-id="b10f4-107">Também lista alguns [recursos de tabela sem suporte][unsupported table features] e suas soluções alternativas.</span><span class="sxs-lookup"><span data-stu-id="b10f4-107">It also lists some [unsupported table features][unsupported table features] and their workarounds.</span></span>

## <a name="use-user-defined-schemas-tooconsolidate-databases"></a><span data-ttu-id="b10f4-108">Usar bancos de dados de tooconsolidate esquemas definidos pelo usuário</span><span class="sxs-lookup"><span data-stu-id="b10f4-108">Use user-defined schemas tooconsolidate databases</span></span>

<span data-ttu-id="b10f4-109">Provavelmente, a carga de trabalho tem mais de um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b10f4-109">Your existing workload probably has more than one database.</span></span> <span data-ttu-id="b10f4-110">Por exemplo, um data warehouse do SQL Server pode incluir um banco de dados de preparo, um banco de dados do data warehouse e alguns bancos de dados do data mart.</span><span class="sxs-lookup"><span data-stu-id="b10f4-110">For example, a SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="b10f4-111">Nessa topologia, cada banco de dados é executado como uma carga de trabalho separada, com políticas de segurança separadas.</span><span class="sxs-lookup"><span data-stu-id="b10f4-111">In this topology, each database runs as a separate workload with separate security policies.</span></span>

<span data-ttu-id="b10f4-112">Por outro lado, o SQL Data Warehouse é executado a carga de trabalho do hello todo o data warehouse em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b10f4-112">By contrast, SQL Data Warehouse runs hello entire data warehouse workload within one database.</span></span> <span data-ttu-id="b10f4-113">Uniões cruzadas de banco de dados não são permitidas.</span><span class="sxs-lookup"><span data-stu-id="b10f4-113">Cross database joins are not permitted.</span></span> <span data-ttu-id="b10f4-114">Portanto, o SQL Data Warehouse espera que todas as tabelas usadas pelo Olá toobe de depósito de dados armazenado em um banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="b10f4-114">Therefore, SQL Data Warehouse expects all tables used by hello data warehouse toobe stored within hello one database.</span></span>

<span data-ttu-id="b10f4-115">É recomendável usar esquemas definidos pelo usuário tooconsolidate sua carga de trabalho existente em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b10f4-115">We recommend using user-defined schemas tooconsolidate your existing workload into one database.</span></span> <span data-ttu-id="b10f4-116">Para obter exemplos, confira [Esquemas definidos pelo usuário](sql-data-warehouse-develop-user-defined-schemas.md)</span><span class="sxs-lookup"><span data-stu-id="b10f4-116">For examples, see [User-defined schemas](sql-data-warehouse-develop-user-defined-schemas.md)</span></span>

## <a name="use-compatible-data-types"></a><span data-ttu-id="b10f4-117">Usar tipos de dados compatíveis</span><span class="sxs-lookup"><span data-stu-id="b10f4-117">Use compatible data types</span></span>
<span data-ttu-id="b10f4-118">Modifique seu toobe de tipos de dados compatível com o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b10f4-118">Modify your data types toobe compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="b10f4-119">Para obter uma lista de tipos de dados com e sem suporte, confira [tipos de dados][data types].</span><span class="sxs-lookup"><span data-stu-id="b10f4-119">For a list of supported and unsupported data types, see [data types][data types].</span></span> <span data-ttu-id="b10f4-120">Esse tópico fornece soluções alternativas para os tipos de saudação sem suporte.</span><span class="sxs-lookup"><span data-stu-id="b10f4-120">That topic gives workarounds for hello unsupported types.</span></span> <span data-ttu-id="b10f4-121">Ele também fornece uma consulta tooidentify tipos existentes que não têm suporte no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b10f4-121">It also provides a query tooidentify existing types that are not supported in SQL Data Warehouse.</span></span>

## <a name="minimize-row-size"></a><span data-ttu-id="b10f4-122">Minimizar o tamanho de linha</span><span class="sxs-lookup"><span data-stu-id="b10f4-122">Minimize row size</span></span>
<span data-ttu-id="b10f4-123">Para melhor desempenho, minimiza o comprimento de linha de saudação de suas tabelas.</span><span class="sxs-lookup"><span data-stu-id="b10f4-123">For best performance, minimize hello row length of your tables.</span></span> <span data-ttu-id="b10f4-124">Porque os comprimentos de linha menores levam toobetter desempenho, use Olá menor tipos de dados que funcionam para seus dados.</span><span class="sxs-lookup"><span data-stu-id="b10f4-124">Since shorter row lengths lead toobetter performance, use hello smallest data types that work for your data.</span></span> 

<span data-ttu-id="b10f4-125">Para a largura da linha de tabela, o PolyBase tem um limite de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="b10f4-125">For table row width, PolyBase has a 1 MB limit.</span></span>  <span data-ttu-id="b10f4-126">Se você planejar dados tooload no SQL Data Warehouse com o PolyBase, atualize seu larguras de linha máximo tabelas toohave menos de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="b10f4-126">If you plan tooload data into SQL Data Warehouse with PolyBase, update your tables toohave maximum row widths of less than 1 MB.</span></span> 

<!--
- For example, this table uses variable length data but hello largest possible size of hello row is still less than 1 MB. PolyBase will load data into this table.

- This table uses variable length data and hello defined row width is less than one MB. When loading rows, PolyBase allocates hello full length of hello variable-length data. hello full length of this row is greater than one MB.  PolyBase will not load data into this table.  

-->

## <a name="specify-hello-distribution-option"></a><span data-ttu-id="b10f4-127">Especifique a opção de distribuição Olá</span><span class="sxs-lookup"><span data-stu-id="b10f4-127">Specify hello distribution option</span></span>
<span data-ttu-id="b10f4-128">SQL Data Warehouse é um sistema de banco de dados distribuído.</span><span class="sxs-lookup"><span data-stu-id="b10f4-128">SQL Data Warehouse is a distributed database system.</span></span> <span data-ttu-id="b10f4-129">Cada tabela é distribuída ou replicada em nós de computação hello.</span><span class="sxs-lookup"><span data-stu-id="b10f4-129">Each table is distributed or replicated across hello Compute nodes.</span></span> <span data-ttu-id="b10f4-130">Há uma opção de tabela que permite que você especifique como toodistribute Olá dados.</span><span class="sxs-lookup"><span data-stu-id="b10f4-130">There's a table option that lets you specify how toodistribute hello data.</span></span> <span data-ttu-id="b10f4-131">Opções de saudação são round-robin replicado, ou distribuídos de hash.</span><span class="sxs-lookup"><span data-stu-id="b10f4-131">hello choices are  round-robin, replicated, or hash distributed.</span></span> <span data-ttu-id="b10f4-132">Cada um tem prós e contras.</span><span class="sxs-lookup"><span data-stu-id="b10f4-132">Each has pros and cons.</span></span> <span data-ttu-id="b10f4-133">Se você não especificar a opção de distribuição hello, o SQL Data Warehouse usará round-robin como padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="b10f4-133">If you don't specify hello distribution option, SQL Data Warehouse will use round-robin as hello default.</span></span>

- <span data-ttu-id="b10f4-134">Round robin é o padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="b10f4-134">Round-robin is hello default.</span></span> <span data-ttu-id="b10f4-135">Ele é toouse mais simples de saudação e carrega dados de saudação tão rápidos quanto possível, mas junções exigirá a movimentação de dados que reduz o desempenho da consulta.</span><span class="sxs-lookup"><span data-stu-id="b10f4-135">It is hello simplest toouse, and loads hello data as fast as possible, but joins will require data movement which slows query performance.</span></span>
- <span data-ttu-id="b10f4-136">Replicado armazena uma cópia da tabela de saudação em cada nó de computação.</span><span class="sxs-lookup"><span data-stu-id="b10f4-136">Replicated stores a copy of hello table on each Compute node.</span></span> <span data-ttu-id="b10f4-137">Tabelas replicadas são eficazes porque não exigem a movimentação de dados para junções e agregações.</span><span class="sxs-lookup"><span data-stu-id="b10f4-137">Replicated tables are performant because they do not require data movement for joins and aggregations.</span></span> <span data-ttu-id="b10f4-138">Isso exige armazenamento adicional e, assim, funciona melhor para tabelas menores.</span><span class="sxs-lookup"><span data-stu-id="b10f4-138">They do require extra storage, and therefore work best for smaller tables.</span></span>
- <span data-ttu-id="b10f4-139">Hash distribuído distribui as linhas de saudação em todos os nós de saudação por meio de uma função de hash.</span><span class="sxs-lookup"><span data-stu-id="b10f4-139">Hash distributed distributes hello rows across all hello nodes via a hash function.</span></span> <span data-ttu-id="b10f4-140">Tabelas de hash distribuída são coração de saudação do SQL Data Warehouse porque eles são projetados tooprovide alto desempenho de consultas em tabelas grandes.</span><span class="sxs-lookup"><span data-stu-id="b10f4-140">Hash distributed tables are hello heart of SQL Data Warehouse since they are designed tooprovide high query performance on large tables.</span></span> <span data-ttu-id="b10f4-141">Essa opção exige algum planejamento tooselect Olá melhor coluna onde os dados Olá toodistribute.</span><span class="sxs-lookup"><span data-stu-id="b10f4-141">This option requires some planning tooselect hello best column on which toodistribute hello data.</span></span> <span data-ttu-id="b10f4-142">No entanto, se você não escolher Olá Olá de coluna melhor a primeira vez, você pode facilmente novamente distribuir Olá dados em uma coluna diferente.</span><span class="sxs-lookup"><span data-stu-id="b10f4-142">However, if you don't choose hello best column hello first time, you can easily re-distribute hello data on a different column.</span></span> 

<span data-ttu-id="b10f4-143">toochoose Olá melhor opção de distribuição para cada tabela, consulte [distribuídas tabelas](sql-data-warehouse-tables-distribute.md).</span><span class="sxs-lookup"><span data-stu-id="b10f4-143">toochoose hello best distribution option for each table, see [Distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="b10f4-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b10f4-144">Next steps</span></span>
<span data-ttu-id="b10f4-145">Depois que o tooSQL de esquema de banco de dados do Data Warehouse foi migrado com êxito, prossiga tooone de saudação artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b10f4-145">Once you have successfully migrated your database schema tooSQL Data Warehouse, proceed tooone of hello following articles:</span></span>

* <span data-ttu-id="b10f4-146">[Migrar seus dados][Migrate your data]</span><span class="sxs-lookup"><span data-stu-id="b10f4-146">[Migrate your data][Migrate your data]</span></span>
* <span data-ttu-id="b10f4-147">[Migrar seu código][Migrate your code]</span><span class="sxs-lookup"><span data-stu-id="b10f4-147">[Migrate your code][Migrate your code]</span></span>

<span data-ttu-id="b10f4-148">Para obter mais informações sobre as práticas recomendadas do SQL Data Warehouse, consulte Olá [práticas recomendadas] [ best practices] artigo.</span><span class="sxs-lookup"><span data-stu-id="b10f4-148">For more about SQL Data Warehouse best practices, see hello [best practices][best practices] article.</span></span>

<!--Image references-->

<!--Article references-->
[Migrate your code]: ./sql-data-warehouse-migrate-code.md
[Migrate your data]: ./sql-data-warehouse-migrate-data.md
[best practices]: ./sql-data-warehouse-best-practices.md
[table overview]: ./sql-data-warehouse-tables-overview.md
[unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[data types]: ./sql-data-warehouse-tables-data-types.md
[unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types

<!--MSDN references-->


<!--Other Web references-->
