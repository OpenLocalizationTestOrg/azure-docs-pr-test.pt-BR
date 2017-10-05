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
ms.openlocfilehash: a9f71b566ffdb163f95634835f64589a700d712f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-active-active-s2s-vpn-connections-with-azure-vpn-gateways"></a><span data-ttu-id="3cd50-103">Configurar conexões VPN S2S ativa-ativa com Gateways de VPN</span><span class="sxs-lookup"><span data-stu-id="3cd50-103">Configure active-active S2S VPN connections with Azure VPN Gateways</span></span>

<span data-ttu-id="3cd50-104">Este artigo explica as etapas para criar conexões VNet para VNet e entre instalações ativo-ativo usando o modelo de implantação do Resource Manager e o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3cd50-104">This article walks you through the steps to create active-active cross-premises and VNet-to-VNet connections using the Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-highly-available-cross-premises-connections"></a><span data-ttu-id="3cd50-105">Sobre conexões altamente disponíveis entre instalações</span><span class="sxs-lookup"><span data-stu-id="3cd50-105">About Highly Available Cross-Premises Connections</span></span>
<span data-ttu-id="3cd50-106">Para obter alta disponibilidade para conectividade entre instalações e VNet para VNet, você deve implantar vários gateways de VPN e estabelecer várias conexões paralelas entre suas redes e o Azure.</span><span class="sxs-lookup"><span data-stu-id="3cd50-106">To achieve high availability for cross-premises and VNet-to-VNet connectivity, you should deploy multiple VPN gateways and establish multiple parallel connections between your networks and Azure.</span></span> <span data-ttu-id="3cd50-107">Consulte [Conectividade Altamente Disponível entre os Locais e VNet para VNet](vpn-gateway-highlyavailable.md) para obter uma visão geral das opções de conectividade e topologia.</span><span class="sxs-lookup"><span data-stu-id="3cd50-107">Please see [Highly Available Cross-Premises and VNet-to-VNet Connectivity](vpn-gateway-highlyavailable.md) for an overview of connectivity options and topology.</span></span>

<span data-ttu-id="3cd50-108">Este artigo fornece as instruções para configurar uma conexão VPN entre os locais ativo-ativo e uma conexão ativo-ativo entre duas redes virtuais:</span><span class="sxs-lookup"><span data-stu-id="3cd50-108">This article provides the instructions to set up an active-active cross-premises VPN connection, and active-active connection between two virtual networks:</span></span>

* [<span data-ttu-id="3cd50-109">Parte 1 – Criar e configurar seu gateway de VPN do Azure no modo ativo-ativo</span><span class="sxs-lookup"><span data-stu-id="3cd50-109">Part 1 - Create and configure your Azure VPN gateway in active-active mode</span></span>](#aagateway)
* [<span data-ttu-id="3cd50-110">Parte 2 – Estabelecer conexões entre os locais ativo-ativo</span><span class="sxs-lookup"><span data-stu-id="3cd50-110">Part 2 - Establish active-active cross-premises connections</span></span>](#aacrossprem)
* [<span data-ttu-id="3cd50-111">Parte 3 – Estabelecer conexões VNet para VNet ativo-ativo</span><span class="sxs-lookup"><span data-stu-id="3cd50-111">Part 3 - Establish active-active VNet-to-VNet connections</span></span>](#aav2v)
* [<span data-ttu-id="3cd50-112">Parte 4 – Atualizar o gateway existente entre ativo-ativo e ativo-em espera</span><span class="sxs-lookup"><span data-stu-id="3cd50-112">Part 4 - Update existing gateway between active-active and active-standby</span></span>](#aaupdate)

<span data-ttu-id="3cd50-113">Você pode combiná-los para criar uma topologia de rede mais complexa e altamente disponível que atenda às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="3cd50-113">You can combine these together to build a more complex, highly available network topology that meets your needs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3cd50-114">Observe que o modo ativo-ativo usa somente os seguintes SKUs:</span><span class="sxs-lookup"><span data-stu-id="3cd50-114">Please note that the active-active mode uses only the following SKUs:</span></span> 
  * <span data-ttu-id="3cd50-115">VpnGw1, VpnGw2, VpnGw3</span><span class="sxs-lookup"><span data-stu-id="3cd50-115">VpnGw1, VpnGw2, VpnGw3</span></span>
  * <span data-ttu-id="3cd50-116">HighPerformance (para SKUs herdados antigos)</span><span class="sxs-lookup"><span data-stu-id="3cd50-116">HighPerformance (for old legacy SKUs)</span></span>
> 
> 

## <span data-ttu-id="3cd50-117"><a name ="aagateway"></a>Parte 1 – Criar e configurar os gateways de VPN ativo-ativo</span><span class="sxs-lookup"><span data-stu-id="3cd50-117"><a name ="aagateway"></a>Part 1 - Create and configure active-active VPN gateways</span></span>
<span data-ttu-id="3cd50-118">As etapas a seguir configurarão seu gateway de VPN do Azure nos modos ativo-ativo.</span><span class="sxs-lookup"><span data-stu-id="3cd50-118">The following steps will configure your Azure VPN gateway in active-active modes.</span></span> <span data-ttu-id="3cd50-119">As principais diferenças entre os gateways ativo-ativo e ativo-em espera:</span><span class="sxs-lookup"><span data-stu-id="3cd50-119">The key differences between the active-active and active-standby gateways:</span></span>

* <span data-ttu-id="3cd50-120">Você precisa criar duas configurações de IP do gateway com dois endereços IP públicos</span><span class="sxs-lookup"><span data-stu-id="3cd50-120">You need to create two Gateway IP configurations with two public IP addresses</span></span>
* <span data-ttu-id="3cd50-121">Você precisa definir o sinalizador EnableActiveActiveFeature</span><span class="sxs-lookup"><span data-stu-id="3cd50-121">You need set the EnableActiveActiveFeature flag</span></span>
* <span data-ttu-id="3cd50-122">O SKU de gateway deve ser VpnGw1, VpnGw2, VpnGw3 ou HighPerformance (SKU herdado).</span><span class="sxs-lookup"><span data-stu-id="3cd50-122">The gateway SKU must be VpnGw1, VpnGw2, VpnGw3, or HighPerformance (legacy SKU).</span></span>

<span data-ttu-id="3cd50-123">As outras propriedades são as mesmas que os gateways não ativo-ativo.</span><span class="sxs-lookup"><span data-stu-id="3cd50-123">The other properties are the same as the non-active-active gateways.</span></span> 

### <a name="before-you-begin"></a><span data-ttu-id="3cd50-124">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="3cd50-124">Before you begin</span></span>
* <span data-ttu-id="3cd50-125">Verifique se você tem uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="3cd50-125">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="3cd50-126">Se ainda não tiver uma assinatura do Azure, você poderá ativar os [Benefícios do assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se para obter uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3cd50-126">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="3cd50-127">Você precisará instalar os cmdlets do Azure Resource Manager PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3cd50-127">You'll need to install the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="3cd50-128">Consulte [Visão geral do Azure PowerShell](/powershell/azure/overview) para obter mais informações sobre como instalar os cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3cd50-128">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span>

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="3cd50-129">Etapa 1 - Criar e configurar VNet1</span><span class="sxs-lookup"><span data-stu-id="3cd50-129">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="3cd50-130">1. Declare as variáveis</span><span class="sxs-lookup"><span data-stu-id="3cd50-130">1. Declare your variables</span></span>
<span data-ttu-id="3cd50-131">Para este exercício, começaremos declarando nossa variáveis.</span><span class="sxs-lookup"><span data-stu-id="3cd50-131">For this exercise, we'll start by declaring our variables.</span></span> <span data-ttu-id="3cd50-132">O exemplo a seguir declara as variáveis usando os valores para este exercício.</span><span class="sxs-lookup"><span data-stu-id="3cd50-132">The example below declares the variables using the values for this exercise.</span></span> <span data-ttu-id="3cd50-133">Certifique-se de substituir os valores pelos seus próprios ao configurar para a produção.</span><span class="sxs-lookup"><span data-stu-id="3cd50-133">Be sure to replace the values with your own when configuring for production.</span></span> <span data-ttu-id="3cd50-134">Se você estiver executando as etapas para se familiarizar com esse tipo de configuração, poderá usar essas variáveis.</span><span class="sxs-lookup"><span data-stu-id="3cd50-134">You can use these variables if you are running through the steps to become familiar with this type of configuration.</span></span> <span data-ttu-id="3cd50-135">Modifique as variáveis e, em seguida, copie e cole em seu console do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3cd50-135">Modify the variables, and then copy and paste into your PowerShell console.</span></span>

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

#### <a name="2-connect-to-your-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="3cd50-136">2. Conectar à sua assinatura do Azure e criar um novo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="3cd50-136">2. Connect to your subscription and create a new resource group</span></span>
<span data-ttu-id="3cd50-137">Alterne para o modo do PowerShell para usar os cmdlets do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="3cd50-137">Make sure you switch to PowerShell mode to use the Resource Manager cmdlets.</span></span> <span data-ttu-id="3cd50-138">Para obter mais informações, consulte [Usando o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="3cd50-138">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="3cd50-139">Abra o console do PowerShell e conecte-se à sua conta.</span><span class="sxs-lookup"><span data-stu-id="3cd50-139">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="3cd50-140">Use o exemplo a seguir para ajudar com a conexão:</span><span class="sxs-lookup"><span data-stu-id="3cd50-140">Use the following sample to help you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="3cd50-141">3. Criar TestVNet1</span><span class="sxs-lookup"><span data-stu-id="3cd50-141">3. Create TestVNet1</span></span>
<span data-ttu-id="3cd50-142">O exemplo abaixo cria uma rede virtual denominada TestVNet1 e três sub-redes: GatewaySubnet, FrontEnd e Backend.</span><span class="sxs-lookup"><span data-stu-id="3cd50-142">The sample below creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="3cd50-143">Ao substituir valores, é importante você sempre nomear sua sub-rede de gateway especificamente como GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="3cd50-143">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="3cd50-144">Se você usar outro nome, a criação do gateway falhará.</span><span class="sxs-lookup"><span data-stu-id="3cd50-144">If you name it something else, your gateway creation will fail.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-the-vpn-gateway-for-testvnet1-with-active-active-mode"></a><span data-ttu-id="3cd50-145">Etapa 2 – Criar o gateway de VPN para TestVNet1 com modo ativo-ativo</span><span class="sxs-lookup"><span data-stu-id="3cd50-145">Step 2 - Create the VPN gateway for TestVNet1 with active-active mode</span></span>
#### <a name="1-create-the-public-ip-addresses-and-gateway-ip-configurations"></a><span data-ttu-id="3cd50-146">1. Criar os endereços IP públicos e as configurações de IP do gateway</span><span class="sxs-lookup"><span data-stu-id="3cd50-146">1. Create the public IP addresses and gateway IP configurations</span></span>
<span data-ttu-id="3cd50-147">Solicite dois endereços IP públicos para serem alocados ao gateway que você criará para sua VNet.</span><span class="sxs-lookup"><span data-stu-id="3cd50-147">Request two public IP addresses to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="3cd50-148">Você também definirá as configurações de IP e sub-rede necessárias.</span><span class="sxs-lookup"><span data-stu-id="3cd50-148">You'll also define the subnet and IP configurations required.</span></span>

```powershell
$gw1pip1 = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$gw1pip2 = New-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1
$gw1ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf2 -Subnet $subnet1 -PublicIpAddress $gw1pip2
```

#### <a name="2-create-the-vpn-gateway-with-active-active-configuration"></a><span data-ttu-id="3cd50-149">2. Criar o gateway de VPN com configuração ativo-ativo</span><span class="sxs-lookup"><span data-stu-id="3cd50-149">2. Create the VPN gateway with active-active configuration</span></span>
<span data-ttu-id="3cd50-150">Crie o gateway de rede virtual para TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="3cd50-150">Create the virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="3cd50-151">Observe que há duas entradas GatewayIpConfig, e o sinalizador EnableActiveActiveFeature foi definido.</span><span class="sxs-lookup"><span data-stu-id="3cd50-151">Note that there are two GatewayIpConfig entries, and the EnableActiveActiveFeature flag is set.</span></span> <span data-ttu-id="3cd50-152">Criar um gateway pode demorar um pouco (45 minutos ou mais para ser concluído).</span><span class="sxs-lookup"><span data-stu-id="3cd50-152">Creating a gateway can take a while (45 minutes or more to complete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1,$gw1ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN -EnableActiveActiveFeature -Debug
```

#### <a name="3-obtain-the-gateway-public-ip-addresses-and-the-bgp-peer-ip-address"></a><span data-ttu-id="3cd50-153">3. Obter os endereços IP públicos do gateway e o endereço IP do par no nível de protocolo BGP</span><span class="sxs-lookup"><span data-stu-id="3cd50-153">3. Obtain the gateway public IP addresses and the BGP Peer IP address</span></span>
<span data-ttu-id="3cd50-154">Depois de criar o gateway, você precisará obter o endereço IP do par no nível de protocolo BGP no Gateway de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="3cd50-154">Once the gateway is created, you will need to obtain the BGP Peer IP address on the Azure VPN Gateway.</span></span> <span data-ttu-id="3cd50-155">Esse endereço é necessário para configurar o Gateway de VPN do Azure como um par no nível de protocolo BGP para os dispositivos VPN locais.</span><span class="sxs-lookup"><span data-stu-id="3cd50-155">This address is needed to configure the Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$gw1pip1 = Get-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1
$gw1pip2 = Get-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
```

<span data-ttu-id="3cd50-156">Use os seguintes cmdlets para mostrar os dois endereços IP públicos alocados para seu gateway de VPN e seus endereços IP do par no nível de protocolo BGP correspondentes para cada instância do gateway:</span><span class="sxs-lookup"><span data-stu-id="3cd50-156">Use the following cmdlets to show the two public IP addresses allocated for your VPN gateway, and their corresponding BGP Peer IP addresses for each gateway instance:</span></span>

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

<span data-ttu-id="3cd50-157">A ordem dos endereços IP públicos para as instâncias do gateway e os endereços de emparelhamento via protocolo BGP correspondentes são os mesmos.</span><span class="sxs-lookup"><span data-stu-id="3cd50-157">The order of the public IP addresses for the gateway instances and the corresponding BGP Peering Addresses are the same.</span></span> <span data-ttu-id="3cd50-158">Neste exemplo, a VM do gateway com o IP público 40.112.190.5 usará 10.12.255.4 como seu endereço de emparelhamento via protocolo BGP, e o gateway com 138.91.156.129 usará 10.12.255.5.</span><span class="sxs-lookup"><span data-stu-id="3cd50-158">In this example, the gateway VM with public IP of 40.112.190.5 will use 10.12.255.4 as its BGP Peering Address, and the gateway with 138.91.156.129 will use 10.12.255.5.</span></span> <span data-ttu-id="3cd50-159">Essas informações são necessárias quando você configura os dispositivos VPN locais que se conectam ao gateway ativo-ativo.</span><span class="sxs-lookup"><span data-stu-id="3cd50-159">This information is needed when you set up your on premises VPN devices connecting to the active-active gateway.</span></span> <span data-ttu-id="3cd50-160">O gateway é mostrado no diagrama abaixo, com todos os endereços:</span><span class="sxs-lookup"><span data-stu-id="3cd50-160">The gateway is shown in the diagram below with all addresses:</span></span>

![gateway ativo-ativo](./media/vpn-gateway-activeactive-rm-powershell/active-active-gw.png)

<span data-ttu-id="3cd50-162">Depois de criar o gateway, você poderá usá-lo para estabelecer a conexão entre os locais ativo-ativo ou a conexão VNet para VNet.</span><span class="sxs-lookup"><span data-stu-id="3cd50-162">Once the gateway is created, you can use this gateway to establish active-active cross-premises or VNet-to-VNet connection.</span></span> <span data-ttu-id="3cd50-163">As seções a seguir explicam as etapas para concluir o exercício.</span><span class="sxs-lookup"><span data-stu-id="3cd50-163">The following sections will walk through the steps to complete the exercise.</span></span>

## <span data-ttu-id="3cd50-164"><a name ="aacrossprem"></a>Parte 2 – Estabelecer uma conexão entre os locais ativo-ativo</span><span class="sxs-lookup"><span data-stu-id="3cd50-164"><a name ="aacrossprem"></a>Part 2 - Establish an active-active cross-premises connection</span></span>
<span data-ttu-id="3cd50-165">Para estabelecer uma conexão entre instalações, você precisará criar um Gateway de Rede Local para representar o dispositivo VPN local e uma Conexão para conectar o gateway de VPN do Azure com ao gateway de rede local.</span><span class="sxs-lookup"><span data-stu-id="3cd50-165">To establish a cross-premises connection, you need to create a Local Network Gateway to represent your on-premises VPN device, and a Connection to connect the Azure VPN gateway with the local network gateway.</span></span> <span data-ttu-id="3cd50-166">Neste exemplo, o gateway de VPN do Azure está no modo ativo-ativo.</span><span class="sxs-lookup"><span data-stu-id="3cd50-166">In this example, the Azure VPN gateway is in active-active mode.</span></span> <span data-ttu-id="3cd50-167">Como resultado, mesmo que haja apenas um dispositivo VPN local (gateway de rede local) e um recurso de conexão, as duas instâncias de gateway de VPN do Azure estabelecerão túneis de VPN S2S com o dispositivo local.</span><span class="sxs-lookup"><span data-stu-id="3cd50-167">As a result, even though there is only one on-premises VPN device (local network gateway) and one connection resource, both Azure VPN gateway instances will establish S2S VPN tunnels with the on-premises device.</span></span>

<span data-ttu-id="3cd50-168">Antes de prosseguir, verifique se você concluiu a [Parte 1](#aagateway) deste exercício.</span><span class="sxs-lookup"><span data-stu-id="3cd50-168">Before proceeding, please make sure you have completed [Part 1](#aagateway) of this exercise.</span></span>

### <a name="step-1---create-and-configure-the-local-network-gateway"></a><span data-ttu-id="3cd50-169">Etapa 1 - Criar e configurar o gateway de rede local</span><span class="sxs-lookup"><span data-stu-id="3cd50-169">Step 1 - Create and configure the local network gateway</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="3cd50-170">1. Declare as variáveis</span><span class="sxs-lookup"><span data-stu-id="3cd50-170">1. Declare your variables</span></span>
<span data-ttu-id="3cd50-171">Este exercício continuará a compilar a configuração mostrada no diagrama.</span><span class="sxs-lookup"><span data-stu-id="3cd50-171">This exercise will continue to build the configuration shown in the diagram.</span></span> <span data-ttu-id="3cd50-172">Não se esqueça de substituir os valores com aqueles que você deseja usar para sua configuração.</span><span class="sxs-lookup"><span data-stu-id="3cd50-172">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

```powershell
$RG5 = "TestAARG5"
$Location5 = "West US"
$LNGName51 = "Site5_1"
$LNGPrefix51 = "10.52.255.253/32"
$LNGIP51 = "131.107.72.22"
$LNGASN5 = 65050
$BGPPeerIP51 = "10.52.255.253"
```

<span data-ttu-id="3cd50-173">Algumas coisas para observar relacionadas aos parâmetros de gateway de rede:</span><span class="sxs-lookup"><span data-stu-id="3cd50-173">A couple of things to note regarding the local network gateway parameters:</span></span>

* <span data-ttu-id="3cd50-174">O gateway de rede local pode estar no mesmo ou em outro local e grupo de recursos como o gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="3cd50-174">The local network gateway can be in the same or different location and resource group as the VPN gateway.</span></span> <span data-ttu-id="3cd50-175">Este exemplo os mostra em grupos de recursos diferentes, mas na mesma localização do Azure.</span><span class="sxs-lookup"><span data-stu-id="3cd50-175">This example shows them in different resource groups but in the same Azure location.</span></span>
* <span data-ttu-id="3cd50-176">Se houver apenas um dispositivo VPN local, conforme mostrado acima, a conexão ativo-ativo poderá funcionar com ou sem o protocolo BGP.</span><span class="sxs-lookup"><span data-stu-id="3cd50-176">If there is only one on-premises VPN device as shown above, the active-active connection can work with or without BGP protocol.</span></span> <span data-ttu-id="3cd50-177">Este exemplo usa o BGP para a conexão entre os locais.</span><span class="sxs-lookup"><span data-stu-id="3cd50-177">This example uses BGP for the cross-premises connection.</span></span>
* <span data-ttu-id="3cd50-178">Se o BGP for habilitado, o prefixo que você precisará declarar para o gateway de rede local é o endereço de host do seu endereço IP do par no nível de protocolo BGP em seu dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="3cd50-178">If BGP is enabled, the prefix you need to declare for the local network gateway is the host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="3cd50-179">Nesse caso, é um prefixo /32 de "10.52.255.253/32".</span><span class="sxs-lookup"><span data-stu-id="3cd50-179">In this case, it's a /32 prefix of "10.52.255.253/32".</span></span>
* <span data-ttu-id="3cd50-180">Como lembrete, você deve usar diferentes ASNs BGP entre suas redes locais e a VNet do Azure.</span><span class="sxs-lookup"><span data-stu-id="3cd50-180">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="3cd50-181">Se eles forem iguais, você precisará alterar seu ASN VNet se o dispositivo VPN local já usar o ASN para emparelhar com outros vizinhos de BGP.</span><span class="sxs-lookup"><span data-stu-id="3cd50-181">If they are the same, you need to change your VNet ASN if your on-premises VPN device already uses the ASN to peer with other BGP neighbors.</span></span>

#### <a name="2-create-the-local-network-gateway-for-site5"></a><span data-ttu-id="3cd50-182">2. Criar o gateway de rede local para Site5</span><span class="sxs-lookup"><span data-stu-id="3cd50-182">2. Create the local network gateway for Site5</span></span>
<span data-ttu-id="3cd50-183">Antes de continuar, verifique se que você ainda está conectado à Assinatura 1.</span><span class="sxs-lookup"><span data-stu-id="3cd50-183">Before you continue, please make sure you are still connected to Subscription 1.</span></span> <span data-ttu-id="3cd50-184">Crie o grupo de recursos se ele ainda não tiver sido criado.</span><span class="sxs-lookup"><span data-stu-id="3cd50-184">Create the resource group if it is not yet created.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5
New-AzureRmLocalNetworkGateway -Name $LNGName51 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP51 -AddressPrefix $LNGPrefix51 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP51
```

### <a name="step-2---connect-the-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="3cd50-185">Etapa 2 - Conectar o gateway de VNet e o gateway de rede local</span><span class="sxs-lookup"><span data-stu-id="3cd50-185">Step 2 - Connect the VNet gateway and local network gateway</span></span>
#### <a name="1-get-the-two-gateways"></a><span data-ttu-id="3cd50-186">1. Obter os dois gateways</span><span class="sxs-lookup"><span data-stu-id="3cd50-186">1. Get the two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw1 = Get-AzureRmLocalNetworkGateway  -Name $LNGName51 -ResourceGroupName $RG5
```

#### <a name="2-create-the-testvnet1-to-site5-connection"></a><span data-ttu-id="3cd50-187">2. Criar a conexão TestVNet1 para Site5</span><span class="sxs-lookup"><span data-stu-id="3cd50-187">2. Create the TestVNet1 to Site5 connection</span></span>
<span data-ttu-id="3cd50-188">Nesta etapa, você criará a conexão de TestVNet1 para Site5_1 com "EnableBGP" definido como $True.</span><span class="sxs-lookup"><span data-stu-id="3cd50-188">In this step, you will create the connection from TestVNet1 to Site5_1 with "EnableBGP" set to $True.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection151 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw1 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-on-premises-vpn-device"></a><span data-ttu-id="3cd50-189">3. Parâmetros VPN e BGP para seu dispositivo VPN local</span><span class="sxs-lookup"><span data-stu-id="3cd50-189">3. VPN and BGP parameters for your on-premises VPN device</span></span>
<span data-ttu-id="3cd50-190">O exemplo a seguir lista os parâmetros que você inserirá na seção de configuração de BGP em seu dispositivo VPN local para este exercício:</span><span class="sxs-lookup"><span data-stu-id="3cd50-190">The example below lists the parameters you will enter into the BGP configuration section on your on-premises VPN device for this exercise:</span></span>

    - <span data-ttu-id="3cd50-191">Site5 ASN            : 65050</span><span class="sxs-lookup"><span data-stu-id="3cd50-191">Site5 ASN            : 65050</span></span>
    - <span data-ttu-id="3cd50-192">Site5 BGP IP         : 10.52.255.253</span><span class="sxs-lookup"><span data-stu-id="3cd50-192">Site5 BGP IP         : 10.52.255.253</span></span>
    - <span data-ttu-id="3cd50-193">Prefixes to announce : (for example) 10.51.0.0/16 and 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="3cd50-193">Prefixes to announce : (for example) 10.51.0.0/16 and 10.52.0.0/16</span></span>
    - <span data-ttu-id="3cd50-194">Azure VNet ASN       : 65010</span><span class="sxs-lookup"><span data-stu-id="3cd50-194">Azure VNet ASN       : 65010</span></span>
    - <span data-ttu-id="3cd50-195">Azure VNet BGP IP 1  : 10.12.255.4 for tunnel to 40.112.190.5</span><span class="sxs-lookup"><span data-stu-id="3cd50-195">Azure VNet BGP IP 1  : 10.12.255.4 for tunnel to 40.112.190.5</span></span>
    - <span data-ttu-id="3cd50-196">Azure VNet BGP IP 2  : 10.12.255.5 for tunnel to 138.91.156.129</span><span class="sxs-lookup"><span data-stu-id="3cd50-196">Azure VNet BGP IP 2  : 10.12.255.5 for tunnel to 138.91.156.129</span></span>
    - <span data-ttu-id="3cd50-197">Static routes        : Destination 10.12.255.4/32, nexthop the VPN tunnel interface to 40.112.190.5                        Destination 10.12.255.5/32, nexthop the VPN tunnel interface to 138.91.156.129</span><span class="sxs-lookup"><span data-stu-id="3cd50-197">Static routes        : Destination 10.12.255.4/32, nexthop the VPN tunnel interface to 40.112.190.5                        Destination 10.12.255.5/32, nexthop the VPN tunnel interface to 138.91.156.129</span></span>
    - <span data-ttu-id="3cd50-198">eBGP Multihop        : Ensure the "multihop" option for eBGP is enabled on your device if needed</span><span class="sxs-lookup"><span data-stu-id="3cd50-198">eBGP Multihop        : Ensure the "multihop" option for eBGP is enabled on your device if needed</span></span>

<span data-ttu-id="3cd50-199">A conexão deve ser estabelecida após alguns minutos, e a sessão de emparelhamento via protocolo BGP iniciará uma vez estabelecida a conexão IPsec.</span><span class="sxs-lookup"><span data-stu-id="3cd50-199">The connection should be established after a few minutes, and the BGP peering session will start once the IPsec connection is established.</span></span> <span data-ttu-id="3cd50-200">Até agora, este exemplo configurou apenas um dispositivo VPN local, resultando no diagrama mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="3cd50-200">This example so far has configured only one on-premises VPN device, resulting in the diagram shown below:</span></span>

![ativo-ativo-entre-os-locais](./media/vpn-gateway-activeactive-rm-powershell/active-active.png)

### <a name="step-3---connect-two-on-premises-vpn-devices-to-the-active-active-vpn-gateway"></a><span data-ttu-id="3cd50-202">Etapa 3 – Conectar dois dispositivos VPN locais ao gateway de VPN ativo-ativo</span><span class="sxs-lookup"><span data-stu-id="3cd50-202">Step 3 - Connect two on-premises VPN devices to the active-active VPN gateway</span></span>
<span data-ttu-id="3cd50-203">Se você tiver dois dispositivos VPN na mesma rede local, você poderá obter redundância dupla ao conectar o gateway de VPN do Azure ao segundo dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="3cd50-203">If you have two VPN devices at the same on-premises network, you can achieve dual redundancy by connecting the Azure VPN gateway to the second VPN device.</span></span>

#### <a name="1-create-the-second-local-network-gateway-for-site5"></a><span data-ttu-id="3cd50-204">1. Criar o segundo gateway de rede local para Site5</span><span class="sxs-lookup"><span data-stu-id="3cd50-204">1. Create the second local network gateway for Site5</span></span>
<span data-ttu-id="3cd50-205">Observe que o endereço IP do gateway, o prefixo do endereço e o endereço de emparelhamento via protocolo BGP para o segundo gateway de rede local não devem se sobrepor ao gateway de rede local anterior para a mesma rede local.</span><span class="sxs-lookup"><span data-stu-id="3cd50-205">Note that the gateway IP address, address prefix, and BGP peering address for the second local network gateway must not overlap with the previous local network gateway for the same on-premises network.</span></span>

```powershell
$LNGName52 = "Site5_2"
$LNGPrefix52 = "10.52.255.254/32"
$LNGIP52 = "131.107.72.23"
$BGPPeerIP52 = "10.52.255.254"

New-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP52 -AddressPrefix $LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP52
```

#### <a name="2-connect-the-vnet-gateway-and-the-second-local-network-gateway"></a><span data-ttu-id="3cd50-206">2. Conectar o gateway da VNet e segundo gateway de rede local</span><span class="sxs-lookup"><span data-stu-id="3cd50-206">2. Connect the VNet gateway and the second local network gateway</span></span>
<span data-ttu-id="3cd50-207">Crie a conexão de TestVNet1 para Site5_2 com "EnableBGP" definido como $True</span><span class="sxs-lookup"><span data-stu-id="3cd50-207">Create the connection from TestVNet1 to Site5_2 with "EnableBGP" set to $True</span></span>

```powershell
$lng5gw2 = Get-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection152 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw2 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-second-on-premises-vpn-device"></a><span data-ttu-id="3cd50-208">3. Parâmetros VPN e BGP para seu segundo dispositivo VPN local</span><span class="sxs-lookup"><span data-stu-id="3cd50-208">3. VPN and BGP parameters for your second on-premises VPN device</span></span>
<span data-ttu-id="3cd50-209">Da mesma forma, encontram-se abaixo os parâmetros que você digitará no segundo dispositivo VPN:</span><span class="sxs-lookup"><span data-stu-id="3cd50-209">Similarly, below lists the parameters you will enter into the second VPN device:</span></span>

```
- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes to announce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP 1  : 10.12.255.4 for tunnel to 40.112.190.5
- Azure VNet BGP IP 2  : 10.12.255.5 for tunnel to 138.91.156.129
- Static routes        : Destination 10.12.255.4/32, nexthop the VPN tunnel interface to 40.112.190.5
                         Destination 10.12.255.5/32, nexthop the VPN tunnel interface to 138.91.156.129
- eBGP Multihop        : Ensure the "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="3cd50-210">Depois que (os túneis da) conexão forem estabelecidos, você terá túneis e dispositivos VPN redundantes duplos conectando-se à sua rede local e ao Azure:</span><span class="sxs-lookup"><span data-stu-id="3cd50-210">Once the connection (tunnels) are established, you will have dual redundant VPN devices and tunnels connecting your on-premises network and Azure:</span></span>

![redundância-dupla-entre-os-locais](./media/vpn-gateway-activeactive-rm-powershell/dual-redundancy.png)

## <span data-ttu-id="3cd50-212"><a name ="aav2v"></a>Parte 3 – Estabelecer uma conexão VNet para VNet ativo-ativo</span><span class="sxs-lookup"><span data-stu-id="3cd50-212"><a name ="aav2v"></a>Part 3 - Establish an active-active VNet-to-VNet connection</span></span>
<span data-ttu-id="3cd50-213">Esta seção cria uma conexão VNet para VNet ativo-ativo com o BGP.</span><span class="sxs-lookup"><span data-stu-id="3cd50-213">This section creates an active-active VNet-to-VNet connection with BGP.</span></span> 

<span data-ttu-id="3cd50-214">As instruções abaixo continuam das etapas anteriores listadas acima.</span><span class="sxs-lookup"><span data-stu-id="3cd50-214">The instructions below continue from the previous steps listed above.</span></span> <span data-ttu-id="3cd50-215">Você deve concluir a [Parte 1](#aagateway) para criar e configurar TestVNet1 e o Gateway de VPN com BGP.</span><span class="sxs-lookup"><span data-stu-id="3cd50-215">You must complete [Part 1](#aagateway) to create and configure TestVNet1 and the VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-the-vpn-gateway"></a><span data-ttu-id="3cd50-216">Etapa 1 - Criar TestVNet2 e gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="3cd50-216">Step 1 - Create TestVNet2 and the VPN gateway</span></span>
<span data-ttu-id="3cd50-217">É importante certificar-se de que o espaço de endereço IP da nova rede virtual, TestVNet2, não se sobreponha a nenhum dos seus intervalos de VNet.</span><span class="sxs-lookup"><span data-stu-id="3cd50-217">It is important to make sure that the IP address space of the new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="3cd50-218">Neste exemplo, as redes virtuais pertencem à mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="3cd50-218">In this example, the virtual networks belong to the same subscription.</span></span> <span data-ttu-id="3cd50-219">Você pode configurar conexões de VNet para VNet entre assinaturas diferentes; consulte [Configurar uma conexão VNet para VNet](vpn-gateway-vnet-vnet-rm-ps.md) para saber mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="3cd50-219">You can set up VNet-to-VNet connections between different subscriptions; please refer to [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) to learn more details.</span></span> <span data-ttu-id="3cd50-220">Verifique se você adicionou "-EnableBgp $True" ao criar conexões para habilitar o BGP.</span><span class="sxs-lookup"><span data-stu-id="3cd50-220">Make sure you add the "-EnableBgp $True" when creating the connections to enable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="3cd50-221">1. Declare as variáveis</span><span class="sxs-lookup"><span data-stu-id="3cd50-221">1. Declare your variables</span></span>
<span data-ttu-id="3cd50-222">Não se esqueça de substituir os valores com aqueles que você deseja usar para sua configuração.</span><span class="sxs-lookup"><span data-stu-id="3cd50-222">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

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

#### <a name="2-create-testvnet2-in-the-new-resource-group"></a><span data-ttu-id="3cd50-223">2. Criar TestVNet2 no novo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="3cd50-223">2. Create TestVNet2 in the new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-the-active-active-vpn-gateway-for-testvnet2"></a><span data-ttu-id="3cd50-224">3. Criar um gateway de VPN ativo-ativo para TestVNet2</span><span class="sxs-lookup"><span data-stu-id="3cd50-224">3. Create the active-active VPN gateway for TestVNet2</span></span>
<span data-ttu-id="3cd50-225">Solicite dois endereços IP públicos para serem alocados ao gateway que você criará para sua VNet.</span><span class="sxs-lookup"><span data-stu-id="3cd50-225">Request two public IP addresses to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="3cd50-226">Você também definirá as configurações de IP e sub-rede necessárias.</span><span class="sxs-lookup"><span data-stu-id="3cd50-226">You'll also define the subnet and IP configurations required.</span></span>

```powershell
$gw2pip1 = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$gw2pip2 = New-AzureRmPublicIpAddress -Name $GW2IPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2 = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1
$gw2ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf2 -Subnet $subnet2 -PublicIpAddress $gw2pip2
```

<span data-ttu-id="3cd50-227">Crie o gateway de VPN com o número AS e o sinalizador "EnableActiveActiveFeature".</span><span class="sxs-lookup"><span data-stu-id="3cd50-227">Create the VPN gateway with the AS number and the "EnableActiveActiveFeature" flag.</span></span> <span data-ttu-id="3cd50-228">Observe que você deve substituir o ASN padrão em seus gateways de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="3cd50-228">Note that you must override the default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="3cd50-229">As ASNs para as VNets conectadas devem ser diferentes para habilitar o BGP e roteamento de tráfego.</span><span class="sxs-lookup"><span data-stu-id="3cd50-229">The ASNs for the connected VNets must be different to enable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1,$gw2ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet2ASN -EnableActiveActiveFeature
```

### <a name="step-2---connect-the-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="3cd50-230">Etapa 2 - Conectar os gateways de TestVNet1 e TestVNet2</span><span class="sxs-lookup"><span data-stu-id="3cd50-230">Step 2 - Connect the TestVNet1 and TestVNet2 gateways</span></span>
<span data-ttu-id="3cd50-231">Neste exemplo, ambos os gateways estão na mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="3cd50-231">In this example, both gateways are in the same subscription.</span></span> <span data-ttu-id="3cd50-232">Você pode concluir essa etapa na mesma sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3cd50-232">You can complete this step in the same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="3cd50-233">1. Obter ambos os gateways</span><span class="sxs-lookup"><span data-stu-id="3cd50-233">1. Get both gateways</span></span>
<span data-ttu-id="3cd50-234">Certifique-se de fazer logon e se conectar à Assinatura 1.</span><span class="sxs-lookup"><span data-stu-id="3cd50-234">Make sure you log in and connect to Subscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="3cd50-235">2. Criar ambas as conexões</span><span class="sxs-lookup"><span data-stu-id="3cd50-235">2. Create both connections</span></span>
<span data-ttu-id="3cd50-236">Nesta etapa, você criará a conexão de TestVNet1 para TestVNet2 e a conexão de TestVNet2 to TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="3cd50-236">In this step, you will create the connection from TestVNet1 to TestVNet2, and the connection from TestVNet2 to TestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="3cd50-237">Certifique-se de habilitar o BGP para AMBAS as conexões.</span><span class="sxs-lookup"><span data-stu-id="3cd50-237">Be sure to enable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="3cd50-238">Após concluir essas etapas, a conexão será estabelecida em alguns minutos e a sessão de emparelhamento via protocolo BGP estará em funcionamento quando a conexão VNet para VNet for concluída com redundância dupla:</span><span class="sxs-lookup"><span data-stu-id="3cd50-238">After completing these steps, the connection will be establish in a few minutes, and the BGP peering session will be up once the VNet-to-VNet connection is completed with dual redundancy:</span></span>

![ativo-ativo-v2v](./media/vpn-gateway-activeactive-rm-powershell/vnet-to-vnet.png)

## <span data-ttu-id="3cd50-240"><a name ="aaupdate"></a>Parte 4 – Atualizar o gateway existente entre ativo-ativo e ativo-em espera</span><span class="sxs-lookup"><span data-stu-id="3cd50-240"><a name ="aaupdate"></a>Part 4 - Update existing gateway between active-active and active-standby</span></span>
<span data-ttu-id="3cd50-241">A última seção descreverá como você pode configurar um gateway de VPN do Azure existente por meio do modo ativo-em espera ou ativo-ativo ou vice-versa.</span><span class="sxs-lookup"><span data-stu-id="3cd50-241">The last section will describe how you can configure an existing Azure VPN gateway from active-standby to active-active mode, or vice versa.</span></span>

> [!NOTE]
> <span data-ttu-id="3cd50-242">Esta seção inclui as etapas para redimensionar de Standard para HighPerformance um SKU herdado (SKU antigo) de um Gateway de VPN já criado.</span><span class="sxs-lookup"><span data-stu-id="3cd50-242">This section includes the steps to resize a legacy SKU (old SKU) of an already created VPN gateway from Standard to HighPerformance.</span></span> <span data-ttu-id="3cd50-243">Essas etapas não atualizam um SKU herdado antigo para um dos SKUs novos.</span><span class="sxs-lookup"><span data-stu-id="3cd50-243">These steps do not upgrade an old legacy SKU to one of the new SKUs.</span></span>
> 
> 

### <a name="configure-an-active-standby-gateway-to-active-active-gateway"></a><span data-ttu-id="3cd50-244">Configurar um gateway ativo-em espera para um gateway ativo-ativo</span><span class="sxs-lookup"><span data-stu-id="3cd50-244">Configure an active-standby gateway to active-active gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="3cd50-245">1. Parâmetros do gateway</span><span class="sxs-lookup"><span data-stu-id="3cd50-245">1. Gateway parameters</span></span>
<span data-ttu-id="3cd50-246">O exemplo a seguir converte um gateway ativo-em espera em um gateway ativo-ativo.</span><span class="sxs-lookup"><span data-stu-id="3cd50-246">The following example converts an active-standby gateway into an active-active gateway.</span></span> <span data-ttu-id="3cd50-247">Você precisa criar outro endereço IP público e adicionar uma configuração do segundo IP do Gateway.</span><span class="sxs-lookup"><span data-stu-id="3cd50-247">You need to create another public IP address, then add a second Gateway IP configuration.</span></span> <span data-ttu-id="3cd50-248">Abaixo, encontram-se os parâmetros usados:</span><span class="sxs-lookup"><span data-stu-id="3cd50-248">Below shows the parameters used:</span></span>

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

#### <a name="2-create-the-public-ip-address-then-add-the-second-gateway-ip-configuration"></a><span data-ttu-id="3cd50-249">2. Crie o endereço IP público e adicione a configuração do segundo IP do Gateway</span><span class="sxs-lookup"><span data-stu-id="3cd50-249">2. Create the public IP address, then add the second gateway IP configuration</span></span>

```powershell
$gwpip2 = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG -Location $location -AllocationMethod Dynamic
Add-AzureRmVirtualNetworkGatewayIpConfig -VirtualNetworkGateway $gw -Name $GWIPconf2 -Subnet $subnet -PublicIpAddress $gwpip2
```

#### <a name="3-enable-active-active-mode-and-update-the-gateway"></a><span data-ttu-id="3cd50-250">3. Habilitar o modo ativo-ativo e atualizar o gateway</span><span class="sxs-lookup"><span data-stu-id="3cd50-250">3. Enable active-active mode and update the gateway</span></span>
<span data-ttu-id="3cd50-251">Você deve definir o objeto do gateway no PowerShell para disparar a atualização real.</span><span class="sxs-lookup"><span data-stu-id="3cd50-251">You must set the gateway object in PowerShell to trigger the actual update.</span></span> <span data-ttu-id="3cd50-252">O SKU do gateway de rede virtual também deve ser alterado (redimensionado) para HighPerformance já que foi criado anteriormente como Standard.</span><span class="sxs-lookup"><span data-stu-id="3cd50-252">The SKU of the virtual network gateway must also be changed (resized) to HighPerformance since it was created previously as Standard.</span></span>

```powershell
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -EnableActiveActiveFeature -GatewaySku HighPerformance
```

<span data-ttu-id="3cd50-253">Esta atualização pode demorar de 30 a 45 minutos.</span><span class="sxs-lookup"><span data-stu-id="3cd50-253">This update can take 30 to 45 minutes.</span></span>

### <a name="configure-an-active-active-gateway-to-active-standby-gateway"></a><span data-ttu-id="3cd50-254">Configurar um gateway ativo-ativo para um gateway ativo-em espera</span><span class="sxs-lookup"><span data-stu-id="3cd50-254">Configure an active-active gateway to active-standby gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="3cd50-255">1. Parâmetros do gateway</span><span class="sxs-lookup"><span data-stu-id="3cd50-255">1. Gateway parameters</span></span>
<span data-ttu-id="3cd50-256">Usando os mesmos parâmetros acima, obtenha o nome da configuração de IP que você deseja remover.</span><span class="sxs-lookup"><span data-stu-id="3cd50-256">Use the same parameters as above, get the name of the IP configuration you want to remove.</span></span>

```powershell
$GWName = "TestVNetAA1GW"
$RG = "TestVPNActiveActive01"

$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$ipconfname = $gw.IpConfigurations[1].Name
```

#### <a name="2-remove-the-gateway-ip-configuration-and-disable-the-active-active-mode"></a><span data-ttu-id="3cd50-257">2. Remover a configuração de IP do gateway e desabilitar o modo ativo-ativo</span><span class="sxs-lookup"><span data-stu-id="3cd50-257">2. Remove the gateway IP configuration and disable the active-active mode</span></span>
<span data-ttu-id="3cd50-258">Da mesma forma, você deverá definir o objeto do gateway no PowerShell para disparar a atualização real.</span><span class="sxs-lookup"><span data-stu-id="3cd50-258">Similarly, you must set the gateway object in PowerShell to trigger the actual update.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGatewayIpConfig -Name $ipconfname -VirtualNetworkGateway $gw
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -DisableActiveActiveFeature
```

<span data-ttu-id="3cd50-259">Esta atualização pode levar de 30 a 45 minutos.</span><span class="sxs-lookup"><span data-stu-id="3cd50-259">This update can take up to 30 to  45 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3cd50-260">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3cd50-260">Next steps</span></span>
<span data-ttu-id="3cd50-261">Quando sua conexão for concluída, você poderá adicionar máquinas virtuais às suas redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="3cd50-261">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="3cd50-262">Veja [Criar uma máquina virtual](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obter as etapas.</span><span class="sxs-lookup"><span data-stu-id="3cd50-262">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>