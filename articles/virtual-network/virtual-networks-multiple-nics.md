---
title: "aaaCreate uma VM (clássico) com várias placas de rede usando o PowerShell | Microsoft Docs"
description: "Saiba como toocreate e configurar máquinas virtuais com várias placas de rede usando o PowerShell."
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
ms.openlocfilehash: 8ef35bd4cfd7e6a527080f1cfc541275ca86f5e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics"></a><span data-ttu-id="c5836-103">Criar uma VM (Clássica) com diversas NICs</span><span class="sxs-lookup"><span data-stu-id="c5836-103">Create a VM (Classic) with multiple NICs</span></span>
<span data-ttu-id="c5836-104">Você pode criar máquinas virtuais (VMs) no Azure e anexar várias tooeach (NICs) de interfaces de rede das suas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="c5836-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="c5836-105">Várias NICs são um requisito para muitos aplicativos virtuais de rede, como soluções de distribuição de aplicativos e de otimização de WAN.</span><span class="sxs-lookup"><span data-stu-id="c5836-105">Multiple NICs are a requirement for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span> <span data-ttu-id="c5836-106">Várias NICs também fornecem isolamento do tráfego entre NICs.</span><span class="sxs-lookup"><span data-stu-id="c5836-106">Multiple NICs also provide isolation of traffic between NICs.</span></span>

![Várias NICs da VM](./media/virtual-networks-multiple-nics/IC757773.png)

<span data-ttu-id="c5836-108">Olá figura mostra uma VM com três NICs, cada um conectado tooa outra sub-rede.</span><span class="sxs-lookup"><span data-stu-id="c5836-108">hello figure shows a VM with three NICs, each connected tooa different subnet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c5836-109">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c5836-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c5836-110">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="c5836-110">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="c5836-111">A Microsoft recomenda que a maioria das implantações novas use o Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="c5836-111">Microsoft recommends that most new deployments use Resource Manager.</span></span>

* <span data-ttu-id="c5836-112">Só há suporte para o VIP da Internet (implantações clássicas) em uma NIC hello "padrão".</span><span class="sxs-lookup"><span data-stu-id="c5836-112">Internet-facing VIP (classic deployments) is only supported on hello "default" NIC.</span></span> <span data-ttu-id="c5836-113">Há apenas um VIP toohello IP da NIC saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="c5836-113">There is only one VIP toohello IP of hello default NIC.</span></span>
* <span data-ttu-id="c5836-114">Neste momento, não há suporte para endereços LPIP (PI público no nível da instância) (implantações clássicas) para VMs com várias NICs.</span><span class="sxs-lookup"><span data-stu-id="c5836-114">At this time, Instance Level Public IP (LPIP) addresses (classic deployments) are not supported for multi NIC VMs.</span></span>
* <span data-ttu-id="c5836-115">Olá a ordem das NICs de saudação do dentro Olá VM será aleatória e também pode mudar entre atualizações de infraestrutura do Azure.</span><span class="sxs-lookup"><span data-stu-id="c5836-115">hello order of hello NICs from inside hello VM will be random, and could also change across Azure infrastructure updates.</span></span> <span data-ttu-id="c5836-116">No entanto, Olá endereços IP e Olá correspondente ethernet MAC permanecerão endereços Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="c5836-116">However, hello IP addresses, and hello corresponding ethernet MAC addresses will remain hello same.</span></span> <span data-ttu-id="c5836-117">Por exemplo, suponha que **Eth1** tem o endereço IP 10.1.0.100 e o endereço MAC 00-0D-3A-B0-39-0D; após uma atualização de infraestrutura do Azure e a reinicialização, ela pode ser alterada muito**Eth2**, mas Olá IP e MAC emparelhamento será permanecem Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="c5836-117">For example, assume **Eth1** has IP address 10.1.0.100 and MAC address 00-0D-3A-B0-39-0D; after an Azure infrastructure update and reboot, it could be changed too**Eth2**, but hello IP and MAC pairing will remain hello same.</span></span> <span data-ttu-id="c5836-118">Quando uma reinicialização for iniciada pelo cliente, Olá ordem da NIC permanecerá Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="c5836-118">When a restart is customer-initiated, hello NIC order will remain hello same.</span></span>
* <span data-ttu-id="c5836-119">Olá endereço para cada NIC em cada VM deve estar localizado em uma sub-rede, várias NICs em uma única VM pode cada ter Olá de endereços que estão na mesma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="c5836-119">hello address for each NIC on each VM must be located in a subnet, multiple NICs on a single VM can each be assigned addresses that are in hello same subnet.</span></span>
* <span data-ttu-id="c5836-120">Olá tamanho da VM determina o número de saudação de NICS que você pode criar para uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c5836-120">hello VM size determines hello number of NICS that you can create for a VM.</span></span> <span data-ttu-id="c5836-121">Saudação de referência [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tamanhos de VM toodetermine artigos de quantos NICS dá suporte a cada tamanho VM.</span><span class="sxs-lookup"><span data-stu-id="c5836-121">Reference hello [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM sizes articles toodetermine how many NICS each VM size supports.</span></span> 

## <a name="network-security-groups-nsgs"></a><span data-ttu-id="c5836-122">Grupos de segurança de rede (NSG)</span><span class="sxs-lookup"><span data-stu-id="c5836-122">Network Security Groups (NSGs)</span></span>
<span data-ttu-id="c5836-123">Em uma implantação do Gerenciador de recursos, qualquer NIC em uma máquina virtual pode estar associada com um NSG (grupo de segurança de rede), incluindo todas as NICs em uma VM que tenha várias NICs habilitadas.</span><span class="sxs-lookup"><span data-stu-id="c5836-123">In a Resource Manager deployment, any NIC on a VM may be associated with a Network Security Group (NSG), including any NICs on a VM that has multiple NICs enabled.</span></span> <span data-ttu-id="c5836-124">Se uma NIC é atribuída um endereço de sub-rede onde a sub-rede de saudação é associada um NSG, em seguida, hello regras NSG da sub-rede Olá também se aplicam NIC toothat.</span><span class="sxs-lookup"><span data-stu-id="c5836-124">If a NIC is assigned an address within a subnet where hello subnet is associated with an NSG, then hello rules in hello subnet’s NSG also apply toothat NIC.</span></span> <span data-ttu-id="c5836-125">Em sub-redes tooassociating de adição com NSGs, você também pode associar uma NIC com um NSG.</span><span class="sxs-lookup"><span data-stu-id="c5836-125">In addition tooassociating subnets with NSGs, you can also associate a NIC with an NSG.</span></span>

<span data-ttu-id="c5836-126">Se uma sub-rede é associada a um NSG e uma NIC dentro dessa sub-rede individualmente associada a um NSG, Olá associado NSG regras são aplicadas em **fluxo ordem** toohello direção do tráfego de saudação sendo passado dentro ou fora de acordo com Olá NIC:</span><span class="sxs-lookup"><span data-stu-id="c5836-126">If a subnet is associated with an NSG, and a NIC within that subnet is individually associated with an NSG, hello associated NSG rules are applied in **flow order** according toohello direction of hello traffic being passed into or out of hello NIC:</span></span>

* <span data-ttu-id="c5836-127">**Tráfego de entrada** cujo destino é hello NIC em questão flui do primeiro sub-rede hello, disparar regras NSG da sub-rede hello, antes de passar para Olá NIC e disparar regras NSG de saudação do NIC.</span><span class="sxs-lookup"><span data-stu-id="c5836-127">**Incoming traffic** whose destination is hello NIC in question flows first through hello subnet, triggering hello subnet’s NSG rules, before passing into hello NIC, then triggering hello NIC’s NSG rules.</span></span>
* <span data-ttu-id="c5836-128">**Tráfego de saída** cuja origem é hello NIC em questão flui primeiro a sair de saudação NIC, disparar regras NSG da NIC hello, antes de passar por sub-rede hello e disparar regras do NSG da sub-rede hello.</span><span class="sxs-lookup"><span data-stu-id="c5836-128">**Outgoing traffic** whose source is hello NIC in question flows first out from hello NIC, triggering hello NIC’s NSG rules, before passing through hello subnet, then triggering hello subnet’s NSG rules.</span></span>

<span data-ttu-id="c5836-129">Saiba mais sobre [grupos de segurança de rede](virtual-networks-nsg.md) e como elas são aplicadas com base nas associações toosubnets, VMs e NICs.</span><span class="sxs-lookup"><span data-stu-id="c5836-129">Learn more about [Network Security Groups](virtual-networks-nsg.md) and how they are applied based on associations toosubnets, VMs, and NICs..</span></span>

## <a name="how-tooconfigure-a-multi-nic-vm-in-a-classic-deployment"></a><span data-ttu-id="c5836-130">Como tooConfigure uma várias VMs de NIC em uma implantação clássica</span><span class="sxs-lookup"><span data-stu-id="c5836-130">How tooConfigure a multi NIC VM in a classic deployment</span></span>
<span data-ttu-id="c5836-131">instruções de saudação abaixo ajudará você a criar uma várias VMs de NIC contendo 3 NICs: uma NIC padrão e duas NICs adicionais.</span><span class="sxs-lookup"><span data-stu-id="c5836-131">hello instructions below will help you create a multi NIC VM containing 3 NICs: a default NIC and two additional NICs.</span></span> <span data-ttu-id="c5836-132">etapas de configuração de saudação criará uma VM que será configurada de acordo com o fragmento configuração de arquivo do serviço toohello abaixo:</span><span class="sxs-lookup"><span data-stu-id="c5836-132">hello configuration steps will create a VM that will be configured according toohello service configuration file fragment below:</span></span>

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
    … Skip over hello remainder section …
    </VirtualNetworkSite>


<span data-ttu-id="c5836-133">Você precisa de saudação pré-requisitos a seguir antes de tentar toorun Olá comandos do PowerShell exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="c5836-133">You need hello following prerequisites before trying toorun hello PowerShell commands in hello example.</span></span>

* <span data-ttu-id="c5836-134">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="c5836-134">An Azure subscription.</span></span>
* <span data-ttu-id="c5836-135">Uma rede virtual configurada.</span><span class="sxs-lookup"><span data-stu-id="c5836-135">A configured virtual network.</span></span> <span data-ttu-id="c5836-136">Confira a [Visão geral da Rede Virtual](virtual-networks-overview.md) para saber mais sobre VNets.</span><span class="sxs-lookup"><span data-stu-id="c5836-136">See [Virtual Network Overview](virtual-networks-overview.md) for more information about VNets.</span></span>
* <span data-ttu-id="c5836-137">versão mais recente de saudação do Azure PowerShell baixada e instalada.</span><span class="sxs-lookup"><span data-stu-id="c5836-137">hello latest version of Azure PowerShell downloaded and installed.</span></span> <span data-ttu-id="c5836-138">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c5836-138">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="c5836-139">toocreate uma VM com várias NICs, Olá concluir etapas a seguir, inserindo cada comando em uma única sessão do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c5836-139">toocreate a VM with multiple NICs, complete hello following steps by entering each command within a single PowerShell session:</span></span>

1. <span data-ttu-id="c5836-140">Selecione uma imagem de VM na galeria de imagens de VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="c5836-140">Select a VM image from Azure VM image gallery.</span></span> <span data-ttu-id="c5836-141">Observe que as imagens são alteradas frequentemente e estão disponíveis por região.</span><span class="sxs-lookup"><span data-stu-id="c5836-141">Note that images change frequently and are available by region.</span></span> <span data-ttu-id="c5836-142">Olá imagem especificada no exemplo hello abaixo pode alterar ou pode não estar em sua região, portanto, imagem Olá toospecify que você precisa.</span><span class="sxs-lookup"><span data-stu-id="c5836-142">hello image specified in hello example below may change or might not be in your region, so be sure toospecify hello image you need.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    -ImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201410.01-en.us-127GB.vhd"
    ```

2. <span data-ttu-id="c5836-143">Crie a configuração da VM.</span><span class="sxs-lookup"><span data-stu-id="c5836-143">Create a VM configuration.</span></span>

    ```powershell
    $vm = New-AzureVMConfig -Name "MultiNicVM" -InstanceSize "ExtraLarge" `
    -Image $image.ImageName –AvailabilitySetName "MyAVSet"
    ```

3. <span data-ttu-id="c5836-144">Crie logon de administrador saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="c5836-144">Create hello default administrator login.</span></span>

    ```powershell
    Add-AzureProvisioningConfig –VM $vm -Windows -AdminUserName "<YourAdminUID>" `
    -Password "<YourAdminPassword>"
    ```

4. <span data-ttu-id="c5836-145">Adicione configuração da VM toohello NICs adicional.</span><span class="sxs-lookup"><span data-stu-id="c5836-145">Add additional NICs toohello VM configuration.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name "Ethernet1" `
    -SubnetName "Midtier" -StaticVNetIPAddress "10.1.1.111" -VM $vm
    Add-AzureNetworkInterfaceConfig -Name "Ethernet2" `
    -SubnetName "Backend" -StaticVNetIPAddress "10.1.2.222" -VM $vm
    ```

5. <span data-ttu-id="c5836-146">Especifique uma sub-rede de saudação e endereço IP para a NIC saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="c5836-146">Specify hello subnet and IP address for hello default NIC.</span></span>

    ```powershell
    Set-AzureSubnet -SubnetNames "Frontend" -VM $vm
    Set-AzureStaticVNetIP -IPAddress "10.1.0.100" -VM $vm
    ```

6. <span data-ttu-id="c5836-147">Crie hello VM em sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c5836-147">Create hello VM in your virtual network.</span></span>

    ```powershell
    New-AzureVM -ServiceName "MultiNIC-CS" –VNetName "MultiNIC-VNet" –VMs $vm
    ```

    > [!NOTE]
    > <span data-ttu-id="c5836-148">Olá VNet que você especificar aqui já deve existir (conforme mencionado nos pré-requisitos Olá).</span><span class="sxs-lookup"><span data-stu-id="c5836-148">hello VNet that you specify here must already exist (as mentioned in hello prerequisites).</span></span> <span data-ttu-id="c5836-149">exemplo Hello abaixo especifica uma rede virtual denominada **MultiNIC-VNet**.</span><span class="sxs-lookup"><span data-stu-id="c5836-149">hello example below specifies a virtual network named **MultiNIC-VNet**.</span></span>
    >

## <a name="limitations"></a><span data-ttu-id="c5836-150">Limitações</span><span class="sxs-lookup"><span data-stu-id="c5836-150">Limitations</span></span>
<span data-ttu-id="c5836-151">Olá limitações a seguir é aplicável ao usar várias NICs:</span><span class="sxs-lookup"><span data-stu-id="c5836-151">hello following limitations are applicable when using multiple NICs:</span></span>

* <span data-ttu-id="c5836-152">VMs com várias NICs devem ser criadas nas redes virtuais do Azure (VNets).</span><span class="sxs-lookup"><span data-stu-id="c5836-152">VMs with multiple NICs must be created in Azure virtual networks (VNets).</span></span> <span data-ttu-id="c5836-153">As VMs que não sejam Redes Virtuais não podem ser configuradas com várias NICs.</span><span class="sxs-lookup"><span data-stu-id="c5836-153">Non-VNet VMs cannot be configured with multiple NICs.</span></span>
* <span data-ttu-id="c5836-154">Todas as VMs em um disponibilidade definido necessidade toouse várias NICs ou uma única placa de rede.</span><span class="sxs-lookup"><span data-stu-id="c5836-154">All VMs in an availability set need toouse either multiple NICs or a single NIC.</span></span> <span data-ttu-id="c5836-155">Não é possível haver uma combinação de VMs com várias NICs e VMs com uma única NIC em um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="c5836-155">There cannot be a mixture of multiple NIC VMs and single NIC VMs within an availability set.</span></span> <span data-ttu-id="c5836-156">As mesmas regras se aplicam a VMs em um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="c5836-156">Same rules apply for VMs in a cloud service.</span></span> <span data-ttu-id="c5836-157">Para várias VMs de NIC, eles não são necessários toohave Olá mesmo número de NICs, desde que cada um deles tem pelo menos dois.</span><span class="sxs-lookup"><span data-stu-id="c5836-157">For multiple NIC VMs, they aren't required toohave hello same number of NICs, as long as they each have at least two.</span></span>
* <span data-ttu-id="c5836-158">Uma VM com uma única NIC não pode ser configurada com várias NICs (e vice-versa) depois de implantada, sem sua exclusão e recriação.</span><span class="sxs-lookup"><span data-stu-id="c5836-158">A VM with a single NIC cannot be configured with multi NICs (and vice-versa) once it is deployed, without deleting and re-creating it.</span></span>

## <a name="secondary-nics-access-tooother-subnets"></a><span data-ttu-id="c5836-159">Secundário NICs acesso tooother sub-redes</span><span class="sxs-lookup"><span data-stu-id="c5836-159">Secondary NICs access tooother subnets</span></span>
<span data-ttu-id="c5836-160">Por padrão NICs secundárias não serão configuradas com um gateway padrão, devido o fluxo de tráfego de saudação toowhich em Olá NICs secundárias será limitado toobe dentro Olá mesma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="c5836-160">By default secondary NICs will not be configured with a default gateway, due toowhich hello traffic flow on hello secondary NICs will be limited toobe within hello same subnet.</span></span> <span data-ttu-id="c5836-161">Se quiserem que os usuários de saudação tooenable secundário NICs tootalk fora da sua própria sub-rede, será necessário tooadd uma entrada na Olá tabela tooconfigure Olá gateway de roteamento como descrita abaixo.</span><span class="sxs-lookup"><span data-stu-id="c5836-161">If hello users want tooenable secondary NICs tootalk outside their own subnet, they will need tooadd an entry in hello routing table tooconfigure hello gateway as described below.</span></span>

> [!NOTE]
> <span data-ttu-id="c5836-162">VMs criadas antes de julho de 2015 poderão ter um gateway padrão configurado para todas as NICs.</span><span class="sxs-lookup"><span data-stu-id="c5836-162">VMs created before July 2015 may have a default gateway configured for all NICs.</span></span> <span data-ttu-id="c5836-163">gateway padrão Olá NICs secundárias não será removido até que essas VMs são reiniciados.</span><span class="sxs-lookup"><span data-stu-id="c5836-163">hello default gateway for secondary NICs will not be removed until these VMs are rebooted.</span></span> <span data-ttu-id="c5836-164">Em sistemas operacionais que usam o modelo roteamento de saudação host fraco, como o Linux, a conectividade com a Internet pode quebrar se o tráfego de entrada e saída hello usar NICs diferentes.</span><span class="sxs-lookup"><span data-stu-id="c5836-164">In Operating systems that use hello weak host routing model, such as Linux, Internet connectivity can break if hello ingress and egress traffic use different NICs.</span></span>
> 

### <a name="configure-windows-vms"></a><span data-ttu-id="c5836-165">Configurar máquinas virtuais do Windows</span><span class="sxs-lookup"><span data-stu-id="c5836-165">Configure Windows VMs</span></span>
<span data-ttu-id="c5836-166">Suponha que você tenha uma VM do Windows com duas NICs da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="c5836-166">Suppose that you have a Windows VM with two NICs as follows:</span></span>

* <span data-ttu-id="c5836-167">Endereço IP primário da NIC: 192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="c5836-167">Primary NIC IP address: 192.168.1.4</span></span>
* <span data-ttu-id="c5836-168">Endereço IP secundário da NIC: 192.168.2.5</span><span class="sxs-lookup"><span data-stu-id="c5836-168">Secondary NIC IP address: 192.168.2.5</span></span>

<span data-ttu-id="c5836-169">tabela de rotas do IPv4 Olá para essa VM deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="c5836-169">hello IPv4 route table for this VM would look like this:</span></span>

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

<span data-ttu-id="c5836-170">Observe a que rota padrão (0.0.0.0) hello está apenas disponível toohello principal placa de rede.</span><span class="sxs-lookup"><span data-stu-id="c5836-170">Notice that hello default route (0.0.0.0) is only available toohello primary NIC.</span></span> <span data-ttu-id="c5836-171">Você não será capaz de tooaccess recursos fora da sub-rede Olá Olá secundário NIC, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="c5836-171">You will not be able tooaccess resources outside hello subnet for hello secondary NIC, as seen below:</span></span>

    C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5

    Pinging 192.168.1.7 from 192.165.2.5 with 32 bytes of data:
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.

<span data-ttu-id="c5836-172">tooadd uma rota padrão em Olá NIC secundário, siga Olá etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="c5836-172">tooadd a default route on hello secondary NIC, follow hello steps below:</span></span>

1. <span data-ttu-id="c5836-173">Em um prompt de comando, execute o comando de saudação abaixo tooidentify Olá número de índice para Olá NIC secundário:</span><span class="sxs-lookup"><span data-stu-id="c5836-173">From a command prompt, run hello command below tooidentify hello index number for hello secondary NIC:</span></span>
   
        C:\Users\Administrator>route print
        ===========================================================================
        Interface List
         29...00 15 17 d9 b1 6d ......Microsoft Virtual Machine Bus Network Adapter #16
         27...00 15 17 d9 b1 41 ......Microsoft Virtual Machine Bus Network Adapter #14
          1...........................Software Loopback Interface 1
         14...00 00 00 00 00 00 00 e0 Teredo Tunneling Pseudo-Interface
         20...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
        ===========================================================================
2. <span data-ttu-id="c5836-174">Observe que a segunda entrada hello na tabela hello, com um índice de 27 (no exemplo).</span><span class="sxs-lookup"><span data-stu-id="c5836-174">Notice hello second entry in hello table, with an index of 27 (in this example).</span></span>
3. <span data-ttu-id="c5836-175">Saudação prompt de comando, execute Olá **Adicionar rota** comando conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="c5836-175">From hello command prompt, run hello **route add** command as shown below.</span></span> <span data-ttu-id="c5836-176">Neste exemplo, você está especificando 192.168.2.1 como gateway padrão Olá Olá NIC secundário:</span><span class="sxs-lookup"><span data-stu-id="c5836-176">In this example, you are specifying 192.168.2.1 as hello default gateway for hello secondary NIC:</span></span>
   
        route ADD -p 0.0.0.0 MASK 0.0.0.0 192.168.2.1 METRIC 5000 IF 27
4. <span data-ttu-id="c5836-177">conectividade de tootest voltar toohello prompt de comando e tente tooping uma sub-rede diferente do hello NIC secundário como int mostrado eh exemplo abaixo:</span><span class="sxs-lookup"><span data-stu-id="c5836-177">tootest connectivity, go back toohello command prompt and try tooping a different subnet from hello secondary NIC as shown int eh example below:</span></span>
   
        C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5
   
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time=2ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
5. <span data-ttu-id="c5836-178">Você também pode verificar que a saudação de toocheck de tabela de rota recém-adicionado rota, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="c5836-178">You can also check your route table toocheck hello newly added route, as shown below:</span></span>
   
        C:\Users\Administrator>route print
   
        ...
   
        IPv4 Route Table
        ===========================================================================
        Active Routes:
        Network Destination        Netmask          Gateway       Interface  Metric
                  0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
                  0.0.0.0          0.0.0.0      192.168.2.1      192.168.2.5   5005
                127.0.0.0        255.0.0.0         On-link         127.0.0.1    306

### <a name="configure-linux-vms"></a><span data-ttu-id="c5836-179">Configurar máquinas virtuais Linux</span><span class="sxs-lookup"><span data-stu-id="c5836-179">Configure Linux VMs</span></span>
<span data-ttu-id="c5836-180">Para VMs do Linux, como o comportamento padrão de saudação usa host fraco roteamento, recomendamos que Olá secundárias NICs são fluxos de tootraffic restrito apenas em Olá mesma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="c5836-180">For Linux VMs, since hello default behavior uses weak host routing, we recommend that hello secondary NICs are restricted tootraffic flows only within hello same subnet.</span></span> <span data-ttu-id="c5836-181">No entanto, se determinados cenários exigem conectividade fora da sub-rede hello, os usuários devem habilitar tooensure de roteamento baseado em política que Olá ingresso e usos de tráfego de saída Olá NIC mesmo.</span><span class="sxs-lookup"><span data-stu-id="c5836-181">However if certain scenarios demand connectivity outside hello subnet, users should enable policy based routing tooensure that hello ingress and egress traffic uses hello same NIC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5836-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c5836-182">Next steps</span></span>
* <span data-ttu-id="c5836-183">Implante [VMs com MultiNIC em um cenário de aplicativo de 2 camadas, em uma implantação do Gerenciador de Recursos](virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="c5836-183">Deploy [MultiNIC VMs in a 2-tier application scenario in a Resource Manager deployment](virtual-network-deploy-multinic-arm-template.md).</span></span>
* <span data-ttu-id="c5836-184">Implante [VMs com MultiNIC em um cenário de aplicativo de 2 camadas, em uma implantação clássica](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c5836-184">Deploy [MultiNIC VMs in a 2-tier application scenario in a classic deployment](virtual-network-deploy-multinic-classic-ps.md).</span></span>

