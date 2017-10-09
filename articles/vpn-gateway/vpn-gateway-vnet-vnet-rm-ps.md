---
title: 'Conectar uma rede virtual de tooanother de rede virtual do Azure: PowerShell | Microsoft Docs'
description: Este artigo mostra como conectar redes virtuais em conjunto usando o PowerShell e o Gerenciador de Recursos do Azure.
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
ms.openlocfilehash: 2da30c76867cc3f71d040e63e0dd15d153e15c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-powershell"></a><span data-ttu-id="e42ec-103">Configurar uma conexão gateway de VPN de Vnet pra VNet usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="e42ec-103">Configure a VNet-to-VNet VPN gateway connection using PowerShell</span></span>

<span data-ttu-id="e42ec-104">Este artigo mostra como toocreate uma conexão de gateway VPN entre redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="e42ec-104">This article shows you how toocreate a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="e42ec-105">Olá redes virtuais podem ser Olá mesmas ou em diferentes regiões e de Olá mesmo ou em assinaturas diferentes.</span><span class="sxs-lookup"><span data-stu-id="e42ec-105">hello virtual networks can be in hello same or different regions, and from hello same or different subscriptions.</span></span> <span data-ttu-id="e42ec-106">Quando conexão VNets de assinaturas diferentes, assinaturas de saudação não precisarem toobe associado Olá mesmo locatário do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e42ec-106">When connecting VNets from different subscriptions, hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> 

<span data-ttu-id="e42ec-107">etapas de saudação neste artigo aplicam o modelo de implantação do Gerenciador de recursos de toohello e usam o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e42ec-107">hello steps in this article apply toohello Resource Manager deployment model and use PowerShell.</span></span> <span data-ttu-id="e42ec-108">Você também pode criar essa configuração usando uma ferramenta de implantação diferente ou um modelo de implantação, selecionando uma opção diferente de saudação lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="e42ec-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e42ec-109">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e42ec-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="e42ec-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e42ec-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="e42ec-111">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="e42ec-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="e42ec-112">Portal do Azure (clássico)</span><span class="sxs-lookup"><span data-stu-id="e42ec-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="e42ec-113">Conectar modelos de implantação diferentes – portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e42ec-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="e42ec-114">Conectar modelos de implantação diferentes - PowerShell</span><span class="sxs-lookup"><span data-stu-id="e42ec-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="e42ec-115">Conectar uma rede virtual tooanother VPN (rede virtual a rede) é semelhante tooconnecting uma VNet tooan no site local.</span><span class="sxs-lookup"><span data-stu-id="e42ec-115">Connecting a virtual network tooanother virtual network (VNet-to-VNet) is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="e42ec-116">Ambos os tipos de conectividade usam um gateway VPN tooprovide um túnel seguro usando IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="e42ec-116">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="e42ec-117">Se seus VNets estão em Olá mesma região, talvez você queira tooconsider conectá-los usando o emparelhamento de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="e42ec-117">If your VNets are in hello same region, you may want tooconsider connecting them using VNet Peering.</span></span> <span data-ttu-id="e42ec-118">O emparelhamento Vnet não usa um gateway de VPN.</span><span class="sxs-lookup"><span data-stu-id="e42ec-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="e42ec-119">Para obter mais informações, consulte [Emparelhamento da VNet](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e42ec-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="e42ec-120">Você pode combinar a comunicação de VNet a VNet usando configurações multissite.</span><span class="sxs-lookup"><span data-stu-id="e42ec-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="e42ec-121">Isso permite que você estabeleça topologias de rede que combinem conectividade entre instalações com conectividade de rede intervirtual, como mostrado no diagrama a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="e42ec-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in hello following diagram:</span></span>

![Sobre as conexões](./media/vpn-gateway-vnet-vnet-rm-ps/aboutconnections.png)

### <a name="why-connect-virtual-networks"></a><span data-ttu-id="e42ec-123">Por que conectar redes virtuais?</span><span class="sxs-lookup"><span data-stu-id="e42ec-123">Why connect virtual networks?</span></span>

<span data-ttu-id="e42ec-124">Você talvez queira redes virtuais tooconnect para Olá motivos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e42ec-124">You may want tooconnect virtual networks for hello following reasons:</span></span>

* <span data-ttu-id="e42ec-125">**Redundância geográfica entre regiões e presença geográfica**</span><span class="sxs-lookup"><span data-stu-id="e42ec-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="e42ec-126">Você pode configurar sua própria sincronização ou replicação geográfica com conectividade segura sem passar por pontos de extremidade voltados para a Internet.</span><span class="sxs-lookup"><span data-stu-id="e42ec-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="e42ec-127">Com o Balanceador de Carga e o Gerenciador de Tráfego do Azure você pode configurar a carga de trabalho de alta disponibilidade com redundância geográfica em várias regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="e42ec-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="e42ec-128">Um exemplo importante é tooset backup SQL Always On com grupos de disponibilidade espalhados por várias regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="e42ec-128">One important example is tooset up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="e42ec-129">**Aplicativos multicamadas regionais com limite administrativo ou de isolamento**</span><span class="sxs-lookup"><span data-stu-id="e42ec-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="e42ec-130">Olá na mesma região, você pode configurar aplicativos de várias camadas com várias redes virtuais conectadas devido tooisolation ou requisitos administrativos.</span><span class="sxs-lookup"><span data-stu-id="e42ec-130">Within hello same region, you can set up multi-tier applications with multiple virtual networks connected together due tooisolation or administrative requirements.</span></span>

<span data-ttu-id="e42ec-131">Para obter mais informações sobre conexões de rede virtual a rede, consulte Olá [perguntas Frequentes de VNet para VNet](#faq) final Olá deste artigo.</span><span class="sxs-lookup"><span data-stu-id="e42ec-131">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span>

## <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="e42ec-132">Qual conjunto de etapas devo usar?</span><span class="sxs-lookup"><span data-stu-id="e42ec-132">Which set of steps should I use?</span></span>

<span data-ttu-id="e42ec-133">Neste artigo, você verá dois conjuntos de etapas diferentes.</span><span class="sxs-lookup"><span data-stu-id="e42ec-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="e42ec-134">Um conjunto de etapas para [Olá de VNets que residem na mesma assinatura](#samesub)e outro para [VNets que residem em diferentes assinaturas](#difsub).</span><span class="sxs-lookup"><span data-stu-id="e42ec-134">One set of steps for [VNets that reside in hello same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span> <span data-ttu-id="e42ec-135">Olá diferença importante entre conjuntos de saudação é se você pode criar e configurar todos os recursos de rede e gateway virtuais dentro Olá mesma sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e42ec-135">hello key difference between hello sets is whether you can create and configure all virtual network and gateway resources within hello same PowerShell session.</span></span>

<span data-ttu-id="e42ec-136">Hello etapas neste artigo utilizar variáveis que são declaradas no início de cada seção Olá.</span><span class="sxs-lookup"><span data-stu-id="e42ec-136">hello steps in this article use variables that are declared at hello beginning of each section.</span></span> <span data-ttu-id="e42ec-137">Se você já estiver trabalhando com VNets existentes, modificar configurações de saudação de tooreflect do hello variáveis no seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="e42ec-137">If you already are working with existing VNets, modify hello variables tooreflect hello settings in your own environment.</span></span> <span data-ttu-id="e42ec-138">Se você deseja resolução de nomes para suas redes virtuais, confira [a Resolução de nomes](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="e42ec-138">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

## <span data-ttu-id="e42ec-139"><a name="samesub"></a>Como a tooconnect VNets que estão em Olá mesma assinatura</span><span class="sxs-lookup"><span data-stu-id="e42ec-139"><a name="samesub"></a>How tooconnect VNets that are in hello same subscription</span></span>

![Diagrama de v2v](./media/vpn-gateway-vnet-vnet-rm-ps/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="e42ec-141">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="e42ec-141">Before you begin</span></span>

<span data-ttu-id="e42ec-142">Antes de começar, é necessário a versão mais recente do tooinstall Olá Olá Azure o Gerenciador de recursos de cmdlets do PowerShell, pelo menos 4.0 ou posteriores.</span><span class="sxs-lookup"><span data-stu-id="e42ec-142">Before beginning, you need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets, at least 4.0 or later.</span></span> <span data-ttu-id="e42ec-143">Para obter mais informações sobre como instalar os cmdlets do PowerShell hello, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e42ec-143">For more information about installing hello PowerShell cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="e42ec-144"><a name="Step1"></a>Etapa 1 – Planejar os intervalos de endereços IP</span><span class="sxs-lookup"><span data-stu-id="e42ec-144"><a name="Step1"></a>Step 1 - Plan your IP address ranges</span></span>

<span data-ttu-id="e42ec-145">Olá etapas a seguir, criamos duas redes virtuais junto com suas configurações e sub-redes do respectivos gateway.</span><span class="sxs-lookup"><span data-stu-id="e42ec-145">In hello following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="e42ec-146">Em seguida, criamos uma conexão VPN entre hello duas VNets.</span><span class="sxs-lookup"><span data-stu-id="e42ec-146">We then create a VPN connection between hello two VNets.</span></span> <span data-ttu-id="e42ec-147">É importante tooplan intervalos de endereços IP Olá para sua configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="e42ec-147">It’s important tooplan hello IP address ranges for your network configuration.</span></span> <span data-ttu-id="e42ec-148">Lembre-se de que você deve garantir que nenhum de seus intervalos de VNet ou intervalos de rede local se sobreponham de forma alguma.</span><span class="sxs-lookup"><span data-stu-id="e42ec-148">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="e42ec-149">Nestes exemplos, não incluímos um servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="e42ec-149">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="e42ec-150">Se você deseja resolução de nomes para suas redes virtuais, confira [a Resolução de nomes](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="e42ec-150">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="e42ec-151">Usamos Olá valores nos exemplos Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="e42ec-151">We use hello following values in hello examples:</span></span>

<span data-ttu-id="e42ec-152">**Valores para TestVNet1:**</span><span class="sxs-lookup"><span data-stu-id="e42ec-152">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="e42ec-153">Nome da rede virtual: TestVNet1</span><span class="sxs-lookup"><span data-stu-id="e42ec-153">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="e42ec-154">Grupo de recursos: TestRG1</span><span class="sxs-lookup"><span data-stu-id="e42ec-154">Resource Group: TestRG1</span></span>
* <span data-ttu-id="e42ec-155">Local: Leste dos EUA</span><span class="sxs-lookup"><span data-stu-id="e42ec-155">Location: East US</span></span>
* <span data-ttu-id="e42ec-156">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="e42ec-156">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="e42ec-157">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="e42ec-157">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="e42ec-158">BackEnd: 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="e42ec-158">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="e42ec-159">GatewaySubnet: 10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="e42ec-159">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="e42ec-160">GatewayName: VNet1GW</span><span class="sxs-lookup"><span data-stu-id="e42ec-160">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="e42ec-161">IP público: VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="e42ec-161">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="e42ec-162">VpnType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="e42ec-162">VPNType: RouteBased</span></span>
* <span data-ttu-id="e42ec-163">Connection(1to4): VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="e42ec-163">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="e42ec-164">Connection(1to5): VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="e42ec-164">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="e42ec-165">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="e42ec-165">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="e42ec-166">**Valores para TestVNet4:**</span><span class="sxs-lookup"><span data-stu-id="e42ec-166">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="e42ec-167">Nome da rede virtual: TestVNet4</span><span class="sxs-lookup"><span data-stu-id="e42ec-167">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="e42ec-168">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="e42ec-168">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="e42ec-169">FrontEnd: 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="e42ec-169">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="e42ec-170">BackEnd: 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="e42ec-170">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="e42ec-171">GatewaySubnet: 10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="e42ec-171">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="e42ec-172">Grupo de recursos: TestRG4</span><span class="sxs-lookup"><span data-stu-id="e42ec-172">Resource Group: TestRG4</span></span>
* <span data-ttu-id="e42ec-173">Local: Oeste dos EUA</span><span class="sxs-lookup"><span data-stu-id="e42ec-173">Location: West US</span></span>
* <span data-ttu-id="e42ec-174">GatewayName: VNet4GW</span><span class="sxs-lookup"><span data-stu-id="e42ec-174">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="e42ec-175">IP público: VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="e42ec-175">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="e42ec-176">VpnType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="e42ec-176">VPNType: RouteBased</span></span>
* <span data-ttu-id="e42ec-177">Conexão: VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="e42ec-177">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="e42ec-178">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="e42ec-178">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="e42ec-179"><a name="Step2"></a>Etapa 2: Criar e configurar o TestVNet1</span><span class="sxs-lookup"><span data-stu-id="e42ec-179"><a name="Step2"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="e42ec-180">Declare as variáveis.</span><span class="sxs-lookup"><span data-stu-id="e42ec-180">Declare your variables.</span></span> <span data-ttu-id="e42ec-181">Este exemplo declara variáveis hello usando valores de saudação para este exercício.</span><span class="sxs-lookup"><span data-stu-id="e42ec-181">This example declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="e42ec-182">Na maioria dos casos, você deve substituir os valores hello com seus próprios.</span><span class="sxs-lookup"><span data-stu-id="e42ec-182">In most cases, you should replace hello values with your own.</span></span> <span data-ttu-id="e42ec-183">No entanto, você pode usar essas variáveis, se você estiver executando a saudação etapas toobecome familiarizado com esse tipo de configuração.</span><span class="sxs-lookup"><span data-stu-id="e42ec-183">However, you can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="e42ec-184">Modificar variáveis de saudação se necessário, em seguida, copiar e colá-los em seu console do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e42ec-184">Modify hello variables if needed, then copy and paste them into your PowerShell console.</span></span>

  ```powershell
  $Sub1 = "Replace_With_Your_Subcription_Name"
  $RG1 = "TestRG1"
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
  $GWName1 = "VNet1GW"
  $GWIPName1 = "VNet1GWIP"
  $GWIPconfName1 = "gwipconf1"
  $Connection14 = "VNet1toVNet4"
  $Connection15 = "VNet1toVNet5"
  ```

2. <span data-ttu-id="e42ec-185">Conecte-se a conta de tooyour.</span><span class="sxs-lookup"><span data-stu-id="e42ec-185">Connect tooyour account.</span></span> <span data-ttu-id="e42ec-186">Use Olá toohelp de exemplo que você se conectar a seguir:</span><span class="sxs-lookup"><span data-stu-id="e42ec-186">Use hello following example toohelp you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="e42ec-187">Verificar as assinaturas de saudação para conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="e42ec-187">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="e42ec-188">Especifique que você deseja toouse de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="e42ec-188">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub1
  ```
3. <span data-ttu-id="e42ec-189">Crie um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e42ec-189">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG1 -Location $Location1
  ```
4. <span data-ttu-id="e42ec-190">Crie configurações de sub-rede para TestVNet1 de saudação.</span><span class="sxs-lookup"><span data-stu-id="e42ec-190">Create hello subnet configurations for TestVNet1.</span></span> <span data-ttu-id="e42ec-191">Este exemplo cria uma rede virtual denominada TestVNet1 e três sub-redes, uma chamada GatewaySubnet, outra FrontEnd e outra Backend.</span><span class="sxs-lookup"><span data-stu-id="e42ec-191">This example creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="e42ec-192">Ao substituir valores, é importante você sempre nomear sua sub-rede de gateway especificamente como GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="e42ec-192">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="e42ec-193">Se você usar outro nome, a criação do gateway falhará.</span><span class="sxs-lookup"><span data-stu-id="e42ec-193">If you name it something else, your gateway creation fails.</span></span>

  <span data-ttu-id="e42ec-194">Olá exemplo a seguir usa variáveis de saudação que você definiu anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e42ec-194">hello following example uses hello variables that you set earlier.</span></span> <span data-ttu-id="e42ec-195">Neste exemplo, a sub-rede de gateway de saudação está usando um /27.</span><span class="sxs-lookup"><span data-stu-id="e42ec-195">In this example, hello gateway subnet is using a /27.</span></span> <span data-ttu-id="e42ec-196">Embora seja possível toocreate tão pequenas quanto /29 uma sub-rede do gateway, é recomendável que você crie uma sub-rede maior que inclui mais endereços selecionando pelo menos /28 ou /27.</span><span class="sxs-lookup"><span data-stu-id="e42ec-196">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="e42ec-197">Isso permitirá suficiente endereços tooaccommodate possíveis configurações adicionais que você pode em Olá futuras.</span><span class="sxs-lookup"><span data-stu-id="e42ec-197">This will allow for enough addresses tooaccommodate possible additional configurations that you may want in hello future.</span></span>

  ```powershell
  $fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
  $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
  $gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1
  ```
5. <span data-ttu-id="e42ec-198">Crie a TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="e42ec-198">Create TestVNet1.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
  ```
6. <span data-ttu-id="e42ec-199">Solicite um público endereço toobe toohello alocado gateway IP que você criará para sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="e42ec-199">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="e42ec-200">Observe que Olá AllocationMethod é dinâmico.</span><span class="sxs-lookup"><span data-stu-id="e42ec-200">Notice that hello AllocationMethod is Dynamic.</span></span> <span data-ttu-id="e42ec-201">Não é possível especificar o endereço IP de saudação que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="e42ec-201">You cannot specify hello IP address that you want toouse.</span></span> <span data-ttu-id="e42ec-202">É gateway tooyour alocada dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="e42ec-202">It's dynamically allocated tooyour gateway.</span></span> 

  ```powershell
  $gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="e42ec-203">Crie a configuração do gateway hello.</span><span class="sxs-lookup"><span data-stu-id="e42ec-203">Create hello gateway configuration.</span></span> <span data-ttu-id="e42ec-204">configuração do gateway Olá define sub-rede hello e toouse de endereço IP público hello.</span><span class="sxs-lookup"><span data-stu-id="e42ec-204">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="e42ec-205">Use toocreate do exemplo hello sua configuração de gateway.</span><span class="sxs-lookup"><span data-stu-id="e42ec-205">Use hello example toocreate your gateway configuration.</span></span>

  ```powershell
  $vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
  $subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
  $gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 `
  -Subnet $subnet1 -PublicIpAddress $gwpip1
  ```
8. <span data-ttu-id="e42ec-206">Crie gateway Olá para TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="e42ec-206">Create hello gateway for TestVNet1.</span></span> <span data-ttu-id="e42ec-207">Nesta etapa, você pode criar o gateway de rede virtual Olá para sua TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="e42ec-207">In this step, you create hello virtual network gateway for your TestVNet1.</span></span> <span data-ttu-id="e42ec-208">As configurações de rede virtual com rede virtual exigem um VpnType RouteBased.</span><span class="sxs-lookup"><span data-stu-id="e42ec-208">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="e42ec-209">Criar um gateway pode levar até 45 minutos ou mais, dependendo da SKU do gateway Olá selecionado.</span><span class="sxs-lookup"><span data-stu-id="e42ec-209">Creating a gateway can often take 45 minutes or more, depending on hello selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 `
  -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-3---create-and-configure-testvnet4"></a><span data-ttu-id="e42ec-210">Etapa 3: criar e configurar TestVNet4</span><span class="sxs-lookup"><span data-stu-id="e42ec-210">Step 3 - Create and configure TestVNet4</span></span>

<span data-ttu-id="e42ec-211">Depois de configurar TestVNet1, crie TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="e42ec-211">Once you've configured TestVNet1, create TestVNet4.</span></span> <span data-ttu-id="e42ec-212">Siga as etapas de saudação abaixo, substituindo valores hello com seu próprio quando necessário.</span><span class="sxs-lookup"><span data-stu-id="e42ec-212">Follow hello steps below, replacing hello values with your own when needed.</span></span> <span data-ttu-id="e42ec-213">Esta etapa pode ser feita em Olá mesma sessão do PowerShell porque ele está em Olá mesmo assinatura.</span><span class="sxs-lookup"><span data-stu-id="e42ec-213">This step can be done within hello same PowerShell session because it is in hello same subscription.</span></span>

1. <span data-ttu-id="e42ec-214">Declare as variáveis.</span><span class="sxs-lookup"><span data-stu-id="e42ec-214">Declare your variables.</span></span> <span data-ttu-id="e42ec-215">Ser tooreplace se valores Olá Olá aqueles que você deseja toouse para sua configuração.</span><span class="sxs-lookup"><span data-stu-id="e42ec-215">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

  ```powershell
  $RG4 = "TestRG4"
  $Location4 = "West US"
  $VnetName4 = "TestVNet4"
  $FESubName4 = "FrontEnd"
  $BESubName4 = "Backend"
  $GWSubName4 = "GatewaySubnet"
  $VnetPrefix41 = "10.41.0.0/16"
  $VnetPrefix42 = "10.42.0.0/16"
  $FESubPrefix4 = "10.41.0.0/24"
  $BESubPrefix4 = "10.42.0.0/24"
  $GWSubPrefix4 = "10.42.255.0/27"
  $GWName4 = "VNet4GW"
  $GWIPName4 = "VNet4GWIP"
  $GWIPconfName4 = "gwipconf4"
  $Connection41 = "VNet4toVNet1"
  ```
2. <span data-ttu-id="e42ec-216">Crie um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e42ec-216">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG4 -Location $Location4
  ```
3. <span data-ttu-id="e42ec-217">Crie configurações de sub-rede para TestVNet4 de saudação.</span><span class="sxs-lookup"><span data-stu-id="e42ec-217">Create hello subnet configurations for TestVNet4.</span></span>

  ```powershell
  $fesub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName4 -AddressPrefix $FESubPrefix4
  $besub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName4 -AddressPrefix $BESubPrefix4
  $gwsub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName4 -AddressPrefix $GWSubPrefix4
  ```
4. <span data-ttu-id="e42ec-218">Crie a TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="e42ec-218">Create TestVNet4.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AddressPrefix $VnetPrefix41,$VnetPrefix42 -Subnet $fesub4,$besub4,$gwsub4
  ```
5. <span data-ttu-id="e42ec-219">Solicite um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="e42ec-219">Request a public IP address.</span></span>

  ```powershell
  $gwpip4 = New-AzureRmPublicIpAddress -Name $GWIPName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AllocationMethod Dynamic
  ```
6. <span data-ttu-id="e42ec-220">Crie a configuração do gateway hello.</span><span class="sxs-lookup"><span data-stu-id="e42ec-220">Create hello gateway configuration.</span></span>

  ```powershell
  $vnet4 = Get-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4
  $subnet4 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet4
  $gwipconf4 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName4 -Subnet $subnet4 -PublicIpAddress $gwpip4
  ```
7. <span data-ttu-id="e42ec-221">Crie hello TestVNet4 gateway.</span><span class="sxs-lookup"><span data-stu-id="e42ec-221">Create hello TestVNet4 gateway.</span></span> <span data-ttu-id="e42ec-222">Criar um gateway pode levar até 45 minutos ou mais, dependendo da SKU do gateway Olá selecionado.</span><span class="sxs-lookup"><span data-stu-id="e42ec-222">Creating a gateway can often take 45 minutes or more, depending on hello selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4 `
  -Location $Location4 -IpConfigurations $gwipconf4 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-4---create-hello-connections"></a><span data-ttu-id="e42ec-223">Etapa 4 - criar conexões Olá</span><span class="sxs-lookup"><span data-stu-id="e42ec-223">Step 4 - Create hello connections</span></span>

1. <span data-ttu-id="e42ec-224">Obter ambos os gateways de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="e42ec-224">Get both virtual network gateways.</span></span> <span data-ttu-id="e42ec-225">Se ambos os gateways Olá Olá mesma assinatura, como estão no exemplo hello, você pode concluir esta etapa no hello mesma sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e42ec-225">If both of hello gateways are in hello same subscription, as they are in hello example, you can complete this step in hello same PowerShell session.</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  $vnet4gw = Get-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4
  ```
2. <span data-ttu-id="e42ec-226">Crie conexão de tooTestVNet4 TestVNet1 hello.</span><span class="sxs-lookup"><span data-stu-id="e42ec-226">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="e42ec-227">Nesta etapa, você pode criar conexão de saudação do TestVNet1 tooTestVNet4.</span><span class="sxs-lookup"><span data-stu-id="e42ec-227">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="e42ec-228">Você verá uma chave compartilhada referenciada nos exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e42ec-228">You'll see a shared key referenced in hello examples.</span></span> <span data-ttu-id="e42ec-229">Você pode usar seus próprios valores para a chave compartilhada hello.</span><span class="sxs-lookup"><span data-stu-id="e42ec-229">You can use your own values for hello shared key.</span></span> <span data-ttu-id="e42ec-230">Olá importante é chave compartilhada Olá deve corresponder para ambas as conexões.</span><span class="sxs-lookup"><span data-stu-id="e42ec-230">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="e42ec-231">Criar uma conexão pode demorar um pouco ao toocomplete.</span><span class="sxs-lookup"><span data-stu-id="e42ec-231">Creating a connection can take a short while toocomplete.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection14 -ResourceGroupName $RG1 `
  -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet4gw -Location $Location1 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
3. <span data-ttu-id="e42ec-232">Crie conexão de tooTestVNet1 TestVNet4 hello.</span><span class="sxs-lookup"><span data-stu-id="e42ec-232">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="e42ec-233">Esta etapa é semelhante toohello mostrado acima, exceto que você está criando a conexão de saudação da TestVNet4 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="e42ec-233">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="e42ec-234">Certifique-se de saudação compartilhada chaves correspondentes.</span><span class="sxs-lookup"><span data-stu-id="e42ec-234">Make sure hello shared keys match.</span></span> <span data-ttu-id="e42ec-235">conexão Olá será estabelecida após alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="e42ec-235">hello connection will be established after a few minutes.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection41 -ResourceGroupName $RG4 `
  -VirtualNetworkGateway1 $vnet4gw -VirtualNetworkGateway2 $vnet1gw -Location $Location4 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="e42ec-236">Verifique a conexão.</span><span class="sxs-lookup"><span data-stu-id="e42ec-236">Verify your connection.</span></span> <span data-ttu-id="e42ec-237">Consulte a seção Olá [como tooverify sua conexão](#verify).</span><span class="sxs-lookup"><span data-stu-id="e42ec-237">See hello section [How tooverify your connection](#verify).</span></span>

## <span data-ttu-id="e42ec-238"><a name="difsub"></a>Como tooconnect VNets que estão em diferentes assinaturas</span><span class="sxs-lookup"><span data-stu-id="e42ec-238"><a name="difsub"></a>How tooconnect VNets that are in different subscriptions</span></span>

![Diagrama de v2v](./media/vpn-gateway-vnet-vnet-rm-ps/v2vdiffsub.png)

<span data-ttu-id="e42ec-240">Nesse cenário, conectamos TestVNet1 e TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="e42ec-240">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="e42ec-241">TestVNet1 e TestVNet5 residem em uma assinatura diferente.</span><span class="sxs-lookup"><span data-stu-id="e42ec-241">TestVNet1 and TestVNet5 reside in a different subscription.</span></span> <span data-ttu-id="e42ec-242">Olá assinaturas não precisem toobe associado Olá mesmo locatário do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e42ec-242">hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> <span data-ttu-id="e42ec-243">diferença de saudação entre essas etapas e o conjunto anterior de saudação é que algumas das etapas de configuração de saudação necessário toobe executada em uma sessão separada do PowerShell no contexto de saudação da assinatura segundo hello.</span><span class="sxs-lookup"><span data-stu-id="e42ec-243">hello difference between these steps and hello previous set is that some of hello configuration steps need toobe performed in a separate PowerShell session in hello context of hello second subscription.</span></span> <span data-ttu-id="e42ec-244">Especialmente quando assinaturas de saudação dois pertencem toodifferent organizações.</span><span class="sxs-lookup"><span data-stu-id="e42ec-244">Especially when hello two subscriptions belong toodifferent organizations.</span></span>

### <a name="step-5---create-and-configure-testvnet1"></a><span data-ttu-id="e42ec-245">Etapa 5: criar e configurar o TestVNet1</span><span class="sxs-lookup"><span data-stu-id="e42ec-245">Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="e42ec-246">Você deve concluir [etapa 1](#Step1) e [etapa 2](#Step2) de saudação anterior seção toocreate e configurar TestVNet1 e hello Gateway VPN para TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="e42ec-246">You must complete [Step 1](#Step1) and [Step 2](#Step2) from hello previous section toocreate and configure TestVNet1 and hello VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="e42ec-247">Para essa configuração, você não é necessário toocreate TestVNet4 da seção anterior do hello, embora se você criá-lo, ele não está em conflito com estas etapas.</span><span class="sxs-lookup"><span data-stu-id="e42ec-247">For this configuration, you are not required toocreate TestVNet4 from hello previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="e42ec-248">Depois de concluir a etapa 1 e 2, continue com a etapa 6 toocreate TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="e42ec-248">Once you complete Step 1 and Step 2, continue with Step 6 toocreate TestVNet5.</span></span> 

### <a name="step-6---verify-hello-ip-address-ranges"></a><span data-ttu-id="e42ec-249">Etapa 6 - Verifique se os intervalos de endereços IP Olá</span><span class="sxs-lookup"><span data-stu-id="e42ec-249">Step 6 - Verify hello IP address ranges</span></span>

<span data-ttu-id="e42ec-250">É importante toomake-se de que o espaço de endereço IP de saudação do hello nova rede virtual, TestVNet5, não coincide com nenhum dos seus intervalos de VNet ou intervalos de gateway de rede local.</span><span class="sxs-lookup"><span data-stu-id="e42ec-250">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet5, does not overlap with any of your VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="e42ec-251">Neste exemplo, redes virtuais Olá podem pertencer toodifferent organizações.</span><span class="sxs-lookup"><span data-stu-id="e42ec-251">In this example, hello virtual networks may belong toodifferent organizations.</span></span> <span data-ttu-id="e42ec-252">Para este exercício, você pode usar Olá Olá TestVNet5 valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="e42ec-252">For this exercise, you can use hello following values for hello TestVNet5:</span></span>

<span data-ttu-id="e42ec-253">**Valores para TestVNet5:**</span><span class="sxs-lookup"><span data-stu-id="e42ec-253">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="e42ec-254">Nome da rede virtual: TestVNet5</span><span class="sxs-lookup"><span data-stu-id="e42ec-254">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="e42ec-255">Grupo de recursos: TestRG5</span><span class="sxs-lookup"><span data-stu-id="e42ec-255">Resource Group: TestRG5</span></span>
* <span data-ttu-id="e42ec-256">Local: Leste do Japão</span><span class="sxs-lookup"><span data-stu-id="e42ec-256">Location: Japan East</span></span>
* <span data-ttu-id="e42ec-257">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="e42ec-257">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="e42ec-258">FrontEnd: 10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="e42ec-258">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="e42ec-259">BackEnd: 10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="e42ec-259">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="e42ec-260">GatewaySubnet: 10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="e42ec-260">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="e42ec-261">GatewayName: VNet5GW</span><span class="sxs-lookup"><span data-stu-id="e42ec-261">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="e42ec-262">IP público: VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="e42ec-262">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="e42ec-263">VpnType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="e42ec-263">VPNType: RouteBased</span></span>
* <span data-ttu-id="e42ec-264">Connection: VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="e42ec-264">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="e42ec-265">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="e42ec-265">ConnectionType: VNet2VNet</span></span>

### <a name="step-7---create-and-configure-testvnet5"></a><span data-ttu-id="e42ec-266">Etapa 7: criar e configurar TestVNet5</span><span class="sxs-lookup"><span data-stu-id="e42ec-266">Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="e42ec-267">Esta etapa deve ser feita no contexto de saudação da nova assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="e42ec-267">This step must be done in hello context of hello new subscription.</span></span> <span data-ttu-id="e42ec-268">Esta parte pode ser executada pelo administrador Olá em uma organização diferente que possui assinatura hello.</span><span class="sxs-lookup"><span data-stu-id="e42ec-268">This part may be performed by hello administrator in a different organization that owns hello subscription.</span></span>

1. <span data-ttu-id="e42ec-269">Declare as variáveis.</span><span class="sxs-lookup"><span data-stu-id="e42ec-269">Declare your variables.</span></span> <span data-ttu-id="e42ec-270">Ser tooreplace se valores Olá Olá aqueles que você deseja toouse para sua configuração.</span><span class="sxs-lookup"><span data-stu-id="e42ec-270">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

  ```powershell
  $Sub5 = "Replace_With_the_New_Subcription_Name"
  $RG5 = "TestRG5"
  $Location5 = "Japan East"
  $VnetName5 = "TestVNet5"
  $FESubName5 = "FrontEnd"
  $BESubName5 = "Backend"
  $GWSubName5 = "GatewaySubnet"
  $VnetPrefix51 = "10.51.0.0/16"
  $VnetPrefix52 = "10.52.0.0/16"
  $FESubPrefix5 = "10.51.0.0/24"
  $BESubPrefix5 = "10.52.0.0/24"
  $GWSubPrefix5 = "10.52.255.0/27"
  $GWName5 = "VNet5GW"
  $GWIPName5 = "VNet5GWIP"
  $GWIPconfName5 = "gwipconf5"
  $Connection51 = "VNet5toVNet1"
  ```
2. <span data-ttu-id="e42ec-271">Conecte-se toosubscription 5.</span><span class="sxs-lookup"><span data-stu-id="e42ec-271">Connect toosubscription 5.</span></span> <span data-ttu-id="e42ec-272">Abra o console do PowerShell e conecte-se a conta de tooyour.</span><span class="sxs-lookup"><span data-stu-id="e42ec-272">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="e42ec-273">Use Olá toohelp de exemplo que você se conectar a seguir:</span><span class="sxs-lookup"><span data-stu-id="e42ec-273">Use hello following sample toohelp you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="e42ec-274">Verificar as assinaturas de saudação para conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="e42ec-274">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="e42ec-275">Especifique que você deseja toouse de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="e42ec-275">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub5
  ```
3. <span data-ttu-id="e42ec-276">Crie um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e42ec-276">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG5 -Location $Location5
  ```
4. <span data-ttu-id="e42ec-277">Crie configurações de sub-rede para TestVNet5 de saudação.</span><span class="sxs-lookup"><span data-stu-id="e42ec-277">Create hello subnet configurations for TestVNet5.</span></span>

  ```powershell
  $fesub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName5 -AddressPrefix $FESubPrefix5
  $besub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName5 -AddressPrefix $BESubPrefix5
  $gwsub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName5 -AddressPrefix $GWSubPrefix5
  ```
5. <span data-ttu-id="e42ec-278">Crie a TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="e42ec-278">Create TestVNet5.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5 -Location $Location5 `
  -AddressPrefix $VnetPrefix51,$VnetPrefix52 -Subnet $fesub5,$besub5,$gwsub5
  ```
6. <span data-ttu-id="e42ec-279">Solicite um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="e42ec-279">Request a public IP address.</span></span>

  ```powershell
  $gwpip5 = New-AzureRmPublicIpAddress -Name $GWIPName5 -ResourceGroupName $RG5 `
  -Location $Location5 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="e42ec-280">Crie a configuração do gateway hello.</span><span class="sxs-lookup"><span data-stu-id="e42ec-280">Create hello gateway configuration.</span></span>

  ```powershell
  $vnet5 = Get-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5
  $subnet5  = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet5
  $gwipconf5 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName5 -Subnet $subnet5 -PublicIpAddress $gwpip5
  ```
8. <span data-ttu-id="e42ec-281">Crie hello TestVNet5 gateway.</span><span class="sxs-lookup"><span data-stu-id="e42ec-281">Create hello TestVNet5 gateway.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5 -Location $Location5 `
  -IpConfigurations $gwipconf5 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-8---create-hello-connections"></a><span data-ttu-id="e42ec-282">Etapa 8 — criar conexões Olá</span><span class="sxs-lookup"><span data-stu-id="e42ec-282">Step 8 - Create hello connections</span></span>

<span data-ttu-id="e42ec-283">Neste exemplo, como gateways Olá estão em assinaturas diferentes do hello, você dividiremos esta etapa em duas sessões do PowerShell marcadas como [1 assinatura] e [5 assinatura].</span><span class="sxs-lookup"><span data-stu-id="e42ec-283">In this example, because hello gateways are in hello different subscriptions, we've split this step into two PowerShell sessions marked as [Subscription 1] and [Subscription 5].</span></span>

1. <span data-ttu-id="e42ec-284">**[Assinatura 1]**  Obter gateway de rede virtual Olá para 1 de assinatura.</span><span class="sxs-lookup"><span data-stu-id="e42ec-284">**[Subscription 1]** Get hello virtual network gateway for Subscription 1.</span></span> <span data-ttu-id="e42ec-285">Logon e se conectar tooSubscription 1 antes de executar o exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="e42ec-285">Log in and connect tooSubscription 1 before running hello following example:</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  ```

  <span data-ttu-id="e42ec-286">Copiar saída Olá Olá elementos a seguir e enviar esses administrador toohello de 5 de assinatura por email ou outro método.</span><span class="sxs-lookup"><span data-stu-id="e42ec-286">Copy hello output of hello following elements and send these toohello administrator of Subscription 5 via email or another method.</span></span>

  ```powershell
  $vnet1gw.Name
  $vnet1gw.Id
  ```

  <span data-ttu-id="e42ec-287">Esses dois elementos terão valores toohello semelhante a saída de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="e42ec-287">These two elements will have values similar toohello following example output:</span></span>

  ```
  PS D:\> $vnet1gw.Name
  VNet1GW
  PS D:\> $vnet1gw.Id
  /subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroupsTestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```
2. <span data-ttu-id="e42ec-288">**[Assinatura 5]**  Obter gateway de rede virtual Olá para 5 de assinatura.</span><span class="sxs-lookup"><span data-stu-id="e42ec-288">**[Subscription 5]** Get hello virtual network gateway for Subscription 5.</span></span> <span data-ttu-id="e42ec-289">Logon e se conectar tooSubscription 5 antes de executar o exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="e42ec-289">Log in and connect tooSubscription 5 before running hello following example:</span></span>

  ```powershell
  $vnet5gw = Get-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5
  ```

  <span data-ttu-id="e42ec-290">Copiar saída Olá Olá elementos a seguir e enviar esses administrador toohello 1 assinatura via email ou outro método.</span><span class="sxs-lookup"><span data-stu-id="e42ec-290">Copy hello output of hello following elements and send these toohello administrator of Subscription 1 via email or another method.</span></span>

  ```powershell
  $vnet5gw.Name
  $vnet5gw.Id
  ```

  <span data-ttu-id="e42ec-291">Esses dois elementos terão valores toohello semelhante a saída de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="e42ec-291">These two elements will have values similar toohello following example output:</span></span>

  ```
  PS C:\> $vnet5gw.Name
  VNet5GW
  PS C:\> $vnet5gw.Id
  /subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```
3. <span data-ttu-id="e42ec-292">**[Assinatura 1]**  Criar conexão Olá TestVNet1 tooTestVNet5.</span><span class="sxs-lookup"><span data-stu-id="e42ec-292">**[Subscription 1]** Create hello TestVNet1 tooTestVNet5 connection.</span></span> <span data-ttu-id="e42ec-293">Nesta etapa, você pode criar conexão de saudação do TestVNet1 tooTestVNet5.</span><span class="sxs-lookup"><span data-stu-id="e42ec-293">In this step, you create hello connection from TestVNet1 tooTestVNet5.</span></span> <span data-ttu-id="e42ec-294">diferença de saudação aqui é que vnet5gw $ não podem ser obtidos diretamente, porque ele está em uma assinatura diferente.</span><span class="sxs-lookup"><span data-stu-id="e42ec-294">hello difference here is that $vnet5gw cannot be obtained directly because it is in a different subscription.</span></span> <span data-ttu-id="e42ec-295">Você precisará toocreate um novo objeto do PowerShell com valores hello comunicados de 1 de assinatura de etapas de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="e42ec-295">You will need toocreate a new PowerShell object with hello values communicated from Subscription 1 in hello steps above.</span></span> <span data-ttu-id="e42ec-296">Use o exemplo hello abaixo.</span><span class="sxs-lookup"><span data-stu-id="e42ec-296">Use hello example below.</span></span> <span data-ttu-id="e42ec-297">Substitua seus próprios valores hello nome, Id e uma chave compartilhada.</span><span class="sxs-lookup"><span data-stu-id="e42ec-297">Replace hello Name, Id, and shared key with your own values.</span></span> <span data-ttu-id="e42ec-298">Olá importante é chave compartilhada Olá deve corresponder para ambas as conexões.</span><span class="sxs-lookup"><span data-stu-id="e42ec-298">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="e42ec-299">Criar uma conexão pode demorar um pouco ao toocomplete.</span><span class="sxs-lookup"><span data-stu-id="e42ec-299">Creating a connection can take a short while toocomplete.</span></span>

  <span data-ttu-id="e42ec-300">Conecte-se tooSubscription 1 antes de executar o exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="e42ec-300">Connect tooSubscription 1 before running hello following example:</span></span>

  ```powershell
  $vnet5gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet5gw.Name = "VNet5GW"
  $vnet5gw.Id   = "/subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW"
  $Connection15 = "VNet1toVNet5"
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet5gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="e42ec-301">**[Assinatura 5]**  Criar conexão Olá TestVNet5 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="e42ec-301">**[Subscription 5]** Create hello TestVNet5 tooTestVNet1 connection.</span></span> <span data-ttu-id="e42ec-302">Esta etapa é semelhante toohello mostrado acima, exceto que você está criando a conexão de saudação da TestVNet5 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="e42ec-302">This step is similar toohello one above, except you are creating hello connection from TestVNet5 tooTestVNet1.</span></span> <span data-ttu-id="e42ec-303">Olá mesmo processo de criação de um objeto do PowerShell com base nos valores hello obtidos 1 assinatura se aplica aqui também.</span><span class="sxs-lookup"><span data-stu-id="e42ec-303">hello same process of creating a PowerShell object based on hello values obtained from Subscription 1 applies here as well.</span></span> <span data-ttu-id="e42ec-304">Nesta etapa, certifique-se de que correspondem chaves Olá compartilhado.</span><span class="sxs-lookup"><span data-stu-id="e42ec-304">In this step, be sure that hello shared keys match.</span></span>

  <span data-ttu-id="e42ec-305">Conecte-se tooSubscription 5 antes de executar o exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="e42ec-305">Connect tooSubscription 5 before running hello following example:</span></span>

  ```powershell
  $vnet1gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet1gw.Name = "VNet1GW"
  $vnet1gw.Id = "/subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW "
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection51 -ResourceGroupName $RG5 -VirtualNetworkGateway1 $vnet5gw -VirtualNetworkGateway2 $vnet1gw -Location $Location5 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```

## <span data-ttu-id="e42ec-306"><a name="verify"></a>Como tooverify uma conexão</span><span class="sxs-lookup"><span data-stu-id="e42ec-306"><a name="verify"></a>How tooverify a connection</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections powershell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="e42ec-307"><a name="faq"></a>Perguntas frequentes sobre Rede Virtual para Rede Virtual</span><span class="sxs-lookup"><span data-stu-id="e42ec-307"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="e42ec-308">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e42ec-308">Next steps</span></span>

* <span data-ttu-id="e42ec-309">Quando a conexão for concluída, você pode adicionar máquinas virtuais tooyour as redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="e42ec-309">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="e42ec-310">Consulte Olá [documentação de máquinas virtuais](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="e42ec-310">See hello [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) for more information.</span></span>
* <span data-ttu-id="e42ec-311">Para obter informações sobre o BGP, consulte Olá [visão geral de BGP](vpn-gateway-bgp-overview.md) e [como tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e42ec-311">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
