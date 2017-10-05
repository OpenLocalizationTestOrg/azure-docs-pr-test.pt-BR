---
title: "Planejar a rede para replicação do Hyper-V (sem o System Center VMM) para o Azure com o Azure Site Recovery | Microsoft Docs"
description: "Este artigo aborda o planejamento de rede necessário ao replicar VMs do Hyper-V (sem VMM) para o Azure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5ca12254-975d-48e8-a84d-422825dac9b2
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 100b9d8a55c2c163e7a04680f0f7d7963315ee73
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="step-4-plan-networking-for-hyper-v-to-azure-replication"></a><span data-ttu-id="a83c2-103">Etapa 4: Planejar a rede para replicação do Hyper-V para o Azure</span><span class="sxs-lookup"><span data-stu-id="a83c2-103">Step 4: Plan networking for Hyper-V to Azure replication</span></span>

<span data-ttu-id="a83c2-104">Este artigo resume as considerações sobre o planejamento de rede ao replicar VMs Hyper-V locais (sem o System Center VMM) para o Azure usando o serviço [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a83c2-104">This article summarizes network planning considerations when replicating on-premises Hyper-V VMs (without System Center VMM) to Azure using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="a83c2-105">Publique eventuais comentários no final deste artigo ou no [Fórum dos Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="a83c2-105">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="connecting-to-replica-vms-after-failover"></a><span data-ttu-id="a83c2-106">Conexão com VMs de réplica após o failover</span><span class="sxs-lookup"><span data-stu-id="a83c2-106">Connecting to replica VMs after failover</span></span>

<span data-ttu-id="a83c2-107">Ao planejar sua estratégia de replicação e failover, uma das principais questões é como se conectar à VM do Azure após o failover.</span><span class="sxs-lookup"><span data-stu-id="a83c2-107">When planning your replication and failover strategy, one of the key questions is how to connect to the Azure VM after failover.</span></span> <span data-ttu-id="a83c2-108">Há algumas opções ao criar sua estratégia de rede para VMs de réplica do Azure:</span><span class="sxs-lookup"><span data-stu-id="a83c2-108">There are a couple of choices when designing your network strategy for replica Azure VMs:</span></span>

- <span data-ttu-id="a83c2-109">**Endereço IP diferente**: você pode optar por usar outro intervalo de endereços IP para a rede VM replicada do Azure.</span><span class="sxs-lookup"><span data-stu-id="a83c2-109">**Different IP address**: You can select to use a different IP address range for the replicated Azure VM network.</span></span> <span data-ttu-id="a83c2-110">Nesse cenário, a VM obtém um novo endereço IP após o failover e uma atualização de DNS é necessária.</span><span class="sxs-lookup"><span data-stu-id="a83c2-110">In this scenario the VM gets a new IP address after failover, and a DNS update is required.</span></span> [<span data-ttu-id="a83c2-111">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="a83c2-111">Learn more</span></span>](site-recovery-test-failover-vmm-to-vmm.md#prepare-the-infrastructure-for-test-failover)
- <span data-ttu-id="a83c2-112">**Mesmo endereço IP**: talvez você deseje usar o mesmo intervalo de endereços IP da rede primária local para a rede do Azure após o failover.</span><span class="sxs-lookup"><span data-stu-id="a83c2-112">**Same IP address**: You might want to use the same IP address range as that in your primary on-premises network, for the Azure network after failover.</span></span>  <span data-ttu-id="a83c2-113">Manter os mesmos endereços IP simplifica a recuperação, reduzindo problemas relacionados à rede após o failover.</span><span class="sxs-lookup"><span data-stu-id="a83c2-113">Keeping the same IP addresses simplifies the recovery by reducing network related issues after failover.</span></span> <span data-ttu-id="a83c2-114">No entanto, quando você estiver replicando para o Azure, precisará atualizar as rotas com o novo local dos endereços IP após o failover.</span><span class="sxs-lookup"><span data-stu-id="a83c2-114">However, when you're replicating to Azure, you will need to update routes with the new location of the IP addresses after failover.</span></span>


## <a name="retain-ip-addresses"></a><span data-ttu-id="a83c2-115">Manter os endereços IP</span><span class="sxs-lookup"><span data-stu-id="a83c2-115">Retain IP addresses</span></span>

<span data-ttu-id="a83c2-116">O Site Recovery fornece a capacidade de manter endereços IP fixos durante o failover para o Azure, com um failover de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="a83c2-116">Site Recovery provides the capability to retain fixed IP addresses when failing over to Azure, with a subnet failover.</span></span>

<span data-ttu-id="a83c2-117">Com o failover de sub-rede, uma sub-rede específica está presente no Site 1 ou Site 2, mas nunca em ambos os sites ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="a83c2-117">With subnet failover, a specific subnet is present at Site 1 or Site 2, but never at both sites simultaneously.</span></span> <span data-ttu-id="a83c2-118">Para manter o espaço de endereço IP no caso de um failover, de forma programática, faça com que a infraestrutura do roteador mova as sub-redes de um site para outro.</span><span class="sxs-lookup"><span data-stu-id="a83c2-118">In order to maintain the IP address space in the event of a failover, you programmatically arrange for the router infrastructure to move the subnets from one site to another.</span></span> <span data-ttu-id="a83c2-119">Durante o failover, as sub-redes são movidas com as VMs protegidas associadas.</span><span class="sxs-lookup"><span data-stu-id="a83c2-119">During failover, the subnets move with the associated protected VMs.</span></span> <span data-ttu-id="a83c2-120">A principal desvantagem é que, em caso de falha, você precisa mover toda a sub-rede.</span><span class="sxs-lookup"><span data-stu-id="a83c2-120">The main drawback is that in the event of a failure, you have to move the whole subnet.</span></span>


### <a name="failover-example"></a><span data-ttu-id="a83c2-121">Exemplo de failover</span><span class="sxs-lookup"><span data-stu-id="a83c2-121">Failover example</span></span>

<span data-ttu-id="a83c2-122">Vejamos um exemplo de failover para o Azure.</span><span class="sxs-lookup"><span data-stu-id="a83c2-122">Let's look at an example for failover to Azure.</span></span>

- <span data-ttu-id="a83c2-123">Uma organização fictícia, o Woodgrove Bank, tem uma infraestrutura local que hospeda seus aplicativos de negócios.</span><span class="sxs-lookup"><span data-stu-id="a83c2-123">A ficticious company, Woodgrove Bank, has an on-premises infrastructure hosting their business apps.</span></span> <span data-ttu-id="a83c2-124">Seus aplicativos móveis são hospedados no Azure.</span><span class="sxs-lookup"><span data-stu-id="a83c2-124">Their mobile applications are hosted on Azure.</span></span>
- <span data-ttu-id="a83c2-125">A conectividade entre as VMs do Woodgrove Bank no Azure e os servidores locais é fornecida por uma conexão (VPN) site a site entre a rede de borda local e a rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="a83c2-125">Connectivity between Woodgrove Bank VMs in Azure and on-premises servers is provided by a site-to-site (VPN) connection between the on-premises edge network and the Azure virtual network.</span></span>
- <span data-ttu-id="a83c2-126">Essa VPN significa que a rede virtual da empresa no Azure aparece como uma extensão de sua rede local.</span><span class="sxs-lookup"><span data-stu-id="a83c2-126">This VPN means that the company's virtual network in Azure appears as an extension of their on-premises network.</span></span>
- <span data-ttu-id="a83c2-127">O Woodgrove deseja usar o Site Recovery para replicar as cargas de trabalho locais para o Azure.</span><span class="sxs-lookup"><span data-stu-id="a83c2-127">Woodgrove wants to use Site Recovery to replicate on-premises workloads to Azure.</span></span>
 - <span data-ttu-id="a83c2-128">O Woodgrove precisa lidar com aplicativos e configurações que dependem de endereços IP embutidos em código e, portanto, precisa reter endereços IP para seus aplicativos após o failover para o Azure.</span><span class="sxs-lookup"><span data-stu-id="a83c2-128">Woodgrove has to deal with applications and configurations which depend on hard-coded IP addresses, and thus need to retain IP addresses for their applications after failover to Azure.</span></span>
 - <span data-ttu-id="a83c2-129">O Woodgrove atribuiu endereços IP do intervalo 172.16.1.0/24 a 172.16.2.0/24 aos seus recursos em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="a83c2-129">Woodgrove has assigned IP addresses from range 172.16.1.0/24, 172.16.2.0/24 to its resources running in Azure.</span></span>


<span data-ttu-id="a83c2-130">Para que o Woodgrove consiga replicar suas VMs para o Azure, ao mesmo tempo que mantém os endereços IP, veja o que a empresa precisa fazer:</span><span class="sxs-lookup"><span data-stu-id="a83c2-130">For Woodgrove to be able to replicate its VMs to Azure while retaining the IP addresses, here's what the company needs to do:</span></span>

1. <span data-ttu-id="a83c2-131">Crie uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="a83c2-131">Create an Azure virtual network.</span></span> <span data-ttu-id="a83c2-132">Ela deve ser uma extensão da rede local, de forma que os aplicativos possam fazer failover de forma ininterrupta.</span><span class="sxs-lookup"><span data-stu-id="a83c2-132">It should be an extension of the on-premises network, so that applications can fail over seamlessly.</span></span>
2. <span data-ttu-id="a83c2-133">O Azure permite que você adicione a conectividade VPN site a site, além da conectividade ponto a site, às redes virtuais criadas no Azure.</span><span class="sxs-lookup"><span data-stu-id="a83c2-133">Azure allows you to add site-to-site VPN connectivity, in addition to point-to-site connectivity to the virtual networks created in Azure.</span></span>
3. <span data-ttu-id="a83c2-134">Ao configurar a conexão site a site, na rede do Azure, você poderá encaminhar o tráfego para a localização local (rede local) somente se o intervalo de endereços IP for diferente do intervalo de endereços IP local.</span><span class="sxs-lookup"><span data-stu-id="a83c2-134">When setting up the site-to-site connection, in the Azure network, you can route traffic to the on-premises location (local-network) only if the IP address range is different from the on-premises IP address range.</span></span>
    - <span data-ttu-id="a83c2-135">Isso ocorre porque o Azure não dá suporte a sub-redes ampliadas.</span><span class="sxs-lookup"><span data-stu-id="a83c2-135">This is because Azure doesn’t support stretched subnets.</span></span> <span data-ttu-id="a83c2-136">Portanto, se você tiver uma sub-rede 192.168.1.0/24 local, não poderá adicionar uma rede local 192.168.1.0/24 à rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="a83c2-136">So if you have subnet 192.168.1.0/24 on-premises, you can’t add a local-network 192.168.1.0/24 in the Azure network.</span></span>
    - <span data-ttu-id="a83c2-137">Isso é esperado, porque o Azure não reconhece que não há nenhuma VM ativa na sub-rede e que a sub-rede está sendo criada apenas para fins de recuperação de desastre.</span><span class="sxs-lookup"><span data-stu-id="a83c2-137">This is expected because Azure doesn’t know that there are no active VMs in the subnet, and that the subnet is being created for disaster recovery only.</span></span>
    - <span data-ttu-id="a83c2-138">Para poder encaminhar o tráfego de rede corretamente para fora de uma rede do Azure, as sub-redes na rede e a rede local não devem entrar em conflito.</span><span class="sxs-lookup"><span data-stu-id="a83c2-138">To be able to correctly route network traffic out of an Azure network the subnets in the network and the local-network mustn't conflict.</span></span>

![Antes do failover da sub-rede](./media/hyper-v-site-walkthrough-network/network-design7.png)

### <a name="before-failover"></a><span data-ttu-id="a83c2-140">Antes do failover</span><span class="sxs-lookup"><span data-stu-id="a83c2-140">Before failover</span></span>

1. <span data-ttu-id="a83c2-141">Crie uma rede adicional (por exemplo, uma Rede de Recuperação).</span><span class="sxs-lookup"><span data-stu-id="a83c2-141">Create an additional network (for example Recovery Network).</span></span> <span data-ttu-id="a83c2-142">Essa é a rede na qual as VMs com failover são criadas.</span><span class="sxs-lookup"><span data-stu-id="a83c2-142">This is the network in which failed over VMs are created.</span></span>
2. <span data-ttu-id="a83c2-143">Para garantir que o endereço IP de um computador é mantido após um failover, nas propriedades da VM > **Configurar**, especifique o mesmo endereço IP que a VM tem no local e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="a83c2-143">To ensure that the IP address for a VM is retained after a failover, in the VM properties > **Configure**, specify the same IP address that the VM has on-premises, and click **Save**.</span></span>
3. <span data-ttu-id="a83c2-144">Quando a VM passar por failover, o Azure Site Recovery atribuirá o endereço IP fornecido a ele.</span><span class="sxs-lookup"><span data-stu-id="a83c2-144">When the VM is failed over, Azure Site Recovery will assign the provided IP address to it.</span></span>

    ![Propriedades da rede](./media/hyper-v-site-walkthrough-network/network-design8.png)

4. <span data-ttu-id="a83c2-146">Depois que o failover for disparado e as VMs forem criadas no Azure com o endereço IP solicitado, você poderá se conectar à rede usando uma [conexão Vnet a Vnet](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span><span class="sxs-lookup"><span data-stu-id="a83c2-146">After failover is trigger is triggered, and the VMs are created in Azure with the required IP address, you can connect to the network using a [Vnet to Vnet vonnection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span> <span data-ttu-id="a83c2-147">Essa ação pode ser inserida em um script.</span><span class="sxs-lookup"><span data-stu-id="a83c2-147">This action can be scripted.</span></span>
5. <span data-ttu-id="a83c2-148">As rotas precisam ser modificadas de maneira apropriada, para refletir que 192.168.1.0/24 agora foi movido para o Azure.</span><span class="sxs-lookup"><span data-stu-id="a83c2-148">Routes need to be appropriately modified, to reflect that 192.168.1.0/24 has now moved to Azure.</span></span>

    ![Após o failover da sub-rede](./media/hyper-v-site-walkthrough-network/network-design9.png)

### <a name="after-failover"></a><span data-ttu-id="a83c2-150">Após o failover</span><span class="sxs-lookup"><span data-stu-id="a83c2-150">After failover</span></span>

<span data-ttu-id="a83c2-151">Caso você não tenha uma rede do Azure, conforme ilustrado acima, poderá criar uma conexão VPN site a site entre o site primário e o Azure, após o failover.</span><span class="sxs-lookup"><span data-stu-id="a83c2-151">If you don't have an Azure network as illustrated above, you can create a site-to-site VPN connection between your primary site and Azure, after failvoer.</span></span>

## <a name="change-ip-addresses"></a><span data-ttu-id="a83c2-152">Alterar os endereços IP</span><span class="sxs-lookup"><span data-stu-id="a83c2-152">Change IP addresses</span></span>

<span data-ttu-id="a83c2-153">Esta [postagem no blog](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explica como configurar a infraestrutura de rede do Azure quando você não precisa reter os endereços IP após o failover.</span><span class="sxs-lookup"><span data-stu-id="a83c2-153">This [blog post](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explains how to set up the Azure networking infrastructure when you don't need to retain IP addresses after failover.</span></span> <span data-ttu-id="a83c2-154">Ela começa com uma descrição do aplicativo, explica como configurar a rede local e no Azure e termina com informações sobre como executar failovers.</span><span class="sxs-lookup"><span data-stu-id="a83c2-154">It starts with an application description, looks at how to set up networking on-premises and in Azure, and concludes with information about running failovers.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="a83c2-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a83c2-155">Next steps</span></span>

<span data-ttu-id="a83c2-156">Ir para a [Etapa 5: Preparar o Azure](hyper-v-site-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="a83c2-156">Go to [Step 5: Prepare Azure](hyper-v-site-walkthrough-prepare-azure.md)</span></span>
