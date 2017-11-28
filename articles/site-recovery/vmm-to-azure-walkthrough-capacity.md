---
title: "aaaPlan capacidade e dimensionamento para tooAzure de replicação (com o VMM) de VM do Hyper-V com o Azure Site Recovery | Microsoft Docs"
description: "Usar essa capacidade do artigo tooplan e escala quando a replicação de máquinas virtuais do Hyper-V no VMM nuvens tooAzure, com o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 41c3c83e-6b1a-496a-8179-498c552ef0c7
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 9818ada9bb21f60ac00b3894696201b06630cb2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-with-vmm-tooazure-replication"></a><span data-ttu-id="c480c-103">Etapa 3: Planejar a capacidade e dimensionamento para a replicação do Hyper-V (com o VMM) tooAzure</span><span class="sxs-lookup"><span data-stu-id="c480c-103">Step 3: Plan capacity and scaling for Hyper-V (with VMM) tooAzure replication</span></span>

<span data-ttu-id="c480c-104">Depois que você tiver examinado Olá [os pré-requisitos de implantação](vmm-to-azure-walkthrough-prerequisites.md), use toofigure este artigo planejamento de capacidade e dimensionamento, durante a replicação local em VMs Hyper-V tooAzure de nuvens do System Center Virtual Machine Manager (VMM), com [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c480c-104">After you've reviewed hello [deployment prerequisites](vmm-to-azure-walkthrough-prerequisites.md), use this article toofigure out planning for capacity and scaling, when replicating on-premises Hyper-V VMs in System Center Virtual Machine Manager (VMM) clouds tooAzure, with [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="c480c-105">Depois de ler este artigo, postar os comentários na parte inferior da saudação ou questões técnicas Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="c480c-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="how-do-i-start-capacity-planning"></a><span data-ttu-id="c480c-106">Como iniciar o planejamento de capacidade?</span><span class="sxs-lookup"><span data-stu-id="c480c-106">How do I start capacity planning?</span></span>


<span data-ttu-id="c480c-107">Você coletar informações sobre o ambiente de replicação e capacidade de plano usando dados hello, junto com as considerações de saudação realçados neste artigo.</span><span class="sxs-lookup"><span data-stu-id="c480c-107">You gather information about your replication environment, and then plan capacity using hello data, together with hello considerations highlighted in this article.</span></span>


## <a name="gather-information"></a><span data-ttu-id="c480c-108">Coletar informações</span><span class="sxs-lookup"><span data-stu-id="c480c-108">Gather information</span></span>

1. <span data-ttu-id="c480c-109">Reunir informações sobre seu ambiente de replicação, inclusive VMs, discos por VMs e armazenamento por disco.</span><span class="sxs-lookup"><span data-stu-id="c480c-109">Gather information about your replication environment, including VMs, disks per VMs, and storage per disk.</span></span>
2. <span data-ttu-id="c480c-110">Identifique sua taxa de alteração (variação) diária de dados replicados.</span><span class="sxs-lookup"><span data-stu-id="c480c-110">Identify your daily change (churn) rate for replicated data.</span></span> <span data-ttu-id="c480c-111">Baixar Olá [ferramenta de planejamento de capacidade de Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) tooget taxa de alteração de saudação.</span><span class="sxs-lookup"><span data-stu-id="c480c-111">Download hello [Hyper-V capacity planning tool](https://www.microsoft.com/download/details.aspx?id=39057) tooget hello change rate.</span></span> <span data-ttu-id="c480c-112">Recomendamos que você execute essa ferramenta em uma semana toocapture médias.</span><span class="sxs-lookup"><span data-stu-id="c480c-112">We recommend you run this tool over a week toocapture averages.</span></span>
 

## <a name="figure-out-capacity"></a><span data-ttu-id="c480c-113">Descobrir a capacidade</span><span class="sxs-lookup"><span data-stu-id="c480c-113">Figure out capacity</span></span>

<span data-ttu-id="c480c-114">Com base nas informações de saudação que você colete, executar Olá [ferramenta de Planejador de capacidade de recuperação de Site](http://aka.ms/asr-capacity-planner-excel) tooanalyze seu ambiente de origem e cargas de trabalho, estimar as necessidades de largura de banda e recursos do servidor para o local de origem hello e Olá recursos (máquinas virtuais e armazenamento etc), que é necessário no local de destino hello.</span><span class="sxs-lookup"><span data-stu-id="c480c-114">Based on hello information you've gather, you run hello [Site Recovery Capacity Planner Tool](http://aka.ms/asr-capacity-planner-excel) tooanalyze your source environment and workloads, estimate bandwidth needs and server resources for hello source location, and hello resources (virtual machines and storage etc), that you need in hello target location.</span></span> <span data-ttu-id="c480c-115">Você pode executar a ferramenta de saudação em dois modos:</span><span class="sxs-lookup"><span data-stu-id="c480c-115">You can run hello tool in a couple of modes:</span></span>

- <span data-ttu-id="c480c-116">Planejando rápida: executar ferramenta Olá nesse modo tooget projeções de rede e servidor com base em um número médio de VMs, discos, armazenamento e a taxa de alteração.</span><span class="sxs-lookup"><span data-stu-id="c480c-116">Quick planning: Run hello tool in this mode tooget network and server projections based on an average number of VMs, disks, storage, and change rate.</span></span>
- <span data-ttu-id="c480c-117">Planejamento detalhado: execute a ferramenta de saudação nesse modo e fornecer detalhes de cada carga de trabalho no nível da VM.</span><span class="sxs-lookup"><span data-stu-id="c480c-117">Detailed planning: Run hello tool in this mode, and provide details of each workload at VM level.</span></span> <span data-ttu-id="c480c-118">Analise a compatibilidade da VM e obtenha as projeções de rede e de servidor.</span><span class="sxs-lookup"><span data-stu-id="c480c-118">Analyze VM compatibility and get network and server projections.</span></span>

<span data-ttu-id="c480c-119">Agora execute a ferramenta de saudação:</span><span class="sxs-lookup"><span data-stu-id="c480c-119">Now run hello tool:</span></span>

1. <span data-ttu-id="c480c-120">Baixar Olá [ferramenta](http://aka.ms/asr-capacity-planner-excel)</span><span class="sxs-lookup"><span data-stu-id="c480c-120">Download hello [tool](http://aka.ms/asr-capacity-planner-excel)</span></span>
2. <span data-ttu-id="c480c-121">Planejador rápida do toorun hello, siga [estas instruções](site-recovery-capacity-planner.md#run-the-quick-planner)e selecione Olá cenário **tooAzure Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="c480c-121">toorun hello quick planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-quick-planner), and select hello scenario **Hyper-V tooAzure**.</span></span>
3. <span data-ttu-id="c480c-122">toorun Olá Planejador detalhada, execute [estas instruções](site-recovery-capacity-planner.md#run-the-detailed-planner)e selecione Olá cenário **tooAzure Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="c480c-122">toorun hello detailed planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-detailed-planner), and select hello scenario **Hyper-V tooAzure**.</span></span>

## <a name="control-network-bandwidth"></a><span data-ttu-id="c480c-123">Controlar largura de banda da rede</span><span class="sxs-lookup"><span data-stu-id="c480c-123">Control network bandwidth</span></span>

<span data-ttu-id="c480c-124">Depois que você tenha largura de banda Olá calculado que é necessário, você tem duas opções para controlar quantidade de saudação de largura de banda usada para replicação:</span><span class="sxs-lookup"><span data-stu-id="c480c-124">After you've calculated hello bandwidth you need, you have a couple of options for controlling hello amount of bandwidth used for replication:</span></span>

* <span data-ttu-id="c480c-125">**Limitação da largura de banda**: tráfego Hyper-V que replica tooAzure passa por um host Hyper-V específico.</span><span class="sxs-lookup"><span data-stu-id="c480c-125">**Throttle bandwidth**: Hyper-V traffic that replicates tooAzure goes through a specific Hyper-V host.</span></span> <span data-ttu-id="c480c-126">Você pode reduzir a largura de banda no servidor de host de saudação.</span><span class="sxs-lookup"><span data-stu-id="c480c-126">You can throttle bandwidth on hello host server.</span></span>
* <span data-ttu-id="c480c-127">**Influenciam a largura de banda**: você pode influenciar a largura de banda de saudação usada para replicação usando duas chaves do registro.</span><span class="sxs-lookup"><span data-stu-id="c480c-127">**Influence bandwidth**: You can influence hello bandwidth used for replication using a couple of registry keys.</span></span>

### <a name="throttle-bandwidth"></a><span data-ttu-id="c480c-128">Restringir a largura de banda</span><span class="sxs-lookup"><span data-stu-id="c480c-128">Throttle bandwidth</span></span>
1. <span data-ttu-id="c480c-129">Abra o snap-in MMC do Backup do Microsoft Azure de saudação no servidor de host do Hyper-V hello.</span><span class="sxs-lookup"><span data-stu-id="c480c-129">Open hello Microsoft Azure Backup MMC snap-in on hello Hyper-V host server.</span></span> <span data-ttu-id="c480c-130">Por padrão um atalho para o Backup do Microsoft Azure está disponível na área de trabalho hello, ou em C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span><span class="sxs-lookup"><span data-stu-id="c480c-130">By default a shortcut for Microsoft Azure Backup is available on hello desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="c480c-131">No snap-in Olá clique **alterar propriedades**.</span><span class="sxs-lookup"><span data-stu-id="c480c-131">In hello snap-in click **Change Properties**.</span></span>
3. <span data-ttu-id="c480c-132">Em Olá **limitação** guia **habilitar limitação para operações de backup do uso de largura de banda de internet**e definir limites de saudação do trabalho e folga horas.</span><span class="sxs-lookup"><span data-stu-id="c480c-132">On hello **Throttling** tab select **Enable internet bandwidth usage throttling for backup operations**, and set hello limits for work and non-work hours.</span></span> <span data-ttu-id="c480c-133">Intervalos válidos são de 512 Mbps de too102 Kbps por segundo.</span><span class="sxs-lookup"><span data-stu-id="c480c-133">Valid ranges are from 512 Kbps too102 Mbps per second.</span></span>

    ![Restringir a largura de banda](./media/vmm-to-azure-walkthrough-capacity/throttle2.png)

<span data-ttu-id="c480c-135">Você também pode usar o hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset limitação.</span><span class="sxs-lookup"><span data-stu-id="c480c-135">You can also use hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset throttling.</span></span> <span data-ttu-id="c480c-136">Veja um exemplo:</span><span class="sxs-lookup"><span data-stu-id="c480c-136">Here's a sample:</span></span>

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

<span data-ttu-id="c480c-137">**Set-OBMachineSetting -NoThrottle** indica que nenhuma limitação é necessária.</span><span class="sxs-lookup"><span data-stu-id="c480c-137">**Set-OBMachineSetting -NoThrottle** indicates that no throttling is required.</span></span>

### <a name="influence-network-bandwidth"></a><span data-ttu-id="c480c-138">Influência da largura de banda de rede</span><span class="sxs-lookup"><span data-stu-id="c480c-138">Influence network bandwidth</span></span>
1. <span data-ttu-id="c480c-139">No registro de saudação navegue muito**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span><span class="sxs-lookup"><span data-stu-id="c480c-139">In hello registry navigate too**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span></span>
   * <span data-ttu-id="c480c-140">tráfego de largura de banda de saudação tooinfluence em um disco de replicação, modificar Olá Olá do valor **UploadThreadsPerVM**, ou criar a chave de saudação se ele não existir.</span><span class="sxs-lookup"><span data-stu-id="c480c-140">tooinfluence hello bandwidth traffic on a replicating disk, modify hello value hello **UploadThreadsPerVM**, or create hello key if it doesn't exist.</span></span>
   * <span data-ttu-id="c480c-141">largura de banda tooinfluence Olá para o tráfego de failback do Azure, modifique o valor de saudação **DownloadThreadsPerVM**.</span><span class="sxs-lookup"><span data-stu-id="c480c-141">tooinfluence hello bandwidth for failback traffic from Azure, modify hello value **DownloadThreadsPerVM**.</span></span>
2. <span data-ttu-id="c480c-142">valor padrão de saudação é 4.</span><span class="sxs-lookup"><span data-stu-id="c480c-142">hello default value is 4.</span></span> <span data-ttu-id="c480c-143">Em uma rede de "sobreprovisionada", essas chaves do registro devem ser diferente dos valores padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="c480c-143">In an “overprovisioned” network, these registry keys should be changed from hello default values.</span></span> <span data-ttu-id="c480c-144">Olá máximo é 32.</span><span class="sxs-lookup"><span data-stu-id="c480c-144">hello maximum is 32.</span></span> <span data-ttu-id="c480c-145">Monitorar o tráfego toooptimize Olá valor.</span><span class="sxs-lookup"><span data-stu-id="c480c-145">Monitor traffic toooptimize hello value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c480c-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c480c-146">Next steps</span></span>

<span data-ttu-id="c480c-147">Vá muito[etapa 4: planejar a rede](vmm-to-azure-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="c480c-147">Go too[Step 4: Plan networking](vmm-to-azure-walkthrough-network.md).</span></span>
