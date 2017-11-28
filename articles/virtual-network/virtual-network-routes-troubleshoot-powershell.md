---
title: rotas aaaTroubleshoot - PowerShell | Microsoft Docs
description: "Saiba como tootroubleshoot roteia no modelo de implantação do Azure Resource Manager hello usando o PowerShell do Azure."
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
ms.openlocfilehash: 7a07806df5c1d0caee921187e6ad29f6755ab535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-routes-using-azure-powershell"></a><span data-ttu-id="bdf0b-103">Solucionar problemas de rotas usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="bdf0b-103">Troubleshoot routes using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bdf0b-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bdf0b-104">Azure Portal</span></span>](virtual-network-routes-troubleshoot-portal.md)
> * [<span data-ttu-id="bdf0b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bdf0b-105">PowerShell</span></span>](virtual-network-routes-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="bdf0b-106">Se você estiver enfrentando tooor de problemas de conectividade de rede de sua máquina Virtual (VM) do Azure, rotas podem estar afetando os fluxos de tráfego VM.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-106">If you are experiencing network connectivity issues tooor from your Azure Virtual Machine (VM), routes may be impacting your VM traffic flows.</span></span> <span data-ttu-id="bdf0b-107">Este artigo fornece uma visão geral dos recursos de diagnóstico para rotas toohelp solucionar outros problemas.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-107">This article provides an overview of diagnostics capabilities for routes toohelp troubleshoot further.</span></span>

<span data-ttu-id="bdf0b-108">As tabelas de rotas são associadas a sub-redes e estão em vigor em todas as NICs (interfaces de rede) nessa sub-rede.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-108">Route tables are associated with subnets and are effective on all network interfaces (NIC) in that subnet.</span></span> <span data-ttu-id="bdf0b-109">Olá seguintes tipos de rotas pode ser aplicado tooeach interface de rede:</span><span class="sxs-lookup"><span data-stu-id="bdf0b-109">hello following types of routes can be applied tooeach network interface:</span></span>

* <span data-ttu-id="bdf0b-110">**Rotas de sistema:** por padrão, cada sub-rede criada em uma VNet (rede virtual) do Azure tem tabelas de rotas de sistema que possibilitam o tráfego da VNet, o tráfego local por meio de gateways de VPN e o tráfego da Internet.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-110">**System routes:** By default, every subnet created in an Azure Virtual Network (VNet) has system route tables that allow local VNet traffic, on-premises traffic via VPN gateways, and Internet traffic.</span></span> <span data-ttu-id="bdf0b-111">Também existem rotas de sistema para VNets emparelhadas.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-111">System routes also exist for peered VNets.</span></span>
* <span data-ttu-id="bdf0b-112">**Rotas de BGP:** propagadas toonetwork interfaces por meio de rota expressa ou conexões VPN site a site.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-112">**BGP routes:** Propagated toonetwork interfaces through ExpressRoute or site-to-site VPN connections.</span></span> <span data-ttu-id="bdf0b-113">Saiba mais sobre o roteamento de BGP lendo Olá [BGP com gateways de VPN](../vpn-gateway/vpn-gateway-bgp-overview.md) e [visão geral do ExpressRoute](../expressroute/expressroute-introduction.md) artigos.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-113">Learn more about BGP routing by reading hello [BGP with VPN gateways](../vpn-gateway/vpn-gateway-bgp-overview.md) and [ExpressRoute overview](../expressroute/expressroute-introduction.md) articles.</span></span>
* <span data-ttu-id="bdf0b-114">**Rotas definidas pelo usuário (UDR):** se você estiver usando dispositivos de rede virtual ou são forçados túnel de tráfego tooan no local de rede por meio de uma VPN site a site, você pode ter definido pelo usuário rotas (UDRs) associadas com sua tabela de rotas de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-114">**User-defined routes (UDR):** If you are using network virtual appliances or are forced-tunneling traffic tooan on-premises network via a site-to-site VPN, you may have user-defined routes (UDRs) associated with your subnet route table.</span></span> <span data-ttu-id="bdf0b-115">Se você não estiver familiarizado com UDRs, leia Olá [rotas definidas pelo usuário](virtual-networks-udr-overview.md#user-defined-routes) artigo.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-115">If you're not familiar with UDRs, read hello [user-defined routes](virtual-networks-udr-overview.md#user-defined-routes) article.</span></span>

<span data-ttu-id="bdf0b-116">Com hello várias rotas que podem ser aplicadas tooa interface de rede, pode ser difícil toodetermine quais rotas agregação entrarão em vigor.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-116">With hello various routes that can be applied tooa network interface, it can be difficult toodetermine which aggregate routes are effective.</span></span> <span data-ttu-id="bdf0b-117">toohelp solucionar problemas de conectividade de rede VM, você pode exibir todas as rotas efetivas de saudação para uma interface de rede no modelo de implantação do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-117">toohelp troubleshoot VM network connectivity, you can view all hello effective routes for a network interface in hello Azure Resource Manager deployment model.</span></span>

## <a name="using-effective-routes-tootroubleshoot-vm-traffic-flow"></a><span data-ttu-id="bdf0b-118">Usando o fluxo de tráfego VM rotas efetivas tootroubleshoot</span><span class="sxs-lookup"><span data-stu-id="bdf0b-118">Using Effective Routes tootroubleshoot VM traffic flow</span></span>
<span data-ttu-id="bdf0b-119">Este artigo usa Olá cenário a seguir como um tooillustrate de exemplo como tootroubleshoot Olá efetiva roteia para uma interface de rede:</span><span class="sxs-lookup"><span data-stu-id="bdf0b-119">This article uses hello following scenario as an example tooillustrate how tootroubleshoot hello effective routes for a network interface:</span></span>

<span data-ttu-id="bdf0b-120">Uma VM (*VM1*) conectados a redes de toohello (*VNet1*, prefixo: 10.9.0.0/16) falha tooconnect tooa VM(VM3) em uma rede virtual peered recentemente (*VNet3*, prefixo 10.10.0.0/16).</span><span class="sxs-lookup"><span data-stu-id="bdf0b-120">A VM (*VM1*) connected toohello VNet (*VNet1*, prefix: 10.9.0.0/16) fails tooconnect tooa VM(VM3) in a newly peered VNet (*VNet3*, prefix 10.10.0.0/16).</span></span> <span data-ttu-id="bdf0b-121">Não há nenhum UDRs ou BGP roteia toohello interface conectada da rede aplicado tooVM1-NIC1 VM, apenas as rotas de sistema são aplicadas.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-121">There are no UDRs or BGP routes applied tooVM1-NIC1 network interface connected toohello VM, only system routes are applied.</span></span>

<span data-ttu-id="bdf0b-122">Este artigo explica como Olá toodetermine causa da falha de conexão hello, usando o recurso de rotas efetiva no modelo de implantação do gerenciamento de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-122">This article explains how toodetermine hello cause of hello connection failure, using effective routes capability in Azure Resource Management deployment model.</span></span>
<span data-ttu-id="bdf0b-123">Enquanto o exemplo hello usa apenas as rotas de sistema, Olá mesmas etapas pode ser usada toodetermine falhas de conexão de entrada e saída em qualquer tipo de rota.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-123">While hello example uses only system routes, hello same steps can be used toodetermine inbound and outbound connection failures over any route type.</span></span>

> [!NOTE]
> <span data-ttu-id="bdf0b-124">Se sua VM tem mais de uma NIC anexada, verifique rotas efetivas para cada Olá tooand de problemas de conectividade NICs toodiagnose rede de uma VM.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-124">If your VM has more than one NIC attached, check effective routes for each of hello NICs toodiagnose network connectivity issues tooand from a VM.</span></span>
> 
> 

### <a name="view-effective-routes-for-a-virtual-machine"></a><span data-ttu-id="bdf0b-125">Exibir rotas em vigor para uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="bdf0b-125">View effective routes for a virtual machine</span></span>
<span data-ttu-id="bdf0b-126">toosee Olá agregação rotas que são aplicada tooa VM, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="bdf0b-126">toosee hello aggregate routes that are applied tooa VM, complete hello following steps:</span></span>

### <a name="view-effective-routes-for-a-network-interface"></a><span data-ttu-id="bdf0b-127">Exibir rotas em vigor para um adaptador de rede</span><span class="sxs-lookup"><span data-stu-id="bdf0b-127">View effective routes for a network interface</span></span>
<span data-ttu-id="bdf0b-128">toosee Olá agregação rotas que são aplicadas tooa interface de rede, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="bdf0b-128">toosee hello aggregate routes that are applied tooa network interface, complete hello following steps:</span></span>

1. <span data-ttu-id="bdf0b-129">Inicie um tooAzure de logon e de sessão do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-129">Start an Azure PowerShell session and login tooAzure.</span></span> <span data-ttu-id="bdf0b-130">Se você não estiver familiarizado com o PowerShell do Azure, leia Olá [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) artigo.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-130">If you’re not familiar with Azure PowerShell, read hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="bdf0b-131">comando a seguir Hello retorna todos os interface de rede de tooa rotas aplicadas denominado *VM1 NIC1* no grupo de recursos de saudação *RG1*.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-131">hello following command returns all routes applied tooa network interface named *VM1-NIC1* in hello resource group *RG1*.</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > <span data-ttu-id="bdf0b-132">Se você não souber o nome de saudação de uma interface de rede, digite Olá nomes de saudação do comando tooretrieve de todas as interfaces de rede em um recurso group.* a seguir</span><span class="sxs-lookup"><span data-stu-id="bdf0b-132">If you don’t know hello name of a network interface, type hello following command tooretrieve hello names of all network interfaces in a resource group.*</span></span>
   > 
   > 
   
       Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name
   
   <span data-ttu-id="bdf0b-133">Olá saída a seguir procura saída toohello semelhante cada saudação de sub-rede rota aplicada toohello A que NIC está conectada:</span><span class="sxs-lookup"><span data-stu-id="bdf0b-133">hello following output looks similar toohello output for each route applied toohello subnet hello NIC is connected to:</span></span>
   
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
   
   <span data-ttu-id="bdf0b-134">Observe o seguinte Olá na saída de hello:</span><span class="sxs-lookup"><span data-stu-id="bdf0b-134">Notice hello following in hello output:</span></span>
   
   * <span data-ttu-id="bdf0b-135">**Nome**: nome da rota efetiva Olá pode ser vazio, a menos que explicitamente especificado, para rotas definidas pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-135">**Name**: Name of hello effective route may be empty, unless explicitly specified, for user-defined routes.</span></span> 
   * <span data-ttu-id="bdf0b-136">**Estado**: indica o estado da rota efetiva hello.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-136">**State**: Indicates state of hello effective route.</span></span> <span data-ttu-id="bdf0b-137">Os valores possíveis são “Active” ou “Invalid”</span><span class="sxs-lookup"><span data-stu-id="bdf0b-137">Possible values are "Active" or "Invalid"</span></span>
   * <span data-ttu-id="bdf0b-138">**AddressPrefixes**: Especifica o prefixo do endereço de saudação da rota efetiva Olá na notação CIDR.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-138">**AddressPrefixes**: Specifies hello address prefix of hello effective route in CIDR notation.</span></span> 
   * <span data-ttu-id="bdf0b-139">**nextHopType**: indica o próximo salto Olá Olá considerando a rota.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-139">**nextHopType**: Indicates hello next hop for hello given route.</span></span> <span data-ttu-id="bdf0b-140">Os valores possíveis são *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering* ou *Null*.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-140">Possible values are *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, or *Null*.</span></span> <span data-ttu-id="bdf0b-141">Um valor *Null* para **nextHopType** em uma UDR pode indicar uma rota inválida.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-141">A value of *Null* for **nextHopType** in a UDR may indicate an invalid route.</span></span> <span data-ttu-id="bdf0b-142">Por exemplo, se **nextHopType** é *VirtualAppliance* e solução de virtualização de rede do hello VM não está em um estado de execução/provisionado.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-142">For example, if **nextHopType** is *VirtualAppliance* and hello network virtual appliance VM is not in a provisioned/running state.</span></span> <span data-ttu-id="bdf0b-143">Se **nextHopType** é *o VPNGateway* e há um gateway provisionado/em execução no hello VNet fornecido, rota Olá pode se tornar inválida.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-143">If **nextHopType** is *VPNGateway* and there is no gateway provisioned/running in hello given VNet, hello route may become invalid.</span></span>
   * <span data-ttu-id="bdf0b-144">**NextHopIpAddress**: Especifica o endereço IP de saudação do próximo salto de saudação da rota efetiva hello.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-144">**NextHopIpAddress**: Specifies hello IP address of hello next hop of hello effective route.</span></span>
   
   <span data-ttu-id="bdf0b-145">Olá comando a seguir retorna as rotas de saudação em uma tabela tooview mais fácil:</span><span class="sxs-lookup"><span data-stu-id="bdf0b-145">hello following command returns hello routes in an easier tooview table:</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1 | Format-Table
   
   <span data-ttu-id="bdf0b-146">Olá saída a seguir está algumas das Olá saída recebida para o cenário de saudação descrito anteriormente:</span><span class="sxs-lookup"><span data-stu-id="bdf0b-146">hello following output is some of hello output received for hello scenario described previously:</span></span>
   
       Name State AddressPrefix NextHopType NextHopIpAddress
       ---- ----- ------------- ----------- ----------------
       Active {10.9.0.0/16} VnetLocal {}
       Active {0.0.0.0/0} Internet {}
3. <span data-ttu-id="bdf0b-147">Não há nenhuma rota listada toohello *WestUS VNet3* VNet (prefixo 10.10.0.0/16)** de *WestUS VNet1* (prefixo 10.9.0.0/16) na saída de saudação da etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-147">There is no route listed toohello *WestUS-VNet3* VNet (Prefix 10.10.0.0/16)** from *WestUS-VNet1* (Prefix 10.9.0.0/16) in hello output from hello previous step.</span></span> <span data-ttu-id="bdf0b-148">Conforme mostrado na figura abaixo de saudação, Olá link de emparelhamento VNet com hello *WestUS VNet3* rede virtual está em Olá *Disconnected* estado.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-148">As shown in hello following picture, hello VNet peering link with hello *WestUS-VNet3* VNet is in hello *Disconnected* state.</span></span>
   
    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)
   
    <span data-ttu-id="bdf0b-149">link de bi-direcional Olá Olá emparelhamento é interrompida, que explica por que VM1 não pôde se conectar tooVM3 em Olá *WestUS VNet3* VNet.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-149">hello bi-directional link for hello peering is broken, which explains why VM1 could not connect tooVM3 in hello *WestUS-VNet3* VNet.</span></span> <span data-ttu-id="bdf0b-150">Configure um link de emparelhamento de VNet bidirecional novamente para as VNets *WestUS-VNet1* e *WestUS-VNet3*.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-150">Setup a bi-directional VNet peering link again for *WestUS-VNet1* and *WestUS-VNet3* VNets.</span></span> <span data-ttu-id="bdf0b-151">saída de Hello retornada depois que o link de emparelhamento de rede virtual Olá é estabelecida corretamente a seguinte:</span><span class="sxs-lookup"><span data-stu-id="bdf0b-151">hello output returned after hello VNet peering link is correctly established follows:</span></span>
   
        Name State AddressPrefix NextHopType NextHopIpAddress
        ---- ----- ------------- ----------- ----------------
        Active {10.9.0.0/16} VnetLocal {}
        Active {10.10.0.0/16} VNetPeering {}
        Active {0.0.0.0/0} Internet {}
   
    <span data-ttu-id="bdf0b-152">Depois de determinar o problema hello, você pode adicionar, remover, ou alterar as rotas e tabelas de rota.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-152">Once you determine hello issue, you can add, remove, or change routes and route tables.</span></span> <span data-ttu-id="bdf0b-153">Digite hello após o comando toosee uma lista de saudação comandos usados toodo assim:</span><span class="sxs-lookup"><span data-stu-id="bdf0b-153">Type hello following command toosee a list of hello commands used toodo so:</span></span>
   
        Get-Help *-AzureRmRouteConfig

## <a name="considerations"></a><span data-ttu-id="bdf0b-154">Considerações</span><span class="sxs-lookup"><span data-stu-id="bdf0b-154">Considerations</span></span>
<span data-ttu-id="bdf0b-155">Alguns tookeep coisas em mente ao examinar a lista de saudação de rotas retornado:</span><span class="sxs-lookup"><span data-stu-id="bdf0b-155">A few things tookeep in mind when reviewing hello list of routes returned:</span></span>

* <span data-ttu-id="bdf0b-156">O roteamento é baseado no LPM (Correspondência de Prefixo Mais Longo) entre UDRs, rotas BGP e do sistema.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-156">Routing is based on Longest Prefix Match (LPM) among UDRs, BGP and system routes.</span></span> <span data-ttu-id="bdf0b-157">Se houver mais de uma rota com hello mesmo LPM corresponder, então uma rota é selecionada com base em sua origem no hello ordem a seguir:</span><span class="sxs-lookup"><span data-stu-id="bdf0b-157">If there is more than one route with hello same LPM match, then a route is selected based on its origin in hello following order:</span></span>
  
  * <span data-ttu-id="bdf0b-158">Rota definida pelo usuário</span><span class="sxs-lookup"><span data-stu-id="bdf0b-158">User-defined route</span></span>
  * <span data-ttu-id="bdf0b-159">Rota BGP</span><span class="sxs-lookup"><span data-stu-id="bdf0b-159">BGP route</span></span>
  * <span data-ttu-id="bdf0b-160">Rota do sistema (padrão)</span><span class="sxs-lookup"><span data-stu-id="bdf0b-160">System (Default) route</span></span>
    
    <span data-ttu-id="bdf0b-161">Com rotas efetivas, você pode ver apenas as rotas efetivas que são LPM correspondência com base em todas as rotas do hello disponível.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-161">With effective routes, you can only see effective routes that are LPM match based on all hello availble routes.</span></span> <span data-ttu-id="bdf0b-162">Mostrando como rotas hello, na verdade, são avaliadas para uma NIC determinada, isso torna muito mais fácil rotas de tootroubleshoot específicas que podem afetar a conectividade de sua VM.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-162">By showing how hello routes are actually evaluated for a given NIC, this makes it a lot easier tootroubleshoot specific routes that may be impacting connectivity to/from your VM.</span></span>
* <span data-ttu-id="bdf0b-163">Se você tiver UDRs e está enviando o dispositivo virtual de rede tooa do tráfego NVA (), com *VirtualAppliance* como **nextHopType**, verifique se o encaminhamento de IP está habilitado no tráfego de recebimento Olá Olá NVA ou os pacotes são descartados.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-163">If you have UDRs and are sending traffic tooa network virtual appliance (NVA), with *VirtualAppliance* as **nextHopType**, ensure that IP forwarding is enabled on hello NVA receiving hello traffic or packets are dropped.</span></span> 
* <span data-ttu-id="bdf0b-164">Se o túnel forçado estiver habilitado, todo o tráfego de saída do Internet será roteado tooon local.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-164">If Forced tunneling is enabled, all outbound Internet traffic will be routed tooon-premises.</span></span> <span data-ttu-id="bdf0b-165">RDP/SSH de Internet tooyour que VM pode não funcionar com essa configuração, dependendo de como Olá local trata esse tráfego.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-165">RDP/SSH from Internet tooyour VM may not work with this setting, depending on how hello on-premises handles this traffic.</span></span> 
  <span data-ttu-id="bdf0b-166">O túnel forçado pode ser habilitado:</span><span class="sxs-lookup"><span data-stu-id="bdf0b-166">Forced-tunneling can be enabled:</span></span>
  * <span data-ttu-id="bdf0b-167">Se você estiver usando a VPN site a site, definindo uma UDR (rota definida pelo usuário) com nextHopType como Gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="bdf0b-167">If using site-to-site VPN, by setting a user-defined route (UDR) with nextHopType as VPN Gateway</span></span>
  * <span data-ttu-id="bdf0b-168">Se uma rota padrão é anunciada por meio do BGP</span><span class="sxs-lookup"><span data-stu-id="bdf0b-168">If a default route is advertised over BGP</span></span>
* <span data-ttu-id="bdf0b-169">Para a rede virtual emparelhamento tráfego toowork corretamente, uma rota de sistema com **nextHopType** *VNetPeering* deve existir para Olá emparelhadas intervalo de prefixo da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-169">For VNet peering traffic toowork correctly, a system route with **nextHopType** *VNetPeering* must exist for hello peered VNet’s prefix range.</span></span> <span data-ttu-id="bdf0b-170">Se tal uma rota não existir e Olá emparelhamento VNet link é Okey:</span><span class="sxs-lookup"><span data-stu-id="bdf0b-170">If such a route doesn’t exist and hello VNet peering link looks OK:</span></span>
  * <span data-ttu-id="bdf0b-171">Aguarde alguns segundos e tente novamente se for um link de emparelhamento recém-estabelecido.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-171">Wait a few seconds and retry if it's a newly established peering link.</span></span> <span data-ttu-id="bdf0b-172">Ocasionalmente, leva mais rotas de toopropagate interfaces de rede Olá tooall em uma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-172">It occasionally takes longer toopropagate routes tooall hello network interfaces in a subnet.</span></span>
  * <span data-ttu-id="bdf0b-173">Regras de grupo de segurança de rede (NSG) podem estar afetando Olá fluxos de tráfego.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-173">Network Security Group (NSG) rules may be impacting hello traffic flows.</span></span> <span data-ttu-id="bdf0b-174">Para obter mais informações, consulte Olá [solucionar problemas de grupos de segurança de rede](virtual-network-nsg-troubleshoot-powershell.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="bdf0b-174">For more information, see hello [Troubleshoot Network Security Groups](virtual-network-nsg-troubleshoot-powershell.md) article.</span></span>

