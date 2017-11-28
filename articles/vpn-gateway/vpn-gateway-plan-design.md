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
ms.openlocfilehash: 3d4587ba31d163384212eca88a7e2c0ba8f3b21f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="planning-and-design-for-vpn-gateway"></a><span data-ttu-id="90340-103">Planejamento e design para o Gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="90340-103">Planning and design for VPN Gateway</span></span>

<span data-ttu-id="90340-104">Planejar e projetar suas conexões entre redes virtuais e entre locais pode ser simples ou complicado, dependendo das suas necessidades de rede.</span><span class="sxs-lookup"><span data-stu-id="90340-104">Planning and designing your cross-premises and VNet-to-VNet configurations can be either simple, or complicated, depending on your networking needs.</span></span> <span data-ttu-id="90340-105">Este artigo traz considerações básicas de design e planejamento.</span><span class="sxs-lookup"><span data-stu-id="90340-105">This article walks you through basic planning and design considerations.</span></span>

## <span data-ttu-id="90340-106"><a name="planning"></a>Planejamento</span><span class="sxs-lookup"><span data-stu-id="90340-106"><a name="planning"></a>Planning</span></span>

### <span data-ttu-id="90340-107"><a name="compare"></a>Opções de conectividade entre locais</span><span class="sxs-lookup"><span data-stu-id="90340-107"><a name="compare"></a>Cross-premises connectivity options</span></span>

<span data-ttu-id="90340-108">Se você quiser tooconnect local sites com segurança de rede virtual tooa, assim que toodo de três maneiras diferentes: Site a Site, ponto a Site e ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="90340-108">If you want tooconnect your on-premises sites securely tooa virtual network, you have three different ways toodo so: Site-to-Site, Point-to-Site, and ExpressRoute.</span></span> <span data-ttu-id="90340-109">Compare as conexões entre locais diferentes Olá disponíveis.</span><span class="sxs-lookup"><span data-stu-id="90340-109">Compare hello different cross-premises connections that are available.</span></span> <span data-ttu-id="90340-110">opção de saudação pode depender de várias considerações, como:</span><span class="sxs-lookup"><span data-stu-id="90340-110">hello option you choose can depend on various considerations, such as:</span></span>

* <span data-ttu-id="90340-111">Que tipo de taxa de transferência sua solução exige?</span><span class="sxs-lookup"><span data-stu-id="90340-111">What kind of throughput does your solution require?</span></span>
* <span data-ttu-id="90340-112">Você deseja toocommunicate sobre Olá Internet pública, por meio de VPN segura, ou em uma conexão privada?</span><span class="sxs-lookup"><span data-stu-id="90340-112">Do you want toocommunicate over hello public Internet via secure VPN, or over a private connection?</span></span>
* <span data-ttu-id="90340-113">Você tem um público toouse disponível de endereço IP?</span><span class="sxs-lookup"><span data-stu-id="90340-113">Do you have a public IP address available toouse?</span></span>
* <span data-ttu-id="90340-114">Você está planejando toouse um dispositivo VPN?</span><span class="sxs-lookup"><span data-stu-id="90340-114">Are you planning toouse a VPN device?</span></span> <span data-ttu-id="90340-115">Nesse caso, é compatível?</span><span class="sxs-lookup"><span data-stu-id="90340-115">If so, is it compatible?</span></span>
* <span data-ttu-id="90340-116">Você está conectando apenas alguns computadores ou deseja ter uma conexão persistente para o seu site?</span><span class="sxs-lookup"><span data-stu-id="90340-116">Are you connecting just a few computers, or do you want a persistent connection for your site?</span></span>
* <span data-ttu-id="90340-117">O tipo de gateway VPN é necessário para a solução de saudação deseja toocreate?</span><span class="sxs-lookup"><span data-stu-id="90340-117">What type of VPN gateway is required for hello solution you want toocreate?</span></span>
* <span data-ttu-id="90340-118">Qual SKU de gateway você deve usar?</span><span class="sxs-lookup"><span data-stu-id="90340-118">Which gateway SKU should you use?</span></span>

### <span data-ttu-id="90340-119"><a name="planningtable"></a>Tabela de planejamento</span><span class="sxs-lookup"><span data-stu-id="90340-119"><a name="planningtable"></a>Planning table</span></span>

<span data-ttu-id="90340-120">Olá a tabela a seguir pode ajudá-lo a decidir hello, a melhor opção de conectividade para sua solução.</span><span class="sxs-lookup"><span data-stu-id="90340-120">hello following table can help you decide hello best connectivity option for your solution.</span></span>

[!INCLUDE [vpn-gateway-cross-premises](../../includes/vpn-gateway-cross-premises-include.md)]

### <span data-ttu-id="90340-121"><a name="gwsku"></a>SKUs do Gateway</span><span class="sxs-lookup"><span data-stu-id="90340-121"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-table-gwtype-aggtput](../../includes/vpn-gateway-table-gwtype-aggtput-include.md)]

### <span data-ttu-id="90340-122"><a name="wf"></a>Fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="90340-122"><a name="wf"></a>Workflow</span></span>

<span data-ttu-id="90340-123">Olá lista a seguir descreve Olá fluxo de trabalho comuns de conectividade de nuvem:</span><span class="sxs-lookup"><span data-stu-id="90340-123">hello following list outlines hello common workflow for cloud connectivity:</span></span>

1. <span data-ttu-id="90340-124">Design e o plano de que seu endereço de saudação conectividade topologia e lista de espaços para todas as redes deseja tooconnect.</span><span class="sxs-lookup"><span data-stu-id="90340-124">Design and plan your connectivity topology and list hello address spaces for all networks you want tooconnect.</span></span>
2. <span data-ttu-id="90340-125">Crie uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="90340-125">Create an Azure virtual network.</span></span> 
3. <span data-ttu-id="90340-126">Crie um gateway VPN para rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="90340-126">Create a VPN gateway for hello virtual network.</span></span>
4. <span data-ttu-id="90340-127">Criar e configurar redes de tooon locais de conexões ou outras redes virtuais (conforme necessário).</span><span class="sxs-lookup"><span data-stu-id="90340-127">Create and configure connections tooon-premises networks or other virtual networks (as needed).</span></span>
5. <span data-ttu-id="90340-128">Crie e configure uma conexão Ponto a Site para o gateway de VPN do Azure (conforme necessário).</span><span class="sxs-lookup"><span data-stu-id="90340-128">Create and configure a Point-to-Site connection for your Azure VPN gateway (as needed).</span></span>

## <span data-ttu-id="90340-129"><a name="design"></a>Design</span><span class="sxs-lookup"><span data-stu-id="90340-129"><a name="design"></a>Design</span></span>
### <span data-ttu-id="90340-130"><a name="topologies"></a>Topologias de conexão</span><span class="sxs-lookup"><span data-stu-id="90340-130"><a name="topologies"></a>Connection topologies</span></span>

<span data-ttu-id="90340-131">Iniciar examinando diagramas Olá Olá [sobre o Gateway de VPN](vpn-gateway-about-vpngateways.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="90340-131">Start by looking at hello diagrams in hello [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span> <span data-ttu-id="90340-132">artigo Olá contém diagramas básicos, modelos de implantação de saudação para cada topologia, Olá disponíveis ferramentas de implantação e você pode usar toodeploy sua configuração.</span><span class="sxs-lookup"><span data-stu-id="90340-132">hello article contains basic diagrams, hello deployment models for each topology, and hello available deployment tools you can use toodeploy your configuration.</span></span>

### <span data-ttu-id="90340-133"><a name="designbasics"></a>Noções básicas sobre design</span><span class="sxs-lookup"><span data-stu-id="90340-133"><a name="designbasics"></a>Design basics</span></span>

<span data-ttu-id="90340-134">Olá seções a seguir discutem Noções básicas sobre o gateway VPN hello.</span><span class="sxs-lookup"><span data-stu-id="90340-134">hello following sections discuss hello VPN gateway basics.</span></span> 

#### <span data-ttu-id="90340-135"><a name="servicelimits"></a>Limites dos serviços de rede</span><span class="sxs-lookup"><span data-stu-id="90340-135"><a name="servicelimits"></a>Networking services limits</span></span>

<span data-ttu-id="90340-136">Percorra Olá tabelas tooview [limites de serviços de rede para](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="90340-136">Scroll through hello tables tooview [networking services limits](../azure-subscription-service-limits.md#networking-limits).</span></span> <span data-ttu-id="90340-137">limites de saudação listados podem afetar seu design.</span><span class="sxs-lookup"><span data-stu-id="90340-137">hello limits listed may impact your design.</span></span>

#### <span data-ttu-id="90340-138"><a name="subnets"></a>Sobre sub-redes</span><span class="sxs-lookup"><span data-stu-id="90340-138"><a name="subnets"></a>About subnets</span></span>

<span data-ttu-id="90340-139">Quando estiver criando conexões, você precisa considerar os intervalos de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="90340-139">When you are creating connections, you must consider your subnet ranges.</span></span> <span data-ttu-id="90340-140">Não pode haver sobreposição dos intervalos de endereço de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="90340-140">You cannot have overlapping subnet address ranges.</span></span> <span data-ttu-id="90340-141">Uma sub-rede sobreposta é quando um local de rede ou local virtual contém Olá contém mesmo espaço de endereço que Olá outro local.</span><span class="sxs-lookup"><span data-stu-id="90340-141">An overlapping subnet is when one virtual network or on-premises location contains hello same address space that hello other location contains.</span></span> <span data-ttu-id="90340-142">Isso significa que você precisa seus engenheiros de rede para sua toocarve de redes locais local um intervalo para você toouse para o IP do Azure/sub-redes de espaço de endereçamento.</span><span class="sxs-lookup"><span data-stu-id="90340-142">This means that you need your network engineers for your local on-premises networks toocarve out a range for you toouse for your Azure IP addressing space/subnets.</span></span> <span data-ttu-id="90340-143">É necessário espaço de endereço que não está sendo usado na rede do local no local de saudação.</span><span class="sxs-lookup"><span data-stu-id="90340-143">You need address space that is not being used on hello local on-premises network.</span></span>

<span data-ttu-id="90340-144">Também é importante evitar a sobreposição de sub-redes quando você estiver trabalhando com conexões VNet a VNet.</span><span class="sxs-lookup"><span data-stu-id="90340-144">Avoiding overlapping subnets is also important when you are working with VNet-to-VNet connections.</span></span> <span data-ttu-id="90340-145">Se a sobreposição de suas sub-redes e um endereço IP existe na enviando hello e o destino VNets, conexões de rede virtual a rede falharem.</span><span class="sxs-lookup"><span data-stu-id="90340-145">If your subnets overlap and an IP address exists in both hello sending and destination VNets, VNet-to-VNet connections fail.</span></span> <span data-ttu-id="90340-146">Azure não pode rotear Olá dados toohello outra VNet como endereço de destino Olá faz parte do hello envio de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="90340-146">Azure can't route hello data toohello other VNet because hello destination address is part of hello sending VNet.</span></span>

<span data-ttu-id="90340-147">Os Gateways de VPN precisam de uma sub-rede específica, chamada sub-rede de gateway.</span><span class="sxs-lookup"><span data-stu-id="90340-147">VPN Gateways require a specific subnet called a gateway subnet.</span></span> <span data-ttu-id="90340-148">Todas as sub-redes de gateway devem ser nomeadas GatewaySubnet toowork corretamente.</span><span class="sxs-lookup"><span data-stu-id="90340-148">All gateway subnets must be named GatewaySubnet toowork properly.</span></span> <span data-ttu-id="90340-149">Verifique se não tooname sua sub-rede de gateway outro nome e não implantar VMs ou qualquer outra transação sub-rede de gateway toohello.</span><span class="sxs-lookup"><span data-stu-id="90340-149">Be sure not tooname your gateway subnet a different name, and don't deploy VMs or anything else toohello gateway subnet.</span></span> <span data-ttu-id="90340-150">Consulte [Sub-redes de gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span><span class="sxs-lookup"><span data-stu-id="90340-150">See [Gateway Subnets](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span></span>

#### <span data-ttu-id="90340-151"><a name="local"></a>Sobre gateways de rede local</span><span class="sxs-lookup"><span data-stu-id="90340-151"><a name="local"></a>About local network gateways</span></span>

<span data-ttu-id="90340-152">Normalmente, o gateway de rede local Olá refere-se tooyour no local.</span><span class="sxs-lookup"><span data-stu-id="90340-152">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="90340-153">No modelo de implantação clássico hello, gateway de rede local Olá é chamado tooas um Site de rede Local.</span><span class="sxs-lookup"><span data-stu-id="90340-153">In hello classic deployment model, hello local network gateway is referred tooas a Local Network Site.</span></span> <span data-ttu-id="90340-154">Quando você configurar um gateway de rede local, dê a ele um nome, especifique o endereço IP público de saudação do dispositivo VPN local hello e especificar prefixos de endereço de saudação que estejam no local de local de saudação.</span><span class="sxs-lookup"><span data-stu-id="90340-154">When you configure a local network gateway, you give it a name, specify hello public IP address of hello on-premises VPN device, and specify hello address prefixes that are in hello on-premises location.</span></span> <span data-ttu-id="90340-155">Azure examina os prefixos de endereço de destino Olá para o tráfego de rede, consulta configuração Olá que você especificou para o gateway de rede local hello e encaminha pacotes adequadamente.</span><span class="sxs-lookup"><span data-stu-id="90340-155">Azure looks at hello destination address prefixes for network traffic, consults hello configuration that you have specified for hello local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="90340-156">Você pode modificar os prefixos de endereço Olá conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="90340-156">You can modify hello address prefixes as needed.</span></span> <span data-ttu-id="90340-157">Para saber mais, confira [Gateways de rede local](vpn-gateway-about-vpn-gateway-settings.md#lng).</span><span class="sxs-lookup"><span data-stu-id="90340-157">For more information, see [Local network gateways](vpn-gateway-about-vpn-gateway-settings.md#lng).</span></span>

#### <span data-ttu-id="90340-158"><a name="gwtype"></a>Sobre tipos de gateway</span><span class="sxs-lookup"><span data-stu-id="90340-158"><a name="gwtype"></a>About gateway types</span></span>

<span data-ttu-id="90340-159">Selecionar tipo de gateway correto Olá para a sua topologia é crítico.</span><span class="sxs-lookup"><span data-stu-id="90340-159">Selecting hello correct gateway type for your topology is critical.</span></span> <span data-ttu-id="90340-160">Se você selecionar o tipo errado Olá, o gateway não funcionará corretamente.</span><span class="sxs-lookup"><span data-stu-id="90340-160">If you select hello wrong type, your gateway won't work properly.</span></span> <span data-ttu-id="90340-161">tipo de gateway Olá Especifica como o próprio gateway Olá se conecta e é uma configuração necessária para o modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="90340-161">hello gateway type specifies how hello gateway itself connects and is a required configuration setting for hello Resource Manager deployment model.</span></span>

<span data-ttu-id="90340-162">tipos de gateway Olá são:</span><span class="sxs-lookup"><span data-stu-id="90340-162">hello gateway types are:</span></span>

* <span data-ttu-id="90340-163">Vpn</span><span class="sxs-lookup"><span data-stu-id="90340-163">Vpn</span></span>
* <span data-ttu-id="90340-164">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="90340-164">ExpressRoute</span></span>

#### <span data-ttu-id="90340-165"><a name="connectiontype"></a>Sobre tipos de conexão</span><span class="sxs-lookup"><span data-stu-id="90340-165"><a name="connectiontype"></a>About connection types</span></span>

<span data-ttu-id="90340-166">Cada configuração exige um tipo específico de conexão.</span><span class="sxs-lookup"><span data-stu-id="90340-166">Each configuration requires a specific connection type.</span></span> <span data-ttu-id="90340-167">tipos de conexão de saudação são:</span><span class="sxs-lookup"><span data-stu-id="90340-167">hello connection types are:</span></span>

* <span data-ttu-id="90340-168">IPsec</span><span class="sxs-lookup"><span data-stu-id="90340-168">IPsec</span></span>
* <span data-ttu-id="90340-169">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="90340-169">Vnet2Vnet</span></span>
* <span data-ttu-id="90340-170">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="90340-170">ExpressRoute</span></span>
* <span data-ttu-id="90340-171">VPNClient</span><span class="sxs-lookup"><span data-stu-id="90340-171">VPNClient</span></span>

#### <span data-ttu-id="90340-172"><a name="vpntype"></a>Sobre tipos de VPN</span><span class="sxs-lookup"><span data-stu-id="90340-172"><a name="vpntype"></a>About VPN types</span></span>

<span data-ttu-id="90340-173">Cada configuração requer um tipo específico de VPN.</span><span class="sxs-lookup"><span data-stu-id="90340-173">Each configuration requires a specific VPN type.</span></span> <span data-ttu-id="90340-174">Se você estiver combinando duas configurações, como a criação de uma conexão Site a Site e um toohello de conexão de ponto para Site mesma rede virtual, você deve usar um tipo VPN que atenda a ambos os requisitos de conexão.</span><span class="sxs-lookup"><span data-stu-id="90340-174">If you are combining two configurations, such as creating a Site-to-Site connection and a Point-to-Site connection toohello same VNet, you must use a VPN type that satisfies both connection requirements.</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="90340-175">Olá tabelas a seguir mostram o tipo de VPN hello como ele mapeia tooeach configuração de conexão.</span><span class="sxs-lookup"><span data-stu-id="90340-175">hello following tables show hello VPN type as it maps tooeach connection configuration.</span></span> <span data-ttu-id="90340-176">Verifique Olá-se de que tipo VPN para a sua configuração de saudação do gateway correspondências que você deseja toocreate.</span><span class="sxs-lookup"><span data-stu-id="90340-176">Make sure hello VPN type for your gateway matches hello configuration that you want toocreate.</span></span> 

[!INCLUDE [vpn-gateway-table-vpntype](../../includes/vpn-gateway-table-vpntype-include.md)]

### <span data-ttu-id="90340-177"><a name="devices"></a>Dispositivos de VPN e conexões Site a Site</span><span class="sxs-lookup"><span data-stu-id="90340-177"><a name="devices"></a>VPN devices for Site-to-Site connections</span></span>

<span data-ttu-id="90340-178">conexão tooconfigure uma Site a Site, independentemente do modelo de implantação, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="90340-178">tooconfigure a Site-to-Site connection, regardless of deployment model, you need hello following items:</span></span>

* <span data-ttu-id="90340-179">Um dispositivo VPN que é compatível com os gateways de VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="90340-179">A VPN device that is compatible with Azure VPN gateways</span></span>
* <span data-ttu-id="90340-180">Um endereço IP IPv4 público que não está protegido por um NAT</span><span class="sxs-lookup"><span data-stu-id="90340-180">A public-facing IPv4 IP address that is not behind a NAT</span></span>

<span data-ttu-id="90340-181">Você precisa de experiência toohave configurar seu dispositivo VPN ou que alguém que possa configurar dispositivo Olá para você.</span><span class="sxs-lookup"><span data-stu-id="90340-181">You need toohave experience configuring your VPN device, or have someone that can configure hello device for you.</span></span>

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <span data-ttu-id="90340-182"><a name="forcedtunnel"></a>Considere a possibilidade de roteamento de túnel forçado</span><span class="sxs-lookup"><span data-stu-id="90340-182"><a name="forcedtunnel"></a>Consider forced tunnel routing</span></span>

<span data-ttu-id="90340-183">Para a maioria das configurações, é possível configurar o túnel forçado.</span><span class="sxs-lookup"><span data-stu-id="90340-183">For most configurations, you can configure forced tunneling.</span></span> <span data-ttu-id="90340-184">Forçado permite redirecionar ou "forçar" todos os direcionado à Internet tráfego tooyour back local através de um túnel VPN Site a Site para inspeção e auditoria de túnel.</span><span class="sxs-lookup"><span data-stu-id="90340-184">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="90340-185">Esse é um requisito crítico de segurança para a maioria das políticas de TI empresariais.</span><span class="sxs-lookup"><span data-stu-id="90340-185">This is a critical security requirement for most enterprise IT policies.</span></span> 

<span data-ttu-id="90340-186">Sem o túnel forçado, o tráfego direcionado à Internet de suas VMs no Azure sempre percorrerá da infraestrutura de rede do Azure diretamente out toohello Internet, sem Olá opção tooallow você tráfego de saudação tooinspect ou auditoria.</span><span class="sxs-lookup"><span data-stu-id="90340-186">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="90340-187">Acesso não autorizado pode levar a divulgação de tooinformation ou outros tipos de violações de segurança.</span><span class="sxs-lookup"><span data-stu-id="90340-187">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

<span data-ttu-id="90340-188">Uma conexão de túnel forçado pode ser configurada em ambos os modelos de implantação e usando ferramentas diferentes.</span><span class="sxs-lookup"><span data-stu-id="90340-188">A forced tunneling connection can be configured in both deployment models and by using different tools.</span></span> <span data-ttu-id="90340-189">Para obter mais informações, consulte [Configurar o túnel forçado](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="90340-189">For more information, see [Configure forced tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>

<span data-ttu-id="90340-190">**Diagrama do túnel forçado**</span><span class="sxs-lookup"><span data-stu-id="90340-190">**Forced tunneling diagram**</span></span>

![Diagrama de túnel forçado do Gateway de VPN do Azure](./media/vpn-gateway-plan-design/forced-tunneling-diagram.png)

## <a name="next-steps"></a><span data-ttu-id="90340-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="90340-192">Next steps</span></span>

<span data-ttu-id="90340-193">Consulte Olá [perguntas frequentes sobre o Gateway de VPN](vpn-gateway-vpn-faq.md) e [sobre o Gateway de VPN](vpn-gateway-about-vpngateways.md) artigos para mais toohelp de informações você com seu design.</span><span class="sxs-lookup"><span data-stu-id="90340-193">See hello [VPN Gateway FAQ](vpn-gateway-vpn-faq.md) and [About VPN Gateway](vpn-gateway-about-vpngateways.md) articles for more information toohelp you with your design.</span></span>

<span data-ttu-id="90340-194">Para obter mais informações sobre configurações de gateway específicas, consulte [Sobre as configurações de Gateway de VPN](vpn-gateway-about-vpn-gateway-settings.md).</span><span class="sxs-lookup"><span data-stu-id="90340-194">For more information about specific gateway settings, see [About VPN Gateway Settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>