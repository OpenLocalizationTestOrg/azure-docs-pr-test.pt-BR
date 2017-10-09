---
title: 'Conecte-se a sua rede de local tooan rede virtual do Azure: VPN Site a Site: PowerShell | Microsoft Docs'
description: "Etapas toocreate uma conexão IPsec de seu local de rede tooan rede virtual do Azure sobre Olá Internet pública. Essas etapas o ajudarão a criar uma conexão de Gateway de VPN Site a Site entre locais usando o PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fcc2fda5-4493-4c15-9436-84d35adbda8e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: cb8db1dab3a5488816a7f7e8e63908a4c02f55db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vnet-with-a-site-to-site-vpn-connection-using-powershell"></a><span data-ttu-id="92d98-104">Criar uma Rede Virtual com uma conexão VPN site a site usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="92d98-104">Create a VNet with a Site-to-Site VPN connection using PowerShell</span></span>

<span data-ttu-id="92d98-105">Este artigo mostra como toouse conexão de gateway VPN do PowerShell toocreate uma Site a Site do seu local de rede toohello VNet.</span><span class="sxs-lookup"><span data-stu-id="92d98-105">This article shows you how toouse PowerShell toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="92d98-106">Olá etapas neste artigo se aplicam a modelo de implantação do Gerenciador de recursos de toohello.</span><span class="sxs-lookup"><span data-stu-id="92d98-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="92d98-107">Você também pode criar essa configuração usando uma ferramenta de implantação diferente ou um modelo de implantação, selecionando uma opção diferente de saudação lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="92d98-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="92d98-108">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="92d98-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="92d98-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="92d98-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="92d98-110">CLI</span><span class="sxs-lookup"><span data-stu-id="92d98-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="92d98-111">Portal do Azure (clássico)</span><span class="sxs-lookup"><span data-stu-id="92d98-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> * [<span data-ttu-id="92d98-112">Portal clássico (clássico)</span><span class="sxs-lookup"><span data-stu-id="92d98-112">Classic portal (classic)</span></span>](vpn-gateway-site-to-site-create.md)
> 
>


<span data-ttu-id="92d98-113">Uma conexão de gateway VPN Site a Site é usado tooconnect seu local de rede tooan rede virtual do Azure por um túnel VPN IPsec/IKE (IKEv1 ou IKEv2).</span><span class="sxs-lookup"><span data-stu-id="92d98-113">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="92d98-114">Esse tipo de conexão exige um VPN de dispositivos localizado localmente que tenha uma tooit de endereço atribuído de IP público externamente.</span><span class="sxs-lookup"><span data-stu-id="92d98-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="92d98-115">Para saber mais sobre os gateways de VPN, veja [Sobre o gateway de VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="92d98-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![Diagrama de conexão Site a Site de Gateway de VPN entre locais](./media/vpn-gateway-create-site-to-site-rm-powershell/site-to-site-diagram.png)

## <span data-ttu-id="92d98-117"><a name="before"></a>Antes de começar</span><span class="sxs-lookup"><span data-stu-id="92d98-117"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="92d98-118">Verifique se você atendeu a saudação critérios a seguir antes de começar a configuração:</span><span class="sxs-lookup"><span data-stu-id="92d98-118">Verify that you have met hello following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="92d98-119">Verifique se você tem um dispositivo VPN compatível e alguém que é capaz de tooconfigure-lo.</span><span class="sxs-lookup"><span data-stu-id="92d98-119">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="92d98-120">Para obter mais informações sobre dispositivos VPN compatíveis e a configuração de dispositivo, confira [Sobre dispositivos VPN](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="92d98-120">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="92d98-121">Verifique se você possui um endereço IPv4 público voltado para o exterior para seu dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="92d98-121">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="92d98-122">Esse endereço IP não pode estar localizado atrás de um NAT.</span><span class="sxs-lookup"><span data-stu-id="92d98-122">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="92d98-123">Se você não estiver familiarizado com intervalos de endereços IP de saudação localizados na configuração de rede local, é necessário toocoordinate com alguém que possa fornecer os detalhes para você.</span><span class="sxs-lookup"><span data-stu-id="92d98-123">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="92d98-124">Quando você criar essa configuração, você deve especificar os prefixos de intervalo endereço IP hello Azure encaminhe tooyour no local.</span><span class="sxs-lookup"><span data-stu-id="92d98-124">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="92d98-125">Nenhuma das sub-redes Olá da sua rede local pode ser sobre colo com sub-redes de rede virtual Olá que você deseja tooconnect para.</span><span class="sxs-lookup"><span data-stu-id="92d98-125">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span>
* <span data-ttu-id="92d98-126">Instale a versão mais recente Olá de saudação cmdlets do PowerShell do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="92d98-126">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="92d98-127">Cmdlets do PowerShell são atualizados com frequência e você geralmente precisará tooupdate sua funcionalidade de recurso mais recente de saudação do PowerShell cmdlets tooget.</span><span class="sxs-lookup"><span data-stu-id="92d98-127">PowerShell cmdlets are updated frequently and you will typically need tooupdate your PowerShell cmdlets tooget hello latest feature functionality.</span></span> <span data-ttu-id="92d98-128">Se você não atualizar seus cmdlets do PowerShell, valores hello especificados poderão falhar.</span><span class="sxs-lookup"><span data-stu-id="92d98-128">If you don't update your PowerShell cmdlets, hello values specified may fail.</span></span> <span data-ttu-id="92d98-129">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para obter mais informações sobre como baixar e instalar os cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="92d98-129">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about downloading and installing PowerShell cmdlets.</span></span>

### <span data-ttu-id="92d98-130"><a name="example"></a>Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="92d98-130"><a name="example"></a>Example values</span></span>

<span data-ttu-id="92d98-131">Olá exemplos neste artigo usam Olá valores a seguir.</span><span class="sxs-lookup"><span data-stu-id="92d98-131">hello examples in this article use hello following values.</span></span> <span data-ttu-id="92d98-132">Você pode usar esses valores toocreate um ambiente de teste, ou consulte toothem toobetter entender exemplos Olá neste artigo.</span><span class="sxs-lookup"><span data-stu-id="92d98-132">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

```
#Example values

VnetName                = TestVNet1
ResourceGroup           = TestRG1
Location                = East US 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.1.0/28 
GatewaySubnet           = 10.11.0.0/27
LocalNetworkGatewayName = Site2
LNG Public IP           = <VPN device IP address> 
Local Address Prefixes  = 10.0.0.0/24, 20.0.0.0/24
Gateway Name            = VNet1GW
PublicIP                = VNet1GWIP
Gateway IP Config       = gwipconfig1 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2

```


## <span data-ttu-id="92d98-133"><a name="Login"></a>1. Conecte-se a assinatura de tooyour</span><span class="sxs-lookup"><span data-stu-id="92d98-133"><a name="Login"></a>1. Connect tooyour subscription</span></span>

[!INCLUDE [PowerShell login](../../includes/vpn-gateway-ps-login-include.md)]

## <span data-ttu-id="92d98-134"><a name="VNet"></a>2. Criar uma rede virtual e uma sub-rede de gateway</span><span class="sxs-lookup"><span data-stu-id="92d98-134"><a name="VNet"></a>2. Create a virtual network and a gateway subnet</span></span>

<span data-ttu-id="92d98-135">Se você ainda não tiver uma rede virtual, crie uma.</span><span class="sxs-lookup"><span data-stu-id="92d98-135">If you don't already have a virtual network, create one.</span></span> <span data-ttu-id="92d98-136">Ao criar uma rede virtual, certifique-se de que os espaços de endereço Olá que você especificar não se sobrepõem a nenhum Olá dos espaços de endereço que você tem em sua rede local.</span><span class="sxs-lookup"><span data-stu-id="92d98-136">When creating a virtual network, make sure that hello address spaces you specify don't overlap any of hello address spaces that you have on your on-premises network.</span></span>

[!INCLUDE [About gateway subnets](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [No NSG warning](../../includes/vpn-gateway-no-nsg-include.md)]

### <span data-ttu-id="92d98-137"><a name="vnet"></a>toocreate uma rede virtual e uma sub-rede do gateway</span><span class="sxs-lookup"><span data-stu-id="92d98-137"><a name="vnet"></a>toocreate a virtual network and a gateway subnet</span></span>

<span data-ttu-id="92d98-138">O exemplo a seguir cria uma rede virtual e uma sub-rede de gateway.</span><span class="sxs-lookup"><span data-stu-id="92d98-138">This example creates a virtual network and a gateway subnet.</span></span> <span data-ttu-id="92d98-139">Se você já tiver uma rede virtual que você precisa tooadd uma sub-rede do gateway para ver [tooadd uma gateway sub-rede tooa rede virtual já tiver criado](#gatewaysubnet).</span><span class="sxs-lookup"><span data-stu-id="92d98-139">If you already have a virtual network that you need tooadd a gateway subnet to, see [tooadd a gateway subnet tooa virtual network you have already created](#gatewaysubnet).</span></span>

<span data-ttu-id="92d98-140">Crie um grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="92d98-140">Create a resource group:</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location 'East US'
```

<span data-ttu-id="92d98-141">Criar sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="92d98-141">Create your virtual network.</span></span>

1. <span data-ttu-id="92d98-142">Definir variáveis de saudação.</span><span class="sxs-lookup"><span data-stu-id="92d98-142">Set hello variables.</span></span>

  ```powershell
  $subnet1 = New-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27
  $subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name 'Subnet1' -AddressPrefix 10.11.1.0/28
  ```
2. <span data-ttu-id="92d98-143">Crie hello VNet.</span><span class="sxs-lookup"><span data-stu-id="92d98-143">Create hello VNet.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1 `
  -Location 'East US' -AddressPrefix 10.11.0.0/16 -Subnet $subnet1, $subnet2
  ```

### <span data-ttu-id="92d98-144"><a name="gatewaysubnet"></a>tooadd uma rede virtual do gateway sub-rede tooa você já criou</span><span class="sxs-lookup"><span data-stu-id="92d98-144"><a name="gatewaysubnet"></a>tooadd a gateway subnet tooa virtual network you have already created</span></span>

1. <span data-ttu-id="92d98-145">Definir variáveis de saudação.</span><span class="sxs-lookup"><span data-stu-id="92d98-145">Set hello variables.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG1 -Name TestVet1
  ```
2. <span data-ttu-id="92d98-146">Crie uma sub-rede de gateway hello.</span><span class="sxs-lookup"><span data-stu-id="92d98-146">Create hello gateway subnet.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27 -VirtualNetwork $vnet
  ```
3. <span data-ttu-id="92d98-147">Definir a configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="92d98-147">Set hello configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```

## <span data-ttu-id="92d98-148">3. <a name="localnet"></a>Criar gateway de rede local Olá</span><span class="sxs-lookup"><span data-stu-id="92d98-148">3. <a name="localnet"></a>Create hello local network gateway</span></span>

<span data-ttu-id="92d98-149">Normalmente, o gateway de rede local Olá refere-se tooyour no local.</span><span class="sxs-lookup"><span data-stu-id="92d98-149">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="92d98-150">Atribuir o site Olá um nome pelo qual Azure pode consulte tooit e especifique o endereço IP de saudação do hello toowhich de dispositivo VPN de local, você criará uma conexão.</span><span class="sxs-lookup"><span data-stu-id="92d98-150">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="92d98-151">Você também pode especificar prefixos de endereço IP de saudação que serão encaminhados através do dispositivo de VPN toohello do gateway VPN hello.</span><span class="sxs-lookup"><span data-stu-id="92d98-151">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="92d98-152">especificar os prefixos de endereço Olá são prefixos Olá localizados em sua rede local.</span><span class="sxs-lookup"><span data-stu-id="92d98-152">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="92d98-153">Se sua rede local for alterada, você pode atualizar facilmente prefixos hello.</span><span class="sxs-lookup"><span data-stu-id="92d98-153">If your on-premises network changes, you can easily update hello prefixes.</span></span>

<span data-ttu-id="92d98-154">Use Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="92d98-154">Use hello following values:</span></span>

* <span data-ttu-id="92d98-155">Olá *GatewayIPAddress* é o endereço IP de saudação do seu dispositivo VPN local.</span><span class="sxs-lookup"><span data-stu-id="92d98-155">hello *GatewayIPAddress* is hello IP address of your on-premises VPN device.</span></span> <span data-ttu-id="92d98-156">O dispositivo VPN não pode estar localizado atrás de um NAT.</span><span class="sxs-lookup"><span data-stu-id="92d98-156">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="92d98-157">Olá *AddressPrefix* é espaço de endereço de seu local.</span><span class="sxs-lookup"><span data-stu-id="92d98-157">hello *AddressPrefix* is your on-premises address space.</span></span>

<span data-ttu-id="92d98-158">tooadd um gateway de rede local com um único prefixo de endereço:</span><span class="sxs-lookup"><span data-stu-id="92d98-158">tooadd a local network gateway with a single address prefix:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.0.0.0/24'
  ```

<span data-ttu-id="92d98-159">tooadd um gateway de rede local com vários prefixos de endereço:</span><span class="sxs-lookup"><span data-stu-id="92d98-159">tooadd a local network gateway with multiple address prefixes:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix @('10.0.0.0/24','20.0.0.0/24')
  ```

<span data-ttu-id="92d98-160">prefixos de endereço IP de toomodify para o gateway de rede local:</span><span class="sxs-lookup"><span data-stu-id="92d98-160">toomodify IP address prefixes for your local network gateway:</span></span><br>
<span data-ttu-id="92d98-161">Às vezes, os prefixos de gateway de rede local são alterados.</span><span class="sxs-lookup"><span data-stu-id="92d98-161">Sometimes your local network gateway prefixes change.</span></span> <span data-ttu-id="92d98-162">etapas de saudação você tomar toomodify seu endereço IP prefixos dependem se você tiver criado uma conexão de gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="92d98-162">hello steps you take toomodify your IP address prefixes depend on whether you have created a VPN gateway connection.</span></span> <span data-ttu-id="92d98-163">Consulte Olá [prefixos de endereço IP modificar para um gateway de rede local](#modify) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="92d98-163">See hello [Modify IP address prefixes for a local network gateway](#modify) section of this article.</span></span>

## <span data-ttu-id="92d98-164"><a name="PublicIP"></a>4. Solicite um endereço IP público</span><span class="sxs-lookup"><span data-stu-id="92d98-164"><a name="PublicIP"></a>4. Request a Public IP address</span></span>

<span data-ttu-id="92d98-165">Um gateway de VPN deve ter um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="92d98-165">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="92d98-166">Você primeiro solicitar o recurso de endereço IP hello e, em seguida, consulte tooit ao criar o gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="92d98-166">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="92d98-167">endereço IP de saudação é atribuído dinamicamente recursos toohello ao gateway de VPN Olá é criado.</span><span class="sxs-lookup"><span data-stu-id="92d98-167">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="92d98-168">O gateway de VPN atualmente suporta apenas alocação de endereços IP público *Dinâmico*.</span><span class="sxs-lookup"><span data-stu-id="92d98-168">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="92d98-169">Você não pode solicitar uma atribuição de endereço IP Público Estático.</span><span class="sxs-lookup"><span data-stu-id="92d98-169">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="92d98-170">No entanto, isso não significa que o endereço IP de saudação alterado depois que ele foi atribuído tooyour gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="92d98-170">However, this does not mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="92d98-171">somente tempo de saudação alterações de endereço IP público hello quando é Olá gateway é excluído e criado novamente.</span><span class="sxs-lookup"><span data-stu-id="92d98-171">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="92d98-172">Isso não altera o redimensionamento, a redefinição ou outras manutenções/atualizações internas do seu gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="92d98-172">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="92d98-173">Solicite um endereço IP público que será atribuído tooyour de gateway VPN de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="92d98-173">Request a Public IP address that will be assigned tooyour virtual network VPN gateway.</span></span>

```powershell
$gwpip= New-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName TestRG1 -Location 'East US' -AllocationMethod Dynamic
```

## <span data-ttu-id="92d98-174"><a name="GatewayIPConfig"></a>5. Criar a configuração de endereçamento de IP de gateway Olá</span><span class="sxs-lookup"><span data-stu-id="92d98-174"><a name="GatewayIPConfig"></a>5. Create hello gateway IP addressing configuration</span></span>

<span data-ttu-id="92d98-175">configuração do gateway Olá define sub-rede hello e toouse de endereço IP público hello.</span><span class="sxs-lookup"><span data-stu-id="92d98-175">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="92d98-176">Use sua configuração de gateway de Olá toocreate de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="92d98-176">Use hello following example toocreate your gateway configuration:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name gwipconfig1 -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
```

## <span data-ttu-id="92d98-177"><a name="CreateGateway"></a>6. Criar gateway VPN Olá</span><span class="sxs-lookup"><span data-stu-id="92d98-177"><a name="CreateGateway"></a>6. Create hello VPN gateway</span></span>

<span data-ttu-id="92d98-178">Crie gateway de VPN de rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="92d98-178">Create hello virtual network VPN gateway.</span></span> <span data-ttu-id="92d98-179">Criar um gateway VPN pode demorar até too45 minutos ou mais toocomplete.</span><span class="sxs-lookup"><span data-stu-id="92d98-179">Creating a VPN gateway can take up too45 minutes or more toocomplete.</span></span>

<span data-ttu-id="92d98-180">Use Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="92d98-180">Use hello following values:</span></span>

* <span data-ttu-id="92d98-181">Olá *- GatewayType* para uma Site a Site configuração é *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="92d98-181">hello *-GatewayType* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="92d98-182">tipo de gateway Olá é sempre configuração toohello específico que você está implementando.</span><span class="sxs-lookup"><span data-stu-id="92d98-182">hello gateway type is always specific toohello configuration that you are implementing.</span></span> <span data-ttu-id="92d98-183">Por exemplo, outras configurações de gateway podem exigir -GatewayType ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="92d98-183">For example, other gateway configurations may require -GatewayType ExpressRoute.</span></span>
* <span data-ttu-id="92d98-184">Olá *- VpnType* pode ser *RouteBased* (conhecida tooas um Gateway dinâmico em alguns documentos), ou *PolicyBased* (chamado tooas um Gateway estático em alguns documentos ).</span><span class="sxs-lookup"><span data-stu-id="92d98-184">hello *-VpnType* can be *RouteBased* (referred tooas a Dynamic Gateway in some documentation), or *PolicyBased* (referred tooas a Static Gateway in some documentation).</span></span> <span data-ttu-id="92d98-185">Para saber mais sobre os tipos de gateway de VPN, veja [Sobre o Gateway de VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="92d98-185">For more information about VPN gateway types, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="92d98-186">Selecione Olá SKU de Gateway que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="92d98-186">Select hello Gateway SKU that you want toouse.</span></span> <span data-ttu-id="92d98-187">Há limitações de configuração para alguns SKUs.</span><span class="sxs-lookup"><span data-stu-id="92d98-187">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="92d98-188">Para obter mais informações, confira [SKUs de gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="92d98-188">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="92d98-189">Se você receber um erro ao criar o gateway VPN Olá sobre Olá - GatewaySku, verifique se você instalou a versão mais recente Olá Olá de cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="92d98-189">If you get an error when creating hello VPN gateway regarding hello -GatewaySku, verify that you have installed hello latest version of hello PowerShell cmdlets.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1 `
-Location 'East US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased -GatewaySku VpnGw1
```

## <span data-ttu-id="92d98-190"><a name="ConfigureVPNDevice"></a>7. Configurar o dispositivo de VPN</span><span class="sxs-lookup"><span data-stu-id="92d98-190"><a name="ConfigureVPNDevice"></a>7. Configure your VPN device</span></span>

<span data-ttu-id="92d98-191">Rede de local de tooan conexões site a Site requer um dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="92d98-191">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="92d98-192">Nesta etapa, você deve configurar seu dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="92d98-192">In this step, you configure your VPN device.</span></span> <span data-ttu-id="92d98-193">Ao configurar seu dispositivo VPN, você precisa seguir hello:</span><span class="sxs-lookup"><span data-stu-id="92d98-193">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="92d98-194">Uma chave compartilhada.</span><span class="sxs-lookup"><span data-stu-id="92d98-194">A shared key.</span></span> <span data-ttu-id="92d98-195">Isso é Olá mesmo chave que você especificar ao criar sua conexão VPN Site a Site.</span><span class="sxs-lookup"><span data-stu-id="92d98-195">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="92d98-196">Em nossos exemplos, usamos uma chave compartilhada básica.</span><span class="sxs-lookup"><span data-stu-id="92d98-196">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="92d98-197">É recomendável que você gerar um toouse chave mais complexa.</span><span class="sxs-lookup"><span data-stu-id="92d98-197">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="92d98-198">Olá endereço IP público do seu gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="92d98-198">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="92d98-199">Você pode exibir o endereço IP público de saudação usando Olá portal do Azure, PowerShell ou CLI.</span><span class="sxs-lookup"><span data-stu-id="92d98-199">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="92d98-200">Olá toofind endereço IP público do seu gateway de rede virtual usando o PowerShell, use Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="92d98-200">toofind hello Public IP address of your virtual network gateway using PowerShell, use hello following example:</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name GW1PublicIP -ResourceGroupName TestRG1
  ```

[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="92d98-201"><a name="CreateConnection"></a>8. Criar conexão de VPN Olá</span><span class="sxs-lookup"><span data-stu-id="92d98-201"><a name="CreateConnection"></a>8. Create hello VPN connection</span></span>

<span data-ttu-id="92d98-202">Em seguida, crie uma conexão de VPN Site a Site Olá entre o gateway de rede virtual e seu dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="92d98-202">Next, create hello Site-to-Site VPN connection between your virtual network gateway and your VPN device.</span></span> <span data-ttu-id="92d98-203">Ser valores de saudação tooreplace-se com seus próprios.</span><span class="sxs-lookup"><span data-stu-id="92d98-203">Be sure tooreplace hello values with your own.</span></span> <span data-ttu-id="92d98-204">chave compartilhada Olá deve corresponder o valor de saudação usado para a sua configuração de dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="92d98-204">hello shared key must match hello value you used for your VPN device configuration.</span></span> <span data-ttu-id="92d98-205">Observe que Olá '-ConnectionType' para o Site a Site é *IPsec*.</span><span class="sxs-lookup"><span data-stu-id="92d98-205">Notice that hello '-ConnectionType' for Site-to-Site is *IPsec*.</span></span>

1. <span data-ttu-id="92d98-206">Definir variáveis de saudação.</span><span class="sxs-lookup"><span data-stu-id="92d98-206">Set hello variables.</span></span>
  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1
  $local = Get-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1
  ```

2. <span data-ttu-id="92d98-207">Crie conexão hello.</span><span class="sxs-lookup"><span data-stu-id="92d98-207">Create hello connection.</span></span>
  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name VNet1toSite2 -ResourceGroupName TestRG1 `
  -Location 'East US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

<span data-ttu-id="92d98-208">Após um instante, Olá conexão será estabelecida.</span><span class="sxs-lookup"><span data-stu-id="92d98-208">After a short while, hello connection will be established.</span></span>

## <span data-ttu-id="92d98-209"><a name="toverify"></a>9. Verifique se a conexão de VPN Olá</span><span class="sxs-lookup"><span data-stu-id="92d98-209"><a name="toverify"></a>9. Verify hello VPN connection</span></span>

<span data-ttu-id="92d98-210">Há alguns tooverify de maneiras diferentes de sua conexão VPN.</span><span class="sxs-lookup"><span data-stu-id="92d98-210">There are a few different ways tooverify your VPN connection.</span></span>

[!INCLUDE [Verify connection](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="92d98-211"><a name="connectVM"></a>máquina de virtual tooa tooconnect</span><span class="sxs-lookup"><span data-stu-id="92d98-211"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]


## <span data-ttu-id="92d98-212"><a name="modify"></a>Modifique os prefixos do endereço IP para um gateway de rede local</span><span class="sxs-lookup"><span data-stu-id="92d98-212"><a name="modify"></a>Modify IP address prefixes for a local network gateway</span></span>

<span data-ttu-id="92d98-213">Se alterar de prefixos de endereço IP hello ser roteada tooyour local, você pode modificar o gateway de rede local hello.</span><span class="sxs-lookup"><span data-stu-id="92d98-213">If hello IP address prefixes that you want routed tooyour on-premises location change, you can modify hello local network gateway.</span></span> <span data-ttu-id="92d98-214">São fornecidos dois conjuntos de instruções.</span><span class="sxs-lookup"><span data-stu-id="92d98-214">Two sets of instructions are provided.</span></span> <span data-ttu-id="92d98-215">instruções de saudação que você escolher dependem se você já criou sua conexão de gateway.</span><span class="sxs-lookup"><span data-stu-id="92d98-215">hello instructions you choose depend on whether you have already created your gateway connection.</span></span>

[!INCLUDE [Modify prefixes](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="92d98-216"><a name="modifygwipaddress"></a>Modificar o endereço IP do gateway Olá para um gateway de rede local</span><span class="sxs-lookup"><span data-stu-id="92d98-216"><a name="modifygwipaddress"></a>Modify hello gateway IP address for a local network gateway</span></span>

[!INCLUDE [Modify gateway IP address](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="92d98-217">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="92d98-217">Next steps</span></span>

*  <span data-ttu-id="92d98-218">Quando a conexão for concluída, você pode adicionar máquinas virtuais tooyour as redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="92d98-218">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="92d98-219">Para saber mais, veja [Máquinas virtuais](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="92d98-219">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="92d98-220">Para obter informações sobre o BGP, consulte Olá [visão geral de BGP](vpn-gateway-bgp-overview.md) e [como tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="92d98-220">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
