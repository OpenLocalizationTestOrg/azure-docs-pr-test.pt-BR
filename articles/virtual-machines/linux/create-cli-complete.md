---
title: aaaCreate ambientes Linux com hello 2.0 do CLI do Azure | Microsoft Docs
description: "Crie armazenamento, uma VM do Linux, uma rede virtual e sub-rede, um balanceador de carga, uma NIC, um IP público e um grupo de segurança de rede, tudo a partir de saudação Terra usando Olá 2.0 do CLI do Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/06/2017
ms.author: iainfou
ms.openlocfilehash: 7287ea178e76001b84dade628ead04a59dc27f40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="2704a-103">Criar uma máquina virtual concluída do Linux com hello CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="2704a-103">Create a complete Linux virtual machine with hello Azure CLI</span></span>
<span data-ttu-id="2704a-104">tooquickly criar uma máquina virtual (VM) no Azure, você pode usar um único comando CLI do Azure que usa o padrão valores toocreate qualquer necessários recursos de suporte.</span><span class="sxs-lookup"><span data-stu-id="2704a-104">tooquickly create a virtual machine (VM) in Azure, you can use a single Azure CLI command that uses default values toocreate any required supporting resources.</span></span> <span data-ttu-id="2704a-105">Recursos como uma rede virtual, um endereço IP público e regras de grupo de segurança de rede são criados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="2704a-105">Resources such as a virtual network, public IP address, and network security group rules are automatically created.</span></span> <span data-ttu-id="2704a-106">Para obter mais controle de seu ambiente de produção usar, você pode criar esses recursos antecipadamente e, em seguida, adicionar toothem suas VMs.</span><span class="sxs-lookup"><span data-stu-id="2704a-106">For more control of your environment in production use, you may create these resources ahead of time and then add your VMs toothem.</span></span> <span data-ttu-id="2704a-107">Este artigo o orienta como toocreate uma VM e cada um dos Olá recursos de suporte uma.</span><span class="sxs-lookup"><span data-stu-id="2704a-107">This article guides you through how toocreate a VM and each of hello supporting resources one by one.</span></span>

<span data-ttu-id="2704a-108">Certifique-se de que você instalou hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) e conta tooan registrada do Azure com [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="2704a-108">Make sure that you have installed hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and logged tooan Azure account in with [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="2704a-109">Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="2704a-109">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="2704a-110">Os nomes de parâmetro de exemplo incluem *myResourceGroup*, *myVnet* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="2704a-110">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="2704a-111">Criar grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="2704a-111">Create resource group</span></span>
<span data-ttu-id="2704a-112">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="2704a-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="2704a-113">Um grupo de recursos deve ser criado antes de uma máquina virtual e de recursos de rede virtual de suporte.</span><span class="sxs-lookup"><span data-stu-id="2704a-113">A resource group must be created before a virtual machine and supporting virtual network resources.</span></span> <span data-ttu-id="2704a-114">Criar grupo de recursos de saudação com [criar grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="2704a-114">Create hello resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="2704a-115">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local:</span><span class="sxs-lookup"><span data-stu-id="2704a-115">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="2704a-116">Por padrão, a saída de saudação de comandos de CLI do Azure é no JSON (JavaScript Object Notation).</span><span class="sxs-lookup"><span data-stu-id="2704a-116">By default, hello output of Azure CLI commands is in JSON (JavaScript Object Notation).</span></span> <span data-ttu-id="2704a-117">lista de tooa toochange saudação padrão saída ou tabela, por exemplo, use [az configura--saída](/cli/azure/#configure).</span><span class="sxs-lookup"><span data-stu-id="2704a-117">toochange hello default output tooa list or table, for example, use [az configure --output](/cli/azure/#configure).</span></span> <span data-ttu-id="2704a-118">Você também pode adicionar `--output` tooany comando por um período de uma alteração no formato de saída.</span><span class="sxs-lookup"><span data-stu-id="2704a-118">You can also add `--output` tooany command for a one time change in output format.</span></span> <span data-ttu-id="2704a-119">Olá, exemplo a seguir mostra a saída JSON de Olá Olá `az group create` comando:</span><span class="sxs-lookup"><span data-stu-id="2704a-119">hello following example shows hello JSON output from hello `az group create` command:</span></span>

```json                       
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "location": "eastus",
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="2704a-120">Criar a rede virtual e a sub-rede</span><span class="sxs-lookup"><span data-stu-id="2704a-120">Create a virtual network and subnet</span></span>
<span data-ttu-id="2704a-121">Em seguida, criar uma rede virtual no Azure e uma sub-rede em toowhich, você pode criar suas VMs.</span><span class="sxs-lookup"><span data-stu-id="2704a-121">Next you create a virtual network in Azure and a subnet in toowhich you can create your VMs.</span></span> <span data-ttu-id="2704a-122">Use [criar redes de rede az](/cli/azure/network/vnet#create) toocreate uma rede virtual denominada *myVnet* com hello *192.168.0.0/16* prefixo de endereço.</span><span class="sxs-lookup"><span data-stu-id="2704a-122">Use [az network vnet create](/cli/azure/network/vnet#create) toocreate a virtual network named *myVnet* with hello *192.168.0.0/16* address prefix.</span></span> <span data-ttu-id="2704a-123">Você também adicionar uma sub-rede denominada *mySubnet* com prefixo de endereço de saudação *192.168.1.0/24*:</span><span class="sxs-lookup"><span data-stu-id="2704a-123">You also add a subnet named *mySubnet* with hello address prefix of *192.168.1.0/24*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="2704a-124">saída de Hello mostra sub-rede Olá logicamente criado dentro da rede virtual hello:</span><span class="sxs-lookup"><span data-stu-id="2704a-124">hello output shows hello subnet as logically created inside hello virtual network:</span></span>

```json
{
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "location": "eastus",
  "name": "myVnet",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "ed62fd03-e9de-430b-84df-8a3b87cacdbb",
  "subnets": [
    {
      "addressPrefix": "192.168.1.0/24",
      "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
      "ipConfigurations": null,
      "name": "mySubnet",
      "networkSecurityGroup": null,
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "resourceNavigationLinks": null,
      "routeTable": null
    }
  ],
  "tags": {},
  "type": "Microsoft.Network/virtualNetworks",
  "virtualNetworkPeerings": null
}
```


## <a name="create-a-public-ip-address"></a><span data-ttu-id="2704a-125">Criar um endereço IP público</span><span class="sxs-lookup"><span data-stu-id="2704a-125">Create a public IP address</span></span>
<span data-ttu-id="2704a-126">Agora, criaremos um endereço IP público com [az network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="2704a-126">Now let's create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="2704a-127">Este endereço IP público permite que você tooconnect tooyour VMs de saudação à Internet.</span><span class="sxs-lookup"><span data-stu-id="2704a-127">This public IP address enables you tooconnect tooyour VMs from hello Internet.</span></span> <span data-ttu-id="2704a-128">Como o endereço de saudação padrão é dinâmico, também criamos uma entrada DNS nomeada com hello `--domain-name-label` opção.</span><span class="sxs-lookup"><span data-stu-id="2704a-128">Because hello default address is dynamic, we also create a named DNS entry with hello `--domain-name-label` option.</span></span> <span data-ttu-id="2704a-129">Olá, exemplo a seguir cria um IP público denominado *myPublicIP* com nome DNS de saudação do *mypublicdns*.</span><span class="sxs-lookup"><span data-stu-id="2704a-129">hello following example creates a public IP named *myPublicIP* with hello DNS name of *mypublicdns*.</span></span> <span data-ttu-id="2704a-130">Como o nome de DNS Olá deve ser exclusivo, fornece seu próprio nome DNS exclusivo:</span><span class="sxs-lookup"><span data-stu-id="2704a-130">Because hello DNS name must be unique, provide your own unique DNS name:</span></span>

```azurecli
az network public-ip create \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --dns-name mypublicdns
```

<span data-ttu-id="2704a-131">Saída:</span><span class="sxs-lookup"><span data-stu-id="2704a-131">Output:</span></span>

```json
{
  "publicIp": {
    "dnsSettings": {
      "domainNameLabel": "mypublicdns",
      "fqdn": "mypublicdns.eastus.cloudapp.azure.com",
      "reverseFqdn": null
    },
    "etag": "W/\"2632aa72-3d2d-4529-b38e-b622b4202925\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "idleTimeoutInMinutes": 4,
    "ipAddress": null,
    "ipConfiguration": null,
    "location": "eastus",
    "name": "myPublicIP",
    "provisioningState": "Succeeded",
    "publicIpAddressVersion": "IPv4",
    "publicIpAllocationMethod": "Dynamic",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "4c65de38-71f5-4684-be10-75e605b3e41f",
    "tags": null,
    "type": "Microsoft.Network/publicIPAddresses"
  }
}
```


## <a name="create-a-network-security-group"></a><span data-ttu-id="2704a-132">Criar um grupo de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="2704a-132">Create a network security group</span></span>
<span data-ttu-id="2704a-133">fluxo de saudação toocontrol de tráfego dentro e fora de suas VMs, crie um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="2704a-133">toocontrol hello flow of traffic in and out of your VMs, create a network security group.</span></span> <span data-ttu-id="2704a-134">Um grupo de segurança de rede pode ser aplicado tooa NIC ou sub-rede.</span><span class="sxs-lookup"><span data-stu-id="2704a-134">A network security group can be applied tooa NIC or subnet.</span></span> <span data-ttu-id="2704a-135">Olá exemplo a seguir usa [criar az rede nsg](/cli/azure/network/nsg#create) toocreate um grupo de segurança de rede denominado *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="2704a-135">hello following example uses [az network nsg create](/cli/azure/network/nsg#create) toocreate a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="2704a-136">Defina regras que permitem ou negam o tráfego específico hello.</span><span class="sxs-lookup"><span data-stu-id="2704a-136">You define rules that allow or deny hello specific traffic.</span></span> <span data-ttu-id="2704a-137">tooallow conexões de entrada na porta 22 (toosupport SSH), crie uma regra de entrada para o grupo de segurança de rede Olá com [criar regra de nsg rede az](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="2704a-137">tooallow inbound connections on port 22 (toosupport SSH), create an inbound rule for hello network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="2704a-138">Olá, exemplo a seguir cria uma regra denominada *myNetworkSecurityGroupRuleSSH*:</span><span class="sxs-lookup"><span data-stu-id="2704a-138">hello following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 22 \
    --access allow
```

<span data-ttu-id="2704a-139">tooallow conexões de entrada na porta 80 (toosupport o tráfego da web), adicione outra regra de grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="2704a-139">tooallow inbound connections on port 80 (toosupport web traffic), add another network security group rule.</span></span> <span data-ttu-id="2704a-140">Olá, exemplo a seguir cria uma regra denominada *myNetworkSecurityGroupRuleHTTP*:</span><span class="sxs-lookup"><span data-stu-id="2704a-140">hello following example creates a rule named *myNetworkSecurityGroupRuleHTTP*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleWeb \
    --protocol tcp \
    --priority 1001 \
    --destination-port-range 80 \
    --access allow
```

<span data-ttu-id="2704a-141">Examine o grupo de segurança de rede hello e regras com [az rede nsg exibir](/cli/azure/network/nsg#show):</span><span class="sxs-lookup"><span data-stu-id="2704a-141">Examine hello network security group and rules with [az network nsg show](/cli/azure/network/nsg#show):</span></span>

```azurecli
az network nsg show --resource-group myResourceGroup --name myNetworkSecurityGroup
```

<span data-ttu-id="2704a-142">Saída:</span><span class="sxs-lookup"><span data-stu-id="2704a-142">Output:</span></span>

```json
{
  "defaultSecurityRules": [
    {
      "access": "Allow",
      "description": "Allow inbound traffic from all VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetInBound",
      "name": "AllowVnetInBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow inbound traffic from azure load balancer",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowAzureLoadBalancerInBou
      "name": "AllowAzureLoadBalancerInBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "AzureLoadBalancer",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all inbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllInBound",
      "name": "DenyAllInBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs tooall VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetOutBound",
      "name": "AllowVnetOutBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs tooInternet",
      "destinationAddressPrefix": "Internet",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowInternetOutBound",
      "name": "AllowInternetOutBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all outbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllOutBound",
      "name": "DenyAllOutBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
  "location": "eastus",
  "name": "myNetworkSecurityGroup",
  "networkInterfaces": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "47a9964e-23a3-438a-a726-8d60ebbb1c3c",
  "securityRules": [
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "22",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleSSH",
      "name": "myNetworkSecurityGroupRuleSSH",
      "priority": 1000,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "80",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleWeb",
      "name": "myNetworkSecurityGroupRuleWeb",
      "priority": 1001,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "subnets": null,
  "tags": null,
  "type": "Microsoft.Network/networkSecurityGroups"
}
```

## <a name="create-a-virtual-nic"></a><span data-ttu-id="2704a-143">Criar um adaptador de rede virtual</span><span class="sxs-lookup"><span data-stu-id="2704a-143">Create a virtual NIC</span></span>
<span data-ttu-id="2704a-144">Placas de interface de rede virtual (NICs) estão disponíveis por meio de programação porque você pode aplicar regras tootheir uso.</span><span class="sxs-lookup"><span data-stu-id="2704a-144">Virtual network interface cards (NICs) are programmatically available because you can apply rules tootheir use.</span></span> <span data-ttu-id="2704a-145">Você também pode ter mais de uma.</span><span class="sxs-lookup"><span data-stu-id="2704a-145">You can also have more than one.</span></span> <span data-ttu-id="2704a-146">Seguir Olá [nic da rede az criar](/cli/azure/network/nic#create) de comando, você cria uma NIC denominada *myNic* e associá-lo ao grupo de segurança de rede hello.</span><span class="sxs-lookup"><span data-stu-id="2704a-146">In hello following [az network nic create](/cli/azure/network/nic#create) command, you create a NIC named *myNic* and associate it with hello network security group.</span></span> <span data-ttu-id="2704a-147">Olá endereço IP público *myPublicIP* também é associada à NIC virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="2704a-147">hello public IP address *myPublicIP* is also associated with hello virtual NIC.</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --public-ip-address myPublicIP \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="2704a-148">Saída:</span><span class="sxs-lookup"><span data-stu-id="2704a-148">Output:</span></span>

```json
{
  "NewNIC": {
    "dnsSettings": {
      "appliedDnsServers": [],
      "dnsServers": [],
      "internalDnsNameLabel": null,
      "internalDomainNameSuffix": "brqlt10lvoxedgkeuomc4pm5tb.bx.internal.cloudapp.net",
      "internalFqdn": null
    },
    "enableAcceleratedNetworking": false,
    "enableIpForwarding": false,
    "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic",
    "ipConfigurations": [
      {
        "applicationGatewayBackendAddressPools": null,
        "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic/ipConfigurations/ipconfig1",
        "loadBalancerBackendAddressPools": null,
        "loadBalancerInboundNatRules": null,
        "name": "ipconfig1",
        "primary": true,
        "privateIpAddress": "192.168.1.4",
        "privateIpAddressVersion": "IPv4",
        "privateIpAllocationMethod": "Dynamic",
        "provisioningState": "Succeeded",
        "publicIpAddress": {
          "dnsSettings": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
          "idleTimeoutInMinutes": null,
          "ipAddress": null,
          "ipConfiguration": null,
          "location": null,
          "name": null,
          "provisioningState": null,
          "publicIpAddressVersion": null,
          "publicIpAllocationMethod": null,
          "resourceGroup": "myResourceGroup",
          "resourceGuid": null,
          "tags": null,
          "type": null
        },
        "resourceGroup": "myResourceGroup",
        "subnet": {
          "addressPrefix": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
          "ipConfigurations": null,
          "name": null,
          "networkSecurityGroup": null,
          "provisioningState": null,
          "resourceGroup": "myResourceGroup",
          "resourceNavigationLinks": null,
          "routeTable": null
        }
      }
    ],
    "location": "eastus",
    "macAddress": null,
    "name": "myNic",
    "networkSecurityGroup": {
      "defaultSecurityRules": null,
      "etag": null,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
      "location": null,
      "name": null,
      "networkInterfaces": null,
      "provisioningState": null,
      "resourceGroup": "myResourceGroup",
      "resourceGuid": null,
      "securityRules": null,
      "subnets": null,
      "tags": null,
      "type": null
    },
    "primary": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "b3dbaa0e-2cf2-43be-a814-5cc49fea3304",
    "tags": null,
    "type": "Microsoft.Network/networkInterfaces",
    "virtualMachine": null
  }
}
```


## <a name="create-an-availability-set"></a><span data-ttu-id="2704a-149">Criar um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="2704a-149">Create an availability set</span></span>
<span data-ttu-id="2704a-150">Conjuntos de disponibilidade ajudam a difundir suas VMs em domínios de falha e domínios de atualização.</span><span class="sxs-lookup"><span data-stu-id="2704a-150">Availability sets help spread your VMs across fault domains and update domains.</span></span> <span data-ttu-id="2704a-151">Embora apenas criar uma máquina virtual no momento, é melhor prática toouse disponibilidade conjuntos toomake-tooexpand mais fácil no hello futuras.</span><span class="sxs-lookup"><span data-stu-id="2704a-151">Even though you only create one VM right now, it's best practice toouse availability sets toomake it easier tooexpand in hello future.</span></span> 

<span data-ttu-id="2704a-152">Os domínios de falha definem um agrupamento de máquinas virtuais que compartilham uma mesma fonte de alimentação e um mesmo comutador de rede.</span><span class="sxs-lookup"><span data-stu-id="2704a-152">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="2704a-153">Por padrão, máquinas virtuais Olá configuradas em seu conjunto de disponibilidade são separadas em domínios de falha de toothree.</span><span class="sxs-lookup"><span data-stu-id="2704a-153">By default, hello virtual machines that are configured within your availability set are separated across up toothree fault domains.</span></span> <span data-ttu-id="2704a-154">Um problema de hardware em um desses domínios de falha não afeta todas as VMs que estiverem executando seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2704a-154">A hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span>

<span data-ttu-id="2704a-155">Domínios de atualização indicam grupos de máquinas virtuais e o hardware físico subjacente que pode ser reinicializado no hello simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="2704a-155">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="2704a-156">Durante a manutenção planejada, ordem Olá no qual atualizar domínios são reiniciados pode não ser sequencial, mas somente uma atualização de domínio é reinicializado por vez.</span><span class="sxs-lookup"><span data-stu-id="2704a-156">During planned maintenance, hello order in which update domains are rebooted might not be sequential, but only one update domain is rebooted at a time.</span></span>

<span data-ttu-id="2704a-157">Azure distribui automaticamente as VMs em domínios de falha e atualização de saudação quando colocando-os em um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="2704a-157">Azure automatically distributes VMs across hello fault and update domains when placing them in an availability set.</span></span> <span data-ttu-id="2704a-158">Para obter mais informações, consulte [gerenciar a disponibilidade de saudação de VMs](manage-availability.md).</span><span class="sxs-lookup"><span data-stu-id="2704a-158">For more information, see [managing hello availability of VMs](manage-availability.md).</span></span>

<span data-ttu-id="2704a-159">Crie um conjunto de disponibilidade para sua VM com [az vm availability-set create](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="2704a-159">Create an availability set for your VM with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="2704a-160">Olá, exemplo a seguir cria um conjunto nomeada de disponibilidade *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="2704a-160">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet
```

<span data-ttu-id="2704a-161">Olá domínios de falha de anotações de saída e domínios de atualização:</span><span class="sxs-lookup"><span data-stu-id="2704a-161">hello output notes fault domains and update domains:</span></span>

```json
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet",
  "location": "eastus",
  "managed": null,
  "name": "myAvailabilitySet",
  "platformFaultDomainCount": 2,
  "platformUpdateDomainCount": 5,
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": null,
    "managed": true,
    "tier": null
  },
  "statuses": null,
  "tags": {},
  "type": "Microsoft.Compute/availabilitySets",
  "virtualMachines": []
}
```


## <a name="create-hello-linux-vms"></a><span data-ttu-id="2704a-162">Criar VMs do Linux Olá</span><span class="sxs-lookup"><span data-stu-id="2704a-162">Create hello Linux VMs</span></span>
<span data-ttu-id="2704a-163">Você criou toosupport de recursos de rede Olá VMs acessível pela Internet.</span><span class="sxs-lookup"><span data-stu-id="2704a-163">You've created hello network resources toosupport Internet-accessible VMs.</span></span> <span data-ttu-id="2704a-164">Agora crie uma VM e proteja-a com uma chave SSH.</span><span class="sxs-lookup"><span data-stu-id="2704a-164">Now create a VM and secure it with an SSH key.</span></span> <span data-ttu-id="2704a-165">Nesse caso, vamos toocreate uma VM Ubuntu com base em Olá LTS mais recente.</span><span class="sxs-lookup"><span data-stu-id="2704a-165">In this case, we're going toocreate an Ubuntu VM based on hello most recent LTS.</span></span> <span data-ttu-id="2704a-166">Você pode encontrar imagens adicionais com [az vm image list](/cli/azure/vm/image#list), conforme descrito em [localizando imagens de VM do Azure](cli-ps-findimage.md).</span><span class="sxs-lookup"><span data-stu-id="2704a-166">You can find additional images with [az vm image list](/cli/azure/vm/image#list), as described in [finding Azure VM images](cli-ps-findimage.md).</span></span>

<span data-ttu-id="2704a-167">Especificar um toouse de chave SSH para autenticação.</span><span class="sxs-lookup"><span data-stu-id="2704a-167">We also specify an SSH key toouse for authentication.</span></span> <span data-ttu-id="2704a-168">Se você não tem um par de chaves públicas SSH, você pode [criá-los](mac-create-ssh-keys.md) ou use Olá `--generate-ssh-keys` toocreate parâmetro por você.</span><span class="sxs-lookup"><span data-stu-id="2704a-168">If you do not have an SSH public key pair, you can [create them](mac-create-ssh-keys.md) or use hello `--generate-ssh-keys` parameter toocreate them for you.</span></span> <span data-ttu-id="2704a-169">Se você já tem um par de chaves, esse parâmetro usa chaves existentes em `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="2704a-169">If you already a key pair, this parameter uses existing keys in `~/.ssh`.</span></span>

<span data-ttu-id="2704a-170">Criar hello VM fazendo com que todos os nossos recursos e informações junto com hello [criar vm az](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="2704a-170">Create hello VM by bringing all our resources and information together with hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="2704a-171">Olá, exemplo a seguir cria uma VM denominada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="2704a-171">hello following example creates a VM named *myVM*:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --availability-set myAvailabilitySet \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="2704a-172">SSH tooyour VM com hello entrada DNS que você forneceu ao criar o endereço IP público de saudação.</span><span class="sxs-lookup"><span data-stu-id="2704a-172">SSH tooyour VM with hello DNS entry you provided when you created hello public IP address.</span></span> <span data-ttu-id="2704a-173">Isso `fqdn` é mostrado na saída de hello conforme você cria a VM:</span><span class="sxs-lookup"><span data-stu-id="2704a-173">This `fqdn` is shown in hello output as you create your VM:</span></span>

```json
{
  "fqdns": "mypublicdns.eastus.cloudapp.azure.com",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-13-71-C8",
  "powerState": "VM running",
  "privateIpAddress": "192.168.1.5",
  "publicIpAddress": "13.90.94.252",
  "resourceGroup": "myResourceGroup"
}
```

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

<span data-ttu-id="2704a-174">Saída:</span><span class="sxs-lookup"><span data-stu-id="2704a-174">Output:</span></span>

```bash
hello authenticity of host 'mypublicdns.eastus.cloudapp.azure.com (13.90.94.252)' can't be established.
ECDSA key fingerprint is SHA256:SylINP80Um6XRTvWiFaNz+H+1jcrKB1IiNgCDDJRj6A.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.eastus.cloudapp.azure.com,13.90.94.252' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.2 LTS (GNU/Linux 4.4.0-81-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.


hello programs included with hello Ubuntu system are free software;
hello exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, toohello extent permitted by
applicable law.

toorun a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

azureuser@myVM:~$
```

<span data-ttu-id="2704a-175">Você pode instalar NGINX e consulte toohello de fluxo de tráfego Olá VM.</span><span class="sxs-lookup"><span data-stu-id="2704a-175">You can install NGINX and see hello traffic flow toohello VM.</span></span> <span data-ttu-id="2704a-176">Instale o NGINX conforme demonstrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="2704a-176">Install NGINX as follows:</span></span>

```bash
sudo apt-get install -y nginx
```

<span data-ttu-id="2704a-177">site NGINX do toosee saudação padrão em ação, abra seu navegador da web e digite o FQDN:</span><span class="sxs-lookup"><span data-stu-id="2704a-177">toosee hello default NGINX site in action, open your web browser and enter your FQDN:</span></span>

![Site NGINX padrão na sua VM](media/create-cli-complete/nginx.png)

## <a name="export-as-a-template"></a><span data-ttu-id="2704a-179">Exportar como um modelo</span><span class="sxs-lookup"><span data-stu-id="2704a-179">Export as a template</span></span>
<span data-ttu-id="2704a-180">Se quiser toocreate um ambiente de desenvolvimento adicional com hello os mesmos parâmetros, ou em um ambiente de produção que faz a correspondência?</span><span class="sxs-lookup"><span data-stu-id="2704a-180">What if you now want toocreate an additional development environment with hello same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="2704a-181">Gerenciador de recursos usa modelos JSON que define todos os parâmetros de saudação para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="2704a-181">Resource Manager uses JSON templates that define all hello parameters for your environment.</span></span> <span data-ttu-id="2704a-182">Crie ambientes inteiros fazendo referência a esse modelo JSON.</span><span class="sxs-lookup"><span data-stu-id="2704a-182">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="2704a-183">Você pode [criar modelos JSON manualmente](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou exportar um modelo existente do ambiente toocreate Olá JSON para você.</span><span class="sxs-lookup"><span data-stu-id="2704a-183">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment toocreate hello JSON template for you.</span></span> <span data-ttu-id="2704a-184">Use [exportação de grupo az](/cli/azure/group#export) tooexport o recurso de grupo da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="2704a-184">Use [az group export](/cli/azure/group#export) tooexport your resource group as follows:</span></span>

```azurecli
az group export --name myResourceGroup > myResourceGroup.json
```

<span data-ttu-id="2704a-185">Este comando cria Olá `myResourceGroup.json` arquivo no diretório de trabalho atual.</span><span class="sxs-lookup"><span data-stu-id="2704a-185">This command creates hello `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="2704a-186">Quando você cria um ambiente com base neste modelo, você será solicitado para todos os nomes de recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="2704a-186">When you create an environment from this template, you are prompted for all hello resource names.</span></span> <span data-ttu-id="2704a-187">Você pode preencher esses nomes em seu arquivo de modelo adicionando Olá `--include-parameter-default-value` toohello parâmetro `az group export` comando.</span><span class="sxs-lookup"><span data-stu-id="2704a-187">You can populate these names in your template file by adding hello `--include-parameter-default-value` parameter toohello `az group export` command.</span></span> <span data-ttu-id="2704a-188">Editar os nomes de recurso do JSON modelo toospecify hello, ou [criar um arquivo parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) que especifica os nomes de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="2704a-188">Edit your JSON template toospecify hello resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies hello resource names.</span></span>

<span data-ttu-id="2704a-189">um ambiente de seu modelo, o uso de toocreate [criar implantação de grupo az](/cli/azure/group/deployment#create) da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="2704a-189">toocreate an environment from your template, use [az group deployment create](/cli/azure/group/deployment#create) as follows:</span></span>

```azurecli
az group deployment create \
    --resource-group myNewResourceGroup \
    --template-file myResourceGroup.json
```

<span data-ttu-id="2704a-190">Talvez você queira tooread [mais informações sobre como toodeploy modelos](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2704a-190">You might want tooread [more about how toodeploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="2704a-191">Saiba mais sobre como tooincrementally ambientes de atualização, use o arquivo de parâmetros de saudação e acessar os modelos de um único local de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2704a-191">Learn about how tooincrementally update environments, use hello parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2704a-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2704a-192">Next steps</span></span>
<span data-ttu-id="2704a-193">Agora você está pronto toobegin trabalhando com vários componentes de rede e máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="2704a-193">Now you're ready toobegin working with multiple networking components and VMs.</span></span> <span data-ttu-id="2704a-194">Você pode usar este toobuild do ambiente de exemplo do aplicativo usando os componentes principais do hello introduzidos aqui.</span><span class="sxs-lookup"><span data-stu-id="2704a-194">You can use this sample environment toobuild out your application by using hello core components introduced here.</span></span>
