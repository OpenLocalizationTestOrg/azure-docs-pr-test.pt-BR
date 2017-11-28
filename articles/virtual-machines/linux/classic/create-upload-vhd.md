---
title: Criar e carregar um VHD Linux para o Azure | Microsoft Docs
description: "Crie e carregue um VHD (disco rígido virtual) do Azure que contém o sistema operacional Linux usando o modelo de implantação Clássico"
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
ms.openlocfilehash: 23c30c954875598ce3e01db137b0ef8cda9779f4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="creating-and-uploading-a-virtual-hard-disk-that-contains-the-linux-operating-system"></a><span data-ttu-id="5b8b1-103">Criando e carregando um disco rígido virtual que contém o sistema operacional Linux</span><span class="sxs-lookup"><span data-stu-id="5b8b1-103">Creating and Uploading a Virtual Hard Disk that Contains the Linux Operating System</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="5b8b1-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="5b8b1-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="5b8b1-105">Este artigo aborda o uso do modelo de implantação Clássica.</span><span class="sxs-lookup"><span data-stu-id="5b8b1-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="5b8b1-106">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="5b8b1-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="5b8b1-107">Você também pode [carregar uma imagem de disco personalizada usando o Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5b8b1-107">You can also [upload a custom disk image using Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="5b8b1-108">Esse artigo mostra como carregar um disco rígido virtual (VHD) para que você o use como sua própria imagem para criar outras máquinas virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="5b8b1-108">This article shows you how to create and upload a virtual hard disk (VHD) so you can use it as your own image to create virtual machines in Azure.</span></span> <span data-ttu-id="5b8b1-109">Saiba como preparar o sistema operacional para que você o use para criar outras máquinas virtuais com base nessa imagem.</span><span class="sxs-lookup"><span data-stu-id="5b8b1-109">Learn how to prepare the operating system so you can use it to create multiple virtual machines based on that image.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="5b8b1-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5b8b1-110">Prerequisites</span></span>
<span data-ttu-id="5b8b1-111">Este artigo pressupõe que você tenha os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="5b8b1-111">This article assumes that you have the following items:</span></span>

* <span data-ttu-id="5b8b1-112">**Sistema operacional Linux instalado em um arquivo .vhd**: você instalou uma [distribuição Linux endossada pelo Azure](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (ou consulte as [informações para distribuições não endossadas](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) em um disco virtual no formato VHD.</span><span class="sxs-lookup"><span data-stu-id="5b8b1-112">**Linux operating system installed in a .vhd file** - You have installed an [Azure-endorsed Linux distribution](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (or see [information for non-endorsed distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) to a virtual disk in the VHD format.</span></span> <span data-ttu-id="5b8b1-113">Existem várias ferramentas para criar uma VM e o VHD:</span><span class="sxs-lookup"><span data-stu-id="5b8b1-113">Multiple tools exist to create a VM and VHD:</span></span>
  * <span data-ttu-id="5b8b1-114">Instalar e configurar o [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) ou o [KVM](http://www.linux-kvm.org/page/RunningKVM), tomando o cuidado de usar o VHD como seu formato de imagem.</span><span class="sxs-lookup"><span data-stu-id="5b8b1-114">Install and configure [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) or [KVM](http://www.linux-kvm.org/page/RunningKVM), taking care to use VHD as your image format.</span></span> <span data-ttu-id="5b8b1-115">Se necessário, você pode [converter uma imagem](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) usando `qemu-img convert`.</span><span class="sxs-lookup"><span data-stu-id="5b8b1-115">If needed, you can [convert an image](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) using `qemu-img convert`.</span></span>
  * <span data-ttu-id="5b8b1-116">Também pode usar o Hyper-V [no Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) ou [no Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="5b8b1-116">You can also use Hyper-V [on Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) or [on Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="5b8b1-117">Não há suporte para o formato VHDX mais recente no Azure.</span><span class="sxs-lookup"><span data-stu-id="5b8b1-117">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="5b8b1-118">Ao criar uma VM, especifique VHD como o formato.</span><span class="sxs-lookup"><span data-stu-id="5b8b1-118">When you create a VM, specify VHD as the format.</span></span> <span data-ttu-id="5b8b1-119">Se necessário, será possível converter discos VHDX para VHD usando o cmdlet [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) ou [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5b8b1-119">If needed, you can convert VHDX disks to VHD using [`qemu-img convert`](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) or the [`Convert-VHD`](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="5b8b1-120">Além disso, o Azure não dá suporte ao carregamento de VHDs dinâmicos, por isso você precisa converter esses discos para VHDs estáticos antes de carregar.</span><span class="sxs-lookup"><span data-stu-id="5b8b1-120">Further, Azure does not support uploading dynamic VHDs, so you need to convert such disks to static VHDs before uploading.</span></span> <span data-ttu-id="5b8b1-121">Você pode usar ferramentas como o [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) para converter os discos dinâmicos durante o processo de carregamento no Azure.</span><span class="sxs-lookup"><span data-stu-id="5b8b1-121">You can use tools such as [Azure VHD Utilities for GO](https://github.com/Microsoft/azure-vhd-utils-for-go) to convert dynamic disks during the process of uploading to Azure.</span></span>

* <span data-ttu-id="5b8b1-122">**Interface de Linha de Comando do Azure** : instale a [Interface de Linha de Comando do Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) mais recente para carregar o VHD.</span><span class="sxs-lookup"><span data-stu-id="5b8b1-122">**Azure Command-line Interface** - Install the latest [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) to upload the VHD.</span></span>

<span data-ttu-id="5b8b1-123"><a id="prepimage"> </a></span><span class="sxs-lookup"><span data-stu-id="5b8b1-123"><a id="prepimage"> </a></span></span>

## <a name="step-1-prepare-the-image-to-be-uploaded"></a><span data-ttu-id="5b8b1-124">Etapa 1: preparar a imagem a ser carregada</span><span class="sxs-lookup"><span data-stu-id="5b8b1-124">Step 1: Prepare the image to be uploaded</span></span>
<span data-ttu-id="5b8b1-125">O Azure dá suporte a várias distribuições do Linux (consulte [Distribuições endossadas](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="5b8b1-125">Azure supports various Linux distributions (see [Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span> <span data-ttu-id="5b8b1-126">Os seguintes artigos explicam como preparar as diversas distribuições Linux com suporte no Azure.</span><span class="sxs-lookup"><span data-stu-id="5b8b1-126">The following articles guide you through how to prepare the various Linux distributions that are supported on Azure.</span></span> <span data-ttu-id="5b8b1-127">Após concluir as etapas descritas nos guias abaixo, volte a este ponto quando tiver um arquivo VHD pronto para upload no Azure:</span><span class="sxs-lookup"><span data-stu-id="5b8b1-127">After you complete the steps in the following guides, come back here once you have a VHD file that is ready to upload to Azure:</span></span>

* <span data-ttu-id="5b8b1-128">**[Distribuições com base em CentOS](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="5b8b1-128">**[CentOS-based Distributions](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="5b8b1-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="5b8b1-129">**[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="5b8b1-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="5b8b1-130">**[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="5b8b1-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="5b8b1-131">**[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="5b8b1-132">**[SLES & openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="5b8b1-132">**[SLES & openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="5b8b1-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="5b8b1-133">**[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>
* <span data-ttu-id="5b8b1-134">**[Outros — Distribuições não endossadas](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span><span class="sxs-lookup"><span data-stu-id="5b8b1-134">**[Other - Non-Endorsed Distributions](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**</span></span>

> [!NOTE]
> <span data-ttu-id="5b8b1-135">O SLA da plataforma Azure aplica-se às máquinas virtuais que executam o sistema operacional Linux somente quando uma das distribuições endossadas é usada com os detalhes de configuração, como especificado nas “Versões com suporte” em [Linux em distribuições endossadas pelo Azure](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5b8b1-135">The Azure platform SLA applies to virtual machines running the Linux OS only when one of the endorsed distributions is used with the configuration details as specified under 'Supported Versions' in [Linux on Azure-Endorsed Distributions](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="5b8b1-136">Todas as distribuições do Linux fornecidas na galeria de imagens do Azure são distribuições endossadas com a configuração necessária.</span><span class="sxs-lookup"><span data-stu-id="5b8b1-136">All Linux distributions in the Azure image gallery are endorsed distributions with the required configuration.</span></span>
> 
> 

<span data-ttu-id="5b8b1-137">Veja também as **[Observações de instalação do Linux](../create-upload-generic.md#general-linux-installation-notes)** para obter mais dicas gerais sobre como preparar as imagens do Linux para o Azure.</span><span class="sxs-lookup"><span data-stu-id="5b8b1-137">Also see the **[Linux Installation Notes](../create-upload-generic.md#general-linux-installation-notes)** for more general tips on preparing Linux images for Azure.</span></span>

<span data-ttu-id="5b8b1-138"><a id="connect"> </a></span><span class="sxs-lookup"><span data-stu-id="5b8b1-138"><a id="connect"> </a></span></span>

## <a name="step-2-prepare-the-connection-to-azure"></a><span data-ttu-id="5b8b1-139">Etapa 2: preparar a conexão com o Azure</span><span class="sxs-lookup"><span data-stu-id="5b8b1-139">Step 2: Prepare the connection to Azure</span></span>
<span data-ttu-id="5b8b1-140">Verifique se você está usando a CLI do Azure no modelo de implantação clássico (`azure config mode asm`) e faça logon na sua conta:</span><span class="sxs-lookup"><span data-stu-id="5b8b1-140">Make sure you are using the Azure CLI in the classic deployment model (`azure config mode asm`), then log in to your account:</span></span>

```azurecli
azure login
```


<span data-ttu-id="5b8b1-141"><a id="upload"> </a></span><span class="sxs-lookup"><span data-stu-id="5b8b1-141"><a id="upload"> </a></span></span>

## <a name="step-3-upload-the-image-to-azure"></a><span data-ttu-id="5b8b1-142">Etapa 3: carregar a imagem no Azure</span><span class="sxs-lookup"><span data-stu-id="5b8b1-142">Step 3: Upload the image to Azure</span></span>
<span data-ttu-id="5b8b1-143">Você precisa de uma conta de armazenamento para carregar o arquivo do VHD.</span><span class="sxs-lookup"><span data-stu-id="5b8b1-143">You need a storage account to upload your VHD file to.</span></span> <span data-ttu-id="5b8b1-144">Você pode escolher uma conta de armazenamento existente ou [criar uma nova](../../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="5b8b1-144">You can either pick an existing storage account or [create a new one](../../../storage/common/storage-create-storage-account.md).</span></span>

<span data-ttu-id="5b8b1-145">Use a CLI do Azure para carregar a imagem utilizando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="5b8b1-145">Use the Azure CLI to upload the image by using the following command:</span></span>

```azurecli
azure vm image create <ImageName> `
    --blob-url <BlobStorageURL>/<YourImagesFolder>/<VHDName> `
    --os Linux <PathToVHDFile>
```

<span data-ttu-id="5b8b1-146">No exemplo anterior:</span><span class="sxs-lookup"><span data-stu-id="5b8b1-146">In the previous example:</span></span>

* <span data-ttu-id="5b8b1-147">**BlobStorageURL** é a URL para a conta de armazenamento que você planeja usar</span><span class="sxs-lookup"><span data-stu-id="5b8b1-147">**BlobStorageURL** is the URL for the storage account you plan to use</span></span>
* <span data-ttu-id="5b8b1-148">**YourImagesFolder** é o contêiner dentro do Armazenamento de Blobs em que você deseja armazenar as imagens</span><span class="sxs-lookup"><span data-stu-id="5b8b1-148">**YourImagesFolder** is the container within blob storage where you want to store your images</span></span>
* <span data-ttu-id="5b8b1-149">**VHDName** é o rótulo que aparece no portal para identificar o disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="5b8b1-149">**VHDName** is the label that appears in portal to identify the virtual hard disk.</span></span>
* <span data-ttu-id="5b8b1-150">**PathToVHDFile** é o caminho completo e o nome do arquivo .vhd em seu computador.</span><span class="sxs-lookup"><span data-stu-id="5b8b1-150">**PathToVHDFile** is the full path and name of the .vhd file on your machine.</span></span>

<span data-ttu-id="5b8b1-151">O comando a seguir mostra um exemplo completo:</span><span class="sxs-lookup"><span data-stu-id="5b8b1-151">The following command shows a complete example:</span></span>

```azurecli
azure vm image create myImage `
    --blob-url https://mystorage.blob.core.windows.net/vhds/myimage.vhd `
    --os Linux /home/ahmet/myimage.vhd
```

## <a name="step-4-create-a-vm-from-the-image"></a><span data-ttu-id="5b8b1-152">Etapa 4: criar uma VM da imagem</span><span class="sxs-lookup"><span data-stu-id="5b8b1-152">Step 4: Create a VM from the image</span></span>
<span data-ttu-id="5b8b1-153">Crie uma VM usando o `azure vm create` da mesma forma que faria com uma VM comum.</span><span class="sxs-lookup"><span data-stu-id="5b8b1-153">You create a VM using `azure vm create` in the same way as a regular VM.</span></span> <span data-ttu-id="5b8b1-154">Especifique o nome que você deu à imagem na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="5b8b1-154">Specify the name you gave your image in the previous step.</span></span> <span data-ttu-id="5b8b1-155">No exemplo a seguir, usamos o nome de imagem **myImage** fornecido na etapa anterior:</span><span class="sxs-lookup"><span data-stu-id="5b8b1-155">In the following example, we use the **myImage** image name given in the previous step:</span></span>

```azurecli
azure vm create --userName ops --password P@ssw0rd! --vm-size Small --ssh `
    --location "West US" "myDeployedVM" myImage
```

<span data-ttu-id="5b8b1-156">Para criar suas próprias VMs, forneça seu próprio nome de usuário + senha, localização, nome DNS e nome da imagem.</span><span class="sxs-lookup"><span data-stu-id="5b8b1-156">To create your own VMs, provide your own username + password, location, DNS name, and image name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b8b1-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5b8b1-157">Next steps</span></span>
<span data-ttu-id="5b8b1-158">Para obter mais informações, consulte [Referência da CLI do Azure para o modelo de implantação clássico do Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="5b8b1-158">For more information, see [Azure CLI reference for the Azure classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

[Step 1: Prepare the image to be uploaded]:#prepimage
[Step 2: Prepare the connection to Azure]:#connect
[Step 3: Upload the image to Azure]:#upload
