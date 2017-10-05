---
title: "Monitoramento de Banco de Dados SQL do Azure usando exibições de gerenciamento dinâmico | Microsoft Docs"
description: "Saiba como detectar e diagnosticar problemas de desempenho comuns usando exibições de gerenciamento dinâmico para monitorar o Banco de Dados SQL do Microsoft Azure."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: d08f505f-3c62-47d4-bab7-35c9a834b79b
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: d9b007d29e06e672db71b4a8415673f258c3fd89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-azure-sql-database-using-dynamic-management-views"></a><span data-ttu-id="0a3d7-103">Monitoramento de Banco de Dados SQL usando exibições de gerenciamento dinâmico</span><span class="sxs-lookup"><span data-stu-id="0a3d7-103">Monitoring Azure SQL Database using dynamic management views</span></span>
<span data-ttu-id="0a3d7-104">O Banco de Dados SQL do Microsoft Azure permite um subconjunto de modos de exibição de gerenciamento dinâmico para diagnosticar problemas de desempenho, que podem ser causados por consultas bloqueadas ou demoradas, afunilamentos de recursos, planos de consulta ruins e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="0a3d7-104">Microsoft Azure SQL Database enables a subset of dynamic management views to diagnose performance problems, which might be caused by blocked or long-running queries, resource bottlenecks, poor query plans, and so on.</span></span> <span data-ttu-id="0a3d7-105">Este tópico fornece informações sobre como detectar problemas de desempenho comuns usando exibições de gerenciamento dinâmico.</span><span class="sxs-lookup"><span data-stu-id="0a3d7-105">This topic provides information on how to detect common performance problems by using dynamic management views.</span></span>

<span data-ttu-id="0a3d7-106">O Banco de Dados SQL oferece suporte parcial para três categorias de exibições de gerenciamento dinâmico:</span><span class="sxs-lookup"><span data-stu-id="0a3d7-106">SQL Database partially supports three categories of dynamic management views:</span></span>

* <span data-ttu-id="0a3d7-107">Exibições de gerenciamento dinâmico relacionadas ao banco de dados.</span><span class="sxs-lookup"><span data-stu-id="0a3d7-107">Database-related dynamic management views.</span></span>
* <span data-ttu-id="0a3d7-108">Exibições de gerenciamento dinâmico relacionadas à execução.</span><span class="sxs-lookup"><span data-stu-id="0a3d7-108">Execution-related dynamic management views.</span></span>
* <span data-ttu-id="0a3d7-109">Exibições de gerenciamento dinâmico relacionadas à transação.</span><span class="sxs-lookup"><span data-stu-id="0a3d7-109">Transaction-related dynamic management views.</span></span>

<span data-ttu-id="0a3d7-110">Para obter informações detalhadas sobre exibições de gerenciamento dinâmico, consulte [Funções e exibições (Transact-SQL) de gerenciamento dinâmico](https://msdn.microsoft.com/library/ms188754.aspx) nos Manuais Online do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0a3d7-110">For detailed information on dynamic management views, see [Dynamic Management Views and Functions (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) in SQL Server Books Online.</span></span>

## <a name="permissions"></a><span data-ttu-id="0a3d7-111">Permissões</span><span class="sxs-lookup"><span data-stu-id="0a3d7-111">Permissions</span></span>
<span data-ttu-id="0a3d7-112">No Banco de Dados SQL, consultar uma visualização de gerenciamento dinâmico requer permissões **VIEW DATABASE STATE** .</span><span class="sxs-lookup"><span data-stu-id="0a3d7-112">In SQL Database, querying a dynamic management view requires **VIEW DATABASE STATE** permissions.</span></span> <span data-ttu-id="0a3d7-113">A permissão **VIEW DATABASE STATE** retorna informações sobre todos os objetos no banco de dados atual.</span><span class="sxs-lookup"><span data-stu-id="0a3d7-113">The **VIEW DATABASE STATE** permission returns information about all objects within the current database.</span></span>
<span data-ttu-id="0a3d7-114">Para conceder a permissão **VIEW DATABASE STATE** a um usuário específico do banco de dados, execute a seguinte consulta:</span><span class="sxs-lookup"><span data-stu-id="0a3d7-114">To grant the **VIEW DATABASE STATE** permission to a specific database user, run the following query:</span></span>

```GRANT VIEW DATABASE STATE TO database_user; ```

<span data-ttu-id="0a3d7-115">Em uma instância do SQL Server local, as exibições de gerenciamento dinâmico retornam informações de estado do servidor.</span><span class="sxs-lookup"><span data-stu-id="0a3d7-115">In an instance of on-premises SQL Server, dynamic management views return server state information.</span></span> <span data-ttu-id="0a3d7-116">Em um Banco de Dados SQL, elas retornam informações relacionadas apenas ao seu banco de dados lógico atual.</span><span class="sxs-lookup"><span data-stu-id="0a3d7-116">In SQL Database, they return information regarding your current logical database only.</span></span>

## <a name="calculating-database-size"></a><span data-ttu-id="0a3d7-117">Calculando o tamanho do banco de dados</span><span class="sxs-lookup"><span data-stu-id="0a3d7-117">Calculating database size</span></span>
<span data-ttu-id="0a3d7-118">A seguinte consulta retorna o tamanho do seu banco de dados (em megabytes):</span><span class="sxs-lookup"><span data-stu-id="0a3d7-118">The following query returns the size of your database (in megabytes):</span></span>

```
-- Calculates the size of the database.
SELECT SUM(reserved_page_count)*8.0/1024
FROM sys.dm_db_partition_stats;
GO
```

<span data-ttu-id="0a3d7-119">A consulta a seguir retorna o tamanho do dos objetos individuais (em megabytes) no seu banco de dados:</span><span class="sxs-lookup"><span data-stu-id="0a3d7-119">The following query returns the size of individual objects (in megabytes) in your database:</span></span>

```
-- Calculates the size of individual database objects.
SELECT sys.objects.name, SUM(reserved_page_count) * 8.0 / 1024
FROM sys.dm_db_partition_stats, sys.objects
WHERE sys.dm_db_partition_stats.object_id = sys.objects.object_id
GROUP BY sys.objects.name;
GO
```

## <a name="monitoring-connections"></a><span data-ttu-id="0a3d7-120">Monitoramento de conexões</span><span class="sxs-lookup"><span data-stu-id="0a3d7-120">Monitoring connections</span></span>
<span data-ttu-id="0a3d7-121">É possível usar a exibição [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) para recuperar informações sobre as conexões estabelecidas com um servidor do Banco de dados SQL do Azure específico e os detalhes de cada conexão.</span><span class="sxs-lookup"><span data-stu-id="0a3d7-121">You can use the [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) view to retrieve information about the connections established to a specific Azure SQL Database server and the details of each connection.</span></span> <span data-ttu-id="0a3d7-122">Além disso, a exibição [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) é útil ao recuperar informações sobre todas as conexões de usuário e tarefas internas ativas.</span><span class="sxs-lookup"><span data-stu-id="0a3d7-122">In addition, the [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) view is helpful when retrieving information about all active user connections and internal tasks.</span></span>
<span data-ttu-id="0a3d7-123">A consulta a seguir recupera as informações sobre a conexão atual:</span><span class="sxs-lookup"><span data-stu-id="0a3d7-123">The following query retrieves information on the current connection:</span></span>

```
SELECT
    c.session_id, c.net_transport, c.encrypt_option,
    c.auth_scheme, s.host_name, s.program_name,
    s.client_interface_name, s.login_name, s.nt_domain,
    s.nt_user_name, s.original_login_name, c.connect_time,
    s.login_time
FROM sys.dm_exec_connections AS c
JOIN sys.dm_exec_sessions AS s
    ON c.session_id = s.session_id
WHERE c.session_id = @@SPID;
```

> [!NOTE]
> <span data-ttu-id="0a3d7-124">Ao executar as exibições **sys.dm_exec_requests** e **sys.dm_exec_sessions**, se você tiver a permissão **EXIBIR ESTADO DO BANCO DE DADOS** no banco de dados, verá todas as sessões em execução no banco de dados; caso contrário, verá apenas a sessão atual.</span><span class="sxs-lookup"><span data-stu-id="0a3d7-124">When executing the **sys.dm_exec_requests** and **sys.dm_exec_sessions views**, if you have **VIEW DATABASE STATE** permission on the database, you see all executing sessions on the database; otherwise, you see only the current session.</span></span>
> 
> 

## <a name="monitoring-query-performance"></a><span data-ttu-id="0a3d7-125">Monitoramento de desempenho da consulta</span><span class="sxs-lookup"><span data-stu-id="0a3d7-125">Monitoring query performance</span></span>
<span data-ttu-id="0a3d7-126">Consultas de execução lenta ou longa podem consumir recursos significativos do sistema.</span><span class="sxs-lookup"><span data-stu-id="0a3d7-126">Slow or long running queries can consume significant system resources.</span></span> <span data-ttu-id="0a3d7-127">Esta seção demonstra como usar exibições de gerenciamento dinâmico para detectar alguns problemas comuns de desempenho de consulta.</span><span class="sxs-lookup"><span data-stu-id="0a3d7-127">This section demonstrates how to use dynamic management views to detect a few common query performance problems.</span></span> <span data-ttu-id="0a3d7-128">Uma referência mais antiga, mas ainda útil para solução de problemas, é o artigo [Solucionando problemas de desempenho no SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) no Microsoft TechNet.</span><span class="sxs-lookup"><span data-stu-id="0a3d7-128">An older but still helpful reference for troubleshooting, is the [Troubleshooting Performance Problems in SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) article on Microsoft TechNet.</span></span>

### <a name="finding-top-n-queries"></a><span data-ttu-id="0a3d7-129">Localizando as principais consultas N</span><span class="sxs-lookup"><span data-stu-id="0a3d7-129">Finding top N queries</span></span>
<span data-ttu-id="0a3d7-130">O exemplo a seguir retorna informações sobre as cinco principais consultas classificadas pelo tempo médio de CPU.</span><span class="sxs-lookup"><span data-stu-id="0a3d7-130">The following example returns information about the top five queries ranked by average CPU time.</span></span> <span data-ttu-id="0a3d7-131">Este exemplo agrega as consultas de acordo com sua hash de consulta, para que as consultas logicamente equivalentes sejam agrupadas em função de seu consumo de recursos cumulativos.</span><span class="sxs-lookup"><span data-stu-id="0a3d7-131">This example aggregates the queries according to their query hash, so that logically equivalent queries are grouped by their cumulative resource consumption.</span></span>

```
SELECT TOP 5 query_stats.query_hash AS "Query Hash",
    SUM(query_stats.total_worker_time) / SUM(query_stats.execution_count) AS "Avg CPU Time",
    MIN(query_stats.statement_text) AS "Statement Text"
FROM
    (SELECT QS.*,
    SUBSTRING(ST.text, (QS.statement_start_offset/2) + 1,
    ((CASE statement_end_offset
        WHEN -1 THEN DATALENGTH(ST.text)
        ELSE QS.statement_end_offset END
            - QS.statement_start_offset)/2) + 1) AS statement_text
     FROM sys.dm_exec_query_stats AS QS
     CROSS APPLY sys.dm_exec_sql_text(QS.sql_handle) as ST) as query_stats
GROUP BY query_stats.query_hash
ORDER BY 2 DESC;
```

### <a name="monitoring-blocked-queries"></a><span data-ttu-id="0a3d7-132">Monitoramento de consultas bloqueadas</span><span class="sxs-lookup"><span data-stu-id="0a3d7-132">Monitoring blocked queries</span></span>
<span data-ttu-id="0a3d7-133">Consultas lentas ou demoradas podem contribuir para consumo excessivo de recursos e ser a consequência de consultas bloqueadas.</span><span class="sxs-lookup"><span data-stu-id="0a3d7-133">Slow or long-running queries can contribute to excessive resource consumption and be the consequence of blocked queries.</span></span> <span data-ttu-id="0a3d7-134">A causa do bloqueio pode ser projeto inadequado de aplicativos, planos de consulta incorretos, a falta de índices úteis e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="0a3d7-134">The cause of the blocking can be poor application design, bad query plans, the lack of useful indexes, and so on.</span></span> <span data-ttu-id="0a3d7-135">Você pode usar o modo de exibição sys.dm_tran_locks para obter informações sobre a atividade de bloqueio atual em seu Banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a3d7-135">You can use the sys.dm_tran_locks view to get information about the current locking activity in your Azure SQL Database.</span></span> <span data-ttu-id="0a3d7-136">Para ver um exemplo de código, veja [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) nos Manuais Online do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0a3d7-136">For example code, see [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) in SQL Server Books Online.</span></span>

### <a name="monitoring-query-plans"></a><span data-ttu-id="0a3d7-137">Monitoramento de planos de consulta</span><span class="sxs-lookup"><span data-stu-id="0a3d7-137">Monitoring query plans</span></span>
<span data-ttu-id="0a3d7-138">Um plano de consulta ineficiente também pode aumentar o consumo de CPU.</span><span class="sxs-lookup"><span data-stu-id="0a3d7-138">An inefficient query plan also may increase CPU consumption.</span></span> <span data-ttu-id="0a3d7-139">O exemplo a seguir usa a exibição [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) para determinar qual consulta usa a CPU mais cumulativa.</span><span class="sxs-lookup"><span data-stu-id="0a3d7-139">The following example uses the [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) view to determine which query uses the most cumulative CPU.</span></span>

```
SELECT
    highest_cpu_queries.plan_handle,
    highest_cpu_queries.total_worker_time,
    q.dbid,
    q.objectid,
    q.number,
    q.encrypted,
    q.[text]
FROM
    (SELECT TOP 50
        qs.plan_handle,
        qs.total_worker_time
    FROM
        sys.dm_exec_query_stats qs
    ORDER BY qs.total_worker_time desc) AS highest_cpu_queries
    CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS q
ORDER BY highest_cpu_queries.total_worker_time DESC;
```

## <a name="see-also"></a><span data-ttu-id="0a3d7-140">Consulte também</span><span class="sxs-lookup"><span data-stu-id="0a3d7-140">See also</span></span>
[<span data-ttu-id="0a3d7-141">Introdução ao Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="0a3d7-141">Introduction to SQL Database</span></span>](sql-database-technical-overview.md)

