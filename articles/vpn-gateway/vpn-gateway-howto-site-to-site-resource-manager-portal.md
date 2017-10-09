---
title: 'Conecte-se a sua rede de local tooan rede virtual do Azure: VPN Site a Site: Portal | Microsoft Docs'
description: "Etapas toocreate uma conexão IPsec de seu local de rede tooan rede virtual do Azure sobre Olá Internet pública. Essas etapas ajudará você a criar uma conexão de Gateway VPN Site a Site entre locais usando o portal de saudação."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 827a4db7-7fa5-4eaf-b7e1-e1518c51c815
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 6f0acbaf1bf016026cefade048a116e94686103d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-in-hello-azure-portal"></a><span data-ttu-id="959e0-104">Criar uma conexão Site a Site no portal do Azure de saudação</span><span class="sxs-lookup"><span data-stu-id="959e0-104">Create a Site-to-Site connection in hello Azure portal</span></span>

<span data-ttu-id="959e0-105">Este artigo mostra como toouse Olá toocreate portal do Azure uma conexão de gateway VPN Site a Site de sua toohello de rede local VNet.</span><span class="sxs-lookup"><span data-stu-id="959e0-105">This article shows you how toouse hello Azure portal toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="959e0-106">Olá etapas neste artigo se aplicam a modelo de implantação do Gerenciador de recursos de toohello.</span><span class="sxs-lookup"><span data-stu-id="959e0-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="959e0-107">Você também pode criar essa configuração usando uma ferramenta de implantação diferente ou um modelo de implantação, selecionando uma opção diferente de saudação lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="959e0-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="959e0-108">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="959e0-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="959e0-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="959e0-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="959e0-110">CLI</span><span class="sxs-lookup"><span data-stu-id="959e0-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="959e0-111">Portal do Azure (clássico)</span><span class="sxs-lookup"><span data-stu-id="959e0-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

<span data-ttu-id="959e0-112">Uma conexão de gateway VPN Site a Site é usado tooconnect seu local de rede tooan rede virtual do Azure por um túnel VPN IPsec/IKE (IKEv1 ou IKEv2).</span><span class="sxs-lookup"><span data-stu-id="959e0-112">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="959e0-113">Esse tipo de conexão exige um VPN de dispositivos localizado localmente que tenha uma tooit de endereço atribuído de IP público externamente.</span><span class="sxs-lookup"><span data-stu-id="959e0-113">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="959e0-114">Para saber mais sobre os gateways de VPN, veja [Sobre o gateway de VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="959e0-114">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![Diagrama de conexão Site a Site de Gateway de VPN entre locais](./media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a><span data-ttu-id="959e0-116">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="959e0-116">Before you begin</span></span>

<span data-ttu-id="959e0-117">Verifique se você atendeu a saudação critérios a seguir antes de começar a configuração:</span><span class="sxs-lookup"><span data-stu-id="959e0-117">Verify that you have met hello following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="959e0-118">Verifique se você tem um dispositivo VPN compatível e alguém que é capaz de tooconfigure-lo.</span><span class="sxs-lookup"><span data-stu-id="959e0-118">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="959e0-119">Para obter mais informações sobre dispositivos VPN compatíveis e a configuração de dispositivo, confira [Sobre dispositivos VPN](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="959e0-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="959e0-120">Verifique se você possui um endereço IPv4 público voltado para o exterior para seu dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="959e0-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="959e0-121">Esse endereço IP não pode estar localizado atrás de um NAT.</span><span class="sxs-lookup"><span data-stu-id="959e0-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="959e0-122">Se você não estiver familiarizado com intervalos de endereços IP de saudação localizados na configuração de rede local, é necessário toocoordinate com alguém que possa fornecer os detalhes para você.</span><span class="sxs-lookup"><span data-stu-id="959e0-122">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="959e0-123">Quando você criar essa configuração, você deve especificar os prefixos de intervalo endereço IP hello Azure encaminhe tooyour no local.</span><span class="sxs-lookup"><span data-stu-id="959e0-123">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="959e0-124">Nenhuma das sub-redes Olá da sua rede local pode ser sobre colo com sub-redes de rede virtual Olá que você deseja tooconnect para.</span><span class="sxs-lookup"><span data-stu-id="959e0-124">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span> 

### <span data-ttu-id="959e0-125"><a name="values"></a>Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="959e0-125"><a name="values"></a>Example values</span></span>

<span data-ttu-id="959e0-126">Olá exemplos neste artigo usam Olá valores a seguir.</span><span class="sxs-lookup"><span data-stu-id="959e0-126">hello examples in this article use hello following values.</span></span> <span data-ttu-id="959e0-127">Você pode usar esses valores toocreate um ambiente de teste, ou consulte toothem toobetter entender exemplos Olá neste artigo.</span><span class="sxs-lookup"><span data-stu-id="959e0-127">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

* <span data-ttu-id="959e0-128">**Nome da rede virtual:** TestVNet1</span><span class="sxs-lookup"><span data-stu-id="959e0-128">**VNet Name:** TestVNet1</span></span>
* <span data-ttu-id="959e0-129">**Espaço de endereço:**</span><span class="sxs-lookup"><span data-stu-id="959e0-129">**Address Space:**</span></span> 
  * <span data-ttu-id="959e0-130">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="959e0-130">10.11.0.0/16</span></span>
  * <span data-ttu-id="959e0-131">10.12.0.0/16 (opcional para este exercício)</span><span class="sxs-lookup"><span data-stu-id="959e0-131">10.12.0.0/16 (optional for this exercise)</span></span>
* <span data-ttu-id="959e0-132">**Sub-redes:**</span><span class="sxs-lookup"><span data-stu-id="959e0-132">**Subnets:**</span></span>
  * <span data-ttu-id="959e0-133">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="959e0-133">FrontEnd: 10.11.0.0/24</span></span>
  * <span data-ttu-id="959e0-134">BackEnd: 10.12.0.0/24 (opcional para este exercício)</span><span class="sxs-lookup"><span data-stu-id="959e0-134">BackEnd: 10.12.0.0/24 (optional for this exercise)</span></span>
* <span data-ttu-id="959e0-135">**GatewaySubnet:** 10.11.255.0/27</span><span class="sxs-lookup"><span data-stu-id="959e0-135">**GatewaySubnet:** 10.11.255.0/27</span></span>
* <span data-ttu-id="959e0-136">**Grupo de recursos:** TestRG1</span><span class="sxs-lookup"><span data-stu-id="959e0-136">**Resource Group:** TestRG1</span></span>
* <span data-ttu-id="959e0-137">**Local:** Leste dos EUA</span><span class="sxs-lookup"><span data-stu-id="959e0-137">**Location:** East US</span></span>
* <span data-ttu-id="959e0-138">**Servidor DNS:** opcional.</span><span class="sxs-lookup"><span data-stu-id="959e0-138">**DNS Server:** Optional.</span></span> <span data-ttu-id="959e0-139">endereço IP de saudação do servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="959e0-139">hello IP address of your DNS server.</span></span>
* <span data-ttu-id="959e0-140">**Nome do gateway de rede virtual:** VNet1GW</span><span class="sxs-lookup"><span data-stu-id="959e0-140">**Virtual Network Gateway Name:** VNet1GW</span></span>
* <span data-ttu-id="959e0-141">**IP público:** VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="959e0-141">**Public IP:** VNet1GWIP</span></span>
* <span data-ttu-id="959e0-142">**Tipo de VPN:** baseada em rota</span><span class="sxs-lookup"><span data-stu-id="959e0-142">**VPN Type:** Route-based</span></span>
* <span data-ttu-id="959e0-143">**Tipo de Conexão:** site a site (IPsec)</span><span class="sxs-lookup"><span data-stu-id="959e0-143">**Connection Type:** Site-to-site (IPsec)</span></span>
* <span data-ttu-id="959e0-144">**Tipo de gateway:** VPN</span><span class="sxs-lookup"><span data-stu-id="959e0-144">**Gateway Type:** VPN</span></span>
* <span data-ttu-id="959e0-145">**Nome do Gateway de Rede Local:** Site2</span><span class="sxs-lookup"><span data-stu-id="959e0-145">**Local Network Gateway Name:** Site2</span></span>
* <span data-ttu-id="959e0-146">**Nome da conexão:** VNet1toSite2</span><span class="sxs-lookup"><span data-stu-id="959e0-146">**Connection Name:** VNet1toSite2</span></span>

## <span data-ttu-id="959e0-147"><a name="CreatVNet"></a>1. Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="959e0-147"><a name="CreatVNet"></a>1. Create a virtual network</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="959e0-148"><a name="dns"></a>2. Especificar um servidor DNS</span><span class="sxs-lookup"><span data-stu-id="959e0-148"><a name="dns"></a>2. Specify a DNS server</span></span>

<span data-ttu-id="959e0-149">DNS não é necessário toocreate uma Site a Site de conexão.</span><span class="sxs-lookup"><span data-stu-id="959e0-149">DNS is not required toocreate a Site-to-Site connection.</span></span> <span data-ttu-id="959e0-150">No entanto, se você quiser toohave a resolução de nomes para recursos de rede virtual tooyour implantado, você deve especificar um servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="959e0-150">However, if you want toohave name resolution for resources that are deployed tooyour virtual network, you should specify a DNS server.</span></span> <span data-ttu-id="959e0-151">Essa configuração permite que você especifique o servidor DNS Olá que você deseja toouse para resolução de nome para essa rede virtual.</span><span class="sxs-lookup"><span data-stu-id="959e0-151">This setting lets you specify hello DNS server that you want toouse for name resolution for this virtual network.</span></span> <span data-ttu-id="959e0-152">Ela não cria um servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="959e0-152">It does not create a DNS server.</span></span> <span data-ttu-id="959e0-153">Para saber mais sobre a resolução de nomes, confira [Resolução de nomes para VMs e instâncias de função](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="959e0-153">For more information about name resolution, see [Name Resolution for VMs and role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <span data-ttu-id="959e0-154"><a name="gatewaysubnet"></a>3. Criar uma sub-rede de gateway Olá</span><span class="sxs-lookup"><span data-stu-id="959e0-154"><a name="gatewaysubnet"></a>3. Create hello gateway subnet</span></span>

[!INCLUDE [vpn-gateway-aboutgwsubnet](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="959e0-155"><a name="VNetGateway"></a>4. Criar gateway VPN Olá</span><span class="sxs-lookup"><span data-stu-id="959e0-155"><a name="VNetGateway"></a>4. Create hello VPN gateway</span></span>

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <span data-ttu-id="959e0-156"><a name="LocalNetworkGateway"></a>5. Criar gateway de rede local Olá</span><span class="sxs-lookup"><span data-stu-id="959e0-156"><a name="LocalNetworkGateway"></a>5. Create hello local network gateway</span></span>

<span data-ttu-id="959e0-157">Normalmente, o gateway de rede local Olá refere-se tooyour no local.</span><span class="sxs-lookup"><span data-stu-id="959e0-157">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="959e0-158">Atribuir o site Olá um nome pelo qual Azure pode consulte tooit e especifique o endereço IP de saudação do hello toowhich de dispositivo VPN de local, você criará uma conexão.</span><span class="sxs-lookup"><span data-stu-id="959e0-158">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="959e0-159">Você também pode especificar prefixos de endereço IP de saudação que serão encaminhados através do dispositivo de VPN toohello do gateway VPN hello.</span><span class="sxs-lookup"><span data-stu-id="959e0-159">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="959e0-160">especificar os prefixos de endereço Olá são prefixos Olá localizados em sua rede local.</span><span class="sxs-lookup"><span data-stu-id="959e0-160">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="959e0-161">Se as alterações de rede local ou precisar de endereço IP público de saudação toochange para dispositivo VPN hello, você pode atualizar facilmente valores hello mais tarde.</span><span class="sxs-lookup"><span data-stu-id="959e0-161">If your on-premises network changes or you need toochange hello public IP address for hello VPN device, you can easily update hello values later.</span></span>

[!INCLUDE [Add local network gateway](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <span data-ttu-id="959e0-162"><a name="VPNDevice"></a>6. Configurar o dispositivo de VPN</span><span class="sxs-lookup"><span data-stu-id="959e0-162"><a name="VPNDevice"></a>6. Configure your VPN device</span></span>

<span data-ttu-id="959e0-163">Rede de local de tooan conexões site a Site requer um dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="959e0-163">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="959e0-164">Nesta etapa, você deve configurar seu dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="959e0-164">In this step, you configure your VPN device.</span></span> <span data-ttu-id="959e0-165">Ao configurar seu dispositivo VPN, você precisa seguir hello:</span><span class="sxs-lookup"><span data-stu-id="959e0-165">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="959e0-166">Uma chave compartilhada.</span><span class="sxs-lookup"><span data-stu-id="959e0-166">A shared key.</span></span> <span data-ttu-id="959e0-167">Isso é Olá mesmo chave que você especificar ao criar sua conexão VPN Site a Site.</span><span class="sxs-lookup"><span data-stu-id="959e0-167">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="959e0-168">Em nossos exemplos, usamos uma chave compartilhada básica.</span><span class="sxs-lookup"><span data-stu-id="959e0-168">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="959e0-169">É recomendável que você gerar um toouse chave mais complexa.</span><span class="sxs-lookup"><span data-stu-id="959e0-169">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="959e0-170">Olá endereço IP público do seu gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="959e0-170">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="959e0-171">Você pode exibir o endereço IP público de saudação usando Olá portal do Azure, PowerShell ou CLI.</span><span class="sxs-lookup"><span data-stu-id="959e0-171">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="959e0-172">Olá toofind endereço IP público do seu gateway VPN usando Olá portal do Azure, navegue muito**gateways de rede Virtual**, clique em nome de saudação do seu gateway.</span><span class="sxs-lookup"><span data-stu-id="959e0-172">toofind hello Public IP address of your VPN gateway using hello Azure portal, navigate too**Virtual network gateways**, then click hello name of your gateway.</span></span>

[!INCLUDE [Configure a VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <span data-ttu-id="959e0-173"><a name="CreateConnection"></a>7. Criar conexão de VPN Olá</span><span class="sxs-lookup"><span data-stu-id="959e0-173"><a name="CreateConnection"></a>7. Create hello VPN connection</span></span>

<span data-ttu-id="959e0-174">Crie conexão de VPN Olá Site a Site entre o gateway de rede virtual e seu dispositivo VPN local.</span><span class="sxs-lookup"><span data-stu-id="959e0-174">Create hello Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span>

[!INCLUDE [Add connections](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <span data-ttu-id="959e0-175"><a name="VerifyConnection"></a>8. Verifique se a conexão de VPN Olá</span><span class="sxs-lookup"><span data-stu-id="959e0-175"><a name="VerifyConnection"></a>8. Verify hello VPN connection</span></span>

[!INCLUDE [Verify - Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="959e0-176"><a name="connectVM"></a>máquina de virtual tooa tooconnect</span><span class="sxs-lookup"><span data-stu-id="959e0-176"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="959e0-177"><a name="reset"></a>Como tooreset um gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="959e0-177"><a name="reset"></a>How tooreset a VPN gateway</span></span>

<span data-ttu-id="959e0-178">Redefinir um gateway de VPN do Azure é útil se você perde a conectividade VPN entre locais em um ou mais túneis de VPN site a site.</span><span class="sxs-lookup"><span data-stu-id="959e0-178">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="959e0-179">Nessa situação, os seus dispositivos VPN local são todos funcionando corretamente, mas são tooestablish não é possível túneis IPsec com gateways de VPN do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="959e0-179">In this situation, your on-premises VPN devices are all working correctly, but are not able tooestablish IPsec tunnels with hello Azure VPN gateways.</span></span> <span data-ttu-id="959e0-180">Para obter as etapas, consulte [Redefinir um gateway de VPN](vpn-gateway-resetgw-classic.md).</span><span class="sxs-lookup"><span data-stu-id="959e0-180">For steps, see [Reset a VPN gateway](vpn-gateway-resetgw-classic.md).</span></span>

## <span data-ttu-id="959e0-181"><a name="resize"></a>Como toochange um gateway de SKU (redimensionar um gateway)</span><span class="sxs-lookup"><span data-stu-id="959e0-181"><a name="resize"></a>How toochange a gateway SKU (resize a gateway)</span></span>

<span data-ttu-id="959e0-182">Para as etapas de saudação toochange um SKU de gateway, consulte [SKUs de Gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="959e0-182">For hello steps toochange a gateway SKU, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

## <a name="next-steps"></a><span data-ttu-id="959e0-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="959e0-183">Next steps</span></span>

* <span data-ttu-id="959e0-184">Para obter informações sobre o BGP, consulte Olá [visão geral de BGP](vpn-gateway-bgp-overview.md) e [como tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="959e0-184">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="959e0-185">Para saber mais sobre Túneis Forçados, confira [Sobre o Túnel Forçado](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="959e0-185">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="959e0-186">Para obter informações sobre Conexões Altamente Disponíveis Ativo-Ativo, consulte [Conectividade Altamente Disponível entre locais e Rede Virtual para Rede Virtual](vpn-gateway-highlyavailable.md).</span><span class="sxs-lookup"><span data-stu-id="959e0-186">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
