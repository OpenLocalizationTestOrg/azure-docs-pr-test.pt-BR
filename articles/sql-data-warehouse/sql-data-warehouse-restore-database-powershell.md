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
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a>Restaurar um Azure SQL Data Warehouse (PowerShell)
> [!div class="op_single_selector"]
> * [Visão geral][Overview]
> * [Portal][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

Neste artigo, você aprenderá como toorestore um Azure SQL Data Warehouse usando o PowerShell.

## <a name="before-you-begin"></a>Antes de começar
**Verifique sua capacidade de DTU.** Cada SQL Data Warehouse é hospedado por um servidor SQL (por exemplo, myserver.database.windows.net) que tem uma cota de DTU padrão.  Antes de poder restaurar um SQL Data Warehouse, verifique se esse saudação que do SQL server tem suficiente restante cota de DTU para o banco de dados de hello está sendo restaurado. toolearn como toocalculate DTU necessário ou toorequest mais DTU, consulte [solicitar uma alteração de cota DTU][Request a DTU quota change].

### <a name="install-powershell"></a>Instalar o PowerShell
Ordem toouse PowerShell do Azure SQL Data warehouse, você precisará tooinstall Azure PowerShell versão 1.0 ou posterior.  Você pode verificar a versão executando **Get-Module -ListAvailable -Name AzureRM**.  versão mais recente do Hello pode ser instalado do [Microsoft Web Platform Installer][Microsoft Web Platform Installer].  Para obter mais informações sobre como instalar a versão mais recente do hello, consulte [como tooinstall e configurar o Azure PowerShell][How tooinstall and configure Azure PowerShell].

## <a name="restore-an-active-or-paused-database"></a>Restaurar um banco de dados ativo ou pausado
toorestore um banco de dados de um instantâneo usar Olá [restauração AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet do PowerShell.

1. Abra o Windows PowerShell.
2. Conecte-se tooyour conta do Azure e listar todas as assinaturas de saudação associadas à sua conta.
3. Selecione a assinatura de saudação que contém a saudação toobe de banco de dados restaurado.
4. Olá lista pontos para banco de dados de saudação de restauração.
5. Selecione o ponto de restauração Olá desejado usando Olá RestorePointCreationDate.
6. Ponto de restauração de toohello desejado Olá banco de dados de restauração.
7. Verifique se o que banco de dados restaurado de saudação está online.

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
> Após a restauração hello, você pode configurar o banco de dados recuperado seguindo [configurar seu banco de dados após a recuperação][Configure your database after recovery].
> 
> 

## <a name="restore-a-deleted-database"></a>Restaurar um banco de dados excluído
toorestore um banco de dados excluído, use Olá [restauração AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet.

1. Abra o Windows PowerShell.
2. Conecte-se tooyour conta do Azure e listar todas as assinaturas de saudação associadas à sua conta.
3. Excluir a assinatura de saudação Select que contém Olá toobe de banco de dados restaurado.
4. Obter banco de dados específico Olá excluído.
5. Restaure o banco de dados de saudação excluído.
6. Verifique se o que banco de dados restaurado de saudação está online.

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
> Após a restauração hello, você pode configurar o banco de dados recuperado seguindo [configurar seu banco de dados após a recuperação][Configure your database after recovery].
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a>Restaurar por meio de uma região geográfica do Azure
toorecover um banco de dados, use Olá [restauração AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet.

1. Abra o Windows PowerShell.
2. Conecte-se tooyour conta do Azure e listar todas as assinaturas de saudação associadas à sua conta.
3. Selecione a assinatura de saudação que contém a saudação toobe de banco de dados restaurado.
4. Obter toorecover de saudação banco de dados.
5. Crie solicitação de recuperação de saudação do banco de dados de saudação.
6. Verificar o status de saudação do banco de dados restaurado geográfica do hello.

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
> tooconfigure seu banco de dados após a restauração hello, consulte [configurar seu banco de dados após a recuperação][Configure your database after recovery].
> 
> 

saudação de banco de dados recuperado será habilitado para TDE se o banco de dados de origem de saudação é habilitado para TDE.

## <a name="next-steps"></a>Próximas etapas
toolearn sobre recursos de continuidade de negócios Olá de edições de banco de dados de SQL do Azure, leia Olá [visão geral de continuidade de negócios do Azure SQL Database][Azure SQL Database business continuity overview].

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
