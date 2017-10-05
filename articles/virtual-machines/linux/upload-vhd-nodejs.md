---
title: Carregar uma imagem personalizada do Linux com a CLI 1.0 do Azure | Microsoft Docs
description: "Crie e carregue um VHD (disco rígido virtual) no Azure com uma imagem personalizada do Linux usando o modelo de implantação do Resource Manager e a CLI 1.0 do Azure."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/10/2016
ms.author: iainfou
ms.openlocfilehash: ca4c6cb9296028275b2b032af0c94baabeec1223
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-image-by-using-the-azure-cli-10"></a><span data-ttu-id="b582b-103">Carregar e criar uma VM Linux com base em uma imagem de disco personalizada usando a CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="b582b-103">Upload and create a Linux VM from custom disk image by using the Azure CLI 1.0</span></span>
<span data-ttu-id="b582b-104">Este artigo mostra como carregar um VHD (disco rígido virtual) no Azure usando o modelo de implantação do Resource Manager e criar VMs Linux com base nessa imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="b582b-104">This article shows you how to upload a virtual hard disk (VHD) to Azure using the Resource Manager deployment model and create Linux VMs from this custom image.</span></span> <span data-ttu-id="b582b-105">Essa funcionalidade permite que você instale e configure uma distribuição do Linux segundo suas necessidades e use esse VHD para criar rapidamente máquinas virtuais (VMs) do Azure.</span><span class="sxs-lookup"><span data-stu-id="b582b-105">This functionality allows you to install and configure a Linux distro to your requirements and then use that VHD to quickly create Azure virtual machines (VMs).</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="b582b-106">Versões da CLI para concluir a tarefa</span><span class="sxs-lookup"><span data-stu-id="b582b-106">CLI versions to complete the task</span></span>
<span data-ttu-id="b582b-107">Você pode concluir a tarefa usando uma das seguintes versões da CLI:</span><span class="sxs-lookup"><span data-stu-id="b582b-107">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="b582b-108">[CLI 1.0 do Azure](#quick-commands) – nossa CLI para os modelos de implantação clássico e de gerenciamento de recursos (este artigo)</span><span class="sxs-lookup"><span data-stu-id="b582b-108">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="b582b-109">[CLI 2.0 do Azure](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) – nossa última geração de CLI para o modelo de implantação de gerenciamento de recursos</span><span class="sxs-lookup"><span data-stu-id="b582b-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="b582b-110">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="b582b-110">Quick commands</span></span>
<span data-ttu-id="b582b-111">Se você precisar realizar rapidamente a tarefa, a seção a seguir detalha a base de dados de comandos para carregar uma VM no Azure.</span><span class="sxs-lookup"><span data-stu-id="b582b-111">If you need to quickly accomplish the task, the following section details the base commands to upload a VM to Azure.</span></span> <span data-ttu-id="b582b-112">Mais informações detalhadas e contexto para cada etapa podem ser encontrados no restante do documento, [começando aqui](#requirements).</span><span class="sxs-lookup"><span data-stu-id="b582b-112">More detailed information and context for each step can be found the rest of the document, [starting here](#requirements).</span></span>

<span data-ttu-id="b582b-113">Verifique se [a CLI 1.0 do Azure](../../cli-install-nodejs.md) está conectada e usando o modo Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="b582b-113">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="b582b-114">Nos exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="b582b-114">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="b582b-115">Os nomes de parâmetro de exemplo incluíram `myResourceGroup`, `mystorageaccount` e `myimages`.</span><span class="sxs-lookup"><span data-stu-id="b582b-115">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="b582b-116">Em primeiro lugar, crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b582b-116">First, create a resource group.</span></span> <span data-ttu-id="b582b-117">O exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` no local `WestUs`:</span><span class="sxs-lookup"><span data-stu-id="b582b-117">The following example creates a resource group named `myResourceGroup` in the `WestUs` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

<span data-ttu-id="b582b-118">Crie uma conta de armazenamento para manter seus discos virtuais.</span><span class="sxs-lookup"><span data-stu-id="b582b-118">Create a storage account to hold your virtual disks.</span></span> <span data-ttu-id="b582b-119">O exemplo a seguir cria uma conta de armazenamento chamada `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="b582b-119">The following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

<span data-ttu-id="b582b-120">Lista as chaves de acesso para a sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b582b-120">List the access keys for your storage account.</span></span> <span data-ttu-id="b582b-121">Anote `key1`:</span><span class="sxs-lookup"><span data-stu-id="b582b-121">Make a note of `key1`:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="b582b-122">Crie um contêiner dentro de sua conta de armazenamento usando a chave de armazenamento obtida.</span><span class="sxs-lookup"><span data-stu-id="b582b-122">Create a container within your storage account using the storage key you obtained.</span></span> <span data-ttu-id="b582b-123">O exemplo a seguir cria um contêiner denominado `myimages` usando o valor de chave de armazenamento de `key1`:</span><span class="sxs-lookup"><span data-stu-id="b582b-123">The following example creates a container named `myimages` using the storage key value from `key1`:</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

<span data-ttu-id="b582b-124">Por fim, carregue o VHD no contêiner que você criou.</span><span class="sxs-lookup"><span data-stu-id="b582b-124">Finally, upload your VHD to the container you created.</span></span> <span data-ttu-id="b582b-125">Especifique o caminho local para o VHD em `/path/to/disk/mydisk.vhd`:</span><span class="sxs-lookup"><span data-stu-id="b582b-125">Specify the local path to your VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

<span data-ttu-id="b582b-126">Agora você pode criar uma VM do disco virtual carregado [usando um modelo do Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="b582b-126">You can now create a VM from your uploaded virtual disk [using a Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span></span> <span data-ttu-id="b582b-127">Você também pode usar a CLI, especificando o URI para o seu disco (`--image-urn`).</span><span class="sxs-lookup"><span data-stu-id="b582b-127">You can also use the CLI by specifying the URI to your disk (`--image-urn`).</span></span> <span data-ttu-id="b582b-128">O exemplo a seguir cria uma VM denominada `myVM` usando o disco virtual carregado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="b582b-128">The following example creates a VM named `myVM` using the virtual disk previously uploaded:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
```

<span data-ttu-id="b582b-129">A conta de armazenamento de destino deve ser a mesma em que você carregou o disco virtual.</span><span class="sxs-lookup"><span data-stu-id="b582b-129">The destination storage account has to be the same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="b582b-130">Você também precisará especificar todos os parâmetros adicionais necessários ou responder a prompts deles pelo comando `azure vm create` , como rede virtual, endereço IP público, nome de usuário e chaves SSH.</span><span class="sxs-lookup"><span data-stu-id="b582b-130">You also need to specify, or answer prompts for, all the additional parameters required by the `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="b582b-131">Leia mais sobre os [parâmetros do Resource Manager na CLI disponíveis](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="b582b-131">You can read more about the [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="b582b-132">Requisitos</span><span class="sxs-lookup"><span data-stu-id="b582b-132">Requirements</span></span>
<span data-ttu-id="b582b-133">Para concluir as etapas a seguir, você precisa:</span><span class="sxs-lookup"><span data-stu-id="b582b-133">To complete the following steps, you need:</span></span>

* <span data-ttu-id="b582b-134">**Sistema operacional Linux instalado em um arquivo .vhd** - Instale uma [distribuição Linux endossada pelo Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (ou confira as [informações para as distribuições não endossadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) em um disco virtual no formato VHD.</span><span class="sxs-lookup"><span data-stu-id="b582b-134">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) to a virtual disk in the VHD format.</span></span> <span data-ttu-id="b582b-135">Existem várias ferramentas para criar uma VM e o VHD:</span><span class="sxs-lookup"><span data-stu-id="b582b-135">Multiple tools exist to create a VM and VHD:</span></span>
  * <span data-ttu-id="b582b-136">Instalar e configurar o [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) ou o [KVM](http://www.linux-kvm.org/page/RunningKVM), tomando o cuidado de usar o VHD como seu formato de imagem.</span><span class="sxs-lookup"><span data-stu-id="b582b-136">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care to use VHD as your image format.</span></span> <span data-ttu-id="b582b-137">Se necessário, você pode [converter uma imagem](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) usando `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="b582b-137">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="b582b-138">Também pode usar o Hyper-V [no Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) ou [no Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="b582b-138">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="b582b-139">Não há suporte para o formato VHDX mais recente no Azure.</span><span class="sxs-lookup"><span data-stu-id="b582b-139">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="b582b-140">Ao criar uma VM, especifique VHD como o formato.</span><span class="sxs-lookup"><span data-stu-id="b582b-140">When you create a VM, specify VHD as the format.</span></span> <span data-ttu-id="b582b-141">Se necessário, será possível converter discos VHDX para VHD usando o cmdlet [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) ou [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b582b-141">If needed, you can convert VHDX disks to VHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or the [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="b582b-142">Além disso, o Azure não dá suporte ao carregamento de VHDs dinâmicos, por isso você precisa converter esses discos para VHDs estáticos antes de carregar.</span><span class="sxs-lookup"><span data-stu-id="b582b-142">Further, Azure does not support uploading dynamic VHDs, so you need to convert such disks to static VHDs before uploading.</span></span> <span data-ttu-id="b582b-143">Você pode usar ferramentas como o [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) para converter os discos dinâmicos durante o processo de carregamento no Azure.</span><span class="sxs-lookup"><span data-stu-id="b582b-143">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) to convert dynamic disks during the process of uploading to Azure.</span></span>
> 
> 

* <span data-ttu-id="b582b-144">As VMs criadas com base em sua imagem personalizada devem residir na mesma conta de armazenamento que a imagem</span><span class="sxs-lookup"><span data-stu-id="b582b-144">VMs created from your custom image must reside in the same storage account as the image itself</span></span>
  * <span data-ttu-id="b582b-145">Criar uma conta de armazenamento e um contêiner para manter a imagem personalizada e as VMs criadas</span><span class="sxs-lookup"><span data-stu-id="b582b-145">Create a storage account and container to hold both your custom image and created VMs</span></span>
  * <span data-ttu-id="b582b-146">Depois de criar todas as VMs, você poderá excluir a imagem com segurança</span><span class="sxs-lookup"><span data-stu-id="b582b-146">After you have created all your VMs, you can safely delete your image</span></span>

<span data-ttu-id="b582b-147">Verifique se [a CLI 1.0 do Azure](../../cli-install-nodejs.md) está conectada e usando o modo Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="b582b-147">Make sure that you have [the Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="b582b-148">Nos exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="b582b-148">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="b582b-149">Os nomes de parâmetro de exemplo incluíram `myResourceGroup`, `mystorageaccount` e `myimages`.</span><span class="sxs-lookup"><span data-stu-id="b582b-149">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="b582b-150"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="b582b-150"><a id="prepimage"> </a></span></span>

## <a name="prepare-the-image-to-be-uploaded"></a><span data-ttu-id="b582b-151">Preparar a imagem a ser carregada</span><span class="sxs-lookup"><span data-stu-id="b582b-151">Prepare the image to be uploaded</span></span>
<span data-ttu-id="b582b-152">O Azure dá suporte a várias distribuições do Linux (consulte [Distribuições endossadas](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="b582b-152">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="b582b-153">Os seguintes artigos explicam como preparar as diversas distribuições Linux com suporte no Azure:</span><span class="sxs-lookup"><span data-stu-id="b582b-153">The following articles guide you through how to prepare the various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="b582b-154">**[Distribuições com base em CentOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="b582b-154">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="b582b-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="b582b-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="b582b-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="b582b-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="b582b-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="b582b-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="b582b-158">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="b582b-158">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="b582b-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="b582b-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="b582b-160">**[Outros — Distribuições não endossadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="b582b-160">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="b582b-161">Veja também as **[Observações de instalação do Linux](create-upload-generic.md#general-linux-installation-notes)** para obter mais dicas gerais sobre como preparar as imagens do Linux para o Azure.</span><span class="sxs-lookup"><span data-stu-id="b582b-161">Also see the **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="b582b-162">O [SLA da plataforma Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/) se aplica às VMs que executam o Linux somente quando uma das distribuições endossadas é usada com os detalhes da configuração, conforme especificado na seção “Versões com suporte” em [Linux em distribuições endossadas pelo Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b582b-162">The [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies to VMs running Linux only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="create-a-resource-group"></a><span data-ttu-id="b582b-163">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="b582b-163">Create a resource group</span></span>
<span data-ttu-id="b582b-164">Os grupos de recursos reúnem logicamente todos os recursos do Azure para dar suporte às suas máquinas virtuais, como a rede virtual e o armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b582b-164">Resource groups logically bring together all the Azure resources to support your virtual machines, such as the virtual networking and storage.</span></span> <span data-ttu-id="b582b-165">Leia mais sobre os [grupos de recursos do Azure aqui](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b582b-165">Read more about [Azure resource groups here](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="b582b-166">Antes de carregar sua imagem de disco personalizada e criar VMs, primeiro você precisa criar um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b582b-166">Before uploading your custom disk image and creating VMs, you first need to create a resource group.</span></span> 

<span data-ttu-id="b582b-167">O exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` no local `WestUS`:</span><span class="sxs-lookup"><span data-stu-id="b582b-167">The following example creates a resource group named `myResourceGroup` in the `WestUS` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="b582b-168">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="b582b-168">Create a storage account</span></span>
<span data-ttu-id="b582b-169">As VMs são armazenadas como blobs de páginas em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b582b-169">VMs are stored as page blobs within a storage account.</span></span> <span data-ttu-id="b582b-170">Leia mais sobre o [armazenamento de blobs do Azure aqui](../../storage/common/storage-introduction.md#blob-storage).</span><span class="sxs-lookup"><span data-stu-id="b582b-170">Read more about [Azure blob storage here](../../storage/common/storage-introduction.md#blob-storage).</span></span> <span data-ttu-id="b582b-171">Você cria uma conta de armazenamento para suas VMs e imagem de disco personalizadas.</span><span class="sxs-lookup"><span data-stu-id="b582b-171">You create a storage account for your custom disk image and VMs.</span></span> <span data-ttu-id="b582b-172">Todas as VMs criadas com base na imagem de disco personalizada precisam estar na mesma conta de armazenamento que a imagem.</span><span class="sxs-lookup"><span data-stu-id="b582b-172">Any VMs that you create from your custom disk image need to be in the same storage account as that image.</span></span>

<span data-ttu-id="b582b-173">O exemplo a seguir cria uma conta de armazenamento denominada `mystorageaccount` no grupo de recursos criado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="b582b-173">The following example creates a storage account named `mystorageaccount` in the resource group previously created:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="b582b-174">Listar chaves da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="b582b-174">List storage account keys</span></span>
<span data-ttu-id="b582b-175">O Azure gera duas chaves de acesso de 512 bits para cada conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b582b-175">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="b582b-176">Essas chaves de acesso são usadas durante a autenticação na conta de armazenamento, por exemplo, para executar operações de gravação.</span><span class="sxs-lookup"><span data-stu-id="b582b-176">These access keys are used when authenticating to the storage account, such as to carry out write operations.</span></span> <span data-ttu-id="b582b-177">Leia mais sobre [como gerenciar o acesso ao armazenamento aqui](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="b582b-177">Read more about [managing access to storage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="b582b-178">É possível exibir as chaves de acesso com o comando `azure storage account keys list` .</span><span class="sxs-lookup"><span data-stu-id="b582b-178">You can view access keys with the `azure storage account keys list` command.</span></span>

<span data-ttu-id="b582b-179">Veja as chaves de acesso da conta de armazenamento que você criou:</span><span class="sxs-lookup"><span data-stu-id="b582b-179">View the access keys for the storage account you created:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="b582b-180">A saída deverá ser semelhante a:</span><span class="sxs-lookup"><span data-stu-id="b582b-180">The output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK

```
<span data-ttu-id="b582b-181">Anote `key1` , pois você usará isso para interagir com sua conta de armazenamento nas próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="b582b-181">Make a note of `key1` as you will use it to interact with your storage account in the next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="b582b-182">Criar um contêiner de armazenamento</span><span class="sxs-lookup"><span data-stu-id="b582b-182">Create a storage container</span></span>
<span data-ttu-id="b582b-183">Da mesma forma que você cria diferentes diretórios para organizar logicamente seu sistema de arquivos local, crie contêineres em uma conta de armazenamento para organizar suas imagens e discos virtuais.</span><span class="sxs-lookup"><span data-stu-id="b582b-183">In the same way that you create different directories to logically organize your local file system, you create containers within a storage account to organize your virtual disks and images.</span></span> <span data-ttu-id="b582b-184">Uma conta de armazenamento pode conter qualquer quantidade de contêineres.</span><span class="sxs-lookup"><span data-stu-id="b582b-184">A storage account can contain any number of containers.</span></span> 

<span data-ttu-id="b582b-185">O exemplo a seguir cria contêiner chamado `myimages`, especificando a chave de acesso obtida na etapa anterior (`key1`):</span><span class="sxs-lookup"><span data-stu-id="b582b-185">The following example creates a container named `myimages`, specifying the access key obtained in the previous step (`key1`):</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

## <a name="upload-vhd"></a><span data-ttu-id="b582b-186">Carregar o VHD</span><span class="sxs-lookup"><span data-stu-id="b582b-186">Upload VHD</span></span>
<span data-ttu-id="b582b-187">Agora, você pode efetivamente carregar sua imagem de disco personalizada.</span><span class="sxs-lookup"><span data-stu-id="b582b-187">Now you can actually upload your custom disk image.</span></span> <span data-ttu-id="b582b-188">Assim como ocorre com todos os discos virtuais usados pelas VMs, você carrega e armazenará sua imagem de disco personalizada como um blob de páginas.</span><span class="sxs-lookup"><span data-stu-id="b582b-188">As with all virtual disks used by VMs, you upload and store your custom disk image as a page blob.</span></span>

<span data-ttu-id="b582b-189">Especifique sua chave de acesso, o contêiner que você criou na etapa anterior e o caminho para a imagem de disco personalizada no seu computador local:</span><span class="sxs-lookup"><span data-stu-id="b582b-189">Specify your access key, the container you created in the previous step, and then the path to the custom disk image on your local computer:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

## <a name="create-vm-from-custom-image"></a><span data-ttu-id="b582b-190">Criar uma VM com base em uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="b582b-190">Create VM from custom image</span></span>
<span data-ttu-id="b582b-191">Quando você cria VMs da sua imagem do disco personalizada, especifique o URI para a imagem de disco.</span><span class="sxs-lookup"><span data-stu-id="b582b-191">When you create VMs from your custom disk image, specify the URI to the disk image.</span></span> <span data-ttu-id="b582b-192">Verifique se a conta de armazenamento de destino corresponde ao local em que a imagem de disco personalizada está armazenada.</span><span class="sxs-lookup"><span data-stu-id="b582b-192">Ensure that the destination storage account matches where your custom disk image is stored.</span></span> <span data-ttu-id="b582b-193">Você pode criar sua VM usando a CLI do Azure ou o modelo JSON do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b582b-193">You can create your VM using the Azure CLI or Resource Manager JSON template.</span></span>

### <a name="create-a-vm-using-the-azure-cli"></a><span data-ttu-id="b582b-194">Criar uma VM usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="b582b-194">Create a VM using the Azure CLI</span></span>
<span data-ttu-id="b582b-195">Especifique o parâmetro `--image-urn` com o comando `azure vm create` para apontar para a imagem de disco personalizada.</span><span class="sxs-lookup"><span data-stu-id="b582b-195">You specify the `--image-urn` parameter with the `azure vm create` command to point to your custom disk image.</span></span> <span data-ttu-id="b582b-196">Verifique se `--storage-account-name` corresponde à conta de armazenamento em que a imagem de disco personalizada está armazenada.</span><span class="sxs-lookup"><span data-stu-id="b582b-196">Ensure that `--storage-account-name` matches the storage account where your custom disk image is stored.</span></span> <span data-ttu-id="b582b-197">Você não precisa usar o mesmo contêiner como a imagem de disco personalizada para armazenar suas VMs.</span><span class="sxs-lookup"><span data-stu-id="b582b-197">You do not have to use the same container as the custom disk image to store your VMs.</span></span> <span data-ttu-id="b582b-198">Certifique-se de criar recipientes adicionais da mesma forma como as etapas anteriores antes de carregar as imagens de disco personalizadas.</span><span class="sxs-lookup"><span data-stu-id="b582b-198">Make sure to create any additional containers in the same way as the earlier steps before uploading your custom disk images.</span></span>

<span data-ttu-id="b582b-199">O exemplo a seguir cria uma VM denominada `myVM` da imagem do disco personalizada:</span><span class="sxs-lookup"><span data-stu-id="b582b-199">The following example creates a VM named `myVM` from your custom disk image:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
    --storage-account-name mystorageaccount
```

<span data-ttu-id="b582b-200">Você ainda precisará especificar todos os parâmetros adicionais necessários ou responder a prompts deles pelo comando `azure vm create` , como rede virtual, endereço IP público, nome de usuário e chaves SSH.</span><span class="sxs-lookup"><span data-stu-id="b582b-200">You still need to specify, or answer prompts for, all the additional parameters required by the `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="b582b-201">Leia mais sobre os [parâmetros do Resource Manager na CLI disponíveis](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="b582b-201">Read more about the [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

### <a name="create-a-vm-using-a-json-template"></a><span data-ttu-id="b582b-202">Criar uma VM usando um modelo JSON</span><span class="sxs-lookup"><span data-stu-id="b582b-202">Create a VM using a JSON template</span></span>
<span data-ttu-id="b582b-203">Os modelos do Azure Resource Manager são arquivos JSON (JavaScript Object Notation) que definem o ambiente que você deseja criar.</span><span class="sxs-lookup"><span data-stu-id="b582b-203">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define the environment you wish to build.</span></span> <span data-ttu-id="b582b-204">Os modelos são divididos em diferentes provedores de recursos, como computação ou rede.</span><span class="sxs-lookup"><span data-stu-id="b582b-204">The templates are broken down in to different resource providers such as compute or network.</span></span> <span data-ttu-id="b582b-205">Você pode usar os modelos existentes ou escrever seus próprios.</span><span class="sxs-lookup"><span data-stu-id="b582b-205">You can use existing templates or write your own.</span></span> <span data-ttu-id="b582b-206">Saiba mais sobre como [usar o Resource Manager e os modelos](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b582b-206">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="b582b-207">No provedor `Microsoft.Compute/virtualMachines` do seu modelo, haverá um nó `storageProfile` que contém os detalhes de configuração da sua VM.</span><span class="sxs-lookup"><span data-stu-id="b582b-207">Within the `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains the configuration details for your VM.</span></span> <span data-ttu-id="b582b-208">Os dois parâmetros principais a serem editados são os URIs `image` e `vhd` que apontam para a imagem de disco personalizada e o disco virtual da nova VM.</span><span class="sxs-lookup"><span data-stu-id="b582b-208">The two main parameters to edit are the `image` and `vhd` URIs that point to your custom disk image and your new VM's virtual disk.</span></span> <span data-ttu-id="b582b-209">A seguir está um exemplo do JSON para o uso de uma imagem de disco personalizada:</span><span class="sxs-lookup"><span data-stu-id="b582b-209">The following shows an example of the JSON for using a custom disk image:</span></span>

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

<span data-ttu-id="b582b-210">Você pode usar [este modelo existente para criar uma VM de uma imagem personalizada](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) ou ler sobre como [criar seus próprios modelos do Azure Resource Manager](../../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b582b-210">You can use [this existing template to create a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="b582b-211">Depois de configurar um modelo, crie suas VMs usando o comando `azure group deployment create` .</span><span class="sxs-lookup"><span data-stu-id="b582b-211">Once you have a template configured, you create your VMs using the `azure group deployment create` command.</span></span> <span data-ttu-id="b582b-212">Especifique o URI do modelo JSON com o parâmetro `--template-uri` :</span><span class="sxs-lookup"><span data-stu-id="b582b-212">Specify the URI of your JSON template with the `--template-uri` parameter:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="b582b-213">Se você tiver um arquivo JSON armazenado localmente no computador, será possível usar o parâmetro `--template-file` :</span><span class="sxs-lookup"><span data-stu-id="b582b-213">If you have a JSON file stored locally on your computer, you can use the `--template-file` parameter instead:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="b582b-214">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b582b-214">Next steps</span></span>
<span data-ttu-id="b582b-215">Depois de preparar e carregar seu disco virtual personalizado, leia mais sobre como [usar o Resource Manager e os modelos](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b582b-215">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="b582b-216">É recomendável [adicionar um disco de dados](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) às novas VMs.</span><span class="sxs-lookup"><span data-stu-id="b582b-216">You may also want to [add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to your new VMs.</span></span> <span data-ttu-id="b582b-217">Se você tiver aplicativos em execução nas VMs que precisa acessar, não se esqueça de [abrir as portas e os pontos de extremidade](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b582b-217">If you have applications running on your VMs that you need to access, be sure to [open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

