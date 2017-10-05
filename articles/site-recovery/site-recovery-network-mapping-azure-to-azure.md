---
title: "Mapeamento de rede entre duas regiões do Azure no Azure Site Recovery | Microsoft Docs"
description: "O Azure Site Recovery coordena a replicação, o failover e a recuperação de máquinas virtuais e servidores físicos. Saiba mais sobre o failover no Azure ou em um datacenter secundário."
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
ms.openlocfilehash: 9d6a806ec533259797080fbfee2c38f918ebd8a2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="network-mapping-between-two-azure-regions"></a><span data-ttu-id="8fff8-104">Mapeamento de rede entre duas regiões do Azure</span><span class="sxs-lookup"><span data-stu-id="8fff8-104">Network mapping between two Azure regions</span></span>


<span data-ttu-id="8fff8-105">Este artigo descreve como mapear as redes virtuais do Azure de duas regiões do Azure entre si.</span><span class="sxs-lookup"><span data-stu-id="8fff8-105">This article describes how to map Azure virtual networks of two Azure regions with each other.</span></span> <span data-ttu-id="8fff8-106">O mapeamento de rede garante que quando a máquina virtual replicada for criada na região do Azure de destino, ela será criada em uma rede virtual que é mapeada para uma rede virtual da máquina virtual de origem.</span><span class="sxs-lookup"><span data-stu-id="8fff8-106">Network mapping ensures that when replicated virtual machine is created in the target Azure region, it is created on the virtual network that is mapped to virtual network of the source virtual machine.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="8fff8-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8fff8-107">Prerequisites</span></span>
<span data-ttu-id="8fff8-108">Antes de mapear as redes, certifique-se de que você criou [redes virtuais do Azure](../virtual-network/virtual-networks-overview.md) em ambas as regiões do Azure de origem e de destino.</span><span class="sxs-lookup"><span data-stu-id="8fff8-108">Before you map networks make sure, you have created [Azure virtual networks](../virtual-network/virtual-networks-overview.md) in both source and target Azure regions.</span></span>

## <a name="map-networks"></a><span data-ttu-id="8fff8-109">Mapear redes</span><span class="sxs-lookup"><span data-stu-id="8fff8-109">Map networks</span></span>

<span data-ttu-id="8fff8-110">Para mapear uma rede virtual do Azure em uma região do Azure para outra rede virtual em outra região, vá para a Infraestrutura do Site Recovery -> Mapeamento de Rede (para Máquinas virtuais do Azure) e crie um mapeamento de rede.</span><span class="sxs-lookup"><span data-stu-id="8fff8-110">To map an Azure virtual network in one Azure region to another virtual network in another region, go to Site Recovery Infrastructure -> Network Mapping (For Azure Virtual Machines) and create a network mapping.</span></span>

![Mapeamento de rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


<span data-ttu-id="8fff8-112">No exemplo a seguir, minha máquina virtual está em execução na região da Ásia Oriental e está sendo replicada como Sudeste Asiático.</span><span class="sxs-lookup"><span data-stu-id="8fff8-112">In the example below my virtual machine is running in East Asia region and is being replicated to Southeast Asia.</span></span>

<span data-ttu-id="8fff8-113">Selecione a rede de origem e de destino e, em seguida, clique em OK para criar um mapeamento de rede da Ásia Oriental como Sudeste Asiático.</span><span class="sxs-lookup"><span data-stu-id="8fff8-113">Select the source and target network and then click OK to create a network mapping from East Asia to Southeast Asia.</span></span>

![Mapeamento de rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


<span data-ttu-id="8fff8-115">Faça o mesmo para criar um mapeamento de rede do Sudeste Asiático para Ásia Oriental.</span><span class="sxs-lookup"><span data-stu-id="8fff8-115">Do the same thing to create a network mapping from Southeast Asia to East Asia.</span></span>  
![Mapeamento de rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a><span data-ttu-id="8fff8-117">Mapeamento de rede ao habilitar a replicação</span><span class="sxs-lookup"><span data-stu-id="8fff8-117">Mapping network when enabling replication</span></span>

<span data-ttu-id="8fff8-118">Se o mapeamento de rede não for feito, quando estiver replicando uma máquina virtual pela primeira vez, formando uma região do Azure para outra, então você poderá escolher a rede de destino como parte do mesmo processo.</span><span class="sxs-lookup"><span data-stu-id="8fff8-118">If network mapping is not done when you are replicating a virtual machine for the first time form one Azure region to another, then you can choose target network as part of the same process.</span></span> <span data-ttu-id="8fff8-119">O Site Recovery cria mapeamentos de rede a partir da região de origem para a região de destino e a partir da região de destino para a região de origem com base nessa seleção.</span><span class="sxs-lookup"><span data-stu-id="8fff8-119">Site Recovery creates network mappings from source region to target region and from target region to source region based on this selection.</span></span>   

![Mapeamento de rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

<span data-ttu-id="8fff8-121">Por padrão, o Site Recovery cria uma rede na região de destino que é idêntica à rede de origem e adicionando “-asr” como um sufixo ao nome da rede de origem.</span><span class="sxs-lookup"><span data-stu-id="8fff8-121">By default, Site Recovery creates a network in the target region that is identical to the source network and by adding '-asr' as a suffix to the name of the source network.</span></span> <span data-ttu-id="8fff8-122">Você pode escolher uma rede já criada, clicando em Personalizar.</span><span class="sxs-lookup"><span data-stu-id="8fff8-122">You can choose an already created network by clicking Customize.</span></span>

![Mapeamento de rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


<span data-ttu-id="8fff8-124">Se o mapeamento de rede já foi feito, você não pode alterar a rede virtual de destino durante a habilitação da replicação.</span><span class="sxs-lookup"><span data-stu-id="8fff8-124">If the network mapping is already done, you can't change the target virtual network while enabling replication.</span></span> <span data-ttu-id="8fff8-125">Para alterá-la, modifique o mapeamento de rede existente.</span><span class="sxs-lookup"><span data-stu-id="8fff8-125">To change it, modify existing network mapping.</span></span>  

![Mapeamento de rede](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![Mapeamento de rede](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> <span data-ttu-id="8fff8-128">Se você modificar um mapeamento de rede da região 1 para a região 2, certifique-se de que você modificou o mapeamento de rede da região 2 para a região 1 também.</span><span class="sxs-lookup"><span data-stu-id="8fff8-128">If you modify a network mapping from region-1 to region-2, make sure you modify the network mapping from region-2 to region-1 as well.</span></span>
>
>


## <a name="subnet-selection"></a><span data-ttu-id="8fff8-129">Seleção de sub-rede</span><span class="sxs-lookup"><span data-stu-id="8fff8-129">Subnet selection</span></span>
<span data-ttu-id="8fff8-130">A sub-rede da máquina virtual de destino é selecionada de acordo com o nome da sub-rede da máquina virtual de origem.</span><span class="sxs-lookup"><span data-stu-id="8fff8-130">Subnet of the target virtual machine is selected based on the name of the subnet of the source virtual machine.</span></span> <span data-ttu-id="8fff8-131">Se houver uma sub-rede com o mesmo nome da máquina virtual de origem disponível na rede de destino, então ele será escolhido para a máquina virtual de destino.</span><span class="sxs-lookup"><span data-stu-id="8fff8-131">If there is a subnet of the same name as that of the source virtual machine available in the target network, then that is chosen for the target virtual machine.</span></span> <span data-ttu-id="8fff8-132">Se não houver nenhuma sub-rede com o mesmo nome na rede de destino, então a primeira sub-rede em ordem alfabética será escolhida como a sub-rede de destino.</span><span class="sxs-lookup"><span data-stu-id="8fff8-132">If there is no subnet with the same name in the target network, then alphabetically first subnet is chosen as the target subnet.</span></span> <span data-ttu-id="8fff8-133">Você pode modificar esta sub-rede indo para as configurações de Computação e Rede da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8fff8-133">You can modify this subnet by going to Compute and Network settings of the virtual machine.</span></span>

![Modificar sub-rede](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a><span data-ttu-id="8fff8-135">Endereço IP</span><span class="sxs-lookup"><span data-stu-id="8fff8-135">IP address</span></span>

<span data-ttu-id="8fff8-136">O endereço IP para cada interface de rede da máquina virtual de destino é escolhido da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="8fff8-136">IP address for each of the network interface of the target virtual machine is chosen as follows:</span></span>

### <a name="dhcp"></a><span data-ttu-id="8fff8-137">DHCP</span><span class="sxs-lookup"><span data-stu-id="8fff8-137">DHCP</span></span>
<span data-ttu-id="8fff8-138">Se a interface de rede da máquina virtual de origem estiver usando DHCP, a interface de rede da máquina virtual de destino também será definida como DHCP.</span><span class="sxs-lookup"><span data-stu-id="8fff8-138">If the network interface of the source virtual machine is using DHCP, then network interface of the target virtual machine is also set as DHCP.</span></span>

### <a name="static-ip"></a><span data-ttu-id="8fff8-139">IP Estático</span><span class="sxs-lookup"><span data-stu-id="8fff8-139">Static IP</span></span>
<span data-ttu-id="8fff8-140">Se a interface de rede da máquina virtual de origem estiver usando um IP estático, a interface de rede da máquina virtual de destino também será definida para usar IP estático.</span><span class="sxs-lookup"><span data-stu-id="8fff8-140">If the network interface of the source virtual machine is using Static IP, then network interface of the target virtual machine is also set to use Static IP.</span></span> <span data-ttu-id="8fff8-141">O IP estático é escolhido da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="8fff8-141">Static IP is chosen as follows:</span></span>

#### <a name="same-address-space"></a><span data-ttu-id="8fff8-142">Mesmo espaço de endereço</span><span class="sxs-lookup"><span data-stu-id="8fff8-142">Same address space</span></span>

<span data-ttu-id="8fff8-143">Se a sub-rede de origem e a sub-rede de destino tiverem o mesmo espaço de endereço, o IP de destino será definido igual ao IP da interface de rede da máquina virtual de origem.</span><span class="sxs-lookup"><span data-stu-id="8fff8-143">If the source subnet and the target subnet have the same address space, then target IP is set same as the IP of  the network interface of the source virtual machine.</span></span> <span data-ttu-id="8fff8-144">Se o mesmo IP não estiver disponível, alguns outros IP disponíveis serão definidos como o IP de destino.</span><span class="sxs-lookup"><span data-stu-id="8fff8-144">If same IP is not available, then some other available IP is set as the target IP.</span></span>

#### <a name="different-address-space"></a><span data-ttu-id="8fff8-145">Espaço de endereço diferente</span><span class="sxs-lookup"><span data-stu-id="8fff8-145">Different address space</span></span>

<span data-ttu-id="8fff8-146">Se a sub-rede de origem e a sub-rede de destino tiverem um espaço de endereço diferente, então o IP de destino será definido como qualquer IP disponível na sub-rede de destino.</span><span class="sxs-lookup"><span data-stu-id="8fff8-146">If the source subnet and the target subnet have different address space, then target IP is set as any available IP in the target subnet.</span></span>

<span data-ttu-id="8fff8-147">Você pode modificar o IP de destino em cada interface de rede, vá para as configurações de Computação e Rede da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8fff8-147">You can modify the target IP on each network interface by going to Compute and Network settings of the virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8fff8-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8fff8-148">Next steps</span></span>

- <span data-ttu-id="8fff8-149">Saiba mais sobre as [diretrizes de rede para replicação de VMs do Azure](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="8fff8-149">Learn about [networking guidance for replicating Azure VMs](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
