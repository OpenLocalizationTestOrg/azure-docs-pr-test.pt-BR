---
title: aaaCreate e carregar um VHD Linux tooAzure | Microsoft Docs
description: "Criar e carregar um Azure disco rígido virtual (VHD) que contém o sistema de operacional Linux hello usando o modelo de implantação clássico Olá"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8058ff98-db03-4309-9bf4-69842bd64dd4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: iainfou
ms.openlocfilehash: 77b01316386c4a6eb68c129fa68d42f0a8996edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-uploading-a-virtual-hard-disk-that-contains-hello-linux-operating-system"></a><span data-ttu-id="ddd93-103">Criando e carregando um disco rígido Virtual que contém Olá o sistema operacional Linux</span><span class="sxs-lookup"><span data-stu-id="ddd93-103">Creating and Uploading a Virtual Hard Disk that Contains hello Linux Operating System</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="ddd93-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ddd93-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ddd93-105">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="ddd93-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="ddd93-106">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="ddd93-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="ddd93-107">Você também pode [carregar uma imagem de disco personalizada usando o Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ddd93-107">You can also [upload a custom disk image using Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="ddd93-108">Este artigo mostra como toocreate e carregar um disco rígido virtual (VHD) para que você pode usá-lo como sua própria imagem toocreate as máquinas virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="ddd93-108">This article shows you how toocreate and upload a virtual hard disk (VHD) so you can use it as your own image toocreate virtual machines in Azure.</span></span> <span data-ttu-id="ddd93-109">Saiba como tooprepare hello, você pode usar toocreate várias máquinas virtuais com base em imagem.</span><span class="sxs-lookup"><span data-stu-id="ddd93-109">Learn how tooprepare hello operating system so you can use it toocreate multiple virtual machines based on that image.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="ddd93-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ddd93-110">Prerequisites</span></span>
<span data-ttu-id="ddd93-111">Este artigo pressupõe que você tenha Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="ddd93-111">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="ddd93-112">**Sistema operacional Linux instalado em um arquivo. vhd** -você instalou um [distribuição aprovadas Azure Linux](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (ou consulte [informações para distribuições não aprovadas](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) disco virtual tooa no formato VHD hello.</span><span class="sxs-lookup"><span data-stu-id="ddd93-112">**Linux operating system installed in a .vhd file** - You have installed an [Azure-endorsed Linux distribution](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtual disk in hello VHD format.</span></span> <span data-ttu-id="ddd93-113">Várias ferramentas existem toocreate uma VM e o VHD:</span><span class="sxs-lookup"><span data-stu-id="ddd93-113">Multiple tools exist toocreate a VM and VHD:</span></span>
  * <span data-ttu-id="ddd93-114">Instalar e configurar [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) ou [KVM](http://www.linux-kvm.org/page/RunningKVM), tomando cuidado toouse VHD como seu formato de imagem.</span><span class="sxs-lookup"><span data-stu-id="ddd93-114">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care toouse VHD as your image format.</span></span> <span data-ttu-id="ddd93-115">Se necessário, você pode [converter uma imagem](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) usando `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="ddd93-115">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="ddd93-116">Também pode usar o Hyper-V [no Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) ou [no Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="ddd93-116">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="ddd93-117">Não há suporte para o formato VHDX mais recente de saudação no Azure.</span><span class="sxs-lookup"><span data-stu-id="ddd93-117">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="ddd93-118">Quando você cria uma máquina virtual, especifique o VHD como formato de saudação.</span><span class="sxs-lookup"><span data-stu-id="ddd93-118">When you create a VM, specify VHD as hello format.</span></span> <span data-ttu-id="ddd93-119">Se necessário, você pode converter tooVHD de discos VHDX usando [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) ou hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ddd93-119">If needed, you can convert VHDX disks tooVHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or hello [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="ddd93-120">Além disso, Azure não oferece suporte Carregando VHDs dinâmicos, portanto, você precisa tooconvert toostatic esses discos VHDs antes de carregar.</span><span class="sxs-lookup"><span data-stu-id="ddd93-120">Further, Azure does not support uploading dynamic VHDs, so you need tooconvert such disks toostatic VHDs before uploading.</span></span> <span data-ttu-id="ddd93-121">Você pode usar ferramentas como [utilitários de VHD do Azure para ir](https://github.com/Microsoft/azure-vhd-utils-for-go) discos dinâmicos de tooconvert durante o processo de saudação de carregamento de tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ddd93-121">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamic disks during hello process of uploading tooAzure.</span></span>

* <span data-ttu-id="ddd93-122">**Interface de linha de comando do Azure** -Olá de instalação mais recente [Interface de linha de comando do Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) Olá tooupload VHD.</span><span class="sxs-lookup"><span data-stu-id="ddd93-122">**Azure Command-line Interface** - Install hello latest [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooupload hello VHD.</span></span>

<span data-ttu-id="ddd93-123"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="ddd93-123"><a id="prepimage"> </a></span></span>

## <a name="step-1-prepare-hello-image-toobe-uploaded"></a><span data-ttu-id="ddd93-124">Etapa 1: Preparar Olá imagem toobe carregado</span><span class="sxs-lookup"><span data-stu-id="ddd93-124">Step 1: Prepare hello image toobe uploaded</span></span>
<span data-ttu-id="ddd93-125">O Azure dá suporte a várias distribuições do Linux (consulte [Distribuições endossadas](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="ddd93-125">Azure supports various Linux distributions (see [Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="ddd93-126">Olá artigos a seguir orientam você na como tooprepare Olá várias distribuições do Linux com suporte no Azure.</span><span class="sxs-lookup"><span data-stu-id="ddd93-126">hello following articles guide you through how tooprepare hello various Linux distributions that are supported on Azure.</span></span> <span data-ttu-id="ddd93-127">Depois de concluir as etapas de Olá Olá guias a seguir, volte aqui uma vez que um arquivo VHD que está pronto tooupload tooAzure:</span><span class="sxs-lookup"><span data-stu-id="ddd93-127">After you complete hello steps in hello following guides, come back here once you have a VHD file that is ready tooupload tooAzure:</span></span>

* <span data-ttu-id="ddd93-128">**[Distribuições com base em CentOS](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="ddd93-128">**[CentOS-based Distributions](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="ddd93-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="ddd93-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="ddd93-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="ddd93-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="ddd93-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="ddd93-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="ddd93-132">**[SLES & openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="ddd93-132">**[SLES & openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="ddd93-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="ddd93-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="ddd93-134">**[Outros — Distribuições não endossadas](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="ddd93-134">**[Other - Non-Endorsed Distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

> [!NOTE]
> <span data-ttu-id="ddd93-135">Olá SLA da plataforma Windows Azure se aplica a máquinas toovirtual executando Olá sistema operacional somente quando uma saudação aprovados distribuições do Linux é usado com os detalhes de configuração Olá conforme especificado em 'Versões com suporte' em [Linux em distribuições Azure-Endorsed ](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ddd93-135">hello Azure platform SLA applies toovirtual machines running hello Linux OS only when one of hello endorsed distributions is used with hello configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="ddd93-136">Todas as distribuições do Linux na Galeria de imagens do Azure de saudação são endossadas distribuições com a configuração solicitada hello.</span><span class="sxs-lookup"><span data-stu-id="ddd93-136">All Linux distributions in hello Azure image gallery are endorsed distributions with hello required configuration.</span></span>
> 
> 

<span data-ttu-id="ddd93-137">Consulte também Olá  **[notas de instalação Linux](../create-upload-generic.md#general-linux-installation-notes)**  mais geral dicas sobre como preparar imagens do Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="ddd93-137">Also see hello **[Linux Installation Notes](../create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

<span data-ttu-id="ddd93-138"><a id="connect"> </a></span><span class="sxs-lookup"><span data-stu-id="ddd93-138"><a id="connect"> </a></span></span>

## <a name="step-2-prepare-hello-connection-tooazure"></a><span data-ttu-id="ddd93-139">Etapa 2: Preparar Olá conexão tooAzure</span><span class="sxs-lookup"><span data-stu-id="ddd93-139">Step 2: Prepare hello connection tooAzure</span></span>
<span data-ttu-id="ddd93-140">Verifique se está usando Olá CLI do Azure no modelo de implantação clássico hello (`azure config mode asm`), em seguida, faça logon no tooyour conta:</span><span class="sxs-lookup"><span data-stu-id="ddd93-140">Make sure you are using hello Azure CLI in hello classic deployment model (`azure config mode asm`), then log in tooyour account:</span></span>

```azurecli
azure login
```


<span data-ttu-id="ddd93-141"><a id="upload"> </a></span><span class="sxs-lookup"><span data-stu-id="ddd93-141"><a id="upload"> </a></span></span>

## <a name="step-3-upload-hello-image-tooazure"></a><span data-ttu-id="ddd93-142">Etapa 3: Carregar Olá imagem tooAzure</span><span class="sxs-lookup"><span data-stu-id="ddd93-142">Step 3: Upload hello image tooAzure</span></span>
<span data-ttu-id="ddd93-143">É necessário um tooupload de conta de armazenamento para seu arquivo VHD para.</span><span class="sxs-lookup"><span data-stu-id="ddd93-143">You need a storage account tooupload your VHD file to.</span></span> <span data-ttu-id="ddd93-144">Você pode escolher uma conta de armazenamento existente ou [criar uma nova](../../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="ddd93-144">You can either pick an existing storage account or [create a new one](../../../storage/common/storage-create-storage-account.md).</span></span>

<span data-ttu-id="ddd93-145">Use imagem de Olá Olá CLI do Azure tooupload usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="ddd93-145">Use hello Azure CLI tooupload hello image by using hello following command:</span></span>

```azurecli
azure vm image create <ImageName> `
    --blob-url <BlobStorageURL>/<YourImagesFolder>/<VHDName> `
    --os Linux <PathToVHDFile>
```

<span data-ttu-id="ddd93-146">No exemplo anterior de saudação:</span><span class="sxs-lookup"><span data-stu-id="ddd93-146">In hello previous example:</span></span>

* <span data-ttu-id="ddd93-147">**BlobStorageURL** é URL Olá Olá conta de armazenamento planejar toouse</span><span class="sxs-lookup"><span data-stu-id="ddd93-147">**BlobStorageURL** is hello URL for hello storage account you plan toouse</span></span>
* <span data-ttu-id="ddd93-148">**YourImagesFolder** é o contêiner Olá no armazenamento de blob onde você deseja toostore suas imagens</span><span class="sxs-lookup"><span data-stu-id="ddd93-148">**YourImagesFolder** is hello container within blob storage where you want toostore your images</span></span>
* <span data-ttu-id="ddd93-149">**VHDName** é Olá rótulo que aparece no portal tooidentify saudação do disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="ddd93-149">**VHDName** is hello label that appears in portal tooidentify hello virtual hard disk.</span></span>
* <span data-ttu-id="ddd93-150">**PathToVHDFile** é o caminho completo do hello e nome do arquivo. vhd de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="ddd93-150">**PathToVHDFile** is hello full path and name of hello .vhd file on your machine.</span></span>

<span data-ttu-id="ddd93-151">saudação de comando a seguir mostra um exemplo completo:</span><span class="sxs-lookup"><span data-stu-id="ddd93-151">hello following command shows a complete example:</span></span>

```azurecli
azure vm image create myImage `
    --blob-url https://mystorage.blob.core.windows.net/vhds/myimage.vhd `
    --os Linux /home/ahmet/myimage.vhd
```

## <a name="step-4-create-a-vm-from-hello-image"></a><span data-ttu-id="ddd93-152">Etapa 4: Criar uma VM da imagem Olá</span><span class="sxs-lookup"><span data-stu-id="ddd93-152">Step 4: Create a VM from hello image</span></span>
<span data-ttu-id="ddd93-153">Criar uma VM usando `azure vm create` em Olá mesma forma que uma VM regular.</span><span class="sxs-lookup"><span data-stu-id="ddd93-153">You create a VM using `azure vm create` in hello same way as a regular VM.</span></span> <span data-ttu-id="ddd93-154">Especifique o nome de saudação você deu a imagem na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="ddd93-154">Specify hello name you gave your image in hello previous step.</span></span> <span data-ttu-id="ddd93-155">Saudação de exemplo a seguir, usamos Olá **myImage** nome de imagem fornecido na etapa anterior hello:</span><span class="sxs-lookup"><span data-stu-id="ddd93-155">In hello following example, we use hello **myImage** image name given in hello previous step:</span></span>

```azurecli
azure vm create --userName ops --password P@ssw0rd! --vm-size Small --ssh `
    --location "West US" "myDeployedVM" myImage
```

<span data-ttu-id="ddd93-156">toocreate suas próprias VMs, fornecer seu próprio nome de usuário + senha local, nome DNS e nome da imagem.</span><span class="sxs-lookup"><span data-stu-id="ddd93-156">toocreate your own VMs, provide your own username + password, location, DNS name, and image name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ddd93-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ddd93-157">Next steps</span></span>
<span data-ttu-id="ddd93-158">Para obter mais informações, consulte [referência da CLI do Azure para o modelo de implantação clássico do Azure Olá](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="ddd93-158">For more information, see [Azure CLI reference for hello Azure classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

[Step 1: Prepare hello image toobe uploaded]:#prepimage
[Step 2: Prepare hello connection tooAzure]:#connect
[Step 3: Upload hello image tooAzure]:#upload
