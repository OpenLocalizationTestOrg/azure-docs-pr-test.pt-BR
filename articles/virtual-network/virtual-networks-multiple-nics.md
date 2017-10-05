---
title: "Criar uma VM (Clássica) com diversas NICs usando o PowerShell | Microsoft Docs"
description: "Saiba como criar e configurar VMs com várias NICs usando PowerShell."
services: virtual-network, virtual-machines
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a1a3952c-2dcc-4977-bd7a-52d623c1fb07
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 68ccc1cac22e593b099729fe68c6bee63df44d9b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-classic-with-multiple-nics"></a><span data-ttu-id="2f390-103">Criar uma VM (Clássica) com diversas NICs</span><span class="sxs-lookup"><span data-stu-id="2f390-103">Create a VM (Classic) with multiple NICs</span></span>
<span data-ttu-id="2f390-104">Você pode criar máquinas virtuais (VMs) no Azure e anexar várias interfaces de rede (NICs) para cada uma de suas VMs.</span><span class="sxs-lookup"><span data-stu-id="2f390-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) to each of your VMs.</span></span> <span data-ttu-id="2f390-105">Várias NICs são um requisito para muitos aplicativos virtuais de rede, como soluções de distribuição de aplicativos e de otimização de WAN.</span><span class="sxs-lookup"><span data-stu-id="2f390-105">Multiple NICs are a requirement for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span> <span data-ttu-id="2f390-106">Várias NICs também fornecem isolamento do tráfego entre NICs.</span><span class="sxs-lookup"><span data-stu-id="2f390-106">Multiple NICs also provide isolation of traffic between NICs.</span></span>

![Várias NICs da VM](./media/virtual-networks-multiple-nics/IC757773.png)

<span data-ttu-id="2f390-108">A figura mostra uma VM com três NICs, cada uma conectada a uma sub-rede diferente.</span><span class="sxs-lookup"><span data-stu-id="2f390-108">The figure shows a VM with three NICs, each connected to a different subnet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f390-109">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="2f390-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="2f390-110">Este artigo aborda o uso do modelo de implantação clássica.</span><span class="sxs-lookup"><span data-stu-id="2f390-110">This article covers using the classic deployment model.</span></span> <span data-ttu-id="2f390-111">A Microsoft recomenda que a maioria das implantações novas use o Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="2f390-111">Microsoft recommends that most new deployments use Resource Manager.</span></span>

* <span data-ttu-id="2f390-112">VIP da Internet (implantações clássicas) têm suporte apenas na NIC "padrão".</span><span class="sxs-lookup"><span data-stu-id="2f390-112">Internet-facing VIP (classic deployments) is only supported on the "default" NIC.</span></span> <span data-ttu-id="2f390-113">Há apenas um VIP para o IP da NIC padrão.</span><span class="sxs-lookup"><span data-stu-id="2f390-113">There is only one VIP to the IP of the default NIC.</span></span>
* <span data-ttu-id="2f390-114">Neste momento, não há suporte para endereços LPIP (PI público no nível da instância) (implantações clássicas) para VMs com várias NICs.</span><span class="sxs-lookup"><span data-stu-id="2f390-114">At this time, Instance Level Public IP (LPIP) addresses (classic deployments) are not supported for multi NIC VMs.</span></span>
* <span data-ttu-id="2f390-115">A ordem das NICs de dentro da VM será aleatória e também pode ser alterada nas atualizações da infraestrutura do Azure.</span><span class="sxs-lookup"><span data-stu-id="2f390-115">The order of the NICs from inside the VM will be random, and could also change across Azure infrastructure updates.</span></span> <span data-ttu-id="2f390-116">No entanto, os endereços IP e os endereços ethernet MAC correspondentes permanecerão os mesmos.</span><span class="sxs-lookup"><span data-stu-id="2f390-116">However, the IP addresses, and the corresponding ethernet MAC addresses will remain the same.</span></span> <span data-ttu-id="2f390-117">Por exemplo, suponha que **Eth1** tenha o endereço IP 10.1.0.100 e um endereço MAC 00-0D-3A-B0-39-0D; após uma atualização de infraestrutura e reinicialização do Azure, ela pode ser alterada para **Eth2**, mas o emparelhamento entre IP e MAC permanecerá o mesmo.</span><span class="sxs-lookup"><span data-stu-id="2f390-117">For example, assume **Eth1** has IP address 10.1.0.100 and MAC address 00-0D-3A-B0-39-0D; after an Azure infrastructure update and reboot, it could be changed to **Eth2**, but the IP and MAC pairing will remain the same.</span></span> <span data-ttu-id="2f390-118">Quando a reinicialização for iniciada pelo cliente, a ordem das NICs permanecerá a mesma.</span><span class="sxs-lookup"><span data-stu-id="2f390-118">When a restart is customer-initiated, the NIC order will remain the same.</span></span>
* <span data-ttu-id="2f390-119">O endereço de cada NIC em cada máquina virtual deve estar localizado em uma sub-rede, várias NICs em uma única VM podem, cada uma, receber a atribuição de endereços que estejam na mesma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="2f390-119">The address for each NIC on each VM must be located in a subnet, multiple NICs on a single VM can each be assigned addresses that are in the same subnet.</span></span>
* <span data-ttu-id="2f390-120">O tamanho da VM determina o número de NICS que você pode criar para uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2f390-120">The VM size determines the number of NICS that you can create for a VM.</span></span> <span data-ttu-id="2f390-121">Consulte os artigos sobre tamanhos de VM do[Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e do [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para determinar a quantas NICS cada tamanho de VM oferece suporte.</span><span class="sxs-lookup"><span data-stu-id="2f390-121">Reference the [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM sizes articles to determine how many NICS each VM size supports.</span></span> 

## <a name="network-security-groups-nsgs"></a><span data-ttu-id="2f390-122">Grupos de segurança de rede (NSG)</span><span class="sxs-lookup"><span data-stu-id="2f390-122">Network Security Groups (NSGs)</span></span>
<span data-ttu-id="2f390-123">Em uma implantação do Gerenciador de recursos, qualquer NIC em uma máquina virtual pode estar associada com um NSG (grupo de segurança de rede), incluindo todas as NICs em uma VM que tenha várias NICs habilitadas.</span><span class="sxs-lookup"><span data-stu-id="2f390-123">In a Resource Manager deployment, any NIC on a VM may be associated with a Network Security Group (NSG), including any NICs on a VM that has multiple NICs enabled.</span></span> <span data-ttu-id="2f390-124">Se uma NIC tiver um endereço atribuído em uma sub-rede que esteja associada a um NSG, as regras do NSG da sub-rede também se aplicarão à NIC.</span><span class="sxs-lookup"><span data-stu-id="2f390-124">If a NIC is assigned an address within a subnet where the subnet is associated with an NSG, then the rules in the subnet’s NSG also apply to that NIC.</span></span> <span data-ttu-id="2f390-125">Além de associar sub-redes a NSGs, você também pode associar uma NIC a um NSG.</span><span class="sxs-lookup"><span data-stu-id="2f390-125">In addition to associating subnets with NSGs, you can also associate a NIC with an NSG.</span></span>

<span data-ttu-id="2f390-126">Se uma sub-rede for associada a um NSG e uma NIC dessa sub-rede for associada individualmente a um NSG, as regras do NSG associado serão aplicadas na **ordem de fluxo** de acordo com a direção do tráfego que estiver sendo passado para dentro ou para fora da NIC:</span><span class="sxs-lookup"><span data-stu-id="2f390-126">If a subnet is associated with an NSG, and a NIC within that subnet is individually associated with an NSG, the associated NSG rules are applied in **flow order** according to the direction of the traffic being passed into or out of the NIC:</span></span>

* <span data-ttu-id="2f390-127">**tráfego de entrada** cujo destino é a NIC em questão flui primeiro pela sub-rede, disparando as regras do NSG da sub-rede, antes de passar pela NIC, quando serão acionadas as regras do NSG da NIC.</span><span class="sxs-lookup"><span data-stu-id="2f390-127">**Incoming traffic** whose destination is the NIC in question flows first through the subnet, triggering the subnet’s NSG rules, before passing into the NIC, then triggering the NIC’s NSG rules.</span></span>
* <span data-ttu-id="2f390-128">**tráfego de saída** cujo destino é a NIC em questão flui primeiro para fora da sub-rede, acionando as regras do NSG da NIC, antes de passar pela sub-rede, quando serão acionadas as regras do NSG da sub-rede.</span><span class="sxs-lookup"><span data-stu-id="2f390-128">**Outgoing traffic** whose source is the NIC in question flows first out from the NIC, triggering the NIC’s NSG rules, before passing through the subnet, then triggering the subnet’s NSG rules.</span></span>

<span data-ttu-id="2f390-129">Saiba mais sobre [grupos de segurança de rede](virtual-networks-nsg.md) e como elas são aplicados com base nas associações a sub-redes, VMs e NICs.</span><span class="sxs-lookup"><span data-stu-id="2f390-129">Learn more about [Network Security Groups](virtual-networks-nsg.md) and how they are applied based on associations to subnets, VMs, and NICs..</span></span>

## <a name="how-to-configure-a-multi-nic-vm-in-a-classic-deployment"></a><span data-ttu-id="2f390-130">Como configurar uma VM de várias NICs em uma implantação clássica</span><span class="sxs-lookup"><span data-stu-id="2f390-130">How to Configure a multi NIC VM in a classic deployment</span></span>
<span data-ttu-id="2f390-131">As instruções a seguir o ajudarão a criar uma VM de várias NICs contendo 3 NICs: uma NIC padrão e duas NICs adicionais.</span><span class="sxs-lookup"><span data-stu-id="2f390-131">The instructions below will help you create a multi NIC VM containing 3 NICs: a default NIC and two additional NICs.</span></span> <span data-ttu-id="2f390-132">As etapas da configuração criarão uma VM que será configurada de acordo com o fragmento do arquivo de configuração de serviços abaixo:</span><span class="sxs-lookup"><span data-stu-id="2f390-132">The configuration steps will create a VM that will be configured according to the service configuration file fragment below:</span></span>

    <VirtualNetworkSite name="MultiNIC-VNet" Location="North Europe">
    <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
    … Skip over the remainder section …
    </VirtualNetworkSite>


<span data-ttu-id="2f390-133">É necessário ter os pré-requisitos a seguir antes de tentar executar os comandos do PowerShell no exemplo.</span><span class="sxs-lookup"><span data-stu-id="2f390-133">You need the following prerequisites before trying to run the PowerShell commands in the example.</span></span>

* <span data-ttu-id="2f390-134">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="2f390-134">An Azure subscription.</span></span>
* <span data-ttu-id="2f390-135">Uma rede virtual configurada.</span><span class="sxs-lookup"><span data-stu-id="2f390-135">A configured virtual network.</span></span> <span data-ttu-id="2f390-136">Confira a [Visão geral da Rede Virtual](virtual-networks-overview.md) para saber mais sobre VNets.</span><span class="sxs-lookup"><span data-stu-id="2f390-136">See [Virtual Network Overview](virtual-networks-overview.md) for more information about VNets.</span></span>
* <span data-ttu-id="2f390-137">A versão mais recente do Azure PowerShell baixada e instalada.</span><span class="sxs-lookup"><span data-stu-id="2f390-137">The latest version of Azure PowerShell downloaded and installed.</span></span> <span data-ttu-id="2f390-138">Consulte [Como instalar e configurar o PowerShell do Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2f390-138">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="2f390-139">Para criar uma VM com várias NICs, conclua as etapas a seguir, inserindo cada comando em uma única sessão do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="2f390-139">To create a VM with multiple NICs, complete the following steps by entering each command within a single PowerShell session:</span></span>

1. <span data-ttu-id="2f390-140">Selecione uma imagem de VM na galeria de imagens de VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="2f390-140">Select a VM image from Azure VM image gallery.</span></span> <span data-ttu-id="2f390-141">Observe que as imagens são alteradas frequentemente e estão disponíveis por região.</span><span class="sxs-lookup"><span data-stu-id="2f390-141">Note that images change frequently and are available by region.</span></span> <span data-ttu-id="2f390-142">A imagem especificada no exemplo a seguir pode ser alterada ou pode não ser da sua região, portanto certifique-se de especificar a imagem correta.</span><span class="sxs-lookup"><span data-stu-id="2f390-142">The image specified in the example below may change or might not be in your region, so be sure to specify the image you need.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    -ImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201410.01-en.us-127GB.vhd"
    ```

2. <span data-ttu-id="2f390-143">Crie a configuração da VM.</span><span class="sxs-lookup"><span data-stu-id="2f390-143">Create a VM configuration.</span></span>

    ```powershell
    $vm = New-AzureVMConfig -Name "MultiNicVM" -InstanceSize "ExtraLarge" `
    -Image $image.ImageName –AvailabilitySetName "MyAVSet"
    ```

3. <span data-ttu-id="2f390-144">Crie o logon de administrador padrão.</span><span class="sxs-lookup"><span data-stu-id="2f390-144">Create the default administrator login.</span></span>

    ```powershell
    Add-AzureProvisioningConfig –VM $vm -Windows -AdminUserName "<YourAdminUID>" `
    -Password "<YourAdminPassword>"
    ```

4. <span data-ttu-id="2f390-145">Adicione outras NICs à configuração da VM.</span><span class="sxs-lookup"><span data-stu-id="2f390-145">Add additional NICs to the VM configuration.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name "Ethernet1" `
    -SubnetName "Midtier" -StaticVNetIPAddress "10.1.1.111" -VM $vm
    Add-AzureNetworkInterfaceConfig -Name "Ethernet2" `
    -SubnetName "Backend" -StaticVNetIPAddress "10.1.2.222" -VM $vm
    ```

5. <span data-ttu-id="2f390-146">Especifique a sub-rede e o endereço IP da NIC padrão.</span><span class="sxs-lookup"><span data-stu-id="2f390-146">Specify the subnet and IP address for the default NIC.</span></span>

    ```powershell
    Set-AzureSubnet -SubnetNames "Frontend" -VM $vm
    Set-AzureStaticVNetIP -IPAddress "10.1.0.100" -VM $vm
    ```

6. <span data-ttu-id="2f390-147">Crie a VM na sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="2f390-147">Create the VM in your virtual network.</span></span>

    ```powershell
    New-AzureVM -ServiceName "MultiNIC-CS" –VNetName "MultiNIC-VNet" –VMs $vm
    ```

    > [!NOTE]
    > <span data-ttu-id="2f390-148">A VNet que você especificar aqui já deve existir (conforme mencionado nos pré-requisitos).</span><span class="sxs-lookup"><span data-stu-id="2f390-148">The VNet that you specify here must already exist (as mentioned in the prerequisites).</span></span> <span data-ttu-id="2f390-149">O exemplo a seguir especifica uma rede virtual chamada **MultiNIC-VNet**.</span><span class="sxs-lookup"><span data-stu-id="2f390-149">The example below specifies a virtual network named **MultiNIC-VNet**.</span></span>
    >

## <a name="limitations"></a><span data-ttu-id="2f390-150">Limitações</span><span class="sxs-lookup"><span data-stu-id="2f390-150">Limitations</span></span>
<span data-ttu-id="2f390-151">As seguintes limitações são aplicáveis ao usar várias NICs:</span><span class="sxs-lookup"><span data-stu-id="2f390-151">The following limitations are applicable when using multiple NICs:</span></span>

* <span data-ttu-id="2f390-152">VMs com várias NICs devem ser criadas nas redes virtuais do Azure (VNets).</span><span class="sxs-lookup"><span data-stu-id="2f390-152">VMs with multiple NICs must be created in Azure virtual networks (VNets).</span></span> <span data-ttu-id="2f390-153">As VMs que não sejam Redes Virtuais não podem ser configuradas com várias NICs.</span><span class="sxs-lookup"><span data-stu-id="2f390-153">Non-VNet VMs cannot be configured with multiple NICs.</span></span>
* <span data-ttu-id="2f390-154">Todas as VMs em um conjunto de disponibilidade precisam usar várias NICs ou uma única NIC.</span><span class="sxs-lookup"><span data-stu-id="2f390-154">All VMs in an availability set need to use either multiple NICs or a single NIC.</span></span> <span data-ttu-id="2f390-155">Não é possível haver uma combinação de VMs com várias NICs e VMs com uma única NIC em um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="2f390-155">There cannot be a mixture of multiple NIC VMs and single NIC VMs within an availability set.</span></span> <span data-ttu-id="2f390-156">As mesmas regras se aplicam a VMs em um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="2f390-156">Same rules apply for VMs in a cloud service.</span></span> <span data-ttu-id="2f390-157">Para VMs de várias NICs, não é necessário ter o mesmo número de NICs, desde que cada uma delas tenha pelo menos duas.</span><span class="sxs-lookup"><span data-stu-id="2f390-157">For multiple NIC VMs, they aren't required to have the same number of NICs, as long as they each have at least two.</span></span>
* <span data-ttu-id="2f390-158">Uma VM com uma única NIC não pode ser configurada com várias NICs (e vice-versa) depois de implantada, sem sua exclusão e recriação.</span><span class="sxs-lookup"><span data-stu-id="2f390-158">A VM with a single NIC cannot be configured with multi NICs (and vice-versa) once it is deployed, without deleting and re-creating it.</span></span>

## <a name="secondary-nics-access-to-other-subnets"></a><span data-ttu-id="2f390-159">Acesso a NICs secundárias a outras sub-redes</span><span class="sxs-lookup"><span data-stu-id="2f390-159">Secondary NICs access to other subnets</span></span>
<span data-ttu-id="2f390-160">Por padrão, as NICs secundárias não serão configuradas com um gateway padrão e, devido a isso, o fluxo de tráfego nas NICs secundárias será limitado à mesma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="2f390-160">By default secondary NICs will not be configured with a default gateway, due to which the traffic flow on the secondary NICs will be limited to be within the same subnet.</span></span> <span data-ttu-id="2f390-161">Se os usuários desejarem habilitar NICs secundárias para falar fora de suas próprias sub-redes, precisarão adicionar uma entrada à tabela de roteamento para configurar o gateway, conforme descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="2f390-161">If the users want to enable secondary NICs to talk outside their own subnet, they will need to add an entry in the routing table to configure the gateway as described below.</span></span>

> [!NOTE]
> <span data-ttu-id="2f390-162">VMs criadas antes de julho de 2015 poderão ter um gateway padrão configurado para todas as NICs.</span><span class="sxs-lookup"><span data-stu-id="2f390-162">VMs created before July 2015 may have a default gateway configured for all NICs.</span></span> <span data-ttu-id="2f390-163">O gateway padrão para NICs secundárias não será removido até que essas VMs sejam reinicializadas.</span><span class="sxs-lookup"><span data-stu-id="2f390-163">The default gateway for secondary NICs will not be removed until these VMs are rebooted.</span></span> <span data-ttu-id="2f390-164">Em sistemas operacionais que usam o modelo de roteamento de host fraco, como o Linux, a conectividade da Internet poderá ser interrompida se o tráfego de entrada e de saída usarem NICs diferentes.</span><span class="sxs-lookup"><span data-stu-id="2f390-164">In Operating systems that use the weak host routing model, such as Linux, Internet connectivity can break if the ingress and egress traffic use different NICs.</span></span>
> 

### <a name="configure-windows-vms"></a><span data-ttu-id="2f390-165">Configurar máquinas virtuais do Windows</span><span class="sxs-lookup"><span data-stu-id="2f390-165">Configure Windows VMs</span></span>
<span data-ttu-id="2f390-166">Suponha que você tenha uma VM do Windows com duas NICs da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="2f390-166">Suppose that you have a Windows VM with two NICs as follows:</span></span>

* <span data-ttu-id="2f390-167">Endereço IP primário da NIC: 192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="2f390-167">Primary NIC IP address: 192.168.1.4</span></span>
* <span data-ttu-id="2f390-168">Endereço IP secundário da NIC: 192.168.2.5</span><span class="sxs-lookup"><span data-stu-id="2f390-168">Secondary NIC IP address: 192.168.2.5</span></span>

<span data-ttu-id="2f390-169">A tabela de rotas do IPv4 para essa VM ficaria assim:</span><span class="sxs-lookup"><span data-stu-id="2f390-169">The IPv4 route table for this VM would look like this:</span></span>

    IPv4 Route Table
    ===========================================================================
    Active Routes:
    Network Destination        Netmask          Gateway       Interface  Metric
              0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
            127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
            127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
      127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        168.63.129.16  255.255.255.255      192.168.1.1      192.168.1.4      6
          192.168.1.0    255.255.255.0         On-link       192.168.1.4    261
          192.168.1.4  255.255.255.255         On-link       192.168.1.4    261
        192.168.1.255  255.255.255.255         On-link       192.168.1.4    261
          192.168.2.0    255.255.255.0         On-link       192.168.2.5    261
          192.168.2.5  255.255.255.255         On-link       192.168.2.5    261
        192.168.2.255  255.255.255.255         On-link       192.168.2.5    261
            224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
            224.0.0.0        240.0.0.0         On-link       192.168.1.4    261
            224.0.0.0        240.0.0.0         On-link       192.168.2.5    261
      255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
      255.255.255.255  255.255.255.255         On-link       192.168.1.4    261
      255.255.255.255  255.255.255.255         On-link       192.168.2.5    261
    ===========================================================================

<span data-ttu-id="2f390-170">Observe que a rota padrão (0.0.0.0) só está disponível para a NIC primária.</span><span class="sxs-lookup"><span data-stu-id="2f390-170">Notice that the default route (0.0.0.0) is only available to the primary NIC.</span></span> <span data-ttu-id="2f390-171">Você não conseguirá acessar recursos fora da sub-rede para a NIC secundária, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="2f390-171">You will not be able to access resources outside the subnet for the secondary NIC, as seen below:</span></span>

    C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5

    Pinging 192.168.1.7 from 192.165.2.5 with 32 bytes of data:
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.

<span data-ttu-id="2f390-172">Para adicionar uma rota padrão à NIC secundária, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="2f390-172">To add a default route on the secondary NIC, follow the steps below:</span></span>

1. <span data-ttu-id="2f390-173">Em um prompt de comando, execute o comando a seguir para identificar o número de índice para a NIC secundária:</span><span class="sxs-lookup"><span data-stu-id="2f390-173">From a command prompt, run the command below to identify the index number for the secondary NIC:</span></span>
   
        C:\Users\Administrator>route print
        ===========================================================================
        Interface List
         29...00 15 17 d9 b1 6d ......Microsoft Virtual Machine Bus Network Adapter #16
         27...00 15 17 d9 b1 41 ......Microsoft Virtual Machine Bus Network Adapter #14
          1...........................Software Loopback Interface 1
         14...00 00 00 00 00 00 00 e0 Teredo Tunneling Pseudo-Interface
         20...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
        ===========================================================================
2. <span data-ttu-id="2f390-174">Observe a segunda entrada na tabela, com um índice de 27 (no exemplo).</span><span class="sxs-lookup"><span data-stu-id="2f390-174">Notice the second entry in the table, with an index of 27 (in this example).</span></span>
3. <span data-ttu-id="2f390-175">No prompt de comando, execute o comando **route add** conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="2f390-175">From the command prompt, run the **route add** command as shown below.</span></span> <span data-ttu-id="2f390-176">Neste exemplo, você está especificando 192.168.2.1 como o gateway padrão para a NIC secundária:</span><span class="sxs-lookup"><span data-stu-id="2f390-176">In this example, you are specifying 192.168.2.1 as the default gateway for the secondary NIC:</span></span>
   
        route ADD -p 0.0.0.0 MASK 0.0.0.0 192.168.2.1 METRIC 5000 IF 27
4. <span data-ttu-id="2f390-177">Para testar a conectividade, volte ao prompt de comando e tente executar o ping em uma sub-rede diferente da NIC secundária, como int eh, mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="2f390-177">To test connectivity, go back to the command prompt and try to ping a different subnet from the secondary NIC as shown int eh example below:</span></span>
   
        C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5
   
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time=2ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
5. <span data-ttu-id="2f390-178">Você também pode conferir a sua tabela de rotas para verificar a rota recém-adicionada, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="2f390-178">You can also check your route table to check the newly added route, as shown below:</span></span>
   
        C:\Users\Administrator>route print
   
        ...
   
        IPv4 Route Table
        ===========================================================================
        Active Routes:
        Network Destination        Netmask          Gateway       Interface  Metric
                  0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
                  0.0.0.0          0.0.0.0      192.168.2.1      192.168.2.5   5005
                127.0.0.0        255.0.0.0         On-link         127.0.0.1    306

### <a name="configure-linux-vms"></a><span data-ttu-id="2f390-179">Configurar máquinas virtuais Linux</span><span class="sxs-lookup"><span data-stu-id="2f390-179">Configure Linux VMs</span></span>
<span data-ttu-id="2f390-180">Para VMs do Linux, como o comportamento padrão usa roteamento de host fraco, recomendamos que as NICs secundárias sejam restritas a fluxos de tráfego somente dentro da mesma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="2f390-180">For Linux VMs, since the default behavior uses weak host routing, we recommend that the secondary NICs are restricted to traffic flows only within the same subnet.</span></span> <span data-ttu-id="2f390-181">No entanto, se determinados cenários exigirem conectividade fora da sub-rede, os usuários devem habilitar a política com base em roteamento para garantir que o tráfego de entrada e saída use a mesma NIC.</span><span class="sxs-lookup"><span data-stu-id="2f390-181">However if certain scenarios demand connectivity outside the subnet, users should enable policy based routing to ensure that the ingress and egress traffic uses the same NIC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f390-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2f390-182">Next steps</span></span>
* <span data-ttu-id="2f390-183">Implante [VMs com MultiNIC em um cenário de aplicativo de 2 camadas, em uma implantação do Gerenciador de Recursos](virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="2f390-183">Deploy [MultiNIC VMs in a 2-tier application scenario in a Resource Manager deployment](virtual-network-deploy-multinic-arm-template.md).</span></span>
* <span data-ttu-id="2f390-184">Implante [VMs com MultiNIC em um cenário de aplicativo de 2 camadas, em uma implantação clássica](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="2f390-184">Deploy [MultiNIC VMs in a 2-tier application scenario in a classic deployment](virtual-network-deploy-multinic-classic-ps.md).</span></span>

