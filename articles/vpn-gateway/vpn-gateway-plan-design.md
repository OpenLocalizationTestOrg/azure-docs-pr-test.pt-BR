---
title: "Planejamento e design de conexões entre locais: Gateway de VPN do Azure | Microsoft Docs"
description: "Saiba mais sobre o planejamento e design de Gateway de VPN para conexões entre locais, híbridas e VNet a VNet"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: d5aaab83-4e74-4484-8bf0-cc465811e757
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/27/2017
ms.author: cherylmc
ms.openlocfilehash: 0ebc3ef4a64432e993dd6ed69766bb64544fe433
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="planning-and-design-for-vpn-gateway"></a><span data-ttu-id="d1db3-103">Planejamento e design para o Gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="d1db3-103">Planning and design for VPN Gateway</span></span>

<span data-ttu-id="d1db3-104">Planejar e projetar suas conexões entre redes virtuais e entre locais pode ser simples ou complicado, dependendo das suas necessidades de rede.</span><span class="sxs-lookup"><span data-stu-id="d1db3-104">Planning and designing your cross-premises and VNet-to-VNet configurations can be either simple, or complicated, depending on your networking needs.</span></span> <span data-ttu-id="d1db3-105">Este artigo traz considerações básicas de design e planejamento.</span><span class="sxs-lookup"><span data-stu-id="d1db3-105">This article walks you through basic planning and design considerations.</span></span>

## <span data-ttu-id="d1db3-106"><a name="planning"></a>Planejamento</span><span class="sxs-lookup"><span data-stu-id="d1db3-106"><a name="planning"></a>Planning</span></span>

### <span data-ttu-id="d1db3-107"><a name="compare"></a>Opções de conectividade entre locais</span><span class="sxs-lookup"><span data-stu-id="d1db3-107"><a name="compare"></a>Cross-premises connectivity options</span></span>

<span data-ttu-id="d1db3-108">Caso você queira conectar seus sites locais com segurança a uma rede virtual, há três maneiras diferentes de fazer isso: Site a Site, Ponto a Site e o ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d1db3-108">If you want to connect your on-premises sites securely to a virtual network, you have three different ways to do so: Site-to-Site, Point-to-Site, and ExpressRoute.</span></span> <span data-ttu-id="d1db3-109">Compare as diferentes conexões entre locais que estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="d1db3-109">Compare the different cross-premises connections that are available.</span></span> <span data-ttu-id="d1db3-110">A opção escolhida pode depender de várias considerações, como:</span><span class="sxs-lookup"><span data-stu-id="d1db3-110">The option you choose can depend on various considerations, such as:</span></span>

* <span data-ttu-id="d1db3-111">Que tipo de taxa de transferência sua solução exige?</span><span class="sxs-lookup"><span data-stu-id="d1db3-111">What kind of throughput does your solution require?</span></span>
* <span data-ttu-id="d1db3-112">Você deseja se comunicar através da Internet pública por meio de VPN segura ou através de uma conexão privada?</span><span class="sxs-lookup"><span data-stu-id="d1db3-112">Do you want to communicate over the public Internet via secure VPN, or over a private connection?</span></span>
* <span data-ttu-id="d1db3-113">Você tem um endereço IP público disponível para uso?</span><span class="sxs-lookup"><span data-stu-id="d1db3-113">Do you have a public IP address available to use?</span></span>
* <span data-ttu-id="d1db3-114">Você planeja usar um dispositivo VPN?</span><span class="sxs-lookup"><span data-stu-id="d1db3-114">Are you planning to use a VPN device?</span></span> <span data-ttu-id="d1db3-115">Nesse caso, é compatível?</span><span class="sxs-lookup"><span data-stu-id="d1db3-115">If so, is it compatible?</span></span>
* <span data-ttu-id="d1db3-116">Você está conectando apenas alguns computadores ou deseja ter uma conexão persistente para o seu site?</span><span class="sxs-lookup"><span data-stu-id="d1db3-116">Are you connecting just a few computers, or do you want a persistent connection for your site?</span></span>
* <span data-ttu-id="d1db3-117">Qual tipo de gateway de VPN é necessário para a solução que você deseja criar?</span><span class="sxs-lookup"><span data-stu-id="d1db3-117">What type of VPN gateway is required for the solution you want to create?</span></span>
* <span data-ttu-id="d1db3-118">Qual SKU de gateway você deve usar?</span><span class="sxs-lookup"><span data-stu-id="d1db3-118">Which gateway SKU should you use?</span></span>

### <span data-ttu-id="d1db3-119"><a name="planningtable"></a>Tabela de planejamento</span><span class="sxs-lookup"><span data-stu-id="d1db3-119"><a name="planningtable"></a>Planning table</span></span>

<span data-ttu-id="d1db3-120">A tabela a seguir pode ajudá-lo a decidir a melhor opção de conectividade para sua solução.</span><span class="sxs-lookup"><span data-stu-id="d1db3-120">The following table can help you decide the best connectivity option for your solution.</span></span>

[!INCLUDE [vpn-gateway-cross-premises](../../includes/vpn-gateway-cross-premises-include.md)]

### <span data-ttu-id="d1db3-121"><a name="gwsku"></a>SKUs do Gateway</span><span class="sxs-lookup"><span data-stu-id="d1db3-121"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-table-gwtype-aggtput](../../includes/vpn-gateway-table-gwtype-aggtput-include.md)]

### <span data-ttu-id="d1db3-122"><a name="wf"></a>Fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="d1db3-122"><a name="wf"></a>Workflow</span></span>

<span data-ttu-id="d1db3-123">A lista a seguir descreve o fluxo de trabalho comum para conectividade de nuvem:</span><span class="sxs-lookup"><span data-stu-id="d1db3-123">The following list outlines the common workflow for cloud connectivity:</span></span>

1. <span data-ttu-id="d1db3-124">Projete e planeje sua topologia de conectividade e liste os espaços de endereço para todas as redes às quais você deseja se conectar.</span><span class="sxs-lookup"><span data-stu-id="d1db3-124">Design and plan your connectivity topology and list the address spaces for all networks you want to connect.</span></span>
2. <span data-ttu-id="d1db3-125">Crie uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1db3-125">Create an Azure virtual network.</span></span> 
3. <span data-ttu-id="d1db3-126">Criar um gateway de VPN para a rede virtual.</span><span class="sxs-lookup"><span data-stu-id="d1db3-126">Create a VPN gateway for the virtual network.</span></span>
4. <span data-ttu-id="d1db3-127">Crie e configure as conexões com redes locais ou outras redes virtuais (conforme necessário).</span><span class="sxs-lookup"><span data-stu-id="d1db3-127">Create and configure connections to on-premises networks or other virtual networks (as needed).</span></span>
5. <span data-ttu-id="d1db3-128">Crie e configure uma conexão Ponto a Site para o gateway de VPN do Azure (conforme necessário).</span><span class="sxs-lookup"><span data-stu-id="d1db3-128">Create and configure a Point-to-Site connection for your Azure VPN gateway (as needed).</span></span>

## <span data-ttu-id="d1db3-129"><a name="design"></a>Design</span><span class="sxs-lookup"><span data-stu-id="d1db3-129"><a name="design"></a>Design</span></span>
### <span data-ttu-id="d1db3-130"><a name="topologies"></a>Topologias de conexão</span><span class="sxs-lookup"><span data-stu-id="d1db3-130"><a name="topologies"></a>Connection topologies</span></span>

<span data-ttu-id="d1db3-131">Comece examinando os diagramas no artigo [Sobre o Gateway de VPN](vpn-gateway-about-vpngateways.md) .</span><span class="sxs-lookup"><span data-stu-id="d1db3-131">Start by looking at the diagrams in the [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span> <span data-ttu-id="d1db3-132">O artigo contém diagramas básicos, os modelos de implantação para cada topologia e as ferramentas de implantação disponíveis que você pode usar para implantar sua configuração.</span><span class="sxs-lookup"><span data-stu-id="d1db3-132">The article contains basic diagrams, the deployment models for each topology, and the available deployment tools you can use to deploy your configuration.</span></span>

### <span data-ttu-id="d1db3-133"><a name="designbasics"></a>Noções básicas sobre design</span><span class="sxs-lookup"><span data-stu-id="d1db3-133"><a name="designbasics"></a>Design basics</span></span>

<span data-ttu-id="d1db3-134">As seções a seguir tratam dos aspectos básicos do gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="d1db3-134">The following sections discuss the VPN gateway basics.</span></span> 

#### <span data-ttu-id="d1db3-135"><a name="servicelimits"></a>Limites dos serviços de rede</span><span class="sxs-lookup"><span data-stu-id="d1db3-135"><a name="servicelimits"></a>Networking services limits</span></span>

<span data-ttu-id="d1db3-136">Percorra as tabelas para exibir [limites de serviços de rede](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="d1db3-136">Scroll through the tables to view [networking services limits](../azure-subscription-service-limits.md#networking-limits).</span></span> <span data-ttu-id="d1db3-137">Os limites listados podem afetar o design.</span><span class="sxs-lookup"><span data-stu-id="d1db3-137">The limits listed may impact your design.</span></span>

#### <span data-ttu-id="d1db3-138"><a name="subnets"></a>Sobre sub-redes</span><span class="sxs-lookup"><span data-stu-id="d1db3-138"><a name="subnets"></a>About subnets</span></span>

<span data-ttu-id="d1db3-139">Quando estiver criando conexões, você precisa considerar os intervalos de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="d1db3-139">When you are creating connections, you must consider your subnet ranges.</span></span> <span data-ttu-id="d1db3-140">Não pode haver sobreposição dos intervalos de endereço de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="d1db3-140">You cannot have overlapping subnet address ranges.</span></span> <span data-ttu-id="d1db3-141">Uma sub-rede sobreposta ocorre quando uma rede virtual ou local contém o mesmo espaço de endereço que outro local.</span><span class="sxs-lookup"><span data-stu-id="d1db3-141">An overlapping subnet is when one virtual network or on-premises location contains the same address space that the other location contains.</span></span> <span data-ttu-id="d1db3-142">Isso significa que seus engenheiros de rede para redes locais deverão definir um intervalo para usar o espaço/sub-redes de endereçamento IP do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1db3-142">This means that you need your network engineers for your local on-premises networks to carve out a range for you to use for your Azure IP addressing space/subnets.</span></span> <span data-ttu-id="d1db3-143">Você precisa de um espaço de endereço que não esteja sendo usado na rede local.</span><span class="sxs-lookup"><span data-stu-id="d1db3-143">You need address space that is not being used on the local on-premises network.</span></span>

<span data-ttu-id="d1db3-144">Também é importante evitar a sobreposição de sub-redes quando você estiver trabalhando com conexões VNet a VNet.</span><span class="sxs-lookup"><span data-stu-id="d1db3-144">Avoiding overlapping subnets is also important when you are working with VNet-to-VNet connections.</span></span> <span data-ttu-id="d1db3-145">Se houver sobreposição das suas sub-redes e um endereço IP existir em ambas as VNets de envio e de destino, as conexões VNet a VNet falharão.</span><span class="sxs-lookup"><span data-stu-id="d1db3-145">If your subnets overlap and an IP address exists in both the sending and destination VNets, VNet-to-VNet connections fail.</span></span> <span data-ttu-id="d1db3-146">O Azure não poderá encaminhar os dados para a outra VNet porque o endereço de destino faz parte da VNet de envio.</span><span class="sxs-lookup"><span data-stu-id="d1db3-146">Azure can't route the data to the other VNet because the destination address is part of the sending VNet.</span></span>

<span data-ttu-id="d1db3-147">Os Gateways de VPN precisam de uma sub-rede específica, chamada sub-rede de gateway.</span><span class="sxs-lookup"><span data-stu-id="d1db3-147">VPN Gateways require a specific subnet called a gateway subnet.</span></span> <span data-ttu-id="d1db3-148">Todas as sub-redes de gateway devem ser nomeadas como GatewaySubnet para funcionar adequadamente.</span><span class="sxs-lookup"><span data-stu-id="d1db3-148">All gateway subnets must be named GatewaySubnet to work properly.</span></span> <span data-ttu-id="d1db3-149">Lembre-se de não pode nomear sua sub-rede de gateway com um nome diferente e não implantar VMs ou qualquer outra coisa para a sub-rede de gateway.</span><span class="sxs-lookup"><span data-stu-id="d1db3-149">Be sure not to name your gateway subnet a different name, and don't deploy VMs or anything else to the gateway subnet.</span></span> <span data-ttu-id="d1db3-150">Consulte [Sub-redes de gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span><span class="sxs-lookup"><span data-stu-id="d1db3-150">See [Gateway Subnets](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span></span>

#### <span data-ttu-id="d1db3-151"><a name="local"></a>Sobre gateways de rede local</span><span class="sxs-lookup"><span data-stu-id="d1db3-151"><a name="local"></a>About local network gateways</span></span>

<span data-ttu-id="d1db3-152">O gateway de rede local geralmente se refere ao seu local.</span><span class="sxs-lookup"><span data-stu-id="d1db3-152">The local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="d1db3-153">No modelo de implantação clássico, o gateway de rede local era conhecido como um Site da Rede Local.</span><span class="sxs-lookup"><span data-stu-id="d1db3-153">In the classic deployment model, the local network gateway is referred to as a Local Network Site.</span></span> <span data-ttu-id="d1db3-154">Quando configura um gateway de rede local, você lhe dá um nome, especifica o endereço IP público do dispositivo VPN local e especifica os prefixos de endereço que estão no caminho local.</span><span class="sxs-lookup"><span data-stu-id="d1db3-154">When you configure a local network gateway, you give it a name, specify the public IP address of the on-premises VPN device, and specify the address prefixes that are in the on-premises location.</span></span> <span data-ttu-id="d1db3-155">O Azure examina os prefixos de endereço de destino para o tráfego de rede, consulta a configuração que você especificou para o gateway de rede local e encaminha os pacotes adequadamente.</span><span class="sxs-lookup"><span data-stu-id="d1db3-155">Azure looks at the destination address prefixes for network traffic, consults the configuration that you have specified for the local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="d1db3-156">Você pode modificar os prefixos de endereço conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="d1db3-156">You can modify the address prefixes as needed.</span></span> <span data-ttu-id="d1db3-157">Para saber mais, confira [Gateways de rede local](vpn-gateway-about-vpn-gateway-settings.md#lng).</span><span class="sxs-lookup"><span data-stu-id="d1db3-157">For more information, see [Local network gateways](vpn-gateway-about-vpn-gateway-settings.md#lng).</span></span>

#### <span data-ttu-id="d1db3-158"><a name="gwtype"></a>Sobre tipos de gateway</span><span class="sxs-lookup"><span data-stu-id="d1db3-158"><a name="gwtype"></a>About gateway types</span></span>

<span data-ttu-id="d1db3-159">É crucial selecionar o tipo de gateway correto para sua topologia.</span><span class="sxs-lookup"><span data-stu-id="d1db3-159">Selecting the correct gateway type for your topology is critical.</span></span> <span data-ttu-id="d1db3-160">Se você selecionar o tipo incorreto, seu gateway não funcionará corretamente.</span><span class="sxs-lookup"><span data-stu-id="d1db3-160">If you select the wrong type, your gateway won't work properly.</span></span> <span data-ttu-id="d1db3-161">O tipo de gateway especifica como o próprio gateway se conecta e é uma definição de configuração necessária para o modelo de implantação do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="d1db3-161">The gateway type specifies how the gateway itself connects and is a required configuration setting for the Resource Manager deployment model.</span></span>

<span data-ttu-id="d1db3-162">Os tipos de gateway são:</span><span class="sxs-lookup"><span data-stu-id="d1db3-162">The gateway types are:</span></span>

* <span data-ttu-id="d1db3-163">Vpn</span><span class="sxs-lookup"><span data-stu-id="d1db3-163">Vpn</span></span>
* <span data-ttu-id="d1db3-164">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="d1db3-164">ExpressRoute</span></span>

#### <span data-ttu-id="d1db3-165"><a name="connectiontype"></a>Sobre tipos de conexão</span><span class="sxs-lookup"><span data-stu-id="d1db3-165"><a name="connectiontype"></a>About connection types</span></span>

<span data-ttu-id="d1db3-166">Cada configuração exige um tipo específico de conexão.</span><span class="sxs-lookup"><span data-stu-id="d1db3-166">Each configuration requires a specific connection type.</span></span> <span data-ttu-id="d1db3-167">Os tipos de conexão são:</span><span class="sxs-lookup"><span data-stu-id="d1db3-167">The connection types are:</span></span>

* <span data-ttu-id="d1db3-168">IPsec</span><span class="sxs-lookup"><span data-stu-id="d1db3-168">IPsec</span></span>
* <span data-ttu-id="d1db3-169">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="d1db3-169">Vnet2Vnet</span></span>
* <span data-ttu-id="d1db3-170">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="d1db3-170">ExpressRoute</span></span>
* <span data-ttu-id="d1db3-171">VPNClient</span><span class="sxs-lookup"><span data-stu-id="d1db3-171">VPNClient</span></span>

#### <span data-ttu-id="d1db3-172"><a name="vpntype"></a>Sobre tipos de VPN</span><span class="sxs-lookup"><span data-stu-id="d1db3-172"><a name="vpntype"></a>About VPN types</span></span>

<span data-ttu-id="d1db3-173">Cada configuração requer um tipo específico de VPN.</span><span class="sxs-lookup"><span data-stu-id="d1db3-173">Each configuration requires a specific VPN type.</span></span> <span data-ttu-id="d1db3-174">Se estiver combinando duas configurações, como a criação de uma conexão Site a Site e uma conexão Ponto a Site com a mesma rede virtual, você deverá usar um tipo VPN que atenda a ambos os requisitos de conexão.</span><span class="sxs-lookup"><span data-stu-id="d1db3-174">If you are combining two configurations, such as creating a Site-to-Site connection and a Point-to-Site connection to the same VNet, you must use a VPN type that satisfies both connection requirements.</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="d1db3-175">As tabelas a seguir mostram o tipo VPN conforme mapeado para cada configuração de conexão.</span><span class="sxs-lookup"><span data-stu-id="d1db3-175">The following tables show the VPN type as it maps to each connection configuration.</span></span> <span data-ttu-id="d1db3-176">Verifique se o tipo de VPN para o gateway corresponde à configuração que você deseja criar.</span><span class="sxs-lookup"><span data-stu-id="d1db3-176">Make sure the VPN type for your gateway matches the configuration that you want to create.</span></span> 

[!INCLUDE [vpn-gateway-table-vpntype](../../includes/vpn-gateway-table-vpntype-include.md)]

### <span data-ttu-id="d1db3-177"><a name="devices"></a>Dispositivos de VPN e conexões Site a Site</span><span class="sxs-lookup"><span data-stu-id="d1db3-177"><a name="devices"></a>VPN devices for Site-to-Site connections</span></span>

<span data-ttu-id="d1db3-178">Para configurar uma conexão Site a Site, independentemente do modelo de implantação, você precisará os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="d1db3-178">To configure a Site-to-Site connection, regardless of deployment model, you need the following items:</span></span>

* <span data-ttu-id="d1db3-179">Um dispositivo VPN que é compatível com os gateways de VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="d1db3-179">A VPN device that is compatible with Azure VPN gateways</span></span>
* <span data-ttu-id="d1db3-180">Um endereço IP IPv4 público que não está protegido por um NAT</span><span class="sxs-lookup"><span data-stu-id="d1db3-180">A public-facing IPv4 IP address that is not behind a NAT</span></span>

<span data-ttu-id="d1db3-181">Você precisa ter experiência para configurar seu dispositivo VPN ou pedir que alguém o configure para você.</span><span class="sxs-lookup"><span data-stu-id="d1db3-181">You need to have experience configuring your VPN device, or have someone that can configure the device for you.</span></span>

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <span data-ttu-id="d1db3-182"><a name="forcedtunnel"></a>Considere a possibilidade de roteamento de túnel forçado</span><span class="sxs-lookup"><span data-stu-id="d1db3-182"><a name="forcedtunnel"></a>Consider forced tunnel routing</span></span>

<span data-ttu-id="d1db3-183">Para a maioria das configurações, é possível configurar o túnel forçado.</span><span class="sxs-lookup"><span data-stu-id="d1db3-183">For most configurations, you can configure forced tunneling.</span></span> <span data-ttu-id="d1db3-184">O túnel forçado permite redirecionar ou "forçar" todo o tráfego direcionado para a Internet de volta para seu local por meio de um túnel VPN de Site a Site para inspeção e auditoria.</span><span class="sxs-lookup"><span data-stu-id="d1db3-184">Forced tunneling lets you redirect or "force" all Internet-bound traffic back to your on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="d1db3-185">Esse é um requisito crítico de segurança para a maioria das políticas de TI empresariais.</span><span class="sxs-lookup"><span data-stu-id="d1db3-185">This is a critical security requirement for most enterprise IT policies.</span></span> 

<span data-ttu-id="d1db3-186">Sem o túnel forçado, o tráfego direcionado para Internet de suas VMs no Azure sempre percorrerão da infraestrutura de rede do Azure diretamente para a Internet, sem a opção para permitir que você inspecione ou audite o tráfego.</span><span class="sxs-lookup"><span data-stu-id="d1db3-186">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out to the Internet, without the option to allow you to inspect or audit the traffic.</span></span> <span data-ttu-id="d1db3-187">O acesso não autorizado à Internet pode levar à divulgação de informações ou outros tipos de violações de segurança.</span><span class="sxs-lookup"><span data-stu-id="d1db3-187">Unauthorized Internet access can potentially lead to information disclosure or other types of security breaches.</span></span>

<span data-ttu-id="d1db3-188">Uma conexão de túnel forçado pode ser configurada em ambos os modelos de implantação e usando ferramentas diferentes.</span><span class="sxs-lookup"><span data-stu-id="d1db3-188">A forced tunneling connection can be configured in both deployment models and by using different tools.</span></span> <span data-ttu-id="d1db3-189">Para obter mais informações, consulte [Configurar o túnel forçado](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="d1db3-189">For more information, see [Configure forced tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>

<span data-ttu-id="d1db3-190">**Diagrama do túnel forçado**</span><span class="sxs-lookup"><span data-stu-id="d1db3-190">**Forced tunneling diagram**</span></span>

![Diagrama de túnel forçado do Gateway de VPN do Azure](./media/vpn-gateway-plan-design/forced-tunneling-diagram.png)

## <a name="next-steps"></a><span data-ttu-id="d1db3-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d1db3-192">Next steps</span></span>

<span data-ttu-id="d1db3-193">Consulte os artigos [Perguntas frequentes sobre o gateway de VPN](vpn-gateway-vpn-faq.md) e [Sobre gateways de VPN](vpn-gateway-about-vpngateways.md) para obter mais informações para ajudá-lo com seu design.</span><span class="sxs-lookup"><span data-stu-id="d1db3-193">See the [VPN Gateway FAQ](vpn-gateway-vpn-faq.md) and [About VPN Gateway](vpn-gateway-about-vpngateways.md) articles for more information to help you with your design.</span></span>

<span data-ttu-id="d1db3-194">Para obter mais informações sobre configurações de gateway específicas, consulte [Sobre as configurações de Gateway de VPN](vpn-gateway-about-vpn-gateway-settings.md).</span><span class="sxs-lookup"><span data-stu-id="d1db3-194">For more information about specific gateway settings, see [About VPN Gateway Settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>