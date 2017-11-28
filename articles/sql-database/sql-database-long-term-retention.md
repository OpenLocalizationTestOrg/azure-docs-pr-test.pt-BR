---
title: "Armazenar backups do Banco de Dados SQL do Azure por um período de até 10 anos | Microsoft Docs"
description: "Saiba como o Banco de Dados SQL do Azure dá suporte ao armazenamento de backups por um período de até 10 anos."
keywords: 
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 66fdb8b8-5903-4d3a-802e-af08d204566e
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 12/22/2016
ms.author: sashan
ms.openlocfilehash: 25e651203f804fbf32d632b5f83145a3f3f72a7f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="store-azure-sql-database-backups-for-up-to-10-years"></a><span data-ttu-id="1b48c-103">Armazenar backups do Banco de Dados SQL do Azure por um período de até 10 anos</span><span class="sxs-lookup"><span data-stu-id="1b48c-103">Store Azure SQL Database backups for up to 10 years</span></span>
<span data-ttu-id="1b48c-104">Muitos aplicativos têm fins regulamentares, de conformidade ou outros fins comerciais que exigem a retenção dos backups de banco de dados além dos 7 a 35 dias fornecidos pelos [backups automáticos](sql-database-automated-backups.md) do Banco de Dados SQL do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1b48c-104">Many applications have regulatory, compliance, or other business purposes that require you to retain database backups beyond the 7-35 days provided by Azure SQL Database [automatic backups](sql-database-automated-backups.md).</span></span> <span data-ttu-id="1b48c-105">Ao utilizar o recurso de retenção de backup de longo prazo, você poderá armazenar seus backups do Banco de Dados SQL em um cofre dos Serviços de Recuperação do Azure por um período de até 10 anos.</span><span class="sxs-lookup"><span data-stu-id="1b48c-105">By using the long-term backup retention feature, you can store your SQL database backups in an Azure Recovery Services vault for up to 10 years.</span></span> <span data-ttu-id="1b48c-106">É possível armazenar até 1.000 bancos de dados por cofre.</span><span class="sxs-lookup"><span data-stu-id="1b48c-106">You can store up to 1,000 databases per vault.</span></span> <span data-ttu-id="1b48c-107">Você poderá selecionar qualquer backup no cofre para restaurá-lo como um novo banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1b48c-107">You then can select any backup in the vault to restore it as a new database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1b48c-108">A retenção de backup de longo prazo está atualmente em versão prévia e está disponível nas seguintes regiões: Leste da Austrália, Sudeste da Austrália, Sul do Brasil, EUA Central, Ásia Oriental, Leste dos EUA, Leste dos EUA 2, Índia Central, Sul da Índia, Leste do Japão, Oeste do Japão, Centro-Norte dos EUA, Europa Setentrional, Centro-Sul dos EUA, Sudeste Asiático, Europa Ocidental e Oeste dos EUA.</span><span class="sxs-lookup"><span data-stu-id="1b48c-108">Long-term backup retention is currently in preview and available in the following regions: Australia East, Australia Southeast, Brazil South, Central US, East Asia, East US, East US 2, India Central, India South, Japan East, Japan West, North Central US, North Europe, South Central US, Southeast Asia, West Europe, and West US.</span></span>
>

> [!NOTE]
> <span data-ttu-id="1b48c-109">Habilite até 200 bancos de dados por cofre durante um período de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="1b48c-109">You can enable up to 200 databases per vault during a 24-hour period.</span></span> <span data-ttu-id="1b48c-110">É recomendável o uso de um cofre separado para cada servidor, a fim de minimizar o impacto desse limite.</span><span class="sxs-lookup"><span data-stu-id="1b48c-110">We recommend that you use a separate vault for each server to minimize the impact of this limit.</span></span> 
> 

## <a name="how-sql-database-long-term-backup-retention-works"></a><span data-ttu-id="1b48c-111">Como funciona a retenção de backup de longo prazo do banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="1b48c-111">How SQL Database long-term backup retention works</span></span>

<span data-ttu-id="1b48c-112">Com a retenção de backup de longo prazo é possível associar um servidor de banco de dados SQL com um cofre dos Serviços de Recuperação do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b48c-112">With long-term backup retention, you can associate a SQL database server with an Azure Recovery Services vault.</span></span> 

* <span data-ttu-id="1b48c-113">O cofre deve ser criado na mesma assinatura do Azure que criou o SQL server e na mesma região geográfica e grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1b48c-113">You must create the vault in the same Azure subscription that created the SQL server and in the same geographic region and resource group.</span></span> 
* <span data-ttu-id="1b48c-114">Em seguida, você configura uma política de retenção para qualquer banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1b48c-114">You then configure a retention policy for any database.</span></span> <span data-ttu-id="1b48c-115">A política faz com que os backups semanais de banco de dados completo sejam copiados para o cofre dos Serviços de Recuperação e retidos durante o período de retenção especificado (até 10 anos).</span><span class="sxs-lookup"><span data-stu-id="1b48c-115">The policy causes the weekly full database backups to be copied to the Recovery Services vault and retained for the specified retention period (up to 10 years).</span></span> 
* <span data-ttu-id="1b48c-116">Depois, será possível restaurar o banco de dados de qualquer um desses backups para um novo banco de dados em qualquer servidor na assinatura.</span><span class="sxs-lookup"><span data-stu-id="1b48c-116">You can then restore the database from any of these backups to a new database in any server in the subscription.</span></span> <span data-ttu-id="1b48c-117">O armazenamento do Azure cria uma cópia de backups existentes e a cópia não afeta o desempenho do banco de dados existente.</span><span class="sxs-lookup"><span data-stu-id="1b48c-117">Azure storage creates a copy from existing backups, and the copy has no performance impact on the existing database.</span></span>

> [!TIP]
> <span data-ttu-id="1b48c-118">Para um guia de instruções, consulte [Configurar e restaurar de uma retenção de backup de longo prazo do Banco de Dados SQL do Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="1b48c-118">For a how-to guide, see [Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="enable-long-term-backup-retention"></a><span data-ttu-id="1b48c-119">Habilitar retenção de backup de longo prazo</span><span class="sxs-lookup"><span data-stu-id="1b48c-119">Enable long-term backup retention</span></span>

<span data-ttu-id="1b48c-120">Para configurar a retenção de backup de longo prazo em um banco de dados:</span><span class="sxs-lookup"><span data-stu-id="1b48c-120">To configure long-term backup retention for a database:</span></span>

1. <span data-ttu-id="1b48c-121">Crie um cofre dos Serviços de Recuperação do Azure na mesma região, assinatura e grupo de recursos que o servidor de banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="1b48c-121">Create an Azure Recovery Services vault in the same region, subscription, and resource group as your SQL database server.</span></span> 
2. <span data-ttu-id="1b48c-122">Registre o servidor no cofre.</span><span class="sxs-lookup"><span data-stu-id="1b48c-122">Register the server to the vault.</span></span>
3. <span data-ttu-id="1b48c-123">Crie uma política de proteção dos Serviços de Recuperação do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b48c-123">Create an Azure Recovery Services protection policy.</span></span>
4. <span data-ttu-id="1b48c-124">Aplique a política de proteção aos bancos de dados que exigem a retenção de backup de longo prazo.</span><span class="sxs-lookup"><span data-stu-id="1b48c-124">Apply the protection policy to the databases that require long-term backup retention.</span></span>

<span data-ttu-id="1b48c-125">Para configurar, gerenciar e restaurar um banco de dados da retenção de backup de longo prazo de backups automatizados em um cofre dos Serviços de Recuperação do Azure, execute um desses procedimentos:</span><span class="sxs-lookup"><span data-stu-id="1b48c-125">To configure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of the following:</span></span>

* <span data-ttu-id="1b48c-126">Utilizando o Portal do Azure: Clique em **Retenção de backup de longo prazo**, selecione um banco de dados e, em seguida, clique em **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="1b48c-126">Using the Azure portal: Click **Long-term backup retention**, select a database, and then click **Configure**.</span></span> 

   ![Selecionar um banco de dados para retenção de backup a longo prazo](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

* <span data-ttu-id="1b48c-128">Utilizando o PowerShell: Vá para [Configurar e restaurar de uma retenção de backup de longo prazo do Banco de Dados SQL do Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="1b48c-128">Using PowerShell: Go to [Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="restore-a-database-thats-stored-with-the-long-term-backup-retention-feature"></a><span data-ttu-id="1b48c-129">Restaurar um banco de dados armazenado com o recurso de retenção de backup de longo prazo</span><span class="sxs-lookup"><span data-stu-id="1b48c-129">Restore a database that's stored with the long-term backup retention feature</span></span>

<span data-ttu-id="1b48c-130">Para fazer a recuperação com base em um backup com retenção de longo prazo:</span><span class="sxs-lookup"><span data-stu-id="1b48c-130">To recover from a long-term backup retention backup:</span></span>

1. <span data-ttu-id="1b48c-131">Liste o cofre em que o backup está armazenado.</span><span class="sxs-lookup"><span data-stu-id="1b48c-131">List the vault where the backup is stored.</span></span>
2. <span data-ttu-id="1b48c-132">Liste o contêiner que está mapeado para o servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="1b48c-132">List the container that is mapped to your logical server.</span></span>
3. <span data-ttu-id="1b48c-133">Liste a fonte de dados no cofre que está mapeada para o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1b48c-133">List the data source within the vault that is mapped to your database.</span></span>
4. <span data-ttu-id="1b48c-134">Liste os pontos de recuperação disponíveis para restauração.</span><span class="sxs-lookup"><span data-stu-id="1b48c-134">List the recovery points that are available to restore.</span></span>
5. <span data-ttu-id="1b48c-135">Restaure o banco de dados do ponto de recuperação para o servidor de destino em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="1b48c-135">Restore the database from the recovery point to the target server within your subscription.</span></span>

<span data-ttu-id="1b48c-136">Para configurar, gerenciar e restaurar um banco de dados da retenção de backup de longo prazo de backups automatizados em um cofre dos Serviços de Recuperação do Azure, execute um desses procedimentos:</span><span class="sxs-lookup"><span data-stu-id="1b48c-136">To configure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of the following:</span></span>

* <span data-ttu-id="1b48c-137">Utilizando o Portal do Azure: Vá para [Gerenciar a retenção de backup de longo prazo usando o portal do Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="1b48c-137">Using the Azure portal: Go to [Manage long-term backup retention using the Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="1b48c-138">Utilizando o PowerShell: Vá para [Gerenciar a retenção de backup de longo prazo usando o PowerShell](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="1b48c-138">Using PowerShell: Go to [Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="get-pricing-for-long-term-backup-retention"></a><span data-ttu-id="1b48c-139">Obter preços para a retenção de backup de longo prazo</span><span class="sxs-lookup"><span data-stu-id="1b48c-139">Get pricing for long-term backup retention</span></span>

<span data-ttu-id="1b48c-140">A retenção de backup de longo prazo de um Banco de Dados SQL é cobrada de acordo com as [taxas de preços dos serviços de backup do Azure](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="1b48c-140">Long-term backup retention of a SQL database is charged according to the [Azure backup services pricing rates](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="1b48c-141">Depois que o servidor de banco de dados SQL é registrado no cofre, você será cobrado pelo armazenamento total usado pelos backups semanais armazenados no cofre.</span><span class="sxs-lookup"><span data-stu-id="1b48c-141">After the SQL database server is registered to the vault, you are charged for the total storage that's used by the weekly backups stored in the vault.</span></span>

## <a name="view-available-backups-that-are-stored-in-long-term-backup-retention"></a><span data-ttu-id="1b48c-142">Exibir backups disponíveis que são armazenados na retenção de backup de longo prazo</span><span class="sxs-lookup"><span data-stu-id="1b48c-142">View available backups that are stored in long-term backup retention</span></span>

<span data-ttu-id="1b48c-143">Para configurar, gerenciar e restaurar um banco de dados da retenção de backup de longo prazo de backups automatizados em um cofre dos Serviços de Recuperação do Azure utilizando o portal do Azure, execute um desses procedimentos:</span><span class="sxs-lookup"><span data-stu-id="1b48c-143">To configure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault by using the Azure portal, do either of the following:</span></span>

* <span data-ttu-id="1b48c-144">Utilizando o Portal do Azure: Vá para [Gerenciar a retenção de backup de longo prazo usando o portal do Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="1b48c-144">Using the Azure portal: Go to [Manage long-term backup retention using the Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="1b48c-145">Utilizando o PowerShell: Vá para [Gerenciar a retenção de backup de longo prazo usando o PowerShell](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="1b48c-145">Using PowerShell: Go to [Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="disable-long-term-retention"></a><span data-ttu-id="1b48c-146">Desabilitar a retenção de longo prazo</span><span class="sxs-lookup"><span data-stu-id="1b48c-146">Disable long-term retention</span></span>

<span data-ttu-id="1b48c-147">O serviço de recuperação manipula automaticamente a limpeza de backups com base na política de retenção fornecida.</span><span class="sxs-lookup"><span data-stu-id="1b48c-147">The recovery service automatically handles the cleanup of backups based on the provided retention policy.</span></span> 

<span data-ttu-id="1b48c-148">Para parar de enviar os backups de um banco de dados específico para o cofre, remova a política de retenção do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1b48c-148">To stop sending the backups for a specific database to the vault, remove the retention policy for that database.</span></span>
  
```
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName 'RG1' -ServerName 'Server1' -DatabaseName 'DB1' -State 'Disabled' -ResourceId $policy.Id
```

> [!NOTE]
> <span data-ttu-id="1b48c-149">Os backups que já estão no cofre não são afetados.</span><span class="sxs-lookup"><span data-stu-id="1b48c-149">The backups that are already in the vault are unaffected.</span></span> <span data-ttu-id="1b48c-150">Eles são excluídos automaticamente pelo serviço de recuperação quando seu período de retenção expirar.</span><span class="sxs-lookup"><span data-stu-id="1b48c-150">They are automatically deleted by the recovery service when their retention period expires.</span></span>

## <a name="long-term-backup-retention-faq"></a><span data-ttu-id="1b48c-151">FAQ sobre retenção de backup de longo prazo</span><span class="sxs-lookup"><span data-stu-id="1b48c-151">Long-term backup retention FAQ</span></span>

<span data-ttu-id="1b48c-152">**Posso excluir manualmente os backups específicos no cofre?**</span><span class="sxs-lookup"><span data-stu-id="1b48c-152">**Can I manually delete specific backups in the vault?**</span></span>

<span data-ttu-id="1b48c-153">Não atualmente.</span><span class="sxs-lookup"><span data-stu-id="1b48c-153">Not currently.</span></span> <span data-ttu-id="1b48c-154">O cofre limpa os backups automaticamente quando o período de retenção expirar.</span><span class="sxs-lookup"><span data-stu-id="1b48c-154">The vault automatically cleans up backups when the retention period has expired.</span></span>

<span data-ttu-id="1b48c-155">**Posso registrar meu servidor para armazenar backups em mais de um cofre?**</span><span class="sxs-lookup"><span data-stu-id="1b48c-155">**Can I register my server to store backups to more than one vault?**</span></span>

<span data-ttu-id="1b48c-156">Não, atualmente só é possível armazenar backups em um cofre por vez.</span><span class="sxs-lookup"><span data-stu-id="1b48c-156">No, you can currently store backups to only one vault at a time.</span></span>

<span data-ttu-id="1b48c-157">**Posso ter um cofre e o servidor em assinaturas diferentes?**</span><span class="sxs-lookup"><span data-stu-id="1b48c-157">**Can I have a vault and server in different subscriptions?**</span></span>

<span data-ttu-id="1b48c-158">Não, atualmente o cofre e o servidor devem estar na mesma assinatura e no mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1b48c-158">No, currently the vault and server must be in the same subscription and resource group.</span></span>

<span data-ttu-id="1b48c-159">**Posso usar um cofre que criei em uma região diferente da região do servidor?**</span><span class="sxs-lookup"><span data-stu-id="1b48c-159">**Can I use a vault that I created in a region that's different from my server’s region?**</span></span>

<span data-ttu-id="1b48c-160">Não, o cofre e o servidor devem estar na mesma região para minimizar o tempo de cópia e evitar os encargos de tráfego.</span><span class="sxs-lookup"><span data-stu-id="1b48c-160">No, the vault and server must be in the same region to minimize copy time and avoid traffic charges.</span></span>

<span data-ttu-id="1b48c-161">**Quantos bancos de dados posso armazenar em um cofre?**</span><span class="sxs-lookup"><span data-stu-id="1b48c-161">**How many databases can I store in one vault?**</span></span>

<span data-ttu-id="1b48c-162">Atualmente, o suporte é para até 1.000 bancos de dados por cofre.</span><span class="sxs-lookup"><span data-stu-id="1b48c-162">Currently, we support up to 1,000 databases per vault.</span></span> 

<span data-ttu-id="1b48c-163">**Quantos cofres posso criar por assinatura?**</span><span class="sxs-lookup"><span data-stu-id="1b48c-163">**How many vaults can I create per subscription?**</span></span>

<span data-ttu-id="1b48c-164">Você pode criar até 25 cofres por assinatura.</span><span class="sxs-lookup"><span data-stu-id="1b48c-164">You can create up to 25 vaults per subscription.</span></span>

<span data-ttu-id="1b48c-165">**Quantos bancos de dados posso configurar por dia e por cofre?**</span><span class="sxs-lookup"><span data-stu-id="1b48c-165">**How many databases can I configure per day per vault?**</span></span>

<span data-ttu-id="1b48c-166">Só é possível configurar até 200 bancos de dados por dia e por cofre.</span><span class="sxs-lookup"><span data-stu-id="1b48c-166">You can set up 200 databases per day per vault.</span></span>

<span data-ttu-id="1b48c-167">**A retenção de backup de longo prazo funciona com pools elásticos?**</span><span class="sxs-lookup"><span data-stu-id="1b48c-167">**Does long-term backup retention work with elastic pools?**</span></span>

<span data-ttu-id="1b48c-168">Sim.</span><span class="sxs-lookup"><span data-stu-id="1b48c-168">Yes.</span></span> <span data-ttu-id="1b48c-169">Qualquer banco de dados no pool pode ser configurado com a política de retenção.</span><span class="sxs-lookup"><span data-stu-id="1b48c-169">Any database in the pool can be configured with the retention policy.</span></span>

<span data-ttu-id="1b48c-170">**Posso escolher a hora em que o backup é criado?**</span><span class="sxs-lookup"><span data-stu-id="1b48c-170">**Can I choose the time at which the backup is created?**</span></span>

<span data-ttu-id="1b48c-171">Não, o Banco de Dados SQL controla o agendamento de backups para minimizar o impacto no desempenho de seus bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="1b48c-171">No, SQL Database controls the backup schedule to minimize the performance impact on your databases.</span></span>

<span data-ttu-id="1b48c-172">**Tenho a transparent data encryption habilitada para meu banco de dados. Posso usá-lo com o cofre?**</span><span class="sxs-lookup"><span data-stu-id="1b48c-172">**I have transparent data encryption enabled for my database. Can I use it with the vault?**</span></span> 

<span data-ttu-id="1b48c-173">Sim, há suporte para a criptografia de dados transparente.</span><span class="sxs-lookup"><span data-stu-id="1b48c-173">Yes, transparent data encryption is supported.</span></span> <span data-ttu-id="1b48c-174">Você poderá restaurar o banco de dados do cofre mesmo se o banco de dados original não existir mais.</span><span class="sxs-lookup"><span data-stu-id="1b48c-174">You can restore the database from the vault even if the original database no longer exists.</span></span>

<span data-ttu-id="1b48c-175">**O que acontecerá com os backups no cofre se minha assinatura for suspensa?**</span><span class="sxs-lookup"><span data-stu-id="1b48c-175">**What happens with the backups in the vault if my subscription is suspended?**</span></span> 

<span data-ttu-id="1b48c-176">Se sua assinatura for suspensa, manteremos os bancos de dados e backups existentes.</span><span class="sxs-lookup"><span data-stu-id="1b48c-176">If your subscription is suspended, we retain the existing databases and backups.</span></span> <span data-ttu-id="1b48c-177">Novos backups não são copiados para o cofre.</span><span class="sxs-lookup"><span data-stu-id="1b48c-177">New backups are not copied to the vault.</span></span> <span data-ttu-id="1b48c-178">Depois que você reativar a assinatura, o serviço continua a copiar os backups no cofre.</span><span class="sxs-lookup"><span data-stu-id="1b48c-178">After you reactivate the subscription, the service resumes copying backups to the vault.</span></span> <span data-ttu-id="1b48c-179">Seu cofre torna-se acessível para as operações de restauração usando os backups que foram copiados nele antes da suspensão da assinatura.</span><span class="sxs-lookup"><span data-stu-id="1b48c-179">Your vault becomes accessible to the restore operations by using the backups that were copied there before the subscription was suspended.</span></span> 

<span data-ttu-id="1b48c-180">**Posso obter acesso aos arquivos de backup do banco de dados SQL para baixá-los ou restaurá-los no SQL Server?**</span><span class="sxs-lookup"><span data-stu-id="1b48c-180">**Can I get access to the SQL database backup files so I can download or restore them to the SQL server?**</span></span>

<span data-ttu-id="1b48c-181">Não no momento.</span><span class="sxs-lookup"><span data-stu-id="1b48c-181">No, not currently.</span></span>

<span data-ttu-id="1b48c-182">**É possível ter vários agendamentos (diário, semanal, mensal, anual) em uma política de retenção do SQL?**</span><span class="sxs-lookup"><span data-stu-id="1b48c-182">**Is it possible to have multiple schedules (daily, weekly, monthly, yearly) within a SQL retention policy.**</span></span>

<span data-ttu-id="1b48c-183">Não, atualmente vários agendamentos estão disponíveis apenas para backups de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="1b48c-183">No, multiple schedules are currently available only for virtual machine backups.</span></span>

<span data-ttu-id="1b48c-184">**E se configurarmos a retenção de backup de longo prazo em um banco de dados que é um banco de dados secundário de replicação geográfica ativa?**</span><span class="sxs-lookup"><span data-stu-id="1b48c-184">**What if we set up long-term backup retention on a database that is an active geo-replication secondary database?**</span></span>

<span data-ttu-id="1b48c-185">Como não fazemos backups em réplicas, atualmente não há nenhuma opção para retenção de backup de longo prazo em bancos de dados secundários.</span><span class="sxs-lookup"><span data-stu-id="1b48c-185">Because we don't take backups on replicas, there is currently no option for long-term backup retention on secondary databases.</span></span> <span data-ttu-id="1b48c-186">No entanto, é importante que os usuários configurem a retenção de backup de longo prazo em um banco de dados de replicação geográfica ativa por esses motivos:</span><span class="sxs-lookup"><span data-stu-id="1b48c-186">However, it is important for users to set up long-term backup retention on an active geo-replication secondary database for these reasons:</span></span>
* <span data-ttu-id="1b48c-187">Quando ocorrer um failover e o banco de dados se torna um banco de dados primário, fazemos um backup completo, o qual é carregado no cofre.</span><span class="sxs-lookup"><span data-stu-id="1b48c-187">When a failover happens and the database becomes a primary database, we take a full backup, which is uploaded to vault.</span></span>
* <span data-ttu-id="1b48c-188">Não há custo adicional ao cliente para configurar a retenção de backup de longo prazo em um banco de dados secundário.</span><span class="sxs-lookup"><span data-stu-id="1b48c-188">There is no extra cost to the customer for setting up long-term backup retention on a secondary database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b48c-189">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1b48c-189">Next steps</span></span>
<span data-ttu-id="1b48c-190">Como os backups de banco de dados protegem os dados de danos ou exclusão acidental, eles são uma parte essencial de qualquer estratégia de recuperação de desastre e continuidade dos negócios.</span><span class="sxs-lookup"><span data-stu-id="1b48c-190">Because database backups protect data from accidental corruption or deletion, they're an essential part of any business continuity and disaster recovery strategy.</span></span> <span data-ttu-id="1b48c-191">Para saber mais sobre as outras soluções de continuidade dos negócios do Banco de Dados SQL, consulte [Visão geral da continuidade dos negócios](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="1b48c-191">To learn about the other SQL Database business-continuity solutions, see [Business continuity overview](sql-database-business-continuity.md).</span></span>
