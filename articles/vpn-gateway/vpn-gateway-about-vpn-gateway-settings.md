---
title: "as configurações do gateway aaaVPN para conexões do Azure entre locais | Microsoft Docs"
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
ms.openlocfilehash: 01229d99fa37e30e00aa00f939f488d631b5593c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-gateway-configuration-settings"></a><span data-ttu-id="c2c72-103">Sobre definições de configuração do Gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="c2c72-103">About VPN Gateway configuration settings</span></span>

<span data-ttu-id="c2c72-104">Um gateway de VPN é um tipo de gateway de rede virtual que envia o tráfego criptografado entre sua rede virtual e seu local em uma conexão pública.</span><span class="sxs-lookup"><span data-stu-id="c2c72-104">A VPN gateway is a type of virtual network gateway that sends encrypted traffic between your virtual network and your on-premises location across a public connection.</span></span> <span data-ttu-id="c2c72-105">Você também pode usar um tráfego de toosend do gateway VPN entre redes virtuais em Olá backbone do Azure.</span><span class="sxs-lookup"><span data-stu-id="c2c72-105">You can also use a VPN gateway toosend traffic between virtual networks across hello Azure backbone.</span></span>

<span data-ttu-id="c2c72-106">Uma conexão de gateway VPN depende da configuração de saudação de vários recursos, cada uma delas contém as definições configuráveis.</span><span class="sxs-lookup"><span data-stu-id="c2c72-106">A VPN gateway connection relies on hello configuration of multiple resources, each of which contains configurable settings.</span></span> <span data-ttu-id="c2c72-107">seções neste artigo Olá abordam recursos hello e as configurações relacionadas tooa gateway VPN para uma rede virtual criada no modelo de implantação do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="c2c72-107">hello sections in this article discuss hello resources and settings that relate tooa VPN gateway for a virtual network created in Resource Manager deployment model.</span></span> <span data-ttu-id="c2c72-108">Você pode encontrar descrições e diagramas de topologia para cada solução de conexão do hello [sobre o Gateway de VPN](vpn-gateway-about-vpngateways.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="c2c72-108">You can find descriptions and topology diagrams for each connection solution in hello [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span>

## <span data-ttu-id="c2c72-109"><a name="gwtype"></a>Tipos de gateway</span><span class="sxs-lookup"><span data-stu-id="c2c72-109"><a name="gwtype"></a>Gateway types</span></span>

<span data-ttu-id="c2c72-110">Cada rede virtual pode ter apenas um gateway de rede virtual de cada tipo.</span><span class="sxs-lookup"><span data-stu-id="c2c72-110">Each virtual network can only have one virtual network gateway of each type.</span></span> <span data-ttu-id="c2c72-111">Quando você estiver criando um gateway de rede virtual, você deve se certificar que o tipo de gateway de Olá está correto para sua configuração.</span><span class="sxs-lookup"><span data-stu-id="c2c72-111">When you are creating a virtual network gateway, you must make sure that hello gateway type is correct for your configuration.</span></span>

<span data-ttu-id="c2c72-112">Olá - GatewayType em valores disponíveis é:</span><span class="sxs-lookup"><span data-stu-id="c2c72-112">hello available values for -GatewayType are:</span></span>

* <span data-ttu-id="c2c72-113">Vpn</span><span class="sxs-lookup"><span data-stu-id="c2c72-113">Vpn</span></span>
* <span data-ttu-id="c2c72-114">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c2c72-114">ExpressRoute</span></span>

<span data-ttu-id="c2c72-115">Um gateway de VPN requer Olá `-GatewayType` *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="c2c72-115">A VPN gateway requires hello `-GatewayType` *Vpn*.</span></span>

<span data-ttu-id="c2c72-116">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c2c72-116">Example:</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased
```

## <span data-ttu-id="c2c72-117"><a name="gwsku"></a>SKUs do Gateway</span><span class="sxs-lookup"><span data-stu-id="c2c72-117"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configure-hello-gateway-sku"></a><span data-ttu-id="c2c72-118">Configurar o gateway de saudação SKU</span><span class="sxs-lookup"><span data-stu-id="c2c72-118">Configure hello gateway SKU</span></span>

#### <a name="azure-portal"></a><span data-ttu-id="c2c72-119">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c2c72-119">Azure portal</span></span>

<span data-ttu-id="c2c72-120">Se você usar Olá toocreate portal do Azure um gateway de rede virtual do Gerenciador de recursos, você pode selecionar o SKU do gateway hello usando o menu suspenso de saudação.</span><span class="sxs-lookup"><span data-stu-id="c2c72-120">If you use hello Azure portal toocreate a Resource Manager virtual network gateway, you can select hello gateway SKU by using hello dropdown.</span></span> <span data-ttu-id="c2c72-121">Opções de saudação que são apresentadas correspondem toohello tipo de Gateway e o tipo VPN que você selecionar.</span><span class="sxs-lookup"><span data-stu-id="c2c72-121">hello options you are presented with correspond toohello Gateway type and VPN type that you select.</span></span>

#### <a name="powershell"></a><span data-ttu-id="c2c72-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2c72-122">PowerShell</span></span>

<span data-ttu-id="c2c72-123">exemplo a seguir do PowerShell Hello Especifica Olá `-GatewaySku` como VpnGw1.</span><span class="sxs-lookup"><span data-stu-id="c2c72-123">hello following PowerShell example specifies hello `-GatewaySku` as VpnGw1.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1 `
-GatewayType Vpn -VpnType RouteBased
```

#### <span data-ttu-id="c2c72-124"><a name="resize"></a>Alterar (redimensionar) uma SKU de gateway</span><span class="sxs-lookup"><span data-stu-id="c2c72-124"><a name="resize"></a>Change (resize) a gateway SKU</span></span>

<span data-ttu-id="c2c72-125">Se você quiser que sua tooa SKU de gateway tooupgrade SKU mais avançado, você pode usar o hello `Resize-AzureRmVirtualNetworkGateway` cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2c72-125">If you want tooupgrade your gateway SKU tooa more powerful SKU, you can use hello `Resize-AzureRmVirtualNetworkGateway` PowerShell cmdlet.</span></span> <span data-ttu-id="c2c72-126">Você também pode fazer o downgrade de tamanho SKU de gateway hello usando este cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c2c72-126">You can also downgrade hello gateway SKU size using this cmdlet.</span></span>

<span data-ttu-id="c2c72-127">Olá PowerShell de exemplo a seguir mostra que um SKU de gateway, que está sendo redimensionada tooVpnGw2.</span><span class="sxs-lookup"><span data-stu-id="c2c72-127">hello following PowerShell example shows a gateway SKU being resized tooVpnGw2.</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

## <span data-ttu-id="c2c72-128"><a name="connectiontype"></a>Tipos de conexão</span><span class="sxs-lookup"><span data-stu-id="c2c72-128"><a name="connectiontype"></a>Connection types</span></span>

<span data-ttu-id="c2c72-129">No modelo de implantação do Gerenciador de recursos de hello, cada configuração requer um tipo de conexão de gateway de rede virtual específica.</span><span class="sxs-lookup"><span data-stu-id="c2c72-129">In hello Resource Manager deployment model, each configuration requires a specific virtual network gateway connection type.</span></span> <span data-ttu-id="c2c72-130">Olá disponíveis do Gerenciador de recursos do PowerShell valores para `-ConnectionType` são:</span><span class="sxs-lookup"><span data-stu-id="c2c72-130">hello available Resource Manager PowerShell values for `-ConnectionType` are:</span></span>

* <span data-ttu-id="c2c72-131">IPsec</span><span class="sxs-lookup"><span data-stu-id="c2c72-131">IPsec</span></span>
* <span data-ttu-id="c2c72-132">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="c2c72-132">Vnet2Vnet</span></span>
* <span data-ttu-id="c2c72-133">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c2c72-133">ExpressRoute</span></span>
* <span data-ttu-id="c2c72-134">VPNClient</span><span class="sxs-lookup"><span data-stu-id="c2c72-134">VPNClient</span></span>

<span data-ttu-id="c2c72-135">Olá PowerShell de exemplo a seguir, criamos uma conexão S2S que requer o tipo de conexão Olá *IPsec*.</span><span class="sxs-lookup"><span data-stu-id="c2c72-135">In hello following PowerShell example, we create a S2S connection that requires hello connection type *IPsec*.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

## <span data-ttu-id="c2c72-136"><a name="vpntype"></a>Tipos de VPN</span><span class="sxs-lookup"><span data-stu-id="c2c72-136"><a name="vpntype"></a>VPN types</span></span>

<span data-ttu-id="c2c72-137">Quando você cria um gateway de rede virtual Olá para uma configuração de gateway VPN, você deve especificar um tipo VPN.</span><span class="sxs-lookup"><span data-stu-id="c2c72-137">When you create hello virtual network gateway for a VPN gateway configuration, you must specify a VPN type.</span></span> <span data-ttu-id="c2c72-138">Olá tipo VPN que você escolher depende de topologia de conexão de saudação que você deseja toocreate.</span><span class="sxs-lookup"><span data-stu-id="c2c72-138">hello VPN type that you choose depends on hello connection topology that you want toocreate.</span></span> <span data-ttu-id="c2c72-139">Por exemplo, uma conexão P2S requer um tipo de VPN RouteBased.</span><span class="sxs-lookup"><span data-stu-id="c2c72-139">For example, a P2S connection requires a RouteBased VPN type.</span></span> <span data-ttu-id="c2c72-140">Um tipo VPN também pode depender de hardware Olá que você está usando.</span><span class="sxs-lookup"><span data-stu-id="c2c72-140">A VPN type can also depend on hello hardware that you are using.</span></span> <span data-ttu-id="c2c72-141">As configurações S2S requerem um dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="c2c72-141">S2S configurations require a VPN device.</span></span> <span data-ttu-id="c2c72-142">Alguns dispositivos VPN recebem suporte apenas de um determinado tipo de VPN.</span><span class="sxs-lookup"><span data-stu-id="c2c72-142">Some VPN devices only support a certain VPN type.</span></span>

<span data-ttu-id="c2c72-143">Olá tipo VPN que você selecionar deve satisfazer todos os requisitos de conexão Olá para solução de saudação que deseja toocreate.</span><span class="sxs-lookup"><span data-stu-id="c2c72-143">hello VPN type you select must satisfy all hello connection requirements for hello solution you want toocreate.</span></span> <span data-ttu-id="c2c72-144">Por exemplo, se você quiser toocreate Olá uma conexão de gateway de VPN S2S e uma conexão de gateway VPN de P2S para a mesma rede virtual, você usaria o tipo de VPN *RouteBased* porque P2S requer um tipo RouteBased VPN.</span><span class="sxs-lookup"><span data-stu-id="c2c72-144">For example, if you want toocreate a S2S VPN gateway connection and a P2S VPN gateway connection for hello same virtual network, you would use VPN type *RouteBased* because P2S requires a RouteBased VPN type.</span></span> <span data-ttu-id="c2c72-145">Também é necessário que o dispositivo VPN com suporte a uma conexão VPN RouteBased de tooverify.</span><span class="sxs-lookup"><span data-stu-id="c2c72-145">You would also need tooverify that your VPN device supported a RouteBased VPN connection.</span></span> 

<span data-ttu-id="c2c72-146">Quando um gateway de rede virtual tiver sido criado, você não pode alterar o tipo VPN hello.</span><span class="sxs-lookup"><span data-stu-id="c2c72-146">Once a virtual network gateway has been created, you can't change hello VPN type.</span></span> <span data-ttu-id="c2c72-147">Você tem toodelete Olá gateway de rede virtual e criar um novo.</span><span class="sxs-lookup"><span data-stu-id="c2c72-147">You have toodelete hello virtual network gateway and create a new one.</span></span> <span data-ttu-id="c2c72-148">Há dois tipos de VPN:</span><span class="sxs-lookup"><span data-stu-id="c2c72-148">There are two VPN types:</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="c2c72-149">exemplo a seguir do PowerShell Hello Especifica Olá `-VpnType` como *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="c2c72-149">hello following PowerShell example specifies hello `-VpnType` as *RouteBased*.</span></span> <span data-ttu-id="c2c72-150">Quando você estiver criando um gateway, você deve garantir que Olá - VpnType está correto para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="c2c72-150">When you are creating a gateway, you must make sure that hello -VpnType is correct for your configuration.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig `
-GatewayType Vpn -VpnType RouteBased
```

## <span data-ttu-id="c2c72-151"><a name="requirements"></a>Requisitos do gateway</span><span class="sxs-lookup"><span data-stu-id="c2c72-151"><a name="requirements"></a>Gateway requirements</span></span>

[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <span data-ttu-id="c2c72-152"><a name="gwsub"></a>Sub-rede do gateway</span><span class="sxs-lookup"><span data-stu-id="c2c72-152"><a name="gwsub"></a>Gateway subnet</span></span>

<span data-ttu-id="c2c72-153">Antes de criar um gateway de VPN, crie uma sub-rede de gateway.</span><span class="sxs-lookup"><span data-stu-id="c2c72-153">Before you create a VPN gateway, you must create a gateway subnet.</span></span> <span data-ttu-id="c2c72-154">sub-rede de gateway Olá contém endereços IP hello esse gateway de rede virtual Olá VMs e serviços usam.</span><span class="sxs-lookup"><span data-stu-id="c2c72-154">hello gateway subnet contains hello IP addresses that hello virtual network gateway VMs and services use.</span></span> <span data-ttu-id="c2c72-155">Quando você criar o gateway de rede virtual, gateway VMs são sub-rede do gateway toohello implantado e configurado com as configurações de gateway VPN Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="c2c72-155">When you create your virtual network gateway, gateway VMs are deployed toohello gateway subnet and configured with hello required VPN gateway settings.</span></span> <span data-ttu-id="c2c72-156">Você nunca deve implantar a sub-rede de gateway toohello qualquer outra transação (por exemplo, VMs adicionais).</span><span class="sxs-lookup"><span data-stu-id="c2c72-156">You must never deploy anything else (for example, additional VMs) toohello gateway subnet.</span></span> <span data-ttu-id="c2c72-157">sub-rede de gateway Olá deve ser nomeado 'GatewaySubnet' toowork corretamente.</span><span class="sxs-lookup"><span data-stu-id="c2c72-157">hello gateway subnet must be named 'GatewaySubnet' toowork properly.</span></span> <span data-ttu-id="c2c72-158">Azure nomenclatura sub-rede de gateway Olá 'GatewaySubnet' permite saber que este é o gateway de rede virtual Olá sub-rede toodeploy Olá VMs e serviços.</span><span class="sxs-lookup"><span data-stu-id="c2c72-158">Naming hello gateway subnet 'GatewaySubnet' lets Azure know that this is hello subnet toodeploy hello virtual network gateway VMs and services to.</span></span>

<span data-ttu-id="c2c72-159">Quando você cria a sub-rede de gateway hello, você especificar Olá número de endereços IP que Olá sub-rede contém.</span><span class="sxs-lookup"><span data-stu-id="c2c72-159">When you create hello gateway subnet, you specify hello number of IP addresses that hello subnet contains.</span></span> <span data-ttu-id="c2c72-160">endereços IP de saudação na sub-rede de gateway Olá são toohello alocado gateway VMs e serviços de gateway.</span><span class="sxs-lookup"><span data-stu-id="c2c72-160">hello IP addresses in hello gateway subnet are allocated toohello gateway VMs and gateway services.</span></span> <span data-ttu-id="c2c72-161">Algumas configurações exigem mais endereços IP do que outras.</span><span class="sxs-lookup"><span data-stu-id="c2c72-161">Some configurations require more IP addresses than others.</span></span> <span data-ttu-id="c2c72-162">Examinar as instruções de saudação para Olá a configuração que você deseja toocreate e verifique a sub-rede de gateway que Olá deseja toocreate atende a esses requisitos.</span><span class="sxs-lookup"><span data-stu-id="c2c72-162">Look at hello instructions for hello configuration that you want toocreate and verify that hello gateway subnet you want toocreate meets those requirements.</span></span> <span data-ttu-id="c2c72-163">Além disso, talvez você queira toomake-se de que sua sub-rede de gateway contém suficiente IP endereços tooaccommodate possíveis futuras configurações adicionais.</span><span class="sxs-lookup"><span data-stu-id="c2c72-163">Additionally, you may want toomake sure your gateway subnet contains enough IP addresses tooaccommodate possible future additional configurations.</span></span> <span data-ttu-id="c2c72-164">Embora seja possível criar uma sub-rede de gateway tão pequena quanto /29, é recomendável criar uma sub-rede de gateway de /28 ou maior (/28, /27, /26 etc.).</span><span class="sxs-lookup"><span data-stu-id="c2c72-164">While you can create a gateway subnet as small as /29, we recommend that you create a gateway subnet of /28 or larger (/28, /27, /26 etc.).</span></span> <span data-ttu-id="c2c72-165">Dessa forma, se você adicionar funcionalidade de saudação futura, você não ter tootear seu gateway, em seguida, exclua e recrie Olá tooallow de sub-rede de gateway de mais endereços IP.</span><span class="sxs-lookup"><span data-stu-id="c2c72-165">That way, if you add functionality in hello future, you won't have tootear your gateway, then delete and recreate hello gateway subnet tooallow for more IP addresses.</span></span>

<span data-ttu-id="c2c72-166">Olá, exemplo do PowerShell do Gerenciador de recursos a seguir mostra uma sub-rede de gateway denominada GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="c2c72-166">hello following Resource Manager PowerShell example shows a gateway subnet named GatewaySubnet.</span></span> <span data-ttu-id="c2c72-167">Você pode ver a notação CIDR Olá Especifica um /27, que permite endereços IP suficientes para a maioria das configurações existentes no momento.</span><span class="sxs-lookup"><span data-stu-id="c2c72-167">You can see hello CIDR notation specifies a /27, which allows for enough IP addresses for most configurations that currently exist.</span></span>

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <span data-ttu-id="c2c72-168"><a name="lng"></a>Gateways de rede locais</span><span class="sxs-lookup"><span data-stu-id="c2c72-168"><a name="lng"></a>Local network gateways</span></span>

<span data-ttu-id="c2c72-169">Ao criar uma configuração de gateway VPN, o gateway de rede local Olá geralmente representa sua localização no local.</span><span class="sxs-lookup"><span data-stu-id="c2c72-169">When creating a VPN gateway configuration, hello local network gateway often represents your on-premises location.</span></span> <span data-ttu-id="c2c72-170">No modelo de implantação clássico hello, gateway de rede local Olá foi chamado tooas um Site Local.</span><span class="sxs-lookup"><span data-stu-id="c2c72-170">In hello classic deployment model, hello local network gateway was referred tooas a Local Site.</span></span> 

<span data-ttu-id="c2c72-171">Dê um nome de gateway de rede local hello, Olá endereço IP público do dispositivo VPN local hello e especificar prefixos de endereço de saudação que estão localizados em Olá no local.</span><span class="sxs-lookup"><span data-stu-id="c2c72-171">You give hello local network gateway a name, hello public IP address of hello on-premises VPN device, and specify hello address prefixes that are located on hello on-premises location.</span></span> <span data-ttu-id="c2c72-172">Azure examina os prefixos de endereço de destino Olá para o tráfego de rede, consulta configuração Olá que você especificou para o gateway de rede local e encaminha pacotes adequadamente.</span><span class="sxs-lookup"><span data-stu-id="c2c72-172">Azure looks at hello destination address prefixes for network traffic, consults hello configuration that you have specified for your local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="c2c72-173">Você também especifica os gateways de rede para configurações de rede virtual para rede virtual que usam uma conexão de gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="c2c72-173">You also specify local network gateways for VNet-to-VNet configurations that use a VPN gateway connection.</span></span>

<span data-ttu-id="c2c72-174">Olá PowerShell de exemplo a seguir cria um novo gateway de rede local:</span><span class="sxs-lookup"><span data-stu-id="c2c72-174">hello following PowerShell example creates a new local network gateway:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

<span data-ttu-id="c2c72-175">Às vezes você precisa de configurações de gateway de rede local toomodify hello.</span><span class="sxs-lookup"><span data-stu-id="c2c72-175">Sometimes you need toomodify hello local network gateway settings.</span></span> <span data-ttu-id="c2c72-176">Por exemplo, quando você adiciona ou modificar o intervalo de endereços hello, ou se o endereço IP de saudação do dispositivo VPN Olá mudar.</span><span class="sxs-lookup"><span data-stu-id="c2c72-176">For example, when you add or modify hello address range, or if hello IP address of hello VPN device changes.</span></span> <span data-ttu-id="c2c72-177">Para uma rede virtual clássica, você pode alterar essas configurações no portal clássico do hello na página de redes locais hello.</span><span class="sxs-lookup"><span data-stu-id="c2c72-177">For a classic VNet, you can change these settings in hello classic portal on hello Local Networks page.</span></span> <span data-ttu-id="c2c72-178">Para o Resource Manager, confira [Modificar as configurações de gateway de rede local usando o PowerShell](vpn-gateway-modify-local-network-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="c2c72-178">For Resource Manager, see [Modify local network gateway settings using PowerShell](vpn-gateway-modify-local-network-gateway.md).</span></span>

## <span data-ttu-id="c2c72-179"><a name="resources"></a>Cmdlets do PowerShell e APIs REST</span><span class="sxs-lookup"><span data-stu-id="c2c72-179"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>

<span data-ttu-id="c2c72-180">Para obter recursos técnicos adicionais e requisitos de sintaxe específica ao usar APIs REST, os cmdlets do PowerShell ou CLI do Azure para configurações de Gateway de VPN, consulte Olá páginas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c2c72-180">For additional technical resources and specific syntax requirements when using REST APIs, PowerShell cmdlets, or Azure CLI for VPN Gateway configurations, see hello following pages:</span></span>

| <span data-ttu-id="c2c72-181">**Clássico**</span><span class="sxs-lookup"><span data-stu-id="c2c72-181">**Classic**</span></span> | <span data-ttu-id="c2c72-182">**Gerenciador de Recursos**</span><span class="sxs-lookup"><span data-stu-id="c2c72-182">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="c2c72-183">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2c72-183">PowerShell</span></span>](/powershell/module/azure#networking) |[<span data-ttu-id="c2c72-184">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2c72-184">PowerShell</span></span>](/powershell/module/azurerm.network#vpn) |
| [<span data-ttu-id="c2c72-185">API REST</span><span class="sxs-lookup"><span data-stu-id="c2c72-185">REST API</span></span>](https://msdn.microsoft.com/library/jj154113) |[<span data-ttu-id="c2c72-186">API REST</span><span class="sxs-lookup"><span data-stu-id="c2c72-186">REST API</span></span>](/rest/api/network/virtualnetworkgateways) |
| <span data-ttu-id="c2c72-187">Sem suporte</span><span class="sxs-lookup"><span data-stu-id="c2c72-187">Not supported</span></span> | [<span data-ttu-id="c2c72-188">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="c2c72-188">Azure CLI</span></span>](/cli/azure/network/vnet-gateway)|

## <a name="next-steps"></a><span data-ttu-id="c2c72-189">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c2c72-189">Next steps</span></span>

<span data-ttu-id="c2c72-190">Para saber mais sobre as configurações de conexão disponíveis, confira [Sobre o Gateway de VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="c2c72-190">For more information about available connection configurations, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>