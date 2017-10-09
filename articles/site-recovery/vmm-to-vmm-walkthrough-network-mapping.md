---
title: "redes aaaMap para o site secundário do Hyper-V VM replicação tooa com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como toomap redes ao replicar máquinas virtuais do Hyper-V tooa site VMM secundário com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 461b7c1c-ef61-4005-aeec-2324e727a3d0
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: d4f621df4ce08ae055bc6809daea0b71b76754ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-map-networks-for-hyper-v-vm-replication-tooa-secondary-site"></a><span data-ttu-id="bd9fc-103">Etapa 7: Mapear redes para o site secundário de tooa de replicação de VM do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="bd9fc-103">Step 7: Map networks for Hyper-V VM replication tooa secondary site</span></span>


<span data-ttu-id="bd9fc-104">Depois de configurar o [configurações de origem e destino](vmm-to-vmm-walkthrough-source-target.md) para a replicação de site tooa System Center Virtual Machine Manager (VMM) secundário (VMs) de máquinas virtuais Hyper-V, use esse mapeamento de rede do artigo tooconfigure virtual Hyper-v tooa de replicação de VM (máquina) secundário do site, usando [do Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bd9fc-104">After setting up [source and target settings](vmm-to-vmm-walkthrough-source-target.md) for replicating Hyper-V virtual machines (VMs) tooa secondary System Center Virtual Machine Manager (VMM) site, use this article tooconfigure network mapping for Hyper-V virtual machine (VM) replication tooa secondary site, using  [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="bd9fc-105">Depois de ler este artigo, postar os comentários na parte inferior do hello, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="bd9fc-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="bd9fc-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="bd9fc-106">Before you start</span></span>

- <span data-ttu-id="bd9fc-107">Saiba mais sobre [mapeamento de rede](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) antes de iniciar.</span><span class="sxs-lookup"><span data-stu-id="bd9fc-107">Learn about [network mapping](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) before you start.</span></span>
- <span data-ttu-id="bd9fc-108">Verifique se máquinas virtuais nos servidores VMM estão conectados tooa rede VM.</span><span class="sxs-lookup"><span data-stu-id="bd9fc-108">Verify that virtual machines on VMM servers are connected tooa VM network.</span></span>

## <a name="configure-network-mapping"></a><span data-ttu-id="bd9fc-109">Configurar o mapeamento de rede</span><span class="sxs-lookup"><span data-stu-id="bd9fc-109">Configure network mapping</span></span>

1. <span data-ttu-id="bd9fc-110">Em **Mapeamento de Rede** > **Mapeamentos de rede**, clique em **+Mapeamento de Rede**.</span><span class="sxs-lookup"><span data-stu-id="bd9fc-110">In **Network Mapping** > **Network mappings**, click **+Network Mapping**.</span></span>
2. <span data-ttu-id="bd9fc-111">Em **Adicionar mapeamento de rede** , selecione a fonte de saudação e servidores do VMM de destino.</span><span class="sxs-lookup"><span data-stu-id="bd9fc-111">In **Add network mapping** tab, select hello source and target VMM servers.</span></span> <span data-ttu-id="bd9fc-112">redes VM Olá associados aos servidores do VMM Olá são recuperados.</span><span class="sxs-lookup"><span data-stu-id="bd9fc-112">hello VM networks associated with hello VMM servers are retrieved.</span></span>
3. <span data-ttu-id="bd9fc-113">Em **rede de origem**, selecione rede hello serão toouse de lista de saudação de redes VM associadas Olá servidor primário do VMM.</span><span class="sxs-lookup"><span data-stu-id="bd9fc-113">In **Source network**, select hello network you want toouse from hello list of VM networks associated with hello primary VMM server.</span></span>
4. <span data-ttu-id="bd9fc-114">Em **rede de destino**, selecione rede hello serão toouse no servidor VMM secundário de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd9fc-114">In **Target network**, select hello network you want toouse on hello secondary VMM server.</span></span> <span data-ttu-id="bd9fc-115">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="bd9fc-115">Then click **OK**.</span></span>

    ![Mapeamento de rede](./media/vmm-to-vmm-walkthrough-network-mapping/network-mapping2.png)

<span data-ttu-id="bd9fc-117">Veja o que acontece quando começa o mapeamento de rede:</span><span class="sxs-lookup"><span data-stu-id="bd9fc-117">Here's what happens when network mapping begins:</span></span>

* <span data-ttu-id="bd9fc-118">Qualquer máquinas de virtuais de réplica existente que correspondem a rede VM de origem toohello será conectado toohello rede VM de destino.</span><span class="sxs-lookup"><span data-stu-id="bd9fc-118">Any existing replica virtual machines that correspond toohello source VM network will be connected toohello target VM network.</span></span>
* <span data-ttu-id="bd9fc-119">Novas máquinas virtuais que estão conectados toohello rede VM de origem será conectado toohello destino mapeadas rede após a replicação.</span><span class="sxs-lookup"><span data-stu-id="bd9fc-119">New virtual machines that are connected toohello source VM network will be connected toohello target mapped network after replication.</span></span>
* <span data-ttu-id="bd9fc-120">Se você modificar um mapeamento existente com uma nova rede, máquinas virtuais de réplica serão conectadas usando Olá novas configurações.</span><span class="sxs-lookup"><span data-stu-id="bd9fc-120">If you modify an existing mapping with a new network, replica virtual machines will be connected using hello new settings.</span></span>
* <span data-ttu-id="bd9fc-121">Se a rede de destino Olá tem várias sub-redes e uma dessas sub-redes tem Olá mesmo nome da sub-rede na qual máquina de virtual de origem hello está localizado, Olá máquina de virtual de réplica será conectada toothat sub-rede de destino após o failover.</span><span class="sxs-lookup"><span data-stu-id="bd9fc-121">If hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after failover.</span></span> <span data-ttu-id="bd9fc-122">Se não houver nenhuma sub-rede de destino com um nome correspondente, Olá máquina de virtual será conectado toohello primeira sub-rede na rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd9fc-122">If there’s no target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>



## <a name="next-steps"></a><span data-ttu-id="bd9fc-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bd9fc-123">Next steps</span></span>

<span data-ttu-id="bd9fc-124">Vá muito[etapa 8: configurar uma política de replicação](vmm-to-vmm-walkthrough-replication.md).</span><span class="sxs-lookup"><span data-stu-id="bd9fc-124">Go too[Step 8: Configure a replication policy](vmm-to-vmm-walkthrough-replication.md).</span></span>
