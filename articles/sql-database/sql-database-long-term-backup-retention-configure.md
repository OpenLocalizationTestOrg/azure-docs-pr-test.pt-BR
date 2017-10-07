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
# <a name="configure-and-restore-from-azure-sql-database-long-term-backup-retention"></a><span data-ttu-id="4eca8-103">Configurar e restaurar de uma retenção de backup de longo prazo do Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="4eca8-103">Configure and restore from Azure SQL Database long-term backup retention</span></span>

<span data-ttu-id="4eca8-104">Você pode configurar backups de banco de dados de SQL do Azure Olá dos serviços de recuperação do Azure cofre toostore e, em seguida, recuperar um banco de dados usando backups retido Olá cofre usando Olá portal do Azure ou o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4eca8-104">You can configure hello Azure Recovery Services vault toostore Azure SQL database backups and then recover a database using backups retained in hello vault using hello Azure portal or PowerShell.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="4eca8-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4eca8-105">Azure portal</span></span>

<span data-ttu-id="4eca8-106">Olá Mostrar seções você como cofre toouse Olá tooconfigure portal do Azure Olá dos serviços de recuperação do Azure, exibir backups no cofre hello e restaurar do cofre Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="4eca8-106">hello following sections show you how toouse hello Azure portal tooconfigure hello Azure Recovery Services vault, view backups in hello vault, and restore from hello vault.</span></span>

### <a name="configure-hello-vault-register-hello-server-and-select-databases"></a><span data-ttu-id="4eca8-107">Configurar Olá cofre, registrar o servidor de saudação e selecionar bancos de dados</span><span class="sxs-lookup"><span data-stu-id="4eca8-107">Configure hello vault, register hello server, and select databases</span></span>

<span data-ttu-id="4eca8-108">Você [configurar um backups de tooretain automatizada de Cofre de serviços de recuperação do Azure](sql-database-long-term-retention.md) para um período maior que o período de retenção Olá para a camada de serviço.</span><span class="sxs-lookup"><span data-stu-id="4eca8-108">You [configure an Azure Recovery Services vault tooretain automated backups](sql-database-long-term-retention.md) for a period longer than hello retention period for your service tier.</span></span> 

1. <span data-ttu-id="4eca8-109">Olá abrir **do SQL Server** página para o servidor.</span><span class="sxs-lookup"><span data-stu-id="4eca8-109">Open hello **SQL Server** page for your server.</span></span>

   ![página do sql server](./media/sql-database-get-started-portal/sql-server-blade.png)

2. <span data-ttu-id="4eca8-111">Clique em **Retenção de backup de longo prazo**.</span><span class="sxs-lookup"><span data-stu-id="4eca8-111">Click **Long-term backup retention**.</span></span>

   ![link da retenção de backup de longo prazo](./media/sql-database-get-started-backup-recovery/long-term-backup-retention-link.png)

3. <span data-ttu-id="4eca8-113">Em Olá **retenção de backup de longo prazo** página para o servidor, revise e aceite os termos de visualização da saudação (a menos que você já tiver feito isso - ou esse recurso não está mais na visualização).</span><span class="sxs-lookup"><span data-stu-id="4eca8-113">On hello **Long-term backup retention** page for your server, review and accept hello preview terms (unless you have already done so - or this feature is no longer in preview).</span></span>

   ![Aceite os termos de visualização Olá](./media/sql-database-get-started-backup-recovery/accept-the-preview-terms.png)

4. <span data-ttu-id="4eca8-115">tooconfigure retenção de backup a longo prazo, selecione o banco de dados na grade de saudação e, em seguida, clique em **configurar** na barra de ferramentas de saudação.</span><span class="sxs-lookup"><span data-stu-id="4eca8-115">tooconfigure long-term backup retention, select that database in hello grid and then click **Configure** on hello toolbar.</span></span>

   ![selecionar o banco de dados para a retenção de backup de longo prazo](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

5. <span data-ttu-id="4eca8-117">Em Olá **configurar** , clique em **definir as configurações necessárias** em **cofre da recuperação de serviço**.</span><span class="sxs-lookup"><span data-stu-id="4eca8-117">On hello **Configure** page, click **Configure required settings** under **Recovery service vault**.</span></span>

   ![configurar link do cofre](./media/sql-database-get-started-backup-recovery/configure-vault-link.png)

6. <span data-ttu-id="4eca8-119">Em Olá **Cofre de serviços de recuperação** , selecione um cofre existente, se houver.</span><span class="sxs-lookup"><span data-stu-id="4eca8-119">On hello **Recovery services vault** page, select an existing vault, if any.</span></span> <span data-ttu-id="4eca8-120">Caso contrário, se nenhum Cofre de serviços de recuperação encontrado para a sua assinatura, clique em fluxo de saudação tooexit e crie um cofre de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="4eca8-120">Otherwise, if no recovery services vault found for your subscription, click tooexit hello flow and create a recovery services vault.</span></span>

   ![criar link do cofre](./media/sql-database-get-started-backup-recovery/create-new-vault-link.png)

7. <span data-ttu-id="4eca8-122">Em Olá **os cofres de serviços de recuperação** , clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4eca8-122">On hello **Recovery Services vaults** page, click **Add**.</span></span>

   ![adicionar link do cofre](./media/sql-database-get-started-backup-recovery/add-new-vault-link.png)
   
8. <span data-ttu-id="4eca8-124">Em Olá **Cofre de serviços de recuperação** , forneça um nome válido para o Cofre de serviços de recuperação de saudação.</span><span class="sxs-lookup"><span data-stu-id="4eca8-124">On hello **Recovery Services vault** page, provide a valid name for hello Recovery Services vault.</span></span>

   ![novo nome do cofre](./media/sql-database-get-started-backup-recovery/new-vault-name.png)

9. <span data-ttu-id="4eca8-126">Selecione sua assinatura e o grupo de recursos e, em seguida, selecione o local de Olá para o Cofre de saudação.</span><span class="sxs-lookup"><span data-stu-id="4eca8-126">Select your subscription and resource group, and then select hello location for hello vault.</span></span> <span data-ttu-id="4eca8-127">Quando terminar, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4eca8-127">When done, click **Create**.</span></span>

   ![criar cofre](./media/sql-database-get-started-backup-recovery/create-new-vault.png)

   > [!IMPORTANT]
   > <span data-ttu-id="4eca8-129">cofre Olá deve estar localizado no hello mesma região que o servidor lógico do SQL Azure hello e deve usar Olá mesmo grupo de recursos como o servidor lógico hello.</span><span class="sxs-lookup"><span data-stu-id="4eca8-129">hello vault must be located in hello same region as hello Azure SQL logical server, and must use hello same resource group as hello logical server.</span></span>
   >

10. <span data-ttu-id="4eca8-130">Após a criação do novo cofre de hello, execute Olá etapas necessárias tooreturn toohello **Cofre de serviços de recuperação** página.</span><span class="sxs-lookup"><span data-stu-id="4eca8-130">After hello new vault is created, execute hello necessary steps tooreturn toohello **Recovery services vault** page.</span></span>

11. <span data-ttu-id="4eca8-131">Em Olá **Cofre de serviços de recuperação** página, clique em cofre hello e, em seguida, clique em **selecione**.</span><span class="sxs-lookup"><span data-stu-id="4eca8-131">On hello **Recovery services vault** page, click hello vault and then click **Select**.</span></span>

   ![selecionar cofre existente](./media/sql-database-get-started-backup-recovery/select-existing-vault.png)

12. <span data-ttu-id="4eca8-133">Em Olá **configurar** página, forneça um nome válido para a nova política de retenção hello, modifique a política de retenção padrão Olá conforme apropriado e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="4eca8-133">On hello **Configure** page, provide a valid name for hello new retention policy, modify hello default retention policy as appropriate, and then click **OK**.</span></span>

   ![definir política de retenção](./media/sql-database-get-started-backup-recovery/define-retention-policy.png)

13. <span data-ttu-id="4eca8-135">Em Olá **retenção de backup de longo prazo** para seu banco de dados, clique em **salvar** e, em seguida, clique em **Okey** tooapply Olá longo prazo tooall de política de retenção de backup selecionado bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="4eca8-135">On hello **Long-term backup retention** page for your database, click **Save** and then click **OK** tooapply hello long-term backup retention policy tooall selected databases.</span></span>

   ![definir política de retenção](./media/sql-database-get-started-backup-recovery/save-retention-policy.png)

14. <span data-ttu-id="4eca8-137">Clique em **salvar** tooenable backup retenção de longo prazo usando esse novo cofre de serviços de recuperação do Azure de toohello de política que você configurou.</span><span class="sxs-lookup"><span data-stu-id="4eca8-137">Click **Save** tooenable long-term backup retention using this new policy toohello Azure Recovery Services vault that you configured.</span></span>

   ![definir política de retenção](./media/sql-database-get-started-backup-recovery/enable-long-term-retention.png)

> [!IMPORTANT]
> <span data-ttu-id="4eca8-139">Uma vez configurado, backups aparecem no cofre Olá nos próximos sete dias.</span><span class="sxs-lookup"><span data-stu-id="4eca8-139">Once configured, backups show up in hello vault within next seven days.</span></span> <span data-ttu-id="4eca8-140">Não continue neste tutorial até que os backups aparecem no cofre hello.</span><span class="sxs-lookup"><span data-stu-id="4eca8-140">Do not continue this tutorial until backups show up in hello vault.</span></span>
>

### <a name="view-backups-in-long-term-retention-using-azure-portal"></a><span data-ttu-id="4eca8-141">Exibir backups na retenção de longo prazo usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4eca8-141">View backups in long-term retention using Azure portal</span></span>

<span data-ttu-id="4eca8-142">Exiba informações sobre os backups de banco de dados na [retenção de backup de longo prazo](sql-database-long-term-retention.md).</span><span class="sxs-lookup"><span data-stu-id="4eca8-142">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

1. <span data-ttu-id="4eca8-143">No hello portal do Azure, abra seu Cofre de serviços de recuperação do Azure para seus backups de banco de dados (vá muito**todos os recursos** e selecioná-lo da lista de saudação de recursos para sua assinatura) tooview quantidade de saudação do armazenamento usado por seu banco de dados backups no cofre hello.</span><span class="sxs-lookup"><span data-stu-id="4eca8-143">In hello Azure portal, open your Azure Recovery Services vault for your database backups (go too**All resources** and select it from hello list of resources for your subscription) tooview hello amount of storage used by your database backups in hello vault.</span></span>

   ![exibir cofre dos serviços de recuperação com backups](./media/sql-database-get-started-backup-recovery/view-recovery-services-vault-with-data.png)

2. <span data-ttu-id="4eca8-145">Olá abrir **banco de dados SQL** página do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="4eca8-145">Open hello **SQL database** page for your database.</span></span>

   ![nova página de BD de exemplo](./media/sql-database-get-started-portal/new-sample-db-blade.png)

3. <span data-ttu-id="4eca8-147">Na barra de ferramentas hello, clique em **restauração**.</span><span class="sxs-lookup"><span data-stu-id="4eca8-147">On hello toolbar, click **Restore**.</span></span>

   ![barra de ferramentas de restauração](./media/sql-database-get-started-backup-recovery/restore-toolbar.png)

4. <span data-ttu-id="4eca8-149">Na página de restauração hello, clique em **longo prazo**.</span><span class="sxs-lookup"><span data-stu-id="4eca8-149">On hello Restore page, click **Long-term**.</span></span>

5. <span data-ttu-id="4eca8-150">Em backups de cofre do Azure, clique em **selecionar um backup** tooview backups de banco de dados disponível Olá no armazenamento de backup de longo prazo.</span><span class="sxs-lookup"><span data-stu-id="4eca8-150">Under Azure vault backups, click **Select a backup** tooview hello available database backups in long-term backup retention.</span></span>

   ![backups no cofre](./media/sql-database-get-started-backup-recovery/view-backups-in-vault.png)

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention-using-hello-azure-portal"></a><span data-ttu-id="4eca8-152">Restaurar um banco de dados de um backup em longo prazo retenção de backup usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4eca8-152">Restore a database from a backup in long-term backup retention using hello Azure portal</span></span>

<span data-ttu-id="4eca8-153">Você pode restaurar Olá tooa novo banco de dados de um backup em Olá que Cofre de serviços de recuperação do Azure.</span><span class="sxs-lookup"><span data-stu-id="4eca8-153">You restore hello database tooa new database from a backup in hello Azure Recovery Services vault.</span></span>

1. <span data-ttu-id="4eca8-154">Em Olá **backups do cofre do Azure** página, clique toorestore backup hello e, em seguida, clique em **selecione**.</span><span class="sxs-lookup"><span data-stu-id="4eca8-154">On hello **Azure vault backups** page, click hello backup toorestore and then click **Select**.</span></span>

   ![selecionar backup no cofre](./media/sql-database-get-started-backup-recovery/select-backup-in-vault.png)

2. <span data-ttu-id="4eca8-156">Em Olá **nome do banco de dados** texto caixa, forneça o nome de saudação do banco de dados restaurado de saudação.</span><span class="sxs-lookup"><span data-stu-id="4eca8-156">In hello **Database name** text box, provide hello name for hello restored database.</span></span>

   ![novo nome do banco de dados](./media/sql-database-get-started-backup-recovery/new-database-name.png)

3. <span data-ttu-id="4eca8-158">Clique em **Okey** toorestore seu banco de dados de backup Olá Olá cofre toohello novo banco de dados.</span><span class="sxs-lookup"><span data-stu-id="4eca8-158">Click **OK** toorestore your database from hello backup in hello vault toohello new database.</span></span>

4. <span data-ttu-id="4eca8-159">Na barra de ferramentas hello, clique em status Olá notificação ícone tooview saudação do trabalho de restauração hello.</span><span class="sxs-lookup"><span data-stu-id="4eca8-159">On hello toolbar, click hello notification icon tooview hello status of hello restore job.</span></span>

   ![progresso do trabalho de restauração no cofre](./media/sql-database-get-started-backup-recovery/restore-job-progress-long-term.png)

5. <span data-ttu-id="4eca8-161">Quando o trabalho de restauração Olá for concluído, abra Olá **bancos de dados SQL** banco de dados do página tooview Olá recentemente restaurado.</span><span class="sxs-lookup"><span data-stu-id="4eca8-161">When hello restore job is completed, open hello **SQL databases** page tooview hello newly restored database.</span></span>

   ![banco de dados restaurado a partir do cofre](./media/sql-database-get-started-backup-recovery/restored-database-from-vault.png)

> [!NOTE]
> <span data-ttu-id="4eca8-163">A partir daqui, você pode se conectar a banco de dados toohello restaurado usando tarefas de tooperform necessário do SQL Server Management Studio, como muito[extrair um pouco de dados de saudação restaurada toocopy de banco de dados no banco de dados existente do hello ou toodelete Olá existente nome de banco de dados de banco de dados e renomear Olá restaurado banco de dados toohello existente](sql-database-recovery-using-backups.md#point-in-time-restore).</span><span class="sxs-lookup"><span data-stu-id="4eca8-163">From here, you can connect toohello restored database using SQL Server Management Studio tooperform needed tasks, such as too[extract a bit of data from hello restored database toocopy into hello existing database or toodelete hello existing database and rename hello restored database toohello existing database name](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>
>

## <a name="powershell"></a><span data-ttu-id="4eca8-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4eca8-164">PowerShell</span></span>

<span data-ttu-id="4eca8-165">Olá seções a seguir mostra como toouse Cofre de serviços de recuperação do Azure para PowerShell tooconfigure hello, exibir backups no cofre hello e restaurar do cofre hello.</span><span class="sxs-lookup"><span data-stu-id="4eca8-165">hello following sections show you how toouse PowerShell tooconfigure hello Azure Recovery Services vault, view backups in hello vault, and restore from hello vault.</span></span>

### <a name="create-a-recovery-services-vault"></a><span data-ttu-id="4eca8-166">Criar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="4eca8-166">Create a recovery services vault</span></span>

<span data-ttu-id="4eca8-167">Saudação de uso [AzureRmRecoveryServicesVault novo](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) toocreate uma recuperação o Cofre de serviços.</span><span class="sxs-lookup"><span data-stu-id="4eca8-167">Use hello [New-AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) toocreate a recovery services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4eca8-168">cofre Olá deve estar localizado no hello mesma região que o servidor lógico do SQL Azure hello e deve usar Olá mesmo grupo de recursos como o servidor lógico hello.</span><span class="sxs-lookup"><span data-stu-id="4eca8-168">hello vault must be located in hello same region as hello Azure SQL logical server, and must use hello same resource group as hello logical server.</span></span>

```PowerShell
# Create a recovery services vault

#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$serverLocation = (Get-AzureRmSqlServer -ServerName $serverName -ResourceGroupName $resourceGroupName).Location
$recoveryServiceVaultName = "{new-vault-name}"

$vault = New-AzureRmRecoveryServicesVault -Name $recoveryServiceVaultName -ResourceGroupName $ResourceGroupName -Location $serverLocation 
Set-AzureRmRecoveryServicesBackupProperties -BackupStorageRedundancy LocallyRedundant -Vault $vault
```

### <a name="set-your-server-toouse-hello-recovery-vault-for-its-long-term-retention-backups"></a><span data-ttu-id="4eca8-169">Definir seu Cofre de recuperação do servidor toouse Olá para seus backups de retenção de longo prazo</span><span class="sxs-lookup"><span data-stu-id="4eca8-169">Set your server toouse hello recovery vault for its long-term retention backups</span></span>

<span data-ttu-id="4eca8-170">Saudação de uso [AzureRmSqlServerBackupLongTermRetentionVault conjunto](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) cmdlet tooassociate criado anteriormente Cofre de serviços de recuperação com um servidor específico do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4eca8-170">Use hello [Set-AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) cmdlet tooassociate a previously created recovery services vault with a specific Azure SQL server.</span></span>

```PowerShell
# Set your server toouse hello vault toofor long-term backup retention 

Set-AzureRmSqlServerBackupLongTermRetentionVault -ResourceGroupName $resourceGroupName -ServerName $serverName -ResourceId $vault.Id
```

### <a name="create-a-retention-policy"></a><span data-ttu-id="4eca8-171">Criar uma política de retenção</span><span class="sxs-lookup"><span data-stu-id="4eca8-171">Create a retention policy</span></span>

<span data-ttu-id="4eca8-172">Uma política de retenção é onde você define tookeep quanto tempo um backup de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="4eca8-172">A retention policy is where you set how long tookeep a database backup.</span></span> <span data-ttu-id="4eca8-173">Saudação de uso [AzureRmRecoveryServicesBackupRetentionPolicyObject Get](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet tooget saudação padrão retenção política toouse como modelo Olá para a criação de políticas.</span><span class="sxs-lookup"><span data-stu-id="4eca8-173">Use hello [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet tooget hello default retention policy toouse as hello template for creating policies.</span></span> <span data-ttu-id="4eca8-174">Neste modelo, o período de retenção de saudação é definido para 2 anos.</span><span class="sxs-lookup"><span data-stu-id="4eca8-174">In this template, hello retention period is set for 2 years.</span></span> <span data-ttu-id="4eca8-175">Em seguida, execute Olá [AzureRmRecoveryServicesBackupProtectionPolicy novo](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) toofinally Criar política de saudação.</span><span class="sxs-lookup"><span data-stu-id="4eca8-175">Next, run hello [New-AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) toofinally create hello policy.</span></span> 

> [!NOTE]
> <span data-ttu-id="4eca8-176">Alguns cmdlets exigem que você defina o contexto de cofre Olá antes de executar ([AzureRmRecoveryServicesVaultContext conjunto](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) para ver esse cmdlet em alguns trechos de código relacionados.</span><span class="sxs-lookup"><span data-stu-id="4eca8-176">Some cmdlets require that you set hello vault context before running ([Set-AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) so you see this cmdlet in a few related snippets.</span></span> <span data-ttu-id="4eca8-177">Você define o contexto de saudação porque a política de saudação é parte do cofre hello.</span><span class="sxs-lookup"><span data-stu-id="4eca8-177">You set hello context because hello policy is part of hello vault.</span></span> <span data-ttu-id="4eca8-178">Você pode criar várias políticas de retenção para cada compartimento e, em seguida, aplicar Olá desejado política toospecific bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="4eca8-178">You can create multiple retention policies for each vault and then apply hello desired policy toospecific databases.</span></span> 


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

### <a name="configure-a-database-toouse-hello-previously-defined-retention-policy"></a><span data-ttu-id="4eca8-179">Configurar uma política de retenção do banco de dados toouse Olá definido anteriormente</span><span class="sxs-lookup"><span data-stu-id="4eca8-179">Configure a database toouse hello previously defined retention policy</span></span>

<span data-ttu-id="4eca8-180">Saudação de uso [AzureRmSqlDatabaseBackupLongTermRetentionPolicy conjunto](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet tooapply Olá nova política tooa banco de dados específico.</span><span class="sxs-lookup"><span data-stu-id="4eca8-180">Use hello [Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet tooapply hello new policy tooa specific database.</span></span>

```PowerShell
# Enable long-term retention for a specific SQL database
$policyState = "enabled"
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -State $policyState -ResourceId $policy.Id
```

### <a name="view-backup-info-and-backups-in-long-term-retention"></a><span data-ttu-id="4eca8-181">Exibir informações de backup e backups de retenção de longo prazo</span><span class="sxs-lookup"><span data-stu-id="4eca8-181">View backup info, and backups in long-term retention</span></span>

<span data-ttu-id="4eca8-182">Exiba informações sobre os backups de banco de dados na [retenção de backup de longo prazo](sql-database-long-term-retention.md).</span><span class="sxs-lookup"><span data-stu-id="4eca8-182">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

<span data-ttu-id="4eca8-183">Use Olá cmdlets tooview fazer backup das informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="4eca8-183">Use hello following cmdlets tooview backup information:</span></span>

- [<span data-ttu-id="4eca8-184">Get-AzureRmRecoveryServicesBackupContainer</span><span class="sxs-lookup"><span data-stu-id="4eca8-184">Get-AzureRmRecoveryServicesBackupContainer</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)
- [<span data-ttu-id="4eca8-185">Get-AzureRmRecoveryServicesBackupItem</span><span class="sxs-lookup"><span data-stu-id="4eca8-185">Get-AzureRmRecoveryServicesBackupItem</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)
- [<span data-ttu-id="4eca8-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="4eca8-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)

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

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention"></a><span data-ttu-id="4eca8-187">Restaurar um banco de dados a partir de um backup na retenção de backup de longo prazo</span><span class="sxs-lookup"><span data-stu-id="4eca8-187">Restore a database from a backup in long-term backup retention</span></span>

<span data-ttu-id="4eca8-188">Restauração de retenção de backup de longo prazo utiliza Olá [AzureRmSqlDatabase restauração](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4eca8-188">Restoring from long-term backup retention uses hello [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet.</span></span>

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
> <span data-ttu-id="4eca8-189">A partir daqui, você pode se conectar a banco de dados de toohello restaurado usando tarefas do SQL Server Management Studio tooperform necessário, como tooextract um pouco de dados de saudação restaurado toocopy de banco de dados no banco de dados existente do hello ou banco de dados existente do hello toodelete e renomear Olá restaurado nome de banco de dados existente do banco de dados toohello.</span><span class="sxs-lookup"><span data-stu-id="4eca8-189">From here, you can connect toohello restored database using SQL Server Management Studio tooperform needed tasks, such as tooextract a bit of data from hello restored database toocopy into hello existing database or toodelete hello existing database and rename hello restored database toohello existing database name.</span></span> <span data-ttu-id="4eca8-190">Confira [recuperação pontual](sql-database-recovery-using-backups.md#point-in-time-restore).</span><span class="sxs-lookup"><span data-stu-id="4eca8-190">See [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4eca8-191">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4eca8-191">Next steps</span></span>

- <span data-ttu-id="4eca8-192">toolearn sobre backups automáticos gerado pelo serviço, consulte [backups automáticos](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="4eca8-192">toolearn about service-generated automatic backups, see [automatic backups](sql-database-automated-backups.md)</span></span>
- <span data-ttu-id="4eca8-193">toolearn sobre retenção de backup de longo prazo, consulte [retenção de backup de longo prazo](sql-database-long-term-retention.md)</span><span class="sxs-lookup"><span data-stu-id="4eca8-193">toolearn about long-term backup retention, see [long-term backup retention](sql-database-long-term-retention.md)</span></span>
- <span data-ttu-id="4eca8-194">toolearn sobre restauração de backups, consulte [restaurar do backup](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="4eca8-194">toolearn about restoring from backups, see [restore from backup](sql-database-recovery-using-backups.md)</span></span>
