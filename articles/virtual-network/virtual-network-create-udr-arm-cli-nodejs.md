---
title: "dispositivos de roteamento e virtual de aaaControl usando Olá 1.0 da CLI do Azure | Microsoft Docs"
description: "Saiba como dispositivos de roteamento e virtual de toocontrol usando Olá 1.0 da CLI do Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/18/2017
ms.author: jdial
ms.openlocfilehash: 1c8a552d949521fa554880c00405e65fa47a8162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-10"></a><span data-ttu-id="2d125-103">Criar rotas definidas pelo usuário (UDR) usando Olá 1.0 da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="2d125-103">Create User-Defined Routes (UDR) using hello Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2d125-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2d125-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="2d125-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="2d125-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="2d125-106">Modelo</span><span class="sxs-lookup"><span data-stu-id="2d125-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="2d125-107">PowerShell (Clássico)</span><span class="sxs-lookup"><span data-stu-id="2d125-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="2d125-108">CLI (Clássica)</span><span class="sxs-lookup"><span data-stu-id="2d125-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

<span data-ttu-id="2d125-109">Crie roteamento personalizado e dispositivos virtuais usando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="2d125-109">Create custom routing and virtual appliances using hello Azure CLI.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="2d125-110">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="2d125-110">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="2d125-111">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="2d125-111">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="2d125-112">[1.0 de CLI do Azure](#Create-the-UDR-for-the-front-end-subnet) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="2d125-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="2d125-113">[2.0 do CLI do Azure](virtual-network-create-udr-arm-cli.md) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="2d125-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) - our next generation CLI for hello resource management deployment model</span></span> 


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="2d125-114">comandos de CLI do Azure de exemplo Hello abaixo esperam um ambiente simples já criado com base no cenário de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="2d125-114">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="2d125-115">Se você quiser comandos de saudação toorun conforme elas são exibidas neste documento, primeiro criar o ambiente de teste Olá implantando [este modelo](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), clique em **implantar tooAzure**, substitua os valores de parâmetro padrão Olá Se necessário e siga as instruções de saudação em Olá portal.</span><span class="sxs-lookup"><span data-stu-id="2d125-115">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>


## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="2d125-116">Criar hello UDR para sub-rede front-end Olá</span><span class="sxs-lookup"><span data-stu-id="2d125-116">Create hello UDR for hello front-end subnet</span></span>
<span data-ttu-id="2d125-117">tabela de rotas toocreate hello e rotas necessárias para a sub-rede de front-end de saudação com base no cenário de saudação acima, siga as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="2d125-117">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="2d125-118">Execute Olá toocreate de comando a seguir uma tabela de rotas para sub-rede front-end hello:</span><span class="sxs-lookup"><span data-stu-id="2d125-118">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="2d125-119">Saída:</span><span class="sxs-lookup"><span data-stu-id="2d125-119">Output:</span></span>
   
        info:    Executing command network route-table create
        info:    Looking up route table "UDR-FrontEnd"
        info:    Creating route table "UDR-FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    Name                            : UDR-FrontEnd
        data:    Type                            : Microsoft.Network/routeTables
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        info:    network route-table create command OK
   
    <span data-ttu-id="2d125-120">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="2d125-120">Parameters:</span></span>
   
   * <span data-ttu-id="2d125-121">**-g (ou --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="2d125-121">**-g (or --resource-group)**.</span></span> <span data-ttu-id="2d125-122">Nome do grupo de recursos de saudação onde Olá UDR será criado.</span><span class="sxs-lookup"><span data-stu-id="2d125-122">Name of hello resource group where hello UDR will be created.</span></span> <span data-ttu-id="2d125-123">Para o nosso cenário, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="2d125-123">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="2d125-124">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="2d125-124">**-l (or --location)**.</span></span> <span data-ttu-id="2d125-125">Região do Azure onde hello UDR novo será criado.</span><span class="sxs-lookup"><span data-stu-id="2d125-125">Azure region where hello new UDR will be created.</span></span> <span data-ttu-id="2d125-126">Para o nosso cenário, *westus*.</span><span class="sxs-lookup"><span data-stu-id="2d125-126">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="2d125-127">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="2d125-127">**-n (or --name)**.</span></span> <span data-ttu-id="2d125-128">Nome para Olá UDR novo.</span><span class="sxs-lookup"><span data-stu-id="2d125-128">Name for hello new UDR.</span></span> <span data-ttu-id="2d125-129">Para nosso cenário, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="2d125-129">For our scenario, *UDR-FrontEnd*.</span></span>
2. <span data-ttu-id="2d125-130">Executar Olá após o comando toocreate uma rota no toosend de tabela de rota Olá todo o tráfego destinado toohello sub-rede de back-end (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="2d125-130">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -y VirtualAppliance -p 192.168.0.4
    ```
   
    <span data-ttu-id="2d125-131">Saída:</span><span class="sxs-lookup"><span data-stu-id="2d125-131">Output:</span></span>
   
        info:    Executing command network route-table route create
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        info:    Creating route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd/routes/RouteToBackEnd
        data:    Name                            : RouteToBackEnd
        data:    Provisioning state              : Succeeded
        data:    Next hop type                   : VirtualAppliance
        data:    Next hop IP address             : 192.168.0.4
        data:    Address prefix                  : 192.168.2.0/24
        info:    network route-table route create command OK
   
    <span data-ttu-id="2d125-132">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="2d125-132">Parameters:</span></span>
   
   * <span data-ttu-id="2d125-133">**-r (ou --route-table-name)**.</span><span class="sxs-lookup"><span data-stu-id="2d125-133">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="2d125-134">Nome da tabela de rota Olá onde rota Olá será adicionada.</span><span class="sxs-lookup"><span data-stu-id="2d125-134">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="2d125-135">Para nosso cenário, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="2d125-135">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="2d125-136">**-a (ou --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="2d125-136">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="2d125-137">Prefixo de endereço de sub-rede Olá onde os pacotes são destinados a.</span><span class="sxs-lookup"><span data-stu-id="2d125-137">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="2d125-138">Para nosso cenário, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="2d125-138">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="2d125-139">**-y (ou --next-hop-type)**.</span><span class="sxs-lookup"><span data-stu-id="2d125-139">**-y (or --next-hop-type)**.</span></span> <span data-ttu-id="2d125-140">Tipo de objeto ao qual o tráfego será enviado.</span><span class="sxs-lookup"><span data-stu-id="2d125-140">Type of object traffic will be sent to.</span></span> <span data-ttu-id="2d125-141">Os valores possíveis são *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* ou *None*.</span><span class="sxs-lookup"><span data-stu-id="2d125-141">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="2d125-142">**-p (ou --next-hop-ip-address**).</span><span class="sxs-lookup"><span data-stu-id="2d125-142">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="2d125-143">Endereço IP do próximo salto.</span><span class="sxs-lookup"><span data-stu-id="2d125-143">IP address for next hop.</span></span> <span data-ttu-id="2d125-144">Para o nosso cenário, *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="2d125-144">For our scenario, *192.168.0.4*.</span></span>
3. <span data-ttu-id="2d125-145">Tabela de rotas Olá tooassociate criada acima com hello comando a seguir de execução Olá **front-end** sub-rede:</span><span class="sxs-lookup"><span data-stu-id="2d125-145">Run hello following command tooassociate hello route table created above with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="2d125-146">Saída:</span><span class="sxs-lookup"><span data-stu-id="2d125-146">Output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    Route Table                     : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    IP configurations:
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConf
        igurations/ipconfig1
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB2/ipConf
        igurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK
   
    <span data-ttu-id="2d125-147">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="2d125-147">Parameters:</span></span>
   
   * <span data-ttu-id="2d125-148">**-e (ou --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="2d125-148">**-e (or --vnet-name)**.</span></span> <span data-ttu-id="2d125-149">Nome de rede virtual onde está localizada a sub-rede de saudação do hello.</span><span class="sxs-lookup"><span data-stu-id="2d125-149">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="2d125-150">Para o nosso cenário, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="2d125-150">For our scenario, *TestVNet*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="2d125-151">Criar hello UDR para a sub-rede de back-end Olá</span><span class="sxs-lookup"><span data-stu-id="2d125-151">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="2d125-152">tabela de rotas de saudação toocreate e rotear necessários para a sub-rede de back-end de saudação com base no cenário de saudação acima, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2d125-152">toocreate hello route table and route needed for hello back-end subnet based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="2d125-153">Execute Olá toocreate de comando a seguir uma tabela de rotas para sub-rede de back-end hello:</span><span class="sxs-lookup"><span data-stu-id="2d125-153">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-BackEnd -l westus
    ```

2. <span data-ttu-id="2d125-154">Executar Olá após o comando toocreate uma rota no toosend de tabela de rota Olá todo o tráfego destinado toohello sub-rede front-end (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="2d125-154">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -y VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="2d125-155">Execução hello após a tabela de rotas do comando tooassociate Olá com hello **back-end** sub-rede:</span><span class="sxs-lookup"><span data-stu-id="2d125-155">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -r UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="2d125-156">Habilite o encaminhamento de IP em FW1</span><span class="sxs-lookup"><span data-stu-id="2d125-156">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="2d125-157">encaminhamento de IP tooenable em Olá NIC usada por **FW1**completa Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2d125-157">tooenable IP forwarding in hello NIC used by **FW1**, complete hello following steps:</span></span>

1. <span data-ttu-id="2d125-158">Executar comando de saudação que segue e observe o valor de saudação para **encaminhamento IP habilitar**.</span><span class="sxs-lookup"><span data-stu-id="2d125-158">Run hello command that follows and notice hello value for **Enable IP forwarding**.</span></span> <span data-ttu-id="2d125-159">Ele deve ser definido muito*false*.</span><span class="sxs-lookup"><span data-stu-id="2d125-159">It should be set too*false*.</span></span>

    ```azurecli
    azure network nic show -g TestRG -n NICFW1
    ```

    <span data-ttu-id="2d125-160">Saída:</span><span class="sxs-lookup"><span data-stu-id="2d125-160">Output:</span></span>
   
        info:    Executing command network nic show
        info:    Looking up hello network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : false
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic show command OK
2. <span data-ttu-id="2d125-161">Execute Olá encaminhamento de IP de tooenable de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="2d125-161">Run hello following command tooenable IP forwarding:</span></span>

    ```azurecli
    azure network nic set -g TestRG -n NICFW1 -f true
    ```
   
    <span data-ttu-id="2d125-162">Saída:</span><span class="sxs-lookup"><span data-stu-id="2d125-162">Output:</span></span>
   
        info:    Executing command network nic set
        info:    Looking up hello network interface "NICFW1"
        info:    Updating network interface "NICFW1"
        info:    Looking up hello network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : true
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic set command OK
   
    <span data-ttu-id="2d125-163">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="2d125-163">Parameters:</span></span>
   
   * <span data-ttu-id="2d125-164">**-f (ou --enable-ip-forwarding)**.</span><span class="sxs-lookup"><span data-stu-id="2d125-164">**-f (or --enable-ip-forwarding)**.</span></span> <span data-ttu-id="2d125-165">*true* ou *false*.</span><span class="sxs-lookup"><span data-stu-id="2d125-165">*true* or *false*.</span></span>

