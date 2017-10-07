---
title: OLTP in-memory aaaIn melhora o desempenho do SQL txn | Microsoft Docs
description: "Desempenho transacional de tooimprove de adotar o OLTP na memória em um banco de dados existente do SQL."
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
ms.openlocfilehash: 1bed796069565eb6741953837cf0477c2ddd8519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-in-memory-oltp-tooimprove-your-application-performance-in-sql-database"></a><span data-ttu-id="75958-103">Use o OLTP na memória tooimprove o desempenho do seu aplicativo no banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="75958-103">Use In-Memory OLTP tooimprove your application performance in SQL Database</span></span>
<span data-ttu-id="75958-104">[OLTP na memória](sql-database-in-memory.md) pode ser usado tooimprove Olá desempenho de processamento de transações, ingestão de dados e cenários de dados transitórios, em [Premium](sql-database-service-tiers.md) bancos de dados SQL Azure sem aumentar Olá camada de preços.</span><span class="sxs-lookup"><span data-stu-id="75958-104">[In-Memory OLTP](sql-database-in-memory.md) can be used tooimprove hello performance of transaction processing, data ingestion, and transient data scenarios, in  [Premium](sql-database-service-tiers.md) Azure SQL Databases without increasing hello pricing tier.</span></span> 

> [!NOTE] 
> <span data-ttu-id="75958-105">Saiba como o [Quorum dobra a principal carga de trabalho do banco de dados, enquanto reduz a DTU em 70% com o Banco de Dados SQL](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span><span class="sxs-lookup"><span data-stu-id="75958-105">Learn how [Quorum doubles key database’s workload while lowering DTU by 70% with SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)</span></span>


<span data-ttu-id="75958-106">Siga essas etapas tooadopt OLTP na memória no banco de dados existente.</span><span class="sxs-lookup"><span data-stu-id="75958-106">Follow these steps tooadopt In-Memory OLTP in your existing database.</span></span>

## <a name="step-1-ensure-you-are-using-a-premium-database"></a><span data-ttu-id="75958-107">Etapa 1: Garantir que você está usando um banco de dados Premium</span><span class="sxs-lookup"><span data-stu-id="75958-107">Step 1: Ensure you are using a Premium database</span></span>
<span data-ttu-id="75958-108">Há suporte para o OLTP in-memory apenas em bancos de dados Premium.</span><span class="sxs-lookup"><span data-stu-id="75958-108">In-Memory OLTP is supported only in Premium databases.</span></span> <span data-ttu-id="75958-109">Na memória é suportada se Olá retornou resultado é 1 (não em 0):</span><span class="sxs-lookup"><span data-stu-id="75958-109">In-Memory is supported if hello returned result is 1 (not 0):</span></span>

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

<span data-ttu-id="75958-110">*XTP* significa *Processamento Extremo de Transações*</span><span class="sxs-lookup"><span data-stu-id="75958-110">*XTP* stands for *Extreme Transaction Processing*</span></span>



## <a name="step-2-identify-objects-toomigrate-tooin-memory-oltp"></a><span data-ttu-id="75958-111">Etapa 2: Identificar objetos tooIn toomigrate memória OLTP</span><span class="sxs-lookup"><span data-stu-id="75958-111">Step 2: Identify objects toomigrate tooIn-Memory OLTP</span></span>
<span data-ttu-id="75958-112">O SSMS inclui um relatório **Visão Geral da Análise do Desempenho da Transação** que pode ser executado em um banco de dados com uma carga de trabalho ativa.</span><span class="sxs-lookup"><span data-stu-id="75958-112">SSMS includes a **Transaction Performance Analysis Overview** report that you can run against a database with an active workload.</span></span> <span data-ttu-id="75958-113">relatório de saudação identifica tabelas e procedimentos armazenados que são candidatos à migração de OLTP in-memory tooIn.</span><span class="sxs-lookup"><span data-stu-id="75958-113">hello report identifies tables and stored procedures that are candidates for migration tooIn-Memory OLTP.</span></span>

<span data-ttu-id="75958-114">No SSMS, relatório de saudação toogenerate:</span><span class="sxs-lookup"><span data-stu-id="75958-114">In SSMS, toogenerate hello report:</span></span>

* <span data-ttu-id="75958-115">Em Olá **Pesquisador de objetos**, clique o nó do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="75958-115">In hello **Object Explorer**, right-click your database node.</span></span>
* <span data-ttu-id="75958-116">Clique em **Relatórios** > **Relatórios Padrão** > **Visão Geral da Análise de Desempenho da Transação**.</span><span class="sxs-lookup"><span data-stu-id="75958-116">Click **Reports** > **Standard Reports** > **Transaction Performance Analysis Overview**.</span></span>

<span data-ttu-id="75958-117">Para obter mais informações, consulte [determinando se uma tabela ou procedimento armazenado deve ser movido OLTP de memória tooIn](http://msdn.microsoft.com/library/dn205133.aspx).</span><span class="sxs-lookup"><span data-stu-id="75958-117">For more information, see [Determining if a Table or Stored Procedure Should Be Ported tooIn-Memory OLTP](http://msdn.microsoft.com/library/dn205133.aspx).</span></span>

## <a name="step-3-create-a-comparable-test-database"></a><span data-ttu-id="75958-118">Etapa 3: Criar um banco de dados de teste comparável</span><span class="sxs-lookup"><span data-stu-id="75958-118">Step 3: Create a comparable test database</span></span>
<span data-ttu-id="75958-119">Suponha que o relatório de saudação indica seu banco de dados tem uma tabela que pode se beneficiar do que está sendo convertido tooa tabela de otimização de memória.</span><span class="sxs-lookup"><span data-stu-id="75958-119">Suppose hello report indicates your database has a table that would benefit from being converted tooa memory-optimized table.</span></span> <span data-ttu-id="75958-120">É recomendável que você primeiro teste indicação de saudação tooconfirm testando.</span><span class="sxs-lookup"><span data-stu-id="75958-120">We recommend that you first test tooconfirm hello indication by testing.</span></span>

<span data-ttu-id="75958-121">Você precisa de uma cópia de teste do seu banco de dados de produção.</span><span class="sxs-lookup"><span data-stu-id="75958-121">You need a test copy of your production database.</span></span> <span data-ttu-id="75958-122">Olá banco de dados de teste deve ser no hello mesmo nível de serviço da camada do banco de dados de produção.</span><span class="sxs-lookup"><span data-stu-id="75958-122">hello test database should be at hello same service tier level as your production database.</span></span>

<span data-ttu-id="75958-123">tooease de teste, ajustar o banco de dados de teste da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="75958-123">tooease testing, tweak your test database as follows:</span></span>

1. <span data-ttu-id="75958-124">Conecte o banco de dados de teste toohello usando o SSMS.</span><span class="sxs-lookup"><span data-stu-id="75958-124">Connect toohello test database by using SSMS.</span></span>
2. <span data-ttu-id="75958-125">tooavoid necessidade Olá a opção WITH (SNAPSHOT) em consultas, defina a opção de banco de dados de saudação conforme Olá instrução T-SQL a seguir:</span><span class="sxs-lookup"><span data-stu-id="75958-125">tooavoid needing hello WITH (SNAPSHOT) option in queries, set hello database option as shown in hello following T-SQL statement:</span></span>
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a><span data-ttu-id="75958-126">Etapa 4: migrar tabelas</span><span class="sxs-lookup"><span data-stu-id="75958-126">Step 4: Migrate tables</span></span>
<span data-ttu-id="75958-127">Você deve criar e preencher uma cópia com otimização de memória da tabela Olá deseja tootest.</span><span class="sxs-lookup"><span data-stu-id="75958-127">You must create and populate a memory-optimized copy of hello table you want tootest.</span></span> <span data-ttu-id="75958-128">Você pode criá-la usando:</span><span class="sxs-lookup"><span data-stu-id="75958-128">You can create it by using either:</span></span>

* <span data-ttu-id="75958-129">Olá útil Assistente de otimização de memória no SSMS.</span><span class="sxs-lookup"><span data-stu-id="75958-129">hello handy Memory Optimization Wizard in SSMS.</span></span>
* <span data-ttu-id="75958-130">T-SQL Manual.</span><span class="sxs-lookup"><span data-stu-id="75958-130">Manual T-SQL.</span></span>

#### <a name="memory-optimization-wizard-in-ssms"></a><span data-ttu-id="75958-131">Assistente de Otimização de Memória no SSMS</span><span class="sxs-lookup"><span data-stu-id="75958-131">Memory Optimization Wizard in SSMS</span></span>
<span data-ttu-id="75958-132">toouse essa opção de migração:</span><span class="sxs-lookup"><span data-stu-id="75958-132">toouse this migration option:</span></span>

1. <span data-ttu-id="75958-133">Conecte o banco de dados de teste de toohello com o SSMS.</span><span class="sxs-lookup"><span data-stu-id="75958-133">Connect toohello test database with SSMS.</span></span>
2. <span data-ttu-id="75958-134">Em Olá **Pesquisador de objetos**, com o botão direito na tabela hello e, em seguida, clique em **orientador de otimização de memória**.</span><span class="sxs-lookup"><span data-stu-id="75958-134">In hello **Object Explorer**, right-click on hello table, and then click **Memory Optimization Advisor**.</span></span>
   
   * <span data-ttu-id="75958-135">Olá **orientador otimizador memória da tabela** assistente é exibido.</span><span class="sxs-lookup"><span data-stu-id="75958-135">hello **Table Memory Optimizer Advisor** wizard is displayed.</span></span>
3. <span data-ttu-id="75958-136">No Assistente de saudação, clique em **validação de migração** (ou hello **próximo** botão) toosee se Olá tabela possui recursos sem suporte que não têm suporte em tabelas com otimização de memória.</span><span class="sxs-lookup"><span data-stu-id="75958-136">In hello wizard, click **Migration validation** (or hello **Next** button) toosee if hello table has any unsupported features that are unsupported in memory-optimized tables.</span></span> <span data-ttu-id="75958-137">Para obter mais informações, consulte:</span><span class="sxs-lookup"><span data-stu-id="75958-137">For more information, see:</span></span>
   
   * <span data-ttu-id="75958-138">Olá *lista de verificação de otimização de memória* na [orientador de otimização de memória](http://msdn.microsoft.com/library/dn284308.aspx).</span><span class="sxs-lookup"><span data-stu-id="75958-138">hello *memory optimization checklist* in [Memory Optimization Advisor](http://msdn.microsoft.com/library/dn284308.aspx).</span></span>
   * <span data-ttu-id="75958-139">[Construções Transact-SQL sem suporte do OLTP Na Memória](http://msdn.microsoft.com/library/dn246937.aspx).</span><span class="sxs-lookup"><span data-stu-id="75958-139">[Transact-SQL Constructs Not Supported by In-Memory OLTP](http://msdn.microsoft.com/library/dn246937.aspx).</span></span>
   * <span data-ttu-id="75958-140">[Migrando OLTP de memória tooIn](http://msdn.microsoft.com/library/dn247639.aspx).</span><span class="sxs-lookup"><span data-stu-id="75958-140">[Migrating tooIn-Memory OLTP](http://msdn.microsoft.com/library/dn247639.aspx).</span></span>
4. <span data-ttu-id="75958-141">Se a tabela de saudação tem recursos sem suporte, advisor Olá pode executar o esquema real hello e migração de dados para você.</span><span class="sxs-lookup"><span data-stu-id="75958-141">If hello table has no unsupported features, hello advisor can perform hello actual schema and data migration for you.</span></span>

#### <a name="manual-t-sql"></a><span data-ttu-id="75958-142">T-SQL Manual</span><span class="sxs-lookup"><span data-stu-id="75958-142">Manual T-SQL</span></span>
<span data-ttu-id="75958-143">toouse essa opção de migração:</span><span class="sxs-lookup"><span data-stu-id="75958-143">toouse this migration option:</span></span>

1. <span data-ttu-id="75958-144">Conecte o banco de dados de teste tooyour usando o SSMS (ou um utilitário semelhante).</span><span class="sxs-lookup"><span data-stu-id="75958-144">Connect tooyour test database by using SSMS (or a similar utility).</span></span>
2. <span data-ttu-id="75958-145">Obter script de T-SQL completo Olá para sua tabela e seus índices.</span><span class="sxs-lookup"><span data-stu-id="75958-145">Obtain hello complete T-SQL script for your table and its indexes.</span></span>
   
   * <span data-ttu-id="75958-146">No SSMS, clique com o botão direito do mouse no nó da sua tabela.</span><span class="sxs-lookup"><span data-stu-id="75958-146">In SSMS, right-click your table node.</span></span>
   * <span data-ttu-id="75958-147">Clique em **Script de Tabela como** > **CRIAR Para** > **Nova Janela de Consulta**.</span><span class="sxs-lookup"><span data-stu-id="75958-147">Click **Script Table As** > **CREATE To** > **New Query Window**.</span></span>
3. <span data-ttu-id="75958-148">Na janela de script hello, adicione WITH (MEMORY_OPTIMIZED = ON) toohello instrução CREATE TABLE.</span><span class="sxs-lookup"><span data-stu-id="75958-148">In hello script window, add WITH (MEMORY_OPTIMIZED = ON) toohello CREATE TABLE statement.</span></span>
4. <span data-ttu-id="75958-149">Se houver um índice CLUSTERIZADO, altere tooNONCLUSTERED.</span><span class="sxs-lookup"><span data-stu-id="75958-149">If there is a CLUSTERED index, change it tooNONCLUSTERED.</span></span>
5. <span data-ttu-id="75958-150">Renomear tabela existente hello usando SP_RENAME.</span><span class="sxs-lookup"><span data-stu-id="75958-150">Rename hello existing table by using SP_RENAME.</span></span>
6. <span data-ttu-id="75958-151">Crie cópia Olá com otimização de memória nova da tabela Olá executando o script CREATE TABLE editado.</span><span class="sxs-lookup"><span data-stu-id="75958-151">Create hello new memory-optimized copy of hello table by running your edited CREATE TABLE script.</span></span>
7. <span data-ttu-id="75958-152">Copie a tabela Olá dados tooyour otimização de memória usando INSERT... SELECIONE * EM:</span><span class="sxs-lookup"><span data-stu-id="75958-152">Copy hello data tooyour memory-optimized table by using INSERT...SELECT * INTO:</span></span>

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a><span data-ttu-id="75958-153">Etapa 5 (opcional): migrar procedimentos armazenados</span><span class="sxs-lookup"><span data-stu-id="75958-153">Step 5 (optional): Migrate stored procedures</span></span>
<span data-ttu-id="75958-154">recurso do Hello na memória também pode modificar um procedimento armazenado para melhorar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="75958-154">hello In-Memory feature can also modify a stored procedure for improved performance.</span></span>

### <a name="considerations-with-natively-compiled-stored-procedures"></a><span data-ttu-id="75958-155">Considerações sobre procedimentos armazenados compilados nativamente</span><span class="sxs-lookup"><span data-stu-id="75958-155">Considerations with natively compiled stored procedures</span></span>
<span data-ttu-id="75958-156">Um procedimento armazenado compilado nativamente deve ter uma saudação em sua cláusula T-SQL com as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="75958-156">A natively compiled stored procedure must have hello following options on its T-SQL WITH clause:</span></span>

* <span data-ttu-id="75958-157">NATIVE_COMPILATION</span><span class="sxs-lookup"><span data-stu-id="75958-157">NATIVE_COMPILATION</span></span>
* <span data-ttu-id="75958-158">SCHEMABINDING: tabelas significado Olá procedimento armazenado não podem ter suas definições de coluna alteradas de qualquer maneira que possa afetar o procedimento armazenado de saudação, a menos que você remover o procedimento armazenado de saudação.</span><span class="sxs-lookup"><span data-stu-id="75958-158">SCHEMABINDING: meaning tables that hello stored procedure cannot have their column definitions changed in any way that would affect hello stored procedure, unless you drop hello stored procedure.</span></span>

<span data-ttu-id="75958-159">Um módulo nativo deve usar grandes [blocos ATOMIC](http://msdn.microsoft.com/library/dn452281.aspx) para o gerenciamento de transações.</span><span class="sxs-lookup"><span data-stu-id="75958-159">A native module must use one big [ATOMIC blocks](http://msdn.microsoft.com/library/dn452281.aspx) for transaction management.</span></span> <span data-ttu-id="75958-160">Não há uma função para BEGIN TRANSACTION explícita ou para ROLLBACK TRANSACTION.</span><span class="sxs-lookup"><span data-stu-id="75958-160">There is no role for an explicit BEGIN TRANSACTION, or for ROLLBACK TRANSACTION.</span></span> <span data-ttu-id="75958-161">Se o seu código detectar uma violação de uma regra de negócio, ele pode ser encerrado bloco atômico de saudação com um [gerar](http://msdn.microsoft.com/library/ee677615.aspx) instrução.</span><span class="sxs-lookup"><span data-stu-id="75958-161">If your code detects a violation of a business rule, it can terminate hello atomic block with a [THROW](http://msdn.microsoft.com/library/ee677615.aspx) statement.</span></span>

### <a name="typical-create-procedure-for-natively-compiled"></a><span data-ttu-id="75958-162">CREATE PROCEDURE típico para compilados nativamente</span><span class="sxs-lookup"><span data-stu-id="75958-162">Typical CREATE PROCEDURE for natively compiled</span></span>
<span data-ttu-id="75958-163">Normalmente, Olá T-SQL toocreate um procedimento armazenado nativamente compilado é semelhante toohello modelo a seguir:</span><span class="sxs-lookup"><span data-stu-id="75958-163">Typically hello T-SQL toocreate a natively compiled stored procedure is similar toohello following template:</span></span>

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

* <span data-ttu-id="75958-164">Para Olá TRANSACTION_ISOLATION_LEVEL, o instantâneo é procedimento mais comum de valor para Olá compilado nativamente armazenado hello.</span><span class="sxs-lookup"><span data-stu-id="75958-164">For hello TRANSACTION_ISOLATION_LEVEL, SNAPSHOT is hello most common value for hello natively compiled stored procedure.</span></span> <span data-ttu-id="75958-165">No entanto, um subconjunto de Olá outros valores também são suportados:</span><span class="sxs-lookup"><span data-stu-id="75958-165">However,  a subset of hello other values are also supported:</span></span>
  
  * <span data-ttu-id="75958-166">REPEATABLE READ</span><span class="sxs-lookup"><span data-stu-id="75958-166">REPEATABLE READ</span></span>
  * <span data-ttu-id="75958-167">SERIALIZABLE</span><span class="sxs-lookup"><span data-stu-id="75958-167">SERIALIZABLE</span></span>
* <span data-ttu-id="75958-168">Olá valor de idioma deve estar presente no modo de exibição de sys.languages hello.</span><span class="sxs-lookup"><span data-stu-id="75958-168">hello LANGUAGE value must be present in hello sys.languages view.</span></span>

### <a name="how-toomigrate-a-stored-procedure"></a><span data-ttu-id="75958-169">Como toomigrate um procedimento armazenado</span><span class="sxs-lookup"><span data-stu-id="75958-169">How toomigrate a stored procedure</span></span>
<span data-ttu-id="75958-170">etapas de migração de saudação são:</span><span class="sxs-lookup"><span data-stu-id="75958-170">hello migration steps are:</span></span>

1. <span data-ttu-id="75958-171">Obter Olá CREATE PROCEDURE script toohello regular procedimento armazenado interpretado.</span><span class="sxs-lookup"><span data-stu-id="75958-171">Obtain hello CREATE PROCEDURE script toohello regular interpreted stored procedure.</span></span>
2. <span data-ttu-id="75958-172">Reescreva o modelo do cabeçalho toomatch Olá anterior.</span><span class="sxs-lookup"><span data-stu-id="75958-172">Rewrite its header toomatch hello previous template.</span></span>
3. <span data-ttu-id="75958-173">Verificar se o procedimento armazenado de saudação código T-SQL usa todos os recursos que não há suporte para procedimentos armazenados compilados nativamente.</span><span class="sxs-lookup"><span data-stu-id="75958-173">Ascertain whether hello stored procedure T-SQL code uses any features that are not supported for natively compiled stored procedures.</span></span> <span data-ttu-id="75958-174">Implemente soluções alternativas, se necessário.</span><span class="sxs-lookup"><span data-stu-id="75958-174">Implement workarounds if necessary.</span></span>
   
   * <span data-ttu-id="75958-175">Para obter detalhes, consulte [Problemas de migração para procedimentos armazenados compilados nativamente](http://msdn.microsoft.com/library/dn296678.aspx).</span><span class="sxs-lookup"><span data-stu-id="75958-175">For details see [Migration Issues for Natively Compiled Stored Procedures](http://msdn.microsoft.com/library/dn296678.aspx).</span></span>
4. <span data-ttu-id="75958-176">Renomear o procedimento armazenado do antigo hello usando SP_RENAME.</span><span class="sxs-lookup"><span data-stu-id="75958-176">Rename hello old stored procedure by using SP_RENAME.</span></span> <span data-ttu-id="75958-177">Ou simplesmente descarte-o usando DROP.</span><span class="sxs-lookup"><span data-stu-id="75958-177">Or simply DROP it.</span></span>
5. <span data-ttu-id="75958-178">Execute o script T-SQL CREATE PROCEDURE editado.</span><span class="sxs-lookup"><span data-stu-id="75958-178">Run your edited CREATE PROCEDURE T-SQL script.</span></span>

## <a name="step-6-run-your-workload-in-test"></a><span data-ttu-id="75958-179">Etapa 6: executar sua carga de trabalho no teste</span><span class="sxs-lookup"><span data-stu-id="75958-179">Step 6: Run your workload in test</span></span>
<span data-ttu-id="75958-180">Execute uma carga de trabalho em seu banco de dados de teste é semelhante toohello carga de trabalho é executado em seu banco de dados de produção.</span><span class="sxs-lookup"><span data-stu-id="75958-180">Run a workload in your test database that is similar toohello workload that runs in your production database.</span></span> <span data-ttu-id="75958-181">Isso deve revelar o ganho de desempenho Olá obtido com o uso do recurso de na memória de saudação para tabelas e procedimentos armazenados.</span><span class="sxs-lookup"><span data-stu-id="75958-181">This should reveal hello performance gain achieved by your use of hello In-Memory feature for tables and stored procedures.</span></span>

<span data-ttu-id="75958-182">Os atributos principais de carga de trabalho de saudação são:</span><span class="sxs-lookup"><span data-stu-id="75958-182">Major attributes of hello workload are:</span></span>

* <span data-ttu-id="75958-183">Número de conexões simultâneas.</span><span class="sxs-lookup"><span data-stu-id="75958-183">Number of concurrent connections.</span></span>
* <span data-ttu-id="75958-184">Taxa de leitura/gravação.</span><span class="sxs-lookup"><span data-stu-id="75958-184">Read/write ratio.</span></span>

<span data-ttu-id="75958-185">tootailor e carga de trabalho de teste de execução hello, considere o uso de ferramenta de ostress.exe útil hello, que ilustrado na [aqui](sql-database-in-memory.md).</span><span class="sxs-lookup"><span data-stu-id="75958-185">tootailor and run hello test workload, consider using hello handy ostress.exe tool, which illustrated in [here](sql-database-in-memory.md).</span></span>

<span data-ttu-id="75958-186">latência de rede toominimize, executar o teste em Olá mesma região geográfica do Azure onde o banco de dados de saudação existe.</span><span class="sxs-lookup"><span data-stu-id="75958-186">toominimize network latency, run your test in hello same Azure geographic region where hello database exists.</span></span>

## <a name="step-7-post-implementation-monitoring"></a><span data-ttu-id="75958-187">Etapa 7: Monitoramento pós-implementação</span><span class="sxs-lookup"><span data-stu-id="75958-187">Step 7: Post-implementation monitoring</span></span>
<span data-ttu-id="75958-188">Considere a possibilidade de monitorar os efeitos do desempenho de saudação de suas implementações de memória em produção:</span><span class="sxs-lookup"><span data-stu-id="75958-188">Consider monitoring hello performance effects of your In-Memory implementations in production:</span></span>

* <span data-ttu-id="75958-189">[Monitorar o armazenamento na memória](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="75958-189">[Monitor In-Memory Storage](sql-database-in-memory-oltp-monitoring.md).</span></span>
* [<span data-ttu-id="75958-190">Monitoramento de Banco de Dados SQL usando exibições de gerenciamento dinâmico</span><span class="sxs-lookup"><span data-stu-id="75958-190">Monitoring Azure SQL Database using dynamic management views</span></span>](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a><span data-ttu-id="75958-191">Links relacionados</span><span class="sxs-lookup"><span data-stu-id="75958-191">Related links</span></span>
* [<span data-ttu-id="75958-192">OLTP Na Memória (Otimização Na Memória)</span><span class="sxs-lookup"><span data-stu-id="75958-192">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
* [<span data-ttu-id="75958-193">Introdução tooNatively Compiled Stored Procedures</span><span class="sxs-lookup"><span data-stu-id="75958-193">Introduction tooNatively Compiled Stored Procedures</span></span>](http://msdn.microsoft.com/library/dn133184.aspx)
* [<span data-ttu-id="75958-194">Supervisor de Otimização de Memória</span><span class="sxs-lookup"><span data-stu-id="75958-194">Memory Optimization Advisor</span></span>](http://msdn.microsoft.com/library/dn284308.aspx)

