---
title: "aaaCreate 2.0 do CLI do Azure de grupos de segurança - rede | Microsoft Docs"
description: "Saiba como toocreate e implantar grupos de segurança de rede usando Olá 2.0 do CLI do Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9ea82c09-f4a6-4268-88bc-fc439db40c48
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/17/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 30b1d60676331bf5e2bbbb046c747477be9d3338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-cli-20"></a><span data-ttu-id="f0301-103">Criar grupos de segurança usando hello Azure CLI 2.0 de rede</span><span class="sxs-lookup"><span data-stu-id="f0301-103">Create network security groups using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="f0301-104">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="f0301-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="f0301-105">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="f0301-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="f0301-106">[1.0 de CLI do Azure](virtual-networks-create-nsg-cli-nodejs.md) – nosso CLI para modelos de implantação de gerenciamento de recursos e clássico de Olá</span><span class="sxs-lookup"><span data-stu-id="f0301-106">[Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="f0301-107">[2.0 do CLI do Azure](#Create-the-nsg-for-the-front-end-subnet) -nossa próxima geração CLI para modelo de implantação de gerenciamento de recursos de saudação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="f0301-107">[Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="f0301-108">exemplo Hello Azure CLI 2.0 comandos a seguir espera um ambiente simples já criado com base no cenário de saudação anterior.</span><span class="sxs-lookup"><span data-stu-id="f0301-108">hello sample Azure CLI 2.0 commands following expect a simple environment already created based on hello scenario preceding.</span></span> 

## <a name="create-hello-nsg-for-hello-frontend-subnet"></a><span data-ttu-id="f0301-109">Criar hello NSG para Olá `FrontEnd` sub-rede</span><span class="sxs-lookup"><span data-stu-id="f0301-109">Create hello NSG for hello `FrontEnd` subnet</span></span>

<span data-ttu-id="f0301-110">toocreate um NSG denominado *NSG-front-end* com base no cenário de saudação anterior, execute o seguinte de etapas de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0301-110">toocreate an NSG named *NSG-FrontEnd* based on hello scenario preceding, follow hello steps following.</span></span>

1. <span data-ttu-id="f0301-111">Se você ainda não tiver ainda, instalar e configurar hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) e fazer logon na conta do Azure usando o tooan [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="f0301-111">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="f0301-112">Criar um NSG usando Olá [criar az rede nsg](/cli/azure/network/nsg#create) comando.</span><span class="sxs-lookup"><span data-stu-id="f0301-112">Create an NSG using hello [az network nsg create](/cli/azure/network/nsg#create) command.</span></span> 

    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-FrontEnd \
    --location centralus 
    ```

    <span data-ttu-id="f0301-113">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="f0301-113">Parameters:</span></span>
   
   * <span data-ttu-id="f0301-114">`--resource-group`: Nome do grupo de recursos de saudação onde Olá NSG é criado.</span><span class="sxs-lookup"><span data-stu-id="f0301-114">`--resource-group`: Name of hello resource group where hello NSG is created.</span></span> <span data-ttu-id="f0301-115">Para o nosso cenário, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="f0301-115">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="f0301-116">`--location`: Região do azure onde hello novo NSG é criado.</span><span class="sxs-lookup"><span data-stu-id="f0301-116">`--location`: Azure region where hello new NSG is created.</span></span> <span data-ttu-id="f0301-117">Para o nosso cenário, *westus*.</span><span class="sxs-lookup"><span data-stu-id="f0301-117">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="f0301-118">`--name`: Nome Olá novo NSG.</span><span class="sxs-lookup"><span data-stu-id="f0301-118">`--name`: Name for hello new NSG.</span></span> <span data-ttu-id="f0301-119">Para o nosso cenário, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="f0301-119">For our scenario, *NSG-FrontEnd*.</span></span>

    <span data-ttu-id="f0301-120">Olá esperado a saída é uma grande quantidade de informações, incluindo uma lista de todas as regras padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0301-120">hello expected output is quite a bit of information including a list of all hello default rules.</span></span> <span data-ttu-id="f0301-121">Olá, exemplo a seguir mostra regras de padrão de saudação com um filtro de consulta JMESPATH Olá `table` formato de saída:</span><span class="sxs-lookup"><span data-stu-id="f0301-121">hello following example shows hello default rules using a JMESPATH query filter with hello `table` output format:</span></span>

    ```azurecli
    az network nsg show \
    -g testrg \
    -n nsg-frontend \
    --query 'defaultSecurityRules[].{Access:access,Desc:description,DestPortRange:destinationPortRange,Direction:direction,Priority:priority}' \
    -o table
    ```
   
   <span data-ttu-id="f0301-122">Saída:</span><span class="sxs-lookup"><span data-stu-id="f0301-122">Output:</span></span>

        Access    Desc                                                    DestPortRange    Direction      Priority
        
        Allow     Allow inbound traffic from all VMs in VNET              *                Inbound           65000
        Allow     Allow inbound traffic from azure load balancer          *                Inbound           65001
        Deny      Deny all inbound traffic                                *                Inbound           65500
        Allow     Allow outbound traffic from all VMs tooall VMs in VNET  *                Outbound          65000
        Allow     Allow outbound traffic from all VMs tooInternet         *                Outbound          65001
        Deny      Deny all outbound traffic                               *                Outbound          65500



3. <span data-ttu-id="f0301-123">Criar uma regra que permita acesso tooport 3389 (RDP) da saudação da Internet com hello [criar regra de nsg rede az](/cli/azure/network/nsg/rule#create) comando.</span><span class="sxs-lookup"><span data-stu-id="f0301-123">Create a rule that allows access tooport 3389 (RDP) from hello Internet with hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f0301-124">Dependendo de você estiver usando o shell de hello, talvez seja necessário toomodify Olá `*` caracteres nos argumentos Olá após assim como não tooexpand de argumento Olá antes da execução.</span><span class="sxs-lookup"><span data-stu-id="f0301-124">Depending on hello shell you are using, you might need toomodify hello `*` character in hello arguments following so as not tooexpand hello argument before execution.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-FrontEnd \
    --name rdp-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 3389
    ```
   
    <span data-ttu-id="f0301-125">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="f0301-125">Expected output:</span></span>
   
    ```json
    {
        "access": "Allow",
        "description": null,
        "destinationAddressPrefix": "*",
        "destinationPortRange": "3389",
        "direction": "Inbound",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule",
        "name": "rdp-rule",
        "priority": 100,
        "protocol": "Tcp",
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "sourceAddressPrefix": "Internet",
        "sourcePortRange": "*"
    }
    ```

    <span data-ttu-id="f0301-126">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="f0301-126">Parameters:</span></span>

    * <span data-ttu-id="f0301-127">`--resource-group testrg`: Olá toouse do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f0301-127">`--resource-group testrg`: hello resource group toouse.</span></span> <span data-ttu-id="f0301-128">Observe que ele diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="f0301-128">Note that it is case-insensitive.</span></span>
    * <span data-ttu-id="f0301-129">`--nsg-name NSG-FrontEnd`: Nome do NSG Olá no qual Olá regra é criada.</span><span class="sxs-lookup"><span data-stu-id="f0301-129">`--nsg-name NSG-FrontEnd`: Name of hello NSG in which hello rule is created.</span></span>
    * <span data-ttu-id="f0301-130">`--name rdp-rule`: O nome para a nova regra de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0301-130">`--name rdp-rule`: Name for hello new rule.</span></span>
    * <span data-ttu-id="f0301-131">`--access Allow`: Nível de acesso para regra de saudação (Deny ou permitir).</span><span class="sxs-lookup"><span data-stu-id="f0301-131">`--access Allow`: Access level for hello rule (Deny or Allow).</span></span>
    * <span data-ttu-id="f0301-132">`--protocol Tcp`:protocolo (Tcp, Udp ou *).</span><span class="sxs-lookup"><span data-stu-id="f0301-132">`--protocol Tcp`: Protocol (Tcp, Udp, or *).</span></span>
    * <span data-ttu-id="f0301-133">`--direction Inbound`: Direção da conexão de saudação (entrada ou saída).</span><span class="sxs-lookup"><span data-stu-id="f0301-133">`--direction Inbound`: Direction of hello connection (Inbound or Outbound).</span></span>
    * <span data-ttu-id="f0301-134">`--priority 100`: Prioridade para a regra de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0301-134">`--priority 100`: Priority for hello rule.</span></span>
    * <span data-ttu-id="f0301-135">`--source-address-prefix Internet`: prefixo do endereço de origem no CIDR ou uso de rótulos padrão.</span><span class="sxs-lookup"><span data-stu-id="f0301-135">`--source-address-prefix Internet`: Source address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="f0301-136">`--source-port-range "*"`: porta de origem ou intervalo de porta.</span><span class="sxs-lookup"><span data-stu-id="f0301-136">`--source-port-range "*"`: Source port or port range.</span></span> <span data-ttu-id="f0301-137">Porta aberta conexão hello.</span><span class="sxs-lookup"><span data-stu-id="f0301-137">Port that opened hello connection.</span></span>
    * <span data-ttu-id="f0301-138">`--destination-address-prefix "*"`: prefixo do endereço de destino no CIDR ou uso de rótulos padrão.</span><span class="sxs-lookup"><span data-stu-id="f0301-138">`--destination-address-prefix "*"`: Destination address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="f0301-139">`--destination-port-range 3389`: porta de destino ou intervalo de porta.</span><span class="sxs-lookup"><span data-stu-id="f0301-139">`--destination-port-range 3389`: Destination port or port range.</span></span> <span data-ttu-id="f0301-140">Porta que recebe a solicitação de conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0301-140">Port that receives hello connection request.</span></span>



4. <span data-ttu-id="f0301-141">Criar uma regra que permita acesso tooport 80 (HTTP) do hello Internet **criar regra de nsg rede az** comando.</span><span class="sxs-lookup"><span data-stu-id="f0301-141">Create a rule that allows access tooport 80 (HTTP) from hello Internet **az network nsg rule create** command.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-FrontEnd \
    --name web-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 200 \
    --source-address-prefix Internet \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 80
    ```
   
    <span data-ttu-id="f0301-142">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="f0301-142">Expected putput:</span></span>
   
    ```json
    {
        "access": "Allow",
        "description": null,
        "destinationAddressPrefix": "*",
        "destinationPortRange": "80",
        "direction": "Inbound",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule",
        "name": "web-rule",
        "priority": 200,
        "protocol": "Tcp",
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "sourceAddressPrefix": "Internet",
        "sourcePortRange": "*"
    }
    ```

5. <span data-ttu-id="f0301-143">Associar Olá NSG toohello **front-end** sub-rede com hello [atualização de sub-rede da rede virtual de rede az](/cli/azure/network/vnet/subnet#update) comando.</span><span class="sxs-lookup"><span data-stu-id="f0301-143">Bind hello NSG toohello **FrontEnd** subnet with hello [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command.</span></span>
        
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name FrontEnd \
    --resource-group testrg \
    --network-security-group NSG-FrontEnd
    ```
   
    <span data-ttu-id="f0301-144">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="f0301-144">Expected output:</span></span>
   
    ```json
    {
        "addressPrefix": "192.168.1.0/24",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/FrontEnd",
        "ipConfigurations": [
            {
            "etag": null,
            "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
            "name": null,
            "privateIpAddress": null,
            "privateIpAllocationMethod": null,
            "provisioningState": null,
            "publicIpAddress": null,
            "resourceGroup": "TestRG",
            "subnet": null
            }
        ],
        "name": "FrontEnd",
        "networkSecurityGroup": {
            "defaultSecurityRules": null,
            "etag": null,
            "id": "/subscriptions/<guid>f/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
            "location": null,
            "name": null,
            "networkInterfaces": null,
            "provisioningState": null,
            "resourceGroup": "testrg",
            "resourceGuid": null,
            "securityRules": null,
            "subnets": null,
            "tags": null,
            "type": null
        },
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "resourceNavigationLinks": null,
        "routeTable": null
    }
    ```

## <a name="create-hello-nsg-for-hello-backend-subnet"></a><span data-ttu-id="f0301-145">Criar hello NSG para Olá `BackEnd` sub-rede</span><span class="sxs-lookup"><span data-stu-id="f0301-145">Create hello NSG for hello `BackEnd` subnet</span></span>
<span data-ttu-id="f0301-146">toocreate um NSG denominado *back-end NSG* com base no cenário de saudação anterior, execute o seguinte de etapas de saudação.</span><span class="sxs-lookup"><span data-stu-id="f0301-146">toocreate an NSG named *NSG-BackEnd* based on hello scenario preceding, follow hello steps following.</span></span>

1. <span data-ttu-id="f0301-147">Criar hello `NSG-BackEnd` NSG com **criar az rede nsg**.</span><span class="sxs-lookup"><span data-stu-id="f0301-147">Create hello `NSG-BackEnd` NSG with **az network nsg create**.</span></span>
   
    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-BackEnd \
    --location centralus
    ```
   
    <span data-ttu-id="f0301-148">Como na etapa 2, anterior, Olá esperado saída é muito grande, incluindo as regras padrão.</span><span class="sxs-lookup"><span data-stu-id="f0301-148">As in step 2, preceding, hello expected output is quite large, including default rules.</span></span>
   
2. <span data-ttu-id="f0301-149">Criar uma regra que permita acesso tooport 1433 (SQL) do hello `FrontEnd` sub-rede com hello **criar regra de nsg rede az** comando.</span><span class="sxs-lookup"><span data-stu-id="f0301-149">Create a rule that allows access tooport 1433 (SQL) from hello `FrontEnd` subnet with hello **az network nsg rule create** command.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-BackEnd \
    --name sql-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix 192.168.1.0/24 \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 1433
    ```
   
    <span data-ttu-id="f0301-150">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="f0301-150">Expected output:</span></span>

    ```json  
    {
    "access": "Allow",
    "description": null,
    "destinationAddressPrefix": "*",
    "destinationPortRange": "1433",
    "direction": "Inbound",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/sql-rule",
    "name": "sql-rule",
    "priority": 100,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "sourceAddressPrefix": "192.168.1.0/24",
    "sourcePortRange": "*"
    }
    ```

3. <span data-ttu-id="f0301-151">Criar uma regra que nega acesso toohello à Internet usando Olá **criar regra de nsg rede az** comando.</span><span class="sxs-lookup"><span data-stu-id="f0301-151">Create a rule that denies access toohello Internet using hello **az network nsg rule create** command.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-BackEnd \
    --name web-rule \
    --access Deny \
    --protocol Tcp  \
    --direction Outbound  \
    --priority 200 \
    --source-address-prefix "*" \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range "*"
    ```
   
    <span data-ttu-id="f0301-152">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="f0301-152">Expected putput:</span></span>
   
    ```json
    {
    "access": "Deny",
    "description": null,
    "destinationAddressPrefix": "*",
    "destinationPortRange": "*",
    "direction": "Outbound",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/web-rule",
    "name": "web-rule",
    "priority": 200,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "sourceAddressPrefix": "*",
    "sourcePortRange": "*"
    }
    ```

4. <span data-ttu-id="f0301-153">Associar Olá NSG toohello `BackEnd` sub-rede usando Olá **conjunto de sub-rede de rede virtual de rede az** comando.</span><span class="sxs-lookup"><span data-stu-id="f0301-153">Bind hello NSG toohello `BackEnd` subnet using hello **az network vnet subnet set** command.</span></span>
   
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name BackEnd \
    --resource-group testrg \
    --network-security-group NSG-BackEnd
    ```
   
    <span data-ttu-id="f0301-154">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="f0301-154">Expected output:</span></span>
   
    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": {
        "defaultSecurityRules": null,
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "location": null,
        "name": null,
        "networkInterfaces": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "resourceGuid": null,
        "securityRules": null,
        "subnets": null,
        "tags": null,
        "type": null
    },
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```
