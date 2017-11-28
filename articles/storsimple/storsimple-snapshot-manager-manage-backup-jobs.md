---
title: "trabalhos de backup de instantâneo Manager aaaStorSimple | Microsoft Docs"
description: "Descreve como toouse Olá MMC Gerenciador de instantâneos StorSimple snap-in tooview e gerenciar trabalhos de backup agendados, atualmente em execução e concluídos."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: bf4dcff6-c819-4766-b9d9-9922831cb200
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 3dba0a2aa527d17d67130f537bcdce5722b05a76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-backup-jobs"></a><span data-ttu-id="a3a3d-103">Use o Gerenciador de instantâneos StorSimple tooview e gerenciar trabalhos de backup</span><span class="sxs-lookup"><span data-stu-id="a3a3d-103">Use StorSimple Snapshot Manager tooview and manage backup jobs</span></span>

## <a name="overview"></a><span data-ttu-id="a3a3d-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a3a3d-104">Overview</span></span>
<span data-ttu-id="a3a3d-105">Olá **trabalhos** nó Olá **escopo** painel mostra Olá **agendada**, **últimas 24 horas**, e **executando**tarefas iniciadas interativamente ou por uma política de configuração de backup.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-105">hello **Jobs** node in hello **Scope** pane shows hello **Scheduled**, **Last 24 hours**, and **Running** backup tasks that you initiated interactively or by a configured policy.</span></span> 

<span data-ttu-id="a3a3d-106">Este tutorial explica como você pode usar o hello **trabalhos** informações do nó toodisplay sobre trabalhos de backup agendados, recentes e em execução no momento.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-106">This tutorial explains how you can use hello **Jobs** node toodisplay information about scheduled, recent, and currently running backup jobs.</span></span> <span data-ttu-id="a3a3d-107">(lista de saudação de trabalhos e as informações correspondentes aparece no hello **resultados** painel.) Além disso, você pode clicar com o botão direito em um trabalho listado e ver um menu de contexto que lista as ações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-107">(hello list of jobs and corresponding information appears in hello **Results** pane.) Additionally, you can right-click a listed job and see a context menu that lists available actions.</span></span>

## <a name="view-scheduled-jobs"></a><span data-ttu-id="a3a3d-108">Ver trabalhos agendados</span><span class="sxs-lookup"><span data-stu-id="a3a3d-108">View scheduled jobs</span></span>
<span data-ttu-id="a3a3d-109">Olá Use seguindo o procedimento tooview trabalhos de backup agendados.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-109">Use hello following procedure tooview scheduled backup jobs.</span></span>

#### <a name="tooview-scheduled-jobs"></a><span data-ttu-id="a3a3d-110">trabalhos agendado do tooview</span><span class="sxs-lookup"><span data-stu-id="a3a3d-110">tooview scheduled jobs</span></span>
1. <span data-ttu-id="a3a3d-111">Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-111">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="a3a3d-112">Em Olá **escopo** painel, expanda Olá **trabalhos** nó e clique em **agendada**.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-112">In hello **Scope** pane, expand hello **Jobs** node, and click **Scheduled**.</span></span> <span data-ttu-id="a3a3d-113">Olá seguintes informações aparecem no hello **resultados** painel:</span><span class="sxs-lookup"><span data-stu-id="a3a3d-113">hello following information appears in hello **Results** pane:</span></span>
   
   * <span data-ttu-id="a3a3d-114">**Nome** – hello nome do instantâneo agendado Olá</span><span class="sxs-lookup"><span data-stu-id="a3a3d-114">**Name** – hello name of hello scheduled snapshot</span></span>
   * <span data-ttu-id="a3a3d-115">**Em seguida execute** – Olá data e hora do próximo instantâneo programado de saudação</span><span class="sxs-lookup"><span data-stu-id="a3a3d-115">**Next Run** – hello date and time of hello next scheduled snapshot</span></span>
   * <span data-ttu-id="a3a3d-116">**Última execução** – Olá data e hora do instantâneo agendado mais recente de saudação</span><span class="sxs-lookup"><span data-stu-id="a3a3d-116">**Last Run** – hello date and time of hello most recent scheduled snapshot</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="a3a3d-117">Apenas para instantâneos únicos, Olá **próxima execução** e **última execução** será Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-117">For one-time only snapshots, hello **Next Run** and **Last Run** will be hello same.</span></span>
     
     ![Trabalhos de backup agendados](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. <span data-ttu-id="a3a3d-119">ações adicionais de tooperform em um trabalho específico, clique com botão direito nome do trabalho Olá no hello **resultados** painel e selecione uma das opções de menu hello.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-119">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>

## <a name="view-recent-jobs"></a><span data-ttu-id="a3a3d-120">Exibir trabalhos recentes</span><span class="sxs-lookup"><span data-stu-id="a3a3d-120">View recent jobs</span></span>
<span data-ttu-id="a3a3d-121">Use Olá backup tooview do procedimento a seguir e restaure os trabalhos que foram concluídos no hello últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-121">Use hello following procedure tooview backup and restore jobs that were completed in hello last 24 hours.</span></span>

#### <a name="tooview-recent-jobs"></a><span data-ttu-id="a3a3d-122">trabalhos recentes tooview</span><span class="sxs-lookup"><span data-stu-id="a3a3d-122">tooview recent jobs</span></span>
1. <span data-ttu-id="a3a3d-123">Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-123">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="a3a3d-124">Em Olá **escopo** painel, expanda Olá **trabalhos** nó e clique em **últimas 24 horas**.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-124">In hello **Scope** pane, expand hello **Jobs** node, and click **Last 24 hours**.</span></span> <span data-ttu-id="a3a3d-125">Olá **resultados** painel mostra os trabalhos de backup para Olá últimas 24 horas (tooa máximo de 64 trabalhos).</span><span class="sxs-lookup"><span data-stu-id="a3a3d-125">hello **Results** pane shows backup jobs for hello last 24 hours (tooa maximum of 64 jobs).</span></span> <span data-ttu-id="a3a3d-126">Olá seguintes informações aparecem no hello **resultados** painel, dependendo da saudação **exibição** opções que você especificar:</span><span class="sxs-lookup"><span data-stu-id="a3a3d-126">hello following information appears in hello **Results** pane, depending on hello **View** options you specify:</span></span>
   
   * <span data-ttu-id="a3a3d-127">**Nome** – hello nome do instantâneo agendado hello.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-127">**Name** – hello name of hello scheduled snapshot.</span></span>
   * <span data-ttu-id="a3a3d-128">**Iniciado** – a saudação data e a hora de início do instantâneo hello.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-128">**Started** – hello date and time when hello snapshot began.</span></span>
   * <span data-ttu-id="a3a3d-129">**Interrompido** – a data de saudação e a hora quando o instantâneo de saudação foi concluído ou terminado.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-129">**Stopped** – hello date and time when hello snapshot finished or was terminated.</span></span>
   * <span data-ttu-id="a3a3d-130">**Decorrido** – quantidade Olá de tempo entre hello **iniciado** e **parado** vezes.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-130">**Elapsed** – hello amount of time between hello **Started** and **Stopped** times.</span></span>
   * <span data-ttu-id="a3a3d-131">**Status** – Olá estado de trabalho Olá concluído recentemente.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-131">**Status** – hello state of hello recently completed job.</span></span> <span data-ttu-id="a3a3d-132">**Sucesso** indica que o backup Olá foi criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-132">**Success** indicates that hello backup was created successfully.</span></span> <span data-ttu-id="a3a3d-133">**Falha ao** indica que o trabalho Olá não foi executado com êxito.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-133">**Failed** indicates that hello job did not run successfully.</span></span>
   * <span data-ttu-id="a3a3d-134">**Informações** – Olá motivo da falha de saudação.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-134">**Information** – hello reason for hello failure.</span></span>
   * <span data-ttu-id="a3a3d-135">**Bytes processados (MB)** – quantidade Olá de dados do grupo de volumes de saudação foi processado (em MBs).</span><span class="sxs-lookup"><span data-stu-id="a3a3d-135">**Bytes processed (MB)** – hello amount of data from hello volume group that was processed (in MBs).</span></span> 
     
     ![Trabalhos executados em Olá últimas 24 horas](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. <span data-ttu-id="a3a3d-137">ações adicionais de tooperform em um trabalho específico, clique com botão direito nome do trabalho Olá no hello **resultados** painel e selecione uma das opções de menu hello.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-137">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>
   
    ![Excluir um trabalho](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png)

## <a name="view-currently-running-jobs"></a><span data-ttu-id="a3a3d-139">Exibir trabalhos em execução</span><span class="sxs-lookup"><span data-stu-id="a3a3d-139">View currently running jobs</span></span>
<span data-ttu-id="a3a3d-140">Use Olá trabalhos tooview de procedimento que estão em execução a seguir.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-140">Use hello following procedure tooview jobs that are currently running.</span></span>

#### <a name="tooview-currently-running-jobs"></a><span data-ttu-id="a3a3d-141">tooview trabalhos em execução</span><span class="sxs-lookup"><span data-stu-id="a3a3d-141">tooview currently running jobs</span></span>
1. <span data-ttu-id="a3a3d-142">Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-142">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="a3a3d-143">Em Olá **escopo** painel, expanda Olá **trabalhos** nó e clique em **executando**.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-143">In hello **Scope** pane, expand hello **Jobs** node, and click **Running**.</span></span> <span data-ttu-id="a3a3d-144">Dependendo da saudação **exibição** opções que você especificar, Olá informações a seguir aparece no hello **resultados** painel:</span><span class="sxs-lookup"><span data-stu-id="a3a3d-144">Depending on hello **View** options you specify, hello following information appears in hello **Results** pane:</span></span>
   
   * <span data-ttu-id="a3a3d-145">**Nome** – hello nome do instantâneo agendado hello.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-145">**Name** – hello name of hello scheduled snapshot.</span></span>
   * <span data-ttu-id="a3a3d-146">**Iniciado** – a saudação data e a hora de início do instantâneo hello.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-146">**Started** – hello date and time when hello snapshot began.</span></span>
   * <span data-ttu-id="a3a3d-147">**Ponto de verificação** – Olá ação atual do backup hello.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-147">**Checkpoint** – hello current action of hello backup.</span></span>
   * <span data-ttu-id="a3a3d-148">**Status** – Olá porcentagem de conclusão.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-148">**Status** – hello percentage of completion.</span></span>
   * <span data-ttu-id="a3a3d-149">**Decorrido** – quantidade de saudação do tempo decorrido desde o início do backup hello.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-149">**Elapsed** – hello amount of time that has passed since hello backup began.</span></span> 
   * <span data-ttu-id="a3a3d-150">**Taxa de transferência média (MB)** – proporção do total de bytes de dados processados toothat do tempo total gasto para processar (MBs).</span><span class="sxs-lookup"><span data-stu-id="a3a3d-150">**Average throughput (MB)** – ratio of total bytes of data processed toothat of total time taken for processing (MBs).</span></span>
   * <span data-ttu-id="a3a3d-151">**Bytes processados (MB)** – total de bytes de dados processados (em MBs).</span><span class="sxs-lookup"><span data-stu-id="a3a3d-151">**Bytes processed (MB)** – total bytes of data processed (in MBs).</span></span>
   * <span data-ttu-id="a3a3d-152">**Bytes gravados (MB)** – total de bytes de dados gravados (em MBs).</span><span class="sxs-lookup"><span data-stu-id="a3a3d-152">**Bytes written (MB)** – total bytes of data written (in MBs).</span></span> <span data-ttu-id="a3a3d-153">Ele inclui dados hello, bem como metadados de saudação e, portanto, é normalmente maior Olá Bytes processados.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-153">It includes hello data as well as hello metadata and hence is typically greater than hello Bytes Processed.</span></span>
     
     ![Trabalhos em execução no momento](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. <span data-ttu-id="a3a3d-155">ações adicionais de tooperform em um trabalho específico, clique com botão direito nome do trabalho Olá no hello **resultados** painel e selecione uma das opções de menu hello.</span><span class="sxs-lookup"><span data-stu-id="a3a3d-155">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3a3d-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a3a3d-156">Next steps</span></span>
* <span data-ttu-id="a3a3d-157">Saiba como muito[usar o Gerenciador de instantâneos StorSimple tooadminister sua solução StorSimple](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="a3a3d-157">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="a3a3d-158">Saiba como muito[usar o catálogo de backup do Gerenciador de instantâneos StorSimple toomanage Olá](storsimple-snapshot-manager-manage-backup-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="a3a3d-158">Learn how too[use StorSimple Snapshot Manager toomanage hello backup catalog](storsimple-snapshot-manager-manage-backup-catalog.md).</span></span>

