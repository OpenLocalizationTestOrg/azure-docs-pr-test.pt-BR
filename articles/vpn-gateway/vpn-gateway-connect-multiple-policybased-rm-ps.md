---
title: "Conectar gateways VPN do Azure a vários dispositivos VPN com base em políticas locais: Azure Resource Manager: PowerShell | Microsoft Docs"
description: "Este artigo orienta você pela configuração do gateway de VPN com base em rotas do Azure para vários dispositivos VPN com base em políticas usando o Azure Resource Manager e o PowerShell."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/27/2017
ms.author: yushwang
ms.openlocfilehash: 17211379ec61891982a02efca6730ca0da87c1ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-azure-vpn-gateways-to-multiple-on-premises-policy-based-vpn-devices-using-powershell"></a><span data-ttu-id="fdbc5-103">Conectar gateways VPN do Azure a vários dispositivos VPN com base em políticas locais usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="fdbc5-103">Connect Azure VPN gateways to multiple on-premises policy-based VPN devices using PowerShell</span></span>

<span data-ttu-id="fdbc5-104">Este artigo ajuda você a configurar um gateway de VPN com base em rotas do Azure para se conectar a vários dispositivos VPN com base em políticas locais utilizando políticas de IPsec/IKE personalizadas em conexões VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-104">This article helps you configure an Azure route-based VPN gateway to connect to multiple on-premises policy-based VPN devices leveraging custom IPsec/IKE policies on S2S VPN connections.</span></span>

## <a name="about-policy-based-and-route-based-vpn-gateways"></a><span data-ttu-id="fdbc5-105">Sobre gateways VPN com base em políticas e rotas</span><span class="sxs-lookup"><span data-stu-id="fdbc5-105">About policy-based and route-based VPN gateways</span></span>

<span data-ttu-id="fdbc5-106">Os dispositivos VPN com base em políticas *x* rotas diferem em como os seletores de tráfego IPsec são definidos em uma conexão:</span><span class="sxs-lookup"><span data-stu-id="fdbc5-106">Policy- *vs.* route-based VPN devices differ in how the IPsec traffic selectors are set on a connection:</span></span>

* <span data-ttu-id="fdbc5-107">Os dispositivos VPN **com base em políticas** usam as combinações de prefixos de ambas as redes para definir como o tráfego será criptografado/descriptografado por meio de túneis IPsec.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-107">**Policy-based** VPN devices use the combinations of prefixes from both networks to define how traffic is encrypted/decrypted through IPsec tunnels.</span></span> <span data-ttu-id="fdbc5-108">Normalmente, ele é criado em dispositivos de firewall que executam a filtragem de pacote.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-108">It is typically built on firewall devices that perform packet filtering.</span></span> <span data-ttu-id="fdbc5-109">A descriptografia e criptografia de túnel IPsec são adicionadas à filtragem de pacote e ao mecanismo de processamento.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-109">IPsec tunnel encryption and decryption are added to the packet filtering and processing engine.</span></span>
* <span data-ttu-id="fdbc5-110">Os dispositivos VPN **com base em rotas** usam seletores de tráfego qualquer (curinga) e permitem roteamento/encaminhamento do tráfego da direção das tabelas para diferentes túneis IPsec.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-110">**Route-based** VPN devices use any-to-any (wildcard) traffic selectors, and let routing/forwarding tables direct traffic to different IPsec tunnels.</span></span> <span data-ttu-id="fdbc5-111">Normalmente, ele é criado em plataformas de roteador, onde cada túnel IPsec é modelado como uma interface de rede ou VTI (interface do túnel virtual).</span><span class="sxs-lookup"><span data-stu-id="fdbc5-111">It is typically built on router platforms where each IPsec tunnel is modeled as a network interface or VTI (virtual tunnel interface).</span></span>

<span data-ttu-id="fdbc5-112">Os diagramas a seguir realçam dois modelos:</span><span class="sxs-lookup"><span data-stu-id="fdbc5-112">The following diagrams highlight the two models:</span></span>

### <a name="policy-based-vpn-example"></a><span data-ttu-id="fdbc5-113">Exemplo de VPN com base em políticas</span><span class="sxs-lookup"><span data-stu-id="fdbc5-113">Policy-based VPN example</span></span>
![baseado em políticas](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedmultisite.png)

### <a name="route-based-vpn-example"></a><span data-ttu-id="fdbc5-115">Exemplo de VPN com base em rotas</span><span class="sxs-lookup"><span data-stu-id="fdbc5-115">Route-based VPN example</span></span>
![baseado em rotas](./media/vpn-gateway-connect-multiple-policybased-rm-ps/routebasedmultisite.png)

### <a name="azure-support-for-policy-based-vpn"></a><span data-ttu-id="fdbc5-117">Suporte do Azure para VPN com base em políticas</span><span class="sxs-lookup"><span data-stu-id="fdbc5-117">Azure support for policy-based VPN</span></span>
<span data-ttu-id="fdbc5-118">Atualmente, o Azure oferece suporte a ambos os modos de gateways VPN: gateways VPN com base em rotas e gateways VPN com base em políticas.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-118">Currently, Azure supports both modes of VPN gateways: route-based VPN gateways and policy-based VPN gateways.</span></span> <span data-ttu-id="fdbc5-119">Eles são criados em diferentes plataformas internas que resultam em especificações diferentes:</span><span class="sxs-lookup"><span data-stu-id="fdbc5-119">They are built on different internal platforms, which result in different specifications:</span></span>

|                          | <span data-ttu-id="fdbc5-120">**Gateway de VPN PolicyBased**</span><span class="sxs-lookup"><span data-stu-id="fdbc5-120">**PolicyBased VPN Gateway**</span></span> | <span data-ttu-id="fdbc5-121">**Gateway de VPN RouteBased**</span><span class="sxs-lookup"><span data-stu-id="fdbc5-121">**RouteBased VPN Gateway**</span></span>               |
| ---                      | ---                         | ---                                      |
| <span data-ttu-id="fdbc5-122">**SKU de gateway do Azure**</span><span class="sxs-lookup"><span data-stu-id="fdbc5-122">**Azure Gateway SKU**</span></span>    | <span data-ttu-id="fdbc5-123">Basic</span><span class="sxs-lookup"><span data-stu-id="fdbc5-123">Basic</span></span>                       | <span data-ttu-id="fdbc5-124">Basic, Standard, HighPerformance</span><span class="sxs-lookup"><span data-stu-id="fdbc5-124">Basic, Standard, HighPerformance</span></span>         |
| <span data-ttu-id="fdbc5-125">**Versão IKE**</span><span class="sxs-lookup"><span data-stu-id="fdbc5-125">**IKE version**</span></span>          | <span data-ttu-id="fdbc5-126">IKEv1</span><span class="sxs-lookup"><span data-stu-id="fdbc5-126">IKEv1</span></span>                       | <span data-ttu-id="fdbc5-127">IKEv2</span><span class="sxs-lookup"><span data-stu-id="fdbc5-127">IKEv2</span></span>                                    |
| <span data-ttu-id="fdbc5-128">**IOPS Conexões S2S**</span><span class="sxs-lookup"><span data-stu-id="fdbc5-128">**Max. S2S connections**</span></span> | <span data-ttu-id="fdbc5-129">**1**</span><span class="sxs-lookup"><span data-stu-id="fdbc5-129">**1**</span></span>                       | <span data-ttu-id="fdbc5-130">Basic/Standard: 10</span><span class="sxs-lookup"><span data-stu-id="fdbc5-130">Basic/Standard: 10</span></span><br> <span data-ttu-id="fdbc5-131">HighPerformance: 30</span><span class="sxs-lookup"><span data-stu-id="fdbc5-131">HighPerformance: 30</span></span> |
|                          |                             |                                          |

<span data-ttu-id="fdbc5-132">Com a política de IPsec/IKE personalizada, agora você pode configurar gateways VPN com base em rota do Azure para usar os seletores de tráfego com base no prefixo com a opção "**PolicyBasedTrafficSelectors**", para se conectar a dispositivos VPN baseados em políticas locais.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-132">With the custom IPsec/IKE policy, you can now configure Azure route-based VPN gateways to use prefix-based traffic selectors with option "**PolicyBasedTrafficSelectors**", to connect to on-premises policy-based VPN devices.</span></span> <span data-ttu-id="fdbc5-133">Esse recurso permite a conexão de uma rede virtual do Azure e o gateway de VPN para vários dispositivos VPN/firewall com base em políticas locais, removendo o limite de conexão única dos gateways VPN com base em políticas atuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-133">This capability allows you to connect from an Azure virtual network and VPN gateway to multiple on-premises policy-based VPN/firewall devices, removing the single connection limit from the current Azure policy-based VPN gateways.</span></span>

> [!IMPORTANT]
> 1. <span data-ttu-id="fdbc5-134">Para habilitar essa conectividade, seus dispositivos VPN com base em políticas locais devem oferecer suporte a **IKEv2** para conectarem os gateways VPN com base em rotas do Azure.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-134">To enable this connectivity, your on-premises policy-based VPN devices must support **IKEv2** to connect to the Azure route-based VPN gateways.</span></span> <span data-ttu-id="fdbc5-135">Verifique as especificações do dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-135">Check your VPN device specifications.</span></span>
> 2. <span data-ttu-id="fdbc5-136">As redes locais que se conectam por meio de dispositivos VPN com base em políticas com esse mecanismo só podem se conectar à rede virtual do Azure. **eles não podem transitar por outras redes locais ou redes virtuais por meio do mesmo gateway de VPN do Azure**.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-136">The on-premises networks connecting through policy-based VPN devices with this mechanism can only connect to the Azure virtual network; **they cannot transit to other on-premises networks or virtual networks via the same Azure VPN gateway**.</span></span>
> 3. <span data-ttu-id="fdbc5-137">A opção de configuração faz parte da política de conexão IPsec/IKE personalizada.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-137">The configuration option is part of the custom IPsec/IKE connection policy.</span></span> <span data-ttu-id="fdbc5-138">Se você habilitar a opção do seletor de tráfego com base em políticas, deverá especificar a política toda (algoritmos de criptografia e de integridade de IPsec/IKE, restrições de chave e tempos de vida do SA).</span><span class="sxs-lookup"><span data-stu-id="fdbc5-138">If you enable the policy-based traffic selector option, you must specify the complete policy (IPsec/IKE encryption and integrity algorithms, key strengths, and SA lifetimes).</span></span>

<span data-ttu-id="fdbc5-139">O diagrama a seguir mostra por que o roteamento de tráfego por meio do gateway de VPN do Azure não funcionará com a opção baseada em políticas:</span><span class="sxs-lookup"><span data-stu-id="fdbc5-139">The following diagram shows why transit routing via Azure VPN gateway doesn't work with the policy-based option:</span></span>

![trânsito com base em políticas](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedtransit.png)

<span data-ttu-id="fdbc5-141">Conforme mostrado no diagrama, o gateway de VPN do Azure terá seletores de tráfego da rede virtual para cada prefixo de rede local, mas não os prefixos de conexão cruzada.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-141">As shown in the diagram, the Azure VPN gateway has traffic selectors from the virtual network to each of the on-premises network prefixes, but not the cross-connection prefixes.</span></span> <span data-ttu-id="fdbc5-142">Por exemplo, o local 2, local 3 e local 4 podem cada um se comunicar com a VNet1 respectivamente, mas não podem se conectar por meio do gateway de VPN do Azure entre si.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-142">For example, on-premises site 2, site 3, and site 4 can each communicate to VNet1 respectively, but cannot connect via the Azure VPN gateway to each other.</span></span> <span data-ttu-id="fdbc5-143">O diagrama mostra os seletores de tráfego com conexão cruzada que não estão disponíveis no gateway de VPN do Azure nesta configuração.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-143">The diagram shows the cross-connect traffic selectors that are not available in the Azure VPN gateway under this configuration.</span></span>

## <a name="configure-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="fdbc5-144">Configurar os seletores de tráfego com base em políticas para uma conexão</span><span class="sxs-lookup"><span data-stu-id="fdbc5-144">Configure policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="fdbc5-145">As instruções neste artigo seguem o mesmo exemplo, conforme descrito em [Configurar política de IPsec/IKE para conexões S2S ou VNet para VNet](vpn-gateway-ipsecikepolicy-rm-powershell.md), para estabelecer uma conexão VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-145">The instructions in this article follow the same example as described in [Configure IPsec/IKE policy for S2S or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) to establish a S2S VPN connection.</span></span> <span data-ttu-id="fdbc5-146">Isso é mostrado no diagrama a seguir:</span><span class="sxs-lookup"><span data-stu-id="fdbc5-146">This is shown in the following diagram:</span></span>

![política de S2S](./media/vpn-gateway-connect-multiple-policybased-rm-ps/s2spolicypb.png)

<span data-ttu-id="fdbc5-148">O fluxo de trabalho para habilitar esta conectividade:</span><span class="sxs-lookup"><span data-stu-id="fdbc5-148">The workflow to enable this connectivity:</span></span>
1. <span data-ttu-id="fdbc5-149">Criar a rede virtual, o gateway de VPN e o gateway de rede local para suas conexões locais cruzadas</span><span class="sxs-lookup"><span data-stu-id="fdbc5-149">Create the virtual network, VPN gateway, and local network gateway for your cross-premises connection</span></span>
2. <span data-ttu-id="fdbc5-150">Criar uma política de IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="fdbc5-150">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="fdbc5-151">Aplicar a política, quando você cria uma conexão S2S ou VNet para VNet e **habilita os seletores de tráfego com base em políticas** na conexão</span><span class="sxs-lookup"><span data-stu-id="fdbc5-151">Apply the policy when you create a S2S or VNet-to-VNet connection, and **enable the policy-based traffic selectors** on the connection</span></span>
4. <span data-ttu-id="fdbc5-152">Se a conexão já foi criada, você poderá aplicar ou atualizar a política para uma conexão existente</span><span class="sxs-lookup"><span data-stu-id="fdbc5-152">If the connection is already created, you can apply or update the policy to an existing connection</span></span>

## <a name="enable-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="fdbc5-153">Habilitar os seletores de tráfego com base em políticas para uma conexão</span><span class="sxs-lookup"><span data-stu-id="fdbc5-153">Enable policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="fdbc5-154">Verifique se você concluiu a [Parte 3 do artigo Configurar a política de IPsec/IKE](vpn-gateway-ipsecikepolicy-rm-powershell.md) para esta seção.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-154">Make sure you have completed [Part 3 of the Configure IPsec/IKE policy article](vpn-gateway-ipsecikepolicy-rm-powershell.md) for this section.</span></span> <span data-ttu-id="fdbc5-155">O exemplo a seguir usa os mesmos parâmetros e etapas:</span><span class="sxs-lookup"><span data-stu-id="fdbc5-155">The following example uses the same parameters and steps:</span></span>

### <a name="step-1---create-the-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="fdbc5-156">Etapa 1 - Criar a rede virtual, o gateway de VPN e o gateway de rede local</span><span class="sxs-lookup"><span data-stu-id="fdbc5-156">Step 1 - Create the virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables--connect-to-your-subscription"></a><span data-ttu-id="fdbc5-157">1. Declare as variáveis e conecte-se à sua assinatura</span><span class="sxs-lookup"><span data-stu-id="fdbc5-157">1. Declare your variables & connect to your subscription</span></span>
<span data-ttu-id="fdbc5-158">Para este exercício, começaremos declarando nossa variáveis.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-158">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="fdbc5-159">Certifique-se de substituir os valores pelos seus próprios ao configurar para a produção.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-159">Be sure to replace the values with your own when configuring for production.</span></span>

```powershell
$Sub1          = "<YourSubscriptionName>"
$RG1           = "TestPolicyRG1"
$Location1     = "East US 2"
$VNetName1     = "TestVNet1"
$FESubName1    = "FrontEnd"
$BESubName1    = "Backend"
$GWSubName1    = "GatewaySubnet"
$VNetPrefix11  = "10.11.0.0/16"
$VNetPrefix12  = "10.12.0.0/16"
$FESubPrefix1  = "10.11.0.0/24"
$BESubPrefix1  = "10.12.0.0/24"
$GWSubPrefix1  = "10.12.255.0/27"
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GW1IPName1    = "VNet1GWIP1"
$GW1IPconf1    = "gw1ipconf1"
$Connection16  = "VNet1toSite6"

$LNGName6      = "Site6"
$LNGPrefix61   = "10.61.0.0/16"
$LNGPrefix62   = "10.62.0.0/16"
$LNGIP6        = "131.107.72.22"
```
<span data-ttu-id="fdbc5-160">Para usar os cmdlets do Resource Manager, alterne para o modo do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-160">To use the Resource Manager cmdlets, make sure you switch to PowerShell mode.</span></span> <span data-ttu-id="fdbc5-161">Para obter mais informações, consulte [Usando o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="fdbc5-161">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="fdbc5-162">Abra o console do PowerShell e conecte-se à sua conta.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-162">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="fdbc5-163">Use o exemplo a seguir para ajudar com a conexão:</span><span class="sxs-lookup"><span data-stu-id="fdbc5-163">Use the following sample to help you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="2-create-the-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="fdbc5-164">2. Criar a rede virtual, o gateway de VPN e o gateway de rede local</span><span class="sxs-lookup"><span data-stu-id="fdbc5-164">2. Create the virtual network, VPN gateway, and local network gateway</span></span>
<span data-ttu-id="fdbc5-165">O exemplo a seguir cria a rede virtual, TestVNet1, com três sub-redes e o gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-165">The following example creates the virtual network, TestVNet1 with three subnets, and the VPN gateway.</span></span> <span data-ttu-id="fdbc5-166">Ao substituir valores, é importante que você sempre nomeie sua sub-rede de gateway especificamente como ‘GatewaySubnet’.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-166">When substituting values, it's important that you always name your gateway subnet specifically 'GatewaySubnet'.</span></span> <span data-ttu-id="fdbc5-167">Se você usar outro nome, a criação do gateway falhará.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-167">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

$gw1pip1    = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1      = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance

New-AzureRmLocalNetworkGateway -Name $LNGName6 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP6 -AddressPrefix $LNGPrefix61,$LNGPrefix62
```

### <a name="step-2---create-a-s2s-vpn-connection-with-an-ipsecike-policy"></a><span data-ttu-id="fdbc5-168">Parte 2 - Criar uma nova conexão de VPN S2S com a política de IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="fdbc5-168">Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="fdbc5-169">1. Criar uma política de IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="fdbc5-169">1. Create an IPsec/IKE policy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fdbc5-170">Você precisa criar uma política de IPsec/IKE para habilitar a opção "UsePolicyBasedTrafficSelectors" na conexão.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-170">You need to create an IPsec/IKE policy in order to enable "UsePolicyBasedTrafficSelectors" option on the connection.</span></span>

<span data-ttu-id="fdbc5-171">O exemplo a seguir cria uma política de IPsec/IKE com esses algoritmos e parâmetros:</span><span class="sxs-lookup"><span data-stu-id="fdbc5-171">The following example creates an IPsec/IKE policy with these algorithms and parameters:</span></span>
* <span data-ttu-id="fdbc5-172">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="fdbc5-172">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="fdbc5-173">IPsec: AES256, SHA256, PFS24, tempo de vida da SA 3600 segundos e 2048KB</span><span class="sxs-lookup"><span data-stu-id="fdbc5-173">IPsec: AES256, SHA256, PFS24, SA Lifetime 3600 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048
```

#### <a name="2-create-the-s2s-vpn-connection-with-policy-based-traffic-selectors-and-ipsecike-policy"></a><span data-ttu-id="fdbc5-174">2. Criar a conexão VPN S2S com seletores de tráfego com base em políticas e a política de IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="fdbc5-174">2. Create the S2S VPN connection with policy-based traffic selectors and IPsec/IKE policy</span></span>
<span data-ttu-id="fdbc5-175">Crie uma conexão VPN S2S e aplique a política de IPsec/IKE criada na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-175">Create an S2S VPN connection and apply the IPsec/IKE policy created in the previous step.</span></span> <span data-ttu-id="fdbc5-176">Observe o parâmetro adicional "-UsePolicyBasedTrafficSelectors $True", que habilita o seletor de tráfego baseado em políticas na conexão.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-176">Be aware of the additional parameter "-UsePolicyBasedTrafficSelectors $True"  which enables policy-based traffic selectors on the connection.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -UsePolicyBasedTrafficSelectors $True -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="fdbc5-177">Depois de concluir as etapas, a conexão VPN S2S usará a política de IPsec/IKE definida e habilita os seletores de tráfego com base em políticas na conexão.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-177">After completing the steps, the S2S VPN connection will use the IPsec/IKE policy defined, and enable policy-based traffic selectors on the connection.</span></span> <span data-ttu-id="fdbc5-178">Você pode repetir as mesmas etapas para adicionar mais conexões para dispositivos VPN baseados em políticas locais adicionais do mesmo gateway de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-178">You can repeat the same steps to add more connections to additional on-premises policy-based VPN devices from the same Azure VPN gateway.</span></span>

## <a name="update-policy-based-traffic-selectors-for-a-connection"></a><span data-ttu-id="fdbc5-179">Atualizar seletores de tráfego com base em políticas para uma conexão</span><span class="sxs-lookup"><span data-stu-id="fdbc5-179">Update policy-based traffic selectors for a connection</span></span>
<span data-ttu-id="fdbc5-180">A última seção mostra como atualizar a opção de seletores de tráfego com base em políticas para uma conexão VPN S2S existente.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-180">The last section shows you how to update the policy-based traffic selectors option for an existing  S2S VPN connection.</span></span>

### <a name="1-get-the-connection"></a><span data-ttu-id="fdbc5-181">1. Obtenha a conexão</span><span class="sxs-lookup"><span data-stu-id="fdbc5-181">1. Get the connection</span></span>
<span data-ttu-id="fdbc5-182">Obtenha o recurso de conexão.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-182">Get the connection resource.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
```

### <a name="2-check-the-policy-based-traffic-selectors-option"></a><span data-ttu-id="fdbc5-183">2. Marque a opção dos seletores de tráfego com base em políticas</span><span class="sxs-lookup"><span data-stu-id="fdbc5-183">2. Check the policy-based traffic selectors option</span></span>
<span data-ttu-id="fdbc5-184">A linha a seguir mostra se os seletores de tráfego com base em políticas são usados para a conexão:</span><span class="sxs-lookup"><span data-stu-id="fdbc5-184">The following line shows whether the policy-based traffic selectors are used for the connection:</span></span>

```powershell
$connection6.UsePolicyBasedTrafficSelectors
```

<span data-ttu-id="fdbc5-185">Se a linha retornar "**True**", então os seletores de tráfego com base em políticas serão configurados na conexão; caso contrário, ela retorna "**False**".</span><span class="sxs-lookup"><span data-stu-id="fdbc5-185">If the line returns "**True**", then policy-based traffic selectors are configured on the connection; otherwise it returns "**False**."</span></span>

### <a name="3-update-the-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="fdbc5-186">3. Atualizar os seletores de tráfego com base em políticas para uma conexão</span><span class="sxs-lookup"><span data-stu-id="fdbc5-186">3. Update the policy-based traffic selectors on a connection</span></span>
<span data-ttu-id="fdbc5-187">Depois de obter o recurso de conexão, você pode habilitar ou desabilitar a opção.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-187">Once you obtain the connection resource, you can enable or disable the option.</span></span>

#### <a name="disable-usepolicybasedtrafficselectors"></a><span data-ttu-id="fdbc5-188">Desabilitar UsePolicyBasedTrafficSelectors</span><span class="sxs-lookup"><span data-stu-id="fdbc5-188">Disable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="fdbc5-189">O exemplo a seguir desabilita a opção de seletores de tráfego com base na política, mas deixa a política de IPsec/IKE inalterada:</span><span class="sxs-lookup"><span data-stu-id="fdbc5-189">The following example disables the policy-based traffic selectors option, but leaves the IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $False
```

#### <a name="enable-usepolicybasedtrafficselectors"></a><span data-ttu-id="fdbc5-190">Habilitar UsePolicyBasedTrafficSelectors</span><span class="sxs-lookup"><span data-stu-id="fdbc5-190">Enable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="fdbc5-191">O exemplo a seguir habilita a opção de seletores de tráfego com base na política, mas deixa a política de IPsec/IKE inalterada:</span><span class="sxs-lookup"><span data-stu-id="fdbc5-191">The following example enables the policy-based traffic selectors option, but leaves the IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $True
```

## <a name="next-steps"></a><span data-ttu-id="fdbc5-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fdbc5-192">Next steps</span></span>
<span data-ttu-id="fdbc5-193">Quando sua conexão for concluída, você poderá adicionar máquinas virtuais às suas redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-193">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="fdbc5-194">Veja [Criar uma máquina virtual](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obter as etapas.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-194">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>

<span data-ttu-id="fdbc5-195">Também analise [Configurar política de IPsec/IKE para conexões de VPN S2S ou Rede Virtual para Rede Virtual](vpn-gateway-ipsecikepolicy-rm-powershell.md) para obter mais detalhes sobre políticas de IPsec/IKE personalizadas.</span><span class="sxs-lookup"><span data-stu-id="fdbc5-195">Also review [Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) for more details on custom IPsec/IKE policies.</span></span>
