---
title: aaaCopy uma VM do Linux usando o Azure CLI 2.0 | Microsoft Docs
description: "Saiba como toocreate uma cópia da VM Azure Linux usando o Azure CLI 2.0 e discos gerenciados."
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
ms.openlocfilehash: ee34a4259dd0c1e7bf49312fe3fe3ba809bf69e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-vm-by-using-azure-cli-20-and-managed-disks"></a><span data-ttu-id="89ddb-103">Criar uma cópia da sua VM Linux usando a CLI do Azure 2.0 e Managed Disks</span><span class="sxs-lookup"><span data-stu-id="89ddb-103">Create a copy of a Linux VM by using Azure CLI 2.0 and Managed Disks</span></span>


<span data-ttu-id="89ddb-104">Este artigo mostra como toocreate uma cópia de sua máquina virtual do Azure (VM) executando o Linux usando Olá 2.0 do CLI do Azure e o modelo de implantação do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="89ddb-104">This article shows you how toocreate a copy of your Azure virtual machine (VM) running Linux using hello Azure CLI 2.0 and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="89ddb-105">Você também pode executar essas etapas com hello [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="89ddb-105">You can also perform these steps with hello [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="89ddb-106">Você também pode [carregar e criar uma VM com base em um VHD](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="89ddb-106">You can also [upload and create a VM from a VHD](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89ddb-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="89ddb-107">Prerequisites</span></span>


-   <span data-ttu-id="89ddb-108">Instalar a [CLI do Azure 2.0](/cli/azure/install-az-cli2)</span><span class="sxs-lookup"><span data-stu-id="89ddb-108">Install [Azure CLI 2.0](/cli/azure/install-az-cli2)</span></span>

-   <span data-ttu-id="89ddb-109">Entrar tooan conta do Azure com [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="89ddb-109">Sign in tooan Azure account with [az login](/cli/azure/#login).</span></span>

-   <span data-ttu-id="89ddb-110">Têm um toouse de VM do Azure como origem de saudação de sua cópia.</span><span class="sxs-lookup"><span data-stu-id="89ddb-110">Have an Azure VM toouse as hello source for your copy.</span></span>

## <a name="step-1-stop-hello-source-vm"></a><span data-ttu-id="89ddb-111">Etapa 1: Interromper a VM de origem Olá</span><span class="sxs-lookup"><span data-stu-id="89ddb-111">Step 1: Stop hello source VM</span></span>


<span data-ttu-id="89ddb-112">Desalocar a VM de origem hello usando [az vm desalocar](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="89ddb-112">Deallocate hello source VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span>
<span data-ttu-id="89ddb-113">exemplo a seguir Hello desaloca Olá VM denominada **myVM** no grupo de recursos de saudação **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="89ddb-113">hello following example deallocates hello VM named **myVM** in hello resource group **myResourceGroup**:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

## <a name="step-2-copy-hello-source-vm"></a><span data-ttu-id="89ddb-114">Etapa 2: Copiar a VM de origem Olá</span><span class="sxs-lookup"><span data-stu-id="89ddb-114">Step 2: Copy hello source VM</span></span>


<span data-ttu-id="89ddb-115">toocopy uma VM, criar uma cópia da saudação subjacente do disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="89ddb-115">toocopy a VM, you create a copy of hello underlying virtual hard disk.</span></span> <span data-ttu-id="89ddb-116">Esse processo cria um VHD especializado como um disco gerenciado que contém Olá mesma configuração e definições como Olá VM de origem.</span><span class="sxs-lookup"><span data-stu-id="89ddb-116">This process creates a specialized VHD as a Managed Disk that contains hello same configuration and settings as hello source VM.</span></span>

<span data-ttu-id="89ddb-117">Para saber mais sobre Azure Managed Disks, veja [Visão geral dos Azure Managed Disks](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="89ddb-117">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span> 

1.  <span data-ttu-id="89ddb-118">Lista cada VM e Olá o nome do seu disco do sistema operacional com [lista de vm az](/cli/azure/vm#list).</span><span class="sxs-lookup"><span data-stu-id="89ddb-118">List each VM and hello name of its OS disk with [az vm list](/cli/azure/vm#list).</span></span> <span data-ttu-id="89ddb-119">Olá, exemplo a seguir lista todas as VMs no grupo de recursos denominado **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="89ddb-119">hello following example lists all VMs in the resource group named **myResourceGroup**:</span></span>
    
    ```azurecli
    az vm list -g myTestRG --query '[].{Name:name,DiskName:storageProfile.osDisk.name}' --output table
    ```

    <span data-ttu-id="89ddb-120">saudação de saída é similar toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="89ddb-120">hello output is similar toohello following example:</span></span>

    ```azurecli
    Name    DiskName
    ------  --------
    myVM    myDisk
    ```

1.  <span data-ttu-id="89ddb-121">Copiar o disco de hello, criando um novo gerenciados usando o disco [criar disco az](/cli/azure/disk#create).</span><span class="sxs-lookup"><span data-stu-id="89ddb-121">Copy hello disk by creating a new managed disk using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="89ddb-122">Olá, exemplo a seguir cria um disco chamado **myCopiedDisk** de saudação gerenciados disco chamado **myDisk**:</span><span class="sxs-lookup"><span data-stu-id="89ddb-122">hello following example creates a disk named **myCopiedDisk** from hello managed disk named **myDisk**:</span></span>

    ```azurecli
    az disk create --resource-group myResourceGroup --name myCopiedDisk --source myDisk
    ``` 

1.  <span data-ttu-id="89ddb-123">Verificar discos Olá gerenciado em seu grupo de recursos usando [lista de discos az](/cli/azure/disk#list).</span><span class="sxs-lookup"><span data-stu-id="89ddb-123">Verify hello managed disks now in your resource group by using [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="89ddb-124">Olá, exemplo a seguir lista discos Olá gerenciado no grupo de recursos de saudação denominado **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="89ddb-124">hello following example lists hello managed disks in hello resource group named **myResourceGroup**:</span></span>

    ```azurecli
    az disk list --resource-group myResourceGroup --output table
    ```

1.  <span data-ttu-id="89ddb-125">Ignorar muito["etapa 3: configurar uma rede virtual"](#step-3-set-up-a-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="89ddb-125">Skip too["Step 3: Set up a virtual network"](#step-3-set-up-a-virtual-network).</span></span>


## <a name="step-3-set-up-a-virtual-network"></a><span data-ttu-id="89ddb-126">Etapa 3: configurar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="89ddb-126">Step 3: Set up a virtual network</span></span>


<span data-ttu-id="89ddb-127">Olá opcionais etapas a seguir criam uma nova rede virtual, a sub-rede, o endereço IP público e a placa de interface de rede virtual (NIC).</span><span class="sxs-lookup"><span data-stu-id="89ddb-127">hello following optional steps create a new virtual network, subnet, public IP address, and virtual network interface card (NIC).</span></span>

<span data-ttu-id="89ddb-128">Se você estiver copiando uma VM para fins ou implantações adicionais de solução de problemas, convém não toouse uma VM em uma rede virtual existente.</span><span class="sxs-lookup"><span data-stu-id="89ddb-128">If you are copying a VM for troubleshooting purposes or additional deployments, you might not want toouse a VM in an existing virtual network.</span></span>

<span data-ttu-id="89ddb-129">Se você quiser toocreate uma infraestrutura de rede virtual para suas VMs copiados, siga lado Olá algumas etapas.</span><span class="sxs-lookup"><span data-stu-id="89ddb-129">If you want toocreate a virtual network infrastructure for your copied VMs, follow hello next few steps.</span></span> <span data-ttu-id="89ddb-130">Se você não quiser toocreate uma rede virtual, ignore muito[etapa 4: criar uma VM](#step-4-create-a-vm).</span><span class="sxs-lookup"><span data-stu-id="89ddb-130">If you don't want toocreate a virtual network, skip too[Step 4: Create a VM](#step-4-create-a-vm).</span></span>

1.  <span data-ttu-id="89ddb-131">Criar rede virtual hello usando [criar redes de rede az](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="89ddb-131">Create hello virtual network by using [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="89ddb-132">Olá, exemplo a seguir cria uma rede virtual denominada **myVnet** e uma sub-rede denominada **mySubnet**:</span><span class="sxs-lookup"><span data-stu-id="89ddb-132">hello following example creates a virtual network named **myVnet** and a subnet named **mySubnet**:</span></span>

    ```azurecli
    az network vnet create --resource-group myResourceGroup --location westus --name myVnet \
        --address-prefix 192.168.0.0/16 --subnet-name mySubnet --subnet-prefix 192.168.1.0/24
    ```

1.  <span data-ttu-id="89ddb-133">Crie um IP público usando [az network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="89ddb-133">Create a public IP by using [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="89ddb-134">Olá, exemplo a seguir cria um IP público denominado **myPublicIP** com nome DNS de saudação do **mypublicdns**.</span><span class="sxs-lookup"><span data-stu-id="89ddb-134">hello following example creates a public IP named **myPublicIP** with hello DNS name of **mypublicdns**.</span></span> <span data-ttu-id="89ddb-135">(o nome DNS Olá deve ser exclusivo, portanto, forneça um nome exclusivo.)</span><span class="sxs-lookup"><span data-stu-id="89ddb-135">(hello DNS name must be unique, so provide a unique name.)</span></span>

    ```azurecli
    az network public-ip create --resource-group myResourceGroup --location westus \
        --name myPublicIP --dns-name mypublicdns --allocation-method static --idle-timeout 4
    ```

1.  <span data-ttu-id="89ddb-136">Criar hello NIC usando [nic da rede az criar](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="89ddb-136">Create hello NIC using [az network nic create](/cli/azure/network/nic#create).</span></span>
    <span data-ttu-id="89ddb-137">Olá, exemplo a seguir cria uma NIC denominada **myNic** toothe anexado que **mySubnet** sub-rede:</span><span class="sxs-lookup"><span data-stu-id="89ddb-137">hello following example creates a NIC named **myNic** that's attached toothe **mySubnet** subnet:</span></span>

    ```azurecli
    az network nic create --resource-group myResourceGroup --location westus --name myNic \
        --vnet-name myVnet --subnet mySubnet --public-ip-address myPublicIP
    ```

## <a name="step-4-create-a-vm"></a><span data-ttu-id="89ddb-138">Etapa 4: criar uma VM</span><span class="sxs-lookup"><span data-stu-id="89ddb-138">Step 4: Create a VM</span></span>

<span data-ttu-id="89ddb-139">Não é possível criar uma VM usando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="89ddb-139">You can now create a VM by using [az vm create](/cli/azure/vm#create).</span></span>

<span data-ttu-id="89ddb-140">Especificar Olá copiado toouse de disco gerenciado como disco de SO de saudação (– anexar-disco do SO), da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="89ddb-140">Specify hello copied managed disk toouse as hello OS disk (--attach-os-disk), as follows:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --name myCopiedVM \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics myNic --size Standard_DS1_v2 --os-type Linux \
    --attach-os-disk myCopiedDisk
```

## <a name="next-steps"></a><span data-ttu-id="89ddb-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="89ddb-141">Next steps</span></span>

<span data-ttu-id="89ddb-142">toolearn como toouse CLI do Azure toomanage sua nova VM, consulte [comandos de CLI do Azure para hello Azure Resource Manager](../azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="89ddb-142">toolearn how toouse Azure CLI toomanage your new VM, see [Azure CLI commands for hello Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>
