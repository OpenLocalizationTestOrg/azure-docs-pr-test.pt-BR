---
title: Restaurar um volume do StorSimple de um backup | Microsoft Docs
description: "Explica como usar a página Catálogo de Backup do serviço StorSimple Manager para restaurar um volume do StorSimple de um conjunto de backup."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b979782e-3184-4465-ad5f-e4516a5885d2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 12484338f5b4d489604d70a657ef0992b6267297
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a><span data-ttu-id="eea91-103">Restaurar um volume do StorSimple de um conjunto de backup</span><span class="sxs-lookup"><span data-stu-id="eea91-103">Restore a StorSimple volume from a backup set</span></span>
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a><span data-ttu-id="eea91-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="eea91-104">Overview</span></span>
<span data-ttu-id="eea91-105">A página **Catálogo de Backup** exibe todos os conjuntos de backup criados após a realização de backups manuais ou automatizados.</span><span class="sxs-lookup"><span data-stu-id="eea91-105">The **Backup Catalog** page displays all the backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="eea91-106">Você pode usar esta página para listar todos os backups para uma política de backup ou volume, selecionar ou excluir os backups, ou usar um backup para restaurar ou clonar um volume.</span><span class="sxs-lookup"><span data-stu-id="eea91-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span></span>

 ![Página Catálogo de Backup](./media/storsimple-restore-from-backup-set/HCS_BackupCatalog.png)

<span data-ttu-id="eea91-108">Este tutorial explica como usar a página **Catálogo de Backup** para restaurar um volume em seu dispositivo a partir de um conjunto de backup.</span><span class="sxs-lookup"><span data-stu-id="eea91-108">This tutorial explains how to use the **Backup Catalog** page to restore a volume on your device from a backup set.</span></span>

## <a name="how-to-use-the-backup-catalog"></a><span data-ttu-id="eea91-109">Como usar o catálogo de backup</span><span class="sxs-lookup"><span data-stu-id="eea91-109">How to use the backup catalog</span></span>
<span data-ttu-id="eea91-110">A página **Catálogo de Backup** oferece uma consulta que ajuda a restringir sua seleção de conjuntos de backup.</span><span class="sxs-lookup"><span data-stu-id="eea91-110">The **Backup Catalog** page provides a query that helps you to narrow your backup set selection.</span></span> <span data-ttu-id="eea91-111">Você pode filtrar os conjuntos de backup recuperados com base nos seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="eea91-111">You can filter the backup sets that are retrieved based on the following parameters:</span></span>

* <span data-ttu-id="eea91-112">**Dispositivo** – O dispositivo no qual o conjunto de backup foi criado.</span><span class="sxs-lookup"><span data-stu-id="eea91-112">**Device** – The device on which the backup set was created.</span></span>
* <span data-ttu-id="eea91-113">**Política** ou **volume** de Backup – A política ou volume de backup associado a este conjunto de backup.</span><span class="sxs-lookup"><span data-stu-id="eea91-113">**Backup policy** or **volume** – The backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="eea91-114">**De** e **Para** – O intervalo de datas e horas em que o conjunto de backup foi criado.</span><span class="sxs-lookup"><span data-stu-id="eea91-114">**From** and **To** – The date and time range when the backup set was created.</span></span>

<span data-ttu-id="eea91-115">Os conjuntos de backup filtrados são então tabulados com base nos seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="eea91-115">The filtered backup sets are then tabulated based on the following attributes:</span></span>

* <span data-ttu-id="eea91-116">**Nome** – O nome da política de backup ou do volume associada a este conjunto de backup.</span><span class="sxs-lookup"><span data-stu-id="eea91-116">**Name** – The name of the backup policy or volume associated with the backup set.</span></span>
* <span data-ttu-id="eea91-117">**Tamanho** – O tamanho real do conjunto de backup.</span><span class="sxs-lookup"><span data-stu-id="eea91-117">**Size** – The actual size of the backup set.</span></span>
* <span data-ttu-id="eea91-118">**Criado em** – O intervalo de data e hora quando os backups foram criados.</span><span class="sxs-lookup"><span data-stu-id="eea91-118">**Created on** – The date and time when the backups were created.</span></span> 
* <span data-ttu-id="eea91-119">**Tipo** – Conjuntos de Backup podem ser instantâneos locais ou instantâneos de nuvem.</span><span class="sxs-lookup"><span data-stu-id="eea91-119">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="eea91-120">Um instantâneo local é um backup de todos os dados do volume armazenadas localmente no dispositivo, enquanto um instantâneo de nuvem refere-se ao backup dos dados do volume que residem na nuvem.</span><span class="sxs-lookup"><span data-stu-id="eea91-120">A local snapshot is a backup of all your volume data stored locally on the device, whereas a cloud snapshot refers to the backup of volume data residing in the cloud.</span></span> <span data-ttu-id="eea91-121">Instantâneos locais fornecem acesso mais rápido, enquanto os instantâneos de nuvem são escolhidos para resiliência de dados.</span><span class="sxs-lookup"><span data-stu-id="eea91-121">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="eea91-122">**Iniciada por** – Os backups podem ser iniciados de forma automática, de acordo com uma agenda, ou de forma manual por um usuário.</span><span class="sxs-lookup"><span data-stu-id="eea91-122">**Initiated by** – The backups can be initiated automatically according to a schedule or manually by a user.</span></span> <span data-ttu-id="eea91-123">(Você pode usar uma política de backup para agendar backups.</span><span class="sxs-lookup"><span data-stu-id="eea91-123">(You can use a backup policy to schedule backups.</span></span> <span data-ttu-id="eea91-124">Como alternativa, você pode usar a opção **Fazer backup** para fazer um backup interativo).</span><span class="sxs-lookup"><span data-stu-id="eea91-124">Alternatively, you can use the **Take backup** option to take an interactive backup.)</span></span>

## <a name="how-to-restore-your-storsimple-volume-from-a-backup"></a><span data-ttu-id="eea91-125">Como restaurar o volume StorSimple de um backup</span><span class="sxs-lookup"><span data-stu-id="eea91-125">How to restore your StorSimple volume from a backup</span></span>
<span data-ttu-id="eea91-126">É possível usar a página **Catálogo de Backup** para restaurar o volume do StorSimple de um backup específico.</span><span class="sxs-lookup"><span data-stu-id="eea91-126">You can use the **Backup Catalog** page to restore your StorSimple volume from a specific backup.</span></span> 

> [!WARNING]
> <span data-ttu-id="eea91-127">A restauração de um backup substituirá os volumes existentes do backup.</span><span class="sxs-lookup"><span data-stu-id="eea91-127">Restoring from a backup will replace the existing volumes from the backup.</span></span> <span data-ttu-id="eea91-128">Isso pode causar a perda de todos os dados gravados depois que o backup tiver sido feito.</span><span class="sxs-lookup"><span data-stu-id="eea91-128">This may cause the loss of any data that was written after the backup was taken.</span></span>
> 
> 

<span data-ttu-id="eea91-129">Antes de iniciar uma restauração em um volume, verifique se o volume está offline.</span><span class="sxs-lookup"><span data-stu-id="eea91-129">Before you initiate a restore on a volume, ensure that the volume is offline.</span></span> <span data-ttu-id="eea91-130">Você precisará colocar o volume offline no host primeiro e, em seguida, no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="eea91-130">You will need to take the volume offline on the host first and then the device.</span></span> <span data-ttu-id="eea91-131">Siga as etapas em [Colocar um volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="eea91-131">Follow the steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span> <span data-ttu-id="eea91-132">Execute as etapas a seguir para restaurar um volume de um conjunto de backup.</span><span class="sxs-lookup"><span data-stu-id="eea91-132">Perform the following steps to restore a volume from a backup set.</span></span>

### <a name="to-restore-from-a-backup-set"></a><span data-ttu-id="eea91-133">Para restaurar de um conjunto de backup</span><span class="sxs-lookup"><span data-stu-id="eea91-133">To restore from a backup set</span></span>
1. <span data-ttu-id="eea91-134">Na página do serviço Gerenciador do StorSimple, clique na guia **Catálogo de backup** .</span><span class="sxs-lookup"><span data-stu-id="eea91-134">On the StorSimple Manager service page, click the **Backup catalog** tab.</span></span>
   
    ![Catálogo de Backup](./media/storsimple-restore-from-backup-set/HCS_Restore.png)
2. <span data-ttu-id="eea91-136">Selecione um conjunto de backup desta maneira:</span><span class="sxs-lookup"><span data-stu-id="eea91-136">Select a backup set as follows:</span></span>
   
   1. <span data-ttu-id="eea91-137">Selecione o dispositivo adequado.</span><span class="sxs-lookup"><span data-stu-id="eea91-137">Select the appropriate device.</span></span>
   2. <span data-ttu-id="eea91-138">Na lista suspensa, escolha o volume ou a política de backup para o backup que você deseja selecionar.</span><span class="sxs-lookup"><span data-stu-id="eea91-138">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   3. <span data-ttu-id="eea91-139">Especifique o intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="eea91-139">Specify the time range.</span></span>
   4. <span data-ttu-id="eea91-140">Clique no ícone de verificação </span><span class="sxs-lookup"><span data-stu-id="eea91-140">Click the check icon</span></span> ![ícone de verificação](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png) <span data-ttu-id="eea91-142">para executar esta consulta.</span><span class="sxs-lookup"><span data-stu-id="eea91-142">to execute this query.</span></span>
      
      <span data-ttu-id="eea91-143">Os backups associados ao volume ou à política de backup selecionada devem aparecer na lista de conjuntos de backup.</span><span class="sxs-lookup"><span data-stu-id="eea91-143">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
3. <span data-ttu-id="eea91-144">Expanda o conjunto de backup para exibir os volumes associados.</span><span class="sxs-lookup"><span data-stu-id="eea91-144">Expand the backup set to view the associated volumes.</span></span> <span data-ttu-id="eea91-145">Esses volumes devem ficar offline no host e no dispositivo antes que você possa restaurá-los.</span><span class="sxs-lookup"><span data-stu-id="eea91-145">These volumes must be taken offline on the host and device before you can restore them.</span></span> <span data-ttu-id="eea91-146">Siga as etapas em [Colocar um volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="eea91-146">Follow the steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="eea91-147">Verifique se você colocou os volumes offline primeiro no host antes de colocar os volumes offline no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="eea91-147">Make sure that you have taken the volumes offline on the host first, before you take the volumes offline on the device.</span></span> <span data-ttu-id="eea91-148">Se você não colocar os volumes offline no host, poderá ocorrer corrupção nos dados.</span><span class="sxs-lookup"><span data-stu-id="eea91-148">If you do not take the volumes offline on the host, it could potentially lead to data corruption.</span></span>
   > 
   > 
4. <span data-ttu-id="eea91-149">Selecione um conjunto de backup.</span><span class="sxs-lookup"><span data-stu-id="eea91-149">Select a backup set.</span></span> <span data-ttu-id="eea91-150">Clique em **Restaurar** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="eea91-150">Click **Restore** at the bottom of the page.</span></span>
5. <span data-ttu-id="eea91-151">Será solicitada a sua confirmação.</span><span class="sxs-lookup"><span data-stu-id="eea91-151">You will be prompted for confirmation.</span></span> 
   
    ![Página de confirmação](./media/storsimple-restore-from-backup-set/HCS_ConfirmRestore.png)
6. <span data-ttu-id="eea91-153">Examine as informações de restauração e clique no ícone de verificação ![ícone de verificação](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span><span class="sxs-lookup"><span data-stu-id="eea91-153">Review the restore information and click the check icon ![check icon](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span></span> <span data-ttu-id="eea91-154">Isso iniciará um trabalho de restauração que poderá ser exibido por meio do acesso à página **Trabalhos** .</span><span class="sxs-lookup"><span data-stu-id="eea91-154">This will initiate a restore job that you can view by accessing the **Jobs** page.</span></span> 
7. <span data-ttu-id="eea91-155">Após a conclusão da restauração, você poderá verificar se o conteúdo de seus volumes foi substituído pelos volumes do backup.</span><span class="sxs-lookup"><span data-stu-id="eea91-155">After the restore is complete, you can verify that the contents of your volumes are replaced by volumes from the backup.</span></span>

<span data-ttu-id="eea91-156">![Vídeo disponível](./media/storsimple-restore-from-backup-set/Video_icon.png) **Vídeo disponível**</span><span class="sxs-lookup"><span data-stu-id="eea91-156">![Video available](./media/storsimple-restore-from-backup-set/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="eea91-157">Para assistir a um vídeo que demonstra como você pode usar os recursos de clonagem e restauração no StorSimple para recuperar arquivos excluídos, clique [aqui](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span><span class="sxs-lookup"><span data-stu-id="eea91-157">To watch a video that demonstrates how you can use the clone and restore features in StorSimple to recover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="eea91-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="eea91-158">Next steps</span></span>
* <span data-ttu-id="eea91-159">Saiba como [Gerenciar volumes do StorSimple](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="eea91-159">Learn how to [Manage StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="eea91-160">Saiba como [usar o serviço StorSimple Manager para administrar seu dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="eea91-160">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

