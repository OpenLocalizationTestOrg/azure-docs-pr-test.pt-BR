---
title: "Configurar conexões VPN S2S ativa-ativa para Gateways de VPN: Azure Resource Manager: PowerShell | Microsoft Docs"
description: "Este artigo mostra como configurar conexões ativo-ativo com gateways de VPN do Azure usando o Azure Resource Manager e o PowerShell."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2017
ms.author: yushwang
ms.openlocfilehash: 964eedc7698e42bf0e082f0105845f2a339daf57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-active-s2s-vpn-connections-with-azure-vpn-gateways"></a><span data-ttu-id="67e19-103">Configurar conexões VPN S2S ativa-ativa com Gateways de VPN</span><span class="sxs-lookup"><span data-stu-id="67e19-103">Configure active-active S2S VPN connections with Azure VPN Gateways</span></span>

<span data-ttu-id="67e19-104">Este artigo orienta Olá etapas toocreate ativo-ativo entre locais e conexões de rede virtual a rede usando o modelo de implantação do Gerenciador de recursos de saudação e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="67e19-104">This article walks you through hello steps toocreate active-active cross-premises and VNet-to-VNet connections using hello Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-highly-available-cross-premises-connections"></a><span data-ttu-id="67e19-105">Sobre conexões altamente disponíveis entre instalações</span><span class="sxs-lookup"><span data-stu-id="67e19-105">About Highly Available Cross-Premises Connections</span></span>
<span data-ttu-id="67e19-106">tooachieve alta disponibilidade para entre locais e a conectividade de rede virtual a rede, você deve implantar vários gateways VPN e estabelecer várias conexões paralelos entre suas redes e o Azure.</span><span class="sxs-lookup"><span data-stu-id="67e19-106">tooachieve high availability for cross-premises and VNet-to-VNet connectivity, you should deploy multiple VPN gateways and establish multiple parallel connections between your networks and Azure.</span></span> <span data-ttu-id="67e19-107">Consulte [Conectividade Altamente Disponível entre os Locais e VNet para VNet](vpn-gateway-highlyavailable.md) para obter uma visão geral das opções de conectividade e topologia.</span><span class="sxs-lookup"><span data-stu-id="67e19-107">Please see [Highly Available Cross-Premises and VNet-to-VNet Connectivity](vpn-gateway-highlyavailable.md) for an overview of connectivity options and topology.</span></span>

<span data-ttu-id="67e19-108">Este artigo fornece instruções de saudação tooset a um ativo-ativo entre locais conexão VPN e conexão ativa entre duas redes virtuais:</span><span class="sxs-lookup"><span data-stu-id="67e19-108">This article provides hello instructions tooset up an active-active cross-premises VPN connection, and active-active connection between two virtual networks:</span></span>

* [<span data-ttu-id="67e19-109">Parte 1 – Criar e configurar seu gateway de VPN do Azure no modo ativo-ativo</span><span class="sxs-lookup"><span data-stu-id="67e19-109">Part 1 - Create and configure your Azure VPN gateway in active-active mode</span></span>](#aagateway)
* [<span data-ttu-id="67e19-110">Parte 2 – Estabelecer conexões entre os locais ativo-ativo</span><span class="sxs-lookup"><span data-stu-id="67e19-110">Part 2 - Establish active-active cross-premises connections</span></span>](#aacrossprem)
* [<span data-ttu-id="67e19-111">Parte 3 – Estabelecer conexões VNet para VNet ativo-ativo</span><span class="sxs-lookup"><span data-stu-id="67e19-111">Part 3 - Establish active-active VNet-to-VNet connections</span></span>](#aav2v)
* [<span data-ttu-id="67e19-112">Parte 4 – Atualizar o gateway existente entre ativo-ativo e ativo-em espera</span><span class="sxs-lookup"><span data-stu-id="67e19-112">Part 4 - Update existing gateway between active-active and active-standby</span></span>](#aaupdate)

<span data-ttu-id="67e19-113">Você pode combinar essas toobuild juntos uma topologia de rede mais complexa, altamente disponível que atenda às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="67e19-113">You can combine these together toobuild a more complex, highly available network topology that meets your needs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="67e19-114">Observe que o modo ativo-ativo Olá usa Olá somente SKUs a seguir:</span><span class="sxs-lookup"><span data-stu-id="67e19-114">Please note that hello active-active mode uses only hello following SKUs:</span></span> 
  * <span data-ttu-id="67e19-115">VpnGw1, VpnGw2, VpnGw3</span><span class="sxs-lookup"><span data-stu-id="67e19-115">VpnGw1, VpnGw2, VpnGw3</span></span>
  * <span data-ttu-id="67e19-116">HighPerformance (para SKUs herdados antigos)</span><span class="sxs-lookup"><span data-stu-id="67e19-116">HighPerformance (for old legacy SKUs)</span></span>
> 
> 

## <span data-ttu-id="67e19-117"><a name ="aagateway"></a>Parte 1 – Criar e configurar os gateways de VPN ativo-ativo</span><span class="sxs-lookup"><span data-stu-id="67e19-117"><a name ="aagateway"></a>Part 1 - Create and configure active-active VPN gateways</span></span>
<span data-ttu-id="67e19-118">Olá etapas a seguir configurará o gateway de VPN do Azure nos modos ativo-ativo.</span><span class="sxs-lookup"><span data-stu-id="67e19-118">hello following steps will configure your Azure VPN gateway in active-active modes.</span></span> <span data-ttu-id="67e19-119">principais diferenças entre os gateways de ativo-ativo e ativa / em espera Olá Olá:</span><span class="sxs-lookup"><span data-stu-id="67e19-119">hello key differences between hello active-active and active-standby gateways:</span></span>

* <span data-ttu-id="67e19-120">Você precisa toocreate duas configurações de IP de Gateway com dois endereços IP públicos</span><span class="sxs-lookup"><span data-stu-id="67e19-120">You need toocreate two Gateway IP configurations with two public IP addresses</span></span>
* <span data-ttu-id="67e19-121">Você precisa definir o sinalizador de EnableActiveActiveFeature de saudação</span><span class="sxs-lookup"><span data-stu-id="67e19-121">You need set hello EnableActiveActiveFeature flag</span></span>
* <span data-ttu-id="67e19-122">SKU do gateway Olá deve ser VpnGw1, VpnGw2, VpnGw3 ou alto desempenho (SKU herdado).</span><span class="sxs-lookup"><span data-stu-id="67e19-122">hello gateway SKU must be VpnGw1, VpnGw2, VpnGw3, or HighPerformance (legacy SKU).</span></span>

<span data-ttu-id="67e19-123">Olá outras propriedades são Olá mesmo como gateways de não-ativo-ativo hello.</span><span class="sxs-lookup"><span data-stu-id="67e19-123">hello other properties are hello same as hello non-active-active gateways.</span></span> 

### <a name="before-you-begin"></a><span data-ttu-id="67e19-124">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="67e19-124">Before you begin</span></span>
* <span data-ttu-id="67e19-125">Verifique se você tem uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="67e19-125">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="67e19-126">Se ainda não tiver uma assinatura do Azure, você poderá ativar os [Benefícios do assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se para obter uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="67e19-126">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="67e19-127">Você precisará tooinstall Olá Gerenciador de recursos de cmdlets do PowerShell Azure.</span><span class="sxs-lookup"><span data-stu-id="67e19-127">You'll need tooinstall hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="67e19-128">Consulte [visão geral do Azure PowerShell](/powershell/azure/overview) para obter mais informações sobre como instalar os cmdlets do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="67e19-128">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="67e19-129">Etapa 1 - Criar e configurar VNet1</span><span class="sxs-lookup"><span data-stu-id="67e19-129">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="67e19-130">1. Declare as variáveis</span><span class="sxs-lookup"><span data-stu-id="67e19-130">1. Declare your variables</span></span>
<span data-ttu-id="67e19-131">Para este exercício, começaremos declarando nossa variáveis.</span><span class="sxs-lookup"><span data-stu-id="67e19-131">For this exercise, we'll start by declaring our variables.</span></span> <span data-ttu-id="67e19-132">exemplo Hello abaixo declara variáveis hello usando valores de saudação para este exercício.</span><span class="sxs-lookup"><span data-stu-id="67e19-132">hello example below declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="67e19-133">Ser valores de saudação tooreplace-se com seu próprio durante a configuração de produção.</span><span class="sxs-lookup"><span data-stu-id="67e19-133">Be sure tooreplace hello values with your own when configuring for production.</span></span> <span data-ttu-id="67e19-134">Você pode usar essas variáveis, se você estiver executando a saudação etapas toobecome familiarizado com esse tipo de configuração.</span><span class="sxs-lookup"><span data-stu-id="67e19-134">You can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="67e19-135">Modificar variáveis de Olá e, em seguida, copie e cole o console do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="67e19-135">Modify hello variables, and then copy and paste into your PowerShell console.</span></span>

```powershell
$Sub1 = "Ross"
$RG1 = "TestAARG1"
$Location1 = "West US"
$VNetName1 = "TestVNet1"
$FESubName1 = "FrontEnd"
$BESubName1 = "Backend"
$GWSubName1 = "GatewaySubnet"
$VNetPrefix11 = "10.11.0.0/16"
$VNetPrefix12 = "10.12.0.0/16"
$FESubPrefix1 = "10.11.0.0/24"
$BESubPrefix1 = "10.12.0.0/24"
$GWSubPrefix1 = "10.12.255.0/27"
$VNet1ASN = 65010
$DNS1 = "8.8.8.8"
$GWName1 = "VNet1GW"
$GW1IPName1 = "VNet1GWIP1"
$GW1IPName2 = "VNet1GWIP2"
$GW1IPconf1 = "gw1ipconf1"
$GW1IPconf2 = "gw1ipconf2"
$Connection12 = "VNet1toVNet2"
$Connection151 = "VNet1toSite5_1"
$Connection152 = "VNet1toSite5_2"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="67e19-136">2. Conecte-se a assinatura de tooyour e criar um novo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="67e19-136">2. Connect tooyour subscription and create a new resource group</span></span>
<span data-ttu-id="67e19-137">Verifique se que você alternar Olá toouse de modo tooPowerShell cmdlets do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="67e19-137">Make sure you switch tooPowerShell mode toouse hello Resource Manager cmdlets.</span></span> <span data-ttu-id="67e19-138">Para obter mais informações, consulte [Usando o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="67e19-138">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="67e19-139">Abra o console do PowerShell e conecte-se a conta de tooyour.</span><span class="sxs-lookup"><span data-stu-id="67e19-139">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="67e19-140">Use Olá toohelp de exemplo que você se conectar a seguir:</span><span class="sxs-lookup"><span data-stu-id="67e19-140">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="67e19-141">3. Criar TestVNet1</span><span class="sxs-lookup"><span data-stu-id="67e19-141">3. Create TestVNet1</span></span>
<span data-ttu-id="67e19-142">exemplo Hello abaixo cria uma rede virtual denominada TestVNet1 e três sub-redes, um GatewaySubnet chamado, um front-end chamado e back-end chamado um.</span><span class="sxs-lookup"><span data-stu-id="67e19-142">hello sample below creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="67e19-143">Ao substituir valores, é importante você sempre nomear sua sub-rede de gateway especificamente como GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="67e19-143">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="67e19-144">Se você usar outro nome, a criação do gateway falhará.</span><span class="sxs-lookup"><span data-stu-id="67e19-144">If you name it something else, your gateway creation will fail.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-active-active-mode"></a><span data-ttu-id="67e19-145">Etapa 2: criar o gateway VPN Olá para TestVNet1 com modo ativo-ativo</span><span class="sxs-lookup"><span data-stu-id="67e19-145">Step 2 - Create hello VPN gateway for TestVNet1 with active-active mode</span></span>
#### <a name="1-create-hello-public-ip-addresses-and-gateway-ip-configurations"></a><span data-ttu-id="67e19-146">1. Criar os endereços IP públicos hello e as configurações de IP do gateway</span><span class="sxs-lookup"><span data-stu-id="67e19-146">1. Create hello public IP addresses and gateway IP configurations</span></span>
<span data-ttu-id="67e19-147">Solicitação dois pública endereços toobe toohello alocado gateway IP que você criará para sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="67e19-147">Request two public IP addresses toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="67e19-148">Você também definirá sub-rede hello e as configurações de IP necessárias.</span><span class="sxs-lookup"><span data-stu-id="67e19-148">You'll also define hello subnet and IP configurations required.</span></span>

```powershell
$gw1pip1 = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$gw1pip2 = New-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1
$gw1ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf2 -Subnet $subnet1 -PublicIpAddress $gw1pip2
```

#### <a name="2-create-hello-vpn-gateway-with-active-active-configuration"></a><span data-ttu-id="67e19-149">2. Criar gateway VPN Olá com configuração ativo-ativo</span><span class="sxs-lookup"><span data-stu-id="67e19-149">2. Create hello VPN gateway with active-active configuration</span></span>
<span data-ttu-id="67e19-150">Crie gateway de rede virtual Olá para TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="67e19-150">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="67e19-151">Observe que há duas entradas GatewayIpConfig e Olá EnableActiveActiveFeature sinalizador é definido.</span><span class="sxs-lookup"><span data-stu-id="67e19-151">Note that there are two GatewayIpConfig entries, and hello EnableActiveActiveFeature flag is set.</span></span> <span data-ttu-id="67e19-152">Criar um gateway pode demorar um pouco (45 minutos ou mais toocomplete).</span><span class="sxs-lookup"><span data-stu-id="67e19-152">Creating a gateway can take a while (45 minutes or more toocomplete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1,$gw1ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN -EnableActiveActiveFeature -Debug
```

#### <a name="3-obtain-hello-gateway-public-ip-addresses-and-hello-bgp-peer-ip-address"></a><span data-ttu-id="67e19-153">3. Obter endereços IP públicos de gateway hello e um endereço de IP do par de BGP Olá</span><span class="sxs-lookup"><span data-stu-id="67e19-153">3. Obtain hello gateway public IP addresses and hello BGP Peer IP address</span></span>
<span data-ttu-id="67e19-154">Depois de criar o gateway Olá, você precisará de endereço de IP do par de BGP tooobtain Olá em Olá Gateway de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="67e19-154">Once hello gateway is created, you will need tooobtain hello BGP Peer IP address on hello Azure VPN Gateway.</span></span> <span data-ttu-id="67e19-155">Esse endereço é necessário tooconfigure Olá Gateway de VPN do Azure como um par de BGP para seus dispositivos VPN local.</span><span class="sxs-lookup"><span data-stu-id="67e19-155">This address is needed tooconfigure hello Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$gw1pip1 = Get-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1
$gw1pip2 = Get-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
```

<span data-ttu-id="67e19-156">Use Olá cmdlets tooshow Olá dois endereços IP públicos alocados para o gateway VPN e seus endereços IP de par de BGP correspondentes para cada instância de gateway a seguir:</span><span class="sxs-lookup"><span data-stu-id="67e19-156">Use hello following cmdlets tooshow hello two public IP addresses allocated for your VPN gateway, and their corresponding BGP Peer IP addresses for each gateway instance:</span></span>

```powershell

    PS D:\> $gw1pip1.IpAddress
    40.112.190.5

    PS D:\> $gw1pip2.IpAddress
    138.91.156.129

    PS D:\> $vnet1gw.BgpSettingsText
    {
      "Asn": 65010,
      "BgpPeeringAddress": "10.12.255.4,10.12.255.5",
      "PeerWeight": 0
    }
```

<span data-ttu-id="67e19-157">ordem de saudação de endereços IP públicos de saudação para instâncias de gateway hello e hello correspondente endereços de emparelhamento BGP são Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="67e19-157">hello order of hello public IP addresses for hello gateway instances and hello corresponding BGP Peering Addresses are hello same.</span></span> <span data-ttu-id="67e19-158">Neste exemplo, gateway Olá VM com o IP público de 40.112.190.5 usará 10.12.255.4 como seu endereço de emparelhamento BGP e gateway Olá com 138.91.156.129 usará 10.12.255.5.</span><span class="sxs-lookup"><span data-stu-id="67e19-158">In this example, hello gateway VM with public IP of 40.112.190.5 will use 10.12.255.4 as its BGP Peering Address, and hello gateway with 138.91.156.129 will use 10.12.255.5.</span></span> <span data-ttu-id="67e19-159">Essas informações são necessárias quando você configura seu local dispositivos VPN conectando toohello gateway de ativo-ativo.</span><span class="sxs-lookup"><span data-stu-id="67e19-159">This information is needed when you set up your on premises VPN devices connecting toohello active-active gateway.</span></span> <span data-ttu-id="67e19-160">gateway de saudação é mostrado no diagrama de saudação abaixo com todos os endereços:</span><span class="sxs-lookup"><span data-stu-id="67e19-160">hello gateway is shown in hello diagram below with all addresses:</span></span>

![gateway ativo-ativo](./media/vpn-gateway-activeactive-rm-powershell/active-active-gw.png)

<span data-ttu-id="67e19-162">Depois que o gateway de saudação é criado, você pode usar este gateway tooestablish ativo-ativo entre os locais ou a conexão de rede virtual a rede.</span><span class="sxs-lookup"><span data-stu-id="67e19-162">Once hello gateway is created, you can use this gateway tooestablish active-active cross-premises or VNet-to-VNet connection.</span></span> <span data-ttu-id="67e19-163">Olá seções a seguir orientará Olá etapas toocomplete Olá exercício.</span><span class="sxs-lookup"><span data-stu-id="67e19-163">hello following sections will walk through hello steps toocomplete hello exercise.</span></span>

## <span data-ttu-id="67e19-164"><a name ="aacrossprem"></a>Parte 2 – Estabelecer uma conexão entre os locais ativo-ativo</span><span class="sxs-lookup"><span data-stu-id="67e19-164"><a name ="aacrossprem"></a>Part 2 - Establish an active-active cross-premises connection</span></span>
<span data-ttu-id="67e19-165">tooestablish uma conexão entre locais, você precisa toocreate toorepresent um Gateway de rede Local seu dispositivo VPN no local e um gateway de VPN do Azure Conexão tooconnect Olá com o gateway de rede local hello.</span><span class="sxs-lookup"><span data-stu-id="67e19-165">tooestablish a cross-premises connection, you need toocreate a Local Network Gateway toorepresent your on-premises VPN device, and a Connection tooconnect hello Azure VPN gateway with hello local network gateway.</span></span> <span data-ttu-id="67e19-166">Neste exemplo, o gateway de VPN do Azure hello está no modo de ativo-ativo.</span><span class="sxs-lookup"><span data-stu-id="67e19-166">In this example, hello Azure VPN gateway is in active-active mode.</span></span> <span data-ttu-id="67e19-167">Como resultado, mesmo que haja apenas um local o dispositivo VPN (gateway de rede local) e recursos de uma conexão, ambas as instâncias de gateway VPN do Azure estabelecerá túneis VPN S2S com o dispositivo do local de saudação.</span><span class="sxs-lookup"><span data-stu-id="67e19-167">As a result, even though there is only one on-premises VPN device (local network gateway) and one connection resource, both Azure VPN gateway instances will establish S2S VPN tunnels with hello on-premises device.</span></span>

<span data-ttu-id="67e19-168">Antes de prosseguir, verifique se você concluiu a [Parte 1](#aagateway) deste exercício.</span><span class="sxs-lookup"><span data-stu-id="67e19-168">Before proceeding, please make sure you have completed [Part 1](#aagateway) of this exercise.</span></span>

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a><span data-ttu-id="67e19-169">Etapa 1: criar e configurar o gateway de rede local Olá</span><span class="sxs-lookup"><span data-stu-id="67e19-169">Step 1 - Create and configure hello local network gateway</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="67e19-170">1. Declare as variáveis</span><span class="sxs-lookup"><span data-stu-id="67e19-170">1. Declare your variables</span></span>
<span data-ttu-id="67e19-171">Este exercício continuará a configuração de saudação toobuild mostrada no diagrama de saudação.</span><span class="sxs-lookup"><span data-stu-id="67e19-171">This exercise will continue toobuild hello configuration shown in hello diagram.</span></span> <span data-ttu-id="67e19-172">Ser tooreplace se valores Olá Olá aqueles que você deseja toouse para sua configuração.</span><span class="sxs-lookup"><span data-stu-id="67e19-172">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG5 = "TestAARG5"
$Location5 = "West US"
$LNGName51 = "Site5_1"
$LNGPrefix51 = "10.52.255.253/32"
$LNGIP51 = "131.107.72.22"
$LNGASN5 = 65050
$BGPPeerIP51 = "10.52.255.253"
```

<span data-ttu-id="67e19-173">Algumas coisas toonote sobre parâmetros de gateway de rede local hello:</span><span class="sxs-lookup"><span data-stu-id="67e19-173">A couple of things toonote regarding hello local network gateway parameters:</span></span>

* <span data-ttu-id="67e19-174">gateway de rede local Olá pode estar em Olá mesmo ou outro local e o recurso grupo Olá gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="67e19-174">hello local network gateway can be in hello same or different location and resource group as hello VPN gateway.</span></span> <span data-ttu-id="67e19-175">Este exemplo mostra-los em grupos de recursos diferentes, mas em Olá mesmo local do Azure.</span><span class="sxs-lookup"><span data-stu-id="67e19-175">This example shows them in different resource groups but in hello same Azure location.</span></span>
* <span data-ttu-id="67e19-176">Se houver apenas um dispositivo VPN local, como mostrado acima, conexão de ativo-ativo Olá pode trabalhar com ou sem o protocolo BGP.</span><span class="sxs-lookup"><span data-stu-id="67e19-176">If there is only one on-premises VPN device as shown above, hello active-active connection can work with or without BGP protocol.</span></span> <span data-ttu-id="67e19-177">Este exemplo usa o BGP para conexão do hello entre locais.</span><span class="sxs-lookup"><span data-stu-id="67e19-177">This example uses BGP for hello cross-premises connection.</span></span>
* <span data-ttu-id="67e19-178">Se o BGP é habilitado, o prefixo de saudação precisar toodeclare para gateway de rede local Olá é endereço do host de saudação do seu endereço IP de par de BGP em seu dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="67e19-178">If BGP is enabled, hello prefix you need toodeclare for hello local network gateway is hello host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="67e19-179">Nesse caso, é um prefixo /32 de "10.52.255.253/32".</span><span class="sxs-lookup"><span data-stu-id="67e19-179">In this case, it's a /32 prefix of "10.52.255.253/32".</span></span>
* <span data-ttu-id="67e19-180">Como lembrete, você deve usar diferentes ASNs BGP entre suas redes locais e a VNet do Azure.</span><span class="sxs-lookup"><span data-stu-id="67e19-180">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="67e19-181">Se eles são hello mesmo, você precisará toochange sua VNet ASN se seu dispositivo VPN local já usa Olá ASN toopeer com outros vizinhos de BGP.</span><span class="sxs-lookup"><span data-stu-id="67e19-181">If they are hello same, you need toochange your VNet ASN if your on-premises VPN device already uses hello ASN toopeer with other BGP neighbors.</span></span>

#### <a name="2-create-hello-local-network-gateway-for-site5"></a><span data-ttu-id="67e19-182">2. Criar gateway de rede local Olá para Site5</span><span class="sxs-lookup"><span data-stu-id="67e19-182">2. Create hello local network gateway for Site5</span></span>
<span data-ttu-id="67e19-183">Antes de continuar, verifique se que você está conectado ainda tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="67e19-183">Before you continue, please make sure you are still connected tooSubscription 1.</span></span> <span data-ttu-id="67e19-184">Crie grupo de recursos de saudação se ainda não foi criado.</span><span class="sxs-lookup"><span data-stu-id="67e19-184">Create hello resource group if it is not yet created.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5
New-AzureRmLocalNetworkGateway -Name $LNGName51 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP51 -AddressPrefix $LNGPrefix51 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP51
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="67e19-185">Etapa 2: conectar-se o gateway de rede virtual hello e gateway de rede local</span><span class="sxs-lookup"><span data-stu-id="67e19-185">Step 2 - Connect hello VNet gateway and local network gateway</span></span>
#### <a name="1-get-hello-two-gateways"></a><span data-ttu-id="67e19-186">1. Obter Olá dois gateways</span><span class="sxs-lookup"><span data-stu-id="67e19-186">1. Get hello two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw1 = Get-AzureRmLocalNetworkGateway  -Name $LNGName51 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a><span data-ttu-id="67e19-187">2. Criar conexão de tooSite5 TestVNet1 Olá</span><span class="sxs-lookup"><span data-stu-id="67e19-187">2. Create hello TestVNet1 tooSite5 connection</span></span>
<span data-ttu-id="67e19-188">Nesta etapa, você irá criar conexão Olá de TestVNet1 tooSite5_1 com "EnableBGP" definido muito$ True.</span><span class="sxs-lookup"><span data-stu-id="67e19-188">In this step, you will create hello connection from TestVNet1 tooSite5_1 with "EnableBGP" set too$True.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection151 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw1 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-on-premises-vpn-device"></a><span data-ttu-id="67e19-189">3. Parâmetros VPN e BGP para seu dispositivo VPN local</span><span class="sxs-lookup"><span data-stu-id="67e19-189">3. VPN and BGP parameters for your on-premises VPN device</span></span>
<span data-ttu-id="67e19-190">exemplo Hello abaixo lista os parâmetros de saudação que será informado no hello seção de configuração de BGP em seu dispositivo VPN local para este exercício:</span><span class="sxs-lookup"><span data-stu-id="67e19-190">hello example below lists hello parameters you will enter into hello BGP configuration section on your on-premises VPN device for this exercise:</span></span>

    - <span data-ttu-id="67e19-191">Site5 ASN            : 65050</span><span class="sxs-lookup"><span data-stu-id="67e19-191">Site5 ASN            : 65050</span></span>
    - <span data-ttu-id="67e19-192">Site5 BGP IP         : 10.52.255.253</span><span class="sxs-lookup"><span data-stu-id="67e19-192">Site5 BGP IP         : 10.52.255.253</span></span>
    - <span data-ttu-id="67e19-193">O prefixo tooannounce: (por exemplo) 10.51.0.0/16 e 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="67e19-193">Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16</span></span>
    - <span data-ttu-id="67e19-194">Azure VNet ASN       : 65010</span><span class="sxs-lookup"><span data-stu-id="67e19-194">Azure VNet ASN       : 65010</span></span>
    - <span data-ttu-id="67e19-195">IP do BGP VNet do Azure 1: 10.12.255.4 para túnel too40.112.190.5</span><span class="sxs-lookup"><span data-stu-id="67e19-195">Azure VNet BGP IP 1  : 10.12.255.4 for tunnel too40.112.190.5</span></span>
    - <span data-ttu-id="67e19-196">IP do BGP VNet do Azure 2: 10.12.255.5 para túnel too138.91.156.129</span><span class="sxs-lookup"><span data-stu-id="67e19-196">Azure VNet BGP IP 2  : 10.12.255.5 for tunnel too138.91.156.129</span></span>
    - <span data-ttu-id="67e19-197">Rotas estáticas: destino 10.12.255.4/32, nexthop Olá VPN túnel interface too40.112.190.5 destino 10.12.255.5/32, nexthop Olá VPN túnel interface too138.91.156.129</span><span class="sxs-lookup"><span data-stu-id="67e19-197">Static routes        : Destination 10.12.255.4/32, nexthop hello VPN tunnel interface too40.112.190.5                        Destination 10.12.255.5/32, nexthop hello VPN tunnel interface too138.91.156.129</span></span>
    - <span data-ttu-id="67e19-198">eBGP Multihop: Verifique se a opção de "multihop" hello eBGP estiver habilitado no seu dispositivo, se necessário</span><span class="sxs-lookup"><span data-stu-id="67e19-198">eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed</span></span>

<span data-ttu-id="67e19-199">deve ser estabelecida a conexão Olá após alguns minutos e a sessão de emparelhamento Olá BGP iniciará uma vez estabelecida a conexão IPsec de saudação.</span><span class="sxs-lookup"><span data-stu-id="67e19-199">hello connection should be established after a few minutes, and hello BGP peering session will start once hello IPsec connection is established.</span></span> <span data-ttu-id="67e19-200">Este exemplo até o momento tiver configurado somente um dispositivo VPN local, resultando em um diagrama de saudação mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="67e19-200">This example so far has configured only one on-premises VPN device, resulting in hello diagram shown below:</span></span>

![ativo-ativo-entre-os-locais](./media/vpn-gateway-activeactive-rm-powershell/active-active.png)

### <a name="step-3---connect-two-on-premises-vpn-devices-toohello-active-active-vpn-gateway"></a><span data-ttu-id="67e19-202">Etapa 3 - conectar dois em dispositivos toohello ativa VPN gateway de VPN local</span><span class="sxs-lookup"><span data-stu-id="67e19-202">Step 3 - Connect two on-premises VPN devices toohello active-active VPN gateway</span></span>
<span data-ttu-id="67e19-203">Se você tiver dois dispositivos VPN Olá mesmo local rede, você pode obter redundância dupla conexão hello Azure toohello segundo VPN dispositivo de gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="67e19-203">If you have two VPN devices at hello same on-premises network, you can achieve dual redundancy by connecting hello Azure VPN gateway toohello second VPN device.</span></span>

#### <a name="1-create-hello-second-local-network-gateway-for-site5"></a><span data-ttu-id="67e19-204">1. Criar gateway de rede local segundo Olá para Site5</span><span class="sxs-lookup"><span data-stu-id="67e19-204">1. Create hello second local network gateway for Site5</span></span>
<span data-ttu-id="67e19-205">Observe que o endereço IP de gateway hello, prefixo de endereço e endereço emparelhamento BGP para gateway de rede local segundo Olá não devem sobrepor gateway de rede local anterior Olá para Olá mesmo rede no local.</span><span class="sxs-lookup"><span data-stu-id="67e19-205">Note that hello gateway IP address, address prefix, and BGP peering address for hello second local network gateway must not overlap with hello previous local network gateway for hello same on-premises network.</span></span>

```powershell
$LNGName52 = "Site5_2"
$LNGPrefix52 = "10.52.255.254/32"
$LNGIP52 = "131.107.72.23"
$BGPPeerIP52 = "10.52.255.254"

New-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP52 -AddressPrefix $LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP52
```

#### <a name="2-connect-hello-vnet-gateway-and-hello-second-local-network-gateway"></a><span data-ttu-id="67e19-206">2. Conecte-se o gateway de rede virtual hello e segundo gateway de rede local Olá</span><span class="sxs-lookup"><span data-stu-id="67e19-206">2. Connect hello VNet gateway and hello second local network gateway</span></span>
<span data-ttu-id="67e19-207">Criar conexão de saudação do TestVNet1 tooSite5_2 com "EnableBGP" definido muito$ True</span><span class="sxs-lookup"><span data-stu-id="67e19-207">Create hello connection from TestVNet1 tooSite5_2 with "EnableBGP" set too$True</span></span>

```powershell
$lng5gw2 = Get-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection152 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw2 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-second-on-premises-vpn-device"></a><span data-ttu-id="67e19-208">3. Parâmetros VPN e BGP para seu segundo dispositivo VPN local</span><span class="sxs-lookup"><span data-stu-id="67e19-208">3. VPN and BGP parameters for your second on-premises VPN device</span></span>
<span data-ttu-id="67e19-209">Da mesma forma, listas de parâmetros de saudação abaixo será informado no dispositivo VPN segundo hello:</span><span class="sxs-lookup"><span data-stu-id="67e19-209">Similarly, below lists hello parameters you will enter into hello second VPN device:</span></span>

```
- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP 1  : 10.12.255.4 for tunnel too40.112.190.5
- Azure VNet BGP IP 2  : 10.12.255.5 for tunnel too138.91.156.129
- Static routes        : Destination 10.12.255.4/32, nexthop hello VPN tunnel interface too40.112.190.5
                         Destination 10.12.255.5/32, nexthop hello VPN tunnel interface too138.91.156.129
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="67e19-210">Após o estabelecimento de conexão da saudação (túneis), você terá dois dispositivos VPN redundantes e túneis ao se conectar a sua rede local e o Azure:</span><span class="sxs-lookup"><span data-stu-id="67e19-210">Once hello connection (tunnels) are established, you will have dual redundant VPN devices and tunnels connecting your on-premises network and Azure:</span></span>

![redundância-dupla-entre-os-locais](./media/vpn-gateway-activeactive-rm-powershell/dual-redundancy.png)

## <span data-ttu-id="67e19-212"><a name ="aav2v"></a>Parte 3 – Estabelecer uma conexão VNet para VNet ativo-ativo</span><span class="sxs-lookup"><span data-stu-id="67e19-212"><a name ="aav2v"></a>Part 3 - Establish an active-active VNet-to-VNet connection</span></span>
<span data-ttu-id="67e19-213">Esta seção cria uma conexão VNet para VNet ativo-ativo com o BGP.</span><span class="sxs-lookup"><span data-stu-id="67e19-213">This section creates an active-active VNet-to-VNet connection with BGP.</span></span> 

<span data-ttu-id="67e19-214">instruções de saudação abaixo continuam nas etapas anteriores de Olá listadas acima.</span><span class="sxs-lookup"><span data-stu-id="67e19-214">hello instructions below continue from hello previous steps listed above.</span></span> <span data-ttu-id="67e19-215">Você deve concluir [parte 1](#aagateway) toocreate configurar TestVNet1 e Olá Gateway de VPN com o BGP.</span><span class="sxs-lookup"><span data-stu-id="67e19-215">You must complete [Part 1](#aagateway) toocreate and configure TestVNet1 and hello VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a><span data-ttu-id="67e19-216">Etapa 1 - criar TestVNet2 e hello gateway VPN</span><span class="sxs-lookup"><span data-stu-id="67e19-216">Step 1 - Create TestVNet2 and hello VPN gateway</span></span>
<span data-ttu-id="67e19-217">É importante toomake-se de que o espaço de endereço IP de saudação do hello nova rede virtual, TestVNet2, não coincide com nenhum dos seus intervalos de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="67e19-217">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="67e19-218">Neste exemplo, redes virtuais Olá pertencem toohello mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="67e19-218">In this example, hello virtual networks belong toohello same subscription.</span></span> <span data-ttu-id="67e19-219">Você pode configurar conexões de rede virtual a rede entre as diferentes assinaturas; Consulte também[configurar uma conexão de rede virtual a rede](vpn-gateway-vnet-vnet-rm-ps.md) toolearn mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="67e19-219">You can set up VNet-to-VNet connections between different subscriptions; please refer too[Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) toolearn more details.</span></span> <span data-ttu-id="67e19-220">Certifique-se de adicionar hello "-EnableBgp $True" ao criar hello conexões tooenable BGP.</span><span class="sxs-lookup"><span data-stu-id="67e19-220">Make sure you add hello "-EnableBgp $True" when creating hello connections tooenable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="67e19-221">1. Declare as variáveis</span><span class="sxs-lookup"><span data-stu-id="67e19-221">1. Declare your variables</span></span>
<span data-ttu-id="67e19-222">Ser tooreplace se valores Olá Olá aqueles que você deseja toouse para sua configuração.</span><span class="sxs-lookup"><span data-stu-id="67e19-222">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG2 = "TestAARG2"
$Location2 = "East US"
$VNetName2 = "TestVNet2"
$FESubName2 = "FrontEnd"
$BESubName2 = "Backend"
$GWSubName2 = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$VNet2ASN = 65020
$DNS2 = "8.8.8.8"
$GWName2 = "VNet2GW"
$GW2IPName1 = "VNet2GWIP1"
$GW2IPconf1 = "gw2ipconf1"
$GW2IPName2 = "VNet2GWIP2"
$GW2IPconf2 = "gw2ipconf2"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a><span data-ttu-id="67e19-223">2. Criar TestVNet2 no novo grupo de recursos Olá</span><span class="sxs-lookup"><span data-stu-id="67e19-223">2. Create TestVNet2 in hello new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-active-active-vpn-gateway-for-testvnet2"></a><span data-ttu-id="67e19-224">3. Criar gateway VPN Olá ativo-ativo para TestVNet2</span><span class="sxs-lookup"><span data-stu-id="67e19-224">3. Create hello active-active VPN gateway for TestVNet2</span></span>
<span data-ttu-id="67e19-225">Solicitação dois pública endereços toobe toohello alocado gateway IP que você criará para sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="67e19-225">Request two public IP addresses toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="67e19-226">Você também definirá sub-rede hello e as configurações de IP necessárias.</span><span class="sxs-lookup"><span data-stu-id="67e19-226">You'll also define hello subnet and IP configurations required.</span></span>

```powershell
$gw2pip1 = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$gw2pip2 = New-AzureRmPublicIpAddress -Name $GW2IPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2 = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1
$gw2ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf2 -Subnet $subnet2 -PublicIpAddress $gw2pip2
```

<span data-ttu-id="67e19-227">Crie gateway VPN Olá com hello como número e hello sinalizador de "EnableActiveActiveFeature".</span><span class="sxs-lookup"><span data-stu-id="67e19-227">Create hello VPN gateway with hello AS number and hello "EnableActiveActiveFeature" flag.</span></span> <span data-ttu-id="67e19-228">Observe que você deve substituir o padrão de saudação ASN em seus gateways de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="67e19-228">Note that you must override hello default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="67e19-229">Olá ASNs para Olá conectado VNets deve ser diferente tooenable BGP e roteamento de tráfego.</span><span class="sxs-lookup"><span data-stu-id="67e19-229">hello ASNs for hello connected VNets must be different tooenable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1,$gw2ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet2ASN -EnableActiveActiveFeature
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="67e19-230">Etapa 2: conectar gateways de TestVNet1 e TestVNet2 Olá</span><span class="sxs-lookup"><span data-stu-id="67e19-230">Step 2 - Connect hello TestVNet1 and TestVNet2 gateways</span></span>
<span data-ttu-id="67e19-231">Neste exemplo, ambos os gateways estão em Olá mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="67e19-231">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="67e19-232">Você pode concluir esta etapa no hello mesma sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="67e19-232">You can complete this step in hello same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="67e19-233">1. Obter ambos os gateways</span><span class="sxs-lookup"><span data-stu-id="67e19-233">1. Get both gateways</span></span>
<span data-ttu-id="67e19-234">Certifique-se de entrar e conectar-se tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="67e19-234">Make sure you log in and connect tooSubscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="67e19-235">2. Criar ambas as conexões</span><span class="sxs-lookup"><span data-stu-id="67e19-235">2. Create both connections</span></span>
<span data-ttu-id="67e19-236">Nesta etapa, você criará conexão Olá de TestVNet1 tooTestVNet2 e conexão de saudação do TestVNet2 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="67e19-236">In this step, you will create hello connection from TestVNet1 tooTestVNet2, and hello connection from TestVNet2 tooTestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="67e19-237">Ser tooenable se BGP para ambas as conexões.</span><span class="sxs-lookup"><span data-stu-id="67e19-237">Be sure tooenable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="67e19-238">Depois de concluir essas etapas, ser estabeleça conexão Olá em alguns minutos e sessão de emparelhamento de BGP hello serão backup após a conclusão da conexão Olá VNet para VNet com redundância dupla:</span><span class="sxs-lookup"><span data-stu-id="67e19-238">After completing these steps, hello connection will be establish in a few minutes, and hello BGP peering session will be up once hello VNet-to-VNet connection is completed with dual redundancy:</span></span>

![ativo-ativo-v2v](./media/vpn-gateway-activeactive-rm-powershell/vnet-to-vnet.png)

## <span data-ttu-id="67e19-240"><a name ="aaupdate"></a>Parte 4 – Atualizar o gateway existente entre ativo-ativo e ativo-em espera</span><span class="sxs-lookup"><span data-stu-id="67e19-240"><a name ="aaupdate"></a>Part 4 - Update existing gateway between active-active and active-standby</span></span>
<span data-ttu-id="67e19-241">última seção do Hello descrevem como você pode configurar um gateway de VPN do Azure existente ativo-ativo tooactive do modo de espera, ou vice-versa.</span><span class="sxs-lookup"><span data-stu-id="67e19-241">hello last section will describe how you can configure an existing Azure VPN gateway from active-standby tooactive-active mode, or vice versa.</span></span>

> [!NOTE]
> <span data-ttu-id="67e19-242">Esta seção inclui Olá etapas tooresize um herdado SKU (SKU antigo) de um gateway VPN já criado do tooHighPerformance padrão.</span><span class="sxs-lookup"><span data-stu-id="67e19-242">This section includes hello steps tooresize a legacy SKU (old SKU) of an already created VPN gateway from Standard tooHighPerformance.</span></span> <span data-ttu-id="67e19-243">Essas etapas não atualizarem um antigo tooone herdado de SKU de saudação SKUs de novo.</span><span class="sxs-lookup"><span data-stu-id="67e19-243">These steps do not upgrade an old legacy SKU tooone of hello new SKUs.</span></span>
> 
> 

### <a name="configure-an-active-standby-gateway-tooactive-active-gateway"></a><span data-ttu-id="67e19-244">Configurar um gateway ativa / em espera de tooactive-ativo</span><span class="sxs-lookup"><span data-stu-id="67e19-244">Configure an active-standby gateway tooactive-active gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="67e19-245">1. Parâmetros do gateway</span><span class="sxs-lookup"><span data-stu-id="67e19-245">1. Gateway parameters</span></span>
<span data-ttu-id="67e19-246">saudação de exemplo a seguir converte um gateway ativa / em espera em um gateway de ativo-ativo.</span><span class="sxs-lookup"><span data-stu-id="67e19-246">hello following example converts an active-standby gateway into an active-active gateway.</span></span> <span data-ttu-id="67e19-247">Você precisa toocreate outro endereço IP público e adiciona uma segunda configuração de IP do Gateway.</span><span class="sxs-lookup"><span data-stu-id="67e19-247">You need toocreate another public IP address, then add a second Gateway IP configuration.</span></span> <span data-ttu-id="67e19-248">Abaixo mostra hello parâmetros usados:</span><span class="sxs-lookup"><span data-stu-id="67e19-248">Below shows hello parameters used:</span></span>

```powershell
$GWName = "TestVNetAA1GW"
$VNetName = "TestVNetAA1"
$RG = "TestVPNActiveActive01"
$GWIPName2 = "gwpip2"
$GWIPconf2 = "gw1ipconf2"

$vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$location = $gw.Location
```

#### <a name="2-create-hello-public-ip-address-then-add-hello-second-gateway-ip-configuration"></a><span data-ttu-id="67e19-249">2. Criar endereço IP público de saudação, em seguida, Adicionar configuração de IP de gateway segundo Olá</span><span class="sxs-lookup"><span data-stu-id="67e19-249">2. Create hello public IP address, then add hello second gateway IP configuration</span></span>

```powershell
$gwpip2 = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG -Location $location -AllocationMethod Dynamic
Add-AzureRmVirtualNetworkGatewayIpConfig -VirtualNetworkGateway $gw -Name $GWIPconf2 -Subnet $subnet -PublicIpAddress $gwpip2
```

#### <a name="3-enable-active-active-mode-and-update-hello-gateway"></a><span data-ttu-id="67e19-250">3. Ativar Ativa modo e atualização de gateway de saudação</span><span class="sxs-lookup"><span data-stu-id="67e19-250">3. Enable active-active mode and update hello gateway</span></span>
<span data-ttu-id="67e19-251">Você deve definir o objeto de gateway Olá atualização real do PowerShell tootrigger hello.</span><span class="sxs-lookup"><span data-stu-id="67e19-251">You must set hello gateway object in PowerShell tootrigger hello actual update.</span></span> <span data-ttu-id="67e19-252">Olá SKU do gateway de rede virtual Olá deve também ser alterado tooHighPerformance (redimensionado) desde que ele foi criado anteriormente como padrão.</span><span class="sxs-lookup"><span data-stu-id="67e19-252">hello SKU of hello virtual network gateway must also be changed (resized) tooHighPerformance since it was created previously as Standard.</span></span>

```powershell
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -EnableActiveActiveFeature -GatewaySku HighPerformance
```

<span data-ttu-id="67e19-253">Essa atualização pode levar 30 minutos too45.</span><span class="sxs-lookup"><span data-stu-id="67e19-253">This update can take 30 too45 minutes.</span></span>

### <a name="configure-an-active-active-gateway-tooactive-standby-gateway"></a><span data-ttu-id="67e19-254">Configure um gateway de espera de tooactive gateway ativo-ativo</span><span class="sxs-lookup"><span data-stu-id="67e19-254">Configure an active-active gateway tooactive-standby gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="67e19-255">1. Parâmetros do gateway</span><span class="sxs-lookup"><span data-stu-id="67e19-255">1. Gateway parameters</span></span>
<span data-ttu-id="67e19-256">Use Olá mesmo parâmetros acima, obter o nome de Olá Olá da configuração de IP desejar tooremove.</span><span class="sxs-lookup"><span data-stu-id="67e19-256">Use hello same parameters as above, get hello name of hello IP configuration you want tooremove.</span></span>

```powershell
$GWName = "TestVNetAA1GW"
$RG = "TestVPNActiveActive01"

$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$ipconfname = $gw.IpConfigurations[1].Name
```

#### <a name="2-remove-hello-gateway-ip-configuration-and-disable-hello-active-active-mode"></a><span data-ttu-id="67e19-257">2. Remover configuração de IP de gateway hello e desativar o modo de ativo-ativo de saudação</span><span class="sxs-lookup"><span data-stu-id="67e19-257">2. Remove hello gateway IP configuration and disable hello active-active mode</span></span>
<span data-ttu-id="67e19-258">Da mesma forma, você deve definir o objeto de gateway de saudação em atualização real do PowerShell tootrigger hello.</span><span class="sxs-lookup"><span data-stu-id="67e19-258">Similarly, you must set hello gateway object in PowerShell tootrigger hello actual update.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGatewayIpConfig -Name $ipconfname -VirtualNetworkGateway $gw
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -DisableActiveActiveFeature
```

<span data-ttu-id="67e19-259">Essa atualização pode levar até too30 muito 45 minutos.</span><span class="sxs-lookup"><span data-stu-id="67e19-259">This update can take up too30 too 45 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67e19-260">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="67e19-260">Next steps</span></span>
<span data-ttu-id="67e19-261">Quando a conexão for concluída, você pode adicionar máquinas virtuais tooyour as redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="67e19-261">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="67e19-262">Veja [Criar uma máquina virtual](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obter as etapas.</span><span class="sxs-lookup"><span data-stu-id="67e19-262">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
