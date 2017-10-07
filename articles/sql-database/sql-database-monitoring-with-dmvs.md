---
title: "Azure SQL Database usando exibições de gerenciamento dinâmico de aaaMonitoring | Microsoft Docs"
description: "Saiba como toodetect e diagnosticar problemas de desempenho comuns usando exibições de gerenciamento dinâmico toomonitor banco de dados SQL do Microsoft Azure."
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
ms.openlocfilehash: 43d5fe2dd9a38d031e9334f6ad49fce5866e3bec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-sql-database-using-dynamic-management-views"></a><span data-ttu-id="c6f14-103">Monitoramento de Banco de Dados SQL usando exibições de gerenciamento dinâmico</span><span class="sxs-lookup"><span data-stu-id="c6f14-103">Monitoring Azure SQL Database using dynamic management views</span></span>
<span data-ttu-id="c6f14-104">Banco de dados SQL do Microsoft Azure habilita um subconjunto de gerenciamento dinâmico exibe toodiagnose problemas de desempenho, que podem ser causados por consultas bloqueadas ou demoradas, afunilamentos de recursos, planos de consulta ruins e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="c6f14-104">Microsoft Azure SQL Database enables a subset of dynamic management views toodiagnose performance problems, which might be caused by blocked or long-running queries, resource bottlenecks, poor query plans, and so on.</span></span> <span data-ttu-id="c6f14-105">Este tópico fornece informações sobre como toodetect problemas comuns de desempenho por meio de exibições de gerenciamento dinâmico.</span><span class="sxs-lookup"><span data-stu-id="c6f14-105">This topic provides information on how toodetect common performance problems by using dynamic management views.</span></span>

<span data-ttu-id="c6f14-106">O Banco de Dados SQL oferece suporte parcial para três categorias de exibições de gerenciamento dinâmico:</span><span class="sxs-lookup"><span data-stu-id="c6f14-106">SQL Database partially supports three categories of dynamic management views:</span></span>

* <span data-ttu-id="c6f14-107">Exibições de gerenciamento dinâmico relacionadas ao banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c6f14-107">Database-related dynamic management views.</span></span>
* <span data-ttu-id="c6f14-108">Exibições de gerenciamento dinâmico relacionadas à execução.</span><span class="sxs-lookup"><span data-stu-id="c6f14-108">Execution-related dynamic management views.</span></span>
* <span data-ttu-id="c6f14-109">Exibições de gerenciamento dinâmico relacionadas à transação.</span><span class="sxs-lookup"><span data-stu-id="c6f14-109">Transaction-related dynamic management views.</span></span>

<span data-ttu-id="c6f14-110">Para obter informações detalhadas sobre exibições de gerenciamento dinâmico, consulte [Funções e exibições (Transact-SQL) de gerenciamento dinâmico](https://msdn.microsoft.com/library/ms188754.aspx) nos Manuais Online do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c6f14-110">For detailed information on dynamic management views, see [Dynamic Management Views and Functions (Transact-SQL)](https://msdn.microsoft.com/library/ms188754.aspx) in SQL Server Books Online.</span></span>

## <a name="permissions"></a><span data-ttu-id="c6f14-111">Permissões</span><span class="sxs-lookup"><span data-stu-id="c6f14-111">Permissions</span></span>
<span data-ttu-id="c6f14-112">No Banco de Dados SQL, consultar uma visualização de gerenciamento dinâmico requer permissões **VIEW DATABASE STATE** .</span><span class="sxs-lookup"><span data-stu-id="c6f14-112">In SQL Database, querying a dynamic management view requires **VIEW DATABASE STATE** permissions.</span></span> <span data-ttu-id="c6f14-113">Olá **VIEW DATABASE STATE** permissão retorna informações sobre todos os objetos de banco de dados atual hello.</span><span class="sxs-lookup"><span data-stu-id="c6f14-113">hello **VIEW DATABASE STATE** permission returns information about all objects within hello current database.</span></span>
<span data-ttu-id="c6f14-114">Olá toogrant **VIEW DATABASE STATE** usuário de banco de dados específico tooa permissão, execute Olá consulta a seguir:</span><span class="sxs-lookup"><span data-stu-id="c6f14-114">toogrant hello **VIEW DATABASE STATE** permission tooa specific database user, run hello following query:</span></span>

```GRANT VIEW DATABASE STATE toodatabase_user; ```

<span data-ttu-id="c6f14-115">Em uma instância do SQL Server local, as exibições de gerenciamento dinâmico retornam informações de estado do servidor.</span><span class="sxs-lookup"><span data-stu-id="c6f14-115">In an instance of on-premises SQL Server, dynamic management views return server state information.</span></span> <span data-ttu-id="c6f14-116">Em um Banco de Dados SQL, elas retornam informações relacionadas apenas ao seu banco de dados lógico atual.</span><span class="sxs-lookup"><span data-stu-id="c6f14-116">In SQL Database, they return information regarding your current logical database only.</span></span>

## <a name="calculating-database-size"></a><span data-ttu-id="c6f14-117">Calculando o tamanho do banco de dados</span><span class="sxs-lookup"><span data-stu-id="c6f14-117">Calculating database size</span></span>
<span data-ttu-id="c6f14-118">Olá consulta a seguir retorna o tamanho de saudação do banco de dados (em megabytes):</span><span class="sxs-lookup"><span data-stu-id="c6f14-118">hello following query returns hello size of your database (in megabytes):</span></span>

```
-- Calculates hello size of hello database.
SELECT SUM(reserved_page_count)*8.0/1024
FROM sys.dm_db_partition_stats;
GO
```

<span data-ttu-id="c6f14-119">Olá consulta a seguir retorna Olá tamanho dos objetos individuais (em megabytes) no banco de dados:</span><span class="sxs-lookup"><span data-stu-id="c6f14-119">hello following query returns hello size of individual objects (in megabytes) in your database:</span></span>

```
-- Calculates hello size of individual database objects.
SELECT sys.objects.name, SUM(reserved_page_count) * 8.0 / 1024
FROM sys.dm_db_partition_stats, sys.objects
WHERE sys.dm_db_partition_stats.object_id = sys.objects.object_id
GROUP BY sys.objects.name;
GO
```

## <a name="monitoring-connections"></a><span data-ttu-id="c6f14-120">Monitoramento de conexões</span><span class="sxs-lookup"><span data-stu-id="c6f14-120">Monitoring connections</span></span>
<span data-ttu-id="c6f14-121">Você pode usar o hello [sys.DM exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) exibir tooretrieve informações sobre o servidor de banco de dados SQL específico do hello conexões estabelecidas tooa e detalhes de saudação de cada conexão.</span><span class="sxs-lookup"><span data-stu-id="c6f14-121">You can use hello [sys.dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) view tooretrieve information about hello connections established tooa specific Azure SQL Database server and hello details of each connection.</span></span> <span data-ttu-id="c6f14-122">Além disso, Olá [sys.DM exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) exibição é útil ao recuperar as informações sobre todas as conexões de usuário ativas e tarefas internas.</span><span class="sxs-lookup"><span data-stu-id="c6f14-122">In addition, hello [sys.dm_exec_sessions](https://msdn.microsoft.com/library/ms176013.aspx) view is helpful when retrieving information about all active user connections and internal tasks.</span></span>
<span data-ttu-id="c6f14-123">Olá consulta a seguir recupera informações sobre a conexão atual hello:</span><span class="sxs-lookup"><span data-stu-id="c6f14-123">hello following query retrieves information on hello current connection:</span></span>

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
> <span data-ttu-id="c6f14-124">Ao executar Olá **exec_requests** e **modos de exibição de sys.DM exec_sessions**, se você tiver **VIEW DATABASE STATE** permissão no banco de dados hello, consulte executando todas as sessões no banco de dados Olá; Caso contrário, você vê apenas Olá sessão atual.</span><span class="sxs-lookup"><span data-stu-id="c6f14-124">When executing hello **sys.dm_exec_requests** and **sys.dm_exec_sessions views**, if you have **VIEW DATABASE STATE** permission on hello database, you see all executing sessions on hello database; otherwise, you see only hello current session.</span></span>
> 
> 

## <a name="monitoring-query-performance"></a><span data-ttu-id="c6f14-125">Monitoramento de desempenho da consulta</span><span class="sxs-lookup"><span data-stu-id="c6f14-125">Monitoring query performance</span></span>
<span data-ttu-id="c6f14-126">Consultas de execução lenta ou longa podem consumir recursos significativos do sistema.</span><span class="sxs-lookup"><span data-stu-id="c6f14-126">Slow or long running queries can consume significant system resources.</span></span> <span data-ttu-id="c6f14-127">Esta seção demonstra como toouse exibições de gerenciamento dinâmico toodetect alguns problemas comuns de desempenho de consulta.</span><span class="sxs-lookup"><span data-stu-id="c6f14-127">This section demonstrates how toouse dynamic management views toodetect a few common query performance problems.</span></span> <span data-ttu-id="c6f14-128">Uma referência mais antiga, mas ainda é útil para solução de problemas, é hello [Solucionando problemas de desempenho no SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) artigo no Microsoft TechNet.</span><span class="sxs-lookup"><span data-stu-id="c6f14-128">An older but still helpful reference for troubleshooting, is hello [Troubleshooting Performance Problems in SQL Server 2008](http://download.microsoft.com/download/D/B/D/DBDE7972-1EB9-470A-BA18-58849DB3EB3B/TShootPerfProbs2008.docx) article on Microsoft TechNet.</span></span>

### <a name="finding-top-n-queries"></a><span data-ttu-id="c6f14-129">Localizando as principais consultas N</span><span class="sxs-lookup"><span data-stu-id="c6f14-129">Finding top N queries</span></span>
<span data-ttu-id="c6f14-130">Olá, exemplo a seguir retorna informações sobre Olá cinco principais consultas classificadas por tempo médio de CPU.</span><span class="sxs-lookup"><span data-stu-id="c6f14-130">hello following example returns information about hello top five queries ranked by average CPU time.</span></span> <span data-ttu-id="c6f14-131">Este exemplo agrega as consultas de saudação de acordo com tootheir hash de consulta, para que as consultas logicamente equivalentes sejam agrupadas pelo respectivo consumo de recursos cumulativo.</span><span class="sxs-lookup"><span data-stu-id="c6f14-131">This example aggregates hello queries according tootheir query hash, so that logically equivalent queries are grouped by their cumulative resource consumption.</span></span>

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

### <a name="monitoring-blocked-queries"></a><span data-ttu-id="c6f14-132">Monitoramento de consultas bloqueadas</span><span class="sxs-lookup"><span data-stu-id="c6f14-132">Monitoring blocked queries</span></span>
<span data-ttu-id="c6f14-133">Consultas de execução longa ou lenta podem contribuir tooexcessive o consumo de recursos e ser consequência de saudação de consultas bloqueadas.</span><span class="sxs-lookup"><span data-stu-id="c6f14-133">Slow or long-running queries can contribute tooexcessive resource consumption and be hello consequence of blocked queries.</span></span> <span data-ttu-id="c6f14-134">causa Olá Olá bloqueio pode ser o design de aplicativo insatisfatório, ruim planos de consulta, Olá falta de índices úteis e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="c6f14-134">hello cause of hello blocking can be poor application design, bad query plans, hello lack of useful indexes, and so on.</span></span> <span data-ttu-id="c6f14-135">Você pode usar o hello tran_locks exibir tooget informações sobre a atividade de bloqueio atual Olá no banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6f14-135">You can use hello sys.dm_tran_locks view tooget information about hello current locking activity in your Azure SQL Database.</span></span> <span data-ttu-id="c6f14-136">Para ver um exemplo de código, veja [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) nos Manuais Online do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c6f14-136">For example code, see [sys.dm_tran_locks (Transact-SQL)](https://msdn.microsoft.com/library/ms190345.aspx) in SQL Server Books Online.</span></span>

### <a name="monitoring-query-plans"></a><span data-ttu-id="c6f14-137">Monitoramento de planos de consulta</span><span class="sxs-lookup"><span data-stu-id="c6f14-137">Monitoring query plans</span></span>
<span data-ttu-id="c6f14-138">Um plano de consulta ineficiente também pode aumentar o consumo de CPU.</span><span class="sxs-lookup"><span data-stu-id="c6f14-138">An inefficient query plan also may increase CPU consumption.</span></span> <span data-ttu-id="c6f14-139">Olá, exemplo a seguir usa Olá [sys.DM exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) exibir toodetermine qual consulta usa a CPU mais cumulativa hello.</span><span class="sxs-lookup"><span data-stu-id="c6f14-139">hello following example uses hello [sys.dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) view toodetermine which query uses hello most cumulative CPU.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="c6f14-140">Consulte também</span><span class="sxs-lookup"><span data-stu-id="c6f14-140">See also</span></span>
[<span data-ttu-id="c6f14-141">Introdução tooSQL banco de dados</span><span class="sxs-lookup"><span data-stu-id="c6f14-141">Introduction tooSQL Database</span></span>](sql-database-technical-overview.md)

