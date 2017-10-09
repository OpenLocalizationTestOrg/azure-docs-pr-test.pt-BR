---
title: 'Conecte-se a rede virtual tooanother VNet: CLI do Azure | Microsoft Docs'
description: Este artigo mostra como conectar redes virtuais em conjunto usando o Azure Resource Manager e a CLI do Azure.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 70113914bcae03c80f9ad133ff081d1cf37fc309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-azure-cli"></a><span data-ttu-id="cebbb-103">Configurar uma conexão gateway de VPN de Vnet pra VNet usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="cebbb-103">Configure a VNet-to-VNet VPN gateway connection using Azure CLI</span></span>

<span data-ttu-id="cebbb-104">Este artigo mostra como toocreate uma conexão de gateway VPN entre redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="cebbb-104">This article shows you how toocreate a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="cebbb-105">Olá redes virtuais podem ser Olá mesmas ou em diferentes regiões e de Olá mesmo ou em assinaturas diferentes.</span><span class="sxs-lookup"><span data-stu-id="cebbb-105">hello virtual networks can be in hello same or different regions, and from hello same or different subscriptions.</span></span> <span data-ttu-id="cebbb-106">Quando conexão VNets de assinaturas diferentes, assinaturas de saudação não precisarem toobe associado Olá mesmo locatário do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cebbb-106">When connecting VNets from different subscriptions, hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> 

<span data-ttu-id="cebbb-107">etapas de saudação neste artigo aplicam o modelo de implantação do Gerenciador de recursos de toohello e usar a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="cebbb-107">hello steps in this article apply toohello Resource Manager deployment model and use Azure CLI.</span></span> <span data-ttu-id="cebbb-108">Você também pode criar essa configuração usando uma ferramenta de implantação diferente ou um modelo de implantação, selecionando uma opção diferente de saudação lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="cebbb-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cebbb-109">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cebbb-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="cebbb-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cebbb-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="cebbb-111">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="cebbb-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="cebbb-112">Portal do Azure (clássico)</span><span class="sxs-lookup"><span data-stu-id="cebbb-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="cebbb-113">Conectar modelos de implantação diferentes – portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cebbb-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="cebbb-114">Conectar modelos de implantação diferentes - PowerShell</span><span class="sxs-lookup"><span data-stu-id="cebbb-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="cebbb-115">Conectar uma rede virtual tooanother VPN (rede virtual a rede) é semelhante tooconnecting uma VNet tooan no site local.</span><span class="sxs-lookup"><span data-stu-id="cebbb-115">Connecting a virtual network tooanother virtual network (VNet-to-VNet) is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="cebbb-116">Ambos os tipos de conectividade usam um gateway VPN tooprovide um túnel seguro usando IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="cebbb-116">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="cebbb-117">Se seus VNets estão em Olá mesma região, talvez você queira tooconsider conectá-los usando o emparelhamento de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="cebbb-117">If your VNets are in hello same region, you may want tooconsider connecting them using VNet Peering.</span></span> <span data-ttu-id="cebbb-118">O emparelhamento Vnet não usa um gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="cebbb-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="cebbb-119">Para obter mais informações, consulte [Emparelhamento da VNet](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cebbb-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="cebbb-120">Você pode combinar a comunicação de VNet a VNet usando configurações multissite.</span><span class="sxs-lookup"><span data-stu-id="cebbb-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="cebbb-121">Isso permite que você estabeleça topologias de rede que combinem conectividade entre instalações com conectividade de rede intervirtual, como mostrado no diagrama a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="cebbb-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in hello following diagram:</span></span>

![Sobre as conexões](./media/vpn-gateway-howto-vnet-vnet-cli/aboutconnections.png)

### <span data-ttu-id="cebbb-123"><a name="why"></a>Por que conectar redes virtuais?</span><span class="sxs-lookup"><span data-stu-id="cebbb-123"><a name="why"></a>Why connect virtual networks?</span></span>

<span data-ttu-id="cebbb-124">Você talvez queira redes virtuais tooconnect para Olá motivos a seguir:</span><span class="sxs-lookup"><span data-stu-id="cebbb-124">You may want tooconnect virtual networks for hello following reasons:</span></span>

* <span data-ttu-id="cebbb-125">**Redundância geográfica entre regiões e presença geográfica**</span><span class="sxs-lookup"><span data-stu-id="cebbb-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="cebbb-126">Você pode configurar sua própria sincronização ou replicação geográfica com conectividade segura sem passar por pontos de extremidade voltados para a Internet.</span><span class="sxs-lookup"><span data-stu-id="cebbb-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="cebbb-127">Com o Balanceador de Carga e o Gerenciador de Tráfego do Azure você pode configurar a carga de trabalho de alta disponibilidade com redundância geográfica em várias regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="cebbb-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="cebbb-128">Um exemplo importante é tooset backup SQL Always On com grupos de disponibilidade espalhados por várias regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="cebbb-128">One important example is tooset up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="cebbb-129">**Aplicativos multicamadas regionais com limite administrativo ou de isolamento**</span><span class="sxs-lookup"><span data-stu-id="cebbb-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="cebbb-130">Olá na mesma região, você pode configurar aplicativos de várias camadas com várias redes virtuais conectadas devido tooisolation ou requisitos administrativos.</span><span class="sxs-lookup"><span data-stu-id="cebbb-130">Within hello same region, you can set up multi-tier applications with multiple virtual networks connected together due tooisolation or administrative requirements.</span></span>

<span data-ttu-id="cebbb-131">Para obter mais informações sobre conexões de rede virtual a rede, consulte Olá [perguntas Frequentes de VNet para VNet](#faq) final Olá deste artigo.</span><span class="sxs-lookup"><span data-stu-id="cebbb-131">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span>

### <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="cebbb-132">Qual conjunto de etapas devo usar?</span><span class="sxs-lookup"><span data-stu-id="cebbb-132">Which set of steps should I use?</span></span>

<span data-ttu-id="cebbb-133">Neste artigo, você verá dois conjuntos de etapas diferentes.</span><span class="sxs-lookup"><span data-stu-id="cebbb-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="cebbb-134">Um conjunto de etapas para [Olá de VNets que residem na mesma assinatura](#samesub)e outro para [VNets que residem em diferentes assinaturas](#difsub).</span><span class="sxs-lookup"><span data-stu-id="cebbb-134">One set of steps for [VNets that reside in hello same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span>

## <span data-ttu-id="cebbb-135"><a name="samesub"></a>Conectar-se VNets que estão em Olá mesma assinatura</span><span class="sxs-lookup"><span data-stu-id="cebbb-135"><a name="samesub"></a>Connect VNets that are in hello same subscription</span></span>

![Diagrama de v2v](./media/vpn-gateway-howto-vnet-vnet-cli/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="cebbb-137">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="cebbb-137">Before you begin</span></span>

<span data-ttu-id="cebbb-138">Antes de começar, instale a versão mais recente Olá de comandos CLI hello (2.0 ou posteriores).</span><span class="sxs-lookup"><span data-stu-id="cebbb-138">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="cebbb-139">Para obter informações sobre como instalar os comandos CLI hello, consulte [instalar o Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="cebbb-139">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

### <span data-ttu-id="cebbb-140"><a name="Plan"></a>Planejar os intervalos de endereços IP</span><span class="sxs-lookup"><span data-stu-id="cebbb-140"><a name="Plan"></a>Plan your IP address ranges</span></span>

<span data-ttu-id="cebbb-141">Olá etapas a seguir, criamos duas redes virtuais junto com suas configurações e sub-redes do respectivos gateway.</span><span class="sxs-lookup"><span data-stu-id="cebbb-141">In hello following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="cebbb-142">Em seguida, criamos uma conexão VPN entre hello duas VNets.</span><span class="sxs-lookup"><span data-stu-id="cebbb-142">We then create a VPN connection between hello two VNets.</span></span> <span data-ttu-id="cebbb-143">É importante tooplan intervalos de endereços IP Olá para sua configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="cebbb-143">It’s important tooplan hello IP address ranges for your network configuration.</span></span> <span data-ttu-id="cebbb-144">Lembre-se de que você deve garantir que nenhum de seus intervalos de VNet ou intervalos de rede local se sobreponham de forma alguma.</span><span class="sxs-lookup"><span data-stu-id="cebbb-144">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="cebbb-145">Nestes exemplos, não incluímos um servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="cebbb-145">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="cebbb-146">Se você deseja resolução de nomes para suas redes virtuais, confira [a Resolução de nomes](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="cebbb-146">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="cebbb-147">Usamos Olá valores nos exemplos Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="cebbb-147">We use hello following values in hello examples:</span></span>

<span data-ttu-id="cebbb-148">**Valores para TestVNet1:**</span><span class="sxs-lookup"><span data-stu-id="cebbb-148">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="cebbb-149">Nome da rede virtual: TestVNet1</span><span class="sxs-lookup"><span data-stu-id="cebbb-149">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="cebbb-150">Grupo de recursos: TestRG1</span><span class="sxs-lookup"><span data-stu-id="cebbb-150">Resource Group: TestRG1</span></span>
* <span data-ttu-id="cebbb-151">Local: Leste dos EUA</span><span class="sxs-lookup"><span data-stu-id="cebbb-151">Location: East US</span></span>
* <span data-ttu-id="cebbb-152">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="cebbb-152">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="cebbb-153">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="cebbb-153">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="cebbb-154">BackEnd: 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="cebbb-154">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="cebbb-155">GatewaySubnet: 10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="cebbb-155">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="cebbb-156">GatewayName: VNet1GW</span><span class="sxs-lookup"><span data-stu-id="cebbb-156">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="cebbb-157">IP público: VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="cebbb-157">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="cebbb-158">VpnType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="cebbb-158">VPNType: RouteBased</span></span>
* <span data-ttu-id="cebbb-159">Connection(1to4): VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="cebbb-159">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="cebbb-160">Connection(1to5): VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="cebbb-160">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="cebbb-161">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="cebbb-161">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="cebbb-162">**Valores para TestVNet4:**</span><span class="sxs-lookup"><span data-stu-id="cebbb-162">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="cebbb-163">Nome da rede virtual: TestVNet4</span><span class="sxs-lookup"><span data-stu-id="cebbb-163">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="cebbb-164">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="cebbb-164">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="cebbb-165">FrontEnd: 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="cebbb-165">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="cebbb-166">BackEnd: 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="cebbb-166">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="cebbb-167">GatewaySubnet: 10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="cebbb-167">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="cebbb-168">Grupo de recursos: TestRG4</span><span class="sxs-lookup"><span data-stu-id="cebbb-168">Resource Group: TestRG4</span></span>
* <span data-ttu-id="cebbb-169">Local: Oeste dos EUA</span><span class="sxs-lookup"><span data-stu-id="cebbb-169">Location: West US</span></span>
* <span data-ttu-id="cebbb-170">GatewayName: VNet4GW</span><span class="sxs-lookup"><span data-stu-id="cebbb-170">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="cebbb-171">IP público: VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="cebbb-171">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="cebbb-172">VpnType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="cebbb-172">VPNType: RouteBased</span></span>
* <span data-ttu-id="cebbb-173">Conexão: VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="cebbb-173">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="cebbb-174">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="cebbb-174">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="cebbb-175"><a name="Connect"></a>Etapa 1: conectar tooyour assinatura</span><span class="sxs-lookup"><span data-stu-id="cebbb-175"><a name="Connect"></a>Step 1 - Connect tooyour subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-numbers-include.md)]

### <span data-ttu-id="cebbb-176"><a name="TestVNet1"></a>Etapa 2: Criar e configurar o TestVNet1</span><span class="sxs-lookup"><span data-stu-id="cebbb-176"><a name="TestVNet1"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="cebbb-177">Crie um grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="cebbb-177">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG1  -l eastus
  ```
2. <span data-ttu-id="cebbb-178">Crie sub-redes TestVNet1 e hello para TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="cebbb-178">Create TestVNet1 and hello subnets for TestVNet1.</span></span> <span data-ttu-id="cebbb-179">O exemplo a seguir cria uma rede virtual chamada TestVNet1 e uma sub-rede chamada FrontEnd.</span><span class="sxs-lookup"><span data-stu-id="cebbb-179">This example creates a virtual network named TestVNet1 and a subnet named FrontEnd.</span></span>

  ```azurecli
  az network vnet create -n TestVNet1 -g TestRG1 --address-prefix 10.11.0.0/16 -l eastus --subnet-name FrontEnd --subnet-prefix 10.11.0.0/24
  ```
3. <span data-ttu-id="cebbb-180">Crie um espaço de endereço adicional para a sub-rede de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="cebbb-180">Create an additional address space for hello backend subnet.</span></span> <span data-ttu-id="cebbb-181">Observe que essa etapa, podemos especificar que ambos Olá espaço de endereço que criamos anteriormente e Olá adicional a que desejamos tooadd de espaço de endereço.</span><span class="sxs-lookup"><span data-stu-id="cebbb-181">Notice that in this step, we specify both hello address space that we created earlier, and hello additional address space that we want tooadd.</span></span> <span data-ttu-id="cebbb-182">Isso ocorre porque Olá [atualização da rede virtual de rede az](https://docs.microsoft.com/cli/azure/network/vnet#update) comando substitui configurações anteriores hello.</span><span class="sxs-lookup"><span data-stu-id="cebbb-182">This is because hello [az network vnet update](https://docs.microsoft.com/cli/azure/network/vnet#update) command overwrites hello previous settings.</span></span> <span data-ttu-id="cebbb-183">Torne toospecify-se de que todos os prefixos de endereço Olá ao usar esse comando.</span><span class="sxs-lookup"><span data-stu-id="cebbb-183">Make sure toospecify all of hello address prefixes when using this command.</span></span>

  ```azurecli
  az network vnet update -n TestVNet1 --address-prefixes 10.11.0.0/16 10.12.0.0/16 -g TestRG1
  ```
4. <span data-ttu-id="cebbb-184">Crie uma sub-rede de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="cebbb-184">Create hello backend subnet.</span></span>
  
  ```azurecli
  az network vnet subnet create --vnet-name TestVNet1 -n BackEnd -g TestRG1 --address-prefix 10.12.0.0/24 
  ```
5. <span data-ttu-id="cebbb-185">Crie uma sub-rede de gateway hello.</span><span class="sxs-lookup"><span data-stu-id="cebbb-185">Create hello gateway subnet.</span></span> <span data-ttu-id="cebbb-186">Observe que essa sub-rede de gateway Olá é denominada 'GatewaySubnet'.</span><span class="sxs-lookup"><span data-stu-id="cebbb-186">Notice that hello gateway subnet is named 'GatewaySubnet'.</span></span> <span data-ttu-id="cebbb-187">Esse nome é obrigatório.</span><span class="sxs-lookup"><span data-stu-id="cebbb-187">This name is required.</span></span> <span data-ttu-id="cebbb-188">Neste exemplo, a sub-rede de gateway de saudação está usando um /27.</span><span class="sxs-lookup"><span data-stu-id="cebbb-188">In this example, hello gateway subnet is using a /27.</span></span> <span data-ttu-id="cebbb-189">Embora seja possível toocreate tão pequenas quanto /29 uma sub-rede do gateway, é recomendável que você crie uma sub-rede maior que inclui mais endereços selecionando pelo menos /28 ou /27.</span><span class="sxs-lookup"><span data-stu-id="cebbb-189">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="cebbb-190">Isso permitirá suficiente endereços tooaccommodate possíveis configurações adicionais que você pode em Olá futuras.</span><span class="sxs-lookup"><span data-stu-id="cebbb-190">This will allow for enough addresses tooaccommodate possible additional configurations that you may want in hello future.</span></span>

  ```azurecli 
  az network vnet subnet create --vnet-name TestVNet1 -n GatewaySubnet -g TestRG1 --address-prefix 10.12.255.0/27
  ```
6. <span data-ttu-id="cebbb-191">Solicite um público endereço toobe toohello alocado gateway IP que você criará para sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="cebbb-191">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="cebbb-192">Observe que Olá AllocationMethod é dinâmico.</span><span class="sxs-lookup"><span data-stu-id="cebbb-192">Notice that hello AllocationMethod is Dynamic.</span></span> <span data-ttu-id="cebbb-193">Não é possível especificar o endereço IP de saudação que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="cebbb-193">You cannot specify hello IP address that you want toouse.</span></span> <span data-ttu-id="cebbb-194">É gateway tooyour alocada dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="cebbb-194">It's dynamically allocated tooyour gateway.</span></span>

  ```azurecli
  az network public-ip create -n VNet1GWIP -g TestRG1 --allocation-method Dynamic
  ```
7. <span data-ttu-id="cebbb-195">Crie gateway de rede virtual Olá para TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="cebbb-195">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="cebbb-196">As configurações de rede virtual com rede virtual exigem um VpnType RouteBased.</span><span class="sxs-lookup"><span data-stu-id="cebbb-196">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="cebbb-197">Se você executar esse comando hello usando o parâmetro '-- Nenhum - wait', você não vir quaisquer comentários ou saída.</span><span class="sxs-lookup"><span data-stu-id="cebbb-197">If you run this command using hello '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="cebbb-198">Olá '-- Nenhum - wait' parâmetro permite Olá gateway toocreate no plano de fundo de saudação.</span><span class="sxs-lookup"><span data-stu-id="cebbb-198">hello '--no-wait' parameter allows hello gateway toocreate in hello background.</span></span> <span data-ttu-id="cebbb-199">Isso não significa que esse gateway VPN Olá termina de criar imediatamente.</span><span class="sxs-lookup"><span data-stu-id="cebbb-199">It does not mean that hello VPN gateway finishes creating immediately.</span></span> <span data-ttu-id="cebbb-200">Criar um gateway pode levar até 45 minutos ou mais, dependendo do gateway Olá SKU que você usa.</span><span class="sxs-lookup"><span data-stu-id="cebbb-200">Creating a gateway can often take 45 minutes or more, depending on hello gateway SKU that you use.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet1GW -l eastus --public-ip-address VNet1GWIP -g TestRG1 --vnet TestVNet1 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="cebbb-201"><a name="TestVNet4"></a>Etapa 3: criar e configurar TestVNet4</span><span class="sxs-lookup"><span data-stu-id="cebbb-201"><a name="TestVNet4"></a>Step 3 - Create and configure TestVNet4</span></span>

1. <span data-ttu-id="cebbb-202">Crie um grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="cebbb-202">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG4  -l westus
  ```
2. <span data-ttu-id="cebbb-203">Crie a TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="cebbb-203">Create TestVNet4.</span></span>

  ```azurecli
  az network vnet create -n TestVNet4 -g TestRG4 --address-prefix 10.41.0.0/16 -l westus --subnet-name FrontEnd --subnet-prefix 10.41.0.0/24
  ```

3. <span data-ttu-id="cebbb-204">Crie sub-redes adicionais para TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="cebbb-204">Create additional subnets for TestVNet4.</span></span>

  ```azurecli
  az network vnet update -n TestVNet4 --address-prefixes 10.41.0.0/16 10.42.0.0/16 -g TestRG4 
  az network vnet subnet create --vnet-name TestVNet4 -n BackEnd -g TestRG4 --address-prefix 10.42.0.0/24 
  ```
4. <span data-ttu-id="cebbb-205">Crie uma sub-rede de gateway hello.</span><span class="sxs-lookup"><span data-stu-id="cebbb-205">Create hello gateway subnet.</span></span>

  ```azurecli
   az network vnet subnet create --vnet-name TestVNet4 -n GatewaySubnet -g TestRG4 --address-prefix 10.42.255.0/27
  ```
5. <span data-ttu-id="cebbb-206">Solicite um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="cebbb-206">Request a Public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet4GWIP -g TestRG4 --allocation-method Dynamic
  ```
6. <span data-ttu-id="cebbb-207">Crie gateway de rede virtual TestVNet4 hello.</span><span class="sxs-lookup"><span data-stu-id="cebbb-207">Create hello TestVNet4 virtual network gateway.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet4GW -l westus --public-ip-address VNet4GWIP -g TestRG4 --vnet TestVNet4 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="cebbb-208"><a name="createconnect"></a>Etapa 4 - criar conexões Olá</span><span class="sxs-lookup"><span data-stu-id="cebbb-208"><a name="createconnect"></a>Step 4 - Create hello connections</span></span>

<span data-ttu-id="cebbb-209">Agora, você tem duas redes virtuais com gateways de VPN.</span><span class="sxs-lookup"><span data-stu-id="cebbb-209">You now have two VNets with VPN gateways.</span></span> <span data-ttu-id="cebbb-210">Olá próxima etapa é toocreate conexões de gateway VPN entre os gateways de rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="cebbb-210">hello next step is toocreate VPN gateway connections between hello virtual network gateways.</span></span> <span data-ttu-id="cebbb-211">Se você usou exemplos de saudação acima, seus gateways de rede virtual estão em diferentes grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="cebbb-211">If you used hello examples above, your VNet gateways are in different resource groups.</span></span> <span data-ttu-id="cebbb-212">Quando os gateways estiverem em diferentes grupos de recursos, você precisa tooidentify e especifique IDs de recurso Olá para cada gateway ao fazer uma conexão.</span><span class="sxs-lookup"><span data-stu-id="cebbb-212">When gateways are in different resource groups, you need tooidentify and specify hello resource IDs for each gateway when making a connection.</span></span> <span data-ttu-id="cebbb-213">Se seus VNets estão em Olá mesmo grupo de recursos, você pode usar o hello [segundo conjunto de instruções](#samerg) porque você não precisa de IDs de recurso Olá toospecify.</span><span class="sxs-lookup"><span data-stu-id="cebbb-213">If your VNets are in hello same resource group, you can use hello [second set of instructions](#samerg) because you don't need toospecify hello resource IDs.</span></span>

### <span data-ttu-id="cebbb-214"><a name="diffrg"></a>tooconnect VNets que residem em diferentes grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="cebbb-214"><a name="diffrg"></a>tooconnect VNets that reside in different resource groups</span></span>

1. <span data-ttu-id="cebbb-215">Obter ID do recurso de VNet1GW de saudação da saída de saudação de saudação comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="cebbb-215">Get hello Resource ID of VNet1GW from hello output of hello following command:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="cebbb-216">Na saída de hello, localize Olá "id:" linha.</span><span class="sxs-lookup"><span data-stu-id="cebbb-216">In hello output, find hello "id:" line.</span></span> <span data-ttu-id="cebbb-217">os valores de Olá aspas Olá são necessários toocreate Olá conexão na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="cebbb-217">hello values within hello quotes are needed toocreate hello connection in hello next section.</span></span> <span data-ttu-id="cebbb-218">Copie o editor de texto de tooa esses valores, como o bloco de notas, para que você possa colá-los facilmente ao criar sua conexão.</span><span class="sxs-lookup"><span data-stu-id="cebbb-218">Copy these values tooa text editor, such as Notepad, so that you can easily paste them when creating your connection.</span></span>

  <span data-ttu-id="cebbb-219">Saída de exemplo:</span><span class="sxs-lookup"><span data-stu-id="cebbb-219">Example output:</span></span>

  ```
  "activeActive": false, 
  "bgpSettings": { 
    "asn": 65515, 
    "bgpPeeringAddress": "10.12.255.30", 
    "peerWeight": 0 
   }, 
  "enableBgp": false, 
  "etag": "W/\"ecb42bc5-c176-44e1-802f-b0ce2962ac04\"", 
  "gatewayDefaultSite": null, 
  "gatewayType": "Vpn", 
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW", 
  "ipConfigurations":
  ```

  <span data-ttu-id="cebbb-220">Copiar os valores hello após **"id":** aspas hello.</span><span class="sxs-lookup"><span data-stu-id="cebbb-220">Copy hello values after **"id":** within hello quotes.</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
 ```

2. <span data-ttu-id="cebbb-221">Obter Olá ID do recurso de VNet4GW e cópia Olá valores tooa editor de texto.</span><span class="sxs-lookup"><span data-stu-id="cebbb-221">Get hello Resource ID of VNet4GW and copy hello values tooa text editor.</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet4GW -g TestRG4
  ```

3. <span data-ttu-id="cebbb-222">Crie conexão de tooTestVNet4 TestVNet1 hello.</span><span class="sxs-lookup"><span data-stu-id="cebbb-222">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="cebbb-223">Nesta etapa, você pode criar conexão de saudação do TestVNet1 tooTestVNet4.</span><span class="sxs-lookup"><span data-stu-id="cebbb-223">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="cebbb-224">Há uma chave compartilhada referenciada nos exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="cebbb-224">There is a shared key referenced in hello examples.</span></span> <span data-ttu-id="cebbb-225">Você pode usar seus próprios valores para a chave compartilhada hello.</span><span class="sxs-lookup"><span data-stu-id="cebbb-225">You can use your own values for hello shared key.</span></span> <span data-ttu-id="cebbb-226">Olá importante é chave compartilhada Olá deve corresponder para ambas as conexões.</span><span class="sxs-lookup"><span data-stu-id="cebbb-226">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="cebbb-227">Criar uma conexão entra em um instante toocomplete.</span><span class="sxs-lookup"><span data-stu-id="cebbb-227">Creating a connection takes a short while toocomplete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW 
  ```
4. <span data-ttu-id="cebbb-228">Crie conexão de tooTestVNet1 TestVNet4 hello.</span><span class="sxs-lookup"><span data-stu-id="cebbb-228">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="cebbb-229">Esta etapa é semelhante toohello mostrado acima, exceto que você está criando a conexão de saudação da TestVNet4 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="cebbb-229">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="cebbb-230">Certifique-se de saudação compartilhada chaves correspondentes.</span><span class="sxs-lookup"><span data-stu-id="cebbb-230">Make sure hello shared keys match.</span></span> <span data-ttu-id="cebbb-231">Levará alguns minutos tooestablish conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="cebbb-231">It takes a few minutes tooestablish hello connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG4 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW -l westus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1G
  ```
5. <span data-ttu-id="cebbb-232">Verifique as conexões.</span><span class="sxs-lookup"><span data-stu-id="cebbb-232">Verify your connections.</span></span> <span data-ttu-id="cebbb-233">Confira [Verificar a conexão](#verify).</span><span class="sxs-lookup"><span data-stu-id="cebbb-233">See [Verify your connection](#verify).</span></span>

### <span data-ttu-id="cebbb-234"><a name="samerg"></a>tooconnect VNets que residem no hello mesmo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="cebbb-234"><a name="samerg"></a>tooconnect VNets that reside in hello same resource group</span></span>

1. <span data-ttu-id="cebbb-235">Crie conexão de tooTestVNet4 TestVNet1 hello.</span><span class="sxs-lookup"><span data-stu-id="cebbb-235">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="cebbb-236">Nesta etapa, você pode criar conexão de saudação do TestVNet1 tooTestVNet4.</span><span class="sxs-lookup"><span data-stu-id="cebbb-236">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="cebbb-237">Grupos de recursos de saudação de aviso são Olá mesmo nos exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="cebbb-237">Notice hello resource groups are hello same in hello examples.</span></span> <span data-ttu-id="cebbb-238">Você também pode ver uma chave compartilhada referenciada nos exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="cebbb-238">You also see a shared key referenced in hello examples.</span></span> <span data-ttu-id="cebbb-239">Você pode usar seus próprios valores para a chave compartilhada Olá, no entanto, a chave compartilhada Olá deve corresponder para ambas as conexões.</span><span class="sxs-lookup"><span data-stu-id="cebbb-239">You can use your own values for hello shared key, however, hello shared key must match for both connections.</span></span> <span data-ttu-id="cebbb-240">Criar uma conexão entra em um instante toocomplete.</span><span class="sxs-lookup"><span data-stu-id="cebbb-240">Creating a connection takes a short while toocomplete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet4GW
  ```
2. <span data-ttu-id="cebbb-241">Crie conexão de tooTestVNet1 TestVNet4 hello.</span><span class="sxs-lookup"><span data-stu-id="cebbb-241">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="cebbb-242">Esta etapa é semelhante toohello mostrado acima, exceto que você está criando a conexão de saudação da TestVNet4 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="cebbb-242">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="cebbb-243">Certifique-se de saudação compartilhada chaves correspondentes.</span><span class="sxs-lookup"><span data-stu-id="cebbb-243">Make sure hello shared keys match.</span></span> <span data-ttu-id="cebbb-244">Levará alguns minutos tooestablish conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="cebbb-244">It takes a few minutes tooestablish hello connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG1 --vnet-gateway1 VNet4GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet1GW
  ```
3. <span data-ttu-id="cebbb-245">Verifique as conexões.</span><span class="sxs-lookup"><span data-stu-id="cebbb-245">Verify your connections.</span></span> <span data-ttu-id="cebbb-246">Confira [Verificar a conexão](#verify).</span><span class="sxs-lookup"><span data-stu-id="cebbb-246">See [Verify your connection](#verify).</span></span>

## <span data-ttu-id="cebbb-247"><a name="difsub"></a>Conectar as VNets que estão em assinaturas diferentes</span><span class="sxs-lookup"><span data-stu-id="cebbb-247"><a name="difsub"></a>Connect VNets that are in different subscriptions</span></span>

![Diagrama de v2v](./media/vpn-gateway-howto-vnet-vnet-cli/v2vdiffsub.png)

<span data-ttu-id="cebbb-249">Nesse cenário, conectamos TestVNet1 e TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="cebbb-249">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="cebbb-250">Olá VNets residir assinaturas diferentes.</span><span class="sxs-lookup"><span data-stu-id="cebbb-250">hello VNets reside different subscriptions.</span></span> <span data-ttu-id="cebbb-251">Olá assinaturas não precisem toobe associado Olá mesmo locatário do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cebbb-251">hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> <span data-ttu-id="cebbb-252">etapas de saudação para essa configuração adicionam uma conexão de rede virtual a rede adicional na ordem tooconnect TestVNet1 tooTestVNet5.</span><span class="sxs-lookup"><span data-stu-id="cebbb-252">hello steps for this configuration add an additional VNet-to-VNet connection in order tooconnect TestVNet1 tooTestVNet5.</span></span>

### <span data-ttu-id="cebbb-253"><a name="TestVNet1diff"></a>Etapa 5: criar e configurar o TestVNet1</span><span class="sxs-lookup"><span data-stu-id="cebbb-253"><a name="TestVNet1diff"></a>Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="cebbb-254">Essas instruções continuam de etapas Olá Olá anterior seções.</span><span class="sxs-lookup"><span data-stu-id="cebbb-254">These instructions continue from hello steps in hello preceding sections.</span></span> <span data-ttu-id="cebbb-255">Você deve concluir [etapa 1](#Connect) e [etapa 2](#TestVNet1) toocreate configurar TestVNet1 e hello Gateway VPN para TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="cebbb-255">You must complete [Step 1](#Connect) and [Step 2](#TestVNet1) toocreate and configure TestVNet1 and hello VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="cebbb-256">Para essa configuração, você não é necessário toocreate TestVNet4 da seção anterior do hello, embora se você criá-lo, ele não está em conflito com estas etapas.</span><span class="sxs-lookup"><span data-stu-id="cebbb-256">For this configuration, you are not required toocreate TestVNet4 from hello previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="cebbb-257">Depois de concluir as Etapas 1 e 2, continue com a Etapa 6 (abaixo).</span><span class="sxs-lookup"><span data-stu-id="cebbb-257">Once you complete Step 1 and Step 2, continue with Step 6 (below).</span></span>

### <span data-ttu-id="cebbb-258"><a name="verifyranges"></a>Etapa 6 - Verifique se os intervalos de endereços IP Olá</span><span class="sxs-lookup"><span data-stu-id="cebbb-258"><a name="verifyranges"></a>Step 6 - Verify hello IP address ranges</span></span>

<span data-ttu-id="cebbb-259">Ao criar conexões adicionais, é importante tooverify que o espaço de endereço IP de saudação da nova rede virtual de saudação não coincide com nenhum dos outros intervalos de VNet ou intervalos de gateway de rede local.</span><span class="sxs-lookup"><span data-stu-id="cebbb-259">When creating additional connections, it's important tooverify that hello IP address space of hello new virtual network does not overlap with any of your other VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="cebbb-260">Para este exercício, você pode usar Olá Olá TestVNet5 valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="cebbb-260">For this exercise, you can use hello following values for hello TestVNet5:</span></span>

<span data-ttu-id="cebbb-261">**Valores para TestVNet5:**</span><span class="sxs-lookup"><span data-stu-id="cebbb-261">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="cebbb-262">Nome da rede virtual: TestVNet5</span><span class="sxs-lookup"><span data-stu-id="cebbb-262">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="cebbb-263">Grupo de recursos: TestRG5</span><span class="sxs-lookup"><span data-stu-id="cebbb-263">Resource Group: TestRG5</span></span>
* <span data-ttu-id="cebbb-264">Local: Leste do Japão</span><span class="sxs-lookup"><span data-stu-id="cebbb-264">Location: Japan East</span></span>
* <span data-ttu-id="cebbb-265">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="cebbb-265">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="cebbb-266">FrontEnd: 10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="cebbb-266">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="cebbb-267">BackEnd: 10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="cebbb-267">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="cebbb-268">GatewaySubnet: 10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="cebbb-268">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="cebbb-269">GatewayName: VNet5GW</span><span class="sxs-lookup"><span data-stu-id="cebbb-269">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="cebbb-270">IP público: VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="cebbb-270">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="cebbb-271">VpnType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="cebbb-271">VPNType: RouteBased</span></span>
* <span data-ttu-id="cebbb-272">Connection: VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="cebbb-272">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="cebbb-273">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="cebbb-273">ConnectionType: VNet2VNet</span></span>

### <span data-ttu-id="cebbb-274"><a name="TestVNet5"></a>Etapa 7: criar e configurar TestVNet5</span><span class="sxs-lookup"><span data-stu-id="cebbb-274"><a name="TestVNet5"></a>Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="cebbb-275">Esta etapa deve ser feita no contexto de saudação da nova assinatura hello, 5 de assinatura.</span><span class="sxs-lookup"><span data-stu-id="cebbb-275">This step must be done in hello context of hello new subscription, Subscription 5.</span></span> <span data-ttu-id="cebbb-276">Esta parte pode ser executada pelo administrador Olá em uma organização diferente que possui assinatura hello.</span><span class="sxs-lookup"><span data-stu-id="cebbb-276">This part may be performed by hello administrator in a different organization that owns hello subscription.</span></span> <span data-ttu-id="cebbb-277">tooswitch entre o uso de assinaturas ' lista de contas az – todos os ' toolist Olá conta tooyour disponíveis de assinaturas, em seguida, use ' az conta conjunto – assinatura <subscriptionID>' tooswitch toohello assinatura que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="cebbb-277">tooswitch between subscriptions use 'az account list --all' toolist hello subscriptions available tooyour account, then use 'az account set --subscription <subscriptionID>' tooswitch toohello subscription that you want toouse.</span></span>

1. <span data-ttu-id="cebbb-278">Verifique se você estiver conectado tooSubscription 5, então, cria um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="cebbb-278">Make sure you are connected tooSubscription 5, then create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG5  -l japaneast
  ```
2. <span data-ttu-id="cebbb-279">Crie a TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="cebbb-279">Create TestVNet5.</span></span>

  ```azurecli
  az network vnet create -n TestVNet5 -g TestRG5 --address-prefix 10.51.0.0/16 -l japaneast --subnet-name FrontEnd --subnet-prefix 10.51.0.0/24
  ```

3. <span data-ttu-id="cebbb-280">Adicione sub-redes.</span><span class="sxs-lookup"><span data-stu-id="cebbb-280">Add subnets.</span></span>

  ```azurecli
  az network vnet update -n TestVNet5 --address-prefixes 10.51.0.0/16 10.52.0.0/16 -g TestRG5
  az network vnet subnet create --vnet-name TestVNet5 -n BackEnd -g TestRG5 --address-prefix 10.52.0.0/24
  ```

4. <span data-ttu-id="cebbb-281">Adicione sub-rede de gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="cebbb-281">Add hello gateway subnet.</span></span>

  ```azurecli
  az network vnet subnet create --vnet-name TestVNet5 -n GatewaySubnet -g TestRG5 --address-prefix 10.52.255.0/27
  ```

5. <span data-ttu-id="cebbb-282">Solicite um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="cebbb-282">Request a public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet5GWIP -g TestRG5 --allocation-method Dynamic
  ```
6. <span data-ttu-id="cebbb-283">Criar hello TestVNet5 gateway</span><span class="sxs-lookup"><span data-stu-id="cebbb-283">Create hello TestVNet5 gateway</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet5GW -l japaneast --public-ip-address VNet5GWIP -g TestRG5 --vnet TestVNet5 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="cebbb-284"><a name="connections5"></a>Etapa 8 — criar conexões Olá</span><span class="sxs-lookup"><span data-stu-id="cebbb-284"><a name="connections5"></a>Step 8 - Create hello connections</span></span>

<span data-ttu-id="cebbb-285">Dividiremos esta etapa em duas sessões CLI marcado como **[1 assinatura]**, e **[assinatura 5]** como gateways Olá estão em assinaturas diferentes hello.</span><span class="sxs-lookup"><span data-stu-id="cebbb-285">We split this step into two CLI sessions marked as **[Subscription 1]**, and **[Subscription 5]** because hello gateways are in hello different subscriptions.</span></span> <span data-ttu-id="cebbb-286">tooswitch entre o uso de assinaturas ' lista de contas az – todos os ' toolist Olá conta tooyour disponíveis de assinaturas, em seguida, use ' az conta conjunto – assinatura <subscriptionID>' tooswitch toohello assinatura que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="cebbb-286">tooswitch between subscriptions use 'az account list --all' toolist hello subscriptions available tooyour account, then use 'az account set --subscription <subscriptionID>' tooswitch toohello subscription that you want toouse.</span></span>

1. <span data-ttu-id="cebbb-287">**[Assinatura 1]**  Login e conecte-se tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="cebbb-287">**[Subscription 1]** Log in and connect tooSubscription 1.</span></span> <span data-ttu-id="cebbb-288">Comando a seguir de execução Olá tooget Olá nome e ID Olá Gateway de saída de hello:</span><span class="sxs-lookup"><span data-stu-id="cebbb-288">Run hello following command tooget hello name and ID of hello Gateway from hello output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="cebbb-289">Copiar saída hello "id:".</span><span class="sxs-lookup"><span data-stu-id="cebbb-289">Copy hello output for "id:".</span></span> <span data-ttu-id="cebbb-290">Envie Olá ID e nome de saudação do Olá VNet (VNet1GW) toohello administrador do gateway de 5 de assinatura por email ou outro método.</span><span class="sxs-lookup"><span data-stu-id="cebbb-290">Send hello ID and hello name of hello VNet gateway (VNet1GW) toohello administrator of Subscription 5 via email or another method.</span></span>

  <span data-ttu-id="cebbb-291">Saída de exemplo:</span><span class="sxs-lookup"><span data-stu-id="cebbb-291">Example output:</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
  ```

2. <span data-ttu-id="cebbb-292">**[Assinatura 5]**  Login e conecte-se tooSubscription 5.</span><span class="sxs-lookup"><span data-stu-id="cebbb-292">**[Subscription 5]** Log in and connect tooSubscription 5.</span></span> <span data-ttu-id="cebbb-293">Comando a seguir de execução Olá tooget Olá nome e ID Olá Gateway de saída de hello:</span><span class="sxs-lookup"><span data-stu-id="cebbb-293">Run hello following command tooget hello name and ID of hello Gateway from hello output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet5GW -g TestRG5
  ```

  <span data-ttu-id="cebbb-294">Copiar saída hello "id:".</span><span class="sxs-lookup"><span data-stu-id="cebbb-294">Copy hello output for "id:".</span></span> <span data-ttu-id="cebbb-295">Envie Olá ID e nome de saudação do Olá VNet (VNet5GW) toohello administrador do gateway de 1 de assinatura por email ou outro método.</span><span class="sxs-lookup"><span data-stu-id="cebbb-295">Send hello ID and hello name of hello VNet gateway (VNet5GW) toohello administrator of Subscription 1 via email or another method.</span></span>

3. <span data-ttu-id="cebbb-296">**[Assinatura 1]**  Nesta etapa, você criar conexão de saudação do TestVNet1 tooTestVNet5.</span><span class="sxs-lookup"><span data-stu-id="cebbb-296">**[Subscription 1]** In this step, you create hello connection from TestVNet1 tooTestVNet5.</span></span> <span data-ttu-id="cebbb-297">Você pode usar seus próprios valores para a chave compartilhada Olá, no entanto, a chave compartilhada Olá deve corresponder para ambas as conexões.</span><span class="sxs-lookup"><span data-stu-id="cebbb-297">You can use your own values for hello shared key, however, hello shared key must match for both connections.</span></span> <span data-ttu-id="cebbb-298">Criar uma conexão pode demorar um pouco ao toocomplete.</span><span class="sxs-lookup"><span data-stu-id="cebbb-298">Creating a connection can take a short while toocomplete.</span></span> <span data-ttu-id="cebbb-299">Verifique se que você se conectar tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="cebbb-299">Make sure you connect tooSubscription 1.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet5 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```

4. <span data-ttu-id="cebbb-300">**[Assinatura 5]**  Esta etapa é semelhante toohello mostrado acima, exceto que você está criando a conexão de saudação da TestVNet5 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="cebbb-300">**[Subscription 5]** This step is similar toohello one above, except you are creating hello connection from TestVNet5 tooTestVNet1.</span></span> <span data-ttu-id="cebbb-301">Certifique-se de que Olá compartilhado correspondência de chaves e que você se conecte tooSubscription 5.</span><span class="sxs-lookup"><span data-stu-id="cebbb-301">Make sure that hello shared keys match and that you connect tooSubscription 5.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet5ToVNet1 -g TestRG5 --vnet-gateway1 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW -l japaneast --shared-key "eeffgg" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```

## <span data-ttu-id="cebbb-302"><a name="verify"></a>Verifique as conexões de saudação</span><span class="sxs-lookup"><span data-stu-id="cebbb-302"><a name="verify"></a>Verify hello connections</span></span>
[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections v2v cli](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

## <span data-ttu-id="cebbb-303"><a name="faq"></a>Perguntas frequentes sobre Rede Virtual para Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="cebbb-303"><a name="faq"></a>VNet-to-VNet FAQ</span></span>
[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="cebbb-304">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cebbb-304">Next steps</span></span>

* <span data-ttu-id="cebbb-305">Quando a conexão for concluída, você pode adicionar máquinas virtuais tooyour as redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="cebbb-305">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="cebbb-306">Para obter mais informações, consulte Olá [documentação de máquinas virtuais](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="cebbb-306">For more information, see hello [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="cebbb-307">Para obter informações sobre o BGP, consulte Olá [visão geral de BGP](vpn-gateway-bgp-overview.md) e [como tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="cebbb-307">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
