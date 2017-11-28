---
title: Controlar dispositivos virtuais e de roteamento usando a CLI do Azure 1.0 | Microsoft Docs
description: Aprenda a controlar dispositivos virtuais e de roteamento usando a CLI do Azure 1.0.
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
ms.openlocfilehash: 5f21bc7a4fcd9507ea9d6b2b752a2328a7b834f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-user-defined-routes-udr-using-the-azure-cli-10"></a><span data-ttu-id="0664b-103">Criar UDRs (Rotas Definidas pelo Usuário) usando a CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="0664b-103">Create User-Defined Routes (UDR) using the Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0664b-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0664b-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="0664b-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="0664b-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="0664b-106">Modelo</span><span class="sxs-lookup"><span data-stu-id="0664b-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="0664b-107">PowerShell (Clássico)</span><span class="sxs-lookup"><span data-stu-id="0664b-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="0664b-108">CLI (Clássica)</span><span class="sxs-lookup"><span data-stu-id="0664b-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

<span data-ttu-id="0664b-109">Crie dispositivos virtuais e de roteamento personalizados usando a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="0664b-109">Create custom routing and virtual appliances using the Azure CLI.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="0664b-110">Versões da CLI para concluir a tarefa</span><span class="sxs-lookup"><span data-stu-id="0664b-110">CLI versions to complete the task</span></span> 

<span data-ttu-id="0664b-111">Você pode concluir a tarefa usando uma das seguintes versões da CLI:</span><span class="sxs-lookup"><span data-stu-id="0664b-111">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="0664b-112">[CLI 1.0 do Azure](#Create-the-UDR-for-the-front-end-subnet) – nossa CLI para os modelos de implantação clássico e de gerenciamento de recursos (este artigo)</span><span class="sxs-lookup"><span data-stu-id="0664b-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="0664b-113">[CLI 2.0 do Azure](virtual-network-create-udr-arm-cli.md) – nossa última geração de CLI para o modelo de implantação de gerenciamento de recursos</span><span class="sxs-lookup"><span data-stu-id="0664b-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) - our next generation CLI for the resource management deployment model</span></span> 


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="0664b-114">Os comandos da CLI do Azure de exemplo abaixo esperam um ambiente simples já criado com base no cenário acima.</span><span class="sxs-lookup"><span data-stu-id="0664b-114">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="0664b-115">Se você quiser executar os comandos conforme eles são exibidos neste documento, primeiro crie o ambiente de teste ao implantar [esse modelo](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), clique em **Implantar no Azure**, substitua os valores de parâmetro padrão, se necessário, e siga as instruções no portal.</span><span class="sxs-lookup"><span data-stu-id="0664b-115">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>


## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="0664b-116">Criar a UDR para a sub-rede de front-end</span><span class="sxs-lookup"><span data-stu-id="0664b-116">Create the UDR for the front-end subnet</span></span>
<span data-ttu-id="0664b-117">Para criar a tabela de rotas e a rota necessária para a sub-rede de front-end com base no cenário acima, siga as etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="0664b-117">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="0664b-118">Execute o comando a seguir para criar uma tabela de rota para a sub-rede de front-end:</span><span class="sxs-lookup"><span data-stu-id="0664b-118">Run the following command to create a route table for the front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="0664b-119">Saída:</span><span class="sxs-lookup"><span data-stu-id="0664b-119">Output:</span></span>
   
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
   
    <span data-ttu-id="0664b-120">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="0664b-120">Parameters:</span></span>
   
   * <span data-ttu-id="0664b-121">**-g (ou --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="0664b-121">**-g (or --resource-group)**.</span></span> <span data-ttu-id="0664b-122">Nome do grupo de recursos em que a UDR será criada.</span><span class="sxs-lookup"><span data-stu-id="0664b-122">Name of the resource group where the UDR will be created.</span></span> <span data-ttu-id="0664b-123">Para o nosso cenário, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="0664b-123">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="0664b-124">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="0664b-124">**-l (or --location)**.</span></span> <span data-ttu-id="0664b-125">Região do Azure em que a nova UDR será criada.</span><span class="sxs-lookup"><span data-stu-id="0664b-125">Azure region where the new UDR will be created.</span></span> <span data-ttu-id="0664b-126">Para o nosso cenário, *westus*.</span><span class="sxs-lookup"><span data-stu-id="0664b-126">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="0664b-127">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="0664b-127">**-n (or --name)**.</span></span> <span data-ttu-id="0664b-128">Nome da nova UDR.</span><span class="sxs-lookup"><span data-stu-id="0664b-128">Name for the new UDR.</span></span> <span data-ttu-id="0664b-129">Para nosso cenário, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="0664b-129">For our scenario, *UDR-FrontEnd*.</span></span>
2. <span data-ttu-id="0664b-130">Execute o comando a seguir para criar uma rota na tabela de rotas para enviar todo o tráfego destinado à sub-rede de back-end (192.168.2.0/24) para a VM **FW1** (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="0664b-130">Run the following command to create a route in the route table to send all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -y VirtualAppliance -p 192.168.0.4
    ```
   
    <span data-ttu-id="0664b-131">Saída:</span><span class="sxs-lookup"><span data-stu-id="0664b-131">Output:</span></span>
   
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
   
    <span data-ttu-id="0664b-132">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="0664b-132">Parameters:</span></span>
   
   * <span data-ttu-id="0664b-133">**-r (ou --route-table-name)**.</span><span class="sxs-lookup"><span data-stu-id="0664b-133">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="0664b-134">Nome da tabela de rotas à qual a rota será adicionada.</span><span class="sxs-lookup"><span data-stu-id="0664b-134">Name of the route table where the route will be added.</span></span> <span data-ttu-id="0664b-135">Para nosso cenário, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="0664b-135">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="0664b-136">**-a (ou --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="0664b-136">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="0664b-137">Prefixo de endereço para a sub-rede à qual os pacotes são destinados.</span><span class="sxs-lookup"><span data-stu-id="0664b-137">Address prefix for the subnet where packets are destined to.</span></span> <span data-ttu-id="0664b-138">Para nosso cenário, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="0664b-138">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="0664b-139">**-y (ou --next-hop-type)**.</span><span class="sxs-lookup"><span data-stu-id="0664b-139">**-y (or --next-hop-type)**.</span></span> <span data-ttu-id="0664b-140">Tipo de objeto ao qual o tráfego será enviado.</span><span class="sxs-lookup"><span data-stu-id="0664b-140">Type of object traffic will be sent to.</span></span> <span data-ttu-id="0664b-141">Os valores possíveis são *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* ou *None*.</span><span class="sxs-lookup"><span data-stu-id="0664b-141">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="0664b-142">**-p (ou --next-hop-ip-address**).</span><span class="sxs-lookup"><span data-stu-id="0664b-142">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="0664b-143">Endereço IP do próximo salto.</span><span class="sxs-lookup"><span data-stu-id="0664b-143">IP address for next hop.</span></span> <span data-ttu-id="0664b-144">Para o nosso cenário, *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="0664b-144">For our scenario, *192.168.0.4*.</span></span>
3. <span data-ttu-id="0664b-145">Execute o comando a seguir para associar a tabela de rotas criada acima à sub-rede de **FrontEnd**:</span><span class="sxs-lookup"><span data-stu-id="0664b-145">Run the following command to associate the route table created above with the **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="0664b-146">Saída:</span><span class="sxs-lookup"><span data-stu-id="0664b-146">Output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up the subnet "FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up the subnet "FrontEnd"
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
   
    <span data-ttu-id="0664b-147">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="0664b-147">Parameters:</span></span>
   
   * <span data-ttu-id="0664b-148">**-e (ou --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="0664b-148">**-e (or --vnet-name)**.</span></span> <span data-ttu-id="0664b-149">Nome da VNet na qual a sub-rede está localizada.</span><span class="sxs-lookup"><span data-stu-id="0664b-149">Name of the VNet where the subnet is located.</span></span> <span data-ttu-id="0664b-150">Para o nosso cenário, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="0664b-150">For our scenario, *TestVNet*.</span></span>

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="0664b-151">Criar o UDR para a sub-rede de back-end</span><span class="sxs-lookup"><span data-stu-id="0664b-151">Create the UDR for the back-end subnet</span></span>
<span data-ttu-id="0664b-152">Para criar a tabela de rotas e a rota necessária para a sub-rede de back-end com base no cenário acima, conclua as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0664b-152">To create the route table and route needed for the back-end subnet based on the scenario above, complete the following steps:</span></span>

1. <span data-ttu-id="0664b-153">Execute o comando a seguir para criar uma tabela de rota para a sub-rede de back-end:</span><span class="sxs-lookup"><span data-stu-id="0664b-153">Run the following command to create a route table for the back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-BackEnd -l westus
    ```

2. <span data-ttu-id="0664b-154">Execute o comando a seguir para criar uma rota na tabela de rotas para enviar todo o tráfego destinado à sub-rede de front-end (192.168.1.0/24) para a VM **FW1** (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="0664b-154">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -y VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="0664b-155">Execute o comando a seguir para associar a tabela de rotas à sub-rede de **BackEnd**:</span><span class="sxs-lookup"><span data-stu-id="0664b-155">Run the following command to associate the route table with the **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -r UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="0664b-156">Habilite o encaminhamento de IP em FW1</span><span class="sxs-lookup"><span data-stu-id="0664b-156">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="0664b-157">Para habilitar o encaminhamento IP na NIC usada por **FW1**, conclua as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="0664b-157">To enable IP forwarding in the NIC used by **FW1**, complete the following steps:</span></span>

1. <span data-ttu-id="0664b-158">Execute o comando a seguir e observe o valor para **Habilitar encaminhamento IP**.</span><span class="sxs-lookup"><span data-stu-id="0664b-158">Run the command that follows and notice the value for **Enable IP forwarding**.</span></span> <span data-ttu-id="0664b-159">Ele deve ser definido como *falso*.</span><span class="sxs-lookup"><span data-stu-id="0664b-159">It should be set to *false*.</span></span>

    ```azurecli
    azure network nic show -g TestRG -n NICFW1
    ```

    <span data-ttu-id="0664b-160">Saída:</span><span class="sxs-lookup"><span data-stu-id="0664b-160">Output:</span></span>
   
        info:    Executing command network nic show
        info:    Looking up the network interface "NICFW1"
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
2. <span data-ttu-id="0664b-161">Execute o seguinte comando para habilitar o encaminhamento IP:</span><span class="sxs-lookup"><span data-stu-id="0664b-161">Run the following command to enable IP forwarding:</span></span>

    ```azurecli
    azure network nic set -g TestRG -n NICFW1 -f true
    ```
   
    <span data-ttu-id="0664b-162">Saída:</span><span class="sxs-lookup"><span data-stu-id="0664b-162">Output:</span></span>
   
        info:    Executing command network nic set
        info:    Looking up the network interface "NICFW1"
        info:    Updating network interface "NICFW1"
        info:    Looking up the network interface "NICFW1"
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
   
    <span data-ttu-id="0664b-163">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="0664b-163">Parameters:</span></span>
   
   * <span data-ttu-id="0664b-164">**-f (ou --enable-ip-forwarding)**.</span><span class="sxs-lookup"><span data-stu-id="0664b-164">**-f (or --enable-ip-forwarding)**.</span></span> <span data-ttu-id="0664b-165">*true* ou *false*.</span><span class="sxs-lookup"><span data-stu-id="0664b-165">*true* or *false*.</span></span>

