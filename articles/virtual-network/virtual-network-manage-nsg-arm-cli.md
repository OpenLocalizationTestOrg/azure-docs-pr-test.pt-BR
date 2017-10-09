---
title: "aaaManage 2.0 do CLI do Azure de grupos de segurança - rede | Microsoft Docs"
description: "Saiba como grupos de segurança de rede toomanage usando hello Azure interface de linha de comando (CLI) 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ed17d314-07e6-4c7f-bcf1-a8a2535d7c14
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a3036b465e1e4049cba00e5e13ce1b479a2301d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-cli-20"></a><span data-ttu-id="b4b73-103">Gerenciar grupos de segurança de rede usando Olá 2.0 do CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="b4b73-103">Manage network security groups using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="b4b73-104">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="b4b73-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="b4b73-105">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4b73-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="b4b73-106">[1.0 de CLI do Azure](virtual-network-manage-nsg-cli-nodejs.md) – nosso CLI para modelos de implantação de gerenciamento de recursos e clássico de Olá</span><span class="sxs-lookup"><span data-stu-id="b4b73-106">[Azure CLI 1.0](virtual-network-manage-nsg-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="b4b73-107">[2.0 do CLI do Azure](#View-existing-NSGs) -nossa próxima geração CLI para modelo de implantação de gerenciamento de recursos de saudação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="b4b73-107">[Azure CLI 2.0](#View-existing-NSGs) - our next generation CLI for hello resource management deployment model (this article)</span></span>


[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="b4b73-108">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b4b73-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b4b73-109">Este artigo aborda usando o modelo de implantação do hello Gerenciador de recursos, a Microsoft recomenda para a maioria das novas implantações em vez do modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="b4b73-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="prerequisite"></a><span data-ttu-id="b4b73-110">Pré-requisito</span><span class="sxs-lookup"><span data-stu-id="b4b73-110">Prerequisite</span></span>
<span data-ttu-id="b4b73-111">Se você ainda não tiver ainda, instalar e configurar hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) e fazer logon na conta do Azure usando o tooan [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="b4b73-111">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 


## <a name="view-existing-nsgs"></a><span data-ttu-id="b4b73-112">Exibir NSGs existentes</span><span class="sxs-lookup"><span data-stu-id="b4b73-112">View existing NSGs</span></span>
<span data-ttu-id="b4b73-113">lista de saudação do tooview de NSGs em um grupo de recursos específico, execute Olá [lista de nsg de rede az](/cli/azure/network/nsg#list) com um `-o table` formato de saída:</span><span class="sxs-lookup"><span data-stu-id="b4b73-113">tooview hello list of NSGs in a specific resource group, run hello [az network nsg list](/cli/azure/network/nsg#list) command with a `-o table` output format:</span></span>

```azurecli
az network nsg list -g RG-NSG -o table
```

<span data-ttu-id="b4b73-114">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="b4b73-114">Expected output:</span></span>

    Location    Name          ProvisioningState    ResourceGroup    ResourceGuid
    ----------  ------------  -------------------  ---------------  ------------------------------------
    centralus   NSG-BackEnd   Succeeded            RG-NSG           <guid>
    centralus   NSG-FrontEnd  Succeeded            RG-NSG           <guid>

## <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="b4b73-115">Listar todas as regras de um NSG</span><span class="sxs-lookup"><span data-stu-id="b4b73-115">List all rules for an NSG</span></span>
<span data-ttu-id="b4b73-116">regras de saudação tooview de um NSG denominado **NSG-front-end**, execute hello [az rede nsg exibir](/cli/azure/network/nsg#show) comando usando um [filtro de consulta JMESPATH](/cli/azure/query-az-cli2) e hello `-o table` formato de saída:</span><span class="sxs-lookup"><span data-stu-id="b4b73-116">tooview hello rules of an NSG named **NSG-FrontEnd**, run hello [az network nsg show](/cli/azure/network/nsg#show) command using a [JMESPATH query filter](/cli/azure/query-az-cli2) and hello `-o table` output format:</span></span>

```azurecli
    az network nsg show \
    --resource-group RG-NSG \
    --name NSG-FrontEnd \
    --query '[defaultSecurityRules[],securityRules[]][].{Name:name,Desc:description,Access:access,Direction:direction,DestPortRange:destinationPortRange,DestAddrPrefix:destinationAddressPrefix,SrcPortRange:sourcePortRange,SrcAddrPrefix:sourceAddressPrefix}' \
    -o table
```

<span data-ttu-id="b4b73-117">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="b4b73-117">Expected output:</span></span>

    Name                           Desc                                                    Access    Direction    DestPortRange    DestAddrPrefix    SrcPortRange    SrcAddrPrefix
    -----------------------------  ------------------------------------------------------  --------  -----------  ---------------  ----------------  --------------  -----------------
    AllowVnetInBound               Allow inbound traffic from all VMs in VNET              Allow     Inbound      *                VirtualNetwork    *               VirtualNetwork
    AllowAzureLoadBalancerInBound  Allow inbound traffic from azure load balancer          Allow     Inbound      *                *                 *               AzureLoadBalancer
    DenyAllInBound                 Deny all inbound traffic                                Deny      Inbound      *                *                 *               *
    AllowVnetOutBound              Allow outbound traffic from all VMs tooall VMs in VNET  Allow     Outbound     *                VirtualNetwork    *               VirtualNetwork
    AllowInternetOutBound          Allow outbound traffic from all VMs tooInternet         Allow     Outbound     *                Internet          *               *
    DenyAllOutBound                Deny all outbound traffic                               Deny      Outbound     *                *                 *               *
    rdp-rule                                                                               Allow     Inbound      3389             *                 *               Internet
    web-rule                                                                               Allow     Inbound      80               *                 *               Internet
> [!NOTE]
> <span data-ttu-id="b4b73-118">Você também pode usar [lista de regras az rede nsg](/cli/azure/network/nsg/rule#list) toolist somente Olá regras personalizadas de um NSG.</span><span class="sxs-lookup"><span data-stu-id="b4b73-118">You can also use [az network nsg rule list](/cli/azure/network/nsg/rule#list) toolist only hello custom rules from an NSG .</span></span>
>

## <a name="view-nsg-associations"></a><span data-ttu-id="b4b73-119">Exibir associações de NSG</span><span class="sxs-lookup"><span data-stu-id="b4b73-119">View NSG associations</span></span>

<span data-ttu-id="b4b73-120">tooview Olá quais recursos **NSG-front-end** NSG está associado ao, execute Olá `az network nsg show` comando conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="b4b73-120">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello `az network nsg show` command as shown below.</span></span> 

```azurecli
az network nsg show -g RG-NSG -n nsg-frontend --query '[subnets,networkInterfaces]'
```

<span data-ttu-id="b4b73-121">Procure Olá **networkInterfaces** e **sub-redes** propriedades conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="b4b73-121">Look for hello **networkInterfaces** and **subnets** properties as shown below:</span></span>

```json
[
  [
    {
      "addressPrefix": null,
      "etag": null,
      "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/FrontEnd",
      "ipConfigurations": null,
      "name": null,
      "networkSecurityGroup": null,
      "provisioningState": null,
      "resourceGroup": "RG-NSG",
      "resourceNavigationLinks": null,
      "routeTable": null
    }
  ],
  null
]
```

<span data-ttu-id="b4b73-122">O exemplo hello acima, Olá NSG não está associado tooany interfaces de rede (NICs) e é associado tooa sub-rede denominada **front-end**.</span><span class="sxs-lookup"><span data-stu-id="b4b73-122">In hello example above, hello NSG is not associated tooany network interfaces (NICs), and it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="add-a-rule"></a><span data-ttu-id="b4b73-123">Adicionar uma regra</span><span class="sxs-lookup"><span data-stu-id="b4b73-123">Add a rule</span></span>
<span data-ttu-id="b4b73-124">tooadd uma regra permitindo **entrada** tráfego tooport **443** de qualquer máquina toohello **NSG-front-end** NSG, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4b73-124">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, enter hello following command:</span></span>

```azurecli
az network nsg rule create  \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd  \
--name allow-https \
--description "Allow access tooport 443 for HTTPS" \
--access Allow \
--protocol Tcp  \
--direction Inbound \
--priority 102 \
--source-address-prefix "*"  \
--source-port-range "*"  \
--destination-address-prefix "*" \
--destination-port-range "443"
```

<span data-ttu-id="b4b73-125">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="b4b73-125">Expected output:</span></span>

```json
{
  "access": "Allow",
  "description": "Allow access tooport 443 for HTTPS",
  "destinationAddressPrefix": "*",
  "destinationPortRange": "443",
  "direction": "Inbound",
  "etag": "W/\"<guid>\"",
  "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https",
  "name": "allow-https",
  "priority": 102,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "RG-NSG",
  "sourceAddressPrefix": "*",
  "sourcePortRange": "*"
}
```

## <a name="change-a-rule"></a><span data-ttu-id="b4b73-126">Alterar uma regra</span><span class="sxs-lookup"><span data-stu-id="b4b73-126">Change a rule</span></span>
<span data-ttu-id="b4b73-127">regra de saudação toochange criada acima tooallow Olá o tráfego de entrada **Internet** somente executar Olá [atualização de regras do nsg de rede az](/cli/azure/network/nsg/rule#update) comando:</span><span class="sxs-lookup"><span data-stu-id="b4b73-127">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command:</span></span>

```azurecli
az network nsg rule update \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https \
--source-address-prefix Internet
```

<span data-ttu-id="b4b73-128">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="b4b73-128">Expected output:</span></span>

```json
{
"access": "Allow",
"description": "Allow access tooport 443 for HTTPS",
"destinationAddressPrefix": "*",
"destinationPortRange": "443",
"direction": "Inbound",
"etag": "W/\"<guid>\"",
"id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https",
"name": "allow-https",
"priority": 102,
"protocol": "Tcp",
"provisioningState": "Succeeded",
"resourceGroup": "RG-NSG",
"sourceAddressPrefix": "Internet",
"sourcePortRange": "*"
}
```

## <a name="delete-a-rule"></a><span data-ttu-id="b4b73-129">Excluir uma regra</span><span class="sxs-lookup"><span data-stu-id="b4b73-129">Delete a rule</span></span>
<span data-ttu-id="b4b73-130">regra de saudação toodelete criou acima, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4b73-130">toodelete hello rule created above, run hello following command:</span></span>

```azurecli
az network nsg rule delete \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https
```


## <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="b4b73-131">Associar um NSG tooa NIC</span><span class="sxs-lookup"><span data-stu-id="b4b73-131">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="b4b73-132">Olá tooassociate **NSG-front-end** NSG toohello **TestNICWeb1** NIC, use Olá [atualização da nic de rede az](/cli/azure/network/nic#update) comando:</span><span class="sxs-lookup"><span data-stu-id="b4b73-132">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, use hello [az network nic update](/cli/azure/network/nic#update) command:</span></span>

```azurecli
az network nic update \
--resource-group RG-NSG \
--name TestNICWeb1 \
--network-security-group NSG-FrontEnd    
```

<span data-ttu-id="b4b73-133">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="b4b73-133">Expected output:</span></span>

```json
{
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": [],
    "internalDnsNameLabel": null,
    "internalDomainNameSuffix": "k0wkaguidnqrh0ud.gx.internal.cloudapp.net",
    "internalFqdn": null
  },
  "enableAcceleratedNetworking": false,
  "enableIpForwarding": false,
  "etag": "W/\"<guid>\"",
  "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1",
  "ipConfigurations": [
    {
      "applicationGatewayBackendAddressPools": null,
      "etag": "W/\"<guid>\"",
      "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1",
      "loadBalancerBackendAddressPools": null,
      "loadBalancerInboundNatRules": null,
      "name": "ipconfig1",
      "primary": true,
      "privateIpAddress": "192.168.1.6",
      "privateIpAddressVersion": "IPv4",
      "privateIpAllocationMethod": "Static",
      "provisioningState": "Succeeded",
      "publicIpAddress": null,
      "resourceGroup": "RG-NSG",
      "subnet": {
        "addressPrefix": null,
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
        "ipConfigurations": null,
        "name": null,
        "networkSecurityGroup": null,
        "provisioningState": null,
        "resourceGroup": "RG-NSG",
        "resourceNavigationLinks": null,
        "routeTable": null
      }
    }
  ],
  "location": "centralus",
  "macAddress": "00-0D-3A-91-A9-60",
  "name": "TestNICWeb1",
  "networkSecurityGroup": {
    "defaultSecurityRules": null,
    "etag": null,
    "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
    "location": null,
    "name": null,
    "networkInterfaces": null,
    "provisioningState": null,
    "resourceGroup": "RG-NSG",
    "resourceGuid": null,
    "securityRules": null,
    "subnets": null,
    "tags": null,
    "type": null
  },
  "primary": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "RG-NSG",
  "resourceGuid": "<guid>",
  "tags": {},
  "type": "Microsoft.Network/networkInterfaces",
  "virtualMachine": null
}
```

## <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="b4b73-134">Desassociar um NSG de uma NIC</span><span class="sxs-lookup"><span data-stu-id="b4b73-134">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="b4b73-135">Olá toodissociate **NSG-front-end** NSG de saudação **TestNICWeb1** NIC, executar Olá [atualização de regra az rede nsg](/cli/azure/network/nsg/rule#update) comando novamente, mas substitua Olá `--network-security-group` argumento com uma cadeia de caracteres vazia (`""`).</span><span class="sxs-lookup"><span data-stu-id="b4b73-135">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command again but replace hello `--network-security-group` argument with an empty string (`""`).</span></span>

```azurecli
az network nic update --resource-group RG-NSG --name TestNICWeb3 --network-security-group ""
```

<span data-ttu-id="b4b73-136">Na saída de Olá Olá `networkSecurityGroup` chave é definida toonull.</span><span class="sxs-lookup"><span data-stu-id="b4b73-136">In hello output, hello `networkSecurityGroup` key is set toonull.</span></span>

## <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="b4b73-137">Desassociar um NSG de uma sub-rede</span><span class="sxs-lookup"><span data-stu-id="b4b73-137">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="b4b73-138">Olá toodissociate **NSG-front-end** NSG de saudação **front-end** sub-rede, execute novamente o hello [atualização de regra az rede nsg](/cli/azure/network/nsg/rule#update) comando novamente, mas substitua Olá `--network-security-group` argumento com uma cadeia de caracteres vazia (`""`).</span><span class="sxs-lookup"><span data-stu-id="b4b73-138">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, again run hello [az network nsg rule update](/cli/azure/network/nsg/rule#update) command again but replace hello `--network-security-group` argument with an empty string (`""`).</span></span>

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group ""
```

<span data-ttu-id="b4b73-139">Na saída de Olá Olá `networkSecurityGroup` chave é definida toonull.</span><span class="sxs-lookup"><span data-stu-id="b4b73-139">In hello output, hello `networkSecurityGroup` key is set toonull.</span></span>

## <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="b4b73-140">Associar uma sub-rede de tooa NSG</span><span class="sxs-lookup"><span data-stu-id="b4b73-140">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="b4b73-141">Olá tooassociate **NSG-front-end** NSG toohello **front-end** sub-rede novamente, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4b73-141">tooassociate hello **NSG-FrontEnd** NSG toohello **FrontEnd** subnet again, run hello following command:</span></span>

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group NSG-FrontEnd
```

<span data-ttu-id="b4b73-142">Na saída de Olá Olá `networkSecurityGroup` chave tem algo semelhante para o valor de saudação:</span><span class="sxs-lookup"><span data-stu-id="b4b73-142">In hello output, hello `networkSecurityGroup` key has something similar for hello value:</span></span>

```json
"networkSecurityGroup": {
    "defaultSecurityRules": null,
    "etag": null,
    "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
    "location": null,
    "name": null,
    "networkInterfaces": null,
    "provisioningState": null,
    "resourceGroup": "RG-NSG",
    "resourceGuid": null,
    "securityRules": null,
    "subnets": null,
    "tags": null,
    "type": null
  }
  ```

## <a name="delete-an-nsg"></a><span data-ttu-id="b4b73-143">Excluir um NSG</span><span class="sxs-lookup"><span data-stu-id="b4b73-143">Delete an NSG</span></span>
<span data-ttu-id="b4b73-144">Você só pode excluir um NSG se ela não está associada tooany recursos.</span><span class="sxs-lookup"><span data-stu-id="b4b73-144">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="b4b73-145">toodelete um NSG, siga as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="b4b73-145">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="b4b73-146">recursos de saudação toocheck associado tooan NSG, execute Olá `azure network nsg show` conforme mostrado na [NSGs exibir associações](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="b4b73-146">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="b4b73-147">Se Olá NSG é associado tooany NICs, execute Olá `azure network nic set` conforme mostrado na [dissociar um NSG de uma NIC](#Dissociate-an-NSG-from-a-NIC) para cada NIC.</span><span class="sxs-lookup"><span data-stu-id="b4b73-147">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="b4b73-148">Se Olá NSG sub-rede associada tooany, execute Olá `azure network vnet subnet set` conforme mostrado na [dissociar um NSG de uma sub-rede](#Dissociate-an-NSG-from-a-subnet) para cada sub-rede.</span><span class="sxs-lookup"><span data-stu-id="b4b73-148">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="b4b73-149">Olá toodelete NSG, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4b73-149">toodelete hello NSG, run hello following command:</span></span>

    ```azurecli
    az network nsg delete --resource-group RG-NSG --name NSG-FrontEnd
    ```
## <a name="next-steps"></a><span data-ttu-id="b4b73-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b4b73-150">Next steps</span></span>
* <span data-ttu-id="b4b73-151">[Habilitar registro em log](virtual-network-nsg-manage-log.md) para NSGs.</span><span class="sxs-lookup"><span data-stu-id="b4b73-151">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

