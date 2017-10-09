---
title: "Configurar as conexões de VPN ExpressRoute e Site a Site que possam coexistir: clássico: Azure | Microsoft Docs"
description: "Este artigo orienta você pela configuração de uma conexão VPN Site a Site que pode coexistir para o modelo de implantação clássico hello e rota expressa."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: dcf1a5af-a289-466a-b812-0bfedbd2bda0
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: abb30fff55e8ec243f2920c5b2f70c43717755fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections-classic"></a><span data-ttu-id="ebd69-103">Configurar as conexões coexistentes do ExpressRoute e do Site a Site (clássico)</span><span class="sxs-lookup"><span data-stu-id="ebd69-103">Configure ExpressRoute and Site-to-Site coexisting connections (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ebd69-104">PowerShell – Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ebd69-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="ebd69-105">PowerShell - clássico</span><span class="sxs-lookup"><span data-stu-id="ebd69-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="ebd69-106">Tendo Olá capacidade tooconfigure VPN Site a Site e ExpressRoute tem várias vantagens.</span><span class="sxs-lookup"><span data-stu-id="ebd69-106">Having hello ability tooconfigure Site-to-Site VPN and ExpressRoute has several advantages.</span></span> <span data-ttu-id="ebd69-107">Você pode configurar VPN Site a Site como um caminho de failover seguro para ExressRoute ou usar VPNs Site a Site tooconnect toosites que não estão conectados por meio de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="ebd69-107">You can configure Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs tooconnect toosites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="ebd69-108">Abordaremos Olá etapas tooconfigure ambos os cenários neste artigo.</span><span class="sxs-lookup"><span data-stu-id="ebd69-108">We will cover hello steps tooconfigure both scenarios in this article.</span></span> <span data-ttu-id="ebd69-109">Este artigo se aplica o modelo de implantação clássico toohello.</span><span class="sxs-lookup"><span data-stu-id="ebd69-109">This article applies toohello classic deployment model.</span></span> <span data-ttu-id="ebd69-110">Essa configuração não está disponível no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="ebd69-110">This configuration is not available in hello portal.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="ebd69-111">**Sobre modelos de implantação do Azure**</span><span class="sxs-lookup"><span data-stu-id="ebd69-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="ebd69-112">Circuitos de rota expressa devem ser configurados previamente antes de seguir as instruções de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="ebd69-112">ExpressRoute circuits must be pre-configured before you follow hello instructions below.</span></span> <span data-ttu-id="ebd69-113">Certifique-se de que você seguiu Olá guias muito[criar um circuito ExpressRoute](expressroute-howto-circuit-classic.md) e [configurar o roteamento](expressroute-howto-routing-classic.md) antes de executar as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="ebd69-113">Make sure that you have followed hello guides too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and [configure routing](expressroute-howto-routing-classic.md) before you follow hello steps below.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="ebd69-114">Limites e limitações</span><span class="sxs-lookup"><span data-stu-id="ebd69-114">Limits and limitations</span></span>
* <span data-ttu-id="ebd69-115">**Não há suporte para o roteamento do tráfego.**</span><span class="sxs-lookup"><span data-stu-id="ebd69-115">**Transit routing is not supported.**</span></span> <span data-ttu-id="ebd69-116">Não é possível fazer o roteamento (por meio do Azure) entre sua rede local conectada via VPN Site a Site e sua rede local conectada via ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ebd69-116">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="ebd69-117">**Não há suporte para o Ponto a site.**</span><span class="sxs-lookup"><span data-stu-id="ebd69-117">**Point-to-site is not supported.**</span></span> <span data-ttu-id="ebd69-118">Não é possível habilitar toohello de conexões de VPN ponto a site mesmo VNet tooExpressRoute conectado.</span><span class="sxs-lookup"><span data-stu-id="ebd69-118">You can't enable point-to-site VPN connections toohello same VNet that is connected tooExpressRoute.</span></span> <span data-ttu-id="ebd69-119">VPN de ponto para site e ExpressRoute não podem coexistir para Olá mesmo VNet.</span><span class="sxs-lookup"><span data-stu-id="ebd69-119">Point-to-site VPN and ExpressRoute cannot coexist for hello same VNet.</span></span>
* <span data-ttu-id="ebd69-120">**Não é possível habilitar o túnel forçado no gateway VPN Site a Site hello.**</span><span class="sxs-lookup"><span data-stu-id="ebd69-120">**Forced tunneling cannot be enabled on hello Site-to-Site VPN gateway.**</span></span> <span data-ttu-id="ebd69-121">Você pode apenas "forçar" todos os direcionado à Internet tráfego tooyour Voltar na rede local através de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="ebd69-121">You can only "force" all Internet-bound traffic back tooyour on-premises network via ExpressRoute.</span></span>
* <span data-ttu-id="ebd69-122">**Não há suporte para o gateway SKU básico.**</span><span class="sxs-lookup"><span data-stu-id="ebd69-122">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="ebd69-123">Você deve usar um gateway de SKU não básica para ambos os Olá [gateway de rota expressa](expressroute-about-virtual-network-gateways.md) e hello [gateway VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="ebd69-123">You must use a non-Basic SKU gateway for both hello [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and hello [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="ebd69-124">**Há suporte para apenas um gateway de VPN baseado em rotas.**</span><span class="sxs-lookup"><span data-stu-id="ebd69-124">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="ebd69-125">Você deve usar uma rota baseada no [Gateway de VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="ebd69-125">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="ebd69-126">**O roteamento estático deve ser configurado para o gateway de VPN.**</span><span class="sxs-lookup"><span data-stu-id="ebd69-126">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="ebd69-127">Se sua rede local está conectada tooboth ExpressRoute e uma Site a Site VPN, você deve ter uma rota estática configurada em sua rede local tooroute Olá Site a Site VPN conexão toohello Internet pública.</span><span class="sxs-lookup"><span data-stu-id="ebd69-127">If your local network is connected tooboth ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network tooroute hello Site-to-Site VPN connection toohello public Internet.</span></span>
* <span data-ttu-id="ebd69-128">**O gateway de ExpressRoute deve ser configurado primeiro.**</span><span class="sxs-lookup"><span data-stu-id="ebd69-128">**ExpressRoute gateway must be configured first.**</span></span> <span data-ttu-id="ebd69-129">Você deve criar o gateway de rota expressa Olá primeiro antes de adicionar o gateway VPN Site a Site hello.</span><span class="sxs-lookup"><span data-stu-id="ebd69-129">You must create hello ExpressRoute gateway first before you add hello Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="ebd69-130">Designs de configuração</span><span class="sxs-lookup"><span data-stu-id="ebd69-130">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="ebd69-131">Configurar uma VPN site a site como um caminho de failover para o ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="ebd69-131">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="ebd69-132">Você pode configurar uma conexão VPN site a site como um backup para o ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ebd69-132">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="ebd69-133">Isso se aplica apenas toovirtual redes vinculado toohello caminho de emparelhamento particular do Azure.</span><span class="sxs-lookup"><span data-stu-id="ebd69-133">This applies only toovirtual networks linked toohello Azure private peering path.</span></span> <span data-ttu-id="ebd69-134">Não há uma solução de failover com base em VPN para serviços acessíveis por meio de emparelhamentos público do Azure e da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ebd69-134">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="ebd69-135">Olá circuito de rota expressa é sempre link principal hello.</span><span class="sxs-lookup"><span data-stu-id="ebd69-135">hello ExpressRoute circuit is always hello primary link.</span></span> <span data-ttu-id="ebd69-136">Dados fluirá pelo caminho VPN Site a Site Olá somente se Olá circuito ExpressRoute falhar.</span><span class="sxs-lookup"><span data-stu-id="ebd69-136">Data will flow through hello Site-to-Site VPN path only if hello ExpressRoute circuit fails.</span></span> 

> [!NOTE]
> <span data-ttu-id="ebd69-137">Enquanto circuito de rota expressa é preferível por VPN Site a Site quando ambas as rotas são Olá mesmo, o Azure usará hello mais longa correspondência toochoose Olá rota de prefixo para o destino do pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="ebd69-137">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are hello same, Azure will use hello longest prefix match toochoose hello route towards hello packet's destination.</span></span>
> 
> 

![Coexistência](media/expressroute-howto-coexist-classic/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a><span data-ttu-id="ebd69-139">Configurar um toosites tooconnect VPN Site a Site não está conectado por meio de rota expressa</span><span class="sxs-lookup"><span data-stu-id="ebd69-139">Configure a Site-to-Site VPN tooconnect toosites not connected through ExpressRoute</span></span>
<span data-ttu-id="ebd69-140">Você pode configurar sua rede onde alguns sites se conectam diretamente tooAzure por VPN Site a Site, e alguns sites se conectam por meio de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="ebd69-140">You can configure your network where some sites connect directly tooAzure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![Coexistência](media/expressroute-howto-coexist-classic/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="ebd69-142">Não é possível configurar uma rede virtual como um roteador de trânsito.</span><span class="sxs-lookup"><span data-stu-id="ebd69-142">You cannot a configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-hello-steps-toouse"></a><span data-ttu-id="ebd69-143">Selecionando Olá etapas toouse</span><span class="sxs-lookup"><span data-stu-id="ebd69-143">Selecting hello steps toouse</span></span>
<span data-ttu-id="ebd69-144">Há dois conjuntos diferentes de toochoose procedimentos de em conexões de tooconfigure de ordem podem coexistir.</span><span class="sxs-lookup"><span data-stu-id="ebd69-144">There are two different sets of procedures toochoose from in order tooconfigure connections that can coexist.</span></span> <span data-ttu-id="ebd69-145">procedimento de configuração de saudação selecionados por você dependerá se você tiver uma rede virtual existente que você deseja tooconnect para, ou você deseja toocreate uma nova rede virtual.</span><span class="sxs-lookup"><span data-stu-id="ebd69-145">hello configuration procedure that you select will depend on whether you have an existing virtual network that you want tooconnect to, or you want toocreate a new virtual network.</span></span>

* <span data-ttu-id="ebd69-146">Não tem uma rede virtual e precisa toocreate um.</span><span class="sxs-lookup"><span data-stu-id="ebd69-146">I don't have a VNet and need toocreate one.</span></span>
  
    <span data-ttu-id="ebd69-147">Se você ainda não tiver uma rede virtual, este procedimento irá orientá-lo por meio de criar uma nova rede virtual usando o modelo de implantação clássico hello e criação de novas conexões de VPN Site a Site e rota expressa.</span><span class="sxs-lookup"><span data-stu-id="ebd69-147">If you don’t already have a virtual network, this procedure will walk you through creating a new virtual network using hello classic deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="ebd69-148">tooconfigure, Olá etapas a seguir na seção de artigo Olá [toocreate uma nova rede virtual e conexões coexistentes](#new).</span><span class="sxs-lookup"><span data-stu-id="ebd69-148">tooconfigure, follow hello steps in hello article section [toocreate a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="ebd69-149">Eu já tenho uma VNet do modelo de implantação clássico</span><span class="sxs-lookup"><span data-stu-id="ebd69-149">I already have a classic deployment model VNet.</span></span>
  
    <span data-ttu-id="ebd69-150">Talvez você já tenha uma rede virtual implementada com uma conexão de VPN Site a Site ou uma conexão de ExpressRoute existente.</span><span class="sxs-lookup"><span data-stu-id="ebd69-150">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="ebd69-151">Olá seção artigo [tooconfigure coexsiting conexões para uma rede virtual já existente](#add) irá orientá-lo por meio de excluir gateway hello e, em seguida, criar novas conexões VPN Site a Site e rota expressa.</span><span class="sxs-lookup"><span data-stu-id="ebd69-151">hello article section [tooconfigure coexsiting connections for an already existing VNet](#add) will walk you through deleting hello gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="ebd69-152">Observe que, ao criar novas conexões de hello, Olá etapas devem ser concluídas em uma ordem muito específica.</span><span class="sxs-lookup"><span data-stu-id="ebd69-152">Note that when creating hello new connections, hello steps must be completed in a very specific order.</span></span> <span data-ttu-id="ebd69-153">Não use instruções Olá toocreate outros artigos seus gateways e conexões.</span><span class="sxs-lookup"><span data-stu-id="ebd69-153">Don't use hello instructions in other articles toocreate your gateways and connections.</span></span>
  
    <span data-ttu-id="ebd69-154">Neste procedimento, criação de conexões que podem coexistir será exigem você toodelete seu gateway e, em seguida, configure novos gateways.</span><span class="sxs-lookup"><span data-stu-id="ebd69-154">In this procedure, creating connections that can coexist will require you toodelete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="ebd69-155">Isso significa que você terá tempo de inatividade para as conexões entre locais enquanto você excluir e recria o gateway e conexões, mas você não precisará toomigrate qualquer uma das sua VMs ou serviços tooa nova rede virtual.</span><span class="sxs-lookup"><span data-stu-id="ebd69-155">This means you will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need toomigrate any of your VMs or services tooa new virtual network.</span></span> <span data-ttu-id="ebd69-156">Suas máquinas virtuais e serviços ainda serão toocommunicate capaz de saída por meio do balanceador de carga Olá enquanto você configurar seu gateway se eles estiverem toodo configurado assim.</span><span class="sxs-lookup"><span data-stu-id="ebd69-156">Your VMs and services will still be able toocommunicate out through hello load balancer while you configure your gateway if they are configured toodo so.</span></span>

## <span data-ttu-id="ebd69-157"><a name="new"></a>conexões coexistentes e toocreate uma nova rede virtual</span><span class="sxs-lookup"><span data-stu-id="ebd69-157"><a name="new"></a>toocreate a new virtual network and coexisting connections</span></span>
<span data-ttu-id="ebd69-158">Este procedimento orientará você na criação de uma Rede Virtual, bem como na criação das conexões site a site e de ExpressRoute que coexistirão.</span><span class="sxs-lookup"><span data-stu-id="ebd69-158">This procedure will walk you through creating a VNet and create Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="ebd69-159">Você precisará tooinstall Olá última versão do hello cmdlets do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="ebd69-159">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="ebd69-160">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações sobre como instalar os cmdlets do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="ebd69-160">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span> <span data-ttu-id="ebd69-161">Observe que Olá cmdlets que você usará para essa configuração pode ser um pouco diferente do que você talvez esteja familiarizado com.</span><span class="sxs-lookup"><span data-stu-id="ebd69-161">Note that hello cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="ebd69-162">Se toouse Olá cmdlets ser especificado nestas instruções.</span><span class="sxs-lookup"><span data-stu-id="ebd69-162">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="ebd69-163">Crie um esquema para a sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="ebd69-163">Create a schema for your virtual network.</span></span> <span data-ttu-id="ebd69-164">Para obter mais informações sobre o esquema de configuração hello, consulte [esquema de configuração de rede Virtual do Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="ebd69-164">For more information about hello configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   
    <span data-ttu-id="ebd69-165">Quando você criar seu esquema, certifique-se de que usar o hello valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="ebd69-165">When you create your schema, make sure you use hello following values:</span></span>
   
   * <span data-ttu-id="ebd69-166">sub-rede de gateway de saudação para rede virtual Olá deve ser /27 ou um prefixo mais curto (como /26 ou /25).</span><span class="sxs-lookup"><span data-stu-id="ebd69-166">hello gateway subnet for hello virtual network must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   * <span data-ttu-id="ebd69-167">tipo de conexão de gateway de saudação é "dedicado".</span><span class="sxs-lookup"><span data-stu-id="ebd69-167">hello gateway connection type is "Dedicated".</span></span>
     
             <VirtualNetworkSite name="MyAzureVNET" Location="Central US">
               <AddressSpace>
                 <AddressPrefix>10.17.159.192/26</AddressPrefix>
               </AddressSpace>
               <Subnets>
                 <Subnet name="Subnet-1">
                   <AddressPrefix>10.17.159.192/27</AddressPrefix>
                 </Subnet>
                 <Subnet name="GatewaySubnet">
                   <AddressPrefix>10.17.159.224/27</AddressPrefix>
                 </Subnet>
               </Subnets>
               <Gateway>
                 <ConnectionsToLocalNetwork>
                   <LocalNetworkSiteRef name="MyLocalNetwork">
                     <Connection type="Dedicated" />
                   </LocalNetworkSiteRef>
                 </ConnectionsToLocalNetwork>
               </Gateway>
             </VirtualNetworkSite>
3. <span data-ttu-id="ebd69-168">Depois de criar e configurar o arquivo de esquema xml, carregue o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="ebd69-168">After creating and configuring your xml schema file, upload hello file.</span></span> <span data-ttu-id="ebd69-169">Isso criará sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="ebd69-169">This will create your virtual network.</span></span>
   
    <span data-ttu-id="ebd69-170">Use Olá tooupload cmdlet a seguir seu arquivo, substituindo o valor de saudação com seus próprios.</span><span class="sxs-lookup"><span data-stu-id="ebd69-170">Use hello following cmdlet tooupload your file, replacing hello value with your own.</span></span>
   
        Set-AzureVNetConfig -ConfigurationPath 'C:\NetworkConfig.xml'
4. <span data-ttu-id="ebd69-171"><a name="gw">
            </a>Crie um gateway de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ebd69-171"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="ebd69-172">Ser toospecify se Olá GatewaySKU como *padrão*, *HighPerformance*, ou *UltraPerformance* e Olá GatewayType como *DynamicRouting*.</span><span class="sxs-lookup"><span data-stu-id="ebd69-172">Be sure toospecify hello GatewaySKU as *Standard*, *HighPerformance*, or *UltraPerformance* and hello GatewayType as *DynamicRouting*.</span></span>
   
    <span data-ttu-id="ebd69-173">Use Olá exemplo a seguir, substituindo valores de saudação para seu próprio.</span><span class="sxs-lookup"><span data-stu-id="ebd69-173">Use hello following sample, substituting hello values for your own.</span></span>
   
        New-AzureVNetGateway -VNetName MyAzureVNET -GatewayType DynamicRouting -GatewaySKU HighPerformance
5. <span data-ttu-id="ebd69-174">Vincule um circuito de rota expressa toohello do gateway de rota expressa hello.</span><span class="sxs-lookup"><span data-stu-id="ebd69-174">Link hello ExpressRoute gateway toohello ExpressRoute circuit.</span></span> <span data-ttu-id="ebd69-175">Após essa etapa foi concluída, a conexão Olá entre sua rede local e o Azure, por meio do ExpressRoute, é estabelecida.</span><span class="sxs-lookup"><span data-stu-id="ebd69-175">After this step has been completed, hello connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span>
   
        New-AzureDedicatedCircuitLink -ServiceKey <service-key> -VNetName MyAzureVNET
6. <span data-ttu-id="ebd69-176"><a name="vpngw"></a>Em seguida, crie seu gateway de VPN Site a Site.</span><span class="sxs-lookup"><span data-stu-id="ebd69-176"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="ebd69-177">Olá GatewaySKU devem ser *padrão*, *HighPerformance*, ou *UltraPerformance* e hello GatewayType deve ser *DynamicRouting*.</span><span class="sxs-lookup"><span data-stu-id="ebd69-177">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance* and hello GatewayType must be *DynamicRouting*.</span></span>
   
        New-AzureVirtualNetworkGateway -VNetName MyAzureVNET -GatewayName S2SVPN -GatewayType DynamicRouting -GatewaySKU  HighPerformance
   
    <span data-ttu-id="ebd69-178">configurações para gateway de rede virtual do hello tooretrieve, incluindo Olá gateway ID e o IP público do hello, usam Olá `Get-AzureVirtualNetworkGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ebd69-178">tooretrieve hello virtual network gateway settings, including hello gateway ID and hello public IP, use hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span>
   
        Get-AzureVirtualNetworkGateway
   
        GatewayId            : 348ae011-ffa9-4add-b530-7cb30010565e
        GatewayName          : S2SVPN
        LastEventData        :
        GatewayType          : DynamicRouting
        LastEventTimeStamp   : 5/29/2015 4:41:41 PM
        LastEventMessage     : Successfully created a gateway for hello following virtual network: GNSDesMoines
        LastEventID          : 23002
        State                : Provisioned
        VIPAddress           : 104.43.x.y
        DefaultSite          :
        GatewaySKU           : HighPerformance
        Location             :
        VnetId               : 979aabcf-e47f-4136-ab9b-b4780c1e1bd5
        SubnetId             :
        EnableBgp            : False
        OperationDescription : Get-AzureVirtualNetworkGateway
        OperationId          : 42773656-85e1-a6b6-8705-35473f1e6f6a
        OperationStatus      : Succeeded
7. <span data-ttu-id="ebd69-179">Crie uma entidade de gateway de VPN de site local.</span><span class="sxs-lookup"><span data-stu-id="ebd69-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="ebd69-180">Esse comando não configura seu gateway de VPN local.</span><span class="sxs-lookup"><span data-stu-id="ebd69-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="ebd69-181">Em vez disso, permite configurações de gateway local tooprovide hello, como o IP público hello e hello local espaço de endereço, para que hello gateway VPN do Azure pode se conectar tooit.</span><span class="sxs-lookup"><span data-stu-id="ebd69-181">Rather, it allows you tooprovide hello local gateway settings, such as hello public IP and hello on-premises address space, so that hello Azure VPN gateway can connect tooit.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="ebd69-182">site local Olá Olá VPN Site a Site não está definido em Olá netcfg.</span><span class="sxs-lookup"><span data-stu-id="ebd69-182">hello local site for hello Site-to-Site VPN is not defined in hello netcfg.</span></span> <span data-ttu-id="ebd69-183">Em vez disso, você deve usar parâmetros cmdlet toospecify Olá site local.</span><span class="sxs-lookup"><span data-stu-id="ebd69-183">Instead, you must use this cmdlet toospecify hello local site parameters.</span></span> <span data-ttu-id="ebd69-184">Não é possível defini-lo usando o portal ou arquivo de netcfg hello.</span><span class="sxs-lookup"><span data-stu-id="ebd69-184">You cannot define it using either portal, or hello netcfg file.</span></span>
   > 
   > 
   
    <span data-ttu-id="ebd69-185">Use Olá exemplo a seguir, substituindo valores hello com seus próprios.</span><span class="sxs-lookup"><span data-stu-id="ebd69-185">Use hello following sample, replacing hello values with your own.</span></span>
   
        New-AzureLocalNetworkGateway -GatewayName MyLocalNetwork -IpAddress <MyLocalGatewayIp> -AddressSpace <MyLocalNetworkAddress>
   
   > [!NOTE]
   > <span data-ttu-id="ebd69-186">Se sua rede local tiver várias rotas, você poderá passá-las como uma matriz.</span><span class="sxs-lookup"><span data-stu-id="ebd69-186">If your local network has multiple routes, you can pass them all in as an array.</span></span>  <span data-ttu-id="ebd69-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span><span class="sxs-lookup"><span data-stu-id="ebd69-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span></span>  
   > 
   > 

    <span data-ttu-id="ebd69-188">configurações para gateway de rede virtual do hello tooretrieve, incluindo Olá gateway ID e o IP público do hello, usam Olá `Get-AzureVirtualNetworkGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ebd69-188">tooretrieve hello virtual network gateway settings, including hello gateway ID and hello public IP, use hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="ebd69-189">Consulte Olá exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="ebd69-189">See hello following example.</span></span>

        Get-AzureLocalNetworkGateway

        GatewayId            : 532cb428-8c8c-4596-9a4f-7ae3a9fcd01b
        GatewayName          : MyLocalNetwork
        IpAddress            : 23.39.x.y
        AddressSpace         : {10.1.2.0/24}
        OperationDescription : Get-AzureLocalNetworkGateway
        OperationId          : ddc4bfae-502c-adc7-bd7d-1efbc00b3fe5
        OperationStatus      : Succeeded


1. <span data-ttu-id="ebd69-190">Configure seu dispositivo tooconnect toohello novo gateway de VPN local.</span><span class="sxs-lookup"><span data-stu-id="ebd69-190">Configure your local VPN device tooconnect toohello new gateway.</span></span> <span data-ttu-id="ebd69-191">Use as informações de saudação recuperado na etapa 6, ao configurar seu dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="ebd69-191">Use hello information that you retrieved in step 6 when configuring your VPN device.</span></span> <span data-ttu-id="ebd69-192">Para obter mais informações sobre a configuração de dispositivo VPN, consulte [Configuração do Dispositivo VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="ebd69-192">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
2. <span data-ttu-id="ebd69-193">Gateway VPN Site a Site link Olá no gateway local toohello do Azure.</span><span class="sxs-lookup"><span data-stu-id="ebd69-193">Link hello Site-to-Site VPN gateway on Azure toohello local gateway.</span></span>
   
    <span data-ttu-id="ebd69-194">Neste exemplo, connectedEntityId é a ID de gateway local hello, que você pode encontrar executando `Get-AzureLocalNetworkGateway`.</span><span class="sxs-lookup"><span data-stu-id="ebd69-194">In this example, connectedEntityId is hello local gateway ID, which you can find by running `Get-AzureLocalNetworkGateway`.</span></span> <span data-ttu-id="ebd69-195">Você pode encontrar virtualNetworkGatewayId usando Olá `Get-AzureVirtualNetworkGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ebd69-195">You can find virtualNetworkGatewayId by using hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="ebd69-196">Após essa etapa, é estabelecida a conexão Olá entre sua rede local e o Azure via Olá conexão VPN Site a Site.</span><span class="sxs-lookup"><span data-stu-id="ebd69-196">After this step, hello connection between your local network and Azure via hello Site-to-Site VPN connection is established.</span></span>

        New-AzureVirtualNetworkGatewayConnection -connectedEntityId <local-network-gateway-id> -gatewayConnectionName Azure2Local -gatewayConnectionType IPsec -sharedKey abc123 -virtualNetworkGatewayId <azure-s2s-vpn-gateway-id>

## <span data-ttu-id="ebd69-197"><a name="add"></a>tooconfigure coexsiting conexões para uma rede virtual já existente</span><span class="sxs-lookup"><span data-stu-id="ebd69-197"><a name="add"></a>tooconfigure coexsiting connections for an already existing VNet</span></span>
<span data-ttu-id="ebd69-198">Se você tiver uma rede virtual existente, verifique o tamanho de sub-rede de gateway hello.</span><span class="sxs-lookup"><span data-stu-id="ebd69-198">If you have an existing virtual network, check hello gateway subnet size.</span></span> <span data-ttu-id="ebd69-199">Se a sub-rede do gateway Olá for /28 ou /29, primeiro exclua o gateway de rede virtual hello e aumentar o tamanho de sub-rede de gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="ebd69-199">If hello gateway subnet is /28 or /29, you must first delete hello virtual network gateway and increase hello gateway subnet size.</span></span> <span data-ttu-id="ebd69-200">Olá etapas nesta seção mostram como toodo que.</span><span class="sxs-lookup"><span data-stu-id="ebd69-200">hello steps in this section will show you how toodo that.</span></span>

<span data-ttu-id="ebd69-201">Se a sub-rede do gateway de saudação é /27 ou maior e rede virtual Olá é conectado por meio de rota expressa, você pode ignorar as etapas de saudação abaixo e prosseguir muito["Etapa 6 – criar um gateway VPN Site a Site"](#vpngw) na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="ebd69-201">If hello gateway subnet is /27 or larger and hello virtual network is connected via ExpressRoute, you can skip hello steps below and proceed too["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in hello previous section.</span></span>

> [!NOTE]
> <span data-ttu-id="ebd69-202">Quando você exclui um gateway existente Olá, seus locais perderá a rede virtual do hello conexão tooyour enquanto você trabalha nessa configuração.</span><span class="sxs-lookup"><span data-stu-id="ebd69-202">When you delete hello existing gateway, your local premises will lose hello connection tooyour virtual network while you are working on this configuration.</span></span>
> 
> 

1. <span data-ttu-id="ebd69-203">Você precisará tooinstall Olá última versão do hello cmdlets do PowerShell do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ebd69-203">You'll need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="ebd69-204">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações sobre como instalar os cmdlets do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="ebd69-204">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span> <span data-ttu-id="ebd69-205">Observe que Olá cmdlets que você usará para essa configuração pode ser um pouco diferente do que você talvez esteja familiarizado com.</span><span class="sxs-lookup"><span data-stu-id="ebd69-205">Note that hello cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="ebd69-206">Se toouse Olá cmdlets ser especificado nestas instruções.</span><span class="sxs-lookup"><span data-stu-id="ebd69-206">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="ebd69-207">Exclua gateway existente Olá rota expressa ou VPN Site a Site.</span><span class="sxs-lookup"><span data-stu-id="ebd69-207">Delete hello existing ExpressRoute or Site-to-Site VPN gateway.</span></span> <span data-ttu-id="ebd69-208">Use Olá cmdlet a seguir, substituindo valores hello com seus próprios.</span><span class="sxs-lookup"><span data-stu-id="ebd69-208">Use hello following cmdlet, replacing hello values with your own.</span></span>
   
        Remove-AzureVNetGateway –VnetName MyAzureVNET
3. <span data-ttu-id="ebd69-209">Exporte o esquema de saudação da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="ebd69-209">Export hello virtual network schema.</span></span> <span data-ttu-id="ebd69-210">Use Olá cmdlet do PowerShell a seguir, substituindo valores hello com seus próprios.</span><span class="sxs-lookup"><span data-stu-id="ebd69-210">Use hello following PowerShell cmdlet, replacing hello values with your own.</span></span>
   
        Get-AzureVNetConfig –ExportToFile “C:\NetworkConfig.xml”
4. <span data-ttu-id="ebd69-211">Edite esquema de arquivo de configuração de rede Olá para que a sub-rede de gateway de saudação é /27 ou um prefixo mais curto (como /26 ou /25).</span><span class="sxs-lookup"><span data-stu-id="ebd69-211">Edit hello network configuration file schema so that hello gateway subnet is /27 or a shorter prefix (such as /26 or /25).</span></span> <span data-ttu-id="ebd69-212">Consulte Olá exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="ebd69-212">See hello following example.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="ebd69-213">Se você não tiver endereços IP suficientes no tamanho de sub-rede de gateway sua rede virtual tooincrease hello, será necessário tooadd mais espaço de endereço IP.</span><span class="sxs-lookup"><span data-stu-id="ebd69-213">If you don't have enough IP addresses left in your virtual network tooincrease hello gateway subnet size, you need tooadd more IP address space.</span></span> <span data-ttu-id="ebd69-214">Para obter mais informações sobre o esquema de configuração hello, consulte [esquema de configuração de rede Virtual do Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="ebd69-214">For more information about hello configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   > 
   > 
   
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.17.159.224/27</AddressPrefix>
          </Subnet>
5. <span data-ttu-id="ebd69-215">Se seu gateway anterior era uma VPN Site a Site, você deve também alterar tipo de conexão de saudação muito**dedicado**.</span><span class="sxs-lookup"><span data-stu-id="ebd69-215">If your previous gateway was a Site-to-Site VPN, you must also change hello connection type too**Dedicated**.</span></span>
   
                 <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="MyLocalNetwork">
                      <Connection type="Dedicated" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
6. <span data-ttu-id="ebd69-216">Neste ponto, você terá uma VNet sem nenhum gateway.</span><span class="sxs-lookup"><span data-stu-id="ebd69-216">At this point, you'll have a VNet with no gateways.</span></span> <span data-ttu-id="ebd69-217">novos gateways do toocreate e concluir as conexões, você pode continuar com a [etapa 4 - criar um gateway de rota expressa](#gw), encontrado em Olá precede o conjunto de etapas.</span><span class="sxs-lookup"><span data-stu-id="ebd69-217">toocreate new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in hello preceding set of steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebd69-218">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ebd69-218">Next steps</span></span>
<span data-ttu-id="ebd69-219">Para obter mais informações sobre a rota expressa, consulte Olá [perguntas frequentes sobre o rota expressa](expressroute-faqs.md)</span><span class="sxs-lookup"><span data-stu-id="ebd69-219">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md)</span></span>

