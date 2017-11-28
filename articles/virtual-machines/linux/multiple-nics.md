---
title: "aaaCreate uma VM do Linux no Azure com várias NICs | Microsoft Docs"
description: "Saiba como toocreate uma VM do Linux com várias NICs anexado tooit usando modelos de hello Azure 2.0 do CLI ou o Gerenciador de recursos."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 5d2d04d0-fc62-45fa-88b1-61808a2bc691
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2723405914777a5dce4354d4f5d8413e357f58e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a><span data-ttu-id="ef45d-103">Como toocreate uma máquina de virtual do Linux no Azure com rede várias placas de interface</span><span class="sxs-lookup"><span data-stu-id="ef45d-103">How toocreate a Linux virtual machine in Azure with multiple network interface cards</span></span>
<span data-ttu-id="ef45d-104">Você pode criar uma máquina virtual (VM) no Azure que tenha vários tooit de interfaces (NICs) conectados a rede virtual.</span><span class="sxs-lookup"><span data-stu-id="ef45d-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached tooit.</span></span> <span data-ttu-id="ef45d-105">Um cenário comum é toohave várias sub-redes para conectividade de front-end e back-end ou uma rede dedicada tooa monitoramento ou solução de backup.</span><span class="sxs-lookup"><span data-stu-id="ef45d-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="ef45d-106">Este artigo detalha como toocreate uma VM com várias NICs anexado tooit e NICs tooadd ou remover de uma VM existente.</span><span class="sxs-lookup"><span data-stu-id="ef45d-106">This article details how toocreate a VM with multiple NICs attached tooit and how tooadd or remove NICs from an existing VM.</span></span> <span data-ttu-id="ef45d-107">Para obter informações detalhadas, incluindo como toocreate várias NICs dentro de sua própria Bash scripts, leia mais sobre [Implantando VMs multi-NIC](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ef45d-107">For detailed information, including how toocreate multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="ef45d-108">Diferentes [tamanhos de VM](sizes.md) dão suporte a um número variável de NICs, sendo assim, dimensione sua VM adequadamente.</span><span class="sxs-lookup"><span data-stu-id="ef45d-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="ef45d-109">Este artigo fornece detalhes sobre como toocreate uma VM com várias NICs com hello 2.0 do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="ef45d-109">This article details how toocreate a VM with multiple NICs with hello Azure CLI 2.0.</span></span> <span data-ttu-id="ef45d-110">Você também pode executar essas etapas com hello [Azure CLI 1.0](multiple-nics-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="ef45d-110">You can also perform these steps with hello [Azure CLI 1.0](multiple-nics-nodejs.md).</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="ef45d-111">Criar recursos de suporte</span><span class="sxs-lookup"><span data-stu-id="ef45d-111">Create supporting resources</span></span>
<span data-ttu-id="ef45d-112">Saudação de instalação mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) e fazer logon na conta do Azure usando o tooan [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="ef45d-112">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="ef45d-113">Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="ef45d-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="ef45d-114">Os nomes de parâmetro de exemplo incluem *myResourceGroup*, *mystorageaccount* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="ef45d-114">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="ef45d-115">Primeiro, crie um grupo de recursos com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="ef45d-115">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="ef45d-116">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local:</span><span class="sxs-lookup"><span data-stu-id="ef45d-116">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="ef45d-117">Criar rede virtual de saudação com [criar redes de rede az](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="ef45d-117">Create hello virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="ef45d-118">Olá, exemplo a seguir cria uma rede virtual denominada *myVnet* e sub-rede denominada *mySubnetFrontEnd*:</span><span class="sxs-lookup"><span data-stu-id="ef45d-118">hello following example creates a virtual network named *myVnet* and subnet named *mySubnetFrontEnd*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="ef45d-119">Criar uma sub-rede para o tráfego de back-end de saudação com [sub-rede de rede virtual de rede az criar](/cli/azure/network/vnet/subnet#create).</span><span class="sxs-lookup"><span data-stu-id="ef45d-119">Create a subnet for hello back-end traffic with [az network vnet subnet create](/cli/azure/network/vnet/subnet#create).</span></span> <span data-ttu-id="ef45d-120">Olá, exemplo a seguir cria uma sub-rede denominada *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="ef45d-120">hello following example creates a subnet named *mySubnetBackEnd*:</span></span>

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

<span data-ttu-id="ef45d-121">Crie um grupo de segurança de rede com [az network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="ef45d-121">Create a network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="ef45d-122">Olá, exemplo a seguir cria um grupo de segurança de rede denominado *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="ef45d-122">hello following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="ef45d-123">Criar e configurar várias NICs</span><span class="sxs-lookup"><span data-stu-id="ef45d-123">Create and configure multiple NICs</span></span>
<span data-ttu-id="ef45d-124">Crie duas NICs com [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="ef45d-124">Create two NICs with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="ef45d-125">Olá, exemplo a seguir cria duas NICs, denominadas *myNic1* e *myNic2*conectados grupo de segurança de rede hello, com uma NIC conectam tooeach sub-rede:</span><span class="sxs-lookup"><span data-stu-id="ef45d-125">hello following example creates two NICs, named *myNic1* and *myNic2*, connected hello network security group, with one NIC connecting tooeach subnet:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic1 \
    --vnet-name myVnet \
    --subnet mySubnetFrontEnd \
    --network-security-group myNetworkSecurityGroup
az network nic create \
    --resource-group myResourceGroup \
    --name myNic2 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a><span data-ttu-id="ef45d-126">Criar uma máquina virtual e anexar Olá NICs</span><span class="sxs-lookup"><span data-stu-id="ef45d-126">Create a VM and attach hello NICs</span></span>
<span data-ttu-id="ef45d-127">Quando você cria Olá VM, especifique Olá NICs criado com `--nics`.</span><span class="sxs-lookup"><span data-stu-id="ef45d-127">When you create hello VM, specify hello NICs you created with `--nics`.</span></span> <span data-ttu-id="ef45d-128">Você também precisa tootake cuidado ao selecionar Olá tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="ef45d-128">You also need tootake care when you select hello VM size.</span></span> <span data-ttu-id="ef45d-129">Há limites para o número total de saudação de NICs que você pode adicionar tooa VM.</span><span class="sxs-lookup"><span data-stu-id="ef45d-129">There are limits for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="ef45d-130">Leia mais sobre [Tamanhos de VM Linux](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="ef45d-130">Read more about [Linux VM sizes](sizes.md).</span></span> 

<span data-ttu-id="ef45d-131">Crie uma VM com [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="ef45d-131">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="ef45d-132">Olá, exemplo a seguir cria uma VM denominada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="ef45d-132">hello following example creates a VM named *myVM*:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --size Standard_DS3_v2 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic1 myNic2
```

## <a name="add-a-nic-tooa-vm"></a><span data-ttu-id="ef45d-133">Adicionar uma NIC tooa VM</span><span class="sxs-lookup"><span data-stu-id="ef45d-133">Add a NIC tooa VM</span></span>
<span data-ttu-id="ef45d-134">etapas anteriores Olá criou uma VM com várias NICs.</span><span class="sxs-lookup"><span data-stu-id="ef45d-134">hello previous steps created a VM with multiple NICs.</span></span> <span data-ttu-id="ef45d-135">Você também pode adicionar tooan NICs existentes VM com hello 2.0 do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="ef45d-135">You can also add NICs tooan existing VM with hello Azure CLI 2.0.</span></span> 

<span data-ttu-id="ef45d-136">Crie outra NIC com [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="ef45d-136">Create another NIC with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="ef45d-137">Olá, exemplo a seguir cria uma NIC denominada *myNic3* conectados toohello sub-rede de back-end e o grupo de segurança de rede criado nas etapas anteriores hello:</span><span class="sxs-lookup"><span data-stu-id="ef45d-137">hello following example creates a NIC named *myNic3* connected toohello back-end subnet and network security group created in hello previous steps:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="ef45d-138">tooadd tooan uma placa de rede VM existente, primeiro desalocar Olá VM com [az vm desalocar](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="ef45d-138">tooadd a NIC tooan existing VM, first deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="ef45d-139">exemplo a seguir Hello desaloca Olá VM denominada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="ef45d-139">hello following example deallocates hello VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="ef45d-140">Adicionar Olá NIC com [nic de vm az adicionar](/cli/azure/vm/nic#add).</span><span class="sxs-lookup"><span data-stu-id="ef45d-140">Add hello NIC with [az vm nic add](/cli/azure/vm/nic#add).</span></span> <span data-ttu-id="ef45d-141">Olá exemplo a seguir adiciona *myNic3* muito*myVM*:</span><span class="sxs-lookup"><span data-stu-id="ef45d-141">hello following example adds *myNic3* too*myVM*:</span></span>

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

<span data-ttu-id="ef45d-142">Iniciar Olá VM com [início de vm az](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="ef45d-142">Start hello VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

## <a name="remove-a-nic-from-a-vm"></a><span data-ttu-id="ef45d-143">Remover uma NIC de uma VM</span><span class="sxs-lookup"><span data-stu-id="ef45d-143">Remove a NIC from a VM</span></span>
<span data-ttu-id="ef45d-144">tooremove uma NIC de uma VM existente, primeiro desalocar Olá VM com [az vm desalocar](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="ef45d-144">tooremove a NIC from an existing VM, first deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="ef45d-145">exemplo a seguir Hello desaloca Olá VM denominada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="ef45d-145">hello following example deallocates hello VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="ef45d-146">Remover Olá NIC com [nic de vm az remover](/cli/azure/vm/nic#remove).</span><span class="sxs-lookup"><span data-stu-id="ef45d-146">Remove hello NIC with [az vm nic remove](/cli/azure/vm/nic#remove).</span></span> <span data-ttu-id="ef45d-147">Olá exemplo a seguir remove *myNic3* de *myVM*:</span><span class="sxs-lookup"><span data-stu-id="ef45d-147">hello following example removes *myNic3* from *myVM*:</span></span>

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM 
    --nics myNic3
```

<span data-ttu-id="ef45d-148">Iniciar Olá VM com [início de vm az](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="ef45d-148">Start hello VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```


## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="ef45d-149">Criar várias NICs usando modelos do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ef45d-149">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="ef45d-150">Modelos do Gerenciador de recursos do Azure usam toodefine declarativa de arquivos JSON seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="ef45d-150">Azure Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="ef45d-151">Você pode ler uma [visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ef45d-151">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="ef45d-152">Modelos do Gerenciador de recursos fornecem uma maneira toocreate várias instâncias de um recurso durante a implantação, como a criação de várias NICs.</span><span class="sxs-lookup"><span data-stu-id="ef45d-152">Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="ef45d-153">Você usa *cópia* toospecify número de saudação do toocreate de instâncias:</span><span class="sxs-lookup"><span data-stu-id="ef45d-153">You use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="ef45d-154">Leia mais sobre a [criação de várias instâncias usando *copiar*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="ef45d-154">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="ef45d-155">Você também pode usar um `copyIndex()` toothen acrescentar um nome de recurso de tooa número, o que permite que você toocreate `myNic1`, `myNic2`, a seguir Olá etc. mostra um exemplo de acrescentar o valor de índice de saudação:</span><span class="sxs-lookup"><span data-stu-id="ef45d-155">You can also use a `copyIndex()` toothen append a number tooa resource name, which allows you toocreate `myNic1`, `myNic2`, etc. hello following shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="ef45d-156">Você pode ler um exemplo completo em [Criando várias NICs usando modelos do Gerenciador de Recursos](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="ef45d-156">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef45d-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ef45d-157">Next steps</span></span>
<span data-ttu-id="ef45d-158">Revisão [tamanhos de VM do Linux](sizes.md) durante a tentativa de toocreating uma VM com várias NICs.</span><span class="sxs-lookup"><span data-stu-id="ef45d-158">Review [Linux VM sizes](sizes.md) when trying toocreating a VM with multiple NICs.</span></span> <span data-ttu-id="ef45d-159">Preste atenção toohello número de NICs dá suporte a cada tamanho VM.</span><span class="sxs-lookup"><span data-stu-id="ef45d-159">Pay attention toohello maximum number of NICs each VM size supports.</span></span> 
