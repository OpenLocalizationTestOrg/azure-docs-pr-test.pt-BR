---
title: aaaView e gerenciar trabalhos de StorSimple | Microsoft Docs
description: "Descreve a página de trabalhos de serviço Olá StorSimple Manager e como toouse ela trabalhos de backup agendados, atual e recentes tootrack."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: cdd3e9e8-7ccd-40a3-8c07-0ab1338c0e59
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: d6ecdcbc3d8a4757c2328303f268e51c8ce26b65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-jobs-update-2"></a><span data-ttu-id="a02a7-103">Usar tooview de serviço do StorSimple Manager hello e gerenciar trabalhos do StorSimple (atualização 2)</span><span class="sxs-lookup"><span data-stu-id="a02a7-103">Use hello StorSimple Manager service tooview and manage StorSimple jobs (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a><span data-ttu-id="a02a7-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a02a7-104">Overview</span></span>
<span data-ttu-id="a02a7-105">Olá **trabalhos** página fornece um único portal central para exibir e gerenciar trabalhos iniciados em dispositivos conectados tooyour o serviço StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="a02a7-105">hello **Jobs** page provides a single central portal for viewing and managing jobs that were started on devices connected tooyour StorSimple Manager service.</span></span> <span data-ttu-id="a02a7-106">É possível exibir os trabalhos agendados, em execução, concluídos, cancelados e com falha para vários dispositivos.</span><span class="sxs-lookup"><span data-stu-id="a02a7-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="a02a7-107">Os resultados são apresentados em um formato tabular.</span><span class="sxs-lookup"><span data-stu-id="a02a7-107">Results are presented in a tabular format.</span></span> 

![Página Trabalhos](./media/storsimple-manage-jobs-u2/jobs.png)

<span data-ttu-id="a02a7-109">Você pode localizar rapidamente os trabalhos de saudação que está interessado ao filtrar campos, como:</span><span class="sxs-lookup"><span data-stu-id="a02a7-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="a02a7-110">**Status** – os trabalhos podem estar em execução, concluídos, cancelados, com falha, em cancelamento ou concluídos com erros.</span><span class="sxs-lookup"><span data-stu-id="a02a7-110">**Status** – Jobs can be running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="a02a7-111">**De e para** – trabalhos podem ser o intervalo de filtrado Olá com base na data e hora.</span><span class="sxs-lookup"><span data-stu-id="a02a7-111">**From and To** – Jobs can be filtered based on hello date and time range.</span></span>
* <span data-ttu-id="a02a7-112">**Tipo** – tipo de trabalho Olá pode ser backup, backup manual, restauração, clonagem, failover de dispositivo, criar volume afixado localmente, modificar o volume, atualizar, suporte de pacote ou provisionamento do dispositivo virtual.</span><span class="sxs-lookup"><span data-stu-id="a02a7-112">**Type** – hello job type can be backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
* <span data-ttu-id="a02a7-113">**Dispositivos** – os trabalhos são iniciados em um determinado serviço de tooyour dispositivo conectado.</span><span class="sxs-lookup"><span data-stu-id="a02a7-113">**Devices** – Jobs are initiated on a certain device connected tooyour service.</span></span>
  <span data-ttu-id="a02a7-114">Olá trabalhos filtrados são então tabulados com base Olá Olá seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="a02a7-114">hello filtered jobs are then tabulated on hello basis of hello following attributes:</span></span>
  
  * <span data-ttu-id="a02a7-115">**Tipo** – backup, backup manual, restauração, clonagem, failover de dispositivo, criação de volume fixado localmente, modificação de volume, atualização, pacote de suporte ou provisionamento do dispositivo virtual.</span><span class="sxs-lookup"><span data-stu-id="a02a7-115">**Type** – backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
  * <span data-ttu-id="a02a7-116">**Status** – em execução, concluídos, cancelados, com falha, em cancelamento ou concluídos com erros.</span><span class="sxs-lookup"><span data-stu-id="a02a7-116">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
  * <span data-ttu-id="a02a7-117">**Entidade** – trabalhos Olá podem ser associados um volume, uma política de backup ou um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a02a7-117">**Entity** – hello jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="a02a7-118">Por exemplo, um trabalho de clone é associado a um volume, enquanto um trabalho de backup agendado é associado a uma política de backup.</span><span class="sxs-lookup"><span data-stu-id="a02a7-118">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="a02a7-119">Um trabalho de dispositivo é criado como resultado de uma recuperação de desastres (DR) ou uma operação de restauração.</span><span class="sxs-lookup"><span data-stu-id="a02a7-119">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
  * <span data-ttu-id="a02a7-120">**Dispositivo** – hello nome de dispositivo de saudação na qual Olá o trabalho foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="a02a7-120">**Device** – hello name of hello device on which hello job was started.</span></span>
  * <span data-ttu-id="a02a7-121">**Iniciado em** – tempo de saudação quando o trabalho de saudação foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="a02a7-121">**Started on** – hello time when hello job was started.</span></span>
  * <span data-ttu-id="a02a7-122">**Andamento** – Olá percentual de conclusão de um trabalho em execução.</span><span class="sxs-lookup"><span data-stu-id="a02a7-122">**Progress** – hello percentage completion of a running job.</span></span> <span data-ttu-id="a02a7-123">Para um trabalho concluído, sempre deve ser 100%.</span><span class="sxs-lookup"><span data-stu-id="a02a7-123">For a completed job, this should always be 100%.</span></span>

<span data-ttu-id="a02a7-124">lista de saudação de trabalhos é atualizada a cada 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="a02a7-124">hello list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="a02a7-125">Você pode executar Olá relacionada ao trabalho ações a seguir nesta página:</span><span class="sxs-lookup"><span data-stu-id="a02a7-125">You can perform hello following job-related actions on this page:</span></span>

* <span data-ttu-id="a02a7-126">Exibir detalhes do trabalho</span><span class="sxs-lookup"><span data-stu-id="a02a7-126">View job details</span></span>
* <span data-ttu-id="a02a7-127">Cancelar um trabalho</span><span class="sxs-lookup"><span data-stu-id="a02a7-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="a02a7-128">Exibir detalhes do trabalho</span><span class="sxs-lookup"><span data-stu-id="a02a7-128">View job details</span></span>
<span data-ttu-id="a02a7-129">Execute Olá etapas tooview Olá detalhes de qualquer trabalho a seguir.</span><span class="sxs-lookup"><span data-stu-id="a02a7-129">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="a02a7-130">detalhes do trabalho tooview</span><span class="sxs-lookup"><span data-stu-id="a02a7-130">tooview job details</span></span>
1. <span data-ttu-id="a02a7-131">Em Olá **trabalhos** página, exibir hello (s) que está interessado executando uma consulta com os filtros apropriados.</span><span class="sxs-lookup"><span data-stu-id="a02a7-131">On hello **Jobs** page, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="a02a7-132">É possível pesquisar trabalhos concluídos, em execução ou cancelados.</span><span class="sxs-lookup"><span data-stu-id="a02a7-132">You can search for completed, running, or canceled jobs.</span></span>
2. <span data-ttu-id="a02a7-133">Selecione um trabalho.</span><span class="sxs-lookup"><span data-stu-id="a02a7-133">Select a job.</span></span>
3. <span data-ttu-id="a02a7-134">Final Olá Olá página, clique em **detalhes**.</span><span class="sxs-lookup"><span data-stu-id="a02a7-134">At hello bottom of hello page, click **Details**.</span></span>
4. <span data-ttu-id="a02a7-135">Em Olá **detalhes do trabalho de Backup** caixa de diálogo, você pode exibir o status de hello, detalhes, estatísticas de tempo e as estatísticas de dados.</span><span class="sxs-lookup"><span data-stu-id="a02a7-135">In hello **Backup Job Details** dialog box, you can view hello status, details, time statistics, and data statistics.</span></span>
   
    ![Página de detalhes do trabalho](./media/storsimple-manage-jobs-u2/JobDetails.png)

## <a name="cancel-a-job"></a><span data-ttu-id="a02a7-137">Cancelar um trabalho</span><span class="sxs-lookup"><span data-stu-id="a02a7-137">Cancel a job</span></span>
<span data-ttu-id="a02a7-138">Execute Olá seguindo as etapas toocancel um trabalho em execução.</span><span class="sxs-lookup"><span data-stu-id="a02a7-138">Perform hello following steps toocancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="a02a7-139">Alguns trabalhos, como modificar um tipo de volume do volume toochange hello ou expandir um volume não podem ser cancelados.</span><span class="sxs-lookup"><span data-stu-id="a02a7-139">Some jobs, such as modifying a volume toochange hello volume type or expanding a volume, cannot be canceled.</span></span>
> 
> 

### <a name="toocancel-a-job"></a><span data-ttu-id="a02a7-140">toocancel um trabalho</span><span class="sxs-lookup"><span data-stu-id="a02a7-140">toocancel a job</span></span>
1. <span data-ttu-id="a02a7-141">Em Olá **trabalhos** página, exibir hello em execução (s) que você deseja toocancel executando uma consulta com os filtros apropriados.</span><span class="sxs-lookup"><span data-stu-id="a02a7-141">On hello **Jobs** page, display hello running job(s) that you want toocancel by running a query with appropriate filters.</span></span>
2. <span data-ttu-id="a02a7-142">Selecione o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="a02a7-142">Select hello job.</span></span>
3. <span data-ttu-id="a02a7-143">Final Olá Olá página, clique em **Cancelar**.</span><span class="sxs-lookup"><span data-stu-id="a02a7-143">At hello bottom of hello page, click **Cancel**.</span></span>
4. <span data-ttu-id="a02a7-144">Quando solicitado a confirmar, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="a02a7-144">When prompted for confirmation, click **Yes**.</span></span>

<span data-ttu-id="a02a7-145">Este trabalho agora está cancelado.</span><span class="sxs-lookup"><span data-stu-id="a02a7-145">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a02a7-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a02a7-146">Next steps</span></span>
* <span data-ttu-id="a02a7-147">Saiba como muito[gerenciar suas políticas de backup StorSimple](storsimple-manage-backup-policies.md).</span><span class="sxs-lookup"><span data-stu-id="a02a7-147">Learn how too[manage your StorSimple backup policies](storsimple-manage-backup-policies.md).</span></span>
* <span data-ttu-id="a02a7-148">Saiba como muito[use Olá tooadminister do serviço StorSimple Manager seu dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="a02a7-148">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

