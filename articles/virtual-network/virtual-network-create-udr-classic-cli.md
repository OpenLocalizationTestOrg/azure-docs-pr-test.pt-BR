---
title: "Controlar o roteamento em uma rede virtual do Azure - CLI - Clássico | Microsoft Docs"
description: "Aprenda a controlar o roteamento em VNets usando o Azure CLI no modelo de implantação clássico"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: ca2b4638-8777-4d30-b972-eb790a7c804f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 8fcb98723e7e872c932908e3456dc8680deb0901
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-the-azure-cli"></a><span data-ttu-id="8ebfb-103">Controlar o roteamento e usar dispositivos virtuais (clássico) usando o Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8ebfb-103">Control routing and use virtual appliances (classic) using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8ebfb-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ebfb-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="8ebfb-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="8ebfb-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="8ebfb-106">Modelo</span><span class="sxs-lookup"><span data-stu-id="8ebfb-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="8ebfb-107">PowerShell (Clássico)</span><span class="sxs-lookup"><span data-stu-id="8ebfb-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="8ebfb-108">CLI (Clássica)</span><span class="sxs-lookup"><span data-stu-id="8ebfb-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="8ebfb-109">Este artigo aborda o modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="8ebfb-109">This article covers the classic deployment model.</span></span> <span data-ttu-id="8ebfb-110">Você também pode [controlar o roteamento e usar dispositivos virtuais no modelo de implantação do Gerenciador de Recursos](virtual-network-create-udr-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8ebfb-110">You can also [control routing and use virtual appliances in the Resource Manager deployment model](virtual-network-create-udr-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="8ebfb-111">Os comandos da CLI do Azure de exemplo abaixo esperam um ambiente simples já criado com base no cenário acima.</span><span class="sxs-lookup"><span data-stu-id="8ebfb-111">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="8ebfb-112">Se você quiser executar os comandos da forma como eles aparecem neste documento, crie o ambiente descrito em [criar uma VNet (clássica) usando o Azure CLI](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8ebfb-112">If you want to run the commands as they are displayed in this document, create the environment shown in [create a VNet (classic) using the Azure CLI](virtual-networks-create-vnet-classic-cli.md).</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="8ebfb-113">Criar o UDR para a sub-rede de front-end</span><span class="sxs-lookup"><span data-stu-id="8ebfb-113">Create the UDR for the front end subnet</span></span>
<span data-ttu-id="8ebfb-114">Para criar a tabela de rotas e a rota necessária para a sub-rede de front-end com base no cenário acima, siga as etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="8ebfb-114">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="8ebfb-115">Execute o seguinte comando para alternar para o modo clássico:</span><span class="sxs-lookup"><span data-stu-id="8ebfb-115">Run the following command to switch to classic mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="8ebfb-116">Saída:</span><span class="sxs-lookup"><span data-stu-id="8ebfb-116">Output:</span></span>

        info:    New mode is asm

2. <span data-ttu-id="8ebfb-117">Execute o comando a seguir para criar uma tabela de rota para a sub-rede de front-end:</span><span class="sxs-lookup"><span data-stu-id="8ebfb-117">Run the following command to create a route table for the front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="8ebfb-118">Saída:</span><span class="sxs-lookup"><span data-stu-id="8ebfb-118">Output:</span></span>
   
        info:    Executing command network route-table create
        info:    Creating route table "UDR-FrontEnd"
        info:    Getting route table "UDR-FrontEnd"
        data:    Name                            : UDR-FrontEnd
        data:    Location                        : West US
        info:    network route-table create command OK
   
    <span data-ttu-id="8ebfb-119">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="8ebfb-119">Parameters:</span></span>
   
   * <span data-ttu-id="8ebfb-120">**-l (or --location)**.</span><span class="sxs-lookup"><span data-stu-id="8ebfb-120">**-l (or --location)**.</span></span> <span data-ttu-id="8ebfb-121">A região do Azure em que o novo NSG será criado.</span><span class="sxs-lookup"><span data-stu-id="8ebfb-121">Azure region where the new NSG will be created.</span></span> <span data-ttu-id="8ebfb-122">Para o nosso cenário, *westus*.</span><span class="sxs-lookup"><span data-stu-id="8ebfb-122">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="8ebfb-123">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="8ebfb-123">**-n (or --name)**.</span></span> <span data-ttu-id="8ebfb-124">Nome para o novo NGS.</span><span class="sxs-lookup"><span data-stu-id="8ebfb-124">Name for the new NSG.</span></span> <span data-ttu-id="8ebfb-125">Para o nosso cenário, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="8ebfb-125">For our scenario, *NSG-FrontEnd*.</span></span>
3. <span data-ttu-id="8ebfb-126">Execute o comando a seguir para criar uma rota na tabela de rotas para enviar todo o tráfego destinado à sub-rede de back-end (192.168.2.0/24) para a VM **FW1** (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="8ebfb-126">Run the following command to create a route in the route table to send all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

    <span data-ttu-id="8ebfb-127">Saída:</span><span class="sxs-lookup"><span data-stu-id="8ebfb-127">Output:</span></span>
   
        info:    Executing command network route-table route set
        info:    Getting route table "UDR-FrontEnd"
        info:    Setting route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    network route-table route set command OK
   
    <span data-ttu-id="8ebfb-128">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="8ebfb-128">Parameters:</span></span>
   
   * <span data-ttu-id="8ebfb-129">**-r (ou --route-table-name)**.</span><span class="sxs-lookup"><span data-stu-id="8ebfb-129">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="8ebfb-130">Nome da tabela de rotas à qual a rota será adicionada.</span><span class="sxs-lookup"><span data-stu-id="8ebfb-130">Name of the route table where the route will be added.</span></span> <span data-ttu-id="8ebfb-131">Para nosso cenário, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="8ebfb-131">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="8ebfb-132">**-a (ou --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="8ebfb-132">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="8ebfb-133">Prefixo de endereço para a sub-rede à qual os pacotes são destinados.</span><span class="sxs-lookup"><span data-stu-id="8ebfb-133">Address prefix for the subnet where packets are destined to.</span></span> <span data-ttu-id="8ebfb-134">Para nosso cenário, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="8ebfb-134">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="8ebfb-135">**-t (ou --next-hop-type)**.</span><span class="sxs-lookup"><span data-stu-id="8ebfb-135">**-t (or --next-hop-type)**.</span></span> <span data-ttu-id="8ebfb-136">Tipo de objeto ao qual o tráfego será enviado.</span><span class="sxs-lookup"><span data-stu-id="8ebfb-136">Type of object traffic will be sent to.</span></span> <span data-ttu-id="8ebfb-137">Os valores possíveis são *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* ou *None*.</span><span class="sxs-lookup"><span data-stu-id="8ebfb-137">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="8ebfb-138">**-p (ou --next-hop-ip-address**).</span><span class="sxs-lookup"><span data-stu-id="8ebfb-138">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="8ebfb-139">Endereço IP do próximo salto.</span><span class="sxs-lookup"><span data-stu-id="8ebfb-139">IP address for next hop.</span></span> <span data-ttu-id="8ebfb-140">Para o nosso cenário, *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="8ebfb-140">For our scenario, *192.168.0.4*.</span></span>
4. <span data-ttu-id="8ebfb-141">Execute o comando a seguir para associar a tabela de rotas criada à sub-rede de **FrontEnd**:</span><span class="sxs-lookup"><span data-stu-id="8ebfb-141">Run the following command to associate the route table created with the **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="8ebfb-142">Saída:</span><span class="sxs-lookup"><span data-stu-id="8ebfb-142">Output:</span></span>
   
        info:    Executing command network vnet subnet route-table add
        info:    Looking up the subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        info:    Associating route table "UDR-FrontEnd" and subnet "FrontEnd"
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        data:    Route table name                : UDR-FrontEnd
        data:      Location                      : West US
        data:      Routes:
        info:    network vnet subnet route-table add command OK    
   
    <span data-ttu-id="8ebfb-143">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="8ebfb-143">Parameters:</span></span>
   
   * <span data-ttu-id="8ebfb-144">**-t (ou --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="8ebfb-144">**-t (or --vnet-name)**.</span></span> <span data-ttu-id="8ebfb-145">Nome da VNet na qual a sub-rede está localizada.</span><span class="sxs-lookup"><span data-stu-id="8ebfb-145">Name of the VNet where the subnet is located.</span></span> <span data-ttu-id="8ebfb-146">Para nosso cenário, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="8ebfb-146">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="8ebfb-147">**-n (ou --subnet-name**.</span><span class="sxs-lookup"><span data-stu-id="8ebfb-147">**-n (or --subnet-name**.</span></span> <span data-ttu-id="8ebfb-148">Nome da sub-rede à qual a tabela de rotas será adicionada.</span><span class="sxs-lookup"><span data-stu-id="8ebfb-148">Name of the subnet the route table will be added to.</span></span> <span data-ttu-id="8ebfb-149">Para o nosso cenário, *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="8ebfb-149">For our scenario, *FrontEnd*.</span></span>

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="8ebfb-150">Criar UDR para a sub-rede de back-end</span><span class="sxs-lookup"><span data-stu-id="8ebfb-150">Create the UDR for the back-end subnet</span></span>
<span data-ttu-id="8ebfb-151">Para criar a tabela de rotas e a rota necessária para a sub-rede de back-end com base no cenário, siga as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8ebfb-151">To create the route table and route needed for the back-end subnet based on the scenario, complete the following steps:</span></span>

1. <span data-ttu-id="8ebfb-152">Execute o comando a seguir para criar uma tabela de rota para a sub-rede de back-end:</span><span class="sxs-lookup"><span data-stu-id="8ebfb-152">Run the following command to create a route table for the back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-BackEnd -l uswest
    ```

2. <span data-ttu-id="8ebfb-153">Execute o comando a seguir para criar uma rota na tabela de rotas para enviar todo o tráfego destinado à sub-rede de front-end (192.168.1.0/24) para a VM **FW1** (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="8ebfb-153">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="8ebfb-154">Execute o comando a seguir para associar a tabela de rotas à sub-rede de **BackEnd**:</span><span class="sxs-lookup"><span data-stu-id="8ebfb-154">Run the following command to associate the route table with the **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n BackEnd -r UDR-BackEnd
    ```

