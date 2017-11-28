---
title: aaaRestore um volume StorSimple de backup | Microsoft Docs
description: "Explica como toouse Olá toorestore de página do Gerenciador do StorSimple serviço Catálogo de Backup a um volume StorSimple um conjunto de backup."
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
ms.openlocfilehash: e0efa74b14603be41af0cfc5400de3c39ab8824e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a><span data-ttu-id="6f8d3-103">Restaurar um volume do StorSimple de um conjunto de backup</span><span class="sxs-lookup"><span data-stu-id="6f8d3-103">Restore a StorSimple volume from a backup set</span></span>
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a><span data-ttu-id="6f8d3-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="6f8d3-104">Overview</span></span>
<span data-ttu-id="6f8d3-105">Olá **catálogo de Backup** página exibe todos os conjuntos de backup de saudação que são criados quando os backups manuais ou automatizados são feitos.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-105">hello **Backup Catalog** page displays all hello backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="6f8d3-106">Você pode usar todos os backups de saudação de toolist essa página para uma política de backup ou um volume, selecione ou excluir backups, ou usar um backup toorestore ou clonar um volume.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-106">You can use this page toolist all hello backups for a backup policy or a volume, select or delete backups, or use a backup toorestore or clone a volume.</span></span>

 ![Página Catálogo de Backup](./media/storsimple-restore-from-backup-set/HCS_BackupCatalog.png)

<span data-ttu-id="6f8d3-108">Este tutorial explica como Olá toouse **catálogo de Backup** página toorestore um volume no dispositivo de um conjunto de backup.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-108">This tutorial explains how toouse hello **Backup Catalog** page toorestore a volume on your device from a backup set.</span></span>

## <a name="how-toouse-hello-backup-catalog"></a><span data-ttu-id="6f8d3-109">Como toouse Olá catálogo de backup</span><span class="sxs-lookup"><span data-stu-id="6f8d3-109">How toouse hello backup catalog</span></span>
<span data-ttu-id="6f8d3-110">Olá **catálogo de Backup** página fornece uma consulta que ajuda você a toonarrow sua seleção de conjunto de backup.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-110">hello **Backup Catalog** page provides a query that helps you toonarrow your backup set selection.</span></span> <span data-ttu-id="6f8d3-111">Você pode filtrar Olá conjuntos de backup que são recuperados com base em Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="6f8d3-111">You can filter hello backup sets that are retrieved based on hello following parameters:</span></span>

* <span data-ttu-id="6f8d3-112">**Dispositivo** – dispositivo Olá no qual Olá o conjunto de backup foi criado.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-112">**Device** – hello device on which hello backup set was created.</span></span>
* <span data-ttu-id="6f8d3-113">**Política de backup** ou **volume** – Olá a política de backup ou volume associado a este conjunto de backup.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-113">**Backup policy** or **volume** – hello backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="6f8d3-114">**De** e **para** – Olá intervalo de data e hora quando o conjunto de backup Olá foi criado.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-114">**From** and **To** – hello date and time range when hello backup set was created.</span></span>

<span data-ttu-id="6f8d3-115">Olá conjuntos de backup filtrados são então tabulados com base em Olá seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="6f8d3-115">hello filtered backup sets are then tabulated based on hello following attributes:</span></span>

* <span data-ttu-id="6f8d3-116">**Nome** – hello nome de política de backup hello ou volumes associados ao conjunto de backup hello.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-116">**Name** – hello name of hello backup policy or volume associated with hello backup set.</span></span>
* <span data-ttu-id="6f8d3-117">**Tamanho** – Olá tamanho real do conjunto de backup hello.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-117">**Size** – hello actual size of hello backup set.</span></span>
* <span data-ttu-id="6f8d3-118">**Criado em** – a data de saudação e a hora quando foram criados backups hello.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-118">**Created on** – hello date and time when hello backups were created.</span></span> 
* <span data-ttu-id="6f8d3-119">**Tipo** – Conjuntos de Backup podem ser instantâneos locais ou instantâneos de nuvem.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-119">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="6f8d3-120">Um instantâneo local é um backup de todos os dados de volume armazenados localmente no dispositivo hello, enquanto um instantâneo de nuvem se refere a toohello backup dos dados de volume que residem na nuvem de saudação.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-120">A local snapshot is a backup of all your volume data stored locally on hello device, whereas a cloud snapshot refers toohello backup of volume data residing in hello cloud.</span></span> <span data-ttu-id="6f8d3-121">Instantâneos locais fornecem acesso mais rápido, enquanto os instantâneos de nuvem são escolhidos para resiliência de dados.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-121">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="6f8d3-122">**Iniciado por** – backups Olá podem ser iniciados automaticamente de acordo com o agendamento de tooa ou manualmente por um usuário.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-122">**Initiated by** – hello backups can be initiated automatically according tooa schedule or manually by a user.</span></span> <span data-ttu-id="6f8d3-123">(Você pode usar backups de tooschedule uma política de backup.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-123">(You can use a backup policy tooschedule backups.</span></span> <span data-ttu-id="6f8d3-124">Como alternativa, você pode usar o hello **fazer backup** tootake opção um backup interativo.)</span><span class="sxs-lookup"><span data-stu-id="6f8d3-124">Alternatively, you can use hello **Take backup** option tootake an interactive backup.)</span></span>

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a><span data-ttu-id="6f8d3-125">Como toorestore seu volume StorSimple de um backup</span><span class="sxs-lookup"><span data-stu-id="6f8d3-125">How toorestore your StorSimple volume from a backup</span></span>
<span data-ttu-id="6f8d3-126">Você pode usar o hello **catálogo de Backup** página toorestore seu volume StorSimple de um backup específico.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-126">You can use hello **Backup Catalog** page toorestore your StorSimple volume from a specific backup.</span></span> 

> [!WARNING]
> <span data-ttu-id="6f8d3-127">Restauração de um backup substituirá os volumes existentes de backup Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-127">Restoring from a backup will replace hello existing volumes from hello backup.</span></span> <span data-ttu-id="6f8d3-128">Isso pode causar perda de saudação de todos os dados gravados após Olá backup foi feito.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-128">This may cause hello loss of any data that was written after hello backup was taken.</span></span>
> 
> 

<span data-ttu-id="6f8d3-129">Antes de iniciar uma restauração em um volume, certifique-se de que o volume de saudação está offline.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-129">Before you initiate a restore on a volume, ensure that hello volume is offline.</span></span> <span data-ttu-id="6f8d3-130">Será necessário volume de saudação do tootake offline no host Olá primeiro e, em seguida, Olá dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-130">You will need tootake hello volume offline on hello host first and then hello device.</span></span> <span data-ttu-id="6f8d3-131">Siga as etapas de saudação em [colocar um volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="6f8d3-131">Follow hello steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span> <span data-ttu-id="6f8d3-132">Execute Olá seguir etapas toorestore um volume de um conjunto de backup.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-132">Perform hello following steps toorestore a volume from a backup set.</span></span>

### <a name="toorestore-from-a-backup-set"></a><span data-ttu-id="6f8d3-133">toorestore um conjunto de backup</span><span class="sxs-lookup"><span data-stu-id="6f8d3-133">toorestore from a backup set</span></span>
1. <span data-ttu-id="6f8d3-134">Na página de serviço do StorSimple Manager hello, clique em Olá **catálogo de Backup** guia.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-134">On hello StorSimple Manager service page, click hello **Backup catalog** tab.</span></span>
   
    ![Catálogo de backup](./media/storsimple-restore-from-backup-set/HCS_Restore.png)
2. <span data-ttu-id="6f8d3-136">Selecione um conjunto de backup desta maneira:</span><span class="sxs-lookup"><span data-stu-id="6f8d3-136">Select a backup set as follows:</span></span>
   
   1. <span data-ttu-id="6f8d3-137">Selecione dispositivo de saudação apropriado.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-137">Select hello appropriate device.</span></span>
   2. <span data-ttu-id="6f8d3-138">Na lista suspensa de saudação, escolha política de backup ou volume Olá para backup de saudação que você deseja tooselect.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-138">In hello drop-down list, choose hello volume or backup policy for hello backup that you wish tooselect.</span></span>
   3. <span data-ttu-id="6f8d3-139">Especifique o intervalo de tempo de saudação.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-139">Specify hello time range.</span></span>
   4. <span data-ttu-id="6f8d3-140">Clique o ícone de verificação Olá</span><span class="sxs-lookup"><span data-stu-id="6f8d3-140">Click hello check icon</span></span> ![ícone de verificação](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png) <span data-ttu-id="6f8d3-142">tooexecute esta consulta.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-142">tooexecute this query.</span></span>
      
      <span data-ttu-id="6f8d3-143">Hello backups associados à política de backup ou volume Olá selecionado devem aparecer na lista de saudação de conjuntos de backup.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-143">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>
3. <span data-ttu-id="6f8d3-144">Expanda Olá conjunto de backup tooview Olá associado volumes.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-144">Expand hello backup set tooview hello associated volumes.</span></span> <span data-ttu-id="6f8d3-145">Esses volumes devem ser colocados offline no host hello e no dispositivo antes de restaurá-los.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-145">These volumes must be taken offline on hello host and device before you can restore them.</span></span> <span data-ttu-id="6f8d3-146">Siga as etapas de saudação em [colocar um volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="6f8d3-146">Follow hello steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="6f8d3-147">Certifique-se de que você colocou Olá volumes offline no host Olá primeiro, antes de colocar Olá volumes offline no dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-147">Make sure that you have taken hello volumes offline on hello host first, before you take hello volumes offline on hello device.</span></span> <span data-ttu-id="6f8d3-148">Se você não colocar volumes de Olá offline no host hello, isso pode levar potencialmente toodata corrupção.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-148">If you do not take hello volumes offline on hello host, it could potentially lead toodata corruption.</span></span>
   > 
   > 
4. <span data-ttu-id="6f8d3-149">Selecione um conjunto de backup.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-149">Select a backup set.</span></span> <span data-ttu-id="6f8d3-150">Clique em **restaurar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-150">Click **Restore** at hello bottom of hello page.</span></span>
5. <span data-ttu-id="6f8d3-151">Será solicitada a sua confirmação.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-151">You will be prompted for confirmation.</span></span> 
   
    ![Página de confirmação](./media/storsimple-restore-from-backup-set/HCS_ConfirmRestore.png)
6. <span data-ttu-id="6f8d3-153">Examinar as informações de restauração hello e clique no ícone de verificação Olá ![ícone de verificação](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span><span class="sxs-lookup"><span data-stu-id="6f8d3-153">Review hello restore information and click hello check icon ![check icon](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span></span> <span data-ttu-id="6f8d3-154">Isso iniciará um trabalho de restauração que você pode exibir acessando Olá **trabalhos** página.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-154">This will initiate a restore job that you can view by accessing hello **Jobs** page.</span></span> 
7. <span data-ttu-id="6f8d3-155">Após a conclusão da restauração hello, você pode verificar se conteúdo Olá de seus volumes é substituído por volumes de backup hello.</span><span class="sxs-lookup"><span data-stu-id="6f8d3-155">After hello restore is complete, you can verify that hello contents of your volumes are replaced by volumes from hello backup.</span></span>

<span data-ttu-id="6f8d3-156">![Vídeo disponível](./media/storsimple-restore-from-backup-set/Video_icon.png) **Vídeo disponível**</span><span class="sxs-lookup"><span data-stu-id="6f8d3-156">![Video available](./media/storsimple-restore-from-backup-set/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="6f8d3-157">toowatch um vídeo que demonstra como você pode usar o clone hello e restaurar recursos no StorSimple toorecover excluído arquivos, clique em [aqui](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span><span class="sxs-lookup"><span data-stu-id="6f8d3-157">toowatch a video that demonstrates how you can use hello clone and restore features in StorSimple toorecover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f8d3-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6f8d3-158">Next steps</span></span>
* <span data-ttu-id="6f8d3-159">Saiba como muito[StorSimple gerenciar volumes](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="6f8d3-159">Learn how too[Manage StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="6f8d3-160">Saiba como muito[use Olá tooadminister do serviço StorSimple Manager seu dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="6f8d3-160">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

