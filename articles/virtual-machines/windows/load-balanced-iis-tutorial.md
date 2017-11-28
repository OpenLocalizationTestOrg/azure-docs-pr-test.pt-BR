---
title: "aaaTutorial - compilação de um aplicativo altamente disponível em VMs do Azure | Microsoft Docs"
description: "Saiba como toocreate um aplicativo altamente disponível e seguro entre três máquinas virtuais do Windows com um balanceador de carga no Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 03/30/2017
ms.author: davidmu
ms.openlocfilehash: f9eff96be4f3999651c4108f0334e4eaa1a39c0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-load-balanced-highly-available-application-on-windows-virtual-machines-in-azure"></a><span data-ttu-id="5ebc8-103">Criar um aplicativo altamente disponível com balanceamento de carga em máquinas virtuais Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="5ebc8-103">Build a load balanced, highly available application on Windows virtual machines in Azure</span></span>

<span data-ttu-id="5ebc8-104">Neste tutorial, você deve criar um aplicativo altamente disponível está eventos toomaintenance resiliente.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-104">In this tutorial, you create a highly available application that is resilient toomaintenance events.</span></span> <span data-ttu-id="5ebc8-105">aplicativo Hello usa três máquinas virtuais do Windows (VMs) de um balanceador de carga e um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-105">hello app uses a load balancer, an availability set, and three Windows virtual machines (VMs).</span></span> <span data-ttu-id="5ebc8-106">Este tutorial instala o IIS, que você pode usar este tutorial toodeploy uma estrutura de aplicativo diferente usando Olá diretrizes e os mesmos componentes de alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-106">This tutorial installs IIS, though you can use this tutorial toodeploy a different application framework using hello same high availability components and guidelines.</span></span> 

## <a name="step-1---azure-prerequisites"></a><span data-ttu-id="5ebc8-107">Etapa 1: pré-requisitos do Azure</span><span class="sxs-lookup"><span data-stu-id="5ebc8-107">Step 1 - Azure prerequisites</span></span>

<span data-ttu-id="5ebc8-108">toocomplete neste tutorial, certifique-se de que você instalou hello mais recente [Azure PowerShell](/powershell/azure/overview) módulo.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-108">toocomplete this tutorial, make sure that you have installed hello latest [Azure PowerShell](/powershell/azure/overview) module.</span></span>

<span data-ttu-id="5ebc8-109">Primeiro, login tooyour assinatura do Azure com hello comando AzureRmAccount de logon e siga a saudação na tela instruções.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-109">First, log in tooyour Azure subscription with hello Login-AzureRmAccount command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="5ebc8-110">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-110">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="5ebc8-111">Antes de criar todos os outros recursos do Azure, você precisa toocreate um grupo de recursos com [AzureRmResourceGroup novo](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="5ebc8-111">Before you can create any other Azure resources, you need toocreate a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="5ebc8-112">Olá, exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` em Olá `westeurope` região:</span><span class="sxs-lookup"><span data-stu-id="5ebc8-112">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` region:</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location westeurope
```

## <a name="step-2---create-availability-set"></a><span data-ttu-id="5ebc8-113">Etapa 2: criar conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="5ebc8-113">Step 2 - Create availability set</span></span>

<span data-ttu-id="5ebc8-114">As máquinas virtuais podem ser criadas em domínios lógicos de falhas e de atualização.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-114">Virtual machines can be created across logical fault and update domains.</span></span> <span data-ttu-id="5ebc8-115">Cada domínio lógico representa uma parte do hardware no data center do Azure subjacente hello.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-115">Each logical domain represents a portion of hardware in hello underlying Azure datacenter.</span></span> <span data-ttu-id="5ebc8-116">Quando você cria duas ou mais VMs, seus recursos de computação e armazenamento são distribuídos entre esses domínios.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-116">When you create two or more VMs, your compute and storage resources are distributed across these domains.</span></span> <span data-ttu-id="5ebc8-117">Essa distribuição mantém a disponibilidade de saudação do seu aplicativo se precisar de um componente de hardware de manutenção.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-117">This distribution maintains hello availability of your app if a hardware component needs maintenance.</span></span> <span data-ttu-id="5ebc8-118">Os conjuntos de disponibilidade permitem que você defina esses domínios lógicos de falha e de atualização.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-118">Availability sets let you define these logical fault and update domains.</span></span>

<span data-ttu-id="5ebc8-119">Crie um conjunto de disponibilidade com [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="5ebc8-119">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="5ebc8-120">Olá, exemplo a seguir cria um conjunto nomeada de disponibilidade `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="5ebc8-120">hello following example creates an availability set named `myAvailabilitySet`:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroup `
  -Name myAvailabilitySet `
  -Location westeurope `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

## <a name="step-3---create-load-balancer"></a><span data-ttu-id="5ebc8-121">Etapa 3: criar um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="5ebc8-121">Step 3 - Create load balancer</span></span>

<span data-ttu-id="5ebc8-122">Um Azure Load Balancer distribui o tráfego entre um conjunto de VMs definidas usando regras de balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-122">An Azure load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="5ebc8-123">Um teste de integridade monitora uma determinada porta em cada VM e só distribui o tráfego tooan operacional VM.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-123">A health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

### <a name="create-public-ip-address"></a><span data-ttu-id="5ebc8-124">Criar um endereço IP público</span><span class="sxs-lookup"><span data-stu-id="5ebc8-124">Create public IP address</span></span>

<span data-ttu-id="5ebc8-125">tooaccess seu aplicativo em Olá Internet, atribua um balanceador de carga do toohello de endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-125">tooaccess your app on hello Internet, assign a public IP address toohello load balancer.</span></span> <span data-ttu-id="5ebc8-126">Crie um endereço IP público com [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="5ebc8-126">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="5ebc8-127">Olá, exemplo a seguir cria um endereço IP público denominado `myPublicIP`:</span><span class="sxs-lookup"><span data-stu-id="5ebc8-127">hello following example creates a public IP address named `myPublicIP`:</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-load-balancer"></a><span data-ttu-id="5ebc8-128">Criar um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="5ebc8-128">Create load balancer</span></span>

<span data-ttu-id="5ebc8-129">Crie um endereço IP de front-end com [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="5ebc8-129">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="5ebc8-130">Olá, exemplo a seguir cria um endereço IP de front-end denominado `myFrontEndPool`:</span><span class="sxs-lookup"><span data-stu-id="5ebc8-130">hello following example creates a frontend IP address named `myFrontEndPool`:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name myFrontEndPool -PublicIpAddress $pip
```

<span data-ttu-id="5ebc8-131">Crie um pool de endereços de back-end com [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span><span class="sxs-lookup"><span data-stu-id="5ebc8-131">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="5ebc8-132">Olá, exemplo a seguir cria um pool de endereços de back-end denominado `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="5ebc8-132">hello following example creates a backend address pool named `myBackEndPool`:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="5ebc8-133">Agora, crie o balanceador de carga Olá com [AzureRmLoadBalancer novo](/powershell/module/azurerm.network/new-azurermloadbalancer).</span><span class="sxs-lookup"><span data-stu-id="5ebc8-133">Now, create hello load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="5ebc8-134">Olá, exemplo a seguir cria um balanceador de carga denominado `myLoadBalancer` usando Olá `myPublicIP` endereço:</span><span class="sxs-lookup"><span data-stu-id="5ebc8-134">hello following example creates a load balancer named `myLoadBalancer` using hello `myPublicIP` address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroup `
  -Name myLoadBalancer `
  -Location westeurope `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-health-probe"></a><span data-ttu-id="5ebc8-135">Criar uma investigação de integridade</span><span class="sxs-lookup"><span data-stu-id="5ebc8-135">Create health probe</span></span>

<span data-ttu-id="5ebc8-136">tooallow Olá balanceador toomonitor Olá status de carga do seu aplicativo, você usar uma investigação de integridade.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-136">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="5ebc8-137">investigação de integridade Olá dinamicamente adiciona ou remove as VMs de rotação do balanceador de carga de saudação com base em suas verificações de toohealth de resposta.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-137">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="5ebc8-138">Por padrão, uma máquina virtual é removida da distribuição de Balanceador de carga Olá após duas falhas consecutivas em intervalos de 15 segundos.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-138">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span>

<span data-ttu-id="5ebc8-139">Crie uma investigação de integridade com [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span><span class="sxs-lookup"><span data-stu-id="5ebc8-139">Create a health probe with [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="5ebc8-140">Olá, exemplo a seguir cria um teste de integridade chamado `myHealthProbe` que monitora a cada VM:</span><span class="sxs-lookup"><span data-stu-id="5ebc8-140">hello following example creates a health probe named `myHealthProbe` that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

### <a name="create-load-balancer-rule"></a><span data-ttu-id="5ebc8-141">Criar uma regra para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="5ebc8-141">Create load balancer rule</span></span>

<span data-ttu-id="5ebc8-142">Uma regra de Balanceador de carga é toodefine usado como o tráfego é distribuído toohello VMs.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-142">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span>

<span data-ttu-id="5ebc8-143">Crie uma regra de balanceador de carga com [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span><span class="sxs-lookup"><span data-stu-id="5ebc8-143">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="5ebc8-144">Olá, exemplo a seguir cria uma regra de Balanceador de carga denominada `myLoadBalancerRule` e saldos de tráfego na porta `80`:</span><span class="sxs-lookup"><span data-stu-id="5ebc8-144">hello following example creates a load balancer rule named `myLoadBalancerRule` and balances traffic on port `80`:</span></span>

```powershell
Add-AzureRmLoadBalancerRuleConfig -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80
```

<span data-ttu-id="5ebc8-145">Atualizar balanceador de carga Olá com [AzureRmLoadBalancer conjunto](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="5ebc8-145">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="step-4---configure-networking"></a><span data-ttu-id="5ebc8-146">Etapa 4: configurar a rede</span><span class="sxs-lookup"><span data-stu-id="5ebc8-146">Step 4 - Configure networking</span></span>

<span data-ttu-id="5ebc8-147">Cada VM tem um ou mais virtual placas de rede (NICs) que se conectam a rede virtual tooa.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-147">Each VM has one or more virtual network interface cards (NICs) that connect tooa virtual network.</span></span> <span data-ttu-id="5ebc8-148">Esta rede virtual está protegida toofilter tráfego com base nas regras de acesso definidas.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-148">This virtual network is secured toofilter traffic based on defined access rules.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="5ebc8-149">Criar rede virtual</span><span class="sxs-lookup"><span data-stu-id="5ebc8-149">Create virtual network</span></span>

<span data-ttu-id="5ebc8-150">Primeiro, configure uma sub-rede com [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="5ebc8-150">First, configure a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="5ebc8-151">Olá, exemplo a seguir cria uma sub-rede denominada `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="5ebc8-151">hello following example creates a subnet named `mySubnet`:</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="5ebc8-152">tooyour de conectividade de rede tooprovide VMs, crie uma rede virtual com [AzureRmVirtualNetwork novo](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="5ebc8-152">tooprovide network connectivity tooyour VMs, create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="5ebc8-153">Olá, exemplo a seguir cria uma rede virtual denominada `myVnet` com `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="5ebc8-153">hello following example creates a virtual network named `myVnet` with `mySubnet`:</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

### <a name="configure-network-security"></a><span data-ttu-id="5ebc8-154">Configurar a segurança de rede</span><span class="sxs-lookup"><span data-stu-id="5ebc8-154">Configure network security</span></span>

<span data-ttu-id="5ebc8-155">Um [grupo de segurança de rede](../../virtual-network/virtual-networks-nsg.md) (NSG) do Azure controla o tráfego de entrada e saída em uma ou mais máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-155">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="5ebc8-156">As regras de grupo de segurança de rede permitem ou negam o tráfego de rede em uma porta específica ou em um intervalo de porta.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-156">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="5ebc8-157">Essas regras também podem incluir um prefixo do endereço de origem para que somente o tráfego originado em uma fonte predefinida possa se comunicar com uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-157">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span>

<span data-ttu-id="5ebc8-158">tooallow web tooreach de tráfego em seu aplicativo, crie uma regra de grupo de segurança de rede com [AzureRmNetworkSecurityRuleConfig novo](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="5ebc8-158">tooallow web traffic tooreach your app, create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="5ebc8-159">Olá, exemplo a seguir cria uma regra de grupo de segurança de rede denominada `myNetworkSecurityGroupRule`:</span><span class="sxs-lookup"><span data-stu-id="5ebc8-159">hello following example creates a network security group rule named `myNetworkSecurityGroupRule`:</span></span>

```powershell
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
```

<span data-ttu-id="5ebc8-160">Crie um grupo de segurança de rede com [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="5ebc8-160">Create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="5ebc8-161">Olá, exemplo a seguir cria um NSG denominado `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="5ebc8-161">hello following example creates an NSG named `myNetworkSecurityGroup`:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule
```

<span data-ttu-id="5ebc8-162">Adicionar sub-rede de toohello de grupo de segurança da rede do hello com [AzureRmVirtualNetworkSubnetConfig conjunto](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="5ebc8-162">Add hello network security group toohello subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="5ebc8-163">Rede virtual de saudação de atualização com [AzureRmVirtualNetwork conjunto](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="5ebc8-163">Update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-network-interface-cards"></a><span data-ttu-id="5ebc8-164">Criar placas de interface de rede virtual</span><span class="sxs-lookup"><span data-stu-id="5ebc8-164">Create virtual network interface cards</span></span>

<span data-ttu-id="5ebc8-165">Carregar a função balanceadores com recurso NIC virtual Olá em vez de Olá VM real.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-165">Load balancers function with hello virtual NIC resource rather than hello actual VM.</span></span> <span data-ttu-id="5ebc8-166">Olá NIC virtual é conectada toohello balanceador de carga e, em seguida, anexado tooa VM.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-166">hello virtual NIC is connected toohello load balancer, and then attached tooa VM.</span></span>

<span data-ttu-id="5ebc8-167">Crie uma NIC virtual com [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="5ebc8-167">Create a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="5ebc8-168">Olá, exemplo a seguir cria três NICs virtuais.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-168">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="5ebc8-169">(Uma NIC virtual para cada VM você criar para seu aplicativo no hello seguindo as etapas):</span><span class="sxs-lookup"><span data-stu-id="5ebc8-169">(One virtual NIC for each VM you create for your app in hello following steps):</span></span>


```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface -ResourceGroupName myResourceGroup `
     -Name myNic$i `
     -Location westeurope `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}

```

## <a name="step-5---create-virtual-machines"></a><span data-ttu-id="5ebc8-170">Etapa 5 – Criar máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="5ebc8-170">Step 5 - Create virtual machines</span></span>

<span data-ttu-id="5ebc8-171">Com hello todos os componentes no lugar de base, agora você pode criar seu aplicativo de toorun de máquinas virtuais altamente disponível.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-171">With all hello underlying components in place, you can now create highly available VMs toorun your app.</span></span> 

<span data-ttu-id="5ebc8-172">Obter Olá nome de usuário e a senha necessários para a conta de administrador de saudação em máquina virtual Olá [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="5ebc8-172">Get hello username and password needed for hello administrator account on hello virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="5ebc8-173">Criar VMs Olá com [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [conjunto AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [AzureRmVMSourceImage conjunto](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [AzureRmVMNetworkInterface adicionar](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), e [AzureRmVM novo](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="5ebc8-173">Create hello VMs with [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="5ebc8-174">saudação de exemplo a seguir cria três VMs:</span><span class="sxs-lookup"><span data-stu-id="5ebc8-174">hello following example creates three VMs:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   $vm = New-AzureRmVMConfig -VMName myVM$i -VMSize Standard_D1 -AvailabilitySetId $availabilitySet.Id
   $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName myVM$i -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2016-Datacenter -Version latest
   $vm = Set-AzureRmVMOSDisk -VM $vm -Name myOsDisk$i -StorageAccountType StandardLRS -DiskSizeInGB 128 -CreateOption FromImage -Caching ReadWrite
   $nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic$i
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM -ResourceGroupName myResourceGroup -Location westeurope -VM $vm
}

```

<span data-ttu-id="5ebc8-175">Ele usa várias toocreate de minutos e configurar todas as três VMs.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-175">It takes several minutes toocreate and configure all three VMs.</span></span> <span data-ttu-id="5ebc8-176">Olá investigação de integridade do balanceador de carga detecta automaticamente quando o aplicativo hello está em execução em cada VM.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-176">hello load balancer health probe automatically detects when hello app is running on each VM.</span></span> <span data-ttu-id="5ebc8-177">Depois que o aplicativo hello está em execução, regra de Balanceador de carga Olá inicia toodistribute tráfego.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-177">Once hello app is running, hello load balancer rule starts toodistribute traffic.</span></span>

### <a name="install-hello-app"></a><span data-ttu-id="5ebc8-178">Instalar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="5ebc8-178">Install hello app</span></span> 

<span data-ttu-id="5ebc8-179">Extensões de máquina virtual do Azure são tarefas de configuração de máquina virtual tooautomate usado como instalar aplicativos e configurar o sistema operacional de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-179">Azure virtual machine extensions are used tooautomate virtual machine configuration tasks such as installing applications and configuring hello operating system.</span></span> <span data-ttu-id="5ebc8-180">Olá [extensão do script personalizado para o Windows](./../virtual-machines-windows-extensions-customscript.md) é toorun usada em qualquer script do PowerShell na máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-180">hello [custom script extension for Windows](./../virtual-machines-windows-extensions-customscript.md) is used toorun any PowerShell script on hello virtual machine.</span></span> <span data-ttu-id="5ebc8-181">script Hello pode ser armazenado no armazenamento do Azure, qualquer ponto de extremidade HTTP acessível, ou na configuração de extensão do script personalizado hello.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-181">hello script can be stored in Azure storage, any accessible HTTP endpoint, or embedded in hello custom script extension configuration.</span></span> <span data-ttu-id="5ebc8-182">Ao usar a extensão do script personalizado Olá, o agente de VM do Azure Olá gerencia a execução do script hello.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-182">When using hello custom script extension, hello Azure VM agent manages hello script execution.</span></span>

<span data-ttu-id="5ebc8-183">Use [AzureRmVMExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmextension) extensão do script personalizado Olá tooinstall.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello custom script extension.</span></span> <span data-ttu-id="5ebc8-184">Olá execuções de extensão `powershell Add-WindowsFeature Web-Server` tooinstall Olá IIS webserver:</span><span class="sxs-lookup"><span data-stu-id="5ebc8-184">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server"}' `
     -Location westeurope
}
```

### <a name="test-your-app"></a><span data-ttu-id="5ebc8-185">Testar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="5ebc8-185">Test your app</span></span>

<span data-ttu-id="5ebc8-186">Obter o endereço IP público de saudação do balanceador de carga com [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="5ebc8-186">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="5ebc8-187">Olá, exemplo a seguir obtém endereço IP hello `myPublicIP` criado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="5ebc8-187">hello following example obtains hello IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroup -Name myPublicIP | select IpAddress
```

<span data-ttu-id="5ebc8-188">Insira o endereço IP público de saudação no navegador da web de tooa.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-188">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="5ebc8-189">Com a regra NSG Olá em vigor, site padrão do IIS Olá é exibida.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-189">With hello NSG rule in place, hello default IIS website is displayed.</span></span> 

![Site do IIS padrão](media/load-balanced-iis-tutorial/iis.png)

## <a name="step-6--management-tasks"></a><span data-ttu-id="5ebc8-191">Etapa 6 – Tarefas de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="5ebc8-191">Step 6 – Management tasks</span></span>

<span data-ttu-id="5ebc8-192">Talvez seja necessário tooperform manutenção Olá VMs que executam seu aplicativo, como ao instalar atualizações do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-192">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="5ebc8-193">toodeal com o aumento no tráfego tooyour aplicativo, talvez seja necessário tooadd VMs adicionais.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-193">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="5ebc8-194">Esta seção mostra como tooremove ou adicionar uma VM do balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-194">This section shows you how tooremove or add a VM from hello load balancer.</span></span> 

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="5ebc8-195">Remover uma máquina virtual do balanceador de carga Olá</span><span class="sxs-lookup"><span data-stu-id="5ebc8-195">Remove a VM from hello load balancer</span></span>

<span data-ttu-id="5ebc8-196">Remova uma máquina virtual do pool de endereços de back-end Olá redefinindo a propriedade de LoadBalancerBackendAddressPools Olá da placa de interface de rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-196">Remove a VM from hello backend address pool by resetting hello LoadBalancerBackendAddressPools property of hello network interface card.</span></span>

<span data-ttu-id="5ebc8-197">Obter a placa de interface de rede Olá com [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="5ebc8-197">Get hello network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic2
``` 

<span data-ttu-id="5ebc8-198">Defina a propriedade de LoadBalancerBackendAddressPools de saudação da placa de interface de rede Olá muito null$:</span><span class="sxs-lookup"><span data-stu-id="5ebc8-198">Set hello LoadBalancerBackendAddressPools property of hello network interface card too$null:</span></span>

```powershell
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
```

<span data-ttu-id="5ebc8-199">Placa de interface de rede de saudação de atualização:</span><span class="sxs-lookup"><span data-stu-id="5ebc8-199">Update hello network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="5ebc8-200">Adicionar um balanceador de carga de toohello VM</span><span class="sxs-lookup"><span data-stu-id="5ebc8-200">Add a VM toohello load balancer</span></span>

<span data-ttu-id="5ebc8-201">Depois de executar a manutenção VM, ou se você precisar de capacidade de tooexpand, adicionando Olá NIC de um pool de endereços de back-end do VM toohello saudação do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="5ebc8-201">After performing VM maintenance, or if you need tooexpand capacity, adding hello NIC of a VM toohello backend address pool of hello load balancer.</span></span>

<span data-ttu-id="5ebc8-202">Obter o balanceador de carga hello:</span><span class="sxs-lookup"><span data-stu-id="5ebc8-202">Get hello load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer -ResourceGroupName myResourceGroup -Name myLoadBalancer 
```

<span data-ttu-id="5ebc8-203">Adicione pool de endereços de back-end de saudação da placa de interface de rede de toohello de Balanceador de carga de saudação:</span><span class="sxs-lookup"><span data-stu-id="5ebc8-203">Add hello backend address pool of hello load balancer toohello network interface card:</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
```

<span data-ttu-id="5ebc8-204">Placa de interface de rede de saudação de atualização:</span><span class="sxs-lookup"><span data-stu-id="5ebc8-204">Update hello network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="5ebc8-205">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5ebc8-205">Next Steps</span></span>

<span data-ttu-id="5ebc8-206">Amostras – [Scripts de exemplo do PowerShell na Máquina Virtual do Azure](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="5ebc8-206">Samples – [Azure Virtual Machine PowerShell sample scripts](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
