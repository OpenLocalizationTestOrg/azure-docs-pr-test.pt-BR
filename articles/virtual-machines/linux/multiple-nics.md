---
title: "Criar uma VM do Linux no Azure com várias NICs | Microsoft Docs"
description: "Saiba como criar uma VM Linux com várias NICs anexadas a ela usando a CLI 2.0 do Azure ou modelos do Resource Manager."
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
ms.openlocfilehash: 8a2931e462079c101c91497d459d7d3126234244
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a><span data-ttu-id="5380e-103">Como criar uma máquina virtual Linux no Azure com várias placas de adaptador de rede</span><span class="sxs-lookup"><span data-stu-id="5380e-103">How to create a Linux virtual machine in Azure with multiple network interface cards</span></span>
<span data-ttu-id="5380e-104">Você pode criar uma VM (máquina virtual) no Azure que tenha várias NICs (interfaces de rede virtual) anexadas a ela.</span><span class="sxs-lookup"><span data-stu-id="5380e-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached to it.</span></span> <span data-ttu-id="5380e-105">Um cenário comum é ter sub-redes diferentes para conectividade de front-end e de back-end ou uma rede dedicada a uma solução de monitoramento ou de backup.</span><span class="sxs-lookup"><span data-stu-id="5380e-105">A common scenario is to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution.</span></span> <span data-ttu-id="5380e-106">Este artigo fornece detalhes sobre como criar uma VM com várias NICs anexadas a ela e como adicionar ou remover NICs de uma VM existente.</span><span class="sxs-lookup"><span data-stu-id="5380e-106">This article details how to create a VM with multiple NICs attached to it and how to add or remove NICs from an existing VM.</span></span> <span data-ttu-id="5380e-107">Para obter informações detalhadas, incluindo como criar várias NICs dentro de seus próprios scripts Bash, leia mais sobre a [implantação de VMs com várias NICs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5380e-107">For detailed information, including how to create multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="5380e-108">Diferentes [tamanhos de VM](sizes.md) dão suporte a um número variável de NICs, sendo assim, dimensione sua VM adequadamente.</span><span class="sxs-lookup"><span data-stu-id="5380e-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="5380e-109">Este artigo fornece detalhes sobre como criar uma VM com várias NICs com a CLI 2.0 do Azure.</span><span class="sxs-lookup"><span data-stu-id="5380e-109">This article details how to create a VM with multiple NICs with the Azure CLI 2.0.</span></span> <span data-ttu-id="5380e-110">Você também pode executar essas etapas com a [CLI do Azure 1.0](multiple-nics-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="5380e-110">You can also perform these steps with the [Azure CLI 1.0](multiple-nics-nodejs.md).</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="5380e-111">Criar recursos de suporte</span><span class="sxs-lookup"><span data-stu-id="5380e-111">Create supporting resources</span></span>
<span data-ttu-id="5380e-112">Instale a [CLI 2.0 do Azure](/cli/azure/install-az-cli2) mais recente e faça logon em uma conta do Azure usando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="5380e-112">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="5380e-113">Nos exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="5380e-113">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="5380e-114">Os nomes de parâmetro de exemplo incluem *myResourceGroup*, *mystorageaccount* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="5380e-114">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="5380e-115">Primeiro, crie um grupo de recursos com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="5380e-115">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="5380e-116">O exemplo a seguir cria um grupo de recursos chamado *myResourceGroup* na localização *eastus*:</span><span class="sxs-lookup"><span data-stu-id="5380e-116">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="5380e-117">Crie a rede virtual com [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="5380e-117">Create the virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="5380e-118">O exemplo a seguir cria uma rede virtual chamada *myVnet* e uma sub-rede chamada *mySubnetFrontEnd*:</span><span class="sxs-lookup"><span data-stu-id="5380e-118">The following example creates a virtual network named *myVnet* and subnet named *mySubnetFrontEnd*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="5380e-119">Crie uma sub-rede para o tráfego de back-end com [az network vnet subnet create](/cli/azure/network/vnet/subnet#create).</span><span class="sxs-lookup"><span data-stu-id="5380e-119">Create a subnet for the back-end traffic with [az network vnet subnet create](/cli/azure/network/vnet/subnet#create).</span></span> <span data-ttu-id="5380e-120">O exemplo a seguir cria uma sub-rede chamada *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="5380e-120">The following example creates a subnet named *mySubnetBackEnd*:</span></span>

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

<span data-ttu-id="5380e-121">Crie um grupo de segurança de rede com [az network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="5380e-121">Create a network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="5380e-122">O exemplo a seguir cria um grupo de segurança de rede denominado *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="5380e-122">The following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="5380e-123">Criar e configurar várias NICs</span><span class="sxs-lookup"><span data-stu-id="5380e-123">Create and configure multiple NICs</span></span>
<span data-ttu-id="5380e-124">Crie duas NICs com [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="5380e-124">Create two NICs with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="5380e-125">O exemplo a seguir cria duas NICs, chamadas *myNic1* e *myNic2*, conectadas ao Grupo de Segurança de Rede, com uma NIC se conectando a cada sub-rede:</span><span class="sxs-lookup"><span data-stu-id="5380e-125">The following example creates two NICs, named *myNic1* and *myNic2*, connected the network security group, with one NIC connecting to each subnet:</span></span>

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

## <a name="create-a-vm-and-attach-the-nics"></a><span data-ttu-id="5380e-126">Criar uma VM e conectar as NICs</span><span class="sxs-lookup"><span data-stu-id="5380e-126">Create a VM and attach the NICs</span></span>
<span data-ttu-id="5380e-127">Quando você criar a VM, especifica as NICs que criou com `--nics`.</span><span class="sxs-lookup"><span data-stu-id="5380e-127">When you create the VM, specify the NICs you created with `--nics`.</span></span> <span data-ttu-id="5380e-128">Você também precisa tomar cuidado ao selecionar o tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="5380e-128">You also need to take care when you select the VM size.</span></span> <span data-ttu-id="5380e-129">Há limites para o número total de NICs que podem ser adicionados a uma VM.</span><span class="sxs-lookup"><span data-stu-id="5380e-129">There are limits for the total number of NICs that you can add to a VM.</span></span> <span data-ttu-id="5380e-130">Leia mais sobre [Tamanhos de VM Linux](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="5380e-130">Read more about [Linux VM sizes](sizes.md).</span></span> 

<span data-ttu-id="5380e-131">Crie uma VM com [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="5380e-131">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="5380e-132">O exemplo a seguir cria uma VM chamada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="5380e-132">The following example creates a VM named *myVM*:</span></span>

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

## <a name="add-a-nic-to-a-vm"></a><span data-ttu-id="5380e-133">Adicionar uma NIC a uma VM</span><span class="sxs-lookup"><span data-stu-id="5380e-133">Add a NIC to a VM</span></span>
<span data-ttu-id="5380e-134">As etapas anteriores criaram uma VM com várias NICs.</span><span class="sxs-lookup"><span data-stu-id="5380e-134">The previous steps created a VM with multiple NICs.</span></span> <span data-ttu-id="5380e-135">Você também pode adicionar NICs a uma VM existente com a CLI do Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="5380e-135">You can also add NICs to an existing VM with the Azure CLI 2.0.</span></span> 

<span data-ttu-id="5380e-136">Crie outra NIC com [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="5380e-136">Create another NIC with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="5380e-137">O exemplo a seguir cria uma NIC chamada *myNic3* conectada à sub-rede de back-end e ao Grupo de Segurança de Rede criado nas etapas anteriores:</span><span class="sxs-lookup"><span data-stu-id="5380e-137">The following example creates a NIC named *myNic3* connected to the back-end subnet and network security group created in the previous steps:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="5380e-138">Para adicionar uma NIC a uma VM existente, primeiro desaloque a VM com [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="5380e-138">To add a NIC to an existing VM, first deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="5380e-139">O exemplo a seguir desaloca a VM chamada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="5380e-139">The following example deallocates the VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="5380e-140">Adicione a NIC com [az vm nic add](/cli/azure/vm/nic#add).</span><span class="sxs-lookup"><span data-stu-id="5380e-140">Add the NIC with [az vm nic add](/cli/azure/vm/nic#add).</span></span> <span data-ttu-id="5380e-141">O exemplo a seguir adiciona *myNic3* à *myVM*:</span><span class="sxs-lookup"><span data-stu-id="5380e-141">The following example adds *myNic3* to *myVM*:</span></span>

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

<span data-ttu-id="5380e-142">Inicie a VM com [az vm start](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="5380e-142">Start the VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

## <a name="remove-a-nic-from-a-vm"></a><span data-ttu-id="5380e-143">Remover uma NIC de uma VM</span><span class="sxs-lookup"><span data-stu-id="5380e-143">Remove a NIC from a VM</span></span>
<span data-ttu-id="5380e-144">Para remover uma NIC de uma VM existente, primeiro desaloque a VM com [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="5380e-144">To remove a NIC from an existing VM, first deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="5380e-145">O exemplo a seguir desaloca a VM chamada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="5380e-145">The following example deallocates the VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="5380e-146">Remova a NIC com [az vm nic remove](/cli/azure/vm/nic#remove).</span><span class="sxs-lookup"><span data-stu-id="5380e-146">Remove the NIC with [az vm nic remove](/cli/azure/vm/nic#remove).</span></span> <span data-ttu-id="5380e-147">O exemplo a seguir remove *myNic3* de *myVM*:</span><span class="sxs-lookup"><span data-stu-id="5380e-147">The following example removes *myNic3* from *myVM*:</span></span>

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM 
    --nics myNic3
```

<span data-ttu-id="5380e-148">Inicie a VM com [az vm start](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="5380e-148">Start the VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```


## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="5380e-149">Criar várias NICs usando modelos do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5380e-149">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="5380e-150">Os modelos do Azure Resource Manager usam arquivos JSON declarativos para definir o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="5380e-150">Azure Resource Manager templates use declarative JSON files to define your environment.</span></span> <span data-ttu-id="5380e-151">Você pode ler uma [visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5380e-151">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="5380e-152">Os modelos do Gerenciador de Recursos oferecem uma maneira de criar várias instâncias de um recurso durante a implantação, como a criação de várias NICs.</span><span class="sxs-lookup"><span data-stu-id="5380e-152">Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="5380e-153">Você usa *copiar* para especificar o número de instâncias a serem criadas:</span><span class="sxs-lookup"><span data-stu-id="5380e-153">You use *copy* to specify the number of instances to create:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="5380e-154">Leia mais sobre a [criação de várias instâncias usando *copiar*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="5380e-154">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="5380e-155">Você também pode usar um `copyIndex()` para acrescentar um número a um nome de recurso, o que lhe permite criar `myNic1`, `myNic2` etc. Veja a seguir um exemplo de como acrescentar o valor de índice:</span><span class="sxs-lookup"><span data-stu-id="5380e-155">You can also use a `copyIndex()` to then append a number to a resource name, which allows you to create `myNic1`, `myNic2`, etc. The following shows an example of appending the index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="5380e-156">Você pode ler um exemplo completo em [Criando várias NICs usando modelos do Gerenciador de Recursos](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="5380e-156">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5380e-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5380e-157">Next steps</span></span>
<span data-ttu-id="5380e-158">Examine [Tamanhos de VM Linux](sizes.md) ao tentar criar uma VM com várias NICs.</span><span class="sxs-lookup"><span data-stu-id="5380e-158">Review [Linux VM sizes](sizes.md) when trying to creating a VM with multiple NICs.</span></span> <span data-ttu-id="5380e-159">Preste atenção ao número máximo de NICs a que cada VM dá suporte.</span><span class="sxs-lookup"><span data-stu-id="5380e-159">Pay attention to the maximum number of NICs each VM size supports.</span></span> 