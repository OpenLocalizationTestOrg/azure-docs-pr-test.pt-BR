---
title: "aaaMigrate toopremium armazenamento de depósito de dados existentes do Azure | Microsoft Docs"
description: "Instruções para migrar um armazenamento toopremium existente do data warehouse"
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
ms.openlocfilehash: 145199c2da1f6f1fb8898626cd04886c42d82204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data-warehouse-toopremium-storage"></a><span data-ttu-id="7f292-103">Migrar o armazenamento do data warehouse toopremium</span><span class="sxs-lookup"><span data-stu-id="7f292-103">Migrate your data warehouse toopremium storage</span></span>
<span data-ttu-id="7f292-104">Recentemente, o Azure SQL Data Warehouse apresentou o [Armazenamento premium para maior previsibilidade de desempenho][premium storage for greater performance predictability].</span><span class="sxs-lookup"><span data-stu-id="7f292-104">Azure SQL Data Warehouse recently introduced [premium storage for greater performance predictability][premium storage for greater performance predictability].</span></span> <span data-ttu-id="7f292-105">Os dados existentes warehouses atualmente no armazenamento padrão podem ser migrados toopremium armazenamento.</span><span class="sxs-lookup"><span data-stu-id="7f292-105">Existing data warehouses currently on standard storage can now be migrated toopremium storage.</span></span> <span data-ttu-id="7f292-106">Você pode tirar proveito da migração automática, ou se você preferir toocontrol quando toomigrate (que envolvem algum tempo de inatividade), você pode fazer Olá a migração.</span><span class="sxs-lookup"><span data-stu-id="7f292-106">You can take advantage of automatic migration, or if you prefer toocontrol when toomigrate (which does involve some downtime), you can do hello migration yourself.</span></span>

<span data-ttu-id="7f292-107">Se você tiver mais de um data warehouse, use Olá [agenda a migração automática] [ automatic migration schedule] toodetermine quando ele também será migrado.</span><span class="sxs-lookup"><span data-stu-id="7f292-107">If you have more than one data warehouse, use hello [automatic migration schedule][automatic migration schedule] toodetermine when it will also be migrated.</span></span>

## <a name="determine-storage-type"></a><span data-ttu-id="7f292-108">Determinar o tipo de armazenamento</span><span class="sxs-lookup"><span data-stu-id="7f292-108">Determine storage type</span></span>
<span data-ttu-id="7f292-109">Se você tiver criado um data warehouse antes de saudação datas a seguir, você está usando atualmente o armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="7f292-109">If you created a data warehouse before hello following dates, you are currently using standard storage.</span></span>

| <span data-ttu-id="7f292-110">**Região**</span><span class="sxs-lookup"><span data-stu-id="7f292-110">**Region**</span></span> | <span data-ttu-id="7f292-111">**Data warehouse criado antes desta data**</span><span class="sxs-lookup"><span data-stu-id="7f292-111">**Data warehouse created before this date**</span></span> |
|:--- |:--- |
| <span data-ttu-id="7f292-112">Leste da Austrália</span><span class="sxs-lookup"><span data-stu-id="7f292-112">Australia East</span></span> |<span data-ttu-id="7f292-113">Armazenamento premium ainda não disponível</span><span class="sxs-lookup"><span data-stu-id="7f292-113">Premium storage not yet available</span></span> |
| <span data-ttu-id="7f292-114">Leste da China</span><span class="sxs-lookup"><span data-stu-id="7f292-114">China East</span></span> |<span data-ttu-id="7f292-115">1º de novembro de 2016</span><span class="sxs-lookup"><span data-stu-id="7f292-115">November 1, 2016</span></span> |
| <span data-ttu-id="7f292-116">Norte da China</span><span class="sxs-lookup"><span data-stu-id="7f292-116">China North</span></span> |<span data-ttu-id="7f292-117">1º de novembro de 2016</span><span class="sxs-lookup"><span data-stu-id="7f292-117">November 1, 2016</span></span> |
| <span data-ttu-id="7f292-118">Alemanha Central</span><span class="sxs-lookup"><span data-stu-id="7f292-118">Germany Central</span></span> |<span data-ttu-id="7f292-119">1º de novembro de 2016</span><span class="sxs-lookup"><span data-stu-id="7f292-119">November 1, 2016</span></span> |
| <span data-ttu-id="7f292-120">Nordeste da Alemanha</span><span class="sxs-lookup"><span data-stu-id="7f292-120">Germany Northeast</span></span> |<span data-ttu-id="7f292-121">1º de novembro de 2016</span><span class="sxs-lookup"><span data-stu-id="7f292-121">November 1, 2016</span></span> |
| <span data-ttu-id="7f292-122">Oeste da Índia</span><span class="sxs-lookup"><span data-stu-id="7f292-122">India West</span></span> |<span data-ttu-id="7f292-123">Armazenamento premium ainda não disponível</span><span class="sxs-lookup"><span data-stu-id="7f292-123">Premium storage not yet available</span></span> |
| <span data-ttu-id="7f292-124">Oeste do Japão</span><span class="sxs-lookup"><span data-stu-id="7f292-124">Japan West</span></span> |<span data-ttu-id="7f292-125">Armazenamento premium ainda não disponível</span><span class="sxs-lookup"><span data-stu-id="7f292-125">Premium storage not yet available</span></span> |
| <span data-ttu-id="7f292-126">Centro-Norte dos EUA</span><span class="sxs-lookup"><span data-stu-id="7f292-126">North Central US</span></span> |<span data-ttu-id="7f292-127">10 de novembro de 2016</span><span class="sxs-lookup"><span data-stu-id="7f292-127">November 10, 2016</span></span> |

## <a name="automatic-migration-details"></a><span data-ttu-id="7f292-128">Detalhes da migração automática</span><span class="sxs-lookup"><span data-stu-id="7f292-128">Automatic migration details</span></span>
<span data-ttu-id="7f292-129">Por padrão, irá migrar seu banco de dados para que você entre 6:00 e às 6:00 AM na hora local, da região durante a saudação [agenda a migração automática][automatic migration schedule].</span><span class="sxs-lookup"><span data-stu-id="7f292-129">By default, we will migrate your database for you between 6:00 PM and 6:00 AM in your region's local time during hello [automatic migration schedule][automatic migration schedule].</span></span> <span data-ttu-id="7f292-130">O data warehouse existente será inutilizável durante a migração de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f292-130">Your existing data warehouse will be unusable during hello migration.</span></span> <span data-ttu-id="7f292-131">migração de saudação levará aproximadamente uma hora por terabyte de armazenamento por depósito de dados.</span><span class="sxs-lookup"><span data-stu-id="7f292-131">hello migration will take approximately one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="7f292-132">Você não será cobrado durante qualquer parte da migração automática de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f292-132">You will not be charged during any portion of hello automatic migration.</span></span>

> [!NOTE]
> <span data-ttu-id="7f292-133">Quando a saudação migração for concluída, o data warehouse será novamente online e utilizável.</span><span class="sxs-lookup"><span data-stu-id="7f292-133">When hello migration is complete, your data warehouse will be back online and usable.</span></span>
>
>

<span data-ttu-id="7f292-134">Microsoft está demorando Olá após a migração de saudação toocomplete etapas (eles não exigem qualquer envolvimento de sua parte).</span><span class="sxs-lookup"><span data-stu-id="7f292-134">Microsoft is taking hello following steps toocomplete hello migration (these do not require any involvement on your part).</span></span> <span data-ttu-id="7f292-135">Neste exemplo, imagine que o data warehouse existente no armazenamento standard é chamado atualmente de "MyDW".</span><span class="sxs-lookup"><span data-stu-id="7f292-135">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="7f292-136">Microsoft renomeia "MyDW" muito "MyDW_DO_NOT_USE_ [Timestamp]".</span><span class="sxs-lookup"><span data-stu-id="7f292-136">Microsoft renames “MyDW” too“MyDW_DO_NOT_USE_[Timestamp].”</span></span>
2. <span data-ttu-id="7f292-137">A Microsoft pausa o “MyDW_DO_NOT_USE_[carimbo de data/hora]”.</span><span class="sxs-lookup"><span data-stu-id="7f292-137">Microsoft pauses “MyDW_DO_NOT_USE_[Timestamp].”</span></span> <span data-ttu-id="7f292-138">Durante esse tempo, um backup é feito.</span><span class="sxs-lookup"><span data-stu-id="7f292-138">During this time, a backup is taken.</span></span> <span data-ttu-id="7f292-139">Você poderá ver várias pausas e retomadas se encontrarmos problemas durante o processo.</span><span class="sxs-lookup"><span data-stu-id="7f292-139">You may see multiple pauses and resumes if we encounter any issues during this process.</span></span>
3. <span data-ttu-id="7f292-140">Microsoft cria um novo data warehouse denominado "MyDW" no armazenamento premium do backup Olá feito na etapa 2.</span><span class="sxs-lookup"><span data-stu-id="7f292-140">Microsoft creates a new data warehouse named “MyDW” on premium storage from hello backup taken in step 2.</span></span> <span data-ttu-id="7f292-141">"MyDW" não será exibido até após a conclusão da restauração de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f292-141">“MyDW” will not appear until after hello restore is complete.</span></span>
4. <span data-ttu-id="7f292-142">Após a conclusão da restauração hello, "MyDW" retorna toohello mesmo data warehouse unidades e estado (em pausa ou ativa) que estava antes da migração de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f292-142">After hello restore is complete, “MyDW” returns toohello same data warehouse units and state (paused or active) that it was before hello migration.</span></span>
5. <span data-ttu-id="7f292-143">Após a conclusão da migração hello, a Microsoft exclui "MyDW_DO_NOT_USE_ [Timestamp]".</span><span class="sxs-lookup"><span data-stu-id="7f292-143">After hello migration is complete, Microsoft deletes “MyDW_DO_NOT_USE_[Timestamp]”.</span></span>

> [!NOTE]
> <span data-ttu-id="7f292-144">Olá configurações a seguir não serão transferidos como parte da migração de saudação:</span><span class="sxs-lookup"><span data-stu-id="7f292-144">hello following settings do not carry over as part of hello migration:</span></span>
>
> * <span data-ttu-id="7f292-145">Auditoria no nível de banco de dados de saudação precisa toobe habilitada novamente.</span><span class="sxs-lookup"><span data-stu-id="7f292-145">Auditing at hello database level needs toobe re-enabled.</span></span>
> * <span data-ttu-id="7f292-146">Regras de firewall no nível de banco de dados de saudação necessário toobe adicionado novamente.</span><span class="sxs-lookup"><span data-stu-id="7f292-146">Firewall rules at hello database level need toobe re-added.</span></span> <span data-ttu-id="7f292-147">Regras de firewall no nível do servidor de saudação não são afetadas.</span><span class="sxs-lookup"><span data-stu-id="7f292-147">Firewall rules at hello server level are not affected.</span></span>
>
>

### <a name="automatic-migration-schedule"></a><span data-ttu-id="7f292-148">cronograma de migração automática</span><span class="sxs-lookup"><span data-stu-id="7f292-148">Automatic migration schedule</span></span>
<span data-ttu-id="7f292-149">As migrações automáticas ocorrerem entre 6:00 e às 6:00 AM (hora local por região) durante a saudação agenda de interrupção a seguir.</span><span class="sxs-lookup"><span data-stu-id="7f292-149">Automatic migrations occur between 6:00 PM and 6:00 AM (local time per region) during hello following outage schedule.</span></span>

| <span data-ttu-id="7f292-150">**Região**</span><span class="sxs-lookup"><span data-stu-id="7f292-150">**Region**</span></span> | <span data-ttu-id="7f292-151">**Data de início estimada**</span><span class="sxs-lookup"><span data-stu-id="7f292-151">**Estimated start date**</span></span> | <span data-ttu-id="7f292-152">**Data de término estimada**</span><span class="sxs-lookup"><span data-stu-id="7f292-152">**Estimated end date**</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7f292-153">Leste da Austrália</span><span class="sxs-lookup"><span data-stu-id="7f292-153">Australia East</span></span> |<span data-ttu-id="7f292-154">Ainda não foi determinado</span><span class="sxs-lookup"><span data-stu-id="7f292-154">Not determined yet</span></span> |<span data-ttu-id="7f292-155">Ainda não foi determinado</span><span class="sxs-lookup"><span data-stu-id="7f292-155">Not determined yet</span></span> |
| <span data-ttu-id="7f292-156">Leste da China</span><span class="sxs-lookup"><span data-stu-id="7f292-156">China East</span></span> |<span data-ttu-id="7f292-157">9 de janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="7f292-157">January 9, 2017</span></span> |<span data-ttu-id="7f292-158">13 de janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="7f292-158">January 13, 2017</span></span> |
| <span data-ttu-id="7f292-159">Norte da China</span><span class="sxs-lookup"><span data-stu-id="7f292-159">China North</span></span> |<span data-ttu-id="7f292-160">9 de janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="7f292-160">January 9, 2017</span></span> |<span data-ttu-id="7f292-161">13 de janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="7f292-161">January 13, 2017</span></span> |
| <span data-ttu-id="7f292-162">Alemanha Central</span><span class="sxs-lookup"><span data-stu-id="7f292-162">Germany Central</span></span> |<span data-ttu-id="7f292-163">9 de janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="7f292-163">January 9, 2017</span></span> |<span data-ttu-id="7f292-164">13 de janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="7f292-164">January 13, 2017</span></span> |
| <span data-ttu-id="7f292-165">Nordeste da Alemanha</span><span class="sxs-lookup"><span data-stu-id="7f292-165">Germany Northeast</span></span> |<span data-ttu-id="7f292-166">9 de janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="7f292-166">January 9, 2017</span></span> |<span data-ttu-id="7f292-167">13 de janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="7f292-167">January 13, 2017</span></span> |
| <span data-ttu-id="7f292-168">Oeste da Índia</span><span class="sxs-lookup"><span data-stu-id="7f292-168">India West</span></span> |<span data-ttu-id="7f292-169">Ainda não foi determinado</span><span class="sxs-lookup"><span data-stu-id="7f292-169">Not determined yet</span></span> |<span data-ttu-id="7f292-170">Ainda não foi determinado</span><span class="sxs-lookup"><span data-stu-id="7f292-170">Not determined yet</span></span> |
| <span data-ttu-id="7f292-171">Oeste do Japão</span><span class="sxs-lookup"><span data-stu-id="7f292-171">Japan West</span></span> |<span data-ttu-id="7f292-172">Ainda não foi determinado</span><span class="sxs-lookup"><span data-stu-id="7f292-172">Not determined yet</span></span> |<span data-ttu-id="7f292-173">Ainda não foi determinado</span><span class="sxs-lookup"><span data-stu-id="7f292-173">Not determined yet</span></span> |
| <span data-ttu-id="7f292-174">Centro-Norte dos EUA</span><span class="sxs-lookup"><span data-stu-id="7f292-174">North Central US</span></span> |<span data-ttu-id="7f292-175">9 de janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="7f292-175">January 9, 2017</span></span> |<span data-ttu-id="7f292-176">13 de janeiro de 2017</span><span class="sxs-lookup"><span data-stu-id="7f292-176">January 13, 2017</span></span> |

## <a name="self-migration-toopremium-storage"></a><span data-ttu-id="7f292-177">Armazenamento de toopremium migração Self</span><span class="sxs-lookup"><span data-stu-id="7f292-177">Self-migration toopremium storage</span></span>
<span data-ttu-id="7f292-178">Se você quiser toocontrol quando o tempo de inatividade, você pode usar o hello seguindo as etapas toomigrate um data warehouse existente no armazenamento de toopremium de armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="7f292-178">If you want toocontrol when your downtime will occur, you can use hello following steps toomigrate an existing data warehouse on standard storage toopremium storage.</span></span> <span data-ttu-id="7f292-179">Se você escolher essa opção, você deve concluir a migração de Self Olá antes de começa a migração automática de saudação nessa região.</span><span class="sxs-lookup"><span data-stu-id="7f292-179">If you choose this option, you must complete hello self-migration before hello automatic migration begins in that region.</span></span> <span data-ttu-id="7f292-180">Isso garante que você evite qualquer risco de migração automática Olá, causando um conflito (consulte toohello [agenda a migração automática][automatic migration schedule]).</span><span class="sxs-lookup"><span data-stu-id="7f292-180">This ensures that you avoid any risk of hello automatic migration causing a conflict (refer toohello [automatic migration schedule][automatic migration schedule]).</span></span>

### <a name="self-migration-instructions"></a><span data-ttu-id="7f292-181">Instruções de automigração</span><span class="sxs-lookup"><span data-stu-id="7f292-181">Self-migration instructions</span></span>
<span data-ttu-id="7f292-182">toomigrate seus dados do data warehouse por conta própria, usam Olá backup e restauração recursos.</span><span class="sxs-lookup"><span data-stu-id="7f292-182">toomigrate your data warehouse yourself, use hello backup and restore features.</span></span> <span data-ttu-id="7f292-183">parte de restauração de saudação de migração de saudação é esperado tootake cerca de uma hora por terabyte de armazenamento por do data warehouse.</span><span class="sxs-lookup"><span data-stu-id="7f292-183">hello restore portion of hello migration is expected tootake around one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="7f292-184">Se você quiser Olá tookeep mesmo nome após a conclusão da migração, siga Olá [toorename etapas durante a migração][steps toorename during migration].</span><span class="sxs-lookup"><span data-stu-id="7f292-184">If you want tookeep hello same name after migration is complete, follow hello [steps toorename during migration][steps toorename during migration].</span></span>

1. <span data-ttu-id="7f292-185">[Pause][Pause] seu data warehouse.</span><span class="sxs-lookup"><span data-stu-id="7f292-185">[Pause][Pause] your data warehouse.</span></span> <span data-ttu-id="7f292-186">Isso leva a um backup automático.</span><span class="sxs-lookup"><span data-stu-id="7f292-186">This takes an automatic backup.</span></span>
2. <span data-ttu-id="7f292-187">[Restaure][Restore] usando o instantâneo mais recente.</span><span class="sxs-lookup"><span data-stu-id="7f292-187">[Restore][Restore] from your most recent snapshot.</span></span>
3. <span data-ttu-id="7f292-188">Exclua seu data warehouse existente do armazenamento standard.</span><span class="sxs-lookup"><span data-stu-id="7f292-188">Delete your existing data warehouse on standard storage.</span></span> <span data-ttu-id="7f292-189">**Se você não toodo esta etapa, você será cobrado para ambos os data warehouses.**</span><span class="sxs-lookup"><span data-stu-id="7f292-189">**If you fail toodo this step, you will be charged for both data warehouses.**</span></span>

> [!NOTE]
> <span data-ttu-id="7f292-190">Olá configurações a seguir não serão transferidos como parte da migração de saudação:</span><span class="sxs-lookup"><span data-stu-id="7f292-190">hello following settings do not carry over as part of hello migration:</span></span>
>
> * <span data-ttu-id="7f292-191">Auditoria no nível de banco de dados de saudação precisa toobe habilitada novamente.</span><span class="sxs-lookup"><span data-stu-id="7f292-191">Auditing at hello database level needs toobe re-enabled.</span></span>
> * <span data-ttu-id="7f292-192">Regras de firewall no nível de banco de dados de saudação necessário toobe adicionado novamente.</span><span class="sxs-lookup"><span data-stu-id="7f292-192">Firewall rules at hello database level need toobe re-added.</span></span> <span data-ttu-id="7f292-193">Regras de firewall no nível do servidor de saudação não são afetadas.</span><span class="sxs-lookup"><span data-stu-id="7f292-193">Firewall rules at hello server level are not affected.</span></span>
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a><span data-ttu-id="7f292-194">Renomear o data warehouse durante a migração (opcional)</span><span class="sxs-lookup"><span data-stu-id="7f292-194">Rename data warehouse during migration (optional)</span></span>
<span data-ttu-id="7f292-195">Dois bancos de dados no mesmo servidor lógico não pode ter de saudação Olá o mesmo nome.</span><span class="sxs-lookup"><span data-stu-id="7f292-195">Two databases on hello same logical server cannot have hello same name.</span></span> <span data-ttu-id="7f292-196">SQL Data Warehouse agora dá suporte a capacidade de saudação toorename um data warehouse.</span><span class="sxs-lookup"><span data-stu-id="7f292-196">SQL Data Warehouse now supports hello ability toorename a data warehouse.</span></span>

<span data-ttu-id="7f292-197">Neste exemplo, imagine que o data warehouse existente no armazenamento standard é chamado atualmente de "MyDW".</span><span class="sxs-lookup"><span data-stu-id="7f292-197">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="7f292-198">Renomear "MyDW" usando Olá após o comando ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="7f292-198">Rename "MyDW" by using hello following ALTER DATABASE command.</span></span> <span data-ttu-id="7f292-199">(Neste exemplo, iremos renomeá-lo "MyDW_BeforeMigration.")  Esse comando interrompe todas as transações existentes e deve ser feito em Olá toosucceed de banco de dados mestre.</span><span class="sxs-lookup"><span data-stu-id="7f292-199">(In this example, we'll rename it "MyDW_BeforeMigration.")  This command stops all existing transactions, and must be done in hello master database toosucceed.</span></span>
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. <span data-ttu-id="7f292-200">[Pause][Pause] "MyDW_BeforeMigration."</span><span class="sxs-lookup"><span data-stu-id="7f292-200">[Pause][Pause] "MyDW_BeforeMigration."</span></span> <span data-ttu-id="7f292-201">Isso leva a um backup automático.</span><span class="sxs-lookup"><span data-stu-id="7f292-201">This takes an automatic backup.</span></span>
3. <span data-ttu-id="7f292-202">[Restaurar] [ Restore] do seu instantâneo mais recente, um novo banco de dados com o nome da saudação era toobe (por exemplo, "MyDW").</span><span class="sxs-lookup"><span data-stu-id="7f292-202">[Restore][Restore] from your most recent snapshot a new database with hello name it used toobe (for example, "MyDW").</span></span>
4. <span data-ttu-id="7f292-203">Exclua "MyDW_BeforeMigration".</span><span class="sxs-lookup"><span data-stu-id="7f292-203">Delete "MyDW_BeforeMigration."</span></span> <span data-ttu-id="7f292-204">**Se você não toodo esta etapa, você será cobrado para ambos os data warehouses.**</span><span class="sxs-lookup"><span data-stu-id="7f292-204">**If you fail toodo this step, you will be charged for both data warehouses.**</span></span>


## <a name="next-steps"></a><span data-ttu-id="7f292-205">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7f292-205">Next steps</span></span>
<span data-ttu-id="7f292-206">Olá alterar toopremium armazenamento, você também tem um número maior de arquivos do banco de dados blob na arquitetura subjacente de saudação do data warehouse.</span><span class="sxs-lookup"><span data-stu-id="7f292-206">With hello change toopremium storage, you also have an increased number of database blob files in hello underlying architecture of your data warehouse.</span></span> <span data-ttu-id="7f292-207">benefícios de desempenho de saudação toomaximize dessa alteração, reconstrua os índices columnstore clusterizados usando Olá script a seguir.</span><span class="sxs-lookup"><span data-stu-id="7f292-207">toomaximize hello performance benefits of this change, rebuild your clustered columnstore indexes by using hello following script.</span></span> <span data-ttu-id="7f292-208">script Hello funciona, forçando a alguns dos seus existente blobs de dados toohello adicionais.</span><span class="sxs-lookup"><span data-stu-id="7f292-208">hello script works by forcing some of your existing data toohello additional blobs.</span></span> <span data-ttu-id="7f292-209">Se você não executar nenhuma ação, dados saudação naturalmente serão redistribuir ao longo do tempo conforme você carregar mais dados em tabelas.</span><span class="sxs-lookup"><span data-stu-id="7f292-209">If you take no action, hello data will naturally redistribute over time as you load more data into your tables.</span></span>

<span data-ttu-id="7f292-210">**Pré-requisitos:**</span><span class="sxs-lookup"><span data-stu-id="7f292-210">**Prerequisites:**</span></span>

- <span data-ttu-id="7f292-211">Olá depósito de dados deve ser executado com unidades de depósito de 1.000 dados ou mais recente (consulte [capacidade de computação de escala][scale compute power]).</span><span class="sxs-lookup"><span data-stu-id="7f292-211">hello data warehouse should run with 1,000 data warehouse units or higher (see [scale compute power][scale compute power]).</span></span>
- <span data-ttu-id="7f292-212">Olá usuário executando o script hello deve estar no hello [mediumrc função] [ mediumrc role] ou superior.</span><span class="sxs-lookup"><span data-stu-id="7f292-212">hello user executing hello script should be in hello [mediumrc role][mediumrc role] or higher.</span></span> <span data-ttu-id="7f292-213">tooadd uma função do usuário toothis, execute o seguinte hello:````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span><span class="sxs-lookup"><span data-stu-id="7f292-213">tooadd a user toothis role, execute hello following: ````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span></span>

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table toocontrol index rebuild
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
-- Step 2: Execute index rebuilds. If script fails, hello below can be re-run toorestart where last left off.
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

<span data-ttu-id="7f292-214">Se você encontrar algum problema com o data warehouse, [criar um tíquete de suporte] [ create a support ticket] e fazer referência a "toopremium de armazenamento de migração" como causa possível hello.</span><span class="sxs-lookup"><span data-stu-id="7f292-214">If you encounter any issues with your data warehouse, [create a support ticket][create a support ticket] and reference “migration toopremium storage” as hello possible cause.</span></span>

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration tooPremium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps toorename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com
