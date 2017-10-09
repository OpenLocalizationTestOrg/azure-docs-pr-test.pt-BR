---
title: "site secundário do aaaEnable Hyper-V replicação tooa com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como a replicação para máquinas virtuais do Hyper-V replicando tooa tooenable System Center VMM secundário do site com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d8782d14-9fef-4396-8912-ff945efc851b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: b4484e0118cb23f343187fe867d9795d30926baf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-enable-replication-tooa-secondary-site-for-hyper-v-vms"></a><span data-ttu-id="e2691-103">Etapa 9: Habilitar o site secundário do tooa de replicação para máquinas virtuais do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="e2691-103">Step 9: Enable replication tooa secondary site for Hyper-V VMs</span></span>


<span data-ttu-id="e2691-104">Depois de configurar uma política de replicação, use o artigo tooenable replicação tooa System Center Virtual Machine Manager (VMM) site secundário para local Hyper-V máquinas virtuais (VM), usando [do Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e2691-104">After setting up a replication policy, use this article tooenable replication tooa secondary System Center Virtual Machine Manager (VMM) site for on-premises Hyper-V virtual machines (VM), using [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="e2691-105">Depois de ler este artigo, postar os comentários na parte inferior do hello, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="e2691-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="select-vms-tooreplicate"></a><span data-ttu-id="e2691-106">Selecione tooreplicate de VMs</span><span class="sxs-lookup"><span data-stu-id="e2691-106">Select VMs tooreplicate</span></span>

1. <span data-ttu-id="e2691-107">Clique em **Etapa 2: replicar aplicativo** > **Origem**.</span><span class="sxs-lookup"><span data-stu-id="e2691-107">Click **Step 2: Replicate application** > **Source**.</span></span> 

    ![Habilitar a replicação](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication1.png)

2. <span data-ttu-id="e2691-109">Em **fonte**, selecione o servidor do VMM hello e Olá nuvem na qual Olá hosts Hyper-V que você deseja tooreplicate estão localizados.</span><span class="sxs-lookup"><span data-stu-id="e2691-109">In **Source**, select hello VMM server, and hello cloud in which hello Hyper-V hosts you want tooreplicate are located.</span></span> <span data-ttu-id="e2691-110">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="e2691-110">Then click **OK**.</span></span>

    ![Habilitar a replicação](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication2.png)
3. <span data-ttu-id="e2691-112">Em **destino**, verifique se Olá servidor secundário do VMM e a nuvem.</span><span class="sxs-lookup"><span data-stu-id="e2691-112">In **Target**, verify hello secondary VMM server and cloud.</span></span>
4. <span data-ttu-id="e2691-113">Em **máquinas virtuais**, selecione VMs Olá deseja tooprotect da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2691-113">In **Virtual machines**, select hello VMs you want tooprotect from hello list.</span></span>

    ![Habilitar Proteção da Máquina Virtual](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication5.png)

<span data-ttu-id="e2691-115">Você pode acompanhar o progresso da saudação **Habilitar proteção** ação **trabalhos** > **trabalhos de recuperação de Site**.</span><span class="sxs-lookup"><span data-stu-id="e2691-115">You can track progress of hello **Enable Protection** action in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="e2691-116">Depois de saudação **finalizar proteção** trabalho for concluído, Olá a replicação inicial está concluída e máquina virtual de saudação está pronta para failover.</span><span class="sxs-lookup"><span data-stu-id="e2691-116">After hello **Finalize Protection** job completes, hello initial replication is complete, and hello virtual machine is ready for failover.</span></span>

<span data-ttu-id="e2691-117">Observe que:</span><span class="sxs-lookup"><span data-stu-id="e2691-117">Note that:</span></span>

- <span data-ttu-id="e2691-118">Você também pode habilitar a proteção para máquinas virtuais no console do VMM hello.</span><span class="sxs-lookup"><span data-stu-id="e2691-118">You can also enable protection for virtual machines in hello VMM console.</span></span> <span data-ttu-id="e2691-119">Clique em **Habilitar proteção** na barra de ferramentas Olá nas propriedades de máquina virtual hello > **do Azure Site Recovery** guia.</span><span class="sxs-lookup"><span data-stu-id="e2691-119">Click **Enable Protection** on hello toolbar in hello virtual machine properties > **Azure Site Recovery** tab.</span></span>
- <span data-ttu-id="e2691-120">Depois de habilitar a replicação, você pode exibir propriedades para Olá VM em **itens duplicados**.</span><span class="sxs-lookup"><span data-stu-id="e2691-120">After you've enabled replication, you can view properties for hello VM in **Replicated Items**.</span></span> <span data-ttu-id="e2691-121">Em Olá **Essentials** painel, você pode ver informações sobre a política de replicação Olá Olá VM e seu status.</span><span class="sxs-lookup"><span data-stu-id="e2691-121">On hello **Essentials** dashboard, you can see information about hello replication policy for hello VM and its status.</span></span> <span data-ttu-id="e2691-122">Clique em **Propriedades** para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="e2691-122">Click **Properties** for more details.</span></span>

## <a name="onboard-existing-vms"></a><span data-ttu-id="e2691-123">Integrar VMs existentes</span><span class="sxs-lookup"><span data-stu-id="e2691-123">Onboard existing VMs</span></span>

<span data-ttu-id="e2691-124">Se você tiver máquinas virtuais existentes no VMM replicadas com a Réplica do Hyper-V, poderá carregá-las na replicação do Azure Site Recovery da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e2691-124">If you have existing virtual machines in VMM that are replicating with Hyper-V Replica, you can onboard them for Azure Site Recovery replication as follows:</span></span>

1. <span data-ttu-id="e2691-125">Verifique se o servidor Olá Hyper-V hospeda Olá que VM existente está localizado na nuvem primária hello e servidor Hyper-V Olá Olá máquina de virtual de réplica de hospedagem está localizado na nuvem secundária hello.</span><span class="sxs-lookup"><span data-stu-id="e2691-125">Ensure that hello Hyper-V server hosting hello existing VM is located in hello primary cloud, and that hello Hyper-V server hosting hello replica virtual machine is located in hello secondary cloud.</span></span>
2. <span data-ttu-id="e2691-126">Certifique-se de que uma política de replicação é configurada para nuvem VMM primária de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2691-126">Make sure a replication policy is configured for hello primary VMM cloud.</span></span>
3. <span data-ttu-id="e2691-127">Habilite a replicação para máquina virtual primária de saudação.</span><span class="sxs-lookup"><span data-stu-id="e2691-127">Enable replication for hello primary virtual machine.</span></span> <span data-ttu-id="e2691-128">Do Azure Site Recovery e o VMM Certifique-se de que hello mesmo host de réplica e máquina virtual for detectado e reutilizar o Azure Site Recovery e restabelecer a replicação usando Olá especificar configurações.</span><span class="sxs-lookup"><span data-stu-id="e2691-128">Azure Site Recovery and VMM ensure that hello same replica host and virtual machine is detected, and Azure Site Recovery will reuse and reestablish replication using hello specified settings.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e2691-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e2691-129">Next steps</span></span>

<span data-ttu-id="e2691-130">Vá muito[etapa 10: executar um failover de teste](vmm-to-vmm-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="e2691-130">Go too[Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>
