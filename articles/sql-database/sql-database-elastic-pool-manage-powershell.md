---
title: "PowerShell: Criar e gerenciar um pool elástico do SQL do Azure | Microsoft Docs"
description: "Saiba como usar o PowerShell para gerenciar um pool elástico."
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
ms.openlocfilehash: 5e76397c62e5a6ff7fb356bd81218c307f3fda31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a><span data-ttu-id="cd6ca-103">Criar e gerenciar um pool elástico com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="cd6ca-103">Create and manage an elastic pool with PowerShell</span></span>
<span data-ttu-id="cd6ca-104">Este tópico mostra como criar e gerenciar [pools elásticos](sql-database-elastic-pool.md) escalonáveis com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-104">This topic shows you how to create and manage scalable [elastic pools](sql-database-elastic-pool.md) with PowerShell.</span></span>  <span data-ttu-id="cd6ca-105">Você também pode criar e gerenciar um pool elástico do Azure usando o [portal do Azure](https://portal.azure.com/), a API REST ou o [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="cd6ca-105">You can also create and manage an Azure elastic pool using the [Azure portal](https://portal.azure.com/), REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="cd6ca-106">Você também pode criar e mover bancos de dados de e para os pools elásticos usando [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="cd6ca-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a><span data-ttu-id="cd6ca-107">Criar um pool elástico</span><span class="sxs-lookup"><span data-stu-id="cd6ca-107">Create an elastic pool</span></span>
<span data-ttu-id="cd6ca-108">O cmdlet [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cria um pool elástico.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-108">The [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet creates an elastic pool.</span></span> <span data-ttu-id="cd6ca-109">Os valores de eDTU por pool e DTUs mínimo e máximo são restringidos pelo valor da camada de serviço (Básico, Standard, Premium ou Premium RS).</span><span class="sxs-lookup"><span data-stu-id="cd6ca-109">The values for eDTU per pool, min, and max DTUs are constrained by the service tier value (Basic, Standard, Premium, or Premium RS).</span></span> <span data-ttu-id="cd6ca-110">Confira [Limites de eDTU e armazenamento para pools elásticos e bancos de dados em pool](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="cd6ca-110">See [eDTU and storage limits for elastic pools and pooled databases](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span></span>

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="cd6ca-111">Criar um banco de dados em pool em um pool elástico</span><span class="sxs-lookup"><span data-stu-id="cd6ca-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="cd6ca-112">Use o cmdlet [AzureRmSqlDatabase novo](/powershell/module/azurerm.sql/new-azurermsqldatabase) e defina o parâmetro **ElasticPoolName** para o pool de destino.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-112">Use the [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet and set the **ElasticPoolName** parameter to the target pool.</span></span> <span data-ttu-id="cd6ca-113">Para mover um banco de dados existente para um pool elástico, confira [Mover um banco de dados para um pool elástico](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span><span class="sxs-lookup"><span data-stu-id="cd6ca-113">To move an existing database into an elastic pool, see [Move a database into an elastic pool](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span></span>

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a><span data-ttu-id="cd6ca-114">Script completo</span><span class="sxs-lookup"><span data-stu-id="cd6ca-114">Complete script</span></span>
<span data-ttu-id="cd6ca-115">Esse script cria um grupo de recursos do Azure e um servidor.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-115">This script creates an Azure resource group and a server.</span></span> <span data-ttu-id="cd6ca-116">Quando solicitado, forneça um nome de usuário de administrador e uma senha para o novo servidor (e não as suas credenciais do Azure).</span><span class="sxs-lookup"><span data-stu-id="cd6ca-116">When prompted, supply an administrator username and password for the new server (not your Azure credentials).</span></span>

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

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a><span data-ttu-id="cd6ca-117">Criar um pool elástico e adicionar vários bancos de dados em pool</span><span class="sxs-lookup"><span data-stu-id="cd6ca-117">Create an elastic pool and add multiple pooled databases</span></span>
<span data-ttu-id="cd6ca-118">A criação de muitos bancos de dados em um pool elástico pode levar tempo quando feito usando o portal ou cmdlets do PowerShell que criam apenas um banco de dados individual por vez.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-118">Creation of many databases in an elastic pool can take time when done using the portal or PowerShell cmdlets that create only a single database at a time.</span></span> <span data-ttu-id="cd6ca-119">Para automatizar a criação em um pool elástico, confira [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span><span class="sxs-lookup"><span data-stu-id="cd6ca-119">To automate creation into an elastic pool, see [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="cd6ca-120">Mover um banco de dados para um pool elástico</span><span class="sxs-lookup"><span data-stu-id="cd6ca-120">Move a database into an elastic pool</span></span>
<span data-ttu-id="cd6ca-121">Você pode mover um banco de dados para dentro ou para fora de um pool elástico com [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span><span class="sxs-lookup"><span data-stu-id="cd6ca-121">You can move a database into or out of an elastic pool with the [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span></span>

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="cd6ca-122">Alterar as configurações de desempenho de um pool elástico</span><span class="sxs-lookup"><span data-stu-id="cd6ca-122">Change performance settings of an elastic pool</span></span>
<span data-ttu-id="cd6ca-123">Quando o desempenho for afetado, você pode alterar as configurações do pool para acomodar o crescimento.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-123">When performance suffers, you can change the settings of the pool to accommodate growth.</span></span> <span data-ttu-id="cd6ca-124">Use o cmdlet [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span><span class="sxs-lookup"><span data-stu-id="cd6ca-124">Use the [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet.</span></span> <span data-ttu-id="cd6ca-125">Defina o parâmetro - Dtu para as eDTUs por pool.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-125">Set the -Dtu parameter to the eDTUs per pool.</span></span> <span data-ttu-id="cd6ca-126">Consulte os valores possível em [limites de armazenamento e eDTU](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="cd6ca-126">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-the-storage-limit-for-an-elastic-pool"></a><span data-ttu-id="cd6ca-127">Alterar o limite de armazenamento para um pool elástico</span><span class="sxs-lookup"><span data-stu-id="cd6ca-127">Change the storage limit for an elastic pool</span></span>

<span data-ttu-id="cd6ca-128">Use o cmdlet [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) para definir o parâmetro _-StorageMB_.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-128">Use the [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet to set the _-StorageMB_ parameter.</span></span> <span data-ttu-id="cd6ca-129">Forneça o limite de armazenamento em MB (por exemplo, 2097152 define o limite de armazenamento como 2 TB).</span><span class="sxs-lookup"><span data-stu-id="cd6ca-129">Provide the storage limit in MB (for example, 2097152 sets the storage limit to 2 TB).</span></span> <span data-ttu-id="cd6ca-130">Consulte os valores possível em [limites de armazenamento e eDTU](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="cd6ca-130">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cd6ca-131">O armazenamento de dados máximo padrão por pool para pools Premium com 1500 eDTUs ou mais são 750 GB.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-131">The default max data storage per pool for Premium pools with 1500 eDTUs or more is 750 GB.</span></span> <span data-ttu-id="cd6ca-132">Para obter o _tamanho máximo de armazenamento de dados por pool_ mais alto, o limite de armazenamento deve ser explicitamente definido.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-132">To obtain the higher _max data storage size per pool_, the storage limit must be explicitly set.</span></span> <span data-ttu-id="cd6ca-133">Os pools Premium com mais de 750 GB de armazenamento estão atualmente em versão prévia pública nas seguintes regiões: Leste dos EUA 2, Oeste dos EUA, US Gov – Virginia, Europa Ocidental, Alemanha Central, Sudeste Asiático, Leste do Japão, Leste da Austrália, Canadá Central e Leste do Canadá.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-133">Premium pools with more than 750 GB of storage is currently in public preview in the following regions: East US 2, West US, US Gov Virginia, West Europe, Germany Central, Southeast Asia, Japan East, Australia East, Canada Central, and Canada East.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-the-status-of-pool-operations"></a><span data-ttu-id="cd6ca-134">Obter o status das operações de pool</span><span class="sxs-lookup"><span data-stu-id="cd6ca-134">Get the status of pool operations</span></span>
<span data-ttu-id="cd6ca-135">Criar um pool elástico pode levar tempo.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-135">Creating an elastic pool can take time.</span></span> <span data-ttu-id="cd6ca-136">Para acompanhar o status das operações de pool, incluindo a criação e as atualizações, use o cmdlet [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity).</span><span class="sxs-lookup"><span data-stu-id="cd6ca-136">To track the status of pool operations including creation and updates, use the [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-the-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a><span data-ttu-id="cd6ca-137">Obter o status de movimentação de um banco de dados para dentro e fora de um pool elástico</span><span class="sxs-lookup"><span data-stu-id="cd6ca-137">Get the status of moving a database into and out of an elastic pool</span></span>
<span data-ttu-id="cd6ca-138">Mover um banco de dados pode levar tempo.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-138">Moving a database can take time.</span></span> <span data-ttu-id="cd6ca-139">Acompanhe o status da movimentação usando o cmdlet [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity).</span><span class="sxs-lookup"><span data-stu-id="cd6ca-139">Track a move status using the [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="cd6ca-140">Obter dados de uso de recursos para um pool elástico</span><span class="sxs-lookup"><span data-stu-id="cd6ca-140">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="cd6ca-141">Métricas que podem ser recuperadas como uma porcentagem do limite do pool de recursos:</span><span class="sxs-lookup"><span data-stu-id="cd6ca-141">Metrics that can be retrieved as a percentage of the resource pool limit:</span></span>

| <span data-ttu-id="cd6ca-142">Nome da métrica</span><span class="sxs-lookup"><span data-stu-id="cd6ca-142">Metric name</span></span> | <span data-ttu-id="cd6ca-143">Descrição</span><span class="sxs-lookup"><span data-stu-id="cd6ca-143">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cd6ca-144">cpu\_percent</span><span class="sxs-lookup"><span data-stu-id="cd6ca-144">cpu\_percent</span></span> |<span data-ttu-id="cd6ca-145">Média de utilização da computação em percentual do limite do pool.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-145">Average compute utilization in percentage of the limit of the pool.</span></span> |
| <span data-ttu-id="cd6ca-146">physical\_data\_read\_percent</span><span class="sxs-lookup"><span data-stu-id="cd6ca-146">physical\_data\_read\_percent</span></span> |<span data-ttu-id="cd6ca-147">Média de utilização de E/S em percentual do limite do pool.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-147">Average I/O utilization in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="cd6ca-148">log\_write\_percent</span><span class="sxs-lookup"><span data-stu-id="cd6ca-148">log\_write\_percent</span></span> |<span data-ttu-id="cd6ca-149">Média de utilização dos recursos de gravação em percentual do limite do pool.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-149">Average write resource utilization in percentage of the limit of the pool.</span></span> |
| <span data-ttu-id="cd6ca-150">DTU\_consumption\_percent</span><span class="sxs-lookup"><span data-stu-id="cd6ca-150">DTU\_consumption\_percent</span></span> |<span data-ttu-id="cd6ca-151">Média de utilização de eDTUs em percentual do limite de eDTUs do pool</span><span class="sxs-lookup"><span data-stu-id="cd6ca-151">Average eDTU utilization in percentage of eDTU limit for the pool</span></span> |
| <span data-ttu-id="cd6ca-152">storage\_percent</span><span class="sxs-lookup"><span data-stu-id="cd6ca-152">storage\_percent</span></span> |<span data-ttu-id="cd6ca-153">Média de utilização do armazenamento em percentual do limite de armazenamento do pool.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-153">Average storage utilization in percentage of the storage limit of the pool.</span></span> |
| <span data-ttu-id="cd6ca-154">workers\_percent</span><span class="sxs-lookup"><span data-stu-id="cd6ca-154">workers\_percent</span></span> |<span data-ttu-id="cd6ca-155">Máximo de trabalhos (solicitações) simultâneos em percentual, com base no limite do pool.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-155">Maximum concurrent workers (requests) in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="cd6ca-156">sessions\_percent</span><span class="sxs-lookup"><span data-stu-id="cd6ca-156">sessions\_percent</span></span> |<span data-ttu-id="cd6ca-157">Número máximo de sessões simultâneas em percentual, com base no limite do pool.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-157">Maximum concurrent sessions in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="cd6ca-158">eDTU_limit</span><span class="sxs-lookup"><span data-stu-id="cd6ca-158">eDTU_limit</span></span> |<span data-ttu-id="cd6ca-159">Configuração atual de DTUs máximas do pool elástico para este pool elástico durante este intervalo.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-159">Current max elastic pool DTU setting for this elastic pool during this interval.</span></span> |
| <span data-ttu-id="cd6ca-160">storage\_limit</span><span class="sxs-lookup"><span data-stu-id="cd6ca-160">storage\_limit</span></span> |<span data-ttu-id="cd6ca-161">Configuração atual de limite máximo de armazenamento do pool elástico para este pool elástico em megabytes durante este intervalo.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-161">Current max elastic pool storage limit setting for this elastic pool in megabytes during this interval.</span></span> |
| <span data-ttu-id="cd6ca-162">eDTU\_used</span><span class="sxs-lookup"><span data-stu-id="cd6ca-162">eDTU\_used</span></span> |<span data-ttu-id="cd6ca-163">Média de eDTUs usadas pelo pool neste intervalo.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-163">Average eDTUs used by the pool in this interval.</span></span> |
| <span data-ttu-id="cd6ca-164">storage\_used</span><span class="sxs-lookup"><span data-stu-id="cd6ca-164">storage\_used</span></span> |<span data-ttu-id="cd6ca-165">Média de armazenamento usado pelo pool neste intervalo em bytes</span><span class="sxs-lookup"><span data-stu-id="cd6ca-165">Average storage used by the pool in this interval in bytes</span></span> |

<span data-ttu-id="cd6ca-166">**Períodos de retenção/granularidade das métricas:**</span><span class="sxs-lookup"><span data-stu-id="cd6ca-166">**Metrics granularity/retention periods:**</span></span>

* <span data-ttu-id="cd6ca-167">Os dados retornam com uma granularidade de cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-167">Data is returned at 5-minute granularity.</span></span>  
* <span data-ttu-id="cd6ca-168">A retenção dos dados é de 35 dias.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-168">Data retention is 35 days.</span></span>  

<span data-ttu-id="cd6ca-169">Esse cmdlet e a API limitam o número de linhas que podem ser recuperadas em uma chamada para 1000 linhas (cerca de três dias de dados a uma granularidade de cinco minutos).</span><span class="sxs-lookup"><span data-stu-id="cd6ca-169">This cmdlet and API limits the number of rows that can be retrieved in one call to 1000 rows (about 3 days of data at 5-minute granularity).</span></span> <span data-ttu-id="cd6ca-170">Mas esse comando pode ser chamado várias vezes com intervalos de tempo de início/término diferentes para recuperar mais dados</span><span class="sxs-lookup"><span data-stu-id="cd6ca-170">But this command can be called multiple times with different start/end time intervals to retrieve more data</span></span>

<span data-ttu-id="cd6ca-171">Para recuperar as métricas:</span><span class="sxs-lookup"><span data-stu-id="cd6ca-171">To retrieve the metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a><span data-ttu-id="cd6ca-172">Obter dados de uso de recursos de um banco de dados em um pool elástico</span><span class="sxs-lookup"><span data-stu-id="cd6ca-172">Get resource usage data for a database in an elastic pool</span></span>
<span data-ttu-id="cd6ca-173">Essas APIs são as mesmas que as APIs usadas para monitorar a utilização de recursos de um banco de dados individual, exceto quanto às seguintes diferenças semânticas: as métricas recuperadas são expressas como um percentual do eDTUs máximo do banco de dados (ou o limite equivalente para a métrica subjacente, como CPU ou E/S) definida para esse pool.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-173">These APIs are the same as the APIs used for monitoring the resource utilization of a single database, except for the following semantic difference: metrics retrieved are expressed as a percentage of the per database max eDTUs (or equivalent cap for the underlying metric like CPU or IO) set for that pool.</span></span> <span data-ttu-id="cd6ca-174">Por exemplo, 50% da utilização de qualquer uma dessas métricas indica que o consumo do recursos específico é de 50% do limite por banco de dados desse recurso no pool pai.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-174">For example, 50% utilization of any of these metrics indicates that the specific resource consumption is at 50% of the per database cap limit for that resource in the parent pool.</span></span>

<span data-ttu-id="cd6ca-175">Para recuperar as métricas:</span><span class="sxs-lookup"><span data-stu-id="cd6ca-175">To retrieve the metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-to-an-elastic-pool-resource"></a><span data-ttu-id="cd6ca-176">Adicionar um alerta para um recurso de pool elástico</span><span class="sxs-lookup"><span data-stu-id="cd6ca-176">Add an alert to an elastic pool resource</span></span>
<span data-ttu-id="cd6ca-177">Você pode adicionar regras de alerta a um pool elástico para enviar notificações de email ou cadeias de caracteres de alerta para [pontos de extremidade da URL](https://msdn.microsoft.com/library/mt718036.aspx) quando o pool elástico atingir um limite de utilização que você configurou.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-177">You can add alert rules to an elastic pool to send email notifications or alert strings to [URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when the elastic pool hits a utilization threshold that you set up.</span></span> <span data-ttu-id="cd6ca-178">Use o cmdlet Add-AzureRmMetricAlertRule.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-178">Use the Add-AzureRmMetricAlertRule cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cd6ca-179">O monitoramento de utilização de recursos para pools elásticos tem um atraso de, pelo menos, 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-179">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="cd6ca-180">No momento, não é permitido definir alertas de menos de 10 minutos para pools elásticos.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-180">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="cd6ca-181">Todos os alertas definidos para pools Elásticos com um ponto (chamado de parâmetro "-Tamanho_da_janela" na API do PowerShell) de menos de 10 minutos pode não ser disparada.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-181">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="cd6ca-182">Certifique-se de que todos os alertas definidos para pools elásticos usem um período (WindowSize) de 10 minutos ou mais.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-182">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>
>

<span data-ttu-id="cd6ca-183">Este exemplo adiciona um alerta para ser notificado quando o consumo de eDTU de um pool elástico ultrapassar determinado limite.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-183">This example adds an alert for getting notified when an elastic pool’s eDTU consumption goes above certain threshold.</span></span>

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

<span data-ttu-id="cd6ca-184">Para obter mais informações, confira [criar alertas do Banco de Dados SQL no portal do Azure](sql-database-insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cd6ca-184">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="add-alerts-to-all-databases-in-an-elastic-pool"></a><span data-ttu-id="cd6ca-185">Adicionar alertas para todos os bancos de dados em um pool elástico</span><span class="sxs-lookup"><span data-stu-id="cd6ca-185">Add alerts to all databases in an elastic pool</span></span>
<span data-ttu-id="cd6ca-186">Você pode adicionar regras de alerta a todos os bancos de dados em um pool elástico para enviar notificações por email ou cadeias de caracteres de alerta para [pontos de extremidade de URL](https://msdn.microsoft.com/library/mt718036.aspx) quando um recurso atingir um limite de utilização configurado pelo alerta.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-186">You can add alert rules to all database in an elastic pool to send email notifications or alert strings to [URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when a resource hits a utilization threshold set up by the alert.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cd6ca-187">O monitoramento de utilização de recursos para pools elásticos tem um atraso de, pelo menos, 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-187">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="cd6ca-188">No momento, não é permitido definir alertas de menos de 10 minutos para pools elásticos.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-188">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="cd6ca-189">Todos os alertas definidos para pools Elásticos com um ponto (chamado de parâmetro "-Tamanho_da_janela" na API do PowerShell) de menos de 10 minutos pode não ser disparada.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-189">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="cd6ca-190">Certifique-se de que todos os alertas definidos para pools elásticos usem um período (WindowSize) de 10 minutos ou mais.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-190">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>

<span data-ttu-id="cd6ca-191">Este exemplo adiciona um alerta a cada banco de dados em um pool elástico para ser notificado quando consumo de DTU do banco de dados ficar acima de um determinado limite.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-191">This example adds an alert to each of the databases in an elastic pool for getting notified when that database’s DTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location = '<location'                          # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

# Get the list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# Get resource usage metrics for a database in an elastic pool for the specified time interval.
foreach ($db in $dbList)
{
    $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName

    # create a unique rule name
    $alertName = $db.DatabaseName + "- DTU consumption rule"

    # Create an alert rule for DTU_consumption_percent
    Add-AzureRMMetricAlertRule -Name $alertName  -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $dbResourceId -MetricName "dtu_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail

    # drop the alert rule
    #Remove-AzureRmAlertRule -ResourceGroup $resourceGroupName -Name $alertName
}
```

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a><span data-ttu-id="cd6ca-192">Coletar e monitorar dados de uso de recursos em vários pools em uma assinatura</span><span class="sxs-lookup"><span data-stu-id="cd6ca-192">Collect and monitor resource usage data across multiple pools in a subscription</span></span>
<span data-ttu-id="cd6ca-193">Quando você tiver muitos bancos de dados em uma assinatura, é complicado monitorar cada pool elástico separadamente.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-193">When you have many databases in a subscription, it is cumbersome to monitor each elastic pool separately.</span></span> <span data-ttu-id="cd6ca-194">Em vez disso, os cmdlets do PowerShell do Banco de Dados SQL e consultas T-SQL podem ser combinadas para coletar dados de uso de recursos de vários pools e bancos de dados para monitoramento e análise de uso de recursos.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-194">Instead, SQL database PowerShell cmdlets and T-SQL queries can be combined to collect resource usage data from multiple pools and their databases for monitoring and analysis of resource usage.</span></span> <span data-ttu-id="cd6ca-195">Uma [implementação de exemplo](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) de tal conjunto de scripts do powershell pode ser encontrada no repositório de exemplos do SQL Server no GitHub com a documentação sobre o que ele faz e como usá-lo.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-195">A [sample implementation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) of such a set of powershell scripts can be found in the GitHub SQL Server samples repository along with documentation on what it does and how to use it.</span></span>

<span data-ttu-id="cd6ca-196">Para usar esta implementação de exemplo, siga estas etapas.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-196">To use this sample implementation, follow these steps.</span></span>

1. <span data-ttu-id="cd6ca-197">Baixe os [scripts e a documentação](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span><span class="sxs-lookup"><span data-stu-id="cd6ca-197">Download the [scripts and documentation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span></span>
2. <span data-ttu-id="cd6ca-198">Modifique os scripts para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-198">Modify the scripts for your environment.</span></span> <span data-ttu-id="cd6ca-199">Especifique um ou mais servidores nos quais os pools elásticos são hospedados.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-199">Specify one or more servers on which elastic pools are hosted.</span></span>
3. <span data-ttu-id="cd6ca-200">Especifique um banco de dados de telemetria no qual as métricas coletadas serão armazenadas.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-200">Specify a telemetry database where the collected metrics are to be stored.</span></span>
4. <span data-ttu-id="cd6ca-201">Personalize o script para especificar a duração da execução de scripts.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-201">Customize the script to specify the duration of the scripts' execution.</span></span>

<span data-ttu-id="cd6ca-202">Em um alto nível, os scripts fazem o seguinte:</span><span class="sxs-lookup"><span data-stu-id="cd6ca-202">At a high level, the scripts do the following:</span></span>

* <span data-ttu-id="cd6ca-203">Enumera todos os servidores em uma determinada assinatura do Azure (ou uma lista de servidores específicos).</span><span class="sxs-lookup"><span data-stu-id="cd6ca-203">Enumerates all servers in a given Azure subscription (or a specified list of servers).</span></span>
* <span data-ttu-id="cd6ca-204">Executa um trabalho em segundo plano para cada servidor.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-204">Runs a background job for each server.</span></span> <span data-ttu-id="cd6ca-205">O trabalho é executado em um loop em intervalos regulares e coleta dados de telemetria de todos os pools no servidor.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-205">The job runs in a loop at regular intervals and collects telemetry data for all the pools in the server.</span></span> <span data-ttu-id="cd6ca-206">Em seguida, ele carrega os dados coletados no banco de dados de telemetria especificado.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-206">It then loads the collected data into the specified telemetry database.</span></span>
* <span data-ttu-id="cd6ca-207">Enumera uma lista de bancos de dados em cada pool para coletar os dados de uso de recursos do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-207">Enumerates a list of databases in each pool to collect the database resource usage data.</span></span> <span data-ttu-id="cd6ca-208">Em seguida, ele carrega os dados coletados no banco de dados de telemetria.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-208">It then loads the collected data into the telemetry database.</span></span>

<span data-ttu-id="cd6ca-209">As métricas coletadas no banco de dados de telemetria podem ser analisadas para monitorar a integridade dos pools elásticos e os bancos de dados nele.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-209">The collected metrics in the telemetry database can be analyzed to monitor the health of elastic pools and the databases in it.</span></span> <span data-ttu-id="cd6ca-210">O script também instala uma TVF (função Tabela-Valor) predefinida no banco de dados de telemetria para ajudar a agregar as métricas para um período específico.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-210">The script also installs a pre-defined Table-Value function (TVF) in the telemetry database to help aggregate the metrics for a specified time window.</span></span> <span data-ttu-id="cd6ca-211">Por exemplo, os resultados da TVF podem ser usados para mostrar "principais pools elásticos N” com a utilização de eDTU máxima em uma determinada janela de tempo".</span><span class="sxs-lookup"><span data-stu-id="cd6ca-211">For example, results of the TVF can be used to show “top N elastic pools with the maximum eDTU utilization in a given time window.”</span></span> <span data-ttu-id="cd6ca-212">Outra opção é usar ferramentas analíticas como o Excel ou o Power BI para consultar e analisar os dados coletados.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-212">Optionally, use analytic tools like Excel or Power BI to query and analyze the collected data.</span></span>

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a><span data-ttu-id="cd6ca-213">Exemplo: recuperar as métricas de consumo de recursos para um pool elástico e seus bancos de dados</span><span class="sxs-lookup"><span data-stu-id="cd6ca-213">Example: retrieve resource consumption metrics for an elastic pool and its databases</span></span>
<span data-ttu-id="cd6ca-214">Este exemplo recupera as métricas de consumo para um determinado pool elástico e todos os seus bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-214">This example retrieves the consumption metrics for a given elastic pool and all its databases.</span></span> <span data-ttu-id="cd6ca-215">Os dados coletados são formatados e gravados em um arquivo formatado. csv.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-215">Collected data is formatted and written to a .csv formatted file.</span></span> <span data-ttu-id="cd6ca-216">O arquivo pode ser navegado com o Excel.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-216">The file can be browsed with Excel.</span></span>

```PowerShell
$subscriptionId = '<Azure subscription id>'          # Azure subscription ID
$resourceGroupName = '<resource group name>'             # Resource Group
$serverName = <server name>                              # server name
$poolName = <elastic pool name>                          # pool name

# Login to Azure account and select the subscription.
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

# Get resource usage metrics for an elastic pool for the specified time interval.
$startTime = '4/27/2016 00:00:00'  # start time in UTC
$endTime = '4/27/2016 01:00:00'    # end time in UTC

# Construct the pool resource ID and retrive pool metrics at 5-minute granularity.
$poolResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticPools/' + $poolName
$poolMetrics = (Get-AzureRmMetric -ResourceId $poolResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)

# Get the list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Get resource usage metrics for a database in an elastic pool for the specified time interval.
$dbMetrics = @()
foreach ($db in $dbList)
{
     $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName
     $dbMetrics = $dbMetrics + (Get-AzureRmMetric -ResourceId $dbResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)
}

#Optionally you can format the metrics and output as .csv file using the following script block.
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

# Output the metrics into a .csv file.
write-output $table | Export-csv -Path $outputFile -Append -NoTypeInformation
}

# Format and output pool metrics
Invoke-Command -ScriptBlock $command -ArgumentList $poolMetrics,c:\temp\poolmetrics.csv

# Format and output database metrics
Invoke-Command -ScriptBlock $command -ArgumentList $dbMetrics,c:\temp\dbmetrics.csv
```

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="cd6ca-217">Latência de operações do pool elástico</span><span class="sxs-lookup"><span data-stu-id="cd6ca-217">Latency of elastic pool operations</span></span>
* <span data-ttu-id="cd6ca-218">Normalmente, a alteração das eDTUs mínimas ou das eDTUs máximas por banco de dados é um processo concluído em cinco minutos ou menos.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-218">Changing the min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="cd6ca-219">A alteração do limite de eDTUs por pool depende da quantidade total de espaço usado por todos os bancos de dados no pool.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-219">Changing the eDTUs per pool depends on the total amount of space used by all databases in the pool.</span></span> <span data-ttu-id="cd6ca-220">As alterações levam, em média, 90 minutos ou menos a cada 100 GB.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-220">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="cd6ca-221">Por exemplo, se o espaço total usado por todos os bancos de dados no pool for de 200 GB, a latência prevista para alterar os eDTUs do pool será de 3 horas por pool ou menos.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-221">For example, if the total space used by all databases in the pool is 200 GB, then the expected latency for changing the pool eDTU per pool is 3 hours or less.</span></span>



## <a name="next-steps"></a><span data-ttu-id="cd6ca-222">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cd6ca-222">Next steps</span></span>
* <span data-ttu-id="cd6ca-223">[Criar trabalhos elásticos](sql-database-elastic-jobs-overview.md) Os trabalhos elásticos permitem a execução de scripts T-SQL em vários bancos de dados no pool.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-223">[Create elastic jobs](sql-database-elastic-jobs-overview.md) Elastic jobs let you run T-SQL scripts against any number of databases in the pool.</span></span>
* <span data-ttu-id="cd6ca-224">Confira [Escalando horizontalmente com o Banco de Dados SQL do Azure](sql-database-elastic-scale-introduction.md): use ferramentas elásticas para escalar horizontalmente, mover os dados, consultar ou criar transações.</span><span class="sxs-lookup"><span data-stu-id="cd6ca-224">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic tools to scale out, move data, query, or create transactions.</span></span>
