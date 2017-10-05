---
title: 'Conectar sua rede local a uma rede virtual do Azure: VPN Site a Site: CLI | Microsoft Docs'
description: "Etapas para criar uma conexão IPsec de sua rede local para uma rede virtual do Azure pela Internet pública. Essas etapas o ajudarão a criar uma conexão de Gateway de VPN Site a Site entre locais usando a CLI."
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
ms.openlocfilehash: 019c5421dc470b18c9087417b93c241cc5730f77
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-virtual-network-with-a-site-to-site-vpn-connection-using-cli"></a><span data-ttu-id="fbf18-104">Criar uma rede virtual com uma conexão VPN Site a Site usando a CLI</span><span class="sxs-lookup"><span data-stu-id="fbf18-104">Create a virtual network with a Site-to-Site VPN connection using CLI</span></span>

<span data-ttu-id="fbf18-105">Este artigo mostra como usar a CLI do Azure para criar uma conexão de gateway de VPN Site a Site de sua rede local para a rede virtual.</span><span class="sxs-lookup"><span data-stu-id="fbf18-105">This article shows you how to use the Azure CLI to create a Site-to-Site VPN gateway connection from your on-premises network to the VNet.</span></span> <span data-ttu-id="fbf18-106">As etapas neste artigo se aplicam ao modelo de implantação do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fbf18-106">The steps in this article apply to the Resource Manager deployment model.</span></span> <span data-ttu-id="fbf18-107">Você também pode criar essa configuração usando uma ferramenta de implantação ou um modelo de implantação diferente, selecionando uma opção diferente na lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="fbf18-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span><br>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fbf18-108">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="fbf18-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="fbf18-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fbf18-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="fbf18-110">CLI</span><span class="sxs-lookup"><span data-stu-id="fbf18-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="fbf18-111">Portal do Azure (clássico)</span><span class="sxs-lookup"><span data-stu-id="fbf18-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>


![Diagrama de conexão Site a Site de Gateway de VPN entre locais](./media/vpn-gateway-howto-site-to-site-resource-manager-cli/site-to-site-diagram.png)

<span data-ttu-id="fbf18-113">Uma conexão de gateway de VPN Site a Site é usada para conectar a rede local a uma rede virtual do Azure por um túnel VPN IPsec/IKE (IKEv1 ou IKEv2).</span><span class="sxs-lookup"><span data-stu-id="fbf18-113">A Site-to-Site VPN gateway connection is used to connect your on-premises network to an Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="fbf18-114">Esse tipo de conexão exige um dispositivo VPN localizado no local que tenha um endereço IP público voltado para o exterior atribuído a ele.</span><span class="sxs-lookup"><span data-stu-id="fbf18-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned to it.</span></span> <span data-ttu-id="fbf18-115">Para saber mais sobre os gateways de VPN, veja [Sobre o gateway de VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="fbf18-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="fbf18-116">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="fbf18-116">Before you begin</span></span>

<span data-ttu-id="fbf18-117">Verifique se você atende aos seguintes critérios antes de iniciar a configuração:</span><span class="sxs-lookup"><span data-stu-id="fbf18-117">Verify that you have met the following criteria before beginning configuration:</span></span>

* <span data-ttu-id="fbf18-118">Verifique se você possui um dispositivo VPN compatível e alguém que possa configurá-lo.</span><span class="sxs-lookup"><span data-stu-id="fbf18-118">Make sure you have a compatible VPN device and someone who is able to configure it.</span></span> <span data-ttu-id="fbf18-119">Para obter mais informações sobre dispositivos VPN compatíveis e a configuração de dispositivo, confira [Sobre dispositivos VPN](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="fbf18-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="fbf18-120">Verifique se você possui um endereço IPv4 público voltado para o exterior para seu dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="fbf18-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="fbf18-121">Esse endereço IP não pode estar localizado atrás de um NAT.</span><span class="sxs-lookup"><span data-stu-id="fbf18-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="fbf18-122">Se não estiver familiarizado com os intervalos de endereços IP localizados na configuração de rede local, você precisará trabalhar em conjunto com alguém que possa lhe fornecer os detalhes.</span><span class="sxs-lookup"><span data-stu-id="fbf18-122">If you are unfamiliar with the IP address ranges located in your on-premises network configuration, you need to coordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="fbf18-123">Ao criar essa configuração, você deve especificar os prefixos de intervalo de endereços IP que o Azure roteará para seu local.</span><span class="sxs-lookup"><span data-stu-id="fbf18-123">When you create this configuration, you must specify the IP address range prefixes that Azure will route to your on-premises location.</span></span> <span data-ttu-id="fbf18-124">Nenhuma das sub-redes da rede local podem se sobrepor às sub-redes de rede virtual às quais você deseja se conectar.</span><span class="sxs-lookup"><span data-stu-id="fbf18-124">None of the subnets of your on-premises network can over lap with the virtual network subnets that you want to connect to.</span></span>
* <span data-ttu-id="fbf18-125">Instale a versão mais recente dos comandos da CLI (2.0 ou posterior).</span><span class="sxs-lookup"><span data-stu-id="fbf18-125">Verify that you have installed latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="fbf18-126">Para saber mais sobre como instalar os comandos da CLI, consulte [Instalar a CLI do Azure 2.0](/cli/azure/install-azure-cli) e [Introdução à CLI do Azure 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fbf18-126">For information about installing the CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

### <span data-ttu-id="fbf18-127"><a name="example"></a>Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="fbf18-127"><a name="example"></a>Example values</span></span>

<span data-ttu-id="fbf18-128">Você pode usar os seguintes valores para criar um ambiente de teste ou fazer referência a esses valores para entender melhor os exemplos neste artigo:</span><span class="sxs-lookup"><span data-stu-id="fbf18-128">You can use the following values to create a test environment, or refer to these values to better understand the examples in this article:</span></span>

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

## <span data-ttu-id="fbf18-129"><a name="Login"></a>1. Conecte-se as suas assinaturas</span><span class="sxs-lookup"><span data-stu-id="fbf18-129"><a name="Login"></a>1. Connect to your subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="fbf18-130"><a name="rg"></a>2. Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="fbf18-130"><a name="rg"></a>2. Create a resource group</span></span>

<span data-ttu-id="fbf18-131">O exemplo a seguir cria um grupo de recursos denominado 'TestRG1' no local 'eastus'.</span><span class="sxs-lookup"><span data-stu-id="fbf18-131">The following example creates a resource group named 'TestRG1' in the 'eastus' location.</span></span> <span data-ttu-id="fbf18-132">Se já tiver um grupo de recursos na região em que deseja criar a rede virtual, você poderá usá-lo.</span><span class="sxs-lookup"><span data-stu-id="fbf18-132">If you already have a resource group in the region that you want to create your VNet, you can use that one instead.</span></span>

```azurecli
az group create --name TestRG1 --location eastus
```

## <span data-ttu-id="fbf18-133"><a name="VNet"></a>3. Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="fbf18-133"><a name="VNet"></a>3. Create a virtual network</span></span>

<span data-ttu-id="fbf18-134">Se você ainda não tiver uma rede virtual, crie uma usando o comando [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="fbf18-134">If you don't already have a virtual network, create one using the [az network vnet create](/cli/azure/network/vnet#create) command.</span></span> <span data-ttu-id="fbf18-135">Ao criar uma rede virtual, certifique-se de que os espaços de endereço que você especificar não se sobreponham nenhum espaço de endereço que você tenha na rede local.</span><span class="sxs-lookup"><span data-stu-id="fbf18-135">When creating a virtual network, make sure that the address spaces you specify don't overlap any of the address spaces that you have on your on-premises network.</span></span>

<span data-ttu-id="fbf18-136">O exemplo a seguir cria uma rede virtual chamada 'TestVNet1' e uma sub-rede 'Subrede 1'.</span><span class="sxs-lookup"><span data-stu-id="fbf18-136">The following example creates a virtual network named 'TestVNet1' and a subnet, 'Subnet1'.</span></span>

```azurecli
az network vnet create --name TestVNet1 --resource-group TestRG1 --address-prefix 10.11.0.0/16 --location eastus --subnet-name Subnet1 --subnet-prefix 10.11.0.0/24
```

## <span data-ttu-id="fbf18-137">4. <a name="gwsub"></a>Criar a sub-rede de gateway</span><span class="sxs-lookup"><span data-stu-id="fbf18-137">4. <a name="gwsub"></a>Create the gateway subnet</span></span>

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="fbf18-138">Para essa configuração, você também precisará de uma sub-rede de gateway.</span><span class="sxs-lookup"><span data-stu-id="fbf18-138">For this configuration, you also need a gateway subnet.</span></span> <span data-ttu-id="fbf18-139">O gateway de rede virtual usa uma sub-rede de gateway que contém os endereços IP que são usados pelos serviços de gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="fbf18-139">The virtual network gateway uses a gateway subnet that contains the IP addresses that are used by the VPN gateway services.</span></span> <span data-ttu-id="fbf18-140">Quando você cria uma sub-rede de gateway, ela deve ser nomeada como 'GatewaySubnet'.</span><span class="sxs-lookup"><span data-stu-id="fbf18-140">When you create a gateway subnet, it must be named 'GatewaySubnet'.</span></span> <span data-ttu-id="fbf18-141">Se usar outro nome, você criará uma sub-rede, mas o Azure não a tratará como uma sub-rede de gateway.</span><span class="sxs-lookup"><span data-stu-id="fbf18-141">If you name it something else, you create a subnet, but Azure won't treat it as a gateway subnet.</span></span>

<span data-ttu-id="fbf18-142">O tamanho da sub-rede de gateway que você especifica depende da configuração do gateway de VPN que deseja criar.</span><span class="sxs-lookup"><span data-stu-id="fbf18-142">The size of the gateway subnet that you specify depends on the VPN gateway configuration that you want to create.</span></span> <span data-ttu-id="fbf18-143">Embora seja possível criar uma sub-rede de gateway tão pequena quanto /29, recomendamos que você crie uma sub-rede maior que inclua mais endereços selecionando /27 ou /28.</span><span class="sxs-lookup"><span data-stu-id="fbf18-143">While it is possible to create a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting /27 or /28.</span></span> <span data-ttu-id="fbf18-144">Usar uma sub-rede de gateway maior permite endereços IP suficientes para acomodar as possíveis configurações futuras.</span><span class="sxs-lookup"><span data-stu-id="fbf18-144">Using a larger gateway subnet allows for enough IP addresses to accommodate possible future configurations.</span></span>

<span data-ttu-id="fbf18-145">Execute o comando [azure network vnet subnet create](/cli/azure/network/vnet/subnet#create) para criar uma sub-rede de gateway.</span><span class="sxs-lookup"><span data-stu-id="fbf18-145">Use the [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command to create the gateway subnet.</span></span>

```azurecli
az network vnet subnet create --address-prefix 10.11.255.0/27 --name GatewaySubnet --resource-group TestRG1 --vnet-name TestVNet1
```

## <span data-ttu-id="fbf18-146"><a name="localnet"></a>5. Criar o gateway de rede local</span><span class="sxs-lookup"><span data-stu-id="fbf18-146"><a name="localnet"></a>5. Create the local network gateway</span></span>

<span data-ttu-id="fbf18-147">O gateway de rede local geralmente se refere ao seu local.</span><span class="sxs-lookup"><span data-stu-id="fbf18-147">The local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="fbf18-148">Você atribui um nome ao site pelo qual o Azure pode fazer referência a ele e especifica o endereço IP do dispositivo VPN local para o qual você criará uma conexão.</span><span class="sxs-lookup"><span data-stu-id="fbf18-148">You give the site a name by which Azure can refer to it, then specify the IP address of the on-premises VPN device to which you will create a connection.</span></span> <span data-ttu-id="fbf18-149">Você também pode especificar os prefixos de endereço IP que serão roteados por meio do gateway de VPN para o dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="fbf18-149">You also specify the IP address prefixes that will be routed through the VPN gateway to the VPN device.</span></span> <span data-ttu-id="fbf18-150">Os prefixos de endereço que você especifica são os prefixos localizados em sua rede local.</span><span class="sxs-lookup"><span data-stu-id="fbf18-150">The address prefixes you specify are the prefixes located on your on-premises network.</span></span> <span data-ttu-id="fbf18-151">Se sua rede local for alterada, você poderá atualizar facilmente os prefixos.</span><span class="sxs-lookup"><span data-stu-id="fbf18-151">If your on-premises network changes, you can easily update the prefixes.</span></span>

<span data-ttu-id="fbf18-152">Use os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="fbf18-152">Use the following values:</span></span>

* <span data-ttu-id="fbf18-153">O *--gateway-ip-address* é o endereço IP do dispositivo VPN local.</span><span class="sxs-lookup"><span data-stu-id="fbf18-153">The *--gateway-ip-address* is the IP address of your on-premises VPN device.</span></span> <span data-ttu-id="fbf18-154">O dispositivo VPN não pode estar localizado atrás de um NAT.</span><span class="sxs-lookup"><span data-stu-id="fbf18-154">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="fbf18-155">Os *--local-address-prefixes* são seus espaços de endereços locais.</span><span class="sxs-lookup"><span data-stu-id="fbf18-155">The *--local-address-prefixes* are your on-premises address spaces.</span></span>

<span data-ttu-id="fbf18-156">Use o comando [az network local-gateway create](/cli/azure/network/local-gateway#create) para adicionar um gateway de rede local com vários prefixos de endereço:</span><span class="sxs-lookup"><span data-stu-id="fbf18-156">Use the [az network local-gateway create](/cli/azure/network/local-gateway#create) command to add a local network gateway with multiple address prefixes:</span></span>

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --resource-group TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

## <span data-ttu-id="fbf18-157"><a name="PublicIP"></a>6. Solicite um endereço IP público</span><span class="sxs-lookup"><span data-stu-id="fbf18-157"><a name="PublicIP"></a>6. Request a Public IP address</span></span>

<span data-ttu-id="fbf18-158">Um gateway de VPN deve ter um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="fbf18-158">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="fbf18-159">Você primeiro solicita o recurso de endereço IP e, em seguida, faz referência a ele ao criar seu gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="fbf18-159">You first request the IP address resource, and then refer to it when creating your virtual network gateway.</span></span> <span data-ttu-id="fbf18-160">O endereço IP é atribuído dinamicamente ao recurso quando o gateway de VPN é criado.</span><span class="sxs-lookup"><span data-stu-id="fbf18-160">The IP address is dynamically assigned to the resource when the VPN gateway is created.</span></span> <span data-ttu-id="fbf18-161">O gateway de VPN atualmente suporta apenas alocação de endereços IP público *Dinâmico*.</span><span class="sxs-lookup"><span data-stu-id="fbf18-161">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="fbf18-162">Você não pode solicitar uma atribuição de endereço IP Público Estático.</span><span class="sxs-lookup"><span data-stu-id="fbf18-162">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="fbf18-163">No entanto, isso não significa que o endereço IP é alterado depois que ele foi atribuído ao seu gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="fbf18-163">However, this does not mean that the IP address changes after it has been assigned to your VPN gateway.</span></span> <span data-ttu-id="fbf18-164">A única vez em que o endereço IP Público é alterado é quando o gateway é excluído e recriado.</span><span class="sxs-lookup"><span data-stu-id="fbf18-164">The only time the Public IP address changes is when the gateway is deleted and re-created.</span></span> <span data-ttu-id="fbf18-165">Isso não altera o redimensionamento, a redefinição ou outras manutenções/atualizações internas do seu gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="fbf18-165">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="fbf18-166">Use o comando [az network public-ip create](/cli/azure/network/public-ip#create) para solicitar um endereço IP público dinâmico.</span><span class="sxs-lookup"><span data-stu-id="fbf18-166">Use the [az network public-ip create](/cli/azure/network/public-ip#create) command to request a Dynamic Public IP address.</span></span>

```azurecli
az network public-ip create --name VNet1GWIP --resource-group TestRG1 --allocation-method Dynamic
```

## <span data-ttu-id="fbf18-167"><a name="CreateGateway"></a>7. Criar o gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="fbf18-167"><a name="CreateGateway"></a>7. Create the VPN gateway</span></span>

<span data-ttu-id="fbf18-168">Crie o gateway de VPN da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="fbf18-168">Create the virtual network VPN gateway.</span></span> <span data-ttu-id="fbf18-169">A criação de um gateway de VPN pode demorar até 45 minutos ou mais para ser concluída.</span><span class="sxs-lookup"><span data-stu-id="fbf18-169">Creating a VPN gateway can take up to 45 minutes or more to complete.</span></span>

<span data-ttu-id="fbf18-170">Use os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="fbf18-170">Use the following values:</span></span>

* <span data-ttu-id="fbf18-171">O *--gateway-type* para uma configuração Site a Site é *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="fbf18-171">The *--gateway-type* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="fbf18-172">O tipo de gateway é sempre específico para a configuração que você está implementando.</span><span class="sxs-lookup"><span data-stu-id="fbf18-172">The gateway type is always specific to the configuration that you are implementing.</span></span> <span data-ttu-id="fbf18-173">Para obter mais informações, consulte [Tipos de gateway](vpn-gateway-about-vpn-gateway-settings.md#gwtype).</span><span class="sxs-lookup"><span data-stu-id="fbf18-173">For more information, see [Gateway types](vpn-gateway-about-vpn-gateway-settings.md#gwtype).</span></span>
* <span data-ttu-id="fbf18-174">O *--vpn-type* pode ser *RouteBased* (referido como Gateway Dinâmico em alguns documentos) ou *PolicyBased* (referido como Gateway Estático em alguns documentos).</span><span class="sxs-lookup"><span data-stu-id="fbf18-174">The *--vpn-type* can be *RouteBased* (referred to as a Dynamic Gateway in some documentation), or *PolicyBased* (referred to as a Static Gateway in some documentation).</span></span> <span data-ttu-id="fbf18-175">A configuração é específica para os requisitos do dispositivo ao qual você está se conectando.</span><span class="sxs-lookup"><span data-stu-id="fbf18-175">The setting is specific to requirements of the device that you are connecting to.</span></span> <span data-ttu-id="fbf18-176">Para obter mais informações sobre tipos de gateway de VPN, confira [Sobre definições de configuração de gateway de VPN](vpn-gateway-about-vpn-gateway-settings.md#vpntype).</span><span class="sxs-lookup"><span data-stu-id="fbf18-176">For more information about VPN gateway types, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md#vpntype).</span></span>
* <span data-ttu-id="fbf18-177">Selecione a SKU de Gateway que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="fbf18-177">Select the Gateway SKU that you want to use.</span></span> <span data-ttu-id="fbf18-178">Há limitações de configuração para alguns SKUs.</span><span class="sxs-lookup"><span data-stu-id="fbf18-178">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="fbf18-179">Para obter mais informações, confira [SKUs de gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="fbf18-179">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

<span data-ttu-id="fbf18-180">Criar o gateway de VPN usando o comando [az network vnet-gateway create](/cli/azure/network/vnet-gateway#create).</span><span class="sxs-lookup"><span data-stu-id="fbf18-180">Create the VPN gateway using the [az network vnet-gateway create](/cli/azure/network/vnet-gateway#create) command.</span></span> <span data-ttu-id="fbf18-181">Se você executar esse comando usando o parâmetro '--no-wait', você não receberá nenhum feedback ou saída.</span><span class="sxs-lookup"><span data-stu-id="fbf18-181">If you run this command using the '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="fbf18-182">Esse parâmetro permite que o gateway seja criado em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="fbf18-182">This parameter allows the gateway to create in the background.</span></span> <span data-ttu-id="fbf18-183">Demora aproximadamente 45 minutos para criar um gateway.</span><span class="sxs-lookup"><span data-stu-id="fbf18-183">It takes around 45 minutes to create a gateway.</span></span>

```azurecli
az network vnet-gateway create --name VNet1GW --public-ip-address VNet1GWIP --resource-group TestRG1 --vnet TestVNet1 --gateway-type Vpn --vpn-type RouteBased --sku VpnGw1 --no-wait 
```

## <span data-ttu-id="fbf18-184"><a name="VPNDevice"></a>8. Configurar o dispositivo de VPN</span><span class="sxs-lookup"><span data-stu-id="fbf18-184"><a name="VPNDevice"></a>8. Configure your VPN device</span></span>

<span data-ttu-id="fbf18-185">As conexões Site a Site para uma rede local exigem um dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="fbf18-185">Site-to-Site connections to an on-premises network require a VPN device.</span></span> <span data-ttu-id="fbf18-186">Nesta etapa, você deve configurar seu dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="fbf18-186">In this step, you configure your VPN device.</span></span> <span data-ttu-id="fbf18-187">Ao configurar seu dispositivo VPN, você precisará dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="fbf18-187">When configuring your VPN device, you need the following:</span></span>

- <span data-ttu-id="fbf18-188">Uma chave compartilhada.</span><span class="sxs-lookup"><span data-stu-id="fbf18-188">A shared key.</span></span> <span data-ttu-id="fbf18-189">Essa é a mesma chave compartilhada especificada ao criar a conexão VPN Site a Site.</span><span class="sxs-lookup"><span data-stu-id="fbf18-189">This is the same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="fbf18-190">Em nossos exemplos, usamos uma chave compartilhada básica.</span><span class="sxs-lookup"><span data-stu-id="fbf18-190">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="fbf18-191">Recomendamos gerar uma chave mais complexa para uso.</span><span class="sxs-lookup"><span data-stu-id="fbf18-191">We recommend that you generate a more complex key to use.</span></span>
- <span data-ttu-id="fbf18-192">O endereço IP público do seu gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="fbf18-192">The Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="fbf18-193">Você pode exibir o endereço IP público usando o portal do Azure, o PowerShell ou a CLI.</span><span class="sxs-lookup"><span data-stu-id="fbf18-193">You can view the public IP address by using the Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="fbf18-194">Para localizar o endereço IP público do seu gateway de rede virtual, use o comando [az network public-ip list](/cli/azure/network/public-ip#list).</span><span class="sxs-lookup"><span data-stu-id="fbf18-194">To find the public IP address of your virtual network gateway, use the [az network public-ip list](/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="fbf18-195">Para facilitar a leitura, a saída é formatada para exibir a lista de IPs públicos em formato de tabela.</span><span class="sxs-lookup"><span data-stu-id="fbf18-195">For easy reading, the output is formatted to display the list of public IPs in table format.</span></span>

  ```azurecli
  az network public-ip list --resource-group TestRG1 --output table
  ```


[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="fbf18-196"><a name="CreateConnection"></a>9. Criar a conexão VPN</span><span class="sxs-lookup"><span data-stu-id="fbf18-196"><a name="CreateConnection"></a>9. Create the VPN connection</span></span>

<span data-ttu-id="fbf18-197">Crie a conexão VPN Site a Site entre o gateway de rede virtual e o dispositivo VPN local.</span><span class="sxs-lookup"><span data-stu-id="fbf18-197">Create the Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span> <span data-ttu-id="fbf18-198">Preste atenção especial ao valor de chave compartilhada, que deve corresponder ao valor de chave compartilhada configurado para seu dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="fbf18-198">Pay particular attention to the shared key value, which must match the configured shared key value for your VPN device.</span></span>

<span data-ttu-id="fbf18-199">Crie a conexão usando o comando [az network vpn-connection create](/cli/azure/network/vpn-connection#create).</span><span class="sxs-lookup"><span data-stu-id="fbf18-199">Create the connection using the [az network vpn-connection create](/cli/azure/network/vpn-connection#create) command.</span></span>

```azurecli
az network vpn-connection create --name VNet1toSite2 -resource-group TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key abc123 --local-gateway2 Site2
```

<span data-ttu-id="fbf18-200">Após um instante, a conexão será estabelecida.</span><span class="sxs-lookup"><span data-stu-id="fbf18-200">After a short while, the connection will be established.</span></span>

## <span data-ttu-id="fbf18-201"><a name="toverify"></a>10. Verificar a conexão VPN</span><span class="sxs-lookup"><span data-stu-id="fbf18-201"><a name="toverify"></a>10. Verify the VPN connection</span></span>

[!INCLUDE [verify connection](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

<span data-ttu-id="fbf18-202">Se quiser usar outro método para verificar a conexão, confira [Verificar uma conexão de gateway de VPN](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="fbf18-202">If you want to use another method to verify your connection, see [Verify a VPN Gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

## <span data-ttu-id="fbf18-203"><a name="connectVM"></a>Para conectar-se a uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="fbf18-203"><a name="connectVM"></a>To connect to a virtual machine</span></span>

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="fbf18-204"><a name="tasks"></a>Tarefas comuns</span><span class="sxs-lookup"><span data-stu-id="fbf18-204"><a name="tasks"></a>Common tasks</span></span>

<span data-ttu-id="fbf18-205">Esta seção contém os comandos comuns que são úteis ao trabalhar com configurações de site a site.</span><span class="sxs-lookup"><span data-stu-id="fbf18-205">This section contains common commands that are helpful when working with site-to-site configurations.</span></span> <span data-ttu-id="fbf18-206">Para obter a lista completa dos comandos de rede da CLI, consulte [CLI do Azure - Rede](/cli/azure/network).</span><span class="sxs-lookup"><span data-stu-id="fbf18-206">For the full list of CLI networking commands, see [Azure CLI - Networking](/cli/azure/network).</span></span>

[!INCLUDE [local network gateway common tasks](../../includes/vpn-gateway-common-tasks-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="fbf18-207">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fbf18-207">Next steps</span></span>

* <span data-ttu-id="fbf18-208">Quando sua conexão for concluída, você poderá adicionar máquinas virtuais às suas redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="fbf18-208">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="fbf18-209">Para saber mais, veja [Máquinas virtuais](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="fbf18-209">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="fbf18-210">Para obter informações sobre o BGP, consulte a [Visão Geral do BGP](vpn-gateway-bgp-overview.md) e [Como configurar o BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="fbf18-210">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="fbf18-211">Para saber mais sobre Túneis Forçados, confira [Sobre o Túnel Forçado](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="fbf18-211">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="fbf18-212">Para obter informações sobre Conexões Altamente Disponíveis Ativo-Ativo, consulte [Conectividade Altamente Disponível entre locais e Rede Virtual para Rede Virtual](vpn-gateway-highlyavailable.md).</span><span class="sxs-lookup"><span data-stu-id="fbf18-212">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
* <span data-ttu-id="fbf18-213">Para obter uma lista de comandos da CLI do Azure de rede, confira [CLI do Azure](https://docs.microsoft.com/cli/azure/network).</span><span class="sxs-lookup"><span data-stu-id="fbf18-213">For a list of networking Azure CLI commands, see [Azure CLI](https://docs.microsoft.com/cli/azure/network).</span></span>