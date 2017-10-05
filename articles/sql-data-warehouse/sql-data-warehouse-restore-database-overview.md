---
title: "Restaurar um Azure data warehouse - local e com redundância geográfica | Microsoft Docs"
description: "Visão geral das opções de restauração para recuperar um banco de dados no SQL Data Warehouse do Azure."
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
ms.openlocfilehash: ea42b7135d0695b66d569095e70bb3d9f8b9594b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="sql-data-warehouse-restore"></a><span data-ttu-id="53105-103">Restauração do SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="53105-103">SQL Data Warehouse restore</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="53105-104">[Visão geral][Overview]</span><span class="sxs-lookup"><span data-stu-id="53105-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="53105-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="53105-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="53105-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="53105-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="53105-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="53105-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="53105-108">O SQL Data Warehouse oferece restaurações locais e geográficas como parte de suas funcionalidades de recuperação de desastre de warehouse.</span><span class="sxs-lookup"><span data-stu-id="53105-108">SQL Data Warehouse offers both local and geographical restores as part of its data warehouse disaster recovery capabilities.</span></span> <span data-ttu-id="53105-109">Use backups de data warehouse para restaurar o data warehouse para um ponto de restauração na região primária ou usar backups com redundância geográfica para restaurá-lo para uma região geográfica diferente.</span><span class="sxs-lookup"><span data-stu-id="53105-109">Use data warehouse backups to restore your data warehouse to a restore point in the primary region, or use geo-redundant backups to restore to a different geographical region.</span></span> <span data-ttu-id="53105-110">Este artigo explica as especificidades de restaurar um data warehouse.</span><span class="sxs-lookup"><span data-stu-id="53105-110">This article explains the specifics of restoring a data warehouse.</span></span>

## <a name="what-is-a-data-warehouse-restore"></a><span data-ttu-id="53105-111">O que é uma restauração do data warehouse?</span><span class="sxs-lookup"><span data-stu-id="53105-111">What is a data warehouse restore?</span></span>
<span data-ttu-id="53105-112">A restauração de um data warehouse é um novo data warehouse criado por meio de um backup de um data warehouse existente ou excluído.</span><span class="sxs-lookup"><span data-stu-id="53105-112">A data warehouse restore is a new data warehouse that is created from a backup of an existing or deleted data warehouse.</span></span> <span data-ttu-id="53105-113">O data warehouse restaurado recria o data warehouse com backup realizado em um momento específico.</span><span class="sxs-lookup"><span data-stu-id="53105-113">The restored data warehouse re-creates the backed-up data warehouse at a specific time.</span></span> <span data-ttu-id="53105-114">Considerando que o SQL Data Warehouse é um sistema distribuído, uma restauração do data warehouse é criada por meio de muitos arquivos de backup armazenados em blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="53105-114">Since SQL Data Warehouse is a distributed system, a data warehouse restore is created from many backup files that are stored in Azure blobs.</span></span> 

<span data-ttu-id="53105-115">A restauração do banco de dados é uma parte essencial de qualquer estratégia de recuperação de desastre e de continuidade dos negócios, porque ela recria seus dados após uma exclusão ou corrupção acidental.</span><span class="sxs-lookup"><span data-stu-id="53105-115">Database restore is an essential part of any business continuity and disaster recovery strategy because it re-creates your data after accidental corruption or deletion.</span></span>

<span data-ttu-id="53105-116">Para obter mais informações, consulte:</span><span class="sxs-lookup"><span data-stu-id="53105-116">For more information, see:</span></span>

* [<span data-ttu-id="53105-117">Backups do SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="53105-117">SQL Data Warehouse backups</span></span>](sql-data-warehouse-backups.md)
* [<span data-ttu-id="53105-118">Visão geral da continuidade dos negócios</span><span class="sxs-lookup"><span data-stu-id="53105-118">Business continuity overview</span></span>](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a><span data-ttu-id="53105-119">Pontos de restauração do data warehouse</span><span class="sxs-lookup"><span data-stu-id="53105-119">Data warehouse restore points</span></span>
<span data-ttu-id="53105-120">Como um benefício do uso do Armazenamento Premium do Azure, o SQL Data Warehouse usa instantâneos do Azure Storage Blob para fazer backup do data warehouse primário.</span><span class="sxs-lookup"><span data-stu-id="53105-120">As a benefit of using Azure Premium Storage, SQL Data Warehouse uses Azure Storage Blob snapshots to backup the primary data warehouse.</span></span> <span data-ttu-id="53105-121">Cada instantâneo tem um ponto de restauração que representa a hora em que o instantâneo é iniciado.</span><span class="sxs-lookup"><span data-stu-id="53105-121">Each snapshot has a restore point that represents the time the snapshot started.</span></span> <span data-ttu-id="53105-122">Para restaurar um data warehouse, escolha um ponto de restauração e emita um comando de restauração.</span><span class="sxs-lookup"><span data-stu-id="53105-122">To restore a data warehouse, you choose a restore point and issue a restore command.</span></span>  

<span data-ttu-id="53105-123">O SQL Data Warehouse sempre restaura o backup para um novo data warehouse.</span><span class="sxs-lookup"><span data-stu-id="53105-123">SQL Data Warehouse always restores the backup to a new data warehouse.</span></span> <span data-ttu-id="53105-124">É possível manter o data warehouse restaurado e o atual ou excluir um deles.</span><span class="sxs-lookup"><span data-stu-id="53105-124">You can either keep the restored data warehouse and the current one, or delete one of them.</span></span> <span data-ttu-id="53105-125">Se você desejar substituir o data warehouse atual pelo data warehouse restaurado, poderá renomeá-lo.</span><span class="sxs-lookup"><span data-stu-id="53105-125">If you want to replace the current data warehouse with the restored data warehouse, you can rename it.</span></span>

<span data-ttu-id="53105-126">Se você precisar restaurar um data warehouse excluído ou em pausa, será possível [criar um tíquete de suporte](sql-data-warehouse-get-started-create-support-ticket.md).</span><span class="sxs-lookup"><span data-stu-id="53105-126">If you need to restore a deleted or paused data warehouse, you can [create a support ticket](sql-data-warehouse-get-started-create-support-ticket.md).</span></span> 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore the last available restore point.

Yes, for the next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps the data warehouse and its snapshots for seven days just in case you need the data. After seven days, you won't be able to restore to any of the restore points. -->

## <a name="geo-redundant-restore"></a><span data-ttu-id="53105-127">Restauração com redundância geográfica</span><span class="sxs-lookup"><span data-stu-id="53105-127">Geo-redundant restore</span></span>
<span data-ttu-id="53105-128">Você pode restaurar seu data warehouse para qualquer região com suporte do SQL Data Warehouse do Azure com o nível de desempenho escolhido.</span><span class="sxs-lookup"><span data-stu-id="53105-128">You can restore your data warehouse to any region supporting Azure SQL Data Warehouse at your chosen performance level.</span></span> <span data-ttu-id="53105-129">Observe que DWU 9000 e 18000 não têm suporte em todas as regiões durante a versão prévia.</span><span class="sxs-lookup"><span data-stu-id="53105-129">Please note that 9000 and 18000 DWU are not supported in all regions during the preview.</span></span>

> [!NOTE]
> <span data-ttu-id="53105-130">Para executar uma restauração com redundância geográfica, você não deve ter recusado esse recurso.</span><span class="sxs-lookup"><span data-stu-id="53105-130">To perform a geo-redundant restore you must not have opted out of this feature.</span></span>
> 
> 

## <a name="restore-timeline"></a><span data-ttu-id="53105-131">Restaurar linha do tempo</span><span class="sxs-lookup"><span data-stu-id="53105-131">Restore timeline</span></span>
<span data-ttu-id="53105-132">É possível restaurar um banco de dados para qualquer ponto de restauração disponível nos últimos sete dias.</span><span class="sxs-lookup"><span data-stu-id="53105-132">You can restore a database to any available restore point within the last seven days.</span></span> <span data-ttu-id="53105-133">Os instantâneos iniciam a cada 4-8 horas e permanecem disponíveis por sete dias.</span><span class="sxs-lookup"><span data-stu-id="53105-133">Snapshots start every four to eight hours and are available for seven days.</span></span> <span data-ttu-id="53105-134">Quando um instantâneo possui mais de sete dias, ele expira e seu ponto de restauração fica indisponível.</span><span class="sxs-lookup"><span data-stu-id="53105-134">When a snapshot is older than seven days, it expires and its restore point is no longer available.</span></span>

## <a name="restore-costs"></a><span data-ttu-id="53105-135">Restaurar custos</span><span class="sxs-lookup"><span data-stu-id="53105-135">Restore costs</span></span>
<span data-ttu-id="53105-136">O custo de armazenamento para o data warehouse restaurado é cobrado na taxa de Armazenamento Premium do Azure.</span><span class="sxs-lookup"><span data-stu-id="53105-136">The storage charge for the restored data warehouse is billed at the Azure Premium Storage rate.</span></span> 

<span data-ttu-id="53105-137">Caso você pause um data warehouse restaurado, você será cobrado pelo armazenamento com a taxa de Armazenamento Premium do Azure.</span><span class="sxs-lookup"><span data-stu-id="53105-137">If you pause a restored data warehouse, you are charged for storage at the Azure Premium Storage rate.</span></span> <span data-ttu-id="53105-138">A vantagem de pausar é que você não é cobrado pelos recursos de computação DWU.</span><span class="sxs-lookup"><span data-stu-id="53105-138">The advantage of pausing is you are not charged for the DWU computing resources.</span></span>

<span data-ttu-id="53105-139">Para obter mais informações sobre os preços do SQL Data Warehouse, consulte [Preços do SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="53105-139">For more information about SQL Data Warehouse pricing, see [SQL Data Warehouse Pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>

## <a name="uses-for-restore"></a><span data-ttu-id="53105-140">Usos para restauração</span><span class="sxs-lookup"><span data-stu-id="53105-140">Uses for restore</span></span>
<span data-ttu-id="53105-141">O uso primário da restauração do data warehouse é recuperar os dados após a perda de dados ou corrupção acidental.</span><span class="sxs-lookup"><span data-stu-id="53105-141">The primary use for data warehouse restore is to recover data after accidental data loss or corruption.</span></span>

<span data-ttu-id="53105-142">Também é possível usar a restauração de data warehouse para manter um backup por mais de sete dias.</span><span class="sxs-lookup"><span data-stu-id="53105-142">You can also use data warehouse restore to retain a backup for longer than seven days.</span></span> <span data-ttu-id="53105-143">Quando o backup for restaurado, o seu data warehouse estará online e será possível pausá-lo indefinidamente para economizar custos de computação.</span><span class="sxs-lookup"><span data-stu-id="53105-143">Once the backup is restored, you have the data warehouse online and can pause it indefinitely to save compute costs.</span></span> <span data-ttu-id="53105-144">O banco de dados em pausa tem encargos de armazenamento com a taxa de armazenamento Premium do Azure.</span><span class="sxs-lookup"><span data-stu-id="53105-144">The paused database incurs storage charges at the Azure Premium Storage rate.</span></span> 

## <a name="related-topics"></a><span data-ttu-id="53105-145">Tópicos relacionados</span><span class="sxs-lookup"><span data-stu-id="53105-145">Related topics</span></span>
### <a name="scenarios"></a><span data-ttu-id="53105-146">Cenários</span><span class="sxs-lookup"><span data-stu-id="53105-146">Scenarios</span></span>
* <span data-ttu-id="53105-147">Para obter uma visão geral sobre a continuidade de negócios, veja [Visão geral da continuidade de negócios](../sql-database/sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="53105-147">For a business continuity overview, see [Business continuity overview](../sql-database/sql-database-business-continuity.md)</span></span>

<!-- ### Tasks -->

<span data-ttu-id="53105-148">Para executar uma restauração de data warehouse, restaure usando:</span><span class="sxs-lookup"><span data-stu-id="53105-148">To perform a data warehouse restore, restore using:</span></span>

* <span data-ttu-id="53105-149">O portal do Azure, consulte [Restore a data warehouse using the Azure portal (Restaurar um data warehouse usando o portal do Azure)](sql-data-warehouse-restore-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="53105-149">Azure portal, see [Restore a data warehouse using the Azure portal](sql-data-warehouse-restore-database-portal.md)</span></span>
* <span data-ttu-id="53105-150">Cmdlets do PowerShell, consulte [Restore a data warehouse using PowerShell cmdlets (Restaurar um data warehouse usando cmdlets do PowerShell)](sql-data-warehouse-restore-database-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="53105-150">PowerShell cmdlets, see [Restore a data warehouse using PowerShell cmdlets](sql-data-warehouse-restore-database-powershell.md)</span></span>
* <span data-ttu-id="53105-151">APIs REST, consulte [Restore a data warehouse using the REST APIs (Restaurar um data warehouse usando APIs REST)](sql-data-warehouse-restore-database-rest-api.md)</span><span class="sxs-lookup"><span data-stu-id="53105-151">REST APIs, see [Restore a data warehouse using the REST APIs](sql-data-warehouse-restore-database-rest-api.md)</span></span>

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
