---
title: "mapeamento de aaaNetwork entre duas regiões do Azure no Azure Site Recovery | Microsoft Docs"
description: "O Azure Site Recovery coordena a replicação hello, failover e recuperação de máquinas virtuais e servidores físicos. Saiba mais sobre tooAzure de failover ou um datacenter secundário."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 4f80c44e3f94eaf446bc01a7041d91fe34aa78d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="network-mapping-between-two-azure-regions"></a><span data-ttu-id="6daef-104">Mapeamento de rede entre duas regiões do Azure</span><span class="sxs-lookup"><span data-stu-id="6daef-104">Network mapping between two Azure regions</span></span>


<span data-ttu-id="6daef-105">Este artigo descreve como toomap Azure redes virtuais de duas regiões do Azure com o outro.</span><span class="sxs-lookup"><span data-stu-id="6daef-105">This article describes how toomap Azure virtual networks of two Azure regions with each other.</span></span> <span data-ttu-id="6daef-106">Mapeamento de rede garante que, quando a máquina virtual replicada é criada no destino Olá região do Azure, é criado na rede virtual de saudação que é mapeada toovirtual rede de saudação da máquina virtual de origem.</span><span class="sxs-lookup"><span data-stu-id="6daef-106">Network mapping ensures that when replicated virtual machine is created in hello target Azure region, it is created on hello virtual network that is mapped toovirtual network of hello source virtual machine.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="6daef-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6daef-107">Prerequisites</span></span>
<span data-ttu-id="6daef-108">Antes de mapear as redes, certifique-se de que você criou [redes virtuais do Azure](../virtual-network/virtual-networks-overview.md) em ambas as regiões do Azure de origem e de destino.</span><span class="sxs-lookup"><span data-stu-id="6daef-108">Before you map networks make sure, you have created [Azure virtual networks](../virtual-network/virtual-networks-overview.md) in both source and target Azure regions.</span></span>

## <a name="map-networks"></a><span data-ttu-id="6daef-109">Mapear redes</span><span class="sxs-lookup"><span data-stu-id="6daef-109">Map networks</span></span>

<span data-ttu-id="6daef-110">toomap uma rede virtual do Azure na rede virtual de tooanother de uma região do Azure em outra região, vá tooSite infra-estrutura de recuperação -> mapeamento de rede (para máquinas virtuais do Azure) e criar um mapeamento de rede.</span><span class="sxs-lookup"><span data-stu-id="6daef-110">toomap an Azure virtual network in one Azure region tooanother virtual network in another region, go tooSite Recovery Infrastructure -> Network Mapping (For Azure Virtual Machines) and create a network mapping.</span></span>

![Mapeamento de rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


<span data-ttu-id="6daef-112">Em Olá exemplo abaixo minha máquina virtual está em execução na região da Ásia Oriental e está sendo replicada tooSoutheast Ásia.</span><span class="sxs-lookup"><span data-stu-id="6daef-112">In hello example below my virtual machine is running in East Asia region and is being replicated tooSoutheast Asia.</span></span>

<span data-ttu-id="6daef-113">Selecione a rede de origem e destino hello e clique em toocreate Okey um mapeamento de rede da Ásia Oriental tooSoutheast Ásia.</span><span class="sxs-lookup"><span data-stu-id="6daef-113">Select hello source and target network and then click OK toocreate a network mapping from East Asia tooSoutheast Asia.</span></span>

![Mapeamento de rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


<span data-ttu-id="6daef-115">Olá a mesma coisa toocreate um mapeamento de rede de tooEast Ásia Sudeste da Ásia.</span><span class="sxs-lookup"><span data-stu-id="6daef-115">Do hello same thing toocreate a network mapping from Southeast Asia tooEast Asia.</span></span>  
![Mapeamento de rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a><span data-ttu-id="6daef-117">Mapeamento de rede ao habilitar a replicação</span><span class="sxs-lookup"><span data-stu-id="6daef-117">Mapping network when enabling replication</span></span>

<span data-ttu-id="6daef-118">Se o mapeamento de rede não for feito, quando você estiver replicando uma máquina virtual para Olá primeiro tempo formulário uma região do Azure tooanother, em seguida, você pode escolher rede de destino como parte da saudação mesmo processo.</span><span class="sxs-lookup"><span data-stu-id="6daef-118">If network mapping is not done when you are replicating a virtual machine for hello first time form one Azure region tooanother, then you can choose target network as part of hello same process.</span></span> <span data-ttu-id="6daef-119">Recuperação de site cria mapeamentos de rede de região de tootarget de região de origem e de região de toosource da região de destino com base nessa seleção.</span><span class="sxs-lookup"><span data-stu-id="6daef-119">Site Recovery creates network mappings from source region tootarget region and from target region toosource region based on this selection.</span></span>   

![Mapeamento de rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

<span data-ttu-id="6daef-121">Por padrão, a recuperação de Site cria uma rede na região de destino de saudação é a rede de origem toohello idênticos e adicionando '-asr' como um nome de toohello sufixo da rede de origem de saudação.</span><span class="sxs-lookup"><span data-stu-id="6daef-121">By default, Site Recovery creates a network in hello target region that is identical toohello source network and by adding '-asr' as a suffix toohello name of hello source network.</span></span> <span data-ttu-id="6daef-122">Você pode escolher uma rede já criada, clicando em Personalizar.</span><span class="sxs-lookup"><span data-stu-id="6daef-122">You can choose an already created network by clicking Customize.</span></span>

![Mapeamento de rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


<span data-ttu-id="6daef-124">Se o mapeamento de rede Olá já for feito, você não pode alterar a rede virtual de destino Olá durante a habilitação da replicação.</span><span class="sxs-lookup"><span data-stu-id="6daef-124">If hello network mapping is already done, you can't change hello target virtual network while enabling replication.</span></span> <span data-ttu-id="6daef-125">toochange, modifique o mapeamento de rede existente.</span><span class="sxs-lookup"><span data-stu-id="6daef-125">toochange it, modify existing network mapping.</span></span>  

![Mapeamento de rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![Mapeamento de rede](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> <span data-ttu-id="6daef-128">Se você modificar um mapeamento de rede de 1 a região tooregion-2, verifique se que você modificar o mapeamento de rede de saudação de região 2 tooregion-1 também.</span><span class="sxs-lookup"><span data-stu-id="6daef-128">If you modify a network mapping from region-1 tooregion-2, make sure you modify hello network mapping from region-2 tooregion-1 as well.</span></span>
>
>


## <a name="subnet-selection"></a><span data-ttu-id="6daef-129">Seleção de sub-rede</span><span class="sxs-lookup"><span data-stu-id="6daef-129">Subnet selection</span></span>
<span data-ttu-id="6daef-130">Subrede Olá virtual da máquina de destino é selecionada com base no nome de saudação da sub-rede de saudação de saudação da máquina virtual de origem.</span><span class="sxs-lookup"><span data-stu-id="6daef-130">Subnet of hello target virtual machine is selected based on hello name of hello subnet of hello source virtual machine.</span></span> <span data-ttu-id="6daef-131">Se houver uma sub-rede de saudação mesmo nome da máquina virtual de origem de saudação disponível na rede de destino hello, em seguida, o que é escolhido para a máquina de virtual de destino hello.</span><span class="sxs-lookup"><span data-stu-id="6daef-131">If there is a subnet of hello same name as that of hello source virtual machine available in hello target network, then that is chosen for hello target virtual machine.</span></span> <span data-ttu-id="6daef-132">Se não houver nenhuma sub-rede com hello mesmo nome na rede de destino hello, em seguida, em ordem alfabética primeira sub-rede é escolhido como Olá sub-rede de destino.</span><span class="sxs-lookup"><span data-stu-id="6daef-132">If there is no subnet with hello same name in hello target network, then alphabetically first subnet is chosen as hello target subnet.</span></span> <span data-ttu-id="6daef-133">Você pode modificar essa sub-rede indo tooCompute e as configurações de rede da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="6daef-133">You can modify this subnet by going tooCompute and Network settings of hello virtual machine.</span></span>

![Modificar sub-rede](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a><span data-ttu-id="6daef-135">Endereço IP</span><span class="sxs-lookup"><span data-stu-id="6daef-135">IP address</span></span>

<span data-ttu-id="6daef-136">Endereço IP para cada interface de rede Olá Olá virtual da máquina de destino é escolhido da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="6daef-136">IP address for each of hello network interface of hello target virtual machine is chosen as follows:</span></span>

### <a name="dhcp"></a><span data-ttu-id="6daef-137">DHCP</span><span class="sxs-lookup"><span data-stu-id="6daef-137">DHCP</span></span>
<span data-ttu-id="6daef-138">Se a interface de rede Olá Olá da máquina virtual de origem estiver usando DHCP, a interface de rede da máquina de virtual de destino Olá também é definido como DHCP.</span><span class="sxs-lookup"><span data-stu-id="6daef-138">If hello network interface of hello source virtual machine is using DHCP, then network interface of hello target virtual machine is also set as DHCP.</span></span>

### <a name="static-ip"></a><span data-ttu-id="6daef-139">IP Estático</span><span class="sxs-lookup"><span data-stu-id="6daef-139">Static IP</span></span>
<span data-ttu-id="6daef-140">Se a interface de rede Olá Olá da máquina virtual de origem estiver usando um IP estático, a interface de rede da máquina de virtual de destino Olá também será definido toouse IP estático.</span><span class="sxs-lookup"><span data-stu-id="6daef-140">If hello network interface of hello source virtual machine is using Static IP, then network interface of hello target virtual machine is also set toouse Static IP.</span></span> <span data-ttu-id="6daef-141">O IP estático é escolhido da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="6daef-141">Static IP is chosen as follows:</span></span>

#### <a name="same-address-space"></a><span data-ttu-id="6daef-142">Mesmo espaço de endereço</span><span class="sxs-lookup"><span data-stu-id="6daef-142">Same address space</span></span>

<span data-ttu-id="6daef-143">Se Olá fonte subrede e sub-rede de destino Olá tem Olá mesmo espaço de endereço, IP de destino é definido igual ao IP Olá Olá da interface de rede de saudação da máquina virtual de origem.</span><span class="sxs-lookup"><span data-stu-id="6daef-143">If hello source subnet and hello target subnet have hello same address space, then target IP is set same as hello IP of  hello network interface of hello source virtual machine.</span></span> <span data-ttu-id="6daef-144">Se o mesmo IP não estiver disponível, alguns outros IP disponível é definido como Olá IP de destino.</span><span class="sxs-lookup"><span data-stu-id="6daef-144">If same IP is not available, then some other available IP is set as hello target IP.</span></span>

#### <a name="different-address-space"></a><span data-ttu-id="6daef-145">Espaço de endereço diferente</span><span class="sxs-lookup"><span data-stu-id="6daef-145">Different address space</span></span>

<span data-ttu-id="6daef-146">Se Olá fonte subrede e sub-rede de destino Olá tiverem espaço de endereço diferente, IP de destino é definido como qualquer IP disponível na sub-rede de destino hello.</span><span class="sxs-lookup"><span data-stu-id="6daef-146">If hello source subnet and hello target subnet have different address space, then target IP is set as any available IP in hello target subnet.</span></span>

<span data-ttu-id="6daef-147">Você pode modificar o IP de destino de saudação em cada interface de rede indo tooCompute e as configurações de rede da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="6daef-147">You can modify hello target IP on each network interface by going tooCompute and Network settings of hello virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6daef-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6daef-148">Next steps</span></span>

- <span data-ttu-id="6daef-149">Saiba mais sobre as [diretrizes de rede para replicação de VMs do Azure](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="6daef-149">Learn about [networking guidance for replicating Azure VMs](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
