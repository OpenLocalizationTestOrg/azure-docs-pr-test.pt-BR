---
title: "Exibir e gerenciar trabalhos para o StorSimple série 8000 | Microsoft Docs"
description: "Descreve a folha Trabalhos do serviço do Gerenciador de Dispositivos do StorSimple e como usá-la para acompanhar os trabalhos de backup recentes, atuais e agendados."
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
ms.openlocfilehash: bf8038b7171053b75eeb9aed88bff4246e65a8a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-view-and-manage-jobs-update-3-and-later"></a><span data-ttu-id="a7eba-103">Use o serviço do Gerenciador de Dispositivos do StorSimple para exibir e gerenciar trabalhos (Atualização 3 e posterior)</span><span class="sxs-lookup"><span data-stu-id="a7eba-103">Use the StorSimple Device Manager service to view and manage jobs (Update 3 and later)</span></span>

## <a name="overview"></a><span data-ttu-id="a7eba-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a7eba-104">Overview</span></span>
<span data-ttu-id="a7eba-105">A folha **Trabalhos** fornece um portal central único para exibir e gerenciar trabalhos que foram iniciados em dispositivos conectados ao serviço do Gerenciador de Dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a7eba-105">The **Jobs** blade provides a single central portal for viewing and managing jobs that were started on devices connected to your StorSimple Device Manager service.</span></span> <span data-ttu-id="a7eba-106">É possível exibir os trabalhos agendados, em execução, concluídos, cancelados e com falha para vários dispositivos.</span><span class="sxs-lookup"><span data-stu-id="a7eba-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="a7eba-107">Os resultados são apresentados em um formato tabular.</span><span class="sxs-lookup"><span data-stu-id="a7eba-107">Results are presented in a tabular format.</span></span>

![Folha de trabalhos](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

<span data-ttu-id="a7eba-109">Você pode localizar rapidamente os trabalhos nos quais está interessado filtrando os campos, como:</span><span class="sxs-lookup"><span data-stu-id="a7eba-109">You can quickly find the jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="a7eba-110">**Status** – Os trabalhos podem estar em andamento, ser bem-sucedidos, cancelados ou concluídos com falha.</span><span class="sxs-lookup"><span data-stu-id="a7eba-110">**Status** – Jobs can be in progress, succeeded, canceled, failed, canceling, or succeeded with errors.</span></span>
* <span data-ttu-id="a7eba-111">**Intervalo de tempo** – Os trabalhos podem ser filtrados com base no intervalo de data e hora.</span><span class="sxs-lookup"><span data-stu-id="a7eba-111">**Time range** – Jobs can be filtered based on the date and time range.</span></span> <span data-ttu-id="a7eba-112">Os intervalos são última hora, últimas 24 horas, últimos 7 dias, últimos 30 dias, último ano ou datas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="a7eba-112">The ranges are past 1 hour, past 24 hours, past 7 days, past 30 days, past year, or custom date.</span></span>
* <span data-ttu-id="a7eba-113">**Tipo** – O tipo do trabalho pode ser backup agendado, backup manual, backup de restauração, clonar volume, fazer failover de contêineres de volume, criar volume fixado localmente, modificar volume, instalar atualizações, coletar logs de suporte e criar dispositivo de nuvem.</span><span class="sxs-lookup"><span data-stu-id="a7eba-113">**Type** – The job type can be scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally-pinned volume, modify volume, install updates, collect support logs and create cloud appliance.</span></span>
* <span data-ttu-id="a7eba-114">**Dispositivos** – os trabalhos são iniciados em um determinado dispositivo conectado ao seu serviço.</span><span class="sxs-lookup"><span data-stu-id="a7eba-114">**Devices** – Jobs are initiated on a certain device connected to your service.</span></span>
  
<span data-ttu-id="a7eba-115">Os trabalhos filtrados são então tabulados com base nos seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="a7eba-115">The filtered jobs are then tabulated on the basis of the following attributes:</span></span>
  
* <span data-ttu-id="a7eba-116">**Nome** – Backup agendado, backup manual, backup de restauração, clonar volume, fazer failover de contêineres de volume, criar volume fixado localmente, modificar volume, instalar atualizações, coletar logs de suporte ou criar dispositivo de nuvem.</span><span class="sxs-lookup"><span data-stu-id="a7eba-116">**Name** – scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally pinned volume, modify volume, install updates, collect support logs, or create cloud appliance.</span></span>
* <span data-ttu-id="a7eba-117">**Status** – em execução, concluídos, cancelados, com falha, em cancelamento ou concluídos com erros.</span><span class="sxs-lookup"><span data-stu-id="a7eba-117">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="a7eba-118">**Entidade** – os trabalhos podem ser associados a um volume, uma política de backup ou um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a7eba-118">**Entity** – The jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="a7eba-119">Por exemplo, um trabalho de clone é associado a um volume, enquanto um trabalho de backup agendado é associado a uma política de backup.</span><span class="sxs-lookup"><span data-stu-id="a7eba-119">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="a7eba-120">Um trabalho de dispositivo é criado como resultado de uma recuperação de desastres (DR) ou uma operação de restauração.</span><span class="sxs-lookup"><span data-stu-id="a7eba-120">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
* <span data-ttu-id="a7eba-121">**Dispositivo** – o nome do dispositivo no qual o trabalho foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="a7eba-121">**Device** – The name of the device on which the job was started.</span></span>
* <span data-ttu-id="a7eba-122">**Iniciado em** – a hora em que o trabalho foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="a7eba-122">**Started on** – The time when the job was started.</span></span>
* <span data-ttu-id="a7eba-123">**Duração** – O tempo necessário para concluir o trabalho.</span><span class="sxs-lookup"><span data-stu-id="a7eba-123">**Duration** – The time required to complete the job.</span></span>

<span data-ttu-id="a7eba-124">A lista de trabalhos é atualizada a cada 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="a7eba-124">The list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="a7eba-125">É possível executar as seguintes ações relacionadas a trabalho nesta página:</span><span class="sxs-lookup"><span data-stu-id="a7eba-125">You can perform the following job-related actions on this page:</span></span>

* <span data-ttu-id="a7eba-126">Exibir detalhes do trabalho</span><span class="sxs-lookup"><span data-stu-id="a7eba-126">View job details</span></span>
* <span data-ttu-id="a7eba-127">Cancelar um trabalho</span><span class="sxs-lookup"><span data-stu-id="a7eba-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="a7eba-128">Exibir detalhes do trabalho</span><span class="sxs-lookup"><span data-stu-id="a7eba-128">View job details</span></span>
<span data-ttu-id="a7eba-129">Execute as etapas a seguir para exibir os detalhes de qualquer trabalho.</span><span class="sxs-lookup"><span data-stu-id="a7eba-129">Perform the following steps to view the details of any job.</span></span>

#### <a name="to-view-job-details"></a><span data-ttu-id="a7eba-130">Para exibir detalhes do trabalho</span><span class="sxs-lookup"><span data-stu-id="a7eba-130">To view job details</span></span>
1. <span data-ttu-id="a7eba-131">Acesse o serviço do Gerenciador de Dispositivos do StorSimple e clique em **Trabalhos**.</span><span class="sxs-lookup"><span data-stu-id="a7eba-131">Go to your StorSimple Device Manager service and then click **Jobs**.</span></span>

2. <span data-ttu-id="a7eba-132">Na folha **Trabalhos**, exiba os trabalhos de seu interesse executando uma consulta com os filtros apropriados.</span><span class="sxs-lookup"><span data-stu-id="a7eba-132">In the **Jobs** blade, display the job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="a7eba-133">É possível pesquisar trabalhos concluídos, em execução ou cancelados.</span><span class="sxs-lookup"><span data-stu-id="a7eba-133">You can search for completed, running, or canceled jobs.</span></span>

    ![Folha de trabalho](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

2. <span data-ttu-id="a7eba-135">Selecione e clique em um trabalho.</span><span class="sxs-lookup"><span data-stu-id="a7eba-135">Select and click a job.</span></span>

    ![Folha de trabalho](./media/storsimple-8000-manage-jobs-u2/jobs3.png)

3. <span data-ttu-id="a7eba-137">Na folha de detalhes do trabalho, é possível exibir o status, os detalhes, as estatísticas de tempo e as estatísticas de dados.</span><span class="sxs-lookup"><span data-stu-id="a7eba-137">In the job details blade, you can view the status, details, time statistics, and data statistics.</span></span>
   
    ![Detalhes do trabalho](./media/storsimple-8000-manage-jobs-u2/jobs4.png)

## <a name="cancel-a-job"></a><span data-ttu-id="a7eba-139">Cancelar um trabalho</span><span class="sxs-lookup"><span data-stu-id="a7eba-139">Cancel a job</span></span>
<span data-ttu-id="a7eba-140">Realize as etapas a seguir para cancelar um trabalho em execução.</span><span class="sxs-lookup"><span data-stu-id="a7eba-140">Perform the following steps to cancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="a7eba-141">Alguns trabalhos, como modificar um volume para alterar o tipo de volume ou expandir um volume, não podem ser cancelados.</span><span class="sxs-lookup"><span data-stu-id="a7eba-141">Some jobs, such as modifying a volume to change the volume type or expanding a volume, cannot be canceled.</span></span>


### <a name="to-cancel-a-job"></a><span data-ttu-id="a7eba-142">Para cancelar um trabalho</span><span class="sxs-lookup"><span data-stu-id="a7eba-142">To cancel a job</span></span>
1. <span data-ttu-id="a7eba-143">Na página **Trabalhos** , exiba os trabalhos em execução que você deseja cancelar executando uma consulta com os filtros apropriados.</span><span class="sxs-lookup"><span data-stu-id="a7eba-143">On the **Jobs** page, display the running job(s) that you want to cancel by running a query with appropriate filters.</span></span> <span data-ttu-id="a7eba-144">Selecione o trabalho.</span><span class="sxs-lookup"><span data-stu-id="a7eba-144">Select the job.</span></span>

2. <span data-ttu-id="a7eba-145">Clique com botão direito do mouse sobre o trabalho selecionado para invocar o menu de contexto e clique em **Cancelar**.</span><span class="sxs-lookup"><span data-stu-id="a7eba-145">Right-click on the selected job to invoke the context menu and click **Cancel**.</span></span>

    ![Detalhes do trabalho](./media/storsimple-8000-manage-jobs-u2/jobs2.png)

3. <span data-ttu-id="a7eba-147">Quando solicitado a confirmar, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="a7eba-147">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="a7eba-148">Este trabalho agora está cancelado.</span><span class="sxs-lookup"><span data-stu-id="a7eba-148">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7eba-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a7eba-149">Next steps</span></span>
* <span data-ttu-id="a7eba-150">Saiba como [gerenciar as políticas de backup do StorSimple](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="a7eba-150">Learn how to [manage your StorSimple backup policies](storsimple-8000-manage-backup-policies-u2.md).</span></span>
* <span data-ttu-id="a7eba-151">Saiba como [usar o serviço Gerenciador de Dispositivos do StorSimple para administrar o dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="a7eba-151">Learn how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

