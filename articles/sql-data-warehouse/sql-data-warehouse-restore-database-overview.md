---
title: "aaaRestore um depósito de dados do Azure - local e com redundância geográfica | Microsoft Docs"
description: "Visão geral das opções de restauração de banco de dados de saudação para recuperar um banco de dados no Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: 3e01c65c-6708-4fd7-82f5-4e1b5f61d304
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: a96b898372b29d420e1416ca93a172ff8af47fc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-restore"></a><span data-ttu-id="838be-103">Restauração do SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="838be-103">SQL Data Warehouse restore</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="838be-104">[Visão geral][Overview]</span><span class="sxs-lookup"><span data-stu-id="838be-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="838be-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="838be-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="838be-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="838be-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="838be-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="838be-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="838be-108">O SQL Data Warehouse oferece restaurações locais e geográficas como parte de suas funcionalidades de recuperação de desastre de warehouse.</span><span class="sxs-lookup"><span data-stu-id="838be-108">SQL Data Warehouse offers both local and geographical restores as part of its data warehouse disaster recovery capabilities.</span></span> <span data-ttu-id="838be-109">Use o data warehouse backups toorestore sua restauração do data warehouse tooa ponto na região primária hello, ou usar backups com redundância geográfica toorestore tooa região geográfica diferente.</span><span class="sxs-lookup"><span data-stu-id="838be-109">Use data warehouse backups toorestore your data warehouse tooa restore point in hello primary region, or use geo-redundant backups toorestore tooa different geographical region.</span></span> <span data-ttu-id="838be-110">Este artigo explica as especificações de saudação da restauração de um data warehouse.</span><span class="sxs-lookup"><span data-stu-id="838be-110">This article explains hello specifics of restoring a data warehouse.</span></span>

## <a name="what-is-a-data-warehouse-restore"></a><span data-ttu-id="838be-111">O que é uma restauração do data warehouse?</span><span class="sxs-lookup"><span data-stu-id="838be-111">What is a data warehouse restore?</span></span>
<span data-ttu-id="838be-112">A restauração de um data warehouse é um novo data warehouse criado por meio de um backup de um data warehouse existente ou excluído.</span><span class="sxs-lookup"><span data-stu-id="838be-112">A data warehouse restore is a new data warehouse that is created from a backup of an existing or deleted data warehouse.</span></span> <span data-ttu-id="838be-113">depósito de dados restaurados Olá recria Olá backup do data warehouse em um momento específico.</span><span class="sxs-lookup"><span data-stu-id="838be-113">hello restored data warehouse re-creates hello backed-up data warehouse at a specific time.</span></span> <span data-ttu-id="838be-114">Considerando que o SQL Data Warehouse é um sistema distribuído, uma restauração do data warehouse é criada por meio de muitos arquivos de backup armazenados em blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="838be-114">Since SQL Data Warehouse is a distributed system, a data warehouse restore is created from many backup files that are stored in Azure blobs.</span></span> 

<span data-ttu-id="838be-115">A restauração do banco de dados é uma parte essencial de qualquer estratégia de recuperação de desastre e de continuidade dos negócios, porque ela recria seus dados após uma exclusão ou corrupção acidental.</span><span class="sxs-lookup"><span data-stu-id="838be-115">Database restore is an essential part of any business continuity and disaster recovery strategy because it re-creates your data after accidental corruption or deletion.</span></span>

<span data-ttu-id="838be-116">Para obter mais informações, consulte:</span><span class="sxs-lookup"><span data-stu-id="838be-116">For more information, see:</span></span>

* [<span data-ttu-id="838be-117">Backups do SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="838be-117">SQL Data Warehouse backups</span></span>](sql-data-warehouse-backups.md)
* [<span data-ttu-id="838be-118">Visão geral da continuidade dos negócios</span><span class="sxs-lookup"><span data-stu-id="838be-118">Business continuity overview</span></span>](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a><span data-ttu-id="838be-119">Pontos de restauração do data warehouse</span><span class="sxs-lookup"><span data-stu-id="838be-119">Data warehouse restore points</span></span>
<span data-ttu-id="838be-120">Uma vantagem de usar o armazenamento Premium do Azure, SQL Data Warehouse usa depósito de dados primário do Blob de armazenamento do Azure instantâneos toobackup hello.</span><span class="sxs-lookup"><span data-stu-id="838be-120">As a benefit of using Azure Premium Storage, SQL Data Warehouse uses Azure Storage Blob snapshots toobackup hello primary data warehouse.</span></span> <span data-ttu-id="838be-121">Cada instantâneo tem um ponto de restauração que representa o tempo de saudação instantâneo Olá iniciado.</span><span class="sxs-lookup"><span data-stu-id="838be-121">Each snapshot has a restore point that represents hello time hello snapshot started.</span></span> <span data-ttu-id="838be-122">toorestore um data warehouse, escolha um ponto de restauração e emitir um comando de restauração.</span><span class="sxs-lookup"><span data-stu-id="838be-122">toorestore a data warehouse, you choose a restore point and issue a restore command.</span></span>  

<span data-ttu-id="838be-123">SQL Data Warehouse sempre restaura Olá tooa backup novo data warehouse.</span><span class="sxs-lookup"><span data-stu-id="838be-123">SQL Data Warehouse always restores hello backup tooa new data warehouse.</span></span> <span data-ttu-id="838be-124">Você pode manter depósito de dados restaurados hello e Olá atual ou excluir um deles.</span><span class="sxs-lookup"><span data-stu-id="838be-124">You can either keep hello restored data warehouse and hello current one, or delete one of them.</span></span> <span data-ttu-id="838be-125">Se você quiser tooreplace Olá atual do data warehouse com hello restaurado do data warehouse, você pode renomeá-la.</span><span class="sxs-lookup"><span data-stu-id="838be-125">If you want tooreplace hello current data warehouse with hello restored data warehouse, you can rename it.</span></span>

<span data-ttu-id="838be-126">Se você precisar toorestore um depósito de dados excluídos ou pausado, você pode [criar um tíquete de suporte](sql-data-warehouse-get-started-create-support-ticket.md).</span><span class="sxs-lookup"><span data-stu-id="838be-126">If you need toorestore a deleted or paused data warehouse, you can [create a support ticket](sql-data-warehouse-get-started-create-support-ticket.md).</span></span> 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore hello last available restore point.

Yes, for hello next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps hello data warehouse and its snapshots for seven days just in case you need hello data. After seven days, you won't be able toorestore tooany of hello restore points. -->

## <a name="geo-redundant-restore"></a><span data-ttu-id="838be-127">Restauração com redundância geográfica</span><span class="sxs-lookup"><span data-stu-id="838be-127">Geo-redundant restore</span></span>
<span data-ttu-id="838be-128">Você pode restaurar sua região de tooany de depósito de dados com suporte do Azure SQL Data Warehouse com o nível de desempenho escolhido.</span><span class="sxs-lookup"><span data-stu-id="838be-128">You can restore your data warehouse tooany region supporting Azure SQL Data Warehouse at your chosen performance level.</span></span> <span data-ttu-id="838be-129">Observe que DWU 9000 e 18000 não têm suporte em todas as regiões durante a visualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="838be-129">Please note that 9000 and 18000 DWU are not supported in all regions during hello preview.</span></span>

> [!NOTE]
> <span data-ttu-id="838be-130">restauração de tooperform uma redundância geográfica que você não deve ter desativado para este recurso.</span><span class="sxs-lookup"><span data-stu-id="838be-130">tooperform a geo-redundant restore you must not have opted out of this feature.</span></span>
> 
> 

## <a name="restore-timeline"></a><span data-ttu-id="838be-131">Restaurar linha do tempo</span><span class="sxs-lookup"><span data-stu-id="838be-131">Restore timeline</span></span>
<span data-ttu-id="838be-132">Você pode restaurar um banco de dados tooany ponto de restauração disponível dentro de saudação últimos sete dias.</span><span class="sxs-lookup"><span data-stu-id="838be-132">You can restore a database tooany available restore point within hello last seven days.</span></span> <span data-ttu-id="838be-133">Instantâneos de iniciar a cada quatro horas tooeight e estão disponíveis por sete dias.</span><span class="sxs-lookup"><span data-stu-id="838be-133">Snapshots start every four tooeight hours and are available for seven days.</span></span> <span data-ttu-id="838be-134">Quando um instantâneo possui mais de sete dias, ele expira e seu ponto de restauração fica indisponível.</span><span class="sxs-lookup"><span data-stu-id="838be-134">When a snapshot is older than seven days, it expires and its restore point is no longer available.</span></span>

## <a name="restore-costs"></a><span data-ttu-id="838be-135">Restaurar custos</span><span class="sxs-lookup"><span data-stu-id="838be-135">Restore costs</span></span>
<span data-ttu-id="838be-136">custos de armazenamento Olá para depósito de dados restaurados Olá é cobrado na taxa de armazenamento do Azure Premium Olá.</span><span class="sxs-lookup"><span data-stu-id="838be-136">hello storage charge for hello restored data warehouse is billed at hello Azure Premium Storage rate.</span></span> 

<span data-ttu-id="838be-137">Se você pausar um depósito de dados restaurado, você é cobrado para armazenamento a taxa de armazenamento do Azure Premium Olá.</span><span class="sxs-lookup"><span data-stu-id="838be-137">If you pause a restored data warehouse, you are charged for storage at hello Azure Premium Storage rate.</span></span> <span data-ttu-id="838be-138">Olá vantagem pausar é que não seja cobrado por recursos de computação de DWU hello.</span><span class="sxs-lookup"><span data-stu-id="838be-138">hello advantage of pausing is you are not charged for hello DWU computing resources.</span></span>

<span data-ttu-id="838be-139">Para obter mais informações sobre os preços do SQL Data Warehouse, consulte [Preços do SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="838be-139">For more information about SQL Data Warehouse pricing, see [SQL Data Warehouse Pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>

## <a name="uses-for-restore"></a><span data-ttu-id="838be-140">Usos para restauração</span><span class="sxs-lookup"><span data-stu-id="838be-140">Uses for restore</span></span>
<span data-ttu-id="838be-141">Olá principal uso do data warehouse restauração é toorecover dados após a perda acidental de dados ou à corrupção.</span><span class="sxs-lookup"><span data-stu-id="838be-141">hello primary use for data warehouse restore is toorecover data after accidental data loss or corruption.</span></span>

<span data-ttu-id="838be-142">Você também pode usar o data warehouse restauração tooretain um backup por mais de sete dias.</span><span class="sxs-lookup"><span data-stu-id="838be-142">You can also use data warehouse restore tooretain a backup for longer than seven days.</span></span> <span data-ttu-id="838be-143">Depois de saudação backup é restaurado, você data warehouse de saudação online e pode fazer uma pausa nela indefinidamente toosave custos de computação.</span><span class="sxs-lookup"><span data-stu-id="838be-143">Once hello backup is restored, you have hello data warehouse online and can pause it indefinitely toosave compute costs.</span></span> <span data-ttu-id="838be-144">banco de dados pausada Olá incorre em encargos de armazenamento a taxa de armazenamento do Azure Premium Olá.</span><span class="sxs-lookup"><span data-stu-id="838be-144">hello paused database incurs storage charges at hello Azure Premium Storage rate.</span></span> 

## <a name="related-topics"></a><span data-ttu-id="838be-145">Tópicos relacionados</span><span class="sxs-lookup"><span data-stu-id="838be-145">Related topics</span></span>
### <a name="scenarios"></a><span data-ttu-id="838be-146">Cenários</span><span class="sxs-lookup"><span data-stu-id="838be-146">Scenarios</span></span>
* <span data-ttu-id="838be-147">Para obter uma visão geral sobre a continuidade de negócios, veja [Visão geral da continuidade de negócios](../sql-database/sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="838be-147">For a business continuity overview, see [Business continuity overview](../sql-database/sql-database-business-continuity.md)</span></span>

<!-- ### Tasks -->

<span data-ttu-id="838be-148">tooperform um data warehouse de restauração, restaurar usando:</span><span class="sxs-lookup"><span data-stu-id="838be-148">tooperform a data warehouse restore, restore using:</span></span>

* <span data-ttu-id="838be-149">Azure portal, consulte [restaurar de um data warehouse usando Olá portal do Azure](sql-data-warehouse-restore-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="838be-149">Azure portal, see [Restore a data warehouse using hello Azure portal](sql-data-warehouse-restore-database-portal.md)</span></span>
* <span data-ttu-id="838be-150">Cmdlets do PowerShell, consulte [Restore a data warehouse using PowerShell cmdlets (Restaurar um data warehouse usando cmdlets do PowerShell)](sql-data-warehouse-restore-database-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="838be-150">PowerShell cmdlets, see [Restore a data warehouse using PowerShell cmdlets](sql-data-warehouse-restore-database-powershell.md)</span></span>
* <span data-ttu-id="838be-151">APIs REST, consulte [restaurar de um data warehouse usando Olá APIs REST](sql-data-warehouse-restore-database-rest-api.md)</span><span class="sxs-lookup"><span data-stu-id="838be-151">REST APIs, see [Restore a data warehouse using hello REST APIs](sql-data-warehouse-restore-database-rest-api.md)</span></span>

<!-- ### Tutorials -->

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->


<!--Other Web references-->
