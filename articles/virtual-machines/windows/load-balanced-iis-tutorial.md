---
title: "Tutorial - Compilar um aplicativo altamente disponível em VMs do Azure | Microsoft Docs"
description: "Saiba como criar um aplicativo altamente disponível e seguro em três VMs Windows com um balanceador de carga no Azure"
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
ms.openlocfilehash: 4b8690a11ec0e711782a112622e1193c24292289
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="build-a-load-balanced-highly-available-application-on-windows-virtual-machines-in-azure"></a><span data-ttu-id="3da81-103">Criar um aplicativo altamente disponível com balanceamento de carga em máquinas virtuais Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="3da81-103">Build a load balanced, highly available application on Windows virtual machines in Azure</span></span>

<span data-ttu-id="3da81-104">Neste tutorial, você criará um aplicativo altamente disponível e resistente a eventos de manutenção.</span><span class="sxs-lookup"><span data-stu-id="3da81-104">In this tutorial, you create a highly available application that is resilient to maintenance events.</span></span> <span data-ttu-id="3da81-105">O aplicativo usa um balanceador de carga, um conjunto de disponibilidade e três VMs (máquinas virtuais) Windows.</span><span class="sxs-lookup"><span data-stu-id="3da81-105">The app uses a load balancer, an availability set, and three Windows virtual machines (VMs).</span></span> <span data-ttu-id="3da81-106">Este tutorial instala o IIS, mas você pode usá-lo para implantar outra estrutura de aplicativo usando os mesmos componentes e diretrizes de alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="3da81-106">This tutorial installs IIS, though you can use this tutorial to deploy a different application framework using the same high availability components and guidelines.</span></span> 

## <a name="step-1---azure-prerequisites"></a><span data-ttu-id="3da81-107">Etapa 1: pré-requisitos do Azure</span><span class="sxs-lookup"><span data-stu-id="3da81-107">Step 1 - Azure prerequisites</span></span>

<span data-ttu-id="3da81-108">Para concluir este tutorial, verifique se você instalou o último módulo do [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3da81-108">To complete this tutorial, make sure that you have installed the latest [Azure PowerShell](/powershell/azure/overview) module.</span></span>

<span data-ttu-id="3da81-109">Primeiro, faça logon em sua assinatura do Azure com o comando Login-AzureRmAccount e siga as instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="3da81-109">First, log in to your Azure subscription with the Login-AzureRmAccount command and follow the on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="3da81-110">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="3da81-110">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="3da81-111">Antes de criar outros recursos do Azure, será necessário criar um grupo de recursos com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="3da81-111">Before you can create any other Azure resources, you need to create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="3da81-112">O seguinte exemplo cria um grupo de recursos chamado `myResourceGroup` na região `westeurope`:</span><span class="sxs-lookup"><span data-stu-id="3da81-112">The following example creates a resource group named `myResourceGroup` in the `westeurope` region:</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location westeurope
```

## <a name="step-2---create-availability-set"></a><span data-ttu-id="3da81-113">Etapa 2: criar conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="3da81-113">Step 2 - Create availability set</span></span>

<span data-ttu-id="3da81-114">As máquinas virtuais podem ser criadas em domínios lógicos de falhas e de atualização.</span><span class="sxs-lookup"><span data-stu-id="3da81-114">Virtual machines can be created across logical fault and update domains.</span></span> <span data-ttu-id="3da81-115">Cada domínio lógico representa uma parte do hardware do datacenter subjacente do Azure.</span><span class="sxs-lookup"><span data-stu-id="3da81-115">Each logical domain represents a portion of hardware in the underlying Azure datacenter.</span></span> <span data-ttu-id="3da81-116">Quando você cria duas ou mais VMs, seus recursos de computação e armazenamento são distribuídos entre esses domínios.</span><span class="sxs-lookup"><span data-stu-id="3da81-116">When you create two or more VMs, your compute and storage resources are distributed across these domains.</span></span> <span data-ttu-id="3da81-117">Essa distribuição mantém a disponibilidade de seu aplicativo, caso um componente de hardware precise de manutenção.</span><span class="sxs-lookup"><span data-stu-id="3da81-117">This distribution maintains the availability of your app if a hardware component needs maintenance.</span></span> <span data-ttu-id="3da81-118">Os conjuntos de disponibilidade permitem que você defina esses domínios lógicos de falha e de atualização.</span><span class="sxs-lookup"><span data-stu-id="3da81-118">Availability sets let you define these logical fault and update domains.</span></span>

<span data-ttu-id="3da81-119">Crie um conjunto de disponibilidade com [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="3da81-119">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="3da81-120">O exemplo a seguir cria um conjunto de disponibilidade chamado `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="3da81-120">The following example creates an availability set named `myAvailabilitySet`:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroup `
  -Name myAvailabilitySet `
  -Location westeurope `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

## <a name="step-3---create-load-balancer"></a><span data-ttu-id="3da81-121">Etapa 3: criar um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="3da81-121">Step 3 - Create load balancer</span></span>

<span data-ttu-id="3da81-122">Um Azure Load Balancer distribui o tráfego entre um conjunto de VMs definidas usando regras de balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="3da81-122">An Azure load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="3da81-123">Uma investigação de integridade monitora uma determinada porta em cada VM e distribui o tráfego somente para uma VM operacional.</span><span class="sxs-lookup"><span data-stu-id="3da81-123">A health probe monitors a given port on each VM and only distributes traffic to an operational VM.</span></span>

### <a name="create-public-ip-address"></a><span data-ttu-id="3da81-124">Criar um endereço IP público</span><span class="sxs-lookup"><span data-stu-id="3da81-124">Create public IP address</span></span>

<span data-ttu-id="3da81-125">Para acessar seu aplicativo na Internet, atribua um endereço IP público para o balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="3da81-125">To access your app on the Internet, assign a public IP address to the load balancer.</span></span> <span data-ttu-id="3da81-126">Crie um endereço IP público com [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="3da81-126">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="3da81-127">O exemplo a seguir cria um endereço IP público chamado `myPublicIP`:</span><span class="sxs-lookup"><span data-stu-id="3da81-127">The following example creates a public IP address named `myPublicIP`:</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-load-balancer"></a><span data-ttu-id="3da81-128">Criar um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="3da81-128">Create load balancer</span></span>

<span data-ttu-id="3da81-129">Crie um endereço IP de front-end com [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="3da81-129">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="3da81-130">O seguinte exemplo cria um endereço IP de front-end chamado `myFrontEndPool`:</span><span class="sxs-lookup"><span data-stu-id="3da81-130">The following example creates a frontend IP address named `myFrontEndPool`:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name myFrontEndPool -PublicIpAddress $pip
```

<span data-ttu-id="3da81-131">Crie um pool de endereços de back-end com [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span><span class="sxs-lookup"><span data-stu-id="3da81-131">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="3da81-132">O seguinte exemplo cria um pool de endereços de back-end chamado `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="3da81-132">The following example creates a backend address pool named `myBackEndPool`:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="3da81-133">Agora, crie o balanceador de carga com [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span><span class="sxs-lookup"><span data-stu-id="3da81-133">Now, create the load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="3da81-134">O exemplo a seguir cria um balanceador de carga chamado `myLoadBalancer` usando o endereço `myPublicIP`:</span><span class="sxs-lookup"><span data-stu-id="3da81-134">The following example creates a load balancer named `myLoadBalancer` using the `myPublicIP` address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroup `
  -Name myLoadBalancer `
  -Location westeurope `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-health-probe"></a><span data-ttu-id="3da81-135">Criar uma investigação de integridade</span><span class="sxs-lookup"><span data-stu-id="3da81-135">Create health probe</span></span>

<span data-ttu-id="3da81-136">Para permitir que o balanceador de carga monitore o status de seu aplicativo, use uma investigação de integridade.</span><span class="sxs-lookup"><span data-stu-id="3da81-136">To allow the load balancer to monitor the status of your app, you use a health probe.</span></span> <span data-ttu-id="3da81-137">A investigação de integridade adiciona ou remove dinamicamente VMs da rotação do balanceador de carga com base na resposta às verificações de integridade.</span><span class="sxs-lookup"><span data-stu-id="3da81-137">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span> <span data-ttu-id="3da81-138">Por padrão, uma VM é removida da distribuição do balanceador de carga após duas falhas consecutivas em intervalos de 15 segundos.</span><span class="sxs-lookup"><span data-stu-id="3da81-138">By default, a VM is removed from the load balancer distribution after two consecutive failures at 15-second intervals.</span></span>

<span data-ttu-id="3da81-139">Crie uma investigação de integridade com [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span><span class="sxs-lookup"><span data-stu-id="3da81-139">Create a health probe with [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="3da81-140">O exemplo a seguir cria uma investigação de integridade chamada `myHealthProbe` que monitora cada VM:</span><span class="sxs-lookup"><span data-stu-id="3da81-140">The following example creates a health probe named `myHealthProbe` that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

### <a name="create-load-balancer-rule"></a><span data-ttu-id="3da81-141">Criar uma regra para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="3da81-141">Create load balancer rule</span></span>

<span data-ttu-id="3da81-142">Uma regra de balanceador de carga é usada para definir como o tráfego é distribuído para as VMs.</span><span class="sxs-lookup"><span data-stu-id="3da81-142">A load balancer rule is used to define how traffic is distributed to the VMs.</span></span>

<span data-ttu-id="3da81-143">Crie uma regra de balanceador de carga com [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span><span class="sxs-lookup"><span data-stu-id="3da81-143">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="3da81-144">O seguinte exemplo cria uma regra de balanceador de carga chamada `myLoadBalancerRule` e faz o balanceamento de carga do tráfego na porta `80`:</span><span class="sxs-lookup"><span data-stu-id="3da81-144">The following example creates a load balancer rule named `myLoadBalancerRule` and balances traffic on port `80`:</span></span>

```powershell
Add-AzureRmLoadBalancerRuleConfig -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80
```

<span data-ttu-id="3da81-145">Atualize o balanceador de carga com [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="3da81-145">Update the load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="step-4---configure-networking"></a><span data-ttu-id="3da81-146">Etapa 4: configurar a rede</span><span class="sxs-lookup"><span data-stu-id="3da81-146">Step 4 - Configure networking</span></span>

<span data-ttu-id="3da81-147">Cada VM tem uma ou mais NICs (placas de interface de rede virtual) que se conecta a uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="3da81-147">Each VM has one or more virtual network interface cards (NICs) that connect to a virtual network.</span></span> <span data-ttu-id="3da81-148">Essa rede virtual é protegida para filtrar o tráfego com base em regras de acesso definidos.</span><span class="sxs-lookup"><span data-stu-id="3da81-148">This virtual network is secured to filter traffic based on defined access rules.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="3da81-149">Criar rede virtual</span><span class="sxs-lookup"><span data-stu-id="3da81-149">Create virtual network</span></span>

<span data-ttu-id="3da81-150">Primeiro, configure uma sub-rede com [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="3da81-150">First, configure a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="3da81-151">O seguinte exemplo cria uma sub-rede chamada `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="3da81-151">The following example creates a subnet named `mySubnet`:</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="3da81-152">Para fornecer conectividade de rede às VMs, crie uma rede virtual com [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="3da81-152">To provide network connectivity to your VMs, create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="3da81-153">O seguinte exemplo cria uma rede virtual chamada `myVnet` com `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="3da81-153">The following example creates a virtual network named `myVnet` with `mySubnet`:</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

### <a name="configure-network-security"></a><span data-ttu-id="3da81-154">Configurar a segurança de rede</span><span class="sxs-lookup"><span data-stu-id="3da81-154">Configure network security</span></span>

<span data-ttu-id="3da81-155">Um [grupo de segurança de rede](../../virtual-network/virtual-networks-nsg.md) (NSG) do Azure controla o tráfego de entrada e saída em uma ou mais máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="3da81-155">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="3da81-156">As regras de grupo de segurança de rede permitem ou negam o tráfego de rede em uma porta específica ou em um intervalo de porta.</span><span class="sxs-lookup"><span data-stu-id="3da81-156">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="3da81-157">Essas regras também podem incluir um prefixo do endereço de origem para que somente o tráfego originado em uma fonte predefinida possa se comunicar com uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3da81-157">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span>

<span data-ttu-id="3da81-158">Para permitir que o tráfego da Web acesse seu aplicativo, crie uma regra de grupo de segurança de rede com [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="3da81-158">To allow web traffic to reach your app, create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="3da81-159">O exemplo a seguir cria uma regra de grupo de segurança de rede chamada `myNetworkSecurityGroupRule`:</span><span class="sxs-lookup"><span data-stu-id="3da81-159">The following example creates a network security group rule named `myNetworkSecurityGroupRule`:</span></span>

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

<span data-ttu-id="3da81-160">Crie um grupo de segurança de rede com [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="3da81-160">Create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="3da81-161">O seguinte exemplo cria um NSG chamado `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="3da81-161">The following example creates an NSG named `myNetworkSecurityGroup`:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule
```

<span data-ttu-id="3da81-162">Adicione o grupo de segurança de rede à sub-rede com [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="3da81-162">Add the network security group to the subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="3da81-163">Atualize a rede virtual com [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="3da81-163">Update the virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-network-interface-cards"></a><span data-ttu-id="3da81-164">Criar placas de interface de rede virtual</span><span class="sxs-lookup"><span data-stu-id="3da81-164">Create virtual network interface cards</span></span>

<span data-ttu-id="3da81-165">Os balanceadores de carga funcionam com o recurso NIC virtual, em vez da VM real.</span><span class="sxs-lookup"><span data-stu-id="3da81-165">Load balancers function with the virtual NIC resource rather than the actual VM.</span></span> <span data-ttu-id="3da81-166">A NIC virtual é conectada ao balanceador de carga e depois anexada a uma VM.</span><span class="sxs-lookup"><span data-stu-id="3da81-166">The virtual NIC is connected to the load balancer, and then attached to a VM.</span></span>

<span data-ttu-id="3da81-167">Crie uma NIC virtual com [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="3da81-167">Create a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="3da81-168">O exemplo a seguir cria três NICs virtuais.</span><span class="sxs-lookup"><span data-stu-id="3da81-168">The following example creates three virtual NICs.</span></span> <span data-ttu-id="3da81-169">(Uma NIC virtual para cada VM criada para seu aplicativo nas etapas a seguir):</span><span class="sxs-lookup"><span data-stu-id="3da81-169">(One virtual NIC for each VM you create for your app in the following steps):</span></span>


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

## <a name="step-5---create-virtual-machines"></a><span data-ttu-id="3da81-170">Etapa 5 – Criar máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="3da81-170">Step 5 - Create virtual machines</span></span>

<span data-ttu-id="3da81-171">Com todos os componentes subjacentes aplicados, agora você pode criar VMs altamente disponíveis para executar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3da81-171">With all the underlying components in place, you can now create highly available VMs to run your app.</span></span> 

<span data-ttu-id="3da81-172">Obtenha o nome de usuário e a senha necessários para a conta de administrador na máquina virtual com [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="3da81-172">Get the username and password needed for the administrator account on the virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="3da81-173">Crie as VMs com [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface) e [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="3da81-173">Create the VMs with [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="3da81-174">O seguinte exemplo cria três VMs:</span><span class="sxs-lookup"><span data-stu-id="3da81-174">The following example creates three VMs:</span></span>

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

<span data-ttu-id="3da81-175">É necessário alguns minutos para criar e configurar as três VMs.</span><span class="sxs-lookup"><span data-stu-id="3da81-175">It takes several minutes to create and configure all three VMs.</span></span> <span data-ttu-id="3da81-176">A investigação de integridade do balanceador de carga detecta automaticamente quando o aplicativo está em execução em cada VM.</span><span class="sxs-lookup"><span data-stu-id="3da81-176">The load balancer health probe automatically detects when the app is running on each VM.</span></span> <span data-ttu-id="3da81-177">Quando o aplicativo estiver em execução, a regra do balanceador de carga começará a distribuir o tráfego.</span><span class="sxs-lookup"><span data-stu-id="3da81-177">Once the app is running, the load balancer rule starts to distribute traffic.</span></span>

### <a name="install-the-app"></a><span data-ttu-id="3da81-178">Instalar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="3da81-178">Install the app</span></span> 

<span data-ttu-id="3da81-179">As extensões de máquina virtual do Azure são usadas para automatizar tarefas de configuração de máquina virtual, como instalar aplicativos e configurar o sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="3da81-179">Azure virtual machine extensions are used to automate virtual machine configuration tasks such as installing applications and configuring the operating system.</span></span> <span data-ttu-id="3da81-180">A [extensão de script personalizado para o Windows](./../virtual-machines-windows-extensions-customscript.md) é usada para executar qualquer script do PowerShell na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3da81-180">The [custom script extension for Windows](./../virtual-machines-windows-extensions-customscript.md) is used to run any PowerShell script on the virtual machine.</span></span> <span data-ttu-id="3da81-181">O script pode ser armazenado no armazenamento do Azure, em qualquer ponto de extremidade HTTP acessível ou inserido na configuração da extensão de script personalizado.</span><span class="sxs-lookup"><span data-stu-id="3da81-181">The script can be stored in Azure storage, any accessible HTTP endpoint, or embedded in the custom script extension configuration.</span></span> <span data-ttu-id="3da81-182">Ao usar a extensão de script personalizado, o agente de VM do Azure gerencia a execução do script.</span><span class="sxs-lookup"><span data-stu-id="3da81-182">When using the custom script extension, the Azure VM agent manages the script execution.</span></span>

<span data-ttu-id="3da81-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) para instalar a extensão de script personalizado.</span><span class="sxs-lookup"><span data-stu-id="3da81-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) to install the custom script extension.</span></span> <span data-ttu-id="3da81-184">A extensão executa `powershell Add-WindowsFeature Web-Server` para instalar o servidor Web do IIS:</span><span class="sxs-lookup"><span data-stu-id="3da81-184">The extension runs `powershell Add-WindowsFeature Web-Server` to install the IIS webserver:</span></span>

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

### <a name="test-your-app"></a><span data-ttu-id="3da81-185">Testar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="3da81-185">Test your app</span></span>

<span data-ttu-id="3da81-186">Obtenha o endereço IP público do balanceador de carga com [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="3da81-186">Obtain the public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="3da81-187">O exemplo a seguir obtém o endereço IP para `myPublicIP` criado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="3da81-187">The following example obtains the IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroup -Name myPublicIP | select IpAddress
```

<span data-ttu-id="3da81-188">Insira o endereço IP público em um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="3da81-188">Enter the public IP address in to a web browser.</span></span> <span data-ttu-id="3da81-189">Com a regra do NSG em vigor, o site padrão do IIS é exibido.</span><span class="sxs-lookup"><span data-stu-id="3da81-189">With the NSG rule in place, the default IIS website is displayed.</span></span> 

![Site do IIS padrão](media/load-balanced-iis-tutorial/iis.png)

## <a name="step-6--management-tasks"></a><span data-ttu-id="3da81-191">Etapa 6 – Tarefas de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="3da81-191">Step 6 – Management tasks</span></span>

<span data-ttu-id="3da81-192">Talvez seja necessário fazer a manutenção nas VMs que executam seu aplicativo, como a instalação de atualizações do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="3da81-192">You may need to perform maintenance on the VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="3da81-193">Para lidar com o aumento de tráfego em seu aplicativo, talvez seja necessário adicionar outras VMs.</span><span class="sxs-lookup"><span data-stu-id="3da81-193">To deal with increased traffic to your app, you may need to add additional VMs.</span></span> <span data-ttu-id="3da81-194">Esta seção mostra como remover ou adicionar uma VM do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="3da81-194">This section shows you how to remove or add a VM from the load balancer.</span></span> 

### <a name="remove-a-vm-from-the-load-balancer"></a><span data-ttu-id="3da81-195">Remover uma VM do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="3da81-195">Remove a VM from the load balancer</span></span>

<span data-ttu-id="3da81-196">Remova uma VM do pool de endereços de back-end redefinindo a propriedade LoadBalancerBackendAddressPools da placa de interface de rede.</span><span class="sxs-lookup"><span data-stu-id="3da81-196">Remove a VM from the backend address pool by resetting the LoadBalancerBackendAddressPools property of the network interface card.</span></span>

<span data-ttu-id="3da81-197">Obtenha a placa de interface de rede com [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="3da81-197">Get the network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic2
``` 

<span data-ttu-id="3da81-198">Defina a propriedade LoadBalancerBackendAddressPools da placa de interface de rede como $null:</span><span class="sxs-lookup"><span data-stu-id="3da81-198">Set the LoadBalancerBackendAddressPools property of the network interface card to $null:</span></span>

```powershell
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
```

<span data-ttu-id="3da81-199">Atualize a placa de interface de rede:</span><span class="sxs-lookup"><span data-stu-id="3da81-199">Update the network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

### <a name="add-a-vm-to-the-load-balancer"></a><span data-ttu-id="3da81-200">Adicionar uma VM ao balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="3da81-200">Add a VM to the load balancer</span></span>

<span data-ttu-id="3da81-201">Depois de executar a manutenção da VM ou se precisar expandir a capacidade, adicione a NIC de uma VM ao pool de endereços de back-end do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="3da81-201">After performing VM maintenance, or if you need to expand capacity, adding the NIC of a VM to the backend address pool of the load balancer.</span></span>

<span data-ttu-id="3da81-202">Obtenha o balanceador de carga:</span><span class="sxs-lookup"><span data-stu-id="3da81-202">Get the load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer -ResourceGroupName myResourceGroup -Name myLoadBalancer 
```

<span data-ttu-id="3da81-203">Adicione o pool de endereços de back-end do balanceador de carga à placa de interface de rede:</span><span class="sxs-lookup"><span data-stu-id="3da81-203">Add the backend address pool of the load balancer to the network interface card:</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
```

<span data-ttu-id="3da81-204">Atualize a placa de interface de rede:</span><span class="sxs-lookup"><span data-stu-id="3da81-204">Update the network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="3da81-205">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3da81-205">Next Steps</span></span>

<span data-ttu-id="3da81-206">Amostras – [Scripts de exemplo do PowerShell na Máquina Virtual do Azure](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="3da81-206">Samples – [Azure Virtual Machine PowerShell sample scripts](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
