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
ms.openlocfilehash: a9d13ae6b319e2efa8965dc2955c9b89ac3fd12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-bgp-on-azure-vpn-gateways-using-powershell"></a><span data-ttu-id="a452b-103">Como tooconfigure BGP em Gateways de VPN do Azure usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="a452b-103">How tooconfigure BGP on Azure VPN Gateways using PowerShell</span></span>
<span data-ttu-id="a452b-104">Este artigo orienta Olá etapas tooenable BGP em uma conexão de VPN Site a Site (S2S) entre locais e uma conexão de rede virtual a rede usando o modelo de implantação do Gerenciador de recursos de saudação e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a452b-104">This article walks you through hello steps tooenable BGP on a cross-premises Site-to-Site (S2S) VPN connection and a VNet-to-VNet connection using hello Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-bgp"></a><span data-ttu-id="a452b-105">Sobre o BGP</span><span class="sxs-lookup"><span data-stu-id="a452b-105">About BGP</span></span>
<span data-ttu-id="a452b-106">O BGP é Olá protocolo de roteamento padrão usado em Olá tooexchange roteamento e acessibilidade informações da Internet entre duas ou mais redes.</span><span class="sxs-lookup"><span data-stu-id="a452b-106">BGP is hello standard routing protocol commonly used in hello Internet tooexchange routing and reachability information between two or more networks.</span></span> <span data-ttu-id="a452b-107">Habilita o BGP Olá Gateways de VPN do Azure e os dispositivos VPN local, chamados de pares de BGP ou vizinhos, tooexchange "rotas" informará ambos os gateways na disponibilidade hello e acessibilidade para os prefixos toogo por meio de gateways de saudação ou roteadores envolvidos.</span><span class="sxs-lookup"><span data-stu-id="a452b-107">BGP enables hello Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, tooexchange "routes" that will inform both gateways on hello availability and reachability for those prefixes toogo through hello gateways or routers involved.</span></span> <span data-ttu-id="a452b-108">BGP também pode habilitar o roteamento de tráfego entre várias redes propagando rotas aprende um gateway BGP de um tooall de par BGP outros pares de BGP.</span><span class="sxs-lookup"><span data-stu-id="a452b-108">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer tooall other BGP peers.</span></span>

<span data-ttu-id="a452b-109">Consulte [visão geral do BGP com Gateways de VPN do Azure](vpn-gateway-bgp-overview.md) para obter mais detalhes sobre os benefícios do BGP e toounderstand requisitos técnicos de saudação e considerações do uso de BGP.</span><span class="sxs-lookup"><span data-stu-id="a452b-109">See [Overview of BGP with Azure VPN Gateways](vpn-gateway-bgp-overview.md) for more discussion on benefits of BGP and toounderstand hello technical requirements and considerations of using BGP.</span></span>

## <a name="getting-started-with-bgp-on-azure-vpn-gateways"></a><span data-ttu-id="a452b-110">Introdução ao BGP em gateways de VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="a452b-110">Getting started with BGP on Azure VPN gateways</span></span>

<span data-ttu-id="a452b-111">Este artigo orienta Olá Olá de toodo etapas seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="a452b-111">This article walks you through hello steps toodo hello following tasks:</span></span>

* [<span data-ttu-id="a452b-112">Parte 1 - Habilitar o BGP em seu gateway de VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="a452b-112">Part 1 - Enable BGP on your Azure VPN gateway</span></span>](#enablebgp)
* [<span data-ttu-id="a452b-113">Parte 2 - Estabelecer uma conexão entre instalações com BGP</span><span class="sxs-lookup"><span data-stu-id="a452b-113">Part 2 - Establish a cross-premises connection with BGP</span></span>](#crossprembgp)
* [<span data-ttu-id="a452b-114">Parte 3 - Estabelecer uma conexão VNet para VNet com BGP</span><span class="sxs-lookup"><span data-stu-id="a452b-114">Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>](#v2vbgp)

<span data-ttu-id="a452b-115">Cada parte de instruções Olá constitui um bloco de construção básico para habilitar o BGP em sua conectividade de rede.</span><span class="sxs-lookup"><span data-stu-id="a452b-115">Each part of hello instructions forms a basic building block for enabling BGP in your network connectivity.</span></span> <span data-ttu-id="a452b-116">Se você concluir todas as três partes, criar uma topologia de hello, conforme mostrado no diagrama a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="a452b-116">If you complete all three parts, you build hello topology as shown in hello following diagram:</span></span>

![Topologia BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

<span data-ttu-id="a452b-118">Você pode combinar partes juntos toobuild uma rede de trânsito mais complexos e de vários saltos, que atende às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="a452b-118">You can combine parts together toobuild a more complex, multi-hop, transit network that meets your needs.</span></span>

## <span data-ttu-id="a452b-119"><a name ="enablebgp"></a>Parte 1 - configurar o BGP Olá Gateway de VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="a452b-119"><a name ="enablebgp"></a>Part 1 - Configure BGP on hello Azure VPN Gateway</span></span>
<span data-ttu-id="a452b-120">etapas de configuração de saudação configurar Olá parâmetros de BGP de gateway de VPN do Azure Olá conforme mostrado no diagrama a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="a452b-120">hello configuration steps set up hello BGP parameters of hello Azure VPN gateway as shown in hello following diagram:</span></span>

![Gateway BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-gateway.png)

### <a name="before-you-begin"></a><span data-ttu-id="a452b-122">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="a452b-122">Before you begin</span></span>
* <span data-ttu-id="a452b-123">Verifique se você tem uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="a452b-123">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="a452b-124">Se ainda não tiver uma assinatura do Azure, você poderá ativar os [Benefícios do assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se para obter uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a452b-124">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a452b-125">Instale os cmdlets do PowerShell do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="a452b-125">Install hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="a452b-126">Para obter mais informações sobre como instalar os cmdlets do PowerShell hello, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a452b-126">For more information about installing hello PowerShell cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="a452b-127">Etapa 1 - Criar e configurar VNet1</span><span class="sxs-lookup"><span data-stu-id="a452b-127">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="a452b-128">1. Declare as variáveis</span><span class="sxs-lookup"><span data-stu-id="a452b-128">1. Declare your variables</span></span>
<span data-ttu-id="a452b-129">Para este exercício, começaremos declarando nossa variáveis.</span><span class="sxs-lookup"><span data-stu-id="a452b-129">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="a452b-130">Olá, exemplo a seguir declara variáveis hello usando valores de saudação para este exercício.</span><span class="sxs-lookup"><span data-stu-id="a452b-130">hello following example declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="a452b-131">Ser valores de saudação tooreplace-se com seu próprio durante a configuração de produção.</span><span class="sxs-lookup"><span data-stu-id="a452b-131">Be sure tooreplace hello values with your own when configuring for production.</span></span> <span data-ttu-id="a452b-132">Você pode usar essas variáveis, se você estiver executando a saudação etapas toobecome familiarizado com esse tipo de configuração.</span><span class="sxs-lookup"><span data-stu-id="a452b-132">You can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="a452b-133">Modificar variáveis de Olá e, em seguida, copie e cole o console do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a452b-133">Modify hello variables, and then copy and paste into your PowerShell console.</span></span>

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

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="a452b-134">2. Conecte-se a assinatura de tooyour e criar um novo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="a452b-134">2. Connect tooyour subscription and create a new resource group</span></span>
<span data-ttu-id="a452b-135">toouse Olá cmdlets do Gerenciador de recursos, verifique se você alternar o modo de tooPowerShell.</span><span class="sxs-lookup"><span data-stu-id="a452b-135">toouse hello Resource Manager cmdlets, Make sure you switch tooPowerShell mode.</span></span> <span data-ttu-id="a452b-136">Para obter mais informações, consulte [Usando o Windows PowerShell com o Gerenciador de Recursos](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="a452b-136">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="a452b-137">Abra o console do PowerShell e conecte-se a conta de tooyour.</span><span class="sxs-lookup"><span data-stu-id="a452b-137">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="a452b-138">Use Olá toohelp de exemplo que você se conectar a seguir:</span><span class="sxs-lookup"><span data-stu-id="a452b-138">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="a452b-139">3. Criar TestVNet1</span><span class="sxs-lookup"><span data-stu-id="a452b-139">3. Create TestVNet1</span></span>
<span data-ttu-id="a452b-140">Olá, exemplo a seguir cria uma rede virtual denominada TestVNet1 e três sub-redes, um GatewaySubnet chamado, um front-end chamado e back-end chamado um.</span><span class="sxs-lookup"><span data-stu-id="a452b-140">hello following sample creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="a452b-141">Ao substituir valores, é importante você sempre nomear sua sub-rede de gateway especificamente como GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="a452b-141">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="a452b-142">Se você usar outro nome, a criação do gateway falhará.</span><span class="sxs-lookup"><span data-stu-id="a452b-142">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-bgp-parameters"></a><span data-ttu-id="a452b-143">Etapa 2: criar hello Gateway VPN para TestVNet1 com parâmetros de BGP</span><span class="sxs-lookup"><span data-stu-id="a452b-143">Step 2 - Create hello VPN Gateway for TestVNet1 with BGP parameters</span></span>
#### <a name="1-create-hello-ip-and-subnet-configurations"></a><span data-ttu-id="a452b-144">1. Criar configurações de IP e a sub-rede de saudação</span><span class="sxs-lookup"><span data-stu-id="a452b-144">1. Create hello IP and subnet configurations</span></span>
<span data-ttu-id="a452b-145">Solicite um público endereço toobe toohello alocado gateway IP que você criará para sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="a452b-145">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="a452b-146">Você também definirá sub-rede Olá necessário e as configurações de IP.</span><span class="sxs-lookup"><span data-stu-id="a452b-146">You'll also define hello required subnet and IP configurations.</span></span>

```powershell
$gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1
```

#### <a name="2-create-hello-vpn-gateway-with-hello-as-number"></a><span data-ttu-id="a452b-147">2. Criar gateway VPN Olá com hello como número</span><span class="sxs-lookup"><span data-stu-id="a452b-147">2. Create hello VPN gateway with hello AS number</span></span>
<span data-ttu-id="a452b-148">Crie gateway de rede virtual Olá para TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="a452b-148">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="a452b-149">BGP requer um baseadas em rota gateway VPN e o parâmetro hello adição - Asn tooset Olá ASN (número) para TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="a452b-149">BGP requires a Route-Based VPN gateway, and also hello addition parameter, -Asn, tooset hello ASN (AS Number) for TestVNet1.</span></span> <span data-ttu-id="a452b-150">Se você não definir parâmetro ASN hello, ASN 65515 é atribuído.</span><span class="sxs-lookup"><span data-stu-id="a452b-150">If you do not set hello ASN parameter, ASN 65515 is assigned.</span></span> <span data-ttu-id="a452b-151">Criar um gateway pode demorar um pouco (30 minutos ou mais toocomplete).</span><span class="sxs-lookup"><span data-stu-id="a452b-151">Creating a gateway can take a while (30 minutes or more toocomplete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance -Asn $VNet1ASN
```

#### <a name="3-obtain-hello-azure-bgp-peer-ip-address"></a><span data-ttu-id="a452b-152">3. Obter o endereço de IP de par de BGP Azure Olá</span><span class="sxs-lookup"><span data-stu-id="a452b-152">3. Obtain hello Azure BGP Peer IP address</span></span>
<span data-ttu-id="a452b-153">Depois de criar gateway Olá, é necessário tooobtain Olá BGP Peer endereço IP de saudação Gateway de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="a452b-153">Once hello gateway is created, you need tooobtain hello BGP Peer IP address on hello Azure VPN Gateway.</span></span> <span data-ttu-id="a452b-154">Esse endereço é necessário tooconfigure Olá Gateway de VPN do Azure como um par de BGP para seus dispositivos VPN local.</span><span class="sxs-lookup"><span data-stu-id="a452b-154">This address is needed tooconfigure hello Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet1gw.BgpSettingsText
```

<span data-ttu-id="a452b-155">comando último Olá mostra configurações de BGP correspondentes da saudação no hello Gateway de VPN do Azure; Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a452b-155">hello last command shows hello corresponding BGP configurations on hello Azure VPN Gateway; for example:</span></span>

```powershell
$vnet1gw.BgpSettingsText
{
    "Asn": 65010,
    "BgpPeeringAddress": "10.12.255.30",
    "PeerWeight": 0
}
```

<span data-ttu-id="a452b-156">Depois que o gateway de saudação é criado, você pode usar esta conexão do gateway tooestablish entre locais ou a conexão de rede virtual a rede com BGP.</span><span class="sxs-lookup"><span data-stu-id="a452b-156">Once hello gateway is created, you can use this gateway tooestablish cross-premises connection or VNet-to-VNet connection with BGP.</span></span> <span data-ttu-id="a452b-157">Olá seções a seguir percorrer Olá etapas toocomplete Olá exercício.</span><span class="sxs-lookup"><span data-stu-id="a452b-157">hello following sections walk through hello steps toocomplete hello exercise.</span></span>

## <span data-ttu-id="a452b-158"><a name ="crossprembbgp"></a>Parte 2 - Estabelecer uma conexão entre instalações com BGP</span><span class="sxs-lookup"><span data-stu-id="a452b-158"><a name ="crossprembbgp"></a>Part 2 - Establish a cross-premises connection with BGP</span></span>

<span data-ttu-id="a452b-159">tooestablish uma conexão entre locais, você precisa toocreate toorepresent um Gateway de rede Local seu dispositivo VPN no local e um gateway VPN de saudação tooconnect Conexão com o gateway de rede local hello.</span><span class="sxs-lookup"><span data-stu-id="a452b-159">tooestablish a cross-premises connection, you need toocreate a Local Network Gateway toorepresent your on-premises VPN device, and a Connection tooconnect hello VPN gateway with hello local network gateway.</span></span> <span data-ttu-id="a452b-160">Enquanto há artigos que orientá-lo através dessas etapas, este artigo contém parâmetros de configuração de BGP Olá propriedades adicionais necessárias toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="a452b-160">While there are articles that walk you through these steps, this article contains hello additional properties required toospecify hello BGP configuration parameters.</span></span>

![BGP para entre instalações](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crossprem.png)

<span data-ttu-id="a452b-162">Antes de prosseguir, verifique se você concluiu a [Parte 1](#enablebgp) deste exercício.</span><span class="sxs-lookup"><span data-stu-id="a452b-162">Before proceeding, make sure you have completed [Part 1](#enablebgp) of this exercise.</span></span>

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a><span data-ttu-id="a452b-163">Etapa 1: criar e configurar o gateway de rede local Olá</span><span class="sxs-lookup"><span data-stu-id="a452b-163">Step 1 - Create and configure hello local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="a452b-164">1. Declare as variáveis</span><span class="sxs-lookup"><span data-stu-id="a452b-164">1. Declare your variables</span></span>

<span data-ttu-id="a452b-165">Este exercício continua a configuração de saudação toobuild mostrada no diagrama de saudação.</span><span class="sxs-lookup"><span data-stu-id="a452b-165">This exercise continues toobuild hello configuration shown in hello diagram.</span></span> <span data-ttu-id="a452b-166">Ser tooreplace se valores Olá Olá aqueles que você deseja toouse para sua configuração.</span><span class="sxs-lookup"><span data-stu-id="a452b-166">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG5 = "TestBGPRG5"
$Location5 = "East US 2"
$LNGName5 = "Site5"
$LNGPrefix50 = "10.52.255.254/32"
$LNGIP5 = "Your_VPN_Device_IP"
$LNGASN5 = 65050
$BGPPeerIP5 = "10.52.255.254"
```

<span data-ttu-id="a452b-167">Algumas coisas toonote sobre parâmetros de gateway de rede local hello:</span><span class="sxs-lookup"><span data-stu-id="a452b-167">A couple of things toonote regarding hello local network gateway parameters:</span></span>

* <span data-ttu-id="a452b-168">gateway de rede local Olá pode estar em Olá mesmo ou outro local e o recurso grupo Olá gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="a452b-168">hello local network gateway can be in hello same or different location and resource group as hello VPN gateway.</span></span> <span data-ttu-id="a452b-169">Este exemplo os mostra em grupos de recursos diferentes em locais diferentes.</span><span class="sxs-lookup"><span data-stu-id="a452b-169">This example shows them in different resource groups in different locations.</span></span>
* <span data-ttu-id="a452b-170">prefixo de mínimo Olá precisar toodeclare para gateway de rede local Olá é endereço do host de saudação do seu endereço IP de par de BGP em seu dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="a452b-170">hello minimum prefix you need toodeclare for hello local network gateway is hello host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="a452b-171">Nesse caso, é um prefixo /32 de "10.52.255.254/32".</span><span class="sxs-lookup"><span data-stu-id="a452b-171">In this case, it's a /32 prefix of "10.52.255.254/32".</span></span>
* <span data-ttu-id="a452b-172">Como lembrete, você deve usar diferentes ASNs BGP entre suas redes locais e a VNet do Azure.</span><span class="sxs-lookup"><span data-stu-id="a452b-172">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="a452b-173">Se eles são hello mesmo, você precisará toochange sua VNet ASN se seu dispositivo VPN local já usa Olá ASN toopeer com outros vizinhos de BGP.</span><span class="sxs-lookup"><span data-stu-id="a452b-173">If they are hello same, you need toochange your VNet ASN if your on-premises VPN device already uses hello ASN toopeer with other BGP neighbors.</span></span>

<span data-ttu-id="a452b-174">Antes de continuar, verifique se que você está conectado ainda tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="a452b-174">Before you continue, make sure you are still connected tooSubscription 1.</span></span>

#### <a name="2-create-hello-local-network-gateway-for-site5"></a><span data-ttu-id="a452b-175">2. Criar gateway de rede local Olá para Site5</span><span class="sxs-lookup"><span data-stu-id="a452b-175">2. Create hello local network gateway for Site5</span></span>

<span data-ttu-id="a452b-176">Ser-se de grupo de recursos de saudação toocreate se ele não for criado, antes de criar o gateway de rede local hello.</span><span class="sxs-lookup"><span data-stu-id="a452b-176">Be sure toocreate hello resource group if it is not created, before you create hello local network gateway.</span></span> <span data-ttu-id="a452b-177">Observe os parâmetros adicionais de saudação dois para gateway de rede local Olá: Asn e BgpPeerAddress.</span><span class="sxs-lookup"><span data-stu-id="a452b-177">Notice hello two additional parameters for hello local network gateway: Asn and BgpPeerAddress.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="a452b-178">Etapa 2: conectar-se o gateway de rede virtual hello e gateway de rede local</span><span class="sxs-lookup"><span data-stu-id="a452b-178">Step 2 - Connect hello VNet gateway and local network gateway</span></span>

#### <a name="1-get-hello-two-gateways"></a><span data-ttu-id="a452b-179">1. Obter Olá dois gateways</span><span class="sxs-lookup"><span data-stu-id="a452b-179">1. Get hello two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a><span data-ttu-id="a452b-180">2. Criar conexão de tooSite5 TestVNet1 Olá</span><span class="sxs-lookup"><span data-stu-id="a452b-180">2. Create hello TestVNet1 tooSite5 connection</span></span>

<span data-ttu-id="a452b-181">Nesta etapa, você pode criar conexão de saudação do TestVNet1 tooSite5.</span><span class="sxs-lookup"><span data-stu-id="a452b-181">In this step, you create hello connection from TestVNet1 tooSite5.</span></span> <span data-ttu-id="a452b-182">Você deve especificar "-EnableBGP $True" tooenable BGP para esta conexão.</span><span class="sxs-lookup"><span data-stu-id="a452b-182">You must specify "-EnableBGP $True" tooenable BGP for this connection.</span></span> <span data-ttu-id="a452b-183">Como discutido anteriormente, é possível toohave conexões de BGP e BGP não Olá mesmo Gateway de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="a452b-183">As discussed earlier, it is possible toohave both BGP and non-BGP connections for hello same Azure VPN Gateway.</span></span> <span data-ttu-id="a452b-184">A menos que o BGP é habilitado na propriedade de conexão Olá, Azure não irá habilitar BGP para esta conexão, embora os parâmetros BGP já estão configurados em ambos os gateways.</span><span class="sxs-lookup"><span data-stu-id="a452b-184">Unless BGP is enabled in hello connection property, Azure will not enable BGP for this connection even though BGP parameters are already configured on both gateways.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

<span data-ttu-id="a452b-185">Olá exemplo a seguir lista os parâmetros de saudação inseridos na seção de configuração de BGP de saudação em seu dispositivo VPN local para este exercício:</span><span class="sxs-lookup"><span data-stu-id="a452b-185">hello following example lists hello parameters you enter into hello BGP configuration section on your on-premises VPN device for this exercise:</span></span>

```

- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP    : 10.12.255.30
- Static route         : Add a route for 10.12.255.30/32, with nexthop being hello VPN tunnel interface on your device
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="a452b-186">conexão de saudação é estabelecida após alguns minutos e inicia Olá BGP de emparelhamento sessão uma vez estabelecida a conexão IPsec de saudação.</span><span class="sxs-lookup"><span data-stu-id="a452b-186">hello connection is established after a few minutes, and hello BGP peering session starts once hello IPsec connection is established.</span></span>

## <span data-ttu-id="a452b-187"><a name ="v2vbgp"></a>Parte 3 - Estabelecer uma conexão VNet para VNet com BGP</span><span class="sxs-lookup"><span data-stu-id="a452b-187"><a name ="v2vbgp"></a>Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>

<span data-ttu-id="a452b-188">Esta seção adiciona uma conexão de rede virtual a rede com BGP, conforme mostrado no diagrama a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="a452b-188">This section adds a VNet-to-VNet connection with BGP, as shown in hello following diagram:</span></span>

![BGP de VNet para VNet](./media/vpn-gateway-bgp-resource-manager-ps/bgp-vnet2vnet.png)

<span data-ttu-id="a452b-190">Olá seguindo instruções continuar nas etapas anteriores hello.</span><span class="sxs-lookup"><span data-stu-id="a452b-190">hello following instructions continue from hello previous steps.</span></span> <span data-ttu-id="a452b-191">Você deve concluir [parte I](#enablebgp) toocreate configurar TestVNet1 e Olá Gateway de VPN com o BGP.</span><span class="sxs-lookup"><span data-stu-id="a452b-191">You must complete [Part I](#enablebgp) toocreate and configure TestVNet1 and hello VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a><span data-ttu-id="a452b-192">Etapa 1 - criar TestVNet2 e hello gateway VPN</span><span class="sxs-lookup"><span data-stu-id="a452b-192">Step 1 - Create TestVNet2 and hello VPN gateway</span></span>

<span data-ttu-id="a452b-193">É importante toomake-se de que o espaço de endereço IP de saudação do hello nova rede virtual, TestVNet2, não coincide com nenhum dos seus intervalos de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="a452b-193">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="a452b-194">Neste exemplo, redes virtuais Olá pertencem toohello mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="a452b-194">In this example, hello virtual networks belong toohello same subscription.</span></span> <span data-ttu-id="a452b-195">Você pode configurar conexões de rede virtual a rede entre assinaturas diferentes.</span><span class="sxs-lookup"><span data-stu-id="a452b-195">You can set up VNet-to-VNet connections between different subscriptions.</span></span> <span data-ttu-id="a452b-196">Para saber mais, veja [Configurar uma conexão VNet com VNet](vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="a452b-196">For more information, see [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md).</span></span> <span data-ttu-id="a452b-197">Certifique-se de adicionar hello "-EnableBgp $True" ao criar hello conexões tooenable BGP.</span><span class="sxs-lookup"><span data-stu-id="a452b-197">Make sure you add hello "-EnableBgp $True" when creating hello connections tooenable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="a452b-198">1. Declare as variáveis</span><span class="sxs-lookup"><span data-stu-id="a452b-198">1. Declare your variables</span></span>

<span data-ttu-id="a452b-199">Ser tooreplace se valores Olá Olá aqueles que você deseja toouse para sua configuração.</span><span class="sxs-lookup"><span data-stu-id="a452b-199">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

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

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a><span data-ttu-id="a452b-200">2. Criar TestVNet2 no novo grupo de recursos Olá</span><span class="sxs-lookup"><span data-stu-id="a452b-200">2. Create TestVNet2 in hello new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-vpn-gateway-for-testvnet2-with-bgp-parameters"></a><span data-ttu-id="a452b-201">3. Criar gateway VPN Olá para TestVNet2 com parâmetros de BGP</span><span class="sxs-lookup"><span data-stu-id="a452b-201">3. Create hello VPN gateway for TestVNet2 with BGP parameters</span></span>

<span data-ttu-id="a452b-202">Solicite um público endereço toobe toohello alocado gateway IP você criará para a sua rede virtual e defina a sub-rede Olá necessário e as configurações de IP.</span><span class="sxs-lookup"><span data-stu-id="a452b-202">Request a public IP address toobe allocated toohello gateway you will create for your VNet and define hello required subnet and IP configurations.</span></span>

```powershell
$gwpip2    = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2     = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gwipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName2 -Subnet $subnet2 -PublicIpAddress $gwpip2
```

<span data-ttu-id="a452b-203">Criar gateway VPN Olá com hello como número.</span><span class="sxs-lookup"><span data-stu-id="a452b-203">Create hello VPN gateway with hello AS number.</span></span> <span data-ttu-id="a452b-204">Você deve substituir o padrão de saudação ASN em seus gateways de VPN do Azure.</span><span class="sxs-lookup"><span data-stu-id="a452b-204">You must override hello default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="a452b-205">Olá ASNs para Olá conectado VNets deve ser diferente tooenable BGP e roteamento de tráfego.</span><span class="sxs-lookup"><span data-stu-id="a452b-205">hello ASNs for hello connected VNets must be different tooenable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gwipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard -Asn $VNet2ASN
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="a452b-206">Etapa 2: conectar gateways de TestVNet1 e TestVNet2 Olá</span><span class="sxs-lookup"><span data-stu-id="a452b-206">Step 2 - Connect hello TestVNet1 and TestVNet2 gateways</span></span>

<span data-ttu-id="a452b-207">Neste exemplo, ambos os gateways estão em Olá mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="a452b-207">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="a452b-208">Você pode concluir esta etapa no hello mesma sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a452b-208">You can complete this step in hello same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="a452b-209">1. Obter ambos os gateways</span><span class="sxs-lookup"><span data-stu-id="a452b-209">1. Get both gateways</span></span>

<span data-ttu-id="a452b-210">Certifique-se de entrar e conectar-se tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="a452b-210">Make sure you log in and connect tooSubscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="a452b-211">2. Criar ambas as conexões</span><span class="sxs-lookup"><span data-stu-id="a452b-211">2. Create both connections</span></span>

<span data-ttu-id="a452b-212">Nesta etapa, você criar conexão de saudação do TestVNet1 tooTestVNet2 e conexão de saudação do TestVNet2 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="a452b-212">In this step, you create hello connection from TestVNet1 tooTestVNet2, and hello connection from TestVNet2 tooTestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="a452b-213">Ser tooenable se BGP para ambas as conexões.</span><span class="sxs-lookup"><span data-stu-id="a452b-213">Be sure tooenable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="a452b-214">Depois de concluir essas etapas, é estabelecida conexão Olá após alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="a452b-214">After completing these steps, hello connection is established after a few minutes.</span></span> <span data-ttu-id="a452b-215">sessão de emparelhamento Olá BGP é concluída Olá conexão de rede virtual a rede.</span><span class="sxs-lookup"><span data-stu-id="a452b-215">hello BGP peering session is up once hello VNet-to-VNet connection is completed.</span></span>

<span data-ttu-id="a452b-216">Se você concluiu todas as três partes para este exercício, estabelecer Olá topologia de rede a seguir:</span><span class="sxs-lookup"><span data-stu-id="a452b-216">If you completed all three parts of this exercise, you have established hello following network topology:</span></span>

![BGP de VNet para VNet](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

## <a name="next-steps"></a><span data-ttu-id="a452b-218">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a452b-218">Next steps</span></span>

<span data-ttu-id="a452b-219">Quando a conexão for concluída, você pode adicionar máquinas virtuais tooyour as redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="a452b-219">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="a452b-220">Veja [Criar uma máquina virtual](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obter as etapas.</span><span class="sxs-lookup"><span data-stu-id="a452b-220">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
