---
title: "aaaManage dados históricos em tabelas temporais com a política de retenção | Microsoft Docs"
description: "Saiba como toouse retenção temporal política tookeep dados históricos sob seu controle."
services: sql-database
documentationcenter: 
author: bonova
manager: drasumic
editor: 
ms.assetid: 76cfa06a-e758-453e-942c-9f1ed6a38c2a
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 10/12/2016
ms.author: bonova
ms.openlocfilehash: a72a6111a6cd7322d734d08bf3852e95f5ffea8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-historical-data-in-temporal-tables-with-retention-policy"></a><span data-ttu-id="9b29d-103">Gerenciar dados históricos em Tabelas Temporais com a política de retenção</span><span class="sxs-lookup"><span data-stu-id="9b29d-103">Manage historical data in Temporal Tables with retention policy</span></span>
<span data-ttu-id="9b29d-104">Tabelas Temporais podem aumentar o tamanho do banco de dados mais do que tabelas regulares, especialmente se você mantiver os dados históricos por um período maior de tempo.</span><span class="sxs-lookup"><span data-stu-id="9b29d-104">Temporal Tables may increase database size more than regular tables, especially if you retain historical data for a longer period of time.</span></span> <span data-ttu-id="9b29d-105">Portanto, a política de retenção para dados históricos é um aspecto importante do planejamento e gerenciamento do ciclo de vida de saudação de cada tabela temporal.</span><span class="sxs-lookup"><span data-stu-id="9b29d-105">Hence, retention policy for historical data is an important aspect of planning and managing hello lifecycle of every temporal table.</span></span> <span data-ttu-id="9b29d-106">Tabelas temporais no Banco de Dados SQL do Azure vem com um mecanismo de retenção de fácil utilização que ajuda você a realizar essa tarefa.</span><span class="sxs-lookup"><span data-stu-id="9b29d-106">Temporal Tables in Azure SQL Database come with easy-to-use retention mechanism that helps you accomplish this task.</span></span>

<span data-ttu-id="9b29d-107">Retenção de histórico temporal pode ser configurada no nível de tabela individual hello, que permite aos usuários as diretivas de vencimento flexível toocreate.</span><span class="sxs-lookup"><span data-stu-id="9b29d-107">Temporal history retention can be configured at hello individual table level, which allows users toocreate flexible aging polices.</span></span> <span data-ttu-id="9b29d-108">A aplicação de retenção temporal é simple: requer apenas um toobe parâmetro definido durante a alteração de esquema ou criação de tabela.</span><span class="sxs-lookup"><span data-stu-id="9b29d-108">Applying temporal retention is simple: it requires only one parameter toobe set during table creation or schema change.</span></span>

<span data-ttu-id="9b29d-109">Após você definir a política de retenção, o Banco de Dados SQL do Azure começa a verificar regularmente se há linhas de histórico qualificadas para limpeza automática de dados.</span><span class="sxs-lookup"><span data-stu-id="9b29d-109">After you define retention policy, Azure SQL Database starts checking regularly if there are historical rows that are eligible for automatic data cleanup.</span></span> <span data-ttu-id="9b29d-110">Identificação de linhas correspondentes e sua remoção da tabela de histórico de saudação ocorrem de modo transparente, na tarefa de plano de fundo Olá que é programada e executada pelo sistema hello.</span><span class="sxs-lookup"><span data-stu-id="9b29d-110">Identification of matching rows and their removal from hello history table occur transparently, in hello background task that is scheduled and run by hello system.</span></span> <span data-ttu-id="9b29d-111">Condição de idade para linhas de tabela de histórico de saudação é verificada com base na coluna de saudação que representa o final do período SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="9b29d-111">Age condition for hello history table rows is checked based on hello column representing end of SYSTEM_TIME period.</span></span> <span data-ttu-id="9b29d-112">Se o período de retenção, por exemplo, é definir toosix em meses, linhas de tabela qualificadas para limpeza satisfazem Olá condição a seguir:</span><span class="sxs-lookup"><span data-stu-id="9b29d-112">If retention period, for example, is set toosix months, table rows eligible for cleanup satisfy hello following condition:</span></span>

````
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
````

<span data-ttu-id="9b29d-113">Em Olá anterior de exemplo, presumimos que **ValidTo** coluna corresponde toohello final do período SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="9b29d-113">In hello preceding example, we assumed that **ValidTo** column corresponds toohello end of SYSTEM_TIME period.</span></span>

## <a name="how-tooconfigure-retention-policy"></a><span data-ttu-id="9b29d-114">Como política de retenção tooconfigure?</span><span class="sxs-lookup"><span data-stu-id="9b29d-114">How tooconfigure retention policy?</span></span>
<span data-ttu-id="9b29d-115">Antes de configurar a política de retenção para uma tabela temporal, verifique primeiro se a retenção de histórico temporal está habilitada *no nível de banco de dados de saudação*.</span><span class="sxs-lookup"><span data-stu-id="9b29d-115">Before you configure retention policy for a temporal table, check first whether temporal historical retention is enabled *at hello database level*.</span></span>

````
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
````

<span data-ttu-id="9b29d-116">Sinalizador de banco de dados **is_temporal_history_retention_enabled** é tooON conjunto por padrão, mas os usuários podem alterá-la com a instrução ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="9b29d-116">Database flag **is_temporal_history_retention_enabled** is set tooON by default, but users can change it with ALTER DATABASE statement.</span></span> <span data-ttu-id="9b29d-117">É também automaticamente conjunto tooOFF após [restauração pontual](sql-database-recovery-using-backups.md) operação.</span><span class="sxs-lookup"><span data-stu-id="9b29d-117">It is also automatically set tooOFF after [point in time restore](sql-database-recovery-using-backups.md) operation.</span></span> <span data-ttu-id="9b29d-118">Limpeza de retenção de histórico temporal tooenable para seu banco de dados, execute Olá instrução a seguir:</span><span class="sxs-lookup"><span data-stu-id="9b29d-118">tooenable temporal history retention cleanup for your database, execute hello following statement:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

> [!IMPORTANT]
> <span data-ttu-id="9b29d-119">Será possível configurar a retenção para tabelas temporais mesmo se **is_temporal_history_retention_enabled** estiver DESATIVADO, mas a limpeza automática de linhas antigas não será disparada nesse caso.</span><span class="sxs-lookup"><span data-stu-id="9b29d-119">You can configure retention for temporal tables even if **is_temporal_history_retention_enabled** is OFF, but automatic cleanup for aged rows is not triggered in that case.</span></span>
> 
> 

<span data-ttu-id="9b29d-120">Política de retenção é configurada durante a criação de uma tabela especificando o valor do parâmetro HISTORY_RETENTION_PERIOD hello:</span><span class="sxs-lookup"><span data-stu-id="9b29d-120">Retention policy is configured during table creation by specifying value for hello HISTORY_RETENTION_PERIOD parameter:</span></span>

````
CREATE TABLE dbo.WebsiteUserInfo
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH
 (
     SYSTEM_VERSIONING = ON
     (
        HISTORY_TABLE = dbo.WebsiteUserInfoHistory,
        HISTORY_RETENTION_PERIOD = 6 MONTHS
     )
 );
````

<span data-ttu-id="9b29d-121">Banco de dados SQL do Azure permite o período de retenção toospecify usando unidades de tempo diferentes: dias, semanas, meses e anos.</span><span class="sxs-lookup"><span data-stu-id="9b29d-121">Azure SQL Database allows you toospecify retention period by using different time units: DAYS, WEEKS, MONTHS, and YEARS.</span></span> <span data-ttu-id="9b29d-122">Se HISTORY_RETENTION_PERIOD for omitido, supõe-se que retenção é INFINITO.</span><span class="sxs-lookup"><span data-stu-id="9b29d-122">If HISTORY_RETENTION_PERIOD is omitted, INFINITE retention is assumed.</span></span> <span data-ttu-id="9b29d-123">Você também pode usar palavra-chave INFINITO explicitamente.</span><span class="sxs-lookup"><span data-stu-id="9b29d-123">You can also use INFINITE keyword explicitly.</span></span>

<span data-ttu-id="9b29d-124">Em alguns cenários, talvez você queira tooconfigure retenção após a criação de tabela ou toochange valor configurado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9b29d-124">In some scenarios, you may want tooconfigure retention after table creation, or toochange previously configured value.</span></span> <span data-ttu-id="9b29d-125">Nesse caso, use a instrução ALTER TABLE:</span><span class="sxs-lookup"><span data-stu-id="9b29d-125">In that case use ALTER TABLE statement:</span></span>

````
ALTER TABLE dbo.WebsiteUserInfo
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 9 MONTHS));
````

> [!IMPORTANT]
> <span data-ttu-id="9b29d-126">Definir SYSTEM_VERSIONING tooOFF *não preserva* valor do período de retenção.</span><span class="sxs-lookup"><span data-stu-id="9b29d-126">Setting SYSTEM_VERSIONING tooOFF *does not preserve* retention period value.</span></span> <span data-ttu-id="9b29d-127">Definir SYSTEM_VERSIONING tooON sem HISTORY_RETENTION_PERIOD explicitamente especificada resulta no período de retenção infinito hello.</span><span class="sxs-lookup"><span data-stu-id="9b29d-127">Setting SYSTEM_VERSIONING tooON without HISTORY_RETENTION_PERIOD specified explicitly results in hello INFINITE retention period.</span></span>
> 
> 

<span data-ttu-id="9b29d-128">tooreview o estado atual da política de retenção hello, esse sinalizador de habilitação de retenção temporal junções em nível de banco de dados de saudação com períodos de retenção para tabelas individuais consulta a seguir de saudação de uso:</span><span class="sxs-lookup"><span data-stu-id="9b29d-128">tooreview current state of hello retention policy, use hello following query that joins temporal retention enablement flag at hello database level with retention periods for individual tables:</span></span>

````
SELECT DB.is_temporal_history_retention_enabled,
SCHEMA_NAME(T1.schema_id) AS TemporalTableSchema,
T1.name as TemporalTableName,  SCHEMA_NAME(T2.schema_id) AS HistoryTableSchema,
T2.name as HistoryTableName,T1.history_retention_period,
T1.history_retention_period_unit_desc
FROM sys.tables T1  
OUTER APPLY (select is_temporal_history_retention_enabled from sys.databases
where name = DB_NAME()) AS DB
LEFT JOIN sys.tables T2   
ON T1.history_table_id = T2.object_id WHERE T1.temporal_type = 2
````


## <a name="how-sql-database-deletes-aged-rows"></a><span data-ttu-id="9b29d-129">Como o Banco de Dados SQL exclui linhas antigas?</span><span class="sxs-lookup"><span data-stu-id="9b29d-129">How SQL Database deletes aged rows?</span></span>
<span data-ttu-id="9b29d-130">o processo de limpeza Olá depende do layout de índice Olá Olá da tabela de histórico.</span><span class="sxs-lookup"><span data-stu-id="9b29d-130">hello cleanup process depends on hello index layout of hello history table.</span></span> <span data-ttu-id="9b29d-131">É importante toonotice que *somente tabelas de histórico com um índice clusterizado (árvore B ou columnstore) podem ter uma política de retenção finito configurada*.</span><span class="sxs-lookup"><span data-stu-id="9b29d-131">It is important toonotice that *only history tables with a clustered index (B-tree or columnstore) can have finite retention policy configured*.</span></span> <span data-ttu-id="9b29d-132">Uma tarefa em segundo plano é criada tooperform a limpeza de dados antigos de todas as tabelas temporais com período de retenção finito.</span><span class="sxs-lookup"><span data-stu-id="9b29d-132">A background task is created tooperform aged data cleanup for all temporal tables with finite retention period.</span></span>
<span data-ttu-id="9b29d-133">Lógica de limpeza para o índice clusterizado do hello rowstore (árvore B) exclui a linha antigo em partes menores (até too10K) minimizando a pressão no log do banco de dados e o subsistema de e/s.</span><span class="sxs-lookup"><span data-stu-id="9b29d-133">Cleanup logic for hello rowstore (B-tree) clustered index deletes aged row in smaller chunks (up too10K) minimizing pressure on database log and I/O subsystem.</span></span> <span data-ttu-id="9b29d-134">Embora utiliza a lógica de limpeza necessárias índice de árvore B, a ordem de exclusões para linhas de saudação mais antigas que o período de retenção não pode ser garantido firmemente.</span><span class="sxs-lookup"><span data-stu-id="9b29d-134">Although cleanup logic utilizes required B-tree index, order of deletions for hello rows older than retention period cannot be firmly guaranteed.</span></span> <span data-ttu-id="9b29d-135">Portanto, *não terão qualquer dependência em ordem de limpeza de saudação em seus aplicativos*.</span><span class="sxs-lookup"><span data-stu-id="9b29d-135">Hence, *do not take any dependency on hello cleanup order in your applications*.</span></span>

<span data-ttu-id="9b29d-136">Olá a tarefa de limpeza para Olá clusterizada columnstore remove todo [grupos de linhas](https://msdn.microsoft.com/library/gg492088.aspx) uma vez (normalmente contém 1 milhão de linhas cada), que é muito eficiente, especialmente quando os dados históricos são gerados em uma alta velocidade.</span><span class="sxs-lookup"><span data-stu-id="9b29d-136">hello cleanup task for hello clustered columnstore removes entire [row groups](https://msdn.microsoft.com/library/gg492088.aspx) at once (typically contain 1 million of rows each), which is very efficient, especially when historical data is generated at a high pace.</span></span>

![Retenção de columnstore clusterizado](./media/sql-database-temporal-tables-retention-policy/cciretention.png)

<span data-ttu-id="9b29d-138">A excelente compactação de dados e a eficiente limpeza retenção tornam o índice columnstore clusterizado uma opção perfeita para cenários em que sua carga de trabalho gera rapidamente uma grande quantidade de dados históricos.</span><span class="sxs-lookup"><span data-stu-id="9b29d-138">Excellent data compression and efficient retention cleanup makes clustered columnstore index a perfect choice for scenarios when your workload rapidly generates high amount of historical data.</span></span> <span data-ttu-id="9b29d-139">Esse padrão é típico para o [cargas de trabalho de processamento transacional intensas que usam tabelas temporais](https://msdn.microsoft.com/library/mt631669.aspx) para controle de alterações e auditoria, análise de tendências ou ingestão de dados de IoT.</span><span class="sxs-lookup"><span data-stu-id="9b29d-139">That pattern is typical for intensive [transactional processing workloads that use temporal tables](https://msdn.microsoft.com/library/mt631669.aspx) for change tracking and auditing, trend analysis, or IoT data ingestion.</span></span>

## <a name="index-considerations"></a><span data-ttu-id="9b29d-140">Considerações de índice</span><span class="sxs-lookup"><span data-stu-id="9b29d-140">Index considerations</span></span>
<span data-ttu-id="9b29d-141">a tarefa de limpeza Olá para tabelas com índice clusterizado rowstore requer toostart de índice com o hello coluna correspondente Olá final do período SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="9b29d-141">hello cleanup task for tables with rowstore clustered index requires index toostart with hello column corresponding hello end of SYSTEM_TIME period.</span></span> <span data-ttu-id="9b29d-142">Se esse índice não existir, você não poderá configurar o período de retenção finito:</span><span class="sxs-lookup"><span data-stu-id="9b29d-142">If such index doesn't exist, you cannot configure a finite retention period:</span></span>

<span data-ttu-id="9b29d-143">*Msg 13765, nível 16, estado 1 <br> </br> definir período de retenção finito falhou na tabela temporal com versão do sistema 'temporalstagetestdb.dbo.WebsiteUserInfo' como tabela de histórico de saudação ' temporalstagetestdb.dbo.WebsiteUserInfoHistory' não contém o índice clusterizado necessário. Considere a criação de uma columnstore clusterizada ou o índice de árvore B começando com a coluna de saudação que corresponde a fim de SYSTEM_TIME period na tabela de histórico de saudação.*</span><span class="sxs-lookup"><span data-stu-id="9b29d-143">*Msg 13765, Level 16, State 1 <br></br> Setting finite retention period failed on system-versioned temporal table 'temporalstagetestdb.dbo.WebsiteUserInfo' because hello history table 'temporalstagetestdb.dbo.WebsiteUserInfoHistory' does not contain required clustered index. Consider creating a clustered columnstore or B-tree index starting with hello column that matches end of SYSTEM_TIME period, on hello history table.*</span></span>

<span data-ttu-id="9b29d-144">É importante toonotice que Olá tabela de histórico padrão criada pelo banco de dados SQL já tem um índice, que é compatível com a política de retenção clusterizado.</span><span class="sxs-lookup"><span data-stu-id="9b29d-144">It is important toonotice that hello default history table created by Azure SQL Database already has clustered index, which is compliant for retention policy.</span></span> <span data-ttu-id="9b29d-145">Se você tentar tooremove índice em uma tabela com o período de retenção finito, a operação falhará com hello erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="9b29d-145">If you try tooremove that index on a table with finite retention period, operation fails with hello following error:</span></span>

<span data-ttu-id="9b29d-146">*Msg 13766, nível 16, estado 1 <br> </br> não é possível descartar o índice clusterizado de saudação 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' porque ele está sendo usado para a limpeza automática de dados antigos. Considere a configuração HISTORY_RETENTION_PERIOD tooINFINITE correspondente tabela temporal com versão do sistema Olá se você precisar toodrop esse índice.*</span><span class="sxs-lookup"><span data-stu-id="9b29d-146">*Msg 13766, Level 16, State 1 <br></br> Cannot drop hello clustered index 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' because it is being used for automatic cleanup of aged data. Consider setting HISTORY_RETENTION_PERIOD tooINFINITE on hello corresponding system-versioned temporal table if you need toodrop this index.*</span></span>

<span data-ttu-id="9b29d-147">Limpeza em um índice columnstore clusterizado Olá funcione de maneira ideal se históricos linhas são inseridas no hello ordem crescente (ordenado pela extremidade de saudação da coluna do período), que é sempre Olá caso de tabela de histórico de saudação é populada exclusivamente pelo Olá sistema _ Mecanismo VERSIONIOING.</span><span class="sxs-lookup"><span data-stu-id="9b29d-147">Cleanup on hello clustered columnstore index works optimally if historical rows are inserted in hello ascending order (ordered by hello end of period column), which is always hello case when hello history table is populated exclusively by hello SYSTEM_VERSIONIOING mechanism.</span></span> <span data-ttu-id="9b29d-148">Se as linhas na tabela de histórico de saudação não são ordenadas pelo final da coluna do período (que pode ser o caso de Olá se você migrou os dados de histórico existentes), você deve recriar o índice columnstore clusterizado na parte superior do índice de rowstore de árvore B corretamente é ordenado, tooachieve ideal desempenho.</span><span class="sxs-lookup"><span data-stu-id="9b29d-148">If rows in hello history table are not ordered by end of period column (which may be hello case if you migrated existing historical data), you should re-create clustered columnstore index on top of B-tree rowstore index that is properly ordered, tooachieve optimal performance.</span></span>

<span data-ttu-id="9b29d-149">Evite a recriação de índice columnstore clusterizado na tabela de histórico de saudação com período de retenção finito hello, porque ele pode alterar a ordem em grupos de linhas de saudação naturalmente impostos pela operação de controle de versão de sistema hello.</span><span class="sxs-lookup"><span data-stu-id="9b29d-149">Avoid rebuilding clustered columnstore index on hello history table with hello finite retention period, because it may change ordering in hello row groups naturally imposed by hello system-versioning operation.</span></span> <span data-ttu-id="9b29d-150">Se você precisar de um índice columnstore clusterizado na tabela de histórico de saudação toorebuild, fazer isso, recriando sobre compatível com índice de árvore B, preservando a ordenação Olá RowGroups necessário para a limpeza de dados regulares.</span><span class="sxs-lookup"><span data-stu-id="9b29d-150">If you need toorebuild clustered columnstore index on hello history table, do that by re-creating it on top of compliant B-tree index, preserving ordering in hello rowgroups necessary for regular data cleanup.</span></span> <span data-ttu-id="9b29d-151">Olá a mesma abordagem deve ser tomada se você criar a tabela temporal com tabela de histórico existente que tem um índice de coluna sem ordem de dados garantida clusterizado:</span><span class="sxs-lookup"><span data-stu-id="9b29d-151">hello same approach should be taken if you create temporal table with existing history table that has clustered column index without guaranteed data order:</span></span>

````
/*Create B-tree ordered by hello end of period column*/
CREATE CLUSTERED INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory (ValidTo)
WITH (DROP_EXISTING = ON);
GO
/*Re-create clustered columnstore index*/
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON);
````

<span data-ttu-id="9b29d-152">Quando o período de retenção finito está configurado para a tabela de histórico de Olá com um índice columnstore clusterizado hello, você não pode criar índices adicionais de árvore B não clusterizado na tabela:</span><span class="sxs-lookup"><span data-stu-id="9b29d-152">When finite retention period is configured for hello history table with hello clustered columnstore index, you cannot create additional non-clustered B-tree indexes on that table:</span></span>

````
CREATE NONCLUSTERED INDEX IX_WebHistNCI ON WebsiteUserInfoHistory ([UserName])
````

<span data-ttu-id="9b29d-153">Um tooexecute tentativa acima instrução falha com hello erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="9b29d-153">An attempt tooexecute above statement fails with hello following error:</span></span>

<span data-ttu-id="9b29d-154">*Msg 13772, Nível 16, Estado 1 <br></br> Não é possível criar índice não clusterizado em uma tabela de histórico temporal “WebsiteUserInfoHistory”, pois ele tem o período de retenção finito e o índice columnstore clusterizado definido.*</span><span class="sxs-lookup"><span data-stu-id="9b29d-154">*Msg 13772, Level 16, State 1 <br></br> Cannot create non-clustered index on a temporal history table 'WebsiteUserInfoHistory' since it has finite retention period and clustered columnstore index defined.*</span></span>

## <a name="querying-tables-with-retention-policy"></a><span data-ttu-id="9b29d-155">Consultando tabelas com a política de retenção</span><span class="sxs-lookup"><span data-stu-id="9b29d-155">Querying tables with retention policy</span></span>
<span data-ttu-id="9b29d-156">Todas as consultas de tabela temporal Olá filtram automaticamente históricas linhas que correspondem a política de retenção finito, tooavoid resultados imprevisíveis e inconsistentes, pois antigas linhas excluídas pela tarefa de limpeza Olá, *em qualquer ponto no tempo e no ordem arbitrária*.</span><span class="sxs-lookup"><span data-stu-id="9b29d-156">All queries on hello temporal table automatically filter out historical rows matching finite retention policy, tooavoid unpredictable and inconsistent results, since aged rows can be deleted by hello cleanup task, *at any point in time and in arbitrary order*.</span></span>

<span data-ttu-id="9b29d-157">Olá, imagem a seguir mostra Olá plano de consulta para uma consulta simples:</span><span class="sxs-lookup"><span data-stu-id="9b29d-157">hello following picture shows hello query plan for a simple query:</span></span>

````
SELECT * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME ALL;
````

<span data-ttu-id="9b29d-158">consulta Olá plano inclui o filtro aplicado tooend da coluna do período (ValidTo) no operador Clustered Index Scan de saudação na tabela de histórico de saudação (realçada).</span><span class="sxs-lookup"><span data-stu-id="9b29d-158">hello query plan includes additional filter applied tooend of period column (ValidTo) in hello Clustered Index Scan operator on hello history table (highlighted).</span></span> <span data-ttu-id="9b29d-159">Este exemplo supõe que o período de retenção de um MÊS foi definido na tabela WebsiteUserInfo.</span><span class="sxs-lookup"><span data-stu-id="9b29d-159">This example assumes that one MONTH retention period was set on WebsiteUserInfo table.</span></span>

![Filtro de consulta de retenção](./media/sql-database-temporal-tables-retention-policy/queryexecplanwithretention.png)

<span data-ttu-id="9b29d-161">No entanto, se você consultar diretamente a tabela de histórico, verá linhas que são mais antigas do que o período de retenção especificado, mas sem qualquer garantia de resultados da consulta repetíveis.</span><span class="sxs-lookup"><span data-stu-id="9b29d-161">However, if you query history table directly, you may see rows that are older than specified retention period, but without any guarantee for repeatable query results.</span></span> <span data-ttu-id="9b29d-162">Olá imagem a seguir mostra plano de execução de consulta para consulta Olá na tabela de histórico de saudação sem filtros adicionais aplicados:</span><span class="sxs-lookup"><span data-stu-id="9b29d-162">hello following picture shows query execution plan for hello query on hello history table without additional filters applied:</span></span>

![Consultando histórico sem filtro de retenção](./media/sql-database-temporal-tables-retention-policy/queryexecplanhistorytable.png)

<span data-ttu-id="9b29d-164">A lógica de negócios não deve contar com a leitura da tabela de histórico além do período de retenção, pois resultados inconsistentes ou inesperados podem ser obtidos.</span><span class="sxs-lookup"><span data-stu-id="9b29d-164">Do not rely your business logic on reading history table beyond retention period as you may get inconsistent or unexpected results.</span></span> <span data-ttu-id="9b29d-165">É recomendável usar consultas temporais com a cláusula FOR SYSTEM_TIME para análise de dados em tabelas temporais.</span><span class="sxs-lookup"><span data-stu-id="9b29d-165">We recommend that you use temporal queries with FOR SYSTEM_TIME clause for analyzing data in temporal tables.</span></span>

## <a name="point-in-time-restore-considerations"></a><span data-ttu-id="9b29d-166">Considerações da recuperação pontual</span><span class="sxs-lookup"><span data-stu-id="9b29d-166">Point in time restore considerations</span></span>
<span data-ttu-id="9b29d-167">Quando você cria o novo banco de dados por [restauração existente ponto específico tooa de banco de dados no tempo](sql-database-recovery-using-backups.md), ele tem retenção temporal desabilitada no nível de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b29d-167">When you create new database by [restoring existing database tooa specific point in time](sql-database-recovery-using-backups.md), it has temporal retention disabled at hello database level.</span></span> <span data-ttu-id="9b29d-168">(**is_temporal_history_retention_enabled** sinalizador definido tooOFF).</span><span class="sxs-lookup"><span data-stu-id="9b29d-168">(**is_temporal_history_retention_enabled** flag set tooOFF).</span></span> <span data-ttu-id="9b29d-169">Essa funcionalidade permite que você tooexamine todas as linhas após a restauração, sem se preocupar com históricos que antigos linhas são removidas antes de obter tooquery-los.</span><span class="sxs-lookup"><span data-stu-id="9b29d-169">This functionality allows you tooexamine all historical rows upon restore, without worrying that aged rows are removed before you get tooquery them.</span></span> <span data-ttu-id="9b29d-170">Você pode usá-lo muito*inspecionar dados históricos além do período de retenção configurado*.</span><span class="sxs-lookup"><span data-stu-id="9b29d-170">You can use it too*inspect historical data beyond configured retention period*.</span></span>

<span data-ttu-id="9b29d-171">Digamos que uma tabela temporal tem o período de retenção de um MÊS especificado.</span><span class="sxs-lookup"><span data-stu-id="9b29d-171">Say that a temporal table has one MONTH retention period specified.</span></span> <span data-ttu-id="9b29d-172">Se seu banco de dados foi criado na camada de serviço Premium, seria toocreate capaz de cópia de banco de dados com o estado do banco de dados Olá backup too35 dias no hello anterior.</span><span class="sxs-lookup"><span data-stu-id="9b29d-172">If your database was created in Premium Service tier, you would be able toocreate database copy with hello database state up too35 days back in hello past.</span></span> <span data-ttu-id="9b29d-173">Que efetivamente permitiria tooanalyze linhas históricos que estão up too65 dias consultando a tabela de histórico de saudação diretamente.</span><span class="sxs-lookup"><span data-stu-id="9b29d-173">That effectively would allow you tooanalyze historical rows that are up too65 days old by querying hello history table directly.</span></span>

<span data-ttu-id="9b29d-174">Se desejar que a limpeza de retenção temporal tooactivate, execute Olá após a instrução Transact-SQL após a restauração pontual:</span><span class="sxs-lookup"><span data-stu-id="9b29d-174">If you want tooactivate temporal retention cleanup, run hello following Transact-SQL statement after point in time restore:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

## <a name="next-steps"></a><span data-ttu-id="9b29d-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9b29d-175">Next steps</span></span>
<span data-ttu-id="9b29d-176">como as tabelas temporais em seus aplicativos, toouse check-out de toolearn [Introdução às tabelas temporais no banco de dados do SQL Azure](sql-database-temporal-tables.md).</span><span class="sxs-lookup"><span data-stu-id="9b29d-176">toolearn how toouse Temporal Tables in your applications, check out [Getting Started with Temporal Tables in Azure SQL Database](sql-database-temporal-tables.md).</span></span>

<span data-ttu-id="9b29d-177">Visite Channel 9 toohear um [real implementação temporal história de sucesso](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) e inspecionar uma [live temporal demonstração](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span><span class="sxs-lookup"><span data-stu-id="9b29d-177">Visit Channel 9 toohear a [real customer temporal implementation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

<span data-ttu-id="9b29d-178">Para obter informações detalhadas sobre as Tabelas Temporais, leia a [documentação do MSDN](https://msdn.microsoft.com/library/dn935015.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b29d-178">For detailed information about Temporal Tables, review [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>

