---
title: Copiar uma VM do Linux usando a CLI do Azure 2.0 | Microsoft Docs
description: "Saiba como criar uma cópia da sua VM Linux do Azure usando a CLI do Azure 2.0 e Managed Disks."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 03/10/2017
ms.author: cynthn
ms.openlocfilehash: 7983061a933370803669480296d7625106e1360c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-copy-of-a-linux-vm-by-using-azure-cli-20-and-managed-disks"></a><span data-ttu-id="7c1c2-103">Criar uma cópia da sua VM Linux usando a CLI do Azure 2.0 e Managed Disks</span><span class="sxs-lookup"><span data-stu-id="7c1c2-103">Create a copy of a Linux VM by using Azure CLI 2.0 and Managed Disks</span></span>


<span data-ttu-id="7c1c2-104">Este artigo mostra como criar uma cópia de sua VM (máquina virtual) do Azure executando o Linux usando a CLI do Azure 2.0 e o modelo de implantação do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7c1c2-104">This article shows you how to create a copy of your Azure virtual machine (VM) running Linux using the Azure CLI 2.0 and the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="7c1c2-105">Você também pode executar essas etapas com a [CLI do Azure 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7c1c2-105">You can also perform these steps with the [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="7c1c2-106">Você também pode [carregar e criar uma VM com base em um VHD](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7c1c2-106">You can also [upload and create a VM from a VHD](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c1c2-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7c1c2-107">Prerequisites</span></span>


-   <span data-ttu-id="7c1c2-108">Instalar a [CLI do Azure 2.0](/cli/azure/install-az-cli2)</span><span class="sxs-lookup"><span data-stu-id="7c1c2-108">Install [Azure CLI 2.0](/cli/azure/install-az-cli2)</span></span>

-   <span data-ttu-id="7c1c2-109">Entre em uma conta do Azure com [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="7c1c2-109">Sign in to an Azure account with [az login](/cli/azure/#login).</span></span>

-   <span data-ttu-id="7c1c2-110">Tenha uma VM do Azure para usar como origem para a cópia.</span><span class="sxs-lookup"><span data-stu-id="7c1c2-110">Have an Azure VM to use as the source for your copy.</span></span>

## <a name="step-1-stop-the-source-vm"></a><span data-ttu-id="7c1c2-111">Etapa 1: interromper a VM de origem</span><span class="sxs-lookup"><span data-stu-id="7c1c2-111">Step 1: Stop the source VM</span></span>


<span data-ttu-id="7c1c2-112">Desaloque a VM de origem usando [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="7c1c2-112">Deallocate the source VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span>
<span data-ttu-id="7c1c2-113">O seguinte exemplo desaloca a VM **myVM** no grupo de recursos chamado **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="7c1c2-113">The following example deallocates the VM named **myVM** in the resource group **myResourceGroup**:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

## <a name="step-2-copy-the-source-vm"></a><span data-ttu-id="7c1c2-114">Etapa 2: copiar a VM de origem</span><span class="sxs-lookup"><span data-stu-id="7c1c2-114">Step 2: Copy the source VM</span></span>


<span data-ttu-id="7c1c2-115">Para copiar uma máquina virtual, você deve criar uma cópia do disco rígido virtual subjacente.</span><span class="sxs-lookup"><span data-stu-id="7c1c2-115">To copy a VM, you create a copy of the underlying virtual hard disk.</span></span> <span data-ttu-id="7c1c2-116">Por meio desse processo, você cria uma VHD especializada que contém a mesma configuração e definições que a VM de origem.</span><span class="sxs-lookup"><span data-stu-id="7c1c2-116">This process creates a specialized VHD as a Managed Disk that contains the same configuration and settings as the source VM.</span></span>

<span data-ttu-id="7c1c2-117">Para saber mais sobre Azure Managed Disks, veja [Visão geral dos Azure Managed Disks](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7c1c2-117">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span> 

1.  <span data-ttu-id="7c1c2-118">Lista cada VM e o nome do disco do sistema operacional com [az vm list](/cli/azure/vm#list).</span><span class="sxs-lookup"><span data-stu-id="7c1c2-118">List each VM and the name of its OS disk with [az vm list](/cli/azure/vm#list).</span></span> <span data-ttu-id="7c1c2-119">O exemplo a seguir lista todas as VMs no grupo de recursos denominado **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="7c1c2-119">The following example lists all VMs in the resource group named **myResourceGroup**:</span></span>
    
    ```azurecli
    az vm list -g myTestRG --query '[].{Name:name,DiskName:storageProfile.osDisk.name}' --output table
    ```

    <span data-ttu-id="7c1c2-120">A saída deverá ser semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="7c1c2-120">The output is similar to the following example:</span></span>

    ```azurecli
    Name    DiskName
    ------  --------
    myVM    myDisk
    ```

1.  <span data-ttu-id="7c1c2-121">Copie o disco, criando um novo disco gerenciado usando [az disk create](/cli/azure/disk#create).</span><span class="sxs-lookup"><span data-stu-id="7c1c2-121">Copy the disk by creating a new managed disk using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="7c1c2-122">O exemplo a seguir cria um disco chamado **myCopiedDisk** do disco gerenciado chamado **myDisk**:</span><span class="sxs-lookup"><span data-stu-id="7c1c2-122">The following example creates a disk named **myCopiedDisk** from the managed disk named **myDisk**:</span></span>

    ```azurecli
    az disk create --resource-group myResourceGroup --name myCopiedDisk --source myDisk
    ``` 

1.  <span data-ttu-id="7c1c2-123">Verifique se os discos gerenciados agora em seu grupo de recursos usando [az disk list](/cli/azure/disk#list).</span><span class="sxs-lookup"><span data-stu-id="7c1c2-123">Verify the managed disks now in your resource group by using [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="7c1c2-124">O exemplo a seguir lista os discos gerenciados no grupo de recursos denominado **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="7c1c2-124">The following example lists the managed disks in the resource group named **myResourceGroup**:</span></span>

    ```azurecli
    az disk list --resource-group myResourceGroup --output table
    ```

1.  <span data-ttu-id="7c1c2-125">Vá para a ["Etapa 3: configurar uma rede virtual"](#step-3-set-up-a-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="7c1c2-125">Skip to ["Step 3: Set up a virtual network"](#step-3-set-up-a-virtual-network).</span></span>


## <a name="step-3-set-up-a-virtual-network"></a><span data-ttu-id="7c1c2-126">Etapa 3: configurar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="7c1c2-126">Step 3: Set up a virtual network</span></span>


<span data-ttu-id="7c1c2-127">As etapas opcionais a seguir criam uma nova rede virtual, uma sub-rede, um endereço IP público e uma placa de adaptador de rede virtual (NIC).</span><span class="sxs-lookup"><span data-stu-id="7c1c2-127">The following optional steps create a new virtual network, subnet, public IP address, and virtual network interface card (NIC).</span></span>

<span data-ttu-id="7c1c2-128">Se você estiver copiando uma VM para fins ou implantações adicionais de solução de problemas, não convém usar uma máquina virtual em uma rede virtual existente.</span><span class="sxs-lookup"><span data-stu-id="7c1c2-128">If you are copying a VM for troubleshooting purposes or additional deployments, you might not want to use a VM in an existing virtual network.</span></span>

<span data-ttu-id="7c1c2-129">Se quiser criar uma infraestrutura de rede virtual para as VMs copiadas, siga as próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="7c1c2-129">If you want to create a virtual network infrastructure for your copied VMs, follow the next few steps.</span></span> <span data-ttu-id="7c1c2-130">Se não quiser criar uma rede virtual, vá para a [Etapa 4: criar uma VM](#step-4-create-a-vm).</span><span class="sxs-lookup"><span data-stu-id="7c1c2-130">If you don't want to create a virtual network, skip to [Step 4: Create a VM](#step-4-create-a-vm).</span></span>

1.  <span data-ttu-id="7c1c2-131">Crie a rede virtual usando [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="7c1c2-131">Create the virtual network by using [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="7c1c2-132">O exemplo a seguir cria uma rede virtual chamada **myVnet** e uma sub-rede chamada **mySubnet**:</span><span class="sxs-lookup"><span data-stu-id="7c1c2-132">The following example creates a virtual network named **myVnet** and a subnet named **mySubnet**:</span></span>

    ```azurecli
    az network vnet create --resource-group myResourceGroup --location westus --name myVnet \
        --address-prefix 192.168.0.0/16 --subnet-name mySubnet --subnet-prefix 192.168.1.0/24
    ```

1.  <span data-ttu-id="7c1c2-133">Crie um IP público usando [az network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="7c1c2-133">Create a public IP by using [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="7c1c2-134">O exemplo a seguir cria um IP público chamado **myPublicIP** com o nome DNS de **mypublicdns**.</span><span class="sxs-lookup"><span data-stu-id="7c1c2-134">The following example creates a public IP named **myPublicIP** with the DNS name of **mypublicdns**.</span></span> <span data-ttu-id="7c1c2-135">(O nome DNS deve ser exclusivo; portanto, forneça um nome exclusivo.)</span><span class="sxs-lookup"><span data-stu-id="7c1c2-135">(The DNS name must be unique, so provide a unique name.)</span></span>

    ```azurecli
    az network public-ip create --resource-group myResourceGroup --location westus \
        --name myPublicIP --dns-name mypublicdns --allocation-method static --idle-timeout 4
    ```

1.  <span data-ttu-id="7c1c2-136">Crie a NIC usando [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="7c1c2-136">Create the NIC using [az network nic create](/cli/azure/network/nic#create).</span></span>
    <span data-ttu-id="7c1c2-137">O exemplo a seguir cria uma NIC chamada **myNic** anexada à sub-rede **mySubnet**:</span><span class="sxs-lookup"><span data-stu-id="7c1c2-137">The following example creates a NIC named **myNic** that's attached to the **mySubnet** subnet:</span></span>

    ```azurecli
    az network nic create --resource-group myResourceGroup --location westus --name myNic \
        --vnet-name myVnet --subnet mySubnet --public-ip-address myPublicIP
    ```

## <a name="step-4-create-a-vm"></a><span data-ttu-id="7c1c2-138">Etapa 4: criar uma VM</span><span class="sxs-lookup"><span data-stu-id="7c1c2-138">Step 4: Create a VM</span></span>

<span data-ttu-id="7c1c2-139">Não é possível criar uma VM usando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="7c1c2-139">You can now create a VM by using [az vm create](/cli/azure/vm#create).</span></span>

<span data-ttu-id="7c1c2-140">Especifique o disco copiado gerenciado para usar como o disco do sistema operacional (--attach-os-disk) da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="7c1c2-140">Specify the copied managed disk to use as the OS disk (--attach-os-disk), as follows:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --name myCopiedVM \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics myNic --size Standard_DS1_v2 --os-type Linux \
    --attach-os-disk myCopiedDisk
```

## <a name="next-steps"></a><span data-ttu-id="7c1c2-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7c1c2-141">Next steps</span></span>

<span data-ttu-id="7c1c2-142">Para saber como usar a CLI do Azure para gerenciar sua nova VM, confira [Comandos da CLI do Azure para o Azure Resource Manager](../azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="7c1c2-142">To learn how to use Azure CLI to manage your new VM, see [Azure CLI commands for the Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>
