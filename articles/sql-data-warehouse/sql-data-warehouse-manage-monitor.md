---
title: aaaMonitor sua carga de trabalho usando DMVs | Microsoft Docs
description: Saiba como toomonitor sua carga de trabalho usando DMVs.
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
ms.openlocfilehash: acccf952d165ccec3de3b4b1c633b18bbbf78077
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-workload-using-dmvs"></a><span data-ttu-id="82b62-103">Monitore sua carga de trabalho usando DMVs</span><span class="sxs-lookup"><span data-stu-id="82b62-103">Monitor your workload using DMVs</span></span>
<span data-ttu-id="82b62-104">Este artigo descreve como toouse exibições de gerenciamento dinâmico (DMVs) toomonitor sua carga de trabalho e investigar a execução de consulta no Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="82b62-104">This article describes how toouse Dynamic Management Views (DMVs) toomonitor your workload and investigate query execution in Azure SQL Data Warehouse.</span></span>

## <a name="permissions"></a><span data-ttu-id="82b62-105">Permissões</span><span class="sxs-lookup"><span data-stu-id="82b62-105">Permissions</span></span>
<span data-ttu-id="82b62-106">Olá tooquery DMVs neste artigo, você precisa de permissão VIEW DATABASE STATE ou controle.</span><span class="sxs-lookup"><span data-stu-id="82b62-106">tooquery hello DMVs in this article, you need either VIEW DATABASE STATE or CONTROL permission.</span></span> <span data-ttu-id="82b62-107">Conceder VIEW DATABASE STATE costuma permissão Olá preferido porque é muito mais restritivo.</span><span class="sxs-lookup"><span data-stu-id="82b62-107">Usually granting VIEW DATABASE STATE is hello preferred permission as it is much more restrictive.</span></span>

```sql
GRANT VIEW DATABASE STATE toomyuser;
```

## <a name="monitor-connections"></a><span data-ttu-id="82b62-108">Conexões do monitor</span><span class="sxs-lookup"><span data-stu-id="82b62-108">Monitor connections</span></span>
<span data-ttu-id="82b62-109">Todos os logons tooSQL Data Warehouse são registrados em log muito[sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span><span class="sxs-lookup"><span data-stu-id="82b62-109">All logins tooSQL Data Warehouse are logged too[sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span></span>  <span data-ttu-id="82b62-110">Essa DMV contém Olá última 10.000 logons.</span><span class="sxs-lookup"><span data-stu-id="82b62-110">This DMV contains hello last 10,000 logins.</span></span>  <span data-ttu-id="82b62-111">Olá session_id é a chave primária hello e é atribuído em sequência para cada novo logon.</span><span class="sxs-lookup"><span data-stu-id="82b62-111">hello session_id is hello primary key and is assigned sequentially for each new logon.</span></span>

```sql
-- Other Active Connections
SELECT * FROM sys.dm_pdw_exec_sessions where status <> 'Closed' and session_id <> session_id();
```

## <a name="monitor-query-execution"></a><span data-ttu-id="82b62-112">Monitorar a execução de consultas</span><span class="sxs-lookup"><span data-stu-id="82b62-112">Monitor query execution</span></span>
<span data-ttu-id="82b62-113">Todas as consultas executadas no SQL Data Warehouse são registradas muito[sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span><span class="sxs-lookup"><span data-stu-id="82b62-113">All queries executed on SQL Data Warehouse are logged too[sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span></span>  <span data-ttu-id="82b62-114">Essa DMV contém Olá última 10.000 consultas executadas.</span><span class="sxs-lookup"><span data-stu-id="82b62-114">This DMV contains hello last 10,000 queries executed.</span></span>  <span data-ttu-id="82b62-115">Olá request_id identifica cada consulta exclusivamente e é a chave primária Olá para esse DMV.</span><span class="sxs-lookup"><span data-stu-id="82b62-115">hello request_id uniquely identifies each query and is hello primary key for this DMV.</span></span>  <span data-ttu-id="82b62-116">Olá request_id é atribuído em sequência para cada nova consulta e é prefixado com QID, que representa o ID da consulta.</span><span class="sxs-lookup"><span data-stu-id="82b62-116">hello request_id is assigned sequentially for each new query and is prefixed with QID, which stands for query ID.</span></span>  <span data-ttu-id="82b62-117">A consulta a esta DMV para uma determinada session_id mostra todas as consultas para um logon específico.</span><span class="sxs-lookup"><span data-stu-id="82b62-117">Querying this DMV for a given session_id shows all queries for a given logon.</span></span>

> [!NOTE]
> <span data-ttu-id="82b62-118">Os procedimentos armazenados usam vários request_ids.</span><span class="sxs-lookup"><span data-stu-id="82b62-118">Stored procedures use multiple Request IDs.</span></span>  <span data-ttu-id="82b62-119">As IDs de solicitação são atribuídas em ordem sequencial.</span><span class="sxs-lookup"><span data-stu-id="82b62-119">Request IDs are assigned in sequential order.</span></span> 
> 
> 

<span data-ttu-id="82b62-120">Aqui estão as etapas toofollow tooinvestigate planos de execução e horários para uma consulta específica.</span><span class="sxs-lookup"><span data-stu-id="82b62-120">Here are steps toofollow tooinvestigate query execution plans and times for a particular query.</span></span>

### <a name="step-1-identify-hello-query-you-wish-tooinvestigate"></a><span data-ttu-id="82b62-121">Etapa 1: Identificar consulta Olá que desejar tooinvestigate</span><span class="sxs-lookup"><span data-stu-id="82b62-121">STEP 1: Identify hello query you wish tooinvestigate</span></span>
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

-- Find a query with hello Label 'My Query'
-- Use brackets when querying hello label column, as it it a key word
SELECT  *
FROM    sys.dm_pdw_exec_requests
WHERE   [label] = 'My Query';
```

<span data-ttu-id="82b62-122">De saudação anterior de resultados da consulta, **Olá Observação ID da solicitação** de consulta Olá que deseja tooinvestigate.</span><span class="sxs-lookup"><span data-stu-id="82b62-122">From hello preceding query results, **note hello Request ID** of hello query that you would like tooinvestigate.</span></span>

<span data-ttu-id="82b62-123">Consultas em Olá **suspenso** estado está sendo enfileirada devido a limites de tooconcurrency.</span><span class="sxs-lookup"><span data-stu-id="82b62-123">Queries in hello **Suspended** state are being queued due tooconcurrency limits.</span></span> <span data-ttu-id="82b62-124">Essas consultas também aparecem em Olá sys.dm_pdw_waits esperas de consulta com um tipo de UserConcurrencyResourceType.</span><span class="sxs-lookup"><span data-stu-id="82b62-124">These queries also appear in hello sys.dm_pdw_waits waits query with a type of UserConcurrencyResourceType.</span></span> <span data-ttu-id="82b62-125">Confira [Concurrency and workload management][Concurrency and workload management] (Gerenciamento de simultaneidade e carga de trabalho) para obter mais detalhes sobre os limites de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="82b62-125">See [Concurrency and workload management][Concurrency and workload management] for more details on concurrency limits.</span></span> <span data-ttu-id="82b62-126">As consultas também podem esperar por motivos, como bloqueios.</span><span class="sxs-lookup"><span data-stu-id="82b62-126">Queries can also wait for other reasons such as for object locks.</span></span>  <span data-ttu-id="82b62-127">Se sua consulta estiver aguardando um recurso, confira [Investigar consultas aguardando recursos][Investigating queries waiting for resources] mais adiante neste artigo.</span><span class="sxs-lookup"><span data-stu-id="82b62-127">If your query is waiting for a resource, see [Investigating queries waiting for resources][Investigating queries waiting for resources] further down in this article.</span></span>

<span data-ttu-id="82b62-128">pesquisa de saudação toosimplify de uma consulta na tabela de sys.dm_pdw_exec_requests hello, use [rótulo] [ LABEL] tooassign uma consulta de tooyour de comentário que pode ser pesquisada no modo de exibição de sys.dm_pdw_exec_requests hello.</span><span class="sxs-lookup"><span data-stu-id="82b62-128">toosimplify hello lookup of a query in hello sys.dm_pdw_exec_requests table, use [LABEL][LABEL] tooassign a comment tooyour query that can be looked up in hello sys.dm_pdw_exec_requests view.</span></span>

```sql
-- Query with Label
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query')
;
```

### <a name="step-2-investigate-hello-query-plan"></a><span data-ttu-id="82b62-129">Etapa 2: Investigar o plano de consulta Olá</span><span class="sxs-lookup"><span data-stu-id="82b62-129">STEP 2: Investigate hello query plan</span></span>
<span data-ttu-id="82b62-130">Usar plano de SQL (DSQL) distribuído da consulta do hello ID da solicitação tooretrieve saudação de [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span><span class="sxs-lookup"><span data-stu-id="82b62-130">Use hello Request ID tooretrieve hello query's distributed SQL (DSQL) plan from [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span></span>

```sql
-- Find hello distributed query plan steps for a specific query.
-- Replace request_id with value from Step 1.

SELECT * FROM sys.dm_pdw_request_steps
WHERE request_id = 'QID####'
ORDER BY step_index;
```

<span data-ttu-id="82b62-131">Quando um plano DSQL está demorando mais do que o esperado, causa Olá pode ser um plano complexo com muitas etapas DSQL ou apenas uma etapa levando muito tempo.</span><span class="sxs-lookup"><span data-stu-id="82b62-131">When a DSQL plan is taking longer than expected, hello cause can be a complex plan with many DSQL steps or just one step taking a long time.</span></span>  <span data-ttu-id="82b62-132">Se o plano de saudação for muitas etapas com várias operações de movimentação, considere a otimizar o movimento de dados tabela distribuições tooreduce.</span><span class="sxs-lookup"><span data-stu-id="82b62-132">If hello plan is many steps with several move operations, consider optimizing your table distributions tooreduce data movement.</span></span> <span data-ttu-id="82b62-133">Olá [distribuição da tabela] [ Table distribution] artigo explica por que os dados devem ser movido toosolve uma consulta e explica algumas movimentação de dados de toominimize de estratégias de distribuição.</span><span class="sxs-lookup"><span data-stu-id="82b62-133">hello [Table distribution][Table distribution] article explains why data must be moved toosolve a query and explains some distribution strategies toominimize data movement.</span></span>

<span data-ttu-id="82b62-134">tooinvestigate obter mais detalhes sobre uma única etapa, hello *operation_type* coluna da saudação de etapa e Observação de consulta longa Olá **índice de etapa**:</span><span class="sxs-lookup"><span data-stu-id="82b62-134">tooinvestigate further details about a single step, hello *operation_type* column of hello long-running query step and note hello **Step Index**:</span></span>

* <span data-ttu-id="82b62-135">Continue com a Etapa 3a para **Operações SQL**: OnOperation, RemoteOperation, ReturnOperation.</span><span class="sxs-lookup"><span data-stu-id="82b62-135">Proceed with Step 3a for **SQL operations**: OnOperation, RemoteOperation, ReturnOperation.</span></span>
* <span data-ttu-id="82b62-136">Continue com a Etapa 3b para **Operações de movimentação de dados**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span><span class="sxs-lookup"><span data-stu-id="82b62-136">Proceed with Step 3b for **Data Movement operations**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span></span>

### <a name="step-3a-investigate-sql-on-hello-distributed-databases"></a><span data-ttu-id="82b62-137">ETAPA 3a: investigar SQL nos bancos de dados distribuído de saudação</span><span class="sxs-lookup"><span data-stu-id="82b62-137">STEP 3a: Investigate SQL on hello distributed databases</span></span>
<span data-ttu-id="82b62-138">Use hello ID da solicitação e detalhes de tooretrieve de índice de etapa de saudação do [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], que contém informações de execução da etapa de consulta Olá em todos os Olá distribuídas bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="82b62-138">Use hello Request ID and hello Step Index tooretrieve details from [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], which contains execution information of hello query step on all of hello distributed databases.</span></span>

```sql
-- Find hello distribution run times for a SQL step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_sql_requests
WHERE request_id = 'QID####' AND step_index = 2;
```

<span data-ttu-id="82b62-139">Quando estiver executando a etapa de consulta hello, [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] pode ser o plano estimado do tooretrieve usado saudação do SQL Server da saudação cache de plano do SQL Server para a etapa de saudação em execução em um determinado distribuição.</span><span class="sxs-lookup"><span data-stu-id="82b62-139">When hello query step is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used tooretrieve hello SQL Server estimated plan from hello SQL Server plan cache for hello step running on a particular distribution.</span></span>

```sql
-- Find hello SQL Server execution plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(1, 78);
```

### <a name="step-3b-investigate-data-movement-on-hello-distributed-databases"></a><span data-ttu-id="82b62-140">ETAPA 3b: investigar a movimentação de dados em bancos de dados distribuído de saudação</span><span class="sxs-lookup"><span data-stu-id="82b62-140">STEP 3b: Investigate data movement on hello distributed databases</span></span>
<span data-ttu-id="82b62-141">Use Olá ID da solicitação e hello informações do índice de etapa tooretrieve sobre uma etapa de movimentação de dados em execução em cada distribuição [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span><span class="sxs-lookup"><span data-stu-id="82b62-141">Use hello Request ID and hello Step Index tooretrieve information about a data movement step running on each distribution from [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span></span>

```sql
-- Find hello information about all hello workers completing a Data Movement Step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_dms_workers
WHERE request_id = 'QID####' AND step_index = 2;
```

* <span data-ttu-id="82b62-142">Verificar Olá *total_elapsed_time* toosee coluna se uma distribuição específica está demorando significativamente mais do que outras pessoas para movimentação de dados.</span><span class="sxs-lookup"><span data-stu-id="82b62-142">Check hello *total_elapsed_time* column toosee if a particular distribution is taking significantly longer than others for data movement.</span></span>
* <span data-ttu-id="82b62-143">Para distribuição de longa execução hello, verifique Olá *rows_processed* toosee coluna se o número de saudação de linhas sendo movido dessa distribuição é significativamente maior do que outras pessoas.</span><span class="sxs-lookup"><span data-stu-id="82b62-143">For hello long-running distribution, check hello *rows_processed* column toosee if hello number of rows being moved from that distribution is significantly larger than others.</span></span> <span data-ttu-id="82b62-144">Se for o caso, isso poderá indicar distorção de dados subjacentes.</span><span class="sxs-lookup"><span data-stu-id="82b62-144">If so, this may indicate skew of your underlying data.</span></span>

<span data-ttu-id="82b62-145">Se estiver executando a consulta hello, [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] pode ser o plano estimado do tooretrieve usado saudação do SQL Server da saudação cache de planos do SQL Server para Olá atualmente em execução SQL etapa dentro de um determinado distribuição.</span><span class="sxs-lookup"><span data-stu-id="82b62-145">If hello query is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used tooretrieve hello SQL Server estimated plan from hello SQL Server plan cache for hello currently running SQL Step within a particular distribution.</span></span>

```sql
-- Find hello SQL Server estimated plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(55, 238);
```

<a name="waiting"></a>

## <a name="monitor-waiting-queries"></a><span data-ttu-id="82b62-146">Monitorar as consultas em espera</span><span class="sxs-lookup"><span data-stu-id="82b62-146">Monitor waiting queries</span></span>
<span data-ttu-id="82b62-147">Se você descobrir que sua consulta não está progredindo porque ele está aguardando um recurso, aqui está uma consulta que mostra todos os recursos de saudação que está aguardando que uma consulta.</span><span class="sxs-lookup"><span data-stu-id="82b62-147">If you discover that your query is not making progress because it is waiting for a resource, here is a query that shows all hello resources a query is waiting for.</span></span>

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

<span data-ttu-id="82b62-148">Se consulta Olá ativamente está esperando em recursos de outra consulta, Olá estado será **AcquireResources**.</span><span class="sxs-lookup"><span data-stu-id="82b62-148">If hello query is actively waiting on resources from another query, then hello state will be **AcquireResources**.</span></span>  <span data-ttu-id="82b62-149">Se consulta Olá tem todos os recursos necessários de saudação, Olá estado será **concedido**.</span><span class="sxs-lookup"><span data-stu-id="82b62-149">If hello query has all hello required resources, then hello state will be **Granted**.</span></span>

## <a name="monitor-tempdb"></a><span data-ttu-id="82b62-150">Monitorar o tempdb</span><span class="sxs-lookup"><span data-stu-id="82b62-150">Monitor tempdb</span></span>
<span data-ttu-id="82b62-151">Tempdb alta utilização pode ser a causa raiz de saudação para um desempenho lento e problemas de memória insuficiente.</span><span class="sxs-lookup"><span data-stu-id="82b62-151">High tempdb utilization can be hello root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="82b62-152">Verifique se você tiver rowgroups de distorção ou de baixa qualidade de dados e executar as ações apropriadas Olá primeiro.</span><span class="sxs-lookup"><span data-stu-id="82b62-152">Please first check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="82b62-153">Considere a possibilidade de dimensionar o data warehouse se descobrir que o tempdb está atingindo seus limites durante a execução de consulta.</span><span class="sxs-lookup"><span data-stu-id="82b62-153">Consider scaling your data warehouse if you find tempdb reaching its limits during query execution.</span></span> <span data-ttu-id="82b62-154">Olá a seguir descrevem como uso de tempdb tooidentify por consulta em cada nó.</span><span class="sxs-lookup"><span data-stu-id="82b62-154">hello following describes how tooidentify tempdb usage per query on each node.</span></span> 

<span data-ttu-id="82b62-155">Crie hello id da seguinte exibição tooassociate Olá nó apropriado para sys.dm_pdw_sql_requests.</span><span class="sxs-lookup"><span data-stu-id="82b62-155">Create hello following view tooassociate hello appropriate node id for sys.dm_pdw_sql_requests.</span></span> <span data-ttu-id="82b62-156">Isso habilitará você tooleverage outros DMVs de passagem e unir essas tabelas com sys.dm_pdw_sql_requests.</span><span class="sxs-lookup"><span data-stu-id="82b62-156">This will enable you tooleverage other pass-through DMVs and join those tables with sys.dm_pdw_sql_requests.</span></span>

```sql
-- sys.dm_pdw_sql_requests with hello correct node id
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
<span data-ttu-id="82b62-157">Execute Olá tempdb de toomonitor de consulta a seguir:</span><span class="sxs-lookup"><span data-stu-id="82b62-157">Run hello following query toomonitor tempdb:</span></span>

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
## <a name="monitor-memory"></a><span data-ttu-id="82b62-158">Monitorar a memória</span><span class="sxs-lookup"><span data-stu-id="82b62-158">Monitor memory</span></span>

<span data-ttu-id="82b62-159">Memória pode ser a causa raiz de saudação para um desempenho lento e problemas de memória insuficiente.</span><span class="sxs-lookup"><span data-stu-id="82b62-159">Memory can be hello root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="82b62-160">Verifique se você tiver rowgroups de distorção ou de baixa qualidade de dados e executar as ações apropriadas Olá primeiro.</span><span class="sxs-lookup"><span data-stu-id="82b62-160">Please first check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="82b62-161">Considere a possibilidade de dimensionar o data warehouse se descobrir que o uso de memória do SQL Server está atingindo seus limites durante a execução de consulta.</span><span class="sxs-lookup"><span data-stu-id="82b62-161">Consider scaling your data warehouse if you find SQL Server memory usage reaching its limits during query execution.</span></span>

<span data-ttu-id="82b62-162">saudação de consulta a seguir retorna a pressão de memória e uso de memória de SQL Server por nó:</span><span class="sxs-lookup"><span data-stu-id="82b62-162">hello following query returns SQL Server memory usage and memory pressure per node:</span></span> 
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
## <a name="monitor-transaction-log-size"></a><span data-ttu-id="82b62-163">Monitorar o tamanho do log de transações</span><span class="sxs-lookup"><span data-stu-id="82b62-163">Monitor transaction log size</span></span>
<span data-ttu-id="82b62-164">Olá consulta a seguir retorna o tamanho de log de transações Olá em cada distribuição.</span><span class="sxs-lookup"><span data-stu-id="82b62-164">hello following query returns hello transaction log size on each distribution.</span></span> <span data-ttu-id="82b62-165">Verifique se você tiver rowgroups de distorção ou de baixa qualidade de dados e executar as ações apropriadas hello.</span><span class="sxs-lookup"><span data-stu-id="82b62-165">Please check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="82b62-166">Se um dos arquivos de log hello está atingindo 160GB, você deve considerar o dimensionamento de sua instância ou limitando o tamanho da transação.</span><span class="sxs-lookup"><span data-stu-id="82b62-166">If one of hello log files is reaching 160GB, you should consider scaling up your instance or limiting your transaction size.</span></span> 
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
## <a name="monitor-transaction-log-rollback"></a><span data-ttu-id="82b62-167">Monitorar a reversão do log de transações</span><span class="sxs-lookup"><span data-stu-id="82b62-167">Monitor transaction log rollback</span></span>
<span data-ttu-id="82b62-168">Se suas consultas estão falhando ou colocar um tooproceed muito tempo, você pode verificar e monitorar se houver transações reversão.</span><span class="sxs-lookup"><span data-stu-id="82b62-168">If your queries are failing or taking a long time tooproceed, you can check and monitor if you have any transactions rolling back.</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="82b62-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="82b62-169">Next steps</span></span>
<span data-ttu-id="82b62-170">Confira [Exibições do sistema][System views] para obter mais informações sobre DMVs.</span><span class="sxs-lookup"><span data-stu-id="82b62-170">See [System views][System views] for more information on DMVs.</span></span>
<span data-ttu-id="82b62-171">Consulte [Práticas Recomendadas do SQL Data Warehouse][SQL Data Warehouse best practices] para saber mais sobre as práticas recomendadas</span><span class="sxs-lookup"><span data-stu-id="82b62-171">See [SQL Data Warehouse best practices][SQL Data Warehouse best practices] for more information about best practices</span></span>

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
