---
title: "aaaControl roteamento em uma rede Virtual do Azure - PowerShell - clássico | Microsoft Docs"
description: "Saiba como toocontrol roteamento em VNets usando o PowerShell | Clássico"
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
ms.openlocfilehash: 36edf263fb434d5fb13310d4324da20e57f016a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-powershell"></a><span data-ttu-id="c1525-103">Controlar o roteamento e usar dispositivos virtuais (clássico) usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1525-103">Control routing and use virtual appliances (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c1525-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1525-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="c1525-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="c1525-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="c1525-106">Modelo</span><span class="sxs-lookup"><span data-stu-id="c1525-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="c1525-107">PowerShell (Clássico)</span><span class="sxs-lookup"><span data-stu-id="c1525-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="c1525-108">CLI (Clássica)</span><span class="sxs-lookup"><span data-stu-id="c1525-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="c1525-109">Antes de trabalhar com recursos do Azure, é importante toounderstand que o Azure atualmente tem dois modelos de implantação: Gerenciador de recursos do Azure e clássico.</span><span class="sxs-lookup"><span data-stu-id="c1525-109">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="c1525-110">Verifique se você entendeu [os modelos e as ferramentas de implantação](../azure-resource-manager/resource-manager-deployment-model.md) antes de trabalhar com qualquer recurso do Azure.</span><span class="sxs-lookup"><span data-stu-id="c1525-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="c1525-111">Você pode exibir a documentação de saudação para diferentes ferramentas selecionando uma opção na parte superior da saudação deste artigo.</span><span class="sxs-lookup"><span data-stu-id="c1525-111">You can view hello documentation for different tools by selecting an option at hello top of this article.</span></span> <span data-ttu-id="c1525-112">Este artigo aborda o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="c1525-112">This article covers hello classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="c1525-113">exemplo Hello Azure PowerShell comandos abaixo esperam um ambiente simples já foi criado com base no cenário de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="c1525-113">hello sample Azure PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="c1525-114">Comandos de saudação toorun conforme elas são exibidas neste documento, criar ambiente Olá mostrado na [criar uma rede virtual (clássica) usando o PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c1525-114">If you want toorun hello commands as they are displayed in this document, create hello environment shown in [create a VNet (classic) using PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="c1525-115">Criar hello UDR para a sub-rede de front-end Olá</span><span class="sxs-lookup"><span data-stu-id="c1525-115">Create hello UDR for hello front end subnet</span></span>
<span data-ttu-id="c1525-116">tabela de rotas toocreate hello e rotas necessárias para a sub-rede de front-end de saudação com base no cenário de saudação acima, siga as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="c1525-116">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="c1525-117">Execute Olá toocreate de comando a seguir uma tabela de rotas para sub-rede front-end hello:</span><span class="sxs-lookup"><span data-stu-id="c1525-117">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-FrontEnd -Location uswest `
    -Label "Route table for front end subnet"
    ```

2. <span data-ttu-id="c1525-118">Executar Olá após o comando toocreate uma rota no toosend de tabela de rota Olá todo o tráfego destinado toohello sub-rede de back-end (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="c1525-118">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-FrontEnd `
    |Set-AzureRoute -RouteName RouteToBackEnd -AddressPrefix 192.168.2.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="c1525-119">Execução hello após a tabela de rotas do comando tooassociate Olá com hello **front-end** sub-rede:</span><span class="sxs-lookup"><span data-stu-id="c1525-119">Run hello following command tooassociate hello route table with hello **FrontEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName FrontEnd `
    -RouteTableName UDR-FrontEnd
    ```

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="c1525-120">Criar hello UDR para a sub-rede de back-end Olá</span><span class="sxs-lookup"><span data-stu-id="c1525-120">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="c1525-121">tabela de rotas toocreate hello e rota necessário para fazer Olá end subrede com base no cenário de saudação, conclua Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c1525-121">toocreate hello route table and route needed for hello back end subnet based on hello scenario, complete hello following steps:</span></span>

1. <span data-ttu-id="c1525-122">Execute Olá toocreate de comando a seguir uma tabela de rotas para sub-rede de back-end hello:</span><span class="sxs-lookup"><span data-stu-id="c1525-122">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-BackEnd `
    -Location uswest `
    -Label "Route table for back end subnet"
    ```

2. <span data-ttu-id="c1525-123">Executar Olá após o comando toocreate uma rota no toosend de tabela de rota Olá todo o tráfego destinado toohello sub-rede front-end (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="c1525-123">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-BackEnd
    | Set-AzureRoute `
    -RouteName RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="c1525-124">Execução hello após a tabela de rotas do comando tooassociate Olá com hello **back-end** sub-rede:</span><span class="sxs-lookup"><span data-stu-id="c1525-124">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName BackEnd `
    -RouteTableName UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-hello-fw1-vm"></a><span data-ttu-id="c1525-125">Habilitar o encaminhamento de IP hello FW1 VM</span><span class="sxs-lookup"><span data-stu-id="c1525-125">Enable IP forwarding on hello FW1 VM</span></span>

<span data-ttu-id="c1525-126">encaminhamento de IP tooenable em Olá FW1 VM, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c1525-126">tooenable IP forwarding in hello FW1 VM, complete hello following steps:</span></span>

1. <span data-ttu-id="c1525-127">Execute Olá status do comando toocheck Olá de encaminhamento IP a seguir:</span><span class="sxs-lookup"><span data-stu-id="c1525-127">Run hello following command toocheck hello status of IP forwarding:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Get-AzureIPForwarding
    ```

2. <span data-ttu-id="c1525-128">Comando a seguir de execução Olá tooenable encaminhamento de IP para Olá *FW1* VM:</span><span class="sxs-lookup"><span data-stu-id="c1525-128">Run hello following command tooenable IP forwarding for hello *FW1* VM:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Set-AzureIPForwarding -Enable
    ```
