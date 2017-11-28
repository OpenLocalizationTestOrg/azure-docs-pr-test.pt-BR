---
title: "aaaControl roteamento em uma rede Virtual do Azure - CLI - clássico | Microsoft Docs"
description: "Saiba como toocontrol roteamento em VNets usando Olá CLI do Azure no modelo de implantação clássico Olá"
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
ms.openlocfilehash: 07dde573f1a605bf280156c261d51e213ede0cdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-hello-azure-cli"></a><span data-ttu-id="8ab33-103">Roteamento de controle e use dispositivos virtuais (clássicos) usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="8ab33-103">Control routing and use virtual appliances (classic) using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8ab33-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ab33-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="8ab33-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="8ab33-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="8ab33-106">Modelo</span><span class="sxs-lookup"><span data-stu-id="8ab33-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="8ab33-107">PowerShell (Clássico)</span><span class="sxs-lookup"><span data-stu-id="8ab33-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="8ab33-108">CLI (Clássica)</span><span class="sxs-lookup"><span data-stu-id="8ab33-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="8ab33-109">Este artigo aborda o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="8ab33-109">This article covers hello classic deployment model.</span></span> <span data-ttu-id="8ab33-110">Você também pode [roteamento de controle e usar dispositivos virtuais no modelo de implantação do Gerenciador de recursos de saudação](virtual-network-create-udr-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8ab33-110">You can also [control routing and use virtual appliances in hello Resource Manager deployment model](virtual-network-create-udr-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="8ab33-111">comandos de CLI do Azure de exemplo Hello abaixo esperam um ambiente simples já criado com base no cenário de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="8ab33-111">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="8ab33-112">Comandos de saudação toorun conforme elas são exibidas neste documento, criar ambiente Olá mostrado na [criar uma rede virtual (clássica) usando Olá CLI do Azure](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8ab33-112">If you want toorun hello commands as they are displayed in this document, create hello environment shown in [create a VNet (classic) using hello Azure CLI](virtual-networks-create-vnet-classic-cli.md).</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="8ab33-113">Criar hello UDR para a sub-rede de front-end Olá</span><span class="sxs-lookup"><span data-stu-id="8ab33-113">Create hello UDR for hello front end subnet</span></span>
<span data-ttu-id="8ab33-114">tabela de rotas toocreate hello e rotas necessárias para a sub-rede de front-end de saudação com base no cenário de saudação acima, siga as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="8ab33-114">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="8ab33-115">Execute Olá modo de tooclassic de tooswitch de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8ab33-115">Run hello following command tooswitch tooclassic mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="8ab33-116">Saída:</span><span class="sxs-lookup"><span data-stu-id="8ab33-116">Output:</span></span>

        info:    New mode is asm

2. <span data-ttu-id="8ab33-117">Execute Olá toocreate de comando a seguir uma tabela de rotas para sub-rede front-end hello:</span><span class="sxs-lookup"><span data-stu-id="8ab33-117">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="8ab33-118">Saída:</span><span class="sxs-lookup"><span data-stu-id="8ab33-118">Output:</span></span>
   
        info:    Executing command network route-table create
        info:    Creating route table "UDR-FrontEnd"
        info:    Getting route table "UDR-FrontEnd"
        data:    Name                            : UDR-FrontEnd
        data:    Location                        : West US
        info:    network route-table create command OK
   
    <span data-ttu-id="8ab33-119">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="8ab33-119">Parameters:</span></span>
   
   * <span data-ttu-id="8ab33-120">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="8ab33-120">**-l (or --location)**.</span></span> <span data-ttu-id="8ab33-121">Região do Azure onde hello novo NSG será criado.</span><span class="sxs-lookup"><span data-stu-id="8ab33-121">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="8ab33-122">Para o nosso cenário, *westus*.</span><span class="sxs-lookup"><span data-stu-id="8ab33-122">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="8ab33-123">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="8ab33-123">**-n (or --name)**.</span></span> <span data-ttu-id="8ab33-124">Nome para Olá novo NSG.</span><span class="sxs-lookup"><span data-stu-id="8ab33-124">Name for hello new NSG.</span></span> <span data-ttu-id="8ab33-125">Para o nosso cenário, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="8ab33-125">For our scenario, *NSG-FrontEnd*.</span></span>
3. <span data-ttu-id="8ab33-126">Executar Olá após o comando toocreate uma rota no toosend de tabela de rota Olá todo o tráfego destinado toohello sub-rede de back-end (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="8ab33-126">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

    <span data-ttu-id="8ab33-127">Saída:</span><span class="sxs-lookup"><span data-stu-id="8ab33-127">Output:</span></span>
   
        info:    Executing command network route-table route set
        info:    Getting route table "UDR-FrontEnd"
        info:    Setting route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    network route-table route set command OK
   
    <span data-ttu-id="8ab33-128">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="8ab33-128">Parameters:</span></span>
   
   * <span data-ttu-id="8ab33-129">**-r (ou --route-table-name)**.</span><span class="sxs-lookup"><span data-stu-id="8ab33-129">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="8ab33-130">Nome da tabela de rota Olá onde rota Olá será adicionada.</span><span class="sxs-lookup"><span data-stu-id="8ab33-130">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="8ab33-131">Para nosso cenário, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="8ab33-131">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="8ab33-132">**-a (ou --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="8ab33-132">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="8ab33-133">Prefixo de endereço de sub-rede Olá onde os pacotes são destinados a.</span><span class="sxs-lookup"><span data-stu-id="8ab33-133">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="8ab33-134">Para nosso cenário, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="8ab33-134">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="8ab33-135">**-t (ou --next-hop-type)**.</span><span class="sxs-lookup"><span data-stu-id="8ab33-135">**-t (or --next-hop-type)**.</span></span> <span data-ttu-id="8ab33-136">Tipo de objeto ao qual o tráfego será enviado.</span><span class="sxs-lookup"><span data-stu-id="8ab33-136">Type of object traffic will be sent to.</span></span> <span data-ttu-id="8ab33-137">Os valores possíveis são *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* ou *None*.</span><span class="sxs-lookup"><span data-stu-id="8ab33-137">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="8ab33-138">**-p (ou --next-hop-ip-address**).</span><span class="sxs-lookup"><span data-stu-id="8ab33-138">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="8ab33-139">Endereço IP do próximo salto.</span><span class="sxs-lookup"><span data-stu-id="8ab33-139">IP address for next hop.</span></span> <span data-ttu-id="8ab33-140">Para o nosso cenário, *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="8ab33-140">For our scenario, *192.168.0.4*.</span></span>
4. <span data-ttu-id="8ab33-141">Tabela de rotas Olá tooassociate criada com hello comando a seguir de execução Olá **front-end** sub-rede:</span><span class="sxs-lookup"><span data-stu-id="8ab33-141">Run hello following command tooassociate hello route table created with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="8ab33-142">Saída:</span><span class="sxs-lookup"><span data-stu-id="8ab33-142">Output:</span></span>
   
        info:    Executing command network vnet subnet route-table add
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        info:    Associating route table "UDR-FrontEnd" and subnet "FrontEnd"
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        data:    Route table name                : UDR-FrontEnd
        data:      Location                      : West US
        data:      Routes:
        info:    network vnet subnet route-table add command OK    
   
    <span data-ttu-id="8ab33-143">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="8ab33-143">Parameters:</span></span>
   
   * <span data-ttu-id="8ab33-144">**-t (ou --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="8ab33-144">**-t (or --vnet-name)**.</span></span> <span data-ttu-id="8ab33-145">Nome de rede virtual onde está localizada a sub-rede de saudação do hello.</span><span class="sxs-lookup"><span data-stu-id="8ab33-145">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="8ab33-146">Para o nosso cenário, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="8ab33-146">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="8ab33-147">**-n (ou --subnet-name**.</span><span class="sxs-lookup"><span data-stu-id="8ab33-147">**-n (or --subnet-name**.</span></span> <span data-ttu-id="8ab33-148">Nome da tabela de rotas de Olá Olá sub-rede será adicionado ao.</span><span class="sxs-lookup"><span data-stu-id="8ab33-148">Name of hello subnet hello route table will be added to.</span></span> <span data-ttu-id="8ab33-149">Para o nosso cenário, *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="8ab33-149">For our scenario, *FrontEnd*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="8ab33-150">Criar hello UDR para a sub-rede de back-end Olá</span><span class="sxs-lookup"><span data-stu-id="8ab33-150">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="8ab33-151">tabela de rotas toocreate hello e rota necessários para a sub-rede de back-end de saudação com base no cenário de hello, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8ab33-151">toocreate hello route table and route needed for hello back-end subnet based on hello scenario, complete hello following steps:</span></span>

1. <span data-ttu-id="8ab33-152">Execute Olá toocreate de comando a seguir uma tabela de rotas para sub-rede de back-end hello:</span><span class="sxs-lookup"><span data-stu-id="8ab33-152">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-BackEnd -l uswest
    ```

2. <span data-ttu-id="8ab33-153">Executar Olá após o comando toocreate uma rota no toosend de tabela de rota Olá todo o tráfego destinado toohello sub-rede front-end (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="8ab33-153">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="8ab33-154">Execução hello após a tabela de rotas do comando tooassociate Olá com hello **back-end** sub-rede:</span><span class="sxs-lookup"><span data-stu-id="8ab33-154">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n BackEnd -r UDR-BackEnd
    ```

