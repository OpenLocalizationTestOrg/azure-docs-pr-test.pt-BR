---
title: "Configurar a retenção de backup de longo prazo – banco de dados SQL do Azure | Microsoft Docs"
description: "Saiba como armazenar backups automatizados no cofre dos Serviços de Recuperação do Azure e restaurar o cofre dos Serviços de Recuperação do Azure"
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
ms.openlocfilehash: ed9f74a59f0ca512e2758c6db4c5c9075030f859
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-restore-from-azure-sql-database-long-term-backup-retention"></a><span data-ttu-id="31478-103">Configurar e restaurar de uma retenção de backup de longo prazo do Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="31478-103">Configure and restore from Azure SQL Database long-term backup retention</span></span>

<span data-ttu-id="31478-104">Você pode configurar o cofre dos Serviços de Recuperação do Azure para armazenar backups do banco de dados SQL do Azure e, em seguida, recuperar um banco de dados usando os backups retidos no cofre usando o portal do Azure ou o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31478-104">You can configure the Azure Recovery Services vault to store Azure SQL database backups and then recover a database using backups retained in the vault using the Azure portal or PowerShell.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="31478-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="31478-105">Azure portal</span></span>

<span data-ttu-id="31478-106">As próximas seções mostram como usar o portal do Azure para configurar o cofre dos Serviços de Recuperação do Azure, exibir os backups no cofre e restaurar do cofre.</span><span class="sxs-lookup"><span data-stu-id="31478-106">The following sections show you how to use the Azure portal to configure the Azure Recovery Services vault, view backups in the vault, and restore from the vault.</span></span>

### <a name="configure-the-vault-register-the-server-and-select-databases"></a><span data-ttu-id="31478-107">Configurar o cofre, registrar o servidor e selecionar bancos de dados</span><span class="sxs-lookup"><span data-stu-id="31478-107">Configure the vault, register the server, and select databases</span></span>

<span data-ttu-id="31478-108">Você [configura um cofre dos Serviços de Recuperação do Azure para reter os backups automatizados](sql-database-long-term-retention.md) por um período maior que o período de retenção da camada de serviços.</span><span class="sxs-lookup"><span data-stu-id="31478-108">You [configure an Azure Recovery Services vault to retain automated backups](sql-database-long-term-retention.md) for a period longer than the retention period for your service tier.</span></span> 

1. <span data-ttu-id="31478-109">Abra a página **SQL Server** do servidor.</span><span class="sxs-lookup"><span data-stu-id="31478-109">Open the **SQL Server** page for your server.</span></span>

   ![página do sql server](./media/sql-database-get-started-portal/sql-server-blade.png)

2. <span data-ttu-id="31478-111">Clique em **Retenção de backup de longo prazo**.</span><span class="sxs-lookup"><span data-stu-id="31478-111">Click **Long-term backup retention**.</span></span>

   ![link da retenção de backup de longo prazo](./media/sql-database-get-started-backup-recovery/long-term-backup-retention-link.png)

3. <span data-ttu-id="31478-113">Na página **Retenção de backup de longo prazo** do servidor, leia e aceite os termos da visualização (a menos que você já tenha feito isso ou que esse recurso não esteja mais em visualização).</span><span class="sxs-lookup"><span data-stu-id="31478-113">On the **Long-term backup retention** page for your server, review and accept the preview terms (unless you have already done so - or this feature is no longer in preview).</span></span>

   ![aceitar os termos da visualização](./media/sql-database-get-started-backup-recovery/accept-the-preview-terms.png)

4. <span data-ttu-id="31478-115">Para configurar a retenção de backup de longo prazo, selecione o banco de dados na grade e clique em **Configurar** na barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="31478-115">To configure long-term backup retention, select that database in the grid and then click **Configure** on the toolbar.</span></span>

   ![selecionar o banco de dados para a retenção de backup de longo prazo](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

5. <span data-ttu-id="31478-117">Na página **Configurar**, clique em **Definir as configurações necessárias** em **Cofre do serviço de recuperação**.</span><span class="sxs-lookup"><span data-stu-id="31478-117">On the **Configure** page, click **Configure required settings** under **Recovery service vault**.</span></span>

   ![configurar link do cofre](./media/sql-database-get-started-backup-recovery/configure-vault-link.png)

6. <span data-ttu-id="31478-119">Na página **Cofre dos serviços de recuperação**, selecione um cofre existente, se houver.</span><span class="sxs-lookup"><span data-stu-id="31478-119">On the **Recovery services vault** page, select an existing vault, if any.</span></span> <span data-ttu-id="31478-120">Caso contrário, se nenhum cofre dos serviços de recuperação for encontrado para sua assinatura, clique para sair do fluxo e crie um cofre dos serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="31478-120">Otherwise, if no recovery services vault found for your subscription, click to exit the flow and create a recovery services vault.</span></span>

   ![criar link do cofre](./media/sql-database-get-started-backup-recovery/create-new-vault-link.png)

7. <span data-ttu-id="31478-122">Na página **Cofres dos Serviços de Recuperação**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="31478-122">On the **Recovery Services vaults** page, click **Add**.</span></span>

   ![adicionar link do cofre](./media/sql-database-get-started-backup-recovery/add-new-vault-link.png)
   
8. <span data-ttu-id="31478-124">Na página **Cofre dos Serviços de Recuperação**, forneça um nome válido para o cofre dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="31478-124">On the **Recovery Services vault** page, provide a valid name for the Recovery Services vault.</span></span>

   ![novo nome do cofre](./media/sql-database-get-started-backup-recovery/new-vault-name.png)

9. <span data-ttu-id="31478-126">Selecione sua assinatura e grupo de recursos, em seguida, selecione o local do cofre.</span><span class="sxs-lookup"><span data-stu-id="31478-126">Select your subscription and resource group, and then select the location for the vault.</span></span> <span data-ttu-id="31478-127">Quando terminar, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="31478-127">When done, click **Create**.</span></span>

   ![criar cofre](./media/sql-database-get-started-backup-recovery/create-new-vault.png)

   > [!IMPORTANT]
   > <span data-ttu-id="31478-129">O cofre deve estar localizado na mesma região do servidor lógico do SQL Azure e deve usar o mesmo grupo de recursos como o servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="31478-129">The vault must be located in the same region as the Azure SQL logical server, and must use the same resource group as the logical server.</span></span>
   >

10. <span data-ttu-id="31478-130">Depois que o novo cofre for criado, execute as etapas necessárias para retornar à página **Cofre dos Serviços de Recuperação**.</span><span class="sxs-lookup"><span data-stu-id="31478-130">After the new vault is created, execute the necessary steps to return to the **Recovery services vault** page.</span></span>

11. <span data-ttu-id="31478-131">Na página **Cofre dos serviços de recuperação**, clique no cofre e, em seguida, em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="31478-131">On the **Recovery services vault** page, click the vault and then click **Select**.</span></span>

   ![selecionar cofre existente](./media/sql-database-get-started-backup-recovery/select-existing-vault.png)

12. <span data-ttu-id="31478-133">Na página **Configurar**, forneça um nome válido para a nova política de retenção, modifique a política de retenção padrão, conforme apropriado e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="31478-133">On the **Configure** page, provide a valid name for the new retention policy, modify the default retention policy as appropriate, and then click **OK**.</span></span>

   ![definir política de retenção](./media/sql-database-get-started-backup-recovery/define-retention-policy.png)

13. <span data-ttu-id="31478-135">Na página **Retenção de backup de longo prazo** do banco de dados, clique em **Salvar** e em **OK** para aplicar a política de retenção de backup de longo prazo a todos os bancos de dados selecionados.</span><span class="sxs-lookup"><span data-stu-id="31478-135">On the **Long-term backup retention** page for your database, click **Save** and then click **OK** to apply the long-term backup retention policy to all selected databases.</span></span>

   ![definir política de retenção](./media/sql-database-get-started-backup-recovery/save-retention-policy.png)

14. <span data-ttu-id="31478-137">Clique em **salvar** para habilitar a retenção de backup a longo prazo, usando essa nova política no cofre de serviços de recuperação do Azure que você configurou.</span><span class="sxs-lookup"><span data-stu-id="31478-137">Click **Save** to enable long-term backup retention using this new policy to the Azure Recovery Services vault that you configured.</span></span>

   ![definir política de retenção](./media/sql-database-get-started-backup-recovery/enable-long-term-retention.png)

> [!IMPORTANT]
> <span data-ttu-id="31478-139">Uma vez configurados, os backups aparecerão no cofre nos próximos sete dias.</span><span class="sxs-lookup"><span data-stu-id="31478-139">Once configured, backups show up in the vault within next seven days.</span></span> <span data-ttu-id="31478-140">Não continue neste tutorial até que os backups apareçam no cofre.</span><span class="sxs-lookup"><span data-stu-id="31478-140">Do not continue this tutorial until backups show up in the vault.</span></span>
>

### <a name="view-backups-in-long-term-retention-using-azure-portal"></a><span data-ttu-id="31478-141">Exibir backups na retenção de longo prazo usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="31478-141">View backups in long-term retention using Azure portal</span></span>

<span data-ttu-id="31478-142">Exiba informações sobre os backups de banco de dados na [retenção de backup de longo prazo](sql-database-long-term-retention.md).</span><span class="sxs-lookup"><span data-stu-id="31478-142">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

1. <span data-ttu-id="31478-143">No portal do Azure, abra o cofre dos Serviços de Recuperação do Azure do banco de dados (acesse **Todos os recursos** e selecione-o na lista de recursos de sua assinatura) para exibir a quantidade de armazenamento usada pelos backups de banco de dados no cofre.</span><span class="sxs-lookup"><span data-stu-id="31478-143">In the Azure portal, open your Azure Recovery Services vault for your database backups (go to **All resources** and select it from the list of resources for your subscription) to view the amount of storage used by your database backups in the vault.</span></span>

   ![exibir cofre dos serviços de recuperação com backups](./media/sql-database-get-started-backup-recovery/view-recovery-services-vault-with-data.png)

2. <span data-ttu-id="31478-145">Abra a página **Banco de dados SQL** do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="31478-145">Open the **SQL database** page for your database.</span></span>

   ![nova página de BD de exemplo](./media/sql-database-get-started-portal/new-sample-db-blade.png)

3. <span data-ttu-id="31478-147">Na barra de ferramentas, clique em **Restaurar**.</span><span class="sxs-lookup"><span data-stu-id="31478-147">On the toolbar, click **Restore**.</span></span>

   ![barra de ferramentas de restauração](./media/sql-database-get-started-backup-recovery/restore-toolbar.png)

4. <span data-ttu-id="31478-149">Na página Restaurar, clique em **Longo prazo**.</span><span class="sxs-lookup"><span data-stu-id="31478-149">On the Restore page, click **Long-term**.</span></span>

5. <span data-ttu-id="31478-150">Nos backups do cofre do Azure, clique em **Selecionar um backup** para exibir os backups do banco de dados disponíveis na retenção de backup de longo prazo.</span><span class="sxs-lookup"><span data-stu-id="31478-150">Under Azure vault backups, click **Select a backup** to view the available database backups in long-term backup retention.</span></span>

   ![backups no cofre](./media/sql-database-get-started-backup-recovery/view-backups-in-vault.png)

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention-using-the-azure-portal"></a><span data-ttu-id="31478-152">Restaurar um banco de dados com base em um backup na retenção de backup de longo prazo usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="31478-152">Restore a database from a backup in long-term backup retention using the Azure portal</span></span>

<span data-ttu-id="31478-153">Você restaura o banco de dados para um novo banco de dados com base em um backup no cofre dos Serviços de Recuperação do Azure.</span><span class="sxs-lookup"><span data-stu-id="31478-153">You restore the database to a new database from a backup in the Azure Recovery Services vault.</span></span>

1. <span data-ttu-id="31478-154">Na página **Backups do cofre do Azure**, clique no backup a ser restaurado e, em seguida, clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="31478-154">On the **Azure vault backups** page, click the backup to restore and then click **Select**.</span></span>

   ![selecionar backup no cofre](./media/sql-database-get-started-backup-recovery/select-backup-in-vault.png)

2. <span data-ttu-id="31478-156">Na caixa de texto **Nome do banco de dados**, forneça o nome do banco de dados restaurado.</span><span class="sxs-lookup"><span data-stu-id="31478-156">In the **Database name** text box, provide the name for the restored database.</span></span>

   ![novo nome do banco de dados](./media/sql-database-get-started-backup-recovery/new-database-name.png)

3. <span data-ttu-id="31478-158">Clique em **OK** para restaurar seu banco de dados a partir do backup no cofre para o novo banco de dados.</span><span class="sxs-lookup"><span data-stu-id="31478-158">Click **OK** to restore your database from the backup in the vault to the new database.</span></span>

4. <span data-ttu-id="31478-159">Na barra de ferramentas, clique no ícone de notificação para exibir o status do trabalho de restauração.</span><span class="sxs-lookup"><span data-stu-id="31478-159">On the toolbar, click the notification icon to view the status of the restore job.</span></span>

   ![progresso do trabalho de restauração no cofre](./media/sql-database-get-started-backup-recovery/restore-job-progress-long-term.png)

5. <span data-ttu-id="31478-161">Quando o trabalho de restauração for concluído, abra a página **Bancos de dados SQL** para exibir o banco de dados recém-restaurado.</span><span class="sxs-lookup"><span data-stu-id="31478-161">When the restore job is completed, open the **SQL databases** page to view the newly restored database.</span></span>

   ![banco de dados restaurado a partir do cofre](./media/sql-database-get-started-backup-recovery/restored-database-from-vault.png)

> [!NOTE]
> <span data-ttu-id="31478-163">A partir daqui, você pode conectar o banco de dados restaurado usando o SQL Server Management Studio para executar as tarefas necessárias, tais como, [extrair um pouco de dados do banco de dados restaurado para copiar para o banco de dados existente ou excluir o banco de dados existente e renomear o banco de dados restaurado com o nome do banco de dados existente](sql-database-recovery-using-backups.md#point-in-time-restore).</span><span class="sxs-lookup"><span data-stu-id="31478-163">From here, you can connect to the restored database using SQL Server Management Studio to perform needed tasks, such as to [extract a bit of data from the restored database to copy into the existing database or to delete the existing database and rename the restored database to the existing database name](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>
>

## <a name="powershell"></a><span data-ttu-id="31478-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="31478-164">PowerShell</span></span>

<span data-ttu-id="31478-165">As próximas seções mostram como usar o PowerShell para configurar o cofre dos Serviços de Recuperação do Azure, exibir os backups no cofre e restaurar do cofre.</span><span class="sxs-lookup"><span data-stu-id="31478-165">The following sections show you how to use PowerShell to configure the Azure Recovery Services vault, view backups in the vault, and restore from the vault.</span></span>

### <a name="create-a-recovery-services-vault"></a><span data-ttu-id="31478-166">Criar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="31478-166">Create a recovery services vault</span></span>

<span data-ttu-id="31478-167">Use o [New-AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) para criar um cofre dos serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="31478-167">Use the [New-AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) to create a recovery services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="31478-168">O cofre deve estar localizado na mesma região do servidor lógico do SQL Azure e deve usar o mesmo grupo de recursos como o servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="31478-168">The vault must be located in the same region as the Azure SQL logical server, and must use the same resource group as the logical server.</span></span>

```PowerShell
# Create a recovery services vault

#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$serverLocation = (Get-AzureRmSqlServer -ServerName $serverName -ResourceGroupName $resourceGroupName).Location
$recoveryServiceVaultName = "{new-vault-name}"

$vault = New-AzureRmRecoveryServicesVault -Name $recoveryServiceVaultName -ResourceGroupName $ResourceGroupName -Location $serverLocation 
Set-AzureRmRecoveryServicesBackupProperties -BackupStorageRedundancy LocallyRedundant -Vault $vault
```

### <a name="set-your-server-to-use-the-recovery-vault-for-its-long-term-retention-backups"></a><span data-ttu-id="31478-169">Definir o servidor para usar o cofre de recuperação para seus backups de retenção de longo prazo</span><span class="sxs-lookup"><span data-stu-id="31478-169">Set your server to use the recovery vault for its long-term retention backups</span></span>

<span data-ttu-id="31478-170">Use o cmdlet [Set-AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) para associar um cofre dos serviços de recuperação criado anteriormente a um SQL Server específico do Azure.</span><span class="sxs-lookup"><span data-stu-id="31478-170">Use the [Set-AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) cmdlet to associate a previously created recovery services vault with a specific Azure SQL server.</span></span>

```PowerShell
# Set your server to use the vault to for long-term backup retention 

Set-AzureRmSqlServerBackupLongTermRetentionVault -ResourceGroupName $resourceGroupName -ServerName $serverName -ResourceId $vault.Id
```

### <a name="create-a-retention-policy"></a><span data-ttu-id="31478-171">Criar uma política de retenção</span><span class="sxs-lookup"><span data-stu-id="31478-171">Create a retention policy</span></span>

<span data-ttu-id="31478-172">Em uma política de retenção, você define por quanto tempo um backup de banco de dados deve ser mantido.</span><span class="sxs-lookup"><span data-stu-id="31478-172">A retention policy is where you set how long to keep a database backup.</span></span> <span data-ttu-id="31478-173">Use o cmdlet [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) para obter a política de retenção padrão a ser usada como modelo para criação de políticas.</span><span class="sxs-lookup"><span data-stu-id="31478-173">Use the [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet to get the default retention policy to use as the template for creating policies.</span></span> <span data-ttu-id="31478-174">Neste modelo, o período de retenção é definido para 2 anos.</span><span class="sxs-lookup"><span data-stu-id="31478-174">In this template, the retention period is set for 2 years.</span></span> <span data-ttu-id="31478-175">Em seguida, execute o [New-AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) para finalmente criar a política.</span><span class="sxs-lookup"><span data-stu-id="31478-175">Next, run the [New-AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) to finally create the policy.</span></span> 

> [!NOTE]
> <span data-ttu-id="31478-176">Alguns cmdlets exigem que você defina o contexto de cofre antes da execução ([Set-AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)); portanto, esse cmdlet é visto em alguns trechos de código relacionados.</span><span class="sxs-lookup"><span data-stu-id="31478-176">Some cmdlets require that you set the vault context before running ([Set-AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) so you see this cmdlet in a few related snippets.</span></span> <span data-ttu-id="31478-177">Você define o contexto porque a política faz parte do cofre.</span><span class="sxs-lookup"><span data-stu-id="31478-177">You set the context because the policy is part of the vault.</span></span> <span data-ttu-id="31478-178">Você pode criar várias políticas de retenção para cada compartimento e aplicar a política desejada a bancos de dados específicos.</span><span class="sxs-lookup"><span data-stu-id="31478-178">You can create multiple retention policies for each vault and then apply the desired policy to specific databases.</span></span> 


```PowerShell
# Retrieve the default retention policy for the AzureSQLDatabase workload type
$retentionPolicy = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType AzureSQLDatabase

# Set the retention value to two years (you can set to any time between 1 week and 10 years)
$retentionPolicy.RetentionDurationType = "Years"
$retentionPolicy.RetentionCount = 2
$retentionPolicyName = "my2YearRetentionPolicy"

# Set the vault context to the vault you are creating the policy for
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# Create the new policy
$policy = New-AzureRmRecoveryServicesBackupProtectionPolicy -name $retentionPolicyName -WorkloadType AzureSQLDatabase -retentionPolicy $retentionPolicy
$policy
```

### <a name="configure-a-database-to-use-the-previously-defined-retention-policy"></a><span data-ttu-id="31478-179">Configurar um banco de dados para usar a política de retenção definida anteriormente</span><span class="sxs-lookup"><span data-stu-id="31478-179">Configure a database to use the previously defined retention policy</span></span>

<span data-ttu-id="31478-180">Use o cmdlet [Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) para aplicar a nova política a um banco de dados específico.</span><span class="sxs-lookup"><span data-stu-id="31478-180">Use the [Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet to apply the new policy to a specific database.</span></span>

```PowerShell
# Enable long-term retention for a specific SQL database
$policyState = "enabled"
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -State $policyState -ResourceId $policy.Id
```

### <a name="view-backup-info-and-backups-in-long-term-retention"></a><span data-ttu-id="31478-181">Exibir informações de backup e backups de retenção de longo prazo</span><span class="sxs-lookup"><span data-stu-id="31478-181">View backup info, and backups in long-term retention</span></span>

<span data-ttu-id="31478-182">Exiba informações sobre os backups de banco de dados na [retenção de backup de longo prazo](sql-database-long-term-retention.md).</span><span class="sxs-lookup"><span data-stu-id="31478-182">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

<span data-ttu-id="31478-183">Use os seguintes cmdlets para exibir informações de backup:</span><span class="sxs-lookup"><span data-stu-id="31478-183">Use the following cmdlets to view backup information:</span></span>

- [<span data-ttu-id="31478-184">Get-AzureRmRecoveryServicesBackupContainer</span><span class="sxs-lookup"><span data-stu-id="31478-184">Get-AzureRmRecoveryServicesBackupContainer</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)
- [<span data-ttu-id="31478-185">Get-AzureRmRecoveryServicesBackupItem</span><span class="sxs-lookup"><span data-stu-id="31478-185">Get-AzureRmRecoveryServicesBackupItem</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)
- [<span data-ttu-id="31478-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="31478-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)

```PowerShell
#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$databaseNeedingRestore = $databaseName

# Set the vault context to the vault we want to restore from
#$vault = Get-AzureRmRecoveryServicesVault -ResourceGroupName $resourceGroupName
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# the following commands find the container associated with the server 'myserver' under resource group 'myresourcegroup'
$container = Get-AzureRmRecoveryServicesBackupContainer -ContainerType AzureSQL -FriendlyName $vault.Name

# Get the long-term retention metadata associated with a specific database
$item = Get-AzureRmRecoveryServicesBackupItem -Container $container -WorkloadType AzureSQLDatabase -Name $databaseNeedingRestore

# Get all available backups for the previously indicated database
# Optionally, set the -StartDate and -EndDate parameters to return backups within a specific time period
$availableBackups = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $item
$availableBackups
```

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention"></a><span data-ttu-id="31478-187">Restaurar um banco de dados a partir de um backup na retenção de backup de longo prazo</span><span class="sxs-lookup"><span data-stu-id="31478-187">Restore a database from a backup in long-term backup retention</span></span>

<span data-ttu-id="31478-188">A restauração da retenção de backup de longo prazo usa o cmdlet [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase).</span><span class="sxs-lookup"><span data-stu-id="31478-188">Restoring from long-term backup retention uses the [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet.</span></span>

```PowerShell
# Restore the most recent backup: $availableBackups[0]
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
> <span data-ttu-id="31478-189">A partir daqui, você pode conectar o banco de dados restaurado usando o SQL Server Management Studio para executar as tarefas necessárias, tais como, extrair um pouco de dados do banco de dados restaurado para copiar para o banco de dados existente ou excluir o banco de dados existente e renomear o banco de dados restaurado com o nome do banco de dados existente.</span><span class="sxs-lookup"><span data-stu-id="31478-189">From here, you can connect to the restored database using SQL Server Management Studio to perform needed tasks, such as to extract a bit of data from the restored database to copy into the existing database or to delete the existing database and rename the restored database to the existing database name.</span></span> <span data-ttu-id="31478-190">Confira [recuperação pontual](sql-database-recovery-using-backups.md#point-in-time-restore).</span><span class="sxs-lookup"><span data-stu-id="31478-190">See [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>

## <a name="next-steps"></a><span data-ttu-id="31478-191">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="31478-191">Next steps</span></span>

- <span data-ttu-id="31478-192">Para saber mais sobre backups automáticos gerados pelo serviço, veja [backups automáticos](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="31478-192">To learn about service-generated automatic backups, see [automatic backups](sql-database-automated-backups.md)</span></span>
- <span data-ttu-id="31478-193">Para saber mais sobre a retenção de backup de longo prazo, consulte [retenção de backup de longo prazo](sql-database-long-term-retention.md)</span><span class="sxs-lookup"><span data-stu-id="31478-193">To learn about long-term backup retention, see [long-term backup retention](sql-database-long-term-retention.md)</span></span>
- <span data-ttu-id="31478-194">Para saber mais sobre a restauração a partir de backups, consulte [restaurar a partir do backup](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="31478-194">To learn about restoring from backups, see [restore from backup](sql-database-recovery-using-backups.md)</span></span>
