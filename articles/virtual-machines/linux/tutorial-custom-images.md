---
title: imagens VM personalizadas aaaCreate com hello CLI do Azure | Microsoft Docs
description: "Tutorial - criar uma imagem VM personalizada usando Olá CLI do Azure."
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
ms.openlocfilehash: 217a993c0c1d48939b74108ac6c5f7a1a619416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-hello-cli"></a><span data-ttu-id="f63cc-103">Criar uma imagem personalizada de uma VM do Azure usando Olá CLI</span><span class="sxs-lookup"><span data-stu-id="f63cc-103">Create a custom image of an Azure VM using hello CLI</span></span>

<span data-ttu-id="f63cc-104">Imagens personalizadas são como imagens do marketplace, mas você mesmo as cria.</span><span class="sxs-lookup"><span data-stu-id="f63cc-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="f63cc-105">Imagens personalizadas podem ser usado toobootstrap configurações como pré-carregamento de aplicativos, configurações de aplicativo e outras configurações do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="f63cc-105">Custom images can be used toobootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="f63cc-106">Neste tutorial, você criará sua própria imagem personalizada de uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="f63cc-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="f63cc-107">Você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="f63cc-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f63cc-108">Desprovisionar e generalizar VMs</span><span class="sxs-lookup"><span data-stu-id="f63cc-108">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="f63cc-109">Criar uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="f63cc-109">Create a custom image</span></span>
> * <span data-ttu-id="f63cc-110">Criar uma VM por meio de uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="f63cc-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="f63cc-111">Lista todas as imagens de saudação em sua assinatura</span><span class="sxs-lookup"><span data-stu-id="f63cc-111">List all hello images in your subscription</span></span>
> * <span data-ttu-id="f63cc-112">Excluir uma imagem</span><span class="sxs-lookup"><span data-stu-id="f63cc-112">Delete an image</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f63cc-113">Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="f63cc-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="f63cc-114">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="f63cc-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="f63cc-115">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f63cc-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="f63cc-116">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="f63cc-116">Before you begin</span></span>

<span data-ttu-id="f63cc-117">etapas de saudação abaixo detalham como tootake uma VM existente e desative-o para um personalizado pode ser reutilizado da imagem que você podem usar toocreate novas instâncias VM.</span><span class="sxs-lookup"><span data-stu-id="f63cc-117">hello steps below detail how tootake an existing VM and turn it into a re-usable custom image that you can use toocreate new VM instances.</span></span>

<span data-ttu-id="f63cc-118">exemplo de hello toocomplete neste tutorial, você deve ter uma máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="f63cc-118">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="f63cc-119">Se necessário, este [exemplo de script](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) pode criar uma para você.</span><span class="sxs-lookup"><span data-stu-id="f63cc-119">If needed, this [script sample](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) can create one for you.</span></span> <span data-ttu-id="f63cc-120">Trabalho tutorial hello, substitua VM e o grupo de recursos de saudação nomes onde for necessário.</span><span class="sxs-lookup"><span data-stu-id="f63cc-120">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

## <a name="create-a-custom-image"></a><span data-ttu-id="f63cc-121">Criar uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="f63cc-121">Create a custom image</span></span>

<span data-ttu-id="f63cc-122">toocreate uma imagem de uma máquina virtual, você precisa tooprepare Olá VM, desprovisionamento, desalocando e, em seguida, marcando fonte Olá VM como generalizado.</span><span class="sxs-lookup"><span data-stu-id="f63cc-122">toocreate an image of a virtual machine, you need tooprepare hello VM by deprovisioning, deallocating, and then marking hello source VM as generalized.</span></span> <span data-ttu-id="f63cc-123">Uma vez Olá que VM tenha sido preparada, você pode criar uma imagem.</span><span class="sxs-lookup"><span data-stu-id="f63cc-123">Once hello VM has been prepared, you can create an image.</span></span>

### <a name="deprovision-hello-vm"></a><span data-ttu-id="f63cc-124">Saudação de desprovisionamento VM</span><span class="sxs-lookup"><span data-stu-id="f63cc-124">Deprovision hello VM</span></span> 

<span data-ttu-id="f63cc-125">Desprovisionamento generaliza Olá VM removendo informações específicas de computador.</span><span class="sxs-lookup"><span data-stu-id="f63cc-125">Deprovisioning generalizes hello VM by removing machine-specific information.</span></span> <span data-ttu-id="f63cc-126">Este generalização torna possível toodeploy muitas máquinas virtuais de uma única imagem.</span><span class="sxs-lookup"><span data-stu-id="f63cc-126">This generalization makes it possible toodeploy many VMs from a single image.</span></span> <span data-ttu-id="f63cc-127">Durante o desprovisionamento, nome de host de saudação é redefinido muito*localdomain*.</span><span class="sxs-lookup"><span data-stu-id="f63cc-127">During deprovisioning, hello host name is reset too*localhost.localdomain*.</span></span> <span data-ttu-id="f63cc-128">As chaves de host de SSH, as configurações de nameserver, a senha raiz e as concessões de DHCP em cache também são excluídas.</span><span class="sxs-lookup"><span data-stu-id="f63cc-128">SSH host keys, nameserver configurations, root password, and cached DHCP leases are also deleted.</span></span>

<span data-ttu-id="f63cc-129">Olá toodeprovision VM, usar o agente de VM do Azure hello (waagent).</span><span class="sxs-lookup"><span data-stu-id="f63cc-129">toodeprovision hello VM, use hello Azure VM agent (waagent).</span></span> <span data-ttu-id="f63cc-130">Agente de VM do Azure Olá Olá VM está instalado e gerencia o provisionamento e interagir com hello controlador de malha do Azure.</span><span class="sxs-lookup"><span data-stu-id="f63cc-130">hello Azure VM agent is installed on hello VM and manages provisioning and interacting with hello Azure Fabric Controller.</span></span> <span data-ttu-id="f63cc-131">Para obter mais informações, consulte Olá [guia do usuário do agente Linux do Azure](agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="f63cc-131">For more information, see hello [Azure Linux Agent user guide](agent-user-guide.md).</span></span>

<span data-ttu-id="f63cc-132">Conecte-se tooyour VM usando SSH e execução Olá comando toodeprovision Olá VM.</span><span class="sxs-lookup"><span data-stu-id="f63cc-132">Connect tooyour VM using SSH and run hello command toodeprovision hello VM.</span></span> <span data-ttu-id="f63cc-133">Com hello `+user` argumento, a última conta de usuário provisionado hello e quaisquer dados associados também serão excluídos.</span><span class="sxs-lookup"><span data-stu-id="f63cc-133">With hello `+user` argument, hello last provisioned user account and any associated data are also deleted.</span></span> <span data-ttu-id="f63cc-134">Substitua o endereço IP de exemplo hello com endereço IP público de saudação da VM.</span><span class="sxs-lookup"><span data-stu-id="f63cc-134">Replace hello example IP address with hello public IP address of your VM.</span></span>

<span data-ttu-id="f63cc-135">SSH toohello VM.</span><span class="sxs-lookup"><span data-stu-id="f63cc-135">SSH toohello VM.</span></span>
```bash
ssh azureuser@52.174.34.95
```
<span data-ttu-id="f63cc-136">Saudação de desprovisionamento VM.</span><span class="sxs-lookup"><span data-stu-id="f63cc-136">Deprovision hello VM.</span></span>

```bash
sudo waagent -deprovision+user -force
```
<span data-ttu-id="f63cc-137">Feche a sessão SSH hello.</span><span class="sxs-lookup"><span data-stu-id="f63cc-137">Close hello SSH session.</span></span>

```bash
exit
```

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a><span data-ttu-id="f63cc-138">Desalocar e marcar Olá VM como generalizado</span><span class="sxs-lookup"><span data-stu-id="f63cc-138">Deallocate and mark hello VM as generalized</span></span>

<span data-ttu-id="f63cc-139">toocreate uma imagem, Olá VM precisa toobe desalocada.</span><span class="sxs-lookup"><span data-stu-id="f63cc-139">toocreate an image, hello VM needs toobe deallocated.</span></span> <span data-ttu-id="f63cc-140">Desalocar Olá VM usando [az vm desalocar](/cli//azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="f63cc-140">Deallocate hello VM using [az vm deallocate](/cli//azure/vm#deallocate).</span></span> 
   
```azurecli-interactive 
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="f63cc-141">Por fim, definir estado de saudação do hello VM como generalizado com [az vm generalizar](/cli//azure/vm#generalize) para Olá plataforma Windows Azure Saiba Olá VM tenha sido generalizada.</span><span class="sxs-lookup"><span data-stu-id="f63cc-141">Finally, set hello state of hello VM as generalized with [az vm generalize](/cli//azure/vm#generalize) so hello Azure platform knows hello VM has been generalized.</span></span> <span data-ttu-id="f63cc-142">Você só pode criar uma imagem por meio de uma VM generalizada.</span><span class="sxs-lookup"><span data-stu-id="f63cc-142">You can only create an image from a generalized VM.</span></span>
   
```azurecli-interactive 
az vm generalize --resource-group myResourceGroup --name myVM
```

### <a name="create-hello-image"></a><span data-ttu-id="f63cc-143">Criar imagem Olá</span><span class="sxs-lookup"><span data-stu-id="f63cc-143">Create hello image</span></span>

<span data-ttu-id="f63cc-144">Agora você pode criar uma imagem de VM de saudação usando [criar imagem az](/cli//azure/image#create).</span><span class="sxs-lookup"><span data-stu-id="f63cc-144">Now you can create an image of hello VM by using [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="f63cc-145">Olá, exemplo a seguir cria uma imagem chamada *myImage* de uma VM denominada *myVM*.</span><span class="sxs-lookup"><span data-stu-id="f63cc-145">hello following example creates an image named *myImage* from a VM named *myVM*.</span></span>
   
```azurecli-interactive 
az image create \
    --resource-group myResourceGroup \
    --name myImage \
    --source myVM
```
 
## <a name="create-vms-from-hello-image"></a><span data-ttu-id="f63cc-146">Criar VMs de imagem Olá</span><span class="sxs-lookup"><span data-stu-id="f63cc-146">Create VMs from hello image</span></span>

<span data-ttu-id="f63cc-147">Agora que você tem uma imagem, você pode criar um ou mais novas VMs do uso de imagem Olá [criar vm az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="f63cc-147">Now that you have an image, you can create one or more new VMs from hello image using [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="f63cc-148">Olá, exemplo a seguir cria uma VM denominada *myVMfromImage* de imagem Olá chamada *myImage*.</span><span class="sxs-lookup"><span data-stu-id="f63cc-148">hello following example creates a VM named *myVMfromImage* from hello image named *myImage*.</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVMfromImage \
    --image myImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

## <a name="image-management"></a><span data-ttu-id="f63cc-149">Gerenciamento de imagens</span><span class="sxs-lookup"><span data-stu-id="f63cc-149">Image management</span></span> 

<span data-ttu-id="f63cc-150">Aqui estão alguns exemplos de tarefas comuns de gerenciamento de imagem e como toocomplete-los usando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="f63cc-150">Here are some examples of common image management tasks and how toocomplete them using hello Azure CLI.</span></span>

<span data-ttu-id="f63cc-151">Liste todas as imagens por nome em um formato de tabela.</span><span class="sxs-lookup"><span data-stu-id="f63cc-151">List all images by name in a table format.</span></span>

```azurecli-interactive 
az image list \
  --resource-group myResourceGroup
```

<span data-ttu-id="f63cc-152">Exclua uma imagem.</span><span class="sxs-lookup"><span data-stu-id="f63cc-152">Delete an image.</span></span> <span data-ttu-id="f63cc-153">Este exemplo exclui Olá imagem chamada *myOldImage* de saudação *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="f63cc-153">This example deletes hello image named *myOldImage* from hello *myResourceGroup*.</span></span>

```azurecli-interactive 
az image delete \
    --name myOldImage \
    --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="f63cc-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f63cc-154">Next steps</span></span>

<span data-ttu-id="f63cc-155">Neste tutorial, você criou uma imagem de VM personalizada.</span><span class="sxs-lookup"><span data-stu-id="f63cc-155">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="f63cc-156">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="f63cc-156">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f63cc-157">Desprovisionar e generalizar VMs</span><span class="sxs-lookup"><span data-stu-id="f63cc-157">Deprovision and generalize VMs</span></span>
> * <span data-ttu-id="f63cc-158">Criar uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="f63cc-158">Create a custom image</span></span>
> * <span data-ttu-id="f63cc-159">Criar uma VM por meio de uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="f63cc-159">Create a VM from a custom image</span></span>
> * <span data-ttu-id="f63cc-160">Lista todas as imagens de saudação em sua assinatura</span><span class="sxs-lookup"><span data-stu-id="f63cc-160">List all hello images in your subscription</span></span>
> * <span data-ttu-id="f63cc-161">Excluir uma imagem</span><span class="sxs-lookup"><span data-stu-id="f63cc-161">Delete an image</span></span>

<span data-ttu-id="f63cc-162">Avançar toohello toolearn próximo de tutorial sobre máquinas virtuais altamente disponíveis.</span><span class="sxs-lookup"><span data-stu-id="f63cc-162">Advance toohello next tutorial toolearn about highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="f63cc-163">[Criar VMs altamente disponíveis](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="f63cc-163">[Create highly available VMs](tutorial-availability-sets.md).</span></span>

