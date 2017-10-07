---
title: "Configurar a retenção de backup de longo prazo – banco de dados SQL do Azure | Microsoft Docs"
description: "Saiba como toostore automatizado backups no hello Cofre de serviços de recuperação do Azure e toorestore de saudação que Cofre de serviços de recuperação do Azure"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: aeb8c4c3-6ae2-45f7-b2c3-fa13e3752eed
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: carlrab
ms.openlocfilehash: 603f4dd21cee4407d46f749655aba8f9ef3322c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-restore-from-azure-sql-database-long-term-backup-retention"></a>Configurar e restaurar de uma retenção de backup de longo prazo do Banco de Dados SQL do Azure

Você pode configurar backups de banco de dados de SQL do Azure Olá dos serviços de recuperação do Azure cofre toostore e, em seguida, recuperar um banco de dados usando backups retido Olá cofre usando Olá portal do Azure ou o PowerShell.

## <a name="azure-portal"></a>Portal do Azure

Olá Mostrar seções você como cofre toouse Olá tooconfigure portal do Azure Olá dos serviços de recuperação do Azure, exibir backups no cofre hello e restaurar do cofre Olá a seguir.

### <a name="configure-hello-vault-register-hello-server-and-select-databases"></a>Configurar Olá cofre, registrar o servidor de saudação e selecionar bancos de dados

Você [configurar um backups de tooretain automatizada de Cofre de serviços de recuperação do Azure](sql-database-long-term-retention.md) para um período maior que o período de retenção Olá para a camada de serviço. 

1. Olá abrir **do SQL Server** página para o servidor.

   ![página do sql server](./media/sql-database-get-started-portal/sql-server-blade.png)

2. Clique em **Retenção de backup de longo prazo**.

   ![link da retenção de backup de longo prazo](./media/sql-database-get-started-backup-recovery/long-term-backup-retention-link.png)

3. Em Olá **retenção de backup de longo prazo** página para o servidor, revise e aceite os termos de visualização da saudação (a menos que você já tiver feito isso - ou esse recurso não está mais na visualização).

   ![Aceite os termos de visualização Olá](./media/sql-database-get-started-backup-recovery/accept-the-preview-terms.png)

4. tooconfigure retenção de backup a longo prazo, selecione o banco de dados na grade de saudação e, em seguida, clique em **configurar** na barra de ferramentas de saudação.

   ![selecionar o banco de dados para a retenção de backup de longo prazo](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

5. Em Olá **configurar** , clique em **definir as configurações necessárias** em **cofre da recuperação de serviço**.

   ![configurar link do cofre](./media/sql-database-get-started-backup-recovery/configure-vault-link.png)

6. Em Olá **Cofre de serviços de recuperação** , selecione um cofre existente, se houver. Caso contrário, se nenhum Cofre de serviços de recuperação encontrado para a sua assinatura, clique em fluxo de saudação tooexit e crie um cofre de serviços de recuperação.

   ![criar link do cofre](./media/sql-database-get-started-backup-recovery/create-new-vault-link.png)

7. Em Olá **os cofres de serviços de recuperação** , clique em **adicionar**.

   ![adicionar link do cofre](./media/sql-database-get-started-backup-recovery/add-new-vault-link.png)
   
8. Em Olá **Cofre de serviços de recuperação** , forneça um nome válido para o Cofre de serviços de recuperação de saudação.

   ![novo nome do cofre](./media/sql-database-get-started-backup-recovery/new-vault-name.png)

9. Selecione sua assinatura e o grupo de recursos e, em seguida, selecione o local de Olá para o Cofre de saudação. Quando terminar, clique em **Criar**.

   ![criar cofre](./media/sql-database-get-started-backup-recovery/create-new-vault.png)

   > [!IMPORTANT]
   > cofre Olá deve estar localizado no hello mesma região que o servidor lógico do SQL Azure hello e deve usar Olá mesmo grupo de recursos como o servidor lógico hello.
   >

10. Após a criação do novo cofre de hello, execute Olá etapas necessárias tooreturn toohello **Cofre de serviços de recuperação** página.

11. Em Olá **Cofre de serviços de recuperação** página, clique em cofre hello e, em seguida, clique em **selecione**.

   ![selecionar cofre existente](./media/sql-database-get-started-backup-recovery/select-existing-vault.png)

12. Em Olá **configurar** página, forneça um nome válido para a nova política de retenção hello, modifique a política de retenção padrão Olá conforme apropriado e, em seguida, clique em **Okey**.

   ![definir política de retenção](./media/sql-database-get-started-backup-recovery/define-retention-policy.png)

13. Em Olá **retenção de backup de longo prazo** para seu banco de dados, clique em **salvar** e, em seguida, clique em **Okey** tooapply Olá longo prazo tooall de política de retenção de backup selecionado bancos de dados.

   ![definir política de retenção](./media/sql-database-get-started-backup-recovery/save-retention-policy.png)

14. Clique em **salvar** tooenable backup retenção de longo prazo usando esse novo cofre de serviços de recuperação do Azure de toohello de política que você configurou.

   ![definir política de retenção](./media/sql-database-get-started-backup-recovery/enable-long-term-retention.png)

> [!IMPORTANT]
> Uma vez configurado, backups aparecem no cofre Olá nos próximos sete dias. Não continue neste tutorial até que os backups aparecem no cofre hello.
>

### <a name="view-backups-in-long-term-retention-using-azure-portal"></a>Exibir backups na retenção de longo prazo usando o portal do Azure

Exiba informações sobre os backups de banco de dados na [retenção de backup de longo prazo](sql-database-long-term-retention.md). 

1. No hello portal do Azure, abra seu Cofre de serviços de recuperação do Azure para seus backups de banco de dados (vá muito**todos os recursos** e selecioná-lo da lista de saudação de recursos para sua assinatura) tooview quantidade de saudação do armazenamento usado por seu banco de dados backups no cofre hello.

   ![exibir cofre dos serviços de recuperação com backups](./media/sql-database-get-started-backup-recovery/view-recovery-services-vault-with-data.png)

2. Olá abrir **banco de dados SQL** página do banco de dados.

   ![nova página de BD de exemplo](./media/sql-database-get-started-portal/new-sample-db-blade.png)

3. Na barra de ferramentas hello, clique em **restauração**.

   ![barra de ferramentas de restauração](./media/sql-database-get-started-backup-recovery/restore-toolbar.png)

4. Na página de restauração hello, clique em **longo prazo**.

5. Em backups de cofre do Azure, clique em **selecionar um backup** tooview backups de banco de dados disponível Olá no armazenamento de backup de longo prazo.

   ![backups no cofre](./media/sql-database-get-started-backup-recovery/view-backups-in-vault.png)

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention-using-hello-azure-portal"></a>Restaurar um banco de dados de um backup em longo prazo retenção de backup usando Olá portal do Azure

Você pode restaurar Olá tooa novo banco de dados de um backup em Olá que Cofre de serviços de recuperação do Azure.

1. Em Olá **backups do cofre do Azure** página, clique toorestore backup hello e, em seguida, clique em **selecione**.

   ![selecionar backup no cofre](./media/sql-database-get-started-backup-recovery/select-backup-in-vault.png)

2. Em Olá **nome do banco de dados** texto caixa, forneça o nome de saudação do banco de dados restaurado de saudação.

   ![novo nome do banco de dados](./media/sql-database-get-started-backup-recovery/new-database-name.png)

3. Clique em **Okey** toorestore seu banco de dados de backup Olá Olá cofre toohello novo banco de dados.

4. Na barra de ferramentas hello, clique em status Olá notificação ícone tooview saudação do trabalho de restauração hello.

   ![progresso do trabalho de restauração no cofre](./media/sql-database-get-started-backup-recovery/restore-job-progress-long-term.png)

5. Quando o trabalho de restauração Olá for concluído, abra Olá **bancos de dados SQL** banco de dados do página tooview Olá recentemente restaurado.

   ![banco de dados restaurado a partir do cofre](./media/sql-database-get-started-backup-recovery/restored-database-from-vault.png)

> [!NOTE]
> A partir daqui, você pode se conectar a banco de dados toohello restaurado usando tarefas de tooperform necessário do SQL Server Management Studio, como muito[extrair um pouco de dados de saudação restaurada toocopy de banco de dados no banco de dados existente do hello ou toodelete Olá existente nome de banco de dados de banco de dados e renomear Olá restaurado banco de dados toohello existente](sql-database-recovery-using-backups.md#point-in-time-restore).
>

## <a name="powershell"></a>PowerShell

Olá seções a seguir mostra como toouse Cofre de serviços de recuperação do Azure para PowerShell tooconfigure hello, exibir backups no cofre hello e restaurar do cofre hello.

### <a name="create-a-recovery-services-vault"></a>Criar um cofre dos Serviços de Recuperação

Saudação de uso [AzureRmRecoveryServicesVault novo](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) toocreate uma recuperação o Cofre de serviços.

> [!IMPORTANT]
> cofre Olá deve estar localizado no hello mesma região que o servidor lógico do SQL Azure hello e deve usar Olá mesmo grupo de recursos como o servidor lógico hello.

```PowerShell
# Create a recovery services vault

#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$serverLocation = (Get-AzureRmSqlServer -ServerName $serverName -ResourceGroupName $resourceGroupName).Location
$recoveryServiceVaultName = "{new-vault-name}"

$vault = New-AzureRmRecoveryServicesVault -Name $recoveryServiceVaultName -ResourceGroupName $ResourceGroupName -Location $serverLocation 
Set-AzureRmRecoveryServicesBackupProperties -BackupStorageRedundancy LocallyRedundant -Vault $vault
```

### <a name="set-your-server-toouse-hello-recovery-vault-for-its-long-term-retention-backups"></a>Definir seu Cofre de recuperação do servidor toouse Olá para seus backups de retenção de longo prazo

Saudação de uso [AzureRmSqlServerBackupLongTermRetentionVault conjunto](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) cmdlet tooassociate criado anteriormente Cofre de serviços de recuperação com um servidor específico do SQL Azure.

```PowerShell
# Set your server toouse hello vault toofor long-term backup retention 

Set-AzureRmSqlServerBackupLongTermRetentionVault -ResourceGroupName $resourceGroupName -ServerName $serverName -ResourceId $vault.Id
```

### <a name="create-a-retention-policy"></a>Criar uma política de retenção

Uma política de retenção é onde você define tookeep quanto tempo um backup de banco de dados. Saudação de uso [AzureRmRecoveryServicesBackupRetentionPolicyObject Get](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet tooget saudação padrão retenção política toouse como modelo Olá para a criação de políticas. Neste modelo, o período de retenção de saudação é definido para 2 anos. Em seguida, execute Olá [AzureRmRecoveryServicesBackupProtectionPolicy novo](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) toofinally Criar política de saudação. 

> [!NOTE]
> Alguns cmdlets exigem que você defina o contexto de cofre Olá antes de executar ([AzureRmRecoveryServicesVaultContext conjunto](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) para ver esse cmdlet em alguns trechos de código relacionados. Você define o contexto de saudação porque a política de saudação é parte do cofre hello. Você pode criar várias políticas de retenção para cada compartimento e, em seguida, aplicar Olá desejado política toospecific bancos de dados. 


```PowerShell
# Retrieve hello default retention policy for hello AzureSQLDatabase workload type
$retentionPolicy = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType AzureSQLDatabase

# Set hello retention value tootwo years (you can set tooany time between 1 week and 10 years)
$retentionPolicy.RetentionDurationType = "Years"
$retentionPolicy.RetentionCount = 2
$retentionPolicyName = "my2YearRetentionPolicy"

# Set hello vault context toohello vault you are creating hello policy for
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# Create hello new policy
$policy = New-AzureRmRecoveryServicesBackupProtectionPolicy -name $retentionPolicyName -WorkloadType AzureSQLDatabase -retentionPolicy $retentionPolicy
$policy
```

### <a name="configure-a-database-toouse-hello-previously-defined-retention-policy"></a>Configurar uma política de retenção do banco de dados toouse Olá definido anteriormente

Saudação de uso [AzureRmSqlDatabaseBackupLongTermRetentionPolicy conjunto](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet tooapply Olá nova política tooa banco de dados específico.

```PowerShell
# Enable long-term retention for a specific SQL database
$policyState = "enabled"
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -State $policyState -ResourceId $policy.Id
```

### <a name="view-backup-info-and-backups-in-long-term-retention"></a>Exibir informações de backup e backups de retenção de longo prazo

Exiba informações sobre os backups de banco de dados na [retenção de backup de longo prazo](sql-database-long-term-retention.md). 

Use Olá cmdlets tooview fazer backup das informações a seguir:

- [Get-AzureRmRecoveryServicesBackupContainer](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)
- [Get-AzureRmRecoveryServicesBackupItem](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)
- [Get-AzureRmRecoveryServicesBackupRecoveryPoint](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)

```PowerShell
#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$databaseNeedingRestore = $databaseName

# Set hello vault context toohello vault we want toorestore from
#$vault = Get-AzureRmRecoveryServicesVault -ResourceGroupName $resourceGroupName
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# hello following commands find hello container associated with hello server 'myserver' under resource group 'myresourcegroup'
$container = Get-AzureRmRecoveryServicesBackupContainer -ContainerType AzureSQL -FriendlyName $vault.Name

# Get hello long-term retention metadata associated with a specific database
$item = Get-AzureRmRecoveryServicesBackupItem -Container $container -WorkloadType AzureSQLDatabase -Name $databaseNeedingRestore

# Get all available backups for hello previously indicated database
# Optionally, set hello -StartDate and -EndDate parameters tooreturn backups within a specific time period
$availableBackups = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $item
$availableBackups
```

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention"></a>Restaurar um banco de dados a partir de um backup na retenção de backup de longo prazo

Restauração de retenção de backup de longo prazo utiliza Olá [AzureRmSqlDatabase restauração](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet.

```PowerShell
# Restore hello most recent backup: $availableBackups[0]
#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$restoredDatabaseName = "{new-database-name}"
$edition = "Basic"
$performanceLevel = "Basic"

$restoredDb = Restore-AzureRmSqlDatabase -FromLongTermRetentionBackup -ResourceId $availableBackups[0].Id -ResourceGroupName $resourceGroupName `
 -ServerName $serverName -TargetDatabaseName $restoredDatabaseName -Edition $edition -ServiceObjectiveName $performanceLevel
$restoredDb
```


> [!NOTE]
> A partir daqui, você pode se conectar a banco de dados de toohello restaurado usando tarefas do SQL Server Management Studio tooperform necessário, como tooextract um pouco de dados de saudação restaurado toocopy de banco de dados no banco de dados existente do hello ou banco de dados existente do hello toodelete e renomear Olá restaurado nome de banco de dados existente do banco de dados toohello. Confira [recuperação pontual](sql-database-recovery-using-backups.md#point-in-time-restore).

## <a name="next-steps"></a>Próximas etapas

- toolearn sobre backups automáticos gerado pelo serviço, consulte [backups automáticos](sql-database-automated-backups.md)
- toolearn sobre retenção de backup de longo prazo, consulte [retenção de backup de longo prazo](sql-database-long-term-retention.md)
- toolearn sobre restauração de backups, consulte [restaurar do backup](sql-database-recovery-using-backups.md)
