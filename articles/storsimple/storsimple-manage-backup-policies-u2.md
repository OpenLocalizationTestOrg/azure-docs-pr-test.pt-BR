---
title: "aaaManage suas políticas de backup StorSimple | Microsoft Docs"
description: "Explica como você pode usar toocreate de serviço do StorSimple Manager hello e gerenciar backups manuais, agendas de backup e retenção de backup."
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
ms.openlocfilehash: 7b01f29a8d8a096d9890c8406557021317b9baff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-backup-policies-update-2"></a><span data-ttu-id="1fd09-103">Usar políticas de backup toomanage (atualização 2) de serviço de Gerenciador de StorSimple Olá</span><span class="sxs-lookup"><span data-stu-id="1fd09-103">Use hello StorSimple Manager service toomanage backup policies (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a><span data-ttu-id="1fd09-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="1fd09-104">Overview</span></span>
<span data-ttu-id="1fd09-105">Este tutorial explica como toouse Olá serviço StorSimple Manager **políticas de Backup** página toocontrol processos de backup e retenção de backup para os volumes do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1fd09-105">This tutorial explains how toouse hello StorSimple Manager service **Backup Policies** page toocontrol backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="1fd09-106">Ele também descreve como toocomplete um backup manual.</span><span class="sxs-lookup"><span data-stu-id="1fd09-106">It also describes how toocomplete a manual backup.</span></span>

<span data-ttu-id="1fd09-107">Quando você faz backup de um volume, você pode escolher toocreate um instantâneo local ou um instantâneo na nuvem.</span><span class="sxs-lookup"><span data-stu-id="1fd09-107">When you back up a volume, you can choose toocreate a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="1fd09-108">Se você estiver fazendo backup de um volume fixado localmente, é recomendável que você especifique um instantâneo de nuvem.</span><span class="sxs-lookup"><span data-stu-id="1fd09-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="1fd09-109">Gravar um grande número de instantâneos locais de um volume fixado localmente juntamente com um conjunto de dados que tem muita variação resultará em uma situação em que você pode, rapidamente, ficar sem espaço local.</span><span class="sxs-lookup"><span data-stu-id="1fd09-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="1fd09-110">Se você escolher tootake instantâneos locais, é recomendável levar menos tooback instantâneos diários estado mais recente Olá mantê-los por dia e, em seguida, excluí-los.</span><span class="sxs-lookup"><span data-stu-id="1fd09-110">If you choose tootake local snapshots, we recommend that you take fewer daily snapshots tooback up hello most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="1fd09-111">Quando você usa um instantâneo de nuvem de um volume localmente afixado, você copiar somente Olá alterado dados toohello na nuvem, onde é eliminação de duplicação e compactado.</span><span class="sxs-lookup"><span data-stu-id="1fd09-111">When you take a cloud snapshot of a locally pinned volume, you copy only hello changed data toohello cloud, where it is deduplicated and compressed.</span></span> 

## <a name="hello-backup-policies-page"></a><span data-ttu-id="1fd09-112">página de políticas de Backup Olá</span><span class="sxs-lookup"><span data-stu-id="1fd09-112">hello Backup Policies page</span></span>
<span data-ttu-id="1fd09-113">Olá **políticas de Backup** página permite que você toomanage as políticas de backup e agendamento locais e instantâneos em nuvem.</span><span class="sxs-lookup"><span data-stu-id="1fd09-113">hello **Backup Policies** page allows you toomanage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="1fd09-114">(As políticas de backup são usados tooconfigure agendas de backup e retenção de backup para um conjunto de volumes). Políticas de backup permitem que você tootake um instantâneo de vários volumes simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="1fd09-114">(Backup policies are used tooconfigure backup schedules and backup retention for a collection of volumes.) Backup policies enable you tootake a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="1fd09-115">Isso significa que os backups de saudação criados por uma política de backup será cópias consistente.</span><span class="sxs-lookup"><span data-stu-id="1fd09-115">This means that hello backups created by a backup policy will be crash-consistent copies.</span></span> <span data-ttu-id="1fd09-116">Olá **políticas de Backup** página lista as políticas de backup hello, seus tipos, volumes Olá associado, número de Olá de backups retidos e Olá opção tooenable essas políticas.</span><span class="sxs-lookup"><span data-stu-id="1fd09-116">hello **Backup Policies** page lists hello backup policies, their types, hello associated volumes, hello number of backups retained, and hello option tooenable these policies.</span></span>

<span data-ttu-id="1fd09-117">Olá **políticas de Backup** página também permite que você toofilter Olá políticas de backup existentes por uma ou mais Olá campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="1fd09-117">hello **Backup Policies** page also allows you toofilter hello existing backup policies by one or more of hello following fields:</span></span>

* <span data-ttu-id="1fd09-118">**Nome da política** – hello nome associado à política de saudação.</span><span class="sxs-lookup"><span data-stu-id="1fd09-118">**Policy name** – hello name associated with hello policy.</span></span> <span data-ttu-id="1fd09-119">Olá os tipos diferentes de políticas incluem:</span><span class="sxs-lookup"><span data-stu-id="1fd09-119">hello different types of policies include:</span></span>
  
  * <span data-ttu-id="1fd09-120">Políticas agendadas, que são criadas explicitamente pelo usuário hello.</span><span class="sxs-lookup"><span data-stu-id="1fd09-120">Scheduled policies, which are explicitly created by hello user.</span></span>
  * <span data-ttu-id="1fd09-121">Políticas automáticas, que são criadas quando o backup do saudação padrão para essa opção de volume foi habilitado no momento de saudação da criação de volume.</span><span class="sxs-lookup"><span data-stu-id="1fd09-121">Automatic policies, which are created when hello default backup for this volume option was enabled at hello time of volume creation.</span></span> <span data-ttu-id="1fd09-122">Essas políticas são denominadas *VolumeName*default onde *VolumeName* refere-se o nome de toohello de saudação volume StorSimple configurado pelo usuário Olá Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="1fd09-122">These policies are named as *VolumeName*_Default where *VolumeName* refers toohello name of hello StorSimple volume configured by hello user in hello Azure classic portal.</span></span> <span data-ttu-id="1fd09-123">políticas automáticas Olá resultam em instantâneos de nuvem diários, começando na hora do dispositivo 22:30.</span><span class="sxs-lookup"><span data-stu-id="1fd09-123">hello automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span></span>
  * <span data-ttu-id="1fd09-124">Políticas importadas, que foram criadas no hello StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="1fd09-124">Imported policies, which were originally created in hello StorSimple Snapshot Manager.</span></span> <span data-ttu-id="1fd09-125">Elas têm uma marca que descreve o host StorSimple Snapshot Manager Olá Olá políticas foram importadas do.</span><span class="sxs-lookup"><span data-stu-id="1fd09-125">These have a tag that describes hello StorSimple Snapshot Manager host that hello policies were imported from.</span></span>
* <span data-ttu-id="1fd09-126">**Volumes** – Olá volumes associados à política de saudação.</span><span class="sxs-lookup"><span data-stu-id="1fd09-126">**Volumes** – hello volumes associated with hello policy.</span></span> <span data-ttu-id="1fd09-127">Todos os volumes de saudação associados a uma política de backup são agrupados durante os backups são criados.</span><span class="sxs-lookup"><span data-stu-id="1fd09-127">All hello volumes associated with a backup policy are grouped together when backups are created.</span></span>
* <span data-ttu-id="1fd09-128">**Último backup bem-sucedido** – Olá data e hora do hello último backup bem-sucedido que foi feito com esta política.</span><span class="sxs-lookup"><span data-stu-id="1fd09-128">**Last successful backup** – hello date and time of hello last successful backup that was taken with this policy.</span></span>
* <span data-ttu-id="1fd09-129">**Próximo backup** – Olá data e hora do hello próximo backup agendado que será iniciado por essa política.</span><span class="sxs-lookup"><span data-stu-id="1fd09-129">**Next backup** – hello date and time of hello next scheduled backup that will be initiated by this policy.</span></span>
* <span data-ttu-id="1fd09-130">**Agendas** – Olá número de agendamentos associados à política de backup hello.</span><span class="sxs-lookup"><span data-stu-id="1fd09-130">**Schedules** – hello number of schedules associated with hello backup policy.</span></span>

<span data-ttu-id="1fd09-131">operações de saudação usada com frequência que você pode executar nessa página são:</span><span class="sxs-lookup"><span data-stu-id="1fd09-131">hello frequently used operations that you can perform from this page are:</span></span>

* <span data-ttu-id="1fd09-132">Adicionar uma política de backup</span><span class="sxs-lookup"><span data-stu-id="1fd09-132">Add a backup policy</span></span> 
* <span data-ttu-id="1fd09-133">Adicionar ou modificar um agendamento</span><span class="sxs-lookup"><span data-stu-id="1fd09-133">Add or modify a schedule</span></span> 
* <span data-ttu-id="1fd09-134">Excluir uma política de backup</span><span class="sxs-lookup"><span data-stu-id="1fd09-134">Delete a backup policy</span></span> 
* <span data-ttu-id="1fd09-135">Fazer um backup manual</span><span class="sxs-lookup"><span data-stu-id="1fd09-135">Take a manual backup</span></span> 
* <span data-ttu-id="1fd09-136">Criar uma política de backup personalizada com vários volumes e agendamentos</span><span class="sxs-lookup"><span data-stu-id="1fd09-136">Create a custom backup policy with multiple volumes and schedules</span></span> 

## <a name="add-a-backup-policy"></a><span data-ttu-id="1fd09-137">Adicionar uma política de backup</span><span class="sxs-lookup"><span data-stu-id="1fd09-137">Add a backup policy</span></span>
<span data-ttu-id="1fd09-138">Adicione uma agenda de tooautomatically de política de backup de seus backups.</span><span class="sxs-lookup"><span data-stu-id="1fd09-138">Add a backup policy tooautomatically schedule your backups.</span></span> <span data-ttu-id="1fd09-139">Execute Olá etapas Olá tooadd portal clássico do Azure uma política de backup para seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1fd09-139">Perform hello following steps in hello Azure classic portal tooadd a backup policy for your StorSimple device.</span></span> <span data-ttu-id="1fd09-140">Depois de adicionar política hello, você pode definir uma agenda (consulte [adicionar ou modificar uma agenda](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="1fd09-140">After you add hello policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-add-backup-policy-u2](../../includes/storsimple-add-backup-policy-u2.md)]

<span data-ttu-id="1fd09-141">![Vídeo disponível](./media/storsimple-manage-backup-policies-u2/Video_icon.png) **Vídeo disponível**</span><span class="sxs-lookup"><span data-stu-id="1fd09-141">![Video available](./media/storsimple-manage-backup-policies-u2/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="1fd09-142">toowatch um vídeo que demonstra como toocreate local ou na nuvem de política de backup, clique em [aqui](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span><span class="sxs-lookup"><span data-stu-id="1fd09-142">toowatch a video that demonstrates how toocreate a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span></span>

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="1fd09-143">Adicionar ou modificar um agendamento</span><span class="sxs-lookup"><span data-stu-id="1fd09-143">Add or modify a schedule</span></span>
<span data-ttu-id="1fd09-144">Você pode adicionar ou modificar uma agenda que é anexado tooan política de backup existente em seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1fd09-144">You can add or modify a schedule that is attached tooan existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="1fd09-145">Execute Olá etapas Olá tooadd de portal clássico do Azure ou modificar uma agenda.</span><span class="sxs-lookup"><span data-stu-id="1fd09-145">Perform hello following steps in hello Azure classic portal tooadd or modify a schedule.</span></span>

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule-u2.md)]

## <a name="delete-a-backup-policy"></a><span data-ttu-id="1fd09-146">Excluir uma política de backup</span><span class="sxs-lookup"><span data-stu-id="1fd09-146">Delete a backup policy</span></span>
<span data-ttu-id="1fd09-147">Execute Olá seguindo as etapas em Olá toodelete portal clássico do Azure uma política de backup no dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1fd09-147">Perform hello following steps in hello Azure classic portal toodelete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="1fd09-148">Fazer um backup manual</span><span class="sxs-lookup"><span data-stu-id="1fd09-148">Take a manual backup</span></span>
<span data-ttu-id="1fd09-149">Execute Olá seguindo as etapas no hello toocreate portal clássico do Azure uma demanda (manual) backup para um único volume.</span><span class="sxs-lookup"><span data-stu-id="1fd09-149">Perform hello following steps in hello Azure classic portal toocreate an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a><span data-ttu-id="1fd09-150">Criar uma política de backup personalizada com vários volumes e agendamentos</span><span class="sxs-lookup"><span data-stu-id="1fd09-150">Create a custom backup policy with multiple volumes and schedules</span></span>
<span data-ttu-id="1fd09-151">Execute Olá etapas Olá toocreate portal clássico do Azure uma política de backup personalizada que tem vários volumes e agendas.</span><span class="sxs-lookup"><span data-stu-id="1fd09-151">Perform hello following steps in hello Azure classic portal toocreate a custom backup policy that has multiple volumes and schedules.</span></span>

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy-u2.md)]

## <a name="next-steps"></a><span data-ttu-id="1fd09-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1fd09-152">Next steps</span></span>
<span data-ttu-id="1fd09-153">Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador do StorSimple em seu dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="1fd09-153">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

