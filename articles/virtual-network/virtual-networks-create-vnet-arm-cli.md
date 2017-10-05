---
title: Criar uma rede virtual - CLI do Azure 2.0 | Microsoft Docs
description: Saiba como criar uma rede virtual usando a CLI do Azure 2.0.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 75966bcc-0056-4667-8482-6f08ca38e77a
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c7d7b3543f488aedff1ea2c68a2b497e0ca744af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-network-using-the-azure-cli-20"></a><span data-ttu-id="ee1c6-103">Criar uma rede virtual usando a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="ee1c6-103">Create a virtual network using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="ee1c6-104">O Azure tem dois modelos de implantação: Azure Resource Manager e clássico.</span><span class="sxs-lookup"><span data-stu-id="ee1c6-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="ee1c6-105">A Microsoft recomenda criar recursos por meio do modelo de implantação do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="ee1c6-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="ee1c6-106">Para saber mais sobre as diferenças entre os dois modelos, leia o artigo [Entender os modelos de implantação do Azure](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ee1c6-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="ee1c6-107">Versões da CLI para concluir a tarefa</span><span class="sxs-lookup"><span data-stu-id="ee1c6-107">CLI versions to complete the task</span></span>
<span data-ttu-id="ee1c6-108">Você pode concluir a tarefa usando uma das seguintes versões da CLI:</span><span class="sxs-lookup"><span data-stu-id="ee1c6-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="ee1c6-109">[CLI do Azure 1.0](virtual-networks-create-vnet-cli-nodejs.md) – nossa CLI para os modelos de implantação clássico e de gerenciamento de recursos</span><span class="sxs-lookup"><span data-stu-id="ee1c6-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span>
- <span data-ttu-id="ee1c6-110">[CLI do Azure 2.0](#create-a-virtual-network) – nossa CLI da próxima geração para o modelo de implantação do resource manager (este artigo)</span><span class="sxs-lookup"><span data-stu-id="ee1c6-110">[Azure CLI 2.0](#create-a-virtual-network) - our next generation CLI for the resource management deployment model (this article)\`</span></span>
 
    <span data-ttu-id="ee1c6-111">Você também pode criar uma rede virtual por meio do Gerenciador de Recursos usando outras ferramentas ou criar uma rede virtual por meio do modelo de implantação clássico, selecionando uma opção diferente na seguinte lista:</span><span class="sxs-lookup"><span data-stu-id="ee1c6-111">You can also create a VNet through Resource Manager using other tools or create a VNet through the classic deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ee1c6-112">Portal</span><span class="sxs-lookup"><span data-stu-id="ee1c6-112">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="ee1c6-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ee1c6-113">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="ee1c6-114">CLI</span><span class="sxs-lookup"><span data-stu-id="ee1c6-114">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="ee1c6-115">Modelo</span><span class="sxs-lookup"><span data-stu-id="ee1c6-115">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="ee1c6-116">Portal (clássico)</span><span class="sxs-lookup"><span data-stu-id="ee1c6-116">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="ee1c6-117">PowerShell (Clássico)</span><span class="sxs-lookup"><span data-stu-id="ee1c6-117">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="ee1c6-118">CLI (Clássica)</span><span class="sxs-lookup"><span data-stu-id="ee1c6-118">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]


## <a name="create-a-virtual-network"></a><span data-ttu-id="ee1c6-119">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="ee1c6-119">Create a virtual network</span></span>

<span data-ttu-id="ee1c6-120">Para criar uma rede virtual usando a CLI do Azure 2.0, conclua as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ee1c6-120">To create a virtual network using the Azure CLI 2.0, complete the following steps:</span></span>

1. <span data-ttu-id="ee1c6-121">Instale e configure a versão mais recente da [CLI do Azure 2.0](/cli/azure/install-az-cli2) e faça logon na conta do Azure usando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="ee1c6-121">Install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

2. <span data-ttu-id="ee1c6-122">Crie um grupo de recursos para sua VNet usando o comando [az group create](/cli/azure/group#create) com os argumentos `--name` e `--location`:</span><span class="sxs-lookup"><span data-stu-id="ee1c6-122">Create a resource group for your VNet using the [az group create](/cli/azure/group#create) command with the `--name` and `--location` arguments:</span></span>

    ```azurecli
    az group create --name TestRG --location centralus
    ```

3. <span data-ttu-id="ee1c6-123">Crie uma VNet e uma sub-rede:</span><span class="sxs-lookup"><span data-stu-id="ee1c6-123">Create a VNet and a subnet:</span></span>

    ```azurecli
    az network vnet create \
    --name TestVNet \
    --resource-group TestRG \
    --location centralus \
    --address-prefix 192.168.0.0/16 \
    --subnet-name FrontEnd \
    --subnet-prefix 192.168.1.0/24
    ```

    <span data-ttu-id="ee1c6-124">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="ee1c6-124">Expected output:</span></span>
    
    ```json
    {
        "newVNet": {
            "addressSpace": {
            "addressPrefixes": [
            "192.168.0.0/16"
            ]
            },
            "dhcpOptions": {
            "dnsServers": []
            },
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>",
            "subnets": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                "name": "FrontEnd",
                "properties": {
                "addressPrefix": "192.168.1.0/24",
                "provisioningState": "Succeeded"
                },
                "resourceGroup": "TestRG"
            }
            ]
            }
    }
    ```

    <span data-ttu-id="ee1c6-125">Parâmetros usados:</span><span class="sxs-lookup"><span data-stu-id="ee1c6-125">Parameters used:</span></span>

    - <span data-ttu-id="ee1c6-126">`--name TestVNet`: nome da VNet a ser criada.</span><span class="sxs-lookup"><span data-stu-id="ee1c6-126">`--name TestVNet`: Name of the VNet to be created.</span></span>
    - <span data-ttu-id="ee1c6-127">`--resource-group TestRG`: o nome do grupo de recursos que controla o recurso.</span><span class="sxs-lookup"><span data-stu-id="ee1c6-127">`--resource-group TestRG`: # The resource group name that controls the resource.</span></span> 
    - <span data-ttu-id="ee1c6-128">`--location centralus`: o local no qual deseja implantar.</span><span class="sxs-lookup"><span data-stu-id="ee1c6-128">`--location centralus`: The location into which to deploy.</span></span>
    - <span data-ttu-id="ee1c6-129">`--address-prefix 192.168.0.0/16`: o bloco e prefixo de endereço.</span><span class="sxs-lookup"><span data-stu-id="ee1c6-129">`--address-prefix 192.168.0.0/16`: The address prefix and block.</span></span>  
    - <span data-ttu-id="ee1c6-130">`--subnet-name FrontEnd`: o nome da sub-rede.</span><span class="sxs-lookup"><span data-stu-id="ee1c6-130">`--subnet-name FrontEnd`: The name of the subnet.</span></span>
    - <span data-ttu-id="ee1c6-131">`--subnet-prefix 192.168.1.0/24`: o bloco e prefixo de endereço.</span><span class="sxs-lookup"><span data-stu-id="ee1c6-131">`--subnet-prefix 192.168.1.0/24`: The address prefix and block.</span></span>

    <span data-ttu-id="ee1c6-132">Para listar as informações básicas para usar no comando seguinte, você pode consultar a VNet usando um [filtro de consulta](/cli/azure/query-az-cli2):</span><span class="sxs-lookup"><span data-stu-id="ee1c6-132">To list the basic information to use in the next command, you can query the VNet using a [query filter](/cli/azure/query-az-cli2):</span></span>

    ```azurecli
    az network vnet list --query '[?name==`TestVNet`].{Where:location,Name:name,Group:resourceGroup}' -o table
    ```

    <span data-ttu-id="ee1c6-133">Que produz esta saída:</span><span class="sxs-lookup"><span data-stu-id="ee1c6-133">Which produces the following output:</span></span>

        Where      Name      Group

        centralus  TestVNet  TestRG

4. <span data-ttu-id="ee1c6-134">Crie uma sub-rede:</span><span class="sxs-lookup"><span data-stu-id="ee1c6-134">Create a subnet:</span></span>

    ```azurecli
    az network vnet subnet create \
    --address-prefix 192.168.2.0/24 \
    --name BackEnd \
    --resource-group TestRG \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="ee1c6-135">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="ee1c6-135">Expected output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid> \"",
    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "TestRG",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```

    <span data-ttu-id="ee1c6-136">Parâmetros usados:</span><span class="sxs-lookup"><span data-stu-id="ee1c6-136">Parameters used:</span></span>

    - <span data-ttu-id="ee1c6-137">`--address-prefix 192.168.2.0/24`: bloco CIDR da sub-rede.</span><span class="sxs-lookup"><span data-stu-id="ee1c6-137">`--address-prefix 192.168.2.0/24`: Subnet CIDR block.</span></span>
    - <span data-ttu-id="ee1c6-138">`--name BackEnd`: nome da nova sub-rede.</span><span class="sxs-lookup"><span data-stu-id="ee1c6-138">`--name BackEnd`: Name of the new subnet.</span></span>
    - <span data-ttu-id="ee1c6-139">`--resource-group TestRG`: o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ee1c6-139">`--resource-group TestRG`: The resource group.</span></span>
    - <span data-ttu-id="ee1c6-140">`--vnet-name TestVNet`: o nome da VNet proprietária.</span><span class="sxs-lookup"><span data-stu-id="ee1c6-140">`--vnet-name TestVNet`: The name of the owning VNet.</span></span>

5. <span data-ttu-id="ee1c6-141">Consulte as propriedades da nova VNet:</span><span class="sxs-lookup"><span data-stu-id="ee1c6-141">Query the properties of the new VNet:</span></span>

    ```azurecli
    az network vnet show \
    -g TestRG \
    -n TestVNet \
    --query '{Name:name,Where:location,Group:resourceGroup,Status:provisioningState,SubnetCount:subnets | length(@)}' \
    -o table
    ```

    <span data-ttu-id="ee1c6-142">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="ee1c6-142">Expected output:</span></span>

        Name      Where      Group    Status       SubnetCount

        TestVNet  centralus  TestRG   Succeeded              2

6. <span data-ttu-id="ee1c6-143">Consulte as propriedades das sub-redes:</span><span class="sxs-lookup"><span data-stu-id="ee1c6-143">Query the properties of the subnets:</span></span>

    ```azurecli
    az network vnet subnet list \
    -g TestRG \
    --vnet-name testvnet \
    --query '[].{Name:name,CIDR:addressPrefix,Status:provisioningState}' \
    -o table
    ```

    <span data-ttu-id="ee1c6-144">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="ee1c6-144">Expected output:</span></span>

        Name      CIDR            Status

        FrontEnd  192.168.1.0/24  Succeeded
        BackEnd   192.168.2.0/24  Succeeded

## <a name="next-steps"></a><span data-ttu-id="ee1c6-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ee1c6-145">Next steps</span></span>

<span data-ttu-id="ee1c6-146">Saiba como se conectar:</span><span class="sxs-lookup"><span data-stu-id="ee1c6-146">Learn how to connect:</span></span>

- <span data-ttu-id="ee1c6-147">Uma VM (máquina virtual) em uma rede virtual lendo o artigo [Criar uma VM Linux](../virtual-machines/linux/quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ee1c6-147">A virtual machine (VM) to a virtual network by reading the [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="ee1c6-148">Em vez de criar uma rede virtual e sub-rede nas etapas dos artigos, você pode selecionar uma rede virtual e uma sub-rede existente para se conectar a uma VM.</span><span class="sxs-lookup"><span data-stu-id="ee1c6-148">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span></span>
- <span data-ttu-id="ee1c6-149">A rede virtual para outras redes virtuais, lendo o artigo [Conectar VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ee1c6-149">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="ee1c6-150">A rede virtual para uma rede local usando uma VPN (rede privada virtual) site a site ou um circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ee1c6-150">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="ee1c6-151">Saiba como lendo [Conectar uma VNet a uma rede local usando uma VPN site a site](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) e [Vincular uma VNet a um circuito ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="ee1c6-151">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>