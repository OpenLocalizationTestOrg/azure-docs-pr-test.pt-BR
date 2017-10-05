---
title: "Solucionar problemas de rotas – PowerShell | Microsoft Docs"
description: "Saiba como solucionar problemas de rotas no modelo de implantação do Azure Resource Manager usando o Azure PowerShell."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: bf7dc5e7-9399-460e-8e0d-8992dbed98a6
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 141e3c571d744470fd07e99538b6e38d4144e8d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-routes-using-azure-powershell"></a><span data-ttu-id="274dc-103">Solucionar problemas de rotas usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="274dc-103">Troubleshoot routes using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="274dc-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="274dc-104">Azure Portal</span></span>](virtual-network-routes-troubleshoot-portal.md)
> * [<span data-ttu-id="274dc-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="274dc-105">PowerShell</span></span>](virtual-network-routes-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="274dc-106">Se você está tendo problemas de conectividade de rede para ou da sua VM (máquina virtual) do Azure, as rotas podem estar afetando os fluxos de tráfego da sua VM.</span><span class="sxs-lookup"><span data-stu-id="274dc-106">If you are experiencing network connectivity issues to or from your Azure Virtual Machine (VM), routes may be impacting your VM traffic flows.</span></span> <span data-ttu-id="274dc-107">Este artigo oferece uma visão geral dos recursos de diagnóstico para rotas a fim de ajudar a solucionar outros problemas.</span><span class="sxs-lookup"><span data-stu-id="274dc-107">This article provides an overview of diagnostics capabilities for routes to help troubleshoot further.</span></span>

<span data-ttu-id="274dc-108">As tabelas de rotas são associadas a sub-redes e estão em vigor em todas as NICs (interfaces de rede) nessa sub-rede.</span><span class="sxs-lookup"><span data-stu-id="274dc-108">Route tables are associated with subnets and are effective on all network interfaces (NIC) in that subnet.</span></span> <span data-ttu-id="274dc-109">Os seguintes tipos de rotas podem ser aplicados a cada adaptador de rede:</span><span class="sxs-lookup"><span data-stu-id="274dc-109">The following types of routes can be applied to each network interface:</span></span>

* <span data-ttu-id="274dc-110">**Rotas de sistema:** por padrão, cada sub-rede criada em uma VNet (rede virtual) do Azure tem tabelas de rotas de sistema que possibilitam o tráfego da VNet, o tráfego local por meio de gateways de VPN e o tráfego da Internet.</span><span class="sxs-lookup"><span data-stu-id="274dc-110">**System routes:** By default, every subnet created in an Azure Virtual Network (VNet) has system route tables that allow local VNet traffic, on-premises traffic via VPN gateways, and Internet traffic.</span></span> <span data-ttu-id="274dc-111">Também existem rotas de sistema para VNets emparelhadas.</span><span class="sxs-lookup"><span data-stu-id="274dc-111">System routes also exist for peered VNets.</span></span>
* <span data-ttu-id="274dc-112">**Rotas BGP:** propagadas para adaptadores de rede por meio do ExpressRoute ou conexões VPN site a site.</span><span class="sxs-lookup"><span data-stu-id="274dc-112">**BGP routes:** Propagated to network interfaces through ExpressRoute or site-to-site VPN connections.</span></span> <span data-ttu-id="274dc-113">Saiba mais sobre o roteamento BGP lendo os artigos [BGP com gateways de VPN](../vpn-gateway/vpn-gateway-bgp-overview.md) e de [visão geral do ExpressRoute](../expressroute/expressroute-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="274dc-113">Learn more about BGP routing by reading the [BGP with VPN gateways](../vpn-gateway/vpn-gateway-bgp-overview.md) and [ExpressRoute overview](../expressroute/expressroute-introduction.md) articles.</span></span>
* <span data-ttu-id="274dc-114">**UDR (Rotas definidas pelo usuário):** se você estiver usando soluções de virtualização de rede ou fazendo o túnel forçado do tráfego para uma rede local por meio de uma VPN site a site, você poderá ter UDRs (rotas definidas pelo usuário) associadas à sua tabela de rotas de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="274dc-114">**User-defined routes (UDR):** If you are using network virtual appliances or are forced-tunneling traffic to an on-premises network via a site-to-site VPN, you may have user-defined routes (UDRs) associated with your subnet route table.</span></span> <span data-ttu-id="274dc-115">Se você não estiver familiarizado com UDRs, leia o artigo [rotas definidas pelo usuário](virtual-networks-udr-overview.md#user-defined-routes) .</span><span class="sxs-lookup"><span data-stu-id="274dc-115">If you're not familiar with UDRs, read the [user-defined routes](virtual-networks-udr-overview.md#user-defined-routes) article.</span></span>

<span data-ttu-id="274dc-116">Com as várias rotas que podem ser aplicadas a um adaptador de rede, pode ser difícil determinar quais rotas agregadas estão em vigor.</span><span class="sxs-lookup"><span data-stu-id="274dc-116">With the various routes that can be applied to a network interface, it can be difficult to determine which aggregate routes are effective.</span></span> <span data-ttu-id="274dc-117">Para ajudar a solucionar problemas de conectividade de rede da VM, você pode exibir todas as rotas em vigor para um adaptador de rede no modelo de implantação do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="274dc-117">To help troubleshoot VM network connectivity, you can view all the effective routes for a network interface in the Azure Resource Manager deployment model.</span></span>

## <a name="using-effective-routes-to-troubleshoot-vm-traffic-flow"></a><span data-ttu-id="274dc-118">Usando rotas em vigor para solucionar problemas de fluxo de tráfego da VM</span><span class="sxs-lookup"><span data-stu-id="274dc-118">Using Effective Routes to troubleshoot VM traffic flow</span></span>
<span data-ttu-id="274dc-119">Este artigo usa o cenário a seguir como um exemplo para ilustrar como solucionar problemas das rotas em vigor de um adaptador de rede:</span><span class="sxs-lookup"><span data-stu-id="274dc-119">This article uses the following scenario as an example to illustrate how to troubleshoot the effective routes for a network interface:</span></span>

<span data-ttu-id="274dc-120">Uma VM (*VM1*) conectada à VNet (*VNet1*, prefixo: 10.9.0.0/16) falha ao se conectar a uma VM(VM3) em uma VNet recém-emparelhada (*VNet3*, prefixo 10.10.0.0/16).</span><span class="sxs-lookup"><span data-stu-id="274dc-120">A VM (*VM1*) connected to the VNet (*VNet1*, prefix: 10.9.0.0/16) fails to connect to a VM(VM3) in a newly peered VNet (*VNet3*, prefix 10.10.0.0/16).</span></span> <span data-ttu-id="274dc-121">Não há nenhuma UDR ou rotas BGP aplicadas ao adaptador de rede VM1-NIC1 conectado à VM. Apenas rotas de sistema foram aplicadas.</span><span class="sxs-lookup"><span data-stu-id="274dc-121">There are no UDRs or BGP routes applied to VM1-NIC1 network interface connected to the VM, only system routes are applied.</span></span>

<span data-ttu-id="274dc-122">Este artigo explica como determinar a causa da falha de conexão, usando a funcionalidade de rotas em vigor no modelo de implantação do Gerenciamento de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="274dc-122">This article explains how to determine the cause of the connection failure, using effective routes capability in Azure Resource Management deployment model.</span></span>
<span data-ttu-id="274dc-123">Embora o exemplo use somente rotas de sistema, as mesmas etapas podem ser usadas para determinar falhas de conexão de entrada e saída em qualquer tipo de porta.</span><span class="sxs-lookup"><span data-stu-id="274dc-123">While the example uses only system routes, the same steps can be used to determine inbound and outbound connection failures over any route type.</span></span>

> [!NOTE]
> <span data-ttu-id="274dc-124">Se sua VM tiver mais de uma NIC conectada, verifique as rotas em vigor para cada uma das NICs a fim de diagnosticar problemas de conectividade de rede para e de uma VM.</span><span class="sxs-lookup"><span data-stu-id="274dc-124">If your VM has more than one NIC attached, check effective routes for each of the NICs to diagnose network connectivity issues to and from a VM.</span></span>
> 
> 

### <a name="view-effective-routes-for-a-virtual-machine"></a><span data-ttu-id="274dc-125">Exibir rotas em vigor para uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="274dc-125">View effective routes for a virtual machine</span></span>
<span data-ttu-id="274dc-126">Para ver as rotas agregadas aplicadas a uma VM, siga as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="274dc-126">To see the aggregate routes that are applied to a VM, complete the following steps:</span></span>

### <a name="view-effective-routes-for-a-network-interface"></a><span data-ttu-id="274dc-127">Exibir rotas em vigor para um adaptador de rede</span><span class="sxs-lookup"><span data-stu-id="274dc-127">View effective routes for a network interface</span></span>
<span data-ttu-id="274dc-128">Para ver as rotas agregadas aplicadas a um adaptador de rede, siga as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="274dc-128">To see the aggregate routes that are applied to a network interface, complete the following steps:</span></span>

1. <span data-ttu-id="274dc-129">Inicie uma sessão do Azure PowerShell e faça logon no Azure.</span><span class="sxs-lookup"><span data-stu-id="274dc-129">Start an Azure PowerShell session and login to Azure.</span></span> <span data-ttu-id="274dc-130">Se você não estiver familiarizado com o Azure PowerShell, leia o artigo [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="274dc-130">If you’re not familiar with Azure PowerShell, read the [How to install and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="274dc-131">O comando a seguir retorna todas as rotas aplicadas a um adaptador de rede denominado *VM1-NIC1* no grupo de recursos *RG1*.</span><span class="sxs-lookup"><span data-stu-id="274dc-131">The following command returns all routes applied to a network interface named *VM1-NIC1* in the resource group *RG1*.</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > <span data-ttu-id="274dc-132">Se você não souber o nome de um adaptador de rede, digite o seguinte comando para recuperar os nomes de todos os adaptadores de rede em um grupo de recursos.*</span><span class="sxs-lookup"><span data-stu-id="274dc-132">If you don’t know the name of a network interface, type the following command to retrieve the names of all network interfaces in a resource group.*</span></span>
   > 
   > 
   
       Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name
   
   <span data-ttu-id="274dc-133">A seguinte saída é semelhante à saída de cada rota aplicada à sub-rede à qual a NIC está conectada:</span><span class="sxs-lookup"><span data-stu-id="274dc-133">The following output looks similar to the output for each route applied to the subnet the NIC is connected to:</span></span>
   
       Name :
       State : Active
       AddressPrefix : {10.9.0.0/16}
       NextHopType : VNetLocal
       NextHopIpAddress : {}
   
       Name :
       State : Active
       AddressPrefix : {0.0.0.0/16}
       NextHopType : Internet
       NextHopIpAddress : {}
   
   <span data-ttu-id="274dc-134">Observe o seguinte na saída:</span><span class="sxs-lookup"><span data-stu-id="274dc-134">Notice the following in the output:</span></span>
   
   * <span data-ttu-id="274dc-135">**Name**: o nome da rota em vigor pode estar vazio, a menos que explicitamente especificado, para rotas definidas pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="274dc-135">**Name**: Name of the effective route may be empty, unless explicitly specified, for user-defined routes.</span></span> 
   * <span data-ttu-id="274dc-136">**State**: indica o estado da rota em vigor.</span><span class="sxs-lookup"><span data-stu-id="274dc-136">**State**: Indicates state of the effective route.</span></span> <span data-ttu-id="274dc-137">Os valores possíveis são “Active” ou “Invalid”</span><span class="sxs-lookup"><span data-stu-id="274dc-137">Possible values are "Active" or "Invalid"</span></span>
   * <span data-ttu-id="274dc-138">**AddressPrefixes**: especifica o prefixo do endereço da rota em vigor na notação CIDR.</span><span class="sxs-lookup"><span data-stu-id="274dc-138">**AddressPrefixes**: Specifies the address prefix of the effective route in CIDR notation.</span></span> 
   * <span data-ttu-id="274dc-139">**nextHopType**: indica o próximo salto para a rota determinada.</span><span class="sxs-lookup"><span data-stu-id="274dc-139">**nextHopType**: Indicates the next hop for the given route.</span></span> <span data-ttu-id="274dc-140">Os valores possíveis são *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering* ou *Null*.</span><span class="sxs-lookup"><span data-stu-id="274dc-140">Possible values are *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, or *Null*.</span></span> <span data-ttu-id="274dc-141">Um valor *Null* para **nextHopType** em uma UDR pode indicar uma rota inválida.</span><span class="sxs-lookup"><span data-stu-id="274dc-141">A value of *Null* for **nextHopType** in a UDR may indicate an invalid route.</span></span> <span data-ttu-id="274dc-142">Por exemplo, se **nextHopType** for *VirtualAppliance* e a VM da solução de virtualização de rede não estiver em um estado provisionado/de execução.</span><span class="sxs-lookup"><span data-stu-id="274dc-142">For example, if **nextHopType** is *VirtualAppliance* and the network virtual appliance VM is not in a provisioned/running state.</span></span> <span data-ttu-id="274dc-143">Se **nextHopType** for *VPNGateway* e não houver nenhum gateway provisionado/em execução na VNet fornecida, a rota poderá se tornar inválida.</span><span class="sxs-lookup"><span data-stu-id="274dc-143">If **nextHopType** is *VPNGateway* and there is no gateway provisioned/running in the given VNet, the route may become invalid.</span></span>
   * <span data-ttu-id="274dc-144">**NextHopIpAddress**: especifica o endereço IP do próximo salto da rota em vigor.</span><span class="sxs-lookup"><span data-stu-id="274dc-144">**NextHopIpAddress**: Specifies the IP address of the next hop of the effective route.</span></span>
   
   <span data-ttu-id="274dc-145">O comando a seguir retorna as rotas de uma maneira mais fácil para ver a tabela:</span><span class="sxs-lookup"><span data-stu-id="274dc-145">The following command returns the routes in an easier to view table:</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1 | Format-Table
   
   <span data-ttu-id="274dc-146">A seguinte saída é parte da saída recebida para o cenário descrito anteriormente:</span><span class="sxs-lookup"><span data-stu-id="274dc-146">The following output is some of the output received for the scenario described previously:</span></span>
   
       Name State AddressPrefix NextHopType NextHopIpAddress
       ---- ----- ------------- ----------- ----------------
       Active {10.9.0.0/16} VnetLocal {}
       Active {0.0.0.0/0} Internet {}
3. <span data-ttu-id="274dc-147">Não há rota listada para a VNet *WestUS-VNet3* (prefixo 10.10.0.0/16)** da *WestUS-VNet1* (prefixo 10.9.0.0/16) na saída da etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="274dc-147">There is no route listed to the *WestUS-VNet3* VNet (Prefix 10.10.0.0/16)** from *WestUS-VNet1* (Prefix 10.9.0.0/16) in the output from the previous step.</span></span> <span data-ttu-id="274dc-148">Conforme mostrado na imagem a seguir, o link de emparelhamento da VNet com a VNet *WestUS-VNet3* está no estado *Desconectado*.</span><span class="sxs-lookup"><span data-stu-id="274dc-148">As shown in the following picture, the VNet peering link with the *WestUS-VNet3* VNet is in the *Disconnected* state.</span></span>
   
    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)
   
    <span data-ttu-id="274dc-149">O link de bi-direcional para o emparelhamento está dividido, o que explica por que a VM1 não pôde se conectar à VM3 na VNet *WestUS-VNet3* .</span><span class="sxs-lookup"><span data-stu-id="274dc-149">The bi-directional link for the peering is broken, which explains why VM1 could not connect to VM3 in the *WestUS-VNet3* VNet.</span></span> <span data-ttu-id="274dc-150">Configure um link de emparelhamento de VNet bidirecional novamente para as VNets *WestUS-VNet1* e *WestUS-VNet3*.</span><span class="sxs-lookup"><span data-stu-id="274dc-150">Setup a bi-directional VNet peering link again for *WestUS-VNet1* and *WestUS-VNet3* VNets.</span></span> <span data-ttu-id="274dc-151">A saída retornada após o link de emparelhamento da VNet é estabelecida corretamente a seguir:</span><span class="sxs-lookup"><span data-stu-id="274dc-151">The output returned after the VNet peering link is correctly established follows:</span></span>
   
        Name State AddressPrefix NextHopType NextHopIpAddress
        ---- ----- ------------- ----------- ----------------
        Active {10.9.0.0/16} VnetLocal {}
        Active {10.10.0.0/16} VNetPeering {}
        Active {0.0.0.0/0} Internet {}
   
    <span data-ttu-id="274dc-152">Depois de determinar o problema, você pode adicionar, remover ou alterar as rotas e tabelas de rotas.</span><span class="sxs-lookup"><span data-stu-id="274dc-152">Once you determine the issue, you can add, remove, or change routes and route tables.</span></span> <span data-ttu-id="274dc-153">Digite o comando a seguir para ver uma lista dos comandos usados para fazer isso:</span><span class="sxs-lookup"><span data-stu-id="274dc-153">Type the following command to see a list of the commands used to do so:</span></span>
   
        Get-Help *-AzureRmRouteConfig

## <a name="considerations"></a><span data-ttu-id="274dc-154">Considerações</span><span class="sxs-lookup"><span data-stu-id="274dc-154">Considerations</span></span>
<span data-ttu-id="274dc-155">Algumas coisas para ter em mente ao examinar a lista de rotas retornadas:</span><span class="sxs-lookup"><span data-stu-id="274dc-155">A few things to keep in mind when reviewing the list of routes returned:</span></span>

* <span data-ttu-id="274dc-156">O roteamento é baseado no LPM (Correspondência de Prefixo Mais Longo) entre UDRs, rotas BGP e do sistema.</span><span class="sxs-lookup"><span data-stu-id="274dc-156">Routing is based on Longest Prefix Match (LPM) among UDRs, BGP and system routes.</span></span> <span data-ttu-id="274dc-157">Se houver mais de uma rota com a mesma correspondência LPM, então uma rota será selecionada com base em sua origem na seguinte ordem:</span><span class="sxs-lookup"><span data-stu-id="274dc-157">If there is more than one route with the same LPM match, then a route is selected based on its origin in the following order:</span></span>
  
  * <span data-ttu-id="274dc-158">Rota definida pelo usuário</span><span class="sxs-lookup"><span data-stu-id="274dc-158">User-defined route</span></span>
  * <span data-ttu-id="274dc-159">Rota BGP</span><span class="sxs-lookup"><span data-stu-id="274dc-159">BGP route</span></span>
  * <span data-ttu-id="274dc-160">Rota do sistema (padrão)</span><span class="sxs-lookup"><span data-stu-id="274dc-160">System (Default) route</span></span>
    
    <span data-ttu-id="274dc-161">Com rotas em vigor, você só pode ver as rotas em vigor com correspondência LPM baseada em todas as rotas disponíveis.</span><span class="sxs-lookup"><span data-stu-id="274dc-161">With effective routes, you can only see effective routes that are LPM match based on all the availble routes.</span></span> <span data-ttu-id="274dc-162">Ao mostrar como as rotas são realmente avaliadas para uma determinada NIC, fica muito mais fácil solucionar problemas de rotas específicas que podem afetar a conectividade para/de sua VM.</span><span class="sxs-lookup"><span data-stu-id="274dc-162">By showing how the routes are actually evaluated for a given NIC, this makes it a lot easier to troubleshoot specific routes that may be impacting connectivity to/from your VM.</span></span>
* <span data-ttu-id="274dc-163">Se você tiver UDRs e estiver enviando o tráfego para uma NVA (solução de virtualização de rede) com *VirtualAppliance* como **nextHopType**, verifique se o encaminhamento de IP está habilitado na NVA que está recebendo o tráfego ou se os pacotes foram removidos.</span><span class="sxs-lookup"><span data-stu-id="274dc-163">If you have UDRs and are sending traffic to a network virtual appliance (NVA), with *VirtualAppliance* as **nextHopType**, ensure that IP forwarding is enabled on the NVA receiving the traffic or packets are dropped.</span></span> 
* <span data-ttu-id="274dc-164">Se túnel forçado estiver habilitado, todo o tráfego de Internet de saída será roteado para o local.</span><span class="sxs-lookup"><span data-stu-id="274dc-164">If Forced tunneling is enabled, all outbound Internet traffic will be routed to on-premises.</span></span> <span data-ttu-id="274dc-165">O RDP/SSH da Internet para sua VM pode não funcionar com essa configuração, dependendo de como o local trata esse tráfego.</span><span class="sxs-lookup"><span data-stu-id="274dc-165">RDP/SSH from Internet to your VM may not work with this setting, depending on how the on-premises handles this traffic.</span></span> 
  <span data-ttu-id="274dc-166">O túnel forçado pode ser habilitado:</span><span class="sxs-lookup"><span data-stu-id="274dc-166">Forced-tunneling can be enabled:</span></span>
  * <span data-ttu-id="274dc-167">Se você estiver usando a VPN site a site, definindo uma UDR (rota definida pelo usuário) com nextHopType como Gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="274dc-167">If using site-to-site VPN, by setting a user-defined route (UDR) with nextHopType as VPN Gateway</span></span>
  * <span data-ttu-id="274dc-168">Se uma rota padrão é anunciada por meio do BGP</span><span class="sxs-lookup"><span data-stu-id="274dc-168">If a default route is advertised over BGP</span></span>
* <span data-ttu-id="274dc-169">Para que o tráfego do emparelhamento de VNet funcione corretamente, deve haver uma rota do sistema com **nextHopType** *VNetPeering* para o intervalo de prefixo da VNet emparelhada.</span><span class="sxs-lookup"><span data-stu-id="274dc-169">For VNet peering traffic to work correctly, a system route with **nextHopType** *VNetPeering* must exist for the peered VNet’s prefix range.</span></span> <span data-ttu-id="274dc-170">Se tal rota não existir e o link de emparelhamento da VNet parecer correto:</span><span class="sxs-lookup"><span data-stu-id="274dc-170">If such a route doesn’t exist and the VNet peering link looks OK:</span></span>
  * <span data-ttu-id="274dc-171">Aguarde alguns segundos e tente novamente se for um link de emparelhamento recém-estabelecido.</span><span class="sxs-lookup"><span data-stu-id="274dc-171">Wait a few seconds and retry if it's a newly established peering link.</span></span> <span data-ttu-id="274dc-172">Ela ocasionalmente demora mais para propagar rotas para todos os adaptadores de rede em uma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="274dc-172">It occasionally takes longer to propagate routes to all the network interfaces in a subnet.</span></span>
  * <span data-ttu-id="274dc-173">As regras do NSG (grupo de segurança de rede) podem afetar os fluxos de tráfego.</span><span class="sxs-lookup"><span data-stu-id="274dc-173">Network Security Group (NSG) rules may be impacting the traffic flows.</span></span> <span data-ttu-id="274dc-174">Para obter mais informações, consulte o artigo [Solucionar problemas dos grupos de segurança de rede](virtual-network-nsg-troubleshoot-powershell.md) .</span><span class="sxs-lookup"><span data-stu-id="274dc-174">For more information, see the [Troubleshoot Network Security Groups](virtual-network-nsg-troubleshoot-powershell.md) article.</span></span>

