---
title: "Planejar a capacidade e o dimensionamento da replicação de VM do Hyper-V (sem o VMM) para o Azure com o Azure Site Recovery | Microsoft Docs"
description: Use este artigo para planejar a capacidade e a escala ao replicar VMs do Hyper-V para o Azure com o Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8687af60-5b50-481c-98ee-0750cbbc2c57
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: c7891c188c2cecbbf056fa79672a13bb16fa7fcf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-to-azure-replication"></a><span data-ttu-id="2ff5b-103">Etapa 3: Planejar a capacidade e o dimensionamento para replicação do Hyper-V para o Azure</span><span class="sxs-lookup"><span data-stu-id="2ff5b-103">Step 3: Plan capacity and scaling for Hyper-V to Azure replication</span></span>

<span data-ttu-id="2ff5b-104">Use este artigo para saber como planejar a capacidade e o dimensionamento ao replicar VMs locais do Hyper-V (sem o System Center VMM) para o Azure com o [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2ff5b-104">Use this article to figure out planning for capacity and scaling, when replicating on-premises Hyper-V VMs (without System Center VMM) to Azure with [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="2ff5b-105">Depois de ler este artigo, poste comentários no final ou faça perguntas técnicas no [Fórum dos Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="2ff5b-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="how-do-i-start-capacity-planning"></a><span data-ttu-id="2ff5b-106">Como iniciar o planejamento de capacidade?</span><span class="sxs-lookup"><span data-stu-id="2ff5b-106">How do I start capacity planning?</span></span>


<span data-ttu-id="2ff5b-107">Você coleta informações sobre o ambiente de replicação e, em seguida, planeja a capacidade usando essas informações, junto com as considerações destacadas neste artigo.</span><span class="sxs-lookup"><span data-stu-id="2ff5b-107">You gather information about your replication environment, and then plan capacity using this information, together with the considerations highlighted in this article.</span></span>


## <a name="gather-information"></a><span data-ttu-id="2ff5b-108">Coletar informações</span><span class="sxs-lookup"><span data-stu-id="2ff5b-108">Gather information</span></span>

1. <span data-ttu-id="2ff5b-109">Reunir informações sobre seu ambiente de replicação, inclusive VMs, discos por VMs e armazenamento por disco.</span><span class="sxs-lookup"><span data-stu-id="2ff5b-109">Gather information about your replication environment, including VMs, disks per VMs, and storage per disk.</span></span>
2. <span data-ttu-id="2ff5b-110">Identifique sua taxa de alteração (variação) diária de dados replicados.</span><span class="sxs-lookup"><span data-stu-id="2ff5b-110">Identify your daily change (churn) rate for replicated data.</span></span> <span data-ttu-id="2ff5b-111">Baixe a [ferramenta de planejamento de capacidade do Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) para obter a taxa de alteração.</span><span class="sxs-lookup"><span data-stu-id="2ff5b-111">Download the [Hyper-V capacity planning tool](https://www.microsoft.com/download/details.aspx?id=39057) to get the change rate.</span></span> <span data-ttu-id="2ff5b-112">Recomendamos que você execute essa ferramenta durante uma semana para capturar as médias.</span><span class="sxs-lookup"><span data-stu-id="2ff5b-112">We recommend you run this tool over a week to capture averages.</span></span>
 

## <a name="figure-out-capacity"></a><span data-ttu-id="2ff5b-113">Descobrir a capacidade</span><span class="sxs-lookup"><span data-stu-id="2ff5b-113">Figure out capacity</span></span>

<span data-ttu-id="2ff5b-114">Com base nas informações coletadas, você executa o [Planejador de Capacidade do Site Recovery](http://aka.ms/asr-capacity-planner-excel) para analisar o ambiente de origem e as cargas de trabalho, estimar as necessidades de largura de banda e os recursos do servidor para o local de origem, bem como os recursos (máquinas virtuais e armazenamento, etc.) necessários no local de destino.</span><span class="sxs-lookup"><span data-stu-id="2ff5b-114">Based on the information you've gather, you run the [Site Recovery Capacity Planner Tool](http://aka.ms/asr-capacity-planner-excel) to analyze your source environment and workloads, estimate bandwidth needs and server resources for the source location, and the resources (virtual machines and storage etc), that you need in the target location.</span></span> <span data-ttu-id="2ff5b-115">Você pode executar a ferramenta em vários modos:</span><span class="sxs-lookup"><span data-stu-id="2ff5b-115">You can run the tool in a couple of modes:</span></span>

- <span data-ttu-id="2ff5b-116">Planejamento rápido: execute a ferramenta nesse modo para obter as projeções de rede e de servidor baseadas no número médio de VMs, de discos, de armazenamento e da taxa de alteração.</span><span class="sxs-lookup"><span data-stu-id="2ff5b-116">Quick planning: Run the tool in this mode to get network and server projections based on an average number of VMs, disks, storage, and change rate.</span></span>
- <span data-ttu-id="2ff5b-117">Planejamento detalhado: execute a ferramenta nesse modo e forneça detalhes de cada carga de trabalho no nível da VM.</span><span class="sxs-lookup"><span data-stu-id="2ff5b-117">Detailed planning: Run the tool in this mode, and provide details of each workload at VM level.</span></span> <span data-ttu-id="2ff5b-118">Analise a compatibilidade da VM e obtenha as projeções de rede e de servidor.</span><span class="sxs-lookup"><span data-stu-id="2ff5b-118">Analyze VM compatibility and get network and server projections.</span></span>

<span data-ttu-id="2ff5b-119">Agora execute a ferramenta:</span><span class="sxs-lookup"><span data-stu-id="2ff5b-119">Now run the tool:</span></span>

1. <span data-ttu-id="2ff5b-120">Baixar a [ferramenta](http://aka.ms/asr-capacity-planner-excel)</span><span class="sxs-lookup"><span data-stu-id="2ff5b-120">Download the [tool](http://aka.ms/asr-capacity-planner-excel)</span></span>
2. <span data-ttu-id="2ff5b-121">Para executar o planejador rápido, siga [estas instruções](site-recovery-capacity-planner.md#run-the-quick-planner) e selecione o cenário **Hyper-V para o Azure**.</span><span class="sxs-lookup"><span data-stu-id="2ff5b-121">To run the quick planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-quick-planner), and select the scenario **Hyper-V to Azure**.</span></span>
3. <span data-ttu-id="2ff5b-122">Para executar o planejador detalhado, siga [estas instruções](site-recovery-capacity-planner.md#run-the-detailed-planner) e selecione o cenário **Hyper-V para o Azure**.</span><span class="sxs-lookup"><span data-stu-id="2ff5b-122">To run the detailed planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-detailed-planner), and select the scenario **Hyper-V to Azure**.</span></span>

## <a name="control-network-bandwidth"></a><span data-ttu-id="2ff5b-123">Controlar largura de banda da rede</span><span class="sxs-lookup"><span data-stu-id="2ff5b-123">Control network bandwidth</span></span>

<span data-ttu-id="2ff5b-124">Depois de calcular a largura de banda necessária, você tem algumas opções para controlar a quantidade de largura de banda usada para replicação:</span><span class="sxs-lookup"><span data-stu-id="2ff5b-124">After you've calculated the bandwidth you need, you have a couple of options for controlling the amount of bandwidth used for replication:</span></span>

* <span data-ttu-id="2ff5b-125">**Restringir a largura de banda**: o tráfego do Hyper-V replicado para o Azure passa por um host específico do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="2ff5b-125">**Throttle bandwidth**: Hyper-V traffic that replicates to Azure goes through a specific Hyper-V host.</span></span> <span data-ttu-id="2ff5b-126">Você pode limitar a largura de banda no servidor host.</span><span class="sxs-lookup"><span data-stu-id="2ff5b-126">You can throttle bandwidth on the host server.</span></span>
* <span data-ttu-id="2ff5b-127">**Influenciar a largura de banda**: você pode influenciar a largura de banda usada para replicação usando algumas chaves do Registro.</span><span class="sxs-lookup"><span data-stu-id="2ff5b-127">**Influence bandwidth**: You can influence the bandwidth used for replication using a couple of registry keys.</span></span>

### <a name="throttle-bandwidth"></a><span data-ttu-id="2ff5b-128">Restringir a largura de banda</span><span class="sxs-lookup"><span data-stu-id="2ff5b-128">Throttle bandwidth</span></span>
1. <span data-ttu-id="2ff5b-129">Abra o snap-in MMC do Backup do Microsoft Azure no servidor host do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="2ff5b-129">Open the Microsoft Azure Backup MMC snap-in on the Hyper-V host server.</span></span> <span data-ttu-id="2ff5b-130">Por padrão, um atalho para o Backup do Microsoft Azure está disponível na área de trabalho ou C:\Arquivos de Programas\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span><span class="sxs-lookup"><span data-stu-id="2ff5b-130">By default a shortcut for Microsoft Azure Backup is available on the desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="2ff5b-131">No snap-in, clique em **Alterar Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="2ff5b-131">In the snap-in click **Change Properties**.</span></span>
3. <span data-ttu-id="2ff5b-132">Na guia **Limitação**, selecione **Habilitar limitação de uso de largura de banda da Internet para operações de backup** e defina os limites do horário comercial e não comercial.</span><span class="sxs-lookup"><span data-stu-id="2ff5b-132">On the **Throttling** tab select **Enable internet bandwidth usage throttling for backup operations**, and set the limits for work and non-work hours.</span></span> <span data-ttu-id="2ff5b-133">Os intervalos válidos são de 512 Kbps a 102 Mbps por segundo.</span><span class="sxs-lookup"><span data-stu-id="2ff5b-133">Valid ranges are from 512 Kbps to 102 Mbps per second.</span></span>

    ![Restringir a largura de banda](./media/hyper-v-site-walkthrough-capacity/throttle2.png)

<span data-ttu-id="2ff5b-135">Você também pode usar o cmdlet [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) para definir a limitação.</span><span class="sxs-lookup"><span data-stu-id="2ff5b-135">You can also use the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet to set throttling.</span></span> <span data-ttu-id="2ff5b-136">Veja um exemplo:</span><span class="sxs-lookup"><span data-stu-id="2ff5b-136">Here's a sample:</span></span>

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

<span data-ttu-id="2ff5b-137">**Set-OBMachineSetting -NoThrottle** indica que nenhuma limitação é necessária.</span><span class="sxs-lookup"><span data-stu-id="2ff5b-137">**Set-OBMachineSetting -NoThrottle** indicates that no throttling is required.</span></span>

### <a name="influence-network-bandwidth"></a><span data-ttu-id="2ff5b-138">Influência da largura de banda de rede</span><span class="sxs-lookup"><span data-stu-id="2ff5b-138">Influence network bandwidth</span></span>
1. <span data-ttu-id="2ff5b-139">No Registro, navegue até **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span><span class="sxs-lookup"><span data-stu-id="2ff5b-139">In the registry navigate to **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span></span>
   * <span data-ttu-id="2ff5b-140">Para influenciar o tráfego de largura de banda em um disco de replicação, modifique o valor de **UploadThreadsPerVM**ou crie a chave caso ela não exista.</span><span class="sxs-lookup"><span data-stu-id="2ff5b-140">To influence the bandwidth traffic on a replicating disk, modify the value the **UploadThreadsPerVM**, or create the key if it doesn't exist.</span></span>
   * <span data-ttu-id="2ff5b-141">Para influenciar a largura de banda para o tráfego de failback do Azure, modifique o valor **DownloadThreadsPerVM**.</span><span class="sxs-lookup"><span data-stu-id="2ff5b-141">To influence the bandwidth for failback traffic from Azure, modify the value **DownloadThreadsPerVM**.</span></span>
2. <span data-ttu-id="2ff5b-142">O valor padrão é 4.</span><span class="sxs-lookup"><span data-stu-id="2ff5b-142">The default value is 4.</span></span> <span data-ttu-id="2ff5b-143">Em uma rede "sobreprovisionada", os valores padrão dessas chaves do registro precisam ser alterados.</span><span class="sxs-lookup"><span data-stu-id="2ff5b-143">In an “overprovisioned” network, these registry keys should be changed from the default values.</span></span> <span data-ttu-id="2ff5b-144">O máximo é 32.</span><span class="sxs-lookup"><span data-stu-id="2ff5b-144">The maximum is 32.</span></span> <span data-ttu-id="2ff5b-145">Monitore o tráfego para otimizar o valor.</span><span class="sxs-lookup"><span data-stu-id="2ff5b-145">Monitor traffic to optimize the value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ff5b-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2ff5b-146">Next steps</span></span>

<span data-ttu-id="2ff5b-147">Ir para a [Etapa 4: Planejar a rede](hyper-v-site-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="2ff5b-147">Go to [Step 4: Plan networking](hyper-v-site-walkthrough-network.md).</span></span>
