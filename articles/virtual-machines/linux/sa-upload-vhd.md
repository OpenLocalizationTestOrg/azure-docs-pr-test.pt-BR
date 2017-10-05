---
title: Carregar um disco Linux personalizado com a CLI 2.0 do Azure | Microsoft Docs
description: "Criar e carregar um VHD (disco rígido virtual) no Azure usando o modelo de implantação do Resource Manager e a CLI 2.0 do Azure"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: 9159960af396e89f373da711e0cc46fdd996ab83
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-with-the-azure-cli-20"></a><span data-ttu-id="27401-103">Carregar e criar uma VM Linux usando disco personalizado com a CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="27401-103">Upload and create a Linux VM from custom disk with the Azure CLI 2.0</span></span>
<span data-ttu-id="27401-104">Este artigo mostra como carregar um VHD (disco rígido virtual) em uma conta de armazenamento do Azure com a CLI 2.0 do Azure e como criar VMs Linux com base nesse disco personalizado.</span><span class="sxs-lookup"><span data-stu-id="27401-104">This article shows you how to upload a virtual hard disk (VHD) to an Azure storage account with the Azure CLI 2.0 and create Linux VMs from this custom disk.</span></span> <span data-ttu-id="27401-105">Você também pode executar essas etapas com a [CLI do Azure 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="27401-105">You can also perform these steps with the [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="27401-106">Essa funcionalidade permite que você instale e configure uma distribuição do Linux segundo suas necessidades e use esse VHD para criar rapidamente máquinas virtuais (VMs) do Azure.</span><span class="sxs-lookup"><span data-stu-id="27401-106">This functionality allows you to install and configure a Linux distro to your requirements and then use that VHD to quickly create Azure virtual machines (VMs).</span></span>

<span data-ttu-id="27401-107">Este tópico usa contas de armazenamento para os VHDs finais, mas você também pode realizar essas etapas usando [Managed Disks](upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="27401-107">This topic uses storage accounts for the final VHDs, but you can also do these steps using [managed disks](upload-vhd.md).</span></span> 

## <a name="quick-commands"></a><span data-ttu-id="27401-108">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="27401-108">Quick commands</span></span>
<span data-ttu-id="27401-109">Caso você precise realizar rapidamente a tarefa, a seção a seguir detalha os comandos básicos para carregar uma VHD no Azure.</span><span class="sxs-lookup"><span data-stu-id="27401-109">If you need to quickly accomplish the task, the following section details the base commands to upload a VHD to Azure.</span></span> <span data-ttu-id="27401-110">Mais informações detalhadas e contexto para cada etapa podem ser encontrados no restante do documento, [começando aqui](#requirements).</span><span class="sxs-lookup"><span data-stu-id="27401-110">More detailed information and context for each step can be found the rest of the document, [starting here](#requirements).</span></span>

<span data-ttu-id="27401-111">Certifique-se de que você tenha instalado a versão mais recente da [CLI 2.0 do Azure](/cli/azure/install-az-cli2) e entrado em uma conta do Azure usando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="27401-111">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="27401-112">Nos exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="27401-112">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="27401-113">Os nomes de parâmetro de exemplo incluíram `myResourceGroup`, `mystorageaccount` e `mydisks`.</span><span class="sxs-lookup"><span data-stu-id="27401-113">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="27401-114">Primeiro, crie um grupo de recursos com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="27401-114">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="27401-115">O exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` no local `WestUs`:</span><span class="sxs-lookup"><span data-stu-id="27401-115">The following example creates a resource group named `myResourceGroup` in the `WestUs` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="27401-116">Criar uma conta de armazenamento para armazenar seus discos virtuais com [criar conta de armazenamento az](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="27401-116">Create a storage account to hold your virtual disks with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="27401-117">O exemplo a seguir cria uma conta de armazenamento chamada `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="27401-117">The following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

<span data-ttu-id="27401-118">Lista as chaves de acesso para sua conta de armazenamento com [lista de chaves de conta de armazenamento az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="27401-118">List the access keys for your storage account with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="27401-119">Anote `key1`:</span><span class="sxs-lookup"><span data-stu-id="27401-119">Make a note of `key1`:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="27401-120">Crie um contêiner dentro de sua conta de armazenamento usando a chave de armazenamento obtida com [az storage container create](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="27401-120">Create a container within your storage account using the storage key you obtained with [az storage container create](/cli/azure/storage/container#create).</span></span> <span data-ttu-id="27401-121">O exemplo a seguir cria um contêiner denominado `mydisks` usando o valor de chave de armazenamento de `key1`:</span><span class="sxs-lookup"><span data-stu-id="27401-121">The following example creates a container named `mydisks` using the storage key value from `key1`:</span></span>

```azurecli
az storage container create --account-name mystorageaccount \
    --account-key key1 --name mydisks
```

<span data-ttu-id="27401-122">Por fim, carregue o VHD no contêiner criado com [carregamento de blob de armazenamento az](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="27401-122">Finally, upload your VHD to the container you created with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="27401-123">Especifique o caminho local para o VHD em `/path/to/disk/mydisk.vhd`:</span><span class="sxs-lookup"><span data-stu-id="27401-123">Specify the local path to your VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

<span data-ttu-id="27401-124">Especifique o URI para o disco (`--image`) com [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="27401-124">Specify the URI to your disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="27401-125">O exemplo a seguir cria uma VM denominada `myVM` usando o disco virtual carregado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="27401-125">The following example creates a VM named `myVM` using the virtual disk previously uploaded:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisk/myDisks.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="27401-126">A conta de armazenamento de destino deve ser a mesma em que você carregou o disco virtual.</span><span class="sxs-lookup"><span data-stu-id="27401-126">The destination storage account has to be the same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="27401-127">Você também precisará especificar todos os parâmetros adicionais necessários ou responder a prompts deles pelo comando **az vm create**, como rede virtual, endereço IP público, nome de usuário e chaves SSH.</span><span class="sxs-lookup"><span data-stu-id="27401-127">You also need to specify, or answer prompts for, all the additional parameters required by the **az vm create** command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="27401-128">Leia mais sobre os [parâmetros do Resource Manager na CLI disponíveis](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="27401-128">You can read more about the [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="27401-129">Requisitos</span><span class="sxs-lookup"><span data-stu-id="27401-129">Requirements</span></span>
<span data-ttu-id="27401-130">Para concluir as etapas a seguir, você precisa:</span><span class="sxs-lookup"><span data-stu-id="27401-130">To complete the following steps, you need:</span></span>

* <span data-ttu-id="27401-131">**Sistema operacional Linux instalado em um arquivo .vhd** - Instale uma [distribuição Linux endossada pelo Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (ou confira as [informações para as distribuições não endossadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) em um disco virtual no formato VHD.</span><span class="sxs-lookup"><span data-stu-id="27401-131">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) to a virtual disk in the VHD format.</span></span> <span data-ttu-id="27401-132">Existem várias ferramentas para criar uma VM e o VHD:</span><span class="sxs-lookup"><span data-stu-id="27401-132">Multiple tools exist to create a VM and VHD:</span></span>
  * <span data-ttu-id="27401-133">Instalar e configurar o [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) ou o [KVM](http://www.linux-kvm.org/page/RunningKVM), tomando o cuidado de usar o VHD como seu formato de imagem.</span><span class="sxs-lookup"><span data-stu-id="27401-133">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care to use VHD as your image format.</span></span> <span data-ttu-id="27401-134">Se necessário, você pode [converter uma imagem](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) usando `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="27401-134">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="27401-135">Também pode usar o Hyper-V [no Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) ou [no Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="27401-135">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="27401-136">Não há suporte para o formato VHDX mais recente no Azure.</span><span class="sxs-lookup"><span data-stu-id="27401-136">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="27401-137">Ao criar uma VM, especifique VHD como o formato.</span><span class="sxs-lookup"><span data-stu-id="27401-137">When you create a VM, specify VHD as the format.</span></span> <span data-ttu-id="27401-138">Se necessário, será possível converter discos VHDX para VHD usando o cmdlet [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) ou [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="27401-138">If needed, you can convert VHDX disks to VHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or the [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="27401-139">Além disso, o Azure não dá suporte ao carregamento de VHDs dinâmicos, por isso você precisa converter esses discos para VHDs estáticos antes de carregar.</span><span class="sxs-lookup"><span data-stu-id="27401-139">Further, Azure does not support uploading dynamic VHDs, so you need to convert such disks to static VHDs before uploading.</span></span> <span data-ttu-id="27401-140">Você pode usar ferramentas como o [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) para converter os discos dinâmicos durante o processo de carregamento no Azure.</span><span class="sxs-lookup"><span data-stu-id="27401-140">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) to convert dynamic disks during the process of uploading to Azure.</span></span>
> 
> 

* <span data-ttu-id="27401-141">As VMs criadas com base em seu disco personalizado devem residir na mesma conta de armazenamento que o disco</span><span class="sxs-lookup"><span data-stu-id="27401-141">VMs created from your custom disk must reside in the same storage account as the disk itself</span></span>
  * <span data-ttu-id="27401-142">Criar uma conta de armazenamento e um contêiner para manter o disco personalizado e as VMs criadas</span><span class="sxs-lookup"><span data-stu-id="27401-142">Create a storage account and container to hold both your custom disk and created VMs</span></span>
  * <span data-ttu-id="27401-143">Depois de criar todas as VMs, você poderá excluir o disco com segurança</span><span class="sxs-lookup"><span data-stu-id="27401-143">After you have created all your VMs, you can safely delete your disk</span></span>

<span data-ttu-id="27401-144">Certifique-se de que você tenha instalado a versão mais recente da [CLI 2.0 do Azure](/cli/azure/install-az-cli2) e entrado em uma conta do Azure usando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="27401-144">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="27401-145">Nos exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="27401-145">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="27401-146">Os nomes de parâmetro de exemplo incluíram `myResourceGroup`, `mystorageaccount` e `mydisks`.</span><span class="sxs-lookup"><span data-stu-id="27401-146">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="27401-147"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="27401-147"><a id="prepimage"> </a></span></span>

## <a name="prepare-the-disk-to-be-uploaded"></a><span data-ttu-id="27401-148">Preparar o disco a ser carregado</span><span class="sxs-lookup"><span data-stu-id="27401-148">Prepare the disk to be uploaded</span></span>
<span data-ttu-id="27401-149">O Azure dá suporte a várias distribuições do Linux (consulte [Distribuições endossadas](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="27401-149">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="27401-150">Os seguintes artigos explicam como preparar as diversas distribuições Linux com suporte no Azure:</span><span class="sxs-lookup"><span data-stu-id="27401-150">The following articles guide you through how to prepare the various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="27401-151">**[Distribuições com base em CentOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="27401-151">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="27401-152">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="27401-152">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="27401-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="27401-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="27401-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="27401-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="27401-155">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="27401-155">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="27401-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="27401-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="27401-157">**[Outros — Distribuições não endossadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="27401-157">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="27401-158">Veja também as **[Observações de instalação do Linux](create-upload-generic.md#general-linux-installation-notes)** para obter mais dicas gerais sobre como preparar as imagens do Linux para o Azure.</span><span class="sxs-lookup"><span data-stu-id="27401-158">Also see the **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="27401-159">O [SLA da plataforma Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/) se aplica às VMs que executam o Linux somente quando uma das distribuições endossadas é usada com os detalhes da configuração, conforme especificado na seção “Versões com suporte” em [Linux em distribuições endossadas pelo Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="27401-159">The [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies to VMs running Linux only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="create-a-resource-group"></a><span data-ttu-id="27401-160">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="27401-160">Create a resource group</span></span>
<span data-ttu-id="27401-161">Os grupos de recursos reúnem logicamente todos os recursos do Azure para dar suporte às suas máquinas virtuais, como a rede virtual e o armazenamento.</span><span class="sxs-lookup"><span data-stu-id="27401-161">Resource groups logically bring together all the Azure resources to support your virtual machines, such as the virtual networking and storage.</span></span> <span data-ttu-id="27401-162">Mais informações sobre grupos de recursos, veja [visão geral de grupos de recurso](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="27401-162">For more information resource groups, see [resource groups overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="27401-163">Antes de carregar seu disco personalizado e criar VMs, primeiro você precisa criar um grupo de recursos com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="27401-163">Before uploading your custom disk and creating VMs, you first need to create a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="27401-164">O exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` no local `westus`:</span><span class="sxs-lookup"><span data-stu-id="27401-164">The following example creates a resource group named `myResourceGroup` in the `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-a-storage-account"></a><span data-ttu-id="27401-165">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="27401-165">Create a storage account</span></span>

<span data-ttu-id="27401-166">Criar uma conta de armazenamento para seu disco personalizado e VMs com [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="27401-166">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="27401-167">Todas as VMs com discos não gerenciados criadas com base no disco personalizado precisam estar na mesma conta de armazenamento que o disco.</span><span class="sxs-lookup"><span data-stu-id="27401-167">Any VMs with unmanaged disks that you create from your custom disk need to be in the same storage account as that disk.</span></span> 

<span data-ttu-id="27401-168">O exemplo a seguir cria uma conta de armazenamento denominada `mystorageaccount` no grupo de recursos criado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="27401-168">The following example creates a storage account named `mystorageaccount` in the resource group previously created:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="27401-169">Listar chaves da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="27401-169">List storage account keys</span></span>
<span data-ttu-id="27401-170">O Azure gera duas chaves de acesso de 512 bits para cada conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="27401-170">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="27401-171">Essas chaves de acesso são usadas durante a autenticação na conta de armazenamento, por exemplo, para executar operações de gravação.</span><span class="sxs-lookup"><span data-stu-id="27401-171">These access keys are used when authenticating to the storage account, such as to carry out write operations.</span></span> <span data-ttu-id="27401-172">Leia mais sobre [como gerenciar o acesso ao armazenamento aqui](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="27401-172">Read more about [managing access to storage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="27401-173">Exibir as chaves de acesso com [lista de chaves de conta de armazenamento az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="27401-173">You view the access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="27401-174">Veja as chaves de acesso da conta de armazenamento que você criou:</span><span class="sxs-lookup"><span data-stu-id="27401-174">View the access keys for the storage account you created:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="27401-175">A saída deverá ser semelhante a:</span><span class="sxs-lookup"><span data-stu-id="27401-175">The output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="27401-176">Anote `key1` , pois você usará isso para interagir com sua conta de armazenamento nas próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="27401-176">Make a note of `key1` as you will use it to interact with your storage account in the next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="27401-177">Criar um contêiner de armazenamento</span><span class="sxs-lookup"><span data-stu-id="27401-177">Create a storage container</span></span>
<span data-ttu-id="27401-178">Da mesma forma que você cria diferentes diretórios para organizar logicamente seu sistema de arquivos local, crie contêineres em uma conta de armazenamento para organizar seus discos.</span><span class="sxs-lookup"><span data-stu-id="27401-178">In the same way that you create different directories to logically organize your local file system, you create containers within a storage account to organize your disks.</span></span> <span data-ttu-id="27401-179">Uma conta de armazenamento pode conter qualquer quantidade de contêineres.</span><span class="sxs-lookup"><span data-stu-id="27401-179">A storage account can contain any number of containers.</span></span> <span data-ttu-id="27401-180">Crie um contêiner com [az storage container create](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="27401-180">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="27401-181">O seguinte exemplo cria um contêiner chamado `mydisks`:</span><span class="sxs-lookup"><span data-stu-id="27401-181">The following example creates a container named `mydisks`:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

## <a name="upload-vhd"></a><span data-ttu-id="27401-182">Carregar o VHD</span><span class="sxs-lookup"><span data-stu-id="27401-182">Upload VHD</span></span>
<span data-ttu-id="27401-183">Agora, carregue seu disco personalizado com [az storage blob upload](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="27401-183">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="27401-184">Carregue e armazene seu disco personalizado como um blob de páginas.</span><span class="sxs-lookup"><span data-stu-id="27401-184">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="27401-185">Especifique sua chave de acesso, o contêiner que você criou na etapa anterior e o caminho para o disco personalizado no seu computador local:</span><span class="sxs-lookup"><span data-stu-id="27401-185">Specify your access key, the container you created in the previous step, and then the path to the custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

## <a name="create-the-vm"></a><span data-ttu-id="27401-186">Criar a VM</span><span class="sxs-lookup"><span data-stu-id="27401-186">Create the VM</span></span>
<span data-ttu-id="27401-187">Para criar uma VM com discos não gerenciados, especifique o URI para o disco (`--image`) com [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="27401-187">To create a VM with unmanaged disks, specify the URI to your disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="27401-188">O exemplo a seguir cria uma VM denominada `myVM` usando o disco virtual carregado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="27401-188">The following example creates a VM named `myVM` using the virtual disk previously uploaded:</span></span>

<span data-ttu-id="27401-189">Especifique o parâmetro `--image` com [az vm create](/cli/azure/vm#create) para apontar para o disco personalizado.</span><span class="sxs-lookup"><span data-stu-id="27401-189">You specify the `--image` parameter with [az vm create](/cli/azure/vm#create) to point to your custom disk.</span></span> <span data-ttu-id="27401-190">Verifique se `--storage-account` corresponde à conta de armazenamento em que o disco personalizado está armazenado.</span><span class="sxs-lookup"><span data-stu-id="27401-190">Ensure that `--storage-account` matches the storage account where your custom disk is stored.</span></span> <span data-ttu-id="27401-191">Você não precisa usar o mesmo contêiner que o disco personalizado para armazenar suas VMs.</span><span class="sxs-lookup"><span data-stu-id="27401-191">You do not have to use the same container as the custom disk to store your VMs.</span></span> <span data-ttu-id="27401-192">Certifique-se de criar recipientes adicionais da mesma forma como as etapas anteriores antes de carregar o disco personalizado.</span><span class="sxs-lookup"><span data-stu-id="27401-192">Make sure to create any additional containers in the same way as the earlier steps before uploading your custom disk.</span></span>

<span data-ttu-id="27401-193">O exemplo a seguir cria uma VM denominada `myVM` do disco personalizado:</span><span class="sxs-lookup"><span data-stu-id="27401-193">The following example creates a VM named `myVM` from your custom disk:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="27401-194">Você ainda precisará especificar todos os parâmetros adicionais necessários ou responder a prompts deles pelo comando **az vm create**, como nome de usuário e chaves SSH.</span><span class="sxs-lookup"><span data-stu-id="27401-194">You still need to specify, or answer prompts for, all the additional parameters required by the **az vm create** command such as username and SSH keys.</span></span>


## <a name="resource-manager-template"></a><span data-ttu-id="27401-195">Modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="27401-195">Resource Manager template</span></span>
<span data-ttu-id="27401-196">Os modelos do Azure Resource Manager são arquivos JSON (JavaScript Object Notation) que definem o ambiente que você deseja criar.</span><span class="sxs-lookup"><span data-stu-id="27401-196">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define the environment you wish to build.</span></span> <span data-ttu-id="27401-197">Os modelos são divididos em diferentes provedores de recursos, como computação ou rede.</span><span class="sxs-lookup"><span data-stu-id="27401-197">The templates are broken down in to different resource providers such as compute or network.</span></span> <span data-ttu-id="27401-198">Você pode usar os modelos existentes ou escrever seus próprios.</span><span class="sxs-lookup"><span data-stu-id="27401-198">You can use existing templates or write your own.</span></span> <span data-ttu-id="27401-199">Saiba mais sobre como [usar o Resource Manager e os modelos](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="27401-199">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="27401-200">No provedor `Microsoft.Compute/virtualMachines` do seu modelo, haverá um nó `storageProfile` que contém os detalhes de configuração da sua VM.</span><span class="sxs-lookup"><span data-stu-id="27401-200">Within the `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains the configuration details for your VM.</span></span> <span data-ttu-id="27401-201">Os dois parâmetros principais a serem editados são os URIs `image` e `vhd` que apontam para o disco personalizado e o disco virtual da nova VM.</span><span class="sxs-lookup"><span data-stu-id="27401-201">The two main parameters to edit are the `image` and `vhd` URIs that point to your custom disk and your new VM's virtual disk.</span></span> <span data-ttu-id="27401-202">A seguir está um exemplo do JSON para o uso de um disco personalizado:</span><span class="sxs-lookup"><span data-stu-id="27401-202">The following shows an example of the JSON for using a custom disk:</span></span>

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

<span data-ttu-id="27401-203">Você pode usar [este modelo existente para criar uma VM de uma imagem personalizada](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) ou ler sobre como [criar seus próprios modelos do Azure Resource Manager](../../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="27401-203">You can use [this existing template to create a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="27401-204">Quando você tiver um modelo configurado, use [criar implantação de grupo az](/cli/azure/group/deployment#create) para criar suas VMs.</span><span class="sxs-lookup"><span data-stu-id="27401-204">Once you have a template configured, use [az group deployment create](/cli/azure/group/deployment#create) to create your VMs.</span></span> <span data-ttu-id="27401-205">Especifique o URI do modelo JSON com o parâmetro `--template-uri` :</span><span class="sxs-lookup"><span data-stu-id="27401-205">Specify the URI of your JSON template with the `--template-uri` parameter:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="27401-206">Se você tiver um arquivo JSON armazenado localmente no computador, será possível usar o parâmetro `--template-file` :</span><span class="sxs-lookup"><span data-stu-id="27401-206">If you have a JSON file stored locally on your computer, you can use the `--template-file` parameter instead:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="27401-207">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="27401-207">Next steps</span></span>
<span data-ttu-id="27401-208">Depois de preparar e carregar seu disco virtual personalizado, leia mais sobre como [usar o Resource Manager e os modelos](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="27401-208">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="27401-209">É recomendável [adicionar um disco de dados](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) às novas VMs.</span><span class="sxs-lookup"><span data-stu-id="27401-209">You may also want to [add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to your new VMs.</span></span> <span data-ttu-id="27401-210">Se você tiver aplicativos em execução nas VMs que precisa acessar, não se esqueça de [abrir as portas e os pontos de extremidade](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="27401-210">If you have applications running on your VMs that you need to access, be sure to [open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

