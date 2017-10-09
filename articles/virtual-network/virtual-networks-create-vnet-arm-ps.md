---
title: aaaCreate uma rede virtual - PowerShell do Azure | Microsoft Docs
description: Saiba como toocreate um virtual de rede usando o PowerShell.
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
ms.openlocfilehash: 8d6e395a77f71de9f94b6304b05450e46b47544f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-powershell"></a><span data-ttu-id="fd609-103">Criar uma rede virtual usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd609-103">Create a virtual network using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="fd609-104">O Azure tem dois modelos de implantação: Azure Resource Manager e clássico.</span><span class="sxs-lookup"><span data-stu-id="fd609-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="fd609-105">A Microsoft recomenda a criação de recursos por meio do modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="fd609-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="fd609-106">mais sobre toolearn Olá diferenças entre modelos de saudação dois ler Olá [modelos de implantação do Azure entender](../azure-resource-manager/resource-manager-deployment-model.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="fd609-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="fd609-107">Este artigo explica como toocreate uma rede virtual por meio da implantação do Gerenciador de recursos de saudação do modelo usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fd609-107">This article explains how toocreate a VNet through hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="fd609-108">Você também pode criar uma rede virtual por meio de Gerenciador de recursos usando outras ferramentas ou criar uma rede virtual por meio do modelo de implantação clássico Olá selecionando uma opção diferente de saudação lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd609-108">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fd609-109">Portal</span><span class="sxs-lookup"><span data-stu-id="fd609-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="fd609-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd609-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="fd609-111">CLI</span><span class="sxs-lookup"><span data-stu-id="fd609-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="fd609-112">Modelo</span><span class="sxs-lookup"><span data-stu-id="fd609-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="fd609-113">Portal (clássico)</span><span class="sxs-lookup"><span data-stu-id="fd609-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="fd609-114">PowerShell (Clássico)</span><span class="sxs-lookup"><span data-stu-id="fd609-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="fd609-115">CLI (Clássica)</span><span class="sxs-lookup"><span data-stu-id="fd609-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="fd609-116">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="fd609-116">Create a virtual network</span></span>

<span data-ttu-id="fd609-117">toocreate as etapas de uma rede virtual usando o PowerShell, Olá completo a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd609-117">toocreate a virtual network using PowerShell, complete hello following steps:</span></span>

1. <span data-ttu-id="fd609-118">Instalar e configurar o Azure PowerShell, seguindo as etapas Olá Olá [como tooInstall e configurar o Azure PowerShell](/powershell/azure/overview) artigo.</span><span class="sxs-lookup"><span data-stu-id="fd609-118">Install and configure Azure PowerShell, by following hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>

2. <span data-ttu-id="fd609-119">Se necessário, crie um novo grupo de recursos, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="fd609-119">If necessary, create a new resource group, as shown below.</span></span> <span data-ttu-id="fd609-120">Para esse cenário, crie um grupo de recursos chamado *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="fd609-120">For this scenario, create a resource group named *TestRG*.</span></span> <span data-ttu-id="fd609-121">Para saber mais sobre grupos de recursos, acesse [Visão geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fd609-121">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="fd609-122">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="fd609-122">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG    
3. <span data-ttu-id="fd609-123">Crie uma nova rede virtual denominada *TestVNet*:</span><span class="sxs-lookup"><span data-stu-id="fd609-123">Create a new VNet named *TestVNet*:</span></span>

    ```powershell
    New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet `
    -AddressPrefix 192.168.0.0/16 -Location centralus
    ```

    <span data-ttu-id="fd609-124">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="fd609-124">Expected output:</span></span>

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
4. <span data-ttu-id="fd609-125">Objeto de rede virtual de saudação de armazenamento em uma variável:</span><span class="sxs-lookup"><span data-stu-id="fd609-125">Store hello virtual network object in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

   > [!TIP]
   > <span data-ttu-id="fd609-126">Você pode combinar as etapas 3 e 4 executando `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.</span><span class="sxs-lookup"><span data-stu-id="fd609-126">You can combine steps 3 and 4 by running `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.</span></span>
   > 

5. <span data-ttu-id="fd609-127">Adicione uma nova rede virtual variável sub-rede toohello:</span><span class="sxs-lookup"><span data-stu-id="fd609-127">Add a subnet toohello new VNet variable:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name FrontEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.1.0/24
    ```

    <span data-ttu-id="fd609-128">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="fd609-128">Expected output:</span></span>
   
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

6. <span data-ttu-id="fd609-129">Repita a etapa 5 acima para cada sub-rede que você deseja toocreate.</span><span class="sxs-lookup"><span data-stu-id="fd609-129">Repeat step 5 above for each subnet you want toocreate.</span></span> <span data-ttu-id="fd609-130">Olá, comando a seguir cria Olá *back-end* sub-rede para o cenário de saudação:</span><span class="sxs-lookup"><span data-stu-id="fd609-130">hello following command creates hello *BackEnd* subnet for hello scenario:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name BackEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.2.0/24
    ```

7. <span data-ttu-id="fd609-131">Embora você criar sub-redes, eles só existem atualmente no Olá local tooretrieve usado variável Olá VNet criado na etapa 4 acima.</span><span class="sxs-lookup"><span data-stu-id="fd609-131">Although you create subnets, they currently only exist in hello local variable used tooretrieve hello VNet you create in step 4 above.</span></span> <span data-ttu-id="fd609-132">toosave Olá alterações tooAzure, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd609-132">toosave hello changes tooAzure, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```
   
    <span data-ttu-id="fd609-133">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="fd609-133">Expected output:</span></span>
   
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

## <a name="next-steps"></a><span data-ttu-id="fd609-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fd609-134">Next steps</span></span>

<span data-ttu-id="fd609-135">Saiba como tooconnect:</span><span class="sxs-lookup"><span data-stu-id="fd609-135">Learn how tooconnect:</span></span>

- <span data-ttu-id="fd609-136">Uma rede virtual de tooa de máquina virtual (VM) lendo Olá [criar uma VM do Windows](../virtual-machines/virtual-machines-windows-ps-create.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="fd609-136">A virtual machine (VM) tooa virtual network by reading hello [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md) article.</span></span> <span data-ttu-id="fd609-137">Em vez de criar uma rede virtual e a sub-rede nas etapas de saudação de artigos hello, você pode selecionar uma rede virtual existente e a sub-rede tooconnect uma VM.</span><span class="sxs-lookup"><span data-stu-id="fd609-137">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="fd609-138">Olá redes virtuais de tooother de rede virtual lendo Olá [VNets conectar](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="fd609-138">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="fd609-139">Olá rede virtual tooan na rede local usando uma rede privada virtual (VPN) site a site ou um circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="fd609-139">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="fd609-140">Saiba como lendo Olá [conectar uma rede de local de tooan de rede virtual usando uma VPN site a site](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) e [vincular um circuito de rota expressa do tooan de VNet](../expressroute/expressroute-howto-linkvnet-arm.md) artigos.</span><span class="sxs-lookup"><span data-stu-id="fd609-140">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>
