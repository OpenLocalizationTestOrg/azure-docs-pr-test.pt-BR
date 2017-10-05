---
title: Exibir e gerenciar trabalhos do StorSimple Virtual Array | Microsoft Docs
description: "Descreve a página de Trabalhos do serviço do Gerenciador de Dispositivos StorSimple e como usá-la para controlar trabalhos recentes e atuais para a Matriz Virtual StorSimple."
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
ms.openlocfilehash: 3fd1c262a8ce94d8e98f2b066a8028d974b15b1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-view-jobs-for-the-storsimple-virtual-array"></a><span data-ttu-id="202b3-103">Use o serviço do Gerenciador de Dispositivos StorSimple para exibir os trabalhos para a Matriz Virtual StorSimple</span><span class="sxs-lookup"><span data-stu-id="202b3-103">Use the StorSimple Device Manager service to view jobs for the StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="202b3-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="202b3-104">Overview</span></span>
<span data-ttu-id="202b3-105">A folha **Trabalhos** fornece um único portal central para exibir e gerenciar trabalhos iniciados em matrizes virtuais que estão conectadas ao serviço do Gerenciador de Dispositivos StorSimple.</span><span class="sxs-lookup"><span data-stu-id="202b3-105">The **Jobs** blade provides a single central portal for viewing and managing jobs that are started on virtual arrays that are connected to your StorSimple Device Manager service.</span></span> <span data-ttu-id="202b3-106">Você pode exibir os trabalhos em execução, concluídos e com falha para vários dispositivos virtuais.</span><span class="sxs-lookup"><span data-stu-id="202b3-106">You can view running, completed, and failed jobs for multiple virtual devices.</span></span> <span data-ttu-id="202b3-107">Os resultados são apresentados em um formato tabular.</span><span class="sxs-lookup"><span data-stu-id="202b3-107">Results are presented in a tabular format.</span></span>

![Folha de trabalhos](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)

<span data-ttu-id="202b3-109">Você pode localizar rapidamente os trabalhos nos quais está interessado filtrando os campos, como:</span><span class="sxs-lookup"><span data-stu-id="202b3-109">You can quickly find the jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="202b3-110">**Intervalo de tempo** – Os trabalhos podem ser filtrados com base no intervalo de data e hora.</span><span class="sxs-lookup"><span data-stu-id="202b3-110">**Time range** – Jobs can be filtered based on the date and time range.</span></span>
* <span data-ttu-id="202b3-111">**Dispositivos** – os trabalhos são iniciados em um dispositivo específico conectado ao seu serviço.</span><span class="sxs-lookup"><span data-stu-id="202b3-111">**Devices** – Jobs are initiated on a specific device connected to your service.</span></span> <span data-ttu-id="202b3-112">Os trabalhos filtrados são então tabulados com base nos seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="202b3-112">The filtered jobs are then tabulated based on the following attributes:</span></span>
  
  * <span data-ttu-id="202b3-113">**Nome** – O nome do trabalho pode ser **Todos**, **Backup**, **Clone**, **Failover**, **Baixar atualizações** ou **Instalar atualizações**.</span><span class="sxs-lookup"><span data-stu-id="202b3-113">**Name** – The job name can be **All**, **Backup**, **Clone**, **Fail over**, **Download updates**, or **Install updates**.</span></span>
  * <span data-ttu-id="202b3-114">**Status** – Os trabalhos podem ser **Todos**, **Em andamento**, **Concluídos com sucesso**, **Com falha**, ou **Cancelado**.</span><span class="sxs-lookup"><span data-stu-id="202b3-114">**Status** – Jobs can be **All**, **In progress**, **Succeeded**, or **Failed**, or **Canceled**.</span></span>
  * <span data-ttu-id="202b3-115">**Entidade** – os trabalhos podem ser associados a um volume, compartilhamento ou dispositivo.</span><span class="sxs-lookup"><span data-stu-id="202b3-115">**Entity** – The jobs can be associated with a volume, share, or device.</span></span>
  * <span data-ttu-id="202b3-116">**Dispositivo** – o nome do dispositivo no qual o trabalho foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="202b3-116">**Device** – The name of the device on which the job was started.</span></span>
  * <span data-ttu-id="202b3-117">**Iniciado em** – a hora em que o trabalho foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="202b3-117">**Started on** – The time when the job was started.</span></span>
  * <span data-ttu-id="202b3-118">**Duração** – a duração de execução do trabalho.</span><span class="sxs-lookup"><span data-stu-id="202b3-118">**Duration** – The duration for on which the job was run.</span></span>
* <span data-ttu-id="202b3-119">**Status** – você pode pesquisar todos os trabalhos em execução, concluídos ou com falha.</span><span class="sxs-lookup"><span data-stu-id="202b3-119">**Status** – You can search for all, running, completed, or failed jobs.</span></span>
* <span data-ttu-id="202b3-120">**Tipo de trabalho** – o tipo de trabalho pode ser todos, backup, restauração, failover, baixar atualizações ou instalar atualizações.</span><span class="sxs-lookup"><span data-stu-id="202b3-120">**Job type** – The job type can be all, backup, restore, failover, download updates, or install updates.</span></span>

<span data-ttu-id="202b3-121">A lista de trabalhos é atualizada a cada 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="202b3-121">The list of jobs is refreshed every 30 seconds.</span></span>

## <a name="view-job-details"></a><span data-ttu-id="202b3-122">Exibir detalhes do trabalho</span><span class="sxs-lookup"><span data-stu-id="202b3-122">View job details</span></span>
<span data-ttu-id="202b3-123">Execute as etapas a seguir para exibir os detalhes de qualquer trabalho.</span><span class="sxs-lookup"><span data-stu-id="202b3-123">Perform the following steps to view the details of any job.</span></span>

#### <a name="to-view-job-details"></a><span data-ttu-id="202b3-124">Para exibir detalhes do trabalho</span><span class="sxs-lookup"><span data-stu-id="202b3-124">To view job details</span></span>
1. <span data-ttu-id="202b3-125">Na folha **Trabalhos** , exiba o(s) trabalho(s) no(s) qual(is) está interessado executando uma consulta com os filtros apropriados.</span><span class="sxs-lookup"><span data-stu-id="202b3-125">On the **Jobs** blade, display the job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="202b3-126">Você pode pesquisar trabalhos concluídos ou em execução.</span><span class="sxs-lookup"><span data-stu-id="202b3-126">You can search for completed or running jobs.</span></span>
2. <span data-ttu-id="202b3-127">Selecione um trabalho na lista tabular dos trabalhos.</span><span class="sxs-lookup"><span data-stu-id="202b3-127">Select a job from the tabular list of jobs.</span></span>
   
    ![Folha de trabalho](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)
3. <span data-ttu-id="202b3-129">Na parte inferior da página, clique em **Detalhes**.</span><span class="sxs-lookup"><span data-stu-id="202b3-129">At the bottom of the page, click **Details**.</span></span>
4. <span data-ttu-id="202b3-130">Na caixa de diálogo **Detalhes** , você pode exibir o status, os detalhes e as estatísticas de tempo.</span><span class="sxs-lookup"><span data-stu-id="202b3-130">In the **Details** dialog box, you can view status, details, and time statistics.</span></span> <span data-ttu-id="202b3-131">A ilustração a seguir mostra um exemplo da caixa de diálogo **Detalhes do trabalho de Backup** .</span><span class="sxs-lookup"><span data-stu-id="202b3-131">The following illustration shows an example of the **Backup Job Details** dialog box.</span></span>
   
    ![Detalhes do trabalho](./media/storsimple-virtual-array-manage-jobs/ova-jobs-details.png)

#### <a name="job-failures-when-the-virtual-machine-is-paused-in-the-hypervisor"></a><span data-ttu-id="202b3-133">Falhas de trabalho quando a máquina virtual está em pausa no hipervisor</span><span class="sxs-lookup"><span data-stu-id="202b3-133">Job failures when the virtual machine is paused in the hypervisor</span></span>
<span data-ttu-id="202b3-134">Quando um trabalho estiver em andamento na sua Matriz Virtual StorSimple e o dispositivo (a máquina virtual provisionada no hipervisor) estiver em pausa há mais de 15 minutos, o trabalho falhará.</span><span class="sxs-lookup"><span data-stu-id="202b3-134">When a job is in progress on your StorSimple Virtual Array and the device (virtual machine provisioned in hypervisor) is paused for greater than 15 minutes, the job fails.</span></span> <span data-ttu-id="202b3-135">Isso ocorre devido ao tempo StorSimple Virtual Array estar fora de sincronia com a hora do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="202b3-135">This is due to your StorSimple Virtual Array time being out of sync with the Microsoft Azure time.</span></span> 

<span data-ttu-id="202b3-136">Você verá o seguinte erro: "A hora do dispositivo está fora de sincronia com a hora do Microsoft Azure por mais de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="202b3-136">You will see the following error: "Your device time is out of sync with the Microsoft Azure time by more than 15 minutes.</span></span> <span data-ttu-id="202b3-137">Certifique-se de que os horários do hipervisor e do dispositivo são sincronizados com um servidor NTP.</span><span class="sxs-lookup"><span data-stu-id="202b3-137">Ensure that the hypervisor and the device times are synchronized with an NTP servier.</span></span> <span data-ttu-id="202b3-138">Certifique-se de que não haja nenhum problema de conectividade.</span><span class="sxs-lookup"><span data-stu-id="202b3-138">Verify that there are no connectivity issues.</span></span> <span data-ttu-id="202b3-139">Para solucionar problemas de conectividade, execute testes de diagnóstico da interface do usuário da Web local do seu dispositivo virtual."</span><span class="sxs-lookup"><span data-stu-id="202b3-139">To troubleshoot connectivity issues, run diagnostic tests from the local web UI of your virtual device."</span></span>

<span data-ttu-id="202b3-140">Essas falhas aplicam-se aos trabalhos de backup, restauração, atualização e failover.</span><span class="sxs-lookup"><span data-stu-id="202b3-140">These failures apply to backup, restore, update, and failover jobs.</span></span> <span data-ttu-id="202b3-141">Se sua máquina virtual for provisionada no Hyper-V, ela eventualmente sincroniza a hora com o hipervisor.</span><span class="sxs-lookup"><span data-stu-id="202b3-141">If your virtual machine is provisioned in Hyper-V, the machine eventually synchronizes time with your hypervisor.</span></span> <span data-ttu-id="202b3-142">Depois que isso acontece, você pode reiniciar seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="202b3-142">Once that happens, you can restart your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="202b3-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="202b3-143">Next steps</span></span>
<span data-ttu-id="202b3-144">[Saiba como usar a interface do usuário da Web local para administrar sua StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="202b3-144">[Learn how to use the local web UI to administer your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

