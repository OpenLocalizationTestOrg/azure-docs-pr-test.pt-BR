---
title: Criar imagens personalizadas da VM com a CLI do Azure | Microsoft Docs
description: Tutorial - Criar uma imagem personalizada da VM usando a CLI do Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/21/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: d32980f05ad17a76793021d0a5355d597974a4e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-the-cli"></a><span data-ttu-id="65271-103">Criar uma imagem personalizada de uma VM do Azure usando a CLI</span><span class="sxs-lookup"><span data-stu-id="65271-103">Create a custom image of an Azure VM using the CLI</span></span>

<span data-ttu-id="65271-104">Imagens personalizadas são como imagens do marketplace, mas você mesmo as cria.</span><span class="sxs-lookup"><span data-stu-id="65271-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="65271-105">As imagens personalizadas podem ser usadas para configurações de inicialização como o pré-carregamento de aplicativos, configurações de aplicativos e outras configurações do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="65271-105">Custom images can be used to bootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="65271-106">Neste tutorial, você criará sua própria imagem personalizada de uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="65271-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="65271-107">Você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="65271-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="65271-108">Desprovisionar e generalizar VMs</span><span class="sxs-lookup"><span data-stu-id="65271-108">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="65271-109">Criar uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="65271-109">Create a custom image</span></span>
> * <span data-ttu-id="65271-110">Criar uma VM por meio de uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="65271-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="65271-111">Listar todas as imagens na sua assinatura</span><span class="sxs-lookup"><span data-stu-id="65271-111">List all the images in your subscription</span></span>
> * <span data-ttu-id="65271-112">Excluir uma imagem</span><span class="sxs-lookup"><span data-stu-id="65271-112">Delete an image</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="65271-113">Se você optar por instalar e usar a CLI localmente, este tutorial exigirá que você execute a CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="65271-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="65271-114">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="65271-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="65271-115">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="65271-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="65271-116">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="65271-116">Before you begin</span></span>

<span data-ttu-id="65271-117">As etapas abaixo detalham como pegar uma máquina virtual existente e transformá-la em uma imagem personalizada reutilizável que você pode usar para criar novas instâncias de VM.</span><span class="sxs-lookup"><span data-stu-id="65271-117">The steps below detail how to take an existing VM and turn it into a re-usable custom image that you can use to create new VM instances.</span></span>

<span data-ttu-id="65271-118">Para concluir o exemplo neste tutorial, você deverá ter uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="65271-118">To complete the example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="65271-119">Se necessário, este [exemplo de script](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) pode criar uma para você.</span><span class="sxs-lookup"><span data-stu-id="65271-119">If needed, this [script sample](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) can create one for you.</span></span> <span data-ttu-id="65271-120">Ao trabalhar com este tutorial, substitua o grupo de recursos e os nomes de VM onde for necessário.</span><span class="sxs-lookup"><span data-stu-id="65271-120">When working through the tutorial, replace the resource group and VM names where needed.</span></span>

## <a name="create-a-custom-image"></a><span data-ttu-id="65271-121">Criar uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="65271-121">Create a custom image</span></span>

<span data-ttu-id="65271-122">Para criar uma imagem de uma máquina virtual, você precisará preparar a VM desprovisionando, desalocando e, em seguida, marcando a VM de origem como generalizada.</span><span class="sxs-lookup"><span data-stu-id="65271-122">To create an image of a virtual machine, you need to prepare the VM by deprovisioning, deallocating, and then marking the source VM as generalized.</span></span> <span data-ttu-id="65271-123">Depois que a VM tiver sido preparada, você poderá criar uma imagem.</span><span class="sxs-lookup"><span data-stu-id="65271-123">Once the VM has been prepared, you can create an image.</span></span>

### <a name="deprovision-the-vm"></a><span data-ttu-id="65271-124">Desprovisionar a VM</span><span class="sxs-lookup"><span data-stu-id="65271-124">Deprovision the VM</span></span> 

<span data-ttu-id="65271-125">Desprovisionar generaliza a VM removendo informações específicas da máquina.</span><span class="sxs-lookup"><span data-stu-id="65271-125">Deprovisioning generalizes the VM by removing machine-specific information.</span></span> <span data-ttu-id="65271-126">Essa generalização permite implantar várias VMs de uma única imagem.</span><span class="sxs-lookup"><span data-stu-id="65271-126">This generalization makes it possible to deploy many VMs from a single image.</span></span> <span data-ttu-id="65271-127">Durante o desprovisionamento, o nome do host é redefinido como *localhost.localdomain*.</span><span class="sxs-lookup"><span data-stu-id="65271-127">During deprovisioning, the host name is reset to *localhost.localdomain*.</span></span> <span data-ttu-id="65271-128">As chaves de host de SSH, as configurações de nameserver, a senha raiz e as concessões de DHCP em cache também são excluídas.</span><span class="sxs-lookup"><span data-stu-id="65271-128">SSH host keys, nameserver configurations, root password, and cached DHCP leases are also deleted.</span></span>

<span data-ttu-id="65271-129">Para desprovisionar a máquina virtual, use o agente de VM do Azure (waagent).</span><span class="sxs-lookup"><span data-stu-id="65271-129">To deprovision the VM, use the Azure VM agent (waagent).</span></span> <span data-ttu-id="65271-130">O agente de VM do Azure está instalado na VM e gerencia o provisionamento e a interação com o Azure Fabric Controller.</span><span class="sxs-lookup"><span data-stu-id="65271-130">The Azure VM agent is installed on the VM and manages provisioning and interacting with the Azure Fabric Controller.</span></span> <span data-ttu-id="65271-131">Para saber mais, confira o [Guia do usuário do agente Linux para o Azure](agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="65271-131">For more information, see the [Azure Linux Agent user guide](agent-user-guide.md).</span></span>

<span data-ttu-id="65271-132">Conectar-se à sua VM usando o SSH e executar o comando para desprovisionar a VM.</span><span class="sxs-lookup"><span data-stu-id="65271-132">Connect to your VM using SSH and run the command to deprovision the VM.</span></span> <span data-ttu-id="65271-133">Com o argumento `+user`, a última conta de usuário provisionada e os dados associados também são excluídos.</span><span class="sxs-lookup"><span data-stu-id="65271-133">With the `+user` argument, the last provisioned user account and any associated data are also deleted.</span></span> <span data-ttu-id="65271-134">Substitua o endereço IP de exemplo pelo endereço IP público de sua VM.</span><span class="sxs-lookup"><span data-stu-id="65271-134">Replace the example IP address with the public IP address of your VM.</span></span>

<span data-ttu-id="65271-135">SSH para a VM.</span><span class="sxs-lookup"><span data-stu-id="65271-135">SSH to the VM.</span></span>
```bash
ssh azureuser@52.174.34.95
```
<span data-ttu-id="65271-136">Desprovisione a VM.</span><span class="sxs-lookup"><span data-stu-id="65271-136">Deprovision the VM.</span></span>

```bash
sudo waagent -deprovision+user -force
```
<span data-ttu-id="65271-137">Feche a sessão do SSH.</span><span class="sxs-lookup"><span data-stu-id="65271-137">Close the SSH session.</span></span>

```bash
exit
```

### <a name="deallocate-and-mark-the-vm-as-generalized"></a><span data-ttu-id="65271-138">Desalocar e marcar a VM como generalizada</span><span class="sxs-lookup"><span data-stu-id="65271-138">Deallocate and mark the VM as generalized</span></span>

<span data-ttu-id="65271-139">Para criar uma imagem, a VM precisará ser desalocada.</span><span class="sxs-lookup"><span data-stu-id="65271-139">To create an image, the VM needs to be deallocated.</span></span> <span data-ttu-id="65271-140">Desaloque a VM usando [az vm deallocate](/cli//azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="65271-140">Deallocate the VM using [az vm deallocate](/cli//azure/vm#deallocate).</span></span> 
   
```azurecli-interactive 
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="65271-141">Por fim, defina o estado da VM como generalizado com [az vm generalize](/cli//azure/vm#generalize), de maneira que a plataforma do Azure saiba que a VM foi generalizada.</span><span class="sxs-lookup"><span data-stu-id="65271-141">Finally, set the state of the VM as generalized with [az vm generalize](/cli//azure/vm#generalize) so the Azure platform knows the VM has been generalized.</span></span> <span data-ttu-id="65271-142">Você só pode criar uma imagem por meio de uma VM generalizada.</span><span class="sxs-lookup"><span data-stu-id="65271-142">You can only create an image from a generalized VM.</span></span>
   
```azurecli-interactive 
az vm generalize --resource-group myResourceGroup --name myVM
```

### <a name="create-the-image"></a><span data-ttu-id="65271-143">Criar a imagem</span><span class="sxs-lookup"><span data-stu-id="65271-143">Create the image</span></span>

<span data-ttu-id="65271-144">Agora você pode criar uma imagem da VM usando [az image create](/cli//azure/image#create).</span><span class="sxs-lookup"><span data-stu-id="65271-144">Now you can create an image of the VM by using [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="65271-145">O exemplo a seguir cria uma imagem chamada *myImage* por meio de uma VM chamada *myVM*.</span><span class="sxs-lookup"><span data-stu-id="65271-145">The following example creates an image named *myImage* from a VM named *myVM*.</span></span>
   
```azurecli-interactive 
az image create \
    --resource-group myResourceGroup \
    --name myImage \
    --source myVM
```
 
## <a name="create-vms-from-the-image"></a><span data-ttu-id="65271-146">Criar VMs por meio da imagem</span><span class="sxs-lookup"><span data-stu-id="65271-146">Create VMs from the image</span></span>

<span data-ttu-id="65271-147">Agora que tem uma imagem, você pode criar uma ou mais VMs novas por meio da imagem usando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="65271-147">Now that you have an image, you can create one or more new VMs from the image using [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="65271-148">O exemplo a seguir cria uma VM chamada *myVMfromImage* por meio da imagem chamada *myImage*.</span><span class="sxs-lookup"><span data-stu-id="65271-148">The following example creates a VM named *myVMfromImage* from the image named *myImage*.</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVMfromImage \
    --image myImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

## <a name="image-management"></a><span data-ttu-id="65271-149">Gerenciamento de imagens</span><span class="sxs-lookup"><span data-stu-id="65271-149">Image management</span></span> 

<span data-ttu-id="65271-150">Estes são alguns exemplos de tarefas comuns de gerenciamento de imagem e como para concluí-las usando a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="65271-150">Here are some examples of common image management tasks and how to complete them using the Azure CLI.</span></span>

<span data-ttu-id="65271-151">Liste todas as imagens por nome em um formato de tabela.</span><span class="sxs-lookup"><span data-stu-id="65271-151">List all images by name in a table format.</span></span>

```azurecli-interactive 
az image list \
  --resource-group myResourceGroup
```

<span data-ttu-id="65271-152">Exclua uma imagem.</span><span class="sxs-lookup"><span data-stu-id="65271-152">Delete an image.</span></span> <span data-ttu-id="65271-153">Este exemplo exclui a imagem denominada *myOldImage* do *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="65271-153">This example deletes the image named *myOldImage* from the *myResourceGroup*.</span></span>

```azurecli-interactive 
az image delete \
    --name myOldImage \
    --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="65271-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="65271-154">Next steps</span></span>

<span data-ttu-id="65271-155">Neste tutorial, você criou uma imagem de VM personalizada.</span><span class="sxs-lookup"><span data-stu-id="65271-155">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="65271-156">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="65271-156">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="65271-157">Desprovisionar e generalizar VMs</span><span class="sxs-lookup"><span data-stu-id="65271-157">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="65271-158">Criar uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="65271-158">Create a custom image</span></span>
> * <span data-ttu-id="65271-159">Criar uma VM por meio de uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="65271-159">Create a VM from a custom image</span></span>
> * <span data-ttu-id="65271-160">Listar todas as imagens na sua assinatura</span><span class="sxs-lookup"><span data-stu-id="65271-160">List all the images in your subscription</span></span>
> * <span data-ttu-id="65271-161">Excluir uma imagem</span><span class="sxs-lookup"><span data-stu-id="65271-161">Delete an image</span></span>

<span data-ttu-id="65271-162">Avance para o próximo tutorial para saber mais sobre máquinas virtuais de alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="65271-162">Advance to the next tutorial to learn about highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="65271-163">[Criar VMs altamente disponíveis](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="65271-163">[Create highly available VMs](tutorial-availability-sets.md).</span></span>

