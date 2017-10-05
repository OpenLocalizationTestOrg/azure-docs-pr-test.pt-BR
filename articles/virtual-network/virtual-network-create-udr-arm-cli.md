---
title: Controlar dispositivos virtuais e de roteamento usando a CLI do Azure 2.0 | Microsoft Docs
description: Aprenda a controlar dispositivos virtuais e de roteamento usando a CLI do Azure 2.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5452a0b8-21a6-4699-8d6a-e2d8faf32c25
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/12/2017
ms.author: jdial
ms.openlocfilehash: e5d9519998346619093f443b740c8904283f76e8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-user-defined-routes-udr-using-the-azure-cli-20"></a><span data-ttu-id="93a70-103">Criar UDRs (Rotas Definidas pelo Usuário) usando a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="93a70-103">Create User-Defined Routes (UDR) using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="93a70-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="93a70-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="93a70-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="93a70-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="93a70-106">Modelo</span><span class="sxs-lookup"><span data-stu-id="93a70-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="93a70-107">PowerShell (Implantação clássica)</span><span class="sxs-lookup"><span data-stu-id="93a70-107">PowerShell (Classic deployment)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="93a70-108">CLI (Implantação clássica)</span><span class="sxs-lookup"><span data-stu-id="93a70-108">CLI (Classic deployment)</span></span>](virtual-network-create-udr-classic-cli.md)

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="93a70-109">Versões da CLI para concluir a tarefa</span><span class="sxs-lookup"><span data-stu-id="93a70-109">CLI versions to complete the task</span></span> 

<span data-ttu-id="93a70-110">Você pode concluir a tarefa usando uma das seguintes versões da CLI:</span><span class="sxs-lookup"><span data-stu-id="93a70-110">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="93a70-111">[CLI do Azure 1.0](virtual-network-create-udr-arm-cli-nodejs.md) – nossa CLI para os modelos de implantação clássico e de gerenciamento de recursos</span><span class="sxs-lookup"><span data-stu-id="93a70-111">[Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span> 
- <span data-ttu-id="93a70-112">[CLI do Azure 2.0](#Create-the-UDR-for-the-front-end-subnet) – nossa CLI da próxima geração para o modelo de implantação do resource manager (este artigo)</span><span class="sxs-lookup"><span data-stu-id="93a70-112">[Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) - our next generation CLI for the resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="93a70-113">Os comandos da CLI do Azure de exemplo abaixo esperam um ambiente simples já criado com base no cenário acima.</span><span class="sxs-lookup"><span data-stu-id="93a70-113">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="93a70-114">Se você quiser executar os comandos conforme eles são exibidos neste documento, primeiro crie o ambiente de teste ao implantar [esse modelo](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), clique em **Implantar no Azure**, substitua os valores de parâmetro padrão, se necessário, e siga as instruções no portal.</span><span class="sxs-lookup"><span data-stu-id="93a70-114">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>


## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="93a70-115">Criar a UDR para a sub-rede de front-end</span><span class="sxs-lookup"><span data-stu-id="93a70-115">Create the UDR for the front-end subnet</span></span>
<span data-ttu-id="93a70-116">Para criar a tabela de rotas e a rota necessária para a sub-rede de front-end com base no cenário acima, siga as etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="93a70-116">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="93a70-117">Criar uma tabela de rota para a sub-rede front-end com o comando [az network route-table create](/cli/azure/network/route-table#create):</span><span class="sxs-lookup"><span data-stu-id="93a70-117">Create a route table for the front-end subnet with the [az network route-table create](/cli/azure/network/route-table#create) command:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --location centralus \
    --name UDR-FrontEnd
    ```

    <span data-ttu-id="93a70-118">Saída:</span><span class="sxs-lookup"><span data-stu-id="93a70-118">Output:</span></span>

    ```json
    {
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
    "location": "centralus",
    "name": "UDR-FrontEnd",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "routes": [],
    "subnets": null,
    "tags": null,
    "type": "Microsoft.Network/routeTables"
    }
    ```

2. <span data-ttu-id="93a70-119">Crie uma rota que envia todo o tráfego destinado à sub-rede de back-end (192.168.2.0/24) para a VM **FW1** (192.168.0.4) com o comando [az network route-table route create](/cli/azure/network/route-table/route#create):</span><span class="sxs-lookup"><span data-stu-id="93a70-119">Create a route that sends all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4) using the [az network route-table route create](/cli/azure/network/route-table/route#create) command:</span></span>

    ```azurecli 
    az network route-table route create \
    --resource-group testrg \
    --name RouteToBackEnd \
    --route-table-name UDR-FrontEnd \
    --address-prefix 192.168.2.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

    <span data-ttu-id="93a70-120">Saída:</span><span class="sxs-lookup"><span data-stu-id="93a70-120">Output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd/routes/RouteToBackEnd",
    "name": "RouteToBackEnd",
    "nextHopIpAddress": "192.168.0.4",
    "nextHopType": "VirtualAppliance",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg"
    }
    ```
    <span data-ttu-id="93a70-121">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="93a70-121">Parameters:</span></span>

    * <span data-ttu-id="93a70-122">**--route-table-name**.</span><span class="sxs-lookup"><span data-stu-id="93a70-122">**--route-table-name**.</span></span> <span data-ttu-id="93a70-123">Nome da tabela de rotas à qual a rota será adicionada.</span><span class="sxs-lookup"><span data-stu-id="93a70-123">Name of the route table where the route will be added.</span></span> <span data-ttu-id="93a70-124">Para nosso cenário, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="93a70-124">For our scenario, *UDR-FrontEnd*.</span></span>
    * <span data-ttu-id="93a70-125">**--address-prefix**.</span><span class="sxs-lookup"><span data-stu-id="93a70-125">**--address-prefix**.</span></span> <span data-ttu-id="93a70-126">Prefixo de endereço para a sub-rede à qual os pacotes são destinados.</span><span class="sxs-lookup"><span data-stu-id="93a70-126">Address prefix for the subnet where packets are destined to.</span></span> <span data-ttu-id="93a70-127">Para nosso cenário, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="93a70-127">For our scenario, *192.168.2.0/24*.</span></span>
    * <span data-ttu-id="93a70-128">**--next-hop-type**.</span><span class="sxs-lookup"><span data-stu-id="93a70-128">**--next-hop-type**.</span></span> <span data-ttu-id="93a70-129">Tipo de objeto ao qual o tráfego será enviado.</span><span class="sxs-lookup"><span data-stu-id="93a70-129">Type of object traffic will be sent to.</span></span> <span data-ttu-id="93a70-130">Os valores possíveis são *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* ou *None*.</span><span class="sxs-lookup"><span data-stu-id="93a70-130">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
    * <span data-ttu-id="93a70-131">**--next-hop-ip-address**.</span><span class="sxs-lookup"><span data-stu-id="93a70-131">**--next-hop-ip-address**.</span></span> <span data-ttu-id="93a70-132">Endereço IP do próximo salto.</span><span class="sxs-lookup"><span data-stu-id="93a70-132">IP address for next hop.</span></span> <span data-ttu-id="93a70-133">Para o nosso cenário, *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="93a70-133">For our scenario, *192.168.0.4*.</span></span>

3. <span data-ttu-id="93a70-134">Execute o comando [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) para associar a tabela de rotas criada acima à sub-rede de **FrontEnd**:</span><span class="sxs-lookup"><span data-stu-id="93a70-134">Run the [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command to associate the route table created above with the **FrontEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name FrontEnd \
    --route-table UDR-FrontEnd
    ```

    <span data-ttu-id="93a70-135">Saída:</span><span class="sxs-lookup"><span data-stu-id="93a70-135">Output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.1.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testvnet/subnets/FrontEnd",
    "ipConfigurations": null,
    "name": "FrontEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": {
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
        "location": null,
        "name": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "routes": null,
        "subnets": null,
        "tags": null,
        "type": null
        }
    }
    ```

    <span data-ttu-id="93a70-136">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="93a70-136">Parameters:</span></span>
    
    * <span data-ttu-id="93a70-137">**--vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="93a70-137">**--vnet-name**.</span></span> <span data-ttu-id="93a70-138">Nome da VNet na qual a sub-rede está localizada.</span><span class="sxs-lookup"><span data-stu-id="93a70-138">Name of the VNet where the subnet is located.</span></span> <span data-ttu-id="93a70-139">Para o nosso cenário, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="93a70-139">For our scenario, *TestVNet*.</span></span>

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="93a70-140">Criar o UDR para a sub-rede de back-end</span><span class="sxs-lookup"><span data-stu-id="93a70-140">Create the UDR for the back-end subnet</span></span>

<span data-ttu-id="93a70-141">Para criar a tabela de rotas e a rota necessária para a sub-rede de back-end com base no cenário acima, conclua as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="93a70-141">To create the route table and route needed for the back-end subnet based on the scenario above, complete the following steps:</span></span>

1. <span data-ttu-id="93a70-142">Execute o comando a seguir para criar uma tabela de rota para a sub-rede de back-end:</span><span class="sxs-lookup"><span data-stu-id="93a70-142">Run the following command to create a route table for the back-end subnet:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --name UDR-BackEnd \
    --location centralus
    ```

2. <span data-ttu-id="93a70-143">Execute o comando a seguir para criar uma rota na tabela de rotas para enviar todo o tráfego destinado à sub-rede de front-end (192.168.1.0/24) para a VM **FW1** (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="93a70-143">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    az network route-table route create \
    --resource-group testrg \
    --name RouteToFrontEnd \
    --route-table-name UDR-BackEnd \
    --address-prefix 192.168.1.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

3. <span data-ttu-id="93a70-144">Execute o comando a seguir para associar a tabela de rotas à sub-rede de **BackEnd**:</span><span class="sxs-lookup"><span data-stu-id="93a70-144">Run the following command to associate the route table with the **BackEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name BackEnd \
    --route-table UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="93a70-145">Habilite o encaminhamento de IP em FW1</span><span class="sxs-lookup"><span data-stu-id="93a70-145">Enable IP forwarding on FW1</span></span>

<span data-ttu-id="93a70-146">Para habilitar o encaminhamento IP na NIC usada por **FW1**, conclua as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="93a70-146">To enable IP forwarding in the NIC used by **FW1**, complete the following steps:</span></span>

1. <span data-ttu-id="93a70-147">Execute o comando [az network nic show](/cli/azure/network/nic#show) com um filtro JMESPATH para exibir o valor atual de **enable-ip-forwarding** para **Habilitar encaminhamento de IP**.</span><span class="sxs-lookup"><span data-stu-id="93a70-147">Run the [az network nic show](/cli/azure/network/nic#show) command with a JMESPATH filter to display the current **enable-ip-forwarding** value for **Enable IP forwarding**.</span></span> <span data-ttu-id="93a70-148">Ele deve ser definido como *falso*.</span><span class="sxs-lookup"><span data-stu-id="93a70-148">It should be set to *false*.</span></span>

    ```azurecli
    az network nic show \
    --resource-group testrg \
    --nname nicfw1 \
    --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="93a70-149">Saída:</span><span class="sxs-lookup"><span data-stu-id="93a70-149">Output:</span></span>

        false

2. <span data-ttu-id="93a70-150">Execute o seguinte comando para habilitar o encaminhamento IP:</span><span class="sxs-lookup"><span data-stu-id="93a70-150">Run the following command to enable IP forwarding:</span></span>

    ```azurecli
    az network nic update \
    --resource-group testrg \
    --name nicfw1 \
    --ip-forwarding true
    ```

    <span data-ttu-id="93a70-151">Você pode examinar a saída transmitida ao console ou apenas testar novamente para um valor de **enableIpForwarding** específico:</span><span class="sxs-lookup"><span data-stu-id="93a70-151">You can examine the output streamed to the console, or just retest for the specific **enableIpForwarding** value:</span></span>

    ```azurecli
    az network nic show -g testrg -n nicfw1 --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="93a70-152">Saída:</span><span class="sxs-lookup"><span data-stu-id="93a70-152">Output:</span></span>

        true

    <span data-ttu-id="93a70-153">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="93a70-153">Parameters:</span></span>

    <span data-ttu-id="93a70-154">**--ip-forwarding**: *true* ou *false*.</span><span class="sxs-lookup"><span data-stu-id="93a70-154">**--ip-forwarding**: *true* or *false*.</span></span>

