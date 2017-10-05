---
title: Restaurar um Azure SQL Data Warehouse (PowerShell) | Microsoft Docs
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
ms.openlocfilehash: 6286c0e682bae2d3bf0435a25b8077a53b117b25
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="628d6-103">Restaurar um Azure SQL Data Warehouse (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="628d6-103">Restore an Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="628d6-104">[Visão geral][Overview]</span><span class="sxs-lookup"><span data-stu-id="628d6-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="628d6-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="628d6-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="628d6-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="628d6-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="628d6-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="628d6-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="628d6-108">Neste artigo, você aprenderá como restaurar um Azure SQL Data Warehouse usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="628d6-108">In this article you will learn how to restore an Azure SQL Data Warehouse using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="628d6-109">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="628d6-109">Before you begin</span></span>
<span data-ttu-id="628d6-110">**Verifique sua capacidade de DTU.**</span><span class="sxs-lookup"><span data-stu-id="628d6-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="628d6-111">Cada SQL Data Warehouse é hospedado por um servidor SQL (por exemplo, myserver.database.windows.net) que tem uma cota de DTU padrão.</span><span class="sxs-lookup"><span data-stu-id="628d6-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="628d6-112">Antes de restaurar um SQL Data Warehouse, verifique se o SQL Server tem cota de DTU suficiente restante para o banco de dados que está sendo restaurado.</span><span class="sxs-lookup"><span data-stu-id="628d6-112">Before you can restore a SQL Data Warehouse, verify that the your SQL server has enough remaining DTU quota for the database being restored.</span></span> <span data-ttu-id="628d6-113">Para saber como calcular a DTU necessária ou para solicitar mais DTU, veja [Solicitar uma alteração de cota de DTU][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="628d6-113">To learn how to calculate DTU needed or to request more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="628d6-114">Instalar o PowerShell</span><span class="sxs-lookup"><span data-stu-id="628d6-114">Install PowerShell</span></span>
<span data-ttu-id="628d6-115">Para usar o Azure PowerShell com o SQL Data Warehouse, você precisará instalar a versão 1.0 ou superior do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="628d6-115">In order to use Azure PowerShell with SQL Data Warehouse, you will need to install Azure PowerShell version 1.0 or greater.</span></span>  <span data-ttu-id="628d6-116">Você pode verificar a versão executando **Get-Module -ListAvailable -Name AzureRM**.</span><span class="sxs-lookup"><span data-stu-id="628d6-116">You can check your version by running **Get-Module -ListAvailable -Name AzureRM**.</span></span>  <span data-ttu-id="628d6-117">A versão mais recente pode ser instalada pelo [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="628d6-117">The latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="628d6-118">Para obter mais informações sobre como instalar a versão mais recente, consulte [Como instalar e configurar o Azure PowerShell][How to install and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="628d6-118">For more information on installing the latest version, see [How to install and configure Azure PowerShell][How to install and configure Azure PowerShell].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="628d6-119">Restaurar um banco de dados ativo ou pausado</span><span class="sxs-lookup"><span data-stu-id="628d6-119">Restore an active or paused database</span></span>
<span data-ttu-id="628d6-120">Para restaurar um banco de dados por meio de um instantâneo, use o cmdlet do PowerShell [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="628d6-120">To restore a database from a snapshot use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] PowerShell cmdlet.</span></span>

1. <span data-ttu-id="628d6-121">Abra o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="628d6-121">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="628d6-122">Conecte-se à sua conta do Azure e liste todas as assinaturas associadas à sua conta.</span><span class="sxs-lookup"><span data-stu-id="628d6-122">Connect to your Azure account and list all the subscriptions associated with your account.</span></span>
3. <span data-ttu-id="628d6-123">Selecione a assinatura que contém o banco de dados a ser restaurado.</span><span class="sxs-lookup"><span data-stu-id="628d6-123">Select the subscription that contains the database to be restored.</span></span>
4. <span data-ttu-id="628d6-124">Liste os pontos de restauração do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="628d6-124">List the restore points for the database.</span></span>
5. <span data-ttu-id="628d6-125">Selecione o ponto de restauração desejado usando o RestorePointCreationDate.</span><span class="sxs-lookup"><span data-stu-id="628d6-125">Pick the desired restore point using the RestorePointCreationDate.</span></span>
6. <span data-ttu-id="628d6-126">Restaure o banco de dados para o ponto de restauração desejado.</span><span class="sxs-lookup"><span data-stu-id="628d6-126">Restore the database to the desired restore point.</span></span>
7. <span data-ttu-id="628d6-127">Verifique se o banco de dados restaurado está online.</span><span class="sxs-lookup"><span data-stu-id="628d6-127">Verify that the restored database is online.</span></span>

```Powershell

$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# List the last 10 database restore points
((Get-AzureRMSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName ($DatabaseName).RestorePointCreationDate)[-10 .. -1]

# Or list all restore points
Get-AzureRmSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Get the specific database to restore
$Database = Get-AzureRmSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Pick desired restore point using RestorePointCreationDate
$PointInTime="<RestorePointCreationDate>"  

# Restore database from a restore point
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromPointInTimeBackup –PointInTime $PointInTime -ResourceGroupName $Database.ResourceGroupName -ServerName $Database.$ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $Database.ResourceID

# Verify the status of restored database
$RestoredDatabase.status

```

> [!NOTE]
> <span data-ttu-id="628d6-128">Depois que a restauração estiver concluída, você poderá configurar o banco de dados recuperado seguindo [Configurar o banco de dados após a recuperação][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="628d6-128">After the restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="628d6-129">Restaurar um banco de dados excluído</span><span class="sxs-lookup"><span data-stu-id="628d6-129">Restore a deleted database</span></span>
<span data-ttu-id="628d6-130">Para restaurar um banco de dados excluído, use o cmdlet [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="628d6-130">To restore a deleted database, use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="628d6-131">Abra o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="628d6-131">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="628d6-132">Conecte-se à sua conta do Azure e liste todas as assinaturas associadas à sua conta.</span><span class="sxs-lookup"><span data-stu-id="628d6-132">Connect to your Azure account and list all the subscriptions associated with your account.</span></span>
3. <span data-ttu-id="628d6-133">Selecione a assinatura que contém o banco de dados excluído a ser restaurado.</span><span class="sxs-lookup"><span data-stu-id="628d6-133">Select the subscription that contains the deleted database to be restored.</span></span>
4. <span data-ttu-id="628d6-134">Obtenha o banco de dados excluído em questão.</span><span class="sxs-lookup"><span data-stu-id="628d6-134">Get the specific deleted database.</span></span>
5. <span data-ttu-id="628d6-135">Restaure o banco de dados excluído.</span><span class="sxs-lookup"><span data-stu-id="628d6-135">Restore the deleted database.</span></span>
6. <span data-ttu-id="628d6-136">Verifique se o banco de dados restaurado está online.</span><span class="sxs-lookup"><span data-stu-id="628d6-136">Verify that the restored database is online.</span></span>

```Powershell
$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Get the deleted database to restore
$DeletedDatabase = Get-AzureRmSqlDeletedDatabaseBackup -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Restore deleted database
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromDeletedDatabaseBackup –DeletionDate $DeletedDatabase.DeletionDate -ResourceGroupName $DeletedDatabase.ResourceGroupName -ServerName $DeletedDatabase.ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $DeletedDatabase.ResourceID

# Verify the status of restored database
$RestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="628d6-137">Depois que a restauração estiver concluída, você poderá configurar o banco de dados recuperado seguindo [Configurar o banco de dados após a recuperação][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="628d6-137">After the restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a><span data-ttu-id="628d6-138">Restaurar por meio de uma região geográfica do Azure</span><span class="sxs-lookup"><span data-stu-id="628d6-138">Restore from an Azure geographical region</span></span>
<span data-ttu-id="628d6-139">Para recuperar um banco de dados, use o cmdlet [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="628d6-139">To recover a database, use the [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="628d6-140">Abra o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="628d6-140">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="628d6-141">Conecte-se à sua conta do Azure e liste todas as assinaturas associadas à sua conta.</span><span class="sxs-lookup"><span data-stu-id="628d6-141">Connect to your Azure account and list all the subscriptions associated with your account.</span></span>
3. <span data-ttu-id="628d6-142">Selecione a assinatura que contém o banco de dados a ser restaurado.</span><span class="sxs-lookup"><span data-stu-id="628d6-142">Select the subscription that contains the database to be restored.</span></span>
4. <span data-ttu-id="628d6-143">Obtenha o banco de dados que você deseja recuperar.</span><span class="sxs-lookup"><span data-stu-id="628d6-143">Get the database you want to recover.</span></span>
5. <span data-ttu-id="628d6-144">Crie a solicitação de recuperação para o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="628d6-144">Create the recovery request for the database.</span></span>
6. <span data-ttu-id="628d6-145">Verifique o status do banco de dados com restauração geográfica.</span><span class="sxs-lookup"><span data-stu-id="628d6-145">Verify the status of the geo-restored database.</span></span>

```Powershell
Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName "<Subscription_name>"

# Get the database you want to recover
$GeoBackup = Get-AzureRmSqlDatabaseGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourServerName>" -DatabaseName "<YourDatabaseName>"

# Recover database
$GeoRestoredDatabase = Restore-AzureRmSqlDatabase –FromGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourTargetServer>" -TargetDatabaseName "<NewDatabaseName>" –ResourceId $GeoBackup.ResourceID

# Verify that the geo-restored database is online
$GeoRestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="628d6-146">Para configurar o banco de dados após a conclusão da restauração, veja [Configurar o banco de dados após a recuperação][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="628d6-146">To configure your database after the restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

<span data-ttu-id="628d6-147">O banco de dados recuperado será habilitado para TDE se o banco de dados de origem for habilitado para TDE.</span><span class="sxs-lookup"><span data-stu-id="628d6-147">The recovered database will be TDE-enabled if the source database is TDE-enabled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="628d6-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="628d6-148">Next steps</span></span>
<span data-ttu-id="628d6-149">Para saber mais sobre os recursos de continuidade dos negócios das edições do Banco de Dados SQL do Azure, leia a [Visão geral da continuidade dos negócios do Banco de Dados SQL do Azure][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="628d6-149">To learn about the business continuity features of Azure SQL Database editions, please read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
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
