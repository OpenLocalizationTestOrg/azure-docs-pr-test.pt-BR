---
title: "Como balancear a carga de máquinas virtuais Windows no Azure | Microsoft Docs"
description: "Saiba como usar o Azure Load Balancer para criar um aplicativo altamente disponível e seguro em três VMs Windows"
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
ms.openlocfilehash: 6738d88d5a0430abaf3855dbf97a618e4c83617f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-load-balance-windows-virtual-machines-in-azure-to-create-a-highly-available-application"></a><span data-ttu-id="32284-103">Como balancear a carga de máquinas virtuais Windows no Azure para criar um aplicativo altamente disponível</span><span class="sxs-lookup"><span data-stu-id="32284-103">How to load balance Windows virtual machines in Azure to create a highly available application</span></span>
<span data-ttu-id="32284-104">O balanceamento de carga fornece um nível mais alto de disponibilidade, distribuindo as solicitações de entrada em várias máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="32284-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="32284-105">Neste tutorial, você aprenderá sobre os diferentes componentes do balanceador de carga do Azure que distribuem o tráfego e fornecem alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="32284-105">In this tutorial, you learn about the different components of the Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="32284-106">Você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="32284-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="32284-107">Criar um balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="32284-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="32284-108">Criar uma investigação de integridade do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="32284-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="32284-109">Criar regras de tráfego para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="32284-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="32284-110">Usar a Extensão de Script Personalizado para criar um site do IIS básico</span><span class="sxs-lookup"><span data-stu-id="32284-110">Use the Custom Script Extension to create a basic IIS site</span></span>
> * <span data-ttu-id="32284-111">Criar máquinas virtuais e anexar a um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="32284-111">Create virtual machines and attach to a load balancer</span></span>
> * <span data-ttu-id="32284-112">Exibir um balanceador de carga em ação</span><span class="sxs-lookup"><span data-stu-id="32284-112">View a load balancer in action</span></span>
> * <span data-ttu-id="32284-113">Adicionar e remover as VMs de um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="32284-113">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="32284-114">Este tutorial requer o módulo do Azure PowerShell, versão 3.6 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="32284-114">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="32284-115">Execute ` Get-Module -ListAvailable AzureRM` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="32284-115">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="32284-116">Se você precisa atualizar, consulte [Instalar o módulo do Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="32284-116">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="azure-load-balancer-overview"></a><span data-ttu-id="32284-117">Visão geral do Balanceador de Carga do Azure</span><span class="sxs-lookup"><span data-stu-id="32284-117">Azure load balancer overview</span></span>
<span data-ttu-id="32284-118">Um Azure Load Balancer é um balanceador de carga de Camada 4 (TCP, UDP) que fornece alta disponibilidade distribuindo o tráfego de entrada entre VMs íntegros.</span><span class="sxs-lookup"><span data-stu-id="32284-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="32284-119">Uma investigação de integridade do balanceador de carga monitora uma determinada porta em cada VM e distribui o tráfego somente para uma VM operacional.</span><span class="sxs-lookup"><span data-stu-id="32284-119">A load balancer health probe monitors a given port on each VM and only distributes traffic to an operational VM.</span></span>

<span data-ttu-id="32284-120">Você define uma configuração de IP de front-end que contém um ou mais endereços IP públicos.</span><span class="sxs-lookup"><span data-stu-id="32284-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="32284-121">Essa configuração de IP de front-end permite que seu balanceador de carga e os aplicativos estejam acessíveis pela Internet.</span><span class="sxs-lookup"><span data-stu-id="32284-121">This front-end IP configuration allows your load balancer and applications to be accessible over the Internet.</span></span> 

<span data-ttu-id="32284-122">As máquinas virtuais conectam-se a um balanceador de carga usando a placa de interface de rede virtual (NIC).</span><span class="sxs-lookup"><span data-stu-id="32284-122">Virtual machines connect to a load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="32284-123">Para distribuir o tráfego para as máquinas virtuais, um pool de endereços de back-end contém os endereços IP das NICs virtuais conectadas ao balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="32284-123">To distribute traffic to the VMs, a back-end address pool contains the IP addresses of the virtual (NICs) connected to the load balancer.</span></span>

<span data-ttu-id="32284-124">Para controlar o fluxo do tráfego, você precisará definir regras do balanceador de carga para portas específicas e protocolos que mapeiam para suas VMs.</span><span class="sxs-lookup"><span data-stu-id="32284-124">To control the flow of traffic, you define load balancer rules for specific ports and protocols that map to your VMs.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="32284-125">Criar o Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="32284-125">Create Azure load balancer</span></span>
<span data-ttu-id="32284-126">Esta seção fornece detalhes sobre como criar e configurar cada componente do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="32284-126">This section details how you can create and configure each component of the load balancer.</span></span> <span data-ttu-id="32284-127">Antes de criar seu balanceador de carga, crie um grupo de recursos com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="32284-127">Before you can create your load balancer, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="32284-128">O seguinte exemplo cria um grupo de recursos chamado *myResourceGroupLoadBalancer* no local *EastUS*:</span><span class="sxs-lookup"><span data-stu-id="32284-128">The following example creates a resource group named *myResourceGroupLoadBalancer* in the *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="32284-129">Criar um endereço IP público</span><span class="sxs-lookup"><span data-stu-id="32284-129">Create a public IP address</span></span>
<span data-ttu-id="32284-130">Para acessar seu aplicativo na Internet, você precisará de um endereço IP público para o balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="32284-130">To access your app on the Internet, you need a public IP address for the load balancer.</span></span> <span data-ttu-id="32284-131">Crie um endereço IP público com [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="32284-131">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="32284-132">O exemplo a seguir cria um endereço IP público chamado *myPublicIP* no grupo de recursos *myResourceGroupLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="32284-132">The following example creates a public IP address named *myPublicIP* in the *myResourceGroupLoadBalancer* resource group:</span></span>

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="32284-133">Criar um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="32284-133">Create a load balancer</span></span>
<span data-ttu-id="32284-134">Crie um endereço IP de front-end com [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="32284-134">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="32284-135">O seguinte exemplo cria um endereço IP de front-end chamado *myFrontEndPool*:</span><span class="sxs-lookup"><span data-stu-id="32284-135">The following example creates a frontend IP address named *myFrontEndPool*:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

<span data-ttu-id="32284-136">Crie um pool de endereços de back-end com [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span><span class="sxs-lookup"><span data-stu-id="32284-136">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="32284-137">O seguinte exemplo cria um pool de endereços de back-end chamado *myBackEndPool*:</span><span class="sxs-lookup"><span data-stu-id="32284-137">The following example creates a backend address pool named *myBackEndPool*:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="32284-138">Agora, crie o balanceador de carga com [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span><span class="sxs-lookup"><span data-stu-id="32284-138">Now, create the load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="32284-139">O exemplo a seguir cria um balanceador de carga chamado *myLoadBalancer* usando o endereço *myPublicIP*:</span><span class="sxs-lookup"><span data-stu-id="32284-139">The following example creates a load balancer named *myLoadBalancer* using the *myPublicIP* address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a><span data-ttu-id="32284-140">Criar uma investigação de integridade</span><span class="sxs-lookup"><span data-stu-id="32284-140">Create a health probe</span></span>
<span data-ttu-id="32284-141">Para permitir que o balanceador de carga monitore o status de seu aplicativo, use uma investigação de integridade.</span><span class="sxs-lookup"><span data-stu-id="32284-141">To allow the load balancer to monitor the status of your app, you use a health probe.</span></span> <span data-ttu-id="32284-142">A investigação de integridade adiciona ou remove dinamicamente VMs da rotação do balanceador de carga com base na resposta às verificações de integridade.</span><span class="sxs-lookup"><span data-stu-id="32284-142">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span> <span data-ttu-id="32284-143">Por padrão, uma VM é removida da distribuição do balanceador de carga após duas falhas consecutivas em intervalos de 15 segundos.</span><span class="sxs-lookup"><span data-stu-id="32284-143">By default, a VM is removed from the load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="32284-144">Crie uma investigação de integridade com base em um protocolo ou página de verificação de integridade específica ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="32284-144">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="32284-145">O exemplo a seguir cria uma investigação de TCP.</span><span class="sxs-lookup"><span data-stu-id="32284-145">The following example creates a TCP probe.</span></span> <span data-ttu-id="32284-146">Você também pode criar investigações de HTTP personalizadas para obter verificações de integridade mais refinadas.</span><span class="sxs-lookup"><span data-stu-id="32284-146">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="32284-147">Ao usar uma investigação de HTTP personalizada, você deverá criar a página de verificação de integridade, como *healthcheck.aspx*.</span><span class="sxs-lookup"><span data-stu-id="32284-147">When using a custom HTTP probe, you must create the health check page, such as *healthcheck.aspx*.</span></span> <span data-ttu-id="32284-148">A investigação deve retornar a reposta **HTTP 200 OK** para o balanceador de carga a fim de manter o host em rotação.</span><span class="sxs-lookup"><span data-stu-id="32284-148">The probe must return an **HTTP 200 OK** response for the load balancer to keep the host in rotation.</span></span>

<span data-ttu-id="32284-149">Para criar uma investigação de integridade de TCP, use [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span><span class="sxs-lookup"><span data-stu-id="32284-149">To create a TCP health probe, you use [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="32284-150">O exemplo a seguir cria uma investigação de integridade chamada *myHealthProbe* que monitora cada VM:</span><span class="sxs-lookup"><span data-stu-id="32284-150">The following example creates a health probe named *myHealthProbe* that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

<span data-ttu-id="32284-151">Atualize o balanceador de carga com [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="32284-151">Update the load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="32284-152">Criar uma regra de balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="32284-152">Create a load balancer rule</span></span>
<span data-ttu-id="32284-153">Uma regra de balanceador de carga é usada para definir como o tráfego é distribuído para as VMs.</span><span class="sxs-lookup"><span data-stu-id="32284-153">A load balancer rule is used to define how traffic is distributed to the VMs.</span></span> <span data-ttu-id="32284-154">Definir a configuração de IP de front-end para o tráfego de entrada e o pool de IP de back-end para receber o tráfego, junto com as portas de origem e de destino necessárias.</span><span class="sxs-lookup"><span data-stu-id="32284-154">You define the front-end IP configuration for the incoming traffic and the back-end IP pool to receive the traffic, along with the required source and destination port.</span></span> <span data-ttu-id="32284-155">Para ter certeza de que apenas VMs íntegras recebem tráfego, defina também a investigação de integridade a ser usada.</span><span class="sxs-lookup"><span data-stu-id="32284-155">To make sure only healthy VMs receive traffic, you also define the health probe to use.</span></span>

<span data-ttu-id="32284-156">Crie uma regra de balanceador de carga com [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span><span class="sxs-lookup"><span data-stu-id="32284-156">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="32284-157">O seguinte exemplo cria uma regra de balanceador de carga chamada *myLoadBalancerRule* e faz o balanceamento de carga do tráfego na porta *80*:</span><span class="sxs-lookup"><span data-stu-id="32284-157">The following example creates a load balancer rule named *myLoadBalancerRule* and balances traffic on port *80*:</span></span>

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

<span data-ttu-id="32284-158">Atualize o balanceador de carga com [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="32284-158">Update the load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a><span data-ttu-id="32284-159">Configurar rede virtual</span><span class="sxs-lookup"><span data-stu-id="32284-159">Configure virtual network</span></span>
<span data-ttu-id="32284-160">Antes de implantar algumas VMs e poder testar o balanceador, crie os recursos de suporte de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="32284-160">Before you deploy some VMs and can test your balancer, create the supporting virtual network resources.</span></span> <span data-ttu-id="32284-161">Para saber mais sobre redes virtuais, veja o tutorial [Gerenciar Redes Virtuais do Azure](tutorial-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="32284-161">For more information about virtual networks, see the [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="32284-162">Criar recursos da rede</span><span class="sxs-lookup"><span data-stu-id="32284-162">Create network resources</span></span>
<span data-ttu-id="32284-163">Crie uma rede virtual com [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="32284-163">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="32284-164">O exemplo a seguir cria uma rede virtual chamada *myVnet* com uma sub-rede chamada *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="32284-164">The following example creates a virtual network named *myVnet* with *mySubnet*:</span></span>

```powershell
# Create subnet config
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create the virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

<span data-ttu-id="32284-165">Criar uma regra de grupo de segurança de rede com [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), em seguida, crie um grupo de segurança de rede com [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="32284-165">Create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), then create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="32284-166">Adicione o grupo de segurança de rede para a sub-rede com [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) e, em seguida, atualize a rede virtual com [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="32284-166">Add the network security group to the subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) and then update the virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span></span> 

<span data-ttu-id="32284-167">O exemplo a seguir cria uma regra de grupo de segurança de rede chamada *myNetworkSecurityGroup* e aplica-se a *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="32284-167">The following example creates a network security group rule named *myNetworkSecurityGroup* and applies it to *mySubnet*:</span></span>

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

# Create the network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule

# Apply the network security group to a subnet
Set-AzureRmVirtualNetworkSubnetConfig `
  -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24

# Update the virtual network
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

<span data-ttu-id="32284-168">As NICs virtuais são criadas com [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="32284-168">Virtual NICs are created with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="32284-169">O exemplo a seguir cria três NICs virtuais.</span><span class="sxs-lookup"><span data-stu-id="32284-169">The following example creates three virtual NICs.</span></span> <span data-ttu-id="32284-170">(Uma NIC virtual para cada VM criada para seu aplicativo nas etapas a seguir).</span><span class="sxs-lookup"><span data-stu-id="32284-170">(One virtual NIC for each VM you create for your app in the following steps).</span></span> <span data-ttu-id="32284-171">Você pode criar VMs e NICs virtuais adicionais a qualquer momento e adicioná-las ao balanceador de carga:</span><span class="sxs-lookup"><span data-stu-id="32284-171">You can create additional virtual NICs and VMs at any time and add them to the load balancer:</span></span>

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

## <a name="create-virtual-machines"></a><span data-ttu-id="32284-172">Criar máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="32284-172">Create virtual machines</span></span>
<span data-ttu-id="32284-173">Para melhorar a alta disponibilidade do seu aplicativo, coloque suas VMs em um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="32284-173">To improve the high availability of your app, place your VMs in an availability set.</span></span>

<span data-ttu-id="32284-174">Crie um conjunto de disponibilidade com [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="32284-174">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="32284-175">O exemplo a seguir cria um conjunto de disponibilidade chamado *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="32284-175">The following example creates an availability set named *myAvailabilitySet*:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

<span data-ttu-id="32284-176">Defina o nome de usuário e a senha de um administrador para as VMs com [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="32284-176">Set an administrator username and password for the VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="32284-177">Agora você pode criar VMs com [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="32284-177">Now you can create the VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="32284-178">O seguinte exemplo cria três VMs:</span><span class="sxs-lookup"><span data-stu-id="32284-178">The following example creates three VMs:</span></span>

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

<span data-ttu-id="32284-179">Demora alguns minutos para criar e configurar todas as três VMs.</span><span class="sxs-lookup"><span data-stu-id="32284-179">It takes a few minutes to create and configure all three VMs.</span></span>

### <a name="install-iis-with-custom-script-extension"></a><span data-ttu-id="32284-180">Instalar o IIS com a extensão de script personalizado</span><span class="sxs-lookup"><span data-stu-id="32284-180">Install IIS with Custom Script Extension</span></span>
<span data-ttu-id="32284-181">Em um tutorial anterior sobre [Como personalizar uma máquina virtual do Windows](tutorial-automate-vm-deployment.md), você aprendeu a automatizar a personalização de VM com a Extensão do Script Personalizado para Windows.</span><span class="sxs-lookup"><span data-stu-id="32284-181">In a previous tutorial on [How to customize a Windows virtual machine](tutorial-automate-vm-deployment.md), you learned how to automate VM customization with the Custom Script Extension for Windows.</span></span> <span data-ttu-id="32284-182">Você pode usar a mesma abordagem para instalar e configurar o IIS em suas VMs.</span><span class="sxs-lookup"><span data-stu-id="32284-182">You can use the same approach to install and configure IIS on your VMs.</span></span>

<span data-ttu-id="32284-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) para instalar a extensão de script personalizado.</span><span class="sxs-lookup"><span data-stu-id="32284-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) to install the Custom Script Extension.</span></span> <span data-ttu-id="32284-184">A extensão executa `powershell Add-WindowsFeature Web-Server` para instalar o servidor Web do IIS e, em seguida, atualiza a página *Default.htm* para mostrar o nome do host da VM:</span><span class="sxs-lookup"><span data-stu-id="32284-184">The extension runs `powershell Add-WindowsFeature Web-Server` to install the IIS webserver and then updates the *Default.htm* page to show the hostname of the VM:</span></span>

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

## <a name="test-load-balancer"></a><span data-ttu-id="32284-185">Testar o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="32284-185">Test load balancer</span></span>
<span data-ttu-id="32284-186">Obtenha o endereço IP público do balanceador de carga com [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="32284-186">Obtain the public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="32284-187">O exemplo a seguir obtém o endereço IP para *myPublicIP* criado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="32284-187">The following example obtains the IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

<span data-ttu-id="32284-188">Você pode inserir o endereço IP público em um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="32284-188">You can then enter the public IP address in to a web browser.</span></span> <span data-ttu-id="32284-189">O site é exibido, incluindo o nome do host da VM para a qual o balanceador de carga distribui o tráfego como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="32284-189">The website is displayed, including the hostname of the VM that the load balancer distributed traffic to as in the following example:</span></span>

![Site do IIS em execução](./media/tutorial-load-balancer/running-iis-website.png)

<span data-ttu-id="32284-191">Para ver o balanceador de carga distribuir tráfego entre todas as três VMs que executam seu aplicativo, você poderá forçar a atualização de seu navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="32284-191">To see the load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="32284-192">Adicionar e remover as VMs</span><span class="sxs-lookup"><span data-stu-id="32284-192">Add and remove VMs</span></span>
<span data-ttu-id="32284-193">Talvez seja necessário fazer a manutenção nas VMs que executam seu aplicativo, como a instalação de atualizações do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="32284-193">You may need to perform maintenance on the VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="32284-194">Para lidar com o aumento de tráfego em seu aplicativo, talvez seja necessário adicionar outras VMs.</span><span class="sxs-lookup"><span data-stu-id="32284-194">To deal with increased traffic to your app, you may need to add additional VMs.</span></span> <span data-ttu-id="32284-195">Esta seção mostra como remover ou adicionar uma VM do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="32284-195">This section shows you how to remove or add a VM from the load balancer.</span></span>

### <a name="remove-a-vm-from-the-load-balancer"></a><span data-ttu-id="32284-196">Remover uma VM do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="32284-196">Remove a VM from the load balancer</span></span>
<span data-ttu-id="32284-197">Obtenha a placa de interface de rede com [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), em seguida, defina a propriedade *LoadBalancerBackendAddressPools* da NIC virtual como *$null*.</span><span class="sxs-lookup"><span data-stu-id="32284-197">Get the network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), then set the *LoadBalancerBackendAddressPools* property of the virtual NIC to *$null*.</span></span> <span data-ttu-id="32284-198">Por fim, atualize a NIC virtual:</span><span class="sxs-lookup"><span data-stu-id="32284-198">Finally, update the virtual NIC.:</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="32284-199">Para ver o balanceador de carga distribuir tráfego entre as duas VMs restantes que executam seu aplicativo, você poderá forçar a atualização de seu navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="32284-199">To see the load balancer distribute traffic across the remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="32284-200">Agora você pode executar a manutenção na VM, como instalação de atualizações do sistema operacional ou execução de uma reinicialização da VM.</span><span class="sxs-lookup"><span data-stu-id="32284-200">You can now perform maintenance on the VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-to-the-load-balancer"></a><span data-ttu-id="32284-201">Adicionar uma VM ao balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="32284-201">Add a VM to the load balancer</span></span>
<span data-ttu-id="32284-202">Após executar a manutenção da máquina virtual ou se precisar expandir a capacidade, defina a propriedade *LoadBalancerBackendAddressPools* da NIC virtual para o *BackendAddressPool* de [Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="32284-202">After performing VM maintenance, or if you need to expand capacity, set the *LoadBalancerBackendAddressPools* property of the virtual NIC to the *BackendAddressPool* from [Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span></span>

<span data-ttu-id="32284-203">Obtenha o balanceador de carga:</span><span class="sxs-lookup"><span data-stu-id="32284-203">Get the load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="32284-204">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="32284-204">Next steps</span></span>

<span data-ttu-id="32284-205">Neste tutorial, você criou um balanceador de carga e anexou VMs.</span><span class="sxs-lookup"><span data-stu-id="32284-205">In this tutorial, you created a load balancer and attached VMs to it.</span></span> <span data-ttu-id="32284-206">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="32284-206">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="32284-207">Criar um balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="32284-207">Create an Azure load balancer</span></span>
> * <span data-ttu-id="32284-208">Criar uma investigação de integridade do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="32284-208">Create a load balancer health probe</span></span>
> * <span data-ttu-id="32284-209">Criar regras de tráfego para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="32284-209">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="32284-210">Usar a Extensão de Script Personalizado para criar um site do IIS básico</span><span class="sxs-lookup"><span data-stu-id="32284-210">Use the Custom Script Extension to create a basic IIS site</span></span>
> * <span data-ttu-id="32284-211">Criar máquinas virtuais e anexar a um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="32284-211">Create virtual machines and attach to a load balancer</span></span>
> * <span data-ttu-id="32284-212">Exibir um balanceador de carga em ação</span><span class="sxs-lookup"><span data-stu-id="32284-212">View a load balancer in action</span></span>
> * <span data-ttu-id="32284-213">Adicionar e remover as VMs de um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="32284-213">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="32284-214">Avance para o próximo tutorial para aprender a gerenciar a rede de VM.</span><span class="sxs-lookup"><span data-stu-id="32284-214">Advance to the next tutorial to learn how to manage VM networking.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="32284-215">Gerencie VMs e redes virtuais</span><span class="sxs-lookup"><span data-stu-id="32284-215">Manage VMs and virtual networks</span></span>](./tutorial-virtual-network.md)
