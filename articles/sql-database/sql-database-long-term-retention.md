---
title: backups de banco de dados do Azure SQL aaaStore para backup too10 anos | Microsoft Docs
description: Saiba como o banco de dados do SQL Azure oferece suporte a backups de armazenamento de backup too10 anos.
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
ms.openlocfilehash: 5825ebd4e3bd66b59b13aea603d377ef814a1df3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="store-azure-sql-database-backups-for-up-too10-years"></a><span data-ttu-id="40ae2-103">Armazenar os backups de banco de dados de SQL do Azure para backup too10 anos</span><span class="sxs-lookup"><span data-stu-id="40ae2-103">Store Azure SQL Database backups for up too10 years</span></span>
<span data-ttu-id="40ae2-104">Muitos aplicativos têm regulamentares, de conformidade ou outros negócios fins que exigem backups de banco de dados tooretain além Olá 7-35 dias fornecidos pelo banco de dados do SQL Azure [backups automáticos](sql-database-automated-backups.md).</span><span class="sxs-lookup"><span data-stu-id="40ae2-104">Many applications have regulatory, compliance, or other business purposes that require you tooretain database backups beyond hello 7-35 days provided by Azure SQL Database [automatic backups](sql-database-automated-backups.md).</span></span> <span data-ttu-id="40ae2-105">Usando o recurso de retenção de backup de longo prazo de saudação, você pode armazenar os backups de banco de dados SQL em um cofre de serviços de recuperação do Azure para backup too10 anos.</span><span class="sxs-lookup"><span data-stu-id="40ae2-105">By using hello long-term backup retention feature, you can store your SQL database backups in an Azure Recovery Services vault for up too10 years.</span></span> <span data-ttu-id="40ae2-106">Você pode armazenar até too1, 000 bancos de dados por cofre.</span><span class="sxs-lookup"><span data-stu-id="40ae2-106">You can store up too1,000 databases per vault.</span></span> <span data-ttu-id="40ae2-107">Você então pode selecionar qualquer backup no hello cofre toorestore-lo como um novo banco de dados.</span><span class="sxs-lookup"><span data-stu-id="40ae2-107">You then can select any backup in hello vault toorestore it as a new database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="40ae2-108">Retenção de backup de longo prazo está atualmente em visualização e está disponível em Olá seguintes regiões: Leste da Austrália, Sudeste da Austrália, Sul do Brasil, centro dos EUA, Ásia Oriental, Leste dos EUA, Leste dos EUA 2, Índia Central, Sul da Índia, Leste do Japão, oeste do Japão, Centro Norte dos EUA, Norte Centro Sul dos EUA, Europa, Sudeste da Ásia, Europa Ocidental e Oeste dos EUA.</span><span class="sxs-lookup"><span data-stu-id="40ae2-108">Long-term backup retention is currently in preview and available in hello following regions: Australia East, Australia Southeast, Brazil South, Central US, East Asia, East US, East US 2, India Central, India South, Japan East, Japan West, North Central US, North Europe, South Central US, Southeast Asia, West Europe, and West US.</span></span>
>

> [!NOTE]
> <span data-ttu-id="40ae2-109">Você pode habilitar o backup de bancos de dados too200 por cofre durante um período de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="40ae2-109">You can enable up too200 databases per vault during a 24-hour period.</span></span> <span data-ttu-id="40ae2-110">É recomendável que você use um cofre separado para cada servidor toominimize Olá o impacto desse limite.</span><span class="sxs-lookup"><span data-stu-id="40ae2-110">We recommend that you use a separate vault for each server toominimize hello impact of this limit.</span></span> 
> 

## <a name="how-sql-database-long-term-backup-retention-works"></a><span data-ttu-id="40ae2-111">Como funciona a retenção de backup de longo prazo do banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="40ae2-111">How SQL Database long-term backup retention works</span></span>

<span data-ttu-id="40ae2-112">Com a retenção de backup de longo prazo é possível associar um servidor de banco de dados SQL com um cofre dos Serviços de Recuperação do Azure.</span><span class="sxs-lookup"><span data-stu-id="40ae2-112">With long-term backup retention, you can associate a SQL database server with an Azure Recovery Services vault.</span></span> 

* <span data-ttu-id="40ae2-113">Você deve criar cofre Olá Olá a mesma assinatura do Azure que criou o servidor SQL Olá no e no hello mesmo grupo de recursos e região geográfico.</span><span class="sxs-lookup"><span data-stu-id="40ae2-113">You must create hello vault in hello same Azure subscription that created hello SQL server and in hello same geographic region and resource group.</span></span> 
* <span data-ttu-id="40ae2-114">Em seguida, você configura uma política de retenção para qualquer banco de dados.</span><span class="sxs-lookup"><span data-stu-id="40ae2-114">You then configure a retention policy for any database.</span></span> <span data-ttu-id="40ae2-115">Olá política causas Olá semanal completo do banco de dados backups toobe copiados toohello Cofre de serviços de recuperação e mantidos por um período de retenção especificado hello (backup too10 anos).</span><span class="sxs-lookup"><span data-stu-id="40ae2-115">hello policy causes hello weekly full database backups toobe copied toohello Recovery Services vault and retained for hello specified retention period (up too10 years).</span></span> 
* <span data-ttu-id="40ae2-116">Em seguida, pode restaurar banco de dados de saudação de qualquer um desses backups tooa novo banco de dados em qualquer servidor na assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="40ae2-116">You can then restore hello database from any of these backups tooa new database in any server in hello subscription.</span></span> <span data-ttu-id="40ae2-117">Armazenamento do Azure cria uma cópia de backup existente e cópia de saudação não tem nenhum impacto no desempenho no banco de dados existente do hello.</span><span class="sxs-lookup"><span data-stu-id="40ae2-117">Azure storage creates a copy from existing backups, and hello copy has no performance impact on hello existing database.</span></span>

> [!TIP]
> <span data-ttu-id="40ae2-118">Para um tooguide como, consulte [configurar e a restauração da retenção de backup de longo prazo do Azure SQL Database](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="40ae2-118">For a how-tooguide, see [Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="enable-long-term-backup-retention"></a><span data-ttu-id="40ae2-119">Habilitar retenção de backup de longo prazo</span><span class="sxs-lookup"><span data-stu-id="40ae2-119">Enable long-term backup retention</span></span>

<span data-ttu-id="40ae2-120">tooconfigure retenção de backup a longo prazo para um banco de dados:</span><span class="sxs-lookup"><span data-stu-id="40ae2-120">tooconfigure long-term backup retention for a database:</span></span>

1. <span data-ttu-id="40ae2-121">Crie um cofre de serviços de recuperação do Azure no hello mesmo grupo de recursos, assinatura e região que seu servidor de banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="40ae2-121">Create an Azure Recovery Services vault in hello same region, subscription, and resource group as your SQL database server.</span></span> 
2. <span data-ttu-id="40ae2-122">Registre o Cofre de toohello do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="40ae2-122">Register hello server toohello vault.</span></span>
3. <span data-ttu-id="40ae2-123">Crie uma política de proteção dos Serviços de Recuperação do Azure.</span><span class="sxs-lookup"><span data-stu-id="40ae2-123">Create an Azure Recovery Services protection policy.</span></span>
4. <span data-ttu-id="40ae2-124">Aplica Olá proteção política toohello bancos de dados que exigem a retenção de backup de longo prazo.</span><span class="sxs-lookup"><span data-stu-id="40ae2-124">Apply hello protection policy toohello databases that require long-term backup retention.</span></span>

<span data-ttu-id="40ae2-125">tooconfigure, gerenciar e restaurar um banco de dados de retenção de backup de longo prazo de backups automáticos em um cofre de serviços de recuperação do Azure, siga um destes procedimentos hello:</span><span class="sxs-lookup"><span data-stu-id="40ae2-125">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of hello following:</span></span>

* <span data-ttu-id="40ae2-126">Usando Olá portal do Azure: clique em **retenção de backup de longo prazo**, selecione um banco de dados e, em seguida, clique em **configurar**.</span><span class="sxs-lookup"><span data-stu-id="40ae2-126">Using hello Azure portal: Click **Long-term backup retention**, select a database, and then click **Configure**.</span></span> 

   ![Selecionar um banco de dados para retenção de backup a longo prazo](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

* <span data-ttu-id="40ae2-128">Usando o PowerShell: Ir muito[configurar e a restauração da retenção de backup de longo prazo do Azure SQL Database](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="40ae2-128">Using PowerShell: Go too[Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="restore-a-database-thats-stored-with-hello-long-term-backup-retention-feature"></a><span data-ttu-id="40ae2-129">Restaurar um banco de dados que é armazenado com o recurso de retenção de backup de longo prazo de Olá</span><span class="sxs-lookup"><span data-stu-id="40ae2-129">Restore a database that's stored with hello long-term backup retention feature</span></span>

<span data-ttu-id="40ae2-130">toorecover de um backup de retenção de backup de longo prazo:</span><span class="sxs-lookup"><span data-stu-id="40ae2-130">toorecover from a long-term backup retention backup:</span></span>

1. <span data-ttu-id="40ae2-131">Cofre de saudação lista onde Olá backup é armazenado.</span><span class="sxs-lookup"><span data-stu-id="40ae2-131">List hello vault where hello backup is stored.</span></span>
2. <span data-ttu-id="40ae2-132">Contêiner de saudação de lista é servidor lógico tooyour mapeada.</span><span class="sxs-lookup"><span data-stu-id="40ae2-132">List hello container that is mapped tooyour logical server.</span></span>
3. <span data-ttu-id="40ae2-133">Fonte de dados lista Olá no cofre de saudação que é mapeada tooyour banco de dados.</span><span class="sxs-lookup"><span data-stu-id="40ae2-133">List hello data source within hello vault that is mapped tooyour database.</span></span>
4. <span data-ttu-id="40ae2-134">Lista Olá pontos de recuperação que estão disponível toorestore.</span><span class="sxs-lookup"><span data-stu-id="40ae2-134">List hello recovery points that are available toorestore.</span></span>
5. <span data-ttu-id="40ae2-135">Restaure o banco de dados de saudação do servidor de destino de toohello de ponto de recuperação de Olá dentro de sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="40ae2-135">Restore hello database from hello recovery point toohello target server within your subscription.</span></span>

<span data-ttu-id="40ae2-136">tooconfigure, gerenciar e restaurar um banco de dados de retenção de backup de longo prazo de backups automáticos em um cofre de serviços de recuperação do Azure, siga um destes procedimentos hello:</span><span class="sxs-lookup"><span data-stu-id="40ae2-136">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of hello following:</span></span>

* <span data-ttu-id="40ae2-137">Usando Olá portal do Azure: ir muito[gerenciar usando o armazenamento de backup a longo prazo Olá portal do Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="40ae2-137">Using hello Azure portal: Go too[Manage long-term backup retention using hello Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="40ae2-138">Usando o PowerShell: Ir muito[gerenciar a retenção de backup a longo prazo, usando o PowerShell](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="40ae2-138">Using PowerShell: Go too[Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="get-pricing-for-long-term-backup-retention"></a><span data-ttu-id="40ae2-139">Obter preços para a retenção de backup de longo prazo</span><span class="sxs-lookup"><span data-stu-id="40ae2-139">Get pricing for long-term backup retention</span></span>

<span data-ttu-id="40ae2-140">Retenção de backup de longo prazo de um banco de dados SQL é cobrada de acordo com o toohello [serviços de backup do Azure, taxas de preço](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="40ae2-140">Long-term backup retention of a SQL database is charged according toohello [Azure backup services pricing rates](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="40ae2-141">Após o servidor de banco de dados SQL Olá cofre toohello registrado, você é cobrado para Olá total de armazenamento que é usado por backups semanais hello, armazenados no cofre hello.</span><span class="sxs-lookup"><span data-stu-id="40ae2-141">After hello SQL database server is registered toohello vault, you are charged for hello total storage that's used by hello weekly backups stored in hello vault.</span></span>

## <a name="view-available-backups-that-are-stored-in-long-term-backup-retention"></a><span data-ttu-id="40ae2-142">Exibir backups disponíveis que são armazenados na retenção de backup de longo prazo</span><span class="sxs-lookup"><span data-stu-id="40ae2-142">View available backups that are stored in long-term backup retention</span></span>

<span data-ttu-id="40ae2-143">tooconfigure, gerenciar e restaurar um banco de dados de retenção de backup de longo prazo de backups automáticos em um cofre de serviços de recuperação do Azure usando Olá portal do Azure, siga um destes procedimentos hello:</span><span class="sxs-lookup"><span data-stu-id="40ae2-143">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault by using hello Azure portal, do either of hello following:</span></span>

* <span data-ttu-id="40ae2-144">Usando Olá portal do Azure: ir muito[gerenciar usando o armazenamento de backup a longo prazo Olá portal do Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="40ae2-144">Using hello Azure portal: Go too[Manage long-term backup retention using hello Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="40ae2-145">Usando o PowerShell: Ir muito[gerenciar a retenção de backup a longo prazo, usando o PowerShell](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="40ae2-145">Using PowerShell: Go too[Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="disable-long-term-retention"></a><span data-ttu-id="40ae2-146">Desabilitar a retenção de longo prazo</span><span class="sxs-lookup"><span data-stu-id="40ae2-146">Disable long-term retention</span></span>

<span data-ttu-id="40ae2-147">o serviço de recuperação Olá automaticamente trata da limpeza de saudação dos backups com base em Olá fornecido a política de retenção.</span><span class="sxs-lookup"><span data-stu-id="40ae2-147">hello recovery service automatically handles hello cleanup of backups based on hello provided retention policy.</span></span> 

<span data-ttu-id="40ae2-148">backups de saudação envio toostop para um cofre de toohello do banco de dados específico, remover a política de retenção de saudação do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="40ae2-148">toostop sending hello backups for a specific database toohello vault, remove hello retention policy for that database.</span></span>
  
```
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName 'RG1' -ServerName 'Server1' -DatabaseName 'DB1' -State 'Disabled' -ResourceId $policy.Id
```

> [!NOTE]
> <span data-ttu-id="40ae2-149">backups de saudação que já estão no cofre Olá não são afetados.</span><span class="sxs-lookup"><span data-stu-id="40ae2-149">hello backups that are already in hello vault are unaffected.</span></span> <span data-ttu-id="40ae2-150">Eles são excluídos automaticamente pelo serviço de recuperação de saudação quando seu período de retenção expira.</span><span class="sxs-lookup"><span data-stu-id="40ae2-150">They are automatically deleted by hello recovery service when their retention period expires.</span></span>

## <a name="long-term-backup-retention-faq"></a><span data-ttu-id="40ae2-151">FAQ sobre retenção de backup de longo prazo</span><span class="sxs-lookup"><span data-stu-id="40ae2-151">Long-term backup retention FAQ</span></span>

<span data-ttu-id="40ae2-152">**Posso excluir manualmente os backups específicos no cofre Olá?**</span><span class="sxs-lookup"><span data-stu-id="40ae2-152">**Can I manually delete specific backups in hello vault?**</span></span>

<span data-ttu-id="40ae2-153">Não atualmente.</span><span class="sxs-lookup"><span data-stu-id="40ae2-153">Not currently.</span></span> <span data-ttu-id="40ae2-154">cofre Olá limpa backups automaticamente quando o período de retenção de saudação expirou.</span><span class="sxs-lookup"><span data-stu-id="40ae2-154">hello vault automatically cleans up backups when hello retention period has expired.</span></span>

<span data-ttu-id="40ae2-155">**Posso registrar meu toomore de backups do servidor toostore de um cofre?**</span><span class="sxs-lookup"><span data-stu-id="40ae2-155">**Can I register my server toostore backups toomore than one vault?**</span></span>

<span data-ttu-id="40ae2-156">Não, você pode armazenar no momento um compartimento de tooonly de backups por vez.</span><span class="sxs-lookup"><span data-stu-id="40ae2-156">No, you can currently store backups tooonly one vault at a time.</span></span>

<span data-ttu-id="40ae2-157">**Posso ter um cofre e o servidor em assinaturas diferentes?**</span><span class="sxs-lookup"><span data-stu-id="40ae2-157">**Can I have a vault and server in different subscriptions?**</span></span>

<span data-ttu-id="40ae2-158">Não, atualmente cofre hello e servidor devem estar no hello mesmo assinatura e grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="40ae2-158">No, currently hello vault and server must be in hello same subscription and resource group.</span></span>

<span data-ttu-id="40ae2-159">**Posso usar um cofre que criei em uma região diferente da região do servidor?**</span><span class="sxs-lookup"><span data-stu-id="40ae2-159">**Can I use a vault that I created in a region that's different from my server’s region?**</span></span>

<span data-ttu-id="40ae2-160">Não, o cofre hello e servidor devem estar no hello mesmo toominimize de região copiar tempo e evitar a cobrança de tráfego.</span><span class="sxs-lookup"><span data-stu-id="40ae2-160">No, hello vault and server must be in hello same region toominimize copy time and avoid traffic charges.</span></span>

<span data-ttu-id="40ae2-161">**Quantos bancos de dados posso armazenar em um cofre?**</span><span class="sxs-lookup"><span data-stu-id="40ae2-161">**How many databases can I store in one vault?**</span></span>

<span data-ttu-id="40ae2-162">Atualmente, há suporte para backup too1, 000 bancos de dados por cofre.</span><span class="sxs-lookup"><span data-stu-id="40ae2-162">Currently, we support up too1,000 databases per vault.</span></span> 

<span data-ttu-id="40ae2-163">**Quantos cofres posso criar por assinatura?**</span><span class="sxs-lookup"><span data-stu-id="40ae2-163">**How many vaults can I create per subscription?**</span></span>

<span data-ttu-id="40ae2-164">Você pode criar até too25 cofres por assinatura.</span><span class="sxs-lookup"><span data-stu-id="40ae2-164">You can create up too25 vaults per subscription.</span></span>

<span data-ttu-id="40ae2-165">**Quantos bancos de dados posso configurar por dia e por cofre?**</span><span class="sxs-lookup"><span data-stu-id="40ae2-165">**How many databases can I configure per day per vault?**</span></span>

<span data-ttu-id="40ae2-166">Só é possível configurar até 200 bancos de dados por dia e por cofre.</span><span class="sxs-lookup"><span data-stu-id="40ae2-166">You can set up 200 databases per day per vault.</span></span>

<span data-ttu-id="40ae2-167">**A retenção de backup de longo prazo funciona com pools elásticos?**</span><span class="sxs-lookup"><span data-stu-id="40ae2-167">**Does long-term backup retention work with elastic pools?**</span></span>

<span data-ttu-id="40ae2-168">Sim.</span><span class="sxs-lookup"><span data-stu-id="40ae2-168">Yes.</span></span> <span data-ttu-id="40ae2-169">Qualquer banco de dados no pool de saudação pode ser configurado com a política de retenção de saudação.</span><span class="sxs-lookup"><span data-stu-id="40ae2-169">Any database in hello pool can be configured with hello retention policy.</span></span>

<span data-ttu-id="40ae2-170">**Tempo de saudação em que o backup de saudação é criado pode escolher?**</span><span class="sxs-lookup"><span data-stu-id="40ae2-170">**Can I choose hello time at which hello backup is created?**</span></span>

<span data-ttu-id="40ae2-171">Não, o banco de dados SQL controla Olá agendamento de backup toominimize Olá impacto no desempenho de seus bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="40ae2-171">No, SQL Database controls hello backup schedule toominimize hello performance impact on your databases.</span></span>

<span data-ttu-id="40ae2-172">**Tenho a transparent data encryption habilitada para meu banco de dados. Posso usá-lo com o cofre Olá?**</span><span class="sxs-lookup"><span data-stu-id="40ae2-172">**I have transparent data encryption enabled for my database. Can I use it with hello vault?**</span></span> 

<span data-ttu-id="40ae2-173">Sim, há suporte para a criptografia de dados transparente.</span><span class="sxs-lookup"><span data-stu-id="40ae2-173">Yes, transparent data encryption is supported.</span></span> <span data-ttu-id="40ae2-174">Pode restaurar banco de dados de saudação do cofre Olá mesmo se o banco de dados original Olá não existe mais.</span><span class="sxs-lookup"><span data-stu-id="40ae2-174">You can restore hello database from hello vault even if hello original database no longer exists.</span></span>

<span data-ttu-id="40ae2-175">**O que acontece com backups Olá no cofre Olá se minha assinatura está suspensa?**</span><span class="sxs-lookup"><span data-stu-id="40ae2-175">**What happens with hello backups in hello vault if my subscription is suspended?**</span></span> 

<span data-ttu-id="40ae2-176">Se sua assinatura for suspensa, podemos manter backups e bancos de dados existentes do hello.</span><span class="sxs-lookup"><span data-stu-id="40ae2-176">If your subscription is suspended, we retain hello existing databases and backups.</span></span> <span data-ttu-id="40ae2-177">Novos backups não são copiados toohello cofre.</span><span class="sxs-lookup"><span data-stu-id="40ae2-177">New backups are not copied toohello vault.</span></span> <span data-ttu-id="40ae2-178">Após você reativar a assinatura hello, o serviço de saudação retoma copiando backups toohello cofre.</span><span class="sxs-lookup"><span data-stu-id="40ae2-178">After you reactivate hello subscription, hello service resumes copying backups toohello vault.</span></span> <span data-ttu-id="40ae2-179">Seu cofre torna-se acessível toohello operações de restauração usando backups de saudação que foram copiados existe antes de saudação assinatura foi suspensa.</span><span class="sxs-lookup"><span data-stu-id="40ae2-179">Your vault becomes accessible toohello restore operations by using hello backups that were copied there before hello subscription was suspended.</span></span> 

<span data-ttu-id="40ae2-180">**Posso obter acesso toohello arquivos de backup do banco de dados SQL para download ou restaurá-los toohello SQL server?**</span><span class="sxs-lookup"><span data-stu-id="40ae2-180">**Can I get access toohello SQL database backup files so I can download or restore them toohello SQL server?**</span></span>

<span data-ttu-id="40ae2-181">Não no momento.</span><span class="sxs-lookup"><span data-stu-id="40ae2-181">No, not currently.</span></span>

<span data-ttu-id="40ae2-182">**É possível toohave vários agendamentos (diária, semanal, mensal, anual) dentro de uma política de retenção SQL.**</span><span class="sxs-lookup"><span data-stu-id="40ae2-182">**Is it possible toohave multiple schedules (daily, weekly, monthly, yearly) within a SQL retention policy.**</span></span>

<span data-ttu-id="40ae2-183">Não, atualmente vários agendamentos estão disponíveis apenas para backups de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="40ae2-183">No, multiple schedules are currently available only for virtual machine backups.</span></span>

<span data-ttu-id="40ae2-184">**E se configurarmos a retenção de backup de longo prazo em um banco de dados que é um banco de dados secundário de replicação geográfica ativa?**</span><span class="sxs-lookup"><span data-stu-id="40ae2-184">**What if we set up long-term backup retention on a database that is an active geo-replication secondary database?**</span></span>

<span data-ttu-id="40ae2-185">Como não fazemos backups em réplicas, atualmente não há nenhuma opção para retenção de backup de longo prazo em bancos de dados secundários.</span><span class="sxs-lookup"><span data-stu-id="40ae2-185">Because we don't take backups on replicas, there is currently no option for long-term backup retention on secondary databases.</span></span> <span data-ttu-id="40ae2-186">No entanto, é importante para os usuários tooset a retenção de backup de longo prazo em um banco de dados secundário de replicação geográfica ativa por esses motivos:</span><span class="sxs-lookup"><span data-stu-id="40ae2-186">However, it is important for users tooset up long-term backup retention on an active geo-replication secondary database for these reasons:</span></span>
* <span data-ttu-id="40ae2-187">Quando ocorre um failover e o banco de dados de saudação se torna um banco de dados primário, podemos usar um backup completo, que é carregado toovault.</span><span class="sxs-lookup"><span data-stu-id="40ae2-187">When a failover happens and hello database becomes a primary database, we take a full backup, which is uploaded toovault.</span></span>
* <span data-ttu-id="40ae2-188">Não há nenhum extra ao cliente toohello de custo para configurar a retenção de backup de longo prazo em um banco de dados secundário.</span><span class="sxs-lookup"><span data-stu-id="40ae2-188">There is no extra cost toohello customer for setting up long-term backup retention on a secondary database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40ae2-189">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="40ae2-189">Next steps</span></span>
<span data-ttu-id="40ae2-190">Como os backups de banco de dados protegem os dados de danos ou exclusão acidental, eles são uma parte essencial de qualquer estratégia de recuperação de desastre e continuidade dos negócios.</span><span class="sxs-lookup"><span data-stu-id="40ae2-190">Because database backups protect data from accidental corruption or deletion, they're an essential part of any business continuity and disaster recovery strategy.</span></span> <span data-ttu-id="40ae2-191">toolearn sobre Olá outras soluções de continuidade de negócios do banco de dados SQL, consulte [visão geral de continuidade de negócios](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="40ae2-191">toolearn about hello other SQL Database business-continuity solutions, see [Business continuity overview](sql-database-business-continuity.md).</span></span>
