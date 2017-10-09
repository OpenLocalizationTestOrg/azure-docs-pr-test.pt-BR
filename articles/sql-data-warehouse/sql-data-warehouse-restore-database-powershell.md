---
title: aaaRestore um Data Warehouse do SQL Azure (PowerShell) | Microsoft Docs
description: Tarefas do PowerShell para restaurar um Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: ac62f154-c8b0-4c33-9c42-f480808aa1d2
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: aa29a315080b1ed477cc6a051ce15a3202630cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="41b31-103">Restaurar um Azure SQL Data Warehouse (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="41b31-103">Restore an Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="41b31-104">[Visão geral][Overview]</span><span class="sxs-lookup"><span data-stu-id="41b31-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="41b31-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="41b31-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="41b31-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="41b31-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="41b31-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="41b31-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="41b31-108">Neste artigo, você aprenderá como toorestore um Azure SQL Data Warehouse usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="41b31-108">In this article you will learn how toorestore an Azure SQL Data Warehouse using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="41b31-109">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="41b31-109">Before you begin</span></span>
<span data-ttu-id="41b31-110">**Verifique sua capacidade de DTU.**</span><span class="sxs-lookup"><span data-stu-id="41b31-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="41b31-111">Cada SQL Data Warehouse é hospedado por um servidor SQL (por exemplo, myserver.database.windows.net) que tem uma cota de DTU padrão.</span><span class="sxs-lookup"><span data-stu-id="41b31-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="41b31-112">Antes de poder restaurar um SQL Data Warehouse, verifique se esse saudação que do SQL server tem suficiente restante cota de DTU para o banco de dados de hello está sendo restaurado.</span><span class="sxs-lookup"><span data-stu-id="41b31-112">Before you can restore a SQL Data Warehouse, verify that hello your SQL server has enough remaining DTU quota for hello database being restored.</span></span> <span data-ttu-id="41b31-113">toolearn como toocalculate DTU necessário ou toorequest mais DTU, consulte [solicitar uma alteração de cota DTU][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="41b31-113">toolearn how toocalculate DTU needed or toorequest more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="41b31-114">Instalar o PowerShell</span><span class="sxs-lookup"><span data-stu-id="41b31-114">Install PowerShell</span></span>
<span data-ttu-id="41b31-115">Ordem toouse PowerShell do Azure SQL Data warehouse, você precisará tooinstall Azure PowerShell versão 1.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="41b31-115">In order toouse Azure PowerShell with SQL Data Warehouse, you will need tooinstall Azure PowerShell version 1.0 or greater.</span></span>  <span data-ttu-id="41b31-116">Você pode verificar a versão executando **Get-Module -ListAvailable -Name AzureRM**.</span><span class="sxs-lookup"><span data-stu-id="41b31-116">You can check your version by running **Get-Module -ListAvailable -Name AzureRM**.</span></span>  <span data-ttu-id="41b31-117">versão mais recente do Hello pode ser instalado do [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="41b31-117">hello latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="41b31-118">Para obter mais informações sobre como instalar a versão mais recente do hello, consulte [como tooinstall e configurar o Azure PowerShell][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="41b31-118">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="41b31-119">Restaurar um banco de dados ativo ou pausado</span><span class="sxs-lookup"><span data-stu-id="41b31-119">Restore an active or paused database</span></span>
<span data-ttu-id="41b31-120">toorestore um banco de dados de um instantâneo usar Olá [restauração AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="41b31-120">toorestore a database from a snapshot use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] PowerShell cmdlet.</span></span>

1. <span data-ttu-id="41b31-121">Abra o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="41b31-121">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="41b31-122">Conecte-se tooyour conta do Azure e listar todas as assinaturas de saudação associadas à sua conta.</span><span class="sxs-lookup"><span data-stu-id="41b31-122">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="41b31-123">Selecione a assinatura de saudação que contém a saudação toobe de banco de dados restaurado.</span><span class="sxs-lookup"><span data-stu-id="41b31-123">Select hello subscription that contains hello database toobe restored.</span></span>
4. <span data-ttu-id="41b31-124">Olá lista pontos para banco de dados de saudação de restauração.</span><span class="sxs-lookup"><span data-stu-id="41b31-124">List hello restore points for hello database.</span></span>
5. <span data-ttu-id="41b31-125">Selecione o ponto de restauração Olá desejado usando Olá RestorePointCreationDate.</span><span class="sxs-lookup"><span data-stu-id="41b31-125">Pick hello desired restore point using hello RestorePointCreationDate.</span></span>
6. <span data-ttu-id="41b31-126">Ponto de restauração de toohello desejado Olá banco de dados de restauração.</span><span class="sxs-lookup"><span data-stu-id="41b31-126">Restore hello database toohello desired restore point.</span></span>
7. <span data-ttu-id="41b31-127">Verifique se o que banco de dados restaurado de saudação está online.</span><span class="sxs-lookup"><span data-stu-id="41b31-127">Verify that hello restored database is online.</span></span>

```Powershell

$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# List hello last 10 database restore points
((Get-AzureRMSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName ($DatabaseName).RestorePointCreationDate)[-10 .. -1]

# Or list all restore points
Get-AzureRmSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Get hello specific database toorestore
$Database = Get-AzureRmSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Pick desired restore point using RestorePointCreationDate
$PointInTime="<RestorePointCreationDate>"  

# Restore database from a restore point
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromPointInTimeBackup –PointInTime $PointInTime -ResourceGroupName $Database.ResourceGroupName -ServerName $Database.$ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $Database.ResourceID

# Verify hello status of restored database
$RestoredDatabase.status

```

> [!NOTE]
> <span data-ttu-id="41b31-128">Após a restauração hello, você pode configurar o banco de dados recuperado seguindo [configurar seu banco de dados após a recuperação][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="41b31-128">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="41b31-129">Restaurar um banco de dados excluído</span><span class="sxs-lookup"><span data-stu-id="41b31-129">Restore a deleted database</span></span>
<span data-ttu-id="41b31-130">toorestore um banco de dados excluído, use Olá [restauração AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet.</span><span class="sxs-lookup"><span data-stu-id="41b31-130">toorestore a deleted database, use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="41b31-131">Abra o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="41b31-131">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="41b31-132">Conecte-se tooyour conta do Azure e listar todas as assinaturas de saudação associadas à sua conta.</span><span class="sxs-lookup"><span data-stu-id="41b31-132">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="41b31-133">Excluir a assinatura de saudação Select que contém Olá toobe de banco de dados restaurado.</span><span class="sxs-lookup"><span data-stu-id="41b31-133">Select hello subscription that contains hello deleted database toobe restored.</span></span>
4. <span data-ttu-id="41b31-134">Obter banco de dados específico Olá excluído.</span><span class="sxs-lookup"><span data-stu-id="41b31-134">Get hello specific deleted database.</span></span>
5. <span data-ttu-id="41b31-135">Restaure o banco de dados de saudação excluído.</span><span class="sxs-lookup"><span data-stu-id="41b31-135">Restore hello deleted database.</span></span>
6. <span data-ttu-id="41b31-136">Verifique se o que banco de dados restaurado de saudação está online.</span><span class="sxs-lookup"><span data-stu-id="41b31-136">Verify that hello restored database is online.</span></span>

```Powershell
$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Get hello deleted database toorestore
$DeletedDatabase = Get-AzureRmSqlDeletedDatabaseBackup -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Restore deleted database
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromDeletedDatabaseBackup –DeletionDate $DeletedDatabase.DeletionDate -ResourceGroupName $DeletedDatabase.ResourceGroupName -ServerName $DeletedDatabase.ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $DeletedDatabase.ResourceID

# Verify hello status of restored database
$RestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="41b31-137">Após a restauração hello, você pode configurar o banco de dados recuperado seguindo [configurar seu banco de dados após a recuperação][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="41b31-137">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a><span data-ttu-id="41b31-138">Restaurar por meio de uma região geográfica do Azure</span><span class="sxs-lookup"><span data-stu-id="41b31-138">Restore from an Azure geographical region</span></span>
<span data-ttu-id="41b31-139">toorecover um banco de dados, use Olá [restauração AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet.</span><span class="sxs-lookup"><span data-stu-id="41b31-139">toorecover a database, use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="41b31-140">Abra o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="41b31-140">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="41b31-141">Conecte-se tooyour conta do Azure e listar todas as assinaturas de saudação associadas à sua conta.</span><span class="sxs-lookup"><span data-stu-id="41b31-141">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="41b31-142">Selecione a assinatura de saudação que contém a saudação toobe de banco de dados restaurado.</span><span class="sxs-lookup"><span data-stu-id="41b31-142">Select hello subscription that contains hello database toobe restored.</span></span>
4. <span data-ttu-id="41b31-143">Obter toorecover de saudação banco de dados.</span><span class="sxs-lookup"><span data-stu-id="41b31-143">Get hello database you want toorecover.</span></span>
5. <span data-ttu-id="41b31-144">Crie solicitação de recuperação de saudação do banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="41b31-144">Create hello recovery request for hello database.</span></span>
6. <span data-ttu-id="41b31-145">Verificar o status de saudação do banco de dados restaurado geográfica do hello.</span><span class="sxs-lookup"><span data-stu-id="41b31-145">Verify hello status of hello geo-restored database.</span></span>

```Powershell
Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName "<Subscription_name>"

# Get hello database you want toorecover
$GeoBackup = Get-AzureRmSqlDatabaseGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourServerName>" -DatabaseName "<YourDatabaseName>"

# Recover database
$GeoRestoredDatabase = Restore-AzureRmSqlDatabase –FromGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourTargetServer>" -TargetDatabaseName "<NewDatabaseName>" –ResourceId $GeoBackup.ResourceID

# Verify that hello geo-restored database is online
$GeoRestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="41b31-146">tooconfigure seu banco de dados após a restauração hello, consulte [configurar seu banco de dados após a recuperação][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="41b31-146">tooconfigure your database after hello restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

<span data-ttu-id="41b31-147">saudação de banco de dados recuperado será habilitado para TDE se o banco de dados de origem de saudação é habilitado para TDE.</span><span class="sxs-lookup"><span data-stu-id="41b31-147">hello recovered database will be TDE-enabled if hello source database is TDE-enabled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="41b31-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="41b31-148">Next steps</span></span>
<span data-ttu-id="41b31-149">toolearn sobre recursos de continuidade de negócios Olá de edições de banco de dados de SQL do Azure, leia Olá [visão geral de continuidade de negócios do Azure SQL Database][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="41b31-149">toolearn about hello business continuity features of Azure SQL Database editions, please read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery

<!--MSDN references-->
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
