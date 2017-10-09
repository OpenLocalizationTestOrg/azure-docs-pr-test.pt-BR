---
title: "aaaManage suas políticas de backup StorSimple | Microsoft Docs"
description: "Explica como você pode usar toocreate de serviço do StorSimple Manager hello e gerenciar backups manuais, agendas de backup e retenção de backup."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: d1834bc8-d520-4463-82ae-3b32fabd021c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
ms.openlocfilehash: 710cbe54d14031b4de43e9da292ed169085d5af9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-backup-policies"></a><span data-ttu-id="94999-103">Usar políticas de backup do hello StorSimple Manager serviço toomanage</span><span class="sxs-lookup"><span data-stu-id="94999-103">Use hello StorSimple Manager service toomanage backup policies</span></span>
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a><span data-ttu-id="94999-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="94999-104">Overview</span></span>
<span data-ttu-id="94999-105">Este tutorial explica como toouse Olá serviço StorSimple Manager **políticas de Backup** página toocontrol processos de backup e retenção de backup para os volumes do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="94999-105">This tutorial explains how toouse hello StorSimple Manager service **Backup Policies** page toocontrol backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="94999-106">Ele também descreve como toocomplete um backup manual.</span><span class="sxs-lookup"><span data-stu-id="94999-106">It also describes how toocomplete a manual backup.</span></span>

<span data-ttu-id="94999-107">Olá **políticas de Backup** página permite que você toomanage as políticas de backup e agendamento locais e instantâneos em nuvem.</span><span class="sxs-lookup"><span data-stu-id="94999-107">hello **Backup Policies** page allows you toomanage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="94999-108">(As políticas de backup são usados tooconfigure agendas de backup e retenção de backup para um conjunto de volumes). Políticas de backup permitem que você tootake um instantâneo de vários volumes simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="94999-108">(Backup policies are used tooconfigure backup schedules and backup retention for a collection of volumes.) Backup policies enable you tootake a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="94999-109">Isso significa que os backups de saudação criados por uma política de backup será cópias consistente.</span><span class="sxs-lookup"><span data-stu-id="94999-109">This means that hello backups created by a backup policy will be crash-consistent copies.</span></span> <span data-ttu-id="94999-110">Esta página lista as políticas de backup hello, seus tipos, volumes Olá associado, número de saudação de backups retidos e Olá opção tooenable essas políticas.</span><span class="sxs-lookup"><span data-stu-id="94999-110">This page lists hello backup policies, their types, hello associated volumes, hello number of backups retained, and hello option tooenable these policies.</span></span>

<span data-ttu-id="94999-111">Olá **políticas de Backup** página também permite que você toofilter Olá políticas de backup existentes por uma ou mais Olá campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="94999-111">hello **Backup Policies** page also allows you toofilter hello existing backup policies by one or more of hello following fields:</span></span>

* <span data-ttu-id="94999-112">**Nome da política** – hello nome associado à política de saudação.</span><span class="sxs-lookup"><span data-stu-id="94999-112">**Policy name** – hello name associated with hello policy.</span></span> <span data-ttu-id="94999-113">Olá os tipos diferentes de políticas incluem:</span><span class="sxs-lookup"><span data-stu-id="94999-113">hello different types of policies include:</span></span>
  
  * <span data-ttu-id="94999-114">Políticas agendadas, que são criadas explicitamente pelo usuário hello.</span><span class="sxs-lookup"><span data-stu-id="94999-114">Scheduled policies, which are explicitly created by hello user.</span></span>
  * <span data-ttu-id="94999-115">Políticas automáticas, que são criadas quando o backup do saudação padrão para essa opção de volume foi habilitado no momento de saudação da criação de volume.</span><span class="sxs-lookup"><span data-stu-id="94999-115">Automatic policies, which are created when hello default backup for this volume option was enabled at hello time of volume creation.</span></span> <span data-ttu-id="94999-116">Essas políticas são chamadas de VolumeName_Default onde o nome do Volume refere-se nome toohello de saudação volume StorSimple configurado pelo usuário Olá Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="94999-116">These policies are named as VolumeName_Default where Volume name refers toohello name of hello StorSimple volume configured by hello user in hello Azure classic portal.</span></span> <span data-ttu-id="94999-117">políticas automáticas Olá resultam em instantâneos de nuvem diários, começando na hora do dispositivo 22:30.</span><span class="sxs-lookup"><span data-stu-id="94999-117">hello automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span></span>
  * <span data-ttu-id="94999-118">Políticas importadas, que foram criadas no hello StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="94999-118">Imported policies, which were originally created in hello StorSimple Snapshot Manager.</span></span> <span data-ttu-id="94999-119">Elas têm uma marca que descreve o host StorSimple Snapshot Manager Olá Olá políticas foram importadas do.</span><span class="sxs-lookup"><span data-stu-id="94999-119">These have a tag that describes hello StorSimple Snapshot Manager host that hello policies were imported from.</span></span>
* <span data-ttu-id="94999-120">**Volumes** – Olá volumes associados à política de saudação.</span><span class="sxs-lookup"><span data-stu-id="94999-120">**Volumes** – hello volumes associated with hello policy.</span></span> <span data-ttu-id="94999-121">Todos os volumes de saudação associados a uma política de backup são agrupados durante os backups são criados.</span><span class="sxs-lookup"><span data-stu-id="94999-121">All hello volumes associated with a backup policy are grouped together when backups are created.</span></span>
* <span data-ttu-id="94999-122">**Último backup bem-sucedido** – Olá data e hora do hello último backup bem-sucedido que foi feito com esta política.</span><span class="sxs-lookup"><span data-stu-id="94999-122">**Last successful backup** – hello date and time of hello last successful backup that was taken with this policy.</span></span>
* <span data-ttu-id="94999-123">**Próximo backup** – Olá data e hora do hello próximo backup agendado que será iniciado por essa política.</span><span class="sxs-lookup"><span data-stu-id="94999-123">**Next backup** – hello date and time of hello next scheduled backup that will be initiated by this policy.</span></span>
* <span data-ttu-id="94999-124">**Agendas** – Olá número de agendamentos associados à política de backup hello.</span><span class="sxs-lookup"><span data-stu-id="94999-124">**Schedules** – hello number of schedules associated with hello backup policy.</span></span>

<span data-ttu-id="94999-125">operações de saudação usada com frequência que você pode executar nessa página são:</span><span class="sxs-lookup"><span data-stu-id="94999-125">hello frequently used operations that you can perform from this page are:</span></span>

* <span data-ttu-id="94999-126">Adicionar uma política de backup</span><span class="sxs-lookup"><span data-stu-id="94999-126">Add a backup policy</span></span> 
* <span data-ttu-id="94999-127">Adicionar ou modificar um agendamento</span><span class="sxs-lookup"><span data-stu-id="94999-127">Add or modify a schedule</span></span> 
* <span data-ttu-id="94999-128">Excluir uma política de backup</span><span class="sxs-lookup"><span data-stu-id="94999-128">Delete a backup policy</span></span> 
* <span data-ttu-id="94999-129">Fazer um backup manual</span><span class="sxs-lookup"><span data-stu-id="94999-129">Take a manual backup</span></span> 
* <span data-ttu-id="94999-130">Criar uma política de backup personalizada com vários volumes e agendamentos</span><span class="sxs-lookup"><span data-stu-id="94999-130">Create a custom backup policy with multiple volumes and schedules</span></span> 

## <a name="add-a-backup-policy"></a><span data-ttu-id="94999-131">Adicionar uma política de backup</span><span class="sxs-lookup"><span data-stu-id="94999-131">Add a backup policy</span></span>
<span data-ttu-id="94999-132">Adicione uma agenda de tooautomatically de política de backup de seus backups.</span><span class="sxs-lookup"><span data-stu-id="94999-132">Add a backup policy tooautomatically schedule your backups.</span></span> <span data-ttu-id="94999-133">Execute Olá etapas Olá tooadd portal clássico do Azure uma política de backup para seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="94999-133">Perform hello following steps in hello Azure classic portal tooadd a backup policy for your StorSimple device.</span></span> <span data-ttu-id="94999-134">Depois de adicionar política hello, você pode definir uma agenda (consulte [adicionar ou modificar uma agenda](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="94999-134">After you add hello policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-add-backup-policy](../../includes/storsimple-add-backup-policy.md)]

<span data-ttu-id="94999-135">![Vídeo disponível](./media/storsimple-manage-backup-policies/Video_icon.png) **Vídeo disponível**</span><span class="sxs-lookup"><span data-stu-id="94999-135">![Video available](./media/storsimple-manage-backup-policies/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="94999-136">toowatch um vídeo que demonstra como toocreate local ou na nuvem de política de backup, clique em [aqui](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span><span class="sxs-lookup"><span data-stu-id="94999-136">toowatch a video that demonstrates how toocreate a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span></span>

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="94999-137">Adicionar ou modificar um agendamento</span><span class="sxs-lookup"><span data-stu-id="94999-137">Add or modify a schedule</span></span>
<span data-ttu-id="94999-138">Você pode adicionar ou modificar uma agenda que é anexado tooan política de backup existente em seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="94999-138">You can add or modify a schedule that is attached tooan existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="94999-139">Execute Olá etapas Olá tooadd de portal clássico do Azure ou modificar uma agenda.</span><span class="sxs-lookup"><span data-stu-id="94999-139">Perform hello following steps in hello Azure classic portal tooadd or modify a schedule.</span></span>

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule.md)]

## <a name="delete-a-backup-policy"></a><span data-ttu-id="94999-140">Excluir uma política de backup</span><span class="sxs-lookup"><span data-stu-id="94999-140">Delete a backup policy</span></span>
<span data-ttu-id="94999-141">Execute Olá seguindo as etapas em Olá toodelete portal clássico do Azure uma política de backup no dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="94999-141">Perform hello following steps in hello Azure classic portal toodelete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="94999-142">Fazer um backup manual</span><span class="sxs-lookup"><span data-stu-id="94999-142">Take a manual backup</span></span>
<span data-ttu-id="94999-143">Execute Olá seguindo as etapas no hello toocreate portal clássico do Azure uma demanda (manual) backup para um único volume.</span><span class="sxs-lookup"><span data-stu-id="94999-143">Perform hello following steps in hello Azure classic portal toocreate an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a><span data-ttu-id="94999-144">Criar uma política de backup personalizada com vários volumes e agendamentos</span><span class="sxs-lookup"><span data-stu-id="94999-144">Create a custom backup policy with multiple volumes and schedules</span></span>
<span data-ttu-id="94999-145">Execute Olá etapas Olá toocreate portal clássico do Azure uma política de backup personalizada que tem vários volumes e agendas.</span><span class="sxs-lookup"><span data-stu-id="94999-145">Perform hello following steps in hello Azure classic portal toocreate a custom backup policy that has multiple volumes and schedules.</span></span>

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy.md)]

## <a name="next-steps"></a><span data-ttu-id="94999-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="94999-146">Next steps</span></span>
<span data-ttu-id="94999-147">Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador do StorSimple em seu dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="94999-147">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

