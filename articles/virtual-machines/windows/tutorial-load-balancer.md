---
title: "aaaHow tooload equilibrar máquinas virtuais do Windows no Azure | Microsoft Docs"
description: "Saiba como toouse hello Azure carregar balanceador toocreate um aplicativo altamente disponível e seguro entre três máquinas virtuais do Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: bfbd6a24e90a33e60d7d4f7b0c471af5d4e71f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-windows-virtual-machines-in-azure-toocreate-a-highly-available-application"></a><span data-ttu-id="d10b5-103">Como o tooload equilibrar a máquinas virtuais do Windows no Azure toocreate um aplicativo altamente disponível</span><span class="sxs-lookup"><span data-stu-id="d10b5-103">How tooload balance Windows virtual machines in Azure toocreate a highly available application</span></span>
<span data-ttu-id="d10b5-104">O balanceamento de carga fornece um nível mais alto de disponibilidade, distribuindo as solicitações de entrada em várias máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="d10b5-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="d10b5-105">Neste tutorial, você aprenderá sobre Olá diferentes componentes do balanceador de carga do Azure Olá que distribuir o tráfego e fornecem alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="d10b5-105">In this tutorial, you learn about hello different components of hello Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="d10b5-106">Você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="d10b5-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d10b5-107">Criar um balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="d10b5-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="d10b5-108">Criar uma investigação de integridade do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="d10b5-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="d10b5-109">Criar regras de tráfego para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="d10b5-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="d10b5-110">Use Olá extensão de Script personalizado toocreate um site IIS básico</span><span class="sxs-lookup"><span data-stu-id="d10b5-110">Use hello Custom Script Extension toocreate a basic IIS site</span></span>
> * <span data-ttu-id="d10b5-111">Criar máquinas virtuais e anexar tooa balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="d10b5-111">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="d10b5-112">Exibir um balanceador de carga em ação</span><span class="sxs-lookup"><span data-stu-id="d10b5-112">View a load balancer in action</span></span>
> * <span data-ttu-id="d10b5-113">Adicionar e remover as VMs de um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="d10b5-113">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="d10b5-114">Este tutorial requer hello Azure PowerShell versão 3.6 ou posterior do módulo.</span><span class="sxs-lookup"><span data-stu-id="d10b5-114">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="d10b5-115">Executar ` Get-Module -ListAvailable AzureRM` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="d10b5-115">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="d10b5-116">Se você precisar tooupgrade, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="d10b5-116">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="azure-load-balancer-overview"></a><span data-ttu-id="d10b5-117">Visão geral do Balanceador de Carga do Azure</span><span class="sxs-lookup"><span data-stu-id="d10b5-117">Azure load balancer overview</span></span>
<span data-ttu-id="d10b5-118">Um Azure Load Balancer é um balanceador de carga de Camada 4 (TCP, UDP) que fornece alta disponibilidade distribuindo o tráfego de entrada entre VMs íntegros.</span><span class="sxs-lookup"><span data-stu-id="d10b5-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="d10b5-119">Um teste de integridade do balanceador de carga monitora uma determinada porta em cada VM e só distribui o tráfego tooan operacional VM.</span><span class="sxs-lookup"><span data-stu-id="d10b5-119">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

<span data-ttu-id="d10b5-120">Você define uma configuração de IP de front-end que contém um ou mais endereços IP públicos.</span><span class="sxs-lookup"><span data-stu-id="d10b5-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="d10b5-121">Essa configuração de IP de front-end permite que seu toobe de aplicativos e o balanceador de carga acessível pela Internet da saudação.</span><span class="sxs-lookup"><span data-stu-id="d10b5-121">This front-end IP configuration allows your load balancer and applications toobe accessible over hello Internet.</span></span> 

<span data-ttu-id="d10b5-122">Máquinas virtuais conectar-se usando sua placa de interface de rede virtual (NIC) de Balanceador de carga tooa.</span><span class="sxs-lookup"><span data-stu-id="d10b5-122">Virtual machines connect tooa load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="d10b5-123">tráfego de toodistribute toohello VMs, um pool de endereços de back-end contém endereços IP Olá Olá virtual (NICs) toohello conectados do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="d10b5-123">toodistribute traffic toohello VMs, a back-end address pool contains hello IP addresses of hello virtual (NICs) connected toohello load balancer.</span></span>

<span data-ttu-id="d10b5-124">fluxo de saudação toocontrol de tráfego, você definir regras de Balanceador de carga para portas e protocolos que mapeiam tooyour VMs específicos.</span><span class="sxs-lookup"><span data-stu-id="d10b5-124">toocontrol hello flow of traffic, you define load balancer rules for specific ports and protocols that map tooyour VMs.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="d10b5-125">Criar o balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="d10b5-125">Create Azure load balancer</span></span>
<span data-ttu-id="d10b5-126">Esta seção fornece detalhes sobre como você pode criar e configurar cada componente de saudação do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="d10b5-126">This section details how you can create and configure each component of hello load balancer.</span></span> <span data-ttu-id="d10b5-127">Antes de criar seu balanceador de carga, crie um grupo de recursos com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="d10b5-127">Before you can create your load balancer, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="d10b5-128">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroupLoadBalancer* em Olá *EastUS* local:</span><span class="sxs-lookup"><span data-stu-id="d10b5-128">hello following example creates a resource group named *myResourceGroupLoadBalancer* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="d10b5-129">Criar um endereço IP público</span><span class="sxs-lookup"><span data-stu-id="d10b5-129">Create a public IP address</span></span>
<span data-ttu-id="d10b5-130">tooaccess Olá de seu aplicativo na Internet, é necessário um endereço IP público Olá balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="d10b5-130">tooaccess your app on hello Internet, you need a public IP address for hello load balancer.</span></span> <span data-ttu-id="d10b5-131">Crie um endereço IP público com [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="d10b5-131">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="d10b5-132">Olá, exemplo a seguir cria um endereço IP público denominado *myPublicIP* em Olá *myResourceGroupLoadBalancer* grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="d10b5-132">hello following example creates a public IP address named *myPublicIP* in hello *myResourceGroupLoadBalancer* resource group:</span></span>

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="d10b5-133">Criar um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="d10b5-133">Create a load balancer</span></span>
<span data-ttu-id="d10b5-134">Crie um endereço IP de front-end com [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="d10b5-134">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="d10b5-135">Olá, exemplo a seguir cria um endereço IP de front-end denominado *myFrontEndPool*:</span><span class="sxs-lookup"><span data-stu-id="d10b5-135">hello following example creates a frontend IP address named *myFrontEndPool*:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

<span data-ttu-id="d10b5-136">Crie um pool de endereços de back-end com [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span><span class="sxs-lookup"><span data-stu-id="d10b5-136">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="d10b5-137">Olá, exemplo a seguir cria um pool de endereços de back-end denominado *myBackEndPool*:</span><span class="sxs-lookup"><span data-stu-id="d10b5-137">hello following example creates a backend address pool named *myBackEndPool*:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="d10b5-138">Agora, crie o balanceador de carga Olá com [AzureRmLoadBalancer novo](/powershell/module/azurerm.network/new-azurermloadbalancer).</span><span class="sxs-lookup"><span data-stu-id="d10b5-138">Now, create hello load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="d10b5-139">Olá, exemplo a seguir cria um balanceador de carga denominado *myLoadBalancer* usando Olá *myPublicIP* endereço:</span><span class="sxs-lookup"><span data-stu-id="d10b5-139">hello following example creates a load balancer named *myLoadBalancer* using hello *myPublicIP* address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a><span data-ttu-id="d10b5-140">Criar uma investigação de integridade</span><span class="sxs-lookup"><span data-stu-id="d10b5-140">Create a health probe</span></span>
<span data-ttu-id="d10b5-141">tooallow Olá balanceador toomonitor Olá status de carga do seu aplicativo, você usar uma investigação de integridade.</span><span class="sxs-lookup"><span data-stu-id="d10b5-141">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="d10b5-142">investigação de integridade Olá dinamicamente adiciona ou remove as VMs de rotação do balanceador de carga de saudação com base em suas verificações de toohealth de resposta.</span><span class="sxs-lookup"><span data-stu-id="d10b5-142">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="d10b5-143">Por padrão, uma máquina virtual é removida da distribuição de Balanceador de carga Olá após duas falhas consecutivas em intervalos de 15 segundos.</span><span class="sxs-lookup"><span data-stu-id="d10b5-143">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="d10b5-144">Crie uma investigação de integridade com base em um protocolo ou página de verificação de integridade específica ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d10b5-144">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="d10b5-145">saudação de exemplo a seguir cria uma investigação TCP.</span><span class="sxs-lookup"><span data-stu-id="d10b5-145">hello following example creates a TCP probe.</span></span> <span data-ttu-id="d10b5-146">Você também pode criar investigações de HTTP personalizadas para obter verificações de integridade mais refinadas.</span><span class="sxs-lookup"><span data-stu-id="d10b5-146">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="d10b5-147">Ao usar uma investigação personalizada de HTTP, você deve criar página de verificação de integridade hello, tais como *healthcheck.aspx*.</span><span class="sxs-lookup"><span data-stu-id="d10b5-147">When using a custom HTTP probe, you must create hello health check page, such as *healthcheck.aspx*.</span></span> <span data-ttu-id="d10b5-148">investigação de saudação deve retornar um **HTTP 200 Okey** resposta para Olá carga balanceador tookeep Olá host rotação.</span><span class="sxs-lookup"><span data-stu-id="d10b5-148">hello probe must return an **HTTP 200 OK** response for hello load balancer tookeep hello host in rotation.</span></span>

<span data-ttu-id="d10b5-149">toocreate uma investigação de integridade TCP, use [AzureRmLoadBalancerProbeConfig adicionar](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span><span class="sxs-lookup"><span data-stu-id="d10b5-149">toocreate a TCP health probe, you use [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="d10b5-150">Olá, exemplo a seguir cria um teste de integridade chamado *myHealthProbe* que monitora a cada VM:</span><span class="sxs-lookup"><span data-stu-id="d10b5-150">hello following example creates a health probe named *myHealthProbe* that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

<span data-ttu-id="d10b5-151">Atualizar balanceador de carga Olá com [AzureRmLoadBalancer conjunto](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="d10b5-151">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="d10b5-152">Criar uma regra de balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="d10b5-152">Create a load balancer rule</span></span>
<span data-ttu-id="d10b5-153">Uma regra de Balanceador de carga é toodefine usado como o tráfego é distribuído toohello VMs.</span><span class="sxs-lookup"><span data-stu-id="d10b5-153">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span> <span data-ttu-id="d10b5-154">Você definir a configuração de IP front-end Olá para o tráfego de entrada hello e Olá back-end pool tooreceive Olá tráfego IP, juntamente com a origem de saudação necessários e porta de destino.</span><span class="sxs-lookup"><span data-stu-id="d10b5-154">You define hello front-end IP configuration for hello incoming traffic and hello back-end IP pool tooreceive hello traffic, along with hello required source and destination port.</span></span> <span data-ttu-id="d10b5-155">toomake-se de que apenas as VMs íntegras receberem tráfego, você também definir Olá toouse de investigação de integridade.</span><span class="sxs-lookup"><span data-stu-id="d10b5-155">toomake sure only healthy VMs receive traffic, you also define hello health probe toouse.</span></span>

<span data-ttu-id="d10b5-156">Crie uma regra de balanceador de carga com [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span><span class="sxs-lookup"><span data-stu-id="d10b5-156">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="d10b5-157">Olá, exemplo a seguir cria uma regra de Balanceador de carga denominada *myLoadBalancerRule* e saldos de tráfego na porta *80*:</span><span class="sxs-lookup"><span data-stu-id="d10b5-157">hello following example creates a load balancer rule named *myLoadBalancerRule* and balances traffic on port *80*:</span></span>

```powershell
$probe = Get-AzureRmLoadBalancerProbeConfig -LoadBalancer $lb -Name myHealthProbe

Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80 `
  -Probe $probe
```

<span data-ttu-id="d10b5-158">Atualizar balanceador de carga Olá com [AzureRmLoadBalancer conjunto](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="d10b5-158">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a><span data-ttu-id="d10b5-159">Configurar rede virtual</span><span class="sxs-lookup"><span data-stu-id="d10b5-159">Configure virtual network</span></span>
<span data-ttu-id="d10b5-160">Antes de implantar algumas máquinas virtuais e testar seu balanceador, crie hello dando suporte a recursos de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="d10b5-160">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="d10b5-161">Para obter mais informações sobre redes virtuais, consulte Olá [gerenciar redes virtuais do Azure](tutorial-virtual-network.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="d10b5-161">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="d10b5-162">Criar recursos da rede</span><span class="sxs-lookup"><span data-stu-id="d10b5-162">Create network resources</span></span>
<span data-ttu-id="d10b5-163">Crie uma rede virtual com [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="d10b5-163">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="d10b5-164">Olá, exemplo a seguir cria uma rede virtual denominada *myVnet* com *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="d10b5-164">hello following example creates a virtual network named *myVnet* with *mySubnet*:</span></span>

```powershell
# Create subnet config
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create hello virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

<span data-ttu-id="d10b5-165">Criar uma regra de grupo de segurança de rede com [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), em seguida, crie um grupo de segurança de rede com [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="d10b5-165">Create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), then create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="d10b5-166">Adicionar sub-rede de toohello de grupo de segurança da rede do hello com [conjunto AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) e, em seguida, atualize a rede virtual Olá com [AzureRmVirtualNetwork conjunto](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="d10b5-166">Add hello network security group toohello subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) and then update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span></span> 

<span data-ttu-id="d10b5-167">Olá, exemplo a seguir cria uma regra de grupo de segurança de rede denominada *myNetworkSecurityGroup* e aplica muito*mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="d10b5-167">hello following example creates a network security group rule named *myNetworkSecurityGroup* and applies it too*mySubnet*:</span></span>

```powershell
# Create security rule config
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1001 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 80 `
  -Access Allow

# Create hello network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule

# Apply hello network security group tooa subnet
Set-AzureRmVirtualNetworkSubnetConfig `
  -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24

# Update hello virtual network
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

<span data-ttu-id="d10b5-168">As NICs virtuais são criadas com [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="d10b5-168">Virtual NICs are created with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="d10b5-169">Olá, exemplo a seguir cria três NICs virtuais.</span><span class="sxs-lookup"><span data-stu-id="d10b5-169">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="d10b5-170">(Uma NIC virtual para cada VM que você criou para seu aplicativo no hello seguindo as etapas.)</span><span class="sxs-lookup"><span data-stu-id="d10b5-170">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="d10b5-171">Você pode criar VMs e NICs virtuais adicionais a qualquer momento e adicioná-los toohello balanceador de carga:</span><span class="sxs-lookup"><span data-stu-id="d10b5-171">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -Name myNic$i `
     -Location EastUS `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}
```

## <a name="create-virtual-machines"></a><span data-ttu-id="d10b5-172">Criar máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="d10b5-172">Create virtual machines</span></span>
<span data-ttu-id="d10b5-173">tooimprove Olá alta disponibilidade do seu aplicativo, colocar suas VMs em um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="d10b5-173">tooimprove hello high availability of your app, place your VMs in an availability set.</span></span>

<span data-ttu-id="d10b5-174">Crie um conjunto de disponibilidade com [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="d10b5-174">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="d10b5-175">Olá, exemplo a seguir cria um conjunto nomeada de disponibilidade *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="d10b5-175">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

<span data-ttu-id="d10b5-176">Definir um administrador de nome de usuário e senha para Olá VMs com [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="d10b5-176">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="d10b5-177">Agora você pode criar VMs Olá com [AzureRmVM novo](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="d10b5-177">Now you can create hello VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="d10b5-178">saudação de exemplo a seguir cria três VMs:</span><span class="sxs-lookup"><span data-stu-id="d10b5-178">hello following example creates three VMs:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
  $vm = New-AzureRmVMConfig `
    -VMName myVM$i `
    -VMSize Standard_D1 `
    -AvailabilitySetId $availabilitySet.Id
  $vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM$i `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
  $vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
  $vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk$i `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
  $nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic$i
  $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
  New-AzureRmVM `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Location EastUS `
    -VM $vm
}
```

<span data-ttu-id="d10b5-179">Ele usa toocreate de alguns minutos e configurar todas as três VMs.</span><span class="sxs-lookup"><span data-stu-id="d10b5-179">It takes a few minutes toocreate and configure all three VMs.</span></span>

### <a name="install-iis-with-custom-script-extension"></a><span data-ttu-id="d10b5-180">Instalar o IIS com a extensão de script personalizado</span><span class="sxs-lookup"><span data-stu-id="d10b5-180">Install IIS with Custom Script Extension</span></span>
<span data-ttu-id="d10b5-181">Um tutorial anterior em [como toocustomize uma máquina virtual Windows](tutorial-automate-vm-deployment.md), você aprendeu como tooautomate personalização de VM com hello extensão para janelas de Script personalizado.</span><span class="sxs-lookup"><span data-stu-id="d10b5-181">In a previous tutorial on [How toocustomize a Windows virtual machine](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with hello Custom Script Extension for Windows.</span></span> <span data-ttu-id="d10b5-182">Você pode usar o hello mesma abordagem tooinstall e configurar o IIS em suas VMs.</span><span class="sxs-lookup"><span data-stu-id="d10b5-182">You can use hello same approach tooinstall and configure IIS on your VMs.</span></span>

<span data-ttu-id="d10b5-183">Use [AzureRmVMExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall Olá extensão de Script personalizado.</span><span class="sxs-lookup"><span data-stu-id="d10b5-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello Custom Script Extension.</span></span> <span data-ttu-id="d10b5-184">Olá execuções de extensão `powershell Add-WindowsFeature Web-Server` tooinstall Olá servidor Web do IIS e, em seguida, Olá atualizações *Default.htm* página tooshow Olá hostname de saudação VM:</span><span class="sxs-lookup"><span data-stu-id="d10b5-184">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver and then updates hello *Default.htm* page tooshow hello hostname of hello VM:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
     -Location EastUS
}
```

## <a name="test-load-balancer"></a><span data-ttu-id="d10b5-185">Testar o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="d10b5-185">Test load balancer</span></span>
<span data-ttu-id="d10b5-186">Obter o endereço IP público de saudação do balanceador de carga com [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="d10b5-186">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="d10b5-187">Olá, exemplo a seguir obtém endereço IP hello *myPublicIP* criado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="d10b5-187">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

<span data-ttu-id="d10b5-188">Você pode inserir o endereço IP público de saudação no navegador da web de tooa.</span><span class="sxs-lookup"><span data-stu-id="d10b5-188">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="d10b5-189">Olá site é exibido, incluindo o nome de host de saudação do hello VM balanceador de carga que Olá distribuído tooas de tráfego em Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="d10b5-189">hello website is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![Site do IIS em execução](./media/tutorial-load-balancer/running-iis-website.png)

<span data-ttu-id="d10b5-191">Balanceador de carga toosee Olá distribuir tráfego entre todas as três VMs executando o aplicativo, você pode forçar atualização de seu navegador da web.</span><span class="sxs-lookup"><span data-stu-id="d10b5-191">toosee hello load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="d10b5-192">Adicionar e remover as VMs</span><span class="sxs-lookup"><span data-stu-id="d10b5-192">Add and remove VMs</span></span>
<span data-ttu-id="d10b5-193">Talvez seja necessário tooperform manutenção Olá VMs que executam seu aplicativo, como ao instalar atualizações do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="d10b5-193">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="d10b5-194">toodeal com o aumento no tráfego tooyour aplicativo, talvez seja necessário tooadd VMs adicionais.</span><span class="sxs-lookup"><span data-stu-id="d10b5-194">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="d10b5-195">Esta seção mostra como tooremove ou adicionar uma VM do balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="d10b5-195">This section shows you how tooremove or add a VM from hello load balancer.</span></span>

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="d10b5-196">Remover uma máquina virtual do balanceador de carga Olá</span><span class="sxs-lookup"><span data-stu-id="d10b5-196">Remove a VM from hello load balancer</span></span>
<span data-ttu-id="d10b5-197">Obter a placa de interface de rede Olá com [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), Olá de conjunto, em seguida, *LoadBalancerBackendAddressPools* propriedade Olá NIC virtual muito*$null*.</span><span class="sxs-lookup"><span data-stu-id="d10b5-197">Get hello network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), then set hello *LoadBalancerBackendAddressPools* property of hello virtual NIC too*$null*.</span></span> <span data-ttu-id="d10b5-198">Por fim, atualize o NIC virtual. hello:</span><span class="sxs-lookup"><span data-stu-id="d10b5-198">Finally, update hello virtual NIC.:</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="d10b5-199">Balanceador de carga toosee Olá distribuir o tráfego entre Olá restantes duas VMs que executam seu aplicativo você pode forçar atualização de seu navegador da web.</span><span class="sxs-lookup"><span data-stu-id="d10b5-199">toosee hello load balancer distribute traffic across hello remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="d10b5-200">Agora você pode realizar uma manutenção em Olá VM, como instalar atualizações do sistema operacional ou executar uma reinicialização da VM.</span><span class="sxs-lookup"><span data-stu-id="d10b5-200">You can now perform maintenance on hello VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="d10b5-201">Adicionar um balanceador de carga de toohello VM</span><span class="sxs-lookup"><span data-stu-id="d10b5-201">Add a VM toohello load balancer</span></span>
<span data-ttu-id="d10b5-202">Após executar a manutenção VM, ou se você precisar de capacidade de tooexpand, defina Olá *LoadBalancerBackendAddressPools* propriedade Olá virtual NIC toohello *BackendAddressPool* de [ Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="d10b5-202">After performing VM maintenance, or if you need tooexpand capacity, set hello *LoadBalancerBackendAddressPools* property of hello virtual NIC toohello *BackendAddressPool* from [Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span></span>

<span data-ttu-id="d10b5-203">Obter o balanceador de carga hello:</span><span class="sxs-lookup"><span data-stu-id="d10b5-203">Get hello load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="d10b5-204">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d10b5-204">Next steps</span></span>

<span data-ttu-id="d10b5-205">Neste tutorial, você criou um balanceador de carga e anexado VMs tooit.</span><span class="sxs-lookup"><span data-stu-id="d10b5-205">In this tutorial, you created a load balancer and attached VMs tooit.</span></span> <span data-ttu-id="d10b5-206">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="d10b5-206">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d10b5-207">Criar um balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="d10b5-207">Create an Azure load balancer</span></span>
> * <span data-ttu-id="d10b5-208">Criar uma investigação de integridade do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="d10b5-208">Create a load balancer health probe</span></span>
> * <span data-ttu-id="d10b5-209">Criar regras de tráfego para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="d10b5-209">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="d10b5-210">Use Olá extensão de Script personalizado toocreate um site IIS básico</span><span class="sxs-lookup"><span data-stu-id="d10b5-210">Use hello Custom Script Extension toocreate a basic IIS site</span></span>
> * <span data-ttu-id="d10b5-211">Criar máquinas virtuais e anexar tooa balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="d10b5-211">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="d10b5-212">Exibir um balanceador de carga em ação</span><span class="sxs-lookup"><span data-stu-id="d10b5-212">View a load balancer in action</span></span>
> * <span data-ttu-id="d10b5-213">Adicionar e remover as VMs de um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="d10b5-213">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="d10b5-214">Avançar toohello toolearn de tutorial Avançar como rede de VM toomanage.</span><span class="sxs-lookup"><span data-stu-id="d10b5-214">Advance toohello next tutorial toolearn how toomanage VM networking.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d10b5-215">Gerencie VMs e redes virtuais</span><span class="sxs-lookup"><span data-stu-id="d10b5-215">Manage VMs and virtual networks</span></span>](./tutorial-virtual-network.md)
