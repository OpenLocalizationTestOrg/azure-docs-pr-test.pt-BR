---
title: Abrir portas para uma VM usando o Azure PowerShell | Microsoft Docs
description: "Saiba como abrir uma porta/criar um ponto de extremidade para sua VM do Windows usando o modelo de implantação do Azure Resource Manager e o Azure PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf45f7d8-451a-48ab-8419-730366d54f1e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: e818e3b3c707e1471d6f580f8379a277d3575b89
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-open-ports-and-endpoints-to-a-vm-in-azure-using-powershell"></a><span data-ttu-id="8bac7-103">Como abrir portas e pontos de extremidade para uma VM no Azure usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="8bac7-103">How to open ports and endpoints to a VM in Azure using PowerShell</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="8bac7-104">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="8bac7-104">Quick commands</span></span>
<span data-ttu-id="8bac7-105">Para criar um Grupo de Segurança de Rede e as regras de ACL, você precisa [ter a versão mais recente do Azure PowerShell instalada](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="8bac7-105">To create a Network Security Group and ACL rules you need [the latest version of Azure PowerShell installed](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="8bac7-106">Você também pode [executar essas etapas usando o Portal do Azure](nsg-quickstart-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8bac7-106">You can also [perform these steps using the Azure portal](nsg-quickstart-portal.md).</span></span>

<span data-ttu-id="8bac7-107">Faça logon na sua Conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="8bac7-107">Log in to your Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="8bac7-108">Nos exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="8bac7-108">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="8bac7-109">Os nomes de parâmetro de exemplo incluem *myResourceGroup*, *myNetworkSecurityGroup* e *myVnet*.</span><span class="sxs-lookup"><span data-stu-id="8bac7-109">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="8bac7-110">Crie uma regra com [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="8bac7-110">Create a rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="8bac7-111">O exemplo a seguir cria uma regra chamada *myNetworkSecurityGroupRule* para permitir o tráfego *tcp* na porta *80*:</span><span class="sxs-lookup"><span data-stu-id="8bac7-111">The following example creates a rule named *myNetworkSecurityGroupRule* to allow *tcp* traffic on port *80*:</span></span>

```powershell
$httprule = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRule" `
    -Description "Allow HTTP" `
    -Access "Allow" `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority "100" `
    -SourceAddressPrefix "Internet" `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80
```

<span data-ttu-id="8bac7-112">Em seguida, crie seu Grupo de Segurança de Rede com [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) e atribua a regra de HTTP que você acabou de criar conforme descrito a seguir.</span><span class="sxs-lookup"><span data-stu-id="8bac7-112">Next, create your Network Security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) and assign the HTTP rule you just created as follows.</span></span> <span data-ttu-id="8bac7-113">O exemplo a seguir cria um Grupo de Segurança de Rede chamado *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="8bac7-113">The following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName "myResourceGroup" `
    -Location "EastUS" `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $httprule
```

<span data-ttu-id="8bac7-114">Agora, vamos atribuir seu Grupo de Segurança de Rede a uma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="8bac7-114">Now let's assign your Network Security Group to a subnet.</span></span> <span data-ttu-id="8bac7-115">O exemplo a seguir atribui uma rede virtual existente chamada *myVnet* à variável *$vnet* com [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="8bac7-115">The following example assigns an existing virtual network named *myVnet* to the variable *$vnet* with [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVnet"
```

<span data-ttu-id="8bac7-116">Associe seu Grupo de Segurança de Rede à sub-rede com [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="8bac7-116">Associate your Network Security Group with your subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="8bac7-117">O exemplo a seguir associa a sub-rede chamada *mySubnet* ao seu Grupo de Segurança de Rede:</span><span class="sxs-lookup"><span data-stu-id="8bac7-117">The following example associates the subnet named *mySubnet* with your Network Security Group:</span></span>

```powershell
$subnetPrefix = $vnet.Subnets|?{$_.Name -eq 'mySubnet'}

Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name "mySubnet" `
    -AddressPrefix $subnetPrefix.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

<span data-ttu-id="8bac7-118">Por fim, atualize sua rede virtual com [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) para que suas alterações entrem em vigor:</span><span class="sxs-lookup"><span data-stu-id="8bac7-118">Finally, update your virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) in order for your changes to take effect:</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```


## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="8bac7-119">Mais informações sobre os Grupos de Segurança de Rede</span><span class="sxs-lookup"><span data-stu-id="8bac7-119">More information on Network Security Groups</span></span>
<span data-ttu-id="8bac7-120">Os comandos rápidos aqui permitem que você coloque tudo em funcionamento com o tráfego que flui para sua VM.</span><span class="sxs-lookup"><span data-stu-id="8bac7-120">The quick commands here allow you to get up and running with traffic flowing to your VM.</span></span> <span data-ttu-id="8bac7-121">Os Grupos de Segurança de Rede fornecem muitos recursos excelentes e granularidade para controlar o acesso aos recursos.</span><span class="sxs-lookup"><span data-stu-id="8bac7-121">Network Security Groups provide many great features and granularity for controlling access to your resources.</span></span> <span data-ttu-id="8bac7-122">Você pode ler mais sobre a [criação de um Grupo de Segurança de Rede e as regras ACL aqui](tutorial-virtual-network.md#manage-internal-traffic).</span><span class="sxs-lookup"><span data-stu-id="8bac7-122">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#manage-internal-traffic).</span></span>

<span data-ttu-id="8bac7-123">Para aplicativos Web altamente disponíveis, você deve colocar suas VMs atrás de um balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="8bac7-123">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="8bac7-124">O balanceador de carga distribui o tráfego para VMs, com um Grupo de Segurança de rede que fornece filtragem.</span><span class="sxs-lookup"><span data-stu-id="8bac7-124">The load balancer distributes traffic to VMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="8bac7-125">Para saber mais, veja [Como balancear a carga de máquinas virtuais Linux no Azure para criar um aplicativo altamente disponível](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="8bac7-125">For more information, see [How to load balance Linux virtual machines in Azure to create a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bac7-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8bac7-126">Next steps</span></span>
<span data-ttu-id="8bac7-127">Neste exemplo, você criou uma regra simples para permitir o tráfego HTTP.</span><span class="sxs-lookup"><span data-stu-id="8bac7-127">In this example, you created a simple rule to allow HTTP traffic.</span></span> <span data-ttu-id="8bac7-128">Você pode encontrar informações sobre a criação de ambientes mais detalhados nos seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="8bac7-128">You can find information on creating more detailed environments in the following articles:</span></span>

* [<span data-ttu-id="8bac7-129">Visão geral do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8bac7-129">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="8bac7-130">O que é um NSG (grupo de segurança de rede)?</span><span class="sxs-lookup"><span data-stu-id="8bac7-130">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="8bac7-131">Visão Geral do Azure Resource Manager para Balanceadores de Carga</span><span class="sxs-lookup"><span data-stu-id="8bac7-131">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

