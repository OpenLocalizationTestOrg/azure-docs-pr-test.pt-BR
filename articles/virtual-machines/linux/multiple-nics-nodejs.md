---
title: "Criar uma VM do Linux no Azure com várias NICs | Microsoft Docs"
description: "Saiba como criar uma VM Linux com várias NICs anexadas usando a CLI do Azure ou modelos do Resource Manager."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 814825cce61909167a1247a96c17a3ee9c5f2af4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-linux-virtual-machine-with-multiple-nics-using-the-azure-cli-10"></a><span data-ttu-id="08cf7-103">Criar uma máquina virtual Linux com várias NICs usando a CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="08cf7-103">Create a Linux virtual machine with multiple NICs using the Azure CLI 1.0</span></span>
<span data-ttu-id="08cf7-104">Você pode criar uma VM (máquina virtual) no Azure que tenha várias NICs (interfaces de rede virtual) anexadas a ela.</span><span class="sxs-lookup"><span data-stu-id="08cf7-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached to it.</span></span> <span data-ttu-id="08cf7-105">Um cenário comum é ter sub-redes diferentes para conectividade de front-end e de back-end ou uma rede dedicada a uma solução de monitoramento ou de backup.</span><span class="sxs-lookup"><span data-stu-id="08cf7-105">A common scenario is to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution.</span></span> <span data-ttu-id="08cf7-106">Este artigo fornece comandos rápidos para criar uma VM com várias NICs anexadas a ela.</span><span class="sxs-lookup"><span data-stu-id="08cf7-106">This article provides quick commands to create a VM with multiple NICs attached to it.</span></span> <span data-ttu-id="08cf7-107">Para obter informações detalhadas, incluindo como criar várias NICs dentro de seus próprios scripts Bash, leia mais sobre a [implantação de VMs com várias NICs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="08cf7-107">For detailed information, including how to create multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="08cf7-108">Diferentes [tamanhos de VM](sizes.md) dão suporte a um número variável de NICs, sendo assim, dimensione sua VM adequadamente.</span><span class="sxs-lookup"><span data-stu-id="08cf7-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

> [!WARNING]
> <span data-ttu-id="08cf7-109">Você deverá anexar várias NICs quando criar a VM – não é possível adicionar NICs a uma VM existente com a CLI do Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="08cf7-109">You must attach multiple NICs when you create a VM - you cannot add NICs to an existing VM with the Azure CLI 1.0.</span></span> <span data-ttu-id="08cf7-110">Você pode [adicionar NICs a uma VM existente com a CLI do Azure 2.0](multiple-nics.md).</span><span class="sxs-lookup"><span data-stu-id="08cf7-110">You can [add NICs to an existing VM with the Azure CLI 2.0](multiple-nics.md).</span></span> <span data-ttu-id="08cf7-111">Você também pode [criar uma VM com base nos discos virtuais originais](copy-vm.md) e criar várias NICs conforme implantar a VM.</span><span class="sxs-lookup"><span data-stu-id="08cf7-111">You can also [create a VM based on the original virtual disk(s)](copy-vm.md) and create multiple NICs as you deploy the VM.</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="08cf7-112">Versões da CLI para concluir a tarefa</span><span class="sxs-lookup"><span data-stu-id="08cf7-112">CLI versions to complete the task</span></span>
<span data-ttu-id="08cf7-113">Você pode concluir a tarefa usando uma das seguintes versões da CLI:</span><span class="sxs-lookup"><span data-stu-id="08cf7-113">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="08cf7-114">[CLI 1.0 do Azure](#create-supporting-resources) – nossa CLI para os modelos de implantação clássico e de gerenciamento de recursos (este artigo)</span><span class="sxs-lookup"><span data-stu-id="08cf7-114">[Azure CLI 1.0](#create-supporting-resources) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="08cf7-115">[CLI 2.0 do Azure](multiple-nics.md) – nossa última geração de CLI para o modelo de implantação de gerenciamento de recursos</span><span class="sxs-lookup"><span data-stu-id="08cf7-115">[Azure CLI 2.0](multiple-nics.md) - our next generation CLI for the resource management deployment model</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="08cf7-116">Criar recursos de suporte</span><span class="sxs-lookup"><span data-stu-id="08cf7-116">Create supporting resources</span></span>
<span data-ttu-id="08cf7-117">Verifique se você tem a [CLI do Azure](../../cli-install-nodejs.md) conectada e está usando o modo do Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="08cf7-117">Make sure that you have the [Azure CLI](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="08cf7-118">Nos exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="08cf7-118">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="08cf7-119">Os nomes de parâmetro de exemplo incluem *myResourceGroup*, *mystorageaccount* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="08cf7-119">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="08cf7-120">Em primeiro lugar, crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="08cf7-120">First, create a resource group.</span></span> <span data-ttu-id="08cf7-121">O exemplo a seguir cria um grupo de recursos chamado *myResourceGroup* na localização *eastus*:</span><span class="sxs-lookup"><span data-stu-id="08cf7-121">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

<span data-ttu-id="08cf7-122">Crie uma conta de armazenamento para manter suas VMs.</span><span class="sxs-lookup"><span data-stu-id="08cf7-122">Create a storage account to hold your VMs.</span></span> <span data-ttu-id="08cf7-123">O exemplo a seguir cria uma conta de armazenamento chamada *mystorageaccount*:</span><span class="sxs-lookup"><span data-stu-id="08cf7-123">The following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
azure storage account create mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus \
    --kind Storage \
    --sku-name PLRS
```

<span data-ttu-id="08cf7-124">Crie uma rede virtual à qual você conectará suas VMs.</span><span class="sxs-lookup"><span data-stu-id="08cf7-124">Create a virtual network to connect your VMs to.</span></span> <span data-ttu-id="08cf7-125">O exemplo a seguir cria uma rede virtual chamada *myVnet* com um prefixo de endereço de *192.168.0.0/16*:</span><span class="sxs-lookup"><span data-stu-id="08cf7-125">The following example creates a virtual network named *myVnet* with an address prefix of *192.168.0.0/16*:</span></span>

```azurecli
azure network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="08cf7-126">Crie duas sub-redes da rede virtual – uma para o tráfego de front-end e uma para o tráfego de back-end.</span><span class="sxs-lookup"><span data-stu-id="08cf7-126">Create two virtual network subnets - one for front-end traffic and one for back-end traffic.</span></span> <span data-ttu-id="08cf7-127">O exemplo a seguir cria duas sub-redes, chamadas *mySubnetFrontEnd* e *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="08cf7-127">The following example creates two subnets, named *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

```azurecli
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetFrontEnd \
    --address-prefix 192.168.1.0/24
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="08cf7-128">Criar e configurar várias NICs</span><span class="sxs-lookup"><span data-stu-id="08cf7-128">Create and configure multiple NICs</span></span>
<span data-ttu-id="08cf7-129">Você pode ler mais detalhes sobre a [implantação de várias NICs usando a CLI do Azure](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), incluindo o script do processo de loop para criar todas as NICs.</span><span class="sxs-lookup"><span data-stu-id="08cf7-129">You can read more details about [deploying multiple NICs using the Azure CLI](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), including scripting the process of looping through to create all the NICs.</span></span>

<span data-ttu-id="08cf7-130">O exemplo a seguir cria duas NICs, chamadas *myNic1* e *myNic2*, com uma NIC se conectando a cada sub-rede:</span><span class="sxs-lookup"><span data-stu-id="08cf7-130">The following example creates two NICs, named *myNic1* and *myNic2*, with one NIC connecting to each subnet:</span></span>

```azurecli
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic1 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetFrontEnd
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic2 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetBackEnd
```

<span data-ttu-id="08cf7-131">Normalmente, você também criaria um [Grupo de Segurança de Rede](../../virtual-network/virtual-networks-nsg.md) ou [balanceador de carga](../../load-balancer/load-balancer-overview.md) para ajudar a gerenciar e distribuir o tráfego entre suas VMs.</span><span class="sxs-lookup"><span data-stu-id="08cf7-131">Typically you also create a [Network Security Group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) to help manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="08cf7-132">O exemplo a seguir cria um Grupo de Segurança de Rede chamado *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="08cf7-132">The following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="08cf7-133">Associe as NICs ao Grupo de Segurança de Rede usando `azure network nic set`.</span><span class="sxs-lookup"><span data-stu-id="08cf7-133">Bind your NICs to the Network Security Group using `azure network nic set`.</span></span> <span data-ttu-id="08cf7-134">O exemplo a seguir associa *myNic1* e *myNic2* a *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="08cf7-134">The following example binds *myNic1* and *myNic2* with *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic1 \
    --network-security-group-name myNetworkSecurityGroup
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic2 \
    --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-the-nics"></a><span data-ttu-id="08cf7-135">Criar uma VM e conectar as NICs</span><span class="sxs-lookup"><span data-stu-id="08cf7-135">Create a VM and attach the NICs</span></span>
<span data-ttu-id="08cf7-136">Ao criar a VM, agora você especifica várias NICs.</span><span class="sxs-lookup"><span data-stu-id="08cf7-136">When creating the VM, you now specify multiple NICs.</span></span> <span data-ttu-id="08cf7-137">Em vez de usar `--nic-name` para fornecer uma única NIC, você usa `--nic-names` e fornece uma lista de NICs separada por vírgulas.</span><span class="sxs-lookup"><span data-stu-id="08cf7-137">Rather using `--nic-name` to provide a single NIC, instead you use `--nic-names` and provide a comma-separated list of NICs.</span></span> <span data-ttu-id="08cf7-138">Você também precisa tomar cuidado ao selecionar o tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="08cf7-138">You also need to take care when you select the VM size.</span></span> <span data-ttu-id="08cf7-139">Há limites para o número total de NICs que podem ser adicionados a uma VM.</span><span class="sxs-lookup"><span data-stu-id="08cf7-139">There are limits for the total number of NICs that you can add to a VM.</span></span> <span data-ttu-id="08cf7-140">Leia mais sobre [Tamanhos de VM Linux](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="08cf7-140">Read more about [Linux VM sizes](sizes.md).</span></span> <span data-ttu-id="08cf7-141">O exemplo a seguir mostra como especificar várias NICs e, em seguida, um tamanho de VM que dê suporte ao uso de várias NICs (*Standard_DS2_v2*):</span><span class="sxs-lookup"><span data-stu-id="08cf7-141">The following example shows how to specify multiple NICs and then a VM size that supports using multiple NICs (*Standard_DS2_v2*):</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --os-type linux \
    --nic-names myNic1,myNic2 \
    --vm-size Standard_DS2_v2 \
    --storage-account-name mystorageaccount \
    --image-urn UbuntuLTS \
    --admin-username azureuser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub
```

## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="08cf7-142">Criar várias NICs usando modelos do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="08cf7-142">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="08cf7-143">Os modelos do Azure Resource Manager usam arquivos JSON declarativos para definir o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="08cf7-143">Azure Resource Manager templates use declarative JSON files to define your environment.</span></span> <span data-ttu-id="08cf7-144">Você pode ler uma [visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="08cf7-144">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="08cf7-145">Os modelos do Gerenciador de Recursos oferecem uma maneira de criar várias instâncias de um recurso durante a implantação, como a criação de várias NICs.</span><span class="sxs-lookup"><span data-stu-id="08cf7-145">Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="08cf7-146">Você usa *copiar* para especificar o número de instâncias a serem criadas:</span><span class="sxs-lookup"><span data-stu-id="08cf7-146">You use *copy* to specify the number of instances to create:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="08cf7-147">Leia mais sobre a [criação de várias instâncias usando *copiar*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="08cf7-147">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="08cf7-148">Você também pode usar um `copyIndex()` para acrescentar um número a um nome de recurso, o que lhe permite criar `myNic1`, `myNic2` etc. Veja a seguir um exemplo de como acrescentar o valor de índice:</span><span class="sxs-lookup"><span data-stu-id="08cf7-148">You can also use a `copyIndex()` to then append a number to a resource name, which allows you to create `myNic1`, `myNic2`, etc. The following shows an example of appending the index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="08cf7-149">Você pode ler um exemplo completo em [Criando várias NICs usando modelos do Gerenciador de Recursos](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="08cf7-149">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="08cf7-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="08cf7-150">Next steps</span></span>
<span data-ttu-id="08cf7-151">Certifique-se de rever os [Tamanhos de VM Linux](sizes.md) ao tentar criar uma VM com várias NICs.</span><span class="sxs-lookup"><span data-stu-id="08cf7-151">Make sure to review [Linux VM sizes](sizes.md) when trying to creating a VM with multiple NICs.</span></span> <span data-ttu-id="08cf7-152">Preste atenção ao número máximo de NICs a que cada VM dá suporte.</span><span class="sxs-lookup"><span data-stu-id="08cf7-152">Pay attention to the maximum number of NICs each VM size supports.</span></span> 

<span data-ttu-id="08cf7-153">Lembre-se de que você não pode adicionar mais NICs a uma VM existente; você deve criar todas as NICs quando implantar a VM.</span><span class="sxs-lookup"><span data-stu-id="08cf7-153">Remember that you cannot add additional NICs to an existing VM, you must create all the NICs when you deploy the VM.</span></span> <span data-ttu-id="08cf7-154">Tome cuidado ao planejar suas implantações para certificar-se de que tenha toda a conectividade de rede necessária desde o início.</span><span class="sxs-lookup"><span data-stu-id="08cf7-154">Take care when planning your deployments to make sure that you have all the required network connectivity from the outset.</span></span>

