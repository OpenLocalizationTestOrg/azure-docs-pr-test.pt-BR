---
title: Trabalhos de backup do StorSimple Snapshot Manager | Microsoft Docs
description: "Descreve como usar o snap-in StorSimple Snapshot Manager MMC para exibir e gerenciar trabalhos de backup agendados, em execução e concluídos."
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
ms.openlocfilehash: 03e306b62250f2bb033cc14e856a59760b5406c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-snapshot-manager-to-view-and-manage-backup-jobs"></a><span data-ttu-id="f9462-103">Usar o StorSimple Snapshot Manager para exibir e gerenciar trabalhos de backup</span><span class="sxs-lookup"><span data-stu-id="f9462-103">Use StorSimple Snapshot Manager to view and manage backup jobs</span></span>

## <a name="overview"></a><span data-ttu-id="f9462-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="f9462-104">Overview</span></span>
<span data-ttu-id="f9462-105">O nó **Trabalhos** no painel **Escopo** mostra as tarefas de backup **Agendado**, **Últimas 24 horas** e **Em execução** iniciadas interativamente ou por uma política configurada.</span><span class="sxs-lookup"><span data-stu-id="f9462-105">The **Jobs** node in the **Scope** pane shows the **Scheduled**, **Last 24 hours**, and **Running** backup tasks that you initiated interactively or by a configured policy.</span></span> 

<span data-ttu-id="f9462-106">Este tutorial explica como você pode usar o nó **Trabalhos** para exibir informações sobre os trabalhos de backup agendados, recentes e em execução no momento.</span><span class="sxs-lookup"><span data-stu-id="f9462-106">This tutorial explains how you can use the **Jobs** node to display information about scheduled, recent, and currently running backup jobs.</span></span> <span data-ttu-id="f9462-107">(A lista de trabalhos e as informações correspondentes aparece no painel **Resultados**.) Além disso, você pode clicar com o botão direito em um trabalho listado e ver um menu de contexto que lista as ações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="f9462-107">(The list of jobs and corresponding information appears in the **Results** pane.) Additionally, you can right-click a listed job and see a context menu that lists available actions.</span></span>

## <a name="view-scheduled-jobs"></a><span data-ttu-id="f9462-108">Ver trabalhos agendados</span><span class="sxs-lookup"><span data-stu-id="f9462-108">View scheduled jobs</span></span>
<span data-ttu-id="f9462-109">Use o procedimento a seguir para exibir os trabalhos de backup agendados.</span><span class="sxs-lookup"><span data-stu-id="f9462-109">Use the following procedure to view scheduled backup jobs.</span></span>

#### <a name="to-view-scheduled-jobs"></a><span data-ttu-id="f9462-110">Para exibir os trabalhos agendados</span><span class="sxs-lookup"><span data-stu-id="f9462-110">To view scheduled jobs</span></span>
1. <span data-ttu-id="f9462-111">Clique no ícone da área de trabalho para iniciar o StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="f9462-111">Click the desktop icon to start StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="f9462-112">No painel **Escopo**, expanda o nó **Trabalhos** e clique em **Agendado**.</span><span class="sxs-lookup"><span data-stu-id="f9462-112">In the **Scope** pane, expand the **Jobs** node, and click **Scheduled**.</span></span> <span data-ttu-id="f9462-113">As seguintes informações aparecem no painel **Resultados** :</span><span class="sxs-lookup"><span data-stu-id="f9462-113">The following information appears in the **Results** pane:</span></span>
   
   * <span data-ttu-id="f9462-114">**Nome** – o nome do instantâneo agendado</span><span class="sxs-lookup"><span data-stu-id="f9462-114">**Name** – the name of the scheduled snapshot</span></span>
   * <span data-ttu-id="f9462-115">**Próxima execução** – a data e hora do próximo instantâneo agendado</span><span class="sxs-lookup"><span data-stu-id="f9462-115">**Next Run** – the date and time of the next scheduled snapshot</span></span>
   * <span data-ttu-id="f9462-116">**Última execução** – a data e hora do instantâneo agendado mais recente</span><span class="sxs-lookup"><span data-stu-id="f9462-116">**Last Run** – the date and time of the most recent scheduled snapshot</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="f9462-117">Para instantâneos únicos, a **Próxima execução** e a **Última execução** serão iguais.</span><span class="sxs-lookup"><span data-stu-id="f9462-117">For one-time only snapshots, the **Next Run** and **Last Run** will be the same.</span></span>
     
     ![Trabalhos de backup agendados](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. <span data-ttu-id="f9462-119">Para executar ações adicionais em um trabalho específico, clique com o botão direito no nome do trabalho no painel **Resultados** e selecione uma das opções de menu.</span><span class="sxs-lookup"><span data-stu-id="f9462-119">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span></span>

## <a name="view-recent-jobs"></a><span data-ttu-id="f9462-120">Exibir trabalhos recentes</span><span class="sxs-lookup"><span data-stu-id="f9462-120">View recent jobs</span></span>
<span data-ttu-id="f9462-121">Use o procedimento a seguir para exibir os trabalhos de backup e restauração que foram concluídos nas últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="f9462-121">Use the following procedure to view backup and restore jobs that were completed in the last 24 hours.</span></span>

#### <a name="to-view-recent-jobs"></a><span data-ttu-id="f9462-122">Para exibir trabalhos recentes</span><span class="sxs-lookup"><span data-stu-id="f9462-122">To view recent jobs</span></span>
1. <span data-ttu-id="f9462-123">Clique no ícone da área de trabalho para iniciar o StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="f9462-123">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="f9462-124">No painel **Escopo**, expanda o nó **Trabalhos** e clique em **Últimas 24 horas**.</span><span class="sxs-lookup"><span data-stu-id="f9462-124">In the **Scope** pane, expand the **Jobs** node, and click **Last 24 hours**.</span></span> <span data-ttu-id="f9462-125">O painel **Resultados** mostra os trabalhos de backup para as últimas 24 horas (até um máximo de 64 trabalhos).</span><span class="sxs-lookup"><span data-stu-id="f9462-125">The **Results** pane shows backup jobs for the last 24 hours (to a maximum of 64 jobs).</span></span> <span data-ttu-id="f9462-126">As seguintes informações aparecem no painel **Resultados**, dependendo das opções de **Exibição** especificadas:</span><span class="sxs-lookup"><span data-stu-id="f9462-126">The following information appears in the **Results** pane, depending on the **View** options you specify:</span></span>
   
   * <span data-ttu-id="f9462-127">**Nome** – o nome do instantâneo agendado.</span><span class="sxs-lookup"><span data-stu-id="f9462-127">**Name** – the name of the scheduled snapshot.</span></span>
   * <span data-ttu-id="f9462-128">**Iniciado** – a data e a hora em que o instantâneo foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="f9462-128">**Started** – the date and time when the snapshot began.</span></span>
   * <span data-ttu-id="f9462-129">**Parado** – a data e a hora em que o instantâneo foi concluído ou encerrado.</span><span class="sxs-lookup"><span data-stu-id="f9462-129">**Stopped** – the date and time when the snapshot finished or was terminated.</span></span>
   * <span data-ttu-id="f9462-130">**Decorrido** – a quantidade de tempo entre os horários **Iniciado** e **Parado**.</span><span class="sxs-lookup"><span data-stu-id="f9462-130">**Elapsed** – the amount of time between the **Started** and **Stopped** times.</span></span>
   * <span data-ttu-id="f9462-131">**Status** – o estado do trabalho concluído recentemente.</span><span class="sxs-lookup"><span data-stu-id="f9462-131">**Status** – the state of the recently completed job.</span></span> <span data-ttu-id="f9462-132">**Sucesso** indica que o backup foi criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="f9462-132">**Success** indicates that the backup was created successfully.</span></span> <span data-ttu-id="f9462-133">**Falha** indica que o trabalho não foi executado com êxito.</span><span class="sxs-lookup"><span data-stu-id="f9462-133">**Failed** indicates that the job did not run successfully.</span></span>
   * <span data-ttu-id="f9462-134">**Informações** – o motivo da falha.</span><span class="sxs-lookup"><span data-stu-id="f9462-134">**Information** – the reason for the failure.</span></span>
   * <span data-ttu-id="f9462-135">**Bytes processados (MB)** – a quantidade de dados do grupo de volumes que foram processados (em MB).</span><span class="sxs-lookup"><span data-stu-id="f9462-135">**Bytes processed (MB)** – the amount of data from the volume group that was processed (in MBs).</span></span> 
     
     ![Trabalhos executados nas últimas 24 horas](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. <span data-ttu-id="f9462-137">Para executar ações adicionais em um trabalho específico, clique com o botão direito no nome do trabalho no painel **Resultados** e selecione uma das opções de menu.</span><span class="sxs-lookup"><span data-stu-id="f9462-137">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span></span>
   
    ![Excluir um trabalho](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png)

## <a name="view-currently-running-jobs"></a><span data-ttu-id="f9462-139">Exibir trabalhos em execução</span><span class="sxs-lookup"><span data-stu-id="f9462-139">View currently running jobs</span></span>
<span data-ttu-id="f9462-140">Use o procedimento a seguir para exibir os trabalhos que estão sendo executados.</span><span class="sxs-lookup"><span data-stu-id="f9462-140">Use the following procedure to view jobs that are currently running.</span></span>

#### <a name="to-view-currently-running-jobs"></a><span data-ttu-id="f9462-141">Para exibir os trabalhos em execução</span><span class="sxs-lookup"><span data-stu-id="f9462-141">To view currently running jobs</span></span>
1. <span data-ttu-id="f9462-142">Clique no ícone da área de trabalho para iniciar o StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="f9462-142">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="f9462-143">No painel **Escopo**, expanda o nó **Trabalhos** e clique em **Em execução**.</span><span class="sxs-lookup"><span data-stu-id="f9462-143">In the **Scope** pane, expand the **Jobs** node, and click **Running**.</span></span> <span data-ttu-id="f9462-144">Dependendo as opções de **Exibição** especificadas, as seguintes informações aparecem no painel **Resultados**:</span><span class="sxs-lookup"><span data-stu-id="f9462-144">Depending on the **View** options you specify, the following information appears in the **Results** pane:</span></span>
   
   * <span data-ttu-id="f9462-145">**Nome** – o nome do instantâneo agendado.</span><span class="sxs-lookup"><span data-stu-id="f9462-145">**Name** – the name of the scheduled snapshot.</span></span>
   * <span data-ttu-id="f9462-146">**Iniciado** – a data e a hora em que o instantâneo foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="f9462-146">**Started** – the date and time when the snapshot began.</span></span>
   * <span data-ttu-id="f9462-147">**Ponto de verificação** – a ação atual do backup.</span><span class="sxs-lookup"><span data-stu-id="f9462-147">**Checkpoint** – the current action of the backup.</span></span>
   * <span data-ttu-id="f9462-148">**Status** – o percentual de conclusão.</span><span class="sxs-lookup"><span data-stu-id="f9462-148">**Status** – the percentage of completion.</span></span>
   * <span data-ttu-id="f9462-149">**Decorrido** – a quantidade de tempo decorrido desde que o backup foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="f9462-149">**Elapsed** – the amount of time that has passed since the backup began.</span></span> 
   * <span data-ttu-id="f9462-150">**Taxa de transferência média (MB)** – proporção do total de bytes de dados processados em relação ao total de bytes do tempo total gasto para processamento (MBs).</span><span class="sxs-lookup"><span data-stu-id="f9462-150">**Average throughput (MB)** – ratio of total bytes of data processed to that of total time taken for processing (MBs).</span></span>
   * <span data-ttu-id="f9462-151">**Bytes processados (MB)** – total de bytes de dados processados (em MBs).</span><span class="sxs-lookup"><span data-stu-id="f9462-151">**Bytes processed (MB)** – total bytes of data processed (in MBs).</span></span>
   * <span data-ttu-id="f9462-152">**Bytes gravados (MB)** – total de bytes de dados gravados (em MBs).</span><span class="sxs-lookup"><span data-stu-id="f9462-152">**Bytes written (MB)** – total bytes of data written (in MBs).</span></span> <span data-ttu-id="f9462-153">Ela inclui os dados, bem como os metadados e, portanto, é geralmente maior que os Bytes Processados.</span><span class="sxs-lookup"><span data-stu-id="f9462-153">It includes the data as well as the metadata and hence is typically greater than the Bytes Processed.</span></span>
     
     ![Trabalhos em execução no momento](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. <span data-ttu-id="f9462-155">Para executar ações adicionais em um trabalho específico, clique com o botão direito no nome do trabalho no painel **Resultados** e selecione uma das opções de menu.</span><span class="sxs-lookup"><span data-stu-id="f9462-155">To perform additional actions on a specific job, right-click the job name in the **Results** pane and select from the menu options.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9462-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f9462-156">Next steps</span></span>
* <span data-ttu-id="f9462-157">Saiba como [usar o StorSimple Snapshot Manager para administrar sua solução do StorSimple](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="f9462-157">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="f9462-158">Saiba como [usar o StorSimple Snapshot Manager para gerenciar o catálogo de backup](storsimple-snapshot-manager-manage-backup-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="f9462-158">Learn how to [use StorSimple Snapshot Manager to manage the backup catalog](storsimple-snapshot-manager-manage-backup-catalog.md).</span></span>

