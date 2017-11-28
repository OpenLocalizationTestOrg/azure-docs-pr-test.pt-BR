---
title: "dispositivos de roteamento e virtual de aaaControl usando Olá 2.0 do CLI do Azure | Microsoft Docs"
description: "Saiba como dispositivos de roteamento e virtual de toocontrol usando Olá 2.0 do CLI do Azure."
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
ms.openlocfilehash: 79b908848932a4365dab1b7497b6a0dbf44bbaf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-20"></a><span data-ttu-id="9044f-103">Criar rotas definidas pelo usuário (UDR) usando Olá 2.0 do CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="9044f-103">Create User-Defined Routes (UDR) using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9044f-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9044f-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="9044f-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="9044f-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="9044f-106">Modelo</span><span class="sxs-lookup"><span data-stu-id="9044f-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="9044f-107">PowerShell (Implantação clássica)</span><span class="sxs-lookup"><span data-stu-id="9044f-107">PowerShell (Classic deployment)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="9044f-108">CLI (Implantação clássica)</span><span class="sxs-lookup"><span data-stu-id="9044f-108">CLI (Classic deployment)</span></span>](virtual-network-create-udr-classic-cli.md)

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="9044f-109">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="9044f-109">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="9044f-110">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="9044f-110">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="9044f-111">[1.0 de CLI do Azure](virtual-network-create-udr-arm-cli-nodejs.md) – nosso CLI para modelos de implantação de gerenciamento de recursos e clássico de Olá</span><span class="sxs-lookup"><span data-stu-id="9044f-111">[Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="9044f-112">[2.0 do CLI do Azure](#Create-the-UDR-for-the-front-end-subnet) -nossa próxima geração CLI para modelo de implantação de gerenciamento de recursos de saudação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="9044f-112">[Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="9044f-113">comandos de CLI do Azure de exemplo Hello abaixo esperam um ambiente simples já criado com base no cenário de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="9044f-113">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="9044f-114">Se você quiser comandos de saudação toorun conforme elas são exibidas neste documento, primeiro criar o ambiente de teste Olá implantando [este modelo](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), clique em **implantar tooAzure**, substitua os valores de parâmetro padrão Olá Se necessário e siga as instruções de saudação em Olá portal.</span><span class="sxs-lookup"><span data-stu-id="9044f-114">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>


## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="9044f-115">Criar hello UDR para sub-rede front-end Olá</span><span class="sxs-lookup"><span data-stu-id="9044f-115">Create hello UDR for hello front-end subnet</span></span>
<span data-ttu-id="9044f-116">tabela de rotas toocreate hello e rotas necessárias para a sub-rede de front-end de saudação com base no cenário de saudação acima, siga as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="9044f-116">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="9044f-117">Criar uma tabela de rotas para sub-rede front-end Olá com hello [criar tabela de rotas de rede de az](/cli/azure/network/route-table#create) comando:</span><span class="sxs-lookup"><span data-stu-id="9044f-117">Create a route table for hello front-end subnet with hello [az network route-table create](/cli/azure/network/route-table#create) command:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --location centralus \
    --name UDR-FrontEnd
    ```

    <span data-ttu-id="9044f-118">Saída:</span><span class="sxs-lookup"><span data-stu-id="9044f-118">Output:</span></span>

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

2. <span data-ttu-id="9044f-119">Crie uma rota que envia todo o tráfego destinado toohello sub-rede de back-end (192.168.2.0/24) toohello **FW1** VM (192.168.0.4) usando Olá [criar rota de tabela de rotas de rede az](/cli/azure/network/route-table/route#create) comando:</span><span class="sxs-lookup"><span data-stu-id="9044f-119">Create a route that sends all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4) using hello [az network route-table route create](/cli/azure/network/route-table/route#create) command:</span></span>

    ```azurecli 
    az network route-table route create \
    --resource-group testrg \
    --name RouteToBackEnd \
    --route-table-name UDR-FrontEnd \
    --address-prefix 192.168.2.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

    <span data-ttu-id="9044f-120">Saída:</span><span class="sxs-lookup"><span data-stu-id="9044f-120">Output:</span></span>

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
    <span data-ttu-id="9044f-121">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="9044f-121">Parameters:</span></span>

    * <span data-ttu-id="9044f-122">**--route-table-name**.</span><span class="sxs-lookup"><span data-stu-id="9044f-122">**--route-table-name**.</span></span> <span data-ttu-id="9044f-123">Nome da tabela de rota Olá onde rota Olá será adicionada.</span><span class="sxs-lookup"><span data-stu-id="9044f-123">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="9044f-124">Para nosso cenário, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="9044f-124">For our scenario, *UDR-FrontEnd*.</span></span>
    * <span data-ttu-id="9044f-125">**--address-prefix**.</span><span class="sxs-lookup"><span data-stu-id="9044f-125">**--address-prefix**.</span></span> <span data-ttu-id="9044f-126">Prefixo de endereço de sub-rede Olá onde os pacotes são destinados a.</span><span class="sxs-lookup"><span data-stu-id="9044f-126">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="9044f-127">Para nosso cenário, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="9044f-127">For our scenario, *192.168.2.0/24*.</span></span>
    * <span data-ttu-id="9044f-128">**--next-hop-type**.</span><span class="sxs-lookup"><span data-stu-id="9044f-128">**--next-hop-type**.</span></span> <span data-ttu-id="9044f-129">Tipo de objeto ao qual o tráfego será enviado.</span><span class="sxs-lookup"><span data-stu-id="9044f-129">Type of object traffic will be sent to.</span></span> <span data-ttu-id="9044f-130">Os valores possíveis são *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* ou *None*.</span><span class="sxs-lookup"><span data-stu-id="9044f-130">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
    * <span data-ttu-id="9044f-131">**--next-hop-ip-address**.</span><span class="sxs-lookup"><span data-stu-id="9044f-131">**--next-hop-ip-address**.</span></span> <span data-ttu-id="9044f-132">Endereço IP do próximo salto.</span><span class="sxs-lookup"><span data-stu-id="9044f-132">IP address for next hop.</span></span> <span data-ttu-id="9044f-133">Para o nosso cenário, *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="9044f-133">For our scenario, *192.168.0.4*.</span></span>

3. <span data-ttu-id="9044f-134">Executar Olá [atualização de sub-rede da rede virtual de rede az](/cli/azure/network/vnet/subnet#update) tabela de rotas do comando tooassociate Olá criado acima com hello **front-end** sub-rede:</span><span class="sxs-lookup"><span data-stu-id="9044f-134">Run hello [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command tooassociate hello route table created above with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name FrontEnd \
    --route-table UDR-FrontEnd
    ```

    <span data-ttu-id="9044f-135">Saída:</span><span class="sxs-lookup"><span data-stu-id="9044f-135">Output:</span></span>

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

    <span data-ttu-id="9044f-136">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="9044f-136">Parameters:</span></span>
    
    * <span data-ttu-id="9044f-137">**--vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="9044f-137">**--vnet-name**.</span></span> <span data-ttu-id="9044f-138">Nome de rede virtual onde está localizada a sub-rede de saudação do hello.</span><span class="sxs-lookup"><span data-stu-id="9044f-138">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="9044f-139">Para o nosso cenário, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="9044f-139">For our scenario, *TestVNet*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="9044f-140">Criar hello UDR para a sub-rede de back-end Olá</span><span class="sxs-lookup"><span data-stu-id="9044f-140">Create hello UDR for hello back-end subnet</span></span>

<span data-ttu-id="9044f-141">tabela de rotas de saudação toocreate e rotear necessários para a sub-rede de back-end de saudação com base no cenário de saudação acima, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9044f-141">toocreate hello route table and route needed for hello back-end subnet based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="9044f-142">Execute Olá toocreate de comando a seguir uma tabela de rotas para sub-rede de back-end hello:</span><span class="sxs-lookup"><span data-stu-id="9044f-142">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --name UDR-BackEnd \
    --location centralus
    ```

2. <span data-ttu-id="9044f-143">Executar Olá após o comando toocreate uma rota no toosend de tabela de rota Olá todo o tráfego destinado toohello sub-rede front-end (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="9044f-143">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    az network route-table route create \
    --resource-group testrg \
    --name RouteToFrontEnd \
    --route-table-name UDR-BackEnd \
    --address-prefix 192.168.1.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

3. <span data-ttu-id="9044f-144">Execução hello após a tabela de rotas do comando tooassociate Olá com hello **back-end** sub-rede:</span><span class="sxs-lookup"><span data-stu-id="9044f-144">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name BackEnd \
    --route-table UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="9044f-145">Habilite o encaminhamento de IP em FW1</span><span class="sxs-lookup"><span data-stu-id="9044f-145">Enable IP forwarding on FW1</span></span>

<span data-ttu-id="9044f-146">encaminhamento de IP tooenable em Olá NIC usada por **FW1**completa Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="9044f-146">tooenable IP forwarding in hello NIC used by **FW1**, complete hello following steps:</span></span>

1. <span data-ttu-id="9044f-147">Executar Olá [Mostrar de nic de rede az](/cli/azure/network/nic#show) com uma saudação de toodisplay JMESPATH filtro atual **ativar encaminhamento ip** valor para **encaminhamento IP habilitar**.</span><span class="sxs-lookup"><span data-stu-id="9044f-147">Run hello [az network nic show](/cli/azure/network/nic#show) command with a JMESPATH filter toodisplay hello current **enable-ip-forwarding** value for **Enable IP forwarding**.</span></span> <span data-ttu-id="9044f-148">Ele deve ser definido muito*false*.</span><span class="sxs-lookup"><span data-stu-id="9044f-148">It should be set too*false*.</span></span>

    ```azurecli
    az network nic show \
    --resource-group testrg \
    --nname nicfw1 \
    --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="9044f-149">Saída:</span><span class="sxs-lookup"><span data-stu-id="9044f-149">Output:</span></span>

        false

2. <span data-ttu-id="9044f-150">Execute Olá encaminhamento de IP de tooenable de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9044f-150">Run hello following command tooenable IP forwarding:</span></span>

    ```azurecli
    az network nic update \
    --resource-group testrg \
    --name nicfw1 \
    --ip-forwarding true
    ```

    <span data-ttu-id="9044f-151">Você pode examinar o console de toohello em fluxo de saída de hello ou apenas testar novamente para Olá específico **enableIpForwarding** valor:</span><span class="sxs-lookup"><span data-stu-id="9044f-151">You can examine hello output streamed toohello console, or just retest for hello specific **enableIpForwarding** value:</span></span>

    ```azurecli
    az network nic show -g testrg -n nicfw1 --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="9044f-152">Saída:</span><span class="sxs-lookup"><span data-stu-id="9044f-152">Output:</span></span>

        true

    <span data-ttu-id="9044f-153">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="9044f-153">Parameters:</span></span>

    <span data-ttu-id="9044f-154">**--ip-forwarding**: *true* ou *false*.</span><span class="sxs-lookup"><span data-stu-id="9044f-154">**--ip-forwarding**: *true* or *false*.</span></span>

