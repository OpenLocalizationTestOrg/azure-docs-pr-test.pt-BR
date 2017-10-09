---
title: aaaOpen portas tooa VM usando o PowerShell do Azure | Microsoft Docs
description: "Saiba como tooopen uma porta / criar um ponto de extremidade tooyour VM do Windows usando o modo de implantação do Gerenciador de recursos do Azure hello e do PowerShell do Azure"
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
ms.openlocfilehash: c1817a0c447ae4ce7a1ce2a1fc6927bedf2dacb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-and-endpoints-tooa-vm-in-azure-using-powershell"></a><span data-ttu-id="df6e3-103">Como tooopen tooa portas e os pontos de extremidade de VM no Azure usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="df6e3-103">How tooopen ports and endpoints tooa VM in Azure using PowerShell</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="df6e3-104">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="df6e3-104">Quick commands</span></span>
<span data-ttu-id="df6e3-105">Grupo de segurança de rede toocreate e precisar de regras de ACL [versão mais recente de saudação do Azure PowerShell instalado](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="df6e3-105">toocreate a Network Security Group and ACL rules you need [hello latest version of Azure PowerShell installed](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="df6e3-106">Você também pode [executar essas etapas usando o portal do Azure de saudação](nsg-quickstart-portal.md).</span><span class="sxs-lookup"><span data-stu-id="df6e3-106">You can also [perform these steps using hello Azure portal](nsg-quickstart-portal.md).</span></span>

<span data-ttu-id="df6e3-107">Faça logon no tooyour conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="df6e3-107">Log in tooyour Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="df6e3-108">Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="df6e3-108">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="df6e3-109">Os nomes de parâmetro de exemplo incluem *myResourceGroup*, *myNetworkSecurityGroup* e *myVnet*.</span><span class="sxs-lookup"><span data-stu-id="df6e3-109">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="df6e3-110">Crie uma regra com [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="df6e3-110">Create a rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="df6e3-111">Olá, exemplo a seguir cria uma regra denominada *myNetworkSecurityGroupRule* tooallow *tcp* o tráfego na porta *80*:</span><span class="sxs-lookup"><span data-stu-id="df6e3-111">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow *tcp* traffic on port *80*:</span></span>

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

<span data-ttu-id="df6e3-112">Em seguida, crie o grupo de segurança de rede com [AzureRmNetworkSecurityGroup novo](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) e atribuir Olá HTTP regra recém-criada da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="df6e3-112">Next, create your Network Security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) and assign hello HTTP rule you just created as follows.</span></span> <span data-ttu-id="df6e3-113">Olá, exemplo a seguir cria um grupo de segurança de rede denominado *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="df6e3-113">hello following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName "myResourceGroup" `
    -Location "EastUS" `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $httprule
```

<span data-ttu-id="df6e3-114">Agora vamos atribuir a sub-rede de tooa do grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="df6e3-114">Now let's assign your Network Security Group tooa subnet.</span></span> <span data-ttu-id="df6e3-115">Olá, exemplo a seguir atribui uma rede virtual existente chamada *myVnet* toohello variável *$vnet* com [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="df6e3-115">hello following example assigns an existing virtual network named *myVnet* toohello variable *$vnet* with [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVnet"
```

<span data-ttu-id="df6e3-116">Associe seu Grupo de Segurança de Rede à sub-rede com [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="df6e3-116">Associate your Network Security Group with your subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="df6e3-117">Olá, exemplo a seguir associa sub-rede Olá denominada *mySubnet* com seu grupo de segurança de rede:</span><span class="sxs-lookup"><span data-stu-id="df6e3-117">hello following example associates hello subnet named *mySubnet* with your Network Security Group:</span></span>

```powershell
$subnetPrefix = $vnet.Subnets|?{$_.Name -eq 'mySubnet'}

Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name "mySubnet" `
    -AddressPrefix $subnetPrefix.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

<span data-ttu-id="df6e3-118">Por fim, atualize sua rede virtual com [AzureRmVirtualNetwork conjunto](/powershell/module/azurerm.network/set-azurermvirtualnetwork) para que o efeito de tootake alterações:</span><span class="sxs-lookup"><span data-stu-id="df6e3-118">Finally, update your virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) in order for your changes tootake effect:</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```


## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="df6e3-119">Mais informações sobre os Grupos de Segurança de Rede</span><span class="sxs-lookup"><span data-stu-id="df6e3-119">More information on Network Security Groups</span></span>
<span data-ttu-id="df6e3-120">Olá aqui rápido comandos permitem que você tooget para cima e em execução com tooyour de fluxo de tráfego VM.</span><span class="sxs-lookup"><span data-stu-id="df6e3-120">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="df6e3-121">Grupos de segurança de rede fornecem vários recursos excelentes e granularidade para controlar recursos tooyour de acesso.</span><span class="sxs-lookup"><span data-stu-id="df6e3-121">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="df6e3-122">Você pode ler mais sobre a [criação de um Grupo de Segurança de Rede e as regras ACL aqui](tutorial-virtual-network.md#manage-internal-traffic).</span><span class="sxs-lookup"><span data-stu-id="df6e3-122">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#manage-internal-traffic).</span></span>

<span data-ttu-id="df6e3-123">Para aplicativos Web altamente disponíveis, você deve colocar suas VMs atrás de um balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="df6e3-123">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="df6e3-124">Balanceador de carga Olá distribui tráfego tooVMs, com um grupo de segurança de rede que fornece filtragem.</span><span class="sxs-lookup"><span data-stu-id="df6e3-124">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="df6e3-125">Para obter mais informações, consulte [como balancear tooload Linux virtual máquinas no Azure toocreate um aplicativo altamente disponível](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="df6e3-125">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="df6e3-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="df6e3-126">Next steps</span></span>
<span data-ttu-id="df6e3-127">Neste exemplo, você criou um tráfego HTTP de tooallow regra simples.</span><span class="sxs-lookup"><span data-stu-id="df6e3-127">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="df6e3-128">Você pode encontrar informações sobre como criar ambientes mais detalhadas no hello artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="df6e3-128">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="df6e3-129">Visão geral do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="df6e3-129">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="df6e3-130">O que é um NSG (grupo de segurança de rede)?</span><span class="sxs-lookup"><span data-stu-id="df6e3-130">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="df6e3-131">Visão Geral do Azure Resource Manager para Balanceadores de Carga</span><span class="sxs-lookup"><span data-stu-id="df6e3-131">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

