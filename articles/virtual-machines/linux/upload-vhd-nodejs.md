---
title: aaaUpload uma imagem personalizada do Linux com o Azure CLI 1.0 | Microsoft Docs
description: "Criar e carregar tooAzure um disco rígido virtual (VHD) com uma imagem personalizada do Linux usando o modelo de implantação do Gerenciador de recursos de saudação e hello 1.0 da CLI do Azure."
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
ms.openlocfilehash: 0bbd232debee1e632233d1c010e388dbc1548bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-image-by-using-hello-azure-cli-10"></a><span data-ttu-id="1232b-103">Carregar e criar uma VM do Linux de imagem de disco personalizada usando Olá 1.0 da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="1232b-103">Upload and create a Linux VM from custom disk image by using hello Azure CLI 1.0</span></span>
<span data-ttu-id="1232b-104">Este artigo mostra como tooupload um disco rígido virtual (VHD) usando o tooAzure Olá modelo de implantação do Gerenciador de recursos e criar VMs do Linux usando essa imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="1232b-104">This article shows you how tooupload a virtual hard disk (VHD) tooAzure using hello Resource Manager deployment model and create Linux VMs from this custom image.</span></span> <span data-ttu-id="1232b-105">Essa funcionalidade permite que você tooinstall e configurar um requisitos de tooyour de distribuição do Linux e, em seguida, usar esse VHD tooquickly criar máquinas virtuais (VMs) do Azure.</span><span class="sxs-lookup"><span data-stu-id="1232b-105">This functionality allows you tooinstall and configure a Linux distro tooyour requirements and then use that VHD tooquickly create Azure virtual machines (VMs).</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="1232b-106">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="1232b-106">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="1232b-107">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="1232b-107">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="1232b-108">[1.0 de CLI do Azure](#quick-commands) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="1232b-108">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="1232b-109">[2.0 do CLI do Azure](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="1232b-109">[Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="1232b-110">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="1232b-110">Quick commands</span></span>
<span data-ttu-id="1232b-111">Se você precisar tooquickly realizar tarefa hello, Olá Olá de detalhes da seção a seguir base tooupload comandos tooAzure uma VM.</span><span class="sxs-lookup"><span data-stu-id="1232b-111">If you need tooquickly accomplish hello task, hello following section details hello base commands tooupload a VM tooAzure.</span></span> <span data-ttu-id="1232b-112">Obter mais informações e o contexto para cada etapa pode ser encontrada restante de saudação do documento hello, [Iniciar aqui](#requirements).</span><span class="sxs-lookup"><span data-stu-id="1232b-112">More detailed information and context for each step can be found hello rest of hello document, [starting here](#requirements).</span></span>

<span data-ttu-id="1232b-113">Certifique-se de que você tenha [hello Azure CLI 1.0](../../cli-install-nodejs.md) conectado e usando o modo do Gerenciador de recursos:</span><span class="sxs-lookup"><span data-stu-id="1232b-113">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="1232b-114">Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="1232b-114">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="1232b-115">Os nomes de parâmetro de exemplo incluíram `myResourceGroup`, `mystorageaccount` e `myimages`.</span><span class="sxs-lookup"><span data-stu-id="1232b-115">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="1232b-116">Em primeiro lugar, crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1232b-116">First, create a resource group.</span></span> <span data-ttu-id="1232b-117">Olá, exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` em Olá `WestUs` local:</span><span class="sxs-lookup"><span data-stu-id="1232b-117">hello following example creates a resource group named `myResourceGroup` in hello `WestUs` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

<span data-ttu-id="1232b-118">Crie um toohold de conta de armazenamento seus discos virtuais.</span><span class="sxs-lookup"><span data-stu-id="1232b-118">Create a storage account toohold your virtual disks.</span></span> <span data-ttu-id="1232b-119">Olá, exemplo a seguir cria uma conta de armazenamento denominada `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="1232b-119">hello following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

<span data-ttu-id="1232b-120">Lista Olá chaves de acesso para sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1232b-120">List hello access keys for your storage account.</span></span> <span data-ttu-id="1232b-121">Anote `key1`:</span><span class="sxs-lookup"><span data-stu-id="1232b-121">Make a note of `key1`:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="1232b-122">Crie um recipiente dentro de sua conta de armazenamento usando a chave de armazenamento de saudação obtidos.</span><span class="sxs-lookup"><span data-stu-id="1232b-122">Create a container within your storage account using hello storage key you obtained.</span></span> <span data-ttu-id="1232b-123">Olá, exemplo a seguir cria um contêiner denominado `myimages` usando o valor de chave de armazenamento de saudação do `key1`:</span><span class="sxs-lookup"><span data-stu-id="1232b-123">hello following example creates a container named `myimages` using hello storage key value from `key1`:</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

<span data-ttu-id="1232b-124">Por fim, carregue seu contêiner de toohello VHD que você criou.</span><span class="sxs-lookup"><span data-stu-id="1232b-124">Finally, upload your VHD toohello container you created.</span></span> <span data-ttu-id="1232b-125">Especificar Olá caminho local tooyour VHD em `/path/to/disk/mydisk.vhd`:</span><span class="sxs-lookup"><span data-stu-id="1232b-125">Specify hello local path tooyour VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

<span data-ttu-id="1232b-126">Agora você pode criar uma VM do disco virtual carregado [usando um modelo do Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="1232b-126">You can now create a VM from your uploaded virtual disk [using a Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd).</span></span> <span data-ttu-id="1232b-127">Você também pode usar o hello CLI especificando o disco do hello URI tooyour (`--image-urn`).</span><span class="sxs-lookup"><span data-stu-id="1232b-127">You can also use hello CLI by specifying hello URI tooyour disk (`--image-urn`).</span></span> <span data-ttu-id="1232b-128">Olá, exemplo a seguir cria uma VM denominada `myVM` usando o disco virtual de saudação carregado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="1232b-128">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
```

<span data-ttu-id="1232b-129">conta de armazenamento de destino Olá tem toobe Olá mesmo como em que você carregou o disco virtual para.</span><span class="sxs-lookup"><span data-stu-id="1232b-129">hello destination storage account has toobe hello same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="1232b-130">Você também precisa toospecify ou responder a prompts para, todos os parâmetros adicionais exigidos pelo Olá de Olá `azure vm create` comando, como a rede virtual, o endereço IP público, o nome de usuário e as chaves de SSH.</span><span class="sxs-lookup"><span data-stu-id="1232b-130">You also need toospecify, or answer prompts for, all hello additional parameters required by hello `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="1232b-131">Você pode ler mais sobre Olá [parâmetros disponíveis do Gerenciador de recursos de CLI](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="1232b-131">You can read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="1232b-132">Requisitos</span><span class="sxs-lookup"><span data-stu-id="1232b-132">Requirements</span></span>
<span data-ttu-id="1232b-133">Olá toocomplete seguintes etapas, você precisa:</span><span class="sxs-lookup"><span data-stu-id="1232b-133">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="1232b-134">**Sistema operacional Linux instalado em um arquivo. vhd** -instalar um [distribuição aprovadas Azure Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (ou consulte [informações para distribuições não aprovadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa o disco virtual no hello VHD formato.</span><span class="sxs-lookup"><span data-stu-id="1232b-134">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="1232b-135">Várias ferramentas existem toocreate uma VM e o VHD:</span><span class="sxs-lookup"><span data-stu-id="1232b-135">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="1232b-136">Instalar e configurar [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) ou [KVM](http://www.linux-kvm.org/page/RunningKVM), tomando cuidado toouse VHD como seu formato de imagem.</span><span class="sxs-lookup"><span data-stu-id="1232b-136">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="1232b-137">Se necessário, você pode [converter uma imagem](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) usando `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="1232b-137">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="1232b-138">Também pode usar o Hyper-V [no Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) ou [no Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="1232b-138">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="1232b-139">Não há suporte para o formato VHDX mais recente de saudação no Azure.</span><span class="sxs-lookup"><span data-stu-id="1232b-139">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="1232b-140">Quando você cria uma máquina virtual, especifique o VHD como formato de saudação.</span><span class="sxs-lookup"><span data-stu-id="1232b-140">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="1232b-141">Se necessário, você pode converter tooVHD de discos VHDX usando [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) ou hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1232b-141">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="1232b-142">Além disso, Azure não oferece suporte Carregando VHDs dinâmicos, portanto, você precisa tooconvert toostatic esses discos VHDs antes de carregar.</span><span class="sxs-lookup"><span data-stu-id="1232b-142">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="1232b-143">Você pode usar ferramentas como [utilitários de VHD do Azure para ir](https://github.com/Microsoft/azure-vhd-utils-for-go) discos dinâmicos de tooconvert durante o processo de saudação de carregamento de tooAzure.</span><span class="sxs-lookup"><span data-stu-id="1232b-143">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 

* <span data-ttu-id="1232b-144">Máquinas virtuais criadas de sua imagem personalizada devem residir no hello mesmo conta de armazenamento como a própria imagem Olá</span><span class="sxs-lookup"><span data-stu-id="1232b-144">VMs created from your custom image must reside in hello same storage account as hello image itself</span></span>
  * <span data-ttu-id="1232b-145">Criar um toohold de conta e o contêiner de armazenamento sua imagem personalizada e VMs criadas</span><span class="sxs-lookup"><span data-stu-id="1232b-145">Create a storage account and container toohold both your custom image and created VMs</span></span>
  * <span data-ttu-id="1232b-146">Depois de criar todas as VMs, você poderá excluir a imagem com segurança</span><span class="sxs-lookup"><span data-stu-id="1232b-146">After you have created all your VMs, you can safely delete your image</span></span>

<span data-ttu-id="1232b-147">Certifique-se de que você tenha [hello Azure CLI 1.0](../../cli-install-nodejs.md) conectado e usando o modo do Gerenciador de recursos:</span><span class="sxs-lookup"><span data-stu-id="1232b-147">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="1232b-148">Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="1232b-148">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="1232b-149">Os nomes de parâmetro de exemplo incluíram `myResourceGroup`, `mystorageaccount` e `myimages`.</span><span class="sxs-lookup"><span data-stu-id="1232b-149">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `myimages`.</span></span>

<span data-ttu-id="1232b-150"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="1232b-150"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-image-toobe-uploaded"></a><span data-ttu-id="1232b-151">Preparar Olá imagem toobe carregado</span><span class="sxs-lookup"><span data-stu-id="1232b-151">Prepare hello image toobe uploaded</span></span>
<span data-ttu-id="1232b-152">O Azure dá suporte a várias distribuições do Linux (consulte [Distribuições endossadas](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="1232b-152">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="1232b-153">Olá artigos a seguir orientam você pelo como tooprepare Olá várias distribuições do Linux com suporte no Azure.</span><span class="sxs-lookup"><span data-stu-id="1232b-153">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="1232b-154">**[Distribuições com base em CentOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="1232b-154">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="1232b-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="1232b-155">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="1232b-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="1232b-156">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="1232b-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="1232b-157">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="1232b-158">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="1232b-158">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="1232b-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="1232b-159">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="1232b-160">**[Outros — Distribuições não endossadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="1232b-160">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="1232b-161">Consulte também Olá  **[notas de instalação Linux](create-upload-generic.md#general-linux-installation-notes)**  mais geral dicas sobre como preparar imagens do Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="1232b-161">Also see hello **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="1232b-162">Olá [plataforma Windows Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) aplica-se tooVMs executando o Linux somente quando uma saudação aprovados distribuições é usado com os detalhes de configuração Olá conforme especificado em 'Versões com suporte' [Linux no Azure aprovadas Distribuições](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1232b-162">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="create-a-resource-group"></a><span data-ttu-id="1232b-163">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="1232b-163">Create a resource group</span></span>
<span data-ttu-id="1232b-164">Grupos de recursos logicamente reunir toosupport de recursos do Azure Olá todas as suas máquinas virtuais, como redes virtuais hello e armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1232b-164">Resource groups logically bring together all hello Azure resources toosupport your virtual machines, such as hello virtual networking and storage.</span></span> <span data-ttu-id="1232b-165">Leia mais sobre os [grupos de recursos do Azure aqui](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1232b-165">Read more about [Azure resource groups here](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="1232b-166">Antes de carregar a imagem de disco personalizada e criar máquinas virtuais, você primeiro precisa toocreate um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1232b-166">Before uploading your custom disk image and creating VMs, you first need toocreate a resource group.</span></span> 

<span data-ttu-id="1232b-167">Olá, exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` em Olá `WestUS` local:</span><span class="sxs-lookup"><span data-stu-id="1232b-167">hello following example creates a resource group named `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure group create myResourceGroup --location "WestUS"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="1232b-168">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="1232b-168">Create a storage account</span></span>
<span data-ttu-id="1232b-169">As VMs são armazenadas como blobs de páginas em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1232b-169">VMs are stored as page blobs within a storage account.</span></span> <span data-ttu-id="1232b-170">Leia mais sobre o [armazenamento de blobs do Azure aqui](../../storage/common/storage-introduction.md#blob-storage).</span><span class="sxs-lookup"><span data-stu-id="1232b-170">Read more about [Azure blob storage here](../../storage/common/storage-introduction.md#blob-storage).</span></span> <span data-ttu-id="1232b-171">Você cria uma conta de armazenamento para suas VMs e imagem de disco personalizadas.</span><span class="sxs-lookup"><span data-stu-id="1232b-171">You create a storage account for your custom disk image and VMs.</span></span> <span data-ttu-id="1232b-172">Todas as máquinas virtuais que você criar a partir de seu toobe de necessidade de imagem de disco personalizada no Olá a mesma conta de armazenamento, como essa imagem.</span><span class="sxs-lookup"><span data-stu-id="1232b-172">Any VMs that you create from your custom disk image need toobe in hello same storage account as that image.</span></span>

<span data-ttu-id="1232b-173">Olá, exemplo a seguir cria uma conta de armazenamento denominada `mystorageaccount` no grupo de recursos de saudação criado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="1232b-173">hello following example creates a storage account named `mystorageaccount` in hello resource group previously created:</span></span>

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="1232b-174">Listar chaves da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="1232b-174">List storage account keys</span></span>
<span data-ttu-id="1232b-175">O Azure gera duas chaves de acesso de 512 bits para cada conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1232b-175">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="1232b-176">Essas chaves de acesso são usadas ao autenticar a conta de armazenamento de toohello, como toocarry operações de gravação.</span><span class="sxs-lookup"><span data-stu-id="1232b-176">These access keys are used when authenticating toohello storage account, such as toocarry out write operations.</span></span> <span data-ttu-id="1232b-177">Leia mais sobre [gerenciando acesso toostorage aqui](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="1232b-177">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="1232b-178">Você pode exibir as chaves de acesso com hello `azure storage account keys list` comando.</span><span class="sxs-lookup"><span data-stu-id="1232b-178">You can view access keys with hello `azure storage account keys list` command.</span></span>

<span data-ttu-id="1232b-179">Exibir chaves de acesso Olá Olá conta de armazenamento criada:</span><span class="sxs-lookup"><span data-stu-id="1232b-179">View hello access keys for hello storage account you created:</span></span>

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

<span data-ttu-id="1232b-180">saída de Hello é semelhante a:</span><span class="sxs-lookup"><span data-stu-id="1232b-180">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK

```
<span data-ttu-id="1232b-181">Anote `key1` como você o usará toointeract com as próximas etapas Olá sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1232b-181">Make a note of `key1` as you will use it toointeract with your storage account in hello next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="1232b-182">Criar um contêiner de armazenamento</span><span class="sxs-lookup"><span data-stu-id="1232b-182">Create a storage container</span></span>
<span data-ttu-id="1232b-183">Em Olá mesma maneira que você crie diferentes diretórios toologically organizar seu sistema de arquivos local, crie contêineres dentro de um tooorganize de conta de armazenamento seus discos virtuais e imagens.</span><span class="sxs-lookup"><span data-stu-id="1232b-183">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your virtual disks and images.</span></span> <span data-ttu-id="1232b-184">Uma conta de armazenamento pode conter qualquer quantidade de contêineres.</span><span class="sxs-lookup"><span data-stu-id="1232b-184">A storage account can contain any number of containers.</span></span> 

<span data-ttu-id="1232b-185">Olá, exemplo a seguir cria um contêiner denominado `myimages`, especificando a chave de acesso de saudação obtido na etapa anterior de saudação (`key1`):</span><span class="sxs-lookup"><span data-stu-id="1232b-185">hello following example creates a container named `myimages`, specifying hello access key obtained in hello previous step (`key1`):</span></span>

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

## <a name="upload-vhd"></a><span data-ttu-id="1232b-186">Carregar o VHD</span><span class="sxs-lookup"><span data-stu-id="1232b-186">Upload VHD</span></span>
<span data-ttu-id="1232b-187">Agora, você pode efetivamente carregar sua imagem de disco personalizada.</span><span class="sxs-lookup"><span data-stu-id="1232b-187">Now you can actually upload your custom disk image.</span></span> <span data-ttu-id="1232b-188">Assim como ocorre com todos os discos virtuais usados pelas VMs, você carrega e armazenará sua imagem de disco personalizada como um blob de páginas.</span><span class="sxs-lookup"><span data-stu-id="1232b-188">As with all virtual disks used by VMs, you upload and store your custom disk image as a page blob.</span></span>

<span data-ttu-id="1232b-189">Especifique sua chave de acesso, o contêiner de saudação criado na etapa anterior hello e hello, em seguida, a imagem de disco personalizada toohello caminho no computador local:</span><span class="sxs-lookup"><span data-stu-id="1232b-189">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk image on your local computer:</span></span>

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

## <a name="create-vm-from-custom-image"></a><span data-ttu-id="1232b-190">Criar uma VM com base em uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="1232b-190">Create VM from custom image</span></span>
<span data-ttu-id="1232b-191">Quando você criar VMs de sua imagem de disco personalizada, especifique a imagem de disco de toohello URI de saudação.</span><span class="sxs-lookup"><span data-stu-id="1232b-191">When you create VMs from your custom disk image, specify hello URI toohello disk image.</span></span> <span data-ttu-id="1232b-192">Certifique-se de que Olá correspondências de conta de armazenamento de destino onde a imagem de disco personalizada está armazenada.</span><span class="sxs-lookup"><span data-stu-id="1232b-192">Ensure that hello destination storage account matches where your custom disk image is stored.</span></span> <span data-ttu-id="1232b-193">Você pode criar sua VM usando o modelo de CLI do Azure ou o Gerenciador de recursos de JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="1232b-193">You can create your VM using hello Azure CLI or Resource Manager JSON template.</span></span>

### <a name="create-a-vm-using-hello-azure-cli"></a><span data-ttu-id="1232b-194">Criar uma VM usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="1232b-194">Create a VM using hello Azure CLI</span></span>
<span data-ttu-id="1232b-195">Especificar Olá `--image-urn` o parâmetro hello `azure vm create` imagem do comando toopoint tooyour disco personalizada.</span><span class="sxs-lookup"><span data-stu-id="1232b-195">You specify hello `--image-urn` parameter with hello `azure vm create` command toopoint tooyour custom disk image.</span></span> <span data-ttu-id="1232b-196">Certifique-se de que `--storage-account-name` correspondências Olá conta de armazenamento onde a imagem de disco personalizada está armazenada.</span><span class="sxs-lookup"><span data-stu-id="1232b-196">Ensure that `--storage-account-name` matches hello storage account where your custom disk image is stored.</span></span> <span data-ttu-id="1232b-197">Você não tem toouse Olá mesmo contêiner como Olá toostore de imagem de disco personalizada suas VMs.</span><span class="sxs-lookup"><span data-stu-id="1232b-197">You do not have toouse hello same container as hello custom disk image toostore your VMs.</span></span> <span data-ttu-id="1232b-198">Fazer toocreate se qualquer contêiner adicional em Olá mesma maneira que Olá etapas anteriores antes de carregar as imagens de disco personalizada.</span><span class="sxs-lookup"><span data-stu-id="1232b-198">Make sure toocreate any additional containers in hello same way as hello earlier steps before uploading your custom disk images.</span></span>

<span data-ttu-id="1232b-199">Olá, exemplo a seguir cria uma VM denominada `myVM` da imagem do disco personalizada:</span><span class="sxs-lookup"><span data-stu-id="1232b-199">hello following example creates a VM named `myVM` from your custom disk image:</span></span>

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
    --storage-account-name mystorageaccount
```

<span data-ttu-id="1232b-200">Você ainda precisa toospecify ou responder a prompts para, todos os parâmetros adicionais exigidos pelo Olá de Olá `azure vm create` comando, como a rede virtual, o endereço IP público, o nome de usuário e as chaves de SSH.</span><span class="sxs-lookup"><span data-stu-id="1232b-200">You still need toospecify, or answer prompts for, all hello additional parameters required by hello `azure vm create` command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="1232b-201">Leia mais sobre Olá [parâmetros disponíveis do Gerenciador de recursos de CLI](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="1232b-201">Read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

### <a name="create-a-vm-using-a-json-template"></a><span data-ttu-id="1232b-202">Criar uma VM usando um modelo JSON</span><span class="sxs-lookup"><span data-stu-id="1232b-202">Create a VM using a JSON template</span></span>
<span data-ttu-id="1232b-203">Modelos do Gerenciador de recursos do Azure são arquivos de notação JSON (JavaScript Object) que definem o ambiente Olá desejar toobuild.</span><span class="sxs-lookup"><span data-stu-id="1232b-203">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define hello environment you wish toobuild.</span></span> <span data-ttu-id="1232b-204">modelos de saudação são divididos em toodifferent provedores de recursos, como computação ou rede.</span><span class="sxs-lookup"><span data-stu-id="1232b-204">hello templates are broken down in toodifferent resource providers such as compute or network.</span></span> <span data-ttu-id="1232b-205">Você pode usar os modelos existentes ou escrever seus próprios.</span><span class="sxs-lookup"><span data-stu-id="1232b-205">You can use existing templates or write your own.</span></span> <span data-ttu-id="1232b-206">Saiba mais sobre como [usar o Resource Manager e os modelos](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1232b-206">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="1232b-207">Dentro de saudação `Microsoft.Compute/virtualMachines` provedor do seu modelo, você tem um `storageProfile` nó que contém os detalhes de configuração Olá para sua VM.</span><span class="sxs-lookup"><span data-stu-id="1232b-207">Within hello `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains hello configuration details for your VM.</span></span> <span data-ttu-id="1232b-208">Olá dois parâmetros principais tooedit são Olá `image` e `vhd` URIs do ponto de imagem de disco personalizada tooyour e disco virtual da VM seu novo.</span><span class="sxs-lookup"><span data-stu-id="1232b-208">hello two main parameters tooedit are hello `image` and `vhd` URIs that point tooyour custom disk image and your new VM's virtual disk.</span></span> <span data-ttu-id="1232b-209">a seguir Olá mostra um exemplo de hello JSON para usar uma imagem de disco personalizado:</span><span class="sxs-lookup"><span data-stu-id="1232b-209">hello following shows an example of hello JSON for using a custom disk image:</span></span>

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

<span data-ttu-id="1232b-210">Você pode usar [este toocreate de modelo existente uma VM por meio de uma imagem personalizada](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) ou leia sobre [criar seus próprios modelos do Azure Resource Manager](../../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="1232b-210">You can use [this existing template toocreate a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="1232b-211">Uma vez que um modelo configurado, você cria suas VMs usando Olá `azure group deployment create` comando.</span><span class="sxs-lookup"><span data-stu-id="1232b-211">Once you have a template configured, you create your VMs using hello `azure group deployment create` command.</span></span> <span data-ttu-id="1232b-212">Especifique Olá URI do seu modelo de JSON com hello `--template-uri` parâmetro:</span><span class="sxs-lookup"><span data-stu-id="1232b-212">Specify hello URI of your JSON template with hello `--template-uri` parameter:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="1232b-213">Se você tiver um arquivo JSON armazenado localmente no seu computador, você pode usar o hello `--template-file` parâmetro em vez disso:</span><span class="sxs-lookup"><span data-stu-id="1232b-213">If you have a JSON file stored locally on your computer, you can use hello `--template-file` parameter instead:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="1232b-214">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1232b-214">Next steps</span></span>
<span data-ttu-id="1232b-215">Depois de preparar e carregar seu disco virtual personalizado, leia mais sobre como [usar o Resource Manager e os modelos](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1232b-215">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="1232b-216">Você também pode desejar muito[adicionar um disco de dados](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour novas VMs.</span><span class="sxs-lookup"><span data-stu-id="1232b-216">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="1232b-217">Se você tiver aplicativos em execução em suas VMs que você precisa tooaccess, certifique-se muito[abrir portas e os pontos de extremidade](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1232b-217">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

