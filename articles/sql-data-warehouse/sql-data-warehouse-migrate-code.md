---
title: "Migrar seu código SQL para o SQL Data Warehouse | Microsoft Docs"
description: "Dicas para migrar seu código SQL para o SQL Data Warehouse do Azure para desenvolvimento de soluções."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 19c252a3-0e41-4eec-9d3e-09a68c7e7add
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/23/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: c6e6b890f5e2d0e31b10bbb6803adad02bf60248
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-sql-code-to-sql-data-warehouse"></a><span data-ttu-id="24d56-103">Migrar seu código SQL para o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="24d56-103">Migrate your SQL code to SQL Data Warehouse</span></span>
<span data-ttu-id="24d56-104">Este artigo explica as alterações de código que você provavelmente terá que fazer ao migrar seu código de outro banco de dados para o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="24d56-104">This article explains code changes you will probably need to make when migrating your code from another database to SQL Data Warehouse.</span></span> <span data-ttu-id="24d56-105">Alguns recursos do SQL Data Warehouse podem melhorar consideravelmente o desempenho, pois foram criados para funcionar diretamente de uma maneira distribuída.</span><span class="sxs-lookup"><span data-stu-id="24d56-105">Some SQL Data Warehouse features can significantly improve performance as they are designed to work in a distributed fashion.</span></span> <span data-ttu-id="24d56-106">No entanto, para manter o desempenho e a escala, alguns recursos também não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="24d56-106">However, to maintain performance and scale, some features are also not available.</span></span>

## <a name="common-t-sql-limitations"></a><span data-ttu-id="24d56-107">Limitações comuns do T-SQL</span><span class="sxs-lookup"><span data-stu-id="24d56-107">Common T-SQL Limitations</span></span>
<span data-ttu-id="24d56-108">A lista a seguir resume os recursos mais comuns aos quais o SQL Data Warehouse não oferece suporte.</span><span class="sxs-lookup"><span data-stu-id="24d56-108">The following list summarizes the most common features that SQL Data Warehouse does not support.</span></span> <span data-ttu-id="24d56-109">Os links levam a soluções alternativas para os recursos sem suporte:</span><span class="sxs-lookup"><span data-stu-id="24d56-109">The links take you to workarounds for the unsupported features:</span></span>

* <span data-ttu-id="24d56-110">[Junções ANSI em atualizações][ANSI joins on updates]</span><span class="sxs-lookup"><span data-stu-id="24d56-110">[ANSI joins on updates][ANSI joins on updates]</span></span>
* <span data-ttu-id="24d56-111">[Junções ANSI em exclusões][ANSI joins on deletes]</span><span class="sxs-lookup"><span data-stu-id="24d56-111">[ANSI joins on deletes][ANSI joins on deletes]</span></span>
* <span data-ttu-id="24d56-112">[instrução merge][merge statement]</span><span class="sxs-lookup"><span data-stu-id="24d56-112">[merge statement][merge statement]</span></span>
* <span data-ttu-id="24d56-113">junções entre bancos de dados</span><span class="sxs-lookup"><span data-stu-id="24d56-113">cross-database joins</span></span>
* <span data-ttu-id="24d56-114">[cursores][cursors]</span><span class="sxs-lookup"><span data-stu-id="24d56-114">[cursors][cursors]</span></span>
* <span data-ttu-id="24d56-115"><seg>
  [INSERT..EXEC][INSERT..EXEC]</seg></span><span class="sxs-lookup"><span data-stu-id="24d56-115">[INSERT..EXEC][INSERT..EXEC]</span></span>
* <span data-ttu-id="24d56-116">cláusula output</span><span class="sxs-lookup"><span data-stu-id="24d56-116">output clause</span></span>
* <span data-ttu-id="24d56-117">funções definidas pelo usuário embutidas</span><span class="sxs-lookup"><span data-stu-id="24d56-117">inline user-defined functions</span></span>
* <span data-ttu-id="24d56-118">funções com várias instruções</span><span class="sxs-lookup"><span data-stu-id="24d56-118">multi-statement functions</span></span>
* [<span data-ttu-id="24d56-119">expressões de tabela comuns</span><span class="sxs-lookup"><span data-stu-id="24d56-119">common table expressions</span></span>](#Common-table-expressions)
* <span data-ttu-id="24d56-120">[CTE (expressão de tabela comum) recursiva] (#Recursive-common-table-expressions-(CTE)</span><span class="sxs-lookup"><span data-stu-id="24d56-120">[recursive common table expressions (CTE)](#Recursive-common-table-expressions-(CTE)</span></span>
* <span data-ttu-id="24d56-121">procedimentos e funções CLR</span><span class="sxs-lookup"><span data-stu-id="24d56-121">CLR functions and procedures</span></span>
* <span data-ttu-id="24d56-122">função $partition</span><span class="sxs-lookup"><span data-stu-id="24d56-122">$partition function</span></span>
* <span data-ttu-id="24d56-123">variáveis de tabela</span><span class="sxs-lookup"><span data-stu-id="24d56-123">table variables</span></span>
* <span data-ttu-id="24d56-124">parâmetros de valor de tabela</span><span class="sxs-lookup"><span data-stu-id="24d56-124">table value parameters</span></span>
* <span data-ttu-id="24d56-125">transações distribuídas</span><span class="sxs-lookup"><span data-stu-id="24d56-125">distributed transactions</span></span>
* <span data-ttu-id="24d56-126">confirmar/reverter trabalho</span><span class="sxs-lookup"><span data-stu-id="24d56-126">commit / rollback work</span></span>
* <span data-ttu-id="24d56-127">salvar transação</span><span class="sxs-lookup"><span data-stu-id="24d56-127">save transaction</span></span>
* <span data-ttu-id="24d56-128">contextos de execução (EXECUTE AS)</span><span class="sxs-lookup"><span data-stu-id="24d56-128">execution contexts (EXECUTE AS)</span></span>
* <span data-ttu-id="24d56-129">[cláusula group by com as opções rollup/cube/grouping sets][group by clause with rollup / cube / grouping sets options]</span><span class="sxs-lookup"><span data-stu-id="24d56-129">[group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options]</span></span>
* <span data-ttu-id="24d56-130">[níveis de aninhamento superiores a 8][nesting levels beyond 8]</span><span class="sxs-lookup"><span data-stu-id="24d56-130">[nesting levels beyond 8][nesting levels beyond 8]</span></span>
* <span data-ttu-id="24d56-131">[atualizando por meio de exibições][updating through views]</span><span class="sxs-lookup"><span data-stu-id="24d56-131">[updating through views][updating through views]</span></span>
* <span data-ttu-id="24d56-132">[uso de select para atribuição de variável][use of select for variable assignment]</span><span class="sxs-lookup"><span data-stu-id="24d56-132">[use of select for variable assignment][use of select for variable assignment]</span></span>
* <span data-ttu-id="24d56-133">[nenhum tipo de dados MAX para cadeias de caracteres SQL dinâmicas][no MAX data type for dynamic SQL strings]</span><span class="sxs-lookup"><span data-stu-id="24d56-133">[no MAX data type for dynamic SQL strings][no MAX data type for dynamic SQL strings]</span></span>

<span data-ttu-id="24d56-134">Felizmente, a maioria dessas limitações pode ser solucionada.</span><span class="sxs-lookup"><span data-stu-id="24d56-134">Fortunately most of these limitations can be worked around.</span></span> <span data-ttu-id="24d56-135">Foram fornecidas explicações nos artigos de desenvolvimento relevantes mencionados acima.</span><span class="sxs-lookup"><span data-stu-id="24d56-135">Explanations are provided in the relevant development articles referenced above.</span></span>

## <a name="supported-cte-features"></a><span data-ttu-id="24d56-136">Recursos do CTE com suporte</span><span class="sxs-lookup"><span data-stu-id="24d56-136">Supported CTE features</span></span>
<span data-ttu-id="24d56-137">Tabela CTEs (expressões comuns) têm suporte parcial no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="24d56-137">Common table expressions (CTEs) are partially supported in SQL Data Warehouse.</span></span>  <span data-ttu-id="24d56-138">Atualmente, há suporte aos seguintes recursos de CTE:</span><span class="sxs-lookup"><span data-stu-id="24d56-138">The following CTE features are currently supported:</span></span>

* <span data-ttu-id="24d56-139">Uma CTE pode ser especificada em uma instrução SELECT.</span><span class="sxs-lookup"><span data-stu-id="24d56-139">A CTE can be specified in a SELECT statement.</span></span>
* <span data-ttu-id="24d56-140">Uma CTE pode ser especificada em uma instrução CREATE VIEW.</span><span class="sxs-lookup"><span data-stu-id="24d56-140">A CTE can be specified in a CREATE VIEW statement.</span></span>
* <span data-ttu-id="24d56-141">Uma CTE pode ser especificada em uma instrução CTAS (CREATE TABLE AS SELECT).</span><span class="sxs-lookup"><span data-stu-id="24d56-141">A CTE can be specified in a CREATE TABLE AS SELECT (CTAS) statement.</span></span>
* <span data-ttu-id="24d56-142">Uma CTE pode ser especificada em uma instrução CRTAS (CREATE REMOTE TABLE AS SELECT).</span><span class="sxs-lookup"><span data-stu-id="24d56-142">A CTE can be specified in a CREATE REMOTE TABLE AS SELECT (CRTAS) statement.</span></span>
* <span data-ttu-id="24d56-143">Uma CTE pode ser especificada em uma instrução CETAS (CREATE EXTERNAL TABLE AS SELECT).</span><span class="sxs-lookup"><span data-stu-id="24d56-143">A CTE can be specified in a CREATE EXTERNAL TABLE AS SELECT (CETAS) statement.</span></span>
* <span data-ttu-id="24d56-144">Uma tabela remota pode ser referenciada de uma CTE.</span><span class="sxs-lookup"><span data-stu-id="24d56-144">A remote table can be referenced from a CTE.</span></span>
* <span data-ttu-id="24d56-145">Uma tabela externa pode ser referenciada de uma CTE.</span><span class="sxs-lookup"><span data-stu-id="24d56-145">An external table can be referenced from a CTE.</span></span>
* <span data-ttu-id="24d56-146">Várias definições de consulta CTE podem ser definidas em uma CTE.</span><span class="sxs-lookup"><span data-stu-id="24d56-146">Multiple CTE query definitions can be defined in a CTE.</span></span>

## <a name="cte-limitations"></a><span data-ttu-id="24d56-147">Limitações da CTE</span><span class="sxs-lookup"><span data-stu-id="24d56-147">CTE Limitations</span></span>
<span data-ttu-id="24d56-148">As expressões de tabela comum têm algumas limitações no SQL Data Warehouse, incluindo:</span><span class="sxs-lookup"><span data-stu-id="24d56-148">Common table expressions have some limitations in SQL Data Warehouse including:</span></span>

* <span data-ttu-id="24d56-149">Uma CTE deve ser seguida por uma única instrução SELECT.</span><span class="sxs-lookup"><span data-stu-id="24d56-149">A CTE must be followed by a single SELECT statement.</span></span> <span data-ttu-id="24d56-150">As instruções INSERT, UPDATE, DELETE e MERGE não têm suporte.</span><span class="sxs-lookup"><span data-stu-id="24d56-150">INSERT, UPDATE, DELETE, and MERGE statements are not supported.</span></span>
* <span data-ttu-id="24d56-151">Não há suporte para a expressão de tabela comum que inclui referências a ela mesma (expressão de tabela comum recursiva) (veja a seção abaixo).</span><span class="sxs-lookup"><span data-stu-id="24d56-151">A common table expression that includes references to itself (a recursive common table expression) is not supported (see below section).</span></span>
* <span data-ttu-id="24d56-152">Não é permitido especificar mais de uma cláusula WITH em uma CTE.</span><span class="sxs-lookup"><span data-stu-id="24d56-152">Specifying more than one WITH clause in a CTE is not allowed.</span></span> <span data-ttu-id="24d56-153">Por exemplo, se CTE_query_definition contiver uma subconsulta, essa subconsulta não poderá conter uma cláusula WITH aninhada que defina outra CTE.</span><span class="sxs-lookup"><span data-stu-id="24d56-153">For example, if a CTE_query_definition contains a subquery, that subquery cannot contain a nested WITH clause that defines another CTE.</span></span>
* <span data-ttu-id="24d56-154">Uma cláusula ORDER BY não pode ser usada em CTE_query_definition, exceto quando existe uma cláusula TOP especificada.</span><span class="sxs-lookup"><span data-stu-id="24d56-154">An ORDER BY clause cannot be used in the CTE_query_definition, except when a TOP clause is specified.</span></span>
* <span data-ttu-id="24d56-155">Quando uma CTE é usada em uma instrução que faz parte de um lote, a instrução anterior deve ser seguida por um ponto-e-vírgula.</span><span class="sxs-lookup"><span data-stu-id="24d56-155">When a CTE is used in a statement that is part of a batch, the statement before it must be followed by a semicolon.</span></span>
* <span data-ttu-id="24d56-156">Quando usado em instruções preparadas por sp_prepare, as CTEs se comportarão da mesma forma que outras instruções SELECT em PDW.</span><span class="sxs-lookup"><span data-stu-id="24d56-156">When used in statements prepared by sp_prepare, CTEs will behave the same way as other SELECT statements in PDW.</span></span> <span data-ttu-id="24d56-157">No entanto, se as CTEs forem usadas como parte das CETAS preparadas por sp_prepare, o comportamento poderá ser diferente do SQL Server e de outras instruções de PDW, devido ao modo como a associação é implementada por sp_prepare.</span><span class="sxs-lookup"><span data-stu-id="24d56-157">However, if CTEs are used as part of CETAS prepared by sp_prepare, the behavior can defer from SQL Server and other PDW statements because of the way binding is implemented for sp_prepare.</span></span> <span data-ttu-id="24d56-158">Se a instrução SELECT que faz referência à CTE estiver usando uma coluna incorreta que não existe na CTE, o sp_prepare passará sem detectar o erro, mas o erro será gerado durante sp_execute.</span><span class="sxs-lookup"><span data-stu-id="24d56-158">If SELECT that references CTE is using a wrong column that does not exist in CTE, the sp_prepare will pass without detecting the error, but the error will be thrown during sp_execute instead.</span></span>

## <a name="recursive-ctes"></a><span data-ttu-id="24d56-159">CTEs recursivas</span><span class="sxs-lookup"><span data-stu-id="24d56-159">Recursive CTEs</span></span>
<span data-ttu-id="24d56-160">As CTEs recursivas não têm suporte no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="24d56-160">Recursive CTEs are not supported in SQL Data Warehouse.</span></span>  <span data-ttu-id="24d56-161">A migração de CTEs recursivas pode ser um pouco complexa e o melhor processo é dividi-la em várias etapas.</span><span class="sxs-lookup"><span data-stu-id="24d56-161">The migration of recursive CTE can be somewhat complex and the best process is to break it into multiple steps.</span></span> <span data-ttu-id="24d56-162">Normalmente, você pode usar um loop e preencher uma tabela temporária à medida que você itera sobre as consultas recursivas provisórias.</span><span class="sxs-lookup"><span data-stu-id="24d56-162">You can typically use a loop and populate a temporary table as you iterate over the recursive interim queries.</span></span> <span data-ttu-id="24d56-163">Depois que a tabela temporária for preenchida, você pode retornar os dados como um único conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="24d56-163">Once the temporary table is populated you can then return the data as a single result set.</span></span> <span data-ttu-id="24d56-164">Uma abordagem semelhante foi usada para resolver o `GROUP BY WITH CUBE` no artigo [Agrupar por cláusula com opções de conjuntos de rollup/cubo/agrupamento][group by clause with rollup / cube / grouping sets options].</span><span class="sxs-lookup"><span data-stu-id="24d56-164">A similar approach has been used to solve `GROUP BY WITH CUBE` in the [group by clause with rollup / cube / grouping sets options][group by clause with rollup / cube / grouping sets options] article.</span></span>

## <a name="unsupported-system-functions"></a><span data-ttu-id="24d56-165">Funções do sistema sem suporte</span><span class="sxs-lookup"><span data-stu-id="24d56-165">Unsupported system functions</span></span>
<span data-ttu-id="24d56-166">Também há algumas funções do sistema que não têm suporte.</span><span class="sxs-lookup"><span data-stu-id="24d56-166">There are also some system functions that are not supported.</span></span> <span data-ttu-id="24d56-167">Estas são algumas das principais e que normalmente são usadas em data warehouse:</span><span class="sxs-lookup"><span data-stu-id="24d56-167">Some of the main ones you might typically find used in data warehousing are:</span></span>

* <span data-ttu-id="24d56-168">NEWSEQUENTIALID()</span><span class="sxs-lookup"><span data-stu-id="24d56-168">NEWSEQUENTIALID()</span></span>
* <span data-ttu-id="24d56-169">@@NESTLEVEL()</span><span class="sxs-lookup"><span data-stu-id="24d56-169">@@NESTLEVEL()</span></span>
* <span data-ttu-id="24d56-170">@@IDENTITY()</span><span class="sxs-lookup"><span data-stu-id="24d56-170">@@IDENTITY()</span></span>
* <span data-ttu-id="24d56-171">@@ROWCOUNT()</span><span class="sxs-lookup"><span data-stu-id="24d56-171">@@ROWCOUNT()</span></span>
* <span data-ttu-id="24d56-172">ROWCOUNT_BIG</span><span class="sxs-lookup"><span data-stu-id="24d56-172">ROWCOUNT_BIG</span></span>
* <span data-ttu-id="24d56-173">ERROR_LINE()</span><span class="sxs-lookup"><span data-stu-id="24d56-173">ERROR_LINE()</span></span>

<span data-ttu-id="24d56-174">Alguns desses problemas podem ser solucionados.</span><span class="sxs-lookup"><span data-stu-id="24d56-174">Some of these issues can be worked around.</span></span>

## <a name="rowcount-workaround"></a><span data-ttu-id="24d56-175">Solução alternativa @@ROWCOUNT</span><span class="sxs-lookup"><span data-stu-id="24d56-175">@@ROWCOUNT workaround</span></span>
<span data-ttu-id="24d56-176">Para solucionar a falta de suporte para @@ROWCOUNT, crie um procedimento armazenado que recuperará a última contagem de linhas de sys.dm_pdw_request_steps e, em seguida, execute `EXEC LastRowCount` após uma instrução DML.</span><span class="sxs-lookup"><span data-stu-id="24d56-176">To work around lack of support for @@ROWCOUNT, create a stored procedure that will retrieve the last row count from sys.dm_pdw_request_steps and then execute `EXEC LastRowCount` after a DML statement.</span></span>

```sql
CREATE PROCEDURE LastRowCount AS
WITH LastRequest as 
(   SELECT TOP 1    request_id
    FROM            sys.dm_pdw_exec_requests
    WHERE           session_id = SESSION_ID()
    AND             resource_class IS NOT NULL
    ORDER BY end_time DESC
),
LastRequestRowCounts as
(
    SELECT  step_index, row_count
    FROM    sys.dm_pdw_request_steps
    WHERE   row_count >= 0
    AND     request_id IN (SELECT request_id from LastRequest)
)
SELECT TOP 1 row_count FROM LastRequestRowCounts ORDER BY step_index DESC
;
```

## <a name="next-steps"></a><span data-ttu-id="24d56-177">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="24d56-177">Next steps</span></span>
<span data-ttu-id="24d56-178">Para obter uma lista completa de todas as instruções T-SQL com suporte, confira [Tópicos do Transact-SQL][Transact-SQL topics].</span><span class="sxs-lookup"><span data-stu-id="24d56-178">For a complete list of all supported T-SQL statements, see [Transact-SQL topics][Transact-SQL topics].</span></span>

<!--Image references-->

<!--Article references-->
[ANSI joins on updates]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-update-statements
[ANSI joins on deletes]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-delete-statements
[merge statement]: ./sql-data-warehouse-develop-ctas.md#replace-merge-statements
[INSERT..EXEC]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[Transact-SQL topics]: ./sql-data-warehouse-reference-tsql-statements.md

[cursors]: ./sql-data-warehouse-develop-loops.md
[group by clause with rollup / cube / grouping sets options]: ./sql-data-warehouse-develop-group-by-options.md
[nesting levels beyond 8]: ./sql-data-warehouse-develop-transactions.md
[updating through views]: ./sql-data-warehouse-develop-views.md
[use of select for variable assignment]: ./sql-data-warehouse-develop-variable-assignment.md
[no MAX data type for dynamic SQL strings]: ./sql-data-warehouse-develop-dynamic-sql.md

<!--MSDN references-->

<!--Other Web references-->
