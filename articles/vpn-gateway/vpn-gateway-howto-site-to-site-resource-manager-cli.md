---
title: 'Conecte-se a sua rede de local tooan rede virtual do Azure: VPN Site a Site: CLI | Microsoft Docs'
description: "Etapas toocreate uma conexão IPsec de seu local de rede tooan rede virtual do Azure sobre Olá Internet pública. Essas etapas o ajudarão a criar uma conexão de Gateway de VPN Site a Site entre locais usando a CLI."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: c652cf2caf3928cdeb19d7dc329f6db101e5ed90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-a-site-to-site-vpn-connection-using-cli"></a><span data-ttu-id="0b716-104">Criar uma rede virtual com uma conexão VPN Site a Site usando a CLI</span><span class="sxs-lookup"><span data-stu-id="0b716-104">Create a virtual network with a Site-to-Site VPN connection using CLI</span></span>

<span data-ttu-id="0b716-105">Este artigo mostra como toouse Olá CLI do Azure toocreate uma conexão de gateway VPN Site a Site de sua toohello de rede local VNet.</span><span class="sxs-lookup"><span data-stu-id="0b716-105">This article shows you how toouse hello Azure CLI toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="0b716-106">Olá etapas neste artigo se aplicam a modelo de implantação do Gerenciador de recursos de toohello.</span><span class="sxs-lookup"><span data-stu-id="0b716-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="0b716-107">Você também pode criar essa configuração usando uma ferramenta de implantação diferente ou um modelo de implantação, selecionando uma opção diferente de saudação lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="0b716-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span><br>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0b716-108">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0b716-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="0b716-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0b716-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="0b716-110">CLI</span><span class="sxs-lookup"><span data-stu-id="0b716-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="0b716-111">Portal do Azure (clássico)</span><span class="sxs-lookup"><span data-stu-id="0b716-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>


![Diagrama de conexão Site a Site de Gateway de VPN entre locais](./media/vpn-gateway-howto-site-to-site-resource-manager-cli/site-to-site-diagram.png)

<span data-ttu-id="0b716-113">Uma conexão de gateway VPN Site a Site é usado tooconnect seu local de rede tooan rede virtual do Azure por um túnel VPN IPsec/IKE (IKEv1 ou IKEv2).</span><span class="sxs-lookup"><span data-stu-id="0b716-113">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="0b716-114">Esse tipo de conexão exige um VPN de dispositivos localizado localmente que tenha uma tooit de endereço atribuído de IP público externamente.</span><span class="sxs-lookup"><span data-stu-id="0b716-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="0b716-115">Para saber mais sobre os gateways de VPN, veja [Sobre o gateway de VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="0b716-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0b716-116">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="0b716-116">Before you begin</span></span>

<span data-ttu-id="0b716-117">Verifique se você atendeu a saudação critérios a seguir antes de iniciar a configuração:</span><span class="sxs-lookup"><span data-stu-id="0b716-117">Verify that you have met hello following criteria before beginning configuration:</span></span>

* <span data-ttu-id="0b716-118">Verifique se você tem um dispositivo VPN compatível e alguém que é capaz de tooconfigure-lo.</span><span class="sxs-lookup"><span data-stu-id="0b716-118">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="0b716-119">Para obter mais informações sobre dispositivos VPN compatíveis e a configuração de dispositivo, confira [Sobre dispositivos VPN](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="0b716-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="0b716-120">Verifique se você possui um endereço IPv4 público voltado para o exterior para seu dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="0b716-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="0b716-121">Esse endereço IP não pode estar localizado atrás de um NAT.</span><span class="sxs-lookup"><span data-stu-id="0b716-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="0b716-122">Se você não estiver familiarizado com intervalos de endereços IP de saudação localizados na configuração de rede local, é necessário toocoordinate com alguém que possa fornecer os detalhes para você.</span><span class="sxs-lookup"><span data-stu-id="0b716-122">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="0b716-123">Quando você criar essa configuração, você deve especificar os prefixos de intervalo endereço IP hello Azure encaminhe tooyour no local.</span><span class="sxs-lookup"><span data-stu-id="0b716-123">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="0b716-124">Nenhuma das sub-redes Olá da sua rede local pode ser sobre colo com sub-redes de rede virtual Olá que você deseja tooconnect para.</span><span class="sxs-lookup"><span data-stu-id="0b716-124">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span>
* <span data-ttu-id="0b716-125">Verifique se você instalou a versão mais recente de comandos CLI hello (2.0 ou posteriores).</span><span class="sxs-lookup"><span data-stu-id="0b716-125">Verify that you have installed latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="0b716-126">Para obter informações sobre como instalar os comandos CLI hello, consulte [instalar o Azure CLI 2.0](/cli/azure/install-azure-cli) e [Introdução ao Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0b716-126">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

### <span data-ttu-id="0b716-127"><a name="example"></a>Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="0b716-127"><a name="example"></a>Example values</span></span>

<span data-ttu-id="0b716-128">Você pode usar o hello valores toocreate um ambiente de teste a seguir, ou consulte valores toothese toobetter entender exemplos Olá neste artigo:</span><span class="sxs-lookup"><span data-stu-id="0b716-128">You can use hello following values toocreate a test environment, or refer toothese values toobetter understand hello examples in this article:</span></span>

```
#Example values

VnetName                = TestVNet1 
ResourceGroup           = TestRG1 
Location                = eastus 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.0.0/24 
GatewaySubnet           = 10.11.255.0/27 
LocalNetworkGatewayName = Site2 
LNG Public IP           = <VPN device IP address>
LocalAddrPrefix1        = 10.0.0.0/24
LocalAddrPrefix2        = 20.0.0.0/24   
GatewayName             = VNet1GW 
PublicIP                = VNet1GWIP 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2
```

## <span data-ttu-id="0b716-129"><a name="Login"></a>1. Conecte-se a assinatura de tooyour</span><span class="sxs-lookup"><span data-stu-id="0b716-129"><a name="Login"></a>1. Connect tooyour subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="0b716-130"><a name="rg"></a>2. Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="0b716-130"><a name="rg"></a>2. Create a resource group</span></span>

<span data-ttu-id="0b716-131">Olá, exemplo a seguir cria um grupo de recursos denominado TestRG1 no local de 'eastus' hello.</span><span class="sxs-lookup"><span data-stu-id="0b716-131">hello following example creates a resource group named 'TestRG1' in hello 'eastus' location.</span></span> <span data-ttu-id="0b716-132">Se você já tiver um grupo de recursos na região de saudação que você deseja toocreate sua rede virtual, você pode usar um em vez disso.</span><span class="sxs-lookup"><span data-stu-id="0b716-132">If you already have a resource group in hello region that you want toocreate your VNet, you can use that one instead.</span></span>

```azurecli
az group create --name TestRG1 --location eastus
```

## <span data-ttu-id="0b716-133"><a name="VNet"></a>3. Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="0b716-133"><a name="VNet"></a>3. Create a virtual network</span></span>

<span data-ttu-id="0b716-134">Se você ainda não tiver uma rede virtual, crie um usando Olá [criar redes de rede az](/cli/azure/network/vnet#create) comando.</span><span class="sxs-lookup"><span data-stu-id="0b716-134">If you don't already have a virtual network, create one using hello [az network vnet create](/cli/azure/network/vnet#create) command.</span></span> <span data-ttu-id="0b716-135">Ao criar uma rede virtual, certifique-se de que os espaços de endereço Olá que você especificar não se sobrepõem a nenhum Olá dos espaços de endereço que você tem em sua rede local.</span><span class="sxs-lookup"><span data-stu-id="0b716-135">When creating a virtual network, make sure that hello address spaces you specify don't overlap any of hello address spaces that you have on your on-premises network.</span></span>

<span data-ttu-id="0b716-136">Olá, exemplo a seguir cria uma rede virtual denominada 'TestVNet1' e uma sub-rede, 'Subnet1'.</span><span class="sxs-lookup"><span data-stu-id="0b716-136">hello following example creates a virtual network named 'TestVNet1' and a subnet, 'Subnet1'.</span></span>

```azurecli
az network vnet create --name TestVNet1 --resource-group TestRG1 --address-prefix 10.11.0.0/16 --location eastus --subnet-name Subnet1 --subnet-prefix 10.11.0.0/24
```

## <span data-ttu-id="0b716-137">4. <a name="gwsub"></a>Criar uma sub-rede de gateway Olá</span><span class="sxs-lookup"><span data-stu-id="0b716-137">4. <a name="gwsub"></a>Create hello gateway subnet</span></span>

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="0b716-138">Para essa configuração, você também precisará de uma sub-rede de gateway.</span><span class="sxs-lookup"><span data-stu-id="0b716-138">For this configuration, you also need a gateway subnet.</span></span> <span data-ttu-id="0b716-139">gateway de rede virtual Olá usa uma sub-rede de gateway que contém endereços IP de saudação que são usados pelos serviços de gateway VPN hello.</span><span class="sxs-lookup"><span data-stu-id="0b716-139">hello virtual network gateway uses a gateway subnet that contains hello IP addresses that are used by hello VPN gateway services.</span></span> <span data-ttu-id="0b716-140">Quando você cria uma sub-rede de gateway, ela deve ser nomeada como 'GatewaySubnet'.</span><span class="sxs-lookup"><span data-stu-id="0b716-140">When you create a gateway subnet, it must be named 'GatewaySubnet'.</span></span> <span data-ttu-id="0b716-141">Se usar outro nome, você criará uma sub-rede, mas o Azure não a tratará como uma sub-rede de gateway.</span><span class="sxs-lookup"><span data-stu-id="0b716-141">If you name it something else, you create a subnet, but Azure won't treat it as a gateway subnet.</span></span>

<span data-ttu-id="0b716-142">tamanho de saudação da sub-rede de gateway de saudação que você especificar depende da configuração de gateway VPN Olá que você deseja toocreate.</span><span class="sxs-lookup"><span data-stu-id="0b716-142">hello size of hello gateway subnet that you specify depends on hello VPN gateway configuration that you want toocreate.</span></span> <span data-ttu-id="0b716-143">Embora seja possível toocreate tão pequenas quanto /29 uma sub-rede do gateway, é recomendável que você crie uma sub-rede maior que inclui mais endereços selecionando /27 ou /28.</span><span class="sxs-lookup"><span data-stu-id="0b716-143">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting /27 or /28.</span></span> <span data-ttu-id="0b716-144">Usar uma sub-rede do gateway maior permite suficiente IP endereços tooaccommodate futuras configurações possíveis.</span><span class="sxs-lookup"><span data-stu-id="0b716-144">Using a larger gateway subnet allows for enough IP addresses tooaccommodate possible future configurations.</span></span>

<span data-ttu-id="0b716-145">Saudação de uso [criar sub-rede de rede virtual de rede az](/cli/azure/network/vnet/subnet#create) sub-rede de gateway do comando toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="0b716-145">Use hello [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command toocreate hello gateway subnet.</span></span>

```azurecli
az network vnet subnet create --address-prefix 10.11.255.0/27 --name GatewaySubnet --resource-group TestRG1 --vnet-name TestVNet1
```

## <span data-ttu-id="0b716-146"><a name="localnet"></a>5. Criar gateway de rede local Olá</span><span class="sxs-lookup"><span data-stu-id="0b716-146"><a name="localnet"></a>5. Create hello local network gateway</span></span>

<span data-ttu-id="0b716-147">Normalmente, o gateway de rede local Olá refere-se tooyour no local.</span><span class="sxs-lookup"><span data-stu-id="0b716-147">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="0b716-148">Atribuir o site Olá um nome pelo qual Azure pode consulte tooit e especifique o endereço IP de saudação do hello toowhich de dispositivo VPN de local, você criará uma conexão.</span><span class="sxs-lookup"><span data-stu-id="0b716-148">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="0b716-149">Você também pode especificar prefixos de endereço IP de saudação que serão encaminhados através do dispositivo de VPN toohello do gateway VPN hello.</span><span class="sxs-lookup"><span data-stu-id="0b716-149">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="0b716-150">especificar os prefixos de endereço Olá são prefixos Olá localizados em sua rede local.</span><span class="sxs-lookup"><span data-stu-id="0b716-150">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="0b716-151">Se sua rede local for alterada, você pode atualizar facilmente prefixos hello.</span><span class="sxs-lookup"><span data-stu-id="0b716-151">If your on-premises network changes, you can easily update hello prefixes.</span></span>

<span data-ttu-id="0b716-152">Use Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="0b716-152">Use hello following values:</span></span>

* <span data-ttu-id="0b716-153">Olá *– endereço ip de gateway* é o endereço IP de saudação do seu dispositivo VPN local.</span><span class="sxs-lookup"><span data-stu-id="0b716-153">hello *--gateway-ip-address* is hello IP address of your on-premises VPN device.</span></span> <span data-ttu-id="0b716-154">O dispositivo VPN não pode estar localizado atrás de um NAT.</span><span class="sxs-lookup"><span data-stu-id="0b716-154">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="0b716-155">Olá *– prefixos de endereço local* é espaços de endereço de seu local.</span><span class="sxs-lookup"><span data-stu-id="0b716-155">hello *--local-address-prefixes* are your on-premises address spaces.</span></span>

<span data-ttu-id="0b716-156">Saudação de uso [criar local de rede az gateway](/cli/azure/network/local-gateway#create) comando tooadd um gateway de rede local com vários prefixos de endereço:</span><span class="sxs-lookup"><span data-stu-id="0b716-156">Use hello [az network local-gateway create](/cli/azure/network/local-gateway#create) command tooadd a local network gateway with multiple address prefixes:</span></span>

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --resource-group TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

## <span data-ttu-id="0b716-157"><a name="PublicIP"></a>6. Solicite um endereço IP público</span><span class="sxs-lookup"><span data-stu-id="0b716-157"><a name="PublicIP"></a>6. Request a Public IP address</span></span>

<span data-ttu-id="0b716-158">Um gateway de VPN deve ter um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="0b716-158">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="0b716-159">Você primeiro solicitar o recurso de endereço IP hello e, em seguida, consulte tooit ao criar o gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="0b716-159">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="0b716-160">endereço IP de saudação é atribuído dinamicamente recursos toohello ao gateway de VPN Olá é criado.</span><span class="sxs-lookup"><span data-stu-id="0b716-160">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="0b716-161">O gateway de VPN atualmente suporta apenas alocação de endereços IP público *Dinâmico*.</span><span class="sxs-lookup"><span data-stu-id="0b716-161">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="0b716-162">Você não pode solicitar uma atribuição de endereço IP Público Estático.</span><span class="sxs-lookup"><span data-stu-id="0b716-162">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="0b716-163">No entanto, isso não significa que o endereço IP de saudação alterado depois que ele foi atribuído tooyour gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="0b716-163">However, this does not mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="0b716-164">somente tempo de saudação alterações de endereço IP público hello quando é Olá gateway é excluído e criado novamente.</span><span class="sxs-lookup"><span data-stu-id="0b716-164">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="0b716-165">Isso não altera o redimensionamento, a redefinição ou outras manutenções/atualizações internas do seu gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="0b716-165">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="0b716-166">Saudação de uso [criar az rede ip público](/cli/azure/network/public-ip#create) comando toorequest um endereço IP público dinâmico.</span><span class="sxs-lookup"><span data-stu-id="0b716-166">Use hello [az network public-ip create](/cli/azure/network/public-ip#create) command toorequest a Dynamic Public IP address.</span></span>

```azurecli
az network public-ip create --name VNet1GWIP --resource-group TestRG1 --allocation-method Dynamic
```

## <span data-ttu-id="0b716-167"><a name="CreateGateway"></a>7. Criar gateway VPN Olá</span><span class="sxs-lookup"><span data-stu-id="0b716-167"><a name="CreateGateway"></a>7. Create hello VPN gateway</span></span>

<span data-ttu-id="0b716-168">Crie gateway de VPN de rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="0b716-168">Create hello virtual network VPN gateway.</span></span> <span data-ttu-id="0b716-169">Criar um gateway VPN pode demorar até too45 minutos ou mais toocomplete.</span><span class="sxs-lookup"><span data-stu-id="0b716-169">Creating a VPN gateway can take up too45 minutes or more toocomplete.</span></span>

<span data-ttu-id="0b716-170">Use Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="0b716-170">Use hello following values:</span></span>

* <span data-ttu-id="0b716-171">Olá *– tipo de gateway* para uma Site a Site configuração é *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="0b716-171">hello *--gateway-type* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="0b716-172">tipo de gateway Olá é sempre configuração toohello específico que você está implementando.</span><span class="sxs-lookup"><span data-stu-id="0b716-172">hello gateway type is always specific toohello configuration that you are implementing.</span></span> <span data-ttu-id="0b716-173">Para obter mais informações, consulte [Tipos de gateway](vpn-gateway-about-vpn-gateway-settings.md#gwtype).</span><span class="sxs-lookup"><span data-stu-id="0b716-173">For more information, see [Gateway types](vpn-gateway-about-vpn-gateway-settings.md#gwtype).</span></span>
* <span data-ttu-id="0b716-174">Olá *- vpn-tipo* pode ser *RouteBased* (conhecida tooas um Gateway dinâmico em alguns documentos), ou *PolicyBased* (chamado tooas um Gateway estático em alguns documentação).</span><span class="sxs-lookup"><span data-stu-id="0b716-174">hello *--vpn-type* can be *RouteBased* (referred tooas a Dynamic Gateway in some documentation), or *PolicyBased* (referred tooas a Static Gateway in some documentation).</span></span> <span data-ttu-id="0b716-175">configuração de saudação é toorequirements específico de dispositivo de saudação que você está se conectando.</span><span class="sxs-lookup"><span data-stu-id="0b716-175">hello setting is specific toorequirements of hello device that you are connecting to.</span></span> <span data-ttu-id="0b716-176">Para obter mais informações sobre tipos de gateway de VPN, confira [Sobre definições de configuração de gateway de VPN](vpn-gateway-about-vpn-gateway-settings.md#vpntype).</span><span class="sxs-lookup"><span data-stu-id="0b716-176">For more information about VPN gateway types, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md#vpntype).</span></span>
* <span data-ttu-id="0b716-177">Selecione Olá SKU de Gateway que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="0b716-177">Select hello Gateway SKU that you want toouse.</span></span> <span data-ttu-id="0b716-178">Há limitações de configuração para alguns SKUs.</span><span class="sxs-lookup"><span data-stu-id="0b716-178">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="0b716-179">Para obter mais informações, confira [SKUs de gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="0b716-179">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

<span data-ttu-id="0b716-180">Criar gateway VPN hello usando Olá [criar gateway de rede virtual az rede](/cli/azure/network/vnet-gateway#create) comando.</span><span class="sxs-lookup"><span data-stu-id="0b716-180">Create hello VPN gateway using hello [az network vnet-gateway create](/cli/azure/network/vnet-gateway#create) command.</span></span> <span data-ttu-id="0b716-181">Se você executar esse comando hello usando o parâmetro '-- Nenhum - wait', você não vir quaisquer comentários ou saída.</span><span class="sxs-lookup"><span data-stu-id="0b716-181">If you run this command using hello '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="0b716-182">Esse parâmetro permite Olá gateway toocreate no plano de fundo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b716-182">This parameter allows hello gateway toocreate in hello background.</span></span> <span data-ttu-id="0b716-183">Leva aproximadamente 45 minutos toocreate um gateway.</span><span class="sxs-lookup"><span data-stu-id="0b716-183">It takes around 45 minutes toocreate a gateway.</span></span>

```azurecli
az network vnet-gateway create --name VNet1GW --public-ip-address VNet1GWIP --resource-group TestRG1 --vnet TestVNet1 --gateway-type Vpn --vpn-type RouteBased --sku VpnGw1 --no-wait 
```

## <span data-ttu-id="0b716-184"><a name="VPNDevice"></a>8. Configurar o dispositivo de VPN</span><span class="sxs-lookup"><span data-stu-id="0b716-184"><a name="VPNDevice"></a>8. Configure your VPN device</span></span>

<span data-ttu-id="0b716-185">Rede de local de tooan conexões site a Site requer um dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="0b716-185">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="0b716-186">Nesta etapa, você deve configurar seu dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="0b716-186">In this step, you configure your VPN device.</span></span> <span data-ttu-id="0b716-187">Ao configurar seu dispositivo VPN, você precisa seguir hello:</span><span class="sxs-lookup"><span data-stu-id="0b716-187">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="0b716-188">Uma chave compartilhada.</span><span class="sxs-lookup"><span data-stu-id="0b716-188">A shared key.</span></span> <span data-ttu-id="0b716-189">Isso é Olá mesmo chave que você especificar ao criar sua conexão VPN Site a Site.</span><span class="sxs-lookup"><span data-stu-id="0b716-189">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="0b716-190">Em nossos exemplos, usamos uma chave compartilhada básica.</span><span class="sxs-lookup"><span data-stu-id="0b716-190">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="0b716-191">É recomendável que você gerar um toouse chave mais complexa.</span><span class="sxs-lookup"><span data-stu-id="0b716-191">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="0b716-192">Olá endereço IP público do seu gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="0b716-192">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="0b716-193">Você pode exibir o endereço IP público de saudação usando Olá portal do Azure, PowerShell ou CLI.</span><span class="sxs-lookup"><span data-stu-id="0b716-193">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="0b716-194">toofind Olá endereço IP público do seu gateway de rede virtual, use Olá [lista de ip público de rede az](/cli/azure/network/public-ip#list) comando.</span><span class="sxs-lookup"><span data-stu-id="0b716-194">toofind hello public IP address of your virtual network gateway, use hello [az network public-ip list](/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="0b716-195">Para facilitar a leitura, a saída de hello é formatado toodisplay lista de saudação de IPs públicos em formato de tabela.</span><span class="sxs-lookup"><span data-stu-id="0b716-195">For easy reading, hello output is formatted toodisplay hello list of public IPs in table format.</span></span>

  ```azurecli
  az network public-ip list --resource-group TestRG1 --output table
  ```


[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="0b716-196"><a name="CreateConnection"></a>9. Criar conexão de VPN Olá</span><span class="sxs-lookup"><span data-stu-id="0b716-196"><a name="CreateConnection"></a>9. Create hello VPN connection</span></span>

<span data-ttu-id="0b716-197">Crie conexão de VPN Olá Site a Site entre o gateway de rede virtual e seu dispositivo VPN local.</span><span class="sxs-lookup"><span data-stu-id="0b716-197">Create hello Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span> <span data-ttu-id="0b716-198">Preste atenção especial toohello compartilhado valor de chave, que deve corresponder ao Olá configurado compartilhado valor de chave para seu dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="0b716-198">Pay particular attention toohello shared key value, which must match hello configured shared key value for your VPN device.</span></span>

<span data-ttu-id="0b716-199">Criar conexão hello usando Olá [criar vpn-conexão de rede de az](/cli/azure/network/vpn-connection#create) comando.</span><span class="sxs-lookup"><span data-stu-id="0b716-199">Create hello connection using hello [az network vpn-connection create](/cli/azure/network/vpn-connection#create) command.</span></span>

```azurecli
az network vpn-connection create --name VNet1toSite2 -resource-group TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key abc123 --local-gateway2 Site2
```

<span data-ttu-id="0b716-200">Após um instante, Olá conexão será estabelecida.</span><span class="sxs-lookup"><span data-stu-id="0b716-200">After a short while, hello connection will be established.</span></span>

## <span data-ttu-id="0b716-201"><a name="toverify"></a>10. Verifique se a conexão de VPN Olá</span><span class="sxs-lookup"><span data-stu-id="0b716-201"><a name="toverify"></a>10. Verify hello VPN connection</span></span>

[!INCLUDE [verify connection](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

<span data-ttu-id="0b716-202">Se você quiser toouse tooverify de outro método sua conexão, consulte [verificar uma conexão de Gateway VPN](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="0b716-202">If you want toouse another method tooverify your connection, see [Verify a VPN Gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

## <span data-ttu-id="0b716-203"><a name="connectVM"></a>máquina de virtual tooa tooconnect</span><span class="sxs-lookup"><span data-stu-id="0b716-203"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="0b716-204"><a name="tasks"></a>Tarefas comuns</span><span class="sxs-lookup"><span data-stu-id="0b716-204"><a name="tasks"></a>Common tasks</span></span>

<span data-ttu-id="0b716-205">Esta seção contém os comandos comuns que são úteis ao trabalhar com configurações de site a site.</span><span class="sxs-lookup"><span data-stu-id="0b716-205">This section contains common commands that are helpful when working with site-to-site configurations.</span></span> <span data-ttu-id="0b716-206">Para Olá a lista completa de comandos de rede, consulte [CLI do Azure - rede](/cli/azure/network).</span><span class="sxs-lookup"><span data-stu-id="0b716-206">For hello full list of CLI networking commands, see [Azure CLI - Networking](/cli/azure/network).</span></span>

[!INCLUDE [local network gateway common tasks](../../includes/vpn-gateway-common-tasks-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="0b716-207">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0b716-207">Next steps</span></span>

* <span data-ttu-id="0b716-208">Quando a conexão for concluída, você pode adicionar máquinas virtuais tooyour as redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="0b716-208">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="0b716-209">Para saber mais, veja [Máquinas virtuais](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="0b716-209">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="0b716-210">Para obter informações sobre o BGP, consulte Olá [visão geral de BGP](vpn-gateway-bgp-overview.md) e [como tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="0b716-210">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="0b716-211">Para saber mais sobre Túneis Forçados, confira [Sobre o Túnel Forçado](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="0b716-211">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="0b716-212">Para obter informações sobre Conexões Altamente Disponíveis Ativo-Ativo, consulte [Conectividade Altamente Disponível entre locais e Rede Virtual para Rede Virtual](vpn-gateway-highlyavailable.md).</span><span class="sxs-lookup"><span data-stu-id="0b716-212">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
* <span data-ttu-id="0b716-213">Para obter uma lista de comandos da CLI do Azure de rede, confira [CLI do Azure](https://docs.microsoft.com/cli/azure/network).</span><span class="sxs-lookup"><span data-stu-id="0b716-213">For a list of networking Azure CLI commands, see [Azure CLI](https://docs.microsoft.com/cli/azure/network).</span></span>