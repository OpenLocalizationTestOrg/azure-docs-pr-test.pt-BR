---
title: "Conectar dispositivos VPN com base na política do Azure VPN gateways toomultiple local: Azure Resource Manager: PowerShell | Microsoft Docs"
description: "Este artigo orienta você pela configuração do Azure baseadas em rota VPN gateway toomultiple baseado em políticas dispositivos VPN usando o Gerenciador de recursos do Azure e o PowerShell."
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
ms.openlocfilehash: 866c78d96305207106a66cc3300c355e4b6bfbb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-azure-vpn-gateways-toomultiple-on-premises-policy-based-vpn-devices-using-powershell"></a><span data-ttu-id="ff0b3-103">Conecte-se a VPN do Azure gateways toomultiple baseado em políticas VPN dispositivos locais usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff0b3-103">Connect Azure VPN gateways toomultiple on-premises policy-based VPN devices using PowerShell</span></span>

<span data-ttu-id="ff0b3-104">Este artigo ajuda você a configurar um Azure baseadas em rota VPN gateway tooconnect toomultiple local baseado em políticas dispositivos VPN utilizando políticas personalizadas de IPsec/IKE em conexões VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-104">This article helps you configure an Azure route-based VPN gateway tooconnect toomultiple on-premises policy-based VPN devices leveraging custom IPsec/IKE policies on S2S VPN connections.</span></span>

## <a name="about-policy-based-and-route-based-vpn-gateways"></a><span data-ttu-id="ff0b3-105">Sobre gateways VPN com base em políticas e rotas</span><span class="sxs-lookup"><span data-stu-id="ff0b3-105">About policy-based and route-based VPN gateways</span></span>

<span data-ttu-id="ff0b3-106">Política - *versus* dispositivos VPN com base em rota diferem em como os seletores de tráfego de IPsec Olá são definidos em uma conexão:</span><span class="sxs-lookup"><span data-stu-id="ff0b3-106">Policy- *vs.* route-based VPN devices differ in how hello IPsec traffic selectors are set on a connection:</span></span>

* <span data-ttu-id="ff0b3-107">**Com base na política** dispositivos VPN usam combinações de saudação de prefixos de ambos os toodefine de redes, como tráfego será criptografado/descriptografado por meio de túneis IPsec.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-107">**Policy-based** VPN devices use hello combinations of prefixes from both networks toodefine how traffic is encrypted/decrypted through IPsec tunnels.</span></span> <span data-ttu-id="ff0b3-108">Normalmente, ele é criado em dispositivos de firewall que executam a filtragem de pacote.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-108">It is typically built on firewall devices that perform packet filtering.</span></span> <span data-ttu-id="ff0b3-109">Descriptografia e criptografia de túnel IPsec são adicionados a filtragem de pacotes toohello e o mecanismo de processamento.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-109">IPsec tunnel encryption and decryption are added toohello packet filtering and processing engine.</span></span>
* <span data-ttu-id="ff0b3-110">**Baseado em rotas** dispositivos VPN usam seletores de tráfego para qualquer (curinga) e permitem roteamento/encaminhamento tabelas túneis do IPsec toodifferent tráfego direto.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-110">**Route-based** VPN devices use any-to-any (wildcard) traffic selectors, and let routing/forwarding tables direct traffic toodifferent IPsec tunnels.</span></span> <span data-ttu-id="ff0b3-111">Normalmente, ele é criado em plataformas de roteador, onde cada túnel IPsec é modelado como uma interface de rede ou VTI (interface do túnel virtual).</span><span class="sxs-lookup"><span data-stu-id="ff0b3-111">It is typically built on router platforms where each IPsec tunnel is modeled as a network interface or VTI (virtual tunnel interface).</span></span>

<span data-ttu-id="ff0b3-112">Olá diagramas a seguir realçam dois modelos de saudação:</span><span class="sxs-lookup"><span data-stu-id="ff0b3-112">hello following diagrams highlight hello two models:</span></span>

### <a name="policy-based-vpn-example"></a><span data-ttu-id="ff0b3-113">Exemplo de VPN com base em políticas</span><span class="sxs-lookup"><span data-stu-id="ff0b3-113">Policy-based VPN example</span></span>
![baseado em políticas](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedmultisite.png)

### <a name="route-based-vpn-example"></a><span data-ttu-id="ff0b3-115">Exemplo de VPN com base em rotas</span><span class="sxs-lookup"><span data-stu-id="ff0b3-115">Route-based VPN example</span></span>
![baseado em rotas](./media/vpn-gateway-connect-multiple-policybased-rm-ps/routebasedmultisite.png)

### <a name="azure-support-for-policy-based-vpn"></a><span data-ttu-id="ff0b3-117">Suporte do Azure para VPN com base em políticas</span><span class="sxs-lookup"><span data-stu-id="ff0b3-117">Azure support for policy-based VPN</span></span>
<span data-ttu-id="ff0b3-118">Atualmente, o Azure oferece suporte a ambos os modos de gateways VPN: gateways VPN com base em rotas e gateways VPN com base em políticas.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-118">Currently, Azure supports both modes of VPN gateways: route-based VPN gateways and policy-based VPN gateways.</span></span> <span data-ttu-id="ff0b3-119">Eles são criados em diferentes plataformas internas que resultam em especificações diferentes:</span><span class="sxs-lookup"><span data-stu-id="ff0b3-119">They are built on different internal platforms, which result in different specifications:</span></span>

|                          | <span data-ttu-id="ff0b3-120">**Gateway de VPN PolicyBased**</span><span class="sxs-lookup"><span data-stu-id="ff0b3-120">**PolicyBased VPN Gateway**</span></span> | <span data-ttu-id="ff0b3-121">**Gateway de VPN RouteBased**</span><span class="sxs-lookup"><span data-stu-id="ff0b3-121">**RouteBased VPN Gateway**</span></span>               |
| ---                      | ---                         | ---                                      |
| <span data-ttu-id="ff0b3-122">**SKU de gateway do Azure**</span><span class="sxs-lookup"><span data-stu-id="ff0b3-122">**Azure Gateway SKU**</span></span>    | <span data-ttu-id="ff0b3-123">Basic</span><span class="sxs-lookup"><span data-stu-id="ff0b3-123">Basic</span></span>                       | <span data-ttu-id="ff0b3-124">Basic, Standard, HighPerformance</span><span class="sxs-lookup"><span data-stu-id="ff0b3-124">Basic, Standard, HighPerformance</span></span>         |
| <span data-ttu-id="ff0b3-125">**Versão IKE**</span><span class="sxs-lookup"><span data-stu-id="ff0b3-125">**IKE version**</span></span>          | <span data-ttu-id="ff0b3-126">IKEv1</span><span class="sxs-lookup"><span data-stu-id="ff0b3-126">IKEv1</span></span>                       | <span data-ttu-id="ff0b3-127">IKEv2</span><span class="sxs-lookup"><span data-stu-id="ff0b3-127">IKEv2</span></span>                                    |
| <span data-ttu-id="ff0b3-128">**IOPS Conexões S2S**</span><span class="sxs-lookup"><span data-stu-id="ff0b3-128">**Max. S2S connections**</span></span> | <span data-ttu-id="ff0b3-129">**1**</span><span class="sxs-lookup"><span data-stu-id="ff0b3-129">**1**</span></span>                       | <span data-ttu-id="ff0b3-130">Basic/Standard: 10</span><span class="sxs-lookup"><span data-stu-id="ff0b3-130">Basic/Standard: 10</span></span><br> <span data-ttu-id="ff0b3-131">HighPerformance: 30</span><span class="sxs-lookup"><span data-stu-id="ff0b3-131">HighPerformance: 30</span></span> |
|                          |                             |                                          |

<span data-ttu-id="ff0b3-132">Com a diretiva de IPsec/IKE personalizada hello, agora você pode configurar o Azure baseadas em rota VPN gateways toouse com base no prefixo seletores de tráfego com a opção "**PolicyBasedTrafficSelectors**", dispositivos VPN com base na política do tooconnect tooon locais.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-132">With hello custom IPsec/IKE policy, you can now configure Azure route-based VPN gateways toouse prefix-based traffic selectors with option "**PolicyBasedTrafficSelectors**", tooconnect tooon-premises policy-based VPN devices.</span></span> <span data-ttu-id="ff0b3-133">Esse recurso permite que você tooconnect de uma rede virtual do Azure e toomultiple de gateway VPN de dispositivos VPN/firewall baseado em políticas, removendo o limite de conexão única de saudação do atuais gateways VPN com base na política do Azure Olá no local.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-133">This capability allows you tooconnect from an Azure virtual network and VPN gateway toomultiple on-premises policy-based VPN/firewall devices, removing hello single connection limit from hello current Azure policy-based VPN gateways.</span></span>

> [!IMPORTANT]
> 1. <span data-ttu-id="ff0b3-134">tooenable essa conectividade, seus dispositivos VPN com base na política local devem oferecer suporte **IKEv2** tooconnect toohello Azure baseadas em rota gateways VPN.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-134">tooenable this connectivity, your on-premises policy-based VPN devices must support **IKEv2** tooconnect toohello Azure route-based VPN gateways.</span></span> <span data-ttu-id="ff0b3-135">Verifique as especificações do dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-135">Check your VPN device specifications.</span></span>
> 2. <span data-ttu-id="ff0b3-136">redes locais de saudação conectando por meio de dispositivos VPN com base na política com esse mecanismo só podem se conectar toohello rede virtual do Azure. **não é possível atravessam redes locais de tooother ou redes virtuais por meio de Olá mesmo gateway VPN do Azure**.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-136">hello on-premises networks connecting through policy-based VPN devices with this mechanism can only connect toohello Azure virtual network; **they cannot transit tooother on-premises networks or virtual networks via hello same Azure VPN gateway**.</span></span>
> 3. <span data-ttu-id="ff0b3-137">opção de configuração de saudação faz parte da política personalizada de conexão do IPsec/IKE hello.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-137">hello configuration option is part of hello custom IPsec/IKE connection policy.</span></span> <span data-ttu-id="ff0b3-138">Se você habilitar a opção de seletor Olá tráfego baseado em políticas, você deve especificar política completa de saudação (algoritmos de criptografia e a integridade de IPsec/IKE, restrições de chave e tempos de vida do SA).</span><span class="sxs-lookup"><span data-stu-id="ff0b3-138">If you enable hello policy-based traffic selector option, you must specify hello complete policy (IPsec/IKE encryption and integrity algorithms, key strengths, and SA lifetimes).</span></span>

<span data-ttu-id="ff0b3-139">Olá diagrama a seguir mostra por que o roteamento de tráfego por meio do gateway de VPN do Azure não funciona com a opção de baseado em políticas de saudação:</span><span class="sxs-lookup"><span data-stu-id="ff0b3-139">hello following diagram shows why transit routing via Azure VPN gateway doesn't work with hello policy-based option:</span></span>

![trânsito com base em políticas](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedtransit.png)

<span data-ttu-id="ff0b3-141">Conforme mostrado no diagrama hello, gateway de VPN do Azure Olá tem seletores de tráfego de saudação tooeach de rede virtual de prefixos de rede local hello, mas não os prefixos de conexão entre hello.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-141">As shown in hello diagram, hello Azure VPN gateway has traffic selectors from hello virtual network tooeach of hello on-premises network prefixes, but not hello cross-connection prefixes.</span></span> <span data-ttu-id="ff0b3-142">Por exemplo, no site local 2, site 3 e 4 do site podem cada comunicar tooVNet1 respectivamente, mas não podem se conectar via Olá VPN do Azure gateway tooeach outros.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-142">For example, on-premises site 2, site 3, and site 4 can each communicate tooVNet1 respectively, but cannot connect via hello Azure VPN gateway tooeach other.</span></span> <span data-ttu-id="ff0b3-143">diagrama de saudação mostra Olá conectar-se entre os seletores de tráfego que não estão disponíveis no gateway de VPN do Azure Olá nesta configuração.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-143">hello diagram shows hello cross-connect traffic selectors that are not available in hello Azure VPN gateway under this configuration.</span></span>

## <a name="configure-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="ff0b3-144">Configurar os seletores de tráfego com base em políticas para uma conexão</span><span class="sxs-lookup"><span data-stu-id="ff0b3-144">Configure policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="ff0b3-145">Olá instruções deste artigo, siga Olá mesmo exemplo conforme descrito em [política IPsec/IKE configurar conexões S2S ou VNet para VNet](vpn-gateway-ipsecikepolicy-rm-powershell.md) tooestablish uma conexão VPN S2S.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-145">hello instructions in this article follow hello same example as described in [Configure IPsec/IKE policy for S2S or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) tooestablish a S2S VPN connection.</span></span> <span data-ttu-id="ff0b3-146">Isso é mostrado no diagrama a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="ff0b3-146">This is shown in hello following diagram:</span></span>

![política de S2S](./media/vpn-gateway-connect-multiple-policybased-rm-ps/s2spolicypb.png)

<span data-ttu-id="ff0b3-148">Olá tooenable de fluxo de trabalho essa conectividade:</span><span class="sxs-lookup"><span data-stu-id="ff0b3-148">hello workflow tooenable this connectivity:</span></span>
1. <span data-ttu-id="ff0b3-149">Criar rede virtual hello, gateway de VPN e o gateway de rede local para a conexão entre locais</span><span class="sxs-lookup"><span data-stu-id="ff0b3-149">Create hello virtual network, VPN gateway, and local network gateway for your cross-premises connection</span></span>
2. <span data-ttu-id="ff0b3-150">Criar uma política de IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="ff0b3-150">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="ff0b3-151">Aplique a política de hello quando você criar uma conexão S2S ou VNet para VNet, e **habilitar seletores de tráfego com base na política de saudação** na conexão Olá</span><span class="sxs-lookup"><span data-stu-id="ff0b3-151">Apply hello policy when you create a S2S or VNet-to-VNet connection, and **enable hello policy-based traffic selectors** on hello connection</span></span>
4. <span data-ttu-id="ff0b3-152">Se a conexão de saudação já foi criado, você pode aplicar ou atualizar a conexão existente do hello política tooan</span><span class="sxs-lookup"><span data-stu-id="ff0b3-152">If hello connection is already created, you can apply or update hello policy tooan existing connection</span></span>

## <a name="enable-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="ff0b3-153">Habilitar os seletores de tráfego com base em políticas para uma conexão</span><span class="sxs-lookup"><span data-stu-id="ff0b3-153">Enable policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="ff0b3-154">Verifique se você concluiu [parte 3 de artigo de diretiva de IPsec/IKE configurar Olá](vpn-gateway-ipsecikepolicy-rm-powershell.md) para essa seção.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-154">Make sure you have completed [Part 3 of hello Configure IPsec/IKE policy article](vpn-gateway-ipsecikepolicy-rm-powershell.md) for this section.</span></span> <span data-ttu-id="ff0b3-155">Olá seguindo o exemplo usa Olá mesmos parâmetros e etapas:</span><span class="sxs-lookup"><span data-stu-id="ff0b3-155">hello following example uses hello same parameters and steps:</span></span>

### <a name="step-1---create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="ff0b3-156">Etapa 1 - Criar rede virtual hello, gateway de VPN e gateway de rede local</span><span class="sxs-lookup"><span data-stu-id="ff0b3-156">Step 1 - Create hello virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables--connect-tooyour-subscription"></a><span data-ttu-id="ff0b3-157">1. Declare as variáveis & conectar-se a assinatura de tooyour</span><span class="sxs-lookup"><span data-stu-id="ff0b3-157">1. Declare your variables & connect tooyour subscription</span></span>
<span data-ttu-id="ff0b3-158">Para este exercício, começaremos declarando nossa variáveis.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-158">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="ff0b3-159">Ser valores de saudação tooreplace-se com seu próprio durante a configuração de produção.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-159">Be sure tooreplace hello values with your own when configuring for production.</span></span>

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
<span data-ttu-id="ff0b3-160">toouse Olá cmdlets do Gerenciador de recursos, verifique se você alternar o modo de tooPowerShell.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-160">toouse hello Resource Manager cmdlets, make sure you switch tooPowerShell mode.</span></span> <span data-ttu-id="ff0b3-161">Para obter mais informações, consulte [Usando o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="ff0b3-161">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="ff0b3-162">Abra o console do PowerShell e conecte-se a conta de tooyour.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-162">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="ff0b3-163">Use Olá toohelp de exemplo que você se conectar a seguir:</span><span class="sxs-lookup"><span data-stu-id="ff0b3-163">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="2-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="ff0b3-164">2. Criar rede virtual hello, gateway de VPN e gateway de rede local</span><span class="sxs-lookup"><span data-stu-id="ff0b3-164">2. Create hello virtual network, VPN gateway, and local network gateway</span></span>
<span data-ttu-id="ff0b3-165">saudação de exemplo a seguir cria rede virtual hello, TestVNet1 com três sub-redes e gateway VPN hello.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-165">hello following example creates hello virtual network, TestVNet1 with three subnets, and hello VPN gateway.</span></span> <span data-ttu-id="ff0b3-166">Ao substituir valores, é importante que você sempre nomeie sua sub-rede de gateway especificamente como ‘GatewaySubnet’.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-166">When substituting values, it's important that you always name your gateway subnet specifically 'GatewaySubnet'.</span></span> <span data-ttu-id="ff0b3-167">Se você usar outro nome, a criação do gateway falhará.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-167">If you name it something else, your gateway creation fails.</span></span>

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

### <a name="step-2---create-a-s2s-vpn-connection-with-an-ipsecike-policy"></a><span data-ttu-id="ff0b3-168">Parte 2 - Criar uma nova conexão de VPN S2S com a política de IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="ff0b3-168">Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="ff0b3-169">1. Criar uma política de IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="ff0b3-169">1. Create an IPsec/IKE policy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff0b3-170">Você precisa de toocreate uma política de IPsec/IKE na ordem tooenable opção "UsePolicyBasedTrafficSelectors" na conexão hello.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-170">You need toocreate an IPsec/IKE policy in order tooenable "UsePolicyBasedTrafficSelectors" option on hello connection.</span></span>

<span data-ttu-id="ff0b3-171">Olá exemplo a seguir cria uma política de IPsec/IKE com esses algoritmos e parâmetros:</span><span class="sxs-lookup"><span data-stu-id="ff0b3-171">hello following example creates an IPsec/IKE policy with these algorithms and parameters:</span></span>
* <span data-ttu-id="ff0b3-172">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="ff0b3-172">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="ff0b3-173">IPsec: AES256, SHA256, PFS24, tempo de vida da SA 3600 segundos e 2048KB</span><span class="sxs-lookup"><span data-stu-id="ff0b3-173">IPsec: AES256, SHA256, PFS24, SA Lifetime 3600 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-policy-based-traffic-selectors-and-ipsecike-policy"></a><span data-ttu-id="ff0b3-174">2. Criar conexão de VPN S2S Olá com seletores de tráfego com base em política e a diretiva de IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="ff0b3-174">2. Create hello S2S VPN connection with policy-based traffic selectors and IPsec/IKE policy</span></span>
<span data-ttu-id="ff0b3-175">Criar uma conexão VPN S2S e aplicar a diretiva de IPsec/IKE Olá criada na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-175">Create an S2S VPN connection and apply hello IPsec/IKE policy created in hello previous step.</span></span> <span data-ttu-id="ff0b3-176">Lembre-se de parâmetro adicionais hello "-UsePolicyBasedTrafficSelectors $True" que permite que os seletores de tráfego baseado em políticas na conexão hello.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-176">Be aware of hello additional parameter "-UsePolicyBasedTrafficSelectors $True"  which enables policy-based traffic selectors on hello connection.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -UsePolicyBasedTrafficSelectors $True -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="ff0b3-177">Depois de concluir as etapas de Olá, Olá conexão VPN S2S usará Olá política IPsec/IKE definida e habilitar os seletores de tráfego baseado em políticas em conexão hello.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-177">After completing hello steps, hello S2S VPN connection will use hello IPsec/IKE policy defined, and enable policy-based traffic selectors on hello connection.</span></span> <span data-ttu-id="ff0b3-178">Você pode repetir Olá mesmo etapas tooadd mais conexões tooadditional local com base na política dispositivos VPN de Olá mesmo gateway VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-178">You can repeat hello same steps tooadd more connections tooadditional on-premises policy-based VPN devices from hello same Azure VPN gateway.</span></span>

## <a name="update-policy-based-traffic-selectors-for-a-connection"></a><span data-ttu-id="ff0b3-179">Atualizar seletores de tráfego com base em políticas para uma conexão</span><span class="sxs-lookup"><span data-stu-id="ff0b3-179">Update policy-based traffic selectors for a connection</span></span>
<span data-ttu-id="ff0b3-180">Olá última seção mostra a você como seletores de tráfego com base na política de saudação tooupdate opção para uma conexão VPN S2S existente.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-180">hello last section shows you how tooupdate hello policy-based traffic selectors option for an existing  S2S VPN connection.</span></span>

### <a name="1-get-hello-connection"></a><span data-ttu-id="ff0b3-181">1. Obter conexão Olá</span><span class="sxs-lookup"><span data-stu-id="ff0b3-181">1. Get hello connection</span></span>
<span data-ttu-id="ff0b3-182">Obter recurso de conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-182">Get hello connection resource.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
```

### <a name="2-check-hello-policy-based-traffic-selectors-option"></a><span data-ttu-id="ff0b3-183">2. Verificar opção de seletores de tráfego com base na política de saudação</span><span class="sxs-lookup"><span data-stu-id="ff0b3-183">2. Check hello policy-based traffic selectors option</span></span>
<span data-ttu-id="ff0b3-184">Olá linha a seguir mostra se os seletores de tráfego com base na política de saudação são usados para conexão hello:</span><span class="sxs-lookup"><span data-stu-id="ff0b3-184">hello following line shows whether hello policy-based traffic selectors are used for hello connection:</span></span>

```powershell
$connection6.UsePolicyBasedTrafficSelectors
```

<span data-ttu-id="ff0b3-185">Se a linha hello retorna "**True**", em seguida, seletores de tráfego com base na política são configurados na conexão de saudação; caso contrário, ele retorna "**False**."</span><span class="sxs-lookup"><span data-stu-id="ff0b3-185">If hello line returns "**True**", then policy-based traffic selectors are configured on hello connection; otherwise it returns "**False**."</span></span>

### <a name="3-update-hello-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="ff0b3-186">3. Atualizar seletores de tráfego com base na política de saudação em uma conexão</span><span class="sxs-lookup"><span data-stu-id="ff0b3-186">3. Update hello policy-based traffic selectors on a connection</span></span>
<span data-ttu-id="ff0b3-187">Depois de obter o recurso de conexão hello, você pode habilitar ou desabilitar a opção de saudação.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-187">Once you obtain hello connection resource, you can enable or disable hello option.</span></span>

#### <a name="disable-usepolicybasedtrafficselectors"></a><span data-ttu-id="ff0b3-188">Desabilitar UsePolicyBasedTrafficSelectors</span><span class="sxs-lookup"><span data-stu-id="ff0b3-188">Disable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="ff0b3-189">Olá exemplo a seguir desabilita a opção de seletores de tráfego com base na política de hello, mas deixa Olá política IPsec/IKE inalterada:</span><span class="sxs-lookup"><span data-stu-id="ff0b3-189">hello following example disables hello policy-based traffic selectors option, but leaves hello IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $False
```

#### <a name="enable-usepolicybasedtrafficselectors"></a><span data-ttu-id="ff0b3-190">Habilitar UsePolicyBasedTrafficSelectors</span><span class="sxs-lookup"><span data-stu-id="ff0b3-190">Enable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="ff0b3-191">Olá exemplo a seguir habilita a opção de seletores de tráfego com base na política de saudação, mas deixa Olá política IPsec/IKE inalterada:</span><span class="sxs-lookup"><span data-stu-id="ff0b3-191">hello following example enables hello policy-based traffic selectors option, but leaves hello IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $True
```

## <a name="next-steps"></a><span data-ttu-id="ff0b3-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ff0b3-192">Next steps</span></span>
<span data-ttu-id="ff0b3-193">Quando a conexão for concluída, você pode adicionar máquinas virtuais tooyour as redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-193">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="ff0b3-194">Veja [Criar uma máquina virtual](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obter as etapas.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-194">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>

<span data-ttu-id="ff0b3-195">Também analise [Configurar política de IPsec/IKE para conexões de VPN S2S ou Rede Virtual para Rede Virtual](vpn-gateway-ipsecikepolicy-rm-powershell.md) para obter mais detalhes sobre políticas de IPsec/IKE personalizadas.</span><span class="sxs-lookup"><span data-stu-id="ff0b3-195">Also review [Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) for more details on custom IPsec/IKE policies.</span></span>
