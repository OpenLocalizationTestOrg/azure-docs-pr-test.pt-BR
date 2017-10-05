---
title: "Configurações de Gateway de VPN para conexões do Azure entre locais | Microsoft Docs"
description: "Saiba mais sobre as configurações do Gateway de VPN para gateways de rede virtual do Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: ae665bc5-0089-45d0-a0d5-bc0ab4e79899
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/26/2017
ms.author: cherylmc
ms.openlocfilehash: 07aa6946b9c3994c5afc5c88837f23567b95d8a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="about-vpn-gateway-configuration-settings"></a><span data-ttu-id="55c53-103">Sobre definições de configuração do Gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="55c53-103">About VPN Gateway configuration settings</span></span>

<span data-ttu-id="55c53-104">Um gateway de VPN é um tipo de gateway de rede virtual que envia o tráfego criptografado entre sua rede virtual e seu local em uma conexão pública.</span><span class="sxs-lookup"><span data-stu-id="55c53-104">A VPN gateway is a type of virtual network gateway that sends encrypted traffic between your virtual network and your on-premises location across a public connection.</span></span> <span data-ttu-id="55c53-105">Você também pode usar o Gateway de VPN para enviar o tráfego entre redes virtuais no backbone do Azure.</span><span class="sxs-lookup"><span data-stu-id="55c53-105">You can also use a VPN gateway to send traffic between virtual networks across the Azure backbone.</span></span>

<span data-ttu-id="55c53-106">Uma conexão de Gateway de VPN tem base na configuração de vários recursos, cada um deles contendo definições configuráveis.</span><span class="sxs-lookup"><span data-stu-id="55c53-106">A VPN gateway connection relies on the configuration of multiple resources, each of which contains configurable settings.</span></span> <span data-ttu-id="55c53-107">As seções neste artigo abordam os recursos e configurações relacionados a um gateway de VPN para uma rede virtual criada no modelo de implantação do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="55c53-107">The sections in this article discuss the resources and settings that relate to a VPN gateway for a virtual network created in Resource Manager deployment model.</span></span> <span data-ttu-id="55c53-108">Você pode encontrar descrições e diagramas da topologia para cada solução de conexão no artigo [Sobre o Gateway de VPN](vpn-gateway-about-vpngateways.md) .</span><span class="sxs-lookup"><span data-stu-id="55c53-108">You can find descriptions and topology diagrams for each connection solution in the [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span>

## <span data-ttu-id="55c53-109"><a name="gwtype"></a>Tipos de gateway</span><span class="sxs-lookup"><span data-stu-id="55c53-109"><a name="gwtype"></a>Gateway types</span></span>

<span data-ttu-id="55c53-110">Cada rede virtual pode ter apenas um gateway de rede virtual de cada tipo.</span><span class="sxs-lookup"><span data-stu-id="55c53-110">Each virtual network can only have one virtual network gateway of each type.</span></span> <span data-ttu-id="55c53-111">Quando estiver criando um gateway de rede virtual, você deve garantir que o tipo de gateway seja o correto para sua configuração.</span><span class="sxs-lookup"><span data-stu-id="55c53-111">When you are creating a virtual network gateway, you must make sure that the gateway type is correct for your configuration.</span></span>

<span data-ttu-id="55c53-112">Os valores disponíveis para o -GatewayType são:</span><span class="sxs-lookup"><span data-stu-id="55c53-112">The available values for -GatewayType are:</span></span>

* <span data-ttu-id="55c53-113">Vpn</span><span class="sxs-lookup"><span data-stu-id="55c53-113">Vpn</span></span>
* <span data-ttu-id="55c53-114">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="55c53-114">ExpressRoute</span></span>

<span data-ttu-id="55c53-115">Um gateway de VPN exige o `-GatewayType` *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="55c53-115">A VPN gateway requires the `-GatewayType` *Vpn*.</span></span>

<span data-ttu-id="55c53-116">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="55c53-116">Example:</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased
```

## <span data-ttu-id="55c53-117"><a name="gwsku"></a>SKUs do Gateway</span><span class="sxs-lookup"><span data-stu-id="55c53-117"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configure-the-gateway-sku"></a><span data-ttu-id="55c53-118">Configurar o SKU de gateway</span><span class="sxs-lookup"><span data-stu-id="55c53-118">Configure the gateway SKU</span></span>

#### <a name="azure-portal"></a><span data-ttu-id="55c53-119">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="55c53-119">Azure portal</span></span>

<span data-ttu-id="55c53-120">Se você usa o portal do Azure para criar um gateway de rede virtual do Resource Manager, é possível selecionar o SKU do gateway usando o menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="55c53-120">If you use the Azure portal to create a Resource Manager virtual network gateway, you can select the gateway SKU by using the dropdown.</span></span> <span data-ttu-id="55c53-121">As opções apresentadas correspondem ao tipo de Gateway e ao tipo de VPN que você selecionar.</span><span class="sxs-lookup"><span data-stu-id="55c53-121">The options you are presented with correspond to the Gateway type and VPN type that you select.</span></span>

#### <a name="powershell"></a><span data-ttu-id="55c53-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="55c53-122">PowerShell</span></span>

<span data-ttu-id="55c53-123">O exemplo do PowerShell a seguir especifica o `-GatewaySku` como VpnGw1.</span><span class="sxs-lookup"><span data-stu-id="55c53-123">The following PowerShell example specifies the `-GatewaySku` as VpnGw1.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1 `
-GatewayType Vpn -VpnType RouteBased
```

#### <span data-ttu-id="55c53-124"><a name="resize"></a>Alterar (redimensionar) uma SKU de gateway</span><span class="sxs-lookup"><span data-stu-id="55c53-124"><a name="resize"></a>Change (resize) a gateway SKU</span></span>

<span data-ttu-id="55c53-125">Se quiser atualizar seu SKU de gateway para um SKU mais avançado, use o cmdlet do PowerShell `Resize-AzureRmVirtualNetworkGateway`.</span><span class="sxs-lookup"><span data-stu-id="55c53-125">If you want to upgrade your gateway SKU to a more powerful SKU, you can use the `Resize-AzureRmVirtualNetworkGateway` PowerShell cmdlet.</span></span> <span data-ttu-id="55c53-126">Você também pode fazer o downgrade do tamanho do SKU de gateway usando esse cmdlet.</span><span class="sxs-lookup"><span data-stu-id="55c53-126">You can also downgrade the gateway SKU size using this cmdlet.</span></span>

<span data-ttu-id="55c53-127">O exemplo de PowerShell a seguir mostra um SKU de gateway sendo redimensionado para VpnGw2.</span><span class="sxs-lookup"><span data-stu-id="55c53-127">The following PowerShell example shows a gateway SKU being resized to VpnGw2.</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

## <span data-ttu-id="55c53-128"><a name="connectiontype"></a>Tipos de conexão</span><span class="sxs-lookup"><span data-stu-id="55c53-128"><a name="connectiontype"></a>Connection types</span></span>

<span data-ttu-id="55c53-129">No modelo de implantação do Resource Manager, cada configuração exige um tipo específico de conexão de gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="55c53-129">In the Resource Manager deployment model, each configuration requires a specific virtual network gateway connection type.</span></span> <span data-ttu-id="55c53-130">Os valores disponíveis do PowerShell do Gerenciador de Recursos para o `-ConnectionType` são:</span><span class="sxs-lookup"><span data-stu-id="55c53-130">The available Resource Manager PowerShell values for `-ConnectionType` are:</span></span>

* <span data-ttu-id="55c53-131">IPsec</span><span class="sxs-lookup"><span data-stu-id="55c53-131">IPsec</span></span>
* <span data-ttu-id="55c53-132">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="55c53-132">Vnet2Vnet</span></span>
* <span data-ttu-id="55c53-133">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="55c53-133">ExpressRoute</span></span>
* <span data-ttu-id="55c53-134">VPNClient</span><span class="sxs-lookup"><span data-stu-id="55c53-134">VPNClient</span></span>

<span data-ttu-id="55c53-135">No exemplo do PowerShell a seguir, criamos uma conexão S2S que exige o tipo de conexão *IPsec*.</span><span class="sxs-lookup"><span data-stu-id="55c53-135">In the following PowerShell example, we create a S2S connection that requires the connection type *IPsec*.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

## <span data-ttu-id="55c53-136"><a name="vpntype"></a>Tipos de VPN</span><span class="sxs-lookup"><span data-stu-id="55c53-136"><a name="vpntype"></a>VPN types</span></span>

<span data-ttu-id="55c53-137">Quando você cria o gateway de rede virtual para uma configuração de gateway de VPN, é preciso especificar um tipo de VPN.</span><span class="sxs-lookup"><span data-stu-id="55c53-137">When you create the virtual network gateway for a VPN gateway configuration, you must specify a VPN type.</span></span> <span data-ttu-id="55c53-138">O tipo de VPN que você escolhe depende da topologia de conexão que quer criar.</span><span class="sxs-lookup"><span data-stu-id="55c53-138">The VPN type that you choose depends on the connection topology that you want to create.</span></span> <span data-ttu-id="55c53-139">Por exemplo, uma conexão P2S requer um tipo de VPN RouteBased.</span><span class="sxs-lookup"><span data-stu-id="55c53-139">For example, a P2S connection requires a RouteBased VPN type.</span></span> <span data-ttu-id="55c53-140">Um tipo de VPN também pode depender do hardware que você usa.</span><span class="sxs-lookup"><span data-stu-id="55c53-140">A VPN type can also depend on the hardware that you are using.</span></span> <span data-ttu-id="55c53-141">As configurações S2S requerem um dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="55c53-141">S2S configurations require a VPN device.</span></span> <span data-ttu-id="55c53-142">Alguns dispositivos VPN recebem suporte apenas de um determinado tipo de VPN.</span><span class="sxs-lookup"><span data-stu-id="55c53-142">Some VPN devices only support a certain VPN type.</span></span>

<span data-ttu-id="55c53-143">O tipo de VPN que você escolher deve atender a todos os requisitos de conexão da solução que você quer criar.</span><span class="sxs-lookup"><span data-stu-id="55c53-143">The VPN type you select must satisfy all the connection requirements for the solution you want to create.</span></span> <span data-ttu-id="55c53-144">Por exemplo, se você quiser criar uma conexão de gateway de VPN S2S e uma conexão de gateway de VPN P2S para a mesma rede virtual, use o tipo de VPN *RouteBased* , pois P2S requer um tipo de VPN RouteBased.</span><span class="sxs-lookup"><span data-stu-id="55c53-144">For example, if you want to create a S2S VPN gateway connection and a P2S VPN gateway connection for the same virtual network, you would use VPN type *RouteBased* because P2S requires a RouteBased VPN type.</span></span> <span data-ttu-id="55c53-145">Você também precisa verificar se o seu dispositivo VPN é compatível com uma conexão VPN RouteBased.</span><span class="sxs-lookup"><span data-stu-id="55c53-145">You would also need to verify that your VPN device supported a RouteBased VPN connection.</span></span> 

<span data-ttu-id="55c53-146">Depois que um gateway de rede virtual é criado, não é possível alterar o tipo de VPN.</span><span class="sxs-lookup"><span data-stu-id="55c53-146">Once a virtual network gateway has been created, you can't change the VPN type.</span></span> <span data-ttu-id="55c53-147">Você precisa excluir o gateway de rede virtual e criar outro.</span><span class="sxs-lookup"><span data-stu-id="55c53-147">You have to delete the virtual network gateway and create a new one.</span></span> <span data-ttu-id="55c53-148">Há dois tipos de VPN:</span><span class="sxs-lookup"><span data-stu-id="55c53-148">There are two VPN types:</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="55c53-149">O exemplo do PowerShell a seguir especifica o `-VpnType` como *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="55c53-149">The following PowerShell example specifies the `-VpnType` as *RouteBased*.</span></span> <span data-ttu-id="55c53-150">Ao criar um gateway, você deve garantir que o -VpnType seja correto para sua configuração.</span><span class="sxs-lookup"><span data-stu-id="55c53-150">When you are creating a gateway, you must make sure that the -VpnType is correct for your configuration.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig `
-GatewayType Vpn -VpnType RouteBased
```

## <span data-ttu-id="55c53-151"><a name="requirements"></a>Requisitos do gateway</span><span class="sxs-lookup"><span data-stu-id="55c53-151"><a name="requirements"></a>Gateway requirements</span></span>

[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <span data-ttu-id="55c53-152"><a name="gwsub"></a>Sub-rede do gateway</span><span class="sxs-lookup"><span data-stu-id="55c53-152"><a name="gwsub"></a>Gateway subnet</span></span>

<span data-ttu-id="55c53-153">Antes de criar um gateway de VPN, crie uma sub-rede de gateway.</span><span class="sxs-lookup"><span data-stu-id="55c53-153">Before you create a VPN gateway, you must create a gateway subnet.</span></span> <span data-ttu-id="55c53-154">A sub-rede de gateway contém os endereços IP que as VMs do gateway de rede virtual e os serviços usam.</span><span class="sxs-lookup"><span data-stu-id="55c53-154">The gateway subnet contains the IP addresses that the virtual network gateway VMs and services use.</span></span> <span data-ttu-id="55c53-155">Quando você cria o gateway de rede virtual, as VMs de gateway são implantadas na sub-rede de gateway e definidas com as configurações necessárias de gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="55c53-155">When you create your virtual network gateway, gateway VMs are deployed to the gateway subnet and configured with the required VPN gateway settings.</span></span> <span data-ttu-id="55c53-156">Nunca implante qualquer outra coisa (por exemplo, VMs adicionais) na sub-rede de gateway.</span><span class="sxs-lookup"><span data-stu-id="55c53-156">You must never deploy anything else (for example, additional VMs) to the gateway subnet.</span></span> <span data-ttu-id="55c53-157">A sub-rede do gateway deve ser nomeada como GatewaySubnet para funcionar corretamente.</span><span class="sxs-lookup"><span data-stu-id="55c53-157">The gateway subnet must be named 'GatewaySubnet' to work properly.</span></span> <span data-ttu-id="55c53-158">Chamar a sub-rede de gateway de 'GatewaySubnet' permite que o Azure saiba que essa é a sub-rede para implantação nas VMs de gateway de rede virtual e nos serviços.</span><span class="sxs-lookup"><span data-stu-id="55c53-158">Naming the gateway subnet 'GatewaySubnet' lets Azure know that this is the subnet to deploy the virtual network gateway VMs and services to.</span></span>

<span data-ttu-id="55c53-159">Quando você cria a sub-rede de gateway, pode especificar o número de endereços IP que contém a sub-rede.</span><span class="sxs-lookup"><span data-stu-id="55c53-159">When you create the gateway subnet, you specify the number of IP addresses that the subnet contains.</span></span> <span data-ttu-id="55c53-160">Os endereços IP na sub-rede do gateway são alocados para as VMs de gateway e para os serviços de gateway.</span><span class="sxs-lookup"><span data-stu-id="55c53-160">The IP addresses in the gateway subnet are allocated to the gateway VMs and gateway services.</span></span> <span data-ttu-id="55c53-161">Algumas configurações exigem mais endereços IP do que outras.</span><span class="sxs-lookup"><span data-stu-id="55c53-161">Some configurations require more IP addresses than others.</span></span> <span data-ttu-id="55c53-162">Examine as instruções da configuração que você deseja criar e verifique se a sub-rede de gateway que você quer criar atende a esses requisitos.</span><span class="sxs-lookup"><span data-stu-id="55c53-162">Look at the instructions for the configuration that you want to create and verify that the gateway subnet you want to create meets those requirements.</span></span> <span data-ttu-id="55c53-163">Além disso, convém certificar-se de que sua sub-rede de gateway contenha endereços IP suficientes para acomodar possíveis configurações adicionais futuras.</span><span class="sxs-lookup"><span data-stu-id="55c53-163">Additionally, you may want to make sure your gateway subnet contains enough IP addresses to accommodate possible future additional configurations.</span></span> <span data-ttu-id="55c53-164">Embora seja possível criar uma sub-rede de gateway tão pequena quanto /29, é recomendável criar uma sub-rede de gateway de /28 ou maior (/28, /27, /26 etc.).</span><span class="sxs-lookup"><span data-stu-id="55c53-164">While you can create a gateway subnet as small as /29, we recommend that you create a gateway subnet of /28 or larger (/28, /27, /26 etc.).</span></span> <span data-ttu-id="55c53-165">Dessa forma, se você adicionar a funcionalidade no futuro, não precisará desfazer o gateway e excluir e recriar a sub-rede de gateway para permitir mais endereços IP.</span><span class="sxs-lookup"><span data-stu-id="55c53-165">That way, if you add functionality in the future, you won't have to tear your gateway, then delete and recreate the gateway subnet to allow for more IP addresses.</span></span>

<span data-ttu-id="55c53-166">O exemplo de PowerShell do Resource Manager a seguir mostra uma sub-rede de gateway chamada GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="55c53-166">The following Resource Manager PowerShell example shows a gateway subnet named GatewaySubnet.</span></span> <span data-ttu-id="55c53-167">Você pode ver que a notação CIDR especifica /27, que permite endereços IP suficientes para a maioria das configurações existentes no momento.</span><span class="sxs-lookup"><span data-stu-id="55c53-167">You can see the CIDR notation specifies a /27, which allows for enough IP addresses for most configurations that currently exist.</span></span>

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <span data-ttu-id="55c53-168"><a name="lng"></a>Gateways de rede locais</span><span class="sxs-lookup"><span data-stu-id="55c53-168"><a name="lng"></a>Local network gateways</span></span>

<span data-ttu-id="55c53-169">Ao criar uma configuração de gateway de VPN, o gateway de rede local geralmente representa sua localização no local.</span><span class="sxs-lookup"><span data-stu-id="55c53-169">When creating a VPN gateway configuration, the local network gateway often represents your on-premises location.</span></span> <span data-ttu-id="55c53-170">No modelo de implantação clássico, o gateway de rede local era conhecido como um Site Local.</span><span class="sxs-lookup"><span data-stu-id="55c53-170">In the classic deployment model, the local network gateway was referred to as a Local Site.</span></span> 

<span data-ttu-id="55c53-171">Você dá ao gateway de rede local um nome e o endereço IP público do dispositivo VPN local e especifica os prefixos de endereço que estão localizados no caminho local.</span><span class="sxs-lookup"><span data-stu-id="55c53-171">You give the local network gateway a name, the public IP address of the on-premises VPN device, and specify the address prefixes that are located on the on-premises location.</span></span> <span data-ttu-id="55c53-172">O Azure examina os prefixos de endereço de destino para o tráfego de rede, consulta a configuração que você especificou para o gateway de rede local e roteia os pacotes adequadamente.</span><span class="sxs-lookup"><span data-stu-id="55c53-172">Azure looks at the destination address prefixes for network traffic, consults the configuration that you have specified for your local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="55c53-173">Você também especifica os gateways de rede para configurações de rede virtual para rede virtual que usam uma conexão de gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="55c53-173">You also specify local network gateways for VNet-to-VNet configurations that use a VPN gateway connection.</span></span>

<span data-ttu-id="55c53-174">O seguinte exemplo de PowerShell cria um novo gateway de rede local:</span><span class="sxs-lookup"><span data-stu-id="55c53-174">The following PowerShell example creates a new local network gateway:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

<span data-ttu-id="55c53-175">Às vezes, você precisa modificar as configurações do gateway de rede local.</span><span class="sxs-lookup"><span data-stu-id="55c53-175">Sometimes you need to modify the local network gateway settings.</span></span> <span data-ttu-id="55c53-176">Por exemplo, quando você adicionar ou modificar o intervalo de endereços, ou se o endereço IP do dispositivo VPN mudar.</span><span class="sxs-lookup"><span data-stu-id="55c53-176">For example, when you add or modify the address range, or if the IP address of the VPN device changes.</span></span> <span data-ttu-id="55c53-177">Para uma rede virtual clássica, você pode alterar essas configurações no Portal Clássico na página Redes Locais.</span><span class="sxs-lookup"><span data-stu-id="55c53-177">For a classic VNet, you can change these settings in the classic portal on the Local Networks page.</span></span> <span data-ttu-id="55c53-178">Para o Resource Manager, confira [Modificar as configurações de gateway de rede local usando o PowerShell](vpn-gateway-modify-local-network-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="55c53-178">For Resource Manager, see [Modify local network gateway settings using PowerShell](vpn-gateway-modify-local-network-gateway.md).</span></span>

## <span data-ttu-id="55c53-179"><a name="resources"></a>Cmdlets do PowerShell e APIs REST</span><span class="sxs-lookup"><span data-stu-id="55c53-179"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>

<span data-ttu-id="55c53-180">Para obter recursos técnicos adicionais e requisitos de sintaxe específicos ao usar APIs REST, cmdlets do PowerShell na CLI do Azure para configurações do Gateway de VPN, veja as seguintes páginas:</span><span class="sxs-lookup"><span data-stu-id="55c53-180">For additional technical resources and specific syntax requirements when using REST APIs, PowerShell cmdlets, or Azure CLI for VPN Gateway configurations, see the following pages:</span></span>

| <span data-ttu-id="55c53-181">**Clássico**</span><span class="sxs-lookup"><span data-stu-id="55c53-181">**Classic**</span></span> | <span data-ttu-id="55c53-182">**Gerenciador de Recursos**</span><span class="sxs-lookup"><span data-stu-id="55c53-182">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="55c53-183">PowerShell</span><span class="sxs-lookup"><span data-stu-id="55c53-183">PowerShell</span></span>](/powershell/module/azure#networking) |[<span data-ttu-id="55c53-184">PowerShell</span><span class="sxs-lookup"><span data-stu-id="55c53-184">PowerShell</span></span>](/powershell/module/azurerm.network#vpn) |
| [<span data-ttu-id="55c53-185">API REST</span><span class="sxs-lookup"><span data-stu-id="55c53-185">REST API</span></span>](https://msdn.microsoft.com/library/jj154113) |[<span data-ttu-id="55c53-186">API REST</span><span class="sxs-lookup"><span data-stu-id="55c53-186">REST API</span></span>](/rest/api/network/virtualnetworkgateways) |
| <span data-ttu-id="55c53-187">Sem suporte</span><span class="sxs-lookup"><span data-stu-id="55c53-187">Not supported</span></span> | [<span data-ttu-id="55c53-188">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="55c53-188">Azure CLI</span></span>](/cli/azure/network/vnet-gateway)|

## <a name="next-steps"></a><span data-ttu-id="55c53-189">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="55c53-189">Next steps</span></span>

<span data-ttu-id="55c53-190">Para saber mais sobre as configurações de conexão disponíveis, confira [Sobre o Gateway de VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="55c53-190">For more information about available connection configurations, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>