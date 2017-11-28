---
title: aaaUpload ou copiar uma VM do Linux personalizado com o Azure CLI 2.0 | Microsoft Docs
description: "Carregar ou copiar uma máquina virtual personalizada usando o modelo de implantação do Gerenciador de recursos de saudação e hello 2.0 do CLI do Azure"
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
ms.date: 07/06/2017
ms.author: cynthn
ms.openlocfilehash: 79af897120a6ba7f4a427ba6c7d0c31b7b870bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a><span data-ttu-id="a34db-103">Criar uma VM do Linux do disco personalizado com hello 2.0 do CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="a34db-103">Create a Linux VM from custom disk with hello Azure CLI 2.0</span></span>

<!-- rename toocreate-vm-specialized -->

<span data-ttu-id="a34db-104">Este artigo mostra como tooupload um disco rígido virtual (VHD) personalizado ou copie um um VHD existente no Azure e criar novas máquinas de virtuais de Linux (VMs) do disco de saudação personalizada.</span><span class="sxs-lookup"><span data-stu-id="a34db-104">This article shows you how tooupload a customized virtual hard disk (VHD) or copy a an existing VHD in Azure and create new Linux virtual machines (VMs) from hello custom disk.</span></span> <span data-ttu-id="a34db-105">Você pode instalar e configurar um requisitos de tooyour de distribuição do Linux e, em seguida, usar esse VHD tooquickly criar uma nova máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="a34db-105">You can install and configure a Linux distro tooyour requirements and then use that VHD tooquickly create a new Azure virtual machine.</span></span>

<span data-ttu-id="a34db-106">Se você quiser toocreate várias VMs do disco personalizado, você deve criar uma imagem da VM ou VHD.</span><span class="sxs-lookup"><span data-stu-id="a34db-106">If you want toocreate multiple VMs from your customized disk, you should create an image from your VM or VHD.</span></span> <span data-ttu-id="a34db-107">Para obter mais informações, consulte [criar uma imagem personalizada de uma VM do Azure usando Olá CLI](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="a34db-107">For more information, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md).</span></span>

<span data-ttu-id="a34db-108">Você tem duas opções:</span><span class="sxs-lookup"><span data-stu-id="a34db-108">You have two options:</span></span>
* [<span data-ttu-id="a34db-109">Carregar um VHD</span><span class="sxs-lookup"><span data-stu-id="a34db-109">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="a34db-110">Copiar uma VM existente do Azure</span><span class="sxs-lookup"><span data-stu-id="a34db-110">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

## <a name="quick-commands"></a><span data-ttu-id="a34db-111">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="a34db-111">Quick commands</span></span>

<span data-ttu-id="a34db-112">Ao criar uma nova VM usando [criar vm az](/cli/azure/vm#create) de um disco especializado ou personalizado você **anexar** disco hello (– anexar-disco do SO) em vez de especificar uma imagem personalizada ou marketplace (-imagem).</span><span class="sxs-lookup"><span data-stu-id="a34db-112">When creating a new VM using [az vm create](/cli/azure/vm#create) from a customized or specialized disk you **attach** hello disk (--attach-os-disk) instead of specifying a custom or marketplace image (--image).</span></span> <span data-ttu-id="a34db-113">Olá, exemplo a seguir cria uma VM denominada *myVM* usando Olá gerenciado disco chamado *myManagedDisk* criado a partir de seu VHD personalizado:</span><span class="sxs-lookup"><span data-stu-id="a34db-113">hello following example creates a VM named *myVM* using hello managed disk named *myManagedDisk* created from your customized VHD:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --location eastus --name myVM \
   --os-type linux --attach-os-disk myManagedDisk
```

## <a name="requirements"></a><span data-ttu-id="a34db-114">Requisitos</span><span class="sxs-lookup"><span data-stu-id="a34db-114">Requirements</span></span>
<span data-ttu-id="a34db-115">Olá toocomplete seguintes etapas, você precisa:</span><span class="sxs-lookup"><span data-stu-id="a34db-115">toocomplete hello following steps, you need:</span></span>

* <span data-ttu-id="a34db-116">Uma máquina virtual Linux que foi preparada para uso no Azure.</span><span class="sxs-lookup"><span data-stu-id="a34db-116">A Linux virtual machine that has been prepared for use in Azure.</span></span> <span data-ttu-id="a34db-117">Olá [preparar Olá VM](#prepare-the-vm) este artigo aborda como distribuição de toofind informações específicas sobre como instalar hello Azure Linux Agent (waagent) que é necessária para Olá VM toowork corretamente no Azure e você toobe capaz de tooconnect tooit usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="a34db-117">hello [Prepare hello VM](#prepare-the-vm) section of this article covers how toofind distro specific information on installing hello Azure Linux Agent (waagent) which is required for hello VM toowork properly in Azure and for you toobe able tooconnect tooit using SSH.</span></span>
* <span data-ttu-id="a34db-118">arquivo VHD de saudação de uma já existente [distribuição aprovadas Azure Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (ou consulte [informações para distribuições não aprovadas](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa o disco virtual no formato VHD hello.</span><span class="sxs-lookup"><span data-stu-id="a34db-118">hello VHD file from an existing [Azure-endorsed Linux distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="a34db-119">Várias ferramentas existem toocreate uma VM e o VHD:</span><span class="sxs-lookup"><span data-stu-id="a34db-119">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="a34db-120">Instalar e configurar [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) ou [KVM](http://www.linux-kvm.org/page/RunningKVM), tomando cuidado toouse VHD como seu formato de imagem.</span><span class="sxs-lookup"><span data-stu-id="a34db-120">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="a34db-121">Se necessário, você pode [converter uma imagem](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) usando **qemu-img convert**.</span><span class="sxs-lookup"><span data-stu-id="a34db-121">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using **qemu-img convert**.</span></span>
  * <span data-ttu-id="a34db-122">Também pode usar o Hyper-V [no Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) ou [no Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="a34db-122">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="a34db-123">Não há suporte para o formato VHDX mais recente de saudação no Azure.</span><span class="sxs-lookup"><span data-stu-id="a34db-123">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="a34db-124">Quando você cria uma máquina virtual, especifique o VHD como formato de saudação.</span><span class="sxs-lookup"><span data-stu-id="a34db-124">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="a34db-125">Se necessário, você pode converter tooVHD de discos VHDX usando [qemu img converter](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) ou hello [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a34db-125">If needed, you can convert VHDX disks tooVHD using [qemu-img convert](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="a34db-126">Além disso, Azure não oferece suporte Carregando VHDs dinâmicos, portanto, você precisa tooconvert toostatic esses discos VHDs antes de carregar.</span><span class="sxs-lookup"><span data-stu-id="a34db-126">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="a34db-127">Você pode usar ferramentas como [utilitários de VHD do Azure para ir](https://github.com/Microsoft/azure-vhd-utils-for-go) discos dinâmicos de tooconvert durante o processo de saudação de carregamento de tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a34db-127">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>
> 
> 


* <span data-ttu-id="a34db-128">Certifique-se de que você tenha mais recente Olá [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e conectado através de conta do Azure tooan [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="a34db-128">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="a34db-129">Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="a34db-129">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="a34db-130">Exemplos de nomes de parâmetro incluem *myResourceGroup*, *mystorageaccount* e *mydisks*.</span><span class="sxs-lookup"><span data-stu-id="a34db-130">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *mydisks*.</span></span>

<span data-ttu-id="a34db-131"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="a34db-131"><a id="prepimage"> </a></span></span>

## <a name="prepare-hello-vm"></a><span data-ttu-id="a34db-132">Preparar Olá VM</span><span class="sxs-lookup"><span data-stu-id="a34db-132">Prepare hello VM</span></span>

<span data-ttu-id="a34db-133">O Azure dá suporte a várias distribuições do Linux (consulte [Distribuições endossadas](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="a34db-133">Azure supports various Linux distributions (see [Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="a34db-134">Olá artigos a seguir orientam você pelo como tooprepare Olá várias distribuições do Linux com suporte no Azure.</span><span class="sxs-lookup"><span data-stu-id="a34db-134">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure:</span></span>

* [<span data-ttu-id="a34db-135">Distribuições com base em CentOS</span><span class="sxs-lookup"><span data-stu-id="a34db-135">CentOS-based Distributions</span></span>](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="a34db-136">Debian Linux</span><span class="sxs-lookup"><span data-stu-id="a34db-136">Debian Linux</span></span>](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="a34db-137">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="a34db-137">Oracle Linux</span></span>](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="a34db-138">Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="a34db-138">Red Hat Enterprise Linux</span></span>](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="a34db-139">SLES e openSUSE</span><span class="sxs-lookup"><span data-stu-id="a34db-139">SLES & openSUSE</span></span>](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="a34db-140">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="a34db-140">Ubuntu</span></span>](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="a34db-141">Outro – distribuições não endossadas</span><span class="sxs-lookup"><span data-stu-id="a34db-141">Other - Non-Endorsed Distributions</span></span>](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="a34db-142">Consulte também Olá [notas de instalação Linux](create-upload-generic.md#general-linux-installation-notes) mais geral dicas sobre como preparar imagens do Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="a34db-142">Also see hello [Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more general tips on preparing Linux images for Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="a34db-143">Olá [plataforma Windows Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) aplica-se tooVMs executando o Linux somente quando uma saudação aprovados distribuições é usado com os detalhes de configuração Olá conforme especificado em 'Versões com suporte' [Linux no Azure aprovadas Distribuições](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a34db-143">hello [Azure platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applies tooVMs running Linux only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

## <a name="option-1-upload-a-vhd"></a><span data-ttu-id="a34db-144">Opção 1: Carregar um VHD</span><span class="sxs-lookup"><span data-stu-id="a34db-144">Option 1: Upload a VHD</span></span>

<span data-ttu-id="a34db-145">Você pode carregar um VHD personalizado que esteja em execução em um computador local ou que você tenha exportado de outra nuvem.</span><span class="sxs-lookup"><span data-stu-id="a34db-145">You can upload a customized VHD that you have running on a local machine or that you exported from another cloud.</span></span> <span data-ttu-id="a34db-146">toouse Olá VHD toocreate uma nova VM do Azure, você precisa de armazenamento de tooa do tooupload Olá VHD da conta e criar um disco gerenciado de saudação VHD.</span><span class="sxs-lookup"><span data-stu-id="a34db-146">toouse hello VHD toocreate a new Azure VM, you need tooupload hello VHD tooa storage account and create a managed disk from hello VHD.</span></span> 

### <a name="create-a-resource-group"></a><span data-ttu-id="a34db-147">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="a34db-147">Create a resource group</span></span>

<span data-ttu-id="a34db-148">Antes de carregar o disco personalizado e criar máquinas virtuais, é necessário primeiro toocreate um grupo de recursos com [criar grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="a34db-148">Before uploading your custom disk and creating VMs, you first need toocreate a resource group with [az group create](/cli/azure/group#create).</span></span>

<span data-ttu-id="a34db-149">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local: [visão geral de discos gerenciado do Azure](../windows/managed-disks-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a34db-149">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location: [Azure Managed Disks overview](../windows/managed-disks-overview.md)</span></span>
```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

### <a name="create-a-storage-account"></a><span data-ttu-id="a34db-150">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="a34db-150">Create a storage account</span></span>

<span data-ttu-id="a34db-151">Criar uma conta de armazenamento para seu disco personalizado e VMs com [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="a34db-151">Create a storage account for your custom disk and VMs with [az storage account create](/cli/azure/storage/account#create).</span></span> 

<span data-ttu-id="a34db-152">Olá, exemplo a seguir cria uma conta de armazenamento denominada *mystorageaccount* no grupo de recursos de saudação criado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="a34db-152">hello following example creates a storage account named *mystorageaccount* in hello resource group previously created:</span></span>

```azurecli
az storage account create \
    --resource-group myResourceGroup \
    --location eastus \
    --name mystorageaccount \
    --kind Storage \
    --sku Standard_LRS
```

### <a name="list-storage-account-keys"></a><span data-ttu-id="a34db-153">Listar chaves da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="a34db-153">List storage account keys</span></span>
<span data-ttu-id="a34db-154">O Azure gera duas chaves de acesso de 512 bits para cada conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a34db-154">Azure generates two 512-bit access keys for each storage account.</span></span> <span data-ttu-id="a34db-155">Essas chaves de acesso são usadas ao autenticar a conta de armazenamento de toohello, como realizar operações de gravação.</span><span class="sxs-lookup"><span data-stu-id="a34db-155">These access keys are used when authenticating toohello storage account, like carrying out write operations.</span></span> <span data-ttu-id="a34db-156">Leia mais sobre [gerenciando acesso toostorage aqui](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="a34db-156">Read more about [managing access toostorage here](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span> <span data-ttu-id="a34db-157">Exibir chaves de acesso de saudação com [lista de chaves de conta de armazenamento az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="a34db-157">You view hello access keys with [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span>

<span data-ttu-id="a34db-158">Exibir chaves de acesso Olá Olá conta de armazenamento criada:</span><span class="sxs-lookup"><span data-stu-id="a34db-158">View hello access keys for hello storage account you created:</span></span>

```azurecli
az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount
```

<span data-ttu-id="a34db-159">saída de Hello é semelhante a:</span><span class="sxs-lookup"><span data-stu-id="a34db-159">hello output is similar to:</span></span>

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
<span data-ttu-id="a34db-160">Anote **key1** como você o usará toointeract com as próximas etapas Olá sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a34db-160">Make a note of **key1** as you will use it toointeract with your storage account in hello next steps.</span></span>

### <a name="create-a-storage-container"></a><span data-ttu-id="a34db-161">Criar um contêiner de armazenamento</span><span class="sxs-lookup"><span data-stu-id="a34db-161">Create a storage container</span></span>
<span data-ttu-id="a34db-162">Em Olá mesma maneira que você crie diferentes diretórios toologically organizar seu sistema de arquivos local, crie contêineres dentro de um tooorganize de conta de armazenamento seus discos.</span><span class="sxs-lookup"><span data-stu-id="a34db-162">In hello same way that you create different directories toologically organize your local file system, you create containers within a storage account tooorganize your disks.</span></span> <span data-ttu-id="a34db-163">Uma conta de armazenamento pode conter qualquer quantidade de contêineres.</span><span class="sxs-lookup"><span data-stu-id="a34db-163">A storage account can contain any number of containers.</span></span> <span data-ttu-id="a34db-164">Crie um contêiner com [az storage container create](/cli/azure/storage/container#create).</span><span class="sxs-lookup"><span data-stu-id="a34db-164">Create a container with [az storage container create](/cli/azure/storage/container#create).</span></span>

<span data-ttu-id="a34db-165">Olá, exemplo a seguir cria um contêiner denominado *mydisks*:</span><span class="sxs-lookup"><span data-stu-id="a34db-165">hello following example creates a container named *mydisks*:</span></span>

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

### <a name="upload-hello-vhd"></a><span data-ttu-id="a34db-166">Carregar Olá VHD</span><span class="sxs-lookup"><span data-stu-id="a34db-166">Upload hello VHD</span></span>
<span data-ttu-id="a34db-167">Agora, carregue seu disco personalizado com [az storage blob upload](/cli/azure/storage/blob#upload).</span><span class="sxs-lookup"><span data-stu-id="a34db-167">Now upload your custom disk with [az storage blob upload](/cli/azure/storage/blob#upload).</span></span> <span data-ttu-id="a34db-168">Carregue e armazene seu disco personalizado como um blob de páginas.</span><span class="sxs-lookup"><span data-stu-id="a34db-168">You upload and store your custom disk as a page blob.</span></span>

<span data-ttu-id="a34db-169">Especifique sua chave de acesso, o contêiner de saudação criado na etapa anterior hello e, em seguida, Olá disco personalizada do caminho toohello no computador local:</span><span class="sxs-lookup"><span data-stu-id="a34db-169">Specify your access key, hello container you created in hello previous step, and then hello path toohello custom disk on your local computer:</span></span>

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 \
    --container-name mydisks \
    --type page \
    --file /path/to/disk/mydisk.vhd \
    --name myDisk.vhd
```
<span data-ttu-id="a34db-170">Carregando Olá VHD pode demorar um pouco.</span><span class="sxs-lookup"><span data-stu-id="a34db-170">Uploading hello VHD may take a while.</span></span>

### <a name="create-a-managed-disk"></a><span data-ttu-id="a34db-171">Criar um disco gerenciado</span><span class="sxs-lookup"><span data-stu-id="a34db-171">Create a managed disk</span></span>


<span data-ttu-id="a34db-172">Criar um disco gerenciado de saudação VHD usando [criar disco az](/cli/azure/disk#create).</span><span class="sxs-lookup"><span data-stu-id="a34db-172">Create a managed disk from hello VHD using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="a34db-173">Olá, exemplo a seguir cria um disco gerenciado chamado *myManagedDisk* de saudação VHD carregado tooyour conta de armazenamento e contêiner:</span><span class="sxs-lookup"><span data-stu-id="a34db-173">hello following example creates a managed disk named *myManagedDisk* from hello VHD you uploaded tooyour named storage account and container:</span></span>

```azurecli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```
## <a name="option-2-copy-an-existing-vm"></a><span data-ttu-id="a34db-174">Opção 2: Copiar uma VM existente</span><span class="sxs-lookup"><span data-stu-id="a34db-174">Option 2: Copy an existing VM</span></span>

<span data-ttu-id="a34db-175">Você também pode criar hello VM personalizado no Azure e, em seguida, copiar o disco de saudação SO e anexá-lo tooa nova VM toocreate outra cópia.</span><span class="sxs-lookup"><span data-stu-id="a34db-175">You can also create hello customized VM in Azure and then copy hello OS disk and attach it tooa new VM toocreate another copy.</span></span> <span data-ttu-id="a34db-176">Isso é bom para teste, mas se você quiser toouse uma VM do Azure existente como modelo Olá para várias novas VMs, você realmente deve criar um **imagem** em vez disso.</span><span class="sxs-lookup"><span data-stu-id="a34db-176">This is fine for testing, but if you want toouse an existing Azure VM as hello model for multiple new VMs, you really should create an **image** instead.</span></span> <span data-ttu-id="a34db-177">Para obter mais informações sobre como criar uma imagem de uma VM existente do Azure, consulte [criar uma imagem personalizada de uma VM do Azure usando Olá CLI](tutorial-custom-images.md)</span><span class="sxs-lookup"><span data-stu-id="a34db-177">For more information about creating an image from an existing Azure VM, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md)</span></span>

### <a name="create-a-snapshot"></a><span data-ttu-id="a34db-178">Criar um instantâneo</span><span class="sxs-lookup"><span data-stu-id="a34db-178">Create a snapshot</span></span>

<span data-ttu-id="a34db-179">Este exemplo cria um instantâneo de uma VM denominada *myVM* no grupo de recursos *myResourceGroup* e cria um instantâneo denominado *osDiskSnapshot*.</span><span class="sxs-lookup"><span data-stu-id="a34db-179">This example creates a snapshot of a VM named *myVM* in resource group *myResourceGroup* and creates a snapshot named *osDiskSnapshot*.</span></span>

```azure-cli
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create \
    -g myResourceGroup \
    --source "$osDiskId" \
    --name osDiskSnapshot
```
###  <a name="create-hello-managed-disk"></a><span data-ttu-id="a34db-180">Criar disco gerenciado Olá</span><span class="sxs-lookup"><span data-stu-id="a34db-180">Create hello managed disk</span></span>

<span data-ttu-id="a34db-181">Crie um novo disco gerenciado de instantâneo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a34db-181">Create a new managed disk from hello snapshot.</span></span>

<span data-ttu-id="a34db-182">Obter ID de saudação do instantâneo hello.</span><span class="sxs-lookup"><span data-stu-id="a34db-182">Get hello ID of hello snapshot.</span></span> <span data-ttu-id="a34db-183">Neste exemplo, chamado instantâneo Olá *osDiskSnapshot* e em Olá *myResourceGroup* grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a34db-183">In this example, hello snapshot is named *osDiskSnapshot* and it is in hello *myResourceGroup* resource group.</span></span>

```azure-cli
snapshotId=$(az snapshot show --name osDiskSnapshot --resource-group myResourceGroup --query [id] -o tsv)
```

<span data-ttu-id="a34db-184">Crie disco de saudação gerenciado.</span><span class="sxs-lookup"><span data-stu-id="a34db-184">Create hello managed disk.</span></span> <span data-ttu-id="a34db-185">Neste exemplo, vamos criar um disco gerenciado chamado *myManagedDisk* com base em nosso instantâneo, que tem um tamanho de 128 GB no armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="a34db-185">In this example, we will create a managed disk named *myManagedDisk* from our snapshot, that is 128GB in size in standard storage.</span></span>

```azure-cli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
    --sku Standard_LRS \
    --size-gb 128 \
    --source $snapshotId
```

## <a name="create-hello-vm"></a><span data-ttu-id="a34db-186">Criar hello VM</span><span class="sxs-lookup"><span data-stu-id="a34db-186">Create hello VM</span></span>

<span data-ttu-id="a34db-187">Agora, crie a VM com [criar vm az](/cli/azure/vm#create) e anexar (– anexar-disco do SO) Olá gerenciados disco como disco Olá sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="a34db-187">Now, create your VM with [az vm create](/cli/azure/vm#create) and attach (--attach-os-disk) hello managed disk as hello OS disk.</span></span> <span data-ttu-id="a34db-188">Olá, exemplo a seguir cria uma VM denominada *myNewVM* usando Olá gerenciado disco criado a partir de seu VHD carregado:</span><span class="sxs-lookup"><span data-stu-id="a34db-188">hello following example creates a VM named *myNewVM* using hello managed disk created from your uploaded VHD:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNewVM \
    --os-type linux \
    --attach-os-disk myManagedDisk
```

<span data-ttu-id="a34db-189">Você deve ser capaz de tooSSH em Olá VM usando credenciais de saudação do VM de origem hello.</span><span class="sxs-lookup"><span data-stu-id="a34db-189">You should be able tooSSH into hello VM using hello credentials from hello source VM.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a34db-190">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a34db-190">Next steps</span></span>
<span data-ttu-id="a34db-191">Depois de preparar e carregar seu disco virtual personalizado, leia mais sobre como [usar o Resource Manager e os modelos](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a34db-191">After you have prepared and uploaded your custom virtual disk, you can read more about [using Resource Manager and templates](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="a34db-192">Você também pode desejar muito[adicionar um disco de dados](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour novas VMs.</span><span class="sxs-lookup"><span data-stu-id="a34db-192">You may also want too[add a data disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour new VMs.</span></span> <span data-ttu-id="a34db-193">Se você tiver aplicativos em execução em suas VMs que você precisa tooaccess, certifique-se muito[abrir portas e os pontos de extremidade](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a34db-193">If you have applications running on your VMs that you need tooaccess, be sure too[open ports and endpoints](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

