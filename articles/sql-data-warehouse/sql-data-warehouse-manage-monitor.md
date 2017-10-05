---
title: Monitore sua carga de trabalho usando DMVs | Microsoft Docs
description: Aprenda a monitorar sua carga de trabalho usando DMVs.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 69ecd479-0941-48df-b3d0-cf54c79e6549
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 7ce6c2cdf1e28852da536414533ccdcdaeb437e5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-your-workload-using-dmvs"></a><span data-ttu-id="59538-103">Monitore sua carga de trabalho usando DMVs</span><span class="sxs-lookup"><span data-stu-id="59538-103">Monitor your workload using DMVs</span></span>
<span data-ttu-id="59538-104">Este artigo descreve como usar Visualizações de Gerenciamento Dinâmico (DMVs) para monitorar sua carga de trabalho e investigar a execução da consulta no SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="59538-104">This article describes how to use Dynamic Management Views (DMVs) to monitor your workload and investigate query execution in Azure SQL Data Warehouse.</span></span>

## <a name="permissions"></a><span data-ttu-id="59538-105">Permissões</span><span class="sxs-lookup"><span data-stu-id="59538-105">Permissions</span></span>
<span data-ttu-id="59538-106">Para consultar as DMVs deste artigo, você precisa de permissão VIEW DATABASE STATE ou CONTROL.</span><span class="sxs-lookup"><span data-stu-id="59538-106">To query the DMVs in this article, you need either VIEW DATABASE STATE or CONTROL permission.</span></span> <span data-ttu-id="59538-107">Geralmente, é preferível conceder a permissão VIEW DATABASE STATE, por ser muito mais restritiva.</span><span class="sxs-lookup"><span data-stu-id="59538-107">Usually granting VIEW DATABASE STATE is the preferred permission as it is much more restrictive.</span></span>

```sql
GRANT VIEW DATABASE STATE TO myuser;
```

## <a name="monitor-connections"></a><span data-ttu-id="59538-108">Conexões do monitor</span><span class="sxs-lookup"><span data-stu-id="59538-108">Monitor connections</span></span>
<span data-ttu-id="59538-109">Todos os logons no SQL Data Warehouse são registrados em [sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span><span class="sxs-lookup"><span data-stu-id="59538-109">All logins to SQL Data Warehouse are logged to [sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span></span>  <span data-ttu-id="59538-110">Essa DMV contém os últimos 10.000 logons.</span><span class="sxs-lookup"><span data-stu-id="59538-110">This DMV contains the last 10,000 logins.</span></span>  <span data-ttu-id="59538-111">A session_id é a chave primária e é atribuída em sequência para cada novo logon.</span><span class="sxs-lookup"><span data-stu-id="59538-111">The session_id is the primary key and is assigned sequentially for each new logon.</span></span>

```sql
-- Other Active Connections
SELECT * FROM sys.dm_pdw_exec_sessions where status <> 'Closed' and session_id <> session_id();
```

## <a name="monitor-query-execution"></a><span data-ttu-id="59538-112">Monitorar a execução de consultas</span><span class="sxs-lookup"><span data-stu-id="59538-112">Monitor query execution</span></span>
<span data-ttu-id="59538-113">Todas as consultas executadas no SQL Data Warehouse são registradas em [sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span><span class="sxs-lookup"><span data-stu-id="59538-113">All queries executed on SQL Data Warehouse are logged to [sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span></span>  <span data-ttu-id="59538-114">Essa DMV contém as últimas 10.000 consultas executadas.</span><span class="sxs-lookup"><span data-stu-id="59538-114">This DMV contains the last 10,000 queries executed.</span></span>  <span data-ttu-id="59538-115">A request_id identifica cada consulta exclusivamente e é a chave primária para essa DMV.</span><span class="sxs-lookup"><span data-stu-id="59538-115">The request_id uniquely identifies each query and is the primary key for this DMV.</span></span>  <span data-ttu-id="59538-116">A request_id é atribuída em sequência para cada nova consulta e é prefixada com QID, que representa a ID da consulta.</span><span class="sxs-lookup"><span data-stu-id="59538-116">The request_id is assigned sequentially for each new query and is prefixed with QID, which stands for query ID.</span></span>  <span data-ttu-id="59538-117">A consulta a esta DMV para uma determinada session_id mostra todas as consultas para um logon específico.</span><span class="sxs-lookup"><span data-stu-id="59538-117">Querying this DMV for a given session_id shows all queries for a given logon.</span></span>

> [!NOTE]
> <span data-ttu-id="59538-118">Os procedimentos armazenados usam vários request_ids.</span><span class="sxs-lookup"><span data-stu-id="59538-118">Stored procedures use multiple Request IDs.</span></span>  <span data-ttu-id="59538-119">As IDs de solicitação são atribuídas em ordem sequencial.</span><span class="sxs-lookup"><span data-stu-id="59538-119">Request IDs are assigned in sequential order.</span></span> 
> 
> 

<span data-ttu-id="59538-120">Estas são as etapas para investigar os planos de execução da consulta e as horas para uma consulta específica.</span><span class="sxs-lookup"><span data-stu-id="59538-120">Here are steps to follow to investigate query execution plans and times for a particular query.</span></span>

### <a name="step-1-identify-the-query-you-wish-to-investigate"></a><span data-ttu-id="59538-121">ETAPA 1: Identificar a consulta que você deseja investigar</span><span class="sxs-lookup"><span data-stu-id="59538-121">STEP 1: Identify the query you wish to investigate</span></span>
```sql
-- Monitor active queries
SELECT * 
FROM sys.dm_pdw_exec_requests 
WHERE status not in ('Completed','Failed','Cancelled')
  AND session_id <> session_id()
ORDER BY submit_time DESC;

-- Find top 10 queries longest running queries
SELECT TOP 10 * 
FROM sys.dm_pdw_exec_requests 
ORDER BY total_elapsed_time DESC;

-- Find a query with the Label 'My Query'
-- Use brackets when querying the label column, as it it a key word
SELECT  *
FROM    sys.dm_pdw_exec_requests
WHERE   [label] = 'My Query';
```

<span data-ttu-id="59538-122">Nos resultados da consulta anterior, **observe a ID da Solicitação** da consulta que você deseja investigar.</span><span class="sxs-lookup"><span data-stu-id="59538-122">From the preceding query results, **note the Request ID** of the query that you would like to investigate.</span></span>

<span data-ttu-id="59538-123">As consultas no estado **Suspenso** estão sendo enfileiradas devido aos limites de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="59538-123">Queries in the **Suspended** state are being queued due to concurrency limits.</span></span> <span data-ttu-id="59538-124">Essas consultas também aparecem na consulta de esperas sys.dm_pdw_waits com um tipo de UserConcurrencyResourceType.</span><span class="sxs-lookup"><span data-stu-id="59538-124">These queries also appear in the sys.dm_pdw_waits waits query with a type of UserConcurrencyResourceType.</span></span> <span data-ttu-id="59538-125">Confira [Concurrency and workload management][Concurrency and workload management] (Gerenciamento de simultaneidade e carga de trabalho) para obter mais detalhes sobre os limites de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="59538-125">See [Concurrency and workload management][Concurrency and workload management] for more details on concurrency limits.</span></span> <span data-ttu-id="59538-126">As consultas também podem esperar por motivos, como bloqueios.</span><span class="sxs-lookup"><span data-stu-id="59538-126">Queries can also wait for other reasons such as for object locks.</span></span>  <span data-ttu-id="59538-127">Se sua consulta estiver aguardando um recurso, confira [Investigar consultas aguardando recursos][Investigating queries waiting for resources] mais adiante neste artigo.</span><span class="sxs-lookup"><span data-stu-id="59538-127">If your query is waiting for a resource, see [Investigating queries waiting for resources][Investigating queries waiting for resources] further down in this article.</span></span>

<span data-ttu-id="59538-128">Para simplificar a pesquisa de uma consulta na tabela sys.dm_pdw_exec_requests, use [LABEL][LABEL] para atribuir um comentário à consulta que pode ser pesquisada no modo de exibição sys.dm_pdw_exec_requests.</span><span class="sxs-lookup"><span data-stu-id="59538-128">To simplify the lookup of a query in the sys.dm_pdw_exec_requests table, use [LABEL][LABEL] to assign a comment to your query that can be looked up in the sys.dm_pdw_exec_requests view.</span></span>

```sql
-- Query with Label
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query')
;
```

### <a name="step-2-investigate-the-query-plan"></a><span data-ttu-id="59538-129">ETAPA 2: investigar o plano de consulta</span><span class="sxs-lookup"><span data-stu-id="59538-129">STEP 2: Investigate the query plan</span></span>
<span data-ttu-id="59538-130">Use a ID de solicitação para recuperar o DSQL (plano de SQL distribuído) da consulta de [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span><span class="sxs-lookup"><span data-stu-id="59538-130">Use the Request ID to retrieve the query's distributed SQL (DSQL) plan from [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span></span>

```sql
-- Find the distributed query plan steps for a specific query.
-- Replace request_id with value from Step 1.

SELECT * FROM sys.dm_pdw_request_steps
WHERE request_id = 'QID####'
ORDER BY step_index;
```

<span data-ttu-id="59538-131">Quando um plano DSQL estiver demorando mais do que o esperado, a causa pode ser um plano complexo com muitas etapas de DSQL ou apenas uma etapa demorando muito tempo.</span><span class="sxs-lookup"><span data-stu-id="59538-131">When a DSQL plan is taking longer than expected, the cause can be a complex plan with many DSQL steps or just one step taking a long time.</span></span>  <span data-ttu-id="59538-132">Se o plano tiver muitas etapas com várias operações de movimentação, considere otimizar suas distribuições de tabela para reduzir a movimentação de dados.</span><span class="sxs-lookup"><span data-stu-id="59538-132">If the plan is many steps with several move operations, consider optimizing your table distributions to reduce data movement.</span></span> <span data-ttu-id="59538-133">O artigo [Distribuição da tabela][Table distribution] explica por que os dados devem ser movidos para resolver uma consulta e explica algumas estratégias de distribuição para minimizar a movimentação de dados.</span><span class="sxs-lookup"><span data-stu-id="59538-133">The [Table distribution][Table distribution] article explains why data must be moved to solve a query and explains some distribution strategies to minimize data movement.</span></span>

<span data-ttu-id="59538-134">Para investigar mais detalhes sobre uma única etapa, verifique a coluna *operation_type* da etapa de consulta de execução longa de consulta e observe o **Índice da etapa**:</span><span class="sxs-lookup"><span data-stu-id="59538-134">To investigate further details about a single step, the *operation_type* column of the long-running query step and note the **Step Index**:</span></span>

* <span data-ttu-id="59538-135">Continue com a Etapa 3a para **Operações SQL**: OnOperation, RemoteOperation, ReturnOperation.</span><span class="sxs-lookup"><span data-stu-id="59538-135">Proceed with Step 3a for **SQL operations**: OnOperation, RemoteOperation, ReturnOperation.</span></span>
* <span data-ttu-id="59538-136">Continue com a Etapa 3b para **Operações de movimentação de dados**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span><span class="sxs-lookup"><span data-stu-id="59538-136">Proceed with Step 3b for **Data Movement operations**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span></span>

### <a name="step-3a-investigate-sql-on-the-distributed-databases"></a><span data-ttu-id="59538-137">ETAPA 3a: investigar o SQL nos bancos de dados distribuídos</span><span class="sxs-lookup"><span data-stu-id="59538-137">STEP 3a: Investigate SQL on the distributed databases</span></span>
<span data-ttu-id="59538-138">Use a ID da Solicitação e o Índice de Etapas para recuperar os detalhes de [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], que contém informações sobre a execução da consulta em todos os bancos de dados distribuídos.</span><span class="sxs-lookup"><span data-stu-id="59538-138">Use the Request ID and the Step Index to retrieve details from [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], which contains execution information of the query step on all of the distributed databases.</span></span>

```sql
-- Find the distribution run times for a SQL step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_sql_requests
WHERE request_id = 'QID####' AND step_index = 2;
```

<span data-ttu-id="59538-139">Se a consulta estiver em execução, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] poderá ser usado para recuperar o plano estimado do SQL Server do cache do plano do SQL Server para a etapa em execução em uma distribuição específica.</span><span class="sxs-lookup"><span data-stu-id="59538-139">When the query step is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used to retrieve the SQL Server estimated plan from the SQL Server plan cache for the step running on a particular distribution.</span></span>

```sql
-- Find the SQL Server execution plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(1, 78);
```

### <a name="step-3b-investigate-data-movement-on-the-distributed-databases"></a><span data-ttu-id="59538-140">ETAPA 3b: investigar a movimentação de dados em bancos de dados distribuídos</span><span class="sxs-lookup"><span data-stu-id="59538-140">STEP 3b: Investigate data movement on the distributed databases</span></span>
<span data-ttu-id="59538-141">Use a ID da Solicitação e o Índice da Etapa para recuperar as informações sobre a etapa de movimentação dos dados em execução em cada distribuição em [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span><span class="sxs-lookup"><span data-stu-id="59538-141">Use the Request ID and the Step Index to retrieve information about a data movement step running on each distribution from [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span></span>

```sql
-- Find the information about all the workers completing a Data Movement Step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_dms_workers
WHERE request_id = 'QID####' AND step_index = 2;
```

* <span data-ttu-id="59538-142">Verifique a coluna *total_elapsed_time* para ver se uma distribuição específica está demorando muito mais do que outras para movimentar dados.</span><span class="sxs-lookup"><span data-stu-id="59538-142">Check the *total_elapsed_time* column to see if a particular distribution is taking significantly longer than others for data movement.</span></span>
* <span data-ttu-id="59538-143">Para a distribuição de longa execução, verifique a coluna *rows_processed* para verificar se o número de linhas sendo movidas dessa distribuição é significativamente maior do que outros.</span><span class="sxs-lookup"><span data-stu-id="59538-143">For the long-running distribution, check the *rows_processed* column to see if the number of rows being moved from that distribution is significantly larger than others.</span></span> <span data-ttu-id="59538-144">Se for o caso, isso poderá indicar distorção de dados subjacentes.</span><span class="sxs-lookup"><span data-stu-id="59538-144">If so, this may indicate skew of your underlying data.</span></span>

<span data-ttu-id="59538-145">Se a consulta estiver em execução, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] poderá ser usado para recuperar o plano estimado do SQL Server do cache do plano do SQL Server para a Etapa de SQL em execução no momento em uma distribuição específica.</span><span class="sxs-lookup"><span data-stu-id="59538-145">If the query is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used to retrieve the SQL Server estimated plan from the SQL Server plan cache for the currently running SQL Step within a particular distribution.</span></span>

```sql
-- Find the SQL Server estimated plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(55, 238);
```

<a name="waiting"></a>

## <a name="monitor-waiting-queries"></a><span data-ttu-id="59538-146">Monitorar as consultas em espera</span><span class="sxs-lookup"><span data-stu-id="59538-146">Monitor waiting queries</span></span>
<span data-ttu-id="59538-147">Caso você descubra que sua consulta não está fazendo progresso porque está aguardando um recurso, veja a seguir uma consulta que mostra todos os recursos que uma consulta está aguardando.</span><span class="sxs-lookup"><span data-stu-id="59538-147">If you discover that your query is not making progress because it is waiting for a resource, here is a query that shows all the resources a query is waiting for.</span></span>

```sql
-- Find queries 
-- Replace request_id with value from Step 1.

SELECT waits.session_id,
      waits.request_id,  
      requests.command,
      requests.status,
      requests.start_time,  
      waits.type,
      waits.state,
      waits.object_type,
      waits.object_name
FROM   sys.dm_pdw_waits waits
   JOIN  sys.dm_pdw_exec_requests requests
   ON waits.request_id=requests.request_id
WHERE waits.request_id = 'QID####'
ORDER BY waits.object_name, waits.object_type, waits.state;
```

<span data-ttu-id="59538-148">Se a consulta estiver ativamente aguardando recursos de outra consulta, o estado será **AcquireResources**.</span><span class="sxs-lookup"><span data-stu-id="59538-148">If the query is actively waiting on resources from another query, then the state will be **AcquireResources**.</span></span>  <span data-ttu-id="59538-149">Se a consulta tiver todos os recursos necessários, o estado será **Concedido**.</span><span class="sxs-lookup"><span data-stu-id="59538-149">If the query has all the required resources, then the state will be **Granted**.</span></span>

## <a name="monitor-tempdb"></a><span data-ttu-id="59538-150">Monitorar o tempdb</span><span class="sxs-lookup"><span data-stu-id="59538-150">Monitor tempdb</span></span>
<span data-ttu-id="59538-151">A alta utilização do tempdb pode ser a causa raiz de problemas de desempenho lento e memória insuficiente.</span><span class="sxs-lookup"><span data-stu-id="59538-151">High tempdb utilization can be the root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="59538-152">Verifique primeiro se você tem rowgroups com distorção de dados ou de baixa qualidade e tome as medidas apropriadas.</span><span class="sxs-lookup"><span data-stu-id="59538-152">Please first check if you have data skew or poor quality rowgroups and take the appropriate actions.</span></span> <span data-ttu-id="59538-153">Considere a possibilidade de dimensionar o data warehouse se descobrir que o tempdb está atingindo seus limites durante a execução de consulta.</span><span class="sxs-lookup"><span data-stu-id="59538-153">Consider scaling your data warehouse if you find tempdb reaching its limits during query execution.</span></span> <span data-ttu-id="59538-154">A seguir, é descrito como identificar o uso do tempdb por consulta em cada nó.</span><span class="sxs-lookup"><span data-stu-id="59538-154">The following describes how to identify tempdb usage per query on each node.</span></span> 

<span data-ttu-id="59538-155">Crie a exibição a seguir para associar a ID do nó apropriado a sys.dm_pdw_sql_requests.</span><span class="sxs-lookup"><span data-stu-id="59538-155">Create the following view to associate the appropriate node id for sys.dm_pdw_sql_requests.</span></span> <span data-ttu-id="59538-156">Isso permitirá que você utilize outras DMVs de passagem e una essas tabelas a sys.dm_pdw_sql_requests.</span><span class="sxs-lookup"><span data-stu-id="59538-156">This will enable you to leverage other pass-through DMVs and join those tables with sys.dm_pdw_sql_requests.</span></span>

```sql
-- sys.dm_pdw_sql_requests with the correct node id
CREATE VIEW sql_requests AS
(SELECT
       sr.request_id,
       sr.step_index,
       (CASE 
              WHEN (sr.distribution_id = -1 ) THEN 
              (SELECT pdw_node_id FROM sys.dm_pdw_nodes WHERE type = 'CONTROL') 
              ELSE d.pdw_node_id END) AS pdw_node_id,
       sr.distribution_id,
       sr.status,
       sr.error_id,
       sr.start_time,
       sr.end_time,
       sr.total_elapsed_time,
       sr.row_count,
       sr.spid,
       sr.command
FROM sys.pdw_distributions AS d
RIGHT JOIN sys.dm_pdw_sql_requests AS sr ON d.distribution_id = sr.distribution_id)
```
<span data-ttu-id="59538-157">Execute a seguinte consulta para monitorar o tempdb:</span><span class="sxs-lookup"><span data-stu-id="59538-157">Run the following query to monitor tempdb:</span></span>

```sql
-- Monitor tempdb
SELECT
    sr.request_id,
    ssu.session_id,
    ssu.pdw_node_id,
    sr.command,
    sr.total_elapsed_time,
    es.login_name AS 'LoginName',
    DB_NAME(ssu.database_id) AS 'DatabaseName',
    (es.memory_usage * 8) AS 'MemoryUsage (in KB)',
    (ssu.user_objects_alloc_page_count * 8) AS 'Space Allocated For User Objects (in KB)',
    (ssu.user_objects_dealloc_page_count * 8) AS 'Space Deallocated For User Objects (in KB)',
    (ssu.internal_objects_alloc_page_count * 8) AS 'Space Allocated For Internal Objects (in KB)',
    (ssu.internal_objects_dealloc_page_count * 8) AS 'Space Deallocated For Internal Objects (in KB)',
    CASE es.is_user_process
    WHEN 1 THEN 'User Session'
    WHEN 0 THEN 'System Session'
    END AS 'SessionType',
    es.row_count AS 'RowCount'
FROM sys.dm_pdw_nodes_db_session_space_usage AS ssu
    INNER JOIN sys.dm_pdw_nodes_exec_sessions AS es ON ssu.session_id = es.session_id AND ssu.pdw_node_id = es.pdw_node_id
    INNER JOIN sys.dm_pdw_nodes_exec_connections AS er ON ssu.session_id = er.session_id AND ssu.pdw_node_id = er.pdw_node_id
    INNER JOIN sql_requests AS sr ON ssu.session_id = sr.spid AND ssu.pdw_node_id = sr.pdw_node_id
WHERE DB_NAME(ssu.database_id) = 'tempdb'
    AND es.session_id <> @@SPID
    AND es.login_name <> 'sa' 
ORDER BY sr.request_id;
```
## <a name="monitor-memory"></a><span data-ttu-id="59538-158">Monitorar a memória</span><span class="sxs-lookup"><span data-stu-id="59538-158">Monitor memory</span></span>

<span data-ttu-id="59538-159">A memória pode ser a causa raiz de problemas de desempenho lento e memória insuficiente.</span><span class="sxs-lookup"><span data-stu-id="59538-159">Memory can be the root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="59538-160">Verifique primeiro se você tem rowgroups com distorção de dados ou de baixa qualidade e tome as medidas apropriadas.</span><span class="sxs-lookup"><span data-stu-id="59538-160">Please first check if you have data skew or poor quality rowgroups and take the appropriate actions.</span></span> <span data-ttu-id="59538-161">Considere a possibilidade de dimensionar o data warehouse se descobrir que o uso de memória do SQL Server está atingindo seus limites durante a execução de consulta.</span><span class="sxs-lookup"><span data-stu-id="59538-161">Consider scaling your data warehouse if you find SQL Server memory usage reaching its limits during query execution.</span></span>

<span data-ttu-id="59538-162">A seguinte consulta retorna o uso e a demanda de memória do SQL Server por nó:</span><span class="sxs-lookup"><span data-stu-id="59538-162">The following query returns SQL Server memory usage and memory pressure per node:</span></span>   
```sql
-- Memory consumption
SELECT
  pc1.cntr_value as Curr_Mem_KB, 
  pc1.cntr_value/1024.0 as Curr_Mem_MB,
  (pc1.cntr_value/1048576.0) as Curr_Mem_GB,
  pc2.cntr_value as Max_Mem_KB,
  pc2.cntr_value/1024.0 as Max_Mem_MB,
  (pc2.cntr_value/1048576.0) as Max_Mem_GB,
  pc1.cntr_value * 100.0/pc2.cntr_value AS Memory_Utilization_Percentage,
  pc1.pdw_node_id
FROM
-- pc1: current memory
sys.dm_pdw_nodes_os_performance_counters AS pc1
-- pc2: total memory allowed for this SQL instance
JOIN sys.dm_pdw_nodes_os_performance_counters AS pc2 
ON pc1.object_name = pc2.object_name AND pc1.pdw_node_id = pc2.pdw_node_id
WHERE
pc1.counter_name = 'Total Server Memory (KB)'
AND pc2.counter_name = 'Target Server Memory (KB)'
```
## <a name="monitor-transaction-log-size"></a><span data-ttu-id="59538-163">Monitorar o tamanho do log de transações</span><span class="sxs-lookup"><span data-stu-id="59538-163">Monitor transaction log size</span></span>
<span data-ttu-id="59538-164">A consulta a seguir retorna o tamanho do log de transações em cada distribuição.</span><span class="sxs-lookup"><span data-stu-id="59538-164">The following query returns the transaction log size on each distribution.</span></span> <span data-ttu-id="59538-165">Verifique se você tem rowgroups com distorção de dados ou de baixa qualidade e tome as medidas apropriadas.</span><span class="sxs-lookup"><span data-stu-id="59538-165">Please check if you have data skew or poor quality rowgroups and take the appropriate actions.</span></span> <span data-ttu-id="59538-166">Se um dos arquivos de log estiver atingindo 160 GB, você deverá considerar a possibilidade de dimensionar a instância ou limitar o tamanho da transação.</span><span class="sxs-lookup"><span data-stu-id="59538-166">If one of the log files is reaching 160GB, you should consider scaling up your instance or limiting your transaction size.</span></span> 
```sql
-- Transaction log size
SELECT
  instance_name as distribution_db,
  cntr_value*1.0/1048576 as log_file_size_used_GB,
  pdw_node_id 
FROM sys.dm_pdw_nodes_os_performance_counters 
WHERE 
instance_name like 'Distribution_%' 
AND counter_name = 'Log File(s) Used Size (KB)'
AND counter_name = 'Target Server Memory (KB)'
```
## <a name="monitor-transaction-log-rollback"></a><span data-ttu-id="59538-167">Monitorar a reversão do log de transações</span><span class="sxs-lookup"><span data-stu-id="59538-167">Monitor transaction log rollback</span></span>
<span data-ttu-id="59538-168">Se as consultas estiverem falhando ou demorando muito para continuar, verifique e monitore se há transações sendo revertidas.</span><span class="sxs-lookup"><span data-stu-id="59538-168">If your queries are failing or taking a long time to proceed, you can check and monitor if you have any transactions rolling back.</span></span>
```sql
-- Monitor rollback
SELECT 
    SUM(CASE WHEN t.database_transaction_next_undo_lsn IS NOT NULL THEN 1 ELSE 0 END),
    t.pdw_node_id,
    nod.[type]
FROM sys.dm_pdw_nodes_tran_database_transactions t
JOIN sys.dm_pdw_nodes nod ON t.pdw_node_id = nod.pdw_node_id
GROUP BY t.pdw_node_id, nod.[type]
```

## <a name="next-steps"></a><span data-ttu-id="59538-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="59538-169">Next steps</span></span>
<span data-ttu-id="59538-170">Confira [Exibições do sistema][System views] para obter mais informações sobre DMVs.</span><span class="sxs-lookup"><span data-stu-id="59538-170">See [System views][System views] for more information on DMVs.</span></span>
<span data-ttu-id="59538-171">Consulte [Práticas Recomendadas do SQL Data Warehouse][SQL Data Warehouse best practices] para saber mais sobre as práticas recomendadas</span><span class="sxs-lookup"><span data-stu-id="59538-171">See [SQL Data Warehouse best practices][SQL Data Warehouse best practices] for more information about best practices</span></span>

<!--Image references-->

<!--Article references-->
[Manage overview]: ./sql-data-warehouse-overview-manage.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[System views]: ./sql-data-warehouse-reference-tsql-system-views.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Concurrency and workload management]: ./sql-data-warehouse-develop-concurrency.md
[Investigating queries waiting for resources]: ./sql-data-warehouse-manage-monitor.md#waiting

<!--MSDN references-->
[sys.dm_pdw_dms_workers]: http://msdn.microsoft.com/library/mt203878.aspx
[sys.dm_pdw_exec_requests]: http://msdn.microsoft.com/library/mt203887.aspx
[sys.dm_pdw_exec_sessions]: http://msdn.microsoft.com/library/mt203883.aspx
[sys.dm_pdw_request_steps]: http://msdn.microsoft.com/library/mt203913.aspx
[sys.dm_pdw_sql_requests]: http://msdn.microsoft.com/library/mt203889.aspx
[DBCC PDW_SHOWEXECUTIONPLAN]: http://msdn.microsoft.com/library/mt204017.aspx
[DBCC PDW_SHOWSPACEUSED]: http://msdn.microsoft.com/library/mt204028.aspx
[LABEL]: https://msdn.microsoft.com/library/ms190322.aspx
