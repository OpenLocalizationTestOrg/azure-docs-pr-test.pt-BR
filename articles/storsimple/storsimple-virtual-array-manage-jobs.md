---
title: aaaView e gerenciar trabalhos de matriz Virtual StorSimple | Microsoft Docs
description: "Descreve a página de trabalhos de serviço de Gerenciador de dispositivos de StorSimple hello e como toouse-tootrack recente e atual dos trabalhos de saudação matriz Virtual StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 31879821-b599-4609-a7f4-d4b0f658a933
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 11/11/2016
ms.author: alkohli
ms.openlocfilehash: cf3f3e7bcdfff0ff2328b7354db2482286800e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-jobs-for-hello-storsimple-virtual-array"></a><span data-ttu-id="79baf-103">Use trabalhos de tooview do serviço de Gerenciador de dispositivos de StorSimple Olá para Olá matriz Virtual StorSimple</span><span class="sxs-lookup"><span data-stu-id="79baf-103">Use hello StorSimple Device Manager service tooview jobs for hello StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="79baf-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="79baf-104">Overview</span></span>
<span data-ttu-id="79baf-105">Olá **trabalhos** folha fornece um único portal central para exibir e gerenciar trabalhos iniciados em matrizes virtuais que estão conectado tooyour serviço do Gerenciador de dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="79baf-105">hello **Jobs** blade provides a single central portal for viewing and managing jobs that are started on virtual arrays that are connected tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="79baf-106">Você pode exibir os trabalhos em execução, concluídos e com falha para vários dispositivos virtuais.</span><span class="sxs-lookup"><span data-stu-id="79baf-106">You can view running, completed, and failed jobs for multiple virtual devices.</span></span> <span data-ttu-id="79baf-107">Os resultados são apresentados em um formato tabular.</span><span class="sxs-lookup"><span data-stu-id="79baf-107">Results are presented in a tabular format.</span></span>

![Folha de trabalhos](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)

<span data-ttu-id="79baf-109">Você pode localizar rapidamente os trabalhos de saudação que está interessado ao filtrar campos, como:</span><span class="sxs-lookup"><span data-stu-id="79baf-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="79baf-110">**Intervalo de tempo** – trabalhos podem ser o intervalo de filtrado Olá com base na data e hora.</span><span class="sxs-lookup"><span data-stu-id="79baf-110">**Time range** – Jobs can be filtered based on hello date and time range.</span></span>
* <span data-ttu-id="79baf-111">**Dispositivos** – os trabalhos são iniciados em um serviço de tooyour específica do dispositivo conectado.</span><span class="sxs-lookup"><span data-stu-id="79baf-111">**Devices** – Jobs are initiated on a specific device connected tooyour service.</span></span> <span data-ttu-id="79baf-112">Olá trabalhos filtrados são então tabulados com base em Olá seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="79baf-112">hello filtered jobs are then tabulated based on hello following attributes:</span></span>
  
  * <span data-ttu-id="79baf-113">**Nome** – nome do trabalho Olá pode ser **todos os**, **Backup**, **Clone**, **failover**, **baixar atualizações** , ou **instalar atualizações**.</span><span class="sxs-lookup"><span data-stu-id="79baf-113">**Name** – hello job name can be **All**, **Backup**, **Clone**, **Fail over**, **Download updates**, or **Install updates**.</span></span>
  * <span data-ttu-id="79baf-114">**Status** – Os trabalhos podem ser **Todos**, **Em andamento**, **Concluídos com sucesso**, **Com falha**, ou **Cancelado**.</span><span class="sxs-lookup"><span data-stu-id="79baf-114">**Status** – Jobs can be **All**, **In progress**, **Succeeded**, or **Failed**, or **Canceled**.</span></span>
  * <span data-ttu-id="79baf-115">**Entidade** – trabalhos Olá podem ser associados um volume, compartilhamento ou dispositivo.</span><span class="sxs-lookup"><span data-stu-id="79baf-115">**Entity** – hello jobs can be associated with a volume, share, or device.</span></span>
  * <span data-ttu-id="79baf-116">**Dispositivo** – hello nome de dispositivo de saudação na qual Olá o trabalho foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="79baf-116">**Device** – hello name of hello device on which hello job was started.</span></span>
  * <span data-ttu-id="79baf-117">**Iniciado em** – tempo de saudação quando o trabalho de saudação foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="79baf-117">**Started on** – hello time when hello job was started.</span></span>
  * <span data-ttu-id="79baf-118">**Duração** – hello duração na qual trabalho Olá foi executada.</span><span class="sxs-lookup"><span data-stu-id="79baf-118">**Duration** – hello duration for on which hello job was run.</span></span>
* <span data-ttu-id="79baf-119">**Status** – você pode pesquisar todos os trabalhos em execução, concluídos ou com falha.</span><span class="sxs-lookup"><span data-stu-id="79baf-119">**Status** – You can search for all, running, completed, or failed jobs.</span></span>
* <span data-ttu-id="79baf-120">**Tipo de trabalho** – tipo de trabalho Olá pode ser all, backup, e restauração, failover, baixar atualizações ou instalar atualizações.</span><span class="sxs-lookup"><span data-stu-id="79baf-120">**Job type** – hello job type can be all, backup, restore, failover, download updates, or install updates.</span></span>

<span data-ttu-id="79baf-121">lista de saudação de trabalhos é atualizada a cada 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="79baf-121">hello list of jobs is refreshed every 30 seconds.</span></span>

## <a name="view-job-details"></a><span data-ttu-id="79baf-122">Exibir detalhes do trabalho</span><span class="sxs-lookup"><span data-stu-id="79baf-122">View job details</span></span>
<span data-ttu-id="79baf-123">Execute Olá etapas tooview Olá detalhes de qualquer trabalho a seguir.</span><span class="sxs-lookup"><span data-stu-id="79baf-123">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="79baf-124">detalhes do trabalho tooview</span><span class="sxs-lookup"><span data-stu-id="79baf-124">tooview job details</span></span>
1. <span data-ttu-id="79baf-125">Em Olá **trabalhos** folha, exibição hello (s) que está interessado executando uma consulta com os filtros apropriados.</span><span class="sxs-lookup"><span data-stu-id="79baf-125">On hello **Jobs** blade, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="79baf-126">Você pode pesquisar trabalhos concluídos ou em execução.</span><span class="sxs-lookup"><span data-stu-id="79baf-126">You can search for completed or running jobs.</span></span>
2. <span data-ttu-id="79baf-127">Selecione um trabalho na lista tabular de saudação de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="79baf-127">Select a job from hello tabular list of jobs.</span></span>
   
    ![Folha de trabalho](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)
3. <span data-ttu-id="79baf-129">Final Olá Olá página, clique em **detalhes**.</span><span class="sxs-lookup"><span data-stu-id="79baf-129">At hello bottom of hello page, click **Details**.</span></span>
4. <span data-ttu-id="79baf-130">Em Olá **detalhes** caixa de diálogo, você pode exibir o status, os detalhes e estatísticas de tempo.</span><span class="sxs-lookup"><span data-stu-id="79baf-130">In hello **Details** dialog box, you can view status, details, and time statistics.</span></span> <span data-ttu-id="79baf-131">Olá, ilustração a seguir mostra um exemplo de hello **detalhes do trabalho de Backup** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="79baf-131">hello following illustration shows an example of hello **Backup Job Details** dialog box.</span></span>
   
    ![Detalhes do trabalho](./media/storsimple-virtual-array-manage-jobs/ova-jobs-details.png)

#### <a name="job-failures-when-hello-virtual-machine-is-paused-in-hello-hypervisor"></a><span data-ttu-id="79baf-133">Falhas de trabalho quando a máquina virtual de saudação está em pausa no hipervisor Olá</span><span class="sxs-lookup"><span data-stu-id="79baf-133">Job failures when hello virtual machine is paused in hello hypervisor</span></span>
<span data-ttu-id="79baf-134">Quando um trabalho está em andamento na sua matriz Virtual do StorSimple e dispositivo hello (máquina virtual provisionada no hipervisor) está em pausa para mais de 15 minutos, Olá trabalho falhar.</span><span class="sxs-lookup"><span data-stu-id="79baf-134">When a job is in progress on your StorSimple Virtual Array and hello device (virtual machine provisioned in hypervisor) is paused for greater than 15 minutes, hello job fails.</span></span> <span data-ttu-id="79baf-135">Isso é devido ao tempo de matriz Virtual StorSimple tooyour sendo fora de sincronia com o tempo do Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="79baf-135">This is due tooyour StorSimple Virtual Array time being out of sync with hello Microsoft Azure time.</span></span> 

<span data-ttu-id="79baf-136">Você verá Olá erro a seguir: "o horário do seu dispositivo está fora de sincronia com o tempo do Microsoft Azure Olá por mais de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="79baf-136">You will see hello following error: "Your device time is out of sync with hello Microsoft Azure time by more than 15 minutes.</span></span> <span data-ttu-id="79baf-137">Certifique-se de que o hipervisor hello e tempos de dispositivo Olá sejam sincronizados com um servidor NTP.</span><span class="sxs-lookup"><span data-stu-id="79baf-137">Ensure that hello hypervisor and hello device times are synchronized with an NTP servier.</span></span> <span data-ttu-id="79baf-138">Certifique-se de que não haja nenhum problema de conectividade.</span><span class="sxs-lookup"><span data-stu-id="79baf-138">Verify that there are no connectivity issues.</span></span> <span data-ttu-id="79baf-139">tootroubleshoot problemas de conectividade, execute testes de diagnóstico da web local de saudação da interface do usuário do seu dispositivo virtual."</span><span class="sxs-lookup"><span data-stu-id="79baf-139">tootroubleshoot connectivity issues, run diagnostic tests from hello local web UI of your virtual device."</span></span>

<span data-ttu-id="79baf-140">Essas falhas aplicam trabalhos toobackup, atualização, failover e restauração.</span><span class="sxs-lookup"><span data-stu-id="79baf-140">These failures apply toobackup, restore, update, and failover jobs.</span></span> <span data-ttu-id="79baf-141">Se sua máquina virtual é provisionada no Hyper-V, máquina Olá eventualmente sincroniza o tempo com o hipervisor.</span><span class="sxs-lookup"><span data-stu-id="79baf-141">If your virtual machine is provisioned in Hyper-V, hello machine eventually synchronizes time with your hypervisor.</span></span> <span data-ttu-id="79baf-142">Depois que isso acontece, você pode reiniciar seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="79baf-142">Once that happens, you can restart your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79baf-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="79baf-143">Next steps</span></span>
<span data-ttu-id="79baf-144">[Saiba como toouse Olá tooadminister de interface do usuário da web local sua matriz Virtual StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="79baf-144">[Learn how toouse hello local web UI tooadminister your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

