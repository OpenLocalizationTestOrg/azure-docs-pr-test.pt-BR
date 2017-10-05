---
title: Criar uma rede virtual - Azure PowerShell | Microsoft Docs
description: Saiba como criar uma rede virtual usando o PowerShell.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a31f4f12-54ee-4339-b968-1a8097ca77d3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e7072ddf51570d46578111e2e392e3cbea53f2aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-network-using-powershell"></a><span data-ttu-id="0bcf9-103">Criar uma rede virtual usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="0bcf9-103">Create a virtual network using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="0bcf9-104">O Azure tem dois modelos de implantação: Azure Resource Manager e clássico.</span><span class="sxs-lookup"><span data-stu-id="0bcf9-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="0bcf9-105">A Microsoft recomenda criar recursos por meio do modelo de implantação do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="0bcf9-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="0bcf9-106">Para saber mais sobre as diferenças entre os dois modelos, leia o artigo [Entender os modelos de implantação do Azure](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0bcf9-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="0bcf9-107">Este artigo explica como criar uma rede virtual por meio do modelo de implantação do Gerenciador de Recursos usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0bcf9-107">This article explains how to create a VNet through the Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="0bcf9-108">Você também pode criar uma rede virtual por meio do Gerenciador de Recursos usando outras ferramentas ou criar uma rede virtual por meio do modelo de implantação clássico, selecionando uma opção diferente na seguinte lista:</span><span class="sxs-lookup"><span data-stu-id="0bcf9-108">You can also create a VNet through Resource Manager using other tools or create a VNet through the classic deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0bcf9-109">Portal</span><span class="sxs-lookup"><span data-stu-id="0bcf9-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="0bcf9-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0bcf9-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="0bcf9-111">CLI</span><span class="sxs-lookup"><span data-stu-id="0bcf9-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="0bcf9-112">Modelo</span><span class="sxs-lookup"><span data-stu-id="0bcf9-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="0bcf9-113">Portal (clássico)</span><span class="sxs-lookup"><span data-stu-id="0bcf9-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="0bcf9-114">PowerShell (Clássico)</span><span class="sxs-lookup"><span data-stu-id="0bcf9-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="0bcf9-115">CLI (Clássica)</span><span class="sxs-lookup"><span data-stu-id="0bcf9-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="0bcf9-116">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="0bcf9-116">Create a virtual network</span></span>

<span data-ttu-id="0bcf9-117">Para criar uma rede virtual usando o PowerShell, conclua as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="0bcf9-117">To create a virtual network using PowerShell, complete the following steps:</span></span>

1. <span data-ttu-id="0bcf9-118">Instalar e configurar o Azure PowerShell executando as etapas a seguir no artigo [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0bcf9-118">Install and configure Azure PowerShell, by following the steps in the [How to Install and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>

2. <span data-ttu-id="0bcf9-119">Se necessário, crie um novo grupo de recursos, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="0bcf9-119">If necessary, create a new resource group, as shown below.</span></span> <span data-ttu-id="0bcf9-120">Para esse cenário, crie um grupo de recursos chamado *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="0bcf9-120">For this scenario, create a resource group named *TestRG*.</span></span> <span data-ttu-id="0bcf9-121">Para saber mais sobre grupos de recursos, acesse [Visão geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0bcf9-121">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="0bcf9-122">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="0bcf9-122">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG    
3. <span data-ttu-id="0bcf9-123">Crie uma nova rede virtual denominada *TestVNet*:</span><span class="sxs-lookup"><span data-stu-id="0bcf9-123">Create a new VNet named *TestVNet*:</span></span>

    ```powershell
    New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet `
    -AddressPrefix 192.168.0.0/16 -Location centralus
    ```

    <span data-ttu-id="0bcf9-124">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="0bcf9-124">Expected output:</span></span>

        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                   : W/"[Id]"
        ProvisioningState          : Succeeded
        Tags                       : 
        AddressSpace               : {
                                   "AddressPrefixes": [
                                     "192.168.0.0/16"
                                   ]
                                  }
        DhcpOptions                : {}
        Subnets                    : []
        VirtualNetworkPeerings     : []
4. <span data-ttu-id="0bcf9-125">Armazene o objeto de rede virtual em uma variável:</span><span class="sxs-lookup"><span data-stu-id="0bcf9-125">Store the virtual network object in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

   > [!TIP]
   > <span data-ttu-id="0bcf9-126">Você pode combinar as etapas 3 e 4 executando `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.</span><span class="sxs-lookup"><span data-stu-id="0bcf9-126">You can combine steps 3 and 4 by running `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.</span></span>
   > 

5. <span data-ttu-id="0bcf9-127">Adicione uma sub-rede à nova variável de Rede Virtual:</span><span class="sxs-lookup"><span data-stu-id="0bcf9-127">Add a subnet to the new VNet variable:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name FrontEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.1.0/24
    ```

    <span data-ttu-id="0bcf9-128">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="0bcf9-128">Expected output:</span></span>
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {}
        Subnets             : [
                                  {
                                    "Name": "FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24"
                                  }
                                ]
        VirtualNetworkPeerings     : []

6. <span data-ttu-id="0bcf9-129">Repita a etapa 5 acima para cada sub-rede que você deseja criar.</span><span class="sxs-lookup"><span data-stu-id="0bcf9-129">Repeat step 5 above for each subnet you want to create.</span></span> <span data-ttu-id="0bcf9-130">O comando abaixo cria a sub-rede *Back-end* para o cenário:</span><span class="sxs-lookup"><span data-stu-id="0bcf9-130">The following command creates the *BackEnd* subnet for the scenario:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name BackEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.2.0/24
    ```

7. <span data-ttu-id="0bcf9-131">Embora você crie sub-redes, elas atualmente só existem na variável local usada para recuperar a VNet criada na etapa 4 acima.</span><span class="sxs-lookup"><span data-stu-id="0bcf9-131">Although you create subnets, they currently only exist in the local variable used to retrieve the VNet you create in step 4 above.</span></span> <span data-ttu-id="0bcf9-132">Para salvar as alterações do Azure, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="0bcf9-132">To save the changes to Azure, run the following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```
   
    <span data-ttu-id="0bcf9-133">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="0bcf9-133">Expected output:</span></span>
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {
                                  "DnsServers": []
                                }
        Subnets               : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  },
                                  {
                                    "Name": "BackEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                    "AddressPrefix": "192.168.2.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  }
                                ]
        VirtualNetworkPeerings : []

## <a name="next-steps"></a><span data-ttu-id="0bcf9-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0bcf9-134">Next steps</span></span>

<span data-ttu-id="0bcf9-135">Saiba como se conectar:</span><span class="sxs-lookup"><span data-stu-id="0bcf9-135">Learn how to connect:</span></span>

- <span data-ttu-id="0bcf9-136">Uma VM (máquina virtual) em uma rede virtual lendo o artigo [Criar uma VM Windows](../virtual-machines/virtual-machines-windows-ps-create.md).</span><span class="sxs-lookup"><span data-stu-id="0bcf9-136">A virtual machine (VM) to a virtual network by reading the [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md) article.</span></span> <span data-ttu-id="0bcf9-137">Em vez de criar uma rede virtual e sub-rede nas etapas dos artigos, você pode selecionar uma rede virtual e uma sub-rede existente para se conectar a uma VM.</span><span class="sxs-lookup"><span data-stu-id="0bcf9-137">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span></span>
- <span data-ttu-id="0bcf9-138">A rede virtual para outras redes virtuais, lendo o artigo [Conectar VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="0bcf9-138">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="0bcf9-139">A rede virtual para uma rede local usando uma VPN (rede privada virtual) site a site ou um circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="0bcf9-139">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="0bcf9-140">Saiba como lendo os artigos [Conectar uma VNet a uma rede local usando uma VPN site a site](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) e [Vincular uma VNet a um circuito ExpressRoute](../expressroute/expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="0bcf9-140">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>
