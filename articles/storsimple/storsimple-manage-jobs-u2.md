---
title: Exibir e gerenciar trabalhos do StorSimple | Microsoft Docs
description: "Descreve a página de Trabalhos do serviço StorSimple Manager e como usá-la para controlar os trabalhos de backup recentes, atuais e agendados."
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
ms.openlocfilehash: 6df1b27ce76de7a781ecc40af8430114d80b20d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-view-and-manage-storsimple-jobs-update-2"></a><span data-ttu-id="895da-103">Use o serviço StorSimple Manager para exibir e gerenciar trabalhos do StorSimple (Atualização 2)</span><span class="sxs-lookup"><span data-stu-id="895da-103">Use the StorSimple Manager service to view and manage StorSimple jobs (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a><span data-ttu-id="895da-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="895da-104">Overview</span></span>
<span data-ttu-id="895da-105">A página **Trabalhos** oferece um portal central único para visualização e gerenciamento de trabalhos que foram iniciados em dispositivos conectados ao serviço StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="895da-105">The **Jobs** page provides a single central portal for viewing and managing jobs that were started on devices connected to your StorSimple Manager service.</span></span> <span data-ttu-id="895da-106">É possível exibir os trabalhos agendados, em execução, concluídos, cancelados e com falha para vários dispositivos.</span><span class="sxs-lookup"><span data-stu-id="895da-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="895da-107">Os resultados são apresentados em um formato tabular.</span><span class="sxs-lookup"><span data-stu-id="895da-107">Results are presented in a tabular format.</span></span> 

![Página Trabalhos](./media/storsimple-manage-jobs-u2/jobs.png)

<span data-ttu-id="895da-109">Você pode localizar rapidamente os trabalhos nos quais está interessado filtrando os campos, como:</span><span class="sxs-lookup"><span data-stu-id="895da-109">You can quickly find the jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="895da-110">**Status** – os trabalhos podem estar em execução, concluídos, cancelados, com falha, em cancelamento ou concluídos com erros.</span><span class="sxs-lookup"><span data-stu-id="895da-110">**Status** – Jobs can be running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="895da-111">**De e Para** – os trabalhos podem ser filtrados com base no intervalo de data e hora.</span><span class="sxs-lookup"><span data-stu-id="895da-111">**From and To** – Jobs can be filtered based on the date and time range.</span></span>
* <span data-ttu-id="895da-112">**Tipo** – o tipo de trabalho pode ser backup, backup manual, restauração, clonagem, failover de dispositivo, criação de volume fixado localmente, modificação de volume, atualização, pacote de suporte ou provisionamento do dispositivo virtual.</span><span class="sxs-lookup"><span data-stu-id="895da-112">**Type** – The job type can be backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
* <span data-ttu-id="895da-113">**Dispositivos** – os trabalhos são iniciados em um determinado dispositivo conectado ao seu serviço.</span><span class="sxs-lookup"><span data-stu-id="895da-113">**Devices** – Jobs are initiated on a certain device connected to your service.</span></span>
  <span data-ttu-id="895da-114">Os trabalhos filtrados são então tabulados com base nos seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="895da-114">The filtered jobs are then tabulated on the basis of the following attributes:</span></span>
  
  * <span data-ttu-id="895da-115">**Tipo** – backup, backup manual, restauração, clonagem, failover de dispositivo, criação de volume fixado localmente, modificação de volume, atualização, pacote de suporte ou provisionamento do dispositivo virtual.</span><span class="sxs-lookup"><span data-stu-id="895da-115">**Type** – backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
  * <span data-ttu-id="895da-116">**Status** – em execução, concluídos, cancelados, com falha, em cancelamento ou concluídos com erros.</span><span class="sxs-lookup"><span data-stu-id="895da-116">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
  * <span data-ttu-id="895da-117">**Entidade** – os trabalhos podem ser associados a um volume, uma política de backup ou um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="895da-117">**Entity** – The jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="895da-118">Por exemplo, um trabalho de clone é associado a um volume, enquanto um trabalho de backup agendado é associado a uma política de backup.</span><span class="sxs-lookup"><span data-stu-id="895da-118">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="895da-119">Um trabalho de dispositivo é criado como resultado de uma recuperação de desastres (DR) ou uma operação de restauração.</span><span class="sxs-lookup"><span data-stu-id="895da-119">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
  * <span data-ttu-id="895da-120">**Dispositivo** – o nome do dispositivo no qual o trabalho foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="895da-120">**Device** – The name of the device on which the job was started.</span></span>
  * <span data-ttu-id="895da-121">**Iniciado em** – a hora em que o trabalho foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="895da-121">**Started on** – The time when the job was started.</span></span>
  * <span data-ttu-id="895da-122">**Andamento** – o percentual de conclusão de um trabalho em execução.</span><span class="sxs-lookup"><span data-stu-id="895da-122">**Progress** – The percentage completion of a running job.</span></span> <span data-ttu-id="895da-123">Para um trabalho concluído, sempre deve ser 100%.</span><span class="sxs-lookup"><span data-stu-id="895da-123">For a completed job, this should always be 100%.</span></span>

<span data-ttu-id="895da-124">A lista de trabalhos é atualizada a cada 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="895da-124">The list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="895da-125">É possível executar as seguintes ações relacionadas a trabalho nesta página:</span><span class="sxs-lookup"><span data-stu-id="895da-125">You can perform the following job-related actions on this page:</span></span>

* <span data-ttu-id="895da-126">Exibir detalhes do trabalho</span><span class="sxs-lookup"><span data-stu-id="895da-126">View job details</span></span>
* <span data-ttu-id="895da-127">Cancelar um trabalho</span><span class="sxs-lookup"><span data-stu-id="895da-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="895da-128">Exibir detalhes do trabalho</span><span class="sxs-lookup"><span data-stu-id="895da-128">View job details</span></span>
<span data-ttu-id="895da-129">Execute as etapas a seguir para exibir os detalhes de qualquer trabalho.</span><span class="sxs-lookup"><span data-stu-id="895da-129">Perform the following steps to view the details of any job.</span></span>

#### <a name="to-view-job-details"></a><span data-ttu-id="895da-130">Para exibir detalhes do trabalho</span><span class="sxs-lookup"><span data-stu-id="895da-130">To view job details</span></span>
1. <span data-ttu-id="895da-131">Na página **Trabalhos** , exiba o(s) trabalho(s) no(s) qual(is) está interessado executando uma consulta com os filtros apropriados.</span><span class="sxs-lookup"><span data-stu-id="895da-131">On the **Jobs** page, display the job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="895da-132">É possível pesquisar trabalhos concluídos, em execução ou cancelados.</span><span class="sxs-lookup"><span data-stu-id="895da-132">You can search for completed, running, or canceled jobs.</span></span>
2. <span data-ttu-id="895da-133">Selecione um trabalho.</span><span class="sxs-lookup"><span data-stu-id="895da-133">Select a job.</span></span>
3. <span data-ttu-id="895da-134">Na parte inferior da página, clique em **Detalhes**.</span><span class="sxs-lookup"><span data-stu-id="895da-134">At the bottom of the page, click **Details**.</span></span>
4. <span data-ttu-id="895da-135">Na caixa de diálogo **Detalhes do Trabalho de Backup** , é possível exibir o status, os detalhes, as estatísticas de tempo e as estatísticas de dados.</span><span class="sxs-lookup"><span data-stu-id="895da-135">In the **Backup Job Details** dialog box, you can view the status, details, time statistics, and data statistics.</span></span>
   
    ![Página de detalhes do trabalho](./media/storsimple-manage-jobs-u2/JobDetails.png)

## <a name="cancel-a-job"></a><span data-ttu-id="895da-137">Cancelar um trabalho</span><span class="sxs-lookup"><span data-stu-id="895da-137">Cancel a job</span></span>
<span data-ttu-id="895da-138">Realize as etapas a seguir para cancelar um trabalho em execução.</span><span class="sxs-lookup"><span data-stu-id="895da-138">Perform the following steps to cancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="895da-139">Alguns trabalhos, como modificar um volume para alterar o tipo de volume ou expandir um volume, não podem ser cancelados.</span><span class="sxs-lookup"><span data-stu-id="895da-139">Some jobs, such as modifying a volume to change the volume type or expanding a volume, cannot be canceled.</span></span>
> 
> 

### <a name="to-cancel-a-job"></a><span data-ttu-id="895da-140">Para cancelar um trabalho</span><span class="sxs-lookup"><span data-stu-id="895da-140">To cancel a job</span></span>
1. <span data-ttu-id="895da-141">Na página **Trabalhos** , exiba os trabalhos em execução que você deseja cancelar executando uma consulta com os filtros apropriados.</span><span class="sxs-lookup"><span data-stu-id="895da-141">On the **Jobs** page, display the running job(s) that you want to cancel by running a query with appropriate filters.</span></span>
2. <span data-ttu-id="895da-142">Selecione o trabalho.</span><span class="sxs-lookup"><span data-stu-id="895da-142">Select the job.</span></span>
3. <span data-ttu-id="895da-143">Na parte inferior da página, clique em **Cancelar**.</span><span class="sxs-lookup"><span data-stu-id="895da-143">At the bottom of the page, click **Cancel**.</span></span>
4. <span data-ttu-id="895da-144">Quando solicitado a confirmar, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="895da-144">When prompted for confirmation, click **Yes**.</span></span>

<span data-ttu-id="895da-145">Este trabalho agora está cancelado.</span><span class="sxs-lookup"><span data-stu-id="895da-145">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="895da-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="895da-146">Next steps</span></span>
* <span data-ttu-id="895da-147">Saiba como [gerenciar as políticas de backup do StorSimple](storsimple-manage-backup-policies.md).</span><span class="sxs-lookup"><span data-stu-id="895da-147">Learn how to [manage your StorSimple backup policies](storsimple-manage-backup-policies.md).</span></span>
* <span data-ttu-id="895da-148">Saiba como [usar o serviço StorSimple Manager para administrar seu dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="895da-148">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

