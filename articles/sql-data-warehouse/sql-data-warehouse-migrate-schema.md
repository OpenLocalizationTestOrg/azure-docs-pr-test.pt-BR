---
title: Migrar seu esquema para o SQL Data Warehouse | Microsoft Docs
description: "Dicas para migrar seu esquema para o SQL Data Warehouse do Azure para desenvolvimento de soluções."
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
ms.openlocfilehash: 07ca2321852e276502187e768177e7e82bdfd080
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-schemas-to-sql-data-warehouse"></a><span data-ttu-id="10beb-103">Migrar seus esquemas para o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="10beb-103">Migrate your schemas to SQL Data Warehouse</span></span>
<span data-ttu-id="10beb-104">Diretrizes para migrar os esquemas do SQL para o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="10beb-104">Guidance for migrating your SQL schemas to SQL Data Warehouse.</span></span> 

## <a name="plan-your-schema-migration"></a><span data-ttu-id="10beb-105">Planejar a migração de esquema</span><span class="sxs-lookup"><span data-stu-id="10beb-105">Plan your schema migration</span></span>

<span data-ttu-id="10beb-106">Ao planejar uma migração, confira a [visão geral da tabela][table overview] para se familiarizar com as considerações de design de tabela, como estatísticas, distribuição, particionamento e indexação.</span><span class="sxs-lookup"><span data-stu-id="10beb-106">As you plan a migration, see the [table overview][table overview] to become familiar with table design considerations such as statistics, distribution, partitioning, and indexing.</span></span>  <span data-ttu-id="10beb-107">Também lista alguns [recursos de tabela sem suporte][unsupported table features] e suas soluções alternativas.</span><span class="sxs-lookup"><span data-stu-id="10beb-107">It also lists some [unsupported table features][unsupported table features] and their workarounds.</span></span>

## <a name="use-user-defined-schemas-to-consolidate-databases"></a><span data-ttu-id="10beb-108">Use esquemas definidos pelo usuário para consolidar os bancos de dados</span><span class="sxs-lookup"><span data-stu-id="10beb-108">Use user-defined schemas to consolidate databases</span></span>

<span data-ttu-id="10beb-109">Provavelmente, a carga de trabalho tem mais de um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="10beb-109">Your existing workload probably has more than one database.</span></span> <span data-ttu-id="10beb-110">Por exemplo, um data warehouse do SQL Server pode incluir um banco de dados de preparo, um banco de dados do data warehouse e alguns bancos de dados do data mart.</span><span class="sxs-lookup"><span data-stu-id="10beb-110">For example, a SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="10beb-111">Nessa topologia, cada banco de dados é executado como uma carga de trabalho separada, com políticas de segurança separadas.</span><span class="sxs-lookup"><span data-stu-id="10beb-111">In this topology, each database runs as a separate workload with separate security policies.</span></span>

<span data-ttu-id="10beb-112">Por outro lado, o SQL Data Warehouse executa toda a carga de trabalho do data warehouse em um só banco de dados.</span><span class="sxs-lookup"><span data-stu-id="10beb-112">By contrast, SQL Data Warehouse runs the entire data warehouse workload within one database.</span></span> <span data-ttu-id="10beb-113">Uniões cruzadas de banco de dados não são permitidas.</span><span class="sxs-lookup"><span data-stu-id="10beb-113">Cross database joins are not permitted.</span></span> <span data-ttu-id="10beb-114">Portanto, o SQL Data Warehouse espera que todas as tabelas usadas pelo data warehouse sejam armazenadas em um só banco de dados.</span><span class="sxs-lookup"><span data-stu-id="10beb-114">Therefore, SQL Data Warehouse expects all tables used by the data warehouse to be stored within the one database.</span></span>

<span data-ttu-id="10beb-115">É recomendável usar esquemas definidos pelo usuário para consolidar sua carga de trabalho existente em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="10beb-115">We recommend using user-defined schemas to consolidate your existing workload into one database.</span></span> <span data-ttu-id="10beb-116">Para obter exemplos, confira [Esquemas definidos pelo usuário](sql-data-warehouse-develop-user-defined-schemas.md)</span><span class="sxs-lookup"><span data-stu-id="10beb-116">For examples, see [User-defined schemas](sql-data-warehouse-develop-user-defined-schemas.md)</span></span>

## <a name="use-compatible-data-types"></a><span data-ttu-id="10beb-117">Usar tipos de dados compatíveis</span><span class="sxs-lookup"><span data-stu-id="10beb-117">Use compatible data types</span></span>
<span data-ttu-id="10beb-118">Modifique os tipos de dados para serem compatíveis com o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="10beb-118">Modify your data types to be compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="10beb-119">Para obter uma lista de tipos de dados com e sem suporte, confira [tipos de dados][data types].</span><span class="sxs-lookup"><span data-stu-id="10beb-119">For a list of supported and unsupported data types, see [data types][data types].</span></span> <span data-ttu-id="10beb-120">Esse tópico fornece soluções alternativas para os tipos sem suporte.</span><span class="sxs-lookup"><span data-stu-id="10beb-120">That topic gives workarounds for the unsupported types.</span></span> <span data-ttu-id="10beb-121">Também fornece uma consulta para identificar os tipos existentes que não têm suporte no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="10beb-121">It also provides a query to identify existing types that are not supported in SQL Data Warehouse.</span></span>

## <a name="minimize-row-size"></a><span data-ttu-id="10beb-122">Minimizar o tamanho de linha</span><span class="sxs-lookup"><span data-stu-id="10beb-122">Minimize row size</span></span>
<span data-ttu-id="10beb-123">Para obter o melhor desempenho, minimize o tamanho de linha das tabelas.</span><span class="sxs-lookup"><span data-stu-id="10beb-123">For best performance, minimize the row length of your tables.</span></span> <span data-ttu-id="10beb-124">Como comprimentos de linha menores resultam em melhor desempenho, use os menores tipos de dados que funcionarem para os dados.</span><span class="sxs-lookup"><span data-stu-id="10beb-124">Since shorter row lengths lead to better performance, use the smallest data types that work for your data.</span></span> 

<span data-ttu-id="10beb-125">Para a largura da linha de tabela, o PolyBase tem um limite de 1 MB.</span><span class="sxs-lookup"><span data-stu-id="10beb-125">For table row width, PolyBase has a 1 MB limit.</span></span>  <span data-ttu-id="10beb-126">Se você pretende carregar dados no SQL Data Warehouse com o PolyBase, atualize as tabelas para que as larguras de linha máximas sejam inferiores a 1 MB.</span><span class="sxs-lookup"><span data-stu-id="10beb-126">If you plan to load data into SQL Data Warehouse with PolyBase, update your tables to have maximum row widths of less than 1 MB.</span></span> 

<!--
- For example, this table uses variable length data but the largest possible size of the row is still less than 1 MB. PolyBase will load data into this table.

- This table uses variable length data and the defined row width is less than one MB. When loading rows, PolyBase allocates the full length of the variable-length data. The full length of this row is greater than one MB.  PolyBase will not load data into this table.  

-->

## <a name="specify-the-distribution-option"></a><span data-ttu-id="10beb-127">Especifique a opção de distribuição</span><span class="sxs-lookup"><span data-stu-id="10beb-127">Specify the distribution option</span></span>
<span data-ttu-id="10beb-128">SQL Data Warehouse é um sistema de banco de dados distribuído.</span><span class="sxs-lookup"><span data-stu-id="10beb-128">SQL Data Warehouse is a distributed database system.</span></span> <span data-ttu-id="10beb-129">Cada tabela é distribuída ou replicada em todos os nós de Computação.</span><span class="sxs-lookup"><span data-stu-id="10beb-129">Each table is distributed or replicated across the Compute nodes.</span></span> <span data-ttu-id="10beb-130">Há uma opção de tabela que permite que você especifique como distribuir os dados.</span><span class="sxs-lookup"><span data-stu-id="10beb-130">There's a table option that lets you specify how to distribute the data.</span></span> <span data-ttu-id="10beb-131">As opções são round robin, replicado ou hash distribuído.</span><span class="sxs-lookup"><span data-stu-id="10beb-131">The choices are  round-robin, replicated, or hash distributed.</span></span> <span data-ttu-id="10beb-132">Cada um tem prós e contras.</span><span class="sxs-lookup"><span data-stu-id="10beb-132">Each has pros and cons.</span></span> <span data-ttu-id="10beb-133">Se você não especificar a opção de distribuição, o SQL Data Warehouse usará round-robin como o padrão.</span><span class="sxs-lookup"><span data-stu-id="10beb-133">If you don't specify the distribution option, SQL Data Warehouse will use round-robin as the default.</span></span>

- <span data-ttu-id="10beb-134">Round robin é o padrão.</span><span class="sxs-lookup"><span data-stu-id="10beb-134">Round-robin is the default.</span></span> <span data-ttu-id="10beb-135">É mais simples de usar e carrega os dados tão rápido quanto possível, mas junções exigirão a movimentação de dados, o que reduz o desempenho da consulta.</span><span class="sxs-lookup"><span data-stu-id="10beb-135">It is the simplest to use, and loads the data as fast as possible, but joins will require data movement which slows query performance.</span></span>
- <span data-ttu-id="10beb-136">O item replicado armazena uma cópia da tabela em cada nó de computação.</span><span class="sxs-lookup"><span data-stu-id="10beb-136">Replicated stores a copy of the table on each Compute node.</span></span> <span data-ttu-id="10beb-137">Tabelas replicadas são eficazes porque não exigem a movimentação de dados para junções e agregações.</span><span class="sxs-lookup"><span data-stu-id="10beb-137">Replicated tables are performant because they do not require data movement for joins and aggregations.</span></span> <span data-ttu-id="10beb-138">Isso exige armazenamento adicional e, assim, funciona melhor para tabelas menores.</span><span class="sxs-lookup"><span data-stu-id="10beb-138">They do require extra storage, and therefore work best for smaller tables.</span></span>
- <span data-ttu-id="10beb-139">O hash distribuído distribui as linhas em todos os nós por meio de uma função de hash.</span><span class="sxs-lookup"><span data-stu-id="10beb-139">Hash distributed distributes the rows across all the nodes via a hash function.</span></span> <span data-ttu-id="10beb-140">As tabelas de hash distribuída são a essência do SQL Data Warehouse, pois foram projetadas para oferecer alto desempenho de consultas em tabelas grandes.</span><span class="sxs-lookup"><span data-stu-id="10beb-140">Hash distributed tables are the heart of SQL Data Warehouse since they are designed to provide high query performance on large tables.</span></span> <span data-ttu-id="10beb-141">Essa opção requer planejamento para selecionar a melhor coluna na qual distribuir os dados.</span><span class="sxs-lookup"><span data-stu-id="10beb-141">This option requires some planning to select the best column on which to distribute the data.</span></span> <span data-ttu-id="10beb-142">No entanto, se não escolher a melhor coluna na primeira vez, você poderá facilmente redistribuir os dados em uma coluna diferente.</span><span class="sxs-lookup"><span data-stu-id="10beb-142">However, if you don't choose the best column the first time, you can easily re-distribute the data on a different column.</span></span> 

<span data-ttu-id="10beb-143">Para escolher a melhor opção de distribuição para cada tabela, confira [Tabelas distribuídas](sql-data-warehouse-tables-distribute.md).</span><span class="sxs-lookup"><span data-stu-id="10beb-143">To choose the best distribution option for each table, see [Distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="10beb-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="10beb-144">Next steps</span></span>
<span data-ttu-id="10beb-145">Depois de migrar com êxito o esquema do seu banco de dados para o SQL Data Warehouse, passe para um dos artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="10beb-145">Once you have successfully migrated your database schema to SQL Data Warehouse, proceed to one of the following articles:</span></span>

* <span data-ttu-id="10beb-146">[Migrar seus dados][Migrate your data]</span><span class="sxs-lookup"><span data-stu-id="10beb-146">[Migrate your data][Migrate your data]</span></span>
* <span data-ttu-id="10beb-147">[Migrar seu código][Migrate your code]</span><span class="sxs-lookup"><span data-stu-id="10beb-147">[Migrate your code][Migrate your code]</span></span>

<span data-ttu-id="10beb-148">Para saber mais sobre as práticas recomendadas do SQL Data Warehouse, confira o artigo sobre as [práticas recomendadas][best practices].</span><span class="sxs-lookup"><span data-stu-id="10beb-148">For more about SQL Data Warehouse best practices, see the [best practices][best practices] article.</span></span>

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
