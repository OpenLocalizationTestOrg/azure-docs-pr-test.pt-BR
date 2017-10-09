---
title: aaaUpload um disco Linux personalizada com o Azure CLI 2.0 | Microsoft Docs
description: "Criar e carregar um tooAzure de disco rígido virtual (VHD) usando o modelo de implantação do Gerenciador de recursos de saudação e hello 2.0 do CLI do Azure"
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
ms.openlocfilehash: cf8556ab4dfe6c4e5eff4e99fe1ddc44393f774c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a><span data-ttu-id="e8317-103">Carregar e criar uma VM do Linux do disco personalizado com hello 2.0 do CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="e8317-103">Upload and create a Linux VM from custom disk with hello Azure CLI 2.0</span></span>
<span data-ttu-id="e8317-104">Este artigo mostra como tooupload tooan um disco rígido virtual (VHD) armazenamento do Azure a conta com hello 2.0 do CLI do Azure e criar VMs do Linux no disco personalizado.</span><span class="sxs-lookup"><span data-stu-id="e8317-104">This article shows you how tooupload a virtual hard disk (VHD) tooan Azure storage account with hello Azure CLI 2.0 and create Linux VMs from this custom disk.</span></span> <span data-ttu-id="e8317-105">Você também pode executar essas etapas com hello [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e8317-105">You can also perform these steps with hello [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="e8317-106">Essa funcionalidade permite que você tooinstall e configurar um requisitos de tooyour de distribuição do Linux e, em seguida, usar esse VHD tooquickly criar máquinas virtuais (VMs) do Azure.</span><span class="sxs-lookup"><span data-stu-id="e8317-106">This functionality allows you tooinstall and configure a Linux distro tooyour requirements and then use that VHD tooquickly create Azure virtual machines (VMs).</span></span>

<span data-ttu-id="e8317-107">Este tópico usa contas de armazenamento para hello VHDs finais, mas você também pode fazer essas etapas usando [discos gerenciado](upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="e8317-107">This topic uses storage accounts for hello final VHDs, but you can also do these steps using [managed disks](upload-vhd.md).</span></span> 

## <a name="quick-commands"></a><span data-ttu-id="e8317-108">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="e8317-108">Quick commands</span></span>
<span data-ttu-id="e8317-109">Se você precisar tooquickly realizar tarefa hello, Olá Olá de detalhes da seção a seguir base tooupload comandos tooAzure um VHD.</span><span class="sxs-lookup"><span data-stu-id="e8317-109">If you need tooquickly accomplish hello task, hello following section details hello base commands tooupload a VHD tooAzure.</span></span> <span data-ttu-id="e8317-110">Obter mais informações e o contexto para cada etapa pode ser encontrada restante de saudação do documento hello, [Iniciar aqui](#requirements).</span><span class="sxs-lookup"><span data-stu-id="e8317-110">More detailed information and context for each step can be found hello rest of hello document, [starting here](#requirements).</span></span>

<span data-ttu-id="e8317-111">Certifique-se de que você tenha mais recente Olá [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e conectado através de conta do Azure tooan [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="e8317-111">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="e8317-112">Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="e8317-112">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="e8317-113">Os nomes de parâmetro de exemplo incluíram `myResourceGroup`, `mystorageaccount` e `mydisks`.</span><span class="sxs-lookup"><span data-stu-id="e8317-113">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="e8317-114">Primeiro, crie um grupo de recursos com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="e8317-114">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="e8317-115">Olá, exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` em Olá `WestUs` local:</span><span class="sxs-lookup"><span data-stu-id="e8317-115">hello following example creates a resource group named `myResourceGroup` in hello `WestUs` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="e8317-116">Criar um toohold de conta de armazenamento discos virtuais com [criar conta de armazenamento az](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="e8317-116">Create a storage account toohold your virtual disks with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="e8317-117">Olá, exemplo a seguir cria uma conta de armazenamento denominada `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="e8317-117">hello following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

<span data-ttu-id="e8317-118">Listar Olá chaves de acesso para sua conta de armazenamento com [lista de chaves de conta de armazenamento az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="e8317-118">List hello access keys for your storage account with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="e8317-119">Anote `key1`:</span><span class="sxs-lookup"><span data-stu-id="e8317-119">Make a note of `key1`:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="e8317-120">Criar um recipiente dentro de sua conta de armazenamento usando a chave de armazenamento de saudação obtidas com [criar contêiner de armazenamento az](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="e8317-120">Create a container within your storage account using hello storage key you obtained with [az storage container create](/cli/azure/storage/container#create).</span></span> <span data-ttu-id="e8317-121">Olá, exemplo a seguir cria um contêiner denominado `mydisks` usando o valor de chave de armazenamento de saudação do `key1`:</span><span class="sxs-lookup"><span data-stu-id="e8317-121">hello following example creates a container named `mydisks` using hello storage key value from `key1`:</span></span>

```azurecli
az storage container create --account-name mystorageaccount \
    --account-key key1 --name mydisks
```

<span data-ttu-id="e8317-122">Por fim, carregar o contêiner de toohello VHD criado com [carregamento de blob de armazenamento az](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="e8317-122">Finally, upload your VHD toohello container you created with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="e8317-123">Especificar Olá caminho local tooyour VHD em `/path/to/disk/mydisk.vhd`:</span><span class="sxs-lookup"><span data-stu-id="e8317-123">Specify hello local path tooyour VHD under `/path/to/disk/mydisk.vhd`:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

<span data-ttu-id="e8317-124">Especifique Olá URI tooyour disco (`--image`) com [criar vm az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="e8317-124">Specify hello URI tooyour disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="e8317-125">Olá, exemplo a seguir cria uma VM denominada `myVM` usando o disco virtual de saudação carregado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="e8317-125">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisk/myDisks.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="e8317-126">conta de armazenamento de destino Olá tem toobe Olá mesmo como em que você carregou o disco virtual para.</span><span class="sxs-lookup"><span data-stu-id="e8317-126">hello destination storage account has toobe hello same as where you uploaded your virtual disk to.</span></span> <span data-ttu-id="e8317-127">Você também precisa toospecify ou responder a prompts para, todos os parâmetros adicionais exigidos pelo Olá de Olá **criar vm az** comando, como a rede virtual, o endereço IP público, o nome de usuário e as chaves de SSH.</span><span class="sxs-lookup"><span data-stu-id="e8317-127">You also need toospecify, or answer prompts for, all hello additional parameters required by hello **az vm create** command such as virtual network, public IP address, username, and SSH keys.</span></span> <span data-ttu-id="e8317-128">Você pode ler mais sobre Olá [parâmetros disponíveis do Gerenciador de recursos de CLI](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="e8317-128">You can read more about hello [available CLI Resource Manager parameters](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).</span></span>

## <a name="requirements"></a><span data-ttu-id="e8317-129">Requisitos</span><span class="sxs-lookup"><span data-stu-id="e8317-129">Requirements</span></span>
<span data-ttu-id="e8317-130">Olá toocomplete seguintes etapas, você precisa:</span><span class="sxs-lookup"><span data-stu-id="e8317-130">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="e8317-131">**Sistema operacional Linux instalado em um arquivo. vhd** -instalar um [distribuição aprovadas Azure Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (ou consulte [informações para distribuições não aprovadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa o disco virtual no hello VHD formato.</span><span class="sxs-lookup"><span data-stu-id="e8317-131">**Linux operating system installed in a .vhd file** - Install an [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="e8317-132">Várias ferramentas existem toocreate uma VM e o VHD:</span><span class="sxs-lookup"><span data-stu-id="e8317-132">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="e8317-133">Instalar e configurar [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) ou [KVM](http://www.linux-kvm.org/page/RunningKVM), tomando cuidado toouse VHD como seu formato de imagem.</span><span class="sxs-lookup"><span data-stu-id="e8317-133">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="e8317-134">Se necessário, você pode [converter uma imagem](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) usando `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="e8317-134">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="e8317-135">Também pode usar o Hyper-V [no Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) ou [no Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="e8317-135">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="e8317-136">Não há suporte para o formato VHDX mais recente de saudação no Azure.</span><span class="sxs-lookup"><span data-stu-id="e8317-136">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="e8317-137">Quando você cria uma máquina virtual, especifique o VHD como formato de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8317-137">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="e8317-138">Se necessário, você pode converter tooVHD de discos VHDX usando [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) ou hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e8317-138">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="e8317-139">Além disso, Azure não oferece suporte Carregando VHDs dinâmicos, portanto, você precisa tooconvert toostatic esses discos VHDs antes de carregar.</span><span class="sxs-lookup"><span data-stu-id="e8317-139">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="e8317-140">Você pode usar ferramentas como [utilitários de VHD do Azure para ir](https://github.com/Microsoft/azure-vhd-utils-for-go) discos dinâmicos de tooconvert durante o processo de saudação de carregamento de tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e8317-140">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 

* <span data-ttu-id="e8317-141">Máquinas virtuais criadas do disco de dados personalizado devem residir no hello mesmo conta de armazenamento como o próprio disco Olá</span><span class="sxs-lookup"><span data-stu-id="e8317-141">VMs created from your custom disk must reside in hello same storage account as hello disk itself</span></span>
  * <span data-ttu-id="e8317-142">Criar um toohold de conta e o contêiner de armazenamento, seu disco personalizado e VMs criadas</span><span class="sxs-lookup"><span data-stu-id="e8317-142">Create a storage account and container toohold both your custom disk and created VMs</span></span>
  * <span data-ttu-id="e8317-143">Depois de criar todas as VMs, você poderá excluir o disco com segurança</span><span class="sxs-lookup"><span data-stu-id="e8317-143">After you have created all your VMs, you can safely delete your disk</span></span>

<span data-ttu-id="e8317-144">Certifique-se de que você tenha mais recente Olá [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e conectado através de conta do Azure tooan [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="e8317-144">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="e8317-145">Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="e8317-145">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="e8317-146">Os nomes de parâmetro de exemplo incluíram `myResourceGroup`, `mystorageaccount` e `mydisks`.</span><span class="sxs-lookup"><span data-stu-id="e8317-146">Example parameter names included `myResourceGroup`, `mystorageaccount`, and `mydisks`.</span></span>

<span data-ttu-id="e8317-147"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="e8317-147"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-disk-toobe-uploaded"></a><span data-ttu-id="e8317-148">Preparar Olá disco toobe carregado</span><span class="sxs-lookup"><span data-stu-id="e8317-148">Prepare hello disk toobe uploaded</span></span>
<span data-ttu-id="e8317-149">O Azure dá suporte a várias distribuições do Linux (consulte [Distribuições endossadas](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="e8317-149">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="e8317-150">Olá artigos a seguir orientam você pelo como tooprepare Olá várias distribuições do Linux com suporte no Azure.</span><span class="sxs-lookup"><span data-stu-id="e8317-150">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* <span data-ttu-id="e8317-151">**[Distribuições com base em CentOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="e8317-151">**[CentOS-based Distributions](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="e8317-152">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="e8317-152">**[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="e8317-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="e8317-153">**[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="e8317-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="e8317-154">**[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="e8317-155">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="e8317-155">**[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="e8317-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="e8317-156">**[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="e8317-157">**[Outros — Distribuições não endossadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="e8317-157">**[Other - Non-Endorsed Distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

<span data-ttu-id="e8317-158">Consulte também Olá  **[notas de instalação Linux](create-upload-generic.md#general-linux-installation-notes)**  mais geral dicas sobre como preparar imagens do Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="e8317-158">Also see hello **[Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="e8317-159">Olá [plataforma Windows Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) aplica-se tooVMs executando o Linux somente quando uma saudação aprovados distribuições é usado com os detalhes de configuração Olá conforme especificado em 'Versões com suporte' [Linux no Azure aprovadas Distribuições](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e8317-159">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="create-a-resource-group"></a><span data-ttu-id="e8317-160">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="e8317-160">Create a resource group</span></span>
<span data-ttu-id="e8317-161">Grupos de recursos logicamente reunir toosupport de recursos do Azure Olá todas as suas máquinas virtuais, como redes virtuais hello e armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e8317-161">Resource groups logically bring together all hello Azure resources toosupport your virtual machines, such as hello virtual networking and storage.</span></span> <span data-ttu-id="e8317-162">Mais informações sobre grupos de recursos, veja [visão geral de grupos de recurso](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e8317-162">For more information resource groups, see [resource groups overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="e8317-163">Antes de carregar o disco personalizado e criar máquinas virtuais, é necessário primeiro toocreate um grupo de recursos com [criar grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="e8317-163">Before uploading your custom disk and creating VMs, you first need toocreate a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="e8317-164">Olá, exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` em Olá `westus` local:</span><span class="sxs-lookup"><span data-stu-id="e8317-164">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-a-storage-account"></a><span data-ttu-id="e8317-165">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="e8317-165">Create a storage account</span></span>

<span data-ttu-id="e8317-166">Criar uma conta de armazenamento para seu disco personalizado e VMs com [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="e8317-166">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="e8317-167">Todas as máquinas virtuais com discos não gerenciados que você cria com seu toobe de necessidade de disco personalizada no Olá a mesma conta de armazenamento que esse disco.</span><span class="sxs-lookup"><span data-stu-id="e8317-167">Any VMs with unmanaged disks that you create from your custom disk need toobe in hello same storage account as that disk.</span></span> 

<span data-ttu-id="e8317-168">Olá, exemplo a seguir cria uma conta de armazenamento denominada `mystorageaccount` no grupo de recursos de saudação criado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="e8317-168">hello following example creates a storage account named `mystorageaccount` in hello resource group previously created:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

## <a name="list-storage-account-keys"></a><span data-ttu-id="e8317-169">Listar chaves da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="e8317-169">List storage account keys</span></span>
<span data-ttu-id="e8317-170">O Azure gera duas chaves de acesso de 512 bits para cada conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e8317-170">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="e8317-171">Essas chaves de acesso são usadas ao autenticar a conta de armazenamento de toohello, como toocarry operações de gravação.</span><span class="sxs-lookup"><span data-stu-id="e8317-171">These access keys are used when authenticating toohello storage account, such as toocarry out write operations.</span></span> <span data-ttu-id="e8317-172">Leia mais sobre [gerenciando acesso toostorage aqui](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="e8317-172">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="e8317-173">Exibir chaves de acesso de saudação com [lista de chaves de conta de armazenamento az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="e8317-173">You view hello access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="e8317-174">Exibir chaves de acesso Olá Olá conta de armazenamento criada:</span><span class="sxs-lookup"><span data-stu-id="e8317-174">View hello access keys for hello storage account you created:</span></span>

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

<span data-ttu-id="e8317-175">saída de Hello é semelhante a:</span><span class="sxs-lookup"><span data-stu-id="e8317-175">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="e8317-176">Anote `key1` como você o usará toointeract com as próximas etapas Olá sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e8317-176">Make a note of `key1` as you will use it toointeract with your storage account in hello next steps.</span></span>

## <a name="create-a-storage-container"></a><span data-ttu-id="e8317-177">Criar um contêiner de armazenamento</span><span class="sxs-lookup"><span data-stu-id="e8317-177">Create a storage container</span></span>
<span data-ttu-id="e8317-178">Em Olá mesma maneira que você crie diferentes diretórios toologically organizar seu sistema de arquivos local, crie contêineres dentro de um tooorganize de conta de armazenamento seus discos.</span><span class="sxs-lookup"><span data-stu-id="e8317-178">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your disks.</span></span> <span data-ttu-id="e8317-179">Uma conta de armazenamento pode conter qualquer quantidade de contêineres.</span><span class="sxs-lookup"><span data-stu-id="e8317-179">A storage account can contain any number of containers.</span></span> <span data-ttu-id="e8317-180">Crie um contêiner com [az storage container create](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="e8317-180">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="e8317-181">Olá, exemplo a seguir cria um contêiner denominado `mydisks`:</span><span class="sxs-lookup"><span data-stu-id="e8317-181">hello following example creates a container named `mydisks`:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

## <a name="upload-vhd"></a><span data-ttu-id="e8317-182">Carregar o VHD</span><span class="sxs-lookup"><span data-stu-id="e8317-182">Upload VHD</span></span>
<span data-ttu-id="e8317-183">Agora, carregue seu disco personalizado com [az storage blob upload](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="e8317-183">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="e8317-184">Carregue e armazene seu disco personalizado como um blob de páginas.</span><span class="sxs-lookup"><span data-stu-id="e8317-184">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="e8317-185">Especifique sua chave de acesso, o contêiner de saudação criado na etapa anterior hello e, em seguida, Olá disco personalizada do caminho toohello no computador local:</span><span class="sxs-lookup"><span data-stu-id="e8317-185">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

## <a name="create-hello-vm"></a><span data-ttu-id="e8317-186">Criar hello VM</span><span class="sxs-lookup"><span data-stu-id="e8317-186">Create hello VM</span></span>
<span data-ttu-id="e8317-187">toocreate uma VM com discos não gerenciados, especifique o disco de tooyour do URI de saudação (`--image`) com [criar vm az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="e8317-187">toocreate a VM with unmanaged disks, specify hello URI tooyour disk (`--image`) with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="e8317-188">Olá, exemplo a seguir cria uma VM denominada `myVM` usando o disco virtual de saudação carregado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="e8317-188">hello following example creates a VM named `myVM` using hello virtual disk previously uploaded:</span></span>

<span data-ttu-id="e8317-189">Especificar Olá `--image` parâmetro com [criar vm az](/cli/azure/vm#create) toopoint tooyour personalizado disco.</span><span class="sxs-lookup"><span data-stu-id="e8317-189">You specify hello `--image` parameter with [az vm create](/cli/azure/vm#create) toopoint tooyour custom disk.</span></span> <span data-ttu-id="e8317-190">Certifique-se de que `--storage-account` correspondências Olá conta de armazenamento onde o disco personalizado é armazenado.</span><span class="sxs-lookup"><span data-stu-id="e8317-190">Ensure that `--storage-account` matches hello storage account where your custom disk is stored.</span></span> <span data-ttu-id="e8317-191">Você não tem toouse Olá mesmo contêiner como Olá disco personalizada toostore suas VMs.</span><span class="sxs-lookup"><span data-stu-id="e8317-191">You do not have toouse hello same container as hello custom disk toostore your VMs.</span></span> <span data-ttu-id="e8317-192">Fazer toocreate se qualquer contêiner adicional em Olá mesma maneira que Olá etapas anteriores antes de carregar o disco personalizado.</span><span class="sxs-lookup"><span data-stu-id="e8317-192">Make sure toocreate any additional containers in hello same way as hello earlier steps before uploading your custom disk.</span></span>

<span data-ttu-id="e8317-193">Olá, exemplo a seguir cria uma VM denominada `myVM` do disco personalizado:</span><span class="sxs-lookup"><span data-stu-id="e8317-193">hello following example creates a VM named `myVM` from your custom disk:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd \
    --use-unmanaged-disk
```

<span data-ttu-id="e8317-194">Você ainda precisa toospecify ou responder a prompts para, todos os parâmetros adicionais exigidos pelo Olá de Olá **criar vm az** comando, como o nome de usuário e as chaves de SSH.</span><span class="sxs-lookup"><span data-stu-id="e8317-194">You still need toospecify, or answer prompts for, all hello additional parameters required by hello **az vm create** command such as username and SSH keys.</span></span>


## <a name="resource-manager-template"></a><span data-ttu-id="e8317-195">Modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e8317-195">Resource Manager template</span></span>
<span data-ttu-id="e8317-196">Modelos do Gerenciador de recursos do Azure são arquivos de notação JSON (JavaScript Object) que definem o ambiente Olá desejar toobuild.</span><span class="sxs-lookup"><span data-stu-id="e8317-196">Azure Resource Manager templates are JavaScript Object Notation (JSON) files that define hello environment you wish toobuild.</span></span> <span data-ttu-id="e8317-197">modelos de saudação são divididos em toodifferent provedores de recursos, como computação ou rede.</span><span class="sxs-lookup"><span data-stu-id="e8317-197">hello templates are broken down in toodifferent resource providers such as compute or network.</span></span> <span data-ttu-id="e8317-198">Você pode usar os modelos existentes ou escrever seus próprios.</span><span class="sxs-lookup"><span data-stu-id="e8317-198">You can use existing templates or write your own.</span></span> <span data-ttu-id="e8317-199">Saiba mais sobre como [usar o Resource Manager e os modelos](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e8317-199">Read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="e8317-200">Dentro de saudação `Microsoft.Compute/virtualMachines` provedor do seu modelo, você tem um `storageProfile` nó que contém os detalhes de configuração Olá para sua VM.</span><span class="sxs-lookup"><span data-stu-id="e8317-200">Within hello `Microsoft.Compute/virtualMachines` provider of your template, you have a `storageProfile` node that contains hello configuration details for your VM.</span></span> <span data-ttu-id="e8317-201">Olá dois parâmetros principais tooedit são Olá `image` e `vhd` URIs que aponte disco personalizada tooyour e disco virtual da VM seu novo.</span><span class="sxs-lookup"><span data-stu-id="e8317-201">hello two main parameters tooedit are hello `image` and `vhd` URIs that point tooyour custom disk and your new VM's virtual disk.</span></span> <span data-ttu-id="e8317-202">a seguir Olá mostra um exemplo de hello JSON para usar um disco personalizado:</span><span class="sxs-lookup"><span data-stu-id="e8317-202">hello following shows an example of hello JSON for using a custom disk:</span></span>

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

<span data-ttu-id="e8317-203">Você pode usar [este toocreate de modelo existente uma VM por meio de uma imagem personalizada](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) ou leia sobre [criar seus próprios modelos do Azure Resource Manager](../../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e8317-203">You can use [this existing template toocreate a VM from a custom image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) or read about [creating your own Azure Resource Manager templates](../../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 

<span data-ttu-id="e8317-204">Quando você tiver um modelo configurado, usar [criar implantação de grupo az](/cli/azure/group/deployment#create) toocreate suas VMs.</span><span class="sxs-lookup"><span data-stu-id="e8317-204">Once you have a template configured, use [az group deployment create](/cli/azure/group/deployment#create) toocreate your VMs.</span></span> <span data-ttu-id="e8317-205">Especifique Olá URI do seu modelo de JSON com hello `--template-uri` parâmetro:</span><span class="sxs-lookup"><span data-stu-id="e8317-205">Specify hello URI of your JSON template with hello `--template-uri` parameter:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-uri https://uri.to.template/mytemplate.json
```

<span data-ttu-id="e8317-206">Se você tiver um arquivo JSON armazenado localmente no seu computador, você pode usar o hello `--template-file` parâmetro em vez disso:</span><span class="sxs-lookup"><span data-stu-id="e8317-206">If you have a JSON file stored locally on your computer, you can use hello `--template-file` parameter instead:</span></span>

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a><span data-ttu-id="e8317-207">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e8317-207">Next steps</span></span>
<span data-ttu-id="e8317-208">Depois de preparar e carregar seu disco virtual personalizado, leia mais sobre como [usar o Resource Manager e os modelos](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e8317-208">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="e8317-209">Você também pode desejar muito[adicionar um disco de dados](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour novas VMs.</span><span class="sxs-lookup"><span data-stu-id="e8317-209">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="e8317-210">Se você tiver aplicativos em execução em suas VMs que você precisa tooaccess, certifique-se muito[abrir portas e os pontos de extremidade](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e8317-210">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

