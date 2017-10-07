---
title: aaaCreate uma rede virtual - 2.0 do CLI do Azure | Microsoft Docs
description: "Saiba como toocreate usando uma rede virtual Olá 2.0 do CLI do Azure."
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
ms.openlocfilehash: e79b7fe780fc81f4866f810d830824e43a5a43b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli-20"></a><span data-ttu-id="ca788-103">Criar uma rede virtual usando Olá 2.0 do CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="ca788-103">Create a virtual network using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="ca788-104">O Azure tem dois modelos de implantação: Azure Resource Manager e clássico.</span><span class="sxs-lookup"><span data-stu-id="ca788-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="ca788-105">A Microsoft recomenda a criação de recursos por meio do modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca788-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="ca788-106">mais sobre toolearn Olá diferenças entre modelos de saudação dois ler Olá [modelos de implantação do Azure entender](../azure-resource-manager/resource-manager-deployment-model.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="ca788-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="ca788-107">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="ca788-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="ca788-108">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="ca788-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="ca788-109">[1.0 de CLI do Azure](virtual-networks-create-vnet-cli-nodejs.md) – nosso CLI para modelos de implantação de gerenciamento de recursos e clássico de Olá</span><span class="sxs-lookup"><span data-stu-id="ca788-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span>
- <span data-ttu-id="ca788-110">[2.0 do CLI do Azure](#create-a-virtual-network) -nossa próxima geração CLI para modelo de implantação de gerenciamento de recursos de saudação (Este artigo)'</span><span class="sxs-lookup"><span data-stu-id="ca788-110">[Azure CLI 2.0](#create-a-virtual-network) - our next generation CLI for hello resource management deployment model (this article)\`</span></span>
 
    <span data-ttu-id="ca788-111">Você também pode criar uma rede virtual por meio de Gerenciador de recursos usando outras ferramentas ou criar uma rede virtual por meio do modelo de implantação clássico Olá selecionando uma opção diferente de saudação lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="ca788-111">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ca788-112">Portal</span><span class="sxs-lookup"><span data-stu-id="ca788-112">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="ca788-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ca788-113">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="ca788-114">CLI</span><span class="sxs-lookup"><span data-stu-id="ca788-114">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="ca788-115">Modelo</span><span class="sxs-lookup"><span data-stu-id="ca788-115">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="ca788-116">Portal (clássico)</span><span class="sxs-lookup"><span data-stu-id="ca788-116">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="ca788-117">PowerShell (Clássico)</span><span class="sxs-lookup"><span data-stu-id="ca788-117">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="ca788-118">CLI (Clássica)</span><span class="sxs-lookup"><span data-stu-id="ca788-118">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]


## <a name="create-a-virtual-network"></a><span data-ttu-id="ca788-119">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="ca788-119">Create a virtual network</span></span>

<span data-ttu-id="ca788-120">toocreate usando uma rede virtual Olá 2.0 do CLI do Azure, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ca788-120">toocreate a virtual network using hello Azure CLI 2.0, complete hello following steps:</span></span>

1. <span data-ttu-id="ca788-121">Instalar e configurar hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) e fazer logon na conta do Azure usando o tooan [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="ca788-121">Install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

2. <span data-ttu-id="ca788-122">Criar um grupo de recursos para sua VNet usando Olá [criar grupo az](/cli/azure/group#create) com hello `--name` e `--location` argumentos:</span><span class="sxs-lookup"><span data-stu-id="ca788-122">Create a resource group for your VNet using hello [az group create](/cli/azure/group#create) command with hello `--name` and `--location` arguments:</span></span>

    ```azurecli
    az group create --name TestRG --location centralus
    ```

3. <span data-ttu-id="ca788-123">Crie uma VNet e uma sub-rede:</span><span class="sxs-lookup"><span data-stu-id="ca788-123">Create a VNet and a subnet:</span></span>

    ```azurecli
    az network vnet create \
    --name TestVNet \
    --resource-group TestRG \
    --location centralus \
    --address-prefix 192.168.0.0/16 \
    --subnet-name FrontEnd \
    --subnet-prefix 192.168.1.0/24
    ```

    <span data-ttu-id="ca788-124">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="ca788-124">Expected output:</span></span>
    
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

    <span data-ttu-id="ca788-125">Parâmetros usados:</span><span class="sxs-lookup"><span data-stu-id="ca788-125">Parameters used:</span></span>

    - <span data-ttu-id="ca788-126">`--name TestVNet`: Nome da saudação VNet toobe criado.</span><span class="sxs-lookup"><span data-stu-id="ca788-126">`--name TestVNet`: Name of hello VNet toobe created.</span></span>
    - <span data-ttu-id="ca788-127">`--resource-group TestRG`: # Olá recurso nome de grupo que controla o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca788-127">`--resource-group TestRG`: # hello resource group name that controls hello resource.</span></span> 
    - <span data-ttu-id="ca788-128">`--location centralus`: Olá local no qual toodeploy.</span><span class="sxs-lookup"><span data-stu-id="ca788-128">`--location centralus`: hello location into which toodeploy.</span></span>
    - <span data-ttu-id="ca788-129">`--address-prefix 192.168.0.0/16`: Olá prefixo de endereço e o bloco.</span><span class="sxs-lookup"><span data-stu-id="ca788-129">`--address-prefix 192.168.0.0/16`: hello address prefix and block.</span></span>  
    - <span data-ttu-id="ca788-130">`--subnet-name FrontEnd`: nome de saudação da sub-rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca788-130">`--subnet-name FrontEnd`: hello name of hello subnet.</span></span>
    - <span data-ttu-id="ca788-131">`--subnet-prefix 192.168.1.0/24`: Olá prefixo de endereço e o bloco.</span><span class="sxs-lookup"><span data-stu-id="ca788-131">`--subnet-prefix 192.168.1.0/24`: hello address prefix and block.</span></span>

    <span data-ttu-id="ca788-132">toolist Olá informações básicas toouse em Olá próximo comando, você pode consultar Olá VNet usando um [filtro de consulta](/cli/azure/query-az-cli2):</span><span class="sxs-lookup"><span data-stu-id="ca788-132">toolist hello basic information toouse in hello next command, you can query hello VNet using a [query filter](/cli/azure/query-az-cli2):</span></span>

    ```azurecli
    az network vnet list --query '[?name==`TestVNet`].{Where:location,Name:name,Group:resourceGroup}' -o table
    ```

    <span data-ttu-id="ca788-133">Quais Olá produz saída a seguir:</span><span class="sxs-lookup"><span data-stu-id="ca788-133">Which produces hello following output:</span></span>

        Where      Name      Group

        centralus  TestVNet  TestRG

4. <span data-ttu-id="ca788-134">Crie uma sub-rede:</span><span class="sxs-lookup"><span data-stu-id="ca788-134">Create a subnet:</span></span>

    ```azurecli
    az network vnet subnet create \
    --address-prefix 192.168.2.0/24 \
    --name BackEnd \
    --resource-group TestRG \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="ca788-135">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="ca788-135">Expected output:</span></span>

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

    <span data-ttu-id="ca788-136">Parâmetros usados:</span><span class="sxs-lookup"><span data-stu-id="ca788-136">Parameters used:</span></span>

    - <span data-ttu-id="ca788-137">`--address-prefix 192.168.2.0/24`: bloco CIDR da sub-rede.</span><span class="sxs-lookup"><span data-stu-id="ca788-137">`--address-prefix 192.168.2.0/24`: Subnet CIDR block.</span></span>
    - <span data-ttu-id="ca788-138">`--name BackEnd`: Nome da nova subrede hello.</span><span class="sxs-lookup"><span data-stu-id="ca788-138">`--name BackEnd`: Name of hello new subnet.</span></span>
    - <span data-ttu-id="ca788-139">`--resource-group TestRG`: o grupo de recursos hello.</span><span class="sxs-lookup"><span data-stu-id="ca788-139">`--resource-group TestRG`: hello resource group.</span></span>
    - <span data-ttu-id="ca788-140">`--vnet-name TestVNet`: nome de saudação do hello proprietária da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="ca788-140">`--vnet-name TestVNet`: hello name of hello owning VNet.</span></span>

5. <span data-ttu-id="ca788-141">Propriedades de saudação de consulta de Olá nova rede virtual:</span><span class="sxs-lookup"><span data-stu-id="ca788-141">Query hello properties of hello new VNet:</span></span>

    ```azurecli
    az network vnet show \
    -g TestRG \
    -n TestVNet \
    --query '{Name:name,Where:location,Group:resourceGroup,Status:provisioningState,SubnetCount:subnets | length(@)}' \
    -o table
    ```

    <span data-ttu-id="ca788-142">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="ca788-142">Expected output:</span></span>

        Name      Where      Group    Status       SubnetCount

        TestVNet  centralus  TestRG   Succeeded              2

6. <span data-ttu-id="ca788-143">Propriedades de saudação de consulta de sub-redes hello:</span><span class="sxs-lookup"><span data-stu-id="ca788-143">Query hello properties of hello subnets:</span></span>

    ```azurecli
    az network vnet subnet list \
    -g TestRG \
    --vnet-name testvnet \
    --query '[].{Name:name,CIDR:addressPrefix,Status:provisioningState}' \
    -o table
    ```

    <span data-ttu-id="ca788-144">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="ca788-144">Expected output:</span></span>

        Name      CIDR            Status

        FrontEnd  192.168.1.0/24  Succeeded
        BackEnd   192.168.2.0/24  Succeeded

## <a name="next-steps"></a><span data-ttu-id="ca788-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ca788-145">Next steps</span></span>

<span data-ttu-id="ca788-146">Saiba como tooconnect:</span><span class="sxs-lookup"><span data-stu-id="ca788-146">Learn how tooconnect:</span></span>

- <span data-ttu-id="ca788-147">Uma rede virtual de tooa de máquina virtual (VM) lendo Olá [criar uma VM do Linux](../virtual-machines/linux/quick-create-cli.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="ca788-147">A virtual machine (VM) tooa virtual network by reading hello [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="ca788-148">Em vez de criar uma rede virtual e a sub-rede nas etapas de saudação de artigos hello, você pode selecionar uma rede virtual existente e a sub-rede tooconnect uma VM.</span><span class="sxs-lookup"><span data-stu-id="ca788-148">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="ca788-149">Olá redes virtuais de tooother de rede virtual lendo Olá [VNets conectar](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="ca788-149">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="ca788-150">Olá rede virtual tooan na rede local usando uma rede privada virtual (VPN) site a site ou um circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="ca788-150">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="ca788-151">Saiba como lendo Olá [conectar uma rede de local de tooan de rede virtual usando uma VPN site a site](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) e [vincular um circuito de rota expressa do tooan de VNet](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="ca788-151">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>
