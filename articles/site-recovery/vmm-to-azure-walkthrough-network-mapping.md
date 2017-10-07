---
title: "mapeamento de rede aaaConfigure para replicar máquinas virtuais do Hyper-V no VMM nuvens tooAzure com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como o mapeamento de rede tooconfigure ao replicar máquinas virtuais do Hyper-V no VMM nuvens tooAzure com o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 081a9fdb0ffa4114099e9bcb9c1b1e43ad26ecbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-configure-network-mapping-for-hyper-v-replication-with-vmm-tooazure"></a><span data-ttu-id="1ec06-103">Etapa 9: Configurar o mapeamento de rede para tooAzure de replicação (com o VMM) do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="1ec06-103">Step 9: Configure network mapping for Hyper-V replication (with VMM) tooAzure</span></span>

<span data-ttu-id="1ec06-104">Depois de configurar Olá [as configurações de replicação de origem e destino](vmm-to-azure-walkthrough-source-target.md), use toomap de mapeamento de rede Este artigo tooconfigure entre redes VM do VMM local e redes do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ec06-104">After you set up hello [source and target replication settings](vmm-to-azure-walkthrough-source-target.md), use this article tooconfigure network mapping toomap between on-premises VMM VM networks, and Azure networks.</span></span>

<span data-ttu-id="1ec06-105">Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="1ec06-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="1ec06-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="1ec06-106">Before you start</span></span>

- <span data-ttu-id="1ec06-107">Saiba mais sobre [mapeamento de rede](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span><span class="sxs-lookup"><span data-stu-id="1ec06-107">Learn about [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="1ec06-108">[Preparar VMM para mapeamento de rede](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping).</span><span class="sxs-lookup"><span data-stu-id="1ec06-108">[Prepare VMM for network mapping](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping).</span></span> 
- <span data-ttu-id="1ec06-109">Verifique se que máquinas virtuais no servidor do VMM Olá são conectados tooa rede VM e que você criou pelo menos uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ec06-109">Verify that virtual machines on hello VMM server are connected tooa VM network, and that you've created at least one Azure virtual network.</span></span> <span data-ttu-id="1ec06-110">Várias redes VM podem ser mapeado tooa única rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ec06-110">Multiple VM networks can be mapped tooa single Azure network.</span></span>

## <a name="configure-mapping"></a><span data-ttu-id="1ec06-111">Configurar o mapeamento</span><span class="sxs-lookup"><span data-stu-id="1ec06-111">Configure mapping</span></span>

<span data-ttu-id="1ec06-112">Configure o mapeamento da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1ec06-112">Configure mapping as follows:</span></span>

1. <span data-ttu-id="1ec06-113">Em **infra-estrutura de recuperação de Site** > **mapeamentos de rede** > **mapeamento de rede**, clique em Olá **+ de mapeamento de rede**  ícone.</span><span class="sxs-lookup"><span data-stu-id="1ec06-113">In **Site Recovery Infrastructure** > **Network mappings** > **Network Mapping**, click hello **+Network Mapping** icon.</span></span>

    ![Mapeamento de rede](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping1.png)
2. <span data-ttu-id="1ec06-115">Em **Adicionar mapeamento de rede**, selecione servidor VMM de origem Olá, e **Azure** como destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ec06-115">In **Add network mapping**, select hello source VMM server, and **Azure** as hello target.</span></span>
3. <span data-ttu-id="1ec06-116">Verifique se a assinatura hello e modelo de implantação de saudação após o failover.</span><span class="sxs-lookup"><span data-stu-id="1ec06-116">Verify hello subscription and hello deployment model after failover.</span></span>
4. <span data-ttu-id="1ec06-117">Em **rede de origem**, selecione rede VM do local de origem de saudação desejado toomap da lista de saudação associada ao servidor do VMM hello.</span><span class="sxs-lookup"><span data-stu-id="1ec06-117">In **Source network**, select hello source on-premises VM network you want toomap from hello list associated with hello VMM server.</span></span>
5. <span data-ttu-id="1ec06-118">Em **rede de destino**, selecione Olá rede do Azure no qual réplica VMs do Azure serão localizadas quando eles são criados.</span><span class="sxs-lookup"><span data-stu-id="1ec06-118">In **Target network**, select hello Azure network in which replica Azure VMs will be located when they're created.</span></span> <span data-ttu-id="1ec06-119">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="1ec06-119">Then click **OK**.</span></span>

    ![Mapeamento de rede](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping2.png)

<span data-ttu-id="1ec06-121">Veja o que acontece quando começa o mapeamento de rede:</span><span class="sxs-lookup"><span data-stu-id="1ec06-121">Here's what happens when network mapping begins:</span></span>

* <span data-ttu-id="1ec06-122">Máquinas virtuais existentes na rede VM de origem de saudação são conectados toohello rede de destino quando iniciar o mapeamento.</span><span class="sxs-lookup"><span data-stu-id="1ec06-122">Existing VMs on hello source VM network are connected toohello target network when mapping begins.</span></span> <span data-ttu-id="1ec06-123">Nova rede VM de origem para toohello conectado VMs estão conectados toohello mapeadas de rede do Azure quando a replicação ocorre.</span><span class="sxs-lookup"><span data-stu-id="1ec06-123">New VMs connected toohello source VM network are connected toohello mapped Azure network when replication occurs.</span></span>
* <span data-ttu-id="1ec06-124">Se você modificar um mapeamento de rede existente, máquinas virtuais de réplica se conectar usando Olá novas configurações.</span><span class="sxs-lookup"><span data-stu-id="1ec06-124">If you modify an existing network mapping, replica virtual machines connect using hello new settings.</span></span>
* <span data-ttu-id="1ec06-125">Se a rede de destino Olá possui várias sub-redes e uma dessas sub-redes tem Olá mesmo nome da sub-rede na qual máquina de virtual de origem hello está localizado, Olá máquina de virtual de réplica se conecta a sub-rede de destino toothat após o failover.</span><span class="sxs-lookup"><span data-stu-id="1ec06-125">If hello target network has multiple subnets, and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine connects toothat target subnet after failover.</span></span>
* <span data-ttu-id="1ec06-126">Se não houver nenhuma sub-rede de destino com um nome correspondente, Olá VM conecta toohello primeira sub-rede na rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ec06-126">If there’s no target subnet with a matching name, hello virtual machine connects toohello first subnet in hello network.</span></span>



## <a name="next-steps"></a><span data-ttu-id="1ec06-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1ec06-127">Next steps</span></span>

<span data-ttu-id="1ec06-128">Vá muito[etapa 10: criar uma política de replicação](vmm-to-azure-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="1ec06-128">Go too[Step 10: Create a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>
