---
title: Migrar seu data warehouse existente do Azure para o armazenamento premium | Microsoft Docs
description: "Instruções para migrar um data warehouse existente para o armazenamento premium"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: barbkess
editor: 
ms.assetid: 04b05dea-c066-44a0-9751-0774eb84c689
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 11/29/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 860e50b532b4b0a21d3be54f087730070b0e56bb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-data-warehouse-to-premium-storage"></a><span data-ttu-id="3a45b-103">Migrar seu data warehouse para o armazenamento premium</span><span class="sxs-lookup"><span data-stu-id="3a45b-103">Migrate your data warehouse to premium storage</span></span>
<span data-ttu-id="3a45b-104">Recentemente, o Azure SQL Data Warehouse apresentou o [Armazenamento premium para maior previsibilidade de desempenho][premium storage for greater performance predictability].</span><span class="sxs-lookup"><span data-stu-id="3a45b-104">Azure SQL Data Warehouse recently introduced [premium storage for greater performance predictability][premium storage for greater performance predictability].</span></span> <span data-ttu-id="3a45b-105">Agora, os data warehouses existentes atualmente no armazenamento standard podem ser migrados para o armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="3a45b-105">Existing data warehouses currently on standard storage can now be migrated to premium storage.</span></span> <span data-ttu-id="3a45b-106">Você pode aproveitar a migração automática ou, se preferir controlar quando migrar (o que envolve algum tempo de inatividade), você mesmo pode fazer a migração.</span><span class="sxs-lookup"><span data-stu-id="3a45b-106">You can take advantage of automatic migration, or if you prefer to control when to migrate (which does involve some downtime), you can do the migration yourself.</span></span>

<span data-ttu-id="3a45b-107">Se você tiver mais de um data warehouse, use o [agendamento de migração automática][automatic migration schedule] para determinar quando ele será migrado também.</span><span class="sxs-lookup"><span data-stu-id="3a45b-107">If you have more than one data warehouse, use the [automatic migration schedule][automatic migration schedule] to determine when it will also be migrated.</span></span>

## <a name="determine-storage-type"></a><span data-ttu-id="3a45b-108">Determinar o tipo de armazenamento</span><span class="sxs-lookup"><span data-stu-id="3a45b-108">Determine storage type</span></span>
<span data-ttu-id="3a45b-109">Se você criou um data warehouse antes das datas abaixo, estará usando o armazenamento standard.</span><span class="sxs-lookup"><span data-stu-id="3a45b-109">If you created a data warehouse before the following dates, you are currently using standard storage.</span></span>

| <span data-ttu-id="3a45b-110">**Região**</span><span class="sxs-lookup"><span data-stu-id="3a45b-110">**Region**</span></span> | <span data-ttu-id="3a45b-111">**Data warehouse criado antes desta data**</span><span class="sxs-lookup"><span data-stu-id="3a45b-111">**Data warehouse created before this date**</span></span> |
|:--- |:--- |
| <span data-ttu-id="3a45b-112">Leste da Austrália</span><span class="sxs-lookup"><span data-stu-id="3a45b-112">Australia East</span></span> |<span data-ttu-id="3a45b-113">Armazenamento premium ainda não disponível</span><span class="sxs-lookup"><span data-stu-id="3a45b-113">Premium storage not yet available</span></span> |
| <span data-ttu-id="3a45b-114">Leste da China</span><span class="sxs-lookup"><span data-stu-id="3a45b-114">China East</span></span> |<span data-ttu-id="3a45b-115">1º de novembro de 2016</span><span class="sxs-lookup"><span data-stu-id="3a45b-115">November 1, 2016</span></span> |
| <span data-ttu-id="3a45b-116">Norte da China</span><span class="sxs-lookup"><span data-stu-id="3a45b-116">China North</span></span> |<span data-ttu-id="3a45b-117">1º de novembro de 2016</span><span class="sxs-lookup"><span data-stu-id="3a45b-117">November 1, 2016</span></span> |
| <span data-ttu-id="3a45b-118">Alemanha Central</span><span class="sxs-lookup"><span data-stu-id="3a45b-118">Germany Central</span></span> |<span data-ttu-id="3a45b-119">1º de novembro de 2016</span><span class="sxs-lookup"><span data-stu-id="3a45b-119">November 1, 2016</span></span> |
| <span data-ttu-id="3a45b-120">Nordeste da Alemanha</span><span class="sxs-lookup"><span data-stu-id="3a45b-120">Germany Northeast</span></span> |<span data-ttu-id="3a45b-121">1º de novembro de 2016</span><span class="sxs-lookup"><span data-stu-id="3a45b-121">November 1, 2016</span></span> |
| <span data-ttu-id="3a45b-122">Oeste da Índia</span><span class="sxs-lookup"><span data-stu-id="3a45b-122">India West</span></span> |<span data-ttu-id="3a45b-123">Armazenamento premium ainda não disponível</span><span class="sxs-lookup"><span data-stu-id="3a45b-123">Premium storage not yet available</span></span> |
| <span data-ttu-id="3a45b-124">Oeste do Japão</span><span class="sxs-lookup"><span data-stu-id="3a45b-124">Japan West</span></span> |<span data-ttu-id="3a45b-125">Armazenamento premium ainda não disponível</span><span class="sxs-lookup"><span data-stu-id="3a45b-125">Premium storage not yet available</span></span> |
| <span data-ttu-id="3a45b-126">Centro-Norte dos EUA</span><span class="sxs-lookup"><span data-stu-id="3a45b-126">North Central US</span></span> |<span data-ttu-id="3a45b-127">10 de novembro de 2016</span><span class="sxs-lookup"><span data-stu-id="3a45b-127">November 10, 2016</span></span> |

## <a name="automatic-migration-details"></a><span data-ttu-id="3a45b-128">Detalhes da migração automática</span><span class="sxs-lookup"><span data-stu-id="3a45b-128">Automatic migration details</span></span>
<span data-ttu-id="3a45b-129">Por padrão, migraremos seu banco de dados para você entre 18h e 6h na hora do local de sua região durante o [agendamento de migração automática][automatic migration schedule].</span><span class="sxs-lookup"><span data-stu-id="3a45b-129">By default, we will migrate your database for you between 6:00 PM and 6:00 AM in your region's local time during the [automatic migration schedule][automatic migration schedule].</span></span> <span data-ttu-id="3a45b-130">Seu data warehouse existente ficará inutilizável durante a migração.</span><span class="sxs-lookup"><span data-stu-id="3a45b-130">Your existing data warehouse will be unusable during the migration.</span></span> <span data-ttu-id="3a45b-131">A migração levará cerca de uma hora por terabyte de armazenamento por data warehouse.</span><span class="sxs-lookup"><span data-stu-id="3a45b-131">The migration will take approximately one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="3a45b-132">Não haverá cobrança durante qualquer parte da migração automática.</span><span class="sxs-lookup"><span data-stu-id="3a45b-132">You will not be charged during any portion of the automatic migration.</span></span>

> [!NOTE]
> <span data-ttu-id="3a45b-133">Após a conclusão da migração, o data warehouse ficará online e utilizável novamente.</span><span class="sxs-lookup"><span data-stu-id="3a45b-133">When the migration is complete, your data warehouse will be back online and usable.</span></span>
>
>

<span data-ttu-id="3a45b-134">A Microsoft está executando as etapas a seguir para concluir a migração (elas não exigem qualquer envolvimento de sua parte).</span><span class="sxs-lookup"><span data-stu-id="3a45b-134">Microsoft is taking the following steps to complete the migration (these do not require any involvement on your part).</span></span> <span data-ttu-id="3a45b-135">Neste exemplo, imagine que o data warehouse existente no armazenamento standard é chamado atualmente de "MyDW".</span><span class="sxs-lookup"><span data-stu-id="3a45b-135">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="3a45b-136">A Microsoft renomeia “MyDW” para “MyDW_DO_NOT_USE_[Carimbo de data/hora]”</span><span class="sxs-lookup"><span data-stu-id="3a45b-136">Microsoft renames “MyDW” to “MyDW_DO_NOT_USE_[Timestamp].”</span></span>
2. <span data-ttu-id="3a45b-137">A Microsoft pausa o “MyDW_DO_NOT_USE_[carimbo de data/hora]”.</span><span class="sxs-lookup"><span data-stu-id="3a45b-137">Microsoft pauses “MyDW_DO_NOT_USE_[Timestamp].”</span></span> <span data-ttu-id="3a45b-138">Durante esse tempo, um backup é feito.</span><span class="sxs-lookup"><span data-stu-id="3a45b-138">During this time, a backup is taken.</span></span> <span data-ttu-id="3a45b-139">Você poderá ver várias pausas e retomadas se encontrarmos problemas durante o processo.</span><span class="sxs-lookup"><span data-stu-id="3a45b-139">You may see multiple pauses and resumes if we encounter any issues during this process.</span></span>
3. <span data-ttu-id="3a45b-140">A Microsoft cria um novo data warehouse chamado "MyDW" no armazenamento premium do backup feito na etapa 2.</span><span class="sxs-lookup"><span data-stu-id="3a45b-140">Microsoft creates a new data warehouse named “MyDW” on premium storage from the backup taken in step 2.</span></span> <span data-ttu-id="3a45b-141">"MyDW" não será exibido até a restauração ser concluída.</span><span class="sxs-lookup"><span data-stu-id="3a45b-141">“MyDW” will not appear until after the restore is complete.</span></span>
4. <span data-ttu-id="3a45b-142">Após a conclusão da restauração, "MyDW" retornará para as mesmas unidades de data warehouse e para o mesmo estado (em pausa ou ativo) em que estava antes da migração.</span><span class="sxs-lookup"><span data-stu-id="3a45b-142">After the restore is complete, “MyDW” returns to the same data warehouse units and state (paused or active) that it was before the migration.</span></span>
5. <span data-ttu-id="3a45b-143">Após a conclusão da migração, a Microsoft excluirá "MyDW_DO_NOT_USE_ [Carimbo de data/hora]".</span><span class="sxs-lookup"><span data-stu-id="3a45b-143">After the migration is complete, Microsoft deletes “MyDW_DO_NOT_USE_[Timestamp]”.</span></span>

> [!NOTE]
> <span data-ttu-id="3a45b-144">As configurações a seguir não são transferidas como parte da migração:</span><span class="sxs-lookup"><span data-stu-id="3a45b-144">The following settings do not carry over as part of the migration:</span></span>
>
> * <span data-ttu-id="3a45b-145">A auditoria no nível do banco de dados precisa ser habilitada novamente.</span><span class="sxs-lookup"><span data-stu-id="3a45b-145">Auditing at the database level needs to be re-enabled.</span></span>
> * <span data-ttu-id="3a45b-146">As regras de firewall no nível do banco de dados precisam ser adicionadas novamente.</span><span class="sxs-lookup"><span data-stu-id="3a45b-146">Firewall rules at the database level need to be re-added.</span></span> <span data-ttu-id="3a45b-147">As regras de firewall no nível do servidor não deverão ser afetadas.</span><span class="sxs-lookup"><span data-stu-id="3a45b-147">Firewall rules at the server level are not affected.</span></span>
>
>

### <a name="automatic-migration-schedule"></a><span data-ttu-id="3a45b-148">cronograma de migração automática</span><span class="sxs-lookup"><span data-stu-id="3a45b-148">Automatic migration schedule</span></span>
<span data-ttu-id="3a45b-149">As migrações automáticas ocorrem das 18h às 6h (hora local por região) durante o cronograma de interrupção a seguir.</span><span class="sxs-lookup"><span data-stu-id="3a45b-149">Automatic migrations occur between 6:00 PM and 6:00 AM (local time per region) during the following outage schedule.</span></span>

| <span data-ttu-id="3a45b-150">**Região**</span><span class="sxs-lookup"><span data-stu-id="3a45b-150">**Region**</span></span> | <span data-ttu-id="3a45b-151">**Data de início estimada**</span><span class="sxs-lookup"><span data-stu-id="3a45b-151">**Estimated start date**</span></span> | <span data-ttu-id="3a45b-152">**Data de término estimada**</span><span class="sxs-lookup"><span data-stu-id="3a45b-152">**Estimated end date**</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3a45b-153">Leste da Austrália</span><span class="sxs-lookup"><span data-stu-id="3a45b-153">Australia East</span></span> |<span data-ttu-id="3a45b-154">Ainda não foi determinado</span><span class="sxs-lookup"><span data-stu-id="3a45b-154">Not determined yet</span></span> |<span data-ttu-id="3a45b-155">Ainda não foi determinado</span><span class="sxs-lookup"><span data-stu-id="3a45b-155">Not determined yet</span></span> |
| <span data-ttu-id="3a45b-156">Leste da China</span><span class="sxs-lookup"><span data-stu-id="3a45b-156">China East</span></span> |<span data-ttu-id="3a45b-157">9 de janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="3a45b-157">January 9, 2017</span></span> |<span data-ttu-id="3a45b-158">13 de janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="3a45b-158">January 13, 2017</span></span> |
| <span data-ttu-id="3a45b-159">Norte da China</span><span class="sxs-lookup"><span data-stu-id="3a45b-159">China North</span></span> |<span data-ttu-id="3a45b-160">9 de janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="3a45b-160">January 9, 2017</span></span> |<span data-ttu-id="3a45b-161">13 de janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="3a45b-161">January 13, 2017</span></span> |
| <span data-ttu-id="3a45b-162">Alemanha Central</span><span class="sxs-lookup"><span data-stu-id="3a45b-162">Germany Central</span></span> |<span data-ttu-id="3a45b-163">9 de janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="3a45b-163">January 9, 2017</span></span> |<span data-ttu-id="3a45b-164">13 de janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="3a45b-164">January 13, 2017</span></span> |
| <span data-ttu-id="3a45b-165">Nordeste da Alemanha</span><span class="sxs-lookup"><span data-stu-id="3a45b-165">Germany Northeast</span></span> |<span data-ttu-id="3a45b-166">9 de janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="3a45b-166">January 9, 2017</span></span> |<span data-ttu-id="3a45b-167">13 de janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="3a45b-167">January 13, 2017</span></span> |
| <span data-ttu-id="3a45b-168">Oeste da Índia</span><span class="sxs-lookup"><span data-stu-id="3a45b-168">India West</span></span> |<span data-ttu-id="3a45b-169">Ainda não foi determinado</span><span class="sxs-lookup"><span data-stu-id="3a45b-169">Not determined yet</span></span> |<span data-ttu-id="3a45b-170">Ainda não foi determinado</span><span class="sxs-lookup"><span data-stu-id="3a45b-170">Not determined yet</span></span> |
| <span data-ttu-id="3a45b-171">Oeste do Japão</span><span class="sxs-lookup"><span data-stu-id="3a45b-171">Japan West</span></span> |<span data-ttu-id="3a45b-172">Ainda não foi determinado</span><span class="sxs-lookup"><span data-stu-id="3a45b-172">Not determined yet</span></span> |<span data-ttu-id="3a45b-173">Ainda não foi determinado</span><span class="sxs-lookup"><span data-stu-id="3a45b-173">Not determined yet</span></span> |
| <span data-ttu-id="3a45b-174">Centro-Norte dos EUA</span><span class="sxs-lookup"><span data-stu-id="3a45b-174">North Central US</span></span> |<span data-ttu-id="3a45b-175">9 de janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="3a45b-175">January 9, 2017</span></span> |<span data-ttu-id="3a45b-176">13 de janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="3a45b-176">January 13, 2017</span></span> |

## <a name="self-migration-to-premium-storage"></a><span data-ttu-id="3a45b-177">Automigração para o armazenamento premium</span><span class="sxs-lookup"><span data-stu-id="3a45b-177">Self-migration to premium storage</span></span>
<span data-ttu-id="3a45b-178">Se quiser controlar quando o tempo de inatividade deverá ocorrer, você poderá usar as etapas a seguir para migrar um data warehouse existente no armazenamento standard para o armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="3a45b-178">If you want to control when your downtime will occur, you can use the following steps to migrate an existing data warehouse on standard storage to premium storage.</span></span> <span data-ttu-id="3a45b-179">Se você escolher essa opção, deverá concluir a migração antes de a migração automática começar nessa região.</span><span class="sxs-lookup"><span data-stu-id="3a45b-179">If you choose this option, you must complete the self-migration before the automatic migration begins in that region.</span></span> <span data-ttu-id="3a45b-180">Isso evita qualquer risco de a migração automática causar um conflito (consulte a [agendamento de migração automática][automatic migration schedule]).</span><span class="sxs-lookup"><span data-stu-id="3a45b-180">This ensures that you avoid any risk of the automatic migration causing a conflict (refer to the [automatic migration schedule][automatic migration schedule]).</span></span>

### <a name="self-migration-instructions"></a><span data-ttu-id="3a45b-181">Instruções de automigração</span><span class="sxs-lookup"><span data-stu-id="3a45b-181">Self-migration instructions</span></span>
<span data-ttu-id="3a45b-182">Para você mesmo migrar seu data warehouse, use os recursos de backup e restauração.</span><span class="sxs-lookup"><span data-stu-id="3a45b-182">To migrate your data warehouse yourself, use the backup and restore features.</span></span> <span data-ttu-id="3a45b-183">A parte de restauração da migração deve demorar cerca de uma hora por terabyte de armazenamento por data warehouse.</span><span class="sxs-lookup"><span data-stu-id="3a45b-183">The restore portion of the migration is expected to take around one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="3a45b-184">Se você desejar manter o mesmo nome após a conclusão da migração, execute as [etapas para renomear durante a migração][steps to rename during migration].</span><span class="sxs-lookup"><span data-stu-id="3a45b-184">If you want to keep the same name after migration is complete, follow the [steps to rename during migration][steps to rename during migration].</span></span>

1. <span data-ttu-id="3a45b-185">[Pause][Pause] seu data warehouse.</span><span class="sxs-lookup"><span data-stu-id="3a45b-185">[Pause][Pause] your data warehouse.</span></span> <span data-ttu-id="3a45b-186">Isso leva a um backup automático.</span><span class="sxs-lookup"><span data-stu-id="3a45b-186">This takes an automatic backup.</span></span>
2. <span data-ttu-id="3a45b-187">[Restaure][Restore] usando o instantâneo mais recente.</span><span class="sxs-lookup"><span data-stu-id="3a45b-187">[Restore][Restore] from your most recent snapshot.</span></span>
3. <span data-ttu-id="3a45b-188">Exclua seu data warehouse existente do armazenamento standard.</span><span class="sxs-lookup"><span data-stu-id="3a45b-188">Delete your existing data warehouse on standard storage.</span></span> <span data-ttu-id="3a45b-189">**Se você não conseguir fazer isso, será cobrado pelos dois data warehouses.**</span><span class="sxs-lookup"><span data-stu-id="3a45b-189">**If you fail to do this step, you will be charged for both data warehouses.**</span></span>

> [!NOTE]
> <span data-ttu-id="3a45b-190">As configurações a seguir não são transferidas como parte da migração:</span><span class="sxs-lookup"><span data-stu-id="3a45b-190">The following settings do not carry over as part of the migration:</span></span>
>
> * <span data-ttu-id="3a45b-191">A auditoria no nível do banco de dados precisa ser habilitada novamente.</span><span class="sxs-lookup"><span data-stu-id="3a45b-191">Auditing at the database level needs to be re-enabled.</span></span>
> * <span data-ttu-id="3a45b-192">As regras de firewall no nível do banco de dados precisam ser adicionadas novamente.</span><span class="sxs-lookup"><span data-stu-id="3a45b-192">Firewall rules at the database level need to be re-added.</span></span> <span data-ttu-id="3a45b-193">As regras de firewall no nível do servidor não deverão ser afetadas.</span><span class="sxs-lookup"><span data-stu-id="3a45b-193">Firewall rules at the server level are not affected.</span></span>
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a><span data-ttu-id="3a45b-194">Renomear o data warehouse durante a migração (opcional)</span><span class="sxs-lookup"><span data-stu-id="3a45b-194">Rename data warehouse during migration (optional)</span></span>
<span data-ttu-id="3a45b-195">Dois bancos de dados no mesmo servidor lógico não podem ter o mesmo nome.</span><span class="sxs-lookup"><span data-stu-id="3a45b-195">Two databases on the same logical server cannot have the same name.</span></span> <span data-ttu-id="3a45b-196">O SQL Data Warehouse agora dá suporte para a capacidade de renomear um data warehouse.</span><span class="sxs-lookup"><span data-stu-id="3a45b-196">SQL Data Warehouse now supports the ability to rename a data warehouse.</span></span>

<span data-ttu-id="3a45b-197">Neste exemplo, imagine que o data warehouse existente no armazenamento standard é chamado atualmente de "MyDW".</span><span class="sxs-lookup"><span data-stu-id="3a45b-197">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="3a45b-198">Renomeie "MyDW" usando o seguinte comando ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="3a45b-198">Rename "MyDW" by using the following ALTER DATABASE command.</span></span> <span data-ttu-id="3a45b-199">(Neste exemplo, o renomearemos como "MyDW_BeforeMigration".) Esse comando interrompe todas as transações existentes e deve ser feito no banco de dados mestre para ter êxito.</span><span class="sxs-lookup"><span data-stu-id="3a45b-199">(In this example, we'll rename it "MyDW_BeforeMigration.")  This command stops all existing transactions, and must be done in the master database to succeed.</span></span>
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. <span data-ttu-id="3a45b-200">[Pause][Pause] "MyDW_BeforeMigration."</span><span class="sxs-lookup"><span data-stu-id="3a45b-200">[Pause][Pause] "MyDW_BeforeMigration."</span></span> <span data-ttu-id="3a45b-201">Isso leva a um backup automático.</span><span class="sxs-lookup"><span data-stu-id="3a45b-201">This takes an automatic backup.</span></span>
3. <span data-ttu-id="3a45b-202">[Restaure][Restore], usando o instantâneo mais recente, um novo banco de dados com o nome antigo (por exemplo, “MyDW”).</span><span class="sxs-lookup"><span data-stu-id="3a45b-202">[Restore][Restore] from your most recent snapshot a new database with the name it used to be (for example, "MyDW").</span></span>
4. <span data-ttu-id="3a45b-203">Exclua "MyDW_BeforeMigration".</span><span class="sxs-lookup"><span data-stu-id="3a45b-203">Delete "MyDW_BeforeMigration."</span></span> <span data-ttu-id="3a45b-204">**Se você não conseguir fazer isso, será cobrado pelos dois data warehouses.**</span><span class="sxs-lookup"><span data-stu-id="3a45b-204">**If you fail to do this step, you will be charged for both data warehouses.**</span></span>


## <a name="next-steps"></a><span data-ttu-id="3a45b-205">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3a45b-205">Next steps</span></span>
<span data-ttu-id="3a45b-206">Com a alteração para o armazenamento premium, também aumentamos o número de arquivos de blob do banco de dados na arquitetura subjacente do seu data warehouse.</span><span class="sxs-lookup"><span data-stu-id="3a45b-206">With the change to premium storage, you also have an increased number of database blob files in the underlying architecture of your data warehouse.</span></span> <span data-ttu-id="3a45b-207">Para maximizar os benefícios de desempenho dessa mudança, recompile seus índices columnstore clusterizados usando o script a seguir.</span><span class="sxs-lookup"><span data-stu-id="3a45b-207">To maximize the performance benefits of this change, rebuild your clustered columnstore indexes by using the following script.</span></span> <span data-ttu-id="3a45b-208">O script funciona forçando alguns dos seus dados existentes para os blobs adicionais.</span><span class="sxs-lookup"><span data-stu-id="3a45b-208">The script works by forcing some of your existing data to the additional blobs.</span></span> <span data-ttu-id="3a45b-209">Se você não tomar nenhuma ação, os dados serão redistribuídos naturalmente com o tempo, conforme você carregar mais dados nas tabelas.</span><span class="sxs-lookup"><span data-stu-id="3a45b-209">If you take no action, the data will naturally redistribute over time as you load more data into your tables.</span></span>

<span data-ttu-id="3a45b-210">**Pré-requisitos:**</span><span class="sxs-lookup"><span data-stu-id="3a45b-210">**Prerequisites:**</span></span>

- <span data-ttu-id="3a45b-211">O data warehouse deve ser executado com 1.000 unidades de data warehouse ou mais (consulte [capacidade de computação de escala][scale compute power]).</span><span class="sxs-lookup"><span data-stu-id="3a45b-211">The data warehouse should run with 1,000 data warehouse units or higher (see [scale compute power][scale compute power]).</span></span>
- <span data-ttu-id="3a45b-212">O usuário que executa o script deve estar na [função mediumrc][mediumrc role] ou superior.</span><span class="sxs-lookup"><span data-stu-id="3a45b-212">The user executing the script should be in the [mediumrc role][mediumrc role] or higher.</span></span> <span data-ttu-id="3a45b-213">Para adicionar um usuário a essa função, execute o seguinte: ````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span><span class="sxs-lookup"><span data-stu-id="3a45b-213">To add a user to this role, execute the following: ````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span></span>

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table to control index rebuild
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------
create table sql_statements
WITH (distribution = round_robin)
as select
    'alter index all on ' + s.name + '.' + t.NAME + ' rebuild;' as statement,
    row_number() over (order by s.name, t.name) as sequence
from
    sys.schemas s
    inner join sys.tables t
        on s.schema_id = t.schema_id
where
    is_external = 0
;
go

--------------------------------------------------------------------------------
-- Step 2: Execute index rebuilds. If script fails, the below can be re-run to restart where last left off.
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------

declare @nbr_statements int = (select count(*) from sql_statements)
declare @i int = 1
while(@i <= @nbr_statements)
begin
      declare @statement nvarchar(1000)= (select statement from sql_statements where sequence = @i)
      print cast(getdate() as nvarchar(1000)) + ' Executing... ' + @statement
      exec (@statement)
      delete from sql_statements where sequence = @i
      set @i += 1
end;
go
-------------------------------------------------------------------------------
-- Step 3: Clean up table created in Step 1
--------------------------------------------------------------------------------
drop table sql_statements;
go
````

<span data-ttu-id="3a45b-214">Se você tiver algum problema com o data warehouse, [crie um tíquete de suporte][create a support ticket] e faça referência à “migração para o armazenamento premium” como a possível causa.</span><span class="sxs-lookup"><span data-stu-id="3a45b-214">If you encounter any issues with your data warehouse, [create a support ticket][create a support ticket] and reference “migration to premium storage” as the possible cause.</span></span>

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration to Premium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps to rename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com
