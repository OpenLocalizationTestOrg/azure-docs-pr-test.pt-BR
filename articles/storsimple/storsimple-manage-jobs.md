---
title: Exibir e gerenciar trabalhos do StorSimple | Microsoft Docs
description: "Descreve a página de Trabalhos do serviço StorSimple Manager e como usá-la para controlar os trabalhos de backup recentes, atuais e agendados."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 55922cd0-d490-48eb-938a-012a67c1c09e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 7d9377bb8f3cb8c587823c2d71d61dfb9b50f52f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-view-and-manage-storsimple-jobs"></a><span data-ttu-id="ac5f3-103">Use o serviço StorSimple Manager para exibir e gerenciar trabalhos do StorSimple</span><span class="sxs-lookup"><span data-stu-id="ac5f3-103">Use the StorSimple Manager service to view and manage StorSimple jobs</span></span>
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a><span data-ttu-id="ac5f3-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="ac5f3-104">Overview</span></span>
<span data-ttu-id="ac5f3-105">A página **Trabalhos** oferece um portal central único para visualização e gerenciamento de trabalhos que foram iniciados em dispositivos conectados ao serviço StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="ac5f3-105">The **Jobs** page provides a single central portal for viewing and managing jobs that were started on devices connected to your StorSimple Manager service.</span></span> <span data-ttu-id="ac5f3-106">É possível exibir os trabalhos agendados, em execução, concluídos e com falha para vários dispositivos.</span><span class="sxs-lookup"><span data-stu-id="ac5f3-106">You can view scheduled, running, completed, and failed jobs for multiple devices.</span></span> <span data-ttu-id="ac5f3-107">Os resultados são apresentados em um formato tabular.</span><span class="sxs-lookup"><span data-stu-id="ac5f3-107">Results are presented in a tabular format.</span></span> 

![Página Trabalhos](./media/storsimple-manage-jobs/HCS_JobsPage.png)

<span data-ttu-id="ac5f3-109">Você pode localizar rapidamente os trabalhos nos quais está interessado filtrando os campos, como:</span><span class="sxs-lookup"><span data-stu-id="ac5f3-109">You can quickly find the jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="ac5f3-110">**Status** – os trabalhos podem estar em execução, agendados, com falha, concluídos, em cancelamento ou cancelados.</span><span class="sxs-lookup"><span data-stu-id="ac5f3-110">**Status** – Jobs can be running, scheduled, failed, completed, canceling, or canceled.</span></span>
* <span data-ttu-id="ac5f3-111">**Tipo** – Os trabalhos podem ser criados como resultado de um backup sob demanda ou agendado (**Fazer Backup**), clonagem, uma restauração de dispositivo ou uma operação de atualização.</span><span class="sxs-lookup"><span data-stu-id="ac5f3-111">**Type** – Jobs can be created as a result of a scheduled or an on-demand backup (**Take Backup**), cloning, a device restore, or an update operation.</span></span>
* <span data-ttu-id="ac5f3-112">**Dispositivos** – os trabalhos são iniciados em um determinado dispositivo conectado ao seu serviço.</span><span class="sxs-lookup"><span data-stu-id="ac5f3-112">**Devices** – Jobs are initiated on a certain device connected to your service.</span></span>
* <span data-ttu-id="ac5f3-113">**De e Para** – os trabalhos podem ser filtrados com base no intervalo de data e hora.</span><span class="sxs-lookup"><span data-stu-id="ac5f3-113">**From and To** – Jobs can be filtered based on the date and time range.</span></span>

<span data-ttu-id="ac5f3-114">Os trabalhos filtrados são então tabulados com base nos seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="ac5f3-114">The filtered jobs are then tabulated on the basis of the following attributes:</span></span>

* <span data-ttu-id="ac5f3-115">**Tipo** – backup, clone, restauração, failover ou atualização.</span><span class="sxs-lookup"><span data-stu-id="ac5f3-115">**Type** – Backup, clone, restore, failover, or update.</span></span>
* <span data-ttu-id="ac5f3-116">**Status** – em execução, agendado, com falha, concluído, em cancelamento ou cancelado.</span><span class="sxs-lookup"><span data-stu-id="ac5f3-116">**Status** – Running, scheduled, failed, completed, canceling, or canceled.</span></span>
* <span data-ttu-id="ac5f3-117">**Entidade** – os trabalhos podem ser associados a um volume, uma política de backup ou um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ac5f3-117">**Entity** – The jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="ac5f3-118">Um trabalho de clone é associado a um volume, enquanto um trabalho de backup agendado é associado a uma política de backup.</span><span class="sxs-lookup"><span data-stu-id="ac5f3-118">A clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="ac5f3-119">Um trabalho de dispositivo é criado como resultado de uma recuperação de desastres (DR) ou uma operação de restauração.</span><span class="sxs-lookup"><span data-stu-id="ac5f3-119">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
* <span data-ttu-id="ac5f3-120">**Dispositivo** – o nome do dispositivo no qual o trabalho foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="ac5f3-120">**Device** – The name of the device on which the job was started.</span></span>
* <span data-ttu-id="ac5f3-121">**Iniciado em** – a hora em que o trabalho foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="ac5f3-121">**Started On** – The time when the job was started.</span></span>
* <span data-ttu-id="ac5f3-122">**Andamento** – o percentual de conclusão de um trabalho em execução.</span><span class="sxs-lookup"><span data-stu-id="ac5f3-122">**Progress** – The percentage completion of a running job.</span></span> <span data-ttu-id="ac5f3-123">Para um trabalho concluído, sempre deve ser 100%.</span><span class="sxs-lookup"><span data-stu-id="ac5f3-123">For a completed job, this should always be 100%.</span></span>

<span data-ttu-id="ac5f3-124">A lista de trabalhos é atualizada a cada 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="ac5f3-124">The list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="ac5f3-125">É possível executar as seguintes ações relacionadas a trabalho nesta página:</span><span class="sxs-lookup"><span data-stu-id="ac5f3-125">You can perform the following job-related actions on this page:</span></span>

* <span data-ttu-id="ac5f3-126">Exibir detalhes do trabalho</span><span class="sxs-lookup"><span data-stu-id="ac5f3-126">View job details</span></span>
* <span data-ttu-id="ac5f3-127">Cancelar um trabalho</span><span class="sxs-lookup"><span data-stu-id="ac5f3-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="ac5f3-128">Exibir detalhes do trabalho</span><span class="sxs-lookup"><span data-stu-id="ac5f3-128">View job details</span></span>
<span data-ttu-id="ac5f3-129">Execute as etapas a seguir para exibir os detalhes de qualquer trabalho.</span><span class="sxs-lookup"><span data-stu-id="ac5f3-129">Perform the following steps to view the details of any job.</span></span>

#### <a name="to-view-job-details"></a><span data-ttu-id="ac5f3-130">Para exibir detalhes do trabalho</span><span class="sxs-lookup"><span data-stu-id="ac5f3-130">To view job details</span></span>
1. <span data-ttu-id="ac5f3-131">Na página **Trabalhos** , exiba o(s) trabalho(s) no(s) qual(is) está interessado executando uma consulta com os filtros apropriados.</span><span class="sxs-lookup"><span data-stu-id="ac5f3-131">On the **Jobs** page, display the job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="ac5f3-132">É possível pesquisar trabalhos concluídos, em execução ou cancelados.</span><span class="sxs-lookup"><span data-stu-id="ac5f3-132">You can search for completed, running, or canceled jobs.</span></span>
2. <span data-ttu-id="ac5f3-133">Selecione um trabalho.</span><span class="sxs-lookup"><span data-stu-id="ac5f3-133">Select a job.</span></span>
3. <span data-ttu-id="ac5f3-134">Na parte inferior da página, clique em **Detalhes**.</span><span class="sxs-lookup"><span data-stu-id="ac5f3-134">At the bottom of the page, click **Details**.</span></span>
4. <span data-ttu-id="ac5f3-135">Na caixa de diálogo **Detalhes do Trabalho de Backup** , é possível exibir o status, os detalhes, as estatísticas de tempo e as estatísticas de dados.</span><span class="sxs-lookup"><span data-stu-id="ac5f3-135">In the **Backup Job Details** dialog box, you can view the status, details, time statistics, and data statistics.</span></span>

## <a name="cancel-a-job"></a><span data-ttu-id="ac5f3-136">Cancelar um trabalho</span><span class="sxs-lookup"><span data-stu-id="ac5f3-136">Cancel a job</span></span>
<span data-ttu-id="ac5f3-137">Realize as etapas a seguir para cancelar um trabalho em execução.</span><span class="sxs-lookup"><span data-stu-id="ac5f3-137">Perform the following steps to cancel a running job.</span></span>

### <a name="to-cancel-a-job"></a><span data-ttu-id="ac5f3-138">Para cancelar um trabalho</span><span class="sxs-lookup"><span data-stu-id="ac5f3-138">To cancel a job</span></span>
1. <span data-ttu-id="ac5f3-139">Na página **Trabalhos** , exiba os trabalhos em execução que você deseja cancelar executando uma consulta com os filtros apropriados.</span><span class="sxs-lookup"><span data-stu-id="ac5f3-139">On the **Jobs** page, display the running job(s) that you want to cancel by running a query with appropriate filters.</span></span>
2. <span data-ttu-id="ac5f3-140">Selecione o trabalho.</span><span class="sxs-lookup"><span data-stu-id="ac5f3-140">Select the job.</span></span>
3. <span data-ttu-id="ac5f3-141">Na parte inferior da página, clique em **Cancelar**.</span><span class="sxs-lookup"><span data-stu-id="ac5f3-141">At the bottom of the page, click **Cancel**.</span></span>
4. <span data-ttu-id="ac5f3-142">Quando solicitado a confirmar, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="ac5f3-142">When prompted for confirmation, click **Yes**.</span></span>

<span data-ttu-id="ac5f3-143">Este trabalho agora está cancelado.</span><span class="sxs-lookup"><span data-stu-id="ac5f3-143">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac5f3-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ac5f3-144">Next steps</span></span>
* <span data-ttu-id="ac5f3-145">Saiba como [gerenciar as políticas de backup do StorSimple](storsimple-manage-backup-policies.md).</span><span class="sxs-lookup"><span data-stu-id="ac5f3-145">Learn how to [manage your StorSimple backup policies](storsimple-manage-backup-policies.md).</span></span>
* <span data-ttu-id="ac5f3-146">Saiba como [usar o serviço StorSimple Manager para administrar seu dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="ac5f3-146">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

