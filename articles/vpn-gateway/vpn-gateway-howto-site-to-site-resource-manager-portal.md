---
title: 'Conectar a sua rede local para uma rede virtual do Azure: VPN Site a Site: portal | Microsoft Docs'
description: "Etapas para criar uma conexão IPsec de sua rede local para uma rede virtual do Azure pela Internet pública. Essas etapas o ajudarão a criar uma conexão de Gateway de VPN Site a Site entre locais usando o portal."
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
ms.openlocfilehash: 0dec0d3744f76a06313928197f3a5229290ba32b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-site-to-site-connection-in-the-azure-portal"></a><span data-ttu-id="2a0b2-104">Criar uma conexão Site a Site no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2a0b2-104">Create a Site-to-Site connection in the Azure portal</span></span>

<span data-ttu-id="2a0b2-105">Este artigo mostra como usar o portal do Azure para criar uma conexão de gateway de VPN Site a Site de sua rede local para a rede virtual.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-105">This article shows you how to use the Azure portal to create a Site-to-Site VPN gateway connection from your on-premises network to the VNet.</span></span> <span data-ttu-id="2a0b2-106">As etapas neste artigo se aplicam ao modelo de implantação do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-106">The steps in this article apply to the Resource Manager deployment model.</span></span> <span data-ttu-id="2a0b2-107">Você também pode criar essa configuração usando uma ferramenta de implantação ou um modelo de implantação diferente, selecionando uma opção diferente na lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="2a0b2-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2a0b2-108">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2a0b2-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="2a0b2-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2a0b2-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="2a0b2-110">CLI</span><span class="sxs-lookup"><span data-stu-id="2a0b2-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="2a0b2-111">Portal do Azure (clássico)</span><span class="sxs-lookup"><span data-stu-id="2a0b2-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

<span data-ttu-id="2a0b2-112">Uma conexão de gateway de VPN Site a Site é usada para conectar a rede local a uma rede virtual do Azure por um túnel VPN IPsec/IKE (IKEv1 ou IKEv2).</span><span class="sxs-lookup"><span data-stu-id="2a0b2-112">A Site-to-Site VPN gateway connection is used to connect your on-premises network to an Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="2a0b2-113">Esse tipo de conexão exige um dispositivo VPN localizado no local que tenha um endereço IP público voltado para o exterior atribuído a ele.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-113">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned to it.</span></span> <span data-ttu-id="2a0b2-114">Para saber mais sobre os gateways de VPN, veja [Sobre o gateway de VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="2a0b2-114">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![Diagrama de conexão Site a Site de Gateway de VPN entre locais](./media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a><span data-ttu-id="2a0b2-116">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="2a0b2-116">Before you begin</span></span>

<span data-ttu-id="2a0b2-117">Verifique se você atende aos seguintes critérios antes de iniciar a configuração:</span><span class="sxs-lookup"><span data-stu-id="2a0b2-117">Verify that you have met the following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="2a0b2-118">Verifique se você possui um dispositivo VPN compatível e alguém que possa configurá-lo.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-118">Make sure you have a compatible VPN device and someone who is able to configure it.</span></span> <span data-ttu-id="2a0b2-119">Para obter mais informações sobre dispositivos VPN compatíveis e a configuração de dispositivo, confira [Sobre dispositivos VPN](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="2a0b2-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="2a0b2-120">Verifique se você possui um endereço IPv4 público voltado para o exterior para seu dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="2a0b2-121">Esse endereço IP não pode estar localizado atrás de um NAT.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="2a0b2-122">Se não estiver familiarizado com os intervalos de endereços IP localizados na configuração de rede local, você precisará trabalhar em conjunto com alguém que possa lhe fornecer os detalhes.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-122">If you are unfamiliar with the IP address ranges located in your on-premises network configuration, you need to coordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="2a0b2-123">Ao criar essa configuração, você deve especificar os prefixos de intervalo de endereços IP que o Azure roteará para seu local.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-123">When you create this configuration, you must specify the IP address range prefixes that Azure will route to your on-premises location.</span></span> <span data-ttu-id="2a0b2-124">Nenhuma das sub-redes da rede local podem se sobrepor às sub-redes de rede virtual às quais você deseja se conectar.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-124">None of the subnets of your on-premises network can over lap with the virtual network subnets that you want to connect to.</span></span> 

### <span data-ttu-id="2a0b2-125"><a name="values"></a>Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="2a0b2-125"><a name="values"></a>Example values</span></span>

<span data-ttu-id="2a0b2-126">Os exemplos neste artigo usam os seguintes valores.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-126">The examples in this article use the following values.</span></span> <span data-ttu-id="2a0b2-127">Você pode usar esses valores para criar um ambiente de teste ou consultá-los para compreender melhor os exemplos neste artigo.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-127">You can use these values to create a test environment, or refer to them to better understand the examples in this article.</span></span>

* <span data-ttu-id="2a0b2-128">**Nome da rede virtual:** TestVNet1</span><span class="sxs-lookup"><span data-stu-id="2a0b2-128">**VNet Name:** TestVNet1</span></span>
* <span data-ttu-id="2a0b2-129">**Espaço de endereço:**</span><span class="sxs-lookup"><span data-stu-id="2a0b2-129">**Address Space:**</span></span> 
  * <span data-ttu-id="2a0b2-130">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="2a0b2-130">10.11.0.0/16</span></span>
  * <span data-ttu-id="2a0b2-131">10.12.0.0/16 (opcional para este exercício)</span><span class="sxs-lookup"><span data-stu-id="2a0b2-131">10.12.0.0/16 (optional for this exercise)</span></span>
* <span data-ttu-id="2a0b2-132">**Sub-redes:**</span><span class="sxs-lookup"><span data-stu-id="2a0b2-132">**Subnets:**</span></span>
  * <span data-ttu-id="2a0b2-133">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="2a0b2-133">FrontEnd: 10.11.0.0/24</span></span>
  * <span data-ttu-id="2a0b2-134">BackEnd: 10.12.0.0/24 (opcional para este exercício)</span><span class="sxs-lookup"><span data-stu-id="2a0b2-134">BackEnd: 10.12.0.0/24 (optional for this exercise)</span></span>
* <span data-ttu-id="2a0b2-135">**GatewaySubnet:** 10.11.255.0/27</span><span class="sxs-lookup"><span data-stu-id="2a0b2-135">**GatewaySubnet:** 10.11.255.0/27</span></span>
* <span data-ttu-id="2a0b2-136">**Grupo de recursos:** TestRG1</span><span class="sxs-lookup"><span data-stu-id="2a0b2-136">**Resource Group:** TestRG1</span></span>
* <span data-ttu-id="2a0b2-137">**Local:** Leste dos EUA</span><span class="sxs-lookup"><span data-stu-id="2a0b2-137">**Location:** East US</span></span>
* <span data-ttu-id="2a0b2-138">**Servidor DNS:** opcional.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-138">**DNS Server:** Optional.</span></span> <span data-ttu-id="2a0b2-139">O endereço IP do seu servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-139">The IP address of your DNS server.</span></span>
* <span data-ttu-id="2a0b2-140">**Nome do gateway de rede virtual:** VNet1GW</span><span class="sxs-lookup"><span data-stu-id="2a0b2-140">**Virtual Network Gateway Name:** VNet1GW</span></span>
* <span data-ttu-id="2a0b2-141">**IP público:** VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="2a0b2-141">**Public IP:** VNet1GWIP</span></span>
* <span data-ttu-id="2a0b2-142">**Tipo de VPN:** baseada em rota</span><span class="sxs-lookup"><span data-stu-id="2a0b2-142">**VPN Type:** Route-based</span></span>
* <span data-ttu-id="2a0b2-143">**Tipo de Conexão:** site a site (IPsec)</span><span class="sxs-lookup"><span data-stu-id="2a0b2-143">**Connection Type:** Site-to-site (IPsec)</span></span>
* <span data-ttu-id="2a0b2-144">**Tipo de gateway:** VPN</span><span class="sxs-lookup"><span data-stu-id="2a0b2-144">**Gateway Type:** VPN</span></span>
* <span data-ttu-id="2a0b2-145">**Nome do Gateway de Rede Local:** Site2</span><span class="sxs-lookup"><span data-stu-id="2a0b2-145">**Local Network Gateway Name:** Site2</span></span>
* <span data-ttu-id="2a0b2-146">**Nome da conexão:** VNet1toSite2</span><span class="sxs-lookup"><span data-stu-id="2a0b2-146">**Connection Name:** VNet1toSite2</span></span>

## <span data-ttu-id="2a0b2-147"><a name="CreatVNet"></a>1. Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="2a0b2-147"><a name="CreatVNet"></a>1. Create a virtual network</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="2a0b2-148"><a name="dns"></a>2. Especificar um servidor DNS</span><span class="sxs-lookup"><span data-stu-id="2a0b2-148"><a name="dns"></a>2. Specify a DNS server</span></span>

<span data-ttu-id="2a0b2-149">O DNS não é necessário para criar uma conexão Site a Site.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-149">DNS is not required to create a Site-to-Site connection.</span></span> <span data-ttu-id="2a0b2-150">No entanto, se você quiser ter a resolução de nomes dos recursos que são implantados em sua rede virtual, deverá especificar um servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-150">However, if you want to have name resolution for resources that are deployed to your virtual network, you should specify a DNS server.</span></span> <span data-ttu-id="2a0b2-151">Essa configuração permite que você especifique o servidor DNS que deseja usar para a resolução de nomes dessa rede virtual.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-151">This setting lets you specify the DNS server that you want to use for name resolution for this virtual network.</span></span> <span data-ttu-id="2a0b2-152">Ela não cria um servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-152">It does not create a DNS server.</span></span> <span data-ttu-id="2a0b2-153">Para saber mais sobre a resolução de nomes, confira [Resolução de nomes para VMs e instâncias de função](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="2a0b2-153">For more information about name resolution, see [Name Resolution for VMs and role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <span data-ttu-id="2a0b2-154"><a name="gatewaysubnet"></a>3. Criar a sub-rede de gateway</span><span class="sxs-lookup"><span data-stu-id="2a0b2-154"><a name="gatewaysubnet"></a>3. Create the gateway subnet</span></span>

[!INCLUDE [vpn-gateway-aboutgwsubnet](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="2a0b2-155"><a name="VNetGateway"></a>4. Criar o gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="2a0b2-155"><a name="VNetGateway"></a>4. Create the VPN gateway</span></span>

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <span data-ttu-id="2a0b2-156"><a name="LocalNetworkGateway"></a>5. Criar o gateway de rede local</span><span class="sxs-lookup"><span data-stu-id="2a0b2-156"><a name="LocalNetworkGateway"></a>5. Create the local network gateway</span></span>

<span data-ttu-id="2a0b2-157">O gateway de rede local geralmente se refere ao seu local.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-157">The local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="2a0b2-158">Você atribui um nome ao site pelo qual o Azure pode fazer referência a ele e especifica o endereço IP do dispositivo VPN local para o qual você criará uma conexão.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-158">You give the site a name by which Azure can refer to it, then specify the IP address of the on-premises VPN device to which you will create a connection.</span></span> <span data-ttu-id="2a0b2-159">Você também pode especificar os prefixos de endereço IP que serão roteados por meio do gateway de VPN para o dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-159">You also specify the IP address prefixes that will be routed through the VPN gateway to the VPN device.</span></span> <span data-ttu-id="2a0b2-160">Os prefixos de endereço que você especifica são os prefixos localizados em sua rede local.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-160">The address prefixes you specify are the prefixes located on your on-premises network.</span></span> <span data-ttu-id="2a0b2-161">Se as alterações de rede local ou se você precisar alterar o endereço IP público para o dispositivo VPN, poderá atualizar facilmente os valores mais tarde.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-161">If your on-premises network changes or you need to change the public IP address for the VPN device, you can easily update the values later.</span></span>

[!INCLUDE [Add local network gateway](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <span data-ttu-id="2a0b2-162"><a name="VPNDevice"></a>6. Configurar o dispositivo de VPN</span><span class="sxs-lookup"><span data-stu-id="2a0b2-162"><a name="VPNDevice"></a>6. Configure your VPN device</span></span>

<span data-ttu-id="2a0b2-163">As conexões Site a Site para uma rede local exigem um dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-163">Site-to-Site connections to an on-premises network require a VPN device.</span></span> <span data-ttu-id="2a0b2-164">Nesta etapa, você deve configurar seu dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-164">In this step, you configure your VPN device.</span></span> <span data-ttu-id="2a0b2-165">Ao configurar seu dispositivo VPN, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="2a0b2-165">When configuring your VPN device, you need the following:</span></span>

- <span data-ttu-id="2a0b2-166">Uma chave compartilhada.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-166">A shared key.</span></span> <span data-ttu-id="2a0b2-167">Essa é a mesma chave compartilhada especificada ao criar a conexão VPN Site a Site.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-167">This is the same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="2a0b2-168">Em nossos exemplos, usamos uma chave compartilhada básica.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-168">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="2a0b2-169">Recomendamos gerar uma chave mais complexa para uso.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-169">We recommend that you generate a more complex key to use.</span></span>
- <span data-ttu-id="2a0b2-170">O endereço IP público do seu gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-170">The Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="2a0b2-171">Você pode exibir o endereço IP público usando o portal do Azure, o PowerShell ou a CLI.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-171">You can view the public IP address by using the Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="2a0b2-172">Para localizar o endereço IP público do seu gateway de VPN usando o portal do Azure, navegue até **Gateways de rede virtual** e clique no nome do seu gateway.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-172">To find the Public IP address of your VPN gateway using the Azure portal, navigate to **Virtual network gateways**, then click the name of your gateway.</span></span>

[!INCLUDE [Configure a VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <span data-ttu-id="2a0b2-173"><a name="CreateConnection"></a>7. Criar a conexão VPN</span><span class="sxs-lookup"><span data-stu-id="2a0b2-173"><a name="CreateConnection"></a>7. Create the VPN connection</span></span>

<span data-ttu-id="2a0b2-174">Crie a conexão VPN Site a Site entre o gateway de rede virtual e o dispositivo VPN local.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-174">Create the Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span>

[!INCLUDE [Add connections](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <span data-ttu-id="2a0b2-175"><a name="VerifyConnection"></a>8. Verificar a conexão VPN</span><span class="sxs-lookup"><span data-stu-id="2a0b2-175"><a name="VerifyConnection"></a>8. Verify the VPN connection</span></span>

[!INCLUDE [Verify - Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="2a0b2-176"><a name="connectVM"></a>Para conectar-se a uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="2a0b2-176"><a name="connectVM"></a>To connect to a virtual machine</span></span>

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="2a0b2-177"><a name="reset"></a>Como redefinir um gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="2a0b2-177"><a name="reset"></a>How to reset a VPN gateway</span></span>

<span data-ttu-id="2a0b2-178">Redefinir um gateway de VPN do Azure é útil se você perde a conectividade VPN entre locais em um ou mais túneis de VPN site a site.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-178">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="2a0b2-179">Nessa situação, os dispositivos VPN locais estão funcionando corretamente, mas não são capazes de estabelecer túneis IPsec com os gateways de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a0b2-179">In this situation, your on-premises VPN devices are all working correctly, but are not able to establish IPsec tunnels with the Azure VPN gateways.</span></span> <span data-ttu-id="2a0b2-180">Para obter as etapas, consulte [Redefinir um gateway de VPN](vpn-gateway-resetgw-classic.md).</span><span class="sxs-lookup"><span data-stu-id="2a0b2-180">For steps, see [Reset a VPN gateway](vpn-gateway-resetgw-classic.md).</span></span>

## <span data-ttu-id="2a0b2-181"><a name="resize"></a>Como alterar um SKU de gateway (redimensionar um gateway)</span><span class="sxs-lookup"><span data-stu-id="2a0b2-181"><a name="resize"></a>How to change a gateway SKU (resize a gateway)</span></span>

<span data-ttu-id="2a0b2-182">Para obter as etapas para alterar um SKU de gateway, consulte [SKUs de gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="2a0b2-182">For the steps to change a gateway SKU, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a0b2-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2a0b2-183">Next steps</span></span>

* <span data-ttu-id="2a0b2-184">Para obter informações sobre o BGP, consulte a [Visão Geral do BGP](vpn-gateway-bgp-overview.md) e [Como configurar o BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="2a0b2-184">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="2a0b2-185">Para saber mais sobre Túneis Forçados, confira [Sobre o Túnel Forçado](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="2a0b2-185">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="2a0b2-186">Para obter informações sobre Conexões Altamente Disponíveis Ativo-Ativo, consulte [Conectividade Altamente Disponível entre locais e Rede Virtual para Rede Virtual](vpn-gateway-highlyavailable.md).</span><span class="sxs-lookup"><span data-stu-id="2a0b2-186">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
