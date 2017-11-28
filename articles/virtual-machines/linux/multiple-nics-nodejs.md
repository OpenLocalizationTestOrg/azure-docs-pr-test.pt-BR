---
title: "aaaCreate uma VM do Linux no Azure com várias NICs | Microsoft Docs"
description: "Saiba como toocreate uma VM do Linux com várias NICs anexado tooit usando modelos de saudação CLI do Azure ou o Gerenciador de recursos."
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
ms.openlocfilehash: 457dab734ceeeefd35cddaf1ebb9ea0a82f4e207
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-multiple-nics-using-hello-azure-cli-10"></a><span data-ttu-id="140fc-103">Criar uma máquina virtual Linux com várias NICs usando Olá 1.0 da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="140fc-103">Create a Linux virtual machine with multiple NICs using hello Azure CLI 1.0</span></span>
<span data-ttu-id="140fc-104">Você pode criar uma máquina virtual (VM) no Azure que tenha vários tooit de interfaces (NICs) conectados a rede virtual.</span><span class="sxs-lookup"><span data-stu-id="140fc-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached tooit.</span></span> <span data-ttu-id="140fc-105">Um cenário comum é toohave várias sub-redes para conectividade de front-end e back-end ou uma rede dedicada tooa monitoramento ou solução de backup.</span><span class="sxs-lookup"><span data-stu-id="140fc-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="140fc-106">Este artigo fornece comandos rápidos toocreate uma VM com vários tooit de NICs conectadas.</span><span class="sxs-lookup"><span data-stu-id="140fc-106">This article provides quick commands toocreate a VM with multiple NICs attached tooit.</span></span> <span data-ttu-id="140fc-107">Para obter informações detalhadas, incluindo como toocreate várias NICs dentro de sua própria Bash scripts, leia mais sobre [Implantando VMs multi-NIC](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="140fc-107">For detailed information, including how toocreate multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="140fc-108">Diferentes [tamanhos de VM](sizes.md) dão suporte a um número variável de NICs, sendo assim, dimensione sua VM adequadamente.</span><span class="sxs-lookup"><span data-stu-id="140fc-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

> [!WARNING]
> <span data-ttu-id="140fc-109">Quando você cria uma VM - não é possível adicionar tooan NICs existentes VM com hello 1.0 da CLI do Azure, você deve anexar várias NICs.</span><span class="sxs-lookup"><span data-stu-id="140fc-109">You must attach multiple NICs when you create a VM - you cannot add NICs tooan existing VM with hello Azure CLI 1.0.</span></span> <span data-ttu-id="140fc-110">Você pode [adicionar NICs tooan existente VM com hello Azure CLI 2.0](multiple-nics.md).</span><span class="sxs-lookup"><span data-stu-id="140fc-110">You can [add NICs tooan existing VM with hello Azure CLI 2.0](multiple-nics.md).</span></span> <span data-ttu-id="140fc-111">Você também pode [criar uma VM com base em discos virtuais original de saudação](copy-vm.md) e crie várias NICs como implantar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="140fc-111">You can also [create a VM based on hello original virtual disk(s)](copy-vm.md) and create multiple NICs as you deploy hello VM.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="140fc-112">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="140fc-112">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="140fc-113">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="140fc-113">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="140fc-114">[1.0 de CLI do Azure](#create-supporting-resources) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="140fc-114">[Azure CLI 1.0](#create-supporting-resources) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="140fc-115">[2.0 do CLI do Azure](multiple-nics.md) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="140fc-115">[Azure CLI 2.0](multiple-nics.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="140fc-116">Criar recursos de suporte</span><span class="sxs-lookup"><span data-stu-id="140fc-116">Create supporting resources</span></span>
<span data-ttu-id="140fc-117">Certifique-se de que você tenha Olá [CLI do Azure](../../cli-install-nodejs.md) conectado e usando o modo do Gerenciador de recursos:</span><span class="sxs-lookup"><span data-stu-id="140fc-117">Make sure that you have hello [Azure CLI](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="140fc-118">Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="140fc-118">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="140fc-119">Os nomes de parâmetro de exemplo incluem *myResourceGroup*, *mystorageaccount* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="140fc-119">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="140fc-120">Em primeiro lugar, crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="140fc-120">First, create a resource group.</span></span> <span data-ttu-id="140fc-121">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local:</span><span class="sxs-lookup"><span data-stu-id="140fc-121">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

<span data-ttu-id="140fc-122">Crie suas VMs de um toohold de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="140fc-122">Create a storage account toohold your VMs.</span></span> <span data-ttu-id="140fc-123">Olá, exemplo a seguir cria uma conta de armazenamento denominada *mystorageaccount*:</span><span class="sxs-lookup"><span data-stu-id="140fc-123">hello following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
azure storage account create mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus \
    --kind Storage \
    --sku-name PLRS
```

<span data-ttu-id="140fc-124">Crie uma rede virtual tooconnect suas VMs.</span><span class="sxs-lookup"><span data-stu-id="140fc-124">Create a virtual network tooconnect your VMs to.</span></span> <span data-ttu-id="140fc-125">Olá, exemplo a seguir cria uma rede virtual denominada *myVnet* com um prefixo de endereço *192.168.0.0/16*:</span><span class="sxs-lookup"><span data-stu-id="140fc-125">hello following example creates a virtual network named *myVnet* with an address prefix of *192.168.0.0/16*:</span></span>

```azurecli
azure network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="140fc-126">Crie duas sub-redes da rede virtual – uma para o tráfego de front-end e uma para o tráfego de back-end.</span><span class="sxs-lookup"><span data-stu-id="140fc-126">Create two virtual network subnets - one for front-end traffic and one for back-end traffic.</span></span> <span data-ttu-id="140fc-127">Olá, exemplo a seguir cria duas sub-redes, denominados *mySubnetFrontEnd* e *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="140fc-127">hello following example creates two subnets, named *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

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

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="140fc-128">Criar e configurar várias NICs</span><span class="sxs-lookup"><span data-stu-id="140fc-128">Create and configure multiple NICs</span></span>
<span data-ttu-id="140fc-129">Você pode ler mais detalhes sobre [implantar várias NICs usando Olá CLI do Azure](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), incluindo o processo de saudação do loop por meio de toocreate todas as NICs de saudação de script.</span><span class="sxs-lookup"><span data-stu-id="140fc-129">You can read more details about [deploying multiple NICs using hello Azure CLI](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), including scripting hello process of looping through toocreate all hello NICs.</span></span>

<span data-ttu-id="140fc-130">Olá, exemplo a seguir cria duas NICs, denominadas *myNic1* e *myNic2*, com uma NIC conectam tooeach sub-rede:</span><span class="sxs-lookup"><span data-stu-id="140fc-130">hello following example creates two NICs, named *myNic1* and *myNic2*, with one NIC connecting tooeach subnet:</span></span>

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

<span data-ttu-id="140fc-131">Normalmente você cria também uma [grupo de segurança de rede](../../virtual-network/virtual-networks-nsg.md) ou [balanceador de carga](../../load-balancer/load-balancer-overview.md) toohelp gerenciar e distribuir o tráfego entre suas VMs.</span><span class="sxs-lookup"><span data-stu-id="140fc-131">Typically you also create a [Network Security Group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) toohelp manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="140fc-132">Olá, exemplo a seguir cria um grupo de segurança de rede denominado *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="140fc-132">hello following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="140fc-133">Associar o grupo de segurança de rede de toohello de NICs usando `azure network nic set`.</span><span class="sxs-lookup"><span data-stu-id="140fc-133">Bind your NICs toohello Network Security Group using `azure network nic set`.</span></span> <span data-ttu-id="140fc-134">Olá exemplo a seguir associa *myNic1* e *myNic2* com *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="140fc-134">hello following example binds *myNic1* and *myNic2* with *myNetworkSecurityGroup*:</span></span>

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

## <a name="create-a-vm-and-attach-hello-nics"></a><span data-ttu-id="140fc-135">Criar uma máquina virtual e anexar Olá NICs</span><span class="sxs-lookup"><span data-stu-id="140fc-135">Create a VM and attach hello NICs</span></span>
<span data-ttu-id="140fc-136">Ao criar hello VM, agora você especificar várias NICs.</span><span class="sxs-lookup"><span data-stu-id="140fc-136">When creating hello VM, you now specify multiple NICs.</span></span> <span data-ttu-id="140fc-137">Em vez disso, usando `--nic-name` tooprovide uma única NIC, em vez disso, você usar `--nic-names` e fornecer uma lista separada por vírgulas de NICs.</span><span class="sxs-lookup"><span data-stu-id="140fc-137">Rather using `--nic-name` tooprovide a single NIC, instead you use `--nic-names` and provide a comma-separated list of NICs.</span></span> <span data-ttu-id="140fc-138">Você também precisa tootake cuidado ao selecionar Olá tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="140fc-138">You also need tootake care when you select hello VM size.</span></span> <span data-ttu-id="140fc-139">Há limites para o número total de saudação de NICs que você pode adicionar tooa VM.</span><span class="sxs-lookup"><span data-stu-id="140fc-139">There are limits for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="140fc-140">Leia mais sobre [Tamanhos de VM Linux](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="140fc-140">Read more about [Linux VM sizes](sizes.md).</span></span> <span data-ttu-id="140fc-141">Olá exemplo a seguir mostra como toospecify várias NICs e, em seguida, uma VM de tamanho que dá suporte ao uso várias NICs (*Standard_DS2_v2*):</span><span class="sxs-lookup"><span data-stu-id="140fc-141">hello following example shows how toospecify multiple NICs and then a VM size that supports using multiple NICs (*Standard_DS2_v2*):</span></span>

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

## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="140fc-142">Criar várias NICs usando modelos do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="140fc-142">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="140fc-143">Modelos do Gerenciador de recursos do Azure usam toodefine declarativa de arquivos JSON seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="140fc-143">Azure Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="140fc-144">Você pode ler uma [visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="140fc-144">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="140fc-145">Modelos do Gerenciador de recursos fornecem uma maneira toocreate várias instâncias de um recurso durante a implantação, como a criação de várias NICs.</span><span class="sxs-lookup"><span data-stu-id="140fc-145">Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="140fc-146">Você usa *cópia* toospecify número de saudação do toocreate de instâncias:</span><span class="sxs-lookup"><span data-stu-id="140fc-146">You use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="140fc-147">Leia mais sobre a [criação de várias instâncias usando *copiar*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="140fc-147">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="140fc-148">Você também pode usar um `copyIndex()` toothen acrescentar um nome de recurso de tooa número, o que permite que você toocreate `myNic1`, `myNic2`, a seguir Olá etc. mostra um exemplo de acrescentar o valor de índice de saudação:</span><span class="sxs-lookup"><span data-stu-id="140fc-148">You can also use a `copyIndex()` toothen append a number tooa resource name, which allows you toocreate `myNic1`, `myNic2`, etc. hello following shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="140fc-149">Você pode ler um exemplo completo em [Criando várias NICs usando modelos do Gerenciador de Recursos](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="140fc-149">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="140fc-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="140fc-150">Next steps</span></span>
<span data-ttu-id="140fc-151">Certifique-se de que tooreview [tamanhos de VM do Linux](sizes.md) durante a tentativa de toocreating uma VM com várias NICs.</span><span class="sxs-lookup"><span data-stu-id="140fc-151">Make sure tooreview [Linux VM sizes](sizes.md) when trying toocreating a VM with multiple NICs.</span></span> <span data-ttu-id="140fc-152">Preste atenção toohello número de NICs dá suporte a cada tamanho VM.</span><span class="sxs-lookup"><span data-stu-id="140fc-152">Pay attention toohello maximum number of NICs each VM size supports.</span></span> 

<span data-ttu-id="140fc-153">Lembre-se de que você não pode adicionar tooan adicional de NICs existentes VM, você deve criar todas as NICs de hello quando você implanta Olá VM.</span><span class="sxs-lookup"><span data-stu-id="140fc-153">Remember that you cannot add additional NICs tooan existing VM, you must create all hello NICs when you deploy hello VM.</span></span> <span data-ttu-id="140fc-154">Tome cuidado ao planejar sua toomake implantações se você tem conectividade de rede todos os Olá necessário desde o início de saudação.</span><span class="sxs-lookup"><span data-stu-id="140fc-154">Take care when planning your deployments toomake sure that you have all hello required network connectivity from hello outset.</span></span>

