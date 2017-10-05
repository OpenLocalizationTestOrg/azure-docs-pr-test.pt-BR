---
title: "Criação de grupos de segurança de rede - CLI 2.0 do Azure | Microsoft Docs"
description: "Aprenda a criar e implantar grupos de segurança de rede usando a CLI 2.0 do Azure."
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
ms.openlocfilehash: 8efb3ab66d07875b51f723fed5594bcb477ed025
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-network-security-groups-using-the-azure-cli-20"></a><span data-ttu-id="6e2eb-103">Como criar grupos de segurança de rede usando a CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="6e2eb-103">Create network security groups using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="6e2eb-104">Versões da CLI para concluir a tarefa</span><span class="sxs-lookup"><span data-stu-id="6e2eb-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="6e2eb-105">Você pode concluir a tarefa usando uma das seguintes versões da CLI:</span><span class="sxs-lookup"><span data-stu-id="6e2eb-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="6e2eb-106">[CLI do Azure 1.0](virtual-networks-create-nsg-cli-nodejs.md) – nossa CLI para os modelos de implantação clássico e de gerenciamento de recursos</span><span class="sxs-lookup"><span data-stu-id="6e2eb-106">[Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span> 
- <span data-ttu-id="6e2eb-107">[CLI do Azure 2.0](#Create-the-nsg-for-the-front-end-subnet) – nossa CLI da próxima geração para o modelo de implantação do resource manager (este artigo)</span><span class="sxs-lookup"><span data-stu-id="6e2eb-107">[Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) - our next generation CLI for the resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="6e2eb-108">Os comandos da CLI 2.0 do Azure de exemplo a seguir esperam um ambiente simples, já criado com base no cenário anterior.</span><span class="sxs-lookup"><span data-stu-id="6e2eb-108">The sample Azure CLI 2.0 commands following expect a simple environment already created based on the scenario preceding.</span></span> 

## <a name="create-the-nsg-for-the-frontend-subnet"></a><span data-ttu-id="6e2eb-109">Como criar o NSG para a `FrontEnd` sub-rede</span><span class="sxs-lookup"><span data-stu-id="6e2eb-109">Create the NSG for the `FrontEnd` subnet</span></span>

<span data-ttu-id="6e2eb-110">Siga as etapas abaixo para criar um NSG chamado *NSG-FrontEnd* com base no cenário anterior.</span><span class="sxs-lookup"><span data-stu-id="6e2eb-110">To create an NSG named *NSG-FrontEnd* based on the scenario preceding, follow the steps following.</span></span>

1. <span data-ttu-id="6e2eb-111">Caso ainda não tenha feito isso, instale e configure a versão mais recente da [CLI do Azure 2.0](/cli/azure/install-az-cli2) e faça logon na conta do Azure usando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="6e2eb-111">If you haven't yet, install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="6e2eb-112">Crie um NSG usando o comando [az network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="6e2eb-112">Create an NSG using the [az network nsg create](/cli/azure/network/nsg#create) command.</span></span> 

    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-FrontEnd \
    --location centralus 
    ```

    <span data-ttu-id="6e2eb-113">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="6e2eb-113">Parameters:</span></span>
   
   * <span data-ttu-id="6e2eb-114">`--resource-group`: nome do grupo de recursos em que o NSG será criado.</span><span class="sxs-lookup"><span data-stu-id="6e2eb-114">`--resource-group`: Name of the resource group where the NSG is created.</span></span> <span data-ttu-id="6e2eb-115">Para o nosso cenário, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="6e2eb-115">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="6e2eb-116">`--location`: região do Azure onde o novo NSG é criado.</span><span class="sxs-lookup"><span data-stu-id="6e2eb-116">`--location`: Azure region where the new NSG is created.</span></span> <span data-ttu-id="6e2eb-117">Para o nosso cenário, *westus*.</span><span class="sxs-lookup"><span data-stu-id="6e2eb-117">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="6e2eb-118">`--name`: nome para o novo NSG.</span><span class="sxs-lookup"><span data-stu-id="6e2eb-118">`--name`: Name for the new NSG.</span></span> <span data-ttu-id="6e2eb-119">Para o nosso cenário, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="6e2eb-119">For our scenario, *NSG-FrontEnd*.</span></span>

    <span data-ttu-id="6e2eb-120">A saída esperada é uma grande quantidade de informações, incluindo uma lista de todas as regras padrão.</span><span class="sxs-lookup"><span data-stu-id="6e2eb-120">The expected output is quite a bit of information including a list of all the default rules.</span></span> <span data-ttu-id="6e2eb-121">O exemplo a seguir mostra as regras padrão usando um filtro de consulta JMESPATH com o formato de saída `table`:</span><span class="sxs-lookup"><span data-stu-id="6e2eb-121">The following example shows the default rules using a JMESPATH query filter with the `table` output format:</span></span>

    ```azurecli
    az network nsg show \
    -g testrg \
    -n nsg-frontend \
    --query 'defaultSecurityRules[].{Access:access,Desc:description,DestPortRange:destinationPortRange,Direction:direction,Priority:priority}' \
    -o table
    ```
   
   <span data-ttu-id="6e2eb-122">Saída:</span><span class="sxs-lookup"><span data-stu-id="6e2eb-122">Output:</span></span>

        Access    Desc                                                    DestPortRange    Direction      Priority
        
        Allow     Allow inbound traffic from all VMs in VNET              *                Inbound           65000
        Allow     Allow inbound traffic from azure load balancer          *                Inbound           65001
        Deny      Deny all inbound traffic                                *                Inbound           65500
        Allow     Allow outbound traffic from all VMs to all VMs in VNET  *                Outbound          65000
        Allow     Allow outbound traffic from all VMs to Internet         *                Outbound          65001
        Deny      Deny all outbound traffic                               *                Outbound          65500



3. <span data-ttu-id="6e2eb-123">Execute o comando [az network nsg rule create](/cli/azure/network/nsg/rule#create) para criar uma regra que permite o acesso à porta 3389 (RDP) a partir da Internet.</span><span class="sxs-lookup"><span data-stu-id="6e2eb-123">Create a rule that allows access to port 3389 (RDP) from the Internet with the [az network nsg rule create](/cli/azure/network/nsg/rule#create) command.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6e2eb-124">Dependendo do shell que você está usando, talvez seja necessário modificar o caractere `*` nos argumentos a seguir para evitar a expansão do argumento antes da execução.</span><span class="sxs-lookup"><span data-stu-id="6e2eb-124">Depending on the shell you are using, you might need to modify the `*` character in the arguments following so as not to expand the argument before execution.</span></span>
   
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
   
    <span data-ttu-id="6e2eb-125">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="6e2eb-125">Expected output:</span></span>
   
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

    <span data-ttu-id="6e2eb-126">Parâmetros:</span><span class="sxs-lookup"><span data-stu-id="6e2eb-126">Parameters:</span></span>

    * <span data-ttu-id="6e2eb-127">`--resource-group testrg`: o grupo de recursos para usar.</span><span class="sxs-lookup"><span data-stu-id="6e2eb-127">`--resource-group testrg`: The resource group to use.</span></span> <span data-ttu-id="6e2eb-128">Observe que ele diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="6e2eb-128">Note that it is case-insensitive.</span></span>
    * <span data-ttu-id="6e2eb-129">`--nsg-name NSG-FrontEnd`: nome do NSG no qual a regra será criada.</span><span class="sxs-lookup"><span data-stu-id="6e2eb-129">`--nsg-name NSG-FrontEnd`: Name of the NSG in which the rule is created.</span></span>
    * <span data-ttu-id="6e2eb-130">`--name rdp-rule`: nome para a nova regra.</span><span class="sxs-lookup"><span data-stu-id="6e2eb-130">`--name rdp-rule`: Name for the new rule.</span></span>
    * <span data-ttu-id="6e2eb-131">`--access Allow`: nível de acesso para a regra (Negar ou Permitir).</span><span class="sxs-lookup"><span data-stu-id="6e2eb-131">`--access Allow`: Access level for the rule (Deny or Allow).</span></span>
    * <span data-ttu-id="6e2eb-132">`--protocol Tcp`:protocolo (Tcp, Udp ou *).</span><span class="sxs-lookup"><span data-stu-id="6e2eb-132">`--protocol Tcp`: Protocol (Tcp, Udp, or *).</span></span>
    * <span data-ttu-id="6e2eb-133">`--direction Inbound`: direção da conexão (Entrada ou Saída).</span><span class="sxs-lookup"><span data-stu-id="6e2eb-133">`--direction Inbound`: Direction of the connection (Inbound or Outbound).</span></span>
    * <span data-ttu-id="6e2eb-134">`--priority 100`: prioridade da regra.</span><span class="sxs-lookup"><span data-stu-id="6e2eb-134">`--priority 100`: Priority for the rule.</span></span>
    * <span data-ttu-id="6e2eb-135">`--source-address-prefix Internet`: prefixo do endereço de origem no CIDR ou uso de rótulos padrão.</span><span class="sxs-lookup"><span data-stu-id="6e2eb-135">`--source-address-prefix Internet`: Source address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="6e2eb-136">`--source-port-range "*"`: porta de origem ou intervalo de porta.</span><span class="sxs-lookup"><span data-stu-id="6e2eb-136">`--source-port-range "*"`: Source port or port range.</span></span> <span data-ttu-id="6e2eb-137">Porta que abriu a conexão.</span><span class="sxs-lookup"><span data-stu-id="6e2eb-137">Port that opened the connection.</span></span>
    * <span data-ttu-id="6e2eb-138">`--destination-address-prefix "*"`: prefixo do endereço de destino no CIDR ou uso de rótulos padrão.</span><span class="sxs-lookup"><span data-stu-id="6e2eb-138">`--destination-address-prefix "*"`: Destination address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="6e2eb-139">`--destination-port-range 3389`: porta de destino ou intervalo de porta.</span><span class="sxs-lookup"><span data-stu-id="6e2eb-139">`--destination-port-range 3389`: Destination port or port range.</span></span> <span data-ttu-id="6e2eb-140">Porta que recebe a solicitação de conexão.</span><span class="sxs-lookup"><span data-stu-id="6e2eb-140">Port that receives the connection request.</span></span>



4. <span data-ttu-id="6e2eb-141">Execute o comando **az network nsg rule create** para criar uma regra que permite o acesso à porta 80 (HTTP) a partir da Internet.</span><span class="sxs-lookup"><span data-stu-id="6e2eb-141">Create a rule that allows access to port 80 (HTTP) from the Internet **az network nsg rule create** command.</span></span>
   
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
   
    <span data-ttu-id="6e2eb-142">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="6e2eb-142">Expected putput:</span></span>
   
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

5. <span data-ttu-id="6e2eb-143">Associe o NSG à sub-rede do **FrontEnd** rede com o comando [az network vnet subnet update](/cli/azure/network/vnet/subnet#update).</span><span class="sxs-lookup"><span data-stu-id="6e2eb-143">Bind the NSG to the **FrontEnd** subnet with the [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command.</span></span>
        
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name FrontEnd \
    --resource-group testrg \
    --network-security-group NSG-FrontEnd
    ```
   
    <span data-ttu-id="6e2eb-144">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="6e2eb-144">Expected output:</span></span>
   
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

## <a name="create-the-nsg-for-the-backend-subnet"></a><span data-ttu-id="6e2eb-145">Como criar o NSG para a `BackEnd` sub-rede</span><span class="sxs-lookup"><span data-stu-id="6e2eb-145">Create the NSG for the `BackEnd` subnet</span></span>
<span data-ttu-id="6e2eb-146">Siga as etapas abaixo para criar um NSG chamado *NSG-BackEnd* com base no cenário anterior.</span><span class="sxs-lookup"><span data-stu-id="6e2eb-146">To create an NSG named *NSG-BackEnd* based on the scenario preceding, follow the steps following.</span></span>

1. <span data-ttu-id="6e2eb-147">Crie o NSG `NSG-BackEnd` com **az network nsg create**.</span><span class="sxs-lookup"><span data-stu-id="6e2eb-147">Create the `NSG-BackEnd` NSG with **az network nsg create**.</span></span>
   
    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-BackEnd \
    --location centralus
    ```
   
    <span data-ttu-id="6e2eb-148">Como na etapa 2 anterior, a saída esperada é muito grande, incluindo regras padrão.</span><span class="sxs-lookup"><span data-stu-id="6e2eb-148">As in step 2, preceding, the expected output is quite large, including default rules.</span></span>
   
2. <span data-ttu-id="6e2eb-149">Execute o comando **az network nsg rule create** para criar uma regra que permite o acesso à porta 1433 (SQL) a partir da sub-rede `FrontEnd`.</span><span class="sxs-lookup"><span data-stu-id="6e2eb-149">Create a rule that allows access to port 1433 (SQL) from the `FrontEnd` subnet with the **az network nsg rule create** command.</span></span>
   
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
   
    <span data-ttu-id="6e2eb-150">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="6e2eb-150">Expected output:</span></span>

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

3. <span data-ttu-id="6e2eb-151">Execute o comando **az network nsg rule create** para criar uma regra que recusa o acesso à Internet.</span><span class="sxs-lookup"><span data-stu-id="6e2eb-151">Create a rule that denies access to the Internet using the **az network nsg rule create** command.</span></span>
   
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
   
    <span data-ttu-id="6e2eb-152">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="6e2eb-152">Expected putput:</span></span>
   
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

4. <span data-ttu-id="6e2eb-153">Associe o NSG à sub-rede `BackEnd` usando o comando **az network vnet subnet set**.</span><span class="sxs-lookup"><span data-stu-id="6e2eb-153">Bind the NSG to the `BackEnd` subnet using the **az network vnet subnet set** command.</span></span>
   
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name BackEnd \
    --resource-group testrg \
    --network-security-group NSG-BackEnd
    ```
   
    <span data-ttu-id="6e2eb-154">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="6e2eb-154">Expected output:</span></span>
   
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
