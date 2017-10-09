---
title: "PowerShell: Criar e gerenciar um pool elástico do SQL do Azure | Microsoft Docs"
description: "Saiba como toouse PowerShell toomanage um pool Elástico."
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 61289770-69b9-4ae3-9252-d0e94d709331
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: data-management
ms.date: 06/06/2017
ms.author: srinia
ms.openlocfilehash: 92de2a4b243dcc74502064e9d2c31682691753d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a><span data-ttu-id="38440-103">Criar e gerenciar um pool elástico com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="38440-103">Create and manage an elastic pool with PowerShell</span></span>
<span data-ttu-id="38440-104">Este tópico mostra como toocreate e gerenciar escalonável [pools Elásticos](sql-database-elastic-pool.md) com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="38440-104">This topic shows you how toocreate and manage scalable [elastic pools](sql-database-elastic-pool.md) with PowerShell.</span></span>  <span data-ttu-id="38440-105">Você também pode criar e gerenciar um pool Elástico do Azure usando Olá [portal do Azure](https://portal.azure.com/), API de REST, ou [c#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="38440-105">You can also create and manage an Azure elastic pool using hello [Azure portal](https://portal.azure.com/), REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="38440-106">Você também pode criar e mover bancos de dados de e para os pools elásticos usando [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="38440-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a><span data-ttu-id="38440-107">Criar um pool elástico</span><span class="sxs-lookup"><span data-stu-id="38440-107">Create an elastic pool</span></span>
<span data-ttu-id="38440-108">Olá [AzureRmSqlElasticPool novo](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet cria um pool Elástico.</span><span class="sxs-lookup"><span data-stu-id="38440-108">hello [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet creates an elastic pool.</span></span> <span data-ttu-id="38440-109">valores de saudação de eDTU por pool, min e max DTUs são restritas por valor de nível de serviço hello (Basic, Standard, Premium ou Premium RS).</span><span class="sxs-lookup"><span data-stu-id="38440-109">hello values for eDTU per pool, min, and max DTUs are constrained by hello service tier value (Basic, Standard, Premium, or Premium RS).</span></span> <span data-ttu-id="38440-110">Confira [Limites de eDTU e armazenamento para pools elásticos e bancos de dados em pool](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="38440-110">See [eDTU and storage limits for elastic pools and pooled databases](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span></span>

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="38440-111">Criar um banco de dados em pool em um pool elástico</span><span class="sxs-lookup"><span data-stu-id="38440-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="38440-112">Saudação de uso [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet e conjunto hello **ElasticPoolName** pool de destino do parâmetro toohello.</span><span class="sxs-lookup"><span data-stu-id="38440-112">Use hello [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet and set hello **ElasticPoolName** parameter toohello target pool.</span></span> <span data-ttu-id="38440-113">toomove banco de dados existente em um pool Elástico, consulte [mover um banco de dados para um pool Elástico](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span><span class="sxs-lookup"><span data-stu-id="38440-113">toomove an existing database into an elastic pool, see [Move a database into an elastic pool](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span></span>

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a><span data-ttu-id="38440-114">Script completo</span><span class="sxs-lookup"><span data-stu-id="38440-114">Complete script</span></span>
<span data-ttu-id="38440-115">Esse script cria um grupo de recursos do Azure e um servidor.</span><span class="sxs-lookup"><span data-stu-id="38440-115">This script creates an Azure resource group and a server.</span></span> <span data-ttu-id="38440-116">Quando solicitado, forneça um nome de usuário administrador e a senha para o novo servidor de saudação (não suas credenciais do Azure).</span><span class="sxs-lookup"><span data-stu-id="38440-116">When prompted, supply an administrator username and password for hello new server (not your Azure credentials).</span></span>

```PowerShell
$subscriptionId = '<your Azure subscription id>'
$resourceGroupName = '<resource group name>'
$location = '<datacenter location>'
$serverName = '<server name>'
$poolName = '<pool name>'
$databaseName = '<database name>'

Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $serverName -Location $location -ServerVersion "12.0"
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $serverName -FirewallRuleName "rule1" -StartIpAddress "192.168.0.198" -EndIpAddress "192.168.0.199"

New-AzureRmSqlElasticPool -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100

New-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -ElasticPoolName $poolName -MaxSizeBytes 10GB
```

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a><span data-ttu-id="38440-117">Criar um pool elástico e adicionar vários bancos de dados em pool</span><span class="sxs-lookup"><span data-stu-id="38440-117">Create an elastic pool and add multiple pooled databases</span></span>
<span data-ttu-id="38440-118">Criação de muitos bancos de dados em um pool Elástico pode levar tempo quando feito usando o portal de saudação ou cmdlets do PowerShell que criar apenas um único banco de dados de cada vez.</span><span class="sxs-lookup"><span data-stu-id="38440-118">Creation of many databases in an elastic pool can take time when done using hello portal or PowerShell cmdlets that create only a single database at a time.</span></span> <span data-ttu-id="38440-119">criação de tooautomate em um pool Elástico, consulte [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span><span class="sxs-lookup"><span data-stu-id="38440-119">tooautomate creation into an elastic pool, see [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="38440-120">Mover um banco de dados para um pool elástico</span><span class="sxs-lookup"><span data-stu-id="38440-120">Move a database into an elastic pool</span></span>
<span data-ttu-id="38440-121">Você pode mover um banco de dados para dentro ou fora de um pool Elástico com hello [AzureRmSqlDatabase conjunto](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span><span class="sxs-lookup"><span data-stu-id="38440-121">You can move a database into or out of an elastic pool with hello [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span></span>

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="38440-122">Alterar as configurações de desempenho de um pool elástico</span><span class="sxs-lookup"><span data-stu-id="38440-122">Change performance settings of an elastic pool</span></span>
<span data-ttu-id="38440-123">Quando o desempenho é prejudicado, você pode alterar as configurações de saudação do crescimento do hello pool tooaccommodate.</span><span class="sxs-lookup"><span data-stu-id="38440-123">When performance suffers, you can change hello settings of hello pool tooaccommodate growth.</span></span> <span data-ttu-id="38440-124">Saudação de uso [AzureRmSqlElasticPool conjunto](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="38440-124">Use hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet.</span></span> <span data-ttu-id="38440-125">Definir Olá - Dtu parâmetro toohello eDTUs por pool.</span><span class="sxs-lookup"><span data-stu-id="38440-125">Set hello -Dtu parameter toohello eDTUs per pool.</span></span> <span data-ttu-id="38440-126">Consulte os valores possível em [limites de armazenamento e eDTU](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="38440-126">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-hello-storage-limit-for-an-elastic-pool"></a><span data-ttu-id="38440-127">Alterar o limite de armazenamento de saudação para um pool Elástico</span><span class="sxs-lookup"><span data-stu-id="38440-127">Change hello storage limit for an elastic pool</span></span>

<span data-ttu-id="38440-128">Saudação de uso [conjunto AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet tooset Olá _- StorageMB_ parâmetro.</span><span class="sxs-lookup"><span data-stu-id="38440-128">Use hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet tooset hello _-StorageMB_ parameter.</span></span> <span data-ttu-id="38440-129">Forneça o limite de armazenamento de saudação em MB (por exemplo, 2097152 conjuntos Olá armazenamento limite too2 TB).</span><span class="sxs-lookup"><span data-stu-id="38440-129">Provide hello storage limit in MB (for example, 2097152 sets hello storage limit too2 TB).</span></span> <span data-ttu-id="38440-130">Consulte os valores possível em [limites de armazenamento e eDTU](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="38440-130">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="38440-131">armazenamento de dados max saudação padrão por pool para pools de Premium com 1500 eDTUs ou mais é 750 GB.</span><span class="sxs-lookup"><span data-stu-id="38440-131">hello default max data storage per pool for Premium pools with 1500 eDTUs or more is 750 GB.</span></span> <span data-ttu-id="38440-132">tooobtain Olá superior _máxima do tamanho de armazenamento de dados por pool_, limite de armazenamento Olá deve ser explicitamente definido.</span><span class="sxs-lookup"><span data-stu-id="38440-132">tooobtain hello higher _max data storage size per pool_, hello storage limit must be explicitly set.</span></span> <span data-ttu-id="38440-133">Pools de Premium com mais de 750 GB de armazenamento está atualmente em visualização pública no hello seguintes regiões: Leste dos EUA 2, oeste dos EUA, nós Gov Virgínia, Europa Ocidental, Alemanha Central, Sudeste da Ásia, Leste do Japão, Leste da Austrália, Canadá Central e Leste do Canadá.</span><span class="sxs-lookup"><span data-stu-id="38440-133">Premium pools with more than 750 GB of storage is currently in public preview in hello following regions: East US 2, West US, US Gov Virginia, West Europe, Germany Central, Southeast Asia, Japan East, Australia East, Canada Central, and Canada East.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-hello-status-of-pool-operations"></a><span data-ttu-id="38440-134">Obter status de saudação de operações de pool</span><span class="sxs-lookup"><span data-stu-id="38440-134">Get hello status of pool operations</span></span>
<span data-ttu-id="38440-135">Criar um pool elástico pode levar tempo.</span><span class="sxs-lookup"><span data-stu-id="38440-135">Creating an elastic pool can take time.</span></span> <span data-ttu-id="38440-136">status de saudação tootrack das operações de pool, incluindo a criação e atualizações, use Olá [AzureRmSqlElasticPoolActivity Get](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="38440-136">tootrack hello status of pool operations including creation and updates, use hello [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-hello-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a><span data-ttu-id="38440-137">Obter status de saudação de mover um banco de dados dentro e fora de um pool Elástico</span><span class="sxs-lookup"><span data-stu-id="38440-137">Get hello status of moving a database into and out of an elastic pool</span></span>
<span data-ttu-id="38440-138">Mover um banco de dados pode levar tempo.</span><span class="sxs-lookup"><span data-stu-id="38440-138">Moving a database can take time.</span></span> <span data-ttu-id="38440-139">Controlar status mover usando Olá [AzureRmSqlDatabaseActivity Get](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="38440-139">Track a move status using hello [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="38440-140">Obter dados de uso de recursos para um pool elástico</span><span class="sxs-lookup"><span data-stu-id="38440-140">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="38440-141">Métricas que podem ser recuperadas como uma porcentagem do limite do pool de recursos de saudação:</span><span class="sxs-lookup"><span data-stu-id="38440-141">Metrics that can be retrieved as a percentage of hello resource pool limit:</span></span>

| <span data-ttu-id="38440-142">Nome da métrica</span><span class="sxs-lookup"><span data-stu-id="38440-142">Metric name</span></span> | <span data-ttu-id="38440-143">Descrição</span><span class="sxs-lookup"><span data-stu-id="38440-143">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="38440-144">cpu\_percent</span><span class="sxs-lookup"><span data-stu-id="38440-144">cpu\_percent</span></span> |<span data-ttu-id="38440-145">Média de utilização em porcentagem do limite de saudação do pool de saudação de computação.</span><span class="sxs-lookup"><span data-stu-id="38440-145">Average compute utilization in percentage of hello limit of hello pool.</span></span> |
| <span data-ttu-id="38440-146">physical\_data\_read\_percent</span><span class="sxs-lookup"><span data-stu-id="38440-146">physical\_data\_read\_percent</span></span> |<span data-ttu-id="38440-147">Utilização média de e/s em porcentagem com base no limite de saudação do pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="38440-147">Average I/O utilization in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="38440-148">log\_write\_percent</span><span class="sxs-lookup"><span data-stu-id="38440-148">log\_write\_percent</span></span> |<span data-ttu-id="38440-149">Média de utilização de recursos de gravação em porcentagem do limite de saudação do pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="38440-149">Average write resource utilization in percentage of hello limit of hello pool.</span></span> |
| <span data-ttu-id="38440-150">DTU\_consumption\_percent</span><span class="sxs-lookup"><span data-stu-id="38440-150">DTU\_consumption\_percent</span></span> |<span data-ttu-id="38440-151">Utilização média de eDTU em porcentagem do limite de eDTU de pool de saudação</span><span class="sxs-lookup"><span data-stu-id="38440-151">Average eDTU utilization in percentage of eDTU limit for hello pool</span></span> |
| <span data-ttu-id="38440-152">storage\_percent</span><span class="sxs-lookup"><span data-stu-id="38440-152">storage\_percent</span></span> |<span data-ttu-id="38440-153">Média de utilização do armazenamento em porcentagem do limite de armazenamento de saudação do pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="38440-153">Average storage utilization in percentage of hello storage limit of hello pool.</span></span> |
| <span data-ttu-id="38440-154">workers\_percent</span><span class="sxs-lookup"><span data-stu-id="38440-154">workers\_percent</span></span> |<span data-ttu-id="38440-155">Máximo simultâneos trabalhadores (solicitações) em porcentagem com base no limite de saudação do pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="38440-155">Maximum concurrent workers (requests) in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="38440-156">sessions\_percent</span><span class="sxs-lookup"><span data-stu-id="38440-156">sessions\_percent</span></span> |<span data-ttu-id="38440-157">Máximo de sessões simultâneas em porcentagem com base no limite de saudação do pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="38440-157">Maximum concurrent sessions in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="38440-158">eDTU_limit</span><span class="sxs-lookup"><span data-stu-id="38440-158">eDTU_limit</span></span> |<span data-ttu-id="38440-159">Configuração atual de DTUs máximas do pool elástico para este pool elástico durante este intervalo.</span><span class="sxs-lookup"><span data-stu-id="38440-159">Current max elastic pool DTU setting for this elastic pool during this interval.</span></span> |
| <span data-ttu-id="38440-160">storage\_limit</span><span class="sxs-lookup"><span data-stu-id="38440-160">storage\_limit</span></span> |<span data-ttu-id="38440-161">Configuração atual de limite máximo de armazenamento do pool elástico para este pool elástico em megabytes durante este intervalo.</span><span class="sxs-lookup"><span data-stu-id="38440-161">Current max elastic pool storage limit setting for this elastic pool in megabytes during this interval.</span></span> |
| <span data-ttu-id="38440-162">eDTU\_used</span><span class="sxs-lookup"><span data-stu-id="38440-162">eDTU\_used</span></span> |<span data-ttu-id="38440-163">EDTUs média usada pelo pool de saudação nesse intervalo.</span><span class="sxs-lookup"><span data-stu-id="38440-163">Average eDTUs used by hello pool in this interval.</span></span> |
| <span data-ttu-id="38440-164">storage\_used</span><span class="sxs-lookup"><span data-stu-id="38440-164">storage\_used</span></span> |<span data-ttu-id="38440-165">Armazenamento média usado pelo pool de saudação nesse intervalo, em bytes</span><span class="sxs-lookup"><span data-stu-id="38440-165">Average storage used by hello pool in this interval in bytes</span></span> |

<span data-ttu-id="38440-166">**Períodos de retenção/granularidade das métricas:**</span><span class="sxs-lookup"><span data-stu-id="38440-166">**Metrics granularity/retention periods:**</span></span>

* <span data-ttu-id="38440-167">Os dados retornam com uma granularidade de cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="38440-167">Data is returned at 5-minute granularity.</span></span>  
* <span data-ttu-id="38440-168">A retenção dos dados é de 35 dias.</span><span class="sxs-lookup"><span data-stu-id="38440-168">Data retention is 35 days.</span></span>  

<span data-ttu-id="38440-169">Esse cmdlet e API limita o número de saudação de linhas que podem ser recuperados em uma chamada too1000 linhas (cerca de 3 dias de dados na granularidade de 5 minutos).</span><span class="sxs-lookup"><span data-stu-id="38440-169">This cmdlet and API limits hello number of rows that can be retrieved in one call too1000 rows (about 3 days of data at 5-minute granularity).</span></span> <span data-ttu-id="38440-170">Mas esse comando pode ser chamado várias vezes com tooretrieve de intervalos de tempo diferentes de início/término mais dados</span><span class="sxs-lookup"><span data-stu-id="38440-170">But this command can be called multiple times with different start/end time intervals tooretrieve more data</span></span>

<span data-ttu-id="38440-171">métricas de saudação tooretrieve:</span><span class="sxs-lookup"><span data-stu-id="38440-171">tooretrieve hello metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a><span data-ttu-id="38440-172">Obter dados de uso de recursos de um banco de dados em um pool elástico</span><span class="sxs-lookup"><span data-stu-id="38440-172">Get resource usage data for a database in an elastic pool</span></span>
<span data-ttu-id="38440-173">Essas APIs são Olá mesmo Olá APIs usadas para monitorar a utilização de recursos de saudação de um único banco de dados, exceto Olá diferença semântica a seguir: métricas recuperadas são expressos como uma porcentagem da saudação por eDTUs máximo do banco de dados (ou equivalente cap para Olá Base métrica, como CPU ou e/s) definido para esse pool.</span><span class="sxs-lookup"><span data-stu-id="38440-173">These APIs are hello same as hello APIs used for monitoring hello resource utilization of a single database, except for hello following semantic difference: metrics retrieved are expressed as a percentage of hello per database max eDTUs (or equivalent cap for hello underlying metric like CPU or IO) set for that pool.</span></span> <span data-ttu-id="38440-174">Por exemplo, a 50% de utilização de qualquer uma dessas métricas indica que o consumo de recursos específicos de saudação é a 50% da saudação por limite de banco de dados para esse recurso no pool de pai hello.</span><span class="sxs-lookup"><span data-stu-id="38440-174">For example, 50% utilization of any of these metrics indicates that hello specific resource consumption is at 50% of hello per database cap limit for that resource in hello parent pool.</span></span>

<span data-ttu-id="38440-175">métricas de saudação tooretrieve:</span><span class="sxs-lookup"><span data-stu-id="38440-175">tooretrieve hello metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-tooan-elastic-pool-resource"></a><span data-ttu-id="38440-176">Adicionar um recurso de pool Elástico tooan alerta</span><span class="sxs-lookup"><span data-stu-id="38440-176">Add an alert tooan elastic pool resource</span></span>
<span data-ttu-id="38440-177">Você pode adicionar regras de alerta tooan pool Elástico toosend notificações por email ou alerta cadeias de caracteres muito[pontos de extremidade de URL](https://msdn.microsoft.com/library/mt718036.aspx) quando o pool Elástico Olá atinge um limite de utilização que você configurou.</span><span class="sxs-lookup"><span data-stu-id="38440-177">You can add alert rules tooan elastic pool toosend email notifications or alert strings too[URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when hello elastic pool hits a utilization threshold that you set up.</span></span> <span data-ttu-id="38440-178">Use o cmdlet Olá AzureRmMetricAlertRule adicionar.</span><span class="sxs-lookup"><span data-stu-id="38440-178">Use hello Add-AzureRmMetricAlertRule cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="38440-179">O monitoramento de utilização de recursos para pools elásticos tem um atraso de, pelo menos, 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="38440-179">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="38440-180">No momento, não é permitido definir alertas de menos de 10 minutos para pools elásticos.</span><span class="sxs-lookup"><span data-stu-id="38440-180">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="38440-181">Todos os alertas definidos para pools Elásticos com um ponto (chamado de parâmetro "-Tamanho_da_janela" na API do PowerShell) de menos de 10 minutos pode não ser disparada.</span><span class="sxs-lookup"><span data-stu-id="38440-181">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="38440-182">Certifique-se de que todos os alertas definidos para pools elásticos usem um período (WindowSize) de 10 minutos ou mais.</span><span class="sxs-lookup"><span data-stu-id="38440-182">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>
>

<span data-ttu-id="38440-183">Este exemplo adiciona um alerta para ser notificado quando o consumo de eDTU de um pool elástico ultrapassar determinado limite.</span><span class="sxs-lookup"><span data-stu-id="38440-183">This example adds an alert for getting notified when an elastic pool’s eDTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location =  '<location'                         # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

#$Target Resource ID
$ResourceID = '/subscriptions/' + $subscriptionId + '/resourceGroups/' +$resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticpools/' + $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# create a unique rule name
$alertName = $poolName + "- DTU consumption rule"

# Create an alert rule for DTU_consumption_percent
Add-AzureRMMetricAlertRule -Name $alertName -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $ResourceID -MetricName "DTU_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail
```

<span data-ttu-id="38440-184">Para obter mais informações, consulte [Criar alertas do Banco de Dados SQL no portal do Azure](sql-database-insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="38440-184">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="add-alerts-tooall-databases-in-an-elastic-pool"></a><span data-ttu-id="38440-185">Adicionar bancos de dados de tooall alertas em um pool Elástico</span><span class="sxs-lookup"><span data-stu-id="38440-185">Add alerts tooall databases in an elastic pool</span></span>
<span data-ttu-id="38440-186">Você pode adicionar regras de alerta tooall banco de dados em um pool Elástico toosend notificações por email ou alerta cadeias de caracteres muito[pontos de extremidade de URL](https://msdn.microsoft.com/library/mt718036.aspx) quando um recurso atinge um limite de utilização configurado pelo alerta hello.</span><span class="sxs-lookup"><span data-stu-id="38440-186">You can add alert rules tooall database in an elastic pool toosend email notifications or alert strings too[URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when a resource hits a utilization threshold set up by hello alert.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="38440-187">O monitoramento de utilização de recursos para pools elásticos tem um atraso de, pelo menos, 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="38440-187">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="38440-188">No momento, não é permitido definir alertas de menos de 10 minutos para pools elásticos.</span><span class="sxs-lookup"><span data-stu-id="38440-188">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="38440-189">Todos os alertas definidos para pools Elásticos com um ponto (chamado de parâmetro "-Tamanho_da_janela" na API do PowerShell) de menos de 10 minutos pode não ser disparada.</span><span class="sxs-lookup"><span data-stu-id="38440-189">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="38440-190">Certifique-se de que todos os alertas definidos para pools elásticos usem um período (WindowSize) de 10 minutos ou mais.</span><span class="sxs-lookup"><span data-stu-id="38440-190">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>

<span data-ttu-id="38440-191">Este exemplo adiciona um alerta tooeach de bancos de dados de saudação em um pool Elástico para ser notificado quando o consumo de DTU do banco de dados fica acima de certo limite.</span><span class="sxs-lookup"><span data-stu-id="38440-191">This example adds an alert tooeach of hello databases in an elastic pool for getting notified when that database’s DTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location = '<location'                          # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
foreach ($db in $dbList)
{
    $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName

    # create a unique rule name
    $alertName = $db.DatabaseName + "- DTU consumption rule"

    # Create an alert rule for DTU_consumption_percent
    Add-AzureRMMetricAlertRule -Name $alertName  -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $dbResourceId -MetricName "dtu_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail

    # drop hello alert rule
    #Remove-AzureRmAlertRule -ResourceGroup $resourceGroupName -Name $alertName
}
```

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a><span data-ttu-id="38440-192">Coletar e monitorar dados de uso de recursos em vários pools em uma assinatura</span><span class="sxs-lookup"><span data-stu-id="38440-192">Collect and monitor resource usage data across multiple pools in a subscription</span></span>
<span data-ttu-id="38440-193">Quando você tiver vários bancos de dados em uma assinatura, é complicado toomonitor cada elástica pool separadamente.</span><span class="sxs-lookup"><span data-stu-id="38440-193">When you have many databases in a subscription, it is cumbersome toomonitor each elastic pool separately.</span></span> <span data-ttu-id="38440-194">Em vez disso, cmdlets do PowerShell de banco de dados SQL e consultas T-SQL podem ser dados de uso de recursos toocollect combinado de vários pools e seus bancos de dados para monitoramento e análise da utilização de recursos.</span><span class="sxs-lookup"><span data-stu-id="38440-194">Instead, SQL database PowerShell cmdlets and T-SQL queries can be combined toocollect resource usage data from multiple pools and their databases for monitoring and analysis of resource usage.</span></span> <span data-ttu-id="38440-195">Um [implementação de exemplo](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) de tal um conjunto de powershell scripts podem encontrados no repositório de exemplos do hello GitHub SQL Server junto com a documentação sobre o que ele faz e como toouse-lo.</span><span class="sxs-lookup"><span data-stu-id="38440-195">A [sample implementation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) of such a set of powershell scripts can be found in hello GitHub SQL Server samples repository along with documentation on what it does and how toouse it.</span></span>

<span data-ttu-id="38440-196">toouse Este exemplo de implementação, siga estas etapas.</span><span class="sxs-lookup"><span data-stu-id="38440-196">toouse this sample implementation, follow these steps.</span></span>

1. <span data-ttu-id="38440-197">Baixar Olá [scripts e a documentação](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span><span class="sxs-lookup"><span data-stu-id="38440-197">Download hello [scripts and documentation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span></span>
2. <span data-ttu-id="38440-198">Modifique os scripts Olá para o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="38440-198">Modify hello scripts for your environment.</span></span> <span data-ttu-id="38440-199">Especifique um ou mais servidores nos quais os pools elásticos são hospedados.</span><span class="sxs-lookup"><span data-stu-id="38440-199">Specify one or more servers on which elastic pools are hosted.</span></span>
3. <span data-ttu-id="38440-200">Especifique um banco de dados de telemetria onde hello métricas coletadas são toobe armazenado.</span><span class="sxs-lookup"><span data-stu-id="38440-200">Specify a telemetry database where hello collected metrics are toobe stored.</span></span>
4. <span data-ttu-id="38440-201">Personalize Olá script toospecify Olá durante execução de scripts de saudação.</span><span class="sxs-lookup"><span data-stu-id="38440-201">Customize hello script toospecify hello duration of hello scripts' execution.</span></span>

<span data-ttu-id="38440-202">Em um nível alto, scripts Olá Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="38440-202">At a high level, hello scripts do hello following:</span></span>

* <span data-ttu-id="38440-203">Enumera todos os servidores em uma determinada assinatura do Azure (ou uma lista de servidores específicos).</span><span class="sxs-lookup"><span data-stu-id="38440-203">Enumerates all servers in a given Azure subscription (or a specified list of servers).</span></span>
* <span data-ttu-id="38440-204">Executa um trabalho em segundo plano para cada servidor.</span><span class="sxs-lookup"><span data-stu-id="38440-204">Runs a background job for each server.</span></span> <span data-ttu-id="38440-205">trabalho de saudação é executado em um loop em intervalos regulares e coleta dados de telemetria para todos os pools de saudação no servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="38440-205">hello job runs in a loop at regular intervals and collects telemetry data for all hello pools in hello server.</span></span> <span data-ttu-id="38440-206">Ele carrega dados Olá coletado no banco de dados de telemetria especificado hello.</span><span class="sxs-lookup"><span data-stu-id="38440-206">It then loads hello collected data into hello specified telemetry database.</span></span>
* <span data-ttu-id="38440-207">Enumera uma lista de bancos de dados em dados de uso de recursos de banco de dados cada pool toocollect hello.</span><span class="sxs-lookup"><span data-stu-id="38440-207">Enumerates a list of databases in each pool toocollect hello database resource usage data.</span></span> <span data-ttu-id="38440-208">Ele carrega dados Olá coletado no banco de dados de telemetria hello.</span><span class="sxs-lookup"><span data-stu-id="38440-208">It then loads hello collected data into hello telemetry database.</span></span>

<span data-ttu-id="38440-209">Hello métricas coletadas no banco de dados de telemetria Olá podem ser analisados toomonitor Olá integridade de pools Elásticos e bancos de dados Olá nele.</span><span class="sxs-lookup"><span data-stu-id="38440-209">hello collected metrics in hello telemetry database can be analyzed toomonitor hello health of elastic pools and hello databases in it.</span></span> <span data-ttu-id="38440-210">script Hello também instala uma função de valor de tabela (TVF) predefinida em métricas de agregação Olá Olá telemetria banco de dados toohelp para uma janela de tempo especificado.</span><span class="sxs-lookup"><span data-stu-id="38440-210">hello script also installs a pre-defined Table-Value function (TVF) in hello telemetry database toohelp aggregate hello metrics for a specified time window.</span></span> <span data-ttu-id="38440-211">Por exemplo, os resultados da saudação TVF podem ser usado tooshow "top N pools Elásticos com a utilização de eDTU máximo Olá em uma janela de tempo determinado."</span><span class="sxs-lookup"><span data-stu-id="38440-211">For example, results of hello TVF can be used tooshow “top N elastic pools with hello maximum eDTU utilization in a given time window.”</span></span> <span data-ttu-id="38440-212">Opcionalmente, use ferramentas analíticas, como Excel ou Power BI tooquery e analisar dados coletado de saudação.</span><span class="sxs-lookup"><span data-stu-id="38440-212">Optionally, use analytic tools like Excel or Power BI tooquery and analyze hello collected data.</span></span>

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a><span data-ttu-id="38440-213">Exemplo: recuperar as métricas de consumo de recursos para um pool elástico e seus bancos de dados</span><span class="sxs-lookup"><span data-stu-id="38440-213">Example: retrieve resource consumption metrics for an elastic pool and its databases</span></span>
<span data-ttu-id="38440-214">Este exemplo recupera as métricas de consumo de saudação para um determinado pool Elástico e todos os seus bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="38440-214">This example retrieves hello consumption metrics for a given elastic pool and all its databases.</span></span> <span data-ttu-id="38440-215">Os dados coletados são formatados e escritos tooa formatado. csv.</span><span class="sxs-lookup"><span data-stu-id="38440-215">Collected data is formatted and written tooa .csv formatted file.</span></span> <span data-ttu-id="38440-216">arquivo Hello possa ser navegado com o Excel.</span><span class="sxs-lookup"><span data-stu-id="38440-216">hello file can be browsed with Excel.</span></span>

```PowerShell
$subscriptionId = '<Azure subscription id>'          # Azure subscription ID
$resourceGroupName = '<resource group name>'             # Resource Group
$serverName = <server name>                              # server name
$poolName = <elastic pool name>                          # pool name

# Login tooAzure account and select hello subscription.
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

# Get resource usage metrics for an elastic pool for hello specified time interval.
$startTime = '4/27/2016 00:00:00'  # start time in UTC
$endTime = '4/27/2016 01:00:00'    # end time in UTC

# Construct hello pool resource ID and retrive pool metrics at 5-minute granularity.
$poolResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticPools/' + $poolName
$poolMetrics = (Get-AzureRmMetric -ResourceId $poolResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
$dbMetrics = @()
foreach ($db in $dbList)
{
     $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName
     $dbMetrics = $dbMetrics + (Get-AzureRmMetric -ResourceId $dbResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)
}

#Optionally you can format hello metrics and output as .csv file using hello following script block.
$command = {
param($metricList, $outputFile)

# Format metrics into a table.
$table = @()
foreach($metric in $metricList) {
   foreach($metricValue in $metric.MetricValues) {
      $sx = New-Object PSObject -Property @{
      Timestamp = $metricValue.Timestamp.ToString()
      MetricName = $metric.Name;
      Average = $metricValue.Average;
      ResourceID = $metric.ResourceId
   }$table = $table += $sx
   }
}

# Output hello metrics into a .csv file.
write-output $table | Export-csv -Path $outputFile -Append -NoTypeInformation
}

# Format and output pool metrics
Invoke-Command -ScriptBlock $command -ArgumentList $poolMetrics,c:\temp\poolmetrics.csv

# Format and output database metrics
Invoke-Command -ScriptBlock $command -ArgumentList $dbMetrics,c:\temp\dbmetrics.csv
```

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="38440-217">Latência de operações do pool elástico</span><span class="sxs-lookup"><span data-stu-id="38440-217">Latency of elastic pool operations</span></span>
* <span data-ttu-id="38440-218">Alterar Olá min eDTUs por banco de dados ou o máximo de eDTUs por banco de dados normalmente é concluído em 5 minutos ou menos.</span><span class="sxs-lookup"><span data-stu-id="38440-218">Changing hello min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="38440-219">Alterar eDTUs Olá por pool de depende da quantidade total de saudação do espaço usado por todos os bancos de dados no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="38440-219">Changing hello eDTUs per pool depends on hello total amount of space used by all databases in hello pool.</span></span> <span data-ttu-id="38440-220">As alterações levam, em média, 90 minutos ou menos a cada 100 GB.</span><span class="sxs-lookup"><span data-stu-id="38440-220">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="38440-221">Por exemplo, se o espaço total Olá usado por todos os bancos de dados no pool de saudação é de 200 GB, Olá esperada de latência para mudar o eDTU do pool de saudação por pool é de 3 horas ou menos.</span><span class="sxs-lookup"><span data-stu-id="38440-221">For example, if hello total space used by all databases in hello pool is 200 GB, then hello expected latency for changing hello pool eDTU per pool is 3 hours or less.</span></span>



## <a name="next-steps"></a><span data-ttu-id="38440-222">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="38440-222">Next steps</span></span>
* <span data-ttu-id="38440-223">[Criar trabalhos Elásticos](sql-database-elastic-jobs-overview.md) trabalhos Elásticos permitem executar scripts T-SQL em relação a qualquer número de bancos de dados no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="38440-223">[Create elastic jobs](sql-database-elastic-jobs-overview.md) Elastic jobs let you run T-SQL scripts against any number of databases in hello pool.</span></span>
* <span data-ttu-id="38440-224">Consulte [expansão com o Azure SQL Database](sql-database-elastic-scale-introduction.md): usar ferramentas Elástico tooscale out, mover os dados, consultar ou criar transações.</span><span class="sxs-lookup"><span data-stu-id="38440-224">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic tools tooscale out, move data, query, or create transactions.</span></span>
