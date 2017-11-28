---
title: "Gerenciar catálogo de backup do StorSimple | Microsoft Docs"
description: "Explica como usar a página Catálogo de Backup do serviço StorSimple Manager para listar, selecionar e excluir conjuntos de backup para um volume."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ad81bee9-fe43-40b3-a384-b15fb274ecd9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/28/2016
ms.author: v-sharos
ms.openlocfilehash: 5ee9855e1428c7a2d871d9c215d302c5c3b7101a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-your-backup-catalog"></a><span data-ttu-id="bc90d-103">Usar o serviço StorSimple Manager para gerenciar o catálogo de backup</span><span class="sxs-lookup"><span data-stu-id="bc90d-103">Use the StorSimple Manager service to manage your backup catalog</span></span>
## <a name="overview"></a><span data-ttu-id="bc90d-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="bc90d-104">Overview</span></span>
<span data-ttu-id="bc90d-105">A página **Catálogo de Backup** do serviço StorSimple Manager exibe todos os conjuntos de backup criados após a realização de backups manuais ou agendados.</span><span class="sxs-lookup"><span data-stu-id="bc90d-105">The StorSimple Manager service **Backup Catalog** page displays all the backup sets that are created when manual or scheduled backups are taken.</span></span> <span data-ttu-id="bc90d-106">Você pode usar esta página para listar todos os backups para uma política de backup ou volume, selecionar ou excluir os backups, ou usar um backup para restaurar ou clonar um volume.</span><span class="sxs-lookup"><span data-stu-id="bc90d-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span></span>

<span data-ttu-id="bc90d-107">Este tutorial explica como listar, selecionar e excluir um conjunto de backup.</span><span class="sxs-lookup"><span data-stu-id="bc90d-107">This tutorial explains how to list, select, and delete a backup set.</span></span> <span data-ttu-id="bc90d-108">Para saber como restaurar seu dispositivo de backup, vá para [Restaurar seu dispositivo por meio de um conjunto de backup](storsimple-restore-from-backup-set.md).</span><span class="sxs-lookup"><span data-stu-id="bc90d-108">To learn how to restore your device from backup, go to [Restore your device from a backup set](storsimple-restore-from-backup-set.md).</span></span> <span data-ttu-id="bc90d-109">Para saber como clonar um volume, vá para [Clonar um volume do StorSimple](storsimple-clone-volume.md).</span><span class="sxs-lookup"><span data-stu-id="bc90d-109">To learn how to clone a volume, go to [Clone a StorSimple volume](storsimple-clone-volume.md).</span></span>

![Catálogo de Backup](./media/storsimple-manage-backup-catalog/backupcatalog.png) 

<span data-ttu-id="bc90d-111">A página **Catálogo de Backup** oferece uma consulta para restringir sua seleção de conjuntos de backup.</span><span class="sxs-lookup"><span data-stu-id="bc90d-111">The **Backup Catalog** page provides a query to narrow your backup set selection.</span></span> <span data-ttu-id="bc90d-112">Você pode filtrar os conjuntos de backup recuperados com base nos seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="bc90d-112">You can filter the backup sets that are retrieved, based on the following parameters:</span></span>

* <span data-ttu-id="bc90d-113">**Dispositivo** – O dispositivo no qual o conjunto de backup foi criado.</span><span class="sxs-lookup"><span data-stu-id="bc90d-113">**Device** – The device on which the backup set was created.</span></span>
* <span data-ttu-id="bc90d-114">**Política de Backup ou de Volume** – a política ou volume de backup associado a este conjunto de backup.</span><span class="sxs-lookup"><span data-stu-id="bc90d-114">**Backup Policy or Volume** – The backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="bc90d-115">**De e Para** – o intervalo de datas e horas em que o conjunto de backup foi criado.</span><span class="sxs-lookup"><span data-stu-id="bc90d-115">**From and To** – The date and time range when the backup set was created.</span></span>

<span data-ttu-id="bc90d-116">Os conjuntos de backup filtrados são então tabulados com base nos seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="bc90d-116">The filtered backup sets are then tabulated based on the following attributes:</span></span>

* <span data-ttu-id="bc90d-117">**Nome** – O nome da política de backup ou do volume associada a este conjunto de backup.</span><span class="sxs-lookup"><span data-stu-id="bc90d-117">**Name** – The name of the backup policy or volume associated with the backup set.</span></span>
* <span data-ttu-id="bc90d-118">**Tamanho** – O tamanho real do conjunto de backup.</span><span class="sxs-lookup"><span data-stu-id="bc90d-118">**Size** – The actual size of the backup set.</span></span>
* <span data-ttu-id="bc90d-119">**Criado em** – O intervalo de data e hora quando os backups foram criados.</span><span class="sxs-lookup"><span data-stu-id="bc90d-119">**Created On** – The date and time when the backups were created.</span></span> 
* <span data-ttu-id="bc90d-120">**Tipo** – Conjuntos de Backup podem ser instantâneos locais ou instantâneos de nuvem.</span><span class="sxs-lookup"><span data-stu-id="bc90d-120">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="bc90d-121">Um instantâneo local é um backup de todos os dados do volume armazenadas localmente no dispositivo, enquanto um instantâneo de nuvem refere-se ao backup dos dados do volume que residem na nuvem.</span><span class="sxs-lookup"><span data-stu-id="bc90d-121">A local snapshot is a backup of all your volume data stored locally on the device, whereas a cloud snapshot refers to the backup of volume data residing in the cloud.</span></span> <span data-ttu-id="bc90d-122">Instantâneos locais fornecem acesso mais rápido, enquanto os instantâneos de nuvem são escolhidos para resiliência de dados.</span><span class="sxs-lookup"><span data-stu-id="bc90d-122">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="bc90d-123">**Iniciada por** – os backups podem ser iniciados de forma automática, de acordo com uma agenda ou de forma manual por um usuário.</span><span class="sxs-lookup"><span data-stu-id="bc90d-123">**Initiated By** – The backups can be initiated automatically by a schedule or manually by a user.</span></span> <span data-ttu-id="bc90d-124">Você pode usar uma política de backup para agendar backups.</span><span class="sxs-lookup"><span data-stu-id="bc90d-124">You can use a backup policy to schedule backups.</span></span> <span data-ttu-id="bc90d-125">Como alternativa, você pode usar a opção **Fazer backup** para fazer um backup manual.</span><span class="sxs-lookup"><span data-stu-id="bc90d-125">Alternatively, you can use the **Take backup** option to take a manual backup.</span></span>

## <a name="list-backup-sets-for-a-volume"></a><span data-ttu-id="bc90d-126">Listar conjuntos de backup para um volume</span><span class="sxs-lookup"><span data-stu-id="bc90d-126">List backup sets for a volume</span></span>
<span data-ttu-id="bc90d-127">Conclua as etapas a seguir para listar todos os backups de um volume.</span><span class="sxs-lookup"><span data-stu-id="bc90d-127">Complete the following steps to list all the backups for a volume.</span></span>

#### <a name="to-list-backup-sets"></a><span data-ttu-id="bc90d-128">Para listar conjuntos de backup</span><span class="sxs-lookup"><span data-stu-id="bc90d-128">To list backup sets</span></span>
1. <span data-ttu-id="bc90d-129">Na página do serviço Gerenciador do StorSimple, clique na guia **Catálogo de backup** .</span><span class="sxs-lookup"><span data-stu-id="bc90d-129">On the StorSimple Manager service page, click the **Backup catalog** tab.</span></span>
2. <span data-ttu-id="bc90d-130">Filtre as seleções da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="bc90d-130">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="bc90d-131">Selecione o dispositivo adequado.</span><span class="sxs-lookup"><span data-stu-id="bc90d-131">Select the appropriate device.</span></span>
   2. <span data-ttu-id="bc90d-132">Na lista suspensa, escolha um volume para exibir os backups correspondentes.</span><span class="sxs-lookup"><span data-stu-id="bc90d-132">In the drop-down list, choose a volume to view the corresponding the backups.</span></span>
   3. <span data-ttu-id="bc90d-133">Especifique o intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="bc90d-133">Specify the time range.</span></span>
   4. <span data-ttu-id="bc90d-134">Clique no ícone de verificação </span><span class="sxs-lookup"><span data-stu-id="bc90d-134">Click the check icon</span></span> ![Ícone de verificação](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="bc90d-136">para executar esta consulta.</span><span class="sxs-lookup"><span data-stu-id="bc90d-136">to execute this query.</span></span>
      
      <span data-ttu-id="bc90d-137">Os backups associados ao volume selecionado devem aparecer na lista de conjuntos de backup.</span><span class="sxs-lookup"><span data-stu-id="bc90d-137">The backups associated with the selected volume should appear in the list of backup sets.</span></span>

## <a name="select-a-backup-set"></a><span data-ttu-id="bc90d-138">Selecione um conjunto de backup</span><span class="sxs-lookup"><span data-stu-id="bc90d-138">Select a backup set</span></span>
<span data-ttu-id="bc90d-139">Conclua as seguintes etapas para selecionar um conjunto de backup para uma política de volume ou backup.</span><span class="sxs-lookup"><span data-stu-id="bc90d-139">Complete the following steps to select a backup set for a volume or backup policy.</span></span>

#### <a name="to-select-a-backup-set"></a><span data-ttu-id="bc90d-140">Para selecionar um conjunto de backups</span><span class="sxs-lookup"><span data-stu-id="bc90d-140">To select a backup set</span></span>
1. <span data-ttu-id="bc90d-141">Na página do serviço Gerenciador do StorSimple, clique na guia **Catálogo de backup** .</span><span class="sxs-lookup"><span data-stu-id="bc90d-141">On the StorSimple Manager service page, click the **Backup catalog** tab.</span></span>
2. <span data-ttu-id="bc90d-142">Filtre as seleções da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="bc90d-142">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="bc90d-143">Selecione o dispositivo adequado.</span><span class="sxs-lookup"><span data-stu-id="bc90d-143">Select the appropriate device.</span></span>
   2. <span data-ttu-id="bc90d-144">Na lista suspensa, escolha o volume ou a política de backup para o backup que você deseja selecionar.</span><span class="sxs-lookup"><span data-stu-id="bc90d-144">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   3. <span data-ttu-id="bc90d-145">Especifique o intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="bc90d-145">Specify the time range.</span></span>
   4. <span data-ttu-id="bc90d-146">Clique no ícone de verificação </span><span class="sxs-lookup"><span data-stu-id="bc90d-146">Click the check icon</span></span> ![Ícone de verificação](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="bc90d-148">para executar esta consulta.</span><span class="sxs-lookup"><span data-stu-id="bc90d-148">to execute this query.</span></span>
      
      <span data-ttu-id="bc90d-149">Os backups associados ao volume ou à política de backup selecionada devem aparecer na lista de conjuntos de backup.</span><span class="sxs-lookup"><span data-stu-id="bc90d-149">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
3. <span data-ttu-id="bc90d-150">Selecione e expanda um conjunto de backups.</span><span class="sxs-lookup"><span data-stu-id="bc90d-150">Select and expand a backup set.</span></span> <span data-ttu-id="bc90d-151">As opções **Restaurar** e **Excluir** são exibidas na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="bc90d-151">The **Restore** and **Delete** options are displayed at the bottom of the page.</span></span> <span data-ttu-id="bc90d-152">Você pode executar qualquer uma dessas ações no conjunto de backup selecionado.</span><span class="sxs-lookup"><span data-stu-id="bc90d-152">You can perform either of these actions on the backup set that you selected.</span></span>

## <a name="delete-a-backup-set"></a><span data-ttu-id="bc90d-153">Excluir um conjunto de backups</span><span class="sxs-lookup"><span data-stu-id="bc90d-153">Delete a backup set</span></span>
<span data-ttu-id="bc90d-154">Exclua um backup quando você não quiser mais manter os dados associados a ele.</span><span class="sxs-lookup"><span data-stu-id="bc90d-154">Delete a backup when you no longer wish to retain the data associated with it.</span></span> <span data-ttu-id="bc90d-155">Execute as etapas a seguir para excluir um conjunto de backups.</span><span class="sxs-lookup"><span data-stu-id="bc90d-155">Perform the following steps to delete a backup set.</span></span>

#### <a name="to-delete-a-backup-set"></a><span data-ttu-id="bc90d-156">Para excluir um conjunto de backups</span><span class="sxs-lookup"><span data-stu-id="bc90d-156">To delete a backup set</span></span>
1. <span data-ttu-id="bc90d-157">Na página do serviço Gerenciador do StorSimple, clique na **guia Catálogo de Backup**.</span><span class="sxs-lookup"><span data-stu-id="bc90d-157">On the StorSimple Manager service page, click the **Backup Catalog tab**.</span></span>
2. <span data-ttu-id="bc90d-158">Filtre as seleções da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="bc90d-158">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="bc90d-159">Selecione o dispositivo adequado.</span><span class="sxs-lookup"><span data-stu-id="bc90d-159">Select the appropriate device.</span></span>
   2. <span data-ttu-id="bc90d-160">Na lista suspensa, escolha o volume ou a política de backup para o backup que você deseja selecionar.</span><span class="sxs-lookup"><span data-stu-id="bc90d-160">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   3. <span data-ttu-id="bc90d-161">Especifique o intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="bc90d-161">Specify the time range.</span></span>
   4. <span data-ttu-id="bc90d-162">Clique no ícone de verificação </span><span class="sxs-lookup"><span data-stu-id="bc90d-162">Click the check icon</span></span> ![Ícone de verificação](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="bc90d-164">para executar esta consulta.</span><span class="sxs-lookup"><span data-stu-id="bc90d-164">to execute this query.</span></span>
      
      <span data-ttu-id="bc90d-165">Os backups associados ao volume ou à política de backup selecionada devem aparecer na lista de conjuntos de backup.</span><span class="sxs-lookup"><span data-stu-id="bc90d-165">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
3. <span data-ttu-id="bc90d-166">Selecione e expanda um conjunto de backups.</span><span class="sxs-lookup"><span data-stu-id="bc90d-166">Select and expand a backup set.</span></span> <span data-ttu-id="bc90d-167">As opções **Restaurar** e **Excluir** são exibidas na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="bc90d-167">The **Restore** and **Delete** options are displayed at the bottom of the page.</span></span> <span data-ttu-id="bc90d-168">Clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="bc90d-168">Click **Delete**.</span></span>
4. <span data-ttu-id="bc90d-169">Você será notificado quando a exclusão estiver em andamento e quando ela for concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="bc90d-169">You will be notified when the deletion is in progress and when it has successfully finished.</span></span> <span data-ttu-id="bc90d-170">Após a exclusão, atualize a consulta nesta página.</span><span class="sxs-lookup"><span data-stu-id="bc90d-170">After the deletion is done, refresh the query on this page.</span></span> <span data-ttu-id="bc90d-171">O conjunto de backup excluído não aparecerá mais na lista de conjuntos de backup.</span><span class="sxs-lookup"><span data-stu-id="bc90d-171">The deleted backup set will no longer appear in the list of backup sets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc90d-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bc90d-172">Next steps</span></span>
* <span data-ttu-id="bc90d-173">Saiba como [usar o catálogo de backup para restaurar seu dispositivo de um conjunto de backup](storsimple-restore-from-backup-set.md).</span><span class="sxs-lookup"><span data-stu-id="bc90d-173">Learn how to [use the backup catalog to restore your device from a backup set](storsimple-restore-from-backup-set.md).</span></span>
* <span data-ttu-id="bc90d-174">Saiba como [usar o serviço StorSimple Manager para administrar seu dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="bc90d-174">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

