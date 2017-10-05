---
title: "Controlar o roteamento em uma rede virtual do Azure - PowerShell - Clássico | Microsoft Docs"
description: Aprenda a controlar o roteamento em VNets usando o PowerShell | Classico
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: d8d07c16-cbe5-4536-acd6-870269346fe3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: e9564d223cb85529f1fa97bc398d35c6debcedae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-powershell"></a><span data-ttu-id="3d092-103">Controlar o roteamento e usar dispositivos virtuais (clássico) usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="3d092-103">Control routing and use virtual appliances (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3d092-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3d092-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="3d092-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="3d092-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="3d092-106">Modelo</span><span class="sxs-lookup"><span data-stu-id="3d092-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="3d092-107">PowerShell (Clássico)</span><span class="sxs-lookup"><span data-stu-id="3d092-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="3d092-108">CLI (Clássica)</span><span class="sxs-lookup"><span data-stu-id="3d092-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="3d092-109">Antes de trabalhar com os recursos do Azure, é importante entender que, no momento, o Azure apresenta dois modelos de implantação: Azure Resource Manager e clássico.</span><span class="sxs-lookup"><span data-stu-id="3d092-109">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="3d092-110">Verifique se você entendeu [os modelos e as ferramentas de implantação](../azure-resource-manager/resource-manager-deployment-model.md) antes de trabalhar com qualquer recurso do Azure.</span><span class="sxs-lookup"><span data-stu-id="3d092-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="3d092-111">Você pode exibir a documentação para ferramentas diferentes selecionando uma opção na parte superior deste artigo.</span><span class="sxs-lookup"><span data-stu-id="3d092-111">You can view the documentation for different tools by selecting an option at the top of this article.</span></span> <span data-ttu-id="3d092-112">Este artigo aborda o modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="3d092-112">This article covers the classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="3d092-113">O exemplo de comando do Azure PowerShell abaixo espera um ambiente simples já criado com base no cenário acima.</span><span class="sxs-lookup"><span data-stu-id="3d092-113">The sample Azure PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="3d092-114">Se você quiser executar os comandos da forma como eles aparecem neste documento, crie o ambiente descrito em [criar uma VNet (clássica) usando o PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).</span><span class="sxs-lookup"><span data-stu-id="3d092-114">If you want to run the commands as they are displayed in this document, create the environment shown in [create a VNet (classic) using PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="3d092-115">Criar o UDR para a sub-rede de front-end</span><span class="sxs-lookup"><span data-stu-id="3d092-115">Create the UDR for the front end subnet</span></span>
<span data-ttu-id="3d092-116">Para criar a tabela de rotas e a rota necessária para a sub-rede de front-end com base no cenário acima, siga as etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="3d092-116">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="3d092-117">Execute o comando a seguir para criar uma tabela de rota para a sub-rede de front-end:</span><span class="sxs-lookup"><span data-stu-id="3d092-117">Run the following command to create a route table for the front-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-FrontEnd -Location uswest `
    -Label "Route table for front end subnet"
    ```

2. <span data-ttu-id="3d092-118">Execute o comando a seguir para criar uma rota na tabela de rotas para enviar todo o tráfego destinado à sub-rede de back-end (192.168.2.0/24) para a VM **FW1** (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="3d092-118">Run the following command to create a route in the route table to send all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-FrontEnd `
    |Set-AzureRoute -RouteName RouteToBackEnd -AddressPrefix 192.168.2.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="3d092-119">Execute o comando a seguir para associar a tabela de rotas à sub-rede de **FrontEnd**:</span><span class="sxs-lookup"><span data-stu-id="3d092-119">Run the following command to associate the route table with the **FrontEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName FrontEnd `
    -RouteTableName UDR-FrontEnd
    ```

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="3d092-120">Criar UDR para a sub-rede de back-end</span><span class="sxs-lookup"><span data-stu-id="3d092-120">Create the UDR for the back-end subnet</span></span>
<span data-ttu-id="3d092-121">Para criar a tabela de rotas e a rota necessária para a sub-rede de back-end com base no cenário, siga as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3d092-121">To create the route table and route needed for the back end subnet based on the scenario, complete the following steps:</span></span>

1. <span data-ttu-id="3d092-122">Execute o comando a seguir para criar uma tabela de rota para a sub-rede de back-end:</span><span class="sxs-lookup"><span data-stu-id="3d092-122">Run the following command to create a route table for the back-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-BackEnd `
    -Location uswest `
    -Label "Route table for back end subnet"
    ```

2. <span data-ttu-id="3d092-123">Execute o comando a seguir para criar uma rota na tabela de rotas para enviar todo o tráfego destinado à sub-rede de front-end (192.168.1.0/24) para a VM **FW1** (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="3d092-123">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-BackEnd
    | Set-AzureRoute `
    -RouteName RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="3d092-124">Execute o comando a seguir para associar a tabela de rotas à sub-rede de **BackEnd**:</span><span class="sxs-lookup"><span data-stu-id="3d092-124">Run the following command to associate the route table with the **BackEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName BackEnd `
    -RouteTableName UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-the-fw1-vm"></a><span data-ttu-id="3d092-125">Habilitar o encaminhamento IP na VM FW1</span><span class="sxs-lookup"><span data-stu-id="3d092-125">Enable IP forwarding on the FW1 VM</span></span>

<span data-ttu-id="3d092-126">Para habilitar o encaminhamento de IP na VM FW1, siga as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3d092-126">To enable IP forwarding in the FW1 VM, complete the following steps:</span></span>

1. <span data-ttu-id="3d092-127">Execute o seguinte comando para verificar o status do encaminhamento de IP:</span><span class="sxs-lookup"><span data-stu-id="3d092-127">Run the following command to check the status of IP forwarding:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Get-AzureIPForwarding
    ```

2. <span data-ttu-id="3d092-128">Execute o comando a seguir para habilitar o encaminhamento de IP para a VM *FW1*:</span><span class="sxs-lookup"><span data-stu-id="3d092-128">Run the following command to enable IP forwarding for the *FW1* VM:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Set-AzureIPForwarding -Enable
    ```
