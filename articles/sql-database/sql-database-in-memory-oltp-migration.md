---
title: "O OLTP in-memory melhora o desempenho de transações do SQL | Microsoft Docs"
description: "Adote o OLTP Na Memória para melhorar o desempenho transacional em um banco de dados SQL existente."
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: MightyPen
ms.assetid: c2bf14a0-905b-47b4-afb6-efe9a61147d5
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: jodebrui
ms.openlocfilehash: 50eed9aed417778bd497f55e20c8e732fdae9cf9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-in-memory-oltp-to-improve-your-application-performance-in-sql-database"></a><span data-ttu-id="17c3b-103">Usar o OLTP in-memory para melhorar o desempenho do aplicativo no Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="17c3b-103">Use In-Memory OLTP to improve your application performance in SQL Database</span></span>
<span data-ttu-id="17c3b-104">O [OLTP in-memory](sql-database-in-memory.md) pode ser usado para melhorar o desempenho do processamento de transações, a ingestão de dados e os cenários de dados transitórios, em Bancos de Dados SQL [Premium](sql-database-service-tiers.md) do Azure sem aumentar o tipo de preço.</span><span class="sxs-lookup"><span data-stu-id="17c3b-104">[In-Memory OLTP](sql-database-in-memory.md) can be used to improve the performance of transaction processing, data ingestion, and transient data scenarios, in  [Premium](sql-database-service-tiers.md) Azure SQL Databases without increasing the pricing tier.</span></span> 

> [!NOTE] 
> <span data-ttu-id="17c3b-105">Saiba como o [Quorum dobra a principal carga de trabalho do banco de dados, enquanto reduz a DTU em 70% com o Banco de Dados SQL](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span><span class="sxs-lookup"><span data-stu-id="17c3b-105">Learn how [Quorum doubles key database’s workload while lowering DTU by 70% with SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span></span>


<span data-ttu-id="17c3b-106">Siga estas etapas para adotar o in-memory OLTP no banco de dados existente.</span><span class="sxs-lookup"><span data-stu-id="17c3b-106">Follow these steps to adopt In-Memory OLTP in your existing database.</span></span>

## <a name="step-1-ensure-you-are-using-a-premium-database"></a><span data-ttu-id="17c3b-107">Etapa 1: Garantir que você está usando um banco de dados Premium</span><span class="sxs-lookup"><span data-stu-id="17c3b-107">Step 1: Ensure you are using a Premium database</span></span>
<span data-ttu-id="17c3b-108">Há suporte para o OLTP in-memory apenas em bancos de dados Premium.</span><span class="sxs-lookup"><span data-stu-id="17c3b-108">In-Memory OLTP is supported only in Premium databases.</span></span> <span data-ttu-id="17c3b-109">Na Memória terá suporte se o resultado retornado for 1 (e não 0):</span><span class="sxs-lookup"><span data-stu-id="17c3b-109">In-Memory is supported if the returned result is 1 (not 0):</span></span>

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

<span data-ttu-id="17c3b-110">*XTP* significa *Processamento Extremo de Transações*</span><span class="sxs-lookup"><span data-stu-id="17c3b-110">*XTP* stands for *Extreme Transaction Processing*</span></span>



## <a name="step-2-identify-objects-to-migrate-to-in-memory-oltp"></a><span data-ttu-id="17c3b-111">Etapa 2: Identificar os objetos para migrar para o OLTP Na Memória</span><span class="sxs-lookup"><span data-stu-id="17c3b-111">Step 2: Identify objects to migrate to In-Memory OLTP</span></span>
<span data-ttu-id="17c3b-112">O SSMS inclui um relatório **Visão Geral da Análise do Desempenho da Transação** que pode ser executado em um banco de dados com uma carga de trabalho ativa.</span><span class="sxs-lookup"><span data-stu-id="17c3b-112">SSMS includes a **Transaction Performance Analysis Overview** report that you can run against a database with an active workload.</span></span> <span data-ttu-id="17c3b-113">O relatório identifica as tabelas e os procedimentos armazenados candidatos à migração para OLTP Na Memória.</span><span class="sxs-lookup"><span data-stu-id="17c3b-113">The report identifies tables and stored procedures that are candidates for migration to In-Memory OLTP.</span></span>

<span data-ttu-id="17c3b-114">No SSMS, para gerar o relatório:</span><span class="sxs-lookup"><span data-stu-id="17c3b-114">In SSMS, to generate the report:</span></span>

* <span data-ttu-id="17c3b-115">No **Pesquisador de Objetos**, clique com o botão direito do mouse no nó do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="17c3b-115">In the **Object Explorer**, right-click your database node.</span></span>
* <span data-ttu-id="17c3b-116">Clique em **Relatórios** > **Relatórios Padrão** > **Visão Geral da Análise de Desempenho da Transação**.</span><span class="sxs-lookup"><span data-stu-id="17c3b-116">Click **Reports** > **Standard Reports** > **Transaction Performance Analysis Overview**.</span></span>

<span data-ttu-id="17c3b-117">Para saber mais, confira [Determinando se uma tabela ou um procedimento armazenado deve ser transportado para o OLTP Na Memória](http://msdn.microsoft.com/library/dn205133.aspx).</span><span class="sxs-lookup"><span data-stu-id="17c3b-117">For more information, see [Determining if a Table or Stored Procedure Should Be Ported to In-Memory OLTP](http://msdn.microsoft.com/library/dn205133.aspx).</span></span>

## <a name="step-3-create-a-comparable-test-database"></a><span data-ttu-id="17c3b-118">Etapa 3: Criar um banco de dados de teste comparável</span><span class="sxs-lookup"><span data-stu-id="17c3b-118">Step 3: Create a comparable test database</span></span>
<span data-ttu-id="17c3b-119">Suponha que o relatório indique que o banco de dados tem uma tabela que pode se beneficiar do que está sendo convertido em uma tabela com otimização de memória.</span><span class="sxs-lookup"><span data-stu-id="17c3b-119">Suppose the report indicates your database has a table that would benefit from being converted to a memory-optimized table.</span></span> <span data-ttu-id="17c3b-120">É recomendável que você primeiro teste para confirmar a indicação.</span><span class="sxs-lookup"><span data-stu-id="17c3b-120">We recommend that you first test to confirm the indication by testing.</span></span>

<span data-ttu-id="17c3b-121">Você precisa de uma cópia de teste do seu banco de dados de produção.</span><span class="sxs-lookup"><span data-stu-id="17c3b-121">You need a test copy of your production database.</span></span> <span data-ttu-id="17c3b-122">O banco de dados de teste deve estar no mesmo nível da camada de serviço que o banco de dados de produção.</span><span class="sxs-lookup"><span data-stu-id="17c3b-122">The test database should be at the same service tier level as your production database.</span></span>

<span data-ttu-id="17c3b-123">Para facilitar o teste, ajuste seu banco de dados de teste da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="17c3b-123">To ease testing, tweak your test database as follows:</span></span>

1. <span data-ttu-id="17c3b-124">Conecte-se ao banco de dados de teste usando o SSMS.</span><span class="sxs-lookup"><span data-stu-id="17c3b-124">Connect to the test database by using SSMS.</span></span>
2. <span data-ttu-id="17c3b-125">Para evitar a necessidade da opção WITH (SNAPSHOT) em consultas, defina a opção de banco de dados como mostrado na seguinte instrução T-SQL:</span><span class="sxs-lookup"><span data-stu-id="17c3b-125">To avoid needing the WITH (SNAPSHOT) option in queries, set the database option as shown in the following T-SQL statement:</span></span>
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a><span data-ttu-id="17c3b-126">Etapa 4: migrar tabelas</span><span class="sxs-lookup"><span data-stu-id="17c3b-126">Step 4: Migrate tables</span></span>
<span data-ttu-id="17c3b-127">Você deve criar e preencher uma cópia com otimização de memória da tabela que você deseja testar.</span><span class="sxs-lookup"><span data-stu-id="17c3b-127">You must create and populate a memory-optimized copy of the table you want to test.</span></span> <span data-ttu-id="17c3b-128">Você pode criá-la usando:</span><span class="sxs-lookup"><span data-stu-id="17c3b-128">You can create it by using either:</span></span>

* <span data-ttu-id="17c3b-129">O Assistente de Otimização de Memória útil no SSMS.</span><span class="sxs-lookup"><span data-stu-id="17c3b-129">The handy Memory Optimization Wizard in SSMS.</span></span>
* <span data-ttu-id="17c3b-130">T-SQL Manual.</span><span class="sxs-lookup"><span data-stu-id="17c3b-130">Manual T-SQL.</span></span>

#### <a name="memory-optimization-wizard-in-ssms"></a><span data-ttu-id="17c3b-131">Assistente de Otimização de Memória no SSMS</span><span class="sxs-lookup"><span data-stu-id="17c3b-131">Memory Optimization Wizard in SSMS</span></span>
<span data-ttu-id="17c3b-132">Para usar essa opção de migração:</span><span class="sxs-lookup"><span data-stu-id="17c3b-132">To use this migration option:</span></span>

1. <span data-ttu-id="17c3b-133">Conecte-se ao banco de dados de teste com o SSMS.</span><span class="sxs-lookup"><span data-stu-id="17c3b-133">Connect to the test database with SSMS.</span></span>
2. <span data-ttu-id="17c3b-134">No **Pesquisador de Objetos**, clique com o botão direito do mouse na tabela e clique em **Supervisor de Otimização de Memória**.</span><span class="sxs-lookup"><span data-stu-id="17c3b-134">In the **Object Explorer**, right-click on the table, and then click **Memory Optimization Advisor**.</span></span>
   
   * <span data-ttu-id="17c3b-135">O assistente **Supervisor Otimizador de Memória da Tabela** é exibido.</span><span class="sxs-lookup"><span data-stu-id="17c3b-135">The **Table Memory Optimizer Advisor** wizard is displayed.</span></span>
3. <span data-ttu-id="17c3b-136">No assistente, clique em **Validação de migração** (ou no botão **Avançar**) para ver se a tabela tem algum recurso sem suporte nas tabelas com otimização de memória.</span><span class="sxs-lookup"><span data-stu-id="17c3b-136">In the wizard, click **Migration validation** (or the **Next** button) to see if the table has any unsupported features that are unsupported in memory-optimized tables.</span></span> <span data-ttu-id="17c3b-137">Para obter mais informações, consulte:</span><span class="sxs-lookup"><span data-stu-id="17c3b-137">For more information, see:</span></span>
   
   * <span data-ttu-id="17c3b-138">A *lista de verificação de otimização de memória* no [Supervisor de Otimização de Memória](http://msdn.microsoft.com/library/dn284308.aspx).</span><span class="sxs-lookup"><span data-stu-id="17c3b-138">The *memory optimization checklist* in [Memory Optimization Advisor](http://msdn.microsoft.com/library/dn284308.aspx).</span></span>
   * <span data-ttu-id="17c3b-139">[Construções Transact-SQL sem suporte do OLTP Na Memória](http://msdn.microsoft.com/library/dn246937.aspx).</span><span class="sxs-lookup"><span data-stu-id="17c3b-139">[Transact-SQL Constructs Not Supported by In-Memory OLTP](http://msdn.microsoft.com/library/dn246937.aspx).</span></span>
   * <span data-ttu-id="17c3b-140">[Migrando para o OLTP Na Memória](http://msdn.microsoft.com/library/dn247639.aspx).</span><span class="sxs-lookup"><span data-stu-id="17c3b-140">[Migrating to In-Memory OLTP](http://msdn.microsoft.com/library/dn247639.aspx).</span></span>
4. <span data-ttu-id="17c3b-141">Se a tabela não tiver recursos sem suporte, o supervisor poderá executar o esquema e a migração de dados reais para você.</span><span class="sxs-lookup"><span data-stu-id="17c3b-141">If the table has no unsupported features, the advisor can perform the actual schema and data migration for you.</span></span>

#### <a name="manual-t-sql"></a><span data-ttu-id="17c3b-142">T-SQL Manual</span><span class="sxs-lookup"><span data-stu-id="17c3b-142">Manual T-SQL</span></span>
<span data-ttu-id="17c3b-143">Para usar essa opção de migração:</span><span class="sxs-lookup"><span data-stu-id="17c3b-143">To use this migration option:</span></span>

1. <span data-ttu-id="17c3b-144">Conecte-se ao banco de dados de teste usando o SSMS (ou um utilitário semelhante).</span><span class="sxs-lookup"><span data-stu-id="17c3b-144">Connect to your test database by using SSMS (or a similar utility).</span></span>
2. <span data-ttu-id="17c3b-145">Obtenha o script T-SQL completo para a tabela e seus índices.</span><span class="sxs-lookup"><span data-stu-id="17c3b-145">Obtain the complete T-SQL script for your table and its indexes.</span></span>
   
   * <span data-ttu-id="17c3b-146">No SSMS, clique com o botão direito do mouse no nó da sua tabela.</span><span class="sxs-lookup"><span data-stu-id="17c3b-146">In SSMS, right-click your table node.</span></span>
   * <span data-ttu-id="17c3b-147">Clique em **Script de Tabela como** > **CRIAR Para** > **Nova Janela de Consulta**.</span><span class="sxs-lookup"><span data-stu-id="17c3b-147">Click **Script Table As** > **CREATE To** > **New Query Window**.</span></span>
3. <span data-ttu-id="17c3b-148">Na janela de script, adicione WITH (MEMORY_OPTIMIZED = ON) à instrução CREATE TABLE.</span><span class="sxs-lookup"><span data-stu-id="17c3b-148">In the script window, add WITH (MEMORY_OPTIMIZED = ON) to the CREATE TABLE statement.</span></span>
4. <span data-ttu-id="17c3b-149">Se houver um índice CLUSTERED, altere-o para NONCLUSTERED.</span><span class="sxs-lookup"><span data-stu-id="17c3b-149">If there is a CLUSTERED index, change it to NONCLUSTERED.</span></span>
5. <span data-ttu-id="17c3b-150">Renomeie a tabela existente usando SP_RENAME.</span><span class="sxs-lookup"><span data-stu-id="17c3b-150">Rename the existing table by using SP_RENAME.</span></span>
6. <span data-ttu-id="17c3b-151">Crie a nova cópia da tabela com otimização de memória executando o script CREATE TABLE editado.</span><span class="sxs-lookup"><span data-stu-id="17c3b-151">Create the new memory-optimized copy of the table by running your edited CREATE TABLE script.</span></span>
7. <span data-ttu-id="17c3b-152">Copie os dados para sua tabela com otimização de memória usando INSERT...SELECT * INTO:</span><span class="sxs-lookup"><span data-stu-id="17c3b-152">Copy the data to your memory-optimized table by using INSERT...SELECT * INTO:</span></span>

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a><span data-ttu-id="17c3b-153">Etapa 5 (opcional): migrar procedimentos armazenados</span><span class="sxs-lookup"><span data-stu-id="17c3b-153">Step 5 (optional): Migrate stored procedures</span></span>
<span data-ttu-id="17c3b-154">O recurso Na Memória também pode modificar um procedimento armazenado para melhorar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="17c3b-154">The In-Memory feature can also modify a stored procedure for improved performance.</span></span>

### <a name="considerations-with-natively-compiled-stored-procedures"></a><span data-ttu-id="17c3b-155">Considerações sobre procedimentos armazenados compilados nativamente</span><span class="sxs-lookup"><span data-stu-id="17c3b-155">Considerations with natively compiled stored procedures</span></span>
<span data-ttu-id="17c3b-156">Um procedimento armazenado compilado nativamente deve ter as seguintes opções na sua cláusula WITH T-SQL:</span><span class="sxs-lookup"><span data-stu-id="17c3b-156">A natively compiled stored procedure must have the following options on its T-SQL WITH clause:</span></span>

* <span data-ttu-id="17c3b-157">NATIVE_COMPILATION</span><span class="sxs-lookup"><span data-stu-id="17c3b-157">NATIVE_COMPILATION</span></span>
* <span data-ttu-id="17c3b-158">SCHEMABINDING: significa tabelas cujas definições de coluna o procedimento armazenado não pode alterar de alguma forma que afete o próprio procedimento armazenado, a menos que você descarte o procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="17c3b-158">SCHEMABINDING: meaning tables that the stored procedure cannot have their column definitions changed in any way that would affect the stored procedure, unless you drop the stored procedure.</span></span>

<span data-ttu-id="17c3b-159">Um módulo nativo deve usar grandes [blocos ATOMIC](http://msdn.microsoft.com/library/dn452281.aspx) para o gerenciamento de transações.</span><span class="sxs-lookup"><span data-stu-id="17c3b-159">A native module must use one big [ATOMIC blocks](http://msdn.microsoft.com/library/dn452281.aspx) for transaction management.</span></span> <span data-ttu-id="17c3b-160">Não há uma função para BEGIN TRANSACTION explícita ou para ROLLBACK TRANSACTION.</span><span class="sxs-lookup"><span data-stu-id="17c3b-160">There is no role for an explicit BEGIN TRANSACTION, or for ROLLBACK TRANSACTION.</span></span> <span data-ttu-id="17c3b-161">Se seu código detectar uma violação de uma regra de negócio, poderá finalizar o bloco atômico com uma instrução [THROW](http://msdn.microsoft.com/library/ee677615.aspx) .</span><span class="sxs-lookup"><span data-stu-id="17c3b-161">If your code detects a violation of a business rule, it can terminate the atomic block with a [THROW](http://msdn.microsoft.com/library/ee677615.aspx) statement.</span></span>

### <a name="typical-create-procedure-for-natively-compiled"></a><span data-ttu-id="17c3b-162">CREATE PROCEDURE típico para compilados nativamente</span><span class="sxs-lookup"><span data-stu-id="17c3b-162">Typical CREATE PROCEDURE for natively compiled</span></span>
<span data-ttu-id="17c3b-163">Normalmente, o T-SQL para criar um procedimento armazenado nativamente compilado é semelhante ao seguinte modelo:</span><span class="sxs-lookup"><span data-stu-id="17c3b-163">Typically the T-SQL to create a natively compiled stored procedure is similar to the following template:</span></span>

```
CREATE PROCEDURE schemaname.procedurename
    @param1 type1, …
    WITH NATIVE_COMPILATION, SCHEMABINDING
    AS
        BEGIN ATOMIC WITH
            (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
            LANGUAGE = N'your_language__see_sys.languages'
            )
        …
        END;
```

* <span data-ttu-id="17c3b-164">Para TRANSACTION_ISOLATION_LEVEL, o SNAPSHOT é o valor mais comum para o procedimento armazenado nativamente compilado.</span><span class="sxs-lookup"><span data-stu-id="17c3b-164">For the TRANSACTION_ISOLATION_LEVEL, SNAPSHOT is the most common value for the natively compiled stored procedure.</span></span> <span data-ttu-id="17c3b-165">No entanto, também há suporte para um subconjunto dos outros valores:</span><span class="sxs-lookup"><span data-stu-id="17c3b-165">However,  a subset of the other values are also supported:</span></span>
  
  * <span data-ttu-id="17c3b-166">REPEATABLE READ</span><span class="sxs-lookup"><span data-stu-id="17c3b-166">REPEATABLE READ</span></span>
  * <span data-ttu-id="17c3b-167">SERIALIZABLE</span><span class="sxs-lookup"><span data-stu-id="17c3b-167">SERIALIZABLE</span></span>
* <span data-ttu-id="17c3b-168">O valor LANGUAGE deve estar presente na exibição sys.languages.</span><span class="sxs-lookup"><span data-stu-id="17c3b-168">The LANGUAGE value must be present in the sys.languages view.</span></span>

### <a name="how-to-migrate-a-stored-procedure"></a><span data-ttu-id="17c3b-169">Como migrar um procedimento armazenado</span><span class="sxs-lookup"><span data-stu-id="17c3b-169">How to migrate a stored procedure</span></span>
<span data-ttu-id="17c3b-170">As etapas de migração são:</span><span class="sxs-lookup"><span data-stu-id="17c3b-170">The migration steps are:</span></span>

1. <span data-ttu-id="17c3b-171">Obtenha o script CREATE PROCEDURE para o procedimento armazenado interpretado regular.</span><span class="sxs-lookup"><span data-stu-id="17c3b-171">Obtain the CREATE PROCEDURE script to the regular interpreted stored procedure.</span></span>
2. <span data-ttu-id="17c3b-172">Reescreva o cabeçalho para que ele corresponda ao modelo anterior.</span><span class="sxs-lookup"><span data-stu-id="17c3b-172">Rewrite its header to match the previous template.</span></span>
3. <span data-ttu-id="17c3b-173">Verificar se o código T-SQL de procedimento armazenado usa os recursos sem suporte para procedimentos armazenados compilados nativamente.</span><span class="sxs-lookup"><span data-stu-id="17c3b-173">Ascertain whether the stored procedure T-SQL code uses any features that are not supported for natively compiled stored procedures.</span></span> <span data-ttu-id="17c3b-174">Implemente soluções alternativas, se necessário.</span><span class="sxs-lookup"><span data-stu-id="17c3b-174">Implement workarounds if necessary.</span></span>
   
   * <span data-ttu-id="17c3b-175">Para obter detalhes, consulte [Problemas de migração para procedimentos armazenados compilados nativamente](http://msdn.microsoft.com/library/dn296678.aspx).</span><span class="sxs-lookup"><span data-stu-id="17c3b-175">For details see [Migration Issues for Natively Compiled Stored Procedures](http://msdn.microsoft.com/library/dn296678.aspx).</span></span>
4. <span data-ttu-id="17c3b-176">Renomeie o antigo procedimento armazenado usando SP_RENAME.</span><span class="sxs-lookup"><span data-stu-id="17c3b-176">Rename the old stored procedure by using SP_RENAME.</span></span> <span data-ttu-id="17c3b-177">Ou simplesmente descarte-o usando DROP.</span><span class="sxs-lookup"><span data-stu-id="17c3b-177">Or simply DROP it.</span></span>
5. <span data-ttu-id="17c3b-178">Execute o script T-SQL CREATE PROCEDURE editado.</span><span class="sxs-lookup"><span data-stu-id="17c3b-178">Run your edited CREATE PROCEDURE T-SQL script.</span></span>

## <a name="step-6-run-your-workload-in-test"></a><span data-ttu-id="17c3b-179">Etapa 6: executar sua carga de trabalho no teste</span><span class="sxs-lookup"><span data-stu-id="17c3b-179">Step 6: Run your workload in test</span></span>
<span data-ttu-id="17c3b-180">Execute uma carga de trabalho em seu banco de dados de teste que seja semelhante à carga de trabalho executada em seu banco de dados de produção.</span><span class="sxs-lookup"><span data-stu-id="17c3b-180">Run a workload in your test database that is similar to the workload that runs in your production database.</span></span> <span data-ttu-id="17c3b-181">Isso deve revelar o ganho de desempenho obtido com o uso do recurso Na Memória para tabelas e procedimentos armazenados.</span><span class="sxs-lookup"><span data-stu-id="17c3b-181">This should reveal the performance gain achieved by your use of the In-Memory feature for tables and stored procedures.</span></span>

<span data-ttu-id="17c3b-182">Os principais atributos da carga de trabalho são:</span><span class="sxs-lookup"><span data-stu-id="17c3b-182">Major attributes of the workload are:</span></span>

* <span data-ttu-id="17c3b-183">Número de conexões simultâneas.</span><span class="sxs-lookup"><span data-stu-id="17c3b-183">Number of concurrent connections.</span></span>
* <span data-ttu-id="17c3b-184">Taxa de leitura/gravação.</span><span class="sxs-lookup"><span data-stu-id="17c3b-184">Read/write ratio.</span></span>

<span data-ttu-id="17c3b-185">Para ajustar e executar a carga de trabalho de teste, considere usar a ferramenta útil ostress.exe, ilustrada [aqui](sql-database-in-memory.md).</span><span class="sxs-lookup"><span data-stu-id="17c3b-185">To tailor and run the test workload, consider using the handy ostress.exe tool, which illustrated in [here](sql-database-in-memory.md).</span></span>

<span data-ttu-id="17c3b-186">Para minimizar a latência de rede, execute o teste na mesma região geográfica do Azure onde está o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="17c3b-186">To minimize network latency, run your test in the same Azure geographic region where the database exists.</span></span>

## <a name="step-7-post-implementation-monitoring"></a><span data-ttu-id="17c3b-187">Etapa 7: Monitoramento pós-implementação</span><span class="sxs-lookup"><span data-stu-id="17c3b-187">Step 7: Post-implementation monitoring</span></span>
<span data-ttu-id="17c3b-188">Considere monitorar os efeitos de desempenho de  suas implementações de Na Memória em produção:</span><span class="sxs-lookup"><span data-stu-id="17c3b-188">Consider monitoring the performance effects of your In-Memory implementations in production:</span></span>

* <span data-ttu-id="17c3b-189">[Monitorar o armazenamento na memória](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="17c3b-189">[Monitor In-Memory Storage](sql-database-in-memory-oltp-monitoring.md).</span></span>
* [<span data-ttu-id="17c3b-190">Monitoramento de Banco de Dados SQL usando exibições de gerenciamento dinâmico</span><span class="sxs-lookup"><span data-stu-id="17c3b-190">Monitoring Azure SQL Database using dynamic management views</span></span>](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a><span data-ttu-id="17c3b-191">Links relacionados</span><span class="sxs-lookup"><span data-stu-id="17c3b-191">Related links</span></span>
* [<span data-ttu-id="17c3b-192">OLTP Na Memória (Otimização Na Memória)</span><span class="sxs-lookup"><span data-stu-id="17c3b-192">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
* [<span data-ttu-id="17c3b-193">Introdução aos procedimentos armazenados compilados nativamente</span><span class="sxs-lookup"><span data-stu-id="17c3b-193">Introduction to Natively Compiled Stored Procedures</span></span>](http://msdn.microsoft.com/library/dn133184.aspx)
* [<span data-ttu-id="17c3b-194">Supervisor de Otimização de Memória</span><span class="sxs-lookup"><span data-stu-id="17c3b-194">Memory Optimization Advisor</span></span>](http://msdn.microsoft.com/library/dn284308.aspx)

