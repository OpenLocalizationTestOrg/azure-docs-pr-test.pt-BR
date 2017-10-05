---
title: 'Configurar o BGP em Gateways de VPN: Gerenciador de Recursos: PowerShell | Microsoft Docs'
description: Este artigo mostra como configurar o BGP com Gateways de VPN do Azure usando o Azure Resource Manager e o PowerShell.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 905b11a7-1333-482c-820b-0fd0f44238e5
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: yushwang
ms.openlocfilehash: b00a3fe7ba4b12c2e9c486188c292cd6fafb60a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-configure-bgp-on-azure-vpn-gateways-using-powershell"></a><span data-ttu-id="60445-103">Como configurar o BGP em Gateways de VPN do Azure usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="60445-103">How to configure BGP on Azure VPN Gateways using PowerShell</span></span>
<span data-ttu-id="60445-104">Este artigo explica as etapas para habilitar o BGP em uma conexão de VPN Site a Site (S2S) entre locais e uma conexão de VNet para VNet usando o modelo de implantação do Resource Manager e o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="60445-104">This article walks you through the steps to enable BGP on a cross-premises Site-to-Site (S2S) VPN connection and a VNet-to-VNet connection using the Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-bgp"></a><span data-ttu-id="60445-105">Sobre o BGP</span><span class="sxs-lookup"><span data-stu-id="60445-105">About BGP</span></span>
<span data-ttu-id="60445-106">O BGP é o protocolo de roteamento padrão usado na Internet para a troca de informações de roteamento e acessibilidade entre duas ou mais redes.</span><span class="sxs-lookup"><span data-stu-id="60445-106">BGP is the standard routing protocol commonly used in the Internet to exchange routing and reachability information between two or more networks.</span></span> <span data-ttu-id="60445-107">O BGP habilita os Gateways de VPN do Azure e os dispositivos de VPN locais, chamados de pares no nível de protocolo BGP, ou vizinhos, para trocar "rotas" que informarão ambos os gateways sobre a disponibilidade e a acessibilidade para que esses prefixos percorram os gateways ou os roteadores envolvidos.</span><span class="sxs-lookup"><span data-stu-id="60445-107">BGP enables the Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, to exchange "routes" that will inform both gateways on the availability and reachability for those prefixes to go through the gateways or routers involved.</span></span> <span data-ttu-id="60445-108">O BGP também pode habilitar o roteamento de trânsito entre várias redes propagando rotas que um gateway BGP obtém de um par no nível de protocolo BGP para todos os outros pares no nível de protocolo BGP.</span><span class="sxs-lookup"><span data-stu-id="60445-108">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer to all other BGP peers.</span></span>

<span data-ttu-id="60445-109">Veja [Visão geral de BGP com Gateways de VPN do Azure](vpn-gateway-bgp-overview.md) para obter mais discussões sobre os benefícios do BGP e entender os requisitos técnicos e as considerações do uso de BGP.</span><span class="sxs-lookup"><span data-stu-id="60445-109">See [Overview of BGP with Azure VPN Gateways](vpn-gateway-bgp-overview.md) for more discussion on benefits of BGP and to understand the technical requirements and considerations of using BGP.</span></span>

## <a name="getting-started-with-bgp-on-azure-vpn-gateways"></a><span data-ttu-id="60445-110">Introdução ao BGP em gateways de VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="60445-110">Getting started with BGP on Azure VPN gateways</span></span>

<span data-ttu-id="60445-111">Este artigo orienta você pelas etapas para executar as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="60445-111">This article walks you through the steps to do the following tasks:</span></span>

* [<span data-ttu-id="60445-112">Parte 1 - Habilitar o BGP em seu gateway de VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="60445-112">Part 1 - Enable BGP on your Azure VPN gateway</span></span>](#enablebgp)
* [<span data-ttu-id="60445-113">Parte 2 - Estabelecer uma conexão entre instalações com BGP</span><span class="sxs-lookup"><span data-stu-id="60445-113">Part 2 - Establish a cross-premises connection with BGP</span></span>](#crossprembgp)
* [<span data-ttu-id="60445-114">Parte 3 - Estabelecer uma conexão VNet para VNet com BGP</span><span class="sxs-lookup"><span data-stu-id="60445-114">Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>](#v2vbgp)

<span data-ttu-id="60445-115">Cada parte das instruções constitui um bloco de construção básico para habilitar o BGP em sua conectividade de rede.</span><span class="sxs-lookup"><span data-stu-id="60445-115">Each part of the instructions forms a basic building block for enabling BGP in your network connectivity.</span></span> <span data-ttu-id="60445-116">Se você concluir todas as três partes, criará a topologia conforme mostrado no diagrama a seguir:</span><span class="sxs-lookup"><span data-stu-id="60445-116">If you complete all three parts, you build the topology as shown in the following diagram:</span></span>

![Topologia BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

<span data-ttu-id="60445-118">Você pode combinar essas partes para criar uma rede de trânsito mais complexa, com saltos múltiplos e que atenda às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="60445-118">You can combine parts together to build a more complex, multi-hop, transit network that meets your needs.</span></span>

## <span data-ttu-id="60445-119"><a name ="enablebgp"></a>Parte 1 - Configurar o BGP no Gateway de VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="60445-119"><a name ="enablebgp"></a>Part 1 - Configure BGP on the Azure VPN Gateway</span></span>
<span data-ttu-id="60445-120">As etapas de configuração definem os parâmetros de BGP do gateway de VPN do Azure, conforme mostrado no diagrama a seguir:</span><span class="sxs-lookup"><span data-stu-id="60445-120">The configuration steps set up the BGP parameters of the Azure VPN gateway as shown in the following diagram:</span></span>

![Gateway BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-gateway.png)

### <a name="before-you-begin"></a><span data-ttu-id="60445-122">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="60445-122">Before you begin</span></span>
* <span data-ttu-id="60445-123">Verifique se você tem uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="60445-123">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="60445-124">Se ainda não tiver uma assinatura do Azure, você poderá ativar os [Benefícios do assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se para obter uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="60445-124">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="60445-125">Instale os cmdlets do PowerShell do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="60445-125">Install the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="60445-126">Para saber mais sobre como instalar os cmdlets do PowerShell, consulte [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="60445-126">For more information about installing the PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="60445-127">Etapa 1 - Criar e configurar VNet1</span><span class="sxs-lookup"><span data-stu-id="60445-127">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="60445-128">1. Declare as variáveis</span><span class="sxs-lookup"><span data-stu-id="60445-128">1. Declare your variables</span></span>
<span data-ttu-id="60445-129">Para este exercício, começaremos declarando nossa variáveis.</span><span class="sxs-lookup"><span data-stu-id="60445-129">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="60445-130">O exemplo a seguir declara as variáveis usando os valores para este exercício.</span><span class="sxs-lookup"><span data-stu-id="60445-130">The following example declares the variables using the values for this exercise.</span></span> <span data-ttu-id="60445-131">Certifique-se de substituir os valores pelos seus próprios ao configurar para a produção.</span><span class="sxs-lookup"><span data-stu-id="60445-131">Be sure to replace the values with your own when configuring for production.</span></span> <span data-ttu-id="60445-132">Se você estiver executando as etapas para se familiarizar com esse tipo de configuração, poderá usar essas variáveis.</span><span class="sxs-lookup"><span data-stu-id="60445-132">You can use these variables if you are running through the steps to become familiar with this type of configuration.</span></span> <span data-ttu-id="60445-133">Modifique as variáveis e, em seguida, copie e cole em seu console do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="60445-133">Modify the variables, and then copy and paste into your PowerShell console.</span></span>

```powershell
$Sub1 = "Replace_With_Your_Subcription_Name"
$RG1 = "TestBGPRG1"
$Location1 = "East US"
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
$GWIPName1 = "VNet1GWIP"
$GWIPconfName1 = "gwipconf1"
$Connection12 = "VNet1toVNet2"
$Connection15 = "VNet1toSite5"
```

#### <a name="2-connect-to-your-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="60445-134">2. Conectar à sua assinatura do Azure e criar um novo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="60445-134">2. Connect to your subscription and create a new resource group</span></span>
<span data-ttu-id="60445-135">Para usar os cmdlets do Gerenciador de Recursos, alterne para o modo do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="60445-135">To use the Resource Manager cmdlets, Make sure you switch to PowerShell mode.</span></span> <span data-ttu-id="60445-136">Para obter mais informações, consulte [Usando o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="60445-136">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="60445-137">Abra o console do PowerShell e conecte-se à sua conta.</span><span class="sxs-lookup"><span data-stu-id="60445-137">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="60445-138">Use o exemplo a seguir para ajudar com a conexão:</span><span class="sxs-lookup"><span data-stu-id="60445-138">Use the following sample to help you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="60445-139">3. Criar TestVNet1</span><span class="sxs-lookup"><span data-stu-id="60445-139">3. Create TestVNet1</span></span>
<span data-ttu-id="60445-140">O exemplo a seguir cria uma rede virtual denominada TestVNet1 e três sub-redes, uma chamada GatewaySubnet, outra FrontEnd e outra Backend.</span><span class="sxs-lookup"><span data-stu-id="60445-140">The following sample creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="60445-141">Ao substituir valores, é importante você sempre nomear sua sub-rede de gateway especificamente como GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="60445-141">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="60445-142">Se você usar outro nome, a criação do gateway falhará.</span><span class="sxs-lookup"><span data-stu-id="60445-142">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-the-vpn-gateway-for-testvnet1-with-bgp-parameters"></a><span data-ttu-id="60445-143">Etapa 2 - Criar um Gateway de VPN para TestVNet1 com parâmetros de BGP</span><span class="sxs-lookup"><span data-stu-id="60445-143">Step 2 - Create the VPN Gateway for TestVNet1 with BGP parameters</span></span>
#### <a name="1-create-the-ip-and-subnet-configurations"></a><span data-ttu-id="60445-144">1. Criar as configurações de IP e sub-redes</span><span class="sxs-lookup"><span data-stu-id="60445-144">1. Create the IP and subnet configurations</span></span>
<span data-ttu-id="60445-145">Solicite um endereço IP público para ser alocado ao gateway que você criará para sua VNet.</span><span class="sxs-lookup"><span data-stu-id="60445-145">Request a public IP address to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="60445-146">Você também definirá as configurações necessárias de IP e sub-rede.</span><span class="sxs-lookup"><span data-stu-id="60445-146">You'll also define the required subnet and IP configurations.</span></span>

```powershell
$gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1
```

#### <a name="2-create-the-vpn-gateway-with-the-as-number"></a><span data-ttu-id="60445-147">2. Criar o gateway de VPN com o número AS</span><span class="sxs-lookup"><span data-stu-id="60445-147">2. Create the VPN gateway with the AS number</span></span>
<span data-ttu-id="60445-148">Crie o gateway de rede virtual para TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="60445-148">Create the virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="60445-149">O BGP exige um gateway de VPN Baseado em Rota, além do parâmetro de adição, -Asn, para definir o Número AS (ASN) como TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="60445-149">BGP requires a Route-Based VPN gateway, and also the addition parameter, -Asn, to set the ASN (AS Number) for TestVNet1.</span></span> <span data-ttu-id="60445-150">Se você não definir o parâmetro ASN, ASN 65515 será atribuído.</span><span class="sxs-lookup"><span data-stu-id="60445-150">If you do not set the ASN parameter, ASN 65515 is assigned.</span></span> <span data-ttu-id="60445-151">Criar um gateway pode demorar um pouco (30 minutos ou mais para ser concluído).</span><span class="sxs-lookup"><span data-stu-id="60445-151">Creating a gateway can take a while (30 minutes or more to complete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance -Asn $VNet1ASN
```

#### <a name="3-obtain-the-azure-bgp-peer-ip-address"></a><span data-ttu-id="60445-152">3. Obter o endereço IP do par no nível de protocolo BGP do Azure</span><span class="sxs-lookup"><span data-stu-id="60445-152">3. Obtain the Azure BGP Peer IP address</span></span>
<span data-ttu-id="60445-153">Depois de criar o gateway, você precisará obter o endereço IP do par no nível de protocolo BGP no Gateway de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="60445-153">Once the gateway is created, you need to obtain the BGP Peer IP address on the Azure VPN Gateway.</span></span> <span data-ttu-id="60445-154">Esse endereço é necessário para configurar o Gateway de VPN do Azure como um par no nível de protocolo BGP para os dispositivos VPN locais.</span><span class="sxs-lookup"><span data-stu-id="60445-154">This address is needed to configure the Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet1gw.BgpSettingsText
```

<span data-ttu-id="60445-155">O último comando mostra as configurações correspondentes de BGP no Gateway de VPN do Azure; por exemplo:</span><span class="sxs-lookup"><span data-stu-id="60445-155">The last command shows the corresponding BGP configurations on the Azure VPN Gateway; for example:</span></span>

```powershell
$vnet1gw.BgpSettingsText
{
    "Asn": 65010,
    "BgpPeeringAddress": "10.12.255.30",
    "PeerWeight": 0
}
```

<span data-ttu-id="60445-156">Depois de criar o gateway, você poderá usar este gateway para estabelecer a conexão entre instalações ou conexão VNet para VNet com BGP.</span><span class="sxs-lookup"><span data-stu-id="60445-156">Once the gateway is created, you can use this gateway to establish cross-premises connection or VNet-to-VNet connection with BGP.</span></span> <span data-ttu-id="60445-157">As seções a seguir explicam as etapas para concluir o exercício.</span><span class="sxs-lookup"><span data-stu-id="60445-157">The following sections walk through the steps to complete the exercise.</span></span>

## <span data-ttu-id="60445-158"><a name ="crossprembbgp"></a>Parte 2 - Estabelecer uma conexão entre instalações com BGP</span><span class="sxs-lookup"><span data-stu-id="60445-158"><a name ="crossprembbgp"></a>Part 2 - Establish a cross-premises connection with BGP</span></span>

<span data-ttu-id="60445-159">Para estabelecer uma conexão entre instalações, você precisará criar um Gateway de Rede Local para representar o dispositivo VPN local e uma Conexão para conectar o gateway de VPN com ao gateway de rede local.</span><span class="sxs-lookup"><span data-stu-id="60445-159">To establish a cross-premises connection, you need to create a Local Network Gateway to represent your on-premises VPN device, and a Connection to connect the VPN gateway with the local network gateway.</span></span> <span data-ttu-id="60445-160">Embora haja artigos para orientar você por meio destas etapas, este artigo contém as propriedades adicionais necessárias para especificar os parâmetros de configuração do BGP.</span><span class="sxs-lookup"><span data-stu-id="60445-160">While there are articles that walk you through these steps, this article contains the additional properties required to specify the BGP configuration parameters.</span></span>

![BGP para entre instalações](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crossprem.png)

<span data-ttu-id="60445-162">Antes de prosseguir, verifique se você concluiu a [Parte 1](#enablebgp) deste exercício.</span><span class="sxs-lookup"><span data-stu-id="60445-162">Before proceeding, make sure you have completed [Part 1](#enablebgp) of this exercise.</span></span>

### <a name="step-1---create-and-configure-the-local-network-gateway"></a><span data-ttu-id="60445-163">Etapa 1 - Criar e configurar o gateway de rede local</span><span class="sxs-lookup"><span data-stu-id="60445-163">Step 1 - Create and configure the local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="60445-164">1. Declare as variáveis</span><span class="sxs-lookup"><span data-stu-id="60445-164">1. Declare your variables</span></span>

<span data-ttu-id="60445-165">Este exercício continua a compilar a configuração mostrada no diagrama.</span><span class="sxs-lookup"><span data-stu-id="60445-165">This exercise continues to build the configuration shown in the diagram.</span></span> <span data-ttu-id="60445-166">Não se esqueça de substituir os valores com aqueles que você deseja usar para sua configuração.</span><span class="sxs-lookup"><span data-stu-id="60445-166">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

```powershell
$RG5 = "TestBGPRG5"
$Location5 = "East US 2"
$LNGName5 = "Site5"
$LNGPrefix50 = "10.52.255.254/32"
$LNGIP5 = "Your_VPN_Device_IP"
$LNGASN5 = 65050
$BGPPeerIP5 = "10.52.255.254"
```

<span data-ttu-id="60445-167">Algumas coisas para observar relacionadas aos parâmetros de gateway de rede:</span><span class="sxs-lookup"><span data-stu-id="60445-167">A couple of things to note regarding the local network gateway parameters:</span></span>

* <span data-ttu-id="60445-168">O gateway de rede local pode estar no mesmo ou em outro local e grupo de recursos como o gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="60445-168">The local network gateway can be in the same or different location and resource group as the VPN gateway.</span></span> <span data-ttu-id="60445-169">Este exemplo os mostra em grupos de recursos diferentes em locais diferentes.</span><span class="sxs-lookup"><span data-stu-id="60445-169">This example shows them in different resource groups in different locations.</span></span>
* <span data-ttu-id="60445-170">O prefixo mínimo que você precisa declarar para o gateway de rede local é o endereço de host do seu endereço IP do par no nível de protocolo BGP em seu dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="60445-170">The minimum prefix you need to declare for the local network gateway is the host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="60445-171">Nesse caso, é um prefixo /32 de "10.52.255.254/32".</span><span class="sxs-lookup"><span data-stu-id="60445-171">In this case, it's a /32 prefix of "10.52.255.254/32".</span></span>
* <span data-ttu-id="60445-172">Como lembrete, você deve usar diferentes ASNs BGP entre suas redes locais e a VNet do Azure.</span><span class="sxs-lookup"><span data-stu-id="60445-172">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="60445-173">Se eles forem iguais, você precisará alterar seu ASN VNet se o dispositivo VPN local já usar o ASN para emparelhar com outros vizinhos de BGP.</span><span class="sxs-lookup"><span data-stu-id="60445-173">If they are the same, you need to change your VNet ASN if your on-premises VPN device already uses the ASN to peer with other BGP neighbors.</span></span>

<span data-ttu-id="60445-174">Antes de continuar, verifique se que você ainda está conectado à Assinatura 1.</span><span class="sxs-lookup"><span data-stu-id="60445-174">Before you continue, make sure you are still connected to Subscription 1.</span></span>

#### <a name="2-create-the-local-network-gateway-for-site5"></a><span data-ttu-id="60445-175">2. Criar o gateway de rede local para Site5</span><span class="sxs-lookup"><span data-stu-id="60445-175">2. Create the local network gateway for Site5</span></span>

<span data-ttu-id="60445-176">Certifique-se de criar o grupo de recursos se ele não for criado, antes de criar o gateway de rede local.</span><span class="sxs-lookup"><span data-stu-id="60445-176">Be sure to create the resource group if it is not created, before you create the local network gateway.</span></span> <span data-ttu-id="60445-177">Observe os dois parâmetros adicionais para o gateway de rede local: Asn e BgpPeerAddress.</span><span class="sxs-lookup"><span data-stu-id="60445-177">Notice the two additional parameters for the local network gateway: Asn and BgpPeerAddress.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

### <a name="step-2---connect-the-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="60445-178">Etapa 2 - Conectar o gateway de VNet e o gateway de rede local</span><span class="sxs-lookup"><span data-stu-id="60445-178">Step 2 - Connect the VNet gateway and local network gateway</span></span>

#### <a name="1-get-the-two-gateways"></a><span data-ttu-id="60445-179">1. Obter os dois gateways</span><span class="sxs-lookup"><span data-stu-id="60445-179">1. Get the two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5
```

#### <a name="2-create-the-testvnet1-to-site5-connection"></a><span data-ttu-id="60445-180">2. Criar a conexão TestVNet1 para Site5</span><span class="sxs-lookup"><span data-stu-id="60445-180">2. Create the TestVNet1 to Site5 connection</span></span>

<span data-ttu-id="60445-181">Nesta etapa, você cria a conexão de TestVNet1 para Site5.</span><span class="sxs-lookup"><span data-stu-id="60445-181">In this step, you create the connection from TestVNet1 to Site5.</span></span> <span data-ttu-id="60445-182">Você deve especificar "-EnableBGP $True" para habilitar o BGP para essa conexão.</span><span class="sxs-lookup"><span data-stu-id="60445-182">You must specify "-EnableBGP $True" to enable BGP for this connection.</span></span> <span data-ttu-id="60445-183">Conforme discutido anteriormente, é possível ter conexões BGP e conexões que não são de BGP para o mesmo Gateway de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="60445-183">As discussed earlier, it is possible to have both BGP and non-BGP connections for the same Azure VPN Gateway.</span></span> <span data-ttu-id="60445-184">A menos que o BGP esteja habilitado na propriedade de conexão, o Azure não habilitará o BGP para essa conexão, mesmo que parâmetros BGP já estejam configurados em ambos os gateways.</span><span class="sxs-lookup"><span data-stu-id="60445-184">Unless BGP is enabled in the connection property, Azure will not enable BGP for this connection even though BGP parameters are already configured on both gateways.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

<span data-ttu-id="60445-185">O exemplo a seguir lista os parâmetros que você inserirá na seção de configuração de BGP em seu dispositivo VPN local para este exercício:</span><span class="sxs-lookup"><span data-stu-id="60445-185">The following example lists the parameters you enter into the BGP configuration section on your on-premises VPN device for this exercise:</span></span>

```

- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes to announce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP    : 10.12.255.30
- Static route         : Add a route for 10.12.255.30/32, with nexthop being the VPN tunnel interface on your device
- eBGP Multihop        : Ensure the "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="60445-186">A conexão é estabelecida após alguns minutos, e a sessão de emparelhamento via protocolo BGP inicia uma vez estabelecida a conexão IPsec.</span><span class="sxs-lookup"><span data-stu-id="60445-186">The connection is established after a few minutes, and the BGP peering session starts once the IPsec connection is established.</span></span>

## <span data-ttu-id="60445-187"><a name ="v2vbgp"></a>Parte 3 - Estabelecer uma conexão VNet para VNet com BGP</span><span class="sxs-lookup"><span data-stu-id="60445-187"><a name ="v2vbgp"></a>Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>

<span data-ttu-id="60445-188">Esta seção adiciona uma conexão de VNet para VNet com BGP, conforme mostrado neste diagrama:</span><span class="sxs-lookup"><span data-stu-id="60445-188">This section adds a VNet-to-VNet connection with BGP, as shown in the following diagram:</span></span>

![BGP de VNet para VNet](./media/vpn-gateway-bgp-resource-manager-ps/bgp-vnet2vnet.png)

<span data-ttu-id="60445-190">As instruções a seguir continuam das etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="60445-190">The following instructions continue from the previous steps.</span></span> <span data-ttu-id="60445-191">Você deve concluir a [Parte 1](#enablebgp) para criar e configurar o Gateway de VPN e TestVNet1 com BGP.</span><span class="sxs-lookup"><span data-stu-id="60445-191">You must complete [Part I](#enablebgp) to create and configure TestVNet1 and the VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-the-vpn-gateway"></a><span data-ttu-id="60445-192">Etapa 1 - Criar TestVNet2 e gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="60445-192">Step 1 - Create TestVNet2 and the VPN gateway</span></span>

<span data-ttu-id="60445-193">É importante certificar-se de que o espaço de endereço IP da nova rede virtual, TestVNet2, não se sobreponha a nenhum dos seus intervalos de VNet.</span><span class="sxs-lookup"><span data-stu-id="60445-193">It is important to make sure that the IP address space of the new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="60445-194">Neste exemplo, as redes virtuais pertencem à mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="60445-194">In this example, the virtual networks belong to the same subscription.</span></span> <span data-ttu-id="60445-195">Você pode configurar conexões de rede virtual a rede entre assinaturas diferentes.</span><span class="sxs-lookup"><span data-stu-id="60445-195">You can set up VNet-to-VNet connections between different subscriptions.</span></span> <span data-ttu-id="60445-196">Para saber mais, veja [Configurar uma conexão VNet com VNet](vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="60445-196">For more information, see [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md).</span></span> <span data-ttu-id="60445-197">Verifique se você adicionou "-EnableBgp $True" ao criar conexões para habilitar o BGP.</span><span class="sxs-lookup"><span data-stu-id="60445-197">Make sure you add the "-EnableBgp $True" when creating the connections to enable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="60445-198">1. Declare as variáveis</span><span class="sxs-lookup"><span data-stu-id="60445-198">1. Declare your variables</span></span>

<span data-ttu-id="60445-199">Não se esqueça de substituir os valores com aqueles que você deseja usar para sua configuração.</span><span class="sxs-lookup"><span data-stu-id="60445-199">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

```powershell
$RG2 = "TestBGPRG2"
$Location2 = "West US"
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
$GWIPName2 = "VNet2GWIP"
$GWIPconfName2 = "gwipconf2"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-testvnet2-in-the-new-resource-group"></a><span data-ttu-id="60445-200">2. Criar TestVNet2 no novo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="60445-200">2. Create TestVNet2 in the new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-the-vpn-gateway-for-testvnet2-with-bgp-parameters"></a><span data-ttu-id="60445-201">3. Criar um gateway de VPN para TestVNet2 com parâmetros de BGP</span><span class="sxs-lookup"><span data-stu-id="60445-201">3. Create the VPN gateway for TestVNet2 with BGP parameters</span></span>

<span data-ttu-id="60445-202">Solicite um endereço IP público a ser alocada para o gateway, você criará para a sua rede virtual e defina a sub-rede necessária e configurações de IP.</span><span class="sxs-lookup"><span data-stu-id="60445-202">Request a public IP address to be allocated to the gateway you will create for your VNet and define the required subnet and IP configurations.</span></span>

```powershell
$gwpip2    = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2     = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gwipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName2 -Subnet $subnet2 -PublicIpAddress $gwpip2
```

<span data-ttu-id="60445-203">Crie o gateway de VPN com o número AS.</span><span class="sxs-lookup"><span data-stu-id="60445-203">Create the VPN gateway with the AS number.</span></span> <span data-ttu-id="60445-204">Você deve substituir o ASN padrão em seus gateways de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="60445-204">You must override the default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="60445-205">As ASNs para as VNets conectadas devem ser diferentes para habilitar o BGP e roteamento de tráfego.</span><span class="sxs-lookup"><span data-stu-id="60445-205">The ASNs for the connected VNets must be different to enable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gwipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard -Asn $VNet2ASN
```

### <a name="step-2---connect-the-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="60445-206">Etapa 2 - Conectar os gateways de TestVNet1 e TestVNet2</span><span class="sxs-lookup"><span data-stu-id="60445-206">Step 2 - Connect the TestVNet1 and TestVNet2 gateways</span></span>

<span data-ttu-id="60445-207">Neste exemplo, ambos os gateways estão na mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="60445-207">In this example, both gateways are in the same subscription.</span></span> <span data-ttu-id="60445-208">Você pode concluir essa etapa na mesma sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="60445-208">You can complete this step in the same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="60445-209">1. Obter ambos os gateways</span><span class="sxs-lookup"><span data-stu-id="60445-209">1. Get both gateways</span></span>

<span data-ttu-id="60445-210">Certifique-se de fazer logon e se conectar à Assinatura 1.</span><span class="sxs-lookup"><span data-stu-id="60445-210">Make sure you log in and connect to Subscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="60445-211">2. Criar ambas as conexões</span><span class="sxs-lookup"><span data-stu-id="60445-211">2. Create both connections</span></span>

<span data-ttu-id="60445-212">Nesta etapa, você cria a conexão de TestVNet1 para TestVNet2 e a conexão de TestVNet2 to TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="60445-212">In this step, you create the connection from TestVNet1 to TestVNet2, and the connection from TestVNet2 to TestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="60445-213">Certifique-se de habilitar o BGP para AMBAS as conexões.</span><span class="sxs-lookup"><span data-stu-id="60445-213">Be sure to enable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="60445-214">Depois de concluir estas etapas, a conexão será estabelecida após alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="60445-214">After completing these steps, the connection is established after a few minutes.</span></span> <span data-ttu-id="60445-215">A sessão de emparelhamento via protocolo BGP fica ativa até a conclusão da conexão VNET a VNET.</span><span class="sxs-lookup"><span data-stu-id="60445-215">The BGP peering session is up once the VNet-to-VNet connection is completed.</span></span>

<span data-ttu-id="60445-216">Se você tiver concluído todas as partes deste exercício, estabeleceu a topologia de rede a seguir:</span><span class="sxs-lookup"><span data-stu-id="60445-216">If you completed all three parts of this exercise, you have established the following network topology:</span></span>

![BGP de VNet para VNet](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

## <a name="next-steps"></a><span data-ttu-id="60445-218">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="60445-218">Next steps</span></span>

<span data-ttu-id="60445-219">Quando sua conexão for concluída, você poderá adicionar máquinas virtuais às suas redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="60445-219">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="60445-220">Veja [Criar uma máquina virtual](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obter as etapas.</span><span class="sxs-lookup"><span data-stu-id="60445-220">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>