---
title: "Gerenciar as políticas de backup do StorSimple da série 8000 | Microsoft Docs"
description: "Explica como você pode usar o serviço do Gerenciador de Dispositivos do StorSimple para criar e gerenciar backups manuais, agendas de backup e retenção de backup em um dispositivo StorSimple da série 8000."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 569dbfdeb7dcd526cb5a54b487ea1bfb59b13cc6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-in-azure-portal-to-manage-backup-policies"></a><span data-ttu-id="3dcf0-103">Usar o serviço do Gerenciador de Dispositivos do StorSimple no Portal do Azure para gerenciar políticas de backup</span><span class="sxs-lookup"><span data-stu-id="3dcf0-103">Use the StorSimple Device Manager service in Azure portal to manage backup policies</span></span>


## <a name="overview"></a><span data-ttu-id="3dcf0-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="3dcf0-104">Overview</span></span>

<span data-ttu-id="3dcf0-105">Este tutorial explica como usar a folha **Políticas de backup** do serviço do Gerenciador de Dispositivos do StorSimple para controlar os processos e a retenção de backup dos volumes do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-105">This tutorial explains how to use the StorSimple Device Manager service **Backup policy** blade to control backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="3dcf0-106">Ele também descreve como concluir um backup manual.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-106">It also describes how to complete a manual backup.</span></span>

<span data-ttu-id="3dcf0-107">Quando você faz backup de um volume, você pode escolher criar um instantâneo local ou um instantâneo de nuvem.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-107">When you back up a volume, you can choose to create a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="3dcf0-108">Se você estiver fazendo backup de um volume fixado localmente, é recomendável que você especifique um instantâneo de nuvem.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="3dcf0-109">Gravar um grande número de instantâneos locais de um volume fixado localmente juntamente com um conjunto de dados que tem muita variação resultará em uma situação em que você pode, rapidamente, ficar sem espaço local.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="3dcf0-110">Se você optar por tirar instantâneos locais, recomendamos que você menos instantâneos diários para fazer backup do estado mais recente, mantê-los por um dia e, em seguida, excluí-los.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-110">If you choose to take local snapshots, we recommend that you take fewer daily snapshots to back up the most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="3dcf0-111">Quando você tira um instantâneo de nuvem de um volume fixado localmente, você copiar apenas os dados alterados para a nuvem, em que ocorrem sua eliminação de duplicação e sua compactação.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-111">When you take a cloud snapshot of a locally pinned volume, you copy only the changed data to the cloud, where it is deduplicated and compressed.</span></span>

## <a name="the-backup-policy-blade"></a><span data-ttu-id="3dcf0-112">A folha Política de backup</span><span class="sxs-lookup"><span data-stu-id="3dcf0-112">The Backup policy blade</span></span>

<span data-ttu-id="3dcf0-113">A folha **Política de backup** do dispositivo StorSimple permite gerenciar políticas de backup e agendar instantâneos locais e de nuvem.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-113">The **Backup policy** blade for your StorSimple device allows you to manage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="3dcf0-114">As políticas de backup são usadas para configurar agendamentos e retenção de backup para uma coleção de volumes.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-114">Backup policies are used to configure backup schedules and backup retention for a collection of volumes.</span></span> <span data-ttu-id="3dcf0-115">Políticas de backup permitem tirar um instantâneo de vários volumes ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-115">Backup policies enable you to take a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="3dcf0-116">Isso significa que os backups criados por uma política de backup serão cópias consistentes com falhas.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-116">This means that the backups created by a backup policy will be crash-consistent copies.</span></span>

<span data-ttu-id="3dcf0-117">A listagem tabular das políticas de backup também permite filtrar as políticas de backup existentes por um ou mais dos seguintes campos:</span><span class="sxs-lookup"><span data-stu-id="3dcf0-117">The backup policies tabular listing also allows you to filter the existing backup policies by one or more of the following fields:</span></span>

* <span data-ttu-id="3dcf0-118">**Nome da política** – o nome associado à política.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-118">**Policy name** – The name associated with the policy.</span></span> <span data-ttu-id="3dcf0-119">Os diferentes tipos de políticas incluem:</span><span class="sxs-lookup"><span data-stu-id="3dcf0-119">The different types of policies include:</span></span>

  * <span data-ttu-id="3dcf0-120">Políticas agendadas, que são criadas explicitamente pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-120">Scheduled policies, which are explicitly created by the user.</span></span>
  * <span data-ttu-id="3dcf0-121">Políticas importadas, que foram originalmente criadas no Gerenciador de Instantâneos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-121">Imported policies, which were originally created in the StorSimple Snapshot Manager.</span></span> <span data-ttu-id="3dcf0-122">Elas têm uma marca que descreve o host do Gerenciador de Instantâneos do StorSimple do qual as políticas foram importadas.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-122">These have a tag that describes the StorSimple Snapshot Manager host that the policies were imported from.</span></span>

  > [!NOTE]
  > <span data-ttu-id="3dcf0-123">Políticas de backup automáticas ou padrão não estão mais habilitadas no momento da criação do volume.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-123">Automatic or default backup policies are no longer enabled at the time of volume creation.</span></span>

* <span data-ttu-id="3dcf0-124">**Último backup bem-sucedido** – a data e hora do último backup bem-sucedido realizado com essa política.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-124">**Last successful backup** – The date and time of the last successful backup that was taken with this policy.</span></span>

* <span data-ttu-id="3dcf0-125">**Próximo backup** – a data e hora do próximo backup agendado que será iniciado por essa política.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-125">**Next backup** – The date and time of the next scheduled backup that will be initiated by this policy.</span></span>

* <span data-ttu-id="3dcf0-126">**Volumes** – os volumes associados à política.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-126">**Volumes** – The volumes associated with the policy.</span></span> <span data-ttu-id="3dcf0-127">Todos os volumes associados a uma política de backup são agrupados quando os backups são criados.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-127">All the volumes associated with a backup policy are grouped together when backups are created.</span></span>

* <span data-ttu-id="3dcf0-128">**Agendas** – o número de agendamentos associados à política de backup.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-128">**Schedules** – The number of schedules associated with the backup policy.</span></span>

<span data-ttu-id="3dcf0-129">As operações usadas com frequência que podem ser executadas nas políticas de backup são:</span><span class="sxs-lookup"><span data-stu-id="3dcf0-129">The frequently used operations that you can perform for backup policies are:</span></span>

* <span data-ttu-id="3dcf0-130">Adicionar uma política de backup</span><span class="sxs-lookup"><span data-stu-id="3dcf0-130">Add a backup policy</span></span>
* <span data-ttu-id="3dcf0-131">Adicionar ou modificar um agendamento</span><span class="sxs-lookup"><span data-stu-id="3dcf0-131">Add or modify a schedule</span></span>
* <span data-ttu-id="3dcf0-132">Adicionar ou remover um volume</span><span class="sxs-lookup"><span data-stu-id="3dcf0-132">Add or remove a volume</span></span>
* <span data-ttu-id="3dcf0-133">Excluir uma política de backup</span><span class="sxs-lookup"><span data-stu-id="3dcf0-133">Delete a backup policy</span></span>
* <span data-ttu-id="3dcf0-134">Fazer um backup manual</span><span class="sxs-lookup"><span data-stu-id="3dcf0-134">Take a manual backup</span></span>

## <a name="add-a-backup-policy"></a><span data-ttu-id="3dcf0-135">Adicionar uma política de backup</span><span class="sxs-lookup"><span data-stu-id="3dcf0-135">Add a backup policy</span></span>

<span data-ttu-id="3dcf0-136">Adicione uma política de backup para agendar automaticamente seus backups.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-136">Add a backup policy to automatically schedule your backups.</span></span> <span data-ttu-id="3dcf0-137">Quando você cria um volume pela primeira vez, nenhuma política de backup padrão é associada a ele.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-137">When you first create a volume, there is no default backup policy associated with your volume.</span></span> <span data-ttu-id="3dcf0-138">Você precisa adicionar e atribuir uma política de backup para proteger os dados do volume.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-138">You need to add and assign a backup policy to protect volume data.</span></span>

<span data-ttu-id="3dcf0-139">Execute as etapas a seguir no Portal do Azure para adicionar uma política de backup ao dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-139">Perform the following steps in the Azure portal to add a backup policy for your StorSimple device.</span></span> <span data-ttu-id="3dcf0-140">Depois de adicionar a política, você poderá definir um agendamento (confira [Adicionar ou modificar um agendamento](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="3dcf0-140">After you add the policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-8000-add-backup-policy-u2](../../includes/storsimple-8000-add-backup-policy-u2.md)]

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="3dcf0-141">Adicionar ou modificar um agendamento</span><span class="sxs-lookup"><span data-stu-id="3dcf0-141">Add or modify a schedule</span></span>

<span data-ttu-id="3dcf0-142">É possível adicionar ou modificar um agendamento que esteja anexado a uma política de backup existente no dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-142">You can add or modify a schedule that is attached to an existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="3dcf0-143">Execute as etapas a seguir no Portal do Azure para adicionar ou modificar um agendamento.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-143">Perform the following steps in the Azure portal to add or modify a schedule.</span></span>

[!INCLUDE [storsimple-8000-add-modify-backup-schedule](../../includes/storsimple-8000-add-modify-backup-schedule-u2.md)]


## <a name="add-or-remove-a-volume"></a><span data-ttu-id="3dcf0-144">Adicionar ou remover um volume</span><span class="sxs-lookup"><span data-stu-id="3dcf0-144">Add or remove a volume</span></span>

<span data-ttu-id="3dcf0-145">Você pode adicionar ou remover um volume atribuído a uma política de backup no dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-145">You can add or remove a volume assigned to a backup policy on your StorSimple device.</span></span> <span data-ttu-id="3dcf0-146">Execute as etapas a seguir no Portal do Azure para adicionar ou remover um volume.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-146">Perform the following steps in the Azure portal to add or remove a volume.</span></span>

[!INCLUDE [storsimple-8000-add-volume-backup-policy-u2](../../includes/storsimple-8000-add-remove-volume-backup-policy-u2.md)]


## <a name="delete-a-backup-policy"></a><span data-ttu-id="3dcf0-147">Excluir uma política de backup</span><span class="sxs-lookup"><span data-stu-id="3dcf0-147">Delete a backup policy</span></span>

<span data-ttu-id="3dcf0-148">Execute as etapas a seguir no Portal do Azure para excluir uma política de backup do dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-148">Perform the following steps in the Azure portal to delete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-8000-delete-backup-policy](../../includes/storsimple-8000-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="3dcf0-149">Fazer um backup manual</span><span class="sxs-lookup"><span data-stu-id="3dcf0-149">Take a manual backup</span></span>

<span data-ttu-id="3dcf0-150">Execute as etapas a seguir no Portal do Azure para criar um backup sob demanda (manual) para um único volume.</span><span class="sxs-lookup"><span data-stu-id="3dcf0-150">Perform the following steps in the Azure portal to create an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-8000-create-manual-backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a><span data-ttu-id="3dcf0-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3dcf0-151">Next steps</span></span>

<span data-ttu-id="3dcf0-152">Saiba mais sobre como [usar o serviço Gerenciador de Dispositivos do StorSimple para administrar o dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="3dcf0-152">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

