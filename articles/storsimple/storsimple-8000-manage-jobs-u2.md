---
title: "aaaView e gerenciar trabalhos para StorSimple série 8000 | Microsoft Docs"
description: "Descreve a folha de trabalhos de serviço de Gerenciador de dispositivos de StorSimple hello e como toouse ela trabalhos de backup agendados, atual e recentes tootrack."
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
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: a76acd67e2568478dd43d0fb16c1ae2dfb72a23d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-and-manage-jobs-update-3-and-later"></a><span data-ttu-id="6f852-103">Usar tooview de serviço do Gerenciador de dispositivos de StorSimple hello e gerenciar trabalhos (atualização 3 e posterior)</span><span class="sxs-lookup"><span data-stu-id="6f852-103">Use hello StorSimple Device Manager service tooview and manage jobs (Update 3 and later)</span></span>

## <a name="overview"></a><span data-ttu-id="6f852-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="6f852-104">Overview</span></span>
<span data-ttu-id="6f852-105">Olá **trabalhos** folha fornece um único portal central para exibir e gerenciar trabalhos iniciados em dispositivos conectados tooyour serviço de Gerenciador de dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6f852-105">hello **Jobs** blade provides a single central portal for viewing and managing jobs that were started on devices connected tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="6f852-106">É possível exibir os trabalhos agendados, em execução, concluídos, cancelados e com falha para vários dispositivos.</span><span class="sxs-lookup"><span data-stu-id="6f852-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="6f852-107">Os resultados são apresentados em um formato tabular.</span><span class="sxs-lookup"><span data-stu-id="6f852-107">Results are presented in a tabular format.</span></span>

![Folha de trabalhos](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

<span data-ttu-id="6f852-109">Você pode localizar rapidamente os trabalhos de saudação que está interessado ao filtrar campos, como:</span><span class="sxs-lookup"><span data-stu-id="6f852-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="6f852-110">**Status** – Os trabalhos podem estar em andamento, ser bem-sucedidos, cancelados ou concluídos com falha.</span><span class="sxs-lookup"><span data-stu-id="6f852-110">**Status** – Jobs can be in progress, succeeded, canceled, failed, canceling, or succeeded with errors.</span></span>
* <span data-ttu-id="6f852-111">**Intervalo de tempo** – trabalhos podem ser o intervalo de filtrado Olá com base na data e hora.</span><span class="sxs-lookup"><span data-stu-id="6f852-111">**Time range** – Jobs can be filtered based on hello date and time range.</span></span> <span data-ttu-id="6f852-112">os intervalos de saudação são após 1 hora, nas últimas 24 horas, últimos 7 dias, últimos 30 dias, o último ano ou data personalizada.</span><span class="sxs-lookup"><span data-stu-id="6f852-112">hello ranges are past 1 hour, past 24 hours, past 7 days, past 30 days, past year, or custom date.</span></span>
* <span data-ttu-id="6f852-113">**Tipo** – tipo de trabalho Olá pode ser backup agendado, o backup manual, o backup da restauração, clonar volume failover contêineres de volume, crie volume localmente afixado, modificar o volume, instalar atualizações, coletar logs de suporte e solução de nuvem.</span><span class="sxs-lookup"><span data-stu-id="6f852-113">**Type** – hello job type can be scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally-pinned volume, modify volume, install updates, collect support logs and create cloud appliance.</span></span>
* <span data-ttu-id="6f852-114">**Dispositivos** – os trabalhos são iniciados em um determinado serviço de tooyour dispositivo conectado.</span><span class="sxs-lookup"><span data-stu-id="6f852-114">**Devices** – Jobs are initiated on a certain device connected tooyour service.</span></span>
  
<span data-ttu-id="6f852-115">Olá trabalhos filtrados são então tabulados com base Olá Olá seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="6f852-115">hello filtered jobs are then tabulated on hello basis of hello following attributes:</span></span>
  
* <span data-ttu-id="6f852-116">**Nome** – Backup agendado, backup manual, backup de restauração, clonar volume, fazer failover de contêineres de volume, criar volume fixado localmente, modificar volume, instalar atualizações, coletar logs de suporte ou criar dispositivo de nuvem.</span><span class="sxs-lookup"><span data-stu-id="6f852-116">**Name** – scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally pinned volume, modify volume, install updates, collect support logs, or create cloud appliance.</span></span>
* <span data-ttu-id="6f852-117">**Status** – em execução, concluídos, cancelados, com falha, em cancelamento ou concluídos com erros.</span><span class="sxs-lookup"><span data-stu-id="6f852-117">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="6f852-118">**Entidade** – trabalhos Olá podem ser associados um volume, uma política de backup ou um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6f852-118">**Entity** – hello jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="6f852-119">Por exemplo, um trabalho de clone é associado a um volume, enquanto um trabalho de backup agendado é associado a uma política de backup.</span><span class="sxs-lookup"><span data-stu-id="6f852-119">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="6f852-120">Um trabalho de dispositivo é criado como resultado de uma recuperação de desastres (DR) ou uma operação de restauração.</span><span class="sxs-lookup"><span data-stu-id="6f852-120">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
* <span data-ttu-id="6f852-121">**Dispositivo** – hello nome de dispositivo de saudação na qual Olá o trabalho foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="6f852-121">**Device** – hello name of hello device on which hello job was started.</span></span>
* <span data-ttu-id="6f852-122">**Iniciado em** – tempo de saudação quando o trabalho de saudação foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="6f852-122">**Started on** – hello time when hello job was started.</span></span>
* <span data-ttu-id="6f852-123">**Duração** – trabalho de Olá Olá tempo toocomplete necessária.</span><span class="sxs-lookup"><span data-stu-id="6f852-123">**Duration** – hello time required toocomplete hello job.</span></span>

<span data-ttu-id="6f852-124">lista de saudação de trabalhos é atualizada a cada 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="6f852-124">hello list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="6f852-125">Você pode executar Olá relacionada ao trabalho ações a seguir nesta página:</span><span class="sxs-lookup"><span data-stu-id="6f852-125">You can perform hello following job-related actions on this page:</span></span>

* <span data-ttu-id="6f852-126">Exibir detalhes do trabalho</span><span class="sxs-lookup"><span data-stu-id="6f852-126">View job details</span></span>
* <span data-ttu-id="6f852-127">Cancelar um trabalho</span><span class="sxs-lookup"><span data-stu-id="6f852-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="6f852-128">Exibir detalhes do trabalho</span><span class="sxs-lookup"><span data-stu-id="6f852-128">View job details</span></span>
<span data-ttu-id="6f852-129">Execute Olá etapas tooview Olá detalhes de qualquer trabalho a seguir.</span><span class="sxs-lookup"><span data-stu-id="6f852-129">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="6f852-130">detalhes do trabalho tooview</span><span class="sxs-lookup"><span data-stu-id="6f852-130">tooview job details</span></span>
1. <span data-ttu-id="6f852-131">Serviço de Gerenciador de dispositivos de StorSimple tooyour go e, em seguida, clique em **trabalhos**.</span><span class="sxs-lookup"><span data-stu-id="6f852-131">Go tooyour StorSimple Device Manager service and then click **Jobs**.</span></span>

2. <span data-ttu-id="6f852-132">Em Olá **trabalhos** folha, exibição hello (s) que está interessado executando uma consulta com os filtros apropriados.</span><span class="sxs-lookup"><span data-stu-id="6f852-132">In hello **Jobs** blade, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="6f852-133">É possível pesquisar trabalhos concluídos, em execução ou cancelados.</span><span class="sxs-lookup"><span data-stu-id="6f852-133">You can search for completed, running, or canceled jobs.</span></span>

    ![Folha de trabalho](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

2. <span data-ttu-id="6f852-135">Selecione e clique em um trabalho.</span><span class="sxs-lookup"><span data-stu-id="6f852-135">Select and click a job.</span></span>

    ![Folha de trabalho](./media/storsimple-8000-manage-jobs-u2/jobs3.png)

3. <span data-ttu-id="6f852-137">Na folha de detalhes do trabalho hello, você pode exibir o status de hello, detalhes, estatísticas de tempo e as estatísticas de dados.</span><span class="sxs-lookup"><span data-stu-id="6f852-137">In hello job details blade, you can view hello status, details, time statistics, and data statistics.</span></span>
   
    ![Detalhes do trabalho](./media/storsimple-8000-manage-jobs-u2/jobs4.png)

## <a name="cancel-a-job"></a><span data-ttu-id="6f852-139">Cancelar um trabalho</span><span class="sxs-lookup"><span data-stu-id="6f852-139">Cancel a job</span></span>
<span data-ttu-id="6f852-140">Execute Olá seguindo as etapas toocancel um trabalho em execução.</span><span class="sxs-lookup"><span data-stu-id="6f852-140">Perform hello following steps toocancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="6f852-141">Alguns trabalhos, como modificar um tipo de volume do volume toochange hello ou expandir um volume não podem ser cancelados.</span><span class="sxs-lookup"><span data-stu-id="6f852-141">Some jobs, such as modifying a volume toochange hello volume type or expanding a volume, cannot be canceled.</span></span>


### <a name="toocancel-a-job"></a><span data-ttu-id="6f852-142">toocancel um trabalho</span><span class="sxs-lookup"><span data-stu-id="6f852-142">toocancel a job</span></span>
1. <span data-ttu-id="6f852-143">Em Olá **trabalhos** página, exibir hello em execução (s) que você deseja toocancel executando uma consulta com os filtros apropriados.</span><span class="sxs-lookup"><span data-stu-id="6f852-143">On hello **Jobs** page, display hello running job(s) that you want toocancel by running a query with appropriate filters.</span></span> <span data-ttu-id="6f852-144">Selecione o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="6f852-144">Select hello job.</span></span>

2. <span data-ttu-id="6f852-145">Clique no menu de contexto de saudação do hello trabalho selecionado tooinvoke **Cancelar**.</span><span class="sxs-lookup"><span data-stu-id="6f852-145">Right-click on hello selected job tooinvoke hello context menu and click **Cancel**.</span></span>

    ![Detalhes do trabalho](./media/storsimple-8000-manage-jobs-u2/jobs2.png)

3. <span data-ttu-id="6f852-147">Quando solicitado a confirmar, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="6f852-147">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="6f852-148">Este trabalho agora está cancelado.</span><span class="sxs-lookup"><span data-stu-id="6f852-148">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f852-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6f852-149">Next steps</span></span>
* <span data-ttu-id="6f852-150">Saiba como muito[gerenciar suas políticas de backup StorSimple](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="6f852-150">Learn how too[manage your StorSimple backup policies](storsimple-8000-manage-backup-policies-u2.md).</span></span>
* <span data-ttu-id="6f852-151">Saiba como muito[use Olá tooadminister de serviço do Gerenciador de dispositivos de StorSimple seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="6f852-151">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

