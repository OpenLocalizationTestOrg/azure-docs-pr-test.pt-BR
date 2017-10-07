---
title: "as políticas de backup aaaManage StorSimple 8000 series | Microsoft Docs"
description: "Explica como você pode usar toocreate de serviço do Gerenciador de dispositivos de StorSimple hello e gerenciar backups manuais, agendas de backup e retenção de backup em um dispositivo da série StorSimple 8000."
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
ms.openlocfilehash: 7c56365abb6ba69d02008829ca6ae703d4632705
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-toomanage-backup-policies"></a><span data-ttu-id="4a779-103">Usar serviço de Gerenciador de dispositivos de StorSimple Olá nas políticas de backup toomanage portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4a779-103">Use hello StorSimple Device Manager service in Azure portal toomanage backup policies</span></span>


## <a name="overview"></a><span data-ttu-id="4a779-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="4a779-104">Overview</span></span>

<span data-ttu-id="4a779-105">Este tutorial explica como toouse Olá serviço do Gerenciador de dispositivos de StorSimple **política de Backup** processos de backup de toocontrol de folha e retenção de backup para os volumes do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4a779-105">This tutorial explains how toouse hello StorSimple Device Manager service **Backup policy** blade toocontrol backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="4a779-106">Ele também descreve como toocomplete um backup manual.</span><span class="sxs-lookup"><span data-stu-id="4a779-106">It also describes how toocomplete a manual backup.</span></span>

<span data-ttu-id="4a779-107">Quando você faz backup de um volume, você pode escolher toocreate um instantâneo local ou um instantâneo na nuvem.</span><span class="sxs-lookup"><span data-stu-id="4a779-107">When you back up a volume, you can choose toocreate a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="4a779-108">Se você estiver fazendo backup de um volume fixado localmente, é recomendável que você especifique um instantâneo de nuvem.</span><span class="sxs-lookup"><span data-stu-id="4a779-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="4a779-109">Gravar um grande número de instantâneos locais de um volume fixado localmente juntamente com um conjunto de dados que tem muita variação resultará em uma situação em que você pode, rapidamente, ficar sem espaço local.</span><span class="sxs-lookup"><span data-stu-id="4a779-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="4a779-110">Se você escolher tootake instantâneos locais, é recomendável levar menos tooback instantâneos diários estado mais recente Olá mantê-los por dia e, em seguida, excluí-los.</span><span class="sxs-lookup"><span data-stu-id="4a779-110">If you choose tootake local snapshots, we recommend that you take fewer daily snapshots tooback up hello most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="4a779-111">Quando você usa um instantâneo de nuvem de um volume localmente afixado, você copiar somente Olá alterado dados toohello na nuvem, onde é eliminação de duplicação e compactado.</span><span class="sxs-lookup"><span data-stu-id="4a779-111">When you take a cloud snapshot of a locally pinned volume, you copy only hello changed data toohello cloud, where it is deduplicated and compressed.</span></span>

## <a name="hello-backup-policy-blade"></a><span data-ttu-id="4a779-112">folha de política de Backup Olá</span><span class="sxs-lookup"><span data-stu-id="4a779-112">hello Backup policy blade</span></span>

<span data-ttu-id="4a779-113">Olá **política de Backup** folha para seu dispositivo StorSimple permite que você toomanage as políticas de backup e agendamento locais e instantâneos em nuvem.</span><span class="sxs-lookup"><span data-stu-id="4a779-113">hello **Backup policy** blade for your StorSimple device allows you toomanage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="4a779-114">Políticas de backup são usados tooconfigure agendas de backup e retenção de backup para um conjunto de volumes.</span><span class="sxs-lookup"><span data-stu-id="4a779-114">Backup policies are used tooconfigure backup schedules and backup retention for a collection of volumes.</span></span> <span data-ttu-id="4a779-115">Políticas de backup permitem que você tootake um instantâneo de vários volumes simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="4a779-115">Backup policies enable you tootake a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="4a779-116">Isso significa que os backups de saudação criados por uma política de backup será cópias consistente.</span><span class="sxs-lookup"><span data-stu-id="4a779-116">This means that hello backups created by a backup policy will be crash-consistent copies.</span></span>

<span data-ttu-id="4a779-117">listagem tabular de políticas de backup Olá também permite que você toofilter Olá políticas de backup existentes por uma ou mais Olá campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4a779-117">hello backup policies tabular listing also allows you toofilter hello existing backup policies by one or more of hello following fields:</span></span>

* <span data-ttu-id="4a779-118">**Nome da política** – hello nome associado à política de saudação.</span><span class="sxs-lookup"><span data-stu-id="4a779-118">**Policy name** – hello name associated with hello policy.</span></span> <span data-ttu-id="4a779-119">Olá os tipos diferentes de políticas incluem:</span><span class="sxs-lookup"><span data-stu-id="4a779-119">hello different types of policies include:</span></span>

  * <span data-ttu-id="4a779-120">Políticas agendadas, que são criadas explicitamente pelo usuário hello.</span><span class="sxs-lookup"><span data-stu-id="4a779-120">Scheduled policies, which are explicitly created by hello user.</span></span>
  * <span data-ttu-id="4a779-121">Políticas importadas, que foram criadas no hello StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="4a779-121">Imported policies, which were originally created in hello StorSimple Snapshot Manager.</span></span> <span data-ttu-id="4a779-122">Elas têm uma marca que descreve o host StorSimple Snapshot Manager Olá Olá políticas foram importadas do.</span><span class="sxs-lookup"><span data-stu-id="4a779-122">These have a tag that describes hello StorSimple Snapshot Manager host that hello policies were imported from.</span></span>

  > [!NOTE]
  > <span data-ttu-id="4a779-123">Políticas de backup automático ou padrão não estão mais habilitadas no momento de saudação da criação de volume.</span><span class="sxs-lookup"><span data-stu-id="4a779-123">Automatic or default backup policies are no longer enabled at hello time of volume creation.</span></span>

* <span data-ttu-id="4a779-124">**Último backup bem-sucedido** – Olá data e hora do hello último backup bem-sucedido que foi feito com esta política.</span><span class="sxs-lookup"><span data-stu-id="4a779-124">**Last successful backup** – hello date and time of hello last successful backup that was taken with this policy.</span></span>

* <span data-ttu-id="4a779-125">**Próximo backup** – Olá data e hora do hello próximo backup agendado que será iniciado por essa política.</span><span class="sxs-lookup"><span data-stu-id="4a779-125">**Next backup** – hello date and time of hello next scheduled backup that will be initiated by this policy.</span></span>

* <span data-ttu-id="4a779-126">**Volumes** – Olá volumes associados à política de saudação.</span><span class="sxs-lookup"><span data-stu-id="4a779-126">**Volumes** – hello volumes associated with hello policy.</span></span> <span data-ttu-id="4a779-127">Todos os volumes de saudação associados a uma política de backup são agrupados durante os backups são criados.</span><span class="sxs-lookup"><span data-stu-id="4a779-127">All hello volumes associated with a backup policy are grouped together when backups are created.</span></span>

* <span data-ttu-id="4a779-128">**Agendas** – Olá número de agendamentos associados à política de backup hello.</span><span class="sxs-lookup"><span data-stu-id="4a779-128">**Schedules** – hello number of schedules associated with hello backup policy.</span></span>

<span data-ttu-id="4a779-129">operações de Olá usado com frequência que você pode executar para políticas de backup são:</span><span class="sxs-lookup"><span data-stu-id="4a779-129">hello frequently used operations that you can perform for backup policies are:</span></span>

* <span data-ttu-id="4a779-130">Adicionar uma política de backup</span><span class="sxs-lookup"><span data-stu-id="4a779-130">Add a backup policy</span></span>
* <span data-ttu-id="4a779-131">Adicionar ou modificar um agendamento</span><span class="sxs-lookup"><span data-stu-id="4a779-131">Add or modify a schedule</span></span>
* <span data-ttu-id="4a779-132">Adicionar ou remover um volume</span><span class="sxs-lookup"><span data-stu-id="4a779-132">Add or remove a volume</span></span>
* <span data-ttu-id="4a779-133">Excluir uma política de backup</span><span class="sxs-lookup"><span data-stu-id="4a779-133">Delete a backup policy</span></span>
* <span data-ttu-id="4a779-134">Fazer um backup manual</span><span class="sxs-lookup"><span data-stu-id="4a779-134">Take a manual backup</span></span>

## <a name="add-a-backup-policy"></a><span data-ttu-id="4a779-135">Adicionar uma política de backup</span><span class="sxs-lookup"><span data-stu-id="4a779-135">Add a backup policy</span></span>

<span data-ttu-id="4a779-136">Adicione uma agenda de tooautomatically de política de backup de seus backups.</span><span class="sxs-lookup"><span data-stu-id="4a779-136">Add a backup policy tooautomatically schedule your backups.</span></span> <span data-ttu-id="4a779-137">Quando você cria um volume pela primeira vez, nenhuma política de backup padrão é associada a ele.</span><span class="sxs-lookup"><span data-stu-id="4a779-137">When you first create a volume, there is no default backup policy associated with your volume.</span></span> <span data-ttu-id="4a779-138">Você precisa tooadd e atribuir um política de backup tooprotect volume de dados.</span><span class="sxs-lookup"><span data-stu-id="4a779-138">You need tooadd and assign a backup policy tooprotect volume data.</span></span>

<span data-ttu-id="4a779-139">Execute Olá etapas Olá tooadd portal do Azure uma política de backup para seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4a779-139">Perform hello following steps in hello Azure portal tooadd a backup policy for your StorSimple device.</span></span> <span data-ttu-id="4a779-140">Depois de adicionar política hello, você pode definir uma agenda (consulte [adicionar ou modificar uma agenda](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="4a779-140">After you add hello policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-8000-add-backup-policy-u2](../../includes/storsimple-8000-add-backup-policy-u2.md)]

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="4a779-141">Adicionar ou modificar um agendamento</span><span class="sxs-lookup"><span data-stu-id="4a779-141">Add or modify a schedule</span></span>

<span data-ttu-id="4a779-142">Você pode adicionar ou modificar uma agenda que é anexado tooan política de backup existente em seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4a779-142">You can add or modify a schedule that is attached tooan existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="4a779-143">Execute Olá etapas Olá tooadd portal do Azure ou modificar uma agenda.</span><span class="sxs-lookup"><span data-stu-id="4a779-143">Perform hello following steps in hello Azure portal tooadd or modify a schedule.</span></span>

[!INCLUDE [storsimple-8000-add-modify-backup-schedule](../../includes/storsimple-8000-add-modify-backup-schedule-u2.md)]


## <a name="add-or-remove-a-volume"></a><span data-ttu-id="4a779-144">Adicionar ou remover um volume</span><span class="sxs-lookup"><span data-stu-id="4a779-144">Add or remove a volume</span></span>

<span data-ttu-id="4a779-145">Você pode adicionar ou remover um volume atribuído tooa política de backup no dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4a779-145">You can add or remove a volume assigned tooa backup policy on your StorSimple device.</span></span> <span data-ttu-id="4a779-146">Executar Olá etapas Olá tooadd portal do Azure ou remover um volume.</span><span class="sxs-lookup"><span data-stu-id="4a779-146">Perform hello following steps in hello Azure portal tooadd or remove a volume.</span></span>

[!INCLUDE [storsimple-8000-add-volume-backup-policy-u2](../../includes/storsimple-8000-add-remove-volume-backup-policy-u2.md)]


## <a name="delete-a-backup-policy"></a><span data-ttu-id="4a779-147">Excluir uma política de backup</span><span class="sxs-lookup"><span data-stu-id="4a779-147">Delete a backup policy</span></span>

<span data-ttu-id="4a779-148">Execute Olá seguindo as etapas em Olá toodelete portal do Azure uma política de backup no dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4a779-148">Perform hello following steps in hello Azure portal toodelete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-8000-delete-backup-policy](../../includes/storsimple-8000-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="4a779-149">Fazer um backup manual</span><span class="sxs-lookup"><span data-stu-id="4a779-149">Take a manual backup</span></span>

<span data-ttu-id="4a779-150">Execute Olá seguindo as etapas no hello toocreate portal do Azure uma demanda (manual) backup para um único volume.</span><span class="sxs-lookup"><span data-stu-id="4a779-150">Perform hello following steps in hello Azure portal toocreate an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-8000-create-manual-backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a><span data-ttu-id="4a779-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4a779-151">Next steps</span></span>

<span data-ttu-id="4a779-152">Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador de dispositivos do StorSimple em seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="4a779-152">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

