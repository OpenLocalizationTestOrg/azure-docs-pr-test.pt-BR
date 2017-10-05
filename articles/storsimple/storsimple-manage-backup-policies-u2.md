---
title: "Gerenciar as políticas de backup do StorSimple | Microsoft Docs"
description: "Explica como você pode usar o serviço StorSimple Manager para criar e gerenciar backups manuais, agendas de backup e retenção de backup."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 4a2db707-bbfc-425c-bfeb-bc5c97781873
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
ms.openlocfilehash: 5448247428ab96887470c6b53f7a9b3dcd9238f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-backup-policies-update-2"></a><span data-ttu-id="dc83b-103">Usar o serviço StorSimple Manager para gerenciar políticas de backup (Atualização 2)</span><span class="sxs-lookup"><span data-stu-id="dc83b-103">Use the StorSimple Manager service to manage backup policies (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a><span data-ttu-id="dc83b-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="dc83b-104">Overview</span></span>
<span data-ttu-id="dc83b-105">Este tutorial explica como usar a página **Políticas de Backup** do serviço Gerenciador do StorSimple para controlar os processos e a retenção de backup dos volumes do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="dc83b-105">This tutorial explains how to use the StorSimple Manager service **Backup Policies** page to control backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="dc83b-106">Ele também descreve como concluir um backup manual.</span><span class="sxs-lookup"><span data-stu-id="dc83b-106">It also describes how to complete a manual backup.</span></span>

<span data-ttu-id="dc83b-107">Quando você faz backup de um volume, você pode escolher criar um instantâneo local ou um instantâneo de nuvem.</span><span class="sxs-lookup"><span data-stu-id="dc83b-107">When you back up a volume, you can choose to create a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="dc83b-108">Se você estiver fazendo backup de um volume fixado localmente, é recomendável que você especifique um instantâneo de nuvem.</span><span class="sxs-lookup"><span data-stu-id="dc83b-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="dc83b-109">Gravar um grande número de instantâneos locais de um volume fixado localmente juntamente com um conjunto de dados que tem muita variação resultará em uma situação em que você pode, rapidamente, ficar sem espaço local.</span><span class="sxs-lookup"><span data-stu-id="dc83b-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="dc83b-110">Se você optar por tirar instantâneos locais, recomendamos que você menos instantâneos diários para fazer backup do estado mais recente, mantê-los por um dia e, em seguida, excluí-los.</span><span class="sxs-lookup"><span data-stu-id="dc83b-110">If you choose to take local snapshots, we recommend that you take fewer daily snapshots to back up the most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="dc83b-111">Quando você tira um instantâneo de nuvem de um volume fixado localmente, você copiar apenas os dados alterados para a nuvem, em que ocorrem sua eliminação de duplicação e sua compactação.</span><span class="sxs-lookup"><span data-stu-id="dc83b-111">When you take a cloud snapshot of a locally pinned volume, you copy only the changed data to the cloud, where it is deduplicated and compressed.</span></span> 

## <a name="the-backup-policies-page"></a><span data-ttu-id="dc83b-112">Página Políticas de Backup</span><span class="sxs-lookup"><span data-stu-id="dc83b-112">The Backup Policies page</span></span>
<span data-ttu-id="dc83b-113">A página **Políticas de Backup** permite gerenciar políticas de backup e agendar instantâneos de nuvem e local.</span><span class="sxs-lookup"><span data-stu-id="dc83b-113">The **Backup Policies** page allows you to manage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="dc83b-114">(As políticas de backup são usadas para configurar agendamentos e retenção de backup para um conjunto de volumes). Políticas de backup permitem tirar um instantâneo de vários volumes ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="dc83b-114">(Backup policies are used to configure backup schedules and backup retention for a collection of volumes.) Backup policies enable you to take a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="dc83b-115">Isso significa que os backups criados por uma política de backup serão cópias consistentes com falhas.</span><span class="sxs-lookup"><span data-stu-id="dc83b-115">This means that the backups created by a backup policy will be crash-consistent copies.</span></span> <span data-ttu-id="dc83b-116">A página **Políticas de Backup** lista as políticas de backup, seus tipos, os volumes associados, o número de backups retidos e a opção para habilitar essas políticas.</span><span class="sxs-lookup"><span data-stu-id="dc83b-116">The **Backup Policies** page lists the backup policies, their types, the associated volumes, the number of backups retained, and the option to enable these policies.</span></span>

<span data-ttu-id="dc83b-117">A página **Políticas de Backup** também permite filtrar as políticas de backup existentes por um ou mais dos seguintes campos:</span><span class="sxs-lookup"><span data-stu-id="dc83b-117">The **Backup Policies** page also allows you to filter the existing backup policies by one or more of the following fields:</span></span>

* <span data-ttu-id="dc83b-118">**Nome da política** – o nome associado à política.</span><span class="sxs-lookup"><span data-stu-id="dc83b-118">**Policy name** – The name associated with the policy.</span></span> <span data-ttu-id="dc83b-119">Os diferentes tipos de políticas incluem:</span><span class="sxs-lookup"><span data-stu-id="dc83b-119">The different types of policies include:</span></span>
  
  * <span data-ttu-id="dc83b-120">Políticas agendadas, que são criadas explicitamente pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="dc83b-120">Scheduled policies, which are explicitly created by the user.</span></span>
  * <span data-ttu-id="dc83b-121">Políticas automáticas, que são criadas quando o backup padrão para essa opção de volume foi habilitado no momento da criação do volume.</span><span class="sxs-lookup"><span data-stu-id="dc83b-121">Automatic policies, which are created when the default backup for this volume option was enabled at the time of volume creation.</span></span> <span data-ttu-id="dc83b-122">Essas políticas são nomeadas como *VolumeName*_Default, em que *VolumeName* refere-se ao nome do volume StorSimple configurado pelo usuário no Portal Clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="dc83b-122">These policies are named as *VolumeName*_Default where *VolumeName* refers to the name of the StorSimple volume configured by the user in the Azure classic portal.</span></span> <span data-ttu-id="dc83b-123">As políticas automáticas resultam em instantâneos diários de nuvem, começando na hora do dispositivo 22:30.</span><span class="sxs-lookup"><span data-stu-id="dc83b-123">The automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span></span>
  * <span data-ttu-id="dc83b-124">Políticas importadas, que foram originalmente criadas no Gerenciador de Instantâneos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="dc83b-124">Imported policies, which were originally created in the StorSimple Snapshot Manager.</span></span> <span data-ttu-id="dc83b-125">Elas têm uma marca que descreve o host do Gerenciador de Instantâneos do StorSimple do qual as políticas foram importadas.</span><span class="sxs-lookup"><span data-stu-id="dc83b-125">These have a tag that describes the StorSimple Snapshot Manager host that the policies were imported from.</span></span>
* <span data-ttu-id="dc83b-126">**Volumes** – os volumes associados à política.</span><span class="sxs-lookup"><span data-stu-id="dc83b-126">**Volumes** – The volumes associated with the policy.</span></span> <span data-ttu-id="dc83b-127">Todos os volumes associados a uma política de backup são agrupados quando os backups são criados.</span><span class="sxs-lookup"><span data-stu-id="dc83b-127">All the volumes associated with a backup policy are grouped together when backups are created.</span></span>
* <span data-ttu-id="dc83b-128">**Último backup bem-sucedido** – a data e hora do último backup bem-sucedido realizado com essa política.</span><span class="sxs-lookup"><span data-stu-id="dc83b-128">**Last successful backup** – The date and time of the last successful backup that was taken with this policy.</span></span>
* <span data-ttu-id="dc83b-129">**Próximo backup** – a data e hora do próximo backup agendado que será iniciado por essa política.</span><span class="sxs-lookup"><span data-stu-id="dc83b-129">**Next backup** – The date and time of the next scheduled backup that will be initiated by this policy.</span></span>
* <span data-ttu-id="dc83b-130">**Agendas** – o número de agendamentos associados à política de backup.</span><span class="sxs-lookup"><span data-stu-id="dc83b-130">**Schedules** – The number of schedules associated with the backup policy.</span></span>

<span data-ttu-id="dc83b-131">As operações usadas com frequência que podem ser executadas nessa página são:</span><span class="sxs-lookup"><span data-stu-id="dc83b-131">The frequently used operations that you can perform from this page are:</span></span>

* <span data-ttu-id="dc83b-132">Adicionar uma política de backup</span><span class="sxs-lookup"><span data-stu-id="dc83b-132">Add a backup policy</span></span> 
* <span data-ttu-id="dc83b-133">Adicionar ou modificar um agendamento</span><span class="sxs-lookup"><span data-stu-id="dc83b-133">Add or modify a schedule</span></span> 
* <span data-ttu-id="dc83b-134">Excluir uma política de backup</span><span class="sxs-lookup"><span data-stu-id="dc83b-134">Delete a backup policy</span></span> 
* <span data-ttu-id="dc83b-135">Fazer um backup manual</span><span class="sxs-lookup"><span data-stu-id="dc83b-135">Take a manual backup</span></span> 
* <span data-ttu-id="dc83b-136">Criar uma política de backup personalizada com vários volumes e agendamentos</span><span class="sxs-lookup"><span data-stu-id="dc83b-136">Create a custom backup policy with multiple volumes and schedules</span></span> 

## <a name="add-a-backup-policy"></a><span data-ttu-id="dc83b-137">Adicionar uma política de backup</span><span class="sxs-lookup"><span data-stu-id="dc83b-137">Add a backup policy</span></span>
<span data-ttu-id="dc83b-138">Adicione uma política de backup para agendar automaticamente seus backups.</span><span class="sxs-lookup"><span data-stu-id="dc83b-138">Add a backup policy to automatically schedule your backups.</span></span> <span data-ttu-id="dc83b-139">Execute as etapas a seguir no Portal clássico do Azure para adicionar uma política de backup ao seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="dc83b-139">Perform the following steps in the Azure classic portal to add a backup policy for your StorSimple device.</span></span> <span data-ttu-id="dc83b-140">Depois de adicionar a política, você poderá definir um agendamento (confira [Adicionar ou modificar um agendamento](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="dc83b-140">After you add the policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-add-backup-policy-u2](../../includes/storsimple-add-backup-policy-u2.md)]

<span data-ttu-id="dc83b-141">![Vídeo disponível](./media/storsimple-manage-backup-policies-u2/Video_icon.png) **Vídeo disponível**</span><span class="sxs-lookup"><span data-stu-id="dc83b-141">![Video available](./media/storsimple-manage-backup-policies-u2/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="dc83b-142">Para assistir a um vídeo que demonstra como criar um local ou a política de backup na nuvem, clique [aqui](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span><span class="sxs-lookup"><span data-stu-id="dc83b-142">To watch a video that demonstrates how to create a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span></span>

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="dc83b-143">Adicionar ou modificar um agendamento</span><span class="sxs-lookup"><span data-stu-id="dc83b-143">Add or modify a schedule</span></span>
<span data-ttu-id="dc83b-144">É possível adicionar ou modificar um agendamento que esteja anexado a uma política de backup existente no dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="dc83b-144">You can add or modify a schedule that is attached to an existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="dc83b-145">Execute as etapas a seguir no Portal clássico do Azure para adicionar ou modificar um agendamento.</span><span class="sxs-lookup"><span data-stu-id="dc83b-145">Perform the following steps in the Azure classic portal to add or modify a schedule.</span></span>

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule-u2.md)]

## <a name="delete-a-backup-policy"></a><span data-ttu-id="dc83b-146">Excluir uma política de backup</span><span class="sxs-lookup"><span data-stu-id="dc83b-146">Delete a backup policy</span></span>
<span data-ttu-id="dc83b-147">Execute as etapas a seguir no Portal clássico do Azure para excluir uma política de backup do seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="dc83b-147">Perform the following steps in the Azure classic portal to delete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="dc83b-148">Fazer um backup manual</span><span class="sxs-lookup"><span data-stu-id="dc83b-148">Take a manual backup</span></span>
<span data-ttu-id="dc83b-149">Execute as etapas a seguir no Portal clássico do Azure para criar um backup sob demanda (manual) para um único volume.</span><span class="sxs-lookup"><span data-stu-id="dc83b-149">Perform the following steps in the Azure classic portal to create an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a><span data-ttu-id="dc83b-150">Criar uma política de backup personalizada com vários volumes e agendamentos</span><span class="sxs-lookup"><span data-stu-id="dc83b-150">Create a custom backup policy with multiple volumes and schedules</span></span>
<span data-ttu-id="dc83b-151">Execute as etapas a seguir no Portal clássico do Azure para criar uma política de backup personalizada que tenha vários volumes e agendamentos.</span><span class="sxs-lookup"><span data-stu-id="dc83b-151">Perform the following steps in the Azure classic portal to create a custom backup policy that has multiple volumes and schedules.</span></span>

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy-u2.md)]

## <a name="next-steps"></a><span data-ttu-id="dc83b-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dc83b-152">Next steps</span></span>
<span data-ttu-id="dc83b-153">Saiba mais sobre o [uso do serviço StorSimple Manager para administrar seu dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="dc83b-153">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

